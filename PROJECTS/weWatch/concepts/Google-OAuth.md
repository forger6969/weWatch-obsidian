---
type: concept
tags: [auth, oauth, weWatch]
---
# 🔵 Google OAuth

**Service:** [[../services/auth]] | **Hub:** [[../00-weWatch-Overview]]

## Polling flow (Expo Go)
1. Mobile открывает браузер → Google
2. Backend создаёт pendingAuth в [[Redis]]
3. Mobile поллит /auth/google/status каждые 2s
4. После callback → возвращает JWT

## Grace period
После закрытия браузера — 10s grace period для poll
