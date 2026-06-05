# FEBC Tags System

## What Are FEBC Tags
String labels attached to user profiles (stored in `users.febc_tags` as PostgreSQL ARRAY).
Tags are assigned automatically by LINE OA flows when users participate in events, activities, or church interactions.

## Tag Sources
1. **middleware.febradio.org/api/tags** — master list of 364 tags (external source of truth)
2. **febc_tags DB table** — metadata layer: description, group_name, available_days
3. **users.febc_tags** — which tags each user has (populated by LINE OA flows)

## Real Data Stats (2026-06-05)
- Total unique tags from middleware: 364
- Unique tags found in user records: 219
- Users with at least one tag: 8,625 (out of 10,048 total)

## Top Tags by User Count
1. Center_พิษณุโลก — 2,583 users
2. Center_ภูเก็ต — 2,532 users
3. richmenu_สหกิจ — 1,577 users
4. MODEL_พิษณุโลก — 1,150 users
5. richmenu_new_คริสตจักรแห่งนิมิตพรหมพิราม — 1,099 users
6. PROJECT_รถประกาศข่าวดี — 813 users

## Tag Groups (auto-detected from prefix)
| Group | Prefix pattern | Example |
|---|---|---|
| Center | CENTER_, Center_ | Center_พิษณุโลก |
| Event | EVENT_, Event_ | Event_MiracleOfLoveD1 |
| Activity | ACTIVITY_, Activity_ | ACTIVITY_ลุ้นรางวัล |
| Target | TARGET_, Target_ | Target_EveryOneThailand |
| Respond | RESPOND_, Respond_ | Respond_ส่งใบสมัคร |
| Richmenu | RICHMENU_ | richmenu_สหกิจ |
| Model | MODEL_ | MODEL_พิษณุโลก |
| Project | PROJECT_ | PROJECT_รถประกาศข่าวดี |
| Home | HOME_, Home_ | Home_MENU_APP_บทเรียนออนไลน์ |
| Driver | DRIVER_, Driver_ | Driver_JaruwanPetpaiprasert |
| Deep Link | DL_ | DL_HOME_FEBC |
| Content | CONTENT_ | Content_Choice_สภาพอากาศใจ |
| Campaign | # prefix | # เกมหัวใจฉันมีค่า... |
| Other | no matching prefix | Staff_กนกพร, SUB_MENU_FB_... |

## "Other" Group — Known Uncategorized Prefixes
Tags in "Other" don't match defined prefixes. Key uncategorized groups:
- MEMBER_ — church members (~35 tags)
- NEW_ — new church contacts (~27 tags)
- SUB_MENU_ — submenu tracking for FB/PC/YT (~30 tags)
- FILTER_ — flow state tracking (6 tags)
- Staff_ — staff assignment tracking (~31 tags)
- Line_ — LINE activity tracking
- Register_ — event registration
- Evnt_ — typo variant of Event_ (e.g. Evnt_อบรมการประกาศ_คจ.เอกชัย)

## Tag Metadata (febc_tags table)
```
id: UUID
name: string (unique)
group_name: string | null
description: text | null
description_detail: text | null
available_days: int | null  (null = permanent)
created_at, updated_at
```

## Tag Groups (febc_tag_groups table)
```
id: UUID
name: string (unique)
color: string (blue/purple/green/orange/red/pink/teal/yellow/indigo/cyan/lime/slate)
description: text | null
created_at
```
Built-in groups: 14 (Center, Event, Activity, Target, Respond, Model, Project, Richmenu, Deep Link, Home, Driver, Content, Campaign, Other) — cannot be deleted.
Custom groups: created by admin, deletable (moves tags to "Other").

## Admin Operations
- View all 364 tags with metadata, grouped and filterable
- Create new tags (stored locally, not pushed to middleware)
- Edit tag metadata: group, description, available_days
- Add/remove users from tags individually or in bulk
- Create custom groups with color picker
- Search tags by name or description

## Usage in Campaigns
CampaignBuilder has a TagSelector component that:
- Loads from `GET /admin/tags` (merged FEBC middleware + DB metadata)
- Displays grouped by group_name (matches Tags Management)
- Allows selecting up to 5 tags per campaign
- Tags stored in Campaign.tags: string[]
- Used for audience targeting and content labeling

## API Endpoints
```
GET  /admin/tags                  list all tags (merged + metadata + member_count)
POST /admin/tags                  create tag
PATCH /admin/tags/{name}          update metadata
DELETE /admin/tags/{name}         delete metadata record
GET  /admin/tags/stats            legacy: member counts
POST /admin/tags/bulk-add         add tag to N users
POST /admin/tags/bulk-remove      remove tag from N users
GET  /admin/tag-groups            list all groups
POST /admin/tag-groups            create custom group
PATCH /admin/tag-groups/{name}    update group
DELETE /admin/tag-groups/{name}   delete custom group
POST /users/{id}/tags             add single tag to user
DELETE /users/{id}/tags/{tag}     remove single tag from user
GET  /users/?febc_tag={tag}       filter users by tag
```
