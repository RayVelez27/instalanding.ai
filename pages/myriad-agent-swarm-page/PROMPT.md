INSTALANDING.AI · Myriad Agent Swarm Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Myriad Agent Swarm Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/myriad-agent-swarm-page

myriad-agent-swarm.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Myriad Agent Swarm Page
  slug     myriad-agent-swarm-page
  prompt   https://instalanding.ai/p/myriad-agent-swarm-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/myriad-agent-swarm-page
  license  MIT. Fictional product; every agent, number and claim is invented. Replace them before shipping.

  MAP
  tokens    :root at the top of <style>: five registered colour properties (@property --c1 --c2 --c3 --bg1 --bg2) that
            each agent's theme swaps and that transition over 1.1s, so the whole page recolours smoothly; fonts
            (--display Unbounded, --body Space Grotesk, --mono JetBrains Mono) and one ease.
  sections  nav, hero, status (a one-screen select screen: the hero holds the swarm, the agent copy and the agent rail)
  scripts   one inline script, no libraries: the AGENTS data (name, role, topology, tagline, copy, three stats, a
            theme and four abilities each) renders the copy, the QECX ability tiles and the hexagon agent rail; a
            Canvas 2D particle swarm (640 points, 380 on phones) springs between five 3D formations (icosahedron,
            sphere with rings, trefoil knot, double helix, ripple rings), drawn with additive glow sprites, two
            nearest-neighbour links per point, message pulses hopping along links and a pointer that repels points and
            casts beams; a katakana glyph matrix masked into the orbit; name scramble, stat count-ups, a 9s autoplay
            with a progress bar, wheel / arrow keys / swipe to change agent, a custom cursor and a live online count.
  assets    none: the logo, glyphs and icons are inline SVG; fonts from Google Fonts

  ADAPTING
  - Add or edit agents in AGENTS; each needs a theme and four abilities (the fourth is the ULT), and a glyph in GLYPHS
    at the same index. Each agent's formation is SHAPES[index]: add a shape function per new agent, or reuse one.
  - The colour transition only works because --c1..--bg2 are registered with @property; keep the registrations.
  - Nearest neighbours are computed once per shape at load (N^2); keep N in the hundreds, not thousands.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Myriad — Agent Swarm</title>
<meta name="description" content="Myriad OS: five specialist AI agents, one swarm. Pick an agent and watch the swarm reform around it.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Unbounded:wght@300;500;700;800&family=Space+Grotesk:wght@400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
@property --c1 { syntax: '<color>'; inherits: true; initial-value: #14d27c; }
@property --c2 { syntax: '<color>'; inherits: true; initial-value: #8ff5c4; }
@property --c3 { syntax: '<color>'; inherits: true; initial-value: #e3fff1; }
@property --bg1 { syntax: '<color>'; inherits: true; initial-value: #03100a; }
@property --bg2 { syntax: '<color>'; inherits: true; initial-value: #062c1b; }

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
:root {
  --c1: #14d27c; --c2: #8ff5c4; --c3: #e3fff1; --bg1: #03100a; --bg2: #062c1b;
  --display: 'Unbounded', system-ui, sans-serif;
  --body: 'Space Grotesk', system-ui, sans-serif;
  --mono: 'JetBrains Mono', ui-monospace, monospace;
  --ease: cubic-bezier(.2,.8,.2,1);
  transition: --c1 1.1s var(--ease), --c2 1.1s var(--ease), --c3 1.1s var(--ease), --bg1 1.1s var(--ease), --bg2 1.1s var(--ease);
}
html, body { height: 100%; }
body {
  font-family: var(--body); font-size: 15px; line-height: 1.6;
  background: var(--bg1); color: color-mix(in srgb, var(--c3) 72%, transparent);
  overflow-x: hidden; -webkit-font-smoothing: antialiased;
}
a { color: inherit; text-decoration: none; }
button { font: inherit; color: inherit; background: none; border: 0; cursor: pointer; }
svg { display: block; }
::selection { background: var(--c1); color: var(--bg1); }

/* ---------- Cursor ---------- */
.cursor, .cursor-dot { position: fixed; top: 0; left: 0; pointer-events: none; z-index: 1000; border-radius: 50%; }
.cursor { width: 38px; height: 38px; margin: -19px 0 0 -19px; border: 1.5px solid var(--c1);
  transition: transform .35s var(--ease), background .35s, opacity .3s; }
.cursor.grow { transform: scale(1.9); background: color-mix(in srgb, var(--c1) 14%, transparent); border-color: var(--c2); }
.cursor-dot { width: 4px; height: 4px; margin: -2px 0 0 -2px; background: var(--c3); }
@media (pointer: coarse) { .cursor, .cursor-dot { display: none; } }

/* ---------- Header ---------- */
.site-header { position: fixed; inset: 0 0 auto; z-index: 50; display: flex; align-items: center; justify-content: space-between;
  padding: 28px 40px; }
.brand { display: flex; align-items: center; gap: 12px; }
.brand svg { width: 42px; height: 42px; filter: drop-shadow(0 0 12px color-mix(in srgb, var(--c1) 60%, transparent)); }
.brand-word { font-family: var(--display); font-weight: 700; font-size: 17px; letter-spacing: .32em; color: var(--c3); }
.brand-word sup { font-family: var(--mono); font-size: 9px; letter-spacing: .1em; color: var(--c1); margin-left: 4px; vertical-align: super; }
.launch { display: flex; align-items: center; gap: 12px; font-family: var(--mono); font-size: 11px; letter-spacing: .24em; text-transform: uppercase;
  color: var(--c3); padding: 12px 18px; border: 1px solid color-mix(in srgb, var(--c1) 45%, transparent);
  background: color-mix(in srgb, var(--c1) 8%, transparent); backdrop-filter: blur(8px); transition: .3s; }
.launch:hover { background: color-mix(in srgb, var(--c1) 22%, transparent); border-color: var(--c1); }
.launch svg { width: 22px; height: 10px; transition: transform .3s var(--ease); }
.launch:hover svg { transform: translateX(4px); }

/* ---------- Stage & background ---------- */
.stage { position: relative; height: 100vh; height: 100svh; min-height: 740px; overflow: hidden; isolation: isolate; }
.bg { position: absolute; inset: 0; z-index: -5;
  background:
    radial-gradient(60% 70% at 36% 56%, color-mix(in srgb, var(--c1) 26%, transparent), transparent 62%),
    radial-gradient(40% 45% at 88% 8%, color-mix(in srgb, var(--bg2) 90%, transparent), transparent 70%),
    radial-gradient(50% 50% at 8% 100%, color-mix(in srgb, var(--bg2) 70%, transparent), transparent 70%),
    linear-gradient(180deg, var(--bg1), color-mix(in srgb, var(--bg1) 70%, black)); }
/* Glyph matrix — contained inside the orbit ring as the swarm's "core" */
.matrix { position: absolute; z-index: -2; pointer-events: none; overflow: hidden; contain: strict; border-radius: 50%;
  display: grid; grid-template-columns: repeat(var(--cols), var(--cell)); grid-auto-rows: var(--cell);
  justify-content: center; align-content: center;
  font-family: var(--mono); font-size: calc(var(--cell) * .55); line-height: 1; user-select: none;
  opacity: .55;
  -webkit-mask-image: radial-gradient(circle closest-side, rgba(0,0,0,.12) 0%, rgba(0,0,0,.45) 38%, #000 66%, rgba(0,0,0,.6) 82%, transparent 96%);
  mask-image: radial-gradient(circle closest-side, rgba(0,0,0,.12) 0%, rgba(0,0,0,.45) 38%, #000 66%, rgba(0,0,0,.6) 82%, transparent 96%); }
.matrix > span { display: grid; place-items: center; color: color-mix(in srgb, var(--c1) 16%, transparent); }
.matrix > span:nth-child(11n) { color: color-mix(in srgb, var(--c2) 34%, transparent); animation: mx-pulse 2.9s ease-in-out infinite 1.1s; }
.matrix > span:nth-child(19n + 2) { animation: mx-pulse 3.5s ease-in-out infinite .2s; }
.matrix > span:nth-child(29n + 1) { animation: mx-pulse 4.1s ease-in-out infinite .7s; }
.matrix > span:nth-child(37n + 10) { animation: mx-pulse 5.3s ease-in-out infinite 1.5s; }
.matrix > span:nth-child(41n + 1) { animation: mx-pulse 3.9s ease-in-out infinite .4s; }
.matrix > span:nth-child(17n + 9) { animation: mx-pulse 2.8s ease-in-out infinite .9s; }
.matrix > span:nth-child(23n + 18) { animation: mx-pulse 4.3s ease-in-out infinite 1.3s; }
.matrix > span:nth-child(31n + 4) { animation: mx-pulse 5.6s ease-in-out infinite .1s; }
.matrix > span:nth-child(43n + 20) { animation: mx-pulse 3.6s ease-in-out infinite 1.8s; }
.matrix > span:nth-child(13n + 6) { animation: mx-pulse 3.2s ease-in-out infinite 1.2s; }
.matrix > span:nth-child(53n + 5) { animation: mx-pulse 4.9s ease-in-out infinite .5s; }
.matrix > span:nth-child(47n + 15) { animation: mx-pulse 5.9s ease-in-out infinite 1s; }
@keyframes mx-pulse {
  0%, 100% { color: color-mix(in srgb, var(--c1) 20%, transparent); text-shadow: none; }
  30% { color: color-mix(in srgb, var(--c2) 75%, transparent); text-shadow: 0 0 8px color-mix(in srgb, var(--c2) 70%, transparent); }
  50% { color: var(--c1); text-shadow: 0 0 10px var(--c1), 0 0 16px color-mix(in srgb, var(--c1) 60%, transparent); }
  70% { color: color-mix(in srgb, var(--c3) 85%, transparent); text-shadow: 0 0 10px color-mix(in srgb, var(--c3) 60%, transparent); }
}
.matrix > span.flick { animation: mx-flick .9s ease-out; }
@keyframes mx-flick { 0% { color: var(--c3); text-shadow: 0 0 12px var(--c1); } 100% { color: color-mix(in srgb, var(--c1) 20%, transparent); text-shadow: none; } }
#swarm { position: absolute; inset: 0; width: 100%; height: 100%; z-index: -1; pointer-events: none; }
.noise { position: absolute; inset: 0; z-index: 2; pointer-events: none; opacity: .09; mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>"); }
.vignette { position: absolute; inset: 0; z-index: 2; pointer-events: none;
  background: radial-gradient(120% 90% at 50% 50%, transparent 55%, rgba(0,0,0,.55) 100%); }

/* ---------- Layout ---------- */
.layout { position: relative; z-index: 5; height: 100%; display: grid;
  grid-template-columns: minmax(0, 1.12fr) minmax(0, .88fr) 150px;
  align-items: center; gap: 28px; padding: 112px 40px 88px; }


/* Visual / HUD */
.visual { position: relative; align-self: stretch; min-height: 320px; }
.orbit-wrap { position: absolute; left: 50%; top: 50%; width: min(96%, 74vh); aspect-ratio: 1; transform: translate(-50%, -50%); pointer-events: none; }
.orbit { position: absolute; inset: 0; width: 100%; height: 100%; fill: none; }
.orbit.o1 { stroke: color-mix(in srgb, var(--c1) 30%, transparent); stroke-dasharray: 2 7; animation: spin 80s linear infinite; }
.orbit.o3 { stroke: color-mix(in srgb, var(--c1) 45%, transparent); animation: spin 140s linear infinite; }
@keyframes spin { to { transform: rotate(360deg); } }
.hud { position: absolute; font-family: var(--mono); font-size: 10.5px; letter-spacing: .18em; text-transform: uppercase; }
.hud-k { color: color-mix(in srgb, var(--c2) 50%, transparent); }
.hud-v { color: var(--c3); }
.hud-br { right: 22px; bottom: 18px; display: grid; gap: 8px; text-align: right; }
.stat { display: flex; align-items: baseline; justify-content: flex-end; gap: 12px; }
.stat .hud-v { font-family: var(--display); font-weight: 500; font-size: 18px; letter-spacing: .02em; min-width: 92px; }
.stat .hud-v small { font-family: var(--mono); font-size: 10px; color: var(--c2); margin-left: 2px; }
.live { width: 7px; height: 7px; border-radius: 50%; background: var(--c1); box-shadow: 0 0 0 0 var(--c1); animation: ping 1.8s infinite; }
@keyframes ping { 0% { box-shadow: 0 0 0 0 color-mix(in srgb, var(--c1) 70%, transparent); } 100% { box-shadow: 0 0 0 10px transparent; } }

/* Content */
.content { position: relative; max-width: 560px; }
.r { opacity: 0; }
.content-inner.is-in .r { animation: rise .9s var(--ease) both; animation-delay: calc(var(--d) * 75ms); }
.content-inner.is-out .r { opacity: 0; transform: translateY(-10px); filter: blur(4px); transition: .3s ease; }
@keyframes rise { from { opacity: 0; transform: translateY(22px); filter: blur(6px); } to { opacity: 1; transform: none; filter: none; } }
.title { display: flex; align-items: stretch; gap: clamp(18px, 1.8vw, 28px); margin-bottom: 4px; }
.title-num { position: relative; flex: 0 0 auto; display: flex; flex-direction: column; justify-content: center;
  padding: 0; padding-right: clamp(18px, 1.8vw, 28px); font-size: clamp(52px, 6.6vw, 112px); }
.title-num::after { content: ""; position: absolute; right: 0; top: 8%; bottom: 8%; width: 1px;
  background: linear-gradient(180deg, transparent, var(--c1) 30%, var(--c2) 70%, transparent); }
.title-num::before { content: ""; position: absolute; right: -3px; top: 8%; width: 7px; height: 7px; border-radius: 50%;
  background: var(--c3); box-shadow: 0 0 10px var(--c1), 0 0 20px var(--c1); animation: tn-travel 4.5s ease-in-out infinite; }
@keyframes tn-travel { 0%, 100% { top: 10%; } 50% { top: calc(90% - 7px); } }
.tn-digits { position: relative; font-family: var(--display); font-weight: 300; font-size: .64em; line-height: .86; letter-spacing: -.02em;
  font-variant-numeric: tabular-nums; color: transparent; -webkit-text-stroke: 1px color-mix(in srgb, var(--c2) 85%, transparent);
  background: linear-gradient(180deg, var(--c3), var(--c1)); -webkit-background-clip: text; background-clip: text;
  background-size: 100% 200%; background-position: 0 100%; animation: tn-fill 1.4s var(--ease) .25s both;
  filter: drop-shadow(0 0 18px color-mix(in srgb, var(--c1) 55%, transparent)); }
@keyframes tn-fill { from { background-position: 0 -100%; } to { background-position: 0 100%; } }
.content-inner.is-out .tn-digits { animation: none; }
.name { font-family: var(--display); font-weight: 800; font-size: clamp(52px, 6.6vw, 112px); line-height: .95; letter-spacing: -.01em;
  margin: 0; align-self: center; background: linear-gradient(180deg, var(--c3) 10%, var(--c1) 92%);
  -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent;
  filter: drop-shadow(0 8px 40px color-mix(in srgb, var(--c1) 40%, transparent)); }
.tagline { font-family: var(--display); font-weight: 300; font-size: clamp(15px, 1.25vw, 19px); color: var(--c3); margin-bottom: 26px; }
.brief { position: relative; display: flex; gap: 18px; padding: 20px 22px; margin-bottom: 18px;
  border: 1px solid color-mix(in srgb, var(--c1) 45%, transparent);
  background: linear-gradient(180deg, color-mix(in srgb, var(--c1) 16%, transparent), color-mix(in srgb, var(--c1) 3%, transparent));
  backdrop-filter: blur(12px); -webkit-backdrop-filter: blur(12px);
  clip-path: polygon(0 0, calc(100% - 18px) 0, 100% 18px, 100% 100%, 18px 100%, 0 calc(100% - 18px)); }
.brief::before { content: ""; position: absolute; top: 0; right: 0; width: 26px; height: 1px; background: var(--c1); transform-origin: right; transform: rotate(45deg) translate(-1px, 9px); }
.brief h5 { font-family: var(--mono); font-weight: 500; font-size: 11.5px; letter-spacing: .3em; text-transform: uppercase; color: var(--c3); margin-bottom: 6px; }
.brief h5 i { color: var(--c1); font-style: normal; margin: 0 6px; }
.brief p { font-size: 14.5px; line-height: 1.62; }
.abilities { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin-bottom: 14px; }
.ab { position: relative; display: flex; flex-direction: column; border: 1px solid color-mix(in srgb, var(--c1) 40%, transparent);
  background: color-mix(in srgb, var(--c1) 5%, transparent); transition: transform .35s var(--ease), border-color .3s, background .3s, box-shadow .35s; }
.ab-icon { padding: 18% 22%; color: var(--c2); }
.ab-icon svg { width: 100%; aspect-ratio: 1; fill: none; stroke: currentColor; stroke-width: 1.4; stroke-linecap: round; stroke-linejoin: round; transition: transform .4s var(--ease); }
.ab-key { font-family: var(--mono); font-size: 12px; letter-spacing: .2em; text-transform: uppercase; text-align: center; padding: 5px 0;
  border-top: 1px solid color-mix(in srgb, var(--c1) 40%, transparent);
  background: linear-gradient(180deg, color-mix(in srgb, var(--c1) 18%, transparent), color-mix(in srgb, var(--c1) 6%, transparent)); color: var(--c3); }
.ab:hover, .ab.sel { transform: translateY(-4px); border-color: var(--c1); background: color-mix(in srgb, var(--c1) 14%, transparent);
  box-shadow: 0 14px 34px -14px var(--c1), inset 0 0 24px -10px var(--c1); }
.ab:hover svg, .ab.sel svg { transform: scale(1.08); }
.ab.ult::after { content: "ULT"; position: absolute; top: -1px; right: -1px; font-family: var(--mono); font-size: 8.5px; letter-spacing: .12em;
  padding: 2px 5px; background: var(--c1); color: var(--bg1); font-weight: 500; }
.ability-detail { display: flex; gap: 14px; align-items: flex-start; min-height: 48px; margin-bottom: 30px; font-size: 13.5px; line-height: 1.55; }
.ad-key { flex: 0 0 auto; font-family: var(--mono); font-size: 11px; color: var(--bg1); background: var(--c2); padding: 2px 8px; margin-top: 2px; }
.ability-detail strong { display: block; font-family: var(--display); font-weight: 500; font-size: 13px; letter-spacing: .14em; text-transform: uppercase; color: var(--c3); }
.cta { display: flex; align-items: center; gap: 28px; flex-wrap: wrap; }
.deploy { position: relative; display: inline-flex; align-items: center; justify-content: space-between; gap: 24px; height: 60px; padding: 0 22px 0 28px; min-width: 260px;
  font-family: var(--display); font-weight: 500; font-size: 12.5px; letter-spacing: .24em; text-transform: uppercase; color: var(--bg1);
  background: linear-gradient(100deg, var(--c2), var(--c1) 70%);
  clip-path: polygon(16px 0, 100% 0, 100% calc(100% - 16px), calc(100% - 16px) 100%, 0 100%, 0 16px); overflow: hidden; transition: filter .3s; }
.deploy::after { content: ""; position: absolute; top: 0; bottom: 0; width: 60px; left: -90px; transform: skewX(-20deg);
  background: linear-gradient(90deg, transparent, rgba(255,255,255,.75), transparent); transition: left .7s var(--ease); }
.deploy:hover::after { left: 110%; }
.deploy:hover { filter: brightness(1.08) drop-shadow(0 0 24px var(--c1)); }
.deploy svg { width: 26px; height: 12px; }
.deploy-wrap { position: relative; filter: drop-shadow(0 10px 30px color-mix(in srgb, var(--c1) 45%, transparent)); }
.deploy-wrap::before { content: ""; position: absolute; inset: -6px; border: 1px solid color-mix(in srgb, var(--c1) 40%, transparent);
  clip-path: polygon(20px 0, 100% 0, 100% calc(100% - 20px), calc(100% - 20px) 100%, 0 100%, 0 20px); pointer-events: none; }
.spec-link { font-family: var(--mono); font-size: 11.5px; letter-spacing: .26em; text-transform: uppercase; color: var(--c2);
  border-bottom: 1px solid color-mix(in srgb, var(--c1) 50%, transparent); padding-bottom: 4px; transition: color .3s, border-color .3s; }
.spec-link:hover { color: var(--c3); border-color: var(--c3); }

/* Right agent nav */
.agent-nav { display: flex; flex-direction: column; align-items: flex-end; gap: 16px; }
.nav-item { display: flex; align-items: center; gap: 14px; color: var(--ac); }
.ni-text { display: flex; flex-direction: column; align-items: flex-end; gap: 3px; opacity: .45; transition: opacity .35s; }
.ni-num { font-family: var(--mono); font-size: 9.5px; letter-spacing: .3em; color: color-mix(in srgb, var(--ac) 80%, white); }
.ni-name { font-family: var(--display); font-size: 11px; font-weight: 500; letter-spacing: .2em; color: #fff; }
.ni-bar { width: 52px; height: 2px; background: rgba(255,255,255,.12); overflow: hidden; opacity: 0; transition: opacity .3s; }
.ni-bar i { display: block; height: 100%; width: 0; background: var(--ac); box-shadow: 0 0 8px var(--ac); }
.ni-glyph { width: 60px; height: 60px; padding: 10px; position: relative; transition: transform .4s var(--ease), filter .4s;
  background: color-mix(in srgb, var(--ac) 8%, transparent); border: 1px solid color-mix(in srgb, var(--ac) 30%, transparent);
  clip-path: polygon(25% 0, 75% 0, 100% 50%, 75% 100%, 25% 100%, 0 50%); }
.ni-glyph svg { width: 100%; height: 100%; fill: none; stroke: currentColor; stroke-width: 1.8; }
.nav-item:hover .ni-text, .nav-item.active .ni-text { opacity: 1; }
.nav-item:hover .ni-glyph { transform: scale(1.06); }
.nav-item.active .ni-glyph { background: color-mix(in srgb, var(--ac) 22%, transparent); border-color: var(--ac); transform: scale(1.12);
  filter: drop-shadow(0 0 14px var(--ac)); }
.nav-item.active .ni-bar { opacity: 1; }

/* Status bar */
.statusbar { position: absolute; left: 0; right: 0; bottom: 0; z-index: 6; height: 58px; padding: 0 40px; display: flex; align-items: center; justify-content: space-between; gap: 24px;
  font-family: var(--mono); font-size: 11px; letter-spacing: .18em; text-transform: uppercase; color: color-mix(in srgb, var(--c2) 70%, transparent);
  border-top: 1px solid color-mix(in srgb, var(--c1) 18%, transparent);
  background: linear-gradient(180deg, transparent, rgba(0,0,0,.3)); backdrop-filter: blur(6px); -webkit-backdrop-filter: blur(6px); }
.sb-online { display: flex; align-items: center; gap: 10px; white-space: nowrap; }
.sb-online b { color: var(--c3); font-weight: 500; }
@keyframes blink { 50% { opacity: 0; } }
.sb-count { display: flex; align-items: center; gap: 14px; white-space: nowrap; }
.sb-count b { color: var(--c3); font-weight: 500; }
.sb-arrow { width: 34px; height: 34px; display: grid; place-items: center; border: 1px solid color-mix(in srgb, var(--c1) 35%, transparent); transition: .3s; }
.sb-arrow:hover { border-color: var(--c1); background: color-mix(in srgb, var(--c1) 18%, transparent); }
.sb-arrow svg { width: 14px; height: 14px; fill: none; stroke: var(--c3); stroke-width: 1.6; }

/* ---------- Responsive ---------- */
@media (max-width: 1500px) {
  .layout { grid-template-columns: minmax(0, 1.1fr) minmax(0, .95fr) 140px; gap: 22px; }
  .brief p { font-size: 13.5px; }
}
@media (max-width: 1200px) {
  .layout { grid-template-columns: minmax(0, 1fr) minmax(0, 1fr) 88px; padding: 104px 28px 84px; }
  .ni-text { display: none; }
}
@media (max-width: 960px) {
  .site-header { padding: 18px 16px; }
  .brand-word { font-size: 14px; }
  .launch { padding: 10px 12px; font-size: 10px; }
  .stage { height: auto; min-height: 100svh; }
  .layout { display: flex; flex-direction: column; align-items: stretch; gap: 18px; padding: 86px 16px 96px; height: auto; }
  .visual { height: 50vh; min-height: 300px; align-self: stretch; }
  .agent-nav { flex-direction: row; justify-content: center; gap: 10px; order: 2; }
  .visual { order: 1; }
  .content { order: 3; }
  .ni-glyph { width: 48px; height: 48px; padding: 8px; }
  .content { max-width: none; }
  .hud-br { right: 12px; bottom: 10px; gap: 4px; }
  .stat .hud-v { font-size: 14px; min-width: 70px; }
  .statusbar { padding: 0 16px; height: 54px; }
}
@media (max-width: 520px) {
  .abilities { gap: 8px; }
  .ab-key { font-size: 11px; }
  .deploy { min-width: 0; width: 100%; }
  .deploy-wrap { width: 100%; }
  .brief { padding: 16px; gap: 14px; }
}
@media (prefers-reduced-motion: reduce) {
  .matrix > span, .orbit { animation: none !important; }
  .content-inner.is-in .r { animation-duration: .01s; }
}
</style>
</head>
<body>
<div class="cursor" aria-hidden="true"></div>
<div class="cursor-dot" aria-hidden="true"></div>

<header class="site-header" data-section="nav">
  <a class="brand" href="#" data-cursor aria-label="Myriad home">
    <svg viewBox="0 0 40 40" fill="none">
      <defs><linearGradient id="lg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" style="stop-color:var(--c3)"/><stop offset="1" style="stop-color:var(--c1)"/></linearGradient></defs>
      <path d="M20 2 36 11v18L20 38 4 29V11z" stroke="url(#lg)" stroke-width="1.6"/>
      <path d="M20 12 12.5 25h15z" stroke="url(#lg)" stroke-width="1.2" opacity=".7"/>
      <path d="M20 12V2M12.5 25 4 29M27.5 25 36 29" stroke="url(#lg)" stroke-width="1" opacity=".45"/>
      <circle cx="20" cy="12" r="2.6" fill="url(#lg)"/><circle cx="12.5" cy="25" r="2.6" fill="url(#lg)"/><circle cx="27.5" cy="25" r="2.6" fill="url(#lg)"/>
      <circle cx="20" cy="20.7" r="1.4" style="fill:var(--c3)"/>
    </svg>
    <span class="brand-word">MYRIAD<sup>OS</sup></span>
  </a>
  <a href="#" class="launch" data-cursor>Launch console
    <svg viewBox="0 0 22 10" fill="none" stroke="currentColor" stroke-width="1.4"><path d="M0 5h20M16 1l4 4-4 4"/></svg>
  </a>
</header>

<main class="stage" id="stage" data-section="hero">
  <div class="bg"></div>
  <div class="matrix" id="matrix" aria-hidden="true"></div>
  <canvas id="swarm" aria-hidden="true"></canvas>
  <div class="noise"></div>
  <div class="vignette"></div>

  <div class="layout">
    <section class="visual" id="visual" aria-label="Live swarm visualization">
      <div class="orbit-wrap" id="orbitWrap">
        <svg class="orbit o1" viewBox="0 0 400 400"><circle cx="200" cy="200" r="197" stroke-width="1"/></svg>
        <svg class="orbit o3" viewBox="0 0 400 400" id="ticks"></svg>
      </div>
      <div class="hud hud-br">
        <div class="stat"><span class="hud-k">Nodes</span><span class="hud-v" id="stNodes">0</span></div>
        <div class="stat"><span class="hud-k">Sync</span><span class="hud-v"><span id="stSync">0</span><small>%</small></span></div>
        <div class="stat"><span class="hud-k">Latency</span><span class="hud-v"><span id="stLat">0</span><small>ms</small></span></div>
      </div>
    </section>

    <section class="content" id="content">
      <div class="content-inner is-in" id="contentInner">
        <div class="title r" style="--d:0">
          <div class="title-num" aria-hidden="true">
            <span class="tn-digits" id="idx">01</span>
          </div>
          <h1 class="name" id="name">AEGIS</h1>
        </div>
        <p class="tagline r" style="--d:1" id="tagline"></p>
        <div class="brief r" style="--d:3">
          <div><h5><span id="role"></span><i>/</i><span id="topoShort"></span></h5><p id="desc"></p></div>
        </div>
        <div class="abilities r" style="--d:4" id="abilities" data-component="ability-tiles"></div>
        <div class="ability-detail r" style="--d:5" aria-live="polite">
          <span class="ad-key" id="adKey">Q</span>
          <div><strong id="adName"></strong><span id="adDesc"></span></div>
        </div>
        <div class="cta r" style="--d:6">
          <span class="deploy-wrap"><a href="#" class="deploy" data-cursor><span id="deployLabel">Deploy agent</span>
            <svg viewBox="0 0 26 12" fill="none" stroke="currentColor" stroke-width="1.6"><path d="M0 6h24M19 1l5 5-5 5"/></svg></a></span>
          <a href="#" class="spec-link" data-cursor>View spec sheet</a>
        </div>
      </div>
    </section>

    <nav class="agent-nav" id="agentNav" aria-label="Agents" data-component="agent-rail"></nav>
  </div>

  <footer class="statusbar" data-section="status">
    <div class="sb-online"><span class="live"></span><b id="online">12,480</b> agents online</div>
    <div class="sb-count">
      <button class="sb-arrow" id="prev" data-cursor aria-label="Previous agent"><svg viewBox="0 0 14 14"><path d="M9 2 4 7l5 5"/></svg></button>
      <span><b id="counter">01</b> / 05</span>
      <button class="sb-arrow" id="next" data-cursor aria-label="Next agent"><svg viewBox="0 0 14 14"><path d="m5 2 5 5-5 5"/></svg></button>
    </div>
  </footer>
</main>

<script>
(() => {
  const ICONS = {
    fork: '<circle cx="12" cy="4" r="2"/><circle cx="5" cy="20" r="2"/><circle cx="19" cy="20" r="2"/><circle cx="12" cy="20" r="2"/><path d="M12 6v5M12 11l-6 7M12 11l6 7M12 11v7"/>',
    merge: '<circle cx="5" cy="5" r="2"/><circle cx="19" cy="5" r="2"/><circle cx="12" cy="19" r="2.6"/><path d="M6.4 6.6 11 16.6M17.6 6.6 13 16.6M7 5h10"/>',
    pulse: '<path d="M2 12h4l2-6 4 12 3-9 2 3h5"/>',
    orbit: '<circle cx="12" cy="12" r="3"/><ellipse cx="12" cy="12" rx="10" ry="4" transform="rotate(-30 12 12)"/><ellipse cx="12" cy="12" rx="10" ry="4" transform="rotate(30 12 12)"/>',
    radar: '<circle cx="12" cy="12" r="9.5"/><circle cx="12" cy="12" r="5"/><path d="M12 12 19 5"/><circle cx="16" cy="9" r="1"/>',
    eye: '<path d="M2 12s4-7 10-7 10 7 10 7-4 7-10 7S2 12 2 12z"/><circle cx="12" cy="12" r="3"/>',
    target: '<circle cx="12" cy="12" r="8"/><path d="M12 1v5M12 18v5M1 12h5M18 12h5"/><circle cx="12" cy="12" r="2"/>',
    bolt: '<path d="M13 2 4 14h7l-1 8 9-12h-7z"/>',
    filter: '<path d="M3 4h18l-7 8v6l-4 2v-8z"/>',
    cube: '<path d="M12 2 21 7v10l-9 5-9-5V7z"/><path d="M12 22V12M21 7l-9 5-9-5"/>',
    lock: '<rect x="5" y="11" width="14" height="10" rx="2"/><path d="M8 11V7a4 4 0 0 1 8 0v4M12 15v2"/>',
    shield: '<path d="M12 2 4 5v6c0 5 3.5 9 8 11 4.5-2 8-6 8-11V5z"/><path d="m9 12 2 2 4-4"/>',
    code: '<path d="m8 6-6 6 6 6M16 6l6 6-6 6M14 4l-4 16"/>',
    layers: '<path d="m12 2 10 5-10 5L2 7z"/><path d="m2 12 10 5 10-5M2 17l10 5 10-5"/>',
    wave: '<path d="M2 10c2-4 4-4 6 0s4 4 6 0 4-4 6 0"/><path d="M2 16c2-4 4-4 6 0s4 4 6 0 4-4 6 0" opacity=".5"/>',
    spark: '<path d="M12 2v6M12 16v6M2 12h6M16 12h6M5 5l3.5 3.5M15.5 15.5 19 19M5 19l3.5-3.5M15.5 8.5 19 5"/>',
    loop: '<path d="M21 12a9 9 0 1 1-3-6.7L21 8"/><path d="M21 3v5h-5"/><path d="m8 12 3 3 5-6"/>',
    scale: '<path d="M12 3v18M6 21h12M4 7h16"/><path d="m4 7-3 7a3 3 0 0 0 6 0zM20 7l-3 7a3 3 0 0 0 6 0z"/>'
  };
  const trefoil = '<path d="M24 7c6 0 8.5 8 4 13.5L24 25l-4-4.5C15.5 15 18 7 24 7z"/>';
  const GLYPHS = [
    '<path d="M24 5 40 14v20L24 43 8 34V14z"/><path d="M24 14 32 18.5v11L24 34l-8-4.5v-11z" opacity=".65"/><path d="M24 5v9M40 14l-8 4.5M40 34l-8-4.5M24 43v-9M8 34l8-4.5M8 14l8 4.5" opacity=".4"/>',
    '<circle cx="24" cy="24" r="7"/><ellipse cx="24" cy="24" rx="20" ry="8" transform="rotate(-25 24 24)"/><ellipse cx="24" cy="24" rx="20" ry="8" transform="rotate(35 24 24)" opacity=".55"/><circle cx="24" cy="24" r="2" fill="currentColor"/>',
    `<g>${trefoil}</g><g transform="rotate(120 24 25)">${trefoil}</g><g transform="rotate(240 24 25)">${trefoil}</g><circle cx="24" cy="25" r="2" fill="currentColor"/>`,
    '<path d="M14 4c0 10 20 10 20 20s-20 10-20 20"/><path d="M34 4c0 10-20 10-20 20s20 10 20 20" opacity=".6"/><path d="M17 9h14M17 39h14M15 24h18" opacity=".45"/>',
    '<circle cx="24" cy="24" r="3" fill="currentColor"/><circle cx="24" cy="24" r="10"/><circle cx="24" cy="24" r="17" opacity=".55" stroke-dasharray="3 4"/><path d="M24 2v5M24 41v5M2 24h5M41 24h5" opacity=".45"/>'
  ];

  const AGENTS = [
    { name: 'AEGIS', role: 'Sentinel', cls: 'Guardrail', topo: 'Zero-trust ring', model: 'Verifier · M',
      tagline: 'Nothing ships without its signature.',
      desc: 'AEGIS watches every action the swarm takes — enforcing policy, sandboxing risky calls, and halting anything that drifts out of bounds before it reaches the real world.',
      stats: [128, 100.0, 3], theme: { c1: '#14d27c', c2: '#8ff5c4', c3: '#e3fff1', bg1: '#03100a', bg2: '#062c1b' },
      abilities: [
        ['filter', 'Policy Gate', 'Checks every tool call against your rules before it executes.'],
        ['cube', 'Sandbox', 'Runs untrusted code in a sealed, disposable environment.'],
        ['lock', 'Seal', 'Signs approved outputs so any later tampering is detectable.'],
        ['shield', 'Bastion', 'Freezes the entire swarm instantly and rolls back the last unsafe step.']] },
    { name: 'AXON', role: 'Orchestrator', cls: 'Coordinator', topo: 'Hierarchical mesh', model: 'Reasoning · L',
      tagline: 'Conducts thousands of minds as one.',
      desc: 'AXON decomposes intent into a living task graph, assigns every branch to the right specialist, and keeps the whole swarm in lockstep — re-routing work the instant a node stalls.',
      stats: [2048, 99.4, 14], theme: { c1: '#8b6cff', c2: '#c3b6ff', c3: '#efeaff', bg1: '#0a0716', bg2: '#1d1347' },
      abilities: [
        ['fork', 'Fan-out', 'Splits one goal into parallel subtasks across up to 2,048 agents.'],
        ['merge', 'Consensus', 'Merges divergent outputs into a single verified answer by weighted vote.'],
        ['pulse', 'Re-route', 'Detects stalled branches and reassigns their work in under 40 ms.'],
        ['orbit', 'Hive Mind', 'Fuses every active agent into one shared context for thirty seconds.']] },
    { name: 'KESTR', role: 'Scout', cls: 'Recon', topo: 'Distributed probe', model: 'Fast · S',
      tagline: 'Sees the whole map before you ask.',
      desc: 'KESTR ranges ahead of the swarm — crawling sources, probing APIs and mapping unknown terrain — so every downstream agent starts from ground truth instead of guesses.',
      stats: [512, 97.8, 9], theme: { c1: '#f5a742', c2: '#ffd59a', c3: '#fff3e2', bg1: '#110a03', bg2: '#33200a' },
      abilities: [
        ['radar', 'Sweep', 'Fans out lightweight crawlers across every source you have connected.'],
        ['eye', 'Deep Scan', 'Reads a target end to end and extracts structured, cited facts.'],
        ['target', 'Signal Lock', 'Pins the three most relevant leads and streams updates as they change.'],
        ['bolt', 'Skyline', 'Launches 512 probes at once and returns a ranked map of everything found.']] },
    { name: 'LOOM', role: 'Synthesist', cls: 'Builder', topo: 'Woven pipeline', model: 'Builder · L',
      tagline: 'Weaves fragments into finished work.',
      desc: 'LOOM takes the swarm\u2019s scattered outputs — code, drafts, data — and threads them into coherent, shippable artifacts, resolving conflicts strand by strand.',
      stats: [864, 98.6, 22], theme: { c1: '#2fc6ff', c2: '#a2e7ff', c3: '#e6f9ff', bg1: '#030b13', bg2: '#06263b' },
      abilities: [
        ['code', 'Thread', 'Stitches code from many agents into one module that compiles.'],
        ['layers', 'Stack', 'Assembles drafts into a structured document with consistent voice.'],
        ['wave', 'Splice', 'Resolves conflicting edits by keeping the strongest version of each part.'],
        ['spark', 'Tapestry', 'Produces the complete deliverable — tested, formatted and ready to ship.']] },
    { name: 'ECHO', role: 'Critic', cls: 'Evaluator', topo: 'Adversarial loop', model: 'Judge · M',
      tagline: 'Every answer, argued with twice.',
      desc: 'ECHO replays the swarm\u2019s reasoning against adversarial tests, scores every claim, and sends weak work back for another pass — so what leaves the hive has already survived scrutiny.',
      stats: [256, 99.1, 18], theme: { c1: '#ff4f8d', c2: '#ffa9c7', c3: '#ffe8f0', bg1: '#13040a', bg2: '#370a1d' },
      abilities: [
        ['loop', 'Replay', 'Re-runs a chain of reasoning step by step to find where it breaks.'],
        ['scale', 'Weigh', 'Scores each claim for evidence, confidence and consistency.'],
        ['eye', 'Red Team', 'Spins up adversarial agents to attack the answer from every side.'],
        ['radar', 'Resonance', 'Cross-checks the full output against every source the swarm touched.']] }
  ];

  const $ = s => document.querySelector(s);
  const root = document.documentElement;
  const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
  const pad = n => String(n).padStart(2, '0');
  const svg48 = g => `<svg viewBox="0 0 48 48">${g}</svg>`;
  let cur = 0;

  /* ---------- Build static UI ---------- */
  const nav = $('#agentNav');
  const navItems = AGENTS.map((a, i) => {
    const b = document.createElement('button');
    b.className = 'nav-item'; b.dataset.cursor = '';
    b.style.setProperty('--ac', a.theme.c1);
    b.setAttribute('aria-label', `${a.name}, ${a.role}`);
    b.innerHTML = `<span class="ni-text"><span class="ni-num">${pad(i + 1)}</span><span class="ni-name">${a.name}</span><span class="ni-bar"><i></i></span></span><span class="ni-glyph">${svg48(GLYPHS[i])}</span>`;
    b.addEventListener('click', () => go(i));
    nav.appendChild(b);
    return b;
  });

  const ticks = $('#ticks');
  let th = '';
  for (let i = 0; i < 90; i++) {
    const a = i / 90 * Math.PI * 2, r1 = i % 5 === 0 ? 180 : 184, r2 = 188;
    th += `<line x1="${200 + Math.cos(a) * r1}" y1="${200 + Math.sin(a) * r1}" x2="${200 + Math.cos(a) * r2}" y2="${200 + Math.sin(a) * r2}" stroke-width="${i % 5 === 0 ? 1.2 : .6}"/>`;
  }
  ticks.innerHTML = th;

  /* Glyph matrix background */
  const KANA = 'アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲンガギグゲゴザジズゼゾダヂヅデドバビブベボパピプペポ';
  const matrix = $('#matrix');
  let mxCols = 0, mxRows = 0;
  const orbitWrap = $('#orbitWrap');
  function buildMatrix() {
    const st = matrix.parentElement.getBoundingClientRect(), ow = orbitWrap.getBoundingClientRect();
    const size = ow.width * .92;
    matrix.style.width = matrix.style.height = size + 'px';
    matrix.style.left = (ow.left - st.left + (ow.width - size) / 2) + 'px';
    matrix.style.top = (ow.top - st.top + (ow.height - size) / 2) + 'px';
    const cell = size < 460 ? 18 : 23;
    const cols = Math.ceil(size / cell), rows = cols;
    if (cols === mxCols && rows === mxRows) return;
    mxCols = cols; mxRows = rows;
    matrix.style.setProperty('--cols', cols);
    matrix.style.setProperty('--cell', cell + 'px');
    let html = '';
    for (let i = 0, n = cols * rows; i < n; i++) html += `<span>${KANA[(Math.random() * KANA.length) | 0]}</span>`;
    matrix.innerHTML = html;
  }
  if (!reduce) setInterval(() => {
    const cells = matrix.children;
    for (let k = 0; k < 3; k++) {
      const c = cells[(Math.random() * cells.length) | 0];
      if (!c || c.getAnimations().length) continue;
      c.textContent = KANA[(Math.random() * KANA.length) | 0];
      c.classList.remove('flick'); void c.offsetWidth; c.classList.add('flick');
    }
  }, 140);

  /* ---------- Content ---------- */
  function showAbility(i) {
    const ab = AGENTS[cur].abilities[i];
    $('#adKey').textContent = 'QECX'[i];
    $('#adName').textContent = ab[1];
    $('#adDesc').textContent = ab[2];
    document.querySelectorAll('.ab').forEach((el, k) => el.classList.toggle('sel', k === i));
  }
  function fill(i) {
    const a = AGENTS[i];
    $('#idx').textContent = pad(i + 1);
    $('#tagline').textContent = a.tagline;
    $('#role').textContent = a.role;
    $('#topoShort').textContent = a.topo;
    $('#desc').textContent = a.desc;
    $('#deployLabel').textContent = 'Deploy ' + a.name;
    const wrap = $('#abilities');
    wrap.innerHTML = a.abilities.map((ab, k) =>
      `<button class="ab${k === 3 ? ' ult' : ''}" data-cursor aria-label="${ab[1]}"><span class="ab-icon"><svg viewBox="0 0 24 24">${ICONS[ab[0]]}</svg></span><span class="ab-key">${'QECX'[k]}</span></button>`).join('');
    wrap.querySelectorAll('.ab').forEach((el, k) => {
      el.addEventListener('mouseenter', () => showAbility(k));
      el.addEventListener('focus', () => showAbility(k));
      el.addEventListener('click', () => showAbility(k));
    });
    showAbility(0);
  }
  function scramble(el, text) {
    if (reduce) { el.textContent = text; return; }
    const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789#/<>%&';
    const start = performance.now(), dur = 750;
    (function step(now) {
      const p = Math.min(1, (now - start) / dur);
      let out = '';
      for (let k = 0; k < text.length; k++) out += p * text.length > k + .2 ? text[k] : chars[(Math.random() * chars.length) | 0];
      el.textContent = out;
      if (p < 1) requestAnimationFrame(step);
    })(start);
  }
  function countTo(el, to, dec) {
    const from = parseFloat(el.textContent.replace(/,/g, '')) || 0, start = performance.now(), dur = 900;
    (function step(now) {
      const p = Math.min(1, (now - start) / dur), e = 1 - Math.pow(1 - p, 3), v = from + (to - from) * e;
      el.textContent = dec ? v.toFixed(dec) : Math.round(v).toLocaleString('en-US');
      if (p < 1) requestAnimationFrame(step);
    })(start);
  }
  function applyChrome(i) {
    const a = AGENTS[i];
    for (const k in a.theme) root.style.setProperty('--' + k, a.theme[k]);
    navItems.forEach((n, k) => n.classList.toggle('active', k === i));
    $('#counter').textContent = pad(i + 1);
    countTo($('#stNodes'), a.stats[0], 0);
    countTo($('#stSync'), a.stats[1], 1);
    countTo($('#stLat'), a.stats[2], 0);
    setTargetColors(a.theme);
  }

  const inner = $('#contentInner');
  function go(i) {
    i = (i + AGENTS.length) % AGENTS.length;
    if (i === cur) return;
    cur = i; elapsed = 0;
    applyChrome(i);
    morphTo(i);
    inner.classList.remove('is-in'); inner.classList.add('is-out');
    setTimeout(() => {
      fill(i);
      inner.classList.remove('is-out'); void inner.offsetWidth; inner.classList.add('is-in');
      scramble($('#name'), AGENTS[i].name);
    }, 300);
  }

  /* ---------- Swarm engine ---------- */
  const canvas = $('#swarm'), ctx = canvas.getContext('2d');
  const stage = $('#stage'), visual = $('#visual');
  const N = innerWidth < 700 ? 380 : 640;
  let W = 0, H = 0, DPR = 1, CX = 0, CY = 0, R = 200;

  const rnd = (a, b) => a + Math.random() * (b - a);
  function rotX(p, a) { const c = Math.cos(a), s = Math.sin(a); return [p[0], p[1] * c - p[2] * s, p[1] * s + p[2] * c]; }
  function rotZ(p, a) { const c = Math.cos(a), s = Math.sin(a); return [p[0] * c - p[1] * s, p[0] * s + p[1] * c, p[2]]; }

  function shapeSphere() {
    const out = [], core = Math.floor(N * .58);
    for (let i = 0; i < core; i++) {
      const y = 1 - (i / (core - 1)) * 2, r = Math.sqrt(1 - y * y), t = i * 2.39996;
      out.push([Math.cos(t) * r * .58, y * .58, Math.sin(t) * r * .58]);
    }
    for (let i = core; i < N; i++) {
      const k = i % 2, a = Math.random() * Math.PI * 2, rr = (k ? 1.02 : .86) + rnd(-.02, .02);
      let p = [Math.cos(a) * rr, rnd(-.02, .02), Math.sin(a) * rr];
      p = rotX(p, k ? 1.2 : -.55); p = rotZ(p, k ? .35 : -.45);
      out.push(p);
    }
    return out;
  }
  function shapeKnot() {
    const out = [];
    for (let i = 0; i < N; i++) {
      const t = i / N * Math.PI * 2, r = Math.cos(3 * t) + 2;
      out.push([r * Math.cos(2 * t) * .36 + rnd(-.04, .04), r * Math.sin(2 * t) * .36 + rnd(-.04, .04), -Math.sin(3 * t) * .36 + rnd(-.04, .04)]);
    }
    return out;
  }
  function shapeIcosa() {
    const p = (1 + Math.sqrt(5)) / 2;
    const V = [[-1,p,0],[1,p,0],[-1,-p,0],[1,-p,0],[0,-1,p],[0,1,p],[0,-1,-p],[0,1,-p],[p,0,-1],[p,0,1],[-p,0,-1],[-p,0,1]];
    const E = [];
    for (let i = 0; i < 12; i++) for (let j = i + 1; j < 12; j++) {
      const d = (V[i][0]-V[j][0])**2 + (V[i][1]-V[j][1])**2 + (V[i][2]-V[j][2])**2;
      if (Math.abs(d - 4) < .01) E.push([i, j]);
    }
    const s = .98 / Math.hypot(1, p), out = [], per = Math.floor(N * .86 / E.length);
    E.forEach(([a, b]) => {
      for (let k = 0; k < per; k++) {
        const t = (k + .5) / per;
        out.push([0,1,2].map(c => (V[a][c] + (V[b][c] - V[a][c]) * t) * s + rnd(-.012, .012)));
      }
    });
    let v = 0;
    while (out.length < N) { const q = V[v++ % 12]; out.push(q.map(c => c * s + rnd(-.05, .05))); }
    return out;
  }
  function shapeHelix() {
    const out = [], strand = Math.floor(N * .78), half = strand / 2;
    for (let i = 0; i < strand; i++) {
      const s = i % 2, idx = Math.floor(i / 2), t = idx / half * 2 - 1, a = t * Math.PI * 3.2 + s * Math.PI;
      out.push([Math.cos(a) * .5 + rnd(-.02, .02), t * 1.12, Math.sin(a) * .5 + rnd(-.02, .02)]);
    }
    const rungs = 18;
    for (let i = strand; i < N; i++) {
      const r = (i - strand) % rungs, t = (r + .5) / rungs * 2 - 1, a = t * Math.PI * 3.2, u = Math.random() * 2 - 1;
      out.push([Math.cos(a) * .5 * u, t * 1.12, Math.sin(a) * .5 * u]);
    }
    return out;
  }
  function shapeEcho() {
    const out = [], rings = 7, radii = [], tot = [];
    let sum = 0;
    for (let k = 0; k < rings; k++) { radii.push(.16 + k * .15); sum += radii[k]; }
    for (let k = 0; k < rings; k++) tot.push(Math.round((N - 20) * radii[k] / sum));
    for (let k = 0; k < rings; k++) for (let j = 0; j < tot[k]; j++) {
      const a = j / tot[k] * Math.PI * 2 + k * .3;
      out.push([Math.cos(a) * radii[k], 0, Math.sin(a) * radii[k]]);
    }
    while (out.length < N) out.push([rnd(-.03, .03), rnd(-.5, .5), rnd(-.03, .03)]);
    return out.slice(0, N);
  }

  const SHAPES = [shapeIcosa, shapeSphere, shapeKnot, shapeHelix, shapeEcho].map(fn => {
    const pts = fn(), T = new Float32Array(N * 3);
    pts.forEach((p, i) => { T[i * 3] = p[0]; T[i * 3 + 1] = p[1]; T[i * 3 + 2] = p[2]; });
    const NB = new Int16Array(N * 2);
    for (let i = 0; i < N; i++) {
      let b1 = -1, b2 = -1, d1 = 1e9, d2 = 1e9;
      const x = T[i * 3], y = T[i * 3 + 1], z = T[i * 3 + 2];
      for (let j = 0; j < N; j++) {
        if (j === i) continue;
        const dx = T[j * 3] - x, dy = T[j * 3 + 1] - y, dz = T[j * 3 + 2] - z, d = dx * dx + dy * dy + dz * dz;
        if (d < d1) { d2 = d1; b2 = b1; d1 = d; b1 = j; } else if (d < d2) { d2 = d; b2 = j; }
      }
      NB[i * 2] = b1; NB[i * 2 + 1] = b2;
    }
    return { T, NB };
  });

  const P = new Float32Array(N * 3), Vv = new Float32Array(N * 3), K = new Float32Array(N);
  const SX = new Float32Array(N), SY = new Float32Array(N), SS = new Float32Array(N);
  for (let i = 0; i < N; i++) {
    const a = Math.random() * Math.PI * 2, b = Math.acos(rnd(-1, 1)), r = rnd(1.5, 3);
    P[i * 3] = Math.sin(b) * Math.cos(a) * r; P[i * 3 + 1] = Math.cos(b) * r; P[i * 3 + 2] = Math.sin(b) * Math.sin(a) * r;
    K[i] = rnd(.012, .04);
  }
  let shape = 0;
  function morphTo(i) {
    shape = i;
    for (let k = 0; k < N * 3; k++) Vv[k] += rnd(-.06, .06);
    pulses.length = 0;
  }

  // colors
  const hex = h => [parseInt(h.slice(1, 3), 16), parseInt(h.slice(3, 5), 16), parseInt(h.slice(5, 7), 16)];
  let col = { c1: hex('#14d27c'), c2: hex('#8ff5c4'), c3: hex('#e3fff1') }, tcol = { ...col };
  function setTargetColors(t) { tcol = { c1: hex(t.c1), c2: hex(t.c2), c3: hex(t.c3) }; }
  const rgb = c => `${c[0] | 0},${c[1] | 0},${c[2] | 0}`;
  function sprite(core, mid, edge) {
    const c = document.createElement('canvas'); c.width = c.height = 64;
    const g = c.getContext('2d'), gr = g.createRadialGradient(32, 32, 0, 32, 32, 32);
    gr.addColorStop(0, `rgba(${core},1)`); gr.addColorStop(.16, `rgba(${mid},.9)`);
    gr.addColorStop(.42, `rgba(${edge},.2)`); gr.addColorStop(1, `rgba(${edge},0)`);
    g.fillStyle = gr; g.fillRect(0, 0, 64, 64); return c;
  }
  let sprA, sprB, sprKey = '';
  function refreshSprites() {
    const key = rgb(col.c1) + rgb(col.c2) + rgb(col.c3);
    if (key === sprKey) return;
    sprKey = key;
    sprA = sprite(rgb(col.c2), rgb(col.c1), rgb(col.c1));
    sprB = sprite(rgb(col.c3), rgb(col.c3), rgb(col.c2));
  }

  function resize() {
    const sr = stage.getBoundingClientRect(), vr = visual.getBoundingClientRect();
    DPR = Math.min(devicePixelRatio || 1, 2);
    W = sr.width; H = sr.height;
    canvas.width = W * DPR; canvas.height = H * DPR;
    CX = vr.left - sr.left + vr.width / 2; CY = vr.top - sr.top + vr.height / 2;
    R = Math.min(vr.width, vr.height) * .36;
    buildMatrix();
  }
  new ResizeObserver(resize).observe(stage);
  addEventListener('resize', resize);

  // mouse
  let tmx = 0, tmy = 0, mx = 0, my = 0, px = -9999, py = -9999;
  addEventListener('mousemove', e => {
    tmx = (e.clientX / innerWidth - .5) * 2; tmy = (e.clientY / innerHeight - .5) * 2;
    const r = canvas.getBoundingClientRect(); px = e.clientX - r.left; py = e.clientY - r.top;
  });
  document.addEventListener('mouseleave', () => { px = py = -9999; });

  const pulses = [];
  let rot = 0, last = performance.now(), elapsed = 0, paused = false;
  const AUTO = 9000;

  function frame(now) {
    const dt = Math.min(50, now - last); last = now;
    const t = now * .001;

    // autoplay
    if (!paused && !reduce) {
      elapsed += dt;
      if (elapsed >= AUTO) go(cur + 1);
    }
    const bar = navItems[cur].querySelector('.ni-bar i');
    navItems.forEach((n, k) => { if (k !== cur) n.querySelector('.ni-bar i').style.width = '0'; });
    bar.style.width = Math.min(100, elapsed / AUTO * 100) + '%';

    // colors
    for (const k of ['c1', 'c2', 'c3']) for (let c = 0; c < 3; c++) col[k][c] += (tcol[k][c] - col[k][c]) * .05;
    refreshSprites();

    mx += (tmx - mx) * .04; my += (tmy - my) * .04;
    rot += dt * (reduce ? .00004 : .00017);
    const ry = rot + mx * .55, rx = .3 + my * .32;
    const cy = Math.cos(ry), sy = Math.sin(ry), cx = Math.cos(rx), sx = Math.sin(rx);
    const { T, NB } = SHAPES[shape];
    const FOV = 3.2;

    for (let i = 0; i < N; i++) {
      const i3 = i * 3;
      let tx = T[i3], ty = T[i3 + 1], tz = T[i3 + 2];
      if (shape === 4) ty += .075 * Math.sin(Math.hypot(tx, tz) * 13 - t * 2.6);
      tx += Math.sin(t * 1.1 + i * 1.7) * .012; ty += Math.cos(t * 1.3 + i) * .012;
      Vv[i3] = Vv[i3] * .86 + (tx - P[i3]) * K[i];
      Vv[i3 + 1] = Vv[i3 + 1] * .86 + (ty - P[i3 + 1]) * K[i];
      Vv[i3 + 2] = Vv[i3 + 2] * .86 + (tz - P[i3 + 2]) * K[i];
      P[i3] += Vv[i3]; P[i3 + 1] += Vv[i3 + 1]; P[i3 + 2] += Vv[i3 + 2];
      const x = P[i3], y = P[i3 + 1], z = P[i3 + 2];
      const x1 = x * cy - z * sy, z1 = x * sy + z * cy;
      const y2 = y * cx - z1 * sx, z2 = y * sx + z1 * cx;
      const s = FOV / (FOV + z2);
      let X = CX + x1 * R * s, Y = CY + y2 * R * s;
      const dx = X - px, dy = Y - py, d2 = dx * dx + dy * dy;
      if (d2 < 14400) { const d = Math.sqrt(d2) || 1, f = (1 - d / 120) * 26; X += dx / d * f; Y += dy / d * f; }
      SX[i] = X; SY[i] = Y; SS[i] = s;
    }

    ctx.setTransform(DPR, 0, 0, DPR, 0, 0);
    ctx.clearRect(0, 0, W, H);
    ctx.globalCompositeOperation = 'lighter';

    // core glow
    const g = ctx.createRadialGradient(CX, CY, 0, CX, CY, R * 1.25);
    g.addColorStop(0, `rgba(${rgb(col.c1)},.22)`); g.addColorStop(1, `rgba(${rgb(col.c1)},0)`);
    ctx.fillStyle = g; ctx.fillRect(CX - R * 1.3, CY - R * 1.3, R * 2.6, R * 2.6);

    // links
    const maxL = R * .34, maxL2 = maxL * maxL;
    ctx.beginPath();
    for (let i = 0; i < N; i++) for (let k = 0; k < 2; k++) {
      const j = NB[i * 2 + k];
      if (j < 0) continue;
      const dx = SX[j] - SX[i], dy = SY[j] - SY[i];
      if (dx * dx + dy * dy < maxL2) { ctx.moveTo(SX[i], SY[i]); ctx.lineTo(SX[j], SY[j]); }
    }
    ctx.strokeStyle = `rgba(${rgb(col.c1)},.2)`; ctx.lineWidth = .7; ctx.stroke();

    // cursor beams
    if (px > -1000) {
      ctx.beginPath(); let n = 0;
      for (let i = 0; i < N && n < 9; i += 3) {
        const dx = SX[i] - px, dy = SY[i] - py;
        if (dx * dx + dy * dy < 25600) { ctx.moveTo(px, py); ctx.lineTo(SX[i], SY[i]); n++; }
      }
      ctx.strokeStyle = `rgba(${rgb(col.c2)},.28)`; ctx.lineWidth = .6; ctx.stroke();
    }

    // particles
    const sc = Math.max(.6, Math.min(1.3, R / 250));
    for (let i = 0; i < N; i++) {
      const s = SS[i], hub = i % 23 === 0;
      const a = Math.max(.12, Math.min(1, .25 + (s - .76) / .55 * .75));
      const size = (hub ? 20 : 10) * s * sc;
      ctx.globalAlpha = hub ? Math.min(1, a + .2) : a;
      ctx.drawImage(hub ? sprB : sprA, SX[i] - size / 2, SY[i] - size / 2, size, size);
    }

    // message pulses along links
    if (!reduce) {
      while (pulses.length < (N > 400 ? 38 : 22)) {
        const a = (Math.random() * N) | 0, b = NB[a * 2 + (Math.random() < .5 ? 0 : 1)];
        if (b >= 0) pulses.push({ a, b, p: 0, sp: rnd(.012, .03), hops: (Math.random() * 6) | 0 });
      }
      ctx.globalAlpha = 1;
      for (let k = pulses.length - 1; k >= 0; k--) {
        const q = pulses[k]; q.p += q.sp * dt / 16;
        if (q.p >= 1) {
          if (q.hops-- > 0) { const nb = NB[q.b * 2 + (Math.random() < .5 ? 0 : 1)]; q.a = q.b; q.b = nb >= 0 ? nb : q.a; q.p = 0; }
          else { pulses.splice(k, 1); continue; }
        }
        const x = SX[q.a] + (SX[q.b] - SX[q.a]) * q.p, y = SY[q.a] + (SY[q.b] - SY[q.a]) * q.p, s = 14 * sc;
        ctx.drawImage(sprB, x - s / 2, y - s / 2, s, s);
      }
    }
    ctx.globalAlpha = 1; ctx.globalCompositeOperation = 'source-over';
    requestAnimationFrame(frame);
  }

  /* ---------- Interactions ---------- */
  $('#prev').addEventListener('click', () => go(cur - 1));
  $('#next').addEventListener('click', () => go(cur + 1));
  addEventListener('keydown', e => {
    if (['ArrowDown', 'ArrowRight'].includes(e.key)) go(cur + 1);
    if (['ArrowUp', 'ArrowLeft'].includes(e.key)) go(cur - 1);
  });
  let wheelLock = 0;
  stage.addEventListener('wheel', e => {
    if (innerWidth <= 960 || Math.abs(e.deltaY) < 18) return;
    const n = performance.now(); if (n - wheelLock < 1100) return;
    wheelLock = n; go(cur + (e.deltaY > 0 ? 1 : -1));
  }, { passive: true });
  let tsx = null;
  visual.addEventListener('touchstart', e => { tsx = e.touches[0].clientX; }, { passive: true });
  visual.addEventListener('touchend', e => {
    if (tsx === null) return; const d = e.changedTouches[0].clientX - tsx;
    if (Math.abs(d) > 45) go(cur + (d < 0 ? 1 : -1)); tsx = null;
  });
  [$('#content'), nav].forEach(el => {
    el.addEventListener('mouseenter', () => paused = true);
    el.addEventListener('mouseleave', () => paused = false);
  });
  document.querySelectorAll('a[href="#"]').forEach(a => a.addEventListener('click', e => e.preventDefault()));

  // cursor
  const cursor = $('.cursor'), dot = $('.cursor-dot');
  let cx2 = innerWidth / 2, cy2 = innerHeight / 2, tx2 = cx2, ty2 = cy2;
  addEventListener('mousemove', e => { tx2 = e.clientX; ty2 = e.clientY; dot.style.transform = `translate(${tx2}px,${ty2}px)`; });
  document.addEventListener('mouseover', e => cursor.classList.toggle('grow', !!e.target.closest('[data-cursor]')));
  (function follow() {
    cx2 += (tx2 - cx2) * .18; cy2 += (ty2 - cy2) * .18;
    cursor.style.left = cx2 + 'px'; cursor.style.top = cy2 + 'px';
    requestAnimationFrame(follow);
  })();

  // status bar: online count + live log
  const online = $('#online'); let count = 12480;
  setInterval(() => { count += Math.round(rnd(-14, 18)); online.textContent = count.toLocaleString('en-US'); }, 1300);

  /* ---------- Init ---------- */
  fill(0); applyChrome(0); resize();
  scramble($('#name'), AGENTS[0].name);
  requestAnimationFrame(frame);
})();
</script>
</body>
</html>
```

