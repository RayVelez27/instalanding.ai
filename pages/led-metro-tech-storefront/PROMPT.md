INSTALANDING.AI · LED Metro Tech Storefront

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
LED Metro Tech Storefront · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/led-metro-tech-storefront

meridian-led-storefront.html:
```html
<!DOCTYPE html>
<!--
  INSTALANDING.AI · LED Metro Tech Storefront
  slug     led-metro-tech-storefront
  prompt   https://instalanding.ai/p/led-metro-tech-storefront.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/led-metro-tech-storefront
  license  MIT. Fictional brand ("Meridian"); replace names, copy, offers and links before shipping.

  MAP
  tokens    :root custom properties at the top of the <style>: --bg-color (warm paper), --brand-dark,
            --brand-purple / --brand-purple-deep, --brand-green, --clay-light, four --clay-shadow-* recipes and
            --soft-shadow; --display (Bricolage Grotesque), --serif (Fraunces italic accents), --text (Instrument
            Sans) from Google Fonts. body.is-business swaps the accent to blue.
  sections  nav, hero, quick-links, featured, travel, ai, faq, ballot, footer
  scripts   GSAP 3.12.2 + ScrollTrigger from cdnjs; one inline DOMContentLoaded script: buildLED() (LED metro
            maps for the hero, the slider laptop and the supply-chain card, trains on GSAP timelines), the
            dot-matrix ticker, Personal/Business mode switch (localStorage), FAQ accordion, intro timeline +
            float loops, scroll reveals with an on-screen sweep, featured slider, laptop-lid scrub, article
            spotlight, magnetic buttons
  assets    every visual is CSS or inline SVG: devices, LED boards, logo mark, icons, grain (data-URI SVG)

  ADAPTING
  - LED lines are waypoint lists on a cols x rows grid; segments must be straight or exactly 45 degrees,
    or expand() never reaches the next waypoint.
  - The LED pitch is recomputed from the screen box by a ResizeObserver; give every .led-screen a real
    size (aspect-ratio or inset:0 in a sized parent) or it renders at 0px.
  - Reveals only hide elements when motion is allowed, and a sweep on ScrollTrigger refresh/scrollEnd
    reveals anything already on screen; a bare batch({ once: true }) leaves sections at opacity 0 when
    the page loads scrolled.
  - Do not put a float loop and the scrubbed parallax on the same element's y (the LED panel only
    has the parallax; the floating pills only float).
  - Personal/Business content is toggled by [data-for]; both copies must exist in the DOM.
  - body uses overflow-x: clip, not hidden, so the sticky nav keeps working.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Meridian · Devices, apps and AI</title>
<meta name="description" content="Meridian, a fictional devices-and-AI company homepage: clay surfaces, an LED metro-map hero and a personal/business mode switch.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,400..800&family=Fraunces:ital,opsz,wght@1,9..144,300..600&family=Instrument+Sans:wght@400..700&family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>

<style>
:root {
  --bg-color: #f6f5f1;
  --surface: #ffffff;
  --text-dark: #111317;
  --text-gray: #6f747c;
  --hairline: rgba(17, 19, 23, 0.08);
  --brand-purple: #9d8cdc;
  --brand-purple-deep: #6c5bbd;
  --brand-green: #8fdea0;
  --brand-dark: #16191e;
  --clay-light: #f1f0ec;

  --serif: "Fraunces", Georgia, serif;
  --display: "Bricolage Grotesque", "Inter", sans-serif;
  --text: "Instrument Sans", "Inter", sans-serif;

  --clay-shadow-light: 15px 15px 30px rgba(0,0,0,0.05),
    -10px -10px 20px rgba(255,255,255,0.8),
    inset 2px 2px 5px rgba(255,255,255,1),
    inset -3px -3px 10px rgba(0,0,0,0.04);
  --clay-shadow-dark: 10px 15px 25px rgba(0,0,0,0.18),
    inset 2px 2px 5px rgba(255,255,255,0.15),
    inset -3px -3px 8px rgba(0,0,0,0.4);
  --clay-shadow-purple: 15px 20px 35px rgba(157,140,220,0.25),
    inset 2px 2px 8px rgba(255,255,255,0.4),
    inset -4px -4px 12px rgba(0,0,0,0.15);
  --clay-shadow-green: 8px 12px 20px rgba(143,222,160,0.3),
    inset 2px 2px 6px rgba(255,255,255,0.6),
    inset -3px -3px 8px rgba(0,0,0,0.1);
  --soft-shadow: 0 1px 2px rgba(17,19,23,0.04), 0 8px 24px rgba(17,19,23,0.06), 0 32px 64px -24px rgba(17,19,23,0.12);
}

* { margin: 0; padding: 0; box-sizing: border-box; font-family: "Inter", sans-serif; }
html { scroll-behavior: smooth; }
/* clip, not hidden: hidden makes body a scroll container and the sticky nav stops sticking */
body { background-color: var(--bg-color); color: var(--text-dark); overflow-x: clip; min-height: 100vh; -webkit-font-smoothing: antialiased; }
a { color: inherit; }
em.serif, .serif { font-family: var(--serif); font-style: italic; font-weight: 400; letter-spacing: -0.5px; }

/* Grain + ambient light */
body::before {
  content: ""; position: fixed; inset: 0; pointer-events: none; z-index: 999; opacity: 0.035;
  background-image: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='160' height='160'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='3' stitchTiles='stitch'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
}
.ambient { position: absolute; inset: 0 0 auto 0; height: 1100px; overflow: hidden; pointer-events: none; z-index: 0; }
.ambient span { position: absolute; border-radius: 50%; filter: blur(90px); }
.ambient span:nth-child(1) { width: 520px; height: 520px; background: rgba(157,140,220,0.28); top: -120px; right: 4%; }
.ambient span:nth-child(2) { width: 420px; height: 420px; background: rgba(143,222,160,0.22); top: 380px; right: 30%; }
.ambient span:nth-child(3) { width: 360px; height: 360px; background: rgba(255,214,170,0.25); top: 120px; left: -120px; }

.container { max-width: 1320px; margin: 0 auto; padding: 20px 40px; position: relative; z-index: 1; }

/* --- Brand mark (fictional): globe with two meridians, then the wordmark --- */
.brandmark { display: inline-flex; align-items: center; gap: 0.32em; font-family: var(--display); font-weight: 720; letter-spacing: -0.04em; line-height: 1; color: inherit; }
.brandmark svg { height: 1.15em; width: auto; display: block; flex: none; }

/* --- Navigation --- */
nav { display: flex; justify-content: space-between; align-items: center; padding: 14px 14px 14px 24px; z-index: 100; position: sticky; top: 14px; gap: 24px;
  background: rgba(255,255,255,0.72); backdrop-filter: blur(18px) saturate(1.4); -webkit-backdrop-filter: blur(18px) saturate(1.4);
  border: 1px solid rgba(255,255,255,0.9); border-radius: 22px; box-shadow: var(--soft-shadow); }
.nav-left { display: flex; align-items: center; gap: 28px; }
.logo { display: flex; align-items: center; color: var(--text-dark); text-decoration: none; font-size: 24px; }
.segmented { display: inline-flex; background: var(--clay-light); padding: 4px; border-radius: 14px; position: relative; box-shadow: inset 0 1px 2px rgba(0,0,0,0.06); }
.segmented button { position: relative; z-index: 1; border: none; background: none; padding: 8px 16px; font-size: 13px; font-weight: 600; color: var(--text-gray); cursor: pointer; border-radius: 10px; transition: color 0.3s; }
.segmented button.active { color: var(--text-dark); }
.segmented button:focus-visible { outline: 2px solid var(--brand-purple-deep); outline-offset: 1px; }
.segmented .seg-thumb { position: absolute; top: 4px; bottom: 4px; left: 4px; border-radius: 10px; background: #fff; box-shadow: 0 1px 2px rgba(0,0,0,0.08), 0 4px 10px rgba(0,0,0,0.06); z-index: 0; }
.nav-links { display: flex; gap: 32px; list-style: none; }
.nav-links a { text-decoration: none; color: var(--text-gray); font-size: 14px; font-weight: 500; transition: color 0.3s; }
.nav-links a:hover { color: var(--text-dark); }
.nav-actions { display: flex; align-items: center; gap: 10px; }
.icon-btn { width: 42px; height: 42px; border-radius: 14px; border: 1px solid var(--hairline); background: #fff; display: flex; align-items: center; justify-content: center; cursor: pointer; color: var(--text-dark); }
.search-icon { width: 18px; height: 18px; }
.menu-toggle { display: none; }
.menu-toggle span, .menu-toggle span::before, .menu-toggle span::after { display: block; width: 16px; height: 2px; background: var(--brand-dark); border-radius: 2px; position: relative; }
.menu-toggle span::before, .menu-toggle span::after { content: ""; position: absolute; left: 0; }
.menu-toggle span::before { top: -5px; } .menu-toggle span::after { top: 5px; }

/* --- Hero --- */
.hero { display: flex; justify-content: space-between; margin-top: 72px; gap: 56px; min-height: 80vh; }
.left-col { flex: 1; max-width: 540px; display: flex; flex-direction: column; justify-content: center; }
.badge-row { display: flex; align-items: center; gap: 12px; margin-bottom: 28px; flex-wrap: wrap; }
.hero-badge { display: inline-flex; align-items: center; gap: 12px; padding: 5px 16px 5px 5px; border-radius: 999px; background: rgba(255,255,255,0.75); border: 1px solid var(--hairline); box-shadow: 0 2px 8px rgba(0,0,0,0.04); backdrop-filter: blur(8px); max-width: 100%; }
.hero-badge-tag { flex: none; display: inline-flex; align-items: center; gap: 7px; background: var(--brand-dark); color: var(--brand-green); padding: 6px 11px 6px 9px; border-radius: 999px; font-size: 11px; font-weight: 700; letter-spacing: 1px; }
.hero-badge-tag::before { content: ""; width: 6px; height: 6px; border-radius: 50%; background: #6ee86e; box-shadow: 0 0 6px #6ee86e; }
.hero-badge-text { font-size: 13px; font-weight: 500; color: var(--text-gray); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
h1 { font-size: 88px; font-weight: 700; line-height: 0.98; letter-spacing: -3.5px; margin-bottom: 28px; color: var(--text-dark); }
h1 em { font-family: var(--serif); font-style: italic; font-weight: 400; letter-spacing: -2px; color: var(--brand-purple-deep); }
.hero-sub { font-size: 17px; line-height: 1.6; color: var(--text-gray); max-width: 470px; margin-bottom: 36px; }
.hero-sub strong { color: var(--text-dark); font-weight: 600; }
.cta-group { display: flex; align-items: center; gap: 24px; margin-bottom: 56px; flex-wrap: wrap; }
.btn-primary { background-color: var(--brand-dark); color: white; padding: 8px 8px 8px 26px; border-radius: 40px; font-size: 14px; font-weight: 600; border: none; cursor: pointer; box-shadow: var(--clay-shadow-dark); transition: transform 0.2s; text-decoration: none; display: inline-flex; align-items: center; gap: 16px; }
.btn-primary .arr { width: 40px; height: 40px; border-radius: 50%; background: var(--brand-green); color: var(--brand-dark); display: flex; align-items: center; justify-content: center; transition: transform 0.35s cubic-bezier(.2,.8,.2,1); }
.btn-primary:hover .arr { transform: rotate(-45deg); }
.btn-primary .arr svg { width: 16px; height: 16px; }
.btn-primary:active { transform: scale(0.97); }
.link-underline { font-size: 14px; font-weight: 600; color: var(--text-dark); text-decoration: none; position: relative; }
.link-underline::after { content: ""; position: absolute; left: 0; bottom: -4px; width: 100%; height: 2px; background-color: var(--text-dark); opacity: 0.2; transform-origin: left; transition: opacity 0.3s; }
.link-underline:hover::after { opacity: 0.8; }

/* AI suggestion card */
.download-card { background: rgba(255,255,255,0.75); backdrop-filter: blur(12px); padding: 22px; border-radius: 26px; box-shadow: var(--soft-shadow); display: flex; flex-direction: column; gap: 18px; width: 100%; max-width: 440px; position: relative; border: 1px solid rgba(255,255,255,0.95); }
.download-top { display: flex; align-items: center; gap: 16px; }
.app-icon { width: 56px; height: 56px; flex: none; background-color: var(--brand-dark); border-radius: 16px; box-shadow: var(--clay-shadow-dark); display: flex; justify-content: center; align-items: center; }
.app-icon svg { width: 26px; height: 26px; fill: var(--brand-green); }
.download-text { font-size: 14px; color: var(--text-dark); font-weight: 600; flex: 1; line-height: 1.4; }
.download-text span { display: block; color: var(--text-gray); font-weight: 500; font-size: 12px; margin-bottom: 2px; letter-spacing: 0.3px; }
.download-text span + span { color: var(--text-dark); font-weight: 600; font-size: 14px; letter-spacing: 0; margin: 0; }
.small-purple-icon { width: 32px; height: 32px; flex: none; background-color: var(--brand-purple); border-radius: 50%; box-shadow: var(--clay-shadow-purple); display: flex; justify-content: center; align-items: center; color: #fff; }
.chips { display: flex; flex-wrap: wrap; gap: 8px; }
.chip { display: inline-flex; align-items: center; gap: 8px; padding: 10px 14px; border-radius: 14px; background: #fff; border: 1px solid var(--hairline); font-size: 13px; font-weight: 500; color: var(--text-dark); text-decoration: none; transition: background 0.25s, border-color 0.25s, transform 0.25s; }
.chip:hover { background: var(--brand-dark); color: #fff; border-color: var(--brand-dark); }
.chip svg { width: 14px; height: 14px; opacity: 0.7; }
.dots-vert { position: absolute; left: -20px; top: 50%; display: flex; flex-direction: column; gap: 4px; }
.dots-vert span { width: 4px; height: 4px; background: #cfcfcf; border-radius: 50%; }

/* Right column */
.right-col { flex: 1.05; position: relative; display: flex; flex-direction: column; }
.top-right-info { display: flex; align-items: center; gap: 16px; margin-left: 20px; margin-bottom: 20px; }
.pixel-art { display: grid; grid-template-columns: repeat(4, 8px); grid-template-rows: repeat(3, 8px); gap: 2px; }
.pixel-art div { background-color: var(--brand-green); border-radius: 2px; }
.pixel-art div:nth-child(even) { background-color: var(--brand-dark); }
.pixel-art div:nth-child(3n) { background-color: var(--text-gray); opacity: 0.5; }
.info-text { font-size: 13px; color: var(--text-gray); font-weight: 500; line-height: 1.4; }

.chart-area { position: relative; width: 100%; height: 440px; margin-top: 20px; }
.chart-area .asterisk { left: -14px; top: -4px; z-index: 4; }
.chart-area .sticker { right: -6px; }

/* ===== LED metro map (style adapted from Ben Evans' CSS LED Challenge) ===== */
.led-panel { position: absolute; top: 20px; left: 0; width: 88%; z-index: 1; padding: 12px; border-radius: 30px;
  background: radial-gradient(at left bottom, #1d1a26, #0c0c10 70%);
  box-shadow: inset 0 0 0 1px rgba(255,255,255,0.06), inset 0 0 24px rgba(0,0,0,0.7),
    0 0 0 6px rgba(255,255,255,0.7), 0 30px 60px -20px rgba(22,25,30,0.55), 0 0 90px -10px rgba(157,140,220,0.45); }
.led-panel::after { content: ""; position: absolute; inset: 0; border-radius: inherit; pointer-events: none; background: linear-gradient(155deg, rgba(255,255,255,0.08), transparent 32%); z-index: 5; }
.led-head { display: flex; justify-content: space-between; align-items: center; gap: 10px; padding: 2px 4px 12px; }
.led-live { display: flex; align-items: center; gap: 8px; font-size: 10px; font-weight: 700; letter-spacing: 1.6px; color: #8b8f98; white-space: nowrap; }
.led-live i { width: 7px; height: 7px; border-radius: 50%; background: #6ee86e; box-shadow: 0 0 6px #6ee86e, 0 0 14px rgba(110,232,110,0.6); animation: led-blink 1.6s ease-in-out infinite; }
.led-controls { display: flex; align-items: center; gap: 12px; }
.led-modes { display: flex; background: rgba(255,255,255,0.06); border-radius: 10px; padding: 3px; box-shadow: inset 0 0 0 1px rgba(255,255,255,0.05); }
.led-modes button { border: none; background: none; color: #8b8f98; font-size: 11px; font-weight: 600; padding: 6px 10px; border-radius: 8px; cursor: pointer; transition: background 0.2s, color 0.2s; }
.led-modes button:hover { color: #e8e8e8; }
.led-modes button.active { background: rgba(255,255,255,0.14); color: #fff; }
.led-swatches { display: flex; gap: 6px; }
.led-swatches button { width: 13px; height: 13px; border-radius: 50%; border: none; padding: 0; background: var(--sw); opacity: 0.45; cursor: pointer; box-shadow: 0 0 0 2px rgba(255,255,255,0.08); transition: opacity 0.15s, transform 0.15s, box-shadow 0.15s; }
.led-swatches button:hover { transform: scale(1.15); }
.led-swatches button.on { opacity: 1; box-shadow: 0 0 0 2px #fff, 0 0 10px var(--sw); }
.led-panel button:focus-visible, .led-swatches button:focus-visible { outline: 2px solid #fff; outline-offset: 2px; }

.led-screen { position: relative; border-radius: 18px; overflow: hidden; background: #17151d; box-shadow: inset 0 0 20px rgba(0,0,0,0.8); }
.hero-led { aspect-ratio: 36 / 20; }
.led-screen::after { content: ""; position: absolute; inset: 0; pointer-events: none; background: linear-gradient(rgba(42,108,255,0.12), transparent 60%); mix-blend-mode: soft-light; }
.led-stage { position: absolute; left: 50%; top: 50%; width: calc(var(--cols) * var(--pitch, 10px)); height: calc(var(--rows) * var(--pitch, 10px)); transform: translate(-50%, -50%);
  --dot: calc(var(--pitch, 10px) * 0.6);
  background-image: radial-gradient(circle closest-side, rgba(255,255,255,0.05) 0 22%, transparent 34%); background-size: var(--pitch, 10px) var(--pitch, 10px); }
.led-stage > div { position: absolute; inset: 0; }
.led-board i, .led-lit i, .led-board u { position: absolute; left: calc((var(--x) + 0.5) * var(--pitch, 10px)); top: calc((var(--y) + 0.5) * var(--pitch, 10px)); border-radius: 50%; }
.led-board i, .led-lit i { --c: var(--lc); width: var(--dot); height: var(--dot); margin: calc(var(--dot) / -2) 0 0 calc(var(--dot) / -2); }
.led-board i { background: color-mix(in srgb, var(--c) 18%, #1f1c26); box-shadow: inset 0 1px 1px rgba(255,255,255,0.08); transition: opacity 0.3s; }
.led-board u { --ring: calc(var(--pitch, 10px) * 1.45); width: var(--ring); height: var(--ring); margin: calc(var(--ring) / -2) 0 0 calc(var(--ring) / -2); border: max(1.5px, calc(var(--pitch, 10px) * 0.13)) solid rgba(230,232,242,0.18); box-sizing: border-box; }
.led-lit { z-index: 2; }
.led-lit i { --vis: 1; background: var(--c);
  box-shadow: 0 0 calc(var(--pitch, 10px) * 0.4) color-mix(in srgb, var(--c) 70%, transparent), 0 0 calc(var(--pitch, 10px) * 1.2) color-mix(in srgb, var(--c) 32%, transparent);
  opacity: calc(0.16 * var(--vis)); transform: scale(0); transition: transform 0.45s ease-out; transition-delay: calc(var(--i) * 14ms); }
.led-screen.booted .led-lit i { transform: scale(1); }
.led-trains { z-index: 3; }
.led-trains t { --c: var(--lc); position: absolute; display: block; left: 0; top: 0; width: calc(var(--pitch, 10px) * 2); height: calc(var(--pitch, 10px) * 0.65); border-radius: 99px;
  background: linear-gradient(90deg, transparent, #fff 50%, rgba(255,255,255,0.9) 78%, transparent);
  box-shadow: 0 0 calc(var(--pitch, 10px) * 0.7) var(--c), 0 0 calc(var(--pitch, 10px) * 1.8) color-mix(in srgb, var(--c) 55%, transparent);
  opacity: 0; transition: opacity 0.6s; }
.led-screen.booted .led-trains t { opacity: 1; }

.led-screen.mode-chase .led-lit i { animation: led-chase 2s linear infinite; animation-delay: calc((var(--n) - var(--i)) * -34ms); }
.led-screen.mode-rainbow .led-lit { animation: led-hues 9s linear infinite; }
.led-screen.mode-rainbow .led-lit i { --c: hsl(calc(var(--i) * 9deg) 92% 62%); opacity: calc(0.92 * var(--vis)); }
.led-screen.mode-breathe .led-lit { animation: led-breathe 5s ease-in-out infinite; }
.led-screen.mode-breathe .led-lit i { opacity: calc(1 * var(--vis)); }
.led-screen.filtering .led-lit i:not(.on) { --vis: 0.07; }
.led-screen.filtering .led-board i:not(.on) { opacity: 0.5; }
.led-screen.booted.filtering .led-trains t:not(.on) { opacity: 0.08; }
.led-screen.offscreen .led-lit, .led-screen.offscreen .led-lit i { animation-play-state: paused; }

@keyframes led-chase { 0% { opacity: calc(1 * var(--vis)); } 14%, 100% { opacity: calc(0.16 * var(--vis)); } }
@keyframes led-hues { to { filter: hue-rotate(360deg); } }
@keyframes led-breathe { 0%, 100% { opacity: 0.32; } 50% { opacity: 1; } }
@keyframes led-blink { 0%, 100% { opacity: 1; } 50% { opacity: 0.35; } }

/* LED screens inside other components */
.laptop .screen .led-screen { position: absolute; inset: 0; border-radius: inherit; }
.v-trade { background: #0c0c10; }
.v-trade .led-screen { position: absolute; inset: 0; border-radius: inherit; }
.agile-chip { position: absolute; right: 14px; bottom: 14px; z-index: 4; background: rgba(255,255,255,0.92); color: var(--brand-dark); font-size: 12px; font-weight: 700; padding: 8px 12px; border-radius: 12px; display: flex; align-items: center; gap: 8px; box-shadow: 0 6px 18px rgba(0,0,0,0.35); }
.agile-chip i { width: 7px; height: 7px; border-radius: 50%; background: #6ee86e; box-shadow: 0 0 8px #6ee86e; animation: led-blink 1.6s ease-in-out infinite; }

/* Dot-matrix ticker */
.ticker { --p: 7px; position: relative; width: 100%; height: calc(var(--p) * 9); border-radius: 16px; overflow: hidden; background-color: #0b0c0f;
  background-image: radial-gradient(circle closest-side, rgba(255,255,255,0.07) 0 30%, transparent 42%); background-size: var(--p) var(--p);
  box-shadow: inset 0 0 18px rgba(0,0,0,0.85), inset 0 0 0 1px rgba(255,255,255,0.07); }
.ticker::after { content: ""; position: absolute; inset: 0; pointer-events: none; background: linear-gradient(90deg, #0b0c0f, transparent 8%, transparent 92%, #0b0c0f), linear-gradient(170deg, rgba(255,255,255,0.06), transparent 40%); }
.ticker-track { position: absolute; left: 0; top: var(--p); display: flex; will-change: transform; }
.ticker svg { display: block; flex: none; filter: drop-shadow(0 0 2px rgba(143,222,160,0.95)) drop-shadow(0 0 7px rgba(143,222,160,0.5)); }

@media (max-width: 720px) {
  .hero .chart-area { height: 300px; }
  .led-panel { width: 92%; padding: 9px; border-radius: 24px; }
  .led-swatches { display: none; }
  .led-modes button { padding: 5px 8px; font-size: 10px; }
  .led-screen { border-radius: 14px; }
  .ticker { --p: 6px; }
}
@media (prefers-reduced-motion: reduce) {
  .led-lit, .led-lit i, .led-live i, .agile-chip i, .eyebrow::before { animation-play-state: paused !important; }
  .led-lit i { transition: none; }
}
.floating-element { position: absolute; z-index: 10; }
.sticker { top: -40px; right: 5%; width: 96px; height: 96px; background-color: var(--brand-dark); border-radius: 50%; color: white; font-size: 11px; font-weight: 700; letter-spacing: 1px; text-align: center; line-height: 1.3; display: flex; justify-content: center; align-items: center; transform: rotate(15deg); box-shadow: var(--clay-shadow-dark); border: 2px solid rgba(255,255,255,0.1); }
.sticker::after { content: ""; position: absolute; bottom: 22px; width: 40px; height: 2px; background-color: var(--brand-green); border-radius: 2px; transform: rotate(-5deg); }
.pill-dark { bottom: 40px; left: 8%; background-color: #fff; padding: 10px 22px 10px 10px; border-radius: 30px; display: flex; align-items: center; gap: 12px; box-shadow: var(--soft-shadow); border: 1px solid #fff; }
.pill-dark .icon { width: 40px; height: 40px; background-color: var(--brand-dark); border-radius: 14px; display: flex; justify-content: center; align-items: center; color: var(--brand-green); box-shadow: var(--clay-shadow-dark); }
.pill-dark .icon svg { width: 18px; height: 18px; }
.pill-dark .text { font-size: 18px; font-weight: 700; letter-spacing: -0.3px; line-height: 1.1; }
.pill-dark .text small { display: block; font-size: 11px; font-weight: 500; color: var(--text-gray); letter-spacing: 0; }
.pill-secure { bottom: 50px; right: 22%; background-color: #fff; padding: 8px 16px 8px 8px; border-radius: 20px; display: flex; align-items: center; gap: 8px; font-size: 13px; font-weight: 600; box-shadow: var(--soft-shadow); border: 1px solid #fff; }
.pill-secure .icon { width: 24px; height: 24px; background-color: var(--brand-dark); border-radius: 50%; display: flex; justify-content: center; align-items: center; }
.pill-secure .icon::after { content: ""; width: 6px; height: 8px; border: 2px solid white; border-radius: 4px; border-bottom: none; transform: translateY(-2px); }
.asterisk { position: absolute; left: 10%; top: 210px; width: 30px; height: 30px; background-image: url('data:image/svg+xml;utf8,<svg viewBox="0 0 24 24" stroke="black" stroke-width="2" stroke-linecap="round" xmlns="http://www.w3.org/2000/svg"><line x1="12" y1="2" x2="12" y2="22"/><line x1="2" y1="12" x2="22" y2="12"/><line x1="4.93" y1="4.93" x2="19.07" y2="19.07"/><line x1="4.93" y1="19.07" x2="19.07" y2="4.93"/></svg>'); opacity: 0.8; z-index: 0; }

.bottom-timeline { margin-top: auto; position: relative; padding-top: 32px; }
/* Line runs into the green end cap; both share one centre line */
.timeline-track { display: flex; align-items: center; gap: 14px; margin-bottom: 24px; }
.timeline-line { flex: 1; min-width: 0; height: 1px; background-color: #d4d3cf; position: relative; }
.timeline-line::after { content: ""; position: absolute; right: 0; top: -4px; width: 7px; height: 7px; border-top: 1.5px solid #bdbcb7; border-right: 1.5px solid #bdbcb7; transform: rotate(45deg); }
.timeline-nodes { position: absolute; top: -4px; left: 0; display: flex; gap: 20px; }
.timeline-nodes span { width: 8px; height: 8px; background-color: var(--brand-dark); }
.timeline-nodes span:nth-child(2) { transform: translateY(-4px); }
.timeline-vertical { position: absolute; top: calc(32px + 48px - 30px); right: calc(96px + 22%); width: 1px; height: 60px; background-color: #d4d3cf; }
.bottom-text-row { display: flex; justify-content: space-between; align-items: flex-start; gap: 20px; }
.bottom-text-left { max-width: 420px; }
.bottom-text-left h3 { font-size: 26px; font-weight: 700; margin-bottom: 10px; letter-spacing: -0.6px; }
.bottom-text-left h3 em { font-family: var(--serif); font-style: italic; font-weight: 400; }
.bottom-text-left p { font-size: 14px; color: var(--text-gray); line-height: 1.55; }
.editors-choice { display: flex; flex-direction: column; align-items: center; gap: 8px; font-size: 10px; font-weight: 700; letter-spacing: 1px; line-height: 1.25; text-align: center; color: var(--brand-dark); }
.editors-choice-icon { display: flex; gap: 2px; height: 24px; }
.editors-choice-icon div { width: 6px; background: var(--text-dark); border-radius: 2px; }
.editors-choice-icon div:nth-child(1) { height: 16px; align-self: flex-end; }
.editors-choice-icon div:nth-child(2) { height: 24px; }
.editors-choice-icon div:nth-child(3) { height: 12px; align-self: flex-end; }
.bg-green-blob { flex: none; width: 82px; height: 96px; border-radius: 22px; display: flex; align-items: center; justify-content: center; background: linear-gradient(160deg, #b9efc4 0%, #9fe5b0 100%); box-shadow: var(--clay-shadow-green); border: 1px solid rgba(255,255,255,0.7); }
body.is-business .bg-green-blob { background: linear-gradient(160deg, #cfe0ff 0%, #b3ccff 100%); box-shadow: 8px 12px 20px rgba(47,111,224,0.2), inset 2px 2px 6px rgba(255,255,255,0.6), inset -3px -3px 8px rgba(0,0,0,0.08); }

/* ================= Sections ================= */
section { padding: 130px 0 0; position: relative; }
.section-head { display: flex; justify-content: space-between; align-items: flex-end; gap: 40px; margin-bottom: 48px; }
.eyebrow { display: inline-flex; align-items: center; gap: 10px; font-size: 12px; font-weight: 700; letter-spacing: 1.5px; text-transform: uppercase; color: var(--text-gray); margin-bottom: 18px; }
.eyebrow::before { content: ""; width: 8px; height: 8px; border-radius: 50%; background: #6ee86e; box-shadow: 0 0 0 4px rgba(110,232,110,0.18), 0 0 8px #6ee86e, 0 0 16px rgba(110,232,110,0.55); animation: led-blink 2.4s ease-in-out infinite; }
h2 { font-size: 60px; font-weight: 700; line-height: 1.02; letter-spacing: -2.4px; max-width: 700px; }
h2 em { font-family: var(--serif); font-style: italic; font-weight: 400; letter-spacing: -1.2px; }
.section-sub { font-size: 16px; color: var(--text-gray); line-height: 1.6; max-width: 380px; }

/* Quick links */
.quick { padding-top: 96px; }
.quick-row { display: grid; grid-template-columns: repeat(6, 1fr); gap: 12px; }
.quick-link { background: #fff; border: 1px solid var(--hairline); border-radius: 22px; padding: 20px; text-decoration: none; display: flex; flex-direction: column; gap: 28px; position: relative; overflow: hidden; transition: border-color 0.3s; }
.quick-link:hover { border-color: transparent; }
.quick-link::before { content: ""; position: absolute; inset: 0; background: var(--brand-dark); transform: translateY(101%); transition: transform 0.45s cubic-bezier(.2,.8,.2,1); z-index: 0; border-radius: inherit; }
.quick-link:hover::before { transform: translateY(0); }
.quick-link > * { position: relative; z-index: 1; transition: color 0.3s; }
.quick-link:hover { color: #fff; }
.ql-top { display: flex; justify-content: space-between; align-items: center; }
.ql-icon { width: 40px; height: 40px; border-radius: 12px; display: flex; align-items: center; justify-content: center; background: var(--clay-light); color: var(--text-dark); transition: background 0.3s, color 0.3s; }
.ql-icon svg { width: 20px; height: 20px; }
.quick-link:hover .ql-icon { background: var(--brand-green); color: var(--brand-dark); }
.ql-arrow { width: 16px; height: 16px; opacity: 0.4; transition: transform 0.35s, opacity 0.3s; }
.quick-link:hover .ql-arrow { transform: rotate(-45deg); opacity: 1; }
.ql-text { font-size: 15px; font-weight: 600; letter-spacing: -0.2px; }

/* Dotted-arrow button (adapted from Uiverse.io by vinodjangid07) */
.btn-dots { --btn-bg: #1d2129; --btn-fg: #fff; --btn-accent: #f59aff; --btn-dot: #1d2129;
  display: inline-flex; align-items: center; justify-content: space-between; gap: 0; padding: 0;
  background: var(--btn-bg); color: var(--btn-fg); border-radius: 40px; border: none; cursor: pointer;
  box-shadow: 0 5px 10px #bebebe; min-width: 170px; text-decoration: none; }
.btn-dots .btn-dots-text { flex: 1; display: flex; align-items: center; justify-content: center; padding: 0 20px 0 26px;
  font-size: 15px; font-weight: 600; letter-spacing: 0.6px; white-space: nowrap; }
.btn-dots .btn-dots-icon { flex: none; width: 51px; height: 51px; border-radius: 50%; background: var(--btn-accent);
  border: 3px solid var(--btn-bg); display: flex; align-items: center; justify-content: center; overflow: hidden; }
.btn-dots .btn-dots-icon svg { fill: var(--btn-dot); transition-duration: 1.5s; }
.btn-dots:hover .btn-dots-icon svg, .btn-dots:focus-visible .btn-dots-icon svg { animation: btn-dots-arrow 1s linear infinite; }
.btn-dots:focus-visible { outline: 2px solid var(--btn-accent); outline-offset: 3px; }
@keyframes btn-dots-arrow { 0% { opacity: 0; margin-left: 0; } 100% { opacity: 1; margin-left: 10px; } }
/* Light backgrounds: softer shadow on the warm page */
.hero .btn-dots, .s2 .btn-dots, .s3 .btn-dots { box-shadow: 0 6px 14px rgba(17,19,23,0.18), 0 2px 4px rgba(17,19,23,0.08); }
/* Dark sections: invert to a light pill */
.btn-dots.on-dark, .s1 .btn-dots.on-dark, .ballot .btn-dots.on-dark { --btn-bg: #ffffff; --btn-fg: #16191e; --btn-dot: #16191e;
  background: var(--btn-bg); color: var(--btn-fg); box-shadow: 0 8px 24px rgba(0,0,0,0.35); }
@media (max-width: 720px) {
  .btn-dots .btn-dots-text { font-size: 14px; padding: 0 16px 0 22px; }
  .btn-dots .btn-dots-icon { width: 47px; height: 47px; }
}
@media (prefers-reduced-motion: reduce) {
  .btn-dots:hover .btn-dots-icon svg, .btn-dots:focus-visible .btn-dots-icon svg { animation: none; }
}

/* ===== Personal / Business mode ===== */
body:not(.is-business) [data-for="business"], body.is-business [data-for="personal"] { display: none !important; }
body.is-business { --brand-purple-deep: #2f6fe0; }
body.is-business .ambient span:nth-child(1) { background: rgba(47,111,224,0.22); }
body.is-business .ambient span:nth-child(3) { background: rgba(120,170,255,0.2); }
.ambient span { transition: background 0.8s ease; }
h1 em { transition: color 0.6s ease; }
body.is-business .hero-badge-tag { color: #9cc0ff; }
body.is-business .hero-badge-tag::before { background: #5b9bff; box-shadow: 0 0 6px #5b9bff; }
body.is-business .btn-dots { --btn-accent: #9cc0ff; }
body.is-business .eyebrow::before { background: #5b9bff; box-shadow: 0 0 0 4px rgba(91,155,255,0.18), 0 0 8px #5b9bff, 0 0 16px rgba(91,155,255,0.55); }
.mode-toast-wrap { position: fixed; left: 0; right: 0; bottom: 24px; z-index: 300; display: flex; justify-content: center; pointer-events: none; padding: 0 16px; }
.mode-toast { background: var(--brand-dark); color: #fff; font-size: 13px; font-weight: 600; padding: 12px 18px 12px 14px; border-radius: 16px; box-shadow: 0 16px 40px rgba(0,0,0,0.25); display: flex; align-items: center; gap: 10px; opacity: 0; pointer-events: none; white-space: nowrap; }
.mode-toast i { width: 8px; height: 8px; border-radius: 50%; background: #6ee86e; box-shadow: 0 0 8px #6ee86e; }
body.is-business .mode-toast i { background: #5b9bff; box-shadow: 0 0 8px #5b9bff; }

/* ===== FAQ ===== */
.faq-wrap { display: grid; grid-template-columns: 1fr 1.35fr; gap: 64px; align-items: start; }
.faq-intro { position: sticky; top: 120px; }
.faq-intro .section-sub { margin-top: 20px; }
.faq-contact { display: inline-flex; align-items: center; gap: 10px; margin-top: 28px; font-size: 14px; font-weight: 600; text-decoration: none; }
.faq-contact .c { width: 36px; height: 36px; border-radius: 50%; background: var(--brand-dark); color: var(--brand-green); display: flex; align-items: center; justify-content: center; }
.faq-contact .c svg { width: 16px; height: 16px; }
.faq-contact:hover { text-decoration: underline; text-underline-offset: 4px; }
.faq-list { display: flex; flex-direction: column; gap: 10px; }
.faq-item { background: #fff; border: 1px solid var(--hairline); border-radius: 22px; transition: box-shadow 0.3s, border-color 0.3s; }
.faq-item.open { box-shadow: var(--soft-shadow); border-color: transparent; }
.faq-q { width: 100%; background: none; border: none; text-align: left; padding: 22px 22px 22px 26px; font-size: 17px; font-weight: 600; letter-spacing: -0.2px; color: var(--text-dark); display: flex; justify-content: space-between; align-items: center; gap: 20px; cursor: pointer; border-radius: 22px; }
.faq-q:focus-visible { outline: 2px solid var(--brand-purple-deep); outline-offset: 2px; }
.faq-plus { flex: none; width: 34px; height: 34px; border-radius: 50%; background: var(--clay-light); position: relative; transition: transform 0.35s cubic-bezier(.2,.8,.2,1), background 0.3s; }
.faq-plus::before, .faq-plus::after { content: ""; position: absolute; left: 50%; top: 50%; width: 12px; height: 2px; background: var(--brand-dark); border-radius: 2px; transform: translate(-50%, -50%); transition: background 0.3s; }
.faq-plus::after { transform: translate(-50%, -50%) rotate(90deg); }
.faq-item.open .faq-plus { transform: rotate(45deg); background: var(--brand-dark); }
.faq-item.open .faq-plus::before, .faq-item.open .faq-plus::after { background: var(--brand-green); }
.faq-a { height: 0; overflow: hidden; }
.faq-a p { padding: 0 72px 24px 26px; font-size: 15px; color: var(--text-gray); line-height: 1.65; }
.faq-a a { color: var(--text-dark); font-weight: 600; text-underline-offset: 3px; }

/* Footer: logo in "Follow Meridian" */
.follow h3 { display: flex; align-items: center; gap: 14px; flex-wrap: wrap; }
.follow-logo { display: inline-flex; color: var(--text-dark); font-size: 34px; }

@media (max-width: 1024px) {
  .faq-wrap { grid-template-columns: 1fr; gap: 32px; }
  .faq-intro { position: static; }
}
@media (max-width: 720px) {
  .faq-q { font-size: 16px; padding: 18px 16px 18px 20px; }
  .faq-a p { padding: 0 20px 20px 20px; }
  .follow-logo { font-size: 28px; }
  .mode-toast-wrap { bottom: 16px; }
}

/* ===== Header + description pairing (glow accent adapted from the illuminated-text reference) ===== */
.glow-filters { position: absolute; width: 0; height: 0; overflow: hidden; pointer-events: none; }
/* Header accents: brand gradient fill + soft light-theme glow */
h1 em, h2 em, .slide h3 em, .bottom-text-left h3 em {
  background: linear-gradient(0deg, #5a49b0 0%, #8f7ee0 55%, #a596ea 100%);
  -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent;
  -webkit-box-decoration-break: clone; box-decoration-break: clone;
  filter: url(#glow-light); padding: 0 0.06em; margin: 0 -0.06em;
}
body.is-business h1 em, body.is-business h2 em, body.is-business .bottom-text-left h3 em {
  background-image: linear-gradient(0deg, #1f5ed6 0%, #3f7ff0 55%, #6d9cf6 100%); filter: url(#glow-light-biz);
}
/* Dark surfaces keep the warm original glow */
.s1 h3 em { background-image: linear-gradient(0deg, #dfe5ee 0%, #fffaf6 50%); filter: url(#glow-warm); }
.ballot-copy h4 em { background: linear-gradient(0deg, #8fdea0 0%, #d9f7df 100%); -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; filter: url(#glow-green); padding: 0 0.06em; }
/* Hero accent eases in like the reference */
h1 em { display: inline-block; animation: accent-in 1.2s ease-out both; animation-delay: 0.9s; }
@keyframes accent-in { 0% { scale: 0.985; opacity: 0.85; } 100% { scale: 1; opacity: 1; } }

/* Descriptions: soft graded grey with one highlighted phrase */
.hero-sub, .section-sub, .travel-copy p, .bottom-text-left p, .s2 p, .s3 p {
  background: linear-gradient(0deg, #4c5158 0%, #7a7f87 100%);
  -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; font-weight: 500;
}
.hl { -webkit-text-fill-color: var(--text-dark); color: var(--text-dark); font-weight: 700; }
/* Dark surfaces use the reference's original greys */
.s1 p, .ballot-copy p { background: linear-gradient(0deg, #86868b 0%, #bdc2c9 100%); -webkit-background-clip: text; background-clip: text; -webkit-text-fill-color: transparent; font-weight: 500; }
.slide p { opacity: 1; }
.s1 .hl, .ballot-copy .hl { -webkit-text-fill-color: #f1e9df; color: #f1e9df; }
@media (prefers-reduced-motion: reduce) { h1 em { animation: none; } }

/* Featured slider */
.slider { position: relative; border-radius: 40px; overflow: hidden; height: 600px; box-shadow: var(--soft-shadow); }
.slide { position: absolute; inset: 0; display: grid; grid-template-columns: 1fr 1.15fr; align-items: center; padding: 64px; gap: 40px; opacity: 0; visibility: hidden; }
.slide.active { opacity: 1; visibility: visible; }
.slide.s1 { background: radial-gradient(120% 120% at 85% 20%, #2b2442 0%, var(--brand-dark) 55%); color: #fff; }
.slide.s2 { background: radial-gradient(120% 120% at 80% 30%, #ddd5fb 0%, #c7bbef 60%, #b4a6e6 100%); }
.slide.s3 { background: radial-gradient(120% 120% at 80% 20%, #d9f5df 0%, #b8eac4 55%, #9fdfaf 100%); }
.slide-copy { position: relative; z-index: 2; max-width: 460px; }
.slide-tag { display: inline-block; font-size: 11px; font-weight: 700; letter-spacing: 1.5px; padding: 7px 12px; border-radius: 10px; margin-bottom: 22px; background: rgba(255,255,255,0.12); border: 1px solid rgba(255,255,255,0.18); }
.s2 .slide-tag, .s3 .slide-tag { background: rgba(255,255,255,0.55); border-color: rgba(255,255,255,0.8); }
.slide h3 { font-size: 56px; font-weight: 700; line-height: 1.02; letter-spacing: -2.2px; margin-bottom: 18px; }
.slide h3 em { font-family: var(--serif); font-style: italic; font-weight: 400; letter-spacing: -1px; }
.slide p { font-size: 16px; line-height: 1.6; opacity: 0.72; margin-bottom: 32px; }
.s1 .btn-primary { background: #fff; color: var(--brand-dark); box-shadow: 0 10px 30px rgba(0,0,0,0.3); }
.slide-visual { position: relative; height: 100%; display: flex; align-items: center; justify-content: center; }

.slider-ui { position: absolute; left: 64px; right: 64px; bottom: 32px; display: flex; align-items: center; justify-content: space-between; z-index: 5; gap: 20px; }
.slider-ui .count { font-size: 13px; font-weight: 600; letter-spacing: 1px; font-variant-numeric: tabular-nums; }
.slider-ui .progress { flex: 1; height: 2px; background: rgba(127,127,127,0.25); border-radius: 2px; overflow: hidden; max-width: 320px; }
.slider-ui .progress i { display: block; height: 100%; width: 0; background: currentColor; }
.slider-ui .ctrls { display: flex; gap: 8px; }
.slider-ui button { width: 44px; height: 44px; border-radius: 50%; border: 1px solid rgba(127,127,127,0.35); background: rgba(255,255,255,0.08); color: inherit; cursor: pointer; display: flex; align-items: center; justify-content: center; backdrop-filter: blur(8px); transition: background 0.25s; }
.slider-ui button:hover { background: rgba(127,127,127,0.18); }
.slider-ui button:focus-visible { outline: 2px solid currentColor; outline-offset: 2px; }
.slider-ui svg { width: 16px; height: 16px; }
.slider.dark-ui .slider-ui { color: #fff; }
.slider:not(.dark-ui) .slider-ui { color: var(--brand-dark); }

/* CSS devices */
.laptop { position: relative; width: 460px; max-width: 100%; perspective: 1400px; }
.laptop .lid { position: relative; width: 88%; margin: 0 auto; aspect-ratio: 3/2; border-radius: 16px 16px 6px 6px; background: #1a1b1f; padding: 10px; box-shadow: 0 30px 60px rgba(0,0,0,0.35), inset 0 0 0 1.5px rgba(255,255,255,0.12); transform-origin: bottom center; }
.laptop .screen { width: 100%; height: 100%; border-radius: 8px; overflow: hidden; position: relative; background: #0d0e12; }
.laptop .screen .bloom { position: absolute; inset: -20%; background: radial-gradient(40% 50% at 30% 60%, #8fdea0 0%, transparent 70%), radial-gradient(50% 60% at 70% 40%, #9d8cdc 0%, transparent 70%), radial-gradient(30% 40% at 55% 75%, #f2c7a1 0%, transparent 70%); filter: blur(14px); opacity: 0.95; }
.laptop .screen .taskbar { position: absolute; left: 50%; bottom: 8px; transform: translateX(-50%); display: flex; gap: 5px; padding: 5px 8px; border-radius: 8px; background: rgba(255,255,255,0.18); backdrop-filter: blur(6px); }
.laptop .screen .taskbar i { width: 10px; height: 10px; border-radius: 3px; background: rgba(255,255,255,0.75); }
.laptop .base { width: 100%; height: 14px; background: linear-gradient(180deg, #d9d8de 0%, #a9a8b0 100%); border-radius: 2px 2px 14px 14px; position: relative; box-shadow: 0 24px 40px -10px rgba(0,0,0,0.45); }
.laptop .base::before { content: ""; position: absolute; left: 50%; top: 0; transform: translateX(-50%); width: 18%; height: 5px; background: rgba(0,0,0,0.18); border-radius: 0 0 6px 6px; }
.laptop.light .lid { background: #e9e8ee; box-shadow: 0 30px 60px rgba(60,40,120,0.25), inset 0 0 0 1.5px rgba(255,255,255,0.8); }
.laptop .glow { position: absolute; left: 10%; right: 10%; top: 10%; bottom: 0; background: radial-gradient(closest-side, rgba(157,140,220,0.55), transparent); filter: blur(40px); z-index: -1; }

.tablet-wrap { position: relative; width: 420px; max-width: 100%; }
.tablet { width: 100%; aspect-ratio: 3/2; border-radius: 22px; background: #2a2b31; padding: 12px; box-shadow: 0 40px 70px rgba(60,40,120,0.35), inset 0 0 0 2px rgba(255,255,255,0.12); transform: rotate(-6deg); }
.tablet .screen { width: 100%; height: 100%; border-radius: 12px; overflow: hidden; position: relative; background: linear-gradient(135deg, #f7f4ff 0%, #e4dcff 100%); }
.tablet .screen .bloom { position: absolute; inset: -20%; background: radial-gradient(45% 55% at 65% 45%, #9d8cdc 0%, transparent 70%), radial-gradient(35% 45% at 35% 65%, #8fdea0 0%, transparent 70%); filter: blur(16px); }
.tablet .pen { position: absolute; right: -18px; top: 18%; width: 10px; height: 64%; border-radius: 6px; background: linear-gradient(90deg, #2a2b31, #4a4b52); box-shadow: 4px 10px 20px rgba(0,0,0,0.25); transform: rotate(-6deg); }
.tablet .kb { width: 92%; margin: -10px auto 0; height: 34px; border-radius: 0 0 14px 14px; background: linear-gradient(180deg, #6c5bbd, #5a4aa8); transform: rotate(-6deg) translateY(16px) skewX(-8deg); box-shadow: 0 18px 30px rgba(60,40,120,0.3); }

.power-stack { position: relative; width: 480px; height: 360px; max-width: 100%; }
.power-stack .laptop { position: absolute; width: 300px; }
.power-stack .laptop:nth-child(1) { left: 0; top: 70px; transform: scale(0.82) rotate(-6deg); opacity: 0.9; }
.power-stack .laptop:nth-child(2) { right: 0; top: 70px; transform: scale(0.82) rotate(6deg); opacity: 0.9; }
.power-stack .laptop:nth-child(3) { left: 50%; top: 40px; margin-left: -150px; z-index: 2; }
.chip-badge { position: absolute; z-index: 3; left: 50%; bottom: 10px; transform: translateX(-50%); background: var(--brand-dark); color: #fff; border-radius: 18px; padding: 10px 16px 10px 10px; display: flex; gap: 10px; align-items: center; font-size: 13px; font-weight: 600; box-shadow: var(--clay-shadow-dark); white-space: nowrap; }
.chip-badge .ci { width: 30px; height: 30px; border-radius: 9px; background: var(--brand-green); display: flex; align-items: center; justify-content: center; color: var(--brand-dark); }
.chip-badge .ci svg { width: 16px; height: 16px; }

/* Travel light banner */
.travel { display: grid; grid-template-columns: 1fr 1fr; gap: 0; border-radius: 40px; overflow: hidden; background: #fff; border: 1px solid var(--hairline); box-shadow: var(--soft-shadow); }
.travel-copy { padding: 72px 64px; display: flex; flex-direction: column; justify-content: center; }
.travel-copy p { font-size: 17px; color: var(--text-gray); line-height: 1.6; margin: 20px 0 36px; max-width: 420px; }
.travel-specs { display: flex; gap: 32px; margin-bottom: 40px; flex-wrap: wrap; }
.spec small { display: block; font-size: 11px; font-weight: 700; letter-spacing: 1.2px; color: var(--text-gray); margin-bottom: 6px; text-transform: uppercase; }
.spec strong { font-family: var(--serif); font-style: italic; font-weight: 400; font-size: 26px; }
.travel-visual { position: relative; background: linear-gradient(160deg, #efeaff 0%, #e6f7ea 100%); display: flex; align-items: center; justify-content: center; padding: 64px 40px; min-height: 520px; overflow: hidden; }
.travel-visual .ring { position: absolute; border-radius: 50%; border: 1px solid rgba(108,91,189,0.18); }
.travel-visual .ring.r1 { width: 380px; height: 380px; }
.travel-visual .ring.r2 { width: 560px; height: 560px; }
.travel-visual .ring.r3 { width: 740px; height: 740px; }
.travel-visual .laptop { width: 420px; z-index: 2; }
.feather { position: absolute; z-index: 3; top: 56px; right: 48px; background: #fff; padding: 10px 16px; border-radius: 16px; font-size: 13px; font-weight: 600; box-shadow: var(--soft-shadow); display: flex; align-items: center; gap: 8px; }
.feather i { width: 8px; height: 8px; border-radius: 50%; background: var(--brand-green); box-shadow: 0 0 0 4px rgba(143,222,160,0.3); }

/* AI articles */
.articles { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
.article { background: #fff; border: 1px solid var(--hairline); border-radius: 32px; overflow: hidden; display: flex; flex-direction: column; text-decoration: none; position: relative; transition: box-shadow 0.4s; }
.article:hover { box-shadow: var(--soft-shadow); }
.article::after { content: ""; position: absolute; inset: 0; pointer-events: none; border-radius: inherit; background: radial-gradient(360px circle at var(--mx, 50%) var(--my, 50%), rgba(157,140,220,0.12), transparent 60%); opacity: 0; transition: opacity 0.3s; }
.article:hover::after { opacity: 1; }
.art-visual { height: 230px; position: relative; overflow: hidden; margin: 8px; border-radius: 26px; }
.art-body { padding: 18px 28px 30px; display: flex; flex-direction: column; flex: 1; }
.art-cat { font-size: 11px; font-weight: 700; letter-spacing: 1.4px; color: var(--text-gray); text-transform: uppercase; margin-bottom: 12px; }
.article h4 { font-size: 22px; font-weight: 700; letter-spacing: -0.5px; line-height: 1.2; margin-bottom: 12px; }
.article p { font-size: 14px; color: var(--text-gray); line-height: 1.6; flex: 1; margin-bottom: 24px; }
.art-link { font-size: 14px; font-weight: 600; display: inline-flex; align-items: center; gap: 10px; }
.art-link .c { width: 34px; height: 34px; border-radius: 50%; border: 1px solid var(--hairline); display: flex; align-items: center; justify-content: center; transition: background 0.3s, color 0.3s, transform 0.35s; }
.art-link svg { width: 14px; height: 14px; }
.article:hover .art-link .c { background: var(--brand-dark); color: #fff; transform: rotate(-45deg); }

.v-gov { background: var(--brand-dark); display: flex; align-items: center; justify-content: center; }
.v-gov .ring { position: absolute; border-radius: 50%; border: 1.5px solid rgba(143,222,160,0.35); }
.v-gov .core { width: 64px; height: 64px; border-radius: 20px; background: var(--brand-green); box-shadow: var(--clay-shadow-green); display: flex; align-items: center; justify-content: center; z-index: 2; color: var(--brand-dark); }
.v-gov .core svg { width: 28px; height: 28px; }
.v-gov .sat { position: absolute; width: 14px; height: 14px; border-radius: 50%; background: var(--brand-purple); box-shadow: 0 0 16px rgba(157,140,220,0.8); }
.v-trade { background: linear-gradient(135deg, #c9bdf0, #a898e0); }
.v-trade svg { position: absolute; inset: 0; width: 100%; height: 100%; }
.v-nature { background: linear-gradient(160deg, #d6f2dc, #a7e2b5); display: flex; align-items: flex-end; justify-content: center; gap: 10px; padding-bottom: 0; }
.v-nature .dc { width: 46px; background: var(--brand-dark); border-radius: 10px 10px 0 0; position: relative; box-shadow: var(--clay-shadow-dark); }
.v-nature .dc::before { content: ""; position: absolute; left: 10px; right: 10px; top: 14px; height: 40%; background: repeating-linear-gradient(180deg, rgba(143,222,160,0.8) 0 3px, transparent 3px 10px); }
.v-nature .leaf { position: absolute; width: 60px; height: 60px; background: #5fbf78; border-radius: 0 60% 0 60%; opacity: 0.9; }

/* Ballot banner */
.ballot { display: flex; flex-direction: column; gap: 24px; background: var(--brand-dark); color: #fff; border-radius: 32px; padding: 16px 16px 28px; position: relative; overflow: hidden; }
.ballot-row { display: flex; align-items: center; gap: 28px; padding: 0 12px 0 16px; width: 100%; }
.ballot::before { content: ""; position: absolute; right: -80px; top: -120px; width: 320px; height: 320px; background: radial-gradient(closest-side, rgba(143,222,160,0.35), transparent); }
.ballot-icon { flex: none; width: 64px; height: 64px; border-radius: 20px; background: var(--brand-green); color: var(--brand-dark); display: flex; align-items: center; justify-content: center; box-shadow: var(--clay-shadow-green); }
.ballot-icon svg { width: 28px; height: 28px; }
.ballot-copy { flex: 1; position: relative; }
.ballot-copy h4 { font-size: 24px; font-weight: 700; letter-spacing: -0.5px; margin-bottom: 4px; }
.ballot-copy h4 em { font-family: var(--serif); font-style: italic; font-weight: 400; color: var(--brand-green); }
.ballot-copy p { font-size: 14px; color: rgba(255,255,255,0.65); }
.ballot .btn-primary { background: #fff; color: var(--brand-dark); box-shadow: none; position: relative; white-space: nowrap; }

/* Follow + footer */
.follow { display: flex; justify-content: space-between; align-items: center; gap: 24px; padding: 40px 0; border-bottom: 1px solid var(--hairline); flex-wrap: wrap; }
.follow h3 { font-size: 34px; font-weight: 700; letter-spacing: -1.2px; }
.follow h3 em { font-family: var(--serif); font-style: italic; font-weight: 400; }
.socials { display: flex; gap: 10px; flex-wrap: wrap; }
.socials a { width: 48px; height: 48px; border-radius: 16px; background: #fff; border: 1px solid var(--hairline); display: flex; align-items: center; justify-content: center; color: var(--brand-dark); transition: background 0.25s, color 0.25s, transform 0.25s; }
.socials a:hover { background: var(--brand-dark); color: var(--brand-green); transform: translateY(-3px); }
.socials svg { width: 18px; height: 18px; }

footer { margin-top: 130px; }
.footer-grid { display: grid; grid-template-columns: repeat(6, 1fr); gap: 32px; padding: 56px 0; }
.footer-col h5 { font-size: 13px; font-weight: 700; margin-bottom: 18px; letter-spacing: -0.1px; }
.footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 11px; }
.footer-col a { font-size: 13px; color: var(--text-gray); text-decoration: none; transition: color 0.25s; line-height: 1.35; }
.footer-col a:hover { color: var(--text-dark); }
.footer-bottom { display: flex; justify-content: space-between; align-items: center; padding: 24px 0 40px; border-top: 1px solid var(--hairline); font-size: 12px; color: var(--text-gray); gap: 16px 28px; flex-wrap: wrap; }
.fb-left, .fb-right { display: flex; align-items: center; gap: 22px; flex-wrap: wrap; }
.footer-bottom a { text-decoration: none; display: inline-flex; align-items: center; gap: 8px; }
.footer-bottom a:hover { color: var(--text-dark); }
.footer-bottom a svg { width: 16px; height: 16px; }
.privacy-toggle { width: 30px; height: 14px; border-radius: 8px; background: #2f6fe0; position: relative; display: inline-block; }
.privacy-toggle::after { content: "✓"; position: absolute; left: 2px; top: 1px; width: 12px; height: 12px; border-radius: 50%; background: #fff; color: #2f6fe0; font-size: 8px; font-weight: 800; display: flex; align-items: center; justify-content: center; }
.footnote { font-size: 11px; color: #9a9ea5; line-height: 1.6; padding-bottom: 32px; }
.footer-logo { color: var(--text-dark); font-size: 16px; display: inline-flex; }

/* ================= Responsive ================= */
@media (max-width: 1180px) {
  .nav-links { gap: 22px; }
  .quick-row { grid-template-columns: repeat(3, 1fr); }
  .footer-grid { grid-template-columns: repeat(3, 1fr); }
}
@media (max-width: 1024px) {
  .nav-links { display: none; position: absolute; top: calc(100% + 10px); left: 0; right: 0; flex-direction: column; gap: 2px; background: rgba(255,255,255,0.96); backdrop-filter: blur(18px); padding: 12px; border-radius: 22px; box-shadow: var(--soft-shadow); border: 1px solid #fff; }
  .nav-links.open { display: flex; }
  .nav-links a { display: block; padding: 12px 14px; font-size: 16px; color: var(--text-dark); }
  .menu-toggle { display: flex; }
  .hero { flex-direction: column; min-height: auto; }
  .left-col { max-width: 100%; }
  .right-col { min-height: 660px; }
  .slider { height: auto; }
  /* minmax(0, 1fr): a bare 1fr track grows to the laptop's 460px min-content and the slider clips it */
  .slide { position: relative; grid-template-columns: minmax(0, 1fr); padding: 48px 40px 110px; display: none; }
  .slide.active { display: grid; }
  .slide-visual { height: 320px; }
  .slider-ui { left: 40px; right: 40px; }
  .travel { grid-template-columns: 1fr; }
  .travel-visual { min-height: 400px; }
  .articles { grid-template-columns: 1fr 1fr; }
  .articles .article:last-child { grid-column: span 2; }
}
@media (max-width: 720px) {
  .container { padding: 12px 16px; }
  nav { padding: 10px 10px 10px 16px; top: 10px; gap: 10px; }
  .nav-left { gap: 14px; }
  .logo { font-size: 19px; }
  .segmented button { padding: 7px 10px; font-size: 12px; }
  .icon-btn.search { display: none; }
  .hero { margin-top: 40px; gap: 40px; }
  h1 { font-size: 56px; letter-spacing: -2.2px; }
  .hero-sub { font-size: 16px; }
  .cta-group { margin-bottom: 40px; }
  .dots-vert { display: none; }
  .right-col { min-height: 0; }
  .chart-area { height: 360px; margin-top: 60px; }
  .pill-dark { left: 0; bottom: 18px; }
  .pill-secure { right: 4%; bottom: 0; }
  .sticker { width: 78px; height: 78px; font-size: 9px; right: 0; }
  .sticker::after { bottom: 16px; width: 30px; }
  .bottom-timeline { padding-top: 40px; }
  .timeline-vertical { top: calc(40px + 40px - 26px); height: 52px; right: calc(80px + 18%); }
  .bg-green-blob { width: 70px; height: 80px; border-radius: 18px; }
  .bottom-text-left h3 { font-size: 23px; }
  section { padding-top: 96px; }
  .quick { padding-top: 72px; }
  .section-head { flex-direction: column; align-items: flex-start; gap: 18px; margin-bottom: 36px; }
  h2 { font-size: 40px; letter-spacing: -1.4px; }
  .quick-row { grid-template-columns: 1fr 1fr; }
  .slider { border-radius: 28px; }
  .slide { padding: 36px 24px 104px; }
  .slide h3 { font-size: 40px; letter-spacing: -1.4px; }
  .slide-visual { height: 260px; }
  .slider-ui { left: 24px; right: 24px; bottom: 24px; }
  .slider-ui .progress { display: none; }
  .power-stack { height: 260px; }
  .power-stack .laptop { width: 210px; }
  .power-stack .laptop:nth-child(3) { margin-left: -105px; }
  .travel { border-radius: 28px; }
  .travel-copy { padding: 40px 24px; }
  .travel-visual { min-height: 320px; padding: 40px 20px; }
  .feather { top: 20px; right: 20px; }
  .articles { grid-template-columns: 1fr; }
  .articles .article:last-child { grid-column: auto; }
  .ballot { padding: 12px 12px 28px; }
  .ballot-row { flex-direction: column; align-items: flex-start; padding: 0 12px; gap: 20px; }
  .follow h3 { font-size: 28px; }
  .footer-grid { grid-template-columns: 1fr 1fr; gap: 36px 20px; }
}

/* ===== Type pairing: Bricolage Grotesque headers, Fraunces italic accents, Instrument Sans descriptions ===== */
h1, h2, .slide h3, .bottom-text-left h3, .ballot-copy h4, .article h4, .follow h3, .faq-q {
  font-family: var(--display); font-optical-sizing: auto;
}
h1 { font-weight: 700; letter-spacing: -0.045em; line-height: 0.96; }
h2 { font-weight: 680; letter-spacing: -0.04em; line-height: 1.02; }
.slide h3 { font-weight: 680; letter-spacing: -0.04em; }
.bottom-text-left h3, .ballot-copy h4, .article h4 { font-weight: 650; letter-spacing: -0.025em; }
.follow h3 { font-weight: 680; letter-spacing: -0.035em; }
.faq-q { font-weight: 600; letter-spacing: -0.015em; }
/* Accent words: Fraunces italic, set a touch lighter so the glow carries them */
h1 em, h2 em, .slide h3 em, .bottom-text-left h3 em, .ballot-copy h4 em, .spec strong {
  font-family: var(--serif); font-style: italic; font-weight: 380; font-optical-sizing: auto; letter-spacing: -0.025em;
}
h1 em { font-weight: 360; letter-spacing: -0.035em; }
/* Descriptions */
.hero-sub, .section-sub, .slide p, .travel-copy p, .bottom-text-left p, .ballot-copy p, .article p, .faq-a p {
  font-family: var(--text); letter-spacing: 0.003em;
}
.hl { font-family: var(--text); font-weight: 650; }
</style>
</head>
<body>
<svg class="glow-filters" aria-hidden="true" focusable="false" width="0" height="0">
  <defs>
    <filter id="glow-light" color-interpolation-filters="sRGB" x="-30%" y="-60%" width="160%" height="240%">
      <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="b2"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="6" result="b6"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="14" result="b14"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="26" result="b26"/>
      <feColorMatrix in="b2" type="matrix" values="0 0 0 0 1.000  0 0 0 0 1.000  0 0 0 0 1.000  0 0 0 0.9 0" result="c0"/>
      <feOffset in="c0" dx="0" dy="0" result="o0"/>
      <feColorMatrix in="b6" type="matrix" values="0 0 0 0 0.718  0 0 0 0 0.659  0 0 0 0 0.941  0 0 0 0.45 0" result="c1"/>
      <feOffset in="c1" dx="0" dy="1" result="o1"/>
      <feColorMatrix in="b14" type="matrix" values="0 0 0 0 0.616  0 0 0 0 0.549  0 0 0 0 0.863  0 0 0 0.32 0" result="c2"/>
      <feOffset in="c2" dx="0" dy="3" result="o2"/>
      <feColorMatrix in="b26" type="matrix" values="0 0 0 0 0.561  0 0 0 0 0.871  0 0 0 0 0.627  0 0 0 0.16 0" result="c3"/>
      <feOffset in="c3" dx="0" dy="8" result="o3"/>
      <feMerge><feMergeNode in="o0"/><feMergeNode in="o1"/><feMergeNode in="o2"/><feMergeNode in="o3"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
    <filter id="glow-light-biz" color-interpolation-filters="sRGB" x="-30%" y="-60%" width="160%" height="240%">
      <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="b2"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="6" result="b6"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="14" result="b14"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="26" result="b26"/>
      <feColorMatrix in="b2" type="matrix" values="0 0 0 0 1.000  0 0 0 0 1.000  0 0 0 0 1.000  0 0 0 0.9 0" result="c0"/>
      <feOffset in="c0" dx="0" dy="0" result="o0"/>
      <feColorMatrix in="b6" type="matrix" values="0 0 0 0 0.612  0 0 0 0 0.753  0 0 0 0 1.000  0 0 0 0.45 0" result="c1"/>
      <feOffset in="c1" dx="0" dy="1" result="o1"/>
      <feColorMatrix in="b14" type="matrix" values="0 0 0 0 0.357  0 0 0 0 0.561  0 0 0 0 0.941  0 0 0 0.3 0" result="c2"/>
      <feOffset in="c2" dx="0" dy="3" result="o2"/>
      <feColorMatrix in="b26" type="matrix" values="0 0 0 0 0.561  0 0 0 0 0.871  0 0 0 0 0.627  0 0 0 0.12 0" result="c3"/>
      <feOffset in="c3" dx="0" dy="8" result="o3"/>
      <feMerge><feMergeNode in="o0"/><feMergeNode in="o1"/><feMergeNode in="o2"/><feMergeNode in="o3"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
    <filter id="glow-warm" color-interpolation-filters="sRGB" x="-30%" y="-60%" width="160%" height="240%">
      <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="b2"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="9" result="b9"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="19" result="b19"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="30" result="b30"/>
      <feColorMatrix in="b2" type="matrix" values="0 0 0 0 1.000  0 0 0 0 0.980  0 0 0 0 0.965  0 0 0 0.75 0" result="c0"/>
      <feOffset in="c0" dx="0" dy="0" result="o0"/>
      <feColorMatrix in="b9" type="matrix" values="0 0 0 0 1.000  0 0 0 0 0.667  0 0 0 0 0.365  0 0 0 0.4 0" result="c1"/>
      <feOffset in="c1" dx="0" dy="2" result="o1"/>
      <feColorMatrix in="b19" type="matrix" values="0 0 0 0 0.816  0 0 0 0 0.494  0 0 0 0 0.263  0 0 0 0.45 0" result="c2"/>
      <feOffset in="c2" dx="0" dy="2" result="o2"/>
      <feColorMatrix in="b30" type="matrix" values="0 0 0 0 1.000  0 0 0 0 0.612  0 0 0 0 0.392  0 0 0 0.35 0" result="c3"/>
      <feOffset in="c3" dx="0" dy="2" result="o3"/>
      <feColorMatrix in="b30" type="matrix" values="0 0 0 0 0.455  0 0 0 0 0.165  0 0 0 0 0.000  0 0 0 0.5 0" result="c4"/>
      <feOffset in="c4" dx="0" dy="16" result="o4"/>
      <feMerge><feMergeNode in="o0"/><feMergeNode in="o1"/><feMergeNode in="o2"/><feMergeNode in="o3"/><feMergeNode in="o4"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
    <filter id="glow-green" color-interpolation-filters="sRGB" x="-30%" y="-60%" width="160%" height="240%">
      <feGaussianBlur in="SourceGraphic" stdDeviation="2" result="b2"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="8" result="b8"/>
      <feGaussianBlur in="SourceGraphic" stdDeviation="20" result="b20"/>
      <feColorMatrix in="b2" type="matrix" values="0 0 0 0 0.949  0 0 0 0 1.000  0 0 0 0 0.957  0 0 0 0.7 0" result="c0"/>
      <feOffset in="c0" dx="0" dy="0" result="o0"/>
      <feColorMatrix in="b8" type="matrix" values="0 0 0 0 0.561  0 0 0 0 0.871  0 0 0 0 0.627  0 0 0 0.55 0" result="c1"/>
      <feOffset in="c1" dx="0" dy="1" result="o1"/>
      <feColorMatrix in="b20" type="matrix" values="0 0 0 0 0.431  0 0 0 0 0.910  0 0 0 0 0.431  0 0 0 0.3 0" result="c2"/>
      <feOffset in="c2" dx="0" dy="3" result="o2"/>
      <feMerge><feMergeNode in="o0"/><feMergeNode in="o1"/><feMergeNode in="o2"/><feMergeNode in="SourceGraphic"/></feMerge>
    </filter>
  </defs>
</svg>
<div class="mode-toast-wrap"><div class="mode-toast" id="modeToast" role="status" aria-live="polite"><i></i><span></span></div></div>
<div class="ambient" aria-hidden="true"><span></span><span></span><span></span></div>

<div class="container">

  <nav class="gsap-nav" data-section="nav" aria-label="Main">
    <div class="nav-left">
      <a href="#" class="logo" aria-label="Meridian home" id="navLogo">
        <span class="brandmark"><svg viewBox="0 0 32 32" aria-hidden="true" focusable="false"><circle cx="16" cy="16" r="15" fill="currentColor"/><path d="M16 3.5c-5.2 3.4-5.2 21.6 0 25M16 3.5c5.2 3.4 5.2 21.6 0 25M3.5 16h25" fill="none" stroke="#f6f5f1" stroke-width="2.2" stroke-linecap="round"/><circle cx="16" cy="16" r="2.6" fill="#8fdea0"/></svg>meridian</span>
      </a>
    </div>
    <ul class="nav-links" id="navLinks">
      <li><a href="#featured">Devices</a></li>
      <li><a href="#travel">Meridian Book</a></li>
      <li><a href="#ai">Assist</a></li>
      <li><a href="#faq">Support</a></li>
      <li><a href="#ai">AI</a></li>
    </ul>
    <div class="nav-actions">
      <div class="segmented" id="segmented" data-component="mode-switch" role="group" aria-label="Audience">
        <div class="seg-thumb"></div>
        <button class="active" data-mode="personal" aria-pressed="true">Personal</button>
        <button data-mode="business" aria-pressed="false">Business</button>
      </div>
      <button class="icon-btn search" aria-label="Search">
        <svg class="search-icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="11" cy="11" r="8"></circle><line x1="21" y1="21" x2="16.65" y2="16.65"></line></svg>
      </button>
      <button class="icon-btn menu-toggle" id="menuToggle" aria-label="Open menu" aria-expanded="false" aria-controls="navLinks"><span></span></button>
    </div>
  </nav>

  <!-- ================= HERO ================= -->
  <main class="hero" data-section="hero">
    <div class="left-col">
      <div class="badge-row gsap-hero">
        <div class="hero-badge"><span class="hero-badge-tag"><span data-for="personal">NEW</span><span data-for="business">BUSINESS</span></span><span class="hero-badge-text"><span data-for="personal">Hi there, welcome to Meridian</span><span data-for="business">Welcome to Meridian for business</span></span></div>
      </div>

      <h1 class="gsap-hero"><span data-for="personal">Meridian<br>Book <em>Ultra</em></span><span data-for="business">Built for<br><em>business</em></span></h1>

      <p class="hero-sub gsap-hero" data-for="business">Get more done with Meridian Workspace, Huddle and Assist, protected by <span class="hl">Meridian Shield</span>. Find the right tools for your organization, from a team of five to five thousand.</p>
      <p class="hero-sub gsap-hero" data-for="personal">The most powerful Meridian Book yet, built around an all-new neural engine. Plus, trade in your current laptop and get <span class="hl">up to $1,000 back.**</span></p>

      <div class="cta-group gsap-hero" data-for="personal">
        <a href="#featured" class="btn-primary btn-dots"><span class="btn-dots-text">Pre-order now</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
        <a href="#faq" class="link-underline">Help me choose a laptop</a>
      </div>
      <div class="cta-group gsap-hero" data-for="business">
        <a href="#featured" class="btn-primary btn-dots"><span class="btn-dots-text">Shop for your business</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
        <a href="#faq" class="link-underline">Explore Meridian Workspace</a>
      </div>

      <div class="download-card gsap-hero float-subtle" data-component="ai-suggestions">
        <div class="dots-vert" aria-hidden="true"><span></span><span></span></div>
        <div class="download-top">
          <div class="app-icon" aria-hidden="true">
            <svg viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path d="M12 2l2.2 6.3L20.5 10.5l-6.3 2.2L12 19l-2.2-6.3L3.5 10.5l6.3-2.2z"/><path d="M19 15l.9 2.1L22 18l-2.1.9L19 21l-.9-2.1L16 18l2.1-.9z"/></svg>
          </div>
          <div class="download-text"><span>AI-powered suggestions</span><span data-for="personal">Find what you need faster</span><span data-for="business">Find the right tools for your team</span></div>
          <div class="small-purple-icon" aria-hidden="true">
            <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"></polyline></svg>
          </div>
        </div>
        <div class="chips" data-for="personal">
          <a class="chip" href="#featured"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="4" width="18" height="12" rx="2"/><line x1="2" y1="20" x2="22" y2="20"/></svg>Help me choose a laptop</a>
          <a class="chip" href="#ai"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M9 18h6M10 22h4M12 2a7 7 0 0 0-4 12.7V17h8v-2.3A7 7 0 0 0 12 2z"/></svg>Workspace tips</a>
          <a class="chip" href="#"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><circle cx="12" cy="8" r="4"/><path d="M4 21c0-4 4-6 8-6s8 2 8 6"/></svg>Sign in to my account</a>
        </div>
        <div class="chips" data-for="business">
          <a class="chip" href="#faq"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="3" width="7" height="7" rx="1.5"/><rect x="14" y="3" width="7" height="7" rx="1.5"/><rect x="3" y="14" width="7" height="7" rx="1.5"/><rect x="14" y="14" width="7" height="7" rx="1.5"/></svg>Workspace for business</a>
          <a class="chip" href="#faq"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>Meridian Shield</a>
          <a class="chip" href="#featured"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2"/></svg>Small business</a>
        </div>
      </div>
    </div>

    <div class="right-col">

      <div class="top-right-info gsap-right">
        <div class="pixel-art" aria-hidden="true"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
        <div class="info-text"><span data-for="personal">Built around an all-new<br>neural engine</span><span data-for="business">Tools for teams<br>of every size</span></div>
      </div>

      <div class="chart-area gsap-right">
        <div class="led-panel" data-component="led-metro-map">
          <div class="led-head">
            <span class="led-live"><i></i><span data-for="personal">LIVE NETWORK</span><span data-for="business">TEAM NETWORK</span></span>
            <div class="led-controls">
              <div class="led-modes" id="heroModes" role="group" aria-label="LED animation">
                <button class="active" data-mode="chase" aria-pressed="true">Chase</button>
                <button data-mode="rainbow" aria-pressed="false">Rainbow</button>
                <button data-mode="breathe" aria-pressed="false">Breathe</button>
              </div>
              <div class="led-swatches" id="heroSwatches" role="group" aria-label="Highlight lines"></div>
            </div>
          </div>
          <div class="led-screen hero-led" id="heroLED" aria-hidden="true"></div>
        </div>
        <div class="asterisk float-delay-2" aria-hidden="true"></div>
        <div class="floating-element sticker float-heavy"><span data-for="personal">PRE-<br>ORDER</span><span data-for="business">FOR<br>TEAMS</span></div>
        <div class="floating-element pill-dark float-subtle">
          <div class="icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="6" y="6" width="12" height="12" rx="2"/><path d="M9 2v4M15 2v4M9 18v4M15 18v4M2 9h4M2 15h4M18 9h4M18 15h4"/></svg></div>
          <div class="text"><span data-for="personal"><small>Trade-in offer</small>$1,000 back</span><span data-for="business"><small>Productivity</small>Workspace</span></div>
        </div>
        <div class="floating-element pill-secure float-delay-1">
          <div class="icon" aria-hidden="true"></div>
          Secure
        </div>
      </div>

      <div class="bottom-timeline gsap-right">
        <div class="timeline-track">
          <div class="timeline-line" aria-hidden="true"><div class="timeline-nodes"><span></span><span></span></div></div>
          <div class="bg-green-blob">
            <div class="editors-choice">
              <div class="editors-choice-icon" aria-hidden="true"><div></div><div></div><div></div></div>
              <span data-for="personal">NEW<br>RELEASE</span><span data-for="business">FOR<br>BUSINESS</span>
            </div>
          </div>
        </div>
        <div class="timeline-vertical" aria-hidden="true"></div>
        <div class="bottom-text-row">
          <div class="bottom-text-left">
            <h3><span data-for="personal">Trade in your <em>old laptop.</em></span><span data-for="business">Security, <em>built in.</em></span></h3>
            <p><span data-for="personal">Get <span class="hl">up to $1,000 back</span> when you pre-order the most powerful Meridian Book yet.**</span><span data-for="business">Meridian Shield helps protect your <span class="hl">people, devices and data</span> across your organization.</span></p>
          </div>
        </div>
      </div>
    </div>
  </main>

  <!-- ================= QUICK LINKS ================= -->
  <section class="quick" data-section="quick-links" aria-label="Quick links">
    <div class="quick-row" data-for="personal">
      <a class="quick-link reveal-card" href="#featured">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="4" width="18" height="12" rx="2"/><line x1="2" y1="20" x2="22" y2="20"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Shop Meridian Book</span>
      </a>
      <a class="quick-link reveal-card" href="#faq">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7" rx="1.5"/><rect x="14" y="3" width="7" height="7" rx="1.5"/><rect x="3" y="14" width="7" height="7" rx="1.5"/><rect x="14" y="14" width="7" height="7" rx="1.5"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Shop Workspace</span>
      </a>
      <a class="quick-link reveal-card" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M6 11h4M8 9v4M15 12h.01M18 10h.01"/><path d="M17.3 5H6.7a4 4 0 0 0-4 3.6L2 15a3 3 0 0 0 5.2 2.1L9 15h6l1.8 2.1A3 3 0 0 0 22 15l-.7-6.4A4 4 0 0 0 17.3 5z"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Shop Meridian Play</span>
      </a>
      <a class="quick-link reveal-card" href="#featured">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><circle cx="11" cy="11" r="7"/><line x1="21" y1="21" x2="16.6" y2="16.6"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Find your next laptop</span>
      </a>
      <a class="quick-link reveal-card" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M3 18v-6a9 9 0 0 1 18 0v6"/><path d="M21 19a2 2 0 0 1-2 2h-1v-6h3zM3 19a2 2 0 0 0 2 2h1v-6H3z"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Shop accessories</span>
      </a>
      <a class="quick-link reveal-card" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Shop for your business</span>
      </a>
    </div>
    <div class="quick-row" data-for="business">
      <a class="quick-link" href="#faq">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7" rx="1.5"/><rect x="14" y="3" width="7" height="7" rx="1.5"/><rect x="3" y="14" width="7" height="7" rx="1.5"/><rect x="14" y="14" width="7" height="7" rx="1.5"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Workspace for business</span>
      </a>
      <a class="quick-link" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Meridian Huddle</span>
      </a>
      <a class="quick-link" href="#faq">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/><polyline points="9 12 11 14 15 10"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Meridian Shield</span>
      </a>
      <a class="quick-link" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Meridian Ledger</span>
      </a>
      <a class="quick-link" href="#">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Meridian Cloud</span>
      </a>
      <a class="quick-link" href="#featured">
        <div class="ql-top"><span class="ql-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><rect x="2" y="7" width="20" height="14" rx="2"/><path d="M16 7V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v2"/></svg></span><svg class="ql-arrow" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></div>
        <span class="ql-text">Small business</span>
      </a>
    </div>
  </section>

  <!-- ================= FEATURED SLIDER ================= -->
  <section id="featured" data-section="featured">
    <div class="section-head">
      <div class="reveal">
        <div class="eyebrow">Featured</div>
        <h2>New devices, <em>built for what's next</em></h2>
      </div>
      <p class="section-sub reveal">From our most powerful laptop to our most portable Slate, find <span class="hl">the Meridian device that fits how you work and play.</span></p>
    </div>

    <div class="slider dark-ui reveal-card" id="slider" data-component="slider" aria-roledescription="carousel" aria-label="Featured devices">
      <div class="slide s1 active">
        <div class="slide-copy">
          <span class="slide-tag">NEW</span>
          <h3>Meridian Book <em>Ultra</em></h3>
          <p>The most powerful Meridian Book yet, built around <span class="hl">an all-new neural engine.</span> Plus, trade in your current laptop and get up to $1,000 back.**</p>
          <a href="#" class="btn-primary btn-dots on-dark"><span class="btn-dots-text">Pre-order now</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
        </div>
        <div class="slide-visual" aria-hidden="true">
          <div class="laptop">
            <div class="glow"></div>
            <div class="lid"><div class="screen"><div class="led-screen" id="laptopLED"></div><div class="taskbar"><i></i><i></i><i></i><i></i><i></i></div></div></div>
            <div class="base"></div>
          </div>
        </div>
      </div>

      <div class="slide s2">
        <div class="slide-copy">
          <span class="slide-tag">NEW MERIDIAN SLATE</span>
          <h3>Laptop power, <em>tablet portability</em></h3>
          <p>Our most portable Slate yet, with tablet flexibility and <span class="hl">full laptop capabilities.</span></p>
          <a href="#" class="btn-primary btn-dots"><span class="btn-dots-text">Shop now</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
        </div>
        <div class="slide-visual" aria-hidden="true">
          <div class="tablet-wrap">
            <div class="tablet"><div class="screen"><div class="bloom"></div></div></div>
            <div class="pen"></div>
            <div class="kb"></div>
          </div>
        </div>
      </div>

      <div class="slide s3">
        <div class="slide-copy">
          <span class="slide-tag">MERIDIAN LAPTOPS</span>
          <h3>What will you do with <em>all this power?</em></h3>
          <p>Meet <span class="hl">the most advanced Meridian laptops yet.</span></p>
          <a href="#" class="btn-primary btn-dots"><span class="btn-dots-text">Learn more</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
        </div>
        <div class="slide-visual" aria-hidden="true">
          <div class="power-stack">
            <div class="laptop light"><div class="lid"><div class="screen"><div class="bloom"></div></div></div><div class="base"></div></div>
            <div class="laptop light"><div class="lid"><div class="screen"><div class="bloom"></div></div></div><div class="base"></div></div>
            <div class="laptop"><div class="lid"><div class="screen"><div class="bloom"></div><div class="taskbar"><i></i><i></i><i></i><i></i></div></div></div><div class="base"></div></div>
            <div class="chip-badge"><span class="ci"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="6" y="6" width="12" height="12" rx="2"/><path d="M9 2v4M15 2v4M9 18v4M15 18v4M2 9h4M2 15h4M18 9h4M18 15h4"/></svg></span>Most advanced Meridian laptops</div>
          </div>
        </div>
      </div>

      <div class="slider-ui">
        <span class="count" aria-live="polite"><span id="slideNum">01</span> / 03</span>
        <div class="progress" aria-hidden="true"><i id="slideProgress"></i></div>
        <div class="ctrls">
          <button id="slidePlay" aria-label="Pause slideshow"><svg id="playIcon" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><rect x="6" y="5" width="4" height="14" rx="1"/><rect x="14" y="5" width="4" height="14" rx="1"/></svg></button>
          <button id="slidePrev" aria-label="Previous slide"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><polyline points="15 18 9 12 15 6"/></svg></button>
          <button id="slideNext" aria-label="Next slide"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><polyline points="9 18 15 12 9 6"/></svg></button>
        </div>
      </div>
    </div>
  </section>

  <!-- ================= TRAVEL LIGHT ================= -->
  <section id="travel" data-section="travel">
    <div class="travel reveal-card">
      <div class="travel-copy">
        <div class="eyebrow">New · Meridian Book Air</div>
        <h2>Think big, <em>travel light</em></h2>
        <p>Our most portable Meridian Book: dependable performance, <span class="hl">all-day battery,</span> and security built in.*</p>
        <div class="travel-specs">
          <div class="spec"><small>Performance</small><strong>Dependable</strong></div>
          <div class="spec"><small>Battery</small><strong>All-day</strong></div>
          <div class="spec"><small>Security</small><strong>Built in</strong></div>
        </div>
        <div><a href="#" class="btn-primary">Shop now <span class="arr" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></span></a></div>
      </div>
      <div class="travel-visual" id="travelVisual" aria-hidden="true">
        <div class="ring r1"></div><div class="ring r2"></div><div class="ring r3"></div>
        <div class="feather float-subtle"><i></i>Our most portable</div>
        <div class="laptop light" id="openLaptop">
          <div class="lid"><div class="screen"><div class="bloom"></div><div class="taskbar"><i></i><i></i><i></i><i></i><i></i></div></div></div>
          <div class="base"></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ================= AI ================= -->
  <section id="ai" data-section="ai">
    <div class="section-head">
      <div class="reveal">
        <div class="eyebrow">AI &amp; Assist</div>
        <h2>Get to know <em>Meridian Assist</em></h2>
      </div>
      <a href="#faq" class="link-underline reveal">Explore Assist</a>
    </div>

    <div class="articles">
      <a class="article reveal-card" href="#">
        <div class="art-visual v-gov" aria-hidden="true">
          <div class="ring" style="width:110px;height:110px"></div>
          <div class="ring" style="width:180px;height:180px"></div>
          <div class="ring" style="width:250px;height:250px"></div>
          <div class="orbit" style="position:absolute;width:180px;height:180px;"><div class="sat" style="top:-7px;left:83px"></div></div>
          <div class="orbit2" style="position:absolute;width:250px;height:250px;"><div class="sat" style="bottom:-7px;left:118px;background:var(--brand-green)"></div></div>
          <div class="core"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/><polyline points="9 12 11 14 15 10"/></svg></div>
        </div>
        <div class="art-body">
          <span class="art-cat">Responsible AI</span>
          <h4>How we govern the AI we ship</h4>
          <p>Our 2026 responsible AI report sets out how Meridian builds, tests, deploys and audits the models inside every product.</p>
          <span class="art-link"><span class="c" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></span>Read the report</span>
        </div>
      </a>

      <a class="article reveal-card" href="#">
        <div class="art-visual v-trade">
          <div class="led-screen" id="tradeLED" aria-hidden="true"></div>
          <div class="agile-chip"><i aria-hidden="true"></i>Stay agile</div>
        </div>
        <div class="art-body">
          <span class="art-cat">Customer story</span>
          <h4>When global trade gets messy, AI is here to help</h4>
          <p>How Northline Freight runs its route planning on Meridian Cloud and replans in minutes when a port closes overnight.</p>
          <span class="art-link"><span class="c" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></span>Read the story</span>
        </div>
      </a>

      <a class="article reveal-card" href="#">
        <div class="art-visual v-nature" aria-hidden="true">
          <div class="leaf" style="left:12%;top:22%;transform:rotate(-20deg)"></div>
          <div class="leaf" style="right:14%;top:14%;transform:rotate(30deg) scale(0.8);background:#79cc8e"></div>
          <div class="leaf" style="left:44%;top:8%;transform:rotate(80deg) scale(0.6);background:#4aa863"></div>
          <div class="dc" style="height:110px"></div>
          <div class="dc" style="height:150px"></div>
          <div class="dc" style="height:90px"></div>
        </div>
        <div class="art-body">
          <span class="art-cat">Sustainability</span>
          <h4>Designing datacenters using lessons from nature</h4>
          <p>Through biomimicry, Meridian is restoring wetlands and meadows around the datacenters that run Assist.</p>
          <span class="art-link"><span class="c" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg></span>Learn more</span>
        </div>
      </a>
    </div>
  </section>

  <!-- ================= FAQ ================= -->
  <section id="faq" data-section="faq">
    <div class="faq-wrap">
      <div class="faq-intro reveal">
        <div class="eyebrow">FAQ</div>
        <h2>Questions, <em>answered</em></h2>
        <p class="section-sub"><span data-for="personal">Shopping, offers, orders and Assist. The quick answers, <span class="hl">all in one place.</span></span><span data-for="business">Plans, security, Assist and buying for your team. The quick answers, <span class="hl">all in one place.</span></span></p>
        <a class="faq-contact" href="#"><span class="c" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg></span>Still need help? Contact us</a>
      </div>
      <div class="faq-list reveal" data-for="personal">
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-0"><span>How does the trade-in offer work?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-0" role="region"><p>When you pre-order Meridian Book Ultra, you can trade in an eligible laptop from any brand and get up to $1,000 back. Eligibility and condition terms are on the <a href="#featured">Meridian Book Ultra page</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-1"><span>Which Meridian device is right for me?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-1" role="region"><p>Meridian Book Ultra is our most powerful laptop. Meridian Slate gives you tablet flexibility with full laptop capabilities, and Meridian Book Air is the one to carry everywhere. Still deciding? Start with the <a href="#featured">featured devices</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-2"><span>What is Meridian Assist?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-2" role="region"><p>Assist is the AI built into every Meridian device and app. It finds answers, drafts and summarizes, and works across Workspace. <a href="#ai">Get to know Assist</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-3"><span>Can I return or track an order?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-3" role="region"><p>Yes. Check the status of a purchase from <a href="#">Order tracking</a>, and see <a href="#">Returns</a> for the 30-day returns policy.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-4"><span>Are there deals for students and parents?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-4" role="region"><p>The Meridian Store offers education pricing on select devices and software. See <a href="#">Deals for students and parents</a> for current offers.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-p-5"><span>Can I pay over time?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-p-5" role="region"><p>Yes. <a href="#">Flexible payments</a> lists the financing options available in the Meridian Store.</p></div>
        </div>
      </div>
      <div class="faq-list reveal" data-for="business">
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-0"><span>Which Workspace plan fits my organization?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-0" role="region"><p>Plans run from small teams to enterprise and include Docs, Sheets, Mail and Huddle. <a href="#">Compare Workspace plans</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-1"><span>How can Assist help my team?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-1" role="region"><p>Assist brings AI into the apps your team already uses to draft, summarize and analyze work. <a href="#ai">Learn about Assist</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-2"><span>How does Meridian Shield protect my business?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-2" role="region"><p>Shield brings identity, device, data and threat protection together in one console. <a href="#">Explore Meridian Shield</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-3"><span>Can I buy devices for my whole team?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-3" role="region"><p>Yes. The <a href="#">Small business store</a> bundles Meridian devices, Workspace and support for teams.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-4"><span>What is Meridian Ledger?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-4" role="region"><p>Ledger is a set of business apps for sales, service, finance and operations. <a href="#">Explore Ledger</a>.</p></div>
        </div>
        <div class="faq-item">
          <button class="faq-q" aria-expanded="false" aria-controls="faq-b-5"><span>Where can developers and IT get started?</span><span class="faq-plus" aria-hidden="true"></span></button>
          <div class="faq-a" id="faq-b-5" role="region"><p>Build and run apps on <a href="#">Meridian Cloud</a>, and skill up with free courses on <a href="#">Meridian Learn</a>.</p></div>
        </div>
      </div>
    </div>
  </section>

  <!-- ================= BALLOT ================= -->
  <section style="padding-top: 64px;" data-section="ballot" aria-label="Election reminder">
    <div class="ballot reveal-card">
      <div class="ticker" id="ticker" data-component="dot-matrix-ticker" role="img" aria-label="Election Day, November 3. Check your registration."><div class="ticker-track" id="tickerTrack"></div></div>
      <div class="ballot-row">
      <div class="ballot-icon" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="10" width="18" height="11" rx="2"/><path d="M8 10V5a1 1 0 0 1 1-1h6a1 1 0 0 1 1 1v5"/><polyline points="9.5 7 11.5 9 15 5.5"/></svg></div>
      <div class="ballot-copy">
        <h4>Take it to <em>the ballot</em></h4>
        <p>Election Day is <span class="hl">November 3.</span> Make sure you're registered to have your say.</p>
      </div>
      <a href="#" class="btn-primary btn-dots on-dark"><span class="btn-dots-text">Check your registration</span><span class="btn-dots-icon" aria-hidden="true"><svg width="16" height="19" viewBox="0 0 16 19" fill="none" xmlns="http://www.w3.org/2000/svg"><circle cx="1.61321" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="1.61321" r="1.5"/><circle cx="5.73583" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="5.5566" r="1.5"/><circle cx="9.85851" cy="9.5" r="1.5"/><circle cx="13.9811" cy="9.5" r="1.5"/><circle cx="5.73583" cy="13.4434" r="1.5"/><circle cx="9.85851" cy="13.4434" r="1.5"/><circle cx="1.61321" cy="17.3868" r="1.5"/><circle cx="5.73583" cy="17.3868" r="1.5"/></svg></span></a>
      </div>
    </div>
  </section>

  <!-- ================= FOOTER ================= -->
  <footer data-section="footer">
    <div class="follow reveal">
      <h3>Follow <span class="follow-logo" id="followLogo" role="img" aria-label="Meridian"></span></h3>
      <div class="socials">
        <a href="#" aria-label="Facebook"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M14 8h3V4h-3c-2.8 0-5 2.2-5 5v2H7v4h2v7h4v-7h3l1-4h-4V9c0-.6.4-1 1-1z"/></svg></a>
        <a href="#" aria-label="X"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M18.2 2H21l-6.5 7.4L22 22h-6l-4.7-6.1L5.8 22H3l7-8L2 2h6.1l4.2 5.6zm-1 18h1.6L7 3.8H5.3z"/></svg></a>
        <a href="#" aria-label="LinkedIn"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M4.98 3.5a2.5 2.5 0 1 1 0 5 2.5 2.5 0 0 1 0-5zM3 9h4v12H3zM9 9h3.8v1.7h.1c.5-1 1.8-2 3.8-2 4 0 4.8 2.6 4.8 6V21h-4v-5.6c0-1.3 0-3-1.9-3s-2.1 1.4-2.1 2.9V21H9z"/></svg></a>
        <a href="#" aria-label="Instagram"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" aria-hidden="true"><rect x="3" y="3" width="18" height="18" rx="5"/><circle cx="12" cy="12" r="4"/><circle cx="17.5" cy="6.5" r="0.6" fill="currentColor"/></svg></a>
        <a href="#" aria-label="YouTube"><svg viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M23 7.2a3 3 0 0 0-2.1-2.1C19 4.6 12 4.6 12 4.6s-7 0-8.9.5A3 3 0 0 0 1 7.2 31 31 0 0 0 .5 12a31 31 0 0 0 .5 4.8 3 3 0 0 0 2.1 2.1c1.9.5 8.9.5 8.9.5s7 0 8.9-.5a3 3 0 0 0 2.1-2.1 31 31 0 0 0 .5-4.8 31 31 0 0 0-.5-4.8zM9.8 15.1V8.9l5.8 3.1z"/></svg></a>
      </div>
    </div>

    <div class="footer-grid">
      <div class="footer-col"><h5>What's new</h5><ul>
        <li><a href="#featured">Meridian Book Ultra</a></li>
        <li><a href="#featured">Meridian Slate</a></li>
        <li><a href="#travel">Meridian Book Air</a></li>
        <li><a href="#">Meridian Dev Box</a></li>
        <li><a href="#ai">Explore Assist</a></li>
        <li><a href="#">All Meridian products</a></li>
        <li><a href="#">Apps for Meridian</a></li>
      </ul></div>
      <div class="footer-col"><h5>Meridian Store</h5><ul>
        <li><a href="#">Account profile</a></li>
        <li><a href="#">Downloads</a></li>
        <li><a href="#">Store support</a></li>
        <li><a href="#">Returns</a></li>
        <li><a href="#">Order tracking</a></li>
        <li><a href="#">Certified refurbished</a></li>
        <li><a href="#">Why buy direct</a></li>
        <li><a href="#">Flexible payments</a></li>
      </ul></div>
      <div class="footer-col"><h5>Education</h5><ul>
        <li><a href="#">Meridian in education</a></li>
        <li><a href="#">Devices for education</a></li>
        <li><a href="#">Huddle for classrooms</a></li>
        <li><a href="#">Workspace Education</a></li>
        <li><a href="#">How to buy for your school</a></li>
        <li><a href="#">Educator training</a></li>
        <li><a href="#">Deals for students and parents</a></li>
        <li><a href="#">AI for education</a></li>
      </ul></div>
      <div class="footer-col"><h5>Business</h5><ul>
        <li><a href="#">Meridian AI</a></li>
        <li><a href="#">Meridian Shield</a></li>
        <li><a href="#">Meridian Ledger</a></li>
        <li><a href="#">Workspace</a></li>
        <li><a href="#">Automation platform</a></li>
        <li><a href="#">Meridian Huddle</a></li>
        <li><a href="#">Assist for business</a></li>
        <li><a href="#">Small business</a></li>
      </ul></div>
      <div class="footer-col"><h5>Developer &amp; IT</h5><ul>
        <li><a href="#">Meridian Cloud</a></li>
        <li><a href="#">Developer center</a></li>
        <li><a href="#">Meridian Learn</a></li>
        <li><a href="#">AI marketplace apps</a></li>
        <li><a href="#">Tech community</a></li>
        <li><a href="#">Marketplace</a></li>
        <li><a href="#">Software partners</a></li>
        <li><a href="#">Meridian Studio</a></li>
      </ul></div>
      <div class="footer-col"><h5>Company</h5><ul>
        <li><a href="#">Careers</a></li>
        <li><a href="#">About Meridian</a></li>
        <li><a href="#">Company news</a></li>
        <li><a href="#">Privacy</a></li>
        <li><a href="#">Investors</a></li>
        <li><a href="#">Diversity and inclusion</a></li>
        <li><a href="#">Accessibility</a></li>
        <li><a href="#">Sustainability</a></li>
      </ul></div>
    </div>

    <div class="footer-bottom">
      <div class="fb-left">
        <a href="#"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true"><circle cx="12" cy="12" r="10"/><path d="M2 12h20M12 2a15 15 0 0 1 0 20M12 2a15 15 0 0 0 0 20"/></svg>English (United States)</a>
        <a href="#"><span class="privacy-toggle" aria-hidden="true"></span>Your Privacy Choices</a>
        <a href="#">Consumer Health Privacy</a>
      </div>
      <div class="fb-right">
        <a href="#">Sitemap</a>
        <a href="#">Contact Meridian</a>
        <span class="footer-logo" id="footerLogo" aria-hidden="true"></span>
      </div>
    </div>
    <p class="footnote">* ** Meridian is a fictional brand. Products, offers and copy are placeholders and not affiliated with any real company. LED metro map style adapted from <a href="https://codepen.io/editor/ivorjetski/pen/01a07dcf-a1e8-7ab6-aea1-aa98135803b3" target="_blank" rel="noopener" style="color:inherit">Ben Evans' CSS LED Challenge</a>.</p>
  </footer>

</div>

<script>
document.addEventListener("DOMContentLoaded", () => {
  gsap.registerPlugin(ScrollTrigger);
  const reduceMotion = window.matchMedia("(prefers-reduced-motion: reduce)").matches;

  // ================= LED metro map builder =================
  const LED_COLORS = { a: "#ff4136", b: "#29b6ff", c: "#ffd60a", d: "#6ee86e", e: "#ff53b0", f: "#ff9a1f" };

  // Expand waypoints into one point per grid cell (straight or 45° segments)
  const expand = (wps) => {
    const pts = [wps[0].slice()];
    for (let k = 0; k < wps.length - 1; k++) {
      let [x, y] = wps[k];
      const [x2, y2] = wps[k + 1];
      while (x !== x2 || y !== y2) {
        if (x !== x2) x += Math.sign(x2 - x);
        if (y !== y2) y += Math.sign(y2 - y);
        pts.push([x, y]);
      }
    }
    return pts;
  };

  function buildLED(screen, { cols, rows, lines, mode = "chase", speed = 0.11 }) {
    const stage = document.createElement("div");
    stage.className = "led-stage";
    stage.style.setProperty("--cols", cols);
    stage.style.setProperty("--rows", rows);
    const board = document.createElement("div"); board.className = "led-board";
    const lit = document.createElement("div"); lit.className = "led-lit";
    const trains = document.createElement("div"); trains.className = "led-trains";
    stage.append(board, lit, trains);
    screen.appendChild(stage);
    screen.classList.add("mode-" + mode);

    const occupancy = new Map();
    const timelines = [];
    let boardHTML = "", litHTML = "";
    const pct = ([x, y]) => ({ left: ((x + 0.5) / cols) * 100 + "%", top: ((y + 0.5) / rows) * 100 + "%" });

    Object.entries(lines).forEach(([key, wps]) => {
      const pts = expand(wps);
      const color = LED_COLORS[key];
      pts.forEach(([x, y], i) => {
        const s = `--x:${x};--y:${y};--i:${i};--n:${pts.length};--lc:${color}`;
        boardHTML += `<i class="ln-${key}" style="${s}"></i>`;
        litHTML += `<i class="ln-${key}" style="${s}"></i>`;
        const id = x + "," + y;
        if (!occupancy.has(id)) occupancy.set(id, new Set());
        occupancy.get(id).add(key);
      });

      // Train gliding along the line
      const t = document.createElement("t");
      t.className = "ln-" + key;
      t.style.setProperty("--lc", color);
      trains.appendChild(t);
      gsap.set(t, { ...pct(wps[0]), xPercent: -50, yPercent: -50 });
      const tl = gsap.timeline({ repeat: -1, paused: true });
      for (let k = 0; k < wps.length - 1; k++) {
        const [ax, ay] = wps[k], [bx, by] = wps[k + 1];
        tl.set(t, { rotation: (Math.atan2(by - ay, bx - ax) * 180) / Math.PI });
        tl.to(t, { ...pct(wps[k + 1]), duration: Math.hypot(bx - ax, by - ay) * speed, ease: "none" });
      }
      tl.progress(Math.random());
      timelines.push(tl);
    });

    // Interchange rings where lines share a cell
    occupancy.forEach((set, id) => {
      if (set.size > 1) {
        const [x, y] = id.split(",");
        boardHTML += `<u style="--x:${x};--y:${y}"></u>`;
      }
    });
    board.innerHTML = boardHTML;
    lit.innerHTML = litHTML;

    // Keep LED pitch matched to the screen size
    const fit = () => {
      const w = screen.clientWidth, h = screen.clientHeight;
      if (!w || !h) return;
      stage.style.setProperty("--pitch", Math.min(w / cols, h / rows) + "px");
    };
    new ResizeObserver(fit).observe(screen);
    fit();

    let booted = false, visible = true;
    const sync = () => timelines.forEach((tl) => (booted && visible && !reduceMotion ? tl.play() : tl.pause()));
    ScrollTrigger.create({
      trigger: screen, start: "top bottom", end: "bottom top",
      onToggle: (self) => { visible = self.isActive; screen.classList.toggle("offscreen", !visible); sync(); }
    });

    return {
      boot() { booted = true; screen.classList.add("booted"); sync(); },
      setMode(m) {
        screen.classList.remove("mode-chase", "mode-rainbow", "mode-breathe");
        screen.classList.add("mode-" + m);
      },
      setFilter(keys) {
        screen.classList.toggle("filtering", keys.size > 0);
        stage.querySelectorAll("[class^='ln-'], [class*=' ln-']").forEach((el) => {
          const key = [...el.classList].find((c) => c.startsWith("ln-")).slice(3);
          el.classList.toggle("on", keys.has(key));
        });
      }
    };
  }

  // Hero network
  const heroLines = {
    a: [[1, 3], [6, 8], [16, 8], [22, 14], [35, 14]],
    b: [[2, 18], [10, 10], [24, 10], [30, 4], [35, 4]],
    c: [[18, 1], [18, 7], [20, 9], [20, 19]],
    d: [[0, 12], [7, 12], [12, 7], [26, 7], [31, 12], [35, 12]],
    e: [[8, 17], [13, 17], [17, 13], [25, 13], [29, 17], [34, 17]],
    f: [[4, 1], [8, 5], [26, 5], [29, 2], [35, 2]]
  };
  const heroLED = buildLED(document.getElementById("heroLED"), { cols: 36, rows: 20, lines: heroLines, mode: "chase" });

  // Hero controls
  const modeBtns = document.querySelectorAll("#heroModes button");
  modeBtns.forEach((btn) => btn.addEventListener("click", () => {
    modeBtns.forEach((b) => { b.classList.toggle("active", b === btn); b.setAttribute("aria-pressed", String(b === btn)); });
    heroLED.setMode(btn.dataset.mode);
  }));
  const activeLines = new Set();
  const swatches = document.getElementById("heroSwatches");
  Object.keys(heroLines).forEach((key) => {
    const b = document.createElement("button");
    b.style.setProperty("--sw", LED_COLORS[key]);
    b.setAttribute("aria-label", "Highlight line " + key.toUpperCase());
    b.setAttribute("aria-pressed", "false");
    b.title = "Line " + key.toUpperCase();
    b.addEventListener("click", () => {
      activeLines.has(key) ? activeLines.delete(key) : activeLines.add(key);
      b.classList.toggle("on", activeLines.has(key));
      b.setAttribute("aria-pressed", String(activeLines.has(key)));
      heroLED.setFilter(activeLines);
    });
    swatches.appendChild(b);
  });

  // Laptop screen in the featured slider
  const laptopLED = buildLED(document.getElementById("laptopLED"), {
    cols: 24, rows: 16, mode: "rainbow", speed: 0.13,
    lines: {
      a: [[1, 2], [5, 6], [13, 6], [18, 11], [23, 11]],
      b: [[1, 14], [7, 8], [17, 8], [22, 3], [23, 3]],
      c: [[12, 0], [12, 15]],
      d: [[0, 10], [4, 10], [8, 14], [23, 14]]
    }
  });
  ScrollTrigger.create({ trigger: "#slider", start: "top 85%", once: true, onEnter: () => laptopLED.boot() });

  // Supply-chain article visual
  const tradeLED = buildLED(document.getElementById("tradeLED"), {
    cols: 30, rows: 17, mode: "chase", speed: 0.12,
    lines: {
      a: [[0, 8], [29, 8]],
      b: [[3, 16], [11, 8], [19, 0]],
      c: [[15, 0], [15, 16]],
      d: [[2, 1], [17, 16], [29, 16]],
      f: [[29, 2], [23, 8], [23, 12], [27, 16]]
    }
  });
  ScrollTrigger.create({ trigger: "#tradeLED", start: "top 90%", once: true, onEnter: () => tradeLED.boot() });

  // ================= Dot-matrix ticker =================
  const FONT = {
    A: ["01110","10001","10001","11111","10001","10001","10001"],
    C: ["01110","10001","10000","10000","10000","10001","01110"],
    D: ["11110","10001","10001","10001","10001","10001","11110"],
    E: ["11111","10000","10000","11110","10000","10000","11111"],
    G: ["01110","10001","10000","10111","10001","10001","01111"],
    H: ["10001","10001","10001","11111","10001","10001","10001"],
    I: ["01110","00100","00100","00100","00100","00100","01110"],
    K: ["10001","10010","10100","11000","10100","10010","10001"],
    L: ["10000","10000","10000","10000","10000","10000","11111"],
    N: ["10001","11001","10101","10011","10001","10001","10001"],
    O: ["01110","10001","10001","10001","10001","10001","01110"],
    R: ["11110","10001","10001","11110","10100","10010","10001"],
    S: ["01111","10000","10000","01110","00001","00001","11110"],
    T: ["11111","00100","00100","00100","00100","00100","00100"],
    U: ["10001","10001","10001","10001","10001","10001","01110"],
    V: ["10001","10001","10001","10001","10001","01010","00100"],
    Y: ["10001","10001","01010","00100","00100","00100","00100"],
    "3": ["11110","00001","00001","01110","00001","00001","11110"],
    "•": ["00000","00000","01110","01110","01110","00000","00000"],
    " ": ["00000","00000","00000","00000","00000","00000","00000"]
  };
  const tickerEl = document.getElementById("ticker");
  const track = document.getElementById("tickerTrack");
  const message = "ELECTION DAY  •  NOV 3  •  CHECK YOUR REGISTRATION  •  ";
  const columns = [];
  [...message].forEach((ch) => {
    const g = FONT[ch] || FONT[" "];
    for (let c = 0; c < 5; c++) columns.push(g.map((row) => row[c] === "1"));
    columns.push(new Array(7).fill(false));
  });
  const buildTicker = () => {
    const p = parseFloat(getComputedStyle(tickerEl).getPropertyValue("--p")) || 7;
    const w = columns.length * p, h = 7 * p, r = p * 0.32;
    let circles = "";
    columns.forEach((col, x) => col.forEach((on, y) => {
      if (on) circles += `<circle cx="${(x + 0.5) * p}" cy="${(y + 0.5) * p}" r="${r}"/>`;
    }));
    const svg = `<svg width="${w}" height="${h}" viewBox="0 0 ${w} ${h}" fill="#b6f5c3" aria-hidden="true">${circles}</svg>`;
    track.innerHTML = svg + svg;
    gsap.killTweensOf(track);
    gsap.set(track, { x: 0 });
    if (!reduceMotion) {
      gsap.to(track, { x: -w, duration: columns.length * 0.07, ease: `steps(${columns.length})`, repeat: -1 });
    }
  };
  buildTicker();
  let tickerP = getComputedStyle(tickerEl).getPropertyValue("--p");
  window.addEventListener("resize", () => {
    const p = getComputedStyle(tickerEl).getPropertyValue("--p");
    if (p !== tickerP) { tickerP = p; buildTicker(); }
  });

  // Footer and "Follow Meridian" reuse the nav brandmark
  const brandmark = document.querySelector("#navLogo").innerHTML;
  document.getElementById("footerLogo").innerHTML = brandmark;
  document.getElementById("followLogo").innerHTML = brandmark;

  // Mobile menu
  const navLinks = document.getElementById("navLinks");
  const menuToggle = document.getElementById("menuToggle");
  menuToggle.addEventListener("click", () => {
    const open = navLinks.classList.toggle("open");
    menuToggle.setAttribute("aria-expanded", String(open));
  });
  navLinks.querySelectorAll("a").forEach(a => a.addEventListener("click", () => {
    navLinks.classList.remove("open");
    menuToggle.setAttribute("aria-expanded", "false");
  }));

  // Personal / Business segmented control
  const MODE_KEY = "meridian.mode";
  const seg = document.getElementById("segmented");
  const thumb = seg.querySelector(".seg-thumb");
  const segBtns = seg.querySelectorAll("button");
  const placeThumb = (btn, animate) => {
    const props = { x: btn.offsetLeft - 4, width: btn.offsetWidth };
    animate && !reduceMotion ? gsap.to(thumb, { ...props, duration: 0.45, ease: "power3.out" }) : gsap.set(thumb, props);
  };
  const pressSeg = (btn) => segBtns.forEach(b => { b.classList.toggle("active", b === btn); b.setAttribute("aria-pressed", String(b === btn)); });
  placeThumb(seg.querySelector(".active"), false);
  const toast = document.getElementById("modeToast");
  const setMode = (mode, animate) => {
    const business = mode === "business";
    if (document.body.classList.contains("is-business") === business) return;
    document.body.classList.toggle("is-business", business);
    try { localStorage.setItem(MODE_KEY, mode); } catch (e) {}
    ScrollTrigger.refresh();
    if (!animate) return;
    toast.querySelector("span").textContent = business ? "Showing Meridian for business" : "Showing Meridian for personal use";
    gsap.killTweensOf(toast);
    if (reduceMotion) {
      gsap.timeline().set(toast, { opacity: 1, y: 0 }).set(toast, { opacity: 0 }, "+=2.2");
      return;
    }
    // Bring the newly shown content in
    const shown = gsap.utils.toArray(`[data-for="${mode}"]`).filter((el) => el.getClientRects().length);
    gsap.fromTo(shown, { y: 14, opacity: 0 }, { y: 0, opacity: 1, duration: 0.6, stagger: 0.03, ease: "power3.out", clearProps: "transform,opacity" });
    gsap.timeline()
      .fromTo(toast, { opacity: 0, y: 20 }, { opacity: 1, y: 0, duration: 0.4, ease: "power3.out" })
      .to(toast, { opacity: 0, y: 10, duration: 0.4, ease: "power2.in" }, "+=1.8");
    if (window.scrollY > window.innerHeight * 0.6) window.scrollTo({ top: 0, behavior: "smooth" });
  };
  segBtns.forEach(btn => btn.addEventListener("click", () => {
    pressSeg(btn);
    placeThumb(btn, true);
    setMode(btn.dataset.mode, true);
  }));
  // Restore last choice
  try {
    if (localStorage.getItem(MODE_KEY) === "business") {
      const bBtn = seg.querySelector('[data-mode="business"]');
      pressSeg(bBtn);
      placeThumb(bBtn, false);
      setMode("business", false);
    }
  } catch (e) {}
  window.addEventListener("resize", () => placeThumb(seg.querySelector(".active"), false));
  // Web fonts change the button widths after first layout
  if (document.fonts) document.fonts.ready.then(() => placeThumb(seg.querySelector(".active"), false));

  // FAQ accordion
  document.querySelectorAll(".faq-item").forEach((item) => {
    const q = item.querySelector(".faq-q");
    const a = item.querySelector(".faq-a");
    const dur = reduceMotion ? 0 : 0.45;
    q.addEventListener("click", () => {
      const open = !item.classList.contains("open");
      item.parentElement.querySelectorAll(".faq-item.open").forEach((other) => {
        if (other === item) return;
        other.classList.remove("open");
        other.querySelector(".faq-q").setAttribute("aria-expanded", "false");
        gsap.to(other.querySelector(".faq-a"), { height: 0, duration: dur, ease: "power2.inOut" });
      });
      item.classList.toggle("open", open);
      q.setAttribute("aria-expanded", String(open));
      gsap.to(a, { height: open ? "auto" : 0, duration: dur, ease: "power2.inOut", onComplete: () => ScrollTrigger.refresh() });
    });
  });

  // ===== Intro, floats and parallax (motion only) =====
  if (reduceMotion) {
    heroLED.boot();
  } else {
    // 1. Entrance timeline
    const tl = gsap.timeline();
    tl.from(".gsap-nav", { y: -30, opacity: 0, duration: 0.8, ease: "power3.out" })
      .from(".gsap-hero", { y: 40, opacity: 0, duration: 0.8, stagger: 0.15, ease: "power2.out" }, "-=0.4")
      .from(".gsap-right", { x: 40, opacity: 0, duration: 1, stagger: 0.2, ease: "power3.out" }, "-=0.8")
      .from(".led-panel", { scale: 0.94, duration: 0.9, ease: "power3.out" }, "-=0.9")
      .add(() => heroLED.boot(), "-=0.5")
      .from(".floating-element", { scale: 0, opacity: 0, rotation: () => gsap.utils.random(-20, 20), duration: 0.6, stagger: 0.1, ease: "back.out(1.5)" }, "-=0.5");

    // 2. Floating loops. The LED panel is not in this list: it carries the scrubbed parallax below,
    // and a float and a scrub on the same y fight and park the element out of place.
    const floatStart = tl.duration();
    gsap.to(".float-subtle", { y: "-=8", rotation: "+=1", duration: 2.5, repeat: -1, yoyo: true, ease: "sine.inOut", delay: floatStart });
    gsap.to(".float-heavy", { y: "-=15", rotation: "-=3", duration: 3.5, repeat: -1, yoyo: true, ease: "sine.inOut", delay: floatStart });
    gsap.to(".float-delay-1", { y: "-=10", duration: 3, repeat: -1, yoyo: true, ease: "sine.inOut", delay: 0.5 });
    gsap.to(".float-delay-2", { y: "-=10", duration: 2.8, repeat: -1, yoyo: true, ease: "sine.inOut", delay: 1 });

    // 3. Hover lift (not the floating card, whose y belongs to its float loop)
    document.querySelectorAll(".btn-primary, .article").forEach((el) => {
      el.addEventListener("mouseenter", () => gsap.to(el, { y: -4, duration: 0.3, ease: "power2.out" }));
      el.addEventListener("mouseleave", () => gsap.to(el, { y: 0, duration: 0.3, ease: "power2.out" }));
    });

    // 4. Scroll parallax
    gsap.to(".led-panel", { y: 24, scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: 1 } });
    gsap.to(".ambient span:nth-child(1)", { y: 160, scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: 1 } });
    gsap.to(".ambient span:nth-child(2)", { y: -120, scrollTrigger: { trigger: ".hero", start: "top top", end: "bottom top", scrub: 1.5 } });
  }

  // ===== Scroll reveals =====
  // batch({ once: true }) only fires for elements that cross the start line while someone watches.
  // Land past it (anchor link, restored scroll, a preview iframe scrolled by its host) and the
  // element would sit at opacity 0 forever, so a sweep also reveals whatever is already on screen
  // after every refresh and every scrollEnd.
  if (!reduceMotion) {
    const pending = new Set(gsap.utils.toArray(".reveal, .reveal-card"));
    gsap.set(".reveal", { y: 40, opacity: 0 });
    gsap.set(".reveal-card", { y: 60, opacity: 0 });
    const reveal = (els) => {
      const todo = els.filter((el) => pending.has(el));
      if (!todo.length) return;
      todo.forEach((el) => pending.delete(el));
      gsap.to(todo, { y: 0, opacity: 1, duration: 0.95, stagger: 0.08, ease: "power3.out", clearProps: "transform,opacity" });
    };
    ScrollTrigger.batch([...pending], { start: "top 90%", once: true, onEnter: reveal });
    const sweep = () => reveal([...pending].filter((el) => {
      const r = el.getBoundingClientRect();
      // display:none (the other audience's copy) reports a 0x0 rect at 0,0: reveal it too, it is off anyway
      return r.top < window.innerHeight * 0.95 || (!r.width && !r.height);
    }));
    ScrollTrigger.addEventListener("refresh", sweep);
    ScrollTrigger.addEventListener("scrollEnd", sweep);
    sweep();
  }

  // ===== Featured slider =====
  const slider = document.getElementById("slider");
  const slides = slider.querySelectorAll(".slide");
  const numEl = document.getElementById("slideNum");
  const bar = document.getElementById("slideProgress");
  const playBtn = document.getElementById("slidePlay");
  const playIcon = document.getElementById("playIcon");
  // Reduced motion: no autoplay, the arrows still work
  let current = 0, playing = !reduceMotion;
  const DURATION = 6;
  const PAUSE_ICON = '<rect x="6" y="5" width="4" height="14" rx="1"/><rect x="14" y="5" width="4" height="14" rx="1"/>';
  const PLAY_ICON = '<path d="M7 4.5v15a1 1 0 0 0 1.5.86l12-7.5a1 1 0 0 0 0-1.72l-12-7.5A1 1 0 0 0 7 4.5z"/>';
  const syncPlayBtn = () => {
    playBtn.setAttribute("aria-label", playing ? "Pause slideshow" : "Play slideshow");
    playIcon.innerHTML = playing ? PAUSE_ICON : PLAY_ICON;
  };
  syncPlayBtn();
  const progressTween = gsap.fromTo(bar, { width: "0%" }, { width: "100%", duration: DURATION, ease: "none", paused: true, onComplete: () => go(current + 1) });

  function go(i) {
    const prev = slides[current];
    current = (i + slides.length) % slides.length;
    const next = slides[current];
    if (prev !== next) {
      if (reduceMotion) {
        prev.classList.remove("active");
        next.classList.add("active");
      } else {
        gsap.to(prev, { opacity: 0, duration: 0.6, ease: "power2.out", onComplete: () => { prev.classList.remove("active"); gsap.set(prev, { clearProps: "opacity,visibility" }); } });
        next.classList.add("active");
        gsap.fromTo(next, { opacity: 0 }, { opacity: 1, duration: 0.6, ease: "power2.out" });
        gsap.from(next.querySelectorAll(".slide-tag, h3, p, .btn-primary"), { y: 30, opacity: 0, duration: 0.8, stagger: 0.08, ease: "power3.out", delay: 0.15 });
        gsap.from(next.querySelector(".slide-visual > *"), { y: 40, scale: 0.94, opacity: 0, duration: 1.1, ease: "power3.out", delay: 0.1 });
      }
    }
    slider.classList.toggle("dark-ui", current === 0);
    numEl.textContent = String(current + 1).padStart(2, "0");
    progressTween.restart();
    if (!playing) progressTween.pause();
  }
  document.getElementById("slideNext").addEventListener("click", () => go(current + 1));
  document.getElementById("slidePrev").addEventListener("click", () => go(current - 1));
  playBtn.addEventListener("click", () => {
    playing = !playing;
    playing ? progressTween.resume() : progressTween.pause();
    syncPlayBtn();
  });
  ScrollTrigger.create({ trigger: slider, start: "top 80%", once: true, onEnter: () => { if (playing) progressTween.play(); } });

  if (!reduceMotion) {
    // Laptop lid opens on scroll
    gsap.fromTo("#openLaptop .lid", { rotationX: -88 }, {
      rotationX: 0, ease: "power2.out",
      scrollTrigger: { trigger: "#travelVisual", start: "top 85%", end: "center 55%", scrub: 1 }
    });
    gsap.utils.toArray(".travel-visual .ring").forEach((r, i) => {
      gsap.from(r, { scale: 0.6, opacity: 0, duration: 1.4, delay: i * 0.15, ease: "power3.out", scrollTrigger: { trigger: "#travelVisual", start: "top 80%" } });
    });

    // Article visuals
    gsap.to(".v-gov .orbit", { rotation: 360, duration: 14, repeat: -1, ease: "none" });
    gsap.to(".v-gov .orbit2", { rotation: -360, duration: 22, repeat: -1, ease: "none" });
    gsap.from(".v-nature .dc", { scaleY: 0, transformOrigin: "bottom", duration: 1, stagger: 0.12, ease: "back.out(1.4)", scrollTrigger: { trigger: ".v-nature", start: "top 85%" } });
    gsap.from(".v-nature .leaf", { scale: 0, duration: 1, stagger: 0.15, ease: "back.out(2)", delay: 0.4, scrollTrigger: { trigger: ".v-nature", start: "top 85%" } });
  }

  // Cursor spotlight on articles
  document.querySelectorAll(".article").forEach((card) => {
    card.addEventListener("mousemove", (e) => {
      const r = card.getBoundingClientRect();
      card.style.setProperty("--mx", (e.clientX - r.left) + "px");
      card.style.setProperty("--my", (e.clientY - r.top) + "px");
    });
  });

  // Magnetic primary buttons (pointer devices only)
  if (!reduceMotion && window.matchMedia("(hover: hover)").matches) {
    document.querySelectorAll(".btn-primary").forEach((btn) => {
      btn.addEventListener("mousemove", (e) => {
        const r = btn.getBoundingClientRect();
        gsap.to(btn, { x: (e.clientX - r.left - r.width / 2) * 0.18, duration: 0.4, ease: "power3.out" });
      });
      btn.addEventListener("mouseleave", () => gsap.to(btn, { x: 0, duration: 0.6, ease: "elastic.out(1, 0.4)" }));
    });
  }
});
</script>
</body>
</html>
```

