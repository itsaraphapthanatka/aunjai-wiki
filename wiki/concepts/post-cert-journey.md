---
title: "Post-Certificate Journey Map"
type: concept
tags: [academy, post-cert, journey, automation, redis, background-worker]
created: 2026-06-11
updated: 2026-06-11
sources: 1
---

# Post-Certificate Journey Map

**เวอร์ชัน:** v1.1 Phase 3 (migration 0013)

## Description

Background service ส่ง follow-up message อัตโนมัติหลัง user ได้รับใบประกาศ — เป็น "ดูแลหลังเรียน" ที่ไม่ต้องมีคนมานั่งเฝ้า

## Timeline Per User

| Day | เนื้อหา | ประเภท |
|-----|---------|--------|
| 0 | Celebration + Share button | ทันทีที่กดรับใบ |
| 2 | AI Reflection Prompt (ใช้ prayer context) | Automated |
| 5 | AI Application Challenge (7-day challenge) | Automated |
| 10 | Personal Growth Report Flex Card | Data-driven |
| 14 | Next Lesson Recommendation (ดู topic_tags) | AI + Prereq |
| 30 | 1-Month Callback | Automated |

## State Machine

`ACTIVE → COMPLETED | PAUSED | SKIPPED`

## Phase 3 Additions

- **Redis flags** per user:
  - `aunjai:journey_reflect:{line_id}` (TTL 72h) — รอรับ reflection response Day 2
  - `aunjai:journey_challenge:{line_id}` (TTL 10 days) — ติดตาม 7-day challenge
- **`capture_journey_response()`** — hook ใน line_webhook.py รับ keyword checkin (ทำแล้ว, done, เสร็จ, ฯลฯ)
- **`send_challenge_reminders()`** — nudge "วันที่ X/7" ทุกเช้า Day 6-11

## Public API

```python
start_journey(db, user_id, curriculum_set_id, certificate_id)
process_due_journeys(db)        # background worker ทุกชั่วโมง
capture_journey_response(line_id, text)  # hook ใน line_webhook
send_challenge_reminders(db)    # daily nudge
```

## Database

- `post_cert_journeys` — 1 row per user-set pair (UNIQUE constraint)
- `journey_day_logs` — audit log ทุกข้อความที่ส่ง
- `curriculum_sets.topic_tags TEXT[]` — ใช้สำหรับ Day 14 recommendation

## Integration

- ([[entities/academy-lmm]]) — triggered หลัง certificate claim
- ([[concepts/topic-affinity]]) — Day 14 recommendation ใช้ topic_tags + user affinity
- ([[concepts/message-pipeline]]) — ส่งผ่าน LINE Push API ไม่ผ่าน OpenClaw pipeline

## Related

- [[entities/academy-lmm]]
- [[concepts/topic-affinity]]
- [[concepts/circle-level-progression]]
- [[sources/work-log-2026-06-08-to-11]]
