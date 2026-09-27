# Reconcile AI

An AI-native pre-audit agent that autonomously matches transactions to supporting evidence (contracts, emails, receipts, bank logs) and drafts the audit-defense package before a human reviews it. See the full design in [`AI_Recon_Obsidian_Vault/01 - Design/Design Specification.md`](AI_Recon_Obsidian_Vault/01%20-%20Design/Design%20Specification.md).

## Status

Early scaffold. Next.js app with Supabase (`@supabase/ssr`, `@supabase/supabase-js`) and Drizzle ORM wired up as dependencies; `src/db` and the `document` / `reconciliation` / `transaction` services in `src/services` are stubbed but not yet implemented.

## Stack

- Next.js 16 (App Router) + React 19
- Tailwind v4, shadcn/ui, Framer Motion, Recharts
- Supabase (Postgres + pgvector) via Drizzle ORM
- Zod for validation

## Getting Started

```bash
npm install
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the app. Edit `src/app/page.tsx` — it hot-reloads.

## Project notes

Deeper project context (architecture, data model, backend/frontend notes, bugs, tasks, dev log) lives in the Obsidian vault at [`AI_Recon_Obsidian_Vault/`](AI_Recon_Obsidian_Vault/) — start at [`Home.md`](AI_Recon_Obsidian_Vault/Home.md).

## Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying)
