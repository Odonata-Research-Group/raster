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

## V2.4 (Shipped)

### Mobile layout
- [x] Canvas locked at top 50vh, sidebar scrolls below — canvas always in viewport
- [x] `100dvh` replaces `100vh` — status bar visible behind browser chrome on all devices
- [x] Breakpoint: `@media (max-width: 480px)` — CSS-only, no JS switching
- [x] Drop zone label: "TAP TO UPLOAD" on mobile, desktop label unchanged

### Mobile typography
- [x] Group labels: 10px → 13px
- [x] Param labels: 9px light → 12px regular
- [x] Param values, buttons, selects, status bar: bumped to 12–13px
- [x] Footer links: 9px → 11px
- [x] Footer link arrows always visible on mobile (no hover state on touch)

### Mobile touch targets
- [x] Button and select height: 36px → 44px
- [x] Slider thumbs: 10×10px → 20×20px
- [x] Toggle: 28×14px → 36×18px

### Mobile UX
- [x] Status bar right side hidden on mobile — avoids collision
- [x] Bottom padding: `env(safe-area-inset-bottom) + 80px` — footer links always reachable

### Export buttons
- [x] Disabled state: ghost button, no hover — matches all other inactive controls
- [x] Enabled state (dark mode): solid white (#ffffff), black text, 80% opacity on hover/tap
- [x] Enabled state (light mode): solid black (#000000), white text, 80% opacity on hover/tap
- [x] Specificity fix: `.btn.export-btn` — was being overridden by `.btn`

### Sidebar
- [x] Dark mode: `#111111` background — separates tool panel from pure black canvas
- [x] Light mode: `#f5f5f5` — subtle off-white panel, distinct from white canvas

---

## V2.5 (Next)

### Bug fixes
- [ ] GIF encoder — broken on desktop and mobile, needs console investigation and fix
  - Suspected: gif.worker.js CORS issue with CDN-loaded worker script

### Export
- [ ] SVG export — dithered canvas traced to SVG rects, respects ink/paper colours
- [ ] Favicon — dithered bitmap mark, 32×32px PNG, added to `<head>`

### Analytics
- [ ] Umami installed — script tag in `<head>` (Nick to set up account first)
- [ ] Custom events: PNG download, JPG download, GIF download, SVG download
- [ ] Goal: measure Instagram → floydsteinberg.art → download funnel

### Mobile
- [ ] Canvas pinch-to-zoom — canvas area only, sidebar unaffected, double-tap to reset

---

## V3

### Export
- [ ] MP4 export (MediaRecorder API)

### Colour
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)

### UI
- [ ] Side-by-side before/after view

---

## Backlog (unscheduled)

- Blue noise dithering
- Line screen / horizontal scan pattern
- Vertical bar dither pattern
- Canvas zoom — pixel-perfect inspection (desktop)
- Preset saves / named looks
- Second effect (ASCII or halftone as standalone)
- Effect combinator
- HTML export

---

## Out of scope (forever)
- User accounts
- Saving/storing images server-side
- Monetisation
- Camera roll export — platform restriction, not possible from browser
- Post-processing effects (CRT, Phosphor, Bloom, Scanlines) — wrong aesthetic for ORG
- Chromatic aberration controls — wrong aesthetic for ORG