# Raster — DECISIONS.md

## Architecture
- Single index.html shell — UI, canvas, controls
- Each effect is a self-contained JS file in /effects/
- New effects drop in without touching core tool
- No frameworks — vanilla JS + Canvas API

## Effect V1: Bitmap/Dither
- Starting with ordered dither (structured dot pattern)
- Parameters: dot size, threshold, pattern type
- Invert toggle

## Typography
- IBM Plex Mono throughout
- Loaded from Google Fonts

## Colour
- Background: #000000
- Text / UI: #FFFFFF
- No accent colours in V1

## Analytics
- Umami (open source, privacy-respecting, self-hostable on Vercel)
- Track: page views, PNG downloads, GIF downloads, TXT downloads

## Export formats V1
- PNG (canvas.toDataURL)
- JPG (canvas.toDataURL with quality param)  
- GIF (frame capture from canvas)
- TXT (ASCII representation)