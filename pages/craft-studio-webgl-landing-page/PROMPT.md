INSTALANDING.AI · CRAFT Studio WebGL Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
CRAFT Studio WebGL Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/craft-studio-webgl-landing-page

craft-studio.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · CRAFT Studio WebGL Landing Page
  slug     craft-studio-webgl-landing-page
  prompt   https://instalanding.ai/p/craft-studio-webgl-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/craft-studio-webgl-landing-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    two :root blocks in <style>: --bg #e8e9ec, --paper, --ink #0d0f14, --mute, --line, --prism (the only accent,
            a 5-stop gradient), --ease cubic-bezier(.7,0,.2,1), --pad; then --serif (Instrument Serif), --mono
            (JetBrains Mono), --lift. Body face: Inter Tight (Google Fonts)
  sections  nav, hero, product, about, features, customers, metrics, pricing, contact, footer
  scripts   import map: Three.js 0.170 + addons (jsDelivr)
            classic <script>: word-by-word statement lighting, reveals, count-ups, footer clock, billing toggle, forms
            module 1: hero, glass TorusKnot (MeshPhysicalMaterial + RoomEnvironment) over the headline as a CanvasTexture
            module 2: lens bands, the same glass knot rendered over each [data-lens] band on #lens-layer
  assets    none binary: CSS/SVG only, SVG-noise grain as a data: URI; fonts from Google Fonts

  ADAPTING
  - The hero headline is read from the sr-only <h1 id="headline"> spans and drawn into the WebGL scene; edit
    those spans (and .hero-fallback, shown under html.no-webgl), not the canvas. BG/INK in module 1 duplicate
    --bg/--ink: change both.
  - Both modules wait for document.fonts.load('900 100px "Inter Tight"') before drawing; swap the family there
    too, or the canvas type renders in a fallback face.
  - Each lens band carries data-lens-bg / data-lens-ink; they must match the section it sits on or the glass
    shows a seam. The hero loop only runs while .hero-spacer is on screen (IntersectionObserver).
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Refract AI</title>
<meta name="description" content="Refract is the AI platform for teams that ship: retrieval, agents, evals and guardrails on your own data." />

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600;700;900&family=Instrument+Serif:ital@0;1&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />

<style>
:root {
  --bg: #e8e9ec;
  --paper: #f3f4f6;
  --ink: #0d0f14;
  --mute: rgba(13, 15, 20, 0.56);
  --line: rgba(13, 15, 20, 0.14);
  /* The only accent: the dispersion spectrum the glass knot throws */
  --prism: linear-gradient(90deg, #ff3b3b, #ffb000, #2fd27a, #1e90ff, #a24bff);
  --ease: cubic-bezier(0.7, 0, 0.2, 1);
  --pad: 40px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html { scroll-behavior: smooth; }

body {
  background: var(--bg);
  color: var(--ink);
  font-family: "Inter Tight", system-ui, sans-serif;
  -webkit-font-smoothing: antialiased;
  overflow-x: hidden;
}

::selection { background: var(--ink); color: var(--bg); }

#scene {
  position: fixed;
  inset: 0;
  display: block;
}

/* Shown only when WebGL is unavailable: the headline as real type */
.hero-fallback {
  position: fixed;
  inset: 0;
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-weight: 900;
  font-size: clamp(56px, 15vw, 260px);
  line-height: 0.86;
  letter-spacing: -0.045em;
  text-transform: uppercase;
  text-align: center;
}
.no-webgl .hero-fallback { display: flex; }
.no-webgl #scene { display: none; }

/* White + difference renders as ink on light sections and paper on dark ones */
.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 28px var(--pad);
  z-index: 20;
  color: #fff;
  mix-blend-mode: difference;
}

.nav__logo {
  font-weight: 900;
  font-size: 18px;
  letter-spacing: -0.02em;
  text-transform: uppercase;
  color: inherit;
  text-decoration: none;
}

.nav__links {
  display: flex;
  gap: 32px;
  list-style: none;
}

.nav__links a {
  color: inherit;
  text-decoration: none;
  font-size: 13px;
  font-weight: 500;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  opacity: 0.7;
  transition: opacity 0.25s ease;
}

.nav__links a:hover,
.nav__links a:focus-visible {
  opacity: 1;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  overflow: hidden;
  clip-path: inset(50%);
  white-space: nowrap;
}

.meta {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 28px var(--pad);
  z-index: 2;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  opacity: 0.6;
  pointer-events: none;
}
.meta__scroll { display: inline-flex; align-items: center; gap: 10px; }
.meta__scroll::after {
  content: "";
  width: 1px;
  height: 22px;
  background: currentColor;
  transform-origin: top;
  animation: drip 1.8s var(--ease) infinite;
}
@keyframes drip {
  0% { transform: scaleY(0); }
  50% { transform: scaleY(1); transform-origin: top; }
  51% { transform-origin: bottom; }
  100% { transform: scaleY(0); transform-origin: bottom; }
}

/* ================= Content: sections slide up over the fixed scene ================= */
main { position: relative; z-index: 1; }
.hero-spacer { height: 100vh; height: 100svh; }

.section {
  position: relative;
  padding: 140px var(--pad);
  background: var(--bg);
  border-top: 1px solid var(--line);
}

.label {
  display: flex;
  gap: 18px;
  margin-bottom: 56px;
  font-size: 12px;
  font-weight: 500;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--mute);
}
.label span:first-child { color: var(--ink); }

.display {
  font-weight: 900;
  font-size: clamp(56px, 12vw, 220px);
  line-height: 0.84;
  letter-spacing: -0.045em;
  text-transform: uppercase;
}

.link-arrow {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  color: var(--ink);
  font-size: 13px;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  text-decoration: none;
  padding-bottom: 4px;
  background: linear-gradient(currentColor, currentColor) 0 100% / 100% 1px no-repeat;
  transition: background-size 0.4s var(--ease);
}
.link-arrow:hover { background-size: 0 1px; background-position: 100% 100%; }

/* ---------- 01 Studio: statement lights up word by word as you scroll ---------- */
.statement {
  max-width: 1280px;
  font-size: clamp(30px, 4.6vw, 76px);
  font-weight: 600;
  line-height: 1.04;
  letter-spacing: -0.035em;
}
.statement .w { opacity: 0.14; transition: opacity 0.25s linear; }
.statement .w.is-lit { opacity: 1; }
.statement em {
  font-style: normal;
  background: var(--prism);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
.intro-foot {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  gap: 32px;
  flex-wrap: wrap;
  margin-top: 88px;
}
.intro-foot p { max-width: 360px; font-size: 15px; line-height: 1.55; color: var(--mute); }

/* ---------- 02 Capabilities ---------- */
.svc { list-style: none; border-top: 1px solid var(--ink); }
.svc-row {
  position: relative;
  display: grid;
  grid-template-columns: 80px 1fr minmax(0, 380px) 48px;
  align-items: center;
  gap: 24px;
  padding: 34px 0;
  border-bottom: 1px solid var(--ink);
  overflow: hidden;
  isolation: isolate;
  cursor: default;
}
/* ink wipe from the bottom on hover */
.svc-row::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  background: var(--ink);
  transform: scaleY(0);
  transform-origin: bottom;
  transition: transform 0.55s var(--ease);
}
.svc-row:hover::before { transform: scaleY(1); }
.svc-row > * { transition: color 0.4s var(--ease), translate 0.55s var(--ease); }
.svc-row:hover > * { color: var(--bg); }
.svc-row:hover h3 { translate: 18px 0; }
.svc-num { font-size: 13px; font-weight: 600; letter-spacing: 0.04em; }
.svc-row h3 { font-size: clamp(32px, 5.4vw, 92px); font-weight: 900; line-height: 0.9; letter-spacing: -0.04em; text-transform: uppercase; }
.svc-row p { font-size: 15px; line-height: 1.5; color: var(--mute); }
.svc-row:hover p { color: rgba(232, 233, 236, 0.7); }
.svc-arrow { justify-self: end; font-size: 28px; transition: rotate 0.55s var(--ease), color 0.4s; }
.svc-row:hover .svc-arrow { rotate: 45deg; }

/* ---------- 03 Selected work ---------- */
.work-head { display: flex; justify-content: space-between; align-items: flex-end; gap: 24px; margin-bottom: 64px; flex-wrap: wrap; }
.work-head .display { font-size: clamp(56px, 10vw, 180px); }
.work-count { font-size: 13px; font-weight: 600; letter-spacing: 0.04em; text-transform: uppercase; }
.work-grid {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 88px 24px;
}
.project { color: var(--ink); text-decoration: none; display: block; }
.project:nth-child(1) { grid-column: 1 / span 7; }
.project:nth-child(2) { grid-column: 9 / span 4; margin-top: 180px; }
.project:nth-child(3) { grid-column: 2 / span 4; margin-top: 120px; }
.project:nth-child(4) { grid-column: 7 / span 6; }
.cover {
  position: relative;
  overflow: hidden;
  aspect-ratio: 4 / 3;
  background: var(--paper);
  container-type: size;
}
.project:nth-child(2) .cover,
.project:nth-child(3) .cover { aspect-ratio: 4 / 5; }
.cover-art { position: absolute; inset: 0; transition: scale 1.1s var(--ease); }
.project:hover .cover-art { scale: 1.03; }
.project-meta {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 4px 16px;
  margin-top: 18px;
  padding-top: 14px;
  border-top: 1px solid var(--ink);
}
.project-meta h3 { font-size: 22px; font-weight: 700; letter-spacing: -0.02em; }
.project-meta span { font-size: 12px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.project-meta .year { grid-row: 1; grid-column: 2; align-self: center; color: var(--ink); }


/* ---------- 04 Numbers (dark) ---------- */
.numbers { background: var(--ink); color: var(--bg); border-top: 0; }
.numbers .label { color: rgba(233, 233, 231, 0.55); }
.numbers .label span:first-child { color: var(--bg); }
.stats { display: grid; grid-template-columns: repeat(4, 1fr); border-top: 1px solid rgba(233, 233, 231, 0.2); }
.stat { padding: 28px 24px 0 0; }
.stat + .stat { padding-left: 24px; border-left: 1px solid rgba(233, 233, 231, 0.2); }
.stat-num { display: block; font-size: clamp(52px, 6.4vw, 116px); font-weight: 900; line-height: 0.9; letter-spacing: -0.05em; font-variant-numeric: tabular-nums; }
.stat-label { display: block; margin-top: 14px; font-size: 12px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; color: rgba(233, 233, 231, 0.6); }
.quote {
  max-width: 1100px;
  margin: 140px 0 0 auto;
  font-size: clamp(26px, 3.4vw, 54px);
  font-weight: 600;
  line-height: 1.1;
  letter-spacing: -0.03em;
}
.quote-by { display: block; margin-top: 28px; font-size: 13px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; color: rgba(233, 233, 231, 0.6); }
.clients {
  display: flex;
  gap: 64px;
  margin: 140px calc(var(--pad) * -1) 0;
  padding: 28px 0;
  border-block: 1px solid rgba(233, 233, 231, 0.2);
  overflow: hidden;
}
.clients-track {
  display: flex;
  flex-shrink: 0;
  gap: 64px;
  min-width: 100%;
  justify-content: space-around;
  animation: marquee 30s linear infinite;
}
.clients:hover .clients-track { animation-play-state: paused; }
@keyframes marquee { to { transform: translateX(calc(-100% - 64px)); } }
.clients-track span { font-size: clamp(28px, 3.4vw, 52px); font-weight: 900; letter-spacing: -0.04em; text-transform: uppercase; white-space: nowrap; opacity: 0.85; }
.clients-track span:nth-child(3n + 2) { font-weight: 400; letter-spacing: -0.02em; text-transform: none; }

/* ---------- 05 Contact ---------- */
.contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: end; }
.mail {
  display: inline-block;
  margin-top: 40px;
  color: var(--ink);
  font-size: clamp(22px, 2.6vw, 40px);
  font-weight: 700;
  letter-spacing: -0.02em;
  text-decoration: none;
  background: linear-gradient(var(--ink), var(--ink)) 0 100% / 100% 2px no-repeat;
  padding-bottom: 6px;
  transition: color 0.3s;
}
.mail:hover { background-image: var(--prism); background-clip: text; -webkit-background-clip: text; color: transparent; background-size: 100% 100%; }
.brief { display: grid; grid-template-columns: 1fr 1fr; gap: 28px 24px; }
.field { position: relative; display: flex; flex-direction: column; gap: 8px; }
.field--full { grid-column: 1 / -1; }
.field > span { font-size: 12px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.field input,
.field textarea {
  width: 100%;
  padding: 10px 0;
  border: 0;
  border-bottom: 1px solid var(--ink);
  border-radius: 0;
  background: transparent;
  color: var(--ink);
  font: 500 18px "Inter Tight", sans-serif;
  outline: none;
  resize: none;
}
.field textarea { height: 96px; }
.field input:focus,
.field textarea:focus { border-bottom-width: 2px; padding-bottom: 9px; }
.field.is-invalid input,
.field.is-invalid textarea { border-bottom-color: #d12b2b; }
.field .err { min-height: 16px; font-size: 12px; color: #d12b2b; }
.budget { display: flex; flex-wrap: wrap; gap: 8px; border: 0; }
.budget legend { margin-bottom: 10px; font-size: 12px; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.budget label { position: relative; }
.budget input { position: absolute; opacity: 0; }
.budget span {
  display: inline-block;
  padding: 10px 18px;
  border: 1px solid var(--ink);
  border-radius: 999px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.25s, color 0.25s;
}
.budget input:checked + span { background: var(--ink); color: var(--bg); }
.budget input:focus-visible + span { outline: 2px solid var(--ink); outline-offset: 3px; }
.brief-foot { grid-column: 1 / -1; display: flex; justify-content: space-between; align-items: center; gap: 24px; }
.brief-status { font-size: 14px; font-weight: 500; }
.send {
  position: relative;
  display: grid;
  place-items: center;
  width: 128px;
  height: 128px;
  flex-shrink: 0;
  border: 0;
  border-radius: 50%;
  background: var(--ink);
  color: var(--bg);
  font: 700 13px "Inter Tight", sans-serif;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  cursor: pointer;
  overflow: hidden;
  isolation: isolate;
  transition: scale 0.4s var(--ease);
}
.send::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  background: var(--prism);
  opacity: 0;
  transition: opacity 0.4s;
}
.send:hover { scale: 1.06; }
.send:hover::before { opacity: 1; }
.send:focus-visible { outline: 2px solid var(--ink); outline-offset: 4px; }
.send[disabled] { cursor: progress; }

/* ---------- SaaS additions ---------- */
.nav__right { display: flex; align-items: center; gap: 32px; }
.nav__cta {
  color: inherit; text-decoration: none; font-size: 13px; font-weight: 600;
  letter-spacing: 0.04em; text-transform: uppercase;
  padding: 9px 16px; border: 1px solid currentColor; border-radius: 999px;
}
.nav__cta:hover { background: #fff; color: #000; }
.snippet {
  flex: 1 1 420px; max-width: 560px; min-width: 0;
  padding: 22px 24px; border-radius: 14px;
  background: var(--ink); color: #c9ccd4;
  font: 500 13px/1.7 ui-monospace, "SFMono-Regular", Menlo, Consolas, monospace;
  overflow-x: auto; white-space: pre;
}
.snippet .k { color: #7fb4ff; } .snippet .s { color: #8fe0a8; } .snippet .c { color: #6b7080; }
.snippet .bar { display: flex; gap: 6px; margin-bottom: 14px; }
.snippet .bar i { width: 10px; height: 10px; border-radius: 50%; background: #2a2e38; }
.intro-side { display: flex; flex-direction: column; gap: 28px; align-items: flex-start; }
.status { display: flex; align-items: center; gap: 8px; }
.status::before { content: ""; width: 8px; height: 8px; border-radius: 50%; background: #2fd27a; box-shadow: 0 0 0 4px rgba(47, 210, 122, 0.2); }

/* ---------- Reveals ---------- */
.reveal { opacity: 0; translate: 0 40px; transition: opacity 1s var(--ease), translate 1s var(--ease); }
.reveal.is-in { opacity: 1; translate: 0 0; }

/* ================= Premium layer ================= */
:root {
  --surface: rgba(255, 255, 255, 0.62);
  --serif: "Instrument Serif", "Iowan Old Style", Georgia, serif;
  --mono: "JetBrains Mono", ui-monospace, Menlo, Consolas, monospace;
  --lift: inset 0 1px 0 rgba(255, 255, 255, 0.9), 0 1px 2px rgba(13, 15, 20, 0.04), 0 18px 40px -22px rgba(13, 15, 20, 0.28);
}
body::after {
  content: ""; position: fixed; inset: 0; z-index: 40; pointer-events: none;
  opacity: 0.05; mix-blend-mode: multiply; background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='180' height='180'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}

/* Floating glass nav */
.nav {
  top: calc(14px + env(safe-area-inset-top, 0px)); left: 50%; right: auto; translate: -50% 0;
  width: min(1120px, calc(100% - 32px));
  padding: 8px 8px 8px 24px;
  color: var(--ink); mix-blend-mode: normal;
  background: var(--surface);
  -webkit-backdrop-filter: blur(18px) saturate(1.5); backdrop-filter: blur(18px) saturate(1.5);
  border: 1px solid rgba(255, 255, 255, 0.75); border-radius: 999px;
  box-shadow: 0 1px 2px rgba(13, 15, 20, 0.05), 0 12px 32px -14px rgba(13, 15, 20, 0.25);
}
.nav__links a { opacity: 0.62; }
.nav__cta { background: var(--ink); color: #fff; border-color: var(--ink); padding: 11px 20px; box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.18); }
.nav__cta:hover { background: #262a33; color: #fff; }

/* Hero calls to action */
.hero-spacer { display: flex; align-items: flex-end; justify-content: center; padding-bottom: 104px; }
.hero-cta { display: flex; gap: 12px; }
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 10px;
  height: 50px; padding: 0 26px; border-radius: 999px;
  font-size: 14px; font-weight: 600; letter-spacing: 0.01em; text-decoration: none;
  transition: translate 0.35s var(--ease), box-shadow 0.35s var(--ease), background 0.3s;
}
.btn:hover { translate: 0 -2px; }
.btn:focus-visible, .nav__cta:focus-visible { outline: 2px solid var(--ink); outline-offset: 3px; }
.btn--ink { background: var(--ink); color: #fff; box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.18), 0 14px 28px -12px rgba(13, 15, 20, 0.6); }
.btn--glass {
  background: var(--surface); color: var(--ink); border: 1px solid rgba(255, 255, 255, 0.85);
  -webkit-backdrop-filter: blur(14px); backdrop-filter: blur(14px); box-shadow: var(--lift);
}

/* Type: serif accents, mono for metadata */
.serif { font-family: var(--serif); font-style: italic; font-weight: 400; text-transform: none; letter-spacing: -0.02em; }
.statement em { font-family: var(--serif); font-style: italic; font-weight: 400; letter-spacing: -0.015em; }
.label, .meta, .work-count, .stat-label, .quote-by, .project-meta span, .footer-cols h4, .footer-bottom, .field > span, .budget legend, .svc-num {
  font-family: var(--mono); font-size: 11.5px; letter-spacing: 0.04em;
}
.label { align-items: center; }
.label::before { content: ""; width: 7px; height: 7px; border-radius: 50%; background: var(--prism); }
.project-meta .year { font-family: "Inter Tight", system-ui, sans-serif; font-size: 15px; font-weight: 700; letter-spacing: -0.01em; }
.quote { font-family: var(--serif); font-weight: 400; font-size: clamp(32px, 4.2vw, 68px); line-height: 1.04; letter-spacing: -0.015em; }

/* Code card */
.snippet {
  border-radius: 20px; border: 1px solid transparent;
  background: linear-gradient(#10131a, #0b0d12) padding-box,
              linear-gradient(150deg, rgba(255, 255, 255, 0.22), rgba(255, 255, 255, 0.03) 40%, rgba(162, 75, 255, 0.35)) border-box;
  box-shadow: 0 40px 70px -36px rgba(13, 15, 20, 0.55);
  font-family: var(--mono);
}

/* Platform rows: quiet hover */
.svc { border-top-color: var(--line); }
.svc-row { border-bottom-color: var(--line); padding: 40px 12px; }
.svc-row::before { background: rgba(255, 255, 255, 0.7); }
.svc-row:hover > * { color: var(--ink); }
.svc-row:hover p { color: var(--mute); }
.svc-row:hover .svc-arrow { background: var(--prism); -webkit-background-clip: text; background-clip: text; color: transparent; }

/* Case study covers */
.cover { border-radius: 22px; box-shadow: var(--lift); }
.project-meta { border-top-color: var(--line); }

/* Metrics: inset dark panel */
.numbers { background: var(--bg); isolation: isolate; }
.numbers::before { content: ""; position: absolute; inset: 16px; z-index: -1; border-radius: 32px; background: var(--ink); }
.section.numbers { padding-inline: calc(var(--pad) + 32px); }
.clients {
  margin-inline: calc((var(--pad) + 16px) * -1);
  -webkit-mask: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
  mask: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
}

/* Contact card */
.brief { padding: 40px; border-radius: 28px; background: var(--surface); border: 1px solid rgba(255, 255, 255, 0.9); box-shadow: var(--lift); }
.field input, .field textarea { border-bottom-color: var(--line); }
.field input:focus, .field textarea:focus { border-bottom-color: var(--ink); }
.budget span { border-color: var(--line); background: rgba(255, 255, 255, 0.7); }
.send { box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.18), 0 20px 40px -18px rgba(13, 15, 20, 0.6); }


@media (max-width: 900px) {
  :root { --pad: 22px; }
  .section { padding: 96px var(--pad); }
  .svc-row { grid-template-columns: 48px 1fr 32px; }
  .svc-row p { grid-column: 2 / -1; grid-row: 2; }
  .work-grid { grid-template-columns: 1fr; gap: 56px; }
  .project:nth-child(n) { grid-column: 1 / -1; margin-top: 0; }
  .stats { grid-template-columns: 1fr 1fr; }
  .stat:nth-child(3) { padding-left: 0; border-left: 0; }
  .stat:nth-child(n + 3) { margin-top: 40px; }
  .contact-grid { grid-template-columns: 1fr; gap: 56px; }
}
@media (max-width: 640px) {
  .nav__links { display: none; }
  .nav,
  .meta {
    padding: 20px 22px;
  }

  .nav__links {
    gap: 18px;
  }
  .brief { grid-template-columns: 1fr; }
  .send { width: 104px; height: 104px; }
  .quote { margin-top: 96px; }
  .clients, .quote { margin-top: 96px; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  .reveal { opacity: 1; translate: none; }
  .statement .w { opacity: 1; }
  .clients-track, .meta__scroll::after { animation: none; }
}
@media (max-width: 640px) {
  .nav { top: calc(10px + env(safe-area-inset-top, 0px)); width: calc(100% - 20px); padding: 6px 6px 6px 18px; }
  .hero-spacer { padding-bottom: 92px; }
  .hero-cta { flex-direction: column; width: 100%; padding-inline: 22px; }
  .numbers::before { inset: 10px 8px; border-radius: 24px; }
  .section.numbers { padding-inline: calc(var(--pad) + 12px); }
  .clients { margin-inline: calc((var(--pad) + 4px) * -1); }
  .brief { padding: 26px 20px; }
}
/* ---------- Product mockup ---------- */
.section.showcase { padding-block: 24px 140px; border-top: 0; }
.app {
  max-width: 1180px; margin: 0 auto; overflow: hidden;
  border-radius: 22px; background: rgba(255, 255, 255, 0.72); border: 1px solid rgba(255, 255, 255, 0.95);
  box-shadow: 0 1px 2px rgba(13, 15, 20, 0.05), 0 70px 120px -60px rgba(13, 15, 20, 0.5);
}
.app-bar { display: flex; align-items: center; gap: 16px; padding: 13px 18px; border-bottom: 1px solid var(--line); }
.app-dots { display: flex; gap: 6px; flex-shrink: 0; }
.app-dots i { width: 11px; height: 11px; border-radius: 50%; background: #d3d6dc; }
.app-url { flex: 1; max-width: 420px; margin: 0 auto; padding: 6px 14px; border-radius: 8px; background: rgba(13, 15, 20, 0.05); font: 500 12px var(--mono); color: var(--mute); text-align: center; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.app-bar-pad { width: 45px; flex-shrink: 0; }
.app-body { display: grid; grid-template-columns: 220px minmax(0, 1fr) 280px; min-height: 540px; }
.app-side { display: flex; flex-direction: column; gap: 22px; padding: 20px 14px; border-right: 1px solid var(--line); }
.app-group h5 { padding: 0 10px 8px; font: 500 10.5px var(--mono); letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.app-item { display: flex; align-items: center; gap: 10px; padding: 8px 10px; border-radius: 9px; font-size: 13.5px; font-weight: 500; }
.app-item.is-active { background: #fff; box-shadow: var(--lift); }
.app-item .dot { width: 7px; height: 7px; border-radius: 50%; background: #2fd27a; }
.app-item .dot.idle { background: #c4c7cf; }
.app-item .count { margin-left: auto; font: 500 11px var(--mono); color: var(--mute); }
.app-main { display: flex; flex-direction: column; gap: 18px; min-width: 0; padding: 26px 30px; }
.app-head { display: flex; justify-content: space-between; align-items: center; gap: 12px; flex-wrap: wrap; }
.app-head h4 { font-size: 17px; font-weight: 700; letter-spacing: -0.01em; }
.pill { display: inline-flex; align-items: center; gap: 6px; padding: 4px 10px; border-radius: 999px; background: rgba(47, 210, 122, 0.15); color: #127a45; font: 500 11px var(--mono); }
.pill::before { content: ""; width: 6px; height: 6px; border-radius: 50%; background: currentColor; }
.msg { max-width: 580px; padding: 14px 16px; border-radius: 14px; font-size: 14.5px; line-height: 1.5; }
.msg--user { align-self: flex-end; background: var(--ink); color: #fff; border-bottom-right-radius: 4px; }
.msg--agent { background: #fff; box-shadow: var(--lift); border-bottom-left-radius: 4px; }
.steps { display: flex; flex-wrap: wrap; gap: 6px; margin-bottom: 12px; }
.step { padding: 4px 8px; border-radius: 6px; background: rgba(13, 15, 20, 0.05); color: var(--mute); font: 500 11px var(--mono); }
.step b { color: var(--ink); font-weight: 500; }
.cite { display: inline-grid; place-items: center; min-width: 17px; height: 17px; margin-left: 2px; padding: 0 4px; border-radius: 5px; background: rgba(30, 144, 255, 0.12); color: #1667c2; font: 600 10px var(--mono); vertical-align: 2px; }
.sources { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 14px; }
.source { min-width: 0; padding: 10px 12px; border-radius: 10px; border: 1px solid var(--line); font-size: 12.5px; line-height: 1.35; }
.source span { display: block; margin-bottom: 3px; color: var(--mute); font: 500 10.5px var(--mono); }
.composer { display: flex; align-items: center; gap: 10px; margin-top: auto; padding: 8px 8px 8px 16px; border-radius: 14px; background: #fff; border: 1px solid var(--line); color: var(--mute); font-size: 14px; }
.composer i { display: grid; place-items: center; width: 32px; height: 32px; margin-left: auto; border-radius: 9px; background: var(--ink); color: #fff; font-style: normal; font-size: 15px; }
.app-trace { display: flex; flex-direction: column; gap: 18px; padding: 22px 20px; border-left: 1px solid var(--line); background: rgba(255, 255, 255, 0.4); }
.app-trace h5 { font: 500 10.5px var(--mono); letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.trace-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; }
.metric { padding: 12px; border-radius: 12px; background: #fff; box-shadow: var(--lift); }
.metric span { display: block; color: var(--mute); font: 500 10px var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
.metric b { display: block; margin-top: 4px; font-size: 20px; font-weight: 700; letter-spacing: -0.02em; font-variant-numeric: tabular-nums; }
.spark { padding: 12px; border-radius: 12px; background: #fff; box-shadow: var(--lift); }
.spark svg { display: block; width: 100%; height: 56px; margin-top: 8px; }
.spark-head { display: flex; justify-content: space-between; color: var(--mute); font: 500 10px var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
.spark-head b { color: var(--ink); font-weight: 500; }
.checks { list-style: none; display: flex; flex-direction: column; gap: 9px; font-size: 13px; }
.checks li { display: flex; align-items: center; gap: 9px; }
.checks li::before { content: "✓"; display: grid; place-items: center; width: 18px; height: 18px; border-radius: 50%; background: rgba(47, 210, 122, 0.16); color: #127a45; font-size: 10px; font-weight: 700; }

/* ---------- Pricing ---------- */
.pricing-head { display: flex; justify-content: space-between; align-items: flex-end; gap: 24px; flex-wrap: wrap; margin-bottom: 56px; }
.pricing-head .display { font-size: clamp(56px, 10vw, 180px); }
.billing { display: inline-flex; padding: 4px; border-radius: 999px; background: var(--surface); border: 1px solid rgba(255, 255, 255, 0.9); box-shadow: var(--lift); }
.billing button { padding: 9px 16px; border: 0; border-radius: 999px; background: transparent; color: var(--mute); font: 600 13px "Inter Tight", system-ui, sans-serif; cursor: pointer; transition: background 0.3s, color 0.3s; }
.billing button[aria-pressed="true"] { background: var(--ink); color: #fff; }
.billing button:focus-visible { outline: 2px solid var(--ink); outline-offset: 2px; }
.billing small { margin-left: 6px; color: #127a45; font: 500 10.5px var(--mono); }
.billing button[aria-pressed="true"] small { color: #8fe0a8; }
.plans { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 20px; }
.plan { display: flex; flex-direction: column; gap: 22px; padding: 32px; border-radius: 26px; background: var(--surface); border: 1px solid rgba(255, 255, 255, 0.9); box-shadow: var(--lift); }
.plan--featured { border: 1.5px solid transparent; background: linear-gradient(#fff, #fff) padding-box, var(--prism) border-box; box-shadow: 0 50px 90px -45px rgba(13, 15, 20, 0.5); }
.plan-top { display: flex; justify-content: space-between; align-items: center; gap: 12px; }
.plan h3 { font-size: 20px; font-weight: 700; letter-spacing: -0.01em; }
.plan-tag { padding: 4px 10px; border-radius: 999px; background: var(--ink); color: #fff; font: 500 10.5px var(--mono); letter-spacing: 0.05em; text-transform: uppercase; }
.price { display: flex; align-items: baseline; gap: 10px; flex-wrap: wrap; }
.price b { font-size: clamp(48px, 4.8vw, 68px); font-weight: 900; line-height: 1; letter-spacing: -0.045em; font-variant-numeric: tabular-nums; }
.price span { color: var(--mute); font: 500 12px var(--mono); }
.plan p { color: var(--mute); font-size: 14.5px; line-height: 1.5; }
.plan ul { list-style: none; display: flex; flex-direction: column; gap: 11px; padding-top: 22px; border-top: 1px solid var(--line); font-size: 14px; }
.plan li { display: flex; gap: 10px; line-height: 1.4; }
.plan li::before { content: "✓"; flex-shrink: 0; color: var(--mute); font-size: 12px; line-height: 1.6; }
.plan .btn { margin-top: auto; }
.btn--line { background: #fff; color: var(--ink); border: 1px solid var(--line); box-shadow: var(--lift); }
.pricing-note { margin-top: 28px; color: var(--mute); font: 500 12px var(--mono); }

@media (max-width: 1100px) {
  .app-body { grid-template-columns: 200px minmax(0, 1fr); }
  .app-trace { display: none; }
}
@media (max-width: 900px) {
  .plans { grid-template-columns: 1fr; }
}
@media (max-width: 700px) {
  .app-body { grid-template-columns: 1fr; min-height: 0; }
  .app-side { display: none; }
  .app-main { padding: 20px 16px; }
  .sources { grid-template-columns: 1fr; }
  .app-bar-pad { display: none; }
  .plan { padding: 26px 22px; }
}

/* ---------- Lens bands: the glass knot returns down the page ---------- */
#lens-layer { position: fixed; inset: 0; z-index: 5; display: block; pointer-events: none; }
.no-webgl #lens-layer { display: none; }
.lens {
  position: relative; display: grid; place-items: center; overflow: hidden;
  width: 100%; aspect-ratio: 3.2 / 1; min-height: 200px; max-height: 520px;
  container-type: inline-size;
}
.lens > span {
  font-weight: 900; font-size: var(--fit, 18cqi); line-height: 1; letter-spacing: -0.045em;
  text-transform: uppercase; white-space: nowrap; color: var(--ink);
}
.lens--dark > span { color: var(--bg); }
.knot-ready .lens > span { visibility: hidden; }
.lens-caption { display: flex; justify-content: space-between; gap: 16px; margin-top: 14px; color: var(--mute); font: 500 11.5px var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
.numbers .lens-caption { color: rgba(232, 233, 236, 0.55); }
.lens-wrap { margin-top: 110px; }
.numbers .lens-wrap { margin: 0 0 72px; }

/* ---------- Footer: inset card ---------- */
.footer { position: relative; z-index: 1; padding: 16px; background: var(--bg); }
.foot {
  overflow: hidden; border-radius: 32px; background: #f6f7f9;
  border: 1px solid rgba(255, 255, 255, 0.95); box-shadow: var(--lift);
}
.foot .lens { max-height: 360px; aspect-ratio: 3.6 / 1; }
.foot-cta { display: flex; justify-content: space-between; align-items: flex-end; gap: 32px; flex-wrap: wrap; padding: 8px 48px 56px; border-bottom: 1px solid var(--line); }
.foot-cta h2 { max-width: 640px; font-size: clamp(30px, 3.6vw, 52px); font-weight: 700; line-height: 1.02; letter-spacing: -0.035em; text-wrap: balance; }
.foot-cta-actions { display: flex; gap: 12px; flex-wrap: wrap; }
.foot-main { display: grid; grid-template-columns: minmax(0, 1.5fr) repeat(3, minmax(0, 1fr)); gap: 40px; padding: 56px 48px; }
.foot-brand { display: flex; flex-direction: column; gap: 18px; align-items: flex-start; }
.foot-logo { font-size: 20px; font-weight: 900; letter-spacing: -0.02em; text-transform: uppercase; color: var(--ink); text-decoration: none; }
.foot-brand > p { max-width: 320px; color: var(--mute); font-size: 14.5px; line-height: 1.55; }
.foot-news { display: flex; width: 100%; max-width: 360px; padding: 5px; border-radius: 999px; background: #fff; border: 1px solid var(--line); }
.foot-news input { flex: 1; min-width: 0; padding: 0 14px; border: 0; background: transparent; color: var(--ink); font: 500 14px "Inter Tight", system-ui, sans-serif; outline: none; }
.foot-news button { height: 38px; padding: 0 16px; border: 0; border-radius: 999px; background: var(--ink); color: #fff; font: 600 13px "Inter Tight", system-ui, sans-serif; cursor: pointer; }
.foot-news:focus-within { border-color: var(--ink); }
.foot-news-msg { min-height: 16px; color: var(--mute); font: 500 11.5px var(--mono); }
.foot-col { display: flex; flex-direction: column; gap: 10px; }
.foot-col h4 { margin-bottom: 6px; color: var(--mute); font: 500 11.5px var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
.foot-col a { width: fit-content; color: var(--ink); font-size: 15px; font-weight: 500; text-decoration: none; background: linear-gradient(currentColor, currentColor) 0 100% / 0 1px no-repeat; transition: background-size 0.4s var(--ease); }
.foot-col a:hover { background-size: 100% 1px; }
.foot-bottom { display: flex; justify-content: space-between; align-items: center; gap: 16px 32px; flex-wrap: wrap; padding: 22px 48px 26px; border-top: 1px solid var(--line); color: var(--mute); font: 500 11.5px var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
.foot-legal { display: flex; gap: 24px; flex-wrap: wrap; }
.foot-legal a { color: inherit; text-decoration: none; }
.foot-legal a:hover { color: var(--ink); }
.foot-status { display: flex; align-items: center; gap: 16px; }

@media (max-width: 900px) {
  .foot-main { grid-template-columns: 1fr 1fr; }
  .foot-brand { grid-column: 1 / -1; }
}
@media (max-width: 640px) {
  .footer { padding: 10px; }
  .foot { border-radius: 24px; }
  .foot-cta, .foot-main, .foot-bottom { padding-inline: 22px; }
  .foot-main { gap: 32px 20px; }
  .lens-wrap { margin-top: 72px; }
  .lens-caption span:last-child { display: none; }
}

/* ---------- Case study scenes: each cover shows the agent doing that customer's job ---------- */
.scene {
  display: flex; flex-direction: column; justify-content: space-between; gap: clamp(8px, 2.6cqi, 16px);
  padding: clamp(16px, 5.5cqi, 36px); overflow: hidden;
  font-size: clamp(11px, 3cqi, 14px); line-height: 1.4;
}
.scene > * { position: relative; z-index: 1; }
.scene-tag { display: flex; align-items: center; gap: 8px; font: 500 clamp(9.5px, 2.3cqi, 11.5px) var(--mono); letter-spacing: 0.05em; text-transform: uppercase; opacity: 0.7; }
.scene-tag .live { width: 7px; height: 7px; border-radius: 50%; background: #2fd27a; box-shadow: 0 0 0 3px rgba(47, 210, 122, 0.22); animation: pulse 2s ease-in-out infinite; }
@keyframes pulse { 50% { box-shadow: 0 0 0 6px rgba(47, 210, 122, 0); } }
.scene-big { position: absolute; z-index: 0; pointer-events: none; font-weight: 900; line-height: 0.8; letter-spacing: -0.06em; white-space: nowrap; }
.mono { font-family: var(--mono); }

/* Staged entrances. Every cycle rests fully built, and the negative delay makes the first frame complete too */
.s1, .s2, .s3, .s4 { animation: 9s var(--ease) -6s infinite both; }
.s1 { animation-name: pop1; } .s2 { animation-name: pop2; } .s3 { animation-name: pop3; } .s4 { animation-name: pop4; }
@keyframes pop1 { 0%, 4% { opacity: 0; translate: 0 10px; } 11%, 90% { opacity: 1; translate: 0 0; } 97%, 100% { opacity: 0; } }
@keyframes pop2 { 0%, 18% { opacity: 0; translate: 0 10px; } 25%, 90% { opacity: 1; translate: 0 0; } 97%, 100% { opacity: 0; } }
@keyframes pop3 { 0%, 32% { opacity: 0; translate: 0 10px; } 39%, 90% { opacity: 1; translate: 0 0; } 97%, 100% { opacity: 0; } }
@keyframes pop4 { 0%, 46% { opacity: 0; translate: 0 10px; } 53%, 90% { opacity: 1; translate: 0 0; } 97%, 100% { opacity: 0; } }
.cover:not(.is-live) .scene, .cover:not(.is-live) .scene * { animation-play-state: paused; }

/* Nova Bank: a refund ticket resolved end to end */
.scene--nova { background: radial-gradient(120% 90% at 100% 0%, #1d2230, var(--ink) 65%); color: #e8e9ec; }
.scene--nova .scene-big { right: -2cqi; bottom: -5cqi; font-size: 24cqi; color: transparent; -webkit-text-stroke: 1.5px rgba(232, 233, 236, 0.13); }
.chat { display: flex; flex-direction: column; gap: clamp(6px, 1.8cqi, 10px); max-width: 92%; }
.bub { max-width: 78%; padding: 0.75em 1em; border-radius: 1.1em; }
.bub--in { align-self: flex-start; background: rgba(232, 233, 236, 0.09); border: 1px solid rgba(232, 233, 236, 0.1); border-bottom-left-radius: 0.3em; }
.bub--out { align-self: flex-end; background: #fff; color: var(--ink); border-bottom-right-radius: 0.3em; box-shadow: 0 20px 40px -20px rgba(0, 0, 0, 0.6); }
.chips { display: flex; flex-wrap: wrap; gap: 4px; margin-bottom: 0.6em; }
.chips span { padding: 0.2em 0.6em; border-radius: 0.4em; background: rgba(13, 15, 20, 0.06); color: var(--mute); font: 500 0.78em var(--mono); }
.resolved { align-self: flex-end; display: inline-flex; gap: 6px; padding: 0.35em 0.8em; border-radius: 999px; background: rgba(47, 210, 122, 0.16); color: #8fe0a8; font: 500 0.8em var(--mono); }
.compare { display: grid; grid-template-columns: auto 1fr auto; align-items: center; gap: 6px 10px; max-width: 64%; font: 500 0.78em var(--mono); color: rgba(232, 233, 236, 0.6); }
.compare i { display: block; height: 6px; border-radius: 3px; background: rgba(232, 233, 236, 0.18); }
.compare .now { width: 38%; background: var(--prism); animation: grow 9s var(--ease) -6s infinite both; transform-origin: left; }
.compare b { color: #e8e9ec; font-weight: 500; }
@keyframes grow { 0%, 46% { scale: 0 1; } 60%, 92% { scale: 1 1; } 100% { scale: 0 1; } }

/* Halo Health: protocol search */
.scene--halo { background: linear-gradient(160deg, #f1f5f8, #dfe7ee); color: var(--ink); }
.scene--halo .scene-big { right: 2cqi; bottom: -4cqi; font: italic 400 80cqi/0.8 var(--serif); color: rgba(30, 144, 255, 0.09); letter-spacing: -0.04em; }
.search { display: flex; align-items: center; gap: 10px; padding: 0.8em 0.9em; border-radius: 0.9em; background: #fff; box-shadow: var(--lift); }
.search::before { content: ""; width: 0.95em; height: 0.95em; flex-shrink: 0; border: 2px solid var(--mute); border-radius: 50%; }
.q { display: inline-block; overflow: hidden; white-space: nowrap; width: 27ch; font: 500 0.92em var(--mono); border-right: 2px solid #1e90ff; animation: type 9s steps(27, end) -6s infinite both; }
@keyframes type { 0%, 3% { width: 0; } 17%, 92% { width: 27ch; } 100% { width: 0; } }
.kbd { margin-left: auto; padding: 0.1em 0.45em; border: 1px solid var(--line); border-radius: 0.35em; color: var(--mute); font: 500 0.8em var(--mono); }
.results { list-style: none; display: flex; flex-direction: column; gap: clamp(6px, 1.8cqi, 9px); }
.r { display: grid; grid-template-columns: 1fr auto; gap: 2px 10px; padding: 0.75em 0.9em; border-radius: 0.8em; background: rgba(255, 255, 255, 0.78); border: 1px solid rgba(255, 255, 255, 0.95); }
.r b { font-weight: 600; }
.r span { grid-column: 1; color: var(--mute); font: 500 0.78em var(--mono); }
.r em { grid-row: 1 / 3; grid-column: 2; align-self: center; font: normal 600 0.8em var(--mono); color: #1667c2; }
.timer { display: flex; align-items: baseline; gap: 14px; flex-wrap: wrap; font: 500 0.8em var(--mono); color: var(--mute); }
.timer b { color: var(--ink); font: 700 1.9em "Inter Tight", system-ui, sans-serif; letter-spacing: -0.03em; }
.timer s { text-decoration-thickness: 1px; }

/* Lumen Legal: a contract with risk flags */
.scene--lumen { background: linear-gradient(170deg, #e9ebef, #d9dce3); color: var(--ink); }
.scene--lumen .scene-big { left: -2cqi; bottom: -5cqi; font-size: 58cqi; color: rgba(13, 15, 20, 0.05); }
.doc { position: relative; overflow: hidden; padding: 1.1em 1.1em 1.3em; border-radius: 0.5em; background: #fff; box-shadow: var(--lift); rotate: -1.2deg; }
.doc-title { margin-bottom: 0.7em; font-weight: 700; font-size: 0.95em; }
.doc-title small { display: block; color: var(--mute); font: 500 0.78em var(--mono); }
.ln { display: block; height: 0.42em; margin-top: 0.55em; border-radius: 2px; background: rgba(13, 15, 20, 0.1); }
.ln.hl { background: transparent; box-shadow: inset 0 0 0 100vmax var(--hl); }
.ln.hl--r { --hl: rgba(255, 59, 59, 0.38); } .ln.hl--a { --hl: rgba(255, 176, 0, 0.5); } .ln.hl--g { --hl: rgba(47, 210, 122, 0.45); }
.scanbar { position: absolute; left: 0; right: 0; height: 2.4em; background: linear-gradient(180deg, transparent, rgba(30, 144, 255, 0.16)); border-bottom: 1.5px solid #1e90ff; animation: scan 9s linear -6s infinite both; }
@keyframes scan { 0% { top: -2.4em; opacity: 1; } 50% { top: 100%; opacity: 1; } 51%, 100% { top: 100%; opacity: 0; } }
.flags { display: flex; flex-direction: column; gap: 6px; }
.flag { display: flex; align-items: center; gap: 8px; padding: 0.5em 0.75em; border-radius: 0.6em; background: rgba(255, 255, 255, 0.82); font-size: 0.9em; }
.flag span:first-child { color: var(--mute); font: 500 0.82em var(--mono); }
.sev { margin-left: auto; padding: 0.15em 0.55em; border-radius: 999px; font: 600 0.72em var(--mono); text-transform: uppercase; letter-spacing: 0.04em; }
.sev--hi { background: rgba(255, 59, 59, 0.14); color: #c22a2a; } .sev--md { background: rgba(255, 176, 0, 0.2); color: #8a5a00; } .sev--ok { background: rgba(47, 210, 122, 0.18); color: #127a45; }

/* Orbit Logistics: overnight dispatch */
.scene--orbit { background: #f3f4f6; color: var(--ink); }
.scene--orbit .map { position: absolute; inset: 0; z-index: 0; width: 100%; height: 100%; }
.feed { align-self: flex-end; display: flex; flex-direction: column; gap: 5px; width: min(68%, 330px); padding: 0.8em 0.9em; border-radius: 0.9em; background: rgba(255, 255, 255, 0.82); -webkit-backdrop-filter: blur(10px); backdrop-filter: blur(10px); border: 1px solid #fff; box-shadow: var(--lift); }
.feed div { display: grid; grid-template-columns: auto 1fr; gap: 10px; }
.feed time { color: var(--mute); font: 500 0.8em/1.75 var(--mono); }
.feed strong { font-weight: 600; }

@container (max-width: 380px) {
  .compare, .chips { display: none; }
  .bub { max-width: 88%; }
  .feed { width: 100%; }
}
@media (max-width: 900px) {
  .project:nth-child(n) .cover { aspect-ratio: 1 / 1; }
}
@media (prefers-reduced-motion: reduce) {
  .scene, .scene * { animation: none !important; }
  .scanbar { display: none; }
}

</style>

<canvas id="scene" aria-hidden="true"></canvas>
<canvas id="lens-layer" aria-hidden="true"></canvas>
<div class="hero-fallback" aria-hidden="true"><span>Intelligence</span><span>for every</span><span>workflow</span></div>

<h1 id="headline" class="sr-only">
  <span>Intelligence</span>
  <span>for every</span>
  <span>workflow</span>
</h1>

<nav class="nav" aria-label="Primary" data-section="nav">
  <a class="nav__logo" href="#top">Refract&reg;</a>
  <div class="nav__right">
    <ul class="nav__links">
      <li><a href="#platform">Platform</a></li>
      <li><a href="#customers">Customers</a></li>
      <li><a href="#metrics">Metrics</a></li>
      <li><a href="#pricing">Pricing</a></li>
    </ul>
    <a class="nav__cta" href="#contact">Get API key</a>
  </div>
</nav>

<div class="meta" aria-hidden="true">
  <span>v4.2 &mdash; Agents are GA</span>
  <span class="meta__scroll">Scroll to explore</span>
</div>

<main id="top">
  <div class="hero-spacer" data-section="hero">
    <div class="hero-cta">
      <a class="btn btn--ink" href="#contact">Start building free</a>
      <a class="btn btn--glass" href="#platform">See the platform <span aria-hidden="true">→</span></a>
    </div>
  </div>

  <!-- PRODUCT -->
  <section class="section showcase" aria-label="Product preview" data-section="product">
    <div class="app reveal">
      <div class="app-bar" aria-hidden="true">
        <div class="app-dots"><i></i><i></i><i></i></div>
        <div class="app-url">app.refract.example/agents/support</div>
        <div class="app-bar-pad"></div>
      </div>
      <div class="app-body">
        <aside class="app-side">
          <div class="app-group">
            <h5>Agents</h5>
            <div class="app-item is-active"><span class="dot"></span>Support agent<span class="count">2.4k</span></div>
            <div class="app-item"><span class="dot"></span>Contract reviewer<span class="count">318</span></div>
            <div class="app-item"><span class="dot idle"></span>Ops copilot<span class="count">96</span></div>
          </div>
          <div class="app-group">
            <h5>Workspace</h5>
            <div class="app-item">Knowledge<span class="count">41</span></div>
            <div class="app-item">Evals</div>
            <div class="app-item">Guardrails</div>
            <div class="app-item">Run logs</div>
          </div>
        </aside>
        <div class="app-main">
          <div class="app-head"><h4>Support agent</h4><span class="pill">Live · refract-pro</span></div>
          <div class="msg msg--user">Why was order #4821 refunded, and was it within policy?</div>
          <div class="msg msg--agent">
            <div class="steps"><span class="step">search · <b>support-docs</b></span><span class="step">stripe · <b>get_charge</b></span><span class="step">zendesk · <b>ticket #9132</b></span></div>
            Order #4821 was refunded in full ($184.00) on Sep 28 after the customer reported a damaged item<span class="cite">1</span>. Damaged-on-arrival claims within 30 days qualify for a full refund, so this was within policy<span class="cite">2</span>.
            <div class="sources">
              <div class="source"><span>[1] Zendesk #9132</span>Customer photo of cracked housing, Sep 27</div>
              <div class="source"><span>[2] Refund policy v7</span>Section 3.2, damaged on arrival</div>
            </div>
          </div>
          <div class="composer" aria-hidden="true">Ask the support agent anything…<i>↑</i></div>
        </div>
        <aside class="app-trace">
          <h5>Run trace</h5>
          <div class="trace-grid">
            <div class="metric"><span>Latency</span><b>1.4s</b></div>
            <div class="metric"><span>Tokens</span><b>2,184</b></div>
            <div class="metric"><span>Cost</span><b>$0.004</b></div>
            <div class="metric"><span>Eval score</span><b>0.96</b></div>
          </div>
          <div class="spark">
            <div class="spark-head">p50 latency · 24h <b>1.2s</b></div>
            <svg viewBox="0 0 220 56" preserveAspectRatio="none" aria-hidden="true">
              <defs><linearGradient id="sparkStroke" x1="0" x2="1"><stop offset="0" stop-color="#1e90ff" /><stop offset="1" stop-color="#a24bff" /></linearGradient>
              <linearGradient id="sparkFill" x1="0" x2="0" y1="0" y2="1"><stop offset="0" stop-color="#1e90ff" stop-opacity="0.18" /><stop offset="1" stop-color="#1e90ff" stop-opacity="0" /></linearGradient></defs>
              <path d="M0 34 L20 30 L40 36 L60 26 L80 30 L100 22 L120 28 L140 18 L160 24 L180 16 L200 20 L220 12 L220 56 L0 56 Z" fill="url(#sparkFill)" />
              <polyline points="0,34 20,30 40,36 60,26 80,30 100,22 120,28 140,18 160,24 180,16 200,20 220,12" fill="none" stroke="url(#sparkStroke)" stroke-width="2" stroke-linejoin="round" vector-effect="non-scaling-stroke" />
            </svg>
          </div>
          <h5>Guardrails</h5>
          <ul class="checks"><li>PII redacted</li><li>Answer grounded in sources</li><li>No prompt injection found</li><li>Refund policy check passed</li></ul>
        </aside>
      </div>
    </div>
  </section>

  <!-- 01 STUDIO -->
  <section class="section" id="about" aria-label="Why Refract" data-section="about">
    <div class="label"><span>(01)</span><span>Why Refract</span></div>
    <p class="statement" data-words>
      Refract is the AI platform for teams that ship. Connect your data, deploy <em>agents, copilots and search</em> in days, and keep every answer grounded, cited and auditable.
    </p>
    <div class="intro-foot reveal">
      <div class="intro-side">
        <p>Bring your own model or use ours. Run in our cloud or inside your VPC. SOC 2 Type II, ISO 27001, and your data is never used for training.</p>
        <a class="link-arrow" href="#platform">Explore the platform <span aria-hidden="true">→</span></a>
      </div>
<pre class="snippet" aria-label="Example API call"><span class="bar" aria-hidden="true"><i></i><i></i><i></i></span><span class="k">import</span> refract

agent = refract.Agent(
    model=<span class="s">"refract-pro"</span>,
    knowledge=[<span class="s">"s3://acme/support-docs"</span>],
    tools=[<span class="s">"zendesk"</span>, <span class="s">"stripe"</span>],
    guardrails=<span class="s">"pii-strict"</span>,
)

reply = agent.run(<span class="s">"Why was order #4821 refunded?"</span>)
<span class="k">print</span>(reply.text, reply.citations)  <span class="c"># grounded + cited</span></pre>
    </div>
    <div class="lens-wrap">
      <div class="lens" data-lens="Grounded" data-lens-bg="#e8e9ec" data-lens-ink="#0d0f14" aria-hidden="true" style="--fit: 19cqi"><span>Grounded</span></div>
      <div class="lens-caption"><span>Every answer traced to a source</span><span>Citations on by default</span></div>
    </div>
  </section>

  <!-- 02 CAPABILITIES -->
  <section class="section" id="platform" aria-label="Platform" data-section="features">
    <div class="label"><span>(02)</span><span>Platform</span></div>
    <ol class="svc">
      <li class="svc-row reveal"><span class="svc-num">01</span><h3>Retrieval</h3><p>Hybrid vector and keyword search over 40+ sources, re-ranked and kept in sync with permissions.</p><span class="svc-arrow" aria-hidden="true">↗</span></li>
      <li class="svc-row reveal"><span class="svc-num">02</span><h3>Agents</h3><p>Multi-step agents that call your tools and APIs, with human approval wherever money or data moves.</p><span class="svc-arrow" aria-hidden="true">↗</span></li>
      <li class="svc-row reveal"><span class="svc-num">03</span><h3>Evals</h3><p>Regression suites, LLM-as-judge scoring and side-by-side model comparisons on every deploy.</p><span class="svc-arrow" aria-hidden="true">↗</span></li>
      <li class="svc-row reveal"><span class="svc-num">04</span><h3>Guardrails</h3><p>PII redaction, prompt-injection filters and policy checks that run before anything reaches a user.</p><span class="svc-arrow" aria-hidden="true">↗</span></li>
    </ol>
  </section>

  <!-- 03 WORK -->
  <section class="section" id="customers" data-section="customers">
    <div class="label"><span>(03)</span><span>Customers</span></div>
    <div class="work-head">
      <h2 class="display reveal">In<br /><span class="serif">production</span></h2>
      <span class="work-count reveal">04 Case studies · 2024—2026</span>
    </div>
    <div class="work-grid">
      <a class="project reveal" href="#contact">
        <div class="cover" aria-hidden="true"><div class="cover-art scene scene--nova">
            <div class="scene-tag"><span class="live"></span>Support agent · live</div>
            <div class="chat">
              <div class="bub bub--in s1">I was charged twice for my card renewal. $84.20 both times.</div>
              <div class="bub bub--out s2"><div class="chips"><span>stripe · find_charges</span><span>stripe · refund</span></div>Found the duplicate from Sep 30 and reversed it. The $84.20 is back in your account in 1–2 business days.</div>
              <div class="resolved s3">✓ Resolved in 38s · no handoff</div>
            </div>
            <div class="compare s4"><span>Before</span><i></i><b>11m</b><span>Refract</span><i class="now"></i><b>4m</b></div>
            <div class="scene-big">−62%</div>
          </div></div>
        <div class="project-meta"><h3>Nova Bank</h3><span class="year">−62%</span><span>Support agent · Resolution time</span></div>
      </a>
      <a class="project reveal" href="#contact">
        <div class="cover" aria-hidden="true"><div class="cover-art scene scene--halo">
            <div class="scene-tag"><span class="live"></span>Clinical search · ED</div>
            <div class="search"><span class="q">sepsis protocol, first hour</span><span class="kbd">↵</span></div>
            <ul class="results">
              <li class="r s2"><b>Hour-1 bundle, adult ED</b><span>ED Protocols v12 · §2.1</span><em>.97</em></li>
              <li class="r s3"><b>Lactate re-measure criteria</b><span>Lab Guide 2026 · p.18</span><em>.88</em></li>
              <li class="r s4"><b>Night-shift escalation contacts</b><span>On-call rota · wk 40</span><em>.74</em></li>
            </ul>
            <div class="timer s4"><b>0.8s</b><span>to answer</span><s>7.2s before</s></div>
            <div class="scene-big">9×</div>
          </div></div>
        <div class="project-meta"><h3>Halo Health</h3><span class="year">9×</span><span>Clinical search · Faster lookups</span></div>
      </a>
      <a class="project reveal" href="#contact">
        <div class="cover" aria-hidden="true"><div class="cover-art scene scene--lumen">
            <div class="scene-tag"><span class="live"></span>Contract review · MSA</div>
            <div class="doc">
              <div class="doc-title">Master Services Agreement<small>Acme × Lumen client · 42 pp</small></div>
              <i class="ln" style="width: 96%"></i><i class="ln" style="width: 88%"></i><i class="ln hl hl--r s2" style="width: 92%"></i><i class="ln hl hl--r s2" style="width: 54%"></i>
              <i class="ln" style="width: 90%"></i><i class="ln" style="width: 72%"></i><i class="ln hl hl--a s3" style="width: 84%"></i>
              <i class="ln" style="width: 94%"></i><i class="ln" style="width: 66%"></i><i class="ln hl hl--g s4" style="width: 58%"></i><i class="ln" style="width: 80%"></i>
              <span class="scanbar"></span>
            </div>
            <div class="flags">
              <div class="flag s2"><span>§8.2</span>Auto-renews, 90-day notice<span class="sev sev--hi">High</span></div>
              <div class="flag s3"><span>§11</span>Liability cap missing<span class="sev sev--md">Med</span></div>
              <div class="flag s4"><span>§14</span>Governing law: New York<span class="sev sev--ok">OK</span></div>
            </div>
            <div class="scene-big">4h</div>
          </div></div>
        <div class="project-meta"><h3>Lumen Legal</h3><span class="year">4 hrs</span><span>Contract review · Saved per deal</span></div>
      </a>
      <a class="project reveal" href="#contact">
        <div class="cover" aria-hidden="true"><div class="cover-art scene scene--orbit">
            <svg class="map" viewBox="0 0 400 300" preserveAspectRatio="xMidYMid slice">
              <defs>
                <pattern id="orb-dots" width="12" height="12" patternUnits="userSpaceOnUse"><circle cx="2" cy="2" r="1" fill="rgba(13,15,20,0.13)" /></pattern>
                <linearGradient id="orb-prism" x1="0" x2="1"><stop offset="0" stop-color="#ff3b3b" /><stop offset=".3" stop-color="#ffb000" /><stop offset=".55" stop-color="#2fd27a" /><stop offset=".8" stop-color="#1e90ff" /><stop offset="1" stop-color="#a24bff" /></linearGradient>
              </defs>
              <rect width="400" height="300" fill="url(#orb-dots)" />
              <path d="M70 200 C 140 250, 260 250, 330 165" fill="none" stroke="rgba(13,15,20,0.22)" stroke-width="1.5" />
              <path d="M140 155 S 200 120, 255 120" fill="none" stroke="rgba(13,15,20,0.25)" stroke-width="1.5" stroke-dasharray="3 4" />
              <g stroke="#d12b2b" stroke-width="2" stroke-linecap="round"><path d="M192 126 l10 10 M202 126 l-10 10" /></g>
              <path id="orb-live" d="M70 200 C 100 180, 110 160, 140 155 C 165 195, 225 195, 255 120 S 305 140, 330 165" fill="none" stroke="url(#orb-prism)" stroke-width="2.5" stroke-linecap="round" />
              <g fill="#fff" stroke="#0d0f14" stroke-width="1.5">
                <circle cx="70" cy="200" r="4.5" /><circle cx="140" cy="155" r="4.5" /><circle cx="255" cy="120" r="4.5" /><circle cx="330" cy="165" r="4.5" />
              </g>
              <g font-family="JetBrains Mono, monospace" font-size="9" font-weight="500" fill="#0d0f14">
                <text x="58" y="190">SFO</text><text x="116" y="146">RNO</text><text x="263" y="137">SLC</text><text x="304" y="186">DEN</text>
                <text x="180" y="117" fill="#d12b2b">I-80 CLOSED</text>
              </g>
              <circle r="5" fill="#0d0f14" stroke="#fff" stroke-width="2"><animateMotion dur="8s" repeatCount="indefinite" begin="-3s"><mpath href="#orb-live" /></animateMotion></circle>
              <circle r="4" fill="#0d0f14" stroke="#fff" stroke-width="2"><animateMotion dur="11s" repeatCount="indefinite" begin="-7s" path="M70 200 C 140 250, 260 250, 330 165" /></circle>
            </svg>
            <div class="scene-tag"><span class="live"></span>Ops copilot · 03:15 UTC</div>
            <div class="feed">
              <div class="s1"><time>03:12</time><span><strong>Rerouted T-14</strong> around the I-80 closure, ETA −22m</span></div>
              <div class="s2"><time>03:14</time><span>Driver swap booked at the Reno hub</span></div>
              <div class="s3"><time>03:15</time><span>6 customers notified of new delivery windows</span></div>
            </div>
          </div></div>
        <div class="project-meta"><h3>Orbit Logistics</h3><span class="year">24/7</span><span>Ops copilot · Dispatch automation</span></div>
      </a>
    </div>
  </section>

  <!-- 04 NUMBERS -->
  <section class="section numbers" id="metrics" aria-labelledby="numbers-title" data-section="metrics">
    <div class="label"><span>(04)</span><span id="numbers-title">In numbers</span></div>
    <div class="lens-wrap">
      <div class="lens lens--dark" data-lens="Measured" data-lens-bg="#0d0f14" data-lens-ink="#e8e9ec" aria-hidden="true" style="--fit: 18cqi"><span>Measured</span></div>
      <div class="lens-caption"><span>Every run traced, scored and costed</span><span>Live across 1,200+ teams</span></div>
    </div>
    <div class="stats">
      <div class="stat reveal"><span class="stat-num" data-count="1200" data-suffix="+">1,200+</span><span class="stat-label">Teams in production</span></div>
      <div class="stat reveal"><span class="stat-num" data-count="40" data-suffix="ms">40ms</span><span class="stat-label">Median retrieval latency</span></div>
      <div class="stat reveal"><span class="stat-num" data-count="62" data-suffix="%">62%</span><span class="stat-label">Avg. faster ticket resolution</span></div>
      <div class="stat reveal"><span class="stat-num" data-count="0">0</span><span class="stat-label">Bytes of your data used for training</span></div>
    </div>
    <blockquote class="quote reveal">
      "We replaced three vendors and a forty-page runbook with one Refract agent. Our on-call team finally sleeps."
      <span class="quote-by">Giulia Ferri · VP Engineering, Nova Bank</span>
    </blockquote>
    <div class="clients" aria-label="Clients">
      <div class="clients-track">
        <span>Nova</span><span>halo health</span><span>Lumen</span><span>Orbit</span><span>Fabbrica</span><span>vento</span><span>Arcadia</span><span>Monolite</span>
      </div>
      <div class="clients-track" aria-hidden="true">
        <span>Nova</span><span>halo health</span><span>Lumen</span><span>Orbit</span><span>Fabbrica</span><span>vento</span><span>Arcadia</span><span>Monolite</span>
      </div>
    </div>
  </section>

  <!-- 05 PRICING -->
  <section class="section" id="pricing" data-section="pricing">
    <div class="label"><span>(05)</span><span>Pricing</span></div>
    <div class="pricing-head">
      <h2 class="display reveal">Simple<br /><span class="serif">pricing</span></h2>
      <div class="billing" role="group" aria-label="Billing period" data-component="billing-toggle">
        <button type="button" data-billing="monthly" aria-pressed="false">Monthly</button>
        <button type="button" data-billing="annual" aria-pressed="true">Annual<small>−20%</small></button>
      </div>
    </div>
    <div class="plans">
      <article class="plan reveal">
        <div class="plan-top"><h3>Starter</h3></div>
        <div class="price"><b>$0</b><span>free forever</span></div>
        <p>For prototypes and side projects. Ship your first agent this afternoon.</p>
        <ul><li>1 agent, 1,000 runs a month</li><li>3 data sources</li><li>Hosted retrieval and evals</li><li>Community support</li></ul>
        <a class="btn btn--line" href="#contact">Start free</a>
      </article>
      <article class="plan plan--featured reveal">
        <div class="plan-top"><h3>Team</h3><span class="plan-tag">Most popular</span></div>
        <div class="price"><b data-price-monthly="$49" data-price-annual="$39">$39</b><span data-per-monthly="per seat / month, billed monthly" data-per-annual="per seat / month, billed annually">per seat / month, billed annually</span></div>
        <p>For product teams running agents in production with real users.</p>
        <ul><li>Unlimited agents, 50,000 runs a month</li><li>All 40+ connectors</li><li>Eval suites and guardrails</li><li>SSO and role-based access</li><li>Priority email support</li></ul>
        <a class="btn btn--ink" href="#contact">Start 14-day trial</a>
      </article>
      <article class="plan reveal">
        <div class="plan-top"><h3>Enterprise</h3></div>
        <div class="price"><b>Custom</b><span>annual contract</span></div>
        <p>For regulated teams that need their own cloud, their own models and a signed SLA.</p>
        <ul><li>Deploy in your VPC or on-prem</li><li>Bring your own model</li><li>99.99% uptime SLA</li><li>Audit logs and SOC 2 reports</li><li>Dedicated solutions engineer</li></ul>
        <a class="btn btn--line" href="#contact">Talk to sales</a>
      </article>
    </div>
    <p class="pricing-note">Prices in USD. Extra runs are $0.002 each. Cancel any time.</p>
  </section>

  <!-- 06 CONTACT -->
  <section class="section" id="contact" data-section="contact">
    <div class="label"><span>(06)</span><span>Get started</span></div>
    <div class="contact-grid">
      <div>
        <h2 class="display reveal">Start<br /><span class="serif">building</span></h2>
        <a class="mail reveal" href="mailto:sales@refract.example">sales@refract.example</a>
      </div>
      <form class="brief reveal" novalidate>
        <label class="field"><span>Name</span><input name="name" autocomplete="name" /><em class="err"></em></label>
        <label class="field"><span>Work email</span><input name="email" type="email" autocomplete="email" /><em class="err"></em></label>
        <fieldset class="budget field--full">
          <legend>Plan</legend>
          <label><input type="radio" name="budget" value="starter" /><span>Starter · Free</span></label>
          <label><input type="radio" name="budget" value="team" checked /><span>Team · $49/seat</span></label>
          <label><input type="radio" name="budget" value="enterprise" /><span>Enterprise</span></label>
        </fieldset>
        <label class="field field--full"><span>What do you want to automate?</span><textarea name="message"></textarea><em class="err"></em></label>
        <div class="brief-foot">
          <p class="brief-status" role="status" aria-live="polite"></p>
          <button class="send" type="submit">Book<br />a demo</button>
        </div>
      </form>
    </div>
  </section>
</main>

<footer class="footer" data-section="footer">
  <div class="foot">
    <div class="lens" data-lens="Ship it" data-lens-bg="#f6f7f9" data-lens-ink="#0d0f14" aria-hidden="true" style="--fit: 21cqi"><span>Ship it</span></div>
    <div class="foot-cta">
      <h2>Your first agent is an <span class="serif">afternoon</span> away.</h2>
      <div class="foot-cta-actions">
        <a class="btn btn--ink" href="#contact">Start building free</a>
        <a class="btn btn--line" href="#pricing">Compare plans</a>
      </div>
    </div>
    <div class="foot-main">
      <div class="foot-brand">
        <a class="foot-logo" href="#top">Refract&reg;</a>
        <p>The AI platform for teams that ship grounded agents, copilots and search on their own data.</p>
        <form class="foot-news" novalidate>
          <label class="sr-only" for="news-email">Email for the changelog</label>
          <input id="news-email" name="email" type="email" placeholder="you@company.com" autocomplete="email" />
          <button type="submit">Subscribe</button>
        </form>
        <p class="foot-news-msg" role="status" aria-live="polite">Monthly changelog. No spam.</p>
      </div>
      <nav class="foot-col" aria-label="Product"><h4>Product</h4><a href="#platform">Platform</a><a href="#pricing">Pricing</a><a href="#">Docs</a><a href="#">Changelog</a><a href="#">API status</a></nav>
      <nav class="foot-col" aria-label="Company"><h4>Company</h4><a href="#customers">Customers</a><a href="#">About</a><a href="#">Careers</a><a href="#">Security</a></nav>
      <nav class="foot-col" aria-label="Contact"><h4>Contact</h4><a href="mailto:sales@refract.example">sales@refract.example</a><a href="#">LinkedIn</a><a href="#">GitHub</a><a href="#top">Back to top ↑</a></nav>
    </div>
    <div class="foot-bottom">
      <span>© 2026 Refract Labs, Inc.</span>
      <div class="foot-legal"><a href="#">Privacy</a><a href="#">Terms</a><a href="#">DPA</a><a href="#">Cookies</a></div>
      <div class="foot-status"><span class="status">All systems operational</span><span class="clock" data-clock>--:--:--</span></div>
    </div>
  </div>
</footer>

<script type="importmap">
  {
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.170.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.170.0/examples/jsm/"
  }
}
</script>

<!-- ================= Page interactions (no WebGL needed) ================= -->
<script>
(() => {
  const reducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  // 01 — split the statement into words; light them as the paragraph crosses the viewport
  const statement = document.querySelector("[data-words]");
  const walk = (node) => {
    for (const child of [...node.childNodes]) {
      if (child.nodeType === Node.TEXT_NODE) {
        const frag = document.createDocumentFragment();
        for (const part of child.textContent.split(/(\s+)/)) {
          if (!part) continue;
          if (/^\s+$/.test(part)) frag.append(part);
          else frag.append(Object.assign(document.createElement("span"), { className: "w", textContent: part }));
        }
        child.replaceWith(frag);
      } else if (child.nodeType === Node.ELEMENT_NODE) {
        walk(child);
      }
    }
  };
  walk(statement);
  const words = [...statement.querySelectorAll(".w")];

  const meta = document.querySelector(".meta");
  let ticking = false;
  const onScroll = () => {
    ticking = false;
    const vh = innerHeight;
    // meta bar belongs to the hero only
    meta.style.opacity = String(Math.max(0, 0.6 * (1 - scrollY / (vh * 0.35))));
    if (reducedMotion) return;
    const r = statement.getBoundingClientRect();
    // 0 when the paragraph's top reaches 85% of the viewport, 1 when its bottom reaches 45%
    const start = vh * 0.85;
    const end = vh * 0.45;
    const p = Math.min(1, Math.max(0, (start - r.top) / (start - end + r.height)));
    const lit = Math.round(p * words.length);
    words.forEach((w, i) => w.classList.toggle("is-lit", i < lit));
  };
  addEventListener("scroll", () => { if (!ticking) { ticking = true; requestAnimationFrame(onScroll); } }, { passive: true });
  addEventListener("resize", onScroll);
  onScroll();

  // Reveals
  const revealer = new IntersectionObserver((entries) => {
    for (const e of entries) {
      if (!e.isIntersecting) continue;
      e.target.classList.add("is-in");
      revealer.unobserve(e.target);
    }
  }, { rootMargin: "0px 0px -8% 0px" });
  document.querySelectorAll(".reveal").forEach((el) => revealer.observe(el));

  // Counters
  const counter = new IntersectionObserver((entries) => {
    for (const e of entries) {
      if (!e.isIntersecting) continue;
      counter.unobserve(e.target);
      const el = e.target;
      const target = Number(el.dataset.count);
      if (reducedMotion) continue;
      const t0 = performance.now();
      const tick = (now) => {
        const k = Math.min(1, (now - t0) / 1400);
        el.textContent = Math.round(target * (1 - Math.pow(1 - k, 3))).toLocaleString("en-US") + (el.dataset.suffix || "");
        if (k < 1) requestAnimationFrame(tick);
      };
      requestAnimationFrame(tick);
    }
  }, { threshold: 0.6 });
  document.querySelectorAll("[data-count]").forEach((el) => counter.observe(el));

  // Status clock (UTC)
  const clock = document.querySelector("[data-clock]");
  const fmt = new Intl.DateTimeFormat("en-GB", { timeZone: "UTC", hour: "2-digit", minute: "2-digit", second: "2-digit", timeZoneName: "short" });
  const tickClock = () => (clock.textContent = fmt.format(new Date()));
  tickClock();
  setInterval(tickClock, 1000);

  // Pricing: monthly / annual toggle
  const billingBtns = document.querySelectorAll("[data-billing]");
  billingBtns.forEach((btn) => btn.addEventListener("click", () => {
    const mode = btn.dataset.billing;
    billingBtns.forEach((b) => b.setAttribute("aria-pressed", String(b === btn)));
    document.querySelectorAll("[data-price-monthly]").forEach((el) => (el.textContent = el.dataset[mode === "annual" ? "priceAnnual" : "priceMonthly"]));
    document.querySelectorAll("[data-per-monthly]").forEach((el) => (el.textContent = el.dataset[mode === "annual" ? "perAnnual" : "perMonthly"]));
  }));

  // Case study scenes: animate only while on screen
  const coverIO = new IntersectionObserver((entries) => {
    for (const e of entries) {
      e.target.classList.toggle("is-live", e.isIntersecting && !reducedMotion);
      const svg = e.target.querySelector("svg.map");
      if (svg) (e.isIntersecting && !reducedMotion ? svg.unpauseAnimations() : svg.pauseAnimations());
    }
  }, { rootMargin: "60px 0px" });
  document.querySelectorAll(".cover").forEach((c) => coverIO.observe(c));

  // Footer changelog signup (demo: nothing is sent)
  const news = document.querySelector(".foot-news");
  const newsMsg = document.querySelector(".foot-news-msg");
  news.addEventListener("submit", (e) => {
    e.preventDefault();
    const ok = /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(news.elements.email.value.trim());
    newsMsg.textContent = ok ? "Subscribed. See you in the next changelog." : "Enter a valid email to subscribe.";
    if (ok) news.reset();
  });

  // Brief form (demo: nothing is sent)
  const form = document.querySelector(".brief");
  const status = form.querySelector(".brief-status");
  const setErr = (el, msg) => {
    const field = el.closest(".field");
    field.classList.toggle("is-invalid", Boolean(msg));
    field.querySelector(".err").textContent = msg;
    el.setAttribute("aria-invalid", String(Boolean(msg)));
  };
  form.addEventListener("input", (e) => { if (e.target.closest(".field.is-invalid")) setErr(e.target, ""); });
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    const { name, email, message } = form.elements;
    setErr(name, name.value.trim() ? "" : "Who are we talking to?");
    setErr(email, /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(email.value.trim()) ? "" : "We need a valid email to reply.");
    setErr(message, message.value.trim().length >= 10 ? "" : "A sentence or two about the project, please.");
    const firstInvalid = form.querySelector('[aria-invalid="true"]');
    if (firstInvalid) { firstInvalid.focus(); status.textContent = ""; return; }
    const btn = form.querySelector(".send");
    btn.disabled = true;
    btn.innerHTML = "Sending…";
    setTimeout(() => {
      btn.innerHTML = "Booked ✓";
      status.textContent = `Thanks, ${name.value.trim().split(/\s+/)[0]}. A solutions engineer will reply within one business day.`;
      form.reset();
    }, 900);
  });
})();
</script>

<!-- ================= Hero scene ================= -->
<script type="module">
import * as THREE from "three";
import { RoomEnvironment } from "three/addons/environments/RoomEnvironment.js";

const LINES = [...document.querySelectorAll("#headline span")].map((span) =>
  span.textContent.trim().toUpperCase()
);
const BG = "#e8e9ec";
const INK = "#0d0f14";
const CAMERA_Z = 5;
const reducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

const canvas = document.getElementById("scene");
let renderer;
try {
  renderer = new THREE.WebGLRenderer({ canvas, antialias: true });
} catch {
  // No WebGL: show the headline as real type instead of a blank hero
  document.documentElement.classList.add("no-webgl");
  throw new Error("WebGL unavailable");
}
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));

const scene = new THREE.Scene();
scene.background = new THREE.Color(BG);

const camera = new THREE.PerspectiveCamera(45, 1, 0.1, 100);
camera.position.z = CAMERA_Z;

const pmrem = new THREE.PMREMGenerator(renderer);
scene.environment = pmrem.fromScene(new RoomEnvironment(), 0.04).texture;

const textCanvas = document.createElement("canvas");
const textCtx = textCanvas.getContext("2d");
let textTexture = null;

const textPlane = new THREE.Mesh(
  new THREE.PlaneGeometry(1, 1),
  new THREE.MeshBasicMaterial({ toneMapped: false, transparent: true })
);
scene.add(textPlane);

const torus = new THREE.Mesh(
  new THREE.TorusKnotGeometry(1, 0.3, 300, 48, 2, 3),
  new THREE.MeshPhysicalMaterial({
    color: 0xffffff,
    metalness: 0,
    roughness: 0,
    transmission: 1,
    thickness: 0.7,
    ior: 1.45,
    dispersion: 4,
    envMapIntensity: 1,
    toneMapped: false
  })
);
torus.position.z = 2.2;
scene.add(torus);

let torusBase = 1;
let visibleHeight = 1;

function drawText(width, height) {
  const dpr = Math.min(window.devicePixelRatio, 2);
  textCanvas.width = Math.round(width * dpr);
  textCanvas.height = Math.round(height * dpr);
  textCtx.setTransform(dpr, 0, 0, dpr, 0, 0);
  textCtx.fillStyle = BG;
  textCtx.fillRect(0, 0, width, height);
  textCtx.fillStyle = INK;
  textCtx.textAlign = "center";
  textCtx.textBaseline = "middle";

  const maxWidth = width * 0.92;
  const maxHeight = height * 0.6;
  const baseSize = 100;
  const lineGap = 0.98;

  textCtx.font = `900 ${baseSize}px "Inter Tight", sans-serif`;
  const sizes = LINES.map(
    (line) => baseSize * (maxWidth / textCtx.measureText(line).width)
  );
  const totalHeight = sizes.reduce((sum, size) => sum + size * lineGap, 0);
  const fit = Math.min(1, maxHeight / totalHeight);

  let y = height * 0.45 - (totalHeight * fit) / 2;
  LINES.forEach((line, i) => {
    const size = sizes[i] * fit;
    textCtx.font = `900 ${size}px "Inter Tight", sans-serif`;
    y += (size * lineGap) / 2;
    textCtx.fillText(line, width / 2, y);
    y += (size * lineGap) / 2;
  });

  if (textTexture) {
    textTexture.dispose();
  }
  textTexture = new THREE.CanvasTexture(textCanvas);
  textTexture.colorSpace = THREE.SRGBColorSpace;
  textTexture.anisotropy = renderer.capabilities.getMaxAnisotropy();
  textPlane.material.map = textTexture;
  textPlane.material.needsUpdate = true;
}

function resize() {
  const width = window.innerWidth;
  const height = window.innerHeight;

  renderer.setSize(width, height);
  camera.aspect = width / height;
  camera.updateProjectionMatrix();

  visibleHeight = 2 * CAMERA_Z * Math.tan(THREE.MathUtils.degToRad(camera.fov / 2));
  const visibleWidth = visibleHeight * camera.aspect;
  textPlane.scale.set(visibleWidth, visibleHeight, 1);

  torusBase = Math.min(visibleWidth, visibleHeight) * 0.09;
  torus.scale.setScalar(torusBase);
  // keep the knot centred on the type, which now sits slightly above centre
  torus.position.y = visibleHeight * 0.05 * ((CAMERA_Z - 2.2) / CAMERA_Z);

  drawText(width, height);
}

const pointer = new THREE.Vector2();
window.addEventListener("pointermove", (e) => {
  pointer.x = (e.clientX / window.innerWidth) * 2 - 1;
  pointer.y = (e.clientY / window.innerHeight) * 2 - 1;
});

// Scroll progress through the hero (0 → 1 over the first viewport)
let heroProgress = 0;
const readScroll = () => (heroProgress = Math.min(1, Math.max(0, window.scrollY / window.innerHeight)));
window.addEventListener("scroll", readScroll, { passive: true });
readScroll();

const clock = new THREE.Clock();

function render() {
  const t = clock.getElapsedTime();
  const p = heroProgress;

  if (!reducedMotion) {
    torus.rotation.x = t * 0.35 + pointer.y * 0.15 + p * 1.6;
    torus.rotation.y = t * 0.5 + pointer.x * 0.2 + p * 2.2;
    // the knot swells toward the camera while the type drifts up and fades
    torus.scale.setScalar(torusBase * (1 + p * 0.9));
    textPlane.position.y = p * visibleHeight * 0.18;
  } else {
    torus.rotation.set(0.6, 0.4, 0);
  }
  textPlane.material.opacity = 1 - p * 0.85;

  renderer.render(scene, camera);
}

function debounce(fn, delay) {
  let timeoutId;
  return () => {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(fn, delay);
  };
}

const debouncedResize = debounce(resize, 150);

window.addEventListener("resize", () => {
  renderer.setSize(window.innerWidth, window.innerHeight);
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  debouncedResize();
});

// Transmission + dispersion is expensive: only render while the hero can be seen
let running = false;
const setRunning = (on) => {
  if (on === running) return;
  running = on;
  renderer.setAnimationLoop(on && !reducedMotion ? render : null);
  if (on && reducedMotion) render();
};
window.addEventListener("scroll", () => { if (reducedMotion && running) render(); }, { passive: true });

// fonts.ready alone resolves at once when nothing has requested the font yet
Promise.race([
  document.fonts.load('900 100px "Inter Tight"'),
  new Promise((r) => setTimeout(r, 2500))
]).then(() => {
  resize();
  // start observing only once the scene is sized and the type is drawn
  new IntersectionObserver(([entry]) => setRunning(entry.isIntersecting)).observe(document.querySelector(".hero-spacer"));
});
</script>

<!-- ================= Lens bands: the same glass knot, further down the page ================= -->
<script type="module">
import * as THREE from "three";
import { RoomEnvironment } from "three/addons/environments/RoomEnvironment.js";

const lensEls = [...document.querySelectorAll("[data-lens]")];
const reducedMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

function start() {
  const canvas = document.getElementById("lens-layer");
  let renderer;
  try {
    renderer = new THREE.WebGLRenderer({ canvas, antialias: true, alpha: true });
  } catch {
    return; // the bands keep their plain type
  }
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  renderer.setClearColor(0x000000, 0);

  const scene = new THREE.Scene();
  const pmrem = new THREE.PMREMGenerator(renderer);
  scene.environment = pmrem.fromScene(new RoomEnvironment(), 0.04).texture;

  // World units are CSS pixels at z = 0, so DOM rects map straight into the scene
  const camera = new THREE.PerspectiveCamera(45, 1, 1, 10000);
  let camZ = 1;

  const knotGeo = new THREE.TorusKnotGeometry(1, 0.3, 300, 48, 2, 3);
  const knotMat = new THREE.MeshPhysicalMaterial({
    color: 0xffffff, metalness: 0, roughness: 0, transmission: 1, thickness: 0.7,
    ior: 1.45, dispersion: 4, envMapIntensity: 1, toneMapped: false
  });
  const planeGeo = new THREE.PlaneGeometry(1, 1);

  const lenses = lensEls.map((el, i) => {
    const cvs = document.createElement("canvas");
    const tex = new THREE.CanvasTexture(cvs);
    tex.colorSpace = THREE.SRGBColorSpace;
    const plane = new THREE.Mesh(planeGeo, new THREE.MeshBasicMaterial({ map: tex, toneMapped: false }));
    const knot = new THREE.Mesh(knotGeo, knotMat);
    const group = new THREE.Group();
    group.add(plane, knot);
    group.visible = false;
    scene.add(group);
    return { el, cvs, tex, plane, knot, group, w: 0, h: 0, offset: i * 1.7,
      word: el.dataset.lens.toUpperCase(), bg: el.dataset.lensBg, ink: el.dataset.lensInk, inView: false };
  });

  function draw(l, w, h) {
    l.w = w; l.h = h;
    const dpr = Math.min(window.devicePixelRatio, 2);
    l.cvs.width = Math.max(1, Math.round(w * dpr));
    l.cvs.height = Math.max(1, Math.round(h * dpr));
    const ctx = l.cvs.getContext("2d");
    ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
    ctx.fillStyle = l.bg;
    ctx.fillRect(0, 0, w, h);
    ctx.fillStyle = l.ink;
    ctx.textAlign = "center";
    ctx.textBaseline = "middle";
    ctx.font = '900 100px "Inter Tight", sans-serif';
    const size = Math.min((100 * w * 0.94) / ctx.measureText(l.word).width, h * 0.78);
    ctx.font = `900 ${size}px "Inter Tight", sans-serif`;
    if ("letterSpacing" in ctx) ctx.letterSpacing = `${-0.045 * size}px`;
    ctx.fillText(l.word, w / 2, h * 0.53);
    l.tex.needsUpdate = true;
  }

  function resize() {
    renderer.setSize(window.innerWidth, window.innerHeight);
    camera.aspect = window.innerWidth / window.innerHeight;
    camZ = window.innerHeight / 2 / Math.tan(THREE.MathUtils.degToRad(camera.fov / 2));
    camera.position.z = camZ;
    camera.far = camZ * 4;
    camera.updateProjectionMatrix();
  }

  const pointer = { x: 0, y: 0 };
  window.addEventListener("pointermove", (e) => {
    pointer.x = (e.clientX / window.innerWidth) * 2 - 1;
    pointer.y = (e.clientY / window.innerHeight) * 2 - 1;
  }, { passive: true });

  const clock = new THREE.Clock();

  function render() {
    const t = reducedMotion ? 0 : clock.getElapsedTime();
    const vw = window.innerWidth;
    const vh = window.innerHeight;
    for (const l of lenses) {
      const r = l.el.getBoundingClientRect();
      const visible = r.bottom > -40 && r.top < vh + 40 && r.width > 0;
      l.group.visible = visible;
      if (!visible) continue;
      if (Math.abs(r.width - l.w) > 0.5 || Math.abs(r.height - l.h) > 0.5) draw(l, r.width, r.height);

      const cx = r.left + r.width / 2 - vw / 2;
      const cy = vh / 2 - (r.top + r.height / 2);
      l.plane.position.set(cx, cy, 0);
      l.plane.scale.set(r.width, r.height, 1);

      // p: +1 when the band sits a full screen below centre, -1 a full screen above
      const p = Math.max(-1, Math.min(1, (r.top + r.height / 2 - vh / 2) / vh));
      const kz = r.height * 0.35;
      const k = (camZ - kz) / camZ; // keep the knot over the band despite perspective
      const drift = reducedMotion ? 0 : -p * r.width * 0.16; // glides across the word as you scroll
      l.knot.position.set((cx + drift) * k, cy * k, kz);
      l.knot.scale.setScalar(((r.height * 0.34) / 1.8) * k * (1 - Math.abs(p) * 0.12));
      if (reducedMotion) {
        l.knot.rotation.set(0.6, 0.4, 0);
      } else {
        l.knot.rotation.x = t * 0.35 + pointer.y * 0.15 + p * 1.6 + l.offset;
        l.knot.rotation.y = t * 0.5 + pointer.x * 0.2 + p * 2.2 + l.offset;
      }
    }
    renderer.render(scene, camera);
  }

  // Only render while a band is on screen
  let running = false;
  const sync = () => {
    const on = lenses.some((l) => l.inView);
    if (on === running) return;
    running = on;
    if (!reducedMotion) renderer.setAnimationLoop(on ? render : null);
    if (!on) renderer.clear();
    else if (reducedMotion) render();
  };
  const io = new IntersectionObserver((entries) => {
    for (const e of entries) {
      const l = lenses.find((x) => x.el === e.target);
      if (l) l.inView = e.isIntersecting;
    }
    sync();
  }, { rootMargin: "80px 0px" });

  if (reducedMotion) {
    window.addEventListener("scroll", () => { if (running) render(); }, { passive: true });
  }
  window.addEventListener("resize", () => { resize(); if (running && reducedMotion) render(); });

  resize();
  lenses.forEach((l) => io.observe(l.el));
  document.documentElement.classList.add("knot-ready");
}

if (lensEls.length) {
  Promise.race([
    document.fonts.load('900 100px "Inter Tight"'),
    new Promise((r) => setTimeout(r, 2500))
  ]).then(start);
}
</script>

</body></html>
```

