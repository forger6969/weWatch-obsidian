---
type: service
tags: [weWatch, backend, gamification]
port: 3005
---
# ⚔️ Battle Service

**Port:** 3005 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Режимы
- 1v1: кто больше посмотрит за 3/5/7 дней
- Группа: командные соревнования

## Очки (POINTS)
- MOVIE_WATCHED: 10
- WATCH_PARTY: 15
- BATTLE_WIN: 50
- ACHIEVEMENT: 20-100
- DAILY_STREAK: 5

## Ранги
- Bronze → Silver → Gold → Platinum → Diamond

## Связи
- ← [[user]] — профиль и очки
- → [[notification]] — результаты battles
- ← [[../services/mobile]] — Battle экраны
