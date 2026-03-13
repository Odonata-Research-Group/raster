# Raster — ROADMAP.md

## Milestone 1 — Ship ✓
- [x] Project scaffold
- [x] GitHub repo + Vercel deployment
- [x] Live at raster-khaki.vercel.app
- [x] Bitmap effect (Bayer 2×2, 4×4, 8×8, Halftone, Noise)
- [x] Image upload, drag+drop, paste, clipboard
- [x] Camera input with real-time dither
- [x] PNG + JPG + TXT export
- [x] PROJECT.md + REQUIREMENTS.md + DECISIONS.md + ROADMAP.md

---

## Milestone 2 — Deepen the dither ✓
- [x] Floyd-Steinberg error diffusion
- [x] Atkinson dithering
- [x] Blue noise dithering
- [x] Line screen / horizontal scan
- [x] Vertical bar dither
- [x] GIF export (animated, from camera frames)
- [x] Umami analytics installed
- [x] Custom domain

---

## Milestone 3 — Colour + polish (in progress)
- [x] Light / dark mode — full UI inversion
- [x] Ink / Paper colour controls — two-colour dither output
- [x] Typography hierarchy — 300 / 400 / 500 weight system
- [x] About modal + sidebar footer links (About · Follow · GitHub)
- [ ] About modal — final content pass
- [ ] Follow link — Instagram handle (pending)
- [ ] Footer arrow consistency — all three use →
- [ ] UX analysis — friction points, quick wins, prioritised backlog
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)
- [ ] Canvas zoom — pixel-perfect inspection
- [ ] MP4 export (MediaRecorder API)
- [ ] SVG export

---

## Milestone 4 — Expand
- [ ] Second effect (ASCII or halftone as standalone)
- [ ] Effect combinator
- [ ] Instagram growth tracking
- [ ] Preset saves / named looks
- [ ] Side-by-side before/after view

---

## Out of scope (forever)
- User accounts
- Server-side image storage
- Monetisation
- Post-processing (CRT, Bloom, Phosphor) — wrong aesthetic
- Frameworks unless genuinely necessary