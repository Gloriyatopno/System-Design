# Legacy OFS — Proposed System Architecture


## Architecture Diagram

```mermaid
flowchart TB
    subgraph Client["Client Devices"]
        UI["React 18 + Vite SPA"]
        PWA["PWA Service Worker"]
        LOCAL["Dexie / IndexedDB"]
        OUTBOX["Local Mutation Outbox"]
        UI <--> LOCAL
        UI --- PWA
        LOCAL --- OUTBOX
    end

    subgraph Server["Single Node.js 22 Application on Fly.io"]
        API["Hono API + Authentication"]
        VALIDATE["Shared Zod Mutation Validation"]
        APPLY["applyMutation.ts<br/>Single Write Path"]
        FEED["Changes Feed"]
        DB["SQLite + Drizzle ORM<br/>better-sqlite3 / WAL"]
        PDF["Server-side PDF Generation<br/>@react-pdf/renderer"]
        XLSX["Excel Export<br/>SheetJS"]
        QBO["QuickBooks Integration<br/>OAuth + REST"]
        API --> VALIDATE
        VALIDATE --> APPLY
        APPLY --> DB
        DB --> FEED
        API --> PDF
        API --> XLSX
        API --> QBO
        QBO <--> DB
    end

    OUTBOX -->|"POST /api/mutations"| API
    FEED -->|"GET /api/changes?since="| LOCAL

    QBO <-->|"OAuth 2.0 + Accounting API"| QUICKBOOKS["QuickBooks Online"]

    DB --> BACKUP["Litestream"]
    BACKUP --> STORAGE["Tigris Backup Storage"]
    API -->|"Photos and stored objects"| STORAGE

    UI -->|"HTTPS API requests"| API
```

## Component Responsibilities

| Component | Responsibility |
|---|---|
| React, Vite, Tailwind CSS, shadcn/ui | User interface for Field Workers and Admins |
| PWA service worker | Caches the application shell and supports installation |
| Dexie / IndexedDB | Local data mirror and offline mutation outbox |
| Zod schemas | Shared validation rules for client mutations and server ingestion |
| Hono | API endpoints, authentication middleware, and request handling |
| `applyMutation.ts` | The single server-side write path for ticket-related mutations |
| SQLite, Drizzle ORM, better-sqlite3 | Persistent relational data and database migrations |
| Changes feed | Returns server-side changes for client synchronization |
| QuickBooks integration | Customer/item synchronization and invoice creation |
| PDF generation | Produces branded ticket and inspection PDFs |
| SheetJS | Generates Excel exports |
| Litestream and Tigris | Database backup replication and object storage |

