---
tags: [frontend]
---

# Frontend Overview

Owner: Developer 1 (Full-Stack / Product). See [[00 - Project/Overview|Team Split]].

## Responsibilities

- Next.js frontend, dashboard
- Application architecture, auth, billing, deployment

## Current code

- `src/app/` — App Router entry (`layout.tsx`, `page.tsx`) — default `create-next-app` scaffold, not yet customized
- `src/components/ui/` — shadcn-based UI primitives (`button.tsx` so far)
- Stack: Next.js 16, React 19, Tailwind v4, shadcn/ui, Framer Motion, Recharts (for dashboard charts), Zod

## Related

- [[01 - Design/Design Specification|Design Specification]] — Core V1 Workflow drives the main dashboard UX (import → review matches → approve/reject → audit trail)
