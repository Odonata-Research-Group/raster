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

## Effect V2: Dither — new algorithms
- Floyd-Steinberg error diffusion — first new pattern (this session)
- Rationale: fundamentally different algorithm from Bayer (error propagation vs matrix lookup), produces organic edges, high ORG aesthetic fit
- Scale on Floyd-Steinberg = pre-downsample factor, consistent with Bayer behaviour
- All new patterns share existing controls: Scale, Threshold, Contrast, Invert — no new UI per pattern
- Patterns drop into existing select dropdown without touching core

## Typography
- IBM Plex Mono throughout
- Loaded from Google Fonts

## Colour
- Background: #000000
- Text / UI: #FFFFFF
- No accent colours in V1

## Light / Dark mode (V3)
- Full inversion: black UI + white output ↔ white UI + black output
- CSS variable swap — one toggle, affects everything
- Not a partial flip — the whole experience inverts

## Colour output mode (V3)
- Dither output in colour, not just black/white
- Needs design thinking before spec — how colour maps to dither pattern is non-trivial
- Likely implemented as a Mode selector (Mono / Tonal / Original)

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