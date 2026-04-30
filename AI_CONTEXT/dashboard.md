---
type: dashboard
---

# 🎯 Dashboard

## Проекты
- [[PROJECTS/weWatch/_context|🎬 weWatch]] — Социальный кинотеатр
- [[PROJECTS/tezCode/_context|🏢 tezCode]] — Команда

## Сегодня
```dataview
LIST
FROM "DAILY"
WHERE date = date(today)
```

## Открытые баги weWatch
```dataview
LIST title
FROM "PROJECTS/weWatch"
WHERE type = "bug" AND status = "open"
```

## Последние решения
```dataview
LIST title
FROM "PROJECTS/weWatch/decisions"
SORT date DESC
LIMIT 5
```
