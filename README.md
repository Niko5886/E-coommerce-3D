<div align="center">

# LTX — The world model

**A full-viewport cinematic fashion scene with click-driven, pre-rendered video state transitions.**

Vanilla HTML + CSS + JavaScript · zero dependencies · a single self-contained `index.html`

</div>

---

## Overview

A centered character stands between pale-blue architectural walls. A frosted-glass
controller bar lets the visitor switch **Scene**, **Lighting**, **Clothing** or **Cast**.
Clicking a control plays a pre-generated video transition, holds the destination on its
final frame, and **Reset** plays the paired reverse clip back to the base state.

Everything is click-driven — **not** scroll-scrubbed. No generation happens at runtime,
no autoplay, no looping, no audio. All media streams remotely, so the page loads zero
local assets.

## Highlights

- **Seam-safe video player** — reveals a clip only once a decoded frame *from that request*
  is ready (`requestVideoFrameCallback` with a stale-frame guard), so there is no black
  flash, base-frame blink or crop jump at either seam.
- **Strict state machine** — `base → forward → selected → reverse → base`. No
  branch-to-branch jumps; Reset always returns to base first.
- **Liquid-glass controller** — a sliding capsule follows hover / keyboard focus, collapses
  to a single centered pill on selection, and expands again on reset. Pure CSS
  `backdrop-filter` glass material, no canvas or WebGL.
- **Synchronous input lock** — rapid or double clicks can never queue competing
  transitions; every async callback is guarded by a transition token.
- **Background-tab safe** — frame-callback deadlines pause while the tab is hidden, so a
  backgrounded tab never fires a false timeout.
- **Accessible** — real buttons/links, keyboard operable, a polite live region announcing
  loading / selection / errors, focus restoration, and `prefers-reduced-motion` support.
- **Fully responsive** — desktop, tablet, phone portrait, and short landscape layouts.

## Run locally

The page loads its own fonts and video from remote CDNs; you only need to serve the file
over HTTP (opening it directly via `file://` blocks some browser features).

```bash
# from the project folder
python -m http.server 8777
# then open http://localhost:8777/index.html
```

Any static server works (`npx serve`, VS Code Live Server, etc.).

## Tech

| | |
|---|---|
| **Markup / styling** | Hand-written HTML5 + modern CSS (grid, `backdrop-filter`, `dvh`, custom properties) |
| **Logic** | ES5-compatible vanilla JavaScript, no build step, no framework |
| **Font** | [Manrope](https://fonts.google.com/specimen/Manrope) via Google Fonts |
| **Media** | Eight pre-rendered `.mp4` clips served from Cloudflare R2 |

## Structure

```
E-coommerce 3D/
├── index.html   # the entire app — markup, styles and logic in one file
├── README.md
└── LICENSE
```

## License

Released under the [MIT License](LICENSE).

Video footage, the LTX name and wordmark belong to their respective owners and are
referenced here for a design/engineering demonstration only.
