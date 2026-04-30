---
type: service
tags: [weWatch, backend, auth]
port: 3001
---
# 🔐 Auth Service

**Port:** 3001 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Стек
- [[../concepts/JWT]] — Access (15min RS256) + Refresh (30d)
- [[../concepts/MongoDB]] — RefreshToken collection
- [[../concepts/Redis]] — Brute force protection

## Провайдеры
- Email/Password — bcrypt 12 rounds
- [[../concepts/Google-OAuth]] — polling flow (Expo Go)
- [[../concepts/Telegram-Auth]] — bot webhook

## Связи
- → [[user]] — создаёт профиль после регистрации
- → [[notification]] — отправляет verification email
- ← [[../services/mobile]] — мобильный клиент
- ← [[../services/admin-ui]] — панель управления

## Решения
- [[../decisions/2026-04-30-obsidian-vault-setup-complete]]
