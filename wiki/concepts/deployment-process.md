---
title: "Deployment Process"
type: concept
tags: [deployment, docker, nextjs, operations]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Deployment Process

## Description
วิธีการ deploy code ขึ้น production ที่ openclaw.appreview.cloud

## Two Methods

### Full Deploy (build-deploy.sh)
Rebuilds Docker image — ช้ากว่า (~5-10 min) แต่ clean ที่สุด

### Fast Manual Deploy
Copy files เข้า running container — เร็วกว่า (~2 min):
1. `npm run build`
2. `docker exec aunjai-admin rm -rf .next/server` ← **critical step**
3. Copy from `.next/standalone/aunjai-swarm/admin-ui/.next/`
4. Sync nginx static: `sudo rm -rf /var/www/aunjai-static/*`
5. `docker restart aunjai-admin`

## The Merge Bug
`docker cp directoryA container:/directoryB` → MERGES, ไม่ replace
ถ้าไม่ delete ก่อน: old files ค้างอยู่ → BUILD_ID mismatch → "Server Action" errors

## Backend Deploy
```bash
docker cp file.py container:/app/path/file.py
docker restart aunjai-middleware
```
DB migration เพิ่มได้ผ่าน `ALTER TABLE ... ADD COLUMN IF NOT EXISTS`

## Verification
```bash
docker exec aunjai-admin cat .next/BUILD_ID  # ต้องตรงกับ local build
curl -s -o /dev/null -w "%{http_code}" https://openclaw.appreview.cloud/admin/
```

## Related
- [[sources/deployment-operations]]
- [[entities/nextjs-admin]]
