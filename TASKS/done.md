---
type: tasks-done
synced: 2026-05-01 06:34
source: docs/Done.md
---

# ✅ Completed Tasks

> Auto-synced from `docs/Done.md` at 2026-05-01 06:34


- **Mas'ul:** Saidazim
- **Bajarildi:**
  - `.github/PULL_REQUEST_TEMPLATE.md` — TypeScript, security, zone, API format tekshiruv ro'yxati
  - `.github/ISSUE_TEMPLATE/bug_report.md` — servis, fayl, qayta ishlab chiqarish, log maydonlari
  - `.github/ISSUE_TEMPLATE/feature_request.md` — prioritet, zona, texnik yondashuv maydonlari

---

### F-020 | 2026-02-27 | [DEVOPS] | CI/CD GitHub Actions (T-S010)

- **Mas'ul:** Saidazim
- **Bajarildi:**
  - `.github/workflows/lint.yml` — PR da barcha 8 service typecheck (matrix strategy, fail-fast: false)
  - `.github/workflows/test.yml` — PR da Jest tests (MongoDB + Redis service containers)
  - `.github/workflows/docker-build.yml` — develop/main push da Docker build + GHCR push (7 service, cache-from/to gha)
  - `.github/workflows/deploy-staging.yml` — develop branch → staging (environment: staging, manual trigger placeholder)
  - `.github/workflows/deploy-prod.yml` — main branch → production (workflow_dispatch confirm='yes' + push, environment: production)

---

### F-021 | 2026-02-27 | [BACKEND] | Swagger API Docs + /api/v1/ prefix (T-S011 + T-C001)

- **Mas'ul:** Saidazim
- **Bajarildi:**
  - Barcha 7 service `src/utils/swagger.ts` — swagger-jsdoc config (OpenAPI 3.0, bearerAuth, tags)
  - Barcha 7 service `app.ts` — `GET /api-docs` (Swagger UI) + `GET /api-docs.json` (spec) route qo'shildi
  - **API versioning** — barcha 7 service `/api/v1/` prefix:
    - auth: `/api/v1/auth`
    - user: `/api/v1/users`, `/api/v1/achievements`
    - content: `/api/v1/movies`
    - watch-party: `/api/v1/watch-party`
    - battle: `/api/v1/battles`
    - notification: `/api/v1/notifications`
    - admin: `/api/v1/admin`, `/api/v1/operator`
  - `swagger-jsdoc` + `swagger-ui-express` — root workspace da o'rnatildi

---

### F-022 | 2026-02-28 | [BACKEND] | Auth E2E login testi + Services startup + ES index yaratildi (T-S001)

- **Mas'ul:** Saidazim
- **Bajarildi:**
  - Barcha 7 service ishga tushirildi (ports 3001-3008, hammasi `/health` → 200 OK)
  - `services/content/src/utils/elastic.init.ts` — BUG-012 tuzatildi: apostrophe_filter mappings ASCII → Unicode escape sequences
  - `services/content/src/utils/elastic.init.ts` — BUG-013 tuzatildi: `boost` parametri ES 8.x incompatible, o'chirildi
  - Elasticsearch `movies` index muvaffaqiyatli yaratildi (green, 1 shard, 0 replica)
  - Auth login E2E test o'tdi: `POST /api/v1/auth/login` → `accessToken` + `refreshToken` + `user` qaytadi
  - Seed credentials (test1@cinesync.app / Test123!) bilan login ✅ ishladi
  - **SMTP (email):** mailtrap.io dan credentials kerak bo'lganda to'ldirish (ixtiyoriy dev uchun)

---

---

---

### F-035 | 2026-02-28 | [WEB] | Next.js Web App — Sprint 1-4 (T-J001..T-J006)

- **Mas'ul:** Jafar
- **Sprint:** S1-S4
- **Commit:** `f32c5e5 feat(web): add Next.js web app — Sprint 1-5 (T-J001..T-J007)`
- **Bajarildi:**
  - **T-J001** — Next.js App Router setup, Tailwind v4, Shadcn/ui, Zustand + React Query, Socket.io client, JWT auth middleware
  - **T-J002** — Landing page: Hero, Features, How it works, Testimonials, Pricing, FAQ, JSON-LD schema, SEO metadata
  - **T-J003** — App layout (sidebar/topbar), `(app)/home/page.tsx` (SSR+ISR), `(app)/movies/[slug]/page.tsx` (dynamic metadata + Movie JSON-LD)
  - **T-J004** — `VideoPlayer.tsx` (hls.js, custom controls, keyboard shortcuts Space/Arrow/F/M, ±2s Watch Party sync), `(app)/search/page.tsx` (debounced, infinite scroll)
  - **T-J005** — `(app)/party/[roomId]/page.tsx` (70% video + 30% chat split layout, sync state, floating emoji, members list), `ChatPanel.tsx`
  - **T-J006** — `(app)/battle/page.tsx` (create modal, filter), `(app)/profile/[username]/page.tsx` (SSR, OG meta, achievements grid, rank badge), `(app)/stats/page.tsx`
  - `manifest.json` + `robots.txt` + PWA icons (72..512px)
  - Playwright test suite (`/tests/auth.spec.ts`) + `playwright.config.ts`
  - API rewrites (`next.config.mjs`) → backend services (3001-3007)

---

### F-036 | 2026-02-28 | [IKKALASI] | Design Tokens — T-C002

- **Mas'ul:** Saidazim + Emirhan + Jafar
- **Sprint:** S1
- **Bajarildi:**
  - **Mobile:** `apps/mobile/src/theme/index.ts` — colors (#E50914, #0A0A0F, #111118...), spacing, borderRadius, typography (Bebas Neue / DM Sans), shadows, RANK_COLORS
  - **Web:** `apps/web/src/app/globals.css` — Tailwind v4 `@theme` block, CSS custom properties
  - Dark mode ONLY — barcha platform

---

---

---

---

---

---

### F-041 | 2026-03-02 | [DEVOPS] | Docker — web hot-reload va bitta komanda setup

- **Mas'ul:** Saidazim
- **Bajarildi:**
  - `apps/web/Dockerfile.dev` — `WATCHPACK_POLLING=true` qo'shildi (Docker FS polling)
  - `docker-compose.dev.yml` — web service ga volumes qo'shildi: `./apps/web/src`, `./apps/web/public`, `web_node_modules`, `web_next_cache`
  - `apps/web/package.json` — `@tailwindcss/oxide-linux-x64-gnu` o'chirildi (Alpine musl bilan mos kelmaydi)
  - Bitta komanda: `docker compose -f docker-compose.dev.yml up -d --build`

---

### F-042 | 2026-03-02 | [BACKEND] | User Service — do'stlik endpointlari qo'shildi

- **Mas'ul:** Saidazim
- **Bajarildi:**
  - `GET /api/v1/users/search?q=` — username bo'yicha qidiruv + `isOnline` holati
  - `GET /api/v1/users/friends` — do'stlar ro'yxati (avval faqat `/me/friends` bor edi)
  - `GET /api/v1/users/friends/requests` — pending so'rovlar, requester profili bilan populate qilingan
  - `POST /api/v1/users/friends/request` — body `{userId}` bilan so'rov yuborish
  - `PATCH /api/v1/users/friends/accept/:friendshipId` — friendship `_id` bilan qabul qilish

---

### BUG-B001 | 2026-03-02 | [BACKEND] | Express route ordering — `/:id` statik routelarni yutib olishi

- **Mas'ul:** Saidazim
- **Muammo:** `GET /:id` dinamik route `GET /friends`, `GET /search` kabi statik routelardan OLDIN
  ro'yxatdan o'tgan edi. Express `/friends` ni `id="friends"` deb qabul qilgan →
  `User.findOne({ authId: "friends" })` → 404 "User not found".
- **Yechim:** Barcha statik routelar `/:id` dan OLDIN ro'yxatdan o'tkazildi.
- **QOIDA — UCHALA DASTURCHI UCHUN:**

```
❌ NOTO'G'RI:
  router.get('/:id', ...)        ← dinamik birinchi
  router.get('/search', ...)     ← hech qachon yetmaydi
  router.get('/me/friends', ...) ← hech qachon yetmaydi

✅ TO'G'RI:
  router.get('/me', ...)         ← statik — /me
  router.get('/me/friends', ...) ← statik — /me/friends
  router.get('/search', ...)     ← statik — /search
  router.get('/friends', ...)    ← statik — /friends
  router.get('/:id', ...)        ← dinamik — ENG OXIRIDA
```

---

### BUG-B002 | 2026-03-02 | [BACKEND] | User identifier mismatch — `_id` vs `authId`

- **Mas'ul:** Saidazim
- **Muammo:** Web `u._id` (MongoDB profile ObjectId) yuboradi, backend `authId` (auth service userId)
  bo'yicha qidiradi → 404 "User not found".
- **Yechim:** `sendFriendRequestByProfileId()` metodi qo'shildi — `_id` orqali `authId` ni
  topib keyin operatsiyani bajaradi.
- **QOIDA — UCHALA DASTURCHI UCHUN:**

```
User collection da IKKI xil identifier bor:

  _id     → MongoDB profile ObjectId  (69a54b70f808cfa9413654f0)
              - faqat user service ichki ishlatish uchun
              - frontend ga expose qilmang (to'g'ridan foydalanmang)

  authId  → Auth service user._id     (69a545eee6496cf6ac946ecc)
              - servislar arasi muloqot uchun STANDART identifier
              - JWT ichida userId = authId
              - Friendship, Battle, WatchParty — barchasi authId ishlatadi

QOIDALAR:
  ✅ Servislar arasi: authId ishlatish
  ✅ Frontend → backend: authId yuborish (search response da authId bor)
  ✅ u.authId — to'g'ri
  ❌ u._id   — foydalanuvchini identify qilish uchun XATO
```

---

### BUG-B003 | 2026-03-02 | [DEVOPS] | root package.json ga react/react-dom qo'shish XATO

- **Mas'ul:** Saidazim
- **Muammo:** `react: 18.3.1` va `react-dom: 18.3.1` monorepo root `package.json` ga
  `dependencies` sifatida qo'shilgan. npm workspaces hoisting natijasida `apps/web` ning
  React versiyasi bilan collision → 129 TypeScript xatosi.
- **Yechim:** Root `package.json` dan o'chirish kerak — `apps/web/package.json` da allaqachon bor.
- **QOIDA:**

```
Root package.json dependencies:
  ✅ swagger-jsdoc, swagger-ui-express  — backend uchun shared dev tools
  ✅ @playwright/test                   — test uchun
  ❌ react, react-dom                   — faqat apps/web/package.json da bo'lishi kerak
  ❌ react-native, expo                 — faqat apps/mobile/package.json da bo'lishi kerak
```

---

### T-S034 | 2026-03-19 | [BACKEND] | Full backend refactor — Faza 1-2-3

- **Mas'ul:** Saidazim
- **Commit:** `85bbd6f`

**Faza 1 — Critical bugs:**
- `rateLimitMap` memory leak — watch-party socket da setInterval(60s) cleanup qo'shildi
- MongoDB `maxPoolSize`: 10 → 5 (7 servis × 5 = 35, Atlas 100 limit dan xavfsiz)
- `REDIS_KEYS` to'liq namespace bilan: `auth:`, `user:`, `content:`, `party:`, `battle:`
- `admin.service.ts` hardcoded `session:${userId}` → `REDIS_KEYS.userSession()`

**Faza 2 — File splitting (Facade pattern):**
- `auth.service.ts` (654 LOC) → `passwordAuth.service.ts` + `googleAuth.service.ts` + `telegramAuth.service.ts` + facade
- `user.service.ts` (464 LOC) → `profile.service.ts` + `friendship.service.ts` + facade
- `content.service.ts` (511 LOC) → `movie.service.ts` + `search.service.ts` + `watchHistory.service.ts` + facade
- `watchParty.socket.ts` (369 LOC) → `roomEvents.handler.ts` + `videoEvents.handler.ts` + `chatEvents.handler.ts` + `voiceEvents.handler.ts`

**Faza 3 — Shared abstractions:**
- `shared/middleware/requestId.middleware.ts` — X-Request-ID tracing header
- `shared/middleware/timeout.middleware.ts` — 30s global timeout (503)
- Barcha 7 servis `app.ts`: `requestId` + `timeout()` middleware qo'shildi

---

### F-182 | T-S054 | 2026-04-17 | Predictive sync — scheduledAt field (Saidazim)

`scheduledAt: now + 150` field qo'shildi — barcha peer'lar PLAY/PAUSE/SEEK aniq bir UTC vaqtda bajaradi.

- `shared/src/types/index.ts` → `SyncState.scheduledAt?: number`
- `services/watch-party/src/services/watchParty.service.ts` → `syncState()`: `scheduledAt: now + 150`
- Commit: `13da353`

---

### F-183 | T-S056 | 2026-04-18 | VIDEO_HEARTBEAT отдельное событие (Saidazim)

`CLIENT_EVENTS.HEARTBEAT = 'video:heartbeat'` + `SERVER_EVENTS.VIDEO_HEARTBEAT` добавлены.
Handler: owner check + broadcast `{ currentTime, timestamp, updatedBy }` без `scheduledAt`.
Peers используют только drift correction (playbackRate), не seekTo — прыжки устранены.

- `shared/src/constants/socketEvents.ts` — HEARTBEAT + VIDEO_HEARTBEAT
- `services/watch-party/src/socket/videoEvents.handler.ts` — HEARTBEAT handler
- Commit: `e39c018`

---

### F-184 | T-S055 | 2026-04-18 | Democratic buffer wait (Saidazim)

BUFFER_START от любого пира → пауза всей комнаты. BUFFER_END когда все готовы → автоматическое возобновление.
Redis Set отслеживает буферящих пользователей. Safety timeout 30s → force resume.
На disconnect пользователь удаляется из Set.

- `shared/src/constants/index.ts` → `REDIS_KEYS.bufferingUsers`
- `watchParty.service.ts` → `markBuffering`, `unmarkBuffering`, `clearAllBuffering`
- `videoEvents.handler.ts` → BUFFER_START/BUFFER_END полная логика
- Commit: `b45f454`

---

### F-185 | T-E098 + T-E100 | 2026-04-18 | Predictive sync + WebView polling (Emirhan)

- `useWatchPartyRoom.ts` → `scheduledAt`: `delay = scheduledAt - Date.now()` → `setTimeout(play, delay)`; `delay ≤ 0` → seek компенсация
- `useWebViewPlayer.ts` → har 2s JS injection: `video.currentTime` → `postMessage(POSITION_POLL)`; faqat `isPlaying=true` da
- Commit: `670d319`

---

### F-186 | T-E099 | 2026-04-18 | Drift correction via playbackRate (Emirhan)

- `useWatchPartyRoom.ts` → `VIDEO_HEARTBEAT` listener: drift > 2s → seekTo; 0.3–2s → playbackRate 0.95/1.05; < 0.3s → ignore
- `expo-av`: `setRateAsync(rate, shouldCorrectPitch: true)`
- Commit: `d342d5f`

---

### F-187 | T-C014 | 2026-04-18 | Shared WebRTC mesh socket events + types (Saidazim)

- `shared/constants/socketEvents.ts` → SERVER_EVENTS: `PEER_OFFER/ANSWER/ICE`, `MESH_PEER_JOINED/LEFT`
- `shared/constants/socketEvents.ts` → CLIENT_EVENTS: `PEER_OFFER/ANSWER/ICE`, `MESH_JOIN/LEAVE`
- `shared/types/index.ts` → `MeshSignalPayload`, `SyncMessage`, `MeshSignalType`
- Разблокирует: T-S052 (backend mesh handler) + T-E096 (mobile MeshClient)
- Commit: `c65dc06`

---

### F-188 | T-S052 | 2026-04-18 | Mesh signalling handler — peer:offer/answer/ice relay (Saidazim)

Pure relay pattern — сервер не хранит WebRTC состояние, только маршрутизирует сигналы через личные комнаты `user:${userId}`.
MESH_JOIN/LEAVE бродкастятся всей комнате. Автоматический MESH_PEER_LEFT при дисконнекте.

- `services/watch-party/src/socket/mesh.handlers.ts` (новый файл)
- `watchParty.socket.ts` → `registerMeshHandlers(io, socket, authSocket)`
- Тест: 5/5 PASS (join, offer, answer, ice, leave)
- Commit: `b916a9b`

---

### F-189 | T-S051 | 2026-04-18 | Playwright stealth + UA rotation (Saidazim)

- `playwrightExtractor.ts`: random UA из 5 вариантов, случайный viewport, `--disable-blink-features=AutomationControlled`, init script: `navigator.webdriver=false`, `window.chrome={runtime:{}}`
- `genericExtractor.ts`: random UA каждый запрос, 100-300ms задержка между iframe рекурсиями
- `index.ts`: generic TTL 1h → 6h (CIS сайты дорого re-extract через Playwright)
- Commit: `b72b1ea`

---

_docs/Done.md | CineSync | Yangilangan: 2026-04-18_
