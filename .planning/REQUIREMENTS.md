# Raster — REQUIREMENTS.md

## V1 (Shipped)

### Input
- [x] Image upload (drag + drop or file picker)
- [x] Paste from clipboard
- [x] Live camera feed with real-time dither

### Effect — Bitmap/Dither
- [x] Real-time canvas preview
- [x] Bayer 2×2, 4×4, 8×8 ordered dither
- [x] Halftone pattern
- [x] Noise pattern
- [x] Scale slider (pixel block size)
- [x] Threshold slider
- [x] Contrast slider
- [x] Invert toggle

### Export
- [x] Download as PNG
- [x] Download as JPG
- [x] Download as TXT (ASCII)

### Constraints
- [x] Single HTML file + effects/ folder
- [x] No frameworks, no build step
- [x] No login, no backend
- [x] Works on mobile (camera feature)

---

## V2 (Shipped)

### Dither — new algorithms
- [x] Floyd-Steinberg error diffusion
- [x] Atkinson dithering
- [x] Blue noise dithering
- [x] Line screen / horizontal scan
- [x] Vertical bar dither

### Export
- [x] GIF export (animated, from camera frames)

### Analytics
- [x] Umami installed (page views, PNG / GIF / TXT download events)
- [x] Custom domain

---

## V2.2 (Shipped)

### Colour
- [x] Ink / Paper colour controls — two hex inputs, live re-render
- [x] Works across all dither patterns automatically
- [x] Defaults to #ffffff / #000000 — no regression on existing output

### UI
- [x] Light / dark mode toggle in header
- [x] Typography hierarchy — section headers 500 weight, control labels 300 weight
- [x] About modal — opens from sidebar footer, closes via ✕ / overlay / Escape
- [x] Sidebar footer — About · Follow · GitHub links
- [x] Export buttons more prominent (border-color: var(--mid))
- [x] Effect label simplified (was "Effect — Bitmap")

---

## V2.3 (Current sprint)

### Content
- [ ] About modal copy — final content pass by Nick
- [ ] Follow link — update href once Instagram handle confirmed

### UI
- [ ] Footer link arrow consistency — all three use → (straight arrow)

### Analysis
- [ ] Structured UX analysis — friction points, missing features, quick wins
- [ ] Output: prioritised improvement list with effort estimates

---

## V3

### UI
- [ ] Canvas zoom — pixel-perfect inspection of dithered output

### Colour
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)

### Export
- [ ] MP4 export (MediaRecorder API)
- [ ] SVG export

---

## Backlog (unscheduled)

- Preset saves / named looks
- Side-by-side before/after view
- Second effect (ASCII or halftone as standalone effect)
- Effect combinator
- HTML export
- Mobile optimisation

---

## Out of scope (forever)
- User accounts
- Saving/storing images server-side
- Monetisation
- Post-processing effects (CRT, Phosphor, Bloom, Scanlines) — wrong aesthetic for ORG
- Chromatic aberration controls — wrong aesthetic for ORG