# xyzouktik.github.io

Personal site for **Youktik Sajjan** — static HTML, no build step, served by GitHub Pages.

Live: https://xyzouktik.github.io

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Homepage: About, Focus, Research, Projects, Experience, Technical Skills, Achievements & Community, Contact, Games |
| `cv.html` | Standalone CV (LaTeX-style typesetting, print-ready) |
| `game.html` | Two canvas games: Immune Runner and Fighter |
| `blog.html` | Legacy Creatives page (not linked from the homepage) |
| `README.md` | This file |

## Theme

Black and white only, with **Black as the default**. Two modes — **Black** (white ink on near-black) and **White**
(black ink on white) — chosen with the two-swatch picker in the header. The choice persists in
`localStorage["site-theme"]` and is shared with `cv.html`.

An interactive arcade **Ender Dragon**, together with its ambient mobs, is drawn in full colour on a fixed `<canvas>`
behind the page on both modes; the page chrome stays black and white.

## Notes

- No CSS/JS frameworks and no external fonts — system font stacks only.
- `index.html` and `cv.html` are self-contained (inline CSS and JS).
- `cv.html` prints with the white palette regardless of the active theme.
- `assets/` (html5up template) and `images/` are legacy and unreferenced.

## Publish

GitHub Pages serves this repository root from `main` → https://xyzouktik.github.io
