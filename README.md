# zahid.dev

**[unrealzahid.netlify.app](https://main-portfolio-eight-iota.vercel.app/)**

Single `index.html`. No build step, no bundler, no framework — just HTML, CSS, and JS with one CDN dependency (Three.js for the globe).

---

## Features

| | |
|---|---|
| Splash screen | ASCII rain with a letter-by-letter `ZAHID` reveal painted on canvas |
| Globe | Interactive Three.js globe — Dhaka marker, mouse-tracked rotation, orbital geometry |
| Terminals | Live-typed bash terminal in About; JS object terminal in Contact — both syntax-highlighted |
| Projects | 3-column card grid with a character-scramble effect on hover |
| Stack | Icon grid with staggered pulse animation |
| Contact | Headline cycles through four phrases with a per-character scramble-in every 3.5s |
| Theme | Dark / light — type `dark` or `light` anywhere, or click the Z logo |
| Cursor | Custom crosshair (desktop only), compositor-threaded via `transform` |
| Misc | Scroll progress bar, scroll-triggered reveals, go-to-top button, mobile nav overlay |

---

## How it was built

Everything lives in one file. CSS and JS are inline — no external stylesheets, no modules, no transpilation.

### Globe

Three.js r128 via CDN. The wireframe icosahedron, orbital arcs, compass ring, bracket markers, and Dhaka star sprite are built entirely with `LineBasicMaterial` and `SpriteMaterial`. Every material reference is pushed into a `_trackedLineMats[]` array at creation time, so `_updateGlobeTheme()` can recolor all of them on a theme switch in a single pass — no geometry is rebuilt.

### Splash

Canvas-based ASCII rain loop using `requestAnimationFrame`. Each frame draws a low-opacity dark fill over the previous frame, which makes older characters fade naturally without explicit tracking. The `ZAHID` title is measured and drawn at `800 weight Syne` — the font is preloaded with `document.fonts.load('800 100px "Syne"')` before the loop starts. Without this, the first frame renders with the fallback font and the measured letter widths are wrong, breaking the centred layout.

### Terminal typing

Each line types one character at a time via `setTimeout`. When a line finishes, the raw text node is swapped for a span-annotated HTML string — keywords, variables, strings, punctuation, and comments all get their own class. The colour palette is white/gray only, differentiated by opacity (`0.22` for punctuation, `0.95` for keywords) and `text-shadow` glow intensity.

### Scramble effect

On project card hover, the title shuffles through random characters and resolves left-to-right over roughly 15 frames. The contact headline uses a randomised per-character order for a more organic dissolve, cycling four phrases on a 3.5s interval.

### Theme switching

CSS custom properties on `:root` for dark and `body.light` for light. Three.js materials sit outside the DOM, so they're recolored via a dedicated `_updateGlobeTheme()` callback that runs whenever `toggleTheme()` fires — and also once immediately after the globe initialises, in case the page loads in light mode.

### Scroll reveals

`IntersectionObserver` on every `.rv` and `.rvs` element. `will-change: opacity, transform` is declared upfront so the browser promotes those elements to compositor layers before the animation triggers, avoiding a repaint on scroll.

### Cursor

A `<div>` with two line elements positioned via `transform: translate(x, y)` rather than `left` / `top`. This keeps all movement on the compositor thread and avoids sub-pixel rounding stutter. The lerp factor is `1.0` — the crosshair tracks the mouse exactly with no lag.

### Performance notes

- Scroll handler is gated behind a `requestAnimationFrame` flag — fires at most once per frame
- Globe mouse influence lerp is `0.07` — gives the globe a sense of weight
- `will-change` is set on every animated element (cards, logo items, go-to-top button, nav indicator)
- `overscroll-behavior: none` prevents rubber-band bounce from fighting scroll animations on mobile

---

## Tech

| | |
|---|---|
| HTML · CSS · JS | Core — no framework |
| [Three.js r128](https://threejs.org) | Globe |
| Bebas Neue · JetBrains Mono · Syne · DM Sans | Fonts via Google Fonts |
| [Netlify](https://netlify.com) | Hosting |

---

## Running locally

```
git clone https://github.com/UnrealZahid101894/portfolio
open index.html
```

No install, no server. The file works directly in a browser.

If you want to modify it — everything is in one file, sections are separated by comment banners (`/* ── SECTION NAME ── */`), and Ctrl+F will get you anywhere.

---

## Contact

`jahidulislam01018940@gmail.com` · [GitHub](https://github.com/UnrealZahid101894) · [LinkedIn](https://linkedin.com/in/jahidul-islam-672461333)
