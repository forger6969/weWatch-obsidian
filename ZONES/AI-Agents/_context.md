---
zone: AI-Agents
type: context
updated: 2026-06-10
---

# AI-Agents Zone — Context

## Текущее состояние (2026-06-10)

### Агентная система WeWatch (.claude/agents/)
| Файл | Зона | Статус |
|------|------|--------|
| auth-agent.md | services/auth/ | ✅ |
| content-agent.md | services/content/ | ✅ |
| watchparty-agent.md | services/watch-party/ | ✅ |
| user-battle-notification-agent.md | services/user,battle,notification/ | ✅ |
| admin-agent.md | services/admin/ + admin-ui/ | ✅ |
| mobile-agent.md | apps/mobile/ | ✅ |
| web-agent.md | apps/web/ | ✅ |
| qa-agent.md | read-only QA | ✅ |
| shared-agent.md | shared/* | ✅ |
| **devops-agent.md** | CI/CD, EAS, Railway | ✅ NEW |
| **marketing-agent.md** | marketing/, Play Store | ✅ NEW |
| **telegram-agent.md** | tg bots, tg-notify.sh | ✅ NEW |
| orchestrator.md | dispatch hub | ✅ updated |

### Multi-Agent Playbooks
| Файл | Задачи | Когда использовать |
|------|--------|-------------------|
| multi-sprint11-migration.md | T-S101 + T-S102 | Sprint 11 migration завершение |
| multi-playstore-launch.md | T-E124 + T-S094 | Play Store submission prep |

### Режимы
- **Mode A (Single)**: < 30 мин, 1-2 файла → Agent без isolation
- **Mode B (Multi)**: > 60 мин, 5+ файлов → Multi-Agent + worktrees

### Параллельность
```
МОЖНО:  auth + mobile | content + admin-ui | user + web
НЕЛЬЗЯ: shared + любой (lock) | T-C*** (backend сначала)
```

### Dispatch pattern
```javascript
// Читать агент файл → вставить в prompt
const agentContent = Read('.claude/agents/auth-agent.md');
Agent({ subagent_type: "general-purpose", isolation: "worktree",
  prompt: `${agentContent}\n\nTASK SPEC:\n...` });
```

## Obsidian zone-auto-detect.sh
При словах "agent/swarm/automation/multi-agent/subagent/skill" → загружает эту зону
Скрипт: `.claude/scripts/zone-auto-detect.sh`

## Следующие улучшения
- Добавить Instagram-specific agent (Remotion video генерация)
- CI/CD agent для автоматических деплоев на Railway
