INSTALANDING.AI · Radiating Rings Hero Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Radiating Rings Hero Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/radiating-rings-hero-page

proxima-edge.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Radiating Rings Hero Page
  slug     radiating-rings-hero-page
  prompt   https://instalanding.ai/p/radiating-rings-hero-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/radiating-rings-hero-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of <style>: --void, --deep, --mid, --lit, --blue (#045cff),
            --ink, --glass, --line, --sans (Poppins), --mono (JetBrains Mono), --ease; per-ring gradient
            stops are --c1..--c3 / --h1..--h3 on each .rings i:nth-child(n)
  sections  nav, hero, features, latency, how-it-works, stats, pricing, faq, cta, footer
  scripts   one inline script, no libraries: seeded starfield + region dot map; pointer-tracked light
            (#lightsrc + #beamcore transforms, lerped, parks when caught up); footer subscribe (local only);
            count-up stats; pill-nav glide measured from the active link; .rv scroll reveals
  assets    none: orb, rings, stars and icons are CSS and inline SVG; fonts from Google Fonts

  ADAPTING
  - The five .rings i stadiums are all centred on .cta-slot; resizing the button or moving it out of
    .ringstack breaks the tunnel. The hover light is a ::after opacity fade keyed on .ringstack:hover and
    :focus-within, with the stagger delay in the :hover rule, not the base rule.
  - The light moves by transform on #lightsrc and #beamcore; do not switch it to animating
    background-position (repaints the whole hero every frame).
  - The pill-nav glide is measured from the active link and re-measured on document.fonts.ready and
    resize; links must keep href="#id" matching a section id for the IntersectionObserver handoff.
  - Count-up targets live in data-to / data-dp on #stats; the visible text is overwritten from them.
-->
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Proxima — run the model next to the request</title>
<meta name="description" content="A fictional inference edge network, staged as concentric stadium rings radiating from the call to action. One file, no images, no libraries." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
<style>
:root {
  --void: #040d2a;
  --deep: #081d5c;
  --mid: #275bbb;
  --lit: #a4d8ff;
  --glass: rgba(4, 17, 60, 0.62);
  --blue: #045cff;
  --ink: #fdfdff;
  --ink-2: #a9bbe4;
  --ink-3: #6a7ea6;
  --line: rgba(123, 161, 244, 0.18);
  --edge-hi: rgba(170, 210, 255, 0.42);
  --edge-lo: rgba(123, 161, 244, 0.05);

  --sans: "Poppins", system-ui, sans-serif;
  --mono: "JetBrains Mono", ui-monospace, monospace;
  --ease: cubic-bezier(0.2, 0.8, 0.2, 1);
}

* { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; }
body {
  font-family: var(--sans);
  color: var(--ink);
  background: var(--void);
  overflow-x: clip;
  -webkit-font-smoothing: antialiased;
}
/* film grain over everything — the cheapest way to make flat gradients feel printed */
body::after {
  content: ""; position: fixed; inset: 0; z-index: 100; pointer-events: none;
  opacity: 0.07; mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
a { color: inherit; text-decoration: none; }
ul { list-style: none; }
.wrap { width: min(1180px, 100% - 40px); margin: 0 auto; }
.lbl {
  display: inline-flex; align-items: center; gap: 10px;
  font-family: var(--mono); font-size: 11px; letter-spacing: 0.18em; text-transform: uppercase; color: var(--lit);
}
.lbl::before {
  content: ""; width: 14px; height: 9px; border-radius: 999px;
  background: linear-gradient(180deg, var(--lit), #3f7ddc);
  box-shadow: 0 0 0 3px rgba(39, 91, 187, 0.35);
}
.grad-text {
  background: linear-gradient(180deg, #ffffff 20%, #9cc6ff 100%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}

/* gradient hairline border, used on every surface below the hero */
.surface {
  border: 1px solid transparent;
  background:
    linear-gradient(180deg, rgba(16, 40, 108, 0.55), rgba(5, 14, 46, 0.7)) padding-box,
    linear-gradient(180deg, var(--edge-hi), var(--edge-lo) 70%) border-box;
}

/* ============================================================ NAV */
.nav { position: absolute; inset: 0 0 auto; z-index: 40; }
.nav .wrap { display: flex; align-items: center; justify-content: space-between; height: 92px; gap: 24px; }
.brand { display: flex; align-items: center; gap: 11px; font-weight: 600; font-size: 19px; letter-spacing: -0.01em; }
.brand svg { width: 24px; height: 24px; }
.pillnav {
  position: relative; display: flex; gap: 4px; padding: 5px;
  border-radius: 999px; background: rgba(123, 161, 244, 0.13);
  box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.1);
  -webkit-backdrop-filter: blur(8px); backdrop-filter: blur(8px);
}
.pillnav a {
  position: relative; z-index: 1; padding: 8px 18px; border-radius: 999px;
  font-size: 14px; color: var(--ink-2); transition: color 0.3s var(--ease);
}
.pillnav a.on { color: #fff; font-weight: 500; }
.pillnav .glide {
  position: absolute; top: 5px; left: 0; height: calc(100% - 10px);
  border-radius: 999px; background: rgba(233, 243, 255, 0.2);
  box-shadow: inset 0 0 0 1px rgba(233, 243, 255, 0.22);
  transition: transform 0.42s var(--ease), width 0.42s var(--ease);
  pointer-events: none;
}
.nav-r { display: flex; align-items: center; gap: 18px; }
.nav-r .ghost { font-size: 14px; color: var(--ink-2); transition: color 0.2s; }
.nav-r .ghost:hover { color: #fff; }
.btn {
  display: inline-flex; align-items: center; gap: 9px;
  padding: 11px 24px; border-radius: 999px; font-size: 14px; font-weight: 500;
  transition: 0.24s var(--ease);
}
.btn--blue {
  background: var(--blue); color: #fff;
  box-shadow: 0 10px 26px -8px rgba(4, 92, 255, 0.85), inset 0 -8px 14px -6px rgba(255, 255, 255, 0.6);
}
.btn--blue:hover { transform: translateY(-2px); box-shadow: 0 16px 32px -8px rgba(4, 92, 255, 0.9), inset 0 -8px 14px -6px rgba(255, 255, 255, 0.7); }
.btn--line { color: var(--ink); box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.32); background: rgba(123, 161, 244, 0.06); }
.btn--line:hover { box-shadow: inset 0 0 0 1px rgba(200, 228, 255, 0.6); background: rgba(123, 161, 244, 0.14); }
.btn:focus-visible, .cta:focus-visible { outline: 2px solid var(--lit); outline-offset: 3px; }

/* ============================================================ HERO */
.hero {
  position: relative; isolation: isolate; overflow: hidden;
  padding: 0 0 clamp(3.5rem, 7vw, 6rem);
  background:
    radial-gradient(90% 60% at 78% 8%, rgba(30, 80, 190, 0.28), transparent 60%),
    linear-gradient(158deg, #0d2a6b 0%, #071845 34%, #04102e 62%, #040d2a 100%);
}
.lightsrc {
  position: absolute; z-index: 0; left: 0; top: 0; pointer-events: none;
  width: min(1500px, 105vw); aspect-ratio: 1;
  margin: -50vh 0 0 -50vw;
  background: radial-gradient(circle,
    rgba(96, 158, 255, 0.85) 0%, rgba(44, 100, 212, 0.46) 26%,
    rgba(12, 34, 88, 0.18) 52%, transparent 72%);
  will-change: transform;
}
.hero::before {
  content: ""; position: absolute; z-index: 0; pointer-events: none;
  left: -14%; top: -46%; width: 52%; height: 130%;
  background: linear-gradient(180deg, rgba(198, 224, 255, 0.34), rgba(198, 224, 255, 0));
  transform: rotate(22deg); border-radius: 999px; filter: blur(96px);
}
.stars { position: absolute; inset: 0; z-index: 1; pointer-events: none; }
.stars i { position: absolute; border-radius: 50%; background: #bcd3ff; opacity: var(--o, 0.4); }

.hero-in { position: relative; z-index: 3; text-align: center; padding-top: clamp(8rem, 14vw, 10.5rem); }
.eyebrow {
  display: inline-flex; align-items: center; gap: 12px;
  padding: 5px 16px 5px 5px; margin-bottom: 1.8rem; border-radius: 999px;
  font-size: 13px; color: var(--ink-2);
  background: rgba(10, 28, 84, 0.55);
  box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.22), 0 10px 30px -14px rgba(4, 92, 255, 0.7);
  -webkit-backdrop-filter: blur(8px); backdrop-filter: blur(8px);
  transition: box-shadow 0.25s var(--ease);
}
.eyebrow:hover { box-shadow: inset 0 0 0 1px rgba(200, 228, 255, 0.5), 0 10px 30px -10px rgba(4, 92, 255, 0.9); }
.eyebrow b {
  padding: 4px 11px; border-radius: 999px; background: var(--blue); color: #fff;
  font-family: var(--mono); font-weight: 500; font-size: 10.5px; letter-spacing: 0.1em; text-transform: uppercase;
  box-shadow: inset 0 -5px 10px -5px rgba(255, 255, 255, 0.55);
}
.eyebrow svg { width: 14px; height: 14px; opacity: 0.7; }
.hero-in h1 {
  font-size: clamp(2.4rem, 1rem + 5.4vw, 4.7rem);
  font-weight: 600; line-height: 1.1; letter-spacing: -0.035em;
  text-wrap: balance; text-shadow: 0 6px 40px rgba(4, 13, 42, 0.5);
}
.hero-sub {
  max-width: 58ch; margin: 1.5rem auto 0;
  font-size: clamp(1rem, 0.94rem + 0.32vw, 1.16rem); font-weight: 300; line-height: 1.7; color: #c3d2f2;
  text-wrap: pretty;
}

/* ---------- feature row ---------- */
.feats { display: flex; justify-content: center; width: fit-content; margin: 2.1rem auto 0; }
.feats li { display: flex; align-items: center; gap: 11px; padding: 2px clamp(16px, 2.4vw, 30px); white-space: nowrap; }
.feats li + li { border-left: 1px solid rgba(164, 216, 255, 0.18); }
.feats svg { flex: none; width: 24px; height: 24px; color: var(--lit); }
.feats b { font-size: 12px; font-weight: 600; letter-spacing: 0.16em; text-transform: uppercase; color: #e8f0ff; }

/* ---------- rings ---------- */
.ringstack {
  position: relative; z-index: 2;
  margin: clamp(2.5rem, 5vw, 4rem) auto 0;
  width: min(1200px, 100% - 28px);
  aspect-ratio: 1200 / 500;
}
.rings { position: absolute; inset: 0; }
.rings i {
  position: absolute; top: 50%; left: 50%; translate: -50% -50%;
  border-radius: 999px;
  background: linear-gradient(176deg, var(--c1) 0%, var(--c2) 46%, var(--c3) 100%);
  box-shadow: inset 0 1px 0 rgba(214, 233, 255, 0.5), 0 0 34px -12px rgba(120, 178, 255, 0.5);
}
.rings i:nth-child(1) { width: 100%; height: 100%; --c1: #3164b8; --c2: #14337c; --c3: #0a1c4d; --h1: #5c92e0; --h2: #2755b4; --h3: #112c6e; }
.rings i:nth-child(2) { width: 86%; height: 86%; --c1: #4076cf; --c2: #1a409a; --c3: #0c2260; --h1: #6fa4ec; --h2: #3063c9; --h3: #143487; }
.rings i:nth-child(3) { width: 72%; height: 72%; --c1: #5b93e6; --c2: #24509f; --c3: #0e2a6e; --h1: #87b8f6; --h2: #3e76d8; --h3: #173e97; }
.rings i:nth-child(4) { width: 58%; height: 58%; --c1: #7fb1f2; --c2: #2f63c4; --c3: #11337f; --h1: #a3cbfb; --h2: #518ce6; --h3: #1b4aab; }
.rings i:nth-child(5) { width: 50%; height: 40%; --c1: #a9d2ff; --c2: #4a85e0; --c3: #14388c; --h1: #c6e2ff; --h2: #6aa3ef; --h3: #2256bd; }
.rings i::after {
  content: ""; position: absolute; inset: 0; border-radius: inherit;
  background: linear-gradient(176deg, var(--h1) 0%, var(--h2) 46%, var(--h3) 100%);
  box-shadow: inset 0 1px 0 rgba(236, 246, 255, 0.7), 0 0 60px -16px rgba(150, 200, 255, 0.6);
  opacity: 0; transition: opacity 0.42s var(--ease);
}
.ringstack:hover .rings i::after, .ringstack:focus-within .rings i::after { opacity: 1; }
.ringstack:hover .rings i:nth-child(4)::after { transition-delay: 0.05s; }
.ringstack:hover .rings i:nth-child(3)::after { transition-delay: 0.1s; }
.ringstack:hover .rings i:nth-child(2)::after { transition-delay: 0.15s; }
.ringstack:hover .rings i:nth-child(1)::after { transition-delay: 0.2s; }


.beam {
  position: absolute; z-index: 3; inset: 0; pointer-events: none;
  background: radial-gradient(64% 20% at 50% 44%, rgba(186, 217, 255, 0.34) 0%, transparent 78%);
  mix-blend-mode: screen;
}
.beam::after {
  content: ""; position: absolute; inset: 0;
  background: radial-gradient(52% 18% at 50% 44%, rgba(255, 255, 255, 0.3) 0%, rgba(200, 228, 255, 0.16) 44%, transparent 78%);
  opacity: 0; transition: opacity 0.42s var(--ease);
}
.ringstack:hover .beam::after, .ringstack:focus-within .beam::after { opacity: 1; transition-delay: 0.12s; }
.beam i {
  position: absolute; inset: 0; display: block;
  background:
    radial-gradient(34% 15% at 50% 44%, rgba(233, 243, 255, 0.82) 0%, rgba(190, 220, 255, 0.4) 46%, transparent 76%),
    radial-gradient(17% 7% at 50% 43%, rgba(255, 255, 255, 0.62), transparent 74%);
  will-change: transform;
}

/* floating readouts in the gaps between rings */
.readout {
  position: absolute; z-index: 6; text-align: left;
  padding: 11px 15px 12px; border-radius: 14px; min-width: 150px;
  background: var(--glass);
  box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.24), 0 18px 40px -18px rgba(0, 0, 0, 0.8);
  -webkit-backdrop-filter: blur(10px); backdrop-filter: blur(10px);
  animation: bob 7s ease-in-out infinite;
}
.readout:nth-of-type(2) { animation-delay: -2s; }
.readout:nth-of-type(3) { animation-delay: -4s; }
.readout:nth-of-type(4) { animation-delay: -5.5s; }
.readout small { display: flex; align-items: center; gap: 7px; font-family: var(--mono); font-size: 10px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--ink-3); }
.readout small::before { content: ""; width: 6px; height: 6px; border-radius: 50%; background: #5bf0b0; box-shadow: 0 0 8px #5bf0b0; animation: pulse 2.4s ease-in-out infinite; }
.readout b { display: block; margin-top: 4px; font-size: 1.15rem; font-weight: 600; letter-spacing: -0.02em; }
.readout b em { font-style: normal; font-weight: 400; font-size: 0.8rem; color: var(--ink-2); margin-left: 3px; }
.ro-1 { left: 3%; top: 2%; }
.ro-2 { right: 2%; top: 12%; }
.ro-3 { left: 7%; bottom: 0; }
.ro-4 { right: 6%; bottom: 4%; }
@keyframes bob { 50% { transform: translateY(-7px); } }
@keyframes pulse { 50% { opacity: 0.35; } }

.cta-slot { position: absolute; z-index: 5; top: 50%; left: 50%; translate: -50% -50%; }

/* ---------- the button as the innermost ring ----------
   Same stadium, same 176deg gradient, the next step lighter than ring 5,
   with the gap to ring 5 matching the gap between the rings around it. */
.ringstack .cta-slot { width: 42%; height: 26%; }
.cta.cta--ring {
  position: relative; isolation: isolate;
  width: 100%; height: 100%; padding: 0 4%;
  justify-content: center; gap: 0.7em;
  border-radius: 999px;
  font-size: clamp(0.9rem, 0.7rem + 0.75vw, 1.4rem); font-weight: 500; letter-spacing: -0.01em;
  color: #061848;
  background: linear-gradient(176deg, #e4f2ff 0%, #9cc8fa 46%, #4d86e2 100%);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.95),
    inset 0 -10px 22px -12px rgba(10, 40, 130, 0.45),
    0 0 40px -10px rgba(170, 215, 255, 0.75);
}
/* the lit state, faded in like the rings around it */
.cta.cta--ring::after {
  content: ""; position: absolute; inset: 0; z-index: -1; border-radius: inherit;
  background: linear-gradient(176deg, #ffffff 0%, #c4e0ff 46%, #6aa3ef 100%);
  box-shadow: inset 0 1px 0 #fff, 0 0 60px -10px rgba(200, 230, 255, 0.9);
  opacity: 0; transition: opacity 0.42s var(--ease);
}
.ringstack:hover .cta.cta--ring::after, .cta.cta--ring:hover::after, .cta.cta--ring:focus-visible::after { opacity: 1; }
.cta.cta--ring svg { flex: none; width: 1.3em; height: 1em; transition: transform 0.3s var(--ease); }
.cta.cta--ring:hover svg { transform: translateX(4px); }
.cta.cta--ring:hover { box-shadow: inset 0 1px 0 #fff, inset 0 -10px 22px -12px rgba(10, 40, 130, 0.4), 0 0 60px -8px rgba(190, 225, 255, 0.95); }
.cta.cta--ring:focus-visible { outline: 2px solid #fff; outline-offset: 4px; }
.cta {
  display: inline-flex; align-items: center; gap: 16px;
  padding: clamp(15px, 2vw, 24px) clamp(30px, 5.2vw, 72px);
  border-radius: 999px;
  font-size: clamp(1rem, 0.88rem + 0.62vw, 1.34rem); font-weight: 400;
  color: #eaf1ff; white-space: nowrap;
  background: linear-gradient(180deg, #0a1440 0%, #050c26 100%);
  box-shadow: inset 0 1px 0 rgba(150, 190, 255, 0.28), 0 0 0 1px rgba(120, 165, 240, 0.28), 0 18px 50px -18px rgba(0, 0, 0, 0.9);
  transition: 0.26s var(--ease);
}
.cta:hover { box-shadow: inset 0 1px 0 rgba(190, 220, 255, 0.45), 0 0 0 1px rgba(170, 205, 255, 0.6), 0 0 54px -10px rgba(120, 180, 255, 0.8); }
.cta svg { width: 26px; height: 20px; }

/* ---------- logo strip ---------- */
.logos { position: relative; z-index: 3; margin-top: clamp(3rem, 6vw, 4.5rem); text-align: center; }
.logos p { font-family: var(--mono); font-size: 11px; letter-spacing: 0.16em; text-transform: uppercase; color: var(--ink-3); }
.logos ul {
  display: flex; flex-wrap: wrap; justify-content: center; align-items: center; gap: 18px clamp(28px, 5vw, 64px);
  margin-top: 1.4rem; color: #7f93bf;
}
.logos li { display: flex; align-items: center; gap: 9px; font-size: 1.05rem; font-weight: 500; letter-spacing: -0.01em; opacity: 0.85; transition: 0.25s; }
.logos li:hover { color: #dbe8ff; opacity: 1; }
.logos li svg { width: 20px; height: 20px; }
.logos li.serif { font-family: Georgia, serif; font-style: italic; font-weight: 400; }
.logos li.caps { font-family: var(--mono); font-size: 0.9rem; letter-spacing: 0.22em; text-transform: uppercase; }

/* ============================================================ SECTIONS */
.sec { position: relative; padding: clamp(5rem, 9vw, 8rem) 0; }
.sec + .sec::before {
  content: ""; position: absolute; top: 0; left: 50%; translate: -50% 0; width: min(1180px, 100% - 40px); height: 1px;
  background: linear-gradient(90deg, transparent, rgba(123, 161, 244, 0.3), transparent);
}
.sec-head { max-width: 62ch; margin-bottom: clamp(2.5rem, 4.5vw, 3.5rem); }
.sec-head.center { margin-inline: auto; text-align: center; }
.sec-head h2 { margin: 0 0 0.9rem; font-size: clamp(1.8rem, 1.1rem + 2.4vw, 2.9rem); font-weight: 600; line-height: 1.12; letter-spacing: -0.03em; text-wrap: balance; }
.sec-head p { color: var(--ink-2); line-height: 1.7; max-width: 54ch; font-weight: 300; font-size: 1.04rem; }
.sec-head.center p { margin-inline: auto; }

/* ---------- bento ---------- */
.bento { display: grid; grid-template-columns: repeat(6, 1fr); gap: 18px; }
.tile {
  position: relative; overflow: hidden; border-radius: 22px; padding: 28px 26px 30px;
  transition: transform 0.35s var(--ease), box-shadow 0.35s var(--ease);
}
.tile:hover { transform: translateY(-4px); box-shadow: 0 30px 60px -34px rgba(90, 160, 255, 0.9); }
.tile::after {
  content: ""; position: absolute; inset: 0; pointer-events: none; border-radius: inherit;
  background: radial-gradient(60% 50% at 20% 0%, rgba(120, 180, 255, 0.14), transparent 70%);
}
.span-4 { grid-column: span 4; }
.span-2 { grid-column: span 2; }
.tile h3 { font-size: 1.2rem; font-weight: 600; margin-bottom: 0.5rem; letter-spacing: -0.015em; }
.tile p { font-size: 0.95rem; line-height: 1.65; color: var(--ink-2); max-width: 46ch; }
.tile .vis { margin-bottom: 24px; height: 150px; position: relative; }

.dotmap { display: grid; grid-template-columns: repeat(32, 1fr); gap: 7px; align-content: center; height: 100%; }
.dotmap i { aspect-ratio: 1; border-radius: 50%; background: rgba(123, 161, 244, 0.16); }
.dotmap i.on { background: var(--lit); box-shadow: 0 0 8px rgba(164, 216, 255, 0.9); animation: pulse 3s ease-in-out infinite; animation-delay: var(--d, 0s); }

.warm { display: grid; gap: 14px; align-content: center; height: 100%; }
.warm div { font-family: var(--mono); font-size: 11px; letter-spacing: 0.08em; color: var(--ink-3); text-transform: uppercase; }
.warm .track { margin-top: 7px; height: 8px; border-radius: 999px; background: rgba(123, 161, 244, 0.14); overflow: hidden; }
.warm .track span { display: block; height: 100%; border-radius: inherit; background: linear-gradient(90deg, #275bbb, var(--lit)); width: var(--w); }

.minirings { position: relative; height: 100%; }
.minirings i { position: absolute; top: 50%; left: 50%; translate: -50% -50%; border-radius: 999px; border: 1px solid rgba(164, 216, 255, 0.3); }
.minirings i:nth-child(1) { width: 100%; height: 100%; }
.minirings i:nth-child(2) { width: 72%; height: 70%; border-color: rgba(164, 216, 255, 0.45); }
.minirings i:nth-child(3) { width: 42%; height: 40%; background: rgba(39, 91, 187, 0.3); border-color: rgba(164, 216, 255, 0.6); }
.minirings b { position: absolute; width: 10px; height: 10px; border-radius: 50%; translate: -50% -50%; }
.minirings .down { left: 50%; top: 30%; background: #ff6b8a; box-shadow: 0 0 10px #ff6b8a; }
.minirings .up { left: 82%; top: 50%; background: #5bf0b0; box-shadow: 0 0 10px #5bf0b0; }
.minirings svg { position: absolute; inset: 0; width: 100%; height: 100%; }

.chips { display: flex; flex-wrap: wrap; gap: 10px; align-content: center; height: 100%; }
.chips span {
  padding: 9px 16px; border-radius: 999px; font-family: var(--mono); font-size: 12.5px; color: #d6e4ff;
  background: rgba(39, 91, 187, 0.18); box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.24);
}
.chips span.hot { background: rgba(4, 92, 255, 0.4); box-shadow: inset 0 0 0 1px rgba(200, 228, 255, 0.5), 0 0 22px -6px rgba(4, 92, 255, 0.9); }

/* ---------- latency ---------- */
.lat { border-radius: 24px; padding: clamp(22px, 3.5vw, 40px); }
.lat-key { display: flex; gap: 22px; margin-bottom: 26px; font-family: var(--mono); font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase; color: var(--ink-3); }
.lat-key span { display: inline-flex; align-items: center; gap: 8px; }
.lat-key span::before { content: ""; width: 18px; height: 6px; border-radius: 999px; background: var(--k); }
.lat-row { display: grid; grid-template-columns: 150px 1fr; gap: 20px; align-items: center; padding: 14px 0; border-top: 1px solid var(--line); }
.lat-row:first-of-type { border-top: 0; }
.lat-row h4 { font-size: 1rem; font-weight: 500; }
.lat-row h4 small { display: block; font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.1em; color: var(--ink-3); font-weight: 400; margin-top: 2px; }
.bars { display: grid; gap: 7px; }
.bar { display: grid; grid-template-columns: 1fr 64px; gap: 12px; align-items: center; }
.bar i { display: block; height: 8px; border-radius: 999px; width: var(--w); transform-origin: left; transform: scaleX(0); transition: transform 1.1s var(--ease); }
.bar.o i { background: linear-gradient(90deg, #2c3e6e, #56679a); }
.bar.p i { background: linear-gradient(90deg, #275bbb, var(--lit)); box-shadow: 0 0 12px rgba(164, 216, 255, 0.6); }
.bar span { font-family: var(--mono); font-size: 12px; color: var(--ink-2); text-align: right; }
.bar.p span { color: #fff; }
.lat.in .bar i { transform: scaleX(1); }
.lat-row:nth-of-type(2) .bar i { transition-delay: 0.08s; }
.lat-row:nth-of-type(3) .bar i { transition-delay: 0.16s; }
.lat-row:nth-of-type(4) .bar i { transition-delay: 0.24s; }
.lat-row:nth-of-type(5) .bar i { transition-delay: 0.32s; }
.lat-row:nth-of-type(6) .bar i { transition-delay: 0.4s; }

/* ---------- how ---------- */
.how { display: grid; grid-template-columns: 1fr 1.1fr; gap: clamp(28px, 5vw, 64px); align-items: start; }
.steps { display: grid; gap: 4px; counter-reset: s; }
.step { counter-increment: s; display: grid; grid-template-columns: 52px 1fr; gap: 4px; padding: 22px 0; border-top: 1px solid var(--line); }
.step:first-child { border-top: 0; padding-top: 0; }
.step::before {
  content: counter(s, decimal-leading-zero); font-family: var(--mono); font-size: 12px; letter-spacing: 0.12em; color: var(--lit);
  padding-top: 4px;
}
.step h3 { font-size: 1.12rem; font-weight: 600; margin-bottom: 0.4rem; }
.step p { font-size: 0.94rem; line-height: 1.65; color: var(--ink-2); }

.term { border-radius: 20px; overflow: hidden; box-shadow: 0 40px 80px -40px rgba(4, 92, 255, 0.6); position: sticky; top: 24px; }
.term-bar { display: flex; align-items: center; gap: 8px; padding: 14px 18px; border-bottom: 1px solid var(--line); }
.term-bar i { width: 10px; height: 10px; border-radius: 50%; background: rgba(164, 216, 255, 0.22); }
.term-bar span { margin-left: 10px; font-family: var(--mono); font-size: 11.5px; color: var(--ink-3); }
.term pre { padding: 22px 22px 26px; font-family: var(--mono); font-size: 13px; line-height: 1.85; color: #d4e2ff; overflow-x: auto; }
.term .c { color: #5f76a8; }
.term .k { color: var(--lit); }
.term .s { color: #ffd59a; }
.term .ok { color: #5bf0b0; }
.term .dim { color: var(--ink-3); }
.term hr { border: 0; border-top: 1px dashed var(--line); margin: 0 22px; }

/* ---------- numbers ---------- */
/* ---------- numbers: one instrument panel ---------- */
.stats {
  position: relative; overflow: hidden; isolation: isolate;
  display: grid; grid-template-columns: repeat(4, minmax(0, 1fr));
  border-radius: 28px; border: 1px solid transparent;
  background:
    radial-gradient(60% 80% at 50% 0%, rgba(46, 102, 214, 0.32), transparent 70%) padding-box,
    linear-gradient(180deg, rgba(14, 36, 102, 0.72), rgba(4, 12, 40, 0.9)) padding-box,
    linear-gradient(180deg, rgba(200, 228, 255, 0.5), rgba(123, 161, 244, 0.1) 50%, rgba(4, 92, 255, 0.35)) border-box;
  box-shadow: 0 50px 100px -50px rgba(4, 92, 255, 0.7), inset 0 1px 0 rgba(220, 238, 255, 0.18);
}
.stat {
  position: relative; display: flex; flex-direction: column;
  padding: clamp(24px, 2.6vw, 34px) clamp(20px, 2.2vw, 30px) clamp(24px, 2.6vw, 30px);
  transition: background 0.35s var(--ease);
}
.stat + .stat { border-left: 1px solid rgba(123, 161, 244, 0.16); }
.stat:hover { background: rgba(120, 175, 255, 0.05); }
.stat .k {
  display: flex; align-items: center; gap: 9px;
  font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.16em; text-transform: uppercase; color: var(--ink-2);
}
.stat .k::before { content: ""; width: 12px; height: 8px; border-radius: 999px; background: linear-gradient(180deg, var(--lit), #3f7ddc); box-shadow: 0 0 0 3px rgba(39, 91, 187, 0.3); }
.stat .v {
  display: flex; align-items: baseline; gap: 6px; margin: 22px 0 0;
  font-size: clamp(2.8rem, 1.6rem + 2.6vw, 4.3rem); font-weight: 600; letter-spacing: -0.05em; line-height: 0.95;
  font-variant-numeric: tabular-nums;
}
.stat .v span {
  background: linear-gradient(180deg, #ffffff 25%, #9cc6ff 100%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}
.stat .v em { font-style: normal; font-size: 0.36em; font-weight: 500; letter-spacing: -0.01em; color: var(--ink-2); }
.stat .viz { height: 64px; margin: 26px 0 20px; display: flex; align-items: flex-end; }
.stat p { margin-top: auto; font-size: 0.9rem; line-height: 1.6; color: var(--ink-2); font-weight: 300; }

/* latency: a distribution, the median bar lit */
.hist { gap: 3px; width: 100%; position: relative; }
.hist i {
  flex: 1; height: calc(var(--h) * 100%); border-radius: 3px 3px 1px 1px;
  background: linear-gradient(180deg, rgba(120, 170, 245, 0.55), rgba(39, 91, 187, 0.2));
  transform-origin: bottom; transform: scaleY(0.04);
  transition: transform 0.9s var(--ease); transition-delay: calc(var(--i) * 18ms);
}
.hist i.p50 { background: linear-gradient(180deg, #ffffff, #8fc3ff 60%, #3f7bff); box-shadow: 0 0 14px rgba(160, 205, 255, 0.85); }
.stats.in .hist i { transform: none; }

/* regions: the ring motif, small */
.mini { position: relative; width: 100%; height: 100%; }
.mini i { position: absolute; left: 50%; top: 50%; translate: -50% -50%; border-radius: 999px; border: 1px solid rgba(164, 216, 255, 0.28); }
.mini i:nth-child(1) { width: 100%; height: 100%; background: rgba(39, 91, 187, 0.12); }
.mini i:nth-child(2) { width: 74%; height: 72%; border-color: rgba(164, 216, 255, 0.4); background: rgba(39, 91, 187, 0.16); }
.mini i:nth-child(3) { width: 48%; height: 44%; border-color: rgba(164, 216, 255, 0.55); background: rgba(63, 125, 220, 0.25); }
.mini i:nth-child(4) { width: 22%; height: 18%; border: 0; background: linear-gradient(180deg, #e4f2ff, #6aa3ef); box-shadow: 0 0 16px rgba(160, 205, 255, 0.85); }
.mini b {
  position: absolute; width: 5px; height: 5px; border-radius: 50%; translate: -50% -50%;
  background: var(--lit); box-shadow: 0 0 8px var(--lit); opacity: 0.3; animation: pulse 2.6s ease-in-out infinite;
}

/* in region: a track nearly full, with the remainder named */
.stat .viz.meter { flex-direction: column; align-items: stretch; justify-content: flex-end; gap: 10px; width: 100%; }
.meter .track { position: relative; height: 10px; border-radius: 999px; background: rgba(123, 161, 244, 0.14); overflow: hidden; }
.meter .track span {
  position: absolute; inset: 0; border-radius: inherit;
  background: linear-gradient(90deg, #275bbb, #8fc3ff 80%, #e4f2ff);
  box-shadow: 0 0 14px rgba(140, 195, 255, 0.6);
  transform-origin: left; transform: scaleX(0); transition: transform 1.3s var(--ease);
}
.stats.in .meter .track span { transform: scaleX(0.9998); }
.meter .ends { display: flex; justify-content: space-between; font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.06em; color: var(--ink-3); }
.meter .ends b { font-weight: 400; color: var(--lit); }

/* hostname: the one thing your clients need */
.host {
  display: flex; align-items: center; gap: 10px; width: 100%;
  padding: 12px 14px; border-radius: 12px;
  font-family: var(--mono); font-size: 12px; color: #d6e4ff; white-space: nowrap; overflow: hidden;
  background: rgba(2, 10, 36, 0.6); box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.2);
}
.host::before { content: ""; flex: none; width: 7px; height: 7px; border-radius: 50%; background: #5bf0b0; box-shadow: 0 0 8px #5bf0b0; }
.host span { overflow: hidden; text-overflow: ellipsis; }
.host::after { content: ""; flex: none; width: 7px; height: 14px; margin-left: -8px; background: var(--lit); animation: blink 1.1s steps(1) infinite; }
@keyframes blink { 50% { opacity: 0; } }
.caveat { margin-top: 1.4rem; font-family: var(--mono); font-size: 11.5px; letter-spacing: 0.08em; color: var(--ink-3); }

/* ---------- pricing ---------- */
.plans { display: grid; grid-template-columns: repeat(3, 1fr); gap: 18px; align-items: stretch; }
.plan { position: relative; display: flex; flex-direction: column; border-radius: 24px; padding: 30px 28px 28px; }
.plan h3 { font-size: 1.05rem; font-weight: 500; color: var(--ink-2); }
.plan .price { margin: 14px 0 6px; font-size: 2.6rem; font-weight: 600; letter-spacing: -0.04em; line-height: 1; }
.plan .price small { font-size: 0.9rem; font-weight: 400; letter-spacing: 0; color: var(--ink-3); margin-left: 4px; }
.plan .tag { font-size: 0.92rem; color: var(--ink-2); line-height: 1.6; min-height: 3.2em; }
.plan ul { margin: 22px 0 28px; display: grid; gap: 12px; flex: 1; padding-top: 22px; border-top: 1px solid var(--line); }
.plan li { display: grid; grid-template-columns: 18px 1fr; gap: 10px; font-size: 0.93rem; color: #cfdcf7; line-height: 1.5; }
.plan li::before { content: ""; width: 14px; height: 9px; margin-top: 6px; border-radius: 999px; background: linear-gradient(180deg, var(--lit), #3f7ddc); }
.plan .btn { justify-content: center; width: 100%; }
.plan.feat {
  background:
    linear-gradient(180deg, rgba(30, 78, 190, 0.55), rgba(8, 24, 80, 0.85)) padding-box,
    linear-gradient(180deg, rgba(200, 228, 255, 0.8), rgba(4, 92, 255, 0.3) 60%, rgba(123, 161, 244, 0.08)) border-box;
  box-shadow: 0 40px 90px -40px rgba(4, 92, 255, 0.85);
}
.plan.feat::before {
  content: "Most deployed"; position: absolute; top: -12px; left: 28px;
  padding: 5px 12px; border-radius: 999px; background: var(--blue); color: #fff;
  font-family: var(--mono); font-size: 10.5px; letter-spacing: 0.1em; text-transform: uppercase;
  box-shadow: 0 8px 20px -6px rgba(4, 92, 255, 0.9);
}

/* ---------- faq ---------- */
.faq-wrap { display: grid; grid-template-columns: 0.8fr 1.2fr; gap: clamp(28px, 5vw, 72px); }
.faq details { border-top: 1px solid var(--line); }
.faq details:last-child { border-bottom: 1px solid var(--line); }
.faq summary {
  list-style: none; cursor: pointer; display: flex; justify-content: space-between; align-items: center; gap: 20px;
  padding: 22px 0; font-size: 1.06rem; font-weight: 500; transition: color 0.2s;
}
.faq summary::-webkit-details-marker { display: none; }
.faq summary:hover { color: var(--lit); }
.faq summary::after {
  content: "+"; flex: none; display: grid; place-items: center; width: 30px; height: 30px; border-radius: 50%;
  font-weight: 300; font-size: 1.2rem; color: var(--lit); box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.3);
  transition: transform 0.3s var(--ease), background 0.3s;
}
.faq details[open] summary::after { transform: rotate(45deg); background: rgba(4, 92, 255, 0.35); }
.faq details p { padding: 0 48px 24px 0; color: var(--ink-2); line-height: 1.7; font-size: 0.97rem; }

/* ---------- close ---------- */
/* the closing panel: a framed window onto the hero's ring stack, rising from below */
.close { padding: clamp(4rem, 8vw, 6.5rem) 0 clamp(5rem, 9vw, 7.5rem); }
.portal {
  position: relative; overflow: hidden; isolation: isolate; text-align: center;
  border-radius: clamp(24px, 3vw, 36px);
  padding: clamp(4rem, 8vw, 6.5rem) clamp(1.25rem, 4vw, 3rem) clamp(13rem, 26vw, 19rem);
  border: 1px solid transparent;
  background:
    radial-gradient(70% 55% at 50% 0%, rgba(46, 102, 214, 0.42), transparent 70%) padding-box,
    linear-gradient(180deg, #0b2266 0%, #061440 46%, #040d2a 100%) padding-box,
    linear-gradient(180deg, rgba(200, 228, 255, 0.55), rgba(123, 161, 244, 0.14) 45%, rgba(4, 92, 255, 0.4)) border-box;
  box-shadow: 0 60px 120px -50px rgba(4, 92, 255, 0.75), inset 0 1px 0 rgba(220, 238, 255, 0.25);
}
/* fine grid, fading out toward the edges */
.portal::before {
  content: ""; position: absolute; inset: 0; z-index: -2; pointer-events: none;
  background-image:
    linear-gradient(rgba(164, 216, 255, 0.07) 1px, transparent 1px),
    linear-gradient(90deg, rgba(164, 216, 255, 0.07) 1px, transparent 1px);
  background-size: 44px 44px; background-position: center top;
  -webkit-mask-image: radial-gradient(70% 70% at 50% 30%, #000 20%, transparent 75%);
  mask-image: radial-gradient(70% 70% at 50% 30%, #000 20%, transparent 75%);
}
/* the stack, centred below the panel's bottom edge so only its upper half shows */
.portal-rings {
  position: absolute; z-index: -1; left: 50%; bottom: 0; translate: -50% 52%;
  width: min(1100px, 170%); aspect-ratio: 1100 / 520; pointer-events: none;
}
.portal-rings i {
  position: absolute; top: 50%; left: 50%; translate: -50% -50%; border-radius: 999px;
  background: linear-gradient(180deg, var(--c1) 0%, var(--c2) 40%, var(--c3) 100%);
  box-shadow: inset 0 1px 0 rgba(214, 233, 255, 0.55), 0 0 40px -14px rgba(120, 178, 255, 0.55);
}
.portal-rings i:nth-child(1) { width: 100%; height: 100%; --c1: #2c5bab; --c2: #133176; --c3: #0a1c4d; }
.portal-rings i:nth-child(2) { width: 82%; height: 82%; --c1: #3e74cc; --c2: #1a409a; --c3: #0c2260; }
.portal-rings i:nth-child(3) { width: 64%; height: 64%; --c1: #5b93e6; --c2: #24509f; --c3: #0e2a6e; }
.portal-rings i:nth-child(4) { width: 46%; height: 46%; --c1: #8dbcf6; --c2: #3468c8; --c3: #11337f; }
.portal-rings i:nth-child(5) { width: 30%; height: 30%; --c1: #c6e2ff; --c2: #5a94e8; --c3: #1b4aab; }
/* the band of light where the stack meets the content */
.portal-rings b {
  position: absolute; inset: 0; mix-blend-mode: screen;
  background: radial-gradient(42% 16% at 50% 2%, rgba(235, 245, 255, 0.75), rgba(160, 205, 255, 0.25) 50%, transparent 80%);
}

.portal .lbl { justify-content: center; }
.portal h2 {
  font-size: clamp(2.3rem, 1.1rem + 4.2vw, 4.4rem); font-weight: 600; letter-spacing: -0.04em; line-height: 1.04;
  text-wrap: balance; text-shadow: 0 8px 40px rgba(4, 13, 42, 0.6);
}
.portal > p {
  max-width: 44ch; margin: 1.3rem auto 2.4rem;
  color: #c3d2f2; line-height: 1.7; font-weight: 300; font-size: clamp(1rem, 0.94rem + 0.3vw, 1.14rem); text-wrap: pretty;
}
/* the closing button is the same light ring as the hero's, sized to its content,
   with two faint outer bands echoing the rings rising below it */
.portal .cta.cta--ring {
  width: auto; height: auto; padding: 20px clamp(34px, 4vw, 56px);
  font-size: clamp(1rem, 0.92rem + 0.4vw, 1.2rem);
  box-shadow:
    inset 0 1px 0 rgba(255, 255, 255, 0.95),
    inset 0 -10px 22px -12px rgba(10, 40, 130, 0.45),
    0 0 0 8px rgba(91, 147, 230, 0.16),
    0 0 0 16px rgba(46, 99, 196, 0.12),
    0 20px 60px -18px rgba(150, 200, 255, 0.7);
}
.portal .cta.cta--ring:hover {
  box-shadow:
    inset 0 1px 0 #fff,
    inset 0 -10px 22px -12px rgba(10, 40, 130, 0.4),
    0 0 0 8px rgba(120, 175, 245, 0.24),
    0 0 0 16px rgba(60, 120, 220, 0.16),
    0 24px 70px -14px rgba(180, 220, 255, 0.9);
}

/* ---------- footer ---------- */
/* the footer: a glowing horizon, the link columns, a status bar, and the wordmark set huge and cropped */
.ft {
  position: relative; overflow: hidden; isolation: isolate;
  padding: clamp(4.5rem, 8vw, 6.5rem) 0 0;
  background:
    radial-gradient(70% 55% at 50% 100%, rgba(4, 92, 255, 0.2), transparent 70%),
    linear-gradient(180deg, transparent 0%, #030a22 100%);
}
.ft::before {
  content: ""; position: absolute; top: 0; left: 50%; translate: -50% 0; width: min(1180px, 100% - 40px); height: 1px;
  background: linear-gradient(90deg, transparent, rgba(164, 216, 255, 0.55) 50%, transparent);
}
.ft::after {
  content: ""; position: absolute; z-index: -1; top: -60px; left: 50%; translate: -50% 0; width: min(760px, 90%); height: 120px;
  background: radial-gradient(closest-side, rgba(90, 150, 255, 0.28), transparent); pointer-events: none;
}
.ft-top { display: grid; grid-template-columns: minmax(0, 1.15fr) minmax(0, 2fr); gap: clamp(36px, 6vw, 88px); }
.ft-brand p { margin-top: 16px; max-width: 34ch; color: var(--ink-2); font-size: 0.95rem; line-height: 1.65; font-weight: 300; }
.ft-news { margin-top: 28px; }
.ft-news label { display: block; margin-bottom: 10px; font-family: var(--mono); font-size: 11px; letter-spacing: 0.14em; text-transform: uppercase; color: var(--ink-3); }
.ft-news .field {
  display: flex; align-items: center; gap: 6px; max-width: 380px; padding: 5px 5px 5px 18px; border-radius: 999px;
  background: rgba(8, 24, 76, 0.55);
  box-shadow: inset 0 0 0 1px rgba(164, 216, 255, 0.22), 0 14px 40px -24px rgba(4, 92, 255, 0.9);
  transition: box-shadow 0.25s var(--ease);
}
.ft-news .field:focus-within { box-shadow: inset 0 0 0 1px rgba(200, 228, 255, 0.6), 0 14px 40px -20px rgba(4, 92, 255, 1); }
.ft-news input { flex: 1; min-width: 0; border: 0; outline: 0; background: none; font: inherit; font-size: 0.92rem; color: #fff; }
.ft-news input::placeholder { color: var(--ink-3); }
.ft-news button { font: inherit; border: 0; cursor: pointer; padding: 10px 20px; white-space: nowrap; }
.ft-cols { display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 28px; }
.ft-cols h4 { font-family: var(--mono); font-size: 11px; font-weight: 500; letter-spacing: 0.16em; text-transform: uppercase; color: var(--lit); margin-bottom: 18px; }
.ft-cols li + li { margin-top: 12px; }
.ft-cols a { position: relative; font-size: 0.94rem; color: var(--ink-2); transition: color 0.2s, padding 0.3s var(--ease); }
.ft-cols a::before { content: ""; position: absolute; left: 0; top: 50%; width: 0; height: 1px; background: var(--lit); transition: width 0.3s var(--ease); }
.ft-cols a:hover { color: #fff; padding-left: 14px; }
.ft-cols a:hover::before { width: 8px; }
.ft-cols .tag { margin-left: 8px; padding: 2px 7px; border-radius: 999px; font-family: var(--mono); font-size: 9.5px; letter-spacing: 0.1em; text-transform: uppercase; color: #fff; background: rgba(4, 92, 255, 0.55); vertical-align: 2px; }
.ft-bar {
  display: flex; justify-content: space-between; align-items: center; gap: 14px 28px; flex-wrap: wrap;
  margin-top: clamp(3.5rem, 6vw, 5rem); padding: 1.4rem 0; border-top: 1px solid var(--line);
  font-family: var(--mono); font-size: 11px; line-height: 1.7; letter-spacing: 0.04em; color: var(--ink-3);
}
.status { display: inline-flex; align-items: center; gap: 9px; padding: 7px 14px; border-radius: 999px; font-family: var(--mono); font-size: 11px; color: var(--ink-2); background: rgba(91, 240, 176, 0.06); box-shadow: inset 0 0 0 1px rgba(91, 240, 176, 0.22); }
.status::before { content: ""; width: 7px; height: 7px; border-radius: 50%; background: #5bf0b0; box-shadow: 0 0 8px #5bf0b0; animation: pulse 2.4s ease-in-out infinite; }
.ft-legal { display: flex; gap: 22px; }
.ft-legal a:hover { color: #fff; }
.ft-mark {
  display: block; text-align: center; pointer-events: none; user-select: none;
  margin: clamp(1.5rem, 4vw, 3rem) 0 -0.17em;
  font-size: clamp(5.5rem, 21vw, 19rem); font-weight: 600; letter-spacing: -0.055em; line-height: 0.82;
  background: linear-gradient(180deg, rgba(164, 216, 255, 0.34) 0%, rgba(80, 140, 240, 0.12) 55%, rgba(4, 13, 42, 0) 92%);
  -webkit-background-clip: text; background-clip: text; color: transparent;
}
.ft-note { padding: 0; margin-top: -0.2rem; max-width: 70ch; font-family: var(--mono); font-size: 10.5px; line-height: 1.8; letter-spacing: 0.04em; color: var(--ink-3); }

/* ---------- reveal ---------- */
.js .rv { opacity: 0; transform: translateY(22px); transition: opacity 0.9s var(--ease), transform 0.9s var(--ease); transition-delay: var(--rd, 0s); }
.js .rv.in { opacity: 1; transform: none; }

/* ============================================================ RESPONSIVE */
@media (max-width: 1100px) {
  .stats { grid-template-columns: repeat(2, minmax(0, 1fr)); }
  .stat:nth-child(3) { border-left: 0; }
  .stat:nth-child(n+3) { border-top: 1px solid rgba(123, 161, 244, 0.16); }
}
@media (max-width: 1020px) {
  .readout { display: none; }
  .nav-r .ghost { display: none; }
}
@media (max-width: 760px) {
  .feats li { gap: 7px; padding: 2px 11px; }
  .feats svg { width: 17px; height: 17px; }
  .feats b { font-size: 10px; letter-spacing: 0.08em; }
}
@media (max-width: 900px) {
  .pillnav { display: none; }
  .bento { grid-template-columns: 1fr; }
  .span-4, .span-2 { grid-column: auto; }
  .how, .faq-wrap { grid-template-columns: 1fr; }
  .term { position: relative; top: 0; }
  .plans { grid-template-columns: 1fr; max-width: 460px; margin-inline: auto; }
  .ft-top { grid-template-columns: minmax(0, 1fr); }
  .ft-cols { grid-template-columns: repeat(2, minmax(0, 1fr)); row-gap: 34px; }
  .dotmap { grid-template-columns: repeat(20, 1fr); }
  .dotmap i:nth-child(n+101) { display: none; }
}
@media (max-width: 560px) {
  .stats { grid-template-columns: minmax(0, 1fr); }
  .stat + .stat { border-left: 0; border-top: 1px solid rgba(123, 161, 244, 0.16); }
  /* a taller stack on phones, so the inner ring is big enough to hold the label */
  .ringstack { aspect-ratio: 1 / 0.66; }
  .rings i:nth-child(1) { width: 100%; height: 100%; }
  .rings i:nth-child(2) { width: 91%; height: 84%; }
  .rings i:nth-child(3) { width: 82%; height: 68%; }
  .rings i:nth-child(4) { width: 73%; height: 52%; }
  .rings i:nth-child(5) { width: 64%; height: 37%; }
  .ringstack .cta-slot { width: 56%; height: 24%; }
  .cta.cta--ring { font-size: 0.8rem; gap: 0.45em; padding: 0 3%; }
  .portal .cta.cta--ring { font-size: 0.95rem; padding: 17px 28px; }
  .lat-row { grid-template-columns: 1fr; gap: 10px; }
  .eyebrow { font-size: 12px; }
  .term pre { font-size: 12px; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after { animation: none !important; transition-duration: 0.01ms !important; }
}
</style>
</head>
<body>

<nav class="nav" aria-label="Main" data-section="nav">
  <div class="wrap">
    <a class="brand" href="#top">
      <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
        <circle cx="12" cy="12" r="3.2" fill="#a4d8ff"/>
        <ellipse cx="12" cy="12" rx="10" ry="5.6" stroke="#4e8ae8" stroke-width="1.5"/>
        <ellipse cx="12" cy="12" rx="5.6" ry="10" stroke="#275bbb" stroke-width="1.5"/>
      </svg>
      Proxima
    </a>
    <div class="pillnav" id="pillnav" data-component="pill-nav">
      <span class="glide" id="glide" aria-hidden="true"></span>
      <a href="#network" class="on">Network</a>
      <a href="#latency">Latency</a>
      <a href="#how">How it works</a>
      <a href="#pricing">Pricing</a>
      <a href="#faq">FAQ</a>
    </div>
    <div class="nav-r">
      <a class="ghost" href="#how">Docs</a>
      <a class="btn btn--blue" href="#start">Sign in</a>
    </div>
  </div>
</nav>

<header class="hero" id="top" data-section="hero">
  <span class="lightsrc" id="lightsrc" aria-hidden="true"></span>
  <div class="stars" id="stars" aria-hidden="true"></div>

  <div class="hero-in">
    <div class="wrap">
      <a class="eyebrow" href="#latency">
        <b>New</b>
        Edge inference is live in 214 regions
        <svg viewBox="0 0 16 16" fill="none" stroke="currentColor" stroke-width="1.6" aria-hidden="true"><path d="M3 8h9M9 4.5 12.5 8 9 11.5" stroke-linecap="round" stroke-linejoin="round"/></svg>
      </a>
      <h1>Run the model<br />next to the request.</h1>
      <p class="hero-sub">Proxima runs your model in every region your users are in, and answers from the nearest one.</p>
      <ul class="feats">
        <li>
          <svg viewBox="0 0 30 30" fill="none" stroke="currentColor" stroke-width="1.4" aria-hidden="true">
            <rect x="1.5" y="6" width="27" height="18" rx="9" opacity=".45"/><rect x="6" y="9.5" width="18" height="11" rx="5.5" opacity=".75"/><rect x="10.5" y="12.5" width="9" height="5" rx="2.5" fill="currentColor"/>
          </svg>
          <b>214 regions</b>
        </li>
        <li>
          <svg viewBox="0 0 30 30" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" aria-hidden="true">
            <circle cx="15" cy="3.5" r="2" fill="currentColor" stroke="none"/><path d="M15 6.5v10"/><rect x="3" y="14" width="24" height="13" rx="6.5" opacity=".55"/><rect x="9" y="17.5" width="12" height="6" rx="3" fill="currentColor" stroke="none"/>
          </svg>
          <b>Nearest edge</b>
        </li>
        <li>
          <svg viewBox="0 0 30 30" fill="none" stroke="currentColor" stroke-width="1.4" stroke-linecap="round" aria-hidden="true">
            <path d="M4 21a11 11 0 0 1 22 0" opacity=".55"/><path d="M8.5 21a6.5 6.5 0 0 1 13 0" opacity=".8"/><path d="M15 21l4.5-6"/><circle cx="15" cy="21" r="1.8" fill="currentColor" stroke="none"/>
          </svg>
          <b>18 ms p50</b>
        </li>
      </ul>
    </div>

    <div class="ringstack">
      <div class="rings" aria-hidden="true"><i></i><i></i><i></i><i></i><i></i></div>
      <div class="beam" aria-hidden="true"><i id="beamcore"></i></div>
      <div class="readout ro-1" aria-hidden="true"><small>Frankfurt</small><b>11<em>ms p50</em></b></div>
      <div class="readout ro-2" aria-hidden="true"><small>Tokyo</small><b>Warm<em>· 3 replicas</em></b></div>
      <div class="readout ro-3" aria-hidden="true"><small>Throughput</small><b>1.2M<em>req / min</em></b></div>
      <div class="readout ro-4" aria-hidden="true"><small>São Paulo</small><b>19<em>ms p50</em></b></div>
      <div class="cta-slot">
        <a class="cta cta--ring" href="#start">
          Deploy in one region free
          <svg viewBox="0 0 28 20" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
            <path d="M2 10h22M17 4l6 6-6 6M13 4l6 6-6 6" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </a>
      </div>
    </div>

    <div class="logos wrap">
      <p>Serving at the edge for teams like these · placeholder names</p>
      <ul>
        <li><svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.6" aria-hidden="true"><path d="M3 15 10 4l7 11z"/></svg>Kestrel</li>
        <li class="caps">Oxbow</li>
        <li class="serif">Tessellate</li>
        <li><svg viewBox="0 0 20 20" fill="none" stroke="currentColor" stroke-width="1.6" aria-hidden="true"><circle cx="10" cy="10" r="6.5"/><circle cx="10" cy="10" r="2.5" fill="currentColor"/></svg>Meridian&nbsp;Nine</li>
        <li class="caps">Quillray</li>
        <li class="serif">Halden&nbsp;&amp;&nbsp;Moor</li>
      </ul>
    </div>
  </div>
</header>

<main>
  <!-- ======================= NETWORK ======================= -->
  <section class="sec" id="network" data-section="features">
    <div class="wrap">
      <div class="sec-head rv">
        <h2>Distance is the part of latency you cannot optimise away.</h2>
        <p>You can quantise the model, batch the requests and rewrite the kernel, and the packet still has to cross an ocean. Proxima moves the model instead.</p>
      </div>
      <div class="bento">
        <article class="tile surface span-4 rv">
          <div class="vis"><div class="dotmap" id="dotmap"></div></div>
          <h3>Two hundred places, one deploy</h3>
          <p>One push lands everywhere at once. Requests resolve to the nearest healthy box without you writing a routing table, or ever maintaining one.</p>
        </article>
        <article class="tile surface span-2 rv" style="--rd:.08s">
          <div class="vis">
            <div class="warm">
              <div>Warm hit rate<div class="track"><span style="--w:96%"></span></div></div>
              <div>Cold starts / region<div class="track"><span style="--w:6%"></span></div></div>
              <div>Weights resident<div class="track"><span style="--w:88%"></span></div></div>
            </div>
          </div>
          <h3>Weights stay warm</h3>
          <p>A region that has served your model keeps it resident. A new region costs one cold start, not one per call.</p>
        </article>
        <article class="tile surface span-2 rv">
          <div class="vis">
            <div class="minirings">
              <i></i><i></i><i></i>
              <svg viewBox="0 0 100 100" preserveAspectRatio="none" aria-hidden="true">
                <path d="M50 30 Q 72 26 82 50" fill="none" stroke="rgba(164,216,255,.7)" stroke-width="0.8" stroke-dasharray="2 2" vector-effect="non-scaling-stroke"/>
              </svg>
              <b class="down"></b><b class="up"></b>
            </div>
          </div>
          <h3>Fails to the next ring</h3>
          <p>A region going dark is a routing event, not an outage. The caller sees a slightly slower answer, not an error.</p>
        </article>
        <article class="tile surface span-4 rv" style="--rd:.08s">
          <div class="vis">
            <div class="chips">
              <span class="hot">GGUF</span><span>safetensors</span><span>ONNX</span><span class="hot">TensorRT plan</span>
              <span>Core ML</span><span>LoRA adapters</span><span>int4 · int8 · fp16</span><span>streaming</span><span class="hot">speculative decoding</span>
            </div>
          </div>
          <h3>Bring the build you already have</h3>
          <p>Proxima does not ask for your training code or your framework of the month. Ship the artifact you already produce and pick the precision per region.</p>
        </article>
      </div>
    </div>
  </section>

  <!-- ======================= LATENCY ======================= -->
  <section class="sec" id="latency" data-section="latency">
    <div class="wrap">
      <div class="sec-head rv">
        <h2>The same model, measured from the same six cities.</h2>
        <p>Time to first token from a single origin in us-east, against the nearest Proxima region. The gap is the round trip you were paying for.</p>
      </div>
      <div class="lat surface rv" id="lat">
        <div class="lat-key"><span style="--k:#56679a">Single origin</span><span style="--k:#a4d8ff">Proxima edge</span></div>
        <div class="lat-row"><h4>Sydney<small>SYD</small></h4><div class="bars"><div class="bar o"><i style="--w:88%"></i><span>212 ms</span></div><div class="bar p"><i style="--w:7%"></i><span>16 ms</span></div></div></div>
        <div class="lat-row"><h4>Mumbai<small>BOM</small></h4><div class="bars"><div class="bar o"><i style="--w:99%"></i><span>238 ms</span></div><div class="bar p"><i style="--w:9%"></i><span>21 ms</span></div></div></div>
        <div class="lat-row"><h4>Lagos<small>LOS</small></h4><div class="bars"><div class="bar o"><i style="--w:84%"></i><span>201 ms</span></div><div class="bar p"><i style="--w:10%"></i><span>24 ms</span></div></div></div>
        <div class="lat-row"><h4>Tokyo<small>NRT</small></h4><div class="bars"><div class="bar o"><i style="--w:68%"></i><span>162 ms</span></div><div class="bar p"><i style="--w:6%"></i><span>14 ms</span></div></div></div>
        <div class="lat-row"><h4>São Paulo<small>GRU</small></h4><div class="bars"><div class="bar o"><i style="--w:62%"></i><span>148 ms</span></div><div class="bar p"><i style="--w:8%"></i><span>19 ms</span></div></div></div>
        <div class="lat-row"><h4>Frankfurt<small>FRA</small></h4><div class="bars"><div class="bar o"><i style="--w:39%"></i><span>94 ms</span></div><div class="bar p"><i style="--w:5%"></i><span>11 ms</span></div></div></div>
      </div>
      <p class="caveat">Illustrative figures for a fictional product. Nothing here was measured.</p>
    </div>
  </section>

  <!-- ======================= HOW ======================= -->
  <section class="sec" id="how" data-section="how-it-works">
    <div class="wrap">
      <div class="sec-head rv">
        <h2>Three calls, then it is somebody else's problem.</h2>
      </div>
      <div class="how">
        <div class="steps">
          <article class="step rv">
            <div>
              <h3>Push the artifact</h3>
              <p>One build, whatever you already produce. It is checksummed once and replicated from there, so the upload is the slowest part of your day.</p>
            </div>
          </article>
          <article class="step rv">
            <div>
              <h3>Pick a footprint</h3>
              <p>One region, a continent, or everywhere. It is a number in a config, and changing it is a deploy rather than a migration.</p>
            </div>
          </article>
          <article class="step rv">
            <div>
              <h3>Point your clients at one host</h3>
              <p>The same hostname everywhere. Anycast puts the call on the nearest edge, and the answer streams back from there.</p>
            </div>
          </article>
        </div>
        <div class="term surface rv" style="--rd:.1s">
          <div class="term-bar"><i></i><i></i><i></i><span>proxima.toml</span></div>
<pre><span class="k">model</span>     = <span class="s">"./build/model-q4.gguf"</span>
<span class="k">footprint</span> = <span class="s">"global"</span>      <span class="c"># "eu" · "us-west" · 1</span>
<span class="k">warm</span>      = <span class="k">true</span>
<span class="k">failover</span>  = <span class="s">"next-ring"</span></pre>
          <hr />
<pre><span class="dim">$</span> proxima deploy
  <span class="ok">✓</span> pushed   <span class="dim">4.1 GB · sha256 9f2c…e01</span>
  <span class="ok">✓</span> placed   <span class="dim">214 regions · 38s</span>
  <span class="ok">✓</span> warm     <span class="dim">214 / 214</span>
  <span class="ok">✓</span> live     <span class="k">https://infer.proxima.example</span></pre>
        </div>
      </div>
    </div>
  </section>

  <!-- ======================= NUMBERS ======================= -->
  <section class="sec" id="numbers" data-section="stats">
    <div class="wrap">
      <div class="sec-head rv">
        <h2>What it looks like from the caller's side.</h2>
      </div>
      <div class="stats rv" id="stats">
        <div class="stat">
          <span class="k">Time to first token</span>
          <div class="v"><span data-to="18">18</span><em>ms p50</em></div>
          <div class="viz hist" aria-hidden="true"><i style="--h:0.11;--i:0"></i><i style="--h:0.17;--i:1"></i><i style="--h:0.29;--i:2"></i><i style="--h:0.47;--i:3"></i><i style="--h:0.69;--i:4"></i><i style="--h:0.91;--i:5"></i><i style="--h:1.00;--i:6"></i><i class="p50" style="--h:1.00;--i:7"></i><i style="--h:0.95;--i:8"></i><i style="--h:0.76;--i:9"></i><i style="--h:0.56;--i:10"></i><i style="--h:0.41;--i:11"></i><i style="--h:0.32;--i:12"></i><i style="--h:0.27;--i:13"></i><i style="--h:0.24;--i:14"></i><i style="--h:0.23;--i:15"></i><i style="--h:0.22;--i:16"></i><i style="--h:0.21;--i:17"></i><i style="--h:0.19;--i:18"></i><i style="--h:0.18;--i:19"></i><i style="--h:0.16;--i:20"></i><i style="--h:0.14;--i:21"></i><i style="--h:0.13;--i:22"></i><i style="--h:0.11;--i:23"></i><i style="--h:0.10;--i:24"></i><i style="--h:0.09;--i:25"></i><i style="--h:0.08;--i:26"></i><i style="--h:0.07;--i:27"></i></div>
          <p>Median from request to first token, measured at the caller.</p>
        </div>
        <div class="stat">
          <span class="k">Regions serving</span>
          <div class="v"><span data-to="214">214</span></div>
          <div class="viz" aria-hidden="true">
            <div class="mini"><i></i><i></i><i></i><i></i>
              <b style="left:8%;top:30%"></b><b style="left:30%;top:6%;animation-delay:-.6s"></b><b style="left:72%;top:8%;animation-delay:-1.2s"></b>
              <b style="left:94%;top:60%;animation-delay:-1.8s"></b><b style="left:20%;top:88%;animation-delay:-.9s"></b><b style="left:64%;top:94%;animation-delay:-2.2s"></b>
            </div>
          </div>
          <p>Each one holds a warm copy of your weights.</p>
        </div>
        <div class="stat">
          <span class="k">Answered in region</span>
          <div class="v"><span data-to="99.98" data-dp="2">99.98</span><em>%</em></div>
          <div class="viz meter" aria-hidden="true">
            <div class="track"><span></span></div>
            <div class="ends"><span>Nearest region</span><b>0.02% next ring</b></div>
          </div>
          <p>The rest fail over one ring out, slower but never an error.</p>
        </div>
        <div class="stat">
          <span class="k">Hostnames to configure</span>
          <div class="v"><span data-to="1">1</span></div>
          <div class="viz" aria-hidden="true"><div class="host"><span>infer.proxima.example</span></div></div>
          <p>The same address everywhere. Anycast does the rest.</p>
        </div>
      </div>
      <p class="caveat">Invented product, invented figures. Nothing here was measured.</p>
    </div>
  </section>

  <!-- ======================= PRICING ======================= -->
  <section class="sec" id="pricing" data-section="pricing">
    <div class="wrap">
      <div class="sec-head center rv">
        <h2>Pay for tokens, not for distance.</h2>
        <p>Every plan uses the same network. What changes is how far your model reaches and how much of it stays warm.</p>
      </div>
      <div class="plans">
        <article class="plan surface rv">
          <h3>Region</h3>
          <div class="price">$0<small>/ month</small></div>
          <p class="tag">One region of your choice, free for as long as you keep it.</p>
          <ul>
            <li>1 region, any continent</li>
            <li>2M tokens a month</li>
            <li>Shared GPU pool</li>
            <li>Community support</li>
          </ul>
          <a class="btn btn--line" href="#start">Deploy free</a>
        </article>
        <article class="plan feat rv" style="--rd:.08s">
          <h3>Continent</h3>
          <div class="price">$0.38<small>/ 1M tokens</small></div>
          <p class="tag">Up to forty regions with the weights kept warm in all of them.</p>
          <ul>
            <li>Up to 40 regions</li>
            <li>Weights kept resident</li>
            <li>Failover to the next ring</li>
            <li>Per-region precision</li>
            <li>Email support, one-day response</li>
          </ul>
          <a class="btn btn--blue" href="#start">Start a continent</a>
        </article>
        <article class="plan surface rv" style="--rd:.16s">
          <h3>Everywhere</h3>
          <div class="price">Custom</div>
          <p class="tag">All 214 regions, reserved capacity, and a person who knows your model.</p>
          <ul>
            <li>Every region, reserved</li>
            <li>Private interconnect</li>
            <li>Regional data pinning</li>
            <li>Named engineer</li>
          </ul>
          <a class="btn btn--line" href="#start">Talk to us</a>
        </article>
      </div>
      <p class="caveat" style="text-align:center">Prices are invented for this demo.</p>
    </div>
  </section>

  <!-- ======================= FAQ ======================= -->
  <section class="sec" id="faq" data-section="faq">
    <div class="wrap faq-wrap">
      <div class="sec-head rv" style="margin-bottom:0">
        <h2>Things people ask before the first deploy.</h2>
        <p>Anything else, the docs go deeper, and a person answers the inbox.</p>
      </div>
      <div class="faq rv" style="--rd:.08s">
        <details open>
          <summary>What counts as a region?</summary>
          <p>A metro with its own GPUs and its own copy of your weights. Two edges in the same city count once. A region is the smallest unit you can add or remove.</p>
        </details>
        <details>
          <summary>Do I have to change my client?</summary>
          <p>Only the hostname. The API is plain HTTP with server-sent events for streaming, and the request and response shapes are the same in every region.</p>
        </details>
        <details>
          <summary>What happens when a region fails?</summary>
          <p>Anycast stops advertising it and the next ring out picks up the call. In-flight streams are retried once on the new region, and the caller sees added latency rather than an error.</p>
        </details>
        <details>
          <summary>Where does my data go?</summary>
          <p>A request is processed in the region it lands in and not stored afterwards. On the Everywhere plan you can pin traffic to a set of regions for residency.</p>
        </details>
        <details>
          <summary>Can I run a different model per region?</summary>
          <p>Yes. Footprint and precision are set per region, so you can serve an int4 build at the far edge and fp16 closer to home from the same deploy.</p>
        </details>
      </div>
    </div>
  </section>

  <!-- ======================= CLOSE ======================= -->
  <section class="close" id="start" data-section="cta">
    <div class="wrap">
      <div class="portal rv">
        <div class="portal-rings" aria-hidden="true"><i></i><i></i><i></i><i></i><i></i><b></b></div>
        <h2>Put it where<br />the people are.</h2>
        <p>Deploy into one region for nothing, and watch what the round trip was costing you.</p>
        <a class="cta cta--ring" href="#top">
          Deploy in one region free
          <svg viewBox="0 0 28 20" fill="none" stroke="currentColor" stroke-width="1.5" aria-hidden="true">
            <path d="M2 10h22M17 4l6 6-6 6M13 4l6 6-6 6" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </a>
      </div>
    </div>
  </section>
</main>

<footer class="ft" data-section="footer">
  <div class="wrap">
    <div class="ft-top">
      <div class="ft-brand">
        <a class="brand" href="#top">
          <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
            <circle cx="12" cy="12" r="3.2" fill="#a4d8ff"/>
            <ellipse cx="12" cy="12" rx="10" ry="5.6" stroke="#4e8ae8" stroke-width="1.5"/>
            <ellipse cx="12" cy="12" rx="5.6" ry="10" stroke="#275bbb" stroke-width="1.5"/>
          </svg>
          Proxima
        </a>
        <p>The inference edge. Your model, in every region your users are in.</p>
        <form class="ft-news" id="ftnews" novalidate>
          <label for="ftemail">The changelog, once a month</label>
          <div class="field">
            <input id="ftemail" type="email" placeholder="you@company.com" autocomplete="email" />
            <button class="btn btn--blue" type="submit">Subscribe</button>
          </div>
        </form>
      </div>
      <nav class="ft-cols" aria-label="Footer">
        <div><h4>Product</h4><ul><li><a href="#network">Network</a></li><li><a href="#latency">Latency</a></li><li><a href="#pricing">Pricing</a></li><li><a href="#numbers">Status</a></li></ul></div>
        <div><h4>Developers</h4><ul><li><a href="#how">Docs</a></li><li><a href="#how">CLI</a></li><li><a href="#how">API reference</a></li><li><a href="#faq">Changelog</a><span class="tag">New</span></li></ul></div>
        <div><h4>Company</h4><ul><li><a href="#top">About</a></li><li><a href="#top">Careers</a></li><li><a href="#faq">Security</a></li><li><a href="#start">Contact</a></li></ul></div>
        <div><h4>Connect</h4><ul><li><a href="#top">GitHub</a></li><li><a href="#top">X</a></li><li><a href="#top">Discord</a></li><li><a href="#top">RSS</a></li></ul></div>
      </nav>
    </div>
    <div class="ft-bar">
      <span class="status">All 214 regions operational</span>
      <span>© 2026 Proxima. A fictional product.</span>
      <span class="ft-legal"><a href="#top">Privacy</a><a href="#top">Terms</a><a href="#top">Cookies</a></span>
    </div>
    <p class="ft-note">This page is a design demo. The network, the claims, the customers and every figure are invented. One file, no images, no libraries.</p>
  </div>
  <div class="ft-mark" aria-hidden="true">Proxima</div>
</footer>

<script>
(() => {
"use strict";
document.documentElement.classList.add("js");
const REDUCED = matchMedia("(prefers-reduced-motion: reduce)").matches;

/* starfield, placed once from a seeded generator */
(() => {
  const host = document.getElementById("stars");
  if (!host) return;
  let x = 20250927;
  const rnd = () => ((x = (x * 48271) % 2147483647) / 2147483647);
  const frag = document.createDocumentFragment();
  for (let i = 0; i < 72; i++) {
    const s = document.createElement("i");
    s.style.left = (rnd() * 100).toFixed(2) + "%";
    s.style.top = (rnd() * 100).toFixed(2) + "%";
    s.style.setProperty("--o", (0.14 + rnd() * 0.45).toFixed(2));
    s.style.width = s.style.height = (rnd() < 0.15 ? 3 : 2) + "px";
    frag.appendChild(s);
  }
  host.appendChild(frag);


  /* region dot map in the bento */
  const map = document.getElementById("dotmap");
  if (map) {
    const f = document.createDocumentFragment();
    for (let i = 0; i < 160; i++) {
      const d = document.createElement("i");
      if (rnd() < 0.24) { d.className = "on"; d.style.setProperty("--d", (rnd() * -3).toFixed(2) + "s"); }
      f.appendChild(d);
    }
    map.appendChild(f);
  }
})();

/* the light, tracking the pointer */
(() => {
  const hero = document.querySelector(".hero");
  const src = document.getElementById("lightsrc");
  const core = document.getElementById("beamcore");
  if (!hero || !src || !core) return;
  const REST = { x: 0.18, y: -0.06 };
  let tx = REST.x, ty = REST.y, cx = REST.x, cy = REST.y;
  let raf = 0, visible = true;
  function place() {
    const r = hero.getBoundingClientRect();
    src.style.transform = "translate3d(" + (cx * r.width).toFixed(1) + "px," + (cy * r.height).toFixed(1) + "px,0)";
    core.style.transform = "translate3d(" + ((cx - 0.5) * 34).toFixed(2) + "%,0,0)";
  }
  place();
  addEventListener("resize", place);
  if (REDUCED) return;
  hero.addEventListener("pointermove", (e) => {
    const r = hero.getBoundingClientRect();
    tx = (e.clientX - r.left) / r.width;
    ty = (e.clientY - r.top) / r.height;
    start();
  });
  hero.addEventListener("pointerleave", () => { tx = REST.x; ty = REST.y; start(); });
  function frame() {
    raf = requestAnimationFrame(frame);
    cx += (tx - cx) * 0.085; cy += (ty - cy) * 0.085;
    place();
    if (Math.abs(tx - cx) < 0.0008 && Math.abs(ty - cy) < 0.0008) { cancelAnimationFrame(raf); raf = 0; }
  }
  const start = () => { if (!raf && visible && !document.hidden) raf = requestAnimationFrame(frame); };
  new IntersectionObserver((es) => {
    for (const e of es) visible = e.isIntersecting;
    if (!visible && raf) { cancelAnimationFrame(raf); raf = 0; }
  }).observe(hero);
})();

/* footer subscribe: a demo, so it only confirms in place and sends nothing */
(() => {
  const f = document.getElementById("ftnews");
  if (!f) return;
  f.addEventListener("submit", (e) => {
    e.preventDefault();
    const b = f.querySelector("button"), i = f.querySelector("input");
    b.textContent = "You're on the list"; b.disabled = true; i.value = ""; i.disabled = true;
  });
})();

/* numbers: count up once the panel scrolls in */
(() => {
  const panel = document.getElementById("stats");
  if (!panel) return;
  const nums = [...panel.querySelectorAll("[data-to]")];
  const fmt = (v, dp) => v.toFixed(dp);
  if (REDUCED || !("IntersectionObserver" in window)) { panel.classList.add("in"); return; }
  nums.forEach((n) => (n.textContent = fmt(0, +(n.dataset.dp || 0))));
  const io = new IntersectionObserver((es) => {
    if (!es.some((e) => e.isIntersecting)) return;
    io.disconnect();
    panel.classList.add("in");
    const t0 = performance.now(), dur = 1500;
    const tick = (t) => {
      const k = Math.min(1, (t - t0) / dur), e = 1 - Math.pow(1 - k, 4);
      nums.forEach((n) => (n.textContent = fmt(+n.dataset.to * e, +(n.dataset.dp || 0))));
      if (k < 1) requestAnimationFrame(tick);
    };
    requestAnimationFrame(tick);
  }, { threshold: 0.35 });
  io.observe(panel);
})();

/* pill nav */
(() => {
  const nav = document.getElementById("pillnav");
  const glide = document.getElementById("glide");
  if (!nav || !glide) return;
  const links = [...nav.querySelectorAll("a")];
  function move(to) {
    const r = to.getBoundingClientRect(), n = nav.getBoundingClientRect();
    glide.style.width = r.width + "px";
    glide.style.transform = "translateX(" + (r.left - n.left) + "px)";
  }
  const setOn = (a) => { for (const b of links) b.classList.toggle("on", b === a); move(a); };
  const active = () => links.find((a) => a.classList.contains("on")) || links[0];
  for (const a of links) {
    a.addEventListener("pointerenter", () => move(a));
    a.addEventListener("focus", () => move(a));
    a.addEventListener("click", () => setOn(a));
  }
  nav.addEventListener("pointerleave", () => move(active()));
  const settle = () => move(active());
  settle();
  if (document.fonts && document.fonts.ready) document.fonts.ready.then(settle);
  addEventListener("resize", settle);
  const map = new Map(links.map((a) => [a.getAttribute("href").slice(1), a]));
  const io = new IntersectionObserver((es) => {
    for (const e of es) if (e.isIntersecting && map.get(e.target.id)) setOn(map.get(e.target.id));
  }, { rootMargin: "-45% 0px -50% 0px" });
  for (const id of map.keys()) { const el = document.getElementById(id); if (el) io.observe(el); }
})();

/* reveal on scroll, and the latency bars draw in */
(() => {
  const els = document.querySelectorAll(".rv");
  if (REDUCED || !("IntersectionObserver" in window)) { els.forEach((e) => e.classList.add("in")); return; }
  const io = new IntersectionObserver((es) => {
    for (const e of es) if (e.isIntersecting) { e.target.classList.add("in"); io.unobserve(e.target); }
  }, { rootMargin: "0px 0px -10% 0px", threshold: 0.08 });
  els.forEach((e) => io.observe(e));
})();
})();
</script>
</body>
</html>
```

