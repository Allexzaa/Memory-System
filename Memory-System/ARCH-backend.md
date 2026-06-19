# ARCH-backend.md — [PROJECT NAME]
# Load this file for: API routes, DB queries, auth, server logic, integrations, infra.
# Read rule: read Summary first. Load the rest only if Summary doesn't answer the question.
# Update rule: replace/update existing entries when things change. Do not append stale info.
# Last updated: [date]

## Summary
<!-- 5 lines max. One sentence per major component. Claude reads this first. -->
- API: [e.g. "Express REST API on Node 20, all routes under /api/v1"]
- DB: [e.g. "PostgreSQL 15 + pgvector, raw SQL via pg client, no ORM"]
- Auth: [e.g. "JWT access tokens (15min) + refresh tokens (7d) in httpOnly cookies"]
- Jobs: [e.g. "BullMQ on Redis for async jobs — email, doc parsing"]
- Hosting: [e.g. "AWS EC2 t3.medium, RDS PostgreSQL, S3 for file storage"]

---

## Stack
- Runtime: [e.g. Node.js 20]
- Framework: [e.g. Express 4]
- Database: [e.g. PostgreSQL 15 + pgvector extension]
- Cache / Queue: [e.g. Redis 7 via BullMQ]
- Auth: [e.g. JWT — jsonwebtoken library]
- File storage: [e.g. AWS S3 via @aws-sdk/client-s3]
- Key deps: [anything non-obvious worth knowing]

## Folder Structure
```
[paste your actual backend folder tree here]
e.g.
src/
├── routes/        ← Express route handlers
├── services/      ← Business logic, no DB calls here
├── db/            ← All DB queries, raw SQL only
├── middleware/    ← Auth, validation, error handling
├── jobs/          ← BullMQ job definitions
└── utils/         ← Shared helpers
```

## API Surface
<!-- Key route groups only — not every endpoint -->
| Route group | File | Purpose |
|---|---|---|
| /api/v1/auth | routes/auth.ts | Login, register, refresh, logout |
| /api/v1/[resource] | routes/[file].ts | [purpose] |

## Data Flow
[Main flows in plain language]
- Request: [e.g. "Request → auth middleware → route handler → service → db → response"]
- Async: [e.g. "File upload → S3 → BullMQ job → parser service → DB write → webhook"]

## Database
- Schema location: [e.g. "db/schema.sql — source of truth, migrations in db/migrations/"]
- Multi-tenancy: [e.g. "All queries scoped to org_id — never query without it"]
- Vector search: [e.g. "pgvector cosine_distance on embeddings column in documents table"]

## Integrations
| Service | Purpose | Auth method | Notes |
|---|---|---|---|
| [e.g. Stripe] | [payments] | [API key in env] | [webhook secret required] |

## Constraints
<!-- Firewall. Claude must not violate without explicit user approval. -->
- [e.g. "No ORM — raw SQL only via pg client"]
- [e.g. "All AI calls server-side only — never expose API keys to frontend"]
- [e.g. "Multi-tenant — always filter by org_id, no exceptions"]
- [e.g. "No direct DB calls from route handlers — must go through service layer"]

## Testing
**Runner:** [e.g. Jest / Vitest / Pytest]
**Command:** [e.g. `npm test`]
**Coverage:** [e.g. Istanbul — or "none yet"]

What is tested:
- Unit: [e.g. "service layer functions, data transformers"]
- Integration: [e.g. "API routes against test DB — run with TEST_DB env var"]
- E2E: [e.g. "not yet"]

Coverage gaps: [things you know are untested]
Skipped tests: [intentionally skipped + reason]
Flaky tests: [intermittent failures + root cause]

## Known Gotchas
<!-- Non-obvious things that cost time — different from FAILURES.md -->
- [e.g. "pgvector cosine_distance returns 0 for identical vectors, not 1"]
- [e.g. "BullMQ jobs silently swallow errors unless you add a failed event listener"]
