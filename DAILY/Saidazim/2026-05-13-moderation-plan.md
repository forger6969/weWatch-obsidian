# 🛡️ Модерация — Большой план (2026-05-13)

## Статус: 🚧 В РАБОТЕ — продолжить если лимит закончился

---

## ЧТО УЖЕ ЕСТЬ (не трогать, использовать)

| Компонент | Файл | Статус |
|-----------|------|--------|
| UrlVisit model | `services/content/src/models/urlVisit.model.ts` | ✅ есть (domain, flagged, blocked) |
| blocked-domains API | `GET /api/v1/content/blocked-domains` | ✅ есть (public, кэш 1ч) |
| useDynamicBlockedDomains | `apps/mobile/src/hooks/useDynamicBlockedDomains.ts` | ✅ есть (синхронизация) |
| WatchPartiesPage | `apps/admin-ui/src/pages/WatchPartiesPage.tsx` | ✅ есть (базовый список) |
| DomainsPage | `apps/admin-ui/src/pages/DomainsPage.tsx` | ✅ есть (block/unblock) |
| Room модель | `services/watch-party/src/models/watchPartyRoom.model.ts` | ⚠️ нет isSuspicious, isBlocked |
| User модель | `services/user/src/models/user.model.ts` | ❌ нет restrictions[] |
| Internal rooms endpoint | `GET /internal/watch-party/rooms` | ✅ есть |

---

## ЗАДАЧИ (параллельные агенты)

### 🔵 AGENT 1 — Backend (services/)

#### 1.1 User restrictions
- Добавить в `services/user/src/models/user.model.ts`:
  ```typescript
  restrictions: { type: [String], default: [] }
  // Возможные значения: 'create_room' | 'change_username' | 'send_message' | 'join_room' | 'upload_avatar' | 'use_chat' | 'create_battle'
  ```
- `services/user/src/services/profile.service.ts` — добавить `adminSetRestrictions(userId, restrictions)`
- `services/user/src/controllers/user.controller.ts` — `PATCH /internal/admin/users/:id/restrictions`
- `services/user/src/routes/user.routes.ts` — зарегистрировать маршрут
- Enforce in `services/watch-party/src/services/watchParty.service.ts` createRoom — проверить restrictions

#### 1.2 Room suspicious content filtering
- Добавить в `services/watch-party/src/models/watchPartyRoom.model.ts`:
  ```typescript
  isSuspicious: { type: Boolean, default: false }
  suspiciousReason: { type: String, default: null }
  isAdminBlocked: { type: Boolean, default: false }
  domain: { type: String, default: null }  // извлечь из videoUrl
  ```
- Создать `services/watch-party/src/utils/contentFilter.ts` — словарь запрещённых слов + функция check
- В createRoom/setVideo: вызвать contentFilter, если совпадение → isSuspicious=true
- В createRoom: извлечь domain из videoUrl, залогировать через content service

#### 1.3 Domain logging при создании комнаты
- В `services/watch-party/src/services/watchParty.service.ts` createRoom:
  - Извлечь domain из videoUrl
  - POST `/internal/content/domains/visit` (создать этот эндпоинт в content service)
  - Проверить: если domain заблокирован → throw error с кодом DOMAIN_BLOCKED

#### 1.4 Admin restrictions endpoint
- `services/admin/src/services/admin.service.ts` — добавить `setUserRestrictions(userId, restrictions)`
- Вызывает `adminSetUserRestrictions` из shared/utils/adminServiceClient.ts

#### 1.5 Shared types
- `shared/src/types/index.ts` — добавить тип UserRestriction
- `shared/src/utils/adminServiceClient.ts` — добавить `adminSetRestrictions(userId, restrictions)`

---

### 🟢 AGENT 2 — Mobile (apps/mobile/src/)

#### 2.1 Blocked domain UI
- Найти где показывается popup для видео (WebView/Player компонент) — скорее всего `apps/mobile/src/screens/watchparty/` или `apps/mobile/src/components/`
- Когда URL домен в заблокированных → вместо плеера показать `BlockedDomainView` компонент:
  ```
  🚫 Этот сайт заблокирован
  [domain.com]
  Данный ресурс нарушает политику конфиденциальности CineSync
  ```
- Использовать `useDynamicBlockedDomains` hook для проверки
- Также в WatchPartyJoin/Create — проверить URL при вводе, показать warning

#### 2.2 Ограничения при создании комнаты
- В WatchPartyCreate экране: если API вернул 403 с кодом USER_RESTRICTED → показать причину

---

### 🟡 AGENT 3 — Admin UI (apps/admin-ui/src/)

#### 3.1 WatchPartiesPage улучшения
- Добавить фильтр: Все | Подозрительные | Заблокированные | Активные
- Колонка: thumbnail + isSuspicious badge
- Кнопки: Block Room (закрыть + запретить переоткрытие), Warn Owner
- Если suspiciousReason — показывать tooltip

#### 3.2 User restrictions в UserDetailPage
- Добавить секцию "Ограничения" после секции "Информация"
- Чекбоксы для каждого restriction типа
- Кнопка "Сохранить ограничения"
- API: PATCH /admin/users/:id/restrictions

#### 3.3 DomainsPage + WatchPartiesPage связь
- В WatchPartiesPage: кликабельный domain → переход на DomainsPage с фильтром

---

## СЛОВАРЬ ЗАПРЕЩЁННЫХ СЛОВ (contentFilter.ts)

```typescript
// Основные категории
const FORBIDDEN_PATTERNS = [
  // Порнография
  /\bporn\b/i, /\bxxx\b/i, /\bsex\b/i, /\bnude\b/i, /\bnaked\b/i,
  /порно/i, /секс/i, /голая/i, /эротика/i,
  // Инцест-контент
  /step.?sister/i, /step.?mom/i, /step.?brother/i, /step.?dad/i,
  /сводная сестра/i, /мачеха/i, /отчим/i,
  // Насилие
  /\bsnuff\b/i, /gore/i, /beheading/i,
  // Другие
  /hentai/i, /onlyfans/i, /brazzers/i, /pornhub/i, /xvideos/i, /xhamster/i,
  /redtube/i, /youporn/i,
]
```

---

## АРХИТЕКТУРА DOMAIN BLOCKING (мобилка)

```
VideoURL введён
    ↓
extractDomain(url)
    ↓
blockedDomains.includes(domain)?
    YES → <BlockedDomainView domain={domain} />
    NO  → <VideoPlayer url={url} />
```

---

## АРХИТЕКТУРА USER RESTRICTIONS

```
User.restrictions = ['create_room', 'change_username']

При createRoom:
  GET user restrictions
  if restrictions.includes('create_room') → 403 USER_RESTRICTED

При changeUsername:
  GET user restrictions  
  if restrictions.includes('change_username') → 403 USER_RESTRICTED
```

---

## ФАЙЛЫ КОТОРЫЕ НАДО СОЗДАТЬ

- [ ] `services/watch-party/src/utils/contentFilter.ts` — словарь + функция
- [ ] `apps/admin-ui/src/components/ui/RestrictionsPanel.tsx` — UI компонент
- [ ] `apps/mobile/src/components/common/BlockedDomainView.tsx` — UI заблокированного сайта

## ФАЙЛЫ КОТОРЫЕ НАДО ИЗМЕНИТЬ

- [ ] `services/watch-party/src/models/watchPartyRoom.model.ts` — +isSuspicious, +domain, +isAdminBlocked
- [ ] `services/watch-party/src/services/watchParty.service.ts` — domain logging + content filter
- [ ] `services/user/src/models/user.model.ts` — +restrictions[]
- [ ] `services/user/src/services/profile.service.ts` — +adminSetRestrictions
- [ ] `services/user/src/controllers/user.controller.ts` — +restrictions endpoint
- [ ] `services/user/src/routes/user.routes.ts` — +маршрут
- [ ] `shared/src/types/index.ts` — +UserRestriction type
- [ ] `shared/src/utils/adminServiceClient.ts` — +adminSetRestrictions
- [ ] `services/admin/src/services/admin.service.ts` — +setUserRestrictions
- [ ] `services/admin/src/controllers/admin.controller.ts` — +restrictions endpoint
- [ ] `services/admin/src/routes/admin.routes.ts` — +маршрут
- [ ] `apps/admin-ui/src/pages/UserDetailPage.tsx` — +restrictions секция
- [ ] `apps/admin-ui/src/pages/WatchPartiesPage.tsx` — +suspicious filter + moderation
- [ ] `apps/admin-ui/src/api/users.api.ts` — +setRestrictions
- [ ] `apps/mobile/src/` — BlockedDomainView компонент + интеграция

---

*Создан: 2026-05-13 | Исполнитель: Saidazim + Claude*
