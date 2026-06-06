---
title: "Keyword Routing (4 Paths)"
type: concept
tags: [middleware, routing, keyword, video, pinecone]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Keyword Routing (4 Paths)

การ route ข้อความเกิดที่ **Middleware (line_webhook.py)** ก่อนถึง OpenClaw/agents

## Entry Point

```
LINE User → Nginx → Middleware (line_webhook.py) → Keyword Check
```

Middleware ส่ง HTTP 200 กลับ LINE ทันที แล้วทำงานเป็น Background Task ใน `handle_non_arc_events_bg`

## 4 Paths

### 🅰️ PATH A — VIDEO_BROWSE_KEYWORDS
*"แนะนำคลิป / มีคลิปอะไรบ้าง"*

1. Push Category Bubble (6 หมวดหมู่)
2. User เลือกหมวด → Postback
3. `_fetch_pinecone_highlights` (category_query, top_k=5)
4. Redis Dedup กรองคลิปซ้ำ
5. `_push_video_clips` → LINE Flex Carousel
6. Schedule follow-up 3 นาที

### 🅱️ PATH B — VIDEO_REQUEST_KEYWORDS
*"ขอดูคลิป / ดูวิดีโอ"*

1. Get Context จาก Redis (last 3 msgs)
2. `_fetch_pinecone_highlights` (context_query, top_k=5)
3. Filter Duplicates
4. Push Flex Cards

### 🅲 PATH C — EMOTIONAL_KEYWORDS
*"เครียด / เหนื่อย / ท้อ"*

1. Empathy Message + คำอธิษฐาน
2. RAG Step 1: Quick Reply "สนใจดูคลิป? / ไม่สนใจ"
   - สนใจ (rag_accept): RAG Step 2 → Smart Query → Push Video Flex Cards
   - ไม่สนใจ (rag_decline): forward ไป ARC-GATE
3. Forward ไป ARC-GATE → OpenClaw → front-desk

### 🅳 PATH D — Normal Message
*ข้อความทั่วไป*

1. Check `is_onboarded`
   - ❌ ยังไม่ onboard → [[concepts/onboarding-flow]]
   - ✅ onboarded → Forward ไป ARC-GATE → OpenClaw → front-desk

## Infrastructure

- **Redis** — dedup video clips + เก็บ conversation context (last 3 msgs)
- **Pinecone** — vector search สำหรับ video content
- **ARC-GATE** — entry point เข้า OpenClaw swarm

## Related

- [[concepts/aunjai-swarm]]
- [[concepts/onboarding-flow]]
- [[concepts/message-pipeline]]
- [[entities/arc-console]]
- [[sources/aunjai-swarm-agent-flow]]
