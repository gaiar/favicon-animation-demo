# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Single-page web application demonstrating animated favicon techniques using HTML5 Canvas and Web Audio API. The app renders real-time animations to canvas elements and updates the browser favicon dynamically.

**Live demo:** https://gaiar.github.io/favicon-animation-demo/

## Development

This is a static site with no build process. To run locally:

```bash
python3 -m http.server 8080
# Open http://localhost:8080
```

## Architecture

### Single File Structure
Everything is contained in `index.html`:
- CSS styles (embedded in `<style>`)
- JavaScript logic (embedded in `<script>`)
- No external dependencies or build tools

### Core Systems

**Animation System:**
- `ANIMS` array defines all animations with id, name, optional sound type, and chaos flag
- `animate(ctx, type, t, sz)` - Main render function using canvas 2D transforms
- Transform animations applied via `ctx.translate()`, `ctx.rotate()`, `ctx.scale()`, `ctx.transform()`
- Post-processing effects via `ctx.getImageData()`/`putImageData()` for pixel manipulation

**Favicon Update Loop:**
- `loop(ts)` runs via `requestAnimationFrame`
- Renders to three preview canvases (64px, 32px, 16px)
- Updates browser favicon from 32px canvas every 50ms using data URL

**Audio System (Web Audio API):**
- `playSound(type)` - Creates oscillators/noise for sound effects
- Sound types: `drone`, `noise`, `pulse`, `chaos`
- Sounds tied to specific animations via `sound` property in ANIMS

### Adding New Animations

1. Add entry to `ANIMS` array with unique `id`
2. Add `case` in `animate()` switch for canvas transforms
3. If using post-processing, add animation id to the includes() check and add effect logic
4. If sound needed, add `sound` property and implement in `playSound()`

## Assets

- `assets/favicon_64.png` - Source image for animations (loaded at runtime)
- `assets/favicon_32.png` - Fallback favicon
- SVG files are unused legacy assets
