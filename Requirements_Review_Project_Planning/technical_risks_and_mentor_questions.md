# Legacy OFS — Technical Risks and Mentor Questions

## 1. Technical Risks and Mitigation

| Risk | Impact | Mitigation |
|---|---|---|
| Offline synchronization conflicts | Ticket changes may be stale or overwritten. | Use the agreed outbox, changes feed, mutation validation, and last-write-wins behavior. Test concurrent changes and invalid transitions. |
| Duplicate QuickBooks invoices | Duplicate billing could occur after retries or lost responses. | Use the agreed invoice lookup and idempotency approach; test interrupted requests and retries against the sandbox. |
| Device limit and revocation failures | Unauthorized or revoked devices could continue accessing the system. | Enforce the five-device limit on the server, validate sessions during sync, and test device revocation. |
| Incorrect ticket or inspection configuration | Required fields, forms, or statuses may not match the client requirements. | Use the handoff as the source of truth, add configuration count assertions, and replace placeholders when final client inputs arrive. |
| SQLite backup or restore failure | Business records could be lost after a failure. | Configure Litestream replication to Tigris and rehearse restoring the database before acceptance. |
| Large photo uploads or poor connectivity | Photo uploads may be slow or fail in the field. | Compress photos client-side, show upload progress, support retry, and test realistic mobile connections. |
| Incorrect permissions or price changes | Unauthorized changes could affect tickets or invoices. | Enforce role permissions on the server, validate ticket states, and test administrator overrides and locked invoiced tickets. |
| Unclear client decisions | Rework could delay delivery. | Record assumptions and defaults in the decisions/open-questions document and raise client questions through Jeff. |
| AI-generated duplicate mechanisms | Code could become inconsistent and difficult to maintain. | Keep one shared mutation/write path, review PRs for DRY and SOLID, and test common logic. |
| Scope expansion | Optional features could delay the core release. | Follow the milestone order and do not implement explicitly excluded features without approval. |

## 2. Dependencies to Confirm

- Repository access and the official provisioning checklist.
- Node.js 22 and the required development environment.
- Fly.io organization and staging deployment access.
- Tigris storage and Litestream backup configuration.
- QuickBooks Online sandbox credentials and API configuration.
- Final client ticket templates, field definitions, inspection forms, catalog information, logo, and branding assets.
- GitHub Actions and any required deployment secrets.

## 3. Questions for Jeff / Client

The handoff already records proposed defaults for these items. Confirm them through Jeff when convenient; do not block implementation unnecessarily.

| Question | Current documented default |
|---|---|
| Are additional ticket statuses needed, such as In Progress or Disputed? | Draft, Submitted, Approved, Rejected, Invoiced, and Void. |
| Should Field Workers be allowed to see line prices? | They can see prices but cannot edit them. |
| Can Field Workers edit tickets after submission? | Field Workers edit Draft or Rejected tickets; Admins can edit Submitted or Approved tickets; Invoiced tickets are locked. |
| How many accounts are required, and should there be one shared crew login or separate logins per crew? | Accounts are provisioned by script; the current assumption is `crew` and `office`. |
| Is a particular ticket-number format required? | Server assigns the ticket number on first sync, using a format such as `T-000123`. |
| Should a batch invoice create one invoice per ticket or group tickets by customer? | The user chooses the grouping for each batch; no per-customer grouping setting is included in the lean MVP. |
| Should the invoice date be the ticket work date or the date the invoice is sent? | Single-ticket invoices use the work date; batch invoices use the current date. |
| Should comments appear on customer-facing ticket PDFs? | Comments print only when an Admin enables the option. |
| Should customer-facing PDFs show unit prices or only totals? | The current handoff assumes unit prices and totals. |
| When will the five actual ticket templates, inspection forms, and field definitions be supplied? | Placeholder configurations are used until the client provides the real versions. |
| Will the client provide a custom domain? | The documented default is the proposed Fly.io domain. |

## 4. Questions to Resolve Internally Before Implementation

- Who owns the shared mutation/write path and offline synchronization module?
- Who is responsible for staging deployment and reviewing database migrations?
- How will the team divide frontend, backend, QuickBooks, and testing tasks?
- Where will the team record test results, staging demonstrations, and changes to decisions?
- Which milestone is currently approved to begin, and what is the expected delivery date?

## 5. Scope Reminders

The following are explicitly out of scope: graphical form builder, in-app email, equipment/inventory management, general dashboards, ticket photos, inspection-to-ticket automation, signatures, native mobile apps, QuickBooks Desktop, multi-tenant support, GPS, and push/SMS/email notifications.

The optional offline creation of a brand-new inspection should be attempted only if time remains after the required work.

