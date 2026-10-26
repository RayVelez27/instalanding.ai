INSTALANDING.AI · Skewed Marquee Wall

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Skewed Marquee Wall · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/skewed-marquee-wall

marquee-wall.html:
```html
<!DOCTYPE html>
<!--
  INSTALANDING.AI · Skewed Marquee Wall
  slug     skewed-marquee-wall
  prompt   https://instalanding.ai/p/skewed-marquee-wall.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/skewed-marquee-wall
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of <style>: --ground #1b1e21, --panel, --well, --chrome / --chrome-hi,
            --ink, --ok / --warn / --stop (+ -glow; semantic only), --speed (marquee multiplier), --f-display VT323, Geist body
  sections  nav, hero, integrations, how-it-works, agents, guardrails, cta, footer
  scripts   1) the run console: scripted planner, step-by-step simulated run with tool-call trace and approval gates,
               fleet kill switch; asks window.claude.use("sample") for live plans when hosted inside Claude, else offline
            2) scroll reveals: IntersectionObserver over a [selector, kind] table, skipped under reduced motion
            No CDN libraries; fonts from Google Fonts.
  assets    none: all CSS and inline SVG

  ADAPTING
  - Each .marquee holds TWO identical .marquee__group children (the second aria-hidden); the keyframe ends at
    translateX(calc(-100% - var(--gap))), not -100%, or the strip jumps one gap per cycle.
  - Lane speed is --duration / --speed per .marquee; the kill switch pauses every lane via body.stopped, so keep that class hook.
  - body uses overflow-x: clip, not hidden, so the skewed bands overhang without a scrollbar and the sticky bar still sticks.
  - Nothing leaves the page: runs are simulated even when Claude writes the plan.
-->
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
<title>SKEWSHOP Agents</title>
<meta name="description" content="SKEWSHOP: agents that run the back office of an online shop, with a live run console, approval gates and a fleet kill switch. Single-file template." />

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=VT323&family=Geist:wght@400..700&display=swap" rel="stylesheet" />

<style>
/* Layout: a machine floor. Lit steel up top, agent runs streaming past in
   skewed lanes, and the run console bolted into the hero like an instrument. */
:root {
  color-scheme: dark;
  --space: 2rem;
  --speed: 1;

  /* Steel and chrome, with phosphor states. Green, amber and coral are
     semantic (ok / waiting / stopped), never decoration. */
  --ground: #1b1e21;
  --ground-2: #23272a;
  --panel: #2a2f33;
  --panel-2: #32383c;
  --well: #15181a;
  --steel: #5a6168;
  --chrome: #9ba2a8;
  --chrome-hi: #e4e8eb;
  --spill: #c3ccd5;
  --ink: #f2f4f5;
  --ink-2: #b6bdc3;
  --mute: #7f878e;
  --line: rgba(228, 232, 235, 0.09);
  --line-2: rgba(228, 232, 235, 0.17);
  --ok: #7fe36a;
  --ok-hi: #a6f593;
  --ok-glow: rgba(127, 227, 106, 0.34);
  --warn: #f2a95e;
  --warn-glow: rgba(242, 169, 94, 0.32);
  --stop: #ff7d83;
  --stop-glow: rgba(255, 125, 131, 0.34);

  --f-display: "VT323", "Geist Mono", ui-monospace, monospace;
  --f-body: "Geist", system-ui, -apple-system, "Segoe UI", sans-serif;
  --f-mono: "VT323", ui-monospace, "SFMono-Regular", Menlo, monospace;

  --ease: cubic-bezier(0.7, 0, 0.2, 1);
  --bevel: inset 0 1px 0 rgba(255, 255, 255, 0.08), inset 0 -1px 0 rgba(0, 0, 0, 0.45);
  --lift: 0 1px 0 rgba(255, 255, 255, 0.04), 0 30px 60px -30px rgba(0, 0, 0, 0.9);
}
*, *::before, *::after { box-sizing: border-box; }
html { -webkit-text-size-adjust: 100%; }

body {
  margin: 0;
  min-height: 100vh;
  color: var(--ink);
  font-family: var(--f-body);
  font-size: 1rem;
  line-height: 1.55;
  background:
    radial-gradient(70% 38% at 50% -8%, rgba(195, 204, 213, 0.28) 0%, rgba(195, 204, 213, 0) 64%),
    linear-gradient(180deg, var(--ground-2) 0%, var(--ground) 38%, var(--ground) 100%);
  background-color: var(--ground);
  background-repeat: no-repeat;
  overflow-x: clip;
  -webkit-font-smoothing: antialiased;
}

img, svg, canvas { display: block; max-width: 100%; }
a { color: inherit; }
button, select, textarea, input { font: inherit; color: inherit; }
button { cursor: pointer; }
:focus-visible { outline: 2px solid var(--ok); outline-offset: 3px; border-radius: 6px; }

.sr-only {
  position: absolute; width: 1px; height: 1px;
  padding: 0; margin: -1px; overflow: hidden;
  clip: rect(0 0 0 0); white-space: nowrap; border: 0;
}
.wrap { width: min(1180px, 100% - 2.5rem); margin-inline: auto; }
.mono { font-family: var(--f-mono); }

/* ════════════════════════════════════════════════════════
   THE RAIL
   Two identical groups, each at least as wide as the rail, both sliding
   left by their own width PLUS one gap.
   ════════════════════════════════════════════════════════ */
.marquee {
  --duration: 60s;
  --gap: var(--space);
  display: flex;
  overflow: hidden;
  user-select: none;
  gap: var(--gap);
  mask-image: linear-gradient(90deg, transparent, #000 7%, #000 93%, transparent);
  -webkit-mask-image: linear-gradient(90deg, transparent, #000 7%, #000 93%, transparent);
}
.marquee__group {
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: space-around;
  gap: var(--gap);
  min-width: 100%;
  animation: scroll calc(var(--duration) / var(--speed, 1)) linear infinite;
  will-change: transform;
}
@keyframes scroll {
  from { transform: translateX(0); }
  to { transform: translateX(calc(-100% - var(--gap))); }
}
.marquee--reverse .marquee__group {
  animation-direction: reverse;
  animation-delay: calc(var(--duration) / var(--speed, 1) / -2);
}
.marquee--skew { transform: skewY(-3deg); }
.marquee--skew-reverse { transform: skewY(3deg); }
.marquee:hover .marquee__group,
.marquee:focus-within .marquee__group { animation-play-state: paused; }

.marquee--vertical {
  flex-direction: column;
  height: clamp(20rem, 46vh, 30rem);
  mask-image: linear-gradient(180deg, transparent, #000 12%, #000 88%, transparent);
  -webkit-mask-image: linear-gradient(180deg, transparent, #000 12%, #000 88%, transparent);
}
.marquee--vertical .marquee__group {
  flex-direction: column;
  min-width: 0;
  min-height: 100%;
  animation-name: scroll-y;
}
@keyframes scroll-y {
  from { transform: translateY(0); }
  to { transform: translateY(calc(-100% - var(--gap))); }
}

/* The kill switch: every lane obeys one class. */
body.stopped .marquee__group { animation-play-state: paused !important; }

@media (prefers-reduced-motion: reduce) {
  .marquee__group { animation-play-state: paused; }
  * { animation-duration: 0.001ms !important; transition-duration: 0.001ms !important; }
}

/* ── Run tiles: what streams through the lanes ─────────── */
.tile {
  flex-shrink: 0;
  display: grid;
  gap: 0.55rem;
  width: clamp(15rem, 10rem + 14vw, 19rem);
  padding: 0.95rem 1.05rem;
  border-radius: 0.9rem;
  border: 1px solid var(--line-2);
  background:
    radial-gradient(120% 80% at 50% -30%, rgba(195, 204, 213, 0.12), rgba(195, 204, 213, 0) 70%),
    linear-gradient(180deg, var(--panel-2), var(--panel));
  box-shadow: var(--bevel), 0 18px 36px -22px rgba(0, 0, 0, 0.9);
}
.tile-top {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-family: var(--f-mono);
  font-size: 0.937rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--mute);
}
.tile-top time { margin-left: auto; font-variant-numeric: tabular-nums; }
.tile p { margin: 0; font-size: 0.92rem; line-height: 1.4; color: var(--ink); }
.tile-tools { font-family: var(--f-mono); font-size: 0.966rem; color: var(--ink-2); }
.tile--you { border-color: rgba(127, 227, 106, 0.45); }

.dot {
  flex-shrink: 0;
  width: 0.46rem; height: 0.46rem;
  border-radius: 50%;
  background: var(--ok);
  box-shadow: 0 0 8px 1px var(--ok-glow);
}
.dot--warn { background: var(--warn); box-shadow: 0 0 8px 1px var(--warn-glow); }
.dot--stop { background: var(--stop); box-shadow: 0 0 8px 1px var(--stop-glow); }
.dot--idle { background: var(--steel); box-shadow: none; }

/* The readout band */
.marquee--rails {
  border-block: 1px solid var(--line-2);
  padding-block: 0.75rem;
  background: linear-gradient(180deg, rgba(0, 0, 0, 0.32), rgba(0, 0, 0, 0.12));
}
.readout {
  flex-shrink: 0;
  margin: 0;
  font-family: var(--f-mono);
  font-weight: 400;
  font-size: clamp(1.42rem, 0.994rem + 1.8vw, 2.56rem);
  line-height: 1.2;
  letter-spacing: 0.04em;
  white-space: nowrap;
  text-transform: uppercase;
  color: var(--ok);
  text-shadow: 0 0 18px var(--ok-glow);
}
.readout em { font-style: normal; color: var(--ink); text-shadow: none; }
body.stopped .readout { color: var(--stop); text-shadow: 0 0 18px var(--stop-glow); }

/* ════════════════════════════════════════════════════════
   PAGE CHROME
   ════════════════════════════════════════════════════════ */
.topbar {
  position: sticky;
  top: env(safe-area-inset-top, 0px);
  z-index: 30;
  display: flex;
  align-items: center;
  gap: 1.5rem;
  padding: 0.75rem clamp(1rem, 3vw, 2rem);
  background: rgba(27, 30, 33, 0.72);
  backdrop-filter: blur(16px) saturate(140%);
  -webkit-backdrop-filter: blur(16px) saturate(140%);
  border-bottom: 1px solid var(--line);
}
.brand {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  font-family: var(--f-display);
  font-weight: 400;
  font-size: 1.38rem;
  letter-spacing: 0.01em;
  text-decoration: none;
}
.dome {
  flex-shrink: 0;
  width: 1.35rem; height: 1.35rem;
  border-radius: 50%;
  background: radial-gradient(circle at 50% 30%, var(--ok-hi), var(--ok) 52%, #2d6a21);
  border: 2px solid var(--chrome);
  box-shadow: 0 0 14px -2px var(--ok-glow);
  transition: background 0.4s var(--ease), box-shadow 0.4s var(--ease);
}
body.stopped .dome {
  background: radial-gradient(circle at 50% 30%, #ffd2c4, var(--stop) 55%, #7a2a2e);
  box-shadow: 0 0 14px -2px var(--stop-glow);
}
.topbar nav { display: flex; gap: 1.4rem; margin-right: auto; font-size: 0.9rem; }
.topbar nav a { text-decoration: none; color: var(--ink-2); transition: color 0.2s; }
.topbar nav a:hover { color: var(--ink); }
.topbar-end { display: flex; align-items: center; gap: 0.75rem; }
@media (max-width: 820px) { .topbar nav { display: none; } .brand { margin-right: auto; } }
@media (max-width: 520px) { .topbar .plate { display: none; } }

.plate {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.38rem 0.75rem;
  border-radius: 0.5rem;
  background: var(--well);
  border: 1px solid var(--line-2);
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.7);
  font-family: var(--f-mono);
  font-weight: 400;
  font-size: 0.994rem;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--ink-2);
  white-space: nowrap;
  font-variant-numeric: tabular-nums;
}
.plate b { font-weight: 600; color: var(--ok); text-shadow: 0 0 10px var(--ok-glow); }
body.stopped .plate b { color: var(--stop); text-shadow: 0 0 10px var(--stop-glow); }

.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  min-height: 2.75rem;
  padding: 0 1.25rem;
  border-radius: 999px;
  border: 1px solid var(--line-2);
  background: linear-gradient(180deg, #3d4347, #2c3135);
  color: var(--chrome-hi);
  font-weight: 600;
  font-size: 0.92rem;
  text-decoration: none;
  white-space: nowrap;
  box-shadow: var(--bevel);
  transition: transform 0.2s var(--ease), border-color 0.25s var(--ease), box-shadow 0.25s var(--ease);
}
.btn:hover { transform: translateY(-1px); border-color: var(--chrome); }
.btn:active { transform: translateY(1px); }
.btn--light {
  background: linear-gradient(180deg, #f6f8f9, #cfd5da);
  border-color: #f6f8f9;
  color: #15181a;
  box-shadow: inset 0 1px 0 #fff, inset 0 -1px 0 rgba(0, 0, 0, 0.18), 0 10px 24px -12px rgba(0, 0, 0, 0.9);
}
.btn--sm { min-height: 2.2rem; padding: 0 0.95rem; font-size: 0.84rem; }
.btn svg { width: 1rem; height: 1rem; }

/* ════════════════════════════════════════════════════════
   HERO
   ════════════════════════════════════════════════════════ */
.hero {
  position: relative;
  isolation: isolate;
  overflow: hidden;
  padding-block: clamp(3.5rem, 8vw, 6rem) clamp(3rem, 6vw, 4.5rem);
}
.hero-reels {
  position: absolute;
  inset: -6% -6% auto;
  height: 74%;
  z-index: 0;
  display: grid;
  align-content: center;
  gap: clamp(1rem, 2vw, 1.6rem);
  pointer-events: none;
  opacity: 0.38;
  transition: opacity 0.6s var(--ease), filter 0.6s var(--ease);
}
body.stopped .hero-reels { opacity: 0.32; filter: saturate(0.2) brightness(0.85); }
.hero-scrim {
  position: absolute;
  inset: 0;
  z-index: 1;
  pointer-events: none;
  background:
    linear-gradient(180deg, rgba(27, 30, 33, 0.55) 0%, rgba(27, 30, 33, 0.9) 22%, rgba(27, 30, 33, 0.94) 52%, var(--ground) 76%);
}
.hero-inner { position: relative; z-index: 2; display: grid; gap: clamp(2rem, 4vw, 3rem); }

.hero-copy {
  display: grid;
  grid-template-columns: minmax(0, 1.35fr) minmax(0, 1fr);
  gap: clamp(1.5rem, 4vw, 4rem);
  align-items: end;
}
@media (max-width: 900px) { .hero-copy { grid-template-columns: minmax(0, 1fr); } }


.hero h1 {
  margin: 0;
  font-family: var(--f-display);
  font-size: clamp(3.33rem, 1.28rem + 6.4vw, 7.17rem);
  font-weight: 400;
  line-height: 0.86;
  letter-spacing: 0.01em;
  text-wrap: balance;
}
.hero h1 em {
  font-style: normal;
  color: transparent;
  background: linear-gradient(180deg, #ffffff 10%, var(--chrome) 62%, #6b7279 100%);
  -webkit-background-clip: text;
  background-clip: text;
}
.hero-side { display: grid; gap: 1.4rem; padding-bottom: 0.4rem; }
.hero-side p { margin: 0; max-width: 42ch; font-size: clamp(1rem, 0.94rem + 0.3vw, 1.12rem); color: var(--ink-2); }
.hero-ctas { display: flex; flex-wrap: wrap; gap: 0.7rem; }

/* ════════════════════════════════════════════════════════
   THE RUN CONSOLE
   ════════════════════════════════════════════════════════ */
.console {
  position: relative;
  min-width: 0;
  border-radius: 1.35rem;
  padding: 1px;
  background: linear-gradient(180deg, rgba(228, 232, 235, 0.42), rgba(228, 232, 235, 0.08) 30%, rgba(228, 232, 235, 0.04) 70%, rgba(228, 232, 235, 0.16));
  box-shadow: 0 50px 100px -40px rgba(0, 0, 0, 0.95), 0 0 0 1px rgba(0, 0, 0, 0.5);
}
.console-body {
  border-radius: calc(1.35rem - 1px);
  overflow: hidden;
  background:
    radial-gradient(90% 40% at 50% -10%, rgba(195, 204, 213, 0.1), rgba(195, 204, 213, 0) 70%),
    linear-gradient(180deg, #2a2f33, #212528);
}

/* Bar */
.c-bar {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.6rem 1rem;
  padding: 0.7rem 0.9rem;
  border-bottom: 1px solid var(--line);
}
.c-bar-title {
  display: inline-flex;
  align-items: center;
  gap: 0.55rem;
  margin-right: auto;
  font-family: var(--f-mono);
  font-size: 1.02rem;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: var(--ink-2);
}
.c-bar-title .dome { width: 1rem; height: 1rem; border-width: 1.5px; }
.c-bar-right { display: flex; align-items: center; flex-wrap: wrap; gap: 0.6rem; }

.field {
  position: relative;
  display: inline-flex;
  align-items: center;
}
.field select {
  appearance: none;
  -webkit-appearance: none;
  height: 2.1rem;
  padding: 0 2rem 0 0.8rem;
  border-radius: 0.55rem;
  border: 1px solid var(--line-2);
  background: var(--well);
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.6);
  font-size: 0.84rem;
  font-weight: 500;
  color: var(--ink);
}
.field::after {
  content: "";
  position: absolute;
  right: 0.75rem;
  width: 0.4rem; height: 0.4rem;
  border-right: 1.5px solid var(--chrome);
  border-bottom: 1.5px solid var(--chrome);
  transform: translateY(-2px) rotate(45deg);
  pointer-events: none;
}

.seg {
  display: inline-flex;
  padding: 2px;
  border-radius: 0.6rem;
  border: 1px solid var(--line-2);
  background: var(--well);
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.6);
}
.seg button {
  height: 1.9rem;
  padding: 0 0.75rem;
  border: 0;
  border-radius: 0.45rem;
  background: transparent;
  font-size: 0.8rem;
  font-weight: 500;
  color: var(--mute);
  white-space: nowrap;
}
.seg button[aria-pressed="true"] {
  background: linear-gradient(180deg, #474e53, #383e42);
  color: var(--ink);
  box-shadow: var(--bevel), 0 2px 6px rgba(0, 0, 0, 0.5);
}

.switch {
  display: inline-flex;
  align-items: center;
  gap: 0.5rem;
  height: 2.1rem;
  padding: 0 0.8rem 0 0.65rem;
  border-radius: 0.55rem;
  border: 1px solid var(--line-2);
  background: linear-gradient(180deg, #3a4044, #2b3034);
  box-shadow: var(--bevel);
  font-family: var(--f-mono);
  font-size: 0.994rem;
  font-weight: 400;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--chrome-hi);
  white-space: nowrap;
}
.switch .dot { width: 0.42rem; height: 0.42rem; }
body.stopped .switch .dot { background: var(--stop); box-shadow: 0 0 8px 1px var(--stop-glow); }

/* Composer */
.c-compose { padding: 1rem 1rem 0.9rem; border-bottom: 1px solid var(--line); }
.c-input {
  position: relative;
  border-radius: 0.9rem;
  border: 1px solid rgba(0, 0, 0, 0.5);
  background: var(--well);
  box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.65);
  transition: box-shadow 0.25s var(--ease), border-color 0.25s var(--ease);
}
.c-input:focus-within { border-color: rgba(127, 227, 106, 0.45); box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.65), 0 0 0 4px rgba(127, 227, 106, 0.1); }
.c-input textarea {
  display: block;
  width: 100%;
  min-height: 4.6rem;
  max-height: 12rem;
  padding: 1rem 1.1rem 0.4rem;
  border: 0;
  background: transparent;
  resize: none;
  font-family: var(--f-display);
  font-size: clamp(1.34rem, 1.25rem + 0.35vw, 1.6rem);
  font-weight: 400;
  line-height: 1.35;
  letter-spacing: 0.01em;
  color: var(--ink);
}
.c-input textarea::placeholder { color: var(--mute); }
.c-input textarea:focus { outline: none; }
.c-input-row {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.45rem 0.55rem 0.55rem 0.7rem;
}
.ctx { display: flex; flex-wrap: wrap; align-items: center; gap: 0.4rem; margin-right: auto; min-width: 0; }
.ctx-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  height: 1.9rem;
  padding: 0 0.6rem;
  border-radius: 0.5rem;
  border: 1px dashed var(--line-2);
  background: transparent;
  font-size: 0.78rem;
  color: var(--ink-2);
  cursor: pointer;
}
.ctx-btn:hover { color: var(--ink); border-color: var(--chrome); }
.ctx-btn svg { width: 0.95rem; height: 0.95rem; }
.ctx-chip {
  display: inline-flex;
  align-items: center;
  gap: 0.35rem;
  height: 1.9rem;
  max-width: 14rem;
  padding: 0 0.3rem 0 0.6rem;
  border-radius: 0.5rem;
  border: 1px solid var(--line-2);
  background: var(--panel);
  font-family: var(--f-mono);
  font-size: 1.02rem;
  color: var(--ink-2);
}
.ctx-chip span { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }
.ctx-chip button { width: 1.3rem; height: 1.3rem; display: grid; place-items: center; padding: 0; border: 0; border-radius: 0.3rem; background: transparent; color: var(--mute); }
.ctx-chip button:hover { color: var(--ink); background: rgba(255, 255, 255, 0.06); }
.kbd { font-family: var(--f-mono); font-size: 0.966rem; color: var(--mute); white-space: nowrap; }
@media (max-width: 560px) { .kbd { display: none; } }

.run-btn {
  display: inline-flex;
  align-items: center;
  gap: 0.55rem;
  height: 2.5rem;
  padding: 0 0.5rem 0 1rem;
  border-radius: 999px;
  border: 1px solid #b6f8a6;
  background: linear-gradient(180deg, var(--ok-hi), #58c541);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.55), inset 0 -1px 0 rgba(0, 0, 0, 0.25), 0 0 26px -8px var(--ok-glow);
  color: #0f2509;
  font-weight: 650;
  font-size: 0.9rem;
  white-space: nowrap;
  transition: filter 0.2s var(--ease), transform 0.15s var(--ease);
}
.run-btn:hover { filter: brightness(1.06); }
.run-btn:active { transform: scale(0.97); }
.run-btn .knob {
  display: grid;
  place-items: center;
  width: 1.65rem; height: 1.65rem;
  border-radius: 50%;
  background: rgba(15, 37, 9, 0.14);
}
.run-btn svg { width: 0.85rem; height: 0.85rem; }
.run-btn .ico-stop { display: none; }
.console.is-running .run-btn {
  border-color: #ffc3c6;
  background: linear-gradient(180deg, #ffb0b4, var(--stop));
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.5), 0 0 26px -8px var(--stop-glow);
  color: #3b0d10;
}
.console.is-running .run-btn .ico-run { display: none; }
.console.is-running .run-btn .ico-stop { display: block; }
.run-btn:disabled { filter: grayscale(1) brightness(0.7); cursor: not-allowed; }

.presets { display: flex; flex-wrap: wrap; gap: 0.45rem; margin-top: 0.8rem; }
.presets-label {
  align-self: center;
  margin-right: 0.2rem;
  font-family: var(--f-mono);
  font-size: 0.937rem;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: var(--mute);
}
.preset {
  height: 2rem;
  padding: 0 0.8rem;
  border-radius: 999px;
  border: 1px solid var(--line-2);
  background: rgba(255, 255, 255, 0.025);
  font-size: 0.8rem;
  color: var(--ink-2);
  white-space: nowrap;
  transition: border-color 0.2s, color 0.2s, background 0.2s;
}
.preset:hover { border-color: var(--chrome); color: var(--ink); background: rgba(255, 255, 255, 0.05); }

/* Run */
.c-run { padding: 1rem 1rem 0; }
.run-head {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.5rem 0.8rem;
  margin-bottom: 0.9rem;
}
.run-title {
  margin: 0;
  min-width: 0;
  margin-right: auto;
  font-family: var(--f-display);
  font-size: 1.43rem;
  font-weight: 400;
  letter-spacing: 0.01em;
  line-height: 1.25;
}
.run-agent { display: block; margin-bottom: 0.15rem; font-family: var(--f-mono); font-size: 0.937rem; font-weight: 400; letter-spacing: 0.07em; text-transform: uppercase; color: var(--mute); }
.pill {
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  height: 1.7rem;
  padding: 0 0.65rem;
  border-radius: 999px;
  border: 1px solid var(--line-2);
  background: var(--well);
  font-family: var(--f-mono);
  font-size: 0.966rem;
  font-weight: 400;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  white-space: nowrap;
}
.pill .dot { width: 0.4rem; height: 0.4rem; }
.pill[data-state="done"] { color: var(--ok); }
.pill[data-state="running"] { color: var(--ink); }
.pill[data-state="running"] .dot { animation: blink 1s steps(2) infinite; }
.pill[data-state="waiting"] { color: var(--warn); }
.pill[data-state="stopped"] { color: var(--stop); }
.pill--ghost { color: var(--mute); border-style: dashed; background: transparent; }
@keyframes blink { 50% { opacity: 0.25; } }

.run-grid {
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1.05fr);
  gap: 1rem;
}
@media (max-width: 760px) { .run-grid { grid-template-columns: minmax(0, 1fr); } }

.pane-label {
  display: flex;
  justify-content: space-between;
  margin-bottom: 0.5rem;
  font-family: var(--f-mono);
  font-size: 0.909rem;
  font-weight: 400;
  letter-spacing: 0.07em;
  text-transform: uppercase;
  color: var(--mute);
}

.plan { list-style: none; margin: 0; padding: 0; display: grid; gap: 0.15rem; }
.step {
  display: grid;
  grid-template-columns: 1.5rem minmax(0, 1fr);
  gap: 0.65rem;
  padding: 0.55rem 0.6rem;
  border-radius: 0.6rem;
  border: 1px solid transparent;
  transition: background 0.3s var(--ease), border-color 0.3s var(--ease);
}
.step-mark {
  display: grid;
  place-items: center;
  width: 1.5rem; height: 1.5rem;
  border-radius: 50%;
  border: 1px solid var(--line-2);
  font-family: var(--f-mono);
  font-size: 0.937rem;
  color: var(--mute);
  font-variant-numeric: tabular-nums;
}
.step-mark svg { width: 0.75rem; height: 0.75rem; }
.step-label { font-size: 0.9rem; line-height: 1.35; color: var(--ink-2); }
.step-tool { display: block; margin-top: 0.15rem; font-family: var(--f-mono); font-size: 0.994rem; color: var(--mute); overflow-wrap: anywhere; }
.step[data-state="running"] { background: rgba(255, 255, 255, 0.035); border-color: var(--line); }
.step[data-state="running"] .step-mark { border-color: var(--ink-2); border-top-color: transparent; animation: spin 0.8s linear infinite; color: transparent; }
.step[data-state="running"] .step-label { color: var(--ink); }
.step[data-state="done"] .step-mark { border-color: rgba(127, 227, 106, 0.5); background: rgba(127, 227, 106, 0.12); color: var(--ok); }
.step[data-state="done"] .step-label { color: var(--ink); }
.step[data-state="waiting"] { background: rgba(242, 169, 94, 0.07); border-color: rgba(242, 169, 94, 0.35); }
.step[data-state="waiting"] .step-mark { border-color: var(--warn); color: var(--warn); }
.step[data-state="waiting"] .step-label { color: var(--ink); }
.step[data-state="skipped"] .step-label { color: var(--mute); text-decoration: line-through; text-decoration-color: rgba(127, 135, 142, 0.6); }
.step[data-state="skipped"] .step-mark { color: var(--mute); }
@keyframes spin { to { transform: rotate(360deg); } }

.gate-tag {
  display: inline-block;
  margin-left: 0.35rem;
  padding: 0 0.35rem;
  border-radius: 0.3rem;
  border: 1px solid rgba(242, 169, 94, 0.45);
  font-family: var(--f-mono);
  font-size: 0.852rem;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  color: var(--warn);
  vertical-align: 0.1em;
}
.gate-actions { display: flex; flex-wrap: wrap; gap: 0.4rem; margin-top: 0.55rem; }
.gate-actions button {
  height: 1.9rem;
  padding: 0 0.8rem;
  border-radius: 0.45rem;
  border: 1px solid var(--line-2);
  background: var(--panel-2);
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--ink);
}
.gate-actions .approve { border-color: #b6f8a6; background: linear-gradient(180deg, var(--ok-hi), #58c541); color: #0f2509; }

.trace {
  height: 15.5rem;
  overflow-y: auto;
  margin: 0;
  padding: 0.75rem 0.85rem;
  border-radius: 0.75rem;
  border: 1px solid rgba(0, 0, 0, 0.5);
  background: var(--well);
  box-shadow: inset 0 2px 10px rgba(0, 0, 0, 0.6);
  font-family: var(--f-mono);
  font-size: 1.02rem;
  line-height: 1.7;
  color: var(--ink-2);
  overscroll-behavior: contain;
}
.trace-line { display: grid; grid-template-columns: 4.6rem minmax(0, 1fr); gap: 0.6rem; }
.trace-line time { color: var(--mute); font-variant-numeric: tabular-nums; }
.trace-line span { overflow-wrap: anywhere; }
.trace-line .fn { color: var(--chrome-hi); }
.trace-line .ok { color: var(--ok); }
.trace-line .wait { color: var(--warn); }
.trace-line .bad { color: var(--stop); }

.result {
  margin-top: 1rem;
  padding: 0.95rem 1.05rem;
  border-radius: 0.8rem;
  border: 1px solid var(--line-2);
  background: linear-gradient(180deg, rgba(255, 255, 255, 0.035), rgba(255, 255, 255, 0.01));
}
.result-label { font-family: var(--f-mono); font-size: 0.909rem; letter-spacing: 0.07em; text-transform: uppercase; color: var(--mute); }
.result p { margin: 0.35rem 0 0; max-width: 72ch; font-size: 0.95rem; color: var(--ink); }

.stats {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  margin: 1rem -1rem 0;
  border-top: 1px solid var(--line);
}
.stat { padding: 0.7rem 1rem 0.8rem; border-right: 1px solid var(--line); min-width: 0; }
.stat:last-child { border-right: 0; }
.stat dt { font-family: var(--f-mono); font-size: 0.88rem; letter-spacing: 0.07em; text-transform: uppercase; color: var(--mute); }
.stat dd { margin: 0.1rem 0 0; font-family: var(--f-mono); font-size: 1.42rem; font-weight: 400; color: var(--ink); font-variant-numeric: tabular-nums; }
@media (max-width: 560px) {
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .stat:nth-child(2) { border-right: 0; }
  .stat:nth-child(-n+2) { border-bottom: 1px solid var(--line); }
}

.c-foot {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 0.5rem 1rem;
  padding: 0.7rem 1rem;
  border-top: 1px solid var(--line);
  background: rgba(0, 0, 0, 0.18);
  font-family: var(--f-mono);
  font-size: 0.937rem;
  letter-spacing: 0.04em;
  color: var(--mute);
}
.c-mode::before {
  content: "";
  display: inline-block;
  width: 0.4rem; height: 0.4rem;
  margin-right: 0.45rem;
  border-radius: 50%;
  vertical-align: 0.06em;
  background: var(--steel);
}
.c-mode[data-mode="live"]::before { background: var(--ok); box-shadow: 0 0 8px 1px var(--ok-glow); }
.c-mode[data-mode="offline"]::before { background: var(--warn); }

/* ════════════════════════════════════════════════════════
   SECTIONS
   ════════════════════════════════════════════════════════ */
.section { padding-block: clamp(4rem, 9vw, 7rem); }
.section-head { display: grid; gap: 0.9rem; max-width: 46rem; margin-bottom: clamp(2rem, 4vw, 3rem); }
.section-head h2 {
  margin: 0;
  font-family: var(--f-display);
  font-size: clamp(2.56rem, 1.54rem + 3vw, 4.35rem);
  font-weight: 400;
  line-height: 0.92;
  letter-spacing: 0.01em;
  text-wrap: balance;
}
.section-head p { margin: 0; max-width: 58ch; color: var(--ink-2); font-size: 1.05rem; }

/* Integrations */
.stack-band { padding-block: 1.6rem; border-block: 1px solid var(--line); background: rgba(0, 0, 0, 0.12); }
.stack-band-label {
  margin-bottom: 1rem;
  text-align: center;
  font-family: var(--f-mono);
  font-size: 0.966rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--mute);
}
.tool-name {
  flex-shrink: 0;
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  font-family: var(--f-display);
  font-size: clamp(1.41rem, 1.15rem + 0.9vw, 1.98rem);
  font-weight: 400;
  letter-spacing: 0.01em;
  color: var(--chrome);
  white-space: nowrap;
}
.tool-name::after { content: ""; width: 0.3rem; height: 0.3rem; margin-left: calc(var(--gap) * 0.5); border-radius: 50%; background: var(--steel); }

/* The run, in five moves */
.moves {
  display: grid;
  grid-template-columns: repeat(5, minmax(0, 1fr));
  border-top: 1px solid var(--line-2);
}
.move { padding: 1.4rem 1.2rem 0 0; display: grid; align-content: start; gap: 0.6rem; min-width: 0; }
.move + .move { padding-left: 1.2rem; border-left: 1px solid var(--line); }
.move-n { font-family: var(--f-mono); font-size: 1.02rem; color: var(--mute); }
.move h3 { margin: 0; font-family: var(--f-display); font-size: 1.73rem; font-weight: 400; letter-spacing: 0.01em; }
.move p { margin: 0; font-size: 0.92rem; color: var(--ink-2); }
.move code { font-family: var(--f-mono); font-size: 1.11rem; color: var(--chrome-hi); }
.move--gate h3 { color: var(--warn); }
@media (max-width: 960px) {
  .moves { grid-template-columns: repeat(2, minmax(0, 1fr)); row-gap: 1.6rem; }
  .move, .move + .move { padding: 1.2rem 1rem 0 0; border-left: 0; border-top: 1px solid var(--line); }
  .moves { border-top: 0; }
}
@media (max-width: 520px) { .moves { grid-template-columns: minmax(0, 1fr); } }

/* Roster */
.roster { display: grid; grid-template-columns: repeat(3, minmax(0, 1fr)); gap: 1rem; }
@media (max-width: 960px) { .roster { grid-template-columns: repeat(2, minmax(0, 1fr)); } }
@media (max-width: 620px) { .roster { grid-template-columns: minmax(0, 1fr); } }
.agent {
  position: relative;
  overflow: hidden;
  display: grid;
  align-content: start;
  gap: 0.8rem;
  padding: 1.35rem;
  border-radius: 1rem;
  border: 1px solid var(--line-2);
  background:
    radial-gradient(90% 60% at 50% -20%, rgba(195, 204, 213, 0.12), rgba(195, 204, 213, 0) 70%),
    linear-gradient(180deg, var(--panel-2), var(--panel));
  box-shadow: var(--bevel), 0 20px 40px -28px rgba(0, 0, 0, 0.95);
  transition: transform 0.45s var(--ease), border-color 0.45s var(--ease);
}
.agent:hover { transform: translateY(-3px); border-color: var(--chrome); }
.agent::after {
  content: "";
  position: absolute;
  inset: 0;
  pointer-events: none;
  background: linear-gradient(105deg, transparent 38%, rgba(228, 232, 235, 0.1) 50%, transparent 62%);
  translate: -120% 0;
  transition: translate 0.9s var(--ease);
}
.agent:hover::after { translate: 120% 0; }
.agent-head { display: flex; align-items: center; gap: 0.75rem; }
.agent-dome {
  position: relative;
  flex-shrink: 0;
  width: 2.6rem; height: 2.6rem;
  border-radius: 50%;
  display: grid; place-items: center;
  color: var(--chrome-hi);
  background: radial-gradient(circle at 50% 28%, #e2e6ea, #9aa0a6 44%, #55595e 72%, #8f959b 100%);
  box-shadow: var(--bevel), 0 8px 14px -8px rgba(0, 0, 0, 0.95);
}
.agent-dome::before {
  content: "";
  position: absolute;
  inset: 0.33rem;
  border-radius: 50%;
  background: radial-gradient(circle at 50% 32%, #9db69f, #5d7466 46%, #26392e 100%);
  box-shadow: inset 0 -2px 5px rgba(0, 0, 0, 0.6), inset 0 2px 3px rgba(255, 255, 255, 0.25);
  transition: background 0.45s var(--ease);
}
.agent:hover .agent-dome::before { background: radial-gradient(circle at 50% 32%, #c4ffb3, var(--ok) 48%, #2d6a21 100%); }
.agent-dome svg { position: relative; z-index: 1; width: 1.1rem; height: 1.1rem; filter: drop-shadow(0 1px 1px rgba(0, 0, 0, 0.6)); }
.agent h3 { margin: 0; font-family: var(--f-display); font-size: 1.54rem; font-weight: 400; letter-spacing: 0.01em; }
.agent-role { display: block; font-family: var(--f-mono); font-size: 0.937rem; letter-spacing: 0.06em; text-transform: uppercase; color: var(--mute); }
.agent p { margin: 0; font-size: 0.92rem; color: var(--ink-2); }
.agent-meta {
  display: grid;
  gap: 0.3rem;
  padding-top: 0.8rem;
  border-top: 1px solid var(--line);
  font-family: var(--f-mono);
  font-size: 0.994rem;
  color: var(--mute);
}
.agent-meta b { font-weight: 500; color: var(--ink-2); }
.agent-meta .gate { color: var(--warn); }

/* Guardrails */
.split { display: grid; grid-template-columns: minmax(0, 1fr) minmax(0, 25rem); gap: clamp(2rem, 5vw, 4.5rem); align-items: center; }
@media (max-width: 900px) { .split { grid-template-columns: minmax(0, 1fr); } }
.guards { list-style: none; margin: 0; padding: 0; display: grid; gap: 0; border-top: 1px solid var(--line-2); }
.guards li { display: grid; grid-template-columns: 9.5rem minmax(0, 1fr); gap: 1rem; padding: 1rem 0; border-bottom: 1px solid var(--line); }
.guards h3 { margin: 0; font-size: 0.95rem; font-weight: 600; }
.guards p { margin: 0; font-size: 0.92rem; color: var(--ink-2); }
@media (max-width: 520px) { .guards li { grid-template-columns: minmax(0, 1fr); gap: 0.3rem; } }

.ledger { --gap: 0.7rem; }
.entry {
  display: grid;
  gap: 0.35rem;
  width: 100%;
  padding: 0.85rem 1rem;
  border-radius: 0.8rem;
  border: 1px solid var(--line-2);
  background: linear-gradient(180deg, var(--panel-2), var(--panel));
  box-shadow: var(--bevel);
}
.entry-top { display: flex; align-items: center; gap: 0.5rem; font-family: var(--f-mono); font-size: 0.937rem; letter-spacing: 0.04em; text-transform: uppercase; color: var(--mute); }
.entry-top time { margin-left: auto; font-variant-numeric: tabular-nums; }
.entry p { margin: 0; font-size: 0.88rem; line-height: 1.4; }
.entry-who { font-family: var(--f-mono); font-size: 0.994rem; color: var(--ok); }
.entry-who.declined { color: var(--stop); }
.entry-who.auto { color: var(--ink-2); }

/* Closing */
.closing { padding-block: clamp(3rem, 7vw, 5rem) 0; overflow: hidden; }
.closing-band .readout { font-family: var(--f-display); font-weight: 400; font-size: clamp(2.82rem, 1.28rem + 5vw, 5.89rem); letter-spacing: 0.01em; text-transform: none; color: var(--chrome-hi); text-shadow: none; }
.closing-band .readout em { color: var(--ok); text-shadow: 0 0 30px var(--ok-glow); }
body.stopped .closing-band .readout { color: var(--chrome); text-shadow: none; }
body.stopped .closing-band .readout em { color: var(--stop); text-shadow: 0 0 30px var(--stop-glow); }
/* The closing plate: same chrome edge as the console, lit from above,
   with an engineering grid that fades out toward the copy. */
.cta {
  position: relative;
  margin-block: clamp(2.5rem, 6vw, 4rem) clamp(3.5rem, 8vw, 6rem);
  padding: 1px;
  border-radius: 1.6rem;
  background: linear-gradient(180deg, rgba(228, 232, 235, 0.5), rgba(228, 232, 235, 0.08) 35%, rgba(228, 232, 235, 0.04) 70%, rgba(228, 232, 235, 0.2));
  box-shadow: 0 60px 120px -50px rgba(0, 0, 0, 0.95), 0 0 0 1px rgba(0, 0, 0, 0.5);
}
.cta-body {
  position: relative;
  overflow: hidden;
  isolation: isolate;
  display: grid;
  grid-template-columns: minmax(0, 1.15fr) minmax(0, 1fr);
  gap: clamp(2rem, 5vw, 4.5rem);
  align-items: center;
  padding: clamp(1.75rem, 5vw, 4rem);
  border-radius: calc(1.6rem - 1px);
  background:
    radial-gradient(70% 90% at 12% -10%, rgba(195, 204, 213, 0.2), rgba(195, 204, 213, 0) 60%),
    radial-gradient(50% 70% at 100% 110%, rgba(127, 227, 106, 0.08), rgba(127, 227, 106, 0) 70%),
    linear-gradient(180deg, #2c3135, #1f2326);
}
.cta-body::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  pointer-events: none;
  background-image:
    linear-gradient(rgba(228, 232, 235, 0.05) 1px, transparent 1px),
    linear-gradient(90deg, rgba(228, 232, 235, 0.05) 1px, transparent 1px);
  background-size: 44px 44px;
  background-position: -1px -1px;
  mask-image: radial-gradient(80% 90% at 85% 50%, #000 0%, transparent 75%);
  -webkit-mask-image: radial-gradient(80% 90% at 85% 50%, #000 0%, transparent 75%);
}
@media (max-width: 900px) { .cta-body { grid-template-columns: minmax(0, 1fr); } }

.cta-copy { display: grid; gap: 1.2rem; align-content: start; min-width: 0; }
.cta h2 {
  margin: 0;
  font-family: var(--f-display);
  font-size: clamp(2.94rem, 1.54rem + 3.6vw, 5.38rem);
  font-weight: 400;
  line-height: 0.88;
  letter-spacing: 0.01em;
  text-wrap: balance;
}
.cta h2 em {
  font-style: normal;
  color: transparent;
  background: linear-gradient(180deg, #ffffff 10%, var(--chrome) 62%, #6b7279 100%);
  -webkit-background-clip: text;
  background-clip: text;
}
.cta-copy > p { margin: 0; max-width: 44ch; font-size: 1.06rem; color: var(--ink-2); }
.cta-actions { display: flex; flex-wrap: wrap; gap: 0.7rem; margin-top: 0.4rem; }
.btn--lg { min-height: 3.2rem; padding: 0 1.5rem; font-size: 0.98rem; }
.btn--light svg { transition: transform 0.25s var(--ease); }
.btn--light:hover svg { transform: translateX(3px); }
.cta-terms {
  list-style: none;
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem 1.4rem;
  margin: 0.6rem 0 0;
  padding: 1.1rem 0 0;
  border-top: 1px solid var(--line);
  font-family: var(--f-mono);
  font-size: 0.994rem;
  letter-spacing: 0.03em;
  color: var(--mute);
}
.cta-terms li { display: inline-flex; align-items: center; gap: 0.5rem; }
.cta-terms li::before {
  content: "";
  width: 0.7rem; height: 0.4rem;
  border-left: 1.5px solid var(--ok);
  border-bottom: 1.5px solid var(--ok);
  transform: translateY(-2px) rotate(-45deg);
}

/* The shift card: a first week, written like a work order. */
.shift {
  min-width: 0;
  border-radius: 1.1rem;
  border: 1px solid var(--line-2);
  background: linear-gradient(180deg, rgba(21, 24, 26, 0.92), rgba(21, 24, 26, 0.75));
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.05), 0 30px 60px -30px rgba(0, 0, 0, 0.95);
  backdrop-filter: blur(6px);
  -webkit-backdrop-filter: blur(6px);
  overflow: hidden;
}
.shift-head {
  display: flex;
  align-items: center;
  gap: 0.85rem;
  padding: 1rem 1.1rem;
  border-bottom: 1px solid var(--line);
}
.shift-dome {
  flex-shrink: 0;
  width: 2.6rem; height: 2.6rem;
  border-radius: 50%;
  border: 3px solid var(--chrome);
  background: radial-gradient(circle at 50% 28%, var(--ok-hi), var(--ok) 50%, #2d6a21 100%);
  box-shadow: inset 0 -3px 6px rgba(0, 0, 0, 0.35), inset 0 2px 3px rgba(255, 255, 255, 0.5), 0 0 26px -4px var(--ok-glow);
}
body.stopped .shift-dome {
  background: radial-gradient(circle at 50% 28%, #ffd2c4, var(--stop) 55%, #7a2a2e);
  box-shadow: inset 0 -3px 6px rgba(0, 0, 0, 0.35), inset 0 2px 3px rgba(255, 255, 255, 0.5), 0 0 26px -4px var(--stop-glow);
}
.shift-name { display: grid; margin-right: auto; min-width: 0; }
.shift-name span { font-family: var(--f-mono); font-size: 0.909rem; letter-spacing: 0.07em; text-transform: uppercase; color: var(--mute); }
.shift-name strong { font-family: var(--f-display); font-size: 1.47rem; font-weight: 400; letter-spacing: 0.01em; }
.shift .pill { color: var(--warn); }

.week { list-style: none; margin: 0; padding: 0.6rem 1.1rem; }
.week li {
  position: relative;
  display: grid;
  grid-template-columns: 2.6rem minmax(0, 1fr);
  gap: 0.85rem;
  padding: 0.75rem 0;
}
.week li + li { border-top: 1px dashed var(--line); }
.day {
  display: grid;
  place-items: center;
  height: 1.7rem;
  border-radius: 0.4rem;
  border: 1px solid var(--line-2);
  font-family: var(--f-mono);
  font-size: 0.909rem;
  font-weight: 400;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--mute);
}
.week strong { display: block; font-size: 0.92rem; font-weight: 600; line-height: 1.35; color: var(--ink-2); }
.week li div span { display: block; margin-top: 0.15rem; font-size: 0.82rem; color: var(--mute); }
.week li[data-state="done"] .day { border-color: rgba(127, 227, 106, 0.45); background: rgba(127, 227, 106, 0.1); color: var(--ok); }
.week li[data-state="done"] strong { color: var(--ink); }
.week li[data-state="now"] .day { border-color: var(--chrome-hi); background: var(--chrome-hi); color: #15181a; }
.week li[data-state="now"] strong { color: var(--ink); }

.shift-foot {
  display: flex;
  align-items: center;
  gap: 0.9rem;
  padding: 0.85rem 1.1rem;
  border-top: 1px solid var(--line);
  background: rgba(0, 0, 0, 0.2);
  font-family: var(--f-mono);
  font-size: 0.966rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--ink-2);
  font-variant-numeric: tabular-nums;
}
.shift-meter { flex: 1; height: 4px; border-radius: 999px; background: rgba(255, 255, 255, 0.08); overflow: hidden; }
.shift-meter i { display: block; width: 50%; height: 100%; border-radius: inherit; background: linear-gradient(90deg, #58c541, var(--ok-hi)); box-shadow: 0 0 10px var(--ok-glow); }

footer { padding-block: 2rem 3rem; border-top: 1px solid var(--line); color: var(--mute); font-size: 0.86rem; }
.footer-row { display: flex; justify-content: space-between; gap: 1rem; flex-wrap: wrap; }

/* ── VT323 in the machine ─────────────────────────────────
   The pixel face is the machine's voice: headlines, readouts, logs, plates.
   Geist stays for paragraphs. Rendered crisp, lit like phosphor, and laid
   over scanlines wherever it sits on a dark screen. */
h1, h2, h3, .readout, .trace, .plate, .pill, .stat dd, .tool-name, .run-title, .c-input textarea, .brand, .shift-name strong {
  -webkit-font-smoothing: none;
  font-smooth: never;
}
.hero h1, .section-head h2, .cta h2 { text-transform: uppercase; }
.hero h1 { text-shadow: 0 0 28px rgba(228, 232, 235, 0.12); }
.readout, .trace .ok, .plate b, .stat dd { text-shadow: 0 0 10px var(--ok-glow); }
.trace, .shift, .c-input, .plate {
  background-image: repeating-linear-gradient(180deg, rgba(255, 255, 255, 0.025) 0 1px, transparent 1px 3px);
}
.trace { font-size: 1.05rem; line-height: 1.35; }
.trace-line { grid-template-columns: 5rem minmax(0, 1fr); }
.c-input textarea { font-size: clamp(1.45rem, 1.3rem + 0.5vw, 1.75rem); line-height: 1.1; letter-spacing: 0.01em; }
.stat dd { font-size: 1.6rem; line-height: 1.1; color: var(--chrome-hi); }
.move h3, .agent h3 { font-size: 1.75rem; line-height: 1; }
.brand { font-size: 1.6rem; letter-spacing: 0.04em; }
.btn, .run-btn, .preset, .seg button, .field select, .ctx-btn { font-family: var(--f-body); }
::selection { background: var(--ok); color: #0f2509; }

/* ── Motion ────────────────────────────────────────────────
   One entrance for the hero on load, then a single quiet reveal per
   section as it scrolls in. Everything is visible without script; the
   hidden state only exists once the observer is running. */
:root { --ease-out: cubic-bezier(0.16, 0.84, 0.24, 1); }

@keyframes rise {
  from { opacity: 0; translate: 0 18px; filter: blur(6px); }
  to   { opacity: 1; translate: 0 0;    filter: blur(0); }
}
@keyframes wipe {
  from { clip-path: inset(0 0 100% 0); opacity: 0.4; }
  to   { clip-path: inset(0 0 0 0);    opacity: 1; }
}
@keyframes console-in {
  from { opacity: 0; translate: 0 34px; scale: 0.985; }
  to   { opacity: 1; translate: 0 0;    scale: 1; }
}
@keyframes fade-in { from { opacity: 0; } }
@keyframes edge-sweep {
  from { translate: -60% 0; opacity: 0; }
  20%  { opacity: 1; }
  to   { translate: 160% 0; opacity: 0; }
}

/* Hero, on load: headline wipe, copy, then the console lands
   and a light runs once along its chrome edge. */
.hero-reels { animation: fade-in 1.6s var(--ease-out) both; }
.hero h1 { animation: wipe 1s steps(14, end) 0.15s both; }
.hero-side > p { animation: rise 0.9s var(--ease-out) 0.4s both; }
.hero-ctas { animation: rise 0.9s var(--ease-out) 0.5s both; }
.console { animation: console-in 1.1s var(--ease-out) 0.6s both; }
.console::after {
  content: "";
  position: absolute;
  top: 0; left: 0;
  width: 40%;
  height: 1px;
  pointer-events: none;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.9), transparent);
  animation: edge-sweep 1.6s var(--ease-out) 1.35s both;
}
.topbar { animation: fade-in 0.8s var(--ease-out) both; }

/* Scroll reveals */
html.reveal-ready [data-reveal]:not(.is-in) { opacity: 0; }
[data-reveal].is-in { animation: rise 0.9s var(--ease-out) calc(var(--i, 0) * 75ms) both; }
[data-reveal="wipe"].is-in { animation: wipe 0.9s steps(12, end) calc(var(--i, 0) * 75ms) both; }
[data-reveal="fade"].is-in { animation: fade-in 1.2s var(--ease-out) calc(var(--i, 0) * 75ms) both; }

@media (prefers-reduced-motion: reduce) {
  .hero-reels, .hero h1, .hero-side > p, .hero-ctas, .console, .topbar, [data-reveal].is-in { animation: none !important; }
  .console::after { display: none; }
  html.reveal-ready [data-reveal]:not(.is-in) { opacity: 1; }
}
</style>
</head>
<body class="spinning">
<a class="sr-only" href="#main">Skip to content</a>

<header class="topbar" data-section="nav">
  <a class="brand" href="#top"><span class="dome" aria-hidden="true"></span>SKEWSHOP</a>
  <nav aria-label="Primary">
    <a href="#console">Run console</a>
    <a href="#how">How a run works</a>
    <a href="#agents">Agents</a>
    <a href="#guardrails">Guardrails</a>
  </nav>
  <div class="topbar-end">
    <span class="plate" id="fleetPlate" role="status">Fleet <b>On shift</b></span>
    <a class="btn btn--light btn--sm" href="#console">Try a run</a>
  </div>
</header>

<main id="main">
  <!-- ─── HERO ─── -->
  <section class="hero" id="top" data-section="hero">
    <div class="hero-reels" aria-hidden="true">
      <div class="marquee marquee--skew " id="laneA" style="--duration: 70s"><div class="marquee__group"><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Support desk</span><time>0:38</time></div><p>Closed 23 tickets, escalated 2 billing disputes</p><span class="tile-tools">zendesk · slack</span></article><article class="tile"><div class="tile-top"><span class="dot dot--warn"></span><span>Finance close</span><time>1:12</time></div><p>Waiting on approval: 6 adjusting entries</p><span class="tile-tools">stripe · postgres</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Inventory</span><time>0:51</time></div><p>Drafted 3 restock orders under two weeks of cover</p><span class="tile-tools">shopify · gmail</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Catalog QA</span><time>0:24</time></div><p>Fixed 41 product pages with missing alt text</p><span class="tile-tools">shopify</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Research</span><time>2:06</time></div><p>Priced 18 competitor SKUs, flagged 4 undercuts</p><span class="tile-tools">web · sheets</span></article></div><div class="marquee__group" aria-hidden="true"><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Support desk</span><time>0:38</time></div><p>Closed 23 tickets, escalated 2 billing disputes</p><span class="tile-tools">zendesk · slack</span></article><article class="tile"><div class="tile-top"><span class="dot dot--warn"></span><span>Finance close</span><time>1:12</time></div><p>Waiting on approval: 6 adjusting entries</p><span class="tile-tools">stripe · postgres</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Inventory</span><time>0:51</time></div><p>Drafted 3 restock orders under two weeks of cover</p><span class="tile-tools">shopify · gmail</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Catalog QA</span><time>0:24</time></div><p>Fixed 41 product pages with missing alt text</p><span class="tile-tools">shopify</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Research</span><time>2:06</time></div><p>Priced 18 competitor SKUs, flagged 4 undercuts</p><span class="tile-tools">web · sheets</span></article></div></div>
      <div class="marquee marquee--rails marquee--skew" style="--duration: 90s"><div class="marquee__group"><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p></div><div class="marquee__group" aria-hidden="true"><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p><p class="readout">Brief it <em>·</em> gate it <em>·</em> ship it <em>·</em></p></div></div>
      <div class="marquee marquee--skew marquee--reverse" style="--duration: 70s"><div class="marquee__group"><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Outbound</span><time>0:44</time></div><p>Sent 12 wholesale follow-ups, 3 replies booked</p><span class="tile-tools">gmail · hubspot</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Returns</span><time>0:33</time></div><p>Issued 9 return labels, refunded 4 orders</p><span class="tile-tools">shopify · shippo</span></article><article class="tile"><div class="tile-top"><span class="dot dot--warn"></span><span>Support desk</span><time>0:19</time></div><p>Waiting on approval: refund $84.20 on #4471</p><span class="tile-tools">zendesk · stripe</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Reviews</span><time>0:57</time></div><p>Answered 16 reviews, routed 2 complaints</p><span class="tile-tools">trustpilot · linear</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Finance close</span><time>1:40</time></div><p>Matched 312 of 318 payouts to the ledger</p><span class="tile-tools">stripe · postgres</span></article></div><div class="marquee__group" aria-hidden="true"><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Outbound</span><time>0:44</time></div><p>Sent 12 wholesale follow-ups, 3 replies booked</p><span class="tile-tools">gmail · hubspot</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Returns</span><time>0:33</time></div><p>Issued 9 return labels, refunded 4 orders</p><span class="tile-tools">shopify · shippo</span></article><article class="tile"><div class="tile-top"><span class="dot dot--warn"></span><span>Support desk</span><time>0:19</time></div><p>Waiting on approval: refund $84.20 on #4471</p><span class="tile-tools">zendesk · stripe</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Reviews</span><time>0:57</time></div><p>Answered 16 reviews, routed 2 complaints</p><span class="tile-tools">trustpilot · linear</span></article><article class="tile"><div class="tile-top"><span class="dot dot--ok"></span><span>Finance close</span><time>1:40</time></div><p>Matched 312 of 318 payouts to the ledger</p><span class="tile-tools">stripe · postgres</span></article></div></div>
    </div>
    <div class="hero-scrim" aria-hidden="true"></div>

    <div class="hero-inner wrap">
      <div class="hero-copy">
        <div>
          <h1>Your back office, <em>on autopilot.</em></h1>
        </div>
        <div class="hero-side">
          <p>SKEWSHOP agents work your inbox, ledger and stockroom in the tools you already use. They plan every job, show their work, and stop for your OK before money moves or a customer hears from them.</p>
          <div class="hero-ctas">
            <a class="btn btn--light" href="#console">Brief an agent</a>
            <a class="btn" href="#guardrails">See the guardrails</a>
          </div>
        </div>
      </div>

      <!-- ─── THE RUN CONSOLE ─── -->
      <section class="console" id="console" data-component="run-console" aria-label="Run console">
        <div class="console-body">
          <div class="c-bar">
            <span class="c-bar-title"><span class="dome" aria-hidden="true"></span>Run console</span>
            <div class="c-bar-right">
              <label class="sr-only" for="agentSelect">Agent</label>
              <span class="field">
                <select id="agentSelect">
                  <option value="auto">Auto-assign agent</option>
                  <option value="Support desk">Support desk</option>
                  <option value="Finance close">Finance close</option>
                  <option value="Inventory">Inventory</option>
                  <option value="Outbound">Outbound</option>
                  <option value="Research">Research</option>
                  <option value="Catalog QA">Catalog QA</option>
                </select>
              </span>
              <div class="seg" role="group" aria-label="Approvals">
                <button type="button" id="modeAsk" aria-pressed="true">Ask before acting</button>
                <button type="button" id="modeAuto" aria-pressed="false">Autonomous</button>
              </div>
              <button type="button" class="switch" id="fleetSwitch" aria-pressed="false"><span class="dot"></span><span id="fleetSwitchLabel">Pause fleet</span></button>
            </div>
          </div>

          <form class="c-compose" id="runForm" autocomplete="off">
            <div class="c-input">
              <label class="sr-only" for="brief">Brief</label>
              <textarea id="brief" rows="2" placeholder="What should get done? e.g. Chase every unpaid wholesale invoice older than 30 days"></textarea>
              <div class="c-input-row">
                <div class="ctx" id="ctx">
                  <label class="ctx-btn" for="ctxFile">
                    <svg aria-hidden="true" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"><path d="m18.375 12.739-7.693 7.693a4.5 4.5 0 0 1-6.364-6.364l10.94-10.94A3 3 0 1 1 19.5 7.372L8.552 18.32m.009-.01-.01.01m5.699-9.941-7.81 7.81a1.5 1.5 0 0 0 2.112 2.13"/></svg>
                    Add context
                  </label>
                  <input id="ctxFile" type="file" class="sr-only" tabindex="-1" />
                </div>
                <span class="kbd">⏎ to run · ⇧⏎ new line</span>
                <button type="submit" class="run-btn" id="runBtn">
                  <span id="runBtnLabel">Run</span>
                  <span class="knob" aria-hidden="true">
                    <svg class="ico-run" viewBox="0 0 24 24" fill="currentColor"><path d="M7 4.5v15a1 1 0 0 0 1.5.86l12.5-7.5a1 1 0 0 0 0-1.72L8.5 3.64A1 1 0 0 0 7 4.5Z"/></svg>
                    <svg class="ico-stop" viewBox="0 0 24 24" fill="currentColor"><rect x="5" y="5" width="14" height="14" rx="2.5"/></svg>
                  </span>
                </button>
              </div>
            </div>
            <div class="presets" id="presets">
              <span class="presets-label">Try</span>
              <button type="button" class="preset" data-preset="support">Triage the support inbox</button>
              <button type="button" class="preset" data-preset="finance">Reconcile last week's payouts</button>
              <button type="button" class="preset" data-preset="inventory">Draft restock orders</button>
            </div>
          </form>

          <div class="c-run" id="run" aria-live="polite">
            <div class="run-head">
              <h2 class="run-title"><span class="run-agent" id="runAgent">Support desk</span><span id="runTitle">Triage this morning's support inbox</span></h2>
              <span class="pill pill--ghost" id="runKind">Example run</span>
              <span class="pill" id="runState" data-state="done"><span class="dot"></span><span id="runStateLabel">Done</span></span>
            </div>
            <div class="run-grid">
              <div>
                <div class="pane-label"><span>Plan</span><span id="planCount">5 steps</span></div>
                <ol class="plan" id="plan"></ol>
              </div>
              <div>
                <div class="pane-label"><span>Activity</span><span>tool calls</span></div>
                <div class="trace" id="trace" role="log" aria-label="Agent activity"></div>
              </div>
            </div>
            <div class="result" id="result">
              <span class="result-label">Outcome</span>
              <p id="resultText"></p>
            </div>
            <dl class="stats">
              <div class="stat"><dt>Steps</dt><dd id="statSteps">5 / 5</dd></div>
              <div class="stat"><dt>Tool calls</dt><dd id="statCalls">9</dd></div>
              <div class="stat"><dt>Approvals</dt><dd id="statGates">1</dd></div>
              <div class="stat"><dt>Elapsed</dt><dd id="statTime">0:38</dd></div>
            </dl>
          </div>

          <div class="c-foot">
            <span class="c-mode" id="planner" data-mode="pending">Planner connecting</span>
            <span>Preview runs are simulated. Nothing leaves this page.</span>
          </div>
        </div>
      </section>
    </div>
  </section>

  <!-- ─── STACK ─── -->
  <section class="stack-band" data-section="integrations" aria-label="Integrations">
    <div class="stack-band-label">Works inside the tools your shop already runs on</div>
    <div class="marquee" style="--duration: 50s; --gap: 2.4rem"><div class="marquee__group"><span class="tool-name">Shopify</span><span class="tool-name">Stripe</span><span class="tool-name">Zendesk</span><span class="tool-name">Gmail</span><span class="tool-name">Slack</span><span class="tool-name">Postgres</span><span class="tool-name">HubSpot</span><span class="tool-name">Linear</span><span class="tool-name">Google Sheets</span><span class="tool-name">Shippo</span><span class="tool-name">Notion</span><span class="tool-name">QuickBooks</span></div><div class="marquee__group" aria-hidden="true"><span class="tool-name">Shopify</span><span class="tool-name">Stripe</span><span class="tool-name">Zendesk</span><span class="tool-name">Gmail</span><span class="tool-name">Slack</span><span class="tool-name">Postgres</span><span class="tool-name">HubSpot</span><span class="tool-name">Linear</span><span class="tool-name">Google Sheets</span><span class="tool-name">Shippo</span><span class="tool-name">Notion</span><span class="tool-name">QuickBooks</span></div></div>
  </section>

  <!-- ─── HOW A RUN WORKS ─── -->
  <section class="section wrap" id="how" data-section="how-it-works">
    <div class="section-head">
      <h2>Every job takes the same five steps, in the same order.</h2>
      <p>The order is the product. An agent can't act before it has a plan you can read, and it can't touch money or customers without passing a gate.</p>
    </div>
    <div class="moves">
      <div class="move"><span class="move-n">01</span><h3>Brief</h3><p>One sentence in plain language. Attach a file or a thread if it helps.</p></div>
      <div class="move"><span class="move-n">02</span><h3>Plan</h3><p>The agent writes the steps and names the tool for each one before it starts.</p></div>
      <div class="move"><span class="move-n">03</span><h3>Act</h3><p>Every call is logged as it happens: <code>stripe.payouts.list</code>, inputs, result.</p></div>
      <div class="move move--gate"><span class="move-n">04</span><h3>Gate</h3><p>Refunds, ledger writes and customer emails wait for your approval, or for a policy you set.</p></div>
      <div class="move"><span class="move-n">05</span><h3>Report</h3><p>A short outcome, and the full replay, posted where your team already reads.</p></div>
    </div>
  </section>

  <!-- ─── AGENTS ─── -->
  <section class="section wrap" id="agents" data-section="agents" style="padding-top: 0">
    <div class="section-head">
      <h2>Six agents, each with one job and a short leash.</h2>
      <p>Each one gets only the tools its job needs and its own approval rules. Add them one at a time.</p>
    </div>
    <div class="roster"><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 13v-1a8 8 0 0 1 16 0v1"/><rect x="3" y="13" width="4" height="6" rx="1.5"/><rect x="17" y="13" width="4" height="6" rx="1.5"/></svg></span><div><span class="agent-role">Customer service</span><h3>Support desk</h3></div></div><p>Reads the inbox, answers what it can, and hands the rest to a person with the order history already attached.</p><div class="agent-meta"><span>Tools <b>zendesk · gmail · slack</b></span><span class="gate">Asks first: Refunds over $50</span></div></article><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 19h16M6 16V9M10 16V6M14 16v-5M18 16V8"/></svg></span><div><span class="agent-role">Bookkeeping</span><h3>Finance close</h3></div></div><p>Matches payouts to the ledger every morning and drafts adjusting entries for anything that doesn&#x27;t reconcile.</p><div class="agent-meta"><span>Tools <b>stripe · postgres · quickbooks</b></span><span class="gate">Asks first: Any ledger write</span></div></article><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m3 7 9-4 9 4-9 4-9-4Z"/><path d="M3 7v10l9 4 9-4V7M12 11v10"/></svg></span><div><span class="agent-role">Operations</span><h3>Inventory</h3></div></div><p>Forecasts cover per SKU, drafts purchase orders and emails suppliers before you run out.</p><div class="agent-meta"><span>Tools <b>shopify · sheets · gmail</b></span><span class="gate">Asks first: Every purchase order</span></div></article><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M4 6h16v12H4z"/><path d="m4 7 8 6 8-6"/></svg></span><div><span class="agent-role">Growth</span><h3>Outbound</h3></div></div><p>Follows up with wholesale leads and lapsed customers in your voice, from your own inbox.</p><div class="agent-meta"><span>Tools <b>gmail · hubspot</b></span><span class="gate">Asks first: Sends over 50 recipients</span></div></article><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="6"/><path d="m20 20-4.5-4.5"/></svg></span><div><span class="agent-role">Merchandising</span><h3>Research</h3></div></div><p>Checks competitor prices and reviews on a schedule and writes up what changed.</p><div class="agent-meta"><span>Tools <b>web · sheets · notion</b></span><span class="gate">Asks first: None, it only reads</span></div></article><article class="agent"><div class="agent-head"><span class="agent-dome" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="m5 12 4.5 4.5L19 7"/></svg></span><div><span class="agent-role">Storefront</span><h3>Catalog QA</h3></div></div><p>Finds broken links, missing alt text and stale prices on product pages, then fixes them.</p><div class="agent-meta"><span>Tools <b>shopify · linear</b></span><span class="gate">Asks first: Price changes</span></div></article></div>
  </section>

  <!-- ─── GUARDRAILS ─── -->
  <section class="section wrap" id="guardrails" data-section="guardrails" style="padding-top: 0">
    <div class="split">
      <div>
        <div class="section-head">
          <h2>Nothing irreversible happens without a gate.</h2>
          <p>Every approval, decline and policy decision lands in one ledger, live, so you can see the fleet working without watching it.</p>
        </div>
        <ul class="guards">
          <li><h3>Approval gates</h3><p>Choose which actions need a person: refunds, ledger writes, purchase orders, bulk email.</p></li>
          <li><h3>Spend caps</h3><p>Dollar and recipient limits per agent, per run and per day. Over the cap means declined, not queued.</p></li>
          <li><h3>Scoped access</h3><p>Each agent holds its own read or write grants. The research agent can't send email at all.</p></li>
          <li><h3>Kill switch</h3><p>One switch pauses every agent mid-step. Try it in the console above; the whole page stops with it.</p></li>
        </ul>
      </div>
      <div>
        <div class="pane-label"><span>Approval ledger</span><span>today</span></div>
        <div class="marquee marquee--vertical ledger" style="--duration: 40s"><div class="marquee__group"><div class="entry"><div class="entry-top"><span class="dot dot--warn"></span><span>Support desk</span><time>09:41</time></div><p>Refund $84.20 to order #4471 (damaged in transit)</p><span class="entry-who ">Approved by support lead</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Inventory</span><time>09:37</time></div><p>Email PO-2291 to Northfield Ceramics, 240 units</p><span class="entry-who ">Approved by ops lead</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Catalog QA</span><time>09:30</time></div><p>Update alt text on 41 product pages</p><span class="entry-who auto">Auto-approved by policy: content edits</span></div><div class="entry"><div class="entry-top"><span class="dot dot--stop"></span><span>Outbound</span><time>09:22</time></div><p>Send discount code to 1,900 lapsed customers</p><span class="entry-who declined">Declined: over the 500-recipient cap</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Finance close</span><time>09:15</time></div><p>Post 6 adjusting entries, net −$212.40</p><span class="entry-who ">Approved by controller</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Returns</span><time>09:04</time></div><p>Refund 4 orders under $40</p><span class="entry-who auto">Auto-approved by policy: refunds under $50</span></div></div><div class="marquee__group" aria-hidden="true"><div class="entry"><div class="entry-top"><span class="dot dot--warn"></span><span>Support desk</span><time>09:41</time></div><p>Refund $84.20 to order #4471 (damaged in transit)</p><span class="entry-who ">Approved by support lead</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Inventory</span><time>09:37</time></div><p>Email PO-2291 to Northfield Ceramics, 240 units</p><span class="entry-who ">Approved by ops lead</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Catalog QA</span><time>09:30</time></div><p>Update alt text on 41 product pages</p><span class="entry-who auto">Auto-approved by policy: content edits</span></div><div class="entry"><div class="entry-top"><span class="dot dot--stop"></span><span>Outbound</span><time>09:22</time></div><p>Send discount code to 1,900 lapsed customers</p><span class="entry-who declined">Declined: over the 500-recipient cap</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Finance close</span><time>09:15</time></div><p>Post 6 adjusting entries, net −$212.40</p><span class="entry-who ">Approved by controller</span></div><div class="entry"><div class="entry-top"><span class="dot dot--ok"></span><span>Returns</span><time>09:04</time></div><p>Refund 4 orders under $40</p><span class="entry-who auto">Auto-approved by policy: refunds under $50</span></div></div></div>
      </div>
    </div>
  </section>

  <!-- ─── CLOSING ─── -->
  <section class="closing" data-section="cta" aria-label="Get started">
    <div class="marquee marquee--skew-reverse closing-band" style="--duration: 45s"><div class="marquee__group"><p class="readout">Brief it · Gate it · <em>Ship it</em> ·</p><p class="readout">Brief it · Gate it · <em>Ship it</em> ·</p></div><div class="marquee__group" aria-hidden="true"><p class="readout">Brief it · Gate it · <em>Ship it</em> ·</p><p class="readout">Brief it · Gate it · <em>Ship it</em> ·</p></div></div>
    <div class="wrap">
      <div class="cta">
        <div class="cta-body">
          <div class="cta-copy">
            <h2>Put one agent <em>on shift</em> this week.</h2>
            <p>Start with the support desk in ask-first mode. It drafts, you approve, and by Friday you know exactly what it does without you.</p>
            <div class="cta-actions">
              <a class="btn btn--light btn--lg" href="#console">Brief an agent
                <svg aria-hidden="true" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
              </a>
              <a class="btn btn--lg" href="#guardrails">Read the guardrails</a>
            </div>
            <ul class="cta-terms">
              <li>Ask-first by default</li>
              <li>Read-only until you approve</li>
              <li>One kill switch for everything</li>
            </ul>
          </div>

          <div class="shift" aria-label="A first week with the support desk agent">
            <div class="shift-head">
              <span class="shift-dome" aria-hidden="true"></span>
              <div class="shift-name">
                <span>Shift 01</span>
                <strong>Support desk</strong>
              </div>
              <span class="pill"><span class="dot dot--warn"></span>Ask first</span>
            </div>
            <ol class="week">
              <li data-state="done">
                <span class="day">Mon</span>
                <div><strong>Connect Zendesk and Gmail</strong><span>Read access only. About 10 minutes.</span></div>
              </li>
              <li data-state="done">
                <span class="day">Tue</span>
                <div><strong>First runs, every reply gated</strong><span>You approve or skip each one from Slack.</span></div>
              </li>
              <li data-state="now">
                <span class="day">Wed</span>
                <div><strong>Review the replays</strong><span>Every tool call, input and result, in order.</span></div>
              </li>
              <li>
                <span class="day">Fri</span>
                <div><strong>Set your first policy</strong><span>Example: refunds under $50 go through on their own.</span></div>
              </li>
            </ol>
            <div class="shift-foot">
              <span>Live by Friday</span>
              <span class="shift-meter" aria-hidden="true"><i></i></span>
              <span class="mono">2 / 4</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</main>

<footer data-section="footer">
  <div class="wrap footer-row">
    <span>SKEWSHOP is a fictional product. The marquees are real CSS.</span>
    <span>Lanes: two groups, one keyframe, one translate.</span>
  </div>
</footer>
<script>
/* ═══════════════════════════════════════════════════════════════
   THE RUN CONSOLE
   A brief becomes a plan, the plan runs step by step with every tool call
   logged, and risky steps stop at a gate. Plans come from Claude when the
   page is opened inside Claude; otherwise from a scripted planner. The run
   itself is always simulated: nothing leaves the page.
   ═══════════════════════════════════════════════════════════════ */
(function () {
  "use strict";

  var REDUCED = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
  var $ = function (id) { return document.getElementById(id); };

  var body = document.body;
  var consoleEl = $("console");
  var form = $("runForm");
  var brief = $("brief");
  var agentSelect = $("agentSelect");
  var modeAsk = $("modeAsk"), modeAuto = $("modeAuto");
  var fleetSwitch = $("fleetSwitch"), fleetSwitchLabel = $("fleetSwitchLabel");
  var fleetPlate = $("fleetPlate");
  var runBtnLabel = $("runBtnLabel");
  var ctx = $("ctx"), ctxFile = $("ctxFile");
  var planEl = $("plan"), traceEl = $("trace");
  var runAgent = $("runAgent"), runTitle = $("runTitle"), runKind = $("runKind");
  var runState = $("runState"), runStateLabel = $("runStateLabel");
  var planCount = $("planCount"), resultText = $("resultText");
  var statSteps = $("statSteps"), statCalls = $("statCalls"), statGates = $("statGates"), statTime = $("statTime");
  var planner = $("planner");
  var laneA = $("laneA");

  /* ── Scripted plans ───────────────────────────────────────── */
  var PRESETS = {
    support: {
      brief: "Triage this morning's support inbox",
      agent: "Support desk",
      title: "Triage this morning's support inbox",
      steps: [
        { label: "Read new tickets since 6 a.m.", call: 'zendesk.search({ status: "new", since: "06:00" })', out: "41 tickets" },
        { label: "Sort them by intent and urgency", call: "classify(tickets: 41)", out: "23 routine · 16 need a person · 2 billing" },
        { label: "Draft replies for the 23 routine tickets", call: 'draft.reply(count: 23, voice: "house")', out: "23 drafts ready" },
        { label: "Send the 23 replies and close those tickets", call: 'zendesk.update(count: 23, status: "solved")', out: "23 solved", gate: true },
        { label: "Escalate the 2 billing disputes to #finance", call: 'slack.post("#finance", threads: 2)', out: "posted" }
      ],
      summary: "23 tickets answered and closed. 2 billing disputes are with #finance, and 16 tickets wait for a person with order history attached."
    },
    finance: {
      brief: "Reconcile last week's Stripe payouts against the ledger",
      agent: "Finance close",
      title: "Reconcile last week's payouts against the ledger",
      steps: [
        { label: "Pull last week's Stripe payouts", call: 'stripe.payouts.list({ week: "last" })', out: "318 payouts · $48,210.66" },
        { label: "Pull matching ledger entries", call: 'postgres.query("ledger", week: "last")', out: "318 entries" },
        { label: "Match payouts to entries", call: "match(payouts, entries, by: [amount, date])", out: "312 matched · 6 off by fees" },
        { label: "Post 6 adjusting entries, net −$212.40", call: "ledger.post(entries: 6)", out: "posted", gate: true },
        { label: "Email the reconciliation report to the controller", call: 'gmail.send("controller", "Weekly reconciliation")', out: "sent" }
      ],
      summary: "312 of 318 payouts matched. 6 Stripe fee differences were booked as adjusting entries (net −$212.40) and the report is in the controller's inbox."
    },
    inventory: {
      brief: "Draft restock orders for anything under two weeks of cover",
      agent: "Inventory",
      title: "Draft restock orders for anything under two weeks of cover",
      steps: [
        { label: "Read stock levels for every SKU", call: "shopify.inventory.list()", out: "412 SKUs" },
        { label: "Forecast days of cover from 30-day sales", call: "forecast.cover(window: 30)", out: "9 SKUs under 14 days" },
        { label: "Draft purchase orders by supplier", call: "draft.po(skus: 9)", out: "PO-2291 · PO-2292 · PO-2293" },
        { label: "Email the 3 POs to suppliers", call: "gmail.send(to: 3 suppliers, attach: POs)", out: "3 sent", gate: true },
        { label: "Open a receiving task for Friday", call: 'linear.create("Receive POs 2291–2293", due: "Fri")', out: "OPS-188" }
      ],
      summary: "9 SKUs were under two weeks of cover. 3 purchase orders went to suppliers, and receiving is scheduled for Friday as OPS-188."
    }
  };

  var AGENT_HINTS = [
    ["Support desk", /\b(ticket|support|inbox|customer|reply|complain|refund)/],
    ["Finance close", /\b(invoice|payout|ledger|reconcil|stripe|tax|expense|payment|unpaid|books?)\b/],
    ["Inventory", /\b(stock|inventory|restock|supplier|purchase order|po|warehouse|sku)\b/],
    ["Outbound", /\b(email|outreach|follow.?up|lead|wholesale|newsletter|campaign)\b/],
    ["Catalog QA", /\b(product page|listing|alt text|catalog|broken|price change|description)\b/],
    ["Research", /\b(competitor|research|market|review|compare|trend)\b/]
  ];
  var AGENT_TOOLS = {
    "Support desk": ["zendesk.search", "zendesk.update", "slack.post"],
    "Finance close": ["stripe.invoices.list", "ledger.post", "gmail.send"],
    "Inventory": ["shopify.inventory.list", "gmail.send", "linear.create"],
    "Outbound": ["hubspot.contacts.search", "gmail.send", "hubspot.log"],
    "Catalog QA": ["shopify.products.list", "shopify.products.update", "linear.create"],
    "Research": ["web.search", "sheets.append", "notion.create"]
  };

  function pickAgent(text) {
    if (agentSelect.value !== "auto") return agentSelect.value;
    var t = text.toLowerCase();
    for (var i = 0; i < AGENT_HINTS.length; i++) if (AGENT_HINTS[i][1].test(t)) return AGENT_HINTS[i][0];
    return "Support desk";
  }
  function hash(s) { var h = 7; for (var i = 0; i < s.length; i++) h = (h * 31 + s.charCodeAt(i)) >>> 0; return h; }
  function cap(s) { return s.charAt(0).toUpperCase() + s.slice(1); }

  function templatePlan(text, agent) {
    var tools = AGENT_TOOLS[agent];
    var n = 6 + (hash(text) % 30);
    var title = cap(text.replace(/[.\s]+$/, "")).slice(0, 90);
    var readOnly = agent === "Research";
    var steps = [
      { label: "Read the brief and pull the account context", call: "context.load(brief" + (attached ? ", attachment" : "") + ")", out: "ok" },
      { label: "Find every record this touches", call: tools[0] + "(match: brief)", out: n + " records" },
      { label: "Work through them and draft the changes", call: "draft(records: " + n + ")", out: n + " drafts ready" },
      readOnly
        ? { label: "Write up the findings", call: tools[1] + "(rows: " + n + ")", out: "saved" }
        : { label: "Apply the " + n + " changes", call: tools[1] + "(count: " + n + ")", out: n + " applied", gate: true },
      { label: "Report back in #ops", call: 'slack.post("#ops", summary)', out: "posted" }
    ];
    return {
      agent: agent,
      title: title,
      steps: steps,
      summary: "Done in preview: the " + agent + " agent found " + n + " records, drafted the work" + (readOnly ? " and wrote up what it found." : ", and applied it after the gate.") + " Connect a workspace and the same plan runs on your real data."
    };
  }

  /* ── Rendering ───────────────────────────────────────────── */
  var CHECK = '<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m5 12 4.5 4.5L19 7"/></svg>';

  function setState(state, label) {
    runState.dataset.state = state;
    runStateLabel.textContent = label;
    var dot = runState.querySelector(".dot");
    dot.className = "dot" + (state === "waiting" ? " dot--warn" : state === "stopped" ? " dot--stop" : state === "running" ? " dot--idle" : "");
  }

  function renderPlan(plan) {
    runAgent.textContent = plan.agent;
    runTitle.textContent = plan.title;
    planCount.textContent = plan.steps.length + " steps";
    planEl.replaceChildren();
    plan.steps.forEach(function (s, i) {
      var li = document.createElement("li");
      li.className = "step";
      li.dataset.state = "pending";
      var mark = document.createElement("span");
      mark.className = "step-mark";
      mark.textContent = String(i + 1);
      var txt = document.createElement("div");
      var lab = document.createElement("span");
      lab.className = "step-label";
      lab.textContent = s.label;
      if (s.gate) {
        var g = document.createElement("span");
        g.className = "gate-tag";
        g.textContent = "Gate";
        lab.append(g);
      }
      var tool = document.createElement("span");
      tool.className = "step-tool";
      tool.textContent = s.call.split("(")[0];
      txt.append(lab, tool);
      li.append(mark, txt);
      planEl.append(li);
    });
  }

  function markStep(i, state) {
    var li = planEl.children[i];
    if (!li) return;
    li.dataset.state = state;
    var mark = li.querySelector(".step-mark");
    if (state === "done") mark.innerHTML = CHECK;
    else if (state === "skipped") mark.textContent = "–";
    else if (state === "waiting") mark.textContent = "!";
    else mark.textContent = String(i + 1);
  }

  function clock(d) {
    d = d || new Date();
    return [d.getHours(), d.getMinutes(), d.getSeconds()].map(function (n) { return String(n).padStart(2, "0"); }).join(":");
  }
  function trace(parts, at) {
    var row = document.createElement("div");
    row.className = "trace-line";
    var t = document.createElement("time");
    t.textContent = at || clock();
    var s = document.createElement("span");
    parts.forEach(function (p) {
      if (typeof p === "string") { s.append(p); return; }
      var e = document.createElement("span");
      e.className = p[0];
      e.textContent = p[1];
      s.append(e);
    });
    row.append(t, s);
    traceEl.append(row);
    traceEl.scrollTop = traceEl.scrollHeight;
  }
  function fmtTime(ms) {
    var s = Math.max(0, Math.round(ms / 1000));
    return Math.floor(s / 60) + ":" + String(s % 60).padStart(2, "0");
  }

  /* The example run, shown complete so the console is never empty. */
  function showExample() {
    var p = PRESETS.support;
    renderPlan(p);
    traceEl.replaceChildren();
    var t0 = new Date(2026, 9, 5, 9, 12, 4);
    var off = [0, 4, 9, 21, 33, 36];
    p.steps.forEach(function (s, i) {
      var at = clock(new Date(t0.getTime() + off[i] * 1000));
      trace(["→ ", ["fn", s.call]], at);
      if (s.gate) trace([["wait", "■ gate: approved by support lead"]], at);
      trace(["← ", ["ok", s.out]], clock(new Date(t0.getTime() + (off[i] + 2) * 1000)));
      markStep(i, "done");
    });
    resultText.textContent = p.summary;
    statSteps.textContent = "5 / 5";
    statCalls.textContent = "5";
    statGates.textContent = "1";
    statTime.textContent = "0:38";
    runKind.textContent = "Example run";
    setState("done", "Done");
  }

  /* ── The fleet ───────────────────────────────────────────── */
  var paused = false;
  var resumeWaiters = [];

  function paintFleet() {
    body.classList.toggle("stopped", paused);
    body.classList.toggle("spinning", !paused);
    fleetSwitch.setAttribute("aria-pressed", String(paused));
    fleetSwitchLabel.textContent = paused ? "Resume fleet" : "Pause fleet";
    fleetPlate.innerHTML = "Fleet <b>" + (paused ? "Paused" : "On shift") + "</b>";
  }
  function setPaused(on) {
    on = !!on;
    if (paused === on) return;
    paused = on;
    paintFleet();
    if (current) {
      trace([[on ? "bad" : "ok", on ? "■ fleet paused by kill switch" : "▶ fleet resumed"]]);
      if (on) setState("stopped", "Paused");
      else setState(current.waitingGate ? "waiting" : "running", current.waitingGate ? "Needs you" : "Running");
    }
    if (!on) { var w = resumeWaiters; resumeWaiters = []; w.forEach(function (f) { f(); }); }
  }
  function whilePaused() {
    return paused ? new Promise(function (r) { resumeWaiters.push(r); }) : Promise.resolve();
  }

  /* ── Running ─────────────────────────────────────────────── */
  var current = null;   // { abort: AbortController, waitingGate }
  var mode = "ask";

  function sleep(ms, signal) {
    return new Promise(function (resolve, reject) {
      if (signal.aborted) return reject(new DOMException("stop", "AbortError"));
      var id = setTimeout(resolve, REDUCED ? Math.min(ms, 120) : ms);
      signal.addEventListener("abort", function () { clearTimeout(id); reject(new DOMException("stop", "AbortError")); }, { once: true });
    });
  }

  function askGate(i, signal) {
    return new Promise(function (resolve, reject) {
      var li = planEl.children[i];
      var box = document.createElement("div");
      box.className = "gate-actions";
      var ok = document.createElement("button");
      ok.type = "button"; ok.className = "approve"; ok.textContent = "Approve";
      var no = document.createElement("button");
      no.type = "button"; no.textContent = "Skip this step";
      box.append(ok, no);
      li.lastChild.append(box);
      ok.focus({ preventScroll: true });
      function done(v) { box.remove(); resolve(v); }
      ok.addEventListener("click", function () { done(true); });
      no.addEventListener("click", function () { done(false); });
      signal.addEventListener("abort", function () { box.remove(); reject(new DOMException("stop", "AbortError")); }, { once: true });
    });
  }

  function setBusy(on) {
    consoleEl.classList.toggle("is-running", on);
    runBtnLabel.textContent = on ? "Stop" : "Run";
  }

  async function execute(plan, kindLabel, ctl) {
    var signal = ctl.signal;
    renderPlan(plan);
    runKind.textContent = kindLabel;
    resultText.textContent = "Working…";
    var calls = 0, gates = 0, finished = 0, skipped = [];
    var t0 = Date.now(), pausedFor = 0, pauseStart = 0;
    statSteps.textContent = "0 / " + plan.steps.length;
    statCalls.textContent = "0"; statGates.textContent = "0"; statTime.textContent = "0:00";
    var timer = setInterval(function () {
      if (paused) { if (!pauseStart) pauseStart = Date.now(); return; }
      if (pauseStart) { pausedFor += Date.now() - pauseStart; pauseStart = 0; }
      statTime.textContent = fmtTime(Date.now() - t0 - pausedFor);
    }, 250);
    setState(paused ? "stopped" : "running", paused ? "Paused" : "Running");
    if (paused) trace([["bad", "■ fleet is paused. The run starts when you resume it."]]);

    var i = 0;
    try {
      for (i = 0; i < plan.steps.length; i++) {
        var s = plan.steps[i];
        await whilePaused();
        markStep(i, "running");
        trace(["→ ", ["fn", s.call]]);
        calls++; statCalls.textContent = String(calls);
        await sleep(650 + (hash(s.call) % 600), signal);
        await whilePaused();

        if (s.gate) {
          if (mode === "ask") {
            markStep(i, "waiting");
            current.waitingGate = true;
            setState("waiting", "Needs you");
            trace([["wait", "■ gate: waiting for your approval"]]);
            var yes = await askGate(i, signal);
            current.waitingGate = false;
            await whilePaused();
            setState("running", "Running");
            if (!yes) {
              trace([["bad", "■ skipped by you"]]);
              markStep(i, "skipped");
              skipped.push(s.label);
              continue;
            }
            trace([["ok", "■ approved by you"]]);
          } else {
            trace([["wait", "■ gate: auto-approved by policy"]]);
          }
          gates++; statGates.textContent = String(gates);
          markStep(i, "running");
          await sleep(500, signal);
        }

        trace(["← ", ["ok", s.out]]);
        markStep(i, "done");
        finished++;
        statSteps.textContent = finished + " / " + plan.steps.length;
      }
      setState("done", "Done");
      resultText.textContent = plan.summary + (skipped.length ? " Skipped at your call: " + skipped.join("; ") + "." : "");
      addTile(plan, fmtTime(Date.now() - t0 - pausedFor));
    } catch (e) {
      if (e && e.name !== "AbortError") throw e;
      markStep(i, "skipped");
      trace([["bad", "■ run stopped by you"]]);
      setState("stopped", "Stopped");
      resultText.textContent = "Stopped after " + finished + " of " + plan.steps.length + " steps. Steps already finished stay finished.";
    } finally {
      clearInterval(timer);
    }
  }

  /* Each finished run joins the top lane, once in each group. */
  function addTile(plan, dur) {
    var tools = plan.steps.map(function (s) { return s.call.split(".")[0].split("(")[0]; })
      .filter(function (t, i, a) { return /^[a-z]+$/.test(t) && a.indexOf(t) === i && ["classify", "draft", "match", "forecast", "context"].indexOf(t) === -1; })
      .slice(0, 3).join(" · ");
    laneA.querySelectorAll(".marquee__group").forEach(function (g) {
      var a = document.createElement("article");
      a.className = "tile tile--you";
      var top = document.createElement("div");
      top.className = "tile-top";
      var dot = document.createElement("span"); dot.className = "dot";
      var who = document.createElement("span"); who.textContent = "You · " + plan.agent;
      var t = document.createElement("time"); t.textContent = dur;
      top.append(dot, who, t);
      var p = document.createElement("p"); p.textContent = plan.title;
      var tl = document.createElement("span"); tl.className = "tile-tools"; tl.textContent = tools || "preview";
      a.append(top, p, tl);
      g.prepend(a);
    });
  }

  /* ── Planner ─────────────────────────────────────────────── */
  var sample = null;
  var GONE = ["not_granted", "sampling_disabled", "not_declared", "capability_disabled", "capability_removed"];

  function setPlanner(m) {
    planner.dataset.mode = m;
    planner.textContent = m === "live" ? "Plans written by Claude" : m === "offline" ? "Offline planner: scripted plans" : "Planner connecting";
  }

  function plannerPrompt(text, agent) {
    return [
      "You plan jobs for SKEWSHOP, a team of AI agents that run the back office of a small online shop.",
      "Write a plan for this brief. The page will simulate running it, so make it concrete and plausible.",
      "",
      "Brief: " + text,
      attached ? "Attached context file: " + attached.name : "",
      "Agent: " + (agent ? agent : "pick the best one of: Support desk, Finance close, Inventory, Outbound, Research, Catalog QA"),
      "Tools available: zendesk.search, zendesk.update, slack.post, stripe.payouts.list, stripe.invoices.list, postgres.query, ledger.post, quickbooks.sync, shopify.inventory.list, shopify.products.list, shopify.products.update, shopify.orders.list, gmail.search, gmail.send, hubspot.contacts.search, hubspot.log, linear.create, sheets.append, notion.create, web.search, classify, draft, match, forecast.",
      "",
      "Rules: 4 to 6 steps. Each step uses exactly one tool. Mark gate: true on every step that moves money, writes to the books, or contacts customers or suppliers, and on no other step. If nothing is risky, no gate. Use realistic small-shop numbers in outputs.",
      "Reply with only JSON in this shape:",
      '{"agent":"Finance close","title":"short imperative title, under 70 characters","steps":[{"label":"plain-language step, under 60 characters","call":"tool.name(short args)","out":"result, under 40 characters","gate":false}],"summary":"two plain sentences on the outcome, past tense, under 240 characters"}'
    ].filter(Boolean).join("\n");
  }

  function clean(raw, agentFallback) {
    if (!raw || !Array.isArray(raw.steps)) return null;
    var steps = raw.steps.slice(0, 7).map(function (s) {
      return {
        label: String((s && s.label) || "").slice(0, 90),
        call: String((s && s.call) || "tool()").slice(0, 90),
        out: String((s && s.out) || "ok").slice(0, 60),
        gate: !!(s && (s.gate === true || s.gate === "true"))
      };
    }).filter(function (s) { return s.label; });
    if (steps.length < 2) return null;
    return {
      agent: String(raw.agent || agentFallback || "Support desk").slice(0, 30),
      title: String(raw.title || "Untitled run").slice(0, 90),
      steps: steps,
      summary: String(raw.summary || "Run complete.").slice(0, 320)
    };
  }

  async function startRun(text, preset) {
    if (current) return;
    var ctl = new AbortController();
    current = { abort: ctl, waitingGate: false };
    setBusy(true);
    traceEl.replaceChildren();

    try {
      var plan, kind;
      if (preset) {
        plan = PRESETS[preset];
        kind = "Simulated run";
      } else {
        var agent = agentSelect.value === "auto" ? null : agentSelect.value;
        if (sample) {
          renderPlan({ agent: agent || "Choosing agent", title: cap(text).slice(0, 90), steps: [] });
          planCount.textContent = "planning";
          resultText.textContent = "Writing the plan…";
          setState("running", "Planning");
          runKind.textContent = "Live plan";
          trace([["fn", "planner"], " drafting steps for the brief"]);
          try {
            var raw = await sample.json(plannerPrompt(text, agent), { modelTier: "quick", signal: ctl.signal });
            plan = clean(raw, agent);
            if (!plan) trace([["bad", "planner returned an unusable plan, using the template"]]);
          } catch (e) {
            var code = e && e.code;
            if (code === "cancelled") throw new DOMException("stop", "AbortError");
            if (GONE.indexOf(code) !== -1) { sample = null; setPlanner("offline"); }
            trace([["bad", "planner unavailable (" + (code || "error") + "), using the template"]]);
          }
          kind = plan ? "Claude plan · simulated run" : "Simulated run";
        }
        if (!plan) { plan = templatePlan(text, agent || pickAgent(text)); kind = "Simulated run"; }
      }
      await execute(plan, kind, ctl);
    } catch (e) {
      if (!e || e.name !== "AbortError") throw e;
      trace([["bad", "■ stopped before the plan was ready"]]);
      setState("stopped", "Stopped");
      resultText.textContent = "Stopped while planning. Nothing ran.";
    } finally {
      current = null;
      setBusy(false);
    }
  }

  /* ── Controls ────────────────────────────────────────────── */
  var attached = null;

  function fleetCommand(t) {
    t = t.toLowerCase();
    if (t.length > 60) return null;
    if (/\b(pause|stop|halt|freeze|kill)\b.*\b(fleet|agents|everything|all|lanes|reels)\b/.test(t)) return "pause";
    if (/\b(resume|restart|start|unpause|wake)\b.*\b(fleet|agents|everything|all|lanes|reels)\b/.test(t)) return "resume";
    return null;
  }

  form.addEventListener("submit", function (e) {
    e.preventDefault();
    if (current) { current.abort.abort(); return; }
    var text = brief.value.trim();
    if (!text) { brief.focus(); return; }
    var cmd = fleetCommand(text);
    if (cmd) {
      brief.value = "";
      setPaused(cmd === "pause");
      traceEl.replaceChildren();
      trace([[cmd === "pause" ? "bad" : "ok", cmd === "pause" ? "■ kill switch thrown: every agent paused" : "▶ fleet back on shift"]]);
      return;
    }
    brief.value = "";
    grow();
    startRun(text, null);
  });
  function grow() { brief.style.height = "auto"; brief.style.height = Math.min(brief.scrollHeight + 2, 192) + "px"; }
  brief.addEventListener("input", grow);
  window.addEventListener("resize", grow);
  brief.addEventListener("keydown", function (e) {
    if (e.key === "Enter" && !e.shiftKey && !e.isComposing) { e.preventDefault(); form.requestSubmit(); }
  });
  $("presets").addEventListener("click", function (e) {
    var b = e.target.closest("[data-preset]");
    if (!b || current) return;
    startRun(null, b.dataset.preset);
  });
  function setMode(m) {
    mode = m;
    modeAsk.setAttribute("aria-pressed", String(m === "ask"));
    modeAuto.setAttribute("aria-pressed", String(m === "auto"));
  }
  modeAsk.addEventListener("click", function () { setMode("ask"); });
  modeAuto.addEventListener("click", function () { setMode("auto"); });
  fleetSwitch.addEventListener("click", function () { setPaused(!paused); });

  ctxFile.addEventListener("change", function () {
    var f = ctxFile.files && ctxFile.files[0];
    ctxFile.value = "";
    if (!f) return;
    attached = { name: f.name };
    var old = ctx.querySelector(".ctx-chip");
    if (old) old.remove();
    var chip = document.createElement("span");
    chip.className = "ctx-chip";
    var n = document.createElement("span");
    n.textContent = f.name;
    var x = document.createElement("button");
    x.type = "button";
    x.setAttribute("aria-label", "Remove " + f.name);
    x.innerHTML = '<svg aria-hidden="true" width="10" height="10" viewBox="0 0 14 14" fill="none"><path stroke="currentColor" stroke-linecap="round" stroke-width="2" d="m1 1 12 12M13 1 1 13"/></svg>';
    x.addEventListener("click", function () { chip.remove(); attached = null; });
    chip.append(n, x);
    ctx.append(chip);
  });

  /* ── Boot ────────────────────────────────────────────────── */
  paused = REDUCED;
  paintFleet();
  showExample();
  grow();
  setPlanner("pending");
  if (window.claude && typeof window.claude.use === "function") {
    window.claude.use("sample").then(function (s) {
      if (s && typeof s.json === "function") { sample = s; setPlanner("live"); }
      else setPlanner("offline");
    }, function () { setPlanner("offline"); });
  } else {
    setPlanner("offline");
  }
})();


/* ── Scroll reveals ──────────────────────────────────────── */
(function () {
  "use strict";
  if (window.matchMedia("(prefers-reduced-motion: reduce)").matches) return;
  if (!("IntersectionObserver" in window)) return;

  /* [selector, kind]. Siblings that match the same selector inside one
     parent stagger by 75 ms each. */
  var GROUPS = [
    [".stack-band", "fade"],
    [".section-head > h2", "wipe"],
    [".section-head > p", "rise"],
    [".move", "rise"],
    [".agent", "rise"],
    [".guards li", "rise"],
    ["#guardrails .split > div:last-child", "rise"],
    [".closing-band", "fade"],
    [".cta", "rise"],
    [".cta-copy > *", "rise"],
    [".week li", "rise"],
    [".shift-foot", "rise"]
  ];

  var seen = new Set();
  GROUPS.forEach(function (g) {
    var byParent = new Map();
    document.querySelectorAll(g[0]).forEach(function (el) {
      if (el.closest(".hero") || seen.has(el)) return;
      seen.add(el);
      el.dataset.reveal = g[1];
      var n = byParent.get(el.parentNode) || 0;
      byParent.set(el.parentNode, n + 1);
      /* Section heads read top to bottom, so give them a running index. */
      if (el.parentNode.classList.contains("section-head")) n = Array.prototype.indexOf.call(el.parentNode.children, el);
      el.style.setProperty("--i", String(Math.min(n, 8)));
    });
  });

  var io = new IntersectionObserver(function (entries) {
    entries.forEach(function (e) {
      if (!e.isIntersecting) return;
      e.target.classList.add("is-in");
      io.unobserve(e.target);
    });
  }, { rootMargin: "0px 0px -8% 0px", threshold: 0.12 });

  seen.forEach(function (el) {
    /* Anything already on screen shows at once rather than blinking. */
    var r = el.getBoundingClientRect();
    if (r.top < window.innerHeight * 0.92 && r.bottom > 0) el.classList.add("is-in");
    else io.observe(el);
  });
  document.documentElement.classList.add("reveal-ready");
})();
</script>
</body>
</html>
```

