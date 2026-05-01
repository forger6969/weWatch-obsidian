---
type: architecture
project: weWatch
title: "Project Guidelines (CLAUDE.md)"
date: 2026-05-01
tags: [architecture, guidelines, claude, workflow]
---

# 🏗 Project Guidelines

**Hub:** [[../00-weWatch-Overview]] | **Источник:** `CLAUDE.md` (v2.1)

---

## Зоны ответственности

| Зона | Путь | Ответственный |
|------|------|--------------|
| Backend | `services/*`, `apps/admin-ui/` | [[../people/Saidazim]] |
| Mobile | `apps/mobile/` | [[../people/Emirhan]] |
| Shared | `shared/*` | Согласование обоих |

---

## Запрещено

```
❌ any type (TypeScript strict)
❌ console.log → Winston Logger (backend)
❌ 400+ строк в файле → разбить
❌ Hardcoded secrets → .env
❌ Трогать зону другого разработчика
❌ shared/* без согласования
❌ Push напрямую в main
```

---

## Task Tracking

### Формат (docs/Tasks.md)
```markdown
### T-S057 | P1 | [BACKEND] | Название

- **Mas'ul:** pending[Saidazim]
- **Beruvchi:** Emirhan
- **Yaratilgan:** 2026-05-01 16:00
- **Holat:** ❌ Boshlanmagan
- **Tavsiya model:** sonnet
```

### Приоритеты
- **P0** — Критично (production down)
- **P1** — Важно (блокирует разработку)
- **P2** — Средний приоритет
- **P3** — Низкий приоритет

---

## Git Flow
```bash
# Branch format:
saidazim/feat-[feature-name]
emirhan/feat-[feature-name]

# Commit format:
feat(auth): add Google OAuth callback
fix(watch-party): correct sync timestamp drift
refactor(content): split search into elasticsearch adapter
```

---

## Telegram уведомления
```bash
# Любое изменение задач:
.claude/scripts/tg-notify.sh <action> <task_id> <meta> <title> [executor]
```
- `T-S***` → только Saidazim
- `T-E***` → только Emirhan
- `T-C***` → оба

---

## Связанные документы
- [[backend-guidelines]] — детали backend правил
- [[mobile-guidelines]] — детали mobile правил
- [[../docs/deploy-railway]] — деплой
