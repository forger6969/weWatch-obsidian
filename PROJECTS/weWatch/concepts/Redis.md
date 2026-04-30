---
type: concept
tags: [infrastructure, cache, weWatch]
---
# ⚡ Redis

**Role:** Кэш + очереди | **Hub:** [[../00-weWatch-Overview]]

## Используется в
- [[../services/auth]] — brute force: login_attempts:{email}
- [[../services/content]] — trending:N, top-rated:N (TTL 10min)
- [[../services/watch-party]] — room state, pub/sub
- [[../services/notification]] — Bull queues (email jobs)

## Конфиг
- Port: 6380
- AOF persistence
- Password protected
