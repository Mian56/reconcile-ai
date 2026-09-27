---
tags: [backend]
---

# Backend Overview

Owner: Developer 2 (Backend / Integrations). See [[00 - Project/Overview|Team Split]].

## Responsibilities

- Postgres schema + migrations (Drizzle ORM, Supabase-hosted)
- Synchronous API routes (reads/writes)
- Inngest for everything async: pulling from external integrations, triggering the AI matching engine, writing results back to the database
- Integrations: Plaid, QuickBooks, Gmail/Outlook
- Webhooks, background jobs, security

## Current code

- `src/db/index.ts` — DB client (stub, not yet implemented)
- `src/services/transaction.service.ts` — transaction ingestion (stub)
- `src/services/document.service.ts` — document ingestion (stub)
- `src/services/reconciliation.service.ts` — match-group orchestration (stub)

## Related

- [[01 - Design/Design Specification|Design Specification]] — full system architecture
- [[02 - Backend/Data Model|Data Model]]
