# xyzouktik.github.io

Personal homepage of **Youktik Sajjan** (Integrated BS-MS, Biological Sciences, IISER Kolkata) — a single, self-contained `index.html` redesigned around **real liquid-glass refraction**, powered by [liquidGL](https://liquidgl.naughtyduk.com) v3.0.0. No build step, no runtime dependencies; served by GitHub Pages.

Live: https://xyzouktik.github.io

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-live-brightgreen)](https://xyzouktik.github.io)
[![liquidGL](https://img.shields.io/badge/liquidGL-v3.0.0-blueviolet)](https://liquidgl.naughtyduk.com)
[![License: MIT](https://img.shields.io/badge/license-MIT-lightgrey)](./LICENSE.txt)

---

## What's New

- **Liquid Glass panes** — the sticky header bar, the About hero pane and all five project cards are now true refracting glass rendered by liquidGL in WebGPU (falling back through WebGL2 → WebGL1 → CSS `backdrop-filter`). Edge bevel, animated specular highlights, soft drop shadows and a light neutral dye are applied to every pane.
- **Static, theme-aware backdrop** — the page paints a static composition of radial gradient glows (greyscale on White, End-dimension violet on Black) directly on `<body>`. The snapshot rasteriser captures it across the full document, so every pane refracts a correct backdrop at *any* scroll depth.
- **Live refraction while scrolling** — the header bar refracts the page content (and the glass cards' rendered output, stacked-lens style) in real time as it scrolls beneath.
- **Theme switch re-snapshot** — toggling Black/White re-captures the snapshot and refreshes every pane's content layer, so the glass always matches the active palette.
- **Mobile guard** — on viewports ≤ 640 px the large project cards drop to the pure-CSS glass fallback, keeping panes small enough for stable Safari rendering.

---

## Overview

The homepage keeps its original design language — black & white themes, serif editorial type, the arcade Ender-dragon canvas — and upgrades its material. The header, hero and project cards are `liquidGL` lenses: their own backgrounds are stripped at runtime, the library snapshot-rasterises the page behind them, and a shader re-draws the backdrop through the pane with refraction, a bevelled edge, specular highlights and a tint. All readable content lives in a child element stacked above the renderer canvas, so nothing inside a pane is refracted or hidden.

---

## Key Features

| Feature                                            | Supported | Feature                                | Supported |
| :------------------------------------------------- | :-------: | :------------------------------------- | :-------: |
| WebGPU rendering (auto fallback to WebGL1)         |    ✅     | Header glass bar                       |    ✅     |
| Real-time refraction of scrolling content          |    ✅     | Hero (About) glass pane                |    ✅     |
| Bevel + specular + shadow on every pane            |    ✅     | Project card lenses (×5)               |    ✅     |
| Tinted glass (`rgba(148,163,190,0.10)`)            |    ✅     | Stacked-lens composition               |    ✅     |
| Static gradient backdrop (theme-aware)             |    ✅     | Theme switch re-snapshot               |    ✅     |
| CSS `backdrop-filter` fallback                     |    ✅     | Animated canvas refracted live         |    ❌     |
| `on.init` callback                                 |    ✅     | External images inside lenses          |    ❌     |

---

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Homepage — About, Focus, Research, Projects, Experience, Skills, Achievements, Gallery, Contact, Games; inline CSS + JS, liquid-glass panes |
| `scripts/liquidGL.js` | liquidGL v3.0.0 (local copy, MIT © NaughtyDuk) — the only runtime dependency |
| `cv.html` | Standalone CV (LaTeX-style typesetting, print-ready) |
| `game.html` | Two canvas games: Immune Runner and Fighter |
| `blog.html` | Legacy Creatives page (not linked from the homepage) |
| `README.md` | This file |

## Prerequisites

Add the library once, before the init code — it is deferred so it executes before `DOMContentLoaded`:

```html
<script src="scripts/liquidGL.js" defer></script>
```

`liquidGL` has no runtime dependencies. The high-resolution snapshot of the page background that it refracts is produced by its own built-in rasteriser.

## Quick start

Every pane is an element with class `glass`. Its readable content lives in a child (`.glass-inner`, or the header's `.wrap`) that is stacked above the renderer canvas:

```html
<!-- Target (glassified) -->
<article class="card glass">
  <!-- Content: live DOM, sits on top of the glass -->
  <div class="glass-inner"> … </div>
</article>
```

Initialise inside `DOMContentLoaded`:

```html
<script>
  document.addEventListener("DOMContentLoaded", () => {
    liquidGL({
      target: ".glass",
      snapshot: "body",
      resolution: 2.0,
      refraction: 0.01,
      bevelDepth: 0.08,
      bevelWidth: 0.15,
      frost: 0,
      shadow: true,
      specular: true,
      tint: "rgba(148,163,190,0.10)",
      tilt: false,
      interaction: "none",
      reveal: "fade",
      on: { init(instance) { /* first frame rendered */ } }
    });
  });
</script>
```

---

## Liquid glass parameters

| Option | Value | Description |
| --- | --- | --- |
| `target` | `".glass"` | Selector for the elements to glassify |
| `snapshot` | `"body"` | Area used for refraction |
| `resolution` | `2.0` | Snapshot quality (clamped 0.1–3.0) |
| `refraction` | `0.01` | Base refraction strength (0–1) |
| `bevelDepth` | `0.08` | Intensity of the edge bevel (0–1) |
| `bevelWidth` | `0.15` | Bevel width as a proportion of the pane |
| `frost` | `0` | Blur radius in px; `0` = crystal clear |
| `shadow` | `true` | Soft drop-shadow under each pane |
| `specular` | `true` | Animated specular highlights |
| `tint` | `"rgba(148,163,190,0.10)"` | Glass dye; alpha sets dye strength |
| `tilt` | `false` | Hover tilt disabled |
| `interaction` | `"none"` | Pointer interaction disabled |
| `reveal` | `"fade"` | Panes fade in after the first snapshot |

## How the glass works here

- **Anchors.** Panes must live in a fixed/sticky containing block. The header is its own sticky anchor (`z-index: 10`); the hero and the five cards sit inside a zero-travel sticky wrapper (`.glass-anchor`) so all six lenses share a single renderer, one canvas and one snapshot.
- **Content.** `.glass-inner` and `.site-head .wrap` are `position: relative; z-index: 2`, above the renderer canvas (`z-index: -1` inside the anchor). All links, buttons, the theme picker, the menu and the live iframe stay interactive DOM.
- **Backdrop.** Static radial gradients on `<body>` (`--backdrop`). The rasteriser paints the body's background across the whole document, so refraction is correct everywhere — unlike a `position: fixed` backdrop, which only rasterises into the first viewport-height of the page.
- **The dragon.** The Ender-dragon canvas is animated by JavaScript every frame. liquidGL cannot track JS canvas animation (its dynamic pipeline listens for CSS transitions/animation events), so keeping the canvas in the snapshot would freeze one frame behind the glass forever. It carries `data-liquid-ignore` and is excluded from refraction; it stays fully live everywhere else.
- **Stacking.** The header renderer (`z 10`) composites the card renderer (`z 5`), so the header bar refracts the cards' glass *and* their rendered content as they scroll underneath.
- **Theme switch.** `window.__lglRefresh` re-captures the snapshot (`liquidGL.registerDynamic([])`) and sets `data-lgl-theme` on every pane, which nudges each content layer's MutationObserver into re-rasterising with the new palette.
- **Fallback.** Each `.glass` rule provides the chain's final stop: `backdrop-filter: blur(18px) saturate(1.4)` plus a translucent theme fill — visible before init and on browsers without WebGPU/WebGL.

---

## FAQ

| Question | Answer |
| :------- | :----- |
| Why isn't the dragon refracted by the glass? | It is a JS-animated canvas; liquidGL re-composites registered elements from DOM/CSS events, so a canvas animation would appear frozen at capture time. It is excluded from the snapshot (`data-liquid-ignore`) and stays live outside the panes. |
| Why are the hero and cards wrapped in a sticky anchor? | liquidGL anchors its canvas to the pane's nearest fixed/sticky ancestor and shares one canvas per (snapshot, anchor, zIndex) group. One sticky wrapper means six lenses share a single renderer instead of six full-page snapshots. The wrapper has zero travel, so it never actually pins. |
| Do the panes work while scrolling? | Yes. The snapshot is a full-page raster; the shader samples it at the pane's current viewport position, so content refracts live as it scrolls beneath the header. |
| What happens on theme switch? | The snapshot is re-captured with the new palette and each pane's content copy re-rasterises; the tint is theme-agnostic so it needs no change. |
| What happens on phones? | The header and hero keep the WebGL effect; the tall project cards drop to the CSS `backdrop-filter` fallback (Safari is unstable with lenses above ~half the viewport). |
| Can I change the tint? | Set `tint` to any CSS colour; the alpha is the dye strength (`0` leaves the glass clear). Update `--glass-fill` to keep the CSS fallback in step. |
| Why are there no images inside lenses? | The snapshot rasteriser needs same-origin/CORS-clean assets. The page uses none inside panes — external images stay in live content above the glass, which is never rasterised. |

---

## Browser Support

| Browser | Supported |
| :------ | :-------- |
| Google Chrome | ✅ |
| Safari | ✅ |
| Firefox | ✅ |
| Microsoft Edge | ✅ |

On any browser without WebGPU/WebGL the CSS `backdrop-filter` fallback renders a frosted approximation automatically.

## Important Notes

- No CSS animations run *behind* a pane — the only animated backdrop element (the dragon canvas) is excluded from the snapshot on purpose. If animated DOM is ever placed behind a pane, register it with `liquidGL.registerDynamic(...)` *after* init.
- The header's hairline border is a `::after` layer (`z-index: 3`) because the pane's own border paints beneath the renderer canvas.
- `html { overflow-x: clip }` absorbs the renderer canvas's transient positioning without creating a scroll container (which would break the sticky anchor).
- Panes get `pointer-events: none` from the library; their content children stay fully interactive, and clicks on empty glass fall through to the page (dragon fire-breath included).

---

## Theme

Black and white only, with **Black as the default** — **Black** (white ink on near-black) and **White** (black ink on white), chosen with the two-swatch picker in the header. The choice persists in `localStorage["site-theme"]` and is shared with `cv.html`.

An interactive arcade **Ender Dragon**, together with its ambient mobs, is drawn in full colour on a fixed `<canvas>` behind the page on both modes; the page chrome and the glass stay black and white.

## Publish

GitHub Pages serves this repository root from `main` → https://xyzouktik.github.io

## License

MIT — see [LICENSE.txt](./LICENSE.txt). liquidGL v3.0.0 is MIT © NaughtyDuk (https://liquidgl.naughtyduk.com).
