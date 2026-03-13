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

## V2 (Current sprint)

### Dither — new algorithms
- [x] Floyd-Steinberg error diffusion
- [x] Atkinson dithering
- [ ] Blue noise dithering
- [ ] Line screen / horizontal scan
- [ ] Vertical bar dither

### Export
- [ ] GIF export (animated, from camera frames)

### Analytics
- [ ] Umami installed (page views, PNG / GIF / TXT download events)
- [ ] Custom domain

---

## V3

### UI
- [ ] Light / dark mode toggle — full inversion (black UI + white output ↔ white UI + black output)
- [ ] Canvas zoom — pixel-perfect inspection of dithered output

### Colour
- [ ] Colour output mode — Mode selector (Mono / Tonal / Original)

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

---

## Out of scope (forever)
- User accounts
- Saving/storing images server-side
- Monetisation
- Post-processing effects (CRT, Phosphor, Bloom, Scanlines) — wrong aesthetic for ORG
- Chromatic aberration controls — wrong aesthetic for ORG