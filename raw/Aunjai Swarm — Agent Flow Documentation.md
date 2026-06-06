---
title: "Aunjai Swarm — Agent Flow Documentation"
source: "https://openclaw.appreview.cloud/docs/aunjai-agent-flow.html"
author:
published:
created: 2026-06-06
description:
tags:
  - "clippings"
---
```
#mermaid-1780721044630{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044630 .error-icon{fill:#552222;}#mermaid-1780721044630 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044630 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044630 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044630 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044630 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044630 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044630 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044630 .marker.cross{stroke:#555770;}#mermaid-1780721044630 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044630 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044630 .cluster-label text{fill:#333;}#mermaid-1780721044630 .cluster-label span,#mermaid-1780721044630 p{color:#333;}#mermaid-1780721044630 .label text,#mermaid-1780721044630 span,#mermaid-1780721044630 p{fill:#333;color:#333;}#mermaid-1780721044630 .node rect,#mermaid-1780721044630 .node circle,#mermaid-1780721044630 .node ellipse,#mermaid-1780721044630 .node polygon,#mermaid-1780721044630 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044630 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044630 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044630 .node .label{text-align:center;}#mermaid-1780721044630 .node.clickable{cursor:pointer;}#mermaid-1780721044630 .arrowheadPath{fill:#333333;}#mermaid-1780721044630 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044630 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044630 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044630 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044630 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044630 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044630 .cluster text{fill:#333;}#mermaid-1780721044630 .cluster span,#mermaid-1780721044630 p{color:#333;}#mermaid-1780721044630 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044630 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044630 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}VIDEO_REQUEST_KEYWORDSVIDEO_BROWSE_KEYWORDSEMOTIONAL_KEYWORDSข้อความทั่วไป❌ ยังไม่ onboard✅ onboardedYesNo👤 LINE Userส่งข้อความ🔀 NginxReverse Proxy⚙️ Middlewareline_webhook.py📨 Webhook Handler✅ Return 200ทันที → LINE🔄 Background Taskhandle_non_arc_events_bg🔍 Keyword Check🎬 Pinecone Search→ Push Flex Video Cards📂 Push Category Bubble6 หมวดหมู่💚 RAG Step 1Quick Reply สนใจ/ไม่สนใจ🚪 Forward toARC-GATE🤖 OpenClaw Gateway💛 front-deskAgent Session🛡️ Spawn sentinelSafety Check⏸️ sessions_yieldรอผล sentinel👤 user_get_profileis_onboarded?📝 Onboarding Flowถามชื่อ, อายุ, จังหวัด🎭 Select Persona 1-12Circle + R_score + sentiment📖 มีข้อพระคัมภีร์?✝️ Spawn truth-auditorตรวจสอบข้อพระคัมภีร์💬 Reply to Uservia LINE
```

🟢 **LINE/OpenClaw** — จุดเข้า-ออกข้อความ

🟡 **Middleware/Agent** — ประมวลผลหลัก

🔴 **Sentinel** — ระบบตรวจความปลอดภัย

🔵 **Decision** — จุดตัดสินใจเส้นทาง

Group 1 — Front Line

ประตูหน้าด่านแรก กระจายงานไปยังทุก agent

Gateway Threads: 11 | RSS: 612.9MB

สลับ 12 บุคลิก ตาม Circle + Sentiment, Nickname Gate

ระบบ Affiliate — ติดตามการแนะนำเพื่อน

Group 2 — UX & Flow

วาง path C1→C4 วางแผนเส้นทางผู้ใช้

สร้าง Flex Message, Carousel, Bubble

Push Campaign & โปรโมชั่น

Group 3 — Academy

ออกแบบและจัดการ Faith Quiz

จัดการ Pinecone Indexing

จัดการ Token & Coins reward system

Group 4 — Soul Care & SOS

ประสานงาน Prayer Partner Bridge

Pinecone RAG Search หลายรูปแบบ

SOS Case Lifecycle ติดตามเคส

Group 5 — C4 & Stewardship

จับคู่คริสตจักร 77 จังหวัด

วิเคราะห์ Analytics & KPI

Group 6 — Memory & Health

Memory Sync ประสาน master-brain

ตรวจ API Health ทุกบริการ

Support Agents

SOSVE Crisis Detection — ตรวจจับวิกฤต

⚡ 55 msgs | P95: 9.5s

ตรวจสอบข้อพระคัมภีร์ — Bible Verification

ปรับจูน Prompt ของ Agent ทุกตัว

```
#mermaid-1780721044687{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044687 .error-icon{fill:#552222;}#mermaid-1780721044687 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044687 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044687 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044687 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044687 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044687 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044687 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044687 .marker.cross{stroke:#555770;}#mermaid-1780721044687 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044687 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044687 .cluster-label text{fill:#333;}#mermaid-1780721044687 .cluster-label span,#mermaid-1780721044687 p{color:#333;}#mermaid-1780721044687 .label text,#mermaid-1780721044687 span,#mermaid-1780721044687 p{fill:#333;color:#333;}#mermaid-1780721044687 .node rect,#mermaid-1780721044687 .node circle,#mermaid-1780721044687 .node ellipse,#mermaid-1780721044687 .node polygon,#mermaid-1780721044687 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044687 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044687 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044687 .node .label{text-align:center;}#mermaid-1780721044687 .node.clickable{cursor:pointer;}#mermaid-1780721044687 .arrowheadPath{fill:#333333;}#mermaid-1780721044687 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044687 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044687 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044687 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044687 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044687 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044687 .cluster text{fill:#333;}#mermaid-1780721044687 .cluster span,#mermaid-1780721044687 p{color:#333;}#mermaid-1780721044687 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044687 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044687 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}🎯 mainALL Agents🛡️ sentinelALL Agents(Safety Override)💛 front-deskSpecialist Agents🗺️ journey-architect📣 aunjai-messenger🎓 academy-specialist🪙 reward-manager🤝 referral-tracker✝️ truth-auditor📦 media-delivery🙏 intercessory-coordinator🔁 care-loop-closer🔧 system-tunerALL Agents(Prompt Updates)🧪 auto-qaExternal Services💜 maac-syncMaster Brain📊 insights-analystALL Agents(Data Collection)
```

### รายละเอียดการสื่อสาร

🎯 main → ALL agents — Gateway Guard กระจายงาน

🛡️ sentinel → ALL agents — Safety Override, SOSVE Freeze

💛 front-desk → ALL specialist agents — User Input Routing

🗺️ journey-architect → front-desk, aunjai-messenger — Context Injection

🎓 academy-specialist → reward-manager — Coin Award Trigger

🤝 referral-tracker → reward-manager — Referral Bonus

✝️ truth-auditor → media-delivery — Approve/Reject Scripture

📣 aunjai-messenger → reward-manager — Budget Sync

🙏 intercessory-coordinator → care-loop-closer — Handoff for Follow-up

🛡️ sentinel → intercessory-coordinator — SOSVE → Partner Bridge

🔁 care-loop-closer → journey-architect — Post-SOS Funnel Adjustment

🔧 system-tuner → ALL agents — Prompt Updates

🧪 auto-qa → ALL external services — API Monitoring

💜 maac-sync → master-brain — Bidirectional Memory Sync

📊 insights-analyst → ALL agents — Data Collection

```
#mermaid-1780721044722{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044722 .error-icon{fill:#552222;}#mermaid-1780721044722 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044722 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044722 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044722 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044722 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044722 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044722 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044722 .marker.cross{stroke:#555770;}#mermaid-1780721044722 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044722 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044722 .cluster-label text{fill:#333;}#mermaid-1780721044722 .cluster-label span,#mermaid-1780721044722 p{color:#333;}#mermaid-1780721044722 .label text,#mermaid-1780721044722 span,#mermaid-1780721044722 p{fill:#333;color:#333;}#mermaid-1780721044722 .node rect,#mermaid-1780721044722 .node circle,#mermaid-1780721044722 .node ellipse,#mermaid-1780721044722 .node polygon,#mermaid-1780721044722 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044722 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044722 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044722 .node .label{text-align:center;}#mermaid-1780721044722 .node.clickable{cursor:pointer;}#mermaid-1780721044722 .arrowheadPath{fill:#333333;}#mermaid-1780721044722 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044722 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044722 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044722 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044722 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044722 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044722 .cluster text{fill:#333;}#mermaid-1780721044722 .cluster span,#mermaid-1780721044722 p{color:#333;}#mermaid-1780721044722 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044722 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044722 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}สนใจrag_acceptไม่สนใจrag_decline👤 User ส่งข้อความ⚙️ MiddlewareKeyword Check🅰️ PATH AVIDEO_BROWSE_KEYWORDS🅱️ PATH BVIDEO_REQUEST_KEYWORDS🅲 PATH CEMOTIONAL_KEYWORDS🅳 PATH DNormal Message📂 Push Category Bubble6 หมวดหมู่👆 User เลือกหมวดPostback🔍 _fetch_pinecone_highlightscategory_query, top_k=5🔄 Redis Dedupกรองคลิปซ้ำ📤 _push_video_clipsLINE Flex Carousel⏰ Schedule Follow-up3 นาที📋 Get ContextRedis last 3 msgs🔍 _fetch_pinecone_highlightscontext_query, top_k=5🔄 Filter Duplicates📤 Push Flex Cards💚 RAG Step 1Quick Replyสนใจดูคลิป? / ไม่สนใจ🔍 RAG Step 2Context → Smart Query📤 Push Video Flex Cards🤗 Empathy Message+ คำอธิษฐาน🚪 ARC-GATE→ OpenClaw💛 front-deskAgent Session
```

🅰️ PATH A แนะนำคลิป / มีคลิปอะไรบ้าง

🅱️ PATH B ขอดูคลิป / ดูวิดีโอ

🅲 PATH C เครียด / เหนื่อย / ท้อ

🅳 PATH D ข้อความปกติ → Agent

```
#mermaid-1780721044759{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044759 .error-icon{fill:#552222;}#mermaid-1780721044759 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044759 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044759 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044759 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044759 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044759 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044759 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044759 .marker.cross{stroke:#555770;}#mermaid-1780721044759 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044759 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044759 .cluster-label text{fill:#333;}#mermaid-1780721044759 .cluster-label span,#mermaid-1780721044759 p{color:#333;}#mermaid-1780721044759 .label text,#mermaid-1780721044759 span,#mermaid-1780721044759 p{fill:#333;color:#333;}#mermaid-1780721044759 .node rect,#mermaid-1780721044759 .node circle,#mermaid-1780721044759 .node ellipse,#mermaid-1780721044759 .node polygon,#mermaid-1780721044759 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044759 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044759 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044759 .node .label{text-align:center;}#mermaid-1780721044759 .node.clickable{cursor:pointer;}#mermaid-1780721044759 .arrowheadPath{fill:#333333;}#mermaid-1780721044759 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044759 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044759 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044759 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044759 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044759 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044759 .cluster text{fill:#333;}#mermaid-1780721044759 .cluster span,#mermaid-1780721044759 p{color:#333;}#mermaid-1780721044759 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044759 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044759 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}📨 ทุกข้อความ🛡️ SentinelSentiment Scan🟢 SAFEscore > 0.0🟡 CAUTION-0.3 to 0.0🟠 WARNING-0.7 to -0.3🔴 ALERT-0.9 to -0.7⛔ FREEZE≤ -0.9💬 ดำเนินการปกติ👀 MonitorGentle Mode💜 Force Persona 8The Healer💜 Healer +🚩 Human Flag🚨 STOP ALL AI→ Human Counselor
```

### ตารางระดับความปลอดภัย

| ระดับ | Sentiment Score | สถานะ | การตอบสนอง |
| --- | --- | --- | --- |
| 🟢 SAFE | `> 0.0` | ปกติ | ดำเนินการตามปกติ |
| 🟡 CAUTION | `-0.3 ถึง 0.0` | เฝ้าระวัง | Monitor + Gentle Mode |
| 🟠 WARNING | `-0.7 ถึง -0.3` | เตือน | บังคับ Persona 8: The Healer |
| 🔴 ALERT | `-0.9 ถึง -0.7` | แจ้งเตือน | Healer + แจ้งทีมมนุษย์ดูแล |
| ⛔ FREEZE | `≤ -0.9` | หยุดทั้งหมด | **หยุด AI ทันที → ส่งต่อที่ปรึกษามนุษย์** |

### ประเภทวิกฤต (Crisis Types)

⚠️ self\_harm ⚠️ suicide ⚠️ violence ⚠️ abuse

```
#mermaid-1780721044781{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044781 .error-icon{fill:#552222;}#mermaid-1780721044781 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044781 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044781 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044781 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044781 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044781 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044781 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044781 .marker.cross{stroke:#555770;}#mermaid-1780721044781 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044781 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044781 .cluster-label text{fill:#333;}#mermaid-1780721044781 .cluster-label span,#mermaid-1780721044781 p{color:#333;}#mermaid-1780721044781 .label text,#mermaid-1780721044781 span,#mermaid-1780721044781 p{fill:#333;color:#333;}#mermaid-1780721044781 .node rect,#mermaid-1780721044781 .node circle,#mermaid-1780721044781 .node ellipse,#mermaid-1780721044781 .node polygon,#mermaid-1780721044781 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044781 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044781 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044781 .node .label{text-align:center;}#mermaid-1780721044781 .node.clickable{cursor:pointer;}#mermaid-1780721044781 .arrowheadPath{fill:#333333;}#mermaid-1780721044781 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044781 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044781 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044781 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044781 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044781 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044781 .cluster text{fill:#333;}#mermaid-1780721044781 .cluster span,#mermaid-1780721044781 p{color:#333;}#mermaid-1780721044781 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044781 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044781 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}ข้ามข้ามข้ามข้าม🆕 New Useris_onboarded = false📝 Step 1ถามชื่อเล่น📝 Step 2ถามชื่อ-นามสกุล📝 Step 3ถามอายุ📝 Step 4ถามจังหวัด✅ is_onboarded = true⏭️ is_onboarded = falseกลับมาทำต่อได้
```

1

ชื่อเล่น

user\_set\_nickname

→

2

ชื่อ-สกุล

first\_name / last\_name

→

3

อายุ

validate 1-120

→

4

จังหวัด

Thai Province

→

✓

สำเร็จ!

is\_onboarded = true

💡 **หมายเหตุ:** หากผู้ใช้ข้ามขั้นตอนใด is\_onboarded จะยังเป็น false — สามารถกลับมาทำต่อได้ในภายหลัง

```
#mermaid-1780721044798{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#333;}#mermaid-1780721044798 .error-icon{fill:#552222;}#mermaid-1780721044798 .error-text{fill:#552222;stroke:#552222;}#mermaid-1780721044798 .edge-thickness-normal{stroke-width:2px;}#mermaid-1780721044798 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-1780721044798 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-1780721044798 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-1780721044798 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-1780721044798 .marker{fill:#555770;stroke:#555770;}#mermaid-1780721044798 .marker.cross{stroke:#555770;}#mermaid-1780721044798 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-1780721044798 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#333;}#mermaid-1780721044798 .cluster-label text{fill:#333;}#mermaid-1780721044798 .cluster-label span,#mermaid-1780721044798 p{color:#333;}#mermaid-1780721044798 .label text,#mermaid-1780721044798 span,#mermaid-1780721044798 p{fill:#333;color:#333;}#mermaid-1780721044798 .node rect,#mermaid-1780721044798 .node circle,#mermaid-1780721044798 .node ellipse,#mermaid-1780721044798 .node polygon,#mermaid-1780721044798 .node path{fill:#ECECFF;stroke:#9370DB;stroke-width:1px;}#mermaid-1780721044798 .flowchart-label text{text-anchor:middle;}#mermaid-1780721044798 .node .katex path{fill:#000;stroke:#000;stroke-width:1px;}#mermaid-1780721044798 .node .label{text-align:center;}#mermaid-1780721044798 .node.clickable{cursor:pointer;}#mermaid-1780721044798 .arrowheadPath{fill:#333333;}#mermaid-1780721044798 .edgePath .path{stroke:#555770;stroke-width:2.0px;}#mermaid-1780721044798 .flowchart-link{stroke:#555770;fill:none;}#mermaid-1780721044798 .edgeLabel{background-color:#e8e8e8;text-align:center;}#mermaid-1780721044798 .edgeLabel rect{opacity:0.5;background-color:#e8e8e8;fill:#e8e8e8;}#mermaid-1780721044798 .labelBkg{background-color:rgba(232, 232, 232, 0.5);}#mermaid-1780721044798 .cluster rect{fill:#ffffde;stroke:#aaaa33;stroke-width:1px;}#mermaid-1780721044798 .cluster text{fill:#333;}#mermaid-1780721044798 .cluster span,#mermaid-1780721044798 p{color:#333;}#mermaid-1780721044798 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:#E0E4EC;border:1px solid #aaaa33;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-1780721044798 .flowchartTitleText{text-anchor:middle;font-size:18px;fill:#333;}#mermaid-1780721044798 :root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}YesNoYesNoYesNo1️⃣ main🎯 Orchestrator GateRoute to Squad2️⃣ sentinel🛡️ Safety Scansecurity_scan_content3️⃣ journey-architect🗺️ user_get_profile+ Campaign Context4️⃣ Domain Agent💛 front-desk / 🎓 academy🔎 search-specialist / etc.📖 มีข้อพระคัมภีร์?5️⃣ truth-auditor✝️ bible_verify_scripture🪙 มี Coin Event?6️⃣ reward-manager🪙 coins_award🆘 SOS?7️⃣ care-loop-closer🔁 case_get_open8️⃣ Log📝 logs_analyze_conversation
```

1. **main** (Orchestrator Gate) — Route to Squad เลือกทีม
2. **sentinel** (Safety Scan) — security\_scan\_content ตรวจความปลอดภัย
3. **journey-architect** — user\_get\_profile + ดึง Campaign Context
4. **Domain Agent** — front-desk / academy / search-specialist ตามประเภทข้อความ
5. **truth-auditor** (ถ้ามีข้อพระคัมภีร์) — bible\_verify\_scripture
6. **reward-manager** (ถ้ามี Coin Event) — coins\_award
7. **care-loop-closer** (ถ้า SOS) — case\_get\_open เปิดเคส
8. **Log** — logs\_analyze\_conversation บันทึกทุกการสนทนา
