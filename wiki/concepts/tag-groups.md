---
title: "Tag Groups"
type: concept
tags: [tags, groups, classification, febc]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# Tag Groups

## Description
ระบบจัดกลุ่ม FEBC Tags เพื่อให้ filter และทำความเข้าใจได้ง่ายขึ้น

## Two-tier System
1. **Built-in groups** (14 กลุ่ม) — auto-detected จาก prefix, ลบไม่ได้
2. **Custom groups** — admin สร้างเอง, มีสีและ description, ลบได้

## Auto-detection Logic (`_auto_group()`)
```python
"CENTER_" → Center
"EVENT_"  → Event
"ACTIVITY_" → Activity
"TARGET_"   → Target
"RESPOND_"  → Respond
"MODEL_"    → Model
"PROJECT_"  → Project
"RICHMENU_" → Richmenu
"DL_"       → Deep Link
"HOME_"     → Home
"DRIVER_"   → Driver
"CONTENT_"  → Content
"#"         → Campaign
else        → Other
```

## Group Priority
Manual `group_name` ใน DB overrides auto-detection เสมอ

## "Other" Group
Tags ที่ prefix ไม่ match pattern ใดเลย ปัจจุบัน 152 tags (ใหญ่ที่สุด)
Known uncategorized: MEMBER_, NEW_, SUB_MENU_, FILTER_, Staff_, Evnt_ (typo)

## Color Options (12)
blue, purple, green, orange, red, pink, teal, yellow, indigo, cyan, lime, slate

## DB Storage
- `febc_tags.group_name` — group ของ tag แต่ละอัน
- `febc_tag_groups` table — custom group definitions พร้อม color

## Related
- [[entities/tags-management]]
- [[entities/febc-middleware]]
- [[sources/febc-tags-system]]
