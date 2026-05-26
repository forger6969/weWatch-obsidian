---
type: decision
project: weWatch
title: "Migration: Единая БД cinesync для всех сервисов"
date: 2026-05-23
executor: Saidazim
---

# 🏛 Migration: Единая БД cinesync для всех сервисов

**Project:** weWatch | **Date:** 2026-05-23 16:42 | **By:** Saidazim

## Decision

## Проблема

Каждый сервис использует свою БД (cinesync_auth, cinesync_user, и т.д.).
При регистрации создаётся 2 записи: auth.users + user.users — дублирование, лишние деньги, сложная синхронизация.

## Решение

Все 6 сервисов → одна БД `cinesync`.
Auth при register создаёт ONE полную запись user (email + passwordHash + rank + fcmTokens + settings).
User service делает getMe по \_id — ту же запись, без authId FK.

## Таски

| ID | Приоритет | Название |
|----|-----------|----------|
| T-S096 | P1 | Аудит — найти все authId references во всех сервисах |
| T-S097 | P1 | Объединённая схема users — merge auth.users + user.users |
| T-S098 | P1 | Auth service — .env → cinesync + register создаёт полный user |
| T-S099 | P1 | User service — .env → cinesync + getMe по _id (без authId) |
| T-S100 | P2 | Остальные 4 сервиса — обновить .env → cinesync |
| T-S101 | P2 | Скрипт миграции данных — перенести auth.users + user.users в cinesync.users |
| T-S102 | P3 | tsc clean + db-architecture.html обновить |

## Зависимости

T-S096 → T-S097 → T-S098 → T-S099 → T-S100 → T-S101 → T-S102

## Статус

Запланировано 2026-05-23. Ещё не начато.

## Rationale

## Consequences
