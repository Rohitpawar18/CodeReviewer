# Code Review Agent

Automated code review system that ingests pull requests, runs analysis agents, and delivers ranked findings. Includes a snippet review dashboard.

## Highlights

- GitHub and GitLab integrations
- Static analysis hooks, security scanning, style checks, docs checks, performance hints
- ScaleDown compression for large diffs and commit history
- Feedback ranking by impact and confidence
- Dashboard for snippet reviews and ranked feedback

## Architecture

- API service: review ingestion, queueing, persistence, REST endpoints
- Worker service: background agent execution and ranking
- Dashboard: web UI for snippet reviews and results
- Shared packages: types, repository utilities, ScaleDown, and agents

## Prerequisites

- Node.js 20+
- PostgreSQL 15+
- Redis 7+ (required only for the background worker)

## Environment

Create .env files in the API and worker apps.

apps/api/.env

```
PORT=4000
DATABASE_URL=postgres://user:password@localhost:5432/codereview
REDIS_URL=redis://localhost:6379
GITHUB_TOKEN=...
GITLAB_TOKEN=...
```

apps/worker/.env

```
DATABASE_URL=postgres://user:password@localhost:5432/codereview
REDIS_URL=redis://localhost:6379
```

If REDIS_URL is omitted in apps/api/.env, the API runs agent analysis inline and the worker is not required.

## Database Setup

Apply the schema using your DATABASE_URL.

```bash
psql "$DATABASE_URL" -f packages/shared/src/schema.sql
```

## Development

Install dependencies once at the repo root.

```bash
npm install
```

Start services in separate terminals.

```bash
npm run dev:api
npm run dev:worker
npm run dev:dashboard
```

## Production Build

```bash
npm run build
```

## Key API Endpoints

- POST /api/reviews
- GET /api/reviews
- GET /api/reviews/:id

## ScaleDown

ScaleDown compresses large diffs and commit history by up to 80 percent while preserving key signals like signatures, TODOs, and security-relevant lines. This reduces review time while keeping context for decisions.

## Repository Layout

- apps/api: API service
- apps/worker: background worker
- apps/dashboard: React dashboard
- packages/agents: analysis agents
- packages/scaledown: compression utilities
- packages/shared: types, schema, repository helpers

## Project Goals

- Compress large PRs (1000+ lines) by 80 percent
- Review with full codebase context
- Reduce review time by 70 percent
- Deliver feedback ranked by impact and confidence

## Roadmap

- Integrate real linters and SAST tools
- Enhance coverage analysis using CI artifacts
- Add SSO for enterprise users
- Expand dashboard analytics and trends
