---
type: architecture
project: weWatch
title: "Mobile Guidelines (CLAUDE_MOBILE.md)"
date: 2026-05-01
tags: [mobile, expo, react-native, zustand, navigation]
---

# 📱 Mobile Guidelines

**Hub:** [[../00-weWatch-Overview]] | **Owner:** [[../people/Emirhan]]
**Источник:** `CLAUDE_MOBILE.md`

---

## Зона (трогать ТОЛЬКО)
```
apps/mobile/src/
├── screens/       ← MAX 300 строк
├── components/    ← MAX 150 строк
├── navigation/    ← React Navigation
├── hooks/         ← Custom hooks
├── api/           ← Axios layer
├── store/         ← Zustand stores
├── socket/        ← Socket.io client
├── theme/         ← Design system
└── types/         ← TypeScript types
```
🚫 **НЕ ТРОГАТЬ:** `services/*`, `apps/admin-ui/`

---

## Navigation Structure
```
AppNavigator
├── AuthStack
│   ├── SplashScreen
│   ├── LoginScreen
│   ├── RegisterScreen
│   └── VerifyEmailScreen
└── MainTabs
    ├── HomeScreen
    ├── SearchScreen
    ├── RoomsScreen      ← ГЛАВНЫЙ (Rave-style)
    ├── FriendsScreen
    └── ProfileScreen
```

---

## Стейт-менеджмент (Zustand)
```typescript
// Stores:
authStore.ts         ← user, token, isAuthenticated
watchPartyStore.ts   ← room, members, syncState
notificationStore.ts ← notifications list, unreadCount
```

---

## Watch Party Sync (текущая реализация)
```typescript
// hooks/useWatchParty.ts
socket.on('video:sync', (payload) => {
  // TODO: добавить drift compensation
  // drift = (Date.now() - payload.sentAt) / 1000
  videoRef.current?.setPositionAsync(payload.position * 1000)
})
```

> ⚠️ **TODO:** Добавить NTP drift compensation
> Подробнее: [[../analysis/rave-reverse-engineering]]

---

## Правила кода
```typescript
// ✅ if (__DEV__) console.log(...)  // только dev
// ❌ console.log(...)               // в prod НЕЛЬЗЯ
// ✅ StyleSheet.create({})          // всегда
// ❌ style={{ ... }}                // inline запрещено
// ❌ any type                       // TypeScript strict
```

---

## Связанные
- [[../services/mobile]]
- [[../services/watch-party]]
- [[../concepts/Socket.io]]
- [[../concepts/FCM]]
- [[../docs/mobile-setup]]

> Полная документация: `CLAUDE_MOBILE.md`
