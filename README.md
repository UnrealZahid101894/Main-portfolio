<div align="center">

# zahid.dev

**[unrealzahid.dev →](https://main-portfolio-eight-iota.vercel.app/)**

single-file portfolio. no framework, no build step, no bundler.

HTML CSS JS Three.js r128

</div>

## features

- **Splash** — ASCII rain, letter-by-letter `ZAHID` reveal
- **Globe** — Three.js wireframe globe, Dhaka marker, mouse-tracked rotation
- **Terminals** — live-typed bash terminal (About) + JS object terminal (Contact), syntax highlighted
- **Project cards** — character-scramble title on hover
- **Contact headline** — 4 phrases, per-character scramble-dissolve, every 3.5s
- **Cursor** — custom crosshair, zero-lag, compositor-threaded
- **Extras** — scroll progress bar, scroll reveals, go-to-top, mobile nav overlay

---

## the tricky bits

**Globe** — every material gets pushed into `_trackedLineMats[]` at creation, so the whole globe recolors in one pass with no geometry rebuild.

**Splash** — the `ZAHID` title is measured before it's drawn. Skip force-loading `Syne` first and the first frame measures in a fallback font, breaking the centered layout.

**Terminal** — types the raw text first, then swaps in span-annotated HTML once a line finishes. Keeps syntax highlighting from breaking the typing animation.

**Cursor** — moves via `transform: translate()` instead of `top`/`left`, keeping it on the compositor thread with zero stutter.

**Scroll** — `will-change` declared upfront so elements are promoted to their own GPU layer before the animation starts, not during. `overscroll-behavior: none` stops rubber-band scroll from fighting the reveal animations.

---

## stack

```
HTML · CSS · JS ─────────── core, no framework
Three.js r128 ────────────── globe
Bebas Neue / JetBrains Mono
Syne / DM Sans ───────────── Google Fonts
Vercel ───────────────────── hosting
```

---

## run locally

```bash
git clone https://github.com/UnrealZahid101894/Main-portfolio
cd Main-portfolio
open index.html
```

no install · no server · no config

everything's in one file, split by `/* ── SECTION NAME ── */` banners. Ctrl+F and go.

---

`jahidulislam01018940@gmail.com` · [GitHub](https://github.com/UnrealZahid101894) · [LinkedIn](https://linkedin.com/in/jahidul-islam-672461333)
