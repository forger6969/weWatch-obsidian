---
type: architecture
project: weWatch
title: "Backend Guidelines (CLAUDE_BACKEND.md)"
date: 2026-05-01
tags: [backend, architecture, node, express, mongodb, socket]
---

# ⚙️ Backend Guidelines

**Hub:** [[../00-weWatch-Overview]] | **Owner:** [[../people/Saidazim]]
**Источник:** `CLAUDE_BACKEND.md`

---

## Зоны (трогать ТОЛЬКО свои)
```
services/auth/           → :3001
services/user/           → :3002
services/content/        → :3003
services/watch-party/    → :3004
services/battle/         → :3005
services/notification/   → :3007
services/admin/          → :3008
apps/admin-ui/           → :5173
shared/                  → middleware, utils, types, constants
```
🚫 **НЕ ТРОГАТЬ:** `apps/mobile/`

---

## Структура каждого сервиса
```
services/[name]/src/
├── controllers/   ← HTTP ONLY, без бизнес-логики
├── services/      ← Вся бизнес-логика
├── models/        ← Mongoose schemas
├── routes/        ← Express Router
├── validators/    ← Joi/Zod
└── types/         ← TypeScript types
```

---

## Паттерны

### Controller — только HTTP
```typescript
// ✅ Правильно
router.get('/:id', verifyToken, async (req, res, next) => {
  try {
    const result = await service.getById(req.params.id)
    res.json(apiResponse.success(result))
  } catch (err) {
    next(err)
  }
})
```

### Logger — ТОЛЬКО Winston, не console.log
```typescript
import { logger } from '@shared/utils/logger'
logger.info('User registered', { userId, email })
logger.error('DB failed', { error: err.message })
```

### Кэширование (Redis)
```typescript
// TTL паттерны
trending:N         → 10 min
top-rated:N        → 10 min
user:${id}         → 5 min
movie:${id}        → 30 min
room:${id}         → 1 hour
```

---

## Socket.io события (НЕЛЬЗЯ ПЕРЕИМЕНОВЫВАТЬ!)
```
room:join, room:leave, room:closed
video:play, video:pause, video:seek, video:sync
room:message, room:emoji
member:kick, member:mute
```

---

## Связанные сервисы
- [[../services/auth]]
- [[../services/watch-party]]
- [[../services/content]]
- [[../concepts/MongoDB]]
- [[../concepts/Redis]]
- [[../concepts/Socket.io]]

> Полная документация: `CLAUDE_BACKEND.md`
