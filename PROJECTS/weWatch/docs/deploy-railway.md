---
type: guide
project: weWatch
title: "Railway Deployment Guide"
date: 2026-05-01
tags: [devops, deploy, railway]
---

# 🚂 Railway Deployment Guide

**Hub:** [[../00-weWatch-Overview]] | **Источник:** `docs/DEPLOY_RAILWAY.md`

## Архитектура
7 микросервисов, каждый — отдельный Railway Service.
Build: `Dockerfile` в root контексте каждого сервиса.

## Сервисы и порты
| Сервис | Порт | Railway URL |
|--------|------|------------|
| [[../services/auth]] | 3001 | auth.railway.app |
| [[../services/user]] | 3002 | user.railway.app |
| [[../services/content]] | 3003 | content.railway.app |
| [[../services/watch-party]] | 3004 | watchparty.railway.app |
| [[../services/battle]] | 3005 | battle.railway.app |
| [[../services/notification]] | 3007 | notification.railway.app |
| [[../services/admin]] | 3008 | admin.railway.app |

## Инфраструктура
- [[../concepts/MongoDB]] — Atlas (внешний)
- [[../concepts/Redis]] — Railway Redis plugin
- [[../concepts/Elasticsearch]] — Railway plugin

## ENV переменные (обязательные)
```
MONGODB_URI=
REDIS_URL=
JWT_ACCESS_SECRET=
JWT_REFRESH_SECRET=
FIREBASE_SERVICE_ACCOUNT=
```

> Полная документация: `docs/DEPLOY_RAILWAY.md`
