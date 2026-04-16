# AgentPlayground

A self-hosted AI operations platform. Build agent teams, automate workflows, and run local LLMs — all on your own server.

## What it is

AgentPlayground is an open-source web application that gives you a unified interface for:

- **Chat with AI** — Stream conversations with Claude (Anthropic), GPT (OpenAI), or local models via Ollama
- **Agent Teams** — Create teams of AI agents with specific roles, skills, and system prompts
- **Task Automation** — Schedule recurring tasks, delegate work to agent teams
- **File Management** — Upload, organize, and search files with vector embeddings
- **n8n Integration** — Connect your agents to 400+ external services (Gmail, Slack, webhooks, etc.)
- **Local LLMs** — Run Qwen, Llama, Mistral, DeepSeek locally via Ollama — zero API costs for routine tasks

## Stack

| Component | Purpose |
|-----------|---------|
| Next.js 15 + React 19 | App framework |
| TypeScript + Prisma 7 | Type-safe ORM |
| PostgreSQL + pgvector | Database + vector search |
| NextAuth v5 | Authentication |
| Tailwind v4 | Styling |
| Docker Compose | Container orchestration |
| Ollama | Local LLM inference |
| n8n | Workflow automation |
| Traefik | Reverse proxy + SSL |

## Requirements

- VPS with **4GB+ RAM** (8GB recommended for local LLMs)
- Ubuntu 22.04 or later
- A domain name pointed to your server
- Docker + Docker Compose

Recommended: [Hetzner CX22](https://hetzner.com) (~$6 USD/month, 4GB RAM)

## Quick Start

```bash
# 1. Clone the repo
git clone https://github.com/augustom1/agentplayground-public
cd agentplayground-public

# 2. Copy the environment template
cp .env.example .env.local

# 3. Edit with your values (domain, passwords, API keys)
nano .env.local

# 4. Start the stack
docker compose up -d

# 5. Open http://localhost:3000/setup → create your admin account
```

## Production Deployment (HTTPS)

```bash
# Set your domain in .env.local
DOMAIN=yourdomain.com
ACME_EMAIL=you@yourdomain.com

# Deploy with Traefik HTTPS
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d --build

# App live at https://app.yourdomain.com
```

## Environment Variables

Copy `.env.example` to `.env.local` and fill in:

| Variable | Required | Description |
|----------|----------|-------------|
| `DATABASE_URL` | Yes | PostgreSQL connection string |
| `AUTH_SECRET` | Yes | NextAuth JWT secret (`openssl rand -hex 32`) |
| `CRON_SECRET` | Yes | Bearer token for cron endpoint |
| `ANTHROPIC_API_KEY` | Optional | Claude API — Ollama works without it |
| `DOMAIN` | Production | Your domain name |

See `.env.example` for the full list.

## First Run

1. Navigate to `/setup` to create your admin account
2. Go to **Agent Lab** to create your first agent team
3. Start chatting at `/chat` — use Claude or a local Ollama model

## Project Structure

```
app/
  (app)/          # Authenticated pages
  (auth)/         # Login + setup
  api/            # API routes
lib/              # Prisma client, chat tools, utilities
components/       # UI components
prisma/           # Database schema
```

## Commands

```bash
npm run dev       # Dev server (port 3000)
npm run build     # Production build
npm run test      # Vitest tests
npx prisma studio # DB GUI at localhost:5555
```

## Managed Hosting

Don't want to manage your own server? [AgentPlayground AR](https://ar.agentplayground.net) offers professional installation and managed hosting (Argentina).

## License

MIT — free to use, modify, and self-host.
