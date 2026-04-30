---
type: concept
tags: [auth, telegram, weWatch]
---
# ✈️ Telegram Auth

**Service:** [[../services/auth]] | **Hub:** [[../00-weWatch-Overview]]

## Flow
1. Bot webhook получает данные
2. Сервер создаёт/обновляет пользователя
3. Отправляет deep link кнопку в Telegram
4. Mobile получает JWT через deep link

## Deep link
- Схема: `auth_` prefix в state
- tg:// scheme для Telegram bot URL
