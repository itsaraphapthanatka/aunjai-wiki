---
title: "FEBC Middleware"
type: entity
tags: [middleware, febc, api, tags]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# FEBC Middleware
**middleware.febradio.org**

## Description
External API ของ FEBC Thailand ที่เป็น source of truth สำหรับ FEBC Tags และ data อื่นๆ

## Key Endpoints Used
- `GET /api/tags` → รายชื่อ tags ทั้งหมด (364 tags, returns string[])

## Role in System
- master tag list (upstream source)
- aunjai admin ดึง tags list จากที่นี่ทุกครั้งที่ render Tags Management
- merge กับ febc_tags DB table (metadata layer)

## Notes
- (single source) — ไม่มี fallback ถ้า middleware ล่ม, tags ใน admin จะแสดงจาก DB เท่านั้น
- Tags ใน middleware อาจไม่ตรงกับ tags ใน user DB (219 vs 364)

## Related
- [[entities/febc-thailand]]
- [[entities/tags-management]]
- [[concepts/tag-groups]]
