---
title: "Aunjai Circle Level Progression (C1→C2→C3→C4)"
type: source
tags: [circle-level, funnel, progression, journey-architect, promotion, aunjai]
created: 2026-06-06
updated: 2026-06-06
sources: 4
raw: aunjai-circle-level-progression
---

# Aunjai Circle Level Progression (C1→C2→C3→C4)

**Sources:** workspace/AUNJAI-BOOTSTRAP.md, workspace/AUNJAI-PERSONAS.md, workspace/aunjai-swarm/AGENTS.md, workspace/aunjai-swarm/specs/coin-management-use-case.md

## Key Claims

- ระบบ Aunjai แบ่งผู้ใช้ออกเป็น 4 ระดับ C-Stage: **C1 (Engage) → C2 (Connect/Transform) → C3 (Send) → C4 (Church Handover)**
- การเลื่อนระดับขับเคลื่อนด้วย **R-Score = S×0.4 + Q×0.3 + I×0.3** คำนวณอัตโนมัติเมื่อ S/Q/I เปลี่ยน
- **Journey Architect** (claude-opus-4-6) เป็น agent รับผิดชอบวางแผนเส้นทาง C1→C4 และ promote funnel
- **C4 (Church Handover)** เป็นระดับสุดท้าย — ส่งผู้ใช้เข้าคริสตจักรท้องถิ่น ดำเนินการโดย Local Connector + `handover.py`

## C-Stage Detail

| Stage | Funnel | R-Score | Personas | กลยุทธ์หลัก |
|-------|--------|---------|----------|-------------|
| C1 | Engage | 0.0–0.3 | P1 (Seeker's Friend), P2 (Youth Mentor) | วิดีโอ, ควิซ, สร้างความไว้วางใจ |
| C2 Connect | Connect | 0.3–0.5 | P3 (Faith Explorer), P4 (Hope Giver), P5 (Grateful Soul), P6 (Messenger of Peace) | พระคัมภีร์เบาๆ, สร้างความสัมพันธ์ |
| C2 Transform | Transform | 0.5–0.75 | P7 (Visionary Guide), P9 (Liberator), P10 (Life Restorer), P11 (Identity Affirmer) | Academy, อธิษฐาน, เติบโตความเชื่อ |
| C3 | Send | ≥ 0.85 | P12 (Mission Motivator) | จับคู่อาสาสมัคร, ชวนเพื่อน, คริสตจักร |
| C4 | Stewardship | — | Local Connector | Church matching + physical handover |

## การปรับระดับ (Promotion)

### สูตร R-Score
```
R = S × 0.4 + Q × 0.3 + I × 0.3

S = Sentiment Score  (อารมณ์/จิตวิญญาณ, -1.0 ถึง +1.0)
Q = Quiz/Quiet Time  (ความสม่ำเสมอ, 0.0–1.0)
I = Interaction      (การมีส่วนร่วม, 0.0–1.0)
```

### API ที่ใช้
```
GET   /api/v1/users/{user_id}/circle          → circle stage ปัจจุบัน
PATCH /users/{user_id}/scores                 → อัปเดต S/Q/I → R auto-recalculate → may auto-promote
POST  /users/{user_id}/promote                → เลื่อนขั้น {to_stage: Connect|Transform|Send}
GET   /users/{user_id}/profile                → full profile รวม circle_level, funnel_stage, r_score
```

### Tools ที่ Journey Architect ใช้
- `middleware_get_funnel` — ดึง funnel + R-score ก่อนทุก session
- `middleware_update_scores` — อัปเดต S/Q/I (trigger auto-promote)
- `middleware_promote_funnel` — promote manually
- `handoff_register` (Local Connector) — ลงทะเบียน C4 handover

## Journey Architect Decision Matrix

```yaml
C1_Engage:    แนะนำวิดีโอเบาๆ, เกมจิตวิทยา, ชวนตอบควิซ
C1_Connect:   เริ่มเรื่องพระคัมภีร์เบาๆ, ชวนเข้ากลุ่ม
C2_Transform: บทเรียนพระคัมภีร์ลึกขึ้น, ชวนอธิษฐาน
C3_Send:      เตรียมเข้าคริสตจักร, จับคู่อาสาสมัคร
```

## C4 Handover Process

```
1. ตรวจ funnel_stage == Send + r_score ≥ 0.85
2. ดึง spiritual_dna + จังหวัด (province)
3. local-connector ค้นหา HoB ใกล้ที่สุด (church_match_local)
4. แจ้ง HoB leader ผ่าน LINE (notify_hob_leader)
5. อัปเดต funnel_stage → C4
6. บันทึก funnel_transitions table
7. ติดตาม baptism_tracking (post-C4)
```

## Coin Incentives ตาม C-Stage

เหรียญเป็น positive reinforcement นำผู้ใช้ C1→C4:

| กิจกรรม | Coins |
|---------|-------|
| ดูวิดีโอจบ | 5 |
| ทำ Quiz ผ่าน | 5 |
| แนะนำเพื่อน | +20 |
| จบบท Academy | ตาม completion_reward_coins |
| แชร์ testimony | +10 |

บางรางวัลกำหนด `required_circles: ["C3"]` — เฉพาะ C3+ เท่านั้น

## Service Files

```
middleware/services/
  funnel_service.py     — Funnel stage transitions logic
  rscore.py             — R-score calculation
  handover.py           — C3→C4 church handover
  c2_flow.py            — C2→C3 learner flow (affinity, recommendations)

DB tables:
  funnel_transitions    — ประวัติการเปลี่ยน stage
  c2_recommendations    — triggered by affinity_score > 0.7
  spiritual_dna         — r_score log, interest_tags
  baptism_tracking      — ติดตามบัพติศมา (post-C4)
```

## Safety Override

Sentinel บังคับ **Persona 8 (The Healer)** เมื่อ S ≤ -0.3 ในทุก C-Stage  
S ≤ -0.9 → SOSVE FREEZE — ห้าม promote circle ขณะ FREEZE อยู่

## Related

- [[concepts/circle-level-progression]]
- [[concepts/funnel-stages]]
- [[concepts/spiritual-scores]]
- [[concepts/sentinel-safety]]
- [[sources/aunjai-swarm-agent-flow]]
- [[entities/academy-lmm]]
