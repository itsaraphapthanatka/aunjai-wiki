---
title: "Academy (LMM)"
type: entity
tags: [academy, lmm, learning, certificate, lessons]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Academy (LMM)
**Learning Management Module**

## Description
แพลตฟอร์มเรียนรู้ออนไลน์ของน้องอุ่นใจ มีบทเรียนเดี่ยวและชุดบทเรียน

## Single Lessons (academy_chapters)
- chapter_number, title, description, video_url
- pass_threshold (คะแนนผ่าน)
- unlock_type: always | previous_pass | custom
- Questions parsed จาก PDF via parse jobs
- Progress tracked per user

## Curriculum Sets (V3)
- CurriculumSet → CampaignLesson[] (ordered)
- Prerequisites between sets
- setCompletionBonusCoins

## Certificate System
- PDF generation (reportlab)
- ชื่อ user วางตำแหน่งด้วย x,y coordinates
- Postal delivery tracking:
  PENDING_DELIVERY → PACKED → SHIPPED → IN_TRANSIT → DELIVERED
- Thailand Post integration

## Learner Analytics
- Dropout detection (on_track | slow | dropout_risk)
- Score averages, completion rates
- Spiritual DNA per learner

## Lesson Types
- VIDEO — YouTube video + quiz
- TEXT — reading content + quiz

## Related
- [[entities/campaign-system]]
- [[concepts/certificate-delivery]]
- [[sources/modules]]
