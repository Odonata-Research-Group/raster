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
- CSS variable swap on html e