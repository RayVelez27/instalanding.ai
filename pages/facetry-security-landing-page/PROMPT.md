INSTALANDING.AI · Facetry Security Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Facetry Security Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/facetry-security-landing-page

facetry-security.html:
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Facetry — Security, cut to shape</title>
<style>
  :root {
    --bg: #09090b;
    --bg-deep: #000;
    --ink: #f4f4f5;
    --ink-2: #d4d4d8;
    --soft: #a1a1aa;
    --muted: #71717a;
    --faint: #3f3f46;
    --line: rgba(255,255,255,0.06);
    --line-2: rgba(255,255,255,0.1);
    --ease: cubic-bezier(0.16, 1, 0.3, 1);
    --metal: linear-gradient(180deg, #fbfbfb 0%, #e4e4e4 18%, #cccbcb 55%, #9e9d9d 100%);
    --surface: radial-gradient(130% 130% at 50% 0%, rgba(255,255,255,0.05) 0%, rgba(255,255,255,0.01) 60%, rgba(0,0,0,0.4) 100%);
    --surface-shadow:
      inset 0 1px 0 0 rgba(255,255,255,0.12),
      inset 0 0 0 1px rgba(255,255,255,0.04),
      0 30px 60px -12px rgba(0,0,0,0.95);
    --font: -apple-system, BlinkMacSystemFont, "Inter", "Segoe UI", Roboto, sans-serif;
    --rock: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='320' height='320'%3E%3Cfilter id='r'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.03' numOctaves='5' seed='7'/%3E%3CfeDiffuseLighting lighting-color='%238f8f8f' surfaceScale='5'%3E%3CfeDistantLight azimuth='235' elevation='42'/%3E%3C/feDiffuseLighting%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23r)'/%3E%3C/svg%3E");
    --mono: ui-monospace, "SF Mono", "JetBrains Mono", Menlo, monospace;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; -webkit-font-smoothing: antialiased; }
  html { scroll-behavior: smooth; }
  body {
    background: var(--bg-deep);
    color: var(--ink);
    font-family: var(--font);
    line-height: 1.55;
    overflow-x: hidden;
  }
  /* Diagonal stripe pattern (from the Uiverse snippet), darkened + dimmed */
  body::before {
    content: ""; position: fixed; z-index: -1; pointer-events: none;
    width: 200%; height: 200%; left: -30%; top: -20%;
    background: repeating-linear-gradient(
      135deg,
      #0e0f10 0px,
      #0e0f10 60px,
      rgba(14, 15, 16, 0.6) 70px,
      #18191b 130px
    );
    opacity: 0.7;
    animation: patternDrift 18s linear infinite alternate;
    will-change: transform;
  }
  /* Vignette on top keeps the original centre glow and pulls the edges to black */
  body::after {
    content: ""; position: fixed; inset: 0; z-index: -1; pointer-events: none;
    background: radial-gradient(circle at 50% 30%, rgba(24, 24, 27, 0.35) 0%, rgba(9, 9, 11, 0.72) 38%, rgba(0, 0, 0, 0.96) 100%);
  }
  @keyframes patternDrift {
    from { transform: translateY(0) scale(1); }
    to   { transform: translateY(-20%) scale(1.02) rotate(1deg); }
  }
  a { color: inherit; text-decoration: none; }
  button { font: inherit; color: inherit; background: none; border: none; cursor: pointer; }
  ::selection { background: rgba(255,255,255,0.18); }

  .wrap { width: 100%; max-width: 1160px; margin: 0 auto; padding: 0 24px; }
  section { position: relative; padding: 120px 0; }

  /* ---------- Shared surfaces ---------- */
  .surface {
    background: var(--surface);
    box-shadow: var(--surface-shadow);
    border-radius: 32px;
  }
  .pill {
    display: inline-flex; align-items: center; gap: 6px;
    padding: 6px; border-radius: 999px;
    background: rgba(18,18,21,0.85);
    backdrop-filter: blur(16px); -webkit-backdrop-filter: blur(16px);
    box-shadow:
      inset 0 1px 0 0 rgba(255,255,255,0.08),
      0 0 0 1px rgba(255,255,255,0.05),
      0 16px 32px -8px rgba(0,0,0,0.7);
  }

  .eyebrow {
    display: inline-flex; align-items: center; gap: 10px;
    font-size: 12px; font-weight: 500; letter-spacing: 0.08em; text-transform: uppercase;
    color: var(--muted);
  }
  .eyebrow::before {
    content: ""; width: 18px; height: 1.5px;
    background: linear-gradient(90deg, rgba(255,255,255,0.2), rgba(255,255,255,0.85));
  }
  .h2 {
    font-size: clamp(34px, 5vw, 56px); line-height: 1.04; letter-spacing: -0.035em; font-weight: 600;
    margin: 18px 0 18px;
  }
  .metal-text {
    background: var(--metal); -webkit-background-clip: text; background-clip: text; color: transparent;
  }
  .lede { color: var(--soft); font-size: 17px; max-width: 560px; }

  /* ---------- Buttons ---------- */
  .btn {
    position: relative; display: inline-flex; align-items: center; gap: 10px;
    height: 46px; padding: 0 22px; border-radius: 999px;
    font-size: 14px; font-weight: 500; letter-spacing: 0.01em;
    transition: transform 0.35s var(--ease), box-shadow 0.35s ease, background 0.25s ease, color 0.25s ease;
  }
  .btn:active { transform: scale(0.97); }
  .btn-metal {
    background: var(--metal); color: #0b0b0c;
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.9), inset 0 -1px 0 rgba(0,0,0,0.15), 0 12px 28px -8px rgba(255,255,255,0.18), 0 2px 6px rgba(0,0,0,0.6);
  }
  .btn-metal:hover { transform: translateY(-2px) scale(1.015); box-shadow: inset 0 1px 0 rgba(255,255,255,0.9), inset 0 -1px 0 rgba(0,0,0,0.15), 0 18px 36px -10px rgba(255,255,255,0.28), 0 2px 6px rgba(0,0,0,0.6); }
  .btn-ghost {
    color: var(--ink-2); background: rgba(255,255,255,0.04);
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.08), inset 0 0 0 1px rgba(255,255,255,0.06);
  }
  .btn-ghost:hover { color: #fff; background: rgba(255,255,255,0.08); transform: translateY(-2px); }
  .btn .arrow { transition: transform 0.35s var(--ease); }
  .btn:hover .arrow { transform: translateX(3px); }

  /* ---------- Nav ---------- */
  .nav {
    position: fixed; top: 16px; left: 50%; transform: translateX(-50%); z-index: 50;
    width: calc(100% - 32px); max-width: 920px;
    display: flex; justify-content: space-between; padding: 8px 8px 8px 24px;
  }
  .brand { display: flex; align-items: center; gap: 12px; font-weight: 600; letter-spacing: -0.015em; font-size: 17px; }
  .brand svg { width: 26px; height: 26px; overflow: visible; }
  .nav-links { display: flex; gap: 6px; }
  .nav-links a {
    font-size: 13.5px; color: var(--muted); padding: 9px 18px; border-radius: 999px;
    transition: color 0.25s ease, background 0.25s ease;
  }
  .nav-links a:hover { color: var(--ink-2); background: rgba(255,255,255,0.04); }
  .nav .btn { height: 42px; padding: 0 20px; font-size: 14px; }
  @media (max-width: 760px) { .nav-links { display: none; } .nav .btn .arrow { display: none; } }

  /* ---------- Hero ---------- */
  .hero { min-height: 100vh; display: flex; align-items: center; padding: 130px 0 80px; overflow: hidden; }
  .hero .wrap { max-width: 1400px; padding: 0 clamp(24px, 8vw, 120px); }
  .hero-grid { display: grid; grid-template-columns: minmax(600px, 1fr) minmax(0, 1.05fr); gap: 16px; align-items: center; }
  @media (max-width: 1180px) {
    .hero-grid { grid-template-columns: 1fr; gap: 24px; text-align: center; }
    .hero-copy { display: flex; flex-direction: column; align-items: center; }
  }
  .badge {
    display: inline-flex; align-items: center; gap: 10px; padding: 6px 14px 6px 6px; border-radius: 999px;
    font-size: 13px; color: var(--ink-2);
    background: rgba(255,255,255,0.03); box-shadow: inset 0 1px 0 rgba(255,255,255,0.08), inset 0 0 0 1px rgba(255,255,255,0.08);
    transition: background 0.25s ease, box-shadow 0.25s ease;
  }
  .badge:hover { background: rgba(255,255,255,0.06); }
  .badge b { font-weight: 600; color: #0b0b0c; background: var(--metal); padding: 3px 9px; border-radius: 999px; font-size: 11px; letter-spacing: 0.02em; }
  .badge .chev { color: var(--muted); margin-left: 2px; transition: transform 0.4s var(--ease); }
  .badge:hover .chev { transform: translateX(3px); }
  .hero h1 {
    font-size: clamp(48px, 5.4vw, 92px); line-height: 1.02; letter-spacing: -0.045em; font-weight: 600;
    margin: 30px 0 26px;
  }
  .hero h1 .metal-text { display: inline-block; padding-bottom: 0.08em; }
  .hero .lede { font-size: clamp(16px, 1.3vw, 19px); max-width: 560px; line-height: 1.6; }
  .cta-row { display: flex; gap: 14px; flex-wrap: wrap; }
  .hero .cta-row { margin-top: 40px; }
  @media (max-width: 1180px) { .hero .cta-row { justify-content: center; } }
  .btn-lg { height: 58px; padding: 0 32px; font-size: 16px; }
  .btn-lg.btn-ghost { background: rgba(255,255,255,0.025); box-shadow: inset 0 1px 0 rgba(255,255,255,0.08), inset 0 0 0 1px rgba(255,255,255,0.09); color: #fff; }
  .btn .play { width: 14px; height: 14px; fill: none; stroke: currentColor; stroke-width: 1.8; stroke-linejoin: round; }

  /* feature chips — double as the morph controls */
  .chips { display: flex; margin-top: 56px; }
  @media (max-width: 1180px) { .chips { justify-content: center; flex-wrap: wrap; row-gap: 18px; } }
  .chip {
    position: relative; display: flex; align-items: center; gap: 16px; text-align: left;
    padding: 4px 26px 14px 0; color: var(--soft);
  }
  .chip + .chip { padding-left: 26px; }
  .chip + .chip::before { content: ""; position: absolute; left: 0; top: 8px; bottom: 18px; width: 1px; background: var(--line-2); }
  .chip-ico {
    width: 46px; height: 46px; border-radius: 12px; display: grid; place-items: center; flex: none;
    background: rgba(255,255,255,0.02);
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.12), inset 0 1px 0 rgba(255,255,255,0.08);
    transition: background 0.35s ease, box-shadow 0.35s ease, color 0.35s ease, transform 0.5s var(--ease);
  }
  .chip-ico svg { width: 20px; height: 20px; fill: none; stroke: currentColor; stroke-width: 1.6; stroke-linecap: round; stroke-linejoin: round; }
  .chip b { display: block; font-size: 15.5px; font-weight: 500; color: var(--ink-2); letter-spacing: -0.01em; transition: color 0.3s; }
  .chip small { white-space: nowrap; display: block; font-size: 13px; color: var(--muted); margin-top: 2px; }
  .chip:hover .chip-ico { transform: translateY(-2px); }
  @media (max-width: 640px) {
    .chips { flex-direction: column; align-items: stretch; gap: 6px; margin-top: 44px; width: 100%; max-width: 320px; }
    .chip, .chip + .chip { padding: 6px 0 12px; }
    .chip + .chip::before { display: none; }
    .chip .bar, .chip + .chip .bar { left: 62px; right: 0; }
  }
  .chip.active { color: #fff; }
  .chip.active b { color: #fff; }
  .chip.active .chip-ico {
    background: rgba(255,255,255,0.07);
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.22), inset 0 1px 0 rgba(255,255,255,0.2), 0 10px 24px -10px rgba(255,255,255,0.18);
  }
  .chip .bar { left: 0; right: 26px; }
  .chip + .chip .bar { left: 26px; }
  .chip.active .bar { opacity: 1; }

  /* ---------- Hero 3D scene ---------- */
  .hero-scene { --s: 1; position: relative; height: calc(640px * var(--s)); display: flex; justify-content: center; align-items: center; }
  @media (max-width: 1320px) { .hero-scene { --s: 0.86; } }
  @media (max-width: 1180px) { .hero-scene { --s: 0.8; margin-top: 24px; } }
  @media (max-width: 640px)  { .hero-scene { --s: 0.56; } }
  .hero-grid > * { min-width: 0; }
  .scene3d {
    position: absolute; left: 50%; top: 50%; width: 640px; height: 640px; margin: -320px 0 0 -320px;
    transform: scale(var(--s));
    perspective: 2200px; perspective-origin: 50% 38%;
  }
  .world {
    position: absolute; inset: 0; transform-style: preserve-3d;
    transform: rotateX(var(--rx, -19deg)) rotateY(var(--ry, -34deg));
  }
  .world > * { position: absolute; left: 50%; top: 50%; transform-style: preserve-3d; }

  /* floor grid */
  .floor {
    width: 1100px; height: 1100px;
    transform: translate(-50%, -50%) translate3d(0, 150px, 0) rotateX(90deg);
    background-image:
      linear-gradient(rgba(255,255,255,0.1) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,0.1) 1px, transparent 1px);
    background-size: 64px 64px; background-position: center;
    -webkit-mask-image: radial-gradient(circle at 50% 50%, #000 0%, rgba(0,0,0,0.5) 28%, transparent 56%);
            mask-image: radial-gradient(circle at 50% 50%, #000 0%, rgba(0,0,0,0.5) 28%, transparent 56%);
  }
  .floor-glow {
    width: 700px; height: 700px;
    transform: translate(-50%, -50%) translate3d(0, 151px, 0) rotateX(90deg);
    background: radial-gradient(circle, rgba(255,255,255,0.07), transparent 55%);
  }

  /* pedestal (stone block) */
  .ped { width: 320px; height: 112px; transform: translate(-50%, -50%) translate3d(0, 94px, 0); }
  .ped .f {
    position: absolute; left: 50%; top: 50%; background-color: #141414;
    background-image: var(--rock); background-size: 320px 320px;
  }
  .ped .f::after { content: ""; position: absolute; inset: 0; background: var(--shade); }
  .ped .front {
    width: 320px; height: 112px; transform: translate(-50%, -50%) translateZ(140px);
    --shade: linear-gradient(180deg, rgba(0,0,0,0.5), rgba(0,0,0,0.92));
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.18), inset -1px 0 0 rgba(255,255,255,0.12);
    clip-path: polygon(0 3%, 9% 0, 22% 4%, 37% 1%, 55% 3%, 71% 0, 86% 4%, 100% 2%, 100% 100%, 0 100%);
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.12);
  }
  .ped .side {
    width: 280px; height: 112px; transform: translate(-50%, -50%) rotateY(90deg) translateZ(160px);
    --shade: linear-gradient(180deg, rgba(0,0,0,0.68), rgba(0,0,0,0.96));
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.1);
    clip-path: polygon(0 2%, 14% 5%, 30% 0, 48% 4%, 63% 1%, 80% 5%, 100% 1%, 100% 100%, 0 100%);
  }
  .ped .top {
    width: 320px; height: 280px; transform: translate(-50%, -50%) rotateX(90deg) translateZ(56px);
    --shade: radial-gradient(circle at 45% 45%, rgba(0,0,0,0.22), rgba(0,0,0,0.62) 80%);
  }
  .ped-shadow {
    width: 520px; height: 440px;
    transform: translate(-50%, -50%) translate3d(20px, 150px, 0) rotateX(90deg);
    background: radial-gradient(closest-side, rgba(0,0,0,0.9), transparent);
  }

  /* extruded metal icon */
  .icon3d { width: 270px; height: 270px; transform: translate(-50%, -50%) translate3d(0, -97px, -30px); cursor: pointer; }
  .icon3d .m3d { position: absolute; inset: 0; transform-style: preserve-3d; will-change: transform; }
  .icon3d .m3d svg { position: absolute; inset: 0; width: 100%; height: 100%; overflow: visible; }
  .icon-flare {
    width: 220px; height: 220px; pointer-events: none;
    transform: translate(-50%, -50%) translate3d(112px, -214px, -26px);
    background: radial-gradient(circle, rgba(255,255,255,0.55) 0%, rgba(255,255,255,0.12) 18%, transparent 50%);
    animation: flare 6s ease-in-out infinite alternate;
  }
  @keyframes flare { from { opacity: 0.55; } to { opacity: 1; } }

  /* glass panels */
  .panel {
    border-radius: 8px;
    background: linear-gradient(160deg, rgba(255,255,255,0.06), rgba(255,255,255,0.012) 60%);
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.1), inset 0 1px 0 rgba(255,255,255,0.14), 0 30px 60px -20px rgba(0,0,0,0.9);
  }
  .panel .plus { position: absolute; font-size: 12px; line-height: 1; color: rgba(255,255,255,0.4); font-family: var(--mono); }
  .panel .plus.tl { top: 8px; left: 9px; } .panel .plus.tr { top: 8px; right: 9px; }
  .panel .plus.bl { bottom: 8px; left: 9px; } .panel .plus.br { bottom: 8px; right: 9px; }
  .p-back { width: 300px; height: 440px; transform: translate(-50%, -50%) translate3d(-30px, -70px, -230px); opacity: 0.7; }
  .p-back::before, .p-back::after { content: ""; position: absolute; background: rgba(255,255,255,0.06); }
  .p-back::before { left: 50%; top: 0; bottom: 0; width: 1px; }
  .p-back::after { top: 34%; left: 0; right: 0; height: 1px; }
  .p-tile { width: 128px; height: 150px; transform: translate(-50%, -50%) translate3d(-240px, -150px, -70px); display: grid; place-items: center; }
  .p-tile .tile {
    width: 78px; height: 78px; border-radius: 16px; display: grid; place-items: center;
    background: rgba(0,0,0,0.35); box-shadow: inset 0 0 0 1px rgba(255,255,255,0.12), inset 0 2px 8px rgba(0,0,0,0.6);
  }
  .p-tile .tile svg { width: 46px; height: 46px; overflow: visible; opacity: 0.7; }
  .p-map { width: 230px; height: 260px; transform: translate(-50%, -50%) translate3d(-255px, 75px, 50px); padding: 30px 18px; display: flex; align-items: center; }
  .p-map svg { width: 100%; height: auto; }
  .p-list {
    width: 180px; height: 270px; transform: translate(-50%, -50%) translate3d(285px, -20px, -40px);
    display: flex; flex-direction: column; justify-content: center; gap: 30px; padding: 0 22px;
  }
  .p-list span {
    display: flex; align-items: center; gap: 12px;
    font-family: var(--mono); font-size: 13px; letter-spacing: 0.18em; color: rgba(255,255,255,0.6);
  }
  .p-list span::before { content: ""; width: 14px; height: 1px; background: rgba(255,255,255,0.35); }
  .p-list span::after { content: ""; flex: 1; height: 1px; background: rgba(255,255,255,0.18); }
  .p-list span.on { color: #fff; }

  /* light rays + sparkles */
  .ray { width: 1px; height: 520px; background: linear-gradient(180deg, transparent, rgba(255,255,255,0.14), transparent); }
  .spark {
    width: 3px; height: 3px; border-radius: 50%; background: #fff;
    box-shadow: 0 0 6px 2px rgba(255,255,255,0.55);
    animation: twinkle 3.2s ease-in-out infinite; animation-delay: var(--t, 0s);
  }
  @keyframes twinkle { 0%, 100% { opacity: 0.15; } 50% { opacity: 1; } }
  .stage {
    position: relative; width: min(380px, 80vw); aspect-ratio: 1; border-radius: 22%;
    background: var(--surface); box-shadow: var(--surface-shadow);
    display: flex; align-items: center; justify-content: center; cursor: pointer;
    transition: transform 0.35s var(--ease), box-shadow 0.35s ease;
  }
  .stage::after {
    content: ""; position: absolute; inset: -40%; z-index: -1; pointer-events: none;
    background: radial-gradient(circle, rgba(255,255,255,0.06) 0%, transparent 55%);
  }
  .stage:hover {
    transform: translateY(-2px) scale(1.015);
    box-shadow: inset 0 1px 0 0 rgba(255,255,255,0.2), inset 0 0 0 1px rgba(255,255,255,0.08), 0 36px 70px -12px rgba(0,0,0,1);
  }
  .stage:active { transform: scale(0.97); }
  .stage svg { width: 65%; height: 65%; overflow: visible; will-change: transform, filter; }

  /* dock tabs (from source DNA) */
  .tab {
    position: relative; display: flex; align-items: center; gap: 8px;
    padding: 8px 18px; border-radius: 999px;
    color: var(--muted); font-size: 12px; font-weight: 500; letter-spacing: 0.02em;
    transition: color 0.25s ease, background 0.25s ease; overflow: hidden;
  }
  .tab:hover { color: var(--ink-2); }
  .tab.active { color: #fff; background: rgba(255,255,255,0.08); box-shadow: inset 0 1px 0 0 rgba(255,255,255,0.1); }
  .tab svg { width: 14px; height: 14px; fill: currentColor; opacity: 0.85; }
  .bar {
    position: absolute; bottom: 0; left: 16px; right: 16px; height: 1.5px;
    background: linear-gradient(90deg, rgba(255,255,255,0.2), rgba(255,255,255,0.85), rgba(255,255,255,0.2));
    transform-origin: left center; transform: scaleX(0); opacity: 0; transition: opacity 0.2s ease;
  }
  .tab.active .bar { opacity: 1; }

  /* ---------- Marquee strip ---------- */
  .strip { padding: 0 0 40px; }
  .strip-inner {
    display: flex; overflow: hidden; border-top: 1px solid var(--line); border-bottom: 1px solid var(--line);
    mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
    -webkit-mask-image: linear-gradient(90deg, transparent, #000 12%, #000 88%, transparent);
  }
  .strip-track { display: flex; gap: 56px; padding: 22px 28px; white-space: nowrap; animation: marquee 38s linear infinite; }
  .strip-track span { display: inline-flex; align-items: center; gap: 12px; color: var(--muted); font-size: 13px; letter-spacing: 0.02em; }
  .strip-track svg { width: 14px; height: 14px; fill: var(--faint); }
  @keyframes marquee { to { transform: translateX(-50%); } }

  /* ---------- Features ---------- */
  .section-head { max-width: 680px; margin-bottom: 64px; }
  .bento { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; }
  @media (max-width: 920px) { .bento { grid-template-columns: 1fr; } }
  .card {
    position: relative; padding: 32px; border-radius: 32px; overflow: hidden;
    background: var(--surface); box-shadow: var(--surface-shadow);
    transition: transform 0.5s var(--ease), box-shadow 0.4s ease;
  }
  .card:hover {
    transform: translateY(-4px);
    box-shadow: inset 0 1px 0 0 rgba(255,255,255,0.2), inset 0 0 0 1px rgba(255,255,255,0.08), 0 36px 70px -12px rgba(0,0,0,1);
  }
  .card .icon {
    width: 76px; height: 76px; overflow: visible; margin-bottom: 36px;
    transition: transform 0.6s var(--ease);
  }
  .card:hover .icon { transform: translateY(-3px) rotate(-4deg) scale(1.06); }
  .card h3 { font-size: 21px; letter-spacing: -0.02em; font-weight: 600; margin-bottom: 10px; }
  .card p { color: var(--soft); font-size: 15px; }
  .card ul { list-style: none; margin-top: 24px; border-top: 1px solid var(--line); padding-top: 18px; display: grid; gap: 10px; }
  .card li { display: flex; align-items: center; gap: 10px; font-size: 13px; color: var(--ink-2); }
  .card li::before { content: ""; width: 6px; height: 6px; transform: rotate(45deg); background: var(--metal); border-radius: 1px; flex: none; }
  .card .num { position: absolute; top: 32px; right: 32px; font-family: var(--mono); font-size: 12px; color: var(--faint); }

  .wide { grid-column: 1 / -1; display: grid; grid-template-columns: 1fr 1.2fr; gap: 40px; align-items: center; }
  @media (max-width: 920px) { .wide { grid-template-columns: 1fr; } }
  .code {
    font-family: var(--mono); font-size: 13px; line-height: 1.8; color: var(--soft);
    background: rgba(0,0,0,0.45); border-radius: 20px; padding: 22px 24px; overflow-x: auto;
    box-shadow: inset 0 0 0 1px var(--line), inset 0 1px 0 rgba(255,255,255,0.04);
  }
  .code .k { color: #fafafa; } .code .s { color: #b4b4b8; } .code .c { color: #52525b; } .code .n { color: #e4e4e7; }
  .code-top { display: flex; gap: 6px; margin-bottom: 16px; }
  .code-top i { width: 9px; height: 9px; border-radius: 50%; background: #27272a; }

  /* ---------- Motion lab ---------- */
  .lab { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }
  @media (max-width: 920px) { .lab { grid-template-columns: 1fr; } }
  .lab-stage-wrap { padding: 40px; display: flex; flex-direction: column; align-items: center; justify-content: center; gap: 28px; }
  .lab-stage-wrap .stage { width: min(260px, 70vw); }
  .lab-controls { padding: 36px; display: flex; flex-direction: column; gap: 28px; }
  .ctrl label { display: flex; justify-content: space-between; font-size: 13px; color: var(--soft); margin-bottom: 12px; }
  .ctrl label output { font-family: var(--mono); color: var(--ink); }
  input[type=range] { -webkit-appearance: none; appearance: none; width: 100%; height: 4px; border-radius: 999px; background: rgba(255,255,255,0.08); outline: none; }
  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none; width: 20px; height: 20px; border-radius: 50%; background: var(--metal); cursor: grab;
    box-shadow: inset 0 1px 0 #fff, 0 4px 10px rgba(0,0,0,0.8); transition: transform 0.3s var(--ease);
  }
  input[type=range]::-webkit-slider-thumb:active { transform: scale(1.2); cursor: grabbing; }
  input[type=range]::-moz-range-thumb { width: 20px; height: 20px; border: none; border-radius: 50%; background: #e4e4e4; box-shadow: 0 4px 10px rgba(0,0,0,0.8); }
  .curve { background: rgba(0,0,0,0.45); border-radius: 18px; padding: 16px; box-shadow: inset 0 0 0 1px var(--line); }
  .curve svg { width: 100%; height: 130px; display: block; overflow: visible; }
  .curve-meta { display: flex; justify-content: space-between; font-family: var(--mono); font-size: 11px; color: var(--muted); margin-top: 10px; }
  .presets { display: flex; gap: 8px; flex-wrap: wrap; }
  .presets button {
    font-size: 12px; padding: 7px 14px; border-radius: 999px; color: var(--soft);
    background: rgba(255,255,255,0.04); box-shadow: inset 0 0 0 1px var(--line);
    transition: color 0.2s, background 0.2s;
  }
  .presets button:hover, .presets button.on { color: #fff; background: rgba(255,255,255,0.1); }

  /* phones: the shape dock must fit, or its width stretches the lab grid past the screen;
     and the stage's glow (inset -40%) is clipped to its card so it can't widen the page */
  .lab > * { min-width: 0; }
  @media (max-width: 920px) { .lab-stage-wrap { overflow: clip; } }
  @media (max-width: 520px) {
    .lab-stage-wrap { padding: 28px 16px; }
    #labDock .tab { padding: 8px 10px; }
    .lab-controls { padding: 28px 22px; }
  }

  /* ---------- Stats ---------- */
  .stats { display: grid; grid-template-columns: repeat(4, 1fr); border-top: 1px solid var(--line); border-bottom: 1px solid var(--line); }
  @media (max-width: 760px) { .stats { grid-template-columns: repeat(2, 1fr); } }
  .stat { padding: 44px 28px; border-right: 1px solid var(--line); }
  .stat:last-child { border-right: none; }
  @media (max-width: 760px) { .stat:nth-child(2) { border-right: none; } .stat:nth-child(-n+2) { border-bottom: 1px solid var(--line); } }
  .stat b { display: block; font-size: clamp(34px, 4.4vw, 52px); font-weight: 600; letter-spacing: -0.04em; line-height: 1; }
  .stat span { display: block; margin-top: 12px; font-size: 13px; color: var(--muted); }

  /* ---------- Pricing ---------- */
  .tiers { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; align-items: stretch; }
  @media (max-width: 920px) { .tiers { grid-template-columns: 1fr; } }
  .tier { display: flex; flex-direction: column; padding: 32px; }
  .tier .icon { width: 44px; height: 44px; margin-bottom: 26px; }
  .tier h3 { font-size: 15px; font-weight: 500; color: var(--soft); letter-spacing: 0.02em; }
  .price { display: flex; align-items: baseline; gap: 6px; margin: 12px 0 8px; }
  .price b { font-size: 46px; font-weight: 600; letter-spacing: -0.04em; }
  .price span { color: var(--muted); font-size: 14px; }
  .tier p { color: var(--soft); font-size: 14px; min-height: 44px; }
  .tier ul { list-style: none; margin: 26px 0 32px; display: grid; gap: 12px; flex: 1; }
  .tier li { display: flex; gap: 10px; font-size: 14px; color: var(--ink-2); }
  .tier li svg { width: 16px; height: 16px; flex: none; margin-top: 3px; stroke: #a1a1aa; fill: none; stroke-width: 2; }
  .tier .btn { justify-content: center; }
  .tier.featured { box-shadow: inset 0 1px 0 0 rgba(255,255,255,0.22), inset 0 0 0 1px rgba(255,255,255,0.14), 0 40px 80px -16px rgba(0,0,0,1), 0 0 80px -30px rgba(255,255,255,0.15); }
  .tag { position: absolute; top: 28px; right: 28px; font-size: 11px; font-weight: 600; color: #0b0b0c; background: var(--metal); padding: 4px 10px; border-radius: 999px; }

  /* ---------- FAQ ---------- */
  .faq { max-width: 760px; margin: 0 auto; }
  .q { border-bottom: 1px solid var(--line); }
  .q button { width: 100%; display: flex; justify-content: space-between; align-items: center; gap: 20px; padding: 26px 0; text-align: left; font-size: 17px; font-weight: 500; letter-spacing: -0.01em; color: var(--ink-2); transition: color 0.2s; }
  .q button:hover { color: #fff; }
  .q .plus { position: relative; width: 14px; height: 14px; flex: none; }
  .q .plus::before, .q .plus::after { content: ""; position: absolute; left: 0; top: 6px; width: 14px; height: 1.5px; background: currentColor; transition: transform 0.5s var(--ease); }
  .q .plus::after { transform: rotate(90deg); }
  .q.open .plus::after { transform: rotate(0); }
  .q.open .plus::before { transform: rotate(180deg); }
  .a { display: grid; grid-template-rows: 0fr; transition: grid-template-rows 0.55s var(--ease); }
  .q.open .a { grid-template-rows: 1fr; }
  .a > div { overflow: hidden; }
  .a p { color: var(--soft); font-size: 15px; padding-bottom: 26px; max-width: 640px; }

  /* ---------- Terminus: CTA + footer as one surface ---------- */
  .terminus { padding: 80px 0 24px; }
  .term {
    position: relative; overflow: hidden; isolation: isolate;
    border-radius: 48px;
    background:
      radial-gradient(120% 90% at 50% 0%, rgba(255,255,255,0.055) 0%, rgba(255,255,255,0.012) 45%, rgba(0,0,0,0.55) 100%);
    box-shadow:
      inset 0 1px 0 0 rgba(255,255,255,0.14),
      inset 0 0 0 1px rgba(255,255,255,0.05),
      0 60px 120px -30px rgba(0,0,0,1);
  }
  /* cursor-follow spotlight */
  .term-glow {
    position: absolute; inset: 0; z-index: -1; pointer-events: none; opacity: 0;
    background: radial-gradient(420px circle at var(--mx, 50%) var(--my, 30%), rgba(255,255,255,0.06), transparent 60%);
    transition: opacity 0.6s ease;
  }
  .term:hover .term-glow { opacity: 1; }
  /* oversized ghost facet, outlined in metal, drifting behind everything */
  .term-ghost {
    position: absolute; z-index: -1; pointer-events: none;
    width: 760px; height: 760px; right: -220px; top: -160px; overflow: visible;
    opacity: 0.09; animation: ghostSpin 90s linear infinite;
  }
  .term-ghost path { fill: none; stroke: url(#iconMetal); stroke-width: 0.6; vector-effect: non-scaling-stroke; }
  @keyframes ghostSpin { to { transform: rotate(360deg); } }
  /* fine facet hairline top edge */
  .term::before {
    content: ""; position: absolute; top: 0; left: 10%; right: 10%; height: 1px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.5), transparent);
  }

  .term-top { display: grid; grid-template-columns: 1.25fr 0.75fr; gap: 48px; align-items: center; padding: 88px 72px 72px; }
  @media (max-width: 920px) { .term-top { grid-template-columns: 1fr; padding: 64px 28px 48px; text-align: center; } .term-copy { display: flex; flex-direction: column; align-items: center; } }
  .term-top .h2 { font-size: clamp(40px, 6vw, 72px); letter-spacing: -0.045em; line-height: 0.98; margin: 20px 0 20px; }
  .term-top .lede { margin-bottom: 36px; }

  .join {
    display: flex; align-items: center; gap: 6px; width: 100%; max-width: 480px;
    padding: 6px 6px 6px 22px; border-radius: 999px;
    background: rgba(0,0,0,0.45);
    box-shadow: inset 0 0 0 1px rgba(255,255,255,0.08), inset 0 2px 6px rgba(0,0,0,0.6), 0 1px 0 rgba(255,255,255,0.06);
    transition: box-shadow 0.35s ease;
  }
  .join:focus-within { box-shadow: inset 0 0 0 1px rgba(255,255,255,0.22), inset 0 2px 6px rgba(0,0,0,0.6), 0 0 0 6px rgba(255,255,255,0.04); }
  .join input {
    flex: 1; min-width: 0; background: none; border: none; outline: none;
    color: var(--ink); font: inherit; font-size: 14px;
  }
  .join input::placeholder { color: var(--muted); }
  .join .btn { height: 42px; flex: none; }
  .join .btn .done { display: none; }
  .join.sent .btn .label { display: none; }
  .join.sent .btn .done { display: inline; }
  .assure { display: flex; flex-wrap: wrap; gap: 18px; margin-top: 18px; font-size: 12px; color: var(--muted); }
  @media (max-width: 920px) { .assure { justify-content: center; } }
  .assure span { display: inline-flex; align-items: center; gap: 8px; }
  .assure span::before { content: ""; width: 5px; height: 5px; transform: rotate(45deg); background: var(--metal); border-radius: 1px; }

  .term-visual { display: flex; flex-direction: column; align-items: center; gap: 18px; }
  .term-visual .stage { width: min(260px, 64vw); border-radius: 26%; }
  .term-visual small { font-family: var(--mono); font-size: 11px; color: var(--muted); letter-spacing: 0.04em; }

  /* live region band */
  .regions { margin: 0 32px; border-radius: 24px; background: rgba(0,0,0,0.38); box-shadow: inset 0 0 0 1px var(--line); overflow: hidden; }
  .regions-head {
    display: flex; justify-content: space-between; align-items: center; gap: 12px; flex-wrap: wrap;
    padding: 14px 22px; border-bottom: 1px solid var(--line);
    font-size: 12px; color: var(--soft);
  }
  .regions-head .mono { font-family: var(--mono); font-size: 11px; color: var(--muted); }
  .pulse { position: relative; width: 7px; height: 7px; border-radius: 50%; background: #e4e4e7; display: inline-block; margin-right: 10px; }
  .pulse::after { content: ""; position: absolute; inset: -5px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.5); animation: ping 2.4s var(--ease) infinite; }
  @keyframes ping { 0% { transform: scale(0.4); opacity: 1; } 100% { transform: scale(1.6); opacity: 0; } }
  .region-grid { display: grid; grid-template-columns: repeat(6, 1fr); }
  @media (max-width: 920px) { .region-grid { grid-template-columns: repeat(3, 1fr); } }
  @media (max-width: 520px) { .region-grid { grid-template-columns: repeat(2, 1fr); } }
  .region { padding: 18px 22px; border-right: 1px solid var(--line); font-family: var(--mono); transition: background 0.3s ease; }
  .region:hover { background: rgba(255,255,255,0.025); }
  .region:last-child { border-right: none; }
  .region .rcode { font-size: 11px; color: var(--muted); letter-spacing: 0.08em; }
  .region .time { display: block; font-size: 18px; color: var(--ink); margin: 6px 0 4px; letter-spacing: -0.02em; font-variant-numeric: tabular-nums; }
  .region .lat { font-size: 11px; color: var(--soft); font-variant-numeric: tabular-nums; }
  .lat-bar { display: block; height: 2px; margin-top: 10px; border-radius: 2px; background: rgba(255,255,255,0.06); overflow: hidden; }
  .lat-bar i { display: block; height: 100%; background: linear-gradient(90deg, rgba(255,255,255,0.25), rgba(255,255,255,0.85)); transform-origin: left; transition: transform 0.9s var(--ease); }

  /* links */
  .term-links { display: grid; grid-template-columns: 1.5fr repeat(4, 1fr); gap: 32px; padding: 64px 72px 48px; }
  @media (max-width: 920px) { .term-links { grid-template-columns: 1fr 1fr; padding: 48px 28px 36px; } .term-manifesto { grid-column: 1 / -1; } }
  .term-manifesto p { font-size: 15px; color: var(--soft); max-width: 280px; line-height: 1.6; }
  .term-manifesto .sig { display: flex; gap: 8px; margin-top: 22px; }
  .term-manifesto .sig svg { width: 22px; height: 22px; overflow: visible; }
  .term-links h4 { font-size: 11px; font-weight: 500; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; margin-bottom: 16px; }
  .term-links nav a {
    position: relative; display: table; font-size: 14px; color: var(--soft); padding: 5px 0;
    transition: color 0.25s ease, transform 0.45s var(--ease);
  }
  .term-links nav a::before {
    content: ""; position: absolute; left: -14px; top: 50%; width: 5px; height: 5px; margin-top: -2.5px;
    transform: rotate(45deg) scale(0); background: var(--metal); border-radius: 1px;
    transition: transform 0.45s var(--ease);
  }
  .term-links nav a:hover { color: #fff; transform: translateX(10px); }
  .term-links nav a:hover::before { transform: rotate(45deg) scale(1); }

  .term-legal {
    display: flex; justify-content: space-between; align-items: center; gap: 16px; flex-wrap: wrap;
    margin: 0 32px; padding: 22px 8px 26px; border-top: 1px solid var(--line);
    font-size: 12px; color: var(--muted);
  }
  .term-legal .legal-links { display: flex; gap: 20px; }
  .term-legal a:hover { color: var(--ink-2); }
  .to-top {
    display: inline-flex; align-items: center; gap: 10px; padding: 6px 14px 6px 6px; border-radius: 999px;
    font-size: 12px; color: var(--soft);
    background: rgba(255,255,255,0.04); box-shadow: inset 0 1px 0 rgba(255,255,255,0.08), inset 0 0 0 1px var(--line);
    transition: color 0.25s, background 0.25s, transform 0.45s var(--ease);
  }
  .to-top:hover { color: #fff; background: rgba(255,255,255,0.08); transform: translateY(-2px); }
  .to-top b { display: grid; place-items: center; width: 26px; height: 26px; border-radius: 50%; background: var(--metal); color: #0b0b0c; font-size: 13px; transition: transform 0.5s var(--ease); }
  .to-top:hover b { transform: translateY(-2px); }

  /* ---------- Reveal ---------- */
  .reveal { opacity: 0; transform: translateY(28px); filter: blur(8px); transition: opacity 0.9s var(--ease), transform 1.1s var(--ease), filter 0.9s ease; transition-delay: var(--d, 0s); }
  .reveal.in { opacity: 1; transform: none; filter: none; }

  @media (prefers-reduced-motion: reduce) {
    .reveal { opacity: 1; transform: none; filter: none; transition: none; }
    .strip-track { animation: none; }
    body::before { animation: none; }
    .term-ghost, .pulse::after, .spark, .icon-flare { animation: none; }
    * { scroll-behavior: auto !important; }
  }
</style>
</head>
<body>

<!-- Shared material: metal gradient + finish filters -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
  <defs>
    <linearGradient id="iconMetal" gradientUnits="userSpaceOnUse" x1="120" y1="14" x2="120" y2="226">
      <stop offset="0%" stop-color="#fbfbfb" />
      <stop offset="18%" stop-color="#e4e4e4" />
      <stop offset="55%" stop-color="#cccbcb" />
      <stop offset="100%" stop-color="#9e9d9d" />
    </linearGradient>
    <filter id="iconFinish" x="-30%" y="-30%" width="160%" height="160%">
      <feDropShadow dx="0" dy="14" stdDeviation="11" flood-color="#000" flood-opacity="0.82" result="shadow" />
      <feOffset in="SourceAlpha" dx="0" dy="1.2" result="offsetAlpha" />
      <feComposite in="SourceAlpha" in2="offsetAlpha" operator="out" result="topEdge" />
      <feFlood flood-color="#fff" flood-opacity="0.65" result="edgeColor" />
      <feComposite in="edgeColor" in2="topEdge" operator="in" result="topHighlight" />
      <feMerge><feMergeNode in="shadow" /><feMergeNode in="SourceGraphic" /><feMergeNode in="topHighlight" /></feMerge>
    </filter>
    <filter id="iconFinishSm" x="-30%" y="-30%" width="160%" height="160%">
      <feDropShadow dx="0" dy="8" stdDeviation="7" flood-color="#000" flood-opacity="0.85" result="shadow" />
      <feOffset in="SourceAlpha" dx="0" dy="2.4" result="offsetAlpha" />
      <feComposite in="SourceAlpha" in2="offsetAlpha" operator="out" result="topEdge" />
      <feFlood flood-color="#fff" flood-opacity="0.7" result="edgeColor" />
      <feComposite in="edgeColor" in2="topEdge" operator="in" result="topHighlight" />
      <feMerge><feMergeNode in="shadow" /><feMergeNode in="SourceGraphic" /><feMergeNode in="topHighlight" /></feMerge>
    </filter>
    <!-- 3D hero: brushed front face with a diagonal sheen, darker extrusion sides -->
    <linearGradient id="iconMetalFront" gradientUnits="userSpaceOnUse" x1="30" y1="10" x2="215" y2="230">
      <stop offset="0%" stop-color="#8d8d8f" />
      <stop offset="22%" stop-color="#f4f4f4" />
      <stop offset="44%" stop-color="#a6a6a8" />
      <stop offset="68%" stop-color="#d9d9da" />
      <stop offset="100%" stop-color="#6e6e70" />
    </linearGradient>
    <linearGradient id="iconMetalDark" gradientUnits="userSpaceOnUse" x1="200" y1="20" x2="40" y2="230">
      <stop offset="0%" stop-color="#9c9c9e" />
      <stop offset="45%" stop-color="#4a4a4d" />
      <stop offset="100%" stop-color="#1e1e20" />
    </linearGradient>
    <filter id="iconEdge" x="-10%" y="-10%" width="120%" height="120%">
      <feOffset in="SourceAlpha" dx="0" dy="1.4" result="o1" />
      <feComposite in="SourceAlpha" in2="o1" operator="out" result="topEdge" />
      <feFlood flood-color="#fff" flood-opacity="0.85" />
      <feComposite in2="topEdge" operator="in" result="hi" />
      <feOffset in="SourceAlpha" dx="0" dy="-1.4" result="o2" />
      <feComposite in="SourceAlpha" in2="o2" operator="out" result="botEdge" />
      <feFlood flood-color="#000" flood-opacity="0.55" />
      <feComposite in2="botEdge" operator="in" result="lo" />
      <feMerge><feMergeNode in="SourceGraphic" /><feMergeNode in="hi" /><feMergeNode in="lo" /></feMerge>
    </filter>
  </defs>
</svg>

<!-- ============ NAV ============ -->
<nav class="nav pill" data-section="nav">
  <a href="#top" class="brand"><svg viewBox="0 0 240 240" data-icon="0" data-metal></svg>Facetry</a>
  <div class="nav-links">
    <a href="#platform">Platform</a>
    <a href="#motion">Motion</a>
    <a href="#pricing">Pricing</a>
    <a href="#faq">FAQ</a>
  </div>
  <a href="#start" class="btn btn-metal">Get started <span class="arrow">→</span></a>
</nav>

<!-- ============ HERO ============ -->
<header class="hero" id="top" data-section="hero">
  <div class="wrap hero-grid">
    <div class="hero-copy">
      <a href="#platform" class="badge reveal"><b>2.0</b> Adaptive policies are here <span class="chev">›</span></a>
      <h1 class="reveal" style="--d:.08s">Security,<br><span class="metal-text">cut to shape.</span></h1>
      <p class="lede reveal" style="--d:.16s">Facetry is the access layer that bends to your architecture without breaking. Precise rules, hard boundaries, and a foundation that holds under load.</p>
      <div class="cta-row reveal" style="--d:.24s">
        <a href="#start" class="btn btn-metal btn-lg">Start building <span class="arrow">→</span></a>
        <a href="#motion" class="btn btn-ghost btn-lg"><svg class="play" viewBox="0 0 16 16"><path d="M4 2.5v11l9-5.5z" /></svg>See it move</a>
      </div>
      <div class="chips reveal" style="--d:.32s" id="heroChips">
        <button class="chip">
          <span class="chip-ico"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="6.5" /><circle cx="12" cy="12" r="1.6" /><path d="M12 2.5v4M12 17.5v4M2.5 12h4M17.5 12h4" /></svg></span>
          <span><b>Precision</b><small>Fine-grained control</small></span>
          <div class="bar"></div>
        </button>
        <button class="chip">
          <span class="chip-ico"><svg viewBox="0 0 24 24"><rect x="5" y="10.5" width="14" height="10" rx="2.2" /><path d="M8.2 10.5V7.8a3.8 3.8 0 0 1 7.6 0v2.7" /><path d="M12 14.6v2" /></svg></span>
          <span><b>Protection</b><small>Zero-trust by default</small></span>
          <div class="bar"></div>
        </button>
        <button class="chip">
          <span class="chip-ico"><svg viewBox="0 0 24 24"><path d="M12 3.5 21 19.5H3z" /><path d="M12 10.5 15.2 16H8.8z" /></svg></span>
          <span><b>Foundation</b><small>Built for scale</small></span>
          <div class="bar"></div>
        </button>
      </div>
    </div>

    <div class="hero-scene reveal" style="--d:.15s" id="heroScene">
      <div class="scene3d">
        <div class="world" id="world">
          <div class="floor"></div>
          <div class="floor-glow"></div>
          <div class="ped-shadow"></div>

          <div class="ray" style="transform:translate(-50%,-50%) translate3d(-370px,40px,50px)"></div>
          <div class="ray" style="transform:translate(-50%,-50%) translate3d(375px,-30px,-40px)"></div>
          <div class="ray" style="transform:translate(-50%,-50%) translate3d(-180px,-150px,-230px)"></div>

          <div class="panel p-back"><i class="plus tl">+</i><i class="plus tr">+</i><i class="plus bl">+</i><i class="plus br">+</i></div>
          <div class="panel p-tile"><i class="plus tl">+</i><i class="plus br">+</i><div class="tile"><svg viewBox="0 0 240 240" data-icon="1" data-metal></svg></div></div>
          <div class="panel p-list" id="pList"><i class="plus tl">+</i><i class="plus tr">+</i><i class="plus bl">+</i><i class="plus br">+</i>
            <span>POLICIES</span><span>ACCESS</span><span>CONTROLS</span><span>MONITORING</span>
          </div>

          <div class="ped"><div class="f top"></div><div class="f front"></div><div class="f side"></div></div>
          <div class="icon3d" id="heroStage" role="button" aria-label="Next shape"></div>
          <div class="icon-flare"></div>

          <div class="panel p-map"><i class="plus tl">+</i><i class="plus tr">+</i><i class="plus bl">+</i><i class="plus br">+</i><svg id="worldMap" viewBox="0 0 400 210"></svg></div>

          <div class="spark" style="transform:translate(-50%,-50%) translate3d(-192px,150px,128px);--t:.2s"></div>
          <div class="spark" style="transform:translate(-50%,-50%) translate3d(256px,150px,64px);--t:1.1s"></div>
          <div class="spark" style="transform:translate(-50%,-50%) translate3d(128px,150px,256px);--t:2s"></div>
          <div class="spark" style="transform:translate(-50%,-50%) translate3d(-64px,150px,-256px);--t:.7s"></div>
          <div class="spark" style="transform:translate(-50%,-50%) translate3d(320px,-170px,-40px);--t:1.6s"></div>
          <div class="spark" style="transform:translate(-50%,-50%) translate3d(-300px,-250px,-70px);--t:2.4s"></div>
        </div>
      </div>
    </div>
  </div>
</header>

<!-- ============ STRIP ============ -->
<div class="strip" data-section="marquee">
  <div class="strip-inner">
    <div class="strip-track" id="stripTrack">
      <span><svg viewBox="0 0 240 240" data-icon="0"></svg>Edge-native evaluation</span>
      <span><svg viewBox="0 0 240 240" data-icon="1"></svg>Zero-trust defaults</span>
      <span><svg viewBox="0 0 240 240" data-icon="2"></svg>Open policy language</span>
      <span><svg viewBox="0 0 240 240" data-icon="0"></svg>Audit-ready logs</span>
      <span><svg viewBox="0 0 240 240" data-icon="1"></svg>Bring your own IdP</span>
      <span><svg viewBox="0 0 240 240" data-icon="2"></svg>Multi-region failover</span>
    </div>
  </div>
</div>

<!-- ============ PLATFORM ============ -->
<section id="platform" data-section="platform">
  <div class="wrap">
    <div class="section-head">
      <div class="eyebrow reveal">Platform</div>
      <h2 class="h2 reveal" style="--d:.06s">Three shapes.<br><span class="metal-text">One system.</span></h2>
      <p class="lede reveal" style="--d:.12s">Every part of Facetry is built on the same geometry — so rules, guards and infrastructure fit together without seams.</p>
    </div>

    <div class="bento">
      <article class="card reveal">
        <span class="num">01</span>
        <svg class="icon" viewBox="0 0 240 240" data-icon="0" data-metal></svg>
        <h3>Precision</h3>
        <p>Fine-grained policies that resolve identity, context and resource in a single pass.</p>
        <ul><li>Attribute & relationship rules</li><li>Deterministic evaluation</li><li>Policy diffs on every deploy</li></ul>
      </article>
      <article class="card reveal" style="--d:.08s">
        <span class="num">02</span>
        <svg class="icon" viewBox="0 0 240 240" data-icon="1" data-metal></svg>
        <h3>Protection</h3>
        <p>Every request is denied until proven otherwise. Sessions are short, keys rotate on their own.</p>
        <ul><li>Continuous verification</li><li>Automatic key rotation</li><li>Anomaly-triggered step-up</li></ul>
      </article>
      <article class="card reveal" style="--d:.16s">
        <span class="num">03</span>
        <svg class="icon" viewBox="0 0 240 240" data-icon="2" data-metal></svg>
        <h3>Foundation</h3>
        <p>A distributed core that keeps answering when regions, links or providers go dark.</p>
        <ul><li>Active-active in 24 regions</li><li>Local cache fallback</li><li>Signed, replayable audit trail</li></ul>
      </article>

      <article class="card wide reveal">
        <div>
          <div class="eyebrow">Policy as code</div>
          <h3 style="font-size:28px;margin:14px 0 12px;letter-spacing:-0.03em">Readable rules.<br>Ruthless enforcement.</h3>
          <p>Write access logic the way you'd explain it. Facetry compiles it to an evaluation graph and ships it to the edge in seconds.</p>
        </div>
        <pre class="code"><div class="code-top"><i></i><i></i><i></i></div><span class="c">// facets/billing.fct</span>
<span class="k">facet</span> <span class="n">billing</span> {
  <span class="k">allow</span> <span class="n">read</span>  <span class="k">when</span> user.team <span class="k">in</span> resource.owners
  <span class="k">allow</span> <span class="n">write</span> <span class="k">when</span> user.role == <span class="s">"finance"</span>
                 <span class="k">and</span> device.trusted
  <span class="k">require</span> <span class="n">mfa</span>  <span class="k">when</span> amount &gt; <span class="s">10_000</span>
  <span class="k">deny</span>  <span class="n">*</span>     <span class="k">otherwise</span>
}</pre>
      </article>
    </div>
  </div>
</section>

<!-- ============ MOTION LAB ============ -->
<section id="motion" data-section="motion-lab">
  <div class="wrap">
    <div class="section-head">
      <div class="eyebrow reveal">Motion lab</div>
      <h2 class="h2 reveal" style="--d:.06s">Motion with <span class="metal-text">mass.</span></h2>
      <p class="lede reveal" style="--d:.12s">Every transition in the Facetry console runs on one spring. Tune it here — stiffness pulls, damping settles.</p>
    </div>

    <div class="lab">
      <div class="surface lab-stage-wrap reveal">
        <div class="stage" id="labStage" role="button" aria-label="Next shape"></div>
        <div class="pill" id="labDock">
          <button class="tab active"><svg viewBox="0 0 240 240" data-icon="0"></svg><span>Diamonds</span><div class="bar"></div></button>
          <button class="tab"><svg viewBox="0 0 240 240" data-icon="1"></svg><span>Shield</span><div class="bar"></div></button>
          <button class="tab"><svg viewBox="0 0 240 240" data-icon="2"></svg><span>Triangle</span><div class="bar"></div></button>
        </div>
      </div>

      <div class="surface lab-controls reveal" style="--d:.08s">
        <div class="presets" id="presets">
          <button data-k="175" data-c="22" class="on">Default</button>
          <button data-k="320" data-c="14">Snappy</button>
          <button data-k="90" data-c="9">Bouncy</button>
          <button data-k="60" data-c="18">Heavy</button>
        </div>
        <div class="ctrl">
          <label for="kRange">Stiffness <output id="kOut">175</output></label>
          <input type="range" id="kRange" min="30" max="500" value="175" />
        </div>
        <div class="ctrl">
          <label for="cRange">Damping <output id="cOut">22</output></label>
          <input type="range" id="cRange" min="4" max="50" value="22" />
        </div>
        <div class="curve">
          <svg viewBox="0 0 300 130" preserveAspectRatio="none">
            <line x1="0" x2="300" y1="40" y2="40" stroke="rgba(255,255,255,0.08)" stroke-dasharray="3 4" />
            <line x1="0" x2="300" y1="120" y2="120" stroke="rgba(255,255,255,0.05)" />
            <path id="curvePath" fill="none" stroke="url(#curveGrad)" stroke-width="2" stroke-linecap="round" vector-effect="non-scaling-stroke" />
            <defs><linearGradient id="curveGrad" x1="0" x2="1"><stop offset="0" stop-color="rgba(255,255,255,0.25)" /><stop offset="1" stop-color="#fff" /></linearGradient></defs>
          </svg>
          <div class="curve-meta"><span>0ms</span><span id="settleOut">settles in —</span><span>1400ms</span></div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ============ STATS ============ -->
<section style="padding-top:40px" data-section="stats">
  <div class="wrap">
    <div class="stats">
      <div class="stat reveal"><b><span data-count="3.2" data-dec="1">0</span>ms</b><span>p99 policy evaluation</span></div>
      <div class="stat reveal" style="--d:.06s"><b><span data-count="99.999" data-dec="3">0</span>%</b><span>Measured availability</span></div>
      <div class="stat reveal" style="--d:.12s"><b><span data-count="24">0</span></b><span>Active-active regions</span></div>
      <div class="stat reveal" style="--d:.18s"><b><span data-count="40">0</span>B</b><span>Decisions per month</span></div>
    </div>
  </div>
</section>

<!-- ============ PRICING ============ -->
<section id="pricing" data-section="pricing">
  <div class="wrap">
    <div class="section-head" style="margin-left:auto;margin-right:auto;text-align:center">
      <div class="eyebrow reveal">Pricing</div>
      <h2 class="h2 reveal" style="--d:.06s">Pick your <span class="metal-text">facet.</span></h2>
      <p class="lede reveal" style="--d:.12s;margin:0 auto">Start free, grow without re-architecting. Every plan runs on the same core.</p>
    </div>

    <div class="tiers">
      <div class="surface tier reveal">
        <svg class="icon" viewBox="0 0 240 240" data-icon="2" data-metal></svg>
        <h3>Foundation</h3>
        <div class="price"><b>$0</b><span>/ month</span></div>
        <p>For side projects and teams getting their first rules in place.</p>
        <ul id="tierA"></ul>
        <a href="#start" class="btn btn-ghost">Start free</a>
      </div>
      <div class="surface tier featured reveal" style="--d:.08s;position:relative">
        <span class="tag">Most chosen</span>
        <svg class="icon" viewBox="0 0 240 240" data-icon="1" data-metal></svg>
        <h3>Protection</h3>
        <div class="price"><b>$49</b><span>/ month</span></div>
        <p>For production apps that need guarantees, not good intentions.</p>
        <ul id="tierB"></ul>
        <a href="#start" class="btn btn-metal">Start 14-day trial</a>
      </div>
      <div class="surface tier reveal" style="--d:.16s">
        <svg class="icon" viewBox="0 0 240 240" data-icon="0" data-metal></svg>
        <h3>Precision</h3>
        <div class="price"><b>Custom</b></div>
        <p>For organizations with compliance mandates and complex topologies.</p>
        <ul id="tierC"></ul>
        <a href="#start" class="btn btn-ghost">Talk to us</a>
      </div>
    </div>
  </div>
</section>

<!-- ============ FAQ ============ -->
<section id="faq" style="padding-top:40px" data-section="faq">
  <div class="wrap">
    <div class="section-head" style="margin-left:auto;margin-right:auto;text-align:center;margin-bottom:40px">
      <div class="eyebrow reveal">FAQ</div>
      <h2 class="h2 reveal" style="--d:.06s">Questions, <span class="metal-text">answered.</span></h2>
    </div>
    <div class="faq" id="faqList"></div>
  </div>
</section>

<!-- ============ TERMINUS: CTA + FOOTER ============ -->
<footer class="terminus" id="start" data-section="footer">
  <div class="wrap">
    <div class="term reveal" id="term">
      <div class="term-glow"></div>
      <svg class="term-ghost" viewBox="0 0 240 240" aria-hidden="true"><path id="ghostPath" /></svg>

      <!-- CTA -->
      <div class="term-top">
        <div class="term-copy">
          <div class="eyebrow">Get started</div>
          <h2 class="h2">Find your<br><span class="metal-text">shape.</span></h2>
          <p class="lede">Ship your first policy in under ten minutes. Bring your stack — we'll fit around it.</p>
          <form class="join" id="joinForm">
            <input type="email" placeholder="you@company.com" aria-label="Work email" required />
            <button class="btn btn-metal" type="submit"><span class="label">Request access <span class="arrow">→</span></span><span class="done">You're in ✓</span></button>
          </form>
          <div class="assure"><span>No credit card</span><span>Free to 10k users</span><span>Cancel anytime</span></div>
        </div>
        <div class="term-visual">
          <div class="stage" id="ctaStage" role="button" aria-label="Next shape"></div>
          <small>TAP TO RESHAPE</small>
        </div>
      </div>

      <!-- Live region band -->
      <div class="regions">
        <div class="regions-head">
          <span><i class="pulse"></i>All systems operational</span>
          <span class="mono" id="regionStamp">24 / 24 regions · live</span>
        </div>
        <div class="region-grid" id="regionGrid"></div>
      </div>

      <!-- Links -->
      <div class="term-links">
        <div class="term-manifesto">
          <p>Precise rules, hard boundaries, and a foundation that holds — every request, every region.</p>
          <div class="sig">
            <svg viewBox="0 0 240 240" data-icon="0" data-metal></svg>
            <svg viewBox="0 0 240 240" data-icon="1" data-metal></svg>
            <svg viewBox="0 0 240 240" data-icon="2" data-metal></svg>
          </div>
        </div>
        <div><h4>Product</h4><nav><a href="#platform">Platform</a><a href="#motion">Motion</a><a href="#pricing">Pricing</a><a href="#">Changelog</a></nav></div>
        <div><h4>Developers</h4><nav><a href="#">Docs</a><a href="#">API reference</a><a href="#">SDKs</a><a href="#">Status</a></nav></div>
        <div><h4>Company</h4><nav><a href="#">About</a><a href="#">Careers</a><a href="#">Security</a><a href="#">Contact</a></nav></div>
        <div><h4>Connect</h4><nav><a href="#">GitHub</a><a href="#">Discord</a><a href="#">X</a><a href="#">Newsletter</a></nav></div>
      </div>

      <div class="term-legal">
        <span>© 2026 · A fictional product made for the INSTALANDING.AI library</span>
        <div class="legal-links"><a href="#">Privacy</a><a href="#">Terms</a><a href="#">Cookies</a></div>
        <a href="#top" class="to-top"><b>↑</b>Back to top</a>
      </div>
    </div>
  </div>
</footer>

<script>
/* =========================================================
   GEOMETRY (from source DNA)
   ========================================================= */
const ICON_PATHS = [
  "M79.8 66.5 L133.5 120 L80.1 174 L26.5 120 Z M79.8 94.1 L105.6 120 L80 145.8 L54.1 120 Z M159.9 66.5 L213.5 120 L159.9 174 L106.4 120 Z M159.9 94.1 L185.4 120 L159.9 145.8 L134.1 120 Z M119.6 27.1 L136.3 43.5 L119.9 59.5 L103.2 43.7 Z M119.5 180.3 L136.9 196.4 L119.5 212.6 L102.9 196.4 Z",
  "M33.5 13.6 H206.5 V190.6 C206.5 211.5 191.4 226.6 170.5 226.6 H69.5 C48.6 226.6 33.5 211.5 33.5 190.6 Z M53.3 33.4 H186.7 V190.4 C186.7 200.5 180.6 206.6 170.5 206.6 H69.5 C59.4 206.6 53.3 200.5 53.3 190.4 Z M81.5 156.7 C71.3 145.2 66.8 133 66.8 119.5 C66.8 90.4 90.6 66.8 120 66.8 C149.4 66.8 173.2 90.4 173.2 119.5 C173.2 133 168.7 145.2 158.5 156.7 L147.3 138.6 C150.8 133.2 152.2 126.5 152.2 119.5 C152.2 101.8 137.8 87.8 120 87.8 C102.2 87.8 87.8 101.8 87.8 119.5 C87.8 126.5 89.2 133.2 92.7 138.6 Z M120 132.9 L153.3 185.9 H86.5 Z",
  "M120.2 28.1 L226.7 213.5 H13.2 Z M120.1 67 L146.8 113.3 H93.9 Z M92.5 133.4 H147.9 L120.2 179.6 Z M75.5 145.3 L105 193.3 H48.5 Z M164.9 145.3 L192.4 193.3 H135.4 Z"
];

function lineSeg(x1, y1, x2, y2) {
  return [x1 + (x2 - x1) / 3, y1 + (y2 - y1) / 3, x1 + ((x2 - x1) * 2) / 3, y1 + ((y2 - y1) * 2) / 3, x2, y2];
}
function polyToCubics(pts) {
  const out = [pts[0][0], pts[0][1]];
  for (let i = 0; i < pts.length; i++) {
    const a = pts[i], b = pts[(i + 1) % pts.length];
    out.push(...lineSeg(a[0], a[1], b[0], b[1]));
  }
  return out;
}

const DIAMOND_OUTER = polyToCubics([[79.8,66.5],[106.6,93.3],[133.5,120.0],[106.8,147.0],[80.1,174.0],[53.3,147.0],[26.5,120.0],[53.1,93.3]]);
const DIAMOND_INNER = polyToCubics([[79.8,94.1],[92.7,107.0],[105.6,120.0],[92.8,132.9],[80.0,145.8],[67.0,132.9],[54.1,120.0],[66.9,107.0]]);
const SHIELD_OUTER = [120.0,13.6, ...lineSeg(120.0,13.6,206.5,13.6), ...lineSeg(206.5,13.6,206.5,190.6), 206.5,211.5,191.4,226.6,170.5,226.6, ...lineSeg(170.5,226.6,120.0,226.6), ...lineSeg(120.0,226.6,69.5,226.6), 48.6,226.6,33.5,211.5,33.5,190.6, ...lineSeg(33.5,190.6,33.5,13.6), ...lineSeg(33.5,13.6,120.0,13.6)];
const SHIELD_INNER = [120.0,33.4, ...lineSeg(120.0,33.4,186.7,33.4), ...lineSeg(186.7,33.4,186.7,190.4), 186.7,200.5,180.6,206.6,170.5,206.6, ...lineSeg(170.5,206.6,120.0,206.6), ...lineSeg(120.0,206.6,69.5,206.6), 59.4,206.6,53.3,200.5,53.3,190.4, ...lineSeg(53.3,190.4,53.3,33.4), ...lineSeg(53.3,33.4,120.0,33.4)];
const TRIANGLE_OUTER = polyToCubics([[120.2,28.1],[155.7,89.9],[191.2,151.7],[226.7,213.5],[120.0,213.5],[13.2,213.5],[48.8,151.7],[84.5,89.9]]);
const TRIANGLE_INNER = polyToCubics([[120.1,67.0],[144.2,109.1],[168.3,151.2],[192.4,193.3],[120.4,193.3],[48.5,193.3],[72.4,151.2],[96.2,109.1]]);
const LAYER2_DIAMOND = polyToCubics([[118.0,131.6],[106.4,120.0],[159.9,66.5],[213.5,120.0],[159.9,174.0],[116.0,129.6],[130.0,115.6],[159.9,145.8],[185.4,120.0],[159.9,94.1],[134.1,120.0],[132.0,117.6]]);
const LAYER2_SHIELD = [81.5,156.7, 71.3,145.2,66.8,133.0,66.8,119.5, 66.8,90.4,90.6,66.8,120.0,66.8, 149.4,66.8,173.2,90.4,173.2,119.5, 173.2,126.5,171.2,133.8,167.6,141.0, 165.0,146.4,162.0,151.6,158.5,156.7, ...lineSeg(158.5,156.7,147.3,138.6), 150.8,133.2,152.2,126.5,152.2,119.5, 152.2,101.8,137.8,87.8,120.0,87.8, 102.2,87.8,87.8,101.8,87.8,119.5, 87.8,124.2,88.6,128.8,90.2,133.2, 90.9,135.1,91.7,136.9,92.7,138.6, ...lineSeg(92.7,138.6,81.5,156.7)];
const LAYER2_TRIANGLE = polyToCubics([[70.8,133.4],[82.4,113.3],[120.2,113.3],[158.0,113.3],[163.8,123.3],[169.5,133.4],[154.0,133.4],[137.0,133.4],[120.2,133.4],[103.4,133.4],[86.4,133.4],[74.0,133.4]]);
const LAYER3_DIAMOND = polyToCubics([[119.6,27.1],[136.3,43.5],[119.9,59.5],[103.2,43.7]]);
const LAYER3_SHIELD = polyToCubics([[120.0,16.5],[129.0,23.5],[120.0,30.5],[111.0,23.5]]);
const LAYER3_TRIANGLE = polyToCubics([[120.2,40.0],[128.5,52.0],[120.2,62.0],[111.9,52.0]]);
const LAYER4_DIAMOND = polyToCubics([[119.5,180.3],[128.2,188.3],[136.9,196.4],[119.5,212.6],[102.9,196.4],[111.2,188.3]]);
const LAYER4_SHIELD = polyToCubics([[120.0,132.9],[136.6,159.4],[153.3,185.9],[120.0,185.9],[86.5,185.9],[103.2,159.4]]);
const LAYER4_TRIANGLE = [120.2,179.6, ...lineSeg(120.2,179.6,153.9,123.3), ...lineSeg(153.9,123.3,169.5,133.4), 152.5,163.3,135.4,193.3,120.2,203.0, 105.0,193.3,87.9,163.3,70.8,133.4, ...lineSeg(70.8,133.4,86.5,123.3), ...lineSeg(86.5,123.3,120.2,179.6)];

const STATES = [
  [[...DIAMOND_OUTER, ...DIAMOND_INNER], LAYER2_DIAMOND, LAYER3_DIAMOND, LAYER4_DIAMOND],
  [[...SHIELD_OUTER, ...SHIELD_INNER], LAYER2_SHIELD, LAYER3_SHIELD, LAYER4_SHIELD],
  [[...TRIANGLE_OUTER, ...TRIANGLE_INNER], LAYER2_TRIANGLE, LAYER3_TRIANGLE, LAYER4_TRIANGLE]
];

const REDUCED = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

/* =========================================================
   STATIC ICONS
   ========================================================= */
document.querySelectorAll("svg[data-icon]").forEach(svg => {
  const d = ICON_PATHS[+svg.dataset.icon];
  svg.innerHTML = svg.hasAttribute("data-metal")
    ? `<g fill="url(#iconMetal)" filter="url(#iconFinishSm)"><path fill-rule="evenodd" d="${d}"/></g>`
    : `<path fill-rule="evenodd" d="${d}"/>`;
});
// duplicate marquee content for seamless loop
const track = document.getElementById("stripTrack");
track.innerHTML += track.innerHTML;

/* =========================================================
   SPRING MORPH ENGINE
   ========================================================= */
function stepSpring(val, target, vel, k, c, dt) {
  const force = -k * (val - target) - c * vel;
  const nv = vel + force * dt;
  return [val + nv * dt, nv];
}
function buildSinglePath(n) {
  let d = `M ${n[0].toFixed(2)} ${n[1].toFixed(2)}`;
  for (let i = 2; i < n.length; i += 6)
    d += ` C ${n[i].toFixed(2)} ${n[i+1].toFixed(2)}, ${n[i+2].toFixed(2)} ${n[i+3].toFixed(2)}, ${n[i+4].toFixed(2)} ${n[i+5].toFixed(2)}`;
  return d + " Z";
}
function buildCompoundPath(n) {
  const h = n.length / 2;
  return buildSinglePath(n.slice(0, h)) + " " + buildSinglePath(n.slice(h));
}

class Morph {
  constructor(stage, { dock = null, tabSel = ".tab", interval = 2.4, k = 175, c = 22, start = 0, depth = 0, onSwitch = null } = {}) {
    const P = `<path fill-rule="evenodd"/><path/><path/><path/>`;
    if (depth) {
      // extruded 3D icon: stacked slices behind a brushed front face
      let html = `<div class="m3d">`;
      for (let i = depth; i >= 1; i--)
        html += `<svg viewBox="0 0 240 240" style="transform:translateZ(${(-i * 2.2).toFixed(1)}px)"><g fill="url(#iconMetalDark)">${P}</g></svg>`;
      html += `<svg viewBox="0 0 240 240"><g fill="url(#iconMetalFront)" filter="url(#iconEdge)">${P}</g></svg></div>`;
      stage.innerHTML = html;
      this.svg = stage.querySelector(".m3d");
    } else {
      stage.innerHTML = `<svg viewBox="0 0 240 240"><g filter="url(#iconFinish)" fill="url(#iconMetal)">${P}</g></svg>`;
      this.svg = stage.querySelector("svg");
    }
    this.depth = depth;
    this.paths = [...this.svg.querySelectorAll("path")];
    this.layers = STATES[start].map(a => ({ vals: [...a], vels: new Array(a.length).fill(0) }));
    Object.assign(this, { interval, k, c, onSwitch, active: start, elapsed: 0, scale: 1, sv: 0, paused: false, visible: true, settled: false });
    this.tabs = dock ? [...dock.querySelectorAll(tabSel)] : [];

    const pause = el => { el.addEventListener("mouseenter", () => this.paused = true); el.addEventListener("mouseleave", () => this.paused = false); };
    pause(stage); if (dock) pause(dock);
    stage.addEventListener("click", () => this.next());
    this.tabs.forEach((t, i) => t.addEventListener("click", () => this.to(i)));
    this.render();
  }
  to(i) {
    this.active = i; this.elapsed = 0; this.sv = -1.35; this.settled = false;
    this.tabs.forEach((t, j) => { t.classList.toggle("active", j === i); t.querySelector(".bar").style.transform = "scaleX(0)"; });
    if (REDUCED) {
      this.layers.forEach((l, li) => { l.vals = [...STATES[i][li]]; l.vels.fill(0); });
      this.sv = 0; this.render(); this.settled = true;
    }
    this.onSwitch && this.onSwitch(i);
  }
  next() { this.to((this.active + 1) % STATES.length); }
  render(blur = 0) {
    const ds = this.layers.map((l, i) => i === 0 ? buildCompoundPath(l.vals) : buildSinglePath(l.vals));
    this.paths.forEach((p, i) => p.setAttribute("d", ds[i % 4]));
    this.svg.style.transform = `scale(${this.scale.toFixed(4)})`;
    // CSS blur would flatten the 3D extrusion, so the hero skips it
    if (!this.depth) this.svg.style.filter = blur > 0.03 ? `blur(${blur.toFixed(2)}px)` : "none";
  }
  tick(dt) {
    if (!this.visible) return;
    if (!this.paused && !REDUCED) {
      this.elapsed += dt;
      const t = this.tabs[this.active];
      if (t) t.querySelector(".bar").style.transform = `scaleX(${Math.min(this.elapsed / this.interval, 1).toFixed(4)})`;
      if (this.elapsed >= this.interval) this.next();
    }
    if (this.settled) return;

    const target = STATES[this.active];
    let speed = 0;
    for (let i = 0; i < 4; i++) {
      const l = this.layers[i], tg = target[i];
      for (let j = 0; j < l.vals.length; j++) {
        const [v, vel] = stepSpring(l.vals[j], tg[j], l.vels[j], this.k, this.c, dt);
        l.vals[j] = v; l.vels[j] = vel; speed += Math.abs(vel);
      }
    }
    [this.scale, this.sv] = stepSpring(this.scale, 1, this.sv, 210, 19, dt);

    if (speed < 0.4 && Math.abs(this.scale - 1) < 0.0005 && Math.abs(this.sv) < 0.01) {
      this.layers.forEach((l, i) => { l.vals = [...target[i]]; l.vels.fill(0); });
      this.scale = 1; this.sv = 0; this.settled = true;
      this.render(0); return;
    }
    this.render(Math.min(speed / 18000, 0.55));
  }
}

/* ---------- Instances ---------- */
const pListSpans = [...document.querySelectorAll("#pList span")];
const hero = new Morph(document.getElementById("heroStage"), {
  dock: document.getElementById("heroChips"), tabSel: ".chip", start: 1, depth: 10, interval: 2.8,
  onSwitch(i) { pListSpans.forEach((sp, j) => sp.classList.toggle("on", j === i)); }
});
hero.to(1);
const lab = new Morph(document.getElementById("labStage"), { dock: document.getElementById("labDock"), interval: 2.0 });
const cta = new Morph(document.getElementById("ctaStage"), { interval: 2.0, start: 1 });
const morphs = [hero, lab, cta];

const vis = new IntersectionObserver(entries => entries.forEach(e => {
  const m = morphs.find(m => m.svg.parentElement === e.target);
  if (m) m.visible = e.isIntersecting;
}), { rootMargin: "100px" });
morphs.forEach(m => vis.observe(m.svg.parentElement));

/* pointer parallax on the hero scene (spring-driven) */
const worldEl = document.getElementById("world");
const heroEl = document.getElementById("top");
const par = { rx: -19, ry: -34, vx: 0, vy: 0, tx: -19, ty: -34 };
heroEl.addEventListener("pointermove", e => {
  const r = heroEl.getBoundingClientRect();
  const nx = (e.clientX - r.left) / r.width - 0.5, ny = (e.clientY - r.top) / r.height - 0.5;
  par.ty = -34 + nx * 12; par.tx = -19 - ny * 7;
});
heroEl.addEventListener("pointerleave", () => { par.tx = -19; par.ty = -34; });
function tickParallax(dt) {
  if (REDUCED || !hero.visible) return;
  [par.rx, par.vx] = stepSpring(par.rx, par.tx, par.vx, 60, 14, dt);
  [par.ry, par.vy] = stepSpring(par.ry, par.ty, par.vy, 60, 14, dt);
  worldEl.style.setProperty("--rx", par.rx.toFixed(2) + "deg");
  worldEl.style.setProperty("--ry", par.ry.toFixed(2) + "deg");
}

/* dotted world map for the glass panel */
(function drawMap() {
  const rows = [
    "        ######      ###         #########           ",
    "    ###########   ###      ####################     ",
    "  ##############  ##    #########################   ",
    "   ############        ########################## # ",
    "    ##########         ####  #################      ",
    "     #######          ######   ##############       ",
    "      ######          #######   ######   ##         ",
    "       ###            ########   ####     #  #      ",
    "         ####          #######    ##      ###       ",
    "          #####         #####              ##  #    ",
    "          #######        ####                ###    ",
    "           ######        ###               #####    ",
    "            ####          ##              ######    ",
    "            ###                             ##      ",
    "            ##                                    # ",
    "            #                                       "
  ];
  let dots = "";
  rows.forEach((row, y) => [...row].forEach((ch, x) => {
    if (ch === "#") dots += `<circle cx="${x * 7.6 + 4}" cy="${y * 13 + 6}" r="2.1"/>`;
  }));
  document.getElementById("worldMap").innerHTML = `<g fill="rgba(255,255,255,0.5)">${dots}</g>`;
})();

let prevTime = performance.now();
function loop(now) {
  const dt = Math.min((now - prevTime) / 1000, 0.032);
  prevTime = now;
  morphs.forEach(m => m.tick(dt));
  tickParallax(dt);
  requestAnimationFrame(loop);
}
requestAnimationFrame(loop);

/* =========================================================
   MOTION LAB CONTROLS
   ========================================================= */
const kRange = document.getElementById("kRange"), cRange = document.getElementById("cRange");
const kOut = document.getElementById("kOut"), cOut = document.getElementById("cOut");
const curvePath = document.getElementById("curvePath"), settleOut = document.getElementById("settleOut");
const presetBtns = [...document.querySelectorAll("#presets button")];

function drawCurve(k, c) {
  const dt = 1 / 240, T = 1.4;
  let x = 0, v = 0, d = "", lastOut = 0;
  for (let i = 0, t = 0; t <= T; i++, t = i * dt) {
    [x, v] = stepSpring(x, 1, v, k, c, dt);
    if (Math.abs(x - 1) > 0.01) lastOut = t;
    if (i % 3 === 0) {
      const px = (t / T) * 300, py = 120 - x * 80;
      d += (d ? " L " : "M ") + px.toFixed(1) + " " + Math.max(-10, py).toFixed(1);
    }
  }
  curvePath.setAttribute("d", d);
  settleOut.textContent = lastOut >= T - dt ? "settles in >1400ms" : `settles in ${Math.round(lastOut * 1000)}ms`;
}
function applySpring(k, c, fromPreset) {
  lab.k = k; lab.c = c; kOut.textContent = k; cOut.textContent = c;
  kRange.value = k; cRange.value = c;
  if (!fromPreset) presetBtns.forEach(b => b.classList.remove("on"));
  drawCurve(k, c);
}
kRange.addEventListener("input", () => applySpring(+kRange.value, +cRange.value));
cRange.addEventListener("input", () => applySpring(+kRange.value, +cRange.value));
presetBtns.forEach(b => b.addEventListener("click", () => {
  presetBtns.forEach(x => x.classList.toggle("on", x === b));
  applySpring(+b.dataset.k, +b.dataset.c, true);
  lab.next();
}));
drawCurve(175, 22);

/* =========================================================
   CONTENT: pricing + FAQ
   ========================================================= */
const check = `<svg viewBox="0 0 24 24"><path d="M5 12.5l4.5 4.5L19 7.5" stroke-linecap="round" stroke-linejoin="round"/></svg>`;
const tiers = {
  tierA: ["Up to 10,000 monthly users", "Core policy engine", "3 environments", "Community support"],
  tierB: ["Unlimited users", "Continuous verification", "Audit log, 1-year retention", "SSO & SCIM", "Priority support"],
  tierC: ["Dedicated regions", "Custom data residency", "Signed audit exports", "99.999% SLA", "Named security engineer"]
};
Object.entries(tiers).forEach(([id, items]) => {
  document.getElementById(id).innerHTML = items.map(t => `<li>${check}${t}</li>`).join("");
});

const faqs = [
  ["How long does integration take?", "Most teams ship their first policy in under ten minutes using our SDKs. A full migration from an in-house system typically takes one to two sprints, and you can run both side by side in shadow mode."],
  ["Where are decisions evaluated?", "At the edge, close to your users. Compiled policies are distributed to every region, so evaluation never waits on a round-trip to a central server."],
  ["What happens if Facetry goes down?", "Each SDK keeps a signed local cache of your policies. If the network disappears, decisions continue from the last known-good version and sync back when connectivity returns."],
  ["Can I bring my own identity provider?", "Yes. Facetry works with any OIDC or SAML provider and syncs groups via SCIM, so your existing directory stays the source of truth."]
];
const faqList = document.getElementById("faqList");
faqList.innerHTML = faqs.map(([q, a], i) => `
  <div class="q reveal" style="--d:${i * 0.05}s">
    <button aria-expanded="false">${q}<span class="plus"></span></button>
    <div class="a"><div><p>${a}</p></div></div>
  </div>`).join("");
faqList.querySelectorAll(".q").forEach(q => {
  q.querySelector("button").addEventListener("click", () => {
    const open = q.classList.toggle("open");
    q.querySelector("button").setAttribute("aria-expanded", open);
  });
});

/* =========================================================
   REVEAL + COUNTERS
   ========================================================= */
const revealIO = new IntersectionObserver(entries => entries.forEach(e => {
  if (e.isIntersecting) { e.target.classList.add("in"); revealIO.unobserve(e.target); }
}), { threshold: 0.15, rootMargin: "0px 0px -40px 0px" });
document.querySelectorAll(".reveal").forEach(el => revealIO.observe(el));

function countUp(el) {
  const target = +el.dataset.count, dec = +(el.dataset.dec || 0);
  if (REDUCED) { el.textContent = target.toFixed(dec); return; }
  let x = 0, v = 0, prev = performance.now();
  (function f(now) {
    const dt = Math.min((now - prev) / 1000, 0.032); prev = now;
    [x, v] = stepSpring(x, 1, v, 60, 15, dt);
    el.textContent = (Math.min(x, 1) * target).toFixed(dec);
    if (Math.abs(1 - x) > 0.0005 || Math.abs(v) > 0.001) requestAnimationFrame(f);
    else el.textContent = target.toFixed(dec);
  })(prev);
}
const countIO = new IntersectionObserver(entries => entries.forEach(e => {
  if (e.isIntersecting) { countUp(e.target); countIO.unobserve(e.target); }
}), { threshold: 0.6 });
document.querySelectorAll("[data-count]").forEach(el => countIO.observe(el));

/* =========================================================
   TERMINUS: ghost facet, spotlight, join form, live regions
   ========================================================= */
document.getElementById("ghostPath").setAttribute("d", ICON_PATHS[2]);

const term = document.getElementById("term");
term.addEventListener("pointermove", e => {
  const r = term.getBoundingClientRect();
  term.style.setProperty("--mx", `${e.clientX - r.left}px`);
  term.style.setProperty("--my", `${e.clientY - r.top}px`);
});

const joinForm = document.getElementById("joinForm");
joinForm.addEventListener("submit", e => {
  e.preventDefault();
  joinForm.classList.add("sent");
  joinForm.querySelector("input").blur();
  cta.next();
  setTimeout(() => { joinForm.classList.remove("sent"); joinForm.reset(); }, 3200);
});

const REGIONS = [
  { code: "SFO", tz: "America/Los_Angeles", base: 4 },
  { code: "IAD", tz: "America/New_York", base: 5 },
  { code: "LHR", tz: "Europe/London", base: 6 },
  { code: "FRA", tz: "Europe/Berlin", base: 5 },
  { code: "SIN", tz: "Asia/Singapore", base: 7 },
  { code: "SYD", tz: "Australia/Sydney", base: 8 }
];
const regionGrid = document.getElementById("regionGrid");
regionGrid.innerHTML = REGIONS.map(r => `
  <div class="region">
    <span class="rcode">${r.code}</span>
    <span class="time">--:--:--</span>
    <span class="lat">— ms</span>
    <span class="lat-bar"><i></i></span>
  </div>`).join("");
const regionEls = [...regionGrid.children];
const fmts = REGIONS.map(r => new Intl.DateTimeFormat("en-GB", { timeZone: r.tz, hour: "2-digit", minute: "2-digit", second: "2-digit", hour12: false }));

function tickRegions() {
  const now = new Date();
  REGIONS.forEach((r, i) => {
    const el = regionEls[i];
    el.querySelector(".time").textContent = fmts[i].format(now);
    const ms = r.base + Math.random() * 1.6 - 0.4;
    el.querySelector(".lat").textContent = `p50 ${ms.toFixed(1)} ms`;
    el.querySelector(".lat-bar i").style.transform = `scaleX(${Math.min(ms / 12, 1).toFixed(3)})`;
  });
}
tickRegions();
setInterval(tickRegions, 1000);
</script>
</body>
</html>
```

