---
title: "Overview"
type: overview
tags: [aunjai, febc, system]
created: 2026-06-05
updated: 2026-06-11
sources: 9
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
    ↕ keyword routing (4 paths)
OpenClaw Gateway (Aunjai Swarm — 15+ agents)
    ↕
Next.js Admin UI  ←  Nginx  ← Browser (admin staff)
    ↕
External: middleware.febradio.org (tags), Pinecone (content), YouTube
```

## AI Agent Layer (Aunjai Swarm)
ระบบ chatbot ทำงานบน **[[concepts/aunjai-swarm]]** — multi-agent swarm บน OpenClaw Gateway
- **[[concepts/keyword-routing]]** — 4 paths ที่ middleware ก่อนถึง agents (video browse/request, emotional, normal)
- **[[concepts/message-pipeline]]** — main → sentinel → journey-architect → domain → log
- **[[concepts/sentinel-safety]]** — 5-level safety scoring; FREEZE ≤ -0.9 → human counselor ทันที
- **[[concepts/onboarding-flow]]** — 4-step resumable profile setup

## Key Modules (14)
Dashboard · Users · **SOS** · **Tags** · Campaigns · Academy · Coins · Churches · Prayer · Volunteer · Content · Commander · Staff · Permissions

## Most Complex Systems
1. **[[entities/sos-command-center]]** — real-time crisis intervention, WebSocket, volunteer escalation chain
2. **[[entities/campaign-system]]** — coin economy, LINE broadcast, ROI tracking
3. **[[entities/academy-lmm]]** — learning paths, certificate postal delivery

## Recently Built (2026-06-08 – 2026-06-11)
- [[entities/access-links-module]] — Smart Access Links v7.0 (QR/Deeplink + 2-level approval + auto-tag)
- [[concepts/post-cert-journey]] — Post-Certificate Journey Map Phase 3 (Day 0/2/5/10/14/30 automation)
- [[concepts/topic-affinity]] — EMA topic affinity scoring ต่อ user ต่อ topic (α=0.2)
- [[concepts/automated-lifecycle-services]] — Night Prayer Service (ใหม่), Morning Greeting v5 Phase 3
- Feature Flags API: quiz_enabled / coin_enabled

## Built (2026-06-05)
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
- [[concepts/post-cert-journey]] — follow-up automation Day 0/2/5/10/14/30 หลังรับใบประกาศ
- [[concepts/topic-affinity]] — EMA scoring per user per topic
- [[concepts/automated-lifecycle-services]] — morning greeting, night prayer, background workers

## Open Questions / Known Gaps
- MEMBER_, NEW_, SUB_MENU_ tags ใน "Other" group — ยังไม่ได้ auto-detect
- Tags ใน middleware (364) vs tags ใน users (219) — 145 tags ไม่มี users
- `available_days` field — logic การ expire ยังไม่ถูก implement ใน backend
- Telegram bot สำหรับ Access Links (สร้าง link ผ่าน Telegram) — ยังไม่พบ bot code
- Agent count v7.0 = 19 agents แต่ list agent เพิ่มใหม่ยังไม่ชัดเจน

## Related
- [[index]]
- [[log]]
