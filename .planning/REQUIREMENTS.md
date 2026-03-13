# Floyd Steinberg — REQUIREMENTS.md

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

---

## V2 (Shipped)

### Dither — new algorithms
- [x] Floyd-Steinberg error diffusion
- [x] Atkinson dithering

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

## V2.3 (Shipped)

### Brand & naming
- [x] Renamed from Raster to Floyd Steinberg
- [x] Instagram handle secured: @floydsteinberg
- [x] Primary domain: floydsteinberg.art (purchased, DNS live)
- [x] Redirect domain: floydsteinberg.app (purchased)
- [x] Wordmark, title tag, status bar, download filenames updated throughout

### Controls
- [x] Brightness slider (-100 to +100)
- [x] Blur slider (0–10px, pre-dither)
- [x] Pixelate slider (1–20, pre-dither)
- [x] Scatter slider (0–5, ordered dither jitter)

### Export
- [x] TXT (ASCII) export removed
- [x] GIF export added — still mode and 3-second camera capture mode

### Content
- [x] About modal copy — final content, tells the real story of Floyd and Steinberg
- [x] Follow link updated to instagram.com/floydsteinberg

### UI
- [x] Footer link arrows — all three use → (straight arrow)
- [x] Status bar empty state — "Error diffusion since 1976" replaces "No image"
- [x] Status bar active state — effect info only shown when image is loaded

---

## V3

### UI
- [ ] Canvas zoom — pixel-perfect inspection of dithered output

### Export
- [ ] SVG export
- [ ] MP4 export (MediaRecorder API)

### Colour
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)

### Analytics
- [ ] Umami installed (page views, PNG / GIF download events)
- [ ] Goal: measure Instagram → floydsteinberg.art → download funnel

---

## Backlog (unscheduled)

- Mobile optimisation
- Blue noise dithering
- Line screen / horizontal scan pattern
- Vertical bar dither pattern
- Canvas zoom — pixel-perfect inspection
- Preset saves / named looks
- Side-by-side before/after view
- Second effect (ASCII or halftone as standalone)
- Effect combinator
- HTML export

---

## Out of scope (forever)
- User accounts
- Saving/storing images server-side
- Monetisation
- Post-processing effects (CRT, Phosphor, Bloom, Scanlines) — wrong aesthetic for ORG
- Chromatic aberration controls — wrong aesthetic for ORG