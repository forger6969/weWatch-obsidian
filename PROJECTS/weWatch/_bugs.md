---
project: weWatch
type: bugs
---

# 🐛 weWatch — Bugs Log

<!-- auto-appended by obsidian-note.sh bug -->

### 🐛 [weWatch] adminClient double /api/v1 — все запросы к admin service падали с 404
> EXPO_PUBLIC_ADMIN_URL уже содержит /api/v1, но client.ts добавлял ещё один. Итог: /api/v1/api/v1/... → 404 на getConversations, sendMessage — support chat полностью не работал. Fix: убрать /api/v1 из createClient вызова.
> Found: 2026-05-09 19:00 | By: Saidazim

### 🐛 [weWatch] FCM token NULL в release APK — resource shrinking стрипает google-services ресурсы
> Симптом: PUSH DIAG показал permission:granted, token:NULL, БЕЗ строки getToken error. getDevicePushTokenAsync() возвращал пустой data без исключения.

Root cause: app.json android — enableShrinkResourcesInReleaseBuilds=true + enableProguardInReleaseBuilds=true, но в proguard-rules.pro НЕ было правил для Firebase. Resource shrinking удалял google-services string resources (google_app_id, gcm_defaultSenderId и др.), которые Firebase читает через Resources.getIdentifier() без прямой ссылки в коде → Firebase auto-init с пустым sender id → FCM getToken пусто, БЕЗ ошибки.

Fix (2 файла):
1. android/app/src/main/res/raw/keep.xml — tools:keep для 7 google-services string resources (защита от shrinkResources)
2. android/app/proguard-rules.pro — -keep com.google.firebase.** / com.google.android.gms.** / expo.modules.**

Подтверждено через agy (внешний критик): keep-правил кода НЕдостаточно при shrinkResources — нужен именно keep.xml для ресурсов. Это и объясняет отсутствие исключения.
> Found: 2026-06-30 15:19 | By: Saidazim
