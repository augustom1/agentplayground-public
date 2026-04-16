# CLAUDE.md — AgentPlayground (Open Source)

> Self-hosted AI operations platform. Read README.md for setup instructions.

## Stack
Next.js 15 · React 19 · TypeScript · Prisma 7 · PostgreSQL + pgvector · NextAuth v5 · Tailwind v4 · Docker

## Commands
```bash
npm run dev          # Dev server (port 3000)
npm run build        # Production build
npm run test         # Vitest tests
npx prisma db push   # Push schema changes
npx prisma generate  # Regenerate client
npx prisma studio    # DB GUI
```

## Key directories
- `app/(app)/` — authenticated app pages (dashboard, chat, agent-lab, files, schedule, settings, tools, users)
- `app/(auth)/` — login + first-run setup
- `app/api/` — API routes
- `lib/` — Prisma client, chat tools (20 tools), AI providers, utilities
- `components/` — shared UI components
- `prisma/schema.prisma` — database schema

## Chat system
`app/api/chat/route.ts` streams Claude/OpenAI/Ollama with a tool-calling loop (up to 10 iterations).
Tools defined in `lib/chat-tools.ts` (20 tools: teams, agents, tasks, files, web, etc.).

## Auth
NextAuth v5, JWT strategy, Credentials provider (bcrypt). First-run: `/setup` creates admin account.

## Env vars
See `.env.example` for all variables. Minimum required: `DATABASE_URL`, `AUTH_SECRET`, `CRON_SECRET`.
