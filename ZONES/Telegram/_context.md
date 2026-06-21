---
zone: Telegram
type: context
updated: 2026-06-21
---

# Telegram Zone — Context

## Текущее состояние (2026-06-10)

### @notification_weWatch_bot
- Бот для уведомлений команды WeWatch
- Saidazim chat_id: **6299152655**
- Используется для: task notifications (tg-notify.sh), статусы задач

### tg-notify.sh
```bash
# Команды:
.claude/scripts/tg-notify.sh <action> <task_id> <meta> <title> [executor] [details]
# actions: new | claim | done | update | blocked
# T-S*** → Saidazim | T-E*** → Emirhan | T-C*** → оба
```

### MCP Tools (plugin:telegram:telegram)
Доступны через ToolSearch: reply, edit_message, react, download_attachment
Входящие сообщения: теги `<channel source="telegram" chat_id="...">`
ВАЖНО: Claude видит только новые сообщения, не историю

### Team Telegram
- TEZCODE Team Management: ID 2640882371
- Bekzod (CEO) — code review, публикует commit рейтинг каждые 48ч
- Saidazim в топ-2 по коммитам (20 за 48ч)

### Blogy Outreach (scripts/blogy_*.py)
Двухшаговая рассылка блогерам для @baluevgeorge:
1. blogy_send_initial.py — первый контакт
2. blogy_send_followup.py — фолловап +48ч
Блокер: аккаунт Диора, Whisper для голосовых

## ПРАВИЛО
При ЛЮБОМ изменении задач в docs/Tasks.md → обязательно tg-notify.sh.
Нельзя молчать при claim/done/blocked.

## Связано

[[../WeWatch-Backend/_context|⚙️ Backend Zone]] | [[../AI-Agents/_context|🤖 AI-Agents Zone]]
[[../../PROJECTS/clients/Georgiy-Baluev|Клиент: Georgiy Baluev]]
[[../../PROJECTS/clients/Blogy-Outreach-System|Blogy Outreach System]]
[[../../AI_CONTEXT/agents-hub|Agents Hub]]