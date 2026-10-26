INSTALANDING.AI · Squircle Keycap Product Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Squircle Keycap Product Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/squircle-keycap-product-page

bigred-runbooks.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Squircle Keycap Product Page
  slug     squircle-keycap-product-page
  prompt   https://instalanding.ai/p/squircle-keycap-product-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/squircle-keycap-product-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties in the second <style>: --paper, --ink, --red, --green, --amber,
            --border (3px ink), --shadow (7px 7px 0 hard), --display/--body/--mono (Bricolage Grotesque,
            Instrument Sans, DM Mono); Material Icons ligatures via Google Fonts
  sections  nav, hero, run-log, stats, audit, registry, proof, playbook, footer
  scripts   one inline IIFE, no libraries: S() superellipse path + createBtn() SVG keycaps (mounted into the
            empty <span id> hosts); isometric CSS 3D deck of .k keys around the red key; six-step simulated
            run log; readiness-audit meter; registry filters + inspector + copy; WebAudio press thunk
  assets    none inlined: keys are JS-built SVG, the deck is CSS 3D, fonts load from Google Fonts

  ADAPTING
  - Keycap widths are measured from the label with canvas measureText in 700 15px Instrument Sans and
    re-measured on document.fonts.ready; change the label font in createBtn() too, or labels clip.
  - Icons are Material Icons ligature text inside SVG tspans; keep text-transform:none on the key
    (createBtn sets it) or an uppercased parent turns the icon name into the literal word.
  - Under 560px fitPhone() makes Sign in icon-only and the hero/audit keys full-width (matchMedia mirrors
    the CSS query); labelled keys otherwise push the page wider than 390px.
  - The deck's six lit ring keys map 1:1 to STEPS; keep DECK, RING_CELLS and STEPS in step together.
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>BIGRED</title>
<meta name="description" content="Landing page for a fictional runbook-automation product: a physical keycap system in a restrained brutalist layout, with a live run console, runbook registry and readiness audit." />

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,400..800&family=Instrument+Sans:wght@400;500;600;700&family=DM+Mono:wght@400;500&family=Material+Icons&display=swap" rel="stylesheet">

<style>
/* Layout: ink-outlined bento for the things you operate (hero, console, audit,
   inspector); everything you only read sits directly on the paper. Red is the
   one colour the product owns. Green means done, amber means running. */
:root {
  color-scheme: light;
  --paper: #f3efe6;
  --surface: #fffdf8;
  --tint: #e8e2d4;
  --ink: #161513;
  --muted: #5f5a51;
  --red: #e2372a;
  --red-soft: #fbd9d2;
  --green: #84cc5f;
  --amber: #f2b632;
  --shadow-c: #161513;
  --key-edge: #161513;
  --console-bg: #161513;
  --console-fg: #ece7dc;
  --console-dim: #8a857a;
  --console-line: #2f2d29;

  --border: 3px solid var(--ink);
  --shadow: 7px 7px 0 var(--shadow-c);
  --shadow-sm: 4px 4px 0 var(--shadow-c);
  --shadow-xs: 3px 3px 0 var(--shadow-c);

  --display: "Bricolage Grotesque", "Instrument Sans", system-ui, sans-serif;
  --body: "Instrument Sans", system-ui, -apple-system, "Segoe UI", sans-serif;
  --mono: "DM Mono", ui-monospace, "SF Mono", Menlo, monospace;

  --gap-section: 104px;
}

* { box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  min-width: 320px;
  margin: 0;
  color: var(--ink);
  background: var(--paper);
  font-family: var(--body);
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
}
button { color: inherit; font: inherit; }
a { color: inherit; }
:focus-visible { outline: 3px solid var(--ink); outline-offset: 4px; border-radius: 6px; }

.shell { width: min(1240px, calc(100% - 32px)); margin: 0 auto; padding-block: 22px 40px; }

.bento { border: var(--border); border-radius: 22px; background: var(--surface); box-shadow: var(--shadow); }

.eyebrow { margin: 0 0 12px; font-family: var(--mono); font-size: 0.74rem; font-weight: 500; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); }
h1, h2, h3 { margin: 0; font-family: var(--display); font-weight: 700; line-height: 1; letter-spacing: -0.035em; text-wrap: balance; }
h2 { font-size: clamp(2rem, 4.2vw, 3.4rem); font-variation-settings: "opsz" 96; }
h3 { font-size: clamp(1.3rem, 2.2vw, 1.75rem); font-variation-settings: "opsz" 48; letter-spacing: -0.025em; }
p { line-height: 1.6; }
.mono { font-family: var(--mono); font-size: 0.72rem; letter-spacing: 0.08em; text-transform: uppercase; }
.section { margin-top: var(--gap-section); }

/* ── Top bar ───────────────────────────────────────────────── */
.topbar { display: flex; align-items: center; justify-content: space-between; gap: 16px; padding: 10px 14px 10px 18px; margin-bottom: 26px; }
.brand { display: inline-flex; align-items: center; gap: 12px; font-family: var(--display); font-weight: 800; font-size: 1.3rem; letter-spacing: -0.04em; }
.topnav { display: flex; gap: 26px; font-family: var(--mono); font-size: 0.74rem; letter-spacing: 0.08em; text-transform: uppercase; }
.topnav a { text-decoration: none; color: var(--muted); transition: color 150ms ease; }
.topnav a:hover { color: var(--ink); }
.top-right { display: flex; align-items: center; gap: 14px; }
.sound-toggle { display: inline-flex; align-items: center; border: 0; background: none; padding: 4px; cursor: pointer; font-family: var(--mono); font-size: 0.7rem; letter-spacing: 0.08em; text-transform: uppercase; white-space: nowrap; color: var(--muted); }
.sound-toggle:hover { color: var(--ink); }
.sound-toggle .mi { display: none; font-size: 22px; }

/* ── Hero ──────────────────────────────────────────────────── */
.hero { display: grid; grid-template-columns: minmax(0, 1.4fr) minmax(300px, 0.8fr); overflow: hidden; }
.hero-copy { display: flex; flex-direction: column; align-items: flex-start; justify-content: center; padding: clamp(32px, 5.5vw, 72px); min-width: 0; }
.hero h1 { font-size: clamp(3.2rem, 8.4vw, 7.4rem); line-height: 0.86; letter-spacing: -0.055em; font-weight: 800; font-variation-settings: "opsz" 96; }
.hero h1 span { display: block; color: var(--red); }
.hero-desc { max-width: 54ch; margin: 28px 0 0; font-size: clamp(1.02rem, 1.4vw, 1.16rem); color: var(--muted); }
.hero-actions { display: flex; flex-wrap: wrap; gap: 14px; margin-top: 32px; align-items: center; }
.hero-note { margin: 18px 0 0; font-family: var(--mono); font-size: 0.7rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--muted); }

.hero-dial {
  position: relative; display: grid; place-items: center; padding: 34px 24px 60px; min-width: 0; overflow: hidden;
  border-left: var(--border); background-color: var(--tint);
  background-image: radial-gradient(circle, color-mix(in srgb, var(--ink) 16%, transparent) 1.2px, transparent 1.6px);
  background-size: 18px 18px;
}
.hero-dial p { position: absolute; right: 18px; bottom: 20px; left: 18px; margin: 0; font-family: var(--mono); font-size: 0.7rem; letter-spacing: 0.1em; text-align: center; text-transform: uppercase; color: var(--muted); }
.hero-dial p b { color: var(--ink); font-weight: 500; }

/* The deck: an isometric control panel built from flat faces.
   Camera = rotateX(54.7deg) rotateZ(45deg), no perspective, so it reads as
   true isometric. Only the two faces the camera can see (south, east) are drawn. */
@property --kh { syntax: "<length>"; inherits: true; initial-value: 16px; }
.deck-wrap { display: grid; place-items: center; width: 100%; }
.deck-wrap.kick { animation: kick 380ms cubic-bezier(.3,.7,.4,1); }
.deck {
  --S: min(290px, 62vw);
  --rx: 54.7deg; --rz: 45deg;
  --slab: 22px;
  position: relative; width: var(--S); height: var(--S); max-width: 100%;
  margin-top: calc(var(--S) * -0.04);
  transform-style: preserve-3d;
  transform: rotateX(var(--rx)) rotateZ(var(--rz));
  transition: transform 700ms cubic-bezier(.2,.75,.2,1);
}
.deck.intro { --rx: 70deg; --rz: 15deg; transition: none; }
.deck * { transform-style: preserve-3d; }
.slab-top, .slab-s, .slab-e { position: absolute; box-sizing: border-box; }
.slab-top { inset: 0; background: #24221f; border: 2px solid #161513; }
.slab-s { left: 0; top: 100%; width: 100%; height: var(--slab); transform-origin: top; transform: rotateX(-90deg); background: #161513; }
.slab-e { left: 100%; top: 0; width: var(--slab); height: 100%; transform-origin: left; transform: rotateY(90deg); background: #0c0b0a; }
.slab-top::after { content: ""; position: absolute; inset: 5px; border: 1px dashed rgba(236, 231, 220, 0.16); }

.plate {
  position: absolute; inset: calc(var(--S) * 0.075);
  display: grid; grid-template-columns: repeat(3, 1fr); grid-template-rows: repeat(3, 1fr);
  gap: calc(var(--S) * 0.05);
  transform: translateZ(1px);
}
.k {
  position: relative; cursor: pointer; border-radius: 4px;
  --kh: 15px;
  --top: var(--surface);
  transition: --kh 110ms ease-out;
  -webkit-tap-highlight-color: transparent;
}
.k.big { --kh: 30px; --top: var(--red); }
.k.big.stop { --top: #4a4f57; }
.k.run { --top: var(--amber); }
.k.done { --top: var(--green); }
@media (hover: hover) {
  .k:hover { --kh: 18px; }
  .k.big:hover { --kh: 33px; }
}
.k.down, .k.down:hover { --kh: 5px; }
.k.big.down, .k.big.down:hover { --kh: 12px; }
.k-top, .k-s, .k-e { position: absolute; box-sizing: border-box; border: 2px solid #161513; transition: background-color 220ms ease; }
.k-top {
  inset: 0; display: grid; place-items: center; border-radius: 4px;
  transform: translateZ(var(--kh));
  background-color: var(--top);
  background-image: linear-gradient(135deg, rgba(255,255,255,0.32), rgba(255,255,255,0) 55%);
}
.k-s { left: 0; top: 100%; width: 100%; height: var(--kh); transform-origin: top; transform: rotateX(90deg); background-color: color-mix(in srgb, var(--top) 80%, #000); }
.k-e { left: 100%; top: 0; width: var(--kh); height: 100%; transform-origin: left; transform: rotateY(-90deg); background-color: color-mix(in srgb, var(--top) 64%, #000); }
.mi {
  font-family: "Material Icons"; font-weight: normal; font-style: normal; line-height: 1; letter-spacing: normal;
  text-transform: none; white-space: nowrap; direction: ltr; font-feature-settings: "liga"; -webkit-font-smoothing: antialiased;
}
.k-top .mi { transform: rotate(-45deg); font-size: calc(var(--S) * 0.095); color: #161513; pointer-events: none; }
.k.big .k-top .mi { font-size: calc(var(--S) * 0.13); color: #fff; }
.k:focus-visible { outline: 3px solid var(--red); outline-offset: 3px; }
@keyframes kick { 0% { transform: translate(0, 0); } 20% { transform: translate(-4px, 2px) rotate(-1deg); } 45% { transform: translate(4px, -1px) rotate(1deg); } 70% { transform: translate(-2px, 0); } 100% { transform: translate(0, 0); } }

/* ── Console ───────────────────────────────────────────────── */
.console { margin-top: 26px; padding: 22px 24px 20px; background: var(--console-bg); color: var(--console-fg); border-color: var(--console-bg); }
.console-head { display: flex; flex-wrap: wrap; align-items: center; gap: 10px 14px; padding-bottom: 14px; border-bottom: 1px solid var(--console-line); font-family: var(--mono); font-size: 0.72rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--console-dim); }
.console-head .live { display: inline-flex; align-items: center; gap: 8px; color: var(--console-fg); }
.console-head .live i { width: 8px; height: 8px; border-radius: 50%; background: var(--green); }
.console-head .live.busy i { background: var(--amber); animation: pulse 1s ease-in-out infinite; }
.console-head .spacer { margin-left: auto; }
@keyframes pulse { 50% { opacity: 0.35; } }

.steps { display: grid; gap: 2px; margin-top: 12px; font-family: var(--mono); font-size: 0.8rem; }
.step { display: grid; grid-template-columns: 18px minmax(0, 1fr) auto; gap: 14px; align-items: start; padding: 10px 6px; border-radius: 10px; color: var(--console-dim); transition: background 200ms ease, color 200ms ease; }
.step .tick { width: 14px; height: 14px; margin-top: 2px; border: 2px solid var(--console-line); border-radius: 50%; }
.step .body { min-width: 0; }
.step .txt { display: block; }
.step .cmd { display: block; margin-top: 3px; font-size: 0.74rem; color: var(--console-dim); opacity: 0.55; overflow-wrap: anywhere; }
.step .cmd::before { content: "$ "; }
.step .meta { text-align: right; font-size: 0.72rem; font-variant-numeric: tabular-nums; white-space: nowrap; }
.step .meta b { display: block; font-weight: 400; color: var(--console-fg); }
.step.run { background: rgba(242, 182, 50, 0.08); color: var(--console-fg); }
.step.run .tick { border-color: var(--amber); border-right-color: transparent; animation: spin 0.7s linear infinite; }
.step.run .cmd, .step.done .cmd { opacity: 1; }
.step.done { color: var(--console-fg); }
.step.done .tick { border-color: var(--green); background: var(--green); }
@keyframes spin { to { transform: rotate(1turn); } }

.prompt { display: flex; align-items: center; gap: 8px; margin-top: 12px; padding: 12px 6px 2px; border-top: 1px solid var(--console-line); font-family: var(--mono); font-size: 0.8rem; }
.prompt .ps { color: var(--green); }
.cursor { display: inline-block; width: 8px; height: 1.1em; background: var(--console-fg); animation: blink 1.05s steps(1) infinite; }
@keyframes blink { 50% { opacity: 0; } }

/* ── Stats (on paper, no frames) ───────────────────────────── */
.stats { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); border-top: var(--border); }
.stat { display: flex; flex-direction: column; gap: 6px; padding: 26px 24px 4px 0; min-width: 0; }
.stat + .stat { padding-left: 24px; border-left: 1px solid color-mix(in srgb, var(--ink) 22%, transparent); }
.stat .mono { color: var(--muted); }
.stat strong { margin-top: 18px; font-family: var(--display); font-size: clamp(3.2rem, 5.6vw, 5rem); font-weight: 700; letter-spacing: -0.06em; line-height: 0.9; font-variant-numeric: tabular-nums; font-variation-settings: "opsz" 96; }
.stat strong small { font-size: 0.4em; letter-spacing: -0.02em; margin-left: 4px; }
.stat:first-child strong { color: var(--red); }
.stat span { font-weight: 500; line-height: 1.4; color: var(--muted); }
.stats-source { margin: 22px 0 0; font-family: var(--mono); font-size: 0.68rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--muted); }

/* ── Audit ─────────────────────────────────────────────────── */
.audit { padding: clamp(26px, 4.4vw, 52px); }
.audit-head, .audit-result, .section-head { display: flex; align-items: center; justify-content: space-between; gap: 22px; }
.grade { display: grid; flex: 0 0 auto; width: 96px; aspect-ratio: 1; place-items: center; border: var(--border); border-radius: 50%; background: var(--tint); box-shadow: var(--shadow-sm); font-family: var(--display); font-size: 2.3rem; font-weight: 800; transition: background 300ms ease; }
.grade.ok { background: var(--green); color: #161513; }
.meter { height: 30px; margin-top: 32px; overflow: hidden; border: var(--border); border-radius: 999px; background: repeating-linear-gradient(-45deg, var(--paper) 0 10px, var(--surface) 10px 20px); }
.meter span { display: block; width: 0; height: 100%; background: var(--ink); transition: width 120ms linear; }
.audit-result { margin-top: 18px; align-items: flex-end; }
.audit-result p { max-width: 70ch; margin: 0; color: var(--muted); }
.audit-result b { flex: 0 0 auto; font-family: var(--mono); font-size: 1.1rem; font-variant-numeric: tabular-nums; }
.audit-actions { display: flex; gap: 12px; margin-top: 26px; flex-wrap: wrap; }

/* ── Registry ──────────────────────────────────────────────── */
.section-head { align-items: flex-end; margin-bottom: 26px; }
.filters { display: flex; flex-wrap: wrap; justify-content: flex-end; gap: 10px; }
.filter { padding: 9px 15px; border: var(--border); border-radius: 999px; background: var(--surface); box-shadow: var(--shadow-xs); font-size: 0.84rem; font-weight: 600; cursor: pointer; transition: transform 140ms ease, box-shadow 140ms ease, background 140ms ease, color 140ms ease; }
.filter:hover { transform: translate(-1px, -1px); box-shadow: 4px 4px 0 var(--shadow-c); }
.filter:active { transform: translate(3px, 3px); box-shadow: 0 0 0 var(--shadow-c); }
.filter.active { background: var(--ink); color: var(--paper); }

.workspace { display: grid; grid-template-columns: minmax(0, 1.5fr) minmax(320px, 0.8fr); gap: 26px; align-items: start; }
.cards { display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); gap: 18px; min-width: 0; }
.rb {
  position: relative; display: grid; gap: 10px; justify-items: start; align-content: start; min-height: 220px; padding: 22px; overflow: hidden; cursor: pointer;
  border: var(--border); border-radius: 20px; background: var(--surface); box-shadow: var(--shadow-sm); text-align: left;
  transition: transform 140ms ease, box-shadow 140ms ease, background 200ms ease;
}
.rb::after { content: ""; position: absolute; right: -28px; bottom: -28px; width: 88px; height: 88px; border: var(--border); border-radius: 50%; background: var(--red); transform: scale(0); transition: transform 260ms cubic-bezier(.3,1.4,.5,1); }
.rb:hover { transform: translate(-2px, -2px); box-shadow: 6px 6px 0 var(--shadow-c); }
.rb:active { transform: translate(3px, 3px); box-shadow: 1px 1px 0 var(--shadow-c); }
.rb.selected { background: var(--red-soft); transform: translate(-2px, -2px); box-shadow: 6px 6px 0 var(--shadow-c); }
.rb.selected::after { transform: scale(1); }
.rb-top { display: flex; justify-content: space-between; gap: 16px; width: 100%; color: var(--muted); }
.rb h3 { max-width: 86%; margin-top: 22px; }
.rb p { max-width: 84%; margin: 0; color: var(--muted); }

.inspector { position: sticky; top: calc(18px + env(safe-area-inset-top, 0px)); min-width: 0; padding: 26px; background: var(--console-bg); color: var(--console-fg); --key-edge: var(--console-fg); }
.inspector-top { display: flex; align-items: center; justify-content: space-between; gap: 16px; }
.badge { padding: 7px 11px; border: 1.5px solid var(--console-fg); border-radius: 999px; font-family: var(--mono); font-size: 0.66rem; font-weight: 500; letter-spacing: 0.06em; text-transform: uppercase; }
.inspector .mono { color: var(--console-dim); }
.detail-cat { margin: 32px 0 8px; color: var(--red); font-family: var(--mono); font-size: 0.72rem; letter-spacing: 0.08em; text-transform: uppercase; }
.inspector h3 { font-size: clamp(1.8rem, 3.2vw, 2.8rem); letter-spacing: -0.04em; }
.detail { margin-top: 24px; }
.detail span { font-family: var(--mono); font-size: 0.66rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--console-dim); }
.detail p { margin: 6px 0 0; color: var(--console-fg); opacity: 0.86; }
.recommend { display: flex; align-items: center; justify-content: space-between; gap: 16px; margin-top: 26px; padding: 16px; border: 1.5px solid var(--console-line); border-radius: 16px; }
.recommend > div > span { font-family: var(--mono); font-size: 0.66rem; letter-spacing: 0.08em; text-transform: uppercase; color: var(--console-dim); }
.recommend strong { display: block; margin-top: 6px; line-height: 1.3; font-weight: 600; }
.inspector-actions { display: flex; flex-wrap: wrap; gap: 14px; margin-top: 24px; align-items: center; }
.text-button { padding: 2px 4px; border: 0; background: none; color: var(--console-fg); font-weight: 600; text-decoration: underline; text-underline-offset: 4px; cursor: pointer; }
.inspector :focus-visible { outline-color: var(--console-fg); }

/* ── Proof (on paper) ──────────────────────────────────────── */
.proof { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 1.2fr); gap: 56px; padding-top: 34px; border-top: var(--border); }
.wordmarks { display: flex; flex-wrap: wrap; gap: 12px 26px; margin: 18px 0 0; padding: 0; list-style: none; }
.wordmarks li { font-family: var(--display); font-size: 1.35rem; font-weight: 700; letter-spacing: -0.03em; color: var(--muted); font-variation-settings: "opsz" 36; }
.trust { display: flex; flex-wrap: wrap; gap: 10px; margin: 30px 0 0; padding: 0; list-style: none; }
.trust li { padding: 7px 12px; border: 1.5px solid var(--ink); border-radius: 999px; font-family: var(--mono); font-size: 0.68rem; letter-spacing: 0.06em; text-transform: uppercase; }
.quote { margin: 0; min-width: 0; }
.quote blockquote { margin: 0; font-family: var(--display); font-size: clamp(1.5rem, 2.6vw, 2.2rem); font-weight: 600; line-height: 1.18; letter-spacing: -0.03em; text-wrap: balance; font-variation-settings: "opsz" 72; }
.quote blockquote::before { content: "“"; display: block; height: 0.55em; color: var(--red); font-size: 2.4em; line-height: 0.9; }
.quote figcaption { display: flex; flex-wrap: wrap; align-items: center; gap: 8px 14px; margin-top: 20px; color: var(--muted); }
.quote figcaption b { color: var(--ink); font-weight: 600; }
.tag { padding: 3px 8px; border-radius: 6px; background: var(--tint); font-family: var(--mono); font-size: 0.64rem; letter-spacing: 0.06em; text-transform: uppercase; }

/* ── Key system spec ───────────────────────────────────────── */
.spec { padding: clamp(26px, 4.4vw, 52px); }
.spec-lede { max-width: 64ch; margin: 16px 0 0; color: var(--muted); }
.spec-row { margin-top: 28px; }
.spec-title { font-family: var(--mono); font-size: 0.7rem; letter-spacing: 0.1em; text-transform: uppercase; margin: 0 0 12px; color: var(--muted); }
.spec-keys { display: flex; flex-wrap: wrap; gap: 14px; align-items: center; }

/* ── Playbook (on paper) ───────────────────────────────────── */
.remedies { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 40px; }
.remedy { padding-top: 22px; border-top: var(--border); min-width: 0; }
.remedy-n { font-family: var(--mono); font-size: 0.74rem; letter-spacing: 0.08em; color: var(--red); }
.remedy .eyebrow { margin-top: 8px; }
.remedy h3 { margin: 22px 0 14px; }
.remedy p { margin: 0; color: var(--muted); max-width: 42ch; }

/* ── Footer ────────────────────────────────────────────────── */
.footer { margin-top: var(--gap-section); padding: clamp(28px, 4.4vw, 52px); }
.footer-top { display: grid; grid-template-columns: minmax(0, 1.4fr) repeat(3, minmax(0, 0.6fr)); gap: 32px; }
.footer h2 { font-size: clamp(2rem, 4vw, 3.2rem); }
.footer h2 span { color: var(--red); }
.footer nav p { margin: 0 0 12px; font-family: var(--mono); font-size: 0.68rem; letter-spacing: 0.1em; text-transform: uppercase; color: var(--muted); }
.footer nav a { display: block; padding: 4px 0; text-decoration: none; font-weight: 500; }
.footer nav a:hover { text-decoration: underline; text-underline-offset: 4px; }
.footer-base { display: flex; flex-wrap: wrap; justify-content: space-between; gap: 12px; margin-top: 40px; padding-top: 20px; border-top: 1px solid color-mix(in srgb, var(--ink) 22%, transparent); font-family: var(--mono); font-size: 0.68rem; letter-spacing: 0.06em; text-transform: uppercase; color: var(--muted); }

/* ── Toast ─────────────────────────────────────────────────── */
.toast {
  position: fixed; right: 24px; bottom: calc(24px + env(safe-area-inset-bottom, 0px)); z-index: 40;
  display: flex; align-items: center; gap: 10px; padding: 13px 18px; border: var(--border); border-radius: 14px;
  background: var(--surface); box-shadow: var(--shadow-sm); font-weight: 600;
  opacity: 0; pointer-events: none; transform: translateY(16px); transition: opacity 200ms ease, transform 200ms ease;
}
.toast::before { content: ""; width: 9px; height: 9px; border-radius: 50%; background: var(--green); }
.toast.visible { opacity: 1; transform: translateY(0); }

/* ── Responsive ────────────────────────────────────────────── */
@media (max-width: 1050px) {
  .hero { grid-template-columns: 1fr; }
  .hero-dial { min-height: 380px; border-left: 0; border-top: var(--border); }
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .stat:nth-child(3) { padding-left: 0; border-left: 0; }
  .workspace, .proof { grid-template-columns: 1fr; }
  .proof { gap: 40px; }
  .inspector { position: relative; top: auto; }
  .topnav { display: none; }
  .footer-top { grid-template-columns: repeat(3, minmax(0, 1fr)); }
  .footer-top > div:first-child { grid-column: 1 / -1; }
}
@media (max-width: 760px) {
  :root { --gap-section: 72px; }
  .bento { border-radius: 18px; box-shadow: 5px 5px 0 var(--shadow-c); }
  .hero-copy { padding: 32px 22px 38px; }
  .cards, .remedies { grid-template-columns: 1fr; }
  .remedies { gap: 30px; }
  .stats { grid-template-columns: 1fr; }
  .stat, .stat + .stat { padding: 22px 0 18px; border-left: 0; }
  .stat + .stat { border-top: 1px solid color-mix(in srgb, var(--ink) 22%, transparent); }
  .audit-head, .audit-result, .section-head { flex-direction: column; align-items: flex-start; }
  .filters { justify-content: flex-start; }
  .footer-top { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .step { grid-template-columns: 18px minmax(0, 1fr); }
  .step .meta { grid-column: 2; text-align: left; }
  .step .meta b { display: inline; margin-right: 8px; }
  .toast { right: 12px; left: 12px; bottom: calc(12px + env(safe-area-inset-bottom, 0px)); justify-content: center; }
}
/* Phones: the bar keeps all three controls on one line. Sound becomes its
   speaker icon and Sign in drops to an icon-only key (script swaps it), and
   the keys that carry a label go full width so none runs past its card. */
@media (max-width: 560px) {
  .topbar { gap: 10px; padding: 8px 10px 8px 12px; }
  .brand { gap: 10px; }
  .top-right { gap: 6px; }
  .sound-toggle .mi { display: inline; }
  .sound-toggle .sound-label { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; }
  .hero-actions, .audit-actions { flex-direction: column; align-items: stretch; width: 100%; }
  .hero-actions > span, .audit-actions > span { display: block; width: 100%; }
}
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { scroll-behavior: auto !important; animation-duration: 1ms !important; animation-iteration-count: 1 !important; transition-duration: 1ms !important; }
  .cursor { animation: none !important; }
}
</style>

<main class="shell" id="top">

  <div class="bento topbar" data-section="nav">
    <span class="brand"><span id="brandKey"></span> BIGRED</span>
    <nav class="topnav" aria-label="Sections">
      <a href="#registry">Registry</a>
      <a href="#audit">Audit</a>
      <a href="#playbook">Playbook</a>
    </nav>
    <div class="top-right">
      <button class="sound-toggle" id="soundToggle" type="button" aria-pressed="true"><span class="mi" id="soundIcon" aria-hidden="true">volume_up</span><span class="sound-label" id="soundLabel">Sound on</span></button>
      <span id="navCta"></span>
    </div>
  </div>

  <!-- HERO -->
  <header class="bento hero" data-section="hero">
    <div class="hero-copy">
      <p class="eyebrow">Runbook automation · AI operator</p>
      <h1>One button<span>per runbook.</span></h1>
      <p class="hero-desc">Wire an incident procedure once. BIGRED turns it into a key anyone on call can press. The model does the steps, the log shows its work, and the rollback is the same key pressed twice.</p>
      <div class="hero-actions">
        <span id="heroPrimary"></span>
        <span id="heroGhost"></span>
      </div>
      <p class="hero-note">Press the red key. Nothing real is touched.</p>
    </div>
    <div class="hero-dial" id="deckStage">
      <div class="deck-wrap" id="deckWrap">
        <div class="deck intro" id="deck">
          <div class="slab-s"></div><div class="slab-e"></div><div class="slab-top"></div>
          <div class="plate" id="plate"></div>
        </div>
      </div>
      <p id="dialLabel"><b>Red key</b> · restart the payments worker</p>
    </div>
  </header>

  <!-- CONSOLE -->
  <section class="bento console" aria-label="Run log" data-section="run-log">
    <div class="console-head">
      <span class="live" id="liveDot"><i></i><span id="liveText">Ready</span></span>
      <span>run log · svc/payments@staging</span>
      <span class="spacer" id="consoleStatus">idle — press the key</span>
    </div>
    <div class="steps" id="steps"></div>
    <div class="prompt"><span class="ps">$</span><span id="promptText">bigred run rb_payments_restart</span><span class="cursor" aria-hidden="true"></span></div>
  </section>

  <!-- STATS -->
  <section class="section" aria-label="Fleet statistics" data-section="stats">
    <div class="stats">
      <article class="stat">
        <p class="mono">Runbooks on keys</p>
        <strong>128</strong>
        <span>across 22 services</span>
      </article>
      <article class="stat">
        <p class="mono">Median time to press</p>
        <strong>9<small>s</small></strong>
        <span>from page to first step</span>
      </article>
      <article class="stat">
        <p class="mono">Longest manual blocker</p>
        <strong>41<small>min</small></strong>
        <span>before the team moved to keys</span>
      </article>
      <article class="stat">
        <p class="mono">Steps run out of scope</p>
        <strong>0</strong>
        <span>every step is bound to a scope you set</span>
      </article>
    </div>
    <p class="stats-source">Example figures · median across 40 teams · Q3 2026</p>
  </section>

  <!-- AUDIT -->
  <section class="bento audit section" id="audit" data-section="audit">
    <div class="audit-head">
      <div>
        <p class="eyebrow">Readiness</p>
        <h2>Runbook readiness audit</h2>
      </div>
      <strong class="grade" id="grade">?</strong>
    </div>
    <div class="meter" id="meter" role="progressbar" aria-label="Audit progress" aria-valuemin="0" aria-valuemax="100" aria-valuenow="0"><span id="meterFill"></span></div>
    <div class="audit-result">
      <p id="auditStatus">Audit not started. Half your procedures are still a doc someone has to read at 3am.</p>
      <b id="auditPercent">0%</b>
    </div>
    <div class="audit-actions">
      <span id="auditBtn"></span>
      <span id="auditExport"></span>
    </div>
  </section>

  <!-- REGISTRY -->
  <section class="section" id="registry" data-section="registry">
    <div class="section-head">
      <div>
        <p class="eyebrow">Registry</p>
        <h2>Every procedure is a key</h2>
      </div>
      <div class="filters" id="filters">
        <button class="filter active" type="button" data-filter="all">All</button>
        <button class="filter" type="button" data-filter="recovery">Recovery</button>
        <button class="filter" type="button" data-filter="deploy">Deploy</button>
        <button class="filter" type="button" data-filter="security">Security</button>
      </div>
    </div>
    <div class="workspace" data-component="registry-inspector">
      <div class="cards" id="cards"></div>
      <aside class="bento inspector" aria-live="polite">
        <div class="inspector-top">
          <span class="badge" id="detailScope">Staging only</span>
          <span class="mono" id="detailNumber">Key 01</span>
        </div>
        <p class="detail-cat" id="detailCat">Recovery</p>
        <h3 id="detailTitle">Restart worker</h3>
        <div class="detail"><span>What it does</span><p id="detailWhat"></p></div>
        <div class="detail"><span>What it will not do</span><p id="detailWont"></p></div>
        <div class="recommend">
          <div><span>Approval</span><strong id="detailApproval">One reviewer · any hour</strong></div>
          <span id="detailKey"></span>
        </div>
        <div class="inspector-actions">
          <span id="nextKeyBtn"></span>
          <button class="text-button" id="copyBtn" type="button">Copy runbook</button>
        </div>
      </aside>
    </div>
  </section>

  <!-- PROOF -->
  <section class="section proof" aria-label="Integrations and security" data-section="proof">
    <div>
      <p class="eyebrow">Works with your stack</p>
      <ul class="wordmarks">
        <li>Kubernetes</li><li>PagerDuty</li><li>Datadog</li><li>Terraform</li><li>GitHub</li><li>Slack</li>
      </ul>
      <ul class="trust">
        <li>SOC 2 Type II</li><li>Append-only audit log</li><li>Scoped, short-lived tokens</li><li>SSO and SCIM</li>
      </ul>
    </div>
    <figure class="quote">
      <blockquote>We had a forty-page wiki for payments incidents. Now it's six keys, and our newest engineer pressed the right one on her first night on call.</blockquote>
      <figcaption><span><b>SRE lead</b> · payments platform, 140 engineers</span><span class="tag">Example quote · replace with a customer</span></figcaption>
    </figure>
  </section>

  <!-- PLAYBOOK -->
  <section class="section" id="playbook" data-section="playbook">
    <div class="section-head"><div><p class="eyebrow">Playbook</p><h2>Three moves, in order</h2></div></div>
    <div class="remedies">
      <article class="remedy">
        <span class="remedy-n">01</span>
        <p class="eyebrow">Scope</p>
        <h3>A key that cannot touch prod is a key anyone can press.</h3>
        <p>Bind every runbook to a service, an environment and a window before it reaches the board.</p>
      </article>
      <article class="remedy">
        <span class="remedy-n">02</span>
        <p class="eyebrow">Automate</p>
        <h3>Replace the doc nobody reads at 3am with one key.</h3>
        <p>The model drafts the step list from your procedure and waits for an approver who is already awake.</p>
      </article>
      <article class="remedy">
        <span class="remedy-n">03</span>
        <p class="eyebrow">Escalate</p>
        <h3>Do not let a blocker age into an incident review.</h3>
        <p>A halted run pages the next name on the rota with the failing step attached, not a summary of it.</p>
      </article>
    </div>
  </section>

  <footer class="bento footer" data-section="footer">
    <div class="footer-top">
      <div>
        <p class="eyebrow">BIGRED</p>
        <h2>Press the key.<br><span>Read the log.</span></h2>
      </div>
      <nav aria-label="Product"><p>Product</p><a href="#registry">Registry</a><a href="#audit">Readiness audit</a></nav>
      <nav aria-label="Learn"><p>Learn</p><a href="#playbook">Playbook</a><a href="#top">Run the demo</a></nav>
      <nav aria-label="Trust"><p>Trust</p><a href="#registry">Scopes and approvals</a><a href="#top">Audit log</a></nav>
    </div>
    <div class="footer-base">
      <span>BIGRED is a fictional product, built as a template</span>
      <span>Every run on this page is simulated · © <span id="year">2026</span></span>
    </div>
  </footer>
</main>

<div class="toast" id="toast" role="status" aria-live="polite">Runbook copied.</div>

<script>
(function () {
  "use strict";

  /* ── Key system ─────────────────────────────────────────────
     S() walks a superellipse (|cos|^0.6) so the corner never flattens.
     createBtn stacks it into a base, side slices and a face that travels
     on press. No drop shadow: depth is the extrusion. The face carries a
     soft top highlight; the outline reads --key-edge from the page. */
  var HEXES = ("3b82f61d4ed822c55e15803def4444b91c1cff6a00cc5500ffc800cca00014b8a6" +
    "0f766edb3b7cb02e649356d46b3fa13341551e293bffbf00cc9900ffffffd3e2ef").match(/.{6}/g);
  var COLORS = { blue: 0, green: 1, red: 2, orange: 3, yellow: 4, teal: 5, pink: 6, purple: 7, slate: 8, amber: 9, white: 10 };
  var INK = "#161513";
  var CTX = document.createElement("canvas").getContext("2d");
  var reduced = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  /* ── Press sound: a short low thunk, synthesized, quiet ───── */
  var soundOn = true, AC = null;
  function thunk(up) {
    if (!soundOn) return;
    try {
      AC = AC || new (window.AudioContext || window.webkitAudioContext)();
      var t = AC.currentTime, o = AC.createOscillator(), g = AC.createGain();
      o.type = "triangle";
      o.frequency.setValueAtTime(up ? 320 : 210, t);
      o.frequency.exponentialRampToValueAtTime(up ? 160 : 62, t + 0.05);
      g.gain.setValueAtTime(0.0001, t);
      g.gain.exponentialRampToValueAtTime(up ? 0.04 : 0.11, t + 0.004);
      g.gain.exponentialRampToValueAtTime(0.0001, t + 0.085);
      o.connect(g); g.connect(AC.destination);
      o.start(t); o.stop(t + 0.1);
    } catch (e) {}
  }
  var soundBtn = document.getElementById("soundToggle");
  soundBtn.addEventListener("click", function () {
    soundOn = !soundOn;
    document.getElementById("soundLabel").textContent = soundOn ? "Sound on" : "Sound off";
    document.getElementById("soundIcon").textContent = soundOn ? "volume_up" : "volume_off";
    soundBtn.setAttribute("aria-pressed", String(soundOn));
  });

  function S(w, h, r, x, y) {
    var p = "";
    for (var j = 0; j < 4; j++) {
      for (var i = 0; i < 31; i++) {
        var q = ((j + i / 30) * Math.PI) / 2, c = Math.cos(q), s = Math.sin(q);
        p += (j || i ? "L" : "M") +
          (x + (c > 0 ? w - r : r) + Math.sign(c) * Math.pow(Math.abs(c), 0.6) * r).toFixed(2) + " " +
          (y + (s > 0 ? h - r : r) + Math.sign(s) * Math.pow(Math.abs(s), 0.6) * r).toFixed(2);
      }
    }
    return p + "Z";
  }

  function createBtn(cfg) {
    var el = document.createElement("div");
    el.style.cursor = "pointer";
    el.style.verticalAlign = "middle";
    el.style.userSelect = "none";
    el.style.webkitTapHighlightColor = "transparent";
    el.style.textTransform = "none";
    el.style.borderRadius = "14px";
    el.setAttribute("role", "button");
    el.setAttribute("tabindex", "0");
    el.setAttribute("aria-label", cfg.aria || cfg.l || cfg.i || "button");

    var pressed = 0, hover = 0, w = 0;
    var u = Math.random().toString(36).slice(2);

    function render() {
      var c = cfg.c || "blue", l = cfg.l || "", icon = cfg.i || "", h = cfg.h || 44, sq = !!cfg.sq;
      var idx = COLORS[c] || 0, hb = HEXES[idx * 2], hd = HEXES[idx * 2 + 1], white = c === "white";
      var mix = function (hex, pct, k) { return "color-mix(in srgb, #" + hex + " " + pct + "%, " + k + ")"; };
      var scale = h / 40, label = l.toUpperCase();

      if (!w) {
        CTX.font = '700 15px "Instrument Sans", system-ui';
        w = sq ? 48 : Math.ceil((CTX.measureText(label).width + (icon ? 96 : 76)) * 1.08);
      }
      var faceY = pressed ? 8 : (hover ? 3 : 4);
      var baseY = 11;
      var z = Math.min(0.5, 20 / w);

      /* `full` can change after mount (see the phone switch below), so the
         box is set on every render rather than once at creation */
      el.style.display = cfg.full ? "block" : "inline-block";
      el.style.width = cfg.full ? "100%" : (w + 14) * scale + "px";
      el.style.height = 60 * scale + "px";

      var slices = "";
      for (var k = 0; k < Math.max(0, baseY - faceY); k++) {
        slices += '<path d="' + S(w, 40, 18, 5, faceY + 1 + k) + '" fill="url(#g' + u + ')"/>';
      }
      var faceFill = white ? "#fffdf8" : "#" + hb;
      var edge = 'style="stroke:var(--key-edge,' + INK + ')" stroke-width="' + (cfg.sw || 3) + '"';

      el.innerHTML =
        '<svg viewBox="0 0 ' + (w + 14) + ' 60" style="width:100%;height:100%;overflow:visible;display:block" preserveAspectRatio="none" aria-hidden="true">' +
          "<defs>" +
            '<linearGradient id="g' + u + '">' +
              '<stop offset="0" stop-color="' + mix(hd, 62, "white") + '"/>' +
              '<stop offset="' + z + '" stop-color="' + mix(hd, 88, "white") + '"/>' +
              '<stop offset="' + (1 - z) + '" stop-color="' + mix(hd, 88, "white") + '"/>' +
              '<stop offset="1" stop-color="' + mix(hd, 62, "white") + '"/>' +
            "</linearGradient>" +
            '<linearGradient id="h' + u + '" x1="0" y1="0" x2="0" y2="1">' +
              '<stop offset="0" stop-color="#fff" stop-opacity="' + (white ? 0 : 0.34) + '"/>' +
              '<stop offset="0.5" stop-color="#fff" stop-opacity="0"/>' +
              '<stop offset="1" stop-color="#000" stop-opacity="' + (white ? 0.04 : 0.08) + '"/>' +
            "</linearGradient>" +
          "</defs>" +
          '<path d="' + S(w, 40, 18, 5, baseY) + '" fill="' + mix(hd, 78, "black") + '" ' + edge + "/>" +
          slices +
          '<path d="' + S(w, 40, 18, 5, faceY) + '" fill="' + faceFill + '" ' + edge + "/>" +
          '<path d="' + S(w - 6, 36, 16, 8, faceY + 2) + '" fill="url(#h' + u + ')"/>' +
          '<text x="' + (5 + w / 2) + '" y="' + (20 + faceY) + '" text-anchor="middle" dominant-baseline="central" fill="' +
            (white ? INK : "#fff") + '" style="pointer-events:none;font-weight:700">' +
            '<tspan style="font-family:\'Material Icons\';font-size:' + (sq ? "26px" : "20px") + '" dy="1">' + icon + "</tspan>" +
            (!sq ? '<tspan dx="' + (icon ? 8 : 0) + '" dy="0" font-size="15" style="letter-spacing:0.6px;font-family:\'Instrument Sans\',system-ui">' + label + "</tspan>" : "") +
          "</text>" +
        "</svg>";
    }

    function press(v) { if (v === pressed) return; pressed = v; if (v) thunk(false); render(); }

    el.onpointerenter = function () { hover = 1; render(); };
    el.onpointerdown = function () { press(1); };
    el.onpointerup = function () { var was = pressed; press(0); if (was) { thunk(true); if (cfg.onPress) cfg.onPress(api); } };
    el.onpointerleave = function () { hover = 0; pressed = 0; render(); };
    el.onkeydown = function (e) { if (e.key === "Enter" || e.key === " ") { e.preventDefault(); if (!e.repeat) press(1); } };
    el.onkeyup = function (e) { if (e.key === "Enter" || e.key === " ") { press(0); thunk(true); if (cfg.onPress) cfg.onPress(api); } };

    if ("ResizeObserver" in window) {
      new ResizeObserver(function () {
        if (!cfg.full) return;
        var next = el.offsetWidth / ((cfg.h || 44) / 40) - 14;
        if (next > 0 && Math.abs(next - w) > 1) { w = next; render(); }
      }).observe(el);
    }

    var api = {
      el: el,
      set: function (next) { Object.keys(next).forEach(function (k) { cfg[k] = next[k]; }); if (!cfg.full) w = 0; render(); },
      press: function () { press(1); setTimeout(function () { press(0); if (cfg.onPress) cfg.onPress(api); }, 120); }
    };
    render();
    return api;
  }

  var mount = function (id, api) { var host = document.getElementById(id); if (host) host.appendChild(api.el); return api; };

  /* re-render keys once the label font arrives so widths are measured right */
  var allKeys = [];
  var make = function (cfg) { var k = createBtn(cfg); allKeys.push(k); return k; };
  if (document.fonts && document.fonts.ready) document.fonts.ready.then(function () { allKeys.forEach(function (k) { k.set({}); }); });

  /* ── Page furniture ─────────────────────────────────────── */
  mount("brandKey", make({ c: "red", i: "bolt", sq: true, h: 30, aria: "BIGRED" }));
  var navCta = mount("navCta", make({ c: "white", l: "Sign in", h: 36, i: "login" }));
  var heroGhost = mount("heroGhost", make({ c: "white", l: "Read the docs", h: 52, i: "menu_book", sw: 2.3 }));


  document.getElementById("year").textContent = new Date().getFullYear();

  /* ── Toast ─────────────────────────────────────────────── */
  var toast = document.getElementById("toast"), toastTimer = 0;
  function showToast(msg) {
    toast.textContent = msg;
    toast.classList.add("visible");
    clearTimeout(toastTimer);
    toastTimer = setTimeout(function () { toast.classList.remove("visible"); }, 2400);
  }

  /* ── Run console ───────────────────────────────────────── */
  var STEPS = [
    ["Fetch runbook rb_payments_restart", "bigred fetch rb_payments_restart --rev latest", 260],
    ["Plan 4 steps · model review", "bigred plan --review model --scope svc/payments@staging", 900],
    ["Drain queue · payments-worker-3", "kubectl -n payments exec payments-worker-3 -- worker drain --timeout 60s", 1100],
    ["Restart pod · wait for rollout", "kubectl -n payments rollout restart deploy/payments-worker && kubectl -n payments rollout status deploy/payments-worker", 1400],
    ["Verify /healthz · 200 in 240ms", "curl -fsS https://payments.staging.internal/healthz", 800],
    ["Write run log · notify #on-call", "bigred log --run r_7f3a --notify \"#on-call\"", 520]
  ];

  var stepsHost = document.getElementById("steps");
  var statusEl = document.getElementById("consoleStatus");
  var liveDot = document.getElementById("liveDot");
  var liveText = document.getElementById("liveText");
  var promptText = document.getElementById("promptText");
  var dialLabel = document.getElementById("dialLabel");
  var deckWrap = document.getElementById("deckWrap");
  var stepEls = [];

  STEPS.forEach(function (s) {
    var row = document.createElement("div");
    row.className = "step";
    row.innerHTML = '<span class="tick"></span><span class="body"><span class="txt"></span><span class="cmd"></span></span><span class="meta"><b class="ts"></b><span class="t"></span></span>';
    row.querySelector(".txt").textContent = s[0];
    row.querySelector(".cmd").textContent = s[1];
    stepsHost.appendChild(row);
    stepEls.push(row);
  });

  function stamp(d) {
    var p = function (n, l) { return String(n).padStart(l || 2, "0"); };
    return p(d.getHours()) + ":" + p(d.getMinutes()) + ":" + p(d.getSeconds()) + "." + p(d.getMilliseconds(), 3);
  }

  var running = false, timers = [], typers = [];

  function typeInto(el, text, ms) {
    if (reduced) { el.textContent = text; return; }
    var i = 0, step = Math.max(1, Math.ceil(text.length / Math.max(1, ms / 16)));
    el.textContent = "";
    var id = setInterval(function () {
      i = Math.min(text.length, i + step);
      el.textContent = text.slice(0, i);
      if (i >= text.length) clearInterval(id);
    }, 16);
    typers.push(id);
  }

  function resetRun() {
    timers.forEach(clearTimeout); timers = [];
    ringKeys.forEach(function (k) { k.classList.remove("run", "done"); });
    typers.forEach(clearInterval); typers = [];
    stepEls.forEach(function (el, i) {
      el.classList.remove("run", "done");
      el.querySelector(".t").textContent = "";
      el.querySelector(".ts").textContent = "";
      el.querySelector(".cmd").textContent = STEPS[i][1];
    });
  }

  function setLive(busy, text) { liveDot.classList.toggle("busy", busy); liveText.textContent = text; }

  function kick() {
    if (reduced) return;
    deckWrap.classList.remove("kick");
    void deckWrap.offsetWidth;
    deckWrap.classList.add("kick");
  }

  /* ── The deck ─────────────────────────────────────────────
     Eight runbook keys ring the red key. During a run, the first six light
     up in step order, so the deck and the log tell the same story. */
  var DEFAULT_LABEL = "<b>Red key</b> · restart the payments worker";
  var DECK = [
    { id: 1, i: "restart_alt", n: "Restart worker" },
    { id: 2, i: "undo", n: "Roll back release" },
    { id: 3, i: "expand", n: "Scale replicas" },
    { id: 4, i: "key", n: "Rotate credentials" },
    { id: 5, i: "cleaning_services", n: "Flush cache" },
    { id: 6, i: "backup", n: "Snapshot database" },
    { id: 7, i: "notifications_active", n: "Page secondary" },
    { id: 8, i: "ac_unit", n: "Freeze deploys" }
  ];
  /* clockwise from the top-left cell: grid cell index for each ring slot */
  var RING_CELLS = [0, 1, 2, 5, 8, 7, 6, 3];
  var plate = document.getElementById("plate");
  var deck = document.getElementById("deck");
  var stage = document.getElementById("deckStage");
  var ringKeys = [];
  var cells = [];

  function buildKey(icon, label, big) {
    var k = document.createElement("div");
    k.className = "k" + (big ? " big" : "");
    k.setAttribute("role", "button");
    k.setAttribute("tabindex", "0");
    k.setAttribute("aria-label", label);
    k.innerHTML = '<div class="k-s"></div><div class="k-e"></div><div class="k-top"><span class="mi" aria-hidden="true"></span></div>';
    k.querySelector(".mi").textContent = icon;
    return k;
  }

  function wireKey(k, action, hoverText) {
    var down = false;
    var start = function () { if (down) return; down = true; k.classList.add("down"); thunk(false); };
    var end = function (fire) { if (!down) return; down = false; k.classList.remove("down"); if (fire) { thunk(true); action(); } };
    k.addEventListener("pointerdown", function (e) { e.preventDefault(); start(); });
    k.addEventListener("pointerup", function () { end(true); });
    k.addEventListener("pointerleave", function () { end(false); if (!running) dialLabel.innerHTML = DEFAULT_LABEL; });
    k.addEventListener("pointerenter", function () { if (!running && hoverText) dialLabel.innerHTML = hoverText; });
    k.addEventListener("keydown", function (e) { if ((e.key === "Enter" || e.key === " ") && !e.repeat) { e.preventDefault(); start(); } });
    k.addEventListener("keyup", function (e) { if (e.key === "Enter" || e.key === " ") end(true); });
    k.addEventListener("focus", function () { if (!running && hoverText) dialLabel.innerHTML = hoverText; });
    k.addEventListener("blur", function () { if (!running) dialLabel.innerHTML = DEFAULT_LABEL; });
    return { press: function () { start(); setTimeout(function () { end(true); }, 130); } };
  }

  for (var ci = 0; ci < 9; ci++) cells.push(null);
  DECK.forEach(function (d, slot) {
    var k = buildKey(d.i, "Inspect " + d.n, false);
    var num = String(d.id).padStart(2, "0");
    wireKey(k, function () {
      select(d.id);
      dialLabel.innerHTML = "<b>Key " + num + "</b> · " + d.n + " · open in the registry below";
    }, "<b>Key " + num + "</b> · " + d.n);
    ringKeys.push(k);
    cells[RING_CELLS[slot]] = k;
  });

  var bigKey = buildKey("power_settings_new", "Run the payments restart runbook", true);
  cells[4] = bigKey;
  cells.forEach(function (k) { plate.appendChild(k); });

  /* the camera eases in from a low angle on load, then follows the pointer */
  requestAnimationFrame(function () { requestAnimationFrame(function () { deck.classList.remove("intro"); }); });
  if (reduced) deck.classList.remove("intro");
  if (!reduced && window.matchMedia("(hover: hover)").matches) {
    stage.addEventListener("pointermove", function (e) {
      var r = stage.getBoundingClientRect();
      var x = (e.clientX - r.left) / r.width - 0.5;
      var y = (e.clientY - r.top) / r.height - 0.5;
      deck.style.setProperty("--rz", (45 + x * 20).toFixed(2) + "deg");
      deck.style.setProperty("--rx", (54.7 - y * 12).toFixed(2) + "deg");
    });
    stage.addEventListener("pointerleave", function () {
      deck.style.removeProperty("--rz");
      deck.style.removeProperty("--rx");
    });
  }

  var bigred = {
    el: bigKey,
    set: function (cfg) {
      if (cfg.i) bigKey.querySelector(".mi").textContent = cfg.i;
      bigKey.classList.toggle("stop", cfg.c && cfg.c !== "red");
    }
  };
  var bigWire = wireKey(bigKey, function () { bigred.onPress(bigred); }, null);
  bigred.press = bigWire.press;
  bigred.onPress = function (btn) {
      if (running) {
        resetRun();
        running = false;
        document.body.classList.remove("running");
        statusEl.textContent = "halted — sequence rolled back";
        dialLabel.innerHTML = DEFAULT_LABEL;
        setLive(false, "Ready");
        typeInto(promptText, "bigred rollback r_7f3a  ✓ rolled back", 400);
        btn.set({ c: "red", i: "power_settings_new" });
        showToast("Run halted and rolled back.");
        return;
      }
      running = true;
      resetRun();
      kick();
      document.body.classList.add("running");
      btn.set({ c: "slate", i: "stop" });
      setLive(true, "Running");
      dialLabel.innerHTML = "<b>Running</b> · press again to roll back";
      promptText.textContent = "bigred run rb_payments_restart";

      var t = 0;
      STEPS.forEach(function (s, idx) {
        var dur = reduced ? 120 : s[2];
        timers.push(setTimeout(function () {
          var row = stepEls[idx];
          row.classList.add("run");
          ringKeys[idx].classList.add("run");
          row.querySelector(".ts").textContent = stamp(new Date());
          typeInto(row.querySelector(".cmd"), s[1], Math.min(dur * 0.6, 420));
          statusEl.textContent = "step " + (idx + 1) + " of " + STEPS.length;
        }, t));
        t += dur;
        timers.push(setTimeout(function () {
          stepEls[idx].classList.remove("run");
          stepEls[idx].classList.add("done");
          ringKeys[idx].classList.remove("run");
          ringKeys[idx].classList.add("done");
          stepEls[idx].querySelector(".t").textContent = (dur / 1000).toFixed(2) + "s";
        }, t));
      });
      timers.push(setTimeout(function () {
        running = false;
        document.body.classList.remove("running");
        statusEl.textContent = "done — 6 steps, 0 errors · " + (t / 1000).toFixed(1) + "s";
        dialLabel.innerHTML = DEFAULT_LABEL;
        setLive(false, "Ready");
        promptText.textContent = "";
        btn.set({ c: "red", i: "power_settings_new" });
        showToast("Run complete. 6 steps, 0 errors.");
        timers.push(setTimeout(function () { ringKeys.forEach(function (k) { k.classList.remove("done"); }); }, 1600));
      }, t + 200));
  };

  var heroPrimary = mount("heroPrimary", make({
    c: "red", l: "Run the demo", h: 52, i: "play_arrow", sw: 2.3,
    onPress: function () {
      document.querySelector(".console").scrollIntoView({ behavior: reduced ? "auto" : "smooth", block: "center" });
      if (!running) setTimeout(function () { bigred.press(); }, reduced ? 0 : 320);
    }
  }));

  /* ── Readiness audit ───────────────────────────────────── */
  var meterFill = document.getElementById("meterFill"), meter = document.getElementById("meter");
  var auditStatus = document.getElementById("auditStatus"), auditPercent = document.getElementById("auditPercent");
  var grade = document.getElementById("grade"), auditTimer = 0;

  var auditBtn = mount("auditBtn", make({
    c: "red", l: "Run audit", h: 48, i: "fact_check",
    onPress: function (btn) {
      clearInterval(auditTimer);
      var p = 0;
      btn.set({ l: "Auditing", c: "slate" });
      grade.textContent = "…";
      grade.classList.remove("ok");
      auditStatus.textContent = "Reading 128 procedures and checking scopes, approvals, rollbacks and who is on the rota tonight.";
      meterFill.style.width = "0%"; auditPercent.textContent = "0%"; meter.setAttribute("aria-valuenow", "0");
      auditTimer = setInterval(function () {
        p += Math.floor(Math.random() * 8) + 3;
        if (p >= 100) {
          p = 100;
          clearInterval(auditTimer);
          grade.textContent = "B+";
          grade.classList.add("ok");
          auditStatus.textContent = "Audit complete. 86% of your procedures are ready to become keys. The rest are missing a rollback or an owner.";
          btn.set({ l: "Run again", c: "red" });
          showToast("Audit complete. B+ across 128 runbooks.");
        }
        meterFill.style.width = p + "%"; auditPercent.textContent = p + "%"; meter.setAttribute("aria-valuenow", String(p));
      }, 90);
    }
  }));
  var auditExport = mount("auditExport", make({ c: "white", l: "Export report", h: 48, i: "download", onPress: function () { showToast("Report ready. Exports are simulated on this page."); } }));

  /* ── Phones ─────────────────────────────────────────────
     A key's width comes from its label, so on a narrow screen the labelled
     keys would run past their card and Sign in would push the bar wider than
     the page. Under 560px Sign in becomes an icon-only key and the hero and
     audit keys take the full width of their column. Matches the CSS query. */
  var phone = window.matchMedia("(max-width: 560px)");
  function fitPhone() {
    navCta.set({ sq: phone.matches });
    [heroPrimary, heroGhost, auditBtn, auditExport].forEach(function (k) { k.set({ full: phone.matches }); });
  }
  fitPhone();
  if (phone.addEventListener) phone.addEventListener("change", fitPhone);
  else if (phone.addListener) phone.addListener(fitPhone);

  /* ── Registry ──────────────────────────────────────────── */
  var RUNBOOKS = [
    { id: 1, name: "Restart worker", cat: "recovery", catLabel: "Recovery", scope: "Staging only", i: "restart_alt",
      summary: "Drains the queue and restarts the pod, then waits for healthy.",
      what: "Drains the queue, restarts the pod and waits for the rollout to report healthy before it writes the log.",
      wont: "Touch anything outside svc/payments, or run without an approver when the scope is prod.",
      approval: "One reviewer · any hour" },
    { id: 2, name: "Roll back release", cat: "deploy", catLabel: "Deploy", scope: "Prod · approval", i: "undo",
      summary: "Pins the previous image and drains traffic off the new one.",
      what: "Pins the last known-good image, drains traffic from the new revision and posts the diff to the incident channel.",
      wont: "Roll back a migration. Anything that touched the schema halts and pages the owner.",
      approval: "Two reviewers · release owner" },
    { id: 3, name: "Scale replicas", cat: "recovery", catLabel: "Recovery", scope: "Any environment", i: "expand",
      summary: "Doubles replicas for a window, then returns them.",
      what: "Doubles the replica count for a fixed window and restores it afterwards whether or not anyone remembers.",
      wont: "Exceed the budget ceiling you set per service.",
      approval: "None under 2× · reviewer above" },
    { id: 4, name: "Rotate credentials", cat: "security", catLabel: "Security", scope: "Prod · approval", i: "key",
      summary: "Issues new secrets and expires the old ones on a delay.",
      what: "Issues fresh secrets, updates the consumers it knows about and expires the old pair on a delay you choose.",
      wont: "Expire anything immediately. The overlap window is required.",
      approval: "Two reviewers · security" },
    { id: 5, name: "Flush cache", cat: "recovery", catLabel: "Recovery", scope: "Any environment", i: "cleaning_services",
      summary: "Invalidates by prefix and paces the refill.",
      what: "Invalidates by key prefix and paces the refill so the origin does not take the whole stampede at once.",
      wont: "Flush everything. A full flush is a different key with a different approver.",
      approval: "One reviewer · business hours" },
    { id: 6, name: "Snapshot database", cat: "security", catLabel: "Security", scope: "Prod · logged", i: "backup",
      summary: "Takes a snapshot and proves it can be restored.",
      what: "Takes a snapshot, records the LSN and restores it into a scratch instance to prove the backup works.",
      wont: "Delete an older snapshot to make room. Retention is a separate decision.",
      approval: "None · always logged" },
    { id: 7, name: "Page secondary", cat: "deploy", catLabel: "Escalation", scope: "Always available", i: "notifications_active",
      summary: "Wakes the next name on the rota with context attached.",
      what: "Pages the next name on the rota with the failing step, the run log and the last three deploys attached.",
      wont: "Page a whole team. One name, then the next, thirty seconds apart.",
      approval: "None · anyone on call" },
    { id: 8, name: "Freeze deploys", cat: "deploy", catLabel: "Deploy", scope: "Org-wide", i: "ac_unit",
      summary: "Blocks the pipeline and tells everyone why.",
      what: "Blocks every pipeline, posts the reason and the expected thaw, and keeps a list of what queued up behind it.",
      wont: "Block a rollback. Recovery keys stay live during a freeze.",
      approval: "One reviewer · incident lead" }
  ];

  var cardsHost = document.getElementById("cards");
  var filters = Array.prototype.slice.call(document.querySelectorAll(".filter"));
  var selected = 1, filter = "all";
  var detail = {
    scope: document.getElementById("detailScope"), number: document.getElementById("detailNumber"),
    cat: document.getElementById("detailCat"), title: document.getElementById("detailTitle"),
    what: document.getElementById("detailWhat"), wont: document.getElementById("detailWont"),
    approval: document.getElementById("detailApproval")
  };
  var detailKey = mount("detailKey", make({ c: "red", i: "restart_alt", sq: true, h: 46, aria: "Selected runbook key" }));

  function renderCards() {
    cardsHost.innerHTML = "";
    RUNBOOKS.forEach(function (rb) {
      var card = document.createElement("button");
      card.type = "button";
      card.className = "rb" + (rb.id === selected ? " selected" : "");
      card.hidden = filter !== "all" && rb.cat !== filter;
      card.dataset.id = rb.id;
      card.setAttribute("aria-pressed", String(rb.id === selected));
      card.innerHTML =
        '<div class="rb-top"><span class="mono">Key ' + String(rb.id).padStart(2, "0") + '</span><span class="mono">' + rb.scope + "</span></div>" +
        "<h3>" + rb.name + "</h3><p>" + rb.summary + "</p>";
      cardsHost.appendChild(card);
    });
  }

  function select(id) {
    var rb = RUNBOOKS.filter(function (r) { return r.id === id; })[0];
    if (!rb) return;
    selected = id;
    detail.scope.textContent = rb.scope;
    detail.number.textContent = "Key " + String(rb.id).padStart(2, "0");
    detail.cat.textContent = rb.catLabel;
    detail.title.textContent = rb.name;
    detail.what.textContent = rb.what;
    detail.wont.textContent = rb.wont;
    detail.approval.textContent = rb.approval;
    detailKey.set({ i: rb.i });
    renderCards();
  }

  cardsHost.addEventListener("click", function (e) { var card = e.target.closest(".rb"); if (card) select(Number(card.dataset.id)); });

  filters.forEach(function (btn) {
    btn.addEventListener("click", function () {
      filter = btn.dataset.filter;
      filters.forEach(function (b) { b.classList.toggle("active", b === btn); });
      var visible = RUNBOOKS.filter(function (r) { return filter === "all" || r.cat === filter; });
      if (visible.length && !visible.some(function (r) { return r.id === selected; })) select(visible[0].id);
      else renderCards();
    });
  });

  mount("nextKeyBtn", make({
    c: "white", l: "Next key", h: 44, i: "chevron_right",
    onPress: function () {
      var visible = RUNBOOKS.filter(function (r) { return filter === "all" || r.cat === filter; });
      if (!visible.length) return;
      var i = -1;
      visible.forEach(function (r, n) { if (r.id === selected) i = n; });
      select(visible[(i + 1) % visible.length].id);
    }
  }));

  function fallbackCopy(text, done) {
    var ta = document.createElement("textarea");
    ta.value = text; ta.setAttribute("readonly", ""); ta.style.cssText = "position:fixed;opacity:0";
    document.body.appendChild(ta); ta.select();
    try { document.execCommand("copy"); } catch (e) {}
    ta.remove(); done();
  }
  document.getElementById("copyBtn").addEventListener("click", function () {
    var rb = RUNBOOKS.filter(function (r) { return r.id === selected; })[0];
    if (!rb) return;
    var text = ["BIGRED RUNBOOK", "", "Key: " + rb.name, "Category: " + rb.catLabel, "Scope: " + rb.scope, "",
      "Does: " + rb.what, "", "Will not: " + rb.wont, "", "Approval: " + rb.approval].join("\n");
    var done = function () { showToast("Runbook copied."); };
    if (navigator.clipboard && navigator.clipboard.writeText) navigator.clipboard.writeText(text).then(done, function () { fallbackCopy(text, done); });
    else fallbackCopy(text, done);
  });

  select(1);
})();
</script>

</body></html>
```

