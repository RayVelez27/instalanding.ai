INSTALANDING.AI · Stage Light Launch Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Stage Light Launch Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/stage-light-launch-page

umbra-eclipse.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Stage Light Launch Page
  slug     stage-light-launch-page
  prompt   https://instalanding.ai/p/stage-light-launch-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/stage-light-launch-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of <style>: --void, --ice/--sky, --flare/--flare-2 (beam
            and sweep colour), --hair/--hair-2 (grid lines), --size (the stage scale; body font-size is
            3% of it), --display Archivo / --mono JetBrains Mono (Google Fonts); body.flare redefines
            the light tokens for the warm lamp
  sections  nav, hero, pitch, features, how-it-works, stats, faq, cta, footer
  scripts   one inline IIFE, no libraries: lamp toggle (cool/warm/off body classes), wordmark sweep
            gated by an IntersectionObserver, scroll-driven stage exit (--out) + letter split, card
            animation gating, demo access form, streamed quickstart output, comparison bars
  assets    none: all CSS (conic spotlights, ridge, grid frame, @property --p sweep) plus one inline SVG chevron

  ADAPTING
  - Recolour through the tokens: the lamp works by redefining them under body.flare, so hard-coded
    colours will not follow the warm light.
  - The hero exit is one value: --out (0 to 1) is written on .stage, .top and .spotlight across the
    180svh .stage-pin, whose -60svh margin lets the page rise behind it. Change the pin height and the
    exit timing changes with it.
  - The wordmark is split into per-letter spans at boot, and each letter's gradient offset (--ox/--bw)
    is re-measured after document.fonts.ready; change the word in both .hero h1s (the second is the
    aria-hidden glow copy).
  - Place stage children in % of the stage, not em: em resolves against the element's own font-size.
-->
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Umbra — the runtime that disappears</title>
<meta name="description" content="A fictional inference runtime, presented under a stage light: conic spotlights, a rising particle field, a hairline grid and a swept-gradient wordmark. One file, no images, no libraries." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
<style>
@property --p {
  syntax: "<percentage>";
  inherits: true;
  initial-value: 0%;
}

:root {
  --void: #05060f;
  --panel: #121521;
  --ice: #d8ecf8;
  --sky: #98c0ef;
  --steel: #9dc3f7;
  --edge: #c2ccff;
  --hair: rgba(186, 215, 247, 0.18);
  --hair-2: rgba(186, 215, 247, 0.36);
  --flare: #bad6f7;
  --flare-2: #98c0ef;
  --display: "Archivo", system-ui, sans-serif;
  --mono: "JetBrains Mono", ui-monospace, monospace;
  --ease: cubic-bezier(0.2, 0.8, 0.2, 1);
  --factor: min(600px, 80vh);
  --size: min(var(--factor), 80vw);
}
body.flare {
  --flare: #f5d87a;
  --flare-2: #d8a910;
  --steel: #f0d89a;
  --edge: #f3dda0;
  --hair: rgba(247, 228, 186, 0.2);
  --hair-2: rgba(247, 228, 186, 0.38);
}

* { box-sizing: border-box; margin: 0; padding: 0; -webkit-font-smoothing: antialiased; }
html { scroll-behavior: smooth; }
body {
  min-height: 100vh;
  background: var(--void) linear-gradient(0deg, rgba(216, 236, 248, 0.06), rgba(152, 192, 239, 0.06));
  color: var(--ice);
  font-family: var(--display);
  font-size: max(calc(var(--size) * 0.03), 13px);
  overflow-x: hidden;
}
button { font: inherit; color: inherit; background: none; border: 0; cursor: pointer; }
a { color: inherit; text-decoration: none; }
.sr { position: absolute; width: 1px; height: 1px; margin: -1px; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; }

/* The stage is pinned for the extra 80svh of its wrapper: the hero holds
   still while it comes apart. The negative margin lets the page below start
   rising behind it while the pieces are still falling, so there is no
   empty screen between the exit and the content. Everything in the stage
   reads one value, --out, which runs 0 → 1 across that pin. */
.stage-pin { position: relative; height: 180svh; margin-bottom: -60svh; }
.stage { position: sticky; top: 0; height: 100svh; min-height: 34em; overflow: hidden; isolation: isolate; }

.spotlight {
  position: fixed; inset: 0; overflow: hidden; pointer-events: none; z-index: 0;
  transition: opacity 0.8s ease-in-out;
  /* on the way out the beams retract up into the bulb */
  --t: clamp(0, calc((var(--out, 0) - 0.1) / 0.6), 1);
  opacity: calc(1 - var(--t));
}
.spotlight span { scale: 1 calc(1 - var(--t) * 0.9); }
.spotlight span {
  position: absolute; inset: 0; display: block; transform-origin: 50% 0;
  animation: drift 19s ease-in-out infinite;
}
.spotlight span:nth-child(2) { animation-duration: 23s; animation-delay: -4s; }
.spotlight span:nth-child(3) { animation-duration: 15s; animation-delay: -9s; }
.spotlight i {
  position: absolute; left: 0; right: 0; top: 3em; margin: 0 auto;
  display: block; width: 30em; height: max(42em, 86vh);
  border-radius: 0 0 50% 50%;
  transform-origin: 50% 0;
  background-image: conic-gradient(from 0deg at 50% -5%,
    transparent 45%,
    color-mix(in srgb, var(--flare) 30%, transparent) 49%,
    color-mix(in srgb, var(--flare) 52%, transparent) 50%,
    color-mix(in srgb, var(--flare) 30%, transparent) 51%,
    transparent 55%);
  filter: blur(10px);
  opacity: 0;
  animation: beam-in 2s var(--ease) forwards, flicker 21s ease-in-out 2s infinite reverse;
}
.spotlight span:nth-child(1) i { rotate: 20deg; animation: beam-in 2s var(--ease) forwards, flicker 17s ease-in-out 2s infinite; }
.spotlight span:nth-child(2) i { rotate: -20deg; animation: beam-in 2s var(--ease) forwards, flicker 14s ease-in-out 2s infinite; }
@keyframes beam-in { from { opacity: 0; scale: 0; } to { opacity: 0.5; scale: 1; } }
@keyframes drift {
  0%, 100% { transform: rotateZ(0deg) scale(1); }
  25% { transform: rotateZ(-1.6deg) scale(1.16); }
  50% { transform: rotateZ(2.2deg) scale(1.26); }
  75% { transform: rotateZ(-2deg) scale(1.12); }
}
@keyframes flicker {
  0%, 100% { opacity: 0.5; } 20% { opacity: 0.64; } 40% { opacity: 0.4; }
  60% { opacity: 0.64; } 80% { opacity: 0.42; }
}
@keyframes fade { to { opacity: 1; } }

.top {
  position: fixed; inset: 0 0 auto; z-index: 60;
  display: flex; align-items: center; justify-content: center;
  padding: 2em; color: var(--flare);
  opacity: 0; translate: 0 -1em;
  animation: fade 2s ease-in 2s forwards, rise 1.4s var(--ease) 2s forwards;
}
@keyframes rise { to { translate: 0; } }
.wordmark, .topcta {
  position: absolute; font-size: 1em; font-weight: 800; letter-spacing: 0.02em;
  color: inherit; background: none; border: 0; padding: 0;
  opacity: 0.6; transition: opacity 0.2s ease; cursor: pointer;
}
.wordmark { left: 2em; }
.topcta { right: 2em; font-weight: 600; }
.wordmark:hover, .topcta:hover { opacity: 1; text-shadow: 0 2px 16px color-mix(in srgb, var(--flare) 60%, transparent); }
.topcta:focus-visible, .wordmark:focus-visible { outline: 2px solid var(--flare); outline-offset: 5px; }
.lamp {
  width: 1.8em; height: 1.8em; border-radius: 50%; background: #000;
  box-shadow: 0 0 1em 0 var(--flare-2);
  transition: box-shadow 0.8s ease-in-out;
}
.lamp:hover { box-shadow: -0.3em 0.1em 0.3em 0 var(--flare-2), 0 0 1.6em 0 var(--flare-2); }
.lamp:focus-visible { outline: 2px solid var(--flare); outline-offset: 6px; }
/* the bulb follows its light out: rises, shrinks, goes dark */
.lamp {
  --t: clamp(0, calc((var(--out, 0) - 0.3) / 0.45), 1);
  translate: 0 calc(var(--t) * -2.2em);
  scale: calc(1 - var(--t) * 0.7);
  opacity: calc(1 - var(--t));
}
.top.lampgone .lamp { visibility: hidden; }
/* past the hero the bar stays put, on a backdrop so copy can pass under it */
.top::before {
  content: ""; position: absolute; inset: 0; z-index: -1; pointer-events: none;
  background: color-mix(in srgb, var(--void) 72%, transparent);
  -webkit-backdrop-filter: blur(14px); backdrop-filter: blur(14px);
  border-bottom: 1px solid var(--hair);
  opacity: 0; transition: opacity 0.4s ease;
}
.top.past::before { opacity: 1; }
body.out .spotlight { opacity: 0; }
body.out .lamp {
  box-shadow: inset 0 0 0 1px rgba(194, 204, 255, 0.22);
  background: #07080e;
}
body.out .lamp:hover { box-shadow: inset 0 0 0 1px rgba(194, 204, 255, 0.45); }

.pill {
  position: absolute; right: 2em;
  width: 9.4em; height: 2.4em; border-radius: 20em;
  border: 1px solid rgba(194, 204, 255, 0.2);
  background: var(--panel); color: var(--steel);
  white-space: nowrap; overflow: hidden;
}
.pill::before {
  content: ""; position: absolute; inset: 0; border-radius: inherit;
  background: radial-gradient(farthest-side at 50% 100%, var(--edge), transparent);
  opacity: 0.1; transition: opacity 0.4s var(--ease);
}
.pill:hover::before { opacity: 0.3; }
.pill span.label {
  position: relative; z-index: 2; font-size: 1.05em; font-weight: 600;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.pill .glow {
  --w: 1px; --loop: 24s;
  position: absolute; inset: calc(var(--w) * -1); border-radius: 50px;
  border: var(--w) solid transparent; pointer-events: none;
  -webkit-mask: linear-gradient(transparent, transparent), linear-gradient(#fff, #fff);
  mask: linear-gradient(transparent, transparent), linear-gradient(#fff, #fff);
  -webkit-mask-clip: padding-box, border-box; mask-clip: padding-box, border-box;
  -webkit-mask-composite: source-in, xor; mask-composite: intersect;
}
.pill:hover .glow { --loop: 2s; }
.pill .glow::before, .pill .glow::after {
  content: ""; position: absolute; display: inline-block; height: 100%; aspect-ratio: 1;
  offset-anchor: 100% 50%;
  offset-path: rect(0 100% 100% 0 round 33px);
  background: radial-gradient(circle at 50% 50%, rgba(255, 255, 255, 0.75), transparent 50%),
              radial-gradient(circle at 50% 50%, var(--edge) 50%, transparent);
  opacity: 0.45; transition: opacity 1s ease-in-out;
  animation: loop var(--loop) linear infinite;
}
.pill .glow::before { animation-delay: calc(var(--loop) / -2); }
.pill:hover .glow::before, .pill:hover .glow::after { opacity: 0.7; }
.pill--cta {
  position: relative; right: auto; margin: 0 auto;
  width: auto; padding: 0 1.5em;
  display: inline-flex; align-items: center; justify-content: center;
}
.pill:focus-visible { outline: 2px solid var(--flare); outline-offset: 4px; }

/* ---------- hero actions ---------- */
.hero-cta {
  display: flex; align-items: center; justify-content: center; flex-wrap: wrap; gap: 1.2em 1.8em;
  opacity: 0; translate: 0 1em;
  animation: fade 2s ease-out 2.4s forwards, rise 1.4s var(--ease) 2.4s forwards;
}
.hero-cta .ghost {
  font-family: var(--mono); font-size: max(0.78em, 12px); letter-spacing: 0.14em; text-transform: uppercase;
  color: var(--steel); opacity: 0.75; transition: opacity 0.2s ease;
}
.hero-cta .ghost:hover { opacity: 1; }
.hero-cta .ghost:focus-visible { outline: 2px solid var(--flare); outline-offset: 5px; }
/* the actions drop away: the pill sinks and shrinks, the link slides off */
.hero-cta > * { --t: clamp(0, calc((var(--out, 0) - 0.12) / 0.4), 1); }
.hero-cta .pill {
  translate: 0 calc(var(--t) * 3em);
  scale: calc(1 - var(--t) * 0.3);
  opacity: calc(1 - var(--t));
  filter: blur(calc(var(--t) * 4px));
}
.hero-cta .ghost { translate: calc(var(--t) * 6em) 0; opacity: calc((1 - var(--t)) * 0.75); }
.stage.gone .hero-cta { visibility: hidden; }
@keyframes loop { to { offset-distance: 100%; } }

.intro {
  position: absolute; left: 0; right: 0; top: 28%; z-index: 20;
  margin: auto; width: fit-content;
  opacity: 0; translate: 0 -1em;
  animation: fade-soft 2s ease-in forwards, rise 1.4s var(--ease) forwards;
}
@keyframes fade-soft { to { opacity: 0.75; } }
.intro p {
  position: relative; width: fit-content; margin: auto;
  font-family: var(--mono); font-size: 0.95em; letter-spacing: 0.24em; text-transform: uppercase;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.intro p::before, .intro p::after {
  content: ""; position: absolute; top: 55%; display: block; width: 5em; height: 1px; opacity: 0;
  animation: rule-soft 1.4s var(--ease) forwards;
}
@keyframes rule-soft { to { opacity: 0.35; } }
.intro p::before { right: 130%; background: linear-gradient(-90deg, var(--steel), transparent); }
.intro p::after { left: 130%; background: linear-gradient(90deg, var(--steel), transparent); }
/* the kicker tracks out and its rules shoot apart */
.intro p {
  --t: clamp(0, calc(var(--out, 0) / 0.45), 1);
  letter-spacing: calc(0.24em + var(--t) * 0.9em);
  opacity: calc(1 - var(--t));
  filter: blur(calc(var(--t) * 4px));
}
.intro p::before { translate: calc(var(--t) * -8em) 0; }
.intro p::after { translate: calc(var(--t) * 8em) 0; }

.hero { position: absolute; left: 0; right: 0; top: 34%; z-index: 20; height: 8em; }
.hero h1 {
  position: absolute; left: 0; right: 0; margin: auto; width: fit-content;
  font-size: 7em; font-weight: 700; letter-spacing: -0.04em; line-height: 1;
  color: var(--steel);
  opacity: 0;
  animation: fade 2s var(--ease) 0.6s forwards;
  background:
    radial-gradient(2em 2em at 50% 50%,
      transparent calc(var(--p) - 2em),
      #fff calc(var(--p) - 1em),
      #fff calc(var(--p) - 0.4em),
      transparent var(--p)),
    linear-gradient(0deg, var(--flare) 30%, var(--steel) 100%);
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  text-shadow: 0 2px 16px color-mix(in srgb, var(--flare) 24%, transparent);
}
.hero h1 + h1 {
  background:
    radial-gradient(2em 2em at 50% 50%,
      transparent calc(var(--p) - 2em),
      transparent calc(var(--p) - 1em),
      #fff calc(var(--p) - 1em),
      #fff calc(var(--p) - 0.4em),
      transparent calc(var(--p) - 0.4em),
      transparent var(--p));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  filter: blur(16px) opacity(0.45);
  text-shadow: none;
}
.sweeping h1 { animation: fade 2s var(--ease) 0.6s forwards, sweep 10s linear 1.4s infinite; }
@keyframes sweep { 0% { --p: 0%; } 50%, 100% { --p: 300%; } }

/* ---------- the wordmark, split for the exit ----------
   Script wraps each letter in a .ch and the h1 drops its own background.
   Each letter carries the same gradients, sized to the whole word and
   shifted by its own offset (--bw, --ox), so at rest the word reads
   exactly as one piece, sweep included; --p inherits so the sweep still
   runs through every letter. Then they scatter from the centre out. */
.hero h1.split { background: none; }
.hero h1 .ch {
  display: inline-block;
  background:
    radial-gradient(2em 2em at 50% 50%,
      transparent calc(var(--p) - 2em),
      #fff calc(var(--p) - 1em),
      #fff calc(var(--p) - 0.4em),
      transparent var(--p)),
    linear-gradient(0deg, var(--flare) 30%, var(--steel) 100%);
  background-size: var(--bw, 100%) 100%;
  background-position: calc(-1 * var(--ox, 0px)) 0;
  background-repeat: no-repeat;
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  --t: clamp(0, calc((var(--out, 0) - 0.04 - var(--da, 0) * 0.07) / 0.5), 1);
  translate: calc(var(--d, 0) * var(--t) * 0.9em) calc(var(--s, 1) * var(--t) * 1.1em);
  rotate: calc(var(--s, 1) * var(--t) * 28deg);
  scale: calc(1 + var(--t) * 0.35);
  opacity: calc(1 - var(--t));
}
.hero h1:first-child .ch { filter: blur(calc(var(--t) * 10px)); }
.hero h1 + h1 .ch {
  background:
    radial-gradient(2em 2em at 50% 50%,
      transparent calc(var(--p) - 2em),
      transparent calc(var(--p) - 1em),
      #fff calc(var(--p) - 1em),
      #fff calc(var(--p) - 0.4em),
      transparent calc(var(--p) - 0.4em),
      transparent var(--p));
  background-size: var(--bw, 100%) 100%;
  background-position: calc(-1 * var(--ox, 0px)) 0;
  background-repeat: no-repeat;
  background-clip: text; -webkit-background-clip: text;
}

/* tagline and the hero's actions stack in one positioned block, so a
   tagline that wraps on a phone pushes the buttons down instead of
   running into them */
.lead {
  position: absolute; left: 0; right: 0; top: 55%; z-index: 20;
  display: flex; flex-direction: column; align-items: center; gap: 1.8em;
  padding: 0 20px;
}
.tagline {
  margin: auto; width: fit-content; text-align: center;
  font-size: 1.15em; line-height: 1.5; text-wrap: balance;
  opacity: 0; translate: 0 1em;
  animation: fade 2s ease-out 2s forwards, rise 1.4s var(--ease) 2s forwards;
}
/* each line carries its own gradient so the two can part company */
.tagline .ln {
  display: block; text-wrap: balance;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  --t: clamp(0, calc((var(--out, 0) - 0.08) / 0.45), 1);
  opacity: calc(1 - var(--t));
  filter: blur(calc(var(--t) * 6px));
}
.tagline .ln:first-child { translate: calc(var(--t) * -7em) 0; }
.tagline .ln:last-child { translate: calc(var(--t) * 7em) 0; }

.ridge {
  position: absolute; left: 0; right: 0; bottom: 0; z-index: 10;
  margin: auto; height: 10em; width: 100%; pointer-events: none;
  opacity: calc(1 - var(--out, 0));
}
.ridge i {
  position: absolute; left: 0; right: 0; margin: auto; display: block;
  width: 20em; height: 20em; rotate: 45deg; z-index: 1;
  background: var(--panel); filter: brightness(0.82);
  box-shadow:
    -1em -0.2em 0.4em -1.1em var(--edge),
    inset 0 0 0 2px var(--edge),
    inset 0.2em 0.3em 0.2em -0.2em var(--edge),
    inset 10.2em 10.3em 2em -10em rgba(212, 230, 255, 0.18);
  bottom: -240%;
}
.ridge i::before {
  content: ""; position: absolute; left: 0; top: 0; display: block;
  width: 12em; height: 12em; border-bottom-right-radius: 100%;
  background: repeating-radial-gradient(at 100% 100%, transparent 0%, rgba(194, 204, 255, 0.13) 2px, transparent 4px);
}
.ridge i {
  translate:
    calc(var(--bx) + var(--ox) * var(--out, 0))
    calc(var(--by) + var(--oy) * var(--out, 0));
}
/* on the way out the outer peaks splay and tip away, the centre one sinks */
.ridge i { rotate: calc(45deg + var(--or, 0deg) * var(--out, 0)); }
.ridge i:nth-child(1) { --bx: -6em; --by: 2em; --ox: -18em; --oy: 9em;  --or: -24deg; animation: ridge-a 2s var(--ease) 2.4s forwards; }
.ridge i:nth-child(2) { --bx: -2em; --by: 0em; --ox: 0em;   --oy: 15em; --or: 0deg; width: 14em; animation: ridge-b 2s var(--ease) 2.2s forwards; }
.ridge i:nth-child(3) { --bx: 6em;  --by: 3em; --ox: 18em;  --oy: 9em;  --or: 24deg; animation: ridge-a 2s var(--ease) 2s forwards; }
@keyframes ridge-a { to { bottom: -140%; } }
@keyframes ridge-b { to { bottom: -108%; } }

.wrap { width: min(1120px, 100% - 40px); margin: 0 auto; }
.band { position: relative; z-index: 20; background: var(--panel); }

/* ============================================================
   THE FRAME — belongs to the hero now, not the viewport.
   It sits inside the stage and comes apart on the same --out
   (0 → 1 over the first half-screen of scroll) that takes the
   ridge down, so the whole stage leaves as one composition.
   Every piece computes its own local progress --t from --out,
   starting at --at and taking --len to finish: that is the
   stagger, with no timeline library behind it.
   ============================================================ */
.field {
  position: absolute; inset: 0; z-index: 0;
  pointer-events: none; overflow: hidden;
  --frame: 20px;
}
.field .br, .field .tk {
  --t: clamp(0, calc((var(--out, 0) - var(--at, 0)) / var(--len, 0.6)), 1);
}

/* corner brackets: each corner splits into its two arms, which slide
   apart along their own lines while the corner fades */
.field .br {
  position: absolute; width: 26px; height: 26px;
  --at: 0.04; --len: 0.75;
  opacity: calc(1 - var(--t));
}
.field .br::before, .field .br::after { content: ""; position: absolute; background: var(--hair-2); }
.field .br::before {
  width: 26px; height: 1px;
  translate: calc(var(--sx) * var(--t) * 90px) calc(var(--sy) * var(--t) * 14px);
  rotate: calc(var(--sx) * var(--sy) * var(--t) * 12deg);
}
.field .br::after {
  width: 1px; height: 26px;
  translate: calc(var(--sx) * var(--t) * 14px) calc(var(--sy) * var(--t) * 70px);
  rotate: calc(var(--sx) * var(--sy) * var(--t) * -12deg);
}
.field .br--tl { top: var(--frame); left: var(--frame); --sx: -1; --sy: -1; }
.field .br--tr { top: var(--frame); right: var(--frame); --sx: 1; --sy: -1; }
.field .br--bl { bottom: var(--frame); left: var(--frame); --sx: -1; --sy: 1; }
.field .br--br { bottom: var(--frame); right: var(--frame); --sx: 1; --sy: 1; }
.field .br--tl::before, .field .br--tl::after { top: 0; left: 0; }
.field .br--tr::before, .field .br--tr::after { top: 0; right: 0; }
.field .br--bl::before, .field .br--bl::after { bottom: 0; left: 0; }
.field .br--br::before, .field .br--br::after { bottom: 0; right: 0; }

/* the depth axis: peels off top to bottom, ticks sliding out to the
   edge, labels drifting in and fanning apart as they blur away */
.field .axis {
  position: absolute; top: var(--frame); left: var(--frame);
  height: calc(100% - var(--frame) * 2); width: 74px;
}
.field .tk { position: absolute; left: 0; height: 0; --at: calc(var(--k) * 0.07); --len: 0.5; }
.field .tk i {
  position: absolute; left: 0; top: 0; width: 9px; height: 1px; background: var(--hair-2);
  transform-origin: left;
  translate: calc(var(--t) * -40px) 0;
  scale: calc(1 + var(--t) * 2) 1;
  opacity: calc(1 - var(--t));
}
.field .tk span {
  position: absolute; left: 34px; top: 0;
  font-family: var(--mono); font-size: 8.5px; letter-spacing: 0.14em;
  color: var(--hair-2); white-space: nowrap;
  translate: calc(var(--t) * 60px) calc(-50% + (var(--k) - 2.5) * var(--t) * 18px);
  rotate: calc((var(--k) - 2.5) * var(--t) * 6deg);
  opacity: calc(1 - var(--t));
  filter: blur(calc(var(--t) * 3px));
}
@media (max-width: 860px) {
  .field .tk span { display: none; }
}

.band { z-index: auto; background: transparent; }
.band::before {
  content: ""; position: absolute; inset: 0; z-index: -1;
  /* feathered top: the panel rises into the emptied stage without an edge */
  background: linear-gradient(to bottom, transparent 0, var(--panel) 40svh);
}
.band > section { position: relative; z-index: 1; }

.pitch { position: relative; overflow: hidden; padding: 10em 0 7em; text-align: center; }
.pitch-acc { position: absolute; left: 0; right: 0; top: 22%; margin: auto; display: flex; justify-content: center; pointer-events: none; }
.pitch-acc i {
  display: block; width: 10em; height: 10em; border-radius: 50%;
  background: repeating-radial-gradient(at 50% 50%, transparent 0%, rgba(194, 204, 255, 0.13) 2px, transparent 4px);
  box-shadow:
    -1em -0.2em 0.4em -1.1em var(--edge),
    inset 0 0 0 2px var(--edge),
    inset 0.2em 0.3em 0.2em -0.2em var(--edge),
    inset -1.2em 2.3em 2em -0.5em rgba(212, 230, 255, 0.18);
  filter: brightness(0.82);
  translate: -18em;
}
.pitch-acc i:nth-child(2) {
  translate: 18em 12em; border-radius: 2em;
  box-shadow:
    -1em -0.2em 0.4em -1.1em var(--edge),
    inset 0 0 0 2px var(--edge),
    inset 0.2em 0.3em 0.2em -0.2em var(--edge),
    inset 10.8em 11.3em 2em -10.5em rgba(212, 230, 255, 0.18);
}
.kicker {
  position: relative; width: fit-content; margin: auto;
  font-family: var(--mono); font-size: 0.8em; letter-spacing: 0.22em; text-transform: uppercase;
  color: color-mix(in srgb, var(--ice) 75%, transparent);
}
.kicker::before, .kicker::after { content: ""; position: absolute; top: 50%; display: block; width: 5em; height: 1px; opacity: 0.45; }
.kicker::before { right: 130%; background: linear-gradient(-90deg, var(--steel), transparent); }
.kicker::after { left: 130%; background: linear-gradient(90deg, var(--steel), transparent); }
.pitch h2 {
  margin: 0.5em 0 0.55em; font-size: clamp(1.7em, 5.2vw, 2.4em); text-wrap: balance; font-weight: 700; line-height: 1.1; letter-spacing: -0.03em;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  text-shadow: 0 2px 16px color-mix(in srgb, var(--flare) 24%, transparent);
}
.pitch > .wrap > p.lede { max-width: 30em; margin: auto; font-size: 1.05em; line-height: 1.6; color: color-mix(in srgb, var(--ice) 74%, transparent); }

.cards { position: relative; padding: 0 0 7em; }
.specs { display: grid; grid-template-columns: repeat(3, 1fr); gap: 1.4em; }

.gcard {
  position: relative; display: flex; overflow: hidden; isolation: isolate;
  min-height: 21em; border-radius: 1em;
  border: 1px solid rgba(255, 255, 255, 0.2);
  transition: border-color 0.4s var(--ease), transform 0.4s var(--ease), box-shadow 0.4s var(--ease);
}
.gcard:hover {
  border-color: color-mix(in srgb, var(--flare) 55%, transparent);
  transform: translateY(-4px);
  box-shadow: 0 0 44px -18px var(--flare-2);
}
.gcard-plate {
  position: absolute; inset: 0; z-index: 0; padding: 3px;
  background: linear-gradient(150deg, var(--flare), color-mix(in srgb, var(--flare-2) 58%, #11141e) 72%);
}
.gcard-plate::before {
  content: ""; display: block; width: 100%; height: 100%;
  border-radius: 0.75em 5.5em 2.2em 0.75em;
  background: #181b28;
}
.gcard-orb { position: absolute; inset: 0; z-index: 1; display: grid; place-items: center end; padding-right: 0.5em; }
.gcard-orb::before {
  content: ""; display: block; width: 8.5em; height: 8.5em; border-radius: 50%;
  background: linear-gradient(45deg,
    color-mix(in srgb, var(--flare-2) 62%, #0a0d18),
    color-mix(in srgb, var(--flare) 72%, #ffffff) 88%);
  animation: turn 12s linear infinite; animation-play-state: paused;
}
.gcard.live .gcard-orb::before { animation-play-state: running; }
/* each spec card gets its own shape, read off its claim:
   01 resident — the solid disc (above)
   02 portable — a rounded die, a piece of silicon turning over
   03 idle     — a ring, the disc with nothing left in the middle */
.specs .gcard:nth-child(2) .gcard-orb::before {
  /* sized so its diagonal matches the disc: it turns without its
     corners running off the card's edge */
  width: 6.2em; height: 6.2em; border-radius: 1.5em;
}
.specs .gcard:nth-child(3) .gcard-orb::before {
  -webkit-mask: radial-gradient(circle, transparent 40%, #000 41%);
  mask: radial-gradient(circle, transparent 40%, #000 41%);
}
/* and the rest of the page's cards, none repeating:
   04 quickstart — a hexagon, a compiled graph node
   8 ms          — a triangle, an arrowhead for speed
   3.2 GB        — a capsule, a memory stick
   comparison    — a half disc, a gauge
   The polygons are inscribed in a square on their own centre, so they
   turn in place at whatever size a breakpoint gives them. */
.how .gcard-orb::before {
  border-radius: 0;
  clip-path: polygon(50% 0, 93.3% 25%, 93.3% 75%, 50% 100%, 6.7% 75%, 6.7% 25%);
}
.stats .gcard:nth-child(1) .gcard-orb::before {
  border-radius: 0;
  clip-path: polygon(50% 0, 93.3% 75%, 6.7% 75%);
}
.stats .gcard:nth-child(2) .gcard-orb::before {
  width: 6.4em; height: 2.9em; border-radius: 2em;
}
.stats .gcard--compare .gcard-orb::before {
  width: 6.6em; height: 3.3em; border-radius: 3.3em 3.3em 0 0;
}
@keyframes turn { to { rotate: 1turn; } }

/* min-width: 0 so a long code line scrolls inside its panel instead of
   stretching the whole card past its frame */
.gcard-body { position: relative; z-index: 2; flex: 1; min-width: 0; display: flex; gap: 0.5em; padding: 0.55em; }
.gcard-panel {
  flex: 1; display: flex; flex-direction: column; padding: 1.1em 1em 0.9em;
  border-radius: 0.75em; border: 1px solid rgba(255, 255, 255, 0.08);
  background: rgba(10, 13, 24, 0.32);
  -webkit-backdrop-filter: blur(16px); backdrop-filter: blur(16px);
}
.gcard-panel h3 { font-size: 1.1em; font-weight: 700; line-height: 1.25; letter-spacing: -0.01em; text-wrap: balance; margin-bottom: 0.5em; }
.gcard-panel p { font-size: 0.9em; line-height: 1.6; color: rgba(233, 240, 252, 0.74); }
.gcard-tag { margin-top: auto; padding-top: 1.2em; font-family: var(--mono); font-size: max(0.66em, 10px); letter-spacing: 0.18em; text-transform: uppercase; color: rgba(233, 240, 252, 0.45); }

.gcard-rail {
  display: flex; flex-direction: column; align-items: flex-end; padding: 0.5em 0.3em 0 0;
  font-family: var(--mono); font-size: max(0.62em, 10px); letter-spacing: 0.14em;
  text-transform: uppercase; line-height: 1.5; color: rgba(233, 240, 252, 0.6);
  text-shadow: 0 1px 3px rgba(5, 7, 16, 0.8);
}
.gcard-go {
  margin-top: auto; display: grid; place-items: center;
  width: 2.6em; height: 2.6em; border-radius: 50%;
  background: rgba(248, 250, 252, 0.18);
  -webkit-backdrop-filter: blur(14px); backdrop-filter: blur(14px);
  color: rgba(255, 255, 255, 0.8);
  transition: background 0.35s var(--ease);
}
.gcard:hover .gcard-go { background: rgba(248, 250, 252, 0.32); }
.gcard-go svg { display: block; width: 1.4em; height: 1.4em; }

.surface { position: relative; padding: 0 0 7em; }
.gcard--wide { min-height: 17em; }
.gcard--wide .gcard-rail { margin-left: auto; }
.gcard--wide .gcard-orb { place-items: center end; padding-right: 3.6em; }
.gcard--wide .gcard-orb::before { width: 13em; height: 13em; animation-duration: 20s; }
.gcard--wide .gcard-panel { flex: 0 1 32em; }
.gcard--wide .gcard-body { gap: 0.5em; }
.gcard--wide .gcard-panel h3 { font-size: 1.7em; letter-spacing: -0.03em; }
.gcard--wide .gcard-panel p { font-size: 0.98em; max-width: 26em; }
.chips { display: flex; flex-wrap: wrap; gap: 0.4em; margin-top: auto; padding-top: 1.4em; }
.chip {
  padding: 0.5em 0.9em; border-radius: 10em;
  font-family: var(--mono); font-size: max(0.62em, 10px); letter-spacing: 0.12em; text-transform: uppercase;
  background: rgba(248, 250, 252, 0.1); border: 1px solid rgba(255, 255, 255, 0.1);
  color: rgba(233, 240, 252, 0.7);
}

.figures { position: relative; padding: 0 0 7em; }
.stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 1em; }
.gcard--stat { min-height: 11.5em; }
.gcard--stat .gcard-plate::before { border-radius: 0.75em 3.4em 1.4em 0.75em; }
.gcard--stat .gcard-body { padding-right: 2.4em; }
.gcard--stat .gcard-orb { padding-right: 0.45em; }
.gcard--stat .gcard-orb::before { width: 6em; height: 6em; animation-duration: 16s; }
.gcard--stat .gcard-panel { padding: 1em 0.95em 0.85em; }
.stat-num {
  font-size: 2.1em; font-weight: 700; letter-spacing: -0.03em; line-height: 1;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.stat-lab {
  margin-top: auto; padding-top: 0.9em;
  font-family: var(--mono); font-size: max(0.64em, 10px); line-height: 1.55; letter-spacing: 0.1em;
  text-transform: uppercase; color: rgba(233, 240, 252, 0.5);
}
.figures .note {
  margin-top: 1.6em; text-align: center;
  font-family: var(--mono); font-size: max(0.68em, 11px); letter-spacing: 0.1em;
  color: color-mix(in srgb, var(--ice) 38%, transparent);
}

/* anchored sections clear the fixed header when jumped to */
.pitch, .how, .figures, .faq, .close { scroll-margin-top: 4.5em; }

/* ---------- quickstart ---------- */
.how { position: relative; padding: 0 0 7em; }
.how .gcard--wide .gcard-panel.how-text { flex: 0 1 22em; }
.how .gcard--wide .gcard-panel.how-text h3 { font-size: 1.5em; }
.code-panel {
  flex: 1 1 26em; min-width: 0; padding: 0; overflow: hidden;
  font-family: var(--mono); font-size: max(0.74em, 12px); line-height: 1.75;
  background: rgba(6, 8, 16, 0.62);
}
.code-bar {
  display: flex; align-items: center; justify-content: space-between; gap: 1em;
  padding: 0.7em 1.1em; border-bottom: 1px solid rgba(255, 255, 255, 0.07);
  color: rgba(233, 240, 252, 0.5); letter-spacing: 0.08em;
}
.code-run {
  font-family: var(--mono); font-size: 1em; letter-spacing: 0.1em; text-transform: uppercase;
  color: var(--steel); padding: 0.2em 0.7em; border-radius: 10em;
  border: 1px solid color-mix(in srgb, var(--steel) 35%, transparent);
  transition: background 0.2s ease;
}
.code-run:hover { background: color-mix(in srgb, var(--steel) 14%, transparent); }
.code-run:focus-visible { outline: 2px solid var(--flare); outline-offset: 3px; }
.code-panel pre { margin: 0; padding: 1em 1.1em 0.6em; overflow-x: auto; color: rgba(233, 240, 252, 0.88); }
.code-panel code { font: inherit; }
.code-panel .sh { color: rgba(233, 240, 252, 0.5); }
.code-panel .k { color: var(--flare); }
.code-panel .s { color: var(--steel); }
.code-panel .c { color: rgba(233, 240, 252, 0.38); font-style: italic; }
.code-out {
  margin: 0 1.1em; padding: 0.8em 0 0.4em; border-top: 1px dashed rgba(255, 255, 255, 0.1);
  color: var(--ice); min-height: 2.6em;
}
.code-out .prompt { color: var(--flare); margin-right: 0.5em; }
.code-out .caret {
  display: inline-block; width: 0.55em; height: 1.1em; vertical-align: -0.2em; margin-left: 0.1em;
  background: var(--flare); opacity: 0.7; animation: blink 1s steps(2) infinite;
}
@keyframes blink { 50% { opacity: 0; } }
.code-meta {
  padding: 0.2em 1.1em 1em; min-height: 2.4em;
  color: rgba(233, 240, 252, 0.5); letter-spacing: 0.08em; font-size: 0.9em;
}

/* ---------- figures: two stats and a comparison ---------- */
.stats { grid-template-columns: 1fr 1fr 2fr; }
.gcard--compare .gcard-panel h3 {
  font-family: var(--mono); font-size: max(0.66em, 10px); font-weight: 500; letter-spacing: 0.1em;
  text-transform: uppercase; color: rgba(233, 240, 252, 0.6); margin-bottom: 1.1em;
}
.bars { display: grid; gap: 0.75em; margin-top: auto; }
.bar {
  display: grid; grid-template-columns: 9.5em 1fr 4.2em; align-items: center; gap: 0.8em;
  font-family: var(--mono); font-size: max(0.66em, 10px); letter-spacing: 0.06em;
  color: rgba(233, 240, 252, 0.7);
}
.bar-val { text-align: right; white-space: nowrap; color: rgba(233, 240, 252, 0.85); }
.bar-track { height: 0.55em; border-radius: 1em; background: rgba(255, 255, 255, 0.06); overflow: hidden; }
.bar-track i {
  display: block; height: 100%; border-radius: inherit;
  width: max(4px, calc(var(--v) * 100%));
  background: color-mix(in srgb, var(--ice) 45%, transparent);
  transform-origin: left; scale: 0 1; transition: scale 1.4s var(--ease);
}
.bar:nth-child(2) .bar-track i { transition-delay: 0.15s; }
.bar:nth-child(3) .bar-track i { transition-delay: 0.3s; }
.drawn .bar-track i { scale: 1 1; }
.bar--us { color: var(--flare); }
.bar--us .bar-val { color: var(--flare); font-weight: 500; }
.bar--us .bar-track i { background: var(--flare); box-shadow: 0 0 10px var(--flare); }

/* ---------- FAQ ---------- */
.faq { position: relative; padding: 0 0 7em; text-align: center; }
.faq h2 {
  margin: 0.5em 0 1.2em; font-size: clamp(1.7em, 5.2vw, 2.2em); font-weight: 700; letter-spacing: -0.03em;
  background: linear-gradient(0deg, var(--ice), var(--flare-2));
  background-clip: text; -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.qs {
  max-width: 44em; margin: 0 auto; text-align: left;
  border-radius: 1em; border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(10, 13, 24, 0.45);
  -webkit-backdrop-filter: blur(16px); backdrop-filter: blur(16px);
}
.qs details + details { border-top: 1px solid rgba(255, 255, 255, 0.07); }
.qs summary {
  list-style: none; cursor: pointer; display: flex; justify-content: space-between; align-items: center; gap: 1em;
  padding: 1.1em 1.3em; font-weight: 600; font-size: 1em;
}
.qs summary::-webkit-details-marker { display: none; }
.qs summary::after {
  content: "+"; font-family: var(--mono); font-weight: 400; font-size: 1.2em; color: var(--steel);
  transition: rotate 0.3s var(--ease);
}
.qs details[open] summary::after { rotate: 45deg; }
.qs summary:hover { color: var(--flare); }
.qs summary:focus-visible { outline: 2px solid var(--flare); outline-offset: -2px; border-radius: 0.6em; }
.qs details p {
  padding: 0 1.3em 1.2em; max-width: 38em;
  font-size: 0.92em; line-height: 1.65; color: rgba(233, 240, 252, 0.72);
}

/* ---------- request access ---------- */
.access { display: flex; justify-content: center; flex-wrap: wrap; gap: 0.6em; max-width: 30em; margin: 0 auto; }
.access[hidden] { display: none; }
.access input {
  flex: 1 1 15em; height: 2.4em; padding: 0 1.2em; border-radius: 20em;
  border: 1px solid rgba(194, 204, 255, 0.25); background: rgba(10, 13, 24, 0.55);
  color: var(--ice); font: inherit; font-size: 1em;
}
.access input::placeholder { color: color-mix(in srgb, var(--ice) 40%, transparent); }
.access input:focus-visible { outline: 2px solid var(--flare); outline-offset: 2px; }
.access .pill { flex: none; margin: 0; }
.access-done { font-size: 1.05em; color: var(--steel); }
.access-done:focus { outline: none; }
.access-fine {
  margin-top: 1.2em; font-family: var(--mono); font-size: max(0.68em, 11px); letter-spacing: 0.08em;
  color: color-mix(in srgb, var(--ice) 45%, transparent);
}

/* ---------- footer nav ---------- */
.foot-nav {
  flex-basis: 100%; display: flex; flex-wrap: wrap; gap: 0.6em 1.8em;
  padding-bottom: 1.6em; border-bottom: 1px solid var(--hair);
  letter-spacing: 0.1em; text-transform: uppercase;
}
.foot .foot-nav a { color: color-mix(in srgb, var(--ice) 70%, transparent); border-bottom: 0; }
.foot .foot-nav a:hover { color: var(--flare); }

.close { position: relative; text-align: center; padding: 0 0 6em; }
.close h2 { font-size: 2em; font-weight: 700; margin-bottom: 0.5em; letter-spacing: -0.03em; }
.close p { max-width: 28em; margin: 0 auto 2em; font-size: 1em; line-height: 1.6; color: color-mix(in srgb, var(--ice) 70%, transparent); }

.foot { position: relative; }
.foot .wrap {
  display: flex; justify-content: space-between; gap: 1.4em; flex-wrap: wrap;
  padding: 2.4em 0 3.4em;
  font-family: var(--mono); font-size: max(0.72em, 10px); line-height: 1.9;
  color: color-mix(in srgb, var(--ice) 45%, transparent);
}
.foot a { color: var(--steel); border-bottom: 1px solid color-mix(in srgb, var(--steel) 50%, transparent); }
.foot a:hover { color: var(--ice); }

@media (max-width: 900px) {
  .specs { grid-template-columns: 1fr; }
  .stats { grid-template-columns: repeat(2, 1fr); }
  .gcard { min-height: 17em; }
  .gcard--wide .gcard-orb { padding-right: 2em; }
  .gcard--wide .gcard-panel { flex: 0 1 24em; }
  .pitch-acc i { translate: -11em; } .pitch-acc i:nth-child(2) { translate: 11em 12em; }
  .gcard--compare { grid-column: span 2; }
  .how .gcard--wide .gcard-body { flex-wrap: wrap; }
  .how .gcard--wide .gcard-panel.how-text, .code-panel { flex: 1 1 100%; }
  .how .gcard-rail { display: none; }
}
@media (max-width: 620px) {
  .topcta { font-size: 0.92em; right: 1.4em; }
  .wordmark { left: 1.4em; }
  .bar { grid-template-columns: 7.5em 1fr 3.8em; }
  .hero h1 { font-size: 4.6em; }
  .pitch-acc { display: none; }
  .gcard { min-height: 0; }
  .gcard--wide .gcard-orb { place-items: end center; padding: 0 0 1.5em; }
  .gcard--wide .gcard-orb::before { width: 9em; height: 9em; }
  .gcard--wide .gcard-panel { flex: 1; }
  .gcard--wide .gcard-panel h3 { font-size: 1.4em; }
}

@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  /* no pin and no exit: the hero is a normal first screen */
  .stage-pin { height: auto; margin-bottom: 0; }
  .stage { position: relative; }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
  .spotlight i { opacity: 0.5; scale: 1; }
  .ridge i:nth-child(1), .ridge i:nth-child(3) { bottom: -140%; }
  .ridge i:nth-child(2) { bottom: -108%; }
  .gcard-orb::before { animation: none; }
  .top, .intro, .tagline, .hero-cta { opacity: 1; translate: 0; }
  .code-out .caret { animation: none; }
  .hero h1 { opacity: 1; }
}
</style>
</head>
<body>

<div class="spotlight" aria-hidden="true"><span><i></i></span><span><i></i></span><span><i></i></span></div>

<header class="top" data-section="nav">
  <a class="wordmark" href="#pitch">UMBRA</a>
  <button class="lamp" type="button" id="lamp" aria-pressed="true">
    <span class="sr" id="lampLabel">Stage light: cool. Press to warm it.</span>
  </button>
  <a class="topcta" href="#access">Request access</a>
</header>

<div class="stage-pin" data-section="hero">
<div class="stage">
  <div class="field" aria-hidden="true">
    <b class="br br--tl"></b><b class="br br--tr"></b><b class="br br--bl"></b><b class="br br--br"></b>
    <div class="axis">
      <b class="tk" style="top:20%;--k:1"><i></i><span>020</span></b>
      <b class="tk" style="top:40%;--k:2"><i></i><span>040</span></b>
      <b class="tk" style="top:60%;--k:3"><i></i><span>060</span></b>
      <b class="tk" style="top:80%;--k:4"><i></i><span>080</span></b>
    </div>
  </div>
  <div class="intro"><p>Introducing</p></div>
  <div class="hero" id="hero">
    <h1>Umbra</h1>
    <h1 aria-hidden="true">Umbra</h1>
  </div>
  <div class="lead">
    <p class="tagline"><span class="ln">The inference runtime that gets out of the way.</span> <span class="ln">Models in, tokens out, nothing left running.</span></p>
    <div class="hero-cta">
      <a class="pill pill--cta" href="#access">
        <span class="glow" aria-hidden="true"></span>
        <span class="label">Request access</span>
      </a>
      <a class="ghost" href="#how">See how it works ↓</a>
    </div>
  </div>
  <div class="ridge" aria-hidden="true"><i></i><i></i><i></i></div>
</div>
</div>

<main class="band">
  <section class="pitch" id="pitch" data-section="pitch">
    <div class="wrap">
      <h2>Load once. Serve everywhere.<br />Pay for none of the waiting.</h2>
      <p class="lede">
        Umbra keeps weights resident and cold-starts in the time it takes to parse the request,
        so the runtime stops being the thing you plan around.
      </p>
    </div>
  </section>

  <section class="cards" data-section="features" aria-label="Capabilities">
    <div class="wrap">
      <div class="specs">
        <article class="gcard">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <h3>You have been paying for cold starts</h3>
              <p>Weights stay mapped and the graph stays compiled between calls. The first request after an idle hour costs what the second one does.</p>
              <span class="gcard-tag">resident</span>
            </div>
            <div class="gcard-rail" aria-hidden="true">
              <span>01</span>
              <span>spec</span>
            </div>
          </div>
        </article>
        <article class="gcard">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <h3>One artifact, any silicon</h3>
              <p>The same build runs on the laptop you developed it on and the rack you deployed it to. No per-target rebuild, no quiet precision swap.</p>
              <span class="gcard-tag">portable</span>
            </div>
            <div class="gcard-rail" aria-hidden="true">
              <span>02</span>
              <span>spec</span>
            </div>
          </div>
        </article>
        <article class="gcard">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <h3>Nothing left running</h3>
              <p>Idle means idle. When traffic stops the runtime releases and the meter stops with it, which is the part every other bill forgets.</p>
              <span class="gcard-tag">idle</span>
            </div>
            <div class="gcard-rail" aria-hidden="true">
              <span>03</span>
              <span>spec</span>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>

  <section class="how" id="how" data-section="how-it-works">
    <div class="wrap">
      <article class="gcard gcard--wide" id="howCard">
        <span class="gcard-plate" aria-hidden="true"></span>
        <span class="gcard-orb" aria-hidden="true"></span>
        <div class="gcard-body">
          <div class="gcard-panel how-text">
            <h3>From weights to first token in four lines.</h3>
            <p>Point Umbra at a model file. It picks the backend for the machine it's on, compiles the graph once and keeps it warm. There is no server process to stand up and no container to keep alive.</p>
            <span class="gcard-tag">quickstart</span>
          </div>
          <div class="gcard-panel code-panel" data-component="quickstart-stream">
            <div class="code-bar">
              <span>quickstart.py</span>
              <button class="code-run" type="button" id="runAgain">▶ Run</button>
            </div>
<pre><code><span class="sh">$ pip install umbra</span>

<span class="k">import</span> umbra

model = umbra.load(<span class="s">"./weights/7b-instruct"</span>)
<span class="c"># backend picked here, once. graph stays warm.</span>

<span class="k">for</span> tok <span class="k">in</span> model.stream(<span class="s">"Say hello"</span>):
    print(tok, end=<span class="s">""</span>)</code></pre>
            <div class="code-out"><span class="prompt" aria-hidden="true">›</span><span id="streamOut">Hello! The weights were already warm.</span><span class="caret" aria-hidden="true"></span></div>
            <div class="code-meta" id="streamMeta">first token 8 ms · 8 tokens · released when idle</div>
          </div>
          <div class="gcard-rail" aria-hidden="true">
            <span>04</span>
            <span>how</span>
            <span class="gcard-go"><svg viewBox="0 0 12 12" aria-hidden="true"><path fill="currentColor" d="M4.646 2.146a.5.5 0 0 0 0 .708L7.793 6L4.646 9.146a.5.5 0 1 0 .708.708l3.5-3.5a.5.5 0 0 0 0-.708l-3.5-3.5a.5.5 0 0 0-.708 0z"/></svg></span>
          </div>
        </div>
      </article>
    </div>
  </section>

  <section class="figures" id="figures" data-section="stats" aria-label="Figures">
    <div class="wrap">
      <div class="stats">
        <article class="gcard gcard--stat">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <span class="stat-num">8 ms</span>
              <span class="stat-lab">to first token, after an idle hour</span>
            </div>
          </div>
        </article>
        <article class="gcard gcard--stat">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <span class="stat-num">3.2 GB</span>
              <span class="stat-lab">resident for a 7B model</span>
            </div>
          </div>
        </article>
        <article class="gcard gcard--stat gcard--compare">
          <span class="gcard-plate" aria-hidden="true"></span>
          <span class="gcard-orb" aria-hidden="true"></span>
          <div class="gcard-body">
            <div class="gcard-panel">
              <h3>Time to first token, after an idle hour</h3>
              <div class="bars">
                <div class="bar bar--us"><span>Umbra</span><span class="bar-track" aria-hidden="true"><i style="--v:0.0019"></i></span><span class="bar-val">8 ms</span></div>
                <div class="bar"><span>Warm container</span><span class="bar-track" aria-hidden="true"><i style="--v:0.043"></i></span><span class="bar-val">180 ms</span></div>
                <div class="bar"><span>Serverless GPU, cold</span><span class="bar-track" aria-hidden="true"><i style="--v:1"></i></span><span class="bar-val">4.2 s</span></div>
              </div>
            </div>
          </div>
        </article>
      </div>
      <p class="note">Invented product, invented figures — nothing here was measured.</p>
    </div>
  </section>

  <section class="faq" id="faq" data-section="faq">
    <div class="wrap">
      <h2>Questions</h2>
      <div class="qs">
        <details>
          <summary>Which model formats does it load?</summary>
          <p>GGUF, safetensors and ONNX, quantised or not. Umbra reads the file as it is, so there is no conversion step and no exported copy to keep in sync.</p>
        </details>
        <details>
          <summary>What hardware does it run on?</summary>
          <p>Apple silicon, consumer and datacentre GPUs, and plain CPU. The backend is chosen when the model loads, so the same artifact moves between them unchanged.</p>
        </details>
        <details>
          <summary>How is it priced?</summary>
          <p>Per second of active serving. When traffic stops the runtime releases and the meter stops with it, so you never pay for capacity sitting idle.</p>
        </details>
        <details>
          <summary>Can we self-host it?</summary>
          <p>Yes. The runtime ships as a single binary you can run on your own machines. The hosted service is that same binary running on ours.</p>
        </details>
        <details>
          <summary>What happens to our prompts and outputs?</summary>
          <p>On the hosted service, requests are processed in memory and not retained. Self-hosted, nothing leaves your machines at all.</p>
        </details>
      </div>
    </div>
  </section>

  <section class="close" id="access" data-section="cta">
    <div class="wrap">
      <h2>Come and watch it do nothing.</h2>
      <p>The interesting part of a runtime is what it stops doing. Put a model in front of it and see how little is left between the request and the first token.</p>
      <form class="access" id="accessForm" data-component="access-form">
        <label class="sr" for="accessEmail">Work email</label>
        <input id="accessEmail" name="email" type="email" required autocomplete="email" placeholder="you@company.com" />
        <button class="pill pill--cta" type="submit">
          <span class="glow" aria-hidden="true"></span>
          <span class="label">Request access</span>
        </button>
      </form>
      <p class="access-done" id="accessDone" role="status" tabindex="-1" hidden>You're on the list. We'll be in touch when a seat opens.</p>
    </div>
  </section>

  <footer class="foot" data-section="footer">
    <div class="wrap">
      <nav class="foot-nav" aria-label="Page">
        <a href="#how">How it works</a>
        <a href="#figures">Figures</a>
        <a href="#faq">FAQ</a>
        <a href="#access">Request access</a>
      </nav>
      <span>
        Umbra is a fictional product and this page is a design demo — the platform,<br />
        the claims and every figure are invented. Nothing here is real.
      </span>
      <span>
        Stage, spotlights and swept wordmark adapted from a pen by
        <a href="https://codepen.io/RAFA3L" target="_blank" rel="noopener">RAFA3L</a><br />
        One file · no images · no libraries
      </span>
    </div>
  </footer>
</main>

<script>
(() => {
"use strict";
const REDUCED = matchMedia("(prefers-reduced-motion: reduce)").matches;

const lamp = document.getElementById("lamp");
const lampLabel = document.getElementById("lampLabel");
const LAMP = [
  { flare: false, out: false, say: "Stage light: cool. Press to warm it." },
  { flare: true,  out: false, say: "Stage light: warm. Press to switch it off." },
  { flare: false, out: true,  say: "Stage light: off. Press to switch it on." }
];
let lampAt = 0;
lamp.addEventListener("click", () => {
  lampAt = (lampAt + 1) % LAMP.length;
  const st = LAMP[lampAt];
  document.body.classList.toggle("flare", st.flare);
  document.body.classList.toggle("out", st.out);
  lamp.setAttribute("aria-pressed", String(!st.out));
  lampLabel.textContent = st.say;
});

const hero = document.getElementById("hero");
if (!REDUCED) {
  new IntersectionObserver((es) => {
    for (const e of es) hero.classList.toggle("sweeping", e.isIntersecting);
  }, { threshold: 0 }).observe(hero);
}

/* the stage's exit. --out runs 0 → 1 across the pinned stretch and is
   written on the three things that read it: the stage, the bar (for the
   lamp) and the spotlights. The bar's backdrop switches on once the hero
   has scrolled away, with or without motion. */
(() => {
  const pin = document.querySelector(".stage-pin");
  const stageEl = document.querySelector(".stage");
  const bar = document.querySelector(".top");
  const spot = document.querySelector(".spotlight");
  if (!pin || !stageEl || !bar) return;

  /* split the wordmark into letters, both the face and its glow copy */
  if (!REDUCED) {
    const hs = [...document.querySelectorAll(".hero h1")];
    for (const [hi, h] of hs.entries()) {
      const word = h.textContent.trim();
      h.textContent = "";
      if (hi === 0) {
        const sr = document.createElement("span");
        sr.className = "sr"; sr.textContent = word; h.appendChild(sr);
      }
      const n = word.length;
      [...word].forEach((c, i) => {
        const s = document.createElement("span");
        const d = i - (n - 1) / 2;
        s.className = "ch"; s.textContent = c; s.setAttribute("aria-hidden", "true");
        s.style.setProperty("--d", d);
        s.style.setProperty("--da", Math.abs(d));
        s.style.setProperty("--s", i % 2 ? 1 : -1);
        h.appendChild(s);
      });
      h.classList.add("split");
    }
    /* each letter's gradient is the word's gradient, offset to where the
       letter sits — measured again once the webfont lands */
    const measure = () => {
      for (const h of hs) {
        h.style.setProperty("--bw", h.clientWidth + "px");
        for (const s of h.querySelectorAll(".ch")) s.style.setProperty("--ox", s.offsetLeft + "px");
      }
    };
    measure();
    if (document.fonts) document.fonts.ready.then(measure);
    addEventListener("resize", measure);
  }

  let queued = false;
  const paint = () => {
    queued = false;
    const D = Math.max(1, pin.offsetHeight - innerHeight);
    bar.classList.toggle("past", scrollY > D * 0.95);
    if (REDUCED) return;
    const o = Math.min(1, Math.max(0, scrollY / (D * 0.9)));
    const v = o.toFixed(3);
    stageEl.style.setProperty("--out", v);
    bar.style.setProperty("--out", v);
    if (spot) spot.style.setProperty("--out", v);
    stageEl.classList.toggle("gone", o > 0.6);
    bar.classList.toggle("lampgone", o > 0.75);
  };
  const req = () => { if (!queued) { queued = true; requestAnimationFrame(paint); } };
  addEventListener("scroll", req, { passive: true });
  addEventListener("resize", req);
  paint();
})();

(() => {
  if (REDUCED) return;
  const cards = document.querySelectorAll(".gcard");
  const onScreen = new Set();
  const apply = () => {
    for (const c of cards) c.classList.toggle("live", !document.hidden && onScreen.has(c));
  };
  const io = new IntersectionObserver((es) => {
    for (const e of es) e.isIntersecting ? onScreen.add(e.target) : onScreen.delete(e.target);
    apply();
  }, { rootMargin: "120px 0px" });
  for (const c of cards) io.observe(c);
  document.addEventListener("visibilitychange", apply);
})();

/* REQUEST ACCESS — a demo form: validates, then swaps to a confirmation */
(() => {
  const form = document.getElementById("accessForm");
  const done = document.getElementById("accessDone");
  if (!form || !done) return;
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    form.hidden = true;
    done.hidden = false;
    done.focus();
  });
})();

/* QUICKSTART — streams the output in when the card first comes into view,
   and again whenever Run is pressed. The finished text is in the HTML, so
   without script (or with reduced motion) the card still reads complete. */
(() => {
  const out = document.getElementById("streamOut");
  const meta = document.getElementById("streamMeta");
  const run = document.getElementById("runAgain");
  const card = document.getElementById("howCard");
  if (!out || !meta || !run || !card) return;
  const TOKENS = ["Hello", "!", " The", " weights", " were", " already", " warm", "."];
  const FINAL = "first token 8 ms · " + TOKENS.length + " tokens · released when idle";
  let timer = 0;
  const play = () => {
    clearTimeout(timer);
    if (REDUCED) { out.textContent = TOKENS.join(""); meta.textContent = FINAL; return; }
    out.textContent = ""; meta.textContent = "";
    let i = 0;
    const step = () => {
      out.textContent += TOKENS[i++];
      if (i === 1) meta.textContent = "first token 8 ms";
      if (i < TOKENS.length) timer = setTimeout(step, 70 + Math.random() * 70);
      else meta.textContent = FINAL;
    };
    /* effectively instant: the point is that nothing visibly waits */
    timer = setTimeout(step, 30);
  };
  run.addEventListener("click", play);
  if (!REDUCED) {
    new IntersectionObserver((es, io) => {
      if (es[0].isIntersecting) { io.disconnect(); play(); }
    }, { threshold: 0.4 }).observe(card);
  }
})();

/* COMPARISON — bars draw in once, the first time the card is on screen */
(() => {
  const cmp = document.querySelector(".gcard--compare");
  if (!cmp) return;
  if (REDUCED || !("IntersectionObserver" in window)) { cmp.classList.add("drawn"); return; }
  new IntersectionObserver((es, io) => {
    if (es[0].isIntersecting) { cmp.classList.add("drawn"); io.disconnect(); }
  }, { threshold: 0.4 }).observe(cmp);
})();

})();
</script>
</body>
</html>
```

