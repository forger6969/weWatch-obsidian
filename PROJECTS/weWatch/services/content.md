---
type: service
tags: [weWatch, backend, content]
port: 3003
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

## Кэш
- [[../concepts/Redis]] — trending:N (TTL 10min), top-rated:N

## Связи
- → [[watch-party]] — videoUrl для комнаты
- ← [[../services/mobile]] — HomeScreen, поиск
- ← [[../services/admin-ui]] — управление контентом
