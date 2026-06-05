---
title: "Overview"
type: overview
tags: [aunjai, febc, system]
created: 2026-06-05
updated: 2026-06-05
sources: 6
---

# น้องอุ่นใจ System — Overview

## What This Wiki Covers
ระบบ Admin Command Center ของน้องอุ่นใจ — LINE OA chatbot + AI companion สำหรับ FEBC Thailand งานดูแลจิตใจและ discipleship

## Core Mission
พา users ผ่าน **Engage → Connect → Transform → Send**
เป้าหมาย: 50,000 users ใน 12 เดือน (ณ 2026-06-05: ~10,048 users)

## System Architecture (ย่อ)
```
LINE OA users
    ↕ (webhook, broadcast)
FastAPI Middleware (Python)  ←→  PostgreSQL + Redis
    ↕
Next.js Admin UI  ←  Nginx  ← Browser (admin staff)
    ↕
External: middleware.febradio.org (tags), Pinecone (content), YouTube
```

## Key Modules (14)
Dashboard · Users · **SOS** · **Tags** · Campaigns · Academy · Coins · Churches · Prayer · Volunteer · Content · Commander · Staff · Permissions

## Most Complex Systems
1. **[[entities/sos-command-center]]** — real-time crisis intervention, WebSocket, volunteer escalation chain
2. **[[entities/campaign-system]]** — coin economy, LINE broadcast, ROI tracking
3. **[[entities/academy-lmm]]** — learning paths, certificate postal delivery

## Recently Built (2026-06-05)
- [[entities/tags-management]] — Tags Management module (สร้างใหม่ทั้งหมด)
  - 364 FEBC tags, auto-grouped, custom group colors
  - Backend CRUD + bulk user-tag operations
  - Integrated into Campaign TagSelector

## Key Concepts
- [[concepts/funnel-stages]] — Engage→Connect→Transform→Send
- [[concepts/spiritual-scores]] — R, S, Q, I scores; S≤-0.9 triggers SOS
- [[concepts/tag-groups]] — prefix-based + custom group system
- [[concepts/volunteer-escalation]] — SOS escalation state machine
- [[concepts/deployment-process]] — docker cp merge bug + safe deploy steps

## Open Questions / Known Gaps
- MEMBER_, NEW_, SUB_MENU_ tags ใน "Other" group — ยังไม่ได้ auto-detect
- Tags ใน middleware (364) vs tags ใน users (219) — 145 tags ไม่มี users
- `available_days` field — logic การ expire ยังไม่ถูก implement ใน backend

## Related
- [[index]]
- [[log]]
