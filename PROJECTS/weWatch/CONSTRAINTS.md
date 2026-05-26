---
type: constraints
project: weWatch
updated: 2026-05-23
---

# WeWatch — Constraints & Anti-Hallucination Rules

> ЧИТАТЬ ПЕРЕД ЛЮБЫМ КОДОМ.
> Эти правила предотвращают галлюцинации и деструктивные изменения.

---

## АБСОЛЮТНЫЕ ЗАПРЕТЫ (никогда, ни при каких условиях)

```
❌ Не трогать apps/mobile/ — зона Emirhan
❌ Не трогать apps/web/ — нет ответственного
❌ Не переименовывать Socket.io events — ломает 3 платформы
❌ Не менять API response format без обновления shared/types
❌ Не делать MongoDB collection drop
❌ Не коммитить .env файлы
❌ Не пушить в main напрямую (только через PR или после review)
❌ Не трогать shared/* без уведомления в Telegram + подтверждения
❌ Не менять production DB вручную
❌ Не пропускать QA (tsc --noEmit) перед merge
```

---

## ANTI-HALLUCINATION PROTOCOL

### Никогда не придумывай:
- Файлы (убедись что они существуют: `ls` или `find`)
- API endpoints (проверяй routes/*.routes.ts)
- Environment variables (проверяй config/index.ts)
- Database schema (читай models/*.model.ts)
- Зависимости (читай package.json)
- Функции/методы (читай сервис перед использованием)
- Импорты (проверяй что модуль реально существует)
- Routes (читай routes файл сервиса)

### Перед любым изменением кода:
```
1. find . -name "*.ts" | grep <service-name>   → найди файл
2. Read <file>                                  → прочитай полностью
3. Проверь текущую реализацию функции
4. grep -r "import.*<symbol>" .                → найди связанные файлы
5. Проверь imports в файле
6. Проверь зависимости (package.json)
7. Только потом пиши код
```

### Если данных недостаточно:
```
→ Сначала исследуй проект (Research Phase)
→ Скажи что информации недостаточно
→ НЕ делай предположений
→ НЕ пиши код пока не прочитал связанные файлы
```

---

## CLEAN CODE CONSTRAINTS

```typescript
// ❌ НИКОГДА
const data: any = {};           // any type
console.log('debug');           // используй logger
function huge() { /* 400+ строк */ }  // split файл
if (a) { try { if (b) { try { // nested try/catch

// ✅ ВСЕГДА
const data: IMovie = {};        // typed
logger.info('msg', { ctx });    // Winston
// файлы ≤ 400 строк          // split если больше
```

---

## АРХИТЕКТУРНЫЕ CONSTRAINTS

### Нельзя без согласования:
- Добавлять новый сервис (новый Docker container)
- Менять схему MongoDB (добавлять required поля к существующей)
- Менять socket event names
- Добавлять новые npm зависимости к shared/
- Менять JWT алгоритм или структуру payload
- Менять API response format (apiResponse.success/error/paginated)
- Менять структуру папок сервиса

### Можно без согласования (зона Saidazim):
- Добавлять новые endpoints в существующие сервисы
- Добавлять optional поля в MongoDB schema
- Создавать новые validators
- Создавать новые middleware
- Рефакторить внутри сервиса без API changes
- Добавлять Redis кэш к существующим endpoints

---

## CODING RULES

### Controller = HTTP только
```typescript
// ❌ Нельзя — логика в controller
router.get('/:id', async (req, res) => {
  const movie = await Movie.findById(req.params.id);  // NO!
});
// ✅ Правильно — сервис вызов
router.get('/:id', verifyToken, async (req, res, next) => {
  try {
    const movie = await contentService.getMovieById(req.params.id, req.user.id);
    res.json(apiResponse.success(movie));
  } catch (error) { next(error); }
});
```

### Не дублировать utils
```
Перед написанием утилиты → проверь shared/utils/
Перед написанием middleware → проверь shared/middleware/
```

### Rate limiting — обязателен для:
- Auth endpoints (brute force)
- Публичные endpoints (abuse)
- Upload endpoints (dos protection)

---

## GIT CONSTRAINTS

```
Branch: saidazim/feat-xxx или saidazim/fix-xxx
Commit: feat(service): ... | fix(service): ... | refactor(service): ...
НЕ: push в main напрямую
НЕ: force push к любой ветке без явной необходимости
НЕ: merge без прохождения tsc --noEmit
```

---

## TASK LOCKING CONSTRAINTS

Перед стартом задачи ОБЯЗАТЕЛЬНО:
```
1. git pull origin main
2. Проверить docs/Tasks.md на pending[другой разработчик]
3. Написать pending[Saidazim] → commit → push
4. tg-notify.sh claim ...
```

НЕ начинать задачу без claim — риск конфликта с Emirhan.

---

## KNOWN BUGS (не воспроизводить!)

### adminClient double /api/v1
`EXPO_PUBLIC_ADMIN_URL` уже содержит `/api/v1`.
НЕ добавлять `/api/v1` при создании axios client — будет `/api/v1/api/v1/...` → 404.

### Socket.io event rename
Переименование любого event → ломает мобильный клиент И web клиент одновременно.
Изменение event name → ТОЛЬКО через shared/constants/socket-events.ts + одновременно все платформы.

---

*CONSTRAINTS.md | WeWatch | Saidazim | updated: 2026-05-23*
