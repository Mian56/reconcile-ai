---
tags: [ai-agent, meta]
---

# AI agent instructions — working in this vault

Context for any AI model or coding assistant (Claude, GPT, Gemini, or otherwise) working across the `reconcile-ai` repo and this vault together. Read this file first before making changes in either the repo or the vault.

Note for tooling: this file follows the filename convention some AI coding tools look for automatically (`CLAUDE.md`, `AGENTS.md`, etc.). If your tool expects a different filename, treat this file as that file — the content below is not Claude-specific.

## What this vault is

Project notes for the AI Financial Reconciliation SaaS, kept separately from the codebase so design decisions, backend/frontend notes, bugs, reviews, and tasks don't clutter the repo itself. The repo's `README.md` stays focused on running the app; deeper context lives here.

## Structure

| Folder | Purpose |
| --- | --- |
| `00 - Project` | Vision, scope, team split — the "why" |
| `01 - Design` | System architecture, data model, agent reasoning loop |
| `02 - Backend` | Postgres schema, APIs, integrations (Plaid, QuickBooks, Gmail/Outlook), background jobs |
| `03 - Frontend` | Next.js app structure, dashboard, components |
| `04 - Bugs` | One note per defect, filed from `99 - Templates/Bug Report Template` |
| `05 - Code Reviews` | Notes from review passes (e.g. `/code-review`), one per pass or PR |
| `06 - Logging` | Running dev log / decisions log, newest entry on top |
| `07 - Tasks` | Active backlog, filed from `99 - Templates/Task Template` |
| `99 - Templates` | Templates for the note types above |

## Conventions

- New bug → copy `99 - Templates/Bug Report Template.md` into `04 - Bugs/`.
- New task → copy `99 - Templates/Task Template.md` into `07 - Tasks/`.
- After a code review pass, drop a summary note into `05 - Code Reviews/` (link the PR/branch and findings).
- Significant decisions or milestones get an entry in `06 - Logging/Dev Log.md`, most recent first.
- Design changes that affect the data model or architecture should update `01 - Design/Design Specification.md` directly rather than forking a new doc.

## Notes on formatting

- Notes link to each other with Obsidian wikilinks, e.g. `[[01 - Design/Design Specification]]`. If your tool doesn't resolve wikilinks, treat them as a relative path to that file's `.md`.
- All notes are plain Markdown with YAML frontmatter (`tags`, sometimes `status`/`owner`) — readable without Obsidian.

## Source of truth

- Product/architecture vision: `01 - Design/Design Specification.md`.
- Actual code state: the repo (`src/`) — don't assume the design spec is implemented; check `src/` before claiming a feature exists.
