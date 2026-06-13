---
type: hub
domain: agents
tags: [hub, agents, claude, ai, automation]
updated: 2026-06-13
---

# 🤖 Claude Agents — Hub

> Карта всех агентов для WeWatch проекта и клиентов

---

## Главный агент

### [[../PROJECTS/weWatch/00-weWatch-Overview|WeWatch Project Agent]]
Файл: `.claude/agents/wewatch-agent.md`
Точка входа для ЛЮБОЙ задачи WeWatch. Знает всю архитектуру, диспатчит зональным агентам.

---

## Зональные агенты (по сервисам)

| Агент | Файл | Зона |
|-------|------|------|
| Auth | `.claude/agents/auth-agent.md` | services/auth/ |
| Content | `.claude/agents/content-agent.md` | services/content/ |
| WatchParty | `.claude/agents/watchparty-agent.md` | services/watch-party/ |
| User+Battle+Notif | `.claude/agents/user-battle-notification-agent.md` | services/user,battle,notification/ |
| Admin | `.claude/agents/admin-agent.md` | services/admin/ + admin-ui/ |
| Mobile | `.claude/agents/mobile-agent.md` | apps/mobile/ |
| Web | `.claude/agents/web-agent.md` | apps/web/ |

---

## Аналитические агенты (NEW 2026-06-13)

| Агент | Файл | Когда использовать |
|-------|------|-------------------|
| **Architect** | `.claude/agents/architect-agent.md` | Перед серьёзным изменением архитектуры |
| **PM** | `.claude/agents/pm-agent.md` | Перед реализацией новой фичи |
| **Competitor Research** | `.claude/agents/competitor-agent.md` | Анализ конкурентов/рынка |
| **Security** | `.claude/agents/security-agent.md` | Security review перед мержем |
| **Code Review** | `.claude/agents/code-review-agent.md` | Качество кода (дополняет critic-agent) |
| **Knowledge Curator** | `.claude/agents/knowledge-curator-agent.md` | Порядок в Obsidian/документации |

---

## Инфраструктурные агенты

| Агент | Файл | Зона |
|-------|------|------|
| DevOps | `.claude/agents/devops-agent.md` | CI/CD, EAS, Railway |
| Marketing | `.claude/agents/marketing-agent.md` | Play Store, Instagram, ASO |
| Telegram | `.claude/agents/telegram-agent.md` | bot, tg-notify, outreach |
| QA | `.claude/agents/qa-agent.md` | read-only валидация |
| Shared | `.claude/agents/shared-agent.md` | shared/* (lock protocol) |

---

## Клиентские агенты

| Клиент | Файл | Проект |
|--------|------|--------|
| Blogy (Георгий) | `.claude/agents/blogy-agent.md` | [[../PROJECTS/clients/Blogy-Outreach-System]] |

---

## Multi-Agent Playbooks

| Playbook | Файл | Задачи |
|----------|------|--------|
| Sprint 11 Migration | `.claude/agents/multi-sprint11-migration.md` | T-S101 + T-S102 параллельно |
| Play Store Launch | `.claude/agents/multi-playstore-launch.md` | T-E124 + T-S094 параллельно |

---

## Диспетчер

`.claude/agents/orchestrator.md` — таблица "файл → агент" + dispatch templates

---

## Связанные зоны

[[../ZONES/AI-Agents/_context|AI-Agents Zone]]
[[../ZONES/WeWatch-Backend/_context|Backend Zone]]
[[../ZONES/WeWatch-Mobile/_context|Mobile Zone]]
[[../ZONES/Telegram/_context|Telegram Zone]]
