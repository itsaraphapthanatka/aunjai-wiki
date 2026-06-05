---
title: "Deployment & Operations"
type: source
tags: [deployment, docker, nginx, operations, debugging]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Deployment & Operations

**Raw source:** `raw/deployment-operations.md`

## Key Claims
- Deploy script: `build-deploy.sh` (full rebuild including Docker image)
- Fast deploy: manual docker cp + restart (no image rebuild)
- Critical bug: `docker cp` merges directories — must delete `.next/server` first

## Safe Fast Deploy (5 steps)
1. `npm run build`
2. `docker exec aunjai-admin rm -rf .next/server`
3. Copy from `.next/standalone/aunjai-swarm/admin-ui/.next/` (not `.next/` directly)
4. Sync nginx: `sudo rm -rf /var/www/aunjai-static/* && sudo cp -r .next/static/* /var/www/aunjai-static/`
5. `docker restart aunjai-admin`

## Backend Changes
- File-only change: `docker cp file middleware:/path && docker restart aunjai-middleware`
- New DB table: `Base.metadata.create_all(tables=[NewModel.__table__])`
- New column: `ALTER TABLE name ADD COLUMN IF NOT EXISTS ...`

## Common Symptoms & Fixes
| Symptom | Cause | Fix |
|---|---|---|
| "Failed to find Server Action" | Browser cached old JS | User hard refresh (Ctrl+Shift+R) |
| 404 on new page | prerender-manifest not updated | Include all manifests in deploy |
| CSS/JS 404 | Nginx serving old static | rm -rf aunjai-static, copy fresh |
| Module missing in sidebar | ModuleCode enum not updated | Add to enum → restart → re-login |

## Health Check Commands
```bash
docker ps --format "{{.Names}}\t{{.Status}}" | grep aunjai
curl -s -o /dev/null -w "%{http_code}" https://openclaw.appreview.cloud/admin/
```

## Related
- [[concepts/deployment-process]]
- [[entities/nextjs-admin]]
- [[entities/fastapi-middleware]]
