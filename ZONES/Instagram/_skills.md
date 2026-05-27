---
zone: Instagram
type: skills
updated: 2026-05-27
---

# Instagram Zone — Skills & Tools

## Skills (fayl yo'li: `.claude/skills/`)

| Skill | Fayl | Qachon ishlatish |
|-------|------|-----------------|
| **remotion-audio** | `remotion-audio.md` | Remotion videoga audio qo'shish |
| **frontend-design** | `frontend-design.md` | Slide UI dizayn qoidalari |
| **visual-testing** | `visual-testing.md` | Render natijasini tekshirish |
| **remotion-video-creation** | `ZONES/Instagram/remotion-video-creation.md` | Полный пайплайн: Remotion + Higgsfield + Reels |

## Remotion Render Buyruqlari

```bash
# Bitta composition render
npx remotion render src/index.ts WeWatchReel out/wewatch-reel.mp4 --codec=h264

# Barcha slideslar (render-all.js)
node render-all.js

# Preview (brauzerda ko'rish)
npx remotion preview src/index.ts
```

## Audio Skills
→ Qarang: [[Skills/remotion-audio]]

## Instagram Formatlar

| Format | O'lcham | FPS | Duration |
|--------|---------|-----|----------|
| Reel | 1080×1920 | 30 | max 90s |
| Carousel slide | 1080×1080 | 30 | 5s |
| Story | 1080×1920 | 30 | max 15s |

## Coremed Uslub (Carousel slides)
- Dark bg (#0a0a12)
- Accent: teal (#7C3AED) yoki brand rangi
- Pill badge: yuqori chap
- Counter: yuqori o'ng (1/5)
- Footer: wewatch.uz | tezcode.dev | swipe →
- Font: system-ui bold, letterSpacing: -0.03em
