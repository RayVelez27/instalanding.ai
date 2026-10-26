INSTALANDING.AI · Mirador Observability Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Mirador Observability Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/mirador-observability-page

mirador-observability.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Mirador Observability Page
  slug     mirador-observability-page
  prompt   https://instalanding.ai/p/mirador-observability-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/mirador-observability-page
  license  MIT. Fictional company; every name, number, customer, quote and contact detail is invented. Replace them before shipping.

  MAP
  tokens    :root at the top of <style>: night, ink, paper and six signal colours (violet, indigo, sky, amber, mint, rose);
            role tokens (--bg, --plate, --text, --muted, --line, --mist, --card, --glass, --accent) that html.light
            swaps for a paper theme; fonts (--f-display / --f-text Geist, --f-mono Geist Mono, --f-serif Instrument Serif
            italic for the one emphasised word per heading); --frame, --r-frame, --r-plate, --fillet, --side, --rail,
            --pad, --stick and two eases.
  sections  nav, hero, intro, features, integrations, gallery, process, pricing, team, reviews, faq, security, contact,
            footer
  scripts   1) GhostFibers: a WebGL2 ribbon field of glowing dots with bloom, depth of field, hover focus and click pulses,
            mounted into [data-fibers] in the hero; it pauses off screen and is skipped without WebGL2. 2) the page
            script: code-drawn heatmap and sparkline, header filters (environment / region / time range) that re-roll
            the hero card's figures, hide-on-scroll header and framed state, the scroll-spy rail, a dark/light theme
            switch with a circular view transition (saved to localStorage), watch/pin/share toggles, the billing
            switch, both forms. 3) GSAP 3.13 + ScrollTrigger + SplitText and Lenis 1.3.4 (jsdelivr): the hero frame
            opening, word-by-word statement, stacking feature cards, region pills unclipping, bento drift, a pinned
            four-step process with a progress ring, plan and FAQ entrances, team portraits, a looping review track,
            the security reveal and the contact circle wipe.
  assets    none: every chart, trace, map, portrait and icon is HTML, CSS, inline SVG or WebGL; fonts from Google Fonts

  ADAPTING
  - Fillets: each plate cut out of a photo carries .fil corner pieces painted in --plate; keep them when moving a plate,
    or the inverted corners show as square notches.
  - .bite masks a circle out of a glass card for the disc that sits in it; --d and --gap on the wrapper must match.
  - html.motion is added in <head> only when motion is allowed and dropped if GSAP has not loaded in 2.5s; hidden
    states are scoped under .motion, so the page is complete without it.
  - Prices swap from data-monthly / data-annual; the footer wordmark sizes from --len (its character count).
-->
<html lang="en" class="no-js">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mirador — See every signal</title>
<meta name="description" content="Mirador is the observability platform that unifies traces, metrics and logs so engineering teams find the cause before customers find the bug.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Geist:wght@300..700&family=Geist+Mono:wght@400;500&family=Instrument+Serif:ital@0;1&display=swap">
<script>(function(){var d=document.documentElement;d.classList.remove('no-js');try{if(localStorage.getItem('mirador-theme')==='light')d.classList.add('light')}catch(e){}if(!window.matchMedia('(prefers-reduced-motion: reduce)').matches){d.classList.add('motion');setTimeout(function(){if(!window.gsap)d.classList.remove('motion')},2500)}})();</script>
<style>
:root{--night:#0a0912;--ink:#14122a;--paper:#f6f5fb;--violet:#8f80ff;--indigo:#3b30b8;--sky:#7cc4ff;--amber:#f5a54a;--mint:#4fe3b0;--rose:#ff6b8a;--dusk:#e9b49c;
--bg:var(--night);--plate:var(--night);--text:#eceaf7;--muted:color-mix(in oklab, #eceaf7 58%, var(--night));--line:color-mix(in oklab, #eceaf7 12%, transparent);--mist:#17152c;--card:#121027;--glass:color-mix(in oklab, var(--night) 48%, transparent);--glass-solid:color-mix(in oklab, var(--night) 86%, transparent);--accent:var(--violet);--on-accent:var(--night);--on-photo:white;--shadow:0 26px 54px -26px rgba(0,0,0,.85);
--f-display:'Geist', ui-sans-serif, system-ui, sans-serif;--f-text:'Geist', ui-sans-serif, system-ui, sans-serif;--f-mono:'Geist Mono', ui-monospace, SFMono-Regular, Menlo, monospace;--f-serif:'Instrument Serif', Georgia, serif;
--frame:14px;--r-frame:40px;--r-plate:34px;--fillet:36px;--side:clamp(20px, 5vw, 72px);--rail:0px;--inset:max(var(--side), var(--rail));--pad:clamp(96px, 11vw, 168px);--stick:48px;--ease:cubic-bezier(.65, 0, .25, 1);--ease-out:cubic-bezier(.2, .8, .2, 1);}
@media (min-width:1024px){:root{--rail:112px;}}
@media (max-width:767px){:root{--frame:8px;--r-frame:28px;--r-plate:26px;--fillet:22px;--stick:14px;}}
html.light{--bg:var(--paper);--plate:var(--paper);--text:var(--ink);--muted:color-mix(in oklab, var(--ink) 62%, var(--paper));--line:color-mix(in oklab, var(--ink) 12%, transparent);--mist:#eae8f6;--card:#ffffff;--glass:color-mix(in oklab, var(--paper) 55%, transparent);--glass-solid:color-mix(in oklab, var(--paper) 90%, transparent);--accent:var(--indigo);--on-accent:var(--paper);--shadow:0 22px 44px -24px color-mix(in oklab, var(--indigo) 50%, transparent);}
*, *::before, *::after{box-sizing:border-box;}html{-webkit-text-size-adjust:100%;}@media (prefers-reduced-motion:no-preference){html{scroll-behavior:smooth;}}html.lenis, html.lenis body{height:auto;}.lenis.lenis-smooth{scroll-behavior:auto !important;}
body{margin:0;background:var(--bg);color:var(--text);font:400 16px/1.55 var(--f-text);-webkit-font-smoothing:antialiased;overflow-x:clip;}
a{color:inherit;text-decoration:none;}button, input, select, textarea{font:inherit;color:inherit;}button{background:none;border:0;padding:0;cursor:pointer;}
h1, h2, h3, p, ul, ol, dl, dd, figure, blockquote{margin:0;}ul, ol{padding:0;list-style:none;}main > section{position:relative;overflow-x:clip;}
:focus-visible{outline:2px solid var(--accent);outline-offset:3px;}
.sprite{position:absolute;width:0;height:0;overflow:hidden;}.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap;}
.i{width:20px;height:20px;flex:none;fill:none;stroke:currentColor;stroke-width:1.7;stroke-linecap:round;stroke-linejoin:round;}
.wrap{padding-inline:var(--inset);}
.h2{font:500 clamp(38px, 4.9vw, 70px)/1 var(--f-display);letter-spacing:-.04em;overflow-wrap:break-word;}
.h2 em, .hero-title em, .statement em, .foot-news em{font-family:var(--f-serif);font-style:italic;font-weight:400;letter-spacing:-.01em;}
.lede{color:var(--muted);font-size:clamp(16px, 1.25vw, 18px);max-width:44ch;}
.eyebrow{display:inline-flex;align-items:center;gap:10px;font:500 12px/1 var(--f-mono);letter-spacing:.12em;text-transform:uppercase;color:var(--muted);}
.eyebrow::before{content:"";width:7px;height:7px;border-radius:50%;background:var(--mint);box-shadow:0 0 0 4px color-mix(in oklab, var(--mint) 22%, transparent);}

/* buttons */
.btn{--ox:calc(100% - 28px);position:relative;isolation:isolate;overflow:hidden;display:inline-flex;align-items:center;gap:16px;min-height:56px;padding:6px 6px 6px 26px;border-radius:999px;background:var(--card);color:var(--text);font-weight:600;font-size:15px;white-space:nowrap;transition:color .45s var(--ease);box-shadow:inset 0 0 0 1px var(--line);}
.btn::before{content:"";position:absolute;inset:0;z-index:-1;background:var(--accent);clip-path:circle(0 at var(--ox) 50%);transition:clip-path .7s var(--ease);}
.btn-dot{width:44px;height:44px;border-radius:50%;display:grid;place-items:center;background:var(--accent);color:var(--on-accent);transition:background-color .45s, color .45s;}
.btn-dot .i{transition:transform .5s var(--ease);}
.btn-solid{background:var(--accent);color:var(--on-accent);box-shadow:0 18px 40px -18px var(--accent);}.btn-solid::before{background:var(--card);}.btn-solid .btn-dot{background:var(--on-accent);color:var(--accent);}
@media (hover:hover){.btn:hover::before{clip-path:circle(160% at var(--ox) 50%);}.btn:hover{color:var(--on-accent);}.btn:hover .btn-dot{background:var(--on-accent);color:var(--accent);}.btn:hover .btn-dot .i{transform:rotate(45deg);}.btn-solid:hover{color:var(--text);}.btn-solid:hover .btn-dot{background:var(--accent);color:var(--on-accent);}}
.btn:focus-visible::before{clip-path:circle(160% at var(--ox) 50%);}.btn:focus-visible{color:var(--on-accent);}
.ibtn{position:relative;isolation:isolate;width:48px;height:48px;flex:none;border-radius:50%;display:grid;place-items:center;background:var(--mist);color:var(--text);transition:color .4s var(--ease);}
.ibtn::before{content:"";position:absolute;inset:0;z-index:-1;border-radius:50%;background:var(--accent);transform:scale(0);transition:transform .5s var(--ease);}
.ibtn-light{background:color-mix(in oklab, white 82%, transparent);color:var(--ink);}
@media (hover:hover){.ibtn:hover::before, a:hover > .ibtn::before{transform:scale(1);}.ibtn:hover, a:hover > .ibtn{color:var(--on-accent);}}
.ibtn:focus-visible::before{transform:scale(1);}.ibtn:focus-visible{color:var(--on-accent);}
.lnk{position:relative;display:inline-block;}.lnk::after{content:"";position:absolute;left:0;right:0;bottom:-2px;height:1.5px;border-radius:2px;background:currentColor;transform:scaleX(0);transform-origin:100% 50%;transition:transform .6s var(--ease);}
@media (hover:hover){.lnk:hover::after{transform:scaleX(1);transform-origin:0 50%;}}.lnk:focus-visible::after{transform:scaleX(1);}

/* plates & fillets */
.plate{background:var(--plate);color:var(--text);position:relative;}
.fil{position:absolute;width:var(--fillet);height:var(--fillet);pointer-events:none;--c:var(--plate);}
.fil-tl{background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--c) var(--fillet));}
.fil-tr{background:radial-gradient(circle at 0 0, transparent calc(var(--fillet) - .6px), var(--c) var(--fillet));}
.fil-bl{background:radial-gradient(circle at 100% 100%, transparent calc(var(--fillet) - .6px), var(--c) var(--fillet));}
.fil-br{background:radial-gradient(circle at 0 100%, transparent calc(var(--fillet) - .6px), var(--c) var(--fillet));}
.glass{background:var(--glass-solid);color:var(--text);}
@media (min-width:1024px) and (hover:hover){.glass{background:var(--glass);-webkit-backdrop-filter:blur(22px) saturate(1.35);backdrop-filter:blur(22px) saturate(1.35);}}
.disc{width:124px;height:124px;border-radius:50%;display:grid;place-items:center;background:radial-gradient(circle at 30% 25%, var(--violet), var(--indigo) 70%);color:var(--paper);box-shadow:inset 0 1px 0 rgba(255,255,255,.25);}
.disc svg{width:46%;height:46%;fill:none;stroke:currentColor;stroke-width:6.5;stroke-linecap:round;}

/* ===== Code-drawn art ===== */
.art{position:absolute;inset:0;overflow:hidden;background:var(--night);}
.aurora{background:radial-gradient(55% 60% at 18% 22%, color-mix(in oklab, var(--violet) 72%, transparent), transparent 70%),radial-gradient(45% 55% at 84% 16%, color-mix(in oklab, var(--sky) 55%, transparent), transparent 70%),radial-gradient(48% 45% at 64% 80%, color-mix(in oklab, var(--amber) 42%, transparent), transparent 70%),radial-gradient(70% 60% at 28% 98%, color-mix(in oklab, var(--indigo) 85%, transparent), transparent 70%),var(--night);}
.aurora.alt{background:radial-gradient(55% 60% at 80% 20%, color-mix(in oklab, var(--rose) 45%, transparent), transparent 70%),radial-gradient(50% 60% at 12% 30%, color-mix(in oklab, var(--violet) 70%, transparent), transparent 70%),radial-gradient(60% 50% at 50% 100%, color-mix(in oklab, var(--indigo) 90%, transparent), transparent 70%),var(--night);}
.aurora.cool{background:radial-gradient(55% 60% at 75% 25%, color-mix(in oklab, var(--sky) 50%, transparent), transparent 70%),radial-gradient(50% 55% at 20% 80%, color-mix(in oklab, var(--mint) 30%, transparent), transparent 70%),radial-gradient(60% 50% at 40% 10%, color-mix(in oklab, var(--indigo) 85%, transparent), transparent 70%),var(--night);}
.stars::before{content:"";position:absolute;inset:0;background-image:radial-gradient(rgba(255,255,255,.55) 1px, transparent 1.6px);background-size:46px 46px;-webkit-mask-image:linear-gradient(to bottom, black, transparent 65%);mask-image:linear-gradient(to bottom, black, transparent 65%);opacity:.28;}
.floor{position:absolute;left:-50%;right:-50%;bottom:-12%;height:72%;background-image:linear-gradient(rgba(255,255,255,.16) 1px, transparent 1px),linear-gradient(90deg, rgba(255,255,255,.16) 1px, transparent 1px);background-size:64px 64px;transform:perspective(520px) rotateX(64deg);transform-origin:50% 100%;-webkit-mask-image:linear-gradient(to top, black 8%, transparent 82%);mask-image:linear-gradient(to top, black 8%, transparent 82%);}
.hero-art{background:radial-gradient(60% 55% at 22% 18%, color-mix(in oklab, var(--violet) 26%, transparent), transparent 70%),radial-gradient(50% 50% at 86% 12%, color-mix(in oklab, var(--sky) 16%, transparent), transparent 70%),radial-gradient(90% 60% at 50% 115%, color-mix(in oklab, var(--indigo) 55%, transparent), transparent 70%),var(--night);}
.fibers{position:absolute;left:0;right:0;top:20%;bottom:-8%;}
.ghost-fibers-canvas{position:absolute;inset:0;width:100%;height:100%;display:block;}
.flow{stroke-dasharray:6 14;animation:flow 3.2s linear infinite;}
@keyframes flow{to{stroke-dashoffset:-200;}}
@keyframes blink{50%{opacity:0;}}
@keyframes pulse{0%{transform:scale(.6);opacity:.9;}100%{transform:scale(2.4);opacity:0;}}
@keyframes spin{to{transform:rotate(1turn);}}
.dots{background-image:radial-gradient(color-mix(in oklab, var(--violet) 70%, white) 1.2px, transparent 1.8px);background-size:22px 22px;}

/* mock windows */
.win{position:absolute;display:flex;flex-direction:column;border-radius:22px;overflow:hidden;background:color-mix(in oklab, #0d0b1c 90%, transparent);border:1px solid rgba(255,255,255,.09);box-shadow:0 40px 80px -30px rgba(0,0,0,.85), inset 0 1px 0 rgba(255,255,255,.06);color:#e7e5f5;font:400 13px/1.45 var(--f-mono);}
.win-bar{display:flex;align-items:center;gap:7px;padding:13px 18px;border-bottom:1px solid rgba(255,255,255,.07);color:rgba(231,229,245,.55);font-size:12px;white-space:nowrap;overflow:hidden;}
.win-bar i{width:10px;height:10px;border-radius:50%;background:rgba(255,255,255,.16);flex:none;}
.win-bar span{margin-left:10px;overflow:hidden;text-overflow:ellipsis;}
.win-bar em{margin-left:auto;font-style:normal;color:var(--mint);display:flex;align-items:center;gap:6px;}
.win-bar em::before{content:"";width:6px;height:6px;border-radius:50%;background:currentColor;}
.win-body{position:relative;flex:1;min-height:0;padding:18px 20px;overflow:hidden;}
.dim{color:rgba(231,229,245,.5);}

/* waterfall */
.wf{display:grid;gap:8px;}
.wf-row{display:grid;grid-template-columns:150px minmax(0,1fr);gap:16px;align-items:center;font-size:12px;}
.wf-row > span{color:rgba(231,229,245,.7);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;padding-left:calc(var(--d, 0) * 12px);}
.wf-track{position:relative;height:14px;border-radius:5px;background:rgba(255,255,255,.035);}
.wf-track b{position:absolute;top:0;bottom:0;left:var(--l);width:var(--w);border-radius:5px;background:var(--c);box-shadow:0 0 22px -6px var(--c);}
.wf-axis{display:grid;grid-template-columns:150px minmax(0,1fr);gap:16px;margin-bottom:6px;font-size:11px;color:rgba(231,229,245,.4);}
.wf-axis div{display:flex;justify-content:space-between;}

/* metrics */
.mx{display:flex;flex-direction:column;height:100%;gap:12px;}
.mx-legend{display:flex;flex-wrap:wrap;gap:8px 20px;font-size:12px;color:rgba(231,229,245,.7);}
.mx-legend span{display:flex;align-items:center;gap:8px;}
.mx-legend span::before{content:"";width:14px;height:3px;border-radius:3px;background:var(--c);}
.mx-chart{position:relative;flex:1;min-height:0;}
.mx-chart svg{position:absolute;inset:0;width:100%;height:100%;}
.mx-chart path, .mx-chart line{vector-effect:non-scaling-stroke;}
.mx-tip{position:absolute;left:58%;top:4%;padding:10px 14px;border-radius:12px;background:rgba(20,18,42,.92);border:1px solid rgba(255,255,255,.1);font-size:12px;line-height:1.5;white-space:nowrap;box-shadow:0 14px 30px -14px black;}
.mx-tip b{color:var(--rose);font-weight:500;}

/* timeline */
.tl{display:grid;gap:13px;}
.tl-head{display:flex;justify-content:space-between;gap:12px;flex-wrap:wrap;margin-bottom:6px;font-size:12px;color:rgba(231,229,245,.6);}
.tl-head b{color:var(--mint);font-weight:500;}
.tl li{display:grid;grid-template-columns:68px 14px minmax(0,1fr);gap:12px;align-items:center;font-size:12.5px;}
.tl li i{width:10px;height:10px;border-radius:50%;background:var(--c);box-shadow:0 0 0 4px color-mix(in oklab, var(--c) 22%, transparent);}
.tl li span:last-child{white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}

/* ===== header ===== */
.head{position:fixed;inset:0 0 auto 0;z-index:60;pointer-events:none;}
.head a, .head button, .filter-menu{pointer-events:auto;}
.bar{position:relative;display:flex;justify-content:space-between;align-items:flex-start;padding:calc(var(--frame) + 18px) calc(var(--frame) + 70px) 0 calc(var(--frame) + 82px);transition:transform .7s var(--ease);}
.head.hide .bar{transform:translateY(calc(-100% - 24px));}
.pill-nav{--ox:30px;justify-content:center;min-width:176px;min-height:58px;padding:6px 50px;background:color-mix(in oklab, white 88%, transparent);color:var(--ink);font-weight:500;box-shadow:none;}
.pill-nav .i{position:absolute;left:22px;color:var(--amber);width:18px;height:18px;stroke-width:2;}
.pill-nav.to-r{--ox:calc(100% - 30px);}.pill-nav.to-r .i{left:auto;right:22px;}
.head:not(.framed) .pill-nav{box-shadow:var(--shadow), inset 0 0 0 1px var(--line);background:var(--card);color:var(--text);}
@media (hover:hover){.pill-nav:hover, .head:not(.framed) .pill-nav:hover{color:var(--on-accent);}}
.tab{position:absolute;top:0;left:0;right:0;margin-inline:auto;width:max-content;max-width:calc(100% - 2 * (var(--frame) + 300px));display:flex;gap:clamp(26px, 3.6vw, 56px);padding:calc(var(--frame) + 16px) 40px 20px;background:var(--plate);border-radius:0 0 var(--fillet) var(--fillet);}
.tab .fil{top:var(--frame);transition:top .5s var(--ease);}
.tab .fil-tl{right:100%;background:radial-gradient(circle at 0 100%, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.tab .fil-tr{left:100%;background:radial-gradient(circle at 100% 100%, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.head:not(.framed) .tab .fil{top:0;}
.filter{position:relative;min-width:0;}
.filter-btn{display:grid;grid-template-columns:minmax(0, auto) auto;column-gap:20px;row-gap:2px;align-items:center;text-align:left;}
.filter-label{grid-column:1 / -1;display:flex;align-items:center;gap:6px;font-size:11.5px;line-height:1.3;color:var(--muted);white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:16ch;}
.filter-label .i{width:14px;height:14px;}
.filter-value{font-weight:600;font-size:15px;line-height:1.3;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;max-width:13ch;}
.filter-btn .chev{width:18px;height:18px;transition:transform .4s var(--ease);}
.filter.open .chev{transform:rotate(180deg);}
.filter-menu{position:absolute;top:calc(100% + 22px);left:-16px;z-index:5;min-width:200px;padding:6px;background:var(--plate);border-radius:24px;box-shadow:var(--shadow), inset 0 0 0 1px var(--line);opacity:0;visibility:hidden;transform:translateY(-8px);transition:opacity .3s, transform .4s var(--ease), visibility 0s .4s;}
.filter.open .filter-menu{opacity:1;visibility:visible;transform:none;transition:opacity .3s, transform .4s var(--ease);}
.filter-menu button{display:block;width:100%;text-align:left;padding:11px 16px;border-radius:18px;white-space:nowrap;font-size:15px;}
.filter-menu [aria-selected="true"]{background:var(--mist);font-weight:600;}
@media (hover:hover){.filter-menu button:hover{background:var(--mist);}}
.rail{position:fixed;left:0;top:50%;transform:translateY(-42%);display:flex;flex-direction:column;gap:14px;}
.rail-g{position:relative;display:flex;flex-direction:column;gap:8px;padding:10px;margin-left:var(--frame);border-radius:40px;transition:margin .6s var(--ease), padding .6s var(--ease), border-radius .6s var(--ease), background-color .4s, box-shadow .5s;}
.rail-plate{background:var(--plate);}
.head.framed .rail-plate{margin-left:0;padding-left:calc(var(--frame) + 10px);border-radius:0 40px 40px 0;}
.rail-plate .fil{left:var(--frame);opacity:0;transition:opacity .25s;}
.rail-plate .fil-tl{bottom:100%;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.rail-plate .fil-bl{top:100%;background:radial-gradient(circle at 100% 100%, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.head.framed .rail-plate .fil{opacity:1;transition-delay:.35s;}
.head:not(.framed) .rail-g{background:var(--plate);box-shadow:var(--shadow), inset 0 0 0 1px var(--line);}
.ico{position:relative;isolation:isolate;width:48px;height:48px;flex:none;border-radius:50%;display:grid;place-items:center;background:var(--mist);color:var(--text);transition:background-color .4s, color .4s;}
.ico::before{content:"";position:absolute;inset:0;z-index:-1;border-radius:50%;background:var(--accent);transform:scale(0);transition:transform .5s var(--ease);}
@media (hover:hover){.ico:hover::before{transform:scale(1);}.ico:hover{color:var(--on-accent);}}
.ico[hidden]{display:none;}
.head.framed .rail-nav .ico{background:color-mix(in oklab, white 22%, transparent);color:white;-webkit-backdrop-filter:blur(6px);backdrop-filter:blur(6px);}
.rail .ico.is-on, .head.framed .rail-nav .ico.is-on{background:white;color:var(--indigo);box-shadow:0 8px 18px -10px rgba(0,0,0,.6);}
.ava{width:48px;height:48px;border-radius:50%;overflow:hidden;display:grid;place-items:center;}
.av{display:grid;place-items:center;border-radius:50%;color:white;font:600 13px/1 var(--f-display);letter-spacing:.02em;background:radial-gradient(circle at 30% 25%, hsl(var(--h) 90% 72%), hsl(calc(var(--h) + 40) 70% 42%) 75%);}
.ava .av{width:100%;height:100%;font-size:14px;}
.rail-me .ico{background:transparent;}
.theme{display:flex;flex-direction:column;gap:4px;padding:4px;margin-inline:-4px;border-radius:999px;background:var(--mist);}
.theme .ico{width:44px;height:44px;background:transparent;}
.theme .ico[aria-pressed="true"]{background:white;color:var(--indigo);}

/* ===== hero ===== */
.hero{height:100vh;height:100svh;min-height:620px;}
.hero-shot{--open:0;position:absolute;inset:0;overflow:hidden;clip-path:inset(calc(var(--frame) * (1 - var(--open))) round calc(var(--r-frame) * (1 - var(--open))));background:var(--night);}
.hero-drift{position:absolute;inset:0;}
.motion .hero-drift, .motion .glint, .motion .rev-track{will-change:transform;}
.hero-shot::after{content:"";position:absolute;inset:0;pointer-events:none;background:linear-gradient(180deg, color-mix(in oklab, var(--night) 40%, transparent) 8%, transparent 45%), linear-gradient(0deg, color-mix(in oklab, var(--night) 45%, transparent), transparent 40%);}
.hero-copy{position:absolute;left:0;right:0;top:calc(var(--frame) + clamp(96px, 13vh, 124px));padding-inline:var(--inset);}
.hero-title{font:500 clamp(52px, min(9.6vw, 15.5vh), 140px)/.88 var(--f-display);letter-spacing:-.05em;text-align:center;color:var(--on-photo);opacity:.9;overflow-wrap:anywhere;}
.hero-title span{display:block;}
.hero-lede{max-width:38ch;margin:clamp(18px, 3vh, 28px) auto 0;text-align:center;text-wrap:balance;color:color-mix(in oklab, var(--on-photo) 86%, transparent);font-size:17px;line-height:1.6;}
.hero-find{position:absolute;left:calc(var(--rail) + 18px);bottom:0;width:min(400px, 30vw);padding:34px 34px calc(var(--frame) + 28px);border-radius:var(--r-plate) var(--r-plate) 0 0;}
.hero-find .fil{bottom:var(--frame);}
.hero-find .fil-bl{right:100%;background:radial-gradient(circle at 0 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.hero-find .fil-br{left:100%;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.find-title{font:600 22px/1.2 var(--f-display);letter-spacing:-.02em;}
.hero-find > p{margin-top:12px;color:var(--muted);font-size:14.5px;line-height:1.55;}
.find-row{display:flex;align-items:center;gap:14px;margin-top:24px;flex-wrap:wrap;}
.find-num{display:grid;line-height:1;margin-right:4px;}
.find-num strong{font:600 clamp(40px, 3.8vw, 54px)/.95 var(--f-display);letter-spacing:-.05em;}
.find-num span{font-size:12.5px;color:var(--muted);margin-top:6px;}
.faces{display:flex;}
.faces .av{width:46px;height:46px;border:3px solid var(--plate);margin-left:-14px;font-size:13px;}
.faces .av:first-child{margin-left:0;}
.hero-feat{--d:124px;--gap:10px;position:absolute;right:calc(var(--frame) + 22px);bottom:calc(var(--frame) + 18px);width:min(400px, 30vw);}
.bite{-webkit-mask:radial-gradient(circle calc(var(--d) / 2 + var(--gap)) at calc(var(--d) / 2 + 2px) calc(100% - var(--d) / 2 - 2px), transparent calc(var(--d) / 2 + var(--gap) - .5px), black calc(var(--d) / 2 + var(--gap)));mask:radial-gradient(circle calc(var(--d) / 2 + var(--gap)) at calc(var(--d) / 2 + 2px) calc(100% - var(--d) / 2 - 2px), transparent calc(var(--d) / 2 + var(--gap) - .5px), black calc(var(--d) / 2 + var(--gap)));}
.feat{position:relative;overflow:hidden;border-radius:var(--r-plate);padding:28px 28px 22px 30px;}
.glint{position:absolute;left:10%;top:-30%;width:90%;aspect-ratio:1;border-radius:50%;pointer-events:none;background:radial-gradient(closest-side, color-mix(in oklab, var(--violet) 45%, transparent), transparent);opacity:.7;}
.feat > *:not(.glint){position:relative;}
.feat-top{display:flex;gap:16px;align-items:flex-start;justify-content:space-between;}
.feat-name{display:flex;align-items:center;gap:10px;font:500 20px/1.2 var(--f-mono);letter-spacing:-.02em;}
.feat-name::before{content:"";width:9px;height:9px;border-radius:50%;background:var(--mint);box-shadow:0 0 0 5px color-mix(in oklab, var(--mint) 22%, transparent);}
.feat-addr{display:flex;gap:8px;margin-top:8px;font-size:13.5px;line-height:1.4;color:var(--muted);}
.feat-addr .i{width:16px;height:16px;margin-top:1px;}
.feat-top .ibtn{width:58px;height:58px;}
.feat-desc{margin-top:16px;font-size:14px;line-height:1.6;color:var(--muted);}
.spark{display:block;width:100%;height:56px;margin-top:14px;overflow:visible;}
.spark path{vector-effect:non-scaling-stroke;}
.specs{display:flex;flex-wrap:wrap;justify-content:flex-end;gap:10px 22px;margin:16px 0 0 calc(var(--d) - 10px);font-size:13.5px;}
.specs li{display:flex;align-items:center;gap:7px;white-space:nowrap;}
.specs b{font:500 13.5px var(--f-mono);}
.specs .i{width:17px;height:17px;color:var(--muted);}
.feat-acts{display:flex;justify-content:flex-end;gap:10px;margin:16px 0 0 calc(var(--d) + 6px);}
.act{display:grid;justify-items:center;gap:5px;font-size:11.5px;color:var(--muted);}
.act .ibtn{width:48px;height:48px;background:color-mix(in oklab, var(--text) 10%, transparent);}
.act[aria-pressed="true"] .ibtn{background:var(--accent);color:var(--on-accent);}
.act[aria-pressed="true"] .i{fill:currentColor;}
.hero-mark{position:absolute;left:2px;bottom:2px;width:var(--d);height:var(--d);}
@media (min-width:768px) and (max-width:1279px){.hero-lede{max-width:31ch;}}
@media (min-width:768px) and (max-height:820px){.hero-find > p, .feat-desc{display:none;}.hero-find{padding-top:26px;}.find-row{margin-top:16px;}.feat{padding-top:22px;}.spark{height:44px;margin-top:10px;}.hero-feat{--d:104px;}.feat-acts{margin-top:10px;}}
@media (max-width:1023px){.hero-find{display:none;}.hero-feat{width:min(420px, 60vw);}}
@media (max-width:767px){.bar{padding:78px calc(var(--frame) + 12px) 0;}.tab{left:calc(var(--frame) + var(--fillet));right:calc(var(--frame) + var(--fillet));width:auto;max-width:none;margin:0;justify-content:space-between;gap:10px;padding:calc(var(--frame) + 10px) 14px 12px;}.filter-btn{column-gap:6px;}.filter-label{font-size:10.5px;max-width:11ch;}.filter-label .i{display:none;}.filter-value{font-size:13.5px;max-width:9ch;}.filter-btn .chev{width:14px;height:14px;}.filter-menu{position:fixed;left:16px;right:16px;top:76px;min-width:0;}.pill-nav{min-width:0;min-height:42px;padding:4px 22px 4px 40px;font-size:14px;}.pill-nav .i{left:16px;}.pill-nav.to-r{padding:4px 40px 4px 22px;}.pill-nav.to-r .i{right:16px;}.hero-copy{top:150px;}.hero-title{font-size:clamp(44px, 15.5vw, 66px);}.hero-lede{margin:20px auto 0;text-align:center;font-size:15px;max-width:32ch;}.hero-feat{--d:76px;--gap:7px;left:calc(var(--frame) + 10px);right:calc(var(--frame) + 10px);bottom:84px;width:auto;}.feat{padding:20px 18px 16px 20px;}.feat-name{font-size:16px;}.feat-addr{font-size:12.5px;margin-top:4px;}.feat-top .ibtn{width:46px;height:46px;}.feat-desc{display:none;}.spark{height:40px;}.specs{margin:12px 0 0 calc(var(--d) - 6px);gap:6px 14px;font-size:12.5px;}.feat-acts{margin-top:10px;}.act .ibtn{width:40px;height:40px;}.act{font-size:10.5px;gap:3px;}}
@media (max-width:1023px){.bar{transition:transform .6s var(--ease);}.rail{top:auto;bottom:10px;left:0;right:0;margin-inline:auto;width:max-content;transform:none;flex-direction:row;gap:6px;padding:6px;background:var(--plate);border-radius:999px;box-shadow:var(--shadow), inset 0 0 0 1px var(--line);pointer-events:auto;}.rail .rail-g, .head.framed .rail .rail-plate, .head:not(.framed) .rail .rail-g{flex-direction:row;gap:6px;margin:0;padding:0;background:none;box-shadow:none;border-radius:0;}.rail .fil, .rail-me{display:none;}.ico{width:44px;height:44px;}.head.framed .rail-nav .ico{background:var(--mist);color:var(--text);-webkit-backdrop-filter:none;backdrop-filter:none;}.theme{flex-direction:row;padding:0;margin:0;background:none;}.theme .ico[aria-pressed="true"]{display:none;}.theme .ico{background:var(--mist);}}

/* ===== intro ===== */
.intro{padding-block:var(--pad) calc(var(--pad) * .8);}
.statement{font:400 clamp(29px, 3.9vw, 56px)/1.14 var(--f-display);letter-spacing:-.03em;}
.inl{display:inline-block;width:1.95em;height:.84em;border-radius:999px;overflow:hidden;vertical-align:-.07em;margin-inline:.06em;background:var(--g);}
.inl svg{display:block;width:100%;height:100%;}
.intro-foot{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:32px;margin-top:clamp(64px, 8vw, 112px);align-items:end;}
.intro-note{grid-column:1 / span 5;display:grid;gap:28px;justify-items:start;}
.intro-note p{color:var(--muted);max-width:42ch;}
.stats{grid-column:7 / -1;display:grid;grid-template-columns:repeat(auto-fit, minmax(130px, 1fr));gap:28px;}
.stats > div{display:flex;flex-direction:column-reverse;gap:10px;padding-top:20px;position:relative;container-type:inline-size;}
.stats > div::before{content:"";position:absolute;left:0;right:0;top:0;height:1px;background:var(--line);transform-origin:0 50%;transform:scaleX(var(--rule, 1));}
.stats dd{font:600 clamp(44px, 4.6vw, 68px)/.95 var(--f-display);font-size:min(clamp(44px, 4.6vw, 68px), 100cqi / var(--len, 1) * 1.63);letter-spacing:-.05em;}
.stats dt{color:var(--muted);font-size:14.5px;line-height:1.4;}
@media (max-width:900px){.intro-note, .stats{grid-column:1 / -1;}}
@media (max-width:767px){.stats{grid-template-columns:repeat(auto-fit, minmax(86px, 1fr));gap:18px;}.stats dd{font-size:min(38px, 100cqi / var(--len, 1) * 1.63);}.stats dt{font-size:12.5px;}}

/* ===== features stack ===== */
.homes{padding-block:calc(var(--pad) * .5) var(--pad);}
.sec-head{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:24px 32px;align-items:end;margin-bottom:clamp(44px, 5.5vw, 80px);}
.sec-head .h2{grid-column:1 / span 7;}
.sec-aside{grid-column:9 / -1;display:grid;gap:24px;justify-items:start;}
.sec-aside p{color:var(--muted);}
@media (max-width:900px){.sec-head .h2, .sec-aside{grid-column:1 / -1;}}
.stack{padding-inline:var(--inset);display:grid;gap:36px;}
.home{position:sticky;top:var(--stick);}
.home-card{--dim:0;position:relative;overflow:hidden;height:calc(100vh - 2 * var(--stick));height:calc(100svh - 2 * var(--stick));min-height:540px;max-height:820px;border-radius:var(--r-frame);transform-origin:50% 0;background:var(--night);}
.home-card::after{content:"";position:absolute;inset:0;z-index:4;background:black;opacity:var(--dim, 0);pointer-events:none;}
.home-card .win{left:4%;top:12%;right:34%;bottom:30%;}
.tag{position:absolute;left:26px;top:26px;display:inline-flex;align-items:center;gap:8px;padding:10px 18px;border-radius:999px;background:color-mix(in oklab, white 88%, transparent);color:var(--ink);font-size:14px;font-weight:600;white-space:nowrap;z-index:2;}
.tag .i{width:16px;height:16px;color:var(--amber);stroke-width:2.2;}
.home-plate{position:absolute;left:0;bottom:0;width:min(460px, 100%);padding:30px 30px 28px 30px;border-radius:0 var(--r-plate) 0 0;display:grid;grid-template-columns:minmax(0, 1fr) auto;gap:6px 20px;align-items:start;}
.home-plate .fil-tl{left:0;bottom:100%;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.home-plate .fil-br{left:100%;bottom:0;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.home-plate h3{font:600 clamp(24px, 2.2vw, 30px)/1.1 var(--f-display);letter-spacing:-.03em;overflow-wrap:break-word;}
.home-where{grid-column:1;display:flex;gap:7px;align-items:center;color:var(--muted);font-size:14.5px;}
.home-where .i{width:16px;height:16px;}
.home-price{grid-column:1 / -1;margin-top:14px;font:600 clamp(22px, 2vw, 28px)/1 var(--f-display);letter-spacing:-.03em;}
.home-price small{font:400 14px/1 var(--f-text);color:var(--muted);letter-spacing:0;}
.home-plate .ibtn{grid-column:2;grid-row:1 / span 2;width:56px;height:56px;}
.home-specs{position:absolute;right:22px;top:22px;width:min(290px, calc(100% - 44px));border-radius:28px;padding:18px 22px;display:grid;gap:12px;}
.home-specs li{display:flex;align-items:center;gap:12px;font-size:15px;}
.home-specs .i{color:var(--muted);}
.home-specs b{font-weight:600;}
@media (max-width:1100px){.home-card .win{right:4%;top:auto;height:44%;bottom:34%;}}
@media (max-width:767px){.home-card{height:calc(100svh - 96px);min-height:560px;}.home-card .win{left:12px;right:12px;top:236px;bottom:186px;height:auto;}.win{font-size:11.5px;}.win-body{padding:14px;}.wf-row, .wf-axis{grid-template-columns:96px minmax(0,1fr);gap:10px;font-size:11px;}.home-plate{width:calc(100% - 44px);padding:22px 20px 20px;}.home-plate .ibtn{width:48px;height:48px;}.home-specs{left:16px;right:auto;top:70px;width:auto;max-width:calc(100% - 32px);display:flex;flex-wrap:wrap;gap:8px 16px;padding:14px 16px;border-radius:22px;}.home-specs li{font-size:13px;gap:6px;}.home-specs .i{width:16px;height:16px;}.tag{left:16px;top:16px;}.tl li{grid-template-columns:58px 12px minmax(0,1fr);gap:8px;font-size:11.5px;}.mx-tip{left:auto;right:4px;}}

/* ===== integrations ===== */
.regions{padding-block:calc(var(--pad) * .6) var(--pad);}
.region-list{padding-inline:var(--inset);display:grid;gap:14px;}
.region-row{--pic-h:116px;display:grid;grid-template-columns:minmax(0, 1.1fr) minmax(0, .8fr) minmax(0, 1.3fr);align-items:center;gap:24px;min-height:136px;padding:10px 10px 10px 44px;border-radius:999px;background:var(--mist);transition:background-color .5s var(--ease);}
@media (hover:hover){.region-row:hover{background:color-mix(in oklab, var(--accent) 16%, var(--mist));}}
.region-name{font:400 clamp(30px, 3.6vw, 52px)/1.02 var(--f-display);letter-spacing:-.04em;overflow-wrap:anywhere;}
.region-meta{display:grid;gap:2px;color:var(--muted);font-size:15px;line-height:1.4;}
.region-meta b{color:var(--text);font-weight:600;}
.region-pic{position:relative;height:var(--pic-h);border-radius:999px;overflow:hidden;background:var(--g);}
.glyphs{position:absolute;inset:0;display:flex;align-items:center;gap:12px;padding:0 calc(var(--pic-h) + 4px) 0 26px;}
.glyphs span{flex:none;width:52px;height:52px;border-radius:16px;display:grid;place-items:center;font:500 14px/1 var(--f-mono);color:white;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.22);-webkit-backdrop-filter:blur(6px);backdrop-filter:blur(6px);}
.glyphs span:nth-child(2n){transform:translateY(-10px);}
.region-pic .ibtn{position:absolute;right:calc((var(--pic-h) - 60px) / 2);top:50%;margin-top:-30px;width:60px;height:60px;background:white;color:var(--ink);}
.motion .region-pic{clip-path:inset(0 0 0 calc(100% - var(--pic-h)) round 999px);}
@media (max-width:767px){.region-row{--pic-h:84px;grid-template-columns:minmax(0, 1fr) 40%;gap:6px 14px;min-height:0;padding:18px 8px 18px 24px;border-radius:44px;}.region-name{grid-column:1;font-size:26px;}.region-meta{grid-column:1;font-size:13px;}.region-pic{grid-column:2;grid-row:1 / span 2;}.region-pic .ibtn{width:44px;height:44px;margin-top:-22px;right:20px;}.glyphs span{width:38px;height:38px;border-radius:12px;font-size:11px;}}

/* ===== product tour bento ===== */
.gallery{padding-block:calc(var(--pad) * .5) var(--pad);}
.bento{padding-inline:var(--inset);display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));grid-auto-rows:clamp(180px, 20vw, 270px);gap:16px;}
.tile{position:relative;overflow:hidden;border-radius:var(--r-plate);background:#0d0b1c;color:#e7e5f5;font:400 12.5px/1.5 var(--f-mono);box-shadow:inset 0 0 0 1px rgba(255,255,255,.06);}
.tile-in{position:absolute;inset:0;padding:22px 24px 58px;display:flex;flex-direction:column;gap:12px;overflow:hidden;}
.tile-h{display:flex;justify-content:space-between;gap:10px;color:rgba(231,229,245,.55);font-size:11.5px;letter-spacing:.06em;text-transform:uppercase;white-space:nowrap;}
.g1{grid-column:1 / 8;grid-row:1 / 3;}.g2{grid-column:8 / 13;grid-row:1 / 2;}.g3{grid-column:8 / 11;grid-row:2 / 4;}.g4{grid-column:11 / 13;grid-row:2 / 4;}.g5{grid-column:1 / 8;grid-row:3 / 4;}
.map{position:absolute;inset:0;width:100%;height:100%;}
.map text{font:500 12px var(--f-mono);fill:#e7e5f5;}
.map .halo{transform-box:fill-box;transform-origin:center;animation:pulse 2.4s var(--ease-out) infinite;}
.log p{white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.lv{display:inline-block;width:46px;}
.lv.info{color:var(--sky);}.lv.warn{color:var(--amber);}.lv.err{color:var(--rose);}.lv.ok{color:var(--mint);}
.cursor{display:inline-block;width:8px;height:14px;vertical-align:-2px;background:var(--violet);animation:blink 1s steps(1) infinite;}
.heat{flex:1;display:grid;grid-template-columns:repeat(10, 1fr);gap:3px;background:linear-gradient(180deg, color-mix(in oklab, var(--amber) 25%, transparent), color-mix(in oklab, var(--violet) 30%, transparent));border-radius:8px;}
.heat:has(i){background:none;}
.heat i{border-radius:3px;background:color-mix(in oklab, var(--amber) calc(var(--v) * 100%), var(--violet));opacity:calc(.1 + var(--v) * .9);}
.slo{display:grid;gap:16px;}
.slo li{display:grid;gap:7px;}
.slo div{display:flex;justify-content:space-between;}
.slo div b{font-weight:500;color:var(--c);}
.slo .bar{display:block !important;height:8px !important;min-height:0;padding:0 !important;border-radius:8px;background:linear-gradient(90deg, var(--c) var(--p), rgba(255,255,255,.07) var(--p));box-shadow:0 0 16px -6px var(--c);}

.code{font-size:13px;line-height:1.75;}
.code .k{color:var(--violet);}.code .s{color:var(--mint);}.code .n{color:var(--amber);}.code .f{color:var(--sky);}.code .ln{display:inline-block;width:26px;color:rgba(231,229,245,.3);}
.chip{align-self:flex-start;padding:6px 12px;border-radius:999px;background:rgba(255,255,255,.07);color:rgba(231,229,245,.7);font-size:11.5px;}
.cap{--fillet:20px;position:absolute;left:0;bottom:0;max-width:calc(100% - 40px);padding:12px 22px 10px 20px;border-radius:0 22px 0 0;font:500 14px/1.35 var(--f-text);}
.cap .fil-tl{left:0;bottom:100%;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.cap .fil-br{left:100%;bottom:0;background:radial-gradient(circle at 100% 0, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
@media (max-width:767px){.bento{grid-template-columns:repeat(2, minmax(0, 1fr));grid-auto-rows:150px;gap:10px;}.g1{grid-column:1 / 3;grid-row:1 / 3;}.g2{grid-column:1 / 3;grid-row:3 / 4;}.g3{grid-column:1 / 2;grid-row:4 / 6;}.g4{grid-column:2 / 3;grid-row:4 / 6;}.g5{grid-column:1 / 3;grid-row:6 / 8;}.cap{font-size:12.5px;padding:9px 16px 8px 14px;}.tile-in{padding:16px 16px 48px;}.tile{font-size:11px;}.code{font-size:11px;}}

/* ===== process ===== */
.proc-stage{position:relative;min-height:100vh;min-height:100svh;display:grid;align-content:space-between;gap:48px;padding:calc(var(--frame) + 116px) var(--inset) calc(var(--frame) + 26px);}
.proc-shot{position:absolute;inset:var(--frame);overflow:hidden;border-radius:var(--r-frame);background:var(--night);}
.radar{position:absolute;right:-12%;top:50%;width:min(110vh, 90vw);aspect-ratio:1;transform:translateY(-50%);}
.radar svg{position:absolute;inset:0;width:100%;height:100%;}
.sweep{position:absolute;inset:0;border-radius:50%;background:conic-gradient(from 0deg, color-mix(in oklab, var(--violet) 55%, transparent), transparent 22%);animation:spin 7s linear infinite;-webkit-mask:radial-gradient(circle, black 69%, transparent 70%);mask:radial-gradient(circle, black 69%, transparent 70%);}
.proc-shot::after{content:"";position:absolute;inset:0;background:linear-gradient(180deg, color-mix(in oklab, var(--night) 55%, transparent), transparent 46%), linear-gradient(0deg, color-mix(in oklab, var(--night) 40%, transparent), transparent 40%);}
.proc-title{position:relative;max-width:14ch;color:var(--on-photo);}
.proc-lens{--d:112px;--gap:9px;position:relative;width:min(480px, 100%);}
.proc-card{border-radius:var(--r-plate);padding:30px 30px 20px;}
.proc-step{display:grid;gap:10px;}
.proc-steps{display:grid;gap:34px;}
.proc-step h3{font:600 clamp(22px, 2vw, 27px)/1.15 var(--f-display);letter-spacing:-.03em;}
.proc-step p{color:var(--muted);font-size:15.5px;}
.proc-step .proc-time{display:flex;align-items:center;justify-content:flex-end;gap:8px;min-height:calc(var(--d) - 12px);margin-left:calc(var(--d) + 8px);color:var(--text);font:500 13.5px var(--f-mono);}
.proc-time .i{width:18px;height:18px;color:var(--muted);}
.proc-disc{position:absolute;left:2px;bottom:2px;width:var(--d);height:var(--d);}
.proc-disc .ring{position:absolute;inset:7px;width:calc(100% - 14px);height:calc(100% - 14px);transform:rotate(-90deg);stroke:currentColor;}
.ring circle{fill:none;stroke-width:3;}.ring .ring-bg{opacity:.22;}.ring .ring-fg{stroke:var(--amber);stroke-linecap:round;stroke-dasharray:1;stroke-dashoffset:0;}
.proc-disc > svg:last-child{width:38%;height:38%;}
.motion .proc-steps{gap:0;}.motion .proc-step{grid-area:1 / 1;}
.motion .mate-pic{clip-path:inset(100% 0 0 0);}
.motion .contact-shot{clip-path:circle(0% at 12% 88%);}
@media (max-width:767px){.proc-stage{padding-top:calc(var(--frame) + 104px);padding-bottom:calc(var(--frame) + 84px);}.proc-lens{--d:84px;--gap:7px;}.proc-card{padding:22px 20px 16px;}.proc-step p{font-size:14.5px;}.radar{right:-40%;top:38%;width:130vw;}}

/* ===== pricing ===== */
.pricing{padding-block:var(--pad);}
.seg{position:relative;isolation:isolate;display:inline-grid;grid-auto-flow:column;grid-auto-columns:1fr;padding:6px;border-radius:999px;background:var(--mist);}
.seg button{position:relative;z-index:1;min-height:52px;padding:0 28px;border-radius:999px;font-weight:600;font-size:15px;white-space:nowrap;color:var(--muted);transition:color .5s var(--ease);}
.seg button small{font:500 11px var(--f-mono);margin-left:6px;color:var(--mint);}
.seg button[aria-pressed="true"]{color:var(--on-accent);}
.seg button[aria-pressed="true"] small{color:inherit;}
.seg-thumb{position:absolute;z-index:0;left:6px;top:6px;bottom:6px;width:calc((100% - 12px) / var(--n, 2));border-radius:999px;background:var(--accent);transform:translateX(calc(var(--i, 0) * 100%));transition:transform .65s var(--ease);}
.plans{padding-inline:var(--inset);display:grid;grid-template-columns:repeat(auto-fit, minmax(270px, 1fr));gap:16px;}
.plan{position:relative;display:flex;flex-direction:column;gap:16px;padding:34px 32px 32px;border-radius:var(--r-plate);background:var(--card);box-shadow:inset 0 0 0 1px var(--line);}
.plan h3{font:600 24px/1.15 var(--f-display);letter-spacing:-.02em;}
.plan-for{color:var(--muted);font-size:15px;margin-top:-8px;}
.plan-fee{margin-top:22px;font:500 clamp(44px, 4.4vw, 66px)/1 var(--f-display);letter-spacing:-.05em;overflow-wrap:anywhere;}
.plan-note{color:var(--muted);font-size:14.5px;margin-top:-6px;}
.plan-list{display:grid;gap:12px;margin-top:8px;padding-top:22px;border-top:1px solid var(--line);}
.plan-list li{display:flex;gap:10px;font-size:15px;line-height:1.45;}
.plan-list .i{color:var(--accent);stroke-width:2.2;}
.plan .btn{margin-top:auto;align-self:flex-start;}.plan-list + .btn{margin-top:12px;}
.plan-hi{background:radial-gradient(120% 80% at 100% 0, color-mix(in oklab, var(--sky) 40%, transparent), transparent 60%), var(--accent);color:var(--on-accent);box-shadow:0 40px 80px -40px var(--accent);}
.plan-hi .plan-for, .plan-hi .plan-note{color:color-mix(in oklab, var(--on-accent) 70%, var(--accent));}
.plan-hi .plan-list{border-color:color-mix(in oklab, var(--on-accent) 22%, transparent);}
.plan-hi .plan-list .i{color:var(--on-accent);}
.plan-hi .btn{background:var(--on-accent);color:var(--accent);box-shadow:none;}.plan-hi .btn::before{background:var(--amber);}.plan-hi .btn-dot{background:var(--amber);color:var(--ink);}
@media (hover:hover){.plan-hi .btn:hover{color:var(--ink);}.plan-hi .btn:hover .btn-dot{background:var(--on-accent);color:var(--accent);}}
.swap{display:inline-block;}

/* ===== team ===== */
.team{padding-block:calc(var(--pad) * .4) var(--pad);}
.crew{padding-inline:var(--inset);display:grid;grid-template-columns:repeat(auto-fit, minmax(230px, 1fr));gap:40px 16px;}
.mate{display:grid;gap:18px;align-content:start;}
.mate-pic{position:relative;overflow:hidden;aspect-ratio:3 / 4;border-radius:50% 50% var(--r-plate) var(--r-plate) / 37.5% 37.5% var(--r-plate) var(--r-plate);background:var(--night);}
.portrait{position:absolute;inset:0;display:grid;place-items:center;color:white;font:400 clamp(64px, 7vw, 104px)/1 var(--f-serif);font-style:italic;letter-spacing:-.02em;background:radial-gradient(circle at 30% 22%, hsl(var(--h) 90% 70% / .95), transparent 55%),radial-gradient(circle at 78% 82%, hsl(calc(var(--h) + 55) 85% 58% / .85), transparent 60%),#0d0b1c;}
.portrait::before, .portrait::after{content:"";position:absolute;border-radius:50%;border:1px solid rgba(255,255,255,.22);}
.portrait::before{width:62%;aspect-ratio:1;}
.portrait::after{width:92%;aspect-ratio:1;border-style:dashed;border-color:rgba(255,255,255,.14);}
.mate-row{display:flex;gap:14px;align-items:flex-start;justify-content:space-between;}
.mate h3{font:600 21px/1.2 var(--f-display);letter-spacing:-.02em;}
.mate p{color:var(--muted);font-size:14.5px;margin-top:4px;}
@media (max-width:767px){.crew{grid-template-columns:repeat(2, minmax(0, 1fr));gap:32px 12px;}.mate h3{font-size:17px;}.mate p{font-size:13px;}.mate-row .ibtn{width:40px;height:40px;}}

/* ===== reviews ===== */
.rev-stage{position:relative;padding:calc(var(--frame) + clamp(72px, 9vw, 128px)) 0 calc(var(--frame) + clamp(40px, 5vw, 64px));overflow:hidden;}
.rev-shot{position:absolute;inset:var(--frame);overflow:hidden;border-radius:var(--r-frame);background:var(--night);}
.rev-shot::after{content:"";position:absolute;inset:0;background:linear-gradient(180deg, color-mix(in oklab, var(--night) 45%, transparent), color-mix(in oklab, var(--night) 15%, transparent));}
.rev-head{position:relative;padding-inline:var(--inset);display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:24px 32px;align-items:end;margin-bottom:clamp(44px, 6vw, 88px);color:var(--on-photo);}
.rev-head .h2{grid-column:1 / span 7;}
.rev-score{grid-column:9 / -1;justify-self:end;display:flex;align-items:flex-end;gap:16px;}
.rev-score strong{font:500 clamp(64px, 7.4vw, 108px)/.82 var(--f-display);letter-spacing:-.06em;}
.rev-score span{max-width:15ch;font-size:15px;line-height:1.4;color:color-mix(in oklab, var(--on-photo) 82%, transparent);}
@media (max-width:900px){.rev-head .h2, .rev-score{grid-column:1 / -1;justify-self:start;}}
.rev-row{position:relative;}
.rev-track{display:flex;flex-wrap:wrap;gap:16px;padding-inline:var(--inset);}
.motion .rev-track{flex-wrap:nowrap;width:max-content;gap:0;padding-inline:0;}
.motion .rev{margin-right:16px;}
.rev{flex:none;width:min(410px, 84vw);display:grid;gap:26px;align-content:space-between;padding:30px 30px 24px;border-radius:30px;}
.rev blockquote{font:400 clamp(17px, 1.4vw, 19px)/1.5 var(--f-display);letter-spacing:-.01em;}
.rev figcaption{display:flex;gap:12px;align-items:center;font-size:13.5px;color:var(--muted);line-height:1.35;}
.rev figcaption .av{width:44px;height:44px;flex:none;}
.rev figcaption b{display:block;color:var(--text);font-size:15px;font-weight:600;}

/* ===== faq ===== */
.faq{padding-block:var(--pad);}
.faq-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:40px 32px;align-items:start;}
.faq-side{grid-column:1 / span 5;position:sticky;top:130px;display:grid;gap:26px;justify-items:start;}
.faq-list{grid-column:7 / -1;display:grid;gap:10px;}
.qa{border-radius:30px;background:var(--card);box-shadow:inset 0 0 0 1px var(--line);transition:background-color .5s var(--ease);}
.qa[open]{background:var(--mist);}
.qa summary{list-style:none;display:flex;align-items:center;justify-content:space-between;gap:20px;padding:14px 14px 14px 28px;cursor:pointer;font:500 clamp(17px, 1.45vw, 20px)/1.35 var(--f-display);letter-spacing:-.015em;}
.qa summary::-webkit-details-marker{display:none;}
.qa summary .i{transition:transform .5s var(--ease);}
.qa[open] summary .i{transform:rotate(45deg);}
.qa-body{padding:2px 28px 26px;color:var(--muted);max-width:62ch;}
.qa-body code{font:500 .9em var(--f-mono);color:var(--text);}
.qa[open] .qa-body{animation:qa-in .6s var(--ease-out);}
@keyframes qa-in{from{opacity:0;transform:translateY(-10px);}}
@media (max-width:900px){.faq-side{grid-column:1 / -1;position:static;}.faq-list{grid-column:1 / -1;}}
@media (max-width:767px){.qa summary{padding-left:22px;}.qa-body{padding-inline:22px;}}

/* ===== security ===== */
.sell{padding-block:calc(var(--pad) * .3) var(--pad);}
.sell-stage{position:relative;min-height:min(92vh, 860px);min-height:min(92svh, 860px);}
.sell-shot{--close:1;position:absolute;inset:0;overflow:hidden;clip-path:inset(0 calc(var(--inset) * var(--close)) round calc(var(--r-frame) * var(--close)));background:var(--night);}
.sell-shot .dots{position:absolute;inset:0;opacity:.35;-webkit-mask-image:radial-gradient(70% 70% at 72% 50%, black, transparent 75%);mask-image:radial-gradient(70% 70% at 72% 50%, black, transparent 75%);}
.shield{position:absolute;right:calc(var(--inset) + 6%);top:50%;width:min(36vw, 420px);transform:translateY(-50%);filter:drop-shadow(0 0 40px color-mix(in oklab, var(--violet) 60%, transparent));}
.sell-plate{position:absolute;left:var(--inset);top:0;width:min(580px, calc(100% - 2 * var(--inset) - var(--fillet)));display:grid;gap:22px;justify-items:start;padding:clamp(32px, 3.4vw, 48px) clamp(28px, 3.4vw, 48px) clamp(32px, 3.4vw, 44px) clamp(28px, 3vw, 40px);border-radius:0 0 var(--r-plate) 0;}
.sell-plate .fil-tr{left:100%;top:0;background:radial-gradient(circle at 100% 100%, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.sell-plate .fil-bl{left:0;top:100%;background:radial-gradient(circle at 100% 100%, transparent calc(var(--fillet) - .6px), var(--plate) var(--fillet));}
.sell-plate p{color:var(--muted);max-width:42ch;}
.sell-facts{position:absolute;left:calc(var(--inset) + 22px);bottom:22px;display:flex;flex-wrap:wrap;justify-content:flex-start;gap:12px;max-width:calc(100% - 2 * var(--inset) - 44px);}
.sell-facts li{display:grid;gap:6px;min-width:190px;padding:20px 24px;border-radius:28px;}
.sell-facts strong{font:500 clamp(40px, 3.8vw, 56px)/.9 var(--f-display);letter-spacing:-.05em;}
.sell-facts span{font-size:14px;color:var(--muted);max-width:18ch;}
@media (max-width:767px){.sell-stage{min-height:760px;}.shield{width:62vw;right:8%;top:62%;opacity:.7;}.sell-facts{left:calc(var(--inset) + 12px);right:calc(var(--inset) + 12px);bottom:12px;max-width:none;justify-content:stretch;}.sell-facts li{flex:1 1 0;min-width:0;padding:16px 18px;}.sell-facts strong{font-size:32px;}.sell-facts span{font-size:12.5px;}}

/* ===== contact ===== */
.contact{padding-block:calc(var(--pad) * .4) var(--pad);}
.contact-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:40px 16px;align-items:stretch;}
.contact-main{grid-column:1 / span 7;display:grid;gap:clamp(32px, 4vw, 56px);align-content:start;}
.cform{display:grid;grid-template-columns:repeat(2, minmax(0, 1fr));gap:20px 16px;padding:clamp(24px, 3vw, 40px);border-radius:var(--r-plate);background:var(--card);box-shadow:inset 0 0 0 1px var(--line);}
.field{display:grid;gap:8px;}
.field-wide, .chips, .cform-end{grid-column:1 / -1;}
.field label, .chips legend{font-size:14px;color:var(--muted);}
.field label span{opacity:.7;}
.field input, .field textarea{width:100%;border:1.5px solid transparent;outline:none;background:var(--mist);color:var(--text);border-radius:999px;padding:15px 22px;font-size:16px;transition:border-color .3s;}
.field textarea{border-radius:26px;resize:vertical;min-height:120px;}
.field input:focus, .field textarea:focus{border-color:var(--accent);}
.chips{border:0;margin:0;padding:0;display:flex;flex-wrap:wrap;gap:8px;}
.chips legend{padding:0;margin-bottom:10px;}
.chips label{position:relative;cursor:pointer;}
.chips input{position:absolute;opacity:0;inset:0;cursor:pointer;}
.chips span{display:inline-flex;align-items:center;min-height:46px;padding:0 22px;border-radius:999px;background:var(--mist);font-size:15px;font-weight:500;white-space:nowrap;transition:background-color .4s, color .4s;}
.chips input:checked + span{background:var(--accent);color:var(--on-accent);}
.chips input:focus-visible + span{outline:2px solid var(--accent);outline-offset:3px;}
.cform-end{display:flex;flex-wrap:wrap;align-items:center;gap:16px 24px;margin-top:6px;}
.cform-done{color:var(--text);font-weight:500;}
.contact-side{grid-column:8 / -1;position:relative;min-height:620px;border-radius:var(--r-frame);overflow:hidden;}
.contact-shot{position:absolute;inset:0;background:var(--night);}
.contact-shot .win{left:22px;right:22px;top:22px;height:52%;}
.term p{white-space:nowrap;overflow:hidden;text-overflow:ellipsis;}
.term .p{color:var(--violet);}.term .ok{color:var(--mint);}
.contact-wrap{--d:104px;--gap:9px;position:absolute;left:16px;right:16px;bottom:16px;}
.contact-card{border-radius:28px;padding:26px 26px 18px;display:grid;gap:8px;}
.contact-card h3{font:600 22px/1.2 var(--f-display);letter-spacing:-.02em;}
.contact-card address{font-style:normal;color:var(--muted);}
.contact-list{display:grid;gap:6px;margin:10px 0 0 calc(var(--d) + 4px);min-height:calc(var(--d) - 14px);align-content:end;font-size:15px;}
.contact-list li{display:flex;gap:10px;align-items:center;}
.contact-list .i{width:18px;height:18px;color:var(--muted);}
.contact-wrap .disc{position:absolute;left:2px;bottom:2px;width:var(--d);height:var(--d);}
@media (max-width:900px){.contact-main, .contact-side{grid-column:1 / -1;}}
@media (max-width:767px){.cform{grid-template-columns:minmax(0, 1fr);}.contact-side{min-height:580px;}.contact-shot .win{left:12px;right:12px;top:12px;height:46%;}.contact-wrap{--d:84px;--gap:7px;left:10px;right:10px;bottom:10px;}.contact-list{font-size:14px;}}

/* ===== footer ===== */
.foot{padding:var(--pad) var(--frame) var(--frame);}
.foot-panel{position:relative;overflow:hidden;background:radial-gradient(60% 80% at 100% 0, color-mix(in oklab, var(--violet) 40%, transparent), transparent 60%), radial-gradient(50% 70% at 0 100%, color-mix(in oklab, var(--amber) 22%, transparent), transparent 60%), #120f2a;color:var(--paper);border-radius:var(--r-frame);padding:clamp(44px, 6vw, 88px) calc(var(--inset) - var(--frame)) 28px;}
.foot-top{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:40px 32px;}
.foot-news{grid-column:1 / span 5;display:grid;gap:26px;align-content:start;}
.foot-news h2{font:500 clamp(28px, 2.8vw, 40px)/1.08 var(--f-display);letter-spacing:-.03em;}
.news{display:flex;align-items:center;gap:8px;padding:6px 6px 6px 22px;border-radius:999px;background:color-mix(in oklab, var(--paper) 12%, transparent);max-width:420px;}
.news input{flex:1;min-width:0;border:0;background:none;outline:none;color:var(--paper);font-size:15px;padding:12px 0;}
.news input::placeholder{color:color-mix(in oklab, var(--paper) 62%, transparent);}
.news .ibtn{background:var(--paper);color:var(--indigo);}.news .ibtn::before{background:var(--amber);}
.news-done{font-size:14px;color:color-mix(in oklab, var(--paper) 80%, transparent);min-height:1.4em;}
.foot-links{grid-column:7 / -1;display:grid;grid-template-columns:repeat(auto-fit, minmax(140px, 1fr));gap:28px;}
.foot-links h3{font-size:14px;font-weight:500;color:color-mix(in oklab, var(--paper) 58%, transparent);margin-bottom:14px;}
.foot-links li + li{margin-top:8px;}.foot-links a{font-size:16px;}
.wordmark{margin-top:clamp(56px, 8vw, 120px);font:600 calc((100vw - 2 * var(--inset)) / var(--len) * 2.08)/.78 var(--f-display);letter-spacing:-.065em;white-space:nowrap;color:var(--paper);background:linear-gradient(180deg, var(--paper) 40%, color-mix(in oklab, var(--paper) 20%, transparent));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent;}
.foot-base{display:flex;flex-wrap:wrap;gap:10px 28px;justify-content:space-between;margin-top:clamp(28px, 3vw, 44px);padding-top:22px;border-top:1px solid color-mix(in oklab, var(--paper) 18%, transparent);font-size:14px;color:color-mix(in oklab, var(--paper) 70%, transparent);}
.status{display:inline-flex;align-items:center;gap:8px;}.status::before{content:"";width:7px;height:7px;border-radius:50%;background:var(--mint);}
@media (max-width:900px){.foot-news, .foot-links{grid-column:1 / -1;}}
@media (max-width:1023px){.foot{padding-bottom:calc(var(--frame) + 74px);}}
.motion .inl{clip-path:inset(0 50% round 999px);}
.motion .stats > div{--rule:0;}
@media (prefers-reduced-motion:reduce){*, *::before, *::after{transition:none !important;animation:none !important;}}
::view-transition-old(root), ::view-transition-new(root){animation:none;mix-blend-mode:normal;}
</style>
</head>
<body>
<svg class="sprite" aria-hidden="true">
  <symbol id="i-ne" viewBox="0 0 24 24"><path d="M7 17 17 7M9 7h8v8"/></symbol>
  <symbol id="i-nw" viewBox="0 0 24 24"><path d="M17 17 7 7M15 7H7v8"/></symbol>
  <symbol id="i-right" viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"/></symbol>
  <symbol id="i-down" viewBox="0 0 24 24"><path d="m6 9 6 6 6-6"/></symbol>
  <symbol id="i-layers" viewBox="0 0 24 24"><path d="m12 4 8 4-8 4-8-4z"/><path d="m4 12 8 4 8-4M4 16l8 4 8-4"/></symbol>
  <symbol id="i-globe" viewBox="0 0 24 24"><circle cx="12" cy="12" r="8"/><path d="M4 12h16M12 4c2.5 2.6 2.5 13.4 0 16M12 4c-2.5 2.6-2.5 13.4 0 16"/></symbol>
  <symbol id="i-server" viewBox="0 0 24 24"><rect x="4" y="4" width="16" height="6.5" rx="2"/><rect x="4" y="13.5" width="16" height="6.5" rx="2"/><path d="M8 7.25h.01M8 16.75h.01"/></symbol>
  <symbol id="i-home" viewBox="0 0 24 24"><path d="M4 10.5 12 4l8 6.5V20a1 1 0 0 1-1 1h-4.5v-6h-5v6H5a1 1 0 0 1-1-1z"/></symbol>
  <symbol id="i-chart" viewBox="0 0 24 24"><path d="M4 20h16M7 16v-5M12 16V7M17 16v-8"/></symbol>
  <symbol id="i-grid" viewBox="0 0 24 24"><rect x="4" y="4" width="6.5" height="6.5" rx="2"/><rect x="13.5" y="4" width="6.5" height="6.5" rx="2"/><rect x="4" y="13.5" width="6.5" height="6.5" rx="2"/><rect x="13.5" y="13.5" width="6.5" height="6.5" rx="2"/></symbol>
  <symbol id="i-chat" viewBox="0 0 24 24"><path d="M5 5h14a1 1 0 0 1 1 1v10a1 1 0 0 1-1 1h-8l-5 3.5V17H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1z"/><path d="M9 11h6"/></symbol>
  <symbol id="i-bell" viewBox="0 0 24 24"><path d="M6 16v-5a6 6 0 0 1 12 0v5l1.5 2h-15z"/><path d="M10 20.5a2 2 0 0 0 4 0"/></symbol>
  <symbol id="i-phone" viewBox="0 0 24 24"><path d="M6.5 4h3l1.5 4-2 1.3a10 10 0 0 0 5.7 5.7l1.3-2 4 1.5v3a2 2 0 0 1-2.2 2A16 16 0 0 1 4.5 6.2 2 2 0 0 1 6.5 4z"/></symbol>
  <symbol id="i-moon" viewBox="0 0 24 24"><path d="M19.5 14.5A7.5 7.5 0 0 1 9.5 4.5a7.5 7.5 0 1 0 10 10z"/></symbol>
  <symbol id="i-sun" viewBox="0 0 24 24"><circle cx="12" cy="12" r="4"/><path d="M12 2.5v2M12 19.5v2M2.5 12h2M19.5 12h2M5.3 5.3l1.4 1.4M17.3 17.3l1.4 1.4M5.3 18.7l1.4-1.4M17.3 6.7l1.4-1.4"/></symbol>
  <symbol id="i-eye" viewBox="0 0 24 24"><path d="M2.5 12S6 5.5 12 5.5 21.5 12 21.5 12 18 18.5 12 18.5 2.5 12 2.5 12z"/><circle cx="12" cy="12" r="2.8"/></symbol>
  <symbol id="i-save" viewBox="0 0 24 24"><path d="M7 4h10v16l-5-3.5L7 20z"/></symbol>
  <symbol id="i-share" viewBox="0 0 24 24"><path d="m14 5 6 6-6 6M20 11h-8a7 7 0 0 0-7 7"/></symbol>
  <symbol id="i-bolt" viewBox="0 0 24 24"><path d="M13 3 5 13.5h6L10 21l8-10.5h-6z"/></symbol>
  <symbol id="i-shield" viewBox="0 0 24 24"><path d="M12 3.5 19 6v5.5c0 4.4-3 7.9-7 9-4-1.1-7-4.6-7-9V6z"/><path d="m9 12 2.2 2.2L15.5 10"/></symbol>
  <symbol id="i-code" viewBox="0 0 24 24"><path d="m9 8-4 4 4 4M15 8l4 4-4 4"/></symbol>
  <symbol id="i-users" viewBox="0 0 24 24"><circle cx="9" cy="9" r="3.2"/><path d="M3.5 19a5.5 5.5 0 0 1 11 0M16 6.2a3 3 0 0 1 0 5.6M17.5 14.2A5 5 0 0 1 20.5 19"/></symbol>
  <symbol id="i-plus" viewBox="0 0 24 24"><path d="M12 5v14M5 12h14"/></symbol>
  <symbol id="i-check" viewBox="0 0 24 24"><path d="m5 12.5 4.5 4.5L19 7.5"/></symbol>
  <symbol id="i-mail" viewBox="0 0 24 24"><rect x="3.5" y="5.5" width="17" height="13" rx="2.5"/><path d="m4.5 7.5 7.5 5.5 7.5-5.5"/></symbol>
  <symbol id="i-clock" viewBox="0 0 24 24"><circle cx="12" cy="12" r="8"/><path d="M12 8v4.5l3 1.5"/></symbol>
  <symbol id="i-mark" viewBox="0 0 64 64"><path d="M12 54V30a20 20 0 0 1 40 0v24M25 54V36a7 7 0 0 1 14 0v18"/></symbol>
</svg>

<header class="head framed" data-head data-section="nav">
  <div class="bar">
    <a class="btn pill-nav" href="#features"><svg class="i"><use href="#i-nw"/></svg><span>Product</span></a>
    <div class="tab">
      <span class="fil fil-tl"></span><span class="fil fil-tr"></span>
      <div class="filter" data-filter="env">
        <button class="filter-btn" type="button" aria-expanded="false">
          <span class="filter-label"><svg class="i"><use href="#i-layers"/></svg>Environment</span>
          <span class="filter-value">Production</span>
          <svg class="i chev"><use href="#i-down"/></svg>
        </button>
        <ul class="filter-menu" role="listbox" aria-label="Environment">
          <li><button type="button" role="option" aria-selected="true">Production</button></li>
          <li><button type="button" role="option">Staging</button></li>
          <li><button type="button" role="option">Development</button></li>
        </ul>
      </div>
      <div class="filter" data-filter="region">
        <button class="filter-btn" type="button" aria-expanded="false">
          <span class="filter-label"><svg class="i"><use href="#i-globe"/></svg>Region</span>
          <span class="filter-value">US West</span>
          <svg class="i chev"><use href="#i-down"/></svg>
        </button>
        <ul class="filter-menu" role="listbox" aria-label="Region">
          <li><button type="button" role="option" aria-selected="true">US West</button></li>
          <li><button type="button" role="option">US East</button></li>
          <li><button type="button" role="option">EU Central</button></li>
          <li><button type="button" role="option">Asia Pacific</button></li>
        </ul>
      </div>
      <div class="filter" data-filter="range">
        <button class="filter-btn" type="button" aria-expanded="false">
          <span class="filter-label"><svg class="i"><use href="#i-clock"/></svg>Time range</span>
          <span class="filter-value">Last 24 hours</span>
          <svg class="i chev"><use href="#i-down"/></svg>
        </button>
        <ul class="filter-menu" role="listbox" aria-label="Time range">
          <li><button type="button" role="option">Last hour</button></li>
          <li><button type="button" role="option" aria-selected="true">Last 24 hours</button></li>
          <li><button type="button" role="option">Last 7 days</button></li>
          <li><button type="button" role="option">Last 30 days</button></li>
        </ul>
      </div>
    </div>
    <a class="btn pill-nav to-r" href="#pricing" data-mode="annual"><span>Pricing</span><svg class="i"><use href="#i-ne"/></svg></a>
  </div>

  <nav class="rail" aria-label="Page">
    <div class="rail-g rail-nav">
      <a class="ico is-on" href="#home" aria-label="Home"><svg class="i"><use href="#i-home"/></svg></a>
      <a class="ico" href="#features" aria-label="Features"><svg class="i"><use href="#i-layers"/></svg></a>
      <a class="ico" href="#gallery" aria-label="Product tour"><svg class="i"><use href="#i-grid"/></svg></a>
      <a class="ico" href="#contact" aria-label="Book a demo"><svg class="i"><use href="#i-chat"/></svg></a>
    </div>
    <div class="rail-g rail-plate rail-me">
      <span class="fil fil-tl"></span><span class="fil fil-bl"></span>
      <a class="ava" href="#team" aria-label="Your solutions engineer"><span class="av" style="--h:262">PC</span></a>
      <a class="ico" href="#alerts" aria-label="Changelog updates"><svg class="i"><use href="#i-bell"/></svg></a>
    </div>
    <div class="rail-g rail-plate rail-set">
      <span class="fil fil-tl"></span><span class="fil fil-bl"></span>
      <a class="ico" href="tel:+14155550142" aria-label="Call sales"><svg class="i"><use href="#i-phone"/></svg></a>
      <div class="theme" role="group" aria-label="Colour theme">
        <button class="ico" type="button" data-theme="dark" aria-pressed="true" aria-label="Dark theme"><svg class="i"><use href="#i-moon"/></svg></button>
        <button class="ico" type="button" data-theme="light" aria-pressed="false" aria-label="Light theme"><svg class="i"><use href="#i-sun"/></svg></button>
      </div>
    </div>
  </nav>
</header>

<main>
  <section id="home" data-section="hero" data-kind="hero" class="hero">
    <div class="hero-shot">
      <div class="hero-drift">
        <div class="art aurora hero-art">
          <div class="fibers" data-fibers></div>
        </div>
      </div>
    </div>
    <div class="hero-copy">
      <h1 class="hero-title"><span>See every</span> <span><em>signal.</em></span></h1>
      <p class="hero-lede">Mirador brings traces, metrics and logs into one calm view, so your team finds the cause before customers notice the bug.</p>
    </div>
    <aside class="hero-find plate">
      <span class="fil fil-bl"></span><span class="fil fil-br"></span>
      <h2 class="find-title">Trusted by teams who ship daily</h2>
      <p>From two-person startups to platforms serving billions of requests, teams run production on Mirador.</p>
      <div class="find-row">
        <p class="find-num"><strong>4,200+</strong><span>Engineering teams</span></p>
        <div class="faces" aria-hidden="true">
          <span class="av" style="--h:262">AK</span>
          <span class="av" style="--h:200">RM</span>
          <span class="av" style="--h:24">JL</span>
        </div>
        <a class="ibtn" href="#reviews" aria-label="Read customer stories"><svg class="i"><use href="#i-ne"/></svg></a>
      </div>
    </aside>
    <div class="hero-feat">
      <article class="glass feat bite">
        <span class="glint" aria-hidden="true"></span>
        <div class="feat-top">
          <div>
            <h2 class="feat-name">checkout-api</h2>
            <p class="feat-addr"><svg class="i"><use href="#i-server"/></svg><span><span data-env>Production</span> · <span data-region>US West</span> · healthy</span></p>
          </div>
          <a class="ibtn ibtn-light" href="#features" aria-label="Open checkout-api"><svg class="i"><use href="#i-ne"/></svg></a>
        </div>
        <p class="feat-desc">p99 latency recovered four minutes after an automatic rollback. Mirador linked the spike to deploy #4182.</p>
        <svg class="spark" viewBox="0 0 300 64" preserveAspectRatio="none" aria-hidden="true">
          <defs><linearGradient id="spk" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#8f80ff" stop-opacity=".45"/><stop offset="1" stop-color="#8f80ff" stop-opacity="0"/></linearGradient></defs>
          <path class="spark-area" fill="url(#spk)" d="M0 40 L20 38 L40 42 L60 36 L80 39 L100 34 L120 37 L140 30 L160 33 L180 12 L200 8 L220 26 L240 36 L260 34 L280 38 L300 35 L300 64 L0 64Z"/>
          <path class="spark-line" fill="none" stroke="#a99dff" stroke-width="2" stroke-linejoin="round" d="M0 40 L20 38 L40 42 L60 36 L80 39 L100 34 L120 37 L140 30 L160 33 L180 12 L200 8 L220 26 L240 36 L260 34 L280 38 L300 35"/>
        </svg>
        <ul class="specs">
          <li><svg class="i"><use href="#i-bolt"/></svg><b data-k="p99">182 ms</b> p99</li>
          <li><svg class="i"><use href="#i-chart"/></svg><b data-k="err">0.02%</b> errors</li>
          <li><svg class="i"><use href="#i-layers"/></svg><b data-k="rpm">12.4k</b> rpm</li>
        </ul>
        <div class="feat-acts">
          <button class="act" type="button" aria-pressed="false" aria-label="Watch"><span class="ibtn"><svg class="i"><use href="#i-eye"/></svg></span>24</button>
          <button class="act" type="button" aria-pressed="false" aria-label="Pin"><span class="ibtn"><svg class="i"><use href="#i-save"/></svg></span>6</button>
          <button class="act" type="button" data-share aria-label="Share"><span class="ibtn"><svg class="i"><use href="#i-share"/></svg></span></button>
        </div>
      </article>
      <a class="disc hero-mark" href="#home" aria-label="Mirador, back to top"><svg viewBox="0 0 64 64"><use href="#i-mark"/></svg></a>
    </div>
  </section>

  <section id="intro" data-section="intro" data-kind="about" class="intro">
    <div class="wrap">
      <p class="statement" data-light>We built Mirador for the moment something breaks at 3 a.m. <span class="inl" style="--g:linear-gradient(120deg,#8f80ff,#3b30b8)"><svg viewBox="0 0 120 52" preserveAspectRatio="none" aria-hidden="true"><path d="M0 30h34l7-16 10 30 9-24 6 10h54" fill="none" stroke="#fff" stroke-width="3.5" stroke-linecap="round" stroke-linejoin="round"/></svg></span> One place to follow the request <span class="inl" style="--g:linear-gradient(120deg,#1a1735,#2b2560)"><svg viewBox="0 0 120 52" preserveAspectRatio="none" aria-hidden="true"><rect x="10" y="10" width="96" height="6" rx="3" fill="#8f80ff"/><rect x="22" y="20" width="40" height="6" rx="3" fill="#7cc4ff"/><rect x="48" y="30" width="50" height="6" rx="3" fill="#f5a54a"/><rect x="66" y="40" width="22" height="6" rx="3" fill="#4fe3b0"/></svg></span>, read the logs and find the change <span class="inl" style="--g:linear-gradient(120deg,#f5a54a,#ff6b8a)"><svg viewBox="0 0 120 52" preserveAspectRatio="none" aria-hidden="true"><path d="M8 26h104" stroke="#fff" stroke-opacity=".5" stroke-width="2.5"/><circle cx="24" cy="26" r="5" fill="#fff" fill-opacity=".7"/><circle cx="52" cy="26" r="5" fill="#fff" fill-opacity=".7"/><circle cx="82" cy="26" r="10" fill="#fff"/><circle cx="82" cy="26" r="4" fill="#ff6b8a"/></svg></span> that caused it, without opening <em>eleven</em> tabs.</p>
      <div class="intro-foot">
        <div class="intro-note" data-reveal>
          <p>Mirador is a team of forty engineers who spent a decade on pager rotations. We replaced six monitoring tools with one, then made it simple enough for every engineer to use.</p>
          <a class="btn" href="#team"><span>Meet the team</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
        </div>
        <dl class="stats">
          <div><dt>Platform uptime, last 12 months</dt><dd style="--len:6">99.99%</dd></div>
          <div><dt>Events ingested per day</dt><dd style="--len:4">2.1T</dd></div>
          <div><dt>Median time to detect</dt><dd style="--len:3">38s</dd></div>
        </dl>
      </div>
    </div>
  </section>

  <section id="features" data-section="features" data-kind="listings" class="homes">
    <div class="wrap sec-head">
      <h2 class="h2" data-split>One platform, <em>every</em> signal</h2>
      <div class="sec-aside" data-reveal>
        <p>Traces, metrics and logs share a single data model, so every chart links straight to the requests behind it.</p>
        <a class="btn" href="#pricing"><span>Start free trial</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </div>
    </div>
    <div class="stack">
      <article class="home">
        <div class="home-card">
          <div class="art aurora stars"></div>
          <span class="tag"><svg class="i"><use href="#i-nw"/></svg>Core</span>
          <div class="win" aria-hidden="true">
            <div class="win-bar"><i></i><i></i><i></i><span>trace 7f3a…e21 · POST /checkout · 486 ms</span><em>live</em></div>
            <div class="win-body">
              <div class="wf-axis"><span></span><div><span>0</span><span>120</span><span>240</span><span>360</span><span>480 ms</span></div></div>
              <div class="wf">
                <div class="wf-row"><span>gateway</span><div class="wf-track"><b style="--l:0%;--w:100%;--c:#8f80ff"></b></div></div>
                <div class="wf-row" style="--d:1"><span>auth-svc</span><div class="wf-track"><b style="--l:3%;--w:12%;--c:#7cc4ff"></b></div></div>
                <div class="wf-row" style="--d:1"><span>checkout-api</span><div class="wf-track"><b style="--l:16%;--w:78%;--c:#8f80ff"></b></div></div>
                <div class="wf-row" style="--d:2"><span>cart-db.query</span><div class="wf-track"><b style="--l:18%;--w:10%;--c:#f5a54a"></b></div></div>
                <div class="wf-row" style="--d:2"><span>pricing-svc</span><div class="wf-track"><b style="--l:30%;--w:18%;--c:#7cc4ff"></b></div></div>
                <div class="wf-row" style="--d:3"><span>inventory.get</span><div class="wf-track"><b style="--l:34%;--w:8%;--c:#4fe3b0"></b></div></div>
                <div class="wf-row" style="--d:2"><span>payments-api</span><div class="wf-track"><b style="--l:50%;--w:34%;--c:#ff6b8a"></b></div></div>
                <div class="wf-row" style="--d:3"><span>fraud-check</span><div class="wf-track"><b style="--l:53%;--w:24%;--c:#f5a54a"></b></div></div>
                <div class="wf-row" style="--d:2"><span>ledger.write</span><div class="wf-track"><b style="--l:85%;--w:6%;--c:#4fe3b0"></b></div></div>
                <div class="wf-row" style="--d:1"><span>queue.publish</span><div class="wf-track"><b style="--l:93%;--w:6%;--c:#7cc4ff"></b></div></div>
              </div>
            </div>
          </div>
          <ul class="glass home-specs">
            <li><svg class="i"><use href="#i-layers"/></svg><span><b>Every</b> request kept 72 h</span></li>
            <li><svg class="i"><use href="#i-code"/></svg><span><b>12</b> language SDKs</span></li>
            <li><svg class="i"><use href="#i-bolt"/></svg><span><b>1 click</b> from chart to span</span></li>
            <li><svg class="i"><use href="#i-check"/></svg><span><b>Zero</b> sampling guesswork</span></li>
          </ul>
          <div class="plate home-plate">
            <span class="fil fil-tl"></span><span class="fil fil-br"></span>
            <h3>Distributed tracing</h3>
            <p class="home-where"><svg class="i"><use href="#i-layers"/></svg>Follow one request across 200 services</p>
            <a class="ibtn" href="#contact" aria-label="See tracing in a demo"><svg class="i"><use href="#i-ne"/></svg></a>
            <p class="home-price">$0 <small>included in every plan</small></p>
          </div>
        </div>
      </article>
      <article class="home">
        <div class="home-card">
          <div class="art aurora cool stars"></div>
          <span class="tag"><svg class="i"><use href="#i-nw"/></svg>Core</span>
          <div class="win" aria-hidden="true">
            <div class="win-bar"><i></i><i></i><i></i><span>checkout-api · latency · last 6 h</span><em>live</em></div>
            <div class="win-body">
              <div class="mx">
                <div class="mx-legend"><span style="--c:#ff6b8a">p99</span><span style="--c:#8f80ff">p50</span><span style="--c:#f5a54a">SLO 300 ms</span></div>
                <div class="mx-chart">
                  <svg viewBox="0 0 600 260" preserveAspectRatio="none">
                    <defs><linearGradient id="mxa" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ff6b8a" stop-opacity=".35"/><stop offset="1" stop-color="#ff6b8a" stop-opacity="0"/></linearGradient></defs>
                    <g stroke="rgba(255,255,255,.07)" stroke-width="1"><line x1="0" y1="65" x2="600" y2="65"/><line x1="0" y1="130" x2="600" y2="130"/><line x1="0" y1="195" x2="600" y2="195"/></g>
                    <line x1="0" y1="96" x2="600" y2="96" stroke="#f5a54a" stroke-width="1.5" stroke-dasharray="6 6"/>
                    <line x1="340" y1="0" x2="340" y2="260" stroke="rgba(255,255,255,.35)" stroke-width="1" stroke-dasharray="3 5"/>
                    <path fill="url(#mxa)" d="M0 170 C40 160 70 150 100 158 S160 140 200 150 S260 120 300 135 S340 60 360 52 S400 140 440 150 S520 130 560 138 L600 132 L600 260 L0 260Z"/>
                    <path fill="none" stroke="#ff6b8a" stroke-width="2.5" d="M0 170 C40 160 70 150 100 158 S160 140 200 150 S260 120 300 135 S340 60 360 52 S400 140 440 150 S520 130 560 138 L600 132"/>
                    <path fill="none" stroke="#8f80ff" stroke-width="2.5" d="M0 215 C60 210 120 205 180 208 S300 200 360 190 S460 205 600 200"/>
                    <circle cx="360" cy="52" r="5" fill="#ff6b8a"/>
                  </svg>
                  <div class="mx-tip"><span class="dim">02:14 · deploy #4182</span><br>p99 <b>412 ms</b> · 3 regions</div>
                </div>
              </div>
            </div>
          </div>
          <ul class="glass home-specs">
            <li><svg class="i"><use href="#i-clock"/></svg><span><b>1 second</b> resolution</span></li>
            <li><svg class="i"><use href="#i-server"/></svg><span><b>13 months</b> retention</span></li>
            <li><svg class="i"><use href="#i-code"/></svg><span><b>PromQL</b> compatible</span></li>
            <li><svg class="i"><use href="#i-grid"/></svg><span><b>Unlimited</b> dashboards</span></li>
          </ul>
          <div class="plate home-plate">
            <span class="fil fil-tl"></span><span class="fil fil-br"></span>
            <h3>Metrics &amp; dashboards</h3>
            <p class="home-where"><svg class="i"><use href="#i-chart"/></svg>Every deploy annotated on every chart</p>
            <a class="ibtn" href="#contact" aria-label="See metrics in a demo"><svg class="i"><use href="#i-ne"/></svg></a>
            <p class="home-price">$0 <small>included in every plan</small></p>
          </div>
        </div>
      </article>
      <article class="home">
        <div class="home-card">
          <div class="art aurora alt stars"></div>
          <span class="tag"><svg class="i"><use href="#i-ne"/></svg>New</span>
          <div class="win" aria-hidden="true">
            <div class="win-bar"><i></i><i></i><i></i><span>incident #212 · checkout-api</span><em>resolved</em></div>
            <div class="win-body">
              <div class="tl-head"><span>Sev 2 · on-call: payments</span><b>resolved in 4m 33s</b></div>
              <ol class="tl">
                <li style="--c:#ff6b8a"><span class="dim">02:14:07</span><i></i><span>Alert fired: p99 &gt; 300 ms for 2 min</span></li>
                <li style="--c:#f5a54a"><span class="dim">02:14:09</span><i></i><span>Paged Priya C. via primary rotation</span></li>
                <li style="--c:#8f80ff"><span class="dim">02:14:31</span><i></i><span>Correlated with deploy #4182 (94% confidence)</span></li>
                <li style="--c:#7cc4ff"><span class="dim">02:15:02</span><i></i><span>Automatic rollback started</span></li>
                <li style="--c:#7cc4ff"><span class="dim">02:16:48</span><i></i><span>Runbook step 3 completed by Priya C.</span></li>
                <li style="--c:#4fe3b0"><span class="dim">02:18:40</span><i></i><span>Recovered: p99 182 ms, error rate 0.02%</span></li>
              </ol>
            </div>
          </div>
          <ul class="glass home-specs">
            <li><svg class="i"><use href="#i-check"/></svg><span><b>SLO</b>-based alerting</span></li>
            <li><svg class="i"><use href="#i-bolt"/></svg><span><b>Automatic</b> deploy correlation</span></li>
            <li><svg class="i"><use href="#i-users"/></svg><span><b>Rotations</b> and escalations</span></li>
            <li><svg class="i"><use href="#i-code"/></svg><span><b>Runbooks</b> attached to alerts</span></li>
          </ul>
          <div class="plate home-plate">
            <span class="fil fil-tl"></span><span class="fil fil-br"></span>
            <h3>Alerts &amp; on-call</h3>
            <p class="home-where"><svg class="i"><use href="#i-bell"/></svg>Page the right person, with the answer attached</p>
            <a class="ibtn" href="#contact" aria-label="See on-call in a demo"><svg class="i"><use href="#i-ne"/></svg></a>
            <p class="home-price">$29 <small>per seat / month, on Team</small></p>
          </div>
        </div>
      </article>
    </div>
  </section>

  <section id="integrations" data-section="integrations" data-kind="locations" class="regions">
    <div class="wrap sec-head">
      <h2 class="h2" data-split>Fits the stack you <em>already</em> run</h2>
      <div class="sec-aside" data-reveal>
        <p>More than 300 integrations, set up in minutes and versioned as code alongside the services they watch.</p>
      </div>
    </div>
    <ul class="region-list">
      <li>
        <a class="region-row" href="#contact">
          <span class="region-name">Infrastructure</span>
          <span class="region-meta"><b>124 integrations</b>Kubernetes, Terraform, containers</span>
          <span class="region-pic" style="--g:linear-gradient(110deg,#3b30b8,#8f80ff 60%,#7cc4ff)"><span class="glyphs" aria-hidden="true"><span>k8s</span><span>tf</span><span>vm</span><span>lb</span><span>dns</span></span><span class="ibtn"><svg class="i"><use href="#i-ne"/></svg></span></span>
        </a>
      </li>
      <li>
        <a class="region-row" href="#contact">
          <span class="region-name">Data stores</span>
          <span class="region-meta"><b>86 integrations</b>Postgres, Redis, Kafka</span>
          <span class="region-pic" style="--g:linear-gradient(110deg,#0f6b5a,#4fe3b0 60%,#7cc4ff)"><span class="glyphs" aria-hidden="true"><span>pg</span><span>rds</span><span>kfk</span><span>s3</span><span>es</span></span><span class="ibtn"><svg class="i"><use href="#i-ne"/></svg></span></span>
        </a>
      </li>
      <li>
        <a class="region-row" href="#contact">
          <span class="region-name">Languages</span>
          <span class="region-meta"><b>12 SDKs</b>Go, Python, TypeScript and more</span>
          <span class="region-pic" style="--g:linear-gradient(110deg,#a1461c,#f5a54a 60%,#ffd29a)"><span class="glyphs" aria-hidden="true"><span>go</span><span>py</span><span>ts</span><span>rb</span><span>rs</span></span><span class="ibtn"><svg class="i"><use href="#i-ne"/></svg></span></span>
        </a>
      </li>
      <li>
        <a class="region-row" href="#contact">
          <span class="region-name">Delivery</span>
          <span class="region-meta"><b>58 integrations</b>CI pipelines, chat, paging</span>
          <span class="region-pic" style="--g:linear-gradient(110deg,#7a1d3c,#ff6b8a 60%,#ffb3c1)"><span class="glyphs" aria-hidden="true"><span>ci</span><span>cd</span><span>#</span><span>sms</span><span>api</span></span><span class="ibtn"><svg class="i"><use href="#i-ne"/></svg></span></span>
        </a>
      </li>
    </ul>
  </section>

  <section id="gallery" data-section="gallery" data-kind="gallery" class="gallery">
    <div class="wrap sec-head">
      <h2 class="h2" data-split>A tour of the <em>product</em></h2>
      <div class="sec-aside" data-reveal>
        <p>Every view is live, linked to the others and shareable with a single URL, so the whole team looks at the same thing.</p>
      </div>
    </div>
    <div class="bento" data-fixed="5">
      <figure class="tile g1" data-drift="30">
        <svg class="map" viewBox="40 20 640 380" preserveAspectRatio="xMidYMid meet" aria-hidden="true">
          <defs><radialGradient id="mg" cx=".5" cy=".5" r=".6"><stop offset="0" stop-color="#3b30b8" stop-opacity=".55"/><stop offset="1" stop-color="#0d0b1c" stop-opacity="0"/></radialGradient></defs>
          <rect width="700" height="420" fill="url(#mg)"/>
          <g fill="none" stroke-width="2" stroke-linecap="round">
            <path d="M120 200 C200 200 210 100 290 100" stroke="#7cc4ff" stroke-opacity=".35"/><path class="flow" d="M120 200 C200 200 210 100 290 100" stroke="#7cc4ff"/>
            <path d="M120 200 L300 210" stroke="#8f80ff" stroke-opacity=".35"/><path class="flow" d="M120 200 L300 210" stroke="#8f80ff"/>
            <path d="M120 200 C200 200 210 320 290 320" stroke="#7cc4ff" stroke-opacity=".35"/><path class="flow" d="M120 200 C200 200 210 320 290 320" stroke="#7cc4ff" style="animation-duration:4s"/>
            <path d="M300 210 C380 210 400 150 480 150" stroke="#ff6b8a" stroke-opacity=".4"/><path class="flow" d="M300 210 C380 210 400 150 480 150" stroke="#ff6b8a" style="animation-duration:2s"/>
            <path d="M300 210 C380 210 400 270 480 270" stroke="#4fe3b0" stroke-opacity=".35"/><path class="flow" d="M300 210 C380 210 400 270 480 270" stroke="#4fe3b0"/>
            <path d="M480 150 C560 150 560 210 610 210" stroke="#f5a54a" stroke-opacity=".35"/><path class="flow" d="M480 150 C560 150 560 210 610 210" stroke="#f5a54a"/>
            <path d="M480 270 C560 270 560 210 610 210" stroke="#4fe3b0" stroke-opacity=".35"/>
          </g>
          <g>
            <circle cx="120" cy="200" r="18" fill="#1a1735" stroke="#8f80ff" stroke-width="2"/>
            <circle cx="290" cy="100" r="14" fill="#1a1735" stroke="#7cc4ff" stroke-width="2"/>
            <circle cx="300" cy="210" r="20" fill="#1a1735" stroke="#8f80ff" stroke-width="2"/>
            <circle cx="290" cy="320" r="14" fill="#1a1735" stroke="#7cc4ff" stroke-width="2"/>
            <circle class="halo" cx="480" cy="150" r="16" fill="none" stroke="#ff6b8a" stroke-width="2"/>
            <circle cx="480" cy="150" r="16" fill="#2a1424" stroke="#ff6b8a" stroke-width="2"/>
            <circle cx="480" cy="270" r="14" fill="#1a1735" stroke="#4fe3b0" stroke-width="2"/>
            <circle cx="610" cy="210" r="16" fill="#1a1735" stroke="#f5a54a" stroke-width="2"/>
          </g>
          <text x="92" y="242">gateway</text><text x="262" y="72">auth</text><text x="262" y="252">checkout</text><text x="262" y="356">search</text><text x="446" y="120">payments</text><text x="444" y="304">inventory</text><text x="588" y="250">ledger</text>
        </svg>
        <figcaption class="plate cap"><span class="fil fil-tl"></span><span class="fil fil-br"></span>Service map, built automatically</figcaption>
      </figure>
      <figure class="tile g2" data-drift="-40">
        <div class="tile-in log" aria-hidden="true">
          <div class="tile-h"><span>Live tail · payments-api</span><span>1,284 / s</span></div>
          <p><span class="dim">02:14:05</span> <span class="lv info">INFO</span> charge.created amount=4900</p>
          <p><span class="dim">02:14:06</span> <span class="lv warn">WARN</span> fraud-check slow: 812 ms</p>
          <p><span class="dim">02:14:07</span> <span class="lv err">ERROR</span> upstream timeout after 3 retries</p>
          <p><span class="dim">02:14:31</span> <span class="lv info">INFO</span> rollback to v2.41.3 requested</p>
          <p><span class="dim">02:18:40</span> <span class="lv ok">OK</span> health check passing <span class="cursor"></span></p>
        </div>
        <figcaption class="plate cap"><span class="fil fil-tl"></span><span class="fil fil-br"></span>Live tail, with trace links</figcaption>
      </figure>
      <figure class="tile g3" data-drift="-70">
        <div class="tile-in" aria-hidden="true">
          <div class="tile-h"><span>Error budget · 30 d</span></div>
          <ul class="slo">
            <li style="--c:#4fe3b0;--p:92%"><div><span>checkout</span><b>92%</b></div><span class="bar"></span></li>
            <li style="--c:#7cc4ff;--p:71%"><div><span>search</span><b>71%</b></div><span class="bar"></span></li>
            <li style="--c:#f5a54a;--p:38%"><div><span>payments</span><b>38%</b></div><span class="bar"></span></li>
            <li style="--c:#4fe3b0;--p:99%"><div><span>auth</span><b>99%</b></div><span class="bar"></span></li>
            <li style="--c:#ff6b8a;--p:14%"><div><span>exports</span><b>14%</b></div><span class="bar"></span></li>
          </ul>
        </div>
        <figcaption class="plate cap"><span class="fil fil-tl"></span><span class="fil fil-br"></span>SLO budgets</figcaption>
      </figure>
      <figure class="tile g4" data-drift="-20">
        <div class="tile-in" aria-hidden="true">
          <div class="tile-h"><span>Latency</span></div>
          <div class="heat" data-heat></div>
        </div>
        <figcaption class="plate cap"><span class="fil fil-tl"></span><span class="fil fil-br"></span>Heatmaps</figcaption>
      </figure>
      <figure class="tile g5" data-drift="50">
        <div class="tile-in code" aria-hidden="true">
          <p><span class="ln">1</span><span class="k">from</span> traces</p>
          <p><span class="ln">2</span>| <span class="k">where</span> service == <span class="s">"checkout-api"</span> <span class="k">and</span> duration &gt; <span class="n">300ms</span></p>
          <p><span class="ln">3</span>| <span class="k">summarize</span> <span class="f">p99</span>(duration) <span class="k">by</span> <span class="f">bin</span>(<span class="n">1m</span>), region</p>
          <span class="chip">Ran in 84 ms · 1.2 billion spans scanned</span>
        </div>
        <figcaption class="plate cap"><span class="fil fil-tl"></span><span class="fil fil-br"></span>One query language for every signal</figcaption>
      </figure>
    </div>
  </section>

  <section id="process" data-section="process" data-kind="steps" class="process">
    <div class="proc-stage">
      <div class="proc-shot">
        <div class="art aurora stars proc-art">
          <div class="radar" aria-hidden="true">
            <div class="sweep"></div>
            <svg viewBox="0 0 200 200">
              <g fill="none" stroke="rgba(255,255,255,.16)" stroke-width=".5"><circle cx="100" cy="100" r="96"/><circle cx="100" cy="100" r="72"/><circle cx="100" cy="100" r="48"/><circle cx="100" cy="100" r="24"/><path d="M100 4v192M4 100h192"/></g>
              <circle cx="132" cy="70" r="2.4" fill="#4fe3b0"/><circle cx="62" cy="128" r="2.4" fill="#7cc4ff"/><circle cx="150" cy="140" r="2.8" fill="#ff6b8a"/><circle cx="84" cy="52" r="2" fill="#f5a54a"/>
            </svg>
          </div>
        </div>
      </div>
      <h2 class="h2 proc-title">From install to first <em>insight</em> in one afternoon</h2>
      <div class="proc-lens">
        <div class="glass proc-card bite">
          <ol class="proc-steps">
            <li class="proc-step">
              <h3>Install one agent</h3>
              <p>A single command or Helm chart. The agent speaks OpenTelemetry, so nothing you add later is locked in.</p>
              <p class="proc-time"><svg class="i"><use href="#i-clock"/></svg>About 5 minutes</p>
            </li>
            <li class="proc-step">
              <h3>Everything is discovered</h3>
              <p>Services, dependencies and deploys appear on the map on their own, with sensible default dashboards for each.</p>
              <p class="proc-time"><svg class="i"><use href="#i-clock"/></svg>Within seconds</p>
            </li>
            <li class="proc-step">
              <h3>Set the goals that matter</h3>
              <p>Define service-level objectives in plain language. Mirador turns them into alerts that only fire when users feel it.</p>
              <p class="proc-time"><svg class="i"><use href="#i-clock"/></svg>One afternoon</p>
            </li>
            <li class="proc-step">
              <h3>Page the right person</h3>
              <p>Alerts arrive with the suspect deploy, the slow span and the runbook already attached. Most incidents end there.</p>
              <p class="proc-time"><svg class="i"><use href="#i-clock"/></svg>Every incident after</p>
            </li>
          </ol>
        </div>
        <div class="disc proc-disc" aria-hidden="true">
          <svg class="ring" viewBox="0 0 100 100"><circle class="ring-bg" cx="50" cy="50" r="46"/><circle class="ring-fg" cx="50" cy="50" r="46" pathLength="1"/></svg>
          <svg viewBox="0 0 64 64"><use href="#i-mark"/></svg>
        </div>
      </div>
    </div>
  </section>

  <section id="pricing" data-section="pricing" data-kind="pricing" class="pricing" data-modes>
    <div class="wrap sec-head">
      <h2 class="h2" data-split>Priced per seat, <em>never</em> per gigabyte</h2>
      <div class="sec-aside" data-reveal>
        <p>Unlimited hosts and data on every paid plan. Your bill stays the same when traffic spikes.</p>
        <div class="seg" role="group" aria-label="Billing period">
          <span class="seg-thumb" aria-hidden="true"></span>
          <button type="button" data-mode="monthly" aria-pressed="true">Monthly</button>
          <button type="button" data-mode="annual" aria-pressed="false">Annual<small>−17%</small></button>
        </div>
      </div>
    </div>
    <div class="plans">
      <article class="plan">
        <h3>Starter</h3>
        <p class="plan-for">For side projects and small teams</p>
        <p class="plan-fee"><span class="swap" data-monthly="$0" data-annual="$0">$0</span></p>
        <p class="plan-note"><span class="swap" data-monthly="free forever, up to 3 seats" data-annual="free forever, up to 3 seats">free forever, up to 3 seats</span></p>
        <ul class="plan-list">
          <li><svg class="i"><use href="#i-check"/></svg>Traces, metrics and logs</li>
          <li><svg class="i"><use href="#i-check"/></svg>7-day retention</li>
          <li><svg class="i"><use href="#i-check"/></svg>Community support</li>
        </ul>
        <a class="btn" href="#contact"><span>Start free</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </article>
      <article class="plan plan-hi">
        <h3>Team</h3>
        <p class="plan-for">Our most popular plan</p>
        <p class="plan-fee"><span class="swap" data-monthly="$29" data-annual="$24">$29</span></p>
        <p class="plan-note"><span class="swap" data-monthly="per seat / month, billed monthly" data-annual="per seat / month, billed yearly">per seat / month, billed monthly</span></p>
        <ul class="plan-list">
          <li><svg class="i"><use href="#i-check"/></svg>Everything in Starter</li>
          <li><svg class="i"><use href="#i-check"/></svg>30-day retention, unlimited hosts</li>
          <li><svg class="i"><use href="#i-check"/></svg>SLOs, alerts and on-call routing</li>
          <li><svg class="i"><use href="#i-check"/></svg>SAML single sign-on</li>
        </ul>
        <a class="btn" href="#contact"><span>Start 14-day trial</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </article>
      <article class="plan">
        <h3>Enterprise</h3>
        <p class="plan-for">For regulated and global teams</p>
        <p class="plan-fee"><span class="swap" data-monthly="Custom" data-annual="Custom">Custom</span></p>
        <p class="plan-note"><span class="swap" data-monthly="volume pricing, annual contract" data-annual="volume pricing, annual contract">volume pricing, annual contract</span></p>
        <ul class="plan-list">
          <li><svg class="i"><use href="#i-check"/></svg>Everything in Team</li>
          <li><svg class="i"><use href="#i-check"/></svg>Custom retention and data residency</li>
          <li><svg class="i"><use href="#i-check"/></svg>Dedicated support engineer</li>
        </ul>
        <a class="btn" href="#contact"><span>Talk to sales</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </article>
    </div>
  </section>

  <section id="team" data-section="team" data-kind="team" class="team">
    <div class="wrap sec-head">
      <h2 class="h2" data-split>The people behind the <em>pager</em></h2>
      <div class="sec-aside" data-reveal>
        <p>Forty engineers across four time zones. Every one of us takes a turn on call for Mirador itself.</p>
      </div>
    </div>
    <div class="crew">
      <article class="mate">
        <div class="mate-pic"><div class="portrait" style="--h:262" aria-hidden="true">EM</div></div>
        <div class="mate-row"><div><h3>Elena Marsh</h3><p>Co-founder &amp; CEO, former SRE lead</p></div><a class="ibtn" href="mailto:elena@mirador.example" aria-label="Write to Elena Marsh"><svg class="i"><use href="#i-mail"/></svg></a></div>
      </article>
      <article class="mate">
        <div class="mate-pic"><div class="portrait" style="--h:200" aria-hidden="true">TL</div></div>
        <div class="mate-row"><div><h3>Theo Lindqvist</h3><p>Co-founder &amp; CTO</p></div><a class="ibtn" href="mailto:theo@mirador.example" aria-label="Write to Theo Lindqvist"><svg class="i"><use href="#i-mail"/></svg></a></div>
      </article>
      <article class="mate">
        <div class="mate-pic"><div class="portrait" style="--h:24" aria-hidden="true">PC</div></div>
        <div class="mate-row"><div><h3>Priya Castell</h3><p>Head of Solutions Engineering</p></div><a class="ibtn" href="mailto:priya@mirador.example" aria-label="Write to Priya Castell"><svg class="i"><use href="#i-mail"/></svg></a></div>
      </article>
      <article class="mate">
        <div class="mate-pic"><div class="portrait" style="--h:150" aria-hidden="true">JR</div></div>
        <div class="mate-row"><div><h3>Jonah Reyes</h3><p>Head of Security</p></div><a class="ibtn" href="mailto:jonah@mirador.example" aria-label="Write to Jonah Reyes"><svg class="i"><use href="#i-mail"/></svg></a></div>
      </article>
    </div>
  </section>

  <section id="reviews" data-section="reviews" data-kind="reviews" class="reviews">
    <div class="rev-stage">
      <div class="rev-shot"><div class="art aurora alt stars" data-parallax="5"></div></div>
      <div class="rev-head">
        <h2 class="h2" data-split>What teams say after the <em>first</em> incident</h2>
        <p class="rev-score" data-reveal><strong>4.9</strong><span>average rating from 1,300 engineering teams</span></p>
      </div>
      <div class="rev-row">
        <div class="rev-track">
          <figure class="glass rev">
            <blockquote>The alert arrived with the bad deploy already named. We rolled back before anyone had finished reading the page.</blockquote>
            <figcaption><span class="av" style="--h:262">HB</span><span><b>Hana Brandt</b>Staff SRE, Halcyon Pay</span></figcaption>
          </figure>
          <figure class="glass rev">
            <blockquote>We retired four tools and one very large invoice. Seat pricing means nobody argues about adding more logs.</blockquote>
            <figcaption><span class="av" style="--h:200">MO</span><span><b>Marcus Ode</b>VP Engineering, Fernway</span></figcaption>
          </figure>
          <figure class="glass rev">
            <blockquote>New engineers can follow a request through forty services on their first day. That used to take a month of tribal knowledge.</blockquote>
            <figcaption><span class="av" style="--h:24">CN</span><span><b>Clara Nguyen</b>Platform lead, Quillstack</span></figcaption>
          </figure>
          <figure class="glass rev">
            <blockquote>Mean time to resolve dropped from 52 minutes to 9 in our first quarter. The service map alone paid for it.</blockquote>
            <figcaption><span class="av" style="--h:150">DF</span><span><b>Daniel Fisk</b>Head of Infrastructure, Brightloom</span></figcaption>
          </figure>
          <figure class="glass rev">
            <blockquote>Our auditors asked for the data residency report and we sent it the same afternoon. That has never happened before.</blockquote>
            <figcaption><span class="av" style="--h:320">AS</span><span><b>Ana Soler</b>CISO, Orbit Health</span></figcaption>
          </figure>
        </div>
      </div>
    </div>
  </section>

  <section id="faq" data-section="faq" data-kind="faq" class="faq">
    <div class="wrap faq-grid">
      <div class="faq-side">
        <h2 class="h2" data-split>Questions engineers <em>ask</em> us</h2>
        <p class="lede">If yours is not here, ask it. A solutions engineer replies, usually within two hours.</p>
        <a class="btn" href="#contact"><span>Ask your own</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </div>
      <div class="faq-list">
        <details class="qa" name="faq" open>
          <summary><span>How long does setup take?</span><i class="ibtn"><svg class="i"><use href="#i-plus"/></svg></i></summary>
          <div class="qa-body"><p>Most teams see their first traces within five minutes of running <code>mirador agent install</code>. Dashboards and the service map build themselves as traffic flows.</p></div>
        </details>
        <details class="qa" name="faq">
          <summary><span>Do you charge for data volume?</span><i class="ibtn"><svg class="i"><use href="#i-plus"/></svg></i></summary>
          <div class="qa-body"><p>No. Paid plans are priced per seat, with unlimited hosts and ingest. Fair-use limits exist, and we contact you long before they matter.</p></div>
        </details>
        <details class="qa" name="faq">
          <summary><span>Can we keep using OpenTelemetry?</span><i class="ibtn"><svg class="i"><use href="#i-plus"/></svg></i></summary>
          <div class="qa-body"><p>Yes. Mirador accepts OpenTelemetry natively. Point your existing collectors at us and nothing in your code has to change.</p></div>
        </details>
        <details class="qa" name="faq">
          <summary><span>Where is our data stored?</span><i class="ibtn"><svg class="i"><use href="#i-plus"/></svg></i></summary>
          <div class="qa-body"><p>In the region you choose: US or EU on every plan, with more regions and single-tenant deployments available on Enterprise.</p></div>
        </details>
        <details class="qa" name="faq">
          <summary><span>What happens when the trial ends?</span><i class="ibtn"><svg class="i"><use href="#i-plus"/></svg></i></summary>
          <div class="qa-body"><p>Your workspace moves to Starter automatically. Nothing is deleted, and you can upgrade again at any time with one click.</p></div>
        </details>
      </div>
    </div>
  </section>

  <section id="security" data-section="security" data-kind="valuation" class="sell">
    <div class="sell-stage">
      <div class="sell-shot">
        <div class="art aurora cool">
          <div class="dots"></div>
          <svg class="shield" viewBox="0 0 200 230" aria-hidden="true">
            <defs><linearGradient id="shg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#b9b0ff"/><stop offset="1" stop-color="#7cc4ff"/></linearGradient></defs>
            <path d="M100 8 186 40v62c0 56-36 100-86 120C50 202 14 158 14 102V40z" fill="rgba(143,128,255,.08)" stroke="url(#shg)" stroke-width="2.5"/>
            <path d="M100 34 164 58v46c0 42-26 76-64 92-38-16-64-50-64-92V58z" fill="none" stroke="rgba(255,255,255,.18)" stroke-dasharray="4 6"/>
            <path d="m70 116 22 22 40-46" fill="none" stroke="#4fe3b0" stroke-width="6" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
      </div>
      <div class="plate sell-plate">
        <span class="fil fil-tr"></span><span class="fil fil-bl"></span>
        <span class="eyebrow">Security</span>
        <h2 class="h2">Built for teams with <em>auditors</em></h2>
        <p>SOC 2 Type II audited, encrypted in transit and at rest, with role-based access, audit logs and data residency in the US or EU.</p>
        <a class="btn btn-solid" href="#contact"><span>Request the security pack</span><i class="btn-dot"><svg class="i"><use href="#i-ne"/></svg></i></a>
      </div>
      <ul class="sell-facts">
        <li class="glass"><strong>99.99%</strong><span>uptime SLA on Enterprise</span></li>
        <li class="glass"><strong>Zero</strong><span>third parties with access to your data</span></li>
      </ul>
    </div>
  </section>

  <section id="contact" data-section="contact" data-kind="contact" class="contact">
    <div class="wrap contact-grid">
      <div class="contact-main">
        <h2 class="h2" data-split>See your own system in <em>Mirador</em></h2>
        <form class="cform" data-sent="Thank you. A solutions engineer will reply within one working day." novalidate>
          <div class="field"><label for="c-name">Your name</label><input id="c-name" name="name" autocomplete="name" required></div>
          <div class="field"><label for="c-mail">Work email</label><input id="c-mail" name="email" type="email" autocomplete="email" required></div>
          <div class="field field-wide"><label for="c-co">Company <span>(optional)</span></label><input id="c-co" name="company" autocomplete="organization"></div>
          <fieldset class="chips">
            <legend>Engineering team size</legend>
            <label><input type="radio" name="size" value="1-20" checked><span>1–20</span></label>
            <label><input type="radio" name="size" value="21-200"><span>21–200</span></label>
            <label><input type="radio" name="size" value="201-1000"><span>201–1,000</span></label>
            <label><input type="radio" name="size" value="1000+"><span>1,000+</span></label>
          </fieldset>
          <div class="field field-wide"><label for="c-msg">What are you monitoring today?</label><textarea id="c-msg" name="message" rows="4"></textarea></div>
          <div class="cform-end">
            <button class="btn btn-solid" type="submit"><span>Book a demo</span><i class="btn-dot"><svg class="i"><use href="#i-right"/></svg></i></button>
            <p class="cform-done" aria-live="polite"></p>
          </div>
        </form>
      </div>
      <aside class="contact-side">
        <div class="contact-shot">
          <div class="art aurora stars">
            <div class="win" aria-hidden="true">
              <div class="win-bar"><i></i><i></i><i></i><span>terminal</span></div>
              <div class="win-body term">
                <p><span class="p">$</span> mirador agent install --env production</p>
                <p><span class="ok">✓</span> Kubernetes cluster detected, 14 nodes</p>
                <p><span class="ok">✓</span> 63 services discovered</p>
                <p><span class="ok">✓</span> Streaming traces, metrics and logs</p>
                <p><span class="p">→</span> Your first dashboard is ready <span class="cursor"></span></p>
              </div>
            </div>
          </div>
        </div>
        <div class="contact-wrap">
          <div class="glass contact-card bite">
            <h3>Talk to an engineer</h3>
            <address>Not a salesperson. Average reply under two hours.</address>
            <ul class="contact-list">
              <li><svg class="i"><use href="#i-phone"/></svg><a class="lnk" href="tel:+14155550142">+1 415 555 0142</a></li>
              <li><svg class="i"><use href="#i-mail"/></svg><a class="lnk" href="mailto:sales@mirador.example">sales@mirador.example</a></li>
              <li><svg class="i"><use href="#i-clock"/></svg>Monday to Friday, 7 to 7 PT</li>
            </ul>
          </div>
          <a class="disc" href="#home" aria-label="Mirador, back to top"><svg viewBox="0 0 64 64"><use href="#i-mark"/></svg></a>
        </div>
      </aside>
    </div>
  </section>
</main>

<footer class="foot" id="alerts" data-section="footer">
  <div class="foot-panel">
    <div class="foot-top">
      <div class="foot-news">
        <h2>The changelog, <em>every other</em> Thursday</h2>
        <form class="news" data-done="Subscribed. The next release notes will reach you first." novalidate>
          <label class="sr" for="news-mail">Email</label>
          <input id="news-mail" type="email" placeholder="Your work email" autocomplete="email" required>
          <button class="ibtn" type="submit" aria-label="Subscribe"><svg class="i"><use href="#i-right"/></svg></button>
        </form>
        <p class="news-done" aria-live="polite"></p>
      </div>
      <nav class="foot-links" aria-label="Footer">
        <div><h3>Product</h3><ul><li><a class="lnk" href="#features">Features</a></li><li><a class="lnk" href="#integrations">Integrations</a></li><li><a class="lnk" href="#pricing">Pricing</a></li><li><a class="lnk" href="#security">Security</a></li></ul></div>
        <div><h3>Company</h3><ul><li><a class="lnk" href="#intro">About</a></li><li><a class="lnk" href="#team">Team</a></li><li><a class="lnk" href="#faq">Questions</a></li></ul></div>
        <div><h3>Contact</h3><ul><li><a class="lnk" href="tel:+14155550142">+1 415 555 0142</a></li><li><a class="lnk" href="mailto:sales@mirador.example">sales@mirador.example</a></li><li><a class="lnk" href="#contact">Book a demo</a></li></ul></div>
      </nav>
    </div>
    <p class="wordmark" style="--len:7">Mirador</p>
    <div class="foot-base">
      <span>© 2026 Mirador Labs</span>
      <span class="status">All systems operational</span>
      <a class="lnk" href="#home">Back to top</a>
    </div>
  </div>
</footer>

<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js"></script>
<script>
/* GhostFibers — WebGL2 ribbon field, ported from the React component to plain JS */
(function(){
const MAX_RENDER_DIM = 2400;
const BLOOM_LEVELS = 5;
const INTRO_SECONDS = 2.6;
const CAMERA = 7.5;
const FOV = 0.56;
const RIBBON_LENGTH = 24;
const HOVER_EFFECTS = { focus: 0, part: 1, none: 2 };
const FIBER_STYLES = { dots: 0, dashes: 0.45, lines: 1 };
const GRADIENTS = { depth: 0, along: 1, across: 2 };
const RIBBON_TINT = [0, 0.75, 0.35];
const PLACEMENTS = [
  [0, 0, 0, 0],
  [1.9, -4.6, -0.08, 2.4],
  [-1.05, 2.0, 0.12, 4.1]
];
const RIBBON_GAIN = [1, 0.5, 0.55];
const DEG = Math.PI / 180;
const FOCAL = 1 / (2 * Math.tan(FOV / 2));

const HEADER = `#version 300 es
precision highp float;
`;

const SHAPE = `
uniform float uTime;
uniform float uTwist;
uniform float uRoll;
uniform float uWaves;
uniform float uWidth;
uniform float uRibbon;
uniform mat3 uOrient;
uniform float uScale;
uniform vec4 uPlace;
uniform float uVolume;

float hash11(float n) {
  return fract(sin(n * 91.3458) * 47453.5453);
}

vec3 centerLocal(float s) {
  float t = uTime;
  float ph = uPlace.w;
  float x = s * ${RIBBON_LENGTH.toFixed(1)};
  float y = uWaves * (0.52 * sin(x * 0.43 + t * 0.31 + ph) + 0.26 * sin(x * 0.79 - t * 0.23 + 1.3 + ph * 0.7)) + uPlace.x + x * uPlace.z;
  float z = uWaves * 0.65 * sin(x * 0.33 + t * 0.19 + 0.7 + ph * 1.3) + uPlace.y;
  return vec3(x, y, z);
}

float twistAt(float s, float layer) {
  float x = s * ${RIBBON_LENGTH.toFixed(1)};
  return uTwist * 0.483 * x + uRoll + uPlace.w * 0.6 + layer * uVolume * 0.42 + 0.5 * sin(x * 0.26 + uTime * 0.27 + uPlace.w);
}

vec3 ribbonPoint(float s, float v, float n, float layer, out vec3 normal) {
  vec3 c0 = centerLocal(s);
  vec3 c1 = centerLocal(s + 0.004);
  vec3 tangent = normalize(c1 - c0);
  vec3 up = vec3(0.0, 1.0, 0.0);
  vec3 n0 = normalize(up - tangent * dot(up, tangent));
  vec3 b0 = cross(tangent, n0);
  float th = twistAt(s, layer);
  vec3 across = cos(th) * n0 + sin(th) * b0;
  vec3 sheet = -sin(th) * n0 + cos(th) * b0;
  float halfWidth = uWidth * (0.78 + 0.22 * cos(s * 3.14159));
  vec3 local = c0 + across * v * halfWidth + sheet * (n + layer * uVolume * 0.16) * halfWidth;
  normal = uOrient * sheet;
  return uOrient * (local * uScale);
}
`;

const DOT_VERTEX = `${HEADER}
${SHAPE}
uniform mat4 uViewProj;
uniform vec3 uEye;
uniform vec2 uViewport;
uniform float uDpr;
uniform float uFibers;
uniform float uDots;
uniform float uFlow;
uniform float uSize;
uniform float uFocus;
uniform float uDof;
uniform float uMaxCoc;
uniform float uFocal;
uniform float uIntro;
uniform vec4 uPulse;
uniform vec4 uHover;
uniform float uPart;
uniform float uDotLength;
uniform float uSparkle;
uniform float uDepthSpread;
uniform float uGain;
uniform float uTips;
uniform float uTint;
uniform float uGradient;
uniform float uFold;

out vec2 vLocal;
out float vRadius;
out float vSegment;
out vec3 vLight;
out float vTint;

vec3 project(vec3 world, out float depth) {
  vec4 clip = uViewProj * vec4(world, 1.0);
  depth = clip.w;
  vec2 ndc = clip.xy / clip.w;
  return vec3((ndc * 0.5 + 0.5) * uViewport, clip.w);
}

vec2 part(vec2 px) {
  if (uPart <= 0.0 || uHover.w <= 0.0) return px;
  vec2 away = px - uHover.xy;
  float dist = length(away);
  float radius = uHover.z;
  float push = uPart * uHover.w * radius * 0.55 * exp(-dist * dist / (radius * radius));
  return px + away / max(dist, 1e-3) * push * smoothstep(0.0, radius * 0.25, dist);
}

void main() {
  int perFiber = int(uDots);
  int fiber = gl_InstanceID / perFiber;
  int bead = gl_InstanceID - fiber * perFiber;
  float fi = float(fiber);
  float fk = float(bead);

  float seed = hash11(fi * 1.731 + uRibbon * 17.0);
  float s = fract((fk + uFlow + seed * uDots) / uDots) - 0.5;
  float sNext = s + 1.0 / uDots;
  float layer = mod(fi, 3.0) - 1.0;
  float slot = floor(fi / 3.0);
  float perLayer = max(floor(uFibers / 3.0), 1.0);
  float v = ((slot + 0.5) / perLayer) * 2.0 - 1.0 + (hash11(fi * 3.113 + 4.0) - 0.5) * (1.6 / perLayer) + layer * 0.12 / perLayer;
  float depthOffset = (hash11(fi * 7.919 + 2.0) - 0.5) * uDepthSpread * (0.35 + 6.0 * s * s);

  vec3 normal;
  vec3 world = ribbonPoint(s, v, depthOffset, layer, normal);
  vec3 nextNormal;
  vec3 nextWorld = ribbonPoint(sNext, v, depthOffset, layer, nextNormal);

  float depth;
  vec3 p0 = project(world, depth);
  float nextDepth;
  vec3 p1 = project(nextWorld, nextDepth);
  vec2 px = part(p0.xy);
  vec2 pxNext = part(p1.xy);

  float baseRadius = max(0.5 * uSize * uDpr * uFocal / max(depth, 0.1), 0.45);
  float coc = min(uDof * abs(1.0 - uFocus / max(depth, 0.1)) * uViewport.y * 0.035, uMaxCoc * uDpr);
  float radius = baseRadius + coc;
  float spill = max(10.0 * uDpr, baseRadius);
  float energy = pow(baseRadius / min(radius, spill), 1.25) * pow(min(1.0, spill / radius), 2.0);

  vec3 toEye = normalize(uEye - world);
  float facing = abs(dot(normalize(normal), toEye));
  float focalPx = uViewport.y * ${FOCAL.toFixed(5)} / max(depth, 0.1);
  float widthPx = 2.0 * uWidth * uScale * focalPx;
  float stack = (widthPx * facing + 2.0 * baseRadius) / (widthPx + 2.0 * baseRadius);
  float spacingFace = length(nextWorld - world) * focalPx;
  float trail = (length(p1.xy - p0.xy) + 2.0 * baseRadius) / (spacingFace + 2.0 * baseRadius);
  float crowd = sqrt(clamp(stack * trail, 0.002, 1.0));
  float fold = pow(1.0 - facing, 6.0) * uFold;
  float endFade = smoothstep(0.5, 0.4, abs(s)) * smoothstep(1.6, 4.2, depth);
  float tipEnd = mix(0.6, 0.06 + 0.26 * hash11(fi * 9.137 + uPlace.w * 3.0), uTips);
  float tip = exp(-pow((s - tipEnd) / 0.0065, 2.0)) * uTips;
  endFade *= smoothstep(tipEnd + 0.003, tipEnd - 0.001, s);
  float appear = smoothstep(0.0, 0.12, uIntro * 1.3 - (s + 0.5) - seed * 0.12);
  float twinklePhase = hash11(fi * 13.7 + fk * 0.917 + uRibbon * 3.0);
  float twinkle = pow(max(sin(uTime * (1.2 + 2.6 * twinklePhase) * 3.0 + twinklePhase * 61.0), 0.0), 36.0) * uSparkle * (1.0 - 0.85 * uDotLength);
  float pulseGap = abs(s - uPulse.x) - uPulse.y * 0.42;
  float pulse = uPulse.z * exp(-pulseGap * pulseGap / 0.0018) * (abs(uPulse.w - uRibbon) < 0.5 ? 1.0 : 0.35);
  float strength = mix(0.45, 1.0, hash11(fi * 5.37 + 1.0)) * mix(1.0, 0.72, abs(layer) * uVolume);
  float intensity = energy * crowd * strength * endFade * appear * 0.8 * uGain * (1.0 + fold * 7.0 + twinkle * 5.0 + pulse * 4.0 + tip * 7.0);
  float highlight = clamp(fold * 0.55 + twinkle + pulse + tip, 0.0, 1.0);

  vec2 segment = (pxNext - px) * uDotLength;
  float segmentLength = length(segment);
  intensity *= mix(1.0, (2.0 * radius) / (segmentLength + 2.0 * radius) * 1.6, uDotLength);
  vec2 axis = segmentLength > 1e-3 ? segment / segmentLength : vec2(1.0, 0.0);
  vec2 perp = vec2(-axis.y, axis.x);
  vec2 corner = vec2(gl_VertexID == 1 || gl_VertexID == 3 ? 1.0 : 0.0, gl_VertexID >= 2 ? 1.0 : 0.0);
  float along = mix(-radius, segmentLength + radius, corner.x);
  float across = mix(-radius, radius, corner.y);
  vec2 position = px + axis * along + perp * across;

  vLocal = vec2(along, across);
  vRadius = radius;
  vSegment = segmentLength;
  vLight = vec3(intensity, highlight, coc / max(radius, 1e-3));
  float depthTint = clamp(uTint + smoothstep(uFocus, uFocus + 5.0, depth) * 0.5, 0.0, 1.0);
  vTint = uGradient < 0.5 ? depthTint : uGradient < 1.5 ? smoothstep(-0.42, 0.42, s) : clamp(v * 0.5 + 0.5, 0.0, 1.0);
  if (intensity < 0.0005) position = vec2(-1e4);
  gl_Position = vec4(position / uViewport * 2.0 - 1.0, 0.0, 1.0);
}`;

const DUST_VERTEX = `${HEADER}
uniform mat4 uViewProj;
uniform vec2 uViewport;
uniform float uDpr;
uniform float uTime;
uniform float uSize;
uniform float uFocus;
uniform float uDof;
uniform float uMaxCoc;
uniform float uFocal;
uniform float uIntro;
uniform float uSparkle;
uniform float uScale;
uniform float uGradient;
uniform float uGain;

out vec2 vLocal;
out float vRadius;
out float vSegment;
out vec3 vLight;
out float vTint;

float hash11(float n) {
  return fract(sin(n * 91.3458) * 47453.5453);
}

void main() {
  float id = float(gl_InstanceID);
  vec3 seed = vec3(hash11(id * 1.37 + 0.3), hash11(id * 2.91 + 1.7), hash11(id * 4.17 + 2.9));
  vec3 box = vec3(9.0, 5.4, 6.0);
  vec3 p = (seed - 0.5) * box;
  p.z -= 0.6;
  p += 0.18 * vec3(sin(uTime * 0.21 + seed.x * 40.0), sin(uTime * 0.17 + seed.y * 40.0), sin(uTime * 0.13 + seed.z * 40.0));
  p *= mix(1.0, uScale, 0.5);
  vec4 clip = uViewProj * vec4(p, 1.0);
  float depth = clip.w;
  vec2 px = (clip.xy / clip.w * 0.5 + 0.5) * uViewport;
  float size = uSize * mix(0.5, 1.4, hash11(id * 7.7));
  float baseRadius = max(0.5 * size * uDpr * uFocal / max(depth, 0.1), 0.45);
  float coc = min(uDof * abs(1.0 - uFocus / max(depth, 0.1)) * uViewport.y * 0.035, uMaxCoc * uDpr * 1.6);
  float radius = baseRadius + coc;
  float spill = max(10.0 * uDpr, baseRadius);
  float energy = pow(baseRadius / min(radius, spill), 0.9) * pow(min(1.0, spill / radius), 2.0);
  float twinkle = pow(max(sin(uTime * (0.8 + 1.6 * seed.y) * 2.0 + seed.z * 50.0), 0.0), 8.0);
  float intensity = energy * (0.35 + 0.65 * twinkle) * mix(0.4, 1.0, seed.x) * smoothstep(0.3, 1.0, uIntro) * (depth > 0.2 ? 1.0 : 0.0);
  vec2 corner = vec2(gl_VertexID == 1 || gl_VertexID == 3 ? 1.0 : 0.0, gl_VertexID >= 2 ? 1.0 : 0.0) * 2.0 - 1.0;
  vec2 position = px + corner * radius;
  vLocal = corner * radius;
  vRadius = radius;
  vSegment = 0.0;
  vLight = vec3(intensity * 0.8 * uGain, 0.3 + 0.6 * twinkle * uSparkle, coc / max(radius, 1e-3));
  vTint = uGradient < 0.5 ? 0.45 + 0.55 * seed.y : seed.y;
  gl_Position = vec4(position / uViewport * 2.0 - 1.0, 0.0, 1.0);
}`;

const DOT_FRAGMENT = `${HEADER}
uniform vec3 uGlowColor;
uniform vec3 uLineColor;
uniform vec3 uSecondaryColor;
in vec2 vLocal;
in float vRadius;
in float vSegment;
in vec3 vLight;
in float vTint;
out vec4 outColor;
void main() {
  float along = clamp(vLocal.x, 0.0, vSegment);
  float d = length(vec2(vLocal.x - along, vLocal.y));
  float rho = d / max(vRadius, 1e-3);
  if (rho > 1.0) discard;
  float soft = clamp(2.6 / max(vRadius, 1e-3), 0.14, 1.0);
  float disk = 1.0 - smoothstep(1.0 - soft, 1.0, rho);
  float bokeh = disk * (0.94 + 0.08 * smoothstep(0.55, 0.95, rho));
  float core = exp(-rho * rho * 3.2);
  float shape = mix(core, bokeh, smoothstep(0.25, 0.7, vLight.z));
  vec3 color = mix(mix(uGlowColor, uSecondaryColor, vTint), uLineColor, vLight.y);
  outColor = vec4(color * shape * vLight.x, shape * vLight.x);
}`;

const FULLSCREEN = `${HEADER}
out vec2 vUv;
void main() {
  vec2 p = vec2(gl_VertexID == 1 ? 3.0 : -1.0, gl_VertexID == 2 ? 3.0 : -1.0);
  vUv = p * 0.5 + 0.5;
  gl_Position = vec4(p, 0.0, 1.0);
}`;

const BRIGHT_FRAGMENT = `${HEADER}
uniform sampler2D uSource;
uniform vec2 uTexel;
in vec2 vUv;
out vec4 outColor;
vec3 pick(vec2 uv) {
  vec3 c = texture(uSource, uv).rgb;
  float peak = max(max(c.r, c.g), c.b);
  return c * smoothstep(0.35, 1.2, peak);
}
void main() {
  vec2 o = uTexel;
  vec3 c = pick(vUv + vec2(-o.x, -o.y)) + pick(vUv + vec2(o.x, -o.y)) + pick(vUv + vec2(-o.x, o.y)) + pick(vUv + vec2(o.x, o.y));
  outColor = vec4(c * 0.25, 1.0);
}`;

const DOWN_FRAGMENT = `${HEADER}
uniform sampler2D uSource;
uniform vec2 uTexel;
in vec2 vUv;
out vec4 outColor;
void main() {
  vec2 o = uTexel;
  vec3 c = texture(uSource, vUv).rgb * 4.0;
  c += texture(uSource, vUv + vec2(-o.x, -o.y)).rgb;
  c += texture(uSource, vUv + vec2(o.x, -o.y)).rgb;
  c += texture(uSource, vUv + vec2(-o.x, o.y)).rgb;
  c += texture(uSource, vUv + vec2(o.x, o.y)).rgb;
  outColor = vec4(c / 8.0, 1.0);
}`;

const UP_FRAGMENT = `${HEADER}
uniform sampler2D uSource;
uniform vec2 uTexel;
in vec2 vUv;
out vec4 outColor;
void main() {
  vec2 o = uTexel;
  vec3 c = texture(uSource, vUv + vec2(-o.x * 2.0, 0.0)).rgb;
  c += texture(uSource, vUv + vec2(-o.x, o.y)).rgb * 2.0;
  c += texture(uSource, vUv + vec2(0.0, o.y * 2.0)).rgb;
  c += texture(uSource, vUv + vec2(o.x, o.y)).rgb * 2.0;
  c += texture(uSource, vUv + vec2(o.x * 2.0, 0.0)).rgb;
  c += texture(uSource, vUv + vec2(o.x, -o.y)).rgb * 2.0;
  c += texture(uSource, vUv + vec2(0.0, -o.y * 2.0)).rgb;
  c += texture(uSource, vUv + vec2(-o.x, -o.y)).rgb * 2.0;
  outColor = vec4(c / 12.0, 1.0);
}`;

const COMPOSITE_FRAGMENT = `${HEADER}
uniform sampler2D uScene;
uniform sampler2D uBloom;
uniform float uGlow;
uniform float uBrightness;
uniform float uLightMode;
uniform float uGrain;
uniform float uVignette;
uniform float uFrame;
uniform vec2 uView;
uniform float uDpr;
in vec2 vUv;
out vec4 outColor;

float hash(vec2 p) {
  vec3 q = fract(vec3(p.xyx) * 0.1031);
  q += dot(q, q.yzx + 33.33);
  return fract((q.x + q.y) * q.z);
}

float smoother(float x) {
  x = clamp(x, 0.0, 1.0);
  return x * x * x * (x * (x * 6.0 - 15.0) + 10.0);
}

void main() {
  vec4 scene = texture(uScene, vUv);
  vec3 bloom = texture(uBloom, vUv).rgb;
  vec3 light = (scene.rgb + bloom * uGlow) * uBrightness;
  float reach = max(uVignette * 0.3, 1e-4);
  float mask = uVignette > 0.0 ? smoother(vUv.x / reach) * smoother((1.0 - vUv.x) / reach) * smoother(vUv.y / reach) * smoother((1.0 - vUv.y) / reach) : 1.0;
  vec2 cell = floor(vUv * uView / max(uDpr, 1.0));
  float grain = hash(cell + uFrame * 17.31) + hash(cell * 1.31 + uFrame * 3.7 + 9.1) - 1.0;
  if (uLightMode > 0.5) {
    float amount = scene.a * uBrightness;
    float ink = (1.0 - exp(-amount * 1.5)) * mask;
    ink = clamp(ink * (1.0 + grain * uGrain * 2.0), 0.0, 1.0);
    vec3 hue = clamp(scene.rgb / max(scene.a, 1e-4), 0.0, 1.0);
    vec3 tone = hue * mix(1.0, 0.72, clamp(amount * 0.35, 0.0, 1.0));
    outColor = vec4(tone * ink, ink);
    return;
  }
  vec3 color = (1.0 - exp(-light * 1.25)) * mask;
  float peak = max(color.r, max(color.g, color.b));
  color = max(color + grain * uGrain * (0.25 + 0.75 * sqrt(peak)), 0.0);
  outColor = vec4(color, max(color.r, max(color.g, color.b)));
}`;

const SHAPE_UNIFORMS = [
  'uTime',
  'uTwist',
  'uRoll',
  'uWaves',
  'uWidth',
  'uRibbon',
  'uOrient',
  'uScale',
  'uPlace',
  'uVolume'
];
const DOT_UNIFORMS = [
  ...SHAPE_UNIFORMS,
  'uViewProj',
  'uEye',
  'uViewport',
  'uDpr',
  'uFibers',
  'uDots',
  'uFlow',
  'uSize',
  'uFocus',
  'uDof',
  'uMaxCoc',
  'uFocal',
  'uIntro',
  'uPulse',
  'uHover',
  'uPart',
  'uDotLength',
  'uSparkle',
  'uDepthSpread',
  'uGain',
  'uTips',
  'uTint',
  'uGradient',
  'uFold',
  'uGlowColor',
  'uLineColor',
  'uSecondaryColor'
];
const DUST_UNIFORMS = [
  'uViewProj',
  'uViewport',
  'uDpr',
  'uTime',
  'uSize',
  'uFocus',
  'uDof',
  'uMaxCoc',
  'uFocal',
  'uIntro',
  'uSparkle',
  'uScale',
  'uGradient',
  'uGain',
  'uGlowColor',
  'uLineColor',
  'uSecondaryColor'
];
const PASS_UNIFORMS = ['uSource', 'uTexel'];
const COMPOSITE_UNIFORMS = [
  'uScene',
  'uBloom',
  'uGlow',
  'uBrightness',
  'uLightMode',
  'uGrain',
  'uVignette',
  'uFrame',
  'uView',
  'uDpr'
];

const clamp = (value, min, max) => Math.min(max, Math.max(min, value));

const compile = (gl, type, source) => {
  const shader = gl.createShader(type);
  if (!shader) return null;
  gl.shaderSource(shader, source);
  gl.compileShader(shader);
  if (gl.getShaderParameter(shader, gl.COMPILE_STATUS)) return shader;
  gl.deleteShader(shader);
  return null;
};

const link = (gl, vertexSource, fragmentSource, names) => {
  const vertex = compile(gl, gl.VERTEX_SHADER, vertexSource);
  const fragment = compile(gl, gl.FRAGMENT_SHADER, fragmentSource);
  const program = gl.createProgram();
  if (!vertex || !fragment || !program) return null;
  gl.attachShader(program, vertex);
  gl.attachShader(program, fragment);
  gl.linkProgram(program);
  gl.deleteShader(vertex);
  gl.deleteShader(fragment);
  if (!gl.getProgramParameter(program, gl.LINK_STATUS)) {
    gl.deleteProgram(program);
    return null;
  }
  const uniforms = {};
  for (const name of names) uniforms[name] = gl.getUniformLocation(program, name);
  return { program, uniforms };
};

const frustum = (fov, aspect, near, far) => {
  const f = 1 / Math.tan(fov / 2);
  const nf = 1 / (near - far);
  return [f / aspect, 0, 0, 0, 0, f, 0, 0, 0, 0, (far + near) * nf, -1, 0, 0, 2 * far * near * nf, 0];
};

const multiply = (a, b) => {
  const out = new Array(16);
  for (let col = 0; col < 4; col += 1) {
    for (let row = 0; row < 4; row += 1) {
      out[col * 4 + row] =
        a[row] * b[col * 4] + a[4 + row] * b[col * 4 + 1] + a[8 + row] * b[col * 4 + 2] + a[12 + row] * b[col * 4 + 3];
    }
  }
  return out;
};

const orientation = (yaw, pitch, roll) => {
  const cy = Math.cos(yaw);
  const sy = Math.sin(yaw);
  const cp = Math.cos(pitch);
  const sp = Math.sin(pitch);
  const cr = Math.cos(roll);
  const sr = Math.sin(roll);
  const ry = [cy, 0, -sy, 0, 1, 0, sy, 0, cy];
  const rx = [1, 0, 0, 0, cp, sp, 0, -sp, cp];
  const rz = [cr, sr, 0, -sr, cr, 0, 0, 0, 1];
  const mul = (a, b) => {
    const out = new Array(9);
    for (let col = 0; col < 3; col += 1) {
      for (let row = 0; row < 3; row += 1) {
        out[col * 3 + row] = a[row] * b[col * 3] + a[3 + row] * b[col * 3 + 1] + a[6 + row] * b[col * 3 + 2];
      }
    }
    return out;
  };
  return mul(rz, mul(rx, ry));
};

const applyMat3 = (m, v) => [
  m[0] * v[0] + m[3] * v[1] + m[6] * v[2],
  m[1] * v[0] + m[4] * v[1] + m[7] * v[2],
  m[2] * v[0] + m[5] * v[1] + m[8] * v[2]
];

function mountGhostFibers(container, {
  glowColor = '#8b5cf6',
  lineColor,
  secondaryColor,
  gradient = 'depth',
  speed = 0.5,
  scale = 1,
  rotation = 18,
  rollSpeed = 0.15,
  layers = 3,
  waves = 1,
  twist = 1.2,
  threads = 72,
  volume = 0.7,
  spread = 1,
  density = 1,
  thickness = 1,
  flow = 0.4,
  fiberStyle = 'dots',
  tips = 0,
  foldGlow = 1,
  perspective = 0.65,
  depthOfField = 0.85,
  focusDepth = 0,
  particles = 0.5,
  sparkle = 0.5,
  glow = 0.8,
  brightness = 1,
  vignette = 0.3,
  grain = 0.06,
  mouseInteraction = true,
  hoverEffect = 'focus',
  mouseStrength = 1,
  pulseOnClick = true,
  intro = true,
  lightMode = false,
  paused = false,
  dpr,
  ...rest
} = {}) {
  const settings = {
    glowColor: String(glowColor),
    lineColor: lineColor ? String(lineColor) : '',
    secondaryColor: secondaryColor ? String(secondaryColor) : '',
    gradient: GRADIENTS[gradient] ?? 0,
    speed: Math.max(0, speed),
    scale: clamp(scale, 0.3, 3),
    rotation: rotation * DEG,
    rollSpeed,
    layers: clamp(Math.round(layers), 1, 3),
    waves: Math.max(0, waves),
    twist: Math.max(0, twist),
    threads: clamp(Math.round(threads), 6, 180),
    volume: clamp(volume, 0, 2),
    spread: clamp(spread, 0.2, 3),
    density: clamp(density, 0.2, 3),
    thickness: clamp(thickness, 0.2, 4),
    flow,
    dotLength: FIBER_STYLES[fiberStyle] ?? 0,
    tips: clamp(tips, 0, 1),
    foldGlow: clamp(foldGlow, 0, 3),
    perspective: clamp(perspective, 0, 1),
    depthOfField: clamp(depthOfField, 0, 2),
    focusDepth: clamp(focusDepth, -1, 1),
    particles: clamp(particles, 0, 2),
    sparkle: clamp(sparkle, 0, 2),
    glow: Math.max(0, glow),
    brightness: Math.max(0, brightness),
    vignette: clamp(vignette, 0, 1),
    grain: Math.max(0, grain),
    mouseInteraction,
    hover: HOVER_EFFECTS[hoverEffect] ?? 0,
    mouseStrength: Math.max(0, mouseStrength),
    pulseOnClick,
    intro,
    lightMode,
    paused,
    dpr
  };
  const settingsRef = { current: settings };
  const wakeRef = { current: null };
    const canvas = document.createElement('canvas');
    canvas.className = 'ghost-fibers-canvas';
    canvas.setAttribute('aria-hidden', 'true');
    container.appendChild(canvas);
    const gl = canvas?.getContext('webgl2', {
      alpha: true,
      premultipliedAlpha: true,
      antialias: false,
      depth: false,
      stencil: false
    });
    if (!gl) { canvas.remove(); return null; }

    const floatTargets = !!gl.getExtension('EXT_color_buffer_float');
    const dots = link(gl, DOT_VERTEX, DOT_FRAGMENT, DOT_UNIFORMS);
    const dust = link(gl, DUST_VERTEX, DOT_FRAGMENT, DUST_UNIFORMS);
    const bright = link(gl, FULLSCREEN, BRIGHT_FRAGMENT, PASS_UNIFORMS);
    const down = link(gl, FULLSCREEN, DOWN_FRAGMENT, PASS_UNIFORMS);
    const up = link(gl, FULLSCREEN, UP_FRAGMENT, PASS_UNIFORMS);
    const composite = link(gl, FULLSCREEN, COMPOSITE_FRAGMENT, COMPOSITE_UNIFORMS);
    if (!dots || !dust || !bright || !down || !up || !composite) { canvas.remove(); return null; }

    const format = floatTargets ? gl.RGBA16F : gl.RGBA8;
    const makeTarget = () => ({ texture: null, framebuffer: gl.createFramebuffer(), width: 0, height: 0 });
    const allocate = (target, width, height) => {
      if (target.texture && target.width === width && target.height === height) return;
      if (target.texture) gl.deleteTexture(target.texture);
      const texture = gl.createTexture();
      gl.bindTexture(gl.TEXTURE_2D, texture);
      gl.texStorage2D(gl.TEXTURE_2D, 1, format, width, height);
      gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MIN_FILTER, gl.LINEAR);
      gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_MAG_FILTER, gl.LINEAR);
      gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_S, gl.CLAMP_TO_EDGE);
      gl.texParameteri(gl.TEXTURE_2D, gl.TEXTURE_WRAP_T, gl.CLAMP_TO_EDGE);
      gl.bindFramebuffer(gl.FRAMEBUFFER, target.framebuffer);
      gl.framebufferTexture2D(gl.FRAMEBUFFER, gl.COLOR_ATTACHMENT0, gl.TEXTURE_2D, texture, 0);
      target.texture = texture;
      target.width = width;
      target.height = height;
    };
    const scene = makeTarget();
    const chain = Array.from({ length: BLOOM_LEVELS }, makeTarget);
    const vao = gl.createVertexArray();

    const probe = document.createElement('canvas');
    probe.width = 1;
    probe.height = 1;
    const probeContext = probe.getContext('2d', { willReadFrequently: true });
    const reduce = window.matchMedia?.('(prefers-reduced-motion: reduce)').matches ?? false;
    const state = {
      time: 0,
      roll: 0,
      flow: 0,
      frame: 0,
      intro: settingsRef.current.intro && !reduce ? 0 : INTRO_SECONDS,
      width: 1,
      height: 1,
      fit: 1,
      colorKey: '',
      glow: [0.55, 0.36, 0.96],
      line: [1, 0.85, 0.98],
      secondary: [0.44, 0.29, 0.77],
      pointer: { x: 0, y: 0, inside: false },
      hover: { x: 0, y: 0, presence: 0, placed: false },
      look: { x: 0, y: 0, vx: 0, vy: 0 },
      focus: CAMERA + settingsRef.current.focusDepth * 3,
      pulse: { s: 0, age: 9, strength: 0, ribbon: 0 },
      camera: null
    };
    let raf = 0;
    let last = 0;
    let visible = true;
    let alive = true;

    const toRgb = (value, fallback) => {
      if (!probeContext || !value) return fallback;
      const css = /^[0-9a-f]{3,8}$/i.test(value) ? `#${value}` : value;
      probeContext.clearRect(0, 0, 1, 1);
      probeContext.fillStyle = '#000000';
      probeContext.fillStyle = css;
      probeContext.fillRect(0, 0, 1, 1);
      const [r, g, b] = probeContext.getImageData(0, 0, 1, 1).data;
      return [r / 255, g / 255, b / 255];
    };

    const resolveColors = s => {
      const key = `${s.glowColor}|${s.lineColor}|${s.secondaryColor}|${s.lightMode}`;
      if (key === state.colorKey) return;
      state.colorKey = key;
      state.glow = toRgb(s.glowColor, [0.55, 0.36, 0.96]);
      state.secondary = s.secondaryColor ? toRgb(s.secondaryColor, state.glow) : state.glow.map(c => c * 0.8);
      if (s.lineColor) state.line = toRgb(s.lineColor, state.glow);
      else state.line = s.lightMode ? state.glow : state.glow.map(c => c + (1 - c) * 0.72);
    };

    const centerLocal = (s, t, ribbon, waves) => {
      const place = PLACEMENTS[ribbon];
      const ph = place[3];
      const x = s * RIBBON_LENGTH;
      const y =
        waves * (0.52 * Math.sin(x * 0.43 + t * 0.31 + ph) + 0.26 * Math.sin(x * 0.79 - t * 0.23 + 1.3 + ph * 0.7)) +
        place[0] +
        x * place[2];
      const z = waves * 0.65 * Math.sin(x * 0.33 + t * 0.19 + 0.7 + ph * 1.3) + place[1];
      return [x, y, z];
    };

    const cameraFor = s => {
      const aspect = state.width / Math.max(state.height, 1);
      const eye = [0, 0, CAMERA];
      const projection = frustum(FOV, aspect, 0.1, 60);
      const view = [1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, -eye[0], -eye[1], -eye[2], 1];
      const orient = orientation(s.perspective * 0.85 + state.look.x * 0.22, 0.12 - state.look.y * 0.14, s.rotation);
      return { eye, viewProj: multiply(projection, view), orient };
    };

    const screenOf = (camera, world) => {
      const m = camera.viewProj;
      const x = m[0] * world[0] + m[4] * world[1] + m[8] * world[2] + m[12];
      const y = m[1] * world[0] + m[5] * world[1] + m[9] * world[2] + m[13];
      const w = m[3] * world[0] + m[7] * world[1] + m[11] * world[2] + m[15];
      return { x: ((x / w) * 0.5 + 0.5) * state.width, y: (0.5 - (y / w) * 0.5) * state.height, depth: w };
    };

    const nearestOnRibbon = (s, px, py) => {
      const camera = state.camera;
      if (!camera) return null;
      let best = null;
      for (let ribbon = 0; ribbon < s.layers; ribbon += 1) {
        for (let i = 0; i <= 96; i += 1) {
          const u = i / 96 - 0.5;
          const local = centerLocal(u, state.time, ribbon, s.waves).map(c => c * s.scale * state.fit);
          const world = applyMat3(camera.orient, local);
          const screen = screenOf(camera, world);
          const gap = Math.hypot(screen.x - px, screen.y - py);
          if (!best || gap < best.gap) best = { gap, s: u, ribbon, depth: screen.depth };
        }
      }
      return best;
    };

    const resize = () => {
      const s = settingsRef.current;
      const width = Math.max(1, container.clientWidth);
      const height = Math.max(1, container.clientHeight);
      const baseDpr = Math.min(s.dpr || window.devicePixelRatio || 1, 2);
      const longest = Math.max(width, height) * baseDpr;
      const ratio = longest > MAX_RENDER_DIM ? (baseDpr * MAX_RENDER_DIM) / longest : baseDpr;
      const pixelWidth = Math.max(1, Math.round(width * ratio));
      const pixelHeight = Math.max(1, Math.round(height * ratio));
      if (canvas.width !== pixelWidth || canvas.height !== pixelHeight) {
        canvas.width = pixelWidth;
        canvas.height = pixelHeight;
      }
      state.width = width;
      state.height = height;
      state.fit = clamp(width / height / 1.5, 0.6, 1);
      render();
    };

    const drawPass = (program, target, source, texel) => {
      gl.bindFramebuffer(gl.FRAMEBUFFER, target.framebuffer);
      gl.viewport(0, 0, target.width, target.height);
      gl.useProgram(program.program);
      gl.activeTexture(gl.TEXTURE0);
      gl.bindTexture(gl.TEXTURE_2D, source.texture);
      gl.uniform1i(program.uniforms.uSource, 0);
      gl.uniform2f(program.uniforms.uTexel, texel[0], texel[1]);
      gl.drawArrays(gl.TRIANGLES, 0, 3);
    };

    const render = () => {
      const s = settingsRef.current;
      resolveColors(s);
      const camera = cameraFor(s);
      state.camera = camera;
      const ratio = canvas.height / Math.max(state.height, 1);
      const intro = s.paused || reduce ? 1 : clamp(state.intro / INTRO_SECONDS, 0, 1);
      const introEase = 1 - (1 - intro) * (1 - intro) * (1 - intro);

      allocate(scene, canvas.width, canvas.height);
      gl.bindVertexArray(vao);
      gl.bindFramebuffer(gl.FRAMEBUFFER, scene.framebuffer);
      gl.viewport(0, 0, canvas.width, canvas.height);
      gl.clearColor(0, 0, 0, 0);
      gl.clear(gl.COLOR_BUFFER_BIT);
      gl.enable(gl.BLEND);
      gl.blendFunc(gl.ONE, gl.ONE);

      const dotsPerFiber = Math.round(260 * s.density);
      const blurCap = 22 * clamp(Math.sqrt(56000 / (s.threads * dotsPerFiber * s.layers)), 0.45, 1);
      const area = Math.max(0.8 * s.thickness, 0.45) ** 2 / 0.64;
      const load = Math.pow((s.threads / 72) * s.density * area, -0.75);
      gl.useProgram(dots.program);
      const u = dots.uniforms;
      gl.uniform1f(u.uTime, state.time);
      gl.uniform1f(u.uTwist, s.twist);
      gl.uniform1f(u.uRoll, state.roll);
      gl.uniform1f(u.uWaves, s.waves);
      gl.uniform1f(u.uWidth, 0.62 * s.spread);
      gl.uniformMatrix3fv(u.uOrient, false, camera.orient);
      gl.uniform1f(u.uScale, s.scale * state.fit);
      gl.uniformMatrix4fv(u.uViewProj, false, camera.viewProj);
      gl.uniform3f(u.uEye, camera.eye[0], camera.eye[1], camera.eye[2]);
      gl.uniform2f(u.uViewport, canvas.width, canvas.height);
      gl.uniform1f(u.uDpr, ratio);
      gl.uniform1f(u.uFibers, s.threads);
      gl.uniform1f(u.uDots, dotsPerFiber);
      gl.uniform1f(u.uFlow, state.flow);
      gl.uniform1f(u.uSize, 1.6 * s.thickness);
      gl.uniform1f(u.uFocus, state.focus);
      gl.uniform1f(u.uDof, s.depthOfField);
      gl.uniform1f(u.uMaxCoc, blurCap);
      gl.uniform1f(u.uFocal, CAMERA);
      gl.uniform1f(u.uIntro, introEase);
      gl.uniform4f(u.uPulse, state.pulse.s, state.pulse.age, state.pulse.strength, state.pulse.ribbon);
      gl.uniform4f(
        u.uHover,
        state.hover.x * ratio,
        (state.height - state.hover.y) * ratio,
        140 * ratio,
        state.hover.presence * s.mouseStrength
      );
      gl.uniform1f(u.uPart, s.hover === 1 ? 1 : 0);
      gl.uniform1f(u.uDotLength, s.dotLength);
      gl.uniform1f(u.uSparkle, s.sparkle);
      gl.uniform1f(u.uDepthSpread, 0.12);
      gl.uniform1f(u.uVolume, s.volume);
      gl.uniform3f(u.uGlowColor, state.glow[0], state.glow[1], state.glow[2]);
      gl.uniform3f(u.uLineColor, state.line[0], state.line[1], state.line[2]);
      gl.uniform3f(u.uSecondaryColor, state.secondary[0], state.secondary[1], state.secondary[2]);
      gl.uniform1f(u.uTips, s.tips);
      gl.uniform1f(u.uGradient, s.gradient);
      gl.uniform1f(u.uFold, s.foldGlow);
      for (let ribbon = 0; ribbon < s.layers; ribbon += 1) {
        const place = PLACEMENTS[ribbon];
        gl.uniform1f(u.uRibbon, ribbon);
        gl.uniform4f(u.uPlace, place[0], place[1], place[2], place[3]);
        gl.uniform1f(u.uGain, RIBBON_GAIN[ribbon] * load);
        gl.uniform1f(u.uTint, RIBBON_TINT[ribbon]);
        gl.drawArraysInstanced(gl.TRIANGLE_STRIP, 0, 4, s.threads * dotsPerFiber);
      }

      const dustCount = Math.round(420 * s.particles);
      if (dustCount > 0) {
        gl.useProgram(dust.program);
        const d = dust.uniforms;
        gl.uniformMatrix4fv(d.uViewProj, false, camera.viewProj);
        gl.uniform2f(d.uViewport, canvas.width, canvas.height);
        gl.uniform1f(d.uDpr, ratio);
        gl.uniform1f(d.uTime, state.time);
        gl.uniform1f(d.uSize, 2.2 * s.thickness);
        gl.uniform1f(d.uFocus, state.focus);
        gl.uniform1f(d.uDof, s.depthOfField);
        gl.uniform1f(d.uMaxCoc, 22);
        gl.uniform1f(d.uFocal, CAMERA);
        gl.uniform1f(d.uIntro, introEase);
        gl.uniform1f(d.uSparkle, s.sparkle);
        gl.uniform1f(d.uScale, s.scale * state.fit);
        gl.uniform1f(d.uGradient, s.gradient);
        gl.uniform1f(d.uGain, 1 / s.thickness);
        gl.uniform3f(d.uGlowColor, state.glow[0], state.glow[1], state.glow[2]);
        gl.uniform3f(d.uLineColor, state.line[0], state.line[1], state.line[2]);
        gl.uniform3f(d.uSecondaryColor, state.secondary[0], state.secondary[1], state.secondary[2]);
        gl.drawArraysInstanced(gl.TRIANGLE_STRIP, 0, 4, dustCount);
      }
      gl.disable(gl.BLEND);

      const blooming = s.glow > 0.001 && !s.lightMode;
      gl.bindVertexArray(vao);
      if (blooming) {
        chain.forEach((target, index) => {
          allocate(
            target,
            Math.max(1, Math.round(canvas.width / 2 ** (index + 1))),
            Math.max(1, Math.round(canvas.height / 2 ** (index + 1)))
          );
        });
        drawPass(bright, chain[0], scene, [0.5 / scene.width, 0.5 / scene.height]);
        for (let index = 1; index < BLOOM_LEVELS; index += 1) {
          drawPass(down, chain[index], chain[index - 1], [1 / chain[index - 1].width, 1 / chain[index - 1].height]);
        }
        gl.enable(gl.BLEND);
        gl.blendFunc(gl.ONE, gl.ONE);
        for (let index = BLOOM_LEVELS - 1; index > 0; index -= 1) {
          drawPass(up, chain[index - 1], chain[index], [0.5 / chain[index].width, 0.5 / chain[index].height]);
        }
        gl.disable(gl.BLEND);
      }

      gl.bindFramebuffer(gl.FRAMEBUFFER, null);
      gl.viewport(0, 0, canvas.width, canvas.height);
      gl.clearColor(0, 0, 0, 0);
      gl.clear(gl.COLOR_BUFFER_BIT);
      gl.useProgram(composite.program);
      const c = composite.uniforms;
      gl.activeTexture(gl.TEXTURE0);
      gl.bindTexture(gl.TEXTURE_2D, scene.texture);
      gl.activeTexture(gl.TEXTURE1);
      gl.bindTexture(gl.TEXTURE_2D, blooming ? chain[0].texture : scene.texture);
      gl.uniform1i(c.uScene, 0);
      gl.uniform1i(c.uBloom, 1);
      gl.uniform1f(c.uGlow, blooming ? s.glow : 0);
      gl.uniform1f(c.uBrightness, s.brightness);
      gl.uniform1f(c.uLightMode, s.lightMode ? 1 : 0);
      gl.uniform1f(c.uGrain, s.grain);
      gl.uniform1f(c.uVignette, s.vignette);
      gl.uniform1f(c.uFrame, state.frame % 977);
      gl.uniform2f(c.uView, canvas.width, canvas.height);
      gl.uniform1f(c.uDpr, ratio);
      gl.drawArrays(gl.TRIANGLES, 0, 3);
      gl.activeTexture(gl.TEXTURE1);
      gl.bindTexture(gl.TEXTURE_2D, null);
      gl.activeTexture(gl.TEXTURE0);
      gl.bindTexture(gl.TEXTURE_2D, null);
      gl.bindVertexArray(null);
    };

    const frame = now => {
      raf = 0;
      if (!alive || !visible || document.hidden) return;
      const s = settingsRef.current;
      const elapsed = last ? (now - last) / 1000 : 1 / 60;
      const dt = Math.min(0.05, elapsed);
      last = now;
      const moving = !s.paused && !reduce;
      if (moving) {
        state.frame += 1;
        state.time += dt * s.speed;
        state.roll += dt * s.speed * s.rollSpeed;
        state.flow += dt * s.flow * 12;
        state.intro += Math.min(elapsed, 1);
      } else if (state.intro < INTRO_SECONDS) {
        state.intro = INTRO_SECONDS;
      }
      state.pulse.age += dt;
      state.pulse.strength = Math.max(0, 1 - state.pulse.age / 1.8) ** 2;

      const { pointer, hover, look } = state;
      const active = s.mouseInteraction && pointer.inside && !reduce;
      if (active && !hover.placed) {
        hover.x = pointer.x;
        hover.y = pointer.y;
        hover.placed = true;
      }
      hover.x += (pointer.x - hover.x) * (1 - Math.exp(-dt / 0.08));
      hover.y += (pointer.y - hover.y) * (1 - Math.exp(-dt / 0.08));
      const goal = active ? 1 : 0;
      hover.presence += (goal - hover.presence) * (1 - Math.exp(-dt / (goal > hover.presence ? 0.3 : 0.6)));
      if (!active && hover.presence < 0.001) hover.placed = false;
      const lookX = active ? (pointer.x / state.width - 0.5) * 0.5 : 0;
      const lookY = active ? (0.5 - pointer.y / state.height) * 0.5 : 0;
      look.vx += (30 * (lookX - look.x) - 11 * look.vx) * dt;
      look.vy += (30 * (lookY - look.y) - 11 * look.vy) * dt;
      look.x += look.vx * dt;
      look.y += look.vy * dt;

      const resting = CAMERA + s.focusDepth * 3;
      let focusGoal = resting;
      if (active && s.hover === 0) {
        const near = nearestOnRibbon(s, hover.x, hover.y);
        if (near) focusGoal = resting + (near.depth - resting) * hover.presence * Math.min(1, s.mouseStrength);
      }
      state.focus += (focusGoal - state.focus) * (1 - Math.exp(-dt / 0.35));

      render();
      const settling =
        Math.abs(goal - hover.presence) > 0.002 ||
        Math.abs(lookX - look.x) > 0.0002 ||
        Math.abs(lookY - look.y) > 0.0002 ||
        Math.abs(focusGoal - state.focus) > 0.001 ||
        state.pulse.strength > 0.001;
      if (moving || settling) raf = requestAnimationFrame(frame);
      else last = 0;
    };

    const wake = () => {
      if (!raf && alive && visible && !document.hidden) raf = requestAnimationFrame(frame);
    };

    const onPointerMove = event => {
      const rect = container.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;
      state.pointer.x = x;
      state.pointer.y = y;
      state.pointer.inside = x >= 0 && y >= 0 && x <= rect.width && y <= rect.height;
      wake();
    };

    const onPointerDown = event => {
      const s = settingsRef.current;
      if (!s.mouseInteraction || !s.pulseOnClick || event.button !== 0 || reduce) return;
      if (
        event.target instanceof Element &&
        event.target.closest('a, button, input, textarea, select, label, [role="button"]')
      )
        return;
      const rect = container.getBoundingClientRect();
      const x = event.clientX - rect.left;
      const y = event.clientY - rect.top;
      if (x < 0 || y < 0 || x > rect.width || y > rect.height) return;
      const near = nearestOnRibbon(s, x, y);
      if (near) state.pulse = { s: near.s, age: 0, strength: 1, ribbon: near.ribbon };
      wake();
    };

    const onPointerLeave = () => {
      state.pointer.inside = false;
      wake();
    };

    const onVisibility = () => {
      last = 0;
      wake();
    };

    const resizeObserver = new ResizeObserver(resize);
    resizeObserver.observe(container);
    const intersection = new IntersectionObserver(entries => {
      visible = entries.some(entry => entry.isIntersecting);
      if (visible) {
        last = 0;
        wake();
      }
    });
    intersection.observe(container);
    window.addEventListener('pointermove', onPointerMove, { passive: true });
    window.addEventListener('pointerdown', onPointerDown);
    document.documentElement.addEventListener('pointerleave', onPointerLeave);
    document.addEventListener('visibilitychange', onVisibility);
    resize();
    wake();

    wakeRef.current = () => {
      if (!raf) render();
      wake();
    };

    return () => {
      alive = false;
      cancelAnimationFrame(raf);
      wakeRef.current = null;
      resizeObserver.disconnect();
      intersection.disconnect();
      window.removeEventListener('pointermove', onPointerMove);
      window.removeEventListener('pointerdown', onPointerDown);
      document.documentElement.removeEventListener('pointerleave', onPointerLeave);
      document.removeEventListener('visibilitychange', onVisibility);
      gl.deleteVertexArray(vao);
      [scene, ...chain].forEach(target => {
        if (target.texture) gl.deleteTexture(target.texture);
        gl.deleteFramebuffer(target.framebuffer);
      });
      [dots, dust, bright, down, up, composite].forEach(entry => gl.deleteProgram(entry.program));
    };
}
window.mountGhostFibers = mountGhostFibers;
})();
</script>
<script>(()=>{const root=document.documentElement;const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;const init=(sel,fn)=>document.querySelectorAll(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});
/* code-drawn data */
const rng=seed=>{let s=seed%233280;return()=>(s=(s*9301+49297)%233280)/233280};
init('[data-fibers]',el=>{if(!window.mountGhostFibers)return;const small=innerWidth<768;window.mountGhostFibers(el,{glowColor:'#8f63ff',secondaryColor:'#5b7cff',lineColor:'#ffd6a0',gradient:'depth',speed:.45,scale:small?1.15:1,rotation:-16,rollSpeed:.12,layers:3,waves:1,twist:1.2,threads:small?48:72,volume:.7,spread:1,density:small?.75:.9,thickness:1,flow:.4,fiberStyle:'dots',tips:0,foldGlow:1.1,perspective:.65,depthOfField:.85,focusDepth:0,particles:small?.35:.55,sparkle:.7,glow:.9,brightness:.95,vignette:.28,grain:.05,mouseInteraction:true,hoverEffect:'focus',mouseStrength:1,pulseOnClick:true,intro:true,lightMode:false})});
init('[data-heat]',h=>{const cols=10,rows=14,r=rng(11);for(let y=0;y<rows;y++)for(let x=0;x<cols;x++){const c=rows*.62-Math.sin(x/1.6)*1.8;const band=Math.exp(-Math.pow(y-c,2)/4);let v=band*.85+r()*.22;if(x===6&&y<5)v+=.6;const cell=document.createElement('i');cell.style.setProperty('--v',Math.min(1,v).toFixed(2));h.appendChild(cell)}});
const spark=(svg,seed)=>{const r=rng(seed),n=40,pts=[];let v=.38;for(let i=0;i<n;i++){v+=(r()-.5)*.18;v=Math.max(.12,Math.min(.6,v));let y=v;if(i>=24&&i<=28)y=Math.min(.94,v+.38-Math.abs(i-26)*.08);pts.push([(i/(n-1)*300).toFixed(1),(62-y*56).toFixed(1)])}const d='M'+pts.map(p=>p.join(' ')).join(' L');const line=svg.querySelector('.spark-line'),area=svg.querySelector('.spark-area');if(line)line.setAttribute('d',d);if(area)area.setAttribute('d',d+' L300 64 L0 64Z')};
init('.spark',s=>spark(s,7));
document.addEventListener('mirador:filter',e=>{const{name,value}=e.detail;if(name==='env')document.querySelectorAll('[data-env]').forEach(el=>el.textContent=value);if(name==='region')document.querySelectorAll('[data-region]').forEach(el=>el.textContent=value);const seed=Math.floor(Math.random()*9999)+1,r=rng(seed);document.querySelectorAll('.spark').forEach(s=>spark(s,seed));const set=(k,t)=>document.querySelectorAll('[data-k="'+k+'"]').forEach(el=>el.textContent=t);set('p99',Math.round(140+r()*90)+' ms');set('err',(0.01+r()*0.05).toFixed(2)+'%');set('rpm',(9+r()*7).toFixed(1)+'k')});
init('[data-head]',head=>{const hero=document.querySelector('.hero');let last=scrollY,queued=false;const update=()=>{queued=false;const y=scrollY;head.classList.toggle('framed',!!hero&&y<6);if(y<140)head.classList.remove('hide');else if(y>last+3)head.classList.add('hide');else if(y<last-3)head.classList.remove('hide');if(head.classList.contains('hide'))head.querySelectorAll('[data-filter].open').forEach(f=>f.classList.remove('open'));last=y};addEventListener('scroll',()=>{if(!queued){queued=true;requestAnimationFrame(update)}},{passive:true});update()});
init('.rail',rail=>{const pairs=[];rail.querySelectorAll('a[href^="#"]').forEach(a=>{const id=a.getAttribute('href');const target=id.length>1?document.querySelector(id):null;if(!target){a.hidden=true;return}if(a.closest('.rail-nav'))pairs.push([target,a])});if(!pairs.length||!('IntersectionObserver'in window))return;const io=new IntersectionObserver(entries=>entries.forEach(e=>{if(!e.isIntersecting)return;pairs.forEach(([t,a])=>a.classList.toggle('is-on',t===e.target))}),{rootMargin:'-48% 0px -50% 0px'});pairs.forEach(([t])=>io.observe(t))});
init('.theme',group=>{const buttons=[...group.querySelectorAll('[data-theme]')];if(!buttons.length)return;const set=mode=>{root.classList.toggle('light',mode==='light');document.querySelectorAll('.theme [data-theme]').forEach(b=>b.setAttribute('aria-pressed',String(b.dataset.theme===mode)));try{localStorage.setItem('mirador-theme',mode)}catch(e){}};set(root.classList.contains('light')?'light':'dark');buttons.forEach(b=>b.addEventListener('click',()=>{const mode=b.dataset.theme;if(root.classList.contains('light')===(mode==='light'))return;if(!document.startViewTransition||reduce)return set(mode);const r=b.getBoundingClientRect(),x=r.left+r.width/2,y=r.top+r.height/2;const R=Math.hypot(Math.max(x,innerWidth-x),Math.max(y,innerHeight-y));const vt=document.startViewTransition(()=>set(mode));vt.ready.then(()=>root.animate({clipPath:[`circle(0px at ${x}px ${y}px)`,`circle(${R}px at ${x}px ${y}px)`]},{duration:800,easing:'cubic-bezier(.65,0,.25,1)',pseudoElement:'::view-transition-new(root)'})).catch(()=>{})}))});
init('[data-filter]',f=>{const btn=f.querySelector('.filter-btn'),menu=f.querySelector('.filter-menu'),value=f.querySelector('.filter-value');if(!btn||!menu)return;const close=()=>{f.classList.remove('open');btn.setAttribute('aria-expanded','false')};btn.addEventListener('click',e=>{e.stopPropagation();const open=!f.classList.contains('open');document.querySelectorAll('[data-filter].open').forEach(o=>{if(o!==f)o.classList.remove('open')});f.classList.toggle('open',open);btn.setAttribute('aria-expanded',String(open))});menu.querySelectorAll('button').forEach(o=>o.addEventListener('click',()=>{if(value)value.textContent=o.textContent;menu.querySelectorAll('button').forEach(x=>x.setAttribute('aria-selected',String(x===o)));close();btn.focus();document.dispatchEvent(new CustomEvent('mirador:filter',{detail:{name:f.dataset.filter,value:o.textContent}}))}));document.addEventListener('click',e=>{if(!f.contains(e.target))close()});document.addEventListener('keydown',e=>{if(e.key==='Escape')close()})});
init('.act',b=>{if(b.hasAttribute('data-share')){b.addEventListener('click',async()=>{try{if(navigator.share)await navigator.share({title:document.title,url:location.href});else await navigator.clipboard.writeText(location.href)}catch(e){}});return}b.addEventListener('click',()=>b.setAttribute('aria-pressed',String(b.getAttribute('aria-pressed')!=='true')))});
init('form.news',form=>{const out=form.parentElement&&form.parentElement.querySelector('.news-done');form.addEventListener('submit',e=>{e.preventDefault();const input=form.querySelector('input');if(input&&!input.checkValidity()){input.focus();return}if(out)out.textContent=form.dataset.done||'';form.reset()})});
init('[data-modes]',sec=>{const seg=sec.querySelector('.seg');const buttons=seg?[...seg.querySelectorAll('[data-mode]')]:[];if(!buttons.length)return;seg.style.setProperty('--n',buttons.length);const set=(mode,animate)=>{const idx=Math.max(0,buttons.findIndex(b=>b.dataset.mode===mode));buttons.forEach((b,i)=>b.setAttribute('aria-pressed',String(i===idx)));seg.style.setProperty('--i',idx);sec.querySelectorAll('.swap').forEach(el=>{const next=el.getAttribute('data-'+mode);if(next==null||el.textContent===next)return;if(!animate||reduce||!el.animate){el.textContent=next;return}el.animate([{opacity:1,transform:'none'},{opacity:0,transform:'translateY(-30%)'}],{duration:220,easing:'ease-in'}).onfinish=()=>{el.textContent=next;el.animate([{opacity:0,transform:'translateY(30%)'},{opacity:1,transform:'none'}],{duration:380,easing:'cubic-bezier(.2,.8,.2,1)'})}})};buttons.forEach(b=>b.addEventListener('click',()=>set(b.dataset.mode,true)));document.querySelectorAll('a[href="#'+sec.id+'"][data-mode]').forEach(a=>a.addEventListener('click',()=>set(a.dataset.mode,false)))});
init('form.cform',form=>{const out=form.querySelector('.cform-done');form.addEventListener('submit',e=>{e.preventDefault();const bad=[...form.querySelectorAll('[required]')].find(f=>!f.checkValidity());if(bad){bad.focus();return}if(out)out.textContent=form.dataset.sent||'';form.reset()})});
if(!window.gsap||!window.ScrollTrigger||!root.classList.contains('motion'))return;gsap.registerPlugin(ScrollTrigger);if(window.SplitText)gsap.registerPlugin(SplitText);ScrollTrigger.config({ignoreMobileResize:true,autoRefreshEvents:'visibilitychange,DOMContentLoaded,resize'});let lenis=null;if(window.Lenis){lenis=new Lenis({lerp:0.11});lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0);document.querySelectorAll('a[href^="#"]').forEach(a=>a.addEventListener('click',e=>{const id=a.getAttribute('href');const target=id.length>1?document.querySelector(id):null;if(!target)return;e.preventDefault();lenis.scrollTo(id==='#home'?0:target,{duration:1.4})}))}
const num=name=>parseFloat(getComputedStyle(root).getPropertyValue(name))||0;const loop=(trigger,tweens)=>ScrollTrigger.create({trigger,start:'top bottom',end:'bottom top',onToggle:s=>tweens.forEach(t=>s.isActive?t.resume():t.pause())});const inView=el=>el.getBoundingClientRect().top<innerHeight*0.9;const sections=[...document.querySelectorAll('main > section')];const scenes=[];const scene=(sel,fn,eager)=>scenes.push({sel,fn,eager});const ready=new WeakSet;
const effects=sec=>{sec.querySelectorAll('[data-reveal]').forEach(el=>{if(inView(el))return;gsap.set(el,{autoAlpha:0,y:34});ScrollTrigger.create({trigger:el,start:'top 90%',once:true,onEnter:()=>gsap.to(el,{autoAlpha:1,y:0,duration:1.1,ease:'power3.out',clearProps:'transform'})})});sec.querySelectorAll('[data-parallax]').forEach(el=>{const a=parseFloat(el.dataset.parallax)||8;gsap.fromTo(el,{yPercent:-a,scale:1+a/40},{yPercent:a,scale:1+a/40,ease:'none',scrollTrigger:{trigger:el.parentElement,start:'top bottom',end:'bottom top',scrub:true}})});if(window.SplitText)sec.querySelectorAll('[data-split]').forEach(el=>{if(inView(el))return;SplitText.create(el,{type:'lines',mask:'lines',autoSplit:true,onSplit:self=>gsap.from(self.lines,{yPercent:110,duration:1.15,ease:'power4.out',stagger:0.09,scrollTrigger:{trigger:el,start:'top 86%',once:true}})})})};
const setup=sec=>{if(ready.has(sec))return;ready.add(sec);try{effects(sec)}catch(e){console.error(e)}scenes.forEach(s=>{if(sec.matches(s.sel)){try{s.fn(sec)}catch(e){console.error(e)}}});ScrollTrigger.sort()};const queue=[];let draining=false;const drain=()=>{if(draining)return;draining=true;const step=()=>{const sec=queue.shift();if(sec)setup(sec);if(queue.length)setTimeout(step,0);else draining=false};setTimeout(step,0)};const start=()=>{sections.filter(sec=>scenes.some(s=>s.eager&&sec.matches(s.sel))).forEach(setup);if(!('IntersectionObserver'in window)){sections.forEach(s=>queue.push(s));drain();return}const io=new IntersectionObserver(entries=>{entries.forEach(e=>{if(!e.isIntersecting)return;io.unobserve(e.target);sections.slice(0,sections.indexOf(e.target)+1).forEach(s=>{if(!ready.has(s)&&!queue.includes(s))queue.push(s)})});drain()},{rootMargin:'0px 0px 70% 0px'});sections.forEach(s=>{if(!ready.has(s))io.observe(s)})};
scene('.hero',sec=>{const shot=sec.querySelector('.hero-shot'),drift=sec.querySelector('.hero-drift');if(!shot)return;const art=shot.querySelector('.hero-art');const tweens=[];if(drift)tweens.push(gsap.fromTo(drift,{scale:1.03,xPercent:-1.2},{scale:1.09,xPercent:1.2,duration:16,ease:'sine.inOut',repeat:-1,yoyo:true,paused:true}));const glint=sec.querySelector('.glint');if(glint)tweens.push(gsap.fromTo(glint,{xPercent:-45,yPercent:-10},{xPercent:35,yPercent:30,duration:9,ease:'sine.inOut',repeat:-1,yoyo:true,paused:true}));const startLoops=()=>setTimeout(()=>loop(sec,tweens),1200);if(document.readyState==='complete')startLoops();else addEventListener('load',startLoops,{once:true});const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top top',end:'+=90%',scrub:0.7,pin:true}});tl.fromTo(shot,{'--open':0},{'--open':1,ease:'power1.inOut'},0);if(art)tl.fromTo(art,{scale:1.14},{scale:1},0);const lines=sec.querySelectorAll('.hero-title > span');if(lines[0])tl.to(lines[0],{yPercent:-55},0);if(lines[1])tl.to(lines[1],{yPercent:-18},0);const title=sec.querySelector('.hero-title');if(title)tl.to(title,{scale:1.1,opacity:1},0);const lede=sec.querySelector('.hero-lede');if(lede)tl.to(lede,{y:-90,autoAlpha:0,duration:0.55},0);const find=sec.querySelector('.hero-find');if(find)tl.to(find,{yPercent:70,xPercent:-12,autoAlpha:0,duration:0.8},0);const feat=sec.querySelector('.hero-feat');if(feat)tl.to(feat,{yPercent:40,xPercent:26,autoAlpha:0,duration:0.9},0.05);const mark=sec.querySelector('.hero-mark');if(mark)tl.to(mark,{yPercent:90,rotate:-40,duration:0.9},0.05)});
scene('.intro',sec=>{const text=sec.querySelector('[data-light]');sec.querySelectorAll('.inl').forEach(pill=>{const g=pill.firstElementChild;const tl=gsap.timeline({scrollTrigger:{trigger:pill,start:'top 88%',end:'top 58%',scrub:0.6}}).fromTo(pill,{clipPath:'inset(0% 50% 0% 50% round 999px)'},{clipPath:'inset(0% 0% 0% 0% round 999px)',ease:'none'},0);if(g)tl.fromTo(g,{scale:1.5},{scale:1,ease:'none'},0)});if(text&&window.SplitText){const split=SplitText.create(text,{type:'words'});gsap.fromTo(split.words,{opacity:0.16},{opacity:1,ease:'none',stagger:0.08,scrollTrigger:{trigger:text,start:'top 82%',end:'bottom 52%',scrub:true}})}const stats=sec.querySelectorAll('.stats > div');if(stats.length)gsap.fromTo(stats,{'--rule':0},{'--rule':1,duration:1.4,ease:'power3.inOut',stagger:0.12,scrollTrigger:{trigger:stats[0],start:'top 92%',once:true}})});
scene('.homes',sec=>{const cards=gsap.utils.toArray(sec.querySelectorAll('.home'));cards.forEach((home,i)=>{const card=home.querySelector('.home-card'),art=card&&card.querySelector(':scope > .art'),win=card&&card.querySelector('.win');if(!card)return;const next=cards[i+1];if(art)gsap.fromTo(art,{scale:1.16,yPercent:-4},{scale:1.04,yPercent:0,ease:'none',scrollTrigger:{trigger:home,start:'top bottom',end:'top top',scrub:true}});if(win)gsap.fromTo(win,{y:80,autoAlpha:.2},{y:0,autoAlpha:1,ease:'power2.out',scrollTrigger:{trigger:home,start:'top 90%',end:'top 30%',scrub:0.6}});if(next)gsap.to(card,{scale:0.9,'--dim':0.55,ease:'none',scrollTrigger:{trigger:next,start:'top bottom',end:()=>`top ${num('--stick')+1}px`,scrub:true,invalidateOnRefresh:true}})})});
scene('.regions',sec=>{sec.querySelectorAll('.region-row').forEach(row=>{const pic=row.querySelector('.region-pic'),g=pic&&pic.querySelector('.glyphs'),name=row.querySelector('.region-name');if(!pic)return;const tl=gsap.timeline({scrollTrigger:{trigger:pic,start:'top 92%',end:'top 48%',scrub:0.7,invalidateOnRefresh:true}});tl.fromTo(pic,{clipPath:()=>`inset(0px 0px 0px ${Math.max(0,pic.offsetWidth-pic.offsetHeight)}px round 999px)`},{clipPath:'inset(0px 0px 0px 0px round 999px)',ease:'power2.inOut'},0);if(g)tl.fromTo(g,{xPercent:18,opacity:0},{xPercent:0,opacity:1,ease:'power2.out'},0);if(name)tl.fromTo(name,{xPercent:10,opacity:0},{xPercent:0,opacity:1,ease:'power2.out',duration:0.6},0)})});
scene('.gallery',sec=>{const bento=sec.querySelector('.bento'),tiles=bento?bento.querySelectorAll('[data-drift]'):[];if(!tiles.length)return;const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:bento,start:'top bottom',end:'bottom top',scrub:true}});tiles.forEach(tile=>{const d=parseFloat(tile.dataset.drift)||0;tl.fromTo(tile,{y:d},{y:-d},0)})});
scene('.process',sec=>{const stage=sec.querySelector('.proc-stage'),lens=sec.querySelector('.proc-lens');const steps=gsap.utils.toArray(sec.querySelectorAll('.proc-step'));if(!stage||!lens||steps.length<2)return;const n=steps.length,ring=sec.querySelector('.ring-fg'),art=sec.querySelector('.proc-art'),title=sec.querySelector('.proc-title');gsap.set(steps.slice(1),{autoAlpha:0,y:36});if(ring)gsap.set(ring,{strokeDashoffset:1-1/n});const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top top',end:()=>'+='+Math.round(innerHeight*0.75*(n-1)),pin:true,scrub:0.7,invalidateOnRefresh:true}});steps.forEach((s,i)=>{if(!i)return;tl.to(steps[i-1],{autoAlpha:0,y:-36,duration:0.35,ease:'power2.in'},i-0.55).to(s,{autoAlpha:1,y:0,duration:0.4,ease:'power2.out'},i-0.25);if(ring)tl.to(ring,{strokeDashoffset:1-(i+1)/n,duration:0.6,ease:'power2.inOut'},i-0.5)});tl.to({},{duration:0.3},n-1);if(art)tl.fromTo(art,{scale:1.16},{scale:1,duration:n-0.7},0);if(title)tl.to(title,{yPercent:-18,duration:n-0.7},0);if(matchMedia('(min-width: 768px)').matches)tl.fromTo(lens,{x:0},{x:()=>Math.max(0,stage.clientWidth-lens.offsetWidth-2*lens.offsetLeft),duration:n-0.7,ease:'power1.inOut'},0)},true);
scene('.pricing',sec=>{const plans=gsap.utils.toArray(sec.querySelectorAll('.plan')).filter(p=>!inView(p));if(!plans.length)return;gsap.set(plans,{y:110,autoAlpha:0});ScrollTrigger.create({trigger:plans[0],start:'top 92%',once:true,onEnter:()=>gsap.to(plans,{y:0,autoAlpha:1,duration:1.2,ease:'power4.out',stagger:0.12,clearProps:'transform'})})});
scene('.team',sec=>{const mates=sec.querySelectorAll('.mate');if(!mates.length)return;const tl=gsap.timeline({scrollTrigger:{trigger:mates[0],start:'top 85%',once:true}});mates.forEach((m,i)=>{const pic=m.querySelector('.mate-pic'),p=pic&&pic.querySelector('.portrait');if(!pic)return;tl.fromTo(pic,{clipPath:'inset(100% 0% 0% 0%)'},{clipPath:'inset(0% 0% 0% 0%)',duration:1.3,ease:'power4.inOut'},i*0.1);if(p)tl.fromTo(p,{yPercent:22,scale:1.25},{yPercent:0,scale:1,duration:1.6,ease:'power3.out'},i*0.1)})});
scene('.reviews',sec=>{const track=sec.querySelector('.rev-track');const items=track?[...track.children]:[];if(!items.length)return;items.forEach(it=>{const c=it.cloneNode(true);c.setAttribute('aria-hidden','true');c.querySelectorAll('a, button').forEach(x=>x.setAttribute('tabindex','-1'));track.appendChild(c)});const tw=gsap.to(track,{xPercent:-50,duration:items.length*10,ease:'none',repeat:-1,paused:true});let seen=false,held=false;const sync=()=>seen&&!held?tw.resume():tw.pause();track.addEventListener('mouseenter',()=>{held=true;sync()});track.addEventListener('mouseleave',()=>{held=false;sync()});track.addEventListener('focusin',()=>{held=true;sync()});track.addEventListener('focusout',()=>{held=false;sync()});ScrollTrigger.create({trigger:sec,start:'top bottom',end:'bottom top',onToggle:s=>{seen=s.isActive;sync()}})});
scene('.faq',sec=>{const items=gsap.utils.toArray(sec.querySelectorAll('.qa')).filter(q=>!inView(q));if(!items.length)return;gsap.set(items,{x:90,autoAlpha:0});ScrollTrigger.create({trigger:items[0],start:'top 90%',once:true,onEnter:()=>gsap.to(items,{x:0,autoAlpha:1,duration:1.1,ease:'power3.out',stagger:0.08,clearProps:'transform'})})});
scene('.sell',sec=>{const shot=sec.querySelector('.sell-shot'),plate=sec.querySelector('.sell-plate'),art=shot&&shot.querySelector('.art'),shield=sec.querySelector('.shield');if(!shot)return;const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top bottom',end:'top 12%',scrub:0.7}});tl.fromTo(shot,{'--close':0},{'--close':1,ease:'power1.inOut'},0);if(art)tl.fromTo(art,{scale:1.18},{scale:1},0);if(shield)tl.fromTo(shield,{rotate:-12,scale:.8,autoAlpha:0},{rotate:0,scale:1,autoAlpha:1,ease:'power2.out',duration:0.7},0.2);if(plate)tl.fromTo(plate,{yPercent:-105},{yPercent:0,ease:'power2.out',duration:0.6},0.4);sec.querySelectorAll('.sell-facts li').forEach((f,i)=>tl.fromTo(f,{y:60,autoAlpha:0},{y:0,autoAlpha:1,duration:0.3,ease:'power2.out'},0.6+i*0.1))});
scene('.contact',sec=>{const shot=sec.querySelector('.contact-shot');if(!shot)return;gsap.fromTo(shot,{clipPath:'circle(0% at 12% 88%)'},{clipPath:'circle(142% at 12% 88%)',ease:'none',scrollTrigger:{trigger:shot.parentElement,start:'top 85%',end:'top 25%',scrub:0.7}})});
sections.filter(sec=>sec.matches('.hero')).forEach(setup);Promise.race([document.fonts?document.fonts.ready:Promise.resolve(),new Promise(r=>setTimeout(r,1800))]).then(()=>setTimeout(start,0))})();</script>
</body>
</html>
```

