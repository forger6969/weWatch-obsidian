---
type: plan
project: weWatch
title: "CineSync → Rave Transformation Plan"
date: 2026-04-14
version: "1.0"
author: "Claude Opus 4.6 + Project owner"
tags: [plan, architecture, ux, scope]
---

# 🔄 CineSync → Rave Transformation Plan

**Hub:** [[../00-weWatch-Overview]] | **Источник:** `docs/RAVE_TRANSFORMATION_PLAN.md`

## Executive Summary

**Цель:** Сделать weWatch функциональным клоном Rave (rave.io).

**Основная проблема:** ~50% из 173 commits потрачено на вещи которых нет в Rave:
- Movie catalog + Elasticsearch
- yt-dlp + HLS pipeline  
- Battle / Achievement / Stats
- Admin panel
- Web app (Next.js)

**Первый реальный Rave-style commit появился только на 5-й неделе.**

---

## Ключевые изменения UX

### Entry Point
```
Было:  App → Home (Netflix-style catalog) → Rooms
Нужно: App → Rooms tab (главный экран) → Source Picker
```

### Создание комнаты
```
Room создаётся → "+" в комнате → Source Picker
→ Browser tab → пользователь открывает любой сайт
→ URL detected → popup "Add to party?"
→ CHANGE_MEDIA event → все участники видят контент
```

---

## Рекомендованная архитектура (Hybrid)

### Watch Party Sync
```
Socket.io — сигнальный слой (play/pause/seek, metadata)
WebRTC DataChannel — быстрый sync (timestamp, buffer state)
```

### Source Detection
| Тип | Метод |
|-----|-------|
| YouTube | ytdl-core → DASH MPD |
| Любой сайт | WebView URL intercept |
| Direct video | HLS/MP4 proxy |

---

## Scope Cleanup (что убрать)

| Компонент | Статус |
|-----------|--------|
| Movie catalog (Netflix-style) | ❌ Убрать из главного |
| Battle / Achievement | 📦 Второй приоритет |
| Admin panel | 📦 Второй приоритет |
| Web app (Next.js) | 📦 После MVP |
| Rooms tab | ✅ ГЛАВНЫЙ ЭКРАН |
| Source Picker + Browser | ✅ Приоритет |
| Chat + Emoji в комнате | ✅ Приоритет |

---

## Timeline

| Неделя | Задача |
|--------|--------|
| 1 | Entry point fix, Room creation flow |
| 2 | Source Picker + Browser tab |
| 3 | URL Detection + Media popup |
| 4 | Sync (Socket.io + NTP) |
| 5 | Voice chat (WebRTC) |

> Полная документация: `docs/RAVE_TRANSFORMATION_PLAN.md` (1735 строк)
