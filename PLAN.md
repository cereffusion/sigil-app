# Sigil Forge — Product Roadmap

Written Aug 2026. Current state: three free tools live, $8 mailed sigil postcard
selling through the Mail-A-Mix pipeline (Stripe → PostGrid, compliance-verified),
PWA installed, tip jar live. Marketing intentionally on hold.

---

## Revenue model (three lanes)

| Lane | What | Price | Cut | Status |
|------|------|-------|-----|--------|
| Physical | Mailed sigil postcard | $8 | ~100% minus ~$2–3 print/postage | **LIVE** |
| Digital premium | "The Grimoire" unlock (below) | $4.99 one-time | Stripe ~3% (web) / 15% (app stores) | planned |
| Tips | $1 tip jar | $1 | ~5% | live (web only — must be removed or converted to IAP in store builds) |

Physical goods stay on our own Stripe even inside store apps (Apple/Google only
tax digital goods). The postcard is therefore the margin anchor everywhere.

---

## Premium tier: "The Grimoire" ($4.99 one-time)

Free stays generous — forge, all current palettes, chaos, SVG/PNG export, the
Invocation Guide, The Working. The free toy is the marketing.

Paid unlocks, in build order:

1. **Servitor Builder** (centerpiece — prototypes already exist in repo)
   - Charter worksheet as a guided form (`servitor-framework.md` → UI)
   - Form/appearance generator (`servitor-form-prototype.html`, finished)
   - Seal generation wired to the forge (`?phrase=` hand-off already works)
   - Feed-cadence reminders via calendar file (.ics download — no backend)
   - Birth / feed / retire ritual scripts inline
2. **Sigil Library** — save, name, and revisit sigils (localStorage; no accounts)
3. **Animated export** — the draw animation as a shareable WebM/GIF
4. **Print-quality PDF export** — 300dpi with bleed, for home framing
5. **Effect inks** — premium stroke styles the free custom-color picker can't
   replicate (flat colors are already free, so premium must be *effects*):
   Gold Leaf, Ember, Holographic, Starfield, Blood Ritual, UV Glow, Smoke,
   Verdigris. Built like the existing Glitter mode (gradient stroke + particle
   layer). Glitter itself stays free as the teaser for the category. Effect
   inks also carry onto the mailed postcard, upgrading the $8 product.

### Gating without accounts
- Web: Stripe Checkout → server issues a signed unlock code (stored in
  Supabase keyed to email) → code entered on site → localStorage flag.
  "Restore" = re-enter code. No passwords, no accounts.
- App stores: same features behind native IAP; platform handles restore.
- The servitor pages ship as new files (`servitor.html`) — remove the two
  prototype files from the public repo when the real one ships.

---

## App plan (Capacitor wrap)

**Do not start until triggered** (see sequencing). The web PWA already covers
install-to-home-screen for the motivated.

- **Wrapper:** Capacitor, one codebase, the existing three pages + servitor page.
  App id `com.coeus.sigilforge`. Icons exist (512px); need splash screens.
- **Native touches** (required to pass Apple's "more than a website" bar):
  haptics on forge/draw-complete (plugin covers iOS), native share sheet for
  exports, save-to-photos, offline mode (already done via service worker).
- **Payments in-app:** Grimoire via IAP (RevenueCat recommended — one API for
  both stores, free tier suffices). Postcard stays on Stripe (physical). Tip
  jar removed from store builds.
- **Costs:** Apple $99/yr + Google $25 once. Review prep: privacy policy page,
  support email, 13+ age rating, "entertainment purposes" disclaimer.
- **Order of stores:** Google Play first (cheap, fast review, catches issues),
  then Apple.

---

## Sequencing — triggers, not dates

| Milestone | Trigger | Work |
|-----------|---------|------|
| 1. Grimoire on web | now / whenever ready | Servitor Builder + library + unlock-code flow |
| 2. Polish pass | with milestone 1 | privacy page, disclaimer footer, accessibility, domain |
| 3. Marketing revisit | Grimoire live | Etsy listing + SEO pass (lowest-effort lanes) |
| 4. Google Play app | ~25 organic sales/mo OR 1k visitors/mo | Capacitor + IAP |
| 5. Apple App Store | Play version stable + selling | same build + StoreKit review prep |

Rationale: premium features first (they work on the web today, no fees, no
review), app stores only after demand is proven — $99/yr against zero traffic
is donation, not distribution.

---

## Open decisions

- [ ] Grimoire price: $4.99 assumed — could test $2.99 / $6.99
- [ ] Domain (sigilforge.app etc.) — buy before marketing revisit
- [ ] Mixtape price: $5 is thin (~$1–2 net); consider $8 to match sigil card
- [ ] Servitor prototypes: stay public until real feature ships, or pull now?
- [ ] og:image URL — confirm actual Vercel URL and update meta tags
