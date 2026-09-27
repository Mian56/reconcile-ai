---
tags: [tasks, backlog]
---

# Backlog

Derived from the [[01 - Design/Design Specification#Core V1 Workflow|Core V1 Workflow]]. Copy [[99 - Templates/Task Template|Task Template]] for a new task note when one needs its own detail.

## Not started

- [ ] Define Drizzle schema for `transactions`, `documents`, `match_groups`, `match_group_items`, `evidence_links`, `reasoning_traces`, `audit_records` — Dev 2
- [ ] Plaid integration for transaction import — Dev 2
- [ ] Manual transaction import (CSV) — Dev 2
- [ ] Document upload + storage (invoices, receipts, contracts, emails) — Dev 2
- [ ] pgvector embedding pipeline for uploaded documents — Dev 3
- [ ] Agent reasoning loop: candidate retrieval → tool calls → gap check — Dev 3
- [ ] Sub-tools: FX-rate lookup, tax-rule check, contract-terms extractor — Dev 3
- [ ] Confidence scoring — Dev 3
- [ ] Audit packet generation (versioned document) — Dev 3 / Dev 2
- [ ] Dashboard: review queue, match detail view, approve/reject — Dev 1
- [ ] Auth + billing — Dev 1
- [ ] Inngest job orchestration wiring — Dev 2

## In progress

_(none)_

## Done

- [x] Design specification drafted
- [x] Next.js scaffold + Supabase/Drizzle deps added
