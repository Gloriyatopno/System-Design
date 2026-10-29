# Architecture Review Notes — Legacy OFS

**Date:** 19 October 2026  
**Topic:** Capstone Progress & Architecture Review

## 1. Architectural Approach

Legacy OFS uses a single-package TypeScript application with a React Progressive Web App, a Hono backend, and SQLite persistence. The architecture is designed to keep deployment and maintenance simple while supporting mobile ticketing, offline work, administration, invoicing, and inspections.

## 2. Frontend Responsibilities

The React application provides separate workflows for Field Workers and Admins.

Field Workers create tickets, add comments and line items, and submit work. Admins search and review tickets, manage devices and catalog entries, approve or reject submissions, and generate exports.

TanStack Router handles client-side routing, and TanStack Query is used for reads. Writes to tickets, lines, comments, and statuses must use the outbox module rather than independent query mutations.

## 3. Offline Storage and Synchronization

Dexie stores the local data mirror and mutation outbox in IndexedDB. User actions are queued locally before the server receives them.

When connectivity returns:

1. The client sends queued mutations to `POST /api/mutations`.
2. The server validates the request using the shared Zod schemas.
3. `applyMutation.ts` applies permitted changes to SQLite.
4. The client pulls server changes through `GET /api/changes?since=`.
5. The local mirror is refreshed and pending or failed changes are displayed to the user.

The implementation must handle retries, duplicate mutation IDs, invalid status transitions, revoked devices, and stale data according to the handoff.

## 4. Backend and Database

Hono serves the API and the built frontend. Authentication middleware validates the per-device session token and attaches the account and device context to requests.

Drizzle ORM defines the SQLite schema and migrations. The database uses `better-sqlite3` and WAL mode.

The shared folder contains configuration, Zod schemas, types, status rules, and integer-cent money helpers. Shared code must not import from the server or client layers.

A single `applyMutation.ts` module is responsible for ticket-related writes. This avoids having different endpoints implement conflicting write logic.

## 5. QuickBooks Online Integration

The backend communicates with QuickBooks Online through its Accounting API v3 using OAuth token handling.

The integration synchronizes customers and items, supports catalog mappings, and creates invoices from approved tickets. The implementation must prevent duplicate invoices when requests are retried and must record useful integration results and errors.

Testing should begin with the QuickBooks sandbox. Production credentials must only be used when authorized.

## 6. PDF, Excel, and Object Storage

- `@react-pdf/renderer` generates ticket and inspection PDFs server-side.
- SheetJS generates real `.xlsx` exports from filtered ticket data.
- Tigris stores photos, cached PDFs, and replicated backups as specified by the handoff.
- Litestream continuously replicates SQLite backups to Tigris.

## 7. Hosting and Operations

The prescribed deployment is a single Node.js 22 application on Fly.io, in the Dallas region, using a persistent Fly volume for SQLite.

The design includes a health endpoint, monitoring, continuous backup replication, and a documented restoration procedure. The team must demonstrate that backups can actually be restored before acceptance.

## 8. Technical Trade-offs

| Decision | Benefit | Trade-off |
|---|---|---|
| SQLite instead of a managed database | Low operating cost and simple backup model | Requires careful single-machine and volume management |
| PWA instead of native mobile apps | One application for phone and laptop workflows | Browser storage and mobile browser behavior require testing |
| Dexie outbox | Supports ticket work without connectivity | Synchronization and error recovery add complexity |
| Shared accounts with device identity | Matches the client's requested workflow | Requires strong device registration, revocation, and auditing |
| Configuration-based forms | Simple, controlled templates without a form builder | Template changes require code changes and deployment |
| One server write path | Consistent validation and state transitions | All ticket-writing behavior must use the shared mutation mechanism |

