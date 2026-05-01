---
type: guide
project: weWatch
title: "Mobile Setup Guide"
date: 2026-05-01
tags: [mobile, expo, setup, react-native]
---

# 📱 Mobile Setup Guide

**Hub:** [[../00-weWatch-Overview]] | **Owner:** [[../people/Emirhan]]
**Источник:** `docs/MOBILE_SETUP.md`

## Стек
- React Native + TypeScript
- Expo SDK 54 / React Native 0.81.5
- Expo Go (dev) / EAS Build (prod)

## Первый запуск (после `git clone`)
```bash
# 1. Зависимости
cd apps/mobile && npm install

# 2. Запустить инфру
docker compose -f docker-compose.dev.yml up -d

# 3. Expo
npx expo start
```

## Переменные окружения
Файл: `apps/mobile/.env`
```
API_BASE_URL=http://localhost:3001
SOCKET_URL=http://localhost:3004
FIREBASE_API_KEY=
```

## Связанные сервисы
- [[../services/auth]] — login/register
- [[../services/watch-party]] — Socket.io rooms
- [[../concepts/FCM]] — push notifications

> Полная документация: `docs/MOBILE_SETUP.md`
