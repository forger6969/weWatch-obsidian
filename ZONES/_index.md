---
type: hub
domain: zones
tags: [hub, zones, context]
updated: 2026-06-10
---

# 🗺️ Zones — Hub

> Каждая зона = платформа или направление. Загружается автоматически при ключевых словах.

---

## WeWatch Зоны

| Зона | Контекст | Ключевые слова |
|------|----------|----------------|
| [[WeWatch-Mobile/_context\|📱 Mobile]] | React Native, Expo, push, APK | "mobile", "react native", "expo" |
| [[WeWatch-Backend/_context\|⚙️ Backend]] | 7 сервисов, cinesync DB, Railway | "backend", "service", "api", "auth" |
| [[WeWatch-Web/_context\|🌐 Web]] | Next.js, landing, branding | "web", "next.js", "landing" |

## Контент Зоны

| Зона | Контекст | Ключевые слова |
|------|----------|----------------|
| [[Instagram/_context\|📸 Instagram]] | Remotion Reels, slides | "instagram", "reel", "slides" |
| [[Telegram/_context\|✈️ Telegram]] | bot, tg-notify, outreach | "telegram", "bot", "tg" |

## AI & Tools Зоны

| Зона | Контекст | Ключевые слова |
|------|----------|----------------|
| [[AI-Agents/_context\|🤖 AI-Agents]] | агентная система, orchestrator | "agent", "swarm", "automation" |
| MCPs/ | MCP инструменты | "mcp", "tool" |
| Skills/ | навыки Claude | "skill", "скилл" |
| Plugins/ | плагины | "plugin" |

---

## Как работает автодетект

```bash
# При каждом промпте:
.claude/scripts/zone-auto-detect.sh → определяет зону по ключевым словам
                                    → загружает _context.md нужной зоны
```

---

## Связано

[[../WeWatch-Hub]] — главный Hub проекта
[[../AI_CONTEXT/agents-hub]] — агентная система
[[../PROJECTS/clients/_index]] — клиенты
