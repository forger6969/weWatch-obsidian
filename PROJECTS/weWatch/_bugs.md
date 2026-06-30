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

### 🐛 [weWatch] Google native login DEVELOPER_ERROR — нет Android OAuth client + debug SHA-1 не зарегистрирован
> Симптом: 'не удалось войти через google' в release APK, нативный @react-native-google-signin путь.

Root cause (НЕ код, конфиг Google Cloud):
- Mobile webClientId (useSocialAuth.ts:13) = 756077214118-top29... (проект A)
- Backend GOOGLE_CLIENT_ID = тот же 756077214118 → mobile и backend СОГЛАСОВАНЫ
- НО в проекте A нет OAuth Android client (package com.wewatch.app + SHA-1), поэтому Play Services не выдаёт idToken → DEVELOPER_ERROR (code 10)
- Backend GOOGLE_ANDROID_CLIENT_ID='dev_android_client_id' — заглушка
- google-services.json в APK из проекта B (151878141751 ravetokenauth, только FCM) — менять НЕ нужно (webClientId явно переопределяет)

APK подписан debug-ключом: SHA-1 5E:8F:16:06:2E:A3:CD:2C:4A:0D:54:78:76:BA:A6:F3:8C:AB:F6:25

Fix (Google Cloud Console, проект 756077214118):
1. Credentials → Create OAuth client ID → Android
2. Package: com.wewatch.app, SHA-1: 5E:8F:16:06:... (debug ключа)
3. (опц.) полученный android client id → backend GOOGLE_ANDROID_CLIENT_ID
Подтверждено через agy: одного Android-клиента в проекте A достаточно, google-services.json трогать не надо (idToken→свой backend).
> Found: 2026-06-30 15:41 | By: Saidazim
