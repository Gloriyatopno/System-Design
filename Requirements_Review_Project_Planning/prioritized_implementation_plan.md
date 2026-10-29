# Legacy OFS — Prioritized Implementation Plan

## 1. Planning Objective

Break the agreed project scope into manageable milestones, implement dependencies in the correct order, and demonstrate working features regularly.

The official build plan targets:
- A releasable online ticketing application on staging by the end of Week 2.
- Offline ticketing by Week 3.
- QuickBooks invoicing by Week 4.
- Inspections by Week 5.
- Final templates, real QuickBooks configuration, backup/restore rehearsal, and the client walkthrough in Week 6.

These are planning targets, not a guarantee; a single developer may need more time than a team of two or three.

## 2. Milestone 0 — Project Foundation (Day 1)

**Priority:** P1

### Tasks
1. Set up the repository and Node.js 22 environment.
2. Initialize the single-package project with TypeScript, Vite, React, Tailwind CSS, and shadcn/ui.
3. Set up the Hono server and health endpoint.
4. Define the agreed SQLite schema with Drizzle ORM.
5. Generate and commit database migrations.
6. Configure Fly.io staging, the application volume, and deployment settings.
7. Implement account seeding, login, device naming, authentication middleware, and device-list endpoints.
8. Configure the initial GitHub Actions workflow.

### Dependencies
- Access to the repository and required hosting configuration.
- Environment variables and secrets.
- Confirmation that the project setup follows the official provisioning checklist.

### Completion criteria
- Staging displays the login page.
- A Field Worker can sign in and name a device.
- The device limit is enforced.
- A revoked device is denied access.
- The application health endpoint works.

## 3. Milestone 1 — Online Ticketing and Catalog (Weeks 1–2)

**Priority:** P1

### Tasks
1. Configure ticket templates, fields, lists, and statuses.
2. Define shared mutation schemas.
3. Implement the single write path through `POST /api/mutations`.
4. Implement `GET /api/changes` and the local Dexie mirror.
5. Build the Field Worker ticket interface.
6. Build the Admin ticket grid and review interface.
7. Implement catalog editing and customer/item selection.
8. Add ticket PDF generation and Excel exports.
9. Add the initial QuickBooks catalog synchronization.
10. Add unit and server integration tests for the implemented features.

### Dependencies
- Milestone 0 authentication and database.
- Confirmed ticket data model and placeholder templates.
- Shared mutation and synchronization contracts.

### Completion criteria
- Users can create, save, submit, review, approve, reject, and void tickets as permitted.
- Admins can search and filter tickets.
- Ticket PDFs and Excel exports work.
- The online workflow is demonstrated on staging using a phone.

## 4. Milestone 2 — Offline Ticketing (Week 3)

**Priority:** P1

### Tasks
1. Add the local mutation outbox.
2. Add service-worker support for the PWA.
3. Queue ticket changes while offline.
4. Replay queued mutations when connectivity returns.
5. Display pending and failed synchronization states.
6. Implement retry handling, duplicate prevention, and conflict behavior.
7. Handle device revocation and local schema-version changes safely.
8. Test the complete offline workflow on an iPhone and Android phone.

### Dependencies
- The online mutation endpoint and Dexie mirror from Milestone 1.
- Agreed mutation schemas and server-side status validation.

### Completion criteria
- Field workers can create, edit, comment on, and submit tickets offline.
- Queued changes synchronize after reconnection.
- The application reports pending and failed changes clearly.
- Tests cover stale data, retries, revoked devices, and duplicate mutations.

## 5. Milestone 3 — QuickBooks Invoicing (Week 4)

**Priority:** P2

### Tasks
1. Complete the QuickBooks Online connection and token-refresh flow.
2. Map application customers and catalog items to QuickBooks records.
3. Push approved tickets as invoices.
4. Support single-ticket and batch invoicing.
5. Prevent duplicate invoices after retries or lost responses.
6. Log successes and failures and provide actionable error messages.
7. Test unmapped items, inactive customers, token refresh, and invoice grouping.

### Dependencies
- Approved-ticket workflow.
- QuickBooks sandbox access and configuration.
- Stable customer and item mappings.

### Completion criteria
- Approved tickets can produce invoices in the sandbox.
- Unit prices and overrides are preserved.
- Batch invoicing follows the selected grouping option.
- Repeated or retried requests do not create duplicate invoices.

## 6. Milestone 4 — Inspections (Week 5)

**Priority:** P3

### Tasks
1. Configure the predefined inspection forms.
2. Implement section-by-section online form completion.
3. Add question validation and draft saving.
4. Support photo upload and client-side compression.
5. Store photo objects and inspection metadata.
6. Generate branded inspection PDFs.
7. Implement completion locking and administrative reopening.
8. Test inspection forms and generated reports.

### Dependencies
- Approved inspection configuration.
- Logo and branding assets.
- Object-storage configuration.
- Confirmed PDF layout and photo requirements.

### Completion criteria
- Users can complete the configured forms online.
- Photos appear correctly in inspection PDFs.
- Completed forms are locked as specified.
- The optional offline-creation behavior is attempted only if time remains after required features.

## 7. Milestone 5 — Finalization and Acceptance (Week 6)

**Priority:** P1/P2 across release requirements

### Tasks
1. Replace placeholder templates and forms with the final supplied client versions.
2. Configure and verify the real QuickBooks company connection.
3. Run the complete unit, integration, end-to-end, and real-device tests.
4. Perform the backup and restore rehearsal.
5. Verify monitoring, security configuration, and data export.
6. Review documentation, environment setup, and deployment procedures.
7. Demonstrate the ticketing, invoicing, and inspection workflows.
8. Document remaining issues and decisions.

### Completion criteria
- Required acceptance scenarios pass.
- Backup restoration is demonstrated and recorded.
- The application is documented and deployable.
- Jeff and the client can review the working application against the agreed scope.

## 8. Working Method

For each feature:

1. Read the relevant handoff requirement.
2. Identify dependencies and acceptance criteria.
3. Use AI coding tools to implement a small, focused change.
4. Review the code for duplication, maintainability, naming, and security.
5. Run the relevant tests and record their actual results.
6. Submit a pull request with a clear description and testing summary.
7. Demonstrate the feature on staging when the milestone requires it.
8. Record decisions, unresolved questions, and scope changes.



