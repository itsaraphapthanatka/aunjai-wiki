---
title: "Smart Access Links Module"
type: entity
tags: [access-links, qr-code, deeplink, approval-workflow, tags]
created: 2026-06-11
updated: 2026-06-11
sources: 1
---

# Smart Access Links Module

**เวอร์ชัน:** v7.0 (สร้างใหม่ทั้งหมด 8–11 มิ.ย. 2026)

## Description

โมดูลสร้าง QR Code และ Deeplink อัตโนมัติสำหรับแคมเปญและ event ต่างๆ ผูก FEBC tags เข้า link เพื่อ auto-tag user เมื่อ scan/follow

## Architecture

```
Staff สร้าง Link (web / Telegram)
    ↓
Draft → PendingL1 → PendingL2 → Active
              ↑ regional_coord+    ↑ super_admin only
    ↓ (เมื่อ Active)
/go/{code} redirect endpoint
    ↓
Redis pending_follow:{line_id} (TTL 30 min)
    ↓ (เมื่อ user follow LINE OA)
Apply tags + log scan event
```

## Database Tables (migration 0015)

| ตาราง | ความหมาย |
|---|---|
| `access_links` | หลัก — metadata, status, scan/follow counts |
| `access_link_tags` | tag_name ที่ผูกกับ link (string, consistent กับ users.febc_tags) |
| `access_link_scans` | log ทุก scan event + IP, user_agent, tags_applied |
| `access_link_approvals` | audit trail ทุก approval/rejection |

## Status Workflow

`Draft → PendingL1 → PendingL2 → Active → Paused → Expired`

- L1 approval: regional_coord+ (role ≥ 2)
- L2 approval: super_admin เท่านั้น (role ≥ 3)

## Channel Types

Event, Social, Print, Referral, Internal

## QR Code

- สร้างด้วย `qrcode` Python library, RoundedModuleDrawer
- รองรับ custom fill color (hex)
- บันทึกที่ `/app/static/qr/{code}.png`

## Admin UI

- `/admin/access-links` — list + filter by status/channel/region + summary cards
- `/admin/access-links/new` — form สร้าง link
- `/admin/access-links/[id]` — detail + approval + QR preview + scan timeline

## Permissions

view / create / edit / delete / export (granular per staff role)

## Staff Members (Telegram extension)

เพิ่ม columns: `tg_chat_id`, `tg_username`, `tg_region`, `tg_role`, `tg_verified`, `tg_setup_token`

## Related

- [[entities/tags-management]]
- [[concepts/tag-groups]]
- [[sources/work-log-2026-06-08-to-11]]
