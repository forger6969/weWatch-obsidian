---
type: analysis
project: weWatch
title: "Rave App — Reverse Engineering Analysis"
date: 2026-05-01
author: Claude Sonnet 4.6
source: Rave-1.17.12-universal.dmg
tags: [analysis, rave, reverse-engineering, sync, video]
---

# 🔬 Rave App — Полный Технический Анализ

> **Источник:** `docs/RAVE_ANALIZ.md`
> **Метод:** Reverse engineering ASAR archive (Electron app)
> **Версия:** Rave 1.17.12

**Hub:** [[../00-weWatch-Overview]] | **Связан:** [[../services/watch-party]] [[../services/content]]

---

## Стек Rave

| Слой | Технология |
|------|-----------|
| Runtime | Electron (Chromium + Node.js) |
| UI | React + Webpack |
| Sync Protocol | WebSocket ("Priapus" — кастомный сервер) |
| Video Extraction | ytdl-core (только YouTube) |
| Video Playback | WebView + нативный Chromium player |
| Time Sync | NTP (pool.ntp.org + time.google.com) |
| P2P | switchboard-js (Rust/NAPI) |

---

## Провайдеры видео (16 штук)

| Провайдер | Метод |
|-----------|-------|
| YouTube | ytdl-core → DASH MPD |
| Netflix | WebView + cookie scrape |
| Amazon Prime | Header injection (X-Rave-Credentials) |
| Disney+ | WebView + cookie |
| HBO Max | WebView |
| Twitch | WebView + dark mode cookie inject |
| Pluto TV / Tubi / Crunchyroll | WebView + URL regex |
| VK | OAuth flow |
| Web (universal) | Любой URL → WebView |

---

## Механизм синхронизации

### Уровень 1 — NTP Correction
```javascript
class NTPSync {
  // Опрос 20+ NTP серверов (pool.ntp.org, time.google.com, etc.)
  // Скользящее среднее по 60 значениям
  // Отправляет "ntp-delta" в renderer каждые 4 сек
  poll(iteration = 1) {
    this.cache(await this.getJSOffset())
    mainWindow.webContents.send("ntp-delta", this.cachedNtpDelta)
    setTimeout(this.poll, 4000)
  }
}
```

### Уровень 2 — Priapus WebSocket
```
wss://cdn01.godmademefunky.com  (или cdn02)
Authorization: Bearer <priapusToken>
API-Version: 4
```

### Уровень 3 — Drift Compensation
```javascript
// У каждого получателя:
const drift = (Date.now() + ntpDelta) - payload.sentAt
const corrected = payload.position + drift
video.currentTime = corrected
```

### Ключевые IPC события
| Код | Реальное имя | Назначение |
|-----|-------------|-----------|
| `a9` | `sync` | Синхронизация состояния |
| `mF` | `reset_sync` | Сброс синхронизации |
| `du` | `open_video` | Открыть видео в комнате |
| `mX` | `handlemi` | Обработчик WSS сообщений |

---

## Что нам нужно добавить

### КРИТИЧНО — NTP drift compensation
```typescript
// В useWatchParty.ts
socket.on('video:sync', (payload) => {
  const drift = (Date.now() - payload.sentAt) / 1000
  const corrected = payload.position + drift
  videoRef.current?.setPositionAsync(corrected * 1000)
})

// В каждый emit:
socket.emit('video:play', {
  position: currentTime,
  sentAt: Date.now(),   // ← ДОБАВИТЬ!
  roomId
})
```

### НЕ нужно копировать
- Switchboard (P2P bandwidth monetization)
- Netflix/Disney WebView scraping (платные платформы)

---

> Полная документация: `docs/RAVE_ANALIZ.md` (825 строк)
