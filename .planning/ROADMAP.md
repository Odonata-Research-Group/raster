# Floyd Steinberg — ROADMAP.md

## Milestone 1 — Ship ✓
- [x] Project scaffold
- [x] GitHub repo + Vercel deployment
- [x] Bitmap effect (Bayer 2×2, 4×4, 8×8, Halftone, Noise)
- [x] Image upload, drag+drop, paste, clipboard
- [x] Camera input with real-time dither
- [x] PNG + JPG + TXT export
- [x] PROJECT.md + REQUIREMENTS.md + DECISIONS.md + ROADMAP.md

---

## Milestone 2 — Deepen the dither ✓
- [x] Floyd-Steinberg error diffusion
- [x] Atkinson dithering
- [x] GIF export (still + 3-second camera capture)
- [x] Light / dark mode — full UI inversion
- [x] Ink / Paper colour controls — two-colour dither output
- [x] Typography hierarchy — 300 / 400 / 500 weight system
- [x] About modal + sidebar footer links (About · Follow · GitHub)

---

## Milestone 3 — Brand + controls ✓
- [x] Renamed to Floyd Steinberg
- [x] Instagram handle secured: @floydsteinberg
- [x] Primary domain: floydsteinberg.art (live)
- [x] Redirect domain: floydsteinberg.app
- [x] About modal — final content (real story of Floyd + Steinberg)
- [x] Follow link → instagram.com/floydsteinberg
- [x] Footer arrows — all three use →
- [x] Status bar empty state — "Error diffusion since 1976"
- [x] TXT export removed
- [x] Brightness, Blur, Pixelate, Scatter sliders added

---

## Milestone 4 — Mobile + polish ✓
- [x] Mobile layout — canvas locked top 50vh, sidebar scrolls below
- [x] `100dvh` fix — status bar visible on all mobile browsers
- [x] Mobile typography pass — all labels legible at phone distance
- [x] Mobile touch targets — 44px buttons, 20×20px slider thumbs
- [x] Export button hierarchy — ghost when disabled, solid when enabled
- [x] Sidebar background — #111111 dark / #f5f5f5 light (canvas vs tool zone)
- [x] Export button light mode — solid black when enabled, ghost when disabled

---

## Milestone 5 — Fix, export, measure (next)
- [ ] GIF encoder fix — broken on desktop and mobile (CORS / worker issue suspected)
- [ ] SVG export — dithered canvas to SVG rects, respects ink/paper colours
- [ ] Favicon — dithered bitmap mark, 32×32px
- [ ] Umami analytics — page views + PNG / JPG / GIF / SVG download events
- [ ] Canvas pinch-to-zoom on mobile — canvas only, sidebar unaffected

---

## Milestone 6 — Expand the tool
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)
- [ ] Blue noise dithering
- [ ] Line screen / horizontal scan pattern
- [ ] Second effect (ASCII or halftone as standalone)
- [ ] MP4 export (MediaRecorder API)
- [ ] Canvas zoom — pixel-perfect inspection (desktop)

---

## Milestone 7 — Platform
- [ ] Effect combinator
- [ ] Preset saves / named looks
- [ ] Side-by-side before/after view
- [ ] Instagram growth tracking

---

## Out of scope (forever)
- User accounts
- Server-side image storage
- Monetisation
- Camera roll export — platform restriction, not possible from browser
- Post-processing (CRT, Bloom, Phosphor) — wrong aesthetic
- Frameworks unless genuinely necessary