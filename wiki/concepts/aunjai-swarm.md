---
title: "Aunjai Swarm"
type: concept
tags: [swarm, agents, openclaw, architecture]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Aunjai Swarm

Multi-agent AI architecture ของน้องอุ่นใจ ทำงานบน **OpenClaw Gateway**

## ภาพรวม

ระบบประกอบด้วย agents 15+ ตัว จัดเป็น 6 functional groups + support agents แต่ละ agent มีหน้าที่เฉพาะ สื่อสารกันผ่าน OpenClaw orchestration layer

## Agent List

### Group 1 — Front Line
- **🎯 main** — Orchestrator Gate; route ข้อความไปยัง squad ที่เหมาะสม
- **💛 front-desk** — รับ input จาก main; สลับ 12 persona ตาม Circle + R_score + sentiment; 11 threads, 612.9MB RSS

### Group 2 — UX & Flow
- **🗺️ journey-architect** — วาง path C1→C4; inject campaign context; ส่ง context update กลับ front-desk
- **📣 aunjai-messenger** — สร้าง Flex Message, Carousel, Bubble; sync budget กับ reward-manager

### Group 3 — Academy
- **🎓 academy-specialist** — ออกแบบ Faith Quiz; trigger coin award ผ่าน reward-manager
- **🪙 reward-manager** — จัดการ Token & Coins reward system
- **🤝 referral-tracker** — ระบบ Affiliate ติดตามการแนะนำเพื่อน; ส่ง referral bonus ไป reward-manager

### Group 4 — Soul Care & SOS
- **🙏 intercessory-coordinator** — ประสานงาน Prayer Partner Bridge; handoff ไป care-loop-closer
- **🔎 search-specialist** — Pinecone RAG Search หลายรูปแบบ
- **🔁 care-loop-closer** — SOS Case Lifecycle; เปิด/ติดตามเคส; ส่ง funnel adjustment กลับ journey-architect

### Group 5 — C4 & Stewardship
- **📊 insights-analyst** — Analytics & KPI; collect data จาก ALL agents

### Group 6 — Memory & Health
- **💜 maac-sync** — Memory Sync ประสาน master-brain (bidirectional)
- **🧪 auto-qa** — ตรวจ API Health ทุกบริการ

### Support Agents
- **🛡️ sentinel** — SOSVE Crisis Detection; scan ทุกข้อความ; P95 9.5s, 55 msgs; override ALL agents
- **✝️ truth-auditor** — ตรวจสอบข้อพระคัมภีร์; approve/reject scripture ก่อน delivery
- **🔧 system-tuner** — ปรับ Prompt ของ agents ทุกตัว

## การสื่อสารระหว่าง Agents

- **main → ALL** — Gateway Guard กระจายงาน
- **sentinel → ALL** — Safety Override, SOSVE Freeze (สูงสุด priority)
- **front-desk → specialists** — User Input Routing
- **journey-architect → front-desk, aunjai-messenger** — Context Injection
- **truth-auditor → media-delivery** — Approve/Reject Scripture
- **care-loop-closer → journey-architect** — Post-SOS Funnel Adjustment
- **system-tuner → ALL** — Prompt Updates
- **insights-analyst → ALL** — Data Collection

## Related

- [[concepts/sentinel-safety]]
- [[concepts/keyword-routing]]
- [[concepts/message-pipeline]]
- [[concepts/onboarding-flow]]
- [[entities/arc-console]]
- [[sources/aunjai-swarm-agent-flow]]
