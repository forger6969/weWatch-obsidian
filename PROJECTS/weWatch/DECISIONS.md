---
type: decisions
project: weWatch
updated: 2026-05-23
---

# WeWatch — Architecture Decisions

> Читать при: архитектурном изменении, добавлении сервиса, изменении паттернов.
> Добавлять новое решение сразу после его принятия.

---

## Формат записи

```markdown
### D-XXX | Название решения
**Дата:** YYYY-MM-DD
**Статус:** Принято | Пересмотрено | Отменено
**Контекст:** Почему встала задача
**Решение:** Что именно решили
**Причина:** Почему именно это (не альтернативы)
**Альтернативы:** Что рассматривалось и почему отклонено
**Последствия:** Что это означает для кода
```

---

## D-001 | Микросервисная архитектура

**Дата:** 2026-04-01 (retroaktiv)
**Статус:** Принято

**Контекст:** Нужно масштабируемое приложение с независимыми командами.

**Решение:** 7 отдельных Node.js/Express сервисов вместо монолита.

**Причина:** Разные зоны ответственности (auth, content, watch-party — разная нагрузка и логика). Сайдазим и Эмирхан могут работать независимо.

**Последствия:** Каждый сервис — отдельный порт, отдельный Docker container, отдельная MongoDB database.

---

## D-002 | Socket.io для Watch Party синхронизации

**Дата:** 2026-04-01 (retroaktiv)
**Статус:** Принято — НЕЛЬЗЯ менять event names

**Контекст:** Нужен real-time видео синхрон между пользователями.

**Решение:** Socket.io в services/watch-party с ±2 секунды threshold и buffer compensation.

**Причина:** Проверенная технология, простая интеграция с React Native и React Web. Rave использует WebRTC/WSS — мы адаптировали под Socket.io.

**Последствия:** Event names (video:play, video:pause, video:seek, room:sync и т.д.) зафиксированы — менять нельзя без синхронных изменений на 3 платформах.

---

## D-003 | JWT RS256 + MongoDB refresh tokens

**Дата:** 2026-04-01 (retroaktiv)
**Статус:** Принято

**Контекст:** Auth с коротким access token и долгим refresh.

**Решение:** Access 15min RS256, refresh 30days hashed в MongoDB.

**Причина:** RS256 — асимметричный (публичный ключ для verify), безопаснее HS256. Refresh в MongoDB — можно отозвать любой токен.

**Последствия:** Private key — только в auth service. Public key — в других сервисах для verify.

---

## D-004 | Railway для деплоя

**Дата:** 2026-04-15 (retroaktiv)
**Статус:** Принято

**Контекст:** Нужен простой деплой для стартапа без DevOps.

**Решение:** Railway с Docker containers для всех сервисов.

**Причина:** Простой деплой из git, автоматический HTTPS, environment variables, дешевле AWS/GCP для MVP.

**Последствия:** `railway up` для деплоя. Каждый сервис — отдельный Railway service.

---

## D-005 | Obsidian vault как AI memory layer

**Дата:** 2026-04-30
**Статус:** Принято

**Контекст:** Claude теряет контекст между сессиями, галлюцинирует про архитектуру.

**Решение:** Vault в `~/Documents/weWatch-obsidian` — общий для Saidazim и Emirhan. SessionStart hook читает vault → передаёт контекст Клоду.

**Причина:** Персистентная память между сессиями. Структурированные handoff файлы.

**Последствия:** `.claude/scripts/obsidian-session-start.sh` читает vault при каждом старте. `.claude/scripts/obsidian-session-stop.sh` пишет handoff при завершении.

---

## D-006 | Rave reverse engineering → Socket.io адаптация

**Дата:** 2026-04-20 (retroaktiv)
**Статус:** Принято

**Контекст:** Rave использует проприетарный NTP + Priapus WSS + drift compensation.

**Решение:** Упростили до Socket.io с serverTimestamp и ±2sec threshold. Без P2P.

**Причина:** P2P (WebRTC) слишком сложно для MVP. Socket.io + server as hub достаточно для первых пользователей.

**Последствия:** Все клиенты идут через сервер. При 10+ пользователях в комнате — star topology.

---

## D-007 | Раздельные зоны разработчиков

**Дата:** 2026-04-01 (retroaktiv)
**Статус:** Принято — ЖЁСТКОЕ ПРАВИЛО

**Контекст:** 2 разработчика, разные части codebase.

**Решение:** Saidazim = services/* + apps/admin-ui/. Emirhan = apps/mobile/. shared/* = lock protocol.

**Причина:** Избежать конфликтов, чёткая ответственность.

**Последствия:** Нарушение зоны = потенциальный конфликт + нарушение доверия. Claude не трогает чужую зону.

---

## D-008 | Multi-agent система с Obsidian memory

**Дата:** 2026-05-23
**Статус:** Принято

**Контекст:** Нужна долговременная память, anti-hallucination rules, resume system.

**Решение:** 5-фазный workflow (Research → Summary → Plan → Execute → Memory Update) + новые skills (memory.md, research.md, read-before-write.md, status.md, bugs.md, constraints.md) + обновлённые Obsidian файлы (ARCHITECTURE.md, LAST_SESSION.md, DECISIONS.md, API.md, CONSTRAINTS.md).

**Причина:** Claude должен опираться на реальные файлы проекта, а не придумывать архитектуру.

**Последствия:** Перед любым кодом — research phase. Файл LAST_SESSION.md обновляется в конце каждой сессии. CONSTRAINTS.md содержит жёсткие запреты.

---

*DECISIONS.md | WeWatch | Saidazim | updated: 2026-05-23*
