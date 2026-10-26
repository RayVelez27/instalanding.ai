INSTALANDING.AI · Ochre AI Meditation App Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Ochre AI Meditation App Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/ochre-ai-meditation-app-page

ochre-meditation.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Ochre AI Meditation App Page
  slug     ochre-ai-meditation-app-page
  prompt   https://instalanding.ai/p/ochre-ai-meditation-app-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/ochre-ai-meditation-app-page
  license  Fictional brand ("Ochre", Porto); every plan, price, figure, person and quote is invented.
           Replace names, numbers and copy before shipping. Every picture is drawn in code; no image files.

  MAP
  tokens    one :root block at the top of the <style>: ink --ink, paper --paper, sun --sun, sage --sage, khaki --khaki,
            rust --rust and the mixed --dim-on-ink / --soft-on-ink / --soft-on-paper; Reddit Sans 100-900 (--f-display,
            --f-text, display set at 100-300); --gut, --maxw, --head-h, --pill, --ease.
  sections  nav, hero, ticker, manifesto, features, soundscapes, privacy, day, pricing, gallery, reviews, trial, faq,
            contact, footer (each region carries data-section)
  scripts   0. (head) adds .motion unless prefers-reduced-motion, and takes it away again if GSAP never arrives
            1. Scene renderer: phone mockups (breathe, sleep, check-in, insights screens with a CSS glass breathing orb)
               and canvas landscapes painted from presets (lake at dawn, ocean at dusk, desert night with the Milky
               Way, forest rain, northern lights, valley fog, moonlit water), with live rain and snow; the hero phone
               runs a real-time WebGL ocean that tilts toward the pointer, falling back to the painted ocean
            2. UI that works without motion: progress bar, menu, smooth anchors, pillar heights from the prices, the
               trial disc size, the local-only signup form
            3. (motion only) GSAP 3.13 + ScrollTrigger + SplitText and Lenis 1.3.4 (jsdelivr): the hero's ink field
               sweeping across the paper while the sun sets, words lighting up, ruled feature rows, soundscape
               cards rising in staggered parallax, the moon window opening into the night scene, a sun dot running
               down the day timeline, price pillars rising, the collage drifting, the quote marquee, the trial
               title turning paper inside a growing ink disc
  assets    no image files

  ADAPTING
  - Paint a new picture with <canvas class="scene" data-scene="name"> and a preset in P (sky stops, sun or moon,
    clouds, ridge layers, fog, water, weather).
  - Phones are <div class="phone" data-screen="breathe|sleep|checkin|insights" data-scene="...">.
  - Fill-to-width words (.wm) size from --len; pillar heights come from the price text.
  - prefers-reduced-motion: no pinning, scrubbing, breathing or weather; one still frame of each scene.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Ochre — Meditation That Listens</title>
<meta name="description" content="Ochre is an AI meditation app that hears your breath, learns your day and builds a session that fits — from three minutes to a full night's sleep.">
<script>(function(){var d=document.documentElement;if(!window.matchMedia||!matchMedia('(prefers-reduced-motion: reduce)').matches){d.classList.add('motion');setTimeout(function(){if(!window.gsap)d.classList.remove('motion')},2500)}})();</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Reddit+Sans:ital,wght@0,200..900;1,200..900&display=swap">
<style>
:root{--ink:#01262d;--paper:#f5c279;--sun:#ee8903;--sage:#586354;--khaki:#8c7d5a;--rust:#9a4703;
--f-display:'Reddit Sans', system-ui, sans-serif;--f-text:'Reddit Sans', system-ui, sans-serif;--gut:clamp(16px, 3.4vw, 48px);--maxw:1520px;--head-h:64px;--pill:999px;--rule:1px;--ease:cubic-bezier(.2, .7, .1, 1);--dim-on-ink:color-mix(in oklab, var(--paper) 26%, var(--ink));--soft-on-ink:color-mix(in oklab, var(--paper) 72%, var(--ink));--soft-on-paper:color-mix(in oklab, var(--ink) 78%, var(--paper));}
@media (max-width:760px){:root{--head-h:56px;}}
*, *::before, *::after{box-sizing:border-box;}
html{background:var(--paper);color:var(--ink);-webkit-text-size-adjust:100%;}
body{margin:0;font-family:var(--f-text);font-weight:400;font-size:clamp(16px, .45vw + 12px, 18px);line-height:1.5;background:var(--paper);color:var(--ink);overflow-x:clip;-webkit-font-smoothing:antialiased;}
body::after{content:'';position:fixed;inset:0;z-index:90;pointer-events:none;opacity:.08;mix-blend-mode:multiply;background-image:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='220' height='220'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1.4 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");}
::selection{background:var(--sun);color:var(--ink);}
a{color:inherit;}
h1, h2, h3, p, ul, ol, figure, blockquote, dl, dd{margin:0;}
ul, ol{padding:0;list-style:none;}
button{font:inherit;color:inherit;}
main > *{position:relative;overflow-x:clip;}
.wrap{width:100%;max-width:var(--maxw);margin:0 auto;padding:0 var(--gut);}
.sr-only{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap;}

/* ---------- rendered imagery ---------- */
.frame{position:relative;isolation:isolate;overflow:hidden;}
.art{display:block;width:100%;height:100%;}
.scene{display:block;width:100%;height:100%;background:linear-gradient(180deg,#26324a 0%,#8d7d95 45%,#e8b088 62%,#1a2030 100%);}
.layered{position:relative;}
.layered > .scene{position:absolute;inset:0;}

/* glass breathing orb */
.orb{--d:60cqi;position:relative;width:var(--d);aspect-ratio:1;border-radius:50%;flex:none;
background:radial-gradient(circle at 34% 26%,rgba(255,255,255,.96) 0,rgba(255,255,255,.55) 3.5%,rgba(255,255,255,0) 13%),radial-gradient(circle at 64% 80%,rgba(255,218,160,.7) 0,rgba(255,218,160,0) 30%),radial-gradient(circle at 42% 38%,#ffd08a 0,#f8a12a 24%,#cf6407 54%,#6a2b03 84%,#2a1001 100%);
box-shadow:0 0 calc(var(--d)*.28) calc(var(--d)*.05) rgba(238,137,3,.5),0 0 calc(var(--d)*.8) calc(var(--d)*.16) rgba(238,137,3,.22),inset calc(var(--d)*-.06) calc(var(--d)*-.09) calc(var(--d)*.2) rgba(40,10,0,.6),inset calc(var(--d)*.03) calc(var(--d)*.05) calc(var(--d)*.12) rgba(255,236,200,.35);
animation:breathe 10s cubic-bezier(.45,0,.55,1) infinite;}
.orb::before{content:'';position:absolute;inset:0;border-radius:50%;background:radial-gradient(circle at 50% 50%,transparent 61%,rgba(255,232,195,.3) 68%,transparent 71%);mix-blend-mode:screen;}
.orb::after{content:'';position:absolute;left:24%;right:24%;bottom:7%;height:15%;border-radius:50%;background:radial-gradient(ellipse at 50% 50%,rgba(255,242,215,.6),transparent 70%);filter:blur(1px);}
@keyframes breathe{0%{transform:scale(.78)}40%{transform:scale(1)}55%{transform:scale(1)}100%{transform:scale(.78)}}

/* phone mockup */
.phone{position:relative;aspect-ratio:9 / 19.5;container-type:inline-size;}
.phone::before, .phone::after{content:'';position:absolute;width:1.4cqi;border-radius:2px;background:linear-gradient(90deg,#3a3532,#8a817a,#2a2624);}
.phone::before{right:-1cqi;top:24%;height:14%;}
.phone::after{left:-1cqi;top:20%;height:8%;box-shadow:0 13cqi 0 #3a3532, 0 26cqi 0 #3a3532;}
.phone__body{position:absolute;inset:0;border-radius:15cqi;padding:3.4cqi;background:linear-gradient(135deg,#6a625c 0%,#26221f 14%,#0c0b0b 48%,#221f1d 84%,#7a716a 100%);box-shadow:inset 0 0 0 .55cqi rgba(255,255,255,.28),inset 0 0 0 1.5cqi #060606,0 4cqi 10cqi -2cqi rgba(0,0,0,.55),0 22cqi 44cqi -14cqi rgba(0,0,0,.6);}
.phone__screen{position:relative;height:100%;border-radius:11.8cqi;overflow:hidden;background:#000;container-type:inline-size;}
.phone__screen .scene{position:absolute;inset:0;}
.phone__screen::after{content:'';position:absolute;inset:0;z-index:6;pointer-events:none;background:linear-gradient(118deg,rgba(255,255,255,.17) 0%,rgba(255,255,255,.05) 26%,rgba(255,255,255,0) 40%),linear-gradient(0deg,rgba(255,255,255,.04),rgba(255,255,255,0) 30%);}
.phone__island{position:absolute;z-index:5;top:2.8cqi;left:50%;width:31cqi;height:8.8cqi;translate:-50% 0;border-radius:99px;background:radial-gradient(circle at 80% 50%,#1d2a48 0 1.3cqi,#0a0d16 1.9cqi,#000 2.4cqi);}
.phone__ui{position:absolute;inset:0;z-index:2;display:flex;flex-direction:column;padding:17cqi 7cqi 8cqi;color:#fff;font-family:var(--f-text);font-size:4.4cqi;line-height:1.3;text-shadow:0 1px 10px rgba(0,0,0,.25);background:linear-gradient(180deg,rgba(0,0,0,.32),rgba(0,0,0,0) 30%,rgba(0,0,0,0) 52%,rgba(0,0,0,.55));}
.ui-status{position:absolute;top:4.6cqi;left:10cqi;right:9cqi;display:flex;align-items:center;justify-content:space-between;font-size:4.2cqi;font-weight:600;}
.ui-ic{display:flex;align-items:center;gap:1.8cqi;}
.ui-sig{display:flex;align-items:flex-end;gap:.6cqi;height:2.8cqi;}
.ui-sig i{width:.9cqi;background:#fff;border-radius:.3cqi;}
.ui-sig i:nth-child(1){height:35%}.ui-sig i:nth-child(2){height:58%}.ui-sig i:nth-child(3){height:80%}.ui-sig i:nth-child(4){height:100%}
.ui-bat{width:6.4cqi;height:3cqi;border:.4cqi solid rgba(255,255,255,.65);border-radius:1cqi;padding:.35cqi;}
.ui-bat::before{content:'';display:block;width:72%;height:100%;background:#fff;border-radius:.3cqi;}
.ui-eyebrow{font-size:3.3cqi;letter-spacing:.24em;text-transform:uppercase;opacity:.82;font-weight:600;}
.ui-title{font-size:8.4cqi;font-weight:300;letter-spacing:-.02em;line-height:1.05;margin-top:1.6cqi;}
.ui-sub{font-size:4.2cqi;opacity:.86;margin-top:2cqi;}
.ui-clock{font-size:25cqi;font-weight:200;letter-spacing:-.05em;line-height:.9;margin-top:4cqi;}
.ui-fill{flex:1;}
.ui-orbwrap{flex:1;display:grid;place-items:center;}
.ui-orbwrap .orb{--d:60cqi;}
.ui-cue{position:relative;height:7cqi;text-align:center;font-size:5.2cqi;font-weight:300;letter-spacing:.01em;}
.ui-cue span{position:absolute;inset:0;opacity:0;animation:10s linear infinite;}
.ui-cue span:nth-child(1){animation-name:cue1}.ui-cue span:nth-child(2){animation-name:cue2}.ui-cue span:nth-child(3){animation-name:cue3}
@keyframes cue1{0%,36%{opacity:1}40%,100%{opacity:0}}
@keyframes cue2{0%,38%{opacity:0}42%,52%{opacity:1}56%,100%{opacity:0}}
@keyframes cue3{0%,54%{opacity:0}58%,96%{opacity:1}100%{opacity:0}}
.ui-progress{height:.9cqi;border-radius:9px;background:rgba(255,255,255,.25);margin-top:6cqi;overflow:hidden;}
.ui-progress i{display:block;height:100%;width:42%;background:#fff;border-radius:inherit;}
.ui-row{display:flex;justify-content:space-between;align-items:center;margin-top:3.4cqi;font-size:3.6cqi;font-variant-numeric:tabular-nums;}
.ui-glass, .ui-btn, .ui-chips span, .ui-moods span{background:rgba(255,255,255,.15);border:1px solid rgba(255,255,255,.26);-webkit-backdrop-filter:blur(14px) saturate(1.5);backdrop-filter:blur(14px) saturate(1.5);}
.ui-btn{width:15cqi;height:15cqi;border-radius:50%;display:grid;place-items:center;}
.ui-btn svg{width:6cqi;height:6cqi;}
.ui-glass{border-radius:6cqi;padding:4.5cqi;box-shadow:0 2cqi 6cqi rgba(0,0,0,.18);}
.ui-wave{display:flex;align-items:center;gap:1cqi;height:12cqi;}
.ui-wave i{flex:1;height:calc(14% + var(--r, .5) * 86%);background:linear-gradient(180deg,#fff,rgba(255,255,255,.55));border-radius:9px;}
.ui-small{font-size:3.6cqi;opacity:.86;margin-top:2.6cqi;}
.ui-chips{display:flex;flex-wrap:wrap;gap:2cqi;margin-top:3cqi;}
.ui-chips span{padding:2.2cqi 3.6cqi;border-radius:99px;font-size:3.4cqi;}
.ui-moods{display:grid;grid-template-columns:repeat(3, 1fr);gap:2.4cqi;margin-top:6cqi;}
.ui-moods span{padding:3.6cqi 0;border-radius:99px;text-align:center;font-size:3.8cqi;}
.ui-moods .on{background:var(--sun);color:var(--ink);border-color:transparent;text-shadow:none;font-weight:600;}
.ui-card{display:flex;align-items:center;gap:4cqi;font-size:4.4cqi;line-height:1.25;}
.ui-card small{display:block;font-size:3.2cqi;opacity:.8;}
.ui-play{flex:none;position:relative;width:11cqi;height:11cqi;border-radius:50%;background:var(--sun);box-shadow:0 0 6cqi rgba(238,137,3,.6);}
.ui-play::after{content:'';position:absolute;left:42%;top:29%;border-left:3.4cqi solid var(--ink);border-top:2.2cqi solid transparent;border-bottom:2.2cqi solid transparent;}
.ui-bars{display:flex;align-items:flex-end;gap:2.6cqi;height:44cqi;margin-top:8cqi;}
.ui-bars i{position:relative;flex:1;height:calc(var(--h) * 100%);background:linear-gradient(180deg,#ffb04a,rgba(238,137,3,.3));border-radius:2cqi 2cqi .8cqi .8cqi;box-shadow:0 0 4cqi rgba(238,137,3,.35);}
.ui-bars b{position:absolute;bottom:-6cqi;left:0;right:0;text-align:center;font-size:3cqi;font-weight:500;opacity:.8;}
.ui-stats{display:grid;grid-template-columns:1fr 1fr;gap:3cqi;margin-top:12cqi;font-size:6cqi;font-weight:300;}
.ui-stats small{display:block;font-size:3.2cqi;opacity:.8;font-weight:500;}
.ui-note{margin-top:3cqi;font-size:3.9cqi;}

.progress{position:fixed;z-index:80;top:0;left:0;right:0;height:2px;background:var(--sun);transform-origin:left;transform:scaleX(0);pointer-events:none;}

.tracked{font-weight:600;font-size:12.5px;line-height:1.5;letter-spacing:.42em;text-transform:uppercase;}
.h2{font-family:var(--f-display);font-weight:200;font-size:clamp(46px, 7.4vw, 124px);line-height:.94;letter-spacing:-.035em;}
.h3{font-family:var(--f-display);font-weight:300;font-size:clamp(24px, 2.3vw, 36px);line-height:1.08;letter-spacing:-.015em;}
.lead{font-size:clamp(18px, 1.1vw + 10px, 23px);line-height:1.42;}
.dark{background:var(--ink);color:var(--paper);}
.btn{position:relative;isolation:isolate;display:inline-flex;align-items:center;justify-content:center;gap:.6em;padding:15px 28px;border-radius:var(--pill);background:var(--ink);color:var(--paper);font-weight:600;font-size:15px;line-height:1.2;letter-spacing:.01em;text-decoration:none;white-space:nowrap;overflow:hidden;border:0;cursor:pointer;}
.btn::before{content:'';position:absolute;inset:0;z-index:-1;background:var(--sun);clip-path:inset(0 100% 0 0);}
.btn--sun{background:var(--sun);color:var(--ink);}
.btn--sun::before{background:var(--ink);}
.btn--paper{background:var(--paper);color:var(--ink);}
.btn .arr{width:14px;height:14px;transition:transform .45s var(--ease);}
.link{position:relative;display:inline-block;font-weight:600;text-decoration:none;white-space:nowrap;padding-bottom:3px;}
.link::after{content:'';position:absolute;left:0;right:0;bottom:0;height:1px;background:currentColor;transform-origin:left;}
.ibtn{position:relative;isolation:isolate;display:inline-grid;place-items:center;width:46px;height:46px;flex:none;border-radius:50%;border:1px solid currentColor;background:none;cursor:pointer;overflow:hidden;}
.ibtn::before{content:'';position:absolute;inset:0;z-index:-1;border-radius:50%;background:var(--sun);transform:translateY(101%);}
.ibtn svg{width:18px;height:18px;}
@media (hover:hover) and (prefers-reduced-motion:no-preference){
.btn{transition:color .45s var(--ease);}.btn::before{transition:clip-path .55s var(--ease);}
.btn:hover::before, .btn:focus-visible::before{clip-path:inset(0 0 0 0);}
.btn:hover, .btn:focus-visible{color:var(--ink);}
.btn--sun:hover, .btn--sun:focus-visible{color:var(--paper);}
.btn:hover .arr{transform:translateX(4px);}
.link:hover::after, .link:focus-visible::after{animation:redraw .8s var(--ease);}
.ibtn{transition:color .4s var(--ease);}.ibtn::before{transition:transform .5s var(--ease);}
.ibtn:hover::before, .ibtn:focus-visible::before{transform:none;}
.ibtn:hover, .ibtn:focus-visible{color:var(--ink);border-color:var(--sun);}
}
@keyframes redraw{0%{transform:scaleX(1);transform-origin:right;}45%{transform:scaleX(0);transform-origin:right;}46%{transform:scaleX(0);transform-origin:left;}100%{transform:scaleX(1);transform-origin:left;}}

.site-head{position:fixed;z-index:60;top:0;left:0;right:0;height:var(--head-h);display:flex;align-items:center;gap:28px;padding:0 var(--gut);background:color-mix(in oklab, var(--paper) 88%, transparent);-webkit-backdrop-filter:blur(14px) saturate(1.2);backdrop-filter:blur(14px) saturate(1.2);color:var(--ink);box-shadow:0 1px 0 color-mix(in oklab, var(--ink) 18%, transparent);transition:transform .45s var(--ease), background-color .3s, box-shadow .3s;}
.site-head.is-hidden{transform:translateY(-100%);}
body:has(main > .hero:first-child) .site-head:not(.is-solid){background:transparent;box-shadow:none;-webkit-backdrop-filter:none;backdrop-filter:none;}
body:has(main > .hero:first-child) .site-head:not(.is-solid) .brand{color:var(--paper);}
.brand{display:inline-flex;align-items:center;gap:10px;font-family:var(--f-display);font-weight:500;font-size:19px;letter-spacing:.02em;text-decoration:none;white-space:nowrap;}
.brand svg{width:20px;height:20px;flex:none;}
.nav{display:flex;align-items:center;gap:clamp(18px, 2.2vw, 34px);margin-left:auto;}
.nav a:not(.btn){font-size:14.5px;font-weight:500;text-decoration:none;white-space:nowrap;}
.nav .btn{padding:11px 22px;font-size:14px;}
.menu-btn{display:none;margin-left:auto;width:46px;height:46px;border:0;background:none;cursor:pointer;position:relative;}
.menu-btn span{position:absolute;left:11px;right:11px;height:1.5px;background:currentColor;transition:transform .35s var(--ease);}
.menu-btn span:first-child{top:18px;}.menu-btn span:last-child{top:27px;}
.menu-open .menu-btn span:first-child{transform:translateY(4.5px) rotate(45deg);}
.menu-open .menu-btn span:last-child{transform:translateY(-4.5px) rotate(-45deg);}
@media (max-width:1020px){
.menu-btn{display:block;z-index:2;}
.nav{position:fixed;inset:0;z-index:1;margin:0;flex-direction:column;align-items:flex-start;justify-content:center;gap:6px;padding:calc(var(--head-h) + 24px) var(--gut) 40px;background:var(--ink);color:var(--paper);visibility:hidden;opacity:0;transition:opacity .35s, visibility .35s;}
.nav a:not(.btn){font-family:var(--f-display);font-weight:200;font-size:clamp(38px, 10vw, 64px);line-height:1.12;letter-spacing:-.02em;}
.nav .btn{margin-top:28px;padding:15px 28px;font-size:15px;}
.menu-open .nav{visibility:visible;opacity:1;}
.menu-open .site-head{background:transparent;box-shadow:none;-webkit-backdrop-filter:none;backdrop-filter:none;}
.menu-open .site-head .menu-btn, .menu-open .site-head .brand{color:var(--paper);}
.menu-open .brand{position:relative;z-index:2;}
}

/* hero */
.hero{--split-0:38%;--sweep:0;--split:calc(var(--split-0) + (100% - var(--split-0)) * var(--sweep));--disc:min(64svh, 44vw);background:var(--paper);}
.hero__stage{position:relative;height:100svh;min-height:620px;display:flex;flex-direction:column;overflow:hidden;}
.hero__poster{position:relative;flex:1;}
.motion .hero::after{content:'';display:block;height:110svh;}
.motion .hero__stage{position:sticky;top:0;}
.hero__field{position:absolute;inset:0;background:var(--ink);clip-path:inset(0 calc(100% - var(--split)) 0 0);}
.hero__field::after{content:'';position:absolute;inset:0;background-image:radial-gradient(circle, color-mix(in oklab, var(--paper) 22%, transparent) 1px, transparent 1.4px);background-size:9px 9px;-webkit-mask-image:linear-gradient(180deg, transparent 40%, #000);mask-image:linear-gradient(180deg, transparent 40%, #000);opacity:.5;}
.hero__sun{position:absolute;left:var(--split-0);top:17%;width:var(--disc);aspect-ratio:1;z-index:1;}
.hero__disc{width:100%;height:100%;border-radius:50%;background:radial-gradient(circle at 34% 30%, color-mix(in oklab, var(--sun) 65%, #fff4dc), var(--sun) 44%, color-mix(in oklab, var(--sun) 80%, var(--rust)));box-shadow:0 0 120px color-mix(in oklab, var(--sun) 45%, transparent), inset -30px -40px 90px color-mix(in oklab, var(--rust) 55%, transparent);}
.hero__orbit{position:absolute;left:-16%;top:-9%;width:124%;height:124%;fill:none;stroke:var(--sun);stroke-width:.22;overflow:visible;}
.hero__title{position:absolute;z-index:3;left:0;right:0;top:calc(var(--head-h) - .4vw);container-type:inline-size;font-weight:inherit;}
.wm{display:block;padding:0 var(--gut);font-family:var(--f-display);font-weight:200;font-size:calc((100cqi - 2 * var(--gut)) / var(--len) / .64);line-height:.8;letter-spacing:-.02em;white-space:nowrap;background:linear-gradient(90deg, var(--paper) var(--split), var(--ink) var(--split));-webkit-background-clip:text;background-clip:text;color:transparent;}
.hero__year{--glow:0;position:absolute;z-index:2;left:var(--gut);top:45%;font-family:var(--f-display);font-weight:100;font-size:min(19svh, 12vw);line-height:.84;letter-spacing:-.03em;color:color-mix(in oklab, var(--sun) calc(var(--glow) * 100%), var(--dim-on-ink));}
.hero__year span{display:block;}
.hero__pillars{position:absolute;z-index:3;left:var(--gut);right:29%;bottom:0;height:27%;display:flex;align-items:flex-end;}
.pillar{flex:var(--w, 1) 1 0;height:var(--h, 60%);background:var(--c, var(--khaki));}
.pl-a{--w:1;--h:72%;--c:var(--khaki);}.pl-b{--w:1.4;--h:100%;--c:var(--sage);}.pl-c{--w:.8;--h:58%;--c:color-mix(in oklab, var(--sage) 55%, var(--ink));}.pl-d{--w:2.2;--h:88%;--c:var(--khaki);}.pl-e{--w:1.1;--h:44%;--c:color-mix(in oklab, var(--khaki) 45%, var(--paper));}.pl-f{--w:1.6;--h:76%;--c:var(--sage);}.pl-g{--w:.9;--h:34%;--c:var(--rust);}
.hero__figure{position:absolute;z-index:4;left:24%;bottom:-13%;width:min(17vw, 31svh);perspective:1100px;}
.phone--tilt{transform:rotateX(var(--rx, 0deg)) rotateY(var(--ry, 0deg));transform-style:preserve-3d;will-change:transform;}
.gl3d{background:linear-gradient(180deg,#120f2a 0%,#4a2a4e 38%,#e9874a 56%,#1a1626 60%,#05070d 100%);}
.hero__dates{position:absolute;z-index:3;left:calc(var(--split-0) + var(--disc) * .66);top:calc(17% + var(--disc) * .47);max-width:calc(100% - var(--split-0) - var(--disc) * .66 - var(--gut));}
.hero__intro{position:absolute;z-index:4;right:var(--gut);bottom:4%;width:min(25vw, 360px);}
.hero__intro p{font-size:clamp(16px, .5vw + 11px, 19px);line-height:1.45;}
.hero__actions{display:flex;flex-wrap:wrap;align-items:center;gap:14px 24px;margin-top:22px;}
.hero__base{position:relative;z-index:5;flex:none;display:flex;flex-wrap:wrap;justify-content:space-between;gap:6px 32px;padding:14px var(--gut) 12px;background:var(--paper);font-size:12px;line-height:1.35;}
.hero__base::before{content:'';position:absolute;left:var(--gut);right:var(--gut);top:4px;height:5px;border-top:1px solid var(--ink);border-bottom:1px solid var(--ink);}
.hero__base p:nth-child(2){text-align:center;}.hero__base p:last-child{text-align:right;}
@media (max-width:760px){
.hero{--split-0:40%;--disc:60vw;}.hero__stage{min-height:640px;}.hero__sun{top:11%;}
.hero__year{top:41%;font-size:min(14svh, 22vw);}
.hero__pillars{left:0;right:42%;height:24%;}
.hero__figure{left:6%;width:32vw;bottom:-10%;}
.hero__dates{left:auto;right:var(--gut);top:calc(11% + var(--disc) + 16px);max-width:calc(60% - var(--gut));letter-spacing:.3em;font-size:11px;text-align:right;}
.hero__intro{width:calc(53% - var(--gut));bottom:3%;}.hero__intro p{font-size:15px;}
.hero__actions{flex-direction:column;align-items:flex-start;gap:12px;margin-top:16px;}
.hero__actions .btn{padding:13px 20px;}
.hero__base{font-size:11px;gap:4px 18px;}.hero__base p:nth-child(2){text-align:left;}
}

/* ticker */
.ticker{background:var(--sun);color:var(--ink);padding:clamp(18px, 2vw, 28px) 0;border-top:1px solid var(--ink);border-bottom:1px solid var(--ink);overflow:hidden;}
.ticker__track{display:flex;width:max-content;animation:tick 46s linear infinite;}
.ticker__track span{display:inline-flex;align-items:center;font-family:var(--f-display);font-weight:200;font-size:clamp(30px, 3.6vw, 58px);line-height:1;letter-spacing:-.025em;white-space:nowrap;}
.ticker__track i{display:inline-block;width:.34em;height:.34em;margin:0 .9em;border-radius:50%;background:var(--ink);}
.ticker__track em{font-style:italic;font-weight:300;}
@keyframes tick{to{transform:translateX(-50%);}}

/* about */
.about{padding:clamp(96px, 14vw, 200px) 0 clamp(80px, 10vw, 150px);}
.about__statement{max-width:22ch;font-family:var(--f-display);font-weight:200;font-size:clamp(34px, 4.7vw, 78px);line-height:1.04;letter-spacing:-.025em;}
.facts{display:grid;grid-template-columns:repeat(auto-fit, minmax(230px, 1fr));gap:40px var(--gut);margin-top:clamp(72px, 9vw, 140px);}
.fact{container-type:inline-size;border-top:var(--rule) solid var(--dim-on-ink);padding-top:18px;}
.fact__num{display:block;font-family:var(--f-display);font-weight:100;font-size:min(clamp(110px, 14vw, 230px), 100cqi / var(--len, 2) / .6);line-height:.82;letter-spacing:-.05em;color:var(--paper);}
.fact__text{display:block;margin-top:16px;max-width:24ch;color:var(--soft-on-ink);}
.about__arc{position:absolute;right:-12vw;top:8%;width:44vw;aspect-ratio:1;fill:none;stroke:var(--sun);stroke-width:.22;pointer-events:none;}

/* features */
.programme{padding:clamp(96px, 12vw, 180px) 0 clamp(80px, 10vw, 150px);}
.sec-head{display:grid;grid-template-columns:minmax(0, 1.4fr) minmax(0, 1fr);align-items:end;gap:28px var(--gut);margin-bottom:clamp(48px, 6vw, 88px);}
.sec-head__text{max-width:40ch;}
.prog-list{border-bottom:var(--rule) solid var(--ink);}
.prog{position:relative;}
.prog__rule{position:absolute;left:0;right:0;top:0;height:1px;background:var(--ink);transform-origin:left;}
.prog__link{position:relative;isolation:isolate;display:grid;grid-template-columns:3ch minmax(0, 1.25fr) minmax(0, 1.2fr) minmax(0, .7fr) auto;align-items:center;gap:20px var(--gut);padding:clamp(22px, 2.4vw, 34px) 0;text-decoration:none;}
.prog__link::before{content:'';position:absolute;z-index:-1;inset:0 calc(-1 * var(--gut));background:var(--ink);transform:scaleY(0);transform-origin:bottom;}
.prog__no{font-weight:600;font-size:12px;letter-spacing:.1em;font-variant-numeric:tabular-nums;align-self:start;padding-top:.9em;}
.prog__title{font-family:var(--f-display);font-weight:200;font-size:clamp(38px, 4.6vw, 76px);line-height:.96;letter-spacing:-.03em;}
.prog__text{max-width:44ch;color:var(--soft-on-paper);}
.prog__meta{font-weight:600;font-size:13px;letter-spacing:.06em;text-transform:uppercase;}
.prog__img{width:clamp(78px, 8vw, 124px);aspect-ratio:1;border-radius:50%;container-type:inline-size;box-shadow:0 14px 30px -12px rgba(1,38,45,.55), inset 0 0 0 1px rgba(255,255,255,.1);}
.prog__img .art, .prog__img .orb{transition:transform .9s var(--ease);}
.orbthumb{display:grid;place-items:center;background:radial-gradient(circle at 50% 50%,#3a1a06 0,#140902 55%,#050302 100%);}
.orbthumb .orb{--d:56cqi;}
@media (hover:hover) and (prefers-reduced-motion:no-preference){
.prog__link, .prog__text{transition:color .45s var(--ease);}
.prog__link::before{transition:transform .6s var(--ease);}
.prog__link:hover::before, .prog__link:focus-visible::before{transform:scaleY(1);}
.prog__link:hover, .prog__link:focus-visible{color:var(--paper);}
.prog__link:hover .prog__text, .prog__link:focus-visible .prog__text{color:var(--soft-on-ink);}
.prog__link:hover .prog__img .art{transform:scale(1.14);}
}
@media (max-width:900px){
.sec-head{grid-template-columns:1fr;}
.prog__link{grid-template-columns:minmax(0, 1fr) auto;}
.prog__no{display:none;}
.prog__title{grid-column:1;}
.prog__img{grid-column:2;grid-row:1 / span 2;align-self:start;width:84px;}
.prog__text, .prog__meta{grid-column:1;}
}

/* soundscapes */
.speakers{background:var(--sun);color:var(--ink);padding:clamp(96px, 12vw, 180px) 0 clamp(110px, 13vw, 200px);}
.people{display:grid;grid-template-columns:repeat(3, minmax(0, 1fr));gap:clamp(44px, 5vw, 80px) var(--gut);}
.person__frame{aspect-ratio:4 / 5.2;border-radius:var(--pill) var(--pill) 0 0;box-shadow:0 34px 60px -30px color-mix(in oklab, var(--ink) 70%, transparent);}
.person__frame .art{transition:transform 1.4s var(--ease);transform-origin:50% 70%;}
.person:hover .person__frame .art{transform:scale(1.06);}
.pill-play{position:absolute;z-index:2;left:16px;bottom:16px;display:inline-flex;align-items:center;gap:10px;padding:7px 15px 7px 7px;border-radius:99px;background:rgba(255,255,255,.16);border:1px solid rgba(255,255,255,.32);-webkit-backdrop-filter:blur(12px) saturate(1.4);backdrop-filter:blur(12px) saturate(1.4);color:#fff;font-size:13px;font-weight:600;font-variant-numeric:tabular-nums;text-shadow:0 1px 6px rgba(0,0,0,.3);}
.pill-play i{position:relative;width:28px;height:28px;border-radius:50%;background:var(--sun);box-shadow:0 0 18px rgba(238,137,3,.6);}
.pill-play i::after{content:'';position:absolute;left:11px;top:9px;border-left:8px solid var(--ink);border-top:5px solid transparent;border-bottom:5px solid transparent;}
.person__name{margin-top:20px;}
.person__role{margin-top:6px;color:color-mix(in oklab, var(--ink) 74%, var(--sun));}
.person__talk{margin-top:14px;padding-top:12px;border-top:var(--rule) solid color-mix(in oklab, var(--ink) 40%, transparent);font-weight:600;font-size:13px;letter-spacing:.05em;text-transform:uppercase;}
@media (max-width:760px){.people{grid-template-columns:repeat(2, minmax(0, 1fr));gap:36px 14px;}.person__name{font-size:20px;margin-top:14px;}.person__role{font-size:14px;}.person__talk{font-size:11.5px;}.pill-play{left:10px;bottom:10px;font-size:11px;padding-right:11px;}}

/* privacy / venue */
.venue{background:var(--ink);color:var(--paper);}
.venue__stage{position:relative;min-height:100svh;display:flex;flex-direction:column;justify-content:space-between;gap:40px;padding:calc(var(--head-h) + 7svh) var(--gut) 7svh;overflow:hidden;}
.motion .venue::after{content:'';display:block;height:140svh;}
.motion .venue__stage{position:sticky;top:0;}
.venue__photo{position:absolute;inset:0;clip-path:circle(75% at 50% 52%);}
.venue__tint{position:absolute;z-index:1;inset:0;background:var(--sun);mix-blend-mode:screen;opacity:0;pointer-events:none;}
.venue__shade{position:absolute;inset:0;background:linear-gradient(0deg, color-mix(in oklab, var(--ink) 88%, transparent) 8%, color-mix(in oklab, var(--ink) 20%, transparent) 55%, color-mix(in oklab, var(--ink) 50%, transparent));}
.venue__moon{position:absolute;left:50%;top:52%;width:40vmin;aspect-ratio:1;margin:-20vmin 0 0 -20vmin;border-radius:50%;background:var(--ink);opacity:0;}
.venue__ring{position:absolute;left:50%;top:52%;width:50vmin;height:50vmin;margin:-25vmin 0 0 -25vmin;fill:none;stroke:var(--sun);stroke-width:.25;opacity:0;overflow:visible;}
.venue__title{position:relative;max-width:12ch;}
.venue__info{position:relative;display:grid;grid-template-columns:minmax(0, 1.1fr) minmax(0, 1fr);align-items:end;gap:28px var(--gut);}
.venue__info .lead{max-width:38ch;}
.venue__facts{display:grid;gap:14px;}
.venue__facts div{display:grid;grid-template-columns:minmax(0, .8fr) minmax(0, 1.4fr);gap:16px;padding-top:12px;border-top:var(--rule) solid color-mix(in oklab, var(--paper) 40%, transparent);}
.venue__facts dt{font-weight:600;font-size:13px;letter-spacing:.05em;text-transform:uppercase;overflow-wrap:anywhere;}
.venue__actions{grid-column:1 / -1;}
@media (max-width:760px){.venue__info{grid-template-columns:1fr;}.venue__moon{width:62vmin;margin:-31vmin 0 0 -31vmin;}.venue__ring{width:76vmin;height:76vmin;margin:-38vmin 0 0 -38vmin;}}

/* day */
.schedule{--at:34%;background:linear-gradient(90deg, var(--ink) var(--at), var(--paper) var(--at));color:var(--ink);padding:clamp(100px, 12vw, 180px) 0 clamp(100px, 12vw, 180px);}
.schedule__title{display:block;padding:0 var(--gut);margin-bottom:clamp(64px, 8vw, 128px);background:linear-gradient(90deg, var(--paper) var(--at), var(--ink) var(--at));-webkit-background-clip:text;background-clip:text;color:transparent;}
.schedule__line{position:absolute;left:var(--at);top:0;bottom:0;width:2px;margin-left:-1px;background:var(--sun);transform-origin:top;}
.schedule__dot{position:absolute;left:var(--at);top:0;width:18px;height:18px;margin-left:-9px;border-radius:50%;background:var(--sun);opacity:0;box-shadow:0 0 0 6px color-mix(in oklab, var(--sun) 25%, transparent), 0 0 24px var(--sun);}
.day{position:relative;display:grid;grid-template-columns:var(--at) minmax(0, 1fr);}
.day + .day{margin-top:clamp(64px, 8vw, 120px);}
.day__head{position:sticky;top:calc(var(--head-h) + 32px);align-self:start;padding:0 var(--gut);color:var(--paper);}
.day__name{display:block;}
.day__date{display:block;margin:8px 0 0 -.04em;font-family:var(--f-display);font-weight:100;font-size:clamp(96px, 12vw, 210px);line-height:.8;letter-spacing:-.05em;color:var(--dim-on-ink);transition:color .6s var(--ease);}
.day.is-now .day__date{color:var(--sun);}
.day__month{display:block;margin-top:14px;color:var(--soft-on-ink);}
.day__list{display:grid;grid-template-columns:minmax(7ch, max-content) minmax(0, 1.5fr) minmax(0, 1fr);column-gap:28px;padding:0 var(--gut) 0 clamp(32px, 5vw, 96px);border-bottom:var(--rule) solid color-mix(in oklab, var(--ink) 30%, transparent);}
.slot{grid-column:1 / -1;display:grid;grid-template-columns:subgrid;align-items:baseline;gap:6px 28px;padding:22px 0;border-top:var(--rule) solid color-mix(in oklab, var(--ink) 30%, transparent);}
.slot > div{display:contents;}
.slot__time{max-width:12ch;overflow-wrap:anywhere;font-weight:600;font-variant-numeric:tabular-nums;padding-top:.3em;}
.slot__title{font-family:var(--f-display);font-weight:300;font-size:clamp(22px, 1.9vw, 30px);line-height:1.15;letter-spacing:-.01em;}
.slot__meta{color:var(--soft-on-paper);}
@media (max-width:760px){.schedule{--at:31%;}.day__head{padding:0 10px 0 var(--gut);}.day__name{letter-spacing:.16em;font-size:10.5px;overflow-wrap:anywhere;}.day__date{font-size:64px;}.day__month{font-size:13px;}.day__list{display:block;padding:0 var(--gut) 0 18px;}.slot{grid-template-columns:1fr;gap:4px;padding:18px 0;}.slot__time{max-width:none;padding:0;font-size:14px;}.slot__title{font-size:20px;}.slot__meta{font-size:14px;}}

/* pricing */
.tickets{padding:clamp(100px, 12vw, 180px) 0 0;}
.tiers{--p-min:96px;--p-rise:min(40svh, 380px);display:grid;grid-template-columns:repeat(auto-fit, minmax(210px, 1fr));align-items:end;gap:0 clamp(12px, 1.6vw, 24px);overflow:hidden;border-bottom:5px double color-mix(in oklab, var(--paper) 60%, transparent);}
.tier{display:flex;flex-direction:column;min-width:0;}
.tier__body{display:flex;flex-direction:column;align-items:flex-start;gap:14px;padding:0 4px 26px;}
.tier__text{color:var(--soft-on-ink);}
.tier__list{display:grid;gap:6px;font-size:15px;}
.tier__list li{position:relative;padding-left:20px;}
.tier__list li::before{content:'';position:absolute;left:0;top:.62em;width:9px;height:9px;border-radius:50%;background:var(--c);}
.tier__body .btn{margin-top:8px;}
.tier__pillar{container-type:inline-size;position:relative;min-height:calc(var(--p-min) + var(--h, .5) * var(--p-rise));padding:18px 20px;background:var(--c);color:var(--on-c, var(--ink));overflow:hidden;}
.tier__pillar::after{content:'';position:absolute;inset:0;background:linear-gradient(115deg, rgba(255,255,255,.22), rgba(255,255,255,0) 40%), linear-gradient(0deg, rgba(0,0,0,.18), rgba(0,0,0,0) 60%);pointer-events:none;}
.tier__price{font-family:var(--f-display);font-weight:200;font-size:min(clamp(54px, 5.4vw, 96px), 100cqi / var(--len, 4) / .6);line-height:.9;letter-spacing:-.04em;}
.tier__unit{display:block;margin-top:8px;font-weight:600;font-size:13px;letter-spacing:.05em;text-transform:uppercase;}
.t-khaki{--c:var(--khaki);--on-c:var(--ink);}.t-sage{--c:var(--sage);--on-c:var(--paper);}.t-sun{--c:var(--sun);--on-c:var(--ink);}.t-paper{--c:var(--paper);--on-c:var(--ink);}
.tiers__note{max-width:60ch;padding:28px 0 clamp(100px, 12vw, 170px);color:var(--soft-on-ink);}
@media (max-width:760px){.tiers{grid-template-columns:1fr;gap:44px;border-bottom:0;overflow:visible;}.tier__body{padding:0 0 18px;}.tier__pillar{min-height:0;width:calc(34% + var(--h, .5) * 66%);}.tier__price{font-size:min(52px, 100cqi / var(--len, 4) / .6);}}

/* gallery */
.gallery{padding:clamp(100px, 12vw, 180px) 0 clamp(110px, 13vw, 200px);}
.gallery__title{max-width:12ch;margin-bottom:clamp(48px, 6vw, 96px);}
.collage{position:relative;isolation:isolate;display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:clamp(16px, 2vw, 32px);align-items:start;}
.collage::before{content:'';position:absolute;z-index:-1;right:10%;top:1%;width:25%;aspect-ratio:1;border-radius:50%;background:radial-gradient(circle at 36% 32%, color-mix(in oklab, var(--sun) 65%, #fff4dc), var(--sun) 50%, color-mix(in oklab, var(--sun) 80%, var(--rust)));}
.collage::after{content:'';position:absolute;z-index:-1;left:27%;top:36%;width:7%;height:46%;background:var(--sage);}
.shot{position:relative;min-width:0;}
.shot__img{position:relative;overflow:hidden;container-type:inline-size;box-shadow:0 34px 60px -34px color-mix(in oklab, var(--ink) 75%, transparent);}
.shot__img > .art{transition:transform 1.4s var(--ease);}
.shot:hover .shot__img > .art{transform:scale(1.04);}
.shot figcaption{display:flex;gap:10px;margin-top:10px;font-size:13px;line-height:1.4;color:var(--soft-on-paper);}
.shot figcaption b{font-weight:600;color:var(--ink);font-variant-numeric:tabular-nums;}
.shot--a{grid-column:1 / 7;}.shot--a .shot__img{aspect-ratio:4 / 3;}
.shot--b{grid-column:6 / 9;margin-top:17vw;z-index:2;}.shot--b .shot__img{aspect-ratio:1;border-radius:50%;}
.shot--c{grid-column:10 / 13;margin-top:4vw;}.shot--c .shot__img{aspect-ratio:3 / 4.3;border-radius:var(--pill) var(--pill) 0 0;}
.shot--d{grid-column:3 / 9;margin-top:2vw;}.shot--d .shot__img{aspect-ratio:16 / 10;}
.shot--e{grid-column:9 / 13;margin-top:15vw;}.shot--e .shot__img{aspect-ratio:4 / 3;}
.shot--f{grid-column:1 / 4;margin-top:-9vw;z-index:2;}.shot--f .shot__img{aspect-ratio:3 / 4;}
.shot--a .phone{position:absolute;right:10%;top:7%;width:25%;transform:rotate(-7deg);filter:drop-shadow(0 26px 26px rgba(0,0,0,.45));}
.shot--c .phone{position:absolute;left:50%;bottom:-16%;width:54%;translate:-50% 0;filter:drop-shadow(0 30px 30px rgba(0,0,0,.6));}
.macro{position:relative;display:grid;place-items:center;background:radial-gradient(circle at 50% 50%,#3b1b06 0,#170a03 46%,#050302 100%);}
.macro .orb{--d:52cqi;}
.ripple{position:absolute;left:50%;top:50%;width:52cqi;aspect-ratio:1;border-radius:50%;border:1px solid rgba(255,196,130,.55);translate:-50% -50%;animation:ripple 10s cubic-bezier(.2,.6,.3,1) infinite;}
.ripple.r2{animation-delay:-5s;}
@keyframes ripple{0%{transform:scale(.8);opacity:0}10%{opacity:.7}100%{transform:scale(1.85);opacity:0}}
.studio{position:relative;display:flex;align-items:center;justify-content:center;gap:4%;perspective:1400px;background:radial-gradient(ellipse 85% 75% at 50% 32%,#fde6bd 0%,#f1b66c 42%,#bd6a1f 82%,#7a3b0c 100%);}
.studio::after{content:'';position:absolute;left:0;right:0;bottom:0;height:24%;background:linear-gradient(180deg,rgba(90,40,8,0),rgba(70,30,6,.4));pointer-events:none;}
.studio .phone{width:19%;z-index:1;-webkit-box-reflect:below 4px linear-gradient(transparent 72%, rgba(255,255,255,.2));}
.studio .phone:nth-child(1){transform:rotateY(22deg) translateY(5%);}
.studio .phone:nth-child(2){width:22%;transform:translateY(-1%);}
.studio .phone:nth-child(3){transform:rotateY(-22deg) translateY(5%);}
.focus-card{position:absolute;left:50%;top:50%;translate:-50% -50%;width:min(58%, 280px);padding:clamp(14px, 6cqi, 26px);border-radius:24px;text-align:center;color:#fff;background:rgba(255,255,255,.14);border:1px solid rgba(255,255,255,.3);-webkit-backdrop-filter:blur(16px) saturate(1.4);backdrop-filter:blur(16px) saturate(1.4);box-shadow:0 30px 60px -20px rgba(0,0,0,.55);font-size:13px;font-weight:600;letter-spacing:.04em;}
.focus-card svg{display:block;width:70%;margin:0 auto 8px;}
.candle-scene{position:relative;overflow:hidden;background:radial-gradient(ellipse 70% 60% at 50% 40%,#5c2f0d 0%,#2b1406 32%,#0d0704 66%,#040201 100%);}
.candle{position:absolute;left:50%;bottom:15%;width:28%;height:40%;translate:-50% 0;}
.candle__glow{position:absolute;left:50%;top:-60%;width:340%;aspect-ratio:1;translate:-50% -40%;border-radius:50%;background:radial-gradient(circle,rgba(255,176,72,.5) 0%,rgba(255,120,30,.14) 32%,rgba(255,120,30,0) 62%);animation:glow 3.2s ease-in-out infinite;pointer-events:none;}
.candle__wax{position:absolute;inset:16% 0 0 0;border-radius:4% 4% 3% 3% / 2% 2% 2% 2%;background:linear-gradient(90deg,#6c4b2e 0%,#d9bf9b 18%,#f6e8d0 38%,#ead2ae 60%,#a98258 84%,#4e3420 100%);box-shadow:inset 0 22px 34px -12px rgba(255,170,80,.7);}
.candle__wax::before{content:'';position:absolute;left:0;right:0;top:-5%;height:10%;border-radius:50%;background:radial-gradient(ellipse at 50% 42%,#ffe1ac 0%,#f6c98f 32%,#d9a56c 70%,#b8834f 100%);box-shadow:0 0 22px rgba(255,180,90,.6);}
.candle__wax::after{content:'';position:absolute;left:12%;top:2%;width:6%;height:30%;border-radius:0 0 50% 50%;background:linear-gradient(180deg,#f6e3c3,#e3c79e);opacity:.8;}
.candle__wick{position:absolute;left:50%;top:6%;width:2.4%;height:11%;translate:-50% 0;border-radius:40%;background:linear-gradient(#0d0703,#3a2414);}
.candle__flame{position:absolute;left:50%;bottom:89%;width:17%;height:48%;translate:-50% 0;border-radius:50% 50% 50% 50% / 64% 64% 36% 36%;background:radial-gradient(ellipse 50% 60% at 50% 76%,#fff 0%,#fff6d6 22%,#ffd36b 40%,#ff9a2a 60%,rgba(255,110,20,.35) 76%,rgba(255,110,20,0) 84%);filter:blur(.7px);transform-origin:50% 92%;animation:flick 2.8s ease-in-out infinite;box-shadow:0 -6px 30px 6px rgba(255,170,60,.35);}
.candle__flame i{position:absolute;left:28%;bottom:3%;width:44%;height:22%;border-radius:50%;background:radial-gradient(ellipse at 50% 70%,rgba(70,110,255,.6),rgba(70,110,255,0) 70%);}
.candle__table{position:absolute;left:0;right:0;bottom:0;height:16%;background:linear-gradient(180deg,#2a150a,#0b0603);}
.candle__table::before{content:'';position:absolute;left:20%;right:20%;top:-6%;height:60%;border-radius:50%;background:radial-gradient(ellipse at 50% 30%,rgba(255,160,60,.45),rgba(255,160,60,0) 70%);animation:glow 3.2s ease-in-out infinite;}
@keyframes flick{0%,100%{transform:scale(1,1) skewX(0)}20%{transform:scale(.95,1.05) skewX(1.6deg)}45%{transform:scale(1.03,.96) skewX(-1.2deg)}70%{transform:scale(.98,1.03) skewX(.8deg)}}
@keyframes glow{0%,100%{opacity:1}35%{opacity:.82}60%{opacity:.95}80%{opacity:.86}}
@media (max-width:760px){.collage{grid-template-columns:repeat(2, minmax(0, 1fr));gap:26px 14px;}.collage::before{right:-12%;top:12%;width:62%;}.collage::after{left:44%;top:54%;width:12%;height:22%;}.shot--a, .shot--d{grid-column:1 / -1;margin-top:0;}.shot--b, .shot--c, .shot--e, .shot--f{grid-column:auto;margin-top:0;}.shot--c{margin-top:16vw;}.shot--f{margin-top:16vw;}}

/* voices */
.voices{padding:clamp(100px, 12vw, 170px) 0 clamp(100px, 12vw, 170px);}
.voices__head{margin-bottom:clamp(44px, 5vw, 80px);}
.voices__head .h2{max-width:12ch;}
.voices__row{overflow:hidden;padding:0 var(--gut);}
.voices__track{display:flex;flex-wrap:wrap;gap:18px;}
.quote{flex:1 1 300px;max-width:460px;display:flex;flex-direction:column;justify-content:space-between;gap:32px;padding:clamp(24px, 2.4vw, 36px);background:var(--c);color:var(--on-c);}
.quote p{font-family:var(--f-display);font-weight:300;font-size:clamp(21px, 1.7vw, 27px);line-height:1.25;letter-spacing:-.01em;}
.quote__who{display:flex;align-items:center;gap:14px;font-size:14.5px;line-height:1.35;}
.quote__name{display:block;font-weight:600;}
.gem{--h:30;position:relative;width:52px;height:52px;flex:none;border-radius:50%;display:grid;place-items:center;color:#fff;font-size:15px;font-weight:600;letter-spacing:.04em;text-shadow:0 1px 4px rgba(0,0,0,.4);background:radial-gradient(circle at 32% 26%,rgba(255,255,255,.9) 0,rgba(255,255,255,.35) 7%,rgba(255,255,255,0) 22%),radial-gradient(circle at 50% 62%,hsl(var(--h) 90% 62%) 0,hsl(var(--h) 85% 40%) 52%,hsl(var(--h) 70% 16%) 100%);box-shadow:inset -4px -6px 10px rgba(0,0,0,.35),0 6px 14px -4px hsl(var(--h) 80% 30% / .6);}
.q-line{--c:transparent;--on-c:var(--paper);box-shadow:inset 0 0 0 1px color-mix(in oklab, var(--paper) 45%, transparent);}
.q-paper{--c:var(--paper);--on-c:var(--ink);}.q-sun{--c:var(--sun);--on-c:var(--ink);}
.voices__track.is-loop{flex-wrap:nowrap;width:max-content;gap:0;}
.voices__track.is-loop .quote{flex:none;width:clamp(290px, 30vw, 440px);max-width:none;margin-right:18px;}
@media (max-width:760px){.voices__track.is-loop .quote{width:82vw;}}

/* trial */
.opencall{background:var(--sun);color:var(--ink);padding:clamp(110px, 13vw, 200px) 0 clamp(90px, 10vw, 150px);}
.opencall__stage{--k:1;--R:20vw;position:relative;}
.opencall__disc{position:absolute;left:50%;top:50%;width:calc(2 * var(--R));height:calc(2 * var(--R));margin:calc(-1 * var(--R)) 0 0 calc(-1 * var(--R));border-radius:50%;background:radial-gradient(circle at 38% 32%, #0a3a44, var(--ink) 60%, #00161b);transform:scale(var(--k));box-shadow:0 0 0 1px rgba(1,38,45,.4), 0 40px 80px -30px rgba(1,38,45,.7);}
.opencall__ring{position:absolute;left:50%;top:50%;width:calc(2.36 * var(--R));height:calc(2.36 * var(--R));margin:calc(-1.18 * var(--R)) 0 0 calc(-1.18 * var(--R));fill:none;stroke:var(--ink);stroke-width:.2;overflow:visible;}
.opencall__title{position:relative;padding:0 var(--gut);font-family:var(--f-display);font-weight:200;font-size:clamp(60px, 10.2vw, 184px);line-height:.92;letter-spacing:-.04em;text-align:center;text-wrap:balance;background:radial-gradient(circle calc(var(--k) * var(--R)) at 50% 50%, var(--paper) calc(100% - .5px), var(--ink) 100%);-webkit-background-clip:text;background-clip:text;color:transparent;}
.opencall__foot{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:flex-end;gap:28px var(--gut);margin-top:clamp(72px, 9vw, 140px);}
.opencall__foot .lead{max-width:42ch;}
.opencall__actions{display:flex;flex-wrap:wrap;align-items:center;gap:14px 26px;}
@media (max-width:760px){.opencall__title{font-size:16vw;}}

/* faq */
.faq{padding:clamp(100px, 12vw, 180px) 0;}
.faq__grid{display:grid;grid-template-columns:minmax(0, .85fr) minmax(0, 1.3fr);gap:48px var(--gut);align-items:start;}
.faq__title{position:sticky;top:calc(var(--head-h) + 32px);max-width:8ch;}
.faq__list{border-bottom:var(--rule) solid var(--ink);}
.qa{border-top:var(--rule) solid var(--ink);}
.qa summary{display:flex;align-items:center;justify-content:space-between;gap:24px;padding:clamp(20px, 2vw, 28px) 0;list-style:none;cursor:pointer;}
.qa summary::-webkit-details-marker{display:none;}
.qa__q{font-family:var(--f-display);font-weight:300;font-size:clamp(21px, 1.8vw, 28px);line-height:1.2;letter-spacing:-.01em;}
.qa__icon svg{transition:transform .45s var(--ease);}
.qa[open] .qa__icon svg{transform:rotate(45deg);}
.qa[open] .qa__icon::before{transform:none;}
.qa[open] .qa__icon{border-color:var(--sun);}
.qa__a{max-width:60ch;padding:0 0 28px;color:var(--soft-on-paper);}
@media (hover:hover) and (prefers-reduced-motion:no-preference){.qa summary:hover .ibtn::before{transform:none;}.qa summary:hover .ibtn{border-color:var(--sun);}}
.motion .qa[open] .qa__a{animation:qa-in .6s var(--ease);}
@keyframes qa-in{from{opacity:0;transform:translateY(-10px);}}
@media (max-width:860px){.faq__grid{grid-template-columns:1fr;}.faq__title{position:static;max-width:none;}}

/* contact */
.contact{display:grid;grid-template-columns:minmax(0, 1fr) minmax(0, 1fr);background:var(--paper);}
.contact__main{background:var(--ink);color:var(--paper);padding:clamp(100px, 12vw, 170px) var(--gut) clamp(80px, 10vw, 140px);}
.contact__main .h2{max-width:9ch;}
.contact__list{margin-top:clamp(44px, 5vw, 72px);border-bottom:var(--rule) solid var(--dim-on-ink);}
.contact__list div{display:grid;grid-template-columns:minmax(0, .7fr) minmax(0, 1.6fr);gap:8px 20px;padding:18px 0;border-top:var(--rule) solid var(--dim-on-ink);}
.contact__list dt{font-weight:600;font-size:13px;letter-spacing:.05em;text-transform:uppercase;padding-top:.2em;overflow-wrap:anywhere;}
.contact__list dd{overflow-wrap:anywhere;}
.contact__side{position:relative;display:flex;flex-direction:column;padding:clamp(100px, 12vw, 170px) var(--gut) 0;overflow:hidden;}
.signup{position:relative;z-index:2;max-width:460px;}
.signup > p{margin-top:12px;color:var(--soft-on-paper);}
.signup__row{display:flex;flex-wrap:wrap;gap:10px;margin-top:24px;}
.signup__field{flex:1 1 210px;min-width:0;}
.signup input{width:100%;padding:15px 22px;border:var(--rule) solid var(--ink);border-radius:var(--pill);background:transparent;color:var(--ink);font:inherit;font-size:16px;}
.signup input::placeholder{color:var(--soft-on-paper);}
.signup input:focus-visible{outline:2px solid var(--sun);outline-offset:2px;}
.signup__status{margin-top:14px;min-height:1.5em;font-weight:600;}
.contact__scene{position:relative;margin:clamp(48px, 6vw, 90px) calc(-1 * var(--gut)) 0;height:clamp(230px, 28vw, 400px);}
.contact__sun{position:absolute;left:50%;bottom:-12%;width:min(62%, 360px);aspect-ratio:1;border-radius:50%;background:radial-gradient(circle at 36% 30%, color-mix(in oklab, var(--sun) 65%, #fff4dc), var(--sun) 48%, color-mix(in oklab, var(--sun) 80%, var(--rust)));box-shadow:0 0 90px color-mix(in oklab, var(--sun) 45%, transparent);translate:-50% 0;}
.contact__pillars{position:absolute;left:0;right:0;bottom:0;height:42%;display:flex;align-items:flex-end;}
@media (max-width:860px){.contact{grid-template-columns:1fr;}.contact__side{padding-top:72px;}.contact__list div{grid-template-columns:1fr;gap:4px;}}

/* footer */
.site-foot{position:relative;overflow-x:clip;background:var(--paper);color:var(--ink);padding:28px 0 0;}
.foot__rule{height:5px;margin:0 var(--gut);border-top:1px solid var(--ink);border-bottom:1px solid var(--ink);}
.foot__cols{display:grid;grid-template-columns:repeat(auto-fit, minmax(190px, 1fr));gap:22px var(--gut);padding:22px var(--gut) 0;font-size:13px;line-height:1.5;}
.foot__cols a{text-decoration:none;}
.foot__links{display:flex;flex-direction:column;align-items:flex-start;gap:2px;}
.foot__mark{container-type:inline-size;margin-top:clamp(32px, 5vw, 64px);}
.foot__mark .wm{--split:0%;line-height:.74;padding-bottom:1.2vw;}

@media (prefers-reduced-motion:reduce){
.ticker__track, .orb, .ripple, .candle__flame, .candle__glow, .candle__table::before, .ui-cue span{animation:none;}
.ui-cue span:first-child{opacity:1;}
}
</style>
</head>
<body>

<div class="progress" aria-hidden="true"></div>

<header class="site-head" data-section="nav">
  <a class="brand" href="#hero" aria-label="Ochre, home"><svg viewBox="0 0 20 20" aria-hidden="true"><circle cx="11" cy="10" r="8" fill="var(--sun)"/><path d="M3.6 16.5A9 9 0 0 1 6 3.2" fill="none" stroke="currentColor" stroke-width="1.2"/></svg>Ochre</a>
  <nav class="nav" id="site-nav" aria-label="Main">
    <a href="#programme">Features</a>
    <a href="#speakers">Soundscapes</a>
    <a href="#schedule">Your day</a>
    <a href="#tickets">Pricing</a>
    <a href="#contact">Contact</a>
    <a class="btn" href="#tickets">Start free</a>
  </nav>
  <button class="menu-btn" type="button" aria-expanded="false" aria-controls="site-nav" aria-label="Open menu" data-label-open="Open menu" data-label-close="Close menu"><span></span><span></span></button>
</header>

<main>
  <section id="hero" data-section="hero" class="hero" data-kind="hero">
    <div class="hero__stage">
      <div class="hero__poster">
        <div class="hero__field" aria-hidden="true"></div>
        <div class="hero__sun" aria-hidden="true">
          <div class="hero__disc"></div>
          <svg class="hero__orbit" viewBox="0 0 100 100"><circle cx="50" cy="50" r="49.5" pathLength="100" stroke-dasharray="30 70" stroke-dashoffset="-44"/></svg>
        </div>
        <h1 class="hero__title"><span class="wm" style="--len:5">OCHRE</span><span class="sr-only"> — meditation that listens</span></h1>
        <p class="hero__year" aria-hidden="true"><span>in</span><span>out</span></p>
        <div class="hero__pillars" aria-hidden="true">
          <i class="pillar pl-a"></i><i class="pillar pl-b"></i><i class="pillar pl-c"></i><i class="pillar pl-d"></i><i class="pillar pl-e"></i><i class="pillar pl-f"></i><i class="pillar pl-g"></i>
        </div>
        <div class="hero__figure" role="img" aria-label="The Ochre app on a phone, guiding a breathing session over an ocean at dusk">
          <div class="phone phone--tilt" data-screen="breathe" data-scene="ocean" data-gl="1" aria-hidden="true"></div>
        </div>
        <p class="hero__dates tracked">iOS · Android · 14 days free</p>
        <div class="hero__intro">
          <p>Meditation that listens. Ochre hears your breath, learns the shape of your day and builds a session that fits — three minutes or thirty, guided by a voice that never hurries.</p>
          <div class="hero__actions">
            <a class="btn" href="#tickets">Start free <svg class="arr" viewBox="0 0 14 14" aria-hidden="true"><path d="M1 7h11M8 3l4 4-4 4" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
            <a class="link" href="#programme">See how it works</a>
          </div>
        </div>
      </div>
      <div class="hero__base">
        <p>AI meditation companion<br>Version 4</p>
        <p>Adapts to breath, mood and sleep<br>Private by design</p>
        <p>iPhone, Android and web<br>Plans from $6 a month</p>
      </div>
    </div>
  </section>

  <div class="ticker" data-section="ticker" aria-hidden="true">
    <div class="ticker__track">
      <span>Breathwork<i></i>Sleep stories<i></i><em>Adaptive sessions</em><i></i>Focus<i></i>Body scan<i></i><em>Soundscapes</em><i></i>14 days free<i></i></span>
      <span>Breathwork<i></i>Sleep stories<i></i><em>Adaptive sessions</em><i></i>Focus<i></i>Body scan<i></i><em>Soundscapes</em><i></i>14 days free<i></i></span>
    </div>
  </div>

  <section id="about" data-section="manifesto" class="about dark" data-kind="manifesto">
    <svg class="about__arc" viewBox="0 0 100 100" aria-hidden="true" data-drift><circle cx="50" cy="50" r="49.5" pathLength="100" stroke-dasharray="34 66" stroke-dashoffset="-8"/></svg>
    <div class="wrap">
      <p class="about__statement" data-words>Ochre began with one question: what if a meditation app listened back? It hears how you breathe, notices when you slept badly and shapes every session around the person you are today — not a playlist, a practice.</p>
      <ul class="facts">
        <li class="fact" data-reveal><span class="fact__num" style="--len:1">3</span><span class="fact__text">minutes — the shortest session that still works</span></li>
        <li class="fact" data-reveal><span class="fact__num" style="--len:3">180</span><span class="fact__text">hours of original guidance and field-recorded sound</span></li>
        <li class="fact" data-reveal><span class="fact__num" style="--len:1">9</span><span class="fact__text">languages, each with its own unhurried voice</span></li>
      </ul>
    </div>
  </section>

  <section id="programme" data-section="features" class="programme" data-kind="features">
    <div class="wrap">
      <div class="sec-head">
        <h2 class="h2" data-lines>Six ways it meets you</h2>
        <p class="sec-head__text lead" data-reveal>Every plan includes all of them. Turn on what helps, ignore the rest — Ochre learns from what you actually use.</p>
      </div>
      <ul class="prog-list">
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">01</span>
            <span class="prog__title">Adaptive sessions</span>
            <span class="prog__text">Tell it how you feel in a sentence. It writes a session around that — length, pace, focus — and adjusts as you go.</span>
            <span class="prog__meta">Every session · AI-built</span>
            <span class="prog__img frame orbthumb" aria-hidden="true"><span class="orb"></span></span>
          </a>
        </li>
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">02</span>
            <span class="prog__title">Breath sensing</span>
            <span class="prog__text">Hold your phone or wear earbuds. Ochre hears your breathing slow and paces the guidance to it — never ahead of you.</span>
            <span class="prog__meta">Microphone · On device</span>
            <span class="prog__img frame" aria-hidden="true"><svg class="art" viewBox="0 0 100 100">
              <defs>
                <linearGradient id="wv" x1="0" x2="1"><stop offset="0" stop-color="#ee8903" stop-opacity="0"/><stop offset=".5" stop-color="#ffd9a0"/><stop offset="1" stop-color="#ee8903" stop-opacity="0"/></linearGradient>
                <filter id="wglow" x="-20%" y="-60%" width="140%" height="220%"><feGaussianBlur stdDeviation="2.2" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
                <radialGradient id="wbg" cx=".5" cy=".5" r=".7"><stop offset="0" stop-color="#2e1a0a"/><stop offset="1" stop-color="#050302"/></radialGradient>
              </defs>
              <rect width="100" height="100" fill="url(#wbg)"/>
              <g fill="none" stroke="url(#wv)" stroke-linecap="round" filter="url(#wglow)">
                <path d="M0 50 C10 50 14 30 22 30 S32 70 40 70 S50 22 58 22 S68 76 76 76 S88 50 100 50" stroke-width="1.6"/>
                <path d="M0 50 C12 50 16 40 24 40 S34 62 42 62 S52 34 60 34 S70 64 78 64 S90 50 100 50" stroke-width="1" opacity=".7"/>
                <path d="M0 50 C10 50 18 45 26 45 S36 56 44 56 S54 42 62 42 S72 57 80 57 S90 50 100 50" stroke-width=".6" opacity=".5"/>
              </g>
            </svg></span>
          </a>
        </li>
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">03</span>
            <span class="prog__title">Sleep</span>
            <span class="prog__text">Stories that fade as your breathing deepens, and a soft alarm that wakes you in your lightest sleep.</span>
            <span class="prog__meta">Nightly · 20–60 min</span>
            <span class="prog__img frame" aria-hidden="true"><canvas class="scene art" data-scene="desert"></canvas></span>
          </a>
        </li>
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">04</span>
            <span class="prog__title">Focus</span>
            <span class="prog__text">Fifty-minute blocks wrapped in a soundscape, with a two-minute reset between them so the afternoon doesn't eat you.</span>
            <span class="prog__meta">Workdays · 50 min</span>
            <span class="prog__img frame" aria-hidden="true"><canvas class="scene art" data-scene="forest"></canvas></span>
          </a>
        </li>
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">05</span>
            <span class="prog__title">Daily check-in</span>
            <span class="prog__text">Thirty seconds each morning: one word for your mood, one for your energy. Ochre remembers so you don't have to.</span>
            <span class="prog__meta">Mornings · 30 sec</span>
            <span class="prog__img frame" aria-hidden="true"><canvas class="scene art" data-scene="fog"></canvas></span>
          </a>
        </li>
        <li class="prog">
          <span class="prog__rule" data-rule></span>
          <a class="prog__link" href="#schedule">
            <span class="prog__no">06</span>
            <span class="prog__title">Weekly letter</span>
            <span class="prog__text">A short note each Sunday on your sleep, stress and practice — written in plain words, not dashboards.</span>
            <span class="prog__meta">Sundays · In the app</span>
            <span class="prog__img frame" aria-hidden="true"><canvas class="scene art" data-scene="ocean"></canvas></span>
          </a>
        </li>
      </ul>
    </div>
  </section>

  <section id="speakers" data-section="soundscapes" class="speakers" data-kind="soundscapes">
    <div class="wrap">
      <div class="sec-head">
        <h2 class="h2" data-lines>Places to close your eyes</h2>
        <p class="sec-head__text lead" data-reveal>Sixty soundscapes recorded on location, in spatial audio. Ochre picks one to match the session — or you choose.</p>
      </div>
      <ul class="people">
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="dawn" role="img" aria-label="Mountain lake at dawn, mist on the water"></canvas><span class="pill-play" aria-hidden="true"><i></i>30:00</span></figure>
          <h3 class="person__name h3">Mountain lake at dawn</h3>
          <p class="person__role">Lakeshore, northern Italy</p>
          <p class="person__talk">Morning · 30 min</p>
        </li>
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="ocean" role="img" aria-label="Ocean at dusk with the sun on the horizon"></canvas><span class="pill-play" aria-hidden="true"><i></i>45:00</span></figure>
          <h3 class="person__name h3">Ocean at dusk</h3>
          <p class="person__role">Atlantic coast, Portugal</p>
          <p class="person__talk">Wind-down · 45 min</p>
        </li>
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="desert" role="img" aria-label="Moonlit sand dunes under the Milky Way"></canvas><span class="pill-play" aria-hidden="true"><i></i>60:00</span></figure>
          <h3 class="person__name h3">Desert night</h3>
          <p class="person__role">Dunes, southern Morocco</p>
          <p class="person__talk">Sleep · 60 min</p>
        </li>
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="forest" role="img" aria-label="Rain falling through a misty conifer forest"></canvas><span class="pill-play" aria-hidden="true"><i></i>50:00</span></figure>
          <h3 class="person__name h3">Forest rain</h3>
          <p class="person__role">Rainforest, Pacific Northwest</p>
          <p class="person__talk">Focus · 50 min</p>
        </li>
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="aurora" role="img" aria-label="Northern lights over snowy mountains"></canvas><span class="pill-play" aria-hidden="true"><i></i>60:00</span></figure>
          <h3 class="person__name h3">Northern lights</h3>
          <p class="person__role">Snowfield, Finnish Lapland</p>
          <p class="person__talk">Sleep · 60 min</p>
        </li>
        <li class="person">
          <figure class="person__frame frame" data-rise><canvas class="scene art" data-scene="fog" role="img" aria-label="Layers of hills in valley fog at first light"></canvas><span class="pill-play" aria-hidden="true"><i></i>20:00</span></figure>
          <h3 class="person__name h3">Valley fog</h3>
          <p class="person__role">Douro valley, first light</p>
          <p class="person__talk">Breathwork · 20 min</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="venue" data-section="privacy" class="venue" data-kind="privacy">
    <div class="venue__stage">
      <figure class="venue__photo">
        <div class="venue__tint" aria-hidden="true"></div>
        <canvas class="scene art" data-scene="night" role="img" aria-label="A full moon over still water at night"></canvas>
      </figure>
      <div class="venue__shade" aria-hidden="true"></div>
      <div class="venue__moon" aria-hidden="true"></div>
      <svg class="venue__ring" viewBox="0 0 100 100" aria-hidden="true"><circle cx="50" cy="50" r="49.5" pathLength="100" stroke-dasharray="62 38" stroke-dashoffset="12"/></svg>
      <h2 class="venue__title h2">A quiet room in your pocket</h2>
      <div class="venue__info">
        <p class="lead">What Ochre hears stays with you. Your breath is analysed on the phone itself, your journal is encrypted, and nothing you say is used to train anything without your permission.</p>
        <dl class="venue__facts">
          <div><dt>Breath</dt><dd>Processed on device, never uploaded</dd></div>
          <div><dt>Offline</dt><dd>Download any session or soundscape</dd></div>
          <div><dt>Health</dt><dd>Syncs sleep and mindful minutes with your phone's health app</dd></div>
        </dl>
        <div class="venue__actions"><a class="btn btn--sun" href="#faq">Read our privacy promise</a></div>
      </div>
    </div>
  </section>

  <section id="schedule" data-section="day" class="schedule" data-kind="your day">
    <div class="schedule__line" aria-hidden="true"></div>
    <div class="schedule__dot" aria-hidden="true"></div>
    <h2 class="schedule__title h2" data-reveal>A day with Ochre</h2>
    <article class="day">
      <header class="day__head"><span class="day__name tracked">Morning</span><span class="day__date">07</span><span class="day__month">o'clock</span></header>
      <ol class="day__list">
        <li class="slot"><span class="slot__time">07:00</span><div><h3 class="slot__title">Check-in: one word for your mood</h3><p class="slot__meta">30 seconds · Lock screen</p></div></li>
        <li class="slot"><span class="slot__time">07:05</span><div><h3 class="slot__title">Wake-up breathwork</h3><p class="slot__meta">6 min · Valley fog</p></div></li>
        <li class="slot"><span class="slot__time">08:10</span><div><h3 class="slot__title">Commute mode: eyes open, earbuds in</h3><p class="slot__meta">12 min · Audio only</p></div></li>
      </ol>
    </article>
    <article class="day">
      <header class="day__head"><span class="day__name tracked">Afternoon</span><span class="day__date">13</span><span class="day__month">o'clock</span></header>
      <ol class="day__list">
        <li class="slot"><span class="slot__time">13:00</span><div><h3 class="slot__title">Focus block</h3><p class="slot__meta">50 min · Forest rain</p></div></li>
        <li class="slot"><span class="slot__time">15:30</span><div><h3 class="slot__title">Two-minute reset after a hard meeting</h3><p class="slot__meta">Breath sensing on</p></div></li>
        <li class="slot"><span class="slot__time">17:00</span><div><h3 class="slot__title">Walking meditation, phone in pocket</h3><p class="slot__meta">20 min · Audio only</p></div></li>
      </ol>
    </article>
    <article class="day">
      <header class="day__head"><span class="day__name tracked">Evening</span><span class="day__date">19</span><span class="day__month">o'clock</span></header>
      <ol class="day__list">
        <li class="slot"><span class="slot__time">19:30</span><div><h3 class="slot__title">Wind-down</h3><p class="slot__meta">15 min · Ocean at dusk</p></div></li>
        <li class="slot"><span class="slot__time">21:00</span><div><h3 class="slot__title">Voice journal: say it, then let it go</h3><p class="slot__meta">Private · Encrypted</p></div></li>
      </ol>
    </article>
    <article class="day">
      <header class="day__head"><span class="day__name tracked">Night</span><span class="day__date">23</span><span class="day__month">o'clock</span></header>
      <ol class="day__list">
        <li class="slot"><span class="slot__time">22:45</span><div><h3 class="slot__title">A sleep story that fades with your breathing</h3><p class="slot__meta">40 min · Desert night</p></div></li>
        <li class="slot"><span class="slot__time">06:50</span><div><h3 class="slot__title">Soft alarm in your lightest sleep</h3><p class="slot__meta">The next morning</p></div></li>
      </ol>
    </article>
  </section>

  <section id="tickets" data-section="pricing" class="tickets dark" data-kind="pricing">
    <div class="wrap">
      <div class="sec-head">
        <h2 class="h2" data-lines>Pick your plan</h2>
        <p class="sec-head__text lead" data-reveal>Every plan includes adaptive sessions, all sixty soundscapes and offline downloads. Try any of them free for fourteen days.</p>
      </div>
      <ul class="tiers">
        <li class="tier t-khaki">
          <div class="tier__body">
            <h3 class="h3">Monthly</h3>
            <p class="tier__text">Month to month. Cancel in two taps, any time.</p>
            <ul class="tier__list"><li>Unlimited AI sessions</li><li>All soundscapes</li><li>Sleep stories</li></ul>
            <a class="btn btn--paper" href="#contact">Start monthly</a>
          </div>
          <div class="tier__pillar"><p class="tier__price" data-price style="--len:3">$12</p><span class="tier__unit">Per month</span></div>
        </li>
        <li class="tier t-sun">
          <div class="tier__body">
            <h3 class="h3">Annual</h3>
            <p class="tier__text">What most people choose — under $6 a month.</p>
            <ul class="tier__list"><li>Everything in monthly</li><li>Breath sensing</li><li>The weekly letter</li></ul>
            <a class="btn btn--sun" href="#contact">Start annual</a>
          </div>
          <div class="tier__pillar"><p class="tier__price" data-price style="--len:3">$70</p><span class="tier__unit">Per year</span></div>
        </li>
        <li class="tier t-sage">
          <div class="tier__body">
            <h3 class="h3">Family</h3>
            <p class="tier__text">Up to six people, each with their own private practice.</p>
            <ul class="tier__list"><li>Six separate accounts</li><li>Kids' mode, ages 6–12</li><li>Shared bedtime stories</li></ul>
            <a class="btn btn--paper" href="#contact">Start family</a>
          </div>
          <div class="tier__pillar"><p class="tier__price" data-price style="--len:4">$110</p><span class="tier__unit">Per year</span></div>
        </li>
        <li class="tier t-paper">
          <div class="tier__body">
            <h3 class="h3">Lifetime</h3>
            <p class="tier__text">Pay once, keep it forever — and fund a year for someone who can't.</p>
            <ul class="tier__list"><li>Everything, for good</li><li>Early access to new guides</li><li>One gifted annual plan</li></ul>
            <a class="btn btn--paper" href="#contact">Go lifetime</a>
          </div>
          <div class="tier__pillar"><p class="tier__price" data-price style="--len:4">$240</p><span class="tier__unit">Once</span></div>
        </li>
      </ul>
      <p class="tiers__note">Students and teachers get half off. If the price is the only thing in the way, write to us — we would rather you meditate.</p>
    </div>
  </section>

  <section id="gallery" data-section="gallery" class="gallery" data-kind="gallery">
    <div class="wrap">
      <h2 class="h2 gallery__title" data-lines>Inside the app</h2>
      <div class="collage" data-fixed="6">
        <figure class="shot shot--a" data-speed="-.5"><div class="shot__img">
          <div class="art layered" role="img" aria-label="The morning check-in screen on a phone, against a lake at dawn">
            <canvas class="scene" data-scene="dawn"></canvas>
            <div class="phone" data-screen="checkin" data-scene="fog" aria-hidden="true"></div>
          </div>
        </div><figcaption><b>01</b>The morning check-in</figcaption></figure>
        <figure class="shot shot--b" data-speed=".6"><div class="shot__img">
          <div class="art macro" role="img" aria-label="Close-up of the glowing breathing orb">
            <span class="ripple"></span><span class="ripple r2"></span><span class="orb"></span>
          </div>
        </div><figcaption><b>02</b>The breathing orb, up close</figcaption></figure>
        <figure class="shot shot--c" data-speed="-.2"><div class="shot__img">
          <div class="art layered" role="img" aria-label="A sleep story playing on a phone under the northern lights">
            <canvas class="scene" data-scene="aurora"></canvas>
            <div class="phone" data-screen="sleep" data-scene="desert" aria-hidden="true"></div>
          </div>
        </div><figcaption><b>03</b>Sleep story, 22:40</figcaption></figure>
        <figure class="shot shot--d" data-speed=".3"><div class="shot__img">
          <div class="art studio" role="img" aria-label="Three phones showing the check-in, breathing and weekly insight screens">
            <div class="phone" data-screen="checkin" data-scene="fog" aria-hidden="true"></div>
            <div class="phone" data-screen="breathe" data-scene="dawn" aria-hidden="true"></div>
            <div class="phone" data-screen="insights" data-scene="ocean" aria-hidden="true"></div>
          </div>
        </div><figcaption><b>04</b>Check-in, session and the weekly letter</figcaption></figure>
        <figure class="shot shot--e" data-speed="-.7"><div class="shot__img">
          <div class="art layered" role="img" aria-label="A focus timer floating over a rainy forest">
            <canvas class="scene" data-scene="forest"></canvas>
            <div class="focus-card"><svg viewBox="0 0 120 120" aria-hidden="true"><circle cx="60" cy="60" r="52" fill="none" stroke="rgba(255,255,255,.22)" stroke-width="5"/><circle cx="60" cy="60" r="52" fill="none" stroke="#ee8903" stroke-width="5" stroke-linecap="round" pathLength="100" stroke-dasharray="84 100" transform="rotate(-90 60 60)"/><text x="60" y="68" text-anchor="middle" fill="#fff" font-size="24" font-weight="200" font-family="Reddit Sans, sans-serif">42:18</text></svg>Focus · Forest rain</div>
          </div>
        </div><figcaption><b>05</b>A focus block in the rain</figcaption></figure>
        <figure class="shot shot--f" data-speed=".8"><div class="shot__img">
          <div class="art candle-scene" role="img" aria-label="A lit candle in a dark room">
            <div class="candle"><div class="candle__glow"></div><div class="candle__wax"></div><div class="candle__wick"></div><div class="candle__flame"><i></i></div></div>
            <div class="candle__table"></div>
          </div>
        </div><figcaption><b>06</b>Night mode, for the last light of the day</figcaption></figure>
      </div>
    </div>
  </section>

  <section id="voices" data-section="reviews" class="voices dark" data-kind="reviews">
    <div class="wrap voices__head"><h2 class="h2" data-lines>What people noticed</h2></div>
    <div class="voices__row">
      <ul class="voices__track">
        <li class="quote q-paper">
          <blockquote><p>“I've tried every meditation app. This is the first one that noticed I was rushing and slowed down with me.”</p></blockquote>
          <div class="quote__who"><span class="gem" style="--h:28" aria-hidden="true">MS</span><span><span class="quote__name">Marta Silva</span>Nurse, Lisbon</span></div>
        </li>
        <li class="quote q-line">
          <blockquote><p>“The sleep stories actually stop when I fall asleep. I didn't know I needed that.”</p></blockquote>
          <div class="quote__who"><span class="gem" style="--h:190" aria-hidden="true">DO</span><span><span class="quote__name">Daniel Osei</span>Night-shift engineer, Accra</span></div>
        </li>
        <li class="quote q-sun">
          <blockquote><p>“Three minutes before every pitch. My hands stopped shaking somewhere around week two.”</p></blockquote>
          <div class="quote__who"><span class="gem" style="--h:12" aria-hidden="true">PN</span><span><span class="quote__name">Priya Nair</span>Product designer, Porto</span></div>
        </li>
        <li class="quote q-line">
          <blockquote><p>“My whole family uses it, and nobody can read anyone else's journal. That's what sold me.”</p></blockquote>
          <div class="quote__who"><span class="gem" style="--h:150" aria-hidden="true">LM</span><span><span class="quote__name">Luca Moretti</span>Father of three, Milan</span></div>
        </li>
        <li class="quote q-paper">
          <blockquote><p>“It feels less like an app and more like someone sitting quietly next to you.”</p></blockquote>
          <div class="quote__who"><span class="gem" style="--h:42" aria-hidden="true">HW</span><span><span class="quote__name">Hannah Weiss</span>Photographer, Vienna</span></div>
        </li>
      </ul>
    </div>
  </section>

  <section id="opencall" data-section="trial" class="opencall" data-kind="trial">
    <div class="opencall__stage">
      <div class="opencall__disc" aria-hidden="true"></div>
      <svg class="opencall__ring" viewBox="0 0 100 100" aria-hidden="true"><circle cx="50" cy="50" r="49.5" pathLength="100" stroke-dasharray="40 60"/></svg>
      <h2 class="opencall__title">Your first breath is on us</h2>
    </div>
    <div class="wrap opencall__foot">
      <p class="lead" data-reveal>Fourteen days, every feature, no card needed. If it doesn't help, delete it — and we delete everything with it.</p>
      <div class="opencall__actions" data-reveal><a class="btn" href="#tickets">Start free trial</a><a class="link" href="#faq">How we use AI</a></div>
    </div>
  </section>

  <section id="faq" data-section="faq" class="faq" data-kind="faq">
    <div class="wrap faq__grid">
      <h2 class="h2 faq__title" data-lines>Before you ask</h2>
      <div class="faq__list">
        <details class="qa">
          <summary><span class="qa__q">Is my breathing recorded?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>No. The microphone signal is analysed on your phone in real time and thrown away. Only your breaths per minute are kept, and only if you allow it.</p></div>
        </details>
        <details class="qa">
          <summary><span class="qa__q">How does the AI build a session?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>Our teachers wrote thousands of short passages of guidance. Ochre's model arranges and paces them around what you tell it and how you're breathing, then reads them in a voice you choose.</p></div>
        </details>
        <details class="qa">
          <summary><span class="qa__q">Is this a replacement for therapy?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>No. Ochre is a meditation companion, not a medical device. If you're having a hard time, it will point you to people who can help.</p></div>
        </details>
        <details class="qa">
          <summary><span class="qa__q">Does it work offline?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>Yes. Download any session or soundscape. With no signal, adaptive sessions run on a smaller model that lives on your phone.</p></div>
        </details>
        <details class="qa">
          <summary><span class="qa__q">Can I cancel any time?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>Yes, in two taps from settings. Annual plans are refundable within thirty days, no questions asked.</p></div>
        </details>
        <details class="qa">
          <summary><span class="qa__q">Is it suitable for children?</span><span class="ibtn qa__icon" aria-hidden="true"><svg viewBox="0 0 18 18"><path d="M9 2v14M2 9h14" fill="none" stroke="currentColor" stroke-width="1.4"/></svg></span></summary>
          <div class="qa__a"><p>The family plan includes a kids' mode for ages 6–12, with shorter sessions, bedtime stories and no journal or microphone features.</p></div>
        </details>
      </div>
    </div>
  </section>

  <section id="contact" data-section="contact" class="contact" data-kind="contact">
    <div class="contact__main">
      <h2 class="h2" data-lines>Talk to a person</h2>
      <dl class="contact__list">
        <div><dt>Support</dt><dd><a class="link" href="mailto:hello@ochre.example">hello@ochre.example</a></dd></div>
        <div><dt>Press</dt><dd><a class="link" href="mailto:press@ochre.example">press@ochre.example</a></dd></div>
        <div><dt>Studio</dt><dd>Rua das Flores 28<br>4050-262 Porto, Portugal</dd></div>
        <div><dt>Replies</dt><dd>Within one working day, written by a human</dd></div>
      </dl>
    </div>
    <div class="contact__side">
      <form class="signup" data-sent="Thank you — your first practice arrives on Sunday." novalidate>
        <h3 class="h3">A breath in your inbox</h3>
        <p>One short practice a week, written by our teachers. No streaks, no guilt.</p>
        <div class="signup__row">
          <label class="signup__field"><span class="sr-only">Email address</span><input type="email" name="email" placeholder="Your email" autocomplete="email" required></label>
          <button class="btn" type="submit">Subscribe</button>
        </div>
        <p class="signup__status" role="status" aria-live="polite"></p>
      </form>
      <div class="contact__scene" aria-hidden="true">
        <div class="contact__sun"></div>
        <div class="contact__pillars"><i class="pillar pl-d"></i><i class="pillar pl-c"></i><i class="pillar pl-f"></i><i class="pillar pl-e"></i><i class="pillar pl-b"></i><i class="pillar pl-g"></i></div>
      </div>
    </div>
  </section>
</main>

<footer class="site-foot" data-section="footer">
  <div class="foot__rule"></div>
  <div class="foot__cols">
    <p>Ochre — meditation that listens<br>Made in Porto and San Francisco</p>
    <p>© 2026 Ochre · a fictional brand; every figure is illustrative</p>
    <div class="foot__links"><a class="link" href="#faq">Privacy</a><a class="link" href="#faq">Terms</a></div>
    <div class="foot__links"><a class="link" href="#contact">Careers</a><a class="link" href="#contact">Instagram</a></div>
  </div>
  <p class="foot__mark" aria-hidden="true"><span class="wm" style="--len:5">OCHRE</span></p>
</footer>

<!-- Procedural scene renderer: phones, landscapes, water, skies -->
<script>(()=>{
const reduce=window.matchMedia&&matchMedia('(prefers-reduced-motion: reduce)').matches;
/* ---- phone mockups ---- */
const ST='<div class="ui-status"><b>9:41</b><span class="ui-ic"><span class="ui-sig"><i></i><i></i><i></i><i></i></span><span class="ui-bat"></span></span></div>';
const wave=Array.from({length:26},(_,i)=>`<i style="--r:${(.12+.88*Math.abs(Math.sin(i*1.7)*Math.cos(i*.55))).toFixed(2)}"></i>`).join('');
const SCREENS={
breathe:`${ST}<p class="ui-eyebrow">Evening wind-down</p><p class="ui-title">Breathe with me</p><div class="ui-orbwrap"><div class="orb"></div></div><p class="ui-cue"><span>Breathe in</span><span>Hold</span><span>Breathe out</span></p><div class="ui-progress"><i></i></div><div class="ui-row"><span>04:12</span><span class="ui-btn"><svg viewBox="0 0 24 24"><path d="M8 6v12M16 6v12" stroke="currentColor" stroke-width="2.6" stroke-linecap="round"/></svg></span><span>10:00</span></div>`,
sleep:`${ST}<p class="ui-eyebrow">Sleep story</p><p class="ui-clock">22:40</p><p class="ui-sub">Desert night · fades as you drift off</p><div class="ui-fill"></div><div class="ui-glass"><div class="ui-wave">${wave}</div><p class="ui-small">Fading out in 18 min</p></div><div class="ui-chips"><span>Wake 06:30–07:00</span><span>Soft alarm</span></div>`,
checkin:`${ST}<p class="ui-eyebrow">Thursday · 07:02</p><p class="ui-title">Good morning, Ana</p><p class="ui-sub">How are you arriving?</p><div class="ui-moods"><span>Calm</span><span class="on">Tired</span><span>Restless</span><span>Bright</span><span>Heavy</span><span>Open</span></div><div class="ui-fill"></div><div class="ui-glass ui-card"><span class="ui-play"></span><span><small>Suggested for you</small>6-min wake-up breath</span></div>`,
insights:`${ST}<p class="ui-eyebrow">This week</p><p class="ui-title">54 minutes</p><div class="ui-bars">${[.4,.7,.3,.9,.6,1,.5].map((h,i)=>`<i style="--h:${h}"><b>${'MTWTFSS'[i]}</b></i>`).join('')}</div><div class="ui-stats"><div class="ui-glass"><small>Sleep</small>+38 min</div><div class="ui-glass"><small>Streak</small>6 days</div></div><div class="ui-fill"></div><div class="ui-glass ui-note">You slept better on the nights you did the wind-down.</div>`
};
document.querySelectorAll('.phone[data-screen]').forEach(p=>{p.innerHTML=`<div class="phone__body"><div class="phone__screen">${p.dataset.gl?`<canvas class="scene gl3d" data-fallback="${p.dataset.scene||'ocean'}"></canvas>`:`<canvas class="scene" data-scene="${p.dataset.scene||'ocean'}"></canvas>`}<div class="phone__ui">${SCREENS[p.dataset.screen]||''}</div><span class="phone__island"></span></div></div>`});

/* ---- maths ---- */
const rng=seed=>{let s=(seed>>>0)||1;return()=>(s=(s*1664525+1013904223)%4294967296)/4294967296};
const vnoise=seed=>{const r=rng(seed),v=new Float32Array(512);for(let i=0;i<512;i++)v[i]=r();return x=>{const i=Math.floor(x),f=x-i,t=f*f*(3-2*f),a=v[i&511],b=v[(i+1)&511];return a+(b-a)*t}};
const fbm=(n,x,o,ridged)=>{let s=0,a=1,f=1,t=0;for(let k=0;k<o;k++){let v=n(x*f+k*17.3);if(ridged)v=1-Math.abs(v*2-1);s+=a*v;t+=a;a*=.5;f*=2.1}return s/t};
const rgba=(c,a)=>`rgba(${c},${a})`;
const lin=(x,y0,y1,stops)=>{const g=x.createLinearGradient(0,y0,0,y1);stops.forEach(([o,c])=>g.addColorStop(o,c));return g};
const soft=(x,cx,cy,rx,ry,col,a)=>{if(rx<=0||ry<=0)return;x.save();x.translate(cx,cy);x.scale(1,ry/rx);const g=x.createRadialGradient(0,0,0,0,0,rx);g.addColorStop(0,rgba(col,a));g.addColorStop(.45,rgba(col,a*.55));g.addColorStop(1,rgba(col,0));x.fillStyle=g;x.fillRect(-rx,-rx,rx*2,rx*2);x.restore()};
let G=null;const grain=()=>{if(G)return G;G=document.createElement('canvas');G.width=G.height=128;const g=G.getContext('2d'),d=g.createImageData(128,128);for(let i=0;i<d.data.length;i+=4){const v=Math.random()*255;d.data[i]=d.data[i+1]=d.data[i+2]=v;d.data[i+3]=255}g.putImageData(d,0,0);return G};

/* ---- scene presets (colours as "r,g,b") ---- */
const P={
dawn:{seed:3,horizon:.6,sky:[[0,'#212c45'],[.32,'#5d6283'],[.62,'#c99a93'],[.84,'#f4bf90'],[1,'#ffe1ae']],
 sun:{x:.66,y:.47,r:.028,core:'#fffaf0',edge:'#ffdca6',halo:'255,196,135'},
 clouds:[{y:.3,h:.16,n:16,shade:'110,96,128',lit:'255,186,160',a:.32}],
 ridges:[{y:.6,a:.24,f:1.8,o:5,ridged:1,top:'128,122,152',bot:'170,148,158',lit:'255,206,176',light:1,k:.9},{y:.6,a:.11,f:3,o:5,ridged:1,top:'84,82,108',bot:'112,98,114',lit:'255,190,150',light:1,k:.7,trees:{gap:4,h:.022}}],
 haze:'240,196,178',fog:[{y:.59,h:.03,col:'255,226,206',a:.55}],
 water:{top:'rgba(250,192,146,.16)',bot:'rgba(16,22,36,.8)'},
 fg:[{y:.95,a:.1,f:2.6,o:5,top:'18,24,32',bot:'7,9,13',trees:{gap:7,h:.2},hz:0}],vig:.38},
ocean:{seed:11,horizon:.56,sky:[[0,'#0f1a30'],[.36,'#352f55'],[.64,'#a95a72'],[.84,'#ee935a'],[1,'#ffc77a']],
 sun:{x:.5,y:.505,r:.036,core:'#fff4dc',edge:'#ffb35c',halo:'255,160,96'},
 clouds:[{y:.4,h:.22,n:20,shade:'64,46,78',lit:'255,148,108',a:.42},{y:.18,h:.1,n:8,shade:'40,34,66',lit:'200,110,120',a:.3}],
 ridges:[],water:{top:'rgba(240,140,92,.14)',bot:'rgba(8,13,26,.86)',rough:3},waves:1,vig:.42},
desert:{seed:5,horizon:.6,stars:8,milky:1,sky:[[0,'#02040b'],[.55,'#091227'],[.85,'#1b2846'],[1,'#36405f']],
 moon:{x:.74,y:.19,r:.05},
 ridges:[{y:.66,a:.12,f:2.2,o:2,dune:1,top:'44,46,70',bot:'34,36,56',lit:'120,124,156',light:1,k:3},{y:.82,a:.18,f:1.7,o:2,dune:1,top:'32,32,50',bot:'24,24,38',lit:'150,146,170',light:1,k:3},{y:1.02,a:.24,f:1.3,o:2,dune:1,top:'22,21,32',bot:'14,14,20',lit:'170,160,175',light:1,k:3,hz:0}],
 haze:'50,62,100',vig:.5},
forest:{seed:21,horizon:.72,sky:[[0,'#3f4b50'],[.6,'#879593'],[1,'#b7c1ba']],
 ridges:[{y:.48,a:.1,f:2,o:5,top:'126,140,137',bot:'140,153,149',trees:{gap:3,h:.05}},{y:.6,a:.1,f:2.5,o:5,top:'92,108,105',bot:'106,121,118',trees:{gap:4,h:.08}},{y:.76,a:.08,f:3,o:5,top:'56,70,68',bot:'70,83,80',trees:{gap:6,h:.14}},{y:1.02,a:.08,f:3,o:5,top:'22,30,29',bot:'13,19,19',trees:{gap:10,h:.42},hz:0}],
 haze:'186,198,192',fog:[{y:.52,h:.07,col:'205,214,208',a:.5},{y:.66,h:.07,col:'192,202,196',a:.45},{y:.82,h:.06,col:'170,182,176',a:.3}],rain:1,vig:.45},
aurora:{seed:8,horizon:.72,stars:7,sky:[[0,'#01040c'],[.6,'#06182a'],[1,'#123441']],aurora:1,
 ridges:[{y:.72,a:.2,f:1.8,o:5,ridged:1,top:'150,172,186',bot:'48,70,86',lit:'190,255,225',light:-1,k:.9,snow:1}],
 fg:[{y:.97,a:.07,f:1.5,o:3,top:'196,212,222',bot:'120,142,158',lit:'210,255,236',light:-1,k:2,hz:0}],haze:'40,92,96',snow:1,vig:.5},
fog:{seed:14,horizon:.66,sky:[[0,'#7b8fa0'],[.5,'#d6c0a4'],[.85,'#f4d4a8'],[1,'#fbe4bd']],
 sun:{x:.32,y:.4,r:.03,core:'#fffdf4',edge:'#ffe6b6',halo:'255,225,172'},
 ridges:[{y:.5,a:.1,f:1.6,o:5,top:'166,162,166',bot:'184,174,166'},{y:.6,a:.1,f:2,o:5,top:'140,138,141',bot:'160,151,144',trees:{gap:5,h:.03}},{y:.72,a:.1,f:2.4,o:5,top:'106,106,106',bot:'125,118,111',trees:{gap:5,h:.045}},{y:.87,a:.1,f:2.8,o:5,top:'62,64,62',bot:'74,71,65',trees:{gap:7,h:.08}},{y:1.04,a:.1,f:3,o:5,top:'27,29,28',bot:'17,17,17',trees:{gap:10,h:.26},hz:0}],
 haze:'246,226,202',fog:[{y:.53,h:.05,col:'252,236,216',a:.7},{y:.64,h:.05,col:'246,229,206',a:.65},{y:.77,h:.05,col:'240,222,200',a:.55}],vig:.3},
night:{seed:4,horizon:.62,stars:6,sky:[[0,'#020611'],[.6,'#0b1830'],[1,'#22324e']],moon:{x:.72,y:.28,r:.06},
 ridges:[{y:.62,a:.07,f:2,o:6,top:'12,20,34',bot:'10,16,28'}],water:{top:'rgba(150,172,214,.07)',bot:'rgba(2,6,14,.86)'},vig:.5}
};

/* ---- painters ---- */
function stars(x,W,hz,R,dens){const n=Math.round(W*hz/1000*dens);for(let i=0;i<n;i++){const sx=R()*W,sy=Math.pow(R(),1.25)*hz,b=R(),r=b>.985?1.4:b>.9?.9:.5;x.globalAlpha=(.25+R()*.75)*(1-sy/hz*.7);x.fillStyle=R()<.15?'#ffe7c4':R()<.25?'#cfe0ff':'#fff';x.beginPath();x.arc(sx,sy,r,0,6.3);x.fill();if(r>1){x.globalAlpha=1;soft(x,sx,sy,r*5,r*5,'210,225,255',.25)}}x.globalAlpha=1}
function milky(x,W,hz,R){x.save();x.translate(W*.42,hz*.42);x.rotate(-.62);const L=Math.hypot(W,hz);x.globalCompositeOperation='lighter';for(let i=0;i<46;i++)soft(x,(R()-.5)*L,(R()-.5)*hz*.12,L*.07*(.5+R()),hz*.06*(.5+R()),'140,152,200',.06);for(let i=0;i<1600*W/800;i++){const u=(R()-.5)*L,v=(R()+R()+R()-1.5)*hz*.09;x.fillStyle=`rgba(255,255,255,${R()*.45})`;x.fillRect(u,v,.7,.7)}x.restore()}
function aurora(x,W,hz,seed){x.save();x.globalCompositeOperation='lighter';[['80,255,170',.5,0],['60,200,255',.28,1],['170,255,120',.34,2]].forEach(([col,a,k])=>{const n=vnoise(seed*13+k*7);for(let px=0;px<W;px+=2){const v=fbm(n,px/W*1.6+k,4);const base=hz*(.3+v*.38+k*.04);const len=hz*(.16+fbm(n,px/W*7+50,3)*.38);const inten=a*Math.pow(fbm(n,px/W*3.2+90,4),1.6)*1.9;const g=x.createLinearGradient(0,base-len,0,base);g.addColorStop(0,rgba(col,0));g.addColorStop(.78,rgba(col,inten*.55));g.addColorStop(1,rgba(col,inten));x.fillStyle=g;x.fillRect(px,base-len,2,len);x.fillStyle=rgba(col,inten*.22);x.fillRect(px,base,2,hz*.035)}});x.restore()}
function sun(x,W,H,s){const cx=s.x*W,cy=s.y*H,r=s.r*Math.min(W,H);x.save();x.globalCompositeOperation='lighter';soft(x,cx,cy,r*20,r*20,s.halo,.26);soft(x,cx,cy,r*7,r*7,s.halo,.45);soft(x,cx,cy,r*2.6,r*2.6,'255,242,222',.6);soft(x,cx,cy,r*16,r*1.1,s.halo,.22);x.restore();const g=x.createRadialGradient(cx,cy,0,cx,cy,r);g.addColorStop(0,s.core);g.addColorStop(.62,s.core);g.addColorStop(.86,'rgba(255,240,215,.75)');g.addColorStop(1,'rgba(255,236,205,0)');x.fillStyle=g;x.beginPath();x.arc(cx,cy,r,0,7);x.fill()}
function moon(x,cx,cy,r,R){x.save();x.globalCompositeOperation='lighter';soft(x,cx,cy,r*10,r*10,'150,175,230',.16);soft(x,cx,cy,r*3.2,r*3.2,'220,232,255',.28);x.restore();const g=x.createRadialGradient(cx-r*.3,cy-r*.3,r*.1,cx,cy,r);g.addColorStop(0,'#fbf8f0');g.addColorStop(.72,'#e8e2d3');g.addColorStop(1,'#b9b19f');x.fillStyle=g;x.beginPath();x.arc(cx,cy,r,0,7);x.fill();x.save();x.beginPath();x.arc(cx,cy,r,0,7);x.clip();[[-.32,-.18,.36],[.18,-.36,.24],[.08,.14,.3],[-.26,.36,.2],[.42,.22,.18],[-.04,-.04,.14],[.3,-.05,.12]].forEach(([dx,dy,s])=>soft(x,cx+dx*r,cy+dy*r,s*r,s*r*.8,'120,114,104',.3));for(let i=0;i<40;i++){const a=R()*7,d=Math.sqrt(R())*r,s=r*.035*(1+R()*2);soft(x,cx+Math.cos(a)*d,cy+Math.sin(a)*d,s,s,'110,102,94',.12)}x.restore()}
function clouds(x,W,H,R,c){for(let i=0;i<c.n;i++){const cx=R()*W*1.2-W*.1,cy=H*c.y+(R()-.5)*H*c.h,rx=W*(.08+R()*.2),ry=rx*(.06+R()*.08);soft(x,cx,cy,rx,ry,c.shade,c.a);soft(x,cx+rx*.08,cy+ry*.4,rx*.8,ry*.55,c.lit,c.a*.9)}}
function fogBand(x,W,H,R,f){for(let i=0;i<28;i++)soft(x,R()*W,H*f.y+(R()-.5)*H*f.h,W*(.12+R()*.22),H*f.h*(.35+R()*.4),f.col,f.a*(.4+R()*.6))}
function treePath(pa,R,ys,step,h,gap){for(let k=0;k<ys.length;k+=Math.max(1,Math.round(gap*(.5+R())))){const cx=-4+k*step,by=ys[k]+h*.1,th=h*(.45+R()*.8),w=th*(.2+R()*.08),t=7+(R()*4|0),pts=[];for(let j=1;j<=t;j++){const yy=by-th+th*j/t,ww=w*Math.pow(j/t,.9)*(.8+R()*.4);pts.push([ww,yy],[ww*.3,yy+th/t*.12])}pa.moveTo(cx,by-th);pts.forEach(q=>pa.lineTo(cx+q[0],q[1]));pa.lineTo(cx+w*.05,by+h*.3);pa.lineTo(cx-w*.05,by+h*.3);for(let j=pts.length-1;j>=0;j--)pa.lineTo(cx-pts[j][0]*(.85+R()*.3),pts[j][1]);pa.closePath()}}
function layers(x,W,H,R,p,L,off){L.forEach((l,i)=>{const n=vnoise(p.seed*31+i*7+off),base=H*l.y,amp=H*l.a,step=2,ys=[];for(let px=-4;px<=W+4;px+=step){let v=fbm(n,px/W*l.f,l.o||6,l.ridged);if(l.ridged)v=v*v*1.4;ys.push(base-v*amp)}
 const top=base-amp*(l.ridged?1.4:1),path=new Path2D();path.moveTo(-4,H+2);ys.forEach((y,k)=>path.lineTo(-4+k*step,y));path.lineTo(W+4,H+2);path.closePath();
 const fill=lin(x,top,Math.min(H,base+H*.15),[[0,`rgb(${l.top})`],[1,`rgb(${l.bot||l.top})`]]);x.fillStyle=fill;x.fill(path);
 if(l.lit){x.save();x.clip(path);const dir=l.light||1,k=l.k||.8,sl=ys.map((_,j)=>{const a=Math.max(0,j-1),b=Math.min(ys.length-1,j+1);return(ys[b]-ys[a])/((b-a)*step)}),win=l.dune?10:5,sm=sl.map((_,j)=>{let s=0,c=0;for(let q=-win;q<=win;q++){const v=sl[j+q];if(v!==undefined){const w=win+1-Math.abs(q);s+=v*w;c+=w}}return s/c});
  for(let j=0;j<ys.length;j++){const f=-sm[j]*dir,px=-4+j*step,y=ys[j],len=(base-y)*.95+amp*.25,col=f>0?l.lit:'0,0,0',a=f>0?Math.min(.5,f*k):Math.min(.32,-f*k*.6);if(a<.01)continue;const g=x.createLinearGradient(0,y,0,y+len);g.addColorStop(0,rgba(col,a));g.addColorStop(.55,rgba(col,a*.6));g.addColorStop(1,rgba(col,0));x.fillStyle=g;x.fillRect(px-.5,y,step+1,len)}
  if(l.snow){x.fillStyle=lin(x,top,top+amp*.9,[[0,'rgba(240,247,250,.75)'],[1,'rgba(240,247,250,0)']]);x.fillRect(0,top,W,amp)}
  x.fillStyle=lin(x,base-amp*.45,base+H*.04,[[0,`rgba(${l.bot||l.top},0)`],[1,`rgba(${l.bot||l.top},.9)`]]);x.fillRect(0,base-amp*.45,W,amp*.45+H*.05);
  if(l.dune){x.strokeStyle=rgba(l.lit,.22);x.lineWidth=1;x.beginPath();ys.forEach((y,k)=>k?x.lineTo(-4+k*step,y):x.moveTo(-4,y));x.stroke()}
  x.restore()}
 if(l.trees){const tp=new Path2D();treePath(tp,R,ys,step,H*l.trees.h,l.trees.gap);x.fillStyle=fill;x.fill(tp)}
 if(p.haze&&l.hz!==0){x.fillStyle=lin(x,base-amp*.5,base+H*.03,[[0,rgba(p.haze,0)],[1,rgba(p.haze,l.hz||.35)]]);x.fillRect(0,base-amp*.5,W,amp*.5+H*.03)}
 if(p.fog){const nextY=L[i+1]?L[i+1].y:9;p.fog.forEach(f=>{if(f.y+.02>=l.y&&f.y+.02<nextY&&!f.done){fogBand(x,W,H,R,f)}})}
})}
function waterFx(c,x,W,H,hz,dpr,R,p){const cw=c.width,ch=c.height,h0=Math.round(hz*dpr);x.save();x.setTransform(1,0,0,1,0,0);for(let y=h0;y<ch;y+=2){const d=y-h0,sy=Math.max(0,h0-d-2),t=d/Math.max(1,ch-h0),rf=p.water.rough||1,amp=(.5*rf+t*t*14*rf)*dpr,o=Math.sin(d*.11/dpr+Math.sin(d*.031/dpr)*2.5)*amp+(R()-.5)*amp*(rf>1?1.6:.6);x.drawImage(c,0,sy,cw,2,o-8*dpr,y,cw+16*dpr,2)}x.restore();
 x.fillStyle=lin(x,hz,H,[[0,p.water.top],[1,p.water.bot]]);x.fillRect(0,hz,W,H-hz);x.fillStyle='rgba(255,240,222,.12)';x.fillRect(0,hz,W,1)}
function waves(x,W,H,hz,R){for(let i=0;i<Math.round(W*.6);i++){const t=R(),y=hz+(H-hz)*t*t,len=W*(.01+R()*.08)*(.3+t*1.5),xx=R()*W-len/2,th=.4+t*t*3;x.fillStyle=R()<.6?`rgba(4,8,20,${.1+t*.25})`:`rgba(255,214,180,${.03+t*.06})`;x.fillRect(xx,y,len,th)}}
function glitter(x,cx,hz,W,H,R,col,n){x.save();x.globalCompositeOperation='lighter';for(let i=0;i<n;i++){const t=Math.pow(R(),1.4),y=hz+2+(H-hz)*t,spread=W*(.012+t*.11),gx=cx+(R()-.5)*2*spread*Math.sqrt(R()),len=2+t*W*.03*R();x.fillStyle=rgba(col,(.15+R()*.6)*(1-t*.45));x.fillRect(gx-len/2,y,len,.6+t*1.8)}x.restore()}

function paint(c,p){const W=c.clientWidth,H=c.clientHeight;if(W<2||H<2)return false;const dpr=Math.min(2,window.devicePixelRatio||1);c.width=Math.round(W*dpr);c.height=Math.round(H*dpr);const x=c.getContext('2d');x.setTransform(dpr,0,0,dpr,0,0);const R=rng(p.seed*977+13),hz=H*p.horizon;
 x.fillStyle=lin(x,0,hz,p.sky);x.fillRect(0,0,W,Math.ceil(hz)+1);x.fillStyle=p.sky[p.sky.length-1][1];x.fillRect(0,hz,W,H-hz);
 if(p.milky)milky(x,W,hz,R);if(p.stars)stars(x,W,hz,R,p.stars);if(p.aurora)aurora(x,W,hz,p.seed);if(p.sun)sun(x,W,H,p.sun);if(p.moon)moon(x,p.moon.x*W,p.moon.y*H,p.moon.r*Math.min(W,H),R);if(p.clouds)p.clouds.forEach(cl=>clouds(x,W,H,R,cl));
 layers(x,W,H,R,p,p.ridges||[],0);
 if(p.water){waterFx(c,x,W,H,hz,dpr,R,p);if(p.waves)waves(x,W,H,hz,R);const l=p.sun||p.moon;if(l)glitter(x,l.x*W,hz,W,H,R,p.sun?p.sun.halo:'214,224,244',Math.round((p.sun?1.1:.7)*W))}
 if(p.fg)layers(x,W,H,R,p,p.fg,500);
 const v=x.createRadialGradient(W/2,H*.48,Math.min(W,H)*.25,W/2,H/2,Math.hypot(W,H)*.62);v.addColorStop(0,'rgba(0,0,0,0)');v.addColorStop(1,`rgba(0,0,0,${p.vig||.35})`);x.fillStyle=v;x.fillRect(0,0,W,H);
 x.save();x.globalAlpha=.07;x.globalCompositeOperation='overlay';x.fillStyle=x.createPattern(grain(),'repeat');x.fillRect(0,0,W,H);x.restore();return true}

/* ---- weather particles ---- */
const live=new Set();let raf=0,last=0;
function initFx(c,p){const W=c.clientWidth,H=c.clientHeight,n=p.rain?Math.round(W*H/1700):Math.round(W*H/2400);c._fx=Array.from({length:n},()=>({x:Math.random()*W,y:Math.random()*H,z:Math.random()}));c._type=p.rain?'rain':'snow';const b=document.createElement('canvas');b.width=c.width;b.height=c.height;b.getContext('2d').drawImage(c,0,0);c._base=b}
function frame(c,dt){const x=c.getContext('2d'),W=c.clientWidth,H=c.clientHeight,dpr=c.width/W,s=dt/16.7;x.setTransform(1,0,0,1,0,0);x.drawImage(c._base,0,0);x.setTransform(dpr,0,0,dpr,0,0);
 if(c._type==='rain'){x.strokeStyle='rgba(226,234,236,.26)';x.lineWidth=1;x.beginPath();for(const d of c._fx){d.y+=(10+d.z*14)*s;d.x+=(1.6+d.z*2.4)*s;if(d.y>H+20){d.y=-20;d.x=Math.random()*W}if(d.x>W)d.x-=W;const L=8+d.z*16;x.moveTo(d.x,d.y);x.lineTo(d.x-L*.16,d.y-L)}x.stroke()}
 else{x.fillStyle='#fff';for(const d of c._fx){d.y+=(.35+d.z*1.1)*s;d.x+=Math.sin((d.y+d.z*90)*.02)*.4*s;if(d.y>H+4){d.y=-4;d.x=Math.random()*W}x.globalAlpha=.35+d.z*.6;x.beginPath();x.arc(d.x,d.y,.5+d.z*1.7,0,6.3);x.fill()}x.globalAlpha=1}}
const loop=t=>{const dt=last?Math.min(50,t-last):16.7;last=t;live.forEach(c=>frame(c,dt));if(live.size)raf=requestAnimationFrame(loop);else{raf=0;last=0}};
const wake=()=>{if(!raf&&live.size)raf=requestAnimationFrame(loop)};

/* ---- real-time 3D ocean (WebGL ray-marched heightfield) ---- */
const seaFn=(name,N)=>`float ${name}(vec2 p){float t=uTime;float h=.32*sin(p.y*.16+t*.7+p.x*.05)+.12*sin(p.x*.21-t*.4);float a=.24,f=.62;vec2 d=normalize(vec2(.25,1.));
for(int i=0;i<${N};i++){float ph=dot(p,d)*f+t*(1.1+.32*float(i))+noise(p*f*.35+float(i)*7.)*2.2;float s=.5+.5*sin(ph);h+=a*(pow(s,2.3)*2.-.9);d=vec2(d.x*.77-d.y*.64,d.x*.64+d.y*.77);f*=1.9;a*=.46;}return h;}`;
const FRAG=`precision highp float;uniform vec2 uRes;uniform float uTime;uniform vec2 uLook;
const vec3 SUN=vec3(0.,.048,1.);
float hash(vec2 p){vec3 q=fract(vec3(p.xyx)*.1031);q+=dot(q,q.yzx+33.33);return fract((q.x+q.y)*q.z);}
float noise(vec2 p){vec2 i=floor(p),f=fract(p),u=f*f*(3.-2.*f);return mix(mix(hash(i),hash(i+vec2(1,0)),u.x),mix(hash(i+vec2(0,1)),hash(i+vec2(1,1)),u.x),u.y);}
float fbm(vec2 p){float s=0.,a=.5;for(int i=0;i<5;i++){s+=a*noise(p);p=mat2(1.6,1.2,-1.2,1.6)*p;a*=.5;}return s;}
${seaFn('seaLo',3)}
${seaFn('seaHi',6)}
float map(vec3 p){return p.y-seaLo(p.xz);}
float trace(vec3 ro,vec3 rd,out vec3 p){float tm=0.,tx=900.;float hx=map(ro+rd*tx);p=ro+rd*tx;if(hx>0.)return -1.;float hm=map(ro),tmid=0.;
for(int i=0;i<10;i++){tmid=mix(tm,tx,hm/(hm-hx));p=ro+rd*tmid;float hmid=map(p);if(hmid<0.){tx=tmid;hx=hmid;}else{tm=tmid;hm=hmid;}}return tmid;}
vec3 sky(vec3 rd,vec3 ro){vec3 sd=normalize(SUN);float y=max(rd.y,0.);
vec3 zen=vec3(.03,.03,.11),mid=vec3(.34,.13,.3),hor=vec3(1.,.5,.22);
vec3 c=mix(hor,mid,smoothstep(0.,.16,y));c=mix(c,zen,smoothstep(.1,.55,y));
float sdot=max(dot(rd,sd),0.);
c+=vec3(1.,.5,.22)*pow(sdot,5.)*.5+vec3(1.,.68,.38)*pow(sdot,48.)*.9;
if(rd.y>.004){float t=(70.-ro.y)/rd.y;vec2 cp=ro.xz+rd.xz*t;float n=fbm(cp*.011+vec2(uTime*.012,0.));float n2=fbm(cp*.03-vec2(0.,uTime*.02));
float dens=smoothstep(.52,.9,n*.75+n2*.35)*smoothstep(.0,.07,rd.y);float lit=pow(sdot,2.5);
vec3 cc=mix(vec3(.24,.12,.22),vec3(1.,.5,.34),.2+.8*lit);cc+=vec3(1.,.62,.32)*pow(sdot,18.)*.8;c=mix(c,cc,dens*.9);}
c+=vec3(1.,.92,.75)*smoothstep(.99935,.99975,sdot)*3.5;
return c;}
void main(){vec2 uv=(gl_FragCoord.xy-.5*uRes)/uRes.y*2.;float t=uTime;
vec3 ro=vec3(0.,2.05+sin(t*.55)*.09,t*1.5);
float yaw=uLook.x*.14,pitch=.12+uLook.y*.05,roll=sin(t*.42)*.014+uLook.x*.02;
vec3 rd=normalize(vec3(uv.x,uv.y+pitch,2.1));
rd.xy=mat2(cos(roll),-sin(roll),sin(roll),cos(roll))*rd.xy;
rd.xz=mat2(cos(yaw),-sin(yaw),sin(yaw),cos(yaw))*rd.xz;
vec3 sd=normalize(SUN),col,p;float d=trace(ro,rd,p);
if(d<0.){col=sky(rd,ro);
 float ang=atan(rd.x,rd.z);float hill=.032*pow(fbm(vec2(ang*7.+2.3,1.7)),2.6)*smoothstep(.05,.3,abs(ang-.02));
 if(rd.y<hill&&rd.y>-.01){vec3 isl=mix(vec3(.2,.1,.18),sky(normalize(vec3(rd.x,0.,rd.z)),ro),.55);col=mix(col,isl,smoothstep(hill,hill-.002,rd.y));}
}else{
 float e=.015+d*.0012;
 vec3 n=normalize(vec3(seaHi(p.xz-vec2(e,0.))-seaHi(p.xz+vec2(e,0.)),2.*e,seaHi(p.xz-vec2(0.,e))-seaHi(p.xz+vec2(0.,e))));
 n=normalize(mix(n,vec3(0.,1.,0.),smoothstep(0.,260.,d)));
 vec3 rf=reflect(rd,n);rf.y=abs(rf.y);
 float fr=.03+.97*pow(1.-max(dot(n,-rd),0.),5.);
 vec3 deep=vec3(.006,.02,.045);
 vec3 sss=vec3(.62,.24,.1)*pow(max(dot(rd,sd),0.),3.)*max(p.y+.25,0.)*.3;
 col=mix(deep+sss,sky(rf,p),fr);
 col+=vec3(1.,.78,.5)*pow(max(dot(rf,sd),0.),220.)*4.;
 col+=vec3(1.,.7,.45)*pow(max(dot(rf,sd),0.),18.)*.12;
 col=mix(col,sky(normalize(vec3(rd.x,.002,rd.z)),ro),1.-exp(-d*.0065));
}
col=1.-exp(-col*1.15);col=mix(col,col*col*(3.-2.*col),.45);
vec2 q=gl_FragCoord.xy/uRes;col*=.5+.5*pow(16.*q.x*q.y*(1.-q.x)*(1.-q.y),.18);
col+=(hash(gl_FragCoord.xy+fract(t)*91.)-.5)*(2./255.);
gl_FragColor=vec4(col,1.);}`;
function gl3d(c){let gl=null;try{gl=c.getContext('webgl',{antialias:false,alpha:false,powerPreference:'high-performance'})}catch(_){}if(!gl)return false;
 const sh=(type,src)=>{const s=gl.createShader(type);gl.shaderSource(s,src);gl.compileShader(s);if(!gl.getShaderParameter(s,gl.COMPILE_STATUS)){console.warn(gl.getShaderInfoLog(s));return null}return s};
 const vs=sh(gl.VERTEX_SHADER,'attribute vec2 a;void main(){gl_Position=vec4(a,0.,1.);}'),fs=sh(gl.FRAGMENT_SHADER,FRAG);if(!vs||!fs)return false;
 const pr=gl.createProgram();gl.attachShader(pr,vs);gl.attachShader(pr,fs);gl.linkProgram(pr);if(!gl.getProgramParameter(pr,gl.LINK_STATUS))return false;gl.useProgram(pr);
 const b=gl.createBuffer();gl.bindBuffer(gl.ARRAY_BUFFER,b);gl.bufferData(gl.ARRAY_BUFFER,new Float32Array([-1,-1,3,-1,-1,3]),gl.STATIC_DRAW);const loc=gl.getAttribLocation(pr,'a');gl.enableVertexAttribArray(loc);gl.vertexAttribPointer(loc,2,gl.FLOAT,false,0,0);
 const uRes=gl.getUniformLocation(pr,'uRes'),uTime=gl.getUniformLocation(pr,'uTime'),uLook=gl.getUniformLocation(pr,'uLook');
 const dpr=Math.min(1.75,window.devicePixelRatio||1),phone=c.closest('.phone--tilt'),t0=performance.now();
 let look=[0,0],target=[0,0],vis=true,raf=0,lost=false;
 const resize=()=>{const w=Math.max(1,Math.round(c.clientWidth*dpr)),h=Math.max(1,Math.round(c.clientHeight*dpr));if(c.width!==w||c.height!==h){c.width=w;c.height=h;gl.viewport(0,0,w,h)}};
 const draw=now=>{if(lost)return;resize();look[0]+=(target[0]-look[0])*.06;look[1]+=(target[1]-look[1])*.06;gl.uniform2f(uRes,c.width,c.height);gl.uniform1f(uTime,reduce?14:(now-t0)/1000+14);gl.uniform2f(uLook,look[0],look[1]);gl.drawArrays(gl.TRIANGLES,0,3);if(phone){phone.style.setProperty('--ry',(look[0]*9).toFixed(2)+'deg');phone.style.setProperty('--rx',(look[1]*6).toFixed(2)+'deg')}};
 const loop=now=>{if(!vis||document.hidden||lost){raf=0;return}draw(now);raf=requestAnimationFrame(loop)};
 const go=()=>{if(reduce){requestAnimationFrame(draw);return}if(!raf)raf=requestAnimationFrame(loop)};
 addEventListener('pointermove',e=>{target=[(e.clientX/innerWidth)*2-1,-((e.clientY/innerHeight)*2-1)];if(reduce)go()},{passive:true});
 document.addEventListener('visibilitychange',go);
 c.addEventListener('webglcontextlost',e=>{e.preventDefault();lost=true});
 c.addEventListener('webglcontextrestored',()=>{c.classList.remove('gl3d');c.dataset.scene=c.dataset.fallback;lost=true;render(c)});
 if(window.IntersectionObserver)new IntersectionObserver(es=>es.forEach(e=>{vis=e.isIntersecting;if(vis)go()})).observe(c);
 c.style.background='none';go();return true}
document.querySelectorAll('canvas.gl3d').forEach(c=>{if(!gl3d(c)){c.classList.remove('gl3d');c.dataset.scene=c.dataset.fallback}});

/* ---- lifecycle ---- */
function render(c){const p=P[c.dataset.scene];if(!p)return;if(!paint(c,p))return;c._done=true;c._w=c.clientWidth;c._h=c.clientHeight;c.style.background='none';if(p.rain||p.snow){initFx(c,p);if(reduce)frame(c,0)}}
const canvases=[...document.querySelectorAll('canvas.scene[data-scene]')];
const io=window.IntersectionObserver?new IntersectionObserver(es=>es.forEach(e=>{const c=e.target;if(e.isIntersecting){if(!c._done)render(c);if(c._fx&&!reduce){live.add(c);wake()}}else live.delete(c)}),{rootMargin:'300px 0px'}):null;
canvases.forEach(c=>io?io.observe(c):render(c));
let rt=0;const ro=window.ResizeObserver?new ResizeObserver(()=>{clearTimeout(rt);rt=setTimeout(()=>canvases.forEach(c=>{if(c._done&&(Math.abs(c.clientWidth-c._w)>3||Math.abs(c.clientHeight-c._h)>3)){const was=live.has(c);render(c);if(was&&c._fx){live.add(c);wake()}}}),160)}):null;
if(ro)canvases.forEach(c=>ro.observe(c));
})();</script>

<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js"></script>
<script>(()=>{const root=document.documentElement;const $$=(s,r=document)=>[...r.querySelectorAll(s)];const init=(sel,fn)=>$$(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});let lenis=null;
const bar=document.querySelector('.progress');if(bar){let pt=false;const p=()=>{const h=document.documentElement.scrollHeight-innerHeight;bar.style.transform='scaleX('+(h>0?Math.min(1,scrollY/h):0)+')';pt=false};addEventListener('scroll',()=>{if(!pt){pt=true;requestAnimationFrame(p)}},{passive:true});p()}
init('.site-head',head=>{const btn=head.querySelector('.menu-btn'),nav=head.querySelector('.nav');const setOpen=open=>{root.classList.toggle('menu-open',open);if(btn){btn.setAttribute('aria-expanded',String(open));const l=btn.dataset[open?'labelClose':'labelOpen'];if(l)btn.setAttribute('aria-label',l)}if(lenis)open?lenis.stop():lenis.start()};if(btn)btn.addEventListener('click',()=>setOpen(!root.classList.contains('menu-open')));if(nav)nav.addEventListener('click',e=>{if(e.target.closest('a'))setOpen(false)});addEventListener('keydown',e=>{if(e.key==='Escape'&&root.classList.contains('menu-open'))setOpen(false)});let last=scrollY,ticking=false;const update=()=>{const y=scrollY;head.classList.toggle('is-solid',y>12);if(y>last+2&&y>320&&!root.classList.contains('menu-open'))head.classList.add('is-hidden');if(y<last-2||y<320)head.classList.remove('is-hidden');last=y;ticking=false};addEventListener('scroll',()=>{if(!ticking){ticking=true;requestAnimationFrame(update)}},{passive:true});update()});
document.addEventListener('click',e=>{const a=e.target.closest('a[href^="#"]');if(!a)return;const id=a.getAttribute('href');if(id.length<2)return;let t=null;try{t=document.querySelector(id)}catch(_){return}if(!t)return;e.preventDefault();if(lenis)lenis.scrollTo(t,{duration:1.4});else t.scrollIntoView({behavior:root.classList.contains('motion')?'smooth':'auto'})});
init('.tiers',list=>{const tiers=[...list.querySelectorAll('.tier')];const num=t=>{const el=t.querySelector('[data-price]');if(!el)return NaN;const m=el.textContent.match(/\d[\d\s.,'’]*/);if(!m)return NaN;let s=m[0].replace(/[\s'’]/g,'').replace(/[.,]$/,'');const last=Math.max(s.lastIndexOf('.'),s.lastIndexOf(','));s=last>=0&&s.length-last-1!==3?s.slice(0,last).replace(/[.,]/g,'')+'.'+s.slice(last+1):s.replace(/[.,]/g,'');return parseFloat(s)};const vals=tiers.map(num),max=Math.max(0,...vals.filter(v=>v>0));tiers.forEach((t,i)=>t.style.setProperty('--h',max>0&&vals[i]>0?(vals[i]/max).toFixed(3):'0'))});
init('.opencall__stage',stage=>{const title=stage.querySelector('.opencall__title');if(!title)return;const size=()=>stage.style.setProperty('--R',Math.round(Math.max(title.offsetHeight/2+28,title.offsetWidth*.2))+'px');size();if(window.ResizeObserver)new ResizeObserver(size).observe(title)});
init('.signup',form=>{const status=form.querySelector('.signup__status'),input=form.querySelector('input[type="email"]');form.addEventListener('submit',e=>{e.preventDefault();if(input&&!input.checkValidity()){input.reportValidity();return}if(status)status.textContent=form.dataset.sent||'';form.reset()})});
const start=()=>{if(!root.classList.contains('motion')||!window.gsap||!window.ScrollTrigger)return;gsap.registerPlugin(ScrollTrigger);const hasSplit=!!window.SplitText;if(hasSplit)gsap.registerPlugin(SplitText);if(window.Lenis){lenis=new Lenis({lerp:.1});lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0)}const queue=[];const later=fn=>queue.push(fn);const sceneInit=(sel,fn)=>later(()=>init(sel,fn));const run=()=>{const fn=queue.shift();if(!fn)return;try{fn()}catch(e){console.error(e)}setTimeout(run,0)};const onEnter=(els,fn,margin)=>{if(!els.length)return;if(!window.IntersectionObserver){els.forEach(fn);return}const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){io.unobserve(e.target);fn(e.target)}}),{rootMargin:margin});els.forEach(el=>io.observe(el))};const groups=['[data-reveal]','[data-rule]','[data-rise]','[data-lines]'].map(sel=>$$(sel));const lowLine=innerHeight*.98;const[reveal,rules,rises,lines]=groups.map(g=>g.filter(el=>el.getBoundingClientRect().top>lowLine));gsap.set(reveal,{y:44,opacity:0});onEnter(reveal,el=>gsap.to(el,{y:0,opacity:1,duration:1.1,ease:'power3.out',clearProps:'transform'}),'0px 0px -10% 0px');gsap.set(rules,{scaleX:0});onEnter(rules,el=>gsap.to(el,{scaleX:1,duration:1.3,ease:'power3.inOut'}),'0px 0px -8% 0px');gsap.set(rises,{clipPath:'inset(100% 0% 0% 0%)'});onEnter(rises,el=>gsap.to(el,{clipPath:'inset(0% 0% 0% 0%)',duration:1.4,ease:'expo.out'}),'0px 0px -12% 0px');if(hasSplit){gsap.set(lines,{autoAlpha:0});onEnter(lines,el=>document.fonts.ready.then(()=>{try{SplitText.create(el,{type:'lines',mask:'lines',autoSplit:true,onSplit:self=>{gsap.set(el,{autoAlpha:1});return gsap.from(self.lines,{yPercent:108,duration:1.15,ease:'power4.out',stagger:.09})}})}catch(e){gsap.set(el,{autoAlpha:1});console.error(e)}}),'0px 0px -12% 0px')}
sceneInit('.hero',hero=>{const stage=hero.querySelector('.hero__stage');if(!stage)return;const q=s=>hero.querySelector(s),qa=s=>hero.querySelectorAll(s);const poster=q('.hero__poster'),sun=q('.hero__sun'),disc=q('.hero__disc'),orbit=q('.hero__orbit'),year=q('.hero__year'),fig=q('.hero__figure'),pillars=qa('.hero__pillars .pillar'),fade=qa('.hero__dates, .hero__intro');const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:hero,start:'top top',end:'bottom bottom',scrub:.7,invalidateOnRefresh:true}});tl.to(hero,{'--sweep':1,duration:1,ease:'power1.inOut'},0);if(sun&&poster)tl.to(sun,{y:()=>poster.offsetHeight*.84,duration:1,ease:'power1.in'},0);if(year)tl.to(year,{yPercent:-22,'--glow':1,duration:1},0);if(fig)tl.to(fig,{yPercent:-12,duration:1},0);if(pillars.length)tl.to(pillars,{yPercent:i=>8+i%3*7,duration:1,stagger:.02},0);if(fade.length)tl.to(fade,{opacity:0,y:-24,duration:.35},.45);const loops=[];if(orbit)loops.push(gsap.fromTo(orbit,{rotation:-14},{rotation:22,duration:7,ease:'sine.inOut',yoyo:true,repeat:-1,transformOrigin:'50% 50%'}));if(disc)loops.push(gsap.to(disc,{y:'1.6svh',duration:5.5,ease:'sine.inOut',yoyo:true,repeat:-1}));ScrollTrigger.create({trigger:hero,start:'top bottom',end:'bottom top',onToggle:s=>loops.forEach(l=>s.isActive?l.resume():l.pause())})});
sceneInit('[data-drift]',el=>{gsap.fromTo(el,{rotation:-30},{rotation:40,ease:'none',scrollTrigger:{trigger:el.parentElement,start:'top bottom',end:'bottom top',scrub:true}})});
if(hasSplit)sceneInit('[data-words]',el=>{document.fonts.ready.then(()=>{try{SplitText.create(el,{type:'words',autoSplit:true,onSplit:self=>gsap.fromTo(self.words,{opacity:.16},{opacity:1,ease:'none',stagger:.1,scrollTrigger:{trigger:el,start:'top 78%',end:'bottom 42%',scrub:true}})})}catch(e){console.error(e)}})});
sceneInit('.people',list=>{const mm=gsap.matchMedia();mm.add('(min-width: 761px)',()=>{const items=[...list.children];const lefts=[...new Set(items.map(el=>Math.round(el.offsetLeft)))].sort((a,b)=>a-b);items.forEach(el=>{const c=lefts.indexOf(Math.round(el.offsetLeft));const k=[0,1,.45][c%3];if(!k)return;gsap.fromTo(el,{y:90*k},{y:-90*k,ease:'none',scrollTrigger:{trigger:list,start:'top bottom',end:'bottom top',scrub:true}})})})});
sceneInit('.venue',sec=>{const stage=sec.querySelector('.venue__stage'),photo=sec.querySelector('.venue__photo');if(!stage||!photo)return;const q=s=>sec.querySelector(s);const img=photo.querySelector('.art'),tint=q('.venue__tint'),shade=q('.venue__shade'),moon=q('.venue__moon'),ring=q('.venue__ring'),title=q('.venue__title'),info=q('.venue__info');const r0=()=>(innerWidth<761?31:20)+'vmin';const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top top',end:'bottom bottom',scrub:.7,invalidateOnRefresh:true}});tl.fromTo(photo,{clipPath:()=>`circle(${r0()} at 50% 52%)`},{clipPath:'circle(75% at 50% 52%)',duration:.62,ease:'power2.inOut'},.16);if(img)tl.fromTo(img,{scale:1.4,transformOrigin:'50% 40%'},{scale:1,duration:.8},0);if(tint)tl.fromTo(tint,{opacity:1},{opacity:0,duration:.4,ease:'power1.inOut'},.3);if(moon)tl.fromTo(moon,{xPercent:42,opacity:1},{xPercent:170,opacity:0,duration:.34,ease:'power1.in'},0);if(ring)tl.fromTo(ring,{scale:1,opacity:1,rotation:-40},{scale:3.4,opacity:0,rotation:20,duration:.55},.08);if(shade)tl.fromTo(shade,{opacity:0},{opacity:1,duration:.35},.42);if(title)tl.fromTo(title,{y:0},{y:-30,duration:1},0);if(info)tl.fromTo(info,{y:50,opacity:0},{y:0,opacity:1,duration:.25},.7)});
sceneInit('.schedule',sec=>{const line=sec.querySelector('.schedule__line'),dot=sec.querySelector('.schedule__dot');const st={trigger:sec,start:'top 60%',end:'bottom 60%',scrub:.5};if(line)gsap.fromTo(line,{scaleY:0},{scaleY:1,ease:'none',scrollTrigger:st});if(dot)gsap.fromTo(dot,{y:0,opacity:1},{y:()=>sec.offsetHeight-18,opacity:1,ease:'none',scrollTrigger:{...st,invalidateOnRefresh:true}});sec.querySelectorAll('.day').forEach(day=>ScrollTrigger.create({trigger:day,start:'top 60%',end:'bottom 60%',toggleClass:'is-now'}))});
sceneInit('.tiers',list=>{const tiers=[...list.querySelectorAll('.tier')];if(!tiers.length)return;const mm=gsap.matchMedia();mm.add('(min-width: 761px)',()=>{gsap.fromTo(tiers,{yPercent:100},{yPercent:0,ease:'power2.out',stagger:.14,duration:.6,scrollTrigger:{trigger:list,start:'top 88%',end:'bottom 82%',scrub:.8}})});mm.add('(max-width: 760px)',()=>{tiers.forEach(t=>{const p=t.querySelector('.tier__pillar');if(!p)return;gsap.fromTo(p,{clipPath:'inset(0% 100% 0% 0%)'},{clipPath:'inset(0% 0% 0% 0%)',ease:'power2.out',scrollTrigger:{trigger:p,start:'top 94%',end:'top 62%',scrub:.6}})})})});
sceneInit('.collage',c=>{c.querySelectorAll('[data-speed]').forEach(el=>{const k=parseFloat(el.dataset.speed)||0;const amp=()=>(innerWidth<761?36:90)*k;gsap.fromTo(el,{y:()=>amp()},{y:()=>-amp(),ease:'none',scrollTrigger:{trigger:c,start:'top bottom',end:'bottom top',scrub:true,invalidateOnRefresh:true}})})});
sceneInit('.voices__track',track=>{const items=[...track.children];if(items.length<2)return;items.forEach(el=>{const c=el.cloneNode(true);c.setAttribute('aria-hidden','true');c.setAttribute('inert','');track.appendChild(c)});track.classList.add('is-loop');const loop=gsap.to(track,{xPercent:-50,ease:'none',repeat:-1,duration:items.length*9});const row=track.parentElement||track;let over=false,seen=false;const sync=()=>seen&&!over?loop.resume():loop.pause();row.addEventListener('mouseenter',()=>{over=true;sync()});row.addEventListener('mouseleave',()=>{over=false;sync()});row.addEventListener('focusin',()=>{over=true;sync()});row.addEventListener('focusout',()=>{over=false;sync()});ScrollTrigger.create({trigger:row,start:'top bottom',end:'bottom top',onToggle:s=>{seen=s.isActive;sync()}});sync()});
sceneInit('.opencall__stage',stage=>{const ring=stage.querySelector('.opencall__ring');const st={trigger:stage,start:'top 92%',end:'center 48%',scrub:.6};gsap.fromTo(stage,{'--k':.05},{'--k':1,ease:'none',scrollTrigger:st});if(ring)gsap.fromTo(ring,{rotation:-120,scale:.4,opacity:0},{rotation:30,scale:1,opacity:1,ease:'none',scrollTrigger:st})});
sceneInit('.contact__scene',scene=>{const sun=scene.querySelector('.contact__sun');if(!sun)return;gsap.fromTo(sun,{yPercent:75},{yPercent:-8,ease:'none',scrollTrigger:{trigger:scene,start:'top bottom',end:'bottom 85%',scrub:.6}})});
let begun=false;const begin=()=>{if(!begun){begun=true;setTimeout(run,0)}};if(document.readyState==='complete')begin();else{addEventListener('load',begin,{once:true});setTimeout(begin,2500)}};if(document.readyState==='loading')document.addEventListener('DOMContentLoaded',start);else start()})();</script>
</body>
</html>
```

