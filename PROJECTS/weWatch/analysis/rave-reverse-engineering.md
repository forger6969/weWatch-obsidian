---
title: Rave Reverse Engineering
updated: 2026-05-01
---

# Rave v1.17.12 — Reverse Engineering

> Полный анализ: [[rave-analiz-full]]

## Ключевые выводы

- **Стек:** Electron (Chromium + Node.js), React, Webpack
- **Видео:** только YouTube извлекается через `ytdl-core` → DASH MPD. Netflix/Amazon/Disney — просто WebView + cookie scrape
- **Синхронизация:** NTP (20+ серверов, каждые 4 сек) → Priapus WSS (`wss://cdn01.godmademefunky.com`) → drift compensation
- **Формула:** `correctedPosition = sentPosition + (receivedAt - sentAt) / 1000`
- **Switchboard** — P2P монетизация трафика (Infatica/HoneyGain/Pawns), не синхронизация

## Что нужно нам

| Фича | Статус |
|------|--------|
| ytdl-core + DASH | ✅ есть |
| Socket.io комнаты | ✅ есть |
| `serverTimestamp` в SyncState | ✅ есть |
| Drift compensation в useWatchParty | ⏳ не применяется |
| NTP clock offset | ❌ нет |
