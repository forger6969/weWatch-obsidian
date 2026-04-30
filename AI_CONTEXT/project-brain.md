---
type: brain
updated: 
---

# 🧠 Мозг Клода — Архитектура и контекст

## weWatch
- Microservices monorepo: 7 backend services + mobile + admin-ui
- Socket.io для WatchParty синхронизации (event names менять НЕЛЬЗЯ!)
- Redis для кэша + Bull queues
- FCM для push уведомлений
- Railway для деплоя

## Зоны (строго соблюдать)
- services/*, apps/admin-ui/ → Saidazim
- apps/mobile/ → Emirhan
- shared/* → только с согласования

## Текущий статус
<!-- auto-updated -->
