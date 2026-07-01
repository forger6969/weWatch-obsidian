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

## Deploy (Render) — ВАЖНО (2026-07-01)
- `render.yaml` в репо УСТАРЕЛ (описывает старый Python `uvicorn backend.main`). НЕ используется.
- Реальные сервисы заведены в дашборде Render, autoDeploy on commit → main:
  - **doonya-shop-api** (web_service, `rootDir: ./backend-node`) → https://doonya-shop-api.onrender.com | health: `/health` → 200
  - **doonya-shop-frontend** (static, `cd frontend && build`) → doonya-shop-frontend.onrender.com
  - **doonya-landing** (static, `cd landing && build`)
- Деплой = `git push origin main`. Проверка: `render deploys list srv-d8re6rn7f7vs73dv8660 -o json --confirm`
- Backend Node: Express + Mongoose + Telegraf. `strict:true` схемы → поля вне схемы молча теряются при updateOne (был баг с email/avatar).
- Ник при регистрации: FE модал `needsUsernameSetup` (App.tsx) + `POST /username` (лочится). `getOrCreateUser` теперь НЕ сеет TG-@username → окошко у всех.
