---
type: service
tags: [weWatch, backend, realtime, socket]
port: 3004
updated: 2026-05-01 06:35
---
# 🎭 Watch Party Service

**Port:** 3004 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Стек
- [[../concepts/Socket.io]] — real-time комнаты
- [[../concepts/Redis]] — состояние комнат, pub/sub
- [[../concepts/MongoDB]] — история комнат

## Sync Algorithm (текущий)
- Latency compensation ±2sec threshold
- Buffer event → pause всех участников
- Owner: play/pause/seek права
- Member: только просмотр + chat + emoji

## ⚠️ TODO — NTP Drift Compensation
Анализ Rave показал, что они используют **NTP clock correction + timestamp drift compensation**:
```typescript
// В каждый emit добавить sentAt:
socket.emit('video:play', {
  position: currentTime,
  sentAt: Date.now(),   // ← ДОБАВИТЬ!
  roomId
})

// При получении — компенсировать задержку:
socket.on('video:sync', (payload) => {
  const drift = (Date.now() - payload.sentAt) / 1000
  const corrected = payload.position + drift
  videoRef.current?.setPositionAsync(corrected * 1000)
})
```
Подробнее: [[../analysis/rave-reverse-engineering]]

## События (НЕЛЬЗЯ МЕНЯТЬ!)
- room:join, room:leave, room:closed
- video:play, video:pause, video:seek, video:sync
- room:message, room:emoji
- member:kick, member:mute

## Связи
- ← [[../services/mobile]] — WatchParty экраны
- → [[../services/notification]] — invites, room events
- ← [[../services/content]] — videoUrl
