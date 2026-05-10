---
type: metrics
project: weWatch
tags: [kpis, analytics, growth, metrics]
updated: 2026-05-11
---

# 📊 KPIs — WeWatch Marketing

## North Star Metric

> **Weekly Active Rooms** — количество уникальных room сессий в неделю.
> Если люди создают и заходят в rooms — продукт работает.

---

## Acquisition метрики

| Метрика | Формула | Цель Ф1 | Цель Ф2 | Факт |
|---------|---------|---------|---------|------|
| Установки (total) | App Store + Play | 500 | 5 000 | — |
| Установки/неделю | новые инсталлы | 50 | 500 | — |
| K-factor | invites × conversion | 0.5 | 1.0+ | — |
| Invite Rate | % users → shared link | 50% | 70% | — |
| Web → App конверсия | web visitors → install | 10% | 20% | — |
| CPI (если реклама) | $spent / installs | — | < $1.5 | — |

---

## Activation метрики

| Метрика | Формула | Цель Ф1 | Факт |
|---------|---------|---------|------|
| Activation Rate | % установивших → создал room | 40% | — |
| Time to First Room | мин. от регистрации до room | < 5 мин | — |
| Onboarding completion | % прошедших onboarding | > 80% | — |

---

## Retention метрики

| Метрика | Формула | Цель Ф1 | Цель Ф2 | Факт |
|---------|---------|---------|---------|------|
| Day-1 Retention | вернулись на следующий день | > 30% | > 40% | — |
| Day-7 Retention | вернулись через неделю | > 20% | > 30% | — |
| Day-30 Retention | вернулись через месяц | > 10% | > 20% | — |
| MAU | активных за месяц | 200 | 2 000 | — |
| Sessions/user/week | среднее сессий на юзера | > 2 | > 3 | — |

---

## Engagement метрики

| Метрика | Цель Ф1 | Факт |
|---------|---------|------|
| Avg session duration | > 45 мин | — |
| Chat messages/session | > 5 | — |
| Reactions/session | > 3 | — |
| Battles created/week | > 10 | — |
| Achievements unlocked | > 30% users | — |

---

## Revenue метрики (будущее)

| Метрика | Когда | Цель |
|---------|-------|------|
| Premium conversion | После 5 000 MAU | 5% |
| ARPU | После монетизации | $2–5/мес |
| LTV | После 6 мес данных | > $15 |

---

## Еженедельный трекинг

### Шаблон (каждую пятницу)

```
## Неделя [X] — [дата]

### Acquisition
- Установки: [N] (+/- vs прошлая нед.)
- Top канал: [канал]
- K-factor: [N]

### Retention
- Day-7: [%]
- WAR (Weekly Active Rooms): [N]

### Highlights
- [что хорошо]

### Issues
- [что плохо / что исправить]

### Next week focus
- [1 главная задача]
```

---

## Инструменты аналитики

| Инструмент | Что трекает | Статус |
|-----------|-----------|--------|
| App Store Connect | iOS installs, ratings, crashes | ⬜ Настроить |
| Google Play Console | Android installs, ANRs | ⬜ Настроить |
| Mixpanel / Amplitude | Events, funnels, cohorts | ⬜ Фаза 1 |
| Sentry | Crashes, errors | ✅ Реализован |
| Custom Analytics | Room sessions, WAR | ✅ Backend готов |
