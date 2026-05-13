# Nil Pansiyon v2 — Handoff (Session 4 → Session 5)

**Tarih:** 2026-05-13 · **Branch:** `main` · **Latest commit:** `4506505`
**Live:** https://ozzaii.github.io/nilpansiyon-v2/ (CNAME hazır: `nilpansiyon.info` — DNS taşınınca otomatik geçer)
**Repo:** https://github.com/ozzaii/nilpansiyon-v2

---

## Mission (next session)

Kaan'ın bir sonraki seans için verdiği hedef listesi — **müzelik kalitede, mobile-first, custom animations + reveals**. "Cleaner, leaner, way better design." Goal-loop: her round'da test → fix → re-test, hedef vurulana kadar dönsün.

1. **Cleaner + leaner** — 5932 satırlık tek dosyayı oku, dead code purge et, CSS gruplaması netleştir. Tipografi rhythm pass (font-size scale ratio'ları, leading, tracking). Whitespace disiplini — section padding ritmi tutarlı mı?
2. **Room videos watchable with playback** — şu an `r1/r2/r3` kartlarında **hover'da** background video oynuyor. **Mobilde hover yok → mobil kullanıcı hiç göremiyor.** İki yaklaşım:
   - **A (recommended):** Tap-to-open fullscreen lightbox — `<video controls playsinline autoplay loop>` + ESC/backdrop close + scroll-lock
   - **B:** Inline autoplay muted loop on mobile (gate behind ilk tap because of 15.5 MB total data)
3. **Agent-driven translations (AR + RU)** — TR/EN halihazırda `data-i18n` ile çalışıyor (`tr`/`en` `data-i18n-{tr,en}`). **AR + RU "soon" işaretli.** Tek tek `data-i18n` key'leri için **gerçek profesyonel hospitality tone Arapça + Rusça** üret. RTL Arabic için `body.rtl` class toggle (`direction: rtl`). Subagent kullan — emlak/lüks otel terminolojisi öğrencisi değil, native.
4. **Horizontal scroll fix** — Kaan mobilde sağa kaydırma şikayeti. `html { overflow-x: clip }` mevcut ama içeride taşma var. Audit gerekli:
   - `.awards .marquee` infinite scroll — taşıyor olabilir
   - `width: 100vw` kullanan element varsa scrollbar genişliği taşmayı yapar → `width: 100%` + padding kullan
   - Negative margins
   - `.testimonials` scroll-snap (bilinçli, OK ama mobile padding/inset tut)
5. **Way better design + custom animations + reveals** — yeni vurucu hareketler:
   - Hero "nil pansiyon" letter-split daha karakterli (italic axes opsz/SOFT/WONK live oynat)
   - Section reveal'ları unique olsun — şu an çoğu translate+fade. Her bölüme **kendine özgü** bir reveal: Hikâye'de drop-cap üzerinde brass akış, Konum'da harita ladin tek tek yer alır, Defter'de testimonials kart yerlerini editorial-rotate ile alır
   - Odalar grid mobilde stack ritmik mi?
   - Sofra menu hover micro-interactions (item italic glow, tag pulse)
   - Konum SVG harita mobilde okunaklı mı?
6. **60 FPS locked** — Chrome DevTools Performance tab kullan. Şu an yoğun olan yerler:
   - Falling spruce needles canvas (hero)
   - Weather particles canvas (rain/snow/mist/storm modes)
   - Cursor lerp + magnetic + 3D card tilt
   - Hero 4-photo cross-fade
   - **Compositor-only kural:** sadece `transform` ve `opacity` animate et. `width/height/top/left/margin` = layout thrash = jank.
   - `will-change` sadece animate olan node'lara, sonra temizle
   - Reduce paint area: küçük rotating brass dot vs full-section gradient shift
7. **Mobile-first recursive loop** — **primary target: iPhone 13/14/15 portrait (390×844).** Loop:
   1. Chrome DevTools mobile emulator
   2. Her section'a scroll → overflow / tap target / font-size / padding kontrol
   3. Lighthouse mobile audit (perf/a11y/SEO 90+ hedef)
   4. Fix → reload → re-test
   5. Her round Kaan'a screenshot, geribildirim al
   6. Hedef vurulana kadar döngü kapanmasın

---

## Mevcut durum (Session 4 sonu)

### ✅ Tamamlandı (commit list)
- `bdabb14` initial 11-bölüm yapısı
- `227e97e` hero rebuild (single italic centered title)
- `be5e2f8` SEO + a11y + ambient sound + ink-wash + 404
- `b75f7ff` real logo wired + CNAME
- `4506505` paths fix (absolute → relative for GH Pages)

### 🎨 Brand
- Logo: `assets/img/logo-icon.png` (N+tree shield, 256px transparent) + `@2x.png` (512) + `logo-mark.png` (full lockup) + multi-size favicons (96/192/512)
- Top nav: real logo + brass shimmer sweep every 7s (mask + animated gradient + mix-blend screen)
- Boot screen: logo crest scale .6→1 with blur, then 2.6s shimmer pass
- Footer: full lockup with reveal-on-intersect + 2.8s sweep, `brightness(1.85) saturate(1.32) contrast(1.05)` to pop on dark

### 🔧 Infrastructure
- SEO: 15+ meta tags (og:type, twitter:card, geo coords, hreflang tr/en, canonical, apple-touch, business contact data)
- JSON-LD `@graph`: LodgingBusiness (full address, geo, 6 HotelRoom offers, amenities, aggregateRating 4.9/287, ReserveAction → WhatsApp), WebSite, BreadcrumbList
- `robots.txt` + `sitemap.xml` (with hreflang xhtml:link alternates)
- `.nojekyll` for clean GH Pages serving
- `CNAME` = `nilpansiyon.info`
- All asset paths relative (works on both `ozzaii.github.io/nilpansiyon-v2/` and `nilpansiyon.info/`)

### 🎭 Atmosphere
- **Live weather** — Open-Meteo API (40.6201, 40.2822), `body[data-weather]` drives tint + particle mode (rain/snow/mist/storm), chip auto-hide on scroll
- **Ambient sound** — bottom-left brass speaker icon, WebAudio synth (no asset files): pink-filtered stream (BP 600-1200 + LFO), low-pass wind (380 + slow LFO), sub rumble 55Hz, sparse FM bird chirps every 6-14s. Master fade in 1.4s / out 0.8s. localStorage preference.
- **Easter egg** — hero crest triple-click within 1.4s → vintage postkart overlay
- **Paper grain** — SVG fractal noise overlay on sofra/hikaye/konum/defter/mevsimler
- **Reading progress** — brass hairline top of viewport, scroll-driven width
- **Ink-wash dividers** — SVG fractal-noise displaced deckle-edge at section transitions

### ♿ A11y
- Skip-link "İçeriğe atla — Skip to content"
- Universal `:focus-visible` brass ring (offset 3-4px)
- Keyboard mode detector: Tab → `body.is-tabbing` → restores cursor, hides custom cursor
- `.sr-only` utility
- All images: `loading="lazy" decoding="async" width="1200" height="800"` (CLS prevention)

---

## Dosya yapısı

```
/Users/ozai/projects/nilpansiyon-v2/
├── index.html                       ← 5932 satır, tüm CSS+JS inline
├── 404.html                          ← bespoke 404, italic Fraunces zero pulse
├── CNAME                              ← nilpansiyon.info
├── manifest.webmanifest               ← PWA manifest
├── robots.txt
├── sitemap.xml
├── .nojekyll
├── HANDOFF.md                         ← bu dosya
├── assets/
│   ├── img/
│   │   ├── hero-uzungol-kusbakisi.jpg    ← hero p1, p3
│   │   ├── otel-uzungol-genel-gorunum.jpg ← hero p2
│   │   ├── otel-dis-cephe-yesil.jpg       ← hero p4, hikaye main photo
│   │   ├── hero-balkon-{dag,koy}-manzara.jpg
│   │   ├── deluxe-cift-kisilik-oda.jpg    ← Oda I (Deluxe)
│   │   ├── family-bungalov-mutfak-salon.jpg ← Oda II (2+1)
│   │   ├── family-bungalov-oturma-alani.jpg ← Oda III (1+1)
│   │   ├── superior-ikiz-yatak-oda.jpg    ← Oda IV
│   │   ├── family-bungalov-salon-alternatif.jpg ← Oda V
│   │   ├── standard-cift-kisilik-oda.jpg  ← Oda VI
│   │   ├── banyo-*.jpg, family-bungalov-{giris,mutfak-detay}.jpg
│   │   ├── logo.png                       ← 512px transparent
│   │   ├── logo-icon{,@2x,-192,-96}.png  ← N+tree shield variants
│   │   └── logo-mark{,@2x}.png            ← full lockup
│   └── video/
│       ├── deluxe-room-tour.mp4         ← 3.9 MB — Oda I
│       ├── 2plus1-apartment-tour.mp4    ← 7.3 MB — Oda II
│       └── 1plus1-mountain-view.mp4     ← 4.3 MB — Oda III
└── _reference/                          ← gitignore'd, eski v1
```

---

## Operating instructions

### Local dev
```bash
cd /Users/ozai/projects/nilpansiyon-v2
python3 -m http.server 4912 &
open http://localhost:4912/
```

### Deploy (GH Pages auto-deploys main)
```bash
git add <files>
git commit -m "..."
git push origin main
# wait 30-45s, GH Pages picks up
gh api repos/ozzaii/nilpansiyon-v2/pages/builds/latest --jq '{status,commit:.commit[:7]}'
```

### Path convention (CRITICAL)
- **Asset paths must be RELATIVE** (`assets/img/foo.jpg`, not `/assets/img/foo.jpg`)
  - Works on both `ozzaii.github.io/nilpansiyon-v2/` and final `nilpansiyon.info/`
- **SEO URLs must be ABSOLUTE** (canonical, og:url, twitter:image, JSON-LD use `https://nilpansiyon.info/...`)
  - These are indexing targets, not loading targets

### Visual verification
- Use Claude-in-Chrome MCP to **screenshot** after changes
- Test sections in order: hero → manifesto → odalar → sofra → hikaye → mevsimler → konum → defter → rezervasyon → footer
- Check console for errors after every reload
- **Mobile audit:** Chrome DevTools → toggle device toolbar → iPhone 14 Pro (390×844)
- Track FPS in Performance tab during scroll

---

## Architecture quick-ref

### CSS variables (top of `:root`)
```
--display:  Fraunces (italic, opsz+SOFT+WONK axes animated)
--display2: Cormorant Garamond
--body:     Spectral
--sans:     Bricolage Grotesque
--mono:     IBM Plex Mono
--ink:#07080A  --paper:#F5EEDC  --moss:#16201A  --brass:#C8A45C
```

### JS modules in `<script>` block (line 4329+)
- a11y keyboard detector (Tab → `.is-tabbing`)
- easter egg crest triple-click → postcard
- letter-split for `[data-letters]` and `.ch-head h2 em`
- 3D card tilt (rooms/seasons/testimonials)
- cursor-lens (`.data-lens` gets `--lx`, `--ly` vars)
- magnetic links (`data-magnet`, STRENGTH .35, RADIUS 140)
- shuffle counters (`data-count`)
- weather fetch → drives `body[data-weather]`
- weather particles canvas
- ambient sound WebAudio synth
- rezervasyon date picker + guest counter + room selector → WhatsApp deeplink (`https://wa.me/905453842829`)
- nav dots scroll-spy
- sticky booking bar visibility (hides WA fab when shown)

### i18n
- `data-i18n="key"` for text content
- `data-i18n-tr="..."` etc. for attribute-based overrides
- Lang switcher: TR/EN active, AR/RU `aria-disabled` ("soon")
- Selection persists in `localStorage`
- **Missing:** AR + RU content. RTL toggle for AR (add `body.rtl { direction: rtl }`).

---

## Known issues / pitfalls

1. **Mobile horizontal scroll** — Kaan reported. Find culprit (awards marquee, season-grid, 100vw usage).
2. **Room videos hover-only** — `r1/r2/r3` cards play video on `:hover`. Mobile has no hover → never visible. Fix to tap-to-open or always-on muted loop.
3. **Custom cursor** — desktop only (`@media (pointer: coarse)` removes). Touch fallback works.
4. **Boot screen** — auto-dismisses on page settle. Add timeout fallback if JS fails.
5. **`content-visibility: auto`** is on `defter, konum, rez, awards, foot, cevre` — perf win but check layout shift on mobile.
6. **Ambient sound** — requires user gesture (autoplay policy). Don't try to auto-start.
7. **Weather API** — no auth, ~10k req/day free. Fallback to mist mode wired in.
8. **Decorative images** — check `aria-hidden` + empty `alt=""` on lens/parallax layers.

---

## Quality bar

Kaan's target: **museum-grade luxury, mobile cinematic experience**.

| Dimension | Target |
|---|---|
| Lighthouse Perf (mobile) | 90+ |
| Lighthouse A11y | 95+ |
| Lighthouse SEO | 100 |
| FPS during scroll | 60 locked, never < 50 |
| Console errors | 0 |
| Mobile horizontal scroll | 0px overflow |
| Time to interactive (4G) | < 3s |
| First contentful paint | < 1.5s |
| Cumulative layout shift | < 0.05 |

### Visual checklist
- [ ] Hero loads <2s, weather chip + reading progress visible
- [ ] Each section reveal triggers exactly once
- [ ] Ink-wash dividers organic, not pixelated
- [ ] Top nav stays readable on all backgrounds (paper/dark/cream/moss)
- [ ] Boot screen dismisses smoothly without flash
- [ ] Postcard easter egg opens + closes cleanly
- [ ] Ambient toggle plays + stops, bars animate
- [ ] Footer lockup brass reads clearly
- [ ] 404 page links return home (relative `./`)
- [ ] Rezervasyon form opens calendar + counter + sends to WhatsApp
- [ ] **Room videos play on tap (mobile)**
- [ ] **AR locale flips body to RTL + Arabic content renders**
- [ ] **RU locale renders Russian content**

---

## Communication with Kaan

- "knk" or "Kaan"
- Casual, küfür OK, no praise-spam, direct
- TR/EN mix — match his tone
- Late nights — keep responses **terse**
- Show, don't tell — screenshots > explanations
- Verify with eyes before reporting done

---

## Next session start sequence

```bash
cd /Users/ozai/projects/nilpansiyon-v2
git status
git log --oneline -5

# start local
python3 -m http.server 4912 &

# check live build status
gh api repos/ozzaii/nilpansiyon-v2/pages/builds/latest --jq '{status,commit:.commit[:7]}'

# pull latest if stale
git pull origin main
```

Then open **Mission** section above. Recommended order (highest impact first):

1. **Room videos watchable on mobile** (#2) — primary target user can't see them at all
2. **Horizontal scroll fix** (#4) — confirmed mobile bug
3. **60 FPS lock** (#6) — measurable, mobile feels janky if missed
4. **Mobile recursive loop** (#7) — wrap the above in a tight goal-loop
5. **AR + RU translations** (#3) — agent-generated, RTL toggle
6. **Custom animations + reveals + design polish** (#5) — section-by-section
7. **Cleaner + leaner code** (#1) — refactor pass at the end

**Don't ship without testing on mobile.** Primary target. Goal-loop until quality bar hit.
