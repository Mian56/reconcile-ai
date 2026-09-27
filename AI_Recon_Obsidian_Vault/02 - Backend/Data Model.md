---
tags: [backend, data-model]
---

# Data Model

Canonical definition lives in [[01 - Design/Design Specification|Design Specification]]; this note tracks implementation status against it.

The schema centers on match *groups* (N:M), not 1:1 pairs, so a set of transactions can reconcile against a set of documents with a justified residual.

| Entity | Purpose | Key fields | Implemented? |
| --- | --- | --- | --- |
| `transactions` | Raw bank/ledger transactions from Plaid or manual import | amount, date, currency, account_id, org_id, status | ☐ |
| `documents` | Uploaded or synced invoices, receipts, contracts, emails | file_url, extracted_text, embedding (pgvector), org_id | ☐ |
| `match_groups` | N:M link between one or more transactions and one or more documents | id, status, confidence_score, residual_amount, org_id | ☐ |
| `match_group_items` | Join table: which transactions/documents belong to a group | match_group_id, item_type, item_id | ☐ |
| `evidence_links` | The specific evidence cited for a match | match_group_id, source_document_id, excerpt, locator | ☐ |
| `reasoning_traces` | The agent's structured explanation | match_group_id, steps (jsonb), tool_calls (jsonb) | ☐ |
| `audit_records` | Immutable record of the human decision | match_group_id, decision, decided_by, decided_at, packet_url | ☐ |

No Drizzle schema or migrations exist yet — `src/db/index.ts` is currently an empty stub.
