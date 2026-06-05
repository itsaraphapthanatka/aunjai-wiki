# System Modules

## 1. Dashboard
Route: `/admin/`
- KPI cards: Followers, SOS Active, Coins, Prayers
- Funnel chart: Engage → Connect → Transform → Send counts
- SOS Alert banner (pulses red when active cases > 0)
- Budget status bar (Blessing Budget)
- Growth target progress (toward 50,000 users)
- Data sources: `/analytics/dashboard`, `/sos/summary`, `/coins/admin/summary`, `/campaigns/budget/status`

## 2. Users Management
Route: `/admin/users`, `/admin/users/[id]`
- List view: search, filter by funnel stage, paginated table
- User drawer (slide-in): scores, funnel journey, tags, coin balance, transactions
- User detail page: full profile, Spiritual DNA scores, topic affinity bars, FEBC tags, info
- Actions: change circle level, grant coins, flag SOS, edit profile
- febc_tags: string ARRAY — populated by LINE OA interactions and events
- API: `GET /users/?search=&funnel_stage=&febc_tag=&limit=&page=`

## 3. SOS Command Center
Route: `/admin/sos`
The "Spiritual ER" — crisis intervention system.

### Priority levels (from S-score):
- Critical: s ≤ -0.9 (immediate)
- Urgent/High: s ≤ -0.7
- Moderate: s ≤ -0.5
- Low: s > -0.5

### Case lifecycle:
1. Detected (s-score threshold) → SOS alert created
2. AUTOPILOT — ARC AI responds automatically
3. Staff takeover → ARC Console opens, AI paused
4. Resolution: direct close OR volunteer escalation OR field escalation

### Volunteer escalation states:
- waiting → timeout (>15 min) → accepted / returned

### ARC System (Aunjai Rescue Console):
- AI-driven chat with user during crisis
- Admin can "take over" to pause AI and chat manually
- Quick message templates for comfort/prayer
- Shows nearest HoB (House of Blessing) by location

### Real-time: WebSocket at `/sos/ws`
Events: new_sos, alert_update (arc_takeover, arc_resumed, case_resolved, volunteer_escalated, volunteer_accepted, volunteer_returned)

### Permissions: canCreate, canEdit, canDelete, canExport

## 4. Tags Management
Route: `/admin/tags`
FEBC tag system for categorizing users by activity, church, and campaign participation.

### Data sources:
- Tag names: from middleware.febradio.org/api/tags (364 tags, external)
- Tag metadata: febc_tags DB table (description, description_detail, available_days, group_name)
- Member counts: counted from users.febc_tags ARRAY in real-time

### Tag fields:
- name: tag identifier
- group_name: auto-detected or manually set
- description: short text
- description_detail: long explanation
- available_days: null = permanent, N = expires N days after attachment

### Groups (auto-detected from prefix + custom):
Center, Event, Activity, Target, Respond, Model, Project, Richmenu, Deep Link, Home, Driver, Content, Campaign, Other

### Tag groups (febc_tag_groups table):
Custom groups with color (12 color options) and description. Built-in groups cannot be deleted.

### Operations:
- View all tags grouped by category
- Filter by group (chip filter bar)
- Edit metadata per tag
- Add/remove users from tags (individual or bulk)
- Create custom groups with color picker
- Search by name or description

### User-tag endpoints:
- POST /users/{id}/tags — add tag
- DELETE /users/{id}/tags/{tag} — remove tag
- POST /admin/tags/bulk-add — bulk add
- POST /admin/tags/bulk-remove — bulk remove

## 5. Campaigns (CMM v5.1/5.2)
Route: `/admin/campaigns`
Campaign Management Module — LINE OA broadcast campaigns.

### Campaign fields:
- title, start_date, end_date, status (DRAFT/ACTIVE/PAUSED/COMPLETED)
- budget_cap_coins, current_burn_coins
- tags (from FEBC tags, used for audience targeting)
- rules: CampaignRule[] (trigger_type: VIDEO_WATCH, QUIZ_PASS, REFERRAL_CONVERT)
- deep_link_chapter_id, retargeting config, bonus_coins

### Budget system:
- Global Blessing Budget (coin value in baht)
- Per-campaign budget cap
- Soft/hard/emergency brake thresholds
- Budget status: ok → soft → hard → emergency

### LINE Broadcast:
- Send flex messages to users
- Video content (YouTube), chapter deeplinks, curriculum sets
- Promo text, banner image, promo video
- Quiz integration

### Campaign ROI tracking:
- video_watch_count, quiz_pass_count, open_chapter_count
- cpb (cost per baptism), cpa (cost per video watch), cpq (cost per quiz pass)

### TagSelector component:
Uses `getTags()` from `/admin/tags` (not direct FEBC middleware).
Groups come from Tags Management system.
Session-level cache of tag list.

## 6. Academy (LMM — Learning Management Module)
Route: `/admin/academy`, `/admin/academy/lessons`, `/admin/academy/learners`

### Single lessons (academy_chapters):
- chapter_number, title, description, video_url
- pass_threshold, unlock_type (always/previous_pass/custom)
- Questions parsed from PDFs via parse jobs
- Progress tracked per user

### Curriculum sets (academy_v3):
- CurriculumSet → CampaignLesson[] (ordered lessons)
- Prerequisites between sets
- Certificate issuance on completion

### Certificate system:
- PDF generation with user name positioned via coordinates
- Postal delivery tracking: PENDING_DELIVERY → SHIPPED → DELIVERED
- Thailand Post integration for tracking numbers

### Learner stats:
- Dropout detection, score averages, completion rates
- Spiritual DNA per learner

## 7. Coins & Rewards
Route: `/admin/coins`, `/admin/rewards`
- CoinLedger: earn/spend history per user
- ActivityType: VideoWatch, QuizPass, AdminGrant, etc.
- RewardCatalog: items with coin_cost, stock
- Daily earning cap per user
- Redemption tracking

## 8. Churches
Route: `/admin/churches`
- Church directory with province, district, pastor, contact, coordinates
- BaptismTracking: scheduling and recording baptisms
- Export to CSV/Excel
- Province filtering

## 9. Prayer / Intercessory
Route: `/admin/prayers`
- PrayerRequest: content, urgency (Normal/Urgent/SOS), status (New/InProgress/Resolved/Escalated)
- PrayerPartner assignment
- Response recording

## 10. Volunteer System
Route: `/admin/volunteer`, `/admin/volunteer/ambassador`
- Volunteer roster with LINE IDs
- Active case counts per volunteer
- Ambassador Hub for outreach volunteers
- SOS escalation integration

## 11. Content Hub
Route: `/admin/content`
Primary source: Pinecone full-clip namespace (YouTube videos with transcripts)
Fallback: `/line/videos`
- VideoWatch tracking
- Quiz extraction from video transcripts
- Theme tags for categorization

## 12. Commander (Budget/Agent Control)
Route: `/admin/commander`
- Budget overview and management
- Agent logs and control
- Swarm tester (AI agent testing interface)

## 13. Staff Management
Route: `/admin/staff`
- Staff member CRUD
- Custom roles with per-module permissions
- Scope: Regional / Unit

## 14. Permissions
Route: `/admin/permissions`
- Role-based permission matrix
- All 17 modules configurable
- Custom role creation
- Invite link generation
