---
title: "SOS Command Center"
type: entity
tags: [sos, crisis, module, arc]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# SOS Command Center
**"The Spiritual ER"**

## Description
ระบบ crisis intervention ของน้องอุ่นใจ ตรวจจับผู้ใช้ที่อยู่ในภาวะวิกฤตจิตใจ และ route ไปยังการช่วยเหลือ

## Trigger Condition
S-score ≤ -0.9 หรือ admin สร้างมือ

## Response Chain
AI Autopilot → Staff Takeover → Volunteer Escalation / Field Escalation

## Key Components
- **KPI Bar** — active SOS, critical count, avg response time, handover 24h
- **Alert List** — tabs: Active / Resolved / ทั้งหมด
- **Case Detail Drawer** — ใช้ admin จัดการ case แต่ละ case
- **ARC Console** — AI chat overlay
- **VolunteerEscalationModal** — เลือก volunteer + ส่ง LINE

## Real-time
WebSocket `/sos/ws` — auto-reconnect 5s, full refresh 30s, wait-time ticker 15s

## Volunteer Status States
🟣 waiting → 🟡 timeout → 🟢 accepted / 🔵 returned

## Related
- [[entities/arc-console]]
- [[concepts/volunteer-escalation]]
- [[concepts/spiritual-scores]]
- [[sources/sos-flow]]
