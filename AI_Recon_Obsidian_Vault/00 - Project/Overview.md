---
tags: [project]
---

# Project Overview

An AI-native pre-audit agent that autonomously matches transactions to supporting evidence and drafts the audit-defense package before a human reviews it.

## Problem

Traditional rule-based reconciliation breaks whenever invoice descriptions, exchange rates, split payments, or vendor names don't match exactly — dumping thousands of edge cases on human accountants at month-end.

## Approach

This system replaces that manual detective work with an autonomous pre-audit agent. It ingests contracts, emails, receipts, and bank logs; deduces why numbers differ (tax, shipping, FX conversion, partial shipments); cross-references internal context; and links the underlying evidence. Instead of a raw discrepancy list, it presents a pre-solved package — three disparate charges equal one invoice because of tax and shipping — ready for a one-click approve, post, and file.

See [[01 - Design/Design Specification|Design Specification]] for architecture, data model, and the agent reasoning loop.

## Team Split

| Developer | Focus | Key responsibilities |
| --- | --- | --- |
| Developer 1 | Full-Stack / Product | Next.js frontend, dashboard, application architecture, auth, billing, deployment |
| Developer 2 | Backend / Integrations | Postgres, APIs, Plaid, QuickBooks, Gmail/Outlook, webhooks, background jobs, security |
| Developer 3 | AI / Data | Document extraction, embeddings, matching algorithms, agent reasoning, confidence scoring, vendor intelligence |

## Status

Early scaffold — Next.js app with Supabase/Drizzle wired up; `document`, `reconciliation`, and `transaction` services stubbed but not yet implemented. See [[06 - Logging/Dev Log|Dev Log]] for the latest state and [[07 - Tasks/Backlog|Backlog]] for what's next.
