---
zone: WeWatch-Mobile
type: context
updated: 2026-06-10
---

# WeWatch-Mobile Zone — Context

## Текущее состояние (2026-06-10)

### Что сделано
- **Push notifications** (2026-06-10): FCM токен через `getDevicePushTokenAsync()`, ravetokenauth
- **APK собран**: `apps/mobile/wewatch-push-notifications.apk` (145MB, Jun 10 22:26)
- **VK/Rutube**: hidden WebView CDN sniffing + ExoPlayer switch
- **WatchParty sync**: NTP + buffer compensation, executeSync работает
- **Branding**: CineSync → WeWatch переименован

### Ключевые файлы
- `src/hooks/usePushNotifications.ts` — только `getDevicePushTokenAsync()`, НЕ ExponentPushToken
- `apps/mobile/google-services.json` — ravetokenauth (project_id: ravetokenauth)
- `apps/mobile/app.json` — version 1.0.1, versionCode 2, googleServicesFile: ./google-services.json
- `apps/mobile/eas.json` — profiles: local (apk debug) | preview (apk) | production (aab)

### CRITICAL: Push notifications
1. `getDevicePushTokenAsync()` → raw FCM token (Android: string)
2. `userApi.updateFcmToken(token)` → cinesync.users.fcmTokens[]
3. Notification service: `sendEachForMulticast()` Firebase Admin SDK ravetokenauth
4. НЕ использовать `getExpoPushTokenAsync` — требует EAS credentials

## Активные задачи
- T-E124 P2: Play Store Feature Graphic (1024×500) + 5 screenshots ❌ Boshlanmagan
- T-E081 P1: Real device smoke test ⚠️ Qisman

## Следующий шаг
Установить APK → `GET /users/internal/admin/all-push-tokens` → должен вернуть токены

## Build команда
```bash
cd apps/mobile
JAVA_HOME=/opt/homebrew/opt/openjdk@17 ANDROID_HOME=~/Library/Android/sdk \
eas build -p android --profile local --local --output ./wewatch.apk
```

## Агент: `.claude/agents/mobile-agent.md`
## Multi-agent: `.claude/agents/multi-playstore-launch.md`

<!-- session ended: 2026-05-27 00:14 -->

<!-- session ended: 2026-05-27 01:14 -->

<!-- session ended: 2026-05-27 23:50 -->

<!-- session ended: 2026-06-02 12:14 -->

<!-- session ended: 2026-06-02 15:59 -->

<!-- session ended: 2026-06-03 19:19 -->

<!-- session ended: 2026-06-03 19:39 -->

<!-- session ended: 2026-06-04 15:12 -->

<!-- session ended: 2026-06-06 14:33 -->

<!-- session ended: 2026-06-06 21:22 -->

<!-- session ended: 2026-06-08 18:29 -->

<!-- session ended: 2026-06-08 18:37 -->

<!-- session ended: 2026-06-08 21:34 -->

<!-- session ended: 2026-06-09 14:50 -->

<!-- session ended: 2026-06-09 14:52 -->

<!-- session ended: 2026-06-09 15:30 -->

<!-- session ended: 2026-06-10 15:21 -->
