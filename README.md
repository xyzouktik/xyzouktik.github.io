# Youktik Sajjan — Portfolio

Personal site and CV for Youktik Sajjan. Static HTML, no build step, served by GitHub Pages.

Live: https://xyzouktik.github.io

## Files

- `index.html` — homepage (About, Current Focus, Research Interests, Selected Projects, Experience, Technical Skills, Achievements & Community, Contact)
- `cv.html` — standalone CV, linked from the homepage
- `blog.html` — legacy Creatives page, still on the old dark theme and not linked from the homepage
- `README.md` — this file
- `GITHUB_PROFILE_README.md` — profile README for the separate `xyzouktik/xyzouktik` GitHub profile repo; not part of the site

## Design and implementation

- Serif body text, monospaced labels, a single accent colour.
- Light/dark: automatic via `prefers-color-scheme`, plus a manual toggle stored in `localStorage`.
- No CSS/JS frameworks and no external fonts — system font stacks only.
- Background: an inline arcade Ender Dragon `<canvas id="dragon-canvas">` fixed at `z-index:0`, with content wrapped in `.page` at `z-index:1`.
- `index.html` and `cv.html` are each self-contained (inline CSS and JS).

## Notes

- The Underwater AI card links to and embeds https://underwaterai.org/.
- `assets/` (html5up template) and `images/` are legacy and unreferenced by the current pages.
- `blog.html` has not been migrated to the current design.

## Publish

GitHub Pages serves this repository root from the `main` branch.

1. Repository: `xyzouktik.github.io`
2. Settings → Pages → Deploy from a branch → `main` / `(root)`
3. Published at https://xyzouktik.github.io
