INSTALANDING.AI · Monax Analytics Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Monax Analytics Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/monax-analytics-landing-page

monax-analytics.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Monax Analytics Landing Page
  slug     monax-analytics-landing-page
  prompt   https://instalanding.ai/p/monax-analytics-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/monax-analytics-landing-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of the main <style>: --bg #efede8, --bg-2, --ink #0d0d10, --mute, --line,
            --green / --green-dark, the shadow stack --shadow-card/-soft/-pill/-dark, --ease-soft; Inter (Google Fonts)
  sections  nav, hero, fan-stack, logos, product, features, testimonials, pricing, resources, footer
  scripts   1) GSAP 3.12.5 + ScrollTrigger (cdnjs): intro timeline, pill bobs, fanned card stack, section reveals,
               product-demo tabs, bento alert feed, stories carousel, monthly/annual toggle, demo newsletter (sends nothing)
            2) dithered field: plain-WebGL port of FaultyTerminal, one canvas per [data-fx] host (data-fx-ink / data-fx-paper)
  assets    none: all CSS gradients, inline SVG and SVG data URIs (grain, avatar glyph)

  ADAPTING
  - [data-fx] hosts get position:relative + isolation:isolate and a z-index:-1 canvas as first child; their CSS
    gradient is the no-WebGL fallback, so keep it. Recolour via data-fx-ink / data-fx-paper, not CSS.
  - Section reveals use ScrollTrigger.batch with clearProps:"transform" so CSS :hover lifts survive; never put a
    second ScrollTrigger tween on the same element's transform.
  - Fan-slot mouse parallax uses the CSS translate property, kept off GSAP's transform; keep them separate.
  - The GSAP script runs gsap.set() initial states inline at parse time: an element renamed in the markup stays hidden.
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Monax</title>
<meta name="description" content="Single-file analytics SaaS landing page: warm grain, glossy 3D orbs, masked headline reveal, tabbed product demo, bento, pricing and GSAP motion." />

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet" />

<style>
:root {
  --bg: #efede8;
  --bg-2: #e5e2da;
  --ink: #0d0d10;
  --ink-soft: #2a2a2d;
  --mute: #8a8780;
  --line: #dad6c9;
  --pill: #0d0d10;
  --green: #bfd58f;
  --green-dark: #5c7838;

  /* Shadow stacks used throughout the original sections, named for reuse */
  --shadow-card: 0 22px 40px -16px rgba(40, 30, 10, 0.18),
    0 8px 16px -4px rgba(40, 30, 10, 0.08), inset 0 1px 0 rgba(255, 255, 255, 0.7);
  --shadow-soft: 0 14px 24px -10px rgba(40, 30, 10, 0.18),
    0 5px 10px -3px rgba(40, 30, 10, 0.08), inset 0 1px 0 rgba(255, 255, 255, 0.6);
  --shadow-pill: 0 12px 22px -8px rgba(0, 0, 0, 0.4),
    0 4px 8px -2px rgba(0, 0, 0, 0.18), inset 0 1px 0 rgba(255, 255, 255, 0.12),
    inset 0 -2px 4px rgba(0, 0, 0, 0.4);
  --shadow-dark: 0 40px 80px -30px rgba(20, 12, 0, 0.45),
    0 16px 32px -12px rgba(20, 12, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -3px 8px rgba(0, 0, 0, 0.5);
  --ease-soft: cubic-bezier(0.6, 0, 0.2, 1);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html,
body {
  background: var(--bg);
  color: var(--ink);
  font-family: "Inter", system-ui, sans-serif;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
}
body {
  background: radial-gradient(
    120% 70% at 50% 0%,
    #f4f1ec 0%,
    #eae7df 60%,
    #dfdbcf 100%
  );
  min-height: 100vh;
}

.grain {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 100;
  opacity: 0.05;
  mix-blend-mode: multiply;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='220' height='220'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.85' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0.1  0 0 0 0 0.1  0 0 0 0 0.1  0 0 0 0.6 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}

/* ============ NAV ============ */
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 50;
  padding: 22px 40px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(239, 237, 232, 0.78);
  backdrop-filter: blur(14px);
  -webkit-backdrop-filter: blur(14px);
  border-bottom: 1px solid rgba(20, 20, 22, 0.06);
}
.logo {
  font-family: "Inter", sans-serif;
  font-weight: 700;
  font-size: 22px;
  letter-spacing: -0.03em;
}
.nav-links {
  list-style: none;
  display: flex;
  gap: 28px;
  position: absolute;
  left: 50%;
  transform: translateX(-50%);
}
.nav-links a {
  color: var(--ink-soft);
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  display: inline-flex;
  align-items: center;
  gap: 4px;
  position: relative;
  padding: 4px 2px;
  transition: color 0.3s;
}
.nav-links a:hover {
  color: var(--ink);
}
.nav-links a svg {
  transition: transform 0.3s;
}
.nav-links a:hover svg {
  transform: rotate(180deg);
}
.contact-pill {
  background: var(--pill);
  color: #fafaf7;
  border: none;
  padding: 13px 28px;
  border-radius: 999px;
  font-family: "Inter", sans-serif;
  font-size: 14px;
  font-weight: 500;
  cursor: pointer;
  box-shadow: 0 12px 22px -8px rgba(0, 0, 0, 0.4),
    0 4px 8px -2px rgba(0, 0, 0, 0.18), inset 0 1px 0 rgba(255, 255, 255, 0.12),
    inset 0 -2px 4px rgba(0, 0, 0, 0.4);
  transition: transform 0.4s cubic-bezier(0.6, 0, 0.2, 1);
}
.contact-pill:hover {
  transform: translateY(-2px);
}

/* ============ HERO ============ */
.hero {
  padding: 130px 40px 40px;
  text-align: center;
  position: relative;
  z-index: 5;
}

.headline {
  font-family: "Inter", sans-serif;
  font-weight: 800;
  font-size: clamp(48px, 8vw, 130px);
  line-height: 1;
  letter-spacing: -0.045em;
  color: var(--ink);
  max-width: 1300px;
  margin: 0 auto;
}
.headline .line {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 28px;
  overflow: visible;
  padding: 4px 0;
}
.headline .word {
  display: inline-block;
  overflow: hidden;
  padding-bottom: 0.1em;
  margin-bottom: -0.1em;
}
.headline .word > span {
  display: inline-block;
  transform: translateY(105%);
}

/* Inline image pill (yellow blob) */
.inline-img {
  display: inline-block;
  width: clamp(110px, 14vw, 220px);
  height: clamp(58px, 7.4vw, 116px);
  border-radius: 999px;
  overflow: hidden;
  position: relative;
  box-shadow: 0 18px 30px -10px rgba(80, 60, 20, 0.35),
    0 6px 12px -3px rgba(80, 60, 20, 0.18),
    inset 0 2px 0 rgba(255, 255, 255, 0.25),
    inset 0 -3px 6px rgba(80, 40, 0, 0.18);
  background: linear-gradient(
    135deg,
    #ffd66b 0%,
    #ffaa4b 35%,
    #e26a4d 70%,
    #4d9cc6 100%
  );
  transform: scale(0);
  will-change: transform;
}
.inline-img::before {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(
      ellipse at 70% 60%,
      rgba(78, 162, 200, 0.55),
      transparent 50%
    ),
    radial-gradient(
      circle at 30% 30%,
      rgba(255, 255, 255, 0.3),
      transparent 50%
    );
  pointer-events: none;
}
.inline-img::after {
  content: "";
  position: absolute;
  inset: 0;
  /* coiled tube illusion */
  background: repeating-linear-gradient(
      95deg,
      transparent 0 6px,
      rgba(0, 0, 0, 0.08) 6px 7px
    ),
    linear-gradient(
      155deg,
      rgba(255, 255, 255, 0.18) 0%,
      transparent 30%,
      transparent 70%,
      rgba(60, 30, 0, 0.18) 100%
    );
  pointer-events: none;
  border-radius: inherit;
}

/* Green idea pill */
.idea-pill {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  background: var(--green);
  border-radius: 999px;
  padding: 8px 12px 8px 22px;
  box-shadow: 0 14px 24px -10px rgba(60, 100, 30, 0.3),
    0 5px 10px -2px rgba(60, 100, 30, 0.15),
    inset 0 2px 0 rgba(255, 255, 255, 0.4),
    inset 0 -2px 4px rgba(60, 100, 30, 0.2);
  transform: scale(0);
  will-change: transform;
}
.idea-pill .txt {
  font-family: "Inter", sans-serif;
  font-weight: 600;
  font-size: clamp(11px, 1.2vw, 18px);
  line-height: 1.15;
  letter-spacing: -0.015em;
  color: var(--ink);
  text-align: left;
}
.idea-pill .leaf {
  width: clamp(40px, 5vw, 76px);
  height: clamp(40px, 5vw, 76px);
  border-radius: 50%;
  position: relative;
  overflow: hidden;
  box-shadow: 0 6px 12px -2px rgba(60, 100, 30, 0.4),
    inset 0 2px 0 rgba(255, 255, 255, 0.3),
    inset 0 -2px 4px rgba(40, 80, 20, 0.4);
  background: radial-gradient(
    circle at 35% 35%,
    #d7f08c 0%,
    #8fb852 40%,
    #4a6e22 100%
  );
  flex-shrink: 0;
}
.idea-pill .leaf::before {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(
      circle at 70% 70%,
      transparent 30%,
      rgba(0, 0, 0, 0.15) 60%,
      transparent 80%
    ),
    radial-gradient(
      circle at 30% 80%,
      rgba(255, 255, 255, 0.2),
      transparent 40%
    );
}
.idea-pill .leaf::after {
  content: "";
  position: absolute;
  width: 30%;
  height: 30%;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: radial-gradient(circle at 30% 30%, #c8e078, #5c7b30);
  border-radius: 50%;
  box-shadow: 0 0 0 4px rgba(255, 255, 255, 0.15);
}

/* Stats line above the headline */
.hero-eyebrow {
  justify-content: center;
  margin-bottom: 26px;
  letter-spacing: 0.2em;
  text-wrap: balance;
}
.hero-eyebrow b { color: var(--ink); font-weight: 700; font-variant-numeric: tabular-nums; }

/* ============ BELOW HERO: fanned card stack ============
   Portrait cards tilted and overlapping across a ghost phrase.
   Three layers per card so no two motions fight over one transform:
   .fan-slot  scroll fan-out (x / y / rotation) + mouse parallax (translate)
   .fan-card  intro drop, resting tilt and the idle float
   .fan-face  hover tilt in 3D, and the painted surface itself          */
.fan-section {
  --k: 1; /* card scale; stepped down by the breakpoints below */
  position: relative;
  z-index: 5;
  padding: 20px 40px 90px;
}
.fan-stage {
  position: relative;
  max-width: 1320px;
  margin: 0 auto;
  height: calc(400px * var(--k));
  display: flex;
  align-items: center;
  justify-content: center;
}
.fan-ghost {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 0;
  font-size: clamp(60px, 12.5vw, 200px);
  font-style: italic;
  font-weight: 900;
  line-height: 0.85;
  letter-spacing: -0.055em;
  white-space: nowrap;
  color: var(--line);
  user-select: none;
  pointer-events: none;
}
.fan-ghost .gl { display: inline-block; transform-origin: bottom; }

.fan {
  position: relative;
  z-index: 2;
  display: flex;
  align-items: center;
  justify-content: center;
}
.fan-slot {
  position: relative;
  top: calc(var(--y) * var(--k));
  z-index: var(--z);
  width: calc(var(--w) * var(--k));
  height: calc(var(--h) * var(--k));
  margin-inline: calc(-6px * var(--k));
  flex-shrink: 0;
}
.fan-card { width: 100%; height: 100%; transform: rotate(var(--rot)); will-change: transform; }

.fan-face {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: calc(14px * var(--k));
  border-radius: calc(22px * var(--k));
  overflow: hidden;
  cursor: pointer;
  color: #fafaf7;
  font-size: max(10px, calc(13px * var(--k)));
  background: linear-gradient(180deg, var(--c1) 0%, var(--c2) 35%, var(--c3) 70%, var(--c4) 100%);
  box-shadow: 0 30px 50px -16px rgba(var(--sh), 0.5),
    0 14px 26px -8px rgba(var(--sh), 0.32),
    0 5px 10px -2px rgba(var(--sh), 0.2),
    inset 0 2px 0 rgba(255, 255, 255, 0.4),
    inset 0 -4px 8px rgba(var(--sh), 0.4);
  transition: box-shadow 0.5s var(--ease-soft);
}
.fan-face::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: 2;
  border-radius: inherit;
  pointer-events: none;
  background: linear-gradient(155deg, rgba(255, 255, 255, 0.26) 0%, transparent 30%,
    transparent 70%, rgba(var(--sh), 0.22) 100%);
}
.fan-face > * { position: relative; z-index: 3; }
.fan-face:hover {
  box-shadow: 0 44px 70px -20px rgba(var(--sh), 0.6),
    0 22px 38px -10px rgba(var(--sh), 0.38),
    0 8px 14px -3px rgba(var(--sh), 0.22),
    inset 0 2px 0 rgba(255, 255, 255, 0.45),
    inset 0 -4px 8px rgba(var(--sh), 0.4);
}

/* Palette per card, from the page's own orb recipes */
.f-coral  { --c1: #b83515; --c2: #e26a4d; --c3: #ffaa4b; --c4: #ffd66b; --sh: 150, 50, 20; }
.f-green  { --c1: #4a6e22; --c2: #7fa645; --c3: #bfd58f; --c4: #e4f5a8; --sh: 60, 100, 30; }
.f-purple { --c1: #5e3da0; --c2: #8b5bd9; --c3: #b592e0; --c4: #e0cff0; --sh: 80, 45, 130; }
.f-gold   { --c1: #966d14; --c2: #e0a82e; --c3: #ffd66b; --c4: #fff0c0; --sh: 130, 90, 10; }
.f-hero   { --c1: #8163c6; --c2: #e83a4d; --c3: #f2a03b; --c4: #ffe066; --sh: 100, 40, 50; }
.f-blue   { --c1: #3d6f88; --c2: #6fa8c3; --c3: #b5e3f2; --c4: #e6f5fa; --sh: 40, 80, 110; }
.f-sand   { --c1: #8a7050; --c2: #c9a576; --c3: #e8dcc6; --c4: #f4ead6; --sh: 100, 75, 40; }
/* Holographic card: previews the dark Connect tab further down the page */
.f-holo {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
  --sh: 20, 20, 24;
  background: radial-gradient(70% 55% at 50% 45%, rgba(191, 213, 143, 0.14), transparent 70%), var(--ink);
  outline: 1px solid rgba(191, 213, 143, 0.35);
  outline-offset: -1px;
}
.f-holo .f-live { color: rgba(215, 240, 140, 0.8); }
.f-hub {
  position: relative;
  align-self: center;
  width: 62%;
  aspect-ratio: 1;
  perspective: 900px;
  font-size: calc(86px * var(--k));
}
.f-hub .hub-holo { border-radius: calc(20px * var(--k)); }
.f-red    { --c1: #8a0e1e; --c2: #c82938; --c3: #ff7565; --c4: #ffc2b0; --sh: 140, 20, 25; }

/* Frosted caption, always visible so every card reads at rest */
.f-meta {
  padding: 0.7em 0.9em;
  border-radius: calc(14px * var(--k));
  background: rgba(13, 13, 16, 0.62);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.12);
  color: #fafaf7;
}
.f-meta b { display: block; font-size: 1em; font-weight: 700; letter-spacing: -0.01em; }
.f-meta span { display: block; margin-top: 2px; font-size: 0.82em; color: rgba(255, 255, 255, 0.66); }

/* Card contents, all drawn in CSS */
.f-live { display: inline-flex; align-items: center; gap: 0.5em; font-size: 0.85em; font-weight: 600; }
.f-live i { width: 0.6em; height: 0.6em; border-radius: 50%; background: #d7f08c; box-shadow: 0 0 0 3px rgba(215, 240, 140, 0.3); }
.f-live--dark { align-self: flex-start; padding: 0.35em 0.7em; border-radius: 999px; background: rgba(13, 13, 16, 0.62); color: #fafaf7; }
.f-kpi strong { display: block; font-size: 2.3em; font-weight: 800; letter-spacing: -0.05em; line-height: 1; }
.f-kpi em { display: inline-block; margin-top: 0.4em; font-style: normal; font-size: 0.85em; font-weight: 700; }
.f-bars { display: flex; align-items: flex-end; gap: 0.4em; height: 38%; }
.f-bars i {
  flex: 1;
  height: var(--b);
  border-radius: 0.5em 0.5em 0.25em 0.25em;
  background: rgba(255, 255, 255, 0.4);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.6);
}
.f-bars i:first-child { background: rgba(255, 255, 255, 0.85); }
.f-donut {
  align-self: center;
  width: 58%;
  aspect-ratio: 1;
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: conic-gradient(#fafaf7 0 8%, rgba(255, 255, 255, 0.28) 8% 100%);
  -webkit-mask: radial-gradient(circle, transparent 54%, #000 55%);
  mask: radial-gradient(circle, transparent 54%, #000 55%);
}
.f-donut-wrap { position: relative; display: grid; place-items: center; }
.f-donut-wrap strong { position: absolute; font-size: 1.25em; font-weight: 800; letter-spacing: -0.03em; }
.f-ask {
  align-self: flex-end;
  max-width: 88%;
  padding: 0.7em 0.9em;
  border-radius: 1.1em 1.1em 0.35em 1.1em;
  background: var(--ink);
  color: #fafaf7;
  font-size: 0.9em;
  font-weight: 500;
  line-height: 1.3;
  box-shadow: var(--shadow-pill);
}
.f-alert {
  width: 2.6em;
  height: 2.6em;
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: rgba(255, 255, 255, 0.9);
  color: #c82938;
  font-weight: 900;
  font-size: 1.05em;
  box-shadow: 0 0 0 0.45em rgba(255, 255, 255, 0.22);
}
.f-end { align-items: flex-end; }
.f-end .f-meta { text-align: right; }
.f-spark { width: 100%; height: 26%; display: block; }
.arrow-pill:focus-visible { outline: 2px solid var(--green-dark); outline-offset: 3px; }

/* Primary CTA, sitting across the middle of the card row */
.fan-cta {
  position: absolute;
  left: 50%;
  top: 50%;
  z-index: 30;
  translate: -50% -50%;
}
.arrow-pill {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  gap: 14px;
  padding: 14px 14px 14px 32px;
  border: none;
  border-radius: 999px;
  background: var(--pill);
  color: #fafaf7;
  font-family: inherit;
  font-size: 16px;
  font-weight: 600;
  letter-spacing: -0.01em;
  white-space: nowrap;
  cursor: pointer;
  /* light halo separates the pill from the busy card faces behind it */
  box-shadow: 0 0 0 6px rgba(239, 237, 232, 0.6), 0 26px 44px -14px rgba(0, 0, 0, 0.55),
    0 10px 18px -6px rgba(0, 0, 0, 0.3), inset 0 1px 0 rgba(255, 255, 255, 0.14),
    inset 0 -2px 4px rgba(0, 0, 0, 0.4);
  transition: transform 0.4s var(--ease-soft);
}
.arrow-pill:hover { transform: translateY(-2px); }
.arrow-pill .ar {
  width: 32px;
  height: 32px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  color: var(--ink);
  background: radial-gradient(circle at 35% 30%, #d7f08c, #8fb852 70%);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), inset 0 -2px 3px rgba(60, 100, 30, 0.35);
  transition: transform 0.4s var(--ease-soft);
}
.arrow-pill:hover .ar { transform: rotate(45deg); }

@media (max-width: 1280px) { .fan-section { --k: 0.84; } }
@media (max-width: 1060px) { .fan-section { --k: 0.7; } }
@media (max-width: 860px) {
  .fan-section { --k: 0.72; }
  .fan-slot:is(.s1, .s8) { display: none; }
}
@media (max-width: 700px) {
  .fan-section { --k: 0.6; padding: 10px 18px 60px; }
  .fan-slot:is(.s2, .s7) { display: none; }
  .fan-slot { margin-inline: calc(-10px * var(--k)); }
}
@media (max-width: 420px) { .fan-section { --k: 0.52; } }
@media (max-width: 700px) { .f-meta span { display: none; } }
@media (max-width: 380px) { .fan-section { --k: 0.47; } }
@media (max-width: 700px) {
  .hero-eyebrow { margin-bottom: 18px; letter-spacing: 0.12em; }
  .hero-eyebrow::before { display: none; }
  .arrow-pill { gap: 10px; padding: 11px 11px 11px 24px; font-size: 15px; }
  .arrow-pill .ar { width: 28px; height: 28px; }
}

/* kept from the old block: used by other sections */
.read-more {
  color: var(--ink);
  text-decoration: underline;
  text-underline-offset: 4px;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.avatar-stack {
  display: inline-flex;
}
.avatar-stack > * {
  width: 38px;
  height: 38px;
  border-radius: 50%;
  border: 2px solid var(--bg);
  margin-left: -10px;
  background-size: cover;
  background-position: center;
  box-shadow: 0 4px 10px rgba(20, 10, 5, 0.12);
}
.avatar-stack > *:first-child {
  margin-left: 0;
}

/* ============ SECTION 2: FEATURES ============ */
.features {
  padding: 80px 40px 60px;
  position: relative;
  z-index: 5;
}
.features-head,
.sec-head {
  max-width: 1280px;
  margin: 0 auto 50px;
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 40px;
  flex-wrap: wrap;
}
.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-size: 11px;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: var(--mute);
  font-weight: 500;
  margin-bottom: 14px;
}
.eyebrow::before {
  content: "";
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: var(--green-dark);
  box-shadow: 0 0 0 3px rgba(92, 120, 56, 0.2);
}
.features-head h2,
.sec-head h2 {
  font-family: "Inter", sans-serif;
  font-weight: 700;
  font-size: clamp(32px, 4vw, 56px);
  line-height: 1;
  letter-spacing: -0.03em;
  max-width: 700px;
}
.features-head p,
.sec-head > p {
  font-size: 15px;
  line-height: 1.55;
  color: var(--ink-soft);
  max-width: 340px;
}

.features-grid {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}
.feat-card {
  background: #ffffff;
  border-radius: 26px;
  padding: 28px;
  box-shadow: 0 22px 40px -16px rgba(40, 30, 10, 0.18),
    0 8px 16px -4px rgba(40, 30, 10, 0.08),
    inset 0 1px 0 rgba(255, 255, 255, 0.7);
  display: flex;
  flex-direction: column;
  gap: 16px;
  cursor: pointer;
  transition: transform 0.5s cubic-bezier(0.6, 0, 0.2, 1);
}
.feat-card:hover {
  transform: translateY(-8px);
}

.feat-icon {
  width: 64px;
  height: 64px;
  border-radius: 16px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 12px 22px -6px rgba(40, 30, 10, 0.25),
    inset 0 2px 0 rgba(255, 255, 255, 0.3),
    inset 0 -2px 4px rgba(40, 30, 10, 0.2);
}
.feat-icon.ic-1 {
  background: radial-gradient(
    circle at 30% 30%,
    #ffd66b 0%,
    #e26a4d 60%,
    #8a2818
  );
}
.feat-icon.ic-2 {
  background: radial-gradient(
    circle at 30% 30%,
    #c9e37b 0%,
    #6b9d2c 60%,
    #2f5810
  );
}
.feat-icon.ic-3 {
  background: radial-gradient(
    circle at 30% 30%,
    #c9a6f4 0%,
    #6a3db8 60%,
    #391b72
  );
}
.feat-icon::after {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(
    155deg,
    rgba(255, 255, 255, 0.2) 0%,
    transparent 35%
  );
}

.feat-card h3 {
  font-family: "Inter", sans-serif;
  font-weight: 700;
  font-size: 22px;
  letter-spacing: -0.025em;
  color: var(--ink);
}
.feat-card p {
  font-size: 14px;
  line-height: 1.55;
  color: var(--ink-soft);
  flex: 1;
}
.feat-card .feat-link {
  color: var(--ink);
  text-decoration: none;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  transition: gap 0.3s;
}
.feat-card .feat-link:hover {
  gap: 12px;
}

/* ============ SECTION 3: CTA ============ */
.cta-section {
  padding: 80px 40px 140px;
  position: relative;
  z-index: 5;
}
.cta-inner {
  max-width: 1280px;
  margin: 0 auto;
  background: var(--ink);
  border-radius: 36px;
  padding: 80px 60px;
  color: #f4f0eb;
  display: grid;
  grid-template-columns: 1.5fr 1fr;
  gap: 50px;
  align-items: center;
  position: relative;
  overflow: hidden;
  box-shadow: 0 40px 80px -30px rgba(20, 12, 0, 0.45),
    0 16px 32px -12px rgba(20, 12, 0, 0.25),
    inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -3px 8px rgba(0, 0, 0, 0.5);
}
.cta-inner::before {
  content: "";
  position: absolute;
  width: 500px;
  height: 500px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(191, 213, 143, 0.25),
    transparent 65%
  );
  top: -200px;
  left: -100px;
  filter: blur(30px);
}
.cta-inner::after {
  content: "";
  position: absolute;
  width: 400px;
  height: 400px;
  border-radius: 50%;
  background: radial-gradient(
    circle,
    rgba(255, 198, 130, 0.18),
    transparent 65%
  );
  bottom: -180px;
  right: -80px;
  filter: blur(30px);
}
.cta-inner h2 {
  font-family: "Inter", sans-serif;
  font-weight: 800;
  font-size: clamp(32px, 4vw, 60px);
  line-height: 1;
  letter-spacing: -0.035em;
  position: relative;
  z-index: 1;
}
.cta-inner h2 em {
  font-style: italic;
  font-weight: 700;
  background: linear-gradient(135deg, #bfd58f, #ffd66b);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.cta-right {
  position: relative;
  z-index: 1;
}
.cta-right p {
  font-size: 15px;
  line-height: 1.55;
  color: rgba(255, 255, 255, 0.65);
  margin-bottom: 24px;
}
.cta-btn {
  background: #ffffff;
  color: var(--ink);
  border: none;
  padding: 14px 32px;
  border-radius: 999px;
  font-family: inherit;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 12px;
  box-shadow: 0 16px 26px -10px rgba(0, 0, 0, 0.4),
    0 5px 10px -2px rgba(0, 0, 0, 0.18);
  transition: transform 0.4s cubic-bezier(0.6, 0, 0.2, 1);
}
.cta-btn:hover {
  transform: translateY(-3px) scale(1.02);
}

/* ============================================================
   EXTENDED SECTIONS
   Same palette, Inter weights, layered drop + inset shadows,
   26–28px radii, black pills and glossy radial-gradient orbs.
   ============================================================ */

html { scroll-behavior: smooth; }
section[id] { scroll-margin-top: 90px; }

.section {
  position: relative;
  z-index: 5;
  padding: 100px 40px;
}
.section-inner { max-width: 1280px; margin: 0 auto; }

/* Glossy orb, the same recipe as the hero spheres */
.orb {
  position: relative;
  display: inline-block;
  flex-shrink: 0;
  width: 28px;
  height: 28px;
  border-radius: 50%;
  box-shadow: 0 6px 12px -4px rgba(40, 30, 10, 0.3), inset 0 -2px 4px rgba(40, 30, 10, 0.25);
}
.orb::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: radial-gradient(circle at 30% 25%, rgba(255, 255, 255, 0.6) 0%, transparent 35%);
}
.orb--coral { background: radial-gradient(circle at 35% 30%, #ffd66b, #e26a4d 60%, #8a2818); }
.orb--green { background: radial-gradient(circle at 35% 30%, #d7f08c, #8fb852 45%, #4a6e22); }
.orb--purple { background: radial-gradient(circle at 35% 30%, #c7a6f7, #8b5bd9 60%, #5e3da0); }
.orb--blue { background: radial-gradient(circle at 35% 30%, #b5e3f2, #6fa8c3 60%, #3d6f88); }
.orb--sand { background: radial-gradient(circle at 35% 30%, #fff0dc, #d4bc92 60%, #8a7050); }
.orb--red { background: radial-gradient(circle at 35% 30%, #ff7565, #c82938 60%, #8a0e1e); }
.orb--gold { background: radial-gradient(circle at 35% 30%, #ffe078, #e0a82e 60%, #966d14); }

/* ---------- Logo marquee ---------- */
.logos {
  position: relative;
  z-index: 5;
  padding: 0 0 40px;
}
.logos-label {
  margin-bottom: 26px;
  text-align: center;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: var(--mute);
}
.logo-marquee {
  display: flex;
  gap: 64px;
  overflow: hidden;
  -webkit-mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
  mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
}
.logo-track {
  display: flex;
  flex-shrink: 0;
  align-items: center;
  justify-content: space-around;
  gap: 64px;
  min-width: 100%;
  animation: logo-scroll 38s linear infinite;
}
.logo-marquee:hover .logo-track { animation-play-state: paused; }
@keyframes logo-scroll {
  to { transform: translateX(calc(-100% - 64px)); }
}
.brand {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-size: 22px;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: var(--ink-soft);
  white-space: nowrap;
  opacity: 0.7;
  transition: opacity 0.3s;
}
.brand:hover { opacity: 1; }
.brand .orb { width: 22px; height: 22px; }
.brand--light { font-weight: 400; letter-spacing: -0.01em; }
.brand--italic { font-style: italic; font-weight: 600; }
.brand--caps { font-size: 15px; font-weight: 800; letter-spacing: 0.2em; text-transform: uppercase; }

/* ---------- Product demo ---------- */
.demo {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1fr 1.55fr;
  gap: 32px;
  align-items: stretch;
}
.demo-tabs { display: flex; flex-direction: column; gap: 14px; }
.demo-tab {
  position: relative;
  display: grid;
  grid-template-columns: auto 1fr;
  gap: 18px;
  padding: 24px 24px 30px;
  border: none;
  border-radius: 26px;
  background: transparent;
  color: var(--ink);
  font-family: inherit;
  text-align: left;
  cursor: pointer;
  overflow: hidden;
  transition: background 0.4s var(--ease-soft), box-shadow 0.4s var(--ease-soft);
}
.demo-tab:hover { background: rgba(255, 255, 255, 0.45); }
.demo-tab.active { background: #fff; box-shadow: var(--shadow-card); }
.demo-tab:focus-visible { outline: 2px solid var(--green-dark); outline-offset: 3px; }
.demo-tab-num {
  padding-top: 6px;
  font-size: 12px;
  font-weight: 600;
  letter-spacing: 0.08em;
  color: var(--mute);
}
.demo-tab strong {
  display: block;
  margin-bottom: 6px;
  font-size: 22px;
  font-weight: 700;
  letter-spacing: -0.025em;
}
.demo-tab-copy > span { display: block; font-size: 14px; line-height: 1.55; color: var(--ink-soft); }
.demo-tab:not(.active) .demo-tab-copy > span { color: var(--mute); }
.demo-tab-bar {
  position: absolute;
  left: 24px;
  right: 24px;
  bottom: 14px;
  height: 3px;
  border-radius: 3px;
  background: var(--line);
  overflow: hidden;
  opacity: 0;
  transition: opacity 0.3s;
}
.demo-tab.active .demo-tab-bar { opacity: 1; }
.demo-tab-bar i {
  display: block;
  height: 100%;
  border-radius: inherit;
  background: var(--green-dark);
  transform: scaleX(0);
  transform-origin: left center;
}

.demo-window {
  display: flex;
  flex-direction: column;
  min-height: 560px;
  padding: 14px;
  border-radius: 28px;
  background: var(--bg-2);
  box-shadow: 0 40px 70px -20px rgba(60, 40, 30, 0.35),
    0 18px 32px -10px rgba(60, 40, 30, 0.18), inset 0 1px 0 rgba(255, 255, 255, 0.6);
}
.win-bar { display: flex; align-items: center; gap: 7px; padding: 4px 8px 14px; }
.win-bar i {
  width: 11px;
  height: 11px;
  border-radius: 50%;
  box-shadow: inset 0 -1px 2px rgba(40, 30, 10, 0.2);
}
.win-bar i:nth-child(1) { background: #e26a4d; }
.win-bar i:nth-child(2) { background: #ffd66b; }
.win-bar i:nth-child(3) { background: #8fb852; }
.win-bar span { margin-left: 10px; font-size: 12px; font-weight: 500; color: var(--mute); }
.win-body {
  position: relative;
  flex: 1;
  border-radius: 20px;
  background: #fbfaf7;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.8), inset 0 -2px 6px rgba(40, 30, 10, 0.05);
  overflow: hidden;
}
.panel {
  position: absolute;
  inset: 0;
  padding: 28px;
  opacity: 0;
  visibility: hidden;
}
.panel.is-active { opacity: 1; visibility: visible; }

/* Connect: sources wired into a holographic Monax hub, on a dark ground */
.panel-connect {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
  background:
    radial-gradient(60% 60% at 50% 50%, rgba(var(--holo), 0.1), transparent 70%),
    var(--ink);
}
.wires { position: absolute; inset: 0; width: 100%; height: 100%; }
.wires line {
  stroke: rgba(191, 213, 143, 0.35);
  stroke-width: 1.5;
  stroke-dasharray: 5 7;
  vector-effect: non-scaling-stroke;
  animation: wire-flow 1.2s linear infinite;
}
@keyframes wire-flow {
  to { stroke-dashoffset: -24; }
}
/* Hub: three "M" layers stacked in depth inside a glass tile that wobbles */
.hub {
  position: absolute;
  left: 50%;
  top: 50%;
  z-index: 2;
  width: 120px;
  height: 120px;
  translate: -50% -50%;
  perspective: 900px;
  font-size: 92px;
}
.hub-holo {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 26px;
  transform-style: preserve-3d;
  animation: holo-wobble 6.2s ease-in-out infinite;
}
.hub-holo::before,
.hub-holo::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
}
.hub-holo::before {
  background: radial-gradient(circle at 40% 35%, rgba(var(--holo), 0.22), transparent 62%);
  filter: blur(8px);
  transform: translateZ(-80px);
}
.hub-holo::after {
  border: 1px solid rgba(var(--holo), 0.3);
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.07), rgba(255, 255, 255, 0.01) 45%, transparent),
    rgba(13, 13, 16, 0.55);
  transform: translateZ(-45px);
}
.hub-layer {
  position: absolute;
  z-index: 1;
  font-size: 1em;
  font-weight: 900;
  letter-spacing: -0.06em;
  line-height: 1;
  -webkit-text-stroke: 1px rgba(var(--holo-hi), 0.78);
  background: linear-gradient(90deg, rgba(var(--holo), 0.18) 0%, rgba(var(--holo-hi), 0.95) 35%,
    rgba(var(--holo), 0.7) 60%, rgba(var(--holo), 0.22) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  filter: drop-shadow(0 10px 22px rgba(0, 0, 0, 0.55));
}
.hub-layer--back { opacity: 0.18; filter: blur(1px); transform: translateZ(-70px); }
.hub-layer--mid { opacity: 0.42; filter: blur(0.4px); transform: translateZ(-34px); }
.hub-layer--front { opacity: 0.98; transform: translateZ(0); }
/* .src positions (CSS translate); .src-chip is what GSAP animates */
.src {
  position: absolute;
  left: var(--x);
  top: var(--y);
  z-index: 2;
  translate: -50% -50%;
}
.src-chip {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 7px 16px 7px 7px;
  border-radius: 999px;
  border: 1px solid rgba(var(--holo), 0.35);
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), rgba(255, 255, 255, 0.01) 50%), rgba(20, 20, 24, 0.85);
  box-shadow: 0 14px 24px -12px rgba(0, 0, 0, 0.7), inset 0 1px 0 rgba(255, 255, 255, 0.08);
  color: #f4f0eb;
  font-size: 13px;
  font-weight: 600;
  white-space: nowrap;
}
.src-chip .orb { width: 26px; height: 26px; }
.sync-chip {
  position: absolute;
  top: 22px;
  left: 24px;
  z-index: 3;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 12px;
  font-weight: 500;
  color: rgba(var(--holo-hi), 0.75);
}
.live-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #8fb852;
  box-shadow: 0 0 0 3px rgba(143, 184, 82, 0.25);
}

/* Ask: natural-language question → chart answer */
.panel-ask { display: flex; flex-direction: column; gap: 18px; }
.ask-q {
  align-self: flex-end;
  display: flex;
  flex-direction: row-reverse;
  align-items: center;
  gap: 10px;
  max-width: 85%;
}
.ask-q p {
  padding: 12px 18px;
  border-radius: 20px 20px 6px 20px;
  background: var(--ink);
  color: #fafaf7;
  font-size: 14px;
  font-weight: 500;
  box-shadow: var(--shadow-pill);
}
.ask-avatar {
  flex-shrink: 0;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  border: 2px solid #fff;
  background-size: cover;
  background-position: center;
  box-shadow: 0 4px 10px rgba(20, 10, 5, 0.12);
}
.ask-a {
  max-width: 92%;
  padding: 18px 20px;
  border-radius: 20px 20px 20px 6px;
  background: #fff;
  box-shadow: var(--shadow-soft);
}
.ask-a-head { display: flex; align-items: center; gap: 8px; margin-bottom: 8px; font-size: 13px; }
.ask-a-head .orb { width: 20px; height: 20px; }
.ask-meta { margin-left: auto; font-size: 12px; color: var(--mute); }
.ask-a p { margin-bottom: 16px; font-size: 14px; line-height: 1.5; color: var(--ink-soft); }
.ask-a p b { color: var(--green-dark); }
.bars {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  align-items: end;
  gap: 12px;
  height: 130px;
  margin-bottom: 24px;
}
.bar {
  position: relative;
  height: var(--h);
  border-radius: 12px 12px 6px 6px;
  background: linear-gradient(180deg, #e8dcc6, #cdbb9a);
  box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.4), inset 0 -2px 4px rgba(60, 30, 10, 0.12);
  transform-origin: bottom center;
}
.bar:first-child { background: linear-gradient(180deg, #d7f08c, #8fb852); }
.bar em {
  position: absolute;
  top: 8px;
  left: 0;
  right: 0;
  text-align: center;
  font-size: 12px;
  font-style: normal;
  font-weight: 700;
}
.bar span {
  position: absolute;
  bottom: -22px;
  left: 0;
  right: 0;
  text-align: center;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.06em;
  color: var(--mute);
}
.ask-input {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin-top: auto;
  padding: 8px 8px 8px 20px;
  border-radius: 999px;
  background: #fff;
  box-shadow: var(--shadow-soft);
  font-size: 13px;
  color: var(--mute);
}
.send {
  width: 36px;
  height: 36px;
  border: none;
  border-radius: 50%;
  background: var(--ink);
  color: #fff;
  font-size: 15px;
  cursor: pointer;
  box-shadow: var(--shadow-pill);
}

/* Share: KPI tiles + live chart */
.panel-share { display: flex; flex-direction: column; gap: 16px; }
.kpis { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; }
.kpi {
  display: flex;
  flex-direction: column;
  gap: 4px;
  padding: 14px 16px;
  border-radius: 18px;
  background: #fff;
  box-shadow: var(--shadow-soft);
}
.kpi span { font-size: 11px; font-weight: 500; letter-spacing: 0.04em; color: var(--mute); }
.kpi strong { font-size: 24px; font-weight: 800; letter-spacing: -0.04em; }
.kpi em { font-size: 12px; font-style: normal; font-weight: 600; color: var(--green-dark); }
.chart-card {
  flex: 1;
  display: flex;
  flex-direction: column;
  min-height: 0;
  padding: 16px 18px 10px;
  border-radius: 20px;
  background: #fff;
  box-shadow: var(--shadow-soft);
}
.chart-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 8px;
  font-size: 13px;
}
.viewers { display: flex; align-items: center; gap: 8px; font-size: 12px; color: var(--mute); }
.viewers .avatar-stack > * { width: 26px; height: 26px; margin-left: -8px; border-color: #fff; }
.viewers .avatar-stack > *:first-child { margin-left: 0; }
.line-chart { flex: 1; width: 100%; min-height: 120px; display: block; }
.share-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  font-size: 12px;
  color: var(--mute);
}
.mini-pill {
  padding: 9px 18px;
  border: none;
  border-radius: 999px;
  background: var(--ink);
  color: #fafaf7;
  font-family: inherit;
  font-size: 12px;
  font-weight: 500;
  cursor: pointer;
  box-shadow: var(--shadow-pill);
}


/* Holographic treatment carried across all three demo tabs:
   dark ground, glass surfaces with a thin green outline, outlined gradient numerals */
.win-body {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
  --on-dark: 244, 240, 235;
  background: var(--ink);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06), inset 0 -2px 6px rgba(0, 0, 0, 0.4);
}
.panel-ask,
.panel-share {
  background: radial-gradient(70% 60% at 50% 45%, rgba(var(--holo), 0.08), transparent 70%), var(--ink);
  color: rgb(var(--on-dark));
}
.ask-a,
.ask-input,
.kpi,
.chart-card {
  border: 1px solid rgba(var(--holo), 0.3);
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.07), rgba(255, 255, 255, 0.01) 45%, transparent),
    rgba(20, 20, 24, 0.85);
  box-shadow: 0 18px 30px -16px rgba(0, 0, 0, 0.7), inset 0 1px 0 rgba(255, 255, 255, 0.07);
  color: rgb(var(--on-dark));
}
.holo-num {
  -webkit-text-stroke: 1px rgba(var(--holo-hi), 0.75);
  background: linear-gradient(90deg, rgba(var(--holo), 0.25) 0%, rgba(var(--holo-hi), 0.95) 35%,
    rgba(var(--holo), 0.7) 60%, rgba(var(--holo), 0.3) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  filter: drop-shadow(0 6px 12px rgba(0, 0, 0, 0.5));
}
.ask-q p { background: rgb(var(--on-dark)); color: var(--ink); box-shadow: 0 12px 22px -10px rgba(0, 0, 0, 0.6); }
.ask-avatar { border-color: var(--ink); }
.ask-meta,
.kpi span,
.bar span,
.viewers,
.share-row,
.ask-input { color: rgba(var(--on-dark), 0.5); }
.ask-a p { color: rgba(var(--on-dark), 0.72); }
.ask-a p b { color: rgb(var(--holo-hi)); }
.bar {
  border: 1px solid rgba(var(--holo), 0.45);
  background: linear-gradient(180deg, rgba(var(--holo), 0.26), rgba(var(--holo), 0.05));
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.12);
}
.bar:first-child {
  border-color: rgba(var(--holo-hi), 0.8);
  background: linear-gradient(180deg, rgba(var(--holo-hi), 0.55), rgba(var(--holo), 0.12));
}
.bar em { color: rgb(var(--on-dark)); }
.send {
  background: radial-gradient(circle at 35% 30%, #d7f08c, #8fb852 70%);
  color: var(--ink);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), inset 0 -2px 3px rgba(60, 100, 30, 0.35);
}
.kpi strong { color: rgb(var(--on-dark)); }
.kpi em { color: rgba(var(--holo-hi), 0.85); }
.viewers .avatar-stack > * { border-color: var(--ink); }
.mini-pill {
  border: 1px solid rgba(var(--holo), 0.45);
  background: rgba(var(--holo), 0.12);
  color: rgb(var(--on-dark));
  box-shadow: none;
  white-space: nowrap;
}

/* ---------- Bento ---------- */
.bento {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 250px;
  gap: 22px;
}
.tile {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  gap: 8px;
  padding: 28px;
  border-radius: 26px;
  background: #fff;
  box-shadow: var(--shadow-card);
  overflow: hidden;
  transition: transform 0.5s var(--ease-soft);
}
.tile:hover { transform: translateY(-6px); }
.tile h3 { font-size: 22px; font-weight: 700; letter-spacing: -0.025em; }
.tile p { max-width: 340px; font-size: 14px; line-height: 1.55; color: var(--ink-soft); }

.tile--layers {
  grid-column: span 2;
  grid-row: span 2;
  background: var(--ink);
  color: #f4f0eb;
  box-shadow: var(--shadow-dark);
}
.tile--layers::before {
  content: "";
  position: absolute;
  width: 480px;
  height: 480px;
  top: -180px;
  right: -140px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(191, 213, 143, 0.22), transparent 65%);
  filter: blur(30px);
}
.tile--layers > * { position: relative; }
.tile--layers p { color: rgba(255, 255, 255, 0.65); }
.tile--layers .eyebrow { color: rgba(255, 255, 255, 0.5); margin-bottom: 4px; }
/* Holographic stack: three translucent panes in depth, Sources at the back,
   Metrics at the front. CSS wobbles the stack; GSAP tweens --gap on hover. */
.layers {
  --gap: 36px;
  --holo: 191, 213, 143;   /* var(--green) as rgb */
  --holo-hi: 215, 240, 140;
  position: absolute;
  top: 47%;
  left: 50%;
  width: min(250px, 68%);
  aspect-ratio: 25 / 13;
  translate: -50% -50%;
  perspective: 900px;
}
.layers-rot {
  position: absolute;
  inset: 0;
  transform-style: preserve-3d;
  animation: holo-wobble 6.2s ease-in-out infinite;
}
@keyframes holo-wobble {
  0%, 100% { transform: rotateX(16deg) rotateY(-18deg); }
  50% { transform: rotateX(18deg) rotateY(18deg); }
}
.slab {
  position: absolute;
  inset: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 14px 22px 18px;
  border-radius: 26px;
  border: 1px solid rgba(var(--holo), 0.4);
  background:
    radial-gradient(circle at 40% 35%, rgba(var(--holo), 0.12), transparent 62%),
    linear-gradient(120deg, rgba(255, 255, 255, 0.07), rgba(255, 255, 255, 0.01) 45%, transparent),
    rgba(13, 13, 16, 0.82);
  box-shadow: 0 30px 50px -22px rgba(0, 0, 0, 0.7), inset 0 1px 0 rgba(255, 255, 255, 0.08);
  /* each pane steps back in depth and up-left, so every label stays in view */
  transform: translate3d(calc(var(--i) * -12px), calc(var(--i) * -66px), calc(var(--i) * var(--gap) * -1));
}
.slab strong {
  font-size: clamp(30px, 3.2vw, 42px);
  font-weight: 900;
  letter-spacing: -0.04em;
  line-height: 1;
  -webkit-text-stroke: 1px rgba(var(--holo-hi), 0.75);
  background: linear-gradient(90deg, rgba(var(--holo), 0.2) 0%, rgba(var(--holo-hi), 0.95) 35%,
    rgba(var(--holo), 0.7) 60%, rgba(var(--holo), 0.22) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  filter: drop-shadow(0 8px 16px rgba(0, 0, 0, 0.55));
}
.slab small {
  white-space: nowrap;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  color: rgba(var(--holo-hi), 0.7);
}
.slab:not(.slab--3) small { visibility: hidden; }
.slab--1 { --i: 2; opacity: 0.45; filter: blur(1px); border-color: rgba(var(--holo), 0.3); }
.slab--2 { --i: 1; opacity: 0.7; filter: blur(0.4px); }
.slab--3 { --i: 0; opacity: 1; border-color: rgba(var(--holo), 0.55); }
@media (max-width: 700px) { .tile--layers { min-height: 540px; } .layers { top: 44%; } }
@media (prefers-reduced-motion: reduce) { .layers-rot { animation: none; transform: rotateX(16deg) rotateY(-14deg); } }

.tile--count { justify-content: space-between; background: var(--bg-2); box-shadow: var(--shadow-soft); }
.orb-row { display: flex; }
.orb-row .orb { width: 34px; height: 34px; margin-left: -8px; }
.orb-row .orb:first-child { margin-left: 0; }
.big-num {
  display: flex;
  align-items: baseline;
  gap: 4px;
  font-size: 56px;
  font-weight: 800;
  letter-spacing: -0.05em;
  line-height: 1;
}
.big-num small { font-size: 0.55em; font-weight: 700; color: var(--ink-soft); }

.tile--govern { justify-content: space-between; }
.lock-orb {
  position: relative;
  width: 64px;
  height: 64px;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background: radial-gradient(circle at 30% 30%, #c9e37b 0%, #6b9d2c 60%, #2f5810);
  box-shadow: 0 12px 22px -6px rgba(40, 30, 10, 0.25), inset 0 2px 0 rgba(255, 255, 255, 0.3),
    inset 0 -2px 4px rgba(40, 30, 10, 0.2);
}
.lock-orb svg { width: 26px; height: 26px; }

.tile--alerts { grid-column: span 2; }
.tile--alerts .tile-copy { max-width: 42%; }
.alert-stack {
  position: absolute;
  top: 24px;
  right: 24px;
  width: 54%;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.alert {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 12px 14px;
  border-radius: 16px;
  background: var(--bg);
  box-shadow: var(--shadow-soft);
}
.alert .orb { width: 24px; height: 24px; }
.alert strong { display: block; font-size: 13px; font-weight: 600; letter-spacing: -0.01em; }
.alert span { font-size: 11px; color: var(--mute); }

/* ---------- Customer stories ---------- */
.stories {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 0.9fr 1.4fr;
  gap: 22px;
}
/* Orbs stack in one grid cell, so no centering transform fights GSAP */
.story-art {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 34px;
  min-height: 420px;
  border-radius: 28px;
  overflow: hidden;
  background: radial-gradient(60% 55% at 50% 45%, rgba(191, 213, 143, 0.14), transparent 70%), var(--ink);
  box-shadow: var(--shadow-dark);
}
/* Holographic customer initial; swaps with the testimonial */
.story-holo {
  position: relative;
  width: min(200px, 56%);
  aspect-ratio: 1;
  perspective: 900px;
  font-size: clamp(120px, 13vw, 168px);
}
@media (max-width: 1000px) {
  .story-art { min-height: 300px; gap: 22px; }
  .story-holo { width: 150px; font-size: 118px; }
}
.story-co {
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.32em;
  text-transform: uppercase;
  color: rgba(215, 240, 140, 0.75);
}
.story-orb {
  grid-area: 1 / 1;
  width: min(58%, 260px);
  aspect-ratio: 1;
  border-radius: 50%;
  opacity: 0;
  box-shadow: 0 40px 60px -20px rgba(60, 30, 10, 0.5);
}
.story-orb.is-active { opacity: 1; }
.story-orb::after {
  content: "";
  display: block;
  height: 100%;
  border-radius: inherit;
  background: radial-gradient(circle at 30% 25%, rgba(255, 255, 255, 0.55) 0%, transparent 35%);
}
.story-orb--purple { background: radial-gradient(circle at 35% 30%, #c7a6f7, #8b5bd9 60%, #5e3da0); }
.story-orb--gold { background: radial-gradient(circle at 35% 30%, #ffe078, #e0a82e 60%, #966d14); }
.story-orb--green { background: radial-gradient(circle at 35% 30%, #d7f08c, #8fb852 45%, #4a6e22); }

.story-card {
  display: flex;
  flex-direction: column;
  gap: 40px;
  padding: 48px;
  border-radius: 28px;
  background: #fff;
  box-shadow: var(--shadow-card);
}
.story-stack { display: grid; flex: 1; }
.story {
  grid-area: 1 / 1;
  display: flex;
  flex-direction: column;
  gap: 32px;
  opacity: 0;
  visibility: hidden;
}
.story.is-active { opacity: 1; visibility: visible; }
.story blockquote {
  font-size: clamp(22px, 2.3vw, 32px);
  font-weight: 600;
  line-height: 1.25;
  letter-spacing: -0.025em;
}
.story-author { display: flex; align-items: center; gap: 14px; flex-wrap: wrap; margin-top: auto; }
.story-author .face {
  width: 48px;
  height: 48px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  flex-shrink: 0;
  background: var(--ink);
  color: var(--green);
  box-shadow: 0 6px 14px -4px rgba(20, 10, 5, 0.3), inset 0 0 0 1px rgba(191, 213, 143, 0.35);
}
.story-author .face svg { width: 24px; height: 24px; }
.story-author strong { display: block; font-size: 15px; font-weight: 700; }
.story-author strong + span { display: block; font-size: 13px; color: var(--mute); }
.story-metric {
  margin-left: auto;
  color: var(--ink);
  padding: 8px 16px;
  border-radius: 999px;
  background: var(--green);
  font-size: 13px;
  font-weight: 600;
  box-shadow: 0 10px 18px -8px rgba(60, 100, 30, 0.35), inset 0 2px 0 rgba(255, 255, 255, 0.4),
    inset 0 -2px 4px rgba(60, 100, 30, 0.2);
}
.story-controls { display: flex; justify-content: space-between; align-items: center; }
.story-count {
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.08em;
  color: var(--mute);
  font-variant-numeric: tabular-nums;
}
.story-nav { display: flex; gap: 10px; }
.round {
  width: 48px;
  height: 48px;
  border: none;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  background: var(--bg-2);
  color: var(--ink);
  cursor: pointer;
  box-shadow: var(--shadow-soft);
  transition: transform 0.4s var(--ease-soft);
}
.round:hover { transform: translateY(-2px); }
.round--dark { background: var(--ink); color: #fafaf7; box-shadow: var(--shadow-pill); }

/* ---------- Pricing ---------- */
.billing { display: inline-flex; align-items: center; gap: 14px; font-size: 14px; font-weight: 600; }
.billing-label { transition: color 0.3s; }
.billing-label.is-dim { color: var(--mute); }
.switch {
  position: relative;
  width: 64px;
  height: 34px;
  border: none;
  border-radius: 999px;
  background: var(--bg-2);
  cursor: pointer;
  box-shadow: inset 0 2px 5px rgba(40, 30, 10, 0.18), inset 0 -1px 0 rgba(255, 255, 255, 0.6);
}
.switch i {
  position: absolute;
  top: 4px;
  left: 4px;
  width: 26px;
  height: 26px;
  border-radius: 50%;
  background: var(--ink);
  box-shadow: var(--shadow-pill);
  transition: transform 0.45s var(--ease-soft);
}
.switch[aria-checked="true"] i { transform: translateX(30px); }
.switch:focus-visible { outline: 2px solid var(--green-dark); outline-offset: 3px; }
.save-badge {
  padding: 5px 10px;
  border-radius: 999px;
  background: var(--green);
  font-size: 11px;
  font-weight: 700;
  box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.4), inset 0 -2px 4px rgba(60, 100, 30, 0.2);
}

.plans {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
  align-items: stretch;
}
.plan {
  position: relative;
  display: flex;
  flex-direction: column;
  gap: 22px;
  padding: 34px;
  border-radius: 28px;
  background: #fff;
  box-shadow: var(--shadow-card);
  overflow: hidden;
  transition: transform 0.5s var(--ease-soft);
}
.plan:hover { transform: translateY(-8px); }
.plan > * { position: relative; }
.plan-name { display: flex; justify-content: space-between; align-items: center; font-size: 15px; font-weight: 700; }
.plan-name .orb { width: 34px; height: 34px; }
.plan-price { display: flex; align-items: baseline; gap: 6px; flex-wrap: wrap; }
.plan-price strong {
  font-size: 56px;
  font-weight: 800;
  letter-spacing: -0.05em;
  line-height: 1;
  font-variant-numeric: tabular-nums;
}
.plan-price span { font-size: 13px; color: var(--mute); }
.plan-desc { font-size: 14px; line-height: 1.55; color: var(--ink-soft); }
.plan ul {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 12px;
  padding-top: 22px;
  border-top: 1px solid var(--line);
  list-style: none;
}
.plan li { display: flex; align-items: flex-start; gap: 10px; font-size: 14px; line-height: 1.45; }
.plan li::before {
  content: "";
  flex-shrink: 0;
  width: 18px;
  height: 18px;
  margin-top: 1px;
  border-radius: 50%;
  background: var(--green) url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%230d0d10' stroke-width='3.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='5 12 10 17 19 7'/%3E%3C/svg%3E") center / 10px no-repeat;
  box-shadow: inset 0 -1px 2px rgba(60, 100, 30, 0.3);
}
.plan-cta { width: 100%; }
.plan-cta--ghost { background: transparent; color: var(--ink); box-shadow: inset 0 0 0 1.5px var(--ink); }
.plan--featured { background: var(--ink); color: #f4f0eb; box-shadow: var(--shadow-dark); }
.plan--featured::before {
  content: "";
  position: absolute;
  width: 420px;
  height: 420px;
  top: -200px;
  left: -120px;
  border-radius: 50%;
  background: radial-gradient(circle, rgba(191, 213, 143, 0.25), transparent 65%);
  filter: blur(30px);
}
.plan--featured .plan-desc,
.plan--featured .plan-price span { color: rgba(255, 255, 255, 0.6); }
.plan--featured ul { border-color: rgba(255, 255, 255, 0.12); }
.plan--featured .plan-cta { background: #fff; color: var(--ink); }
.popular {
  padding: 6px 12px;
  border-radius: 999px;
  background: var(--green);
  color: var(--ink);
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.04em;
}
.plans-note { margin-top: 34px; text-align: center; font-size: 13px; color: var(--mute); }

/* ---------- Resources ---------- */
.resources {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}
.res-card {
  display: flex;
  flex-direction: column;
  gap: 16px;
  padding: 14px 14px 24px;
  border-radius: 26px;
  background: var(--bg-2);
  box-shadow: var(--shadow-soft);
  color: var(--ink);
  text-decoration: none;
  transition: transform 0.5s var(--ease-soft);
}
.res-card:hover { transform: translateY(-6px); }
.res-thumb {
  position: relative;
  height: 200px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: inset 0 2px 0 rgba(255, 255, 255, 0.2), inset 0 -2px 4px rgba(60, 30, 10, 0.2);
}
.res-art { position: absolute; inset: 0; transition: transform 0.8s var(--ease-soft); }
.res-card:hover .res-art { transform: scale(1.06); }
.res-art .orb { position: absolute; }
.res-art--coral {
  background: radial-gradient(ellipse at 30% 40%, #ffc97a 0%, transparent 55%),
    radial-gradient(ellipse at 65% 65%, #e25c2c 0%, transparent 55%),
    radial-gradient(ellipse at 50% 80%, rgba(180, 40, 0, 0.3), transparent 50%),
    linear-gradient(180deg, #f0e4d0, #c8b8a0);
}
.res-art--purple {
  background: radial-gradient(ellipse at 30% 40%, #c9a6f4 0%, transparent 55%),
    radial-gradient(ellipse at 65% 65%, #8053c6 0%, transparent 55%),
    radial-gradient(ellipse at 50% 80%, rgba(60, 30, 80, 0.4), transparent 50%),
    linear-gradient(180deg, #e0cff0, #a88bc8);
}
.res-art--green {
  background: radial-gradient(ellipse at 35% 40%, #e4f5a8 0%, transparent 55%),
    radial-gradient(ellipse at 65% 65%, #6b9d2c 0%, transparent 55%),
    radial-gradient(ellipse at 50% 85%, rgba(40, 70, 10, 0.35), transparent 50%),
    linear-gradient(180deg, #eef3dc, #b9c79a);
}
.res-tag {
  position: absolute;
  top: 14px;
  left: 14px;
  z-index: 2;
  padding: 6px 12px;
  border-radius: 999px;
  background: rgba(239, 237, 232, 0.82);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
}
.res-card h3 { padding: 0 8px; font-size: 19px; font-weight: 700; letter-spacing: -0.02em; line-height: 1.25; }
.res-meta {
  display: flex;
  justify-content: space-between;
  padding: 0 8px;
  margin-top: auto;
  font-size: 12px;
  font-weight: 500;
  color: var(--mute);
}

/* ---------- Footer ---------- */
.footer { position: relative; z-index: 5; padding: 20px 40px 30px; overflow: hidden; }
.footer-top {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 1.6fr repeat(3, 1fr);
  gap: 40px;
  padding-bottom: 40px;
}
.footer-brand p { margin: 10px 0 20px; font-size: 14px; color: var(--ink-soft); }
.newsletter {
  display: flex;
  gap: 8px;
  max-width: 380px;
  padding: 6px;
  border-radius: 999px;
  background: var(--bg-2);
  box-shadow: inset 0 2px 5px rgba(40, 30, 10, 0.12), inset 0 -1px 0 rgba(255, 255, 255, 0.6);
}
.newsletter input {
  flex: 1;
  min-width: 0;
  padding: 0 16px;
  border: none;
  background: transparent;
  color: var(--ink);
  font-family: inherit;
  font-size: 14px;
  font-weight: 500;
  outline: none;
}
.newsletter input::placeholder { color: var(--mute); }
.newsletter .contact-pill { padding: 11px 22px; }
.nl-status { min-height: 18px; margin-top: 10px; padding-left: 16px; font-size: 12px; font-weight: 600; color: var(--green-dark); }
.footer-col h4 {
  margin-bottom: 16px;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: var(--mute);
}
.footer-col a {
  display: block;
  width: fit-content;
  padding: 5px 0;
  color: var(--ink-soft);
  text-decoration: none;
  font-size: 14px;
  font-weight: 500;
  transition: color 0.3s;
}
.footer-col a:hover { color: var(--ink); }
.footer-mark {
  margin: 0 -40px;
  text-align: center;
  font-size: 25vw;
  font-weight: 900;
  line-height: 0.8;
  letter-spacing: -0.07em;
  white-space: nowrap;
  background: linear-gradient(180deg, rgba(13, 13, 16, 0.14), rgba(13, 13, 16, 0) 85%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  user-select: none;
  pointer-events: none;
}
/* The disclaimer, which is not fine print here: every number, quote and
   customer on this page is invented. */
.footer-legal {
  max-width: 1280px;
  margin: 0 auto 18px;
  font-size: 12px;
  line-height: 1.55;
  color: var(--mute);
}

.footer-bottom {
  max-width: 1280px;
  margin: 0 auto;
  padding-top: 22px;
  border-top: 1px solid var(--line);
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 14px;
  font-size: 13px;
  color: var(--mute);
}
.footer-bottom a { color: inherit; text-decoration: none; transition: color 0.3s; }
.footer-bottom a:hover { color: var(--ink); }
.status { display: inline-flex; align-items: center; gap: 8px; }

/* Responsive */
@media (max-width: 1000px) {
  .cta-inner {
    grid-template-columns: 1fr;
    padding: 50px 30px;
  }
  .features-grid {
    grid-template-columns: 1fr 1fr;
  }

  .demo { grid-template-columns: 1fr; }
  .demo-tabs { display: grid; grid-template-columns: repeat(3, 1fr); }
  .demo-tab { grid-template-columns: 1fr; gap: 6px; }
  .bento { grid-template-columns: repeat(2, 1fr); }
  .stories { grid-template-columns: 1fr; }
  .story-art { min-height: 260px; }
  .plans { grid-template-columns: 1fr; max-width: 560px; }
  .footer-top { grid-template-columns: repeat(3, 1fr); }
  .footer-brand { grid-column: 1 / -1; }
}
@media (max-width: 700px) {
  .nav {
    padding: 14px 18px;
  }
  .nav-links {
    display: none;
  }
  .hero {
    padding: 100px 18px 24px;
  }
  .headline .line {
    gap: 12px;
    flex-wrap: wrap; /* line 2 (blob + word + pill) is wider than a phone */
  }
  .features {
    padding: 40px 18px;
  }
  .features-grid {
    grid-template-columns: 1fr;
  }
  .cta-section {
    padding: 20px 18px 60px;
  }

  .section { padding: 60px 18px; }
  .demo-tabs { gap: 8px; }
  .demo-tab { gap: 2px; padding: 14px 14px 22px; border-radius: 20px; }
  .demo-tab strong { margin-bottom: 0; font-size: 16px; }
  .demo-tab-copy > span { display: none; }
  .demo-tab-bar { left: 14px; right: 14px; bottom: 10px; }
  .demo-window { min-height: 520px; }
  .panel { padding: 20px; }
  .src { left: clamp(58px, var(--x), calc(100% - 58px)); }
  .src-chip { gap: 6px; padding: 5px 10px 5px 5px; font-size: 11px; }
  .src-chip .orb { width: 20px; height: 20px; }
  .hub { width: 84px; height: 84px; font-size: 64px; }
  .kpi { padding: 12px; }
  .kpi strong { font-size: 18px; }
  .ask-meta { display: none; }
  .bento { grid-template-columns: 1fr; grid-auto-rows: minmax(230px, auto); }
  .tile--layers,
  .tile--alerts { grid-column: auto; }
  .tile--alerts { gap: 20px; }
  .tile--alerts .tile-copy { max-width: none; }
  .alert-stack { position: static; width: 100%; }
  .story-card { padding: 28px; gap: 28px; }
  .story-metric { margin-left: 0; }
  .plan { padding: 26px; }
  .resources { grid-template-columns: 1fr; }
  .footer { padding: 10px 18px 24px; }
  .footer-top { grid-template-columns: 1fr 1fr; }
  .footer-mark { margin: 0 -18px; }
  .footer-bottom { flex-direction: column; }
}
@media (prefers-reduced-motion: reduce) {
  .logo-track,
  .wires line,
  .hub-holo { animation: none; }
}

/* ============ HOLOGRAPHIC SCENES: CTA + resources ============
   Same material as the Connect hub: dark glass, 1px green outline,
   outlined gradient glyphs, slow 3D motion. */
.cta-inner,
.res-thumb {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
}

/* CTA headline: outlined lettering with a faint echo set back behind it */
.cta-inner h2 em {
  position: relative;
  display: inline-block;
  font-weight: 900;
  -webkit-text-stroke: 1px rgba(var(--holo-hi), 0.85);
  background: linear-gradient(90deg, rgba(var(--holo), 0.2) 0%, rgba(var(--holo-hi), 0.95) 35%,
    rgba(var(--holo), 0.7) 60%, rgba(var(--holo), 0.25) 100%);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.cta-inner h2 em::after {
  content: attr(data-echo);
  position: absolute;
  left: 0;
  top: 0;
  z-index: -1;
  -webkit-text-stroke: 1px rgba(var(--holo), 0.3);
  color: transparent;
  transform: translate(0.035em, 0.05em);
  opacity: 0.7;
}

/* CTA orbit: three tilted rings carry the team around a holographic chart */
.cta-orbit {
  position: relative;
  height: 200px;
  margin-bottom: 18px;
  perspective: 900px;
}
.orbit-rings {
  position: absolute;
  inset: 0;
  transform-style: preserve-3d;
  transform: rotateX(62deg);
}
.ring {
  position: absolute;
  left: 50%;
  top: 50%;
  width: var(--d);
  height: var(--d);
  translate: -50% -50%;
  border-radius: 50%;
  border: 1px solid rgba(var(--holo), var(--a));
  transform-style: preserve-3d;
  animation: orbit var(--t) linear infinite;
}
.ring--1 { --d: min(290px, 96%); --a: 0.28; --t: 22s; }
.ring--2 { --d: min(210px, 70%); --a: 0.4; --t: 15s; animation-direction: reverse; }
.ring--3 { --d: min(130px, 44%); --a: 0.55; --t: 10s; }
@keyframes orbit { to { transform: rotate(360deg); } }
.ring > i {
  position: absolute;
  top: -7px;
  left: calc(50% - 7px);
  width: 14px;
  height: 14px;
  border-radius: 50%;
  /* counter-tilt so the orb faces the viewer instead of lying flat */
  transform: rotateX(-62deg);
  box-shadow: 0 0 14px 2px rgba(var(--holo), 0.35), inset 0 -2px 3px rgba(0, 0, 0, 0.3);
}
.ring > i:nth-child(2) { top: auto; bottom: -7px; }
.orbit-core {
  position: absolute;
  left: 50%;
  top: 50%;
  translate: -50% -58%;
  width: 84px;
  height: 64px;
  padding: 10px 12px;
  display: flex;
  align-items: flex-end;
  gap: 6px;
  border-radius: 16px;
  border: 1px solid rgba(var(--holo), 0.5);
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), transparent 50%), rgba(13, 13, 16, 0.85);
  box-shadow: 0 18px 30px -12px rgba(0, 0, 0, 0.8), 0 0 30px rgba(var(--holo), 0.12);
  animation: holo-wobble 6.2s ease-in-out infinite;
}
.orbit-core i {
  flex: 1;
  height: var(--h);
  border-radius: 4px 4px 2px 2px;
  border: 1px solid rgba(var(--holo-hi), 0.7);
  background: linear-gradient(180deg, rgba(var(--holo-hi), 0.45), rgba(var(--holo), 0.06));
  transform-origin: bottom;
  animation: bar-breathe 2.8s ease-in-out infinite alternate;
  animation-delay: calc(var(--n) * -0.7s);
}
@keyframes bar-breathe { from { transform: scaleY(0.7); } to { transform: scaleY(1); } }

/* Resource thumbnails: one holographic scene per format */
.res-art.holo-scene {
  display: grid;
  place-items: center;
  background: radial-gradient(65% 70% at 50% 50%, rgba(var(--holo), 0.14), transparent 70%), var(--ink);
  perspective: 800px;
}
/* Guide: isometric stack that turns slowly and spreads on hover */
.rs-stack {
  position: relative;
  width: 140px;
  height: 104px;
  transform-style: preserve-3d;
  animation: rs-turn 7s ease-in-out infinite alternate;
}
@keyframes rs-turn {
  from { transform: rotateX(58deg) rotateZ(-40deg); }
  to { transform: rotateX(54deg) rotateZ(-20deg); }
}
.rs-stack i {
  position: absolute;
  inset: 0;
  border-radius: 16px;
  border: 1px solid rgba(var(--holo), var(--a));
  background: linear-gradient(120deg, rgba(255, 255, 255, 0.08), transparent 50%), rgba(13, 13, 16, 0.78);
  transform: translateZ(calc(var(--n) * 20px));
  box-shadow: 0 16px 24px -12px rgba(0, 0, 0, 0.8);
  transition: transform 0.6s var(--ease-soft);
}
.rs-stack i:nth-child(1) { --n: 0; --a: 0.3; }
.rs-stack i:nth-child(2) { --n: 1; --a: 0.5; }
.rs-stack i:nth-child(3) { --n: 2; --a: 0.85; box-shadow: 0 0 24px rgba(var(--holo), 0.25); }
.res-card:hover .rs-stack i { transform: translateZ(calc(var(--n) * 34px)); }
/* Case study: 2 days struck out, 4h in holographic depth */
.rs-num { display: grid; justify-items: center; gap: 12px; }
.rs-num s {
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(244, 240, 235, 0.45);
  text-decoration-color: rgba(var(--holo-hi), 0.8);
}
.rs-glyph {
  position: relative;
  width: 170px;
  height: 104px;
  font-size: 96px;
  perspective: 900px;
}
.rs-glyph .hub-holo::after,
.rs-glyph .hub-holo::before { display: none; }
/* Webinar: a glass speech bubble holding a question, voice waveform below */
.rs-talk { display: grid; justify-items: center; gap: 14px; }
.rs-bubble {
  position: relative;
  width: 104px;
  height: 84px;
  font-size: 66px;
  perspective: 900px;
}
.rs-bubble .hub-holo { border-radius: 24px 24px 24px 6px; }
.rs-bubble .hub-holo::after { border-radius: inherit; border-color: rgba(var(--holo), 0.55); }
.rs-wave { display: flex; align-items: center; gap: 4px; height: 20px; }
.rs-wave i {
  width: 4px;
  height: 100%;
  border-radius: 2px;
  background: rgba(var(--holo-hi), 0.8);
  animation: wave 1.1s ease-in-out infinite alternate;
  animation-delay: calc(var(--n) * -0.18s);
}
@keyframes wave { from { transform: scaleY(0.25); } to { transform: scaleY(1); } }
.res-tag { background: rgba(13, 13, 16, 0.6); color: rgba(var(--holo-hi), 0.9); border: 1px solid rgba(var(--holo), 0.35); }

@media (prefers-reduced-motion: reduce) {
  .ring, .orbit-core, .orbit-core i, .rs-stack, .rs-wave i { animation: none; }
}

/* ============ Governed tile + pricing: hero card recipe ============
   Vertical four-stop gradient from the orb palette, a glossy sheen,
   inset highlights and a colour-tinted drop shadow. */
.tile--govern,
.plan.p-sand,
.plan.p-purple {
  background: linear-gradient(180deg, var(--c1) 0%, var(--c2) 35%, var(--c3) 70%, var(--c4) 100%);
  box-shadow: 0 30px 50px -16px rgba(var(--sh), 0.45), 0 14px 26px -8px rgba(var(--sh), 0.28),
    inset 0 2px 0 rgba(255, 255, 255, 0.4), inset 0 -4px 8px rgba(var(--sh), 0.35);
}
.tile--govern::before,
.plan.p-sand::before,
.plan.p-purple::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  pointer-events: none;
  background: linear-gradient(155deg, rgba(255, 255, 255, 0.26) 0%, transparent 30%,
    transparent 70%, rgba(var(--sh), 0.2) 100%);
}
.tile--govern > * { position: relative; }
.tile--govern { --c1: #3d6f88; --c2: #6fa8c3; --c3: #b5e3f2; --c4: #e6f5fa; --sh: 40, 80, 110; }
.tile--govern .lock-orb {
  background: rgba(255, 255, 255, 0.2);
  border: 1px solid rgba(255, 255, 255, 0.4);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  box-shadow: 0 12px 22px -8px rgba(20, 50, 70, 0.45), inset 0 1px 0 rgba(255, 255, 255, 0.5);
}

.plan.p-sand { --c1: #8a7050; --c2: #b38d5e; --c3: #d9c29c; --c4: #f4ead6; --sh: 100, 75, 40; }
.plan.p-purple { --c1: #4e3290; --c2: #7a4fc8; --c3: #ad8ade; --c4: #e6d8f6; --sh: 80, 45, 130; }
.plan.p-sand,
.plan.p-purple { color: #fafaf7; }
.plan.p-sand .plan-desc,
.plan.p-purple .plan-desc { color: rgba(255, 255, 255, 0.82); }
.plan.p-sand .plan-price span,
.plan.p-purple .plan-price span { color: rgba(255, 255, 255, 0.72); }
/* feature list in a frosted panel, like the hero cards' captions */
.plan.p-sand ul,
.plan.p-purple ul {
  padding: 20px;
  border: 1px solid rgba(255, 255, 255, 0.14);
  border-radius: 18px;
  background: rgba(13, 13, 16, 0.55);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}
.plan.p-sand .plan-cta--ghost,
.plan.p-purple .plan-cta--ghost { background: var(--ink); color: #fafaf7; box-shadow: var(--shadow-pill); }

/* Team: the holographic plan */
.plan--featured {
  --holo: 191, 213, 143;
  --holo-hi: 215, 240, 140;
  background: radial-gradient(70% 45% at 80% 12%, rgba(191, 213, 143, 0.16), transparent 70%), var(--ink);
  outline: 1px solid rgba(191, 213, 143, 0.4);
  outline-offset: -1px;
}
.plan--featured .plan-name { justify-content: flex-start; gap: 10px; }
.seat-holo {
  position: absolute;
  top: 22px;
  right: 22px;
  z-index: 1;
  width: 96px;
  height: 96px;
  perspective: 900px;
}
.seat-holo .hub-layer { width: 70%; display: block; }
.seat-holo svg {
  display: block;
  width: 100%;
  fill: none;
  stroke: rgba(var(--holo-hi), 0.9);
  stroke-width: 1.6;
  stroke-linecap: round;
  filter: drop-shadow(0 6px 10px rgba(0, 0, 0, 0.5));
}
@media (max-width: 700px) { .seat-holo { width: 78px; height: 78px; top: 16px; right: 16px; } }

/* Headline badges: left pill takes the Live dashboard card's dithered field,
   right pill takes the Revenue card's glossy green gradient */
.inline-img[data-fx]::before { background: none; }
.inline-img[data-fx]::after {
  background: linear-gradient(155deg, rgba(255, 255, 255, 0.26) 0%, transparent 30%,
    transparent 70%, rgba(100, 40, 50, 0.2) 100%);
}
.idea-pill {
  background: linear-gradient(180deg, #4a6e22 0%, #7fa645 35%, #bfd58f 70%, #e4f5a8 100%);
  box-shadow: 0 30px 50px -16px rgba(60, 100, 30, 0.45), 0 14px 26px -8px rgba(60, 100, 30, 0.28),
    inset 0 2px 0 rgba(255, 255, 255, 0.4), inset 0 -4px 8px rgba(60, 100, 30, 0.35);
  position: relative;
  overflow: hidden;
}
.idea-pill::before {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  pointer-events: none;
  background: linear-gradient(155deg, rgba(255, 255, 255, 0.26) 0%, transparent 30%,
    transparent 70%, rgba(60, 100, 30, 0.2) 100%);
}
.idea-pill > * { position: relative; }
.idea-pill .txt { color: #fafaf7; font-weight: 700; text-shadow: 0 1px 2px rgba(40, 70, 15, 0.45); }

/* Eyebrow dots glow in the Revenue card's green: white core, then a tight
   and a wide halo, stacked as drop shadows */
.eyebrow::before {
  background: radial-gradient(circle at 40% 35%, #e4f5a8 0%, #bfd58f 45%, #7fa645 100%);
  box-shadow: none;
  filter: drop-shadow(0 0 2px rgba(255, 255, 255, 0.9))
    drop-shadow(0 0 6px rgba(143, 184, 82, 0.8))
    drop-shadow(0 0 14px rgba(127, 166, 69, 0.5));
  animation: eyebrow-glow 3.2s ease-in-out infinite;
}
@keyframes eyebrow-glow {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.72; }
}
@media (prefers-reduced-motion: reduce) { .eyebrow::before { animation: none; } }
/* Avatars are drawn, not fetched. The rest of this page is CSS and inline
   SVG, and the four photos these replace were its only image requests. Orb
   recipe for the disc, the story byline's own person glyph on top. */
:root {
  --face-glyph: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23ffffff' stroke-opacity='0.88' stroke-width='1.7' stroke-linecap='round'%3E%3Ccircle cx='12' cy='8.5' r='3.6'/%3E%3Cpath d='M5 19.5c1.2-3.4 3.9-5.2 7-5.2s5.8 1.8 7 5.2'/%3E%3C/svg%3E");
}
.ask-avatar,
.avatar-stack > * {
  background-repeat: no-repeat;
  background-position: center 58%, center;
  background-size: 116%, cover;
}
.av-a { background-image: var(--face-glyph), radial-gradient(circle at 35% 30%, #c7a6f7, #8b5bd9 60%, #5e3da0); }
.av-b { background-image: var(--face-glyph), radial-gradient(circle at 35% 30%, #ffd66b, #e26a4d 60%, #8a2818); }
.av-c { background-image: var(--face-glyph), radial-gradient(circle at 35% 30%, #d7f08c, #8fb852 45%, #4a6e22); }

/* ============ DITHERED FIELD ============
   A halftone material, not a page background. Any element carrying data-fx
   gets a WebGL canvas laid into it that replaces its gradient fill with a
   dithered field mixed from that element's own colours. The CSS gradient
   underneath is what shows if WebGL is missing, so nothing depends on it. */
/* isolation gives the host a stacking context of its own, so the layer can sit
   at z-index -1: above the element's background, below its ::before/::after
   gloss and every child, and with no way to escape behind the section. */
[data-fx] { position: relative; isolation: isolate; }
.fx-layer {
  position: absolute;
  inset: 0;
  z-index: -1;
  width: 100%;
  height: 100%;
  display: block;
  border-radius: inherit;
  pointer-events: none;
}

</style>

<div class="grain" aria-hidden="true"></div>

<!-- ============ NAV ============ -->
<nav class="nav" data-section="nav" aria-label="Primary">
  <div class="logo">Monax</div>
  <ul class="nav-links">
    <li><a href="#product">Products
        <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" aria-hidden="true">
          <polyline points="6 9 12 15 18 9" />
        </svg>
      </a></li>
    <li><a href="#pricing">Pricing
        <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" aria-hidden="true">
          <polyline points="6 9 12 15 18 9" />
        </svg>
      </a></li>
    <li><a href="#platform">About</a></li>
    <li><a href="#resources">Resources
        <svg width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" aria-hidden="true">
          <polyline points="6 9 12 15 18 9" />
        </svg>
      </a></li>
  </ul>
  <button class="contact-pill" data-target="#contact">Contact us</button>
</nav>

<!-- ============ HERO ============ -->
<section class="hero" data-section="hero">
  <p class="eyebrow hero-eyebrow" id="heroEyebrow"><span><b>120+</b> data teams · <b>200+</b> connectors</span></p>
  <h1 class="headline" id="headline">
    <div class="line line-1">
      <span class="word"><span>Business</span></span>
      <span class="word"><span>Teams</span></span>
    </div>
    <div class="line line-2">
      <span class="inline-img" id="inlineImg" data-fx data-fx-ink="#8163c6,#f2a03b,#e83a4d,#7bafce" data-fx-paper="#f2ece0,#e8e0ce,#c8b89e" data-fx-coverage="0.92" data-fx-density="0.55"></span>
      <span class="word"><span>Around</span></span>
      <span class="idea-pill" id="ideaPill">
        <span class="txt">Behind every<br />great idea</span>
        <span class="leaf"></span>
      </span>
    </div>
    <div class="line line-3">
      <span class="word"><span>Analytical</span></span>
      <span class="word"><span>Work</span></span>
    </div>
  </h1>
</section>

<!-- ============ BELOW HERO: fanned card stack ============ -->
<section class="fan-section" data-section="fan-stack" aria-label="What your team sees in Monax">
  <div class="fan-stage" id="fanStage">
    <div class="fan-ghost" aria-hidden="true"><span class="gl">r</span><span class="gl">e</span><span class="gl">a</span><span class="gl">l</span><span class="gl">&nbsp;</span><span class="gl">a</span><span class="gl">n</span><span class="gl">s</span><span class="gl">w</span><span class="gl">e</span><span class="gl">r</span><span class="gl">s</span></div>

    <div class="fan" id="fan">
      <div class="fan-slot s1" style="--w:130px; --h:180px; --y:-10px; --z:1" data-rot="-9" data-depth="14">
        <div class="fan-card"><div class="fan-face f-coral">
          <span class="f-live"><i></i>Live</span>
          <div class="f-meta"><b>Freshness</b><span>2 min ago</span></div>
        </div></div>
      </div>

      <div class="fan-slot s2" style="--w:160px; --h:220px; --y:12px; --z:2" data-rot="-5" data-depth="10">
        <div class="fan-card"><div class="fan-face f-green">
          <div class="f-kpi"><strong>$4.2M</strong><em>▲ 12.4%</em></div>
          <div class="f-meta"><b>Revenue</b><span>This quarter</span></div>
        </div></div>
      </div>

      <div class="fan-slot s3" style="--w:200px; --h:270px; --y:-18px; --z:3" data-rot="-2" data-depth="8">
        <div class="fan-card"><div class="fan-face f-holo">
          <span class="f-live"><i></i>Synced just now</span>
          <div class="f-hub" aria-hidden="true"><div class="hub-holo"><span class="hub-layer hub-layer--back">M</span><span class="hub-layer hub-layer--mid">M</span><span class="hub-layer hub-layer--front">M</span></div></div>
          <div class="f-meta"><b>Connect</b><span>6 sources synced</span></div>
        </div></div>
      </div>

      <div class="fan-slot s4" style="--w:150px; --h:200px; --y:26px; --z:4" data-rot="3" data-depth="12">
        <div class="fan-card"><div class="fan-face f-gold">
          <div class="f-bars" aria-hidden="true"><i style="--b:100%"></i><i style="--b:72%"></i><i style="--b:52%"></i><i style="--b:34%"></i></div>
          <div class="f-meta"><b>Regions</b><span>EMEA up 32%</span></div>
        </div></div>
      </div>

      <div class="fan-slot s5" style="--w:230px; --h:310px; --y:-24px; --z:5" data-rot="0" data-depth="6">
        <div class="fan-card"><div class="fan-face f-hero" data-fx data-fx-ink="#8163c6,#f2a03b,#e83a4d,#7bafce" data-fx-paper="#f2ece0,#e8e0ce,#c8b89e" data-fx-coverage="0.92" data-fx-density="1.3">
          <span class="f-live f-live--dark"><i></i>3 viewing</span>
<div class="f-meta"><b>Live dashboard</b><span>Shared with #growth</span></div>
        </div></div>
      </div>

      <div class="fan-slot s6" style="--w:160px; --h:215px; --y:16px; --z:4" data-rot="4" data-depth="11">
        <div class="fan-card"><div class="fan-face f-blue">
          <div class="f-donut-wrap"><div class="f-donut" style="width:74%"></div><strong>2.3%</strong></div>
          <div class="f-meta"><b>Churn</b><span>Down 0.4 pt</span></div>
        </div></div>
      </div>

      <div class="fan-slot s7" style="--w:175px; --h:240px; --y:-8px; --z:3" data-rot="7" data-depth="9">
        <div class="fan-card"><div class="fan-face f-sand" data-fx data-fx-ink="#c99368,#e0a82e,#8a7050,#f8d6a6" data-fx-paper="#f4ead6,#e8dcc6,#d4bc92" data-fx-coverage="0.85" data-fx-density="1.5">
          <p class="f-ask">Which regions grew fastest last quarter?</p>
          <div class="f-meta"><b>Ask Monax</b><span>Answered in 0.8s</span></div>
        </div></div>
      </div>

      <div class="fan-slot s8" style="--w:130px; --h:175px; --y:14px; --z:2" data-rot="-4" data-depth="13">
        <div class="fan-card"><div class="fan-face f-red f-end">
          <span class="f-alert" aria-hidden="true">!</span>
          <div class="f-meta"><b>Alerts</b><span>3 new today</span></div>
        </div></div>
      </div>
    </div>

    <div class="fan-cta" id="fanCta">
      <button class="arrow-pill" data-target="#pricing">
        Try for free
        <span class="ar"><svg width="13" height="13" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><line x1="7" y1="17" x2="17" y2="7" /><polyline points="7 7 17 7 17 17" /></svg></span>
      </button>
    </div>
  </div>

</section>

<!-- ============ LOGO MARQUEE ============ -->
<section class="logos" data-section="logos" aria-label="Teams using Monax">
  <p class="logos-label">Trusted by data-driven teams at</p>
  <div class="logo-marquee">
    <div class="logo-track">
      <span class="brand"><i class="orb orb--coral"></i>Northwind</span>
      <span class="brand brand--light">halcyon</span>
      <span class="brand brand--caps">Parabola</span>
      <span class="brand brand--italic"><i class="orb orb--purple"></i>Lumen&amp;Co</span>
      <span class="brand">Fieldstone</span>
      <span class="brand brand--light"><i class="orb orb--green"></i>orbital</span>
      <span class="brand brand--caps">Kestrel</span>
      <span class="brand brand--italic">Vantage</span>
    </div>
    <div class="logo-track" aria-hidden="true">
      <span class="brand"><i class="orb orb--coral"></i>Northwind</span>
      <span class="brand brand--light">halcyon</span>
      <span class="brand brand--caps">Parabola</span>
      <span class="brand brand--italic"><i class="orb orb--purple"></i>Lumen&amp;Co</span>
      <span class="brand">Fieldstone</span>
      <span class="brand brand--light"><i class="orb orb--green"></i>orbital</span>
      <span class="brand brand--caps">Kestrel</span>
      <span class="brand brand--italic">Vantage</span>
    </div>
  </div>
</section>

<!-- ============ PRODUCT DEMO ============ -->
<section class="section" id="product" data-section="product">
  <div class="sec-head">
    <div class="reveal">
      <div class="eyebrow">How it works · Three steps</div>
      <h2>From raw tables<br />to shared answers.</h2>
    </div>
    <p class="reveal">Connect once, ask in plain language, and share live views your whole team trusts. Here's the loop, end to end.</p>
  </div>

  <div class="demo">
    <div class="demo-tabs reveal" role="tablist" aria-label="Product walkthrough">
      <button class="demo-tab active" role="tab" id="dt-connect" aria-selected="true" aria-controls="demo-stage">
        <span class="demo-tab-num">01</span>
        <span class="demo-tab-copy"><strong>Connect</strong><span>Plug in warehouses, apps and spreadsheets in a few clicks. Monax keeps them in sync.</span></span>
        <span class="demo-tab-bar"><i></i></span>
      </button>
      <button class="demo-tab" role="tab" id="dt-ask" aria-selected="false" aria-controls="demo-stage" tabindex="-1">
        <span class="demo-tab-num">02</span>
        <span class="demo-tab-copy"><strong>Ask</strong><span>Type a question the way you'd ask a colleague. Get a chart and the reasoning behind it.</span></span>
        <span class="demo-tab-bar"><i></i></span>
      </button>
      <button class="demo-tab" role="tab" id="dt-share" aria-selected="false" aria-controls="demo-stage" tabindex="-1">
        <span class="demo-tab-num">03</span>
        <span class="demo-tab-copy"><strong>Share</strong><span>Pin answers to live dashboards, schedule digests, and see who's looking in real time.</span></span>
        <span class="demo-tab-bar"><i></i></span>
      </button>
    </div>

    <div class="demo-window reveal" id="demo-stage" role="tabpanel" aria-labelledby="dt-connect">
      <div class="win-bar"><i></i><i></i><i></i><span>monax.app / growth-workspace</span></div>
      <div class="win-body">

        <div class="panel panel-connect is-active">
          <svg class="wires" viewBox="0 0 100 100" preserveAspectRatio="none" aria-hidden="true">
            <line x1="14" y1="26" x2="50" y2="50" />
            <line x1="14" y1="74" x2="50" y2="50" />
            <line x1="50" y1="12" x2="50" y2="50" />
            <line x1="86" y1="26" x2="50" y2="50" />
            <line x1="86" y1="74" x2="50" y2="50" />
            <line x1="50" y1="88" x2="50" y2="50" />
          </svg>
          <div class="sync-chip"><span class="live-dot"></span>6 sources synced · just now</div>
          <div class="hub" aria-hidden="true"><div class="hub-holo"><span class="hub-layer hub-layer--back">M</span><span class="hub-layer hub-layer--mid">M</span><span class="hub-layer hub-layer--front">M</span></div></div>
          <div class="src" style="--x: 14%; --y: 26%"><div class="src-chip"><i class="orb orb--blue"></i>Postgres</div></div>
          <div class="src" style="--x: 14%; --y: 74%"><div class="src-chip"><i class="orb orb--sand"></i>Snowflake</div></div>
          <div class="src" style="--x: 50%; --y: 12%"><div class="src-chip"><i class="orb orb--purple"></i>Stripe</div></div>
          <div class="src" style="--x: 86%; --y: 26%"><div class="src-chip"><i class="orb orb--coral"></i>HubSpot</div></div>
          <div class="src" style="--x: 86%; --y: 74%"><div class="src-chip"><i class="orb orb--gold"></i>BigQuery</div></div>
          <div class="src" style="--x: 50%; --y: 88%"><div class="src-chip"><i class="orb orb--green"></i>Sheets</div></div>
        </div>

        <div class="panel panel-ask">
          <div class="ask-q">
            <span class="ask-avatar av-a"></span>
            <p>Which regions grew fastest last quarter?</p>
          </div>
          <div class="ask-a">
            <div class="ask-a-head"><i class="orb orb--purple"></i><strong>Monax</strong><span class="ask-meta">Queried 3 tables · 0.8s</span></div>
            <p>EMEA led with <b>+32%</b>, driven by mid-market expansion. APAC followed at +21%.</p>
            <div class="bars">
              <div class="bar" style="--h: 88%"><em>+32%</em><span>EMEA</span></div>
              <div class="bar" style="--h: 64%"><em>+21%</em><span>APAC</span></div>
              <div class="bar" style="--h: 46%"><em>+14%</em><span>NA</span></div>
              <div class="bar" style="--h: 30%"><em>+8%</em><span>LATAM</span></div>
            </div>
          </div>
          <div class="ask-input"><span>Ask anything about your data…</span><button class="send" aria-label="Send question">↑</button></div>
        </div>

        <div class="panel panel-share">
          <div class="kpis">
            <div class="kpi"><span>Revenue</span><strong>$4.2M</strong><em>▲ 12.4%</em></div>
            <div class="kpi"><span>Active accounts</span><strong>1,284</strong><em>▲ 6.1%</em></div>
            <div class="kpi"><span>Churn</span><strong>2.3%</strong><em>▼ 0.4 pt</em></div>
          </div>
          <div class="chart-card">
            <div class="chart-head">
              <strong>Weekly revenue</strong>
              <div class="viewers">
                <div class="avatar-stack">
                  <div class="av-a"></div>
                  <div class="av-b"></div>
                  <div class="av-c"></div>
                </div>
                3 viewing
              </div>
            </div>
            <svg class="line-chart" viewBox="0 0 400 140" preserveAspectRatio="none" aria-hidden="true">
              <defs>
                <linearGradient id="lc-fill" x1="0" y1="0" x2="0" y2="1">
                  <stop offset="0" stop-color="#bfd58f" stop-opacity="0.35" />
                  <stop offset="1" stop-color="#bfd58f" stop-opacity="0" />
                </linearGradient>
              </defs>
              <path d="M0,112 C30,104 55,92 85,96 S140,74 175,76 S235,54 265,58 S325,34 355,30 S388,22 400,18 L400,140 L0,140 Z" fill="url(#lc-fill)" />
              <path d="M0,112 C30,104 55,92 85,96 S140,74 175,76 S235,54 265,58 S325,34 355,30 S388,22 400,18" fill="none" stroke="#d7f08c" stroke-width="2.5" stroke-linecap="round" vector-effect="non-scaling-stroke" />
            </svg>
          </div>
          <div class="share-row"><span>Shared with #growth · refreshes hourly</span><button class="mini-pill">Copy link</button></div>
        </div>

      </div>
    </div>
  </div>
</section>

<!-- ============ BENTO ============ -->
<section class="section" id="platform" data-section="features">
  <div class="sec-head">
    <div class="reveal">
      <div class="eyebrow">The platform · Built in layers</div>
      <h2>Every layer of the stack,<br />finally speaking together.</h2>
    </div>
    <p class="reveal">Sources, models and metrics live in one governed layer, so every chart in the company starts from the same definitions.</p>
  </div>

  <div class="bento">
    <article class="tile tile--layers reveal">
      <div class="layers" aria-hidden="true">
        <div class="layers-rot">
          <div class="slab slab--1"><strong>Sources</strong><small>POSTGRES · STRIPE · SHEETS</small></div>
          <div class="slab slab--2"><strong>Models</strong><small>ORDERS · ACCOUNTS · EVENTS</small></div>
          <div class="slab slab--3"><strong>Metrics</strong><small>REVENUE · CHURN · MRR</small></div>
        </div>
      </div>
      <div class="eyebrow">Semantic layer</div>
      <h3>One model. Every answer.</h3>
      <p>Define revenue once. Every dashboard, question and export inherits the same logic, with no more spreadsheets that disagree.</p>
    </article>

    <article class="tile tile--count reveal">
      <div class="orb-row" aria-hidden="true">
        <i class="orb orb--blue"></i><i class="orb orb--gold"></i><i class="orb orb--purple"></i><i class="orb orb--red"></i><i class="orb orb--green"></i>
      </div>
      <div>
        <div class="big-num" data-count="200"><span>200</span><small>+</small></div>
        <p>Native connectors, from warehouses to spreadsheets.</p>
      </div>
    </article>

    <article class="tile tile--govern reveal">
      <div class="lock-orb" aria-hidden="true">
        <svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="5" y="11" width="14" height="10" rx="2.5" /><path d="M8 11V8a4 4 0 0 1 8 0v3" /></svg>
      </div>
      <div>
        <h3>Governed by default</h3>
        <p>Row-level permissions and a full audit trail on every query.</p>
      </div>
    </article>

    <article class="tile tile--alerts reveal">
      <div class="alert-stack" aria-hidden="true">
        <div class="alert"><i class="orb orb--red"></i><div><strong>Churn above 3% in EMEA</strong><span>Monitor · 2 min ago</span></div></div>
        <div class="alert"><i class="orb orb--green"></i><div><strong>Weekly revenue beat forecast</strong><span>Digest · 1 h ago</span></div></div>
        <div class="alert"><i class="orb orb--gold"></i><div><strong>Signups spiked after launch</strong><span>Anomaly · 3 h ago</span></div></div>
      </div>
      <div class="tile-copy">
        <h3>Alerts that find you</h3>
        <p>Pinged the moment a metric moves.</p>
      </div>
    </article>
  </div>
</section>

<!-- ============ CUSTOMER STORIES ============ -->
<section class="section" id="stories" data-section="testimonials">
  <div class="sec-head">
    <div class="reveal">
      <div class="eyebrow">Customer stories</div>
      <h2>Teams that stopped<br />waiting on the queue.</h2>
    </div>
    <a href="#resources" class="read-more reveal">All case studies →</a>
  </div>

  <div class="stories reveal">
    <div class="story-art" aria-hidden="true">
      <div class="story-holo">
        <div class="hub-holo"><span class="hub-layer hub-layer--back">N</span><span class="hub-layer hub-layer--mid">N</span><span class="hub-layer hub-layer--front">N</span></div>
      </div>
      <p class="story-co">Northwind</p>
    </div>
    <div class="story-card" aria-roledescription="carousel" aria-label="Customer stories">
      <div class="story-stack" aria-live="polite">
        <figure class="story is-active">
          <blockquote>"We cut four weekly reporting meetings in the first month. People just open Monax and answer the question themselves."</blockquote>
          <figcaption class="story-author">
            <span class="face" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="8.5" r="3.6" /><path d="M5 19.5c1.2-3.4 3.9-5.2 7-5.2s5.8 1.8 7 5.2" /></svg></span>
            <span><strong>Daniel Reyes</strong><span>Head of Data, Northwind</span></span>
            <span class="story-metric">4 meetings cut</span>
          </figcaption>
        </figure>
        <figure class="story">
          <blockquote>"Month-end close used to mean two days of exports. Now finance pulls it from one governed model before lunch."</blockquote>
          <figcaption class="story-author">
            <span class="face" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="8.5" r="3.6" /><path d="M5 19.5c1.2-3.4 3.9-5.2 7-5.2s5.8 1.8 7 5.2" /></svg></span>
            <span><strong>Marcus Webb</strong><span>VP Finance, Halcyon</span></span>
            <span class="story-metric">Close in hours, not days</span>
          </figcaption>
        </figure>
        <figure class="story">
          <blockquote>"Our growth team asks Monax the questions they used to file tickets for. The analytics backlog basically disappeared."</blockquote>
          <figcaption class="story-author">
            <span class="face" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><circle cx="12" cy="8.5" r="3.6" /><path d="M5 19.5c1.2-3.4 3.9-5.2 7-5.2s5.8 1.8 7 5.2" /></svg></span>
            <span><strong>Elena Park</strong><span>Growth Lead, Parabola</span></span>
            <span class="story-metric">Backlog cleared</span>
          </figcaption>
        </figure>
      </div>
      <div class="story-controls">
        <span class="story-count">01 / 03</span>
        <div class="story-nav">
          <button class="round" data-dir="-1" aria-label="Previous story">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><line x1="19" y1="12" x2="5" y2="12" /><polyline points="12 19 5 12 12 5" /></svg>
          </button>
          <button class="round round--dark" data-dir="1" aria-label="Next story">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round"><line x1="5" y1="12" x2="19" y2="12" /><polyline points="12 5 19 12 12 19" /></svg>
          </button>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ============ PRICING ============ -->
<section class="section" id="pricing" data-section="pricing">
  <div class="sec-head">
    <div class="reveal">
      <div class="eyebrow">Compare plans</div>
      <h2>Simple pricing that<br />grows with your team.</h2>
    </div>
    <div class="billing reveal">
      <span class="billing-label" data-period="monthly">Monthly</span>
      <button class="switch" role="switch" aria-checked="false" aria-label="Bill annually"><i></i></button>
      <span class="billing-label is-dim" data-period="annual">Annual</span>
      <span class="save-badge">Save 20%</span>
    </div>
  </div>

  <div class="plans">
    <article class="plan p-sand reveal">
      <div class="plan-name">Starter</div>
      <div class="plan-price"><strong>$0</strong><span>forever</span></div>
      <p class="plan-desc">For individuals exploring their own data.</p>
      <ul>
        <li>Up to 3 data sources</li>
        <li>1 workspace, unlimited dashboards</li>
        <li>Natural-language questions</li>
        <li>Community support</li>
      </ul>
      <button class="contact-pill plan-cta plan-cta--ghost">Start free</button>
    </article>

    <article class="plan plan--featured reveal">
      <div class="seat-holo" aria-hidden="true"><div class="hub-holo"><span class="hub-layer hub-layer--back"><svg viewBox="0 0 48 48"><circle cx="24" cy="16" r="6" /><path d="M13 36c1.8-5.6 6-8.6 11-8.6s9.2 3 11 8.6" /><circle cx="10.5" cy="20" r="4.2" /><path d="M3 33c1.2-3.8 4-5.8 7.4-5.8" /><circle cx="37.5" cy="20" r="4.2" /><path d="M45 33c-1.2-3.8-4-5.8-7.4-5.8" /></svg></span><span class="hub-layer hub-layer--mid"><svg viewBox="0 0 48 48"><circle cx="24" cy="16" r="6" /><path d="M13 36c1.8-5.6 6-8.6 11-8.6s9.2 3 11 8.6" /><circle cx="10.5" cy="20" r="4.2" /><path d="M3 33c1.2-3.8 4-5.8 7.4-5.8" /><circle cx="37.5" cy="20" r="4.2" /><path d="M45 33c-1.2-3.8-4-5.8-7.4-5.8" /></svg></span><span class="hub-layer hub-layer--front"><svg viewBox="0 0 48 48"><circle cx="24" cy="16" r="6" /><path d="M13 36c1.8-5.6 6-8.6 11-8.6s9.2 3 11 8.6" /><circle cx="10.5" cy="20" r="4.2" /><path d="M3 33c1.2-3.8 4-5.8 7.4-5.8" /><circle cx="37.5" cy="20" r="4.2" /><path d="M45 33c-1.2-3.8-4-5.8-7.4-5.8" /></svg></span></div></div>
      <div class="plan-name">Team <span class="popular">Most popular</span></div>
      <div class="plan-price"><strong data-monthly="49" data-annual="39">$49</strong><span class="per">/ seat / month</span></div>
      <p class="plan-desc">For teams that want every layer of the stack in one place.</p>
      <ul>
        <li>200+ connectors, unlimited sources</li>
        <li>AI-assisted exploration</li>
        <li>Scheduled digests and metric alerts</li>
        <li>Row-level permissions</li>
      </ul>
      <button class="contact-pill plan-cta">Start 30-day trial</button>
    </article>

    <article class="plan p-purple reveal">
      <div class="plan-name">Enterprise</div>
      <div class="plan-price"><strong>Custom</strong></div>
      <p class="plan-desc">For organisations with advanced governance and scale needs.</p>
      <ul>
        <li>Everything in Team</li>
        <li>SSO and SCIM provisioning</li>
        <li>Dedicated success manager</li>
        <li>Custom contract and SLAs</li>
      </ul>
      <button class="contact-pill plan-cta plan-cta--ghost" data-target="#contact">Talk to sales</button>
    </article>
  </div>
  <p class="plans-note reveal">Every plan starts with a 30-day trial of Team. No credit card required.</p>
</section>

<!-- ============ RESOURCES ============ -->
<section class="section" id="resources" data-section="resources">
  <div class="sec-head">
    <div class="reveal">
      <div class="eyebrow">Resources</div>
      <h2>Learn from teams<br />who've done it.</h2>
    </div>
    <a href="#resources" class="read-more reveal">View all resources →</a>
  </div>

  <div class="resources">
    <a href="#resources" class="res-card reveal">
      <div class="res-thumb">
        <div class="res-art holo-scene" aria-hidden="true"><div class="rs-stack"><i></i><i></i><i></i></div></div>
      </div>
      <h3>The modern data stack, explained for business teams</h3>
      <div class="res-meta"><span>8 min read</span><span>→</span></div>
    </a>
    <a href="#resources" class="res-card reveal">
      <div class="res-thumb">
        <div class="res-art holo-scene" aria-hidden="true"><div class="rs-num"><s>2 days</s><div class="rs-glyph"><div class="hub-holo"><span class="hub-layer hub-layer--back">4h</span><span class="hub-layer hub-layer--mid">4h</span><span class="hub-layer hub-layer--front">4h</span></div></div></div></div>
      </div>
      <h3>How Halcyon moved month-end close from days to hours</h3>
      <div class="res-meta"><span>5 min read</span><span>→</span></div>
    </a>
    <a href="#resources" class="res-card reveal">
      <div class="res-thumb">
        <div class="res-art holo-scene" aria-hidden="true"><div class="rs-talk"><div class="rs-bubble"><div class="hub-holo"><span class="hub-layer hub-layer--back">?</span><span class="hub-layer hub-layer--mid">?</span><span class="hub-layer hub-layer--front">?</span></div></div><div class="rs-wave"><i style="--n: 0"></i><i style="--n: 1"></i><i style="--n: 2"></i><i style="--n: 3"></i><i style="--n: 4"></i><i style="--n: 5"></i><i style="--n: 6"></i></div></div></div>
      </div>
      <h3>Asking better questions of your data with AI</h3>
      <div class="res-meta"><span>42 min watch</span><span>→</span></div>
    </a>
  </div>
</section>

<!-- ============ FOOTER ============ -->
<footer class="footer" id="contact" data-section="footer">
  <div class="footer-top">
    <div class="footer-brand">
      <div class="logo">Monax</div>
      <p>Analytics your whole team can actually use.</p>
      <form class="newsletter" data-component="newsletter">
        <input type="email" name="email" placeholder="Work email" aria-label="Work email" autocomplete="email" required />
        <button type="submit" class="contact-pill">Subscribe</button>
      </form>
      <p class="nl-status" role="status" aria-live="polite"></p>
    </div>
    <nav class="footer-col" aria-label="Product">
      <h4>Product</h4>
      <a href="#product">Pipelines</a>
      <a href="#product">Self-serve</a>
      <a href="#product">AI exploration</a>
      <a href="#pricing">Pricing</a>
    </nav>
    <nav class="footer-col" aria-label="Company">
      <h4>Company</h4>
      <a href="#platform">About</a>
      <a href="#stories">Customers</a>
      <a href="#contact">Careers</a>
      <a href="#contact">Contact</a>
    </nav>
    <nav class="footer-col" aria-label="Resources">
      <h4>Resources</h4>
      <a href="#resources">Guides</a>
      <a href="#resources">Case studies</a>
      <a href="#resources">Webinars</a>
      <a href="#resources">Docs</a>
    </nav>
  </div>

  <div class="footer-mark" aria-hidden="true">Monax</div>

  <p class="footer-legal">
    Monax is a fictional company and this page is a design demo. The product, the connectors, the customers,
    the quotes, the pricing and every figure quoted here are invented. Nothing here is real, and nothing on
    this page can be bought or subscribed to.
  </p>

  <div class="footer-bottom">
    <span>© <span id="year">2026</span> Monax, Inc.</span>
    <span class="status"><span class="live-dot"></span>All systems normal</span>
    <span><a href="#">Privacy</a> · <a href="#">Terms</a> · <a href="#">Security</a></span>
  </div>
</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script>
gsap.registerPlugin(ScrollTrigger);

// Initial states
gsap.set(".nav", { opacity: 0, y: -20 });
gsap.set(".headline .word > span", { y: "105%" });
gsap.set("#heroEyebrow", { opacity: 0, y: 12 });
gsap.set("#inlineImg, #ideaPill", { scale: 0 });

// ============================================================
// INTRO TIMELINE
// ============================================================
const intro = gsap.timeline({ defaults: { ease: "power3.out" } });
intro
  .to(".nav", { opacity: 1, y: 0, duration: 0.8 }, 0.1)
  .to("#heroEyebrow", { opacity: 1, y: 0, duration: 0.7 }, 0.2)
  .to(".line-1 .word > span", { y: "0%", duration: 0.9, stagger: 0.1 }, 0.3)
  .to(".line-2 .word > span", { y: "0%", duration: 0.9 }, 0.55)
  .to("#inlineImg", { scale: 1, duration: 0.9, ease: "back.out(1.6)" }, 0.5)
  .to("#ideaPill", { scale: 1, duration: 0.9, ease: "back.out(1.6)" }, 0.7)
  .to(".line-3 .word > span", { y: "0%", duration: 0.9, stagger: 0.1 }, 0.75);

// ============================================================
// CONTINUOUS: inline img + idea pill bob
// ============================================================
gsap.to("#inlineImg", {
  y: "+=6",
  rotation: 2,
  duration: 2.8,
  delay: 1.8,
  ease: "sine.inOut",
  yoyo: true,
  repeat: -1
});
gsap.to("#ideaPill", {
  y: "+=5",
  rotation: -1.5,
  duration: 3.2,
  delay: 2.0,
  ease: "sine.inOut",
  yoyo: true,
  repeat: -1
});
// ============================================================
// INLINE BADGE HOVER
// ============================================================
document.getElementById("inlineImg").addEventListener("mouseenter", (e) => {
  gsap.to(e.target, {
    scale: 1.08,
    rotation: 4,
    duration: 0.4,
    ease: "back.out(1.6)"
  });
});
document.getElementById("inlineImg").addEventListener("mouseleave", (e) => {
  gsap.to(e.target, {
    scale: 1,
    rotation: 0,
    duration: 0.6,
    ease: "elastic.out(1, 0.6)"
  });
});
document.getElementById("ideaPill").addEventListener("mouseenter", (e) => {
  gsap.to(e.currentTarget, {
    scale: 1.06,
    rotation: -3,
    duration: 0.4,
    ease: "back.out(1.6)"
  });
  gsap.to(e.currentTarget.querySelector(".leaf"), {
    rotation: 360,
    duration: 0.8,
    ease: "power2.inOut"
  });
});
document.getElementById("ideaPill").addEventListener("mouseleave", (e) => {
  gsap.to(e.currentTarget, {
    scale: 1,
    rotation: 0,
    duration: 0.6,
    ease: "elastic.out(1, 0.6)"
  });
});

// ============================================================
// FANNED CARD STACK (below the headline)
// ============================================================
(function () {
  const slots = [...document.querySelectorAll(".fan-slot")];
  const cards = slots.map((s) => s.querySelector(".fan-card"));
  const faces = slots.map((s) => s.querySelector(".fan-face"));
  const rests = slots.map((s) => parseFloat(s.dataset.rot) || 0);
  const still = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  gsap.set(cards, { rotation: (i) => rests[i] });
  if (still) return; // resting fan, no drop, float, parallax or scroll spread

  // Intro: ghost letters rise, then cards drop in from above, centre first
  gsap.set(".fan-ghost .gl", { y: 80, opacity: 0 });
  gsap.set(cards, { y: -700, rotation: (i) => rests[i] + 25, opacity: 0, scale: 0.7 });
  gsap.set("#fanCta .arrow-pill", { opacity: 0, scale: 0.6 });
  gsap.timeline({ delay: 0.9, defaults: { ease: "power3.out" } })
    .to(".fan-ghost .gl", { y: 0, opacity: 1, duration: 0.9, stagger: 0.04, ease: "back.out(1.6)" }, 0)
    .to(cards, {
      y: 0, opacity: 1, scale: 1,
      rotation: (i) => rests[i],
      duration: 1.1,
      stagger: { each: 0.08, from: "center" },
      ease: "back.out(1.4)"
    }, 0.25)
    .to("#fanCta .arrow-pill", { opacity: 1, scale: 1, duration: 0.8, ease: "back.out(1.8)", clearProps: "transform" }, 1.15)
    .add(() => {
      // Idle float starts once every card has landed
      cards.forEach((card, i) => {
        gsap.to(card, {
          y: `+=${6 + (i % 3) * 4}`,
          rotation: rests[i] + (i % 2 === 0 ? 1.5 : -1.5),
          duration: 3 + (i % 4) * 0.5,
          delay: i * 0.1,
          ease: "sine.inOut",
          yoyo: true,
          repeat: -1
        });
      });
    });

  // Mouse parallax on the slots (CSS translate, separate from GSAP transforms)
  const stage = document.getElementById("fanStage");
  let mx = 0, my = 0, tx = 0, ty = 0;
  stage.addEventListener("mousemove", (e) => {
    const r = stage.getBoundingClientRect();
    mx = ((e.clientX - r.left) / r.width - 0.5) * 2;
    my = ((e.clientY - r.top) / r.height - 0.5) * 2;
  });
  stage.addEventListener("mouseleave", () => { mx = 0; my = 0; });
  (function drift() {
    tx += (mx - tx) * 0.05;
    ty += (my - ty) * 0.05;
    slots.forEach((s) => {
      const d = parseFloat(s.dataset.depth) || 8;
      s.style.translate = `${tx * d}px ${ty * d * 0.5}px`;
    });
    requestAnimationFrame(drift);
  })();

  // Hover: the face tilts toward the pointer and lifts above its neighbours
  faces.forEach((face, i) => {
    const slot = slots[i];
    face.addEventListener("mousemove", (e) => {
      const r = face.getBoundingClientRect();
      const px = (e.clientX - r.left) / r.width - 0.5;
      const py = (e.clientY - r.top) / r.height - 0.5;
      slot.style.zIndex = 20;
      gsap.to(face, {
        rotateX: -py * 16, rotateY: px * 16, scale: 1.1,
        transformPerspective: 700, duration: 0.4, ease: "power2.out", overwrite: "auto"
      });
    });
    face.addEventListener("mouseleave", () => {
      slot.style.zIndex = "";
      gsap.to(face, { rotateX: 0, rotateY: 0, scale: 1, duration: 0.8, ease: "elastic.out(1, 0.6)", overwrite: "auto" });
    });
  });

  // Scroll: outer cards fan out, the ghost phrase swells and fades
  const moves = [
    { x: -260, y: -40, rot: -25 }, { x: -200, y: 20, rot: -18 },
    { x: -120, y: 80, rot: -10 }, { x: -40, y: 120, rot: -4 },
    { x: 40, y: 120, rot: 4 }, { x: 120, y: 80, rot: 12 },
    { x: 200, y: 20, rot: 22 }, { x: 260, y: -40, rot: 28 }
  ];
  ScrollTrigger.create({
    trigger: stage,
    start: "top 40%",
    end: "bottom top",
    scrub: 0.8,
    onUpdate: (self) => {
      const p = self.progress;
      const k = Math.min(1, stage.clientWidth / 1280);
      gsap.set(".fan-ghost", { scale: 1 + 0.12 * p, opacity: 1 - 0.5 * p });
      slots.forEach((s, i) => {
        const m = moves[i];
        gsap.set(s, { x: m.x * p * k, y: m.y * p * k, rotation: m.rot * p });
      });
    }
  });
})();

// Headline letters subtle spread on scroll
ScrollTrigger.create({
  trigger: ".hero",
  start: "top top",
  end: "bottom top",
  scrub: 0.8,
  onUpdate: (self) => {
    const p = self.progress;
    gsap.set(".headline", { y: -50 * p, opacity: 1 - p * 0.4 });
  }
});

// Button click pulse
document
  .querySelectorAll(".contact-pill, .arrow-pill, .cta-btn")
  .forEach((btn) => {
    btn.addEventListener("click", () => {
      gsap.fromTo(
        btn,
        { scale: 1 },
        {
          scale: 0.92,
          duration: 0.12,
          yoyo: true,
          repeat: 1,
          ease: "power2.inOut"
        }
      );
    });
  });

// ============================================================
// EXTENDED SECTIONS
// ============================================================
const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

// Buttons that name a section scroll to it (links use native #anchors)
document.querySelectorAll("button[data-target]").forEach((btn) => {
  btn.addEventListener("click", () => {
    document.querySelector(btn.dataset.target)?.scrollIntoView({ behavior: "smooth" });
  });
});

// Section reveals — clearProps so CSS :hover lifts keep working afterwards
gsap.set(".reveal", { opacity: 0, y: 40 });
ScrollTrigger.batch(".reveal", {
  start: "top 85%",
  once: true,
  onEnter: (batch) =>
    gsap.to(batch, {
      opacity: 1,
      y: 0,
      duration: 0.9,
      stagger: 0.1,
      ease: "power3.out",
      clearProps: "transform"
    })
});

// Bento 200+ counter
document.querySelectorAll(".big-num[data-count]").forEach((el) => {
  const span = el.querySelector("span");
  const counter = { v: 0 };
  span.textContent = "0";
  gsap.to(counter, {
    v: Number(el.dataset.count),
    duration: 1.6,
    ease: "power2.out",
    onUpdate: () => (span.textContent = Math.floor(counter.v).toLocaleString()),
    scrollTrigger: { trigger: el, start: "top 85%", once: true }
  });
});

// ---------- Product demo: tabs with auto-advancing progress ----------
const demoTabs = [...document.querySelectorAll(".demo-tab")];
const panels = [...document.querySelectorAll(".panel")];
const demoStage = document.getElementById("demo-stage");
const barOf = (i) => demoTabs[i].querySelector(".demo-tab-bar i");
let demoIndex = 0;
let autoplay = !reduceMotion;
let demoVisible = false;
let demoStarted = false;
let hovering = false;
let progress = null;

// fromTo everywhere so an interrupted intro can't leave elements half-hidden
const panelIntro = [
  (p) =>
    gsap.fromTo(
      p.querySelectorAll(".src-chip"),
      { scale: 0, opacity: 0 },
      { scale: 1, opacity: 1, duration: 0.6, stagger: 0.07, ease: "back.out(1.8)", overwrite: true }
    ),
  (p) =>
    gsap
      .timeline()
      .fromTo(p.querySelector(".ask-q"), { y: 16, opacity: 0 }, { y: 0, opacity: 1, duration: 0.5 })
      .fromTo(p.querySelector(".ask-a"), { y: 16, opacity: 0 }, { y: 0, opacity: 1, duration: 0.5 }, "+=0.1")
      .fromTo(p.querySelectorAll(".bar"), { scaleY: 0 }, { scaleY: 1, duration: 0.8, stagger: 0.08, ease: "back.out(1.4)" }, "-=0.2"),
  (p) =>
    gsap
      .timeline()
      .fromTo(p.querySelectorAll(".kpi"), { y: 16, opacity: 0 }, { y: 0, opacity: 1, duration: 0.5, stagger: 0.08 })
      .fromTo(
        p.querySelector(".line-chart"),
        { clipPath: "inset(0% 100% 0% 0%)" },
        { clipPath: "inset(0% 0% 0% 0%)", duration: 1.2, ease: "power2.inOut" },
        "-=0.2"
      )
];

const runProgress = () => {
  progress?.kill();
  demoTabs.forEach((_, i) => gsap.set(barOf(i), { scaleX: 0 }));
  progress = gsap.fromTo(
    barOf(demoIndex),
    { scaleX: 0 },
    { scaleX: 1, duration: 6, ease: "none", onComplete: () => showStep((demoIndex + 1) % panels.length) }
  );
  if (!demoVisible || hovering) progress.pause();
};

const stopAutoplay = () => {
  autoplay = false;
  progress?.kill();
  demoTabs.forEach((_, i) => gsap.set(barOf(i), { scaleX: 1 }));
};

function showStep(i, fromUser = false) {
  if (fromUser) stopAutoplay();
  const prev = panels[demoIndex];
  const next = panels[i];
  demoTabs.forEach((t, k) => {
    const on = k === i;
    t.classList.toggle("active", on);
    t.setAttribute("aria-selected", String(on));
    t.tabIndex = on ? 0 : -1;
  });
  demoStage.setAttribute("aria-labelledby", demoTabs[i].id);
  if (prev !== next) {
    gsap.to(prev, {
      opacity: 0,
      y: -12,
      duration: 0.3,
      ease: "power2.in",
      overwrite: true,
      onComplete: () => {
        prev.classList.remove("is-active");
        gsap.set(prev, { clearProps: "opacity,transform" });
      }
    });
    next.classList.add("is-active");
    gsap.fromTo(next, { opacity: 0, y: 12 }, { opacity: 1, y: 0, duration: 0.45, delay: 0.2, ease: "power3.out", overwrite: true });
    panelIntro[i](next);
  }
  demoIndex = i;
  if (autoplay) runProgress();
}

demoTabs.forEach((tab, i) => tab.addEventListener("click", () => showStep(i, true)));
document.querySelector(".demo-tabs").addEventListener("keydown", (e) => {
  const step = { ArrowDown: 1, ArrowRight: 1, ArrowUp: -1, ArrowLeft: -1 }[e.key];
  if (!step) return;
  e.preventDefault();
  const i = (demoTabs.indexOf(document.activeElement) + step + demoTabs.length) % demoTabs.length;
  demoTabs[i].focus();
  showStep(i, true);
});
demoStage.addEventListener("mouseenter", () => {
  hovering = true;
  progress?.pause();
});
demoStage.addEventListener("mouseleave", () => {
  hovering = false;
  if (demoVisible) progress?.resume();
});
if (!autoplay) stopAutoplay();

ScrollTrigger.create({
  trigger: ".demo",
  start: "top 75%",
  end: "bottom 15%",
  onToggle: (self) => {
    demoVisible = self.isActive;
    if (demoVisible && !demoStarted) {
      demoStarted = true;
      panelIntro[0](panels[0]);
      if (autoplay) runProgress();
      return;
    }
    if (demoVisible && !hovering) progress?.resume();
    else progress?.pause();
  }
});

// ---------- Bento: holographic layers (wobble is CSS; hover spreads the depth) ----------
const layers = document.querySelector(".layers");
const layersTile = document.querySelector(".tile--layers");
layersTile.addEventListener("mouseenter", () =>
  gsap.to(layers, { "--gap": "64px", duration: 0.6, ease: "back.out(1.6)" })
);
layersTile.addEventListener("mouseleave", () =>
  gsap.to(layers, { "--gap": "36px", duration: 0.8, ease: "elastic.out(1, 0.6)" })
);

// ---------- Bento: rotating alert feed (manual FLIP) ----------
const alertStack = document.querySelector(".alert-stack");
let alertsVisible = false;
ScrollTrigger.create({
  trigger: alertStack,
  start: "top bottom",
  end: "bottom top",
  onToggle: (self) => (alertsVisible = self.isActive)
});
const rotateAlerts = () => {
  if (!alertsVisible || document.hidden) return;
  const items = [...alertStack.children];
  const before = items.map((el) => el.getBoundingClientRect().top);
  const moved = items[items.length - 1];
  alertStack.prepend(moved);
  items.forEach((el, i) => {
    if (el === moved) return;
    const dy = before[i] - el.getBoundingClientRect().top;
    gsap.fromTo(el, { y: dy }, { y: 0, duration: 0.6, ease: "power3.out" });
  });
  gsap.fromTo(moved, { opacity: 0, y: -18, scale: 0.94 }, { opacity: 1, y: 0, scale: 1, duration: 0.6, ease: "back.out(1.6)" });
};
if (!reduceMotion) setInterval(rotateAlerts, 3200);

// ---------- Customer stories ----------
const stories = [...document.querySelectorAll(".story")];
const storyCount = document.querySelector(".story-count");
const pad = (n) => String(n).padStart(2, "0");
let storyIndex = 0;

const storyBrands = ["Northwind", "Halcyon", "Parabola"];
const storyCo = document.querySelector(".story-co");
const showStory = (dir) => {
  const i = (storyIndex + dir + stories.length) % stories.length;
  const out = stories[storyIndex];
  const inn = stories[i];
  gsap.to(out, {
    opacity: 0,
    y: -16,
    duration: 0.3,
    overwrite: true,
    onComplete: () => out.classList.remove("is-active")
  });
  inn.classList.add("is-active");
  gsap.fromTo(inn, { opacity: 0, y: 16 }, { opacity: 1, y: 0, duration: 0.5, delay: 0.2, ease: "power3.out", overwrite: true });
  const holo = document.querySelector(".story-holo .hub-holo");
  gsap.to(holo, {
    opacity: 0, scale: 0.85, duration: 0.25, overwrite: true,
    onComplete: () => {
      holo.querySelectorAll(".hub-layer").forEach((l) => (l.textContent = storyBrands[i][0]));
      storyCo.textContent = storyBrands[i];
      gsap.to(holo, { opacity: 1, scale: 1, duration: 0.6, ease: "back.out(1.6)" });
    }
  });
  storyIndex = i;
  storyCount.textContent = `${pad(i + 1)} / ${pad(stories.length)}`;
};
document.querySelectorAll(".story-nav .round").forEach((btn) =>
  btn.addEventListener("click", () => showStory(Number(btn.dataset.dir)))
);

// ---------- Pricing: monthly / annual ----------
const billingSwitch = document.querySelector(".switch");
billingSwitch.addEventListener("click", () => {
  const annual = billingSwitch.getAttribute("aria-checked") !== "true";
  billingSwitch.setAttribute("aria-checked", String(annual));
  document.querySelectorAll(".billing-label").forEach((label) => {
    label.classList.toggle("is-dim", label.dataset.period !== (annual ? "annual" : "monthly"));
  });
  document.querySelectorAll("[data-monthly]").forEach((el) => {
    const counter = { v: Number(el.textContent.replace(/\D/g, "")) };
    gsap.to(counter, {
      v: Number(annual ? el.dataset.annual : el.dataset.monthly),
      duration: 0.6,
      ease: "power2.out",
      onUpdate: () => (el.textContent = `$${Math.round(counter.v)}`)
    });
  });
  document.querySelectorAll(".per").forEach((el) => {
    el.textContent = annual ? "/ seat / month, billed yearly" : "/ seat / month";
  });
});

// ---------- Newsletter (demo: nothing is sent) ----------
const newsletter = document.querySelector(".newsletter");
newsletter.addEventListener("submit", (e) => {
  e.preventDefault();
  if (!newsletter.checkValidity()) {
    newsletter.reportValidity();
    return;
  }
  const btn = newsletter.querySelector("button");
  btn.textContent = "Subscribed ✓";
  btn.disabled = true;
  document.querySelector(".nl-status").textContent = "Thanks! The next issue lands in your inbox.";
});

document.getElementById("year").textContent = new Date().getFullYear();

// Webfont swap can shift section heights; re-measure trigger positions
window.addEventListener("load", () => ScrollTrigger.refresh());
</script>
<script>
/* ============ DITHERED FIELD ============
   A CRT/halftone material adapted from the FaultyTerminal shader (fbm -> digit
   grid -> scanline -> dither), ported off React/ogl to plain WebGL so this page
   stays one file with no build step.

   It is applied per element, not to the page: anything with data-fx has its
   gradient fill replaced by the field, printed in that element's own colours
   (data-fx-ink / data-fx-paper). So the hero product panel, the two art cards
   beside it and the stories panel share one material while the page itself
   keeps its paper background.

   Changes from the original, both about fitting the page: the single uTint is
   four inks mixed along a drifting diagonal, and the black background is a
   three-stop paper gradient rebuilt in shader, so the dither smooths the
   gradient's banding as well as the dot edges.
   ========================================================================= */
(function () {
  var hosts = [].slice.call(document.querySelectorAll("[data-fx]"));
  if (!hosts.length) return;

  var VERT = [
    "attribute vec2 position;",
    "attribute vec2 uv;",
    "varying vec2 vUv;",
    "void main() {",
    "  vUv = uv;",
    "  gl_Position = vec4(position, 0.0, 1.0);",
    "}"
  ].join("\n");

  var FRAG = [
    "precision mediump float;",
    "varying vec2 vUv;",
    "",
    "uniform float iTime;",
    "uniform vec3  iResolution;",
    "uniform float uScale;",
    "uniform vec2  uGridMul;",
    "uniform float uDigitSize;",
    "uniform float uScanlineIntensity;",
    "uniform float uGlitchAmount;",
    "uniform float uFlickerAmount;",
    "uniform float uNoiseAmp;",
    "uniform float uChromaticAberration;",
    "uniform float uDither;",
    "uniform float uCurvature;",
    "uniform float uCoverage;",
    "uniform float uBrightness;",
    "uniform vec2  uMouse;",
    "uniform float uMouseStrength;",
    "uniform float uLoad;",
    "uniform vec3  uInkA;",
    "uniform vec3  uInkB;",
    "uniform vec3  uInkC;",
    "uniform vec3  uInkD;",
    "uniform vec3  uPaperA;",
    "uniform vec3  uPaperB;",
    "uniform vec3  uPaperC;",
    "",
    "float time;",
    "",
    "float hash21(vec2 p){",
    "  p = fract(p * 234.56);",
    "  p += dot(p, p + 34.56);",
    "  return fract(p.x * p.y);",
    "}",
    "",
    "float noise(vec2 p){",
    "  return sin(p.x * 10.0) * sin(p.y * (3.0 + sin(time * 0.090909))) + 0.2;",
    "}",
    "",
    "mat2 rotate(float angle){",
    "  float c = cos(angle);",
    "  float s = sin(angle);",
    "  return mat2(c, -s, s, c);",
    "}",
    "",
    "float fbm(vec2 p){",
    "  p *= 1.1;",
    "  float f = 0.0;",
    "  float amp = 0.5 * uNoiseAmp;",
    "  mat2 modify0 = rotate(time * 0.02);",
    "  f += amp * noise(p);",
    "  p = modify0 * p * 2.0;",
    "  amp *= 0.454545;",
    "  mat2 modify1 = rotate(time * 0.02);",
    "  f += amp * noise(p);",
    "  p = modify1 * p * 2.0;",
    "  amp *= 0.454545;",
    "  mat2 modify2 = rotate(time * 0.08);",
    "  f += amp * noise(p);",
    "  return f;",
    "}",
    "",
    "float pattern(vec2 p, out vec2 q, out vec2 r){",
    "  vec2 offset1 = vec2(1.0);",
    "  vec2 offset0 = vec2(0.0);",
    "  mat2 rot01 = rotate(0.1 * time);",
    "  mat2 rot1 = rotate(0.1);",
    "  q = vec2(fbm(p + offset1), fbm(rot01 * p + offset1));",
    "  r = vec2(fbm(rot1 * q + offset0), fbm(q + offset0));",
    "  return fbm(p + r);",
    "}",
    "",
    "float digit(vec2 p){",
    "  vec2 grid = uGridMul * 15.0;",
    "  vec2 s = floor(p * grid) / grid;",
    "  p = p * grid;",
    "  vec2 q, r;",
    "  float intensity = pattern(s * 0.1, q, r) * 1.3 - 0.03;",
    "",
    "  vec2 mouseWorld = uMouse * uScale;",
    "  float distToMouse = distance(s, mouseWorld);",
    "  float mouseInfluence = exp(-distToMouse * 8.0) * uMouseStrength * 10.0;",
    "  intensity += mouseInfluence;",
    "  intensity += sin(distToMouse * 20.0 - iTime * 5.0) * 0.1 * mouseInfluence;",
    "",
    "  float cellRandom = fract(sin(dot(s, vec2(12.9898, 78.233))) * 43758.5453);",
    "  intensity *= smoothstep(0.0, 1.0, clamp((uLoad - cellRandom * 0.8) / 0.2, 0.0, 1.0));",
    "",
    "  p = fract(p);",
    "  p *= uDigitSize;",
    "",
    "  float px5 = p.x * 5.0;",
    "  float py5 = (1.0 - p.y) * 5.0;",
    "  float x = fract(px5);",
    "  float y = fract(py5);",
    "",
    "  float i = floor(py5) - 2.0;",
    "  float j = floor(px5) - 2.0;",
    "  float n = i * i + j * j;",
    "  float f = n * 0.0625;",
    "",
    "  float isOn = step(0.1, intensity - f);",
    "  float brightness = isOn * (0.2 + y * 0.8) * (0.75 + x * 0.25);",
    "  return step(0.0, p.x) * step(p.x, 1.0) * step(0.0, p.y) * step(p.y, 1.0) * brightness;",
    "}",
    "",
    "float onOff(float a, float b, float c){",
    "  return step(c, sin(iTime + a * cos(iTime * b))) * uFlickerAmount;",
    "}",
    "",
    "float displace(vec2 look){",
    "  float y = look.y - mod(iTime * 0.25, 1.0);",
    "  float window = 1.0 / (1.0 + 50.0 * y * y);",
    "  return sin(look.y * 20.0 + iTime) * 0.0125 * onOff(4.0, 2.0, 0.8) * (1.0 + cos(iTime * 60.0)) * window;",
    "}",
    "",
    "vec3 getColor(vec2 p){",
    "  float bar = step(mod(p.y + time * 20.0, 1.0), 0.2) * 0.4 + 1.0;",
    "  bar *= uScanlineIntensity;",
    "",
    "  float displacement = displace(p);",
    "  p.x += displacement;",
    "  if (uGlitchAmount != 1.0) p.x += displacement * (uGlitchAmount - 1.0);",
    "",
    "  float middle = digit(p);",
    "  const float off = 0.002;",
    "  float sum = digit(p + vec2(-off, -off)) + digit(p + vec2(0.0, -off)) + digit(p + vec2(off, -off)) +",
    "              digit(p + vec2(-off, 0.0)) + digit(p + vec2(0.0, 0.0)) + digit(p + vec2(off, 0.0)) +",
    "              digit(p + vec2(-off, off)) + digit(p + vec2(0.0, off)) + digit(p + vec2(off, off));",
    "  return vec3(0.9) * middle + sum * 0.1 * bar;",
    "}",
    "",
    "vec2 barrel(vec2 uv){",
    "  vec2 c = uv * 2.0 - 1.0;",
    "  float r2 = dot(c, c);",
    "  c *= 1.0 + uCurvature * r2;",
    "  return c * 0.5 + 0.5;",
    "}",
    "",
    "/* Four inks drifting along a diagonal, so the panel never reads as one flat",
    "   tint -- this is what replaces the stack of radial gradients. */",
    "vec3 palette(vec2 uv){",
    "  float g = uv.x * 0.52 + uv.y * 0.48",
    "          + 0.24 * sin(time * 0.55 + uv.y * 2.6)",
    "          + 0.18 * cos(time * 0.31 - uv.x * 3.1);",
    "  g = clamp(g, 0.0, 1.0);",
    "  vec3 c = mix(uInkA, uInkB, smoothstep(0.02, 0.36, g));",
    "  c = mix(c, uInkC, smoothstep(0.36, 0.68, g));",
    "  return mix(c, uInkD, smoothstep(0.68, 0.98, g));",
    "}",
    "",
    "/* The element's own 160deg base gradient, rebuilt so the dots print onto it. */",
    "vec3 paperAt(vec2 uv){",
    "  float t = clamp((1.0 - uv.y) * 0.78 + uv.x * 0.22, 0.0, 1.0);",
    "  vec3 p = mix(uPaperA, uPaperB, smoothstep(0.0, 0.55, t));",
    "  return mix(p, uPaperC, smoothstep(0.55, 1.0, t));",
    "}",
    "",
    "void main(){",
    "  time = iTime * 0.333333;",
    "  vec2 uv = vUv;",
    "  if (uCurvature != 0.0) uv = barrel(uv);",
    "",
    "  vec2 p = uv * uScale;",
    "  vec3 col = getColor(p);",
    "",
    "  if (uChromaticAberration != 0.0) {",
    "    vec2 ca = vec2(uChromaticAberration) / iResolution.xy;",
    "    col.r = getColor(p + ca).r;",
    "    col.b = getColor(p - ca).b;",
    "  }",
    "  col *= uBrightness;",
    "",
    "  float energy = max(max(col.r, col.g), col.b);",
    "  float coverage = clamp(smoothstep(0.04, 0.92, energy) * uCoverage, 0.0, 1.0);",
    "  vec3 outc = mix(paperAt(uv), palette(uv), coverage);",
    "",
    "  /* Dither last, in paper space: it breaks the gradient's banding as well",
    "     as the dot edges, which is the whole reason it is here. */",
    "  if (uDither > 0.0) {",
    "    float rnd = hash21(gl_FragCoord.xy + fract(iTime) * 17.0);",
    "    outc += (rnd - 0.5) * uDither * 0.016;",
    "  }",
    "",
    "  gl_FragColor = vec4(outc, 1.0);",
    "}"
  ].join("\n");

  function rgb(hex) {
    var n = parseInt(hex.trim().slice(1), 16);
    return [((n >> 16) & 255) / 255, ((n >> 8) & 255) / 255, (n & 255) / 255];
  }
  function list(value, fallback) {
    return (value || fallback).split(",").map(rgb);
  }
  function num(value, fallback) {
    var n = parseFloat(value);
    return isNaN(n) ? fallback : n;
  }

  var DPR = Math.min(window.devicePixelRatio || 1, 1.5);
  var reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var instances = [];

  function attach(host) {
    var canvas = document.createElement("canvas");
    canvas.className = "fx-layer";
    canvas.setAttribute("aria-hidden", "true");

    var gl = null;
    try {
      var opts = { alpha: false, antialias: false, depth: false, stencil: false, powerPreference: "low-power" };
      gl = canvas.getContext("webgl", opts) || canvas.getContext("experimental-webgl", opts);
    } catch (e) {
      gl = null;
    }
    if (!gl) return null; // the element keeps its CSS gradient

    function compile(type, src) {
      var sh = gl.createShader(type);
      gl.shaderSource(sh, src);
      gl.compileShader(sh);
      if (!gl.getShaderParameter(sh, gl.COMPILE_STATUS)) {
        console.warn("fx shader:", gl.getShaderInfoLog(sh));
        return null;
      }
      return sh;
    }
    var vs = compile(gl.VERTEX_SHADER, VERT);
    var fs = compile(gl.FRAGMENT_SHADER, FRAG);
    if (!vs || !fs) return null;

    var prog = gl.createProgram();
    gl.attachShader(prog, vs);
    gl.attachShader(prog, fs);
    gl.linkProgram(prog);
    if (!gl.getProgramParameter(prog, gl.LINK_STATUS)) {
      console.warn("fx link:", gl.getProgramInfoLog(prog));
      return null;
    }
    gl.useProgram(prog);

    // One oversized triangle covers the element with no index buffer.
    var buf = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, buf);
    gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([-1, -1, 0, 0, 3, -1, 2, 0, -1, 3, 0, 2]), gl.STATIC_DRAW);
    var aPos = gl.getAttribLocation(prog, "position");
    var aUv = gl.getAttribLocation(prog, "uv");
    gl.enableVertexAttribArray(aPos);
    gl.vertexAttribPointer(aPos, 2, gl.FLOAT, false, 16, 0);
    gl.enableVertexAttribArray(aUv);
    gl.vertexAttribPointer(aUv, 2, gl.FLOAT, false, 16, 8);

    function u(name) { return gl.getUniformLocation(prog, name); }

    var inks = list(host.dataset.fxInk, "#8163c6,#f2a03b,#e83a4d,#7bafce");
    var paper = list(host.dataset.fxPaper, "#f2ece0,#e8e0ce,#c8b89e");
    var density = num(host.dataset.fxDensity, 1);

    gl.uniform1f(u("uScale"), num(host.dataset.fxScale, 1.4));
    gl.uniform1f(u("uDigitSize"), num(host.dataset.fxDigitSize, 1.2));
    gl.uniform1f(u("uScanlineIntensity"), 0.45);
    gl.uniform1f(u("uGlitchAmount"), 1.0);
    gl.uniform1f(u("uFlickerAmount"), 0.7);
    gl.uniform1f(u("uNoiseAmp"), 1.0);
    gl.uniform1f(u("uChromaticAberration"), 1.4);
    gl.uniform1f(u("uDither"), 1.0);
    gl.uniform1f(u("uCurvature"), num(host.dataset.fxCurvature, 0.08));
    gl.uniform1f(u("uCoverage"), num(host.dataset.fxCoverage, 0.9));
    gl.uniform1f(u("uBrightness"), 1.0);
    gl.uniform1f(u("uMouseStrength"), num(host.dataset.fxMouse, 0.22));
    gl.uniform3fv(u("uInkA"), inks[0]);
    gl.uniform3fv(u("uInkB"), inks[1 % inks.length]);
    gl.uniform3fv(u("uInkC"), inks[2 % inks.length]);
    gl.uniform3fv(u("uInkD"), inks[3 % inks.length]);
    gl.uniform3fv(u("uPaperA"), paper[0]);
    gl.uniform3fv(u("uPaperB"), paper[1 % paper.length]);
    gl.uniform3fv(u("uPaperC"), paper[2 % paper.length]);

    var inst = {
      host: host, gl: gl, canvas: canvas,
      uTime: u("iTime"), uMouse: u("uMouse"), uLoad: u("uLoad"),
      uRes: u("iResolution"), uGrid: u("uGridMul"),
      seed: Math.random() * 100, start: 0, visible: true,
      mouse: { x: 0.5, y: 0.5 }, smooth: { x: 0.5, y: 0.5 },
      density: density,
      resize: function () {
        var w = Math.max(1, Math.round(host.clientWidth * DPR));
        var h = Math.max(1, Math.round(host.clientHeight * DPR));
        if (canvas.width === w && canvas.height === h) return;
        canvas.width = w;
        canvas.height = h;
        gl.viewport(0, 0, w, h);
        gl.uniform3f(inst.uRes, w, h, w / h);
        // Square cells whatever the element's shape: 15 rows, aspect x 15 columns.
        gl.uniform2f(inst.uGrid, Math.max(0.5, (w / h) * density), density);
      }
    };

    // First child at z-index -1 (see the .fx-layer rule): the element's own
    // ::before/::after gloss and all of its children keep painting on top.
    host.insertBefore(canvas, host.firstChild);
    inst.resize();

    host.addEventListener("mousemove", function (e) {
      var r = host.getBoundingClientRect();
      inst.mouse.x = (e.clientX - r.left) / r.width;
      inst.mouse.y = 1 - (e.clientY - r.top) / r.height;
    }, { passive: true });

    if ("ResizeObserver" in window) new ResizeObserver(inst.resize).observe(host);
    return inst;
  }

  for (var i = 0; i < hosts.length; i++) {
    var inst = attach(hosts[i]);
    if (inst) instances.push(inst);
  }
  if (!instances.length) return;

  // Panels out of view cost nothing.
  if ("IntersectionObserver" in window) {
    var io = new IntersectionObserver(function (entries) {
      for (var i = 0; i < entries.length; i++) {
        for (var j = 0; j < instances.length; j++) {
          if (instances[j].host === entries[i].target) instances[j].visible = entries[i].isIntersecting;
        }
      }
    }, { rootMargin: "120px" });
    for (var k = 0; k < instances.length; k++) io.observe(instances[k].host);
  }

  var timeScale = 0.28;
  function frame(t) {
    requestAnimationFrame(frame);
    if (document.hidden) return;

    for (var i = 0; i < instances.length; i++) {
      var inst = instances[i];
      if (!inst.visible) continue;
      if (!inst.start) inst.start = t;

      var gl = inst.gl;
      gl.uniform1f(inst.uLoad, Math.min((t - inst.start) / 1400, 1));
      // Frozen time still gets a fully formed field, just no drift.
      gl.uniform1f(inst.uTime, reduced ? 9.0 : (t * 0.001 + inst.seed) * timeScale);

      inst.smooth.x += (inst.mouse.x - inst.smooth.x) * 0.08;
      inst.smooth.y += (inst.mouse.y - inst.smooth.y) * 0.08;
      gl.uniform2f(inst.uMouse, inst.smooth.x, inst.smooth.y);

      gl.drawArrays(gl.TRIANGLES, 0, 3);

      // Reduced motion: draw through the load-in, then leave the frame alone.
      if (reduced && t - inst.start > 1800) inst.visible = false;
    }
  }
  requestAnimationFrame(frame);
})();
</script>



</body></html>
```

