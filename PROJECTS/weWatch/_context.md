---
type: context
project: weWatch
tags: [weWatch, backend, architecture]
updated: 2026-05-01 06:35
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

*Updated: 2026-05-01 06:42*

- 85e4a37 fix(player): never fall back to YouTube iframe embed when proxy URL exists
- 3615c50 fix(youtube): store original URL in room, pass YouTube URL to proxy
- 33aa37a fix(content): pass poToken+visitorData to ytdl agent + add 15s timeout
- 11dedfc fix(user): save username on profile update + fix avatar response key
- 442b015 fix(mobile): pass inviteCode param when navigating to WatchPartyJoin from notification


## Архитектурные решения
- [[decisions/2026-04-30-obsidian-vault-setup-complete]]
- [[analysis/rave-reverse-engineering]] — Rave sync mechanism (NTP + Priapus WSS + drift compensation)
