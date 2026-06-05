---
title: "Spiritual Scores (DNA)"
type: concept
tags: [scores, spiritual-dna, sentiment, sos-trigger]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# Spiritual Scores (Spiritual DNA)

## Description
สี่ตัวเลข (0.0–1.0 หรือ -1.0–1.0) ที่วัดสุขภาพจิตวิญญาณของ user
ใช้สำหรับ SOS trigger, funnel progression, และ campaign targeting

## The Four Scores

| Score | ชื่อ | Range | ความหมาย |
|---|---|---|---|
| R | Relationship | 0–1 | engagement กับ platform และชุมชน |
| S | Spiritual/Sentiment | -1 to 1 | สุขภาพจิตใจ/วิญญาณ |
| Q | Quiet Time | 0–1 | ความสม่ำเสมอในการภาวนา |
| I | Involvement | 0–1 | การมีส่วนร่วมกิจกรรม |

## Critical Threshold
**S-score ≤ -0.9** → SOS alert triggered automatically

## SOS Priority from S-score
- Critical: s ≤ -0.9 (🔴)
- Urgent: s ≤ -0.7 (🟠)
- Moderate: s ≤ -0.5 (🟡)
- Low: s > -0.5 (🟢)

## Topic Affinities (additional)
สามตัวเลข 0.0–1.0 แยกจาก four scores:
- topic_affinity_healing
- topic_affinity_faith
- topic_affinity_community

## Display
- Admin users page: 4 progress bars
- SOS drawer: S-score + R-score prominently displayed
- Color coding: green ≥ 0.7, yellow ≥ 0.4, red < 0.4

## Related
- [[entities/sos-command-center]]
- [[concepts/funnel-stages]]
- [[sources/aunjai-system-overview]]
