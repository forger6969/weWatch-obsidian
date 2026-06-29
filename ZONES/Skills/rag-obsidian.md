---
zone: Skills
type: tool
tool: rag
updated: 2026-06-29
---

# 🔎 RAG — Семантический поиск по Obsidian vault

Локальный RAG над всем vault'ом (`~/Documents/weWatch-obsidian`). Полностью офлайн — данные наружу не уходят. Собран 2026-06-29.

## Использование

```bash
bash .claude/scripts/rag.sh q "<вопрос>"   # семантический поиск (RU/UZ/EN), ~1с
bash .claude/scripts/rag.sh index          # пересобрать индекс после изменений vault
```

## Когда применять

- Перед нетривиальной задачей — вспомнить прошлые решения/баги/контекст.
- На вопрос «мы это уже решали? где про X?».
- **Дополняет grep:** grep ищет буквально (по словам), RAG — по смыслу. Узбекский/английский запрос находит русскую заметку.

## Стек (лёгкий, без torch)

- `fastembed` (ONNX) + `paraphrase-multilingual-MiniLM-L12-v2`
- `numpy` + brute-force cosine (векторная БД не нужна — vault маленький)

## Файлы

- Скрипты (коммитятся): `.claude/scripts/rag.sh`, `rag_common.py`, `rag_index.py`, `rag_query.py`
- Индекс + venv: `.claude/rag/` — **в .gitignore** (правило `.claude/*`), не коммитится

## Показатели

- 203 заметки → 1098 чанков, индекс ~2.8 МБ
- Запрос ~1с (модель в кэше)

## Интеграция

Вшито в `CLAUDE.md`: раздел «Сначала поиск», блок «загрузка памяти», дерево скиллов. Применяется каждую сессию автоматически как часть research-фазы.

## Связано

[[../MCPs/computer-control-mcp|Computer Control MCP]] | [[../../WeWatch-Hub|Hub]]
[[../../PROJECTS/weWatch/LAST_SESSION|Last Session]]
