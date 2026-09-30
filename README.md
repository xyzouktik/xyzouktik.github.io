# Youktik Sajjan — End Dimension Portfolio

Static GitHub Pages portfolio with a Minecraft End-inspired interface, an arcade-style dragon canvas background, and a separate Creatives page for essays, poetry, and literature.

Live site: https://xyzouktik.github.io

## Files

- `index.html` — main portfolio page
- `blog.html` — Creatives page (writing, poetry, literature)
- `cv.html` — CV document, embedded in `index.html` and openable on its own
- `README.md` — project notes
- `TRANSFORMATION.md` — technical notes on the current implementation

## Current sections

- About
- Projects
- Ventures
- Culture
- Music
- Gallery (`Coming Soon`)
- Contact
- CV (final section)
- Creatives page in `blog.html`

## Visual system

- Void background: `#050508` / `#0a0b12`
- Surfaces: `#0f1020` / `#161830`
- Accent: chorus purple `#c084fc`
- CTA: portal cyan `#67e8f9`
- Fonts: Press Start 2P, VT323, Share Tech Mono, Nunito
- Geometry: `0px` border radius everywhere

## Interactive features

- Fixed canvas background with a 2D arcade-style Ender Dragon (`index.html`)
- Dragon follows cursor movement, animates wings/jaw, and breathes fire
- Ambient Minecraft mobs spawn from screen edges and react to the dragon
- GitHub project fetch for the `xyzouktik.github.io` repo
- Scroll-triggered reveal animations
- Separate Creatives page with category filters and a drifting particle/starfield background

## Notes

- No build step: plain HTML with Tailwind loaded from the CDN and inline canvas scripts.
- The `assets/` and `images/` folders are legacy template assets and are not referenced by the current pages.
- The contact form in `index.html` posts to a placeholder Formspree endpoint (`formspree.io/f/your-id`) and needs a real form ID to deliver messages.

## Publish to GitHub Pages

1. Use the repository `xyzouktik.github.io`.
2. Keep these files in the repository root: `index.html`, `blog.html`, `cv.html`, `README.md`.
3. In GitHub repository settings, open `Pages`.
4. Set source to `Deploy from a branch`.
5. Choose branch `main` and folder `/ (root)`.
6. Wait for Pages to build, then open https://xyzouktik.github.io.
