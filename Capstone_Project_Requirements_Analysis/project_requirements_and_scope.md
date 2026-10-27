# Legacy OFS — Project Requirements and Scope


## 1. Project Overview

Legacy OFS is a mobile-friendly web application for an oilfield services company. It will manage field tickets, service work, inspections, maintenance-related records, reporting, and invoice generation.

The application must support field workers operating in locations with unreliable internet connectivity while providing administrators with tools to manage devices, review tickets, configure catalogs, and oversee business operations.

## 2. Problem Statement

Field operations require reliable recording of work details, customer information, materials, service quantities, inspections, and approvals. An application that depends entirely on continuous internet access may interrupt field work. Manual processes can also make it difficult to track ticket status, maintain consistent records, and prepare invoices.

The proposed application will centralize these activities, support offline ticket workflows, provide configurable inspection forms, and integrate approved tickets with QuickBooks Online.

## 3. Project Objectives

- Provide secure access for Field Workers and Administrators.
- Support creation, editing, submission, review, and approval of field tickets.
- Enable ticket creation and editing while offline.
- Synchronize pending changes when connectivity returns.
- Manage inspection forms, answers, photos, and observations.
- Synchronize customer and item information with QuickBooks Online.
- Generate invoices from approved tickets without creating duplicates.
- Generate ticket PDFs, inspection PDFs, and Excel exports.
- Provide maintainable, tested, and documented application functionality.

## 4. Intended Users

### Field Worker
- Log in and use an authorized device.
- Create and edit field tickets.
- Enter customer details, work information, line items, and comments.
- Save and submit tickets, including offline submissions queued for synchronization.
- Complete inspection forms and capture required photos.

### Administrator
- Review and revoke registered devices.
- Search, filter, review, approve, reject, and manage tickets.
- Configure service and material catalogs and default prices.
- Manage inspection configuration files as specified.
- Manage QuickBooks synchronization and invoicing workflows.
- Access reports, PDFs, and filtered Excel exports.

## 5. Functional Requirements

### Authentication and Device Management
- Support Field Worker and Administrator roles.
- Support shared accounts with individual device naming.
- Enforce a maximum of five active devices per account.
- Allow administrators to view and revoke devices.

### Field Ticket Management
- Support five configurable ticket templates.
- Capture customer details, work dates, custom fields, line items, quantities, prices, and comments.
- Track Draft, Submitted, Approved, Rejected, Invoiced, and Void statuses.
- Provide administrative search, filtering, review, and approval.

### Offline Functionality
- Support offline ticket creation, editing, comments, and submission.
- Store pending operations locally.
- Synchronize when connectivity returns.
- Display pending and failed operations and handle synchronization errors.

### QuickBooks Online
- Synchronize customer and item information.
- Manage service/material catalogs and default prices.
- Generate invoices from approved tickets and support batch invoicing.
- Handle errors and prevent duplicate invoices.

### Inspections
- Load configurable forms from configuration files rather than a form-builder interface.
- Support sections, question types, required fields, photos, comments, and observations as specified.
- Include a sample oil-well equipment condition report.
- Generate branded inspection PDFs.

### Reports and Administration
- Generate downloadable ticket PDFs.
- Export filtered ticket data to Excel.
- Provide the required administrative functions.

### Quality and Delivery
- Implement unit, integration, and end-to-end tests.
- Test mobile usability and offline workflows.
- Follow the prescribed architecture and technology stack.
- Maintain setup instructions, implementation notes, and deployment documentation.

## 6. Scope Boundaries

### In scope
All features explicitly listed in the assigned project brief, including offline functionality, QuickBooks integration, inspections, reporting, administration, testing, deployment, and documentation.

### Not yet defined
- Final ticket-template fields and validation rules.
- Final inspection questions and form configurations.
- Branding assets and final report layouts.
- Exact deployment environment and production configuration.
- Detailed synchronization conflict-resolution rules.

These items must be confirmed using the official architecture and handoff documents and client inputs.

### Out of scope unless approved
Any additional features or technology changes not specified in the project requirements.

## 7. Technology Constraints

The assigned stack includes TypeScript, Node.js, Hono, React, Vite, Tailwind CSS, SQLite, Drizzle ORM, Dexie, Progressive Web App (PWA) support, QuickBooks Online APIs, and the specified PDF and Excel libraries.

The architecture document must be reviewed before finalizing component responsibilities, database deployment, libraries, or implementation decisions.

## 8. Expected Deliverables

- Requirements and scope documentation.
- Initial feature checklist.
- Project task breakdown and implementation milestones.
- High-level architecture and data-flow documentation.
- Risk register, testing strategy, and acceptance criteria.
- Implemented application and required integrations.
- Automated tests, deployment, setup instructions, and project documentation.

## 9. Initial Assumptions

- The project brief describes the required capabilities but does not provide all final client-specific configuration.
- Sample ticket templates and inspection forms are placeholders until approved inputs arrive.
- The prescribed architecture and technology stack take precedence over personal technology preferences.
- Implementation estimates and milestones remain provisional until dependencies and the delivery schedule are confirmed.

## 10. Success Criteria

The project will be considered successful when the approved requirements are implemented, authorized users can complete their workflows, offline operations synchronize reliably, invoices are not duplicated, reports contain the required information, and the application passes the agreed tests and deployment checks.

