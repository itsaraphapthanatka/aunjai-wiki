# อุ่นใจ — Circle Level Progression (C1→C2→C3→C4)

_Clipped: 2026-06-06 | Source: workspace/aunjai-swarm/ + workspace/AUNJAI-BOOTSTRAP.md_

---

## ภาพรวม C-Stage System

ระบบอุ่นใจแบ่งเส้นทางการเติบโตทางจิตวิญญาณของผู้ใช้ออกเป็น 4 ระดับ (Circle Level) โดย Journey Architect เป็น agent หลักที่วางแผนและกำหนดจังหวะการย้ายระดับ

```
C1 (Engage) → C2 (Connect/Transform) → C3 (Send) → C4 (Stewardship/Church Handover)
```

---

## ระดับ C1 — Engage (ผู้มาใหม่)

| ฟิลด์ | ค่า |
|-------|-----|
| Funnel Stage | Engage |
| R-Score | 0.0 – 0.3 |
| Personas | P1 (Seeker's Friend), P2 (Youth Mentor) |
| Strategy | แนะนำวิดีโอเบาๆ, เกมจิตวิทยา, ชวนตอบควิซ, เริ่มเรื่องพระคัมภีร์เบาๆ |

**ลักษณะผู้ใช้:** ยังไม่รู้จักองค์กร, ไม่แน่ใจในความเชื่อ, ต้องการสร้างความไว้วางใจก่อน  
**Priority:** Nickname gate → Video → Quiz → สร้าง R-score เพื่อ promote

---

## ระดับ C2 — Connect / Transform (ผู้เชื่อมต่อและเปลี่ยนแปลง)

| ฟิลด์ | ค่า |
|-------|-----|
| Funnel Stage | Connect → Transform |
| R-Score | 0.3 – 0.75 |
| Connect Personas | P3 (Faith Explorer), P4 (Hope Giver), P5 (Grateful Soul), P6 (Messenger of Peace) |
| Transform Personas | P7 (Visionary Guide), P9 (Liberator), P10 (Life Restorer), P11 (Identity Affirmer) |
| Strategy | บทเรียนพระคัมภีร์ลึกขึ้น, ชวนอธิษฐาน, Academy chapters, c2_recommendations |

**ลักษณะผู้ใช้:** มีการมีส่วนร่วมสม่ำเสมอ, เริ่มสำรวจความเชื่อ, อาจมี SOS ที่ต้องดูแล  
**Data model:** `c2_recommendations` (triggered_by affinity_score > 0.7), `c2_flow.py`

---

## ระดับ C3 — Send (ผู้พร้อมรับใช้)

| ฟิลด์ | ค่า |
|-------|-----|
| Funnel Stage | Send |
| R-Score | ≥ 0.85 |
| Personas | P12 (Mission Motivator) |
| Strategy | เตรียมเข้าคริสตจักร, จับคู่อาสาสมัคร, ชวนแนะนำเพื่อน (+20 coins) |

**ลักษณะผู้ใช้:** พร้อมส่งต่อ, กำลังรับใช้หรือเตรียมตัว  
**Rewards:** ของรางวัลบางรายการกำหนด `required_circles: ["C3"]`

---

## ระดับ C4 — Stewardship / Church Handover (ส่งต่อคริสตจักร)

| ฟิลด์ | ค่า |
|-------|-----|
| Agent รับผิดชอบ | Local Connector (kimi-k2.5), Group 5 |
| Tools | `church_match_local`, `handoff_register`, `coverage_get_province` |
| Service | `handover.py` (C3→C4 church handover) |

**กระบวนการ:** ดึง spiritual_dna + แจ้ง HoB leader (LINE pastor) + set funnel→C4 + log `funnel_transitions`  
**API:** `/transition/handover`

---

## กลไกการปรับระดับ (Promotion Mechanism)

### สูตร R-Score
```
R = S × 0.4 + Q × 0.3 + I × 0.3

S = Sentiment Score  (อารมณ์/จิตวิญญาณ, -1.0 ถึง +1.0)
Q = Quiz/Quiet Time  (ความสม่ำเสมอ, 0.0–1.0)
I = Interaction      (การมีส่วนร่วม, 0.0–1.0)
```

### API Endpoints

```
GET   /api/v1/users/{user_id}/circle       → ดู circle stage ปัจจุบัน (C1–C3)
GET   /api/v1/users/{user_id}/profile      → profile + circle_level, funnel_stage, r_score
PATCH /users/{user_id}/scores              → อัปเดต S/Q/I → auto-recalculate R → may auto-promote
POST  /users/{user_id}/promote             → เลื่อนขั้น to_stage: Connect|Transform|Send
```

### Tool ที่ Agent ใช้

| Tool | Agent | หน้าที่ |
|------|-------|---------|
| `middleware_update_scores` | Journey Architect, Front-Desk | อัปเดต S/Q/I → R-score |
| `middleware_promote_funnel` | Journey Architect | promote to_stage |
| `middleware_get_funnel` | Journey Architect | ดึง funnel + R-score ปัจจุบัน |
| `user_update_rscore` | ทุก agent | shared tool |
| `handoff_register` | Local Connector | ลงทะเบียน C4 handover |

### Decision Matrix (Journey Architect)

```yaml
C1_Engage:    แนะนำวิดีโอเบาๆ, เกมจิตวิทยา, ชวนตอบควิซ
C1_Connect:   เริ่มเรื่องพระคัมภีร์เบาๆ, ชวนเข้ากลุ่ม
C2_Transform: บทเรียนพระคัมภีร์ลึกขึ้น, ชวนอธิษฐาน
C3_Send:      เตรียมเข้าคริสตจักร, จับคู่อาสาสมัคร
```

---

## Coin Incentives ตามระดับ

เหรียญถูกใช้เป็น positive reinforcement นำผู้ใช้ C1 → C4:

| กิจกรรม | Coins |
|---------|-------|
| ดูวิดีโอจบ | 5 |
| ทำ Quiz ผ่าน | 5 |
| แนะนำเพื่อน (Referral) | +20 |
| บทเรียน Academy จบ | ตาม completion_reward_coins |
| แชร์ testimony | +10 |

---

## Service Files ที่เกี่ยวข้อง

```
middleware/services/
  funnel_service.py     — Funnel stage transitions
  rscore.py             — R-score calculation
  handover.py           — C3→C4 church handover
  c2_flow.py            — C2→C3 learner flow (affinity, recommendations)

DB tables:
  funnel_transitions    — ประวัติการเปลี่ยน funnel stage
  c2_recommendations    — recommendation triggered by affinity > 0.7
  spiritual_dna         — interest_tags, q_score_log, r_score
  baptism_tracking      — ติดตามบัพติศมา (post-C4)
```

---

## Agents ต่อ Circle Group

| Group | Agents | Circle |
|-------|--------|--------|
| 1 — Front Line | main, front-desk, referral-tracker | C1/C2 |
| 2 — UX & Flow | journey-architect, media-delivery, aunjai-messenger | C1→C4 |
| 3 — Academy | academy-specialist, archivist, reward-manager | C3 |
| 4 — Soul Care | intercessory-coordinator, search-specialist, care-loop-closer | ทุก C |
| 5 — Stewardship | local-connector, insights-analyst | C4 |
| 6 — Memory | maac-sync, auto-qa | ทุก C |

---

## Safety Override (ไม่ขึ้นกับ C-Stage)

Sentinel agent ทำงานก่อนทุก agent — ถ้า S ≤ -0.3 บังคับ Persona 8 (The Healer) ทันที  
ถ้า S ≤ -0.9 → SOSVE FREEZE + แจ้ง Admin + สายด่วน 1323 — ไม่ promote circle ขณะอยู่ใน SOSVE
