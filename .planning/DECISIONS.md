# Floyd Steinberg — DECISIONS.md

## Naming & Brand (V2.3, shipped)
- Renamed from Raster to Floyd Steinberg
- Named after Robert W. Floyd and Louis Steinberg, authors of the 1976 error diffusion algorithm
- Rationale: the algorithm runs inside the tool, the name has lore, it's unexpected and memorable
- Instagram handle: @floydsteinberg
- Primary domain: floydsteinberg.art — .art chosen over .app/.io as more appropriate for a creative tool
- Redirect domain: floydsteinberg.app — purchased to protect the name
- Both domains purchased via Porkbun, DNS pointed to Vercel

## Architecture
- Single index.html shell — UI, canvas, controls
- Each effect is a self-contained JS file in /effects/
- New effects drop in without touching core tool
- No frameworks — vanilla JS + Canvas API
- No build step — what you see is what deploys

## Effect V1: Bitmap/Dither (shipped)
- Ordered dither via Bayer matrices (2×2, 4×4, 8×8)
- Halftone pattern (circular dot threshold)
- Noise pattern (random threshold per pixel)
- Parameters: Scale, Threshold, Contrast, Invert toggle
- Scale = pixel block size (pre-downsample factor, then pixelated upscale)

## Effect V2: Dither — new algorithms (shipped)
- Floyd-Steinberg error diffusion — first new pattern
- Rationale: fundamentally different algorithm from Bayer (error propagation vs matrix lookup), produces organic edges, high ORG aesthetic fit
- Atkinson dithering — 6-neighbour, 3/4 total error propagation, harder edges than Floyd-Steinberg
- Scale on Floyd-Steinberg and Atkinson = pre-downsample factor, consistent with Bayer behaviour
- All new patterns share existing controls: Scale, Threshold, Contrast, Invert — no new UI per pattern
- Patterns drop into existing select dropdown without touching core

## New sliders (V2.3, shipped)
- Brightness (-100 to +100, default 0) — applied as pixel-level offset before dithering
- Blur (0–10px, default 0) — CSS filter blur applied to offscreen canvas before dithering; softens pattern edges, creates atmospheric output
- Pixelate (1–20, default 1) — downsamples to block grid before dithering; produces chunky mosaic + dither layered look
- Scatter (0–5, default 0) — jitters the sample position in ordered dither patterns; breaks rigid Bayer grid, more organic feel
- Pre-processing order: pixelate → blur → brightness → dither
- Blur and pixelate are mutually exclusive in the pipeline — pixelate takes precedence when > 1

## Colour output — Ink / Paper (V2.2, shipped)
- Two hex inputs: Ink (foreground, default #ffffff) and Paper (background, default #000000)
- Labelled "Ink / Paper" — fits the darkroom/print aesthetic
- Colour applied at pixel write step in dither() — replaces hardcoded 255/0 values
- Works across all patterns automatically — no per-pattern logic
- Invert toggle continues to work — swaps which pixels get Ink vs Paper
- Defaults match original black/white output exactly — no regression
- Mode selector (Mono / Tonal / Palette / RGB / Original) — still V3, not this session

## Light / Dark mode (V2.2, shipped)
- CSS variable swap on html element — single class toggle, no JS logic
- Dark default: `--bg: #000000`, `--fg: #ffffff`
- Light mode: `--bg: #ffffff`, `--fg: #000000`
- Theme toggle in header — label updates between "Light" and "Dark"

## Mobile layout (V2.4, shipped)
- Breakpoint: `@media (max-width: 480px)`
- Layout decision: canvas locked at top 50vh, sidebar scrolls below — canvas always in viewport regardless of scroll position
- Rationale: tool feedback is immediate — user adjusts controls and sees result without scrolling back up
- `main` switches from `grid-template-columns: 1fr 200px` to `grid-template-rows: 50vh 1fr`
- Canvas gets `border-bottom` instead of `border-right` on mobile
- `100dvh` replaces `100vh` on mobile — dynamic viewport height accounts for browser chrome so status bar is always visible
- CSS-only solution — no JS layout switching

## Mobile typography (V2.4, shipped)
- All type sizes bumped within `@media (max-width: 480px)` — no changes to desktop
- Group labels: 10px → 13px
- Param labels: 9px light → 12px regular (weight bump from 300 to 400)
- Param values: 11px → 13px
- Buttons and selects: 10px → 12px
- Status bar: 9px → 12px
- Footer links: 9px → 11px
- Toggle labels: 9px light → 12px regular
- Theme toggle: 10px → 12px (V2.6 fix — was visibly smaller than param labels on mobile)
- Rationale: 9px at arm's length on a phone is not legible — minimum comfortable reading size on mobile is 12px

## Mobile touch targets (V2.4, shipped)
- `--control-h` bumped from 36px to 44px on mobile (buttons, selects)
- Slider thumbs: 10×10px → 20×20px
- Toggle: 28×14px → 36×18px
- Apple HIG minimum touch target is 44px — applied throughout

## Mobile UX details (V2.4, shipped)
- Drop zone label: "DROP IMAGE / CLICK TO UPLOAD" on desktop, "TAP TO UPLOAD" on mobile — implemented as two elements, CSS toggles visibility
- Status bar right side (live badge, domain) hidden on mobile — avoids collision with dims/effect text
- Footer link arrows always visible on mobile — hover state doesn't exist on touch
- Bottom padding: `env(safe-area-inset-bottom) + 80px` — clears iOS home indicator and browser chrome so footer links are always reachable

## Export buttons (V2.4, shipped)
- Hierarchy decision: ghost buttons for all inputs and controls, solid buttons for export actions — output is the primary action
- Dark mode: disabled = ghost (transparent, `var(--border)` stroke, no hover), enabled = solid `#ffffff` with black text, hover = `rgba(255,255,255,0.8)`
- Light mode: disabled = ghost (transparent, `var(--border)` stroke), enabled = solid `#000000` with white text, hover = `rgba(0,0,0,0.8)`
- `opacity: 1` override on both states — prevents base `.btn:disabled { opacity: 0.3 }` from making disabled state look broken rather than intentional
- Specificity fix: `.btn.export-btn` — `.export-btn` alone was being overridden by the later `.btn` declaration

## Sidebar background (V2.4, shipped)
- Dark mode: `#111111` — separates tool panel from pure black canvas without adding colour
- Light mode: `#f5f5f5` — subtle off-white panel, distinct from white canvas
- Rationale: canvas = output space, sidebar = tool space — visual separation makes the interface feel more intentional
- Hardcoded values rather than CSS variables — `var(--dim)` was `#222222` (too light in dark mode) and `#eeeeee` (too similar to white in light mode)

## Camera roll export (decided against, V2.4)
- Not possible from a browser-based tool — platform restriction on both iOS and Android
- iOS: downloads go to Files app only; Photos requires native app or Share Sheet
- Android: downloads go to Downloads folder
- Resolution: mention in Instagram caption/bio to set expectations
- Native app wrapper (React Native) would be required — out of scope

## GIF export fix (V2.5, shipped)
- Root cause: gif.js spawns a Web Worker using the `workerScript` URL; browsers block cross-origin worker scripts (CORS)
- Fix: fetch gif.worker.js once as a regular HTTP request, wrap in a Blob, pass `blob://` URL as `workerScript` — Workers can always load from blob URLs
- Worker URL cached in `gifWorkerUrl` variable — fetch only happens once per session
- For camera GIF capture: worker is pre-fetched before the 3-second recording window starts, so encoding fires immediately when recording ends

## SVG export (V2.5, shipped; updated V2.10)
- Approach: rect-per-pixel at dithered resolution — one `<rect x y width height />` per ink pixel
- viewBox set to dithered dimensions (e.g. 400×300 at Scale 2 on an 800×600 image) — infinitely scalable
- `shape-rendering="crispEdges"` — keeps output pixel-sharp at any zoom in Figma/Illustrator
- V2.5: paper colour fills a background rect; ink colour fills all dot rects
- V2.10 update: last palette slot = background rect; all other slots each get one `<g fill="...">` containing only their ink pixels — scales naturally to N colours
- Resolution cap: if dithered pixel count exceeds 640,000, user is warned before generating — at that size files exceed ~18MB
- Use case: screen printing, laser cutting, editorial, merch — any context requiring scalable bitmap art
- Decided against path-tracing (merging adjacent rects into paths) — different project, not needed for intended use

## Favicon (V2.5, shipped)
- User-supplied 32×32 image (black cat on white circle), JPEG encoded
- Injected at runtime via JS: image loaded into a canvas, clipped to a circle path, exported as PNG data URI, appended as `<link rel="icon">` to `<head>`
- Circle clip removes JPEG background square — transparent corners, clean circle in browser tab
- No external favicon file — entirely self-contained in index.html

## Analytics — Plausible (V2.5, shipped; updated V2.10)
- Plausible chosen over Umami (Umami cloud email verification failed) and Google Analytics (too heavy, cookie-based)
- Plausible: open source, privacy-respecting, no cookies, GDPR compliant, no consent banner required
- Script injected in `<head>` — page views and referrers tracked automatically
- Custom events: `Image Upload`, `Camera Used`, `Preset Used`, `Palette Colour Added`, `Download PNG`, `Download JPG`, `Download GIF`, `Download SVG`
- Eight goals configured in Plausible dashboard to match event names exactly
- Goal: measure Instagram → floydsteinberg.art → download funnel

## Canvas pinch-to-zoom (V2.6, shipped)
- Zoom is a CSS transform only — never touches the render pipeline or re-renders the canvas
- `touch-action: none` on `.canvas-wrap` — intercepts all pointer events, prevents browser native pinch-zoom
- Pointer event Map tracks up to 2 simultaneous touches by `pointerId`
- Two pointers: distance delta drives zoom scale, midpoint delta drives pan — pinch focal point stays fixed on canvas content
- One pointer (when zoomed in): drags to pan
- Double-tap within 300ms resets to 1× (100% / fit)
- Zoom range: 0.5× (50%) to 8× (800%)
- Step size: 0.25× (25%) per button tap — sequence reads 50% → 75% → 100% → 125% etc.
- `clampPan()` keeps canvas edge-bound so it cannot be dragged fully off screen
- Zoom state lives in main `state` object — `clearAll()` resets it cleanly

## Zoom indicator (V2.6, shipped)
- `− 100% +` widget, absolute positioned bottom-right of `.canvas-wrap`, 12px from each edge
- Hidden when no image loaded, shown via `.visible` class on `setHasImage(true)`
- `−` dims when at 50% minimum, `+` dims when at 800% maximum
- Background `var(--bg)`, 1px border — reads as control, not canvas content
- Rationale: without it users have no reference for how zoomed in they are; disorienting at 4–8×

## Modal body text (V2.6, fixed)
- Was `var(--mid)` (#555555 in dark mode) — effectively unreadable against black modal background
- Fixed to `var(--fg)` — pure white in dark mode, pure black in light mode
- Modal title was already `var(--fg)` — body now consistent with it

## Presets (V2.7, shipped; updated V2.10)
- Sidebar position: below Input group, above Effect group — order follows workflow logic (load → starting point → tune)
- Implementation: standard `.btn` buttons in a `PRESETS` group — zero new UI patterns introduced
- Active state: selected preset highlights with `.active` class; clears automatically when user manually adjusts any slider (signals "custom territory")
- Set: Newsprint (Bayer 4×4, Scale 3, high contrast), Zine (Atkinson, Scale 2, pushed threshold), Glitch (Noise, Scale 1, inverted), Lo-Fi (Bayer 8×8, Scale 4, soft contrast), Raw (Floyd-Steinberg, Scale 1, neutral)
- Rationale: new users need a fast path to a result they're excited about — presets get them there in one tap instead of 3 minutes of slider exploration
- V2.10: presets reset palette to their defined 2-colour ink/paper pair — intentional, presets are opinionated looks, multi-colour is a manual creative choice

## Collapsible sidebar sections (V2.8, shipped)
- All sections open by default — no hidden complexity for new users
- User can collapse any section via `+` / `−` toggle at far right of group label
- State persists via localStorage — collapsed sections stay collapsed across sessions
- Rationale: build this after presets so we're collapsing the final sidebar structure, not an interim one
- Implementation: `localStorage.setItem('collapsed', JSON.stringify({colour: true, export: true}))` on each toggle, read on init

## Dithered modal background (decided, V2.8 candidate)
- About modal background to be replaced with a canvas-generated Bayer dither pattern
- Rationale: makes the About page feel like it belongs to the tool rather than being a generic overlay; strong for Instagram screenshots of the tool itself
- To be specced properly in V2.8

## N-colour palette dithering (V2.10, shipped)
- Engine upgraded from 2-colour (ink/paper binary snap) to N-colour (2–5 colours, RGB vector error propagation)
- `state.palette` array is now the source of truth — replaces `state.inkColor` / `state.paperColor` as separate values
- `state.inkColor` and `state.paperColor` kept as getter/setter aliases pointing to `palette[0]` and `palette[last]` — all existing preset, export, and status bar logic unchanged
- 2-colour output is bit-for-bit identical to V2.9 — no regression

### Engine: error diffusion algorithms
- All five error diffusion patterns (Floyd-Steinberg, Atkinson, Jarvis-Judice-Ninke, Stucki, Ostromoukhov) unified into a single RGB vector pass — replaces five separate grayscale implementations
- Snap step: nearest palette colour by RGB Euclidean distance, not a binary threshold
- Error propagated as an [R, G, B] vector using the same kernel weights as before — algorithm behaviour unchanged, colour space expanded

### Engine: ordered dither patterns
- Bayer (2×2, 4×4, 8×8), Noise, and Halftone use a luminance-mapped palette snap
- `orderedSnap(lum, threshNorm)` maps luminance to a position in the palette sorted by luminance, using the threshold value to decide between adjacent palette entries
- With 2 colours, output is identical to V2.9

### Invert with N colours (bug — fix in progress)
- Original V2.10 implementation reversed the palette array before passing to the dither engine
- This does not work: error diffusion uses Euclidean distance which is order-agnostic; ordered dither sorts by luminance internally — reversing the input array has no effect in either case
- Fix approach: restore invert as a pixel pre-processing step — when `state.invert` is true, apply `r = 255 - r, g = 255 - g, b = 255 - b` at the sampling stage before any dither math
- This correctly inverts output for all 10 patterns at all palette sizes

### Palette UI
- Replaces fixed Ink / Paper rows in the Colour section
- Dynamic swatch row: 2 swatches by default, `+` button adds up to 5
- `+` button: 20×20px dashed border, hidden when palette length = 5
- Remove affordance: 11×11px `×` badge top-right of each swatch, hidden on last two swatches (minimum 2 enforced)
- Desktop: `×` revealed on swatch hover (`.removable` class, CSS only)
- Mobile: tap swatch to reveal `×` (touch-selected state); tap outside to dismiss; on 2-colour palette, tap opens picker directly — no remove affordance shown
- Hex readout: single line below the swatch row, all current colours joined by ` · ` (e.g. `#0a0a0a · #c83c28 · #f5f0e8`)
- Mobile swatches: 20×20px → 28×28px in `@media (max-width: 480px)`
- Palette order matters — palette[0] is conventionally darkest (ink), palette[last] is conventionally lightest (paper/background); not enforced, user's responsibility

### SVG export with N colours
- One `<g fill="...">` per palette slot, excluding the last slot
- Last slot = background rect — fills the full SVG canvas
- Nearest-palette-index lookup mirrors the dither engine — SVG faithfully represents what the canvas shows
- Background rule: last slot is always background regardless of its colour value — user controls this by palette order; Invert toggle effectively swaps which end is background

## Gallery / settings share (backlog, to be specced)
- Idea: export an image with current settings baked into it — shareable output that communicates how a result was made
- Could also manifest as a URL-based state share (settings encoded in query params) — load a URL, tool opens with those exact settings applied
- High value for community/Instagram use case — people can share not just the output but the recipe
- Needs full spec before building

## MP4 export (decided against for V2, backlog for V3)
- Instagram does not accept GIF uploads — MP4 is the correct format for video content
- Browser-native path (canvas.captureStream → MediaRecorder) outputs WebM, not MP4 — Instagram incompatible
- Correct approach: WebCodecs API (VideoEncoder) + mp4-muxer library — outputs real H.264 MP4, no heavy dependencies
- Decided against for V2: meaningful implementation effort, full session's work, not a quick add
- Backlog as named V3 item: "MP4 export via WebCodecs + mp4-muxer"

## Colour group label — Canvas → Paper rename (V2.10e, shipped)
- The background colour control was previously labelled "Canvas" — renamed to "Paper"
- Rationale: "Paper" is the correct mental model for the control — it's the surface the ink sits on, not a removal or transparency tool
- "Canvas" implied a workspace concept or alpha channel behaviour, which led to incorrect expectations about what the colour would do
- "Paper" is accurate to how dithering works: light pixels snap to paper, dark pixels snap to ink — the label now matches the algorithm
- Single label change in HTML — no logic, no state, no behaviour changed

## Canvas colour architecture fix — attempted and reverted (V2.10e)
- Attempted: remove `canvasRgb` from `effectivePal`, replace with an RGB distance pre-pass (`isBackground`) driven by a remapped threshold slider (0–100, default 30)
- Goal was to give users explicit control over which pixels are treated as background, independent of the dither snap
- Broke all Bayer / halftone / noise patterns: the pre-pass collapsed `N` to `1` for ordered dithering (only one colour ever reached the dither step)
- Also misclassified subject pixels as background when the paper colour wasn't white — pre-pass assumption did not hold for non-default palettes
- Reverted fully to V2.10d production code — threshold slider unchanged at −128 to 128
- Learning: the canvas/paper colour behaviour is a fundamental property of how dithering works, not a bug. Lightest pixels snap to paper, darkest snap to ink — this is correct and expected. The label rename was the right and complete response to the UX confusion.