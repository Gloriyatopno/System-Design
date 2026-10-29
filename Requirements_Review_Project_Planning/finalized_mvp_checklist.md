# Legacy OFS — Finalized MVP Checklist


## 1. MVP Objective

Deliver a lean, single-tenant field-service application for Legacy Crane Solutions that supports field tickets, offline ticket operations, QuickBooks Online invoicing, and online inspections.

The MVP must follow the official project handoff. Features explicitly marked out of scope must not be added without approval.

## 2. Priority Levels

- **P1 — Essential foundation:** Required for the core application and secure operation.
- **P2 — Required supporting features:** Needed for a complete operational release, reporting, monitoring, or administration.
- **P3 — Later milestone within the agreed scope:** Planned after the core ticketing workflow; not a reason to expand the initial build unnecessarily.

These labels summarize implementation order. They do not remove requirements from the agreed scope.

## 3. Foundation and Security — P1

- [ ] Set up the prescribed Node.js and TypeScript project structure.
- [ ] Configure Vite, React, Tailwind CSS, shadcn/ui, and Hono.
- [ ] Set up SQLite and Drizzle ORM with the agreed schema.
- [ ] Configure staging deployment on Fly.io and the health endpoint.
- [ ] Implement authentication using Argon2id password hashing.
- [ ] Implement sessions and device registration with device names.
- [ ] Enforce a maximum of five concurrent active devices per account.
- [ ] Provide device listing and revocation.
- [ ] Record the acting device on every write.
- [ ] Apply Field Worker and Admin role permissions.
- [ ] Keep secrets out of the repository and configure HTTPS.

## 4. Ticket Management — P1

- [ ] Configure five ticket templates and their fields in code/configuration.
- [ ] Provide customer selection and a configurable service/material catalog.
- [ ] Support line items, quantities, default prices, and administrator price overrides.
- [ ] Allow ticket creation, draft saving, editing, comments, and submission.
- [ ] Implement Draft, Submitted, Approved, Rejected, Invoiced, and Void states.
- [ ] Provide administrator search, filtering, ticket review, approval, rejection, and voiding.
- [ ] Preserve ticket history and device information.
- [ ] Generate downloadable ticket PDFs with the agreed branding and layout.
- [ ] Export filtered ticket data to Excel.
- [ ] Validate required fields on submission while allowing incomplete drafts to be saved.

## 5. Offline Ticketing and Synchronization — P1

- [ ] Use Dexie/IndexedDB for the local ticket mirror.
- [ ] Implement the shared mutation schemas and a single write path.
- [ ] Implement the server mutation endpoint and changes feed.
- [ ] Add an outbox to queue offline changes.
- [ ] Synchronize queued changes when connectivity returns.
- [ ] Display pending changes and synchronization errors.
- [ ] Handle retries, duplicate mutation IDs, stale data, and invalid status transitions.
- [ ] Support the agreed last-write-wins behavior.
- [ ] Warn users before a local schema-version change removes pending local work.
- [ ] Test offline creation, editing, comments, submission, and synchronization on real phones.

## 6. QuickBooks Online Integration — P2

- [ ] Configure the QuickBooks Online connection and token handling.
- [ ] Synchronize customers and items for ticket selection.
- [ ] Manage the service/material catalog and default prices.
- [ ] Map application catalog items to QuickBooks items.
- [ ] Push approved tickets as invoices.
- [ ] Support batch invoicing using the agreed grouping options.
- [ ] Prevent duplicate invoices, including when a request succeeds but its response is lost.
- [ ] Record integration outcomes and provide useful error messages.
- [ ] Test integration against the QuickBooks sandbox before connecting the real company.

## 7. Reports, Administration, and Operations — P2

- [ ] Provide server-side ticket search and filtering.
- [ ] Provide the device management and catalog administration screens.
- [ ] Generate Excel exports with the agreed ticket and line-item sheets.
- [ ] Provide an application data-export procedure.
- [ ] Configure health checks and basic monitoring.
- [ ] Configure continuous SQLite backups using Litestream and Tigris.
- [ ] Test database restoration and document the procedure.
- [ ] Pin dependencies and check for known dependency vulnerabilities.

## 8. Inspections — P3

- [ ] Configure up to ten inspection forms, with no more than fifty questions in total.
- [ ] Group questions into sections and support the specified question types.
- [ ] Validate required answers, number ranges, and dates.
- [ ] Allow draft saving and completion of inspection forms online.
- [ ] Attach and compress photos client-side.
- [ ] Store photos in the agreed object storage.
- [ ] Generate branded inspection PDFs with answers and photo grids.
- [ ] Lock completed inspections and allow administrators to reopen them.
- [ ] Treat offline creation of a brand-new inspection as optional, only if time remains after the required work.

## 9. Testing and Acceptance — Required Across All Milestones

- [ ] Unit tests with Vitest.
- [ ] Server integration tests using a temporary SQLite database.
- [ ] Playwright end-to-end tests for the principal ticket workflow.
- [ ] Offline synchronization tests on an iPhone and Android phone.
- [ ] QuickBooks sandbox tests, including duplicate-prevention scenarios.
- [ ] A documented backup and restore rehearsal.
- [ ] GitHub Actions for tests and deployment to staging after successful checks.
- [ ] A phone-based staging demonstration at the end of each milestone.
- [ ] A short written progress note for Jeff covering working features, known gaps, and changes to the decisions/open-questions document.

## 10. Explicitly Out of Scope

Do not add these to the MVP without an approved scope change:

- Graphical form-builder UI.
- In-app email or email notifications.
- Equipment and inventory management.
- Dashboards and general reporting beyond the specified exports.
- Photos attached to tickets.
- Inspection-to-ticket automation.
- Electronic signatures.
- Data migration/import.
- Native mobile applications.
- A price book or pricing-rules engine.
- QuickBooks Desktop.
- General multi-tenant support or individual identities for each worker.
- Push, SMS, or email notifications.
- Customer portal, email approvals, time tracking, or GPS.
- Carrying queued changes across local-schema versions.

