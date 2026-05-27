# Remotion + AI Video — Полный скилл

**Дата изучения:** 2026-05-27
**Контекст:** Создание Instagram Reels для weWatch (1080×1920, 9:16)

---

## 1. REMOTION — React-based видео фреймворк

### Установка и запуск
```bash
cd marketing/instagram
npx remotion studio          # предпросмотр в браузере
npx remotion render <CompId> output.mp4 --codec=h264
```

### Структура проекта
```
marketing/instagram/
  src/
    Root.tsx          # регистрация всех Composition
    slides/           # каждый компонент = отдельный слайд/видео
  public/             # статические файлы (фото, mp4, svg, mp3)
```

### Регистрация компонента в Root.tsx
```tsx
import { WeWatchReel2, REEL2_DURATION } from './slides/WeWatchReel2';

<Composition
  id="WeWatchReel2"
  component={WeWatchReel2}
  width={1080} height={1920}   // 9:16 portrait
  fps={30}
  durationInFrames={REEL2_DURATION}
/>
```

### Форматы
| Формат | Размер | Использование |
|--------|--------|---------------|
| Instagram Post | 1080×1080 | Карусели, посты |
| Instagram Reel | 1080×1920 | Reels, Stories |
| App Store | 1080×1920 | Скриншоты приложения |

---

## 2. АНИМАЦИИ — Ключевые паттерны

### Плавные анимации (НЕ кринж)
```tsx
import { Easing, interpolate, spring } from 'remotion';

// Хорошо — Easing curves (профессионально)
const t = interpolate(frame, [0, 30], [0, 1], {
  extrapolateLeft: 'clamp',
  extrapolateRight: 'clamp',
  easing: Easing.out(Easing.cubic),  // плавный выход
});

// Spring с высоким damping = без отскока
const s = spring({ frame, fps, config: { damping: 26, mass: 0.85 }, delay: 8 });

// Helper для часто используемого ease
const ease = (frame, from, to, delay = 0, duration = 24) =>
  interpolate(frame, [delay, delay + duration], [from, to], {
    extrapolateLeft: 'clamp', extrapolateRight: 'clamp',
    easing: Easing.out(Easing.cubic),
  });
```

### Spring damping — правило:
| damping | Эффект |
|---------|--------|
| 10–14 | Сильный отскок (кринж) |
| 18–22 | Лёгкий отскок (ОК) |
| 24–28 | Плавно без отскока (профессионально) |

### Ken Burns (живое фото)
```tsx
const kenBurns = interpolate(frame, [0, DURATION], [1.0, 1.06], {
  extrapolateLeft: 'clamp', extrapolateRight: 'clamp',
  easing: Easing.inOut(Easing.sin),
});
<img style={{ transform: `scale(${kenBurns})`, transformOrigin: 'center center' }} />
```

### Floating glow (дрейфующее свечение)
```tsx
const glowY = Math.sin(frame * 0.03) * 30;  // медленный дрейф
<div style={{ top: -150 + glowY, ... }} />
```

### Breathing glow в CTA
```tsx
const glowScale = 1 + Math.sin(frame * 0.07) * 0.06;   // ±6%
const glowOpacity = 0.2 + Math.sin(frame * 0.07) * 0.05;
```

### Fade out сегмента
```tsx
const fadeOut = ease(frame, 1, 0, DURATION - 10, 10);
```

### Flash transition между сегментами
```tsx
const FlashTransition = () => {
  const frame = useCurrentFrame();
  const opacity = interpolate(frame, [0, 2, 8], [0, 0.4, 0], {
    extrapolateLeft: 'clamp', extrapolateRight: 'clamp',
    easing: Easing.out(Easing.quad),
  });
  return <AbsoluteFill style={{ background: 'rgba(255,255,255,1)', opacity }} />;
};

// В main компоненте:
<Sequence from={SEGMENT_END - 2} durationInFrames={10}><FlashTransition /></Sequence>
```

---

## 3. СТРУКТУРА РИЛСА (проверенная)

```tsx
const INTRO_DUR = 3 * 30;   // 3s — "Как работает? 3 шага"
const LOGIN_DUR = 4 * 30;   // 4s — Шаг 1 с Ken Burns фото
const TEXT_DUR  = 2 * 30;   // 2s — Переходный слайд "ТЕПЕРЬ..."
const VIDEO_DUR = 5 * 30;   // 5s — AI-сгенерированное видео
const CTA_DUR   = 3 * 30;   // 3s — CTA + URL
// Итого: 17 секунд
```

### Логотип — использовать настоящий
```tsx
// Скопировать: apps/web/public/favicon.svg → marketing/instagram/public/logo.svg
<img src={staticFile('logo.svg')} style={{ width: 52, height: 52, borderRadius: 10 }} />
```

### Видео в Sequence
```tsx
<Video
  src={staticFile('tap-transition-reel.mp4')}
  style={{ position: 'absolute', inset: 0, width: '100%', height: '100%', objectFit: 'cover',
    transform: `scale(${videoZoom})` }}
/>
```

### Фоновая музыка
```tsx
<Audio src={staticFile('audio/bg.mp3')} volume={0.28} />
```

---

## 4. HIGGSFIELD — AI Video Generation

### CLI
```bash
higgsfield account status           # баланс кредитов
higgsfield model list --json        # все модели
higgsfield model get kling3_0       # параметры модели
```

### Kling 3.0 (работает на basic plan)
```bash
higgsfield generate create kling3_0 \
  --prompt "описание движения" \
  --start-image ./начало.jpg \
  --end-image ./конец.jpg \
  --aspect_ratio 9:16 \        # ВАЖНО для Reels
  --duration 5 \
  --mode std \                  # pro стоит больше
  --wait
```

### Аккаунты
- Основной: `ertan.emirhan.tur@gmail.com` — basic, ~12 кредитов
- Kling std 9:16 5s ≈ 7-8 кредитов

### Модели по задачам
| Задача | Модель | Заметки |
|--------|--------|---------|
| Image-to-video переход | `kling3_0` | start-image + end-image |
| Серьёзное видео | `seedance_2_0` | Pro plan required |
| Маркетинговое видео | `marketing_studio_video` | avatars + products |

### Скачать результат
```bash
curl -L "https://...cloudfront.net/....mp4" -o public/tap-transition-reel.mp4
```

---

## 5. РАБОЧИЙ ПРОЦЕСС (весь пайплайн)

```
1. Генерация фото      → Leonardo AI (промпт: рука держит телефон с зелёным экраном)
2. Генерация видео     → Higgsfield Kling (start→end image, 9:16)
3. Скачать активы      → public/ папка
4. Создать компонент   → src/slides/NewSlide.tsx
5. Зарегистрировать    → src/Root.tsx
6. TypeScript check    → npx tsc --noEmit
7. Рендер              → npx remotion render <Id> /tmp/output.mp4 --codec=h264
8. Отправить           → mcp__plugin_telegram_telegram__reply
```

---

## 6. WEWATCH ВИЗУАЛЬНЫЙ СТИЛЬ

```
Фон:       radial-gradient(ellipse at 50% -5%, #2a1060, #0e0525, #030212)
Акцент:    #A78BFA (фиолетовый светлый)
Тёмный:    #7C3AED (фиолетовый тёмный)
Градиент:  linear-gradient(90deg, #A78BFA, #7C3AED) → WebkitTextFillColor
Текст:     #fff (заголовки), #C4B5FD (подписи), rgba(255,255,255,0.32) (мелкий)
Pill:      background: rgba(167,139,250,0.13), border: 1px solid rgba(167,139,250,0.32)
Сетка:     backgroundImage: linear-gradient(rgba(167,139,250,0.025) 1px, ...)
Шрифт:     fontWeight 900 (заголовки), 800 (лого), 700 (pill)
```

---

## 7. ЧАСТЫЕ ОШИБКИ

| Ошибка | Решение |
|--------|---------|
| `Easing.sine` не существует | Использовать `Easing.sin` |
| Видео не заполняет 9:16 | Генерировать с `--aspect_ratio 9:16`, не центрировать 1:1 |
| Spring с bounce (кринж) | Поднять damping до 24-28 |
| `not_enough_credits` | Переключиться на std mode или другой аккаунт |
| `multi_prompt must be valid JSON` | Убрать запятую в конце JSON |
| Логотип не наш | Копировать `apps/web/public/favicon.svg` → `public/logo.svg` |

---

*Создано: 2026-05-27 | Проект: weWatch Instagram Marketing*
