---
type: concept
tags: [infrastructure, realtime, weWatch]
---
# 🔌 Socket.io

**Role:** Real-time синхронизация | **Hub:** [[../00-weWatch-Overview]]

## Используется в
- [[../services/watch-party]] — комнаты, sync
- [[../services/notification]] — in-app real-time
- [[../services/mobile]] — клиент

## ⚠️ Event names НЕЛЬЗЯ МЕНЯТЬ
Изменение ломает 3 платформы одновременно.
Все события → shared/constants/socket-events.ts
