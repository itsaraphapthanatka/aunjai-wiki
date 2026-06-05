---
title: "Technical Architecture"
type: source
tags: [nextjs, fastapi, postgresql, docker, infrastructure]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Technical Architecture

**Raw source:** `raw/technical-architecture.md`

## Key Claims
- Frontend: Next.js 15.5.14, TypeScript, Tailwind CSS
- Backend: FastAPI + SQLAlchemy async + asyncpg
- DB: PostgreSQL; Cache: Redis
- Deploy: Docker Compose + Nginx reverse proxy
- Domain: openclaw.appreview.cloud

## Containers
| Container | Port | Role |
|---|---|---|
| aunjai-admin | 3001 | Next.js standalone server |
| aunjai-middleware | 8000 | FastAPI uvicorn |
| aunjai-db | 5432 | PostgreSQL |
| aunjai-redis | 6379 | Redis |

## Notable Config
- Next.js `basePath: "/admin"`, `output: "standalone"`, `trailingSlash: true`
- Static files at `/var/www/aunjai-static/` served by Nginx directly
- Auth: JWT in localStorage, auto-refresh on 401 via `fetchAPI()` wrapper

## External Integrations
- LINE OA — primary user channel
- middleware.febradio.org — source of FEBC tags (364 tags)
- Pinecone — vector search for video content
- YouTube — video source
- Thailand Post — postal tracking

## Database Key Tables
users, staff_members, sos_events, febc_tags, febc_tag_groups, campaign_registry, coin_ledger, academy_chapters, church, prayer_requests

## Critical Deployment Bug
`docker cp` of directory MERGES, not replaces. Always delete `.next/server/` in container before copying new build. Symptom: "Failed to find Server Action" errors.

## Related
- [[concepts/deployment-process]]
- [[concepts/api-authentication]]
- [[entities/nextjs-admin]]
- [[entities/fastapi-middleware]]
