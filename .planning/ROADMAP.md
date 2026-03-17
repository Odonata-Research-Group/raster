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

## Milestone 5 — Fix, export, measure ✓
- [x] GIF encoder fixed — blob worker URL resolves CORS block on gif.worker.js
- [x] SVG export — rect-per-pixel at dithered resolution, respects ink/paper colours, resolution warning, works in Figma/Illustrator
- [x] Favicon — user-supplied image, circle-clipped at runtime, injected as PNG data URI
- [x] Plausible analytics — page views + PNG / JPG / GIF / SVG / Image Upload / Camera Used / Preset Used / Palette Colour Added, eight goals configured

---

## Milestone 6 — Mobile zoom ✓
- [x] Canvas pinch-to-zoom — canvas area only, sidebar unaffected
- [x] Single-finger pan when zoomed in
- [x] Double-tap to reset to 1× (100%)
- [x] Zoom range: 0.5× (50%) to 8× (800%), steps of 25%
- [x] Zoom indicator — `− 100% +` widget, bottom-right of canvas, always visible when image loaded
- [x] About modal body text fixed — readable in both light and dark mode
- [x] Theme toggle label — consistent size with param labels on mobile

---

## Milestone 7 — Presets ✓
- [x] 5 named one-tap presets: Newsprint, Zine, Glitch, Lo-Fi, Raw
- [x] Positioned below Input, above Effect — follows workflow order
- [x] Active state clears on any manual slider adjustment
- [x] Each preset defines its own ink/paper colours — resets palette to 2-colour pair on apply

---

## Milestone 8 — Polish + new algorithms ✓
- [x] Collapsible sidebar sections — `+` / `−` per group, state persists via localStorage, all open by default
- [x] Jarvis-Judice-Ninke error diffusion
- [x] Stucki error diffusion
- [x] Ostromoukhov variable-weight error diffusion
- [x] True AM Halftone — rotated dot grid, luminance-driven dot radius
- [x] Dot Size + Screen Angle controls — param-disabled when pattern ≠ Halftone

---

## Milestone 9 — N-colour palette dithering ✓
- [x] Engine upgraded from binary ink/paper snap to N-colour RGB vector error propagation
- [x] All 5 error diffusion algorithms unified into single RGB pass
- [x] Ordered dither (Bayer, Noise, Halftone) use luminance-mapped palette snap
- [x] 2-colour output identical to previous — no regression
- [x] Dynamic palette UI — 2 swatches default, `+` adds up to 5, `×` removes (minimum 2)
- [x] Desktop hover reveal / mobile tap-to-select for remove affordance
- [x] Hex readout below swatch row
- [x] SVG export updated — one `<g>` per ink slot, last slot = background rect
- [x] Background colour control renamed from "Canvas" to "Paper" — correct mental model
- [x] Invert fix — redundant palette inversion removed; pixel pre-processing in `render()` is now the sole invert path; correct for all 10 patterns at all palette sizes

---

## Milestone 10 — Animate ✓
- [x] ANIMATE section in sidebar — collapsible, below EXPORT
- [x] Frame shelf — 3×5 grid, 15 slots maximum; empty slots dashed; filled slots show thumbnail pixel preview
- [x] Add Still — captures current canvas `ImageData`, appends to shelf; disabled when no image loaded
- [x] Remove frame — `×` badge top-right; hover to reveal (desktop), tap-select (mobile)
- [x] Clear — removes all frames, resets shelf
- [x] Speed: segmented control — Slow (4fps) / Med (8fps) / Fast (12fps)
- [x] Loop: segmented control — Loop / Ping-Pong (ping-pong excludes endpoints to avoid double-frame stutter)
- [x] Preview — plays sequence on canvas via `setInterval`; no encoding; button toggles ▶ / ■
- [x] Stop restores current render
- [x] Export GIF — encodes via gif.js; passes 2D context to `gif.addFrame()` to avoid silent worker failure; mismatched frame dimensions scaled to first frame
- [x] Export GIF disabled below 2 frames
- [x] Plausible events: `Still Captured`, `Download GIF Animated`

---

## Milestone 11 — Perceptual colour (next)
- [ ] LAB/HSL colour-accurate error calculation — replace RGB Euclidean distance with perceptual colour space distance function
- [ ] Engine-only change — no UI additions

---

## Milestone 12 — Share + expand
- [ ] Gallery / settings share — export image with settings baked in, or URL-encoded state for sharing exact recipes
- [ ] MP4 export — WebCodecs API + mp4-muxer, H.264 output, Instagram compatible
- [ ] Colour output mode selector (Mono / Tonal / Palette / RGB / Original)
- [ ] Palette extraction from image
- [ ] Side-by-side before/after view
- [ ] Landing page

---

## Milestone 13 — Platform
- [ ] Blue noise dithering
- [ ] Line screen / horizontal scan pattern
- [ ] Second effect (ASCII or halftone as standalone)
- [ ] Effect combinator
- [ ] Canvas zoom — pixel-perfect inspection (desktop)
- [ ] Instagram growth tracking

---

## Out of scope (forever)
- User accounts
- Server-side image storage
- Monetisation
- Camera roll export — platform restriction, not possible from browser
- Post-processing (CRT, Bloom, Phosphor) — wrong aesthetic
- Frameworks unless genuinely necessary