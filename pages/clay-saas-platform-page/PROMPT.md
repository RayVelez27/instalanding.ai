INSTALANDING.AI · Clay SaaS Platform Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Clay SaaS Platform Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/clay-saas-platform-page

dermexcel-clay-hero.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Clay SaaS Platform Page
  slug     clay-saas-platform-page
  prompt   https://instalanding.ai/p/clay-saas-platform-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/clay-saas-platform-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of the second <style>: --greyLight-1 (the one page colour),
            --greyLight-2, --white, --primary / --primary-light / --primary-dark, --text-dark, --shadow /
            --shadow-inset / --shadow-lg (soft-UI pair); html font-size 62.5% so 1rem = 10px; Funnel Display +
            JetBrains Mono from Google Fonts; dark/dim themes are body:has(input[value=dark|dim]:checked) overrides
  sections  nav, menu, hero, platform, modules, how-it-works, pipelines, testimonials, faq, footer
  scripts   no libraries. Head one-liner adds .mo to <html> unless reduced motion; one inline DOMContentLoaded
            script: split-letter generate button, theme switcher, .m morph shells, .rv reveals +
            stat counters via IntersectionObserver, floating pill + full-page menu, data-target scroll,
            module cards/toggles, pipeline tabs, FAQ accordion
  assets    one base64 WebP displacement map inlined in the #switcher SVG filter (theme switcher glass);
            everything else inline SVG / CSS

  ADAPTING
  - Soft UI only works when every raised or pressed surface is the same colour as the page: tint a card
    or band away from --greyLight-1 and the shadow pair reads as a drop shadow.
  - .rv/.m start hidden only under html.mo (set by the head one-liner) and the IntersectionObserver adds .is-in;
    if you drop or break the observer script, drop .mo too or those sections stay at opacity 0.
  - The generate button's letters are split from plain text in JS; keep the label as text, not spans.
  - The first <style> and the <title> inside <body> are a host wrapper, not page styles.
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Dermexcel</title>
<script>if(!window.matchMedia("(prefers-reduced-motion: reduce)").matches)document.documentElement.classList.add("mo");</script>
<meta name="description" content="Dermexcel, a fictional AI agent platform with a skincare-inspired routine: brief, run and review agents from one control plane." />

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Funnel+Display:wght@300..800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">

<style>
:root {
  /* ============================================================
     SOFT UI
     One light source at the top left, and every raised or pressed
     surface is the SAME colour as the page. That rule is the whole
     effect: tint a card away from its background and the pair of
     shadows stops reading as relief and becomes a drop shadow.
     ============================================================ */
  --greyLight-1: #e4ebf5;
  --greyLight-2: #c8d0e7;
  --greyLight-3: #bec8e4;
  --greyDark: #9baacf;
  --white: #ffffff;

  --primary-light: #8abdff;
  --primary: #6d5dfc;
  --primary-dark: #5b0eeb;

  /* the page is one flat colour — soft UI cannot sit on a gradient or on
     alternating section bands, because the surfaces would stop matching */
  --bg-top: var(--greyLight-1);
  --bg-bottom: var(--greyLight-1);
  --text-dark: #2c3557;
  --text-muted: #8091bb;
  --accent-hue: 249deg;
  --accent-orange: var(--primary);
  --accent-soft: var(--primary-light);
  --clay-dark: #1b2138;
  --clay-light: var(--greyLight-1);
  --ink-panel: linear-gradient(180deg, #232a45, #171c2e);
  --mono: "JetBrains Mono", ui-monospace, SFMono-Regular, Menlo, monospace;

  /* the two directions, and there are only two */
  --shadow: 0.3rem 0.3rem 0.6rem var(--greyLight-2),
    -0.2rem -0.2rem 0.5rem var(--white);
  --shadow-inset: inset 0.2rem 0.2rem 0.5rem var(--greyLight-2),
    inset -0.2rem -0.2rem 0.5rem var(--white);
  --shadow-lg: 0.8rem 0.8rem 1.4rem var(--greyLight-2),
    -0.2rem -0.2rem 1.8rem var(--white);

  /* the old names kept so every existing rule still resolves */
  --shadow-light: var(--shadow);
  --shadow-glass: var(--shadow);
  --shadow-dark: 0.5rem 0.5rem 1rem rgba(24, 30, 52, 0.45),
    -0.2rem -0.2rem 0.6rem rgba(255, 255, 255, 0.55);
  --shadow-orange: inset 0.2rem 0.2rem 1rem var(--primary-light),
    inset -0.2rem -0.2rem 1rem var(--primary-dark),
    0.3rem 0.3rem 0.6rem var(--greyLight-2),
    -0.2rem -0.2rem 0.5rem var(--white);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Funnel Display", system-ui, sans-serif;
}
/* the kit is written in rem at 1rem = 10px */
html { font-size: 62.5%; }
@media screen and (min-width: 900px) { html { font-size: 68.75%; } }
body { font-size: 1.6rem; }

body {
  background-color: var(--bg-top);
  color: var(--text-dark);
  overflow-x: hidden;
  min-height: 150vh;
}

/* --- Header --- */
header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 24px 48px;
  z-index: 100;
  mix-blend-mode: exclusion;
  color: white;
  transition: all 0.3s ease;
}

.logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 22px;
  font-weight: 600;
  letter-spacing: -0.5px;
}

.logo svg {
  width: 24px;
  height: 24px;
  fill: currentColor;
}

.nav-center {
  display: flex;
  gap: 32px;
  list-style: none;
  font-size: 13px;
  font-weight: 500;
}

.nav-center li {
  cursor: pointer;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.nav-center li.active::after {
  content: "•";
  font-size: 10px;
  line-height: 0.5;
  margin-top: 4px;
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 24px;
  font-size: 11px;
  font-weight: 500;
  line-height: 1.4;
  text-align: right;
}

.menu-btn {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
  backdrop-filter: blur(4px);
  font-size: 12px;
}

/* --- Hero Section --- */
.hero {
  position: relative;
  height: 100vh;
  width: 100vw;
  display: flex;
  align-items: center;
  padding: 0 48px;
  overflow: hidden;
}

/* Giant Background Text */
.bg-text {
  position: absolute;
  bottom: 15vh;
  left: 50%;
  transform: translateX(-50%);
  font-size: 26vw;
  font-weight: 800;
  color: rgba(255, 255, 255, 0.6);
  line-height: 0.8;
  white-space: nowrap;
  z-index: 1;
  letter-spacing: -2vw;
  background: linear-gradient(
    180deg,
    rgba(255, 255, 255, 0.9) 0%,
    rgba(255, 255, 255, 0) 100%
  );
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  pointer-events: none;
}

/* Main Image Overlay */
.hero-main-img {
  position: absolute;
  bottom: 5vh;
  left: 50%;
  transform: translateX(-50%);
  height: 80vh;
  max-width: 80vw;
  z-index: 5;
  object-fit: contain;
  object-position: bottom;
  /* Drop shadow for 3D depth over the background text */
  filter: drop-shadow(0 30px 40px rgba(0, 0, 0, 0.15));
}

/* Hero Content Left */
.hero-left {
  position: relative;
  z-index: 10;
  max-width: 480px;
}

.label {
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 24px;
  display: block;
  color: var(--text-dark);
}

/* ============================================================
   BLOCK HEADINGS
   Press Start 2P is a fixed-width pixel face: every glyph is a full
   em wide against Inter's ~0.5, so the same px size renders about
   twice as wide. Each level is resized for its own measure rather
   than inheriting the old scale, and the tight tracking from the
   source is what keeps the blocks reading as one mass.
   ============================================================ */
/* The reset sets Inter on * , which matches a heading's own child spans
   directly and beats inheritance — so the spans have to be named too or
   half of every headline drops back to the body face. */
h1, h2, h3, .section-title, .plan-title,
h1 span, h2 span, h3 span, .section-title span, .plan-title span {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 600;
  letter-spacing: -0.035em;
}
.hero h1 {
  /* 25% up from clamp(15px, 2vw, 28px). The margin carries the space the
     status row used to hold, so the buttons do not ride up under the type. */
  font-size: clamp(19px, 2.5vw, 35px);
  line-height: 1.32;
  margin-bottom: 44px;
}
.hero h1 span {
  color: var(--text-muted);
}

.reviews {
  display: flex;
  align-items: center;
  gap: 12px;
  font-size: 13px;
  font-weight: 500;
  margin-bottom: 48px;
}
.stars {
  color: #f59e0b;
  letter-spacing: 2px;
  font-size: 14px;
}

.hero-actions {
  display: flex;
  gap: 16px;
}

/* ── Primary button ─────────────────────────────────────────────────────
   Adapted from the Uiverse button by dexter-st. Kept intact: the stacked
   inset highlights that make the face read as lit glass, the ::before plate
   that carries the glow, the ::after sheen, and the letter-by-letter flicker.
   Wired to the page: --button-color is the clay dark, --highlight-color-hue
   is the page accent hue, so the button is the source of the accent rather
   than a guest on the page.

   The wrapper isolates: ::before lives at z-index -1 and without a stacking
   context of its own it would slip behind whatever card the button sits on.
   ──────────────────────────────────────────────────────────────────────── */
.btn-wrapper {
  position: relative;
  display: inline-block;
  isolation: isolate;
}

.btn {
  --border-radius: 24px;
  --padding: 4px;
  --transition: 0.4s;
  --button-color: var(--primary);
  --highlight-color-hue: var(--accent-hue);

  user-select: none;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5em 0.5em 0.5em 1.1em;
  font-family: "Funnel Display", system-ui, sans-serif;
  font-size: 0.95em;
  font-weight: 400;
  color: var(--greyLight-1);

  background-color: var(--button-color);

  /* lit from inside with its own hue, resting on the page's shadow pair */
  box-shadow: var(--shadow-orange);

  border: 0;
  border-radius: var(--border-radius);
  cursor: pointer;

  transition:
    box-shadow var(--transition),
    border var(--transition),
    background-color var(--transition);
}
.btn::before {
  content: "";
  position: absolute;
  top: calc(0px - var(--padding));
  left: calc(0px - var(--padding));
  width: calc(100% + var(--padding) * 2);
  height: calc(100% + var(--padding) * 2);
  border-radius: calc(var(--border-radius) + var(--padding));
  pointer-events: none;
  background-image: linear-gradient(0deg, #0004, #000a);

  z-index: -1;
  transition:
    box-shadow var(--transition),
    filter var(--transition);
  box-shadow:
    0 -8px 8px -6px #0000 inset,
    0 -16px 16px -8px #00000000 inset,
    1px 1px 1px #fff2,
    2px 2px 2px #fff1,
    -1px -1px 1px #0002,
    -2px -2px 2px #0001;
}
.btn::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border-radius: inherit;
  pointer-events: none;
  background-image: linear-gradient(
    0deg,
    #fff,
    hsl(var(--highlight-color-hue), 100%, 70%),
    hsla(var(--highlight-color-hue), 100%, 70%, 50%),
    8%,
    transparent
  );
  background-position: 0 0;
  opacity: 0;
  transition:
    opacity var(--transition),
    filter var(--transition);
}

.btn-letter {
  position: relative;
  display: inline-block;
  color: #fff5;
  animation: letter-anim 2s ease-in-out infinite;
  transition:
    color var(--transition),
    text-shadow var(--transition),
    opacity var(--transition);
}
@keyframes letter-anim {
  50% {
    text-shadow: 0 0 3px #fff8;
    color: #fff;
  }
}

.btn-svg {
  flex-grow: 1;
  height: 22px;
  width: 22px;
  margin-right: 0.5rem;
  fill: #e8e8e8;
  animation: flicker 2s linear infinite;
  animation-delay: 0.5s;
  filter: drop-shadow(0 0 2px #fff9);
  transition:
    fill var(--transition),
    filter var(--transition),
    opacity var(--transition);
}
@keyframes flicker {
  50% { opacity: 0.3; }
}

/* The label swaps to its busy twin while the button holds focus, which on a
   click is exactly as long as the thing it kicked off is the user's subject. */
.txt-wrapper {
  position: relative;
  display: flex;
  align-items: center;
  min-width: var(--label-width, 6.4em);
  height: 1.5em;
}
.txt-1,
.txt-2 {
  position: absolute;
  white-space: nowrap;
}
.txt-1 { animation: appear-anim 1s ease-in-out forwards; }
.txt-2 { opacity: 0; }
@keyframes appear-anim {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
.btn:focus .txt-1,
.btn.is-busy .txt-1 {
  animation: opacity-anim 0.3s ease-in-out forwards;
  animation-delay: 1s;
}
.btn:focus .txt-2,
.btn.is-busy .txt-2 {
  animation: opacity-anim 0.3s ease-in-out reverse forwards;
  animation-delay: 1s;
}
@keyframes opacity-anim {
  0% { opacity: 1; }
  100% { opacity: 0; }
}

.btn:focus .btn-letter,
.btn.is-busy .btn-letter {
  animation:
    focused-letter-anim 1s ease-in-out forwards,
    letter-anim 1.2s ease-in-out infinite;
  animation-delay: 0s, 1s;
}
@keyframes focused-letter-anim {
  0%,
  100% { filter: blur(0px); }
  50% {
    transform: scale(2);
    filter: blur(10px) brightness(150%)
      drop-shadow(-36px 12px 12px hsl(var(--highlight-color-hue), 100%, 70%));
  }
}
.btn:focus .btn-svg,
.btn.is-busy .btn-svg {
  animation-duration: 1.2s;
  animation-delay: 0.2s;
}

.btn:focus::before,
.btn.is-busy::before {
  box-shadow:
    0 -8px 12px -6px #fff3 inset,
    0 -16px 16px -8px hsla(var(--highlight-color-hue), 100%, 70%, 20%) inset,
    1px 1px 1px #fff3,
    2px 2px 2px #fff1,
    -1px -1px 1px #0002,
    -2px -2px 2px #0001;
}
.btn:focus::after,
.btn.is-busy::after {
  opacity: 0.6;
  mask-image: linear-gradient(0deg, #fff, transparent);
  filter: brightness(100%);
}

/* Letter flicker runs as a wave, one step per letter. */
.btn-letter:nth-child(1) { animation-delay: 0s; }
.btn-letter:nth-child(2) { animation-delay: 0.08s; }
.btn-letter:nth-child(3) { animation-delay: 0.16s; }
.btn-letter:nth-child(4) { animation-delay: 0.24s; }
.btn-letter:nth-child(5) { animation-delay: 0.32s; }
.btn-letter:nth-child(6) { animation-delay: 0.4s; }
.btn-letter:nth-child(7) { animation-delay: 0.48s; }
.btn-letter:nth-child(8) { animation-delay: 0.56s; }
.btn-letter:nth-child(9) { animation-delay: 0.64s; }
.btn-letter:nth-child(10) { animation-delay: 0.72s; }
.btn-letter:nth-child(11) { animation-delay: 0.8s; }
.btn-letter:nth-child(12) { animation-delay: 0.88s; }
.btn-letter:nth-child(13) { animation-delay: 0.96s; }

.btn:active {
  border: solid 1px hsla(var(--highlight-color-hue), 100%, 80%, 70%);
  background-color: hsla(var(--highlight-color-hue), 50%, 20%, 0.5);
}
.btn:active::before {
  box-shadow:
    0 -8px 12px -6px #fffa inset,
    0 -16px 16px -8px hsla(var(--highlight-color-hue), 100%, 70%, 80%) inset,
    1px 1px 1px #fff4,
    2px 2px 2px #fff2,
    -1px -1px 1px #0002,
    -2px -2px 2px #0001;
}
.btn:active::after {
  opacity: 1;
  mask-image: linear-gradient(0deg, #fff, transparent);
  filter: brightness(200%);
}
.btn:active .btn-letter {
  text-shadow: 0 0 1px hsla(var(--highlight-color-hue), 100%, 90%, 90%);
  animation: none;
}

.btn:hover {
  border: solid 1px hsla(var(--highlight-color-hue), 100%, 80%, 40%);
}
.btn:hover::before {
  box-shadow:
    0 -8px 8px -6px #fffa inset,
    0 -16px 16px -8px hsla(var(--highlight-color-hue), 100%, 70%, 30%) inset,
    1px 1px 1px #fff2,
    2px 2px 2px #fff1,
    -1px -1px 1px #0002,
    -2px -2px 2px #0001;
}
.btn:hover::after {
  opacity: 1;
  mask-image: linear-gradient(0deg, #fff, transparent);
}
.btn:hover .btn-svg {
  fill: #fff;
  filter: drop-shadow(0 0 3px hsl(var(--highlight-color-hue), 100%, 70%))
    drop-shadow(0 -4px 6px #0009);
  animation: none;
}

/* A quieter twin for secondary actions: same geometry, clay instead of glass. */
.btn-glass {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 0.72em 1.2em;
  border-radius: 24px;
  background: var(--greyLight-1);
  border: 1px solid rgba(255, 255, 255, 0.75);
  font-family: var(--mono);
  font-size: 12px;
  letter-spacing: 0.02em;
  color: var(--text-dark);
  cursor: pointer;
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow-glass), var(--shadow-light);
  transition: transform 0.2s, border-color 0.4s, background 0.4s;
}
.btn-glass:hover {
  background: var(--greyLight-1);
  border-color: hsla(var(--accent-hue), 90%, 60%, 0.45);
}
.btn-glass:active { transform: scale(0.97); }

/* Hero Content Right */
.hero-right {
  position: absolute;
  top: 20%;
  right: 48px;
  z-index: 10;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 60px;
}

.clay-widget {
  background: var(--greyLight-1);
  backdrop-filter: blur(20px);
  border-radius: 24px;
  padding: 16px;
  display: flex;
  align-items: center;
  gap: 24px;
  box-shadow: var(--shadow-glass), var(--shadow-light);
  border: 0;
  width: 340px;
}

.widget-img {
  width: 100px;
  height: 100px;
  background: var(--clay-dark);
  border-radius: 16px;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: var(--shadow-dark);
}
.widget-img svg {
  width: 32px;
  height: 32px;
  fill: white;
}

.widget-info {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 90px;
}

.w-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
.w-title {
  font-size: 16px;
  font-weight: 500;
  line-height: 1.2;
}
.w-dot {
  width: 6px;
  height: 6px;
  border: 1px solid var(--text-dark);
  border-radius: 50%;
}

.w-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.w-line {
  height: 2px;
  background: rgba(0, 0, 0, 0.1);
  width: 40px;
  border-radius: 2px;
  position: relative;
}
.w-line::after {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  height: 100%;
  width: 50%;
  background: var(--text-dark);
  border-radius: 2px;
}
.w-controls {
  display: flex;
  gap: 6px;
}
.w-ctrl {
  width: 24px;
  height: 24px;
  background: rgba(0, 0, 0, 0.05);
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 12px;
  cursor: pointer;
}

.partners {
  text-align: right;
  opacity: 0.6;
  max-width: 280px;
}
.p-label {
  font-size: 11px;
  font-weight: 600;
  margin-bottom: 12px;
}
.p-logos {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: flex-end;
  font-size: 12px;
  font-weight: 500;
}

/* Hero Footer Bar */
.hero-footer {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 70px;
  background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 48px;
  color: rgba(255, 255, 255, 0.7);
  font-size: 12px;
  font-weight: 500;
  z-index: 15;
  padding-bottom: 10px;
}

/* --- Section 2: White Area --- */
.bottom-section {
  background-color: var(--bg-bottom);
  border-top-left-radius: 40px;
  border-top-right-radius: 40px;
  position: relative;
  z-index: 20;
  padding: 80px 48px;
  margin-top: -30px; /* Overlap hero */
  box-shadow: 0 -20px 40px rgba(0, 0, 0, 0.05);
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
}

/* Wireframe Globe Background */
.wireframe-globe {
  position: absolute;
  top: 0;
  left: -15vw;
  width: 800px;
  height: 800px;
  opacity: 0.03;
  pointer-events: none;
  z-index: 0;
  background-image: radial-gradient(
      circle,
      transparent 40%,
      #000 41%,
      transparent 42%
    ),
    linear-gradient(0deg, transparent 49%, #000 50%, transparent 51%),
    linear-gradient(90deg, transparent 49%, #000 50%, transparent 51%);
  background-size: 100% 100%, 50px 50px, 50px 50px;
  border-radius: 50%;
  transform: perspective(600px) rotateX(60deg) translateY(-20%);
}

.s2-content {
  display: flex;
  justify-content: space-between;
  width: 100%;
  max-width: 1200px;
  position: relative;
  z-index: 10;
}

.s2-left {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 80px;
}
.about-label {
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 13px;
  font-weight: 600;
}
.about-label .dot {
  width: 6px;
  height: 6px;
  background: var(--text-dark);
  border-radius: 50%;
}

.hub-info {
  display: flex;
  align-items: center;
  gap: 16px;
  font-size: 12px;
  font-weight: 500;
  color: var(--text-muted);
  max-width: 220px;
  line-height: 1.4;
}
.hub-info svg {
  width: 32px;
  height: 32px;
  stroke: currentColor;
  fill: none;
  stroke-width: 1.5;
}

.s2-right {
  flex: 1.2;
  display: flex;
  flex-direction: column;
  gap: 60px;
}

.s2-right h2 {
  font-size: clamp(13px, 1.6vw, 18px);
  font-weight: 400;
  line-height: 1.3;
  letter-spacing: -1px;
}
.s2-right h2 span {
  color: var(--text-muted);
}

.social-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.s-icons {
  display: flex;
  gap: 12px;
  align-items: center;
}
.s-label {
  font-size: 12px;
  color: var(--text-muted);
  margin-right: 16px;
}
.s-icon {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  background: var(--bg-top);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 12px;
  cursor: pointer;
  transition: transform 0.2s;
}
.s-icon:hover {
  transform: scale(1.1);
}
.s-icon.orange {
  background: var(--accent-orange);
  color: white;
}

.about-btn {
  font-size: 13px;
  font-weight: 600;
  display: flex;
  align-items: center;
  gap: 8px;
  cursor: pointer;
}

/* --- Giant Clay Pills --- */
.pill-container {
  display: flex;
  justify-content: center;
  gap: 24px;
  margin-top: 100px;
  position: relative;
  z-index: 10;
  width: 100%;
  max-width: 1000px;
  flex-wrap: wrap;
}

.giant-pill {
  flex: 1;
  min-width: 180px;
  height: 120px;
  border-radius: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 28px;
  font-weight: 400;
  cursor: pointer;
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
  border: 2px solid transparent;
}

.giant-pill:hover {
  transform: translateY(-8px) scale(1.02);
}

.pill-white {
  background: var(--bg-bottom);
  box-shadow: var(--shadow-light);
  border-color: rgba(255, 255, 255, 0.8);
  color: var(--text-dark);
}

.pill-orange {
  background: var(--accent-orange);
  box-shadow: var(--shadow-orange);
  color: white;
  border-color: rgba(255, 255, 255, 0.2);
}

.pill-black {
  background: var(--clay-dark);
  box-shadow: var(--shadow-dark);
  color: white;
  border-color: rgba(255, 255, 255, 0.1);
}
.pill-black svg {
  width: 48px;
  height: 48px;
  stroke: white;
  stroke-width: 2;
  fill: none;
}

.pill-gray {
  background: var(--clay-light);
  box-shadow: inset 4px 4px 10px rgba(0, 0, 0, 0.05),
    inset -4px -4px 10px rgba(255, 255, 255, 0.6);
  color: #b0b0b0;
  border-color: rgba(255, 255, 255, 0.5);
}

/* =========================================================
   Extended sections: reuse the tokens, clay shadows and type
   scale above. Nothing new but layout.
   ========================================================= */

.section {
  position: relative;
  padding: 120px 48px;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  overflow: clip; /* clip, not hidden, so position: sticky still works inside */
}
.section--gray { background: var(--bg-top); }
.section--white { background: var(--bg-bottom); }

.section-inner {
  position: relative;
  z-index: 2;
  width: 100%;
  max-width: 1200px;
}

.section-head {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 48px;
  margin-bottom: 64px;
}
.section-head .about-label { margin-bottom: 24px; }

.section-title {
  font-size: clamp(13px, 1.5vw, 20px);
  line-height: 1.5;
  max-width: 680px;
}
.section-title span { color: var(--text-muted); }

.section-sub {
  max-width: 340px;
  font-size: 14px;
  line-height: 1.6;
  color: var(--text-muted);
}

.about-label--light { color: #fff; }
.about-label--light .dot { background: var(--accent-orange); }

/* --- Periodic element tiles: every capability gets a two-letter symbol --- */
.el {
  position: relative;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  border-radius: 10px;
  border: 1px solid rgba(0, 0, 0, 0.14);
  background: var(--greyLight-1);
  font-size: 12px;
  font-weight: 600;
  letter-spacing: -0.3px;
  flex-shrink: 0;
}
.el::before {
  content: attr(data-n);
  position: absolute;
  top: 3px;
  left: 4px;
  font-size: 7px;
  font-weight: 500;
  opacity: 0.55;
}

/* --- Ingredient marquee --- */
.ingredient-band {
  position: relative;
  z-index: 20;
  background: var(--bg-bottom);
  padding: 0 0 100px;
}
.marquee {
  display: flex;
  gap: 16px;
  overflow: hidden;
  padding: 24px 0;
  -webkit-mask-image: linear-gradient(90deg, transparent, #000 8%, #000 92%, transparent);
  mask-image: linear-gradient(90deg, transparent, #000 8%, #000 92%, transparent);
}
.marquee-track {
  display: flex;
  gap: 16px;
  flex-shrink: 0;
  min-width: 100%;
  justify-content: space-around;
  animation: marquee 45s linear infinite;
}
.marquee:hover .marquee-track { animation-play-state: paused; }
@keyframes marquee {
  to { transform: translateX(calc(-100% - 16px)); }
}

.chip {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  padding: 8px 22px 8px 8px;
  border-radius: 40px;
  background: var(--bg-bottom);
  border: 1px solid rgba(0, 0, 0, 0.04);
  box-shadow: var(--shadow-light);
  font-size: 14px;
  font-weight: 500;
  white-space: nowrap;
}
.chip--orange { background: var(--accent-orange); color: #fff; box-shadow: var(--shadow-orange); }
.chip--dark { background: var(--clay-dark); color: #fff; box-shadow: var(--shadow-dark); }
.chip--orange .el,
.chip--dark .el { border-color: rgba(255, 255, 255, 0.3); background: rgba(255, 255, 255, 0.08); }

/* --- Products --- */
.product-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}
.product-card {
  display: flex;
  flex-direction: column;
  gap: 20px;
  padding: 14px 14px 22px;
  border-radius: 32px;
  background: var(--clay-light);
  border: 0;
  box-shadow: var(--shadow-light);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.product-card:hover { transform: translateY(-8px); }

.product-stage {
  position: relative;
  height: 260px;
  border-radius: 24px;
  background: linear-gradient(180deg, #fafbfc 0%, #e4e6e9 100%);
  box-shadow: inset 4px 4px 10px rgba(0, 0, 0, 0.05),
    inset -4px -4px 10px rgba(255, 255, 255, 0.7);
  display: flex;
  align-items: flex-end;
  justify-content: center;
  overflow: hidden;
}
.product-badge {
  position: absolute;
  top: 14px;
  left: 14px;
  z-index: 2;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 11px;
  font-weight: 600;
  background: var(--greyLight-1);
  border: 0;
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow-glass);
}
.product-badge--orange {
  background: var(--accent-orange);
  color: #fff;
  border-color: transparent;
  box-shadow: var(--shadow-orange);
}

/* CSS-drawn module slabs, same matte black as the hero console */
.mod-tilt { transform: rotate(var(--tilt, 0deg)); }
.mod {
  width: 138px;
  padding: 14px 12px 12px;
  border-radius: 18px;
  background: var(--ink-panel);
  box-shadow: var(--shadow-dark);
  color: #e8eef7;
  display: grid;
  gap: 10px;
}
.mod-rail {
  height: 5px;
  border-radius: 3px;
  background: linear-gradient(90deg, var(--accent-orange), transparent);
  opacity: 0.9;
}
.mod-name {
  font-family: var(--mono);
  font-size: 10px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #8fa6c4;
}
.mod-face {
  border: 1px solid #1d2532;
  border-radius: 12px;
  background: #0c1016;
  padding: 10px;
  display: grid;
  gap: 7px;
}
.mod-bar {
  height: 6px;
  border-radius: 3px;
  background: #1b2330;
  overflow: hidden;
}
.mod-bar i {
  display: block;
  height: 100%;
  width: var(--w, 60%);
  border-radius: 3px;
  background: linear-gradient(90deg, var(--accent-orange), var(--accent-soft));
}
.mod-pins { display: flex; gap: 4px; }
.mod-pins i {
  width: 6px;
  height: 12px;
  border-radius: 2px;
  background: #222c3a;
}
.mod-pins i:nth-child(-n + 3) { background: var(--accent-orange); opacity: 0.8; }
.mod-mark { width: 18px; height: 18px; fill: rgba(255, 255, 255, 0.5); justify-self: end; }

.product-info { display: flex; flex-direction: column; gap: 16px; padding: 0 8px; }
.product-info h3 { font-size: 12px; font-weight: 500; letter-spacing: -0.5px; }
.product-for { display: block; margin-top: 4px; font-size: 12px; color: var(--text-muted); }
.el-row { display: flex; flex-wrap: wrap; gap: 6px; }
.product-foot {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 12px;
  color: var(--text-muted);
}

.round-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--clay-dark);
  color: #fff;
  font-size: 18px;
  font-weight: 300;
  box-shadow: var(--shadow-dark);
  transition: transform 0.2s, background 0.2s;
}
.round-btn:hover { transform: scale(1.08); }
.round-btn:active { transform: scale(0.94); }
.round-btn.added { background: var(--accent-orange); box-shadow: var(--shadow-orange); font-size: 14px; }

/* --- Formulation technology --- */
.wireframe-globe--right { left: auto; right: -20vw; top: 8%; }

.step-track {
  height: 2px;
  margin-bottom: 32px;
  border-radius: 2px;
  background: rgba(0, 0, 0, 0.08);
  overflow: hidden;
}
.step-track-fill {
  height: 100%;
  background: var(--accent-orange);
  transform-origin: left center;
}

.step-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}
.step-card {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 28px 24px 32px;
  border-radius: 28px;
  background: var(--bg-bottom);
  border: 1px solid rgba(0, 0, 0, 0.05);
  box-shadow: var(--shadow-light);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.step-card:hover { transform: translateY(-6px); }
.step-num {
  position: absolute;
  top: 24px;
  right: 24px;
  font-size: 13px;
  font-weight: 600;
  color: var(--text-muted);
}
.step-icon {
  width: 56px;
  height: 56px;
  margin-bottom: 12px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--clay-dark);
  box-shadow: var(--shadow-dark);
}
.step-icon--orange { background: var(--accent-orange); box-shadow: var(--shadow-orange); }
.step-icon svg {
  width: 24px;
  height: 24px;
  fill: none;
  stroke: #fff;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.step-card h3 { font-size: 13px; font-weight: 500; letter-spacing: -0.5px; }
.step-card p { font-size: 13px; line-height: 1.6; color: var(--text-muted); }

/* --- Stats panel (dark clay) --- */
.stats-panel {
  position: relative;
  margin-top: 96px;
  padding: 64px;
  border-radius: 40px;
  display: grid;
  grid-template-columns: 1.4fr repeat(4, 1fr);
  gap: 32px;
  align-items: end;
  background: var(--clay-dark);
  color: #fff;
  box-shadow: var(--shadow-dark);
}
.stats-panel::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: radial-gradient(circle at 100% 0%, hsla(var(--accent-hue), 92%, 52%, 0.32), transparent 50%);
  pointer-events: none;
}
.stats-intro { position: relative; display: flex; flex-direction: column; gap: 20px; }
.stats-intro p { max-width: 260px; font-size: 15px; line-height: 1.5; color: rgba(255, 255, 255, 0.6); }
.stat {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding-left: 20px;
  border-left: 1px solid rgba(255, 255, 255, 0.12);
}
.stat-num { font-size: clamp(36px, 4vw, 56px); font-weight: 500; letter-spacing: -2px; line-height: 1; }
.stat-label { font-size: 12px; line-height: 1.4; color: rgba(255, 255, 255, 0.55); }

/* --- Treatment plans --- */
.plan-tabs { display: flex; flex-wrap: wrap; gap: 12px; margin-bottom: 32px; }
.plan-tab {
  padding: 12px 24px;
  border-radius: 30px;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  color: var(--text-dark);
  background: rgba(255, 255, 255, 0.4);
  border: 1px solid rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(10px);
  box-shadow: var(--shadow-glass);
  transition: background 0.2s, color 0.2s, box-shadow 0.2s;
}
.plan-tab:hover { background: rgba(255, 255, 255, 0.7); }
.plan-tab.active {
  background: var(--clay-dark);
  color: #fff;
  border-color: transparent;
  box-shadow: var(--shadow-dark);
}
.plan-tab:focus-visible { outline: 2px solid var(--accent-orange); outline-offset: 3px; }

.plan-panel { display: grid; grid-template-columns: 1fr 1.2fr; gap: 24px; }
.plan-summary {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 40px;
  border-radius: 32px;
  background: var(--bg-bottom);
  border: 0;
  box-shadow: var(--shadow-light);
}
.plan-kicker { font-size: 12px; font-weight: 600; color: var(--accent-orange); }
.plan-title { font-size: clamp(32px, 3.5vw, 48px); font-weight: 500; letter-spacing: -2px; line-height: 1; }
.plan-desc { max-width: 420px; font-size: 15px; line-height: 1.6; color: var(--text-muted); }
.plan-focus { display: flex; flex-wrap: wrap; gap: 8px; margin-top: auto; padding-top: 16px; }
.plan-focus span {
  padding: 6px 14px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: 500;
  background: var(--bg-top);
}

.plan-pipe { display: flex; flex-direction: column; gap: 16px; }
.pipe-row {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 20px;
  padding: 20px 24px 20px 20px;
  border-radius: 28px;
  background: var(--clay-light);
  box-shadow: inset 4px 4px 10px rgba(0, 0, 0, 0.05),
    inset -4px -4px 10px rgba(255, 255, 255, 0.6);
}
.pipe-time {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
  font-weight: 600;
  background: var(--bg-bottom);
  box-shadow: var(--shadow-light);
}
.pipe-row--pm .pipe-time { background: var(--clay-dark); color: #fff; box-shadow: var(--shadow-dark); }
.pipe-row--review .pipe-time { background: var(--accent-orange); color: #fff; box-shadow: var(--shadow-orange); }
.pipe-product { display: block; font-size: 17px; font-weight: 500; letter-spacing: -0.3px; }
.pipe-note { display: block; margin-top: 4px; font-size: 13px; line-height: 1.5; color: var(--text-muted); }
.pipe-step { font-size: 12px; font-weight: 500; color: var(--text-muted); }
.plan-note { padding: 4px 8px; font-size: 12px; color: var(--text-muted); }

/* --- Reviews --- */
.review-summary {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  gap: 6px;
  font-size: 13px;
  font-weight: 500;
}
.review-summary .stars { font-size: 18px; }
.review-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
  align-items: start;
}
.review-card {
  display: flex;
  flex-direction: column;
  gap: 24px;
  padding: 32px;
  border-radius: 32px;
  background: var(--bg-bottom);
  border: 1px solid rgba(0, 0, 0, 0.05);
  box-shadow: var(--shadow-light);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.review-card:hover { transform: translateY(-6px); }
.review-card--dark {
  margin-top: 40px;
  background: var(--clay-dark);
  color: #fff;
  border-color: transparent;
  box-shadow: var(--shadow-dark);
}
.review-card blockquote { font-size: 17px; line-height: 1.5; letter-spacing: -0.3px; }
.review-card figcaption { display: flex; align-items: center; gap: 12px; }
.avatar {
  width: 44px;
  height: 44px;
  flex-shrink: 0;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 13px;
  font-weight: 600;
  background: var(--bg-top);
  box-shadow: var(--shadow-light);
}
.review-card--dark .avatar { background: var(--accent-orange); color: #fff; box-shadow: var(--shadow-orange); }
.review-card figcaption strong { display: block; font-size: 14px; font-weight: 600; }
.review-card figcaption em {
  display: block;
  margin-top: 2px;
  font-size: 12px;
  font-style: normal;
  color: var(--text-muted);
}
.review-card--dark figcaption em { color: rgba(255, 255, 255, 0.55); }

/* --- FAQ --- */
.faq-layout {
  display: grid;
  grid-template-columns: 1fr 1.4fr;
  gap: 64px;
  align-items: start;
}
.faq-intro {
  position: sticky;
  top: 120px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 24px;
}
.faq-intro .btn-wrapper { margin-top: 8px; }
.faq-list { display: flex; flex-direction: column; gap: 16px; }
.faq-item {
  border-radius: 28px;
  background: var(--bg-bottom);
  border: 0;
  box-shadow: var(--shadow-light);
}
.faq-q {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 24px;
  padding: 24px 24px 24px 32px;
  background: none;
  border: none;
  cursor: pointer;
  text-align: left;
  font-size: 17px;
  font-weight: 500;
  letter-spacing: -0.3px;
  color: var(--text-dark);
}
.faq-q:focus-visible { outline: 2px solid var(--accent-orange); outline-offset: -4px; border-radius: 28px; }
.faq-icon {
  position: relative;
  width: 36px;
  height: 36px;
  flex-shrink: 0;
  border-radius: 50%;
  background: var(--bg-top);
  transition: transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), background 0.2s, color 0.2s;
}
.faq-icon::before,
.faq-icon::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 12px;
  height: 1.5px;
  background: currentColor;
  transform: translate(-50%, -50%);
}
.faq-icon::after { transform: translate(-50%, -50%) rotate(90deg); }
.faq-item.open .faq-icon { transform: rotate(45deg); background: var(--clay-dark); color: #fff; }
/* 0fr -> 1fr animates to the answer's natural height without measuring it */
.faq-a { display: grid; grid-template-rows: 0fr; transition: grid-template-rows 0.4s ease; }
.faq-a > div { overflow: hidden; }
.faq-item.open .faq-a { grid-template-rows: 1fr; }
.faq-a p { max-width: 600px; padding: 0 32px 28px; font-size: 14px; line-height: 1.7; color: var(--text-muted); }

/* --- Consultation CTA --- */
.consult-card {
  position: relative;
  width: 100%;
  max-width: 1200px;
  display: grid;
  grid-template-columns: 1.1fr 1fr;
  gap: 64px;
  align-items: center;
  padding: 72px;
  border-radius: 40px;
  background: var(--clay-dark);
  color: #fff;
  box-shadow: var(--shadow-dark);
}
.consult-card::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: radial-gradient(circle at 100% 100%, hsla(var(--accent-hue), 92%, 52%, 0.45), transparent 55%);
  pointer-events: none;
}
.consult-copy { position: relative; display: flex; flex-direction: column; gap: 24px; }
.consult-copy h2 { font-size: clamp(14px, 1.8vw, 23px); font-weight: 500; line-height: 1.05; letter-spacing: -2px; }
.consult-copy h2 span { color: rgba(255, 255, 255, 0.5); }
.consult-copy p { max-width: 420px; font-size: 15px; line-height: 1.6; color: rgba(255, 255, 255, 0.6); }

.consult-form {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 28px;
  border-radius: 32px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(20px);
  box-shadow: inset 1px 1px 2px rgba(255, 255, 255, 0.1);
}
.field { display: flex; flex-direction: column; gap: 8px; font-size: 12px; font-weight: 500; color: rgba(255, 255, 255, 0.6); }
.field input,
.field select {
  width: 100%;
  padding: 16px 20px;
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.08);
  background-color: rgba(0, 0, 0, 0.35);
  color: #fff;
  font-size: 15px;
  outline: none;
  -webkit-appearance: none;
  appearance: none;
  box-shadow: inset 2px 2px 6px rgba(0, 0, 0, 0.5), inset -2px -2px 6px rgba(255, 255, 255, 0.04);
  transition: border-color 0.2s;
}
.field select {
  cursor: pointer;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='white' stroke-width='2'%3E%3Cpolyline points='6 9 12 15 18 9'/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: right 20px center;
}
.field select option { color: #111; }
.field input::placeholder { color: rgba(255, 255, 255, 0.35); }
.field input:focus,
.field select:focus { border-color: var(--accent-orange); }
.btn-orange {
  justify-content: center;
  margin-top: 8px;
  padding: 16px 24px;
  background: var(--accent-orange);
  box-shadow: var(--shadow-orange);
}
.btn-orange:disabled { cursor: default; }
.form-status { min-height: 18px; font-size: 13px; color: rgba(255, 255, 255, 0.7); }

/* --- Footer --- */
.site-footer {
  position: relative;
  z-index: 20;
  margin-top: -30px; /* overlap the section above, like the About panel does the hero */
  padding: 96px 48px 32px;
  background: var(--bg-top);
  border-top-left-radius: 40px;
  border-top-right-radius: 40px;
  box-shadow: 0 -20px 40px rgba(0, 0, 0, 0.05);
  overflow: hidden;
}
.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.6fr 1fr 1fr 1fr;
  gap: 48px;
}
.footer-brand { display: flex; flex-direction: column; gap: 20px; }
.footer-brand .s-icon { background: var(--bg-bottom); box-shadow: var(--shadow-light); }
.footer-brand .s-icon.orange { background: var(--accent-orange); box-shadow: var(--shadow-orange); }
.footer-brand p { max-width: 280px; font-size: 14px; line-height: 1.6; color: var(--text-muted); }
.footer-col { display: flex; flex-direction: column; gap: 12px; }
.footer-col h4 { margin-bottom: 8px; font-size: 12px; font-weight: 600; }
.footer-col a,
.footer-bottom a {
  width: fit-content;
  font-size: 14px;
  color: var(--text-muted);
  text-decoration: none;
  transition: color 0.2s;
}
.footer-col a:hover,
.footer-bottom a:hover { color: var(--text-dark); }
.footer-wordmark {
  margin: 72px -48px 0;
  text-align: center;
  font-size: 17vw;
  font-weight: 800;
  line-height: 0.8;
  letter-spacing: -1vw;
  white-space: nowrap;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.12) 0%, rgba(0, 0, 0, 0) 85%);
  -webkit-background-clip: text;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  user-select: none;
  pointer-events: none;
}
.footer-bottom {
  max-width: 1200px;
  margin: 24px auto 0;
  padding-top: 24px;
  border-top: 1px solid rgba(0, 0, 0, 0.08);
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 16px;
  font-size: 12px;
  color: var(--text-muted);
}
.footer-bottom a { font-size: 12px; }

/* ── Hero: two columns, copy against a drawn console ───────────────────── */
.hero-grid {
  position: relative;
  z-index: 10;
  width: 100%;
  max-width: 1320px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  gap: 56px;
  align-items: center;
}
/* 640, not 560: at the larger size "Ship skin analysis" no longer fits the
   old measure and wrapped, turning the authored three lines into four.
   640 + 56 gap + the console still clears the grid's 1320 cap. */
.hero-left { max-width: 640px; }
.hero-right {
  position: static;
  display: grid;
  gap: 20px;
  justify-items: stretch;
  align-items: start;
}
.hero h1 span.accent { color: var(--accent-orange); }
/* Press Start 2P is a full-width face: "Ship skin analysis" is 18 characters
   and at the new 19px floor it needs 342px, which fits a 390 phone exactly
   and runs off a 360 one. Below 420 the size tracks the viewport instead of
   sitting on the floor. 4.3vw lands within a pixel of 19px at the boundary,
   so there is no step. */

@media (max-width: 1100px) {
  .hero { height: auto; padding: 120px 24px 80px; }
  .hero-grid { grid-template-columns: minmax(0, 1fr); }
  .hero-left { max-width: none; }
}

/* ── Console: the hero's product shot, drawn rather than photographed ──── */
.console {
  position: relative;
  z-index: 5;
  width: min(560px, 42vw);
  padding: 18px;
  border-radius: 26px;
  background: var(--ink-panel);
  box-shadow: var(--shadow-dark), 0 40px 60px -30px rgba(10, 13, 18, 0.55);
  color: #e9eef5;
}
.console-head {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: var(--mono);
  font-size: 11px;
  color: #8fa6c4;
}
.console-dot { width: 8px; height: 8px; border-radius: 50%; background: #253041; }
.console-dot--live {
  background: var(--accent-orange);
  box-shadow: 0 0 10px hsla(var(--accent-hue), 92%, 60%, 0.9);
}
.console-head .spacer { margin-left: auto; opacity: 0.7; }
.code {
  margin-top: 14px;
  padding: 14px;
  border: 1px solid #1b2230;
  border-radius: 14px;
  background: #0b0f15;
  font-family: var(--mono);
  font-size: 12.5px;
  line-height: 1.75;
  white-space: pre;
  overflow-x: auto;
}
.code .k { color: #7aa2ff; }
.code .s { color: #7ee0a8; }
.code .c { color: #56657c; }
.console-out {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  margin-top: 12px;
}
.out-tile {
  padding: 10px 12px;
  border: 1px solid #1b2230;
  border-radius: 14px;
  background: #0f141c;
}
.out-k {
  font-family: var(--mono);
  font-size: 9px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: #6d829e;
}
.out-v { font-size: 17px; font-weight: 600; margin-top: 3px; }
.meter { height: 4px; border-radius: 2px; background: #1b2230; margin-top: 8px; overflow: hidden; }
.meter i {
  display: block;
  height: 100%;
  width: var(--w, 60%);
  background: linear-gradient(90deg, var(--accent-orange), var(--accent-soft));
}

/* ── Mono labels, metric chips ────────────────────────────── */
.mono { font-family: var(--mono); }
.quote-metric {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 5px 11px;
  border-radius: 20px;
  font-family: var(--mono);
  font-size: 11px;
  color: var(--accent-orange);
  background: hsla(var(--accent-hue), 92%, 52%, 0.1);
  border: 1px solid hsla(var(--accent-hue), 92%, 52%, 0.25);
}
.review-card--dark .quote-metric {
  color: #cfe0ff;
  background: rgba(255, 255, 255, 0.08);
  border-color: rgba(255, 255, 255, 0.18);
}


@media (max-width: 1100px) {
  .console { width: min(560px, 86vw); }
}
@media (max-width: 760px) {
  /* The version readout crowds the wordmark long before it is useful. */
  .nav-right > div { display: none; }
}

@media (max-width: 1024px) {
  .hero-bg-img {
    height: 60vh;
  }
  .bg-text {
    font-size: 20vw;
    bottom: 25vh;
  }
  .hero-right {
    position: relative;
    top: 0;
    right: 0;
    align-items: flex-start;
    margin-top: 40px;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .hero {
    flex-direction: column;
    align-items: flex-start;
    padding-top: 120px;
    height: auto;
    padding-bottom: 120px;
  }
  .s2-content {
    flex-direction: column;
    gap: 60px;
  }
  header {
    mix-blend-mode: normal;
    color: var(--text-dark);
    background: rgba(255, 255, 255, 0.9);
    backdrop-filter: blur(10px);
    padding: 16px 24px;
  }
  .menu-btn {
    color: var(--text-dark);
    border-color: #ccc;
  }
  .nav-center {
    display: none;
  } /* Hide nav on mobile for simplicity */
}

/* --- Extended sections: responsive --- */
@media (max-width: 1024px) {
  .section { padding: 88px 24px; }
  .section-head { flex-direction: column; align-items: flex-start; gap: 24px; margin-bottom: 48px; }
  .review-summary { align-items: flex-start; }
  .product-grid,
  .step-grid { grid-template-columns: repeat(2, 1fr); }
  .stats-panel { grid-template-columns: repeat(2, 1fr); margin-top: 72px; padding: 48px 40px; }
  .stats-intro { grid-column: 1 / -1; }
  .plan-panel { grid-template-columns: 1fr; }
  .review-grid { grid-template-columns: repeat(2, 1fr); }
  .review-card--dark { margin-top: 0; }
  .faq-layout { grid-template-columns: 1fr; gap: 40px; }
  .faq-intro { position: static; }
  .consult-card { grid-template-columns: 1fr; gap: 40px; padding: 48px 40px; }
  .ingredient-band { padding-bottom: 72px; }
  .site-footer { padding: 72px 24px 24px; }
  .footer-inner { grid-template-columns: repeat(3, 1fr); }
  .footer-brand { grid-column: 1 / -1; }
  .footer-wordmark { margin: 56px -24px 0; }
}

@media (max-width: 640px) {
  .section { padding: 72px 20px; }
  .product-grid,
  .step-grid,
  .review-grid { grid-template-columns: 1fr; }
  .stats-panel { grid-template-columns: 1fr; padding: 40px 28px; border-radius: 32px; }
  .plan-summary { padding: 28px; }
  .pipe-row { grid-template-columns: auto 1fr; }
  .pipe-step { display: none; }
  .faq-q { padding: 20px 20px 20px 24px; font-size: 15px; }
  .faq-a p { padding: 0 24px 24px; }
  .consult-card { padding: 36px 24px; border-radius: 32px; }
  .consult-form { padding: 20px; }
  .footer-inner { grid-template-columns: 1fr 1fr; }
  .footer-bottom { flex-direction: column; }
}

@media (prefers-reduced-motion: reduce) {
  .marquee-track { animation: none; }
  .faq-a { transition: none; }
}

/* pressing either button inverts its relief, which is the whole interaction
   language of this style */
.btn:active { box-shadow: inset 0.2rem 0.2rem 1rem var(--primary-dark), inset -0.2rem -0.2rem 1rem var(--primary-light); }
.btn-glass:active { box-shadow: var(--shadow-inset); }
.btn-glass:hover { color: var(--primary); }


/* ============================================================
   LIQUID GLASS
   Every surface is a pane of tinted glass over a soft field of
   colour: a 12% glass fill, blur plus saturation behind it, and
   a stack of inset highlights (light) and inset shading (dark)
   that reads as a curved edge. Three themes switch the glass,
   the reflections and the accent together.
   ============================================================ */
body {
  /* palette: the original soft-UI colours */
  --c-glass: #bec8e4;
  --c-light: #ffffff;
  --c-dark: #1b2138;
  --c-content: #2c3557;
  --c-action: #6d5dfc;
  --c-on-action: #ffffff;
  --c-bg: #e4ebf5;
  --glass-reflex-dark: 1;
  --glass-reflex-light: 1;
  --saturation: 150%;
  --action-hue: 249deg;
  --orb-1: #8abdff;
  --orb-2: #a99ffd;
  --orb-3: #c8d0e7;
  --orb-4: #9baacf;
  --smoke: color-mix(in srgb, #1b2138 82%, transparent);
  color-scheme: light;

  --glass-fill: color-mix(in srgb, var(--c-glass) 12%, transparent);
  --glass-fill-strong: color-mix(in srgb, var(--c-glass) 36%, transparent);
  --glass-blur: blur(8px) saturate(var(--saturation));
  --glass-blur-lg: blur(14px) saturate(var(--saturation));

  /* the pane: eight inset reflections, two drop shadows */
  --glass-shadow:
    inset 0 0 0 1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 10%), transparent),
    inset 1.8px 3px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 90%), transparent),
    inset -2px -2px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 80%), transparent),
    inset -3px -8px 1px -6px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 60%), transparent),
    inset -0.3px -1px 4px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 12%), transparent),
    inset -1.5px 2.5px 0px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 20%), transparent),
    inset 0px 3px 4px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 20%), transparent),
    inset 2px -6.5px 1px -4px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 10%), transparent),
    0px 1px 5px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 10%), transparent),
    0px 6px 16px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 8%), transparent);

  /* the same ten layers, pressed in: highlights dimmed, shading from above, no lift */
  --glass-well:
    inset 0 0 0 1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 10%), transparent),
    inset 1.8px 3px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 30%), transparent),
    inset -2px -2px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 70%), transparent),
    inset -3px -8px 1px -6px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 40%), transparent),
    inset 0px 2px 8px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 16%), transparent),
    inset -1.5px 3.5px 1px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 22%), transparent),
    inset 0px 6px 8px -3px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 20%), transparent),
    inset 2px -6.5px 1px -4px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 4%), transparent),
    0px 0px 0px 0px transparent,
    0px 0px 0px 0px transparent;

  /* and lifted off the page, mid-morph */
  --glass-lift:
    inset 0 0 0 1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 14%), transparent),
    inset 1.8px 3px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 100%), transparent),
    inset -2px -2px 0px -2px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 90%), transparent),
    inset -3px -8px 1px -6px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 70%), transparent),
    inset -0.3px -1px 4px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 10%), transparent),
    inset -1.5px 2.5px 0px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 16%), transparent),
    inset 0px 3px 4px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 14%), transparent),
    inset 2px -6.5px 1px -4px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 8%), transparent),
    0px 4px 10px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 12%), transparent),
    0px 18px 36px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 12%), transparent);

  /* smaller pieces: chips, tabs, the switcher thumb */
  --glass-shadow-sm:
    inset 0 0 0 1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 10%), transparent),
    inset 2px 1px 0px -1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 90%), transparent),
    inset -1.5px -1px 0px -1px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 80%), transparent),
    inset -2px -6px 1px -5px color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 60%), transparent),
    inset -1px 2px 3px -1px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 20%), transparent),
    inset 0px -4px 1px -2px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 10%), transparent),
    0px 3px 6px 0px color-mix(in srgb, var(--c-dark) calc(var(--glass-reflex-dark) * 8%), transparent);

  /* the soft-UI tokens the rest of the stylesheet still speaks, mapped onto glass */
  --text-dark: var(--c-content);
  --text-muted: color-mix(in srgb, var(--c-content) 62%, var(--c-bg));
  --primary: var(--c-action);
  --primary-light: color-mix(in srgb, var(--c-action) 55%, white);
  --primary-dark: color-mix(in srgb, var(--c-action) 70%, black);
  --accent-orange: var(--c-action);
  --accent-soft: var(--primary-light);
  --accent-hue: var(--action-hue);
  --greyLight-1: var(--glass-fill);
  --bg-top: transparent;
  --bg-bottom: transparent;
  --clay-light: var(--glass-fill);
  --clay-dark: var(--smoke);
  --ink-panel: var(--smoke);
  --shadow: var(--glass-shadow-sm);
  --shadow-light: var(--glass-shadow-sm);
  --shadow-glass: var(--glass-shadow-sm);
  --shadow-lg: var(--glass-shadow);
  --shadow-dark: var(--glass-shadow-sm);
  --shadow-orange: var(--glass-shadow-sm);
  --shadow-inset: var(--glass-well);

  font-family: "Funnel Display", system-ui, sans-serif;
  font-optical-sizing: auto;
  background: var(--c-bg);
  color: var(--c-content);
  transition: background 400ms cubic-bezier(1, 0, 0.4, 1), color 400ms cubic-bezier(1, 0, 0.4, 1);
}
body:has(input[value="dark"]:checked) {
  --c-glass: #9baacf;
  --c-light: #e4ebf5;
  --c-dark: #0b0e1a;
  --c-content: #e4ebf5;
  --c-action: #8abdff;
  --c-on-action: #1b2138;
  --c-bg: #1b2138;
  --glass-reflex-dark: 2;
  --glass-reflex-light: 0.3;
  --action-hue: 213deg;
  --orb-1: #5b0eeb;
  --orb-2: #6d5dfc;
  --orb-3: #232a45;
  --orb-4: #3d6fb8;
  --smoke: color-mix(in srgb, #0b0e1a 60%, transparent);
  color-scheme: dark;
}
body:has(input[value="dim"]:checked) {
  --c-light: #8abdff;
  --c-dark: #0b0e1a;
  --c-glass: #9baacf;
  --c-content: #c8d0e7;
  --c-action: #8f83ff;
  --c-on-action: #ffffff;
  --c-bg: #171c2e;
  --glass-reflex-dark: 2;
  --glass-reflex-light: 0.7;
  --saturation: 150%;
  --action-hue: 249deg;
  --orb-1: #6d5dfc;
  --orb-2: #5b0eeb;
  --orb-3: #3b3f8f;
  --orb-4: #232a45;
  --smoke: color-mix(in srgb, #0b0e1a 62%, transparent);
  color-scheme: dark;
}

/* the field of colour the glass sits on */
.ambient {
  position: fixed;
  inset: 0;
  z-index: -1;
  overflow: hidden;
  pointer-events: none;
}
.ambient i {
  position: absolute;
  border-radius: 50%;
  filter: blur(70px);
  opacity: 0.8;
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1);
}
.ambient i:nth-child(1) { width: 52vw; height: 52vw; top: -16vw; left: -12vw; background-color: var(--orb-1); }
.ambient i:nth-child(2) { width: 44vw; height: 44vw; top: 18vh; right: -14vw; background-color: var(--orb-2); }
.ambient i:nth-child(3) { width: 58vw; height: 40vw; bottom: -18vw; left: 18vw; background-color: var(--orb-3); }
.ambient i:nth-child(4) { width: 30vw; height: 30vw; top: 52vh; left: -8vw; background-color: var(--orb-4); opacity: 0.55; }
.ambient::after {
  content: "";
  position: absolute;
  inset: 0;
  background-image: radial-gradient(color-mix(in srgb, var(--c-content) 14%, transparent) 1px, transparent 1.4px);
  background-size: 22px 22px;
  -webkit-mask-image: linear-gradient(180deg, #000, transparent 70%);
  mask-image: linear-gradient(180deg, #000, transparent 70%);
}

/* ── generic glass pieces ─────────────────────────────────── */
.btn-glass, .chip, .el, .product-badge, .s-icon, .round-btn, .faq-icon, .avatar,
.plan-focus span, .pipe-time, .quote-metric, .consult-form, .step-icon, .widget-img,
header .logo, .nav-center, .plan-tabs {
  background: var(--glass-fill);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
  border: 0;
  color: var(--c-content);
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1), color 160ms;
}
/* smoked glass */
.chip--dark, .step-icon, .round-btn, .pipe-row--pm .pipe-time, .faq-item.open .faq-icon {
  background: var(--smoke);
  color: #fff;
}
/* glass tinted with the action colour */
.chip--orange, .s-icon.orange, .product-badge--orange, .round-btn.added, .step-icon--orange,
.pipe-row--review .pipe-time, .review-card--dark .avatar {
  background: color-mix(in srgb, var(--c-action) 82%, transparent);
  color: var(--c-on-action);
}
.chip--orange .el, .chip--dark .el { background: color-mix(in srgb, var(--c-light) 14%, transparent); color: inherit; }
.step-icon svg { stroke: currentColor; }
.quote-metric { color: var(--c-action); }
.review-card--dark .quote-metric { color: #fff; }
.btn-glass:hover { color: var(--c-action); background: var(--glass-fill-strong); }
.s-icon:hover { scale: 1.1; }

/* ── type ─────────────────────────────────────────────────── */
h1, h2, h3, .section-title, .plan-title { letter-spacing: -0.035em; font-weight: 600; text-wrap: balance; }
.hero h1 { font-size: clamp(34px, 5.2vw, 66px); line-height: 1.02; margin-bottom: 40px; }
@media (max-width: 520px) { .hero h1 { font-size: 9.4vw; } }
.hero-left { max-width: 680px; }
.section-title { font-size: clamp(28px, 3.4vw, 44px); line-height: 1.08; }
.s2-right h2 { font-size: clamp(26px, 3vw, 38px); line-height: 1.12; letter-spacing: -0.03em; }
.consult-copy h2 { font-size: clamp(30px, 3.4vw, 44px); line-height: 1.06; letter-spacing: -0.035em; }
.product-info h3, .step-card h3 { font-size: 17px; letter-spacing: -0.01em; }
.giant-pill { font-weight: 600; letter-spacing: -0.03em; }
.section-sub, .plan-desc, .faq-a p, .step-card p { color: var(--text-muted); }
a { color: inherit; }

/* ── header: three floating glass pills ───────────────────── */
header {
  mix-blend-mode: normal;
  color: var(--c-content);
  padding: 16px 24px;
  gap: 16px;
}
header .logo { padding: 12px 20px; border-radius: 99em; font-size: 18px; }
header .logo svg { fill: var(--c-action); transition: fill 400ms; }
.nav-center { padding: 6px; gap: 2px; border-radius: 99em; font-size: 14px; }
.nav-center li { padding: 10px 16px; border-radius: 99em; transition: background-color 300ms, box-shadow 300ms, color 160ms; }
.nav-center li:hover { color: var(--c-action); }
.nav-center li.active { background: var(--glass-fill-strong); box-shadow: var(--glass-shadow-sm); }
.nav-center li.active::after { display: none; }
.nav-right { gap: 14px; color: var(--text-muted); }
@media (max-width: 1024px) {
  header { background: none; backdrop-filter: none; padding: 12px 16px; }
}

/* the theme switcher, docked in the header */
.switcher {
  --fz: 20px;
  position: relative;
  z-index: 1;
  display: flex;
  align-items: center;
  gap: 8px;
  width: 244px;
  height: 70px;
  box-sizing: border-box;
  padding: 8px 12px 10px;
  margin: 0;
  border: none;
  border-radius: 99em;
  zoom: 0.72;
  background-color: color-mix(in srgb, var(--c-glass) 12%, transparent);
  backdrop-filter: blur(8px) url(#switcher) saturate(var(--saturation));
  -webkit-backdrop-filter: blur(8px) saturate(var(--saturation));
  box-shadow: var(--glass-shadow);
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1);
}
.switcher__legend, .switcher__input {
  position: absolute; width: 1px; height: 1px; margin: -1px; border: 0; padding: 0;
  white-space: nowrap; clip-path: inset(100%); clip: rect(0 0 0 0); overflow: hidden;
}
.switcher__icon { display: block; width: 100%; transition: scale 200ms cubic-bezier(0.5, 0, 0, 1); }
.switcher__option {
  --c: var(--c-content);
  display: flex; justify-content: center; align-items: center;
  padding: 0 16px; width: 68px; height: 100%; box-sizing: border-box;
  border-radius: 99em; transition: all 160ms; cursor: pointer;
}
.switcher__option:hover { --c: var(--c-action); }
.switcher__option:hover .switcher__icon { scale: 1.2; }
.switcher__option:has(input:checked) { --c: var(--c-content); cursor: auto; }
.switcher__option:has(input:checked) .switcher__icon { scale: 1; }
.switcher__option:has(input:focus-visible) { outline: 2px solid var(--c-action); outline-offset: -4px; }
.switcher::after {
  content: "";
  position: absolute;
  left: 4px;
  top: 4px;
  width: 84px;
  height: calc(100% - 10px);
  border-radius: 99em;
  background-color: color-mix(in srgb, var(--c-glass) 36%, transparent);
  z-index: -1;
  box-shadow: var(--glass-shadow-sm);
}
.switcher:has(input[c-option="1"]:checked)::after {
  translate: 0 0; transform-origin: right;
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1), translate 400ms cubic-bezier(1, 0, 0.4, 1);
  animation: scaleToggle 440ms ease;
}
.switcher:has(input[c-option="2"]:checked)::after {
  translate: 76px 0;
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1), translate 400ms cubic-bezier(1, 0, 0.4, 1);
  animation: scaleToggle2 440ms ease;
}
.switcher[c-previous="1"]:has(input[c-option="2"]:checked)::after { transform-origin: left; }
.switcher[c-previous="3"]:has(input[c-option="2"]:checked)::after { transform-origin: right; }
.switcher:has(input[c-option="3"]:checked)::after {
  translate: 152px 0; transform-origin: left;
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1), translate 400ms cubic-bezier(1, 0, 0.4, 1);
  animation: scaleToggle3 440ms ease;
}
@keyframes scaleToggle { 50% { scale: 1.1 1; } }
@keyframes scaleToggle2 { 50% { scale: 1.2 1; } }
@keyframes scaleToggle3 { 50% { scale: 1.1 1; } }
.svg-defs { position: absolute; width: 0; height: 0; overflow: hidden; }

/* ── primary button: action-tinted glass, letters still flicker ─ */
.btn {
  --button-color: color-mix(in srgb, var(--c-action) 84%, transparent);
  --highlight-color-hue: var(--action-hue);
  font-family: "Funnel Display", system-ui, sans-serif;
  font-weight: 500;
  color: var(--c-on-action);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow);
}
.btn:active { box-shadow: var(--glass-well); }
.btn-svg { fill: var(--c-on-action); }

/* ── hero ─────────────────────────────────────────────────── */
.bg-text {
  background: linear-gradient(180deg, color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 55%), transparent) 0%, transparent 100%);
  -webkit-background-clip: text;
  background-clip: text;
}
.hero-footer { background: none; color: var(--text-muted); }
.console { width: min(540px, 40vw); color: #e9eef5; }
.code { background: color-mix(in srgb, #05070d 72%, transparent); border-color: color-mix(in srgb, #fff 10%, transparent); }
.out-tile { background: color-mix(in srgb, #05070d 55%, transparent); border-color: color-mix(in srgb, #fff 10%, transparent); }
.console-dot--live { background: var(--c-action); box-shadow: 0 0 10px var(--c-action); }

/* ── surfaces the morph doesn't own ───────────────────────── */
.bottom-section { background: transparent; box-shadow: none; }
.pill-gray { color: var(--text-muted); }
.pill-white, .pill-gray { color: var(--c-content); }
.product-stage {
  background: color-mix(in srgb, var(--c-glass) 8%, transparent);
  box-shadow: var(--glass-well);
}
.mod { background: var(--smoke); -webkit-backdrop-filter: var(--glass-blur); backdrop-filter: var(--glass-blur); box-shadow: var(--glass-shadow-sm); }
.mod-face { background: color-mix(in srgb, #05070d 70%, transparent); border-color: color-mix(in srgb, #fff 8%, transparent); }
.step-track { background: color-mix(in srgb, var(--c-content) 10%, transparent); }
.step-track-fill { background: var(--c-action); }
.stats-panel, .consult-card, .review-card--dark { color: #fff; }
.field input, .field select { background-color: color-mix(in srgb, #000 30%, transparent); border-color: color-mix(in srgb, #fff 12%, transparent); }
.consult-form { box-shadow: var(--glass-shadow-sm); background: color-mix(in srgb, var(--c-light) 6%, transparent); }

/* pipeline tabs: one glass track, one thumb that slides and squashes */
.plan-tabs {
  position: relative;
  display: inline-flex;
  flex-wrap: nowrap;
  gap: 2px;
  max-width: 100%;
  padding: 6px;
  border-radius: 99em;
  overflow-x: auto;
  scrollbar-width: none;
}
.plan-tabs::-webkit-scrollbar { display: none; }
.plan-tab, .plan-tab:hover, .plan-tab.active {
  position: relative;
  z-index: 1;
  background: none;
  border: 0;
  box-shadow: none;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
  color: var(--c-content);
  white-space: nowrap;
}
.plan-tab:hover { color: var(--c-action); }
.plan-tab.active { color: var(--c-content); }
.plan-tabs::after {
  content: "";
  position: absolute;
  top: 6px;
  left: 0;
  width: var(--tw, 0px);
  height: calc(100% - 12px);
  translate: var(--tx, 0px) 0;
  transform-origin: var(--to, center);
  border-radius: 99em;
  background-color: var(--glass-fill-strong);
  box-shadow: var(--glass-shadow-sm);
  transition: translate 400ms cubic-bezier(1, 0, 0.4, 1), width 400ms cubic-bezier(1, 0, 0.4, 1), background-color 400ms;
}
.plan-tabs.squash::after { animation: scaleToggle2 440ms ease; }
.plan-tabs.no-slide::after { transition: none; }

/* footer: one wide pane */
.site-footer {
  background: var(--glass-fill);
  -webkit-backdrop-filter: var(--glass-blur-lg);
  backdrop-filter: var(--glass-blur-lg);
  box-shadow: var(--glass-shadow);
}
.footer-wordmark { background: linear-gradient(180deg, color-mix(in srgb, var(--c-content) 16%, transparent) 0%, transparent 85%); -webkit-background-clip: text; background-clip: text; }
.footer-bottom { border-top-color: color-mix(in srgb, var(--c-content) 12%, transparent); }
.footer-col a:hover { color: var(--c-action); }
:focus-visible { outline-color: var(--c-action); }

/* ============================================================
   MORPH, in glass
   Same four beats as before: a pressed droplet, which lifts off
   the page, stretches to full height, then widens into the pane.
   The shell is the glass; the content waits until it lands.
   ============================================================ */
:root { --m-ease: cubic-bezier(0.16, 1, 0.3, 1); }
.m {
  --m-size: 6rem;
  --m-dur: 1.9s;
  --m-delay: 0s;
  --m-r: 2rem;
  --m-bg: var(--glass-fill);
  --m-end: var(--glass-shadow);
}
.m--inset { --m-bg: color-mix(in srgb, var(--c-glass) 8%, transparent); --m-end: var(--glass-well); }
.m--dark { --m-bg: var(--smoke); }
.m--console { --m-bg: var(--smoke); --m-dur: 2.6s; --m-size: 7rem; }
.m--accent { --m-bg: color-mix(in srgb, var(--c-action) 80%, transparent); }
.pill-orange { color: var(--c-on-action); }

.mo .m {
  position: relative;
  isolation: isolate;
  background: transparent !important;
  box-shadow: none !important;
  transition: border-color 0.6s ease calc(var(--m-delay) + var(--m-dur) * 0.7);
}
.mo .m:not(.is-in) { border-color: transparent !important; transition: none; }

.m-shell { display: none; }
.mo .m-shell {
  display: block;
  position: absolute;
  left: 50%;
  top: 50%;
  translate: -50% -50%;
  z-index: -1;
  pointer-events: none;
  width: var(--m-size);
  height: var(--m-size);
  border-radius: min(2rem, var(--m-r));
  background-color: color-mix(in srgb, var(--c-glass) 18%, transparent);
  -webkit-backdrop-filter: var(--glass-blur-lg);
  backdrop-filter: var(--glass-blur-lg);
  box-shadow: var(--glass-well);
}
.mo .m.is-in > .m-shell { animation: morph var(--m-dur) var(--m-ease) var(--m-delay) forwards; }
@keyframes morph {
  0% {
    width: var(--m-size); height: var(--m-size);
    border-radius: min(2rem, var(--m-r));
    background-color: color-mix(in srgb, var(--c-glass) 18%, transparent);
    box-shadow: var(--glass-well);
  }
  22% {
    width: var(--m-size); height: var(--m-size);
    border-radius: min(2rem, var(--m-r));
    background-color: color-mix(in srgb, var(--c-light) 20%, transparent);
    box-shadow: var(--glass-lift);
  }
  50% {
    width: var(--m-size); height: 100%;
    border-radius: min(2rem, var(--m-r));
    background-color: color-mix(in srgb, var(--c-light) 20%, transparent);
    box-shadow: var(--glass-lift);
  }
  100% {
    width: 100%; height: 100%;
    border-radius: var(--m-r);
    background-color: var(--m-bg);
    box-shadow: var(--m-end);
  }
}
/* once landed, the pane keeps tracking theme changes */
.mo .m.landed > .m-shell {
  animation: none;
  width: 100%; height: 100%;
  border-radius: var(--m-r);
  background-color: var(--m-bg);
  box-shadow: var(--m-end);
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1);
}
.m-shell { transition: none; }

.mo .m > :not(.m-shell),
.mo .m::before {
  opacity: 0;
  translate: 0 0.8rem;
  transition: opacity 0.7s ease, translate 0.9s var(--m-ease);
  transition-delay: calc(var(--m-delay) + var(--m-dur) * 0.62);
}
.mo .m.is-in > :not(.m-shell),
.mo .m.is-in::before { opacity: 1; translate: 0 0; }

.mo .rv { opacity: 0; translate: 0 2rem; transition: opacity 0.8s ease, translate 1s var(--m-ease); transition-delay: var(--m-delay, 0s); }
.mo .rv.is-in { opacity: 1; translate: 0 0; }

.mo .gsap-hero { animation: hero-in 1s var(--m-ease) both; }
.mo .hero-actions.gsap-hero { animation-delay: 0.15s; }
.mo .gsap-bg-text { animation: bg-in 1.6s var(--m-ease) both; }
@keyframes hero-in { from { opacity: 0; translate: -3rem 0; } }
@keyframes bg-in { from { opacity: 0; scale: 0.92; } }

.mo .step-track-fill { transform: scaleX(0); transition: transform 1.8s var(--m-ease) 0.8s; }
.mo .steps.is-in .step-track-fill { transform: scaleX(1); }

.giant-pill:active { scale: 0.95; transition: scale 0.1s; }
.round-btn.pop { animation: pop 0.4s var(--m-ease); }
@keyframes pop { from { scale: 0.8; } }
.plan-panel { transition: opacity 0.2s ease; }
.plan-panel.swap { opacity: 0; }

@media (prefers-reduced-motion: reduce) {
  body, .ambient i, .switcher, .switcher::after, .plan-tabs::after { transition: none !important; animation: none !important; }
}
.hero-right { grid-template-columns: minmax(0, 1fr); }
.console { min-width: 0; max-width: 100%; }
@media (max-width: 1100px) { .console { width: min(560px, 100%); } }
html:not(.mo) .m { -webkit-backdrop-filter: var(--glass-blur-lg); backdrop-filter: var(--glass-blur-lg); }


/* ── static glass panes (the morph now belongs to the hero alone) ── */
.pane {
  background: var(--glass-fill);
  -webkit-backdrop-filter: var(--glass-blur-lg);
  backdrop-filter: var(--glass-blur-lg);
  box-shadow: var(--glass-shadow);
  border-color: transparent;
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1),
    transform 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275), opacity 0.8s ease, translate 1s var(--m-ease);
}
.pane--dark { background: var(--smoke); }
.pane--inset { background: color-mix(in srgb, var(--c-glass) 8%, transparent); box-shadow: var(--glass-well); }

html { scroll-padding-top: 100px; }
html.menu-lock { overflow: hidden; }

/* ── floating glass pill ──────────────────────────────────── */
.site-nav {
  position: fixed;
  z-index: 100;
  top: calc(env(safe-area-inset-top, 0px) + 14px);
  left: 50%;
  right: auto;
  translate: -50% 0;
  width: min(1180px, calc(100% - 32px));
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  padding: 8px 8px 8px 22px;
  border-radius: 99em;
  mix-blend-mode: normal;
  color: var(--c-content);
  background: var(--glass-fill);
  -webkit-backdrop-filter: blur(14px) saturate(var(--saturation));
  backdrop-filter: blur(14px) saturate(var(--saturation));
  box-shadow: var(--glass-shadow);
  transition: width 0.6s var(--m-ease), background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1);
}
.site-nav.scrolled { width: min(960px, calc(100% - 32px)); background: color-mix(in srgb, var(--c-glass) 22%, transparent); }
.site-nav.menu-open { width: min(1180px, calc(100% - 32px)); background: var(--glass-fill); }
.site-nav .logo {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 0;
  font-size: 17px;
  font-weight: 600;
  letter-spacing: 0.01em;
  color: inherit;
  text-decoration: none;
  background: none;
  box-shadow: none;
  -webkit-backdrop-filter: none;
  backdrop-filter: none;
}
.site-nav .logo svg { width: 22px; height: 22px; fill: var(--c-action); transition: fill 400ms; }
.nav-actions { display: flex; align-items: center; gap: 8px; }
.nav-cta {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  height: 44px;
  padding: 0 20px;
  border-radius: 99em;
  font-size: 14px;
  font-weight: 500;
  white-space: nowrap;
  text-decoration: none;
  color: var(--c-on-action);
  background: color-mix(in srgb, var(--c-action) 86%, transparent);
  box-shadow: var(--glass-shadow-sm);
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1), scale 0.2s;
}
.nav-cta:hover { background: var(--c-action); }
.nav-cta:active { scale: 0.97; }
@media (max-width: 520px) { .site-nav .nav-cta { display: none; } }

.burger {
  position: relative;
  width: 48px;
  height: 48px;
  flex-shrink: 0;
  border: 0;
  border-radius: 50%;
  cursor: pointer;
  color: var(--c-content);
  background: var(--glass-fill-strong);
  box-shadow: var(--glass-shadow-sm);
  transition: color 160ms, background-color 400ms cubic-bezier(1, 0, 0.4, 1), scale 0.2s;
}
.burger:hover { color: var(--c-action); }
.burger:active { scale: 0.94; }
.burger span {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 18px;
  height: 2px;
  margin: -1px 0 0 -9px;
  border-radius: 2px;
  background: currentColor;
  transition: transform 0.5s var(--m-ease), width 0.3s var(--m-ease);
}
.burger span:nth-child(1) { transform: translateY(-4px); }
.burger span:nth-child(2) { transform: translateY(4px); width: 12px; }
.burger:hover span:nth-child(2) { width: 18px; }
.burger[aria-expanded="true"] span:nth-child(1) { transform: rotate(45deg); }
.burger[aria-expanded="true"] span:nth-child(2) { transform: rotate(-45deg); width: 18px; }

/* ── full-page menu: a sheet of glass that pours out of the button ── */
.menu {
  --mx: calc(100% - 48px);
  --my: 46px;
  position: fixed;
  inset: 0;
  z-index: 90;
  overflow-y: auto;
  visibility: hidden;
  pointer-events: none;
  background: color-mix(in srgb, var(--c-bg) 84%, transparent);
  -webkit-backdrop-filter: blur(30px) saturate(var(--saturation));
  backdrop-filter: blur(30px) saturate(var(--saturation));
  clip-path: circle(0px at var(--mx) var(--my));
  transition: clip-path 0.7s var(--m-ease), visibility 0s linear 0.7s;
}
.menu.open {
  visibility: visible;
  pointer-events: auto;
  clip-path: circle(150vmax at var(--mx) var(--my));
  transition: clip-path 0.9s var(--m-ease), visibility 0s;
}
.menu-inner {
  width: min(1180px, calc(100% - 32px));
  min-height: 100%;
  margin: 0 auto;
  padding: 112px 0 40px;
  display: grid;
  grid-template-columns: minmax(0, 1.55fr) minmax(0, 1fr);
  gap: 40px 72px;
  align-content: center;
}
.menu-links { list-style: none; margin: 0; padding: 0; }
.menu-links li,
.menu-aside > * {
  opacity: 0;
  translate: 0 1.6rem;
  transition: opacity 0.4s ease, translate 0.6s var(--m-ease);
}
.menu.open .menu-links li,
.menu.open .menu-aside > * {
  opacity: 1;
  translate: 0 0;
  transition-delay: calc(0.18s + var(--i, 0) * 0.055s);
}
.menu-links a {
  display: grid;
  grid-template-columns: 2.8em minmax(0, 1fr) auto;
  align-items: baseline;
  gap: 12px;
  padding: 8px 4px;
  color: var(--c-content);
  text-decoration: none;
  border-bottom: 1px solid color-mix(in srgb, var(--c-content) 10%, transparent);
}
.menu-links li:first-child a { border-top: 1px solid color-mix(in srgb, var(--c-content) 10%, transparent); }
.menu-links .idx { font: 500 12px var(--mono); letter-spacing: 0.08em; color: var(--text-muted); }
.menu-links .label {
  font-size: clamp(28px, min(4vw, 6.2vh), 54px);
  font-weight: 600;
  line-height: 1.04;
  letter-spacing: -0.045em;
  transition: color 0.25s, translate 0.5s var(--m-ease);
}
.menu-links .hint { font-size: 14px; color: var(--text-muted); text-align: right; transition: color 0.25s; }
.menu-links a:hover .label,
.menu-links a:focus-visible .label { color: var(--c-action); translate: 12px 0; }
.menu-links a:hover .hint { color: var(--c-content); }
.menu-links a:focus-visible { outline: none; }

.menu-aside { display: grid; gap: 16px; align-content: center; }
.menu-card { display: grid; gap: 12px; justify-items: start; padding: 24px; border-radius: 28px; }
.menu-kicker { font: 500 11px var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-muted); }
.menu-lead { font-size: 18px; line-height: 1.45; letter-spacing: -0.01em; }
.menu-status { display: flex; align-items: center; gap: 10px; font-size: 18px; font-weight: 500; }
.live-dot { width: 9px; height: 9px; border-radius: 50%; background: #2fd47a; box-shadow: 0 0 0 4px color-mix(in srgb, #2fd47a 22%, transparent); }
.menu-meta { font: 12px var(--mono); color: var(--text-muted); }
.menu-social { display: flex; gap: 18px; font-size: 14px; }
.menu-social a { color: var(--text-muted); text-decoration: none; }
.menu-social a:hover { color: var(--c-action); }
.menu-card .switcher { zoom: 0.8; }

@media (max-width: 860px) {
  .menu-inner { grid-template-columns: minmax(0, 1fr); padding: 104px 0 32px; align-content: start; gap: 32px; }
  .menu-links .hint { display: none; }
  .menu-links a { grid-template-columns: 2.6em minmax(0, 1fr); padding: 10px 2px; }
  .menu-links .label { font-size: clamp(30px, 9vw, 44px); }
}
@media (prefers-reduced-motion: reduce) {
  .menu, .menu.open { transition: visibility 0s; }
  .menu-links li, .menu-aside > * { transition: none !important; }
  .site-nav { transition: none; }
}

/* ── platform section ─────────────────────────────────────── */
.platform {
  position: relative;
  z-index: 20;
  display: flex;
  justify-content: center;
  padding: 140px 48px 120px;
}
.platform-inner { width: 100%; max-width: 1200px; display: grid; gap: 56px; }
.platform-head {
  display: grid;
  grid-template-columns: minmax(0, 1.25fr) minmax(0, 1fr);
  gap: 24px 64px;
  align-items: end;
}
.platform-head .about-label { grid-column: 1 / -1; }
.platform-title {
  margin: 0;
  font-size: clamp(34px, 4.6vw, 64px);
  line-height: 1;
  letter-spacing: -0.045em;
}
.platform-title span { color: var(--text-muted); }
.platform-sub { max-width: 30em; font-size: 17px; line-height: 1.6; color: var(--text-muted); }

.flow {
  list-style: none;
  margin: 0;
  padding: 0;
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 32px;
}
.flow-step {
  position: relative;
  min-width: 0;
  display: flex;
  flex-direction: column;
  gap: 14px;
  padding: 28px;
  border-radius: 32px;
}
.flow-top { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; }
.flow-icon {
  width: 52px;
  height: 52px;
  display: grid;
  place-items: center;
  border-radius: 16px;
  color: #fff;
  background: var(--smoke);
  box-shadow: var(--glass-shadow-sm);
}
.flow-step--core .flow-icon { background: color-mix(in srgb, var(--c-action) 84%, transparent); color: var(--c-on-action); }
.flow-icon svg, .flow-link svg, .region svg {
  width: 24px;
  height: 24px;
  fill: none;
  stroke: currentColor;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.flow-num { font: 500 11px var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-muted); }
.flow-step h3 { margin: 0; font-size: 28px; line-height: 1.1; letter-spacing: -0.035em; }
.flow-step p { font-size: 15px; line-height: 1.6; color: var(--text-muted); }
.flow-call {
  width: fit-content;
  max-width: 100%;
  padding: 8px 12px;
  border-radius: 12px;
  font: 12.5px/1.4 var(--mono);
  color: var(--c-content);
  background: color-mix(in srgb, var(--c-glass) 10%, transparent);
  box-shadow: var(--glass-well);
  overflow-wrap: anywhere;
}
.flow-metric {
  margin-top: auto;
  padding-top: 16px;
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  gap: 12px;
  border-top: 1px solid color-mix(in srgb, var(--c-content) 10%, transparent);
  font-size: 13px;
  color: var(--text-muted);
}
.flow-metric strong { font-size: 24px; font-weight: 600; letter-spacing: -0.03em; color: var(--c-content); font-variant-numeric: tabular-nums; }
.flow-link {
  position: absolute;
  z-index: 2;
  top: 50%;
  right: -32px;
  width: 32px;
  height: 32px;
  margin-top: -16px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  color: var(--c-action);
  background: var(--glass-fill-strong);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
}
.flow-link svg { width: 16px; height: 16px; stroke-width: 2; }

.platform-foot {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 14px 24px;
  padding: 12px 12px 12px 24px;
  border-radius: 99em;
}
.region { display: flex; align-items: center; gap: 12px; font-size: 15px; }
.region strong { font-weight: 600; }
.region svg { color: var(--c-action); flex-shrink: 0; }
.region-chips { display: flex; flex-wrap: wrap; gap: 6px; }
.region-chips span {
  padding: 6px 11px;
  border-radius: 99em;
  font: 12px var(--mono);
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow-sm);
}
.platform-foot .btn-glass { text-decoration: none; }

@media (max-width: 1024px) {
  .platform { padding: 112px 20px 80px; }
  .platform-foot { border-radius: 28px; padding: 20px; }
}
@media (max-width: 900px) {
  .platform-head { grid-template-columns: minmax(0, 1fr); }
  .flow { grid-template-columns: minmax(0, 1fr); gap: 28px; }
  .flow-link { top: auto; right: auto; bottom: -30px; left: 50%; margin: 0 0 0 -16px; rotate: 90deg; }
}
.mo .pane.rv {
  transition: opacity 0.8s ease var(--m-delay, 0s), translate 1s var(--m-ease) var(--m-delay, 0s),
    background-color 400ms cubic-bezier(1, 0, 0.4, 1), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1);
}


/* ── module cards: one glass pane, one live instrument each ── */
.mgrid { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 20px; }
@media (max-width: 1100px) { .mgrid { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
@media (max-width: 600px) { .mgrid { grid-template-columns: minmax(0, 1fr); } }

.mcard {
  position: relative;
  min-width: 0;
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 16px 16px 18px;
  border-radius: 32px;
  transition: translate 0.5s var(--m-ease), box-shadow 400ms cubic-bezier(1, 0, 0.4, 1),
    background-color 400ms cubic-bezier(1, 0, 0.4, 1), opacity 0.8s ease;
}
.mcard:hover { translate: 0 -6px; box-shadow: var(--glass-lift); }
/* a specular highlight that follows the pointer */
.mcard::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  pointer-events: none;
  background: radial-gradient(260px circle at var(--px, 50%) var(--py, 0%),
    color-mix(in srgb, var(--c-light) calc(var(--glass-reflex-light) * 26%), transparent), transparent 70%);
  opacity: 0;
  transition: opacity 0.4s ease;
}
.mcard:hover::after { opacity: 1; }
.mcard--new { background: color-mix(in srgb, var(--c-action) 7%, var(--glass-fill)); }

.mcard-head { display: flex; justify-content: space-between; align-items: center; gap: 8px; padding: 2px 4px 0; }
.mcard-kicker { font: 500 11px var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-muted); }
.mcard-chip {
  padding: 5px 10px;
  border-radius: 99em;
  font: 11px var(--mono);
  white-space: nowrap;
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow-sm);
}
.mcard-chip--new { background: color-mix(in srgb, var(--c-action) 84%, transparent); color: var(--c-on-action); }

.mcard-stage {
  position: relative;
  height: 196px;
  display: grid;
  place-items: center;
  padding: 16px;
  border-radius: 22px;
  overflow: hidden;
  background: color-mix(in srgb, var(--c-glass) 8%, transparent);
  box-shadow: var(--glass-well);
}
.mcard-body { display: grid; gap: 6px; padding: 0 4px; }
.mcard-body h3 { margin: 0; font-size: 22px; line-height: 1.15; letter-spacing: -0.03em; }
.mcard-body p { font-size: 14px; line-height: 1.55; color: var(--text-muted); }
.mcard-caps { display: flex; flex-wrap: wrap; gap: 6px; margin: 0; padding: 0 4px; list-style: none; }
.mcard-caps li {
  padding: 5px 10px;
  border-radius: 99em;
  font: 12px var(--mono);
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow-sm);
}
.mcard-foot {
  margin-top: auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  padding: 14px 4px 0;
  border-top: 1px solid color-mix(in srgb, var(--c-content) 10%, transparent);
  font-size: 13px;
  color: var(--text-muted);
}

/* glass switch: the thumb slides and squashes like the theme switcher */
.gswitch {
  position: relative;
  flex-shrink: 0;
  width: 60px;
  height: 34px;
  border: 0;
  border-radius: 99em;
  cursor: pointer;
  background: color-mix(in srgb, var(--c-glass) 16%, transparent);
  box-shadow: var(--glass-well);
  transition: background-color 400ms cubic-bezier(1, 0, 0.4, 1);
}
.gswitch[aria-checked="true"] { background: color-mix(in srgb, var(--c-action) 86%, transparent); }
.gswitch-thumb {
  position: absolute;
  top: 3px;
  left: 3px;
  width: 38px;
  height: 28px;
  border-radius: 99em;
  background: color-mix(in srgb, #fff 78%, transparent);
  box-shadow: var(--glass-shadow-sm), 0 2px 6px rgba(0, 0, 0, 0.12);
  transform-origin: left;
  transition: translate 400ms cubic-bezier(1, 0, 0.4, 1);
}
.gswitch[aria-checked="true"] .gswitch-thumb { translate: 16px 0; transform-origin: right; }
.gswitch.squash .gswitch-thumb { animation: scaleToggle2 440ms ease; }
.gswitch:focus-visible { outline: 2px solid var(--c-action); outline-offset: 3px; }

/* instrument: Vision */
.viz-vision { width: 100%; height: 100%; }
.viz-contour { fill: none; stroke: var(--c-action); stroke-width: 1.6; stroke-dasharray: 4 3; }
.viz-brackets { fill: none; stroke: var(--c-content); stroke-width: 1.4; opacity: 0.55; }
.viz-score {
  position: absolute;
  top: 12px;
  right: 12px;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 10px 4px 4px;
  border-radius: 99em;
  font: 500 12px var(--mono);
  background: var(--glass-fill-strong);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
}
.viz-score svg { width: 22px; height: 22px; rotate: -90deg; }
.viz-score circle { fill: none; stroke: color-mix(in srgb, var(--c-content) 16%, transparent); stroke-width: 4; }
.viz-score .arc { stroke: var(--c-action); stroke-linecap: round; }
.viz-tag {
  position: absolute;
  left: 12px;
  bottom: 12px;
  padding: 4px 10px;
  border-radius: 99em;
  font: 11px var(--mono);
  background: var(--glass-fill-strong);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
}
.viz-tag--ok::before { content: ""; display: inline-block; width: 6px; height: 6px; margin-right: 6px; border-radius: 50%; background: #2fd47a; vertical-align: 1px; }

/* instrument: Triage */
.viz-queue { width: 100%; display: grid; gap: 8px; }
.q-row {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto;
  align-items: center;
  gap: 10px;
  padding: 8px 10px 8px 8px;
  border-radius: 14px;
  font: 12px var(--mono);
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow-sm);
  opacity: 0.7;
}
.q-row.is-top { opacity: 1; background: var(--glass-fill-strong); scale: 1.03; }
.q-pri { padding: 3px 7px; border-radius: 8px; font-weight: 500; font-size: 11px; color: #fff; }
.q-pri.p1 { background: #e5484d; }
.q-pri.p2 { background: #d9822b; }
.q-pri.p3 { background: color-mix(in srgb, var(--c-content) 40%, transparent); }
.q-id { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.q-to { color: var(--text-muted); white-space: nowrap; }

/* instrument: Records */
.viz-sync {
  position: relative;
  width: 100%;
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto;
  align-items: center;
  gap: 8px;
  margin-top: -14px;
}
.viz-sync::before {
  content: "";
  position: absolute;
  left: 18px;
  right: 18px;
  top: 50%;
  border-top: 1.5px dashed color-mix(in srgb, var(--c-action) 60%, transparent);
}
.sync-node {
  position: relative;
  width: 36px;
  height: 36px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  font: 600 10px var(--mono);
  color: #fff;
  background: var(--smoke);
  box-shadow: var(--glass-shadow-sm);
}
.sync-node svg { width: 18px; height: 18px; fill: var(--c-action); }
.sync-node--ehr { background: color-mix(in srgb, var(--c-action) 84%, transparent); color: var(--c-on-action); }
.sync-chips { position: relative; display: grid; gap: 6px; justify-items: center; }
.sync-chips span {
  max-width: 100%;
  padding: 4px 7px;
  border-radius: 99em;
  font: 10px var(--mono);
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  background: var(--glass-fill-strong);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
}

/* instrument: Insights */
.viz-chart { width: 100%; height: 100%; display: flex; flex-direction: column; justify-content: space-between; gap: 12px; }
.chart-head { display: flex; justify-content: space-between; align-items: baseline; gap: 8px; font-size: 12px; color: var(--text-muted); }
.chart-head strong { font-size: 22px; font-weight: 600; letter-spacing: -0.03em; color: var(--c-content); font-variant-numeric: tabular-nums; }
.chart-head em { font-style: normal; font-size: 12px; font-weight: 500; color: #1fa463; margin-left: 4px; }
body:has(input[value="dark"]:checked) .chart-head em, body:has(input[value="dim"]:checked) .chart-head em { color: #45d88a; }
.bars { flex: 1; display: flex; align-items: flex-end; gap: 5px; border-bottom: 1px solid color-mix(in srgb, var(--c-content) 14%, transparent); }
.bars i { flex: 1; height: var(--h); border-radius: 5px 5px 2px 2px; background: color-mix(in srgb, var(--c-content) 16%, transparent); }
.bars i:last-child { background: var(--c-action); box-shadow: 0 0 14px color-mix(in srgb, var(--c-action) 50%, transparent); }

/* pipeline summary under the grid */
.pipebar {
  margin-top: 24px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 12px 20px;
  padding: 12px 22px 12px 12px;
  border-radius: 99em;
}
.pipebar-label {
  padding: 8px 14px;
  border-radius: 99em;
  font: 500 11px var(--mono);
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #fff;
  background: var(--smoke);
  box-shadow: var(--glass-shadow-sm);
}
.pipebar-flow { flex: 1; min-width: 0; display: flex; flex-wrap: wrap; align-items: center; gap: 8px; font-size: 14px; }
.pipebar-flow .chip-mod { padding: 6px 12px; border-radius: 99em; font-weight: 500; background: var(--glass-fill-strong); box-shadow: var(--glass-shadow-sm); }
.pipebar-flow .chip-mod.async { font-weight: 400; color: var(--text-muted); }
.pipebar-flow svg { width: 14px; height: 14px; fill: none; stroke: var(--c-action); stroke-width: 2.2; stroke-linecap: round; stroke-linejoin: round; }
.pipebar-flow .empty { color: var(--text-muted); }
.pipebar-meta { font: 12px var(--mono); color: var(--text-muted); font-variant-numeric: tabular-nums; }
@media (max-width: 760px) { .pipebar { border-radius: 28px; padding: 16px; } }
@media (prefers-reduced-motion: reduce) { .mcard, .mcard:hover { translate: none; } .gswitch.squash .gswitch-thumb { animation: none; } }


/* ── type pairing: Instrument Serif italic for display, Rubik for reading, JetBrains Mono for labels ── */
h1, h2, .plan-title, .menu-links .label,
:is(h1, h2, .section-title, .platform-title, .plan-title) :is(span, em, strong) {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-style: italic;
  font-weight: 400;
  letter-spacing: -0.02em;
  font-optical-sizing: auto;
}
h3, .mcard-body h3, .flow-step h3 { font-family: "Funnel Display", system-ui, sans-serif; font-style: normal; font-weight: 500; letter-spacing: -0.02em; }
.hero h1 { font-size: clamp(46px, 6.6vw, 90px); line-height: 0.92; margin-bottom: 24px; }
@media (max-width: 520px) { .hero h1 { font-size: 12.4vw; } }
.hero-lede {
  max-width: 34em;
  margin: 0 0 36px;
  font-size: clamp(16px, 1.3vw, 19px);
  line-height: 1.55;
  color: var(--text-muted);
}
.mo .hero-lede.gsap-hero { animation-delay: 0.08s; }
.section-title { font-size: clamp(38px, 4.6vw, 64px); line-height: 0.98; }
.platform-title { font-size: clamp(44px, 6vw, 86px); line-height: 0.94; letter-spacing: -0.025em; }
.consult-copy h2 { font-size: clamp(38px, 4.4vw, 62px); line-height: 0.98; letter-spacing: -0.02em; }
.plan-title { font-size: clamp(38px, 4.2vw, 58px); line-height: 0.98; }
.menu-links .label { font-size: clamp(36px, min(5.4vw, 7.6vh), 72px); line-height: 1; letter-spacing: -0.02em; }


/* ── uppercase display headlines + serif wordmark ── */
h1, h2, .plan-title, .menu-links .label,
:is(h1, h2, .section-title, .platform-title, .plan-title) :is(span, em, strong) {
  text-transform: uppercase;
  letter-spacing: -0.03em;
}
.hero-left { max-width: 720px; }
.hero h1 { font-size: clamp(40px, 5vw, 72px); line-height: 0.9; }
@media (max-width: 520px) { .hero h1 { font-size: 10.6vw; } }
.section-title { font-size: clamp(32px, 3.8vw, 54px); line-height: 0.94; }
.platform-title { font-size: clamp(38px, 5vw, 72px); line-height: 0.9; }
.consult-copy h2 { font-size: clamp(32px, 3.8vw, 52px); line-height: 0.94; }
.plan-title { font-size: clamp(32px, 3.6vw, 48px); line-height: 0.94; }
.menu-links .label { font-size: clamp(32px, min(4.6vw, 6.8vh), 62px); line-height: 0.95; }
.site-nav .logo,
.footer-brand .logo {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-style: italic;
  font-weight: 400;
  font-size: 24px;
  letter-spacing: 0.01em;
  text-transform: uppercase;
  line-height: 1;
}


/* ── hero headline: the section-title style, at exactly twice its size ── */
.hero h1 {
  font-size: calc(2 * clamp(32px, 3.8vw, 54px));
  line-height: 0.94;
  letter-spacing: -0.03em;
  margin-bottom: 28px;
}
@media (max-width: 520px) { .hero h1 { font-size: calc(2 * clamp(32px, 3.8vw, 54px)); } }
.hero h1 span.accent { color: var(--text-muted); }
.hero { height: auto; min-height: 100vh; padding-block: 128px 104px; }


/* desktop: the hero headline at 60% of its 2x size (a 40% reduction) */
@media (min-width: 1025px) {
  .hero h1 { font-size: calc(0.6 * 2 * clamp(32px, 3.8vw, 54px)); }
}


/* ============================================================
   HERO, recomposed: copy on the left, a layered composition of
   live modules on the right (capture → crop → layers → request →
   response). Everything on the right is drawn in code.
   ============================================================ */
.hero.hx {
  position: relative;
  height: auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 132px 48px 88px;
  overflow: hidden;
}
.hx-grid {
  position: relative;
  z-index: 10;
  width: 100%;
  max-width: 1360px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: minmax(0, 0.92fr) minmax(0, 1.08fr);
  gap: clamp(32px, 4vw, 64px);
  align-items: center;
}
.hx-copy { min-width: 0; }

.hx-eyebrow {
  display: flex;
  align-items: center;
  gap: 18px;
  margin: 0 0 22px;
  font: 500 12px var(--mono);
  letter-spacing: 0.42em;
  text-transform: uppercase;
  color: var(--text-muted);
}
.hx-eyebrow span { width: 56px; height: 1.5px; background: var(--c-action); }

.hero .hx-title,
.hero .hx-title span {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-style: italic;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: -0.035em;
}
.hero .hx-title {
  margin: 0 0 26px;
  font-size: clamp(54px, 5.9vw, 104px);
  line-height: 0.86;
  color: var(--c-content);
}
.hero .hx-title span { color: color-mix(in srgb, var(--c-content) 62%, var(--c-action) 8%); opacity: 0.78; }
.hero .hero-lede { max-width: 30em; margin: 0 0 32px; }

.hx-points {
  display: flex;
  flex-wrap: nowrap;
  gap: 18px 0;
  margin: 44px 0 0;
  padding: 0;
  list-style: none;
}
.hx-points li {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 0 20px;
  white-space: nowrap;
  border-left: 1px solid color-mix(in srgb, var(--c-content) 14%, transparent);
}
.hx-points li:first-child { padding-left: 0; border-left: 0; }
.hx-points svg {
  width: 26px;
  height: 26px;
  flex-shrink: 0;
  fill: none;
  stroke: var(--c-action);
  stroke-width: 1.6;
  stroke-linejoin: round;
  stroke-linecap: round;
}
.hx-points span { display: grid; gap: 2px; font-size: 13px; color: var(--text-muted); }
.hx-points strong { font-size: 15px; font-weight: 600; color: var(--c-content); }

/* ── the stage ─────────────────────────────────────────────── */
.hx-stage {
  position: relative;
  container-type: inline-size;
  width: 100%;
  aspect-ratio: 822 / 620;
  min-width: 0;
}
.hx-glow {
  position: absolute;
  left: 2%;
  top: -14%;
  width: 104%;
  aspect-ratio: 1;
  border-radius: 50%;
  background: radial-gradient(circle, color-mix(in srgb, var(--c-action) 26%, transparent) 0%, color-mix(in srgb, var(--c-action) 10%, transparent) 46%, transparent 68%);
  pointer-events: none;
}
.hx-stage > .m,
.mo .hx-stage > .m { position: absolute; }

/* capture viewport */
.hx-view {
  left: 0;
  top: 22%;
  width: 66%;
  height: 68%;
  border-radius: 4.2cqw;
  overflow: hidden;
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow);
}
.mo .hx-view { overflow: visible; }
.hx-skin {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  border-radius: inherit;
  display: block;
}
.mo .hx-view > .hx-skin { clip-path: inset(0 round 4.2cqw); }
.hx-marker {
  position: absolute;
  left: calc(236 / 560 * 100%);
  top: calc(236 / 420 * 100%);
  width: 6.4cqw;
  height: 6.4cqw;
  translate: -50% -50%;
  border-radius: 50%;
  border: 1.5px solid color-mix(in srgb, #fff 85%, transparent);
  box-shadow: 0 0 0 4px color-mix(in srgb, var(--c-action) 30%, transparent);
}
.hx-chip {
  position: absolute;
  padding: 0.7cqw 1.3cqw;
  border-radius: 99em;
  font: 500 clamp(9px, 1.3cqw, 12px) var(--mono);
  color: var(--c-content);
  background: color-mix(in srgb, #fff 62%, transparent);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
  white-space: nowrap;
}
.hx-chip--tl { left: 2.4cqw; top: 2.4cqw; }
.hx-chip--bl { left: 2.4cqw; bottom: 2.4cqw; display: inline-flex; align-items: center; gap: 0.8cqw; }
.hx-chip--bl i { width: 0.9cqw; height: 0.9cqw; min-width: 6px; min-height: 6px; border-radius: 50%; background: var(--c-action); }

/* leader line from the lesion to the crop */
.hx-link {
  position: absolute;
  z-index: 3;
  left: calc(66% * 236 / 560 + 3.2cqw);
  top: calc(22% + 68% * 236 / 420);
  width: calc(37% - 66% * 236 / 560 - 3.2cqw);
  height: 1.5px;
  background: color-mix(in srgb, #fff 80%, transparent);
  box-shadow: 0 0 6px color-mix(in srgb, var(--c-action) 40%, transparent);
  transform-origin: left;
}
.mo .hx-link { animation: hx-draw 0.8s var(--m-ease) 1.6s both; }
@keyframes hx-draw { from { scale: 0 1; } }

/* stacked analysis layers */
.hx-sheets { position: absolute; z-index: 2; left: 37%; top: 44%; width: 25%; height: 33%; }
.hx-sheet {
  position: absolute;
  inset: 0;
  border-radius: 3cqw;
  translate: calc(var(--k) * 3.6cqw) calc(var(--k) * 3cqw);
  background: color-mix(in srgb, #fff calc(28% - var(--k) * 5%), transparent);
  -webkit-backdrop-filter: blur(6px) saturate(var(--saturation));
  backdrop-filter: blur(6px) saturate(var(--saturation));
  box-shadow: var(--glass-shadow-sm);
  border: 1px solid color-mix(in srgb, #fff 55%, transparent);
}
.hx-sheet em {
  position: absolute;
  right: 1.4cqw;
  bottom: 1cqw;
  font: 500 clamp(8px, 1.1cqw, 11px) var(--mono);
  font-style: normal;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: color-mix(in srgb, var(--c-content) 60%, transparent);
}
.mo .hx-sheet { animation: hx-fan 0.9s var(--m-ease) both; animation-delay: calc(1.5s + var(--k) * 0.12s); }
@keyframes hx-fan { from { translate: 0 0; opacity: 0; } }

/* the crop */
.hx-crop {
  z-index: 4;
  left: 37%;
  top: 44%;
  width: 25%;
  height: 33%;
  padding: 2.2cqw;
  border-radius: 3cqw;
  display: grid;
  place-items: center;
  background: var(--glass-fill);
  box-shadow: var(--glass-shadow);
}
.hx-crop-inner { position: relative; width: 100%; height: 100%; }
.hx-crop-inner svg { display: block; width: 100%; height: 100%; border-radius: 1.2cqw; }
.hx-contour { fill: none; stroke: #fff; stroke-width: 1.4; stroke-dasharray: 4 3; opacity: 0.9; }
.hx-brackets { position: absolute; inset: -0.6cqw; pointer-events: none; }
.hx-brackets::before, .hx-brackets::after {
  content: "";
  position: absolute;
  inset: 0;
  border: 2.5px solid #fff;
  border-radius: 1.2cqw;
  -webkit-mask: linear-gradient(#000 0 0) top left / 22% 22% no-repeat, linear-gradient(#000 0 0) bottom right / 22% 22% no-repeat;
  mask: linear-gradient(#000 0 0) top left / 22% 22% no-repeat, linear-gradient(#000 0 0) bottom right / 22% 22% no-repeat;
}
.hx-brackets::after {
  -webkit-mask: linear-gradient(#000 0 0) top right / 22% 22% no-repeat, linear-gradient(#000 0 0) bottom left / 22% 22% no-repeat;
  mask: linear-gradient(#000 0 0) top right / 22% 22% no-repeat, linear-gradient(#000 0 0) bottom left / 22% 22% no-repeat;
}
.hx-crop-label {
  position: absolute;
  left: 50%;
  bottom: -3.4cqw;
  translate: -50% 0;
  font: 500 clamp(8px, 1.1cqw, 11px) var(--mono);
  color: var(--text-muted);
  white-space: nowrap;
}

/* request */
.hx-console {
  z-index: 5;
  left: 40%;
  top: 0;
  width: 60%;
  height: 32%;
  padding: 2.4cqw 2.6cqw;
  border-radius: 3.4cqw;
  display: flex;
  flex-direction: column;
  gap: 1.6cqw;
  color: #e9eef5;
  background: var(--smoke);
  box-shadow: var(--glass-shadow);
}
.hx-console-head { display: flex; align-items: center; gap: 1cqw; font: clamp(9px, 1.35cqw, 12.5px) "Funnel Display", system-ui, sans-serif; color: #9aa6c4; }
.hx-console-head .dot { width: 1.2cqw; height: 1.2cqw; min-width: 7px; min-height: 7px; border-radius: 50%; background: #3a4363; }
.hx-console-head .dot--live { background: var(--c-action); box-shadow: 0 0 8px var(--c-action); }
.hx-console-head .route { margin-left: auto; }
.hx-code {
  flex: 1;
  margin: 0;
  padding: 1.8cqw 2.2cqw;
  border-radius: 2cqw;
  font: clamp(8.5px, 1.72cqw, 15px)/1.62 var(--mono);
  white-space: pre;
  overflow: hidden;
  background: color-mix(in srgb, #05070d 70%, transparent);
  border: 1px solid color-mix(in srgb, #fff 8%, transparent);
}
.hx-code .k { color: #93b2ff; }
.hx-code .s { color: #8fe0b4; }

/* response */
.hx-results {
  z-index: 5;
  left: 70.5%;
  top: 35%;
  width: 29.5%;
  height: 43%;
  padding: 1.4cqw;
  border-radius: 3cqw;
  display: grid;
  grid-template-rows: repeat(3, minmax(0, 1fr));
  gap: 1cqw;
  color: #e9eef5;
  background: var(--smoke);
  box-shadow: var(--glass-shadow);
}
.hx-tile {
  min-height: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.5cqw;
  padding: 0 1.8cqw;
  border-radius: 1.8cqw;
  background: color-mix(in srgb, #05070d 45%, transparent);
  border: 1px solid color-mix(in srgb, #fff 7%, transparent);
}
.hx-tile .k { font: 500 clamp(7.5px, 1.15cqw, 11px) var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: #8d99b8; }
.hx-tile .v { font-size: clamp(13px, 2.3cqw, 21px); font-weight: 600; letter-spacing: -0.01em; font-variant-numeric: tabular-nums; }
.hx-tile .meter { display: block; height: 0.45cqw; min-height: 3px; border-radius: 99em; background: color-mix(in srgb, #fff 12%, transparent); overflow: hidden; }
.hx-tile .meter i { display: block; height: 100%; width: var(--w); border-radius: inherit; background: linear-gradient(90deg, var(--c-action), color-mix(in srgb, var(--c-action) 40%, #fff)); }

/* the wordmark sits low, behind everything */
.hx .bg-text { bottom: -7vw; font-size: 22vw; z-index: 1; opacity: 0.55; }

@media (max-width: 1100px) {
  .hero.hx { padding: 120px 24px 72px; }
  .hx-grid { grid-template-columns: minmax(0, 1fr); gap: 56px; }
  .hx-stage { max-width: 760px; }
}
@media (max-width: 1240px) {
  .hx-points li { padding: 0 14px; }
  .hx-points span { font-size: 12px; }
}
@media (max-width: 640px) {
  .hx-points { flex-direction: column; gap: 14px; margin-top: 32px; }
  .hx-points li { padding: 0; border-left: 0; }
  .hero .hx-title { font-size: clamp(48px, 15vw, 72px); }
  .hx-eyebrow { letter-spacing: 0.3em; }
}
@media (prefers-reduced-motion: reduce) { .mo .hx-link, .mo .hx-sheet { animation: none; } }


/* ── capture module: a dermatoscope readout, not a photo ── */
.hx-view-grid {
  position: absolute;
  inset: 0;
  border-radius: inherit;
  pointer-events: none;
  background-image:
    linear-gradient(color-mix(in srgb, var(--c-content) 7%, transparent) 1px, transparent 1px),
    linear-gradient(90deg, color-mix(in srgb, var(--c-content) 7%, transparent) 1px, transparent 1px);
  background-size: 2.6cqw 2.6cqw;
  -webkit-mask-image: radial-gradient(circle at 32% 54%, #000 0%, transparent 62%);
  mask-image: radial-gradient(circle at 32% 54%, #000 0%, transparent 62%);
}
.hx-view-head {
  position: absolute;
  left: 2.4cqw;
  top: 2.2cqw;
  display: flex;
  align-items: center;
  gap: 0.9cqw;
}
.hx-view-title {
  display: inline-flex;
  align-items: center;
  gap: 0.9cqw;
  margin-right: 0.6cqw;
  font: 500 clamp(9px, 1.3cqw, 12px) var(--mono);
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--c-content);
}
.hx-view-title i {
  width: 1cqw;
  height: 1cqw;
  min-width: 6px;
  min-height: 6px;
  border-radius: 50%;
  background: #e5484d;
  box-shadow: 0 0 0 0.5cqw color-mix(in srgb, #e5484d 22%, transparent);
}
.mo .hx-view-title i { animation: hx-rec 1.6s ease-in-out infinite; }
@keyframes hx-rec { 50% { opacity: 0.35; } }
.hx-badge {
  padding: 0.6cqw 1.2cqw;
  border-radius: 99em;
  font: 500 clamp(8.5px, 1.2cqw, 11.5px) var(--mono);
  white-space: nowrap;
  color: #fff;
  background: var(--smoke);
  box-shadow: var(--glass-shadow-sm);
}
.hx-badge--soft { color: var(--c-content); background: var(--glass-fill-strong); }

.hx-lens {
  position: absolute;
  left: calc(32% - 15cqw);
  top: calc(54% - 15cqw);
  width: 30cqw;
  height: 30cqw;
  border-radius: 50%;
  box-shadow: 0 2cqw 4cqw -1.4cqw rgba(27, 33, 56, 0.45), 0 0 0 0.7cqw color-mix(in srgb, #fff 55%, transparent);
}

.hx-view-foot {
  position: absolute;
  left: 2.4cqw;
  bottom: 2.2cqw;
  display: flex;
  gap: 0.8cqw;
}
.hx-check {
  display: inline-flex;
  align-items: center;
  gap: 0.7cqw;
  padding: 0.6cqw 1.2cqw;
  border-radius: 99em;
  font: 500 clamp(8px, 1.15cqw, 11px) var(--mono);
  white-space: nowrap;
  color: var(--c-content);
  background: var(--glass-fill-strong);
  -webkit-backdrop-filter: var(--glass-blur);
  backdrop-filter: var(--glass-blur);
  box-shadow: var(--glass-shadow-sm);
}
.hx-check i { width: 0.8cqw; height: 0.8cqw; min-width: 5px; min-height: 5px; border-radius: 50%; background: #2fbf71; }
.hx-check--site { color: #fff; background: color-mix(in srgb, var(--c-action) 84%, transparent); }

/* leader line now leaves the lens centre */
.hx-link {
  left: calc(66% * 0.32 + 3.6cqw);
  top: calc(22% + 68% * 0.54);
  width: calc(37% - 66% * 0.32 - 3.6cqw);
}


/* ============================================================
   DARK TERMINAL CARDS (after the Uiverse card by pharmacist-sabot)
   Deep navy face, hairline border, a grid that fades downward and
   drifts on hover, an accent glow in the top-right corner, and a
   springy lift with an accent ring. Used by the hero composition
   and the four module cards. Accent follows the page palette.
   ============================================================ */
body {
  --card-bg: #0e1324;
  --card-border: #1f2937;
  --card-text: #f3f4f6;
  --card-muted: #9ca3af;
  --card-glow: color-mix(in srgb, var(--c-action) 38%, transparent);
  /* ten layers, shaped like the glass lists so the hero morph can land on them */
  --card-shadow:
    inset 0 0 0 1px var(--card-border),
    inset 0 0 0 0 transparent, inset 0 0 0 0 transparent, inset 0 0 0 0 transparent,
    inset 0 0 0 0 transparent, inset 0 0 0 0 transparent, inset 0 0 0 0 transparent,
    inset 0 0 0 0 transparent,
    0 4px 24px -1px rgba(0, 0, 0, 0.2),
    0 0 0 0 transparent;
  --card-shadow-hover:
    inset 0 0 0 1px color-mix(in srgb, var(--c-action) 55%, transparent),
    inset 0 0 0 0 transparent, inset 0 0 0 0 transparent, inset 0 0 0 0 transparent,
    inset 0 0 0 0 transparent, inset 0 0 0 0 transparent, inset 0 0 0 0 transparent,
    inset 0 0 0 0 transparent,
    0 20px 40px -5px rgba(0, 0, 0, 0.4),
    0 0 0 1px color-mix(in srgb, var(--c-action) 30%, transparent);
}
@keyframes card-grid-move { to { background-position: 30px 30px; } }
@keyframes card-blink { 50% { opacity: 0; } }

/* the shared layers */
.card-fx {
  position: absolute;
  inset: 0;
  z-index: -1;
  border-radius: inherit;
  overflow: hidden;
  pointer-events: none;
}
.card-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 30px 30px;
  -webkit-mask-image: linear-gradient(to bottom, #000 40%, transparent 100%);
  mask-image: linear-gradient(to bottom, #000 40%, transparent 100%);
  opacity: 0.5;
  transition: opacity 0.5s ease;
}
.card-glow {
  position: absolute;
  top: -50px;
  right: -50px;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  background: radial-gradient(circle, var(--card-glow) 0%, transparent 70%);
  filter: blur(40px);
  transition: transform 0.5s ease, background 0.5s ease;
}
.dcard:hover .card-grid { opacity: 0.8; animation: card-grid-move 20s linear infinite; }
.dcard:hover .card-glow { transform: scale(1.5); background: radial-gradient(circle, color-mix(in srgb, var(--c-action) 45%, transparent) 0%, transparent 70%); }
@media (prefers-reduced-motion: reduce) { .dcard:hover .card-grid { animation: none; } }

/* text and glass inside a dark card read light */
.dcard {
  --c-content: var(--card-text);
  --text-muted: var(--card-muted);
  --glass-fill: rgba(255, 255, 255, 0.04);
  --glass-fill-strong: rgba(255, 255, 255, 0.08);
  isolation: isolate;
  color: var(--card-text);
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1), translate 0.3s cubic-bezier(0.34, 1.56, 0.64, 1),
    box-shadow 0.3s ease, border-color 0.3s ease;
}
.dcard:hover { transform: translateY(-4px) scale(1.01); }

/* ── hero composition ─────────────────────────────────────── */
.hx-stage > .dcard { background: var(--card-bg); box-shadow: var(--card-shadow); }
.hx-stage .m { --m-bg: var(--card-bg); --m-end: var(--card-shadow); }
.hx-stage .m:hover { --m-end: var(--card-shadow-hover); }
html:not(.mo) .hx-stage > .dcard:hover { box-shadow: var(--card-shadow-hover); }
.hx-stage .dcard:hover { z-index: 8; }
.hx-view, .hx-crop, .hx-console, .hx-results { border-radius: 2.2cqw; }
.hx-stage .card-glow { width: 18cqw; height: 18cqw; top: -6cqw; right: -6cqw; }
.hx-stage .card-grid { background-size: 3.6cqw 3.6cqw; }
.hx-view-head .hx-badge { background: rgba(255, 255, 255, 0.06); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: none; }
.hx-view-head .hx-badge--soft { color: #a99ffd; background: color-mix(in srgb, var(--c-action) 12%, transparent); border-color: color-mix(in srgb, var(--c-action) 28%, transparent); }
.hx-check { border-radius: 6px; background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.08); box-shadow: none; }
.hx-check--site { color: #a99ffd; background: color-mix(in srgb, var(--c-action) 12%, transparent); border-color: color-mix(in srgb, var(--c-action) 28%, transparent); }
.hx-lens { box-shadow: 0 2cqw 4cqw -1.4cqw rgba(0, 0, 0, 0.6), 0 0 0 0.5cqw rgba(255, 255, 255, 0.06); }
.hx-crop { padding: 2cqw; }
.hx-crop-inner svg { border-radius: 1cqw; }
.hx-console, .hx-results { background: var(--card-bg); }
.hx-code { background: rgba(255, 255, 255, 0.03); border-color: rgba(255, 255, 255, 0.07); }
.hx-tile { background: rgba(255, 255, 255, 0.03); border-color: rgba(255, 255, 255, 0.07); border-radius: 1.2cqw; }
.hx-sheet {
  border-radius: 2.2cqw;
  background: color-mix(in srgb, var(--card-bg) calc(78% - var(--k) * 14%), transparent);
  border: 1px solid color-mix(in srgb, var(--c-action) calc(34% - var(--k) * 7%), transparent);
  box-shadow: 0 8px 20px -8px rgba(0, 0, 0, 0.35);
}
.hx-sheet em { color: #a99ffd; }

/* ── module cards ─────────────────────────────────────────── */
.mcard.dcard,
.mcard--new.dcard {
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  border-radius: 16px;
  box-shadow: 0 4px 24px -1px rgba(0, 0, 0, 0.2);
  -webkit-backdrop-filter: none;
  backdrop-filter: none;
  padding: 20px;
}
.mcard.dcard:hover {
  translate: none;
  border-color: color-mix(in srgb, var(--c-action) 55%, transparent);
  box-shadow: 0 20px 40px -5px rgba(0, 0, 0, 0.4), 0 0 0 1px color-mix(in srgb, var(--c-action) 30%, transparent);
}
.mcard.dcard::after { display: none; }
.mcard .mcard-kicker { color: var(--card-muted); }
.mcard .mcard-chip {
  border-radius: 8px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: none;
  color: var(--card-text);
}
.mcard .mcard-chip--new { color: #a99ffd; background: color-mix(in srgb, var(--c-action) 12%, transparent); border-color: color-mix(in srgb, var(--c-action) 30%, transparent); }
.mcard .mcard-stage {
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.025);
  border: 1px solid rgba(255, 255, 255, 0.06);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.04);
}
.mcard .mcard-body h3 {
  display: flex;
  align-items: center;
  font: 500 22px/1.2 var(--mono);
  letter-spacing: -0.02em;
  color: var(--card-text);
}
.mcard .mcard-body h3::after {
  content: "";
  width: 10px;
  height: 3px;
  margin-left: 6px;
  align-self: flex-end;
  margin-bottom: 6px;
  background: var(--c-action);
  box-shadow: 0 0 8px var(--c-action);
  animation: card-blink 1s step-end infinite;
}
@media (prefers-reduced-motion: reduce) { .mcard .mcard-body h3::after { animation: none; } }
.mcard .mcard-body p { color: var(--card-muted); font-size: 14.5px; }
.mcard .mcard-caps li {
  padding: 4px 10px;
  border-radius: 6px;
  font: 600 12px var(--mono);
  color: #a99ffd;
  background: color-mix(in srgb, var(--c-action) 10%, transparent);
  border: 1px solid color-mix(in srgb, var(--c-action) 22%, transparent);
  box-shadow: none;
  transition: background-color 0.3s ease, box-shadow 0.3s ease, translate 0.3s ease;
}
.mcard .mcard-caps li:nth-child(2) {
  color: #8abdff;
  background: rgba(138, 189, 255, 0.1);
  border-color: rgba(138, 189, 255, 0.22);
}
.mcard .mcard-caps li:hover { translate: 0 -1px; background: color-mix(in srgb, var(--c-action) 20%, transparent); box-shadow: 0 0 12px color-mix(in srgb, var(--c-action) 30%, transparent); }
.mcard .mcard-caps li:nth-child(2):hover { background: rgba(138, 189, 255, 0.2); box-shadow: 0 0 12px rgba(138, 189, 255, 0.3); }
.mcard .mcard-foot { border-top-color: rgba(255, 255, 255, 0.08); color: var(--card-muted); }
.mcard .gswitch { background: rgba(255, 255, 255, 0.08); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08); }
.mcard .gswitch[aria-checked="true"] { background: var(--c-action); box-shadow: 0 0 14px color-mix(in srgb, var(--c-action) 45%, transparent); }
.mcard .viz-brackets { stroke: #f3f4f6; }
.mcard .viz-score, .mcard .viz-tag, .mcard .sync-chips span {
  background: rgba(12, 17, 29, 0.72);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: none;
  color: var(--card-text);
}
.mcard .viz-score circle { stroke: rgba(255, 255, 255, 0.14); }
.mcard .viz-score .arc { stroke: var(--c-action); }
.mcard .q-row { background: rgba(255, 255, 255, 0.04); border: 1px solid rgba(255, 255, 255, 0.07); box-shadow: none; border-radius: 10px; }
.mcard .q-row.is-top { background: rgba(255, 255, 255, 0.08); border-color: color-mix(in srgb, var(--c-action) 35%, transparent); }
.mcard .sync-node { background: rgba(255, 255, 255, 0.06); border: 1px solid rgba(255, 255, 255, 0.12); box-shadow: none; }
.mcard .sync-node--ehr { background: var(--c-action); color: #fff; border-color: transparent; }
.mcard .bars { border-bottom-color: rgba(255, 255, 255, 0.1); }
.mcard .bars i { background: rgba(255, 255, 255, 0.12); }
.mcard .bars i:last-child { background: var(--c-action); box-shadow: 0 0 14px color-mix(in srgb, var(--c-action) 60%, transparent); }
.mcard .chart-head em { color: #45d88a; }


/* Instrument Serif ships one weight; never let a heading synthesize bold */
h1, h2, .section-title, .platform-title, .plan-title, .consult-copy h2 { font-weight: 400 !important; font-synthesis: none; }

/* every display headline in the serif, whatever older rule targets it */
:is(h1, h2).section-title, h2.platform-title, .consult-copy h2, h3.plan-title, .hero .hx-title,
:is(h1, h2).section-title span, h2.platform-title span, .consult-copy h2 span, .hero .hx-title span {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-style: italic;
  font-weight: 400;
  text-transform: uppercase;
}

/* ============================================================
   TYPE: Funnel Display throughout, in the reference's weights.
   800 tight for headlines (sentence case, upright), 700 for
   card titles, 600 for buttons, 500 for UI, 400 muted for body.
   JetBrains Mono stays for code and technical labels only.
   ============================================================ */
body, button, input, select, textarea { font-family: "Funnel Display", system-ui, sans-serif; }
body { letter-spacing: -0.005em; -webkit-font-smoothing: antialiased; }

h1, h2, .plan-title, .menu-links .label,
:is(h1, h2).section-title, h2.platform-title, .consult-copy h2, h3.plan-title, .hero .hx-title,
:is(h1, h2, .section-title, .platform-title, .plan-title, .hx-title) :is(span, em, strong),
.consult-copy h2 span {
  font-family: "Funnel Display", system-ui, sans-serif !important;
  font-style: normal !important;
  font-weight: 800 !important;
  text-transform: none !important;
  letter-spacing: -0.045em !important;
  font-synthesis: none;
}
.hero .hx-title { font-size: clamp(44px, 5vw, 84px); line-height: 1.0; margin-bottom: 24px; }
.hero .hx-title span { color: var(--text-muted); opacity: 1; }
@media (max-width: 640px) { .hero .hx-title { font-size: clamp(40px, 11.4vw, 60px); } }
:is(h1, h2).section-title { font-size: clamp(34px, 3.8vw, 56px); line-height: 1.02; }
h2.platform-title { font-size: clamp(38px, 4.6vw, 68px); line-height: 1.0; }
.consult-copy h2 { font-size: clamp(34px, 3.6vw, 52px); line-height: 1.02; }
h3.plan-title { font-size: clamp(32px, 3.2vw, 46px); line-height: 1.02; }
.menu-links .label { font-size: clamp(30px, min(4.4vw, 6.6vh), 60px); line-height: 1.02; }

h3, .flow-step h3, .step-card h3, .product-info h3, .faq-q, .mcard-body h3 { font-weight: 700; letter-spacing: -0.025em; }
.flow-step h3 { font-size: 26px; }
.step-card h3 { font-size: 20px; }
.btn, .btn-glass, .nav-cta, .plan-tab, .pipebar-flow .chip-mod { font-weight: 600; letter-spacing: -0.005em; }
.btn-glass { font-family: "Funnel Display", system-ui, sans-serif; font-size: 14.5px; }
.hero-lede, .section-sub, .platform-sub, .plan-desc, .flow-step p, .step-card p, .faq-a p, .mcard-body p, .start-copy p {
  font-weight: 400;
  letter-spacing: -0.005em;
}
.hx-points strong { font-weight: 700; letter-spacing: -0.02em; }
.stat-num, .flow-metric strong, .big-figure .display, .hx-tile .v { font-weight: 800; letter-spacing: -0.04em; }
.review-card blockquote, .quote blockquote { font-family: "Funnel Display", system-ui, sans-serif; font-weight: 500; font-style: normal; letter-spacing: -0.015em; }

/* wordmark */
.site-nav .logo, .footer-brand .logo {
  font-family: "Funnel Display", system-ui, sans-serif;
  font-style: normal;
  font-weight: 800;
  font-size: 19px;
  letter-spacing: -0.02em;
  text-transform: uppercase;
}
.bg-text { font-family: "Funnel Display", system-ui, sans-serif; font-weight: 800; letter-spacing: -0.06em; }

/* the module-card titles keep the terminal mono + cursor from the card style */
.mcard .mcard-body h3 { font: 500 22px/1.2 var(--mono); letter-spacing: -0.02em; }

/* ── intake + crop: an agent brief, not a photo ── */
.hx-intent {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 0.35em;
  padding: 0 1.4cqw;
  border-radius: 1cqw;
  background: #0b1020;
  border: 1px solid rgba(255, 255, 255, 0.08);
  font: 500 clamp(7.5px, 1.32cqw, 12.5px)/1.3 var(--mono);
  color: #c8d0e7;
  white-space: nowrap;
  overflow: hidden;
}
.hx-intent .ln.in { padding-left: 1.2em; }
.hx-intent i { font-style: normal; color: #8d99b8; }
.hx-intent b { font-weight: 500; color: #93b2ff; }
.hx-intent em { font-style: normal; color: #8fe0b4; }
.hx-intent .hl {
  margin-left: -0.4em;
  padding: 0.3em 0.4em 0.3em 1.6em;
  border-radius: 0.5em;
  background: color-mix(in srgb, var(--c-action) 26%, transparent);
  outline: 1.2px dashed color-mix(in srgb, #fff 70%, transparent);
  outline-offset: 2px;
}

/* ── Agent Runtime card: a live step trace ── */
.viz-trace { width: 100%; display: grid; gap: 7px; position: relative; padding-left: 4px; }
.viz-trace::before {
  content: "";
  position: absolute;
  left: 9.5px;
  top: 14px;
  bottom: 14px;
  width: 1.5px;
  background: linear-gradient(var(--c-action), color-mix(in srgb, var(--c-action) 20%, transparent));
}
.tr-row {
  position: relative;
  display: grid;
  grid-template-columns: 12px minmax(0, 1fr) auto;
  align-items: center;
  gap: 10px;
  padding: 6px 10px 6px 0;
  font: 12px var(--mono);
  color: #c8d0e7;
}
.tr-dot { width: 12px; height: 12px; border-radius: 50%; background: #0e1324; border: 1.5px solid var(--c-action); }
.tr-row.done .tr-dot { background: var(--c-action); box-shadow: 0 0 8px color-mix(in srgb, var(--c-action) 55%, transparent); }
.tr-row.live { border-radius: 8px; background: rgba(255, 255, 255, 0.05); border: 1px solid color-mix(in srgb, var(--c-action) 30%, transparent); margin-left: -4px; padding-left: 4px; }
.tr-row.live .tr-dot { animation: tr-pulse 1.4s ease-in-out infinite; }
@keyframes tr-pulse { 50% { box-shadow: 0 0 0 4px color-mix(in srgb, var(--c-action) 25%, transparent); } }
@media (prefers-reduced-motion: reduce) { .tr-row.live .tr-dot { animation: none; } }
.tr-step { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.tr-t { color: #8d99b8; font-size: 11px; }
.mcard .viz-score { top: 10px; right: 10px; }
.mcard-stage:has(.viz-trace) { place-items: center stretch; padding-top: 40px; padding-bottom: 40px; }

.hx-link {
  left: calc(66% * 0.32 + 6.4cqw);
  width: calc(37% - 66% * 0.32 - 6.4cqw);
}
.mcard-stage:has(.viz-trace) { padding-top: 50px; padding-bottom: 14px; }
.mcard-stage:has(.viz-trace) .viz-tag { top: 12px; bottom: auto; left: 12px; }
.viz-trace { gap: 4px; }
.tr-row { padding-top: 5px; padding-bottom: 5px; }

/* ── routine picker: a glass listbox in place of the native select ── */
.consult-card { overflow: visible; z-index: 30; }
.field-label { font-size: 12px; font-weight: 500; color: rgba(255, 255, 255, 0.6); }
.rpick { position: relative; }
.rpick-trigger {
  width: 100%;
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto;
  align-items: center;
  gap: 14px;
  padding: 10px 16px 10px 10px;
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.06), rgba(255, 255, 255, 0.02)), rgba(0, 0, 0, 0.3);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -2px 6px rgba(0, 0, 0, 0.35), 0 8px 20px -12px rgba(0, 0, 0, 0.6);
  color: #fff;
  font: inherit;
  text-align: left;
  cursor: pointer;
  transition: border-color 0.25s ease, box-shadow 0.25s ease, background-color 0.25s ease;
}
.rpick-trigger:hover { border-color: rgba(255, 255, 255, 0.2); }
.rpick-trigger:focus-visible, .rpick.open .rpick-trigger {
  outline: none;
  border-color: color-mix(in srgb, var(--c-action) 70%, transparent);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), 0 0 0 4px color-mix(in srgb, var(--c-action) 22%, transparent), 0 12px 28px -14px color-mix(in srgb, var(--c-action) 70%, transparent);
}
.rpick.invalid .rpick-trigger { border-color: #ff8a8f; box-shadow: 0 0 0 4px rgba(255, 99, 105, 0.18); }

.rpick-ico {
  width: 40px;
  height: 40px;
  flex-shrink: 0;
  display: grid;
  place-items: center;
  border-radius: 13px;
  color: #fff;
  background: linear-gradient(160deg, color-mix(in srgb, var(--c-action) 95%, #fff 10%), color-mix(in srgb, var(--c-action) 80%, #000 20%));
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.35), 0 6px 14px -6px color-mix(in srgb, var(--c-action) 80%, transparent);
}
.rpick-ico--empty { color: rgba(255, 255, 255, 0.7); background: rgba(255, 255, 255, 0.06); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.12); }
.rpick-ico svg, .rpick-chev svg, .rpick-check svg {
  width: 20px;
  height: 20px;
  fill: none;
  stroke: currentColor;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.rpick-text { min-width: 0; display: grid; gap: 2px; }
.rpick-name { font-size: 15.5px; font-weight: 600; letter-spacing: -0.01em; color: #fff; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.rpick-desc { font-size: 12.5px; color: rgba(255, 255, 255, 0.55); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.rpick-chev {
  width: 30px;
  height: 30px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  color: rgba(255, 255, 255, 0.8);
  background: rgba(255, 255, 255, 0.06);
  transition: rotate 0.35s var(--m-ease), background-color 0.2s;
}
.rpick-chev svg { width: 16px; height: 16px; }
.rpick.open .rpick-chev { rotate: 180deg; background: color-mix(in srgb, var(--c-action) 30%, transparent); }

.rpick-list {
  position: absolute;
  z-index: 40;
  left: 0;
  right: 0;
  top: calc(100% + 10px);
  margin: 0;
  padding: 8px;
  list-style: none;
  border-radius: 22px;
  background: color-mix(in srgb, #0e1324 96%, transparent);
  -webkit-backdrop-filter: blur(22px) saturate(160%);
  backdrop-filter: blur(22px) saturate(160%);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), 0 30px 60px -20px rgba(0, 0, 0, 0.65), 0 0 0 1px color-mix(in srgb, var(--c-action) 18%, transparent);
  transform-origin: top center;
  outline: none;
}
.rpick.open .rpick-list { animation: rpick-in 0.32s var(--m-ease); }
.rpick.closing .rpick-list { animation: rpick-out 0.18s ease forwards; }
@keyframes rpick-in { from { opacity: 0; transform: translateY(-6px) scale(0.97); } }
@keyframes rpick-out { to { opacity: 0; transform: translateY(-4px) scale(0.98); } }
.rpick-list li {
  display: grid;
  grid-template-columns: auto minmax(0, 1fr) auto 20px;
  align-items: center;
  gap: 12px;
  padding: 9px 12px 9px 9px;
  border-radius: 15px;
  cursor: pointer;
  transition: background-color 0.18s ease;
}
.rpick-list li .rpick-ico { width: 36px; height: 36px; border-radius: 11px; color: rgba(255, 255, 255, 0.85); background: rgba(255, 255, 255, 0.06); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08); transition: background 0.2s, box-shadow 0.2s, color 0.2s; }
.rpick-list li .rpick-ico svg { width: 18px; height: 18px; }
.rpick-list li.active { background: rgba(255, 255, 255, 0.07); }
.rpick-list li.active .rpick-ico,
.rpick-list li[aria-selected="true"] .rpick-ico {
  color: #fff;
  background: linear-gradient(160deg, color-mix(in srgb, var(--c-action) 95%, #fff 10%), color-mix(in srgb, var(--c-action) 80%, #000 20%));
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.35), 0 6px 14px -6px color-mix(in srgb, var(--c-action) 80%, transparent);
}
.rpick-meta {
  padding: 3px 8px;
  border-radius: 6px;
  font: 500 11px var(--mono);
  color: #a99ffd;
  background: color-mix(in srgb, var(--c-action) 12%, transparent);
  border: 1px solid color-mix(in srgb, var(--c-action) 26%, transparent);
  white-space: nowrap;
}
.rpick-check { color: #fff; opacity: 0; transform: scale(0.6); transition: opacity 0.2s, transform 0.3s var(--m-ease); }
.rpick-check svg { width: 18px; height: 18px; stroke-width: 2.2; }
.rpick-list li[aria-selected="true"] .rpick-check { opacity: 1; transform: none; color: #a99ffd; }
.rpick-error { margin: 8px 0 0 4px; font-size: 12.5px; color: #ff9ea2; }
@media (max-width: 520px) { .rpick-meta { display: none; } .rpick-list li { grid-template-columns: auto minmax(0, 1fr) 20px; } }
@media (prefers-reduced-motion: reduce) { .rpick.open .rpick-list, .rpick.closing .rpick-list { animation: none; } .rpick-chev { transition: none; } }

.rpick-list .rpick-desc { white-space: normal; overflow: visible; }

/* ── hero: static cards (no loading morph) ── */
.hx-stage > .dcard { position: absolute; }
.hx-stage > .dcard:hover { box-shadow: var(--card-shadow-hover); }
.mo .hx-sheet { animation: none; }

/* ── intake graphic (after the Uiverse chip by Vosoone) ── */
.hx-chipwrap {
  position: absolute;
  left: 1.6cqw;
  top: 50%;
  translate: 0 -44%;
  width: 54cqw;
  pointer-events: none;
}
.hx-chip-svg { display: block; width: 100%; height: auto; overflow: visible; }
.hx-chip-svg .trace-bg { stroke: #333; stroke-width: 1.8; fill: none; }
.hx-chip-svg .trace-flow {
  stroke-width: 1.8;
  fill: none;
  stroke-dasharray: 40 400;
  stroke-dashoffset: 438;
  filter: drop-shadow(0 0 6px currentColor);
  animation: hx-flow 3s cubic-bezier(0.5, 0, 0.9, 1) infinite;
}
.hx-chip-svg .yellow { stroke: #ffea00; color: #ffea00; }
.hx-chip-svg .blue { stroke: #00ccff; color: #00ccff; }
.hx-chip-svg .green { stroke: #00ff15; color: #00ff15; }
.hx-chip-svg .purple { stroke: #9900ff; color: #9900ff; }
.hx-chip-svg .red { stroke: #ff3300; color: #ff3300; }
@keyframes hx-flow { to { stroke-dashoffset: 0; } }
.hx-chip-svg text { font-weight: bold; letter-spacing: 1px; }
@media (prefers-reduced-motion: reduce) { .hx-chip-svg .trace-flow { animation: none; stroke-dasharray: none; opacity: 0.5; } }

/* ── module graphics: the circuit system from the intake chip ── */
.mcard .mcard-stage { padding: 10px 6px; place-items: center; }
.mc-svg { display: block; width: 100%; height: 100%; max-height: 172px; overflow: visible; }
.mc-bg { stroke: #333; stroke-width: 1.8; fill: none; }
.mc-flow {
  stroke-width: 1.8;
  fill: none;
  stroke-dasharray: 16 120;
  stroke-dashoffset: 136;
  filter: drop-shadow(0 0 5px currentColor);
  animation: mc-flow 3s cubic-bezier(0.5, 0, 0.9, 1) infinite;
}
@keyframes mc-flow { to { stroke-dashoffset: 0; } }
.mc-pad { fill: #05070d; stroke: #444; stroke-width: 1.2; }
.mc-label { font: 500 10px "JetBrains Mono", ui-monospace, monospace; fill: #8d99b8; letter-spacing: 0.02em; }
.mc-chip-text { font: 700 10.5px "Funnel Display", system-ui, sans-serif; letter-spacing: 1px; fill: #e2e2e2; }
.mcard:hover .mc-pad { stroke: #666; }
@media (prefers-reduced-motion: reduce) { .mc-flow { animation: none; stroke-dasharray: none; opacity: 0.45; } }

/* ── footer: one dark terminal panel, no oversized wordmark ── */
.site-footer.fx-footer {
  margin-top: 0;
  padding: 24px 24px calc(24px + env(safe-area-inset-bottom, 0px));
  background: none;
  box-shadow: none;
  -webkit-backdrop-filter: none;
  backdrop-filter: none;
}
.ft-card {
  position: relative;
  max-width: 1280px;
  margin: 0 auto;
  padding: 56px 56px 28px;
  border-radius: 28px;
  background: var(--card-bg);
  border: 1px solid var(--card-border);
  box-shadow: 0 30px 60px -30px rgba(10, 13, 30, 0.55);
  overflow: hidden;
}
.ft-card:hover { transform: none; }
.ft-card .card-glow { width: 420px; height: 420px; top: -180px; right: -120px; filter: blur(70px); }
.ft-top { display: grid; grid-template-columns: minmax(0, 1.1fr) minmax(0, 1.4fr); gap: 48px 64px; }
.ft-brand { display: grid; gap: 18px; align-content: start; justify-items: start; }
.ft-logo {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  color: #fff;
  text-decoration: none;
  font: 800 20px "Funnel Display", system-ui, sans-serif;
  letter-spacing: -0.02em;
}
.ft-logo svg { width: 22px; height: 22px; fill: var(--c-action); }
.ft-brand p { max-width: 30em; font-size: 15px; line-height: 1.6; color: var(--card-muted); }
.ft-status {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 8px 14px;
  border-radius: 99em;
  font-size: 13px;
  font-weight: 500;
  color: var(--card-text);
  text-decoration: none;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: border-color 0.2s;
}
.ft-status:hover { border-color: rgba(47, 212, 122, 0.45); }
.ft-dot { width: 8px; height: 8px; border-radius: 50%; background: #2fd47a; box-shadow: 0 0 0 4px rgba(47, 212, 122, 0.18), 0 0 10px #2fd47a; }
.ft-status-meta { font: 11px var(--mono); color: var(--card-muted); }
.ft-cols { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 32px; }
.ft-col { display: grid; gap: 12px; align-content: start; }
.ft-col h4 { margin: 0 0 6px; font: 500 11px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--card-muted); }
.ft-col a {
  width: fit-content;
  font-size: 15px;
  color: #d4d8e4;
  text-decoration: none;
  transition: color 0.2s, translate 0.25s var(--m-ease);
}
.ft-col a:hover { color: #fff; translate: 3px 0; }

.ft-cta {
  margin-top: 48px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 16px 24px;
  padding: 18px 18px 18px 24px;
  border-radius: 18px;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.08);
}
.ft-cta div { display: grid; gap: 2px; }
.ft-cta strong { font-size: 18px; font-weight: 700; letter-spacing: -0.02em; color: #fff; }
.ft-cta span { font-size: 14px; color: var(--card-muted); }

.ft-bottom {
  margin-top: 28px;
  padding-top: 22px;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-between;
  gap: 14px 24px;
  font-size: 13px;
  color: var(--card-muted);
}
.ft-regions { display: flex; flex-wrap: wrap; gap: 6px; }
.ft-regions i {
  font: normal 11px var(--mono);
  padding: 3px 8px;
  border-radius: 6px;
  color: #a99ffd;
  background: color-mix(in srgb, var(--c-action) 10%, transparent);
  border: 1px solid color-mix(in srgb, var(--c-action) 22%, transparent);
}
.ft-legal { display: flex; flex-wrap: wrap; gap: 18px; }
.ft-legal a { color: var(--card-muted); text-decoration: none; transition: color 0.2s; }
.ft-legal a:hover { color: #fff; }

@media (max-width: 960px) {
  .ft-card { padding: 40px 28px 24px; }
  .ft-top { grid-template-columns: minmax(0, 1fr); }
}
@media (max-width: 560px) {
  .site-footer.fx-footer { padding-inline: 12px; }
  .ft-card { padding: 32px 22px 22px; border-radius: 24px; }
  .ft-cols { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .ft-bottom { flex-direction: column; align-items: flex-start; }
}

.mc-label { font-size: 11.5px; }
.mc-chip-text { font-size: 12px; }
.mc-svg { max-height: none; }

/* ── four circuit concepts ── */
.mc-loop {
  stroke-width: 2;
  fill: none;
  stroke-dasharray: 9 41;
  filter: drop-shadow(0 0 5px currentColor);
  animation: mc-loop 3.2s linear infinite;
}
@keyframes mc-loop { from { stroke-dashoffset: 100; } to { stroke-dashoffset: 0; } }
.mc-flow.fast { animation-duration: 1.8s; }
.mc-flow.slow { animation-duration: 4.2s; }
.mc-lit { fill: none; stroke-width: 1.8; opacity: 0.55; filter: drop-shadow(0 0 4px currentColor); }
.mc-node { fill: #333; }
.mc-node.on { fill: #777; }
.mc-pad.lit { fill: currentColor; filter: drop-shadow(0 0 5px currentColor); }
.mc-label.on { fill: #e6f9ff; }
.mc-label.dim { fill: #5f6b86; font-size: 10px; }
.mc-cell { fill: #2fd47a; opacity: 0.55; }
.mc-big { font: 800 22px "Funnel Display", system-ui, sans-serif; fill: #f3f4f6; letter-spacing: -0.03em; }
.mc-up { fill: #45d88a; }
.mcard .mcard-stage { padding: 12px 10px; }
@media (prefers-reduced-motion: reduce) { .mc-loop { animation: none; } }

/* regions bar: the stacked tablet/mobile layout at every width */
.platform-foot {
  display: grid;
  justify-items: start;
  gap: 14px;
  padding: 22px 24px;
  border-radius: 28px;
}
.platform-foot .region-chips { gap: 8px; }
</style>
<svg width="0" height="0" style="position: absolute" aria-hidden="true">
  <symbol id="dx-mark" viewBox="0 0 338.3 330">
    <path d="M75.8,182.2h30.6v-32.5c0-23.6,19.1-43.3,43.3-43.3h33.8v-30.6h-76.5V0h-30.6v75.2H0v30.6h75.2v76.5h.6Z" />
    <path d="M265,76.5h-51.6v30.6h51.6c23.6,0,43.3,19.1,43.3,43.3v105.8c0,23.6-19.1,43.3-43.3,43.3H106.4v-85.4h-30.6v116h189.2c40.8,0,73.3-33.1,73.3-73.3v-105.8c0-41.4-33.1-74.5-73.3-74.5Z" />
  </symbol>
</svg>

<div class="ambient" aria-hidden="true"><i></i><i></i><i></i><i></i></div>
<svg class="svg-defs" aria-hidden="true"><filter id="switcher" primitiveUnits="objectBoundingBox">
        <feImage result="map" width="100%" height="100%" x="0" y="0" href="data:image/webp;base64,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" />

        <feGaussianBlur in="SourceGraphic" stdDeviation="0.04" result="blur" />
        <feDisplacementMap id="disp" in="blur" in2="map" scale="0.5" xChannelSelector="R" yChannelSelector="G">
        </feDisplacementMap>
      </filter></svg>

<header class="site-nav" data-section="nav">
  <a class="logo" href="#top" data-close aria-label="Dermexcel, back to top">
    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 338.3 330" aria-hidden="true"><use href="#dx-mark"></use></svg>
    DERMEXCEL
  </a>
  <div class="nav-actions">
    <a class="nav-cta" href="#consult" data-close>Get a sandbox key</a>
    <button class="burger" type="button" aria-expanded="false" aria-controls="site-menu" aria-label="Open menu">
      <span></span><span></span>
    </button>
  </div>
</header>

<div class="menu" id="site-menu" data-section="menu" role="dialog" aria-modal="true" aria-label="Site menu" inert>
  <div class="menu-inner">
    <nav aria-label="Primary">
      <ul class="menu-links">
        <li style="--i: 0"><a href="#platform" data-close><span class="idx">01</span><span class="label">Platform</span><span class="hint">Cleanse, treat, protect</span></a></li>
        <li style="--i: 1"><a href="#products" data-close><span class="idx">02</span><span class="label">Modules</span><span class="hint">Four, one control plane</span></a></li>
        <li style="--i: 2"><a href="#science" data-close><span class="idx">03</span><span class="label">How it works</span><span class="hint">Brief to finished task</span></a></li>
        <li style="--i: 3"><a href="#plans" data-close><span class="idx">04</span><span class="label">Routines</span><span class="hint">Templates you can fork</span></a></li>
        <li style="--i: 4"><a href="#reviews" data-close><span class="idx">05</span><span class="label">Customers</span><span class="hint">4.2M runs a month</span></a></li>
        <li style="--i: 5"><a href="#faq" data-close><span class="idx">06</span><span class="label">Docs</span><span class="hint">Auth, limits, data, SLA</span></a></li>
        <li style="--i: 6"><a href="#consult" data-close><span class="idx">07</span><span class="label">Pricing</span><span class="hint">Start on a sandbox key</span></a></li>
      </ul>
    </nav>

    <aside class="menu-aside">
      <div class="menu-card pane" style="--i: 2">
        <span class="menu-kicker">Sandbox access</span>
        <p class="menu-lead">10,000 free agent runs and the quickstart for your stack. No sales call.</p>
        <a class="nav-cta" href="#consult" data-close>Get a sandbox key →</a>
      </div>
      <div class="menu-card pane" style="--i: 3">
        <span class="menu-kicker">Appearance</span>
        <fieldset class="switcher" data-component="theme-switcher">
          <legend class="switcher__legend">Choose theme</legend>
          <label class="switcher__option" title="Light">
            <input class="switcher__input" type="radio" name="theme" value="light" c-option="1" checked />
            <svg class="switcher__icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 36 36" aria-hidden="true">
              <path fill="var(--c)" fill-rule="evenodd" d="M18 12a6 6 0 1 1 0 12 6 6 0 0 1 0-12Zm0 2a4 4 0 1 0 0 8 4 4 0 0 0 0-8Z" clip-rule="evenodd" />
              <path fill="var(--c)" d="M17 6.038a1 1 0 1 1 2 0v3a1 1 0 0 1-2 0v-3ZM24.244 7.742a1 1 0 1 1 1.618 1.176L24.1 11.345a1 1 0 1 1-1.618-1.176l1.763-2.427ZM29.104 13.379a1 1 0 0 1 .618 1.902l-2.854.927a1 1 0 1 1-.618-1.902l2.854-.927ZM29.722 20.795a1 1 0 0 1-.619 1.902l-2.853-.927a1 1 0 1 1 .618-1.902l2.854.927ZM25.862 27.159a1 1 0 0 1-1.618 1.175l-1.763-2.427a1 1 0 1 1 1.618-1.175l1.763 2.427ZM19 30.038a1 1 0 0 1-2 0v-3a1 1 0 1 1 2 0v3ZM11.755 28.334a1 1 0 0 1-1.618-1.175l1.764-2.427a1 1 0 1 1 1.618 1.175l-1.764 2.427ZM6.896 22.697a1 1 0 1 1-.618-1.902l2.853-.927a1 1 0 1 1 .618 1.902l-2.853.927ZM6.278 15.28a1 1 0 1 1 .618-1.901l2.853.927a1 1 0 1 1-.618 1.902l-2.853-.927ZM10.137 8.918a1 1 0 0 1 1.618-1.176l1.764 2.427a1 1 0 0 1-1.618 1.176l-1.764-2.427Z" />
            </svg>
          </label>
          <label class="switcher__option" title="Dark">
            <input class="switcher__input" type="radio" name="theme" value="dark" c-option="2" />
            <svg class="switcher__icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 36 36" aria-hidden="true">
              <path fill="var(--c)" d="M12.5 8.473a10.968 10.968 0 0 1 8.785-.97 7.435 7.435 0 0 0-3.737 4.672l-.09.373A7.454 7.454 0 0 0 28.732 20.4a10.97 10.97 0 0 1-5.232 7.125l-.497.27c-5.014 2.566-11.175.916-14.234-3.813l-.295-.483C5.53 18.403 7.13 11.93 12.017 8.77l.483-.297Zm4.234.616a8.946 8.946 0 0 0-2.805.883l-.429.234A9 9 0 0 0 10.206 22.5l.241.395A9 9 0 0 0 22.5 25.794l.416-.255a8.94 8.94 0 0 0 2.167-1.990 9.433 9.433 0 0 1-2.782-.313c-5.043-1.352-8.036-6.535-6.686-11.578l.147-.491c.242-.745.573-1.440.972-2.078Z" />
            </svg>
          </label>
          <label class="switcher__option" title="Dim">
            <input class="switcher__input" type="radio" name="theme" value="dim" c-option="3" />
            <svg class="switcher__icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 36 36" aria-hidden="true">
              <path fill="var(--c)" d="M5 21a1 1 0 0 1 1-1h24a1 1 0 1 1 0 2H6a1 1 0 0 1-1-1ZM12 25a1 1 0 0 1 1-1h10a1 1 0 1 1 0 2H13a1 1 0 0 1-1-1ZM15 29a1 1 0 0 1 1-1h4a1 1 0 1 1 0 2h-4a1 1 0 0 1-1-1ZM18 13a6 6 0 0 1 5.915 7h-2.041A4.005 4.005 0 0 0 18 15a4 4 0 0 0-3.874 5h-2.041A6 6 0 0 1 18 13ZM17 7.038a1 1 0 1 1 2 0v3a1 1 0 0 1-2 0v-3ZM24.244 8.742a1 1 0 1 1 1.618 1.176L24.1 12.345a1 1 0 1 1-1.618-1.176l1.763-2.427ZM29.104 14.379a1 1 0 0 1 .618 1.902l-2.854.927a1 1 0 1 1-.618-1.902l2.854-.927ZM6.278 16.28a1 1 0 1 1 .618-1.901l2.853.927a1 1 0 1 1-.618 1.902l-2.853-.927ZM10.137 9.918a1 1 0 0 1 1.618-1.176l1.764 2.427a1 1 0 0 1-1.618 1.176l-1.764-2.427Z" />
            </svg>
          </label>
        </fieldset>
      </div>
      <div class="menu-card pane" style="--i: 4">
        <span class="menu-kicker">Status</span>
        <p class="menu-status"><span class="live-dot" aria-hidden="true"></span>All systems normal</p>
        <p class="menu-meta">API v2.4 · 99.98% uptime, trailing 90 days</p>
        <p class="menu-social"><a href="#top" data-close>X</a><a href="#top" data-close>LinkedIn</a><a href="#top" data-close>GitHub</a></p>
      </div>
    </aside>
  </div>
</div>


<section class="hero hx" data-section="hero">
  <div class="bg-text gsap-bg-text" aria-hidden="true">DERMEXCEL</div>

  <div class="hx-grid">
    <div class="hx-copy">
      <h1 class="hx-title gsap-hero">Clean agents.<br>Visible results.<br><span>In a single<br>API call.</span></h1>
      <p class="hero-lede gsap-hero">Dermexcel briefs, runs and reviews AI agents the way a good routine works: a few well-chosen tools, applied in order, with every step traced so you can see exactly what each one did.</p>

      <div class="hero-actions gsap-hero">
        <div class="btn-wrapper">
          <button class="btn" data-target="#consult" data-label="Generate" data-label-busy="Generating">
            <svg class="btn-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.090-3.090L2.250 12l2.846-.813a4.5 4.5 0 0 0 3.090-3.090L9 5.250l.813 2.846a4.5 4.5 0 0 0 3.090 3.090L15.750 12l-2.846.813a4.5 4.5 0 0 0-3.090 3.090ZM18.259 8.715 18 9.750l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.250 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.250l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.750 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.500 21.750l-.394-1.183a2.250 2.250 0 0 0-1.423-1.423L13.500 18.750l1.183-.394a2.250 2.250 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.250 2.250 0 0 0 1.423 1.423l1.183.394-1.183.394a2.250 2.250 0 0 0-1.423 1.423Z"></path>
            </svg>
            <span class="txt-wrapper">
              <span class="txt-1">Generate</span>
              <span class="txt-2">Generating</span>
            </span>
          </button>
        </div>
        <button class="btn-glass" data-target="#faq">Read the docs →</button>
      </div>

      <ul class="hx-points gsap-hero">
        <li>
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M13 2 4.5 13.5H11L10 22l8.5-11.5H12L13 2Z"></path></svg>
          <span><strong>~200 ms</strong>Time to first step</span>
        </li>
        <li>
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 3l7.5 3v5.5c0 4.6-3.2 8.4-7.5 9.5-4.3-1.1-7.5-4.9-7.5-9.5V6L12 3Z"></path><path d="M9 12l2 2 4-4"></path></svg>
          <span><strong>Eval-tested</strong>Every release patch-tested</span>
        </li>
        <li>
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M12 2.5 20.5 7v10L12 21.5 3.5 17V7L12 2.5Z"></path><path d="M3.5 7 12 11.5 20.5 7M12 11.5v10"></path></svg>
          <span><strong>Gentle on your stack</strong>One REST API</span>
        </li>
      </ul>
    </div>

    <div class="hx-stage" role="group" aria-label="Example: a task is taken in, planned, checked and handed off">
      <div class="hx-glow" aria-hidden="true"></div>

      <!-- capture viewport, drawn rather than photographed -->
      <div class="hx-view dcard">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="hx-view-head">
          <span class="hx-view-title"><i></i>Intake</span>
          <span class="hx-badge">run_8f2c</span>
          <span class="hx-badge hx-badge--soft">3 tools · AM routine</span>
        </div>

        <div class="hx-chipwrap"><svg class="hx-chip-svg" viewBox="40 60 720 320" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
      <defs>
        <linearGradient id="hx-chipGradient" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#2d2d2d"></stop>
          <stop offset="100%" stop-color="#0f0f0f"></stop>
        </linearGradient>

        <linearGradient id="hx-textGradient" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%" stop-color="#eeeeee"></stop>
          <stop offset="100%" stop-color="#888888"></stop>
        </linearGradient>

        <linearGradient id="hx-pinGradient" x1="1" y1="0" x2="0" y2="0">
          <stop offset="0%" stop-color="#bbbbbb"></stop>
          <stop offset="50%" stop-color="#888888"></stop>
          <stop offset="100%" stop-color="#555555"></stop>
        </linearGradient>
      </defs>

      <g>
        <path d="M100 100 H200 V210 H326" class="trace-bg"></path>
        <path d="M100 100 H200 V210 H326" class="trace-flow purple"></path>

        <path d="M80 180 H180 V230 H326" class="trace-bg"></path>
        <path d="M80 180 H180 V230 H326" class="trace-flow blue"></path>

        <path d="M60 260 H150 V250 H326" class="trace-bg"></path>
        <path d="M60 260 H150 V250 H326" class="trace-flow yellow"></path>

        <path d="M100 350 H200 V270 H326" class="trace-bg"></path>
        <path d="M100 350 H200 V270 H326" class="trace-flow green"></path>

        <path d="M700 90 H560 V210 H474" class="trace-bg"></path>
        <path d="M700 90 H560 V210 H474" class="trace-flow blue"></path>

        <path d="M740 160 H580 V230 H474" class="trace-bg"></path>
        <path d="M740 160 H580 V230 H474" class="trace-flow green"></path>

        <path d="M720 250 H590 V250 H474" class="trace-bg"></path>
        <path d="M720 250 H590 V250 H474" class="trace-flow red"></path>

        <path d="M680 340 H570 V270 H474" class="trace-bg"></path>
        <path d="M680 340 H570 V270 H474" class="trace-flow yellow"></path>
      </g>

      <rect
        x="330"
        y="190"
        width="140"
        height="100"
        rx="20"
        ry="20"
        fill="url(#hx-chipGradient)"
        stroke="#222"
        stroke-width="3"
        filter="drop-shadow(0 0 6px rgba(0,0,0,0.8))"
      ></rect>

      <g>
        <rect
          x="322"
          y="205"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="322"
          y="225"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="322"
          y="245"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="322"
          y="265"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
      </g>

      <g>
        <rect
          x="470"
          y="205"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="470"
          y="225"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="470"
          y="245"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
        <rect
          x="470"
          y="265"
          width="8"
          height="10"
          fill="url(#hx-pinGradient)"
          rx="2"
        ></rect>
      </g>

      <text
        x="400"
        y="240"
        font-family="Arial, sans-serif"
        font-size="22"
        fill="url(#hx-textGradient)"
        text-anchor="middle"
        alignment-baseline="middle"
      >Intake</text>

      <circle cx="100" cy="100" r="5" fill="black"></circle>
      <circle cx="80" cy="180" r="5" fill="black"></circle>
      <circle cx="60" cy="260" r="5" fill="black"></circle>
      <circle cx="100" cy="350" r="5" fill="black"></circle>

      <circle cx="700" cy="90" r="5" fill="black"></circle>
      <circle cx="740" cy="160" r="5" fill="black"></circle>
      <circle cx="720" cy="250" r="5" fill="black"></circle>
      <circle cx="680" cy="340" r="5" fill="black"></circle>
    </svg></div>

        <div class="hx-view-foot">
          <span class="hx-check"><i></i>Context 98%</span>
          <span class="hx-check"><i></i>Drift none</span>
          <span class="hx-check hx-check--site">Routine · support</span>
        </div>
      </div>

      <!-- the crop -->
      <div class="hx-crop dcard">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="hx-crop-inner">
          <div class="hx-intent" aria-hidden="true">
            <span class="ln"><i>{</i></span>
            <span class="ln in hl"><b>"intent"</b>: <em>"refund"</em>,</span>
            <span class="ln in"><b>"order"</b>: <em>"#4821"</em>,</span>
            <span class="ln in"><b>"tools"</b>: [<em>3</em>],</span>
            <span class="ln in"><b>"pii"</b>: <em>"redacted"</em></span>
            <span class="ln"><i>}</i></span>
          </div>
          <span class="hx-brackets" aria-hidden="true"></span>
        </div>
      </div>

      <!-- request -->
      <div class="hx-console dcard">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="hx-console-head">
          <span class="dot dot--live"></span><span class="dot"></span><span class="dot"></span>
          <span class="route">POST /v2/runs · 218 ms</span>
        </div>
<pre class="hx-code"><span class="k">curl</span> https://api.dermexcel.dev/v2/runs \
  -H <span class="s">"Authorization: Bearer $DX_KEY"</span> \
  -F <span class="s">"brief=@ticket.json"</span> \
  -F <span class="s">"routine=support"</span></pre>
      </div>

      <!-- response -->
      <div class="hx-results dcard">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="hx-tile"><span class="k">Task success</span><span class="v">0.94</span><span class="meter"><i style="--w: 94%"></i></span></div>
        <div class="hx-tile"><span class="k">Steps</span><span class="v">4 of 4</span><span class="meter"><i style="--w: 100%"></i></span></div>
        <div class="hx-tile"><span class="k">Handled by</span><span class="v">Agent</span><span class="meter"><i style="--w: 72%"></i></span></div>
      </div>
    </div>
  </div>
</section>

<section class="platform" id="platform" data-section="platform">
  <div class="platform-inner">
    <div class="platform-head">
      <h2 class="platform-title rv">One API.<br><span>The whole agent routine.</span></h2>
      <p class="platform-sub rv">Like any routine worth keeping, it runs in order: clean the context, do the work, protect the result. One endpoint, one event schema, every step logged.</p>
    </div>

    <ol class="flow">
      <li class="flow-step pane rv">
        <div class="flow-top">
          <span class="flow-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24"><path d="M12 3c3 4 6 7.2 6 10.5A6 6 0 0 1 6 13.5C6 10.2 9 7 12 3Z"></path><path d="M9.5 14.5a2.5 2.5 0 0 0 2.5 2.5"></path></svg>
          </span>
          <span class="flow-num">Step 01</span>
        </div>
        <h3>Cleanse</h3>
        <p>Every brief is tidied before an agent sees it: duplicates merged, personal data redacted, context trimmed to what the task needs.</p>
        <code class="flow-call">POST /v2/runs</code>
        <div class="flow-metric"><span>Median intake</span><strong>120 ms</strong></div>
        <span class="flow-link" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"></path></svg></span>
      </li>
      <li class="flow-step flow-step--core pane rv">
        <div class="flow-top">
          <span class="flow-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24"><path d="M9 3h6M10 3v4.5L5.5 17a2.5 2.5 0 0 0 2.2 3.5h8.6a2.5 2.5 0 0 0 2.2-3.5L14 7.5V3"></path><path d="M7.5 14h9"></path></svg>
          </span>
          <span class="flow-num">Step 02</span>
        </div>
        <h3>Treat</h3>
        <p>The agent plans, calls your tools and checks its own work. Every step is traced and scored, so you can see what each one did.</p>
        <code class="flow-call">planner.v3 · tools · self-check</code>
        <div class="flow-metric"><span>p95 per step</span><strong>240 ms</strong></div>
        <span class="flow-link" aria-hidden="true"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"></path></svg></span>
      </li>
      <li class="flow-step pane rv">
        <div class="flow-top">
          <span class="flow-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24"><path d="M12 3l7.5 3v5.5c0 4.6-3.2 8.4-7.5 9.5-4.3-1.1-7.5-4.9-7.5-9.5V6L12 3Z"></path><path d="M9 12l2 2 4-4"></path></svg>
          </span>
          <span class="flow-num">Step 03</span>
        </div>
        <h3>Protect</h3>
        <p>Guardrails check every result against your policies. Anything uncertain goes to a person, a queue or a webhook instead of a customer.</p>
        <code class="flow-call">guard.policies → human · webhook</code>
        <div class="flow-metric"><span>Policy check</span><strong>40 ms</strong></div>
      </li>
    </ol>

    <div class="platform-foot pane rv">
      <div class="region">
        <svg viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="12" r="9.5"></circle><path d="M2.5 12h19M12 2.5a14.5 14.5 0 0 1 0 19M12 2.5a14.5 14.5 0 0 0 0 19"></path></svg>
        <span><strong>Six regions.</strong> Agent data never leaves the one you pick.</span>
      </div>
      <div class="region-chips" aria-label="Regions">
        <span>us-west</span><span>us-east</span><span>eu-central</span><span>eu-west</span><span>ap-southeast</span><span>ap-south</span>
      </div>
      <a class="btn-glass" href="#faq">Read the changelog →</a>
    </div>
  </div>
</section>


<!-- ============ Modules ============ -->
<section class="section section--gray" id="products" data-section="modules">
  <div class="section-inner">
    <div class="section-head">
      <div class="rv">
        <h2 class="section-title">Four modules.<br><span>One control plane.</span></h2>
      </div>
      <p class="section-sub rv">Turn on what you need and leave the rest out. Every module speaks the same event schema, so an agent routine is a list, not an integration project.</p>
    </div>

    <div class="mgrid">
      <article class="mcard pane dcard" data-name="Agent Runtime" data-latency="168">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="mcard-head"><span class="mcard-kicker">Runtime</span><span class="mcard-chip">v2.4 · 168 ms</span></div>
        <div class="mcard-stage">
          <svg class="mc-svg" viewBox="0 0 300 160" aria-hidden="true"><defs><linearGradient id="mc-chip" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2d2d2d"></stop><stop offset="1" stop-color="#0f0f0f"></stop></linearGradient><linearGradient id="mc-pin" x1="1" y1="0" x2="0" y2="0"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient><linearGradient id="mc-pin-v" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient></defs><path d="M82 22 H218 A22 22 0 0 1 240 44 V116 A22 22 0 0 1 218 138 H82 A22 22 0 0 1 60 116 V44 A22 22 0 0 1 82 22 Z" class="mc-bg"></path><path d="M82 22 H218 A22 22 0 0 1 240 44 V116 A22 22 0 0 1 218 138 H82 A22 22 0 0 1 60 116 V44 A22 22 0 0 1 82 22 Z" class="mc-loop" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:0s"></path><path d="M82 22 H218 A22 22 0 0 1 240 44 V116 A22 22 0 0 1 218 138 H82 A22 22 0 0 1 60 116 V44 A22 22 0 0 1 82 22 Z" class="mc-loop" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:1.6s"></path><path d="M150 55 V22" class="mc-bg"></path><path d="M150 55 V22" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:0.2s"></path><path d="M188 80 H240" class="mc-bg"></path><path d="M188 80 H240" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:0.7s"></path><path d="M150 105 V138" class="mc-bg"></path><path d="M150 105 V138" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:1.2s"></path><path d="M112 80 H60" class="mc-bg"></path><path d="M112 80 H60" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:1.7s"></path><circle cx="150" cy="22" r="4.5" class="mc-pad lit" style="stroke:#9900ff;color:#9900ff"></circle><circle cx="240" cy="80" r="4.5" class="mc-pad"></circle><circle cx="150" cy="138" r="4.5" class="mc-pad"></circle><circle cx="60" cy="80" r="4.5" class="mc-pad"></circle><text x="150" y="12" class="mc-label" text-anchor="middle">plan</text><text x="248" y="84" class="mc-label" text-anchor="start">act</text><text x="150" y="157" class="mc-label" text-anchor="middle">check</text><text x="52" y="84" class="mc-label" text-anchor="end">learn</text><rect x="117" y="60" width="66" height="40" rx="12" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="112" y="66.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="183" y="66.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="112" y="76.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="183" y="76.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="112" y="86.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="183" y="86.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="130.0" y="55" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><rect x="130.0" y="100" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><rect x="146.5" y="55" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><rect x="146.5" y="100" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><rect x="163.0" y="55" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><rect x="163.0" y="100" width="7" height="5" rx="1.5" fill="url(#mc-pin-v)"></rect><text x="150.0" y="84.0" class="mc-chip-text" text-anchor="middle">AGENT</text><text x="282" y="18" class="mc-label dim" text-anchor="end">loop ×4</text></svg>
        </div>
        <div class="mcard-body">
          <h3>Agent Runtime</h3>
          <p>Plans and runs multi-step tasks, with a calibrated confidence score on every step.</p>
        </div>
        <ul class="mcard-caps"><li>Plan</li><li>Act</li><li>Score</li></ul>
        <div class="mcard-foot">
          <span>Add to routine</span>
          <button class="gswitch" type="button" role="switch" aria-checked="true" aria-label="Add Agent Runtime to routine"><span class="gswitch-thumb"></span></button>
        </div>
      </article>

      <article class="mcard pane dcard" data-name="Router" data-latency="40">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="mcard-head"><span class="mcard-kicker">Routing</span><span class="mcard-chip">v2.4 · 40 ms</span></div>
        <div class="mcard-stage">
          <svg class="mc-svg" viewBox="0 0 300 160" aria-hidden="true"><defs><linearGradient id="mc-chip" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2d2d2d"></stop><stop offset="1" stop-color="#0f0f0f"></stop></linearGradient><linearGradient id="mc-pin" x1="1" y1="0" x2="0" y2="0"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient><linearGradient id="mc-pin-v" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient></defs><path d="M48 81 H65" class="mc-bg"></path><path d="M48 81 H65" class="mc-flow" pathLength="100" style="stroke:#ffea00;color:#ffea00;animation-delay:0s"></path><path d="M145 81 H180" class="mc-bg"></path><path d="M180 81 V43 H215" class="mc-bg"></path><path d="M180 81 V119 H215" class="mc-bg"></path><path d="M215 43 V24 H250" class="mc-bg"></path><path d="M215 43 V62 H250" class="mc-bg"></path><path d="M215 119 V100 H250" class="mc-bg"></path><path d="M215 119 V138 H250" class="mc-bg"></path><path d="M145 81 H180 V43 H215 V62 H250" class="mc-lit" style="stroke:#00ccff;color:#00ccff"></path><path d="M145 81 H180 V43 H215 V62 H250" class="mc-flow fast" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:0.4s"></path><path d="M215 119 V100 H250" class="mc-flow" pathLength="100" style="stroke:#ff3300;color:#ff3300;animation-delay:1.4s"></path><path d="M215 43 V24 H250" class="mc-flow" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:2.0s"></path><path d="M215 119 V138 H250" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:2.6s"></path><circle cx="180" cy="81" r="3.2" class="mc-node on"></circle><circle cx="215" cy="43" r="3.2" class="mc-node on"></circle><circle cx="215" cy="119" r="3.2" class="mc-node"></circle><circle cx="44" cy="81" r="4.5" class="mc-pad"></circle><circle cx="254" cy="24" r="4.5" class="mc-pad"></circle><circle cx="254" cy="62" r="4.5" class="mc-pad lit" style="stroke:#00ccff;color:#00ccff"></circle><circle cx="254" cy="100" r="4.5" class="mc-pad"></circle><circle cx="254" cy="138" r="4.5" class="mc-pad"></circle><text x="36" y="85" class="mc-label" text-anchor="end">task</text><text x="262" y="28" class="mc-label" text-anchor="start">agent</text><text x="262" y="66" class="mc-label on" text-anchor="start">model</text><text x="262" y="104" class="mc-label" text-anchor="start">human</text><text x="262" y="142" class="mc-label" text-anchor="start">queue</text><rect x="70" y="61" width="70" height="40" rx="12" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="65" y="67.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="140" y="67.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="65" y="77.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="140" y="77.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="65" y="87.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="140" y="87.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><text x="105.0" y="85.0" class="mc-chip-text" text-anchor="middle">ROUTER</text><text x="20" y="18" class="mc-label dim">conf 0.94 → model</text></svg>
        </div>
        <div class="mcard-body">
          <h3>Router</h3>
          <p>Decides which agent, model or person takes each task, using rules you version like code.</p>
        </div>
        <ul class="mcard-caps"><li>Rules</li><li>Priority</li><li>Handoff</li></ul>
        <div class="mcard-foot">
          <span>Add to routine</span>
          <button class="gswitch" type="button" role="switch" aria-checked="true" aria-label="Add Router to routine"><span class="gswitch-thumb"></span></button>
        </div>
      </article>

      <article class="mcard pane dcard" data-name="Memory Sync" data-latency="async">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="mcard-head"><span class="mcard-kicker">Memory</span><span class="mcard-chip">at-least-once</span></div>
        <div class="mcard-stage">
          <svg class="mc-svg" viewBox="0 0 300 160" aria-hidden="true"><defs><linearGradient id="mc-chip" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2d2d2d"></stop><stop offset="1" stop-color="#0f0f0f"></stop></linearGradient><linearGradient id="mc-pin" x1="1" y1="0" x2="0" y2="0"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient><linearGradient id="mc-pin-v" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient></defs><path d="M88 72 H150" class="mc-bg"></path><path d="M88 72 H150" class="mc-flow" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:0s"></path><path d="M150 88 H88" class="mc-bg"></path><path d="M150 88 H88" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:0.8s"></path><path d="M150 24 V136" class="mc-bg"></path><path d="M150 72 V24" class="mc-flow" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:0.3s"></path><path d="M150 88 V136" class="mc-flow" pathLength="100" style="stroke:#ffea00;color:#ffea00;animation-delay:0.9s"></path><path d="M150 32 H187" class="mc-bg"></path><path d="M150 32 H187" class="mc-flow" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:1.1s"></path><path d="M150 80 H187" class="mc-bg"></path><path d="M150 80 H187" class="mc-flow" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:1.6s"></path><path d="M187 128 H150" class="mc-bg"></path><path d="M187 128 H150" class="mc-flow" pathLength="100" style="stroke:#ffea00;color:#ffea00;animation-delay:2.1s"></path><circle cx="150" cy="32" r="3" class="mc-node on"></circle><circle cx="150" cy="80" r="3" class="mc-node on"></circle><circle cx="150" cy="128" r="3" class="mc-node on"></circle><rect x="26" y="56" width="56" height="48" rx="12" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="82" y="64.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="82" y="76.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="82" y="88.5" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><text x="54.0" y="84.0" class="mc-chip-text" text-anchor="middle" style="font-size:10.5px">AGENT</text><rect x="192" y="18" width="74" height="28" rx="6" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="187" y="24" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="30" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="36" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="242" y="27" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="247" y="27" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="252" y="27" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="257" y="27" width="3" height="10" rx="1" class="mc-cell"></rect><text x="216" y="36" class="mc-chip-text" text-anchor="middle" style="font-size:10px">CRM</text><rect x="192" y="66" width="74" height="28" rx="6" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="187" y="72" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="78" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="84" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="242" y="75" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="247" y="75" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="252" y="75" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="257" y="75" width="3" height="10" rx="1" class="mc-cell"></rect><text x="216" y="84" class="mc-chip-text" text-anchor="middle" style="font-size:10px">DESK</text><rect x="192" y="114" width="74" height="28" rx="6" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="187" y="120" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="126" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="187" y="132" width="5" height="4" rx="1" fill="url(#mc-pin)"></rect><rect x="242" y="123" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="247" y="123" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="252" y="123" width="3" height="10" rx="1" class="mc-cell"></rect><rect x="257" y="123" width="3" height="10" rx="1" class="mc-cell"></rect><text x="216" y="132" class="mc-chip-text" text-anchor="middle" style="font-size:10px">DWH</text><text x="119" y="64" class="mc-label dim" text-anchor="middle">write</text><text x="119" y="102" class="mc-label dim" text-anchor="middle">read</text></svg>
        </div>
        <div class="mcard-body">
          <h3>Memory Sync</h3>
          <p>Keeps what your agents remember in step with your CRM, help desk and warehouse.</p>
        </div>
        <ul class="mcard-caps"><li>CRM</li><li>Help desk</li><li>Webhooks</li></ul>
        <div class="mcard-foot">
          <span>Add to routine</span>
          <button class="gswitch" type="button" role="switch" aria-checked="false" aria-label="Add Memory Sync to routine"><span class="gswitch-thumb"></span></button>
        </div>
      </article>

      <article class="mcard mcard--new pane dcard" data-name="Insights" data-latency="async">
        <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>
        <div class="mcard-head"><span class="mcard-kicker">Analytics</span><span class="mcard-chip mcard-chip--new">New · beta</span></div>
        <div class="mcard-stage">
          <svg class="mc-svg" viewBox="0 0 300 160" aria-hidden="true"><defs><linearGradient id="mc-chip" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2d2d2d"></stop><stop offset="1" stop-color="#0f0f0f"></stop></linearGradient><linearGradient id="mc-pin" x1="1" y1="0" x2="0" y2="0"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient><linearGradient id="mc-pin-v" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#bbbbbb"></stop><stop offset="0.5" stop-color="#888888"></stop><stop offset="1" stop-color="#555555"></stop></linearGradient></defs><path d="M58 138 H262" class="mc-bg"></path><path d="M58 138 H262" class="mc-flow slow" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:0s"></path><path d="M80 138 V106" class="mc-bg"></path><path d="M80 138 V106" class="mc-flow" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:0.0s"></path><circle cx="80" cy="106" r="4.5" class="mc-pad"></circle><path d="M102 138 V98" class="mc-bg"></path><path d="M102 138 V98" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:0.25s"></path><circle cx="102" cy="98" r="4.5" class="mc-pad"></circle><path d="M124 138 V102" class="mc-bg"></path><path d="M124 138 V102" class="mc-flow" pathLength="100" style="stroke:#ffea00;color:#ffea00;animation-delay:0.5s"></path><circle cx="124" cy="102" r="4.5" class="mc-pad"></circle><path d="M146 138 V90" class="mc-bg"></path><path d="M146 138 V90" class="mc-flow" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:0.75s"></path><circle cx="146" cy="90" r="4.5" class="mc-pad"></circle><path d="M168 138 V82" class="mc-bg"></path><path d="M168 138 V82" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:1.0s"></path><circle cx="168" cy="82" r="4.5" class="mc-pad"></circle><path d="M190 138 V86" class="mc-bg"></path><path d="M190 138 V86" class="mc-flow" pathLength="100" style="stroke:#ffea00;color:#ffea00;animation-delay:1.25s"></path><circle cx="190" cy="86" r="4.5" class="mc-pad"></circle><path d="M212 138 V70" class="mc-bg"></path><path d="M212 138 V70" class="mc-flow" pathLength="100" style="stroke:#00ccff;color:#00ccff;animation-delay:1.5s"></path><circle cx="212" cy="70" r="4.5" class="mc-pad"></circle><path d="M234 138 V60" class="mc-bg"></path><path d="M234 138 V60" class="mc-flow" pathLength="100" style="stroke:#00ff15;color:#00ff15;animation-delay:1.75s"></path><circle cx="234" cy="60" r="4.5" class="mc-pad"></circle><path d="M256 138 V38" class="mc-lit" style="stroke:#9900ff;color:#9900ff"></path><path d="M256 138 V38" class="mc-flow fast" pathLength="100" style="stroke:#9900ff;color:#9900ff;animation-delay:0.2s"></path><circle cx="256" cy="38" r="4.5" class="mc-pad lit" style="stroke:#9900ff;color:#9900ff"></circle><rect x="16" y="124" width="40" height="28" rx="9" fill="url(#mc-chip)" stroke="#222" stroke-width="2"></rect><rect x="56" y="129.8" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><rect x="56" y="139.2" width="5" height="7" rx="1.5" fill="url(#mc-pin)"></rect><text x="36.0" y="142.0" class="mc-chip-text" text-anchor="middle" style="font-size:9.5px">SQL</text><text x="16" y="34" class="mc-big">98.4k</text><text x="16" y="52" class="mc-label">runs / week <tspan class="mc-up">▲ 5%</tspan></text></svg>
        </div>
        <div class="mcard-body">
          <h3>Insights</h3>
          <p>SQL access to runs, tool calls, costs and overrides, with scheduled exports.</p>
        </div>
        <ul class="mcard-caps"><li>SQL</li><li>Exports</li><li>Audit log</li></ul>
        <div class="mcard-foot">
          <span>Add to routine</span>
          <button class="gswitch" type="button" role="switch" aria-checked="false" aria-label="Add Insights to routine"><span class="gswitch-thumb"></span></button>
        </div>
      </article>
    </div>

    <div class="pipebar pane">
      <span class="pipebar-label">Your routine</span>
      <div class="pipebar-flow" aria-live="polite"></div>
      <span class="pipebar-meta"></span>
    </div>
  </div>
</section>

<!-- ============ How it works + numbers ============ -->
<section class="section section--white" id="science" data-section="how-it-works">
  <div class="wireframe-globe wireframe-globe--right"></div>
  <div class="section-inner">
    <div class="section-head">
      <div class="rv">
        <h2 class="section-title">From brief<br><span>to a finished task.</span></h2>
      </div>
      <p class="section-sub rv">Four steps, all of them yours to call directly. Nothing here is a black box you cannot log, replay or export.</p>
    </div>

    <div class="steps">
      <div class="step-track"><div class="step-track-fill"></div></div>
      <div class="step-grid">
        <div class="step-card pane">
          <span class="step-num">01</span>
          <div class="step-icon">
            <svg viewBox="0 0 24 24"><path d="M12 16V4"></path><polyline points="7 9 12 4 17 9"></polyline><path d="M4 16v3a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-3"></path></svg>
          </div>
          <h3>Brief</h3>
          <p>Describe the task and hand over the tools it may use. Inputs are cleaned and personal data redacted on arrival.</p>
        </div>
        <div class="step-card pane">
          <span class="step-num">02</span>
          <div class="step-icon">
            <svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="3"></rect><path d="M8 13l3-3 2 2 3-4"></path></svg>
          </div>
          <h3>Run</h3>
          <p>The agent plans, calls tools and checks its own work, with every step traced and scored as it goes.</p>
        </div>
        <div class="step-card pane">
          <span class="step-num">03</span>
          <div class="step-icon">
            <svg viewBox="0 0 24 24"><circle cx="6" cy="6" r="3"></circle><circle cx="18" cy="18" r="3"></circle><path d="M6 9v4a2 2 0 0 0 2 2h7"></path></svg>
          </div>
          <h3>Review</h3>
          <p>Guardrails check each result. Anything below your confidence threshold goes to a person, not a customer.</p>
        </div>
        <div class="step-card pane">
          <span class="step-num">04</span>
          <div class="step-icon step-icon--orange">
            <svg viewBox="0 0 24 24"><path d="M21 12a9 9 0 1 1-3-6.7"></path><polyline points="21 4 21 9 16 9"></polyline></svg>
          </div>
          <h3>Learn</h3>
          <p>Every override becomes an eval. Ship a new routine behind a flag and compare it on live traffic.</p>
        </div>
      </div>
    </div>

    <div class="stats-panel pane pane--dark">
      <div class="stats-intro">
        <p>Run in production by teams who page someone when it breaks.</p>
      </div>
      <div class="stat"><span class="stat-num">99.98%</span><span class="stat-label">Uptime, trailing 90 days</span></div>
      <div class="stat"><span class="stat-num" data-count="240" data-suffix=" ms">240 ms</span><span class="stat-label">p95 step latency</span></div>
      <div class="stat"><span class="stat-num" data-count="40" data-suffix="+">40+</span><span class="stat-label">Tool integrations</span></div>
      <div class="stat"><span class="stat-num" data-count="6">6</span><span class="stat-label">Regions</span></div>
    </div>
  </div>
</section>

<!-- ============ Pipelines ============ -->
<section class="section section--gray" id="plans" data-section="pipelines">
  <div class="section-inner">
    <div class="section-head">
      <div class="rv">
        <h2 class="section-title">Pick a routine.<br><span>We'll wire the agents.</span></h2>
      </div>
      <p class="section-sub rv">Each routine is a template you can fork: the same modules with different tools, thresholds and retention.</p>
    </div>

    <div class="plan-tabs rv" role="tablist" aria-label="Routines">
      <button class="plan-tab active" role="tab" id="tab-telederm" aria-selected="true" aria-controls="plan-panel" data-plan="support">Support</button>
      <button class="plan-tab" role="tab" id="tab-triage" aria-selected="false" aria-controls="plan-panel" tabindex="-1" data-plan="sales">Sales ops</button>
      <button class="plan-tab" role="tab" id="tab-screening" aria-selected="false" aria-controls="plan-panel" tabindex="-1" data-plan="research">Research</button>
      <button class="plan-tab" role="tab" id="tab-research" aria-selected="false" aria-controls="plan-panel" tabindex="-1" data-plan="backoffice">Back office</button>
      <button class="plan-tab" role="tab" id="tab-enterprise" aria-selected="false" aria-controls="plan-panel" tabindex="-1" data-plan="enterprise">Enterprise</button>
    </div>

    <div class="plan-panel" id="plan-panel" role="tabpanel" aria-labelledby="tab-telederm">
      <div class="plan-summary pane">
        <h3 class="plan-title">Support</h3>
        <p class="plan-desc">Tickets in, resolved replies out, with anything uncertain handed to a person before a customer ever sees it.</p>
        <div class="plan-focus"><span>Agent Runtime</span><span>Memory Sync</span><span>Webhooks</span></div>
      </div>
      <div class="plan-pipe">
        <div class="pipe-row pipe-row--am pane pane--inset">
          <span class="pipe-time">IN</span>
          <div><strong class="pipe-product">POST /v2/runs</strong><span class="pipe-note">A new ticket arrives with the customer's history, personal data redacted at the edge.</span></div>
          <span class="pipe-step">Step 1</span>
        </div>
        <div class="pipe-row pipe-row--pm pane pane--inset">
          <span class="pipe-time">RUN</span>
          <div><strong class="pipe-product">planner.v3 · help-desk tools</strong><span class="pipe-note">Plan, look things up, draft a reply, then check it against your policies.</span></div>
          <span class="pipe-step">Step 2</span>
        </div>
        <div class="pipe-row pipe-row--review pane pane--inset">
          <span class="pipe-time">OUT</span>
          <div><strong class="pipe-product">reply → help desk</strong><span class="pipe-note">Posted with the full trace attached, or handed to a person when confidence is low.</span></div>
          <span class="pipe-step">Ongoing</span>
        </div>
        <p class="plan-note">Illustrative routine. Dermexcel is a fictional product built for this template.</p>
      </div>
    </div>
  </div>
</section>

<!-- ============ Customers ============ -->
<section class="section section--white" id="reviews" data-section="testimonials">
  <div class="section-inner">
    <div class="section-head">
      <div class="rv">
        <h2 class="section-title">Shipped in a sprint.<br><span>Still running a year on.</span></h2>
      </div>
      <div class="review-summary rv">
        <span class="quote-metric">4.2M runs / month</span>
      </div>
    </div>

    <div class="review-grid">
      <figure class="review-card pane">
        <span class="quote-metric">−38% time to resolution</span>
        <blockquote>"We replaced a support macro library two people maintained by hand with one routine. The part I did not expect was replaying a week of tickets against a new agent before switching."</blockquote>
        <figcaption><span class="avatar">SM</span><span><strong>Sarah Mbeki</strong><em>Staff engineer · Northwind Health</em></span></figcaption>
      </figure>
      <figure class="review-card review-card--dark pane pane--dark">
        <span class="quote-metric">3 days to production</span>
        <blockquote>"Sandbox key on Monday, first real tickets answered on Thursday. The SDK did what the docs said it would, which is rarer than it should be."</blockquote>
        <figcaption><span class="avatar">JK</span><span><strong>James Kerr</strong><em>CTO · Clinic OS</em></span></figcaption>
      </figure>
      <figure class="review-card pane">
        <span class="quote-metric">0 PII leaves region</span>
        <blockquote>"Our security team cares where customer data lives. Running the agents in our own region, with a trace of every tool call we can export, is what got this approved."</blockquote>
        <figcaption><span class="avatar">PR</span><span><strong>Priya Raman</strong><em>Head of platform · Meridian Care</em></span></figcaption>
      </figure>
    </div>
  </div>
</section>

<!-- ============ FAQ ============ -->
<section class="section section--gray" id="faq" data-section="faq">
  <div class="section-inner faq-layout">
    <div class="faq-intro rv">
      <h2 class="section-title">Questions,<br><span>answered.</span></h2>
      <p class="section-sub">Everything else is in the docs, and the docs are versioned with the API.</p>
      <div class="btn-wrapper">
        <button class="btn" data-target="#consult" data-label="Generate" data-label-busy="Generating">
          <svg class="btn-svg" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M9.813 15.904 9 18.75l-.813-2.846a4.5 4.5 0 0 0-3.09-3.09L2.25 12l2.846-.813a4.5 4.5 0 0 0 3.09-3.09L9 5.25l.813 2.846a4.5 4.5 0 0 0 3.09 3.09L15.75 12l-2.846.813a4.5 4.5 0 0 0-3.09 3.09ZM18.259 8.715 18 9.75l-.259-1.035a3.375 3.375 0 0 0-2.455-2.456L14.25 6l1.036-.259a3.375 3.375 0 0 0 2.455-2.456L18 2.25l.259 1.035a3.375 3.375 0 0 0 2.456 2.456L21.75 6l-1.035.259a3.375 3.375 0 0 0-2.456 2.456ZM16.894 20.567 16.5 21.75l-.394-1.183a2.25 2.25 0 0 0-1.423-1.423L13.5 18.75l1.183-.394a2.25 2.25 0 0 0 1.423-1.423l.394-1.183.394 1.183a2.25 2.25 0 0 0 1.423 1.423l1.183.394-1.183.394a2.25 2.25 0 0 0-1.423 1.423Z"></path>
          </svg>
          <span class="txt-wrapper">
            <span class="txt-1">Generate</span>
            <span class="txt-2">Generating</span>
          </span>
        </button>
      </div>
    </div>

    <div class="faq-list">
      <div class="faq-item open pane">
        <button class="faq-q" id="faq-q-1" aria-expanded="true" aria-controls="faq-a-1">How does authentication work?<span class="faq-icon" aria-hidden="true"></span></button>
        <div class="faq-a" id="faq-a-1" role="region" aria-labelledby="faq-q-1"><div><p>Project-scoped bearer keys, rotated from the dashboard or the API. Server-side keys can be pinned to an IP range; browser SDKs get short-lived tokens minted by your backend.</p></div></div>
      </div>
      <div class="faq-item pane">
        <button class="faq-q" id="faq-q-2" aria-expanded="false" aria-controls="faq-a-2">What are the rate limits?<span class="faq-icon" aria-hidden="true"></span></button>
        <div class="faq-a" id="faq-a-2" role="region" aria-labelledby="faq-q-2"><div><p>60 requests per second per project on the standard plan, burst to 200. Every response carries the remaining budget, and a 429 tells you when to retry rather than making you guess.</p></div></div>
      </div>
      <div class="faq-item pane">
        <button class="faq-q" id="faq-q-3" aria-expanded="false" aria-controls="faq-a-3">Where does customer data live?<span class="faq-icon" aria-hidden="true"></span></button>
        <div class="faq-a" id="faq-a-3" role="region" aria-labelledby="faq-q-3"><div><p>In the region you pick, and only there. Conversations can be dropped the moment a run finishes, or kept for a retention window you set per routine. Every read is in the audit log.</p></div></div>
      </div>
      <div class="faq-item pane">
        <button class="faq-q" id="faq-q-4" aria-expanded="false" aria-controls="faq-a-4">Can we self-host?<span class="faq-icon" aria-hidden="true"></span></button>
        <div class="faq-a" id="faq-a-4" role="region" aria-labelledby="faq-q-4"><div><p>Agent workers ship as a container you can run in your own VPC, with the control plane still managed. Model and planner updates arrive as signed images you choose to promote.</p></div></div>
      </div>
      <div class="faq-item pane">
        <button class="faq-q" id="faq-q-5" aria-expanded="false" aria-controls="faq-a-5">What does the SLA cover?<span class="faq-icon" aria-hidden="true"></span></button>
        <div class="faq-a" id="faq-a-5" role="region" aria-labelledby="faq-q-5"><div><p>99.95% on the API and a p95 latency target per region, measured from our edge, with credits applied automatically from the same numbers on the status page.</p></div></div>
      </div>
    </div>
  </div>
</section>

<!-- ============ Footer ============ -->
<footer class="site-footer fx-footer" data-section="footer">
  <div class="ft-card dcard">
    <span class="card-fx" aria-hidden="true"><span class="card-grid"></span><span class="card-glow"></span></span>

    <div class="ft-top">
      <div class="ft-brand">
        <a class="ft-logo" href="#top">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 338.3 330" aria-hidden="true"><use href="#dx-mark"></use></svg>
          DERMEXCEL
        </a>
        <p>Brief, run and review AI agents from one control plane. Every step traced, every result checked.</p>
        <a class="ft-status" href="#faq"><span class="ft-dot" aria-hidden="true"></span>All systems normal<span class="ft-status-meta">99.98% · 90 days</span></a>
      </div>

      <div class="ft-cols">
        <nav class="ft-col" aria-label="Platform">
          <h4>Platform</h4>
          <a href="#products">Agent Runtime</a>
          <a href="#products">Router</a>
          <a href="#products">Memory Sync</a>
          <a href="#products">Insights</a>
        </nav>
        <nav class="ft-col" aria-label="Developers">
          <h4>Developers</h4>
          <a href="#faq">Quickstart</a>
          <a href="#faq">API reference</a>
          <a href="#plans">Routine templates</a>
          <a href="#faq">Changelog</a>
        </nav>
        <nav class="ft-col" aria-label="Company">
          <h4>Company</h4>
          <a href="#science">How it works</a>
          <a href="#reviews">Customers</a>
          <a href="#faq">Security</a>
          <a href="#consult">Pricing</a>
        </nav>
      </div>
    </div>

    <div class="ft-cta" id="consult">
      <div>
        <strong>Start on a sandbox key.</strong>
        <span>10,000 free agent runs. No sales call.</span>
      </div>
      <a class="nav-cta" href="#faq">Read the quickstart →</a>
    </div>

    <div class="ft-bottom">
      <span>© <span id="year">2026</span> Dermexcel. A fictional product built as a template.</span>
      <span class="ft-regions" aria-label="Regions"><i>us-west</i><i>us-east</i><i>eu-central</i><i>eu-west</i><i>ap-southeast</i><i>ap-south</i></span>
      <span class="ft-legal"><a href="#top">Privacy</a><a href="#top">Terms</a><a href="#top">X</a><a href="#top">LinkedIn</a><a href="#top">GitHub</a></span>
    </div>
  </div>
</footer>

<script>
document.addEventListener("DOMContentLoaded", () => {
  const $ = (s, r = document) => r.querySelector(s);
  const $$ = (s, r = document) => [...r.querySelectorAll(s)];
  const motion = document.documentElement.classList.contains("mo");

  /* The generate button animates letter by letter, so each label is split
     into spans here. The plain text stays readable if this never runs. */
  $$(".btn .txt-1, .btn .txt-2").forEach((label) => {
    const text = label.textContent.trim();
    label.replaceChildren(
      ...[...text].map((char) => {
        const span = document.createElement("span");
        span.className = "btn-letter";
        span.textContent = char === " " ? " " : char;
        return span;
      })
    );
  });

  // Theme switcher: start from the viewer's own theme, then remember which
  // option the thumb is leaving so it squashes in the right direction.
  const switcher = $(".switcher");
  // The page always opens in the light theme; dark and dim stay one tap away in the menu.

  const trackPrevious = (el) => {
    const radios = el.querySelectorAll('input[type="radio"]');
    let previousValue = null;
    const initiallyChecked = el.querySelector('input[type="radio"]:checked');
    if (initiallyChecked) {
      previousValue = initiallyChecked.getAttribute("c-option");
      el.setAttribute("c-previous", previousValue);
    }
    radios.forEach((radio) => {
      radio.addEventListener("change", () => {
        if (radio.checked) {
          el.setAttribute("c-previous", previousValue ?? "");
          previousValue = radio.getAttribute("c-option");
        }
      });
    });
  };
  trackPrevious(switcher);

  // Morph surfaces: give each a shell, its own radius, and a stagger
  // among the siblings it arrives with.
  $$(".m").forEach((el) => {
    const shell = document.createElement("span");
    shell.className = "m-shell";
    shell.setAttribute("aria-hidden", "true");
    el.prepend(shell);
    el.style.setProperty("--m-r", getComputedStyle(el).borderTopLeftRadius);
    const siblings = [...el.parentElement.children].filter((c) => c.classList.contains("m"));
    el.style.setProperty("--m-delay", `${siblings.indexOf(el) * 0.14}s`);
  });
  // hero composition lands in reading order: capture, request, response, then the crop
  [[".hx-view", 0], [".hx-console", 0.25], [".hx-results", 0.45], [".hx-crop", 0.85]].forEach(([sel, d]) => {
    const el = $(sel);
    if (el) el.style.setProperty("--m-delay", `${d}s`);
  });
  $$(".m-shell").forEach((shell) =>
    shell.addEventListener("animationend", () => shell.parentElement.classList.add("landed"))
  );

  $$(".rv").forEach((el) => {
    const siblings = [...el.parentElement.children].filter((c) => c.classList.contains("rv"));
    el.style.setProperty("--m-delay", `${siblings.indexOf(el) * 0.12}s`);
  });

  // Stat counters run once the panel has finished landing
  const runCounters = (panel) => {
    const wait = motion ? 1600 : 0;
    $$(".stat-num[data-count]", panel).forEach((el) => {
      const target = Number(el.dataset.count);
      const suffix = el.dataset.suffix || "";
      if (!motion) return;
      el.textContent = "0" + suffix;
      setTimeout(() => {
        const start = performance.now();
        const tick = (now) => {
          const t = Math.min((now - start) / 1600, 1);
          const eased = 1 - Math.pow(1 - t, 3);
          el.textContent = Math.round(target * eased).toLocaleString("en-US") + suffix;
          if (t < 1) requestAnimationFrame(tick);
        };
        requestAnimationFrame(tick);
      }, wait);
    });
  };

  const watched = $$(".m, .rv, .steps, .stats-panel");
  if (motion && "IntersectionObserver" in window) {
    const io = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (!entry.isIntersecting) return;
          entry.target.classList.add("is-in");
          if (entry.target.classList.contains("stats-panel")) runCounters(entry.target);
          io.unobserve(entry.target);
        });
      },
      { threshold: 0.12, rootMargin: "0px 0px -6% 0px" }
    );
    watched.forEach((el) => io.observe(el));
  } else {
    watched.forEach((el) => el.classList.add("is-in"));
  }


  // Floating pill + full-page menu
  const nav = $(".site-nav");
  const burger = $(".burger");
  const menu = $("#site-menu");
  const onScroll = () => nav.classList.toggle("scrolled", window.scrollY > 40);
  onScroll();
  window.addEventListener("scroll", onScroll, { passive: true });

  const isOpen = () => menu.classList.contains("open");
  const setMenu = (open, { restoreFocus = true } = {}) => {
    const r = burger.getBoundingClientRect();
    menu.style.setProperty("--mx", `${r.left + r.width / 2}px`);
    menu.style.setProperty("--my", `${r.top + r.height / 2}px`);
    menu.classList.toggle("open", open);
    menu.inert = !open;
    nav.classList.toggle("menu-open", open);
    burger.setAttribute("aria-expanded", String(open));
    burger.setAttribute("aria-label", open ? "Close menu" : "Open menu");
    document.documentElement.classList.toggle("menu-lock", open);
    if (open) setTimeout(() => $(".menu-links a", menu).focus({ preventScroll: true }), 250);
    else if (restoreFocus) burger.focus({ preventScroll: true });
  };
  burger.addEventListener("click", () => setMenu(!isOpen()));
  document.addEventListener("keydown", (e) => {
    if (!isOpen()) return;
    if (e.key === "Escape") { setMenu(false); return; }
    if (e.key !== "Tab") return;
    // keep focus inside the menu and its close button
    const stops = [burger, ...$$("a, button, input:checked", menu)];
    const i = stops.indexOf(document.activeElement);
    const next = e.shiftKey ? (i <= 0 ? stops.length - 1 : i - 1) : (i === stops.length - 1 ? 0 : i + 1);
    e.preventDefault();
    stops[next].focus();
  });
  $$("[data-close]").forEach((link) => {
    link.addEventListener("click", (e) => {
      const target = $(link.getAttribute("href"));
      if (!target) return;
      e.preventDefault();
      const wasOpen = isOpen();
      if (wasOpen) setMenu(false, { restoreFocus: false });
      setTimeout(() => target.scrollIntoView({ behavior: motion ? "smooth" : "auto", block: "start" }), wasOpen ? 120 : 0);
    });
  });

  // Nav items and buttons that name a section scroll to it
  $$("[data-target]").forEach((el) => {
    el.style.cursor = "pointer";
    el.addEventListener("click", (e) => {
      const target = $(el.dataset.target);
      if (!target) return;
      e.preventDefault();
      target.scrollIntoView({ behavior: motion ? "smooth" : "auto", block: "start" });
    });
  });

  /* iOS Safari does not focus a button on tap, and :focus drives the label
     swap. Mirror it with a class so a tap gets the same "Generating" beat. */
  $$(".btn").forEach((btn) => {
    btn.addEventListener("click", () => {
      if (btn.type === "submit") return;
      btn.classList.add("is-busy");
      clearTimeout(btn._busy);
      btn._busy = setTimeout(() => btn.classList.remove("is-busy"), 2600);
    });
  });


  // Module cards: pointer highlight, glass switches, live pipeline summary
  const mcards = $$(".mcard");
  mcards.forEach((card) => {
    card.addEventListener("pointermove", (e) => {
      const r = card.getBoundingClientRect();
      card.style.setProperty("--px", `${e.clientX - r.left}px`);
      card.style.setProperty("--py", `${e.clientY - r.top}px`);
    });
  });
  const flow = $(".pipebar-flow");
  const meta = $(".pipebar-meta");
  const arrow = '<svg viewBox="0 0 24 24" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"></path></svg>';
  const renderPipeline = () => {
    const on = mcards.filter((c) => $(".gswitch", c).getAttribute("aria-checked") === "true");
    if (!on.length) {
      flow.innerHTML = '<span class="empty">Switch on a module to start a routine.</span>';
      meta.textContent = "0 of 4 modules";
      return;
    }
    flow.innerHTML = on
      .map((c) => `<span class="chip-mod${c.dataset.latency === "async" ? " async" : ""}">${c.dataset.name}</span>`)
      .join(arrow);
    const inline = on.filter((c) => c.dataset.latency !== "async");
    const ms = inline.reduce((sum, c) => sum + Number(c.dataset.latency), 0);
    const asyncCount = on.length - inline.length;
    meta.textContent =
      `${on.length} of 4 modules · ` +
      (inline.length ? `${ms} ms p95 in the request path` : "nothing in the request path") +
      (asyncCount ? ` · ${asyncCount} async` : "");
  };
  $$(".gswitch").forEach((sw) => {
    sw.addEventListener("click", () => {
      const on = sw.getAttribute("aria-checked") !== "true";
      sw.setAttribute("aria-checked", String(on));
      sw.classList.remove("squash");
      void sw.offsetWidth;
      if (motion) sw.classList.add("squash");
      renderPipeline();
    });
  });
  renderPipeline();

  // Module enable toggle
  $$(".round-btn").forEach((btn) => {
    const name = (btn.getAttribute("aria-label") || "").replace(/^Enable /, "");
    btn.addEventListener("click", () => {
      const added = btn.classList.toggle("added");
      btn.textContent = added ? "✓" : "+";
      btn.setAttribute("aria-pressed", String(added));
      btn.setAttribute("aria-label", `${added ? "Disable" : "Enable"} ${name}`);
      btn.classList.remove("pop");
      void btn.offsetWidth;
      btn.classList.add("pop");
    });
  });

  // Pipeline tabs
  const plans = {
    support: {
      modules: 3,
      desc: "Tickets in, resolved replies out, with anything uncertain handed to a person before a customer ever sees it.",
      focus: ["Agent Runtime", "Memory Sync", "Webhooks"],
      am: ["POST /v2/runs", "A new ticket arrives with the customer's history, personal data redacted at the edge."],
      pm: ["planner.v3 · help-desk tools", "Plan, look things up, draft a reply, then check it against your policies."],
      out: ["reply → help desk", "Posted with the full trace attached, or handed to a person when confidence is low."]
    },
    sales: {
      modules: 2,
      desc: "Inbound leads researched, scored and routed while they are still warm, with the reasoning attached to every score.",
      focus: ["Agent Runtime", "Router", "CRM"],
      am: ["POST /v2/runs?routine=sales", "Form fills and replies arrive as briefs, batched or one at a time."],
      pm: ["research.tools · score.v2", "Look up the company, score fit and intent, draft a first touch."],
      out: ["router → account owner", "Assigned in your CRM with the score, the sources and a draft ready to send."]
    },
    research: {
      modules: 2,
      desc: "Pinned planner versions, deterministic runs and an export of everything, so a result can be reproduced a year later.",
      focus: ["Version pinning", "Insights", "Audit log"],
      am: ["POST /v2/runs?planner=v3.1", "Pin the version. It stays callable after it is retired."],
      pm: ["deterministic · seed=fixed", "Same brief, same steps, with every tool call and score kept."],
      out: ["dataset.export", "Briefs, traces and overrides, with a manifest that ties them together."]
    },
    backoffice: {
      modules: 3,
      desc: "Invoices, refunds and account changes handled overnight, in order, with a person signing off anything over your limits.",
      focus: ["Agent Runtime", "Router", "Insights"],
      am: ["schedule://nightly", "Runs on a schedule, like a PM routine, against the day's queue."],
      pm: ["planner.v3 · finance tools", "Reconcile, apply the change, and check it twice before committing."],
      out: ["approval → finance lead", "Anything over threshold waits for a signature; the rest posts with its trace."]
    },
    enterprise: {
      modules: 4,
      desc: "Everything in your own VPC: agent workers you run, a control plane we keep, and the audit trail your security team asks for.",
      focus: ["Self-hosted workers", "SSO", "Custom SLA"],
      am: ["ingress → your VPC", "Briefs never leave the region or the account you choose."],
      pm: ["signed worker image", "Planner updates arrive signed, and you decide what gets promoted."],
      out: ["audit → your SIEM", "Every tool call and override streamed out as it happens."]
    }
  };

  const tabs = $$(".plan-tab");
  const planPanel = $(".plan-panel");
  const tabTrack = $(".plan-tabs");
  let thumbAt = null;
  const placeThumb = (tab, animate) => {
    tabTrack.classList.toggle("no-slide", !animate);
    if (animate && thumbAt) {
      const goingRight = tab.offsetLeft > thumbAt.offsetLeft;
      tabTrack.style.setProperty("--to", goingRight ? "left" : "right");
      tabTrack.classList.remove("squash");
      void tabTrack.offsetWidth;
      if (motion) tabTrack.classList.add("squash");
    }
    tabTrack.style.setProperty("--tx", `${tab.offsetLeft}px`);
    tabTrack.style.setProperty("--tw", `${tab.offsetWidth}px`);
    thumbAt = tab;
  };
  const activeTab = () => tabs.find((t) => t.classList.contains("active")) || tabs[0];
  placeThumb(activeTab(), false);
  window.addEventListener("resize", () => placeThumb(activeTab(), false));
  document.fonts && document.fonts.ready.then(() => placeThumb(activeTab(), false));

  const renderPlan = (tab) => {
    const p = plans[tab.dataset.plan];
    planPanel.setAttribute("aria-labelledby", tab.id);
    $(".plan-title", planPanel).textContent = tab.textContent;
    $(".plan-desc", planPanel).textContent = p.desc;
    $(".plan-focus", planPanel).replaceChildren(
      ...p.focus.map((f) => Object.assign(document.createElement("span"), { textContent: f }))
    );
    [
      [".pipe-row--am", p.am],
      [".pipe-row--pm", p.pm],
      [".pipe-row--review", p.out]
    ].forEach(([row, [product, note]]) => {
      $(`${row} .pipe-product`, planPanel).textContent = product;
      $(`${row} .pipe-note`, planPanel).textContent = note;
    });
  };

  const selectPlan = (tab) => {
    if (tab.classList.contains("active")) return;
    placeThumb(tab, motion);
    tabs.forEach((t) => {
      const on = t === tab;
      t.classList.toggle("active", on);
      t.setAttribute("aria-selected", String(on));
      t.tabIndex = on ? 0 : -1;
    });
    if (!motion) { renderPlan(tab); return; }
    planPanel.classList.add("swap");
    setTimeout(() => {
      renderPlan(tab);
      planPanel.classList.remove("swap");
    }, 200);
  };

  tabs.forEach((tab) => tab.addEventListener("click", () => selectPlan(tab)));
  $(".plan-tabs").addEventListener("keydown", (e) => {
    if (e.key !== "ArrowRight" && e.key !== "ArrowLeft") return;
    const i = tabs.indexOf(document.activeElement);
    if (i < 0) return;
    const next = tabs[(i + (e.key === "ArrowRight" ? 1 : -1) + tabs.length) % tabs.length];
    next.focus();
    selectPlan(next);
  });

  // FAQ accordion: one open at a time
  const faqItems = $$(".faq-item");
  faqItems.forEach((item) => {
    const q = $(".faq-q", item);
    q.addEventListener("click", () => {
      const open = !item.classList.contains("open");
      faqItems.forEach((other) => {
        other.classList.remove("open");
        $(".faq-q", other).setAttribute("aria-expanded", "false");
      });
      item.classList.toggle("open", open);
      q.setAttribute("aria-expanded", String(open));
    });
  });


  $("#year").textContent = new Date().getFullYear();
});
</script>

</body></html>
```

