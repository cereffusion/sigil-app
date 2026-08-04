# Sigil Forge — Project Status & Handoff

A small suite of occult-themed, browser-based "manifestation" toys. Three linked
pages, no backend, no build step, no dependencies. Everything runs client-side in
a single static HTML file per page.

**Status:** Working prototype, feature-complete for a v1. Built and tested locally.
Not yet deployed, not yet hardened for public release (see *Going Public* below).

---

## What it does

A three-tab flow for turning an intention into a symbol and a practice:

> **Intent → who to petition → a glyph to charge → a method to release it**

The user's phrase carries across all three tabs via a `?phrase=` URL parameter,
so the tools chain into one ritual.

### 1. Sigil Forge — `index.html`
Turns a typed phrase into a sigil (a personal magical glyph).

- **Two generation methods:**
  - *Rose Wheel* — letters placed on a three-ring witch's-wheel cipher, connected
    into a single drawn path with start/end markers.
  - *Letter Overlay* — the distilled letterforms stacked and rotated into one
    composite glyph.
- **Distillation:** strips vowels and duplicate letters (the classic Spare method).
- **Color palettes:** 11 presets including an iridescent "Glitter" mode (gradient
  stroke + scattered sparkles), plus a custom color picker.
- **Chaos slider (0–100):** seeded, deterministic geometric disorder — drifts
  points, warps lines into curves, varies stroke weight like hand pressure, and
  bleeds in stray marks at higher levels. A **Reroll** button reseeds for variations.
- **Export:** Save as SVG or PNG (1200×1200).
- **Animation:** the sigil draws itself stroke by stroke on render.

### 2. Invocation Guide — `invoke.html`
Matches an intention to mythological/spiritual figures who traditionally govern it.

- **90 figures** across 6 types: Goddesses (33), Gods (28), Angels (12),
  Demons — Ars Goetia (12), Orishas (3), Saints (2).
- Traditions span Greek, Roman, Norse, Egyptian, Hindu, Celtic, Sumerian/
  Mesopotamian, Yoruba, Abrahamic, Inca/Andean, Aztec, Maya, and more.
- **Divine mode:** keyword-matches the user's phrase to ~24 life domains
  (wealth, love, healing, protection, grief, etc.) and ranks matching figures.
- **Browse All mode:** the full roster grouped by type.
- Each card gives origin, domains, a description, and a traditional **"To invoke"**
  line (offerings, sacred days, mantras, sayings) drawn from attested practice.
- Links out to Sigil Forge to forge a glyph for the same intent.

### 3. The Working — `manifest.html`
A guide to manifestation methods themselves.

- **20 methods** in 5 families: Word & Writing, Fire & Element, Visualization,
  Lunar Timing, Object & Ritual (sigils, scripting, 369, 55×5, burning, candle
  working, vision boards, knot magic, deity invocation, and more).
- **Finder mode:** three questions (goal: attract/release/reflect · approach ·
  rhythm) → scored, ranked recommendations.
- **Browse All mode:** every method grouped by family.
- Each card lists materials needed, timing, and numbered steps.
- **Live moon phase:** computes tonight's actual lunar phase from the date and
  notes whether it's a waxing (build) or waning (release) window.
- Links back into Sigil Forge and the Invocation Guide to close the loop.

---

## Tech

- **Plain HTML + CSS + vanilla JS.** One self-contained file per page.
- **No framework, no build, no package manager, no backend, no external requests.**
- Rendering: inline SVG (sigils, glyphs), Canvas only for PNG export.
- State: in-memory; the only persistence is the `?phrase=` URL parameter.
- Shared visual language: dark occult theme, gold accents, Georgia serif.

## File structure

```
sigil-app/
├── index.html      Sigil Forge   (~21 KB)
├── invoke.html     Invocation Guide (~47 KB)
├── manifest.html   The Working   (~27 KB)
└── README.md       this file
```

No other assets. Each HTML file is fully standalone and could run from `file://`.

## Run locally

Open any of the three `.html` files in a browser. That's it. (For the `?phrase=`
hand-off between tabs to work cleanly, serving over `http://` via any static
server is slightly nicer than `file://`, but both work.)

---

## Going Public — what to consider

The app is trivial to deploy (static files), so most of the work is **content,
legal, and polish**, not engineering. Ordered by importance:

### 1. Intellectual property — RESOLVED
- ~~Fictional figures (She-Ra, Rainbow Brite)~~ Removed Aug 2026 before
  commercial launch — the site now only features mythological/religious figures.
- The mythological/religious figures themselves are public domain. The *written
  descriptions* are original to this project, so they're yours to license.

### 2. Cultural sensitivity
Several entries come from **living and sometimes closed traditions** — Yoruba
orishas, Santa Muerte, Andean (Pachamama, Inti) and Mesoamerican (Aztec/Maya)
deities. A public audience will include practitioners. Consider:
- A respectful framing note acknowledging these are living traditions, not relics.
- Reviewing the orisha and closed-practice entries for accuracy and tone.

### 3. Disclaimers
There's a light disclaimer line on each page already. For public release,
strengthen it: explicitly "for entertainment and reflection," **not** medical,
financial, legal, or psychological advice. Put it in a footer on every page.

### 4. Privacy (currently a strength)
- No backend, no cookies, no analytics, no data leaves the browser. That's a
  clean privacy story — keep it that way if you can.
- If you add **Vercel Analytics** or similar, you'll need a privacy note and
  possibly cookie/GDPR consent. The `?phrase=` value stays client-side, but note
  that if analytics logs full URLs, users' typed intentions could end up in logs.

### 5. Deployment on Vercel
- It's a static site, so this is easy. Options:
  - Drag-and-drop the folder in the Vercel dashboard, **or**
  - `vercel` CLI from the project root, **or**
  - Push to a Git repo and connect it (enables preview deploys).
- No framework preset needed — choose **"Other"** / no build command; output dir
  is the project root.
- Optional `vercel.json` to set a clean home route and security headers
  (see below). Not required for it to work.
- Add a **custom domain** in the Vercel project settings if desired.

### 6. Polish for a public audience
- **Meta tags:** add `<meta name="description">`, Open Graph / Twitter card tags,
  and a social preview image so shared links look good. Currently none.
- **Favicon:** none yet — add one.
- **Accessibility:** check color contrast (the dim grey on dark is low),
  add ARIA labels to icon-only buttons, ensure full keyboard navigation, and
  add `prefers-reduced-motion` handling for the sigil-draw and chaos animations.
- **Mobile:** layouts are responsive and use a viewport tag; test on real phones,
  especially the palette/chaos rows and the figure grid.
- **Analytics consent / age gate:** probably unnecessary, but occult content may
  warrant a brief "for ages 13+/entertainment" note depending on your audience.

### 7. Licensing & repo hygiene
- Pick a license (e.g. **MIT** for the code). Decide separately how the written
  content may be reused.
- If handing to a developer: it's not currently a Git repo — `git init` first.
- No secrets, env vars, or API keys exist, so nothing to scrub.

### Suggested pre-launch checklist
- [x] Resolve the She-Ra / Rainbow Brite IP question (removed Aug 2026)
- [ ] Add/strengthen a footer disclaimer on all three pages
- [ ] Add a cultural-respect note for living traditions
- [ ] Add meta tags, Open Graph image, and a favicon
- [ ] Accessibility pass (contrast, ARIA, reduced-motion, keyboard)
- [ ] Mobile test on real devices
- [ ] Choose a license; `git init`
- [ ] Deploy to Vercel; attach custom domain
