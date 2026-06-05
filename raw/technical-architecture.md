# Technical Architecture

## Stack

### Frontend — admin-ui
- Framework: Next.js 15.5.14
- Language: TypeScript
- Styling: Tailwind CSS with CSS variables (theme tokens)
- Icons: lucide-react
- Config: `basePath: "/admin"`, `output: "standalone"`, `trailingSlash: true`
- Auth: JWT access token + refresh token, stored in localStorage
- Real-time: WebSocket (SOS system)

### Backend — middleware
- Framework: FastAPI (Python)
- ORM: SQLAlchemy async (asyncpg driver)
- DB: PostgreSQL (async)
- Cache: Redis
- Auth: JWT (PyJWT), MFA via TOTP (pyotp)
- AI/ML: OpenAI Whisper (audio), tiktoken
- Vector DB: Pinecone (content search)
- PDF/Docs: reportlab, python-docx

### Infrastructure
- Deployment: Docker Compose
- Reverse proxy: Nginx
- Domain: openclaw.appreview.cloud (HTTPS)
- Static files: /var/www/aunjai-static/ (served by Nginx directly)

## Docker Containers
```
aunjai-admin      port 3001  Next.js standalone server
aunjai-middleware port 8000  FastAPI uvicorn
aunjai-db         port 5432  PostgreSQL
aunjai-redis      port 6379  Redis
petty-cash-frontend  port 3003
petty-cash-backend   port 8002
petty-cash-db        port 5434
```

## Nginx Routing
```
/admin/            → proxy 127.0.0.1:3001
/admin/_next/static/ → /var/www/aunjai-static/ (file serve)
/aunjai-api/api/v1/ → proxy 127.0.0.1:8000/api/v1/
/pinecone-proxy/   → Pinecone vector DB
```

## Deployment Process
1. `npm run build` (Next.js, ~20s)
2. `docker cp` new `.next/` files into running container
   - Must delete `.next/server/` before copying to avoid stale file merging
   - Copy from `.next/standalone/` not `.next/` directly
3. Sync `/var/www/aunjai-static/` from `.next/static/`
4. `docker restart aunjai-admin`

Critical gotcha: `docker cp` of a directory MERGES (not replaces). Always `docker exec aunjai-admin rm -rf .next/server` first, then copy fresh.

## Key External Integrations
- **LINE OA** — primary user channel, broadcast, flex messages
- **middleware.febradio.org** — FEBC middleware, source of FEBC tags (364 tags)
- **Pinecone** — vector search for video content (full-clip namespace)
- **YouTube** — video content source
- **Thailand Post** — postal tracking for certificate delivery

## API Authentication
- `Authorization: Bearer {access_token}` for most endpoints
- `X-API-Key` for some internal endpoints (broadcast, banner upload)
- Staff auth via `/auth/login` → JWT access + refresh tokens
- Auto-refresh on 401 via `fetchAPI()` wrapper in `lib/api.ts`

## Permission System
Module-based permissions stored per staff member:
```
ModuleCode enum: dashboard, users, sos, budget, campaign, rewards,
church_map, academy, content, analytics, staff_management, agents,
settings, permissions, volunteer, intercessory, tags
```
Each module has: view, create, edit, delete, export flags.
SuperAdmin gets all permissions automatically.

## Database Key Tables
- `users` — LINE users, febc_tags ARRAY, scores
- `staff_members` — admin users
- `sos_events` — SOS alert records
- `febc_tags` — tag metadata (description, group, available_days)
- `febc_tag_groups` — custom group definitions
- `campaign_registry` — campaigns
- `coin_ledger` — coin transactions
- `academy_chapters` — learning chapters
- `church` — church records
- `prayer_requests` — intercessory prayer

## Module Code Files (backend)
```
middleware/
├── main.py              router registration
├── models/
│   ├── user.py          User, FunnelStage, CircleLevel
│   ├── safety.py        SOSEvent, PrayerRequest
│   ├── campaign.py      CampaignRegistry, CampaignRule
│   ├── coin.py          CoinLedger, RewardCatalog
│   ├── academy.py/v2/v3 Chapter, Lesson, Certificate
│   ├── staff_auth.py    StaffMember, ModuleCode
│   ├── tag.py           FEBCTag (metadata)
│   └── tag_group.py     FEBCTagGroup
└── routes/
    ├── users.py
    ├── admin.py         tags, churches, HoB, rewards
    ├── safety.py        SOS, prayer
    ├── auth.py          login, permissions
    └── academy.py
```
