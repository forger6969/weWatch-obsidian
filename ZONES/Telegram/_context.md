---
zone: Telegram
type: context
updated: 2026-06-15
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

<!-- session ended: 2026-05-26 21:03 -->

<!-- session ended: 2026-05-26 21:15 -->

<!-- session ended: 2026-05-26 21:19 -->

<!-- session ended: 2026-05-26 21:25 -->

<!-- session ended: 2026-05-26 21:27 -->

<!-- session ended: 2026-05-26 21:50 -->

<!-- session ended: 2026-05-26 22:00 -->

<!-- session ended: 2026-05-26 22:18 -->

<!-- session ended: 2026-05-26 22:26 -->

<!-- session ended: 2026-05-26 22:31 -->

<!-- session ended: 2026-05-26 22:34 -->

<!-- session ended: 2026-05-26 22:56 -->

<!-- session ended: 2026-05-26 23:06 -->

<!-- session ended: 2026-05-26 23:06 -->

<!-- session ended: 2026-05-26 23:11 -->

<!-- session ended: 2026-05-27 00:16 -->

<!-- session ended: 2026-05-27 01:16 -->

<!-- session ended: 2026-05-27 01:40 -->

<!-- session ended: 2026-05-27 02:01 -->

<!-- session ended: 2026-05-27 02:20 -->

<!-- session ended: 2026-05-27 02:54 -->

<!-- session ended: 2026-05-27 02:59 -->

<!-- session ended: 2026-05-27 03:09 -->

<!-- session ended: 2026-05-27 03:15 -->

<!-- session ended: 2026-05-27 04:21 -->

<!-- session ended: 2026-05-27 04:40 -->

<!-- session ended: 2026-05-27 06:40 -->

<!-- session ended: 2026-05-27 13:52 -->

<!-- session ended: 2026-05-27 22:10 -->

<!-- session ended: 2026-05-27 23:28 -->

<!-- session ended: 2026-05-27 23:58 -->

<!-- session ended: 2026-05-28 15:23 -->

<!-- session ended: 2026-05-28 16:36 -->

<!-- session ended: 2026-05-28 16:48 -->

<!-- session ended: 2026-05-28 16:54 -->

<!-- session ended: 2026-05-28 16:59 -->

<!-- session ended: 2026-05-28 17:20 -->

<!-- session ended: 2026-05-29 20:49 -->

<!-- session ended: 2026-05-31 21:23 -->

<!-- session ended: 2026-05-31 22:39 -->

<!-- session ended: 2026-06-01 14:13 -->

<!-- session ended: 2026-06-01 15:37 -->

<!-- session ended: 2026-06-01 22:24 -->

<!-- session ended: 2026-06-02 12:26 -->

<!-- session ended: 2026-06-02 15:13 -->

<!-- session ended: 2026-06-02 19:39 -->

<!-- session ended: 2026-06-03 15:59 -->

<!-- session ended: 2026-06-03 19:34 -->

<!-- session ended: 2026-06-03 19:41 -->

<!-- session ended: 2026-06-03 22:03 -->

<!-- session ended: 2026-06-04 17:21 -->

<!-- session ended: 2026-06-05 16:21 -->

<!-- session ended: 2026-06-05 19:00 -->

<!-- session ended: 2026-06-05 19:04 -->

<!-- session ended: 2026-06-05 19:34 -->

<!-- session ended: 2026-06-06 16:23 -->

<!-- session ended: 2026-06-06 21:35 -->

<!-- session ended: 2026-06-06 21:41 -->

<!-- session ended: 2026-06-06 21:44 -->

<!-- session ended: 2026-06-08 17:18 -->

<!-- session ended: 2026-06-08 18:29 -->

<!-- session ended: 2026-06-08 18:37 -->

<!-- session ended: 2026-06-08 18:49 -->

<!-- session ended: 2026-06-09 13:59 -->

<!-- session ended: 2026-06-09 14:50 -->

<!-- session ended: 2026-06-09 15:43 -->

<!-- session ended: 2026-06-10 17:09 -->

<!-- session ended: 2026-06-10 17:40 -->

<!-- session ended: 2026-06-10 21:40 -->

<!-- session ended: 2026-06-10 22:04 -->

<!-- session ended: 2026-06-11 14:07 -->

<!-- session ended: 2026-06-11 14:11 -->

<!-- session ended: 2026-06-11 18:27 -->

<!-- session ended: 2026-06-11 18:58 -->

<!-- session ended: 2026-06-12 14:20 -->

<!-- session ended: 2026-06-12 14:21 -->

<!-- session ended: 2026-06-12 15:26 -->

<!-- session ended: 2026-06-12 20:57 -->

<!-- session ended: 2026-06-13 14:58 -->

<!-- session ended: 2026-06-13 15:06 -->

<!-- session ended: 2026-06-13 19:37 -->

<!-- session ended: 2026-06-14 01:34 -->

<!-- session ended: 2026-06-14 15:29 -->

<!-- session ended: 2026-06-14 15:54 -->

<!-- session ended: 2026-06-14 20:12 -->

<!-- session ended: 2026-06-14 22:29 -->

<!-- session ended: 2026-06-14 23:24 -->

<!-- session ended: 2026-06-15 01:20 -->
