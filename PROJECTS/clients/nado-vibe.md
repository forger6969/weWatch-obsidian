# NADO VIBE — E-commerce System

**Клиент:** @nado_vibe (MEN'S WEAR Ташкент)
**Статус:** В разработке (продаём/сдаём в аренду)
**Локальный путь:** `/Users/saidazim/Desktop/nado-vibe/`
**GitHub:** https://github.com/forger6969/nado-vibe

---

## Инфраструктура

| Сервис | URL | Технология |
|--------|-----|-----------|
| Лендинг | https://nado-vibe-landing.vercel.app | React + Vite + Tailwind + Framer Motion |
| TMA (каталог) | https://nado-vibe-tma.vercel.app | React + Vite + TypeScript |
| Bot API | https://nado-vibe-bot.onrender.com | Python aiogram3 + aiohttp |
| БД | Supabase (PostgreSQL) | REST API + RLS |
| Фото | Cloudinary | cloud: `dr0z8c9ag`, preset: `nado_vibe` |

---

## Стек

- **Frontend:** React + Vite + TypeScript + Tailwind CSS v3 + Framer Motion
- **Fonts:** Unbounded (display) / Inter (body) / Space Mono (mono)
- **Bot:** Python 3.11 + aiogram3 + aiohttp HTTP server (PORT=10000)
- **DB:** Supabase PostgreSQL с RLS политиками
- **Фото продуктов:** Cloudinary unsigned upload (НЕ Supabase Storage — сломан)
- **Деплой:** Vercel (лендинг + TMA), Render (бот, автодеплой с GitHub)

---

## Архитектура

```
Telegram Bot → /start → открывает TMA (nado-vibe-tma.vercel.app)
TMA → Supabase напрямую (products, orders, reviews)
TMA → Bot API /notify_client (уведомления клиенту)
TMA → Bot API /notify_order (уведомления админу)
Лендинг → Bot API /api/products (кэш 5 мин, защита Supabase от нагрузки)
```

---

## Таблицы Supabase

### products
- id, name, category, price, sizes[], description, image_url, stock, active, created_at

### orders
- id, cart_id (UUID — группировка корзины), product_id, product_name, size
- buyer_tg_id, buyer_name, buyer_username, phone, address
- status: new|processing|shipped|delivered|cancelled
- courier_name, courier_phone (заполняется при отправке)
- confirmed (bool, дефолт false — клиент подтверждает получение)
- created_at

### reviews
- id, order_id, buyer_tg_id, rating (1-5), text, photo_url, created_at

### admins
- tg_id (bigint) — список tg_id администраторов

---

## Флоу заказа

```
1. Клиент → каталог → в корзину (несколько товаров)
2. Клиент → оформить → вводит телефон + адрес
   → генерируется cart_id (UUID), все товары привязаны к нему
   → createOrders() → Bot /notify_order (одно уведомление на корзину)
3. Админ → видит заказ как КОРЗИНУ (все товары вместе, сгруппировано по cart_id)
4. Админ → меняет статус на "Отправлен" → CourierForm (имя + телефон курьера)
   → shipOrder() на все товары корзины + notifyClient() в TG
5. Клиент получает уведомление с данными курьера
6. Статус "Доставлен" → клиент получает уведомление
7. Клиент → TMA → "Подтвердить получение + оставить отзыв"
   → ReviewForm (звёзды + текст + фото Cloudinary)
   → createReview() + confirmDelivery()
```

---

## Ключевые env vars (TMA — Vercel)

- `VITE_SUPABASE_URL` — Supabase project URL
- `VITE_SUPABASE_ANON_KEY` — Supabase anon key
- `VITE_BOT_NOTIFY_URL` — https://nado-vibe-bot.onrender.com/notify_order
- `VITE_NOTIFY_SECRET` — секрет для бота
- `VITE_TMA_URL` — https://nado-vibe-tma.vercel.app (кнопка в TG уведомлениях)

## Ключевые env vars (Bot — Render)

- `BOT_TOKEN` — Telegram bot token
- `SUPABASE_URL`, `SUPABASE_SERVICE_KEY` — для прямого доступа к БД
- `NOTIFY_SECRET` — совпадает с TMA

---

## Известные решения

- **Supabase Storage сломан** → используем Cloudinary (cloud `dr0z8c9ag`, preset `nado_vibe`)
- **Python 3.14 Render** → файл `bot/.python-version = 3.11.0` (pydantic-core не собирается на 3.14)
- **cart_id** — UUID генерируется на клиенте при чекауте, привязывается ко всем товарам

---

## Миграции (в порядке)

1. `20260613100000_initial.sql` — начальные таблицы
2. `20260613120000_add_stock_and_fix_rls.sql` — stock + RLS для CRUD
3. `20260613140000_courier_reviews.sql` — courier_name/phone/confirmed + таблица reviews
4. `20260613150000_add_cart_id.sql` — cart_id в orders

---

*Обновлено: 2026-06-13*
