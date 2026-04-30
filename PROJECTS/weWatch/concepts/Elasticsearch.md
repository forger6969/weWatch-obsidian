---
type: concept
tags: [infrastructure, search, weWatch]
---
# 🔍 Elasticsearch

**Role:** Поиск контента | **Port:** 9200
**Hub:** [[../00-weWatch-Overview]]

## Используется в
- [[../services/content]] — поиск фильмов

## ⚠️ Известный баг
Movie.findByIdAndUpdate обходит Mongoose post-save hook
→ Elasticsearch не обновляется при редактировании
