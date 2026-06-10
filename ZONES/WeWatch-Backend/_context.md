---
zone: WeWatch-Backend
type: context
updated: 2026-06-10
---

# WeWatch-Backend Zone — Context

## Текущее состояние (2026-06-10)

### Архитектура — единая БД cinesync (Sprint 11 ✅)
- `cinesync.users` — объединённая коллекция (auth + user поля в одном документе)
- Все 7 сервисов: MONGO_URI → `cinesync` (НЕ cinesync_auth / cinesync_user)
- T-S096..S100: ✅ все завершены (2026-05-27)

### Сервисы
| Сервис | Port | БД/Cache |
|--------|------|----------|
| auth | 3001 | cinesync |
| user | 3002 | cinesync |
| content | 3003 | cinesync + Elasticsearch 9200 |
| watch-party | 3004 | Redis 6380 + Socket.io |
| battle | 3005 | cinesync + Redis |
| notification | 3007 | Firebase ravetokenauth + Bull |
| admin | 3008 | cinesync |

### CRITICAL: Notification service
- `FIREBASE_PROJECT_ID=ravetokenauth`
- `FIREBASE_PRIVATE_KEY=...ravetokenauth private key...`
- Token type: raw FCM device token (`getDevicePushTokenAsync` result)
- Push method: `sendEachForMulticast()` (не Expo, не sendToDevice)

### Безопасность
- JWT: RS256, access=15min, refresh=30d
- bcrypt: 12 rounds
- Brute force: Redis `login_attempts:{email}`, 5 попыток → 15min блок

## Активные задачи (Saidazim)

### T-S101 P1 ❌ BOSHLANMAGAN — СЛЕДУЮЩИЙ ПРИОРИТЕТ
Migration script: объединить cinesync_auth.users + cinesync_user.users → cinesync.users
- Создать `services/auth/scripts/migrate-to-single-db.ts`
- Email-based merge strategy
- `--dry-run` флаг обязателен
- Шаблон: `.claude/agents/multi-sprint11-migration.md`

### T-S102 P3 ❌ BOSHLANMAGAN
- `npx tsc --noEmit` на всех 7 сервисах
- Обновить `docs/db-architecture.html` (old: 3 DBs → new: 1 cinesync)

## Паттерны (всегда соблюдать)
```typescript
res.json(apiResponse.success(data, 'message'));
res.status(400).json(apiResponse.error('message'));
import { logger } from '@shared/utils/logger';
logger.info('msg', { userId });  // НЕ console.log
```

## Агенты
- `.claude/agents/auth-agent.md` → services/auth/
- `.claude/agents/content-agent.md` → services/content/
- `.claude/agents/watchparty-agent.md` → services/watch-party/
- `.claude/agents/user-battle-notification-agent.md` → services/user,battle,notification/
- `.claude/agents/admin-agent.md` → services/admin/ + apps/admin-ui/
- Multi: `.claude/agents/multi-sprint11-migration.md`

## Связано

[[../WeWatch-Mobile/_context|📱 Mobile Zone]] | [[../WeWatch-Web/_context|🌐 Web Zone]]
[[../../PROJECTS/weWatch/00-weWatch-Overview|WeWatch Overview]]
[[../../PROJECTS/weWatch/ARCHITECTURE|Architecture]]
[[../../PROJECTS/weWatch/decisions/2026-05-23-migration-единая-бд-cinesync-для-всех-сервисов|Decision: cinesync migration]]
[[../../AI_CONTEXT/agents-hub|Agents Hub]]

<!-- session ended: 2026-05-26 21:02 -->

<!-- session ended: 2026-05-26 21:07 -->

<!-- session ended: 2026-05-26 21:16 -->

<!-- session ended: 2026-05-26 23:03 -->

<!-- session ended: 2026-05-26 23:06 -->

<!-- session ended: 2026-05-27 01:38 -->

<!-- session ended: 2026-05-27 01:46 -->

<!-- session ended: 2026-05-27 02:57 -->

<!-- session ended: 2026-05-27 03:05 -->

<!-- session ended: 2026-05-27 04:19 -->

<!-- session ended: 2026-05-27 04:27 -->

<!-- session ended: 2026-05-27 06:37 -->

<!-- session ended: 2026-05-27 23:00 -->

<!-- session ended: 2026-05-28 16:32 -->

<!-- session ended: 2026-05-28 16:45 -->

<!-- session ended: 2026-05-28 16:50 -->

<!-- session ended: 2026-05-28 16:54 -->

<!-- session ended: 2026-05-28 17:02 -->

<!-- session ended: 2026-05-29 22:04 -->

<!-- session ended: 2026-06-01 14:23 -->

<!-- session ended: 2026-06-01 15:39 -->

<!-- session ended: 2026-06-02 15:09 -->

<!-- session ended: 2026-06-03 19:20 -->

<!-- session ended: 2026-06-04 18:38 -->

<!-- session ended: 2026-06-05 17:35 -->

<!-- session ended: 2026-06-05 17:41 -->

<!-- session ended: 2026-06-05 18:36 -->

<!-- session ended: 2026-06-05 19:33 -->

<!-- session ended: 2026-06-06 14:17 -->

<!-- session ended: 2026-06-06 15:55 -->

<!-- session ended: 2026-06-08 17:17 -->

<!-- session ended: 2026-06-08 18:23 -->

<!-- session ended: 2026-06-09 15:26 -->

<!-- session ended: 2026-06-10 00:52 -->

<!-- session ended: 2026-06-10 16:13 -->

<!-- session ended: 2026-06-10 17:39 -->

<!-- session ended: 2026-06-10 17:51 -->

<!-- session ended: 2026-06-10 22:04 -->
