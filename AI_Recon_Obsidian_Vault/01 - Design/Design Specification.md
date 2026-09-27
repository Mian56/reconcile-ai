---
tags: [design]
date: 2026-09-27
author: Hassan
---

# AI Financial Reconciliation SaaS — Design Specification

Sep 27, 2026 · @Hassan

An AI-native pre-audit agent that autonomously matches transactions to supporting evidence and drafts the audit-defense package before a human reviews it.

## Overview

Traditional rule-based reconciliation breaks whenever invoice descriptions, exchange rates, split payments, or vendor names don't match exactly — dumping thousands of edge cases on human accountants at month-end.

This system replaces that manual detective work with an autonomous pre-audit agent. It ingests contracts, emails, receipts, and bank logs; deduces why numbers differ (tax, shipping, FX conversion, partial shipments); cross-references internal context; and links the underlying evidence. Instead of a raw discrepancy list, it presents a pre-solved package — three disparate charges equal one invoice because of tax and shipping — ready for a one-click approve, post, and file.

## System Architecture

6 components · Inngest orchestrates matching jobs.

Backend/API handles synchronous reads and writes; Inngest owns everything async — pulling from external integrations, triggering the AI matching engine, and writing results back to the database.

See [[02 - Backend/Overview|Backend Overview]] for implementation notes.

## Data Model

The schema centers on match *groups* (N:M), not 1:1 pairs, so a set of transactions can reconcile against a set of documents with a justified residual.

| Entity | Purpose | Key fields |
| --- | --- | --- |
| `transactions` | Raw bank/ledger transactions from Plaid or manual import | amount, date, currency, account_id, org_id, status |
| `documents` | Uploaded or synced invoices, receipts, contracts, emails | file_url, extracted_text, embedding (pgvector), org_id |
| `match_groups` | N:M link between one or more transactions and one or more documents | id, status, confidence_score, residual_amount, org_id |
| `match_group_items` | Join table: which transactions/documents belong to a group | match_group_id, item_type, item_id |
| `evidence_links` | The specific evidence cited for a match — a contract clause, an email line, a receipt row | match_group_id, source_document_id, excerpt, locator |
| `reasoning_traces` | The agent's structured explanation: tool calls made and the arithmetic that closed the gap | match_group_id, steps (jsonb), tool_calls (jsonb) |
| `audit_records` | Immutable record of the human decision | match_group_id, decision, decided_by, decided_at, packet_url |

See [[02 - Backend/Data Model|Data Model detail]] for schema/migration notes as they land.

## Agent Reasoning Loop

Candidate retrieval → tool calls → gap check, looping until explained.

pgvector similarity search surfaces candidates; the agent then calls structured sub-tools — an FX-rate lookup, a tax-rule check, a contract-terms extractor — and reconciles the arithmetic itself. An unexplained gap re-runs retrieval with a wider net rather than surfacing the raw discrepancy to a human.

## Audit Packet

The packet is the actual deliverable — not a byproduct of the match, but a generated, versioned document bundling everything an auditor would ask for.

| Field | Contents |
| --- | --- |
| Matched transactions | Every transaction row included in the match group |
| Matched evidence | Document excerpts, contract clauses, email threads cited, each with a locator |
| Reasoning trace | Step-by-step explanation, including which sub-tools were called and the arithmetic that closed the gap |
| Confidence score | The model's confidence in the proposed match |
| Residual explanation | Any unexplained variance and why it was accepted |
| Human decision | Approve/reject, decided by whom, timestamp |
| Immutability | Versioned once approved — amendments create a new linked record, never overwrite |

## Core V1 Workflow

4 stages · accountant reviews before the trail closes.

1. Connect/import transactions and upload or connect invoices and receipts.
2. The agent finds supporting evidence and explains the match with a confidence score.
3. The accountant approves or rejects.
4. The decision and evidence are stored in the audit trail either way.

See [[07 - Tasks/Backlog|Backlog]] for how this workflow breaks down into shippable tasks.

## Team Split

| Developer | Focus | Key responsibilities |
| --- | --- | --- |
| Developer 1 | Full-Stack / Product | Next.js frontend, dashboard, application architecture, auth, billing, deployment |
| Developer 2 | Backend / Integrations | Postgres, APIs, Plaid, QuickBooks, Gmail/Outlook, webhooks, background jobs, security |
| Developer 3 | AI / Data | Document extraction, embeddings, matching algorithms, agent reasoning, confidence scoring, vendor intelligence |
