<div align="center">

# zahid.dev

**[unrealzahid.dev →](https://main-portfolio-eight-iota.vercel.app/)**

single-file portfolio. no framework, no build step, no bundler.

`HTML` `CSS` `JS` `Three.js r128`

</div>

---

## features

| | |
|---|---|
| **Splash** | ASCII rain → letter-by-letter `ZAHID` reveal |
| **Globe** | Three.js wireframe globe, Dhaka marker, mouse-tracked rotation |
| **Terminals** | Live-typed bash terminal (About) + JS object terminal (Contact), syntax highlighted |
| **Project cards** | Character-scramble title on hover |
| **Contact headline** | 4 phrases, per-character scramble-dissolve, every 3.5s |
| **Cursor** | Custom crosshair, zero-lag, compositor-threaded |
| **Extras** | Scroll progress bar · scroll reveals · go-to-top · mobile nav overlay |

---

## the tricky bits

| what | why it matters |
|---|---|
| Globe materials tracked in `_trackedLineMats[]` | recolor everything in one pass, no rebuild |
| Splash force-loads `Syne` before drawing | fallback font = wrong measured width = off-center title |
| Terminal types raw text first, swaps to spans after | syntax highlighting without breaking the typing animation |
| Cursor uses `transform: translate()` not `top`/`left` | stays on compositor thread → no stutter |
| `will-change` set upfront on animated elements | promotes to GPU layer before animation starts, not during |
| `overscroll-behavior: none` | kills rubber-band scroll fighting the reveal animations |

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

<div align="center">

`jahidulislam01018940@gmail.com` · [GitHub](https://github.com/UnrealZahid101894) · [LinkedIn](https://linkedin.com/in/jahidul-islam-672461333)

</div>
