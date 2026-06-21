# nyx-shop-bot (doonya_shop)

**Путь:** `/Users/saidazim/Desktop/nyx-shop-bot/`
**GitHub:** `github.com/forger6969/doonya_shop`
**Тип:** Telegram Mini App — магазин игровых товаров (UC, Robux, Stars, Gems и т.д.)

## Стек
- **Backend:** FastAPI + Motor (async MongoDB) + aiogram v3
- **Frontend:** React + TypeScript + Vite + Tailwind CSS
- **DB:** MongoDB Atlas (`doonya_shop`)
- **Медиа:** Cloudinary (папка `doonya_shop/catalog`)
- **Deploy:** Render

## Структура
```
backend/     — FastAPI routers: admin, support, auth, orders, promos
bot/         — aiogram v3 бот
frontend/    — React TMA (CatalogPage, AdminPage, SupportPage, SupportAgentPage)
```

## Ключевые факты
- Варианты товаров **убраны** (2026-06-21): каждый вариант = отдельный продукт в MongoDB
- `migrate_variants.py` — скрипт миграции (уже выполнен, 122 товара создано, 17 родителей деактивированы)
- `tsc -b` — билд команда (строже чем `tsc --noEmit`, падает на TS6133 unused imports)
- Поддержка реализована: WebSocket чат (юзер↔агент), `SupportPage.tsx` + `SupportAgentPage.tsx` + `backend/routers/support.py`
- `SUPPORT_AGENT_IDS` в `.env` — список ID агентов поддержки
- Скидки: `PATCH /admin/products/{id}/discount` — на каждый продукт отдельно

## Игры и категории
PUBG (UC), Telegram (Stars, Premium, Gifts), Clash of Clans (Gold+GoldPass), Free Fire (Diamonds), Minecraft (MC Coins), Fortnite (V-Bucks), Roblox (Robux) и др.

## Admin Panel
- Секции: dashboard, payments, orders, catalog, analytics, promos
- Агент поддержки входит через `?admin=1` или отдельный роут
