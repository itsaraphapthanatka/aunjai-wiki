---
title: "SOS Flow — Spiritual Emergency System"
type: source
tags: [sos, crisis, arc, volunteer, websocket]
created: 2026-06-05
updated: 2026-06-05
sources: 1
---

# SOS Flow

**Raw source:** `raw/sos-flow.md`

## Key Claims
- Trigger: S-score ≤ -0.9 (auto) หรือ admin สร้างมือ
- Response chain: AI Autopilot → Staff Takeover → Volunteer Escalation / Field
- Real-time via WebSocket: auto-reconnect 5s, full refresh 30s

## Priority Levels
| Priority | S-score | สี |
|---|---|---|
| Critical | ≤ -0.9 | 🔴 |
| Urgent/High | ≤ -0.7 | 🟠 |
| Moderate | ≤ -0.5 | 🟡 |
| Low | > -0.5 | 🟢 |

## Volunteer States
waiting → timeout (>15min) → accepted / returned

## Quick Templates
1. ยืนยันการรับเรื่อง
2. ขออธิษฐานเผื่อ
3. ปลอบประโลม

## Key Endpoints
```
POST /admin/sos/takeover          pause AI, admin takes control
POST /admin/sos/resolve           close case, send closing msg
POST /admin/sos/escalate-volunteer send to volunteer via LINE
POST /admin/sos/escalation-resend  resend volunteer invite
POST /admin/sos/create-case       manual case creation
GET  /admin/sos/export            CSV report
```

## Deep Link Navigation
- `?caseId=UUID` → opens ARC overlay
- `?caseId=UUID&panel=escalate` → opens escalation panel

## Related
- [[entities/sos-command-center]]
- [[entities/arc-console]]
- [[concepts/volunteer-escalation]]
- [[concepts/spiritual-scores]]
