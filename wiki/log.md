# Activity Log

## [2026-06-12] ingest | 📖 Aunjai Bible Knowledge (10 แหล่ง)
- Extracted: 10 ไฟล์ (docx/pdf/pptx) → raw/bible/*.md (~48.5K chars) ผ่าน pypdf + python-docx + zipfile/xml (pptx)
- Pages created: 24 — sources (10): thiessen-systematic-theology, baptist-doctrine-encyclopedia, jesus-the-messiah, theological-puzzles, purpose-driven-life, seeker-spiritual-framework, bible-survey-ot, bible-survey-nt, israel-history-ep1, israel-history-ep2 · concepts (12): systematic-theology, trinity, christology, soteriology, bibliology, bible-canon, baptist-distinctives, messianic-prophecy, israel-history-ot, five-purposes, christian-apologetics, christian-denominations · entities (2): jesus-christ, israel-nation
- Pages updated: index.md (sources 9→19, entities 9→11, concepts 15→27, pages 37→61), overview.md
- Key additions: โดเมนความรู้ใหม่ (ศาสนศาสตร์/พระคัมภีร์) สำหรับ AI ใช้ตอบคู่สนทนา — จุดยืนนิกาย **แบ๊บติสต์**, 8 สาขาศาสนศาสตร์ระบบ, คริสตวิทยา + คำพยากรณ์เมสสิยาห์, 5 จุดประสงค์ชีวิต, ประวัติศาสตร์อิสราเอล (timeline OT)
- Conflict flags: ธรรมบัญญัติ/พระคุณ (israel-history-ep1); eschatology single-source (systematic-theology)

## [2026-06-11] ingest | Work Log 8–11 มิ.ย. 2026
- Pages created: 6 (sources/work-log-2026-06-08-to-11, entities/access-links-module, concepts/post-cert-journey, concepts/topic-affinity, concepts/automated-lifecycle-services, raw/work-log-2026-06-08-to-11)
- Pages updated: 7 (entities/academy-lmm, concepts/aunjai-swarm, sources/aunjai-swarm-agent-flow, overview, index, log, wiki/sources/work-log-2026-06-08-to-11)
- Key additions: Smart Access Links module (QR + 2-level approval), Post-Cert Journey Phase 3 (Day 0/2/5/10/14/30), Topic Affinity EMA system, Night Prayer Service, Morning Greeting v5 Ph3, Feature Flags API, agent model updates (kimi-code, multi-model stack), front-desk/aunjai-messenger SOUL updates

## [2026-06-06] ingest | Aunjai Swarm — Agent Flow Documentation
- Pages created: 6 (sources/aunjai-swarm-agent-flow, concepts/aunjai-swarm, concepts/sentinel-safety, concepts/keyword-routing, concepts/message-pipeline, concepts/onboarding-flow)
- Pages updated: 5 (entities/arc-console, entities/sos-command-center, overview, index, log)
- Key additions: full agent swarm architecture (15+ agents, 6 groups), 4-path keyword routing, sentinel 5-level safety system, per-message pipeline, onboarding flow

## [2026-06-05] init | Wiki initialized
- Structure created: raw/, wiki/entities/, wiki/concepts/, wiki/sources/, wiki/queries/
- Schema written: CLAUDE.md
- Pages created: index.md, log.md, overview.md
- Status: ready for first source

## [2026-06-05] ingest | aunjai-system-overview
- Pages created: sources/aunjai-system-overview.md, entities/febc-thailand.md
- Pages updated: index.md, log.md, overview.md
- Key additions: funnel stages, circle levels, spiritual scores, staff roles

## [2026-06-05] ingest | technical-architecture
- Pages created: sources/technical-architecture.md, concepts/deployment-process.md
- Pages updated: index.md, overview.md
- Key additions: Docker containers, Nginx routing, external integrations, deployment bug

## [2026-06-05] ingest | modules
- Pages created: sources/modules.md, entities/campaign-system.md, entities/academy-lmm.md
- Pages updated: index.md, overview.md
- Key additions: 14 modules catalog, ARC system description, certificate delivery

## [2026-06-05] ingest | sos-flow
- Pages created: sources/sos-flow.md, entities/sos-command-center.md, entities/arc-console.md, concepts/volunteer-escalation.md
- Pages updated: index.md, overview.md
- Key additions: SOS lifecycle, volunteer state machine, WebSocket events, deep link navigation

## [2026-06-05] ingest | febc-tags-system
- Pages created: sources/febc-tags-system.md, entities/tags-management.md, entities/febc-middleware.md, concepts/tag-groups.md
- Pages updated: index.md, overview.md
- Key additions: 364 tags, top tags by count, group auto-detection, API endpoints

## [2026-06-05] ingest | deployment-operations
- Pages created: sources/deployment-operations.md
- Pages updated: concepts/deployment-process.md, index.md, overview.md
- Key additions: fast deploy steps, docker cp merge bug, health check commands, common symptoms table
