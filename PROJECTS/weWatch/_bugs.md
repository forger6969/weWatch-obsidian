---
project: weWatch
type: bugs
---

# 🐛 weWatch — Bugs Log

<!-- auto-appended by obsidian-note.sh bug -->

### 🐛 [weWatch] adminClient double /api/v1 — все запросы к admin service падали с 404
> EXPO_PUBLIC_ADMIN_URL уже содержит /api/v1, но client.ts добавлял ещё один. Итог: /api/v1/api/v1/... → 404 на getConversations, sendMessage — support chat полностью не работал. Fix: убрать /api/v1 из createClient вызова.
> Found: 2026-05-09 19:00 | By: Saidazim
