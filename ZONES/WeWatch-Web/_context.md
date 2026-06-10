---
zone: WeWatch-Web
type: context
updated: 2026-06-10
---

# WeWatch-Web Zone — Context

## Текущее состояние (2026-06-10)

### Что сделано
- **T-E134 ✅** (2026-05-24): Брендинг CineSync → WeWatch во всех web файлах
- **T-E135 ✅** (2026-06-02): PhoneMockup UI fix — proportions (280×580px), contrast, readability
  - ScreenHome: элементы крупнее, spacing лучше
  - ScreenRoom: video preview 90px, participants крупнее
  - ScreenWatching: video area 45%, chat contrast повышен

### Стек
- Next.js (App Router)
- Путь: `apps/web/src/`
- Landing: `apps/web/src/app/page.tsx` → `LandingContent.tsx`
- Phone mockup: `apps/web/src/components/PhoneMockup/`

### Privacy Policy
- `apps/web/src/app/privacy-policy/` — существует (T-S094 ✅)
- URL: https://wewatch.uz/privacy-policy (нужно проверить что задеплоено)

## Активные задачи
- Нет активных задач (всё сделано в Sprint 10)

## Следующие возможные задачи
- SEO оптимизация landing page
- OG meta tags для social sharing
- Performance audit (Core Web Vitals)

## Агент: `.claude/agents/web-agent.md`

<!-- session ended: 2026-05-27 02:52 -->
