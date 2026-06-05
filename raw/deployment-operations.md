# Deployment & Operations

## Deployment Script
`/home/ai_studio_febcth/.openclaw/workspace/aunjai-swarm/admin-ui/build-deploy.sh`

Full rebuild + deploy:
```bash
npm run build
docker compose up -d --build --force-recreate admin-ui
docker cp .next/static aunjai-admin:/app/.next/
docker cp .next/server aunjai-admin:/app/.next/
sudo cp -r .next/static/* /var/www/aunjai-static/
docker restart aunjai-admin
```

## Safe Manual Deploy (faster, no image rebuild)
```bash
# 1. Build
npm run build

# 2. Critical: DELETE old server dir first (merge bug)
docker exec aunjai-admin rm -rf .next/server

# 3. Copy all manifests from standalone (not from .next/ directly)
STANDALONE=.next/standalone/aunjai-swarm/admin-ui
for f in server build-manifest.json app-build-manifest.json \
          prerender-manifest.json routes-manifest.json \
          react-loadable-manifest.json BUILD_ID; do
  docker cp $STANDALONE/.next/$f aunjai-admin:/app/.next/$f
done
docker cp $STANDALONE/server.js aunjai-admin:/app/server.js
docker cp .next/static aunjai-admin:/app/.next/static

# 4. Sync nginx static
sudo rm -rf /var/www/aunjai-static/*
sudo cp -r .next/static/* /var/www/aunjai-static/
sudo chown -R www-data:www-data /var/www/aunjai-static/

# 5. Restart
docker restart aunjai-admin
```

## Critical Deployment Bug — docker cp merge
When copying a directory with `docker cp`, Docker MERGES (not replaces).
Old files not present in the new build remain in the container.
This causes BUILD_ID mismatch between server-rendered HTML and static JS chunks.
Symptom: "Failed to find Server Action" errors in browser console.
Fix: always `docker exec aunjai-admin rm -rf .next/server` before copying.

## Backend Deploy (middleware)
For Python changes, just copy the file and restart:
```bash
docker cp routes/users.py aunjai-middleware:/app/middleware/routes/users.py
docker restart aunjai-middleware
```
For model changes that need DB migration:
```bash
docker exec aunjai-middleware python3 -c "
import asyncio
from middleware.models.base import Base, engine
from middleware.models.new_model import NewModel
async def run():
    async with engine.begin() as conn:
        await conn.run_sync(Base.metadata.create_all, tables=[NewModel.__table__])
asyncio.run(run())
"
```
For column additions:
```bash
docker exec aunjai-middleware python3 -c "
import asyncio
from middleware.models.base import engine
from sqlalchemy import text
async def run():
    async with engine.begin() as conn:
        await conn.execute(text('ALTER TABLE table_name ADD COLUMN IF NOT EXISTS col_name TYPE'))
asyncio.run(run())
"
```

## Health Checks
```bash
# Service status
docker ps --format "{{.Names}}\t{{.Status}}" | grep aunjai

# Admin up?
curl -s -o /dev/null -w "%{http_code}" https://openclaw.appreview.cloud/admin/

# API up?
curl -s https://openclaw.appreview.cloud/aunjai-api/api/v1/admin/tags | head -c 50

# BUILD_ID sync?
docker exec aunjai-admin cat .next/BUILD_ID
cat .next/standalone/aunjai-swarm/admin-ui/.next/BUILD_ID
```

## Known Issues & Solutions

### "Failed to find Server Action" in browser
**Cause:** Browser has old JS chunks cached from previous build.
**Fix:** User needs hard refresh (Ctrl+Shift+R). Server itself is fine.
**Prevention:** Consistent full-manifest sync on every deploy.

### 404 on new pages after deploy
**Cause:** `prerender-manifest.json` not updated — Next.js doesn't know the route exists.
**Fix:** Include all manifest files in deploy, not just `.next/server/`.

### CSS/JS 404 after deploy
**Cause:** Nginx serving old static from `/var/www/aunjai-static/` while Next.js serves HTML with new chunk hashes.
**Fix:** Always `sudo rm -rf /var/www/aunjai-static/*` before copying new static.

### Module not found in sidebar
**Cause:** New module code not in `ModuleCode` enum in `staff_auth.py`. User's `accessible_modules` in localStorage from before the enum update.
**Fix:** Add to enum → restart middleware → user logout + login to refresh token.

## Environment Variables
```
NEXT_PUBLIC_API_URL=/aunjai-api/api/v1   (Next.js → API base)
NEXT_PUBLIC_INTERNAL_API_KEY             (for internal API calls)
MIDDLEWARE_URL=http://aunjai-middleware:8000  (for Next.js rewrites)
DATABASE_URL                             (PostgreSQL async URL)
DB_POOL_SIZE, DB_MAX_OVERFLOW
DEBUG
```
