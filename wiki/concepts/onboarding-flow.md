---
title: "Onboarding Flow"
type: concept
tags: [onboarding, user, profile, line]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Onboarding Flow

กระบวนการสร้างโปรไฟล์ผู้ใช้ใหม่ใน LINE chatbot — trigger เมื่อ `is_onboarded = false`

## 4 ขั้นตอน

| ขั้น | ข้อมูล | Field | Validation |
|-----|--------|-------|------------|
| 1 | ชื่อเล่น | `user_set_nickname` | — |
| 2 | ชื่อ-นามสกุล | `first_name` / `last_name` | — |
| 3 | อายุ | — | validate 1–120 |
| 4 | จังหวัด | — | Thai Province list |

เมื่อครบทั้ง 4 ขั้น → `is_onboarded = true`

## Resumable

(confirmed) หากผู้ใช้ข้ามขั้นตอนใด `is_onboarded` ยังเป็น `false` — สามารถกลับมาทำต่อได้ในภายหลัง ไม่ต้องเริ่มใหม่

## Trigger Point

Middleware [[concepts/keyword-routing]] PATH D ตรวจ `is_onboarded` — ถ้า false จะเบี่ยงไป onboarding ก่อนถึง ARC-GATE

## ความสัมพันธ์กับ Persona

หลัง onboard สำเร็จ front-desk จะเลือก Persona 1–12 โดยใช้ Circle level + R_score + sentiment (ดู [[concepts/aunjai-swarm]] section front-desk)

## Related

- [[concepts/aunjai-swarm]]
- [[concepts/keyword-routing]]
- [[concepts/funnel-stages]]
- [[concepts/spiritual-scores]]
- [[sources/aunjai-swarm-agent-flow]]
