INSTALANDING.AI · ButtonZilla Glass Console Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
ButtonZilla Glass Console Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/buttonzilla-glass-console-page

buttonzilla-glass-console.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · ButtonZilla Glass Console Page
  slug     buttonzilla-glass-console-page
  prompt   https://instalanding.ai/p/buttonzilla-glass-console-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/buttonzilla-glass-console-page
  license  The glass buttons are ButtonZilla, a 3D button generator by Shakuro (credited in the foot line and kept as a
           link to buttonzilla.vercel.app); this console is a hardware-style front end for those buttons, and the "BZ-8"
           model name, channel names and presets are made up. Keep the credit if you ship it.

  MAP
  tokens    :root custom properties: chassis greys (--chassis-hi / --chassis-lo / --panel-*), --text / --engrave / --dim,
            amber --amber #ffb547 for lit keys and the LCD, --hot, --green for lamps; Inter for UI, JetBrains Mono for
            readouts, Unbounded for the logo
  sections  nav (topbar: logo h1, status lamps, Shuffle / Reset / Copy JSON), monitor (the WebGL preview, solo or a
            grid of eight), rack (LCD readout, signal meters, scene knobs and backdrop), bank (eight channel keys),
            modules (label, motion, shape, glass, liquid), footer (hint line and credit) (each carries data-section)
  scripts   one module script after an import map: params (FONTS, DEFAULTS, hover / click motion presets, the eight
            PRESETS), Spring, ButtonScene (three.js: a rounded slab built by slabGeometry() in MeshPhysicalMaterial with
            transmission, a canvas-texture label, a shader backdrop, bloom, ripple and liquid displacement, springs for
            hover / press), then the console: state per channel, the monitor views, segmented controls, knobs, the
            channel bank, shuffle / reset / copy, keyboard shortcuts and the signal meters
  assets    three.js 0.170.0 and its addons (RoomEnvironment, EffectComposer, RenderPass, UnrealBloomPass, OutputPass)
            from cdn.jsdelivr.net through the import map; Inter, JetBrains Mono and Unbounded from Google Fonts, and the
            label typefaces (Onest, Manrope, Unbounded, Geologica, Rubik) loaded on demand; no image files

  ADAPTING
  - Add or change a look in PRESETS (swatch, hover and click preset ids, look values); the bank and the 1-8 keys follow
    the array. Any key in DEFAULTS can go in a look.
  - Knobs are declared in KNOBS as [key, label, min, max, step, format]; a key must exist in DEFAULTS.
  - Grid view runs eight WebGL renderers at once; each scene stops drawing off screen (IntersectionObserver),
    drops to 20-30fps when only the backdrop or liquid moves, and stops when nothing does.
    Browsers cap live WebGL contexts at about 16, so don't add a second grid.
  - prefers-reduced-motion zeroes backdrop motion, float and liquid flow (the `calm` override) and turns off CSS
    transitions; the button still reacts to hover and press.
  - The import map must stay before the module script, and the file needs a network connection for three.js.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ButtonZilla Console</title>
<meta name="description" content="A control console for ButtonZilla's 3D glass buttons: eight channels, live preview, knobs for shape, glass, liquid and scene." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@500;600;700&family=JetBrains+Mono:wght@500;700&family=Unbounded:wght@700&display=swap" rel="stylesheet" />
<style>
  :root {
    --void: #070709;
    --chassis-hi: #1f1f25;
    --chassis-lo: #131317;
    --panel-hi: #1c1c22;
    --panel-lo: #15151a;
    --rim: #0a0a0d;
    --groove: #26262e;
    --text: #efedf6;
    --engrave: #aaa6ba;
    --dim: #8f8ba0;
    --amber: #ffb547;
    --amber-deep: #e8962c;
    --hot: #ff6a3d;
    --green: #5ee08f;
    --lcd: #110c05;
    --glow: 0 0 10px rgba(255, 181, 71, 0.55);
    --sans: "Inter", system-ui, -apple-system, "Segoe UI", sans-serif;
    --mono: "JetBrains Mono", ui-monospace, "SF Mono", Menlo, monospace;
    --noise: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='180' height='180'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 .045 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
  }
  * { box-sizing: border-box; }
  html, body { margin: 0; }
  body {
    min-height: 100vh;
    background:
      radial-gradient(1100px 520px at 50% -12%, rgba(255, 181, 71, 0.09), transparent 62%),
      radial-gradient(900px 600px at 100% 110%, rgba(120, 90, 255, 0.07), transparent 60%),
      var(--void);
    color: var(--text);
    font: 500 14px/1.45 var(--sans);
    -webkit-font-smoothing: antialiased;
    padding: 28px 20px 40px;
  }
  button, input, select { font: inherit; color: inherit; }
  :focus-visible { outline: 2px solid var(--amber); outline-offset: 3px; }
  svg { display: block; }
  kbd {
    display: inline-grid; place-items: center; min-width: 20px; height: 20px; padding: 0 5px;
    border-radius: 5px; background: #24242b; box-shadow: inset 0 -1px 0 rgba(0, 0, 0, 0.5), 0 0 0 1px #0b0b0e;
    font: 700 11px/1 var(--mono); color: var(--engrave);
  }

  /* ---------- chassis ---------- */
  .console {
    position: relative; max-width: 1480px; margin: 0 auto; padding: 16px;
    display: grid; gap: 14px;
    border-radius: 30px;
    background: var(--noise), linear-gradient(180deg, var(--chassis-hi) 0%, var(--chassis-lo) 100%);
    box-shadow:
      0 0 0 1px #000,
      inset 0 1px 0 rgba(255, 255, 255, 0.08),
      inset 0 -1px 0 rgba(0, 0, 0, 0.6),
      0 50px 120px rgba(0, 0, 0, 0.65),
      0 10px 30px rgba(0, 0, 0, 0.4);
  }
  .module {
    position: relative; padding: 18px 18px 20px; border-radius: 18px;
    background: var(--noise), linear-gradient(180deg, var(--panel-hi) 0%, var(--panel-lo) 100%);
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.055), 0 0 0 1px var(--rim), 0 10px 24px rgba(0, 0, 0, 0.3);
  }
  .module::before, .module::after {
    content: ""; position: absolute; top: 8px; width: 8px; height: 8px; border-radius: 50%;
    background:
      linear-gradient(45deg, transparent 42%, rgba(0, 0, 0, 0.65) 43% 57%, transparent 58%),
      radial-gradient(circle at 35% 30%, #4a4a54, #1d1d23 75%);
    box-shadow: 0 1px 0 rgba(255, 255, 255, 0.06), inset 0 0 0 0.5px rgba(0, 0, 0, 0.6);
  }
  .module::before { left: 8px; }
  .module::after { right: 8px; transform: rotate(70deg); }
  .module-head {
    display: flex; align-items: baseline; justify-content: space-between; gap: 12px; margin: 0 0 16px;
    font: 700 11px/1 var(--sans); letter-spacing: 0.18em; text-transform: uppercase; color: var(--engrave);
  }
  .module-head b { color: var(--amber); font-family: var(--mono); letter-spacing: 0.04em; margin-right: 8px; }
  .module-head small { font: 500 11px/1 var(--mono); letter-spacing: 0.02em; text-transform: none; color: var(--dim); }
  .field-label {
    display: block; margin: 0 0 8px;
    font: 700 10.5px/1 var(--sans); letter-spacing: 0.16em; text-transform: uppercase; color: var(--engrave);
  }

  /* ---------- hardware keys ---------- */
  .key {
    display: inline-flex; align-items: center; justify-content: center; gap: 8px;
    min-height: 44px; padding: 0 14px; border: 0; border-radius: 11px; cursor: pointer;
    background: linear-gradient(180deg, #2c2c34 0%, #1f1f25 100%);
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -1px 0 rgba(0, 0, 0, 0.45), 0 3px 6px rgba(0, 0, 0, 0.45), 0 0 0 1px var(--rim);
    color: #d6d3e2; font: 600 12.5px/1 var(--sans); letter-spacing: 0.05em; text-transform: uppercase; white-space: nowrap;
    transition: background 0.15s, color 0.15s, box-shadow 0.12s, transform 0.08s;
  }
  .key:hover { background: linear-gradient(180deg, #33333c 0%, #23232a 100%); color: #fff; }
  .key:active { transform: translateY(1px); box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.6), 0 0 0 1px var(--rim); }
  .key svg { width: 17px; height: 17px; flex: none; }
  .key kbd { margin-left: 2px; height: 18px; min-width: 18px; font-size: 10.5px; }
  .key .led {
    width: 7px; height: 7px; border-radius: 50%; flex: none;
    background: #3a3a44; box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.7);
    transition: background 0.15s, box-shadow 0.15s;
  }
  .key[aria-checked="true"] {
    background: linear-gradient(180deg, #18181d 0%, #212128 100%);
    box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.7), inset 0 -1px 0 rgba(255, 255, 255, 0.04), 0 0 0 1px var(--rim);
    color: #fff;
  }
  .key[aria-checked="true"] .led { background: var(--amber); box-shadow: var(--glow); }
  .key[aria-checked="true"] svg { color: var(--amber); filter: drop-shadow(0 0 5px rgba(255, 181, 71, 0.5)); }
  .key-amber {
    background: linear-gradient(180deg, #ffc771 0%, #ec9a33 100%); color: #2a1500;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), inset 0 -2px 0 rgba(120, 60, 0, 0.35), 0 4px 14px rgba(255, 160, 50, 0.28), 0 0 0 1px #5a3205;
  }
  .key-amber:hover { background: linear-gradient(180deg, #ffd189 0%, #f2a541 100%); color: #2a1500; }
  .keyrow { display: flex; flex-wrap: wrap; gap: 6px; }
  .segs {
    display: flex; flex-wrap: wrap; gap: 4px; padding: 4px; border-radius: 14px;
    background: #0f0f13; box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.6), 0 1px 0 rgba(255, 255, 255, 0.04);
  }
  .segs .key { min-height: 40px; padding: 0 12px; flex: 1 0 auto; }
  .segs.icons .key { padding: 0; min-width: 40px; flex: 1 0 40px; }

  /* ---------- top bar ---------- */
  .topbar {
    display: flex; flex-wrap: wrap; align-items: center; gap: 14px 22px; padding: 10px 10px 10px 22px;
    border-radius: 20px;
    background: linear-gradient(180deg, #19191e 0%, #141418 100%);
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.05), 0 0 0 1px var(--rim);
  }
  .brand { display: flex; align-items: baseline; gap: 14px; margin-right: auto; }
  .logo { margin: 0; font: 700 19px/1 "Unbounded", var(--sans); letter-spacing: -0.01em; color: #fff; }
  .model {
    padding: 5px 9px; border-radius: 6px; background: #0f0f13; box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.6);
    font: 700 10.5px/1 var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--amber);
  }
  .status { display: flex; gap: 16px; }
  .lamp { display: inline-flex; align-items: center; gap: 7px; font: 700 10.5px/1 var(--mono); letter-spacing: 0.14em; color: var(--engrave); }
  .lamp i { width: 8px; height: 8px; border-radius: 50%; background: #34343d; box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.7); transition: background 0.1s, box-shadow 0.1s; }
  .lamp[data-state="on"] i { background: var(--c, var(--amber)); box-shadow: 0 0 9px var(--c, var(--amber)); }
  .lamp[data-state="err"] i { background: var(--hot); box-shadow: 0 0 9px var(--hot); }
  #lamp-gl { --c: var(--green); }
  #lamp-sig { --c: var(--hot); }
  .actions { display: flex; flex-wrap: wrap; gap: 8px; }

  /* ---------- monitor + rack ---------- */
  .main { display: grid; grid-template-columns: minmax(0, 1fr) 320px; gap: 14px; }
  .monitor {
    display: flex; flex-direction: column; gap: 10px; padding: 12px; border-radius: 24px;
    background: linear-gradient(180deg, #27272e 0%, #15151a 100%);
    box-shadow: 0 0 0 1px var(--rim), inset 0 1px 0 rgba(255, 255, 255, 0.09), 0 26px 50px rgba(0, 0, 0, 0.45);
  }
  .monitor-bar, .monitor-foot { display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 10px 16px; padding: 0 6px; }
  .onair { display: flex; align-items: center; gap: 10px; min-width: 0; font: 700 11px/1 var(--mono); letter-spacing: 0.16em; text-transform: uppercase; color: var(--engrave); }
  .rec { width: 8px; height: 8px; border-radius: 50%; background: var(--hot); box-shadow: 0 0 10px var(--hot); animation: rec 1.6s ease-in-out infinite; }
  @keyframes rec { 50% { opacity: 0.35; } }
  .onair .ch { color: #fff; letter-spacing: 0.08em; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .onair .ch b { color: var(--amber); }
  .monitor-bar .segs .key { min-height: 34px; padding: 0 14px; font-size: 11.5px; }
  .monitor-foot { font-size: 12.5px; color: var(--dim); }
  .shortcuts { display: inline-flex; align-items: center; gap: 6px; flex-wrap: wrap; }

  .screen {
    position: relative; flex: 1; min-height: 560px; border-radius: 16px; overflow: hidden;
    background: #0c0c0f;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.05), 0 0 0 1px #000;
  }
  .screen::after {
    content: ""; position: absolute; inset: 0; z-index: 3; pointer-events: none; border-radius: inherit;
    box-shadow: inset 0 0 70px rgba(0, 0, 0, 0.22), inset 0 1px 0 rgba(255, 255, 255, 0.08);
    background: linear-gradient(180deg, rgba(255, 255, 255, 0.045) 0%, transparent 22%);
  }
  .stage { position: absolute; inset: 0; }
  .stage:focus-visible { outline: 2px solid var(--amber); outline-offset: -2px; }
  .screen[data-view="grid"] {
    display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); grid-template-rows: repeat(2, minmax(0, 1fr));
    gap: 6px; padding: 6px; background: #08080a;
  }
  .cell { position: relative; border-radius: 11px; overflow: hidden; background: #16161b; }
  .cell::after {
    content: ""; position: absolute; inset: 0; z-index: 2; pointer-events: none; border-radius: inherit;
    box-shadow: inset 0 0 0 1px rgba(255, 255, 255, 0.06); transition: box-shadow 0.2s;
  }
  .cell[data-current="true"]::after { box-shadow: inset 0 0 0 2px var(--amber), inset 0 0 24px rgba(255, 181, 71, 0.25); }
  .tag {
    position: absolute; top: 8px; left: 8px; z-index: 2; pointer-events: none;
    display: inline-flex; align-items: center; gap: 6px; padding: 5px 8px; border-radius: 7px;
    background: rgba(10, 10, 13, 0.72); -webkit-backdrop-filter: blur(8px); backdrop-filter: blur(8px);
    font: 700 10.5px/1 var(--mono); letter-spacing: 0.08em; text-transform: uppercase; color: #e7e4f0;
  }
  .tag b { color: var(--amber); }
  .fallback { position: absolute; inset: 0; display: grid; place-items: center; margin: 0; padding: 24px; text-align: center; color: var(--engrave); font-weight: 600; }

  .rack { display: grid; gap: 14px; align-content: start; }
  .lcd {
    position: relative; overflow: hidden; padding: 14px 16px 12px; border-radius: 12px;
    background: radial-gradient(120% 140% at 30% 0%, #1d1406 0%, var(--lcd) 70%);
    box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.85), 0 0 0 1px #000, 0 1px 0 rgba(255, 255, 255, 0.05);
    font: 500 12px/1.5 var(--mono); color: var(--amber); text-shadow: 0 0 8px rgba(255, 181, 71, 0.45);
  }
  .lcd::after {
    content: ""; position: absolute; inset: 0; pointer-events: none;
    background: repeating-linear-gradient(180deg, rgba(0, 0, 0, 0.22) 0 1px, transparent 1px 3px);
  }
  .lcd-row { display: flex; justify-content: space-between; gap: 12px; letter-spacing: 0.08em; }
  .lcd-row span:first-child { opacity: 0.72; }
  .lcd-name { margin: 6px 0 8px; font: 700 26px/1.05 var(--mono); letter-spacing: 0.04em; text-transform: uppercase; }
  .lcd-status { margin-top: 8px; padding-top: 8px; border-top: 1px dashed rgba(255, 181, 71, 0.28); letter-spacing: 0.1em; }
  .lcd-status::before { content: "> "; opacity: 0.7; }
  .meters { display: grid; gap: 12px; }
  .meter { display: grid; grid-template-columns: 52px minmax(0, 1fr); align-items: center; gap: 10px; }
  .meter span { font: 700 10.5px/1 var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: var(--engrave); }
  .bar { display: grid; grid-template-columns: repeat(20, minmax(0, 1fr)); gap: 3px; padding: 5px; border-radius: 7px; background: #0d0d10; box-shadow: inset 0 1px 3px rgba(0, 0, 0, 0.7); }
  .bar i { height: 10px; border-radius: 2px; background: #24242b; transition: background 0.05s; }
  .bar i.on { background: var(--amber); box-shadow: 0 0 6px rgba(255, 181, 71, 0.65); }
  .bar i:nth-child(n + 15).on { background: var(--hot); box-shadow: 0 0 6px rgba(255, 106, 61, 0.7); }

  .backdrop-row { display: grid; gap: 14px; margin-top: 18px; padding-top: 16px; border-top: 1px solid rgba(255, 255, 255, 0.05); }
  .wells { display: flex; gap: 14px; }
  .well { display: grid; justify-items: center; gap: 6px; font: 700 10px/1 var(--sans); letter-spacing: 0.14em; text-transform: uppercase; color: var(--engrave); cursor: pointer; }
  .well input {
    width: 40px; height: 40px; padding: 0; border: 0; border-radius: 50%; cursor: pointer; background: none;
    -webkit-appearance: none; appearance: none;
    box-shadow: 0 0 0 3px #0e0e12, 0 0 0 4px rgba(255, 255, 255, 0.08), 0 4px 10px rgba(0, 0, 0, 0.5);
  }
  .well input::-webkit-color-swatch-wrapper { padding: 0; }
  .well input::-webkit-color-swatch { border: 0; border-radius: 50%; }
  .well input::-moz-color-swatch { border: 0; border-radius: 50%; }

  /* ---------- channel bank ---------- */
  .bank { display: grid; grid-template-columns: repeat(8, minmax(0, 1fr)); gap: 8px; padding: 8px; border-radius: 20px; background: #0f0f13; box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.65), 0 1px 0 rgba(255, 255, 255, 0.04); }
  .chan {
    position: relative; display: grid; gap: 10px; align-content: space-between; min-height: 76px; padding: 12px 14px; border: 0; border-radius: 13px; cursor: pointer; text-align: left;
    background: linear-gradient(180deg, #2a2a31 0%, #1d1d23 100%);
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -1px 0 rgba(0, 0, 0, 0.45), 0 3px 8px rgba(0, 0, 0, 0.45), 0 0 0 1px var(--rim);
    transition: background 0.15s, box-shadow 0.12s, transform 0.08s;
  }
  .chan:hover { background: linear-gradient(180deg, #313139 0%, #222229 100%); }
  .chan:active { transform: translateY(1px); }
  .chan[aria-pressed="true"] {
    background: linear-gradient(180deg, #17171c 0%, #202027 100%);
    box-shadow: inset 0 2px 7px rgba(0, 0, 0, 0.75), 0 0 0 1px var(--rim), 0 0 0 1px color-mix(in srgb, var(--led) 45%, transparent) inset;
  }
  .chan-top { display: flex; align-items: center; justify-content: space-between; }
  .chan-num { font: 700 11px/1 var(--mono); letter-spacing: 0.1em; color: var(--dim); }
  .chan[aria-pressed="true"] .chan-num { color: var(--amber); }
  .chan-led {
    width: 10px; height: 10px; border-radius: 50%;
    background: radial-gradient(circle at 35% 30%, #fff 0 12%, var(--led) 55%);
    opacity: 0.38; box-shadow: inset 0 -1px 2px rgba(0, 0, 0, 0.4);
    transition: opacity 0.15s, box-shadow 0.15s;
  }
  .chan[aria-pressed="true"] .chan-led { opacity: 1; box-shadow: 0 0 12px var(--led), 0 0 3px var(--led); }
  .chan-name { font: 700 14px/1.1 var(--sans); color: #e9e6f2; }
  .chan-edit { position: absolute; right: 14px; bottom: 13px; font: 700 9.5px/1 var(--mono); letter-spacing: 0.12em; color: var(--amber); opacity: 0; transition: opacity 0.15s; }
  .chan[data-edited="true"] .chan-edit { opacity: 1; }

  /* ---------- modules ---------- */
  .modules { display: grid; grid-template-columns: repeat(12, minmax(0, 1fr)); gap: 14px; }
  .m-label { grid-column: span 5; }
  .m-motion { grid-column: span 7; }
  .m-shape { grid-column: span 3; }
  .m-glass { grid-column: span 6; }
  .m-liquid { grid-column: span 3; }
  .stack { display: grid; gap: 16px; }
  .split { display: grid; grid-template-columns: auto minmax(0, 1fr); gap: 16px; align-items: end; }
  .lcd-input {
    width: 100%; height: 50px; padding: 0 16px; border: 0; border-radius: 11px;
    background: radial-gradient(120% 160% at 20% 0%, #1d1406 0%, var(--lcd) 70%);
    box-shadow: inset 0 2px 8px rgba(0, 0, 0, 0.85), 0 0 0 1px #000, 0 1px 0 rgba(255, 255, 255, 0.05);
    color: var(--amber); caret-color: var(--amber); text-shadow: 0 0 8px rgba(255, 181, 71, 0.45);
    font: 700 18px/1 var(--mono); letter-spacing: 0.02em;
  }
  .lcd-input:focus { outline: 2px solid var(--amber); outline-offset: 2px; }
  .select {
    width: 100%; height: 48px; padding: 0 40px 0 14px; border: 0; border-radius: 12px; cursor: pointer;
    -webkit-appearance: none; appearance: none;
    background:
      url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%23ffb547' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M7 10l5 5 5-5'/%3E%3C/svg%3E") no-repeat right 12px center / 18px,
      linear-gradient(180deg, #2c2c34 0%, #1f1f25 100%);
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), 0 3px 6px rgba(0, 0, 0, 0.45), 0 0 0 1px var(--rim);
    color: #fff; font: 600 14px/1 var(--sans);
  }
  .select option { background: #1d1d23; color: #fff; }
  .motion-grid { display: grid; grid-template-columns: minmax(0, 1fr) auto; gap: 18px 22px; align-items: center; }
  .motion-keys { display: grid; gap: 14px; }
  .motion-keys .keyrow { display: grid; grid-template-columns: repeat(6, minmax(0, 1fr)); }
  .motion-keys .key { min-width: 0; padding: 0 6px; gap: 6px; font-size: 12px; letter-spacing: 0.03em; }
  .knobs { display: flex; flex-wrap: wrap; justify-content: space-around; gap: 14px 8px; }
  .divider { width: 1px; align-self: stretch; background: linear-gradient(180deg, transparent, rgba(255, 255, 255, 0.07), transparent); }

  /* ---------- knob ---------- */
  .knob { display: grid; justify-items: center; gap: 4px; width: 76px; }
  .dial { position: relative; width: 72px; height: 72px; border-radius: 50%; cursor: ns-resize; touch-action: none; }
  .dial svg { position: absolute; inset: 0; width: 72px; height: 72px; overflow: visible; }
  .dial .ticks line { stroke: #4a4855; stroke-width: 1.4; stroke-linecap: round; }
  .dial .track { fill: none; stroke: #0b0b0e; stroke-width: 4.5; stroke-linecap: round; }
  .dial .fill { fill: none; stroke: var(--amber); stroke-width: 3; stroke-linecap: round; filter: drop-shadow(0 0 3px rgba(255, 181, 71, 0.7)); }
  .cap {
    position: absolute; inset: 15px; border-radius: 50%;
    background: radial-gradient(circle at 36% 28%, #55555f 0%, #2a2a31 46%, #18181d 100%);
    box-shadow: 0 7px 12px rgba(0, 0, 0, 0.6), 0 2px 3px rgba(0, 0, 0, 0.5), inset 0 1px 0 rgba(255, 255, 255, 0.14), inset 0 -2px 4px rgba(0, 0, 0, 0.5);
  }
  .cap::before {
    content: ""; position: absolute; inset: 0; border-radius: 50%;
    background: repeating-conic-gradient(rgba(255, 255, 255, 0.075) 0 5deg, rgba(0, 0, 0, 0.18) 5deg 10deg);
    -webkit-mask: radial-gradient(circle, transparent 68%, #000 70%); mask: radial-gradient(circle, transparent 68%, #000 70%);
  }
  .cap::after {
    content: ""; position: absolute; inset: 9px; border-radius: 50%;
    background: radial-gradient(circle at 40% 30%, #3c3c45, #1e1e24);
    box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.6), 0 1px 0 rgba(255, 255, 255, 0.05);
  }
  .mark { position: absolute; z-index: 1; top: 3px; left: calc(50% - 1.5px); width: 3px; height: 9px; border-radius: 2px; background: var(--amber); box-shadow: var(--glow); }
  .dial:focus-visible { outline: 2px solid var(--amber); outline-offset: 2px; }
  .dial.is-drag .cap { box-shadow: 0 4px 8px rgba(0, 0, 0, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.14), inset 0 -2px 4px rgba(0, 0, 0, 0.5), 0 0 0 1px rgba(255, 181, 71, 0.35); }
  .knob-label { font: 700 10.5px/1 var(--sans); letter-spacing: 0.14em; text-transform: uppercase; color: var(--engrave); }
  .knob-val { font: 500 11.5px/1 var(--mono); color: var(--text); min-height: 1em; }

  .foot { max-width: 1480px; margin: 16px auto 0; display: flex; flex-wrap: wrap; justify-content: space-between; gap: 8px; color: var(--dim); font-size: 12.5px; }
  .foot a { color: var(--engrave); font-weight: 700; }

  /* ---------- responsive ---------- */
  @media (max-width: 1200px) {
    .main { grid-template-columns: 1fr; }
    .rack { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    .m-label, .m-motion { grid-column: span 12; }
    .m-shape, .m-liquid { grid-column: span 6; }
    .m-glass { grid-column: span 12; }
  }
  @media (max-width: 860px) {
    .rack { grid-template-columns: 1fr; }
    .bank { grid-template-columns: repeat(4, minmax(0, 1fr)); }
    .main { display: contents; }
    .monitor { order: 1; }
    .bank { order: 2; }
    .rack { order: 3; }
    .modules { order: 4; }
    .motion-keys .keyrow { grid-template-columns: repeat(3, minmax(0, 1fr)); }
    .screen { min-height: 420px; }
    .screen[data-view="grid"] { min-height: 820px; grid-template-columns: repeat(2, minmax(0, 1fr)); grid-template-rows: repeat(4, minmax(0, 1fr)); }
    .motion-grid { grid-template-columns: 1fr; }
  }
  @media (max-width: 640px) {
    body { padding: 12px 10px 28px; }
    .console { padding: 10px; gap: 10px; border-radius: 22px; }
    .main, .modules, .rack { gap: 10px; }
    .m-shape, .m-liquid { grid-column: span 12; }
    .topbar { padding: 12px; }
    .status { display: none; }
    .actions { width: 100%; }
    .actions .key { flex: 1; padding: 0 10px; }
    .actions kbd { display: none; }
    .monitor { padding: 8px; border-radius: 18px; }
    .screen { min-height: 340px; }
    .screen[data-view="grid"] { min-height: 680px; }
    .monitor-foot .shortcuts { display: none; }
    .chan { min-height: 64px; padding: 10px; }
    .chan-name { font-size: 12.5px; }
    .chan-edit { display: none; }
    .split { grid-template-columns: 1fr; }
  }
  @media (prefers-reduced-motion: reduce) {
    * { transition: none !important; animation: none !important; }
  }
</style>
</head>
<body>

<main class="console" id="console">
  <header class="topbar" data-section="nav">
    <div class="brand">
      <h1 class="logo">ButtonZilla</h1>
      <span class="model">Glass console · BZ-8</span>
    </div>
    <div class="status" aria-label="Status lamps">
      <span class="lamp" data-state="on"><i></i>PWR</span>
      <span class="lamp" id="lamp-gl"><i></i>GL</span>
      <span class="lamp" id="lamp-sig"><i></i>SIG</span>
    </div>
    <div class="actions">
      <button type="button" class="key" id="shuffle" aria-keyshortcuts="R">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M3 7h3.5c4.5 0 6.5 10 11 10H21"/><path d="M3 17h3.5c1.6 0 2.8-1.2 3.8-2.9"/><path d="M13.7 9.9C14.7 8.2 15.9 7 17.5 7H21"/><path d="M18.5 4.5L21 7l-2.5 2.5"/><path d="M18.5 14.5L21 17l-2.5 2.5"/></svg>
        Shuffle <kbd>R</kbd>
      </button>
      <button type="button" class="key" id="reset">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 12a8 8 0 1 0 2.4-5.7"/><path d="M4 4.5v4h4"/></svg>
        Reset
      </button>
      <button type="button" class="key key-amber" id="copy">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="8.5" y="8.5" width="11" height="11" rx="2.5"/><path d="M15.5 8.5V6.5a2 2 0 0 0-2-2h-7a2 2 0 0 0-2 2v7a2 2 0 0 0 2 2h2"/></svg>
        Copy JSON
      </button>
    </div>
  </header>

  <div class="main">
    <section class="monitor" data-section="monitor" aria-label="Preview monitor">
      <div class="monitor-bar">
        <div class="onair"><span class="rec" aria-hidden="true"></span>Live <span class="ch" id="hud"></span></div>
        <div class="segs" id="view" role="radiogroup" aria-label="Monitor view"></div>
      </div>
      <div class="screen" id="screen" data-view="solo"></div>
      <div class="monitor-foot">
        <span>Hover to tilt · Press to squash · Release for the wave</span>
        <span class="shortcuts"><kbd>1</kbd>–<kbd>8</kbd> channel · <kbd>G</kbd> grid · <kbd>R</kbd> shuffle</span>
      </div>
    </section>

    <aside class="rack" data-section="rack">
      <div class="module">
        <h2 class="module-head"><span>Readout</span></h2>
        <div class="lcd">
          <div class="lcd-row"><span>CHANNEL</span><span id="lcd-ch"></span></div>
          <div class="lcd-name" id="lcd-name"></div>
          <div class="lcd-row"><span>MOTION</span><span id="lcd-motion"></span></div>
          <div class="lcd-row"><span>PRESSES</span><span id="lcd-presses"></span></div>
          <div class="lcd-row"><span>STATE</span><span id="lcd-state"></span></div>
          <div class="lcd-status" id="lcd-status" role="status">READY</div>
        </div>
      </div>
      <div class="module">
        <h2 class="module-head"><span>Signal</span><small>live</small></h2>
        <div class="meters">
          <div class="meter"><span>Hover</span><div class="bar" id="m-hover" aria-hidden="true"></div></div>
          <div class="meter"><span>Press</span><div class="bar" id="m-press" aria-hidden="true"></div></div>
          <div class="meter"><span>Wave</span><div class="bar" id="m-wave" aria-hidden="true"></div></div>
        </div>
      </div>
      <div class="module">
        <h2 class="module-head"><span><b>06</b>Scene</span></h2>
        <div class="knobs" data-group="scene"></div>
        <div class="backdrop-row">
          <div>
            <span class="field-label" id="bd-label">Backdrop</span>
            <div class="segs" id="backdrop" role="radiogroup" aria-labelledby="bd-label"></div>
          </div>
          <div class="wells">
            <label class="well"><input type="color" id="bgA" />Base</label>
            <label class="well"><input type="color" id="bgB" />Glow A</label>
            <label class="well"><input type="color" id="bgC" />Glow B</label>
          </div>
        </div>
      </div>
    </aside>
  </div>

  <nav class="bank" id="bank" data-section="bank" aria-label="Channels"></nav>

  <div class="modules" data-section="modules">
    <section class="module m-label">
      <h2 class="module-head"><span><b>01</b>Label</span><small>all channels</small></h2>
      <div class="stack">
        <div>
          <label class="field-label" for="text">Text</label>
          <input id="text" class="lcd-input" type="text" maxlength="40" spellcheck="false" value="Get started" />
        </div>
        <div>
          <span class="field-label" id="icon-label">Icon</span>
          <div class="segs icons" id="icons" role="radiogroup" aria-labelledby="icon-label"></div>
        </div>
        <div class="split">
          <div>
            <span class="field-label" id="side-label">Icon side</span>
            <div class="segs" id="side" role="radiogroup" aria-labelledby="side-label"></div>
          </div>
          <div>
            <label class="field-label" for="font">Typeface <span style="letter-spacing:0; text-transform:none; color: var(--dim)">· this channel</span></label>
            <select id="font" class="select"></select>
          </div>
        </div>
      </div>
    </section>

    <section class="module m-motion">
      <h2 class="module-head"><span><b>02</b>Motion</span><small id="motion-note"></small></h2>
      <div class="motion-grid">
        <div class="motion-keys">
          <div>
            <span class="field-label" id="hover-label">Hover</span>
            <div class="keyrow" id="hover" role="radiogroup" aria-labelledby="hover-label"></div>
          </div>
          <div>
            <span class="field-label" id="click-label">Click</span>
            <div class="keyrow" id="click" role="radiogroup" aria-labelledby="click-label"></div>
          </div>
        </div>
        <div class="knobs" data-group="motion"></div>
      </div>
    </section>

    <section class="module m-shape">
      <h2 class="module-head"><span><b>03</b>Shape</span></h2>
      <div class="knobs" data-group="shape"></div>
    </section>

    <section class="module m-glass">
      <h2 class="module-head"><span><b>04</b>Glass</span><small>double-click a knob to reset it</small></h2>
      <div class="knobs" data-group="glass"></div>
    </section>

    <section class="module m-liquid">
      <h2 class="module-head"><span><b>05</b>Liquid</span></h2>
      <div class="knobs" data-group="liquid"></div>
    </section>
  </div>
</main>

<p class="foot" data-section="footer"><span>Drag a knob up or down. Hold Shift for fine control. Arrow keys work too.</span><span>Buttons by <a href="https://buttonzilla.vercel.app" target="_blank" rel="noopener">ButtonZilla</a> · Shakuro</span></p>

<script type="importmap">
{ "imports": {
  "three": "https://cdn.jsdelivr.net/npm/three@0.170.0/build/three.module.js",
  "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.170.0/examples/jsm/"
} }
</script>
<script type="module">
import * as THREE from 'three';
import { RoomEnvironment } from 'three/addons/environments/RoomEnvironment.js';
import { EffectComposer } from 'three/addons/postprocessing/EffectComposer.js';
import { RenderPass } from 'three/addons/postprocessing/RenderPass.js';
import { UnrealBloomPass } from 'three/addons/postprocessing/UnrealBloomPass.js';
import { OutputPass } from 'three/addons/postprocessing/OutputPass.js';

// ================= params =================

const FONTS = [
  { name: 'Inter', axis: '100..900' },
  { name: 'Onest', axis: '100..900' },
  { name: 'Manrope', axis: '200..800' },
  { name: 'Unbounded', axis: '200..900' },
  { name: 'Geologica', axis: '100..900' },
  { name: 'Rubik', axis: '300..900' },
];

const DEFAULTS = {
  text: 'Shakuro.com', font: 'Inter', weight: 500, fontSize: 18, letterSpacing: 0.01, uppercase: false,
  icon: 'arrow', iconSide: 'right', textColor: '#0e0a1f', textHoverColor: '#3b1d8f',
  textDepth: 0.15, textGlow: 0, textShadow: 0.12,
  paddingX: 32, paddingY: 19, minWidth: 0, radius: 0.52, depth: 26, bevel: 8, smoothness: 10,
  color: '#f3efff', transmission: 1, ior: 1.45, thickness: 26, roughness: 0.32, metalness: 0,
  dispersion: 0.4, clearcoat: 0.6, clearcoatRoughness: 0.12, iridescence: 0, iridescenceIOR: 1.3,
  iridescenceThickness: 400, sheen: 0, sheenColor: '#ffffff', sheenRoughness: 0.5,
  attenuationColor: '#ffffff', attenuationDistance: 1000, specularIntensity: 1,
  emissive: '#000000', emissiveIntensity: 0,
  liquid: 0, liquidSpeed: 0.6, liquidScale: 1, liquidHover: 1.5, bulge: 0.35, bulgeRadius: 46,
  freedom: 1, tilt: 15, tiltMode: 'press', magnet: 0.12, lift: 14, hoverScale: 1.035, twist: 0,
  stretch: 0, stiffness: 170, damping: 0.72, float: 0, cursorLight: 0.6,
  pressDepth: 9, pressSquash: 0.04, pressTilt: 4, clickPop: 0.03, pressStiffness: 240, pressDamping: 0.7,
  clickFlash: 0, ripple: 0.6, rippleOn: 'release', rippleSpeed: 240, rippleWavelength: 57, rippleLife: 1, rippleReach: 170,
  backdrop: 'aurora', bgA: '#d6d0f3', bgB: '#ff8fd0', bgC: '#9a74ff', backdropMotion: 0.3,
  patternScale: 1, patternAngle: 0, patternWeight: 0.5, patternSeed: 0,
  shadow: 0.35, shadowSoftness: 1, keyLight: 1.6, envIntensity: 1, envRotation: 0, exposure: 1,
  bloom: 0.2, bloomThreshold: 0.9, zoom: 1,
};

const hoverMotion = (v) => ({
  tilt: 15, tiltMode: 'press', magnet: 0.12, lift: 14, hoverScale: 1.035,
  twist: 0, stretch: 0, stiffness: 170, damping: 0.72, ...v,
});
const HOVER_PRESETS = [
  { id: 'soft', name: 'Soft', values: hoverMotion({}) },
  { id: 'still', name: 'Still', values: hoverMotion({ tilt: 5, magnet: 0.03, lift: 6, hoverScale: 1.015, stiffness: 210, damping: 1 }) },
  { id: 'magnetic', name: 'Magnetic', values: hoverMotion({ tilt: 10, tiltMode: 'lean', magnet: 0.32, lift: 18, hoverScale: 1.04, stretch: 0.03, stiffness: 150, damping: 0.66 }) },
  { id: 'springy', name: 'Springy', values: hoverMotion({ tilt: 18, magnet: 0.14, lift: 18, hoverScale: 1.06, twist: 3, stiffness: 220, damping: 0.28 }) },
  { id: 'elastic', name: 'Elastic', values: hoverMotion({ tilt: 8, tiltMode: 'lean', magnet: 0.2, lift: 12, hoverScale: 1.02, stretch: 0.12, stiffness: 130, damping: 0.42 }) },
  { id: 'playful', name: 'Playful', values: hoverMotion({ tilt: 14, tiltMode: 'lean', magnet: 0.18, lift: 22, hoverScale: 1.05, twist: 5, stretch: 0.04, stiffness: 180, damping: 0.45 }) },
];
const clickMotion = (v) => ({
  pressDepth: 9, pressSquash: 0.04, pressTilt: 4, clickPop: 0.03, pressStiffness: 240, pressDamping: 0.7,
  clickFlash: 0, ripple: 0.6, rippleOn: 'release', rippleSpeed: 240, rippleWavelength: 57, rippleLife: 1, rippleReach: 170, ...v,
});
const CLICK_PRESETS = [
  { id: 'soft', name: 'Soft', values: clickMotion({}) },
  { id: 'firm', name: 'Firm', values: clickMotion({ pressDepth: 5, pressSquash: 0.01, pressTilt: 2, clickPop: 0, pressStiffness: 420, pressDamping: 0.9, ripple: 0.25, rippleSpeed: 320, rippleWavelength: 40, rippleLife: 0.6, rippleReach: 120 }) },
  { id: 'deep', name: 'Deep', values: clickMotion({ pressDepth: 22, pressSquash: 0.06, pressTilt: 7, clickPop: 0.02, pressStiffness: 200, pressDamping: 0.78, ripple: 0.5, rippleSpeed: 200, rippleWavelength: 70, rippleLife: 1.2 }) },
  { id: 'squishy', name: 'Squishy', values: clickMotion({ pressDepth: 12, pressSquash: 0.14, pressTilt: 5, clickPop: 0.06, pressStiffness: 180, pressDamping: 0.34, ripple: 1, rippleSpeed: 200, rippleWavelength: 70, rippleLife: 1.4, rippleReach: 210 }) },
  { id: 'pop', name: 'Pop', values: clickMotion({ pressDepth: 6, pressSquash: 0.05, pressTilt: 2, clickPop: 0.12, pressStiffness: 320, pressDamping: 0.45, clickFlash: 0.6, ripple: 0.4, rippleSpeed: 320, rippleWavelength: 50, rippleLife: 0.7, rippleReach: 150 }) },
  { id: 'splash', name: 'Splash', values: clickMotion({ pressTilt: 3, pressDamping: 0.6, clickFlash: 0.3, ripple: 1.3, rippleOn: 'press', rippleSpeed: 160, rippleWavelength: 80, rippleLife: 2.2, rippleReach: 320 }) },
];

const PRESETS = [
  { id: 'frosted', name: 'Frosted', swatch: ['#f3efff', '#9a74ff'], hover: 'soft', click: 'soft',
    desc: 'Soft frosted glass over a drifting aurora.', look: {} },
  { id: 'crystal', name: 'Crystal', swatch: ['#ffffff', '#8fcfff'], hover: 'soft', click: 'firm',
    desc: 'Clear, high-dispersion crystal with a crisp press.',
    look: { color: '#ffffff', roughness: 0.04, ior: 1.55, thickness: 30, dispersion: 0.9,
      clearcoat: 1, clearcoatRoughness: 0.12, depth: 30, bevel: 12, radius: 0.6,
      textColor: '#0f1626', textHoverColor: '#1d4ed8', textDepth: 0.1, textShadow: 0.06,
      backdrop: 'aurora', bgA: '#e8edf5', bgB: '#a9d8ff', bgC: '#cdbfff', backdropMotion: 0.2,
      shadow: 0.25, bloom: 0.1, cursorLight: 0.35 } },
  { id: 'amber', name: 'Amber', swatch: ['#ffd98f', '#e08a1e'], hover: 'elastic', click: 'squishy',
    desc: 'Warm resin pill that stretches toward the cursor.',
    look: { color: '#ffe7b8', roughness: 0.08, ior: 1.54, thickness: 44, dispersion: 0.3,
      attenuationColor: '#f2a43a', attenuationDistance: 150, clearcoat: 1, clearcoatRoughness: 0.08,
      liquid: 0.4, liquidSpeed: 0.4, liquidHover: 1, bulge: 0.3, depth: 30, bevel: 14, radius: 1,
      font: 'Onest', weight: 600, textColor: '#4a2604', textHoverColor: '#2b1400', textDepth: 0.12, textShadow: 0.06,
      backdrop: 'aurora', bgA: '#fff1dd', bgB: '#ffc978', bgC: '#ffa98a', backdropMotion: 0.2,
      shadow: 0.3, bloom: 0.1, cursorLight: 0.4 } },
  { id: 'jelly', name: 'Jelly', swatch: ['#ffc6d6', '#ff5c8a'], hover: 'springy', click: 'squishy',
    desc: 'Wobbly pink jelly with the label sunk inside.',
    look: { color: '#ffc6d6', roughness: 0.14, ior: 1.33, thickness: 40, dispersion: 0.2,
      attenuationColor: '#ff6b93', attenuationDistance: 110, clearcoat: 1, clearcoatRoughness: 0.06,
      liquid: 0.5, liquidSpeed: 0.9, liquidHover: 1.5, bulge: 0.5, bulgeRadius: 56, depth: 34, bevel: 16, radius: 1,
      font: 'Rubik', weight: 600, textColor: '#6a1030', textHoverColor: '#8c0f3c', textDepth: -0.25, textShadow: 0,
      backdrop: 'aurora', bgA: '#ffe9ef', bgB: '#ffb8cc', bgC: '#ffd9b0', backdropMotion: 0.3,
      shadow: 0.3, bloom: 0.1, cursorLight: 0.4 } },
  { id: 'bubble', name: 'Bubble', swatch: ['#c9f1ff', '#ffc9f5'], hover: 'playful', click: 'pop',
    desc: 'Iridescent soap bubble that floats and pops.',
    look: { color: '#ffffff', roughness: 0, ior: 1.12, thickness: 6, dispersion: 0.6,
      iridescence: 1, iridescenceIOR: 1.33, iridescenceThickness: 820, clearcoat: 1, clearcoatRoughness: 0.1,
      liquid: 0.6, liquidSpeed: 0.5, depth: 34, bevel: 17, radius: 1,
      textColor: '#1d2b4f', textHoverColor: '#5b21b6', textDepth: 0.15,
      backdrop: 'aurora', bgA: '#eaf3ff', bgB: '#a6e9ff', bgC: '#ffc0ef', backdropMotion: 0.4,
      envIntensity: 1.4, shadow: 0.12, float: 5, cursorLight: 0.3 } },
  { id: 'cobalt', name: 'Cobalt', swatch: ['#9dbbff', '#2a55e6'], hover: 'magnetic', click: 'pop',
    desc: 'Deep blue glass that follows the cursor.',
    look: { color: '#9dbbff', roughness: 0.16, ior: 1.5, thickness: 34, dispersion: 0.4,
      attenuationColor: '#2350e4', attenuationDistance: 80, clearcoat: 1, clearcoatRoughness: 0.08,
      depth: 28, bevel: 12, radius: 1,
      font: 'Manrope', weight: 700, textColor: '#ffffff', textHoverColor: '#ffffff', textDepth: 0.15, textShadow: 0.18,
      backdrop: 'aurora', bgA: '#e9eefb', bgB: '#aac4ff', bgC: '#dacdff', backdropMotion: 0.2,
      shadow: 0.35, bloom: 0.08, cursorLight: 0.4 } },
  { id: 'clay', name: 'Clay', swatch: ['#ffd7c2', '#e8896a'], hover: 'still', click: 'deep',
    desc: 'Matte, opaque clay with a deep, soft press.',
    look: { ripple: 0, pressSquash: 0.08,
      color: '#ffcfb8', transmission: 0, roughness: 0.82, metalness: 0, clearcoat: 0, dispersion: 0,
      sheen: 1, sheenColor: '#fff1e8', sheenRoughness: 0.6, specularIntensity: 0.4,
      depth: 28, bevel: 14, radius: 0.7, bulge: 0,
      font: 'Manrope', weight: 700, textColor: '#6b2a14', textHoverColor: '#3d1408', textDepth: 0.05, textShadow: 0.15,
      backdrop: 'solid', bgA: '#f3e3d8', shadow: 0.45, shadowSoftness: 1.4, bloom: 0, cursorLight: 0.5 } },
  { id: 'seaglass', name: 'Sea glass', swatch: ['#dcf5ea', '#3fb48f'], hover: 'magnetic', click: 'deep',
    desc: 'Tumbled, frosty green glass from the shore.',
    look: { color: '#e2f7ee', roughness: 0.42, ior: 1.5, thickness: 40, dispersion: 0.2,
      attenuationColor: '#36b48c', attenuationDistance: 120, clearcoat: 0.5, clearcoatRoughness: 0.25,
      depth: 26, bevel: 10, radius: 0.45,
      font: 'Geologica', weight: 500, textColor: '#0d3b2c', textHoverColor: '#04261a', textDepth: 0.12, textShadow: 0.08,
      backdrop: 'aurora', bgA: '#e7f4ee', bgB: '#a3e4c8', bgC: '#bcd9ff', backdropMotion: 0.2,
      shadow: 0.3, bloom: 0.05, cursorLight: 0.45 } },
];

const ICON_CHOICES = [['none', 'None'], ['arrow', 'Arrow'], ['external', 'External link'], ['plus', 'Plus'], ['check', 'Check'], ['spark', 'Spark'], ['heart', 'Heart']];
const GLYPH_SVG = {
  none: '<circle cx="12" cy="12" r="7"/><path d="M7.1 16.9l9.8-9.8"/>',
  arrow: '<path d="M5 12h14"/><path d="M13 6l6 6-6 6"/>',
  external: '<path d="M7 17L17 7"/><path d="M9 7h8v8"/>',
  plus: '<path d="M12 5v14"/><path d="M5 12h14"/>',
  check: '<path d="M5 12.5l4.5 4.5L19 7"/>',
  heart: '<path d="M12 19.5C6.5 15.8 4 13 4 9.6 4 7.3 5.8 5.5 8.1 5.5c1.6 0 3 .9 3.9 2.3.9-1.4 2.3-2.3 3.9-2.3 2.3 0 4.1 1.8 4.1 4.1 0 3.4-2.5 6.2-8 9.9z" fill="currentColor" stroke="none"/>',
  spark: '<path d="M12 3.5c.7 4.6 3.9 7.8 8.5 8.5-4.6.7-7.8 3.9-8.5 8.5-.7-4.6-3.9-7.8-8.5-8.5 4.6-.7 7.8-3.9 8.5-8.5z"/>',
};
const svgIcon = (name) => `<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">${GLYPH_SVG[name] ?? ''}</svg>`;

// ================= button scene =================

const BACK = 140;
const FOV = 30;
const LABEL_MAX_SIDE = 4096;

const safeValue = (key, v) => (v === undefined ? DEFAULTS[key] : v);
function safeConfig(config) {
  const out = {};
  for (const k in config) if (k in DEFAULTS) out[k] = config[k];
  return out;
}

const smooth = THREE.MathUtils.smoothstep;
function knee(x, limit) {
  const a = Math.abs(x);
  const k = limit * 0.7;
  return a <= k ? x : Math.sign(x) * (k + (limit - k) * Math.tanh((a - k) / (limit - k)));
}
const toLinear = (u) => (u <= 0.04045 ? u / 12.92 : ((u + 0.055) / 1.055) ** 2.4);
const luminance = (r, g, b) => 0.2126 * toLinear(r) + 0.7152 * toLinear(g) + 0.0722 * toLinear(b);
const luminanceOf = (col) => 0.2126 * col.r + 0.7152 * col.g + 0.0722 * col.b;
const contrast = (a, b) => (Math.max(a, b) + 0.05) / (Math.min(a, b) + 0.05);

const fontLinks = new Map();
function loadFont(family, weight, text) {
  const spec = FONTS.find((f) => f.name === family);
  if (spec && !fontLinks.has(family)) {
    fontLinks.set(family, new Promise((resolve) => {
      const link = document.createElement('link');
      link.rel = 'stylesheet';
      link.href = `https://fonts.googleapis.com/css2?family=${family.replace(/ /g, '+')}:wght@${spec.axis}&display=swap`;
      link.onload = link.onerror = resolve;
      document.head.appendChild(link);
    }));
  }
  return (fontLinks.get(family) ?? Promise.resolve())
    .then(() => document.fonts.load(`${weight} 32px "${family}"`, text || 'H'))
    .catch(() => {});
}

function axisSamples(h, inner, nFlat, nBand) {
  const out = [];
  const push = (v) => { if (!out.length || v - out[out.length - 1] > 1e-4) out.push(v); };
  for (let i = 0; i <= nBand; i++) push(-h + (h - inner) * (i / nBand));
  if (inner > 1e-4) for (let i = 1; i <= nFlat; i++) push(-inner + 2 * inner * (i / nFlat));
  for (let i = 1; i <= nBand; i++) push(inner + (h - inner) * (i / nBand));
  return out;
}

function slabGeometry(w, h, { radius, depth, bevel, segments }) {
  const hx = w / 2, hy = h / 2;
  const hz = Math.max(depth / 2, 0.5);
  const R = Math.min(radius, hy, hx);
  const rb = Math.max(0.5, Math.min(bevel, hz, hy, hx));
  const c = Math.max(R - rb, 0);
  const ix = Math.max(hx - rb - c, 0);
  const iy = Math.max(hy - rb - c, 0);
  const iz = Math.max(hz - rb, 0);
  const seg = Math.round(segments);
  const xs = axisSamples(hx, ix, Math.min(Math.ceil((2 * ix) / 5), 160), seg + 2);
  const ys = axisSamples(hy, iy, Math.min(Math.ceil((2 * iy) / 5), 60), seg + 2);
  const zs = axisSamples(hz, iz, Math.min(Math.ceil((2 * iz) / 6), 10), seg);
  const pos = [], nor = [], uv = [], idx = [];

  const project = (x, y, z, fn) => {
    const kx = THREE.MathUtils.clamp(x, -ix, ix);
    const ky = THREE.MathUtils.clamp(y, -iy, iy);
    const dx = x - kx, dy = y - ky;
    const L = Math.hypot(dx, dy);
    let cx = x, cy = y;
    if (L > c) { cx = kx + (dx / L) * c; cy = ky + (dy / L) * c; }
    const cz = THREE.MathUtils.clamp(z, -iz, iz);
    let nx = x - cx, ny = y - cy, nz = z - cz;
    let nl = Math.hypot(nx, ny, nz);
    if (nl < 1e-6) { [nx, ny, nz] = fn; nl = 1; }
    nx /= nl; ny /= nl; nz /= nl;
    pos.push(cx + nx * rb, cy + ny * rb, cz + nz * rb);
    nor.push(nx, ny, nz);
    uv.push(x / w + 0.5, y / h + 0.5);
  };

  const faces = [
    { n: [0, 0, 1], A: xs, B: ys, p: (a, b) => [a, b, hz] },
    { n: [0, 0, -1], A: xs, B: ys, p: (a, b) => [a, b, -hz] },
    { n: [1, 0, 0], A: zs, B: ys, p: (a, b) => [hx, b, a] },
    { n: [-1, 0, 0], A: zs, B: ys, p: (a, b) => [-hx, b, a] },
    { n: [0, 1, 0], A: xs, B: zs, p: (a, b) => [a, hy, b] },
    { n: [0, -1, 0], A: xs, B: zs, p: (a, b) => [a, -hy, b] },
  ];
  for (const f of faces) {
    const base = pos.length / 3;
    const na = f.A.length, nb = f.B.length;
    for (let j = 0; j < nb; j++) for (let i = 0; i < na; i++) {
      const [x, y, z] = f.p(f.A[i], f.B[j]);
      project(x, y, z, f.n);
    }
    const p0 = f.p(f.A[0], f.B[0]), p1 = f.p(f.A[1], f.B[0]), p2 = f.p(f.A[0], f.B[1]);
    const u = [p1[0] - p0[0], p1[1] - p0[1], p1[2] - p0[2]];
    const v = [p2[0] - p0[0], p2[1] - p0[1], p2[2] - p0[2]];
    const cr = [u[1] * v[2] - u[2] * v[1], u[2] * v[0] - u[0] * v[2], u[0] * v[1] - u[1] * v[0]];
    const flip = cr[0] * f.n[0] + cr[1] * f.n[1] + cr[2] * f.n[2] < 0;
    for (let j = 0; j < nb - 1; j++) for (let i = 0; i < na - 1; i++) {
      const a = base + j * na + i, b = a + 1, d = a + na, e = d + 1;
      if (flip) idx.push(a, d, b, b, d, e);
      else idx.push(a, b, d, b, e, d);
    }
  }
  const geo = new THREE.BufferGeometry();
  geo.setAttribute('position', new THREE.Float32BufferAttribute(pos, 3));
  geo.setAttribute('normal', new THREE.Float32BufferAttribute(nor, 3));
  geo.setAttribute('uv', new THREE.Float32BufferAttribute(uv, 2));
  geo.setIndex(idx);
  geo.computeBoundingBox();
  geo.computeBoundingSphere();
  return { geo, front: hz, radius: Math.max(R, rb) };
}

const LIQUID_VERT = /* glsl */`
uniform float uTime;
uniform float uLiquid;
uniform float uLiqFreq;
uniform float uLiqSpeed;
uniform vec3 uCursor;
uniform float uBulge;
uniform float uBulgeR;
uniform vec4 uRipple;
uniform vec4 uRippleShape;
uniform float uLiquidOn;
varying vec3 vLqLocal;
varying float vLqFront;

vec4 lq_perm(vec4 x) { return mod(((x * 34.0) + 1.0) * x, 289.0); }
float lq_noise(vec3 p) {
  vec3 a = floor(p);
  vec3 d = p - a;
  d = d * d * (3.0 - 2.0 * d);
  vec4 b = a.xxyy + vec4(0.0, 1.0, 0.0, 1.0);
  vec4 k1 = lq_perm(b.xyxy);
  vec4 k2 = lq_perm(k1.xyxy + b.zzww);
  vec4 c = k2 + a.zzzz;
  vec4 k3 = lq_perm(c);
  vec4 k4 = lq_perm(c + 1.0);
  vec4 o1 = fract(k3 * (1.0 / 41.0));
  vec4 o2 = fract(k4 * (1.0 / 41.0));
  vec4 o3 = o2 * d.z + o1 * (1.0 - d.z);
  vec2 o4 = o3.yw * d.x + o3.xz * (1.0 - d.x);
  return (o4.y * d.y + o4.x * (1.0 - d.y)) * 2.0 - 1.0;
}
float lq_field(vec3 p, float front) {
  float t = uTime * uLiqSpeed;
  vec3 q = p * uLiqFreq;
  float f = uLiquid * (lq_noise(q + vec3(0.0, t * 0.6, t)) * 0.7
                     + lq_noise(q * 2.3 + vec3(t * 0.8, 4.1, -t * 0.5)) * 0.3);
  vec2 dc = p.xy - uCursor.xy;
  f += uBulge * exp(-dot(dc, dc) / (uBulgeR * uBulgeR)) * front;
  if (uRipple.w != 0.0) {
    float d = length(p.xy - uRipple.xy);
    float age = uRipple.z;
    float k = uRippleShape.x;
    float edge = age * uRippleShape.y;
    float wave = sin(d * k - age * k * uRippleShape.y * 0.5) * exp(-age * uRippleShape.z) * exp(-d * uRippleShape.w)
               * (1.0 - smoothstep(edge, edge + 3.0 / k, d));
    f += uRipple.w * wave * front;
  }
  return f;
}
`;
const CURSOR_GLOW_PARS = /* glsl */`
uniform vec3 uCursor;
uniform float uGlow;
uniform float uGlowR;
varying vec3 vLqLocal;
varying float vLqFront;
`;
const CURSOR_GLOW = /* glsl */`
if (uGlow > 0.0) {
  vec2 gd = vLqLocal.xy - uCursor.xy;
  float pool = exp(-dot(gd, gd) / (uGlowR * uGlowR));
  totalEmissiveRadiance += mix(vec3(1.0), diffuseColor.rgb, 0.35) * uGlow * pool * (0.3 + 0.7 * vLqFront);
}
`;
const LIQUID_NORMAL = /* glsl */`
vec3 objectNormal = vec3( normal );
vec3 lqPos = position;
if (uLiquidOn > 0.5) {
  float front = smoothstep(-0.3, 0.7, normal.z);
  float f0 = lq_field(position, front);
  float e = 1.5;
  vec3 grad = vec3(
    lq_field(position + vec3(e, 0.0, 0.0), front) - f0,
    lq_field(position + vec3(0.0, e, 0.0), front) - f0,
    lq_field(position + vec3(0.0, 0.0, e), front) - f0) / e;
  grad -= normal * dot(normal, grad);
  lqPos = position + normal * f0;
  objectNormal = normalize(normal - grad);
}
`;

// backdrop: only the styles the presets use (aurora, solid) are kept
const BACKDROP_FRAG = /* glsl */`
uniform vec3 uA;
uniform vec3 uB;
uniform vec3 uC;
uniform float uTime;
uniform int uStyle;
uniform float uUnit;
uniform vec4 uBtn;
uniform vec3 uBtnShape;
uniform float uShadow;
uniform float uSoft;
varying vec2 vPos;

float sdRound(vec2 p, vec2 b, float r) {
  vec2 q = abs(p) - b + r;
  return length(max(q, 0.0)) + min(max(q.x, q.y), 0.0) - r;
}
float blob(vec2 p, vec2 c, float r) { vec2 d = (p - c) / r; return exp(-dot(d, d)); }

void main() {
  vec2 p = vPos;
  float t = uTime;
  vec3 col = uA;
  float u = uUnit;
  if (uStyle == 0) {
    col = mix(col, uB, 0.85 * blob(p, vec2(-0.9 * u + sin(t * 0.5) * 0.4 * u, 0.35 * u + cos(t * 0.4) * 0.25 * u), 0.75 * u));
    col = mix(col, uC, 0.85 * blob(p, vec2(0.85 * u + cos(t * 0.45) * 0.4 * u, -0.25 * u + sin(t * 0.6) * 0.3 * u), 0.8 * u));
    col = mix(col, mix(uB, uC, 0.5), 0.5 * blob(p, vec2(sin(t * 0.3) * 0.6 * u, -0.7 * u + cos(t * 0.35) * 0.2 * u), 0.55 * u));
    col = mix(col, uA, 0.35 * blob(p, vec2(cos(t * 0.25) * 0.3 * u, 0.6 * u), 0.5 * u));
  }
  float hgt = uBtnShape.y;
  vec2 sp = p - uBtn.xy + vec2(0.0, hgt * 0.1);
  float blur = (5.0 + hgt * 0.11) * uSoft;
  float d = sdRound(sp, uBtn.zw * (1.0 + hgt * 0.0006), uBtnShape.x);
  float a = (1.0 - smoothstep(-blur, blur * 1.6, d)) * uShadow * mix(1.0, 0.55, clamp((hgt - ${BACK.toFixed(1)}) / 60.0, 0.0, 1.0));
  col = mix(col, col * vec3(0.32, 0.28, 0.45), a);
  gl_FragColor = vec4(col, 1.0);
  #include <colorspace_fragment>
}
`;
const BACKDROP_STYLES = { aurora: 0, solid: 4 };

class Spring {
  constructor(v = 0) { this.x = v; this.v = 0; }
  step(target, dt, k, c) {
    const n = Math.max(1, Math.ceil(dt / (1 / 240)));
    const h = dt / n;
    for (let i = 0; i < n; i++) {
      this.v += (-k * (this.x - target) - c * this.v) * h;
      this.x += this.v * h;
    }
    return this.x;
  }
}

const GLYPHS = {
  external: { d: ['M7 17L17 7', 'M9 7h8v8'], stroke: true },
  heart: { d: ['M12 19.5C6.5 15.8 4 13 4 9.6 4 7.3 5.8 5.5 8.1 5.5c1.6 0 3 .9 3.9 2.3.9-1.4 2.3-2.3 3.9-2.3 2.3 0 4.1 1.8 4.1 4.1 0 3.4-2.5 6.2-8 9.9z'], fill: true },
};
function drawIcon(g, kind, x, y, s) {
  g.lineCap = 'round';
  g.lineJoin = 'round';
  g.lineWidth = s * 0.1;
  g.beginPath();
  if (kind === 'arrow') {
    g.moveTo(x + s * 0.08, y); g.lineTo(x + s * 0.92, y);
    g.moveTo(x + s * 0.58, y - s * 0.34); g.lineTo(x + s * 0.92, y); g.lineTo(x + s * 0.58, y + s * 0.34);
    g.stroke();
  } else if (kind === 'plus') {
    g.moveTo(x + s * 0.5, y - s * 0.4); g.lineTo(x + s * 0.5, y + s * 0.4);
    g.moveTo(x + s * 0.1, y); g.lineTo(x + s * 0.9, y);
    g.stroke();
  } else if (kind === 'check') {
    g.moveTo(x + s * 0.1, y + s * 0.02); g.lineTo(x + s * 0.4, y + s * 0.3); g.lineTo(x + s * 0.92, y - s * 0.32);
    g.stroke();
  } else if (kind === 'spark') {
    const cx = x + s * 0.5, r = s * 0.48, k = s * 0.09;
    g.moveTo(cx, y - r);
    g.quadraticCurveTo(cx + k, y - k, cx + r, y);
    g.quadraticCurveTo(cx + k, y + k, cx, y + r);
    g.quadraticCurveTo(cx - k, y + k, cx - r, y);
    g.quadraticCurveTo(cx - k, y - k, cx, y - r);
    g.fill();
  } else if (GLYPHS[kind]) {
    const gl = GLYPHS[kind];
    const w = 24, h = 24;
    const k = s / 16;
    g.save();
    g.translate(x + s / 2 - (w * k) / 2, y - (h * k) / 2);
    g.scale(k, k);
    g.lineWidth = (s * 0.1) / k;
    for (const d of gl.d) {
      const path = new Path2D(d);
      if (gl.fill) g.fill(path);
      if (gl.stroke) g.stroke(path);
    }
    g.restore();
  }
}

function measureLabel(cfg) {
  const text = cfg.uppercase ? cfg.text.toUpperCase() : cfg.text;
  const fs = cfg.fontSize;
  const font = `${cfg.weight} ${fs}px "${cfg.font}", system-ui, sans-serif`;
  const spacing = cfg.letterSpacing * fs;
  const g = document.createElement('canvas').getContext('2d');
  g.font = font;
  if ('letterSpacing' in g) g.letterSpacing = `${spacing}px`;
  const tw = text ? Math.max(g.measureText(text).width - spacing, 0) : 0;
  const cap = g.measureText('H').actualBoundingBoxAscent || fs * 0.72;
  const icon = cfg.icon !== 'none';
  const aw = icon ? fs * 0.86 : 0;
  const gap = icon && tw > 0 ? fs * 0.5 : 0;
  return { text, fs, font, spacing, tw, cap, aw, gap, total: tw + gap + aw };
}

function labelCanvas(w, h, scale, draw, blur = 0) {
  const cv = document.createElement('canvas');
  cv.width = Math.max(2, Math.ceil(w * scale));
  cv.height = Math.max(2, Math.ceil(h * scale));
  const g = cv.getContext('2d');
  g.scale(scale, scale);
  if (blur) g.filter = `blur(${blur * scale}px)`;
  g.fillStyle = g.strokeStyle = '#fff';
  draw(g);
  const tex = new THREE.CanvasTexture(cv);
  tex.colorSpace = THREE.NoColorSpace;
  tex.anisotropy = 8;
  return tex;
}

const GEOMETRY_KEYS = new Set(['text', 'font', 'weight', 'fontSize', 'letterSpacing', 'uppercase', 'icon', 'iconSide',
  'paddingX', 'paddingY', 'minWidth', 'radius', 'depth', 'bevel', 'smoothness', 'textDepth']);

class ButtonScene {
  constructor(container, config = {}) {
    this.container = container;
    this.cfg = { ...DEFAULTS, ...safeConfig(config) };
    this.onClick = null;

    const renderer = new THREE.WebGLRenderer({ antialias: true, powerPreference: 'high-performance' });
    renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
    renderer.toneMapping = THREE.NeutralToneMapping;
    Object.assign(renderer.domElement.style, { display: 'block', width: '100%', height: '100%', touchAction: 'pan-y' });
    container.appendChild(renderer.domElement);
    this.renderer = renderer;

    const scene = new THREE.Scene();
    this.scene = scene;
    const pmrem = new THREE.PMREMGenerator(renderer);
    scene.environment = pmrem.fromScene(new RoomEnvironment(), 0.04).texture;
    pmrem.dispose();

    this.camera = new THREE.PerspectiveCamera(FOV, 1, 10, 20000);
    this.view = { dist: 0 };

    this.key = new THREE.DirectionalLight(0xffffff, 1);
    this.key.position.set(-0.6, 1, 0.9);
    scene.add(this.key);

    this.time = { value: 0 };
    this.backdropMat = new THREE.ShaderMaterial({
      uniforms: {
        uA: { value: new THREE.Color() }, uB: { value: new THREE.Color() }, uC: { value: new THREE.Color() },
        uTime: { value: 0 }, uStyle: { value: 0 }, uUnit: { value: 300 },
        uBtn: { value: new THREE.Vector4() }, uBtnShape: { value: new THREE.Vector3() },
        uShadow: { value: 0 }, uSoft: { value: 1 },
      },
      vertexShader: 'varying vec2 vPos; void main() { vec4 w = modelMatrix * vec4(position, 1.0); vPos = w.xy; gl_Position = projectionMatrix * viewMatrix * w; }',
      fragmentShader: BACKDROP_FRAG,
    });
    const backdrop = new THREE.Mesh(new THREE.PlaneGeometry(40000, 40000), this.backdropMat);
    backdrop.position.z = -BACK;
    scene.add(backdrop);

    this.group = new THREE.Group();
    scene.add(this.group);
    this.liquid = {
      uTime: this.time,
      uLiquid: { value: 0 }, uLiqFreq: { value: 1 / 60 }, uLiqSpeed: { value: 1 },
      uCursor: { value: new THREE.Vector3() }, uBulge: { value: 0 }, uBulgeR: { value: 40 },
      uRipple: { value: new THREE.Vector4() }, uRippleShape: { value: new THREE.Vector4() }, uLiquidOn: { value: 0 },
      uGlow: { value: 0 }, uGlowR: { value: 40 },
    };
    this.material = new THREE.MeshPhysicalMaterial();
    this.material.onBeforeCompile = (shader) => {
      Object.assign(shader.uniforms, this.liquid);
      shader.vertexShader = LIQUID_VERT + shader.vertexShader
        .replace('#include <beginnormal_vertex>', LIQUID_NORMAL)
        .replace('#include <begin_vertex>', 'vec3 transformed = lqPos; vLqLocal = lqPos; vLqFront = smoothstep(-0.3, 0.7, normal.z);');
      shader.fragmentShader = CURSOR_GLOW_PARS + shader.fragmentShader
        .replace('#include <emissivemap_fragment>', '#include <emissivemap_fragment>\n' + CURSOR_GLOW);
    };
    this.glass = new THREE.Mesh(new THREE.BufferGeometry(), this.material);
    this.group.add(this.glass);
    this.label = new THREE.Group();
    this.group.add(this.label);
    this.size = { w: 0, h: 0, front: 0, radius: 0 };

    const rt = new THREE.WebGLRenderTarget(1, 1, { type: THREE.HalfFloatType, samples: 4 });
    this.composer = new EffectComposer(renderer, rt);
    this.composer.addPass(new RenderPass(scene, this.camera));
    this.bloomPass = new UnrealBloomPass(new THREE.Vector2(256, 256), 0.2, 0.5, 0.9);
    this.composer.addPass(this.bloomPass);
    const labelPass = new RenderPass(scene, this.camera);
    labelPass.clear = false;
    const renderLabel = labelPass.render.bind(labelPass);
    labelPass.render = (...args) => {
      this.camera.layers.set(1);
      renderLabel(...args);
      this.camera.layers.set(0);
    };
    this.composer.addPass(labelPass);
    this.composer.addPass(new OutputPass());

    this.pointer = { ndc: new THREE.Vector2(), inside: false, lx: 0, ly: 0 };
    this.hovered = false;
    this.pressed = false;
    this.hover = 0;
    this.press = 0;
    this.bulgeAmp = 0;
    this.ripple = { x: 0, y: 0, age: 99, amp: 0 };
    this.flash = 0;
    this.inkFix = { to: new THREE.Color(), rest: 0, hover: 0, restT: 0, hoverT: 0, due: 0 };
    this.springs = {
      rx: new Spring(), ry: new Spring(), rz: new Spring(), x: new Spring(), y: new Spring(), z: new Spring(), s: new Spring(1),
      stx: new Spring(), sty: new Spring(),
      pz: new Spring(), ps: new Spring(), sq: new Spring(), prx: new Spring(), pry: new Spring(),
    };
    this.raycaster = new THREE.Raycaster();
    this.plane = new THREE.Plane(new THREE.Vector3(0, 0, 1), 0);
    this.bindPointer();

    this.applyMaterial();
    this.rebuild();

    this.resizeObserver = new ResizeObserver(() => this.resize());
    this.resizeObserver.observe(container);
    this.onScreen = true;
    this.visibility = new IntersectionObserver(([e]) => { this.onScreen = e.isIntersecting; this.wake(); });
    this.visibility.observe(container);
    this.resize();
    this.lastFrame = 0;
    this.frame = this.frame.bind(this);
    this.raf = requestAnimationFrame(this.frame);
  }

  set(patch) {
    let geometry = false;
    for (const k in patch) {
      if (!(k in DEFAULTS)) continue;
      const v = safeValue(k, patch[k]);
      if (this.cfg[k] === v) continue;
      this.cfg[k] = v;
      if (GEOMETRY_KEYS.has(k)) geometry = true;
    }
    this.applyMaterial();
    this.inkFix.due = 0;
    this.wake();
    if (geometry || (this.sink < -0.02) !== this.labelEmbedded) this.rebuild();
  }

  labelSink() {
    const c = this.cfg;
    if (c.textDepth >= 0) return c.textDepth;
    const body = new THREE.Color(c.attenuationColor);
    const e = c.thickness / Math.max(c.attenuationDistance, 1);
    const pass = 0.2126 * body.r ** e + 0.7152 * body.g ** e + 0.0722 * body.b ** e;
    const clarity = c.transmission * (1 - c.metalness) * (1 - smooth(c.roughness, 0.25, 0.7)) * smooth(pass, 0.06, 0.3);
    return c.textDepth * smooth(clarity, 0.3, 0.75);
  }

  applyMaterial() {
    const c = this.cfg;
    const m = this.material;
    this.sink = this.labelSink();
    m.color.set(c.color);
    m.transmission = c.transmission;
    m.ior = c.ior;
    m.thickness = c.thickness;
    m.roughness = c.roughness;
    m.metalness = c.metalness;
    m.dispersion = c.dispersion;
    m.clearcoat = c.clearcoat;
    m.clearcoatRoughness = c.clearcoatRoughness;
    m.iridescence = c.iridescence;
    m.iridescenceIOR = c.iridescenceIOR;
    m.iridescenceThicknessRange = [100, c.iridescenceThickness];
    m.sheen = c.sheen;
    m.sheenColor.set(c.sheenColor);
    m.sheenRoughness = c.sheenRoughness;
    m.attenuationColor.set(c.attenuationColor);
    m.attenuationDistance = c.attenuationDistance >= 1000 ? Infinity : c.attenuationDistance;
    m.specularIntensity = c.specularIntensity;
    m.emissive.set(c.emissive);
    m.emissiveIntensity = c.emissiveIntensity;

    const u = this.backdropMat.uniforms;
    u.uA.value.set(c.bgA);
    u.uB.value.set(c.bgB);
    u.uC.value.set(c.bgC);
    u.uStyle.value = BACKDROP_STYLES[c.backdrop] ?? 0;
    u.uShadow.value = c.shadow;
    u.uSoft.value = c.shadowSoftness;
    this.scene.background = null;
    this.key.intensity = c.keyLight;
    this.scene.environmentIntensity = c.envIntensity;
    this.scene.environmentRotation.set(0, THREE.MathUtils.degToRad(c.envRotation), 0);
    this.renderer.toneMappingExposure = c.exposure;
    this.bloomPass.strength = c.bloom;
    this.bloomPass.threshold = c.bloomThreshold;
    this.bloomPass.enabled = c.bloom > 0.001;
    this.liquid.uLiqFreq.value = c.liquidScale / 60;
    this.liquid.uLiqSpeed.value = c.liquidSpeed;
    this.liquid.uBulgeR.value = c.bulgeRadius;
  }

  rebuild() {
    const token = (this.buildToken = (this.buildToken ?? 0) + 1);
    const c = this.cfg;
    const run = () => { if (token === this.buildToken) this.buildButton(); };
    if (this.fontReady === `${c.font}|${c.weight}`) { run(); return; }
    run();
    loadFont(c.font, c.weight, c.text).then(() => {
      this.fontReady = `${c.font}|${c.weight}`;
      run();
    });
  }

  buildButton() {
    const c = this.cfg;
    const L = measureLabel(c);
    const h = Math.round(c.fontSize * 1.2 + c.paddingY * 2);
    const w = Math.round(Math.max(c.minWidth, L.total + c.paddingX * 2, h));
    const R = c.radius * (h / 2);
    const { geo, front, radius } = slabGeometry(w, h, { radius: R, depth: c.depth, bevel: c.bevel, segments: c.smoothness });
    this.glass.geometry.dispose();
    this.glass.geometry = geo;
    this.size = { w, h, front, radius };
    this.labelLayout = L;
    this.buildLabel();
    this.wake();
  }

  buildLabel() {
    const c = this.cfg;
    const L = this.labelLayout;
    const { front } = this.size;
    const S = (this.labelScale = this.labelScaleFor());
    for (const m of this.label.children) { m.material.map?.dispose(); m.material.dispose(); m.geometry.dispose(); }
    this.label.clear();
    const pad = Math.ceil(L.fs * 0.6);
    const lh = L.fs * 2;
    const baseline = pad + lh / 2 + L.cap / 2;
    const drawText = (g) => {
      g.font = L.font;
      if ('letterSpacing' in g) g.letterSpacing = `${L.spacing}px`;
      g.textBaseline = 'alphabetic';
      g.fillText(L.text, pad, baseline);
    };
    const drawIconAt = (g, x) => drawIcon(g, c.icon, x, pad + lh / 2, L.aw);
    const plane = (pw) => new THREE.PlaneGeometry(pw + pad * 2, lh + pad * 2);

    const embedded = this.sink < -0.02;
    const z = embedded ? front * (1 + this.sink) * 0.92 : front + 0.6 + Math.max(this.sink, 0) * 22;
    const labelMat = (map) => new THREE.MeshBasicMaterial({
      map, color: 0xffffff, toneMapped: true,
      transparent: !embedded, alphaTest: embedded ? 0.5 : 0, alphaToCoverage: embedded,
      depthWrite: embedded, depthTest: embedded,
    });

    const x0 = -L.total / 2;
    const left = c.iconSide === 'left';
    const textX = left ? L.aw + L.gap : 0;
    const iconX = left ? 0 : L.tw + L.gap;
    if (L.tw > 0) {
      const text = new THREE.Mesh(plane(L.tw), labelMat(labelCanvas(L.tw + pad * 2, lh + pad * 2, S, drawText)));
      text.position.set(x0 + textX + L.tw / 2, 0, z);
      text.renderOrder = 2;
      if (!embedded) text.layers.enable(1);
      text.userData.role = 'ink';
      this.label.add(text);
    }
    if (L.aw) {
      const icon = new THREE.Mesh(plane(L.aw), labelMat(labelCanvas(L.aw + pad * 2, lh + pad * 2, S, (g) => drawIconAt(g, pad))));
      icon.position.set(x0 + iconX + L.aw / 2, 0, z);
      icon.renderOrder = 2;
      if (!embedded) icon.layers.enable(1);
      icon.userData.role = 'ink';
      icon.userData.icon = true;
      icon.userData.baseX = icon.position.x;
      icon.userData.slide = left ? -1 : 1;
      this.label.add(icon);
    }
    if (!embedded) {
      const sw = L.total;
      const shadowTex = labelCanvas(sw + pad * 2, lh + pad * 2, S, (g) => {
        g.save();
        g.translate(textX, 0);
        drawText(g);
        g.restore();
        if (L.aw) drawIconAt(g, pad + iconX);
      }, L.fs * 0.055);
      const shadow = new THREE.Mesh(plane(sw), new THREE.MeshBasicMaterial({ map: shadowTex, transparent: true, depthWrite: false, depthTest: false, color: 0x2a1660 }));
      shadow.position.set(0, -1.2, z - 4);
      shadow.renderOrder = 1;
      shadow.userData.role = 'shadow';
      this.label.add(shadow);
    }
    this.labelZ = z;
    this.labelEmbedded = embedded;
    this.labelBox = L.total > 0 ? { x: L.total / 2, y: L.cap / 2 + L.fs * 0.3 } : null;
  }

  labelScaleFor() {
    const L = this.labelLayout;
    if (!this.viewport || !L) return 4;
    const d = Math.max(this.fitDistance() - this.size.front, 1);
    const viewH = 2 * d * Math.tan(THREE.MathUtils.degToRad(FOV / 2));
    const density = ((this.viewport.h * this.renderer.getPixelRatio()) / viewH) * 1.15;
    const step = 2 ** (Math.ceil(Math.log2(density) * 3) / 3);
    const side = Math.max(L.total, L.fs * 2) + Math.ceil(L.fs * 0.6) * 2;
    return THREE.MathUtils.clamp(step, 1.5, LABEL_MAX_SIDE / side);
  }

  resize() {
    const w = Math.max(1, this.container.clientWidth);
    const h = Math.max(1, this.container.clientHeight);
    this.viewport = { w, h };
    this.renderer.setSize(w, h, false);
    this.composer.setPixelRatio(this.renderer.getPixelRatio());
    this.composer.setSize(w, h);
    this.bloomPass.resolution.set(w / 2, h / 2);
    this.camera.aspect = w / h;
    this.camera.updateProjectionMatrix();
    this.wake();
  }

  fitDistance() {
    const { w, h } = this.size;
    const vp = this.viewport;
    const viewH = Math.max(h * 3.6, (w * 1.7 * vp.h) / vp.w, 160) / this.cfg.zoom;
    return viewH / 2 / Math.tan(THREE.MathUtils.degToRad(FOV / 2));
  }

  bindPointer() {
    const el = this.renderer.domElement;
    const p = this.pointer;
    const toNdc = (e) => {
      const r = el.getBoundingClientRect();
      p.ndc.set(((e.clientX - r.left) / r.width) * 2 - 1, -((e.clientY - r.top) / r.height) * 2 + 1);
    };
    el.addEventListener('pointermove', (e) => { this.wake(); toNdc(e); p.inside = true; });
    el.addEventListener('pointerleave', () => { p.inside = false; this.pressed = false; this.wake(); });
    el.addEventListener('pointerdown', (e) => {
      this.wake();
      toNdc(e);
      p.inside = true;
      this.pick();
      if (this.hovered) this.pressAt(p.lx, p.ly);
    });
    el.addEventListener('pointerup', () => {
      this.wake();
      if (this.pressed && this.hovered) this.click(p.lx, p.ly);
      this.pressed = false;
    });
    el.addEventListener('pointercancel', () => { this.pressed = false; p.inside = false; this.wake(); });
  }

  tap() {
    this.wake(1);
    this.pressAt(0, 0);
    this.hover = Math.max(this.hover, 0.6);
    setTimeout(() => { this.pressed = false; this.click(0, 0); }, 140);
  }

  pressAt(x, y) {
    this.pressed = true;
    if (this.cfg.rippleOn === 'press') this.splash(x, y);
  }

  click(x, y) {
    const c = this.cfg;
    this.springs.ps.v += c.clickPop * Math.sqrt(c.pressStiffness) * 2.7;
    this.flash = 1;
    this.liquid.uCursor.value.set(x, y, this.size.front);
    if (c.rippleOn !== 'press') this.splash(x, y);
    this.onClick?.();
  }

  splash(x, y) { this.ripple = { x, y, age: 0, amp: this.cfg.ripple * 7 }; }

  pick() {
    const p = this.pointer;
    if (!p.inside) { this.hovered = false; return; }
    this.raycaster.setFromCamera(p.ndc, this.camera);
    const hit = this.raycaster.intersectObject(this.glass, false)[0];
    this.hovered = !!hit;
    const pt = new THREE.Vector3();
    if (this.raycaster.ray.intersectPlane(this.plane, pt)) { p.x = pt.x; p.y = pt.y; }
    if (hit) {
      const local = this.glass.worldToLocal(hit.point.clone());
      p.lx = local.x;
      p.ly = local.y;
    }
  }

  wake(seconds = 0.5) {
    this.busy = true;
    this.awake = Math.max(this.awake ?? 0, (this.time?.value ?? 0) + seconds);
  }

  idleInterval() {
    const c = this.cfg;
    const flows = c.liquid > 0 || c.float > 0;
    if (c.backdrop !== 'solid' && c.backdropMotion > 0) return flows ? 1 / 30 : 1 / 20;
    return flows ? 1 / 30 : Infinity;
  }

  settling(hv) {
    const near = (a, b, e = 0.002) => Math.abs(a - b) < e;
    const v = this.view;
    const fix = this.inkFix;
    const c = this.cfg;
    return Object.values(this.springs).some((s) => Math.abs(s.v) > 0.01)
      || !near(this.hover, hv) || !near(this.press, this.pressed ? 1 : 0)
      || !near(this.bulgeAmp, hv * c.bulge * 7 - (this.pressed ? Math.abs(c.bulge) * 9 : 0), 0.01)
      || this.flash > 0.002 || this.liquid.uRipple.value.w > 0
      || !near(v.dist, this.fitDistance(), v.dist * 1e-4)
      || !near(fix.rest, fix.restT) || !near(fix.hover, fix.hoverT);
  }

  frame(ms) {
    this.raf = requestAnimationFrame(this.frame);
    const now = ms / 1000;
    const interval = !this.onScreen ? Infinity : this.busy ? 1 / 60 : this.idleInterval();
    if (now - this.lastFrame < interval - 0.004) return;
    const dt = Math.min(now - this.lastFrame, 1 / 20);
    this.lastFrame = now;
    const c = this.cfg;
    this.time.value += dt;
    const t = this.time.value;

    this.pick();
    this.renderer.domElement.style.cursor = this.hovered ? 'pointer' : 'default';

    const ease = (v, target, rate) => v + (target - v) * (1 - Math.exp(-dt * rate));
    this.hover = ease(this.hover, this.hovered ? 1 : 0, 8);
    this.press = ease(this.press, this.pressed ? 1 : 0, 22);

    const k = c.stiffness;
    const damp = 2 * c.damping * Math.sqrt(k);
    const pk = c.pressStiffness;
    const pdamp = 2 * c.pressDamping * Math.sqrt(pk);
    const S = this.springs;
    const { w, h, front } = this.size;
    const free = c.freedom;
    const hv = this.hovered ? 1 : 0;
    const px = hv * THREE.MathUtils.clamp((this.pointer.x ?? 0) / (w / 2 || 1), -1, 1);
    const py = hv * THREE.MathUtils.clamp((this.pointer.y ?? 0) / (h / 2 || 1), -1, 1);
    const sign = c.tiltMode === 'lean' ? -1 : 1;
    const tilt = THREE.MathUtils.degToRad(c.tilt) * free;

    const aspect = Math.min(h / Math.max(w, 1), 1);
    const yawShare = 0.45 + 0.55 * aspect;
    const ry = S.ry.step(sign * px * tilt * yawShare, dt, k, damp);
    const rx = S.rx.step(-sign * py * tilt, dt, k, damp);
    const rz = S.rz.step(-px * THREE.MathUtils.degToRad(c.twist) * free, dt, k, damp);
    const ox = S.x.step(px * (w / 2) * c.magnet * free, dt, k, damp);
    const oy = S.y.step(py * (h / 2) * c.magnet * free, dt, k, damp);
    const stx = S.stx.step(px * c.stretch * free, dt, k, damp);
    const sty = S.sty.step(py * c.stretch * free, dt, k, damp);
    const lift = S.z.step(hv * c.lift * free, dt, k, damp);
    const hs = S.s.step(1 + hv * (c.hoverScale - 1), dt, k, damp);

    const pr = this.pressed ? 1 : 0;
    const pTilt = THREE.MathUtils.degToRad(c.pressTilt) * pr;
    const pry = S.pry.step(px * pTilt * yawShare, dt, pk, pdamp);
    const prx = S.prx.step(-py * pTilt, dt, pk, pdamp);
    const sink = S.pz.step(pr * c.pressDepth, dt, pk, pdamp);
    const ps = S.ps.step(-pr * c.pressSquash * 0.5, dt, pk, pdamp);
    const sq = S.sq.step(pr * c.pressSquash, dt, pk * 1.4, pdamp * 0.8);
    const sc = hs + ps;

    const floatY = Math.sin(t * 1.3) * c.float * (1 - this.hover);
    const reachX = knee(stx, 0.25);
    const reachY = knee(sty, 0.25);

    this.group.position.set(
      knee(ox + reachX * w * 0.25, w * 0.3),
      knee(oy + reachY * h * 0.25, h * 0.6) + floatY,
      knee(lift, 60) - knee(sink, Math.max(front * 2, 20)));
    this.group.rotation.set(
      knee(rx + prx + Math.sin(t * 0.9) * c.float * 0.004 * (1 - this.hover), 0.55),
      knee(ry + pry + Math.cos(t * 0.7) * c.float * 0.003 * (1 - this.hover), 0.55),
      knee(rz, 0.4));

    const scale = 1 + knee(sc - 1, 0.3);
    const sx = scale * (1 + sq * 0.5) * (1 + Math.abs(reachX) * 0.5);
    const sy = scale * (1 + sq * 0.25) * (1 + Math.abs(reachY) * 0.5 * aspect);
    this.group.scale.set(sx, sy, Math.max(scale * (1 - sq * 2.2), 0.3));

    const lq = this.liquid;
    this.bulgeAmp = ease(this.bulgeAmp, hv * c.bulge * 7 - (this.pressed ? Math.abs(c.bulge) * 9 : 0), 10);
    this.ripple.age += dt;
    const fade = 2 / Math.max(c.rippleLife, 0.05);
    const flow = c.liquid * (1 + c.liquidHover * this.hover);
    const wave = this.ripple.age * fade < 5 ? this.ripple.amp : 0;
    const room = Math.min(front, h / 2) * 0.6;
    const fit = Math.min(1, room / Math.max(flow + Math.abs(this.bulgeAmp) + wave, 1e-6));
    lq.uLiquid.value = flow * fit;
    lq.uBulge.value = this.bulgeAmp * fit;
    if (this.hovered) lq.uCursor.value.set(this.pointer.lx, this.pointer.ly, front);
    lq.uRipple.value.set(this.ripple.x, this.ripple.y, this.ripple.age, wave * fit);
    lq.uRippleShape.value.set((Math.PI * 2) / Math.max(c.rippleWavelength, 4), c.rippleSpeed, fade, 1 / Math.max(c.rippleReach, 1));
    lq.uLiquidOn.value = (lq.uLiquid.value > 0.01 || Math.abs(this.bulgeAmp) > 0.01 || lq.uRipple.value.w > 0) ? 1 : 0;

    const fix = this.inkFix;
    fix.rest = ease(fix.rest, fix.restT, 6);
    fix.hover = ease(fix.hover, fix.hoverT, 6);
    const ink = new THREE.Color(c.textColor).lerp(fix.to, fix.rest)
      .lerp(new THREE.Color(c.textHoverColor).lerp(fix.to, fix.hover), this.hover);
    ink.multiplyScalar(1 + c.textGlow * 2.5);
    let labelZ = this.labelZ;
    if (this.labelEmbedded) {
      labelZ = this.size.front * (1 + this.sink) * 0.92;
      const dent = lq.uLiquid.value + Math.max(0, -lq.uBulge.value) + lq.uRipple.value.w;
      labelZ = Math.max(Math.min(labelZ, this.size.front - dent - 1.5), -this.size.front * 0.5);
    }
    for (const m of this.label.children) {
      m.position.z = labelZ - (m.userData.role === 'shadow' ? 4 : 0);
      if (m.userData.role === 'ink') m.material.color.copy(ink);
      else { m.material.opacity = c.textShadow; m.material.color.set(c.textColor).multiplyScalar(0.6); }
      if (m.userData.icon) m.position.x = m.userData.baseX + (this.hover * 5 - this.press * 2) * m.userData.slide;
    }

    this.flash = ease(this.flash, 0, 7);
    lq.uGlow.value = c.cursorLight * 0.32 * this.hover + c.clickFlash * 0.5 * this.flash;
    lq.uGlowR.value = Math.max(h * 0.85, 36);

    const bu = this.backdropMat.uniforms;
    bu.uTime.value = t * c.backdropMotion;
    bu.uUnit.value = Math.max(w * 0.9, 220);
    bu.uBtn.value.set(this.group.position.x, this.group.position.y, (w / 2) * sx, (h / 2) * sy);
    bu.uBtnShape.value.set(this.size.radius * scale, BACK + this.group.position.z - front, 0);

    const v = this.view;
    const dist = this.fitDistance();
    v.dist = v.dist ? ease(v.dist, dist, 5) : dist;
    this.camera.position.set(0, 0, v.dist);
    this.camera.lookAt(0, 0, 0);

    this.composer.render();

    if (this.hover < 0.05 && !this.pressed && t >= fix.due) {
      fix.due = t + 0.4;
      this.checkInk();
    }
    this.busy = t < this.awake || this.settling(hv);

    if (!this.busy && this.labelLayout && this.labelScaleFor() !== this.labelScale) {
      this.buildLabel();
      this.wake(0.1);
    }
  }

  // keeps the label at readable contrast against whatever the glass shows
  checkInk() {
    const box = this.labelBox;
    const fix = this.inkFix;
    if (!box) { fix.restT = fix.hoverT = 0; return; }
    const c = this.cfg;
    const { w, h, front } = this.size;
    const edge = Math.max(c.bevel, 1) * 0.7 + 1;
    const pts = [];
    const sx = Math.min(box.x + c.paddingX * 0.5, w / 2 - edge);
    if (sx > box.x + 1) pts.push([sx, 0], [-sx, 0]);
    const sy = Math.min((box.y + h / 2 - edge) / 2, h / 2 - edge);
    if (sy > box.y + 1) for (const x of [-box.x * 0.6, 0, box.x * 0.6]) pts.push([x, sy], [x, -sy]);
    if (!pts.length) return;

    const gl = this.renderer.getContext();
    const cv = this.renderer.domElement;
    const px = new Uint8Array(4);
    const v = new THREE.Vector3();
    const lums = [];
    for (const [x, y] of pts) {
      v.set(x, y, front).applyMatrix4(this.glass.matrixWorld).project(this.camera);
      if (Math.abs(v.x) > 1 || Math.abs(v.y) > 1) continue;
      gl.readPixels(Math.round((v.x + 1) / 2 * (cv.width - 1)), Math.round((v.y + 1) / 2 * (cv.height - 1)), 1, 1, gl.RGBA, gl.UNSIGNED_BYTE, px);
      lums.push(luminance(px[0] / 255, px[1] / 255, px[2] / 255));
    }
    if (!lums.length) return;
    lums.sort((a, b) => a - b);
    const face = lums[lums.length >> 1];
    const white = (1.05) / (face + 0.05) >= (face + 0.05) / 0.05;
    fix.to.set(white ? '#ffffff' : '#000000');
    const min = this.labelEmbedded ? 4.5 : 4;
    const need = (hex) => {
      const ink = new THREE.Color(hex);
      const ok = (tt) => contrast(luminanceOf(ink.clone().lerp(fix.to, tt)), face) >= min;
      if (ok(0)) return 0;
      let lo = 0, hi = 1;
      for (let i = 0; i < 10; i++) { const mid = (lo + hi) / 2; if (ok(mid)) hi = mid; else lo = mid; }
      return hi;
    };
    fix.restT = need(c.textColor);
    fix.hoverT = need(c.textHoverColor);
  }
}


ButtonScene.prototype.dispose = function () {
  this.buildToken = NaN;
  cancelAnimationFrame(this.raf);
  this.resizeObserver.disconnect();
  this.visibility.disconnect();
  this.glass.geometry.dispose();
  this.material.dispose();
  for (const m of this.label.children) { m.material.map?.dispose(); m.material.dispose(); m.geometry.dispose(); }
  this.scene.environment?.dispose();
  this.composer.dispose?.();
  this.renderer.dispose();
  this.renderer.forceContextLoss();
  this.renderer.domElement.remove();
};

// ================= console =================

const $ = (s) => document.querySelector(s);
const pad = (n, w = 2) => String(n).padStart(w, '0');
const byId = (list, id) => list.find((x) => x.id === id);
const reduceMotion = matchMedia('(prefers-reduced-motion: reduce)').matches;
const calm = reduceMotion ? { backdropMotion: 0, float: 0, liquid: 0 } : {};

const HOVER_NOTES = {
  soft: 'Soft: a gentle tilt and lift', still: 'Still: barely moves', magnetic: 'Magnetic: follows the cursor',
  springy: 'Springy: overshoots and wobbles', elastic: 'Elastic: stretches toward you', playful: 'Playful: lifts and twists',
};
const CLICK_NOTES = {
  soft: 'shallow press', firm: 'stiff switch', deep: 'sinks deep', squishy: 'squash and jiggle', pop: 'swell and flash', splash: 'big slow wave',
};

const pct = (v) => `${Math.round(v * 100)}%`;
const spct = (v) => `${v > 0 ? '+' : ''}${Math.round(v * 100)}%`;
const num = (v) => `${+v.toFixed(1)}`;
const deg = (v) => `${Math.round(v)}°`;
const x2 = (v) => v.toFixed(2);
const KNOBS = {
  shape: [['radius', 'Corner', 0, 1, 0.01, pct], ['depth', 'Depth', 10, 60, 1, num], ['bevel', 'Bevel', 1, 20, 0.5, num]],
  glass: [['roughness', 'Frost', 0, 1, 0.01, pct], ['ior', 'IOR', 1, 2.33, 0.01, x2], ['dispersion', 'Prism', 0, 1, 0.01, pct],
          ['thickness', 'Thick', 0, 80, 1, num], ['clearcoat', 'Coat', 0, 1, 0.01, pct], ['iridescence', 'Irid', 0, 1, 0.01, pct]],
  liquid: [['liquid', 'Flow', 0, 1, 0.01, pct], ['bulge', 'Bulge', -1, 1, 0.01, spct], ['ripple', 'Wave', 0, 2, 0.01, pct]],
  motion: [['tilt', 'Tilt', 0, 30, 1, deg], ['pressDepth', 'Press', 0, 30, 1, num]],
  scene: [['bloom', 'Bloom', 0, 1, 0.01, pct], ['shadow', 'Shadow', 0, 1, 0.01, pct], ['exposure', 'Expose', 0.5, 1.6, 0.01, x2]],
};

// ---------- state ----------
const baseFor = (ch) => ({ ...byId(HOVER_PRESETS, ch.hover).values, ...byId(CLICK_PRESETS, ch.click).values, ...ch.preset.look });
const channels = PRESETS.map((p) => ({ preset: p, hover: p.hover, click: p.click, values: null, presses: 0, edited: false }));
for (const ch of channels) ch.values = baseFor(ch);
const shared = { text: 'Get started', icon: 'arrow', iconSide: 'right' };
let sel = PRESETS.findIndex((p) => p.id === 'amber');
let view = 'solo';
let scenes = [];
const val = (ch, k) => ch.values[k] ?? DEFAULTS[k];
const cfgFor = (i) => ({ ...DEFAULTS, ...channels[i].values, ...shared, ...calm, zoom: view === 'solo' ? 0.9 : 1.05 });
const active = () => (view === 'solo' ? scenes[0]?.scene : scenes[sel]?.scene);

function apply(patch, { edit = true } = {}) {
  const ch = channels[sel];
  Object.assign(ch.values, patch);
  if (edit) ch.edited = true;
  active()?.set({ ...patch, ...calm });
  syncChannelChrome();
}
function applyShared(patch) {
  Object.assign(shared, patch);
  for (const s of scenes) s.scene?.set(patch);
}

// ---------- lamps + lcd ----------
const lampGl = $('#lamp-gl');
const lampSig = $('#lamp-sig');
let sigTimer;
function flashSig() {
  lampSig.dataset.state = 'on';
  clearTimeout(sigTimer);
  sigTimer = setTimeout(() => { lampSig.dataset.state = ''; }, 170);
}
const lcdStatus = $('#lcd-status');
let statusTimer;
function status(text) {
  lcdStatus.textContent = text;
  clearTimeout(statusTimer);
  statusTimer = setTimeout(() => { lcdStatus.textContent = 'READY'; }, 2200);
}

// ---------- monitor ----------
const screen = $('#screen');
function makeStage(label) {
  const el = document.createElement('div');
  el.className = 'stage';
  el.tabIndex = 0;
  el.setAttribute('role', 'button');
  el.setAttribute('aria-label', label);
  el.addEventListener('keydown', (e) => {
    if ((e.key === 'Enter' || e.key === ' ') && e.target === el) {
      e.preventDefault();
      scenes.find((s) => s.el === el)?.scene?.tap();
    }
  });
  return el;
}
function mount(el, i) {
  try {
    const scene = new ButtonScene(el, cfgFor(i));
    scene.onClick = () => pressed(view === 'solo' ? sel : i);
    lampGl.dataset.state = 'on';
    return scene;
  } catch (err) {
    console.error(err);
    lampGl.dataset.state = 'err';
    el.insertAdjacentHTML('beforeend', '<p class="fallback">WebGL is off in this browser, so the preview can’t run.</p>');
    return null;
  }
}
function buildView() {
  for (const s of scenes) s.scene?.dispose();
  scenes = [];
  screen.textContent = '';
  screen.dataset.view = view;
  if (view === 'solo') {
    const el = makeStage('');
    screen.append(el);
    scenes.push({ el, scene: mount(el, sel) });
  } else {
    channels.forEach((ch, i) => {
      const cell = document.createElement('div');
      cell.className = 'cell';
      cell.innerHTML = `<span class="tag"><b>${pad(i + 1)}</b>${ch.preset.name}</span>`;
      const el = makeStage(`${ch.preset.name} button. Press Enter to click it.`);
      cell.prepend(el);
      cell.addEventListener('pointerdown', () => { if (sel !== i) select(i); });
      el.addEventListener('focus', () => { if (sel !== i) select(i); });
      screen.append(cell);
      scenes.push({ el, cell, scene: mount(el, i) });
    });
  }
  syncChannelChrome();
}
function pressed(i) {
  channels[i].presses += 1;
  flashSig();
  if (i === sel) $('#lcd-presses').textContent = pad(channels[i].presses, 4);
}

// ---------- radio groups (keys) ----------
function radioGroup(root, items, current, onPick) {
  const buttons = items.map(({ value, label, html, led }) => {
    const b = document.createElement('button');
    b.type = 'button';
    b.className = 'key';
    b.dataset.value = value;
    b.setAttribute('role', 'radio');
    if (html) { b.innerHTML = html; b.setAttribute('aria-label', label); b.title = label; }
    else b.innerHTML = `${led ? '<i class="led" aria-hidden="true"></i>' : ''}${label}`;
    b.addEventListener('click', () => { current = value; sync(); onPick(value); });
    return b;
  });
  root.append(...buttons);
  root.addEventListener('keydown', (e) => {
    const step = { ArrowRight: 1, ArrowDown: 1, ArrowLeft: -1, ArrowUp: -1 }[e.key];
    if (!step) return;
    e.preventDefault();
    const i = buttons.indexOf(document.activeElement);
    const next = buttons[(i + step + buttons.length) % buttons.length];
    next.focus();
    next.click();
  });
  function sync() {
    for (const b of buttons) {
      const on = b.dataset.value === current;
      b.setAttribute('aria-checked', String(on));
      b.tabIndex = on ? 0 : -1;
    }
  }
  sync();
  return { set(v) { current = v; sync(); } };
}

// ---------- knobs ----------
const C = 36, R = 27;
const pt = (t, r = R) => {
  const a = ((-135 + 270 * t) * Math.PI) / 180;
  return [C + r * Math.sin(a), C - r * Math.cos(a)];
};
function arc(t0, t1) {
  const a = Math.min(t0, t1), b = Math.max(t0, t1);
  if (b - a < 0.002) return '';
  const [x0, y0] = pt(a), [x1, y1] = pt(b);
  return `M${x0.toFixed(2)} ${y0.toFixed(2)} A${R} ${R} 0 ${(b - a) * 270 > 180 ? 1 : 0} 1 ${x1.toFixed(2)} ${y1.toFixed(2)}`;
}
const TICKS = Array.from({ length: 11 }, (_, i) => {
  const [ax, ay] = pt(i / 10, 31.5), [bx, by] = pt(i / 10, 34.5);
  return `<line x1="${ax.toFixed(2)}" y1="${ay.toFixed(2)}" x2="${bx.toFixed(2)}" y2="${by.toFixed(2)}"/>`;
}).join('');

function makeKnob([key, label, min, max, step, fmt]) {
  const wrap = document.createElement('div');
  wrap.className = 'knob';
  wrap.innerHTML = `
    <div class="dial" role="slider" tabindex="0" aria-label="${label}" aria-valuemin="${min}" aria-valuemax="${max}">
      <svg viewBox="0 0 72 72" aria-hidden="true"><g class="ticks">${TICKS}</g><path class="track" d="${arc(0, 1)}"/><path class="fill"/></svg>
      <span class="cap"><span class="mark"></span></span>
    </div>
    <span class="knob-label" aria-hidden="true">${label}</span>
    <output class="knob-val" aria-hidden="true"></output>`;
  const dial = wrap.querySelector('.dial');
  const fill = wrap.querySelector('.fill');
  const cap = wrap.querySelector('.cap');
  const out = wrap.querySelector('output');
  const t0 = min < 0 ? -min / (max - min) : 0;
  let value = NaN;
  const quantize = (v) => {
    v = Math.min(max, Math.max(min, v));
    return +(Math.round((v - min) / step) * step + min).toFixed(4);
  };
  function render(v) {
    value = v;
    const t = (v - min) / (max - min);
    fill.setAttribute('d', arc(t0, t));
    cap.style.transform = `rotate(${-135 + 270 * t}deg)`;
    out.textContent = fmt(v);
    dial.setAttribute('aria-valuenow', String(v));
    dial.setAttribute('aria-valuetext', fmt(v));
  }
  function commit(v) {
    v = quantize(v);
    if (v === value) return;
    render(v);
    apply({ [key]: v });
  }
  let drag = null;
  dial.addEventListener('pointerdown', (e) => {
    if (e.button !== 0) return;
    e.preventDefault();
    dial.focus();
    dial.setPointerCapture(e.pointerId);
    drag = { x: e.clientX, y: e.clientY, v: value };
    dial.classList.add('is-drag');
  });
  dial.addEventListener('pointermove', (e) => {
    if (!drag) return;
    const d = drag.y - e.clientY + (e.clientX - drag.x);
    commit(drag.v + (d / 220) * (max - min) * (e.shiftKey ? 0.2 : 1));
  });
  const end = () => { drag = null; dial.classList.remove('is-drag'); };
  dial.addEventListener('pointerup', end);
  dial.addEventListener('pointercancel', end);
  dial.addEventListener('keydown', (e) => {
    const big = (max - min) / 10;
    const d = { ArrowUp: step, ArrowRight: step, ArrowDown: -step, ArrowLeft: -step, PageUp: big, PageDown: -big }[e.key];
    if (d !== undefined) { e.preventDefault(); commit(value + d * (e.shiftKey ? 10 : 1)); }
    else if (e.key === 'Home') { e.preventDefault(); commit(min); }
    else if (e.key === 'End') { e.preventDefault(); commit(max); }
  });
  dial.addEventListener('dblclick', () => commit(baseFor(channels[sel])[key] ?? DEFAULTS[key]));
  return { key, el: wrap, render };
}
const knobs = [];
for (const group of document.querySelectorAll('[data-group]')) {
  for (const spec of KNOBS[group.dataset.group]) {
    const k = makeKnob(spec);
    group.append(k.el);
    knobs.push(k);
  }
}

// ---------- channel bank ----------
const bank = $('#bank');
const chanButtons = channels.map((ch, i) => {
  const b = document.createElement('button');
  b.type = 'button';
  b.className = 'chan';
  b.style.setProperty('--led', ch.preset.swatch[1]);
  b.setAttribute('aria-label', `Channel ${i + 1}: ${ch.preset.name}`);
  b.innerHTML = `<span class="chan-top"><span class="chan-num">CH ${pad(i + 1)}</span><i class="chan-led" aria-hidden="true"></i></span><span class="chan-name">${ch.preset.name}</span><span class="chan-edit" aria-hidden="true">EDIT</span>`;
  b.addEventListener('click', () => select(i));
  bank.append(b);
  return b;
});

// ---------- controls ----------
const viewRG = radioGroup($('#view'), [{ value: 'solo', label: 'Solo', led: true }, { value: 'grid', label: 'Grid', led: true }], view, setView);
function setView(v) {
  if (v === view) return;
  view = v;
  viewRG.set(v);
  buildView();
  status(v === 'grid' ? 'GRID: ALL 8 CHANNELS' : 'SOLO: ' + channels[sel].preset.name.toUpperCase());
}

const hoverRG = radioGroup($('#hover'), HOVER_PRESETS.map((p) => ({ value: p.id, label: p.name, led: true })), '', (id) => {
  channels[sel].hover = id;
  apply(byId(HOVER_PRESETS, id).values);
  refresh();
});
const clickRG = radioGroup($('#click'), CLICK_PRESETS.map((p) => ({ value: p.id, label: p.name, led: true })), '', (id) => {
  channels[sel].click = id;
  apply(byId(CLICK_PRESETS, id).values);
  refresh();
});
const backdropRG = radioGroup($('#backdrop'), [{ value: 'aurora', label: 'Aurora', led: true }, { value: 'solid', label: 'Solid', led: true }], '', (v) => apply({ backdrop: v }));

radioGroup($('#icons'), ICON_CHOICES.map(([value, label]) => ({ value, label, html: svgIcon(value) })), shared.icon, (v) => applyShared({ icon: v }));
radioGroup($('#side'), [{ value: 'left', label: 'Left', led: true }, { value: 'right', label: 'Right', led: true }], shared.iconSide, (v) => applyShared({ iconSide: v }));
$('#text').addEventListener('input', (e) => applyShared({ text: e.target.value }));

const fontSel = $('#font');
fontSel.innerHTML = FONTS.map((f) => `<option value="${f.name}">${f.name}</option>`).join('');
fontSel.addEventListener('change', () => apply({ font: fontSel.value }));

for (const id of ['bgA', 'bgB', 'bgC']) {
  $('#' + id).addEventListener('input', (e) => apply({ [id]: e.target.value }));
}

// ---------- selection + refresh ----------
function select(i) {
  sel = i;
  if (view === 'solo') scenes[0]?.scene?.set(cfgFor(i));
  refresh();
}
function syncChannelChrome() {
  const ch = channels[sel];
  chanButtons.forEach((b, i) => {
    b.setAttribute('aria-pressed', String(i === sel));
    b.dataset.edited = String(channels[i].edited);
  });
  for (const s of scenes) if (s.cell) s.cell.dataset.current = String(scenes.indexOf(s) === sel);
  if (view === 'solo' && scenes[0]) scenes[0].el.setAttribute('aria-label', `${ch.preset.name} button. Press Enter to click it.`);
  $('#hud').innerHTML = view === 'solo'
    ? `<b>CH ${pad(sel + 1)}</b> · ${ch.preset.name}`
    : `<b>Grid</b> · editing CH ${pad(sel + 1)} ${ch.preset.name}`;
  $('#lcd-state').textContent = ch.edited ? 'EDITED' : 'PRESET';
}
function refresh() {
  const ch = channels[sel];
  for (const k of knobs) k.render(val(ch, k.key));
  hoverRG.set(ch.hover);
  clickRG.set(ch.click);
  backdropRG.set(val(ch, 'backdrop') === 'solid' ? 'solid' : 'aurora');
  for (const id of ['bgA', 'bgB', 'bgC']) $('#' + id).value = val(ch, id);
  fontSel.value = val(ch, 'font');
  $('#motion-note').textContent = `${HOVER_NOTES[ch.hover]} · ${CLICK_NOTES[ch.click]}`;
  $('#lcd-ch').textContent = `${pad(sel + 1)} / ${pad(channels.length)}`;
  $('#lcd-name').textContent = ch.preset.name;
  $('#lcd-motion').textContent = `${ch.hover} / ${ch.click}`.toUpperCase();
  $('#lcd-presses').textContent = pad(ch.presses, 4);
  syncChannelChrome();
}

// ---------- actions ----------
function shuffle() {
  const ch = channels[sel];
  const pick = (a) => a[Math.floor(Math.random() * a.length)];
  const r = (a, b) => +(a + Math.random() * (b - a)).toFixed(2);
  const look = pick(PRESETS);
  ch.hover = pick(HOVER_PRESETS).id;
  ch.click = pick(CLICK_PRESETS).id;
  ch.values = {
    ...byId(HOVER_PRESETS, ch.hover).values, ...byId(CLICK_PRESETS, ch.click).values, ...look.look,
    roughness: r(0, 0.45), ior: r(1.15, 1.8), dispersion: r(0, 1), thickness: Math.round(r(12, 56)),
    radius: pick([0.45, 0.7, 1]), liquid: Math.random() < 0.5 ? 0 : r(0.2, 0.6), bulge: r(0, 0.6),
    iridescence: Math.random() < 0.25 ? r(0.6, 1) : 0,
  };
  ch.edited = true;
  active()?.set(cfgFor(sel));
  refresh();
  status(`SHUFFLED · BASE ${look.name.toUpperCase()}`);
}
function reset() {
  const ch = channels[sel];
  ch.hover = ch.preset.hover;
  ch.click = ch.preset.click;
  ch.values = baseFor(ch);
  ch.edited = false;
  active()?.set(cfgFor(sel));
  refresh();
  status(`RESET · ${ch.preset.name.toUpperCase()}`);
}
async function copyJson() {
  const cfg = { ...channels[sel].values, ...shared };
  const out = {};
  for (const k in cfg) {
    if (!(k in DEFAULTS) || cfg[k] === DEFAULTS[k]) continue;
    out[k] = typeof cfg[k] === 'number' ? +cfg[k].toFixed(3) : cfg[k];
  }
  try {
    await navigator.clipboard.writeText(JSON.stringify(out, null, 2));
    status(`JSON COPIED · ${Object.keys(out).length} KEYS`);
  } catch {
    status('CLIPBOARD BLOCKED');
  }
}
$('#shuffle').addEventListener('click', shuffle);
$('#reset').addEventListener('click', reset);
$('#copy').addEventListener('click', copyJson);

document.addEventListener('keydown', (e) => {
  if (e.metaKey || e.ctrlKey || e.altKey) return;
  if (e.target.closest('input, select, textarea, [role="slider"]')) return;
  if (/^[1-8]$/.test(e.key)) { select(+e.key - 1); return; }
  const k = e.key.toLowerCase();
  if (k === 'g') setView(view === 'solo' ? 'grid' : 'solo');
  else if (k === 'r') shuffle();
});

// ---------- meters ----------
const meters = ['hover', 'press', 'wave'].map((id) => {
  const bar = $('#m-' + id);
  bar.innerHTML = '<i></i>'.repeat(20);
  return { segs: [...bar.children], lit: -1 };
});
function tick() {
  requestAnimationFrame(tick);
  const s = active();
  let levels = [0, 0, 0];
  if (s) {
    const wave = s.ripple.amp > 0 ? Math.exp((-s.ripple.age * 2) / Math.max(s.cfg.rippleLife, 0.05)) : 0;
    levels = [s.hover, s.press, wave];
  }
  levels.forEach((v, k) => {
    const m = meters[k];
    const n = Math.round(Math.min(1, Math.max(0, v)) * 20);
    if (n === m.lit) return;
    m.lit = n;
    m.segs.forEach((seg, j) => seg.classList.toggle('on', j < n));
  });
}

refresh();
buildView();
requestAnimationFrame(tick);
</script>
</body>
</html>
```
