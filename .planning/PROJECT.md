# Floyd Steinberg — PROJECT.md

## What is Floyd Steinberg?

Floyd Steinberg is a browser-based image dithering tool. Drop in a photo, apply a bitmap effect, download the result. No login, no signup, no friction. Just open and experiment.

**Live:** https://floydsteinberg.art
**Instagram:** @floydsteinberg
**Status:** V2.3 shipped — bitmap dither, camera input, colour output, GIF/PNG/JPG export, brightness/blur/pixelate/scatter controls

## Why does it exist?

Three reasons:
1. A learning lab for creative coding — effects built in Canvas API / vanilla JS
2. A content engine for ORG — images made with Floyd Steinberg get posted to Instagram
3. An experiment in virality — can a free tool spread on its own?

## Who is it for?

Designers, creatives, and curious people who want to make something interesting with an image quickly. People who would share the output on Instagram.

## What feeling should it create?

Immediate. Tactile. Like a darkroom tool that runs in the browser. The aesthetic is precise and considered — not flashy.

## What it is NOT

- Not a photo editor (no cropping, colour correction etc.)
- Not a social platform (no accounts, no feeds)
- Not a monetisation play

## Aesthetic principles

- Monochromatic foundation — black/white default, two-colour output supported
- IBM Plex Mono typography
- Swiss grid discipline — 8px base unit
- No decoration, no gradients, no shadows
- The output should feel built, not styled
- Reference: Joy Division, Swiss modernism, ASCII art

## The name

Named after Robert W. Floyd and Louis Steinberg, who published "An Adaptive Algorithm for Spatial Greyscale" in 1976. Their error diffusion algorithm runs inside this tool. Nearly fifty years later it still runs inside almost every printer, image editor, and display pipeline on earth.

## Stack

- Single `index.html` shell + `effects/` folder
- Vanilla JS + Canvas API
- No frameworks, no build step
- Deployed on Vercel, auto-deploys from GitHub main
- Primary domain: floydsteinberg.art
- Repo: https://github.com/Odonata-Research-Group/raster