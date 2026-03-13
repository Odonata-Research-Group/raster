# Raster — REQUIREMENTS.md

## V1 (Launch weekend)

### Input
- [ ] Image upload (drag + drop or file picker)
- [ ] Take a photo (device camera)
- [ ] Live camera feed (webcam / phone)

### Effect — Bitmap/Dither
- [ ] Real-time canvas preview
- [ ] Adjustable parameters (dot size, threshold, pattern)
- [ ] Invert toggle

### Output
- [ ] Download as PNG
- [ ] Download as JPG
- [ ] Download as GIF (animated, live camera frames)
- [ ] Download as TXT (ASCII version)

### Analytics
- [ ] Umami installed (page views, download events)

### Constraints
- Single HTML file + effects/bitmap.js
- No frameworks, no build step
- No login, no backend
- Must work on mobile (camera feature)

## V2 (Next sprint)
- MP4 export (MediaRecorder API)
- Second effect (ASCII or halftone)
- SVG export

## V3
- Third effect
- HTML export
- Effect combinator

## Out of scope (forever)
- User accounts
- Saving/storing images server-side
- Monetisation