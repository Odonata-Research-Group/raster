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

## V2.5 (Shipped)

### Bug fixes
- [x] GIF encoder fixed — gif.worker.js fetched as blob URL to resolve CORS block on CDN-loaded worker script

### Export
- [x] SVG export — rect-per-pixel at dithered resolution, respects ink/paper colours, resolution warning above 640k pixels, works in Figma/Illustrator
- [x] Favicon — user-supplied image, circle-clipped at runtime, injected as PNG data URI into `<head>`

### Analytics
- [x] Plausible installed — script tag in `<head>`, privacy-respecting, no cookies, GDPR compliant
- [x] Custom events: PNG download, JPG download, GIF download, SVG download, Image Upload, Camera Used, Preset Used, Palette Colour Added
- [x] Eight goals configured in Plausible dashboard
- [x] Goal: measure Instagram → floydsteinberg.art → download funnel

---

## V2.6 (Shipped)

### Canvas zoom
- [x] Pinch-to-zoom on canvas area only — sidebar completely unaffected
- [x] `touch-action: none` on `.canvas-wrap` — intercepts pointer events, prevents browser native zoom
- [x] Zoom is CSS transform only — never triggers re-render
- [x] Single-finger pan when zoomed in
- [x] Double-tap to reset to 1× (100%)
- [x] Zoom range: 0.5× (50%) to 8× (800%)
- [x] Step size: 0.25× (25%) per button tap

### Zoom indicator
- [x] `− 100% +` widget, bottom-right of canvas area, always visible when image loaded
- [x] `−` dims at 50% minimum, `+` dims at 800% maximum
- [x] Resets to 100% on double-tap and on clear

### Bug fixes
- [x] About modal body text — was `var(--mid)` (#555555), fixed to `var(--fg)` — readable in both modes
- [x] Theme toggle label — bumped to 12px on mobile, now consistent with param labels

---

## V2.7 (Shipped)

### Presets
- [x] 5 named one-tap presets — positioned below Input, above Effect
- [x] Preset group uses standard `.btn` style — no new UI patterns
- [x] Active state: `.active` class on selected preset, clears on any manual slider adjustment
- [x] Set: Newsprint, Zine, Glitch, Lo-Fi, Raw
- [x] Each preset defines its own ink/paper colours — resets palette to 2-colour pair on apply

---

## V2.8 (Shipped)

### UI
- [x] Collapsible sidebar sections — `+` / `−` toggle at far right of each group label
- [x] All sections open by default
- [x] Collapsed state persists via localStorage

---

## V2.9 (Shipped)

### Dither — new algorithms
- [x] Jarvis-Judice-Ninke error diffusion
- [x] Stucki error diffusion
- [x] Ostromoukhov variable-weight error diffusion

### Halftone
- [x] True AM Halftone — replaces old circular threshold, rotated dot grid, luminance-driven dot radius
- [x] Dot Size slider (2–20, default 6) — visible always, param-disabled when pattern ≠ Halftone
- [x] Screen Angle slider (0–90°, default 45°) — visible always, param-disabled when pattern ≠ Halftone

### Pattern dropdown order
- [x] Bayer 2×2, Bayer 4×4, Bayer 8×8, Halftone, Noise, Floyd-Steinberg, Atkinson, Jarvis-Judice-Ninke, Stucki, Ostromoukhov

---

## V2.10 (Shipped)

### Engine — N-colour palette dithering
- [x] `state.palette` array replaces `state.inkColor` / `state.paperColor` as source of truth
- [x] `inkColor` and `paperColor` kept as getter/setter aliases — backwards compatibility with presets, export, status bar
- [x] Error diffusion (all 5 algorithms): RGB vector error propagation, nearest palette colour by Euclidean distance
- [x] Ordered dither (Bayer, Noise, Halftone): luminance-mapped palette snap via `orderedSnap()`
- [x] 2-colour output identical to V2.9 — no regression

### Palette UI
- [x] Replaces fixed Ink / Paper rows in Colour section
- [x] Dynamic swatch row — 2 swatches default, `+` adds up to 5
- [x] `+` button: 20×20px dashed border, hidden at palette length 5
- [x] Remove affordance: 11×11px `×` badge top-right of each swatch
- [x] `×` hidden on last two swatches — minimum 2 enforced
- [x] Desktop: `×` revealed on swatch hover (CSS only)
- [x] Mobile: tap swatch to reveal `×`; tap outside to dismiss; 2-colour mode taps open picker directly
- [x] Mobile swatches: 20×20px → 28×28px
- [x] Hex readout: single line below row, colours joined by ` · `

### Export — SVG multi-colour
- [x] One `<g fill="...">` per palette slot (excluding last slot)
- [x] Last palette slot = background rect
- [x] Nearest-index lookup mirrors dither engine — SVG matches canvas output

---

## V2.10e (Shipped)

### UI
- [x] Background colour control in Colour group renamed from "Canvas" to "Paper"
- [x] Label only — no logic, no state, no behaviour changed

---

## V2.11 (Shipped)

### Bug fixes
- [x] Invert fix — removed redundant `maybeInvert()` from `dither()` and conditional canvas fill inversion from `render()`; pixel pre-processing in `render()` is now the sole invert path; correct for all 10 patterns at all palette sizes

### Animate — manual frame sequencer
- [x] ANIMATE section in sidebar — collapsible, below EXPORT, follows existing group pattern
- [x] Frame shelf — 3×5 grid, 15 slots maximum; empty slots dashed border; filled slots show thumbnail canvas preview
- [x] Thumbnail is actual pixel preview rendered from stored `ImageData` — not a colour block
- [x] Add Still — captures current canvas `ImageData`, appends to shelf; disabled when no image loaded
- [x] Remove frame — 11×11px `×` badge top-right of filled slot; hover to reveal (desktop); tap-select to reveal (mobile)
- [x] Clear — removes all frames, resets shelf
- [x] Speed: segmented control — Slow (4fps) / Med (8fps, default) / Fast (12fps)
- [x] Loop: segmented control — Loop / Ping-Pong
- [x] Ping-pong excludes first and last frames from the reversed segment — no double-frame stutter at endpoints
- [x] Preview — plays frame sequence on canvas via `setInterval` at selected FPS; no encoding; button toggles to ■ Stop
- [x] Stop — clears interval, restores current render
- [x] Export GIF — encodes via existing gif.js pipeline; passes 2D context to `gif.addFrame()` (not canvas element) to avoid silent worker failure; frames with differing dimensions scaled to match first frame
- [x] Export GIF disabled below 2 frames
- [x] Plausible events: `Still Captured` on capture, `Download GIF Animated` on export

---

## V3

### Export
- [ ] MP4 export — WebCodecs API (VideoEncoder) + mp4-muxer, outputs H.264 MP4 compatible with Instagram
- [ ] Gallery / settings share — export image with current settings baked in, or URL-encoded state for sharing exact recipes

### Colour
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)
- [ ] Palette extraction from image

### UI
- [ ] Side-by-side before/after view
- [ ] Landing page

---

## Backlog (unscheduled)

- Blue noise dithering
- Line screen / horizontal scan pattern
- Vertical bar dither pattern
- Canvas zoom — pixel-perfect inspection (desktop)
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