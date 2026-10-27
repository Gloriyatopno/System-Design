# Legacy OFS — Initial Feature Checklist



## 1. Authentication and Device Management
- [ ] Implement login and role-based access for Field Workers and Administrators.
- [ ] Support shared accounts and individual device naming.
- [ ] Enforce a maximum of five active devices per account.
- [ ] Provide administrator device listing and revocation.

## 2. Field Ticket Management
- [ ] Obtain and configure the five approved ticket templates.
- [ ] Implement ticket creation, editing, and required-field validation.
- [ ] Capture customer details, work dates, and custom fields.
- [ ] Support service/material line items, quantities, and prices.
- [ ] Support ticket comments and status tracking.
- [ ] Implement Draft, Submitted, Approved, Rejected, Invoiced, and Void states.
- [ ] Implement administrator search, filtering, review, approval, and rejection.

## 3. Offline Functionality
- [ ] Store ticket data locally.
- [ ] Support offline ticket creation, editing, comments, and submission.
- [ ] Persist pending synchronization actions.
- [ ] Synchronize pending changes after reconnection.
- [ ] Display pending, successful, and failed synchronization states.
- [ ] Handle retries, duplicate actions, and conflicting changes.

## 4. QuickBooks Online
- [ ] Configure authorized QuickBooks Online connectivity.
- [ ] Synchronize customer information.
- [ ] Synchronize item information.
- [ ] Implement administrator catalog management and default prices.
- [ ] Generate invoices from approved tickets.
- [ ] Support batch invoicing.
- [ ] Handle API errors, retries, and duplicate-invoice prevention.

## 5. Inspections
- [ ] Obtain the approved sample inspection form and configuration format.
- [ ] Load configurable inspection forms without building a form-builder interface.
- [ ] Support sections, question types, and required fields.
- [ ] Capture photos, comments, and observations as required.
- [ ] Save inspection responses reliably.
- [ ] Generate branded inspection PDFs containing required details, answers, and photos.

## 6. Reports and Administration
- [ ] Generate downloadable ticket PDFs.
- [ ] Export filtered ticket records to Excel.
- [ ] Implement the remaining required administrative functions.
- [ ] Verify report accuracy and permissions.

## 7. Testing and Delivery
- [ ] Write unit tests.
- [ ] Write API and database integration tests.
- [ ] Write end-to-end workflow tests.
- [ ] Test mobile browser and PWA behavior.
- [ ] Test offline workflows, reconnection, and synchronization failures.
- [ ] Test QuickBooks errors and duplicate prevention.
- [ ] Document environment setup and configuration.
- [ ] Document deployment, testing, and known limitations.

## MVP Planning

The initial implementation should prioritize a working end-to-end ticket workflow, including authentication, ticket creation, persistence, submission, administrative review, and offline synchronization.

Inspection workflows, QuickBooks invoicing, and reporting must also be included in the agreed project scope. Their exact milestone placement should be confirmed with the mentor rather than treating them as optional or excluded features.


