---
title: "Campaign System (CMM)"
type: entity
tags: [campaigns, cmm, line, broadcast, coins]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# Campaign System (CMM v5.1/5.2)
**Campaign Management Module**

## Description
ระบบจัดการ LINE broadcast campaigns พร้อม coin reward, targeting, และ ROI tracking

## Campaign Fields
- title, start/end dates, status (DRAFT/ACTIVE/PAUSED/COMPLETED)
- budget_cap_coins, current_burn_coins
- tags (FEBC tags สำหรับ audience targeting)
- rules: CampaignRule[] (VIDEO_WATCH, QUIZ_PASS, REFERRAL_CONVERT)
- deep_link_chapter_id (Golden Bridge → lesson link)
- retargeting config, bonus_coins

## Budget System
- Global "Blessing Budget" (coin → baht value)
- Per-campaign budget cap
- Alert thresholds: soft → hard → emergency brake
- Status: ok | soft | hard | emergency

## Broadcast Types
- Video Flex Message (YouTube)
- Chapter Deep Link (single lesson)
- Curriculum Set (lesson series)
- Promo message + banner + video

## ROI Metrics
- video_watch_count, quiz_pass_count, open_chapter_count
- cpb (cost per baptism — manual count)
- cpa (cost per video watch / C1→C2 proxy)
- cpq (cost per quiz pass / C2→C3 proxy)
- daily_burn trend

## Tag Integration
TagSelector component โหลดจาก `GET /admin/tags`
Groups และสีตรงกับ Tags Management
Session cache ต่อ browser tab

## Related
- [[entities/tags-management]]
- [[entities/academy-lmm]]
- [[concepts/blessing-budget]]
- [[concepts/funnel-stages]]
