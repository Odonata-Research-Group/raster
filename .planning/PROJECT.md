# Floyd Steinberg — PROJECT.md

## What is Floyd Steinberg?

Floyd Steinberg is a browser-based image dithering tool. Drop in a photo, apply a bitmap effect, download the result. No login, no signup, no friction. Just open and experiment.

**Live:** https://floydsteinberg.art
**Instagram:** @floydsteinberg
**Status:** V2.11 shipped — bitmap dither, camera input, N-colour palette dithering, GIF/PNG/JPG/SVG export, animated GIF sequencer, brightness/blur/pixelate/scatter controls, full mobile support, pinch-to-zoom, presets, collapsible sidebar, analytics, Paper label

## Why does it exist?

Three reasons:
1. A learning lab for creative coding — effects built in Canvas API / vanilla JS
2. A content engine for ORG — images made with Floyd Steinberg get posted to Instagram
3. An experiment in virality — can a free tool spread on its own?

## Who is it for?

Designers, creatives, and curious people who want to make something interesting with an image quickly. People who would share the output on Instagram. Primarily encountered on mobile — the tool is fully usable on phone from V2.4.

## What feeling should it create?

Immediate. Tactile. Like a darkroom tool that runs in the browser. The aesthetic is precise and considered — not flashy.

## What it is NOT

- Not a photo editor (no cropping, colour correction etc.)
- Not a social platform (no accounts, no feeds)
- Not a monetisation play
- Not a native app — exports go to Files/Downloads, not camera roll (platform restriction)

## Aesthetic principles

- Monochromatic foundation — black/white default, N-colour palette (2–5 colours) supported from V2.10
- IBM Plex Mono typography throughout
- Swiss grid discipline — 8px base unit
- No decoration, no gradients, no shadows
- The output should feel built, not styled
- Reference: Joy Division, Swiss modernism, ASCII art
- Two-zone UI: canvas = pure output space (#000000), sidebar = tool space (#111111 dark / #f5f5f5 light)

## The name

Named after Robert W. Floyd and Louis Steinberg, who published "An Adaptive Algorithm for Spatial Greyscale" in 1976. Their error diffusion algorithm runs inside this tool. Nearly fifty years later it still runs inside almost every printer, image editor, and display pipeline on earth.

## Stack

- Single `index.html` — UI, canvas, controls, all effects inline
- Vanilla JS + Canvas API
- No frameworks, no build step
- Deployed on Vercel, auto-deploys from GitHub main
- Primary domain: floydsteinberg.art
- Redirect domain: floydsteinberg.app
- Repo: https://github.com/Odonata-Research-Group/raster

## Distribution

- Primary channel: Instagram (@floydsteinberg) → floydsteinberg.art
- Funnel: post output image → link in bio → tool → download
- Analytics: Plausible (privacy-respecting, no cookies, GDPR compliant) — shipped V2.5
- Ten goals tracked: Image Upload, Camera Used, Preset Used, Palette Colour Added, Download PNG, Download JPG, Download SVG, Download GIF, Still Captured, Download GIF Animated
- No paid distribution, no SEO investment — organic only

## Roadmap

### Shipped
- V2.7: Presets — Newsprint, Zine, Glitch, Lo-Fi, Raw
- V2.8: Collapsible sidebar sections
- V2.9: Jarvis-Judice-Ninke, Stucki, Ostromoukhov error diffusion + true AM Halftone (rotated dot grid, Dot Size + Screen Angle controls)
- V2.10: N-colour palette dithering engine — RGB vector error propagation, dynamic palette UI (2–5 colours), SVG multi-colour export
- V2.10e: Paper label — background colour control renamed from "Canvas" to "Paper" for accuracy
- V2.11: Animate — manual frame sequencer; capture up to 15 dithered stills, preview at 4/8/12fps, loop or ping-pong, export as animated GIF via gif.js. Invert fix — redundant palette inversion removed, pre-processing step is now the sole invert path.

### Next
- TBD — to be specced

### V3
- Gallery / settings share — export image with settings baked in, or URL-encoded state for sharing exact recipes
- MP4 export via WebCodecs + mp4-muxer (Instagram-compatible H.264)
- Mode selector: Mono / Tonal / Palette / RGB / Original
- Palette extraction from image
- Landing page