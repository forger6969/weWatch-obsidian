---
type: log
project: weWatch
title: "Debug Log"
date: 2026-05-01
tags: [debug, bugs, fixes]
---

# 🐛 Debug Log

**Hub:** [[../00-weWatch-Overview]] | **Источник:** `docs/DebugLog.md`
**Ответственные:** [[../people/Saidazim]] (Backend) | [[../people/Emirhan]] (Mobile)

> Хронологический лог багов и их решений.
> Полный лог: `docs/DebugLog.md`

## Связанные файлы
- [[../../../TASKS/active]] — Активные задачи
- [[../../../TASKS/done]] — Завершённые задачи
- [[_bugs]] — Баги weWatch

## Последние фиксы (из git)

### 2026-05-01
- `fix(player)`: never fall back to YouTube iframe embed when proxy URL exists
- `fix(youtube)`: store original URL in room, pass YouTube URL to proxy

### 2026-04-30
- `fix(content)`: pass poToken+visitorData to ytdl agent + 15s timeout
- `fix(user)`: save username on profile update + fix avatar response key
- `fix(mobile)`: pass inviteCode param when navigating to WatchPartyJoin from notification
