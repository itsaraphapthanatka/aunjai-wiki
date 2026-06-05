# SOS Flow — Spiritual Emergency System

## Overview
The SOS system is น้องอุ่นใจ's crisis intervention layer. It detects users in emotional/spiritual distress and routes them through a structured response chain.

## Trigger
- User's S-score drops to ≤ -0.9 (detected by backend sentiment analysis)
- Or: admin manually creates a case via `/admin/sos/create-case`

## Alert Object Fields
```
id, user_id, user_nickname, user_circle_level, user_province
s_score_at_trigger, r_score_at_trigger
priority: critical | urgent | moderate | low
status: open | inprogress | resolved
trigger_reason: text description
wait_time_seconds: time since case opened
assigned_to, assigned_admin_name
ai_status: AUTOPILOT | PAUSED
current_pipeline: SOS_COMMAND | VOLUNTEER_ESCALATED | VOLUNTEER_ACTIVE
volunteer_id, volunteer_name, volunteer_status, escalated_at
escalation_timeout_at, escalation_retry_count
```

## Response Chain

### Stage 1: AI AUTOPILOT
- ARC (Aunjai Rescue Console) automatically converses with user
- ai_status = "AUTOPILOT"
- Case shows in Command Center

### Stage 2: Staff Takeover
- Admin clicks "Take Over Chat"
- `POST /admin/sos/takeover` → ai_status = "PAUSED"
- ARC Console overlay opens
- Admin chats manually using quick templates or free text

### Stage 3: Resolution Options

**A. Direct Resolve**
- `POST /admin/sos/resolve` with `send_closing_message: true`
- Status → resolved, ai_status → AUTOPILOT

**B. Volunteer Escalation**
- Admin opens VolunteerEscalationModal
- Selects 1+ volunteers (filtered by SOS permission)
- `POST /admin/sos/escalate-volunteer` per volunteer
- LINE notification sent to volunteer with "กดรับเคส" button
- volunteer_status → waiting

**Volunteer timeout flow:**
- If no response within 15 minutes: volunteer_status → timeout
- Staff admin sees amber warning, can:
  - "ส่งซ้ำอีกครั้ง" → `POST /admin/sos/escalation-resend`
  - "รับเคสมาเอง" → takeover via `POST /admin/sos/takeover`

**Volunteer accepted:**
- volunteer_status → accepted
- Volunteer chats with user via their LINE interface

**Volunteer returned:**
- volunteer_status → returned
- Staff must take back via ARC

**C. Field Escalation**
- Via ARC Console Actions → HoB (House of Blessing) assignment

## KPI Metrics
- active_sos: count of open cases
- critical_count: cases with priority=critical
- avg_response_time_seconds
- handover_to_field_24h: cases escalated to field in last 24h

## WebSocket Events
Connection: `wss://host/aunjai-api/api/v1/sos/ws`
Auto-reconnect: 5s on disconnect
Full refresh: every 30s (safety net)
Wait-time ticker: every 15s (live counter)

Event types:
- new_sos → push new alert to list
- sos_resolved → mark resolved
- alert_update → case state machine transitions

## Quick Message Templates
1. "ยืนยันการรับเรื่อง" — น้องอุ่นใจรับเรื่องแล้วนะคะ 💙 พี่อยู่ตรงนี้ฟังน้องค่ะ
2. "ขออธิษฐานเผื่อ" — ขอให้พระเจ้าทรงประทานความสุขุมและความหวังให้กับน้อง 🙏
3. "ปลอบประโลม" — น้องไม่ได้อยู่คนเดียวนะคะ มีพระเจ้าและพี่ๆ อยู่กับน้องเสมอ 💛

## Nearest HoB Feature
- `GET /sos/nearest-hob?lat=&lng=`
- Returns House of Blessing contacts within range
- Shows leader name, phone, distance in km
- Phone click-to-call from drawer

## Admin Permissions
- canCreate: สร้างเคส SOS ใหม่
- canEdit: take over, resolve, escalate
- canDelete: ลบเคส
- canExport: download CSV report (`GET /admin/sos/export`)

## Case Navigation via URL
- `/admin/sos?caseId=UUID` → auto-open ARC overlay
- `/admin/sos?caseId=UUID&panel=escalate` → open escalation panel
(Used by LINE Flex Message deep links)
