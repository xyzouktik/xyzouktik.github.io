# xyzouktik.github.io

Personal site for **Youktik Sajjan** — static HTML, no build step, served by GitHub Pages.

Live: https://xyzouktik.github.io

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Homepage: About, Focus, Research, Projects, Experience, Technical Skills, Achievements & Community, Contact, Games, plus the animated scene background |
| `cv.html` | Standalone CV (LaTeX-style typesetting, print-ready, no canvas) |
| `game.html` | Two canvas games: Immune Runner and Fighter |
| `blog.html` | Legacy Creatives page — still on the old theme, not linked from the homepage |
| `README.md` | This file |

## Four living themes

The background is a procedural Canvas 2D scene, one per theme. Pick a theme with the swatch
picker in the header (Ender / Koi / Verdant / Abyss). It persists in `localStorage["site-theme"]`,
is shared with `cv.html`, and follows `prefers-color-scheme` on first visit (never auto-picks
green or blue). Each theme defines a full token set (paper/bg, ink/foreground, muted, rule,
accent, card, card-border, shadow, selection) with WCAG AA contrast; content cards are
translucent with a `backdrop-filter` blur so text stays legible over the animation.

| Theme | id | Scene |
| --- | --- | --- |
| Ender | `dark` | The arcade Ender Dragon canvas (the original experience) |
| Koi / Taiji | `light` | Two koi chase each other in a Taiji over a wave-field pond |
| Verdant | `green` | A forest ecosystem across the day (deer, beavers, elephants, butterflies) |
| ABYSS-1 | `blue` | A pilotable ROV descending past a glowing manta school and a whale |

## Scene architecture

- `THEMES = { dark:{scene:EnderScene}, light:{scene:KoiScene}, green:{scene:ForestScene}, blue:{scene:AbyssScene} }`
- Every scene implements `init / resize / update / draw / start / stop / destroy`.
- One `requestAnimationFrame` loop drives the active scene only; `dt` is clamped to 50 ms.
- Shared `Input` (pointer + velocity, keys, scroll fraction, click/double-click, UI-target
  guard), a seeded `mulberry32` PRNG, and 2-D value noise.
- The Ender dragon keeps its own loop and is started/stopped by the ThemeManager, so the dark
  experience is unchanged. Two stacked canvases (`#dragon-canvas`, `#scene-canvas`) cross-fade
  via CSS opacity; the canvas is `pointer-events:none` and `aria-hidden`.

## Controls

**Abyss ROV** — WASD / arrows move · `Shift` boost · `F` headlamp · long-press sonar ·
double-click a creature to log a specimen · scroll = depth.

**Other scenes** — move the pointer; click (Koi: drop food, Verdant: spawn butterflies);
double-click a koi to make it leap.

## Scene Lab

Press `L` (or the "Scene Lab" button, bottom-right) for tuning controls: animation speed,
creature density, per-theme sliders (Koi water calmness; Verdant wind + time of day; ABYSS
manta count / glow / current / lamp radius / ROV speed), buttons to spawn a creature, pause,
reset, save a PNG snapshot, randomise the seed, and ABYSS-specific actions (call the school,
summon whale, dolphin breach, toggle restoration light). Values persist per theme.

## Performance and accessibility

- devicePixelRatio capped at 2 (desktop) / 1.5 (mobile); the ABYSS scene auto-degrades
  (fewer mantas, shorter trails) if the rolling frame time exceeds ~20 ms.
- The loop pauses when the tab is hidden.
- `prefers-reduced-motion` is respected; the CV prints with the light palette regardless of theme.

## Publish

GitHub Pages serves this repository root from `main` → https://xyzouktik.github.io