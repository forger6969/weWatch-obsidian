---
title: Blogy — Система рассылки (outreach)
type: project
client: Георгий Балуев (@baluevgeorge)
created: 2026-06-03
updated: 2026-06-03
tags: [blogy, outreach, telegram, marketing]
---

# 🚀 Blogy — Система рассылки блогерам

> Проект для Георгия Балуева. Привлечение UGC-блогеров в каталог Blogy через холодную рассылку в Telegram.

## Что такое Blogy

- **Платформа** от Bloger.agency (@bloger.agency) — ассоциация блогеров Узбекистана, с 2020 года
- **2500+ блогеров** в базе, работают с Adidas, Samsung, Wildberries, Fix Price, BergHoff
- Работает **внутри Telegram** (есть бот `t.me/BlogyUz_bot`)
- Миссия: «Мы делаем рекламу у блогеров доступнее и проще»
- Суть для блогера: рекламодатели сами находят его в каталоге и пишут напрямую — без поиска заказов
- Сайт: bloger.agency | Каталог: bloger.agency/blogy

## Архитектура системы

```
1. ПАРСИНГ групп → blogy_parser.py
   собирает username, имя, активность, bio
        ↓
2. ШАГ 1 рассылка → blogy_sender.py run
   2 коротких сообщения БЕЗ ссылки, заканчивается "Интересно?"
        ↓
3. ЛИСТЕНЕР → blogy_listener.py (фоном)
   • положительный ответ → сразу ссылка на форму → статус link_sent
   • негатив (нет/спам)  → статус declined
        ↓
4. ДОГОН → blogy_sender.py followup
   не ответившим через 24ч → напоминание
        ↓
5. ФОРМА → blogy-form.vercel.app?uid=BLG-XXXX
   блогер заполняет → данные в Google Sheets → статус filled
```

## Файлы

```
~/.claude/scripts/
  blogy_parser.py     — парсер участников TG групп
  blogy_sender.py     — двухшаговая рассылка (run / followup / stats / preview)
  blogy_listener.py   — ловит ответы, шлёт ссылку
  blogy_data/         — JSON+CSV спарсенных, send_log.json (воронка)
  blogy_form/
    index.html        — анкета блогера (Vercel)
    apps_script.gs    — Google Apps Script backend
```

## Ключевое решение — почему двухшаговый заход

Георгий (голосовое 2026-06-02): длинное сообщение + чужая ссылка = недоверие, низкая конверсия. «Лучше маленькое, бренды сами».

**Решение:** первое сообщение БЕЗ ссылки → вопрос «Интересно?». Ссылка только тем кто ответил.
- Ниже порог → выше % ответов
- Кто ответил = тёплый → клик по ссылке почти 100%
- Telegram не банит за сообщения без ссылок → аккаунт в безопасности

## Тексты (шаг 1, без ссылки)

```
Добрый день, {Имя}! Меня зовут Саидазим, пишу от Blogy (@bloger.agency) 👋

У нас бренды сами находят блогеров для рекламы — без поиска заказов
с вашей стороны. Хотим добавить вас в базу, бесплатно. Интересно?
```

После ответа «да» → ссылка:
```
Отлично! 🙌 Вот короткая анкета — соцсети, тематика, расценки (5 минут).
После этого рекламодатели увидят вас в каталоге:
👉 Заполнить анкету →
```

## Группы для парсинга

| Группа | ~Участников | Тип |
|--------|-------------|-----|
| @photovideokontent | 11 775 | фото/видео/UGC (нужен bio-фильтр) |
| @contentzavo | 291 | UGC-креаторы |
| @bartermicrobloger | 286 | микроблогеры (бартер) |
| @blogix_support_bloggers | 82 | блогеры конкурента Blogix |
| @blogix_support | 54 | рекламодатели Blogix |

## Форма — поля

Личные: имя, телефон (маска +998 XX XXX XX XX), город, язык
Соцсети: Instagram, TikTok, YouTube, Telegram (хотя бы одна)
Контент: тематика, аудитория, формат, UGC да/нет
Расценки: сторис / Reels / фото / UGC (формат "150 000 сум")
Real-time валидация + зелёная рамка при правильном заполнении

## Google Sheets

- ID: `1qDGGr5spXq_86CsilK1djjWLqERbUdrpGaaJMcc5cgU`
- Лист: «Блогеры», название: «Blogy — База блогеров»
- Apps Script ID: `1V-tCi3U1FVIEsIM7LPY30imZ2PqzjyEQsxnNAUgfu8AyPpURJ_8U3FUE`
- Web App URL (v7): `AKfycbx-q1zoST_YDcv7T3MA17lXBHjLuh530FWsfbB35ZjreSq--EZzIVzI5UpuK2cgk21T`
- Читаемые заголовки на русском + цветовая кодировка по статусу + автофильтр
- Деплой через clasp API (токен в `~/.clasprc.json`, refresh при 401)

## Антибан

- 45–90 сек между людьми, макс 30/день (первые дни 15-20 — прогрев)
- 3+ варианта текста (рандом)
- Без ссылок в первом контакте

## ⚠️ Блокеры

- **Аккаунт Диора** — нужен для рассылки. Сейчас в скриптах сессия Саидазима (`wewatch_session`). Диор дал доступ (2FA код 46723), но НЕ авторизован в Telethon — нужен номер телефона → SMS.
- Telethon: 2 процесса не могут на одной сессии одновременно (sender + listener). Решение: единый `blogy_bot.py` ИЛИ запускать по очереди.

## Возможные улучшения (обсуждали)

- Редирект `bloger.agency/join` → форма (официальный домен = доверие)
- Вести через `t.me/BlogyUz_bot` вместо vercel-ссылки
- OG-карточка в форме (красивое превью ссылки в Telegram)
- bio-фильтр в парсере (отсеять не-блогеров в больших группах)

## Голосовые из Telegram

Whisper установлен (`openai-whisper` + ffmpeg). Читаю голосовые:
```python
import whisper
model = whisper.load_model('base')
result = model.transcribe('/tmp/voice.ogg', language='ru')
```

## Связано

[[_index|Clients Hub]] | [[Georgiy-Baluev|Georgiy Baluev]]
[[../../ZONES/Telegram/_context|Telegram Zone]]
[[../../AI_CONTEXT/agents-hub|Agents Hub]]
[[../../WeWatch-Hub|WeWatch Hub]]
