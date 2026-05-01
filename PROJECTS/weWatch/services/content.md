---
type: service
tags: [weWatch, backend, content]
port: 3003
updated: 2026-05-01 06:36
---
# 🎬 Content Service

**Port:** 3003 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Функции
- Каталог фильмов
- Поиск → [[../concepts/Elasticsearch]]
- Video extraction (YouTube, Rutube, VK)
- Watch Progress tracking
- Trending / Top-rated

## Video Extraction

### YouTube (ytdl-core)
```typescript
// ytdl.getInfo(videoId) → DASH MPD manifest
// poToken + visitorData для обхода age-gate
// 15 секунд timeout
```

### Как это делает Rave (для сравнения)
Rave использует тот же ytdl-core + генерирует DASH MPD:
```javascript
const mpd = generate_dash_file_from_formats(
  info.player_response.streamingData.adaptiveFormats,
  info.videoDetails.lengthSeconds
)
// Retry: 2 раза, minTimeout 2500ms, maxTimeout 10000ms
```
→ Подробнее: [[../analysis/rave-reverse-engineering]]

## Кэш
- [[../concepts/Redis]] — trending:N (TTL 10min), top-rated:N

## Связи
- → [[watch-party]] — videoUrl для комнаты
- ← [[../services/mobile]] — HomeScreen, поиск
- ← [[../services/admin-ui]] — управление контентом
