---
title: "Automated Lifecycle Services"
type: concept
tags: [automation, morning-greeting, night-prayer, post-cert, background-worker, redis]
created: 2026-06-11
updated: 2026-06-11
sources: 1
---

# Automated Lifecycle Services

บริการที่วิ่งอัตโนมัติ ไม่ต้องรอ user ส่งข้อความก่อน — ส่ง LINE Push Message โดยตรงผ่าน LINE API

## Morning Greeting Service (v5 Phase 3)

**เวลา:** 07:00–08:30 ICT ทุกวัน  
**target:** active users ทุกคน

Phase 3 additions (บน phase 2 streak/milestone):
- **Re-engagement detection** — users ที่หายไปนาน ได้ special comeback message
- **Unresolved prayer tracking** — ถ้า user มี prayer request ค้าง → ถามติดตามผล
- **Interest tags enrichment** — ดู febc_tags + topic_affinity เพื่อ personalize greeting topic
- **Day-of-week rhythm** — จันทร์ = motivational, ศุกร์ = recap, อาทิตย์ = spiritual

Fallback templates แยก 4 circle levels (C1/C2/C3/C4) ใช้เมื่อ AI ล่มเท่านั้น

## Night Prayer Service (ใหม่ 2026-06-08)

**เวลา:** 21:00 ICT (14:00 UTC) ทุกคืน  
**target:** users ที่มี prayer request ค้าง สร้างภายใน 24h

- หา `prayer_requests` status New/InProgress อายุ ≤ 24h
- ส่งข้อความหนุนใจ + คืนนี้อธิษฐานให้
- Redis dedup: `aunjai:night_prayer_user:{user_id}:{date_ict}` TTL 72000s (ไม่ส่งซ้ำ)

## Post-Certificate Journey Worker

**ทุก 1 ชั่วโมง:** `process_due_journeys(db)` + `send_challenge_reminders(db)`  
รายละเอียดเพิ่มเติม → ([[concepts/post-cert-journey]])

## Feature Flags

ทุก service รองรับ feature flags ปิด/เปิด:
- `quiz_enabled` — เปิด/ปิด quiz flow และ topic affinity collection
- `coin_enabled` — เปิด/ปิด coin award events

API: `GET/PUT /admin/feature-flags/{key}` — permission gated

## Guardian Rules (ทุก service ต้องปฏิบัติ)

- **is_onboarded gate** — ห้ามส่ง proactive ถ้า user ยังไม่ onboard
- **48h cooldown** — ห้าม proactive ซ้ำภายใน 48h (ยกเว้น admin override)
- **S-score threshold** — S ≤ -0.3 → Gentle Care Mode งดแคมเปญ · S ≤ -0.9 → FREEZE
- **Post-video cooldown** — หลังส่งวิดีโอ → ห้าม proactive แทรก 24h จนกว่า user จะ interact

## Related

- [[concepts/post-cert-journey]]
- [[concepts/topic-affinity]]
- [[concepts/sentinel-safety]]
- [[concepts/message-pipeline]]
- [[sources/work-log-2026-06-08-to-11]]
