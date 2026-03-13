# Raster — DECISIONS.md

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

## Colour output — Ink / Paper (V2.2, shipped)
- Two hex inputs: Ink (foreground, default #ffffff) and Paper (background, default #000000)
- Labelled "Ink / Paper" — fits the darkroom/print aesthetic
- Colour applied at pixel write step in dither() — replaces hardcoded 255/0 values
- Works across all patterns automatically — no per-pattern logic
- Invert toggle continues to work — swaps which pixels get Ink vs Paper
- Defaults match original black/white output exactly — no regression
- Mode selector (Mono / Tonal / Palette / RGB / Original) — still V3, not this session

## Light / Dark mode (V2.2, shipped)
- CSS variable swap on html element — one toggle, affects everything
- Dark (default): #000000 bg, #ffffff text
- Light: #ffffff bg, #000000 text, adjusted mid (#888888) and border (#cccccc)
- Toggle lives in header, replaces "Bitmap — V1" label
- Label updates contextually: shows "Light" in dark mode, "Dark" in light mode

## Typography system (V2.2, shipped)
- IBM Plex Mono throughout — all three loaded weights used
- Section headers (group-label): 500 weight, white (var(--fg)), 10px — primary visual anchor
- Control labels (param-name, toggle-label, colour-label): 300 weight, mid gray — recede correctly
- Param values: 400 weight, white, 11px — reads as data not decoration
- Wordmark: 500 weight, 13px, 0.2em tracking

## About modal (V2.2, shipped)
- Modal overlay — stays in tool, no navigation away
- Triggered from About link in sidebar footer
- Closes via ✕ button, clicking overlay, or Escape key
- Content: tone reference is honest, anti-friction (Alim's site aesthetic)
- Credit: "Made by Nick — Odonata Research Group"
- Instagram link placeholder — href="#" until handle confirmed

## Sidebar footer (V2.2, shipped)
- Three links: About · Follow · GitHub
- Pushed to bottom of sidebar via margin-top: auto
- Styling: 300 weight, mid gray, hover reveals arrow + brightens to white
- Arrow treatment: all three use → (straight arrow) — consistent regardless of destination
- Rationale: diagonal ↗ signals "exits the experience" which was inconsistent with About; uniformity wins

## Export buttons (V2.2, shipped)
- Export buttons use border-color: var(--mid) default — visually distinct from Input buttons
- Same .btn base class, additional .export-btn class for the treatment

## Canvas zoom (backlog)
- Pixel-perfect inspection of dithered output
- Useful for high-resolution export verification
- Fits "built, not styled" aesthetic

## Analytics
- Umami (open source, privacy-respecting, self-hostable on Vercel)
- Track: page views, PNG downloads, GIF downloads, TXT downloads
- Goal: measure Instagram → raster → download funnel

## Export formats
- V1 shipped: PNG, JPG, TXT (ASCII)
- V2 planned: GIF (animated, camera frames)
- V3 planned: MP4 (MediaRecorder API), SVG

## Competitive reference
- Reviewed comparable browser-based dither tool (March 2026)
- Decision: don't chase feature parity — their UX is a settings panel, ours is a tool
- Steal: more dither algorithms, colour modes, canvas zoom
- Ignore: post-processing (CRT, Phosphor, Bloom), chromatic aberration sliders — wrong aesthetic for ORG