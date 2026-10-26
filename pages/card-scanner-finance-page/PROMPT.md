INSTALANDING.AI · Card Scanner Finance Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Card Scanner Finance Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/card-scanner-finance-page

nova-agentic-finance.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Card Scanner Finance Page
  slug     card-scanner-finance-page
  prompt   https://instalanding.ai/p/card-scanner-finance-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/card-scanner-finance-page
  license  MIT. Fictional brand; replace names, copy, figures and compliance claims before shipping.
  credit   Made by Beings (https://madebybeings.com). The card scanner is inspired by evervault (https://evervault.com/).

  MAP
  tokens    :root at the top of <style>: --bg/--bg-2 (near-black violet), --text/--muted, --lilac #c4b5fd,
            --violet #8b5cf6, --warm #e3857a, --cream #f1dba7. Headline gradients are palettes .g-lilac,
            .g-indigo, .g-ember (oklch stops --c0..--c3 + --glow). Inter Tight (display), Inter (copy),
            JetBrains Mono (UI) from Google Fonts.
  sections  hero, scanner, control, faq, cta (the super footer)
  scripts   GSAP 3.12.5 + ScrollTrigger and three.js r128 (cdnjs), then one inline <script>:
            card + ASCII builders; ParticleSystem (three.js additive points, the drifting dust);
            ParticleScanner (2D canvas light bar + particle spray at screen centre); one RAF loop that only
            renders sections on screen; scroll setup (pinned horizontal card track, headline gradient
            "light" scrubbed by scroll, reveals); the deploy CTA (a simulated agent run); the hero scene
            (fit-to-column scale, pointer tilt, orbit dust, a transaction walked through a checklist);
            the Control bento (live ledger, guardrail switches + autonomy meter, connector orbit, audit
            trail, approvals); the FAQ accordion; the footer newsletter (front end only).
  assets    none: cards, scene, orbit and wordmark are CSS, inline SVG and canvas.

  ADAPTING
  - The scanner is a fixed line at the viewport's horizontal centre; updateClipping() clips each card's
    solid and ASCII layers against it every frame. Keep the cards in .pin-wrap and the canvases full width.
  - The hero scene is built at a fixed 880x640 and scaled by fit() to its column; move pieces in that
    coordinate space, never in percentages.
  - Headline gradients are radial backgrounds clipped to text whose centre (--gy) GSAP scrubs with scroll;
    each .headline needs width: fit-content or the gradient box clips the longest line.
  - Under prefers-reduced-motion the decorative loops (orbit, glitch, floats, sweeps, the wordmark split)
    stop; the pinned scroll still works because the reader drives it.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>NOVA Agentic Finance</title>
<meta name="description" content="NOVA runs autonomous finance agents that read every transaction, tokenize every card, and reconcile and close the books in real time, with a person in the loop.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@600;700;800;900&family=Inter:wght@400;500;600&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
<style>
@property --split {
  syntax: "<percentage>";
  inherits: true;
  initial-value: 50%;
}

:root {
  --bg: #050508;
  --bg-2: #0b0a14;
  --text: #ece9ff;
  --muted: rgba(236, 233, 255, 0.55);
  --lilac: #c4b5fd;
  --violet: #8b5cf6;
  --warm: #e3857a;
  --cream: #f1dba7;
}

* { margin: 0; padding: 0; box-sizing: border-box; }

html, body { background: var(--bg); }

body {
  color: var(--text);
  font-family: "JetBrains Mono", monospace;
  overflow-x: hidden;
  overscroll-behavior: none;
  -webkit-font-smoothing: antialiased;
}

/* ---------- HERO ---------- */
.hero {
  --stats-h: 150px;
  position: relative;
  min-height: max(100vh, 760px);
  display: flex;
  flex-direction: column;
  overflow: hidden;
  isolation: isolate;
  background:
    radial-gradient(ellipse 42% 50% at 70% 40%, rgba(124, 58, 237, 0.22), transparent 70%),
    radial-gradient(ellipse 60% 40% at 0% 100%, rgba(76, 29, 149, 0.16), transparent 70%),
    linear-gradient(180deg, #08070f 0%, #050508 100%);
}

.hero-bg { position: absolute; inset: 0; z-index: 0; pointer-events: none; }
.hero-particles { position: absolute; top: 0; left: 0; opacity: 0.75; }
.hero-grid {
  position: absolute;
  top: 0; right: 0; bottom: var(--stats-h); left: 40%;
  background:
    repeating-linear-gradient(90deg, rgba(196, 181, 253, 0.04) 0 1px, transparent 1px 140px),
    repeating-linear-gradient(0deg, rgba(196, 181, 253, 0.025) 0 1px, transparent 1px 140px);
  -webkit-mask-image: radial-gradient(ellipse 70% 70% at 55% 45%, #000 20%, transparent 75%);
  mask-image: radial-gradient(ellipse 70% 70% at 55% 45%, #000 20%, transparent 75%);
}
.rocks {
  position: absolute;
  left: 0;
  bottom: calc(var(--stats-h) - 2px);
  width: 100%;
  height: clamp(140px, 22vh, 240px);
}
.water {
  position: absolute;
  left: 0; right: 0; bottom: 0;
  height: var(--stats-h);
  border-top: 1px solid rgba(196, 181, 253, 0.22);
  background:
    radial-gradient(ellipse 18% 70% at var(--beam-x, 66%) 0%, rgba(167, 139, 250, 0.42), transparent 70%),
    repeating-linear-gradient(180deg, rgba(196, 181, 253, 0.045) 0 1px, transparent 1px 6px),
    linear-gradient(180deg, #0d0a1c 0%, #060509 70%);
}
.water::before {
  content: "";
  position: absolute;
  top: -1px;
  left: var(--beam-x, 66%);
  width: 46vw;
  height: 2px;
  transform: translateX(-50%);
  background: linear-gradient(90deg, transparent, rgba(196, 181, 253, 0.85), #fff, rgba(196, 181, 253, 0.85), transparent);
  box-shadow: 0 0 18px rgba(167, 139, 250, 0.8);
}
.water::after {
  content: "";
  position: absolute;
  top: 0;
  left: var(--beam-x, 66%);
  width: 90px;
  height: 100%;
  transform: translateX(-50%);
  background:
    linear-gradient(90deg, transparent 47%, rgba(255, 255, 255, 0.9) 49% 51%, transparent 53%),
    repeating-linear-gradient(180deg, rgba(196, 181, 253, 0.45) 0 2px, transparent 2px 7px),
    radial-gradient(ellipse 50% 100% at 50% 0%, rgba(196, 181, 253, 0.5), transparent 75%);
  -webkit-mask-image: linear-gradient(180deg, #000 0%, transparent 92%);
  mask-image: linear-gradient(180deg, #000 0%, transparent 92%);
  filter: blur(0.6px);
  opacity: 0.85;
}

/* ---------- NAV ---------- */
.nav {
  position: relative;
  z-index: 40;
  display: grid;
  grid-template-columns: 1fr auto 1fr;
  align-items: center;
  padding: 26px 6vw;
}
.brand {
  justify-self: start;
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: "Inter Tight", sans-serif;
  font-weight: 800;
  font-size: 15px;
  letter-spacing: 0.16em;
  color: var(--text);
  text-decoration: none;
}
.brand i {
  width: 9px; height: 9px;
  border-radius: 50%;
  background: var(--lilac);
  box-shadow: 0 0 14px var(--violet);
}
.nav-links { display: flex; gap: clamp(20px, 2.6vw, 44px); }
.nav-links a {
  font-size: 12.5px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: rgba(236, 233, 255, 0.78);
  text-decoration: none;
  transition: color 0.25s;
}
.nav-links a:hover { color: #fff; }
.nav-cta {
  justify-self: end;
  font-size: 12.5px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--text);
  text-decoration: none;
  padding: 11px 18px;
  border-radius: 999px;
  border: 1px solid rgba(236, 233, 255, 0.4);
  transition: background 0.25s, border-color 0.25s;
}
.nav-cta:hover { background: rgba(196, 181, 253, 0.12); border-color: var(--lilac); }

/* ---------- HERO COPY ---------- */
.hero-main {
  position: relative;
  z-index: 10;
  flex: 1;
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1.15fr);
  align-items: center;
  gap: 2vw;
  padding-left: 6vw;
  min-height: 540px;
}
.hero-copy { position: relative; z-index: 12; padding: 30px 0 60px; }

.eyebrow {
  display: inline-flex;
  align-items: center;
  gap: 9px;
  margin-bottom: 26px;
  padding: 7px 14px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.28);
  background: rgba(196, 181, 253, 0.05);
  font-size: 12px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--text);
}
.eyebrow i {
  width: 7px; height: 7px;
  border-radius: 50%;
  background: #4ade80;
  box-shadow: 0 0 10px #4ade80;
  animation: pulse 1.6s ease-in-out infinite;
}
@keyframes pulse { 50% { opacity: 0.35; } }

/* ---------- HEADLINES: heavy type lit by a scroll-driven gradient ---------- */
.headline {
  --gy: 50vh;
  font-family: "Inter Tight", "Inter", system-ui, sans-serif;
  font-weight: 900;
  line-height: 0.9;
  letter-spacing: -0.045em;
  /* room for the clipped gradient on the glyph edges, without shifting layout */
  padding: 0.08em 0.06em 0.12em;
  margin: -0.08em -0.06em -0.12em;
}
.grad { color: var(--text); }
@supports ((background-clip: text) or (-webkit-background-clip: text)) and (color: oklch(0 0 0)) {
  .grad {
    color: transparent;
    -webkit-text-fill-color: transparent;
    -webkit-background-clip: text;
    background-clip: text;
    background-image: radial-gradient(circle at 50% var(--gy), var(--c0) 0vh, var(--c1) 50vh, var(--c2) 90vh, var(--c3) 150vh);
    background-image: radial-gradient(in oklch circle at 50% var(--gy), var(--c0) 0vh, var(--c1) 50vh, var(--c2) 90vh, var(--c3) 150vh);
  }
  .headline.grad { filter: drop-shadow(0 0 30px var(--glow)); }
}
/* palettes pulled from the page: lilac brand, indigo orbit, ember CTA glow */
.g-lilac {
  --c0: oklch(0.98 0.03 300);
  --c1: oklch(0.84 0.12 298);
  --c2: oklch(0.58 0.22 290);
  --c3: oklch(0.2 0.08 285 / 0);
  --glow: oklch(0.65 0.22 295 / 0.18);
}
.g-indigo {
  --c0: oklch(0.96 0.05 280);
  --c1: oklch(0.77 0.16 276);
  --c2: oklch(0.52 0.22 270);
  --c3: oklch(0.18 0.08 270 / 0);
  --glow: oklch(0.6 0.2 275 / 0.18);
}
.g-ember {
  --c0: oklch(0.95 0.08 85);
  --c1: oklch(0.77 0.16 42);
  --c2: oklch(0.64 0.17 30);
  --c3: oklch(0.2 0.08 340 / 0);
  --glow: oklch(0.7 0.18 40 / 0.18);
}

h1.headline {
  width: fit-content; /* gradient box always covers the longest line */
  font-size: clamp(2.8rem, 5.9vw, 6.8rem);
  letter-spacing: -0.035em;
  text-transform: uppercase;
}
@media (max-width: 960px) {
  h1.headline { font-size: min(12.4vw, 4.6rem); }
}
h1 span { display: block; }

/* descriptions: Inter, paired with Inter Tight headlines and JetBrains Mono UI */
.hero-lede, .pin-intro p, .caption span, .cta-panel > p {
  font-family: "Inter", system-ui, sans-serif;
  letter-spacing: -0.005em;
}

.hero-lede {
  margin-top: 28px;
  max-width: 560px;
  font-size: clamp(15px, 1.15vw, 18px);
  line-height: 1.6;
  color: rgba(236, 233, 255, 0.7);
}
.hero-lede strong { color: #fff; font-weight: 600; }

.hero-actions { display: flex; gap: 20px; margin-top: 38px; flex-wrap: wrap; }
.btn {
  display: inline-flex;
  align-items: center;
  gap: 14px;
  height: 58px;
  padding: 0 30px;
  border-radius: 999px;
  font-family: "JetBrains Mono", monospace;
  font-size: 13px;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  text-decoration: none;
  transition: transform 0.3s, box-shadow 0.3s, background 0.3s, border-color 0.3s;
}
.btn svg { width: 18px; height: 18px; transition: transform 0.3s; }
.btn-primary {
  background: #ece9ff;
  color: #0b0a14;
  box-shadow: 0 10px 40px rgba(196, 181, 253, 0.25);
}
.btn-primary:hover { transform: translateY(-2px); box-shadow: 0 14px 50px rgba(196, 181, 253, 0.42); }
.btn-primary:hover svg { transform: translateX(4px); }
.btn-ghost {
  color: var(--text);
  border: 1px solid rgba(196, 181, 253, 0.28);
  background: rgba(255, 255, 255, 0.02);
}
.btn-ghost:hover { background: rgba(196, 181, 253, 0.1); border-color: var(--lilac); }
.play {
  width: 24px; height: 24px;
  border-radius: 50%;
  border: 1.5px solid currentColor;
  display: grid;
  place-items: center;
}
.play svg { width: 9px; height: 9px; margin-left: 2px; }

.rise { animation: rise 0.9s cubic-bezier(0.2, 0.7, 0.2, 1) both; animation-delay: var(--d, 0s); }
@keyframes rise { from { opacity: 0; translate: 0 22px; } }

/* ---------- HERO SCENE ---------- */
.hero-scene { position: relative; align-self: stretch; min-height: 520px; }
.scene-inner {
  position: absolute;
  right: 4vw;
  bottom: 0;
  width: 880px;
  height: 640px;
  transform-origin: 100% 100%;
  transform: scale(var(--s, 1)) perspective(2200px) rotateX(var(--rx, 0deg)) rotateY(var(--ry, 0deg));
  transition: transform 0.8s cubic-bezier(0.2, 0.7, 0.2, 1);
  animation: sceneIn 1.4s 0.2s cubic-bezier(0.2, 0.7, 0.2, 1) both;
}
@keyframes sceneIn { from { opacity: 0; filter: blur(8px); } to { opacity: 1; filter: blur(0); } }

.ring { position: absolute; left: 0; top: 0; width: 880px; height: 640px; overflow: visible; }
.ring-run { animation: ringRun 7s linear infinite; filter: drop-shadow(0 0 6px #c4b5fd); }
@keyframes ringRun { to { stroke-dashoffset: -1000; } }
.tw { animation: twinkle 2.6s ease-in-out infinite; }
@keyframes twinkle { 50% { opacity: 0.1; } }

.glass {
  position: absolute;
  border: 1px solid rgba(196, 181, 253, 0.3);
  border-radius: 14px;
  background: linear-gradient(160deg, rgba(46, 30, 96, 0.32), rgba(10, 8, 22, 0.55));
  box-shadow: inset 0 0 0 1px rgba(196, 181, 253, 0.04), 0 0 40px rgba(139, 92, 246, 0.14);
  color: rgba(226, 218, 255, 0.85);
  font-family: "JetBrains Mono", monospace;
}
.panel-json {
  left: 245px; top: 50px;
  width: 310px;
  padding: 16px 20px;
  transform: perspective(1200px) rotateY(-14deg) rotateX(10deg) rotateZ(-8deg);
}
.panel-json pre { font-size: 12px; line-height: 1.55; white-space: pre; }
.panel-json .k { color: rgba(196, 181, 253, 0.95); }
.panel-json .v { color: rgba(236, 233, 255, 0.82); transition: color 0.5s, text-shadow 0.5s; }
.panel-json .v.flash { color: #fff; text-shadow: 0 0 10px rgba(167, 139, 250, 0.95); }

.panel-code {
  left: 30px; top: 230px;
  width: 180px; height: 170px;
  padding: 14px 16px;
  overflow: hidden;
  opacity: 0.85;
  transform: perspective(1200px) rotateY(24deg) rotateX(4deg) rotateZ(-3deg);
}
.panel-ghost {
  left: 615px; top: 0;
  width: 150px; height: 105px;
  padding: 10px 12px;
  overflow: hidden;
  opacity: 0.35;
  transform: perspective(1200px) rotateY(-18deg) rotateZ(-6deg);
}
.panel-code pre, .panel-ghost pre {
  font-size: 9.5px;
  line-height: 1.4;
  color: rgba(196, 181, 253, 0.6);
  white-space: pre;
}

.panel-check {
  left: 700px; top: 300px;
  width: 195px;
  padding: 14px 18px;
  transform: perspective(1200px) rotateY(-22deg) rotateX(4deg) rotateZ(4deg);
}
.panel-check ul { list-style: none; }
.panel-check li {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 5px 0;
  font-size: 12.5px;
  color: rgba(236, 233, 255, 0.45);
  transition: color 0.4s;
}
.panel-check li i {
  width: 9px; height: 9px;
  flex-shrink: 0;
  border-radius: 50%;
  background: rgba(196, 181, 253, 0.3);
  transition: background 0.4s, box-shadow 0.4s;
}
.panel-check li.active { color: #fff; }
.panel-check li.active i {
  background: #c4b5fd;
  box-shadow: 0 0 0 4px rgba(196, 181, 253, 0.15), 0 0 14px #8b5cf6;
  animation: pulse 1s ease-in-out infinite;
}
.panel-check li.done { color: rgba(236, 233, 255, 0.88); }
.panel-check li.done i { background: #a78bfa; box-shadow: 0 0 10px rgba(139, 92, 246, 0.8); }

/* hero cards */
.hcard { position: absolute; }
.hcard .card-wrapper { width: 100%; height: auto; aspect-ratio: 1.6; }
.hcard-copper { left: 490px; top: 45px; width: 360px; animation: floatB 7s ease-in-out infinite; }
.hcard-copper .card-wrapper {
  font-size: 14.5px;
  transform: perspective(1400px) rotateY(-24deg) rotateX(14deg) rotateZ(-11deg);
}
.hcard-graphite { left: 210px; top: 215px; width: 500px; animation: floatA 6s ease-in-out infinite; }
.hcard-graphite .card-wrapper {
  font-size: 20px;
  transform: perspective(1400px) rotateY(-22deg) rotateX(14deg) rotateZ(-9deg);
}
@keyframes floatA { 50% { translate: 0 -12px; } }
@keyframes floatB { 50% { translate: 0 10px; } }

.hcard .card-normal {
  clip-path: none;
  box-shadow: 0 40px 80px rgba(0, 0, 0, 0.65), 0 0 70px rgba(139, 92, 246, 0.28);
}
.hcard .card-normal::after {
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  border: 1px solid rgba(255, 255, 255, 0.18);
  pointer-events: none;
}
.hcard .card-logo { font-size: 1.2em; transform: skewX(-10deg); }
.hcard .card-number { font-weight: 500; letter-spacing: 0.16em; }

.theme-graphite {
  background:
    repeating-linear-gradient(90deg, rgba(255, 255, 255, 0.03) 0 1px, transparent 1px 3px),
    linear-gradient(135deg, #26262d 0%, #4d4d58 34%, #1b1b21 68%, #3a3a45 100%);
}
.theme-copper {
  background:
    repeating-linear-gradient(90deg, rgba(255, 255, 255, 0.025) 0 1px, transparent 1px 3px),
    linear-gradient(135deg, #5a1f0e 0%, #a84a24 40%, #d98a5f 64%, #8a3a1c 100%);
}

.sweep {
  position: absolute;
  top: 0; bottom: 0;
  left: -40%;
  width: 40%;
  opacity: 0;
  pointer-events: none;
  z-index: 3;
  background: linear-gradient(90deg, transparent, rgba(196, 181, 253, 0.28) 70%, rgba(255, 255, 255, 0.9) 98%, transparent);
  mix-blend-mode: screen;
}
.sweep.go { animation: sweep 1.1s cubic-bezier(0.5, 0, 0.3, 1); }
@keyframes sweep {
  0% { left: -40%; opacity: 1; }
  100% { left: 110%; opacity: 1; }
}

/* light beam into the water */
.beam {
  position: absolute;
  left: 452px; top: 495px;
  width: 3px; height: 145px;
  transform: translateX(-50%);
  border-radius: 2px;
  background: linear-gradient(180deg, rgba(196, 181, 253, 0), #c4b5fd 40%, #fff);
  box-shadow: 0 0 12px #a78bfa, 0 0 30px rgba(139, 92, 246, 0.8);
  animation: beamPulse 3s ease-in-out infinite;
}
@keyframes beamPulse { 50% { opacity: 0.65; } }
.beam-lines {
  position: absolute;
  left: 452px; bottom: 0;
  width: 150px; height: 115px;
  transform: translateX(-50%);
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
}
.beam-lines i { width: 1px; background: linear-gradient(180deg, transparent, rgba(196, 181, 253, 0.6)); }
.beam-base {
  position: absolute;
  left: 452px; bottom: -30px;
  width: 260px; height: 60px;
  transform: translateX(-50%);
  background: radial-gradient(ellipse at center, rgba(233, 222, 255, 0.9), rgba(139, 92, 246, 0.4) 35%, transparent 70%);
  filter: blur(4px);
}

.pipeline {
  position: absolute;
  left: 100px; top: 552px;
  display: flex;
  align-items: center;
  gap: 22px;
  transform: rotateZ(-3deg);
  font-size: 11px;
  letter-spacing: 0.28em;
  text-transform: uppercase;
}
.pipeline span { color: rgba(196, 181, 253, 0.5); transition: color 0.4s, text-shadow 0.4s; }
.pipeline span.on { color: #fff; text-shadow: 0 0 12px #a78bfa; }
.pipeline em { font-style: normal; letter-spacing: 0; color: rgba(196, 181, 253, 0.3); }
.plus { position: absolute; font-size: 22px; font-weight: 300; line-height: 1; color: rgba(196, 181, 253, 0.6); }

/* ---------- HERO STATS ---------- */
.hero-stats {
  position: relative;
  z-index: 12;
  height: var(--stats-h);
  margin: 0 6vw;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  align-content: center;
}
.stat {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding: 6px 12px;
  text-align: center;
  border-left: 1px solid rgba(196, 181, 253, 0.16);
}
.stat:first-child { border-left: none; }
.stat b {
  font-family: "JetBrains Mono", monospace;
  font-weight: 700;
  font-size: clamp(1.6rem, 2.4vw, 2.4rem);
  letter-spacing: -0.02em;
  color: #e4dcff;
  text-shadow: 0 0 24px rgba(139, 92, 246, 0.5);
}
.stat span { font-size: 13px; letter-spacing: 0.04em; color: rgba(236, 233, 255, 0.62); }

@media (max-width: 960px) {
  .hero { --stats-h: 200px; min-height: auto; }
  .hero-main { grid-template-columns: 1fr; padding: 0 6vw; min-height: 0; }
  .hero-copy { padding: 24px 0 0; }
  .hero-scene { min-height: 0; height: min(80vw, 560px); }
  .scene-inner {
    right: auto;
    left: 50%;
    transform-origin: 0 100%;
    margin-left: calc(-440px * var(--s, 1));
  }
  .hero-grid { left: 0; }
  .nav { grid-template-columns: 1fr auto; }
  .hero-stats { grid-template-columns: repeat(2, 1fr); row-gap: 22px; }
  .stat:nth-child(3) { border-left: none; }
  .btn { height: 52px; padding: 0 22px; }
}

/* ---------- CARDS ---------- */
.card-wrapper {
  position: relative;
  width: 400px;
  height: 250px;
  flex-shrink: 0;
  font-size: 16px;
}

.card {
  position: absolute;
  inset: 0;
  border-radius: 15px;
  overflow: hidden;
}

.card-normal {
  color: #fff;
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.5);
  z-index: 2;
  clip-path: inset(0 0 0 var(--clip-right, 0%));
}

.card-face {
  position: absolute;
  inset: 0;
  padding: 1.4em 1.5em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.card-face::before {
  content: "";
  position: absolute;
  inset: 0;
  background:
    linear-gradient(115deg, transparent 30%, rgba(255, 255, 255, 0.16) 45%, transparent 60%),
    repeating-linear-gradient(135deg, rgba(255, 255, 255, 0.025) 0 2px, transparent 2px 9px);
  pointer-events: none;
}
.card-face > * { position: relative; }

.theme-0 { background: linear-gradient(135deg, #1e1b4b 0%, #4c1d95 55%, #7c3aed 100%); }
.theme-1 { background: linear-gradient(135deg, #020617 0%, #0e7490 60%, #22d3ee 100%); }
.theme-2 { background: linear-gradient(135deg, #0c0a09 0%, #27272a 50%, #52525b 100%); }
.theme-3 { background: linear-gradient(135deg, #431407 0%, #c2410c 55%, #e3857a 100%); }
.theme-4 { background: linear-gradient(135deg, #1c1917 0%, #57534e 50%, #bcb8ad 100%); }

.card-top { display: flex; align-items: center; gap: 0.8em; }

.card-chip {
  width: 2.6em;
  height: 1.9em;
  background: linear-gradient(45deg, #ffd700, #ffed4e);
  border-radius: 0.35em;
  position: relative;
}
.card-chip::before {
  content: "";
  position: absolute;
  inset: 3px;
  background:
    linear-gradient(90deg, transparent 32%, rgba(0,0,0,0.18) 32% 36%, transparent 36% 64%, rgba(0,0,0,0.18) 64% 68%, transparent 68%),
    linear-gradient(45deg, #e6c200, #f4d03f);
  border-radius: 2px;
}

.contactless {
  position: relative;
  width: 1.5em;
  height: 1.5em;
  border: 2px solid rgba(255, 255, 255, 0.8);
  border-radius: 50%;
  background: radial-gradient(circle, rgba(255, 255, 255, 0.2), transparent);
}
.contactless::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 0.8em;
  height: 0.8em;
  border: 1px solid rgba(255, 255, 255, 0.6);
  border-radius: 50%;
}

.card-logo {
  margin-left: auto;
  font-family: "Inter Tight", sans-serif;
  font-weight: 800;
  font-size: 1.05em;
  letter-spacing: 0.14em;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.card-number {
  font-size: 1.35em;
  font-weight: 500;
  letter-spacing: 0.14em;
  text-shadow: 0 2px 4px rgba(0, 0, 0, 0.35);
}

.card-info { display: flex; justify-content: space-between; align-items: flex-end; }
.card-info small {
  display: block;
  font-size: 0.55em;
  opacity: 0.65;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  margin-bottom: 0.3em;
}
.card-holder, .card-expiry { font-size: 0.85em; letter-spacing: 0.08em; text-transform: uppercase; }

.card-ascii {
  z-index: 1;
  background: rgba(12, 10, 24, 0.55);
  border: 1px solid rgba(196, 181, 253, 0.18);
  clip-path: inset(0 calc(100% - var(--clip-left, 0%)) 0 0);
}

.ascii-content {
  position: absolute;
  inset: 0;
  color: rgba(220, 210, 255, 0.6);
  font-family: "Courier New", monospace;
  font-size: 11px;
  line-height: 13px;
  overflow: hidden;
  white-space: pre;
  clip-path: inset(0 calc(100% - var(--clip-left, 0%)) 0 0);
  animation: glitch 0.1s infinite linear alternate-reverse;
  -webkit-mask-image: linear-gradient(to right, #000 0%, rgba(0,0,0,0.8) 30%, rgba(0,0,0,0.6) 50%, rgba(0,0,0,0.4) 80%, rgba(0,0,0,0.2) 100%);
  mask-image: linear-gradient(to right, #000 0%, rgba(0,0,0,0.8) 30%, rgba(0,0,0,0.6) 50%, rgba(0,0,0,0.4) 80%, rgba(0,0,0,0.2) 100%);
}

@keyframes glitch {
  0% { opacity: 1; } 15% { opacity: 0.9; } 16% { opacity: 1; }
  49% { opacity: 0.8; } 50% { opacity: 1; } 99% { opacity: 0.9; } 100% { opacity: 1; }
}

.scan-effect {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, transparent, rgba(196, 181, 253, 0.4), transparent);
  animation: scanEffect 0.6s ease-out;
  pointer-events: none;
  z-index: 5;
  border-radius: 15px;
}
@keyframes scanEffect {
  0% { transform: translateX(-100%); opacity: 0; }
  50% { opacity: 1; }
  100% { transform: translateX(100%); opacity: 0; }
}

/* ---------- PINNED HORIZONTAL SECTION ---------- */
#sectionPin {
  --cw: min(520px, 78vw, calc((100svh - 240px) * 1.6));
  position: relative;
  height: 100vh;
  height: 100svh;
  overflow: hidden;
  background:
    linear-gradient(rgba(196, 181, 253, 0.04) 1px, transparent 1px) 0 0 / 100% 64px,
    linear-gradient(90deg, rgba(196, 181, 253, 0.04) 1px, transparent 1px) 0 0 / 64px 100%,
    var(--bg-2);
}

#sectionPin .fx-particles,
#sectionPin .fx-scanner {
  position: absolute;
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 100vw;
  pointer-events: none;
}
#sectionPin .fx-particles { z-index: 0; }
#sectionPin .fx-scanner { z-index: 15; }

.pin-label {
  position: absolute;
  top: 32px;
  left: 6vw;
  font-size: 12px;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--muted);
  z-index: 20;
}
.pin-label b { color: var(--lilac); font-weight: 500; }

.pin-progress {
  position: absolute;
  left: 6vw;
  right: 6vw;
  bottom: 36px;
  height: 1px;
  background: rgba(196, 181, 253, 0.15);
  z-index: 20;
}
.pin-progress i {
  position: absolute;
  inset: 0;
  background: var(--lilac);
  transform-origin: left;
  transform: scaleX(0);
  box-shadow: 0 0 12px var(--violet);
}

.pin-wrap {
  position: relative;
  z-index: 10;
  height: 100%;
  width: max-content;
  display: flex;
  align-items: center;
  gap: 10vw;
  padding: 0 50vw 0 8vw;
}

.pin-intro { width: min(520px, 80vw); }
.pin-intro h2 {
  font-size: clamp(1.7rem, 2.9vw, 2.9rem);
  line-height: 1.02;
  letter-spacing: -0.022em;
}
.pin-intro p {
  margin-top: 1.4rem;
  font-size: 15px;
  line-height: 1.55;
  color: var(--muted);
}

.panel { position: relative; }
.panel .card-wrapper {
  width: var(--cw);
  height: auto;
  aspect-ratio: 1.6;
  font-size: calc(var(--cw) / 25);
}
.caption {
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  margin-top: 22px;
  font-size: 12px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--text);
}
.caption b { color: var(--lilac); font-weight: 500; margin-right: 0.8em; }
.caption span {
  display: block;
  margin-top: 8px;
  font-size: 14.5px;
  letter-spacing: -0.005em;
  text-transform: none;
  line-height: 1.5;
  color: var(--muted);
  max-width: min(420px, var(--cw));
}

/* tablet */
@media (max-width: 1024px) {
  .pin-wrap { gap: 12vw; padding-left: 7vw; }
  .pin-intro { width: min(520px, 72vw); }
}

/* phone portrait */
@media (max-width: 640px) {
  #sectionPin { --cw: min(84vw, calc((100svh - 260px) * 1.6)); }
  .pin-label { top: 22px; left: 6vw; font-size: 11px; }
  .pin-progress { bottom: 24px; }
  .pin-wrap { gap: 16vw; padding-left: 6vw; }
  .pin-intro { width: 86vw; }
  .pin-intro h2 { font-size: clamp(1.6rem, 7.4vw, 2.1rem); line-height: 1.02; }
  .pin-intro p { font-size: 14px; margin-top: 1rem; }
  .stats { gap: 14px 22px; margin-top: 1.4rem; }
  .stats b { font-size: 1.15rem; }
  .stats span { font-size: 10px; }
  .caption { margin-top: 16px; font-size: 11px; }
  .caption span { font-size: 13.5px; }
}

/* short screens: landscape phones, small tablets on their side */
@media (max-height: 520px) {
  #sectionPin { --cw: min(78vw, calc((100svh - 150px) * 1.6)); }
  .pin-label { top: 14px; }
  .pin-progress { bottom: 14px; }
  .pin-intro { width: min(560px, 60vw); }
  .pin-intro h2 { font-size: clamp(1.15rem, 4vh + 0.5vw, 1.7rem); line-height: 1.02; }
  .pin-intro p { display: none; }
  .stats { margin-top: 1rem; gap: 10px 22px; }
  .stats b { font-size: 1.05rem; }
  .caption { margin-top: 10px; }
  .caption span { display: none; }
}

.stats {
  display: flex;
  gap: 32px;
  margin-top: 2rem;
  flex-wrap: wrap;
}
.stats b {
  display: block;
  font-family: "Inter Tight", sans-serif;
  font-size: 1.6rem;
  font-weight: 800;
  letter-spacing: -0.03em;
  color: var(--lilac);
}
.stats span {
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
}

/* ---------- OUTRO ---------- */
.outro {
  position: relative;
  min-height: 100vh;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(320px, 100%), 1fr));
  gap: 4rem;
  padding: 100px 8vw 120px;
  place-items: center;
  overflow: hidden;
  background:
    radial-gradient(ellipse 50% 45% at 30% 50%, rgba(227, 133, 122, 0.22), transparent 70%),
    var(--bg);
}

.static-card .card-wrapper {
  width: min(440px, 80vw);
  height: auto;
  aspect-ratio: 1.6;
  font-size: min(17.6px, 3.2vw);
  animation: split 3.6s ease-in-out infinite alternate;
}
.static-card .card-normal { clip-path: inset(0 0 0 var(--split)); }
.static-card .card-ascii { clip-path: inset(0 calc(100% - var(--split)) 0 0); }
.static-card .ascii-content { clip-path: none; }
.static-scan {
  position: absolute;
  top: -10%;
  bottom: -10%;
  left: var(--split);
  width: 3px;
  transform: translateX(-50%);
  border-radius: 3px;
  background: linear-gradient(to bottom, transparent, #fff 20%, #fff 80%, transparent);
  box-shadow: 0 0 12px rgba(196, 181, 253, 0.9), 0 0 32px rgba(139, 92, 246, 0.6);
  z-index: 6;
}
@keyframes split { from { --split: 12%; } to { --split: 88%; } }

.static-col { display: flex; flex-direction: column; align-items: center; gap: 22px; }
.static-col small {
  font-size: 11px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--muted);
}
.static-col small b { color: var(--cream); font-weight: 500; }

/* ---------- AGENTIC CTA ---------- */
.cta-panel {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  width: 100%;
  max-width: 540px;
  padding: 48px 40px 40px;
  border-radius: 24px;
  background: linear-gradient(180deg, #0f0d1a, #08070d);
  border: 1px solid rgba(196, 181, 253, 0.14);
  box-shadow: 0 40px 120px rgba(0, 0, 0, 0.6);
}
.cta-panel h2 {
  font-size: clamp(2.1rem, 3.8vw, 3.4rem);
  line-height: 0.98;
  letter-spacing: -0.025em;
}
.cta-panel h2 em { font-style: normal; }
.cta-panel > p {
  margin-top: 18px;
  font-size: 15px;
  line-height: 1.6;
  color: var(--muted);
}

.cta-wrap {
  position: relative;
  width: 286px;
  height: 70px;
  margin: 40px 0 30px;
}

.real-button {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  z-index: 3;
  border: none;
  outline: none;
  border-radius: 24px;
  cursor: pointer;
  opacity: 0;
  font-size: 0;
}

.button-container {
  position: relative;
  width: 286px;
  height: 70px;
  border-radius: 24px;
}

.button-border {
  position: relative;
  padding: 3px;
  width: 286px;
  height: 70px;
  background: #0005;
  border-radius: inherit;
  clip-path: path("M 251 0 C 281 0 286 5 286 35 C 286 65 281 70 251 70 L 35 70 C 5 70 0 65 0 35 C 0 5 5 0 35 0 Z");
}

.button {
  position: relative;
  z-index: 1;
  width: 280px;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  background: #111215;
  color: #fff;
  font-family: "JetBrains Mono", monospace;
  font-weight: 500;
  font-size: 14px;
  letter-spacing: 0.04em;
  clip-path: path("M 248 0 C 275 0 280 5 280 32 C 280 59 275 64 248 64 L 32 64 C 5 64 0 59 0 32 C 0 5 5 0 32 0 Z");
  overflow: hidden;
}
.button svg { width: 18px; height: 18px; flex-shrink: 0; }
.button .arrow { transition: transform 0.3s; }
.real-button:hover ~ .button-container .arrow { transform: translateX(4px); }
.real-button:focus-visible ~ .button-container { outline: 2px solid var(--lilac); outline-offset: 4px; }
.nav a:focus-visible, .btn:focus-visible, .link-arrow:focus-visible { outline: 2px solid var(--lilac); outline-offset: 4px; border-radius: 999px; }
.cta-wrap.running .arrow { display: none; }
.cta-wrap.running .button svg { animation: spinIcon 1.4s linear infinite; }
@keyframes spinIcon { to { transform: rotate(360deg); } }

.dots::after {
  content: "";
  display: inline-block;
  width: 1.5em;
  text-align: left;
  animation: dots 1.2s steps(4) infinite;
}
@keyframes dots {
  0% { content: ""; } 25% { content: "."; } 50% { content: ".."; } 75% { content: "..."; }
}

.backdrop {
  position: absolute;
  inset: -9900%;
  background: radial-gradient(circle at 50% 50%, #0000 0, #0000 20%, #111111aa 50%);
  background-size: 3px 3px;
  z-index: -1;
  pointer-events: none;
}

.spin {
  position: absolute;
  inset: 0;
  z-index: -2;
  opacity: 0.5;
  overflow: hidden;
  transition: 0.3s;
  pointer-events: none;
}
.real-button:active ~ .button-container .spin,
.real-button:focus-visible ~ .button-container .spin,
.cta-wrap.running .spin { opacity: 1; }
.cta-wrap.done .spin { opacity: 0.8; }

.spin-blur { filter: blur(2em) url(#unopaq); }
.spin-intense {
  inset: -0.125em;
  filter: blur(0.25em) url(#unopaq2);
  border-radius: 0.75em;
}
.spin-inside {
  inset: -2px;
  border-radius: inherit;
  filter: blur(2px) url(#unopaq3);
  z-index: 0;
}

.spin::before {
  content: "";
  position: absolute;
  inset: -150%;
  animation:
    speen 8s cubic-bezier(0.56, 0.15, 0.28, 0.86) infinite,
    woah 4s infinite;
  animation-play-state: paused;
}
.real-button:hover ~ .button-container .spin::before,
.real-button:focus-visible ~ .button-container .spin::before,
.cta-wrap.running .spin::before,
.cta-wrap.done .spin::before { animation-play-state: running; }
.cta-wrap.running .spin::before { animation-duration: 2.4s, 1.6s; }

.spin-blur::before { background: linear-gradient(90deg, #ff5a1f 30%, #0000 50%, #5b5cff 70%); }
.spin-intense::before { background: linear-gradient(90deg, #ff9a6b 20%, #0000 45% 55%, #8f8bff 80%); }
.spin-inside::before { background: linear-gradient(90deg, #ffd2b0 30%, #0000 45% 55%, #c4b5fd 70%); }

@keyframes speen {
  0% { rotate: 10deg; }
  50% { rotate: 190deg; }
  to { rotate: 370deg; }
}
@keyframes woah {
  0%, to { scale: 1; }
  50% { scale: 0.75; }
}

.agent-log {
  border-top: 1px solid rgba(196, 181, 253, 0.12);
  padding-top: 18px;
  font-size: 12.5px;
  line-height: 1.9;
  min-height: 150px;
}
.log-line {
  display: flex;
  gap: 10px;
  opacity: 0;
  transform: translateY(4px);
  transition: opacity 0.35s, transform 0.35s;
}
.log-line.show { opacity: 1; transform: none; }
.log-line .pr { color: var(--lilac); }
.log-line .st { margin-left: auto; color: var(--muted); white-space: nowrap; }
.log-line .st.ok { color: #86efac; }
.log-line .st.flag { color: #fbbf24; }
.log-line.idle { color: var(--muted); }
.log-line.final { color: var(--cream); margin-top: 6px; }
.log-line.final a { color: var(--cream); margin-left: auto; text-decoration: none; border-bottom: 1px solid rgba(241, 219, 167, 0.4); }
.log-line.final a:hover { color: var(--warm); }

.trust {
  display: flex;
  flex-wrap: wrap;
  gap: 8px 18px;
  margin-top: 22px;
  font-size: 10.5px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: rgba(236, 233, 255, 0.4);
}

.site-foot {
  position: absolute;
  left: 6vw;
  right: 6vw;
  bottom: 28px;
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  flex-wrap: wrap;
  font-size: 11px;
  letter-spacing: 0.08em;
  color: var(--muted);
}
.site-foot a { color: var(--cream); text-decoration: none; }
.site-foot a:hover { color: var(--warm); }

@media (max-width: 768px) {
  .nav-links { display: none; }
  .outro { padding: 90px 16px 120px; }
  .cta-panel { padding: 36px 20px 28px; }
}
@media (max-width: 360px) {
  .cta-wrap { transform: scale(0.86); transform-origin: left center; }
}

[hidden] { display: none !important; }

/* =========================================================
   SHARED SECTION DNA
   ========================================================= */
.sec { position: relative; padding: clamp(96px, 14vh, 160px) 6vw; overflow: hidden; }
.sec-label {
  display: inline-flex;
  align-items: center;
  gap: 0.7em;
  font-family: "JetBrains Mono", monospace;
  font-size: 12px;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--muted);
}
.sec-label b { color: var(--lilac); font-weight: 500; }
.sec-lede {
  font-family: "Inter", system-ui, sans-serif;
  font-size: clamp(15px, 1.1vw, 17px);
  line-height: 1.6;
  color: rgba(236, 233, 255, 0.66);
  max-width: 460px;
}
.sec h2.headline { margin-top: 22px; font-size: clamp(2.4rem, 5.2vw, 5rem); line-height: 0.95; letter-spacing: -0.035em; }

.link-arrow {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding-bottom: 4px;
  font-family: "JetBrains Mono", monospace;
  font-size: 12.5px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--cream);
  text-decoration: none;
  border-bottom: 1px solid rgba(241, 219, 167, 0.3);
  transition: color 0.25s, border-color 0.25s;
}
.link-arrow svg { width: 15px; height: 15px; transition: transform 0.3s; }
.link-arrow:hover { color: #fff; border-color: var(--cream); }
.link-arrow:hover svg { transform: translateX(4px); }

/* glass tile with a hairline gradient border and a pointer-following glow */
.tile {
  position: relative;
  border-radius: 20px;
  background: linear-gradient(180deg, rgba(22, 18, 40, 0.72), rgba(10, 9, 18, 0.85));
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.45), inset 0 1px 0 rgba(255, 255, 255, 0.04);
  overflow: hidden;
  isolation: isolate;
}
.tile::before,
.cta-panel::before {
  content: "";
  position: absolute;
  inset: 0;
  padding: 1px;
  border-radius: inherit;
  background: linear-gradient(150deg, rgba(196, 181, 253, 0.5), rgba(196, 181, 253, 0.06) 35%, rgba(196, 181, 253, 0.04) 65%, rgba(241, 219, 167, 0.34));
  -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
  z-index: 3;
}
.tile::after {
  content: "";
  position: absolute;
  inset: 0;
  background: radial-gradient(380px circle at var(--mx, 50%) var(--my, 0%), rgba(139, 92, 246, 0.14), transparent 60%);
  opacity: 0;
  transition: opacity 0.4s;
  pointer-events: none;
  z-index: 0;
}
.tile:hover::after { opacity: 1; }
.tile-in { position: relative; z-index: 1; height: 100%; display: flex; flex-direction: column; padding: 26px 26px 24px; }
.tile-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--muted);
}
.live { display: inline-flex; align-items: center; gap: 7px; color: #86efac; }
.live i { width: 6px; height: 6px; border-radius: 50%; background: #4ade80; box-shadow: 0 0 8px #4ade80; animation: pulse 1.6s ease-in-out infinite; }
.tile h3 {
  margin-top: 16px;
  font-family: "Inter Tight", sans-serif;
  font-weight: 700;
  font-size: clamp(1.2rem, 1.6vw, 1.45rem);
  line-height: 1.15;
  letter-spacing: -0.02em;
  color: #f1eeff;
}
.tile p {
  margin-top: 8px;
  max-width: 46ch;
  font-family: "Inter", system-ui, sans-serif;
  font-size: 14px;
  line-height: 1.55;
  color: rgba(236, 233, 255, 0.6);
}
.tile-viz { margin-top: auto; padding-top: 22px; }

/* =========================================================
   CONTROL (bento)
   ========================================================= */
.control {
  background:
    radial-gradient(ellipse 50% 40% at 88% 8%, rgba(91, 108, 255, 0.12), transparent 70%),
    radial-gradient(ellipse 40% 40% at 0% 92%, rgba(139, 92, 246, 0.12), transparent 70%),
    var(--bg);
}
.control-head {
  display: grid;
  grid-template-columns: 1.2fr 1fr;
  gap: 4vw;
  align-items: end;
  margin-bottom: clamp(40px, 6vh, 72px);
}
.control-head .sec-lede { justify-self: end; }

.bento { display: grid; grid-template-columns: repeat(12, minmax(0, 1fr)); gap: 18px; }
.t-ledger { grid-column: span 7; grid-row: span 2; }
.t-guard, .t-connect { grid-column: span 5; }
.t-audit, .t-close, .t-approve { grid-column: span 4; }

/* live ledger */
.ledger {
  position: relative;
  overflow: hidden;
  border-radius: 14px;
  border: 1px solid rgba(196, 181, 253, 0.12);
  background: rgba(5, 5, 10, 0.55);
  font-family: "JetBrains Mono", monospace;
  font-size: 12.5px;
}
.ledger-row {
  display: grid;
  grid-template-columns: 72px minmax(0, 1fr) 112px 100px;
  gap: 12px;
  align-items: center;
  min-height: 44px;
  padding: 0 16px;
  border-bottom: 1px solid rgba(196, 181, 253, 0.06);
}
.ledger-row .t { color: rgba(236, 233, 255, 0.38); }
.ledger-row .cp { font-family: "Inter", sans-serif; font-size: 13.5px; color: rgba(236, 233, 255, 0.88); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.ledger-row .amt { text-align: right; font-variant-numeric: tabular-nums; color: #ece9ff; }
.ledger-headrow { min-height: 36px; font-size: 10.5px; letter-spacing: 0.16em; text-transform: uppercase; color: rgba(236, 233, 255, 0.4); }
.ledger-headrow .amt { color: inherit; }
.ledger-body { height: 264px; overflow: hidden; }
.t-ledger .tile-viz { flex: 1; display: flex; flex-direction: column; }
.t-ledger .ledger { flex: 1; display: flex; flex-direction: column; }
.t-ledger .ledger-body { flex: 1; height: auto; min-height: 264px; }
.ledger-body .ledger-row:last-child { border-bottom: none; }
.ledger-row.enter { animation: rowIn 0.6s cubic-bezier(0.2, 0.7, 0.2, 1); }
@keyframes rowIn {
  from { opacity: 0; transform: translateY(-14px); background: rgba(139, 92, 246, 0.16); }
  to { background: transparent; }
}
.badge {
  justify-self: start;
  display: inline-flex;
  align-items: center;
  gap: 6px;
  padding: 4px 9px;
  border-radius: 999px;
  border: 1px solid;
  font-size: 10.5px;
  letter-spacing: 0.1em;
  text-transform: uppercase;
}
.b-scan { color: var(--lilac); border-color: rgba(196, 181, 253, 0.35); background: rgba(196, 181, 253, 0.08); }
.b-scan::before { content: ""; width: 5px; height: 5px; border-radius: 50%; background: currentColor; animation: pulse 0.7s infinite; }
.b-ok { color: #86efac; border-color: rgba(134, 239, 172, 0.3); background: rgba(134, 239, 172, 0.06); }
.b-flag { color: #fbbf24; border-color: rgba(251, 191, 36, 0.32); background: rgba(251, 191, 36, 0.06); }
.ledger-beam {
  position: absolute;
  top: 0; bottom: 0;
  left: 2%;
  width: 2px;
  background: linear-gradient(180deg, transparent, #fff 18%, #c4b5fd 82%, transparent);
  box-shadow: 0 0 12px #a78bfa, 0 0 30px rgba(139, 92, 246, 0.6);
  animation: beamX 5s cubic-bezier(0.6, 0, 0.4, 1) infinite alternate;
  pointer-events: none;
}
@keyframes beamX { to { left: 98%; } }
.ledger-foot {
  display: flex;
  flex-wrap: wrap;
  gap: 8px 22px;
  margin-top: 14px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11.5px;
  letter-spacing: 0.06em;
  color: var(--muted);
}
.ledger-foot span:first-child { color: var(--lilac); text-transform: uppercase; letter-spacing: 0.16em; }
.ledger-foot b { color: #ece9ff; font-weight: 500; font-variant-numeric: tabular-nums; }
.ledger-foot .fl b { color: #fbbf24; }

/* guardrails */
.guards { list-style: none; }
.guards li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
  padding: 12px 0;
  border-bottom: 1px solid rgba(196, 181, 253, 0.08);
}
.guards b { display: block; font-family: "Inter", sans-serif; font-size: 14px; font-weight: 500; color: #ece9ff; }
.guards span { display: block; margin-top: 3px; font-family: "JetBrains Mono", monospace; font-size: 11.5px; color: var(--muted); }
.switch {
  position: relative;
  flex-shrink: 0;
  width: 42px;
  height: 24px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.25);
  background: rgba(255, 255, 255, 0.06);
  cursor: pointer;
  transition: background 0.3s, border-color 0.3s, box-shadow 0.3s;
}
.switch::after {
  content: "";
  position: absolute;
  top: 3px; left: 3px;
  width: 16px; height: 16px;
  border-radius: 50%;
  background: #a1a1b5;
  transition: transform 0.3s cubic-bezier(0.2, 0.7, 0.2, 1), background 0.3s;
}
.switch[aria-checked="true"] {
  background: linear-gradient(90deg, #6d28d9, #a78bfa);
  border-color: transparent;
  box-shadow: 0 0 16px rgba(139, 92, 246, 0.5);
}
.switch[aria-checked="true"]::after { transform: translateX(18px); background: #fff; }
.switch:focus-visible { outline: 2px solid var(--lilac); outline-offset: 3px; }
.autonomy {
  display: grid;
  grid-template-columns: auto 1fr auto;
  align-items: center;
  gap: 14px;
  margin-top: 16px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.14em;
  text-transform: uppercase;
  color: var(--muted);
}
.meter { height: 6px; border-radius: 99px; background: rgba(255, 255, 255, 0.06); overflow: hidden; }
.meter i {
  display: block;
  height: 100%;
  border-radius: inherit;
  background: linear-gradient(90deg, #5b6cff, #c4b5fd, #f1dba7);
  box-shadow: 0 0 12px rgba(139, 92, 246, 0.6);
  transition: width 0.6s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.autonomy em { font-style: normal; color: #ece9ff; }

/* connectors orbit */
.orbit { position: relative; height: 210px; }
.orbit-svg { position: absolute; inset: 0; width: 100%; height: 100%; overflow: visible; }
.orbit-core {
  position: absolute;
  left: 50%; top: 50%;
  transform: translate(-50%, -50%);
  z-index: 2;
  width: 72px; height: 72px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: radial-gradient(circle at 35% 30%, #d8ccff, #6d28d9 60%, #2e1065);
  box-shadow: 0 0 44px rgba(139, 92, 246, 0.6), inset 0 0 18px rgba(255, 255, 255, 0.25);
  font-family: "Inter Tight", sans-serif;
  font-weight: 900;
  font-size: 12px;
  letter-spacing: 0.14em;
  color: #fff;
}
.orbit-core::after {
  content: "";
  position: absolute;
  inset: -8px;
  border-radius: 50%;
  border: 1px solid rgba(196, 181, 253, 0.5);
  animation: ripple 2.6s ease-out infinite;
}
@keyframes ripple { from { transform: scale(0.9); opacity: 1; } to { transform: scale(1.7); opacity: 0; } }
.node {
  position: absolute;
  left: 0; top: 0;
  padding: 6px 11px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.28);
  background: rgba(14, 12, 28, 0.92);
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.08em;
  color: #ece9ff;
  white-space: nowrap;
  will-change: transform;
}

/* audit trail */
.audit { list-style: none; }
.audit li {
  display: grid;
  grid-template-columns: 14px 1fr auto;
  gap: 3px 10px;
  padding: 11px 0;
  border-bottom: 1px solid rgba(196, 181, 253, 0.07);
  animation: auditIn 0.5s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.audit li:last-child { border-bottom: none; }
@keyframes auditIn { from { opacity: 0; transform: translateY(-8px); } }
.audit li::before {
  content: "";
  grid-row: 1 / span 3;
  width: 7px; height: 7px;
  margin-top: 5px;
  border-radius: 50%;
  background: var(--lilac);
  box-shadow: 0 0 10px rgba(139, 92, 246, 0.8);
}
.audit li.h::before { background: var(--cream); box-shadow: 0 0 10px rgba(227, 133, 122, 0.8); }
.audit .who { font-family: "JetBrains Mono", monospace; font-size: 11.5px; color: var(--lilac); }
.audit li.h .who { color: var(--cream); }
.audit time { font-family: "JetBrains Mono", monospace; font-size: 11px; color: rgba(236, 233, 255, 0.4); }
.audit .what { grid-column: 2 / 4; font-family: "Inter", sans-serif; font-size: 13px; line-height: 1.4; color: rgba(236, 233, 255, 0.85); }
.audit .hash { grid-column: 2 / 4; font-family: "JetBrains Mono", monospace; font-size: 10.5px; color: rgba(236, 233, 255, 0.32); }

/* month-end */
.close-big { display: block; margin-top: 18px; font-size: clamp(3.2rem, 5vw, 4.6rem); line-height: 0.9; letter-spacing: -0.045em; }
.bars { display: grid; gap: 12px; }
.bar {
  display: grid;
  grid-template-columns: 78px 1fr auto;
  align-items: center;
  gap: 10px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.06em;
  color: var(--muted);
}
.bar i { position: relative; height: 8px; border-radius: 99px; background: rgba(255, 255, 255, 0.06); overflow: hidden; }
.bar i::after {
  content: "";
  position: absolute;
  inset: 0;
  width: 0;
  border-radius: inherit;
  background: rgba(236, 233, 255, 0.28);
  transition: width 1.4s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.bar.now i::after { background: linear-gradient(90deg, #e3857a, #f1dba7); box-shadow: 0 0 12px rgba(227, 133, 122, 0.6); transition-delay: 0.3s; }
.t-close.in .bar i::after { width: var(--w); }
.bar em { font-style: normal; color: #ece9ff; }

/* approvals */
.approval {
  padding: 16px;
  border-radius: 14px;
  border: 1px solid rgba(196, 181, 253, 0.14);
  background: rgba(5, 4, 10, 0.6);
}
.ap-head { display: flex; align-items: center; gap: 10px; }
.ap-avatar {
  width: 30px; height: 30px;
  flex-shrink: 0;
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: radial-gradient(circle at 35% 30%, #e9e3ff, #8b5cf6 70%);
  font-family: "Inter Tight", sans-serif;
  font-weight: 900;
  font-size: 12px;
  color: #160f2b;
}
.ap-head b { display: block; font-family: "Inter", sans-serif; font-size: 13.5px; font-weight: 600; color: #ece9ff; }
.ap-head span { font-family: "JetBrains Mono", monospace; font-size: 10.5px; color: var(--muted); }
.tile .ap-msg { margin: 12px 0 14px; max-width: none; font-size: 13.5px; line-height: 1.5; color: rgba(236, 233, 255, 0.8); }
.tile .ap-msg b { color: #fff; font-weight: 600; }
.ap-actions { display: flex; gap: 10px; }
.ap-btn {
  flex: 1;
  height: 40px;
  border-radius: 10px;
  font-family: "JetBrains Mono", monospace;
  font-size: 12px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  cursor: pointer;
  transition: box-shadow 0.25s, background 0.25s, border-color 0.25s;
}
.ap-btn.ok { border: none; background: #ece9ff; color: #0b0a14; }
.ap-btn.ok:hover { box-shadow: 0 8px 26px rgba(196, 181, 253, 0.35); }
.ap-btn.hold { border: 1px solid rgba(196, 181, 253, 0.25); background: transparent; color: #ece9ff; }
.ap-btn.hold:hover { border-color: var(--lilac); background: rgba(196, 181, 253, 0.08); }
.ap-btn:focus-visible { outline: 2px solid var(--lilac); outline-offset: 2px; }
.ap-result {
  padding: 11px 12px;
  border-radius: 10px;
  border: 1px solid rgba(134, 239, 172, 0.22);
  background: rgba(134, 239, 172, 0.06);
  font-family: "JetBrains Mono", monospace;
  font-size: 12px;
  color: #86efac;
  animation: auditIn 0.4s ease;
}
.ap-result.held { color: #fbbf24; border-color: rgba(251, 191, 36, 0.25); background: rgba(251, 191, 36, 0.06); }

/* =========================================================
   FAQ
   ========================================================= */
.faq {
  background:
    linear-gradient(rgba(196, 181, 253, 0.03) 1px, transparent 1px) 0 0 / 100% 64px,
    linear-gradient(90deg, rgba(196, 181, 253, 0.03) 1px, transparent 1px) 0 0 / 64px 100%,
    radial-gradient(ellipse 45% 40% at 15% 20%, rgba(139, 92, 246, 0.12), transparent 70%),
    var(--bg-2);
}
.faq-grid { display: grid; grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.3fr); gap: 6vw; align-items: start; }
.faq-head { position: sticky; top: 96px; }
.faq-head .sec-lede { margin-top: 24px; }
.faq-contact { margin-top: 36px; max-width: 420px; }
.faq-contact .tile-in { padding: 22px 24px; }
.faq-contact p { margin: 12px 0 18px; }

.faq-list { border-bottom: 1px solid rgba(196, 181, 253, 0.12); }
.faq-item { position: relative; border-top: 1px solid rgba(196, 181, 253, 0.12); transition: background 0.4s; }
.faq-item::before {
  content: "";
  position: absolute;
  left: 0; top: -1px; bottom: -1px;
  width: 2px;
  background: linear-gradient(180deg, transparent, #fff 20%, #c4b5fd 80%, transparent);
  box-shadow: 0 0 12px #a78bfa;
  transform: scaleY(0);
  transition: transform 0.5s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.faq-item[open] { background: linear-gradient(90deg, rgba(139, 92, 246, 0.09), transparent 65%); }
.faq-item[open]::before { transform: scaleY(1); }
.faq-item summary {
  display: grid;
  grid-template-columns: 44px 1fr 30px;
  gap: 16px;
  align-items: center;
  padding: 26px 8px 26px 20px;
  list-style: none;
  cursor: pointer;
}
.faq-item summary::-webkit-details-marker { display: none; }
.faq-item summary:focus-visible { outline: 2px solid var(--lilac); outline-offset: -2px; border-radius: 6px; }
.q-num { font-family: "JetBrains Mono", monospace; font-size: 12px; color: rgba(196, 181, 253, 0.6); }
.q {
  font-family: "Inter Tight", sans-serif;
  font-weight: 600;
  font-size: clamp(1.05rem, 1.45vw, 1.32rem);
  line-height: 1.3;
  letter-spacing: -0.015em;
  color: rgba(236, 233, 255, 0.86);
  transition: color 0.3s;
}
.faq-item summary:hover .q, .faq-item[open] .q { color: #fff; }
.q-icon {
  position: relative;
  width: 30px; height: 30px;
  border-radius: 50%;
  border: 1px solid rgba(196, 181, 253, 0.25);
  transition: border-color 0.3s, background 0.3s;
}
.q-icon::before, .q-icon::after {
  content: "";
  position: absolute;
  left: 50%; top: 50%;
  width: 11px; height: 1.5px;
  background: #ece9ff;
  transform: translate(-50%, -50%);
  transition: transform 0.4s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.q-icon::after { transform: translate(-50%, -50%) rotate(90deg); }
.faq-item[open] .q-icon { border-color: var(--lilac); background: rgba(196, 181, 253, 0.12); }
.faq-item[open] .q-icon::after { transform: translate(-50%, -50%) rotate(90deg) scaleX(0); }
.faq-item summary:hover .q-icon { border-color: var(--lilac); }
.faq-a { overflow: hidden; }
.faq-a p {
  max-width: 64ch;
  padding: 0 54px 28px 80px;
  font-family: "Inter", system-ui, sans-serif;
  font-size: 15.5px;
  line-height: 1.65;
  color: rgba(236, 233, 255, 0.66);
}

/* =========================================================
   CTA PANEL (premium)
   ========================================================= */
.cta-panel {
  max-width: 600px;
  padding: 44px 44px 36px;
  border: none;
  background:
    radial-gradient(120% 80% at 100% 0%, rgba(139, 92, 246, 0.16), transparent 50%),
    radial-gradient(90% 70% at 0% 100%, rgba(227, 133, 122, 0.1), transparent 60%),
    linear-gradient(180deg, #110f1e, #08070d);
  box-shadow: 0 50px 140px rgba(0, 0, 0, 0.65), 0 0 0 1px rgba(0, 0, 0, 0.4);
}
.cta-panel::after {
  content: "";
  position: absolute;
  top: 0; left: 12%; right: 12%;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.75), transparent);
  z-index: 3;
  pointer-events: none;
}
.hud { position: absolute; width: 14px; height: 14px; border: 0 solid rgba(196, 181, 253, 0.55); z-index: 3; pointer-events: none; }
.hud.tl { top: 14px; left: 14px; border-width: 1px 0 0 1px; }
.hud.tr { top: 14px; right: 14px; border-width: 1px 1px 0 0; }
.hud.bl { bottom: 14px; left: 14px; border-width: 0 0 1px 1px; }
.hud.br { bottom: 14px; right: 14px; border-width: 0 1px 1px 0; }

.cta-top { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 12px; margin-bottom: 26px; }
.chip-status {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 6px 12px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.22);
  background: rgba(196, 181, 253, 0.06);
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #ece9ff;
  transition: border-color 0.3s;
}
.chip-status em { font-style: normal; }
.chip-status i { width: 7px; height: 7px; border-radius: 50%; background: #4ade80; box-shadow: 0 0 10px #4ade80; animation: pulse 1.6s infinite; }
.chip-status.running i { background: #c4b5fd; box-shadow: 0 0 10px #8b5cf6; animation-duration: 0.6s; }
.chip-status.live { border-color: rgba(134, 239, 172, 0.4); }
.chip-status.live i { animation: none; }

.cta-row { display: flex; align-items: center; flex-wrap: wrap; gap: 22px 30px; margin: 36px 0 18px; }
.cta-row .cta-wrap { margin: 0; }
.cta-points {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  gap: 8px 20px;
  margin-bottom: 26px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11.5px;
  letter-spacing: 0.04em;
  color: rgba(236, 233, 255, 0.55);
}
.cta-points li { display: inline-flex; align-items: center; gap: 8px; }
.cta-points li::before { content: "✓"; color: #86efac; }

.console {
  position: relative;
  overflow: hidden;
  border-radius: 14px;
  border: 1px solid rgba(196, 181, 253, 0.14);
  background: rgba(5, 4, 10, 0.78);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.03);
}
.console-bar {
  display: flex;
  align-items: center;
  gap: 12px;
  padding: 10px 14px;
  border-bottom: 1px solid rgba(196, 181, 253, 0.08);
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.08em;
  color: var(--muted);
}
.win-dots { display: flex; gap: 6px; }
.win-dots i { width: 8px; height: 8px; border-radius: 50%; background: rgba(236, 233, 255, 0.14); }
.console-time { margin-left: auto; font-variant-numeric: tabular-nums; color: var(--lilac); }
.console-progress { height: 2px; background: rgba(196, 181, 253, 0.08); }
.console-progress i {
  display: block;
  width: 0;
  height: 100%;
  background: linear-gradient(90deg, #8b5cf6, #c4b5fd, #f1dba7);
  box-shadow: 0 0 10px #8b5cf6;
  transition: width 0.5s cubic-bezier(0.2, 0.7, 0.2, 1);
}
.console .agent-log { border-top: none; padding: 14px 16px 16px; min-height: 204px; }
.log-line .ts { flex-shrink: 0; width: 3.4em; color: rgba(236, 233, 255, 0.3); font-variant-numeric: tabular-nums; }
.log-line.plan { color: rgba(236, 233, 255, 0.32); }
.log-line .tx { flex: 1 1 0; min-width: 0; }

.cta-panel .trust { gap: 8px; margin-top: 22px; color: rgba(236, 233, 255, 0.6); }
.cta-panel .trust span {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 7px 11px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.14);
  background: rgba(255, 255, 255, 0.02);
}
.cta-panel .trust svg { width: 12px; height: 12px; color: var(--lilac); }

/* responsive */
@media (max-width: 1100px) {
  .t-ledger { grid-column: span 12; grid-row: auto; }
  .t-guard, .t-connect, .t-audit, .t-approve { grid-column: span 6; }
  .t-close { grid-column: span 12; }
}
@media (max-width: 900px) {
  .control-head { grid-template-columns: 1fr; }
  .control-head .sec-lede { justify-self: start; }
  .faq-grid { grid-template-columns: 1fr; gap: 48px; }
  .faq-head { position: static; }
}
@media (max-width: 720px) {
  .bento > * { grid-column: span 12 !important; }
  .tile-in { padding: 22px 18px 20px; }
  .ledger-row { grid-template-columns: minmax(0, 1fr) auto auto; gap: 10px; padding: 0 12px; }
  .ledger-row .cp { font-size: 13px; }
  .badge { padding: 3px 7px; font-size: 9.5px; letter-spacing: 0.08em; }
  .console .log-line { flex-wrap: wrap; column-gap: 10px; line-height: 1.45; padding: 5px 0; }
  .console .log-line .st,
  .console .log-line.final a { flex-basis: 100%; margin-left: 0; padding-left: calc(3.4em + 22px); white-space: normal; font-size: 11.5px; }
  .ledger-row .t { display: none; }
  .ledger { font-size: 12px; }
  .faq-item summary { grid-template-columns: 28px 1fr 28px; gap: 10px; padding: 22px 4px 22px 12px; }
  .faq-a p { padding: 0 8px 24px 50px; font-size: 15px; }
  .cta-panel { padding: 34px 20px 26px; }
  .cta-row { gap: 18px; }
}

/* =========================================================
   SUPER FOOTER (call to action + footer)
   ========================================================= */
.super-footer {
  position: relative;
  padding: clamp(96px, 14vh, 150px) 6vw 0;
  overflow: hidden;
  background:
    radial-gradient(ellipse 55% 40% at 50% 0%, rgba(139, 92, 246, 0.16), transparent 70%),
    radial-gradient(ellipse 40% 35% at 85% 40%, rgba(227, 133, 122, 0.1), transparent 70%),
    radial-gradient(ellipse 60% 30% at 50% 100%, rgba(91, 108, 255, 0.12), transparent 70%),
    linear-gradient(180deg, #07060d, #040307);
}
/* horizon line, echoing the hero's water line */
.super-footer::before {
  content: "";
  position: absolute;
  top: 0; left: 50%;
  width: 70vw;
  height: 1px;
  transform: translateX(-50%);
  background: linear-gradient(90deg, transparent, rgba(196, 181, 253, 0.7), #fff, rgba(196, 181, 253, 0.7), transparent);
  box-shadow: 0 0 24px rgba(167, 139, 250, 0.8);
}

.sf-stage {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  display: grid;
  grid-template-columns: minmax(0, 1.05fr) minmax(0, 1fr);
  gap: clamp(32px, 4vw, 64px);
  align-items: center;
  padding: clamp(36px, 4.6vw, 68px);
  border-radius: 28px;
  background:
    radial-gradient(120% 90% at 0% 0%, rgba(139, 92, 246, 0.16), transparent 50%),
    radial-gradient(90% 80% at 100% 100%, rgba(227, 133, 122, 0.12), transparent 60%),
    linear-gradient(180deg, #110f1e, #08070d);
  box-shadow: 0 60px 160px rgba(0, 0, 0, 0.7);
}
.sf-stage::before {
  content: "";
  position: absolute;
  inset: 0;
  padding: 1px;
  border-radius: inherit;
  background: linear-gradient(140deg, rgba(196, 181, 253, 0.6), rgba(196, 181, 253, 0.06) 32%, rgba(196, 181, 253, 0.04) 68%, rgba(241, 219, 167, 0.45));
  -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  pointer-events: none;
  z-index: 3;
}
.sf-stage::after {
  content: "";
  position: absolute;
  top: 0; left: 10%; right: 10%;
  height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.8), transparent);
  z-index: 3;
  pointer-events: none;
}
.sf-stage .hud.tl { top: 18px; left: 18px; }
.sf-stage .hud.tr { top: 18px; right: 18px; }
.sf-stage .hud.bl { bottom: 18px; left: 18px; }
.sf-stage .hud.br { bottom: 18px; right: 18px; }

.sf-pitch, .sf-demo { position: relative; z-index: 1; }
.sf-pitch h2.headline { font-size: clamp(2.5rem, 5vw, 5.2rem); line-height: 0.94; letter-spacing: -0.035em; }
.sf-pitch h2 em { font-style: normal; }
.sf-lede {
  margin-top: 22px;
  max-width: 520px;
  font-family: "Inter", system-ui, sans-serif;
  font-size: clamp(15px, 1.15vw, 17.5px);
  line-height: 1.6;
  color: rgba(236, 233, 255, 0.68);
}
.sf-stage .trust { gap: 8px; margin-top: 4px; color: rgba(236, 233, 255, 0.6); }
.sf-stage .trust span {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 7px 11px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.14);
  background: rgba(255, 255, 255, 0.02);
}
.sf-stage .trust svg { width: 12px; height: 12px; color: var(--lilac); }

.sf-demo-label {
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--muted);
}
.sf-demo .console .agent-log { min-height: 232px; }
.sf-metrics { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 10px; margin-top: 12px; }
.sf-metrics div {
  padding: 13px 14px;
  border-radius: 12px;
  border: 1px solid rgba(196, 181, 253, 0.12);
  background: rgba(5, 4, 10, 0.55);
}
.sf-metrics span {
  display: block;
  font-family: "JetBrains Mono", monospace;
  font-size: 10.5px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--muted);
}
.sf-metrics b {
  display: block;
  margin-top: 6px;
  font-family: "Inter Tight", sans-serif;
  font-weight: 800;
  font-size: 1.45rem;
  letter-spacing: -0.02em;
  color: rgba(236, 233, 255, 0.35);
}
.sf-metrics b.pop { color: #fff; text-shadow: 0 0 18px rgba(139, 92, 246, 0.7); animation: pop 0.5s cubic-bezier(0.2, 0.7, 0.2, 1); }
@keyframes pop { from { opacity: 0; transform: translateY(6px) scale(0.96); } }

/* footer body */
.sf-main {
  position: relative;
  z-index: 2;
  display: grid;
  grid-template-columns: minmax(0, 1.1fr) minmax(0, 2fr);
  gap: 6vw;
  padding: clamp(72px, 10vh, 110px) 0 clamp(40px, 6vh, 70px);
}
.sf-brand .brand { font-size: 18px; }
.sf-brand > p {
  max-width: 360px;
  margin: 18px 0 22px;
  font-family: "Inter", system-ui, sans-serif;
  font-size: 15px;
  line-height: 1.6;
  color: rgba(236, 233, 255, 0.6);
}
.sf-status {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 7px 12px;
  border-radius: 999px;
  border: 1px solid rgba(134, 239, 172, 0.25);
  background: rgba(134, 239, 172, 0.05);
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #86efac;
  text-decoration: none;
}
.sf-status i { width: 6px; height: 6px; border-radius: 50%; background: #4ade80; box-shadow: 0 0 8px #4ade80; animation: pulse 1.6s ease-in-out infinite; }

.sf-news { margin-top: 32px; max-width: 390px; }
.sf-news label {
  display: block;
  margin-bottom: 10px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--muted);
}
.sf-field {
  display: flex;
  align-items: center;
  padding: 5px 5px 5px 18px;
  border-radius: 999px;
  border: 1px solid rgba(196, 181, 253, 0.22);
  background: rgba(255, 255, 255, 0.03);
  transition: border-color 0.3s, box-shadow 0.3s;
}
.sf-field:focus-within { border-color: var(--lilac); box-shadow: 0 0 0 4px rgba(196, 181, 253, 0.1), 0 0 24px rgba(139, 92, 246, 0.25); }
.sf-field input {
  flex: 1;
  min-width: 0;
  height: 40px;
  border: none;
  outline: none;
  background: none;
  font-family: "Inter", system-ui, sans-serif;
  font-size: 15px;
  color: #fff;
}
.sf-field input::placeholder { color: rgba(236, 233, 255, 0.38); }
.sf-field button {
  width: 40px; height: 40px;
  flex-shrink: 0;
  display: grid;
  place-items: center;
  border: none;
  border-radius: 50%;
  background: #ece9ff;
  color: #0b0a14;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}
.sf-field button:hover { transform: translateX(2px); box-shadow: 0 6px 22px rgba(196, 181, 253, 0.4); }
.sf-field button:focus-visible { outline: 2px solid var(--lilac); outline-offset: 2px; }
.sf-field button svg { width: 16px; height: 16px; }
.sf-news-note { margin-top: 10px; font-family: "JetBrains Mono", monospace; font-size: 11px; letter-spacing: 0.04em; color: var(--muted); }
.sf-news-note.ok { color: #86efac; }
.sf-news-note.err { color: #fbbf24; }

.sf-cols { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 32px; }
.sf-cols h4 {
  margin-bottom: 18px;
  font-family: "JetBrains Mono", monospace;
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--lilac);
}
.sf-cols ul { list-style: none; display: grid; gap: 12px; }
.sf-cols a {
  font-family: "Inter", system-ui, sans-serif;
  font-size: 15px;
  color: rgba(236, 233, 255, 0.62);
  text-decoration: none;
  transition: color 0.25s;
}
.sf-cols a:hover { color: #fff; }
.sf-cols a:focus-visible, .sf-bottom a:focus-visible { outline: 2px solid var(--lilac); outline-offset: 3px; border-radius: 3px; }

/* giant wordmark: solid on one side of the scanner, wireframe on the other */
.sf-mark {
  --split: 50%;
  position: relative;
  height: 0.74em;
  margin-top: clamp(8px, 2vh, 24px);
  overflow: hidden;
  font-size: 29vw;
  user-select: none;
  pointer-events: none;
  animation: markSplit 7s ease-in-out infinite alternate;
  -webkit-mask-image: linear-gradient(180deg, #000 0%, rgba(0,0,0,0.99) 30%, rgba(0,0,0,0.95) 42%, rgba(0,0,0,0.86) 54%, rgba(0,0,0,0.7) 66%, rgba(0,0,0,0.48) 78%, rgba(0,0,0,0.22) 90%, transparent 100%);
  mask-image: linear-gradient(180deg, #000 0%, rgba(0,0,0,0.99) 30%, rgba(0,0,0,0.95) 42%, rgba(0,0,0,0.86) 54%, rgba(0,0,0,0.7) 66%, rgba(0,0,0,0.48) 78%, rgba(0,0,0,0.22) 90%, transparent 100%);
}
@keyframes markSplit { from { --split: 6%; } to { --split: 94%; } }
.sf-mark .mark {
  display: block;
  width: 100%;
  margin: -0.12em 0 -0.3em;
  padding: 0.12em 0.04em 0.3em; /* gradient paint area covers the full glyphs */
  text-align: center;
  font-family: "Inter Tight", sans-serif;
  font-weight: 900;
  font-size: 1em;
  line-height: 0.82;
  letter-spacing: -0.06em;
}
.sf-mark .mark-solid { clip-path: inset(0 0 0 var(--split)); filter: none; }
.sf-mark .mark-wire {
  position: absolute;
  top: 0; left: 0;
  color: transparent;
  -webkit-text-fill-color: transparent;
  -webkit-text-stroke: 1.5px rgba(196, 181, 253, 0.55);
  background: repeating-linear-gradient(180deg, rgba(196, 181, 253, 0.3) 0 1px, transparent 1px 6px);
  -webkit-background-clip: text;
  background-clip: text;
  clip-path: inset(0 calc(100% - var(--split)) 0 0);
}
.mark-scan {
  position: absolute;
  top: 0; bottom: 0;
  left: var(--split);
  width: 2px;
  transform: translateX(-50%);
  background: linear-gradient(180deg, #fff, #c4b5fd 55%, transparent);
  box-shadow: 0 0 16px #a78bfa, 0 0 42px rgba(139, 92, 246, 0.7);
}

.sf-bottom {
  position: relative;
  z-index: 2;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px 24px;
  padding: 22px 0 30px;
  border-top: 1px solid rgba(196, 181, 253, 0.1);
  font-family: "JetBrains Mono", monospace;
  font-size: 11.5px;
  letter-spacing: 0.06em;
  color: var(--muted);
}
.sf-bottom a { color: var(--cream); text-decoration: none; transition: color 0.25s; }
.sf-bottom a:hover { color: #fff; }
.sf-legal { display: flex; gap: 22px; }
.sf-legal a { color: var(--muted); }

@media (prefers-reduced-motion: reduce) {
  .sf-mark { animation: none; }
  .rise, .scene-inner, .hcard-copper, .hcard-graphite, .ring-run, .tw, .beam, .ascii-content,
  .static-card .card-wrapper, .eyebrow i, .live i, .orbit-core::after, .ledger-beam, .sf-status i,
  .chip-status i, .panel-check li.active i { animation: none !important; }
  .sweep.go, .scan-effect { animation: none; opacity: 0; }
}
@media (max-width: 1024px) {
  .sf-stage { grid-template-columns: 1fr; }
  .sf-main { grid-template-columns: 1fr; gap: 52px; }
}
@media (max-width: 640px) {
  .sf-stage { padding: 34px 18px 26px; border-radius: 22px; }
  .sf-stage .hud.tl, .sf-stage .hud.tr { top: 10px; }
  .sf-stage .hud.bl, .sf-stage .hud.br { bottom: 8px; }
  .sf-stage .hud.tl, .sf-stage .hud.bl { left: 10px; }
  .sf-stage .hud.tr, .sf-stage .hud.br { right: 10px; }
  .sf-cols { grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 34px 20px; }
  .sf-metrics { gap: 8px; }
  .sf-metrics div { padding: 11px 10px; }
  .sf-metrics span { font-size: 9px; letter-spacing: 0.08em; }
  .sf-metrics b { font-size: 1.15rem; }
  .sf-mark { font-size: 33vw; }
  .sf-bottom { flex-direction: column; align-items: flex-start; }
}
</style>
</head>
<body>

<!-- SVG filters for the CTA glow -->
<svg style="position: absolute; width: 0; height: 0;" aria-hidden="true">
  <filter width="300%" x="-100%" height="300%" y="-100%" id="unopaq">
    <feColorMatrix values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 9 0"></feColorMatrix>
  </filter>
  <filter width="300%" x="-100%" height="300%" y="-100%" id="unopaq2">
    <feColorMatrix values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 3 0"></feColorMatrix>
  </filter>
  <filter width="300%" x="-100%" height="300%" y="-100%" id="unopaq3">
    <feColorMatrix values="1 0 0 0.2 0  0 1 0 0.2 0  0 0 1 0.2 0  0 0 0 2 0"></feColorMatrix>
  </filter>
</svg>

<main>
<section class="hero" id="hero" data-section="hero">
  <div class="hero-bg" aria-hidden="true">
    <canvas id="heroParticles" class="hero-particles"></canvas>
    <div class="hero-grid"></div>
    <svg class="rocks" viewBox="0 0 1600 240" preserveAspectRatio="none">
      <defs>
        <linearGradient id="rockA" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0" stop-color="#231c3d"/><stop offset="0.5" stop-color="#110d1f"/><stop offset="1" stop-color="#07060b"/>
        </linearGradient>
        <linearGradient id="rockB" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0" stop-color="#171230"/><stop offset="1" stop-color="#06050a"/>
        </linearGradient>
      </defs>
      <path fill="url(#rockB)" d="M0 240 L0 150 C 120 140 220 170 330 160 C 450 150 520 175 640 168 C 760 160 860 182 980 176 C 1100 170 1180 188 1300 182 C 1420 176 1500 190 1600 186 L1600 240 Z"/>
      <path fill="url(#rockA)" d="M0 240 L0 20 C 30 10 60 30 85 60 C 110 90 120 120 150 140 C 175 158 205 168 240 176 C 300 190 360 184 420 196 C 470 206 520 200 560 210 L560 240 Z"/>
      <path fill="url(#rockA)" opacity="0.9" d="M1180 240 C 1220 214 1260 200 1310 205 C 1360 210 1380 196 1420 200 C 1480 206 1540 214 1600 210 L1600 240 Z"/>
    </svg>
    <div class="water"></div>
  </div>

  <nav class="nav" aria-label="Primary" data-section="nav">
    <a href="#hero" class="brand"><i></i>NOVA</a>
    <div class="nav-links">
      <a href="#sectionPin">Agents</a>
      <a href="#control">Control</a>
      <a href="#faq">FAQ</a>
      <a href="#cta">Pricing</a>
    </div>
    <a href="#cta" class="nav-cta">Get access</a>
  </nav>

  <div class="hero-main">
    <div class="hero-copy" data-scroll-speed="1">
      <div class="eyebrow rise" style="--d: .1s"><i></i>Agents online · v2.4</div>
      <h1 class="headline grad g-lilac rise" style="--d: .2s"><span>Autonomous</span> <span class="grad g-indigo">Finance</span> <span>Agents</span></h1>
      <p class="hero-lede rise" style="--d: .35s">NOVA reads every transaction, <strong>tokenizes every card</strong> and acts on your behalf: reconciling, flagging fraud and closing the books in real time.</p>
      <div class="hero-actions rise" style="--d: .5s">
        <a href="#cta" class="btn btn-primary">Get access
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
        </a>
        <a href="#sectionPin" class="btn btn-ghost">
          <span class="play"><svg viewBox="0 0 10 10" aria-hidden="true"><path d="M1 0.5 L9 5 L1 9.5 Z" fill="currentColor"/></svg></span>Watch demo
        </a>
      </div>
    </div>

    <div class="hero-scene" id="heroScene" aria-hidden="true">
      <div class="scene-inner" id="sceneInner">
        <svg class="ring" viewBox="0 0 880 640">
          <defs>
            <linearGradient id="ringGrad" x1="0" y1="0" x2="1" y2="0">
              <stop offset="0" stop-color="#5b6cff" stop-opacity="0.95"/>
              <stop offset="0.45" stop-color="#c4b5fd" stop-opacity="0.9"/>
              <stop offset="0.7" stop-color="#8b5cf6" stop-opacity="0.45"/>
              <stop offset="1" stop-color="#a78bfa" stop-opacity="0.95"/>
            </linearGradient>
            <filter id="ringGlow" x="-20%" y="-60%" width="140%" height="220%"><feGaussianBlur stdDeviation="6"/></filter>
            <filter id="nodeGlow" x="-200%" y="-200%" width="500%" height="500%"><feGaussianBlur stdDeviation="9"/></filter>
          </defs>
          <g transform="rotate(-13 450 360)">
            <g id="ringDust"></g>
            <ellipse cx="450" cy="360" rx="400" ry="120" fill="none" stroke="url(#ringGrad)" stroke-width="7" filter="url(#ringGlow)" opacity="0.7"/>
            <ellipse cx="450" cy="360" rx="400" ry="120" fill="none" stroke="url(#ringGrad)" stroke-width="1.6"/>
            <ellipse cx="450" cy="360" rx="372" ry="102" fill="none" stroke="rgba(196,181,253,0.2)" stroke-width="1" stroke-dasharray="2 7"/>
            <ellipse class="ring-run" cx="450" cy="360" rx="400" ry="120" fill="none" stroke="#fff" stroke-width="2.2" stroke-linecap="round" pathLength="1000" stroke-dasharray="70 930"/>
            <path id="orbitPath" d="M 50 360 A 400 120 0 1 0 850 360 A 400 120 0 1 0 50 360" fill="none"/>
            <circle r="3" fill="#fff"><animateMotion dur="9s" repeatCount="indefinite"><mpath href="#orbitPath"/></animateMotion></circle>
            <circle r="2.2" fill="#c4b5fd"><animateMotion dur="9s" begin="-3s" repeatCount="indefinite"><mpath href="#orbitPath"/></animateMotion></circle>
            <circle r="2.6" fill="#a5b4fc"><animateMotion dur="9s" begin="-6s" repeatCount="indefinite"><mpath href="#orbitPath"/></animateMotion></circle>
            <circle cx="52" cy="360" r="14" fill="#6d7dff" filter="url(#nodeGlow)"/>
            <circle cx="52" cy="360" r="3.5" fill="#fff"/>
            <circle cx="846" cy="345" r="10" fill="#a78bfa" filter="url(#nodeGlow)"/>
            <circle cx="846" cy="345" r="2.5" fill="#fff"/>
          </g>
        </svg>

        <div class="glass panel-ghost"><pre id="ghostCode"></pre></div>
        <div class="glass panel-json"><pre id="txnJson"></pre></div>
        <div class="glass panel-code"><pre id="miniCode"></pre></div>

        <div class="hcard hcard-copper">
          <div class="card-wrapper">
            <div class="card card-normal theme-copper">
              <div class="card-face">
                <div class="card-top"><div class="card-chip"></div><div class="contactless"></div><div class="card-logo">NOVA</div></div>
                <div class="card-number">4447 8533 •••• 2659</div>
                <div class="card-info">
                  <div><small>Card holder</small><div class="card-holder">Kestrel Freight</div></div>
                  <div><small>Expires</small><div class="card-expiry">01/30</div></div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="beam-lines">
          <i style="height:40%"></i><i style="height:75%"></i><i style="height:30%"></i><i style="height:90%"></i>
          <i style="height:55%"></i><i style="height:20%"></i><i style="height:70%"></i><i style="height:45%"></i>
        </div>
        <div class="beam" id="beam"></div>
        <div class="beam-base"></div>

        <div class="hcard hcard-graphite">
          <div class="card-wrapper">
            <div class="card card-normal theme-graphite">
              <div class="card-face">
                <div class="card-top"><div class="card-chip"></div><div class="contactless"></div><div class="card-logo">NOVA</div></div>
                <div class="card-number">4233 9615 •••• 0154</div>
                <div class="card-info">
                  <div><small>Card holder</small><div class="card-holder">Northwind Ops</div></div>
                  <div><small>Expires</small><div class="card-expiry">09/28</div></div>
                </div>
              </div>
              <div class="sweep" id="cardSweep"></div>
            </div>
          </div>
        </div>

        <div class="glass panel-check">
          <ul id="checklist">
            <li><i></i>Transaction read</li>
            <li><i></i>Card tokenized</li>
            <li><i></i>Risk analysis</li>
            <li><i></i>Category assigned</li>
            <li><i></i>Reconciled</li>
            <li><i></i>Books updated</li>
          </ul>
        </div>

        <div class="pipeline" id="pipeline">
          <span>Read</span><em>→</em><span>Tokenize</span><em>→</em><span>Analyze</span><em>→</em><span>Reconcile</span><em>→</em><span>Close</span>
        </div>
        <span class="plus" style="left: 852px; top: 92px">+</span>
        <span class="plus" style="left: 760px; top: 582px">+</span>
      </div>
    </div>
  </div>

  <div class="hero-stats rise" style="--d: .7s">
    <div class="stat"><b>1M+</b><span>Transactions processed</span></div>
    <div class="stat"><b>&lt;200ms</b><span>Agent response time</span></div>
    <div class="stat"><b>99.9%</b><span>Reconciliation accuracy</span></div>
    <div class="stat"><b>24/7</b><span>Autonomous operation</span></div>
  </div>
</section>

<!-- PINNED: scroll drives cards through the scanner -->
<section id="sectionPin" data-section="scanner" aria-label="How the agent works">
  <div class="pin-label"><b>02</b> — How the agent works</div>
  <canvas class="fx-particles" id="pinParticles" aria-hidden="true"></canvas>
  <canvas class="fx-scanner" id="pinScanner" aria-hidden="true"></canvas>

  <div class="pin-wrap">
    <div class="pin-intro">
      <h2 class="headline grad g-indigo">Every payment that crosses the line is tokenized, scored and understood before it settles.</h2>
      <p>Keep scrolling and watch each card pass through NOVA's decision layer.</p>
      <div class="stats">
        <div><b>38 ms</b><span>Median decision</span></div>
        <div><b>99.4%</b><span>Auto-reconciled</span></div>
        <div><b>0</b><span>Raw card numbers stored</span></div>
      </div>
    </div>
    <div class="panel" data-pin-card="0"><div class="caption"><b>01</b>Tokenize<span>Card numbers are swapped for vault tokens at the edge, so your systems never touch raw card data.</span></div></div>
    <div class="panel" data-pin-card="1"><div class="caption"><b>02</b>Score<span>A risk model checks each transaction for velocity, merchant and behavioral anomalies.</span></div></div>
    <div class="panel" data-pin-card="3"><div class="caption"><b>03</b>Act<span>Agents resolve what they can, such as refunds, holds and vendor follow-ups, and send the rest to a person.</span></div></div>
    <div class="panel" data-pin-card="4"><div class="caption"><b>04</b>Close<span>Ledgers reconcile continuously, so month-end becomes a review instead of a scramble.</span></div></div>
  </div>

  <div class="pin-progress"><i id="pinBar"></i></div>
</section>

<!-- CONTROL -->
<section class="sec control" id="control" data-section="control">
  <div class="control-head">
    <div>
      <div class="sec-label"><b>03</b> — Control</div>
      <h2 class="headline grad g-indigo">Every move,<br>governed.</h2>
    </div>
    <p class="sec-lede">NOVA does the work. You decide how far it goes, with policies, approvals and a complete audit trail built in from day one.</p>
  </div>

  <div class="bento">
    <article class="tile t-ledger" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Live ledger</span><span class="live"><i></i>Streaming</span></div>
        <h3>Every transaction, reconciled as it lands.</h3>
        <p>The agent scans each line the moment it posts, matches it to invoices and receipts, and flags whatever doesn't add up.</p>
        <div class="tile-viz">
          <div class="ledger">
            <div class="ledger-row ledger-headrow"><span class="t">Time</span><span>Counterparty</span><span class="amt">Amount</span><span>Status</span></div>
            <div class="ledger-body" id="ledgerBody"></div>
            <div class="ledger-beam" aria-hidden="true"></div>
          </div>
          <div class="ledger-foot"><span>Today</span><span><b id="ledScan">0</b> scanned</span><span><b id="ledOk">0</b> matched</span><span class="fl"><b id="ledFlag">0</b> flagged</span></div>
        </div>
      </div>
    </article>

    <article class="tile t-guard" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Guardrails</span><span>Try them</span></div>
        <h3>You set the limits.</h3>
        <p>Plain-language policies decide what the agent may do alone and what needs a person.</p>
        <div class="tile-viz">
          <ul class="guards" id="guards">
            <li><div><b>Auto-approve payments</b><span>under $5,000 to known vendors</span></div><button type="button" class="switch" role="switch" aria-checked="true" data-policy="auto-approve under $5,000" aria-label="Auto-approve payments under $5,000"></button></li>
            <li><div><b>Escalate new vendors</b><span>first payment, any amount</span></div><button type="button" class="switch" role="switch" aria-checked="true" data-policy="escalate new vendors" aria-label="Escalate new vendors"></button></li>
            <li><div><b>Hold cross-border</b><span>over $25,000</span></div><button type="button" class="switch" role="switch" aria-checked="true" data-policy="hold cross-border over $25,000" aria-label="Hold cross-border payments over $25,000"></button></li>
            <li><div><b>Pause on anomalies</b><span>risk score above 0.82</span></div><button type="button" class="switch" role="switch" aria-checked="false" data-policy="pause on anomalies" aria-label="Pause on anomalies"></button></li>
          </ul>
          <div class="autonomy"><span>Autonomy</span><div class="meter"><i id="autoMeter"></i></div><em id="autoLabel">Supervised</em></div>
        </div>
      </div>
    </article>

    <article class="tile t-connect" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Connectors</span><span>140+ sources</span></div>
        <h3>Plugs into the stack you already run.</h3>
        <p>Banks, ERPs, payroll and billing, connected in minutes with read-only access by default.</p>
        <div class="tile-viz">
          <div class="orbit" id="orbit" aria-hidden="true">
            <svg class="orbit-svg" viewBox="0 0 100 100" preserveAspectRatio="none">
              <defs>
                <linearGradient id="orbitGrad" x1="0" y1="0" x2="1" y2="0">
                  <stop offset="0" stop-color="#5b6cff" stop-opacity="0.9"/>
                  <stop offset="0.5" stop-color="#c4b5fd" stop-opacity="0.35"/>
                  <stop offset="1" stop-color="#a78bfa" stop-opacity="0.9"/>
                </linearGradient>
              </defs>
              <ellipse cx="50" cy="50" rx="40" ry="34" fill="none" stroke="url(#orbitGrad)" stroke-width="1.3" vector-effect="non-scaling-stroke"/>
              <ellipse cx="50" cy="50" rx="28" ry="22" fill="none" stroke="rgba(196,181,253,0.22)" stroke-width="1" stroke-dasharray="2 5" vector-effect="non-scaling-stroke"/>
            </svg>
            <div class="orbit-core">NOVA</div>
            <span class="node">Banks</span><span class="node">ERP</span><span class="node">Payroll</span>
            <span class="node">Billing</span><span class="node">Issuers</span><span class="node">Treasury</span><span class="node">Chat</span>
          </div>
        </div>
      </div>
    </article>

    <article class="tile t-audit" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Audit trail</span><span class="live"><i></i>Signed</span></div>
        <h3>Every action, on the record.</h3>
        <p>Who did it, why, and a tamper-evident hash.</p>
        <div class="tile-viz"><ol class="audit" id="audit"></ol></div>
      </div>
    </article>

    <article class="tile t-close" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Month-end</span><span>Typical team</span></div>
        <b class="close-big headline grad g-ember">2 days</b>
        <p>Continuous reconciliation turns the close into a review instead of a scramble.</p>
        <div class="tile-viz bars">
          <div class="bar"><span>Before</span><i style="--w: 100%"></i><em>12 days</em></div>
          <div class="bar now"><span>With NOVA</span><i style="--w: 17%"></i><em>2 days</em></div>
        </div>
      </div>
    </article>

    <article class="tile t-approve" data-reveal>
      <div class="tile-in">
        <div class="tile-head"><span>Approvals</span><span>Human in the loop</span></div>
        <h3>Approve from anywhere.</h3>
        <div class="tile-viz">
          <div class="approval" aria-live="polite">
            <div class="ap-head"><span class="ap-avatar">N</span><div><b>NOVA agent</b><span>needs your approval · just now</span></div></div>
            <p class="ap-msg" id="apMsg"></p>
            <div class="ap-actions" id="apActions"><button type="button" class="ap-btn ok" id="apOk">Approve</button><button type="button" class="ap-btn hold" id="apHold">Hold</button></div>
            <div class="ap-result" id="apResult" hidden></div>
          </div>
        </div>
      </div>
    </article>
  </div>
</section>

<!-- FAQ -->
<section class="sec faq" id="faq" data-section="faq">
  <div class="faq-grid">
    <div class="faq-head">
      <div class="sec-label"><b>04</b> — FAQ</div>
      <h2 class="headline grad g-lilac">Questions,<br>answered.</h2>
      <p class="sec-lede">What finance and security teams ask before they hand an agent the keys.</p>
      <div class="tile faq-contact" data-reveal>
        <div class="tile-in">
          <div class="tile-head"><span>Talk to a human</span><span class="live"><i></i>Online</span></div>
          <p>Our finance engineers have run month-end at scale. Bring your messiest workflow.</p>
          <a href="#cta" class="link-arrow">Book a call <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"/></svg></a>
        </div>
      </div>
    </div>
    <div class="faq-list" data-reveal>
      <details class="faq-item" open>
        <summary><span class="q-num">01</span><span class="q">What does a NOVA agent actually do?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>It connects to your bank feeds, card programs and accounting system, then works through every transaction: tokenizing card data, scoring risk, categorizing, matching it to invoices and posting to your ledger. Anything it can't resolve within your policies goes to a person, with the context already attached.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">02</span><span class="q">Can the agent move money without approval?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>Only within the limits you set. By default every payment needs a human approval. From there you can allow auto-approval below a threshold, for known vendors or for specific categories, and you can change or pause any policy at any time.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">03</span><span class="q">Does NOVA store raw card numbers?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>No. Card numbers are swapped for vault tokens at the edge, so neither the agents nor your own systems ever handle raw card data. That keeps your compliance scope small.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">04</span><span class="q">Which systems does it connect to?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>Bank feeds, ERPs and accounting tools, card issuers, payroll and billing platforms, and the chat tools your team already uses for approvals. Connections are read-only by default, and write access is granted per action.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">05</span><span class="q">What happens if the agent gets something wrong?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>Every action is logged with its reasoning and can be reversed from the audit trail. Your correction becomes a rule for your workspace, so the same mistake isn't repeated.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">06</span><span class="q">Is our financial data used to train models?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>No. Your data is used only to run your workspace. It is never used to train shared models.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">07</span><span class="q">How long does setup take?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>Most teams connect their first accounts in under an hour, then run the agent in supervised mode through their first close before widening its permissions.</p></div>
      </details>
      <details class="faq-item">
        <summary><span class="q-num">08</span><span class="q">How is pricing structured?</span><span class="q-icon" aria-hidden="true"></span></summary>
        <div class="faq-a"><p>A flat platform fee plus usage based on the number of entities and monthly transaction volume. The sandbox is free, with no card required.</p></div>
      </details>
    </div>
  </div>
</section>

</main>

<!-- SUPER FOOTER: call to action + footer -->
<footer class="super-footer" id="cta" data-section="cta">
  <div class="sf-stage" data-reveal>
    <span class="hud tl"></span><span class="hud tr"></span><span class="hud bl"></span><span class="hud br"></span>

    <div class="sf-pitch">
      <div class="cta-top">
        <span class="sec-label"><b>05</b> — Deploy</span>
        <span class="chip-status" id="ctaStatus"><i></i><em>Sandbox ready</em></span>
      </div>
      <h2 class="headline grad g-lilac">Put your finance ops on <em class="grad g-ember">autopilot.</em></h2>
      <p class="sf-lede">Deploy an agent on a sample workspace and watch it connect, reconcile and flag risk live, before you've written a line of code.</p>

      <div class="cta-row">
        <div class="cta-wrap" id="ctaWrap">
          <button type="button" class="real-button" id="ctaButton" aria-label="Deploy your agent"></button>
          <div class="button-container">
            <div class="spin spin-blur"></div>
            <div class="spin spin-intense"></div>
            <div class="backdrop"></div>
            <div class="button-border">
              <div class="spin spin-inside"></div>
              <div class="button">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                  <path d="M12 2l2.2 6.3L20.5 10l-6.3 2.2L12 18.5l-2.2-6.3L3.5 10l6.3-1.7z"/>
                  <path d="M19 15l.9 2.1L22 18l-2.1.9L19 21l-.9-2.1L16 18l2.1-.9z"/>
                </svg>
                <span id="ctaLabel">Deploy your agent</span>
                <span class="arrow">→</span>
              </div>
            </div>
          </div>
        </div>
        <a href="#faq" class="link-arrow">Talk to sales <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"/></svg></a>
      </div>

      <ul class="cta-points">
        <li>No card required</li><li>Sample data, real workflow</li><li>Runs in ~6 seconds</li>
      </ul>
      <div class="trust">
        <span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3l7 3v6c0 4.5-3 7.5-7 9-4-1.5-7-4.5-7-9V6z"/></svg>SOC 2 Type II</span><span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="6" width="18" height="12" rx="2"/><path d="M3 10h18"/></svg>PCI DSS L1</span><span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="5" y="11" width="14" height="10" rx="2"/><path d="M8 11V8a4 4 0 0 1 8 0v3"/></svg>AES-256 vault</span><span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="8" r="4"/><path d="M4 21c1.5-4 4.5-6 8-6s6.5 2 8 6"/></svg>Human-in-the-loop</span>
      </div>
    </div>

    <div class="sf-demo">
      <div class="sf-demo-label"><span>Live sandbox</span><span>Sample workspace</span></div>
      <div class="console">
        <div class="console-bar"><span class="win-dots"><i></i><i></i><i></i></span><span>nova-agent · sandbox</span><span class="console-time" id="ctaTimer">00:00.00</span></div>
        <div class="console-progress"><i id="ctaProgress"></i></div>
        <div class="agent-log" id="agentLog" aria-live="polite">
          <div class="log-line idle show"><span class="pr">›</span>Agent idle. Press deploy to run a live demo.</div>
          <div class="log-line plan show"><span class="pr">·</span>plan: connect → ingest → tokenize → score → reconcile → close</div>
        </div>
      </div>
      <div class="sf-metrics">
        <div><span>Transactions</span><b data-metric="1,284">—</b></div>
        <div><span>Auto-matched</span><b data-metric="99.4%">—</b></div>
        <div><span>Flagged</span><b data-metric="3">—</b></div>
      </div>
    </div>
  </div>

  <div class="sf-main">
    <div class="sf-brand">
      <a href="#hero" class="brand"><i></i>NOVA</a>
      <p>Autonomous finance agents that read, reconcile and close, with a person in the loop for every decision that matters.</p>
      <a class="sf-status" href="#control"><i></i>All systems operational</a>
      <form class="sf-news" id="sfNews" novalidate>
        <label for="sfEmail">The monthly close report</label>
        <div class="sf-field">
          <input id="sfEmail" type="email" required autocomplete="email" placeholder="you@company.com">
          <button type="submit" aria-label="Subscribe"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
        </div>
        <p class="sf-news-note" id="sfNote">One email a month. Unsubscribe anytime.</p>
      </form>
    </div>
    <nav class="sf-cols" aria-label="Footer">
      <div><h4>Product</h4><ul><li><a href="#sectionPin">How it works</a></li><li><a href="#control">Control</a></li><li><a href="#control">Connectors</a></li><li><a href="#faq">Security</a></li><li><a href="#cta">Pricing</a></li></ul></div>
      <div><h4>Company</h4><ul><li><a href="#">About</a></li><li><a href="#">Customers</a></li><li><a href="#">Careers</a></li><li><a href="#">Press</a></li></ul></div>
      <div><h4>Resources</h4><ul><li><a href="#">Docs</a></li><li><a href="#">API reference</a></li><li><a href="#">Changelog</a></li><li><a href="#">Status</a></li></ul></div>
      <div><h4>Legal</h4><ul><li><a href="#">Privacy</a></li><li><a href="#">Terms</a></li><li><a href="#">DPA</a></li><li><a href="#">Responsible AI</a></li></ul></div>
    </nav>
  </div>

  <div class="sf-mark" aria-hidden="true">
    <span class="mark mark-solid headline grad g-lilac">NOVA</span>
    <span class="mark mark-wire">NOVA</span>
    <i class="mark-scan"></i>
  </div>

  <div class="sf-bottom">
    <span>© 2026 NOVA Labs, Inc.</span>
    <span>Made by <a href="https://madebybeings.com" target="_blank" rel="noopener">Beings</a> · Scanner inspired by <a href="https://evervault.com/" target="_blank" rel="noopener">evervault</a></span>
    <div class="sf-legal"><a href="#">Privacy</a><a href="#">Terms</a><a href="#">Cookies</a></div>
  </div>
</footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script>
/* =========================================================
   CARD + ASCII BUILDERS
   ========================================================= */
const HOLDERS = ["Halcyon Labs", "Okafor & Co", "Northwind Ops", "Kestrel Freight", "Atlas Payroll", "Lumen Health"];
const randInt = (min, max) => Math.floor(Math.random() * (max - min + 1)) + min;
const pick = (arr) => arr[randInt(0, arr.length - 1)];

function cardNumber() {
  const g = () => String(randInt(0, 9999)).padStart(4, "0");
  return `${randInt(4000, 4999)} ${g()} •••• ${g()}`;
}

function generateCode(width, height) {
  const library = [
    "// nova-agent • realtime ledger runtime",
    "/* rendered for visual effect – not executed */",
    "const RISK_THRESHOLD = 0.82;", "const SETTLEMENT = 'T+0';",
    "const token = vault.tokenize(pan, { scheme: 'FPE' });",
    "const score = await risk.score(txn, { model: 'nova-r4' });",
    "if (score > RISK_THRESHOLD) agent.flag(txn, 'velocity_anomaly');",
    "await agent.reconcile(ledger, bankFeed);",
    "ledger.post({ debit: 'AR', credit: 'Cash', amount });",
    "const fx = await rates.convert(amount, 'EUR', 'USD');",
    "agent.plan(['match', 'categorize', 'approve']);",
    "// PAN never leaves the vault boundary",
    "const kyc = await identity.verify(entity);",
    "emit('txn.settled', { id, latency_ms: 38 });",
    "if (!policy.allows(action)) return agent.escalate(human);",
  ];
  for (let i = 0; i < 30; i++) library.push(`const txn_${i} = { amt: ${randInt(10, 9999)}.${randInt(10, 99)}, cur: 'USD', mcc: ${randInt(1000, 9999)} };`);
  for (let i = 0; i < 12; i++) library.push(`risk.window[${i}] = ${Math.random().toFixed(4)};`);

  let flow = library.sort(() => Math.random() - 0.5).join(" ");
  while (flow.length < width * height + width) flow += " " + pick(library);

  const rows = [];
  for (let r = 0; r < height; r++) rows.push(flow.slice(r * width, r * width + width).padEnd(width, " "));
  return rows.join("\n");
}

function fillAscii(wrapper) {
  const el = wrapper.querySelector(".ascii-content");
  const cols = Math.floor(wrapper.offsetWidth / 6.6) + 2;
  const rows = Math.floor(wrapper.offsetHeight / 13) + 1;
  el.dataset.cols = cols;
  el.dataset.rows = rows;
  el.textContent = generateCode(cols, rows);
}

function buildCard(index) {
  const wrapper = document.createElement("div");
  wrapper.className = "card-wrapper";
  const month = String(randInt(1, 12)).padStart(2, "0");
  wrapper.innerHTML = `
    <div class="card card-normal theme-${index % 5}">
      <div class="card-face">
        <div class="card-top">
          <div class="card-chip"></div>
          <div class="contactless"></div>
          <div class="card-logo">NOVA</div>
        </div>
        <div class="card-number">${cardNumber()}</div>
        <div class="card-info">
          <div><small>Card holder</small><div class="card-holder">${HOLDERS[index % HOLDERS.length]}</div></div>
          <div><small>Expires</small><div class="card-expiry">${month}/${randInt(27, 31)}</div></div>
        </div>
      </div>
    </div>
    <div class="card card-ascii"><div class="ascii-content"></div></div>`;
  return wrapper;
}

/* Clip each card against the scanner line at screen center. Returns true if any card is being scanned. */
function updateClipping(wrappers) {
  const scannerX = window.innerWidth / 2;
  const sLeft = scannerX - 4;
  const sRight = scannerX + 4;
  let active = false;

  for (const wrapper of wrappers) {
    const rect = wrapper.getBoundingClientRect();
    const normal = wrapper.querySelector(".card-normal");
    const ascii = wrapper.querySelector(".card-ascii");

    if (rect.left < sRight && rect.right > sLeft) {
      active = true;
      const iLeft = Math.max(sLeft - rect.left, 0);
      const iRight = Math.min(sRight - rect.left, rect.width);
      normal.style.setProperty("--clip-right", `${(iLeft / rect.width) * 100}%`);
      ascii.style.setProperty("--clip-left", `${(iRight / rect.width) * 100}%`);

      if (!wrapper.hasAttribute("data-scanned") && iLeft > 0) {
        wrapper.setAttribute("data-scanned", "true");
        const fx = document.createElement("div");
        fx.className = "scan-effect";
        wrapper.appendChild(fx);
        setTimeout(() => fx.remove(), 600);
      }
    } else {
      if (rect.right < sLeft) {
        normal.style.setProperty("--clip-right", "100%");
        ascii.style.setProperty("--clip-left", "100%");
      } else if (rect.left > sRight) {
        normal.style.setProperty("--clip-right", "0%");
        ascii.style.setProperty("--clip-left", "0%");
      }
      wrapper.removeAttribute("data-scanned");
    }
  }
  return active;
}

/* =========================================================
   THREE.JS AMBIENT PARTICLES
   ========================================================= */
class ParticleSystem {
  constructor(canvas, height, fitEl = null, speed = 1) {
    this.canvas = canvas;
    this.fitEl = fitEl;
    this.speed = speed;
    this.hFn = typeof height === "function" ? height : null;
    this.h = fitEl ? fitEl.offsetHeight : this.hFn ? this.hFn() : height;
    this.count = 400;

    this.scene = new THREE.Scene();
    this.camera = new THREE.OrthographicCamera(-innerWidth / 2, innerWidth / 2, this.h / 2, -this.h / 2, 1, 1000);
    this.camera.position.z = 100;
    this.renderer = new THREE.WebGLRenderer({ canvas, alpha: true, antialias: true });
    this.renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
    this.renderer.setSize(innerWidth, this.h);
    this.renderer.setClearColor(0x000000, 0);
    this.create();
    addEventListener("resize", () => this.resize());
  }

  create() {
    const geo = new THREE.BufferGeometry();
    const pos = new Float32Array(this.count * 3);
    const col = new Float32Array(this.count * 3).fill(1);
    const alpha = new Float32Array(this.count);
    this.vel = new Float32Array(this.count);

    const c = document.createElement("canvas");
    c.width = c.height = 100;
    const ctx = c.getContext("2d");
    const g = ctx.createRadialGradient(50, 50, 0, 50, 50, 50);
    g.addColorStop(0.025, "#fff");
    g.addColorStop(0.1, "hsl(260, 61%, 40%)");
    g.addColorStop(0.25, "hsl(260, 64%, 8%)");
    g.addColorStop(1, "transparent");
    ctx.fillStyle = g;
    ctx.beginPath();
    ctx.arc(50, 50, 50, 0, Math.PI * 2);
    ctx.fill();

    for (let i = 0; i < this.count; i++) {
      pos[i * 3] = (Math.random() - 0.5) * innerWidth * 2;
      pos[i * 3 + 1] = (Math.random() - 0.5) * this.h;
      this.vel[i] = Math.random() * 60 + 30;
      alpha[i] = (Math.random() * 8 + 2) / 10;
    }
    geo.setAttribute("position", new THREE.BufferAttribute(pos, 3));
    geo.setAttribute("color", new THREE.BufferAttribute(col, 3));
    geo.setAttribute("alpha", new THREE.BufferAttribute(alpha, 1));

    const mat = new THREE.ShaderMaterial({
      uniforms: { pointTexture: { value: new THREE.CanvasTexture(c) }, size: { value: 15.0 } },
      vertexShader: `
        attribute float alpha; varying float vAlpha; varying vec3 vColor; uniform float size;
        void main() { vAlpha = alpha; vColor = color;
          gl_PointSize = size; gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0); }`,
      fragmentShader: `
        uniform sampler2D pointTexture; varying float vAlpha; varying vec3 vColor;
        void main() { gl_FragColor = vec4(vColor, vAlpha) * texture2D(pointTexture, gl_PointCoord); }`,
      transparent: true,
      blending: THREE.AdditiveBlending,
      depthWrite: false,
      vertexColors: true,
    });
    this.points = new THREE.Points(geo, mat);
    this.scene.add(this.points);
  }

  render() {
    const pos = this.points.geometry.attributes.position.array;
    const alpha = this.points.geometry.attributes.alpha.array;
    const t = Date.now() * 0.001;
    for (let i = 0; i < this.count; i++) {
      pos[i * 3] += this.vel[i] * 0.016 * this.speed;
      if (pos[i * 3] > innerWidth / 2 + 100) {
        pos[i * 3] = -innerWidth / 2 - 100;
        pos[i * 3 + 1] = (Math.random() - 0.5) * this.h;
      }
      pos[i * 3 + 1] += Math.sin(t + i * 0.1) * 0.5;
      const tw = Math.floor(Math.random() * 10);
      if (tw === 1) alpha[i] -= 0.05; else if (tw === 2) alpha[i] += 0.05;
      alpha[i] = Math.max(0, Math.min(1, alpha[i]));
    }
    this.points.geometry.attributes.position.needsUpdate = true;
    this.points.geometry.attributes.alpha.needsUpdate = true;
    this.renderer.render(this.scene, this.camera);
  }

  resize() {
    if (this.fitEl || this.hFn) {
      this.h = this.fitEl ? this.fitEl.offsetHeight : this.hFn();
      this.camera.top = this.h / 2;
      this.camera.bottom = -this.h / 2;
    }
    this.camera.left = -innerWidth / 2;
    this.camera.right = innerWidth / 2;
    this.camera.updateProjectionMatrix();
    this.renderer.setSize(innerWidth, this.h);
  }
}

/* =========================================================
   CANVAS SCANNER (light bar + particle spray)
   ========================================================= */
class ParticleScanner {
  constructor(canvas, height) {
    this.canvas = canvas;
    this.ctx = canvas.getContext("2d");
    this.hFn = typeof height === "function" ? height : () => height;
    this.h = this.hFn();
    this.particles = [];
    this.count = 0;
    this.lightBarWidth = 3;

    this.baseIntensity = 0.8; this.scanIntensity = 1.8;
    this.baseMax = 800;       this.scanMax = 2500;
    this.baseFade = 60;       this.scanFade = 35;
    this.intensity = this.baseIntensity;
    this.maxParticles = this.baseMax;
    this.fadeZone = this.baseFade;
    this.glow = 1;
    this.transition = 0.05;
    this.scanning = false;

    this.resize();
    this.makeSprite();
    for (let i = 0; i < this.baseMax; i++) this.particles[++this.count] = this.create();
    addEventListener("resize", () => this.resize());
  }

  resize() {
    this.w = innerWidth;
    this.h = this.hFn();
    this.lightBarX = this.w / 2;
    this.canvas.width = this.w;
    this.canvas.height = this.h;
    this.canvas.style.width = this.w + "px";
    this.canvas.style.height = this.h + "px";
  }

  makeSprite() {
    this.sprite = document.createElement("canvas");
    this.sprite.width = this.sprite.height = 16;
    const c = this.sprite.getContext("2d");
    const g = c.createRadialGradient(8, 8, 0, 8, 8, 8);
    g.addColorStop(0, "rgba(255,255,255,1)");
    g.addColorStop(0.3, "rgba(196,181,253,0.8)");
    g.addColorStop(0.7, "rgba(139,92,246,0.4)");
    g.addColorStop(1, "transparent");
    c.fillStyle = g;
    c.beginPath();
    c.arc(8, 8, 8, 0, Math.PI * 2);
    c.fill();
  }

  rf(a, b) { return Math.random() * (b - a) + a; }

  create() {
    const r = this.intensity / this.baseIntensity;
    const sp = 1 + (r - 1) * 1.2;
    const sz = 1 + (r - 1) * 0.7;
    const a = this.rf(0.6, 1);
    return {
      x: this.lightBarX + this.rf(-1.5, 1.5),
      y: this.rf(0, this.h),
      vx: this.rf(0.2, 1.0) * sp,
      vy: this.rf(-0.15, 0.15) * sp,
      radius: this.rf(0.4, 1) * sz,
      alpha: a, originalAlpha: a,
      decay: this.rf(0.005, 0.025) * (2 - r * 0.5),
      life: 1, time: 0,
      twinkleSpeed: this.rf(0.02, 0.08) * sp,
      twinkleAmount: this.rf(0.1, 0.25),
    };
  }

  setActive(active) { this.scanning = active; }

  drawBar() {
    const ctx = this.ctx, x = this.lightBarX, lw = this.lightBarWidth;
    this.glow += ((this.scanning ? 3.5 : 1) - this.glow) * this.transition;
    const gi = this.glow;

    ctx.globalCompositeOperation = "lighter";
    const layer = (half, stops, alpha, radius) => {
      const g = ctx.createLinearGradient(x - half, 0, x + half, 0);
      stops.forEach(([o, c]) => g.addColorStop(o, c));
      ctx.globalAlpha = alpha;
      ctx.fillStyle = g;
      ctx.beginPath();
      ctx.roundRect(x - half, 0, half * 2, this.h, radius);
      ctx.fill();
    };
    layer(lw / 2, [[0, "rgba(255,255,255,0)"], [0.3, `rgba(255,255,255,${0.9 * gi})`], [0.5, `rgba(255,255,255,${gi})`], [0.7, `rgba(255,255,255,${0.9 * gi})`], [1, "rgba(255,255,255,0)"]], 1, 15);
    layer(lw * 2, [[0, "rgba(139,92,246,0)"], [0.5, `rgba(196,181,253,${0.8 * gi})`], [1, "rgba(139,92,246,0)"]], this.scanning ? 1 : 0.8, 25);
    layer(lw * 4, [[0, "rgba(139,92,246,0)"], [0.5, `rgba(139,92,246,${0.4 * gi})`], [1, "rgba(139,92,246,0)"]], this.scanning ? 0.8 : 0.6, 35);
    if (this.scanning) layer(lw * 8, [[0, "rgba(139,92,246,0)"], [0.5, "rgba(139,92,246,0.2)"], [1, "rgba(139,92,246,0)"]], 0.6, 45);

    const v = ctx.createLinearGradient(0, 0, 0, this.h);
    v.addColorStop(0, "rgba(255,255,255,0)");
    v.addColorStop(this.fadeZone / this.h, "rgba(255,255,255,1)");
    v.addColorStop(1 - this.fadeZone / this.h, "rgba(255,255,255,1)");
    v.addColorStop(1, "rgba(255,255,255,0)");
    ctx.globalCompositeOperation = "destination-in";
    ctx.globalAlpha = 1;
    ctx.fillStyle = v;
    ctx.fillRect(0, 0, this.w, this.h);
  }

  render() {
    const t = this.transition;
    this.intensity += ((this.scanning ? this.scanIntensity : this.baseIntensity) - this.intensity) * t;
    this.maxParticles += ((this.scanning ? this.scanMax : this.baseMax) - this.maxParticles) * t;
    this.fadeZone += ((this.scanning ? this.scanFade : this.baseFade) - this.fadeZone) * t;
    const max = Math.floor(this.maxParticles);

    const ctx = this.ctx;
    ctx.globalCompositeOperation = "source-over";
    ctx.clearRect(0, 0, this.w, this.h);
    this.drawBar();

    ctx.globalCompositeOperation = "lighter";
    for (let i = 1; i <= this.count; i++) {
      const p = this.particles[i];
      if (!p) continue;
      p.x += p.vx; p.y += p.vy; p.time++;
      p.alpha = p.originalAlpha * p.life + Math.sin(p.time * p.twinkleSpeed) * p.twinkleAmount;
      p.life -= p.decay;
      if (p.x > this.w + 10 || p.life <= 0) {
        Object.assign(p, this.create(), { decay: p.decay });
        continue;
      }
      let fade = 1;
      if (p.y < this.fadeZone) fade = p.y / this.fadeZone;
      else if (p.y > this.h - this.fadeZone) fade = (this.h - p.y) / this.fadeZone;
      ctx.globalAlpha = Math.max(0, Math.min(1, p.alpha * Math.max(0, Math.min(1, fade))));
      ctx.drawImage(this.sprite, p.x - p.radius, p.y - p.radius, p.radius * 2, p.radius * 2);
    }

    const r = this.intensity / this.baseIntensity;
    let spawn = (Math.random() < this.intensity && this.count < max) ? 1 : 0;
    [[1.1, 1.0, 1.2], [1.3, 1.3, 1.4], [1.5, 1.5, 1.8], [2.0, 2.0, 2.0]].forEach(([th, base, k]) => {
      if (r > th && Math.random() < (r - base) * k) spawn++;
    });
    for (let s = 0; s < spawn; s++) this.particles[++this.count] = this.create();

    if (this.count > max + 200) {
      const excess = Math.min(15, this.count - max);
      for (let i = 0; i < excess; i++) delete this.particles[this.count - i];
      this.count -= excess;
    }
  }
}

/* =========================================================
   WIRE IT UP
   ========================================================= */
gsap.registerPlugin(ScrollTrigger);
ScrollTrigger.config({ ignoreMobileResize: true });


// pinned-section cards
const pinCards = [];
document.querySelectorAll("[data-pin-card]").forEach((panel) => {
  const card = buildCard(+panel.dataset.pinCard);
  panel.prepend(card);
  fillAscii(card);
  pinCards.push(card);
});


const heroFx = {
  particles: new ParticleSystem(document.getElementById("heroParticles"), 0, document.getElementById("hero"), 0.35),
  visible: true,
};
const pinSection = document.getElementById("sectionPin");
const pinIntro = document.querySelector(".pin-intro");
const pinScannerCanvas = document.getElementById("pinScanner");
const pinFx = {
  particles: new ParticleSystem(document.getElementById("pinParticles"), () => Math.round(Math.min(360, pinSection.offsetHeight * 0.7))),
  scanner: new ParticleScanner(document.getElementById("pinScanner"), () => Math.round(Math.min(420, pinSection.offsetHeight * 0.82))),
  visible: false,
};

// only render effects for sections on screen
const io = new IntersectionObserver((entries) => {
  entries.forEach((e) => {
    if (e.target.id === "hero") heroFx.visible = e.isIntersecting;
    if (e.target.id === "sectionPin") pinFx.visible = e.isIntersecting;
  });
});
io.observe(document.getElementById("hero"));
io.observe(document.getElementById("sectionPin"));

// one RAF loop for everything
let last = performance.now();
function loop(now) {
  const dt = Math.min((now - last) / 1000, 0.05);
  last = now;

  if (heroFx.visible) heroFx.particles.render();
  if (pinFx.visible) {
    // keep the scanner out of the way until the intro text has moved past it
    const introRight = pinIntro.getBoundingClientRect().right;
    const fade = Math.max(0, Math.min(1, (innerWidth / 2 - introRight + 20) / 140));
    pinScannerCanvas.style.opacity = fade.toFixed(3);
    pinFx.scanner.setActive(updateClipping(pinCards));
    pinFx.particles.render();
    pinFx.scanner.render();
  }
  requestAnimationFrame(loop);
}
requestAnimationFrame(loop);

addEventListener("resize", () => pinCards.forEach(fillAscii));

// churn the ASCII so it feels live
setInterval(() => {
  document.querySelectorAll(".ascii-content").forEach((el) => {
    if (Math.random() < 0.15) el.textContent = generateCode(+el.dataset.cols, +el.dataset.rows);
  });
}, 200);

/* ---------- Scroll: pin + horizontal + parallax ---------- */
function setupScroll() {
  const track = document.querySelector(".pin-wrap");
  const getLen = () => track.scrollWidth - window.innerWidth;

  gsap.to(track, {
    x: () => -getLen(),
    ease: "none",
    scrollTrigger: {
      trigger: "#sectionPin",
      pin: true,
      anticipatePin: 1,
      start: "top top",
      end: () => "+=" + getLen(),
      scrub: 1,
      invalidateOnRefresh: true,
      onUpdate: (self) => gsap.set("#pinBar", { scaleX: self.progress }),
    },
  });

  // replaces Locomotive's data-scroll-speed parallax
  gsap.utils.toArray("[data-scroll-speed]").forEach((el) => {
    const speed = parseFloat(el.dataset.scrollSpeed) || 1;
    const section = el.closest("section");
    const isHero = section.id === "hero";
    gsap.to(el, {
      y: -speed * (isHero ? 120 : 60),
      ease: "none",
      scrollTrigger: {
        trigger: section,
        start: isHero ? "top top" : "top bottom",
        end: "bottom top",
        scrub: true,
      },
    });
  });

  // fade-and-rise for blocks in the new sections
  gsap.utils.toArray("[data-reveal]").forEach((el, i) => {
    gsap.from(el, {
      opacity: 0,
      y: 36,
      duration: 1,
      ease: "power3.out",
      delay: (i % 3) * 0.08,
      scrollTrigger: { trigger: el, start: "top 90%", once: true },
    });
  });

  // move each headline's gradient "light" as it travels through the viewport
  gsap.utils.toArray(".headline").forEach((el) => {
    const inPin = el.closest("#sectionPin");
    const inMark = el.closest(".sf-mark");
    gsap.fromTo(el, { "--gy": "140vh" }, {
      "--gy": inPin ? "25vh" : inMark ? "8vh" : "-40vh",
      ease: "none",
      scrollTrigger: inPin
        ? { trigger: "#sectionPin", start: "top bottom", end: "top top", scrub: 0.6 }
        : inMark
        ? { trigger: el, start: "top bottom", end: "bottom bottom", scrub: 0.6 }
        : { trigger: el, start: "top bottom", end: "bottom top", scrub: 0.6 },
    });
  });

  ScrollTrigger.refresh();
}

/* ---------- Agentic CTA: runs a simulated agent deployment ---------- */
(function () {
  const wrap = document.getElementById("ctaWrap");
  const btn = document.getElementById("ctaButton");
  const label = document.getElementById("ctaLabel");
  const log = document.getElementById("agentLog");
  const status = document.getElementById("ctaStatus");
  const timer = document.getElementById("ctaTimer");
  const bar = document.getElementById("ctaProgress");
  const metrics = document.querySelectorAll("[data-metric]");
  const sleep = (ms) => new Promise((r) => setTimeout(r, ms));
  const steps = [
    ["Connecting 3 bank feeds", "ok · 212 ms", "ok"],
    ["Ingesting 1,284 transactions", "ok · 0.9 s", "ok"],
    ["Tokenizing card data", "0 raw card numbers stored", "ok"],
    ["Scoring risk on every payment", "3 flagged", "flag"],
    ["Auto-reconciling ledger", "99.4% matched", "ok"],
    ["Drafting month-end close", "ready for review", "ok"],
  ];
  let state = "idle", t0 = 0, raf = 0;

  const fmt = (ms) => {
    const s = ms / 1000;
    return String(Math.floor(s / 60)).padStart(2, "0") + ":" + (s % 60).toFixed(2).padStart(5, "0");
  };
  const tick = () => { timer.textContent = fmt(performance.now() - t0); raf = requestAnimationFrame(tick); };
  const setStatus = (text, cls) => { status.className = "chip-status " + cls; status.querySelector("em").textContent = text; };

  function addLine(html, cls = "") {
    const line = document.createElement("div");
    line.className = "log-line " + cls;
    const ts = ((performance.now() - t0) / 1000).toFixed(2) + "s";
    line.innerHTML = `<span class="ts">${ts}</span>` + html;
    log.appendChild(line);
    requestAnimationFrame(() => requestAnimationFrame(() => line.classList.add("show")));
    return line;
  }

  btn.addEventListener("click", async () => {
    if (state === "running") return;
    state = "running";
    wrap.classList.remove("done");
    wrap.classList.add("running");
    label.innerHTML = '<span class="dots">Agent working</span>';
    btn.setAttribute("aria-label", "Agent working");
    log.innerHTML = "";
    bar.style.width = "0%";
    metrics.forEach((m) => { m.textContent = "—"; m.classList.remove("pop"); });
    t0 = performance.now();
    cancelAnimationFrame(raf);
    tick();
    setStatus(`Running · 0/${steps.length}`, "running");

    for (let i = 0; i < steps.length; i++) {
      const [text, result, kind] = steps[i];
      const line = addLine(`<span class="pr">›</span><span class="tx">${text}</span><span class="st dots"></span>`);
      await sleep(450 + Math.random() * 500);
      const st = line.querySelector(".st");
      st.className = "st " + kind;
      st.textContent = result;
      bar.style.width = ((i + 1) / steps.length) * 100 + "%";
      setStatus(`Running · ${i + 1}/${steps.length}`, "running");
    }

    await sleep(350);
    addLine('<span class="pr">✓</span><span class="tx">Agent deployed</span><a href="#faq">Book a 20-min onboarding →</a>', "final");
    cancelAnimationFrame(raf);
    setStatus("Agent live", "live");
    wrap.classList.remove("running");
    wrap.classList.add("done");
    label.textContent = "Agent live · run again";
    btn.setAttribute("aria-label", "Run the agent demo again");
    state = "done";
    metrics.forEach((m, i) => setTimeout(() => { m.textContent = m.dataset.metric; m.classList.add("pop"); }, i * 160));
  });
})();

/* ---------- Hero scene: fit, tilt, orbit dust, live agent pipeline ---------- */
(function () {
  const hero = document.getElementById("hero");
  const scene = document.getElementById("heroScene");
  const inner = document.getElementById("sceneInner");
  const beam = document.getElementById("beam");

  // scale the fixed-size scene to its column and line the water reflection up with the beam
  function fit() {
    const box = scene.getBoundingClientRect();
    const mobile = window.innerWidth <= 960;
    const s = Math.min(1.15, box.width / (mobile ? 720 : 860), box.height / 640);
    inner.style.transition = "none";
    inner.style.setProperty("--rx", "0deg");
    inner.style.setProperty("--ry", "0deg");
    inner.style.setProperty("--s", s.toFixed(3));
    const b = beam.getBoundingClientRect();
    const h = hero.getBoundingClientRect();
    hero.style.setProperty("--beam-x", (b.left + b.width / 2 - h.left).toFixed(1) + "px");
    void inner.offsetWidth;
    inner.style.transition = "";
  }
  fit();
  addEventListener("resize", fit);
  if (document.fonts) document.fonts.ready.then(fit);

  // subtle mouse tilt
  if (matchMedia("(pointer: fine)").matches) {
    hero.addEventListener("pointermove", (e) => {
      const r = hero.getBoundingClientRect();
      const x = (e.clientX - r.left) / r.width - 0.5;
      const y = (e.clientY - r.top) / r.height - 0.5;
      inner.style.setProperty("--ry", (x * 6).toFixed(2) + "deg");
      inner.style.setProperty("--rx", (-y * 4).toFixed(2) + "deg");
    });
    hero.addEventListener("pointerleave", () => {
      inner.style.setProperty("--rx", "0deg");
      inner.style.setProperty("--ry", "0deg");
    });
  }

  // dust scattered around the orbit
  const NS = "http://www.w3.org/2000/svg";
  const dust = document.getElementById("ringDust");
  for (let i = 0; i < 160; i++) {
    const a = Math.random() * Math.PI * 2;
    const r = Math.random() < 0.6 ? 0.86 + Math.random() * 0.22 : Math.sqrt(Math.random());
    const c = document.createElementNS(NS, "circle");
    c.setAttribute("cx", (450 + Math.cos(a) * 400 * r).toFixed(1));
    c.setAttribute("cy", (360 + Math.sin(a) * 120 * r).toFixed(1));
    c.setAttribute("r", (Math.random() * 1.1 + 0.3).toFixed(2));
    c.setAttribute("fill", "#d8ccff");
    c.setAttribute("opacity", (Math.random() * 0.7 + 0.15).toFixed(2));
    if (Math.random() < 0.35) {
      c.classList.add("tw");
      c.style.animationDelay = (-Math.random() * 3).toFixed(2) + "s";
    }
    dust.appendChild(c);
  }

  // live code in the side panels
  const mini = document.getElementById("miniCode");
  const ghost = document.getElementById("ghostCode");
  mini.textContent = generateCode(26, 11);
  ghost.textContent = generateCode(22, 7);
  setInterval(() => {
    if (!heroFx.visible) return;
    mini.textContent = generateCode(26, 11);
    if (Math.random() < 0.5) ghost.textContent = generateCode(22, 7);
  }, 450);

  // the agent working through one transaction at a time
  const items = [...document.querySelectorAll("#checklist li")];
  const stages = [...document.querySelectorAll("#pipeline span")];
  const stageOf = [0, 1, 2, 2, 3, 4];
  const json = document.getElementById("txnJson");
  const sweep = document.getElementById("cardSweep");
  const fields = ["txn_id", "amount", "currency", "category", "agent", "status", "timestamp"];
  const wait = (ms) => new Promise((r) => setTimeout(r, ms));
  let txn;

  function renderTxn(flash = []) {
    const lines = fields.map((f, i) => {
      const v = txn[f];
      const val = typeof v === "number" ? v.toFixed(2) : `"${v}"`;
      const cls = flash.includes(f) ? "v flash" : "v";
      return `  <span class="k">"${f}"</span>: <span class="${cls}">${val}</span>${i < fields.length - 1 ? "," : ""}`;
    });
    json.innerHTML = "{\n" + lines.join("\n") + "\n}";
    setTimeout(() => json.querySelectorAll(".flash").forEach((el) => el.classList.remove("flash")), 600);
  }

  function newTxn() {
    txn = {
      txn_id: String(randInt(1e9, 9e9)),
      amount: Math.random() * 9800 + 120,
      currency: pick(["USD", "EUR", "GBP"]),
      category: "pending",
      agent: "ingest",
      status: "received",
      timestamp: new Date().toISOString().replace(/\.\d+Z$/, "Z"),
    };
  }

  async function cycle() {
    for (;;) {
      newTxn();
      items.forEach((li) => (li.className = ""));
      stages.forEach((s) => s.classList.remove("on"));
      renderTxn(["txn_id", "amount", "currency", "timestamp"]);

      for (let i = 0; i < items.length; i++) {
        items[i].className = "active";
        stages.forEach((s, j) => s.classList.toggle("on", j === stageOf[i]));
        if (i === 1) {
          Object.assign(txn, { agent: "vault", status: "tokenized" });
          sweep.classList.remove("go");
          void sweep.offsetWidth;
          sweep.classList.add("go");
          renderTxn(["agent", "status"]);
        }
        if (i === 2) { Object.assign(txn, { agent: "risk", status: "approved" }); renderTxn(["agent", "status"]); }
        if (i === 3) { txn.category = pick(["supplies", "software", "travel", "logistics", "payroll"]); renderTxn(["category"]); }
        if (i === 4) { Object.assign(txn, { agent: "reconcile", status: "matched" }); renderTxn(["agent", "status"]); }
        if (i === 5) { txn.status = "posted"; renderTxn(["status"]); }
        await wait(900);
        items[i].className = "done";
      }
      stages.forEach((s) => s.classList.remove("on"));
      await wait(1600);
    }
  }
  cycle();
})();

/* ---------- Control section: ledger, guardrails, connectors, audit, approvals ---------- */
(function () {
  const section = document.getElementById("control");
  let visible = false;
  new IntersectionObserver(([e]) => { visible = e.isIntersecting; }).observe(section);

  // pointer-following glow on glass tiles
  document.querySelectorAll(".tile").forEach((t) => t.addEventListener("pointermove", (e) => {
    const r = t.getBoundingClientRect();
    t.style.setProperty("--mx", (e.clientX - r.left).toFixed(0) + "px");
    t.style.setProperty("--my", (e.clientY - r.top).toFixed(0) + "px");
  }));

  // bars grow once the month-end tile is on screen
  const once = new IntersectionObserver((es) => es.forEach((e) => {
    if (e.isIntersecting) { e.target.classList.add("in"); once.unobserve(e.target); }
  }), { threshold: 0.35 });
  document.querySelectorAll(".t-close").forEach((el) => once.observe(el));

  const VENDORS = ["Halcyon Labs", "Kestrel Freight", "Atlas Payroll", "Lumen Health", "Northwind Ops", "Okafor & Co",
    "Vela Cloud", "Brightline Media", "Orchard Supply", "Meridian Travel"];
  const clock = () => new Date().toTimeString().slice(0, 8);
  const money = (n) => "$" + n.toLocaleString("en-US", { minimumFractionDigits: 2, maximumFractionDigits: 2 });
  const hex = (n) => Array.from({ length: n }, () => "0123456789abcdef"[randInt(0, 15)]).join("");

  // ---- audit trail
  const audit = document.getElementById("audit");
  const EVENTS = [
    ["agent/reconcile", () => `Matched INV-${randInt(2000, 9999)} to TXN ${randInt(1000, 9999)}`],
    ["agent/risk", () => `Flagged ${pick(VENDORS)} for a velocity anomaly`],
    ["agent/vault", () => `Tokenized card ending ${randInt(1000, 9999)}`],
    ["agent/close", () => `Accrued ${money(Math.random() * 9000 + 500)} to ${pick(["Software", "Travel", "Freight", "Payroll"])}`],
  ];
  function addAudit(who, what, human = false) {
    const li = document.createElement("li");
    if (human) li.className = "h";
    li.innerHTML = `<span class="who">${who}</span><time>${clock()}</time><span class="what">${what}</span><span class="hash">sha256 0x${hex(6)}…${hex(4)}</span>`;
    audit.prepend(li);
    while (audit.children.length > 3) audit.lastElementChild.remove();
  }
  for (let i = 0; i < 3; i++) { const [w, f] = pick(EVENTS); addAudit(w, f()); }
  setInterval(() => { if (visible) { const [w, f] = pick(EVENTS); addAudit(w, f()); } }, 3400);

  // ---- live ledger
  const body = document.getElementById("ledgerBody");
  const out = { scan: document.getElementById("ledScan"), ok: document.getElementById("ledOk"), flag: document.getElementById("ledFlag") };
  const n = { scan: 1284, ok: 1271, flag: 13 };
  const counts = () => Object.keys(n).forEach((k) => (out[k].textContent = n[k].toLocaleString("en-US")));
  function row(settled) {
    const el = document.createElement("div");
    el.className = "ledger-row";
    const flag = Math.random() < 0.14;
    const amt = Math.random() < 0.7 ? Math.random() * 4800 + 40 : Math.random() * 42000 + 5000;
    el.innerHTML = `<span class="t">${clock()}</span><span class="cp">${pick(VENDORS)}</span><span class="amt">${money(amt)}</span><span class="badge b-scan">Scanning</span>`;
    const settle = () => {
      const b = el.querySelector(".badge");
      b.className = "badge " + (flag ? "b-flag" : "b-ok");
      b.textContent = flag ? "Flagged" : "Matched";
    };
    if (settled) settle();
    return { el, settle, flag };
  }
  for (let i = 0; i < 14; i++) body.appendChild(row(true).el);
  counts();
  setInterval(() => {
    if (!visible) return;
    const r = row(false);
    r.el.classList.add("enter");
    body.prepend(r.el);
    while (body.children.length > 14) body.lastElementChild.remove();
    n.scan++;
    counts();
    setTimeout(() => { r.settle(); r.flag ? n.flag++ : n.ok++; counts(); }, 900);
  }, 1800);

  // ---- guardrails
  const switches = [...document.querySelectorAll("#guards .switch")];
  const meter = document.getElementById("autoMeter");
  const autoLabel = document.getElementById("autoLabel");
  function autonomy() {
    const on = switches.map((s) => s.getAttribute("aria-checked") === "true");
    const score = Math.max(8, Math.min(100, 45 + (on[0] ? 35 : 0) - (on[1] ? 10 : 0) - (on[2] ? 10 : 0) - (on[3] ? 12 : 0)));
    meter.style.width = score + "%";
    autoLabel.textContent = score >= 70 ? "Autonomous" : score >= 40 ? "Supervised" : "Guarded";
  }
  switches.forEach((s) => s.addEventListener("click", () => {
    const next = s.getAttribute("aria-checked") !== "true";
    s.setAttribute("aria-checked", String(next));
    autonomy();
    addAudit("human/you", `${next ? "Enabled" : "Disabled"} policy: ${s.dataset.policy}`, true);
  }));
  autonomy();

  // ---- approvals
  const REQUESTS = [
    ["Kestrel Freight", 18240, "new bank details, verified by callback"],
    ["Vela Cloud", 42600, "annual renewal, 12% above last year"],
    ["Meridian Travel", 7315.5, "first invoice from this vendor"],
    ["Orchard Supply", 26980, "cross-border payment to a EUR account"],
  ];
  const apMsg = document.getElementById("apMsg");
  const apActions = document.getElementById("apActions");
  const apResult = document.getElementById("apResult");
  let req = null;
  function newRequest() {
    let next;
    do { next = pick(REQUESTS); } while (next === req);
    req = next;
    apMsg.innerHTML = `Pay <b>${req[0]}</b> ${money(req[1])}: ${req[2]}.`;
    apActions.hidden = false;
    apResult.hidden = true;
  }
  function decide(ok) {
    apActions.hidden = true;
    apResult.hidden = false;
    apResult.className = "ap-result" + (ok ? "" : " held");
    apResult.textContent = ok ? "Approved · payment scheduled · logged" : "Held · vendor asked to re-verify · logged";
    addAudit("human/you", `${ok ? "Approved" : "Held"} ${money(req[1])} to ${req[0]}`, true);
    setTimeout(newRequest, 4000);
  }
  document.getElementById("apOk").addEventListener("click", () => decide(true));
  document.getElementById("apHold").addEventListener("click", () => decide(false));
  newRequest();

  // ---- connectors orbit
  const orbit = document.getElementById("orbit");
  const nodes = [...orbit.querySelectorAll(".node")];
  let W = 0, H = 0, sizes = [];
  const measure = () => { W = orbit.clientWidth; H = orbit.clientHeight; sizes = nodes.map((el) => [el.offsetWidth, el.offsetHeight]); };
  measure();
  addEventListener("resize", measure);
  if (document.fonts) document.fonts.ready.then(measure);
  function spin(t) {
    if (visible) {
      const rx = W * 0.4, ry = H * 0.34, cx = W / 2, cy = H / 2;
      nodes.forEach((el, i) => {
        const a = (t / 14000) * Math.PI * 2 + (i / nodes.length) * Math.PI * 2;
        const depth = (Math.sin(a) + 1) / 2;
        const x = cx + Math.cos(a) * rx - sizes[i][0] / 2;
        const y = cy + Math.sin(a) * ry - sizes[i][1] / 2;
        el.style.transform = `translate(${x.toFixed(1)}px, ${y.toFixed(1)}px) scale(${(0.82 + depth * 0.26).toFixed(3)})`;
        el.style.opacity = (0.4 + depth * 0.6).toFixed(2);
        el.style.zIndex = depth > 0.5 ? 3 : 1;
      });
    }
    requestAnimationFrame(spin);
  }
  requestAnimationFrame(spin);
})();

/* ---------- FAQ accordion with smooth height ---------- */
(function () {
  const items = [...document.querySelectorAll(".faq-item")];
  let refreshT;
  const refresh = () => { clearTimeout(refreshT); refreshT = setTimeout(() => ScrollTrigger.refresh(), 450); };

  function open(d) {
    const a = d.querySelector(".faq-a");
    d.open = true;
    a.animate([{ height: "0px", opacity: 0 }, { height: a.scrollHeight + "px", opacity: 1 }],
      { duration: 420, easing: "cubic-bezier(.2,.7,.2,1)" });
  }
  function close(d) {
    const a = d.querySelector(".faq-a");
    const anim = a.animate([{ height: a.offsetHeight + "px", opacity: 1 }, { height: "0px", opacity: 0 }],
      { duration: 300, easing: "ease", fill: "forwards" });
    anim.onfinish = () => { d.open = false; anim.cancel(); };
  }
  items.forEach((d) => {
    d.querySelector("summary").addEventListener("click", (e) => {
      e.preventDefault();
      if (d.open) close(d);
      else { items.filter((o) => o !== d && o.open).forEach(close); open(d); }
      refresh();
    });
  });
})();

/* ---------- Footer newsletter (front end only; wire to your email provider) ---------- */
(function () {
  const form = document.getElementById("sfNews");
  const input = document.getElementById("sfEmail");
  const note = document.getElementById("sfNote");
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    if (!input.value || !input.checkValidity()) {
      note.textContent = "Enter a valid work email.";
      note.className = "sf-news-note err";
      input.focus();
      return;
    }
    note.textContent = "You're on the list. Check your inbox to confirm.";
    note.className = "sf-news-note ok";
    input.value = "";
  });
})();

if (document.readyState === "complete") setupScroll();
else window.addEventListener("load", setupScroll);
document.fonts && document.fonts.ready.then(() => ScrollTrigger.refresh());
</script>
</body>
</html>
```

