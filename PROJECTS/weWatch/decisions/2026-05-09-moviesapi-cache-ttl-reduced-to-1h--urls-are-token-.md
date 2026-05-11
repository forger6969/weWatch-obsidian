---
type: decision
project: weWatch
title: moviesapi cache TTL reduced to 1h — URLs are token-signed and rotate every 1-2h
date: 2026-05-09
executor: Saidazim
---

# 🏛 moviesapi cache TTL reduced to 1h — URLs are token-signed and rotate every 1-2h

**Project:** weWatch | **Date:** 2026-05-09 17:07 | **By:** Saidazim

## Decision

Previously cached for 24h which caused stale/expired video URLs to be served. Security API on moviesapi.club rotates signed tokens frequently.

## Rationale

## Consequences
