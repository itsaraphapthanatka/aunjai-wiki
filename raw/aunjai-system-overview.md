# น้องอุ่นใจ — System Overview

## What It Is
น้องอุ่นใจ (Nong Aunjai) is a LINE OA chatbot and AI companion operated by FEBC Thailand (Far East Broadcasting Company). The system is a spiritual care and discipleship platform that accompanies users on a journey from first contact through faith transformation and eventual church connection.

The admin interface is the "น้องอุ่นใจ Command Center" — an internal dashboard for managing users, campaigns, crisis response, and content.

## Mission
FEBC Thailand's stated goal: reach 50,000 users within 12 months. The funnel model guides people through four stages: Engage → Connect → Transform → Send.

## Core URL
- Admin: https://openclaw.appreview.cloud/admin/
- API base: https://openclaw.appreview.cloud/aunjai-api/api/v1/

## Codebase Location
- `/home/ai_studio_febcth/.openclaw/workspace/aunjai-swarm/`
  - `admin-ui/` — Next.js 15 frontend
  - `middleware/` — FastAPI backend

## Key Numbers (as of 2026-06-05)
- Total users: ~10,048
- Users with febc_tags: ~8,625
- Unique tags in user DB: ~219
- Total FEBC tags (middleware): 364
- Content videos: tracked via Pinecone vector DB

## Funnel Stages
The four stages define where a user is in their spiritual journey:
1. **Engage** — discovered FEBC content, initial contact
2. **Connect** — interacting regularly, relationship forming
3. **Transform** — active discipleship, faith deepening
4. **Send** — ready to serve, becoming a church member or volunteer

## Circle Levels
Within Connect and beyond, users are classified:
- **C1** — casual follower
- **C2** — engaged learner
- **C3** — committed disciple / ready for church connection

## User Scores (Spiritual DNA)
Four scores characterize each user's spiritual health:
- **R-score** (Relationship) — relational engagement with platform
- **S-score** (Spiritual/Sentiment) — emotional/spiritual wellbeing; ≤ -0.9 triggers SOS
- **Q-score** (Quiet Time) — consistency of devotional practice
- **I-score** (Involvement) — participation in activities and events

Topic affinities also tracked: healing, faith, community (0.0–1.0 scale).

## Persona Types
- **SERVANT** — service-oriented, outward-focused
- **LEARNER** — knowledge-seeking, growth-focused

## Roles (Staff)
- super_admin — full access
- regional_coordinator — regional management
- field_staff — field operations
- prayer_partner — prayer ministry
- volunteer — volunteer duties
