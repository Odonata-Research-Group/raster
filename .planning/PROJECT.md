# Raster — PROJECT.md

## What is Raster?

Raster is a browser-based image effect tool. Drop in a photo, apply a visual effect, download the result. No login, no signup, no friction. Just open and experiment.

**Live:** https://raster-khaki.vercel.app
**Status:** V2.2 shipped — bitmap dither, camera input, colour output, PNG/JPG/TXT export

## Why does it exist?

Three reasons:
1. A learning lab for creative coding — effects built in Canvas API / vanilla JS
2. A content engine for ORG — images made with Raster get posted to Instagram
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

## Stack

- Single `index.html` shell + `effects/` folder
- Vanilla JS + Canvas API
- No frameworks, no build step
- Deployed on Vercel, auto-deploys from GitHub main
- Repo: https://github.com/Odonata-Research-Group/raster