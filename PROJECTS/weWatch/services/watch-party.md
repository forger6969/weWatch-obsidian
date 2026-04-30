---
type: service
tags: [weWatch, backend, realtime, socket]
port: 3004
---
# 🎭 Watch Party Service

**Port:** 3004 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Стек
- [[../concepts/Socket.io]] — real-time комнаты
- [[../concepts/Redis]] — состояние комнат, pub/sub
- [[../concepts/MongoDB]] — история комнат

## Sync Algorithm
- Latency compensation ±2sec threshold
- Buffer event → pause всех участников
- Owner: play/pause/seek права
- Member: только просмотр + chat + emoji

## События (НЕЛЬЗЯ МЕНЯТЬ!)
- room:join, room:leave, room:closed
- video:play, video:pause, video:seek, video:sync
- room:message, room:emoji
- member:kick, member:mute

## Связи
- ← [[../services/mobile]] — WatchParty экраны
- → [[notification]] — invites, room events
- ← [[content]] — videoUrl
