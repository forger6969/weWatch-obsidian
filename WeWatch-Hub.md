---
type: hub
domain: weWatch
version: 1.0
updated: 2026-05-26
---

# WeWatch — Hub (Single Source of Truth)

> Bu fayl sessiya boshida BIRINCHI o'qiladi.
> Sub-agent spawn'da INLINE PASTE qilinadi — file path emas, to'liq matn.
> Har o'zgarishda darhol yangilanadi — session oxirida emas.

---

## DOMAIN OVERVIEW

WeWatch (Rave / CineSync) — ijtimoiy onlayn kinoteatr.
Monorepo, mikroservislar. MVP bosqichi. Railway'da deploy qilingan.

**Repo:** /Users/saidazim/Desktop/Rave/
**Branch strategiyasi:** saidazim/feat-xxx | main → production (protected)
**Railway project:** rave (TezCode Team)
**Domain:** wewatch.uz

---

## SERVICE REGISTRY

| Servis | Tech | Port | Railway URL |
|--------|------|------|-------------|
| auth | Node.js + Express + MongoDB | 3001 | auth-production-47a8.up.railway.app |
| user | Node.js + Express + MongoDB | 3002 | user-production-86ed.up.railway.app |
| content | Node.js + Express + Elasticsearch | 3003 | content-production-4e08.up.railway.app |
| watch-party | Express + Socket.io + Redis | 3004 | watch-part-production.up.railway.app |
| battle | Express + MongoDB + Redis | 3005 | — |
| notification | Express + Firebase FCM + Bull | 3007 | notification-production-9c30.up.railway.app |
| admin | Express + MongoDB | 3008 | admin-production-8d2a.up.railway.app |
| admin-ui | React + Vite + Tailwind | 5173 | admin.wewatch.uz |
| web | Next.js | — | wewatch.uz |
| mobile | React Native + Expo | — | — |

**Infra:**
- MongoDB: Railway self-hosted volume (1.23 GB), port 27017
- Redis: Railway self-hosted volume (1.59 GB), port 6380
- Elasticsearch: port 9200

---

## SERVICE OWNER MAP

| Zona | Mas'ul | Sharhlar |
|------|--------|----------|
| services/* | Saidazim | barcha backend servislar |
| apps/admin-ui/ | Saidazim | React admin panel |
| apps/mobile/ | Saidazim + Emirhan | 2026-05-23 dan birgalikda |
| apps/web/ | — | hozircha mas'ul yo'q |
| shared/types,utils,constants | UMUMIY | lock protocol kerak |

---

## SKILLS REGISTRY

| Skill | Fayl | Qachon ishlatiladi |
|-------|------|--------------------|
| research | .claude/skills/research.md | har yangi vazifadan oldin |
| dev-workflow | .claude/skills/dev-workflow.md | ≥3 fayl yoki >20 min |
| spec-driven | .claude/skills/spec-driven-implement.md | kod yozishdan oldin |
| self-reflection | .claude/skills/self-reflection.md | har commit oldidan |
| critic-agent | .claude/skills/critic-agent.md | muhim arxitektura |
| root-cause | .claude/skills/root-cause-tracing.md | bug/xato |
| subagent-dispatch | .claude/skills/subagent-dispatch.md | >5 fayl, multi-agent |
| code-review | .claude/skills/code-review.md | PR review |
| security-audit | .claude/skills/security-audit.md | auth/JWT o'zgarish |
| frontend-design | .claude/skills/frontend-design.md | UI komponent |
| deploy | .claude/skills/deploy.md | Railway deploy |
| brainstorm | .claude/skills/brainstorm.md | /brainstorm |

**Agentlar:** .claude/agents/ — auth, content, watchparty, user-battle-notification, admin, mobile, web, qa, orchestrator

---

## ACTIVE CONTACTS

| Kim | Telegram | Chat ID | Rol |
|-----|----------|---------|-----|
| Saidazim | @forgerjunior | 6299152655 | Backend + Admin |
| Emirhan | @Emirhan7788 | — | Mobile TL |
| TEZCODE Team | — | -1002640882371 | Jamoa guruh |
| AI Council | — | -1003874059304 | Bot maslahat |
| notification bot | @notification_weWatch_bot | — | Vazifa notify |

---

## CREDENTIALS PATH

> Inline ko'rsatilmaydi. Quyidagi fayllarda:

- `.env` fayllar: har servis root'ида
- Railway env vars: `railway variables` CLI orqali
- MongoDB URI: services/*/src/config/index.ts → `MONGODB_URI`
- Redis: `REDIS_URL` env var
- JWT keys: `JWT_SECRET`, `JWT_REFRESH_SECRET`
- Firebase: `FIREBASE_SERVICE_ACCOUNT_KEY`

---

## RULES SUBSET

### MUTLAQ TAQIQLAR (hech qachon, hech qanday holatda)
```
❌ apps/mobile/ — Emirhan zonasi (2026-05-23 dan birgalikda, ammo ehtiyot bo'l)
❌ Socket.io event nomlarini o'zgartirish — 3 platformani buzadi
❌ API response format o'zgartirish — shared/types yangilanmasdan
❌ MongoDB collection drop
❌ .env faylni commit qilish
❌ main ga to'g'ridan push
❌ shared/* — Telegram notify + tasdiqlashsiz
❌ Production DB ni qo'lda o'zgartirish
❌ QA (tsc --noEmit) ni o'tkazib yuborish
❌ Claim qilmasdan vazifa boshlash
```

### KOD QOIDALARI
```
❌ any type   ❌ console.log (logger ishlatish)   ❌ 400+ qator fayl
❌ Magic numbers   ❌ Nested try/catch   ❌ Hardcoded secrets
Controller = faqat HTTP | Service = biznes logika | Screen = render
```

### ANTI-GALLYUTSINATSIYA
```
✅ Har o'zgarishdan oldin: find → Read to'liq → import tekshir → Edit
✅ Fayl mavjudligini tekshir: ls yoki find, keyin gapir
✅ Endpoint: routes/*.routes.ts o'qi
✅ Env var: config/index.ts o'qi
❌ Fayl, endpoint, schema, funksiyani o'ylab topma
```

### GIT QOIDALARI
```
Branch: saidazim/feat-xxx | emirhan/feat-xxx
Commits: feat(auth): | fix(watch-party): | refactor(content):
Vazifa claim: docs/Tasks.md → git add → commit → push → keyin kod
```

---

## PROJECT CONTEXTS

| Kontekst | Fayl | Nima bor |
|----------|------|----------|
| To'liq arxitektura | PROJECTS/weWatch/ARCHITECTURE.md | servislar, pattern, kod |
| Taqiqlar | PROJECTS/weWatch/CONSTRAINTS.md | anti-gallyutsinatsiya + zapretlar |
| Qarorlar | PROJECTS/weWatch/DECISIONS.md | nima uchun shunday |
| API | PROJECTS/weWatch/API.md | barcha endpoints |
| Buglar | PROJECTS/weWatch/_bugs.md | ma'lum buglar (qayta hosil qilma) |
| Android buglar | PROJECTS/weWatch/_android-bugs.md | mobile-specific |
| Vazifalar | docs/Tasks.md (repo ichida) | joriy vazifalar |
| Bajarilganlar | docs/Done.md (repo ichida) | arxiv |
| Oxirgi sessiya | PROJECTS/weWatch/LAST_SESSION.md | qayerda to'xtadik |

---

## ACTIVE SPRINT

**Joriy vazifalar (Saidazim):**
- T-S094 | P2 | [DEVOPS] | Play Store: Privacy Policy + DMCA sahifasi
- T-S082 | P2 | [DEVOPS] | Security: CI/CD pipeline qo'shish
- T-S083 | P3 | [BACKEND] | 26 god files — split eng katta 3 tasi

**Hozirgi fokus:** Instagram marketing (WeWatch launch prep)

**Railway holati (2026-05-26):**
- 10 servis online (8 app + MongoDB + Redis)
- Idle RAM: ~945 MB, cost: ~$10/oy
- MongoDB: 1.23 GB disk | Redis: 1.59 GB disk

---

## SESSION START PROTOCOL

```
1. CLAUDE.md o'qi (global qoidalar)
2. WeWatch-Hub.md o'qi (SHU FAYL — hamma bilim)
3. docs/Tasks.md o'qi (joriy vazifalar)
4. Ish boshlash ✅
```

**Sub-agent spawn pattern:**
```
== DOMAIN == weWatch
== HUB BUNDLE ==
{WeWatch-Hub.md to'liq matni — inline paste, file path emas}
== APPLICABLE RULES ==
Anti-hallucination | Zone check | No Socket.io rename | No shared/* without lock
== TASK ==
{aniq vazifa — file:line, nima o'zgartirish}
```

---

## ORPHAN PREVENTION (Rule 41)

Har yangi fayl = 2 ATOMIK QADAM:
```
Qadam 1: Faylni yoz
Qadam 2: DARHOL shu Hub'ning tegishli bo'limiga link qo'sh:
  - Yangi qaror → PROJECT CONTEXTS bo'limiga
  - Yangi skill → SKILLS REGISTRY ga
  - Yangi servis → SERVICE REGISTRY ga
  - Yangi bug → _bugs.md + PROJECT CONTEXTS
```

Orphan fayl = keyingi sessiyada ko'rinmaydi = yo'qolgan bilim ❌
