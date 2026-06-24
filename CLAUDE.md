# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Classic Asteroids arcade clone built with vanilla HTML5 Canvas and JavaScript — no frameworks, no bundler, no dependencies. Single-file game logic (`game.js`) loaded by `index.html`.

## Running

Open `index.html` directly in a browser, or:

```bash
npx serve .
```

There is no build step, no tests, and no linter configured.

## Architecture

Everything lives in `game.js` as a single-script game loop:

- **Input**: `keydown`/`keyup` listeners populate `keys` (held) and `justPressed` (single-fire) maps
- **Entity classes**: `Ship`, `Asteroid`, `Bullet`, `Particle` — each has `update(dt)` and `draw()` methods
- **Game state machine**: `state` variable drives three modes: `playing`, `dead` (respawn delay), `gameover`
- **Loop**: `requestAnimationFrame` → `update(dt)` → `draw()`, with `dt` clamped at 50ms

Canvas is fixed at 800×600 (`W`/`H` constants). All entities use screen-space wrapping via `wrap()`.

### Key mechanics

- Asteroids have 3 sizes (indexed 1–3); arrays `RADII`, `SPEEDS`, `POINTS` are indexed by size
- Splitting: destroying size N spawns two size N-1; size 1 just explodes
- Ship gets 3 seconds of invincibility on spawn (blink effect)
- Collision uses simple circle-circle distance checks (`dist()`)
- Level advances when `asteroids.length === 0`; next level spawns `3 + level` asteroids

## Language

UI text and comments are in Spanish.
