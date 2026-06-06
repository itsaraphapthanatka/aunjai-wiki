---
title: "Funnel Stages"
type: concept
tags: [funnel, discipleship, journey, stages]
created: 2026-06-05
updated: 2026-06-05
sources: 2
---

# Funnel Stages

## Description
โมเดล 4 ขั้นตอนที่ describe journey ของผู้ใช้ตั้งแต่ค้นพบ FEBC จนถึงการรับใช้ในคริสตจักร
เป็น core organizing framework ของระบบทั้งหมด

## Stages

| Stage | ความหมาย | ลักษณะ user |
|---|---|---|
| **Engage** | พบเจอ content ครั้งแรก | casual listener, new contact |
| **Connect** | interact สม่ำเสมอ | relationship forming, C1-C2 |
| **Transform** | discipleship เชิงลึก | active learning, C2-C3 |
| **Send** | พร้อมรับใช้ | church member, volunteer |

## Usage
- Users ทุกคนมี `funnel_stage` field
- Dashboard แสดง funnel chart (จำนวน users แต่ละ stage)
- Campaign targeting ใช้ funnel stage
- Reports: conversion rates ระหว่าง stages

## Circle Levels (sub-classification)
ใช้ใน Connect และ Transform — ดูรายละเอียดเต็มที่ [[concepts/circle-level-progression]]:
- C1 = Engage (R 0.0–0.3) — casual follower
- C2 = Connect/Transform (R 0.3–0.75) — engaged learner → active disciple
- C3 = Send (R ≥ 0.85) — committed disciple ready for church
- C4 = Stewardship — church handover (Local Connector)

## Related
- [[concepts/circle-level-progression]] — C1→C4 กลไกปรับระดับ, R-score, APIs
- [[concepts/spiritual-scores]]
- [[entities/campaign-system]]
- [[sources/aunjai-system-overview]]
- [[sources/aunjai-circle-level-progression]]
