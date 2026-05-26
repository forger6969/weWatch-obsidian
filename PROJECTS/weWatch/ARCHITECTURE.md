---
type: architecture
project: weWatch
updated: 2026-05-23
---

# WeWatch — Architecture Reference

> Читать при: новой задаче, изменении сервиса, добавлении endpoint-а.
> НЕ менять архитектуру без обновления этого файла.

---

## Обзор

WeWatch (CineSync / Rave) — социальный онлайн-кинотеатр.
Монорепо с микросервисами. Backend = Saidazim. Mobile = Emirhan.

---

## Сервисы и порты

| Сервис | Tech | Port | Зона |
|--------|------|------|------|
| auth | Node.js + Express + MongoDB | 3001 | Saidazim |
| user | Node.js + Express + MongoDB | 3002 | Saidazim |
| content | Node.js + Express + Elasticsearch | 3003 | Saidazim |
| watch-party | Express + Socket.io + Redis | 3004 | Saidazim |
| battle | Express + MongoDB + Redis | 3005 | Saidazim |
| notification | Express + Firebase FCM + Bull | 3007 | Saidazim |
| admin | Express + MongoDB | 3008 | Saidazim |
| mobile | React Native + Expo + TypeScript | — | Emirhan |
| admin-ui | React + Vite + Tailwind | 5173 | Saidazim |

---

## Инфраструктура

```
MongoDB Atlas      → основная БД (порт 27017)
Redis 7            → кэш + Bull queues (порт 6380)
Elasticsearch      → поиск контента (порт 9200)
Firebase FCM       → push уведомления
Socket.io          → real-time синхронизация watch party
Railway            → деплой всех сервисов
nginx              → reverse proxy
```

---

## Структура каждого сервиса

```
services/[name]/
├── src/
│   ├── app.ts                    # Express init, middleware, routes
│   ├── server.ts                 # Port listen + graceful shutdown
│   ├── config/index.ts           # Environment variables
│   ├── controllers/[name].controller.ts   # HTTP layer ТОЛЬКО
│   ├── services/[name].service.ts         # Бизнес-логика
│   ├── models/[entity].model.ts           # Mongoose schema
│   ├── routes/[name].routes.ts            # Express Router
│   ├── validators/[name].validator.ts     # Joi/Zod schemas
│   └── types/index.ts                     # Service-specific types
├── package.json
├── tsconfig.json
└── Dockerfile
```

---

## Паттерны (обязательны везде)

### Controller = HTTP only
```typescript
// ✅ Правильно
async getMovie(req, res, next) {
  try {
    const data = await contentService.getMovieById(req.params.id, req.user.id);
    res.json(apiResponse.success(data));
  } catch (err) { next(err); }
}
// ❌ Нельзя: DB query в controller
```

### Service = бизнес-логика
```typescript
class ContentService {
  async getMovieById(movieId: string, userId: string): Promise<IMovie> {
    const movie = await Movie.findById(movieId).lean();
    if (!movie) throw new NotFoundError('Movie not found');
    return movie;
  }
}
```

### API Response (стандарт для ВСЕХ endpoint-ов)
```typescript
interface ApiResponse<T> {
  success: boolean;
  data: T | null;
  message: string;
  errors: string[] | null;
  meta?: { page, limit, total, totalPages }
}
res.json(apiResponse.success(data, 'msg'));
res.status(404).json(apiResponse.error('Not found'));
res.json(apiResponse.paginated(items, { page, limit, total }));
```

---

## Auth (JWT RS256)

```
Access token:  15 min, RS256, payload: { userId, email, role }
Refresh token: 30 days, MongoDB (hashed), crypto.randomBytes(64)
Brute force:   5 попыток → 15min блок (Redis: login_attempts:{email})
```

### Middleware stack
```
verifyToken       → JWT verify, req.user attach
optionalAuth      → token optional (public endpoints)
requireVerified   → isEmailVerified === true
requireRole(role) → role check (admin/operator)
rateLimiter       → Redis per-IP + per-user
```

---

## Socket.io — Watch Party Sync

**КРИТИЧНО: event names НЕЛЬЗЯ переименовывать — ломает 3 платформы!**

```typescript
// Server → Client
'room:joined' | 'room:left' | 'video:play' | 'video:pause'
'video:seek'  | 'video:sync' | 'video:buffer'
'member:kicked' | 'member:muted' | 'room:message' | 'room:emoji' | 'room:closed'

// Client → Server
'room:join' | 'room:leave' | 'video:play' | 'video:pause'
'video:seek' | 'room:message' | 'room:emoji' | 'member:kick' | 'member:mute'
```

### Sync Algorithm
```
SyncState: { currentTime, isPlaying, serverTimestamp, updatedBy }
Threshold: ±2 sec → force seek если отклонение больше
Buffer:    pause остальных когда один буферизует
```

---

## MongoDB схема (паттерн)

```typescript
const schema = new Schema<IEntity>({
  field: { type: String, required: true, unique: true, lowercase: true, trim: true },
  isBlocked: { type: Boolean, default: false },
}, { timestamps: true,
  toJSON: { virtuals: true, transform: (_, ret) => { delete ret.__v; } }
});
// Индексы — обязательно для query fields
schema.index({ email: 1 });
schema.index({ createdAt: -1 });
```

---

## Gamification

```typescript
const POINTS = { MOVIE_WATCHED: 10, WATCH_PARTY: 15, BATTLE_WIN: 50,
                 ACHIEVEMENT: 20, DAILY_STREAK: 5 }
Ranks: Bronze(0-499) | Silver(500-1999) | Gold(2000-4999)
       Platinum(5000-9999) | Diamond(10000+)
```

---

## Logging (всегда Winston, никогда console.log)

```typescript
import { logger } from '@shared/utils/logger';
logger.info('msg', { userId });
logger.error('err', { error, stack });
// Mobile: if (__DEV__) console.log  (только dev)
```

---

## Security stack

```
helmet + DOMPurify | mongoose-sanitize | CORS whitelist
Joi/Zod на всех endpoints | bcrypt 12 rounds
```

---

## Деплой

```
Railway → production
docker-compose.dev.yml → local development
docker-compose.prod.yml → production build
nginx/ → reverse proxy config
```

---

## Запрещённые подходы

```
❌ any type в TypeScript
❌ console.log (Winston logger)
❌ DB query в controller (только в service)
❌ Nested try/catch
❌ Magic numbers (использовать constants)
❌ Hardcoded secrets
❌ Socket event rename (ломает 3 платформы)
❌ API response format change без shared/types
❌ MongoDB collection drop вручную
❌ .env в commit
❌ push в main напрямую
❌ Трогать apps/mobile/ (зона Emirhan)
❌ shared/* без lock и согласования
```

---

*ARCHITECTURE.md | WeWatch | Saidazim | updated: 2026-05-23*
