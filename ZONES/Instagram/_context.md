---
zone: Instagram
type: context
updated: 2026-05-26
---

# Instagram Zone — Context

## Nima qilindi

### 2026-05-26 — WeWatch Instagram Reels + Slides

**Slides (carousel, 1080×1080):**
- Slide09-IntroUz — WeWatch tanishuv, Coremed uslubida
- Slide10-ProblemUz — Muammo slide
- Slide11-FeaturesUz — Imkoniyatlar
- Slide12-HowItWorksUz — Qanday ishlaydi (3 qadam)
- Slide13-CTAUz — CTA (wewatch.uz)

**Reel (1080×1920, 30fps, 30s) — `marketing/instagram/out/wewatch-reel.mp4`:**
- Intro (5s): LogoIcon + wordmark, "Birga Tomosha 🎬"
- Problem (6s): "Filmni yolg'iz ko'ryapsanmi?" — amber fon, word-by-word
- Solution (5s): "Biz — WeWatch." — watermark W, centered, scale reveal
- Features (8s): 4 ta kartochka pop-in, teal fon
- CTA (6s): "Birinchilar qatorida bo'l.", circle rings, wewatch.uz

**Audio:**
- Fon: Kevin MacLeod "Electro Sketch" (incompetech.com, CC BY)
- Whoosh: sox brownnoise + reverb
- Pop: sox sine 300→80Hz

## Fayl joylashuvi
```
marketing/instagram/
  src/
    slides/09-13-*.tsx       — Uzbek carousel slides
    slides/WeWatchReel.tsx   — 30s Reel
    components/
      SlideLayout.tsx        — Coremed-style layout
      Logo.tsx               — LogoIcon + Logo (wordmark)
      Pill.tsx               — tag pill
  public/audio/              — bg.mp3, whoosh.mp3, pop.mp3
  out/
    wewatch-reel.mp4         — tayyor video
    Slide09-13 *.mp4         — carousel slides
  src/Root.tsx               — barcha composition'lar
  render-all.js              — batch render script
```

## Texnik stack
- **Remotion** — React-based video framework
- **sox** — SFX generatsiya (brew install sox)
- **ffmpeg** — audio processing
- **TypeScript + React**

## Keyingi qadamlar
- [ ] Reels Instagram'ga yuklash
- [ ] Slides carousel sifatida yuklash
- [ ] Kevin MacLeod attribution qo'shish caption'ga
- [ ] Stories version yaratish (boshqacha format)

## Qarorlar
- `Logo showIcon=true` = 2 ta W belgisi ko'rinadi → YOQIMLI EMAS. Faqat `LogoIcon` yoki `Logo` (showIcon=false) ishlatish
- Instagram safe zone: paddingBottom min 320px, paddingRight min 150px
- Overlay elementlar (corner logo) DOM'da OXIRIDA bo'lishi kerak (z-index emas, DOM order)

<!-- session ended: 2026-05-26 21:23 -->

<!-- session ended: 2026-05-26 21:26 -->

<!-- session ended: 2026-05-26 21:46 -->

<!-- session ended: 2026-05-26 21:58 -->

<!-- session ended: 2026-05-26 22:11 -->

<!-- session ended: 2026-05-26 22:20 -->
