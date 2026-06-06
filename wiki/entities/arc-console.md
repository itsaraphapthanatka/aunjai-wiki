---
title: "ARC Console"
type: entity
tags: [arc, ai, chat, sos, openclaw]
created: 2026-06-05
updated: 2026-06-06
sources: 2
---

# ARC Console
**Aunjai Rescue Console**

## Description
AI-driven chat system ที่ทำงานระหว่าง SOS case
มีสองโหมด: AUTOPILOT (AI ตอบเอง) และ PAUSED (admin ควบคุม)

## Modes
- **AUTOPILOT** — AI สนทนากับ user โดยอัตโนมัติ
- **PAUSED** — Admin take over; AI หยุดตอบ

## Admin Actions in ARC
- ส่งข้อความเอง
- ใช้ Quick Templates (3 รูปแบบ)
- Assign prayer partner
- Escalate to field team
- Resolve case

## Takeover Flow
1. Admin กด "Take Over Chat"
2. `POST /admin/sos/takeover` → ai_status = "PAUSED"
3. ARC Console overlay เปิด
4. Admin chat + actions available

## Navigation
- เปิดจาก SOS Command Center
- เปิดได้จาก LINE Flex Message: `?caseId=UUID`

## OpenClaw Backend

(confirmed) ARC Console's AI chat is powered by the **front-desk agent** in [[concepts/aunjai-swarm]] — accessed via ARC-GATE → OpenClaw Gateway. ข้อความผ่าน [[concepts/message-pipeline]] เต็มรูปแบบ รวมถึง sentinel safety scan

## Related
- [[entities/sos-command-center]]
- [[concepts/volunteer-escalation]]
- [[concepts/aunjai-swarm]]
- [[concepts/sentinel-safety]]
- [[sources/sos-flow]]
- [[sources/aunjai-swarm-agent-flow]]
