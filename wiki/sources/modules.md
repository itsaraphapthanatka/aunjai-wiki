---
title: "System Modules"
type: source
tags: [modules, dashboard, sos, tags, campaigns, academy, coins]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# System Modules

**Raw source:** `raw/modules.md`

## Key Claims
- ระบบมี 14 modules หลัก แต่ละ module มี permission flags: view, create, edit, delete, export
- แต่ละ module route อยู่ใต้ `/admin/[module]`

## Module Summary

| Module | Route | หน้าที่หลัก |
|---|---|---|
| Dashboard | / | KPI, funnel chart, SOS alert, budget |
| Users | /users | จัดการ user profiles, scores, tags |
| SOS | /sos | Crisis intervention, volunteer escalation |
| Tags | /tags | FEBC tag management, grouping |
| Campaigns | /campaigns | LINE broadcast, coin rewards, ROI |
| Academy | /academy | Online learning, certificates, shipping |
| Coins & Rewards | /coins /rewards | Gamification, redemption |
| Churches | /churches | Church directory, baptism tracking |
| Prayer | /prayers | Intercessory prayer requests |
| Volunteer | /volunteer | Volunteer management, ambassador hub |
| Content | /content | Video content via Pinecone |
| Commander | /commander | Budget control, AI agents |
| Staff | /staff | Staff management, custom roles |
| Permissions | /permissions | Module permission matrix |

## Key Design Patterns
- User drawer (slide-in right panel) ใช้ใน Users และ SOS
- Real-time WebSocket ใน SOS
- Permission-gated UI (ซ่อน actions ถ้าไม่มี permission)
- Standalone Next.js + nginx for static serving

## Related
- [[entities/sos-command-center]]
- [[entities/tags-management]]
- [[entities/campaign-system]]
- [[entities/academy-lmm]]
- [[concepts/funnel-stages]]
