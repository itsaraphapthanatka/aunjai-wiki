---
title: "Circle Level Progression (C1→C4)"
type: concept
tags: [circle-level, C1, C2, C3, C4, funnel, promotion, journey-architect]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Circle Level Progression (C1→C4)

## Description
ระบบ Circle Level คือการจำแนกระยะการเติบโตทางจิตวิญญาณของผู้ใช้อุ่นใจออกเป็น 4 ระดับ  
ขับเคลื่อนด้วย R-Score ที่คำนวณจาก S (Sentiment) + Q (Quiz/QT) + I (Interaction)

## ระดับและเกณฑ์

| Circle | ชื่อ | R-Score | Funnel Stage |
|--------|------|---------|--------------|
| **C1** | Engage — ผู้มาใหม่ | 0.0–0.3 | Engage |
| **C2** | Connect/Transform — ผู้เชื่อมต่อ | 0.3–0.75 | Connect → Transform |
| **C3** | Send — ผู้พร้อมรับใช้ | ≥ 0.85 | Send |
| **C4** | Stewardship — ส่งต่อคริสตจักร | — | (post-Send) |

## กลไกการเลื่อนระดับ

```
อัปเดต S/Q/I → auto-recalculate R → threshold เกิน → auto-promote
หรือ Journey Architect เรียก middleware_promote_funnel ด้วยตรง
```

R-Score: `R = S×0.4 + Q×0.3 + I×0.3`

## Agents ต่อระดับ

- **C1/C2**: front-desk (12 personas), journey-architect
- **C3**: academy-specialist, reward-manager, aunjai-messenger
- **C4**: local-connector (`church_match_local` + `handiff_register`)

## Usage

- ทุก LINE webhook ส่ง `circle_level` ใน `aunjai_user_context` payload
- Journey Architect อ่าน circle_level → เลือก decision matrix → กำหนดทิศทาง
- Reward catalog บางรายการ lock เฉพาะ circle: `required_circles: ["C3"]`
- Insights Analyst รายงาน conversion rates ต่อระดับ

## Related

- [[concepts/funnel-stages]] — Engage→Connect→Transform→Send
- [[concepts/spiritual-scores]] — R, S, Q, I scores
- [[sources/aunjai-circle-level-progression]] — full detail + API
- [[sources/aunjai-swarm-agent-flow]] — agent pipeline
