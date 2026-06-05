---
title: "Volunteer Escalation"
type: concept
tags: [volunteer, sos, escalation, line]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Volunteer Escalation

## Description
กระบวนการส่งต่อ SOS case จาก staff ไปยัง volunteer ผ่าน LINE notification
เป็นส่วนหนึ่งของ SOS response chain (หลัง staff takeover)

## State Machine
```
waiting → accepted (< 15 min)
        → timeout  (> 15 min) → resend / staff takeover
accepted → resolved
         → returned → staff takeover
```

## Visual Indicators
- 🟣 waiting — อาสารับแจ้งแล้ว รอกดรับ
- 🟡 timeout — เกิน 15 นาที ต้องการ staff action
- 🟢 accepted — อาสากำลังดูแล
- 🔵 returned — ส่งกลับ staff

## Staff Actions on Timeout
- "รับเคสมาเอง" → staff takeover
- "ส่งซ้ำอีกครั้ง" → resend LINE invite (max 1 retry)

## Volunteer Requirements
- ต้องมี LINE user ID ลงทะเบียนในระบบ
- ต้องมี SOS permission ใน custom role

## VolunteerEscalationModal
- Search + filter volunteers
- แสดง: ชื่อ, role, LINE status (✅/⚠️), active cases count
- Select multiple volunteers
- Optional note to volunteer
- ส่งแบบ serialize (ทีละคน เพื่อ avoid rate limit)

## Related
- [[entities/sos-command-center]]
- [[entities/arc-console]]
- [[sources/sos-flow]]
