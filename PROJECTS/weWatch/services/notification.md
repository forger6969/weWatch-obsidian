---
type: service
tags: [weWatch, backend, notifications]
port: 3007
---
# 🔔 Notification Service

**Port:** 3007 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Каналы
- Push → [[../concepts/FCM]] (Firebase Cloud Messaging)
- In-app → [[../concepts/MongoDB]] + [[../concepts/Socket.io]]
- Email → Nodemailer + Bull queue

## Типы уведомлений
- friend_request / friend_accepted
- watch_party_invite
- battle_invite / battle_result
- achievement_unlocked
- friend_online / friend_watching

## Связи
- ← [[auth]] — verification emails
- ← [[user]] — friend events
- ← [[watch-party]] — invite events
- ← [[battle]] — results
