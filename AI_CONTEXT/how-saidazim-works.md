---
type: profile
updated: 2026-05-03
source: telegram-full-history + прямое общение
---

# 👤 Как работать с Saidazim

## Кто он

- **GitHub:** Foreger
- **Компания:** tezCode (Ташкент, UTC+5) — AI-first стартап-студия
- **Проект:** Rave (weWatch / CineSync) — социальный онлайн-кинотеатр
- **Роль по RACI:** Developer (Emirhan формально TL, но Saidazim делает основную работу)
- **Активность:** топ-2 в компании — 20 коммитов за 48ч, уступает только Bekzod (27)
- **Claude план:** Pro $20/мес (Rave команда = $40 всего: Emir + Foreger)

## Технический стек

- **Сильное:** Node.js, Express, MongoDB, Redis, Socket.io, Docker, микросервисы
- **Зона в Rave:** services/*, apps/admin-ui/ (backend + admin UI)
- **Не его зона:** apps/mobile/ (Emirhan), apps/web/ (нет ответственного)

## Стиль работы с Claude

- **Язык:** только русский (АБСОЛЮТНОЕ правило, без исключений)
- **Режим:** предпочитает Multi-Agent (Mode B) для больших задач
- **Стиль:** пишет кратко → ожидает краткости в ответ, без лишних объяснений
- **Доверие:** доверяет Claude самостоятельно принимать технические решения и просто делать
- **Не любит:** когда Claude много спрашивает разрешения, объясняет очевидное, затягивает
- **Работает:** пик 16:00–18:00, вечер 22:00–23:00 (UTC+5)

## Контекст в команде

- Bekzod — CEO/основатель, делает code review всех проектов, двигает AI-first культуру
- Bekzod делал review Rave (2026-04-21): **оценка B-** — sync протокол хорошо, но Redis adapter отсутствует
- Emirhan (Emir) — официально Mobile TL Rave, но коммитит мало
- Все 14 человек работают через Telegram (TEZCODE Team Managment, ID: 2640882371)
- Commit рейтинг — публичный KPI, бот публикует каждые 48ч, Saidazim держит высокую планку

## Проекты tezCode (для контекста)

| Приоритет | Проект | Статус |
|-----------|--------|--------|
| 🏆 Флагман | HamshiraGo | Production Beta (мед. платформа) |
| ⭐ Его проект | Rave | MVP (онлайн-кинотеатр) |
| 🤖 CEO-проект | AI-office | Alpha/Beta (AI платформа) |
| 💰 Работает | VENTRA / POS | Production (аналитика / касса) |
| 🧪 Labs | savdo-builder, Zzone, Work-Controll | MVP стадия |

## Что Claude должен делать автоматически

- При старте: читать daily note + проверять незакрытые checkpoints
- При старте: читать tezCode Telegram (последние 3 дня) → сообщать важное
- Telegram: если URGENT/BUG/MENTION → сразу показать, не ждать вопроса
- Commit рейтинг — если в чате есть → упомянуть позицию Saidazim
- Если Bekzod написал что-то про Rave в чате → обязательно показать Saidazim
