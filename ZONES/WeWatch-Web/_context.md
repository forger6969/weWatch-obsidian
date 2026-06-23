---
zone: WeWatch-Web
type: context
updated: 2026-06-23
---

# WeWatch-Web Zone — Context

## Текущее состояние (2026-06-10)

### Что сделано
- **T-E134 ✅** (2026-05-24): Брендинг CineSync → WeWatch во всех web файлах
- **T-E135 ✅** (2026-06-02): PhoneMockup UI fix — proportions (280×580px), contrast, readability
  - ScreenHome: элементы крупнее, spacing лучше
  - ScreenRoom: video preview 90px, participants крупнее
  - ScreenWatching: video area 45%, chat contrast повышен

### Стек
- Next.js (App Router)
- Путь: `apps/web/src/`
- Landing: `apps/web/src/app/page.tsx` → `LandingContent.tsx`
- Phone mockup: `apps/web/src/components/PhoneMockup/`

### Privacy Policy
- `apps/web/src/app/privacy-policy/` — существует (T-S094 ✅)
- URL: https://wewatch.uz/privacy-policy (нужно проверить что задеплоено)

## Активные задачи
- Нет активных задач (всё сделано в Sprint 10)

## Следующие возможные задачи
- SEO оптимизация landing page
- OG meta tags для social sharing
- Performance audit (Core Web Vitals)

## Связано

[[../WeWatch-Backend/_context|⚙️ Backend Zone]] | [[../WeWatch-Mobile/_context|📱 Mobile Zone]]
[[../../PROJECTS/weWatch/00-weWatch-Overview|WeWatch Overview]]
[[../../AI_CONTEXT/agents-hub|Agents Hub]]

## Сессия 2026-06-15/16 — VideoPlayer sync overhaul

### Что сделано
- **Custom video controls**: убрали `controls` атрибут → свой UI (Play/Pause, seek bar, volume, fullscreen)
- **Mac OS native player**: подавление через `setActionHandler(action, noop)` (не null!) + `disablePictureInPicture` + `x-webkit-airplay: deny`
- **Non-owner control**: кастомные controls показывают Play/Pause только owner-у; server блокирует PLAY/PAUSE от non-owner через `resolveIsOwner()`
- **Join at owner position**: `hls.startPosition` в constructor config (не property — read-only в TypeScript) → HLS.js буферит с позиции owner-а
- **Auto-resume bug FIX**: `isGenuineBufferRef` в NativeVideoPlayer + module-level `roomUserPaused` на сервере
- **Web sync lag FIX**: heartbeat 1s вместо 2s, агрессивная коррекция 1.08x/1.15x/hard-seek

### Ключевые паттерны
- `startPosition` в `new Hls({ startPosition: N })` — единственный способ (TypeScript read-only)
- `noop = () => {}` handler — пустой handler говорит OS "app handles media" → НЕ null (null = revert to defaults)
- `isGenuineBufferRef` — только отправлять BUFFER_END если BUFFER_START был отправлен (video was playing)
- `roomUserPaused` Map — module-level на сервере чтобы PAUSE event из любого socket-а видел флаг

### Файлы изменены
- `apps/web/src/components/party/VideoPlayer.tsx` — custom controls, startPosition, sync fixes
- `services/watch-party/src/socket/videoEvents.handler.ts` — module-level bufferTimeouts + roomUserPaused
- `apps/web/Dockerfile` — build-id bump для cache bust

### Pending
- Railway deploy после всех фиксов

---
## 2026-06-16 — Фикс регрессии "видео не приходит"

**Баг:** После деплоя ce73f7d у пользователя перестало приходить видео. currentTime=0 во всех PLAY/PAUSE событиях.

**Корень:** `roomUserPaused` флаг на сервере застревал в `true`. Когда sync-effect вызывал `video.pause()` и 200ms `isRemoteAction` окно истекало ДО того как `onPause` event был доставлен, `handlePause` отправлял PAUSE socket event → `roomUserPaused=true` → `resumeRoom` блокировался навсегда → VIDEO_PLAY никогда не приходил.

**Фикс (ab31114):**
- Сервер: убран `roomUserPaused` Map полностью + `clearAllBuffering` из PAUSE handler (остался только `cancelTimeout`)
- Web: добавлен `ownerExplicitlyPausedRef` в VideoPlayer — устанавливается ТОЛЬКО в `handlePlay`/`handlePause` при `!isRemoteAction`, checked в sync effect
- Mobile: уже защищён через `intendedPlayingRef` + `ownerInitialSyncedRef`

**Деплой:** web build-id="20260616-2", watch-part задеплоен