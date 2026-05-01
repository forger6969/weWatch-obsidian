---
type: decision
project: weWatch
title: "YouTube: iframe embed over proxy stream"
date: 2026-05-01
executor: Saidazim
---

# 🏛 YouTube: iframe embed over proxy stream

**Project:** weWatch | **Date:** 2026-05-01 11:13 | **By:** Saidazim

## Decision

Decided to use YouTube IFrame Player API (embed) instead of yt-dlp+proxy stream. Reasons: 1) googlevideo.com URLs are IP-locked to server — mobile cant stream directly; 2) proxy = server bandwidth cost for full video; 3) iframe = zero server traffic, no bot detection. Known limitation: no onSeek event in IFrame API — seek sync goes via PAUSE→PLAY pattern. Member controls: blocked by pointerEvents overlay, controls:1 still visible (cosmetic).

## Rationale

## Consequences
