---
type: concept
tags: [notifications, mobile, weWatch]
---
# 🔥 Firebase FCM

**Role:** Push notifications | **Hub:** [[../00-weWatch-Overview]]

## Flow
[[../services/mobile]] → регистрирует token
→ [[../services/user]] — сохраняет fcmTokens[]
→ [[../services/notification]] — отправляет push

## Особенности
- Set-based dedup токенов (предотвращает 10x дублирование)
- Android: shouldShowAlert для foreground
