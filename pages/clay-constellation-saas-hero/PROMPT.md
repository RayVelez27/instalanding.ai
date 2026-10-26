INSTALANDING.AI · Clay Constellation SaaS Hero

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Clay Constellation SaaS Hero · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/clay-constellation-saas-hero

traffo-constellation.html:
```html
<!DOCTYPE html>
<!--
  INSTALANDING.AI · Clay Constellation SaaS Hero
  slug     clay-constellation-saas-hero
  prompt   https://instalanding.ai/p/clay-constellation-saas-hero.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/clay-constellation-saas-hero
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of <style>: --bg #ebe9e1, --cream, --ink #0a0a0a, --ink-soft, clay families
            --mint / --yellow / --purple (each -light/-deep), --spring; button frame tokens --dot-size, --line-weight,
            --line-distance, --animation-speed, --dot-color, --line-color, --squish*. Fonts: Funnel Display, JetBrains Mono
  sections  nav, menu, hero, logos, stats, features, product, quote, testimonials, pricing, faq, cta, footer
  scripts   1 pixel type: turns each .px element's text into a CSS shape() clip-path (only where supported)
            2 chat demo: scripted conversation in the hero composer (the `script` array)
            3 pricing billing toggle   4 metric fills on view, CTA form, footer wordmark   5 mobile menu
            6 GSAP 3.12.5 + ScrollTrigger (cdnjs): entrance timeline, hero scrub, per-word heading reveals, card tilt
  assets    none binary: inline SVG icons/logos, SVG turbulence grain; fonts from Google Fonts

  ADAPTING
  - .px text is drawn from a per-letter glyph table: only a-z (lowercased) and spaces render; anything else becomes a
    space. Browsers without clip-path shape() keep it as plain text.
  - Hidden start states are set by GSAP in JS (gsap.set), not CSS, so the page renders complete if the CDN fails.
    Tweens that move hoverable elements end with clearProps; keep that or hover transforms stay pinned.
  - Headings are split into per-word masks by walking text nodes, so inner accent spans survive; keep markup inside them.
  - The button frame reads --line-color / --dot-color; the dark CTA slab re-points them on .final-cta .btn-wrapper.
    Stats render from data-num / data-decimals / data-prefix / data-suffix, not from the visible text.
-->
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Traffo Landing Page</title>
<meta name="description" content="Traffo AI landing page: an AI analyst you ask about your traffic, shown in a live chat demo, with GSAP entrance and scroll reveals on warm paper." />

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet" />

<style>
:root {
  color-scheme: light;
  --bg: #ebe9e1;
  --bg-warm: #efece4;
  --ink: #0a0a0a;
  --ink-soft: #6a6a64;
  --cream: #f6f3eb;
  --cream-2: #f1ede2;
  --cream-line: #e8e4d6;
  --mint: #c8ecc8;
  --mint-light: #dcf5dc;
  --mint-deep: #95c598;
  --yellow: #fde351;
  --yellow-light: #ffe760;
  --yellow-deep: #f7d130;
  --yellow-line: #d8b020;
  --dot-size: 6px;
  --line-weight: 1px;
  --line-distance: 0.9rem 1.1rem;
  --animation-speed: 0.35s;
  --dot-color: #666;
  --line-color: #999;
  --squish: 30% / 200%;
  --squish-hover: 10% / 200%;
  --squish-active: 20% / 200%;
  --purple: #dcd0ee;
  --purple-light: #ece2f8;
  --purple-deep: #ab9bd0;
  --cream-deep: #ddd5bf;
  --spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; overflow-x: clip; }

body {
  background: var(--bg);
  font-family: "Funnel Display", system-ui, sans-serif;
  color: var(--ink);
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
  line-height: 1.5;
}

body::before {
  content: "";
  position: fixed;
  inset: 0;
  background-image: url("data:image/svg+xml;utf8,<svg viewBox='0 0 240 240' xmlns='http://www.w3.org/2000/svg'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='3' stitchTiles='stitch'/></filter><rect width='100%25' height='100%25' filter='url(%23n)' opacity='0.55'/></svg>");
  opacity: 0.1;
  pointer-events: none;
  z-index: 200;
  mix-blend-mode: multiply;
}

.ambient-1, .ambient-2 {
  position: fixed;
  border-radius: 50%;
  pointer-events: none;
  z-index: 0;
}
.ambient-1 {
  top: 10%; right: -10%;
  width: 600px; height: 600px;
  background: radial-gradient(circle, rgba(253, 227, 81, 0.16) 0%, transparent 60%);
  filter: blur(80px);
}
.ambient-2 {
  bottom: -10%; left: -5%;
  width: 500px; height: 500px;
  background: radial-gradient(circle, rgba(220, 208, 238, 0.18) 0%, transparent 60%);
  filter: blur(60px);
}

a { text-decoration: none; color: inherit; }
svg { display: block; }

:focus-visible {
  outline: 3px solid var(--ink);
  outline-offset: 3px;
  border-radius: 8px;
}

.sr-only {
  position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px;
  overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; border: 0;
}

.skip {
  position: absolute;
  left: 16px; top: -60px;
  z-index: 300;
  background: var(--ink);
  color: #fff;
  padding: 10px 18px;
  border-radius: 10px;
  font-size: 13px;
  transition: top 0.25s ease;
}
.skip:focus { top: 16px; }

.top-rule {
  position: fixed; top: 0; left: 0; right: 0; z-index: 60;
  height: 14px;
  background: linear-gradient(180deg, var(--yellow) 0%, #fbd640 100%);
}
.site-header {
  position: fixed; top: 14px; left: 0; right: 0; z-index: 55;
  display: flex; justify-content: center;
  padding: 4px clamp(14px, 3vw, 40px);
  pointer-events: none;
}
.nav-frame {
  position: relative;
  display: inline-flex;
  padding: var(--line-distance);
  max-width: 100%;
}
.nav-pill {
  pointer-events: auto;
  display: inline-flex; align-items: center; gap: 4px;
  padding: 6px;
  border-radius: 17px / 50%;
  transition: border-radius 0.3s ease-in-out;
  background: linear-gradient(180deg, #1a1a1a 0%, #0a0a0a 100%);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    inset 0 -1px 2px rgba(0, 0, 0, 0.5),
    0 2px 0 #000,
    0 6px 14px -2px rgba(0, 0, 0, 0.25),
    0 16px 30px -10px rgba(0, 0, 0, 0.2);
  max-width: 100%;
}
.logo {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: 17px;
  letter-spacing: -0.02em;
  color: #fff;
  padding: 10px 16px 11px;
  display: flex; align-items: center; gap: 9px;
  white-space: nowrap;
}
.logo-ai {
  margin-left: 6px;
  font-family: "JetBrains Mono", monospace;
  font-size: 10px; font-weight: 600; letter-spacing: 0.1em;
  color: var(--ink);
  background: var(--yellow);
  padding: 2px 6px 1px;
  border-radius: 5px / 50%;
  vertical-align: 2px;
}
.logo-cube { width: 20px; height: 20px; display: grid; place-items: center; }
.logo-cube svg { width: 20px; height: 20px; }
.header-nav {
  display: flex; align-items: center; gap: 2px;
  font-size: 14.5px; font-weight: 500;
}
.header-nav a {
  color: #ccc;
  padding: 10px 15px 11px;
  border-radius: 11px / 50%;
  display: flex; align-items: center; gap: 4px;
  letter-spacing: -0.005em;
  transition: color 0.2s, background 0.2s;
}
.header-nav a:hover { color: #fff; background: rgba(255, 255, 255, 0.08); }
.book-cta {
  margin-left: 6px;
  padding: 10px 20px 11px;
  border-radius: 11px / 50%;
  border: 1px solid var(--yellow-line);
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  color: var(--ink);
  font-size: 14.5px; font-weight: 600; letter-spacing: -0.005em;
  white-space: nowrap;
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.6),
    inset 0 -1px 2px rgba(180, 140, 30, 0.3),
    0 2px 4px rgba(200, 160, 30, 0.3);
  transition: transform 0.2s ease-in-out, border-radius 0.3s ease-in-out;
}
.book-cta:hover, .book-cta:focus-visible { border-radius: 4px / 50%; }
.book-cta:active { transform: scale(0.98); border-radius: 8px / 50%; }
.nav-pill:has(.book-cta:hover),
.nav-pill:has(.book-cta:focus-visible) { border-radius: 6px / 50%; }
.nav-pill:has(.book-cta:active) { border-radius: 11px / 50%; }

.hero {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 24px;
  padding: 40px clamp(20px, 4vw, 56px);
  align-items: center;
  position: relative;
  z-index: 5;
  min-height: 720px;
}
.hero-title {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 800;
  font-size: clamp(40px, 6vw, 96px);
  line-height: 0.96;
  letter-spacing: -0.042em;
  margin-bottom: 36px;
}
.title-line { display: block; overflow: hidden; padding-bottom: 0.1em; white-space: nowrap; }
.title-inner { display: inline-block; will-change: transform; }
.hero-desc {
  font-size: 16px;
  line-height: 1.55;
  color: var(--ink-soft);
  max-width: 380px;
}

.hero {
  margin: 128px clamp(12px, 2.2vw, 30px) 0;
  border-radius: 38px;
  background: #ffffff;
  box-shadow:
    0 18px 70px -14px rgba(92, 82, 24, 0.22),
    0 40px 90px -40px rgba(15, 15, 15, 0.35),
    inset 0 -14px 26px -6px rgba(92, 82, 30, 0.16),
    inset 0 3px 0 rgba(255, 255, 255, 0.9);
}

.glass {
  position: absolute;
  z-index: 6;
  -webkit-backdrop-filter: blur(7px);
  backdrop-filter: blur(7px);
  background: rgba(255, 255, 255, 0.42);
  border: 0.5px solid rgba(255, 255, 255, 0.55);
  pointer-events: none;
}
.glass--tab {
  top: -34px;
  left: clamp(18px, 4vw, 64px);
  display: grid;
  place-items: center;
  padding: 0 22px;
  height: 92px;
  border-radius: 22px;
  box-shadow:
    0 10px 30px -8px rgba(62, 54, 30, 0.28),
    inset 0 -12px 22px 0 rgba(171, 155, 208, 0.42);
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: 12px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  line-height: 1.5;
  text-align: center;
  color: #3b3a2a;
}
.glass--disc {
  right: -26px;
  bottom: -26px;
  width: 104px;
  height: 104px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.34);
  box-shadow:
    0 14px 28px -6px rgba(62, 54, 30, 0.32),
    inset 0 -16px 26px -6px rgba(171, 155, 208, 0.55),
    inset 0 6px 14px 0 rgba(255, 255, 255, 0.9);
}

.title-line.sticker { padding: 0.02em 0.12em 0.16em 0; margin-bottom: -0.1em; }
.title-line.sticker .title-inner {
  color: var(--yellow);
  -webkit-text-stroke: 0.045em var(--ink);
  text-stroke: 0.045em var(--ink);
  paint-order: stroke fill;
  text-shadow: 0.05em 0.06em 0 var(--ink);
  letter-spacing: -0.012em;
}
.title-mark { position: relative; }
.title-mark::before {
  content: "";
  position: absolute;
  z-index: -1;
  left: -0.06em;
  right: -0.06em;
  bottom: 0.06em;
  height: 0.36em;
  background: var(--yellow);
  border-radius: 0.06em;
  transform: rotate(-1.2deg);
}

@media (max-width: 900px) {
  .glass--tab {
    height: 62px; font-size: 9.5px; letter-spacing: 0.13em;
    padding: 0 14px; top: -22px; border-radius: 16px;
  }
  .glass--disc { width: 76px; height: 76px; right: -18px; bottom: -18px; }
  .hero { border-radius: 28px; }
  .hero { padding-top: 62px; }
}

.btn-wrapper {
  position: relative;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: var(--line-distance);
  background-color: transparent;
  transition: background-color 0.3s ease-in-out;
  user-select: none;
}
.btn-wrapper:has(.btn:hover),
.btn-wrapper:focus-within,
.nav-frame:has(.book-cta:hover),
.nav-frame:has(.book-cta:focus-visible) {
  animation: frame-wash calc(var(--animation-speed) * 4) ease-in-out forwards;
}
@keyframes frame-wash {
  80% { background-color: transparent; }
  100% { background-color: #fde35140; }
}

.btn {
  position: relative;
  display: inline-flex;
  justify-content: center;
  align-items: center;
  padding: 0.8rem 1.25rem;
  background-color: var(--yellow);
  background-image: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  border: none;
  color: rgba(0, 0, 0, 0.82);
  font-family: "Funnel Display", system-ui, sans-serif;
  font-size: 1rem;
  font-weight: 600;
  text-transform: capitalize;
  border-radius: var(--squish);
  cursor: pointer;
  box-shadow:
    0 0 0 1px #0003,
    0 1px 1px rgba(3, 7, 18, 0.02),
    0 5px 4px rgba(3, 7, 18, 0.04),
    0 12px 9px rgba(3, 7, 18, 0.06),
    0 20px 15px rgba(3, 7, 18, 0.08),
    0 32px 24px rgba(3, 7, 18, 0.1);
  transition:
    background-color 0.2s ease-in-out,
    transform 0.2s ease-in-out,
    box-shadow 0.2s ease-in-out,
    border-radius 0.3s ease-in-out,
    color 0.2s ease-in-out;
}
.btn:hover { background-color: #fff; transform: scale(1.05); border-radius: var(--squish-hover); }
.btn:active { background-color: var(--yellow); transform: scale(0.98); border-radius: var(--squish-active); }
.btn.btn-sm { padding: 0.55rem 0.95rem; font-size: 0.85rem; }
.btn.btn-sm .btn-svg { height: 17px; }

.btn-svg {
  margin-left: 0.5rem;
  height: 22px;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke: #0007;
  fill: #fffa;
  transition: all 0.3s ease-in-out;
}
.btn:hover .btn-svg { stroke: #0008; fill: var(--yellow); }
.btn:active .btn-svg { stroke: #0009; fill: var(--yellow-light); }

.dot {
  position: absolute;
  width: var(--dot-size);
  aspect-ratio: 1;
  border-radius: 50%;
  background-color: var(--dot-color);
  transition: all 0.3s ease-in-out;
  opacity: 0;
}
.btn-wrapper:has(.btn:hover) .dot.top.left,
.btn-wrapper:focus-within .dot.top.left,
.nav-frame:has(.book-cta:hover) .dot.top.left,
.nav-frame:has(.book-cta:focus-visible) .dot.top.left {
  top: 50%; left: 20%;
  animation: move-top-left var(--animation-speed) ease-in-out forwards;
}
@keyframes move-top-left {
  90% { opacity: 0.6; }
  100% { top: calc(var(--dot-size) * -0.5); left: calc(var(--dot-size) * -0.5); opacity: 1; }
}
.btn-wrapper:has(.btn:hover) .dot.top.right,
.btn-wrapper:focus-within .dot.top.right,
.nav-frame:has(.book-cta:hover) .dot.top.right,
.nav-frame:has(.book-cta:focus-visible) .dot.top.right {
  top: 50%; right: 20%;
  animation: move-top-right var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 0.6);
}
@keyframes move-top-right {
  80% { opacity: 0.6; }
  100% { top: calc(var(--dot-size) * -0.5); right: calc(var(--dot-size) * -0.5); opacity: 1; }
}
.btn-wrapper:has(.btn:hover) .dot.bottom.right,
.btn-wrapper:focus-within .dot.bottom.right,
.nav-frame:has(.book-cta:hover) .dot.bottom.right,
.nav-frame:has(.book-cta:focus-visible) .dot.bottom.right {
  bottom: 50%; right: 20%;
  animation: move-bottom-right var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 1.2);
}
@keyframes move-bottom-right {
  80% { opacity: 0.6; }
  100% { bottom: calc(var(--dot-size) * -0.5); right: calc(var(--dot-size) * -0.5); opacity: 1; }
}
.btn-wrapper:has(.btn:hover) .dot.bottom.left,
.btn-wrapper:focus-within .dot.bottom.left,
.nav-frame:has(.book-cta:hover) .dot.bottom.left,
.nav-frame:has(.book-cta:focus-visible) .dot.bottom.left {
  bottom: 50%; left: 20%;
  animation: move-bottom-left var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 1.8);
}
@keyframes move-bottom-left {
  80% { opacity: 0.6; }
  100% { bottom: calc(var(--dot-size) * -0.5); left: calc(var(--dot-size) * -0.5); opacity: 1; }
}

.line { position: absolute; transition: all 0.3s ease-in-out; }
.line.horizontal {
  height: var(--line-weight);
  width: 100%;
  background-image: repeating-linear-gradient(90deg,
    #0000 0 calc(var(--line-weight) * 2),
    var(--line-color) calc(var(--line-weight) * 2) calc(var(--line-weight) * 4));
}
.line.vertical {
  width: var(--line-weight);
  height: 100%;
  background-image: repeating-linear-gradient(0deg,
    #0000 0 calc(var(--line-weight) * 2),
    var(--line-color) calc(var(--line-weight) * 2) calc(var(--line-weight) * 4));
}
.line.top { top: calc(var(--line-weight) * -0.5); transform-origin: top left; transform: rotate(5deg) scaleX(0); }
.line.bottom { bottom: calc(var(--line-weight) * -0.5); transform-origin: bottom right; transform: rotate(5deg) scaleX(0); }
.line.left { left: calc(var(--line-weight) * -0.5); transform-origin: bottom left; transform: rotate(0deg) scaleY(0); }
.line.right { right: calc(var(--line-weight) * -0.5); transform-origin: top right; transform: rotate(5deg) scaleY(0); }

.btn-wrapper:has(.btn:hover) .line.top,
.btn-wrapper:focus-within .line.top,
.nav-frame:has(.book-cta:hover) .line.top,
.nav-frame:has(.book-cta:focus-visible) .line.top {
  animation: draw-x var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 0.8);
}
.btn-wrapper:has(.btn:hover) .line.right,
.btn-wrapper:focus-within .line.right,
.nav-frame:has(.book-cta:hover) .line.right,
.nav-frame:has(.book-cta:focus-visible) .line.right {
  animation: draw-y var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 1.4);
}
.btn-wrapper:has(.btn:hover) .line.bottom,
.btn-wrapper:focus-within .line.bottom,
.nav-frame:has(.book-cta:hover) .line.bottom,
.nav-frame:has(.book-cta:focus-visible) .line.bottom {
  animation: draw-x var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 2);
}
.btn-wrapper:has(.btn:hover) .line.left,
.btn-wrapper:focus-within .line.left,
.nav-frame:has(.book-cta:hover) .line.left,
.nav-frame:has(.book-cta:focus-visible) .line.left {
  animation: draw-y var(--animation-speed) ease-in-out forwards;
  animation-delay: calc(var(--animation-speed) * 2.4);
}
@keyframes draw-x { 100% { transform: rotate(0deg) scaleX(1); } }
@keyframes draw-y { 100% { transform: rotate(0deg) scaleY(1); } }

.framed { position: relative; }
.framed::before,
.framed::after {
  content: "";
  position: absolute;
  pointer-events: none;
  opacity: 0;
  transition: opacity 0.3s ease-in-out;
}
.framed::before {
  inset: -10px -14px;
  background:
    repeating-linear-gradient(90deg, #0000 0 2px, var(--line-color) 2px 4px) top left / 100% var(--line-weight) no-repeat,
    repeating-linear-gradient(90deg, #0000 0 2px, var(--line-color) 2px 4px) bottom left / 100% var(--line-weight) no-repeat,
    repeating-linear-gradient(0deg, #0000 0 2px, var(--line-color) 2px 4px) top left / var(--line-weight) 100% no-repeat,
    repeating-linear-gradient(0deg, #0000 0 2px, var(--line-color) 2px 4px) top right / var(--line-weight) 100% no-repeat;
}
.framed::after {
  inset: calc(-10px - var(--dot-size) / 2) calc(-14px - var(--dot-size) / 2);
  background:
    radial-gradient(circle at 0 0, var(--dot-color) calc(var(--dot-size) / 2), #0000 calc(var(--dot-size) / 2)),
    radial-gradient(circle at 100% 0, var(--dot-color) calc(var(--dot-size) / 2), #0000 calc(var(--dot-size) / 2)),
    radial-gradient(circle at 0 100%, var(--dot-color) calc(var(--dot-size) / 2), #0000 calc(var(--dot-size) / 2)),
    radial-gradient(circle at 100% 100%, var(--dot-color) calc(var(--dot-size) / 2), #0000 calc(var(--dot-size) / 2));
}
.framed:hover::before { opacity: 1; transition-delay: 0.05s; }
.framed:hover::after { opacity: 1; transition-delay: calc(var(--animation-speed) * 0.8); }

.hero-right { display: grid; place-items: center; position: relative; min-width: 0; }

.chat-stage { width: 100%; max-width: 470px; position: relative; }

.chat {
  height: 600px;
  display: flex;
  flex-direction: column;
  border-radius: 34px;
  background: linear-gradient(180deg, var(--cream) 0%, var(--cream-2) 100%);
  border: 1px solid var(--cream-line);
  box-shadow:
    inset 0 3px 0 rgba(255, 255, 255, 0.9),
    inset 0 -10px 22px -8px rgba(92, 82, 30, 0.14),
    0 22px 50px -18px rgba(92, 82, 24, 0.3),
    0 50px 90px -50px rgba(15, 15, 15, 0.35);
  overflow: hidden;
  position: relative;
}

.chat-head {
  margin: 10px 10px 0;
  padding: 10px 14px 10px 10px;
  display: flex;
  align-items: center;
  gap: 12px;
  border-radius: 24px;
  background: linear-gradient(180deg, #1a1a1a 0%, #0a0a0a 100%);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.08),
    inset 0 -1px 2px rgba(0, 0, 0, 0.5),
    0 2px 0 #000,
    0 8px 16px -6px rgba(0, 0, 0, 0.3);
  color: #fff;
}
.chat-avatar {
  flex: none;
  width: 38px; height: 38px;
  border-radius: 13px;
  display: grid; place-items: center;
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.6), inset 0 -2px 3px rgba(180, 140, 30, 0.35);
  color: var(--ink);
}
.chat-avatar svg { width: 20px; height: 20px; }
.chat-who { min-width: 0; flex: 1; }
.chat-name { font-size: 15px; font-weight: 700; letter-spacing: -0.01em; line-height: 1.2; }
.chat-status {
  font-family: "JetBrains Mono", monospace;
  font-size: 10.5px;
  letter-spacing: 0.04em;
  color: #a9a9a2;
  display: flex; align-items: center; gap: 6px;
  white-space: nowrap; overflow: hidden; text-overflow: ellipsis;
}
.chat-status::before {
  content: "";
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--mint);
  box-shadow: 0 0 0 3px rgba(200, 236, 200, 0.18);
  flex: none;
}
.chat-tag {
  flex: none;
  font-family: "JetBrains Mono", monospace;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: var(--ink);
  background: var(--cream);
  padding: 5px 9px 4px;
  border-radius: 8px / 50%;
}

.chat-log {
  flex: 1;
  min-height: 0;
  overflow-y: auto;
  overscroll-behavior: contain;
  padding: 22px 18px 12px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  scrollbar-width: none;
  -webkit-mask-image: linear-gradient(180deg, transparent 0, #000 22px);
  mask-image: linear-gradient(180deg, transparent 0, #000 22px);
}
.chat-log::-webkit-scrollbar { display: none; }

.msg { display: flex; align-items: flex-end; gap: 9px; max-width: 88%; }
.msg.from-ai { align-self: flex-start; }
.msg.from-you { align-self: flex-end; flex-direction: row-reverse; }
.msg .chat-avatar { width: 28px; height: 28px; border-radius: 10px; margin-bottom: 18px; }
.msg .chat-avatar svg { width: 16px; height: 16px; }

.bubble-wrap { display: flex; flex-direction: column; gap: 5px; min-width: 0; }
.from-you .bubble-wrap { align-items: flex-end; }
.bubble {
  padding: 11px 14px 12px;
  font-size: 14.5px;
  line-height: 1.45;
  color: var(--ink);
  overflow-wrap: anywhere;
}
.from-ai .bubble {
  background: #fff;
  border-radius: 18px 18px 18px 6px;
  box-shadow: inset 0 -2px 0 rgba(92, 82, 30, 0.07), 0 2px 8px -2px rgba(92, 82, 30, 0.12);
}
.from-you .bubble {
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 60%, var(--yellow-deep) 100%);
  border-radius: 18px 18px 6px 18px;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.55), inset 0 -2px 2px rgba(180, 140, 30, 0.3), 0 2px 6px -2px rgba(200, 160, 30, 0.35);
}
.bubble strong { font-weight: 700; }
.stamp {
  font-family: "JetBrains Mono", monospace;
  font-size: 10px;
  letter-spacing: 0.04em;
  color: var(--ink-soft);
  padding-inline: 4px;
}

.msg.is-new .bubble { animation: bubble-pop 520ms cubic-bezier(0.34, 1.56, 0.64, 1) both; }
.from-ai.is-new .bubble { transform-origin: 0 100%; }
.from-you.is-new .bubble { transform-origin: 100% 100%; }
@keyframes bubble-pop {
  0% { transform: scale(0); opacity: 0; }
  40% { opacity: 1; }
  100% { transform: scale(1); opacity: 1; }
}

.typing { display: flex; gap: 5px; padding: 15px 16px; }
.typing i {
  width: 7px; height: 7px; border-radius: 50%;
  background: var(--ink);
  opacity: 0.55;
  animation: dot 0.45s cubic-bezier(0, 0, 0.15, 1) alternate infinite;
}
.typing i:nth-child(2) { animation-delay: 0.15s; }
.typing i:nth-child(3) { animation-delay: 0.3s; }
@keyframes dot { from { transform: translateY(2px) scaleY(0.8); } to { transform: translateY(-5px); } }

.mini-chart {
  margin-top: 10px;
  padding: 12px 12px 10px;
  border-radius: 14px;
  background: var(--cream);
  border: 1px solid var(--cream-line);
}
.mini-chart-head {
  display: flex; justify-content: space-between; align-items: baseline; gap: 8px;
  font-family: "JetBrains Mono", monospace;
  font-size: 10px; letter-spacing: 0.06em; text-transform: uppercase;
  color: var(--ink-soft);
  margin-bottom: 10px;
}
.mini-chart-head b { color: #b3261e; font-weight: 600; font-variant-numeric: tabular-nums; }
.bars { display: grid; grid-template-columns: repeat(7, 1fr); gap: 6px; height: 72px; align-items: end; }
.bar {
  height: var(--h);
  border-radius: 5px 5px 2px 2px;
  background: var(--ink);
  position: relative;
}
.bar.after { background: var(--yellow-deep); }
.bar.deploy::after {
  content: "";
  position: absolute; left: calc(100% + 2px); bottom: 0;
  height: 72px; width: 0;
  border-left: 1.5px dashed var(--ink-soft);
}
.bar-days {
  display: grid; grid-template-columns: repeat(7, 1fr); gap: 6px;
  margin-top: 6px;
  font-family: "JetBrains Mono", monospace; font-size: 9.5px; color: var(--ink-soft);
  text-align: center;
}

.chat-suggest {
  display: flex; gap: 6px; flex-wrap: wrap;
  padding: 4px 14px 8px;
}
.chip {
  font: inherit;
  font-size: 12.5px; font-weight: 500;
  color: var(--ink);
  background: #fff;
  border: 1px solid var(--cream-line);
  padding: 6px 11px 7px;
  border-radius: 9px / 50%;
  cursor: pointer;
  box-shadow: inset 0 -1.5px 0 rgba(92, 82, 30, 0.08);
  transition: border-radius 0.3s ease-in-out, background 0.2s;
}
.chip:hover { border-radius: 4px / 50%; background: var(--yellow-light); }

.composer {
  margin: 0 10px 10px;
  display: flex; align-items: center; gap: 8px;
  padding: 6px 6px 6px 16px;
  background: #fff;
  border: 1px solid var(--cream-line);
  border-radius: 17px / 50%;
  box-shadow: inset 0 2px 3px rgba(92, 82, 30, 0.06);
  transition: border-radius 0.3s ease-in-out;
}
.composer:focus-within { outline: 2px solid var(--ink); outline-offset: 2px; }
.composer:has(.send:hover) { border-radius: 6px / 50%; }
.composer textarea {
  flex: 1; min-width: 0;
  border: 0; outline: 0; resize: none; background: transparent;
  font: inherit; font-size: 14.5px; line-height: 1.4;
  color: var(--ink);
  height: 21px;
  padding: 0;
}
.composer textarea::placeholder { color: #8d8b82; }
.send {
  flex: none;
  display: inline-flex; align-items: center; gap: 6px;
  padding: 9px 14px 10px 16px;
  font: inherit; font-size: 14px; font-weight: 600;
  color: var(--ink);
  cursor: pointer;
  border: 1px solid var(--yellow-line);
  border-radius: 11px / 50%;
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.6), inset 0 -1px 2px rgba(180, 140, 30, 0.3);
  transition: border-radius 0.3s ease-in-out, transform 0.2s ease-in-out;
}
.send:hover { border-radius: 4px / 50%; }
.send:active { transform: scale(0.97); border-radius: 8px / 50%; }
.send svg { width: 16px; height: 16px; }

.stats-bar {
  padding: 80px clamp(20px, 4vw, 56px);
  background: var(--bg-warm);
  border-radius: 48px 48px 0 0;
  margin-top: 88px;
  position: relative;
  z-index: 5;
}
.stats-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 40px; }
.stat { padding: 32px 0; border-right: 1px solid rgba(0, 0, 0, 0.08); }
.stat:last-child { border-right: none; }
.stat-num {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: clamp(40px, 4.5vw, 72px);
  letter-spacing: -0.04em;
  line-height: 1;
  margin-bottom: 12px;
  font-variant-numeric: tabular-nums;
}
.stat-num .accent { color: var(--yellow-deep); }
.stat-label {
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: var(--ink-soft);
  font-weight: 500;
}

.features { padding: 120px clamp(20px, 4vw, 56px); background: var(--bg-warm); position: relative; }
.features-head {
  display: flex;
  justify-content: space-between;
  align-items: end;
  margin-bottom: 80px;
  gap: 60px;
}
.section-eyebrow {
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--ink-soft);
  margin-bottom: 24px;
  display: flex;
  align-items: center;
  gap: 12px;
}
.section-eyebrow::before { content: ""; width: 32px; height: 1.5px; background: var(--ink); }
.features-title {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: clamp(40px, 5vw, 72px);
  line-height: 1;
  letter-spacing: -0.035em;
  max-width: 720px;
}
.features-meta {
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: var(--ink-soft);
  line-height: 1.6;
  text-align: right;
}
.feature-cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
.feature-card {
  padding: 32px;
  border-radius: 36px;
  min-height: 340px;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  will-change: transform;
}
.feature-card.fc-mint {
  background: linear-gradient(165deg, var(--mint-light) 0%, var(--mint) 100%);
  box-shadow: inset 0 3px 0 rgba(255, 255, 255, 0.6), inset 0 -4px 0 rgba(0, 0, 0, 0.08),
    0 20px 40px rgba(149, 197, 152, 0.3), 0 40px 80px rgba(0, 0, 0, 0.06);
}
.feature-card.fc-yellow {
  background: linear-gradient(165deg, var(--yellow-light) 0%, var(--yellow) 100%);
  box-shadow: inset 0 3px 0 rgba(255, 255, 255, 0.5), inset 0 -4px 0 rgba(0, 0, 0, 0.12),
    0 20px 40px rgba(214, 170, 30, 0.28), 0 40px 80px rgba(0, 0, 0, 0.08);
}
.feature-card.fc-purple {
  background: linear-gradient(165deg, var(--purple-light) 0%, var(--purple) 100%);
  box-shadow: inset 0 3px 0 rgba(255, 255, 255, 0.6), inset 0 -4px 0 rgba(0, 0, 0, 0.08),
    0 20px 40px rgba(171, 155, 208, 0.3), 0 40px 80px rgba(0, 0, 0, 0.06);
}
.fc-num {
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.14em;
  margin-bottom: 24px;
  opacity: 0.6;
}
.feature-card h3 {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: 28px;
  line-height: 1.05;
  letter-spacing: -0.025em;
  margin-bottom: 16px;
}
.feature-card p { font-size: 14px; line-height: 1.55; opacity: 0.75; flex: 1; }
.fc-icon {
  width: 56px; height: 56px;
  border-radius: 18px;
  background: rgba(0, 0, 0, 0.08);
  display: grid;
  place-items: center;
  margin-top: 24px;
  box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.4), inset 0 -2px 0 rgba(0, 0, 0, 0.1);
}

.quote-section { padding: 140px clamp(20px, 4vw, 56px); text-align: center; }
.quote-mark {
  display: inline-block;
  font-family: "Funnel Display", system-ui, sans-serif;
  font-size: 120px;
  line-height: 0.4;
  color: var(--yellow-deep);
  margin-bottom: 24px;
}
.quote-text {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 600;
  font-size: clamp(32px, 4.5vw, 64px);
  line-height: 1.1;
  letter-spacing: -0.03em;
  max-width: 1000px;
  margin: 0 auto 32px;
}
.quote-author {
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  color: var(--ink-soft);
}

.final-cta { padding: 100px clamp(20px, 4vw, 56px) 120px; text-align: center; }
.final-cta-card {
  max-width: 1100px;
  margin: 0 auto;
  padding: clamp(48px, 7vw, 80px) clamp(24px, 5vw, 60px);
  border-radius: 48px;
  background: linear-gradient(165deg, #2a2a2a 0%, #0a0a0a 100%);
  color: #fff;
  position: relative;
  overflow: hidden;
  box-shadow: inset 0 3px 0 rgba(255, 255, 255, 0.15), inset 0 -5px 0 rgba(0, 0, 0, 0.5),
    0 30px 60px rgba(0, 0, 0, 0.3), 0 60px 120px rgba(0, 0, 0, 0.2);
}
.final-cta-h2 {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: clamp(40px, 5.5vw, 80px);
  line-height: 1;
  letter-spacing: -0.035em;
  margin-bottom: 32px;
  position: relative;
}
.final-cta-h2 .accent { color: var(--yellow); }
.final-cta p {
  font-size: 16px;
  color: rgba(255, 255, 255, 0.7);
  max-width: 540px;
  margin: 0 auto 40px;
  position: relative;
}
.final-cta .btn-wrapper { --line-color: rgba(255, 255, 255, 0.45); --dot-color: rgba(255, 255, 255, 0.75); }
.final-cta .btn { box-shadow: 0 0 0 1px #0006, 0 10px 24px rgba(0, 0, 0, 0.45); }
.orb { position: absolute; border-radius: 50%; pointer-events: none; }
.orb-1 {
  width: 200px; height: 200px;
  background: radial-gradient(circle, rgba(253, 227, 81, 0.22) 0%, transparent 70%);
  top: -50px; left: -50px;
  filter: blur(40px);
}
.orb-2 {
  width: 250px; height: 250px;
  background: radial-gradient(circle, rgba(220, 208, 238, 0.2) 0%, transparent 70%);
  bottom: -80px; right: -80px;
  filter: blur(50px);
}

.site-footer {
  padding: 60px clamp(20px, 4vw, 56px) 40px;
  border-top: 1px solid rgba(0, 0, 0, 0.06);
}
.footer-top { display: flex; justify-content: space-between; margin-bottom: 60px; gap: 60px; flex-wrap: wrap; }
.footer-brand h3 {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 700;
  font-size: 32px;
  letter-spacing: -0.02em;
  margin-bottom: 12px;
}
.footer-brand p { color: var(--ink-soft); font-size: 14px; max-width: 280px; }
.footer-cols { display: flex; gap: clamp(28px, 5vw, 60px); flex-wrap: wrap; }
.footer-col h4 {
  font-family: "JetBrains Mono", monospace;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.18em;
  margin-bottom: 18px;
  color: var(--ink-soft);
  font-weight: 600;
}
.footer-col a { display: block; font-size: 14px; margin-bottom: 10px; }
.footer-col a:hover { text-decoration: underline; }
.footer-bottom {
  padding-top: 32px;
  border-top: 1px solid rgba(0, 0, 0, 0.06);
  display: flex;
  justify-content: space-between;
  gap: 12px;
  flex-wrap: wrap;
  font-family: "JetBrains Mono", monospace;
  font-size: 10px;
  text-transform: uppercase;
  letter-spacing: 0.14em;
  color: var(--ink-soft);
}



/* ════════════════════════════════════════════════
   HERO v2 — headline + CTAs left, tilted chat in a cloud of
   floating clay cards right, lit from behind with a yellow glow.
   ════════════════════════════════════════════════ */
.hero {
  grid-template-columns: minmax(0, 1fr) minmax(0, 1.04fr);
  gap: 32px;
  padding: 72px clamp(24px, 4vw, 64px) 64px;
  min-height: 780px;
  background:
    radial-gradient(60% 70% at 78% 52%, rgba(253, 227, 81, 0.20) 0%, rgba(253, 227, 81, 0) 70%),
    linear-gradient(180deg, #faf9f5 0%, #f4f2ec 100%);
  border: 1px solid rgba(255, 255, 255, 0.9);
  box-shadow:
    0 30px 80px -30px rgba(92, 82, 24, 0.22),
    0 2px 0 rgba(255, 255, 255, 0.8) inset,
    inset 0 -16px 30px -10px rgba(92, 82, 30, 0.08);
  overflow: visible;
}
.hero-left { position: relative; z-index: 3; }

.hero-eyebrow {
  font-family: "JetBrains Mono", monospace;
  font-size: 13px; font-weight: 500;
  letter-spacing: 0.38em; text-transform: uppercase;
  color: #57564f;
  margin-bottom: 28px;
}
.hero-title {
  font-size: clamp(44px, 6.3vw, 104px);
  line-height: 0.9;
  letter-spacing: -0.05em;
  margin-bottom: 30px;
}
.hero-title .title-line { padding-bottom: 0.08em; }
.accent-line .title-inner { letter-spacing: -0.045em; padding-right: 0.06em; }
.accent-line .title-hl {
  background: linear-gradient(180deg, #ffd83a 0%, #f6c21b 55%, #ebb20c 100%);
  -webkit-background-clip: text; background-clip: text;
  -webkit-text-fill-color: transparent; color: #f6c21b;
}
.title-hl { position: relative; display: inline-block; }
.title-hl::before {
  content: ""; position: absolute; z-index: -1;
  left: -0.06em; right: -0.1em; bottom: 0.1em; height: 0.36em;
  background: linear-gradient(90deg, rgba(253, 227, 81, 0.62), rgba(253, 227, 81, 0.3));
  border-radius: 0.06em;
}

.hero-desc {
  font-size: clamp(17px, 1.35vw, 20px);
  line-height: 1.5;
  color: #5e5d56;
  max-width: 500px;
}

.hero-ctas { display: flex; align-items: center; gap: 10px; flex-wrap: wrap; margin-top: 30px; margin-left: -1.1rem; }
.btn.btn-lg {
  padding: 1.05rem 1.9rem 1.1rem 2.1rem;
  font-size: 1.2rem; font-weight: 700;
  text-transform: none;
  border-radius: 22px / 50%;
  box-shadow:
    0 0 0 1px rgba(170, 130, 10, 0.35),
    inset 0 2px 0 rgba(255, 255, 255, 0.6),
    inset 0 -3px 4px rgba(170, 120, 10, 0.3),
    0 4px 0 #e7b81a,
    0 18px 30px -10px rgba(200, 150, 20, 0.55);
}
.btn.btn-lg:hover { border-radius: 8px / 50%; }
.btn.btn-lg .btn-svg { height: 24px; stroke: #0a0a0a; stroke-width: 2.2; fill: none; }
.demo-btn {
  display: inline-flex; align-items: center; gap: 12px;
  padding: 1.05rem 1.7rem 1.1rem 1.3rem;
  font-size: 1.05rem; font-weight: 600;
  background: #fff;
  border-radius: 22px / 50%;
  border: 1px solid rgba(232, 228, 214, 0.9);
  box-shadow: inset 0 -2px 0 rgba(92, 82, 30, 0.06), 0 14px 30px -14px rgba(92, 82, 24, 0.28);
  transition: border-radius 0.3s ease-in-out, transform 0.2s;
}
.demo-btn:hover { border-radius: 8px / 50%; }
.demo-btn:active { transform: scale(0.98); }
.demo-play { width: 26px; height: 26px; border-radius: 50%; background: var(--ink); color: #fff; display: grid; place-items: center; }
.demo-play svg { width: 13px; height: 13px; margin-left: 2px; }

.hero-trust {
  list-style: none; display: flex; gap: 0; margin-top: 34px; flex-wrap: wrap;
}
.hero-trust li {
  display: flex; align-items: center; gap: 14px;
  font-size: 14.5px; line-height: 1.35; color: #66655d;
  padding: 2px 30px 2px 0; margin-right: 30px;
  border-right: 1px solid rgba(0, 0, 0, 0.09);
}
.hero-trust li:last-child { border-right: 0; margin-right: 0; padding-right: 0; }
.hero-trust svg { width: 24px; height: 24px; color: #4a4943; flex: none; }

/* glass chips on the slab's edge */
.glass--tab {
  top: -20px; left: clamp(28px, 3.6vw, 56px);
  height: auto; padding: 10px 16px 10px 13px; border-radius: 15px;
  display: flex; align-items: center; gap: 10px;
  font-family: "JetBrains Mono", monospace; font-weight: 500;
  font-size: 10.5px; letter-spacing: 0.1em; text-align: left; line-height: 1.5;
  color: #2c2b25;
  background: rgba(255, 255, 255, 0.62);
  box-shadow: 0 14px 30px -12px rgba(62, 54, 30, 0.3), inset 0 -10px 20px -4px rgba(171, 155, 208, 0.38), inset 0 2px 0 #fff;
}
.tab-dot {
  width: 12px; height: 12px; border-radius: 4px;
  background: linear-gradient(180deg, var(--yellow-light), var(--yellow-deep));
  box-shadow: 0 0 0 4px rgba(253, 227, 81, 0.25);
  transform: rotate(45deg) scale(0.85);
}
.glass--live {
  top: -26px; right: clamp(20px, 3vw, 44px);
  padding: 15px 22px 15px 18px; border-radius: 20px;
  display: flex; align-items: center; gap: 14px;
  font-family: "JetBrains Mono", monospace; font-size: 11.5px; line-height: 1.6; letter-spacing: 0.04em;
  color: #3b3a33;
  background: rgba(255, 255, 255, 0.66);
  box-shadow: 0 14px 30px -12px rgba(62, 54, 30, 0.28), inset 0 2px 0 #fff;
}
.glass--live b { font-weight: 600; letter-spacing: 0.14em; text-transform: uppercase; color: var(--ink); }
.live-dot {
  flex: none; width: 9px; height: 9px; border-radius: 50%; background: #2fb14c;
  box-shadow: 0 0 0 4px rgba(47, 177, 76, 0.18);
  animation: live 2.2s ease-in-out infinite;
}
@keyframes live { 50% { box-shadow: 0 0 0 7px rgba(47, 177, 76, 0.05); } }
.glass--disc {
  width: 150px; height: 150px; right: -40px; bottom: -44px;
  background: radial-gradient(circle at 35% 30%, rgba(255,255,255,0.9), rgba(236,226,248,0.55) 55%, rgba(220,208,238,0.45));
}

/* the visual */
.hero-right { align-self: stretch; }
.hero-visual { position: relative; width: 100%; height: 100%; min-height: 660px; display: grid; place-items: center; }
.hv-glow {
  position: absolute; z-index: 0; pointer-events: none;
  width: 72%; aspect-ratio: 1; right: -4%; top: 14%;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(253, 220, 60, 0.75) 0%, rgba(253, 227, 81, 0.35) 38%, rgba(253, 227, 81, 0) 70%);
  filter: blur(30px);
}
.hv-orbit { position: absolute; z-index: 0; inset: -6% -10%; width: 120%; height: 112%; pointer-events: none; }
.hv-orbit ellipse { stroke: rgba(240, 196, 30, 0.55); stroke-width: 1.4; }
.hv-dots {
  position: absolute; z-index: 0; pointer-events: none;
  width: 92px; height: 70px;
  background-image: radial-gradient(circle, rgba(10, 10, 10, 0.22) 1.6px, transparent 2px);
  background-size: 23px 23px;
}
.hv-dots--a { top: 6%; left: 22%; }
.hv-dots--b { bottom: 14%; right: 2%; }

.chat-stage { z-index: 2; max-width: 500px; margin-left: 12%; perspective: 1600px; }
.chat {
  transform: rotateY(-9deg) rotateX(4deg) rotateZ(-2.2deg);
  transform-origin: 40% 50%;
  border: 1px solid rgba(255, 236, 160, 0.9);
  background: linear-gradient(180deg, #fbf9f2 0%, #f4f0e4 100%);
  box-shadow:
    0 0 0 8px rgba(255, 246, 205, 0.55),
    inset 0 3px 0 rgba(255, 255, 255, 0.95),
    inset 0 -10px 22px -8px rgba(92, 82, 30, 0.12),
    0 30px 70px -20px rgba(140, 110, 20, 0.35),
    0 60px 100px -50px rgba(15, 15, 15, 0.4);
}

.float-card { position: absolute; z-index: 3; }
.fl-inner {
  padding: 18px 20px;
  border-radius: 22px;
  background: linear-gradient(180deg, rgba(255,255,255,0.92), rgba(250,248,242,0.88));
  -webkit-backdrop-filter: blur(10px); backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.95);
  box-shadow:
    inset 0 2px 0 #fff,
    inset 0 -6px 14px -6px rgba(92, 82, 30, 0.1),
    0 22px 40px -18px rgba(92, 82, 24, 0.35);
  animation: bob 6s ease-in-out infinite;
}
@keyframes bob { 50% { transform: translateY(-8px); } }
.fl-label { font-size: 14px; font-weight: 500; color: #4d4c45; }
.fl-big { display: block; font-size: 30px; font-weight: 700; letter-spacing: -0.03em; line-height: 1.15; font-variant-numeric: tabular-nums; }
.fl-row { display: flex; align-items: center; justify-content: space-between; gap: 18px; margin-top: 8px; }
.fl-up {
  font-family: "JetBrains Mono", monospace; font-size: 11.5px; font-weight: 600; color: #1f8a3a;
  background: rgba(47, 177, 76, 0.12); padding: 3px 7px; border-radius: 7px;
}
.fl-spark { width: 150px; height: 54px; margin-top: 12px; }
.fl-spark path { stroke: #f2c21b; stroke-width: 2.6; stroke-linecap: round; }
.fl-spark circle { fill: #f2c21b; stroke: #fff; stroke-width: 2; }
.fc-rate { left: 0; top: 14%; transform: rotate(3deg); }
.fc-rate .fl-inner { width: 188px; padding-bottom: 22px; }
.fc-fix { left: -2%; top: 52%; transform: rotate(2deg); }
.fc-fix .fl-inner { width: 214px; animation-delay: -2s; }
.fl-title { font-size: 16px; font-weight: 700; letter-spacing: -0.01em; }
.fl-list { list-style: none; display: grid; gap: 14px; margin-top: 16px; font-size: 13.5px; font-weight: 500; }
.fl-list li { display: flex; align-items: center; gap: 12px; }
.fl-list svg { width: 22px; height: 22px; flex: none; }
.fc-visitors { right: -8%; top: 53%; transform: rotate(-1.5deg); }
.fc-visitors .fl-inner { width: 182px; animation-delay: -4s; }
.fl-conf { display: flex; align-items: center; gap: 8px; margin-top: 10px; font-size: 13.5px; font-weight: 600; color: #1f8a3a; }
.fl-conf svg { width: 20px; height: 20px; }

@media (max-width: 1400px) {
  .chat-stage { max-width: 430px; margin-left: 18%; }
  .float-card { scale: 0.86; }
  .fc-rate { left: -6%; top: 10%; }
  .fc-fix { left: -8%; top: 54%; }
  .fc-visitors { right: -10%; top: 60%; }
  .hero-trust li { padding-right: 18px; margin-right: 18px; gap: 10px; font-size: 13.5px; }
}
@media (max-width: 1100px) {
  .hero { padding-top: 84px; }
  .hero-visual { min-height: 640px; }
  .chat-stage { margin-left: 0; }
  .fc-rate { left: 2%; }
  .fc-fix { left: 0; }
  .fc-visitors { right: -2%; }
  .glass--live { display: none; }
}
@media (max-width: 760px) {
  .hero { padding: 72px 20px 40px; }
  .hero-eyebrow { font-size: 11px; letter-spacing: 0.26em; }
  .hero-ctas { margin-left: 0; }
  .hero-ctas .btn-wrapper { margin: 0 -0.9rem; }
  .btn.btn-lg { font-size: 1.05rem; padding: 0.95rem 1.5rem 1rem 1.7rem; }
  .demo-btn { font-size: 0.98rem; padding: 0.95rem 1.4rem 1rem 1.1rem; }
  .hero-trust { gap: 14px; }
  .hero-trust li { border: 0; margin: 0; padding: 0; width: 100%; }
  .hero-visual { min-height: 0; padding-top: 8px; }
  .chat { transform: none; }
  .float-card, .hv-orbit, .hv-dots { display: none; }
  .glass--tab { padding: 9px 13px 9px 11px; font-size: 9.5px; top: -18px; }
  .glass--disc { width: 90px; height: 90px; right: -20px; bottom: -24px; }
}
@media (prefers-reduced-motion: reduce) {
  .fl-inner, .live-dot { animation: none !important; }
}

.px {
  --s1: calc(1em/14);
  --s2: calc(var(--s1)*2);
  --s3: calc(var(--s1)*3);
  --s4: calc(var(--s1)*4);
  --s5: calc(var(--s1)*5);
  --s6: calc(var(--s1)*6);
  --s7: calc(var(--s1)*7);
  --s8: calc(var(--s1)*8);
  --s10: calc(var(--s1)*10);
  --s12: calc(var(--s1)*12);
  --s14: calc(var(--s1)*14);

  --n1: calc(var(--s1)*-1);
  --n2: calc(var(--s1)*-2);
  --n3: calc(var(--s1)*-3);
  --n4: calc(var(--s1)*-4);
  --n5: calc(var(--s1)*-5);
  --n6: calc(var(--s1)*-6);
  --n7: calc(var(--s1)*-7);
  --n8: calc(var(--s1)*-8);
  --n10: calc(var(--s1)*-10);
  --n12: calc(var(--s1)*-12);
  --n14: calc(var(--s1)*-14);

  --space: move by var(--s6) 0;
  --a:
    move by var(--s4) 0,hline by var(--s2),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--s10),hline by var(--n2),
    vline by var(--n4),hline by var(--n6),vline by var(--s4),
    hline by var(--n2),vline by var(--n10),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--s3),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s3),hline by var(--s6),
    vline by var(--n3),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n2),
    vline by var(--n3),move by var(--s8) 0;
  --b:
    move by 0 var(--s14),hline by var(--s8),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n4),hline by var(--n1),vline by var(--n2),
    hline by var(--s1),vline by var(--n4),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n8),vline by var(--s14),move by var(--s7) var(--n12),
    vline by var(--s1),hline by var(--s1),vline by var(--s2),
    hline by var(--n1),vline by var(--s1),hline by var(--n5),
    vline by var(--n4),hline by var(--s5),move by 0 var(--s6),
    vline by var(--s1),hline by var(--s1),vline by var(--s2),
    hline by var(--n1),vline by var(--s1),hline by var(--n5),
    vline by var(--n4),hline by var(--s5),move by var(--n7) var(--s6),
    move by var(--s12) var(--n14);
  --c:
    move by var(--s2) var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s10),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s6),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n2),
    hline by var(--n2),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n4),vline by var(--n1),
    hline by var(--n1),vline by var(--n8),hline by var(--s1),
    vline by var(--n1),hline by var(--s4),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s2),
    vline by var(--n2),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n6),
    vline by var(--s1),move by var(--s10) var(--n1);
  --d:
    hline by var(--s8),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s10),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n8),vline by var(--n14),
    move by var(--s2) var(--s2),vline by var(--s10),hline by var(--s5),
    vline by var(--n1),hline by var(--s1),vline by var(--n8),
    hline by var(--n1),vline by var(--n1),hline by var(--n5),
    move by var(--n2) var(--n2),move by var(--s12) 0;
  --e:
    hline by var(--s10),vline by var(--s2),hline by var(--n8),
    vline by var(--s4),hline by var(--s7),vline by var(--s2),
    hline by var(--n7),vline by var(--s4),hline by var(--s8),
    vline by var(--s2),hline by var(--n10),vline by var(--n14),
    move by var(--s12) 0;
  --f:
    hline by var(--s10),vline by var(--s2),hline by var(--n8),
    vline by var(--s4),hline by var(--s7),vline by var(--s2),
    hline by var(--n7),vline by var(--s6),hline by var(--n2),
    vline by var(--n14),move by var(--s12) 0;
  --g:
    move by var(--s2) 0,hline by var(--s6),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s2),hline by var(--n2),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n4),
    vline by var(--s1),hline by var(--n1),vline by var(--s8),
    hline by var(--s1),vline by var(--s1),hline by var(--s4),
    vline by var(--n1),hline by var(--s1),vline by var(--n2),
    hline by var(--n2),vline by var(--n2),hline by var(--s4),
    vline by var(--s5),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n6),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n10),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    move by var(--s10) 0;
  --h:
    hline by var(--s2),vline by var(--s6),hline by var(--s6),
    vline by var(--n6),hline by var(--s2),vline by var(--s14),
    hline by var(--n2),vline by var(--n6),hline by var(--n6),
    vline by var(--s6),hline by var(--n2),vline by var(--n14),
    move by var(--s12) 0;
  --i:
    hline by var(--s10),vline by var(--s2),hline by var(--n4),
    vline by var(--s10),hline by var(--s4),vline by var(--s2),
    hline by var(--n10),vline by var(--n2),hline by var(--s4),
    vline by var(--n10),hline by var(--n4),vline by var(--n2),
    move by var(--s12) 0;
  --j:
    move by var(--s4) 0,hline by var(--s6),vline by var(--s2),
    hline by var(--n2),vline by var(--s10),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n4),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n2),
    hline by var(--s2),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s2),vline by var(--n1),
    hline by var(--s1),vline by calc(var(--s1)*-9),hline by var(--n2),
    vline by var(--n2),move by var(--s8) 0;
  --k:
    hline by var(--s2),vline by var(--s6),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s2),
    vline by var(--s2),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s2),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s2),
    hline by var(--n2),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n2),vline by var(--s5),
    hline by var(--n2),vline by var(--n14),move by var(--s12) 0;
  --l:
    hline by var(--s2),vline by var(--s12),hline by var(--s8),
    vline by var(--s2),hline by var(--n10),vline by var(--n14),
    move by var(--s12) 0;
  --m:
    hline by var(--s2),vline by var(--s2),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s2),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n2),
    hline by var(--s2),vline by var(--s14),hline by var(--n2),
    vline by calc(var(--s1)*-9),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s2),hline by var(--n2),
    vline by var(--n2),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by calc(var(--s1)*9),hline by var(--n2),
    vline by var(--n14),move by var(--s12) 0;
  --n:
    hline by var(--s2),vline by var(--s2),hline by var(--s1),
    vline by var(--s2),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--n8),hline by var(--s2),
    vline by var(--s14),hline by var(--n2),vline by var(--n2),
    hline by var(--n1),vline by var(--n2),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--s8),
    hline by var(--n2),vline by var(--n14),move by var(--s12) 0;
  --o:
    move by var(--s2) 0,hline by var(--s6),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s10),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n6),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n10),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    move by var(--s1) var(--s2),vline by var(--s1),hline by var(--n1),
    vline by var(--s8),hline by var(--s1),vline by var(--s1),
    hline by var(--s4),vline by var(--n1),hline by var(--s1),
    vline by var(--n8),hline by var(--n1),vline by var(--n1),
    hline by var(--n4),move by var(--n1) var(--n2),move by var(--s10) 0;
  --p:
    hline by var(--s8),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s4),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n6),vline by var(--s6),
    hline by var(--n2),vline by var(--n14),move by var(--s2) var(--s2),
    vline by var(--s4),hline by var(--s5),vline by var(--n1),
    hline by var(--s1),vline by var(--n2),hline by var(--n1),
    vline by var(--n1),hline by var(--n5),move by var(--n2) var(--n2),
    move by var(--s12) 0;
  --q:
    move by var(--s2) 0,hline by var(--s6),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by calc(var(--s1)*9),hline by var(--n1),vline by var(--s1),
    hline by var(--s1),vline by var(--s2),hline by var(--n2),
    vline by var(--n1),hline by var(--n1),vline by var(--s1),
    hline by var(--n5),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n10),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),move by var(--s1) var(--s2),vline by var(--s1),
    hline by var(--n1),vline by var(--s8),hline by var(--s1),
    vline by var(--s1),hline by var(--s3),vline by var(--n1),
    hline by var(--n1),vline by var(--n2),hline by var(--s2),
    vline by var(--s1),hline by var(--s1),vline by var(--n7),
    hline by var(--n1),vline by var(--n1),hline by var(--n4),
    move by var(--n1) var(--n2),move by var(--s10) 0;
  --r:
    hline by var(--s8),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s4),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--s1),vline by var(--s2),hline by var(--s1),
    vline by var(--s2),hline by var(--s1),vline by var(--s1),
    hline by var(--n3),vline by var(--n2),hline by var(--n1),
    vline by var(--n2),hline by var(--n1),vline by var(--n2),
    hline by var(--n3),vline by var(--s6),hline by var(--n2),
    vline by var(--n14),move by var(--s2) var(--s2),vline by var(--s4),
    hline by var(--s5),vline by var(--n1),hline by var(--s1),
    vline by var(--n2),hline by var(--n1),vline by var(--n1),
    hline by var(--n5),move by var(--n2) var(--n2),move by var(--s12) 0;
  --s:
    move by var(--s2) 0,hline by var(--s6),vline by var(--s1),
    hline by var(--s1),vline by var(--s1),hline by var(--s1),
    vline by var(--s2),hline by var(--n2),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n4),
    vline by var(--s1),hline by var(--n1),vline by var(--s2),
    hline by var(--s1),vline by var(--s1),hline by var(--s5),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--s4),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n6),vline by var(--n1),hline by var(--n1),
    vline by var(--n1),hline by var(--n1),vline by var(--n2),
    hline by var(--s2),vline by var(--s1),hline by var(--s1),
    vline by var(--s1),hline by var(--s4),vline by var(--n1),
    hline by var(--s1),vline by var(--n2),hline by var(--n1),
    vline by var(--n1),hline by var(--n5),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n1),
    vline by var(--n4),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),move by var(--s10) 0;
  --t:
    hline by var(--s10),vline by var(--s2),hline by var(--n4),
    vline by var(--s12),hline by var(--n2),vline by var(--n12),
    hline by var(--n4),vline by var(--n2),move by var(--s12) 0;
  --u:
    hline by var(--s2),vline by calc(var(--s1)*11),hline by var(--s1),
    vline by var(--s1),hline by var(--s4),vline by var(--n1),
    hline by var(--s1),vline by calc(var(--s1)*-11),hline by var(--s2),
    vline by var(--s12),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n6),
    vline by var(--n1),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n12),move by var(--s12) 0;
  --v:
    hline by var(--s2),vline by var(--s6),hline by var(--s1),
    vline by var(--s2),hline by var(--s1),vline by var(--s2),
    hline by var(--s2),vline by var(--n2),hline by var(--s1),
    vline by var(--n2),hline by var(--s1),vline by var(--n6),
    hline by var(--s2),vline by var(--s6),hline by var(--n1),
    vline by var(--s2),hline by var(--n1),vline by var(--s2),
    hline by var(--n1),vline by var(--s2),hline by var(--n1),
    vline by var(--s2),hline by var(--n2),vline by var(--n2),
    hline by var(--n1),vline by var(--n2),hline by var(--n1),
    vline by var(--n2),hline by var(--n1),vline by var(--n2),
    hline by var(--n1),vline by var(--n6),move by var(--s12) 0;
  --w:
    hline by var(--s2),vline by calc(var(--s1)*11),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n6),
    hline by var(--s2),vline by var(--s6),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by calc(var(--s1)*-11),
    hline by var(--s2),vline by var(--s12),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n2),vline by var(--n2),hline by var(--n2),
    vline by var(--s2),hline by var(--n2),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n1),
    vline by var(--n12),move by var(--s12) 0;
  --x:
    hline by var(--s2),vline by var(--s3),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s2),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n3),
    hline by var(--s2),vline by var(--s4),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s2),hline by var(--s1),
    vline by var(--s1),hline by var(--s1),vline by var(--s1),
    hline by var(--s1),vline by var(--s4),hline by var(--n2),
    vline by var(--n3),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n2),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s3),hline by var(--n2),
    vline by var(--n4),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n2),hline by var(--n1),vline by var(--n1),
    hline by var(--n1),vline by var(--n1),hline by var(--n1),
    vline by var(--n4),move by var(--s12) 0;
  --y:
    hline by var(--s2),vline by var(--s2),hline by var(--s1),
    vline by var(--s2),hline by var(--s1),vline by var(--s2),
    hline by var(--s2),vline by var(--n2),hline by var(--s1),
    vline by var(--n2),hline by var(--s1),vline by var(--n2),
    hline by var(--s2),vline by var(--s2),hline by var(--n1),
    vline by var(--s2),hline by var(--n1),vline by var(--s2),
    hline by var(--n1),vline by var(--s2),hline by var(--n1),
    vline by var(--s6),hline by var(--n2),vline by var(--n6),
    hline by var(--n1),vline by var(--n2),hline by var(--n1),
    vline by var(--n2),hline by var(--n1),vline by var(--n2),
    hline by var(--n1),vline by var(--n2),move by var(--s12) 0;
  --z:
    hline by var(--s10),vline by var(--s4),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--n1),vline by var(--s1),hline by var(--n1),
    vline by var(--s1),hline by var(--n1),vline by var(--s1),
    hline by var(--s8),vline by var(--s2),hline by var(--n10),
    vline by var(--n4),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--s1),
    vline by var(--n1),hline by var(--s1),vline by var(--n1),
    hline by var(--s1),vline by var(--n1),hline by var(--n8),
    vline by var(--n2),move by var(--s12) 0;
}


/* ════════════════════════════════════════════════
   PIXEL TYPE
   A 10×14 block font drawn entirely with clip-path: shape(). Paired
   with Funnel Display: the pixel face takes accents and labels, the
   humanist sans keeps headlines and reading text. Lowercase a–z and
   space only, so it is reserved for words, never numbers.
   ════════════════════════════════════════════════ */
.px-on .px {
  display: inline-block;
  white-space: nowrap;
  /* Chrome swallows every rule after a shape() that holds a var() when it is
     written straight into clip-path; routed through a custom property it
     parses cleanly and still resolves on this element. */
  --px-clip: shape(from 0 0, var(--letters));
  clip-path: var(--px-clip);
  height: calc(var(--s1) * 14);
  width: calc(var(--count) * var(--s12));
  color: transparent;
  line-height: calc(var(--s1) * 14);
  overflow: hidden;
  vertical-align: -0.12em;
  background: var(--px-fill, currentColor);
  font-family: monospace;
}
/* each label's pixel size is a whole px at 14px, so it stays crisp */
.px-on .hero-eyebrow, .px-on .section-eyebrow { letter-spacing: 0; text-transform: none; }
.px-on .hero-eyebrow .px { font-size: 14px; --px-fill: #57564f; }
.px-on .section-eyebrow .px { font-size: 14px; --px-fill: var(--ink-soft); vertical-align: middle; }

/* hero accent: yellow pixels with an ink offset, like a printed sticker */
.px-on .accent-line .title-hl {
  background: none; -webkit-text-fill-color: currentColor; color: inherit;
}
.px-on .px-shadow { display: inline-block; filter: drop-shadow(0.035em 0.045em 0 #0a0a0a); }
.px-on .title-hl .px {
  font-size: 0.82em;
  vertical-align: 0.02em;
  --px-fill: linear-gradient(180deg, #ffe55c 0%, #fbd02a 50%, #f0b90e 100%);
}
.px-on .accent-line .title-hl::before { bottom: 0.04em; height: 0.34em; right: -0.08em; }

/* final CTA accent */
.px-on .final-cta-h2 .px { font-size: 0.8em; vertical-align: 0; --px-fill: var(--yellow); }
.px-on .final-cta-h2 .px-shadow { filter: drop-shadow(0.04em 0.05em 0 rgba(0, 0, 0, 0.6)); }


/* ════════════════════════════════════════════════
   METRICS — four clay tiles, each with its own instrument
   ════════════════════════════════════════════════ */
.stats-bar { padding: 72px clamp(20px, 4vw, 56px) 40px; }
.metrics-head { display: flex; justify-content: space-between; align-items: center; gap: 20px; margin-bottom: 28px; flex-wrap: wrap; }
.metrics-head .section-eyebrow { margin-bottom: 0; }
.metrics-live {
  display: inline-flex; align-items: center; gap: 10px;
  font-family: "JetBrains Mono", monospace; font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase;
  color: var(--ink-soft);
  padding: 8px 14px 7px; border-radius: 12px / 50%;
  background: #fff; border: 1px solid var(--cream-line);
}
.metrics-live .live-dot { width: 8px; height: 8px; }
.metric-grid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 18px; }
.metric {
  position: relative; overflow: hidden;
  display: flex; flex-direction: column; gap: 14px;
  min-height: 300px; padding: 24px 24px 22px;
  border-radius: 30px;
  background: linear-gradient(180deg, #fff 0%, var(--cream) 100%);
  border: 1px solid var(--cream-line);
  box-shadow: inset 0 3px 0 rgba(255,255,255,0.9), inset 0 -8px 18px -8px rgba(92,82,30,0.12), 0 18px 40px -22px rgba(92,82,24,0.3);
  transition: transform 0.4s var(--spring), box-shadow 0.4s;
}
.metric:hover { transform: translateY(-6px); box-shadow: inset 0 3px 0 rgba(255,255,255,0.9), inset 0 -8px 18px -8px rgba(92,82,30,0.12), 0 28px 50px -22px rgba(92,82,24,0.4); }
.metric-label .px { font-size: 14px; --px-fill: var(--ink-soft); }
.metric .stat-num { font-size: clamp(48px, 4.6vw, 72px); font-weight: 800; letter-spacing: -0.05em; margin: 0; }
.metric .stat-num .accent { color: var(--yellow-deep); }
.m-foot { margin-top: auto; font-size: 13px; color: var(--ink-soft); padding-top: 12px; border-top: 1px dashed var(--cream-deep); }
.m-dark {
  background: linear-gradient(170deg, #1d1d1c 0%, #0a0a0a 100%); border-color: #000; color: #fff;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.1), 0 2px 0 #000, 0 24px 44px -22px rgba(0,0,0,0.5);
}
.m-dark .metric-label .px { --px-fill: #8f8d85; }
.m-dark .stat-num .accent { color: var(--yellow); }
.m-dark .m-foot { color: #a9a9a2; border-color: rgba(255,255,255,0.12); }
.m-yellow {
  background: linear-gradient(170deg, var(--yellow-light) 0%, var(--yellow) 65%, var(--yellow-deep) 100%);
  border-color: var(--yellow-line);
  box-shadow: inset 0 3px 0 rgba(255,255,255,0.5), inset 0 -6px 14px -6px rgba(150,110,10,0.35), 0 20px 40px -20px rgba(200,160,30,0.5);
}
.m-yellow .metric-label .px { --px-fill: rgba(0,0,0,0.6); }
.m-yellow .stat-num .accent { color: var(--ink); }
.m-yellow .m-foot { color: rgba(0,0,0,0.65); border-color: rgba(0,0,0,0.18); }

.m-bars { display: grid; grid-template-columns: repeat(16, 1fr); gap: 4px; align-items: end; height: 64px; }
.m-bars i { height: var(--h); border-radius: 3px 3px 1px 1px; background: rgba(255,255,255,0.16); transform-origin: bottom; }
.m-bars i:nth-last-child(-n+4) { background: rgba(253,227,81,0.55); }
.m-bars i:last-child { background: var(--yellow); box-shadow: 0 0 14px rgba(253,227,81,0.6); }

.m-gauge { width: 100%; max-width: 200px; height: auto; align-self: center; overflow: visible; }
.g-track { fill: none; stroke: var(--cream-2); stroke-width: 14; stroke-linecap: round; }
.g-fill { fill: none; stroke: var(--yellow-deep); stroke-width: 14; stroke-linecap: round; stroke-dasharray: 100; stroke-dashoffset: 64; transition: stroke-dashoffset 1.6s cubic-bezier(.2,.8,.2,1); }
.g-ticks path { stroke: var(--cream-deep); stroke-width: 2; stroke-linecap: round; }
.g-needle { stroke: var(--ink); stroke-width: 3.5; stroke-linecap: round; transform-origin: 100px 100px; transform: rotate(-25deg); transition: transform 1.6s cubic-bezier(.3,1.5,.5,1); }
.g-hub { fill: var(--ink); stroke: #fff; stroke-width: 3; }
.metric.is-seen .g-needle { transform: rotate(-25deg); }
.metric.pre .g-fill { stroke-dashoffset: 100; }
.metric.pre .g-needle { transform: rotate(-90deg); }

.m-matrix { display: grid; grid-template-columns: repeat(12, 1fr); gap: 5px; }
.m-matrix i { aspect-ratio: 1; border-radius: 3px; background: rgba(0,0,0,0.1); }
.m-matrix i.on { background: var(--ink); animation: blink 2.4s steps(1) infinite; }
.m-matrix i.on:nth-child(3n) { animation-delay: -0.8s; }
.m-matrix i.on:nth-child(5n) { animation-delay: -1.6s; }
.m-matrix i.on:nth-child(7n) { animation-duration: 3.1s; }
@keyframes blink { 50% { background: rgba(0,0,0,0.1); } }

.m-race { display: grid; gap: 6px; font-size: 12.5px; }
.race-row { display: flex; justify-content: space-between; color: var(--ink-soft); }
.race-row b { font-family: "JetBrains Mono", monospace; font-size: 11px; color: var(--ink); }
.race-bar { height: 12px; border-radius: 99px; background: var(--cream-2); border: 1px solid var(--cream-line); overflow: hidden; margin-bottom: 6px; }
.race-bar i { display: block; height: 100%; border-radius: 99px; transition: width 1.6s cubic-bezier(.2,.8,.2,1); }
.race-bar.slow i { width: 100%; background: repeating-linear-gradient(135deg, #2a2a2a 0 6px, #0a0a0a 6px 12px); }
.race-bar.fast i { width: 4%; min-width: 14px; background: var(--yellow-deep); box-shadow: 0 0 10px rgba(247,209,48,0.8); }
.metric.pre .race-bar i { width: 0; }

/* ════════════════════════════════════════════════
   FEATURE CARDS v2 — each one carries a working slice of the product
   ════════════════════════════════════════════════ */
.feature-card { min-height: 0; padding: 26px 26px 30px; gap: 0; }
.fc-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px; }
.fc-step {
  font-size: 46px; font-weight: 800; letter-spacing: -0.05em; line-height: 1;
  color: transparent; -webkit-text-stroke: 1.5px rgba(10,10,10,0.55);
}
.fc-chip {
  display: inline-flex; align-items: center;
  padding: 8px 12px; border-radius: 11px / 50%;
  background: rgba(255,255,255,0.6); border: 1px solid rgba(255,255,255,0.8);
  box-shadow: inset 0 -2px 0 rgba(0,0,0,0.05);
}
.fc-chip .px { font-size: 14px; --px-fill: var(--ink); }
.fc-visual {
  position: relative;
  height: 190px; margin-bottom: 26px; padding: 16px;
  border-radius: 22px;
  background: rgba(255,255,255,0.55);
  border: 1px solid rgba(255,255,255,0.9);
  box-shadow: inset 0 2px 0 #fff, inset 0 -10px 20px -10px rgba(0,0,0,0.08), 0 14px 30px -18px rgba(0,0,0,0.25);
  -webkit-backdrop-filter: blur(6px); backdrop-filter: blur(6px);
  overflow: hidden;
}
.feature-card h3 { font-size: 26px; margin-bottom: 12px; }

/* 01 ask */
.ask-input {
  display: flex; align-items: center; gap: 2px;
  padding: 12px 14px; border-radius: 14px; background: #fff;
  border: 1px solid rgba(0,0,0,0.06); box-shadow: 0 6px 14px -8px rgba(0,0,0,0.25);
  font-size: 13.5px; font-weight: 500; white-space: nowrap; overflow: hidden;
}
.ask-q { overflow: hidden; display: inline-block; max-width: 0; animation: type 4.5s steps(32) infinite; white-space: nowrap; }
@keyframes type { 0% { max-width: 0; } 45%, 100% { max-width: 100%; } }
.caret { width: 2px; height: 17px; background: var(--ink); animation: caret 0.9s steps(1) infinite; flex: none; }
@keyframes caret { 50% { opacity: 0; } }
.ask-answer {
  margin-top: 12px; display: flex; gap: 10px; align-items: center;
  padding: 10px 12px; border-radius: 14px 14px 14px 5px;
  background: rgba(255,255,255,0.85); font-size: 13px; line-height: 1.35;
  width: fit-content; max-width: 100%;
}
.ask-answer .chat-avatar { width: 26px; height: 26px; border-radius: 9px; }
.ask-answer .chat-avatar svg { width: 13px; height: 13px; }
.ask-answer em { font-style: normal; margin-left: 8px; font-family: "JetBrains Mono", monospace; font-size: 11px; font-weight: 600; color: #b3261e; }
.ask-meta { position: absolute; left: 16px; bottom: 14px; display: flex; gap: 6px; font-family: "JetBrains Mono", monospace; font-size: 10.5px; color: rgba(0,0,0,0.5); }

/* 02 leak */
.leak-head { display: flex; justify-content: space-between; align-items: center; font-size: 12.5px; font-weight: 600; }
.leak-head b {
  display: inline-flex; align-items: center; gap: 6px;
  font-family: "JetBrains Mono", monospace; font-size: 10.5px; font-weight: 600; letter-spacing: 0.06em; text-transform: uppercase;
  background: #fff; color: #b3261e; padding: 4px 8px; border-radius: 8px;
}
.leak-head b i { width: 7px; height: 7px; border-radius: 50%; background: #e0533d; animation: live 1.6s ease-in-out infinite; box-shadow: 0 0 0 3px rgba(224,83,61,0.2); }
.v-leak svg { position: absolute; left: 0; right: 0; bottom: 34px; width: 100%; height: 110px; }
.lk-area { fill: rgba(10,10,10,0.07); }
.lk-line { fill: none; stroke: var(--ink); stroke-width: 2.4; vector-effect: non-scaling-stroke; }
.lk-deploy { stroke: rgba(0,0,0,0.4); stroke-width: 1.2; stroke-dasharray: 3 3; vector-effect: non-scaling-stroke; }
.lk-dot { fill: #e0533d; stroke: #fff; stroke-width: 2.5; vector-effect: non-scaling-stroke; }
.leak-tag {
  position: absolute; left: 16px; bottom: 12px;
  font-family: "JetBrains Mono", monospace; font-size: 10.5px; color: rgba(0,0,0,0.6);
  background: rgba(255,255,255,0.75); padding: 4px 8px; border-radius: 7px;
}

/* 03 a/b */
.v-ab { display: flex; flex-direction: column; justify-content: center; gap: 14px; }
.ab-row { display: grid; grid-template-columns: 28px 1fr 42px; align-items: center; gap: 10px; position: relative; }
.ab-key { width: 28px; height: 28px; border-radius: 9px; display: grid; place-items: center; background: #fff; font-weight: 700; font-size: 13px; }
.ab-bar { height: 26px; border-radius: 9px; background: rgba(255,255,255,0.6); overflow: hidden; }
.ab-bar i { display: block; height: 100%; width: var(--w); border-radius: 8px; background: rgba(10,10,10,0.25); }
.ab-row.win .ab-bar i { background: linear-gradient(180deg, #2a2a2a, #0a0a0a); }
.ab-row.win .ab-key { background: var(--ink); color: #fff; }
.ab-row b { font-family: "JetBrains Mono", monospace; font-size: 12px; text-align: right; }
.ab-badge {
  position: absolute; right: 52px; top: -11px;
  font-family: "JetBrains Mono", monospace; font-size: 9.5px; font-weight: 600; letter-spacing: 0.1em; text-transform: uppercase;
  padding: 3px 7px; border-radius: 7px; color: var(--ink);
  background: linear-gradient(180deg, var(--yellow-light), var(--yellow-deep)); border: 1px solid var(--yellow-line);
}
.ab-foot { display: flex; justify-content: space-between; font-family: "JetBrains Mono", monospace; font-size: 10.5px; color: rgba(0,0,0,0.55); padding-top: 4px; }
.ab-conf { display: inline-flex; align-items: center; gap: 6px; color: #1f6b33; font-weight: 600; }
.ab-conf i { width: 7px; height: 7px; border-radius: 50%; background: #2fb14c; }

/* ════════════════════════════════════════════════
   FINALE — the CTA and the footer are one dark slab: a lit grid,
   a glow from above, the measuring rule between them, and the
   name set in pixels across the bottom edge.
   ════════════════════════════════════════════════ */
.final-cta.finale {
  position: relative; overflow: hidden;
  margin-top: 40px;
  padding: 140px clamp(20px, 4vw, 56px) 0;
  background: linear-gradient(180deg, #121211 0%, #0a0a0a 55%, #080808 100%);
  border-radius: 56px 56px 0 0;
  color: #fff;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.08);
}
.finale-grid {
  position: absolute; inset: 0; pointer-events: none;
  background-image:
    linear-gradient(rgba(255,255,255,0.045) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.045) 1px, transparent 1px);
  background-size: 64px 64px;
  background-position: center top;
  -webkit-mask-image: radial-gradient(70% 55% at 50% 22%, #000 0%, transparent 75%);
  mask-image: radial-gradient(70% 55% at 50% 22%, #000 0%, transparent 75%);
}
.finale-glow {
  position: absolute; pointer-events: none;
  left: 50%; top: -260px; width: 900px; height: 600px; transform: translateX(-50%);
  background: radial-gradient(closest-side, rgba(253,227,81,0.32), rgba(253,227,81,0.08) 55%, transparent);
  filter: blur(10px);
}
.final-cta.finale .final-cta-card {
  background: none; box-shadow: none; border-radius: 0; overflow: visible;
  padding: 0; max-width: 860px; position: relative; z-index: 2;
}
.finale-kicker {
  display: inline-flex; align-items: center; gap: 10px;
  font-family: "JetBrains Mono", monospace; font-size: 11.5px; letter-spacing: 0.08em; text-transform: uppercase;
  color: #d8d6cc; padding: 9px 15px 8px; border-radius: 13px / 50%;
  background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.1);
  margin-bottom: 30px;
}
.finale-kicker .live-dot { width: 8px; height: 8px; }
.final-cta.finale .final-cta-h2 { font-size: clamp(48px, 7vw, 108px); line-height: 0.98; margin-bottom: 28px; }
.final-cta.finale .final-cta-h2 .px { font-size: 0.78em; }
.final-cta.finale p { color: rgba(255,255,255,0.62); font-size: 17px; max-width: 620px; margin-bottom: 36px; }

.cta-form {
  display: flex; align-items: center; gap: 4px;
  max-width: 560px; margin: 0 auto;
  padding: 6px 4px 6px 22px;
  border-radius: 22px / 50%;
  background: rgba(255,255,255,0.06);
  border: 1px solid rgba(255,255,255,0.14);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.06), 0 20px 50px -20px rgba(0,0,0,0.6);
  transition: border-color 0.2s, background 0.2s;
}
.cta-form:focus-within { border-color: rgba(253,227,81,0.6); background: rgba(255,255,255,0.08); }
.cta-form input {
  flex: 1; min-width: 0; border: 0; outline: 0; background: transparent;
  font: inherit; font-size: 16px; color: #fff; padding: 12px 0;
}
.cta-form input::placeholder { color: rgba(255,255,255,0.4); }
.cta-form .btn-wrapper { padding: 0.55rem 0.75rem; }
.cta-form .btn { font-size: 15px; padding: 0.8rem 1.3rem; text-transform: none; }
.final-cta.finale .cta-note {
  margin: 18px auto 0; font-family: "JetBrains Mono", monospace; font-size: 11px;
  letter-spacing: 0.1em; text-transform: uppercase; color: rgba(255,255,255,0.45);
}
.cta-note.ok { color: var(--yellow) !important; }

.finale-rule {
  position: relative; z-index: 2;
  display: flex; align-items: center;
  margin: 120px 0 0;
}
.finale-rule span {
  flex: 1; height: 1px;
  background-image: repeating-linear-gradient(90deg, rgba(255,255,255,0.28) 0 2px, transparent 2px 6px);
}
.finale-rule i { width: 7px; height: 7px; border-radius: 50%; background: rgba(255,255,255,0.6); flex: none; }

.final-cta.finale .site-footer {
  position: relative; z-index: 2;
  padding: 64px 0 0; border: 0; text-align: left;
  color: #d8d6cc;
}
.final-cta.finale .footer-top { margin-bottom: 64px; }
.f-logo {
  display: inline-flex; align-items: center; gap: 10px;
  font-size: 22px; font-weight: 700; letter-spacing: -0.02em; color: #fff; margin-bottom: 16px;
}
.f-cube {
  width: 34px; height: 34px; border-radius: 11px; display: grid; place-items: center; color: var(--ink);
  background: linear-gradient(180deg, var(--yellow-light), var(--yellow) 55%, var(--yellow-deep));
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.6), 0 6px 16px -4px rgba(253,227,81,0.4);
}
.f-cube svg { width: 17px; height: 17px; }
.final-cta.finale .footer-brand p { color: rgba(255,255,255,0.55); font-size: 14.5px; max-width: 290px; margin: 0 0 20px; }
.f-status {
  display: inline-flex; align-items: center; gap: 9px;
  font-family: "JetBrains Mono", monospace; font-size: 11px; letter-spacing: 0.06em; color: rgba(255,255,255,0.7);
  padding: 7px 12px 6px; border-radius: 10px / 50%; border: 1px solid rgba(255,255,255,0.12);
}
.f-status .live-dot { width: 7px; height: 7px; }
.final-cta.finale .footer-cols { gap: clamp(32px, 6vw, 88px); }
.final-cta.finale .footer-col h4 { margin-bottom: 20px; }
.final-cta.finale .footer-col h4 .px { font-size: 14px; --px-fill: var(--yellow); }
.final-cta.finale .footer-col a {
  color: rgba(255,255,255,0.7); font-size: 14.5px; margin-bottom: 12px;
  width: fit-content; position: relative; transition: color 0.2s;
}
.final-cta.finale .footer-col a::after {
  content: ""; position: absolute; left: 0; right: 0; bottom: -3px; height: 1px;
  background: var(--yellow); transform: scaleX(0); transform-origin: left; transition: transform 0.3s ease;
}
.final-cta.finale .footer-col a:hover { color: #fff; text-decoration: none; }
.final-cta.finale .footer-col a:hover::after { transform: scaleX(1); }
.final-cta.finale .footer-bottom { border-top: 1px solid rgba(255,255,255,0.08); color: rgba(255,255,255,0.45); align-items: center; }
.f-badges { display: flex; gap: 8px; flex-wrap: wrap; }
.f-badges span { padding: 5px 9px 4px; border-radius: 8px; border: 1px solid rgba(255,255,255,0.1); }

.footer-mark {
  margin-top: 40px; line-height: 0;
  display: flex; justify-content: center;
  margin-bottom: -3.2vw;
}
.footer-mark .px {
  font-size: 16.8vw;
  --px-fill: radial-gradient(circle at var(--mx, 50%) var(--my, 30%), #fff8cf 0, var(--yellow) 14%, rgba(253,227,81,0.55) 34%, rgba(253,227,81,0.12) 70%);
}
html:not(.px-on) .footer-mark { font-size: 16vw; line-height: 1; color: rgba(253,227,81,0.3); font-weight: 800; }

@media (max-width: 1100px) {
  .metric-grid { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .final-cta.finale { padding-top: 100px; }
  .finale-rule { margin-top: 80px; }
}
@media (max-width: 700px) {
  .metric-grid { grid-template-columns: 1fr; }
  .metric { min-height: 260px; }
  .final-cta.finale { border-radius: 36px 36px 0 0; }
  .final-cta.finale .final-cta-h2 .px { font-size: 0.64em; }
  .cta-form { flex-direction: column; align-items: stretch; padding: 10px; border-radius: 24px; }
  .cta-form input { padding: 10px 12px; text-align: center; }
  .cta-form .btn-wrapper { padding: 0.4rem; }
  .cta-form .btn { width: 100%; }
  .final-cta.finale .footer-cols { display: grid; grid-template-columns: 1fr 1fr; }
}
@media (prefers-reduced-motion: reduce) {
  .ask-q { animation: none !important; max-width: 100%; }
  .m-matrix i.on, .caret { animation: none !important; }
}


/* ════════════════════════════════════════════════
   MOBILE MENU — the bar's yellow button becomes a two-line toggle;
   the menu opens as a dark sheet that grows out of it, the same
   material as the closing section.
   ════════════════════════════════════════════════ */
.menu-btn {
  display: none;
  place-items: center;
  width: 46px; height: 42px; margin-left: 6px;
  border: 1px solid var(--yellow-line);
  border-radius: 11px / 50%;
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.6), inset 0 -1px 2px rgba(180,140,30,0.3), 0 2px 4px rgba(200,160,30,0.3);
  cursor: pointer; color: var(--ink);
  transition: border-radius 0.3s ease-in-out, transform 0.2s;
}
.menu-btn:hover { border-radius: 4px / 50%; }
.menu-btn:active { transform: scale(0.95); }
.mb-lines { position: relative; width: 18px; height: 10px; display: block; }
.mb-lines i {
  position: absolute; left: 0; right: 0; height: 2px; border-radius: 2px; background: currentColor;
  transition: transform 0.45s var(--spring), top 0.3s ease, width 0.3s ease;
}
.mb-lines i:first-child { top: 0; }
.mb-lines i:last-child { top: 8px; width: 12px; left: auto; }
.menu-open .mb-lines i:first-child { top: 4px; transform: rotate(45deg); }
.menu-open .mb-lines i:last-child { top: 4px; width: 18px; transform: rotate(-45deg); }

.mobile-menu {
  position: fixed; inset: 0; z-index: 50; overflow-x: hidden;
  background: linear-gradient(180deg, #121211 0%, #0a0a0a 60%, #080808 100%);
  color: #fff;
  overflow-y: auto; overscroll-behavior: contain;
  clip-path: circle(0px at var(--ox, 90%) var(--oy, 40px));
  transition: clip-path 0.7s cubic-bezier(0.7, 0, 0.2, 1);
  visibility: hidden;
}
.mobile-menu[hidden] { display: none; }
.menu-open .mobile-menu { clip-path: circle(150% at var(--ox, 90%) var(--oy, 40px)); visibility: visible; }
.mobile-menu.closing { visibility: visible; }
.mm-glow {
  position: absolute; pointer-events: none; left: 50%; top: -220px; width: 700px; height: 520px; transform: translateX(-50%);
  background: radial-gradient(closest-side, rgba(253,227,81,0.26), rgba(253,227,81,0.06) 60%, transparent);
}
.mm-inner {
  position: relative; z-index: 2;
  max-width: 640px; margin: 0 auto;
  min-height: 100%;
  display: flex; flex-direction: column;
  padding: 128px clamp(20px, 5vw, 40px) calc(14vw + 16px);
}
.mm-top, .mm-list li, .mm-cta, .mm-foot {
  opacity: 0; transform: translateY(24px);
  transition: opacity 0.5s ease, transform 0.6s var(--spring);
}
.menu-open .mm-top, .menu-open .mm-list li, .menu-open .mm-cta, .menu-open .mm-foot {
  opacity: 1; transform: none;
  transition-delay: calc(0.22s + var(--i) * 0.06s);
}
.mm-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 18px; }
.mm-top .px { font-size: 14px; --px-fill: var(--yellow); }
.mm-status {
  display: inline-flex; align-items: center; gap: 9px;
  font-family: "JetBrains Mono", monospace; font-size: 10.5px; letter-spacing: 0.06em; color: rgba(255,255,255,0.65);
  padding: 6px 11px 5px; border-radius: 10px / 50%; border: 1px solid rgba(255,255,255,0.12);
}
.mm-status .live-dot { width: 7px; height: 7px; }
.mm-list { list-style: none; border-top: 1px solid rgba(255,255,255,0.08); }
.mm-list li { border-bottom: 1px solid rgba(255,255,255,0.08); }
.mm-list a {
  display: grid; grid-template-columns: 40px 1fr 44px; align-items: center; gap: 12px;
  padding: 18px 2px;
  transition: padding 0.35s var(--spring);
}
.mm-num { font-family: "JetBrains Mono", monospace; font-size: 11px; color: rgba(255,255,255,0.4); letter-spacing: 0.06em; }
.mm-text { display: flex; flex-direction: column; gap: 2px; min-width: 0; }
.mm-label { font-size: clamp(34px, 8vw, 52px); font-weight: 700; letter-spacing: -0.04em; line-height: 1; transition: color 0.25s; }
.mm-sub { font-size: 13px; color: rgba(255,255,255,0.45); }
.mm-arrow {
  width: 44px; height: 44px; border-radius: 14px; display: grid; place-items: center;
  border: 1px solid rgba(255,255,255,0.14); color: rgba(255,255,255,0.7);
  transition: background 0.25s, color 0.25s, border-color 0.25s, transform 0.35s var(--spring);
}
.mm-arrow svg { width: 18px; height: 18px; }
.mm-list a:hover, .mm-list a:focus-visible { padding-left: 10px; }
.mm-list a:hover .mm-label, .mm-list a:focus-visible .mm-label { color: var(--yellow); }
.mm-list a:hover .mm-arrow, .mm-list a:focus-visible .mm-arrow {
  background: var(--yellow); color: var(--ink); border-color: var(--yellow-line); transform: rotate(45deg);
}
.mm-cta { display: grid; gap: 10px; margin-top: 32px; }
.mm-primary, .mm-secondary {
  display: flex; align-items: center; justify-content: center; gap: 10px;
  padding: 17px 20px; border-radius: 20px / 50%;
  font-size: 17px; font-weight: 700;
  transition: border-radius 0.3s ease-in-out, transform 0.2s;
}
.mm-primary {
  color: var(--ink);
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  border: 1px solid var(--yellow-line);
  box-shadow: inset 0 2px 0 rgba(255,255,255,0.55), 0 4px 0 #b88f10, 0 18px 34px -12px rgba(253,227,81,0.45);
}
.mm-primary svg { width: 20px; height: 20px; }
.mm-secondary { color: #fff; font-weight: 600; background: rgba(255,255,255,0.06); border: 1px solid rgba(255,255,255,0.14); }
.mm-secondary .demo-play { background: #fff; color: var(--ink); }
.mm-primary:hover, .mm-secondary:hover { border-radius: 8px / 50%; }
.mm-primary:active, .mm-secondary:active { transform: scale(0.98); }
.mm-foot {
  margin-top: auto; padding-top: 36px;
  display: flex; justify-content: space-between; gap: 12px;
  font-family: "JetBrains Mono", monospace; font-size: 11px; letter-spacing: 0.08em; text-transform: uppercase;
  color: rgba(255,255,255,0.45);
}
.mm-foot a { color: #fff; text-decoration: underline; text-decoration-color: var(--yellow); text-underline-offset: 4px; }
.mm-mark { position: absolute; left: 0; right: 0; bottom: -4vw; z-index: 1; display: flex; justify-content: center; line-height: 0; pointer-events: none; }
.mm-mark .px { opacity: 0; transform: translateY(30%); transition: opacity 0.6s ease, transform 0.8s var(--spring); }
.menu-open .mm-mark .px { opacity: 1; transform: none; transition-delay: 0.5s; }
@media (max-width: 480px) {
  .mm-inner { padding-top: 112px; padding-bottom: calc(14vw + 12px); }
  .mm-list a { padding: 13px 2px; grid-template-columns: 30px 1fr 40px; }
  .mm-label { font-size: 32px; }
  .mm-arrow { width: 40px; height: 40px; }
  .mm-cta { margin-top: 22px; }
  .mm-primary, .mm-secondary { padding: 15px 18px; font-size: 16px; }
  .mm-foot { padding-top: 24px; font-size: 10px; }
}
.mm-mark .px {
  font-size: 17vw;
  --px-fill: linear-gradient(180deg, rgba(253,227,81,0.35), rgba(253,227,81,0.04));
}
html:not(.px-on) .mm-mark { display: none; }
.menu-open { overflow: hidden; }
.menu-open .site-header { z-index: 70; }
.menu-open .top-rule { z-index: 71; }

@media (max-width: 1100px) {
  .header-nav, .book-cta { display: none; }
  .menu-btn { display: grid; }
  .nav-frame { width: min(100%, 560px); }
  .nav-pill { width: 100%; justify-content: space-between; padding-left: 4px; }
}
@media (min-width: 1101px) {
  .mobile-menu { display: none !important; }
}
@media (prefers-reduced-motion: reduce) {
  .mobile-menu { transition: none; }
}

/* ════════════════════════════════════════════════
   SHARED SECTION HEAD
   ════════════════════════════════════════════════ */
.section { padding: 120px clamp(20px, 4vw, 56px); position: relative; }
.section-head { display: flex; justify-content: space-between; align-items: end; gap: 60px; margin-bottom: 64px; }
.section-head.center { flex-direction: column; align-items: center; text-align: center; gap: 0; }
.section-head.center .section-eyebrow { justify-content: center; }
.section-title {
  font-weight: 700;
  font-size: clamp(38px, 4.6vw, 68px);
  line-height: 1;
  letter-spacing: -0.035em;
  max-width: 760px;
}
.section-lede { font-size: 16px; line-height: 1.55; color: var(--ink-soft); max-width: 380px; }
.section-head.center .section-lede { margin-top: 22px; max-width: 520px; }

/* ════════════════════════════════════════════════
   LOGO MARQUEE
   ════════════════════════════════════════════════ */
.logos { padding: 72px 0 0; position: relative; z-index: 5; text-align: center; }
.logos-label {
  font-family: "JetBrains Mono", monospace; font-size: 11px;
  text-transform: uppercase; letter-spacing: 0.18em; color: var(--ink-soft);
  margin-bottom: 28px;
}
.marquee {
  overflow: hidden;
  -webkit-mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
  mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
}
.marquee-track { display: flex; width: max-content; animation: marquee 38s linear infinite; }
.marquee:hover .marquee-track { animation-play-state: paused; }
.marquee-group { display: flex; align-items: center; gap: 64px; padding-right: 64px; }
@keyframes marquee { to { transform: translateX(-50%); } }
.wordmark {
  display: inline-flex; align-items: center; gap: 9px;
  font-size: 22px; font-weight: 700; letter-spacing: -0.03em;
  color: #3a3934; opacity: 0.62; white-space: nowrap;
  transition: opacity 0.2s;
}
.wordmark:hover { opacity: 1; }
.wordmark i { display: inline-block; width: 18px; height: 18px; background: currentColor; }
.wm-circle i { border-radius: 50%; }
.wm-squish i { border-radius: 30% / 60%; }
.wm-tri i { clip-path: polygon(50% 0, 100% 100%, 0 100%); }
.wm-ring i { border-radius: 50%; background: transparent; border: 4px solid currentColor; }
.wm-diamond i { transform: rotate(45deg) scale(0.8); border-radius: 3px; }
.wm-serif { font-family: Georgia, "Times New Roman", serif; font-weight: 600; font-style: italic; letter-spacing: -0.01em; }
.wm-mono { font-family: "JetBrains Mono", monospace; font-size: 18px; font-weight: 600; letter-spacing: 0; }
.wm-light { font-weight: 400; letter-spacing: 0.04em; text-transform: uppercase; font-size: 18px; }

/* ════════════════════════════════════════════════
   PRODUCT BENTO
   ════════════════════════════════════════════════ */
.product { background: var(--bg); }
.bento { display: grid; grid-template-columns: repeat(4, 1fr); grid-auto-rows: minmax(260px, auto); gap: 20px; }
.tile {
  border-radius: 32px; padding: 28px;
  background: linear-gradient(180deg, #fff 0%, var(--cream) 100%);
  border: 1px solid var(--cream-line);
  box-shadow:
    inset 0 3px 0 rgba(255, 255, 255, 0.9),
    inset 0 -8px 18px -8px rgba(92, 82, 30, 0.12),
    0 18px 40px -20px rgba(92, 82, 24, 0.25);
  display: flex; flex-direction: column; gap: 10px;
  position: relative; overflow: hidden;
}
.tile h3 { font-size: 22px; font-weight: 700; letter-spacing: -0.02em; line-height: 1.1; }
.tile p { font-size: 14px; line-height: 1.55; color: var(--ink-soft); max-width: 380px; }
.tile-kicker {
  font-family: "JetBrains Mono", monospace; font-size: 10.5px;
  text-transform: uppercase; letter-spacing: 0.16em; color: var(--ink-soft);
}
.tile-visual { margin-top: auto; padding-top: 18px; }
.t-big { grid-column: span 2; grid-row: span 2; }
.t-wide { grid-column: span 2; }
.t-dark {
  background: linear-gradient(170deg, #1c1c1b 0%, #0a0a0a 100%);
  border-color: #000; color: #fff;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.1), inset 0 -2px 4px rgba(0,0,0,0.5), 0 2px 0 #000, 0 20px 40px -18px rgba(0,0,0,0.45);
}
.t-dark p, .t-dark .tile-kicker { color: #a9a9a2; }
.t-yellow {
  background: linear-gradient(170deg, var(--yellow-light) 0%, var(--yellow) 70%, var(--yellow-deep) 100%);
  border-color: var(--yellow-line);
  box-shadow: inset 0 3px 0 rgba(255,255,255,0.5), inset 0 -6px 14px -6px rgba(150,110,10,0.35), 0 20px 40px -18px rgba(200,160,30,0.45);
}
.t-yellow p, .t-yellow .tile-kicker { color: rgba(0,0,0,0.66); }

/* funnel visual */
.funnel { display: grid; gap: 10px; }
.funnel-row { display: grid; grid-template-columns: 110px 1fr 46px; align-items: center; gap: 12px; font-size: 13px; }
.funnel-row span:first-child { color: var(--ink-soft); }
.funnel-row b { font-family: "JetBrains Mono", monospace; font-size: 12px; font-weight: 600; text-align: right; font-variant-numeric: tabular-nums; }
.funnel-bar { height: 30px; border-radius: 9px; background: var(--cream-2); border: 1px solid var(--cream-line); overflow: hidden; }
.funnel-bar i {
  display: block; height: 100%; width: var(--w);
  background: linear-gradient(180deg, #2a2a2a, #0a0a0a);
  border-radius: 8px;
  transform-origin: left; 
}
.funnel-row.leak .funnel-bar i { background: linear-gradient(180deg, var(--yellow-light), var(--yellow-deep)); }
.funnel-row.leak b { color: #b3261e; }
.funnel-note {
  margin-top: 14px; display: flex; gap: 10px; align-items: flex-start;
  padding: 12px 14px; border-radius: 14px; background: #fff;
  border: 1px dashed var(--line-color); font-size: 13px; line-height: 1.45;
}
.funnel-note .chat-avatar { width: 26px; height: 26px; border-radius: 9px; }
.funnel-note .chat-avatar svg { width: 14px; height: 14px; }

/* alert toast */
.toast {
  display: flex; gap: 12px; align-items: center;
  padding: 12px 14px; border-radius: 16px; background: #fff;
  border: 1px solid var(--cream-line);
  box-shadow: 0 10px 24px -12px rgba(92,82,24,0.4);
  font-size: 13px; line-height: 1.35;
}
.toast + .toast { margin-top: 8px; opacity: 0.55; transform: scale(0.96); }
.toast-dot { width: 10px; height: 10px; border-radius: 50%; background: #e0533d; box-shadow: 0 0 0 4px rgba(224,83,61,0.15); flex: none; }
.toast small { display: block; font-family: "JetBrains Mono", monospace; font-size: 10px; color: var(--ink-soft); letter-spacing: 0.04em; }

/* code */
.code {
  font-family: "JetBrains Mono", monospace; font-size: 12px; line-height: 1.7;
  background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.08);
  border-radius: 14px; padding: 14px 16px; color: #d8d6cc; white-space: pre; overflow-x: auto;
}
.code .k { color: var(--yellow); }
.code .c { color: #7d7b72; }
.code .s { color: var(--mint); }

/* significance meter */
.meter { display: grid; gap: 8px; }
.meter-track { height: 14px; border-radius: 99px; background: rgba(0,0,0,0.12); overflow: hidden; box-shadow: inset 0 2px 3px rgba(0,0,0,0.15); }
.meter-track i { display: block; height: 100%; width: 87%; border-radius: 99px; background: linear-gradient(180deg, #2a2a2a, #0a0a0a); }
.meter-legend { display: flex; justify-content: space-between; font-family: "JetBrains Mono", monospace; font-size: 11px; font-weight: 600; }
.big-num { font-size: 56px; font-weight: 800; letter-spacing: -0.05em; line-height: 1; }

/* integrations */
.int-grid { display: flex; flex-wrap: wrap; gap: 8px; }
.int {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 8px 13px 9px; border-radius: 11px / 50%;
  background: #fff; border: 1px solid var(--cream-line);
  font-size: 13px; font-weight: 500;
  box-shadow: inset 0 -1.5px 0 rgba(92,82,30,0.08);
}
.int i { width: 8px; height: 8px; border-radius: 50%; background: var(--mint-deep); }
.int.more { background: var(--ink); color: #fff; border-color: #000; }

/* ════════════════════════════════════════════════
   TESTIMONIALS
   ════════════════════════════════════════════════ */
.voices { background: var(--bg-warm); }
.voice-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
.voice {
  border-radius: 30px; padding: 30px;
  background: #fff; border: 1px solid var(--cream-line);
  box-shadow: inset 0 -6px 14px -8px rgba(92,82,30,0.14), 0 16px 36px -22px rgba(92,82,24,0.3);
  display: flex; flex-direction: column; gap: 22px;
}
.voice-metric { display: flex; align-items: baseline; gap: 10px; }
.voice-metric b { font-size: 44px; font-weight: 800; letter-spacing: -0.05em; line-height: 1; }
.voice-metric span { font-family: "JetBrains Mono", monospace; font-size: 10.5px; text-transform: uppercase; letter-spacing: 0.14em; color: var(--ink-soft); }
.voice blockquote { font-size: 17px; line-height: 1.45; letter-spacing: -0.01em; flex: 1; }
.voice-who { display: flex; align-items: center; gap: 12px; padding-top: 18px; border-top: 1px dashed var(--cream-deep); }
.voice-av {
  width: 40px; height: 40px; border-radius: 14px; display: grid; place-items: center;
  font-weight: 700; font-size: 14px;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.6), inset 0 -2px 3px rgba(0,0,0,0.12);
}
.voice-who strong { display: block; font-size: 14px; }
.voice-who small { font-size: 12.5px; color: var(--ink-soft); }

/* ════════════════════════════════════════════════
   PRICING
   ════════════════════════════════════════════════ */
.pricing { background: var(--bg); }
.billing {
  margin-top: 32px; display: inline-flex; padding: 5px; gap: 4px;
  background: linear-gradient(180deg, #1a1a1a, #0a0a0a);
  border-radius: 17px / 50%;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.08), 0 2px 0 #000, 0 10px 20px -10px rgba(0,0,0,0.35);
}
.billing button {
  font: inherit; font-size: 14px; font-weight: 600;
  border: 0; cursor: pointer; color: #ccc; background: transparent;
  padding: 9px 18px 10px; border-radius: 12px / 50%;
  display: inline-flex; align-items: center; gap: 8px;
  transition: background 0.25s, color 0.25s, border-radius 0.3s;
}
.billing button[aria-pressed="true"] {
  color: var(--ink);
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.6);
}
.billing em {
  font-style: normal; font-family: "JetBrains Mono", monospace; font-size: 10px;
  letter-spacing: 0.08em; padding: 2px 6px; border-radius: 6px;
  background: var(--mint); color: var(--ink);
}
.plans { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; align-items: stretch; }
.plan {
  border-radius: 34px; padding: 34px 30px 30px;
  background: linear-gradient(180deg, #fff 0%, var(--cream) 100%);
  border: 1px solid var(--cream-line);
  box-shadow: inset 0 3px 0 rgba(255,255,255,0.9), inset 0 -8px 18px -8px rgba(92,82,30,0.12), 0 18px 40px -22px rgba(92,82,24,0.3);
  display: flex; flex-direction: column; position: relative;
}
.plan.featured {
  background: linear-gradient(170deg, #1f1f1e 0%, #0a0a0a 100%);
  border-color: #000; color: #fff;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.12), 0 2px 0 #000, 0 30px 60px -24px rgba(0,0,0,0.5);
  transform: translateY(-12px);
}
.plan-badge {
  position: absolute; top: -16px; right: 26px;
  font-family: "JetBrains Mono", monospace; font-size: 10.5px; font-weight: 600;
  text-transform: uppercase; letter-spacing: 0.14em; color: var(--ink);
  padding: 7px 12px 6px; border-radius: 10px / 50%;
  background: linear-gradient(180deg, var(--yellow-light), var(--yellow-deep));
  border: 1px solid var(--yellow-line);
  box-shadow: 0 6px 14px -4px rgba(200,160,30,0.5);
}
.plan-name { font-family: "JetBrains Mono", monospace; font-size: 11px; text-transform: uppercase; letter-spacing: 0.16em; color: var(--ink-soft); }
.plan.featured .plan-name, .plan.featured .plan-desc, .plan.featured .per { color: #a9a9a2; }
.price { margin: 18px 0 6px; display: flex; align-items: baseline; gap: 6px; }
.price .amt { font-size: 60px; font-weight: 800; letter-spacing: -0.05em; line-height: 1; font-variant-numeric: tabular-nums; }
.per { font-size: 14px; color: var(--ink-soft); }
.plan-desc { font-size: 14px; color: var(--ink-soft); line-height: 1.5; min-height: 42px; }
.plan ul { list-style: none; margin: 24px 0 28px; display: grid; gap: 11px; font-size: 14px; flex: 1; }
.plan li { display: flex; gap: 10px; align-items: flex-start; }
.plan li::before {
  content: ""; flex: none; width: 18px; height: 18px; margin-top: 1px; border-radius: 6px;
  background: var(--mint) url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%230a0a0a' stroke-width='3' stroke-linecap='round' stroke-linejoin='round'><path d='M6 12l4 4 8-8'/></svg>") center / 12px no-repeat;
}
.plan.featured li::before { background-color: var(--yellow); }
.plan-cta {
  display: flex; justify-content: center; align-items: center; gap: 8px;
  padding: 13px 18px 14px; border-radius: 14px / 50%;
  font-size: 15px; font-weight: 600;
  background: #fff; border: 1px solid var(--cream-deep);
  box-shadow: inset 0 -2px 0 rgba(92,82,30,0.08);
  transition: border-radius 0.3s ease-in-out, transform 0.2s;
}
.plan-cta:hover { border-radius: 5px / 50%; }
.plan-cta:active { transform: scale(0.98); }
.plan.featured .plan-cta {
  background: linear-gradient(180deg, var(--yellow-light) 0%, var(--yellow) 55%, var(--yellow-deep) 100%);
  border-color: var(--yellow-line);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.6), inset 0 -1px 2px rgba(180,140,30,0.3);
  color: var(--ink);
}
.pricing-foot {
  margin-top: 40px; text-align: center;
  font-family: "JetBrains Mono", monospace; font-size: 11px;
  text-transform: uppercase; letter-spacing: 0.14em; color: var(--ink-soft);
}

/* ════════════════════════════════════════════════
   FAQ
   ════════════════════════════════════════════════ */
.faq { background: var(--bg-warm); }
.faq-wrap { display: grid; grid-template-columns: minmax(0, 0.8fr) minmax(0, 1.2fr); gap: 60px; align-items: start; }
.faq-side { position: sticky; top: 120px; }
.faq-side .section-lede { margin-top: 22px; }
.faq-side a { text-decoration: underline; text-underline-offset: 3px; text-decoration-color: var(--yellow-deep); text-decoration-thickness: 2px; }
.faq-list { display: grid; gap: 12px; }
.faq-item {
  border-radius: 22px; background: #fff; border: 1px solid var(--cream-line);
  box-shadow: inset 0 -4px 10px -6px rgba(92,82,30,0.12);
  transition: box-shadow 0.3s;
}
.faq-item[open] { box-shadow: inset 0 -4px 10px -6px rgba(92,82,30,0.12), 0 16px 30px -20px rgba(92,82,24,0.35); }
.faq-item summary {
  list-style: none; cursor: pointer;
  padding: 22px 24px; display: flex; justify-content: space-between; align-items: center; gap: 20px;
  font-size: 17px; font-weight: 600; letter-spacing: -0.01em;
  border-radius: 22px;
}
.faq-item summary::-webkit-details-marker { display: none; }
.faq-plus {
  flex: none; width: 32px; height: 32px; border-radius: 11px; display: grid; place-items: center;
  background: var(--cream-2); border: 1px solid var(--cream-line);
  transition: transform 0.35s var(--spring), background 0.2s;
}
.faq-plus svg { width: 14px; height: 14px; }
.faq-item[open] .faq-plus { transform: rotate(45deg); background: var(--yellow); border-color: var(--yellow-line); }
.faq-item p { padding: 0 24px 24px; font-size: 15px; line-height: 1.6; color: var(--ink-soft); max-width: 620px; }

@media (max-width: 1100px) {
  .hero { grid-template-columns: 1fr; gap: 60px; min-height: 0; }
  .stats-grid { grid-template-columns: repeat(2, 1fr); }
  .stat:nth-child(2) { border-right: none; }
  .feature-cards { grid-template-columns: 1fr; }
  .features, .stats-bar { padding-block: 60px; }
  .final-cta, .quote-section { padding-block: 60px; }
  .features-head { flex-direction: column; align-items: flex-start; }
  .features-meta { text-align: left; }
  .footer-top { flex-direction: column; gap: 40px; }
}

@media (max-width: 700px) {
  .header-nav { display: none; }
  .chat { height: 540px; border-radius: 28px; }
  .stats-grid { grid-template-columns: 1fr; }
  .stat { border-right: none; border-bottom: 1px solid rgba(0, 0, 0, 0.08); }
  .stat:last-child { border-bottom: none; }
  .quote-section { padding-block: 80px; }
}
@media (max-width: 480px) {
  .chat-tag { display: none; }
  .msg { max-width: 94%; }
}


@media (max-width: 1100px) {
  .section { padding-block: 72px; }
  .section-head { flex-direction: column; align-items: flex-start; gap: 20px; }
  .bento { grid-template-columns: repeat(2, 1fr); }
  .voice-grid, .plans { grid-template-columns: 1fr; max-width: 560px; margin-inline: auto; }
  .plan.featured { transform: none; }
  .faq-wrap { grid-template-columns: 1fr; gap: 36px; }
  .faq-side { position: static; }
}
@media (max-width: 700px) {
  .bento { grid-template-columns: 1fr; }
  .t-big, .t-wide { grid-column: auto; grid-row: auto; }
  .funnel-row { grid-template-columns: 84px 1fr 40px; }
  .wordmark { font-size: 19px; }
  .marquee-group { gap: 44px; padding-right: 44px; }
}

@media (prefers-reduced-motion: reduce) {
  .marquee-track { animation: none !important; }
}
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.001ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.001ms !important;
  }
}
</style>
</head>
<body>
<a class="skip" href="#main">Skip to content</a>

<div class="ambient-1" aria-hidden="true"></div>
<div class="ambient-2" aria-hidden="true"></div>

<div class="top-rule" aria-hidden="true"></div>

<header class="site-header" data-section="nav">
  <div class="nav-frame">
    <div class="line horizontal top" aria-hidden="true"></div>
    <div class="line vertical right" aria-hidden="true"></div>
    <div class="line horizontal bottom" aria-hidden="true"></div>
    <div class="line vertical left" aria-hidden="true"></div>
    <div class="dot top left" aria-hidden="true"></div>
    <div class="dot top right" aria-hidden="true"></div>
    <div class="dot bottom right" aria-hidden="true"></div>
    <div class="dot bottom left" aria-hidden="true"></div>
  <div class="nav-pill">
  <div class="logo">
    <span class="logo-cube" aria-hidden="true">
      <svg width="34" height="34" viewBox="0 0 34 34" fill="none">
        <defs>
          <linearGradient id="cubeGrad" x1="0" y1="0" x2="1" y2="1">
            <stop offset="0%" stop-color="#3a3a3a" />
            <stop offset="100%" stop-color="#0a0a0a" />
          </linearGradient>
        </defs>
        <path d="M17 3 L29 9 L29 21 L17 27 L17 15 L5 9 Z" fill="url(#cubeGrad)" stroke="#000" stroke-width="0.5" />
        <path d="M5 9 L17 15 L17 27 L5 21 Z" fill="#2a2a2a" stroke="#000" stroke-width="0.5" />
        <path d="M17 3 L29 9 L17 15 L5 9 Z" fill="#444" stroke="#000" stroke-width="0.5" />
      </svg>
    </span>
    <span>TRAFFO<span class="logo-ai">AI</span></span>
  </div>
  <nav class="header-nav" aria-label="Primary">
    <a href="#product">Product</a>
    <a href="#features">Features
      <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <polyline points="6 9 12 15 18 9" />
      </svg>
    </a>
    <a href="#quote">Customers</a>
    <a href="#pricing">Pricing</a>
  </nav>
  <a class="book-cta" href="#start">Start for free</a>
  <button class="menu-btn" type="button" aria-expanded="false" aria-controls="mobileMenu" aria-label="Open menu">
    <span class="mb-lines" aria-hidden="true"><i></i><i></i></span>
  </button>
  </div>
  </div>
</header>

<div class="mobile-menu" id="mobileMenu" data-section="menu" role="dialog" aria-modal="true" aria-label="Site menu" hidden>
  <span class="finale-grid" aria-hidden="true"></span>
  <span class="mm-glow" aria-hidden="true"></span>
  <div class="mm-inner">
    <div class="mm-top" style="--i:0"><span class="px">menu</span><span class="mm-status"><i class="live-dot"></i>All systems normal</span></div>
    <nav aria-label="Mobile">
      <ul class="mm-list">
      <li style="--i:0"><a href="#product"><span class="mm-num">01</span><span class="mm-text"><span class="mm-label">Product</span><span class="mm-sub">The assistant, up close</span></span><span class="mm-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M9 7h8v8"/></svg></span></a></li>
      <li style="--i:1"><a href="#features"><span class="mm-num">02</span><span class="mm-text"><span class="mm-label">Features</span><span class="mm-sub">Ask · Understand · Ship</span></span><span class="mm-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M9 7h8v8"/></svg></span></a></li>
      <li style="--i:2"><a href="#customers"><span class="mm-num">03</span><span class="mm-text"><span class="mm-label">Customers</span><span class="mm-sub">Teams shipping with Traffo</span></span><span class="mm-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M9 7h8v8"/></svg></span></a></li>
      <li style="--i:3"><a href="#pricing"><span class="mm-num">04</span><span class="mm-text"><span class="mm-label">Pricing</span><span class="mm-sub">Start free, scale later</span></span><span class="mm-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M9 7h8v8"/></svg></span></a></li>
      <li style="--i:4"><a href="#faq"><span class="mm-num">05</span><span class="mm-text"><span class="mm-label">FAQ</span><span class="mm-sub">Before you ask, ask us</span></span><span class="mm-arrow"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M7 17 17 7M9 7h8v8"/></svg></span></a></li>
      </ul>
    </nav>
    <div class="mm-cta" style="--i:5">
      <a class="mm-primary" href="#start">Start for free<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"/></svg></a>
      <a class="mm-secondary" href="#product"><span class="demo-play" aria-hidden="true"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M8 5.5v13l11-6.5z"/></svg></span>Watch 2 min demo</a>
    </div>
    <div class="mm-foot" style="--i:6">
      <span>Free for your first 10,000 events</span>
      <a href="#start">Sign in</a>
    </div>
  </div>
  <div class="mm-mark" aria-hidden="true"><span class="px">traffo</span></div>
</div>

<main class="hero" id="main" data-section="hero">
  <span class="glass glass--tab" aria-hidden="true"><i class="live-dot"></i><span>Assistant 4.2<br />now live</span></span>
  
  <div class="hero-left">
    <p class="hero-eyebrow"><span class="px">turn data into conversions</span></p>
    <h1 class="hero-title">
      <span class="title-line"><span class="title-inner">An AI analyst</span></span>
      <span class="title-line accent-line"><span class="title-inner"><span class="title-hl"><span class="px-shadow"><span class="px">for every</span></span></span></span></span>
      <span class="title-line"><span class="title-inner">conversion</span></span>
    </h1>
    <p class="hero-desc">Ask Traffo why visitors leave. It reads every session, finds where your funnel leaks and drafts the test that fixes it, all in plain English.</p>

    <div class="hero-ctas">
      <span class="btn-wrapper">
        <div class="line horizontal top" aria-hidden="true"></div>
        <div class="line vertical right" aria-hidden="true"></div>
        <div class="line horizontal bottom" aria-hidden="true"></div>
        <div class="line vertical left" aria-hidden="true"></div>
        <div class="dot top left" aria-hidden="true"></div>
        <div class="dot top right" aria-hidden="true"></div>
        <div class="dot bottom right" aria-hidden="true"></div>
        <div class="dot bottom left" aria-hidden="true"></div>
        <a class="btn btn-lg" href="#start"><span class="btn-text">Start for free</span><svg class="btn-svg" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"></path></svg></a>
      </span>
      <a class="demo-btn" href="#product">
        <span class="demo-play" aria-hidden="true"><svg viewBox="0 0 24 24" fill="currentColor"><path d="M8 5.5v13l11-6.5z"/></svg></span>
        Watch 2 min demo
      </a>
    </div>

    <ul class="hero-trust">
      <li><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M13 2 4 14h7l-1 8 9-12h-7z"/></svg><span>No credit card<br />required</span></li>
      <li><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><rect x="4" y="13" width="4" height="7" rx="1"/><rect x="10" y="9" width="4" height="11" rx="1"/><rect x="16" y="5" width="4" height="15" rx="1"/></svg><span>Live on<br />your data</span></li>
      <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="9" cy="8" r="3.2"/><path d="M3 20c0-3.3 2.7-5.5 6-5.5s6 2.2 6 5.5"/><circle cx="17" cy="9" r="2.6"/><path d="M16.5 14.6c2.6.2 4.5 2.2 4.5 5"/></svg><span>Trusted by<br />4,000+ growth teams</span></li>
    </ul>
  </div>

  <div class="hero-right">
    <div class="hero-visual">
      <span class="hv-glow" aria-hidden="true"></span>
      <span class="hv-dots hv-dots--a" aria-hidden="true"></span>
      <span class="hv-dots hv-dots--b" aria-hidden="true"></span>

      <div class="chat-stage">
        <section class="chat" aria-label="Demo chat with the Traffo assistant" data-component="chat-demo">
        <header class="chat-head">
          <span class="chat-avatar"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 L13.5 10.5 L22 12 L13.5 13.5 L12 22 L10.5 13.5 L2 12 L10.5 10.5 Z" /></svg></span>
          <div class="chat-who">
            <div class="chat-name">Traffo AI</div>
            <div class="chat-status">Online · reading 2.4B events</div>
          </div>
          <span class="chat-tag">Demo</span>
        </header>
        <div class="chat-log" id="chatLog" role="log" aria-live="polite"></div>
        <div class="chat-suggest" id="chatSuggest" hidden>
          <button class="chip" type="button">Show funnel</button>
          <button class="chip" type="button">Bounce rate?</button>
          <button class="chip" type="button">Top revenue source</button>
        </div>
        <form class="composer" id="chatForm" autocomplete="off">
          <label for="chatInput" class="sr-only">Ask Traffo a question</label>
          <textarea id="chatInput" rows="1" placeholder="Ask about your traffic…"></textarea>
          <button class="send" type="submit">Send
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" /></svg>
          </button>
        </form>
      </section>
      </div>

      <div class="float-card fc-rate" aria-hidden="true">
        <div class="fl-inner">
          <span class="fl-label">Conversion rate</span>
          <div class="fl-row"><b class="fl-big">4.8%</b><span class="fl-up">↑ 12%</span></div>
          <svg class="fl-spark" viewBox="0 0 150 54" fill="none"><path d="M3 50 C 18 30, 26 28, 38 34 S 60 44, 74 30 S 98 22, 110 26 S 132 12, 146 8" /><circle cx="146" cy="8" r="4.5" /></svg>
        </div>
      </div>

      <div class="float-card fc-fix" aria-hidden="true">
        <div class="fl-inner">
          <span class="fl-title">Fix detected</span>
          <ul class="fl-list">
            <li><svg viewBox="0 0 24 24"><path d="M12 3 2 20h20z" fill="#f4c21a"/><path d="M12 9v5M12 17h.01" stroke="#0a0a0a" stroke-width="2" stroke-linecap="round"/></svg>Form validation error</li>
            <li><svg viewBox="0 0 24 24" fill="none" stroke="#0a0a0a" stroke-width="1.8"><rect x="7" y="2.5" width="10" height="19" rx="2.4"/><path d="M11 18.5h2" stroke-linecap="round"/></svg>Mobile Safari</li>
            <li><svg viewBox="0 0 24 24" fill="#0a0a0a"><path d="M14.5 3.5c3-1 5.5-1 6 0 1 .5 1 3 0 6l-6.2 6.2-6-6zM7 11l-3.5.5L2 14l4 .5zM13 17l-.5 3.5L10 22l-.5-4zM6.5 15.5c-1.5.3-2.8 2-3 5 3-.2 4.7-1.5 5-3z"/></svg>Deploy test draft</li>
          </ul>
        </div>
      </div>

    </div>
  </div>
</main>


<section class="logos" aria-label="Teams using Traffo" data-section="logos">
  <p class="logos-label">Trusted by 4,000+ growth teams</p>
  <div class="marquee">
    <div class="marquee-track">
      <div class="marquee-group">
        <span class="wordmark wm-circle"><i></i>Makebelief</span>
        <span class="wordmark wm-serif">Holloway &amp; Pine</span>
        <span class="wordmark wm-squish"><i></i>Brightloom</span>
        <span class="wordmark wm-mono">northwind/</span>
        <span class="wordmark wm-tri"><i></i>Kestrel</span>
        <span class="wordmark wm-light">Oatfield</span>
        <span class="wordmark wm-ring"><i></i>Lumenary</span>
        <span class="wordmark wm-diamond"><i></i>Parcelry</span>
      </div>
      <div class="marquee-group" aria-hidden="true">
        <span class="wordmark wm-circle"><i></i>Makebelief</span>
        <span class="wordmark wm-serif">Holloway &amp; Pine</span>
        <span class="wordmark wm-squish"><i></i>Brightloom</span>
        <span class="wordmark wm-mono">northwind/</span>
        <span class="wordmark wm-tri"><i></i>Kestrel</span>
        <span class="wordmark wm-light">Oatfield</span>
        <span class="wordmark wm-ring"><i></i>Lumenary</span>
        <span class="wordmark wm-diamond"><i></i>Parcelry</span>
      </div>
    </div>
  </div>
</section>

<section class="stats-bar" aria-label="Traffo by the numbers" data-section="stats">
  <div class="metrics-head">
    <div class="section-eyebrow"><span class="px">traffo by the numbers</span></div>
    <span class="metrics-live"><i class="live-dot"></i>Live across all workspaces</span>
  </div>
  <div class="metric-grid">
    <article class="metric m-dark">
      <span class="metric-label"><span class="px">questions per day</span></span>
      <div class="stat-num" data-num="546" data-prefix="+" data-suffix="k">+546<span class="accent">k</span></div>
      <div class="m-bars" aria-hidden="true"><i style="--h:18%"></i><i style="--h:22%"></i><i style="--h:20%"></i><i style="--h:28%"></i><i style="--h:26%"></i><i style="--h:34%"></i><i style="--h:31%"></i><i style="--h:40%"></i><i style="--h:44%"></i><i style="--h:41%"></i><i style="--h:52%"></i><i style="--h:58%"></i><i style="--h:63%"></i><i style="--h:72%"></i><i style="--h:70%"></i><i style="--h:84%"></i></div>
      <span class="m-foot">+38% month over month</span>
    </article>
    <article class="metric">
      <span class="metric-label"><span class="px">median answer</span></span>
      <div class="stat-num" data-num="1.8" data-decimals="1" data-suffix="s">1.8<span class="accent">s</span></div>
      <svg class="m-gauge" viewBox="0 0 200 110" aria-hidden="true">
        <path class="g-track" d="M20 100 A80 80 0 0 1 180 100" />
        <path class="g-fill" d="M20 100 A80 80 0 0 1 180 100" pathLength="100" />
        <g class="g-ticks"><path d="M20 100h10M100 20v10M180 100h-10M43.4 43.4l7 7M156.6 43.4l-7 7" /></g>
        <line class="g-needle" x1="100" y1="100" x2="100" y2="34" />
        <circle class="g-hub" cx="100" cy="100" r="7" />
      </svg>
      <span class="m-foot">p95 under 4 seconds</span>
    </article>
    <article class="metric m-yellow">
      <span class="metric-label"><span class="px">events per day</span></span>
      <div class="stat-num" data-num="2.4" data-decimals="1" data-suffix="B">2.4<span class="accent">B</span></div>
      <div class="m-matrix" aria-hidden="true"><i class="on"></i><i class="on"></i><i></i><i class="on"></i><i></i><i class="on"></i><i class="on"></i><i></i><i class="on"></i><i></i><i class="on"></i><i class="on"></i><i></i><i></i><i class="on"></i><i class="on"></i><i></i><i></i><i></i><i class="on"></i><i></i><i class="on"></i><i></i><i class="on"></i><i class="on"></i><i class="on"></i><i class="on"></i><i></i><i class="on"></i><i></i><i></i><i class="on"></i><i></i><i class="on"></i><i class="on"></i><i class="on"></i><i></i><i></i><i class="on"></i><i></i><i></i><i class="on"></i><i></i><i></i><i class="on"></i><i></i><i></i><i></i></div>
      <span class="m-foot">Raw events, never sampled</span>
    </article>
    <article class="metric">
      <span class="metric-label"><span class="px">faster answers</span></span>
      <div class="stat-num" data-num="42" data-suffix="×">42<span class="accent">×</span></div>
      <div class="m-race" aria-hidden="true">
        <div class="race-row"><span>Building a report</span><b>~2 days</b></div>
        <div class="race-bar slow"><i></i></div>
        <div class="race-row"><span>Asking Traffo</span><b>~1 hour</b></div>
        <div class="race-bar fast"><i></i></div>
      </div>
      <span class="m-foot">Than building the report yourself</span>
    </article>
  </div>
</section>

<section class="features" id="features" data-section="features">
  <div class="features-head">
    <div>
      <div class="section-eyebrow"><span class="px">how traffo works</span></div>
      <h2 class="features-title">Ask. Understand. Ship. No dashboards required.</h2>
    </div>
    <div class="features-meta">
      ASSISTANT 4.2<br />
      SHIPPED MAY 2026<br />
      24 INTEGRATIONS
    </div>
  </div>

  <div class="feature-cards">
    <article class="feature-card framed fc-mint">
      <div class="fc-top"><span class="fc-step">01</span><span class="fc-chip"><span class="px">ask</span></span></div>
      <div class="fc-visual v-ask" aria-hidden="true">
        <div class="ask-input"><span class="ask-q">why did signups dip on tuesday?</span><i class="caret"></i></div>
        <div class="ask-answer"><span class="chat-avatar"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 L13.5 10.5 L22 12 L13.5 13.5 L12 22 L10.5 13.5 L2 12 L10.5 10.5 Z" /></svg></span><span><b>Mobile Safari</b> form stopped validating<em>−18%</em></span></div>
        <div class="ask-meta"><span>signups</span><span>· 7 days</span><span>· 1.6s</span></div>
      </div>
      <h3>Plain questions. Real answers.</h3>
      <p>Type “why did signups dip on Tuesday?” and get the answer with the chart behind it. No SQL, no tagging, no waiting on the data team.</p>
    </article>

    <article class="feature-card framed fc-yellow">
      <div class="fc-top"><span class="fc-step">02</span><span class="fc-chip"><span class="px">understand</span></span></div>
      <div class="fc-visual v-leak" aria-hidden="true">
        <div class="leak-head"><span>Checkout funnel</span><b><i></i>Leak found</b></div>
        <svg viewBox="0 0 300 110" preserveAspectRatio="none">
          <path class="lk-area" d="M0 30 C 30 26, 60 32, 90 28 S 140 24, 160 30 L 175 70 C 195 76, 230 72, 260 78 S 290 74, 300 76 L 300 110 L 0 110 Z" />
          <path class="lk-line" d="M0 30 C 30 26, 60 32, 90 28 S 140 24, 160 30 L 175 70 C 195 76, 230 72, 260 78 S 290 74, 300 76" />
          <line class="lk-deploy" x1="167" y1="6" x2="167" y2="110" />
          <circle class="lk-dot" cx="175" cy="70" r="6" />
        </svg>
        <div class="leak-tag">Deploy #482 · /checkout +2.3s</div>
      </div>
      <h3>It finds the leak before you do.</h3>
      <p>Traffo watches every funnel around the clock and flags drop-offs, broken forms and slow pages the moment they start costing you conversions.</p>
    </article>

    <article class="feature-card framed fc-purple">
      <div class="fc-top"><span class="fc-step">03</span><span class="fc-chip"><span class="px">ship</span></span></div>
      <div class="fc-visual v-ab" aria-hidden="true">
        <div class="ab-row"><span class="ab-key">A</span><div class="ab-bar"><i style="--w:62%"></i></div><b>4.1%</b></div>
        <div class="ab-row win"><span class="ab-key">B</span><div class="ab-bar"><i style="--w:80%"></i></div><b>5.3%</b><span class="ab-badge">Winner</span></div>
        <div class="ab-foot"><span>3,214 visitors</span><span class="ab-conf"><i></i>96% confidence</span></div>
      </div>
      <h3>From answer to experiment in one message.</h3>
      <p>Ask for a fix and Traffo drafts the A/B test, sizes the audience and tells you when the result is significant.</p>
    </article>
  </div>
</section>


<section class="section product" id="product" data-section="product">
  <div class="section-head">
    <div>
      <div class="section-eyebrow"><span class="px">inside the assistant</span></div>
      <h2 class="section-title">Everything a data team does, one message away.</h2>
    </div>
    <p class="section-lede">Traffo reads raw events, not sampled reports, so every answer comes with the numbers and the query behind it.</p>
  </div>

  <div class="bento">
    <article class="tile t-big framed">
      <span class="tile-kicker">Funnel autopsy</span>
      <h3>It shows you exactly which step is bleeding.</h3>
      <p>Every funnel, every segment, compared against its own history. The step that broke is highlighted before anyone files a ticket.</p>
      <div class="tile-visual">
        <div class="funnel">
          <div class="funnel-row"><span>Landing</span><div class="funnel-bar"><i style="--w:100%"></i></div><b>100%</b></div>
          <div class="funnel-row"><span>Pricing</span><div class="funnel-bar"><i style="--w:61%"></i></div><b>61%</b></div>
          <div class="funnel-row"><span>Signup form</span><div class="funnel-bar"><i style="--w:34%"></i></div><b>34%</b></div>
          <div class="funnel-row leak"><span>Confirmed</span><div class="funnel-bar"><i style="--w:9%"></i></div><b>9%</b></div>
        </div>
        <div class="funnel-note"><span class="chat-avatar"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 L13.5 10.5 L22 12 L13.5 13.5 L12 22 L10.5 13.5 L2 12 L10.5 10.5 Z" /></svg></span><span><strong>Form → confirmed</strong> fell from 22% to 9% on mobile Safari after Tuesday’s deploy.</span></div>
      </div>
    </article>

    <article class="tile framed">
      <span class="tile-kicker">Watchdog</span>
      <h3>Alerts that explain themselves.</h3>
      <div class="tile-visual">
        <div class="toast"><span class="toast-dot"></span><span><strong>/checkout slowed to 4.1s</strong><small>Paid traffic · 2 min ago</small></span></div>
        <div class="toast"><span class="toast-dot"></span><span><strong>Promo code field erroring</strong><small>Android · 1 hr ago</small></span></div>
      </div>
    </article>

    <article class="tile t-dark framed">
      <span class="tile-kicker">Show your work</span>
      <h3>Every answer, with its query.</h3>
      <div class="tile-visual">
<div class="code"><span class="c">-- why did signups drop?</span>
<span class="k">select</span> browser, count(*)
<span class="k">from</span> signup_attempts
<span class="k">where</span> error = <span class="s">'email_invalid'</span>
<span class="k">group by</span> 1;</div>
      </div>
    </article>

    <article class="tile t-yellow framed">
      <span class="tile-kicker">Experiments</span>
      <h3>Knows when to call it.</h3>
      <div class="tile-visual">
        <div class="big-num">87%</div>
        <div class="meter">
          <div class="meter-track"><i></i></div>
          <div class="meter-legend"><span>Confidence</span><span>Ship at 95%</span></div>
        </div>
      </div>
    </article>

    <article class="tile framed">
      <span class="tile-kicker">Connects in minutes</span>
      <h3>Reads where your data lives.</h3>
      <div class="tile-visual">
        <div class="int-grid">
          <span class="int"><i></i>Web SDK</span><span class="int"><i></i>Data warehouse</span>
          <span class="int"><i></i>Payments</span><span class="int"><i></i>CRM</span>
          <span class="int"><i></i>Ad platforms</span><span class="int"><i></i>Email</span>
                    <span class="int more">+16 more</span>
        </div>
      </div>
    </article>
  </div>
</section>

<section class="quote-section" id="quote" aria-label="Customer quote" data-section="quote">
  <span class="quote-mark" aria-hidden="true">"</span>
  <blockquote class="quote-text">We stopped building dashboards and started asking Traffo. Our conversion rate went up 38% in a quarter.</blockquote>
  <div class="quote-author">— Trinette Eckard, Head of Growth at Makebelief</div>
</section>


<section class="section voices" id="customers" data-section="testimonials">
  <div class="section-head">
    <div>
      <div class="section-eyebrow"><span class="px">from the teams using it</span></div>
      <h2 class="section-title">Fewer dashboards. Better quarters.</h2>
    </div>
    <p class="section-lede">Growth, product and marketing teams use Traffo to get from “something’s off” to a shipped fix in the same afternoon.</p>
  </div>
  <div class="voice-grid">
    <figure class="voice">
      <div class="voice-metric"><b>−6 hrs</b><span>Weekly reporting</span></div>
      <blockquote>Our Monday metrics review used to take a morning of exports. Now we ask Traffo the five questions and spend the meeting deciding what to do.</blockquote>
      <figcaption class="voice-who"><span class="voice-av" style="background:var(--mint)">OA</span><span><strong>Odile Ashworth</strong><small>VP Product, Brightloom</small></span></figcaption>
    </figure>
    <figure class="voice">
      <div class="voice-metric"><b>+21%</b><span>Trial to paid</span></div>
      <blockquote>It found a pricing-page bug only Firefox users hit. We’d been blaming the copy for two months.</blockquote>
      <figcaption class="voice-who"><span class="voice-av" style="background:var(--yellow)">DK</span><span><strong>Dev Kalra</strong><small>Growth Lead, Kestrel</small></span></figcaption>
    </figure>
    <figure class="voice">
      <div class="voice-metric"><b>3×</b><span>Tests shipped</span></div>
      <blockquote>The experiment drafts are the part I didn’t expect. It sizes the audience and tells me when to stop, so we run three tests where we used to run one.</blockquote>
      <figcaption class="voice-who"><span class="voice-av" style="background:var(--purple)">MR</span><span><strong>Maren Rios</strong><small>Head of CRO, Parcelry</small></span></figcaption>
    </figure>
  </div>
</section>

<section class="section pricing" id="pricing" data-section="pricing">
  <div class="section-head center">
    <div class="section-eyebrow"><span class="px">pricing</span></div>
    <h2 class="section-title">Start free. Pay when it pays for itself.</h2>
    <div class="billing" role="group" aria-label="Billing period">
      <button type="button" data-bill="monthly" aria-pressed="true">Monthly</button>
      <button type="button" data-bill="yearly" aria-pressed="false">Yearly <em>−20%</em></button>
    </div>
  </div>
  <div class="plans">
    <article class="plan">
      <span class="plan-name">Starter</span>
      <div class="price"><span class="amt">$0</span><span class="per">/ month</span></div>
      <p class="plan-desc">For side projects and first questions.</p>
      <ul>
        <li>10,000 events a month</li>
        <li>100 questions a month</li>
        <li>1 site, 2 seats</li>
        <li>7-day history</li>
      </ul>
      <a class="plan-cta" href="#start">Start for free</a>
    </article>
    <article class="plan featured">
      <span class="plan-badge">Most popular</span>
      <span class="plan-name">Growth</span>
      <div class="price"><span class="amt" data-monthly="$79" data-yearly="$63">$79</span><span class="per">/ month</span></div>
      <p class="plan-desc">For teams running experiments every week.</p>
      <ul>
        <li>2M events a month</li>
        <li>Unlimited questions</li>
        <li>Anomaly alerts &amp; Slack digests</li>
        <li>Experiment drafting &amp; sizing</li>
        <li>13-month history, 10 seats</li>
      </ul>
      <a class="plan-cta" href="#start">Start 14-day trial</a>
    </article>
    <article class="plan">
      <span class="plan-name">Scale</span>
      <div class="price"><span class="amt">Custom</span></div>
      <p class="plan-desc">For high-volume sites and data teams.</p>
      <ul>
        <li>Unlimited events &amp; seats</li>
        <li>Warehouse-native mode</li>
        <li>SSO, SCIM &amp; audit log</li>
        <li>Dedicated analyst onboarding</li>
      </ul>
      <a class="plan-cta" href="#start">Talk to us</a>
    </article>
  </div>
  <p class="pricing-foot">No card for Starter · Cancel anytime · SOC 2 Type II</p>
</section>

<section class="section faq" id="faq" data-section="faq">
  <div class="faq-wrap">
    <div class="faq-side">
      <div class="section-eyebrow"><span class="px">questions</span></div>
      <h2 class="section-title">Before you ask Traffo, ask us.</h2>
      <p class="section-lede">Can’t find what you need? <a href="#start">Talk to the team</a> and a real person will reply within a day.</p>
    </div>
    <div class="faq-list">
      <details class="faq-item" open>
        <summary>Where does Traffo get its answers?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>From your own events. Traffo runs real queries against the data you connect and shows the query with every answer, so nothing is guessed or summarised from a sample.</p>
      </details>
      <details class="faq-item">
        <summary>Do I need to tag events first?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>No. The web SDK captures page views, clicks and form interactions automatically. You can add custom events later for anything specific to your product.</p>
      </details>
      <details class="faq-item">
        <summary>Is my data used to train models?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>No. Your data is only used to answer your team’s questions, and it never leaves the region you choose.</p>
      </details>
      <details class="faq-item">
        <summary>Can it change my site on its own?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>Never. Traffo drafts experiments and recommends fixes, but launching anything always takes a person saying yes.</p>
      </details>
      <details class="faq-item">
        <summary>What happens if I go over my event limit?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>Nothing breaks. We keep collecting and let you know, and you can upgrade or wait for the next cycle.</p>
      </details>
      <details class="faq-item">
        <summary>How long does setup take?<span class="faq-plus" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"><path d="M12 5v14M5 12h14"/></svg></span></summary>
        <p>Most teams paste one snippet and ask their first question within two minutes. Warehouse connections take about ten.</p>
      </details>
    </div>
  </div>
</section>

<section class="final-cta finale" id="start" data-section="cta">
  <span class="finale-grid" aria-hidden="true"></span>
  <span class="finale-glow" aria-hidden="true"></span>
  <div class="final-cta-card">
    <span class="finale-kicker"><i class="live-dot"></i>Free for your first 10,000 events</span>
    <h2 class="final-cta-h2">Stop guessing. <span class="accent"><span class="px-shadow"><span class="px">start asking</span></span></span></h2>
    <p>Connect your site in two minutes and ask your first question today. Traffo answers from your real events, with the query behind every number.</p>
    <form class="cta-form" id="ctaForm" novalidate>
      <label for="ctaEmail" class="sr-only">Work email</label>
      <input id="ctaEmail" type="email" placeholder="you@company.com" autocomplete="email" />
      <span class="btn-wrapper">
        <div class="line horizontal top" aria-hidden="true"></div>
        <div class="line vertical right" aria-hidden="true"></div>
        <div class="line horizontal bottom" aria-hidden="true"></div>
        <div class="line vertical left" aria-hidden="true"></div>
        <div class="dot top left" aria-hidden="true"></div>
        <div class="dot top right" aria-hidden="true"></div>
        <div class="dot bottom right" aria-hidden="true"></div>
        <div class="dot bottom left" aria-hidden="true"></div>
        <button class="btn" type="submit"><span class="btn-text">Start for free</span><svg class="btn-svg" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"></path></svg></button>
      </span>
    </form>
    <p class="cta-note" id="ctaNote" role="status">No credit card · Setup in 2 minutes · Cancel anytime</p>
  </div>

  <div class="finale-rule" aria-hidden="true"><i></i><span></span><i></i></div>

  <footer class="site-footer" data-section="footer">
    <div class="footer-top">
      <div class="footer-brand">
        <div class="f-logo">
          <span class="f-cube" aria-hidden="true"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 L13.5 10.5 L22 12 L13.5 13.5 L12 22 L10.5 13.5 L2 12 L10.5 10.5 Z" /></svg></span>
          TRAFFO<span class="logo-ai">AI</span>
        </div>
        <p>The AI analyst for teams who’d rather ship than spreadsheet.</p>
        <span class="f-status"><i class="live-dot"></i>All systems normal</span>
      </div>
      <div class="footer-cols">
        <div class="footer-col">
          <h4><span class="px">product</span></h4>
          <a href="#product">Assistant</a><a href="#product">Experiments</a>
          <a href="#pricing">Pricing</a><a href="#faq">FAQ</a>
        </div>
        <div class="footer-col">
          <h4><span class="px">company</span></h4>
          <a href="#quote">About</a><a href="#quote">Blog</a>
          <a href="#quote">Careers</a><a href="#start">Contact</a>
        </div>
        <div class="footer-col">
          <h4><span class="px">resources</span></h4>
          <a href="#">Changelog</a><a href="#">Docs</a>
          <a href="#">Status</a><a href="#customers">Customers</a>
        </div>
        <div class="footer-col">
          <h4><span class="px">legal</span></h4>
          <a href="#">Privacy</a><a href="#">Terms</a>
          <a href="#">Security</a><a href="#">GDPR</a>
        </div>
      </div>
    </div>
    <div class="footer-bottom">
      <span>© 2026 Traffo — a fictional product, for a template</span>
      <span class="f-badges"><span>SOC 2 Type II</span><span>GDPR ready</span><span>EU &amp; US hosting</span></span>
    </div>
    <div class="footer-mark" id="footerMark" aria-hidden="true"><span class="px">traffo</span></div>
  </footer>
</section>

<script>
/* Pixel type: turn each .px element's text into the shape() path it
   draws. Only runs where the browser supports shape(); elsewhere the
   text stays as ordinary text. */
(function () {
  var ok = window.CSS && CSS.supports && CSS.supports("clip-path", "shape(from 0 0, hline by 1px)");
  if (!ok) return;
  document.documentElement.classList.add("px-on");
  document.querySelectorAll(".px").forEach(function (el) {
    var text = el.textContent.toLowerCase(), parts = [], count = 0;
    for (var i = 0; i < text.length; i++) {
      var c = text[i];
      if (c >= "a" && c <= "z") { parts.push("var(--" + c + ")"); count += 1; }
      else { parts.push("var(--space)"); count += 0.5; }
    }
    el.style.setProperty("--letters", parts.join(","));
    el.style.setProperty("--count", count);
    el.setAttribute("aria-label", el.textContent);
  });
})();
</script>
<script>
(function () {
  "use strict";
  var log = document.getElementById("chatLog");
  var form = document.getElementById("chatForm");
  var input = document.getElementById("chatInput");
  var suggest = document.getElementById("chatSuggest");
  if (!log || !form) return;

  var REDUCED = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var SPARK = '<svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2 L13.5 10.5 L22 12 L13.5 13.5 L12 22 L10.5 13.5 L2 12 L10.5 10.5 Z" /></svg>';
  var busy = false, lastStamp = "";

  var SIGNUP_CHART =
    '<div class="mini-chart" role="img" aria-label="Signups over the last seven days: 412 on Monday, 398 on Tuesday, then 301, 296, 310, 288 and 305 after the Tuesday deploy.">' +
      '<div class="mini-chart-head"><span>Signups · last 7 days</span><b>−18%</b></div>' +
      '<div class="bars">' +
        [412, 398, 301, 296, 310, 288, 305].map(function (v, i) {
          return '<span class="bar' + (i > 1 ? " after" : "") + (i === 1 ? " deploy" : "") + '" style="--h:' + (v / 412 * 100).toFixed(1) + '%"></span>';
        }).join("") +
      '</div>' +
      '<div class="bar-days"><span>M</span><span>T</span><span>W</span><span>T</span><span>F</span><span>S</span><span>S</span></div>' +
    '</div>';

  var script = [
    { who: "ai", html: "Hi, I’m Traffo. Ask me anything about your traffic and I’ll answer from your real events." },
    { who: "you", text: "Why did signups drop last week?" },
    { who: "ai", html: "Signups fell <strong>18%</strong> after Tuesday’s deploy. 72% of the drop is mobile Safari: the email field on /signup stopped validating." + SIGNUP_CHART },
    { who: "you", text: "Can you fix it?" },
    { who: "ai", html: "I drafted a rollback test: 50/50 on mobile Safari, about <strong>3,200 visitors</strong> to reach 95% confidence. Say “launch” and it goes live." }
  ];

  var rules = [
    [/launch|go ahead|yes|ship/i, "Test is live. At current traffic it should reach 95% confidence by Thursday, and I’ll message you the moment it does."],
    [/funnel/i, "Mobile Safari this week: landing <strong>100%</strong> → pricing <strong>61%</strong> → signup form <strong>34%</strong> → confirmed <strong>9%</strong>. Form to confirmed was 22% before Tuesday, so that step is the leak."],
    [/bounce/i, "Bounce rate is <strong>41%</strong> this week, down 3 points. The worst page is /blog/pricing-guide at 78%, and it takes 4.1s to load on mobile."],
    [/revenue|money|mrr|sales|source/i, "Newsletter traffic converts best at <strong>6.2%</strong>, three times the site average. Paid social spend rose 20% but brought 4% fewer paying customers."],
    [/^(hi|hello|hey)\b/i, "Hey! Try asking why a page underperforms, or what changed since last week."]
  ];
  var fallback = [
    "Over the last 30 days, returning visitors converted at <strong>4.8%</strong> and first-time visitors at <strong>1.1%</strong>. Want me to break that down by channel?",
    "Your fastest-growing page is /pricing, up <strong>34%</strong> in visits this month. Most of that is from one comparison article linking to you.",
    "This is a demo workspace, so my answers here come from sample data. Connect your site and I’ll answer from yours."
  ];
  var f = 0;

  function reply(q) {
    for (var k = 0; k < rules.length; k++) if (rules[k][0].test(q)) return rules[k][1];
    return fallback[f++ % fallback.length];
  }

  function scrollDown() { log.scrollTop = log.scrollHeight; }

  function stamp() {
    var d = new Date();
    var t = d.getHours() + ":" + String(d.getMinutes()).padStart(2, "0");
    if (t === lastStamp) return "";
    lastStamp = t;
    return t;
  }

  function add(who, content, isHtml) {
    var row = document.createElement("div");
    row.className = "msg from-" + who + (REDUCED ? "" : " is-new");
    var wrap = document.createElement("div");
    wrap.className = "bubble-wrap";
    var b = document.createElement("div");
    b.className = "bubble";
    if (isHtml) b.innerHTML = content; else b.textContent = content;
    wrap.appendChild(b);
    var t = stamp();
    if (t) {
      var s = document.createElement("span");
      s.className = "stamp";
      s.textContent = (who === "ai" ? "Traffo · " : "You · ") + t;
      wrap.appendChild(s);
    }
    if (who === "ai") {
      var av = document.createElement("span");
      av.className = "chat-avatar";
      av.innerHTML = SPARK;
      row.appendChild(av);
    }
    row.appendChild(wrap);
    log.appendChild(row);
    scrollDown();
    return row;
  }

  function typing() {
    var row = document.createElement("div");
    row.className = "msg from-ai";
    row.innerHTML = '<span class="chat-avatar">' + SPARK + '</span><div class="bubble-wrap"><div class="bubble typing" aria-label="Traffo is typing"><i></i><i></i><i></i></div></div>';
    log.appendChild(row);
    scrollDown();
    return row;
  }

  function aiSays(html, then) {
    var t = typing();
    setTimeout(function () {
      t.remove();
      add("ai", html, true);
      if (then) then();
    }, 900 + Math.random() * 700);
  }

  function ask(text) {
    text = text.trim();
    if (!text || busy) return;
    busy = true;
    add("you", text, false);
    setTimeout(function () {
      aiSays(reply(text), function () { busy = false; });
    }, 350);
  }

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    var v = input.value;
    input.value = "";
    ask(v);
  });
  input.addEventListener("keydown", function (e) {
    if (e.key === "Enter" && !e.shiftKey) {
      e.preventDefault();
      form.requestSubmit ? form.requestSubmit() : form.dispatchEvent(new Event("submit", { cancelable: true }));
    }
  });
  suggest.addEventListener("click", function (e) {
    var chip = e.target.closest(".chip");
    if (chip) ask(chip.textContent);
  });

  function play(n) {
    if (n >= script.length) { busy = false; suggest.hidden = false; return; }
    var line = script[n];
    if (line.who === "ai") aiSays(line.html, function () { setTimeout(function () { play(n + 1); }, 700); });
    else { add("you", line.text, false); setTimeout(function () { play(n + 1); }, 450); }
  }
  busy = true;
  setTimeout(function () { play(0); }, REDUCED ? 0 : 1300);
})();
</script>

<script>
(function () {
  var btns = document.querySelectorAll(".billing button");
  btns.forEach(function (b) {
    b.addEventListener("click", function () {
      var mode = b.dataset.bill;
      btns.forEach(function (x) { x.setAttribute("aria-pressed", x === b ? "true" : "false"); });
      document.querySelectorAll(".amt[data-monthly]").forEach(function (el) { el.textContent = el.dataset[mode]; });
    });
  });
})();
</script>

<script>
/* Metrics instruments fill when they scroll in; CTA form; wordmark light. */
(function () {
  var metrics = document.querySelectorAll(".metric");
  var reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  if ("IntersectionObserver" in window && !reduced) {
    metrics.forEach(function (m) { m.classList.add("pre"); });
    var io = new IntersectionObserver(function (entries) {
      entries.forEach(function (e) {
        if (e.isIntersecting) { e.target.classList.remove("pre"); io.unobserve(e.target); }
      });
    }, { threshold: 0.35 });
    metrics.forEach(function (m) { io.observe(m); });
  }

  var form = document.getElementById("ctaForm"), note = document.getElementById("ctaNote");
  if (form) form.addEventListener("submit", function (e) {
    e.preventDefault();
    var v = document.getElementById("ctaEmail").value.trim();
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v)) { note.textContent = "Enter a work email to get started"; note.classList.remove("ok"); return; }
    note.textContent = "You're in. Check your inbox for the setup link.";
    note.classList.add("ok");
    form.reset();
  });

  var mark = document.getElementById("footerMark");
  if (mark && !reduced) {
    var px = mark.querySelector(".px");
    mark.parentElement.addEventListener("pointermove", function (e) {
      var r = px.getBoundingClientRect();
      px.style.setProperty("--mx", ((e.clientX - r.left) / r.width * 100).toFixed(1) + "%");
      px.style.setProperty("--my", ((e.clientY - r.top) / r.height * 100).toFixed(1) + "%");
    });
  }
})();
</script>
<script>
/* Mobile menu: opens from the toggle's own position, locks the page,
   closes on a link, Escape, or growing back to desktop width. */
(function () {
  var btn = document.querySelector(".menu-btn");
  var menu = document.getElementById("mobileMenu");
  if (!btn || !menu) return;
  var root = document.documentElement, closeTimer;

  function setOrigin() {
    var r = btn.getBoundingClientRect();
    menu.style.setProperty("--ox", (r.left + r.width / 2) + "px");
    menu.style.setProperty("--oy", (r.top + r.height / 2) + "px");
  }
  function open() {
    clearTimeout(closeTimer);
    setOrigin();
    menu.hidden = false;
    menu.classList.remove("closing");
    void menu.offsetWidth;            // let the closed clip-path paint first
    root.classList.add("menu-open");
    btn.setAttribute("aria-expanded", "true");
    btn.setAttribute("aria-label", "Close menu");
    var first = menu.querySelector(".mm-list a");
    if (first) setTimeout(function () { first.focus({ preventScroll: true }); }, 300);
  }
  function close(returnFocus) {
    if (!root.classList.contains("menu-open")) return;
    setOrigin();
    menu.classList.add("closing");
    root.classList.remove("menu-open");
    btn.setAttribute("aria-expanded", "false");
    btn.setAttribute("aria-label", "Open menu");
    closeTimer = setTimeout(function () { menu.hidden = true; menu.classList.remove("closing"); }, 720);
    if (returnFocus) btn.focus();
  }
  btn.addEventListener("click", function () {
    root.classList.contains("menu-open") ? close(true) : open();
  });
  menu.addEventListener("click", function (e) {
    if (e.target.closest("a")) close(false);
  });
  document.addEventListener("keydown", function (e) {
    if (!root.classList.contains("menu-open")) return;
    if (e.key === "Escape") { close(true); return; }
    if (e.key === "Tab") {        // keep focus inside the bar's toggle + the menu
      var f = [btn].concat([].slice.call(menu.querySelectorAll("a")));
      var i = f.indexOf(document.activeElement);
      if (e.shiftKey && (i <= 0)) { e.preventDefault(); f[f.length - 1].focus(); }
      else if (!e.shiftKey && i === f.length - 1) { e.preventDefault(); f[0].focus(); }
    }
  });
  window.addEventListener("resize", function () {
    if (window.innerWidth > 1100) close(false);
  });
})();
</script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script>
(function () {
  "use strict";
  if (!window.gsap) return;
  gsap.registerPlugin(ScrollTrigger);

  var REDUCED = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var body = document.body;

  if (!REDUCED) {
    gsap.set(".title-inner", { yPercent: 110 });
    gsap.set([".hero-desc", ".site-header"], { opacity: 0 });
    gsap.set(".chat-stage", { opacity: 0, y: 40, scale: 0.97 });

    var tl = gsap.timeline({ defaults: { ease: "power3.out" } });
    tl.to(".site-header", { opacity: 1, duration: 0.8 }, 0)
      .to(".title-inner", { yPercent: 0, duration: 1.1, stagger: 0.08, ease: "power4.out" }, 0.2)
      .to(".hero-desc", { opacity: 1, y: 0, duration: 0.8 }, 0.9)
      .from(".hero-desc", { y: 20, duration: 0.8 }, 0.9)
      .to(".chat-stage", { opacity: 1, y: 0, scale: 1, duration: 1, ease: "power3.out", clearProps: "transform" }, 0.5)
      .from(".float-card", { opacity: 0, y: 30, scale: 0.9, duration: 0.9, stagger: 0.12, ease: "back.out(1.6)" }, 0.9)
      .from(".hero-ctas, .hero-trust, .hero-eyebrow", { opacity: 0, y: 16, duration: 0.7, stagger: 0.08 }, 0.8);
  }

  if (!REDUCED) {
    gsap.to(".chat-stage", {
      y: 70,
      scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: 1 }
    });
    gsap.to(".hero-left", {
      y: 60, opacity: 0.4,
      scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: 1 }
    });
  }

  document.querySelectorAll(".stat-num").forEach(function (el) {
    var target = parseFloat(el.dataset.num);
    var decimals = parseInt(el.dataset.decimals || "0", 10);
    var prefix = el.dataset.prefix || "";
    var suffix = el.dataset.suffix || "";
    var render = function (value) {
      el.innerHTML = prefix + value.toFixed(decimals) +
        (suffix ? '<span class="accent">' + suffix + "</span>" : "");
    };
    if (REDUCED) { render(target); return; }
    ScrollTrigger.create({
      trigger: el,
      start: "top 85%",
      once: true,
      onEnter: function () {
        var counter = { val: 0 };
        render(0);
        gsap.to(counter, {
          val: target,
          duration: 2,
          ease: "power2.out",
          onUpdate: function () { render(counter.val); }
        });
      }
    });
  });

  var splitWords = function (selector) {
    document.querySelectorAll(selector).forEach(function (root) {
      var walker = document.createTreeWalker(root, NodeFilter.SHOW_TEXT);
      var nodes = [];
      while (walker.nextNode()) nodes.push(walker.currentNode);
      nodes.forEach(function (node) {
        if (!node.nodeValue.trim() || node.parentNode.closest(".px")) return;
        var frag = document.createDocumentFragment();
        node.nodeValue.split(/(\s+)/).forEach(function (chunk) {
          if (!chunk.trim()) return frag.appendChild(document.createTextNode(chunk));
          var mask = document.createElement("span");
          mask.className = "sword";
          mask.style.cssText = "display:inline-block;overflow:hidden;padding-bottom:0.12em;vertical-align:top;";
          var word = document.createElement("span");
          word.className = "sword-inner";
          word.style.cssText = "display:inline-block;will-change:transform;";
          word.textContent = chunk;
          mask.appendChild(word);
          frag.appendChild(mask);
        });
        node.parentNode.replaceChild(frag, node);
      });
    });
  };

  if (!REDUCED) {
    [".features-title", ".quote-text", ".final-cta-h2", ".section-title"].forEach(function (selector) {
      splitWords(selector);
      gsap.fromTo(selector + " .sword-inner",
        { yPercent: 110 },
        {
          yPercent: 0,
          duration: 1,
          stagger: 0.04,
          ease: "power4.out",
          scrollTrigger: { trigger: selector, start: "top 80%", toggleActions: "play none none reverse" }
        });
    });

    gsap.from(".feature-card", {
      y: 80, opacity: 0, duration: 1, stagger: 0.15, ease: "power3.out",
      scrollTrigger: { trigger: ".feature-cards", start: "top 75%", toggleActions: "play none none reverse" }
    });
    gsap.from(".quote-mark", {
      scale: 0, rotation: -45, duration: 1.2, ease: "elastic.out(1, 0.6)",
      scrollTrigger: { trigger: ".quote-mark", start: "top 80%", toggleActions: "play none none reverse" }
    });

    [[".metric", ".metric-grid"], [".tile", ".bento"], [".voice", ".voice-grid"], [".plan", ".plans"], [".faq-item", ".faq-list"]].forEach(function (p) {
      gsap.from(p[0], {
        y: 50, opacity: 0, duration: 0.9, stagger: 0.08, ease: "power3.out", clearProps: "transform,opacity",
        scrollTrigger: { trigger: p[1], start: "top 80%" }
      });
    });
    gsap.from(".funnel-bar i", {
      scaleX: 0, duration: 1.2, stagger: 0.12, ease: "power3.out",
      scrollTrigger: { trigger: ".funnel", start: "top 85%" }
    });
    gsap.from(".meter-track i", {
      width: 0, duration: 1.6, ease: "power3.out",
      scrollTrigger: { trigger: ".meter", start: "top 90%" }
    });
    gsap.from(".final-cta-card", {
      y: 40, opacity: 0, duration: 1.2, ease: "power3.out",
      scrollTrigger: { trigger: ".final-cta-card", start: "top 80%", toggleActions: "play none none reverse" }
    });
  }

  if (!REDUCED && !window.matchMedia("(pointer: coarse)").matches) {
    document.querySelectorAll(".feature-card").forEach(function (card) {
      card.addEventListener("pointermove", function (e) {
        var r = card.getBoundingClientRect();
        gsap.to(card, {
          rotationY: ((e.clientX - r.left) / r.width - 0.5) * 8,
          rotationX: -((e.clientY - r.top) / r.height - 0.5) * 8,
          y: -12,
          duration: 0.5,
          transformPerspective: 1200,
          ease: "power2.out"
        });
      });
      card.addEventListener("pointerleave", function () {
        gsap.to(card, { rotationY: 0, rotationX: 0, y: 0, duration: 0.8, ease: "elastic.out(1, 0.5)" });
      });
    });
  }

  window.addEventListener("load", function () { ScrollTrigger.refresh(); });
})();
</script>
</body>
</html>
```

