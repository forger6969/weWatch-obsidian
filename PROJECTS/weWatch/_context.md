---
project: weWatch
type: context
last_worked: 
---

# 🎬 weWatch (CineSync / Rave)

Социальный онлайн-кинотеатр. Смотреть фильмы с друзьями, battles, achievements, gamification.

## Стек
- Auth / User / Content / WatchParty / Battle / Notification / Admin — Node.js + Express + MongoDB
- Mobile — React Native + Expo
- Infra — Redis, Elasticsearch, FCM, Socket.io

## Зоны
- **Saidazim** → services/*, apps/admin-ui/
- **Emirhan** → apps/mobile/

## Recent Commits

*Updated: 2026-04-30 12:13*

- 442b015 fix(mobile): pass inviteCode param when navigating to WatchPartyJoin from notification
- b3c1e1a fix(mobile): add shouldShowAlert for Android foreground push notifications
- 9d56459 fix(shared): use Railway auto-provided URLs as fallback for user/notification service URLs
- 64d501f chore(auth): remove temporary find user endpoint
- d41451e temp: add internal find user endpoint


## Архитектурные решения
<!-- auto-linked from decisions/ -->
