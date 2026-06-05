---
title: "FEBC Tags System"
type: source
tags: [tags, febc, groups, user-management]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# FEBC Tags System

**Raw source:** `raw/febc-tags-system.md`

## Key Claims
- 364 tags จาก middleware.febradio.org (source of truth)
- 219 unique tags พบในข้อมูล users จริง
- 8,625 จาก 10,048 users มี febc_tags
- Tags เก็บเป็น PostgreSQL ARRAY ใน `users.febc_tags`

## Top 5 Tags
1. Center_พิษณุโลก — 2,583 users
2. Center_ภูเก็ต — 2,532 users
3. richmenu_สหกิจ — 1,577 users
4. MODEL_พิษณุโลก — 1,150 users
5. richmenu_new_คริสตจักรแห่งนิมิตพรหมพิราม — 1,099 users

## Group Detection Logic
`_auto_group()` function ใน `middleware/routes/admin.py`
ตรวจ prefix ของชื่อ tag → assign group
Tags ที่ไม่ match → group = "Other"

## Notable Uncategorized (Other)
MEMBER_, NEW_, SUB_MENU_, FILTER_, Staff_, Evnt_ (typo of Event_)

## Available Days Field
`null` = tag ติดถาวร
`N` = tag หมดอายุ N วันหลังจากถูกติด

## API Key Flow
```
GET /admin/tags → merge middleware tags + DB metadata + member_count
PATCH /admin/tags/{name} → set group, description, available_days
POST /users/{id}/tags → add tag to user
DELETE /users/{id}/tags/{tag} → remove tag from user
POST /admin/tags/bulk-add → N users at once
POST /admin/tags/bulk-remove → N users at once
```

## Related
- [[entities/tags-management]]
- [[entities/febc-middleware]]
- [[concepts/tag-groups]]
- [[sources/modules]]
