---
type: concept
tags: [infrastructure, database, weWatch]
---
# 🍃 MongoDB

**Role:** Основная БД | **Hub:** [[../00-weWatch-Overview]]

## Используется в
- [[../services/auth]] — Users, RefreshTokens
- [[../services/user]] — Profiles, Friends
- [[../services/content]] — Movies, WatchProgress
- [[../services/watch-party]] — Rooms, Messages
- [[../services/battle]] — Battles, Scores
- [[../services/notification]] — Notifications
- [[../services/admin]] — Logs, ErrorEvents

## Паттерны
- Mongoose schemas со строгой типизацией
- TTL indexes для сессий и OTP
- Text indexes → или [[Elasticsearch]]
- explain() для оптимизации запросов
