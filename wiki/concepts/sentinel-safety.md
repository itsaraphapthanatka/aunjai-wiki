---
title: "Sentinel Safety System"
type: concept
tags: [sentinel, safety, sos, sentiment, crisis]
created: 2026-06-06
updated: 2026-06-06
sources: 1
---

# Sentinel Safety System

**🛡️ sentinel** — agent ที่ scan ทุกข้อความก่อนถึง domain agents

## Safety Levels

| ระดับ | Sentiment Score | สถานะ | การตอบสนอง |
|-------|----------------|-------|------------|
| 🟢 SAFE | `> 0.0` | ปกติ | ดำเนินการตามปกติ |
| 🟡 CAUTION | `-0.3 ถึง 0.0` | เฝ้าระวัง | Monitor + Gentle Mode |
| 🟠 WARNING | `-0.7 ถึง -0.3` | เตือน | บังคับ Persona 8: The Healer |
| 🔴 ALERT | `-0.9 ถึง -0.7` | แจ้งเตือน | Healer + แจ้งทีมมนุษย์ดูแล |
| ⛔ FREEZE | `≤ -0.9` | หยุดทั้งหมด | **หยุด AI ทันที → Human Counselor** |

## Crisis Types ที่ตรวจจับ

- `self_harm`
- `suicide`
- `violence`
- `abuse`

## ตำแหน่งใน Pipeline

sentinel คือ step ที่ 2 ของ [[concepts/message-pipeline]] — ทุกข้อความผ่าน sentinel ก่อน domain agents เสมอ sentinel มี authority override agents ทุกตัวในระบบ

## ความสัมพันธ์กับ SOS

(confirmed) FREEZE threshold ≤ -0.9 ตรงกับ S-score trigger ของ [[entities/sos-command-center]] ที่ระบุใน [[sources/sos-flow]] — sentinel คือกลไกที่ detect SOS ในฝั่ง LINE chatbot

## Performance

- (single source) 55 msgs processed, P95 latency 9.5s

## Related

- [[concepts/aunjai-swarm]]
- [[concepts/message-pipeline]]
- [[concepts/spiritual-scores]]
- [[entities/sos-command-center]]
- [[sources/aunjai-swarm-agent-flow]]
- [[sources/sos-flow]]
