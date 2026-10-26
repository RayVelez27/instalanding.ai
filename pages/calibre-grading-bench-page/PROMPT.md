INSTALANDING.AI · Calibre Grading Bench Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Calibre Grading Bench Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/calibre-grading-bench-page

calibre-bench.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Calibre Grading Bench Page
  slug     calibre-grading-bench-page
  prompt   https://instalanding.ai/p/calibre-grading-bench-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/calibre-grading-bench-page
  license  MIT. Fictional brand; every name and number is invented. Replace them before shipping.
  lineage  Bred from Machine Front Panel Page (Kiln: the lamps, the gauge and needle, the amber, the display type) ×
           Highlighter Markup Page (Footnote: the serif, the claim-by-claim document and the verdict highlighters).

  MAP
  tokens    :root custom properties at the top of <style>: surfaces (--void, --alu*, --well, --line), three text
            greys (--text-1/2/3), the amber accent, the verdict system (--v-* lamp tones and --hl-* highlighter tones,
            one hue per verdict), fonts (--display Archivo, --serif Source Serif 4, --mono JetBrains Mono), a 4px
            spacing scale (--s1..--s9), three radii and --ease
  sections  nav, hero, verdicts, how-it-works, stats, faq, cta, footer
  scripts   one inline <script>, no libraries: the bench (gauge ticks, scans the answer claim by claim, draws each
            mark, swings the needle on a damped spring, lights the verdict chips, sets the gate; the replay button
            reruns it, a claim or the next arrow shows its source), marks that draw in on view, rolling counters,
            scroll reveals, the sign-up message
  assets    none: the planet horizon, terrain, glass source cards and gauge are CSS and inline SVG; the highlighter
            edge is an SVG displacement filter (#rough); fonts from Google Fonts

  ADAPTING
  - The highlighter means a verdict: it appears only on the bench and the verdict cards. A mark is coloured by its
    ::before through --c; the claims are split by the script into one marked word each (.w) so they can wrap.
  - Keep the page's figures in agreement with the bench: score 64 = (1 + 0.85 + 0.35 + 1 + 0) / 5, gate at 80,
    2 grounded / 1 reworded / 1 stretched / 1 unsupported. Change a claim's data-v and update the copy with it.
  - The needle is a spring (stiffness 120, damping 14) toward the running score; the loop stops when it settles.
    Under prefers-reduced-motion the bench renders finished, with no scan.
  - The planet is a 1380px circle clipped by .stage. The floating source cards are children of .hero (not the stage),
    placed from its top either side of the copy; they hide under 1280px, where the copy leaves no room beside it.
-->
<html lang="en">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Calibre — measure every answer before it ships</title>
<meta name="description" content="A fictional evaluation bench for AI answers: it reads a model's answer claim by claim, marks each one in its verdict colour and swings a needle to the score." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Archivo:wdth,wght@62..125,100..900&family=JetBrains+Mono:wght@400;500;700&family=Source+Serif+4:ital,opsz,wght@0,8..60,400;0,8..60,600;1,8..60,400&display=swap" rel="stylesheet" />
<style>
:root {
  /* surfaces */
  --void: #08090b;
  --alu-hi: #26292e;
  --alu: #1c1e23;
  --alu-lo: #15161a;
  --well: #0e0f12;
  --line: rgba(255, 255, 255, 0.07);
  --line-strong: rgba(255, 255, 255, 0.12);

  /* text: three steps only */
  --text-1: #eceef1;
  --text-2: #a8aeb7;
  --text-3: #7d838d;

  /* brand accent */
  --amber: #ff9426;
  --amber-hi: #ffb562;
  --amber-lo: #e5750e;

  /* verdict system: one hue per verdict, a lamp tone and a highlighter tone */
  --v-green: #4ad87a;   --hl-green: hsl(100, 38%, 27%);
  --v-yellow: #ffd34d;  --hl-yellow: hsl(44, 62%, 28%);
  --v-orange: #ff7d3a;  --hl-orange: hsl(22, 66%, 30%);
  --v-red: #ff4f44;     --hl-red: hsl(4, 58%, 33%);

  /* sheet: the dark card that holds documents and content */
  --paper: #18191d;
  --paper-2: #0f1013;
  --ink: #eceef1;
  --ink-2: #a8aeb7;
  --rule: rgba(255, 255, 255, 0.08);


  --display: "Archivo", "Helvetica Neue", Arial, sans-serif;
  --serif: "Source Serif 4", Georgia, serif;
  --mono: "JetBrains Mono", ui-monospace, monospace;

  /* scale */
  --s1: 4px; --s2: 8px; --s3: 12px; --s4: 16px; --s5: 24px; --s6: 32px; --s7: 48px; --s8: 64px; --s9: 96px;
  --r-lg: 16px; --r-md: 10px; --r-sm: 4px;

  --ease: cubic-bezier(0.2, 0.8, 0.2, 1);
  --wrap: min(1160px, 100% - 48px);
}

*, *::before, *::after { box-sizing: border-box; }
html { background: var(--void); scroll-behavior: smooth; scroll-padding-top: 88px; }
body {
  margin: 0;
  color: var(--text-2);
  font: 400 17px/1.6 var(--serif);
  background: var(--void);
  overflow-x: clip;
  -webkit-font-smoothing: antialiased;
}
a { color: inherit; }
:focus-visible { outline: 2px solid var(--amber); outline-offset: 3px; border-radius: 4px; }
p { margin: 0; }

/* ---------- type ---------- */
.label {
  display: inline-flex; align-items: center; gap: var(--s2);
  font: 500 11px/1.2 var(--mono); letter-spacing: 0.16em; text-transform: uppercase; color: var(--text-3);
}
h1, h2, h3 { margin: 0; color: var(--text-1); }
h2 { font: 800 clamp(30px, 3.2vw, 44px)/1.05 var(--display); letter-spacing: -0.025em; }
h3 { font: 600 21px/1.3 var(--serif); }

.sr-only { position: absolute; width: 1px; height: 1px; padding: 0; margin: -1px; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; border: 0; }

.lamp { --l: var(--amber); flex: none; display: inline-block; width: 8px; height: 8px; border-radius: 50%; background: #2a2d33; box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.6); transition: background 0.25s, box-shadow 0.25s; }
.lamp.on { background: var(--l); box-shadow: 0 0 10px var(--l), 0 0 2px var(--l); }
.l-green { --l: var(--v-green); } .l-yellow { --l: var(--v-yellow); } .l-orange { --l: var(--v-orange); } .l-red { --l: var(--v-red); }

/* ---------- the highlighter: means a verdict, never decoration ---------- */
mark.hl { position: relative; isolation: isolate; display: inline-block; padding: 0 0.12em; margin: 0 -0.04em; color: inherit; background: none; }
mark.hl::before, .claim .w::before {
  content: ""; position: absolute; z-index: -1;
  inset: 0.18em -0.05em 0.08em;
  border-radius: 0.2em 0.35em 0.25em 0.4em;
  background: var(--c, var(--hl-green));
  filter: url(#rough);
  transform-origin: left center;
  transform: scaleX(var(--p, 1));
  transition: transform 0.6s var(--ease);
}
mark.claim { display: inline; padding: 0; margin: 0; isolation: auto; cursor: pointer; border-radius: 3px; }
mark.claim::before { display: none; }
.claim:focus-visible { outline: 2px solid var(--ink); outline-offset: 2px; }
.claim .w { position: relative; isolation: isolate; display: inline-block; }
.claim .w::before { inset: 0.18em -0.2em 0.08em -0.06em; transition-delay: calc(var(--i, 0) * 40ms); }
.claim .w:last-child::before { right: -0.06em; }
mark.hl.draw { --p: 0; }
mark.hl.drawn { --p: 1; }
.v-green { --c: var(--hl-green); } .v-yellow { --c: var(--hl-yellow); }
.v-orange { --c: var(--hl-orange); } .v-red { --c: var(--hl-red); }

/* ---------- buttons ---------- */
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 10px;
  height: 46px; padding: 0 var(--s5); border: 0; border-radius: var(--r-md); cursor: pointer; text-decoration: none; white-space: nowrap;
  font: 700 15px/1 var(--display); letter-spacing: -0.005em;
  transition: transform 0.2s var(--ease), box-shadow 0.2s var(--ease), filter 0.2s, background 0.2s;
}
.btn-sm { height: 40px; padding: 0 var(--s5); font-size: 14px; }
.btn-lg { height: 54px; padding: 0 var(--s6); font-size: 16px; border-radius: 12px; }
.btn-primary { color: #1b0c02; background: linear-gradient(180deg, var(--amber-hi), var(--amber) 48%, var(--amber-lo)); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), 0 2px 0 #7a3a07, 0 12px 30px -10px rgba(255, 148, 38, 0.7); }
.btn-secondary { color: var(--text-1); background: linear-gradient(180deg, #2e3137, #22252a); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.09), 0 2px 0 #0b0c0f, 0 0 0 1px rgba(0, 0, 0, 0.6); }
.btn-ghost { color: var(--text-1); background: rgba(14, 15, 18, 0.7); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.14); backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px); }
.btn-ghost:hover { background: rgba(28, 30, 35, 0.8); }
.btn:hover { transform: translateY(-1px); filter: brightness(1.05); }
.btn:active { transform: translateY(1px); }
.btn:disabled { cursor: default; opacity: 0.6; transform: none; filter: none; }

/* ---------- nav ---------- */
.nav-bar { position: sticky; top: 0; z-index: 30; background: linear-gradient(180deg, rgba(8, 9, 11, 0.85), rgba(8, 9, 11, 0.55)); backdrop-filter: blur(14px) saturate(1.3); -webkit-backdrop-filter: blur(14px) saturate(1.3); border-bottom: 1px solid rgba(255, 255, 255, 0.04); }
.nav { width: min(1180px, 100% - 48px); margin: 0 auto; height: 72px; display: grid; grid-template-columns: 1fr auto 1fr; align-items: center; gap: var(--s5); }
.brand { justify-self: start; display: flex; align-items: center; gap: 14px; font: 800 17px/1 var(--display); font-stretch: 118%; letter-spacing: 0.22em; color: var(--text-1); text-decoration: none; text-transform: uppercase; }
.brand svg { color: var(--amber); filter: drop-shadow(0 0 8px rgba(255, 148, 38, 0.45)); }
.nav ul { display: flex; gap: 38px; margin: 0; padding: 0; list-style: none; }
.nav ul a { font: 500 15px/1 var(--display); color: var(--text-2); text-decoration: none; transition: color 0.2s; }
.nav ul a:hover { color: var(--text-1); }
.nav-actions { justify-self: end; display: flex; gap: var(--s3); }

/* ============================================================
   HERO
   ============================================================ */
.hero { position: relative; isolation: isolate; padding-top: var(--s6); text-align: center; overflow: hidden; }
.hero::before { /* warm ceiling glow */
  content: ""; position: absolute; z-index: -3; left: 50%; top: -260px; width: 1400px; height: 760px; transform: translateX(-50%);
  background: radial-gradient(closest-side, rgba(255, 140, 40, 0.09), transparent 70%); pointer-events: none;
}
.hero-copy { width: min(1180px, 100% - 48px); margin: 0 auto; display: flex; flex-direction: column; align-items: center; }
.pill { display: inline-flex; align-items: center; gap: 12px; height: 38px; padding: 0 20px; border-radius: 999px; background: rgba(14, 15, 18, 0.7); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.1); font: 500 12px/1 var(--mono); letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-2); }
.pill .lamp { width: 9px; height: 9px; }
.hero h1 {
  margin-top: 22px;
  font: 900 clamp(40px, 5.5vw, 86px)/0.92 var(--display); font-stretch: 110%; letter-spacing: -0.03em; text-transform: uppercase;
  color: #f4f5f7; text-shadow: 0 2px 30px rgba(0, 0, 0, 0.5);
}
.hero h1 .row { display: block; }
.hero h1 .gold {
  filter: drop-shadow(0 0 28px rgba(255, 150, 40, 0.18));
}
.hero .lede { max-width: 700px; margin: var(--s5) auto 0; font: 400 clamp(17px, 1.45vw, 21px)/1.55 var(--display); color: #b3b8c0; }
.hero .lede em { font: italic 400 1.06em/1 var(--serif); color: #e8eaed; }
.ctas { display: flex; flex-wrap: wrap; justify-content: center; gap: var(--s5); margin-top: var(--s6); }
.ctas .btn-ghost { min-width: 208px; }
.trust { display: flex; flex-wrap: wrap; justify-content: center; gap: var(--s3) var(--s7); margin: var(--s6) 0 0; padding: 0; list-style: none; font: 400 15px/1.4 var(--display); color: var(--text-2); }
.trust li { display: flex; align-items: center; gap: 14px; }
.trust svg { color: var(--amber); flex: none; }

/* ---------- the stage: planet, terrain, floating sources, bench ---------- */
.stage { position: relative; width: 100%; clip-path: inset(-700px 0 0 0); margin: 0 auto; padding: 64px 24px 120px; }
.planet {
  position: absolute; z-index: -2; left: 50%; top: 38px; width: 1380px; aspect-ratio: 1; transform: translateX(-50%); border-radius: 50%;
  background:
    radial-gradient(120% 60% at 50% 0%, rgba(255, 150, 60, 0.22), transparent 26%),
    radial-gradient(closest-side, #0b0b0d 92%, #120d0a 99%);
  box-shadow:
    inset 0 3px 2px -1px rgba(255, 226, 180, 0.95),
    inset 0 18px 40px -12px rgba(255, 150, 50, 0.7),
    inset 0 80px 120px -60px rgba(255, 120, 30, 0.35),
    0 -6px 30px rgba(255, 160, 70, 0.45),
    0 -30px 120px rgba(255, 130, 40, 0.28),
    0 -80px 260px rgba(255, 110, 20, 0.14);
}
.flare { position: absolute; z-index: -1; width: 180px; height: 2px; border-radius: 2px; background: linear-gradient(90deg, transparent, rgba(255, 200, 140, 0.9), transparent); filter: blur(0.5px); pointer-events: none; }
.flare::after { content: ""; position: absolute; left: 50%; top: 50%; width: 14px; height: 14px; transform: translate(-50%, -50%); border-radius: 50%; background: #fff3e0; box-shadow: 0 0 18px 6px rgba(255, 170, 80, 0.8), 0 0 60px 20px rgba(255, 130, 40, 0.35); }
.flare.f1 { left: calc(50% - 560px); top: 222px; }
.flare.f2 { left: calc(50% + 380px); top: 222px; }
.spark { position: absolute; z-index: -1; width: 3px; height: 3px; border-radius: 50%; background: #ffd9a8; box-shadow: 0 0 8px 2px rgba(255, 160, 70, 0.8); animation: twinkle 3.6s ease-in-out infinite; animation-delay: var(--d, 0s); }
@keyframes twinkle { 0%, 100% { opacity: 0.35; transform: scale(0.8); } 50% { opacity: 1; transform: scale(1.2); } }
.terrain { position: absolute; z-index: -1; left: 50%; bottom: -20px; width: max(1600px, 100%); height: 420px; transform: translateX(-50%); pointer-events: none; }
.terrain.front { z-index: 2; height: 300px; bottom: -40px; }
.hero-fade { position: absolute; z-index: 3; left: 0; right: 0; bottom: 0; height: 120px; background: linear-gradient(180deg, transparent, var(--void)); pointer-events: none; }

/* floating glass source cards */
.src {
  position: absolute; z-index: 1; width: 214px; padding: 18px 18px 16px; border-radius: 14px; text-align: left;
  background: linear-gradient(160deg, rgba(255, 255, 255, 0.09), rgba(255, 255, 255, 0.02) 60%);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.14), inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 30px 50px -20px rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(8px); -webkit-backdrop-filter: blur(8px);
  display: grid; grid-template-columns: auto 1fr; gap: 10px 18px; align-items: center;
  transform: perspective(900px) rotateY(var(--ry)) rotateZ(var(--rz)); animation: drift 7s ease-in-out infinite; animation-delay: var(--d, 0s);
}
@keyframes drift { 0%, 100% { translate: 0 0; } 50% { translate: 0 -8px; } }
.src svg { color: #c9ccd1; }
.src .lines { display: grid; gap: 7px; }
.src .lines i { display: block; height: 3px; border-radius: 2px; background: rgba(255, 255, 255, 0.22); }
.src .lines i:nth-child(2) { width: 82%; } .src .lines i:nth-child(3) { width: 64%; } .src .lines i:nth-child(4) { width: 74%; }
.src .label { grid-column: 1 / -1; font-size: 10px; letter-spacing: 0.16em; color: var(--text-2); }
/* in the empty space either side of the hero copy, measured from the top of .hero */
.src.s3 { left: max(12px, calc(50% - 700px)); top: 58px; --ry: 22deg; --rz: 8deg; }
.src.s1 { left: max(44px, calc(50% - 650px)); top: 318px; --ry: 22deg; --rz: 5deg; --d: -2s; }
.src.s2 { right: max(12px, calc(50% - 700px)); top: 88px; --ry: -22deg; --rz: -6deg; --d: -4s; }
.src.s4 { right: max(44px, calc(50% - 660px)); top: 348px; --ry: -22deg; --rz: -4deg; --d: -1s; }

/* the bench */
.bench-wrap { position: relative; z-index: 2; perspective: 2000px; }
.bench {
  position: relative; width: min(900px, 100%); margin: 0 auto; padding: 22px; border-radius: 24px; text-align: left;
  background: linear-gradient(180deg, rgba(36, 38, 44, 0.92), rgba(15, 16, 19, 0.96) 40%);
  box-shadow:
    inset 0 0 0 1px rgba(255, 255, 255, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.22),
    0 0 0 1px rgba(0, 0, 0, 0.7), 0 50px 90px -30px rgba(0, 0, 0, 0.95), 0 0 80px -20px rgba(255, 140, 40, 0.35);
  backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
  transform: rotateX(9deg); transform-origin: 50% 100%;
}
.bench::before { /* the stacked layer behind */
  content: ""; position: absolute; z-index: -1; inset: 0; border-radius: 26px; transform: translate(-16px, -14px);
  background: linear-gradient(180deg, rgba(40, 42, 48, 0.75), rgba(18, 19, 22, 0.75));
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.1), inset 0 1px 0 rgba(255, 255, 255, 0.18);
}
.bench::after { /* rim light on the lower edge */
  content: ""; position: absolute; left: 6%; right: 6%; bottom: -1px; height: 2px; border-radius: 2px;
  background: linear-gradient(90deg, transparent, rgba(255, 170, 90, 0.9), transparent); filter: blur(0.5px); box-shadow: 0 0 24px 2px rgba(255, 140, 40, 0.5);
}
.bench-top { display: flex; align-items: center; justify-content: space-between; gap: var(--s4); margin: 2px 4px 16px; }
.bench-top .label { color: var(--text-2); letter-spacing: 0.18em; font-size: 12px; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.status { display: flex; align-items: center; gap: 12px; font: 500 12px/1 var(--mono); letter-spacing: 0.16em; text-transform: uppercase; color: var(--text-2); white-space: nowrap; }
.status .lamp { --l: var(--amber); }
.status[data-state="done"] .lamp { --l: var(--v-green); }
.status[data-state="busy"] .lamp { animation: pulse 0.9s ease-in-out infinite; }
@keyframes pulse { 50% { opacity: 0.3; } }
.icon-btn { display: grid; place-items: center; width: 34px; height: 34px; border: 0; border-radius: 10px; cursor: pointer; color: var(--text-2); background: rgba(255, 255, 255, 0.05); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.1); transition: color 0.2s, background 0.2s; }
.icon-btn:hover { color: var(--text-1); background: rgba(255, 255, 255, 0.09); }
.icon-btn:disabled { opacity: 0.4; cursor: default; }

.bench-grid { display: grid; grid-template-columns: minmax(0, 1.6fr) minmax(0, 1fr); gap: 14px; }
.card { position: relative; border-radius: 16px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.035), rgba(255, 255, 255, 0.01)), #111215; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08), inset 0 1px 0 rgba(255, 255, 255, 0.06); }
.answer { padding: 20px 22px 22px; }
.answer-head { display: flex; justify-content: space-between; align-items: center; gap: var(--s3); margin-bottom: 16px; font: 500 11px/1.3 var(--mono); letter-spacing: 0.16em; text-transform: uppercase; color: var(--text-2); }
.answer-head b { display: flex; align-items: center; gap: 10px; font-weight: 700; color: var(--text-1); }
.answer p { font: 400 20px/1.75 var(--serif); color: #f3f4f6; }
.bench .claim .w::before { filter: none; border-radius: 2px; inset: 0.1em -0.26em 0 -0.08em; }
.bench .claim .w:last-child::before { right: -0.08em; }
.scanline { position: absolute; left: 14px; right: 14px; height: 2px; top: 0; background: linear-gradient(90deg, transparent, var(--amber), transparent); box-shadow: 0 0 14px var(--amber); opacity: 0; pointer-events: none; transition: top 0.45s var(--ease), opacity 0.3s; }
.answer.scanning .scanline { opacity: 1; }

.gauge { display: flex; flex-direction: column; align-items: center; justify-content: center; padding: 18px 16px 20px; text-align: center; }
.gauge svg { display: block; width: 100%; max-width: 210px; height: auto; overflow: visible; }
.needle { transform-origin: 85px 85px; transform: rotate(calc(-120deg + var(--a, 0) * 240deg)); }
.score { margin-top: -54px; font: 800 52px/1 var(--display); letter-spacing: -0.03em; color: var(--text-1); font-variant-numeric: tabular-nums; }
.score small { margin-left: 2px; font: 500 15px/1 var(--mono); letter-spacing: 0; color: var(--text-2); }
.gauge .label { margin-top: 12px; font-size: 12px; letter-spacing: 0.24em; color: var(--text-2); }
.gate { margin-top: 14px; display: inline-flex; align-items: center; gap: 8px; height: 26px; padding: 0 12px; border-radius: 999px; background: rgba(0, 0, 0, 0.35); box-shadow: inset 0 0 0 1px var(--line); font: 500 10px/1 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-3); }
.gate b { font-weight: 700; color: var(--text-2); }
.gate[data-state="pass"] b { color: var(--v-green); }
.gate[data-state="block"] b { color: var(--v-red); }

.chips { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 12px; margin-top: 14px; }
.chip { display: flex; align-items: center; gap: 12px; height: 50px; padding: 0 16px; border-radius: 12px; background: #111215; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08); font: 500 11px/1 var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-2); }
.chip .lamp { width: 9px; height: 9px; }
.chip b { margin-left: auto; font: 700 14px/1 var(--mono); color: var(--text-1); font-variant-numeric: tabular-nums; }

.source { display: flex; align-items: center; gap: 18px; margin-top: 14px; padding: 12px 12px 12px 12px; border-radius: 14px; background: #111215; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08); min-height: 78px; }
.source .tile { flex: none; display: grid; place-items: center; width: 56px; height: 56px; border-radius: 12px; background: radial-gradient(circle at 50% 45%, rgba(255, 148, 38, 0.18), transparent 70%), #0a0b0d; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08); color: var(--amber); }
.source .tile svg { filter: drop-shadow(0 0 8px rgba(255, 148, 38, 0.8)); }
.source .body { flex: 1; min-width: 0; font: 400 13px/1.55 var(--mono); color: var(--text-2); }
.source .body b { display: flex; align-items: center; gap: 8px; margin-bottom: 4px; font: 700 12px/1.3 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-1); }
.source .body b .lamp { --l: var(--c, var(--amber)); }

/* logo strip (invented names) */
.logos { position: relative; z-index: 4; width: min(1240px, 100% - 48px); margin: -40px auto 0; padding-bottom: var(--s7); text-align: center; }
.logos .label { letter-spacing: 0.22em; color: var(--text-3); }
.logos ul { display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; gap: var(--s5) var(--s7); margin: var(--s5) 0 0; padding: 0; list-style: none; }
.logos li { display: flex; align-items: center; gap: 10px; font: 600 21px/1 var(--display); letter-spacing: -0.01em; color: #8f949c; opacity: 0.9; }
.logos li:nth-child(3) { font-stretch: 120%; font-weight: 800; letter-spacing: 0.06em; font-size: 17px; text-transform: uppercase; }
.logos li:nth-child(5) { font-family: var(--serif); font-style: italic; font-weight: 600; font-size: 23px; }
.logos li:nth-child(7) { font-weight: 400; letter-spacing: 0.02em; }
.logos svg { flex: none; }

/* ============================================================
   SECTIONS · the hero's language carried down the page
   ============================================================ */
.gold {
  background: linear-gradient(92deg, #e6c43e 0%, #ffbb30 32%, #ffa22a 62%, #ff8c1e 100%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}
.sec { position: relative; isolation: isolate; width: var(--wrap); margin: 0 auto; padding: 140px 0; }
.sec::before { /* horizon hairline */
  content: ""; position: absolute; left: 50%; top: 0; width: min(880px, 92%); height: 1px; transform: translateX(-50%);
  background: linear-gradient(90deg, transparent, rgba(255, 176, 100, 0.38), transparent);
}
.sec::after { /* warm ambient glow under the hairline */
  content: ""; position: absolute; z-index: -1; left: 50%; top: -160px; width: min(1100px, 100%); height: 420px; transform: translateX(-50%);
  background: radial-gradient(closest-side, rgba(255, 140, 40, 0.075), transparent); pointer-events: none;
}
.sec-head { display: flex; flex-direction: column; align-items: center; gap: 22px; max-width: 780px; margin: 0 auto 64px; text-align: center; }
.sec-head h2 { font: 900 clamp(34px, 4.4vw, 62px)/0.95 var(--display); font-stretch: 110%; letter-spacing: -0.03em; text-transform: uppercase; color: #f4f5f7; }
.sec-head p { max-width: 620px; font: 400 clamp(17px, 1.35vw, 20px)/1.55 var(--display); color: #b3b8c0; }
.sec-head.left { align-items: flex-start; text-align: left; margin: 0; }
.sec-head .pill { max-width: none; font: 500 12px/1 var(--mono); letter-spacing: 0.2em; color: var(--text-2); }

/* glass: the bench's surface, reused for every card */
.glass {
  position: relative; border-radius: 20px;
  background: linear-gradient(180deg, rgba(34, 36, 42, 0.82), rgba(14, 15, 18, 0.92) 55%);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.09), inset 0 1px 0 rgba(255, 255, 255, 0.16), 0 30px 60px -30px rgba(0, 0, 0, 0.9);
  transition: transform 0.35s var(--ease), box-shadow 0.35s var(--ease);
}
.glass.lift:hover {
  transform: translateY(-4px);
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.14), inset 0 1px 0 rgba(255, 255, 255, 0.22), 0 40px 70px -30px rgba(0, 0, 0, 0.95), 0 0 60px -18px var(--glow, rgba(255, 140, 40, 0.45));
}
.itile {
  --tc: var(--amber);
  flex: none; display: grid; place-items: center; width: 52px; height: 52px; border-radius: 14px; color: var(--tc);
  background: radial-gradient(circle at 50% 42%, color-mix(in srgb, var(--tc) 24%, transparent), transparent 72%), #0a0b0d;
  box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08), 0 0 24px -8px color-mix(in srgb, var(--tc) 60%, transparent);
}
.itile svg { filter: drop-shadow(0 0 6px color-mix(in srgb, var(--tc) 70%, transparent)); }

/* vivid, flat marks: the bench and the verdict examples share them */
.bench, .vivid { --hl-green: #1d7a3b; --hl-yellow: #9c6c0e; --hl-orange: #b0481a; --hl-red: #a8202b; }
.vivid mark.hl::before { filter: none; border-radius: 3px; inset: 0.08em -0.04em 0; }

/* reveal on scroll */
.reveal { opacity: 0; transform: translateY(22px); transition: opacity 0.9s var(--ease), transform 0.9s var(--ease); }
.reveal.in { opacity: 1; transform: none; }

/* ---------- 01 verdicts ---------- */
.verdicts { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 20px; }
.vcard { --glow: color-mix(in srgb, var(--tc) 55%, transparent); display: flex; flex-direction: column; padding: 28px 24px 24px; overflow: hidden; }
.vcard::before { /* lit top edge in the verdict colour */
  content: ""; position: absolute; left: 22px; right: 22px; top: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--tc), transparent); box-shadow: 0 0 16px 1px var(--tc); opacity: 0.85;
}
.vcard::after {
  content: ""; position: absolute; z-index: -1; inset: 0; border-radius: inherit; pointer-events: none;
  background: radial-gradient(240px 150px at 50% -10px, color-mix(in srgb, var(--tc) 16%, transparent), transparent 75%);
}
.vcard .vtop { display: flex; align-items: center; justify-content: space-between; }
.vcard .itile { --tc: inherit; }
.vcard .weight { font: 500 11px/1 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-3); }
.vcard .weight b { font-weight: 700; color: var(--text-1); }
.vcard .tag { display: flex; align-items: center; gap: 10px; margin-top: 26px; font: 700 11px/1 var(--mono); letter-spacing: 0.18em; text-transform: uppercase; color: var(--tc); }
.vcard h3 { margin: 12px 0 10px; font: 700 22px/1.2 var(--display); letter-spacing: -0.01em; color: var(--text-1); }
.vcard p { font: 400 15px/1.6 var(--display); color: var(--text-2); }
.vcard .eg { margin-top: auto; padding-top: 22px; }
.vcard .eg > div { padding: 14px 16px; border-radius: 12px; background: #0b0c0f; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.07); }
.vcard .eg small { display: block; margin-bottom: 8px; font: 500 10px/1 var(--mono); letter-spacing: 0.18em; text-transform: uppercase; color: var(--text-3); }
.vcard .eg p { font: 400 17px/1.5 var(--serif); color: #f3f4f6; }
.scoring { display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 12px 28px; margin-top: 36px; font: 500 12px/1 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-3); }
.scoring code { font: inherit; color: var(--text-1); }
.scoring code i { font-style: normal; color: var(--amber); }

/* ---------- 02 how it works ---------- */
.steps { position: relative; display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 24px; }
.steps::before { /* the pipeline that joins the stages */
  content: ""; position: absolute; z-index: -1; left: 12%; right: 12%; top: 59px; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 148, 38, 0.7) 15%, rgba(255, 148, 38, 0.7) 85%, transparent);
}
.steps::after { /* a pulse that runs along it */
  content: ""; position: absolute; z-index: -1; top: 56px; left: 12%; width: 7px; height: 7px; border-radius: 50%;
  background: #ffe2c0; box-shadow: 0 0 14px 4px rgba(255, 148, 38, 0.8); animation: travel 4.5s linear infinite;
}
@keyframes travel { 0% { left: 12%; opacity: 0; } 8% { opacity: 1; } 92% { opacity: 1; } 100% { left: 88%; opacity: 0; } }
.step { display: flex; flex-direction: column; padding: 34px 28px 28px; }
.step .shead { display: flex; align-items: center; justify-content: space-between; }
.step .big { font: 800 52px/1 var(--display); font-stretch: 110%; letter-spacing: -0.03em; color: transparent; -webkit-text-stroke: 1px rgba(255, 255, 255, 0.14); }
.step .num { margin-top: 26px; font: 500 11px/1 var(--mono); letter-spacing: 0.2em; text-transform: uppercase; color: var(--amber); }
.step h3 { margin: 12px 0 10px; font: 800 28px/1.1 var(--display); font-stretch: 108%; letter-spacing: -0.02em; text-transform: uppercase; color: var(--text-1); }
.step p { font: 400 16px/1.6 var(--display); color: var(--text-2); }
.term { margin-top: auto; padding-top: 26px; }
.term > div { border-radius: 12px; background: #08090b; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.08), 0 14px 30px -16px rgba(0, 0, 0, 0.9); overflow: hidden; }
.term header { display: flex; align-items: center; gap: 6px; height: 32px; padding: 0 12px; border-bottom: 1px solid rgba(255, 255, 255, 0.06); font: 500 10px/1 var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--text-3); }
.term header i { width: 8px; height: 8px; border-radius: 50%; background: #2c2f35; }
.term header span { margin-left: auto; }
.term pre { margin: 0; padding: 14px 16px; font: 400 13px/1.75 var(--mono); color: var(--text-2); white-space: pre; overflow-x: auto; }
.term .p { color: var(--amber); } .term .ok { color: var(--v-green); } .term .y { color: var(--v-yellow); } .term .o { color: var(--v-orange); } .term .r { color: var(--v-red); }

/* ---------- 03 numbers ---------- */
.stats-panel { overflow: hidden; }
.stats-panel::before { /* lit top edge */
  content: ""; position: absolute; left: 8%; right: 8%; top: 0; height: 1px;
  background: linear-gradient(90deg, transparent, rgba(255, 176, 100, 0.9), transparent); box-shadow: 0 0 22px 2px rgba(255, 140, 40, 0.45);
}
.stats-panel::after {
  content: ""; position: absolute; z-index: -1; inset: 0; border-radius: inherit; pointer-events: none;
  background: radial-gradient(70% 120% at 50% -30%, rgba(255, 140, 40, 0.14), transparent 60%);
}
.stats { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); }
.stat { position: relative; padding: 48px 32px 44px; }
.stat + .stat::before { content: ""; position: absolute; left: 0; top: 18%; bottom: 18%; width: 1px; background: linear-gradient(180deg, transparent, rgba(255, 255, 255, 0.12), transparent); }
.stat .k { display: flex; align-items: center; gap: 10px; font: 500 11px/1 var(--mono); letter-spacing: 0.18em; text-transform: uppercase; color: var(--text-3); }
.stat .n {
  margin-top: 22px; font: 900 clamp(44px, 4.6vw, 68px)/1 var(--display); font-stretch: 110%; letter-spacing: -0.035em; font-variant-numeric: tabular-nums;
  background: linear-gradient(180deg, #ffffff 30%, #9ea4ad); -webkit-background-clip: text; background-clip: text; color: transparent;
}
.stat .n.hot { background: linear-gradient(92deg, #ffbb30, #ff8c1e); -webkit-background-clip: text; background-clip: text; }
.stat p { margin-top: 14px; font: 400 15px/1.5 var(--display); color: var(--text-2); }

/* ---------- 04 faq ---------- */
.faq-layout { display: grid; grid-template-columns: minmax(0, 0.85fr) minmax(0, 1.15fr); gap: 72px; align-items: start; }
.faq-side { position: sticky; top: 112px; display: grid; gap: 32px; }
.contact { display: flex; gap: 18px; align-items: flex-start; padding: 22px; }
.contact b { display: block; font: 700 17px/1.3 var(--display); color: var(--text-1); }
.contact p { margin-top: 6px; font: 400 15px/1.55 var(--display); color: var(--text-2); }
.contact a { display: inline-flex; gap: 8px; margin-top: 12px; font: 700 14px/1 var(--display); color: var(--amber); text-decoration: none; }
.contact a:hover { color: var(--amber-hi); }
.qa-list { display: grid; gap: 14px; }
.qa { border-radius: 18px; }
.qa[open] { box-shadow: inset 0 0 0 1px rgba(255, 148, 38, 0.35), inset 0 1px 0 rgba(255, 255, 255, 0.16), 0 30px 60px -30px rgba(0, 0, 0, 0.9), 0 0 50px -24px rgba(255, 140, 40, 0.5); }
.qa summary { display: flex; align-items: center; justify-content: space-between; gap: 20px; padding: 22px 24px; cursor: pointer; list-style: none; font: 700 18px/1.35 var(--display); letter-spacing: -0.005em; color: var(--text-1); }
.qa summary::-webkit-details-marker { display: none; }
.qa .plus { position: relative; flex: none; width: 34px; height: 34px; border-radius: 10px; background: #0a0b0d; box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.09); transition: transform 0.35s var(--ease), box-shadow 0.3s; }
.qa .plus::before, .qa .plus::after { content: ""; position: absolute; left: 50%; top: 50%; width: 12px; height: 1.6px; border-radius: 2px; background: var(--text-2); transform: translate(-50%, -50%); transition: background 0.3s, transform 0.35s var(--ease); }
.qa .plus::after { transform: translate(-50%, -50%) rotate(90deg); }
.qa[open] .plus { box-shadow: inset 0 0 0 1px rgba(255, 148, 38, 0.5), 0 0 16px -4px rgba(255, 148, 38, 0.7); }
.qa[open] .plus::before, .qa[open] .plus::after { background: var(--amber); }
.qa[open] .plus::before { transform: translate(-50%, -50%) rotate(45deg); }
.qa[open] .plus::after { transform: translate(-50%, -50%) rotate(135deg); }
.qa p { padding: 0 82px 24px 24px; font: 400 16px/1.65 var(--display); color: var(--text-2); }

/* ---------- 05 cta finale ---------- */
.finale { position: relative; overflow: hidden; isolation: isolate; padding: 104px 32px 200px; border-radius: 32px; text-align: center; }
.finale .planet { top: auto; bottom: -1150px; width: 1300px; z-index: -1; }
.finale .glowfloor { position: absolute; z-index: -1; left: 50%; bottom: -120px; width: 900px; height: 300px; transform: translateX(-50%); background: radial-gradient(closest-side, rgba(255, 140, 40, 0.28), transparent); pointer-events: none; }
.finale h2 { margin-top: 26px; font: 900 clamp(36px, 5.4vw, 80px)/0.92 var(--display); font-stretch: 110%; letter-spacing: -0.035em; text-transform: uppercase; color: #f4f5f7; }
.finale h2 .row { display: block; }
.finale .finale-lede { max-width: 560px; margin: 24px auto 0; font: 400 clamp(17px, 1.35vw, 20px)/1.55 var(--display); color: #b3b8c0; }
.cta-form { display: flex; gap: 8px; width: min(540px, 100%); margin: 40px auto 0; padding: 7px; border-radius: 16px; background: rgba(8, 9, 11, 0.75); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.12), 0 20px 50px -20px rgba(0, 0, 0, 0.9); backdrop-filter: blur(10px); -webkit-backdrop-filter: blur(10px); }
.cta-form:focus-within { box-shadow: inset 0 0 0 1px rgba(255, 148, 38, 0.55), 0 0 40px -12px rgba(255, 140, 40, 0.6); }
.cta-form input { flex: 1; min-width: 0; height: 50px; padding: 0 16px; border: 0; background: transparent; font: 400 16px var(--display); color: var(--text-1); outline: none; }
.cta-form input::placeholder { color: var(--text-3); }
.cta-form .btn { height: 50px; }
.cta-notes { display: flex; flex-wrap: wrap; justify-content: center; gap: 10px 28px; margin: 22px 0 0; padding: 0; list-style: none; font: 400 14px/1.4 var(--display); color: var(--text-2); }
.cta-notes li { display: flex; align-items: center; gap: 8px; }
.cta-notes svg { color: var(--v-green); }
.cta-msg { min-height: 22px; margin-top: 14px; font: 500 14px/1.4 var(--display); color: var(--v-green); }

/* ---------- footer ---------- */
.site-footer { position: relative; width: var(--wrap); margin: 0 auto; padding: 96px 0 40px; }
.site-footer::before { content: ""; position: absolute; left: 50%; top: 0; width: min(880px, 92%); height: 1px; transform: translateX(-50%); background: linear-gradient(90deg, transparent, rgba(255, 176, 100, 0.38), transparent); }
.f-top { display: grid; grid-template-columns: minmax(0, 1.6fr) repeat(3, minmax(0, 1fr)); gap: 40px; }
.f-brand p { max-width: 300px; margin-top: 18px; font: 400 15px/1.6 var(--display); color: var(--text-2); }
.f-status { display: inline-flex; align-items: center; gap: 10px; height: 32px; margin-top: 22px; padding: 0 14px; border-radius: 999px; background: rgba(14, 15, 18, 0.7); box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.1); font: 500 11px/1 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--text-2); }
.f-col h4 { margin: 0 0 18px; font: 500 11px/1 var(--mono); letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-3); }
.f-col ul { display: grid; gap: 12px; margin: 0; padding: 0; list-style: none; }
.f-col a { font: 400 15px/1.4 var(--display); color: var(--text-2); text-decoration: none; transition: color 0.2s; }
.f-col a:hover { color: var(--text-1); }
.f-bottom { display: flex; flex-wrap: wrap; justify-content: space-between; gap: 16px; margin-top: 72px; padding-top: 24px; border-top: 1px solid rgba(255, 255, 255, 0.06); font: 400 13px/1.6 var(--display); color: var(--text-3); }
.f-word { margin-top: 56px; font: 900 clamp(48px, 14.5vw, 240px)/0.8 var(--display); font-stretch: 125%; letter-spacing: 0; white-space: nowrap; overflow: hidden; text-transform: uppercase; text-align: center; color: transparent; -webkit-text-stroke: 1px rgba(255, 255, 255, 0.06); background: linear-gradient(180deg, rgba(255, 148, 38, 0.1), transparent 70%); -webkit-background-clip: text; background-clip: text; user-select: none; }

/* ---------- responsive ---------- */
/* while the source cards show, hold the headline to three lines so it never runs into them */
@media (min-width: 1280px) {
  .hero h1 { max-width: 11em; }
}
@media (max-width: 1279px) {
  .src { display: none; }
}
@media (max-width: 1040px) {
  .verdicts { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .stat:nth-child(3)::before { display: none; }
  .stat:nth-child(n+3) { border-top: 1px solid rgba(255, 255, 255, 0.07); }
  .faq-layout { grid-template-columns: minmax(0, 1fr); gap: 40px; }
  .faq-side { position: static; }
  .f-top { grid-template-columns: repeat(3, minmax(0, 1fr)); }
  .f-brand { grid-column: 1 / -1; }
  .nav { grid-template-columns: auto 1fr auto; }
  .nav ul { justify-content: center; gap: 26px; }
}
@media (max-width: 860px) {
  .nav ul { display: none; }
  .nav { grid-template-columns: 1fr auto; }
  .bench { transform: none; }
  .bench::before { transform: translate(-8px, -8px); }
  .bench-grid { grid-template-columns: minmax(0, 1fr); }
  .chips { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .planet { width: 1100px; top: 40px; }
  .logos ul { justify-content: center; }
  .steps { grid-template-columns: minmax(0, 1fr); max-width: 560px; margin: 0 auto; }
  .steps::before, .steps::after { display: none; }
}
@media (max-width: 760px) {
  :root { --wrap: min(1160px, 100% - 32px); }
  .nav, .hero-copy { width: min(1180px, 100% - 32px); }
  .sec { padding: 96px 0; }
  .sec-head { margin-bottom: 44px; }
  .stage { padding: 56px 16px 100px; }
  .bench { padding: 14px; border-radius: 20px; }
  .answer { padding: 16px; }
  .answer p { font-size: 17px; }
  .flare { display: none; }
  .finale { padding: 72px 20px 120px; border-radius: 24px; }
  .finale { padding-bottom: 210px; }
  .finale .planet { width: 900px; bottom: -790px; }
}
@media (max-width: 560px) {
  .nav-actions .btn-ghost { display: none; }
  .brand { letter-spacing: 0.16em; font-size: 15px; }
  .pill { font-size: 10px; letter-spacing: 0.16em; padding: 0 14px; }
  .ctas { width: 100%; gap: var(--s3); }
  .ctas .btn { flex: 1 1 100%; }
  .trust { flex-direction: column; align-items: flex-start; gap: var(--s3); align-self: center; }
  .chip { padding: 0 12px; gap: 8px; font-size: 10px; letter-spacing: 0.06em; }
  .bench-top .label { font-size: 10px; letter-spacing: 0.1em; }
  .bench-top .long, .answer-head .meta { display: none; }
  .status { font-size: 10px; letter-spacing: 0.1em; }
  .source .tile { width: 44px; height: 44px; }
  .verdicts { grid-template-columns: minmax(0, 1fr); }
  .stats { grid-template-columns: minmax(0, 1fr); }
  .stat { padding: 32px 24px; }
  .stat + .stat::before { display: none; }
  .stat + .stat { border-top: 1px solid rgba(255, 255, 255, 0.07); }
  .qa summary { padding: 18px; font-size: 16px; }
  .qa p { padding: 0 18px 20px; }
  .cta-form { flex-direction: column; }
  .cta-form .btn { width: 100%; }
  .cta-notes { flex-direction: column; align-items: center; }
  .f-top { grid-template-columns: 1fr 1fr; }
  .logos li { font-size: 17px; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after { transition: none !important; animation: none !important; }
  .reveal { opacity: 1; transform: none; }
}
</style>
</head>
<body>
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <filter id="rough" x="-5%" y="-20%" width="110%" height="140%">
    <feTurbulence type="fractalNoise" baseFrequency="0.045 0.6" numOctaves="2" seed="4" />
    <feDisplacementMap in="SourceGraphic" scale="4" />
  </filter>
</svg>

<div class="nav-bar" data-section="nav">
  <header class="nav">
    <a class="brand" href="#top" aria-label="Calibre home">
      <svg width="40" height="26" viewBox="0 0 40 26" fill="none" aria-hidden="true"><path d="M4 23a16 16 0 0 1 32 0" stroke="currentColor" stroke-width="5" stroke-linecap="round" /><path d="M20 22l7.5-9" stroke="currentColor" stroke-width="3.4" stroke-linecap="round" /><circle cx="20" cy="22" r="2.6" fill="currentColor" /></svg>
      Calibre
    </a>
    <ul>
      <li><a href="#verdicts">Verdicts</a></li>
      <li><a href="#how">How it works</a></li>
      <li><a href="#numbers">Numbers</a></li>
      <li><a href="#faq">FAQ</a></li>
    </ul>
    <div class="nav-actions">
      <a class="btn btn-ghost btn-sm" href="#start">Sign in</a>
      <a class="btn btn-primary btn-sm" href="#start">Get a bench <span aria-hidden="true">→</span></a>
    </div>
  </header>
</div>

<main id="top">
  <section class="hero" data-section="hero">
    <div class="hero-copy">
      <p class="pill"><span class="lamp on" aria-hidden="true"></span>Eval bench for AI answers</p>
      <h1>
        <span class="row">Measure <span class="gold">every answer</span></span>
        <span class="row">before it ships.</span>
      </h1>
      <p class="lede">Calibre reads what your model wrote, checks every claim against the sources it was given, and <em>marks it up like an editor</em>. Then it gives you one number you can put a release gate on.</p>
      <div class="ctas">
        <a class="btn btn-primary btn-lg" href="#start">Run your first bench <span aria-hidden="true">→</span></a>
        <a class="btn btn-ghost btn-lg" href="#how"><svg width="14" height="16" viewBox="0 0 14 16" aria-hidden="true"><path d="M1 1.5v13l12-6.5z" fill="currentColor" /></svg>See how it grades</a>
      </div>
      <ul class="trust">
        <li><svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round" aria-hidden="true"><path d="M12 2.8l8 4.4v9.6l-8 4.4-8-4.4V7.2z" /><path d="M4 7.2l8 4.4 8-4.4M12 11.6v9.6" /></svg>Works with any model</li>
        <li><svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round" aria-hidden="true"><path d="M13.5 2.5L5 13.5h6l-1 8 8.5-11h-6z" /></svg>Runs in your VPC</li>
        <li><svg width="26" height="26" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linejoin="round" aria-hidden="true"><rect x="4.5" y="10.5" width="15" height="10.5" rx="2" /><path d="M8 10.5V7.5a4 4 0 0 1 8 0v3" /><circle cx="12" cy="15.5" r="1.3" fill="currentColor" /></svg>Gates CI in one line</li>
      </ul>
    </div>

    <div class="src s3" aria-hidden="true"><svg width="38" height="44" viewBox="0 0 38 44" fill="none" stroke="currentColor" stroke-width="2"><path d="M6 2h18l10 10v28a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2z" /><path d="M24 2v10h10" /><text x="8" y="31" fill="currentColor" stroke="none" font-family="Archivo, sans-serif" font-weight="800" font-size="11">PDF</text></svg><span class="lines"><i></i><i></i><i></i><i></i></span><span class="label">Source 3</span></div>
    <div class="src s1" aria-hidden="true"><svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.4"><circle cx="12" cy="12" r="9.5" /><path d="M2.5 12h19M12 2.5c2.8 2.7 4 6 4 9.5s-1.2 6.8-4 9.5c-2.8-2.7-4-6-4-9.5s1.2-6.8 4-9.5z" /></svg><span class="lines"><i></i><i></i><i></i><i></i></span><span class="label">Source 1</span></div>
    <div class="src s2" aria-hidden="true"><svg width="36" height="40" viewBox="0 0 24 26" fill="none" stroke="currentColor" stroke-width="1.6"><ellipse cx="12" cy="5" rx="9" ry="3.5" /><path d="M3 5v16c0 1.9 4 3.5 9 3.5s9-1.6 9-3.5V5M3 10.5c0 1.9 4 3.5 9 3.5s9-1.6 9-3.5M3 16c0 1.9 4 3.5 9 3.5s9-1.6 9-3.5" /></svg><span class="lines"><i></i><i></i><i></i><i></i></span><span class="label">Source 2</span></div>
    <div class="src s4" aria-hidden="true"><svg width="36" height="42" viewBox="0 0 24 28" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M4 1.5h11l6 6v18a1.5 1.5 0 0 1-1.5 1.5h-15A1.5 1.5 0 0 1 3 25.5v-22A1.5 1.5 0 0 1 4 1.5z" /><path d="M15 1.5v6h6" /><path d="M8 19.5c2.5-1 4.5-4 5-8 .5 4 2.5 6.5 4 7-2 0-5.5.5-9 1z" /></svg><span class="lines"><i></i><i></i><i></i><i></i></span><span class="label">Source 4</span></div>
    <div class="stage">
      <div class="planet" aria-hidden="true"></div>
      <span class="flare f1" aria-hidden="true"></span>
      <span class="flare f2" aria-hidden="true"></span>
      <span class="spark" style="left:16%;top:6%;--d:-1s" aria-hidden="true"></span>
      <span class="spark" style="left:21%;top:32%;--d:-2.2s" aria-hidden="true"></span>
      <span class="spark" style="left:9%;top:58%;--d:-0.4s" aria-hidden="true"></span>
      <span class="spark" style="left:80%;top:10%;--d:-1.6s" aria-hidden="true"></span>
      <span class="spark" style="left:86%;top:44%;--d:-3s" aria-hidden="true"></span>
      <span class="spark" style="left:74%;top:28%;--d:-0.8s" aria-hidden="true"></span>

      <svg class="terrain" viewBox="0 0 1600 420" preserveAspectRatio="none" aria-hidden="true">
        <defs><linearGradient id="fadeT" x1="0" y1="0" x2="0" y2="1"><stop offset="0.45" stop-color="#08090b" stop-opacity="0" /><stop offset="1" stop-color="#08090b" /></linearGradient><linearGradient id="rockB" x1="0" y1="0" x2="0" y2="1"><stop offset="0.25" stop-color="#2b1810" /><stop offset="0.55" stop-color="#110c0a" /><stop offset="1" stop-color="#09090a" /></linearGradient><filter id="rim" x="-5%" y="-50%" width="110%" height="200%"><feGaussianBlur stdDeviation="2.5" result="b" /><feMerge><feMergeNode in="b" /><feMergeNode in="SourceGraphic" /></feMerge></filter></defs>
        <path fill="url(#rockB)" d="M0 420V150C40 140 70 120 110 135C150 150 160 118 205 128C250 140 262 175 300 180C340 186 352 160 392 178C432 196 440 232 480 240C520 248 548 236 590 262C630 288 660 296 720 300C780 304 820 296 880 300C940 304 970 290 1010 266C1050 242 1080 250 1120 236C1160 222 1170 190 1210 182C1250 174 1262 196 1300 186C1338 176 1350 140 1395 132C1440 124 1452 150 1495 140C1538 130 1560 112 1600 120V420Z" />
        <path fill="none" stroke="rgba(255,176,100,0.7)" stroke-width="1.6" filter="url(#rim)" d="M0 150C40 140 70 120 110 135C150 150 160 118 205 128C250 140 262 175 300 180C340 186 352 160 392 178C432 196 440 232 480 240M1120 236C1160 222 1170 190 1210 182C1250 174 1262 196 1300 186C1338 176 1350 140 1395 132C1440 124 1452 150 1495 140C1538 130 1560 112 1600 120" />
        <rect width="1600" height="420" fill="url(#fadeT)" />
      </svg>


      <div class="bench-wrap">
        <div class="bench">
          <div class="bench-top">
            <span class="label">// Run 0418<span class="long"> · support-bot</span></span>
            <div class="status" id="status" data-state="busy">
              <span class="lamp on" aria-hidden="true"></span><span id="statusText">Scanning</span>
              <button class="icon-btn" id="run" type="button" aria-label="Run the bench again" title="Run again"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M20 12a8 8 0 1 1-2.3-5.6" /><path d="M20 4v5h-5" /></svg></button>
            </div>
          </div>

          <div class="bench-grid">
            <div class="card answer" id="answer">
              <div class="scanline" id="scan" aria-hidden="true"></div>
              <div class="answer-head">
                <b><svg width="15" height="15" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round" aria-hidden="true"><path d="M4 5h16v11H9l-5 4z" /></svg>Model answer</b>
                <span class="meta">4 sources · 5 claims</span>
              </div>
              <p id="sheet">
                <mark class="hl claim" tabindex="0" data-v="green" data-src="Refund policy §2: “Refunds are issued to the original payment method within 5 business days.”">Your refund goes back to the card you paid with</mark>
                and
                <mark class="hl claim" tabindex="0" data-v="yellow" data-src="Refund policy §2 says 5 business days; the answer rounds it to “about a week”. Reworded, still right.">usually lands within about a week.</mark>
                <mark class="hl claim" tabindex="0" data-v="orange" data-src="Shipping FAQ: free returns apply to orders over $50. The answer drops the condition.">Returns are always free,</mark>
                and
                <mark class="hl claim" tabindex="0" data-v="green" data-src="Account help §4: “Open Orders, choose the item and select Start a return.”">you can start one from the Orders page.</mark>
                <mark class="hl claim" tabindex="0" data-v="red" data-src="No source mentions a store credit bonus. Nothing in the context supports this.">We'll also add a 10% store credit bonus.</mark>
              </p>
            </div>

            <div class="card gauge">
              <svg viewBox="0 0 170 128" aria-hidden="true">
                <defs>
                  <linearGradient id="arc" x1="0" x2="1">
                    <stop offset="0" stop-color="#ff3b30" /><stop offset="0.35" stop-color="#ff8a1f" /><stop offset="0.62" stop-color="#ffd23f" /><stop offset="1" stop-color="#2fd36b" />
                  </linearGradient>
                  <filter id="glow" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="3" result="b" /><feMerge><feMergeNode in="b" /><feMergeNode in="SourceGraphic" /></feMerge></filter>
                </defs>
                <path d="M 24.1 120.2 A 70 70 0 1 1 145.9 120.2" fill="none" stroke="#1b1d22" stroke-width="12" stroke-linecap="round" />
                <path d="M 24.1 120.2 A 70 70 0 1 1 145.9 120.2" fill="none" stroke="url(#arc)" stroke-width="11" stroke-linecap="round" filter="url(#glow)" />
                <g id="ticks" stroke="#3e434b" stroke-width="1.3"></g>
                <g class="needle" id="needle">
                  <path d="M85 85 L83.4 82 L85 40 L86.6 82 Z" fill="#ffb562" />
                  <circle cx="85" cy="85" r="4.5" fill="#2a2d33" stroke="#ffb562" stroke-width="1.5" />
                </g>
              </svg>
              <div class="score"><span id="score">0</span><small>/100</small></div>
              <div class="label">Grounding</div>
              <span class="gate" id="gate">Gate ≥ 80 · <b>waiting</b></span>
            </div>
          </div>

          <div class="chips" aria-label="Verdict counts">
            <div class="chip"><span class="lamp l-green" data-lamp="green"></span>Grounded<b data-count="green">0</b></div>
            <div class="chip"><span class="lamp l-yellow" data-lamp="yellow"></span>Reworded<b data-count="yellow">0</b></div>
            <div class="chip"><span class="lamp l-orange" data-lamp="orange"></span>Stretched<b data-count="orange">0</b></div>
            <div class="chip"><span class="lamp l-red" data-lamp="red"></span>Unsupported<b data-count="red">0</b></div>
          </div>

          <div class="source" id="sourceBar">
            <span class="tile" aria-hidden="true"><svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor"><path d="M12 1.5c.6 5.6 4.9 9.9 10.5 10.5-5.6.6-9.9 4.9-10.5 10.5-.6-5.6-4.9-9.9-10.5-10.5C7.1 11.4 11.4 7.1 12 1.5z" /></svg></span>
            <div class="body" id="source" aria-live="polite"><b>Source check</b>Select any marked claim to see what it was checked against.</div>
            <button class="icon-btn" id="next" type="button" aria-label="Show the next claim's source" title="Next claim"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M9 5l7 7-7 7" /></svg></button>
          </div>
        </div>
      </div>

      <svg class="terrain front" viewBox="0 0 1600 300" preserveAspectRatio="none" aria-hidden="true">
        <defs><linearGradient id="fadeF" x1="0" y1="0" x2="0" y2="1"><stop offset="0.4" stop-color="#08090b" stop-opacity="0" /><stop offset="0.95" stop-color="#08090b" /></linearGradient><linearGradient id="rockF" x1="0" y1="0" x2="0" y2="1"><stop offset="0.1" stop-color="#1e120c" /><stop offset="0.45" stop-color="#0d0b0a" /><stop offset="1" stop-color="#08090b" /></linearGradient></defs>
        <path fill="url(#rockF)" d="M0 300V96C50 84 80 110 130 100C180 90 200 60 250 72C300 84 320 128 360 146C400 164 420 200 470 214C520 228 540 260 600 300H1000C1060 262 1090 230 1140 214C1190 198 1210 166 1250 148C1290 130 1320 86 1370 74C1420 62 1440 94 1490 92C1540 90 1570 70 1600 78V300Z" />
        <path fill="none" stroke="rgba(255,176,100,0.75)" stroke-width="1.6" filter="url(#rim)" d="M0 96C50 84 80 110 130 100C180 90 200 60 250 72C300 84 320 128 360 146M1250 148C1290 130 1320 86 1370 74C1420 62 1440 94 1490 92C1540 90 1570 70 1600 78" />
        <rect width="1600" height="300" fill="url(#fadeF)" />
      </svg>
      <div class="hero-fade" aria-hidden="true"></div>
    </div>

    <div class="logos">
      <p class="label">Trusted by teams shipping AI products</p>
      <ul>
        <li><svg width="22" height="20" viewBox="0 0 22 20" aria-hidden="true"><path d="M11 0l11 20H0z" fill="currentColor" /></svg>Northwind</li>
        <li><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><circle cx="12" cy="12" r="9" /><circle cx="12" cy="12" r="4" /></svg>Halcyon</li>
        <li>Meridian</li>
        <li>parallax</li>
        <li><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><rect x="3" y="3" width="18" height="18" rx="3" /><path d="M8 16V8l8 8V8" /></svg>Lumen</li>
        <li>orbital <svg width="18" height="16" viewBox="0 0 18 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><path d="M2 14C6 8 11 4 16 2M10 2h6v6" /></svg></li>
        <li><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" aria-hidden="true"><path d="M12 2v20M2 12h20M5 5l14 14M19 5L5 19" /></svg>quanta</li>
        <li><svg width="24" height="24" viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="12" r="10" fill="currentColor" opacity="0.85" /><path d="M5 15l10-10M8 18l10-10" stroke="#08090b" stroke-width="2" /></svg>Stackwise</li>
      </ul>
    </div>
  </section>

  <section class="sec" id="verdicts" data-section="verdicts">
    <div class="sec-head reveal">
      <p class="pill"><span class="lamp on" aria-hidden="true"></span>01 · Verdicts</p>
      <h2>Four colours. <span class="gold">One verdict</span> per claim.</h2>
      <p>Every sentence is split into claims and every claim gets exactly one mark, so a reviewer reads a whole answer at a glance.</p>
    </div>
    <div class="verdicts vivid reveal">
      <article class="glass lift vcard" style="--tc: var(--v-green)">
        <div class="vtop"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4.5 12.5l4.5 4.5L19.5 6.5" /></svg></span><span class="weight">weight <b>1.00</b></span></div>
        <span class="tag"><span class="lamp l-green on"></span>Grounded</span>
        <h3>Said in the source</h3>
        <p>The claim matches a span in the context, word for word or nearly.</p>
        <div class="eg"><div><small>Example</small><p>Orders <mark class="hl v-green draw" data-mark>ship in 2 days</mark>.</p></div></div>
      </article>
      <article class="glass lift vcard" style="--tc: var(--v-yellow)">
        <div class="vtop"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 20h4L19 9l-4-4L4 16z" /><path d="M13.5 6.5l4 4" /></svg></span><span class="weight">weight <b>0.85</b></span></div>
        <span class="tag"><span class="lamp l-yellow on"></span>Reworded</span>
        <h3>Right, in other words</h3>
        <p>The meaning holds but the wording moved. Fine for users, flagged for auditors.</p>
        <div class="eg"><div><small>Example</small><p>Lands in <mark class="hl v-yellow draw" data-mark>about a week</mark>.</p></div></div>
      </article>
      <article class="glass lift vcard" style="--tc: var(--v-orange)">
        <div class="vtop"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 12h18M7 8l-4 4 4 4M17 8l4 4-4 4" /></svg></span><span class="weight">weight <b>0.35</b></span></div>
        <span class="tag"><span class="lamp l-orange on"></span>Stretched</span>
        <h3>More than it said</h3>
        <p>A condition was dropped or a number rounded up. The quiet failure that ships.</p>
        <div class="eg"><div><small>Example</small><p>Returns are <mark class="hl v-orange draw" data-mark>always free</mark>.</p></div></div>
      </article>
      <article class="glass lift vcard" style="--tc: var(--v-red)">
        <div class="vtop"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><circle cx="12" cy="12" r="8.5" /><path d="M6 18L18 6" /></svg></span><span class="weight">weight <b>0.00</b></span></div>
        <span class="tag"><span class="lamp l-red on"></span>Unsupported</span>
        <h3>Nowhere in the context</h3>
        <p>Nothing it was given backs this up. Blocked at the gate before a customer reads it.</p>
        <div class="eg"><div><small>Example</small><p>Plus a <mark class="hl v-red draw" data-mark>10% store credit</mark>.</p></div></div>
      </article>
    </div>
    <p class="scoring reveal"><span>Score = mean of weights</span><code>(1 + 0.85 + 0.35 + 1 + 0) ÷ 5 = <i>64</i></code></p>
  </section>

  <section class="sec" id="how" data-section="how-it-works">
    <div class="sec-head reveal">
      <p class="pill"><span class="lamp on" aria-hidden="true"></span>02 · How it grades</p>
      <h2>Bolt it on. <span class="gold">Read the needle.</span></h2>
      <p>Calibre sits between your model and your users. Three stages, one score, and a gate your CI can trust.</p>
    </div>
    <div class="steps reveal">
      <article class="glass lift step">
        <div class="shead"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 6h16M4 12h10M4 18h13" /><path d="M18 10l3 2-3 2" /></svg></span><span class="big" aria-hidden="true">01</span></div>
        <span class="num">Stage one</span>
        <h3>Split</h3>
        <p>Each answer is cut into atomic claims: one fact, one number, one promise each.</p>
        <div class="term"><div><header><i></i><i></i><i></i><span>terminal</span></header><pre><span class="p">$</span> calibre split answer.md
→ 5 claims</pre></div></div>
      </article>
      <article class="glass lift step">
        <div class="shead"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="10.5" cy="10.5" r="6.5" /><path d="M15.5 15.5L21 21M7.5 10.5l2 2 4-4" /></svg></span><span class="big" aria-hidden="true">02</span></div>
        <span class="num">Stage two</span>
        <h3>Check</h3>
        <p>Every claim is matched against the exact spans it was given and marked in its verdict colour.</p>
        <div class="term"><div><header><i></i><i></i><i></i><span>terminal</span></header><pre><span class="p">$</span> calibre check --sources ctx/
→ <span class="ok">2 grounded</span> · <span class="y">1 reworded</span>
  <span class="o">1 stretched</span> · <span class="r">1 unsupported</span></pre></div></div>
      </article>
      <article class="glass lift step">
        <div class="shead"><span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 3l7.5 3v5.5c0 4.5-3.2 8-7.5 9.5-4.3-1.5-7.5-5-7.5-9.5V6z" /><path d="M9 12l2 2 4-4" /></svg></span><span class="big" aria-hidden="true">03</span></div>
        <span class="num">Stage three</span>
        <h3>Gate</h3>
        <p>The weighted score drives the needle. Below your line, the release stops with the marked-up answer attached.</p>
        <div class="term"><div><header><i></i><i></i><i></i><span>terminal</span></header><pre><span class="p">$</span> calibre gate --min 80
→ 64 · <span class="r">blocked</span></pre></div></div>
      </article>
    </div>
  </section>

  <section class="sec" id="numbers" data-section="stats">
    <div class="sec-head reveal">
      <p class="pill"><span class="lamp on" aria-hidden="true"></span>03 · This month on the bench</p>
      <h2>The numbers, <span class="gold">measured.</span></h2>
    </div>
    <div class="glass stats-panel reveal">
      <div class="stats">
        <div class="stat"><span class="k"><span class="lamp l-green on"></span>Volume</span><div class="n"><span data-roll="48">0</span>M</div><p>claims checked across every bench</p></div>
        <div class="stat"><span class="k"><span class="lamp l-red on"></span>Risk</span><div class="n hot">1 in 9</div><p>answers carried a claim nothing backed up</p></div>
        <div class="stat"><span class="k"><span class="lamp l-yellow on"></span>Latency</span><div class="n"><span data-roll="210">0</span>ms</div><p>median time added per answer</p></div>
        <div class="stat"><span class="k"><span class="lamp on"></span>Integration</span><div class="n">Zero</div><p>changes to the model you already run</p></div>
      </div>
    </div>
  </section>

  <section class="sec" id="faq" data-section="faq">
    <div class="faq-layout">
      <div class="faq-side reveal">
        <div class="sec-head left">
          <p class="pill"><span class="lamp on" aria-hidden="true"></span>04 · Questions</p>
          <h2>Before you <span class="gold">bolt it on.</span></h2>
          <p>Everything teams ask before they put a needle on production answers.</p>
        </div>
        <div class="glass contact">
          <span class="itile"><svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linejoin="round" aria-hidden="true"><path d="M4 5h16v11H9l-5 4z" /></svg></span>
          <div><b>Still unsure?</b><p>Send us the answer that worries you most and we'll run it on a bench.</p><a href="#start">Talk to an engineer <span aria-hidden="true">→</span></a></div>
        </div>
      </div>
      <div class="qa-list reveal">
        <details class="glass qa" open><summary>Does it need my model's weights?<span class="plus" aria-hidden="true"></span></summary><p>No. Calibre only reads the answer and the context it was given, so it works with any hosted or open model.</p></details>
        <details class="glass qa"><summary>What counts as a source?<span class="plus" aria-hidden="true"></span></summary><p>Whatever you passed in: retrieved documents, tool results, a policy page. A claim is grounded only if one of those spans supports it.</p></details>
        <details class="glass qa"><summary>Where does it run?<span class="plus" aria-hidden="true"></span></summary><p>In your own cloud. Answers and sources never leave your network, and the bench keeps no copies.</p></details>
        <details class="glass qa"><summary>Can I tune the gate?<span class="plus" aria-hidden="true"></span></summary><p>Yes. Set the minimum score, weight each verdict, and choose whether a single unsupported claim blocks on its own.</p></details>
        <details class="glass qa"><summary>How fast is it?<span class="plus" aria-hidden="true"></span></summary><p>A median of 210 ms per answer, so it can sit inline in production or run as a batch job in CI.</p></details>
      </div>
    </div>
  </section>

  <section class="sec" id="start" data-section="cta">
    <div class="glass finale reveal">
      <div class="planet" aria-hidden="true"></div>
      <div class="glowfloor" aria-hidden="true"></div>
      <span class="pill"><span class="lamp on" aria-hidden="true"></span>05 · Your bench</span>
      <h2><span class="row">Put a needle on</span><span class="row gold">every answer.</span></h2>
      <p class="finale-lede">Point Calibre at one answer and its sources. You'll have a score and a marked-up page in under a minute.</p>
      <form class="cta-form" id="ctaForm">
        <label for="email" class="sr-only">Work email</label>
        <input id="email" type="email" required placeholder="you@company.com" autocomplete="email" />
        <button class="btn btn-primary" type="submit">Get a bench <span aria-hidden="true">→</span></button>
      </form>
      <p class="cta-msg" id="ctaMsg" aria-live="polite"></p>
      <ul class="cta-notes">
        <li><svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 8.5l3.2 3L13 4.5" /></svg>Free for the first 100,000 claims</li>
        <li><svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 8.5l3.2 3L13 4.5" /></svg>No card required</li>
        <li><svg width="14" height="14" viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 8.5l3.2 3L13 4.5" /></svg>Runs in your VPC</li>
      </ul>
    </div>
  </section>
</main>

<footer class="site-footer" data-section="footer">
  <div class="f-top">
    <div class="f-brand">
      <a class="brand" href="#top" aria-label="Calibre home">
        <svg width="40" height="26" viewBox="0 0 40 26" fill="none" aria-hidden="true"><path d="M4 23a16 16 0 0 1 32 0" stroke="currentColor" stroke-width="5" stroke-linecap="round" /><path d="M20 22l7.5-9" stroke="currentColor" stroke-width="3.4" stroke-linecap="round" /><circle cx="20" cy="22" r="2.6" fill="currentColor" /></svg>
        Calibre
      </a>
      <p>The eval bench that measures every AI answer before it ships.</p>
      <span class="f-status"><span class="lamp l-green on" aria-hidden="true"></span>All benches operational</span>
    </div>
    <div class="f-col"><h4>Product</h4><ul><li><a href="#verdicts">Verdicts</a></li><li><a href="#how">How it works</a></li><li><a href="#numbers">Numbers</a></li><li><a href="#start">Get a bench</a></li></ul></div>
    <div class="f-col"><h4>Resources</h4><ul><li><a href="#faq">FAQ</a></li><li><a href="#how">CLI reference</a></li><li><a href="#how">CI gate guide</a></li></ul></div>
    <div class="f-col"><h4>Company</h4><ul><li><a href="#faq">Security</a></li><li><a href="#start">Contact</a></li><li><a href="#top">Changelog</a></li></ul></div>
  </div>
  <div class="f-word" aria-hidden="true">Calibre</div>
  <div class="f-bottom">
    <span>© 2026 Calibre Instruments · a fictional product; every name and number here is invented.</span>
    <span>Built to measure.</span>
  </div>
</footer>

<script>
(() => {
  "use strict";
  const reduced = matchMedia("(prefers-reduced-motion: reduce)").matches;
  const $ = (s, r = document) => r.querySelector(s);
  const $$ = (s, r = document) => [...r.querySelectorAll(s)];

  /* gauge ticks, inside the arc */
  const ticks = $("#ticks");
  for (let i = 0; i <= 20; i++) {
    const a = (-120 + i * 12) * Math.PI / 180, big = i % 5 === 0;
    const r1 = big ? 50 : 54, r2 = 58;
    const l = document.createElementNS("http://www.w3.org/2000/svg", "line");
    l.setAttribute("x1", 85 + Math.sin(a) * r1); l.setAttribute("y1", 85 - Math.cos(a) * r1);
    l.setAttribute("x2", 85 + Math.sin(a) * r2); l.setAttribute("y2", 85 - Math.cos(a) * r2);
    if (big) l.setAttribute("stroke", "#7d838d");
    ticks.appendChild(l);
  }

  /* the needle: a damped spring toward the running score */
  const needle = $("#needle"), scoreEl = $("#score");
  let pos = 0, vel = 0, target = 0, shown = 0, raf = 0, last = 0;
  const K = 120, D = 14;
  function frame(now) {
    const dt = Math.min(0.033, (now - (last || now)) / 1000); last = now;
    vel += (K * (target - pos) - D * vel) * dt;
    pos += vel * dt;
    needle.style.setProperty("--a", Math.max(-0.02, Math.min(1.02, pos)).toFixed(4));
    shown += (target * 100 - shown) * Math.min(1, dt * 7);
    scoreEl.textContent = Math.round(shown);
    if (Math.abs(target - pos) < 0.0005 && Math.abs(vel) < 0.0005 && Math.abs(target * 100 - shown) < 0.3) {
      pos = target; scoreEl.textContent = Math.round(target * 100); raf = 0; last = 0; return;
    }
    raf = requestAnimationFrame(frame);
  }
  function setTarget(v) {
    target = v;
    if (reduced) { pos = shown = v; needle.style.setProperty("--a", v); scoreEl.textContent = Math.round(v * 100); return; }
    if (!raf) raf = requestAnimationFrame(frame);
  }

  /* the bench run */
  const WEIGHT = { green: 1, yellow: 0.85, orange: 0.35, red: 0 };
  const NAMES = { green: "Grounded", yellow: "Reworded", orange: "Stretched", red: "Unsupported" };
  const claims = $$("#sheet .claim");
  claims.forEach((c) => {
    const words = c.textContent.trim().split(/\s+/);
    c.textContent = "";
    words.forEach((w, i) => {
      const s = document.createElement("span");
      s.className = "w"; s.style.setProperty("--i", i); s.textContent = w;
      c.append(s);
      if (i < words.length - 1) c.append(" ");
    });
  });
  const answer = $("#answer"), scan = $("#scan"), source = $("#source"), runBtn = $("#run"), nextBtn = $("#next"), gate = $("#gate");
  const status = $("#status"), statusText = $("#statusText");
  const counts = { green: 0, yellow: 0, orange: 0, red: 0 };
  const DEFAULT_SRC = "<b>Source check</b>Select any marked claim to see what it was checked against.";
  let running = false, current = -1;

  function setGate(state, text) { gate.dataset.state = state; gate.innerHTML = `Gate ≥ 80 · <b>${text}</b>`; }
  function setStatus(state, text) { status.dataset.state = state; statusText.textContent = text; }
  function reset() {
    Object.keys(counts).forEach((k) => (counts[k] = 0));
    $$("[data-count]").forEach((b) => (b.textContent = "0"));
    $$("[data-lamp]").forEach((l) => l.classList.remove("on"));
    claims.forEach((c) => { c.classList.remove("v-green", "v-yellow", "v-orange", "v-red", "drawn"); c.classList.add("draw"); });
    source.innerHTML = DEFAULT_SRC; current = -1;
    setGate("", "scanning");
    setStatus("busy", "Scanning");
    setTarget(0);
  }
  function mark(c, i) {
    const v = c.dataset.v;
    c.classList.add("v-" + v);
    requestAnimationFrame(() => c.classList.add("drawn"));
    counts[v]++;
    $(`[data-count="${v}"]`).textContent = counts[v];
    $(`[data-lamp="${v}"]`).classList.add("on");
    const sum = claims.slice(0, i + 1).reduce((s, x) => s + WEIGHT[x.dataset.v], 0);
    setTarget(sum / claims.length);
  }
  function finish(t0) {
    const score = Math.round(claims.reduce((s, x) => s + WEIGHT[x.dataset.v], 0) / claims.length * 100);
    score >= 80 ? setGate("pass", "passed") : setGate("block", "blocked");
    setStatus("done", `Completed  ${((performance.now() - t0) / 1000).toFixed(1)}s`);
  }
  const wait = (ms) => new Promise((res) => setTimeout(res, ms));
  async function run() {
    if (running) return;
    running = true; runBtn.disabled = true;
    const t0 = performance.now();
    reset();
    if (reduced) { claims.forEach(mark); finish(t0); running = false; runBtn.disabled = false; return; }
    answer.classList.add("scanning");
    for (let i = 0; i < claims.length; i++) {
      const c = claims[i];
      scan.style.top = (c.offsetTop + c.offsetHeight / 2) + "px";
      await wait(520);
      mark(c, i);
      await wait(380);
    }
    answer.classList.remove("scanning");
    finish(t0);
    running = false; runBtn.disabled = false;
  }
  runBtn.addEventListener("click", run);

  function show(i) {
    const c = claims[i];
    if (!c || !c.classList.contains("drawn")) return;
    current = i;
    const v = c.dataset.v;
    source.style.setProperty("--c", `var(--v-${v})`);
    source.innerHTML = `<b><span class="lamp on" aria-hidden="true"></span>${NAMES[v]}</b>${c.dataset.src}`;
  }
  claims.forEach((c, i) => {
    c.addEventListener("click", () => show(i));
    c.addEventListener("keydown", (e) => { if (e.key === "Enter" || e.key === " ") { e.preventDefault(); show(i); } });
  });
  nextBtn.addEventListener("click", () => show((current + 1) % claims.length));

  /* marks and counters draw in on view */
  const io = new IntersectionObserver((entries) => {
    for (const e of entries) {
      if (!e.isIntersecting) continue;
      const el = e.target; io.unobserve(el);
      if (el.matches("[data-mark]")) setTimeout(() => el.classList.add("drawn"), 150);
      if (el.matches("[data-roll]")) roll(el);
    }
  }, { threshold: 0.4 });
  $$("[data-mark], [data-roll]").forEach((el) => io.observe(el));

  function roll(el) {
    const to = +el.dataset.roll;
    if (reduced) { el.textContent = to; return; }
    const t0 = performance.now(), dur = 1300;
    const step = (now) => {
      const p = Math.min(1, (now - t0) / dur), e = 1 - Math.pow(1 - p, 3);
      el.textContent = Math.round(to * e);
      if (p < 1) requestAnimationFrame(step);
    };
    requestAnimationFrame(step);
  }

  /* reveal on scroll */
  const rio = new IntersectionObserver((entries) => {
    for (const e of entries) if (e.isIntersecting) { e.target.classList.add("in"); rio.unobserve(e.target); }
  }, { threshold: 0.12, rootMargin: "0px 0px -6% 0px" });
  $$(".reveal").forEach((el) => (reduced ? el.classList.add("in") : rio.observe(el)));

  /* sign-up */
  $("#ctaForm").addEventListener("submit", (e) => {
    e.preventDefault();
    $("#ctaMsg").textContent = "Thanks. Your bench is being machined; we'll email you the keys.";
  });

  reset();
  if (reduced) run(); else setTimeout(run, 700);
})();
</script>
</body>
</html>
```

