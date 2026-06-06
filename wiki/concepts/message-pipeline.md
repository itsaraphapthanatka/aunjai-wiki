---
title: "Message Pipeline (Per-Message)"
type: concept
tags: [pipeline, agents, orchestration, swarm]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Message Pipeline (Per-Message)

ลำดับการทำงานของ agents ต่อข้อความ 1 ข้อความที่ผ่าน ARC-GATE เข้า OpenClaw

## Pipeline Sequence

```
1. main          → Orchestrator Gate — เลือก squad
2. sentinel      → Safety Scan (security_scan_content)
3. journey-architect → user_get_profile + Campaign Context
4. Domain Agent  → front-desk / academy / search-specialist ตามประเภท
5. truth-auditor → (ถ้ามีข้อพระคัมภีร์) bible_verify_scripture
6. reward-manager → (ถ้ามี Coin Event) coins_award
7. care-loop-closer → (ถ้า SOS) case_get_open
8. Log           → logs_analyze_conversation
```

## หมายเหตุ

- Steps 5–7 เป็น **conditional** — ทำงานเฉพาะเมื่อมี event ที่เกี่ยวข้อง
- **sentinel** (step 2) มี authority override ทุก step — FREEZE หยุดทุกอย่างทันที
- **Log** (step 8) ทำงานทุกข้อความเสมอ ไม่ว่าผลลัพธ์จะเป็นอะไร
- **journey-architect** (step 3) inject persona และ campaign context ก่อน domain agent เสมอ

## ก่อน Pipeline (Middleware Level)

ดู [[concepts/keyword-routing]] — PATH A/B/C อาจไม่เข้า pipeline นี้เลย (ตอบ video cards โดยตรง)

## Related

- [[concepts/aunjai-swarm]]
- [[concepts/keyword-routing]]
- [[concepts/sentinel-safety]]
- [[sources/aunjai-swarm-agent-flow]]
