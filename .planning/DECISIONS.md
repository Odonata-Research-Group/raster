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