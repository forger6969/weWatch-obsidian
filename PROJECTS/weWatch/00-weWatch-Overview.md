---
type: hub
project: weWatch
tags: [hub, weWatch, backend]
updated: 2026-05-01 06:35
---

# 🎬 weWatch — Overview

> Социальный онлайн-кинотеатр — функциональный клон Rave (rave.io).
> Смотреть фильмы с друзьями, синхронизация в реальном времени.

---

## 👥 Команда
- [[people/Saidazim]] — Backend + Admin UI
- [[people/Emirhan]] — Mobile (React Native)

---

## 🏗 Сервисы (Backend)
- [[services/auth]] — JWT, Google OAuth, Telegram Auth (port 3001)
- [[services/user]] — Профили, друзья, рейтинги (port 3002)
- [[services/content]] — Фильмы, поиск, видео (port 3003)
- [[services/watch-party]] — Синхронный просмотр, Socket.io (port 3004)
- [[services/battle]] — Gamification, 1v1 (port 3005)
- [[services/notification]] — FCM, in-app, email (port 3007)
- [[services/admin]] — Панель администратора (port 3008)

## 📱 Клиенты
- [[services/mobile]] — React Native + Expo
- [[services/admin-ui]] — React + Vite

---

## 🔧 Инфраструктура
- [[concepts/MongoDB]] — Основная БД
- [[concepts/Redis]] — Кэш + очереди
- [[concepts/Socket.io]] — Real-time синхронизация
- [[concepts/Elasticsearch]] — Поиск контента
- [[concepts/FCM]] — Push уведомления
- [[concepts/JWT]] — Авторизация
- [[concepts/Railway]] — Деплой

---

## 📐 Архитектура
- [[architecture/project-guidelines]] — CLAUDE.md правила (зоны, git, задачи)
- [[architecture/backend-guidelines]] — Backend паттерны (Node.js, Express, MongoDB)
- [[architecture/mobile-guidelines]] — Mobile паттерны (Expo, Zustand, Navigation)

---

## 📚 Документация
- [[docs/transformation-plan]] — CineSync → Rave план трансформации
- [[docs/deploy-railway]] — Railway deployment guide
- [[docs/mobile-setup]] — Mobile setup (Expo SDK 54)
- [[docs/web-design-guide]] — Design System (цвета, шрифты)
- [[docs/debug-log]] — Хронология багов и фиксов

---

## 🔬 Анализ
- [[analysis/rave-reverse-engineering]] — Rave v1.17.12 reverse engineering (видео, sync)

---

## 📋 Задачи
- [[../../TASKS/active]] — Активные задачи (из `docs/Tasks.md`)
- [[../../TASKS/done]] — Завершённые задачи (из `docs/Done.md`)
- [[_bugs]] — Открытые баги
- [[_ideas]] — Идеи и предложения

---

## 🏢 Компания
- [[../../tezCode/00-tezCode-Overview]] — tezCode команда

---

## 🔑 Ключевые решения
- [[decisions/2026-04-30-obsidian-vault-setup-complete]]
