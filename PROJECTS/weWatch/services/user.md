---
type: service
tags: [weWatch, backend, user]
port: 3002
---
# 👤 User Service

**Port:** 3002 | **Owner:** [[../people/Saidazim]]
**Hub:** [[../00-weWatch-Overview]]

## Функции
- Профили пользователей
- Система друзей (request/accept/reject)
- Рейтинги и очки
- FCM токены → [[../concepts/FCM]]

## Связи
- ← [[auth]] — получает userId после JWT verify
- → [[notification]] — уведомления о друзьях
- → [[battle]] — очки и рейтинг
- ← [[../services/mobile]] — профиль экраны
