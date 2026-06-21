---
zone: Blogy
updated: 2026-06-11
---

# Blogy Zone — Контекст

## Что такое Blogy
Платформа от Bloger.agency (@bloger.agency) — маркетплейс инфлюенсеров Узбекистана.
- 2500+ блогеров в базе (Adidas, Samsung, Wildberries, Fix Price, BergHoff)
- Работает внутри Telegram: `t.me/BlogyUz_bot`
- Сайт: bloger.agency | Каталог: bloger.agency/blogy
- Клиент/партнёр: Георгий Балуев (@baluevgeorge)
- Конкуренты: blogix.uz, perfluence.net

## Текущий статус
MVP в разработке. Основное направление — outreach система для привлечения блогеров.
Форма регистрации: blogy-form.vercel.app
Google Sheets база: ID `1qDGGr5spXq_86CsilK1djjWLqERbUdrpGaaJMcc5cgU`

## Скрипты
```
~/.claude/scripts/
  blogy_parser.py     — парсер участников TG групп
  blogy_sender.py     — двухшаговая рассылка (run / followup / stats)
  blogy_listener.py   — ловит ответы, шлёт ссылку на форму
  blogy_data/         — JSON/CSV база блогеров + send_log.json
```

## Блокеры
- Аккаунт Диора нужен для рассылки (нужен номер телефона → SMS авторизация)
- Telethon: нельзя 2 процесса на одной сессии — нужен единый blogy_bot.py

## Связанные файлы
[[outreach]] — подробная архитектура outreach системы
[[../../PROJECTS/clients/Blogy-Outreach-System|Blogy-Outreach-System]] — полный документ