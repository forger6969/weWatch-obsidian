---
zone: Skills
type: skill
name: remotion-audio
updated: 2026-05-26
zones: [Instagram]
---

# Remotion Audio Skill

## Royalty-Free Music — Qayerdan olish

### ✅ ISHLAYDI (curl/wget orqali)

| Manba | URL format | Litsenziya |
|-------|-----------|------------|
| **incompetech.com** (Kevin MacLeod) | `https://incompetech.com/music/royalty-free/mp3-royaltyfree/TRACK.mp3` | CC BY 4.0 |
| **Free Music Archive** | `https://files.freemusicarchive.org/...` | Turli CC |

```bash
# Ishlashi tekshirilgan
curl -L -o bg.mp3 "https://incompetech.com/music/royalty-free/mp3-royaltyfree/Electro%20Sketch.mp3"
```

### ❌ ISHLAMAYDI (CDN blok)
- Pixabay CDN → 403
- Mixkit CDN → 403 / AccessDenied
- Bensound → 403

---

## SFX — Sox (brew install sox)

```bash
# Whoosh — yumshoq (brownnoise + reverb)
sox -n whoosh.wav synth 0.55 brownnoise vol 0.35 fade 0.12 0.55 0.28 rate 44100
sox whoosh.wav whoosh_reverb.wav reverb 55 50 100
sox whoosh_reverb.wav whoosh.mp3

# Pop — card uchun
sox -n pop.wav synth 0.08 sine 300-80 vol 1.0 fade 0 0.08 0.03 rate 44100
sox pop.wav pop.mp3

# Musiqa trim (30s + fade)
sox bg_full.mp3 bg.mp3 trim 0 30 fade 1.5 30 2
```

---

## Remotion Audio Component

```tsx
import { Audio, staticFile, Sequence } from 'remotion';

// Fon musiqasi
<Audio src={staticFile('audio/bg.mp3')} volume={0.28} />

// Whoosh — fazadan 14 frame oldin
<Sequence from={transitionFrame - 14} durationInFrames={30}>
  <Audio src={staticFile('audio/whoosh.mp3')} volume={0.55} />
</Sequence>

// Pop — card chiqish vaqtida
<Sequence from={cardFrame} durationInFrames={20}>
  <Audio src={staticFile('audio/pop.mp3')} volume={0.45} />
</Sequence>
```

**MUHIM:** Audio Sequence'lari DOM'da fazalardan KEYIN yozilsin (aks holda ko'rinmaydi).

---

## Instagram Safe Zone

- `paddingBottom: 320` — pastki tugmalar uchun
- `paddingTop: 120` — yuqori nav uchun
- `paddingRight: 160` — o'ng action buttons uchun

---

## Litsenziya

Kevin MacLeod attribution (caption'ga):
```
🎵 Music: "Track Name" by Kevin MacLeod (incompetech.com) — CC BY 4.0
```
