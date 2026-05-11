---
type: decision
project: weWatch
title: "COOKIE_COLLECTION_JS удалён — Play Store spyware"
date: 2026-05-11
executor: Saidazim
---

# 🏛 COOKIE_COLLECTION_JS удалён — Play Store spyware

**Project:** weWatch | **Date:** 2026-05-11 15:36 | **By:** Saidazim

## Decision

Убрали COOKIE_COLLECTION_JS из мобильного приложения. Это был JS-скрипт который инжектился в WebView и собирал document.cookie со сторонних сайтов. Play Store автоматический сканер классифицирует такой код как spyware. Замена: server-side cookie jar — Playwright сам собирает cookies при извлечении видео, сохраняет в Redis (cookie:{domain}, TTL 24h), yt-dlp читает через --add-header Cookie:.

## Rationale

## Consequences
