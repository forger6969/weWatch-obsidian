---
project: weWatch
type: legal
updated: 2026-05-11
---

# ⚖️ Play Store Compliance — weWatch

Все проблемы и решения, выявленные перед отправкой в Play Store.
Дата аудита: 2026-05-11

---

## 🔴 КРИТИЧЕСКИЕ — Play Store отклонит приложение

### 1. COOKIE_COLLECTION_JS — Spyware
- **Проблема:** JS-скрипт инжектился в WebView и собирал `document.cookie` со сторонних сайтов. Play Store автоматический сканер классифицирует это как шпионское ПО.
- **Статус:** ✅ Исправлено (T-E120)
- **Решение:** Скрипт удалён из `webViewScripts.ts` и `useMediaDetection.ts`. Сбор cookies перенесён на server-side (Playwright → Redis).

### 2. YouTube yt-dlp — нарушение ToS Google
- **Проблема:** yt-dlp загружал видео с YouTube напрямую. Google владеет и YouTube (ToS нарушение) и Play Store (могут забанить приложение) — двойной риск.
- **Статус:** ✅ Исправлено (T-S091)
- **Решение:** YouTube переведён на `extractionMethod: 'embed-api'`. yt-dlp для YouTube убран полностью. Embed через iframe Player API не нарушает ToS.

### 3. Устаревшие Android permissions
- **Проблема:** `READ_EXTERNAL_STORAGE` — deprecated на API 33+. `RECORD_AUDIO` и `RECEIVE_BOOT_COMPLETED` — не используются в приложении, Play Store помечает как избыточные.
- **Статус:** ✅ Исправлено (T-E123)
- **Решение:** `app.json` обновлён — `READ_EXTERNAL_STORAGE` → `READ_MEDIA_IMAGES`, `RECORD_AUDIO` и `RECEIVE_BOOT_COMPLETED` удалены.

### 4. Privacy Policy URL — обязателен для Play Console
- **Проблема:** Без ссылки на Privacy Policy Play Console не позволяет опубликовать приложение.
- **Статус:** ❌ Не сделано (T-S094)
- **Решение:** Нужно создать страницы `wewatch.app/privacy` и `wewatch.app/terms`, добавить URL в Play Console.

### 5. ToS — нет явного согласия
- **Проблема:** Play Store требует checkbox-согласие с ToS при регистрации, не просто текст "нажимая вы соглашаетесь".
- **Статус:** ✅ Исправлено (T-E124)
- **Решение:** В `RegisterScreen.tsx` добавлен checkbox, кнопка регистрации заблокирована пока не отмечен. Ссылки на `wewatch.app/terms` и `wewatch.app/privacy`.

---

## 🟡 СРЕДНИЕ — могут вызвать проблемы при ревью

### 6. Сбор cookies через мобильный WebView
- **Проблема:** Приложение собирало cookies пользователя с внешних сайтов через JS injection — нарушение политики данных.
- **Статус:** ✅ Исправлено (T-S092)
- **Решение:** Server-side cookie jar. Playwright собирает cookies при извлечении видео, сохраняет в Redis (`cookie:{domain}`, TTL 24h). yt-dlp читает через `--add-header Cookie:`. Мобильное приложение cookies не трогает.

### 7. Удаление аккаунта — нет каскадного удаления данных
- **Проблема:** Play Store требует возможность полного удаления данных пользователя. Раньше удалялся только User + Friendship — данные в других сервисах оставались.
- **Статус:** ✅ Исправлено (T-S093)
- **Решение:** `cascadeDeleteUser()` через `Promise.allSettled` — удаляет данные во всех микросервисах (auth, notification, battle, content, admin). Один упавший сервис не блокирует остальные.

### 8. Контент для взрослых в WebView
- **Проблема:** WebView открывал любые URL без фильтрации — включая сайты с контентом 18+. Play Store блокирует приложения с доступом к взрослому контенту без возрастной маркировки.
- **Статус:** ✅ Исправлено (T-E111 + T-E117)
- **Решение:** `useDynamicBlockedDomains` hook — динамический список заблокированных доменов из backend + SecureStore cache 24h + AppState refresh. `isDomainBlocked()` проверяет и статический список и динамический.

### 9. DMCA / Copyright страница
- **Проблема:** Нет публичного контакта для DMCA запросов — требование законодательства и Play Store политики.
- **Статус:** ❌ Не сделано (T-S094)
- **Решение:** Нужна страница `wewatch.app/copyright` с email `copyright@wewatch.app` и процессом подачи DMCA.

---

## 🟢 НИЗКИЕ — информация / принятые решения

### 10. HLS proxy — Play Store не видит backend
- **Статус:** ✅ Оставлено как есть
- **Обоснование:** HLS стриминг идёт через backend proxy, защищён `verifyToken`. Play Store видит только мобильный клиент — backend запросы не проверяются при ревью.

### 11. Rutube / VK Video / kinogo.cc — оставлены
- **Статус:** ✅ Оставлены (yt-dlp на сервере)
- **Обоснование:** CIS юрисдикция, нет связи с Play Store. Server-side scraping Play Store не запрещает — он не видит backend. Ответственность через ToS пользователя.

### 12. Google Video поиск — убран
- **Проблема:** Scraping поисковых результатов Google — Google владеет Play Store, двойной риск (ToS нарушение + бан).
- **Статус:** ✅ Не реализован
- **Решение:** Альтернатива — Rutube API + VK API + Yandex Video (CIS платформы, нет связи с Play Store).

---

## 📋 Pending (что ещё нужно сделать)

| # | Задача | Таск | Приоритет |
|---|--------|------|-----------|
| 1 | Privacy Policy страница (`wewatch.app/privacy`) | T-S094 | P2 |
| 2 | Terms of Service страница (`wewatch.app/terms`) | T-S094 | P2 |
| 3 | DMCA/Copyright страница (`wewatch.app/copyright`) | T-S094 | P2 |
| 4 | Добавить URL в Play Console | T-S094 | P2 |

---

## 📌 Ключевые решения по авторскому праву

- **Юрисдикция:** Узбекистан
- **DMCA контакт:** `copyright@wewatch.app`
- **ToS ответственность:** пользователь соглашается что несёт ответственность за контент
- **YouTube:** только embed, никакого прямого скачивания
- **CIS платформы:** Rutube/VK/kinogo — низкий риск, оставлены
