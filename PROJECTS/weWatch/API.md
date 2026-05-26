---
type: api-reference
project: weWatch
updated: 2026-05-23
---

# WeWatch — API Reference

> Читать перед: добавлением endpoint-а, изменением route, интеграцией сервисов.
> Обновлять при: добавлении/изменении/удалении endpoint-а.

Base URL: `https://api.wewatch.app/api/v1`
Local: `http://localhost:{PORT}/api/v1`

---

## Auth Service (port 3001)

```
POST   /auth/register          — регистрация { email, password, username }
POST   /auth/login             — вход { email, password }
POST   /auth/logout            — выход (verifyToken)
POST   /auth/refresh           — обновить токены { refreshToken }
POST   /auth/verify-email      — подтверждение email { code }
POST   /auth/resend-verify     — повторная отправка кода
POST   /auth/forgot-password   — сброс пароля { email }
POST   /auth/reset-password    — новый пароль { token, newPassword }
GET    /auth/me                — текущий юзер (verifyToken)
POST   /auth/google            — Google OAuth
POST   /auth/telegram          — Telegram Auth
```

---

## User Service (port 3002)

```
GET    /users/profile          — свой профиль (verifyToken)
PATCH  /users/profile          — обновить профиль { username, bio, avatar }
DELETE /users/account          — удалить аккаунт

GET    /users/:id              — профиль пользователя
GET    /users/search?q=        — поиск пользователей

GET    /users/friends          — список друзей
POST   /users/friends/request/:id   — отправить запрос
PATCH  /users/friends/accept/:id    — принять запрос
DELETE /users/friends/:id           — удалить друга

GET    /users/notifications         — уведомления (verifyToken)
PATCH  /users/notifications/:id/read — прочитать
PATCH  /users/notifications/read-all — все прочитать

GET    /users/leaderboard      — рейтинг пользователей
GET    /users/:id/stats        — статистика юзера
```

---

## Content Service (port 3003)

```
GET    /content/movies                    — список фильмов (paginated)
GET    /content/movies/:id                — фильм по ID
POST   /content/movies                    — добавить (operator+)
PATCH  /content/movies/:id                — обновить (operator+)
DELETE /content/movies/:id                — удалить (admin+)

GET    /content/trending?limit=10         — топ по просмотрам (Redis cache 10min)
GET    /content/top-rated?limit=10        — топ по рейтингу (Redis cache 10min)
GET    /content/continue-watching         — незавершённые (verifyToken)

POST   /content/movies/:id/progress       — сохранить прогресс { progress, duration }
GET    /content/movies/:id/progress       — получить прогресс
[alias] POST /content/watch-progress      — { movieId, progress, duration } (старый путь)
[alias] GET  /content/watch-progress?movieId=

GET    /content/search?q=&page=&limit=    — поиск (Elasticsearch)
GET    /content/categories                — список категорий
GET    /content/genres                    — список жанров

POST   /content/domains/visit             — отследить визит домена (verifyToken)
GET    /content/domains                   — список доменов (admin+)
PATCH  /content/domains/:id/block         — заблокировать домен (admin+)
```

---

## Watch Party Service (port 3004)

```
POST   /watch-party/rooms           — создать комнату { movieId, sourceUrl }
GET    /watch-party/rooms/:id       — info комнаты
DELETE /watch-party/rooms/:id       — закрыть комнату (owner only)
POST   /watch-party/rooms/:id/join  — присоединиться { inviteCode? }
POST   /watch-party/rooms/:id/leave — покинуть
GET    /watch-party/rooms/my        — мои комнаты

Socket.io events: см. ARCHITECTURE.md → Socket.io секция
```

---

## Battle Service (port 3005)

```
POST   /battles                     — вызов на battle { opponentId, movieId }
GET    /battles/:id                 — info battle
POST   /battles/:id/accept          — принять вызов
POST   /battles/:id/reject          — отклонить вызов
POST   /battles/:id/vote/:movieId   — голос за фильм
GET    /battles/my                  — мои battles

GET    /achievements                — все достижения
GET    /users/:id/achievements      — достижения юзера

GET    /leaderboard                 — глобальный рейтинг
GET    /leaderboard/friends         — рейтинг среди друзей
```

---

## Notification Service (port 3007)

```
GET    /notifications               — список (verifyToken, paginated)
PATCH  /notifications/:id/read      — прочитать
PATCH  /notifications/read-all      — все прочитать
DELETE /notifications/:id           — удалить

POST   /notifications/fcm-token     — сохранить FCM токен { token }
DELETE /notifications/fcm-token     — удалить FCM токен

Типы: friend_request | friend_accepted | watch_party_invite |
      battle_invite | battle_result | achievement_unlocked |
      friend_online | friend_watching
```

---

## Admin Service (port 3008)

```
GET    /admin/users                 — список пользователей (admin+)
GET    /admin/users/:id             — профиль пользователя
PATCH  /admin/users/:id/block       — заблокировать
PATCH  /admin/users/:id/role        — изменить роль

GET    /admin/content               — весь контент
PATCH  /admin/content/:id/approve   — одобрить фильм
DELETE /admin/content/:id           — удалить

GET    /admin/stats                 — общая статистика
GET    /admin/watch-parties         — активные комнаты
GET    /admin/battles               — активные battles

GET    /admin/support               — support чаты
GET    /admin/support/:id           — конкретный чат
POST   /admin/support/:id/message   — ответить пользователю
```

---

## Стандартные HTTP коды

```
200 OK         — успех
201 Created    — создан
400 Bad Request — ошибка валидации
401 Unauthorized — не авторизован
403 Forbidden  — нет прав (роль)
404 Not Found  — ресурс не найден
409 Conflict   — дубликат (email/username)
422 Unprocessable — бизнес-логика (battle уже принят, room уже закрыта)
429 Too Many Requests — rate limit
500 Internal   — серверная ошибка
```

---

## Environment variables (ключевые)

```bash
# Auth
JWT_PRIVATE_KEY, JWT_PUBLIC_KEY, JWT_EXPIRES_IN=15m
REFRESH_TOKEN_EXPIRES_DAYS=30

# DB
MONGODB_URI, REDIS_URL=redis://localhost:6380

# Elasticsearch
ELASTICSEARCH_URL=http://localhost:9200

# Firebase
FIREBASE_SERVICE_ACCOUNT_JSON

# Email
SENDGRID_API_KEY, FROM_EMAIL

# Services (inter-service calls)
AUTH_SERVICE_URL, USER_SERVICE_URL, CONTENT_SERVICE_URL
WATCH_PARTY_SERVICE_URL, BATTLE_SERVICE_URL, NOTIFICATION_SERVICE_URL

# Admin
ADMIN_UI_URL, EXPO_PUBLIC_ADMIN_URL  # НЕ добавлять /api/v1 к этому!

# Depl
RAILWAY_TOKEN, PORT
```

---

*API.md | WeWatch | Saidazim | updated: 2026-05-23*
