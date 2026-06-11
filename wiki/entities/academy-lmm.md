---
title: "Academy (LMM)"
type: entity
tags: [academy, lmm, learning, certificate, lessons, post-cert, topic-affinity]
created: 2026-06-05
updated: 2026-06-11
sources: 2
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

## Post-Certificate Journey (v1.1 Phase 3) — เพิ่ม 2026-06-08

หลัง user ได้รับใบประกาศ ระบบส่ง follow-up อัตโนมัติ Day 0/2/5/10/14/30  
รายละเอียด → [[concepts/post-cert-journey]]

## Topic Affinity System — เพิ่ม 2026-06-08

EMA scoring per user per topic tag หลัง quiz completion (α=0.2)  
`curriculum_sets.topic_tags TEXT[]` ใช้ label topic สำหรับ journey recommendation  
รายละเอียด → [[concepts/topic-affinity]]

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
- [[concepts/post-cert-journey]]
- [[concepts/topic-affinity]]
- [[sources/modules]]
- [[sources/work-log-2026-06-08-to-11]]
