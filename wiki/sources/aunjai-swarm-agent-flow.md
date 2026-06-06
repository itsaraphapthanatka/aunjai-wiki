---
title: "Aunjai Swarm — Agent Flow Documentation"
type: source
tags: [swarm, agents, openclaw, architecture, sentinel]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Aunjai Swarm — Agent Flow Documentation

**Source:** openclaw.appreview.cloud/docs/aunjai-agent-flow.html

## Key Claims

- ระบบ Aunjai ใช้ multi-agent swarm บน **OpenClaw Gateway** ประกอบด้วย 15+ agents จัดกลุ่มใน 6 groups + support agents
- ทุกข้อความผ่าน **Nginx → Middleware (line_webhook.py)** → keyword check → 4 paths ก่อนถึง agent
- **Pipeline ต่อข้อความ**: main → sentinel → journey-architect → domain agent → (truth-auditor?) → (reward-manager?) → (care-loop-closer?) → log
- **Sentinel** scan ทุกข้อความ ใช้ sentiment score 5 ระดับ; FREEZE (≤ -0.9) หยุด AI ทันที → human counselor
- **front-desk** agent เป็นตัวหลัก: 11 threads, RSS 612.9MB; สลับ 12 persona ตาม Circle + Sentiment
- **Onboarding** 4 ขั้นตอนแบบ resumable: nickname → ชื่อ-สกุล → อายุ → จังหวัด

## Agent Groups

| Group | ชื่อ | Agents หลัก |
|-------|------|-------------|
| 1 — Front Line | ประตูหน้าด่าน | main, front-desk |
| 2 — UX & Flow | วาง path C1→C4 | journey-architect, aunjai-messenger |
| 3 — Academy | Faith Quiz & Rewards | academy-specialist, reward-manager |
| 4 — Soul Care & SOS | Prayer & Crisis | intercessory-coordinator, care-loop-closer |
| 5 — C4 & Stewardship | Church Matching | insights-analyst |
| 6 — Memory & Health | Sync & Monitor | maac-sync, auto-qa |
| Support | Cross-cutting | sentinel, truth-auditor, system-tuner |

## Notable Quotes

> "🛡️ sentinel → ALL agents — Safety Override, SOSVE Freeze"

> "⛔ FREEZE ≤ -0.9 → หยุด AI ทันที → ส่งต่อที่ปรึกษามนุษย์"

> "⚡ 55 msgs | P95: 9.5s" *(sentinel performance)*

## Gaps / Unanswered Questions

- ไม่ระบุ LLM ที่ใช้ใน agents แต่ละตัว (GPT-4? Claude?)
- ไม่มีรายละเอียด `maac-sync` และ master-brain คือระบบอะไร
- `referral-tracker` / affiliate system ไม่มี flow ละเอียด
- `auto-qa` ตรวจ API health ทุก service — ไม่รู้ frequency/alerting

## Related

- [[concepts/aunjai-swarm]]
- [[concepts/sentinel-safety]]
- [[concepts/keyword-routing]]
- [[concepts/message-pipeline]]
- [[concepts/onboarding-flow]]
- [[entities/arc-console]]
- [[entities/sos-command-center]]
- [[sources/sos-flow]]
- [[sources/technical-architecture]]
