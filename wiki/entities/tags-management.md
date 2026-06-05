---
title: "Tags Management"
type: entity
tags: [tags, module, febc, groups]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# Tags Management
Route: `/admin/tags`

## Description
หน้าจัดการ FEBC Tags — แสดง, กรอง, แก้ metadata, และจัดการ users ต่อ tag
สร้างขึ้นใหม่ใน session 2026-06-05

## Data Sources (merged)
1. middleware.febradio.org/api/tags → 364 tags (ชื่อ)
2. febc_tags DB table → metadata (group, description, available_days)
3. users.febc_tags → member_count (real-time count)

## Features
- Group filter chips (14+ groups)
- Tag cards แสดง group color + description + member count + available_days
- Edit modal: group picker (preset + custom), description, available_days
- Create tag modal
- Detail view: member list + search backend real-time
- Add user: search 8,600+ users by name/display_name
- Bulk remove tags from multiple users
- Group Manager: สร้าง custom groups + color picker (12 สี)

## TagSelector (Campaigns)
Component ที่ใช้ใน CampaignBuilder
- โหลดจาก `GET /admin/tags` (แทน FEBC middleware โดยตรง)
- Groups ตรงกับ Tags Management
- Session-level cache

## Related
- [[concepts/tag-groups]]
- [[entities/febc-middleware]]
- [[entities/campaign-system]]
- [[sources/febc-tags-system]]
