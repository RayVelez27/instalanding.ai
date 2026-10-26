INSTALANDING.AI · Holographic Ticket Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Holographic Ticket Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/holographic-ticket-landing-page

murmur-swarm-tickets.html:
```html
<!DOCTYPE html>
<!--
  INSTALANDING.AI · Holographic Ticket Landing Page
  slug     holographic-ticket-landing-page
  prompt   https://instalanding.ai/p/holographic-ticket-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/holographic-ticket-landing-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of <style>: --black-color, --paper, --petal, --albedo, --rose,
            --line, --gold-grad (the one accent); ticket shape vars --stub/--stubw, --notch, --perf, --mask-v/--mask-h;
            Oswald 200-700 from Google Fonts
  sections  hero, marquee, lab, products, how-it-works, models, quote, cta, footer
  scripts   three.js r128 + OrbitControls 0.128 + GSAP 3.12.5 + ScrollTrigger (cdnjs / jsdelivr), then one inline
            script: sphere-swarm scene (fly-in timeline, breathing, raycast push, pairwise collisions, paused
            off-screen by IntersectionObserver); chrome fade-in after the intro; ticket tilt + sheen; marquee
            sheen tracking; .reveal / .parallax ScrollTriggers
  assets    none: tickets, orbs and barcodes are CSS gradients/masks/box-shadows, social marks are inline SVG

  ADAPTING
  - Ticket die-cuts are four mask layers composited with intersect (plus -webkit-mask-composite: source-in);
    switching to add returns a plain rectangle. Notches follow --stub, so change shape through the vars.
  - The float loop uses the translate property and the pointer tilt writes transform; do not merge them.
  - OrbitControls has zoom and pan off (else the wheel stops scrolling) and is disabled on coarse pointers;
    the push only applies while the pointer is inside the hero rect, since mousemove is on window.
  - The marquee band is wider than the viewport; html, body overflow-x: hidden is what keeps 390px clean.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Murmur Labs — Multi-Agent AI</title>
<meta name="description" content="A fictional multi-agent AI lab: a WebGL sphere cluster you can push around, holographic numerals, and die-cut ticket cards for products and models. One file, no image files, no icon font." />

<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@200..700&display=swap" rel="stylesheet" />

<style>

:root {
  --black-color: #101117;
  --white-color: #fff;
  --paper: #fbfaff;
  --blush: #f6e4e4;
  --petal: #f2c4c4;
  --albedo: #c7a5a5;
  --rose: #b76e79;
  --line: rgba(16, 17, 23, 0.12);
  --gold-grad: linear-gradient(135deg, #f7dccf 0%, #dca79c 45%, #b76e79 100%);
}

* { margin: 0px; padding: 0px; box-sizing: border-box; }
html { scroll-behavior: smooth; }
html, body { overflow-x: hidden; }

body {
  font-family: "Oswald", sans-serif;
  background: linear-gradient(to right, #fbfaff 0%, 40.00000059604645%, #fbfaff 80.0000011920929%, 90.00000059604645%, #ecf0fb 100%);
  color: var(--black-color);
  font-size: 16px;
  line-height: 1.3;
}

a { text-decoration: none; color: var(--black-color); }
ul, ol { list-style: none; }
.img-fluid { max-width: 100%; height: auto; }
h1 { font-size: 160px; }
h2 { font-size: 34px; }
button { outline: none; border: none; cursor: pointer; font-family: inherit; }

/* Icons are inline SVG rather than an icon webfont: this repo inlines its
   assets, and pulling ~100kB of icon CSS plus a woff2 for four brand marks
   is the one hotlink the rest of the page does not need. */
.ico { width: 16px; height: 16px; display: block; }
.footer-social .ico { width: 18px; height: 18px; }

.accent {
  background: var(--gold-grad);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

/* ---------- Hero ---------- */
.hero { position: relative; min-height: 100dvh; overflow: hidden; }
.hero canvas { position: absolute; top: 0; left: 0; z-index: 1; }
.hero-content { position: relative; z-index: 2; pointer-events: none; }
.hero-content a, .hero-content button { pointer-events: auto; }


.main-txt {
  position: absolute; top: 50%; left: 50%;
  transform: translate(-50%, -50%); -webkit-transform: translate(-50%, -50%);
  width: fit-content; text-transform: uppercase; letter-spacing: -4px;
  z-index: 0; transition: opacity 0.5s ease-in-out;
}
.hide-text { opacity: 0; transition: opacity 0.5s ease-in-out; }

.header-inner {
  display: flex; display: -webkit-flex; justify-content: space-between;
  align-items: center; padding: 16px 20px;
}
.header-inner .navbar-brand { font-size: 42px; font-weight: 900; letter-spacing: -1px; text-transform: uppercase; }
.header-inner nav ul { display: flex; display: -webkit-flex; gap: 120px; align-items: center; -webkit-align-items: center; }
.header-inner nav ul a { font-weight: 500; position: relative; text-transform: uppercase; }
.header-inner nav ul a::after {
  content: ""; position: absolute; bottom: -5px; left: 0; width: 0; height: 2px;
  background: var(--black-color); transition: all 0.5s; -webkit-transition: all 0.5s;
}
.header-inner nav ul a:hover::after { width: 100%; }

.rotated-text {
  position: absolute; top: 50%; right: 20px; z-index: 2; pointer-events: none;
  transform: translate(45%, -600%) rotate(90deg);
  text-transform: uppercase; font-size: 14px;
}

.banner-inner {
  padding: 100px 20px 30px; min-height: calc(100dvh - 90px); gap: 10px;
  display: flex; display: -webkit-flex; flex-direction: column; -webkit-flex-direction: column;
  justify-content: space-between; -webkit-justify-content: space-between; height: 100%;
}
.banner-inner .top-desc h5 { font-size: 16px; font-weight: 600; margin-bottom: 4px; }
.banner-inner .top-desc h6 { font-size: 14px; font-weight: 400; margin-bottom: 8px; }
.banner-inner .top-desc span { display: inline-block; width: 20px; height: 3px; background: var(--black-color); border-radius: 50px; }

.banner-inner .bottom-desc {
  display: flex; display: -webkit-flex; justify-content: space-between; -webkit-justify-content: space-between;
  align-items: flex-end; -webkit-align-items: flex-end;
}
.banner-inner .bottom-desc .left-desc h1 { margin-bottom: 20px; }
.banner-inner .bottom-desc .left-desc .desc-inner h5 { font-size: 16px; font-weight: 500; margin-bottom: 4px; }
.banner-inner .bottom-desc .left-desc .desc-inner h6 { font-size: 14px; font-weight: 400; margin-bottom: 0px; }
.banner-inner .bottom-desc .middle-desc h2 { text-transform: uppercase; letter-spacing: -2px; }
.banner-inner .bottom-desc .right-desc h1 { margin-bottom: 20px; padding-right: 60px; position: relative; text-align: right; }
.banner-inner .bottom-desc .right-desc h1::after {
  content: ""; position: absolute; top: 50%; right: 0; width: 20%; height: 6px;
  background: var(--black-color); transform: translate(-30%, 100%); -webkit-transform: translate(-30%, 100%);
}
.banner-inner .bottom-desc .right-desc .desc-inner { display: flex; display: -webkit-flex; gap: 30px; align-items: center; -webkit-align-items: center; }
.banner-inner .bottom-desc .right-desc .desc-inner span { text-transform: uppercase; }
.banner-inner .bottom-desc .right-desc .desc-inner ul { display: flex; display: -webkit-flex; gap: 10px; }
.banner-inner .bottom-desc .right-desc .desc-inner ul li a { display: block; }

/* Hero — holographic numerals */
.holo-num {
  background: linear-gradient(115deg, #b76e79 0%, #e0435a 16%, #f4a7c0 30%, #9b7fd1 45%, #7cc3dd 57%, #f7dccf 69%, #d39a8d 82%, #b76e79 100%);
  background-size: 300% 100%;
  -webkit-background-clip: text; background-clip: text;
  color: transparent;
  filter: drop-shadow(0 8px 18px rgba(183, 110, 121, 0.25));
  animation: holo-shift 7s ease-in-out infinite alternate;
}
@keyframes holo-shift { to { background-position: 100% 0; } }
.section-title .accent {
  display: inline-block;
  background: linear-gradient(115deg, #b76e79 0%, #e0435a 16%, #f4a7c0 30%, #9b7fd1 45%, #7cc3dd 57%, #f7dccf 69%, #d39a8d 82%, #b76e79 100%);
  background-size: 300% 100%;
  -webkit-background-clip: text; background-clip: text;
  color: transparent;
  filter: drop-shadow(0 8px 18px rgba(183, 110, 121, 0.22));
  animation: holo-shift 7s ease-in-out infinite alternate;
}
.banner-inner .bottom-desc .right-desc h1.holo-num::after {
  background: linear-gradient(90deg, #b76e79, #e0435a, #9b7fd1, #7cc3dd);
  border-radius: 6px;
}

/* Hero — mini admission ticket */
.ticket.wide.hero-ticket {
  --stubw: 92px;
  --notch: 8px;
  --perf: 4px;
  width: 300px;
  color: var(--black-color);
  filter: none;
}
.hero-ticket .ticket-bg { border-radius: 12px; }
.hero-ticket .ticket-main { padding: 16px 18px 16px 20px; }
.hero-ticket .tag {
  display: inline-block; font-size: 10px; text-transform: uppercase; letter-spacing: 0.5px;
  padding: 4px 9px; border-radius: 999px 0;
  background: rgba(16, 17, 23, 0.88); color: var(--paper);
}
.hero-ticket .ticket-main > p { margin-bottom: 0; max-width: none; }
.hero-ticket .ht-title { margin-top: 10px; font-size: 26px; line-height: 1; font-weight: 700; text-transform: uppercase; letter-spacing: -0.5px; }
.hero-ticket .ht-sub { margin-top: 5px; font-size: 11px; text-transform: uppercase; letter-spacing: 0.3px; font-weight: 400; }
.hero-ticket .ticket-tear-v { margin: calc(var(--notch) + 4px) 0; }
.hero-ticket .ticket-stub-v { padding: 16px 10px 14px 12px; gap: 8px; align-items: flex-start; }
.hero-ticket .ht-no { font-size: 11px; text-transform: uppercase; font-weight: 300; }
.hero-ticket .ht-no b { font-weight: 600; }
.hero-ticket .ticket-stub-v .barcode { transform: scaleX(0.84); transform-origin: left; }
.hero-ticket .barcode-wrap small { font-size: 9px; text-align: left; }

/* ---------- Marquee — holographic ticket strip ---------- */
.marquee { position: relative; padding: 46px 0; overflow: hidden; z-index: 3; }
.marquee-band {
  --perf: 7px;
  --mx: 50%;
  --my: 50%;
  position: relative;
  margin: 0 -6vw;
  padding: 30px 0;
  transform: rotate(-1.6deg);
}
.marquee-band .ticket-bg {
  border-radius: 0;
  -webkit-mask:
    radial-gradient(circle at 50% 0, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) top center / 22px 100% repeat-x,
    radial-gradient(circle at 50% 100%, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) bottom center / 22px 100% repeat-x;
  -webkit-mask-composite: source-in;
  mask:
    radial-gradient(circle at 50% 0, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) top center / 22px 100% repeat-x,
    radial-gradient(circle at 50% 100%, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) bottom center / 22px 100% repeat-x;
  mask-composite: intersect;
}
/* a slow light sweep across the strip */
.marquee-shine {
  position: absolute; inset: 0; z-index: 1; pointer-events: none; overflow: hidden;
  -webkit-mask: inherit;
}
.marquee-shine::before {
  content: ""; position: absolute; top: 0; bottom: 0; left: -30%; width: 30%;
  background: linear-gradient(100deg, transparent, rgba(255, 255, 255, 0.55) 45%, rgba(255, 220, 235, 0.35) 55%, transparent);
  mix-blend-mode: soft-light;
  animation: marquee-sweep 6s ease-in-out infinite;
}
@keyframes marquee-sweep { to { transform: translateX(460%); } }
/* dashed tear lines */
.marquee-band::before,
.marquee-band::after {
  content: ""; position: absolute; left: 0; right: 0; z-index: 1;
  border-top: 2px dashed rgba(16, 17, 23, 0.22);
}
.marquee-band::before { top: 16px; }
.marquee-band::after { bottom: 16px; }

.marquee-track {
  position: relative; z-index: 2;
  display: flex; width: max-content;
  animation: marquee 32s linear infinite;
}
.marquee:hover .marquee-track { animation-play-state: paused; }
.marquee-track span {
  display: flex; align-items: center; gap: 44px; padding-right: 44px;
  font-size: 56px; line-height: 1; text-transform: uppercase; letter-spacing: -1.5px; font-weight: 700; white-space: nowrap;
  color: rgba(16, 17, 23, 0.9);
}
.marquee-track span:nth-child(even) { color: transparent; -webkit-text-stroke: 1.5px var(--black-color); }
.marquee-track span::after {
  content: ""; flex: none; width: 30px; height: 30px; border-radius: 50%;
  background: radial-gradient(circle at 32% 28%, #fff6ef 0%, #f4d3c4 22%, #d8a092 58%, #9c5a63 100%);
  box-shadow: 0 10px 16px -8px rgba(156, 90, 99, 0.6);
}
.marquee-track span:nth-child(even)::after {
  width: 20px; height: 20px;
  background: radial-gradient(circle at 32% 28%, #fff1f1 0%, #ffb3b3 20%, #f26d6d 58%, #c23b4a 100%);
  box-shadow: 0 8px 14px -6px rgba(194, 59, 74, 0.6);
}
@keyframes marquee { to { transform: translateX(-50%); } }

/* ---------- Sections ---------- */
.section { padding: 140px 20px; position: relative; }
.section-head {
  display: flex; justify-content: space-between; align-items: flex-end; gap: 40px;
  border-bottom: 1px solid var(--line); padding-bottom: 24px; margin-bottom: 70px;
}
.section-num { display: flex; align-items: center; gap: 12px; font-size: 14px; font-weight: 500; text-transform: uppercase; white-space: nowrap; }
.section-num::before { content: ""; width: 20px; height: 3px; background: var(--black-color); border-radius: 50px; }
.section-title { font-size: 104px; line-height: 0.92; text-transform: uppercase; letter-spacing: -3px; font-weight: 600; }
.section-head p { max-width: 360px; font-weight: 300; font-size: 17px; }

/* About */
.about-grid { display: grid; grid-template-columns: 1.6fr 1fr; gap: 80px; align-items: end; }
.statement { font-size: 46px; line-height: 1.12; font-weight: 300; letter-spacing: -0.5px; }
.statement strong { font-weight: 600; }
.about-side p { font-weight: 300; font-size: 17px; margin-bottom: 40px; }
.stats { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; border-top: 1px solid var(--line); padding-top: 24px; }
.stats b { display: block; font-size: 52px; font-weight: 500; line-height: 1; letter-spacing: -1px; }
.stats span { font-size: 13px; text-transform: uppercase; }

/* Work — holographic tickets */
.work-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 40px 36px; perspective: 1200px; }
.card { display: block; }
.card:nth-child(3n + 2) { margin-top: 90px; }

.ticket {
  --stub: 96px;
  --perf: 6px;
  --notch: 13px;
  --mx: 50%;
  --my: 30%;
  position: relative;
  display: flex; flex-direction: column;
  padding: 24px 24px 0;
  translate: 0 0;
  animation: ticket-float 4.5s ease-in-out infinite;
  animation-delay: calc(var(--i, 0) * -0.75s);
  filter:
    drop-shadow(0 2px 2px rgba(120, 40, 60, 0.1))
    drop-shadow(0 10px 12px rgba(120, 40, 60, 0.12))
    drop-shadow(0 30px 40px rgba(120, 40, 60, 0.16));
  transform-style: preserve-3d;
  transition: transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
  will-change: transform, translate;
}
@keyframes ticket-float { 50% { translate: 0 -9px; } }

/* Holographic paper with perforated edges and side notches */
.ticket-bg {
  position: absolute; inset: 0; overflow: hidden; border-radius: 16px;
  background:
    linear-gradient(to bottom, var(--hl, rgba(255, 240, 245, 0.55)), 70%, var(--hd, rgba(183, 110, 121, 0.18))),
    conic-gradient(from 200deg at 62% 42%,
      var(--h1, #fbe3ea), var(--h2, #ffb8cf), var(--h3, #f7dccf), var(--h4, #eadaff), var(--h6, #fff4f0), var(--h5, #dca79c),
      var(--h2, #ffc9dc), var(--h7, #dcefff), var(--h3, #f7dccf), var(--h1, #f2c4c4));
  /* vertical ticket: perforated top/bottom, notches on the sides above the stub */
  --mask-v:
    radial-gradient(circle at 50% 0, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) top center / 20px 100% repeat-x,
    radial-gradient(circle at 50% 100%, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) bottom center / 20px 100% repeat-x,
    radial-gradient(circle at 0 calc(100% - var(--stub)), #0000 var(--notch), #000 calc(var(--notch) + 0.5px)),
    radial-gradient(circle at 100% calc(100% - var(--stub)), #0000 var(--notch), #000 calc(var(--notch) + 0.5px));
  /* horizontal ticket: perforated left/right, notches top/bottom beside the stub */
  --mask-h:
    radial-gradient(circle at 0 50%, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) left center / 100% 20px repeat-y,
    radial-gradient(circle at 100% 50%, #0000 var(--perf), #000 calc(var(--perf) + 0.5px)) right center / 100% 20px repeat-y,
    radial-gradient(circle at calc(100% - var(--stubw)) 0, #0000 var(--notch), #000 calc(var(--notch) + 0.5px)),
    radial-gradient(circle at calc(100% - var(--stubw)) 100%, #0000 var(--notch), #000 calc(var(--notch) + 0.5px));
  -webkit-mask: var(--mask-v);
  -webkit-mask-composite: source-in;
  mask: var(--mask-v);
  mask-composite: intersect;
}
/* iridescent rings */
.ticket-bg::before {
  content: ""; position: absolute; inset: -20%;
  background:
    radial-gradient(circle at 75% 15%, rgba(255, 90, 170, 0.35), transparent 45%),
    repeating-radial-gradient(circle at 25% 85%, #fff 0, #ffc2d8 40px, #f6ecff 90px, #fff 140px);
  mix-blend-mode: color-burn;
  opacity: 0.45;
  animation: holo-drift 9s ease-in-out infinite alternate;
}
@keyframes holo-drift { to { transform: translate(6%, -5%) rotate(8deg); } }
/* light sheen that follows the cursor */
.ticket-bg::after {
  content: ""; position: absolute; inset: 0;
  background: radial-gradient(circle at var(--mx) var(--my), rgba(255, 255, 255, 0.85), rgba(255, 214, 232, 0.35) 22%, transparent 55%);
  mix-blend-mode: soft-light;
  transition: background-position 0.3s;
}
.ticket-watermark {
  position: absolute; right: 14px; top: 26%;
  font-size: 190px; font-weight: 700; line-height: 0.8; letter-spacing: -8px;
  color: #fff; opacity: 0.5; mix-blend-mode: overlay; pointer-events: none;
}

.ticket > *:not(.ticket-bg) { position: relative; z-index: 1; }

.ticket-head { display: flex; justify-content: space-between; align-items: center; }
.ticket-head .tag {
  font-size: 12px; text-transform: uppercase; padding: 5px 12px; border-radius: 999px 0;
  background: rgba(16, 17, 23, 0.88); color: var(--paper); letter-spacing: 0.5px;
}
.ticket-head .num { font-size: 13px; font-weight: 300; text-transform: uppercase; }
.ticket-head .num b { font-weight: 600; }
.ticket-head .sym { margin-left: 8px; opacity: 0.45; }

.ticket-title {
  margin-top: 18px;
  font-size: 44px; line-height: 0.9; font-weight: 700; text-transform: uppercase; letter-spacing: -1.5px;
  color: rgba(16, 17, 23, 0.9);
}

.card-visual { position: relative; aspect-ratio: 4 / 3; margin: 4px -6px 10px; }
.card-visual .shadow {
  position: absolute; left: 15%; right: 15%; bottom: 4%; height: 10%;
  background: radial-gradient(ellipse at center, rgba(183, 110, 121, 0.35), transparent 70%);
}
.orb {
  position: absolute; width: var(--s); aspect-ratio: 1; left: var(--x); top: var(--y);
  border-radius: 50%;
  background: radial-gradient(circle at 32% 28%, #fff1f1 0%, #ffb3b3 20%, #f26d6d 58%, #c23b4a 100%);
  box-shadow: 0 30px 50px -22px rgba(194, 59, 74, 0.5);
  transition: transform 0.9s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.orb.gold {
  background: radial-gradient(circle at 32% 28%, #fff6ef 0%, #f4d3c4 22%, #d8a092 58%, #9c5a63 100%);
  box-shadow: 0 30px 50px -22px rgba(156, 90, 99, 0.5);
}
.orb.soft { border-radius: 52% 48% 44% 56% / 58% 56% 44% 42%; }
.card:hover .orb { transform: translate(var(--dx, 0), var(--dy, 0)) scale(1.04); }

.ticket-tear {
  height: 0; border-top: 2px dashed rgba(16, 17, 23, 0.25);
  margin: 0 calc(var(--notch) - 10px);
}
.ticket-stub {
  height: var(--stub);
  display: flex; justify-content: space-between; align-items: center; gap: 16px;
  padding-bottom: 4px;
}
.ticket-stub p { font-size: 15px; font-weight: 300; line-height: 1.2; }
.status {
  display: inline-flex; align-items: center; gap: 6px; margin-top: 6px;
  font-size: 12px; font-weight: 500; text-transform: uppercase;
}
.status::before { content: ""; width: 7px; height: 7px; border-radius: 50%; background: var(--rose); box-shadow: 0 0 0 3px rgba(183, 110, 121, 0.2); }
.status.ga::before { background: #d6405a; box-shadow: 0 0 0 3px rgba(214, 64, 90, 0.2); }
.barcode-wrap { flex: none; text-align: center; }
.barcode-wrap small { display: block; margin-top: 6px; font-size: 10px; letter-spacing: 1px; }
.barcode {
  position: relative; width: 76px; height: 30px;
}
.barcode::before {
  content: ""; position: absolute; left: 1px; top: 0; width: 0; height: 100%;
  box-shadow:
    0 0 0 1px #101117, 5px 0 0 1px #101117, 7px 0 0 1px #101117, 11px 0 0 1px #101117,
    15px 0 0 1px #101117, 16px 0 0 1px #101117, 22px 0 0 1px #101117, 27px 0 0 1px #101117,
    30px 0 0 1px #101117, 35px 0 0 1px #101117, 36px 0 0 1px #101117, 39px 0 0 1px #101117,
    43px 0 0 1px #101117, 47px 0 0 1px #101117, 50px 0 0 1px #101117, 55px 0 0 1px #101117,
    59px 0 0 1px #101117, 60px 0 0 1px #101117, 64px 0 0 1px #101117, 69px 0 0 1px #101117,
    70px 0 0 1px #101117, 74px 0 0 1px #101117;
}

/* Dark (Ink) ticket */
.ticket.dark { color: var(--paper); }
.ticket.dark .ticket-bg { --hl: rgba(255, 255, 255, 0.05); --hd: rgba(0, 0, 0, 0.35); }
.ticket.dark .ticket-bg::before { mix-blend-mode: screen; opacity: 0.12; }
.ticket.dark .ticket-title { color: var(--paper); }
.ticket.dark .ticket-head .tag { background: var(--paper); color: var(--black-color); }
.ticket.dark .ticket-tear { border-color: rgba(251, 250, 255, 0.3); }
.ticket.dark .barcode { filter: invert(1); }
.ticket.dark .ticket-watermark { opacity: 0.08; mix-blend-mode: normal; }
.orb.pearl { background: radial-gradient(circle at 32% 28%, #fff 0%, #fbf6ff 25%, #e6daf0 62%, #b9a6c6 100%); box-shadow: 0 30px 50px -22px rgba(120, 90, 140, 0.45); }
.orb.ink { background: radial-gradient(circle at 32% 28%, #fbe3ea 0%, #8a6a78 18%, #2b2533 55%, #0b0b10 100%); box-shadow: 0 30px 50px -22px rgba(0, 0, 0, 0.7); }

@media (prefers-reduced-motion: reduce) {
  .ticket, .ticket-bg::before, .marquee-shine::before, .holo-num, .section-title .accent { animation: none; }
}

/* Process */
.process-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 30px; }
.step { border-top: 1px solid var(--line); padding-top: 28px; position: relative; }
.step::before {
  content: ""; position: absolute; top: -1px; left: 0; height: 3px; width: 0;
  background: var(--gold-grad); transition: width 0.8s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.step:hover::before { width: 100%; }
.step-num { display: block; font-size: 80px; font-weight: 200; line-height: 1; margin-bottom: 36px; letter-spacing: -2px; }
.step h3 { font-size: 26px; text-transform: uppercase; letter-spacing: -0.5px; margin-bottom: 12px; }
.step p { font-weight: 300; font-size: 16px; }
.step ul { margin-top: 18px; display: flex; flex-wrap: wrap; gap: 6px; }
.step ul li { font-size: 12px; text-transform: uppercase; border: 1px solid var(--line); border-radius: 50px; padding: 4px 10px; }

/* Models — expandable holographic tickets */
.swatches { display: flex; gap: 14px; height: 560px; }
.swatch.ticket {
  --stub: 104px;
  flex: 1; min-width: 0;
  padding: 22px 20px 0;
  transition: flex 0.7s cubic-bezier(0.2, 0.8, 0.2, 1), transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.swatch.ticket:hover { flex: 2.4; }
.swatch .ticket-head { flex-wrap: wrap; gap: 6px; }
.swatch .ticket-title { font-size: 38px; margin-top: 16px; }
.model-detail {
  font-size: 15px; font-weight: 300; line-height: 1.3;
  max-height: 0; opacity: 0; overflow: hidden;
  transition: max-height 0.6s ease, opacity 0.4s ease, margin 0.6s ease;
}
.swatch:hover .model-detail { max-height: 120px; opacity: 1; margin-top: 10px; }
.model-visual { flex: 1; display: grid; place-items: center; min-height: 0; }
.model-visual .orb {
  position: relative; left: auto; top: auto; width: var(--os);
  transition: transform 0.9s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.swatch:hover .model-visual .orb { transform: scale(1.25); }
.swatch .ticket-stub { gap: 10px; }
.swatch .ticket-stub p { font-size: 14px; }
.swatch .barcode-wrap { width: 0; opacity: 0; overflow: hidden; transition: width 0.6s ease, opacity 0.4s ease; }
.swatch:hover .barcode-wrap { width: 76px; opacity: 1; }

/* Quote */
.quote { position: relative; text-align: center; padding: 180px 20px; overflow: hidden; }
.quote blockquote {
  position: relative; z-index: 1; max-width: 1200px; margin: 0 auto;
  font-size: 68px; line-height: 1.04; text-transform: uppercase; letter-spacing: -2px; font-weight: 500;
}
.quote cite { display: block; margin-top: 36px; font-style: normal; font-size: 14px; text-transform: uppercase; }

/* CTA — wide admission ticket */
.ticket.wide {
  --stubw: 320px;
  --notch: 16px;
  flex-direction: row; padding: 0;
}
.ticket.wide .ticket-bg { -webkit-mask: var(--mask-h); -webkit-mask-composite: source-in; mask: var(--mask-h); mask-composite: intersect; border-radius: 20px; }
.ticket.wide .ticket-watermark { top: auto; bottom: -10px; right: calc(var(--stubw) + 30px); font-size: 260px; }
.ticket-main { flex: 1; min-width: 0; padding: 44px 56px 48px; }
.ticket-main .ticket-head { justify-content: flex-start; gap: 16px; }
.cta-title {
  margin: 36px 0 28px;
  font-size: 132px; line-height: 0.88; text-transform: uppercase; letter-spacing: -4px; font-weight: 700;
  color: rgba(16, 17, 23, 0.92);
}
.cta-title .outline { color: transparent; -webkit-text-stroke: 2px var(--black-color); }
.ticket-main > p { max-width: 560px; font-weight: 300; font-size: 18px; margin-bottom: 32px; }
.cta-actions { display: flex; align-items: center; gap: 28px; flex-wrap: wrap; }
.btn {
  display: inline-flex; align-items: center; gap: 14px;
  background: var(--black-color); color: var(--paper);
  padding: 18px 34px; border-radius: 50px; text-transform: uppercase; font-weight: 500; letter-spacing: 0.5px;
  position: relative; overflow: hidden; isolation: isolate;
}
.btn::before {
  content: ""; position: absolute; inset: 0; z-index: -1;
  background: var(--gold-grad); transform: translateY(101%);
  transition: transform 0.5s cubic-bezier(0.2, 0.8, 0.2, 1);
}
.btn:hover::before { transform: none; }
.btn:hover { color: var(--black-color); }
.btn i { font-style: normal; font-size: 1.2em; line-height: 1; transition: transform 0.4s; }
.btn:hover i { transform: translateX(4px) rotate(-45deg); }
/* The header CTA, where the hamburger used to be: the page's own .btn -
   black pill, gold wipe rising on hover, arrow that kicks - shrunk to fit a
   64px bar, so the header and the closing CTA speak one language.
   It has to sit AFTER .btn, not up with the header styles: the two selectors
   tie on specificity and the later one wins, so declaring it earlier left
   .btn's 18px/34px padding in charge and the button came out 54px tall. */
.btn--nav { padding: 11px 22px; font-size: 14px; gap: 10px; }
.mail { display: block; font-size: 20px; text-transform: uppercase; letter-spacing: -0.3px; border-bottom: 1px solid rgba(16, 17, 23, 0.3); padding-bottom: 6px; width: fit-content; }

.ticket-tear-v { width: 0; border-left: 2px dashed rgba(16, 17, 23, 0.25); margin: calc(var(--notch) + 6px) 0; }
.ticket-stub-v {
  width: var(--stubw); flex: none;
  padding: 44px 36px 40px;
  display: flex; flex-direction: column; justify-content: space-between; gap: 20px;
}
.stub-orbs { position: relative; height: 150px; }
.stub-label { font-size: 13px; text-transform: uppercase; font-weight: 400; }
.stub-big { font-size: 34px; line-height: 0.95; text-transform: uppercase; font-weight: 700; letter-spacing: -1px; margin-top: 4px; }
.ticket-stub-v .barcode-wrap { text-align: left; }
.ticket-stub-v .barcode { transform: scaleX(1.6); transform-origin: left; }

/* Footer */
.footer { padding: 80px 20px 30px; border-top: 1px solid var(--line); overflow: hidden; }
.footer-top { display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 40px; }
.footer-top h5 { font-size: 13px; text-transform: uppercase; font-weight: 500; margin-bottom: 16px; display: flex; align-items: center; gap: 10px; }
.footer-top h5::before { content: ""; width: 14px; height: 2px; background: var(--black-color); border-radius: 50px; }
.footer-top p { font-weight: 300; max-width: 340px; }
.footer-top ul li { margin-bottom: 8px; }
.footer-top ul a { text-transform: uppercase; font-size: 15px; position: relative; }
.footer-top ul a::after { content: ""; position: absolute; bottom: -3px; left: 0; width: 0; height: 1px; background: var(--black-color); transition: width 0.4s; }
.footer-top ul a:hover::after { width: 100%; }
.footer-social { display: flex; gap: 10px; }
.footer-social a {
  width: 40px; height: 40px; border-radius: 50%; border: 1px solid var(--line);
  display: grid; place-items: center; transition: background 0.3s, border-color 0.3s;
}
.footer-social a:hover { background: var(--gold-grad); border-color: transparent; }
.footer-word {
  font-size: 19.5vw; line-height: 0.82; font-weight: 700; text-transform: uppercase;
  letter-spacing: -0.04em; margin: 70px 0 20px; white-space: nowrap; text-align: center;
}
/* The disclaimer, which is not fine print here: every product, model and
   number on this page is invented. */
.footer-legal {
  border-top: 1px solid var(--line);
  padding: 22px 0 18px;
  font-weight: 300; font-size: 14px; max-width: 760px;
}
.footer-bottom { display: flex; justify-content: space-between; font-size: 13px; text-transform: uppercase; }

/* ---------- Responsive ---------- */
@media (min-width: 1200px) and (max-width: 1499px) {
  h1 { font-size: 140px; }
  h2 { font-size: 28px; }
  .header-inner .navbar-brand { font-size: 38px; }
  .header-inner nav ul { gap: 100px; }
  .banner-inner { min-height: calc(100dvh - 85px); }
  .banner-inner .bottom-desc .right-desc h1 { padding-right: 40px; }
  .banner-inner .bottom-desc .right-desc h1::after { width: 16%; }
  .banner-inner .bottom-desc .right-desc .desc-inner { gap: 20px; }
  .section-title { font-size: 88px; }
  .cta-title { font-size: 108px; }
}

@media (max-width: 1199px) {
  .section-title { font-size: 72px; }
  .statement { font-size: 36px; }
  .about-grid { gap: 50px; }
  .process-grid { grid-template-columns: repeat(2, 1fr); row-gap: 50px; }
  .quote blockquote { font-size: 52px; }
  .cta-title { font-size: 92px; letter-spacing: -3px; }
  .ticket.wide { --stubw: 270px; }
  .ticket-main { padding: 40px 40px 44px; }
  .swatches { display: grid; grid-template-columns: repeat(3, 1fr); gap: 28px 20px; height: auto; }
  .swatch.ticket { min-height: 470px; }
  .swatch.ticket:hover { flex: 1; }
  .model-detail { max-height: 120px; opacity: 1; margin-top: 10px; }
  .model-visual { min-height: 150px; }
  .swatch .barcode-wrap { width: 76px; opacity: 1; }
  .footer-top { grid-template-columns: 1fr 1fr; }
}

@media (min-width: 992px) and (max-width: 1199px) {
  h1 { font-size: 100px; }
  h2 { font-size: 24px; }
  body { font-size: 14px; }
  .header-inner .navbar-brand { font-size: 32px; }
  .header-inner nav ul { gap: 40px; }
  .banner-inner { min-height: calc(100dvh - 76px); padding-top: 80px; }
  .banner-inner .bottom-desc .right-desc h1 { padding-right: 30px; }
  .banner-inner .bottom-desc .right-desc h1::after { width: 12%; }
  .banner-inner .bottom-desc .right-desc .desc-inner { gap: 16px; }
}

@media (max-width: 991px) {
  .about-grid, .cta-inner { grid-template-columns: 1fr; }
  .work-grid { grid-template-columns: repeat(2, 1fr); }
  .card:nth-child(3n + 2) { margin-top: 0; }
  .card:nth-child(2n) { margin-top: 60px; }
  .work-grid { gap: 40px 28px; }
  .section-head { flex-direction: column; align-items: flex-start; gap: 20px; }
  .swatches { grid-template-columns: repeat(2, 1fr); }
}

@media (min-width: 768px) and (max-width: 991px) {
  h1 { font-size: 80px; }
  h2 { font-size: 20px; }
  body { font-size: 14px; }
  .header-inner .navbar-brand { font-size: 28px; }
  .header-inner nav ul { gap: 20px; }
  .banner-inner { min-height: calc(100dvh - 70px); padding-top: 60px; }
  .banner-inner .bottom-desc .right-desc h1 { padding-right: 30px; }
  .banner-inner .bottom-desc .right-desc h1::after { width: 10%; }
  .banner-inner .bottom-desc .right-desc .desc-inner { gap: 12px; }
}

@media (max-width: 767px) {
  h1 { font-size: 30px; }
  h2 { font-size: 16px; }
  body { font-size: 12px; }
  .main-txt { font-size: 60px; }
  .header-inner .navbar-brand { font-size: 22px; }
  .header-inner nav ul { gap: 16px; display: none; }
  .rotated-text { font-size: 12px; }
  .banner-inner { min-height: calc(100dvh - 60px); padding-top: 40px; }
  .banner-inner .bottom-desc .left-desc h1 { margin-bottom: 14px; }
  .banner-inner .bottom-desc .middle-desc { display: none; }
  .banner-inner .bottom-desc .right-desc h1 { padding-right: 22px; }
  .banner-inner .bottom-desc .right-desc h1::after { width: 10%; }
  .banner-inner .bottom-desc .right-desc .desc-inner { gap: 12px; }
  .banner-inner .bottom-desc .right-desc .desc-inner ul { gap: 8px; }

  .section { padding: 90px 16px; }
  .section-head { margin-bottom: 44px; }
  .section-title { font-size: 48px; letter-spacing: -1.5px; }
  .section-head p, .about-side p { font-size: 15px; }
  .statement { font-size: 26px; }
  .stats b { font-size: 36px; }
  .stats span { font-size: 11px; }
  .marquee { padding: 30px 0; }
  .marquee-band { padding: 24px 0; --perf: 5px; }
  .marquee-band::before { top: 12px; }
  .marquee-band::after { bottom: 12px; }
  .marquee-track span { font-size: 32px; gap: 24px; padding-right: 24px; }
  .marquee-track span::after { width: 18px; height: 18px; }
  .marquee-track span:nth-child(even)::after { width: 13px; height: 13px; }
  .work-grid { grid-template-columns: 1fr; gap: 40px; }
  .card:nth-child(2n) { margin-top: 0; }
  .ticket-title { font-size: 36px; }
  .ticket-watermark { font-size: 150px; }
  .process-grid { grid-template-columns: 1fr; }
  .step-num { font-size: 56px; margin-bottom: 20px; }
  .swatches { grid-template-columns: 1fr; }
  .swatch.ticket { min-height: 420px; }
  .ticket.wide { flex-direction: column; --stub: 300px; --notch: 13px; }
  .ticket.wide .ticket-bg { -webkit-mask: var(--mask-v); -webkit-mask-composite: source-in; mask: var(--mask-v); mask-composite: intersect; }
  .ticket.wide .ticket-watermark { right: 16px; bottom: auto; top: 30%; font-size: 150px; }
  .ticket-main { padding: 34px 24px 32px; }
  .ticket-main > p { font-size: 15px; }
  .ticket-tear-v { width: auto; height: 0; border-left: 0; border-top: 2px dashed rgba(16, 17, 23, 0.25); margin: 0 4px; }
  .ticket-stub-v { width: auto; height: var(--stub); padding: 24px 24px 26px; gap: 10px; }
  .stub-orbs { height: 90px; }
  .stub-big { font-size: 26px; }
  .mail { font-size: 16px; }
  .ticket.wide.hero-ticket { flex-direction: row; width: 214px; --stubw: 70px; --notch: 7px; }
  .hero-ticket .ticket-bg { -webkit-mask: var(--mask-h); -webkit-mask-composite: source-in; mask: var(--mask-h); mask-composite: intersect; }
  .hero-ticket .ticket-main { padding: 12px 10px 12px 14px; }
  .hero-ticket .ht-title { font-size: 18px; margin-top: 7px; }
  .hero-ticket .ht-sub { font-size: 9px; }
  .hero-ticket .ticket-tear-v { width: 0; height: auto; border-top: 0; border-left: 2px dashed rgba(16, 17, 23, 0.25); margin: calc(var(--notch) + 3px) 0; }
  .hero-ticket .ticket-stub-v { width: var(--stubw); height: auto; padding: 12px 6px 10px 8px; }
  .hero-ticket .ticket-stub-v .barcode { transform: scaleX(0.7); }
  .quote { padding: 110px 16px; }
  .quote blockquote { font-size: 32px; letter-spacing: -1px; }
  .cta-title { font-size: 64px; letter-spacing: -2px; }
  .btn { padding: 15px 26px; }
  .mail { font-size: 17px; }
  .footer { padding: 60px 16px 24px; }
  .footer-top { grid-template-columns: 1fr; }
  .footer-legal { font-size: 13px; }
  .footer-bottom { flex-direction: column; gap: 6px; }
  .btn--nav { padding: 9px 16px; font-size: 12px; gap: 7px; }
}
</style>
</head>
<body>

  <!-- ===== Hero ===== -->
  <section class="hero" id="top" data-section="hero">
    <h1 class="main-txt">Murmur</h1>
    <canvas class="webgl" id="webgl" aria-hidden="true"></canvas>

    <div class="hero-content">
      <header class="hide-text">
        <div class="header-inner">
          <a href="#top" class="navbar-brand">Murmur</a>
          <nav>
            <ul>
              <li><a href="#studio">lab</a></li>
              <li><a href="#work">products</a></li>
              <li><a href="#process">platform</a></li>
              <li><a href="#materials">models</a></li>
            </ul>
          </nav>
          <a href="#contact" class="btn btn--nav">Early access <i class="arrow" aria-hidden="true">→</i></a>
        </div>
      </header>

      <div class="banner hide-text">
        <div class="banner-inner">
          <div class="top-desc">
            <h5>Multi-Agent Systems</h5>
            <h6>Applied AI Research Lab</h6>
            <span></span>
          </div>
          <div class="bottom-desc">
            <div class="left-desc">
              <h1 class="holo-num" aria-hidden="true">X</h1>
              <a href="#contact" class="ticket wide hero-ticket" data-tilt="0.8" aria-label="Swarm v1.0 research preview, request early access">
                <div class="ticket-bg"></div>
                <div class="ticket-main">
                  <span class="tag">Research Preview</span>
                  <p class="ht-title">Swarm v1.0</p>
                  <p class="ht-sub">Admit one · Early access</p>
                </div>
                <div class="ticket-tear-v"></div>
                <div class="ticket-stub-v">
                  <span class="ht-no">No. <b>001</b></span>
                  <div class="barcode-wrap"><div class="barcode"></div><small>ML-001</small></div>
                </div>
              </a>
            </div>
            <div class="middle-desc">
              <h2>Agents That Collide</h2>
            </div>
            <div class="right-desc">
              <h1 class="holo-num" aria-hidden="true">01</h1>
              <div class="desc-inner">
                <span>Social Links</span>
                <ul>
                  <li><a href="#" aria-label="X"><svg class="ico" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M3 3h4.9l4.3 5.7L17.4 3H21l-6.9 7.9L21.4 21h-4.9l-4.6-6.1L6.3 21H2.7l7.3-8.4z"/></svg></a></li>
                  <li><a href="#" aria-label="Facebook"><svg class="ico" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M14.6 21v-8h2.7l.4-3.1h-3.1V7.9c0-.9.25-1.5 1.55-1.5h1.65V3.6c-.3 0-1.3-.1-2.45-.1-2.4 0-4.05 1.45-4.05 4.1v2.3H8.6V13h2.7v8z"/></svg></a></li>
                  <li><a href="#" aria-label="Instagram"><svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.2" cy="6.8" r="1.15" fill="currentColor" stroke="none"/></svg></a></li>
                  <li><a href="#" aria-label="YouTube"><svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true"><rect x="2" y="5.5" width="20" height="13" rx="4"/><path d="M10.2 9.4l5 2.6-5 2.6z" fill="currentColor" stroke="none"/></svg></a></li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <span class="rotated-text hide-text">Hover to perturb the swarm</span>
  </section>

  <!-- ===== Marquee ===== -->
  <div class="marquee" aria-hidden="true" data-section="marquee">
    <div class="marquee-band">
      <div class="ticket-bg"></div>
      <div class="marquee-shine"></div>
      <div class="marquee-track">
        <span>Agents</span><span>Reasoning</span><span>Orchestration</span><span>Memory</span><span>Evals</span><span>Alignment</span>
        <span>Agents</span><span>Reasoning</span><span>Orchestration</span><span>Memory</span><span>Evals</span><span>Alignment</span>
      </div>
    </div>
  </div>

  <!-- ===== 02 Studio ===== -->
  <section class="section" id="studio" data-section="lab">
    <div class="section-head reveal">
      <h2 class="section-title">The<br><span class="accent">Lab</span></h2>
      <span class="section-num">02 — Lab</span>
    </div>
    <div class="about-grid">
      <p class="statement reveal">
        Murmur Labs is an <strong>applied AI research lab</strong>. We believe intelligence isn't one giant model — it's
        <span class="accent"><strong>hundreds of specialised agents colliding</strong></span>, challenging each other and settling on answers you can trust.
      </p>
      <div class="about-side reveal">
        <p>Every sphere above is an agent. Swarm, our platform, lets teams spin up, coordinate and evaluate agent collectives in production — with the rigour of a research lab and the reliability of infrastructure.</p>
        <div class="stats">
          <div><b>100+</b><span>Agents per run</span></div>
          <div><b>40ms</b><span>Median routing latency</span></div>
          <div><b>12</b><span>Papers published</span></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== 03 Studies ===== -->
  <section class="section" id="work" data-section="products">
    <div class="section-head reveal">
      <h2 class="section-title">The Swarm<br><span class="accent">Platform</span></h2>
      <p>Six products, one idea: many small models working together beat one big model working alone.</p>
    </div>

    <div class="work-grid">
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:0">
          <div class="ticket-bg"><span class="ticket-watermark">01</span></div>
          <div class="ticket-head">
            <span class="tag">Platform</span>
            <span class="num">No. <b>01</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Swarm<br>Orchestrator</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb" style="--s:46%;--x:27%;--y:32%;--dx:6px;--dy:-4px"></div>
            <div class="orb" style="--s:22%;--x:10%;--y:18%;--dx:-12px;--dy:-10px"></div>
            <div class="orb" style="--s:18%;--x:70%;--y:20%;--dx:12px;--dy:-12px"></div>
            <div class="orb" style="--s:28%;--x:62%;--y:56%;--dx:14px;--dy:8px"></div>
            <div class="orb" style="--s:12%;--x:18%;--y:68%;--dx:-10px;--dy:10px"></div>
            <div class="orb" style="--s:9%;--x:48%;--y:15%;--dx:0;--dy:-16px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Coordinate 100+ agents on one goal</p>
              <span class="status ga">Generally available</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-01-2026</small></div>
          </div>
        </div>
      </a>
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:1">
          <div class="ticket-bg"><span class="ticket-watermark">02</span></div>
          <div class="ticket-head">
            <span class="tag">Research</span>
            <span class="num">No. <b>02</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Adaptive<br>Memory</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb soft" style="--s:62%;--x:19%;--y:28%;--dx:0;--dy:10px"></div>
            <div class="orb gold" style="--s:15%;--x:70%;--y:66%;--dx:10px;--dy:-6px"></div>
            <div class="orb" style="--s:9%;--x:14%;--y:20%;--dx:-6px;--dy:-8px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Context that reshapes itself</p>
              <span class="status ">Public beta</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-02-2026</small></div>
          </div>
        </div>
      </a>
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:2">
          <div class="ticket-bg"><span class="ticket-watermark">03</span></div>
          <div class="ticket-head">
            <span class="tag">Tooling</span>
            <span class="num">No. <b>03</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Eval<br>Studio</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb gold" style="--s:40%;--x:30%;--y:34%;--dx:0;--dy:-6px"></div>
            <div class="orb gold" style="--s:24%;--x:12%;--y:56%;--dx:-10px;--dy:6px"></div>
            <div class="orb gold" style="--s:20%;--x:66%;--y:24%;--dx:10px;--dy:-10px"></div>
            <div class="orb" style="--s:14%;--x:68%;--y:62%;--dx:10px;--dy:8px"></div>
            <div class="orb gold" style="--s:10%;--x:22%;--y:22%;--dx:-8px;--dy:-8px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Benchmark every agent, every run</p>
              <span class="status ga">Generally available</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-03-2026</small></div>
          </div>
        </div>
      </a>
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:3">
          <div class="ticket-bg"><span class="ticket-watermark">04</span></div>
          <div class="ticket-head">
            <span class="tag">Data</span>
            <span class="num">No. <b>04</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Synthetic<br>Bloom</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb" style="--s:12%;--x:44%;--y:40%;--dx:0;--dy:0"></div>
            <div class="orb" style="--s:9%;--x:30%;--y:30%;--dx:-10px;--dy:-10px"></div>
            <div class="orb gold" style="--s:10%;--x:58%;--y:28%;--dx:10px;--dy:-10px"></div>
            <div class="orb" style="--s:8%;--x:62%;--y:48%;--dx:14px;--dy:2px"></div>
            <div class="orb gold" style="--s:9%;--x:28%;--y:52%;--dx:-14px;--dy:4px"></div>
            <div class="orb" style="--s:7%;--x:46%;--y:60%;--dx:0;--dy:14px"></div>
            <div class="orb" style="--s:6%;--x:18%;--y:40%;--dx:-18px;--dy:0"></div>
            <div class="orb gold" style="--s:6%;--x:74%;--y:38%;--dx:18px;--dy:-2px"></div>
            <div class="orb" style="--s:5%;--x:40%;--y:20%;--dx:-4px;--dy:-18px"></div>
            <div class="orb" style="--s:5%;--x:60%;--y:66%;--dx:10px;--dy:16px"></div>
            <div class="orb gold" style="--s:4%;--x:24%;--y:66%;--dx:-12px;--dy:14px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Grounded synthetic training data</p>
              <span class="status ">Public beta</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-04-2026</small></div>
          </div>
        </div>
      </a>
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:4">
          <div class="ticket-bg"><span class="ticket-watermark">05</span></div>
          <div class="ticket-head">
            <span class="tag">Infra</span>
            <span class="num">No. <b>05</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Gravity<br>Router</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb" style="--s:38%;--x:8%;--y:48%;--dx:8px;--dy:0"></div>
            <div class="orb gold" style="--s:26%;--x:42%;--y:38%;--dx:12px;--dy:-4px"></div>
            <div class="orb" style="--s:17%;--x:66%;--y:30%;--dx:14px;--dy:-8px"></div>
            <div class="orb gold" style="--s:10%;--x:80%;--y:22%;--dx:14px;--dy:-10px"></div>
            <div class="orb" style="--s:6%;--x:88%;--y:14%;--dx:10px;--dy:-10px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Send each task to the right model</p>
              <span class="status ga">Generally available</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-05-2026</small></div>
          </div>
        </div>
      </a>
      <a href="#" class="card reveal">
        <div class="ticket" style="--i:5">
          <div class="ticket-bg"><span class="ticket-watermark">06</span></div>
          <div class="ticket-head">
            <span class="tag">Safety</span>
            <span class="num">No. <b>06</b><span class="sym">✦</span></span>
          </div>
          <h3 class="ticket-title">Consensus<br>Layer</h3>
          <div class="card-visual">
            <div class="shadow"></div>
            <div class="orb" style="--s:42%;--x:12%;--y:32%;--dx:-14px;--dy:0"></div>
            <div class="orb gold" style="--s:42%;--x:48%;--y:36%;--dx:14px;--dy:0"></div>
            <div class="orb" style="--s:8%;--x:46%;--y:22%;--dx:0;--dy:-20px"></div>
            <div class="orb gold" style="--s:6%;--x:44%;--y:74%;--dx:0;--dy:18px"></div>
          </div>
          <div class="ticket-tear"></div>
          <div class="ticket-stub">
            <div>
              <p>Agents cross-check before they act</p>
              <span class="status ">Research preview</span>
            </div>
            <div class="barcode-wrap"><div class="barcode"></div><small>ML-06-2026</small></div>
          </div>
        </div>
      </a>
    </div>
  </section>

  <!-- ===== 04 Process ===== -->
  <section class="section" id="process" data-section="how-it-works">
    <div class="section-head reveal">
      <h2 class="section-title">How Swarm<br><span class="accent">Works</span></h2>
      <span class="section-num">04 — Platform</span>
    </div>
    <div class="process-grid">
      <div class="step reveal">
        <span class="step-num">01</span>
        <h3>Connect</h3>
        <p>Plug in your data, tools and existing models through one API. Swarm maps what each agent is allowed to touch.</p>
        <ul><li>API</li><li>Connectors</li></ul>
      </div>
      <div class="step reveal">
        <span class="step-num">02</span>
        <h3>Orchestrate</h3>
        <p>Describe the goal. Swarm spawns specialist agents, routes sub-tasks and lets them debate until the answer settles.</p>
        <ul><li>Routing</li><li>Debate</li></ul>
      </div>
      <div class="step reveal">
        <span class="step-num">03</span>
        <h3>Evaluate</h3>
        <p>Every run is scored for accuracy, cost and safety, so regressions surface before your users ever see them.</p>
        <ul><li>Evals</li><li>Tracing</li></ul>
      </div>
      <div class="step reveal">
        <span class="step-num">04</span>
        <h3>Deploy</h3>
        <p>Ship to our cloud or your own VPC with audit logs, SSO and per-agent permissions built in.</p>
        <ul><li>VPC</li><li>SOC 2</li></ul>
      </div>
    </div>
  </section>

  <!-- ===== 05 Materials ===== -->
  <section class="section" id="materials" data-section="models">
    <div class="section-head reveal">
      <h2 class="section-title">The Model<br><span class="accent">Family</span></h2>
      <p>Six in-house models, each tuned for a role in the swarm. Hover one to open it up.</p>
    </div>
    <div class="swatches reveal">
      <div class="swatch ticket" style="--i:0;--os:42px;--h1:#ffffff;--h2:#f4eefc;--h3:#fff6f2;--h4:#e8e2ff;--h5:#e9dde6;--h7:#e6f4ff">
        <div class="ticket-bg"><span class="ticket-watermark">01</span></div>
        <div class="ticket-head">
          <span class="tag">Edge</span>
          <span class="num">No. <b>01</b></span>
        </div>
        <h4 class="ticket-title">Mote</h4>
        <p class="model-detail">Runs on laptops and phones. Filters and routes work before it ever reaches a bigger model.</p>
        <div class="model-visual"><div class="orb pearl"></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>1B · On-device</p>
            <span class="status">Classification &amp; triage</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M01</small></div>
        </div>
      </div>
      <div class="swatch ticket" style="--i:1;--os:62px;--h1:#fde3ea;--h2:#ffbdd2;--h3:#f9d6d6;--h4:#f2dcff;--h5:#f2c4c4">
        <div class="ticket-bg"><span class="ticket-watermark">02</span></div>
        <div class="ticket-head">
          <span class="tag">Fast</span>
          <span class="num">No. <b>02</b></span>
        </div>
        <h4 class="ticket-title">Petal</h4>
        <p class="model-detail">First drafts, summaries and tool calls at a fraction of the cost of larger models.</p>
        <div class="model-visual"><div class="orb "></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>8B · 128K context</p>
            <span class="status">Fast drafting agents</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M02</small></div>
        </div>
      </div>
      <div class="swatch ticket" style="--i:2;--os:84px;--h1:#f1dede;--h2:#e3b7bd;--h3:#efd9d2;--h4:#e2d3ee;--h5:#c7a5a5;--h6:#f7ecec">
        <div class="ticket-bg"><span class="ticket-watermark">03</span></div>
        <div class="ticket-head">
          <span class="tag">Core</span>
          <span class="num">No. <b>03</b></span>
        </div>
        <h4 class="ticket-title">Core</h4>
        <p class="model-detail">The default agent in most swarms, balancing speed, cost and quality.</p>
        <div class="model-visual"><div class="orb "></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>70B · 256K context</p>
            <span class="status">General-purpose workhorse</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M03</small></div>
        </div>
      </div>
      <div class="swatch ticket" style="--i:3;--os:118px;--h1:#f7dccf;--h2:#e9b3a4;--h3:#fbe8dc;--h4:#f1d0d8;--h5:#b76e79;--h6:#fff1e8;--h7:#f6e2c9">
        <div class="ticket-bg"><span class="ticket-watermark">04</span></div>
        <div class="ticket-head">
          <span class="tag">Flagship</span>
          <span class="num">No. <b>04</b></span>
        </div>
        <h4 class="ticket-title">Aurum</h4>
        <p class="model-detail">Plans the run, breaks goals into tasks and arbitrates when agents disagree.</p>
        <div class="model-visual"><div class="orb gold"></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>Flagship · 1M context</p>
            <span class="status">Deep reasoning &amp; planning</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M04</small></div>
        </div>
      </div>
      <div class="swatch ticket" style="--i:4;--os:70px;--h1:#ffc2cf;--h2:#ff8fa8;--h3:#ffd1d9;--h4:#ffb3e6;--h5:#e0435a;--h6:#ffe4ea;--h7:#ffd7e9">
        <div class="ticket-bg"><span class="ticket-watermark">05</span></div>
        <div class="ticket-head">
          <span class="tag">Realtime</span>
          <span class="num">No. <b>05</b></span>
        </div>
        <h4 class="ticket-title">Pulse</h4>
        <p class="model-detail">Low-latency speech in and out, for agents that talk directly to people.</p>
        <div class="model-visual"><div class="orb "></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>Realtime · &lt;200ms</p>
            <span class="status">Voice &amp; streaming</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M05</small></div>
        </div>
      </div>
      <div class="swatch ticket dark" style="--i:5;--os:76px;--h1:#17171f;--h2:#3a2431;--h3:#1f1f2a;--h4:#2c2440;--h5:#5a3a46;--h6:#241c26;--h7:#1c2433">
        <div class="ticket-bg"><span class="ticket-watermark">06</span></div>
        <div class="ticket-head">
          <span class="tag">Embeddings</span>
          <span class="num">No. <b>06</b></span>
        </div>
        <h4 class="ticket-title">Ink</h4>
        <p class="model-detail">Powers Adaptive Memory and retrieval across every agent in the swarm.</p>
        <div class="model-visual"><div class="orb ink"></div></div>
        <div class="ticket-tear"></div>
        <div class="ticket-stub">
          <div>
            <p>Embeddings · 3072-d</p>
            <span class="status">Search &amp; memory</span>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-M06</small></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== Quote ===== -->
  <section class="quote" aria-label="Quote" data-section="quote">
    <blockquote class="reveal">
      “Intelligence isn't one big model. It's <span class="accent">many small ones colliding</span> until the right answer settles.”
      <cite>— Murmur Labs Research Notes</cite>
    </blockquote>
  </section>

  <!-- ===== 06 Contact ===== -->
  <section class="section" id="contact" data-section="cta">
    <div class="section-head reveal">
      <span class="section-num">06 — Early Access</span>
      <span class="section-num">Research preview open</span>
    </div>
    <div class="cta-wrap reveal">
      <div class="ticket wide" data-tilt="0.3">
        <div class="ticket-bg"><span class="ticket-watermark">EA</span></div>
        <div class="ticket-main">
          <div class="ticket-head">
            <span class="tag">Early Access</span>
            <span class="num">No. <b>001</b><span class="sym">✦</span></span>
          </div>
          <h2 class="cta-title">Let your<br>agents <span class="outline">collide</span></h2>
          <p>Swarm is onboarding a small group of research and product teams each month. Tell us what you're building and we'll get you set up with credits and a lab engineer.</p>
          <div class="cta-actions">
            <a href="#" class="btn">Request early access <i class="arrow" aria-hidden="true">→</i></a>
            <a href="#" class="mail">hello@murmurlabs.ai</a>
          </div>
        </div>
        <div class="ticket-tear-v"></div>
        <div class="ticket-stub-v">
          <div class="ticket-head">
            <span class="num">Admit <b>One</b></span>
            <span class="sym">✦</span>
          </div>
          <div class="stub-orbs">
            <div class="orb gold" style="--s:92px;--x:8%;--y:18%"></div>
            <div class="orb" style="--s:54px;--x:52%;--y:4%"></div>
            <div class="orb pearl" style="--s:34px;--x:62%;--y:58%"></div>
          </div>
          <div>
            <p class="stub-label">Swarm v1.0</p>
            <p class="stub-big">Research<br>Preview</p>
          </div>
          <div class="barcode-wrap"><div class="barcode"></div><small>ML-EA-2026</small></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== Footer ===== -->
  <footer class="footer" data-section="footer">
    <div class="footer-top">
      <div>
        <h5>Murmur Labs</h5>
        <p>An applied AI research lab building multi-agent systems that are fast, measurable and safe to deploy.</p>
      </div>
      <div>
        <h5>Explore</h5>
        <ul>
          <li><a href="#studio">Lab</a></li>
          <li><a href="#work">Products</a></li>
          <li><a href="#process">Platform</a></li>
          <li><a href="#materials">Models</a></li>
        </ul>
      </div>
      <div>
        <h5>Developers</h5>
        <ul>
          <li><a href="#">Docs</a></li>
          <li><a href="#">API Status</a></li>
          <li><a href="#">Changelog</a></li>
        </ul>
      </div>
      <div>
        <h5>Social</h5>
        <div class="footer-social">
          <a href="#" aria-label="X"><svg class="ico" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M3 3h4.9l4.3 5.7L17.4 3H21l-6.9 7.9L21.4 21h-4.9l-4.6-6.1L6.3 21H2.7l7.3-8.4z"/></svg></a>
          <a href="#" aria-label="Facebook"><svg class="ico" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M14.6 21v-8h2.7l.4-3.1h-3.1V7.9c0-.9.25-1.5 1.55-1.5h1.65V3.6c-.3 0-1.3-.1-2.45-.1-2.4 0-4.05 1.45-4.05 4.1v2.3H8.6V13h2.7v8z"/></svg></a>
          <a href="#" aria-label="Instagram"><svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.2" cy="6.8" r="1.15" fill="currentColor" stroke="none"/></svg></a>
          <a href="#" aria-label="YouTube"><svg class="ico" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true"><rect x="2" y="5.5" width="20" height="13" rx="4"/><path d="M10.2 9.4l5 2.6-5 2.6z" fill="currentColor" stroke="none"/></svg></a>
        </div>
      </div>
    </div>
    <div class="footer-word accent">Murmur</div>
    <p class="footer-legal">
      Murmur Labs is a fictional company and this page is a design demo. The lab, the Swarm platform, the six products,
      the model family and every figure quoted here are invented. Nothing here is real, and nothing on this page can be
      bought, signed up for or relied on.
    </p>
    <div class="footer-bottom">
      <span>© 2026 Murmur Labs</span>
      <span>Swarm v1.0 — Research Preview</span>
      <a href="#top">Back to top ↑</a>
    </div>
  </footer>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.5/ScrollTrigger.min.js"></script>
<script>
const hero = document.querySelector(".hero");

// Scene setup
const scene = new THREE.Scene();
const camera = new THREE.PerspectiveCamera(25, hero.clientWidth / hero.clientHeight, 0.1, 1000);
camera.position.z = 24;

const renderer = new THREE.WebGLRenderer({
  canvas: document.querySelector("#webgl"),
  antialias: true,
  alpha: true
});
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;

// Orbit Controls (rotate only, so the page can still scroll)
const controls = new THREE.OrbitControls(camera, renderer.domElement);
controls.enableDamping = true;
controls.dampingFactor = 0.05;
controls.enableZoom = false;
controls.enablePan = false;
if (window.matchMedia("(pointer: coarse)").matches) {
  controls.enabled = false;
  renderer.domElement.style.touchAction = "pan-y";
}

function sizeScene() {
  const w = hero.clientWidth;
  const h = hero.clientHeight;
  camera.aspect = w / h;
  camera.updateProjectionMatrix();
  // Pull the camera back on narrow screens so the cluster fits
  camera.position.setLength(Math.max(24, 28 / camera.aspect));
  renderer.setSize(w, h);
}
sizeScene();

const radii = [
  1, 0.6, 0.8, 0.4, 0.9, 0.7, 0.9, 0.3, 0.2, 0.5, 0.6, 0.4, 0.5, 0.6, 0.7, 0.3, 0.4, 0.8, 0.7, 0.5, 0.4, 0.6, 0.35, 0.38, 0.9,

  0.3, 0.6, 0.4, 0.2, 0.35, 0.5, 0.15, 0.2, 0.25, 0.4, 0.8, 0.76, 0.8, 1, 0.8, 0.7, 0.8, 0.3, 0.5, 0.6, 0.55, 0.42, 0.75, 0.66,
  0.6, 0.7, 0.5, 0.6, 0.35, 0.35, 0.35, 0.8, 0.6, 0.7, 0.8, 0.4, 0.89, 0.3,

  0.3, 0.6, 0.4, 0.2, 0.52, 0.5, 0.15, 0.2, 0.25, 0.4, 0.8, 0.76, 0.8, 1, 0.8, 0.7, 0.8, 0.3, 0.5, 0.6, 0.8, 0.7, 0.75, 0.66,
  0.6, 0.7, 0.5, 0.6, 0.35, 0.35, 0.35, 0.8, 0.6, 0.7, 0.8, 0.4, 0.89, 0.3
];
const positions = [
  { x: 0, y: 0, z: 0 }, { x: 1.2, y: 0.9, z: -0.5 }, { x: 1.8, y: -0.3, z: 0 }, { x: -1, y: -1, z: 0 },
  { x: -1, y: 1.62, z: 0 }, { x: -1.65, y: 0, z: -0.4 }, { x: -2.13, y: -1.54, z: -0.4 }, { x: 0.8, y: 0.94, z: 0.3 },
  { x: 0.5, y: -1, z: 1.2 }, { x: -0.16, y: -1.2, z: 0.9 }, { x: 1.5, y: 1.2, z: 0.8 }, { x: 0.5, y: -1.58, z: 1.4 },
  { x: -1.5, y: 1, z: 1.15 }, { x: -1.5, y: -1.5, z: 0.99 }, { x: -1.5, y: -1.5, z: -1.9 }, { x: 1.85, y: 0.8, z: 0.05 },
  { x: 1.5, y: -1.2, z: -0.75 }, { x: 0.9, y: -1.62, z: 0.22 }, { x: 0.45, y: 2, z: 0.65 }, { x: 2.5, y: 1.22, z: -0.2 },
  { x: 2.35, y: 0.7, z: 0.55 }, { x: -1.8, y: -0.35, z: 0.85 }, { x: -1.02, y: 0.2, z: 0.9 }, { x: 0.2, y: 1, z: 1 },
  { x: -2.88, y: 0.7, z: 1 },

  { x: -2, y: -0.95, z: 1.5 }, { x: -2.3, y: 2.4, z: -0.1 }, { x: -2.5, y: 1.9, z: 1.2 }, { x: -1.8, y: 0.37, z: 1.2 },
  { x: -2.4, y: 1.42, z: 0.05 }, { x: -2.72, y: -0.9, z: 1.1 }, { x: -1.8, y: -1.34, z: 1.67 }, { x: -1.6, y: 1.66, z: 0.91 },
  { x: -2.8, y: 1.58, z: 1.69 }, { x: -2.97, y: 2.3, z: 0.65 }, { x: 1.1, y: -0.2, z: -1.45 }, { x: -4, y: 1.78, z: 0.38 },
  { x: 0.12, y: 1.4, z: -1.29 }, { x: -1.64, y: 1.4, z: -1.79 }, { x: -3.5, y: -0.58, z: 0.1 }, { x: -0.1, y: -1, z: -2 },
  { x: -4.5, y: 0.55, z: -0.5 }, { x: -3.87, y: 0, z: 1 }, { x: -4.6, y: -0.1, z: 0.65 }, { x: -3, y: 1.5, z: -0.7 },
  { x: -0.5, y: 0.2, z: -1.5 }, { x: -1.3, y: -0.45, z: -1.5 }, { x: -3.35, y: 0.25, z: -1.5 }, { x: -4.76, y: -1.26, z: 0.4 },
  { x: -4.32, y: 0.85, z: 1.4 }, { x: -3.5, y: -1.82, z: 0.9 }, { x: -3.6, y: -0.6, z: 1.46 }, { x: -4.55, y: -1.5, z: 1.63 },
  { x: -3.8, y: -1.15, z: 2.1 }, { x: -2.9, y: -0.25, z: 1.86 }, { x: -2.2, y: -0.4, z: 1.86 }, { x: -5.1, y: -0.24, z: 1.86 },
  { x: -5.27, y: 1.24, z: 0.76 }, { x: -5.27, y: 2, z: -0.4 }, { x: -6.4, y: 0.4, z: 1 }, { x: -5.15, y: 0.95, z: 2 },
  { x: -6.2, y: 0.5, z: -0.8 }, { x: -4, y: 0.08, z: 1.8 },

  { x: 2, y: -0.95, z: 1.5 }, { x: 2.3, y: 2.4, z: -0.1 }, { x: 2.5, y: 1.9, z: 1.2 }, { x: 1.8, y: 0.37, z: 1.2 },
  { x: 3.24, y: 0.6, z: 1.05 }, { x: 2.72, y: -0.9, z: 1.1 }, { x: 1.8, y: -1.34, z: 1.67 }, { x: 1.6, y: 1.99, z: 0.91 },
  { x: 2.8, y: 1.58, z: 1.69 }, { x: 2.97, y: 2.3, z: 0.65 }, { x: -1.3, y: -0.2, z: -2.5 }, { x: 4, y: 1.78, z: 0.38 },
  { x: 1.72, y: 1.4, z: -1.29 }, { x: 2.5, y: -1.2, z: -2 }, { x: 3.5, y: -0.58, z: 0.1 }, { x: 0.1, y: 0.4, z: -2.42 },
  { x: 4.5, y: 0.55, z: -0.5 }, { x: 3.87, y: 0, z: 1 }, { x: 4.6, y: -0.1, z: 0.65 }, { x: 3, y: 1.5, z: -0.7 },
  { x: 2.3, y: 0.6, z: -2.6 }, { x: 4, y: 1.5, z: -1.6 }, { x: 3.35, y: 0.25, z: -1.5 }, { x: 4.76, y: -1.26, z: 0.4 },
  { x: 4.32, y: 0.85, z: 1.4 }, { x: 3.5, y: -1.82, z: 0.9 }, { x: 3.6, y: -0.6, z: 1.46 }, { x: 4.55, y: -1.5, z: 1.63 },
  { x: 3.8, y: -1.15, z: 2.1 }, { x: 2.9, y: -0.25, z: 1.86 }, { x: 2.2, y: -0.4, z: 1.86 }, { x: 5.1, y: -0.24, z: 1.86 },
  { x: 5.27, y: 1.24, z: 0.76 }, { x: 5.27, y: 2, z: -0.4 }, { x: 6.4, y: 0.4, z: 1 }, { x: 5.15, y: 0.95, z: 2 },
  { x: 6.2, y: 0.5, z: -0.8 }, { x: 4, y: 0.08, z: 1.8 }
];

const material = new THREE.MeshLambertMaterial({ color: "#c7a5a5", emissive: "red" });
const group = new THREE.Group();
const spheres = [];

positions.forEach((pos, index) => {
  const radius = radii[index];
  const geometry = new THREE.SphereGeometry(radius, 64, 64);
  const sphere = new THREE.Mesh(geometry, material);
  sphere.position.set(pos.x, pos.y, pos.z);
  sphere.userData = { originalPosition: { ...pos }, radius };
  sphere.castShadow = true;
  sphere.receiveShadow = true;
  spheres.push(sphere);
  group.add(sphere);
});
scene.add(group);

// Lighting
const ambientLight = new THREE.AmbientLight(0xffffff, 1);
scene.add(ambientLight);

const spotLight = new THREE.SpotLight(0xffffff, 0.52);
spotLight.position.set(14, 24, 30);
spotLight.castShadow = true;
scene.add(spotLight);

const directionalLight1 = new THREE.DirectionalLight(0xffffff, 0.2);
directionalLight1.position.set(0, -4, 0);
scene.add(directionalLight1);

const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();
const tempVector = new THREE.Vector3();
const forces = new Map();

const initY = -25;
const revolutionRadius = 4;
const revolutionDuration = 2;
const breathingAmplitude = 0.1;
const breathingSpeed = 0.002;

spheres.forEach((sphere) => { sphere.position.y = initY; });

function initLoadingAnimation() {
  spheres.forEach((sphere, i) => {
    const delay = i * 0.02;
    gsap.timeline()
      .to(sphere.position, {
        duration: revolutionDuration / 2,
        y: revolutionRadius,
        ease: "power1.out",
        onUpdate: function () {
          const progress = this.progress();
          sphere.position.z = sphere.userData.originalPosition.z + Math.sin(progress * Math.PI) * revolutionRadius;
        },
        delay: delay
      })
      .to(sphere.position, {
        duration: revolutionDuration / 2,
        y: initY / 5,
        ease: "power1.out",
        onUpdate: function () {
          const progress = this.progress();
          sphere.position.z = sphere.userData.originalPosition.z - Math.sin(progress * Math.PI) * revolutionRadius;
        }
      })
      .to(sphere.position, {
        duration: 0.6,
        x: sphere.userData.originalPosition.x,
        y: sphere.userData.originalPosition.y,
        z: sphere.userData.originalPosition.z,
        ease: "power1.out"
      });
  });
}

if (document.readyState === "complete") {
  initLoadingAnimation();
} else {
  window.addEventListener("load", initLoadingAnimation);
}

const hiddenElements = document.querySelectorAll(".hide-text");
const main_txt = document.querySelector(".main-txt");

hiddenElements.forEach((el) => { el.style.opacity = "0"; });

let loadingComplete = false;
setTimeout(() => {
  loadingComplete = true;
  hiddenElements.forEach((el) => { el.style.opacity = "1"; });
  main_txt.style.opacity = "0";
}, (revolutionDuration + 1) * 1000);

function onMouseMove(event) {
  if (!loadingComplete) return;

  // Only push spheres while the pointer is over the hero
  const rect = renderer.domElement.getBoundingClientRect();
  if (event.clientY < rect.top || event.clientY > rect.bottom) return;

  mouse.x = ((event.clientX - rect.left) / rect.width) * 2 - 1;
  mouse.y = -((event.clientY - rect.top) / rect.height) * 2 + 1;

  raycaster.setFromCamera(mouse, camera);
  const intersects = raycaster.intersectObjects(spheres);

  if (intersects.length > 0) {
    const hoveredSphere = intersects[0].object;
    const force = new THREE.Vector3();
    force.subVectors(intersects[0].point, hoveredSphere.position).normalize().multiplyScalar(0.2);
    forces.set(hoveredSphere.uuid, force);
  }
}

function handleCollisions() {
  for (let i = 0; i < spheres.length; i++) {
    const sphereA = spheres[i];
    const radiusA = sphereA.userData.radius;
    for (let j = i + 1; j < spheres.length; j++) {
      const sphereB = spheres[j];
      const radiusB = sphereB.userData.radius;
      const distance = sphereA.position.distanceTo(sphereB.position);
      const minDistance = (radiusA + radiusB) * 1.2;
      if (distance < minDistance) {
        tempVector.subVectors(sphereB.position, sphereA.position);
        tempVector.normalize();
        const pushStrength = (minDistance - distance) * 0.4;
        sphereA.position.sub(tempVector.multiplyScalar(pushStrength));
        sphereB.position.add(tempVector.multiplyScalar(pushStrength));
      }
    }
  }
}

// Pause the 3D work when the hero is scrolled out of view
let heroVisible = true;
new IntersectionObserver((entries) => {
  heroVisible = entries[0].isIntersecting;
}).observe(hero);

function animate() {
  requestAnimationFrame(animate);
  if (!heroVisible) return;

  if (loadingComplete) {
    const time = Date.now() * breathingSpeed;
    spheres.forEach((sphere, i) => {
      const offset = i * 0.2;
      const breathingY = Math.sin(time + offset) * breathingAmplitude;
      const breathingZ = Math.cos(time + offset) * breathingAmplitude * 0.5;

      const force = forces.get(sphere.uuid);
      if (force) {
        sphere.position.add(force);
        force.multiplyScalar(0.95);
        if (force.length() < 0.01) forces.delete(sphere.uuid);
      }

      const originalPos = sphere.userData.originalPosition;
      tempVector.set(originalPos.x, originalPos.y + breathingY, originalPos.z + breathingZ);
      sphere.position.lerp(tempVector, 0.018);
    });
    handleCollisions();
  }

  controls.update();
  renderer.render(scene, camera);
}

window.addEventListener("mousemove", onMouseMove);
animate();
window.addEventListener("resize", sizeScene);

// Ticket tilt and holographic sheen
if (window.matchMedia("(pointer: fine)").matches) {
  document.querySelectorAll(".ticket").forEach((t) => {
    t.addEventListener("pointermove", (e) => {
      const r = t.getBoundingClientRect();
      const px = (e.clientX - r.left) / r.width;
      const py = (e.clientY - r.top) / r.height;
      const k = parseFloat(t.dataset.tilt || 1);
      t.style.transform = `perspective(900px) rotateX(${(0.5 - py) * 10 * k}deg) rotateY(${(px - 0.5) * 12 * k}deg)`;
      t.style.setProperty("--mx", px * 100 + "%");
      t.style.setProperty("--my", py * 100 + "%");
    });
    t.addEventListener("pointerleave", () => {
      t.style.transform = "";
      t.style.setProperty("--mx", "50%");
      t.style.setProperty("--my", "30%");
    });
  });
}

const band = document.querySelector(".marquee-band");
if (band && window.matchMedia("(pointer: fine)").matches) {
  band.addEventListener("pointermove", (e) => {
    const r = band.getBoundingClientRect();
    band.style.setProperty("--mx", ((e.clientX - r.left) / r.width) * 100 + "%");
    band.style.setProperty("--my", ((e.clientY - r.top) / r.height) * 100 + "%");
  });
}

// Scroll reveals and parallax
if (window.ScrollTrigger) {
  gsap.registerPlugin(ScrollTrigger);

  gsap.utils.toArray(".reveal").forEach((el) => {
    gsap.from(el, {
      y: 60,
      opacity: 0,
      duration: 1.1,
      ease: "power3.out",
      scrollTrigger: { trigger: el, start: "top 88%" }
    });
  });

  gsap.utils.toArray(".parallax").forEach((el) => {
    const speed = parseFloat(el.dataset.speed) || 0.2;
    gsap.to(el, {
      y: () => speed * 300,
      ease: "none",
      scrollTrigger: { trigger: ".quote", start: "top bottom", end: "bottom top", scrub: true }
    });
  });

  gsap.from(".footer-word", {
    yPercent: 40,
    opacity: 0,
    ease: "power3.out",
    duration: 1.2,
    scrollTrigger: { trigger: ".footer-word", start: "top 95%" }
  });
}
</script>
</body>
</html>
```

