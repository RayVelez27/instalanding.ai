INSTALANDING.AI · SmartCare Clinical AI Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
SmartCare Clinical AI Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/smartcare-clinical-ai-landing-page

smartcare-ai.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · SmartCare Clinical AI Landing Page
  slug     smartcare-clinical-ai-landing-page
  prompt   https://instalanding.ai/p/smartcare-clinical-ai-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/smartcare-clinical-ai-landing-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of the main <style>: --ink #070a13, --text, --signal #8db5ff,
            --alert / --warn / --ok, --panel, --radius 16px, --display (Bricolage Grotesque), --sans (Hanken Grotesk), --mono (IBM Plex Mono)
  sections  nav, menu, hero, metrics, features, predictive, how-it-works, testimonials, governance, faq, cta, footer
  scripts   1) page behaviour: full-screen menu + hover preview, CTA spotlight, FAQ accordion, risk chart (Catmull-Rom curve)
            2) hero HUD: builds the tick rings and 36 radiating pills into #hudRings and drives the findings readout
            3) platform card graphics drawn into each card's SVG in JS  4) iridescence shader, plain WebGL, behind the hero
            No CDN libraries; fonts from Google Fonts.
  assets    none: inline SVG, CSS gradients, an SVG-noise data URI for the CTA grain

  ADAPTING
  - The shader's tint is hard-coded (gl.uniform3f uColor 0.3, 0.42, 0.82) and the card-graphics script hard-codes
    SIG/ALERT hex values; neither reads the CSS tokens, so retheme them by hand alongside --signal / --alert.
  - The hero canvas is screen-blended and masked to an ellipse in CSS (.irid); without WebGL the host gets
    data-irid="off" and a CSS glow stands in. Keep both paths.
  - The menu is role=dialog + inert while closed; the script toggles inert/aria-expanded, so keep those ids (#menu, #menuBtn).
  - The CTA (#start) sits inside the FAQ section's .wrap, so moving or restyling the FAQ moves it too.
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>SmartCare Solutions</title>
<meta name="description" content="Clinical AI for imaging and risk. Pre-reads every study, ranks what needs a clinician now, and shows the evidence behind each flag." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,200..600&family=Hanken+Grotesk:wght@300;400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap" rel="stylesheet" />

<style>
/* Layout: a quiet clinical instrument page. Light grotesque headlines on deep ink, one cool
   signal accent, data set in mono. The shader and the lit primary button are the
   only two effects; everything else stays still. Single dark look by choice. */
:root {
  color-scheme: dark;
  --ink: #070a13;
  --ink-2: #0c1121;
  --ink-3: #121933;
  --line: rgba(160, 182, 235, 0.11);
  --line-2: rgba(160, 182, 235, 0.22);
  --text: #e9ecf5;
  --text-2: #b8bfd5;
  --mute: #848ba5;
  --signal: #8db5ff;
  --signal-deep: #2b56c9;
  --glow: rgb(176, 222, 255);
  --glow-soft: rgba(176, 222, 255, 0.45);
  --alert: #ff6b7d;
  --warn: #f0b64e;
  --ok: #4fcf9f;

  /* Panel component: a near-black card with a soft accent glow rising from
     behind its top edge, an icon-tile header, divided KPI row, a smooth
     curve with a live endpoint, and an outline action at the foot. */
  --panel: #05070d;
  --panel-line: rgba(160, 182, 235, 0.14);
  --signal-10: rgba(141, 181, 255, 0.1);
  --signal-16: rgba(141, 181, 255, 0.16);
  --signal-50: rgba(141, 181, 255, 0.5);
  --radius: 16px;

  --display: "Bricolage Grotesque", "Helvetica Neue", Helvetica, Arial, sans-serif;
  --sans: "Hanken Grotesk", "Helvetica Neue", Helvetica, Arial, system-ui, sans-serif;
  --mono: "IBM Plex Mono", ui-monospace, "SFMono-Regular", Menlo, Consolas, monospace;

  --ease: cubic-bezier(0.6, 0, 0.2, 1);
  --gutter: clamp(20px, 4vw, 48px);
  --section: clamp(88px, 11vw, 160px);
}

*, *::before, *::after { box-sizing: border-box; }
html { background: var(--ink); scroll-behavior: smooth; -webkit-font-smoothing: antialiased; }
body {
  margin: 0;
  background: var(--ink);
  color: var(--text);
  font-family: var(--sans);
  font-size: 16px;
  font-weight: 400;
  line-height: 1.55;
  overflow-x: hidden;
}
a { color: inherit; text-decoration: none; }
button { font: inherit; color: inherit; background: none; border: none; cursor: pointer; padding: 0; }
svg, canvas { display: block; max-width: 100%; }
:focus-visible { outline: 2px solid var(--signal); outline-offset: 3px; border-radius: 6px; }

.page { overflow-x: clip; position: relative; }
.wrap { max-width: 1240px; margin: 0 auto; padding-inline: var(--gutter); }

.label {
  font-family: var(--mono);
  font-size: 12px;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--mute);
}

h1, h2, h3 { margin: 0; text-wrap: balance; }
.display {
  font-family: var(--display);
  font-weight: 300;
  letter-spacing: -0.035em;
  line-height: 0.98;
}
.display em, .quote blockquote em { font-style: normal; color: var(--signal); font-weight: 400; }

/* ───────── Buttons ───────── */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  padding: 13px 22px;
  border-radius: 999px;
  font-size: 15px;
  font-weight: 500;
  white-space: nowrap;
  transition: background 0.4s var(--ease), border-color 0.4s var(--ease),
    box-shadow 0.4s var(--ease), color 0.4s var(--ease);
}
.btn svg { width: 15px; height: 15px; transition: transform 0.4s var(--ease); }
.btn:hover svg { transform: translateX(2px); }

/* The power-switch idea, kept: unlit it is a dark pill; on hover current runs
   through it as a tight cyan inset and a short bloom. */
.btn-primary {
  background: var(--signal-deep);
  color: #fff;
  border: 1px solid rgba(190, 215, 255, 0.4);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.16), 0 12px 30px -14px rgba(43, 86, 201, 0.9);
}
.btn-primary:hover, .btn-primary:focus-visible {
  border-color: #fff;
  box-shadow: inset 0 0 1px var(--glow), inset 0 0 10px var(--glow-soft),
    0 0 18px var(--glow-soft), 0 0 52px rgba(43, 86, 201, 0.5);
}
.btn-quiet {
  border: 1px solid var(--line-2);
  color: var(--text-2);
}
.btn-quiet:hover { border-color: rgba(190, 210, 255, 0.45); color: var(--text); }

/* ───────── Header + full-screen menu ─────────
   One header at every width: logo, a live status line, the pilot button and a
   Menu pill. Opening it wipes a full-screen index down over the page: large
   section links that rise out of masks, each with a live figure, a preview
   panel that follows whichever link is hovered or focused, and a slow ring
   instrument turning in the background. The header bar stays on top. */
.header { position: sticky; top: env(safe-area-inset-top, 0px); z-index: 60; }
.header-bar {
  position: relative;
  background: rgba(5, 7, 13, 0.72);
  backdrop-filter: blur(18px) saturate(140%);
  -webkit-backdrop-filter: blur(18px) saturate(140%);
  border-bottom: 1px solid var(--line);
  transition: background 0.5s var(--ease), border-color 0.5s var(--ease), backdrop-filter 0.5s var(--ease);
}
.header[data-open="true"] .header-bar {
  background: transparent;
  border-color: transparent;
  backdrop-filter: none;
  -webkit-backdrop-filter: none;
}
.header-bar .wrap { display: flex; align-items: center; gap: 20px; height: 72px; }
.logo { display: inline-flex; align-items: center; gap: 10px; font-weight: 500; font-size: 15px; letter-spacing: -0.01em; flex-shrink: 0; }
.logo-mark {
  width: 28px; height: 28px;
  border-radius: 8px;
  border: 1px solid var(--line-2);
  display: grid; place-items: center;
  color: var(--signal);
}
.logo-mark svg { width: 15px; height: 15px; }
.logo span { color: var(--mute); font-weight: 400; }
.header-status {
  margin-inline: auto;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-family: var(--mono);
  font-size: 11.5px;
  color: var(--mute);
  white-space: nowrap;
}
.header-status i { width: 6px; height: 6px; border-radius: 50%; background: var(--ok); box-shadow: 0 0 8px var(--ok); }
.header-actions { margin-left: auto; display: flex; align-items: center; gap: 10px; }
.header-status + .header-actions { margin-left: 0; }
.header .btn-primary { padding: 9px 16px; font-size: 14px; }
.menu-btn {
  display: inline-flex;
  align-items: center;
  gap: 12px;
  height: 40px;
  padding: 0 6px 0 16px;
  border-radius: 999px;
  border: 1px solid var(--line-2);
  background: rgba(255, 255, 255, 0.02);
  font-size: 14px;
  font-weight: 500;
  color: var(--text);
  transition: border-color 0.3s var(--ease), background 0.3s var(--ease);
}
.menu-btn:hover { border-color: var(--signal-50); background: var(--signal-10); }
.menu-btn .lbl { min-width: 3.2em; text-align: left; }
.burger { position: relative; width: 28px; height: 28px; border-radius: 50%; background: var(--ink-3); color: var(--text); }
.burger i {
  position: absolute;
  left: 8px; right: 8px;
  height: 1.5px;
  border-radius: 2px;
  background: currentColor;
  transition: transform 0.5s var(--ease), top 0.5s var(--ease), left 0.5s var(--ease);
}
.burger i:first-child { top: 11px; }
.burger i:last-child { top: 16px; left: 11px; }
.header[data-open="true"] .burger i:first-child { top: 13.25px; transform: rotate(45deg); }
.header[data-open="true"] .burger i:last-child { top: 13.25px; left: 8px; transform: rotate(-45deg); }

/* the overlay */
.menu {
  --curtain: cubic-bezier(0.76, 0, 0.24, 1);
  position: fixed;
  inset: 0;
  z-index: 50;
  background: #04060c;
  clip-path: inset(0 0 100% 0);
  visibility: hidden;
  transition: clip-path 0.9s var(--curtain), visibility 0s linear 0.9s;
}
.menu.open { clip-path: inset(0 0 0 0); visibility: visible; transition-delay: 0s; }
.menu-bg { position: absolute; inset: 0; overflow: hidden; pointer-events: none; }
.menu-bg::before {
  content: "";
  position: absolute;
  right: -10%; top: 10%;
  width: 70vmax; height: 70vmax;
  border-radius: 50%;
  background: radial-gradient(closest-side, rgba(43, 86, 201, 0.32), transparent 70%);
}
.menu-bg::after {
  content: "";
  position: absolute;
  inset: 0;
  opacity: 0.06;
  mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.6 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}
.menu-rings {
  position: absolute;
  right: -18vmax;
  bottom: -26vmax;
  width: 80vmax;
  height: 80vmax;
  opacity: 0;
  transform: rotate(-20deg) scale(0.92);
  transition: opacity 1.4s var(--ease) 0.3s, transform 1.8s var(--ease) 0.2s;
}
.menu.open .menu-rings { opacity: 0.55; transform: rotate(0deg) scale(1); }
.menu-rings svg { width: 100%; height: 100%; animation: ring-turn 140s linear infinite; }
.menu-rings circle { fill: none; }
@keyframes ring-turn { to { transform: rotate(1turn); } }

.menu-scroll {
  position: relative;
  height: 100%;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  padding-top: calc(72px + env(safe-area-inset-top, 0px));
  padding-bottom: env(safe-area-inset-bottom, 0px);
}
.menu-scroll > .wrap { width: 100%; }
.menu-grid {
  flex: 1;
  display: grid;
  grid-template-columns: minmax(0, 1.55fr) minmax(0, 1fr);
  gap: 40px clamp(32px, 6vw, 110px);
  align-items: center;
  padding-block: clamp(24px, 5vh, 64px);
}
.menu-index { min-width: 0; }
.menu-index .label { display: block; margin-bottom: 14px; }
.menu-index ul { list-style: none; margin: 0; padding: 0; }
.m-link {
  display: grid;
  grid-template-columns: minmax(0, 1fr) auto;
  align-items: baseline;
  gap: 24px;
  padding-block: clamp(4px, 1vh, 10px);
  border-bottom: 1px solid var(--line);
}
.m-link .mask { display: block; overflow: hidden; padding-bottom: 0.06em; }
.m-link .t {
  display: block;
  font-family: var(--display);
  font-weight: 200;
  font-size: clamp(36px, min(5.6vw, 9.5vh), 92px);
  line-height: 1.02;
  white-space: nowrap;
  letter-spacing: -0.045em;
  transform: translateY(110%);
  transition: transform 1s cubic-bezier(0.2, 0.8, 0.2, 1), color 0.4s var(--ease), opacity 0.4s var(--ease);
}
.menu.open .m-link .t { transform: none; transition-delay: calc(var(--i) * 70ms + 280ms), 0s, 0s; }
.m-link .meta {
  font-family: var(--mono);
  font-size: 12px;
  color: var(--mute);
  white-space: nowrap;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  transition: color 0.4s var(--ease);
}
.m-link .meta svg { width: 16px; height: 16px; transition: transform 0.5s var(--ease); }
.menu-index ul:hover .m-link:not(:hover) .t,
.menu-index ul:focus-within .m-link:not(:focus-visible):not(:hover) .t { opacity: 0.3; }
.m-link:hover .t, .m-link:focus-visible .t { color: var(--signal); }
.m-link:hover .meta, .m-link:focus-visible .meta { color: var(--text); }
.m-link:hover .meta svg, .m-link:focus-visible .meta svg { transform: translateX(6px); }
.m-link:focus-visible { outline: none; }

.menu-preview .panel-body { transition: opacity 0.25s var(--ease); }
.menu-preview.swap .panel-body { opacity: 0; }
.menu-preview h3 { font-family: var(--display); font-weight: 300; font-size: clamp(26px, 2.4vw, 34px); letter-spacing: -0.035em; line-height: 1.05; }
.menu-preview p { margin: 0; font-size: 14.5px; color: var(--text-2); max-width: 42ch; }
.menu-preview .k-line { display: flex; justify-content: space-between; gap: 12px; }

.menu-bottom {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  gap: 20px 32px;
  padding-block: 24px 30px;
  border-top: 1px solid var(--line);
}
.menu-bottom .col { display: flex; flex-direction: column; gap: 6px; min-width: 0; }
.menu-bottom .col .label { margin-bottom: 4px; }
.menu-bottom a { font-size: 14px; color: var(--text-2); width: fit-content; transition: color 0.3s var(--ease); }
.menu-bottom a:hover { color: var(--signal); }
.menu-bottom p { margin: 0; font-family: var(--mono); font-size: 11.5px; line-height: 1.7; color: var(--mute); }

.menu [data-i] {
  opacity: 0;
  transform: translateY(14px);
  transition: opacity 0.6s var(--ease), transform 0.8s var(--ease);
}
.menu.open [data-i] {
  opacity: 1;
  transform: none;
  transition-delay: calc(var(--i) * 70ms + 300ms);
}

@media (max-width: 900px) {
  .menu-grid { grid-template-columns: minmax(0, 1fr); align-items: start; }
  .menu-preview { display: none; }
  .menu-bottom { grid-template-columns: repeat(2, minmax(0, 1fr)); }
}
@media (max-width: 760px) {
  .header-status { display: none; }
  .header-status + .header-actions { margin-left: auto; }
}
@media (max-width: 600px) {
  .header .header-actions .btn-primary { display: none; }
  .m-link .meta span { display: none; }
}
@media (prefers-reduced-motion: reduce) {
  .menu { transition: visibility 0s; }
  .m-link .t { transform: none; }
}

/* ───────── Hero ───────── */
.hero { position: relative; isolation: isolate; }
.hero-glow { position: absolute; inset: 0; z-index: -1; pointer-events: none; }
.irid {
  position: absolute;
  top: -14%;
  right: -16%;
  width: min(1000px, 92vw);
  height: min(860px, 120%);
  opacity: 0;
  mix-blend-mode: screen;
  transition: opacity 2.4s var(--ease);
  -webkit-mask-image: radial-gradient(55% 52% at 58% 46%, #000 0%, rgba(0, 0, 0, 0.6) 46%, transparent 76%);
  mask-image: radial-gradient(55% 52% at 58% 46%, #000 0%, rgba(0, 0, 0, 0.6) 46%, transparent 76%);
}
.irid.on { opacity: 0.5; }
.hero-glow[data-irid="off"] .irid { display: none; }
.hero-glow[data-irid="off"]::after {
  content: "";
  position: absolute;
  top: 0; right: -10%;
  width: 70%; height: 100%;
  background: radial-gradient(40% 40% at 55% 45%, rgba(43, 86, 201, 0.45), transparent 70%);
  filter: blur(30px);
}

.hero-grid {
  display: grid;
  grid-template-columns: minmax(0, 0.95fr) minmax(0, 1.1fr);
  gap: clamp(36px, 5vw, 80px);
  align-items: center;
  padding-block: clamp(56px, 8vw, 120px) clamp(56px, 7vw, 96px);
}
.hero-copy { display: flex; flex-direction: column; gap: 26px; min-width: 0; }
.hero h1 { font-size: clamp(42px, 5.8vw, 82px); }
.hero .lede { margin: 0; max-width: 46ch; font-size: clamp(16px, 1.3vw, 18px); color: var(--text-2); font-weight: 300; }
.hero-actions { display: flex; flex-wrap: wrap; gap: 12px; }
.hero-meta {
  display: flex; flex-wrap: wrap; gap: 8px 20px;
  font-family: var(--mono); font-size: 12px; color: var(--mute);
  padding-top: 6px;
}
.hero-meta span { display: inline-flex; align-items: center; gap: 8px; }
.hero-meta span::before { content: ""; width: 4px; height: 4px; border-radius: 50%; background: var(--signal); opacity: 0.7; }

/* ───────── Hero HUD ─────────
   A tilted radial instrument: a glowing core (the model), five rings of tick
   segments that fade in sequence like a sweep, and 36 pills radiating out.
   Five pills are live findings; the rest are empty slots. Everything is sized
   in --u, a thousandth of the HUD's width, so it scales to any column. */
.hero::after {
  content: "";
  position: absolute;
  inset: 0;
  z-index: 2;
  pointer-events: none;
  opacity: 0.06;
  mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.6 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}
.hero-visual { display: flex; flex-direction: column; gap: 8px; min-width: 0; }
.hud {
  position: relative;
  width: 100%;
  max-width: 100%;
  aspect-ratio: 10 / 7.4;
  container-type: inline-size;
  perspective: 1600px;
  perspective-origin: 50% 30%;
}
.hud-plane {
  --u: 0.1cqi;
  position: absolute;
  left: 50%;
  top: 50%;
  width: 0;
  height: 0;
  transform-style: preserve-3d;
  transform: rotateX(57deg) rotateZ(-18deg);
  animation: hud-wiggle 22s linear infinite;
}
@keyframes hud-wiggle {
  0%, 100% { transform: rotateX(57deg) rotateZ(-18deg); }
  25% { transform: rotateX(59deg) rotateZ(-15deg); }
  50% { transform: rotateX(55deg) rotateZ(-17deg); }
  75% { transform: rotateX(56deg) rotateZ(-21deg); }
}
.core {
  position: absolute;
  width: calc(var(--u) * 36);
  height: calc(var(--u) * 36);
  left: calc(var(--u) * -18);
  top: calc(var(--u) * -18);
  border-radius: 50%;
  background: var(--signal);
  box-shadow: 0 0 calc(var(--u) * 70) calc(var(--u) * 18) rgba(141, 181, 255, 0.5);
}
.tick, .pill {
  position: absolute;
  left: 0;
  top: 0;
  transform-origin: 0 50%;
}
.tick {
  width: calc(var(--u) * var(--w));
  height: calc(var(--u) * var(--h));
  margin-top: calc(var(--u) * var(--h) / -2);
  border-radius: 2px;
  background: var(--c, var(--signal));
  box-shadow: 0 0 calc(var(--u) * 16) var(--c, var(--signal));
  transform: rotate(var(--a)) translateX(calc(var(--u) * var(--r)));
}
.tick.fade { animation: tick-fade var(--t, 5s) var(--d, 0s) ease-in-out infinite; opacity: 0.12; }
@keyframes tick-fade {
  0%, 100% { opacity: 0.08; }
  50% { opacity: 1; }
}
.pill {
  --push: 0;
  width: calc(var(--u) * var(--len));
  height: calc(var(--u) * 22);
  margin-top: calc(var(--u) * -11);
  border-radius: 999px;
  border: max(1px, calc(var(--u) * 3)) solid rgba(141, 181, 255, 0.6);
  box-shadow: 0 0 calc(var(--u) * 24) rgba(141, 181, 255, 0.22);
  transform: rotate(var(--a)) translateX(calc(var(--u) * (var(--r) + var(--push))));
  transition: transform 0.6s var(--ease), background 0.3s var(--ease), box-shadow 0.3s var(--ease), border-color 0.3s var(--ease);
}
.pill.blank { opacity: 0.32; border-color: #3d4b6d; box-shadow: none; pointer-events: none; }
.pill.live { cursor: pointer; }
.pill.hot { border-color: rgba(255, 107, 125, 0.75); box-shadow: 0 0 calc(var(--u) * 24) rgba(255, 107, 125, 0.3); }
.pill.live:hover, .pill.on { --push: 28; background: var(--signal); box-shadow: 0 0 calc(var(--u) * 50) rgba(141, 181, 255, 0.7); }
.pill.hot:hover, .pill.hot.on { background: var(--alert); border-color: var(--alert); box-shadow: 0 0 calc(var(--u) * 50) rgba(255, 107, 125, 0.7); }
.ray {
  position: absolute;
  left: 0;
  top: 0;
  width: calc(var(--u) * 300);
  height: max(1px, calc(var(--u) * 4));
  margin-top: calc(var(--u) * -2);
  transform-origin: 0 50%;
  transform: rotate(var(--ray, 90deg));
  background: linear-gradient(90deg, transparent, var(--signal));
  box-shadow: 0 0 calc(var(--u) * 14) rgba(141, 181, 255, 0.6);
  transition: transform 0.7s var(--ease);
}
.ray.hot { background: linear-gradient(90deg, transparent, var(--alert)); box-shadow: 0 0 calc(var(--u) * 14) rgba(255, 107, 125, 0.6); }

.readout { padding: 18px 20px; }
.readout .panel-body { gap: 14px; }
.ro-top { display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 8px 16px; }
.live { display: inline-flex; align-items: center; gap: 7px; font-family: var(--mono); font-size: 11.5px; color: var(--text-2); }
.live i { width: 6px; height: 6px; border-radius: 50%; background: var(--signal); box-shadow: 0 0 8px var(--signal); }
.ro-main { display: flex; justify-content: space-between; align-items: flex-end; gap: 16px; }
.ro-text { min-width: 0; }
.ro-text b { display: block; font-size: 17px; font-weight: 500; letter-spacing: -0.01em; }
.ro-text small { display: block; margin-top: 2px; font-family: var(--mono); font-size: 11.5px; color: var(--mute); }
.ro-score { text-align: right; flex-shrink: 0; }
.ro-score .k { display: block; font-size: 11px; color: var(--mute); }
.ro-score #roScore { font-family: var(--mono); font-size: 28px; font-variant-numeric: tabular-nums; color: var(--signal); }
.ro-score.hot #roScore { color: var(--alert); }
.ro-chips { display: flex; flex-wrap: wrap; gap: 6px; }
.chip-btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 6px 11px;
  border-radius: 999px;
  border: 1px solid var(--panel-line);
  font-size: 12.5px;
  color: var(--text-2);
  transition: border-color 0.3s var(--ease), color 0.3s var(--ease), background 0.3s var(--ease);
}
.chip-btn em { font-style: normal; font-family: var(--mono); font-size: 11px; color: var(--mute); }
.chip-btn:hover { border-color: var(--signal-50); color: var(--text); }
.chip-btn[aria-selected="true"] { background: var(--signal-10); border-color: var(--signal-50); color: var(--text); }
.chip-btn.hot[aria-selected="true"] { background: rgba(255, 107, 125, 0.1); border-color: rgba(255, 107, 125, 0.55); }
.chip-btn.hot em { color: var(--alert); }
.reader-wrap { max-width: 980px; }

/* platform cards: each workload drawn in the hero's instrument language */
.cap-grid { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 20px; }
.cap-card .panel-body { gap: 20px; height: 100%; }
.cap-card .panel-foot { margin-top: auto; }
.cap-vis {
  border-radius: 12px;
  border: 1px solid var(--panel-line);
  background: radial-gradient(60% 80% at 50% 58%, rgba(43, 86, 201, 0.16), transparent 72%), rgba(255, 255, 255, 0.01);
  overflow: hidden;
}
.cap-vis svg { display: block; width: 100%; height: auto; }
.cap-vis line { stroke-linecap: round; }
.cap-card h3 { font-family: var(--display); font-weight: 300; font-size: clamp(24px, 2.4vw, 30px); letter-spacing: -0.03em; }
.cap-card p { margin: 8px 0 0; color: var(--text-2); font-weight: 300; font-size: 15px; max-width: 52ch; }
.cap-spec { display: flex; justify-content: space-between; gap: 12px; font-family: var(--mono); font-size: 12px; color: var(--mute); }
.cap-spec b { color: var(--signal); font-weight: 500; }
.v-text { font-family: var(--mono); font-size: 10px; letter-spacing: 0.06em; fill: var(--mute); }
.v-text.hi { fill: var(--text); }
.v-text.sig { fill: var(--signal); }
.v-text.alert { fill: var(--alert); }
.v-big { font-family: var(--mono); font-size: 34px; fill: var(--text); }
.v-fade { animation: tick-fade var(--t, 5s) var(--d, 0s) ease-in-out infinite; }
.v-pulse { transform-box: fill-box; transform-origin: center; animation: pulse-ring 2s ease-out infinite; }
.v-dash { animation: dash-run 8s linear infinite; }
@keyframes dash-run { to { stroke-dashoffset: -140; } }
.v-scan { animation: scan-y 5s ease-in-out infinite alternate; }
@keyframes scan-y { from { transform: translateY(-62px); } to { transform: translateY(62px); } }

/* FAQ: question list beside a sticky intro */
.faq-layout {
  display: grid;
  grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.4fr);
  gap: 40px clamp(32px, 6vw, 96px);
  align-items: start;
}
.faq-side {
  position: sticky;
  top: calc(104px + env(safe-area-inset-top, 0px));
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.faq-side h2 { font-size: clamp(34px, 4.4vw, 58px); }
.faq-side p { margin: 0; color: var(--text-2); font-weight: 300; max-width: 40ch; }
.faq-side .btn-outline { width: fit-content; padding-inline: 22px; }
@media (max-width: 860px) {
  .cap-grid, .faq-layout { grid-template-columns: minmax(0, 1fr); }
  .faq-side { position: static; }
}

/* ───────── Instrument (scan reader + chart panels) ───────── */
.instrument {
  background: linear-gradient(180deg, rgba(18, 25, 51, 0.82), rgba(12, 17, 33, 0.94));
  border: 1px solid var(--line-2);
  border-radius: 16px;
  padding: 12px;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.05), 0 50px 100px -50px rgba(0, 0, 0, 0.95);
  min-width: 0;
}
.inst-bar {
  display: flex; align-items: center; gap: 8px; flex-wrap: wrap;
  padding: 4px 4px 12px;
  font-family: var(--mono); font-size: 11.5px; color: var(--mute);
}
.inst-bar .chip { padding: 5px 10px; border: 1px solid var(--line); border-radius: 6px; }
.inst-bar .spacer { flex: 1; }
.inst-bar .live { display: inline-flex; align-items: center; gap: 7px; color: var(--text-2); }
.inst-bar .live i { width: 6px; height: 6px; border-radius: 50%; background: var(--signal); box-shadow: 0 0 8px var(--signal); }

.power { display: inline-flex; align-items: center; gap: 8px; cursor: pointer; }
.power input { position: absolute; opacity: 0; pointer-events: none; }
.power .sw {
  width: 30px; height: 30px; border-radius: 50%;
  display: grid; place-items: center;
  background: #22283c;
  border: 1.5px solid #4f5876;
  box-shadow: 0 0 3px #020202 inset;
  transition: all 0.35s var(--ease);
}
.power .sw svg { width: 13px; height: 13px; }
.power .sw path { fill: #8e96b3; transition: fill 0.35s var(--ease); }
.power input:checked + .sw {
  background: #3f6f8c;
  border-color: #fff;
  box-shadow: inset 0 0 1px var(--glow), inset 0 0 8px var(--glow), 0 0 14px var(--glow-soft);
}
.power input:checked + .sw path { fill: #fff; }
.power input:focus-visible + .sw { outline: 2px solid var(--signal); outline-offset: 3px; }

.scan-stage {
  position: relative;
  border-radius: 10px;
  overflow: hidden;
  background: #05070d;
  aspect-ratio: 16 / 10;
  max-width: 100%;
  touch-action: none;
  cursor: ew-resize;
}
.scan-stage svg { position: absolute; inset: 0; width: 100%; height: 100%; }
.scan-ai { clip-path: inset(0 0 0 var(--split, 50%)); }
.scan-split {
  position: absolute; top: 0; bottom: 0; left: var(--split, 50%);
  width: 1px; background: rgba(230, 240, 255, 0.85);
  box-shadow: 0 0 12px rgba(141, 181, 255, 0.8);
  pointer-events: none;
}
.scan-handle {
  position: absolute; top: 50%; left: var(--split, 50%);
  translate: -50% -50%;
  width: 34px; height: 34px; border-radius: 50%;
  background: var(--ink-3);
  border: 1px solid rgba(190, 210, 255, 0.5);
  display: grid; place-items: center;
  color: #fff;
  cursor: grab;
}
.scan-handle svg { position: static; width: 15px; height: 15px; }
.scan-stage.off .scan-handle, .scan-stage.off .scan-split { opacity: 0; }
.scan-cap {
  position: absolute; bottom: 10px;
  font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.06em; text-transform: uppercase;
  color: rgba(200, 208, 230, 0.7); pointer-events: none;
}
.scan-cap.l { left: 12px; }
.scan-cap.r { right: 12px; color: var(--signal); }

.findings { list-style: none; margin: 0; padding: 14px 6px 4px; display: grid; gap: 10px; }
.findings li {
  display: grid;
  grid-template-columns: minmax(0, 1.4fr) minmax(60px, 1fr) 3.2em;
  align-items: center;
  gap: 14px;
  font-size: 13px;
}
.findings .name { color: var(--text); min-width: 0; }
.findings .name small { display: block; font-family: var(--mono); font-size: 11px; color: var(--mute); }
.meter { height: 3px; border-radius: 3px; background: var(--line); overflow: hidden; }
.meter i { display: block; height: 100%; background: var(--signal); border-radius: inherit; }
.findings .low .meter i { background: #4a5372; }
.findings .pct { font-family: var(--mono); font-size: 12px; text-align: right; color: var(--text-2); font-variant-numeric: tabular-nums; }
.inst-foot {
  margin: 12px 6px 4px; padding-top: 12px;
  border-top: 1px solid var(--line);
  font-size: 12px; color: var(--mute);
}

/* ───────── Partners ───────── */
.partners {
  display: flex; flex-wrap: wrap; align-items: center; gap: 18px 40px;
  padding-block: 28px;
  border-top: 1px solid var(--line);
  border-bottom: 1px solid var(--line);
}
.partners .label { flex-basis: 100%; }
.partner { display: inline-flex; align-items: center; gap: 8px; font-size: 15px; font-weight: 500; color: var(--mute); letter-spacing: -0.01em; }
.partner svg { width: 16px; height: 16px; opacity: 0.8; }

/* ───────── Sections ───────── */
.section { padding-block: var(--section) 0; }
.sec-head {
  display: grid;
  grid-template-columns: minmax(0, 1.2fr) minmax(0, 1fr);
  gap: 20px 48px;
  align-items: end;
  margin-bottom: clamp(40px, 5vw, 64px);
}
.sec-head .label { grid-column: 1 / -1; }
.sec-head h2 { font-size: clamp(34px, 4.4vw, 58px); }
.sec-head p { margin: 0; color: var(--text-2); max-width: 46ch; font-weight: 300; }

/* stats */
.stats { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 32px; }
.stat { border-top: 1px solid var(--line-2); padding-top: 22px; }
.stat .val { font-family: var(--display); font-weight: 200; font-size: clamp(54px, 6vw, 84px); line-height: 0.9; letter-spacing: -0.02em; font-variant-numeric: tabular-nums; }
.stat .val small { font-size: 0.4em; color: var(--signal); margin-left: 4px; letter-spacing: 0; }
.stat .val sup { font-family: var(--mono); font-size: 12px; color: var(--mute); vertical-align: top; margin-left: 4px; }
.stat .val sup a:hover { color: var(--signal); }
.stat h3 { margin-top: 18px; font-size: 15px; font-weight: 500; }
.stat p { margin: 6px 0 0; font-size: 13.5px; color: var(--mute); }
.notes {
  margin: 48px 0 0; padding: 22px 0 0;
  border-top: 1px solid var(--line);
  list-style: none;
  display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 8px 40px;
  font-family: var(--mono); font-size: 11.5px; line-height: 1.6; color: var(--mute);
}
.notes li { display: grid; grid-template-columns: 1.6em minmax(0, 1fr); }
.notes li:target { color: var(--text-2); }

/* capabilities */
.caps { border-top: 1px solid var(--line-2); }
.cap {
  display: grid;
  grid-template-columns: minmax(0, 0.9fr) minmax(0, 1.5fr) minmax(0, 0.7fr);
  gap: 16px 48px;
  padding-block: 30px;
  border-bottom: 1px solid var(--line);
  align-items: baseline;
}
.cap h3 { font-family: var(--display); font-weight: 300; font-size: clamp(26px, 2.6vw, 34px); letter-spacing: -0.01em; }
.cap p { margin: 0; color: var(--text-2); font-weight: 300; max-width: 52ch; }
.cap .spec { font-family: var(--mono); font-size: 12px; color: var(--mute); text-align: right; line-height: 1.7; }
.cap .spec b { color: var(--signal); font-weight: 500; display: block; }

/* predictive */
.predict { display: grid; grid-template-columns: minmax(0, 1.35fr) minmax(0, 1fr); gap: clamp(24px, 3vw, 48px); align-items: start; }
/* ───────── Panel component ───────── */
.panel {
  position: relative;
  overflow: hidden;
  min-width: 0;
  background: var(--panel);
  border: 1px solid var(--panel-line);
  border-radius: var(--radius);
  padding: clamp(20px, 2.4vw, 26px);
  box-shadow: 0 40px 90px -50px rgba(0, 0, 0, 1);
}
.panel::before {
  content: "";
  position: absolute;
  top: -50%;
  left: 50%;
  width: 18rem;
  height: 18rem;
  transform: translateX(-50%);
  border-radius: 50%;
  background: var(--signal-10);
  filter: blur(64px);
  transition: background 0.7s var(--ease);
  pointer-events: none;
}
.panel:hover::before { background: var(--signal-16); }
.panel-body { position: relative; display: flex; flex-direction: column; gap: 20px; }
.panel-head {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 14px 20px;
  padding-bottom: 20px;
  border-bottom: 1px solid var(--panel-line);
}
.panel-title { display: flex; align-items: center; gap: 12px; min-width: 0; }
.panel-title b { display: block; font-size: 15px; font-weight: 600; color: var(--text); }
.panel-title small { display: block; font-size: 12px; color: var(--mute); }
.icon-tile {
  width: 36px; height: 36px;
  flex-shrink: 0;
  border-radius: 10px;
  background: var(--signal-10);
  color: var(--signal);
  display: grid;
  place-items: center;
}
.icon-tile svg { width: 20px; height: 20px; }
.kpis { display: flex; }
.kpi { flex: 1; min-width: 0; padding-inline: 24px; }
.kpi:first-child { padding-left: 0; }
.kpi:last-child { padding-right: 0; }
.kpi + .kpi { border-left: 1px solid var(--panel-line); }
.kpi .k { font-size: 12px; font-weight: 500; color: var(--mute); }
.kpi .v { font-size: 22px; font-weight: 600; color: var(--text); font-variant-numeric: tabular-nums; letter-spacing: -0.01em; }
.kpi .d { margin-top: 2px; font-size: 12px; font-weight: 500; font-variant-numeric: tabular-nums; }
.d.bad { color: var(--alert); }
.d.good { color: var(--ok); }
.d.flat { color: var(--mute); }
.panel-foot { padding-top: 20px; border-top: 1px solid var(--panel-line); }
.btn-outline {
  width: 100%;
  justify-content: center;
  border-radius: 10px;
  padding: 10px 16px;
  font-size: 14px;
  border: 1px solid var(--signal-50);
  color: var(--signal);
  transition: background 0.3s var(--ease), color 0.3s var(--ease);
}
.btn-outline:hover, .btn-outline:focus-visible { background: var(--signal); color: var(--ink); }
@keyframes pulse-ring {
  0% { transform: scale(1); opacity: 0.5; }
  100% { transform: scale(2.8); opacity: 0; }
}

.tabs { display: flex; flex-wrap: wrap; gap: 4px; padding: 4px; border: 1px solid var(--line); border-radius: 999px; width: fit-content; max-width: 100%; }
.tab { padding: 7px 14px; border-radius: 999px; font-size: 13px; color: var(--mute); transition: background 0.3s var(--ease), color 0.3s var(--ease); }
.tab:hover { color: var(--text); }
.tab[aria-selected="true"] { background: var(--ink-3); color: var(--text); box-shadow: inset 0 0 0 1px var(--line-2); }
.chart { width: 100%; height: auto; overflow: visible; }
.chart .grid-line { stroke: var(--panel-line); }
.chart .axis-label { font-family: var(--mono); font-size: 10.5px; fill: var(--mute); }
.chart .area { fill: url(#chartFill); }
.chart .band { fill: rgba(141, 181, 255, 0.07); }
.chart .line { fill: none; stroke: var(--signal); stroke-width: 2; stroke-linecap: round; stroke-linejoin: round; }
.chart .marker { stroke: var(--alert); stroke-dasharray: 3 4; stroke-width: 1; opacity: 0.7; }
.chart .thr-label { font-family: var(--mono); font-size: 10.5px; fill: var(--alert); }
.chart .dot { fill: var(--signal); filter: drop-shadow(0 0 6px rgba(141, 181, 255, 0.7)); }
.chart .ring { fill: var(--signal); opacity: 0.25; transform-box: fill-box; transform-origin: center; animation: pulse-ring 2s ease-out infinite; }
.chart .hot .dot { fill: var(--alert); filter: drop-shadow(0 0 6px rgba(255, 107, 125, 0.7)); }
.chart .hot .ring { fill: var(--alert); }
.legend { display: flex; flex-wrap: wrap; gap: 8px 18px; font-family: var(--mono); font-size: 11px; color: var(--mute); }
.legend span { display: inline-flex; align-items: center; gap: 7px; }
.legend i { display: inline-block; width: 12px; height: 2px; background: var(--signal); }
.legend i.band { height: 8px; background: rgba(141, 181, 255, 0.25); }
.legend i.thr { background: repeating-linear-gradient(90deg, var(--alert) 0 3px, transparent 3px 6px); }
.legend i.seg { background: #9cc0ff; }
.legend i.lesion { background: repeating-linear-gradient(90deg, #ff8a6a 0 4px, transparent 4px 7px); }
.legend i.heat { height: 8px; background: linear-gradient(90deg, rgba(255, 107, 90, 0.85), rgba(240, 182, 78, 0.25)); }
.panel-head .power { font-family: var(--mono); font-size: 12px; color: var(--text-2); }
.kpi .v { white-space: nowrap; }
.chart-caption { margin: 0; font-size: 13px; color: var(--text-2); }
.chart-block { display: flex; flex-direction: column; gap: 12px; }

.patients { list-style: none; margin: 0; padding: 0; border-top: 1px solid var(--line-2); }
.patient { padding-block: 22px; border-bottom: 1px solid var(--line); display: grid; gap: 10px; }
.patient .top { display: flex; justify-content: space-between; align-items: baseline; gap: 12px; }
.patient .who { font-size: 15px; font-weight: 500; }
.patient .who small { display: block; font-family: var(--mono); font-size: 11.5px; color: var(--mute); font-weight: 400; margin-top: 2px; }
.patient .score { font-family: var(--mono); font-size: 20px; font-variant-numeric: tabular-nums; }
.patient .state {
  font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.06em; text-transform: uppercase;
  padding: 3px 8px; border-radius: 4px; border: 1px solid currentColor; margin-right: 10px;
  vertical-align: 3px;
}
.patient.high .score, .patient.high .state { color: var(--alert); }
.patient.mid .score, .patient.mid .state { color: var(--warn); }
.patient.low .score, .patient.low .state { color: var(--ok); }
.patient.high .meter i { background: var(--alert); }
.patient.mid .meter i { background: var(--warn); }
.patient.low .meter i { background: var(--ok); }
.patient p { margin: 0; font-size: 13.5px; color: var(--mute); }
.patient p b { color: var(--text-2); font-weight: 500; }

/* steps */
.steps { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 32px; }
.step { border-top: 1px solid var(--line-2); padding-top: 22px; display: flex; flex-direction: column; gap: 12px; }
.step .when { font-family: var(--mono); font-size: 12px; color: var(--signal); }
.step h3 { font-family: var(--display); font-weight: 300; font-size: 32px; }
.step p { margin: 0; color: var(--text-2); font-weight: 300; font-size: 15px; }
.tags { display: flex; flex-wrap: wrap; gap: 6px; margin-top: 4px; }
.tags span { font-family: var(--mono); font-size: 11px; color: var(--mute); border: 1px solid var(--line); border-radius: 4px; padding: 3px 8px; }

/* quote */
.quote { padding-block: var(--section) 0; }
.quote blockquote {
  margin: 0;
  font-family: var(--display);
  font-weight: 300;
  font-size: clamp(32px, 4.2vw, 58px);
  line-height: 1.08;
  letter-spacing: -0.03em;
  max-width: 22ch;
  text-wrap: balance;
}
.quote blockquote em { color: var(--signal); }
.quote figcaption { margin-top: 30px; display: flex; gap: 14px; align-items: center; font-size: 14px; }
.quote figcaption::before { content: ""; width: 32px; height: 1px; background: var(--line-2); }
.quote figcaption span { color: var(--mute); }

/* governance */
.gov { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 1fr); gap: clamp(24px, 4vw, 64px); align-items: start; }
.reg h3 { font-family: var(--display); font-weight: 300; font-size: 30px; }
.reg p { margin: 0; color: var(--text-2); font-weight: 300; font-size: 15px; }
.reg dl { margin: 6px 0 0; display: grid; grid-template-columns: auto minmax(0, 1fr); gap: 10px 22px; font-size: 13.5px; }
.reg dt { font-family: var(--mono); font-size: 11.5px; color: var(--mute); padding-top: 2px; }
.reg dd { margin: 0; color: var(--text); }
.placeholder { font-family: var(--mono); font-size: 11px; color: var(--warn); }
.checks { list-style: none; margin: 0; padding: 0; border-top: 1px solid var(--line-2); }
.checks li {
  display: grid; grid-template-columns: 22px minmax(0, 1fr) auto; gap: 14px; align-items: baseline;
  padding-block: 18px; border-bottom: 1px solid var(--line);
}
.checks svg { width: 15px; height: 15px; color: var(--signal); transform: translateY(2px); }
.checks b { font-weight: 500; }
.checks span { font-family: var(--mono); font-size: 11.5px; color: var(--mute); text-align: right; }

/* faq */
.faq { border-top: 1px solid var(--line-2); min-width: 0; }
.qa { border-bottom: 1px solid var(--line); }
.qa button {
  width: 100%; display: flex; justify-content: space-between; align-items: center; gap: 20px;
  padding: 24px 0; text-align: left;
  font-size: clamp(17px, 1.6vw, 20px); font-weight: 400; letter-spacing: -0.01em;
}
.qa .sign { width: 14px; height: 14px; color: var(--mute); flex-shrink: 0; transition: transform 0.4s var(--ease), color 0.3s var(--ease); }
.qa[data-open="true"] .sign { transform: rotate(45deg); color: var(--signal); }
.qa .qa-panel { overflow: hidden; height: 0; transition: height 0.45s var(--ease); }
.qa .qa-panel p { margin: 0; padding: 0 0 26px; max-width: 64ch; color: var(--text-2); font-weight: 300; }

/* cta: the closing stage. A light-catching rim, a slow aurora, a perspective
   floor drifting toward the viewer, a spotlight that follows the pointer, and
   the pilot itself laid out as a seven-week plan beside the pitch. */
.cta {
  --mx: 78%;
  --my: 18%;
  margin-top: var(--section);
  position: relative;
  isolation: isolate;
  overflow: hidden;
  border-radius: 24px;
  padding: clamp(28px, 5vw, 72px);
  background: #04060c;
  display: grid;
  grid-template-columns: minmax(0, 1.1fr) minmax(0, 0.9fr);
  gap: 40px clamp(32px, 5vw, 80px);
  align-items: center;
  box-shadow: 0 70px 140px -70px rgba(43, 86, 201, 0.6);
}
.cta::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: 2;
  border-radius: inherit;
  padding: 1px;
  background: linear-gradient(140deg, rgba(176, 222, 255, 0.7), rgba(141, 181, 255, 0.14) 28%, rgba(141, 181, 255, 0.04) 55%, rgba(141, 181, 255, 0.12) 78%, rgba(255, 107, 125, 0.45));
  -webkit-mask: linear-gradient(#000 0 0) content-box, linear-gradient(#000 0 0);
  -webkit-mask-composite: xor;
  mask: linear-gradient(#000 0 0) content-box exclude, linear-gradient(#000 0 0);
  pointer-events: none;
}
.cta-fx { position: absolute; inset: 0; z-index: -1; pointer-events: none; overflow: hidden; border-radius: inherit; }
.cta-fx .aurora {
  position: absolute;
  inset: -20%;
  background:
    radial-gradient(38% 48% at 84% 16%, rgba(43, 86, 201, 0.5), transparent 70%),
    radial-gradient(30% 40% at 14% 100%, rgba(141, 181, 255, 0.16), transparent 70%),
    radial-gradient(20% 28% at 98% 92%, rgba(255, 107, 125, 0.12), transparent 70%);
  animation: aurora-drift 18s ease-in-out infinite alternate;
}
@keyframes aurora-drift { to { transform: translate3d(-4%, 3%, 0) scale(1.06); } }
.cta-fx .floor {
  position: absolute;
  left: -30%;
  right: -30%;
  bottom: -14%;
  height: 72%;
  transform: perspective(560px) rotateX(66deg);
  transform-origin: 50% 100%;
  background-image:
    linear-gradient(rgba(141, 181, 255, 0.32) 1px, transparent 1px),
    linear-gradient(90deg, rgba(141, 181, 255, 0.32) 1px, transparent 1px);
  background-size: 52px 52px;
  animation: floor-run 7s linear infinite;
}
@keyframes floor-run { to { background-position: 0 52px, 0 0; } }
.cta-fx .spot { position: absolute; inset: 0; background: radial-gradient(460px circle at var(--mx) var(--my), rgba(141, 181, 255, 0.14), transparent 60%); }
.cta-fx .grain { position: absolute; inset: 0; opacity: 0.06; mix-blend-mode: overlay; background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.6 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>"); }
.cta-copy { display: flex; flex-direction: column; gap: 22px; min-width: 0; }
.cta h2 { font-size: clamp(38px, 5vw, 72px); max-width: 13ch; }
.cta-copy > p { margin: 0; color: var(--text-2); font-weight: 300; font-size: 17px; max-width: 44ch; }
.cta-assure { list-style: none; margin: 6px 0 0; padding: 20px 0 0; border-top: 1px solid var(--line); display: grid; gap: 10px; font-size: 14px; color: var(--text-2); }
.cta-assure li { display: flex; gap: 10px; align-items: baseline; }
.cta-assure svg { width: 14px; height: 14px; color: var(--signal); flex-shrink: 0; transform: translateY(2px); }
.cta-plan { background: rgba(5, 7, 13, 0.74); backdrop-filter: blur(14px); -webkit-backdrop-filter: blur(14px); }
.plan-track { position: relative; padding-top: 22px; }
.track { display: grid; grid-template-columns: repeat(28, minmax(0, 1fr)); gap: 3px; align-items: end; height: 24px; }
.track i { height: 12px; border-radius: 2px; background: var(--signal); }
.track i.wk { height: 22px; }
.track i.c { opacity: 0.32; }
.track i.s { animation: tick-glow 3.2s ease-in-out infinite; animation-delay: calc(var(--n) * 90ms); }
.track i.l { background: var(--glow); box-shadow: 0 0 10px rgba(176, 222, 255, 0.8); }
@keyframes tick-glow { 0%, 100% { opacity: 0.5; } 50% { opacity: 1; } }
.track-labels { display: grid; grid-template-columns: repeat(7, minmax(0, 1fr)); margin-top: 8px; font-family: var(--mono); font-size: 10.5px; color: var(--mute); }
.gate { position: absolute; top: 14px; bottom: 20px; left: calc(600% / 7 - 1.5px); width: 1px; background: #fff; box-shadow: 0 0 8px rgba(255, 255, 255, 0.8); }
.gate span { position: absolute; top: -16px; left: 50%; transform: translateX(-50%); font-family: var(--mono); font-size: 10.5px; color: var(--text); white-space: nowrap; }
.phases { list-style: none; margin: 0; padding: 0; }
.phase { display: grid; grid-template-columns: 4.4em minmax(0, 1fr); gap: 2px 14px; padding-block: 11px; border-top: 1px solid var(--panel-line); }
.phase .w { font-family: var(--mono); font-size: 11.5px; color: var(--signal); padding-top: 2px; }
.phase b { font-size: 14.5px; font-weight: 500; }
.phase small { grid-column: 2; font-size: 12.5px; color: var(--mute); }


/* footer */
.footer {
  margin-top: clamp(72px, 9vw, 120px);
  border-top: 1px solid var(--line);
  padding-block: 48px 28px;
  display: grid;
  grid-template-columns: minmax(0, 1.4fr) repeat(3, minmax(0, 1fr));
  gap: 32px;
}
.footer p { margin: 14px 0 0; font-size: 13.5px; color: var(--mute); max-width: 34ch; }
.fcol h4 { margin: 0 0 14px; }
.fcol a { display: block; padding: 5px 0; font-size: 14px; color: var(--text-2); transition: color 0.3s var(--ease); }
.fcol a:hover { color: var(--signal); }
.legal {
  border-top: 1px solid var(--line);
  padding-block: 20px 40px;
  display: flex; flex-wrap: wrap; justify-content: space-between; gap: 12px 24px;
  font-family: var(--mono); font-size: 11px; color: var(--mute);
}
.legal .note { max-width: 70ch; }

/* ───────── Responsive ───────── */
@media (max-width: 980px) {
  .hero-grid, .predict, .gov { grid-template-columns: minmax(0, 1fr); }
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .footer { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .irid { right: -30%; top: 20%; }
}
@media (max-width: 860px) {
  .sec-head { grid-template-columns: minmax(0, 1fr); }
  .cap { grid-template-columns: minmax(0, 1fr); gap: 10px; }
  .cap .spec { text-align: left; }
  .steps { grid-template-columns: minmax(0, 1fr); }
  .cta { grid-template-columns: minmax(0, 1fr); }
  .notes { grid-template-columns: minmax(0, 1fr); }
}
@media (max-width: 520px) {
  .stats, .footer { grid-template-columns: minmax(0, 1fr); }
  .scan-stage { aspect-ratio: 4 / 3; }
  .findings li { grid-template-columns: minmax(0, 1fr) 3.2em; }
  .findings .meter { display: none; }
  .kpi { padding-inline: 12px; }
  .kpi .v { font-size: 18px; }
  .checks li { grid-template-columns: 22px minmax(0, 1fr); }
  .checks span { grid-column: 2; text-align: left; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after { transition-duration: 0.001ms !important; animation: none !important; }
  .tick.fade { opacity: 0.55; }
}
</style>

<div class="page">

<header class="header" data-open="false" data-section="nav">
  <div class="header-bar">
    <div class="wrap">
      <a class="logo" href="#top" aria-label="SmartCare Solutions home">
        <span class="logo-mark" aria-hidden="true">
          <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round"><path d="M4 12h6m4 0h6M12 4v6m0 4v6" /></svg>
        </span>
        SmartCare <span>Solutions</span>
      </a>
      <span class="header-status"><i aria-hidden="true"></i>Live at 6 sites · Model v4.2</span>
      <div class="header-actions">
        <a class="btn btn-primary" href="#start">Book a pilot</a>
        <button class="menu-btn" id="menuBtn" aria-expanded="false" aria-controls="menu">
          <span class="lbl">Menu</span>
          <span class="burger" aria-hidden="true"><i></i><i></i></span>
        </button>
      </div>
    </div>
  </div>
</header>

<div class="menu" id="menu" data-section="menu" role="dialog" aria-modal="true" aria-label="Site menu" inert>
  <div class="menu-bg" aria-hidden="true">
    <div class="menu-rings">
      <svg viewBox="0 0 1000 1000">
        <circle cx="500" cy="500" r="480" stroke="rgba(141,181,255,0.16)" stroke-width="1" />
        <circle cx="500" cy="500" r="440" stroke="rgba(141,181,255,0.32)" stroke-width="10" stroke-dasharray="1 13" />
        <circle cx="500" cy="500" r="380" stroke="rgba(169,227,255,0.22)" stroke-width="3" stroke-dasharray="60 14" />
        <circle cx="500" cy="500" r="380" stroke="rgba(255,107,125,0.7)" stroke-width="3" stroke-dasharray="74 2314" />
        <circle cx="500" cy="500" r="300" stroke="rgba(141,181,255,0.14)" stroke-width="1" />
        <circle cx="500" cy="500" r="262" stroke="rgba(141,181,255,0.28)" stroke-width="6" stroke-dasharray="2 7" />
        <circle cx="500" cy="500" r="160" stroke="rgba(141,181,255,0.18)" stroke-width="1" />
        <circle cx="500" cy="500" r="18" style="fill: rgba(141,181,255,0.55)" />
      </svg>
    </div>
  </div>

  <div class="menu-scroll">
    <div class="wrap menu-grid">
      <nav class="menu-index" aria-label="Sections">
        <span class="label" data-i style="--i:0">Index</span>
        <ul id="menuLinks">
          <li><a class="m-link" href="#capabilities" data-key="reader" style="--i:1"><span class="mask"><span class="t">Image analysis</span></span><span class="meta"><span>1.8 s read</span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg></span></a></li>
          <li><a class="m-link" href="#predictive" data-key="predictive" style="--i:2"><span class="mask"><span class="t">Predictive risk</span></span><span class="meta"><span>6 h lead time</span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg></span></a></li>
          <li><a class="m-link" href="#outcomes" data-key="outcomes" style="--i:3"><span class="mask"><span class="t">Outcomes</span></span><span class="meta"><span>97.4% agreement</span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg></span></a></li>
          <li><a class="m-link" href="#governance" data-key="governance" style="--i:4"><span class="mask"><span class="t">Governance</span></span><span class="meta"><span>SOC 2 Type II</span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg></span></a></li>
        </ul>
      </nav>

      <aside class="panel menu-preview" id="menuPreview" data-i style="--i:5" aria-live="polite">
        <div class="panel-body">
          <div class="k-line"><span class="label" id="pvLabel">Current release</span><span class="live"><i></i>v4.2</span></div>
          <h3 id="pvTitle">Pre-reads in 1.8 seconds</h3>
          <p id="pvText">Median model read across MR, CT and X-ray, with every finding traced to the pixels behind it.</p>
          <div class="kpis">
            <div class="kpi"><div class="k" id="pvK1">Read time</div><div class="v" id="pvV1">1.8 s</div></div>
            <div class="kpi"><div class="k" id="pvK2">Agreement</div><div class="v" id="pvV2">97.4%</div></div>
          </div>
          <div class="panel-foot"><a class="btn btn-outline" id="pvCta" href="#start">Book a clinical pilot</a></div>
        </div>
      </aside>
    </div>

    <div class="wrap">
      <div class="menu-bottom">
        <div class="col" data-i style="--i:6">
          <span class="label">Platform</span>
          <a href="#capabilities">Image analysis</a>
          <a href="#capabilities">Predictive risk</a>
          <a href="#capabilities">Treatment planning</a>
          <a href="#capabilities">Research cohorts</a>
        </div>
        <div class="col" data-i style="--i:7">
          <span class="label">Company</span>
          <a href="#workflow">How a pilot runs</a>
          <a href="#faq">FAQ</a>
          <a href="#start">Contact</a>
        </div>
        <div class="col" data-i style="--i:8">
          <span class="label">Assurance</span>
          <p>No PHI leaves your VPC<br />SOC 2 Type II · HIPAA BAA<br />Full audit trail</p>
        </div>
        <div class="col" data-i style="--i:9">
          <span class="label">Status</span>
          <p>Live at 6 sites<br />Model v4.2 · 1.8 s median<br />Esc to close</p>
        </div>
      </div>
    </div>
  </div>
</div>

<main id="top">

  <!-- ───── Hero ───── -->
  <section class="hero" data-section="hero">
    <div class="hero-glow" aria-hidden="true"><canvas class="irid" id="iridCanvas"></canvas></div>
    <div class="wrap hero-grid">
      <div class="hero-copy">
        <span class="label">Clinical AI for imaging and risk</span>
        <h1 class="display">Know which <em>twelve studies</em> to open first.</h1>
        <p class="lede">SmartCare pre-reads every study and every new observation, ranks what needs a clinician now, and shows the evidence behind each flag. A clinician signs every report.</p>
        <div class="hero-actions">
          <a class="btn btn-primary" href="#start">
            Book a clinical pilot
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg>
          </a>
          <a class="btn btn-quiet" href="#predictive">See the risk chart</a>
        </div>
        <div class="hero-meta">
          <span>No PHI leaves your VPC</span>
          <span>SOC 2 Type II</span>
          <span>HIPAA BAA available</span>
        </div>
      </div>

      <div class="hero-visual">
        <div class="hud" id="hud" aria-hidden="true">
          <div class="hud-plane">
            <div class="ray" id="hudRay"></div>
            <div class="core"></div>
            <div id="hudRings"></div>
          </div>
        </div>
        <div class="panel readout">
          <div class="panel-body">
            <div class="ro-top">
              <span class="label">Pre-read · MR AX T2 FLAIR</span>
              <span class="live"><i></i>Model v4.2 · 1.8 s</span>
            </div>
            <div class="ro-main" aria-live="polite">
              <div class="ro-text"><b id="roName">Focal FLAIR hyperintensity</b><small id="roNote">Right frontal · 12.4 mm · prior from 2025-11-04 queued</small></div>
              <div class="ro-score"><span class="k">Confidence</span><span id="roScore">0.93</span></div>
            </div>
            <div class="ro-chips" id="roChips" role="tablist" aria-label="Findings in this study"></div>
          </div>
        </div>
      </div>
    </div>

    <div class="wrap">
      <div class="partners">
        <span class="label">In production at</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><path d="M4 12h16M12 4v16" /></svg>Northvale Health</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><circle cx="12" cy="12" r="8" /><path d="M12 7v10" stroke-linecap="round" /></svg>Meridian Clinics</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><rect x="4" y="4" width="16" height="16" rx="4" /></svg>Halden Institute</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M4 16l6-8 4 5 6-7" /></svg>Cortis Radiology</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8"><path d="M12 4l8 8-8 8-8-8z" /></svg>Provia Care Group</span>
        <span class="partner"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"><path d="M6 18V8M12 18V5M18 18v-7" /></svg>Aldermoor Trust</span>
      </div>
    </div>
  </section>

  <!-- ───── Outcomes ───── -->
  <section class="section" id="outcomes" data-section="metrics">
    <div class="wrap">
      <div class="sec-head">
        <span class="label">Outcomes · 18-month rollout, six sites</span>
        <h2 class="display">Signal you can act on, in the time you <em>actually have</em>.</h2>
        <p>Each figure below is footnoted with its method and links to an auditable model card.</p>
      </div>
      <div class="stats">
        <div class="stat">
          <div class="val">97.4<small>%</small><sup><a href="#n1">1</a></sup></div>
          <h3>Detection agreement</h3>
          <p>Against a three-radiologist consensus read.</p>
        </div>
        <div class="stat">
          <div class="val">12<small>min</small><sup><a href="#n2">2</a></sup></div>
          <h3>Median read time saved</h3>
          <p>Urgent studies move to the top of the worklist.</p>
        </div>
        <div class="stat">
          <div class="val">34<small>%</small><sup><a href="#n3">3</a></sup></div>
          <h3>Fewer 30-day readmissions</h3>
          <p>In cohorts flagged high-risk at discharge.</p>
        </div>
        <div class="stat">
          <div class="val">6<small>sites</small><sup><a href="#n4">4</a></sup></div>
          <h3>Live in production</h3>
          <p>Academic centres, clinics and a national trust.</p>
        </div>
      </div>
      <ol class="notes">
        <li id="n1"><span>1</span><span>41,800 studies across six sites, Jan 2025 to Jun 2026. Consensus of three board-certified radiologists, blinded to model output.</span></li>
        <li id="n2"><span>2</span><span>Median change in time-to-first-read for studies flagged urgent, compared with the 12 months before deployment.</span></li>
        <li id="n3"><span>3</span><span>30-day all-cause readmissions in high-risk cohorts, against a matched pre-deployment period.</span></li>
        <li id="n4"><span>4</span><span>Two academic centres, three outpatient clinics, one national trust. All figures on this page are synthetic.</span></li>
      </ol>
    </div>
  </section>

  <!-- ───── Platform ───── -->
  <section class="section" id="capabilities" data-section="features">
    <div class="wrap">
      <div class="sec-head">
        <span class="label">Platform</span>
        <h2 class="display">One platform, four clinical <em>workloads</em>.</h2>
        <p>Every model ships with its own evaluation set, a drift monitor and a plain-language explanation for the clinician reading it.</p>
      </div>
      <div class="cap-grid">
        <article class="panel cap-card">
          <div class="panel-body">
            <div class="cap-vis"><svg data-vis="imaging" viewBox="0 0 400 220" role="img" aria-label="Stack of MRI slices with a scan plane passing through; with a lesion marker travelling on the scan plane"></svg></div>
            <div><h3>Image analysis</h3><p>Segmentation and detection across MRI, CT, X-ray and digital pathology. Every finding traces back to the voxels that produced it.</p></div>
            <div class="panel-foot cap-spec"><b>4 modalities</b><span>DICOM native</span></div>
          </div>
        </article>
        <article class="panel cap-card">
          <div class="panel-body">
            <div class="cap-vis"><svg data-vis="risk" viewBox="0 0 400 220" role="img" aria-label="Hourly sepsis risk over 12 hours, rising to 0.81"></svg></div>
            <div><h3>Predictive risk</h3><p>Deterioration, sepsis and readmission risk, recalculated on every new observation instead of once a shift.</p></div>
            <div class="panel-foot cap-spec"><b>6 h lead time</b><span>HL7 v2 · FHIR streaming</span></div>
          </div>
        </article>
        <article class="panel cap-card">
          <div class="panel-body">
            <div class="cap-vis"><svg data-vis="plan" viewBox="0 0 400 220" role="img" aria-label="Patient branching to four treatment options with fit meters; the NSAID option is flagged for a heart failure interaction"></svg></div>
            <div><h3>Treatment planning</h3><p>Options ranked against the patient's own history, comorbidities and genomic signals, with the trade-offs shown.</p></div>
            <div class="panel-foot cap-spec"><b>Guideline-aware</b><span>Explainable ranking</span></div>
          </div>
        </article>
        <article class="panel cap-card">
          <div class="panel-body">
            <div class="cap-vis"><svg data-vis="cohort" viewBox="0 0 400 220" role="img" aria-label="Grid of studies on a tilted plane with the queried cohort raised as pins"></svg></div>
            <div><h3>Research cohorts</h3><p>Build a de-identified cohort from a plain-language query and export it to your notebook with provenance intact.</p></div>
            <div class="panel-foot cap-spec"><b>De-identified</b><span>One-click export</span></div>
          </div>
        </article>
      </div>
    </div>
  </section>

  <!-- ───── Predictive ───── -->
  <section class="section" id="predictive" data-section="predictive">
    <div class="wrap">
      <div class="sec-head">
        <span class="label">Predictive risk</span>
        <h2 class="display">Risk that moves <em>before</em> the patient does.</h2>
        <p>Scores recompute on every observation. Pick a cohort to see the last 12 hours and where the alert threshold sits.</p>
      </div>
      <div class="predict">
        <div class="panel">
          <div class="panel-body">
            <div class="panel-head">
              <div class="panel-title">
                <span class="icon-tile" aria-hidden="true">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M3 12h4l3-8 4 16 3-8h4" /></svg>
                </span>
                <div>
                  <b id="panelTitle">Sepsis risk · Bay 4</b>
                  <small>Updated just now · recomputes on every observation</small>
                </div>
              </div>
              <div class="tabs" role="tablist" aria-label="Risk cohort">
                <button class="tab" role="tab" aria-selected="true" data-cohort="sepsis">Sepsis</button>
                <button class="tab" role="tab" aria-selected="false" data-cohort="cardiac">Cardiac</button>
                <button class="tab" role="tab" aria-selected="false" data-cohort="readmission">Readmission</button>
              </div>
            </div>

            <div class="kpis">
              <div class="kpi">
                <div class="k">Current score</div>
                <div class="v" id="kpiScore">0.81</div>
                <div class="d bad" id="kpiDelta">+0.07 in the last hour</div>
              </div>
              <div class="kpi">
                <div class="k">Alert threshold</div>
                <div class="v" id="kpiThr">0.60</div>
                <div class="d bad" id="kpiStatus">Above for 2 h</div>
              </div>
            </div>

            <div class="chart-block">
              <svg class="chart" id="chart" viewBox="0 0 640 220" role="img" aria-label="Risk score over the last twelve hours">
                <defs>
                  <linearGradient id="chartFill" x1="0" y1="0" x2="0" y2="1">
                    <stop offset="0" stop-color="#8db5ff" stop-opacity="0.22" /><stop offset="1" stop-color="#8db5ff" stop-opacity="0" />
                  </linearGradient>
                </defs>
                <g id="chartGrid"></g>
                <path id="chartBand" class="band" d="" />
                <path id="chartArea" class="area" d="" />
                <line id="chartThreshold" class="marker" x1="0" y1="0" x2="0" y2="0" />
                <text id="chartThresholdLabel" class="thr-label" x="0" y="0">alert</text>
                <path id="chartLine" class="line" d="" />
                <g id="chartDots"></g>
                <g id="chartAxis"></g>
              </svg>
              <div class="legend">
                <span><i></i>Risk score</span>
                <span><i class="band"></i>Uncertainty</span>
                <span><i class="thr"></i>Alert threshold</span>
              </div>
              <p class="chart-caption" id="chartCaption">Sepsis · 6 h median lead time before the first vital sign crosses its limit.</p>
            </div>

            <div class="panel-foot">
              <a class="btn btn-outline" href="#governance">Read the sepsis model card</a>
            </div>
          </div>
        </div>

        <ul class="patients" aria-label="Current patients">
          <li class="patient high">
            <div class="top"><div class="who">Bay 4 · PT-40219<small>58F · post-op day 2</small></div><div><span class="state">Escalate</span><span class="score">0.81</span></div></div>
            <div class="meter"><i style="width:81%"></i></div>
            <p>Rising <b>lactate</b>, <b>HR +18</b> over 4 h, falling urine output. Escalate per sepsis pathway.</p>
          </li>
          <li class="patient mid">
            <div class="top"><div class="who">Bay 9 · PT-38820<small>74M · CHF</small></div><div><span class="state">Review</span><span class="score">0.46</span></div></div>
            <div class="meter"><i style="width:46%"></i></div>
            <p>Weight up <b>1.8 kg</b> in 3 days with <b>SpO₂ drift</b>. Review diuretic dose.</p>
          </li>
          <li class="patient low">
            <div class="top"><div class="who">Bay 12 · PT-41007<small>33F · day 1</small></div><div><span class="state">Stable</span><span class="score">0.09</span></div></div>
            <div class="meter"><i style="width:9%"></i></div>
            <p>Stable across all tracked signals. Next recompute in <b>15 min</b>.</p>
          </li>
        </ul>
      </div>
    </div>
  </section>

  <!-- ───── How it works ───── -->
  <section class="section" id="workflow" data-section="how-it-works">
    <div class="wrap">
      <div class="sec-head">
        <span class="label">How a pilot runs</span>
        <h2 class="display">It lives <em>inside</em> the workflow you already have.</h2>
        <p>No new window to learn. Results land in the PACS worklist and the chart your team already opens.</p>
      </div>
      <div class="steps">
        <div class="step">
          <span class="when">Weeks 1–2</span>
          <h3>Connect</h3>
          <p>Point your PACS and HL7 or FHIR feed at an endpoint in your own VPC. Data stays in your region, and nothing trains on it without a signed addendum.</p>
          <div class="tags"><span>DICOM</span><span>HL7 / FHIR</span><span>SSO</span></div>
        </div>
        <div class="step">
          <span class="when">Weeks 3–6</span>
          <h3>Calibrate</h3>
          <p>Run in shadow mode. Compare model output with your own reads, then set alert thresholds for each service line.</p>
          <div class="tags"><span>Shadow mode</span><span>Per-site thresholds</span></div>
        </div>
        <div class="step">
          <span class="when">Week 7 onward</span>
          <h3>Go live</h3>
          <p>Findings arrive as a pre-read with the evidence attached. Drift monitors and a weekly model card keep your governance board current.</p>
          <div class="tags"><span>Pre-read</span><span>Drift monitor</span><span>Audit log</span></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ───── Quote ───── -->
  <section class="quote" data-section="testimonials" aria-label="Customer quote">
    <div class="wrap">
      <figure style="margin:0">
        <blockquote>“The value wasn’t replacing a read. It was knowing <em>which twelve studies</em> to open first.”</blockquote>
        <figcaption>Dr. Amara Osei <span>Clinical lead, Cortis Radiology</span></figcaption>
      </figure>
    </div>
  </section>

  <!-- ───── Governance ───── -->
  <section class="section" id="governance" data-section="governance">
    <div class="wrap">
      <div class="sec-head">
        <span class="label">Governance</span>
        <h2 class="display">Built for the people who have to <em>sign it off</em>.</h2>
        <p>Everything a clinical safety officer asks for on day one, available before you talk to sales.</p>
      </div>
      <div class="gov">
        <div class="panel reg">
          <div class="panel-body">
            <div class="panel-head">
              <div class="panel-title">
                <span class="icon-tile" aria-hidden="true">
                  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M12 3l8 3v6c0 5-4 8-8 9-4-1-8-4-8-9V6z" /><path d="M9 12l2 2 4-4" /></svg>
                </span>
                <div>
                  <b>Regulatory status</b>
                  <small>Listed per model, with validated populations</small>
                </div>
              </div>
            </div>
            <h3>Cleared indications, listed in full</h3>
            <dl>
              <dt>FDA</dt><dd>510(k) number <span class="placeholder">placeholder</span></dd>
              <dt>EU / UK</dt><dd>CE · UKCA class IIa <span class="placeholder">placeholder</span></dd>
              <dt>Intended use</dt><dd>Triage and decision support. Not for standalone diagnosis.</dd>
            </dl>
            <div class="panel-foot">
              <a class="btn btn-outline" href="#outcomes">See the validation footnotes</a>
            </div>
          </div>
        </div>
        <ul class="checks">
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg><b>HIPAA and GDPR</b><span>BAA and DPA on request</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg><b>SOC 2 Type II</b><span>Audited annually</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg><b>Model cards</b><span>Training data, limits, drift</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg><b>Full audit trail</b><span>Every score and override</span></li>
          <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg><b>Version rollback</b><span>From the console, no redeploy</span></li>
        </ul>
      </div>
    </div>
  </section>

  <!-- ───── FAQ ───── -->
  <section class="section" id="faq" data-section="faq">
    <div class="wrap">
      <div class="faq-layout">
      <div class="faq-side">
        <span class="label">Questions</span>
        <h2 class="display">The ones your board will <em>ask</em>.</h2>
        <p>Anything not covered here goes to our clinical safety lead, who replies within one working day.</p>
        <a class="btn btn-outline" href="#start">Ask a question</a>
      </div>
      <div class="faq">
        <div class="qa" data-open="true">
          <button aria-expanded="true">Does the model make the diagnosis?<svg class="sign" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 4v16M4 12h16" /></svg></button>
          <div class="qa-panel" style="height:auto"><p>No. It produces a pre-read with confidence scores and the evidence behind them. A clinician reviews and signs every report, and every override is logged and added to the evaluation set.</p></div>
        </div>
        <div class="qa" data-open="false">
          <button aria-expanded="false">Where does patient data live?<svg class="sign" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 4v16M4 12h16" /></svg></button>
          <div class="qa-panel"><p>In your region, in a VPC you control. De-identification happens before anything leaves that perimeter, and no customer data is used for training without a signed addendum naming the exact cohort.</p></div>
        </div>
        <div class="qa" data-open="false">
          <button aria-expanded="false">How long does integration take?<svg class="sign" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 4v16M4 12h16" /></svg></button>
          <div class="qa-panel"><p>Two weeks to a shadow-mode deployment for a typical PACS and HL7 feed. Then four weeks of calibration against your own reads before anything reaches a clinician.</p></div>
        </div>
        <div class="qa" data-open="false">
          <button aria-expanded="false">What happens when the model is wrong?<svg class="sign" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 4v16M4 12h16" /></svg></button>
          <div class="qa-panel"><p>Misses and false positives are reviewed weekly with your clinical safety officer. Thresholds can be tuned per service line, and any model version can be rolled back from the console.</p></div>
        </div>
        <div class="qa" data-open="false">
          <button aria-expanded="false">How do we know it still works next year?<svg class="sign" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M12 4v16M4 12h16" /></svg></button>
          <div class="qa-panel"><p>Drift monitors compare live inputs and outputs with the validation set every week. A drop past the agreed limit alerts your safety officer and pauses that model's flags until it is reviewed.</p></div>
        </div>
      </div>
      </div>

      <!-- ───── CTA ───── -->
      <div class="cta" id="start" data-section="cta">
        <div class="cta-fx" aria-hidden="true"><div class="aurora"></div><div class="floor"></div><div class="spot"></div><div class="grain"></div></div>
        <div class="cta-copy">
          <span class="label">Clinical pilot · booking for Q1 2027</span>
          <h2 class="display">Bring AI into the read, <em>not around it</em>.</h2>
          <p>Start with one service line and a four-week shadow deployment. If the numbers don’t hold up against your own reads, you walk away.</p>
          <div class="hero-actions">
            <a class="btn btn-primary" href="#start">
              Book a clinical pilot
              <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6" /></svg>
            </a>
            <a class="btn btn-quiet" href="#governance">Read the model card</a>
          </div>
          <ul class="cta-assure">
            <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg>Nothing reaches a clinician until shadow mode is signed off</li>
            <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg>Patient data stays in your VPC and your region</li>
            <li><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12l5 5 9-10" /></svg>No exit fee if you stop at the week 6 decision</li>
          </ul>
        </div>

        <aside class="panel cta-plan" aria-label="Pilot plan">
          <div class="panel-body">
            <div class="panel-head">
              <div class="panel-title">
                <span class="icon-tile" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><path d="M5 21V4M5 4h11l-2 4 2 4H5" /></svg></span>
                <div><b>Pilot plan</b><small>One service line · 7 weeks</small></div>
              </div>
              <span class="live"><i></i>Starts 2 weeks after signing</span>
            </div>
            <div class="plan-track">
              <div class="track" aria-hidden="true"><i class="c wk" style="--n:0"></i><i class="c" style="--n:1"></i><i class="c" style="--n:2"></i><i class="c" style="--n:3"></i><i class="c wk" style="--n:4"></i><i class="c" style="--n:5"></i><i class="c" style="--n:6"></i><i class="c" style="--n:7"></i><i class="s wk" style="--n:8"></i><i class="s" style="--n:9"></i><i class="s" style="--n:10"></i><i class="s" style="--n:11"></i><i class="s wk" style="--n:12"></i><i class="s" style="--n:13"></i><i class="s" style="--n:14"></i><i class="s" style="--n:15"></i><i class="s wk" style="--n:16"></i><i class="s" style="--n:17"></i><i class="s" style="--n:18"></i><i class="s" style="--n:19"></i><i class="s wk" style="--n:20"></i><i class="s" style="--n:21"></i><i class="s" style="--n:22"></i><i class="s" style="--n:23"></i><i class="l wk" style="--n:24"></i><i class="l" style="--n:25"></i><i class="l" style="--n:26"></i><i class="l" style="--n:27"></i></div>
              <div class="gate" aria-hidden="true"><span>Decision</span></div>
              <div class="track-labels" aria-hidden="true"><span>W1</span><span>W2</span><span>W3</span><span>W4</span><span>W5</span><span>W6</span><span>W7</span></div>
            </div>
            <ol class="phases">
              <li class="phase"><span class="w">W1–2</span><b>Connect</b><small>PACS and HL7 or FHIR feed, inside your VPC</small></li>
              <li class="phase"><span class="w">W3–6</span><b>Shadow mode</b><small>Model output compared with your own reads</small></li>
              <li class="phase"><span class="w">W7</span><b>Go live</b><small>Pre-reads land in the worklist, if you approve</small></li>
            </ol>
            <div class="kpis">
              <div class="kpi"><div class="k">Service lines</div><div class="v">1</div></div>
              <div class="kpi"><div class="k">Decision gate</div><div class="v">Week 6</div></div>
              <div class="kpi"><div class="k">Exit fee</div><div class="v">None</div></div>
            </div>
          </div>
        </aside>
      </div>
    </div>
  </section>
</main>

<div class="wrap" data-section="footer">
  <footer class="footer">
    <div>
      <a class="logo" href="#top" aria-label="SmartCare Solutions home">
        <span class="logo-mark" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round"><path d="M4 12h6m4 0h6M12 4v6m0 4v6" /></svg></span>
        SmartCare <span>Solutions</span>
      </a>
      <p>Clinical AI for imaging and risk, built to be reviewed, audited and switched off by the people who use it.</p>
    </div>
    <div class="fcol">
      <h4 class="label">Platform</h4>
      <a href="#capabilities">Image analysis</a>
      <a href="#predictive">Predictive risk</a>
      <a href="#capabilities">Treatment planning</a>
      <a href="#capabilities">Research cohorts</a>
    </div>
    <div class="fcol">
      <h4 class="label">Company</h4>
      <a href="#workflow">How a pilot runs</a>
      <a href="#governance">Governance</a>
      <a href="#faq">FAQ</a>
      <a href="#start">Contact</a>
    </div>
    <div class="fcol">
      <h4 class="label">Evidence</h4>
      <a href="#governance">Model cards</a>
      <a href="#outcomes">Clinical outcomes</a>
      <a href="#governance">Security</a>
    </div>
  </footer>
  <div class="legal">
    <span>© 2026 SmartCare Solutions</span>
    <span class="note">Illustrative demo. SmartCare Solutions is a fictional company. Figures, patients, partners and studies are synthetic and are not medical advice.</span>
  </div>
</div>

</div>

<script>
(function () {
  "use strict";
  var REDUCED = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var $ = function (s, c) { return (c || document).querySelector(s); };
  var $$ = function (s, c) { return Array.prototype.slice.call((c || document).querySelectorAll(s)); };

  /* full-screen menu */
  var header = $(".header"), menuBtn = $("#menuBtn"), menu = $("#menu");
  var menuLbl = $(".lbl", menuBtn);
  var isOpen = false;
  var setMenu = function (open, returnFocus, viaKeys) {
    isOpen = open;
    header.setAttribute("data-open", String(open));
    menu.classList.toggle("open", open);
    menuBtn.setAttribute("aria-expanded", String(open));
    menuLbl.textContent = open ? "Close" : "Menu";
    document.documentElement.style.overflow = open ? "hidden" : "";
    if (open) {
      menu.removeAttribute("inert");
      if (viaKeys) setTimeout(function () { var first = $(".m-link", menu); if (first) first.focus({ preventScroll: true }); }, 450);
    } else {
      menu.setAttribute("inert", "");
      showPreview(null);
      if (returnFocus) menuBtn.focus();
    }
  };
  menuBtn.addEventListener("click", function (e) { setMenu(!isOpen, false, e.detail === 0); });
  menu.addEventListener("click", function (e) {
    var a = e.target.closest("a[href^='#']");
    if (!a) return;
    e.preventDefault();
    var target = document.querySelector(a.getAttribute("href"));
    setMenu(false, false);
    if (target) setTimeout(function () { target.scrollIntoView({ behavior: REDUCED ? "auto" : "smooth" }); }, 380);
  });
  document.addEventListener("keydown", function (e) {
    if (!isOpen) return;
    if (e.key === "Escape") { setMenu(false, true); return; }
    if (e.key !== "Tab") return;
    /* keep focus inside the header bar and the menu while it is open */
    var focusables = $$("a, button", header).concat($$("a, button", menu)).filter(function (el) { return el.offsetParent !== null; });
    var first = focusables[0], last = focusables[focusables.length - 1];
    if (e.shiftKey && document.activeElement === first) { e.preventDefault(); last.focus(); }
    else if (!e.shiftKey && document.activeElement === last) { e.preventDefault(); first.focus(); }
  });

  /* the preview panel follows whichever section link is hovered or focused */
  var PREVIEWS = {
    "default": { label: "Current release", title: "Pre-reads in 1.8 seconds", text: "Median model read across MR, CT and X-ray, with every finding traced to the pixels behind it.", k1: "Read time", v1: "1.8 s", k2: "Agreement", v2: "97.4%", cta: "Book a clinical pilot", href: "#start" },
    reader: { label: "Image analysis", title: "Every finding traced to its pixels", text: "Segmentation and detection across MRI, CT, X-ray and pathology, delivered as a pre-read in the worklist you already use.", k1: "Median read", v1: "1.8 s", k2: "Modalities", v2: "4", cta: "See the platform", href: "#capabilities" },
    predictive: { label: "Predictive risk", title: "Risk that moves before the patient does", text: "Deterioration, sepsis and readmission scores recalculated on every new observation, with the drivers shown.", k1: "Median lead time", v1: "6 h", k2: "Cohorts", v2: "3", cta: "Open the risk chart", href: "#predictive" },
    outcomes: { label: "Outcomes", title: "Footnoted, site by site", text: "Results from an 18-month rollout at six sites, each figure listed with its method and study size.", k1: "Agreement", v1: "97.4%", k2: "Readmissions", v2: "−34%", cta: "Read the outcomes", href: "#outcomes" },
    governance: { label: "Governance", title: "Built to be signed off", text: "Clearance status, model cards, a full audit trail and version rollback from the console.", k1: "Audit", v1: "SOC 2 II", k2: "Rollback", v2: "1 click", cta: "Review governance", href: "#governance" }
  };
  var preview = $("#menuPreview"), pvKey = "default", pvTimer = 0;
  var showPreview = function (key) {
    key = key || "default";
    if (key === pvKey) return;
    pvKey = key;
    var d = PREVIEWS[key];
    preview.classList.add("swap");
    clearTimeout(pvTimer);
    pvTimer = setTimeout(function () {
      $("#pvLabel").textContent = d.label;
      $("#pvTitle").textContent = d.title;
      $("#pvText").textContent = d.text;
      $("#pvK1").textContent = d.k1; $("#pvV1").textContent = d.v1;
      $("#pvK2").textContent = d.k2; $("#pvV2").textContent = d.v2;
      var cta = $("#pvCta"); cta.textContent = d.cta; cta.setAttribute("href", d.href);
      preview.classList.remove("swap");
    }, 180);
  };
  $$(".m-link", menu).forEach(function (a) {
    a.addEventListener("mouseenter", function () { showPreview(a.getAttribute("data-key")); });
    a.addEventListener("focus", function () { showPreview(a.getAttribute("data-key")); });
  });
  $("#menuLinks").addEventListener("mouseleave", function () { showPreview(null); });

  /* cta spotlight follows the pointer */
  var ctaEl = $(".cta");
  if (ctaEl && !REDUCED) {
    ctaEl.addEventListener("pointermove", function (e) {
      var r = ctaEl.getBoundingClientRect();
      ctaEl.style.setProperty("--mx", (e.clientX - r.left) + "px");
      ctaEl.style.setProperty("--my", (e.clientY - r.top) + "px");
    });
  }

  /* faq */
  $$(".qa").forEach(function (qa) {
    var btn = $("button", qa), panel = $(".qa-panel", qa);
    btn.addEventListener("click", function () {
      var open = qa.getAttribute("data-open") === "true";
      panel.style.height = panel.scrollHeight + "px";
      if (open) requestAnimationFrame(function () { panel.style.height = "0px"; });
      qa.setAttribute("data-open", String(!open));
      btn.setAttribute("aria-expanded", String(!open));
    });
    panel.addEventListener("transitionend", function (e) {
      if (e.propertyName === "height" && qa.getAttribute("data-open") === "true") panel.style.height = "auto";
    });
  });

  /* risk chart */
  var COHORTS = {
    sepsis: { threshold: 0.6, caption: "Sepsis · 6 h median lead time before the first vital sign crosses its limit.",
      values: [0.11, 0.13, 0.12, 0.17, 0.21, 0.26, 0.3, 0.39, 0.47, 0.56, 0.65, 0.74, 0.81] },
    cardiac: { threshold: 0.5, caption: "Cardiac decompensation · weight gain and SpO₂ drift carry most of the score.",
      values: [0.3, 0.33, 0.31, 0.36, 0.34, 0.39, 0.42, 0.4, 0.44, 0.47, 0.45, 0.46, 0.46] },
    readmission: { threshold: 0.4, caption: "30-day readmission · recomputed at every discharge milestone.",
      values: [0.52, 0.5, 0.46, 0.44, 0.39, 0.36, 0.34, 0.3, 0.27, 0.24, 0.2, 0.15, 0.09] }
  };
  COHORTS.sepsis.title = "Sepsis risk · Bay 4";
  COHORTS.cardiac.title = "Cardiac decompensation · Bay 9";
  COHORTS.readmission.title = "30-day readmission · Bay 12";
  var X0 = 36, X1 = 616, Y0 = 178, Y1 = 16, NS = "http://www.w3.org/2000/svg";
  var grid = $("#chartGrid"), axis = $("#chartAxis"), dots = $("#chartDots");
  var line = $("#chartLine"), area = $("#chartArea"), band = $("#chartBand");
  var thr = $("#chartThreshold"), thrLabel = $("#chartThresholdLabel"), caption = $("#chartCaption");
  var px = function (i, n) { return X0 + ((X1 - X0) * i) / (n - 1); };
  var py = function (v) { return Y0 - (Y0 - Y1) * v; };
  var mk = function (tag, attrs) {
    var el = document.createElementNS(NS, tag);
    Object.keys(attrs).forEach(function (k) { el.setAttribute(k, attrs[k]); });
    return el;
  };
  var path = function (pts) { return pts.map(function (p, i) { return (i ? "L" : "M") + p[0].toFixed(1) + " " + p[1].toFixed(1); }).join(" "); };

  /* smooth curve through every point (Catmull-Rom as cubic Béziers), clamped to the plot */
  var smooth = function (pts) {
    var clampY = function (y) { return Math.max(Y1, Math.min(Y0, y)); };
    var d = "M" + pts[0][0].toFixed(1) + " " + pts[0][1].toFixed(1);
    for (var i = 0; i < pts.length - 1; i++) {
      var p0 = pts[i - 1] || pts[i], p1 = pts[i], p2 = pts[i + 1], p3 = pts[i + 2] || p2;
      var c1x = p1[0] + (p2[0] - p0[0]) / 6, c1y = clampY(p1[1] + (p2[1] - p0[1]) / 6);
      var c2x = p2[0] - (p3[0] - p1[0]) / 6, c2y = clampY(p2[1] - (p3[1] - p1[1]) / 6);
      d += " C" + c1x.toFixed(1) + "," + c1y.toFixed(1) + " " + c2x.toFixed(1) + "," + c2y.toFixed(1) + " " + p2[0].toFixed(1) + "," + p2[1].toFixed(1);
    }
    return d;
  };

  [0, 0.5, 1].forEach(function (v) {
    grid.appendChild(mk("line", { class: "grid-line", x1: X0, x2: X1, y1: py(v), y2: py(v) }));
    var t = mk("text", { class: "axis-label", x: X0 - 8, y: py(v) + 4, "text-anchor": "end" });
    t.textContent = v === 0 ? "0" : v === 1 ? "1" : v.toFixed(2);
    grid.appendChild(t);
  });
  ["−12h", "−9h", "−6h", "−3h", "now"].forEach(function (lbl, i) {
    var t = mk("text", { class: "axis-label", x: px(i * 3, 13), y: 204, "text-anchor": i === 4 ? "end" : i === 0 ? "start" : "middle" });
    t.textContent = lbl;
    axis.appendChild(t);
  });

  var draw = function (key, animate) {
    var c = COHORTS[key], n = c.values.length;
    var pts = c.values.map(function (v, i) { return [px(i, n), py(v)]; });
    var d = smooth(pts);
    line.setAttribute("d", d);
    area.setAttribute("d", d + " L" + X1 + " " + Y0 + " L" + X0 + " " + Y0 + " Z");
    var up = c.values.map(function (v, i) { return [px(i, n), py(Math.min(1, v + 0.07))]; });
    var dn = c.values.map(function (v, i) { return [px(i, n), py(Math.max(0, v - 0.07))]; }).reverse();
    band.setAttribute("d", smooth(up) + " " + smooth(dn).replace(/^M/, "L") + " Z");

    var ty = py(c.threshold);
    thr.setAttribute("x1", X0); thr.setAttribute("x2", X1);
    thr.setAttribute("y1", ty); thr.setAttribute("y2", ty);
    thrLabel.setAttribute("x", X0 + 6);
    thrLabel.setAttribute("y", ty - 7);
    thrLabel.textContent = "alert " + c.threshold.toFixed(2);
    caption.textContent = c.caption;

    /* live endpoint: solid dot plus a pulsing ring, red once the score is over the threshold */
    var last = c.values[n - 1], prev = c.values[n - 2];
    var hot = last >= c.threshold;
    dots.textContent = "";
    var g = mk("g", { class: hot ? "hot" : "" });
    g.appendChild(mk("circle", { class: "ring", cx: pts[n - 1][0], cy: pts[n - 1][1], r: 5 }));
    g.appendChild(mk("circle", { class: "dot", cx: pts[n - 1][0], cy: pts[n - 1][1], r: 5 }));
    dots.appendChild(g);

    /* KPI row */
    $("#panelTitle").textContent = c.title;
    $("#kpiScore").textContent = last.toFixed(2);
    $("#kpiThr").textContent = c.threshold.toFixed(2);
    var delta = last - prev;
    var deltaEl = $("#kpiDelta");
    deltaEl.textContent = (delta > 0 ? "+" : delta < 0 ? "−" : "±") + Math.abs(delta).toFixed(2) + " in the last hour";
    deltaEl.className = "d " + (delta > 0.005 ? "bad" : delta < -0.005 ? "good" : "flat");
    var statusEl = $("#kpiStatus");
    if (hot) {
      var k = n - 1;
      while (k > 0 && c.values[k - 1] >= c.threshold) k--;
      statusEl.textContent = "Above for " + (n - 1 - k) + " h";
      statusEl.className = "d bad";
    } else {
      statusEl.textContent = (c.threshold - last).toFixed(2) + " below";
      statusEl.className = "d good";
    }

    if (animate && !REDUCED && line.getTotalLength) {
      var len = line.getTotalLength();
      line.style.transition = "none";
      line.style.strokeDasharray = len + " " + len;
      line.style.strokeDashoffset = len;
      void line.getBoundingClientRect();
      line.style.transition = "stroke-dashoffset 1s cubic-bezier(.6,0,.2,1)";
      line.style.strokeDashoffset = "0";
    }
  };
  var current = "sepsis";
  draw(current, false);
  $$(".tab").forEach(function (btn) {
    btn.addEventListener("click", function () {
      if (btn.getAttribute("data-cohort") === current) return;
      $$(".tab").forEach(function (b) { b.setAttribute("aria-selected", "false"); });
      btn.setAttribute("aria-selected", "true");
      current = btn.getAttribute("data-cohort");
      draw(current, true);
    });
  });
})();
</script>

<script>
/* Hero HUD: builds the tick rings and the 36 radiating pills, then keeps the
   pills, the ray from the core, the readout and the chips in step. */
(function () {
  "use strict";
  var host = document.getElementById("hudRings");
  if (!host) return;

  var FINDINGS = [
    { key: "lesion", slot: 11, name: "Focal FLAIR hyperintensity", chip: "Lesion", score: 0.93, note: "Right frontal · 12.4 mm · prior from 2025-11-04 queued", hot: true },
    { key: "ventricles", slot: 8, name: "Ventricular enlargement", chip: "Ventricles", score: 0.11, note: "Within age-matched range" },
    { key: "mass", slot: 14, name: "Mass effect", chip: "Mass effect", score: 0.06, note: "None significant" },
    { key: "midline", slot: 5, name: "Midline shift", chip: "Midline", score: 0.02, note: "None detected" },
    { key: "haem", slot: 17, name: "Acute haemorrhage", chip: "Haemorrhage", score: 0.01, note: "None detected" }
  ];
  var bySlot = {};
  FINDINGS.forEach(function (f) { bySlot[f.slot] = f; });

  var frag = document.createDocumentFragment();
  var add = function (cls, style) {
    var el = document.createElement("div");
    el.className = cls;
    el.setAttribute("style", style);
    frag.appendChild(el);
    return el;
  };

  for (var i = 0; i < 36; i++) {
    /* inner ring: short tangential bars, always lit */
    add("tick", "--a:" + i * 10 + "deg;--r:78;--w:7;--h:20");
    /* second ring: radial dashes sweeping round */
    add("tick fade", "--a:" + i * 10 + "deg;--r:148;--w:24;--h:4;--d:" + (i / 10).toFixed(1) + "s");
    /* third ring: long cool dashes over a 140° arc */
    add("tick fade", "--a:" + i * 4 + "deg;--r:224;--w:46;--h:4;--c:#a9e3ff;--d:" + (i / 10).toFixed(1) + "s");
    /* fourth and fifth: fine counter-arcs on the far side */
    add("tick fade", "--a:" + (i * 4 + 180) + "deg;--r:236;--w:6;--h:4;--t:7s;--d:" + (i / 10).toFixed(1) + "s");
    add("tick fade", "--a:" + (i * 4 + 180) + "deg;--r:206;--w:6;--h:4;--t:7s;--d:" + (i / 10).toFixed(1) + "s");
  }

  var pills = {};
  for (var p = 0; p < 36; p++) {
    var f = bySlot[p];
    var len = 110 + ((p * 37) % 50);
    var el = add("pill " + (f ? "live" + (f.hot ? " hot" : "") : "blank"), "--a:" + p * 10 + "deg;--r:300;--len:" + len);
    if (f) {
      pills[f.key] = el;
      el.addEventListener("pointerenter", (function (k) { return function () { setActive(k); }; })(f.key));
    }
  }
  host.appendChild(frag);

  var ray = document.getElementById("hudRay");
  var roName = document.getElementById("roName");
  var roNote = document.getElementById("roNote");
  var roScore = document.getElementById("roScore");
  var chipsHost = document.getElementById("roChips");
  var chips = {};

  FINDINGS.forEach(function (f) {
    var b = document.createElement("button");
    b.className = "chip-btn" + (f.hot ? " hot" : "");
    b.setAttribute("role", "tab");
    b.setAttribute("aria-selected", "false");
    b.innerHTML = f.chip + " <em>" + f.score.toFixed(2) + "</em>";
    b.addEventListener("click", function () { setActive(f.key); });
    b.addEventListener("keydown", function (e) {
      var idx = FINDINGS.indexOf(f), next = null;
      if (e.key === "ArrowRight") next = FINDINGS[(idx + 1) % FINDINGS.length];
      if (e.key === "ArrowLeft") next = FINDINGS[(idx - 1 + FINDINGS.length) % FINDINGS.length];
      if (next) { e.preventDefault(); setActive(next.key); chips[next.key].focus(); }
    });
    chips[f.key] = b;
    chipsHost.appendChild(b);
  });

  var current = null;
  function setActive(key) {
    if (key === current) return;
    current = key;
    var f = FINDINGS.filter(function (x) { return x.key === key; })[0];
    Object.keys(pills).forEach(function (k) { pills[k].classList.toggle("on", k === key); });
    Object.keys(chips).forEach(function (k) {
      chips[k].setAttribute("aria-selected", String(k === key));
      chips[k].tabIndex = k === key ? 0 : -1;
    });
    ray.style.setProperty("--ray", f.slot * 10 + "deg");
    ray.classList.toggle("hot", !!f.hot);
    roName.textContent = f.name;
    roNote.textContent = f.note;
    roScore.textContent = f.score.toFixed(2);
    roScore.parentNode.classList.toggle("hot", !!f.hot);
  }
  setActive("lesion");
})();
</script>

<script>
/* Platform card graphics, drawn into each SVG in the hero HUD's language:
   a glowing core, tick rings that sweep, radiating pills, one lit signal. */
(function () {
  "use strict";
  var NS = "http://www.w3.org/2000/svg";
  var SIG = "#8db5ff", ALERT = "#ff6b7d", COOL = "#a9e3ff", DIM = "rgba(141,181,255,0.16)";
  var el = function (parent, tag, attrs, text) {
    var n = document.createElementNS(NS, tag);
    for (var k in attrs) n.setAttribute(k, attrs[k]);
    if (text != null) n.textContent = text;
    parent.appendChild(n);
    return n;
  };
  var pt = function (cx, cy, r, deg) {
    var a = deg * Math.PI / 180;
    return [cx + r * Math.cos(a), cy + r * Math.sin(a)];
  };
  var tick = function (g, cx, cy, r1, r2, deg, attrs) {
    var a = pt(cx, cy, r1, deg), b = pt(cx, cy, r2, deg);
    var o = { x1: a[0].toFixed(1), y1: a[1].toFixed(1), x2: b[0].toFixed(1), y2: b[1].toFixed(1), "vector-effect": "non-scaling-stroke" };
    for (var k in attrs) o[k] = attrs[k];
    return el(g, "line", o);
  };
  var glow = function (svg, id) {
    var d = el(svg, "defs", {});
    var f = el(d, "filter", { id: id, x: "-50%", y: "-50%", width: "200%", height: "200%" });
    el(f, "feGaussianBlur", { stdDeviation: "4", result: "b" });
    var m = el(f, "feMerge", {});
    el(m, "feMergeNode", { in: "b" });
    el(m, "feMergeNode", { in: "SourceGraphic" });
    return "url(#" + id + ")";
  };
  var fade = function (n, i, t) {
    n.setAttribute("class", "v-fade");
    n.setAttribute("style", "--d:" + (i / 10).toFixed(1) + "s" + (t ? ";--t:" + t : ""));
  };

  var DRAW = {
    /* a stack of axial slices in the hero's tilt; a scan plane sweeps through,
       one slice is lit and carries the lesion */
    imaging: function (svg) {
      var gl = glow(svg, "gl-img"), cx = 214, active = 3;
      var Y = [56, 76, 96, 116, 136, 156, 176];
      el(svg, "text", { x: 16, y: 24, class: "v-text" }, "MR · AX T2 FLAIR");
      el(svg, "text", { x: 384, y: 24, class: "v-text", "text-anchor": "end" }, "28 SLICES");
      el(svg, "line", { x1: 40, y1: 50, x2: 40, y2: 184, stroke: "rgba(141,181,255,0.18)", "stroke-width": 1 });
      Y.forEach(function (y, k) {
        var on = k === active, rx = 112 + k * 5, ry = 20 + k * 1.6;
        el(svg, "ellipse", { cx: cx, cy: y, rx: rx, ry: ry, fill: on ? "rgba(141,181,255,0.08)" : "rgba(141,181,255,0.015)",
          stroke: on ? SIG : "rgba(141,181,255,0.28)", "stroke-width": on ? 4 : 3, "stroke-dasharray": "1.2 5.5", opacity: on ? 1 : 0.35 + k * 0.06 });
        el(svg, "ellipse", { cx: cx, cy: y, rx: rx * 0.62, ry: ry * 0.62, fill: "none", stroke: on ? "rgba(141,181,255,0.55)" : "rgba(141,181,255,0.12)", "stroke-width": 1 });
        el(svg, "line", { x1: 34, y1: y, x2: on ? 50 : 44, y2: y, stroke: on ? SIG : "rgba(141,181,255,0.4)", "stroke-width": on ? 2 : 1 });
        el(svg, "text", { x: 56, y: y + 3.5, class: "v-text" + (on ? " sig" : "") }, "S" + (8 + k * 2));
      });
      var scan = el(svg, "g", { class: "v-scan" });
      el(scan, "ellipse", { cx: cx, cy: 116, rx: 128, ry: 25, fill: "rgba(141,181,255,0.05)", stroke: COOL, "stroke-width": 1.2, opacity: 0.8 });
      var lx = cx + 36, ly = 112;
      el(scan, "circle", { cx: lx, cy: ly, r: 7, fill: ALERT, class: "v-pulse", opacity: 0.4 });
      el(scan, "circle", { cx: lx, cy: ly, r: 5, fill: ALERT, filter: gl });
      el(svg, "text", { x: 384, y: 210, class: "v-text", "text-anchor": "end" }, "SLICE 14 / 28 · RIGHT FRONTAL · 12.4 MM");
    },

    /* the last 12 hours as pills; red once past the alert line, newest pulses */
    risk: function (svg) {
      var V = [0.11, 0.13, 0.12, 0.17, 0.21, 0.26, 0.3, 0.39, 0.47, 0.56, 0.65, 0.74, 0.81], thr = 0.6;
      var x0 = 52, x1 = 344, base = 172, h = 124, n = V.length;
      var X = function (i) { return x0 + (x1 - x0) * i / (n - 1); };
      el(svg, "text", { x: 16, y: 24, class: "v-text" }, "SEPSIS · BAY 4");
      el(svg, "text", { x: 384, y: 24, class: "v-text", "text-anchor": "end" }, "HOURLY · LAST 12 H");
      V.forEach(function (v, i) {
        var x = X(i), hot = v >= thr;
        el(svg, "line", { x1: x, y1: base, x2: x, y2: base - h, stroke: "rgba(141,181,255,0.06)", "stroke-width": 11 });
        el(svg, "line", { x1: x, y1: base, x2: x, y2: (base - v * h).toFixed(1), stroke: hot ? ALERT : SIG, "stroke-width": 11, opacity: (0.35 + 0.65 * i / (n - 1)).toFixed(2) });
        el(svg, "line", { x1: x, y1: base + 10, x2: x, y2: base + (i % 3 === 0 ? 18 : 14), stroke: "rgba(141,181,255,0.4)", "stroke-width": 1 });
      });
      var ex = X(n - 1), ey = base - V[n - 1] * h;
      el(svg, "circle", { cx: ex, cy: ey, r: 7, fill: ALERT, class: "v-pulse", opacity: 0.4 });
      el(svg, "circle", { cx: ex, cy: ey, r: 5, fill: ALERT, filter: glow(svg, "gl-riskv") });
      el(svg, "text", { x: ex + 16, y: ey + 4, class: "v-text hi" }, "0.81");
      [["−12H", 0], ["−6H", 6], ["NOW", 12]].forEach(function (t) {
        el(svg, "text", { x: X(t[1]), y: base + 32, class: "v-text", "text-anchor": t[1] === 0 ? "start" : t[1] === 12 ? "end" : "middle" }, t[0]);
      });
    },

    /* the patient branches to four options; each fit is a segmented meter,
       and the option that interacts with CHF is cut off in red */
    plan: function (svg) {
      var gl = glow(svg, "gl-plan"), nx = 46, ny = 116;
      var OPTS = [
        { k: "A", name: "ACE INHIBITOR", s: 0.86, y: 44 },
        { k: "B", name: "BETA BLOCKER", s: 0.71, y: 92 },
        { k: "C", name: "DIURETIC TITRATION", s: 0.54, y: 140 },
        { k: "D", name: "NSAID", s: 0.22, y: 188, bad: true }
      ];
      OPTS.forEach(function (o, r) {
        var c = o.bad ? ALERT : SIG, op = o.bad ? 0.9 : [1, 0.6, 0.38][r];
        el(svg, "path", { d: "M" + nx + "," + ny + " C" + (nx + 50) + "," + ny + " " + (nx + 40) + "," + o.y + " 132," + o.y,
          fill: "none", stroke: c, "stroke-width": r === 0 ? 2 : 1.2, opacity: op, "stroke-dasharray": o.bad ? "3 4" : r === 0 ? "6 4" : "none", class: r === 0 ? "v-dash" : "" });
        el(svg, "circle", { cx: 134, cy: o.y, r: 3.5, fill: c, opacity: op });
        el(svg, "text", { x: 148, y: o.y - 5, class: "v-text" + (r === 0 ? " hi" : o.bad ? " alert" : "") }, o.k + "  " + o.name);
        var lit = Math.round(o.s * 20);
        for (var t = 0; t < 20; t++) {
          var x = 150 + t * 9.2;
          el(svg, "line", { x1: x, y1: o.y + 5, x2: x, y2: o.y + 15, stroke: t < lit ? c : "rgba(141,181,255,0.14)", "stroke-width": 3.5, opacity: t < lit ? op : 1 });
        }
        el(svg, "text", { x: 384, y: o.y + 14, class: "v-text" + (r === 0 ? " hi" : o.bad ? " alert" : ""), "text-anchor": "end" }, o.s.toFixed(2));
        if (o.bad) el(svg, "text", { x: 384, y: o.y - 5, class: "v-text alert", "text-anchor": "end" }, "INTERACTION · CHF");
        if (r === 0) el(svg, "text", { x: 384, y: o.y - 5, class: "v-text sig", "text-anchor": "end" }, "FIRST LINE");
      });
      for (var j = 0; j < 16; j++) fade(tick(svg, nx, ny, 11, 15, j * 22.5, { stroke: SIG, "stroke-width": 2 }), j);
      el(svg, "circle", { cx: nx, cy: ny, r: 6, fill: SIG, filter: gl });
      el(svg, "text", { x: 16, y: 24, class: "v-text" }, "PT-38820 · 74M · CHF");
    },

    /* every study as a dot on a tilted plane; the queried cohort rises as pins */
    cohort: function (svg) {
      var gl = glow(svg, "gl-coh"), cols = 17, rows = 9;
      var P = function (i, j) { return [56 + i * 15 + j * 9, 198 - j * 11]; };
      el(svg, "text", { x: 16, y: 24, class: "v-text" }, "QUERY");
      el(svg, "text", { x: 16, y: 38, class: "v-text hi" }, "“FLAIR LESION > 10 MM, AGE 50–70”");
      el(svg, "text", { x: 384, y: 24, class: "v-text sig", "text-anchor": "end" }, "n = 1,284");
      el(svg, "text", { x: 384, y: 38, class: "v-text", "text-anchor": "end" }, "OF 41,800 STUDIES");
      var c = [P(0, 0), P(cols - 1, 0), P(cols - 1, rows - 1), P(0, rows - 1)];
      el(svg, "polygon", { points: c.map(function (p) { return p.join(","); }).join(" "), fill: "rgba(141,181,255,0.03)", stroke: "rgba(141,181,255,0.18)", "stroke-width": 1 });
      for (var t = 0; t < cols; t++) { var q = P(t, 0); el(svg, "line", { x1: q[0], y1: q[1] + 6, x2: q[0], y2: q[1] + (t % 4 === 0 ? 12 : 9), stroke: "rgba(141,181,255,0.4)", "stroke-width": 1 }); }
      var pins = [];
      for (var j = rows - 1; j >= 0; j--) {
        for (var i = 0; i < cols; i++) {
          var p = P(i, j), d = Math.hypot((i - 10.5) / 3.6, (j - 4) / 2.6), sel = d < 1;
          el(svg, "circle", { cx: p[0], cy: p[1], r: sel ? 2 : 1.4, fill: sel ? SIG : "rgba(141,181,255,0.25)" });
          if (sel) pins.push({ p: p, h: 18 + ((i * 7 + j * 13) % 5) * 9 * (1.2 - d) });
        }
      }
      pins.forEach(function (o, k) {
        var top = o.p[1] - o.h;
        el(svg, "line", { x1: o.p[0], y1: o.p[1], x2: o.p[0], y2: top.toFixed(1), stroke: SIG, "stroke-width": 1.2, opacity: 0.55 });
        el(svg, "circle", { cx: o.p[0], cy: top.toFixed(1), r: 2.6, fill: SIG, filter: gl });
        if (k % 5 === 0) el(svg, "circle", { cx: o.p[0], cy: top.toFixed(1), r: 3, fill: SIG, class: "v-pulse", opacity: 0.3 });
      });
    }
  };
  Array.prototype.forEach.call(document.querySelectorAll("svg[data-vis]"), function (svg) {
    var fn = DRAW[svg.getAttribute("data-vis")];
    if (fn) fn(svg);
  });
})();
</script>

<script>
/* Iridescent shader behind the hero instrument. Same fragment shader as before,
   tinted to the page's ink blue, slowed down and masked so it reads as a glow
   behind the scan reader. Pauses off-screen; one still frame under reduced motion. */
(function () {
  "use strict";
  var canvas = document.getElementById("iridCanvas");
  var host = canvas && canvas.parentNode;
  if (!canvas || !host) return;
  var gl = null;
  try {
    var opts = { alpha: true, antialias: false, depth: false, stencil: false, powerPreference: "low-power" };
    gl = canvas.getContext("webgl", opts) || canvas.getContext("experimental-webgl", opts);
  } catch (e) { gl = null; }
  if (!gl) { host.setAttribute("data-irid", "off"); return; }

  var VERT = "attribute vec2 uv;attribute vec2 position;varying vec2 vUv;void main(){vUv=uv;gl_Position=vec4(position,0,1);}";
  var FRAG = [
    "precision highp float;",
    "uniform float uTime;uniform vec3 uColor;uniform vec3 uResolution;uniform vec2 uMouse;uniform float uAmplitude;uniform float uSpeed;",
    "varying vec2 vUv;",
    "void main(){",
    "  float mr=min(uResolution.x,uResolution.y);",
    "  vec2 uv=(vUv.xy*2.0-1.0)*uResolution.xy/mr;",
    "  uv+=(uMouse-vec2(0.5))*uAmplitude;",
    "  float d=-uTime*0.5*uSpeed;float a=0.0;",
    "  for(float i=0.0;i<8.0;++i){a+=cos(i-d-a*uv.x);d+=sin(uv.y*i+a);}",
    "  d+=uTime*0.5*uSpeed;",
    "  vec3 col=vec3(cos(uv*vec2(d,a))*0.6+0.4,cos(a+d)*0.5+0.5);",
    "  col=cos(col*cos(vec3(d,a,2.5))*0.5+0.5)*uColor;",
    "  gl_FragColor=vec4(col,1.0);",
    "}"
  ].join("\n");

  function compile(type, src) {
    var sh = gl.createShader(type);
    gl.shaderSource(sh, src); gl.compileShader(sh);
    return gl.getShaderParameter(sh, gl.COMPILE_STATUS) ? sh : null;
  }
  var vs = compile(gl.VERTEX_SHADER, VERT), fs = compile(gl.FRAGMENT_SHADER, FRAG);
  if (!vs || !fs) { host.setAttribute("data-irid", "off"); return; }
  var prog = gl.createProgram();
  gl.attachShader(prog, vs); gl.attachShader(prog, fs); gl.linkProgram(prog);
  if (!gl.getProgramParameter(prog, gl.LINK_STATUS)) { host.setAttribute("data-irid", "off"); return; }
  gl.useProgram(prog);

  var buf = gl.createBuffer();
  gl.bindBuffer(gl.ARRAY_BUFFER, buf);
  gl.bufferData(gl.ARRAY_BUFFER, new Float32Array([-1, -1, 0, 0, 3, -1, 2, 0, -1, 3, 0, 2]), gl.STATIC_DRAW);
  var aPos = gl.getAttribLocation(prog, "position"), aUv = gl.getAttribLocation(prog, "uv");
  gl.enableVertexAttribArray(aPos); gl.vertexAttribPointer(aPos, 2, gl.FLOAT, false, 16, 0);
  gl.enableVertexAttribArray(aUv); gl.vertexAttribPointer(aUv, 2, gl.FLOAT, false, 16, 8);

  var uTime = gl.getUniformLocation(prog, "uTime");
  var uRes = gl.getUniformLocation(prog, "uResolution");
  var uMouse = gl.getUniformLocation(prog, "uMouse");
  gl.uniform3f(gl.getUniformLocation(prog, "uColor"), 0.3, 0.42, 0.82);
  gl.uniform1f(gl.getUniformLocation(prog, "uAmplitude"), 0.08);
  gl.uniform1f(gl.getUniformLocation(prog, "uSpeed"), 0.32);

  var reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var DPR = Math.min(window.devicePixelRatio || 1, 1.5);
  var mouse = { x: 0.5, y: 0.5 }, smooth = { x: 0.5, y: 0.5 };
  var raf = 0, inView = true;

  function resize() {
    var w = Math.max(1, Math.round(canvas.clientWidth * DPR));
    var h = Math.max(1, Math.round(canvas.clientHeight * DPR));
    if (canvas.width === w && canvas.height === h) return;
    canvas.width = w; canvas.height = h;
    gl.viewport(0, 0, w, h);
    gl.uniform3f(uRes, w, h, w / h);
  }
  resize();

  window.addEventListener("mousemove", function (e) {
    var r = canvas.getBoundingClientRect();
    mouse.x = (e.clientX - r.left) / r.width;
    mouse.y = 1 - (e.clientY - r.top) / r.height;
  }, { passive: true });

  function frame(t) {
    raf = requestAnimationFrame(frame);
    if (document.hidden || !inView) return;
    smooth.x += (mouse.x - smooth.x) * 0.04;
    smooth.y += (mouse.y - smooth.y) * 0.04;
    gl.uniform2f(uMouse, smooth.x, smooth.y);
    gl.uniform1f(uTime, reduced ? 8.4 : t * 0.001);
    gl.drawArrays(gl.TRIANGLES, 0, 3);
    if (reduced) { cancelAnimationFrame(raf); raf = 0; }
  }
  raf = requestAnimationFrame(frame);
  requestAnimationFrame(function () { canvas.classList.add("on"); });

  if ("ResizeObserver" in window) {
    new ResizeObserver(function () { resize(); if (reduced) gl.drawArrays(gl.TRIANGLES, 0, 3); }).observe(canvas);
  }
  if ("IntersectionObserver" in window) {
    new IntersectionObserver(function (en) { inView = en[0].isIntersecting; }, { threshold: 0 }).observe(canvas);
  }
  canvas.addEventListener("webglcontextlost", function (e) {
    e.preventDefault();
    if (raf) cancelAnimationFrame(raf);
    host.setAttribute("data-irid", "off");
  });
})();
</script>

</body></html>
```

