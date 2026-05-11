---
type: decision
project: weWatch
title: "YouTube: embed-only, no yt-dlp"
date: 2026-05-11
executor: Saidazim
---

# 🏛 YouTube: embed-only, no yt-dlp

**Project:** weWatch | **Date:** 2026-05-11 15:36 | **By:** Saidazim

## Decision

Перешли на extractionMethod='embed-api' для YouTube. yt-dlp и googlevideo.com URLs убраны полностью. Причина: Google владеет и YouTube (ToS нарушение) и Play Store (double exposure — могут забанить приложение). Embed через iframe Player API безопасен — не нарушает ToS, Play Store не видит.

## Rationale

## Consequences
