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

Black and white only. Two modes — **White** (black ink on white) and **Black** (white ink on near-black) — chosen with the
two-swatch picker in the header. The choice persists in `localStorage["site-theme"]`, follows `prefers-color-scheme` on
first visit, and is shared with `cv.html`.

In the Black mode an interactive arcade **Ender Dragon** is drawn on a fixed `<canvas>` behind the page, rendered in
grayscale so it stays monochrome.

## Notes

- No CSS/JS frameworks and no external fonts — system font stacks only.
- `index.html` and `cv.html` are self-contained (inline CSS and JS).
- `cv.html` prints with the white palette regardless of the active theme.
- `assets/` (html5up template) and `images/` are legacy and unreferenced.

## Publish

GitHub Pages serves this repository root from `main` → https://xyzouktik.github.io
