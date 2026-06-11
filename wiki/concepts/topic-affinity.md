---
title: "Topic Affinity System"
type: concept
tags: [topic-affinity, ema, quiz, academy, personalization]
created: 2026-06-11
updated: 2026-06-11
sources: 1
---

# Topic Affinity System

**migration:** 0016 | **service:** topic_affinity_service.py

## Description

EMA-based per-user per-topic scoring ที่อัปเดตทุกครั้งหลัง user ทำ quiz เพื่อ personalize content recommendation และ journey path

## EMA Formula (α = 0.2)

```
affinity_score = old × 0.8 + (score × 100) × 0.2   # สูง = user เก่งหัวข้อนี้
weakness_score = old × 0.8 + ((1-score) × 100) × 0.2  # สูง = user ยังอ่อนหัวข้อนี้
```

- α = 0.2: lower = drift ช้า (conservative), higher = reactive มากขึ้น
- score: 0.0–1.0 (accuracy ต่อ quiz submission)

## Database (table: `topic_affinity`)

| Column | ความหมาย |
|--------|----------|
| user_id + topic_tag | UNIQUE key |
| affinity_score | 0–100, สูง = รู้เรื่องนี้ดี |
| weakness_score | 0–100, สูง = ยังอ่อน |
| total_responses / correct_count / incorrect_count | สถิติรวม |

## Integration

- เรียกจาก `process_quiz_complete()` ใน `line_webhook.py` — additive, fail-safe
- ([[concepts/post-cert-journey]]) — Day 14 ใช้ affinity เลือก Next Lesson
- Users page ใน Admin UI แสดง `topic_affinity_healing`, `topic_affinity_faith`, `topic_affinity_community`
- `curriculum_sets.topic_tags TEXT[]` เป็น label ที่ใช้จับคู่

## Topic Tags ตัวอย่าง

(single source) เช่น `การอธิษฐาน`, `ความสัมพันธ์กับพระเจ้า`, `C1`, `healing`, `faith`, `community`

## Related

- [[entities/academy-lmm]]
- [[concepts/post-cert-journey]]
- [[concepts/circle-level-progression]]
- [[sources/work-log-2026-06-08-to-11]]
