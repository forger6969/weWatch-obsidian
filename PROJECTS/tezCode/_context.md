---
project: tezCode
type: context
updated: 2026-05-03
source: telegram-full-history (15542 messages, 2026-02-24 → now)
---

# 🏢 tezCode — Полный контекст

**Тип:** AI-first стартап-студия. Все проекты собственные, заказных нет.  
**Локация:** Ташкент, Узбекистан (UTC+5)  
**Инфра:** Railway (хостинг, переходят на Sevalla+Cloudflare), GitHub AI-automatization орг.  
**AI:** Claude Code (каждый с Pro $20/мес), собственный `notfication_tezcode_bot` (Telethon)

---

## 👥 Команда (14 человек, RACI от 2026-04-28)

| Человек | Telegram | Проект | Роль |
|---------|----------|--------|------|
| **Bekzod** | @webdevelopertk | AI-office | CEO + основатель |
| **Saidazim** | Foreger | Rave | Backend dev |
| **Emirhan** | @Emirhan7788 | Rave | Mobile TL |
| **Abdulaziz Yormatov** | @mr_abdulaziz_yormatov | RAOS | COO + TL |
| **Ibrat** | — | RAOS / POS-cosmetics | Dev |
| **Azim** | @Azim090 | savdo-builder | Savdo TL |
| **Polat** | ogerz3 | savdo-builder | Dev |
| **Diyor** | @diyor_011 | HamshiraGo | TL |
| **Jafar** | WizardJafar | HamshiraGo | Dev |
| **Abubakir** | @abubakirilhomov | HamshiraGo | Dev |
| **Behruz** | @behruz_460 | Zzone | TL |
| **Sardor** | — | VENTRA | TL |
| **Ziyoda** | — | Work-Controll | TL |
| **Rayy / Firdavs** | @RAYYQF | Marketing | TL |

---

## 📦 Проекты — детально

### 🏆 HamshiraGo (флагман)
**Что:** Медицинская платформа — медсестёр/врачей к пациентам и клиникам on-demand  
**Домен:** hamshirago.uz  
**Статус:** Production Beta — самый зрелый проект (661 commit, 181 за последние 30 дней)  
**Стек:** NestJS monorepo + 4 микросервиса (api, clinic, voice-agent, payments) + PostgreSQL + Redis  
**Клиенты:** Mobile Expo (пациент), Medic Expo (врач), Web Next.js 16, Web-medic, Admin Vite  
**Бизнес:** Медсёстры получают доп. заказы, клиники — новый канал. Партнёрство с клиниками.  
**Возможности:** Гранты World Bank MUNIS $50M, IT Park льготы  
**Конкуренты:** Practo, Halodoc (у них есть аптека и страховка — у HamshiraGo пока нет)  
**Команда:** Diyor (TL) + Jafar + Abubakir — Claude $140/мес

---

### 🤖 AI-office (OpenClaw)
**Что:** Multi-agent AI платформа — CEO-ассистент для бизнеса  
**Домен:** ai-office.tezcode.uz | openclaw-web-production-73ae.up.railway.app  
**Статус:** Alpha/Beta Production — Bekzod строит один  
**Фичи:** Telegram userbot (пишет от твоего имени), Lead Manager/Qualifier/Closer, CRM, голосовой клон UZ/RU  
**6 MOAT над конкурентами:** Telegram native, Voice clone UZ/RU, Payme/Click/Humo+soliq.uz, Исламский режим (намаз/Рамадан), Multi-agent уже работает, Цена $49/мес (CIS рынок)  
**Конкуренты:** Motion, Reclaim, Clay, Lindy — но все только на английском  
**Пилот:** Akmal (первый реальный пользователь)  
**Команда:** Только Bekzod — Claude $100/мес

---

### 🎬 Rave (weWatch / CineSync)
**Что:** Социальный онлайн-кинотеатр — смотреть видео вместе с друзьями  
**Статус:** MVP в разработке  
**Стек:** Node.js + Express + MongoDB + Redis + Socket.io (backend), React Native + Expo (mobile)  
**Code review от Bekzod (2026-04-21): B-** — sync протокол хорошо спроектирован, но:
- `@socket.io/redis-adapter` отсутствует → горизонтальное масштабирование сломано
- Несколько незаинтегрированных функций (needsResync не вызывается)  
**Bekzod делал reverse-engineering оригинального Rave** (NTP + Priapus WSS + drift compensation)  
**Команда:** Emir (TL) + Foreger/Saidazim — Claude $40/мес  
**Заметка:** Emirhan как TL почти не коммитит, Saidazim делает основную работу

---

### 📊 VENTRA (sellerTrend)
**Что:** SaaS аналитика продаж для продавцов на Uzum.uz и Wildberries  
**Статус:** Production, есть баги  
**Стек:** NestJS + PostgreSQL + Bright Data proxy (парсинг Uzum)  
**Ключевая метрика:** `weekly_bought` — алгоритм подсчёта недельных продаж (история 6 фаз рефакторинга)  
**Баги (2026-04-21):** Bright Data proxy упал → 100% fail на light-snapshot; данные за Apr 19 потеряны  
**Команда:** Sardor (TL) — Claude $20/мес

---

### 🏪 RAOS (POS-cosmetics)
**Что:** POS кассовая система для розничных магазинов (сначала — косметика)  
**Статус:** В активной разработке, Super Admin уже готов  
**Стек:** Next.js монорепо + Prisma (85 моделей, 26 миграций) + PostgreSQL  
**Фичи:** Кассир (смены, наличные/карта/Click/Payme, split payment, 80мм ESC/POS принтер, возврат, сканер), Super Admin, COO аналитика  
**Реальные данные:** 118 заказов, ~99 млн сум оборот на тестовом клиенте  
**Баги:** Дублирующаяся миграция (KRITIK — deploy на новой DB сломается), CI/CD не работал 13+ дней  
**Команда:** Yormatov (COO/TL) + Ibrat — Claude $120/мес

---

### 🛒 savdo-builder (ShopHub)
**Что:** Telegram Mini App маркетплейс — продавец создаёт магазин в Telegram  
**Статус:** MVP, монетизация отключена, PMF ещё не доказан  
**Интеграция:** OmniChannel стек с POS (RAOS) + sellerTrend: единый инвентарь offline+online  
**Команда:** Azim (TL) + Polat — Claude $120/мес

---

### ⏱ Work-Controll
**Что:** Контроль рабочего времени  
**Статус:** В разработке  
**Команда:** Ziyoda (одна) — Claude $20/мес

---

### 📦 Zzone
**Что:** Неизвестно (мало упоминаний в чате)  
**Команда:** Behruz — Claude $20/мес

---

### 📈 ai-trade-agent
**Что:** AI трейдинг агент  
**Статус:** Только начат (1 коммит)  
**Команда:** ABUQORIgggg / исроилов абдуллох

---

## 💡 Стратегия Bekzod'а

**tezCode.ai разделение:**
- **Systems** = продаётся, есть клиенты, recurring revenue → HamshiraGo, POS, VENTRA
- **Labs** = MVP, тестируется, PMF не доказан → savdo-builder, Rave, Zzone, ai-trade

**Интеграционное видение (2026-04-25):**
1. OmniChannel: POS ⨉ savdo-builder ⨉ sellerTrend — единый инвентарь, 3 дохода
2. Unified SSO для всех продуктов
3. Embedded FinTech/Lending
4. Shared `packages/ui` + `packages/types` для всех Next.js приложений

**Инфра переход:** Railway (200-300ms из Ташкента) → Sevalla+Cloudflare (80-100ms, $15-25/мес)

---

## Важные решения команды
<!-- auto-appended -->
