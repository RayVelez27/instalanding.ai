INSTALANDING.AI · Lumora AI Home Solar Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Lumora AI Home Solar Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/lumora-ai-home-solar-page

lumora-home-solar.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Lumora AI Home Solar Page
  slug     lumora-ai-home-solar-page
  prompt   https://instalanding.ai/p/lumora-ai-home-solar-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/lumora-ai-home-solar-page
  license  Fictional brand ("Lumora"); every installer, figure, rate and quote is invented (the page says so in a footnote).
           Replace names, numbers and copy before shipping. Every picture is SVG or CSS drawn in code; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --bg, --fg, --muted, --primary / --primary-strong (green),
            --forest, --leaf, --sun (amber), --chart-2; Inter, Inter Tight (--ff-head), Newsreader (--ff-serif), JetBrains Mono
  sections  nav, hero, partners, manifesto, product, solutions, results, how-it-works, about, faq, estimate,
            early-access, footer (each region carries data-section)
  scripts   one IIFE, no libraries: SVG art builders (hero sky, rays, clouds, mist, stars; dusk, night and forecast
            landscapes; a golden-hour rooftop), a CSS 3D villa and terrain built from boxes that re-colour for evening
            through registered @property colours, a morning / evening switch, an interactive energy dashboard
            (ranges, hover / keyboard chart, schedulable actions), a horizontal pinned Forecast-Store-Save track,
            a scroll-lit manifesto, a drawn timeline, count-ups, local-only forms and a draggable 3D solar array
  assets    no image files; one SVG sprite of icons and the logo at the top of <body>

  ADAPTING
  - Dashboard data lives in DATA (today, tomorrow, week); chips in `live`; captions in `caps`.
  - The hero is laid out on a 1780 x 884 stage and scaled by layoutHero(); under 900px it stacks.
  - prefers-reduced-motion: animations and transitions cut to near zero, SVG animations paused, no curtain.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Lumora — The AI that runs your home's solar and battery</title>
<meta name="description" content="Lumora forecasts your roof's sunshine and your home's usage, then decides when to charge, when to power the house and when to skip the grid. Lower bills, longer evenings on your own sun.">
<meta name="theme-color" content="#f4f5f1">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' rx='9' fill='%23145a27'/%3E%3Cpath d='M8 17a8 8 0 0 1 16 0z' fill='%23f4b23f'/%3E%3Crect x='8' y='20' width='16' height='2.4' rx='1.2' fill='%2357c76a'/%3E%3Crect x='11' y='24' width='10' height='2.4' rx='1.2' fill='%2357c76a'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300..700&family=Inter+Tight:wght@400..800&family=Newsreader:opsz,wght@6..72,400..600&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f4f5f1;--fg:#0e1a12;--muted:#5c6a61;--border:rgba(14,26,18,.1);--card:#fff;
  --primary:#1e8538;--primary-strong:#145a27;--forest:#0b1f14;--forest-fg:#dfeee2;
  --leaf:#57c76a;--leaf-soft:#e1f1e3;--sage:#b9ccba;--mist:#e8ebe4;--accent:#e3f2e5;--accent-fg:#1b6c31;
  --sun:#f4b23f;--sun-soft:#fdf0d6;--chart-2:#2b7aa0;--grid:#8a9bb0;
  --ff-sans:'Inter',system-ui,-apple-system,sans-serif;--ff-head:'Inter Tight','Inter',system-ui,sans-serif;--ff-serif:'Newsreader',Georgia,'Times New Roman',serif;--ff-mono:'JetBrains Mono',ui-monospace,monospace;
  --ease:cubic-bezier(.22,1,.36,1);
}
*,*::before,*::after{box-sizing:border-box}
html{-webkit-text-size-adjust:100%;scroll-behavior:smooth}
body{margin:0;background:var(--bg);color:var(--fg);font-family:var(--ff-sans);font-size:16px;line-height:1.5;-webkit-font-smoothing:antialiased;overflow-x:hidden}
body::after{content:"";position:fixed;inset:0;z-index:90;pointer-events:none;opacity:.045;mix-blend-mode:multiply;background-image:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>")}
svg{display:block}
a{color:inherit;text-decoration:none}
button,input,select,textarea{font:inherit;color:inherit}
button{background:none;border:0;cursor:pointer;padding:0}
h1,h2,h3,h4,p,figure,blockquote,dl,dd{margin:0}
ul,ol{list-style:none;margin:0;padding:0}
.sr-only{position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;clip:rect(0,0,0,0);white-space:nowrap;border:0}
:focus-visible{outline:2px solid var(--primary);outline-offset:3px}
.container{max-width:80rem;margin:0 auto;padding:0 16px}
@media(min-width:640px){.container{padding:0 24px}}
@media(min-width:1024px){.container{padding:0 32px}}
.ic{width:1em;height:1em;fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;flex-shrink:0}
.mono{font-family:var(--ff-mono)}.tabnum{font-variant-numeric:tabular-nums}

/* Reveal */
.js .reveal{opacity:0;transform:translateY(26px);transition:opacity 1s var(--ease),transform 1s var(--ease)}
.js .reveal.in{opacity:1;transform:none}
.split .w{display:inline-block;overflow:hidden;vertical-align:bottom;padding:.12em 0;margin:-.12em 0}
.split .w>span{display:inline-block}
.js .split .w>span{transform:translateY(115%);transition:transform 1.1s var(--ease);transition-delay:calc(var(--i) * 55ms)}
.js .split.in .w>span{transform:none}

/* Intro + progress */
.curtain{position:fixed;inset:0;z-index:95;background:var(--forest);display:flex;align-items:center;justify-content:center;pointer-events:none;transition:clip-path 1.1s var(--ease);clip-path:inset(0 0 0 0)}
.curtain.out{clip-path:inset(0 0 100% 0)}
.curtain-inner{display:flex;align-items:center;gap:12px;animation:curtainIn 1s var(--ease) both}
.curtain-inner span{font-family:var(--ff-head);font-size:2.25rem;font-weight:700;letter-spacing:-.04em;color:#fff}
.curtain-bar{position:absolute;left:0;bottom:0;height:2px;width:100%;background:linear-gradient(90deg,var(--sun),var(--leaf));transform-origin:left;animation:bar 1.2s var(--ease) both}
@keyframes curtainIn{from{opacity:0;transform:translateY(14px) scale(.96)}to{opacity:1;transform:none}}
@keyframes bar{from{transform:scaleX(0)}to{transform:scaleX(1)}}
.progress{position:fixed;inset:0 0 auto;z-index:60;height:2px;transform-origin:left;transform:scaleX(0);background:linear-gradient(90deg,var(--sun),var(--leaf),var(--primary))}

/* Header */
.site-header{position:fixed;inset:12px 12px auto;z-index:50;transition:transform .55s var(--ease)}
@media(min-width:640px){.site-header{inset:16px 24px auto}}
.site-header.hide{transform:translateY(-140%)}
.nav{max-width:80rem;margin:0 auto;display:flex;align-items:center;justify-content:space-between;gap:16px;border-radius:18px;padding:8px 8px 8px 16px;transition:background .4s,box-shadow .4s}
.site-header.scrolled .nav{background:rgba(255,255,255,.74);-webkit-backdrop-filter:blur(18px) saturate(1.5);backdrop-filter:blur(18px) saturate(1.5);box-shadow:0 0 0 1px rgba(0,0,0,.05),0 18px 40px -26px rgba(14,26,18,.45)}
.logo{display:inline-flex;align-items:center;gap:10px;border-radius:8px}
.logo svg{width:30px;height:30px}
.logo-word{font-family:var(--ff-head);font-size:1.35rem;font-weight:700;letter-spacing:-.035em;color:#0f1f15;transition:color .6s}
.nav-rule{display:none;height:1px;flex:1;background:rgba(20,90,39,.15);transition:background .6s}
.nav-links{display:none;align-items:center;gap:8px}
.nav-link{position:relative;padding:8px 12px;border-radius:999px;font-size:15px;color:var(--primary-strong);transition:color .6s}
.nav-link::after{content:"";position:absolute;left:12px;right:12px;bottom:4px;height:1px;background:currentColor;transform:scaleX(0);transform-origin:right;transition:transform .5s var(--ease)}
.nav-link:hover::after{transform:scaleX(1);transform-origin:left}
.nav-cta{display:flex;align-items:center;gap:8px}
.menu-btn{display:inline-flex;width:40px;height:40px;align-items:center;justify-content:center;border-radius:12px;font-size:20px;transition:background .3s,color .6s}
.menu-btn:hover{background:rgba(0,0,0,.05)}
body.hero-night .site-header:not(.scrolled) .nav-link,body.hero-night .site-header:not(.scrolled) .logo-word,body.hero-night .site-header:not(.scrolled) .menu-btn{color:#fff}
body.hero-night .site-header:not(.scrolled) .nav-rule{background:rgba(255,255,255,.18)}
.mobile-menu{margin-top:8px;border-radius:18px;background:#fff;padding:8px;box-shadow:0 0 0 1px rgba(0,0,0,.05),0 24px 48px -24px rgba(14,26,18,.45)}
.mobile-menu a.mm{display:flex;height:48px;align-items:center;justify-content:space-between;padding:0 16px;border-radius:12px;font-weight:500}
.mobile-menu a.mm:hover{background:var(--mist)}
.mobile-menu .btn{width:100%;margin-top:8px}
@media(min-width:768px){.nav-links{display:flex}.menu-btn,.mobile-menu{display:none!important}}
@media(min-width:1024px){.nav-links{gap:24px}.nav-rule{display:block}}

@media(min-width:900px){
  .site-header{inset:0 0 auto}
  .nav{max-width:none;margin:0;padding:22px 9.66vw 0;border-radius:0;transition:background .4s,box-shadow .4s,padding .5s var(--ease),margin .5s var(--ease),max-width .5s var(--ease),border-radius .5s}
  .site-header.scrolled .nav{max-width:80rem;margin:12px auto 0;padding:8px 8px 8px 18px;border-radius:20px}
  .site-header .logo svg{width:38px;height:38px}
  .site-header .logo-word{font-size:26px}
  .nav-links{margin-left:auto;gap:2vw}
  .nav-link{color:#1c2a21;font-size:16.5px}
  .nav-rule{display:block;flex:0 0 11.5vw;margin:0 2.7vw 0 3.2vw;background:rgba(28,42,33,.16)}
  .site-header .btn-head{height:52px;padding:0 26px;font-size:17px;gap:12px;background:linear-gradient(180deg,#17492d,#0d371f);box-shadow:0 14px 28px -14px rgba(13,55,31,.7)}
}
/* Buttons */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:8px;white-space:nowrap;border-radius:999px;font-weight:500;height:40px;padding:0 20px;font-size:14px;transition:background .3s,color .3s,transform .3s,box-shadow .3s}
.btn:active{transform:scale(.97)}
.btn .ic{transition:transform .3s var(--ease)}
.btn:hover .ic:last-child{transform:translateX(4px)}
.btn-primary{background:var(--primary-strong);color:#fff;box-shadow:0 10px 24px -12px rgba(30,133,56,.75),inset 0 1px 0 rgba(255,255,255,.14)}
.btn-primary:hover{background:var(--forest)}
.btn-green{background:linear-gradient(180deg,#23963f,#1b7a33);color:#fff;box-shadow:0 12px 26px -12px rgba(30,133,56,.8),inset 0 1px 0 rgba(255,255,255,.2)}
.btn-green:hover{background:linear-gradient(180deg,#1e8538,#145a27)}
.btn-glass{background:rgba(255,255,255,.1);color:#fff;box-shadow:inset 0 0 0 1px rgba(255,255,255,.2);-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px)}
.btn-glass:hover{background:rgba(255,255,255,.16)}
.btn-lg{height:48px;padding:0 24px;font-size:15px}
.hide-sm{display:none}
@media(min-width:640px){.hide-sm{display:inline-flex}}

/* Eyebrow + headings */
.eyebrow{display:inline-flex;align-items:center;gap:8px;border-radius:999px;padding:4px 12px;font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;background:#fff;color:rgba(14,26,18,.7);box-shadow:0 0 0 1px rgba(0,0,0,.05)}
.eyebrow::before{content:"";width:6px;height:6px;border-radius:50%;background:var(--sun);box-shadow:0 0 0 3px rgba(244,178,63,.2)}
.eyebrow.dark{background:rgba(255,255,255,.08);color:rgba(223,238,226,.85);box-shadow:0 0 0 1px rgba(255,255,255,.14)}
.h2{margin-top:20px;font-family:var(--ff-head);font-weight:700;font-size:2.15rem;line-height:1.05;letter-spacing:-.036em;text-wrap:balance}
.h2 em,.serif{font-family:var(--ff-serif);font-style:normal;font-weight:500;letter-spacing:-.03em}
@media(min-width:640px){.h2{font-size:3rem}}
.lede{margin-top:20px;font-size:1rem;line-height:1.65;color:var(--muted);text-wrap:pretty}
@media(min-width:640px){.lede{font-size:1.125rem}}
.section-head{max-width:48rem}
.section-head.center{margin:0 auto;text-align:center}
.section-head.center .lede{max-width:42rem;margin-left:auto;margin-right:auto}

/* ================= HERO ================= */
.hero{position:relative;height:175vh;height:175svh;background:#efdcc0}
.hero-sticky{position:sticky;top:0;height:100vh;height:100svh;overflow:hidden}
.hero-scene{position:absolute;inset:0;overflow:hidden;background:#f1dcbc}
.scene-svg{position:absolute;inset:0;width:100%;height:100%;transform-origin:62% 70%}
.night-only{opacity:0;transition:opacity 1.6s ease}
.is-night .night-only{opacity:1}
.day-only{transition:opacity 1.4s ease}
.is-night .day-only{opacity:0}
.night-tint{opacity:0;mix-blend-mode:multiply;transition:opacity 1.6s ease}
.is-night .night-tint{opacity:1}
.sun-move{transition:transform 1.9s var(--ease)}
.is-night .sun-move{transform:translateY(300px)}
.moon-move{transform:translateY(90px);transition:transform 1.9s var(--ease)}
.is-night .moon-move{transform:none}
.cloud{animation:drift 80s linear infinite alternate}
.cloud:nth-child(2n){animation-duration:110s;animation-direction:alternate-reverse}
@keyframes drift{from{transform:translateX(-60px)}to{transform:translateX(80px)}}
.tw{animation:twinkle 3.6s ease-in-out infinite}
@keyframes twinkle{0%,100%{opacity:.2}50%{opacity:1}}
.shoot{animation:shoot 9s ease-in 3s infinite;opacity:0}
@keyframes shoot{0%{transform:translate(0,0);opacity:0}2%{opacity:1}8%{transform:translate(520px,180px);opacity:0}100%{opacity:0;transform:translate(520px,180px)}}
.hero-wash{position:absolute;inset:0;pointer-events:none;transition:opacity 1.4s}
.hero-wash.d{background:linear-gradient(90deg,rgba(250,241,226,.8) 0%,rgba(250,241,226,.5) 26%,rgba(250,241,226,.1) 40%,rgba(250,241,226,0) 47%)}
.hero-wash.n{opacity:0;background:linear-gradient(90deg,rgba(5,10,20,.8) 0%,rgba(5,10,20,.5) 28%,rgba(5,10,20,0) 48%)}
.is-night .hero-wash.d{opacity:0}.is-night .hero-wash.n{opacity:1}
.scene-shade{position:absolute;inset:0;background:rgba(11,31,20,.58);opacity:0;pointer-events:none}
.hero-ui{position:absolute;inset:0;z-index:2}
.hero-stage{position:absolute;left:0;top:0;width:1780px;height:884px;transform-origin:0 0}
.hs-arc{position:absolute;left:0;top:0;pointer-events:none;overflow:visible}
.hs-text{position:absolute;left:172px;top:153px;width:780px}
.hs-pill{display:inline-flex;align-items:center;gap:12px;height:42px;padding:0 15px 0 5px;border-radius:999px;background:rgba(255,255,255,.6);box-shadow:inset 0 0 0 1px rgba(255,255,255,.9),0 12px 30px -18px rgba(90,55,10,.45);-webkit-backdrop-filter:blur(14px);backdrop-filter:blur(14px);font-size:15.5px;font-weight:450;color:#1c2a21;transition:background 1s,color 1s,box-shadow 1s,transform .3s}
.hs-pill:hover{transform:translateY(-1px)}
.hs-pill b{display:inline-flex;align-items:center;height:32px;padding:0 13px;border-radius:999px;background:linear-gradient(180deg,#17532f,#0f3f23);color:#fff;font-size:13px;font-weight:600;letter-spacing:.04em}
.hs-pill .ic{font-size:17px;margin-left:2px;stroke-width:2.2}
.hs-h1{margin-top:30px}
.hs-h1 .a{display:block;font-family:var(--ff-head);font-weight:800;font-size:97px;line-height:.98;letter-spacing:-.047em;color:#0f1f15;transition:color 1s}
.hs-h1 .b{display:block;margin-top:2px;font-family:var(--ff-serif);font-weight:500;font-size:99px;line-height:1.02;letter-spacing:-.035em;color:#1d4630;transition:color 1s}
.hs-p{margin-top:22px;max-width:540px;font-size:20px;line-height:1.5;color:#485048;transition:color 1s,opacity .4s,transform .4s}
.hs-btns{margin-top:34px;display:flex;gap:18px}
.hbtn{white-space:nowrap;display:inline-flex;align-items:center;justify-content:center;gap:14px;height:62px;border-radius:999px;font-size:18px;font-weight:500;letter-spacing:-.005em;transition:transform .3s var(--ease),background .3s,box-shadow .3s,color .8s,border-color .8s}
.hbtn.pri{width:252px;background:linear-gradient(180deg,#17492d,#0d371f);color:#fff;box-shadow:0 20px 36px -16px rgba(13,55,31,.75),inset 0 1px 0 rgba(255,255,255,.14)}
.hbtn.pri:hover{transform:translateY(-2px);box-shadow:0 26px 44px -16px rgba(13,55,31,.8),inset 0 1px 0 rgba(255,255,255,.14)}
.hbtn.sec{width:224px;color:#17231b;border:1.5px solid rgba(23,35,27,.3);background:rgba(255,255,255,.16);-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px)}
.hbtn.sec:hover{background:rgba(255,255,255,.4)}
.hbtn .ic{font-size:21px;transition:transform .3s var(--ease)}
.hbtn.pri:hover .ic{transform:translateX(4px)}
.hbtn .play{width:0;height:0;border-left:13px solid currentColor;border-top:8px solid transparent;border-bottom:8px solid transparent;margin-right:2px}
.hs-proof{margin-top:42px;display:flex;align-items:center;gap:22px}
.avs{display:flex}
.avs span{display:flex;width:48px;height:48px;align-items:center;justify-content:center;margin-left:-12px;border-radius:50%;border:3px solid #fbf2e3;font-size:14px;font-weight:600;color:#fff;box-shadow:0 8px 16px -8px rgba(0,0,0,.4);transition:border-color 1s}
.avs span:first-child{margin-left:0}
.proof-t{font-size:14.5px;color:#4a5148;transition:color 1s}
.stars{margin-top:6px;display:flex;align-items:center;gap:3px;color:#f2b01e}
.stars svg{width:17px;height:17px;fill:currentColor}
.stars b{margin-left:9px;font-size:14.5px;font-weight:500;color:#4a5148;transition:color 1s}
.is-night .hs-h1 .a{color:#fff}.is-night .hs-h1 .b{color:#bfe0c7}
.is-night .hs-p,.is-night .proof-t,.is-night .stars b{color:rgba(255,255,255,.8)}
.is-night .hs-pill{background:rgba(12,20,32,.5);color:#fff;box-shadow:inset 0 0 0 1px rgba(255,255,255,.16)}
.is-night .hbtn.sec{color:#fff;border-color:rgba(255,255,255,.4);background:rgba(255,255,255,.06)}
.is-night .avs span{border-color:#101a2a}
.hs-chip{position:absolute;border-radius:18px;background:linear-gradient(155deg,rgba(255,255,255,.74),rgba(255,255,255,.46));box-shadow:inset 0 0 0 1px rgba(255,255,255,.9),0 26px 50px -26px rgba(90,55,10,.5);-webkit-backdrop-filter:blur(18px) saturate(1.4);backdrop-filter:blur(18px) saturate(1.4);transition:background 1.2s,box-shadow 1.2s,opacity 1s;animation:bob 7s ease-in-out infinite}
@keyframes bob{50%{transform:translateY(-8px)}}
.hs-chip.solar{left:1043px;top:195px;width:256px;height:90px;display:flex;align-items:center;gap:14px;padding:0 17px}
.hs-chip.home{left:938px;top:413px;width:238px;height:88px;display:flex;align-items:center;gap:14px;padding:0 17px;animation-delay:-2.3s}
.hs-chip.batt{left:1475px;top:295px;width:232px;height:114px;padding:15px 18px 0;animation-delay:-4.6s}
.hs-chip.batt .row1{display:flex;align-items:center;gap:14px}
.hc-ic{display:flex;width:46px;height:46px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;color:#fff}
.hc-ic svg{width:25px;height:25px}
.hc-ic.sun{background:radial-gradient(circle at 35% 30%,#ffd84d,#f59f0b);box-shadow:0 0 26px rgba(250,180,30,.65)}
.hc-ic.home{background:linear-gradient(160deg,#4289d0,#225b9c);box-shadow:0 10px 20px -10px rgba(34,91,156,.8)}
.hc-ic.bat{background:linear-gradient(160deg,#3cab60,#1d7a3c);box-shadow:0 10px 20px -10px rgba(29,122,60,.8)}
.hc-l{display:block;white-space:nowrap;font-size:12.5px;font-weight:500;letter-spacing:.08em;color:#6b6f66;transition:color 1s}
.hc-v{display:block;margin-top:3px;font-family:var(--ff-head);font-size:22px;font-weight:600;letter-spacing:-.01em;color:#141d17;font-variant-numeric:tabular-nums;white-space:nowrap;transition:color 1s}
.hc-bars{margin-left:auto;display:flex;align-items:flex-end;gap:2.5px;height:44px;flex-shrink:0}
.hc-bars i{width:5px;border-radius:2px;background:linear-gradient(180deg,var(--c1),var(--c2));transform-origin:bottom;animation:barw 2.8s ease-in-out infinite;transition:height .8s var(--ease)}
@keyframes barw{50%{transform:scaleY(.8)}}
.hs-chip.batt .hc-bars{margin:13px 0 0;width:100%;height:34px}
.hs-chip.batt .hc-bars i{flex:1}
.is-night .hs-chip{background:linear-gradient(155deg,rgba(18,28,44,.68),rgba(18,28,44,.46));box-shadow:inset 0 0 0 1px rgba(255,255,255,.14),0 26px 50px -26px rgba(0,0,0,.7)}
.is-night .hc-l{color:rgba(255,255,255,.6)}.is-night .hc-v{color:#fff}
.is-night .hs-chip.solar{opacity:.7}
.hs-tod{position:absolute;left:968px;top:648px;width:540px;height:76px;display:grid;grid-template-columns:1fr 1fr;padding:5px;border-radius:999px;background:linear-gradient(180deg,rgba(255,255,255,.5),rgba(255,255,255,.28));box-shadow:inset 0 0 0 1px rgba(255,255,255,.75),inset 0 1px 0 rgba(255,255,255,.9),0 24px 50px -24px rgba(90,55,10,.5);-webkit-backdrop-filter:blur(22px) saturate(1.5);backdrop-filter:blur(22px) saturate(1.5);transition:background 1.2s,box-shadow 1.2s}
.tod-ind{position:absolute;top:5px;bottom:5px;left:5px;width:calc(50% - 5px);border-radius:999px;overflow:hidden;background:linear-gradient(135deg,#fffaf0,#ffeec8 55%,#ffe0a0);box-shadow:inset 0 1px 0 #fff,inset 0 0 0 1px rgba(255,214,140,.7),0 10px 26px -10px rgba(214,150,30,.7),0 0 34px -8px rgba(255,200,90,.6);transition:transform .75s var(--ease),background .9s,box-shadow .9s}
.tod-ind i{position:absolute;inset:0;background:linear-gradient(110deg,transparent 35%,rgba(255,255,255,.65) 50%,transparent 65%);transform:translateX(-120%);animation:indSheen 5.5s ease-in-out infinite}
@keyframes indSheen{0%,60%{transform:translateX(-120%)}85%,100%{transform:translateX(120%)}}
.is-night .tod-ind{transform:translateX(100%);background:linear-gradient(135deg,#2f8a55,#1d6a3f 60%,#165633);box-shadow:inset 0 1px 0 rgba(255,255,255,.22),inset 0 0 0 1px rgba(140,230,170,.35),0 10px 26px -10px rgba(10,60,30,.8),0 0 34px -8px rgba(90,210,130,.45)}
.is-night .tod-ind i{background:linear-gradient(110deg,transparent 35%,rgba(255,255,255,.18) 50%,transparent 65%)}
.is-night .hs-tod{background:linear-gradient(180deg,rgba(20,30,46,.62),rgba(20,30,46,.42));box-shadow:inset 0 0 0 1px rgba(255,255,255,.12),inset 0 1px 0 rgba(255,255,255,.14),0 24px 50px -24px rgba(0,0,0,.7)}
.tseg{position:relative;z-index:1;min-width:0;overflow:hidden;display:flex;align-items:center;gap:12px;padding:0 18px 0 9px;border-radius:999px;text-align:left;transition:transform .3s var(--ease)}
.tseg:active{transform:scale(.98)}
.tseg .tb{display:flex;width:48px;height:48px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;transition:background .7s,color .7s,box-shadow .7s}
.tseg .tb svg{width:22px;height:22px}
.tseg .tx{min-width:0}
.tseg .tt{display:block;font-family:var(--ff-head);font-size:16.5px;font-weight:600;letter-spacing:-.015em;line-height:1.2;transition:color .7s}
.tseg .ts{display:block;margin-top:2px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:12.5px;line-height:1.25;transition:color .7s}
.tseg.m .tb{background:radial-gradient(circle at 35% 30%,#ffd95a,#f39b0c);color:#fff;box-shadow:0 0 0 4px rgba(255,214,120,.28),0 8px 18px -8px rgba(220,140,10,.9)}
.tseg.e .tb{background:rgba(23,35,27,.07);color:rgba(23,35,27,.55);box-shadow:inset 0 0 0 1px rgba(23,35,27,.1)}
.tseg .tt{color:#16231a}.tseg .ts{color:rgba(22,35,26,.6)}
.tseg[aria-pressed=false] .tt{color:rgba(22,35,26,.62)}.tseg[aria-pressed=false] .ts{color:rgba(22,35,26,.45)}
.tseg[aria-pressed=false]:hover .tt{color:#16231a}
.is-night .tseg.m .tb{background:rgba(255,255,255,.08);color:rgba(255,255,255,.55);box-shadow:inset 0 0 0 1px rgba(255,255,255,.14)}
.is-night .tseg.e .tb{background:rgba(255,255,255,.14);color:#fff;box-shadow:0 0 0 4px rgba(140,230,170,.16),inset 0 0 0 1px rgba(255,255,255,.25)}
.is-night .tseg .tt{color:#fff}.is-night .tseg .ts{color:rgba(255,255,255,.72)}
.is-night .tseg[aria-pressed=false] .tt{color:rgba(255,255,255,.6)}.is-night .tseg[aria-pressed=false] .ts{color:rgba(255,255,255,.4)}
.js .hero-in{opacity:0;transform:translateY(22px);transition:opacity 1s var(--ease),transform 1s var(--ease)}
.js .loaded .hero-in{opacity:1;transform:none}
.js .fade-in{opacity:0;transition:opacity 1.2s var(--ease)}
.js .loaded .fade-in{opacity:1}
.js .loaded .is-night .hs-arc{opacity:.3}
.hs-pill.hero-in{transition-delay:.15s}.hs-p.hero-in{transition-delay:.55s}.hs-btns.hero-in{transition-delay:.68s}.hs-proof.hero-in{transition-delay:.8s}.hs-tod.hero-in{transition-delay:.9s}
.hs-chip.fade-in:nth-of-type(1){transition-delay:1s}.hs-chip.fade-in{transition-delay:1.15s}
.hero-tag{position:absolute;inset-inline:0;top:50%;transform:translateY(-50%);padding:0 24px;text-align:center;font-family:var(--ff-serif);font-weight:400;letter-spacing:-.03em;color:#fff;font-size:2.5rem;opacity:0;pointer-events:none;z-index:3;text-shadow:0 10px 40px rgba(0,0,0,.25)}
@media(min-width:640px){.hero-tag{font-size:4rem}}
@media(min-width:1024px){.hero-tag{font-size:5rem}}
@media(max-width:899px){
  .hero-wash.d{background:linear-gradient(180deg,rgba(250,241,226,.94) 0%,rgba(250,241,226,.8) 42%,rgba(250,241,226,0) 64%)}
  .hero-wash.n{background:linear-gradient(180deg,rgba(5,10,20,.88),rgba(5,10,20,.62) 42%,rgba(5,10,20,0) 64%)}
  .hero-stage{inset:0;width:auto;height:auto;transform:none!important}
  .hs-text{left:20px;right:20px;top:92px;width:auto}
  .hs-pill{height:34px;gap:7px;padding-right:10px;font-size:11.5px;white-space:nowrap}.hs-pill b{height:26px;padding:0 9px;font-size:11px}
  .hs-h1{margin-top:18px}.hs-h1 .a{font-size:clamp(40px,11.6vw,86px)}.hs-h1 .b{font-size:clamp(40px,11.4vw,90px)}
  .hs-p{margin-top:14px;font-size:16px;max-width:32rem}
  .hs-btns{margin-top:20px;gap:10px}.hbtn{height:50px;width:auto!important;padding:0 16px;font-size:14.5px;gap:9px}.hbtn .ic{font-size:18px}
  .hs-proof{margin-top:18px;gap:14px}.avs span{width:36px;height:36px;font-size:12px;margin-left:-10px}.proof-t,.stars b{font-size:13px}.stars svg{width:14px;height:14px}
  .hs-chip,.hs-arc{display:none}
  .hs-tod{left:14px;right:14px;top:auto;bottom:18px;width:auto;height:64px;padding:4px}
  .tod-ind{top:4px;bottom:4px;left:4px;width:calc(50% - 4px)}
  .tseg{gap:9px;padding:0 10px 0 6px}.tseg .tb{width:40px;height:40px}.tseg .tb svg{width:19px;height:19px}
  .tseg .tt{font-size:14.5px}.tseg .ts{font-size:11px}
  .tseg .tx{flex:1}
}
@media(max-width:899px) and (max-height:900px){.hs-proof{display:none}}
/* ================= 3D VILLA ================= */
@property --w0{syntax:'<color>';inherits:true;initial-value:#fbf3e6}
@property --w1{syntax:'<color>';inherits:true;initial-value:#f6e8d3}
@property --w2{syntax:'<color>';inherits:true;initial-value:#e2cfb4}
@property --w3{syntax:'<color>';inherits:true;initial-value:#cbb393}
@property --wd1{syntax:'<color>';inherits:true;initial-value:#c48654}
@property --wd2{syntax:'<color>';inherits:true;initial-value:#93603a}
@property --dk1{syntax:'<color>';inherits:true;initial-value:#e9d9bd}
@property --dk2{syntax:'<color>';inherits:true;initial-value:#d0ba98}
@property --st1{syntax:'<color>';inherits:true;initial-value:#cdbb9c}
@property --st2{syntax:'<color>';inherits:true;initial-value:#a99476}
@property --in1{syntax:'<color>';inherits:true;initial-value:#ffeacc}
@property --in2{syntax:'<color>';inherits:true;initial-value:#f2c58a}
@property --gls{syntax:'<color>';inherits:true;initial-value:rgba(255,220,160,.24)}
@property --wa1{syntax:'<color>';inherits:true;initial-value:#95d6cf}
@property --wa2{syntax:'<color>';inherits:true;initial-value:#4b9fa6}
@property --pv1{syntax:'<color>';inherits:true;initial-value:#5a90c9}
@property --pv2{syntax:'<color>';inherits:true;initial-value:#1c406d}
@property --tr1{syntax:'<color>';inherits:true;initial-value:#b8c77f}
@property --tr2{syntax:'<color>';inherits:true;initial-value:#6a8442}
@property --tr3{syntax:'<color>';inherits:true;initial-value:#37532b}
@property --glow{syntax:'<color>';inherits:true;initial-value:rgba(255,190,90,0)}
@property --lamp{syntax:'<color>';inherits:true;initial-value:#fff1cc}
.scene-layers{position:absolute;inset:0;transform-origin:62% 70%}
.scene-front{transition:filter 1.6s ease}
.is-night .scene-front{filter:brightness(.34) saturate(.72)}
.villa-layer{position:absolute;left:0;top:0;width:1780px;height:884px;transform-origin:0 0;pointer-events:none}
.villa-pos{position:absolute;left:1352px;top:556px;width:0;height:0}
.villa{position:absolute;width:640px;height:440px;left:-320px;top:-220px;transform:rotateX(var(--rx,58deg)) rotateZ(var(--rz,-38deg)) scale(var(--vs,.9));
  --w0:#fbf3e6;--w1:#f6e8d3;--w2:#e2cfb4;--w3:#cbb393;--wd1:#c48654;--wd2:#93603a;--dk1:#e9d9bd;--dk2:#d0ba98;--st1:#cdbb9c;--st2:#a99476;
  --in1:#ffeacc;--in2:#f2c58a;--gls:rgba(255,220,160,.24);--wa1:#95d6cf;--wa2:#4b9fa6;--pv1:#5a90c9;--pv2:#1c406d;--tr1:#b8c77f;--tr2:#6a8442;--tr3:#37532b;--glow:rgba(255,190,90,0);--lamp:#fff1cc;
  --fr:#2b2621;--refl:.34;--sh:rgba(60,38,14,.3);--led:#57c76a;
  transition:--w0 1.6s,--w1 1.6s,--w2 1.6s,--w3 1.6s,--wd1 1.6s,--wd2 1.6s,--dk1 1.6s,--dk2 1.6s,--st1 1.6s,--st2 1.6s,--in1 1.6s,--in2 1.6s,--gls 1.6s,--wa1 1.6s,--wa2 1.6s,--pv1 1.6s,--pv2 1.6s,--tr1 1.6s,--tr2 1.6s,--tr3 1.6s,--glow 1.6s,--lamp 1.6s}
.is-night .villa{--w0:#4b5367;--w1:#444c5f;--w2:#373e50;--w3:#2d3343;--wd1:#5d4636;--wd2:#45342a;--dk1:#3f3f45;--dk2:#323238;--st1:#34343a;--st2:#28282d;
  --in1:#ffe0a4;--in2:#f4a751;--gls:rgba(255,196,110,.36);--wa1:#4fc3d6;--wa2:#1b5f7c;--pv1:#22324c;--pv2:#0f1a2b;--tr1:#3b4a33;--tr2:#2a3626;--tr3:#1b251a;--glow:rgba(255,178,80,.6);--lamp:#fff6d8;
  --refl:.06;--sh:rgba(0,0,0,.35);--led:#ffc46b}
.villa,.villa *{transform-style:preserve-3d}
.vb,.vf{position:absolute}
.vf{backface-visibility:visible}
.vglass{box-shadow:inset 0 0 0 4px var(--fr),0 0 46px var(--glow)}
.vpv{position:absolute;overflow:hidden;transform-origin:50% 100%;transform:rotateX(-26deg);border-radius:2px;
  background:linear-gradient(180deg,rgba(255,255,255,.22),transparent 45%),repeating-linear-gradient(90deg,transparent 0 calc(16.66% - 1px),rgba(200,220,240,.38) calc(16.66% - 1px) 16.66%),repeating-linear-gradient(0deg,transparent 0 calc(33.3% - 1px),rgba(200,220,240,.32) calc(33.3% - 1px) 33.3%),linear-gradient(135deg,var(--pv1),var(--pv2));
  box-shadow:inset 0 0 0 1.5px #d9e0e6,0 6px 6px -2px rgba(0,0,0,.25)}
.vpv::after{content:"";position:absolute;inset:-40%;background:linear-gradient(115deg,transparent 42%,rgba(255,255,255,.45) 50%,transparent 58%);transform:translateX(-70%);animation:pvs 7s ease-in-out infinite}
.is-night .vpv::after{opacity:0}
@keyframes pvs{0%,55%{transform:translateX(-70%)}85%,100%{transform:translateX(70%)}}
.vwater{position:absolute;overflow:hidden;border-radius:3px;background:linear-gradient(135deg,var(--wa1),var(--wa2));box-shadow:inset 0 0 0 5px var(--st1),inset 8px 8px 24px rgba(0,40,60,.35),0 0 40px var(--glow)}
.vwater::before{content:"";position:absolute;inset:-50%;opacity:.5;background:repeating-radial-gradient(circle at 30% 40%,rgba(255,255,255,.0) 0 14px,rgba(255,255,255,.55) 15px 16px,rgba(255,255,255,0) 17px 30px);animation:caus 9s linear infinite}
.vwater::after{content:"";position:absolute;inset:0;background:linear-gradient(115deg,rgba(255,255,255,.35) 0 18%,transparent 18% 40%,rgba(255,255,255,.18) 40% 46%,transparent 46%)}
@keyframes caus{to{transform:translate(18%,12%) rotate(8deg)}}
.vbat{position:absolute;width:26px;height:52px;border-radius:7px;background:linear-gradient(90deg,#fff,#e3e7ea);box-shadow:inset 0 0 0 1px rgba(0,0,0,.08),3px 4px 8px rgba(0,0,0,.25)}
.vbat::after{content:"";position:absolute;left:11px;top:10px;width:4px;height:26px;border-radius:2px;background:var(--led);box-shadow:0 0 10px 2px var(--led);transition:background 1.6s,box-shadow 1.6s}
.vgar{position:absolute;background:repeating-linear-gradient(180deg,#4b453f 0 9px,#3a3530 9px 11px);box-shadow:inset 0 0 0 3px var(--fr)}
.vlite{border-radius:50%;background:radial-gradient(circle,var(--lamp) 0 30%,rgba(255,206,130,.75) 45%,rgba(255,206,130,0) 70%)}
.vplant{border-radius:50% 50% 46% 46%/82% 82% 18% 18%;background:linear-gradient(90deg,var(--tr1),var(--tr2) 50%,var(--tr3))}
.vbush{border-radius:50%;background:radial-gradient(circle at 35% 30%,var(--tr1),var(--tr2) 55%,var(--tr3))}
.vshadow{position:absolute;background:var(--sh);filter:blur(14px);border-radius:12px}

@property --gr1{syntax:'<color>';inherits:true;initial-value:#c3c47f}
@property --gr2{syntax:'<color>';inherits:true;initial-value:#93a05a}
@property --so1{syntax:'<color>';inherits:true;initial-value:#b38c5c}
@property --so2{syntax:'<color>';inherits:true;initial-value:#86603c}
@property --so3{syntax:'<color>';inherits:true;initial-value:#5a3e2a}
@property --sw1{syntax:'<color>';inherits:true;initial-value:#e3d2b2}
@property --sw2{syntax:'<color>';inherits:true;initial-value:#bba684}
@property --ol1{syntax:'<color>';inherits:true;initial-value:#bfc28c}
@property --ol2{syntax:'<color>';inherits:true;initial-value:#86915c}
@property --hz{syntax:'<color>';inherits:true;initial-value:#f7dcb6}
@property --lav{syntax:'<color>';inherits:true;initial-value:#a08ccc}
.villa{--rz:-38deg;--rx:58deg;--face:rotateZ(calc(var(--rz) * -1)) rotateX(calc(var(--rx) * -1));
  --gr1:#c3c47f;--gr2:#93a05a;--so1:#b38c5c;--so2:#86603c;--so3:#5a3e2a;--sw1:#e3d2b2;--sw2:#bba684;--ol1:#bfc28c;--ol2:#86915c;--hz:#f7dcb6;--lav:#a08ccc}
.villa{transition:--w0 1.6s,--w1 1.6s,--w2 1.6s,--w3 1.6s,--wd1 1.6s,--wd2 1.6s,--dk1 1.6s,--dk2 1.6s,--st1 1.6s,--st2 1.6s,--in1 1.6s,--in2 1.6s,--gls 1.6s,--wa1 1.6s,--wa2 1.6s,--pv1 1.6s,--pv2 1.6s,--tr1 1.6s,--tr2 1.6s,--tr3 1.6s,--glow 1.6s,--lamp 1.6s,--gr1 1.6s,--gr2 1.6s,--so1 1.6s,--so2 1.6s,--so3 1.6s,--sw1 1.6s,--sw2 1.6s,--ol1 1.6s,--ol2 1.6s,--hz 1.6s,--lav 1.6s}
.is-night .villa{--gr1:#33432f;--gr2:#223022;--so1:#4a3b2e;--so2:#352a21;--so3:#221a14;--sw1:#46433f;--sw2:#33312e;--ol1:#3d4635;--ol2:#2a3225;--hz:#16203a;--lav:#4d4670}
.vcyp{border-radius:50% 50% 46% 46%/88% 88% 12% 12%;background:linear-gradient(90deg,var(--tr1),var(--tr2) 42%,var(--tr3));box-shadow:inset 3px 2px 0 rgba(255,214,150,.38)}
.is-night .vcyp{box-shadow:inset 2px 2px 0 rgba(170,190,255,.12)}
.volive{background:
  radial-gradient(22% 16% at 34% 26%,rgba(255,246,210,.45),transparent 70%),
  radial-gradient(40% 26% at 50% 30%,var(--ol1) 0 64%,transparent 66%),
  radial-gradient(28% 20% at 26% 46%,var(--ol2) 0 64%,transparent 66%),
  radial-gradient(30% 22% at 74% 44%,var(--ol2) 0 64%,transparent 66%),
  radial-gradient(34% 22% at 52% 54%,var(--ol2) 0 64%,transparent 66%),
  linear-gradient(90deg,transparent 46%,#6c5844 46% 54%,transparent 54%) 0 100%/100% 40% no-repeat}
.vtsh{position:absolute;border-radius:50%;background:radial-gradient(closest-side,var(--sh),transparent);transform:translateZ(.6px)}
.vstone{position:absolute;border-radius:12px;background:linear-gradient(135deg,var(--sw1),var(--sw2));box-shadow:2px 3px 0 rgba(0,0,0,.12)}
.vpool{position:absolute;border-radius:50%;background:radial-gradient(closest-side,rgba(255,200,110,.75),rgba(255,200,110,0));opacity:0;transition:opacity 1.6s;transform:translateZ(.8px)}
.is-night .vpool{opacity:1}
.vfly{border-radius:50%;background:#ffe9a8;box-shadow:0 0 8px 3px rgba(255,220,120,.7);opacity:0}
.is-night .vfly{animation:fly 5s ease-in-out infinite}
@keyframes fly{0%,100%{opacity:0;translate:0 0}50%{opacity:1;translate:6px -10px}}
.vfire{position:absolute;border-radius:50%;background:radial-gradient(circle,#fff1c2 0 18%,#ffb04a 40%,rgba(255,120,40,0) 70%);opacity:.0;transition:opacity 1.6s;animation:flick 1.4s ease-in-out infinite alternate}
.is-night .vfire{opacity:1}
@keyframes flick{to{transform:translateZ(14px) scale(1.15)}}
.sun-haze{position:absolute;left:315px;top:-318px;width:1400px;height:1400px;border-radius:50%;background:radial-gradient(closest-side,rgba(255,226,170,.55),rgba(255,214,150,.18) 45%,rgba(255,214,150,0));mix-blend-mode:screen;pointer-events:none}

/* Customers */
.customers{padding:56px 0;background:var(--bg)}
@media(min-width:640px){.customers{padding:80px 0}}
.customers h2{text-align:center;font-size:14px;font-weight:400;color:var(--muted)}
.marquee{margin-top:40px;overflow:hidden;-webkit-mask-image:linear-gradient(90deg,transparent,#000 12%,#000 88%,transparent);mask-image:linear-gradient(90deg,transparent,#000 12%,#000 88%,transparent)}
.marquee-track{display:flex;width:max-content;animation:marquee 40s linear infinite}
.marquee:hover .marquee-track{animation-play-state:paused}
@keyframes marquee{to{transform:translateX(-50%)}}
.marquee ul{display:flex;align-items:center;flex-shrink:0}
.marquee li{display:flex;align-items:center;gap:10px;padding:0 32px;color:rgba(14,26,18,.38);transition:color .3s;font-size:24px}
@media(min-width:640px){.marquee li{padding:0 48px}}
.marquee li:hover{color:var(--primary-strong)}
.marquee li span{white-space:nowrap;font-family:var(--ff-head);font-weight:600;letter-spacing:-.02em}

/* Manifesto */
.manifesto{position:relative;height:260vh;height:260svh;background:var(--bg)}
.manifesto-sticky{position:sticky;top:0;height:100vh;height:100svh;display:flex;align-items:center;overflow:hidden}
.manifesto-glow{position:absolute;width:60vmax;height:60vmax;right:-20vmax;top:-10vmax;border-radius:50%;background:radial-gradient(closest-side,rgba(244,178,63,.18),rgba(244,178,63,0));pointer-events:none;opacity:0;transition:opacity 1.2s}
.manifesto-inner{position:relative;width:100%;max-width:72rem;margin:0 auto;padding:56px 16px 0}
@media(min-width:640px){.manifesto-inner{padding:56px 24px 0}}
@media(min-width:1024px){.manifesto-inner{padding:56px 32px 0}}
.m-label{display:flex;align-items:center;gap:16px}
.m-label h2{flex-shrink:0}
.m-label .rule{height:1px;flex:1;background:rgba(14,26,18,.1)}
.m-text{margin-top:32px;font-family:var(--ff-head);font-weight:600;font-size:2rem;line-height:1.12;letter-spacing:-.035em}
@media(min-width:640px){.m-text{margin-top:40px;font-size:3rem;line-height:1.1}}
@media(min-width:1024px){.m-text{font-size:3.75rem}}
.mw{display:inline-block;opacity:.12;transform:translateY(.22em);transition:opacity .45s ease,transform .7s var(--ease)}
.mw.on{opacity:1;transform:none}
.mw.pr{color:#1d4630;font-family:var(--ff-serif);font-weight:500;letter-spacing:-.03em}
.mpill{position:relative;display:inline-block;height:.78em;width:1.9em;border-radius:999px;overflow:hidden;vertical-align:-.04em;clip-path:inset(0 100% 0 0 round 999px);transition:clip-path .9s var(--ease);box-shadow:inset 0 0 0 1px rgba(0,0,0,.06)}
.mpill.on{clip-path:inset(0 0 0 0 round 999px)}
.mpill svg{position:absolute;inset:0;width:100%;height:100%}
.m-meter{margin-top:40px;display:flex;align-items:center;gap:16px}
@media(min-width:640px){.m-meter{margin-top:56px}}
.m-meter .lab{font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;color:var(--muted)}
.m-meter .track{position:relative;height:4px;flex:1;overflow:hidden;border-radius:99px;background:var(--leaf-soft)}
.m-meter .fill{position:absolute;inset:0;border-radius:99px;transform-origin:left;transform:scaleX(0);background:linear-gradient(90deg,var(--sun),var(--leaf),var(--primary))}
.m-meter .pct{width:48px;text-align:right;font-size:14px}

/* Product */
.product{position:relative;isolation:isolate;overflow:hidden;background:var(--forest);padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.product{padding:128px 0}}
.aurora{position:absolute;inset:-10%;z-index:-2;filter:blur(70px);opacity:.75}
.aurora i{position:absolute;border-radius:50%;animation:aur 22s ease-in-out infinite alternate}
.aurora i:nth-child(1){width:48%;height:48%;left:4%;top:6%;background:radial-gradient(closest-side,rgba(87,199,106,.5),transparent)}
.aurora i:nth-child(2){width:44%;height:40%;right:6%;top:2%;background:radial-gradient(closest-side,rgba(244,178,63,.36),transparent);animation-duration:28s;animation-direction:alternate-reverse}
.aurora i:nth-child(3){width:60%;height:50%;left:24%;bottom:-6%;background:radial-gradient(closest-side,rgba(43,122,160,.32),transparent);animation-duration:34s}
@keyframes aur{to{transform:translate(8%,10%) scale(1.15)}}
.dotgrid{position:absolute;inset:0;z-index:-1;background-image:radial-gradient(rgba(255,255,255,.09) 1px,transparent 1.2px);background-size:26px 26px;-webkit-mask-image:radial-gradient(70% 60% at 50% 30%,#000,transparent);mask-image:radial-gradient(70% 60% at 50% 30%,#000,transparent)}
.product .h2{color:#fff}.product .h2 .serif{color:#bfe0c7}.cta .h2 .serif{color:#bfe0c7}
.product .lede{color:rgba(223,238,226,.7)}
.dash-wrap{margin-top:56px;perspective:1600px}
.dash-tilt{transform-origin:center top;will-change:transform,opacity}
.dash{display:flex;overflow:hidden;border-radius:28px;background:var(--bg);text-align:left;box-shadow:0 0 0 1px rgba(255,255,255,.16),0 60px 120px -50px rgba(0,0,0,.85),0 0 140px -30px rgba(87,199,106,.35)}
.dash-side{display:none;width:68px;flex-shrink:0;flex-direction:column;align-items:center;border-right:1px solid rgba(0,0,0,.05);background:rgba(255,255,255,.7);padding:20px 0}
.dash-side .nav-ic{display:flex;width:40px;height:40px;align-items:center;justify-content:center;border-radius:12px;color:var(--muted);font-size:18px}
.dash-side .nav-ic.on{background:var(--fg);color:#fff}
@media(min-width:1024px){.dash-side{display:flex}}
.dash-main{min-width:0;flex:1}
.dash-top{display:flex;align-items:center;justify-content:space-between;gap:16px;border-bottom:1px solid rgba(0,0,0,.05);background:rgba(255,255,255,.7);padding:12px 16px}
@media(min-width:640px){.dash-top{padding:12px 24px}}
.tabs{display:flex;align-items:center;gap:4px;min-width:0}
.tab{white-space:nowrap;border-radius:999px;padding:6px 12px;font-size:12px;font-weight:500;color:var(--muted);display:none}
.tab.on{display:inline;background:var(--bg);color:var(--fg);box-shadow:0 0 0 1px rgba(0,0,0,.05)}
@media(min-width:768px){.tab.md{display:inline}}
@media(min-width:1280px){.tab.xl{display:inline}}
.dash-tools{display:flex;align-items:center;gap:8px;flex-shrink:0}
.livepill{display:none;align-items:center;gap:6px;border-radius:999px;background:var(--accent);padding:6px 12px;font-size:12px;font-weight:500;color:var(--accent-fg)}
.livepill i{width:6px;height:6px;border-radius:50%;background:var(--primary);box-shadow:0 0 0 0 rgba(30,133,56,.5);animation:live 1.8s infinite}
@keyframes live{70%{box-shadow:0 0 0 7px rgba(30,133,56,0)}100%{box-shadow:0 0 0 0 rgba(30,133,56,0)}}
@media(min-width:640px){.livepill{display:inline-flex}}
.avatar{display:flex;width:32px;height:32px;align-items:center;justify-content:center;border-radius:50%;background:linear-gradient(135deg,var(--sun),#e08a3c);font-size:11px;font-weight:600;color:#fff}
.dash-body{padding:16px}
@media(min-width:640px){.dash-body{padding:24px}}
.dash-head{display:flex;flex-direction:column;gap:16px}
@media(min-width:640px){.dash-head{flex-direction:row;align-items:flex-end;justify-content:space-between}}
.dash-head h3{font-family:var(--ff-head);font-size:1.25rem;font-weight:500;letter-spacing:-.02em}
@media(min-width:640px){.dash-head h3{font-size:1.5rem}}
.dash-head p{margin-top:4px;font-size:12px;color:var(--muted)}
@media(min-width:640px){.dash-head p{font-size:14px}}
.seg{display:inline-flex;align-self:flex-start;border-radius:999px;background:#fff;padding:4px;box-shadow:0 0 0 1px rgba(0,0,0,.05)}
@media(min-width:640px){.seg{align-self:auto}}
.seg button{white-space:nowrap;border-radius:999px;padding:6px 14px;font-size:12px;font-weight:500;color:var(--muted);transition:background .3s,color .3s}
.seg button:hover{color:var(--fg)}
.seg button[aria-pressed=true]{background:var(--fg);color:#fff}
.kpis{margin-top:20px;display:grid;grid-template-columns:1fr 1fr;gap:12px}
@media(min-width:1280px){.kpis{grid-template-columns:repeat(4,1fr)}}
.kpi{position:relative;overflow:hidden;display:flex;min-width:0;flex-direction:column;border-radius:16px;background:linear-gradient(180deg,#fff,#fbfcfa);padding:16px;box-shadow:0 0 0 1px rgba(0,0,0,.06),0 10px 24px -20px rgba(14,26,18,.4)}
.kpi.solar::before{content:"";position:absolute;right:-30px;top:-30px;width:110px;height:110px;border-radius:50%;background:radial-gradient(closest-side,rgba(244,178,63,.22),transparent)}
.kpi .k{display:flex;align-items:center;gap:6px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:12px;color:var(--muted)}
.kpi .k .ic{font-size:13px}
.kpi .row{margin-top:8px;display:flex;align-items:flex-end;justify-content:space-between;gap:12px}
.kpi .v{font-family:var(--ff-head);font-size:1.5rem;font-weight:500;letter-spacing:-.02em}
.kpi .v small{margin-left:4px;font-size:12px;font-weight:400;color:var(--muted)}
.kpi .spark{position:relative;margin-bottom:6px;height:28px;width:64px;flex-shrink:0}
@media(min-width:640px){.kpi .spark{width:80px}}
.kpi .spark svg{width:100%;height:100%;overflow:visible}
.kpi .spark path{fill:none;stroke:var(--sage);stroke-width:2;stroke-linecap:round;vector-effect:non-scaling-stroke}
.kpi.solar .spark path{stroke:#f1c77a}
.kpi .spark i{position:absolute;width:8px;height:8px;left:100%;transform:translate(-50%,-50%);border-radius:50%;background:var(--primary);box-shadow:0 0 0 2px #fff}
.kpi.solar .spark i{background:var(--sun)}
.kpi .d{margin-top:auto;display:flex;align-items:center;gap:6px;padding-top:12px;font-size:12px;color:var(--muted)}
.kpi .d.good{color:var(--accent-fg)}
.kpi .d span{overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.kpi .meter{margin-top:12px;height:6px;overflow:hidden;border-radius:99px;background:var(--leaf-soft)}
.kpi .meter div{height:100%;border-radius:99px;background:linear-gradient(90deg,var(--leaf),var(--primary));transition:width .8s var(--ease)}
.dash-lower{margin-top:12px;display:grid;gap:12px}
@media(min-width:1024px){.dash-lower{grid-template-columns:minmax(0,1fr) 20rem}}
.panel{min-width:0;border-radius:16px;background:var(--card);padding:16px;box-shadow:0 0 0 1px rgba(0,0,0,.06),0 10px 24px -20px rgba(14,26,18,.4)}
@media(min-width:640px){.panel{padding:20px}}
.panel-h{display:flex;flex-wrap:wrap;align-items:baseline;justify-content:space-between;gap:4px 16px}
.panel-h h4{font-size:14px;font-weight:500}
.panel-h p{font-size:12px;color:var(--muted)}
.legend{margin-top:12px;display:flex;flex-wrap:wrap;align-items:center;gap:6px 16px;font-size:12px;color:var(--muted)}
.legend li{display:flex;align-items:center;gap:8px}
.lg-line{height:2px;width:16px;border-radius:9px;background:var(--primary)}
.lg-solar{height:10px;width:16px;border-radius:3px;background:linear-gradient(180deg,rgba(244,178,63,.55),rgba(244,178,63,.12));box-shadow:inset 0 2px 0 var(--sun)}
.lg-dot{width:10px;height:10px;border-radius:50%;background:var(--chart-2);box-shadow:0 0 0 2px #fff,0 0 0 3px rgba(0,0,0,.06)}
.chart-panel{display:flex;flex-direction:column}
.chart{position:relative;margin-top:12px;height:240px;padding:36px 0 28px 48px}
@media(min-width:640px){.chart{height:288px}}
@media(min-width:1024px){.chart{flex:1;min-height:288px;height:auto}}
.y-axis{position:absolute;left:0;top:36px;bottom:28px;width:40px}
.y-axis span,.x-axis span{position:absolute;font-size:11px;color:var(--muted);font-variant-numeric:tabular-nums;white-space:nowrap}
.y-axis span{right:0;transform:translateY(-50%)}
.x-axis{position:absolute;left:48px;right:0;bottom:0;height:20px}
.x-axis span{top:0;transform:translateX(-50%)}
.x-axis span:first-child{transform:none}
.plot{position:relative;height:100%}
.plot svg{position:absolute;inset:0;width:100%;height:100%;overflow:visible}
.grid-l{stroke:var(--border);stroke-width:1;vector-effect:non-scaling-stroke}
.band{fill:rgba(30,133,56,.07)}
.sfill{fill:url(#gSolarFill)}
.sline{fill:none;stroke:var(--sun);stroke-width:2;vector-effect:non-scaling-stroke}
.afill{fill:url(#gActual)}
.fline{fill:none;stroke:var(--primary);stroke-opacity:.6;stroke-width:2;stroke-dasharray:6 6;stroke-linecap:round;vector-effect:non-scaling-stroke}
.aline{fill:none;stroke:var(--primary);stroke-width:2.5;stroke-linecap:round;vector-effect:non-scaling-stroke;filter:drop-shadow(0 4px 6px rgba(30,133,56,.35))}
.draw{transition:clip-path 1.6s var(--ease)}
.nowl{position:absolute;top:0;bottom:0;width:1px;background:rgba(14,26,18,.2);pointer-events:none;transition:opacity .4s}
.nowl span{position:absolute;top:-10px;left:50%;transform:translateX(-50%);border-radius:999px;background:var(--fg);color:#fff;font-size:10px;font-weight:500;padding:2px 8px}
.peak{position:absolute;pointer-events:none;transition:left .6s var(--ease),top .6s var(--ease),opacity .3s}
.peak i{position:absolute;width:12px;height:12px;border-radius:50%;background:var(--chart-2);transform:translate(-50%,-50%);box-shadow:0 0 0 2px #fff,0 0 0 8px rgba(43,122,160,.16);animation:peakPulse 2.4s ease-in-out infinite}
@keyframes peakPulse{50%{box-shadow:0 0 0 2px #fff,0 0 0 14px rgba(43,122,160,0)}}
.peak span{position:absolute;bottom:12px;transform:translateX(-50%);white-space:nowrap;border-radius:8px;background:#fff;padding:4px 8px;font-size:11px;font-weight:500;box-shadow:0 1px 2px rgba(0,0,0,.06),0 0 0 1px rgba(0,0,0,.05);transition:opacity .2s}
.hit{position:absolute;inset:0;cursor:crosshair;touch-action:pan-y;border-radius:8px}
.hv{position:absolute;top:0;bottom:0;width:1px;background:rgba(14,26,18,.35);pointer-events:none;opacity:0;transition:opacity .15s}
.hv-dot{position:absolute;width:9px;height:9px;border-radius:50%;transform:translate(-50%,-50%);box-shadow:0 0 0 2px #fff;pointer-events:none;opacity:0;transition:opacity .15s}
.tip{position:absolute;z-index:3;min-width:176px;pointer-events:none;border-radius:12px;background:rgba(11,31,20,.92);color:#fff;padding:10px 12px;font-size:12px;opacity:0;transition:opacity .15s;-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px);box-shadow:0 18px 40px -16px rgba(0,0,0,.5)}
.tip b{display:block;font-weight:500;margin-bottom:6px}
.tip div{display:flex;justify-content:space-between;gap:16px;color:rgba(255,255,255,.7)}
.tip div span:first-child{display:flex;align-items:center;gap:6px}
.tip div span:first-child i{width:7px;height:7px;border-radius:50%}
.tip div span:last-child{color:#fff;font-variant-numeric:tabular-nums}
.chart.hovering .hv,.chart.hovering .hv-dot,.chart.hovering .tip{opacity:1}
.chart.hovering .peak span{opacity:0}
.side-panel{display:flex;flex-direction:column;gap:20px}
.mixbar{margin-top:16px;display:flex;height:12px;gap:2px;overflow:hidden;border-radius:99px}
.mixbar div{height:100%;flex-basis:0;transition:flex-grow .7s var(--ease)}
.mixlist{margin-top:16px;display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px 16px}
.mixlist li{display:flex;flex-direction:column;gap:2px;font-size:12px}
.mixlist li span{display:flex;align-items:center;gap:6px;color:var(--muted)}
.mixlist i{width:10px;height:10px;border-radius:3px}
.mixlist b{font-family:var(--ff-head);font-size:1.125rem;font-weight:500;font-variant-numeric:tabular-nums}
.hr{height:1px;background:rgba(0,0,0,.05)}
.actions{margin-top:12px;display:flex;flex-direction:column;gap:8px}
.action{display:flex;align-items:center;gap:12px;border-radius:12px;background:var(--bg);padding:12px;transition:background .4s,box-shadow .4s}
.action.done{background:var(--accent);box-shadow:inset 0 0 0 1px rgba(30,133,56,.18)}
.action .ai{display:flex;width:32px;height:32px;flex-shrink:0;align-items:center;justify-content:center;border-radius:9px;background:#fff;color:var(--primary);box-shadow:0 0 0 1px rgba(0,0,0,.05);font-size:16px}
.action .ai.amber{color:#c98419}
.action .ai.blue{color:var(--chart-2)}
.action .at{min-width:0;flex:1}
.action .at p:first-child{font-size:13px;font-weight:500;line-height:1.3}
.action .at p:last-child{margin-top:2px;font-size:12px;line-height:1.3;color:var(--muted)}
.sched{display:inline-flex;height:32px;flex-shrink:0;align-items:center;gap:4px;border-radius:999px;padding:0 12px;font-size:12px;font-weight:500;background:var(--fg);color:#fff;transition:background .3s,color .3s}
.sched:hover{background:var(--forest)}
.action.done .sched{background:#fff;color:var(--accent-fg);box-shadow:inset 0 0 0 1px rgba(30,133,56,.3)}
.features3{margin-top:56px;display:grid;gap:32px}
@media(min-width:640px){.features3{grid-template-columns:repeat(3,1fr)}}
.features3 li{display:flex;gap:16px}
.fi{display:flex;width:40px;height:40px;flex-shrink:0;align-items:center;justify-content:center;border-radius:12px;font-size:20px}
.fi.dark{background:linear-gradient(180deg,rgba(255,255,255,.12),rgba(255,255,255,.04));color:var(--leaf);box-shadow:0 0 0 1px rgba(255,255,255,.14)}
.fi.light{background:var(--accent);color:var(--accent-fg)}
.fi.amber{background:var(--sun-soft);color:#b5740f}
.fi.white{background:#fff;color:var(--primary);box-shadow:0 0 0 1px rgba(0,0,0,.05)}
.features3 h3{font-size:1rem;font-weight:500;color:#fff}
.features3 p{margin-top:6px;font-size:14px;line-height:1.65;color:rgba(223,238,226,.65)}

/* Solutions */
.solutions{position:relative;background:var(--bg);padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.solutions{padding:128px 0}}
.sol-head{display:flex;flex-direction:column;gap:40px}
.sol-head .h2 .sub{display:block;font-family:var(--ff-serif);font-weight:500;letter-spacing:-.035em;color:#1d4630}
.stages{position:relative;display:none;width:100%;max-width:28rem;flex-shrink:0;padding-bottom:4px}
.stages .line{position:absolute;left:7px;right:7px;top:7px;height:1px;background:rgba(14,26,18,.1)}
.stages .line .f{position:absolute;inset:0;transform-origin:left;transform:scaleX(0);background:linear-gradient(90deg,var(--sun),var(--leaf),var(--primary))}
.stages .line .dot{position:absolute;top:50%;width:8px;height:8px;border-radius:50%;background:var(--leaf);transform:translate(-50%,-50%);box-shadow:0 0 12px 2px rgba(87,199,106,.65);left:0}
.stages ol{position:relative;display:flex;justify-content:space-between}
.stages li{display:flex;flex-direction:column;gap:6px}
.stages li:nth-child(2){align-items:center;text-align:center}
.stages li:nth-child(3){align-items:flex-end;text-align:right}
.stages .knob{position:relative;width:14px;height:14px;border-radius:50%;background:var(--bg);box-shadow:0 0 0 1px rgba(14,26,18,.2)}
.stages .knob::after{content:"";position:absolute;inset:0;border-radius:50%;background:var(--primary);box-shadow:0 0 0 5px rgba(30,133,56,.16);transform:scale(0);opacity:0;transition:transform .5s var(--ease),opacity .5s}
.stages li.on .knob::after{transform:none;opacity:1}
.stages .n{margin-top:8px;font-size:14px;font-weight:500;opacity:.45;transition:opacity .5s}
.stages .s{font-size:12px;color:var(--muted);opacity:.45;transition:opacity .5s}
.stages li.on .n,.stages li.on .s{opacity:1}
.sol-track-wrap{margin-top:48px}
.sol-track{position:relative;display:flex;flex-direction:column;gap:16px;max-width:80rem;margin:0 auto;padding:0 16px}
@media(min-width:640px){.sol-track{padding:0 24px}}
.sol-intro{max-width:36rem;padding-bottom:16px}
.sol-intro p{font-size:1rem;line-height:1.65;color:var(--muted)}
.sol-intro .cue{display:none;margin-top:32px;align-items:center;gap:12px;font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;color:rgba(14,26,18,.6)}
.cue-line{position:relative;height:1px;width:56px;overflow:hidden;background:rgba(14,26,18,.15)}
.cue-line::after{content:"";position:absolute;inset:0 auto 0 0;width:50%;background:var(--primary);animation:cue 1.8s var(--ease) infinite}
@keyframes cue{from{transform:translateX(-100%)}to{transform:translateX(200%)}}
.stage{position:relative;isolation:isolate;overflow:hidden;border-radius:32px}
.stage.dark{background:var(--forest);color:#fff}
.stage.light{background:#fff;box-shadow:inset 0 0 0 1px rgba(0,0,0,.05),0 30px 60px -40px rgba(14,26,18,.35)}
.stage-bg{position:absolute;inset:0;z-index:-2}
.stage-bg svg{width:100%;height:100%}
.stage.dark::before{content:"";position:absolute;inset:0;z-index:-1;background:linear-gradient(180deg,rgba(11,31,20,.96),rgba(11,31,20,.7) 45%,rgba(11,31,20,.05))}
.stage-in{display:flex;flex-direction:column;gap:32px;padding:24px}
@media(min-width:640px){.stage-in{padding:32px}}
.stage-copy{display:flex;flex-direction:column}
.stage-top{display:flex;align-items:center;justify-content:space-between;gap:16px}
.chip{display:inline-flex;align-items:center;gap:8px;border-radius:999px;padding:4px 12px 4px 4px;font-size:12px;font-weight:500}
.chip .ci{display:flex;width:24px;height:24px;align-items:center;justify-content:center;border-radius:50%;font-size:14px}
.stage.dark .chip{background:rgba(255,255,255,.1);box-shadow:0 0 0 1px rgba(255,255,255,.15)}
.stage.dark .chip .ci{background:var(--sun);color:var(--forest)}
.stage.light .chip{background:var(--bg);box-shadow:0 0 0 1px rgba(0,0,0,.05)}
.stage.light .chip .ci{background:var(--primary);color:#fff}
.stage-num{font-family:var(--ff-mono);font-size:12px;color:var(--muted)}
.stage.dark .stage-num{color:rgba(255,255,255,.5)}
.stage h3{margin-top:24px;max-width:28rem;font-family:var(--ff-head);font-weight:700;font-size:1.875rem;line-height:1.15;letter-spacing:-.03em}
@media(min-width:640px){.stage h3{font-size:2.25rem}}
.stage .sp{margin-top:16px;max-width:28rem;font-size:15px;line-height:1.65;color:var(--muted)}
.stage.dark .sp{color:rgba(223,238,226,.78)}
.stage .next{margin-top:auto;display:flex;align-items:center;gap:12px;padding-top:32px;font-size:14px;line-height:1.4;color:var(--muted)}
.stage.dark .next{color:rgba(223,238,226,.72)}
.stage .next b{font-weight:500;color:var(--fg)}
.stage.dark .next b{color:#fff}
.next .ni{display:flex;width:36px;height:36px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;font-size:16px;background:var(--accent);color:var(--accent-fg);box-shadow:0 0 0 1px rgba(0,0,0,.05)}
.stage.dark .next .ni{background:rgba(255,255,255,.1);color:var(--sun);box-shadow:0 0 0 1px rgba(255,255,255,.15)}
.phone-wrap{display:flex;justify-content:center;margin-bottom:-112px}
@media(min-width:640px){.phone-wrap{margin-bottom:-96px}}
.phone{position:relative;width:248px;border-radius:46px;background:linear-gradient(145deg,#2a3330,#0d1210 40%,#1c2421);padding:10px;box-shadow:0 50px 90px -30px rgba(0,0,0,.85),0 0 0 1px rgba(255,255,255,.12),inset 0 0 0 1px rgba(255,255,255,.06)}
@media(min-width:640px){.phone{width:268px}}
.screen{position:relative;overflow:hidden;border-radius:37px;background:radial-gradient(120% 60% at 80% 0%,rgba(244,178,63,.35),transparent 60%),linear-gradient(180deg,#123222,#0b1f14 60%);padding:12px 16px 24px;color:#fff}
.screen::after{content:"";position:absolute;inset:0;background:linear-gradient(125deg,rgba(255,255,255,.1),transparent 35%);pointer-events:none}
.statusbar{display:flex;align-items:center;justify-content:space-between;padding:0 8px;font-size:11px;font-weight:600}
.notch{height:20px;width:80px;border-radius:99px;background:#000}
.sigs{display:flex;align-items:center;gap:4px}
.sigs .bars{display:flex;align-items:flex-end;gap:1px}
.sigs .bars i{width:3px;border-radius:1px;background:#fff}
.sigs .batt{height:10px;width:20px;border-radius:3px;border:1px solid rgba(255,255,255,.7);padding:1px}
.sigs .batt i{display:block;height:100%;width:75%;border-radius:1px;background:#fff}
.ph-row{margin-top:20px;display:flex;align-items:center;justify-content:space-between}
.ph-row .l{display:flex;align-items:center;gap:8px;font-size:12px;font-weight:500;color:rgba(255,255,255,.8)}
.ph-row .l svg{width:20px;height:20px}
.ph-row .r{border-radius:999px;background:rgba(255,255,255,.1);padding:4px 10px;font-size:10px;font-weight:500;color:rgba(255,255,255,.8)}
.ph-big{margin-top:20px;font-family:var(--ff-head);font-size:2.6rem;font-weight:600;line-height:1;letter-spacing:-.02em}
.ph-big small{margin-left:4px;font-size:14px;font-weight:400;color:rgba(255,255,255,.6)}
.ph-sub{margin-top:8px;display:flex;align-items:center;gap:6px;font-size:11px;color:rgba(255,255,255,.7)}
.ph-sub i{width:6px;height:6px;border-radius:50%;background:var(--sun);box-shadow:0 0 8px var(--sun)}
.ph-chart{position:relative;margin-top:18px;height:112px}
.ph-chart svg{position:absolute;inset:0;width:100%;height:100%;overflow:visible}
.ph-x{margin-top:8px;display:flex;justify-content:space-between;font-size:10px;color:rgba(255,255,255,.45)}
.ph-cards{margin-top:18px;display:grid;grid-template-columns:1fr 1fr;gap:8px}
.ph-cards div{border-radius:16px;background:rgba(255,255,255,.08);padding:12px;box-shadow:inset 0 0 0 1px rgba(255,255,255,.06)}
.ph-cards .ic{font-size:16px;color:var(--sun)}
.ph-cards div+div .ic{color:var(--leaf)}
.ph-cards b{display:block;margin-top:8px;font-size:18px;font-weight:500;line-height:1}
.ph-cards span{display:block;margin-top:4px;font-size:10px;color:rgba(255,255,255,.6)}
.soc{display:flex;align-items:center;gap:24px}
@media(min-width:640px){.soc{gap:32px}}
.ring{position:relative;width:112px;height:112px;flex-shrink:0}
@media(min-width:640px){.ring{width:132px;height:132px}}
.ring svg{width:100%;height:100%;transform:rotate(-90deg);overflow:visible}
.ring .rv{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;justify-content:center}
.ring .rv b{font-family:var(--ff-head);font-size:1.875rem;font-weight:600;letter-spacing:-.02em}
.ring .rv>span{font-size:11px;color:var(--muted)}
.ring-arc{transition:stroke-dashoffset 1.8s var(--ease)}
.soc dl{flex:1;display:grid;gap:12px}
.soc dl div{display:flex;align-items:baseline;justify-content:space-between;gap:12px;border-bottom:1px solid rgba(0,0,0,.05);padding-bottom:10px}
.soc dl div:last-child{border:0;padding:0}
.soc dt{font-size:14px;color:var(--muted)}
.soc dd{font-size:14px;font-weight:500}
.plan{margin-top:28px}
.plan-h{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:8px}
.plan-h p{font-size:12px;font-weight:500}
.plan-h ul{display:flex;align-items:center;gap:12px;font-size:11px;color:var(--muted)}
.plan-h li{display:flex;align-items:center;gap:6px}
.plan-h i{width:10px;height:10px;border-radius:3px}
.cells{margin-top:12px;display:grid;grid-template-columns:repeat(24,1fr);gap:2px}
.cells span{height:36px;border-radius:4px;background:var(--mist);transform-origin:bottom;transition:transform .6s var(--ease)}
.js .cells:not(.in) span{transform:scaleY(.2)}
.cells .c{background:linear-gradient(180deg,#f8c766,#e9a23a)}
.cells .d{background:linear-gradient(180deg,#2fa04b,#1b7a33)}
.cells .cur{box-shadow:0 0 0 2px #fff,0 0 0 4px var(--fg)}
.axis5{margin-top:8px;display:flex;justify-content:space-between;font-size:11px;color:var(--muted);font-variant-numeric:tabular-nums}
.reserve{margin-top:14px;display:flex;align-items:center;gap:8px;font-size:12px;color:var(--muted)}
.reserve .ic{color:var(--chart-2)}
.bars{position:relative;margin-top:32px}
.bars-in{display:flex;height:144px;align-items:flex-end;gap:2px;border-radius:8px}
.bars-in>div{display:flex;height:100%;flex:1;align-items:flex-end;justify-content:center;cursor:pointer}
.bar{position:relative;width:100%;max-width:24px;border-radius:4px 4px 0 0;background:linear-gradient(180deg,#d3dfd4,#bccdbd);transform-origin:bottom;transition:transform .8s var(--ease),opacity .2s}
.bar.win{background:linear-gradient(180deg,#2fa04b,#1b7a33)}
.js .bars:not(.in) .bar{transform:scaleY(0)}
.bars-in:hover .bar{opacity:.45}
.bars-in>div:hover .bar{opacity:1}
.bar span{position:absolute;top:-24px;left:50%;transform:translateX(-50%);white-space:nowrap;font-size:11px;font-weight:500;opacity:0;transition:opacity .2s}
.bar.max span{opacity:1}
.bars-in:hover .bar.max span{opacity:0}
.bars-in>div:hover .bar span{opacity:1!important}
.underneath{padding-top:16px}
.underneath>p{font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;color:var(--muted)}
.underneath ul{margin-top:16px;display:grid;gap:16px}
@media(min-width:768px){.underneath ul{grid-template-columns:repeat(3,1fr)}}
.spot{position:relative;isolation:isolate;overflow:hidden;border-radius:24px;background:#fff;padding:24px;box-shadow:0 0 0 1px rgba(0,0,0,.05);transition:transform .5s var(--ease),box-shadow .5s}
.spot:hover{transform:translateY(-4px);box-shadow:0 0 0 1px rgba(0,0,0,.05),0 24px 48px -28px rgba(14,26,18,.35)}
.spot::before{content:"";position:absolute;inset:0;z-index:-1;border-radius:inherit;opacity:0;transition:opacity .5s;background:radial-gradient(420px circle at var(--sx,50%) var(--sy,50%),rgba(244,178,63,.14),transparent 65%)}
.spot:hover::before{opacity:1}
.spot .sh{display:flex;align-items:center;gap:12px}
.spot h3{font-size:1rem;font-weight:500}
.spot p{margin-top:12px;font-size:14px;line-height:1.65;color:var(--muted)}
@media(min-width:1024px){
  .solutions{padding:0;height:calc(100vh + var(--dist,2000px));height:calc(100svh + var(--dist,2000px))}
  .sol-sticky{position:sticky;top:0;height:100vh;height:100svh;display:flex;flex-direction:column;overflow:hidden;padding:80px 0 40px}
  .sol-head{flex-direction:row;align-items:flex-end;justify-content:space-between}
  .stages{display:block}
  .sol-track-wrap{margin-top:40px;flex:1;min-height:0;overflow:clip}
  .sol-track{flex-direction:row;gap:24px;height:100%;width:max-content;max-width:none;margin:0;padding:0 max(2rem,calc((100vw - 80rem)/2 + 2rem));will-change:transform}
  .sol-intro{display:flex;width:21rem;max-width:none;flex-shrink:0;flex-direction:column;justify-content:space-between;padding:8px 0}
  .sol-intro p{font-size:1.125rem}
  .sol-intro .cue{display:flex}
  .stage{height:100%;width:min(72vw,56rem);flex-shrink:0}
  .stage-in{display:grid;grid-template-columns:minmax(0,.85fr) minmax(0,1fr);grid-template-rows:minmax(0,1fr);gap:40px;padding:40px;height:100%}
  .stage h3{font-size:1.875rem}
  .phone-wrap{margin-bottom:0;align-items:flex-start}
  .stage .viz{align-self:center}
  .underneath{display:flex;height:100%;width:24rem;flex-shrink:0;flex-direction:column;padding-top:0}
  .underneath ul{display:flex;flex-direction:column;flex:1;min-height:0;gap:12px}
  .underneath .spot{flex:1;padding:20px}
}
@media(min-width:1280px){.stage h3{font-size:2.25rem}}

/* Insights */
.insights{background:#fff;padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.insights{padding:128px 0}}
.stats{margin-top:56px;display:grid;gap:40px 32px}
@media(min-width:640px){.stats{grid-template-columns:1fr 1fr}}
@media(min-width:1024px){.stats{grid-template-columns:repeat(4,1fr)}}
.stat{display:flex;flex-direction:column;border-top:1px solid var(--border);padding-top:24px;position:relative}
.stat::before{content:"";position:absolute;top:-1px;left:0;height:1px;width:100%;background:linear-gradient(90deg,var(--sun),var(--primary));transform:scaleX(0);transform-origin:left;transition:transform 1.4s var(--ease) .2s}
.stat.in::before{transform:scaleX(1)}
.stat dt{margin-top:12px;font-size:14px;font-weight:500}
.stat .num{order:-1;font-family:var(--ff-serif);font-size:3.25rem;font-weight:500;letter-spacing:-.035em;font-variant-numeric:tabular-nums}
@media(min-width:640px){.stat .num{font-size:3.75rem}}
.stat .desc{margin-top:8px;font-size:14px;line-height:1.65;color:var(--muted)}
.quotes{margin-top:64px;display:grid;gap:16px}
@media(min-width:1024px){.quotes{grid-template-columns:1.35fr 1fr}}
.q-big{position:relative;isolation:isolate;display:flex;min-height:28rem;flex-direction:column;justify-content:space-between;overflow:hidden;border-radius:32px;background:var(--forest);padding:32px}
@media(min-width:640px){.q-big{padding:40px}}
.q-big .bg{position:absolute;inset:0;z-index:-2;width:100%;height:100%}
.q-big::before{content:"";position:absolute;inset:0;z-index:-1;background:linear-gradient(160deg,rgba(11,31,20,.94),rgba(11,31,20,.6) 55%,rgba(11,31,20,.15))}
.q-big .qi{font-size:32px;color:var(--sun)}
.q-big blockquote{margin-top:32px;font-family:var(--ff-serif);font-size:1.75rem;font-weight:400;line-height:1.3;letter-spacing:-.02em;color:#fff}
@media(min-width:640px){.q-big blockquote{font-size:2.15rem}}
.who{margin-top:40px;display:flex;align-items:center;gap:12px}
.who .av{display:flex;width:44px;height:44px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;font-size:18px}
.who b{display:block;font-size:14px;font-weight:500}
.who span span{display:block;font-size:14px;color:var(--muted)}
.q-big .who b{color:#fff}.q-big .who span span{color:rgba(223,238,226,.65)}
.q-big .av{background:rgba(255,255,255,.12);color:var(--sun);box-shadow:inset 0 0 0 1px rgba(255,255,255,.18)}
.q-sm{display:flex;flex-direction:column;justify-content:space-between;border-radius:32px;background:var(--bg);padding:32px}
.q-sm blockquote{font-size:1.125rem;line-height:1.65}
.q-sm .av{background:var(--accent);color:var(--accent-fg)}
.qcol{display:grid;gap:16px}
.ph-tag{display:inline-block;font-style:normal;margin-left:6px;border-radius:999px;padding:1px 7px;font-size:10px;font-weight:500;letter-spacing:.06em;text-transform:uppercase;vertical-align:1px;background:rgba(14,26,18,.06);color:var(--muted)}
.q-big .ph-tag{background:rgba(255,255,255,.12);color:rgba(255,255,255,.7)}
.footnote{margin-top:20px;font-size:12px;color:var(--muted)}

/* How it works */
.how{background:var(--bg);padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.how{padding:128px 0}}
.timeline{position:relative;max-width:64rem;margin:64px auto 0}
@media(min-width:640px){.timeline{margin-top:80px}}
.tl-rail{position:absolute;top:24px;bottom:24px;left:24px;width:1px;transform:translateX(-50%);background:rgba(14,26,18,.1)}
@media(min-width:768px){.tl-rail{left:50%}}
.tl-rail .f{position:absolute;inset:0;transform-origin:top;transform:scaleY(0);background:linear-gradient(180deg,var(--sun),var(--leaf),var(--primary-strong))}
.tl-rail .dot{position:absolute;left:50%;width:10px;height:10px;border-radius:50%;background:var(--sun);transform:translate(-50%,-50%);box-shadow:0 0 14px 3px rgba(244,178,63,.7);top:0}
.timeline ol{position:relative;display:flex;flex-direction:column;gap:56px}
@media(min-width:768px){.timeline ol{gap:80px}}
.tl{position:relative;display:grid;grid-template-columns:3rem minmax(0,1fr);column-gap:20px;perspective:1200px}
@media(min-width:768px){.tl{grid-template-columns:minmax(0,1fr) 3rem minmax(0,1fr);column-gap:48px}}
.tl-badge{position:relative;z-index:1;grid-column:1;grid-row:1}
@media(min-width:768px){.tl-badge{grid-column:2}}
.badge{position:relative;display:flex;width:48px;height:48px;align-items:center;justify-content:center;border-radius:50%;background:#fff;font-family:var(--ff-head);font-size:14px;font-weight:500;color:var(--muted);box-shadow:0 0 0 1px rgba(0,0,0,.1)}
.badge .on{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;border-radius:50%;background:var(--primary);color:#fff;box-shadow:0 0 0 8px rgba(30,133,56,.12);transform:scale(0);opacity:0;transition:transform .6s var(--ease),opacity .6s}
.badge.final .on{background:var(--forest);color:var(--sun);box-shadow:0 0 0 8px rgba(244,178,63,.18)}
.tl.in .badge .on{transform:none;opacity:1}
.tl-card{grid-column:2;grid-row:1;transform-origin:center top}
.js .tl-card{opacity:.3;transform:translateY(72px) scale(.92) rotate(var(--rot,-2.5deg)) rotateX(28deg);transition:opacity 1.1s var(--ease),transform 1.1s var(--ease)}
.js .tl.in .tl-card{opacity:1;transform:none}
@media(min-width:768px){.tl.left .tl-card{grid-column:1}.tl.right .tl-card{grid-column:3}}
.tl-card .spot{padding:28px;border-radius:28px}
.tl-card .wk{font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;color:var(--primary)}
.tl-card h3{margin-top:8px;font-size:1.125rem;font-weight:500}
.tl-card p{margin-top:8px;font-size:15px;line-height:1.65;color:var(--muted)}
@media(min-width:768px){.tl-card .wk{display:none}.tl-card h3{margin-top:0}}
.tl-ghost{display:none;grid-row:1;padding-top:4px;font-family:var(--ff-head);font-size:3rem;font-weight:300;letter-spacing:-.04em;color:rgba(14,26,18,.15);transition:transform 1.2s var(--ease),opacity 1.2s}
@media(min-width:768px){.tl-ghost{display:block}.tl.left .tl-ghost{grid-column:3;text-align:left}.tl.right .tl-ghost{grid-column:1;text-align:right}}
@media(min-width:1024px){.tl-ghost{font-size:3.75rem}}
.js .tl.left .tl-ghost{transform:translateX(56px);opacity:0}
.js .tl.right .tl-ghost{transform:translateX(-56px);opacity:0}
.js .tl.in .tl-ghost{transform:none;opacity:1}
.tl-final{align-items:center}
.tl-final p{grid-column:2;grid-row:1;font-size:1rem;color:var(--muted)}
.tl-final p b{font-weight:500;color:var(--fg)}
@media(min-width:768px){.tl-final p{grid-column:3}}
.integr{margin-top:80px;border-radius:28px;background:#fff;padding:24px;box-shadow:0 0 0 1px rgba(0,0,0,.05)}
@media(min-width:640px){.integr{padding:32px}}
.integr-in{display:flex;flex-direction:column;gap:24px}
@media(min-width:1024px){.integr-in{flex-direction:row;align-items:center;justify-content:space-between}}
.integr .lft{display:flex;align-items:flex-start;gap:16px}
.integr h3{font-size:1rem;font-weight:500}
.integr .lft p{margin-top:4px;font-size:14px;color:var(--muted)}
.tags{display:flex;flex-wrap:wrap;gap:8px}
@media(min-width:1024px){.tags{max-width:36rem;justify-content:flex-end}}
.tags li{border-radius:999px;background:var(--bg);padding:6px 14px;font-size:14px;box-shadow:0 0 0 1px rgba(0,0,0,.05);transition:background .3s,color .3s}
.tags li:hover{background:var(--accent);color:var(--accent-fg)}

/* About */
.about{background:var(--bg);padding-bottom:96px;scroll-margin-top:80px}
@media(min-width:640px){.about{padding-bottom:128px}}
.about-grid{display:grid;align-items:center;gap:48px}
@media(min-width:1024px){.about-grid{grid-template-columns:1fr 1fr;gap:64px}}
.about-art-wrap{position:relative}
.about-art{position:relative;aspect-ratio:4/5;overflow:hidden;border-radius:32px;box-shadow:0 40px 80px -50px rgba(14,26,18,.6)}
@media(min-width:640px){.about-art{aspect-ratio:5/4}}
@media(min-width:1024px){.about-art{aspect-ratio:4/5}}
.js .about-art{clip-path:inset(100% 0 0 0 round 32px);transition:clip-path 1.6s var(--ease)}
.js .about-art.in{clip-path:inset(0 0 0 0 round 32px)}
.about-art .par{position:absolute;inset:-48px 0}
.about-art svg{width:100%;height:100%}
.mission{position:absolute;bottom:20px;left:20px;right:20px;border-radius:18px;background:rgba(255,255,255,.82);padding:20px;box-shadow:0 0 0 1px rgba(255,255,255,.6),0 20px 40px -20px rgba(14,26,18,.4);-webkit-backdrop-filter:blur(20px) saturate(1.4);backdrop-filter:blur(20px) saturate(1.4)}
@media(min-width:640px){.mission{left:auto;width:18rem}}
.mission p:first-child{font-size:12px;font-weight:500;text-transform:uppercase;letter-spacing:.14em;color:var(--muted)}
.mission p:last-child{margin-top:8px;font-size:15px;line-height:1.6}
.about-stats{margin-top:40px;display:grid;grid-template-columns:repeat(3,1fr);gap:16px;border-top:1px solid var(--border);border-bottom:1px solid var(--border);padding:24px 0}
.about-stats div{display:flex;flex-direction:column}
.about-stats dt{margin-top:4px;font-size:12px;color:var(--muted)}
@media(min-width:640px){.about-stats dt{font-size:14px}}
.about-stats dd{order:-1;font-family:var(--ff-serif);font-size:1.6rem;font-weight:500;letter-spacing:-.03em}
@media(min-width:640px){.about-stats dd{font-size:2.25rem}}
.trust{margin-top:32px;display:flex;flex-direction:column;gap:20px}
.trust li{display:flex;gap:16px}
.trust h3{font-size:1rem;font-weight:500}
.trust p{margin-top:4px;font-size:14px;line-height:1.65;color:var(--muted)}

/* FAQ */
.faq{background:#fff;padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.faq{padding:128px 0}}
.faq-grid{display:grid;gap:48px}
@media(min-width:1024px){.faq-grid{grid-template-columns:.9fr 1.1fr;gap:64px}.faq-side{position:sticky;top:112px;align-self:start}}
.textlink{margin-top:32px;display:inline-flex;align-items:center;gap:8px;font-size:14px;font-weight:500;color:var(--primary);transition:color .3s}
.textlink:hover{color:var(--primary-strong)}
.textlink .ic{transition:transform .3s var(--ease)}.textlink:hover .ic{transform:translateX(4px)}
.qa{display:flex;flex-direction:column;gap:12px}
.qa details{border-radius:18px;background:var(--bg);box-shadow:0 0 0 1px rgba(0,0,0,.05);transition:background .3s,box-shadow .3s}
.qa details[open]{background:#fff;box-shadow:0 0 0 1px rgba(0,0,0,.05),0 20px 40px -30px rgba(14,26,18,.45)}
.qa summary{display:flex;cursor:pointer;list-style:none;align-items:center;justify-content:space-between;gap:16px;border-radius:18px;padding:20px;font-weight:500}
@media(min-width:640px){.qa summary{padding:24px}}
.qa summary::-webkit-details-marker{display:none}
.qa .pl{display:flex;width:32px;height:32px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;background:#fff;font-size:16px;box-shadow:0 0 0 1px rgba(0,0,0,.05);transition:transform .35s var(--ease),background .3s,color .3s}
.qa details[open] .pl{transform:rotate(45deg);background:var(--primary);color:#fff}
.qa .ans{margin-top:-4px;padding:0 20px 24px;font-size:15px;line-height:1.65;color:var(--muted)}
@media(min-width:640px){.qa .ans{padding:0 24px 24px}}
.qa details[open] .ans{animation:ansIn .5s var(--ease)}
@keyframes ansIn{from{opacity:0;transform:translateY(-6px)}to{opacity:1;transform:none}}

/* CTA */
.cta{background:var(--bg);padding:96px 0;scroll-margin-top:80px}
@media(min-width:640px){.cta{padding:128px 0}}
.cta-card{position:relative;isolation:isolate;overflow:hidden;border-radius:40px;background:var(--forest);box-shadow:0 50px 100px -60px rgba(11,31,20,.9)}
.cta-card .bg{position:absolute;inset:0;z-index:-2;width:100%;height:100%}
.cta-card::before{content:"";position:absolute;inset:0;z-index:-1;background:linear-gradient(180deg,rgba(11,31,20,.88),rgba(11,31,20,.55) 45%,rgba(11,31,20,.1))}
@media(min-width:1024px){.cta-card::before{background:linear-gradient(180deg,rgba(11,31,20,.9),rgba(11,31,20,.45) 50%,rgba(11,31,20,0) 80%),linear-gradient(90deg,rgba(11,31,20,.5),rgba(11,31,20,0) 50%)}}
.cta-grid{display:grid;gap:40px;padding:24px}
@media(min-width:640px){.cta-grid{padding:40px}}
@media(min-width:1024px){.cta-grid{grid-template-columns:1fr 1.1fr;gap:56px;padding:56px}}
.cta-copy{display:flex;flex-direction:column}
.cta .h2{color:#fff}.cta .lede{color:rgba(223,238,226,.72)}
.checks{margin-top:32px;display:flex;flex-direction:column;gap:12px}
.checks li{display:flex;align-items:center;gap:12px;font-size:15px;color:#fff}
.checks .ck{display:flex;width:24px;height:24px;flex-shrink:0;align-items:center;justify-content:center;border-radius:50%;background:var(--sun);color:var(--forest);font-size:14px}
.cta-note{margin-top:auto;padding-top:40px;font-size:14px;color:rgba(223,238,226,.65)}
.formcard{border-radius:28px;background:#fff;padding:24px;box-shadow:0 40px 80px -40px rgba(0,0,0,.6)}
@media(min-width:640px){.formcard{padding:32px}}
.formcard h3{font-size:1.125rem;font-weight:500}
.formcard .note{margin-top:4px;font-size:14px;color:var(--muted)}
.fgrid{margin-top:24px;display:grid;gap:16px}
@media(min-width:640px){.fgrid{grid-template-columns:1fr 1fr}.span2{grid-column:span 2}}
.field label,.field legend{font-size:14px;font-weight:500}
.field .opt{font-weight:400;color:var(--muted)}
.req{color:var(--primary)}
.inp{margin-top:6px;height:44px;width:100%;border-radius:12px;border:1px solid #dfe3dc;background:#fff;padding:0 14px;font-size:14px;transition:border-color .2s,box-shadow .2s}
.inp::placeholder{color:rgba(92,106,97,.7)}
.inp:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 4px rgba(30,133,56,.15)}
.inp[aria-invalid=true]{border-color:#d9480f}
.inp[aria-invalid=true]:focus{box-shadow:0 0 0 4px rgba(217,72,15,.15)}
textarea.inp{height:auto;resize:vertical;padding:12px 14px;line-height:1.6}
.selwrap{position:relative}
.selwrap select{appearance:none;-webkit-appearance:none;padding-right:40px;color:var(--fg)}
.selwrap select.empty{color:var(--muted)}
.selwrap .ic{position:absolute;right:14px;top:calc(50% + 3px);transform:translateY(-50%);pointer-events:none;color:var(--muted)}
.err{margin-top:6px;font-size:12px;color:#c2410c}
fieldset.field{border:0;margin:0;padding:0}
.pills{margin-top:8px;display:flex;flex-wrap:wrap;gap:8px}
.pills label{cursor:pointer}
.pills input{position:absolute;opacity:0;pointer-events:none}
.pills span{display:inline-flex;height:36px;align-items:center;gap:6px;border-radius:999px;background:var(--bg);padding:0 14px;font-size:14px;box-shadow:0 0 0 1px rgba(0,0,0,.1);transition:background .25s,color .25s,box-shadow .25s}
.pills input:checked+span{background:var(--accent);color:var(--accent-fg);box-shadow:0 0 0 1px rgba(30,133,56,.4)}
.pills input:focus-visible+span{box-shadow:0 0 0 2px var(--primary)}
.pills .ic{display:none;font-size:13px}.pills input:checked+span .ic{display:block}
.fbot{margin-top:24px;display:flex;flex-direction:column;gap:16px}
@media(min-width:640px){.fbot{flex-direction:row;align-items:center;justify-content:space-between}.fbot p{max-width:16rem}}
.fbot p{font-size:12px;line-height:1.6;color:var(--muted)}
.fbot p a{font-weight:500;text-decoration:underline;text-underline-offset:2px}
.success{display:flex;min-height:28rem;flex-direction:column;align-items:center;justify-content:center;text-align:center;animation:ansIn .7s var(--ease)}
.success .big{display:flex;width:64px;height:64px;align-items:center;justify-content:center;border-radius:50%;background:var(--accent);color:var(--primary);font-size:28px;box-shadow:0 0 0 10px rgba(30,133,56,.08)}
.success h3{margin-top:24px;font-family:var(--ff-head);font-size:1.75rem;font-weight:700;letter-spacing:-.02em}
.success p{margin-top:8px;max-width:22rem;color:var(--muted)}

/* Early access + 3D */
.early{overflow:hidden;border-top:1px solid var(--border);background:#fff}
.early-box{position:relative;max-width:72rem;margin:0 auto;border-left:1px solid var(--border);border-right:1px solid var(--border)}
.early-top{padding:80px 16px 56px;text-align:center}
@media(min-width:640px){.early-top{padding:112px 40px 56px}}
.early h2{max-width:56rem;margin:0 auto;font-family:var(--ff-head);font-weight:800;font-size:3rem;line-height:1;letter-spacing:-.045em;color:var(--primary-strong);text-wrap:balance}
@media(min-width:640px){.early h2{font-size:4.5rem}}
@media(min-width:1024px){.early h2{font-size:5.5rem}}
.early-lede{max-width:36rem;margin:28px auto 0;font-size:1rem;line-height:1.65;color:rgba(20,90,39,.85)}
@media(min-width:640px){.early-lede{font-size:1.125rem}}
.ea-form{max-width:36rem;margin:40px auto 0;display:flex;flex-direction:column;gap:12px}
@media(min-width:640px){.ea-form{flex-direction:row}}
.ea-form input{height:48px;flex:1;border-radius:999px;border:1px solid #dfe3dc;padding:0 20px;font-size:15px;transition:border-color .2s,box-shadow .2s}
.ea-form input::placeholder{color:rgba(20,90,39,.5)}
.ea-form input:focus{outline:none;border-color:var(--primary);box-shadow:0 0 0 4px rgba(30,133,56,.15)}
.ea-form input[aria-invalid=true]{border-color:#d9480f}
.ea-msg{margin-top:12px;min-height:20px;font-size:14px;color:var(--primary-strong)}
.early-model{position:relative;border-top:1px solid var(--border);padding:32px 16px 48px}
@media(min-width:640px){.early-model{padding:32px 40px 64px}}
.model-scale{max-width:64rem;margin:0 auto;will-change:transform}
.model{position:relative;aspect-ratio:4/3;width:100%;overflow:hidden;border-radius:32px;cursor:grab;touch-action:pan-y;user-select:none;-webkit-user-select:none;perspective:1500px;perspective-origin:50% 38%;background:linear-gradient(180deg,#dfeaf1 0%,#eef1ec 46%,#e5ead9 47%,#d8e1cb 100%);box-shadow:inset 0 0 0 1px rgba(0,0,0,.05)}
@media(min-width:640px){.model{aspect-ratio:16/9}}
.model.dragging{cursor:grabbing}
.model .sunburst{position:absolute;right:-6%;top:-36%;width:62%;aspect-ratio:1;border-radius:50%;background:radial-gradient(closest-side,rgba(255,214,150,.75),rgba(255,214,150,0));pointer-events:none}
.model .hz{position:absolute;inset:44% 0 auto;height:8%;background:linear-gradient(180deg,rgba(255,255,255,0),rgba(255,255,255,.7),rgba(255,255,255,0));pointer-events:none}
.model .vign{position:absolute;inset:0;background:radial-gradient(120% 90% at 50% 40%,transparent 55%,rgba(14,26,18,.12));pointer-events:none}
.rig{position:absolute;left:50%;top:62%;width:0;height:0;transform-style:preserve-3d;transition:transform 1.1s var(--ease)}
.model.dragging .rig{transition:none}
.rig *{transform-style:preserve-3d}
.shadow3d{position:absolute;width:900px;height:460px;left:-410px;top:-230px;transform:rotateX(90deg);background:radial-gradient(closest-side,rgba(14,26,18,.32),rgba(14,26,18,0));border-radius:50%}
.pad3d{position:absolute;width:880px;height:420px;left:-400px;top:-210px;transform:rotateX(90deg);border-radius:28px;background:linear-gradient(180deg,rgba(255,255,255,.35),rgba(255,255,255,.1)),repeating-linear-gradient(90deg,rgba(14,26,18,.05) 0 1px,transparent 1px 44px),repeating-linear-gradient(0deg,rgba(14,26,18,.05) 0 1px,transparent 1px 44px)}
.array{position:absolute;width:640px;height:270px;left:-320px;top:-135px;transform:translateY(-118px) rotateX(66deg)}
.face{position:absolute;inset:0;display:grid;grid-template-columns:repeat(3,1fr);grid-template-rows:repeat(2,1fr);gap:8px;backface-visibility:hidden;-webkit-backface-visibility:hidden}
.face.back{transform:rotateY(180deg)}
.rig .face,.rig .face *{transform-style:flat}.rig .cab .f,.rig .cab .f *{transform-style:flat}
.pv{position:relative;overflow:hidden;border-radius:6px;background:
  linear-gradient(180deg,rgba(255,255,255,.2),transparent 45%),
  repeating-linear-gradient(90deg,transparent 0 calc(16.666% - 1.5px),rgba(205,222,240,.42) calc(16.666% - 1.5px) 16.666%),
  repeating-linear-gradient(0deg,transparent 0 calc(25% - 1.5px),rgba(205,222,240,.38) calc(25% - 1.5px) 25%),
  repeating-linear-gradient(90deg,transparent 0 calc(5.555% - .6px),rgba(255,255,255,.09) calc(5.555% - .6px) 5.555%),
  linear-gradient(135deg,#3470b0,#1c4072 48%,#0f2747);
  box-shadow:inset 0 0 0 3px #e3e8ec,inset 0 0 0 4px #8f9ba8,inset 0 10px 18px rgba(255,255,255,.12)}
.pv::after{content:"";position:absolute;inset:-40%;background:linear-gradient(115deg,transparent 40%,rgba(255,255,255,.42) 50%,transparent 60%);animation:sheen 6s ease-in-out infinite;transform:translateX(-60%)}
.pv:nth-child(2)::after{animation-delay:.3s}.pv:nth-child(3)::after{animation-delay:.6s}.pv:nth-child(4)::after{animation-delay:.15s}.pv:nth-child(5)::after{animation-delay:.45s}.pv:nth-child(6)::after{animation-delay:.75s}
@keyframes sheen{0%,55%{transform:translateX(-60%)}85%,100%{transform:translateX(60%)}}
.pvb{border-radius:6px;background:linear-gradient(180deg,#dfe3e7,#b9c2ca);box-shadow:inset 0 0 0 3px #a3adb8}
.pvb::before{content:"";display:block;margin:28% 12% 0;height:12%;border-radius:3px;background:linear-gradient(180deg,#5f6a75,#3f4851)}
.rail{position:absolute;height:10px;width:640px;left:-320px;background:linear-gradient(180deg,#b8c1c9,#7d8894)}
.leg{position:absolute;width:10px;background:linear-gradient(90deg,#8f99a4,#d3d9de 50%,#87919c)}
.leg .x{position:absolute;inset:0;transform:rotateY(90deg);background:linear-gradient(90deg,#87919c,#bdc5cc)}
.cab{position:absolute;left:380px;top:-150px;width:90px;height:150px}
.cab .f{position:absolute;backface-visibility:hidden;-webkit-backface-visibility:hidden}
.cab .fr{left:0;top:0;width:90px;height:150px;border-radius:12px;transform:translateZ(25px);background:linear-gradient(160deg,#ffffff,#e4e8eb 60%,#d4dade)}
.cab .bk{left:0;top:0;width:90px;height:150px;border-radius:12px;transform:rotateY(180deg) translateZ(25px);background:linear-gradient(160deg,#e3e7ea,#c6cdd2)}
.cab .rt{left:20px;top:0;width:50px;height:150px;border-radius:8px;transform:rotateY(90deg) translateZ(45px);background:linear-gradient(180deg,#d6dce0,#bcc4ca)}
.cab .lf{left:20px;top:0;width:50px;height:150px;border-radius:8px;transform:rotateY(-90deg) translateZ(45px);background:linear-gradient(180deg,#e6eaed,#cbd2d7)}
.cab .tp{left:0;top:50px;width:90px;height:50px;border-radius:10px;transform:rotateX(90deg) translateZ(75px);background:linear-gradient(180deg,#f7f9fa,#e3e7ea)}
.cab .led{position:absolute;left:41px;top:28px;width:8px;height:78px;border-radius:4px;background:linear-gradient(180deg,#8ff0a0,#3fb85a);box-shadow:0 0 14px 3px rgba(87,199,106,.75);animation:ledp 2.6s ease-in-out infinite}
@keyframes ledp{50%{box-shadow:0 0 6px 1px rgba(87,199,106,.5);opacity:.75}}
.cab .mk{position:absolute;left:33px;bottom:16px;width:24px;height:24px}
.trench{position:absolute;left:318px;top:-4px;width:64px;height:8px;transform:rotateX(90deg);background:linear-gradient(90deg,#6b7480,#9aa4ae);border-radius:4px}
.drag-hint{position:absolute;left:50%;top:12px;transform:translateX(-50%);display:inline-flex;align-items:center;gap:8px;border-radius:999px;background:rgba(255,255,255,.85);padding:6px 14px;font-size:12px;font-weight:500;color:var(--primary-strong);box-shadow:0 0 0 1px rgba(0,0,0,.05),0 8px 24px -12px rgba(14,26,18,.35);-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px);pointer-events:none;transition:opacity .5s}
@media(min-width:640px){.drag-hint{top:20px}}
.drag-hint .ic{font-size:16px}
.mtag{position:absolute;display:flex;align-items:center;gap:8px;border-radius:12px;background:rgba(255,255,255,.82);padding:8px 12px;font-size:12px;box-shadow:0 0 0 1px rgba(255,255,255,.7),0 14px 30px -18px rgba(14,26,18,.45);-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px);pointer-events:none}
.mtag b{font-family:var(--ff-head);font-size:15px;font-weight:500}
.mtag span{color:var(--muted)}
.mtag i{width:8px;height:8px;border-radius:50%}
.mtag.a{left:16px;bottom:16px}.mtag.b{right:16px;bottom:16px}
@media(max-width:639px){.mtag{display:none}}
.views{margin-top:24px;display:flex;flex-direction:column;align-items:center;gap:16px}
.vbtns{display:inline-flex;border-radius:999px;background:var(--mist);padding:4px;box-shadow:0 0 0 1px rgba(0,0,0,.05)}
.vbtns button{height:36px;border-radius:999px;padding:0 16px;font-size:14px;font-weight:500;color:rgba(20,90,39,.7);transition:background .3s,color .3s}
@media(min-width:640px){.vbtns button{padding:0 20px}}
.vbtns button:hover{color:var(--primary-strong)}
.vbtns button[aria-pressed=true]{background:var(--primary-strong);color:#fff;box-shadow:0 1px 2px rgba(0,0,0,.1)}
.vcap{min-height:2.75rem;max-width:30rem;text-align:center;font-size:14px;line-height:1.6;color:rgba(20,90,39,.75);text-wrap:balance;transition:opacity .3s}

/* Footer */
footer{position:relative;overflow:hidden;background:var(--forest);color:var(--forest-fg)}
footer::before{content:"";position:absolute;width:70vmax;height:40vmax;left:50%;bottom:-20vmax;transform:translateX(-50%);border-radius:50%;background:radial-gradient(closest-side,rgba(244,178,63,.16),transparent);pointer-events:none}
.foot{position:relative;padding:80px 16px 40px;max-width:80rem;margin:0 auto}
@media(min-width:640px){.foot{padding:80px 24px 40px}}
@media(min-width:1024px){.foot{padding:80px 32px 40px}}
.foot-grid{display:grid;gap:48px}
@media(min-width:1024px){.foot-grid{grid-template-columns:1.3fr 2fr}}
.foot-brand{max-width:24rem}
.foot-brand>p{margin-top:20px;font-size:15px;line-height:1.65;color:rgba(223,238,226,.7)}
.foot-brand .btn{margin-top:28px}
.foot-cols{display:grid;grid-template-columns:1fr 1fr;gap:40px}
@media(min-width:640px){.foot-cols{grid-template-columns:repeat(3,1fr)}}
.foot-cols h2{font-size:14px;font-weight:600;color:#fff}
.foot-cols ul{margin-top:16px;display:flex;flex-direction:column;gap:12px}
.foot-cols a{font-size:14px;color:rgba(223,238,226,.65);transition:color .3s}
.foot-cols a:hover{color:#fff}
.foot-bot{margin-top:64px;display:flex;flex-direction:column;gap:12px;border-top:1px solid rgba(255,255,255,.1);padding-top:24px;font-size:14px;color:rgba(223,238,226,.55)}
@media(min-width:640px){.foot-bot{flex-direction:row;align-items:center;justify-content:space-between}}
.wordmark{position:relative;display:flex;justify-content:center;overflow:hidden;padding:0 8px;font-family:var(--ff-head);font-size:23vw;font-weight:800;line-height:.78;letter-spacing:-.07em;user-select:none;pointer-events:none}
.wordmark span{display:inline-block;background:linear-gradient(180deg,rgba(244,178,63,.42),rgba(87,199,106,.14) 55%,rgba(87,199,106,.02));-webkit-background-clip:text;background-clip:text;color:transparent}
.js .wordmark span{opacity:0;transform:translateY(100%);transition:opacity 1s var(--ease),transform 1.2s var(--ease);transition-delay:calc(var(--i) * 70ms)}
.js .wordmark.in span{opacity:1;transform:none}

@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.001ms!important;animation-iteration-count:1!important;transition-duration:.001ms!important;scroll-behavior:auto!important}
}
</style>
</head>
<body>
<svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
  <defs>
    <linearGradient id="gActual" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#1e8538" stop-opacity=".16"/><stop offset="1" stop-color="#1e8538" stop-opacity="0"/></linearGradient>
    <linearGradient id="gSolarFill" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f4b23f" stop-opacity=".42"/><stop offset="1" stop-color="#f4b23f" stop-opacity=".02"/></linearGradient>
  </defs>
  <symbol id="logo-mark" viewBox="0 0 32 32"><defs><linearGradient id="lgBg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#1e8538"/><stop offset="1" stop-color="#0f4a20"/></linearGradient><linearGradient id="lgSun" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffd27a"/><stop offset="1" stop-color="#f09a2a"/></linearGradient></defs><rect width="32" height="32" rx="9" fill="url(#lgBg)"/><path d="M8 17a8 8 0 0 1 16 0z" fill="url(#lgSun)"/><rect x="8" y="20" width="16" height="2.4" rx="1.2" fill="#57c76a"/><rect x="11" y="24" width="10" height="2.4" rx="1.2" fill="#57c76a" opacity=".7"/></symbol>
  <symbol id="i-chevr" viewBox="0 0 24 24"><path d="m9 18 6-6-6-6"/></symbol>
  <symbol id="i-star" viewBox="0 0 24 24"><path d="M12 2.5l2.9 6.4 7 .7-5.3 4.7 1.5 6.9L12 17.6l-6.1 3.6 1.5-6.9L2.1 9.6l7-.7z"/></symbol>
  <symbol id="i-arrow" viewBox="0 0 24 24"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></symbol>
  <symbol id="i-arrow-ur" viewBox="0 0 24 24"><path d="M7 7h10v10"/><path d="M7 17 17 7"/></symbol>
  <symbol id="i-menu" viewBox="0 0 24 24"><path d="M4 12h16M4 6h16M4 18h16"/></symbol>
  <symbol id="i-x" viewBox="0 0 24 24"><path d="M18 6 6 18"/><path d="m6 6 12 12"/></symbol>
  <symbol id="i-sun" viewBox="0 0 24 24"><circle cx="12" cy="12" r="4"/><path d="M12 2v2M12 20v2m-7.07-17.07 1.41 1.41m11.32 11.32 1.41 1.41M2 12h2m16 0h2M6.34 17.66l-1.41 1.41M19.07 4.93l-1.41 1.41"/></symbol>
  <symbol id="i-moon" viewBox="0 0 24 24"><path d="M12 3a6 6 0 0 0 9 9 9 9 0 1 1-9-9Z"/></symbol>
  <symbol id="i-home" viewBox="0 0 24 24"><path d="M15 21v-8a1 1 0 0 0-1-1h-4a1 1 0 0 0-1 1v8"/><path d="M3 10a2 2 0 0 1 .709-1.528l7-5.999a2 2 0 0 1 2.582 0l7 5.999A2 2 0 0 1 21 10v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/></symbol>
  <symbol id="i-zap" viewBox="0 0 24 24"><path d="M4 14a1 1 0 0 1-.78-1.63l9.9-10.2a.5.5 0 0 1 .86.46l-1.92 6.02A1 1 0 0 0 13 10h7a1 1 0 0 1 .78 1.63l-9.9 10.2a.5.5 0 0 1-.86-.46l1.92-6.02A1 1 0 0 0 11 14z"/></symbol>
  <symbol id="i-plug" viewBox="0 0 24 24"><path d="M12 22v-5"/><path d="M9 8V2"/><path d="M15 8V2"/><path d="M18 8v5a4 4 0 0 1-4 4h-4a4 4 0 0 1-4-4V8Z"/></symbol>
  <symbol id="i-storm" viewBox="0 0 24 24"><path d="M6 16.326A7 7 0 1 1 15.71 8h1.79a4.5 4.5 0 0 1 .5 8.973"/><path d="m13 12-3 5h4l-3 5"/></symbol>
  <symbol id="i-thermo" viewBox="0 0 24 24"><path d="M14 4v10.54a4 4 0 1 1-4 0V4a2 2 0 0 1 4 0Z"/></symbol>
  <symbol id="i-dollar" viewBox="0 0 24 24"><path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"/></symbol>
  <symbol id="i-wifi" viewBox="0 0 24 24"><path d="M12 20h.01M2 8.82a15 15 0 0 1 20 0M5 12.86a10 10 0 0 1 14 0M8.5 16.43a5 5 0 0 1 7 0"/></symbol>
  <symbol id="i-waves" viewBox="0 0 24 24"><path d="M2 6c.6.5 1.2 1 2.5 1C7 7 7 5 9.5 5c2.6 0 2.4 2 5 2 2.5 0 2.5-2 5-2 1.3 0 1.9.5 2.5 1"/><path d="M2 12c.6.5 1.2 1 2.5 1 2.5 0 2.5-2 5-2 2.6 0 2.4 2 5 2 2.5 0 2.5-2 5-2 1.3 0 1.9.5 2.5 1"/><path d="M2 18c.6.5 1.2 1 2.5 1 2.5 0 2.5-2 5-2 2.6 0 2.4 2 5 2 2.5 0 2.5-2 5-2 1.3 0 1.9.5 2.5 1"/></symbol>
  <symbol id="i-mountain" viewBox="0 0 24 24"><path d="m8 3 4 8 5-5 5 15H2L8 3z"/></symbol>
  <symbol id="i-battery" viewBox="0 0 24 24"><rect width="16" height="10" x="2" y="7" rx="2"/><path d="M22 11v2M6 11v2m4-2v2m4-2v2"/></symbol>
  <symbol id="i-grid" viewBox="0 0 24 24"><rect width="7" height="7" x="3" y="3" rx="1"/><rect width="7" height="7" x="14" y="3" rx="1"/><rect width="7" height="7" x="14" y="14" rx="1"/><rect width="7" height="7" x="3" y="14" rx="1"/></symbol>
  <symbol id="i-chart" viewBox="0 0 24 24"><path d="M3 3v16a2 2 0 0 0 2 2h16"/><path d="m19 9-5 5-4-4-3 3"/></symbol>
  <symbol id="i-chartcol" viewBox="0 0 24 24"><path d="M3 3v16a2 2 0 0 0 2 2h16"/><path d="M18 17V9M13 17V5M8 17v-3"/></symbol>
  <symbol id="i-charging" viewBox="0 0 24 24"><path d="M15 7h1a2 2 0 0 1 2 2v6a2 2 0 0 1-2 2h-2"/><path d="M6 7H4a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2h1"/><path d="m11 7-3 5h4l-3 5"/><path d="M22 11v2"/></symbol>
  <symbol id="i-bell" viewBox="0 0 24 24"><path d="M6 8a6 6 0 0 1 12 0c0 7 3 9 3 9H3s3-2 3-9"/><path d="M10.3 21a1.94 1.94 0 0 0 3.4 0"/></symbol>
  <symbol id="i-settings" viewBox="0 0 24 24"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 1 1-4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06A1.65 1.65 0 0 0 4.6 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 1 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06A1.65 1.65 0 0 0 9 4.6a1.65 1.65 0 0 0 1-1.51V3a2 2 0 1 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 1 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></symbol>
  <symbol id="i-up" viewBox="0 0 24 24"><path d="M22 7 13.5 15.5 8.5 10.5 2 17"/><path d="M16 7h6v6"/></symbol>
  <symbol id="i-down" viewBox="0 0 24 24"><path d="M22 17 13.5 8.5 8.5 13.5 2 7"/><path d="M16 17h6v-6"/></symbol>
  <symbol id="i-refresh" viewBox="0 0 24 24"><path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8"/><path d="M21 3v5h-5"/><path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16"/><path d="M8 16H3v5"/></symbol>
  <symbol id="i-users" viewBox="0 0 24 24"><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M22 21v-2a4 4 0 0 0-3-3.87M16 3.13a4 4 0 0 1 0 7.75"/></symbol>
  <symbol id="i-shield" viewBox="0 0 24 24"><path d="M20 13c0 5-3.5 7.5-7.66 8.95a1 1 0 0 1-.67-.01C7.5 20.5 4 18 4 13V6a1 1 0 0 1 1-1c2 0 4.5-1.2 6.24-2.72a1.17 1.17 0 0 1 1.52 0C14.51 3.81 17 5 19 5a1 1 0 0 1 1 1z"/><path d="m9 12 2 2 4-4"/></symbol>
  <symbol id="i-repeat" viewBox="0 0 24 24"><path d="m17 2 4 4-4 4"/><path d="M3 11v-1a4 4 0 0 1 4-4h14"/><path d="m7 22-4-4 4-4"/><path d="M21 13v1a4 4 0 0 1-4 4H3"/></symbol>
  <symbol id="i-heart" viewBox="0 0 24 24"><path d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"/><path d="M3.22 12H9.5l.5-1 2 4.5 2-7 1.5 3.5h5.27"/></symbol>
  <symbol id="i-file" viewBox="0 0 24 24"><path d="M4 22h14a2 2 0 0 0 2-2V7l-5-5H6a2 2 0 0 0-2 2v4"/><path d="M14 2v4a2 2 0 0 0 2 2h4"/><path d="m3 15 2 2 4-4"/></symbol>
  <symbol id="i-quote" viewBox="0 0 24 24"><path d="M16 3a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2 1 1 0 0 1 1 1v1a2 2 0 0 1-2 2 1 1 0 0 0-1 1v2a1 1 0 0 0 1 1 6 6 0 0 0 6-6V5a2 2 0 0 0-2-2z"/><path d="M5 3a2 2 0 0 0-2 2v6a2 2 0 0 0 2 2 1 1 0 0 1 1 1v1a2 2 0 0 1-2 2 1 1 0 0 0-1 1v2a1 1 0 0 0 1 1 6 6 0 0 0 6-6V5a2 2 0 0 0-2-2z"/></symbol>
  <symbol id="i-check" viewBox="0 0 24 24"><path d="M20 6 9 17l-5-5"/></symbol>
  <symbol id="i-lock" viewBox="0 0 24 24"><rect width="18" height="11" x="3" y="11" rx="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></symbol>
  <symbol id="i-plus" viewBox="0 0 24 24"><path d="M5 12h14M12 5v14"/></symbol>
  <symbol id="i-chev" viewBox="0 0 24 24"><path d="m6 9 6 6 6-6"/></symbol>
  <symbol id="i-move" viewBox="0 0 24 24"><path d="M5 3v16h16"/><path d="m5 19 6-6"/><path d="m2 6 3-3 3 3"/><path d="m18 16 3 3-3 3"/></symbol>
</svg>

<div class="curtain" id="curtain" aria-hidden="true">
  <div class="curtain-inner"><svg width="42" height="42"><use href="#logo-mark"/></svg><span>Lumora</span></div>
  <span class="curtain-bar"></span>
</div>
<div class="progress" id="progress" aria-hidden="true"></div>
<a href="#main" class="sr-only">Skip to content</a>

<header class="site-header" id="header" data-section="nav">
  <nav class="nav" aria-label="Main">
    <a href="#hero" class="logo" aria-label="Lumora home"><svg aria-hidden="true"><use href="#logo-mark"/></svg><span class="logo-word">Lumora</span></a>
    <ul class="nav-links">
      <li><a class="nav-link" href="#product">The app</a></li>
      <li><a class="nav-link" href="#solutions">How it saves</a></li>
      <li><a class="nav-link" href="#insights">Results</a></li>
      <li><a class="nav-link" href="#about">About</a></li>
    </ul>
    <span class="nav-rule" aria-hidden="true"></span>
    <div class="nav-cta">
      <a class="btn btn-primary btn-head hide-sm" href="#get-started">Get an estimate <svg class="ic"><use href="#i-arrow"/></svg></a>
      <button class="menu-btn" id="menuBtn" type="button" aria-expanded="false" aria-controls="mobileMenu" aria-label="Open menu"><svg class="ic"><use href="#i-menu"/></svg></button>
    </div>
  </nav>
  <div class="mobile-menu" id="mobileMenu" hidden>
    <a class="mm" href="#product">The app <svg class="ic"><use href="#i-arrow"/></svg></a>
    <a class="mm" href="#solutions">How it saves <svg class="ic"><use href="#i-arrow"/></svg></a>
    <a class="mm" href="#insights">Results <svg class="ic"><use href="#i-arrow"/></svg></a>
    <a class="mm" href="#about">About <svg class="ic"><use href="#i-arrow"/></svg></a>
    <a class="btn btn-green btn-lg" href="#get-started">Get a free estimate</a>
  </div>
</header>

<main id="main">
<!-- ================= HERO ================= -->
<section id="hero" class="hero" data-section="hero" aria-labelledby="hero-title">
  <div class="hero-sticky" id="heroSticky">
    <div class="hero-scene" id="heroScene" aria-hidden="true">
      <div class="scene-layers" id="sceneLayers"><svg class="scene-svg" id="sceneSvg" viewBox="0 0 1780 884" preserveAspectRatio="none">
        <defs>
          <linearGradient id="gSky" gradientUnits="userSpaceOnUse" x1="0" y1="-700" x2="0" y2="720"><stop offset="0" stop-color="#dfe0da"/><stop offset=".42" stop-color="#ebe1cf"/><stop offset=".62" stop-color="#f3d7b2"/><stop offset=".8" stop-color="#f7c892"/><stop offset=".92" stop-color="#f1bc84"/><stop offset="1" stop-color="#e7ad79"/></linearGradient>
          <radialGradient id="gWarm" gradientUnits="userSpaceOnUse" cx="1015" cy="382" r="950"><stop offset="0" stop-color="#ffdca4" stop-opacity=".6"/><stop offset=".45" stop-color="#ffd09a" stop-opacity=".18"/><stop offset="1" stop-color="#ffd09a" stop-opacity="0"/></radialGradient>
          <linearGradient id="gSkyN" gradientUnits="userSpaceOnUse" x1="0" y1="-700" x2="0" y2="720"><stop offset="0" stop-color="#02050c"/><stop offset=".5" stop-color="#0a1426"/><stop offset=".78" stop-color="#18284a"/><stop offset=".92" stop-color="#2e3352"/><stop offset="1" stop-color="#463e58"/></linearGradient>
          <radialGradient id="gBloom"><stop offset="0" stop-color="#fff7de"/><stop offset=".07" stop-color="#ffe9b6" stop-opacity=".9"/><stop offset=".2" stop-color="#ffd896" stop-opacity=".38"/><stop offset=".5" stop-color="#ffcc88" stop-opacity=".1"/><stop offset="1" stop-color="#ffcc88" stop-opacity="0"/></radialGradient>
          <radialGradient id="gSunCore"><stop offset="0" stop-color="#fffefa"/><stop offset=".7" stop-color="#fff5da"/><stop offset="1" stop-color="#ffe6b0"/></radialGradient>
          <linearGradient id="gRay" x1="0" x2="1"><stop offset="0" stop-color="#fff2d0" stop-opacity=".55"/><stop offset="1" stop-color="#fff2d0" stop-opacity="0"/></linearGradient>
          <radialGradient id="gMoonGlow"><stop offset="0" stop-color="#d6e2f7" stop-opacity=".5"/><stop offset=".3" stop-color="#d6e2f7" stop-opacity=".12"/><stop offset="1" stop-color="#d6e2f7" stop-opacity="0"/></radialGradient>
          <linearGradient id="gHz" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fbe6c8" stop-opacity="0"/><stop offset=".5" stop-color="#fbe6c8" stop-opacity=".62"/><stop offset="1" stop-color="#fbe6c8" stop-opacity="0"/></linearGradient>
          <linearGradient id="gMtnFar" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f0d7ba"/><stop offset="1" stop-color="#e6c6a3"/></linearGradient>
          <linearGradient id="gMtn2" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#dfbf9c"/><stop offset="1" stop-color="#cca985"/></linearGradient>
          <linearGradient id="gMtnR" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#d8c0ae"/><stop offset="1" stop-color="#c3a690"/></linearGradient>
          <linearGradient id="gSlope" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#959868"/><stop offset="1" stop-color="#5d673f"/></linearGradient>
          <linearGradient id="gMeadow" gradientUnits="userSpaceOnUse" x1="0" y1="700" x2="0" y2="920"><stop offset="0" stop-color="#bba56b"/><stop offset=".45" stop-color="#857f48"/><stop offset="1" stop-color="#4f5630"/></linearGradient>
          <linearGradient id="gCyp2" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#c2a865"/><stop offset=".16" stop-color="#727e46"/><stop offset=".6" stop-color="#3f4d2b"/><stop offset="1" stop-color="#29351d"/></linearGradient>
          <radialGradient id="gOlive" cx=".32" cy=".28" r=".8"><stop offset="0" stop-color="#d2cf9f"/><stop offset=".45" stop-color="#959d6c"/><stop offset="1" stop-color="#5a6642"/></radialGradient>
          <radialGradient id="gShrub" cx=".35" cy=".3" r=".8"><stop offset="0" stop-color="#b3b574"/><stop offset=".55" stop-color="#727e45"/><stop offset="1" stop-color="#434f2c"/></radialGradient>
          <linearGradient id="gConc" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f5ebdb"/><stop offset="1" stop-color="#e0cdb5"/></linearGradient>
          <linearGradient id="gConcS" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#d9c6ad"/><stop offset="1" stop-color="#c2ab8e"/></linearGradient>
          <pattern id="pTimber" width="12" height="400" patternUnits="userSpaceOnUse"><rect width="12" height="400" fill="#ad7244"/><rect x="10" width="2" height="400" fill="#774828"/><rect x="3" width="1.2" height="400" fill="#d29a64" opacity=".6"/><rect x="6.5" width=".6" height="400" fill="#8f5d38" opacity=".5"/></pattern>
          <linearGradient id="gTimShade" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#1a0f06" stop-opacity=".45"/><stop offset=".35" stop-color="#1a0f06" stop-opacity=".05"/><stop offset="1" stop-color="#1a0f06" stop-opacity=".15"/></linearGradient>
          <linearGradient id="gRoof2" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#4a443e"/><stop offset="1" stop-color="#25221e"/></linearGradient>
          <linearGradient id="gPv2" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#5a8dc4"/><stop offset=".45" stop-color="#245283"/><stop offset="1" stop-color="#132c4d"/></linearGradient>
          <radialGradient id="gGlare"><stop offset="0" stop-color="#fff5d6" stop-opacity=".95"/><stop offset=".35" stop-color="#ffd590" stop-opacity=".45"/><stop offset="1" stop-color="#ffd590" stop-opacity="0"/></radialGradient>
          <linearGradient id="gInt" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fff1cf"/><stop offset=".45" stop-color="#ffd897"/><stop offset="1" stop-color="#efa85e"/></linearGradient>
          <linearGradient id="gGlassSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fff" stop-opacity=".28"/><stop offset=".5" stop-color="#fff" stop-opacity="0"/></linearGradient>
          <linearGradient id="gEave" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2a1d12" stop-opacity=".35"/><stop offset="1" stop-color="#2a1d12" stop-opacity="0"/></linearGradient>
          <linearGradient id="gStone" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ddd0b8"/><stop offset="1" stop-color="#bfae90"/></linearGradient>
          <linearGradient id="gPaver" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f1e8d6"/><stop offset="1" stop-color="#d6c7ad"/></linearGradient>
          <radialGradient id="gPool"><stop offset="0" stop-color="#ffcd7d" stop-opacity=".62"/><stop offset="1" stop-color="#ffcd7d" stop-opacity="0"/></radialGradient>
          <linearGradient id="gLeaf" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#7f8d45"/><stop offset="1" stop-color="#3a4722"/></linearGradient>
          <linearGradient id="gShoot" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#fff" stop-opacity="0"/><stop offset="1" stop-color="#fff"/></linearGradient>
          <filter id="fGlow" x="-100%" y="-100%" width="300%" height="300%"><feGaussianBlur stdDeviation="4" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter>
          <filter id="fBig" x="-60%" y="-60%" width="220%" height="220%"><feGaussianBlur stdDeviation="22"/></filter>
          <filter id="fSoft" x="-30%" y="-150%" width="160%" height="400%"><feGaussianBlur stdDeviation="9"/></filter>
          <filter id="fDof" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="5"/></filter>
          <filter id="fShadow" x="-30%" y="-200%" width="160%" height="500%"><feGaussianBlur stdDeviation="14"/></filter>
          <clipPath id="roofQ"><polygon points="1186,300 1352,328 1236,450 1076,414"/></clipPath>
          <clipPath id="glassClip"><polygon points="1352,356 1262,448 1262,606 1456,606 1456,446"/><rect x="1538" y="428" width="168" height="84"/><rect x="1538" y="522" width="168" height="88"/><rect x="978" y="542" width="258" height="68"/><rect x="1500" y="642" width="272" height="70"/></clipPath>
          <mask id="moonMask" maskUnits="userSpaceOnUse" x="-40" y="-40" width="80" height="80"><rect x="-40" y="-40" width="80" height="80" fill="#fff"/><circle cx="12" cy="-9" r="25" fill="#000"/></mask>
        </defs>

        <rect x="-400" y="-1800" width="2600" height="3000" fill="url(#gSky)"/>
        <circle class="day-only" cx="1015" cy="382" r="950" fill="url(#gWarm)"/>
        <rect class="night-only" x="-400" y="-1800" width="2600" height="3000" fill="url(#gSkyN)"/>
        <g class="day-only"><g class="sun-move"><g transform="translate(1015 382)"><g id="rays"></g><circle r="560" fill="url(#gBloom)"/><circle r="34" fill="url(#gSunCore)"/></g></g></g>
        <g class="day-only" id="clouds" filter="url(#fSoft)"></g>

        <g id="mist" class="day-only" filter="url(#fBig)"></g>
        <g id="mistN" class="night-only" filter="url(#fBig)"></g>
        <rect class="night-tint" x="-400" y="-1800" width="2600" height="3600" fill="#283a62"/>
        <g class="night-only">
          <g id="stars" fill="#fff"></g>
          <g transform="translate(300 -40)"><line class="shoot" x1="0" y1="0" x2="130" y2="44" stroke="url(#gShoot)" stroke-width="2" stroke-linecap="round"/></g>
          <g class="moon-move"><g transform="translate(1210 150)"><circle r="260" fill="url(#gMoonGlow)"/><circle r="30" fill="#f1f4f9" mask="url(#moonMask)"/><circle cx="-12" cy="6" r="4" fill="#dfe5ee" mask="url(#moonMask)"/><circle cx="-4" cy="-14" r="3" fill="#dfe5ee" mask="url(#moonMask)"/></g></g>
        </g>
      </svg>
      <div class="villa-layer" id="villaLayer"><div class="villa-pos"><div class="villa" id="villa"></div></div><div class="sun-haze day-only"></div></div>
      </div>
      <div class="hero-wash d"></div><div class="hero-wash n"></div>
      <div class="scene-shade" id="heroShade"></div>
    </div>

    <div class="hero-ui" id="heroUI">
      <div class="hero-stage" id="heroStage">
        <svg class="hs-arc fade-in" width="1780" height="884" viewBox="0 0 1780 884" aria-hidden="true">
          <defs><linearGradient id="arcG" gradientUnits="userSpaceOnUse" x1="1010" y1="372" x2="1592" y2="296"><stop offset="0" stop-color="#fff6d6" stop-opacity="0"/><stop offset=".18" stop-color="#fff2c6" stop-opacity=".95"/><stop offset=".85" stop-color="#ffe9b6" stop-opacity=".85"/><stop offset="1" stop-color="#fff" stop-opacity=".25"/></linearGradient></defs>
          <path d="M1012 370 C 1068 196 1318 116 1470 166 C 1540 190 1574 236 1590 294" fill="none" stroke="url(#arcG)" stroke-width="8" opacity=".5" style="filter:blur(5px)"/>
          <path d="M1012 370 C 1068 196 1318 116 1470 166 C 1540 190 1574 236 1590 294" fill="none" stroke="url(#arcG)" stroke-width="1.6"/>
          <path d="M1591 410 C 1592 430 1592 450 1590 476" fill="none" stroke="#fff4d6" stroke-opacity=".75" stroke-width="1.5"/>
          <circle r="4" fill="#fff8e1" style="filter:drop-shadow(0 0 6px #ffd56b)"><animateMotion dur="3.8s" repeatCount="indefinite" path="M1012 370 C 1068 196 1318 116 1470 166 C 1540 190 1574 236 1590 294"/></circle>
        </svg>

        <div class="hs-text">
          <a href="#product" class="hs-pill hero-in"><b>NEW</b>The AI that runs your home’s solar and battery<svg class="ic"><use href="#i-chevr"/></svg></a>
          <h1 id="hero-title" class="hs-h1"><span class="a split" data-split>Sun by day.</span><span class="b split" data-split data-delay="3">Storage by night.</span></h1>
          <p class="hs-p hero-in" id="heroCap" aria-live="polite">Lumora forecasts tomorrow’s sunshine for your roof and fills your battery from the panels, not the grid.</p>
          <div class="hs-btns hero-in"><a class="hbtn pri" href="#get-started">Get an estimate <svg class="ic"><use href="#i-arrow"/></svg></a><a class="hbtn sec" href="#solutions"><span class="play" aria-hidden="true"></span>See how it works</a></div>
          <div class="hs-proof hero-in">
            <div class="avs" aria-hidden="true"><span style="background:linear-gradient(135deg,#d39a6c,#8d5235)">AR</span><span style="background:linear-gradient(135deg,#7e9fc4,#3d5f87)">MK</span><span style="background:linear-gradient(135deg,#86ad74,#3e6a3a)">JL</span></div>
            <div><p class="proof-t">Trusted by 10,000+ homeowners</p><p class="stars" role="img" aria-label="Rated 4.9 out of 5"><svg viewBox="0 0 24 24"><use href="#i-star"/></svg><svg viewBox="0 0 24 24"><use href="#i-star"/></svg><svg viewBox="0 0 24 24"><use href="#i-star"/></svg><svg viewBox="0 0 24 24"><use href="#i-star"/></svg><svg viewBox="0 0 24 24"><use href="#i-star"/></svg><b>4.9/5</b></p></div>
          </div>
        </div>

        <div class="hs-chip solar fade-in" aria-hidden="true">
          <span class="hc-ic sun"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="5" fill="#fff"/><path d="M12 1.6v2.6M12 19.8v2.6M1.6 12h2.6M19.8 12h2.6M4.6 4.6l1.8 1.8M17.6 17.6l1.8 1.8M4.6 19.4l1.8-1.8M17.6 6.4l1.8-1.8" stroke="#fff" stroke-width="2.2" stroke-linecap="round"/></svg></span>
          <span><span class="hc-l">SOLAR NOW</span><b class="hc-v" id="cSolar">5.0 kW</b></span>
          <span class="hc-bars" id="bSolar" style="--c1:#eef2a8;--c2:#8bcd6a"></span>
        </div>
        <div class="hs-chip home fade-in" aria-hidden="true">
          <span class="hc-ic home"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linejoin="round" stroke-linecap="round"><path d="M3 10.5 12 3l9 7.5V20a1 1 0 0 1-1 1h-5v-6h-6v6H4a1 1 0 0 1-1-1z"/></svg></span>
          <span><span class="hc-l">HOME USE</span><b class="hc-v" id="cHome">1.1 kW</b></span>
          <span class="hc-bars" id="bHome" style="--c1:#b5d6f5;--c2:#3f86d4"></span>
        </div>
        <div class="hs-chip batt fade-in" aria-hidden="true">
          <div class="row1"><span class="hc-ic bat"><svg viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="6.5" y="5" width="11" height="16" rx="2.5"/><path d="M10 2.6h4"/><path d="M9.5 15.5h5M9.5 12h5" opacity=".9"/></svg></span><span><span class="hc-l">BATTERY</span><b class="hc-v" id="cBatt">71% · +2.7 kW</b></span></div>
          <span class="hc-bars" id="bBatt" style="--c1:#d3f0b6;--c2:#36a656"></span>
        </div>

        <div class="hs-tod hero-in" role="group" aria-label="Time of day">
          <span class="tod-ind" aria-hidden="true"><i></i></span>
          <button type="button" class="tseg m" data-tod="day" aria-pressed="true">
            <span class="tb"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="4.4" fill="currentColor"/><path d="M12 2.2v2.3M12 19.5v2.3M2.2 12h2.3M19.5 12h2.3M5.1 5.1l1.6 1.6M17.3 17.3l1.6 1.6M5.1 18.9l1.6-1.6M17.3 6.7l1.6-1.6" stroke="currentColor" stroke-width="1.9" stroke-linecap="round"/></svg></span>
            <span class="tx"><span class="tt">Morning</span><span class="ts">Roof charges the battery</span></span>
          </button>
          <button type="button" class="tseg e" data-tod="night" aria-pressed="false">
            <span class="tb"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linejoin="round"><path d="M12.5 3.2a6.6 6.6 0 0 0 8.3 8.3A8.8 8.8 0 1 1 12.5 3.2Z"/></svg></span>
            <span class="tx"><span class="tt">Evening</span><span class="ts">Battery runs your home</span></span>
          </button>
        </div>
      </div>
    </div>
    <p class="hero-tag" id="heroTag" aria-hidden="true">Every kilowatt-hour, put to work.</p>
  </div>
</section>

<!-- ================= PARTNERS ================= -->
<section class="customers" data-section="partners" aria-labelledby="customers-title">
  <div class="container"><h2 id="customers-title" class="reveal">Trusted by 10,000+ homeowners, installed by local solar pros</h2></div>
  <div class="marquee">
    <div class="marquee-track" id="marquee">
      <ul>
        <li><svg class="ic"><use href="#i-sun"/></svg><span>Brightside Solar</span></li>
        <li><svg class="ic"><use href="#i-zap"/></svg><span>Northgate Electric</span></li>
        <li><svg class="ic"><use href="#i-home"/></svg><span>Sunward Homes</span></li>
        <li><svg class="ic"><use href="#i-waves"/></svg><span>Harbor &amp; Pine</span></li>
        <li><svg class="ic"><use href="#i-mountain"/></svg><span>Clearsky Installers</span></li>
        <li><svg class="ic"><use href="#i-battery"/></svg><span>Meadowline Power</span></li>
      </ul>
    </div>
  </div>
</section>

<!-- ================= MANIFESTO ================= -->
<section id="manifesto" class="manifesto" data-section="manifesto" aria-labelledby="manifesto-title">
  <div class="manifesto-sticky">
    <span class="manifesto-glow" id="mGlow" aria-hidden="true"></span>
    <div class="manifesto-inner">
      <div class="m-label"><h2 id="manifesto-title" class="eyebrow">Why Lumora</h2><span class="rule"></span></div>
      <p class="m-text" id="mText"><span class="sr-only">Your roof rarely runs short of sun. It runs short of timing. Lumora reads the weather, your home and your utility rates as one system, so every kilowatt-hour your panels make lands in the hour it saves you the most.</span></p>
      <div class="m-meter" aria-hidden="true"><span class="lab">Sun put to work</span><span class="track"><span class="fill" id="mFill"></span></span><span class="pct mono tabnum" id="mPct">0%</span></div>
    </div>
  </div>
</section>

<!-- ================= PRODUCT ================= -->
<section id="product" class="product" data-section="product" aria-labelledby="product-title">
  <div class="aurora" aria-hidden="true"><i></i><i></i><i></i></div>
  <div class="dotgrid" aria-hidden="true"></div>
  <div class="container">
    <div class="section-head center">
      <p class="eyebrow dark reveal">The app</p>
      <h2 id="product-title" class="h2"><span class="split" data-split>One calm app for</span> <span class="serif split" data-split data-delay="4">your home's whole energy day.</span></h2>
      <p class="lede reveal">Solar, battery, grid and savings sit side by side, so you always know what your home is running on. Try it: switch the range, hover the chart, schedule an action.</p>
    </div>
    <div class="dash-wrap">
      <div class="dash-tilt" id="dashTilt">
        <div class="dash" role="region" aria-label="Interactive preview of the Lumora app">
          <div class="dash-side" aria-hidden="true">
            <svg width="30" height="30"><use href="#logo-mark"/></svg>
            <div style="margin-top:32px;display:flex;flex-direction:column;gap:8px">
              <span class="nav-ic"><svg class="ic"><use href="#i-home"/></svg></span>
              <span class="nav-ic on"><svg class="ic"><use href="#i-chart"/></svg></span>
              <span class="nav-ic"><svg class="ic"><use href="#i-charging"/></svg></span>
              <span class="nav-ic"><svg class="ic"><use href="#i-sun"/></svg></span>
              <span class="nav-ic"><svg class="ic"><use href="#i-bell"/></svg></span>
            </div>
            <span class="nav-ic" style="margin-top:auto"><svg class="ic"><use href="#i-settings"/></svg></span>
          </div>
          <div class="dash-main">
            <div class="dash-top">
              <div class="tabs" aria-hidden="true"><span class="tab md">Home</span><span class="tab on">Energy</span><span class="tab md">Battery</span><span class="tab md">Savings</span><span class="tab xl">Devices</span><span class="tab xl">Settings</span></div>
              <div class="dash-tools" aria-hidden="true"><span class="livepill"><i></i>Autopilot on</span><span class="avatar">JL</span></div>
            </div>
            <div class="dash-body">
              <div class="dash-head">
                <div><h3>Your home's energy day</h3><p>8.2 kW solar · 13.5 kWh battery · forecast refreshed every five minutes</p></div>
                <div class="seg" role="group" aria-label="Time range" id="rangeSeg">
                  <button type="button" aria-pressed="true" data-range="today">Today</button>
                  <button type="button" aria-pressed="false" data-range="tomorrow">Tomorrow</button>
                  <button type="button" aria-pressed="false" data-range="week">This week</button>
                </div>
              </div>
              <div class="kpis">
                <div class="kpi solar"><p class="k"><svg class="ic" style="color:#d9941f"><use href="#i-sun"/></svg><span id="kSolarL">Solar today</span></p><div class="row"><p class="v" id="kSolar"></p><div class="spark" aria-hidden="true"><svg viewBox="0 0 100 32" preserveAspectRatio="none"><path d="M0,29C3.03,27 6.06,24.46 9.09,23.01C12.12,21.56 15.15,19.59 18.18,19.59C21.21,19.59 24.24,25.58 27.27,25.58C30.3,25.58 33.33,23.14 36.36,21.3C39.39,19.47 42.42,13.61 45.45,13.61C48.48,13.61 51.52,16.17 54.55,16.17C57.58,16.17 60.61,13.16 63.64,11.89C66.67,10.63 69.7,8.47 72.73,8.47C75.76,8.47 78.79,13.61 81.82,13.61C84.85,13.61 87.88,7.31 90.91,5.91C93.94,4.5 96.97,3.97 100,3"/></svg><i style="top:9.4%"></i></div></div><p class="d" id="kSolarD"></p></div>
                <div class="kpi"><p class="k"><svg class="ic" style="color:var(--primary)"><use href="#i-charging"/></svg>Battery</p><div class="row"><p class="v" id="kBatt"></p></div><div class="meter" aria-hidden="true"><div id="kBattBar"></div></div><p class="d" id="kBattD"></p></div>
                <div class="kpi"><p class="k"><svg class="ic" style="color:var(--grid)"><use href="#i-plug"/></svg>From the grid</p><div class="row"><p class="v" id="kGrid"></p><div class="spark" aria-hidden="true"><svg viewBox="0 0 100 32" preserveAspectRatio="none"><path d="M0,3C3.03,4.24 6.06,6.71 9.09,6.71C12.12,6.71 15.15,6.71 18.18,6.71C21.21,6.71 24.24,9.19 27.27,10.43C30.3,11.67 33.33,14.14 36.36,14.14C39.39,14.14 42.42,14.14 45.45,14.14C48.48,14.14 51.52,17.86 54.55,17.86C57.58,17.86 60.61,17.86 63.64,17.86C66.67,17.86 69.7,20.33 72.73,21.57C75.76,22.81 78.79,25.29 81.82,25.29C84.85,25.29 87.88,25.29 90.91,25.29C93.94,25.29 96.97,27.76 100,29"/></svg><i style="top:90.6%"></i></div></div><p class="d" id="kGridD"></p></div>
                <div class="kpi"><p class="k"><svg class="ic" style="color:var(--primary)"><use href="#i-dollar"/></svg><span id="kSaveL">Saved today</span></p><div class="row"><p class="v" id="kSave"></p><div class="spark" aria-hidden="true"><svg viewBox="0 0 100 32" preserveAspectRatio="none"><path d="M0,29C3.03,27.69 6.06,25.06 9.09,25.06C12.12,25.06 15.15,27.03 18.18,27.03C21.21,27.03 24.24,22.7 27.27,21.12C30.3,19.55 33.33,17.18 36.36,17.18C39.39,17.18 42.42,19.15 45.45,19.15C48.48,19.15 51.52,14.23 54.55,13.24C57.58,12.26 60.61,11.27 63.64,11.27C66.67,11.27 69.7,15.21 72.73,15.21C75.76,15.21 78.79,10.88 81.82,9.3C84.85,7.73 87.88,6.35 90.91,5.36C93.94,4.38 96.97,3.79 100,3"/></svg><i style="top:9.4%"></i></div></div><p class="d" id="kSaveD"></p></div>
              </div>
              <div class="dash-lower">
                <div class="panel chart-panel">
                  <div class="panel-h"><h4>Home usage vs. solar</h4><p id="chartSub"></p></div>
                  <ul class="legend"><li><span class="lg-line"></span>Actual usage</li><li><svg width="16" height="2" aria-hidden="true"><line x1="0" y1="1" x2="16" y2="1" stroke="#1e8538" stroke-opacity=".6" stroke-width="2" stroke-dasharray="4 3"/></svg>Usage forecast</li><li><span class="lg-solar"></span>Solar production</li><li><span class="lg-dot"></span>Usage peak</li></ul>
                  <div class="chart" id="chart">
                    <div class="y-axis" id="yAxis" aria-hidden="true"></div>
                    <div class="plot" id="plot">
                      <svg viewBox="0 0 1000 300" preserveAspectRatio="none" aria-hidden="true" class="draw" id="chartSvg">
                        <line class="grid-l" x1="0" x2="1000" y1="300" y2="300"/><line class="grid-l" x1="0" x2="1000" y1="225" y2="225"/><line class="grid-l" x1="0" x2="1000" y1="150" y2="150"/><line class="grid-l" x1="0" x2="1000" y1="75" y2="75"/><line class="grid-l" x1="0" x2="1000" y1="0" y2="0"/>
                        <path class="sfill" id="pSF"/><path class="sline" id="pS"/><path class="band" id="pBand"/><path class="afill" id="pAFill"/><path class="fline" id="pF"/><path class="aline" id="pA"/>
                      </svg>
                      <div class="nowl" id="nowLine" aria-hidden="true"><span>Now</span></div>
                      <div class="peak" id="peak" aria-hidden="true"><i></i><span id="peakLbl"></span></div>
                      <div class="hv" id="hv" aria-hidden="true"></div>
                      <div class="hv-dot" id="hvS" style="background:var(--sun)" aria-hidden="true"></div>
                      <div class="hv-dot" id="hvF" style="background:#7fbf8d" aria-hidden="true"></div>
                      <div class="hv-dot" id="hvA" style="background:var(--primary)" aria-hidden="true"></div>
                      <div class="tip" id="tip" aria-hidden="true"></div>
                      <div class="hit" id="hit" role="group" tabindex="0" aria-roledescription="chart" aria-label="Home usage versus solar production" aria-describedby="chartHelp"></div>
                      <p id="chartHelp" class="sr-only">Use the left and right arrow keys to move through the chart.</p>
                      <p class="sr-only" aria-live="polite" id="chartLive"></p>
                    </div>
                    <div class="x-axis" id="xAxis" aria-hidden="true"></div>
                  </div>
                  <table class="sr-only" id="chartTable"></table>
                </div>
                <div class="panel side-panel">
                  <div>
                    <div class="panel-h"><h4>Where your power came from</h4></div>
                    <div class="mixbar" role="img" id="mixBar" aria-label="">
                      <div style="background:linear-gradient(180deg,#f8c766,#e9a23a)"></div><div style="background:linear-gradient(180deg,#2fa04b,#1b7a33)"></div><div style="background:#a9b6c6"></div>
                    </div>
                    <ul class="mixlist" id="mixList">
                      <li><span><i style="background:#f0b046"></i>Solar</span><b></b></li>
                      <li><span><i style="background:#1e8538"></i>Battery</span><b></b></li>
                      <li><span><i style="background:#a9b6c6"></i>Grid</span><b></b></li>
                    </ul>
                  </div>
                  <div class="hr"></div>
                  <div>
                    <div class="panel-h"><h4>Suggested by Lumora</h4><p id="schedCount" aria-live="polite">0 of 3 scheduled</p></div>
                    <ul class="actions">
                      <li class="action"><span class="ai blue"><svg class="ic"><use href="#i-storm"/></svg></span><div class="at"><p>Fill the battery before Thursday's storm</p><p>Storm Watch: 100% by 22:00 Wednesday</p></div><button type="button" class="sched" aria-label="Schedule: Fill the battery before Thursday's storm">Schedule</button></li>
                      <li class="action"><span class="ai amber"><svg class="ic"><use href="#i-sun"/></svg></span><div class="at"><p>Run the dishwasher at 13:00</p><p>Uses 1.2 kWh of free midday sun</p></div><button type="button" class="sched" aria-label="Schedule: Run the dishwasher at 13:00">Schedule</button></li>
                      <li class="action"><span class="ai"><svg class="ic"><use href="#i-thermo"/></svg></span><div class="at"><p>Pre-cool the house 15:30 to 16:30</p><p>Skips 2.4 kWh of peak-rate power</p></div><button type="button" class="sched" aria-label="Schedule: Pre-cool the house 15:30 to 16:30">Schedule</button></li>
                    </ul>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <ul class="features3">
      <li class="reveal"><span class="fi dark"><svg class="ic"><use href="#i-refresh"/></svg></span><div><h3>Refreshed every five minutes</h3><p>Weather models, your panels and live utility rates stream in, so the plan moves when the clouds do.</p></div></li>
      <li class="reveal" style="transition-delay:.1s"><span class="fi dark"><svg class="ic"><use href="#i-users"/></svg></span><div><h3>One picture for the household</h3><p>Everyone sees the same calm view of what's running, what's stored and what it's saving.</p></div></li>
      <li class="reveal" style="transition-delay:.2s"><span class="fi dark"><svg class="ic"><use href="#i-shield"/></svg></span><div><h3>Every decision explained</h3><p>Tap any charge or discharge to see the forecast and rate that justified it.</p></div></li>
    </ul>
  </div>
</section>

<!-- ================= SOLUTIONS ================= -->
<section id="solutions" class="solutions" data-section="solutions" aria-labelledby="solutions-title">
  <div class="sol-sticky">
    <div class="container" style="width:100%">
      <div class="sol-head">
        <div class="section-head">
          <p class="eyebrow reveal">How it saves</p>
          <h2 id="solutions-title" class="h2"><span class="split" data-split>Forecast. Store. Save.</span><span class="sub split" data-split data-delay="3">Three jobs, one quiet app.</span></h2>
        </div>
        <div class="stages" aria-hidden="true">
          <div class="line"><div class="f" id="stageFill"></div><span class="dot" id="stageDot"></span></div>
          <ol><li class="on"><span class="knob"></span><span class="n">Forecast</span><span class="s">Predicts the sun</span></li><li><span class="knob"></span><span class="n">Store</span><span class="s">Banks it</span></li><li><span class="knob"></span><span class="n">Save</span><span class="s">Spends it at the peak</span></li></ol>
        </div>
      </div>
    </div>
    <div class="sol-track-wrap">
      <div class="sol-track" id="solTrack">
        <div class="sol-intro">
          <p>Lumora replaces guesswork, default battery modes and surprise bills with one system that plans your home's energy day. Each stage hands its answer to the next.</p>
          <p class="cue" aria-hidden="true">Scroll to follow the flow<span class="cue-line"></span></p>
        </div>

        <article class="stage dark">
          <div class="stage-bg" aria-hidden="true"><svg id="fcScene" viewBox="0 0 1200 700" preserveAspectRatio="xMidYMax slice"></svg></div>
          <div class="stage-in">
            <div class="stage-copy">
              <div class="stage-top"><span class="chip"><span class="ci"><svg class="ic"><use href="#i-sun"/></svg></span>Forecast</span><span class="stage-num">01 / 03</span></div>
              <h3>See tomorrow's sunshine before it arrives.</h3>
              <p class="sp">Hyperlocal solar forecasts at 15-minute resolution for your exact roof. Lumora learns its angle, its shade and its quirks, and shows you how sure it is.</p>
              <p class="next"><span class="ni"><svg class="ic"><use href="#i-arrow"/></svg></span><span><b>Next, Store.</b> The surplus it predicts becomes the battery plan.</span></p>
            </div>
            <div class="phone-wrap">
              <div class="phone" role="img" aria-label="Lumora app showing 38.6 kilowatt-hours of solar forecast for tomorrow">
                <div class="screen">
                  <div class="statusbar"><span>9:41</span><span class="notch"></span><span class="sigs"><span class="bars"><i style="height:6px"></i><i style="height:8px"></i><i style="height:10px"></i></span><span class="batt"><i></i></span></span></div>
                  <div class="ph-row"><span class="l"><svg><use href="#logo-mark"/></svg>Solar forecast</span><span class="r">Tomorrow</span></div>
                  <p class="ph-big">38.6<small>kWh</small></p>
                  <p class="ph-sub"><i></i>Sunniest from 11:00 to 15:00</p>
                  <div class="ph-chart"><svg viewBox="0 0 100 60" preserveAspectRatio="none" id="phoneChart"></svg></div>
                  <div class="ph-x"><span>06:00</span><span>10:00</span><span>14:00</span><span>18:00</span></div>
                  <div class="ph-cards"><div><svg class="ic"><use href="#i-sun"/></svg><b>92%</b><span>Confidence</span></div><div><svg class="ic"><use href="#i-charging"/></svg><b>13:40</b><span>Battery full by</span></div></div>
                </div>
              </div>
            </div>
          </div>
        </article>

        <article class="stage light">
          <div class="stage-in">
            <div class="stage-copy">
              <div class="stage-top"><span class="chip"><span class="ci"><svg class="ic"><use href="#i-charging"/></svg></span>Store</span><span class="stage-num">02 / 03</span></div>
              <h3>Charge from the roof. Power the evening.</h3>
              <p class="sp">Charging plans that respect your backup reserve, your battery warranty and your export limits. Set it once and leave it on autopilot.</p>
              <p class="next"><span class="ni"><svg class="ic"><use href="#i-arrow"/></svg></span><span><b>Next, Save.</b> Stored sun is spent in the hours the grid costs most.</span></p>
            </div>
            <div class="viz">
              <div class="soc">
                <div class="ring" role="img" aria-label="Battery 86% charged">
                  <svg viewBox="0 0 120 120"><defs><linearGradient id="gRing" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#f4b23f"/><stop offset=".5" stop-color="#57c76a"/><stop offset="1" stop-color="#1e8538"/></linearGradient></defs><circle cx="60" cy="60" r="52" fill="none" stroke-width="10" stroke="var(--leaf-soft)"/><circle class="ring-arc" id="ringArc" cx="60" cy="60" r="52" fill="none" stroke-width="10" stroke-linecap="round" stroke="url(#gRing)" stroke-dasharray="326.73" stroke-dashoffset="326.73" style="filter:drop-shadow(0 4px 8px rgba(30,133,56,.3))"/></svg>
                  <div class="rv"><b>86%</b><span>charged</span></div>
                </div>
                <dl><div><dt>Charging from roof</dt><dd>+3.8 kW</dd></div><div><dt>Full by</dt><dd>13:40</dd></div><div><dt>Held for tonight</dt><dd>11.6 kWh</dd></div></dl>
              </div>
              <div class="plan">
                <div class="plan-h"><p>Battery plan, today</p><ul><li><i style="background:#f0b046"></i>Charge from sun</li><li><i style="background:var(--primary)"></i>Power home</li><li><i style="background:var(--mist);box-shadow:0 0 0 1px rgba(0,0,0,.05)"></i>Hold</li></ul></div>
                <div class="cells" id="cells" role="img" aria-label="Battery plan: charge from the sun from 09:00 to 13:00, power the home from 17:00 to 22:00, hold otherwise"></div>
                <div class="axis5" aria-hidden="true"><span>00:00</span><span>06:00</span><span>12:00</span><span>18:00</span><span>24:00</span></div>
                <p class="reserve"><svg class="ic"><use href="#i-shield"/></svg>20% always held back for outages</p>
              </div>
            </div>
          </div>
        </article>

        <article class="stage light">
          <div class="stage-in">
            <div class="stage-copy">
              <div class="stage-top"><span class="chip"><span class="ci"><svg class="ic"><use href="#i-dollar"/></svg></span>Save</span><span class="stage-num">03 / 03</span></div>
              <h3>Spend stored sun when the grid costs most.</h3>
              <p class="sp">Lumora ranks every hour by rate, weather and what your household needs, then times the battery. Today that keeps an expected $4.80 in your pocket.</p>
              <p class="next"><span class="ni"><svg class="ic"><use href="#i-repeat"/></svg></span><span><b>Back to Forecast.</b> Every evening sharpens tomorrow's forecast.</span></p>
            </div>
            <div class="viz">
              <div class="plan-h"><p>Your grid price today, ¢/kWh</p><ul><li><i style="background:var(--primary)"></i>Battery covers</li><li><i style="background:var(--sage)"></i>Other hours</li></ul></div>
              <div class="bars" id="bars">
                <div class="bars-in" id="barsIn" role="img" aria-label="Hourly grid price from 14 to 48 cents per kilowatt-hour, peaking from 16:00 to 21:00, when the battery covers your home."></div>
                <div class="axis5" aria-hidden="true"><span>00:00</span><span>06:00</span><span>12:00</span><span>18:00</span><span>23:00</span></div>
              </div>
            </div>
          </div>
        </article>

        <div class="underneath">
          <p>Running in the background</p>
          <ul>
            <li class="spot"><div class="sh"><span class="fi light"><svg class="ic"><use href="#i-storm"/></svg></span><h3>Storm Watch</h3></div><p>When an outage is likely, Lumora fills the battery ahead of time so the lights, fridge and Wi‑Fi stay on.</p></li>
            <li class="spot"><div class="sh"><span class="fi amber"><svg class="ic"><use href="#i-heart"/></svg></span><h3>Battery care</h3></div><p>Gentle cycles and smart temperature limits keep your battery healthy for its full warranty.</p></li>
            <li class="spot"><div class="sh"><span class="fi light"><svg class="ic"><use href="#i-file"/></svg></span><h3>Monthly savings report</h3></div><p>A plain-English summary of what your sun earned, what you avoided and how next month looks.</p></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ================= RESULTS ================= -->
<section id="insights" class="insights" data-section="results" aria-labelledby="insights-title">
  <div class="container">
    <div class="section-head">
      <p class="eyebrow reveal">Results</p>
      <h2 id="insights-title" class="h2"><span class="split" data-split>Homes feel the difference</span> <span class="serif split" data-split data-delay="4">on the first bill.</span></h2>
      <p class="lede reveal">What a typical Lumora home sees in its first year, compared with the same system running on the battery's default settings.</p>
    </div>
    <dl class="stats">
      <div class="stat reveal"><dt>of home energy from your own roof</dt><dd class="num" data-count="72" data-suffix="%">72%</dd><dd class="desc">Sun that used to be exported for pennies now runs your evenings.</dd></div>
      <div class="stat reveal" style="transition-delay:.08s"><dt>day-ahead solar forecast accuracy</dt><dd class="num" data-count="94.6" data-dec="1" data-suffix="%">94.6%</dd><dd class="desc">Tuned to your roof's angle, shade and local weather.</dd></div>
      <div class="stat reveal" style="transition-delay:.16s"><dt>lower electricity bills</dt><dd class="num" data-count="41" data-suffix="%">41%</dd><dd class="desc">Mostly from skipping peak-rate hours entirely.</dd></div>
      <div class="stat reveal" style="transition-delay:.24s"><dt>average yearly savings</dt><dd class="num" data-count="1140" data-prefix="$" data-comma="1">$1,140</dd><dd class="desc">On top of what the panels already save on their own.</dd></div>
    </dl>
    <div class="quotes">
      <figure class="q-big reveal">
        <svg class="bg" id="duskScene" viewBox="0 0 900 600" preserveAspectRatio="xMidYMax slice" aria-hidden="true"></svg>
        <svg class="ic qi"><use href="#i-quote"/></svg>
        <blockquote><p>We used to export our midday sun for pennies and buy it back at dinner. Now the battery is full by lunch and our evenings run on our own roof.</p></blockquote>
        <figcaption class="who"><span class="av" aria-hidden="true"><svg class="ic"><use href="#i-home"/></svg></span><span><b>Homeowner <i class="ph-tag">Sample quote</i></b><span>8.2 kW solar, 13.5 kWh battery</span></span></figcaption>
      </figure>
      <div class="qcol">
        <figure class="q-sm reveal" style="transition-delay:.1s"><blockquote><p>The storm alert charged us to full the night before the outage. We barely noticed the grid went down.</p></blockquote><figcaption class="who"><span class="av" aria-hidden="true"><svg class="ic"><use href="#i-storm"/></svg></span><span><b>Homeowner <i class="ph-tag">Sample quote</i></b><span>6.4 kW solar, 10 kWh battery</span></span></figcaption></figure>
        <figure class="q-sm reveal" style="transition-delay:.2s"><blockquote><p>I stopped checking three apps. One screen tells me what we're running on and what it saved today.</p></blockquote><figcaption class="who"><span class="av" aria-hidden="true"><svg class="ic"><use href="#i-sun"/></svg></span><span><b>Homeowner <i class="ph-tag">Sample quote</i></b><span>11 kW solar, two batteries</span></span></figcaption></figure>
      </div>
    </div>
    <p class="footnote">Figures and quotes on this page are illustrative placeholders for a concept product.</p>
  </div>
</section>

<!-- ================= HOW IT WORKS ================= -->
<section id="how-it-works" class="how" data-section="how-it-works" aria-labelledby="how-title">
  <div class="container">
    <div class="section-head center">
      <p class="eyebrow reveal">How it works</p>
      <h2 id="how-title" class="h2"><span class="split" data-split>Running in an afternoon.</span> <span class="serif split" data-split data-delay="4">Smarter every week.</span></h2>
      <p class="lede reveal">Lumora works with the solar and battery already on your wall. No new hardware, no electrician visit.</p>
    </div>
    <div class="timeline" id="timeline">
      <div class="tl-rail" aria-hidden="true"><div class="f" id="tlFill"></div><span class="dot" id="tlDot"></span></div>
      <ol>
        <li class="tl left"><div class="tl-badge"><span class="badge">01<span class="on" aria-hidden="true">01</span></span></div><div class="tl-card"><div class="spot"><p class="wk">Day 1</p><h3>Connect your system</h3><p>Pair Lumora with your inverter and battery over Wi‑Fi in about ten minutes. Nothing new goes on the roof.</p></div></div><p class="tl-ghost" aria-hidden="true">Day 1</p></li>
        <li class="tl right" style="--rot:2.5deg"><div class="tl-badge"><span class="badge">02<span class="on" aria-hidden="true">02</span></span></div><div class="tl-card"><div class="spot"><p class="wk">Week 1</p><h3>Learn your home</h3><p>Lumora studies your usage, your roof's angle and shade, and your local weather to build a forecast that's yours alone.</p></div></div><p class="tl-ghost" aria-hidden="true">Week 1</p></li>
        <li class="tl left"><div class="tl-badge"><span class="badge">03<span class="on" aria-hidden="true">03</span></span></div><div class="tl-card"><div class="spot"><p class="wk">Week 2</p><h3>Let it run</h3><p>Autopilot charges, powers and exports inside the backup reserve and limits you set. Override anything with one tap.</p></div></div><p class="tl-ghost" aria-hidden="true">Week 2</p></li>
        <li class="tl tl-final"><div class="tl-badge"><span class="badge final"><svg class="ic" style="font-size:20px"><use href="#i-check"/></svg><span class="on" aria-hidden="true"><svg class="ic" style="font-size:20px"><use href="#i-check"/></svg></span></span></div><p><b>Saving from the first bill.</b> And the forecast keeps learning every evening.</p></li>
      </ol>
    </div>
    <div class="integr reveal">
      <div class="integr-in">
        <div class="lft"><span class="fi light"><svg class="ic"><use href="#i-wifi"/></svg></span><div><h3>Works with the gear on your wall</h3><p>Connects over your home Wi‑Fi. Local control keeps running if the internet drops.</p></div></div>
        <ul class="tags"><li>Hybrid inverters</li><li>Home batteries 5–40 kWh</li><li>Time-of-use rate plans</li><li>Net metering and export tariffs</li><li>Smart thermostats</li><li>EV chargers</li><li>Heat pumps</li><li>Outage alerts</li></ul>
      </div>
    </div>
  </div>
</section>

<!-- ================= ABOUT ================= -->
<section id="about" class="about" data-section="about" aria-labelledby="about-title">
  <div class="container about-grid">
    <div class="about-art-wrap">
      <div class="about-art" id="aboutArt" role="img" aria-label="Illustration of rooftop solar panels catching golden evening light over a quiet neighborhood">
        <div class="par" id="aboutPar"><svg id="roofArt" viewBox="0 0 800 1000" preserveAspectRatio="xMidYMid slice" aria-hidden="true"></svg></div>
      </div>
      <div class="mission reveal"><p>Our mission</p><p>Help every home run on its own sunshine, long after the sun goes down.</p></div>
    </div>
    <div>
      <div class="section-head">
        <p class="eyebrow reveal">About Lumora</p>
        <h2 id="about-title" class="h2 split" data-split>Built by energy engineers who wanted a smarter battery at home.</h2>
        <p class="lede reveal">Lumora started when a few grid engineers installed batteries in their own houses and watched them sit full at the wrong hours. Today our team pairs power systems know-how with machine learning, so every home gets the kind of planning utilities use.</p>
      </div>
      <dl class="about-stats reveal">
        <div><dt>homes on autopilot</dt><dd class="num" data-count="10" data-suffix="k+">10k+</dd></div>
        <div><dt>stored and spent daily</dt><dd class="num" data-count="610" data-suffix=" MWh">610 MWh</dd></div>
        <div><dt>platform uptime</dt><dd class="num" data-count="99.95" data-dec="2" data-suffix="%">99.95%</dd></div>
      </dl>
      <ul class="trust">
        <li class="reveal"><span class="fi white"><svg class="ic"><use href="#i-shield"/></svg></span><div><h3>Backup always comes first</h3><p>Your reserve never drops below the floor you set, so essentials stay on in an outage.</p></div></li>
        <li class="reveal"><span class="fi white"><svg class="ic"><use href="#i-wifi"/></svg></span><div><h3>Keeps working offline</h3><p>Today's plan runs locally on your system and resyncs when the internet is back.</p></div></li>
        <li class="reveal"><span class="fi white"><svg class="ic"><use href="#i-lock"/></svg></span><div><h3>Your data stays yours</h3><p>Encrypted end to end, never sold, and exportable any time from the app.</p></div></li>
      </ul>
    </div>
  </div>
</section>

<!-- ================= FAQ ================= -->
<section id="faq" class="faq" data-section="faq" aria-labelledby="faq-title">
  <div class="container faq-grid">
    <div class="faq-side">
      <div class="section-head">
        <p class="eyebrow reveal">FAQ</p>
        <h2 id="faq-title" class="h2 split" data-split>Questions homeowners ask us first.</h2>
        <p class="lede reveal">Anything else, ask us when we send your estimate. We're happy to go deep on your system, your rate plan and your roof.</p>
      </div>
      <a class="textlink" href="#get-started">Check your system's compatibility <svg class="ic"><use href="#i-arrow"/></svg></a>
    </div>
    <div class="qa">
      <details class="reveal"><summary>Which solar and battery systems does Lumora work with?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">Most hybrid inverters and home batteries from 5 to 40 kWh connect over your home Wi‑Fi. Enter your system's model number and we'll confirm compatibility in under a minute.</p></details>
      <details class="reveal"><summary>Do I need a battery?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">Lumora works best with one, but solar-only homes still get forecasts, usage insights and appliance timing. It can also model what a battery would save you before you buy one.</p></details>
      <details class="reveal"><summary>What happens during a power outage?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">Storm Watch fills your battery ahead of forecast outages and never touches your backup reserve, so essentials stay powered the moment the grid drops.</p></details>
      <details class="reveal"><summary>Does it work if my internet goes down?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">Yes. The current plan runs locally on your system and resyncs with the latest forecast as soon as you're back online.</p></details>
      <details class="reveal"><summary>How much will I save?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">It depends on your rate plan, system size and habits. Homes on time-of-use plans usually see the biggest change. Your free estimate shows numbers for your address.</p></details>
      <details class="reveal"><summary>How is Lumora priced?<span class="pl"><svg class="ic"><use href="#i-plus"/></svg></span></summary><p class="ans">$8 a month or $79 a year, with the first 60 days free. No contract, and you can cancel any time from the app.</p></details>
    </div>
  </div>
</section>

<!-- ================= ESTIMATE ================= -->
<section id="get-started" class="cta" data-section="estimate" aria-labelledby="gs-title">
  <div class="container">
    <div class="cta-card">
      <svg class="bg" id="nightScene" viewBox="0 0 1400 800" preserveAspectRatio="xMidYMax slice" aria-hidden="true"></svg>
      <div class="cta-grid">
        <div class="cta-copy">
          <div class="section-head">
            <p class="eyebrow dark reveal">Free savings estimate</p>
            <h2 id="gs-title" class="h2"><span class="split" data-split>See what your roof could save</span> <span class="serif split" data-split data-delay="5">in two minutes.</span></h2>
            <p class="lede reveal">Tell us about your home and we'll model a year of sun, usage and rates for your address.</p>
          </div>
          <ul class="checks">
            <li class="reveal"><span class="ck"><svg class="ic"><use href="#i-check"/></svg></span>A year of solar forecast for your roof</li>
            <li class="reveal" style="transition-delay:.08s"><span class="ck"><svg class="ic"><use href="#i-check"/></svg></span>Estimated savings on your rate plan</li>
            <li class="reveal" style="transition-delay:.16s"><span class="ck"><svg class="ic"><use href="#i-check"/></svg></span>Whether a battery pays off for you</li>
          </ul>
          <p class="cta-note">Free, no obligation. Most estimates arrive the same day.</p>
        </div>
        <div class="formcard reveal" id="formCard">
          <form id="demoForm" novalidate aria-describedby="formNote">
            <h3>Get your estimate</h3>
            <p class="note" id="formNote">Fields marked with an asterisk are required.</p>
            <div class="fgrid">
              <div class="field"><label for="fName">Full name <span class="req" aria-hidden="true">*</span></label><input class="inp" id="fName" type="text" autocomplete="name" required maxlength="100" placeholder="Jordan Lee" aria-invalid="false" aria-describedby="eName"><p class="err" id="eName"></p></div>
              <div class="field"><label for="fEmail">Email <span class="req" aria-hidden="true">*</span></label><input class="inp" id="fEmail" type="email" autocomplete="email" required maxlength="200" placeholder="jordan@example.com" aria-invalid="false" aria-describedby="eEmail"><p class="err" id="eEmail"></p></div>
              <div class="field"><label for="fZip">ZIP code <span class="req" aria-hidden="true">*</span></label><input class="inp" id="fZip" type="text" inputmode="numeric" autocomplete="postal-code" required maxlength="10" placeholder="94110" aria-invalid="false" aria-describedby="eZip"><p class="err" id="eZip"></p></div>
              <div class="field"><label for="fSetup">Your setup <span class="opt">(optional)</span></label><div class="selwrap"><select class="inp empty" id="fSetup"><option value="">Choose one</option><option>Solar and a battery</option><option>Solar only</option><option>Planning to go solar</option></select><svg class="ic"><use href="#i-chev"/></svg></div></div>
              <div class="field span2"><label for="fBill">Average monthly electric bill <span class="opt">(optional)</span></label><div class="selwrap"><select class="inp empty" id="fBill"><option value="">Choose a range</option><option>Under $100</option><option>$100 to $200</option><option>$200 to $350</option><option>Over $350</option></select><svg class="ic"><use href="#i-chev"/></svg></div></div>
              <fieldset class="field span2"><legend>What matters most to you? <span class="opt">(optional)</span></legend>
                <div class="pills">
                  <label><input type="checkbox" value="Lower bills"><span><svg class="ic"><use href="#i-check"/></svg>Lower bills</span></label>
                  <label><input type="checkbox" value="Backup power"><span><svg class="ic"><use href="#i-check"/></svg>Backup power</span></label>
                  <label><input type="checkbox" value="EV charging"><span><svg class="ic"><use href="#i-check"/></svg>EV charging</span></label>
                  <label><input type="checkbox" value="Using my own sun"><span><svg class="ic"><use href="#i-check"/></svg>Using my own sun</span></label>
                </div>
              </fieldset>
              <div class="field span2"><label for="fMsg">Anything we should know? <span class="opt">(optional)</span></label><textarea class="inp" id="fMsg" rows="3" maxlength="2000" placeholder="Your rate plan, roof direction, how often the power goes out…"></textarea></div>
            </div>
            <div class="fbot">
              <p>We only use your details to prepare your estimate. Read our <a href="#faq">privacy policy</a>.</p>
              <button type="submit" class="btn btn-green btn-lg">Get my estimate <svg class="ic"><use href="#i-arrow"/></svg></button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ================= EARLY ACCESS / 3D ================= -->
<section id="early-access" class="early" data-section="early-access" aria-labelledby="ea-title">
  <div class="early-box">
    <div class="early-top">
      <h2 id="ea-title" class="split" data-split>Steady power after every sunset</h2>
      <p class="early-lede reveal">Lumora helps homeowners use more of their own sun, lean less on the grid and keep the lights on when it goes down.</p>
      <form class="ea-form reveal" id="eaForm" novalidate>
        <label for="eaEmail" class="sr-only">Email</label>
        <input id="eaEmail" type="email" autocomplete="email" placeholder="Enter your email" aria-invalid="false" aria-describedby="eaMsg">
        <button type="submit" class="btn btn-primary btn-lg">Start 60 days free</button>
      </form>
      <p class="ea-msg" id="eaMsg" aria-live="polite"></p>
    </div>
    <div class="early-model">
      <div class="model-scale" id="modelScale">
        <div class="model" id="model" role="group" tabindex="0" aria-roledescription="3D model" aria-label="Solar array with a home battery. Drag it, or use the arrow keys, to turn it and see every side.">
          <div class="sunburst"></div><div class="hz"></div>
          <div class="rig" id="rig">
            <div class="pad3d"></div>
            <div class="shadow3d"></div>
            <div class="trench"></div>
            <div id="legs"></div>
            <div class="array">
              <div class="face front"><div class="pv"></div><div class="pv"></div><div class="pv"></div><div class="pv"></div><div class="pv"></div><div class="pv"></div></div>
              <div class="face back"><div class="pvb"></div><div class="pvb"></div><div class="pvb"></div><div class="pvb"></div><div class="pvb"></div><div class="pvb"></div></div>
            </div>
            <div class="cab">
              <div class="f bk"></div><div class="f lf"></div><div class="f rt"></div><div class="f tp"></div>
              <div class="f fr"><span class="led"></span><svg class="mk"><use href="#logo-mark"/></svg></div>
            </div>
          </div>
          <div class="vign"></div>
          <p class="drag-hint" id="dragHint" aria-hidden="true"><svg class="ic"><use href="#i-move"/></svg>Drag to turn it</p>
          <div class="mtag a" aria-hidden="true"><i style="background:var(--sun);box-shadow:0 0 8px var(--sun)"></i><span>Solar now</span><b id="mtSolar">5.4 kW</b></div>
          <div class="mtag b" aria-hidden="true"><i style="background:var(--leaf);box-shadow:0 0 8px var(--leaf)"></i><span>Battery</span><b id="mtBatt">64%</b></div>
        </div>
        <div class="views">
          <div class="vbtns" role="group" aria-label="Choose a side to look at" id="vbtns">
            <button type="button" aria-pressed="true" data-view="front">Front</button>
            <button type="button" aria-pressed="false" data-view="side">Side</button>
            <button type="button" aria-pressed="false" data-view="back">Back</button>
            <button type="button" aria-pressed="false" data-view="top">Top</button>
          </div>
          <p class="vcap" id="vcap" aria-live="polite">Six panels angled at 24 degrees to catch the midday sun, paired with a 13.5 kWh home battery.</p>
        </div>
      </div>
    </div>
  </div>
</section>
</main>

<footer data-section="footer">
  <div class="foot">
    <div class="foot-grid">
      <div class="foot-brand">
        <a href="#hero" class="logo" aria-label="Lumora home"><svg aria-hidden="true"><use href="#logo-mark"/></svg><span class="logo-word" style="color:#fff">Lumora</span></a>
        <p>The AI that runs your home's solar and battery. Forecast the sun, store the surplus and skip the grid's priciest hours, from one calm app.</p>
        <a class="btn btn-glass" href="#get-started" style="height:44px">Get a free estimate <svg class="ic"><use href="#i-arrow-ur"/></svg></a>
      </div>
      <div class="foot-cols">
        <div><h2>Product</h2><ul><li><a href="#product">The app</a></li><li><a href="#solutions">Forecast</a></li><li><a href="#solutions">Store</a></li><li><a href="#solutions">Save</a></li></ul></div>
        <div><h2>Company</h2><ul><li><a href="#about">About</a></li><li><a href="#insights">Results</a></li><li><a href="#get-started">Free estimate</a></li></ul></div>
        <div><h2>Resources</h2><ul><li><a href="#how-it-works">How it works</a></li><li><a href="#faq">FAQ</a></li><li><a href="#faq">Privacy policy</a></li></ul></div>
      </div>
    </div>
    <div class="foot-bot"><p>© 2026 Lumora. All rights reserved.</p><p>Made for homes that run on sunshine.</p></div>
  </div>
  <div class="wordmark" id="wordmark" aria-hidden="true"></div>
</footer>

<script>
(function(){
'use strict';
var doc=document.documentElement;doc.classList.add('js');
var RM=window.matchMedia('(prefers-reduced-motion: reduce)').matches;
var $=function(s,c){return (c||document).querySelector(s)};
var $$=function(s,c){return Array.prototype.slice.call((c||document).querySelectorAll(s))};
var clamp=function(v,a,b){return Math.max(a,Math.min(b,v))};
var lerp=function(a,b,t){return a+(b-a)*t};
var f1=function(v){return (Math.round(v*10)/10).toFixed(1)};
function mk(seed){return function(){seed=(seed*16807)%2147483647;return (seed-1)/2147483646}}
var rnd=mk(42);
function seg(p){var s='';for(var i=0;i<p.length-1;i++){var p0=p[i-1]||p[i],p1=p[i],p2=p[i+1],p3=p[i+2]||p2;s+=' C'+(p1[0]+(p2[0]-p0[0])/6).toFixed(2)+','+(p1[1]+(p2[1]-p0[1])/6).toFixed(2)+' '+(p2[0]-(p3[0]-p1[0])/6).toFixed(2)+','+(p2[1]-(p3[1]-p1[1])/6).toFixed(2)+' '+p2[0].toFixed(2)+','+p2[1].toFixed(2)}return s}
function line(p){return 'M'+p[0][0].toFixed(2)+','+p[0][1].toFixed(2)+seg(p)}

/* ============ Art primitives ============ */
function blob(cx,cy,rx,ry,n,j,r){var pts=[];for(var i=0;i<n;i++){var a=i/n*Math.PI*2,k=1-j/2+r()*j;pts.push([cx+Math.cos(a)*rx*k,cy+Math.sin(a)*ry*k])}
  var w=pts.concat(pts.slice(0,3)),d='M'+pts[0][0].toFixed(1)+','+pts[0][1].toFixed(1);
  for(var t=0;t<n;t++){var p0=w[t-1<0?n-1:t-1],p1=w[t],p2=w[t+1],p3=w[t+2];d+=' C'+(p1[0]+(p2[0]-p0[0])/6).toFixed(1)+','+(p1[1]+(p2[1]-p0[1])/6).toFixed(1)+' '+(p2[0]-(p3[0]-p1[0])/6).toFixed(1)+','+(p2[1]-(p3[1]-p1[1])/6).toFixed(1)+' '+p2[0].toFixed(1)+','+p2[1].toFixed(1)}
  return d+'Z'}
var trnd=mk(77);
function tree(x,y,s,g){
  g=g||'gTree';var cy=y-74*s,o='<g>';
  o+='<ellipse cx="'+x+'" cy="'+y+'" rx="'+(38*s)+'" ry="'+(6*s)+'" fill="#14231a" opacity=".24"/>';
  o+='<path d="M'+(x-3.5*s)+' '+y+' L'+(x-2*s)+' '+(y-50*s)+' L'+(x+2*s)+' '+(y-50*s)+' L'+(x+3.5*s)+' '+y+'Z" fill="#5b4532"/>';
  o+='<path d="M'+x+' '+(y-38*s)+' L'+(x-14*s)+' '+(y-58*s)+'M'+x+' '+(y-44*s)+' L'+(x+12*s)+' '+(y-62*s)+'" stroke="#5b4532" stroke-width="'+(2.2*s)+'" stroke-linecap="round"/>';
  o+='<path d="'+blob(x,cy,40*s,36*s,11,.32,trnd)+'" fill="url(#'+g+')"/>';
  o+='<path d="'+blob(x+4*s,cy+14*s,34*s,16*s,9,.3,trnd)+'" fill="#1d3a22" opacity=".22"/>';
  o+='<path d="'+blob(x-12*s,cy-14*s,18*s,13*s,8,.35,trnd)+'" fill="#d6ebb8" opacity=".28"/>';
  o+='<path d="'+blob(x+14*s,cy-8*s,12*s,9*s,7,.35,trnd)+'" fill="#d6ebb8" opacity=".16"/>';
  return o+'</g>';
}
function cypress(x,y,h,w){return '<path d="M'+x+' '+y+' C '+(x-w)+' '+(y-h*.35)+' '+(x-w*.6)+' '+(y-h*.8)+' '+x+' '+(y-h)+' C '+(x+w*.6)+' '+(y-h*.8)+' '+(x+w)+' '+(y-h*.35)+' '+x+' '+y+'Z" fill="url(#gCyp)"/>'}
function bush(x,y,r){return '<ellipse cx="'+x+'" cy="'+y+'" rx="'+r+'" ry="'+(r*.72)+'" fill="url(#gTree2)"/>'}
function house(x,y,s,c){ // tiny distant house; returns [body, lights]
  c=c||{};var b=c.body||'#efe9dc',r=c.roof||'#545b66',p=c.pv||'#3b6a9c';
  var body='<g><rect x="'+(x-18*s)+'" y="'+(y-18*s)+'" width="'+(36*s)+'" height="'+(18*s)+'" fill="'+b+'"/><polygon points="'+(x-21*s)+','+(y-17*s)+' '+(x-13*s)+','+(y-28*s)+' '+(x+13*s)+','+(y-28*s)+' '+(x+21*s)+','+(y-17*s)+'" fill="'+r+'"/><polygon points="'+(x-14*s)+','+(y-19*s)+' '+(x-9*s)+','+(y-26*s)+' '+(x+8*s)+','+(y-26*s)+' '+(x+13*s)+','+(y-19*s)+'" fill="'+p+'"/></g>';
  var lights='<rect x="'+(x-12*s)+'" y="'+(y-13*s)+'" width="'+(6*s)+'" height="'+(6*s)+'"/><rect x="'+(x+4*s)+'" y="'+(y-13*s)+'" width="'+(8*s)+'" height="'+(6*s)+'"/>';
  return [body,lights];
}
function rays(n,len,grad,op){var s='';for(var k=0;k<n;k++){var l=len*(k%2?.7:1),w=k%3?10:18;s+='<polygon points="0,-4 '+l+',-'+w+' '+l+','+w+' 0,4" fill="url(#'+grad+')" opacity="'+(op||.4)+'" transform="rotate('+(k*360/n)+')"/>'}return '<g><animateTransform attributeName="transform" type="rotate" from="0" to="360" dur="160s" repeatCount="indefinite"/>'+s+'</g>'}
function cloud(x,y,s){return '<g class="cloud"><g filter="url(#fSoft)" fill="#fff" opacity=".78">'+[[0,0,90,20],[-60,8,60,15],[60,6,70,16],[20,-10,60,18]].map(function(e){return '<ellipse cx="'+(x+e[0]*s)+'" cy="'+(y+e[1]*s)+'" rx="'+(e[2]*s)+'" ry="'+(e[3]*s)+'"/>'}).join('')+'</g></g>'}

/* ============ Hero build ============ */
(function(){
  var r=mk(9),i,s='';
  for(i=0;i<170;i++)s+='<circle class="tw" cx="'+(r()*2200-200).toFixed(0)+'" cy="'+(r()*1180-740).toFixed(0)+'" r="'+(r()*1.3+.4).toFixed(2)+'" style="animation-delay:'+(r()*3.6).toFixed(2)+'s"/>';
  $('#stars').innerHTML=s;
  $('#rays').innerHTML=rays(30,1100,'gRay',.26);
  var cl=[[1160,150,300,22,'#f7dcc2'],[1420,104,230,18,'#f5d4ba'],[930,205,200,15,'#f8e2c8'],[330,236,290,20,'#f6e4cf'],[620,166,220,14,'#f3e2cd'],[1660,186,210,16,'#f1cdb2'],[60,120,240,16,'#efe2d2']];
  $('#clouds').innerHTML=cl.map(function(c){return '<g class="cloud"><ellipse cx="'+c[0]+'" cy="'+c[1]+'" rx="'+c[2]+'" ry="'+c[3]+'" fill="'+c[4]+'" opacity=".82"/><ellipse cx="'+(c[0]-c[2]*.2)+'" cy="'+(c[1]+c[3]*.55)+'" rx="'+(c[2]*.6)+'" ry="'+(c[3]*.5)+'" fill="#e8b48f" opacity=".38"/></g>'}).join('');
  var m=[[640,760,260,70],[900,860,340,80],[1260,980,420,90],[420,880,300,60],[1160,860,200,50],[760,640,180,36]];
  $('#mist').innerHTML=m.map(function(e){return '<ellipse cx="'+e[0]+'" cy="'+e[1]+'" rx="'+e[2]+'" ry="'+e[3]+'" fill="#fbead2" opacity=".9"/>'}).join('');
  $('#mistN').innerHTML=m.map(function(e){return '<ellipse cx="'+e[0]+'" cy="'+e[1]+'" rx="'+e[2]+'" ry="'+e[3]+'" fill="#2a3756" opacity=".7"/>'}).join('');
  function bars(id,h){$(id).innerHTML=h.map(function(v,j){return '<i style="height:'+v+'px;animation-delay:-'+(j*.17).toFixed(2)+'s"></i>'}).join('')}
  bars('#bSolar',[8,10,13,16,20,25,30,36,42]);
  bars('#bHome',[8,10,12,14,17,20,24,28,34,40]);
  bars('#bBatt',[8,11,15,10,18,22,13,25,17,27,20,30,23,28,32,22,34,29,33,34]);
})();

/* ============ 3D villa ============ */
(function(){
  function F(st,inner,cls){return '<div class="vf'+(cls?' '+cls:'')+'" style="'+st+'">'+(inner||'')+'</div>'}
  function box(o){
    var w=o.w,d=o.d,h=o.h,s='<div class="vb'+(o.c?' '+o.c:'')+'" style="left:'+o.x+'px;top:'+o.y+'px;width:'+w+'px;height:'+d+'px;transform:translateZ('+(o.z||0)+'px)">';
    if(o.b)s+=F('left:0;top:'+(-h)+'px;width:'+w+'px;height:'+h+'px;transform-origin:50% 100%;transform:rotateX(-90deg);background:'+o.b,o.bi,o.bc);
    if(o.r)s+=F('left:'+(w-h)+'px;top:0;width:'+h+'px;height:'+d+'px;transform-origin:100% 50%;transform:rotateY(90deg);background:'+o.r,o.ri,o.rc);
    if(o.l)s+=F('left:'+(-h)+'px;top:0;width:'+h+'px;height:'+d+'px;transform-origin:100% 50%;transform:rotateY(90deg);background:'+o.l,o.li,o.lc);
    if(o.f)s+=F('left:0;top:'+(d-h)+'px;width:'+w+'px;height:'+h+'px;transform-origin:50% 100%;transform:rotateX(-90deg);background:'+o.f,o.fi,o.fc);
    if(o.t)s+=F('left:0;top:0;width:'+w+'px;height:'+d+'px;transform:translateZ('+h+'px);background:'+o.t,o.ti,o.tc);
    return s+(o.inner||'')+'</div>';
  }
  function bill(x,y,z,w,h,cls){return spr(x,y,z,w,h,cls==='vplant'?'vcyp':cls,!z)}
  function light(x,y,z,sz){return '<div class="vb" style="left:'+x+'px;top:'+y+'px;width:0;height:0;transform:translateZ('+z+'px)">'+F('left:'+(-sz/2)+'px;top:'+(-sz/2)+'px;width:'+sz+'px;height:'+sz+'px;transform:rotateZ(38deg) rotateX(-58deg)','','vlite')+'</div>'}
  function panels(cols,rows,x0,y0,pw,pd,gx,gy){var o='';for(var r=0;r<rows;r++)for(var c=0;c<cols;c++)o+='<div class="vpv" style="left:'+(x0+c*(pw+gx))+'px;top:'+(y0+r*(pd+gy))+'px;width:'+pw+'px;height:'+pd+'px"></div>';return o}
  var conL='linear-gradient(90deg,var(--w1),var(--w2))',conF='linear-gradient(180deg,var(--w2),var(--w3))',conT='linear-gradient(135deg,var(--w0),var(--w1))';
  var inW='linear-gradient(180deg,var(--in1),var(--in2))';
  var woodF='repeating-linear-gradient(90deg,var(--wd1) 0 9px,var(--wd2) 9px 11px)',woodL='repeating-linear-gradient(180deg,var(--wd1) 0 9px,var(--wd2) 9px 11px)';
  var glass='repeating-linear-gradient(90deg,transparent 0 62px,var(--fr) 62px 65px),linear-gradient(112deg,rgba(255,255,255,var(--refl)) 0 13%,rgba(255,255,255,0) 13% 30%,rgba(255,255,255,calc(var(--refl)*.45)) 30% 36%,rgba(255,255,255,0) 36%),var(--gls)';
  var glassL='repeating-linear-gradient(180deg,transparent 0 62px,var(--fr) 62px 65px),linear-gradient(200deg,rgba(255,255,255,var(--refl)) 0 14%,rgba(255,255,255,0) 14%),var(--gls)';
  var deck='repeating-linear-gradient(90deg,var(--dk1) 0 15px,var(--dk2) 15px 16px)';
  var V='';
  /* ground plinth + deck */
  V+=box({x:0,y:0,w:640,d:440,h:12,z:0,l:'linear-gradient(90deg,var(--st1),var(--st2))',f:'linear-gradient(180deg,var(--st1),var(--st2))',t:deck,
    ti:'<div class="vshadow" style="left:368px;top:160px;width:56px;height:236px"></div><div class="vshadow" style="left:52px;top:378px;width:330px;height:30px;opacity:.7"></div><div class="vshadow" style="left:604px;top:70px;width:30px;height:140px"></div>'+
       '<div class="vwater" style="left:404px;top:248px;width:204px;height:164px"></div>'});
  /* living volume A (glass) */
  V+=box({x:40,y:150,w:330,d:230,h:120,z:12,b:inW,r:inW,l:conL,f:glass,fc:'vglass',t:'repeating-linear-gradient(0deg,var(--dk1) 0 13px,var(--dk2) 13px 14px)',
    li:'<div style="position:absolute;left:18px;top:60px;width:84px;height:16px;background:linear-gradient(180deg,var(--in1),var(--in2));box-shadow:inset 0 0 0 3px var(--fr),0 0 30px var(--glow)"></div>'});
  /* interior */
  V+=box({x:120,y:318,w:130,d:40,h:20,z:12,f:'linear-gradient(180deg,#d9c3a2,#b99d78)',t:'linear-gradient(135deg,#efe0c6,#d8c2a0)'});
  V+=box({x:120,y:350,w:130,d:12,h:44,z:12,f:'#cbb08b',t:'#e6d3b4'});
  V+=box({x:262,y:212,w:76,d:34,h:34,z:12,f:'linear-gradient(180deg,#f3ead9,#d6c6aa)',t:'#faf3e6'});
  V+=box({x:58,y:166,w:300,d:14,h:46,z:12,f:'linear-gradient(180deg,#c4935e,#9d6a3e)',t:'#e9dcc6'});
  V+=light(300,228,96,22)+light(185,330,96,22)+light(110,250,90,18);
  /* columns */
  V+=box({x:14,y:256,w:10,d:10,h:119,z:12,l:conL,f:conF})+box({x:362,y:256,w:10,d:10,h:1,z:12});
  /* upper volume B (cantilever) */
  V+=box({x:10,y:70,w:390,d:200,h:100,z:132,b:inW,r:inW,l:woodL,
    f:'linear-gradient(180deg,var(--w2) 0 22px,transparent 22px calc(100% - 16px),var(--w3) calc(100% - 16px)),'+glass,fc:'vglass',
    t:conT,ti:panels(6,3,22,26,54,40,6,18)+'<div style="position:absolute;inset:0;box-shadow:inset 0 0 0 7px var(--w1)"></div>'});
  V+=box({x:280,y:262,w:120,d:8,h:100,z:132,f:woodF});
  V+=light(150,200,212,18)+light(260,190,212,18);
  /* parapets */
  V+=box({x:10,y:262,w:390,d:8,h:9,z:232,l:conL,f:conF,t:'var(--w0)'})+box({x:10,y:70,w:8,d:200,h:9,z:232,l:conL,f:conF,t:'var(--w0)'});
  /* annex C with battery */
  V+=box({x:400,y:60,w:210,d:140,h:92,z:12,l:conL,
    f:woodF,fi:'<div class="vgar" style="left:22px;bottom:0;width:100px;height:66px"></div><div class="vbat" style="right:28px;bottom:14px"></div><div style="position:absolute;right:66px;bottom:44px;width:40px;height:16px;background:linear-gradient(180deg,var(--in1),var(--in2));box-shadow:inset 0 0 0 3px var(--fr),0 0 26px var(--glow)"></div>',
    t:conT,ti:panels(3,2,18,22,52,38,8,20)});
  /* terrace plants on A roof, garden */
  V+=bill(70,340,132,30,30,'vbush')+bill(130,350,132,24,24,'vbush')+bill(330,346,132,28,28,'vbush');
  V+=bill(-26,40,0,40,190,'vplant')+bill(-34,140,0,34,150,'vplant')+bill(-4,330,0,30,120,'vplant')+bill(644,30,0,42,200,'vplant')+bill(668,110,0,34,150,'vplant')+bill(634,300,0,30,130,'vplant');
  V+=bill(110,436,0,40,40,'vbush')+bill(160,440,0,30,30,'vbush')+bill(300,438,0,36,36,'vbush')+bill(360,436,0,26,26,'vbush');
  [[70,424],[250,426],[392,430],[616,426]].forEach(function(p){V+=box({x:p[0],y:p[1],w:6,d:6,h:22,z:12,l:'#2c2722',f:'#25211d',t:'var(--lamp)'})+light(p[0]+3,p[1]+3,40,16)});
  /* ---------- isometric terrain ---------- */
  var tr=mk(31);
  function spr(x,y,z,w,h,cls,shadow){
    var o='<div class="vb" style="left:'+x+'px;top:'+y+'px;width:0;height:0;transform:translateZ('+(z||0)+'px)">';
    if(shadow)o+='<div class="vtsh" style="left:'+(-w*.7)+'px;top:'+(-w*.15)+'px;width:'+(w*1.5)+'px;height:'+(w*.95)+'px"></div>';
    return o+F('left:'+(-w/2)+'px;top:'+(-h)+'px;width:'+w+'px;height:'+h+'px;transform-origin:50% 100%;transform:var(--face)','',cls)+'</div>';
  }
  var soilF='radial-gradient(circle at 30% 40%,rgba(255,255,255,.07) 0 2px,transparent 3px) 0 0/38px 30px,radial-gradient(circle at 70% 70%,rgba(0,0,0,.12) 0 3px,transparent 4px) 0 0/52px 40px,linear-gradient(180deg,var(--gr2) 0 8px,var(--so1) 8px 24%,var(--so2) 24% 60%,var(--so3) 60%)';
  var soilL='radial-gradient(circle at 30% 40%,rgba(255,255,255,.07) 0 2px,transparent 3px) 0 0/30px 38px,radial-gradient(circle at 70% 70%,rgba(0,0,0,.12) 0 3px,transparent 4px) 0 0/40px 52px,linear-gradient(90deg,var(--gr2) 0 8px,color-mix(in srgb,var(--so1) 88%,#fff) 8px 24%,color-mix(in srgb,var(--so2) 90%,#fff) 24% 60%,color-mix(in srgb,var(--so3) 92%,#fff) 60%)';
  var lawn='radial-gradient(60% 40% at 30% 30%,rgba(255,240,190,.28),transparent 70%),repeating-linear-gradient(90deg,rgba(255,255,255,.045) 0 70px,rgba(0,0,0,.03) 70px 140px),linear-gradient(135deg,var(--gr1),var(--gr2))';
  function wall(dir,mix){var c1='color-mix(in srgb,var(--sw1) '+mix+'%,var(--hz))',c2='color-mix(in srgb,var(--sw2) '+mix+'%,var(--hz))',g='color-mix(in srgb,var(--gr2) '+mix+'%,var(--hz))';
    return 'repeating-linear-gradient('+(dir?'90deg':'180deg')+',transparent 0 19px,rgba(60,40,20,.18) 19px 21px),repeating-linear-gradient('+(dir?'180deg':'90deg')+',transparent 0 38px,rgba(60,40,20,.12) 38px 40px),linear-gradient('+(dir?'90deg':'180deg')+','+g+' 0 7px,'+c1+' 7px,'+c2+')'}
  function topMix(mix,extra){return (extra?extra+',':'')+'linear-gradient(135deg,color-mix(in srgb,var(--gr1) '+mix+'%,var(--hz)),color-mix(in srgb,var(--gr2) '+mix+'%,var(--hz)))'}
  var T='';
  /* path, patio, shadows drawn on the lawn (slab-local coords = villa + (200,260)) */
  var lawnDeco='<div class="vshadow" style="left:150px;top:210px;width:700px;height:470px;opacity:.75"></div>';
  for(var k=0;k<11;k++){var t=k/10,px=150+38*Math.sin(t*Math.PI*1.1),py=470+t*520;lawnDeco+='<div class="vstone" style="left:'+(px+200-38).toFixed(0)+'px;top:'+(py+180-18).toFixed(0)+'px;width:'+(70+tr()*10).toFixed(0)+'px;height:'+(34+tr()*6).toFixed(0)+'px;transform:rotate('+((tr()-.5)*14).toFixed(1)+'deg)"></div>'}
  lawnDeco+='<div class="vstone" style="left:'+(-150+200)+'px;top:'+(560+180)+'px;width:190px;height:190px;border-radius:50%"></div>';
  T+=box({x:-200,y:-180,w:1160,d:1180,h:110,z:-110,l:soilL,f:soilF,t:lawn,ti:lawnDeco});
  /* lavender bed + hedge */
  T+=box({x:-176,y:20,w:110,d:430,h:18,z:0,l:wall(1,100),f:wall(0,100),t:'radial-gradient(circle,rgba(255,255,255,.25) 0 1.5px,transparent 2.5px) 0 0/9px 11px,repeating-linear-gradient(90deg,var(--lav) 0 15px,var(--gr2) 15px 22px)'});
  T+=box({x:690,y:30,w:34,d:420,h:30,z:0,l:'linear-gradient(90deg,var(--tr1),var(--tr2))',f:'linear-gradient(180deg,var(--tr1),var(--tr3))',t:'radial-gradient(circle at 30% 30%,var(--tr1),var(--tr2))'});
  T+=box({x:-176,y:820,w:110,d:150,h:18,z:0,l:wall(1,100),f:wall(0,100),t:'radial-gradient(circle,rgba(255,255,255,.25) 0 1.5px,transparent 2.5px) 0 0/9px 11px,repeating-linear-gradient(90deg,var(--lav) 0 15px,var(--gr2) 15px 22px)'});
  /* fire pit on the patio */
  T+=box({x:-72,y:640,w:34,d:34,h:10,z:0,l:'#5a554f',f:'#4a4540',t:'radial-gradient(circle,#2a1d14 0 40%,#6a625a 42%)'});
  T+='<div class="vb" style="left:-55px;top:657px;width:0;height:0">'+F('left:-22px;top:-44px;width:44px;height:44px;transform-origin:50% 100%;transform:translateZ(10px) var(--face)','','vfire')+'</div>';
  /* terraces: olive grove, then vineyard */
  /* trees */
  for(var cx=300;cx<950;cx+=58+tr()*24){var ch=118+tr()*70;T+=spr(cx,-160+tr()*12,0,28+tr()*10,ch,'vcyp',1)}
  [[-120,300,1.2],[-60,560,1],[430,640,1.15],[620,780,1.3],[860,520,1.1],[860,120,.95],[880,860,1.2]].forEach(function(o){T+=spr(o[0],o[1],0,84*o[2],96*o[2],'volive',1)});
  [[260,520],[330,560],[30,470],[540,500],[900,300],[-150,700],[780,640]].forEach(function(o){T+=spr(o[0],o[1],0,30,26,'vbush',1)});
  /* path bollards + night pools */
  for(k=1;k<10;k+=2){var t2=k/10,bx=150+38*Math.sin(t2*Math.PI*1.1),by=470+t2*520;[-62,62].forEach(function(dx){var X=bx+dx,Y=by;T+=box({x:X,y:Y,w:6,d:6,h:22,z:0,l:'#2c2722',f:'#25211d',t:'var(--lamp)'})+'<div class="vpool" style="left:'+(X-40)+'px;top:'+(Y-40)+'px;width:86px;height:86px"></div>'+light(X+3,Y+3,26,14)})}
  T+='<div class="vpool" style="left:-150px;top:560px;width:200px;height:200px"></div>';
  T+='<div class="vpool" style="left:20px;top:440px;width:340px;height:120px"></div><div class="vpool" style="left:380px;top:230px;width:260px;height:200px"></div>';
  for(k=0;k<26;k++)T+='<div class="vb" style="left:'+(-150+tr()*1050).toFixed(0)+'px;top:'+(-120+tr()*1050).toFixed(0)+'px;width:0;height:0;transform:translateZ('+(18+tr()*60).toFixed(0)+'px)">'+F('left:-2px;top:-2px;width:4px;height:4px;transform:var(--face);animation-delay:-'+(tr()*5).toFixed(1)+'s','','vfly')+'</div>';
  $('#villa').innerHTML=T+V;

  /* pointer parallax */
  var villa=$('#villa'),tx=0,ty=0,cx=0,cy=0,raf=0;
  function tick(){cx+=(tx-cx)*.08;cy+=(ty-cy)*.08;villa.style.setProperty('--rz',(-38+cx*7).toFixed(2)+'deg');villa.style.setProperty('--rx',(58+cy*5).toFixed(2)+'deg');raf=(Math.abs(tx-cx)+Math.abs(ty-cy)>.001)?requestAnimationFrame(tick):0}
  if(!RM)$('#hero').addEventListener('pointermove',function(e){tx=e.clientX/window.innerWidth-.5;ty=e.clientY/window.innerHeight-.5;if(!raf)raf=requestAnimationFrame(tick)});
})();

/* ============ Generic scenery ============ */
function hillPath(W,H,y,amp,r){var pts=[],n=5;for(var i=0;i<=n;i++)pts.push([W*i/n,y+(r()-.5)*amp]);return line(pts)+' L'+W+' '+H+' L0 '+H+'Z'}
function scene(id,o){
  var svg=document.getElementById(id);if(!svg)return;
  var W=o.w,H=o.h,p=id,r=mk(o.seed||7),s='';
  s+='<defs><linearGradient id="'+p+'sky" x1="0" y1="0" x2="0" y2="1">'+o.sky.map(function(st){return '<stop offset="'+st[0]+'" stop-color="'+st[1]+'"/>'}).join('')+'</linearGradient>'+
    '<radialGradient id="'+p+'bl"><stop offset="0" stop-color="'+o.glow+'" stop-opacity=".9"/><stop offset=".15" stop-color="'+o.glow+'" stop-opacity=".45"/><stop offset=".45" stop-color="'+o.glow+'" stop-opacity=".12"/><stop offset="1" stop-color="'+o.glow+'" stop-opacity="0"/></radialGradient>'+
    '<linearGradient id="'+p+'hz" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="'+o.haze+'" stop-opacity="0"/><stop offset=".5" stop-color="'+o.haze+'" stop-opacity="'+(o.hazeOp||.4)+'"/><stop offset="1" stop-color="'+o.haze+'" stop-opacity="0"/></linearGradient>'+
    '<linearGradient id="'+p+'ray" x1="0" x2="1"><stop offset="0" stop-color="'+o.glow+'" stop-opacity=".5"/><stop offset="1" stop-color="'+o.glow+'" stop-opacity="0"/></linearGradient>'+
    '<radialGradient id="'+p+'pool"><stop offset="0" stop-color="#ffc978" stop-opacity=".5"/><stop offset="1" stop-color="#ffc978" stop-opacity="0"/></radialGradient>'+
    '<filter id="'+p+'gl" x="-200%" y="-200%" width="500%" height="500%"><feGaussianBlur stdDeviation="2.5" result="b"/><feMerge><feMergeNode in="b"/><feMergeNode in="SourceGraphic"/></feMerge></filter></defs>';
  s+='<rect width="'+W+'" height="'+H+'" fill="url(#'+p+'sky)"/>';
  var i;
  if(o.stars){s+='<g fill="#fff">';for(i=0;i<o.stars;i++)s+='<circle class="tw" cx="'+(r()*W).toFixed(0)+'" cy="'+(r()*H*.55).toFixed(0)+'" r="'+(r()*1.1+.3).toFixed(2)+'" style="animation-delay:'+(r()*3.6).toFixed(2)+'s"/>';s+='</g>'}
  if(o.body){var b=o.body;s+='<g transform="translate('+b[0]+' '+b[1]+')">'+(o.rays?rays(18,b[2]*16,p+'ray',.35).replace(/url\(#gRay\)/g,''):'')+'<circle r="'+(b[2]*9)+'" fill="url(#'+p+'bl)"/><circle r="'+b[2]+'" fill="'+o.core+'"/></g>'}
  var lights='';
  o.hills.forEach(function(hl,k){
    s+='<path d="'+hillPath(W,H,hl[0],hl[1],r)+'" fill="'+hl[2]+'"/>';
    (o.houses||[]).filter(function(h){return h[2]===k}).forEach(function(h){var hh=house(h[0],hl[0]+hl[1]/2,h[1],o.hc);s+=hh[0];if(o.lit){lights+=hh[1];s+='<ellipse cx="'+h[0]+'" cy="'+(hl[0]+hl[1]/2+2)+'" rx="'+(40*h[1])+'" ry="'+(6*h[1])+'" fill="url(#'+p+'pool)"/>'}});
    if(o.lit&&lights){s+='<g fill="#ffcf7a" filter="url(#'+p+'gl)">'+lights+'</g>';lights=''}
    if(o.trees)(o.trees[k]||[]).forEach(function(t){s+='<path d="'+(function(x,y,h,w){return 'M'+x+' '+y+' C '+(x-w)+' '+(y-h*.35)+' '+(x-w*.6)+' '+(y-h*.8)+' '+x+' '+(y-h)+' C '+(x+w*.6)+' '+(y-h*.8)+' '+(x+w)+' '+(y-h*.35)+' '+x+' '+y+'Z'})(t[0],hl[0]+hl[1]/2+4,t[1],t[1]*.2)+'" fill="'+hl[2]+'"/>'});
    if(k<o.hills.length-1)s+='<rect y="'+(hl[0]-hl[1])+'" width="'+W+'" height="'+(hl[1]*2.6)+'" fill="url(#'+p+'hz)"/>';
  });
  if(o.flies){s+='<g fill="#ffe7a0" filter="url(#'+p+'gl)">';for(i=0;i<o.flies;i++){var d=(4+r()*4).toFixed(1);s+='<circle cx="'+(r()*W).toFixed(0)+'" cy="'+(H*.72+r()*H*.25).toFixed(0)+'" r="1.4"><animate attributeName="opacity" values="0;1;0" dur="'+d+'s" begin="'+(r()*4).toFixed(1)+'s" repeatCount="indefinite"/></circle>'}s+='</g>'}
  svg.innerHTML=s;
}
scene('fcScene',{w:1200,h:700,seed:3,sky:[[0,'#163322'],[.4,'#42694d'],[.7,'#c9ae79'],[.86,'#f3cf93'],[1,'#f6dca9']],glow:'#ffe2a6',core:'#fff4da',body:[880,500,30],rays:1,haze:'#fbe6bb',hazeOp:.5,
  hills:[[520,44,'#8aa07a'],[574,50,'#668561'],[630,40,'#466845'],[680,30,'#2a4a30']],houses:[[640,.9,0],[720,.7,0],[300,.8,1],[1040,1.1,1],[1120,.8,1],[180,1.3,2]],hc:{body:'#eae3d3',roof:'#4a5058',pv:'#4b7fb5'},
  trees:[[ [560,60],[800,50] ],[ [380,80],[960,90] ],[ [90,120],[1180,110] ]]});
scene('duskScene',{w:900,h:600,seed:11,sky:[[0,'#0e2219'],[.38,'#2a4a3d'],[.62,'#7c5f52'],[.8,'#d48a52'],[1,'#f0b26e']],glow:'#ffb877',core:'#ffe1b0',body:[640,420,22],rays:1,haze:'#f2a86a',hazeOp:.35,stars:30,
  hills:[[430,36,'#3c4a3c'],[480,40,'#2a3a2e'],[530,34,'#1b2a20'],[575,24,'#101c14']],houses:[[200,.8,0],[260,.6,0],[720,.9,1],[790,.7,1],[120,1.2,2],[460,1,2]],hc:{body:'#c9b9a2',roof:'#2c3036',pv:'#3a5a80'},lit:1,
  trees:[[[420,40]],[[560,70],[880,60]],[[300,90],[860,100]]]});
scene('nightScene',{w:1400,h:800,seed:5,sky:[[0,'#040b14'],[.45,'#0e2232'],[.75,'#24425a'],[1,'#3d6070']],glow:'#d8e6fa',core:'#f4f7fb',body:[1180,150,24],haze:'#6d8fa6',hazeOp:.35,stars:170,flies:30,
  hills:[[560,40,'#2b4a52'],[620,46,'#1e3a3c'],[690,40,'#13281f']],houses:[[200,.9,0],[300,.7,0],[860,.9,0],[1240,1,0],[120,1.3,1],[420,1.2,1],[640,1.5,1],[1080,1.3,1],[300,2.4,2],[1260,2,2]],hc:{body:'#c9c6ba',roof:'#22272c',pv:'#2c4766'},lit:1,
  trees:[[[60,60],[560,50],[1340,50]],[[260,90],[880,100],[1180,90]],[[90,140],[560,130],[1000,150]]]});

/* About: golden-hour rooftop */
(function(){
  var svg=$('#roofArt'),W=800,H=1000,r=mk(19),s='',i,k;
  s+='<defs><linearGradient id="rSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#6f9cc4"/><stop offset=".32" stop-color="#bccfd6"/><stop offset=".52" stop-color="#f0d4a2"/><stop offset=".64" stop-color="#f6b779"/><stop offset="1" stop-color="#ee9b5c"/></linearGradient>'+
    '<radialGradient id="rBl"><stop offset="0" stop-color="#fff3d2"/><stop offset=".08" stop-color="#ffe2a2" stop-opacity=".9"/><stop offset=".3" stop-color="#ffc77e" stop-opacity=".35"/><stop offset="1" stop-color="#ffc77e" stop-opacity="0"/></radialGradient>'+
    '<linearGradient id="rRay" x1="0" x2="1"><stop offset="0" stop-color="#fff0cf" stop-opacity=".55"/><stop offset="1" stop-color="#fff0cf" stop-opacity="0"/></linearGradient>'+
    '<linearGradient id="rRoof" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#4a4f57"/><stop offset="1" stop-color="#1c2025"/></linearGradient>'+
    '<linearGradient id="rPv" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#3e74ae"/><stop offset=".5" stop-color="#1d4677"/><stop offset="1" stop-color="#0f2643"/></linearGradient>'+
    '<radialGradient id="rRef" cx=".5" cy=".5" r=".5"><stop offset="0" stop-color="#fff4d8" stop-opacity=".95"/><stop offset=".3" stop-color="#ffd69a" stop-opacity=".55"/><stop offset="1" stop-color="#ffb870" stop-opacity="0"/></radialGradient>'+
    '<linearGradient id="rHz" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffe0b0" stop-opacity="0"/><stop offset=".5" stop-color="#ffe0b0" stop-opacity=".55"/><stop offset="1" stop-color="#ffe0b0" stop-opacity="0"/></linearGradient>'+
    '<filter id="rGl" x="-50%" y="-50%" width="200%" height="200%"><feGaussianBlur stdDeviation="2"/></filter></defs>';
  s+='<rect width="'+W+'" height="'+H+'" fill="url(#rSky)"/>';
  s+='<g transform="translate(590 545)">'+rays(20,700,'rRay',.4)+'<circle r="420" fill="url(#rBl)"/><circle r="34" fill="#fff8e6"/></g>';
  s+='<path d="'+hillPath(W,H,600,30,r)+'" fill="#9c9a86" opacity=".75"/>';
  // neighborhood rooftops
  var x=-20;while(x<W){var w=50+r()*60,h=22+r()*24,y=618+r()*14;s+='<polygon points="'+x+','+y+' '+(x+w*.2)+','+(y-h)+' '+(x+w*.8)+','+(y-h)+' '+(x+w)+','+y+'" fill="#6f6f68" opacity=".8"/><rect x="'+x+'" y="'+y+'" width="'+w+'" height="40" fill="#837f72" opacity=".8"/>';if(r()>.5)s+='<polygon points="'+(x+w*.28)+','+(y-h*.15)+' '+(x+w*.34)+','+(y-h*.85)+' '+(x+w*.66)+','+(y-h*.85)+' '+(x+w*.72)+','+(y-h*.15)+'" fill="#ffdca0" opacity=".55"/>';x+=w+8+r()*20}
  s+='<rect y="560" width="'+W+'" height="140" fill="url(#rHz)"/>';
  for(i=0;i<14;i++){var tx=r()*W;s+=cypress(tx,660,50+r()*60,12+r()*8).replace('url(#gCyp)','#5d6b4f')}
  s+='<rect y="610" width="'+W+'" height="90" fill="url(#rHz)" opacity=".7"/>';
  // roof plane
  var TL=[-60,712],TR=[860,596],BR=[860,1000],BL=[-60,1000];
  s+='<polygon points="'+[TL,TR,BR,BL].map(function(a){return a.join(',')}).join(' ')+'" fill="url(#rRoof)"/>';
  s+='<polygon points="-60,704 860,588 860,600 -60,716" fill="#2a2e34"/><polygon points="-60,704 860,588 860,591 -60,707" fill="#ffd08a" opacity=".85"/>';
  function bil(u,v){var a=[lerp(TL[0],TR[0],u),lerp(TL[1],TR[1],u)],b=[lerp(BL[0],BR[0],u),lerp(BL[1],BR[1],u)];return [lerp(a[0],b[0],v),lerp(a[1],b[1],v)]}
  var R=3,C=4,clip='',pan='';
  for(var rr=0;rr<R;rr++)for(var cc=0;cc<C;cc++){
    var u0=.08+cc*(.86/C)+.008,u1=.08+(cc+1)*(.86/C)-.008,v0=Math.pow(.06+rr*(.9/R)+.012,1.25),v1=Math.pow(.06+(rr+1)*(.9/R)-.012,1.25);
    var P=[bil(u0,v0),bil(u1,v0),bil(u1,v1),bil(u0,v1)],pts=P.map(function(a){return a[0].toFixed(1)+','+a[1].toFixed(1)}).join(' ');
    clip+='<polygon points="'+pts+'"/>';
    pan+='<polygon points="'+pts+'" fill="url(#rPv)" stroke="#d7dee5" stroke-width="2.4"/>';
    var ls='';for(k=1;k<6;k++){var a=bil(u0+(u1-u0)*k/6,v0),b=bil(u0+(u1-u0)*k/6,v1);ls+='M'+a[0].toFixed(1)+' '+a[1].toFixed(1)+'L'+b[0].toFixed(1)+' '+b[1].toFixed(1)}
    for(k=1;k<4;k++){var a2=bil(u0,v0+(v1-v0)*k/4),b2=bil(u1,v0+(v1-v0)*k/4);ls+='M'+a2[0].toFixed(1)+' '+a2[1].toFixed(1)+'L'+b2[0].toFixed(1)+' '+b2[1].toFixed(1)}
    pan+='<path d="'+ls+'" stroke="#bcd3ea" stroke-opacity=".22" stroke-width="1"/>';
  }
  s+='<clipPath id="rClip">'+clip+'</clipPath>'+pan;
  s+='<g clip-path="url(#rClip)"><ellipse cx="560" cy="700" rx="300" ry="90" fill="url(#rRef)"/><g transform="skewX(-30)"><rect x="200" y="560" width="120" height="460" fill="#fff" opacity=".1"><animate attributeName="x" values="200;1300" dur="9s" repeatCount="indefinite"/></rect></g></g>';
  // flare
  [[470,700,26,.18],[380,800,14,.22],[320,860,40,.08],[250,940,9,.25]].forEach(function(f){s+='<circle cx="'+f[0]+'" cy="'+f[1]+'" r="'+f[2]+'" fill="#ffe2ac" opacity="'+f[3]+'"/>'});
  // motes
  s+='<g fill="#fff3d0" filter="url(#rGl)">';for(i=0;i<26;i++){var d=(6+r()*6).toFixed(1);s+='<circle cx="'+(r()*W).toFixed(0)+'" cy="'+(300+r()*400).toFixed(0)+'" r="'+(1+r()*1.6).toFixed(1)+'" opacity=".7"><animateTransform attributeName="transform" type="translate" values="0 0;'+(20+r()*30).toFixed(0)+' -'+(20+r()*40).toFixed(0)+'" dur="'+d+'s" repeatCount="indefinite"/><animate attributeName="opacity" values="0;.8;0" dur="'+d+'s" repeatCount="indefinite"/></circle>'}s+='</g>';
  svg.innerHTML=s;
})();

/* Phone chart */
(function(){
  var sol=[0,.4,1.4,2.7,3.9,4.9,5.6,5.9,5.8,5.3,4.4,3.2,1.9,.8,.1];
  var pts=sol.map(function(v,i){return [i/(sol.length-1)*100,58-v/6.2*54]});
  var d=line(pts);var pk=7;
  $('#phoneChart').innerHTML='<defs><linearGradient id="phG" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f4b23f" stop-opacity=".55"/><stop offset="1" stop-color="#f4b23f" stop-opacity="0"/></linearGradient></defs><path d="'+d+' L100,60 L0,60Z" fill="url(#phG)"/><path d="'+d+'" fill="none" stroke="#ffcb6b" stroke-width="2" stroke-linecap="round" vector-effect="non-scaling-stroke"/>';
  $('.ph-chart').insertAdjacentHTML('beforeend','<span style="position:absolute;left:'+pts[pk][0]+'%;top:'+(pts[pk][1]/60*100)+'%;width:10px;height:10px;border-radius:50%;background:#fff3d6;transform:translate(-50%,-50%);box-shadow:0 0 0 2px #0b1f14,0 0 14px 4px rgba(244,178,63,.8)"></span>');
})();

if(RM){$$('svg').forEach(function(s){if(s.pauseAnimations)s.pauseAnimations()})}

/* ============ Split headings ============ */
$$('[data-split]').forEach(function(el){
  var txt=el.textContent.trim(),d=+(el.getAttribute('data-delay')||0),words=txt.split(/\s+/);
  el.innerHTML='<span class="sr-only">'+txt+'</span><span aria-hidden="true">'+words.map(function(w,i){return '<span class="w"><span style="--i:'+(i+d)+'">'+w+'</span></span>'}).join(' ')+'</span>';
});

/* ============ Manifesto ============ */
var pills={
  sun:'<svg viewBox="0 0 190 78" preserveAspectRatio="xMidYMid slice"><defs><linearGradient id="ms1" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#8fb3cf"/><stop offset=".55" stop-color="#f3d4a0"/><stop offset="1" stop-color="#f3a964"/></linearGradient><radialGradient id="ms2"><stop offset="0" stop-color="#fff6de"/><stop offset=".2" stop-color="#ffdf9d" stop-opacity=".8"/><stop offset="1" stop-color="#ffdf9d" stop-opacity="0"/></radialGradient></defs><rect width="190" height="78" fill="url(#ms1)"/><circle cx="96" cy="58" r="70" fill="url(#ms2)"/><circle cx="96" cy="58" r="13" fill="#fff8e8"/><path d="M0 62 C 50 54 120 64 190 56 L190 78 L0 78Z" fill="#6f8f5a"/></svg>',
  house:'<svg viewBox="0 0 190 78" preserveAspectRatio="xMidYMid slice"><defs><linearGradient id="mh1" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#0a1424"/><stop offset="1" stop-color="#2d3a55"/></linearGradient></defs><rect width="190" height="78" fill="url(#mh1)"/><g fill="#fff" opacity=".8"><circle cx="20" cy="14" r="1"/><circle cx="160" cy="10" r="1.2"/><circle cx="120" cy="22" r=".8"/><circle cx="40" cy="30" r=".7"/></g><path d="M0 66 C 60 60 130 68 190 62 L190 78 L0 78Z" fill="#141e2a"/><rect x="66" y="40" width="60" height="26" fill="#2e3846"/><polygon points="60,41 76,24 116,24 132,41" fill="#141a22"/><polygon points="70,39 80,28 112,28 122,39" fill="#2a4767"/><rect x="72" y="46" width="22" height="14" fill="#ffc874"/><rect x="104" y="46" width="12" height="14" fill="#ffc874"/><ellipse cx="96" cy="68" rx="50" ry="5" fill="#ffc874" opacity=".3"/></svg>',
  battery:'<svg viewBox="0 0 190 78" preserveAspectRatio="xMidYMid slice"><defs><linearGradient id="mb1" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#103322"/><stop offset="1" stop-color="#0b1f14"/></linearGradient><linearGradient id="mb2" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#f4b23f"/><stop offset="1" stop-color="#57c76a"/></linearGradient></defs><rect width="190" height="78" fill="url(#mb1)"/><rect x="38" y="22" width="104" height="34" rx="9" fill="none" stroke="#dfeee2" stroke-opacity=".7" stroke-width="3"/><rect x="144" y="32" width="6" height="14" rx="2" fill="#dfeee2" fill-opacity=".7"/><rect x="44" y="28" width="80" height="22" rx="5" fill="url(#mb2)" style="filter:drop-shadow(0 0 6px rgba(87,199,106,.8))"/></svg>'
};
(function(){
  var M=[['Your roof rarely runs short of sun.',''],['@sun'],['It runs short of timing.','pr'],['Lumora reads the weather,',''],['@house'],['your home and your utility rates as one system, so every kilowatt-hour',''],['@battery'],['your panels make lands in the hour',''],['it saves you the most.','pr']];
  var html='<span aria-hidden="true">';
  M.forEach(function(sg){
    if(sg[0].charAt(0)==='@'){html+='<span class="mpill">'+pills[sg[0].slice(1)]+'</span> ';return}
    sg[0].split(' ').forEach(function(w){html+='<span class="mw '+sg[1]+'">'+w+'</span> '});
  });
  $('#mText').insertAdjacentHTML('beforeend',html+'</span>');
})();
var mTokens=$$('#mText .mw, #mText .mpill');

/* ============ Reveal ============ */
var io=new IntersectionObserver(function(es){es.forEach(function(e){if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target);if(e.target._onIn)e.target._onIn()}})},{rootMargin:'0px 0px -12% 0px',threshold:.08});
$$('.reveal,.split:not(#hero .split),.tl,.cells,.bars,.wordmark,.stat').forEach(function(el){io.observe(el)});

/* ============ Intro ============ */
var cur=$('#curtain');
function start(){
  if(cur.classList.contains('out'))return;
  cur.classList.add('out');
  setTimeout(function(){document.body.classList.add('loaded');$$('#hero .split').forEach(function(e){e.classList.add('in')})},RM?0:250);
  setTimeout(function(){cur.style.display='none'},1300);
}
if(RM){cur.style.display='none';document.body.classList.add('loaded');$$('#hero .split').forEach(function(e){e.classList.add('in')})}
else{window.addEventListener('load',function(){setTimeout(start,700)});setTimeout(start,2600)}

/* ============ Hero day / evening ============ */
var hero=$('#hero'),cap=$('#heroCap'),mode='day';
var caps={day:'Lumora forecasts tomorrow’s sunshine for your roof and fills your battery from the panels, not the grid.',night:'When rates peak after sunset, Lumora runs your home on stored sunshine, so the evening costs you next to nothing.'};
var live={day:{s:5.0,h:1.1,b:71},night:{s:0,h:2.9,b:86}};
function paintChips(){
  var L=live[mode],e;
  if(e=$('#cSolar'))e.textContent=f1(L.s)+' kW';
  if(e=$('#cHome'))e.textContent=f1(L.h)+' kW';
  var flow=mode==='day'?Math.max(.4,L.s-L.h-1.2):-(L.h-1.1);
  if(e=$('#cBatt'))e.textContent=L.b+'% · '+(flow>=0?'+':'−')+f1(Math.abs(flow))+' kW';
  if(e=$('#mtSolar'))e.textContent=f1(live.day.s)+' kW';
  if(e=$('#mtBatt'))e.textContent=live.day.b+'%';
  $$('#bSolar i').forEach(function(b,j){b.style.height=(mode==='day'?[8,10,13,16,20,25,30,36,42][j]:3)+'px'});
}
$$('[data-tod]').forEach(function(b){b.addEventListener('click',function(){
  mode=b.dataset.tod==='night'?'night':'day';hero.classList.toggle('is-night',mode==='night');
  $$('[data-tod]').forEach(function(x){x.setAttribute('aria-pressed',x===b)});
  cap.style.opacity=0;cap.style.transform='translateY(6px)';
  setTimeout(function(){cap.textContent=caps[mode];cap.style.opacity=1;cap.style.transform='none'},250);
  paintChips();onScroll();
})});
setInterval(function(){
  if(document.hidden)return;
  var d=live.day,n=live.night;
  d.s=clamp(d.s+(Math.random()-.5)*.24,4.7,5.4);d.h=clamp(d.h+(Math.random()-.5)*.14,.9,1.4);if(Math.random()<.35)d.b=d.b<99?d.b+1:71;
  n.h=clamp(n.h+(Math.random()-.5)*.26,2.5,3.3);if(Math.random()<.3)n.b=n.b>40?n.b-1:86;
  paintChips();
},2400);

/* ============ Header + menu ============ */
var header=$('#header'),menuBtn=$('#menuBtn'),menu=$('#mobileMenu'),lastY=0;
menuBtn.addEventListener('click',function(){var o=menu.hidden;menu.hidden=!o;menuBtn.setAttribute('aria-expanded',o);menuBtn.setAttribute('aria-label',o?'Close menu':'Open menu');menuBtn.querySelector('use').setAttribute('href',o?'#i-x':'#i-menu');onScroll()});
$$('#mobileMenu a').forEach(function(a){a.addEventListener('click',function(){menu.hidden=true;menuBtn.setAttribute('aria-expanded','false');menuBtn.querySelector('use').setAttribute('href','#i-menu')})});

/* ============ Dashboard ============ */
var hrs=[];for(var h=0;h<24;h++)hrs.push((h<10?'0':'')+h+':00');
var uF=[.52,.46,.42,.40,.41,.55,.95,1.45,1.30,.95,.80,.78,.85,.82,.90,1.20,1.85,2.65,3.10,2.95,2.40,1.70,1.05,.70];
var uA=[.50,.47,.43,.39,.42,.58,.98,1.41,1.34,.92,.83,.75,.88,.80,.93];
var sT=[0,0,0,0,0,0,.15,.8,1.9,3.1,4.2,5.0,5.5,5.6,5.2,4.4,3.2,1.9,.7,.1,0,0,0,0];
var band=function(a,p){return [a.map(function(v,i){return v*(1-p-i*.002)}),a.map(function(v,i){return v*(1+p+i*.002)})]};
var bT=band(uF,.08),uF2=uF.map(function(v){return v*1.04}),bT2=band(uF2,.12);
var wkU=[28.4,31.2,26.9,25.8,30.6,32.1,29.4],wkS=[38.6,27.8,41.2,40.4,22.5,35.0,39.1],bW=band(wkU,.06);
var DATA={
  today:{f:uF,a:uA,lo:bT[0],hi:bT[1],s:sT,lab:hrs,now:14,ymax:6,unit:'kW',sub:'Power in kW, actuals up to 14:00',ticks:[0,3,6,9,12,15,18,21],peakL:'Evening peak',
    k:{solarL:'Solar today',solar:'31.4',solarD:['up','+12% vs yesterday',1],batt:86,battD:['','11.6 of 13.5 kWh stored',0],grid:'2.1',gridD:['down','68% less than last Monday',1],saveL:'Saved today',save:'$4.80',saveD:['up','On track for $96 this month',1]},mix:[58,31,11]},
  tomorrow:{f:uF2,a:[],lo:bT2[0],hi:bT2[1],s:sT.map(function(v,i){return v*(i<11?.95:.58)}),lab:hrs,now:null,ymax:6,unit:'kW',sub:'Power in kW, forecast',ticks:[0,3,6,9,12,15,18,21],peakL:'Evening peak',
    k:{solarL:'Solar tomorrow',solar:'22.6',solarD:['down','Clouds roll in after 11:00',0],batt:100,battD:['','Storm Watch fills it by 10:30',1],grid:'4.3',gridD:['down','Still 55% less than usual',1],saveL:'Expected savings',save:'$3.20',saveD:['','Lower sun, evening still covered',0]},mix:[49,34,17]},
  week:{f:wkU,a:[],lo:bW[0],hi:bW[1],s:wkS,lab:['Mon','Tue','Wed','Thu','Fri','Sat','Sun'],now:null,ymax:48,unit:'kWh',sub:'Daily energy in kWh, this week',ticks:[0,1,2,3,4,5,6],peakL:'Highest use',
    k:{solarL:'Solar this week',solar:'244.6',solarD:['up','Sunniest day: Wednesday',1],batt:92,battD:['','Average charge at sunset',0],grid:'21.8',gridD:['down','61% less than a typical week',1],saveL:'Expected this week',save:'$29.40',saveD:['up','About $1,530 a year at this pace',1]},mix:[55,32,13]}
};
var curRange='today',CD=DATA.today,chartSvg=$('#chartSvg');
function delta(el,d){el.className='d'+(d[2]?' good':'');el.innerHTML=(d[0]?'<svg class="ic"><use href="#i-'+d[0]+'"/></svg>':'')+'<span>'+d[1]+'</span>'}
function renderChart(key,animate){
  var D=DATA[key];CD=D;var n=D.f.length;
  var X=function(i){return i/(n-1)*1000},Y=function(v){return 300-v/D.ymax*300};
  var P=function(arr){return arr.map(function(v,i){return [X(i),Y(v)]})};
  var hi=P(D.hi),lo=P(D.lo).reverse();
  $('#pBand').setAttribute('d',line(hi)+' L'+lo[0][0]+','+lo[0][1].toFixed(2)+seg(lo)+'Z');
  var sp=P(D.s);$('#pS').setAttribute('d',line(sp));$('#pSF').setAttribute('d',line(sp)+' L1000,300 L0,300Z');
  $('#pF').setAttribute('d',line(P(D.f)));
  if(D.a.length>1){var ap=P(D.a);$('#pA').setAttribute('d',line(ap));$('#pAFill').setAttribute('d',line(ap)+' L'+ap[ap.length-1][0].toFixed(2)+',300 L0,300Z')}else{$('#pA').setAttribute('d','');$('#pAFill').setAttribute('d','')}
  var nl=$('#nowLine');if(D.now!=null){nl.style.opacity=1;nl.style.left=(D.now/(n-1)*100)+'%'}else nl.style.opacity=0;
  var mi=0;D.f.forEach(function(v,i){if(v>D.f[mi])mi=i});
  var pk=$('#peak');pk.style.left=(mi/(n-1)*100)+'%';pk.style.top=(Y(D.f[mi])/3)+'%';
  $('#peakLbl').textContent=D.peakL+' '+D.lab[mi]+', '+f1(D.f[mi])+' '+D.unit;
  $('#chartSub').textContent=D.sub;
  $('#yAxis').innerHTML=[0,.25,.5,.75,1].map(function(t){var v=D.ymax*t;return '<span style="top:'+((1-t)*100)+'%">'+(D.unit==='kW'?f1(v):Math.round(v))+'</span>'}).join('');
  $('#xAxis').innerHTML=D.ticks.map(function(i){return '<span style="left:'+(i/(n-1)*100)+'%">'+D.lab[i]+'</span>'}).join('');
  var k=D.k;
  $('#kSolarL').textContent=k.solarL;$('#kSolar').innerHTML=k.solar+'<small>kWh</small>';delta($('#kSolarD'),k.solarD);
  $('#kBatt').innerHTML=k.batt+'<small>%</small>';$('#kBattBar').style.width=k.batt+'%';delta($('#kBattD'),k.battD);
  $('#kGrid').innerHTML=k.grid+'<small>kWh</small>';delta($('#kGridD'),k.gridD);
  $('#kSaveL').textContent=k.saveL;$('#kSave').innerHTML=k.save;delta($('#kSaveD'),k.saveD);
  var nm=['Solar','Battery','Grid'];
  $$('#mixBar div').forEach(function(d,i){d.style.flexGrow=D.mix[i]});
  $$('#mixList b').forEach(function(b,i){b.textContent=D.mix[i]+'%'});
  $('#mixBar').setAttribute('aria-label','Where your power came from: '+nm.map(function(x,i){return x+' '+D.mix[i]+'%'}).join(', '));
  var u=D.unit,rows=D.f.map(function(v,i){return '<tr><th scope="row">'+D.lab[i]+'</th><td>'+f1(D.s[i])+'</td><td>'+f1(v)+'</td><td>'+(D.a[i]!=null?f1(D.a[i]):'Not yet available')+'</td></tr>'}).join('');
  $('#chartTable').innerHTML='<caption>Home usage versus solar, '+D.sub.toLowerCase()+'</caption><thead><tr><th scope="col">Time</th><th scope="col">Solar ('+u+')</th><th scope="col">Usage forecast ('+u+')</th><th scope="col">Actual usage ('+u+')</th></tr></thead><tbody>'+rows+'</tbody>';
  if(animate&&!RM){chartSvg.style.transition='none';chartSvg.style.clipPath='inset(-10% 100% -10% 0)';void chartSvg.getBoundingClientRect();chartSvg.style.transition='';chartSvg.style.clipPath='inset(-10% 0% -10% 0)';
    $$('.kpi .v').forEach(function(v){v.animate&&v.animate([{opacity:.2,transform:'translateY(6px)'},{opacity:1,transform:'none'}],{duration:500,easing:'cubic-bezier(.22,1,.36,1)'})})}
}
renderChart('today',false);
if(!RM)chartSvg.style.clipPath='inset(-10% 100% -10% 0)';
var dashTilt=$('#dashTilt');
dashTilt._onIn=function(){setTimeout(function(){chartSvg.style.clipPath='inset(-10% 0% -10% 0)'},500)};
io.observe(dashTilt);
$$('#rangeSeg button').forEach(function(b){b.addEventListener('click',function(){
  if(b.dataset.range===curRange)return;curRange=b.dataset.range;
  $$('#rangeSeg button').forEach(function(x){x.setAttribute('aria-pressed',x===b)});renderChart(curRange,true);
})});
var chart=$('#chart'),hit=$('#hit'),tip=$('#tip'),hIdx=-1;
function showIdx(i){
  var D=CD,n=D.f.length;i=clamp(i,0,n-1);hIdx=i;var u=D.unit;
  var Y=function(v){return (300-v/D.ymax*300)/3+'%'},l=i/(n-1)*100+'%';
  chart.classList.add('hovering');$('#hv').style.left=l;
  [['#hvS',D.s[i]],['#hvF',D.f[i]],['#hvA',D.a[i]]].forEach(function(p){var e=$(p[0]);if(p[1]==null){e.style.display='none'}else{e.style.display='';e.style.left=l;e.style.top=Y(p[1])}});
  var row=function(c,t,v){return '<div><span><i style="background:'+c+'"></i>'+t+'</span><span>'+v+'</span></div>'};
  tip.innerHTML='<b>'+D.lab[i]+'</b>'+row('#f4b23f','Solar',f1(D.s[i])+' '+u)+row('#7fbf8d','Usage forecast',f1(D.f[i])+' '+u)+(D.a[i]!=null?row('#1e8538','Actual usage',f1(D.a[i])+' '+u):'');
  var pw=hit.clientWidth,x=i/(n-1)*pw,tw=tip.offsetWidth||180;
  tip.style.left=clamp(x+14>pw-tw?x-tw-14:x+14,0,Math.max(0,pw-tw))+'px';
  tip.style.top=Math.max(0,(300-Math.max(D.f[i],D.s[i],D.a[i]||0)/D.ymax*300)/300*hit.clientHeight-40)+'px';
  $('#chartLive').textContent=D.lab[i]+': solar '+f1(D.s[i])+', usage forecast '+f1(D.f[i])+(D.a[i]!=null?', actual '+f1(D.a[i]):'')+' '+u;
}
function hideTip(){chart.classList.remove('hovering')}
hit.addEventListener('pointermove',function(e){var r=hit.getBoundingClientRect();showIdx(Math.round((e.clientX-r.left)/r.width*(CD.f.length-1)))});
hit.addEventListener('pointerleave',hideTip);
hit.addEventListener('keydown',function(e){if(e.key==='ArrowRight'||e.key==='ArrowLeft'){e.preventDefault();showIdx((hIdx<0?0:hIdx)+(e.key==='ArrowRight'?1:-1))}else if(e.key==='Escape')hideTip()});
hit.addEventListener('blur',hideTip);
function updSched(){$('#schedCount').textContent=$$('.action.done').length+' of 3 scheduled'}
$$('.sched').forEach(function(b){b.addEventListener('click',function(){
  var li=b.closest('.action'),on=!li.classList.contains('done');li.classList.toggle('done',on);
  b.innerHTML=on?'<svg class="ic"><use href="#i-check"/></svg>Scheduled':'Schedule';
  b.setAttribute('aria-label',(on?'Unschedule: ':'Schedule: ')+li.querySelector('.at p').textContent);updSched();
})});

/* ============ Store / Save visuals ============ */
(function(){
  var h='';for(var i=0;i<24;i++){var c=(i>=9&&i<=12)?'c':(i>=17&&i<=21)?'d':'';h+='<span class="'+c+(i===11?' cur':'')+'" style="transition-delay:'+(i*25)+'ms"></span>'}
  $('#cells').innerHTML=h;
  var pr=[14,14,14,14,14,14,18,24,24,22,20,18,18,18,20,26,44,48,48,46,44,30,18,14],win=[16,17,18,19,20];
  $('#barsIn').innerHTML=pr.map(function(p,i){return '<div><span class="bar'+(win.indexOf(i)>-1?' win':'')+(i===17?' max':'')+'" style="height:'+(p/48*100)+'%;transition-delay:'+(i*30)+'ms"><span>'+p+'¢ · '+(i<10?'0':'')+i+':00</span></span></div>'}).join('');
  var ring=$('#ringArc'),viz=ring.closest('.viz');viz._onIn=function(){ring.style.strokeDashoffset=(326.73*(1-.86)).toFixed(2)};io.observe(viz);
})();
$$('.spot').forEach(function(s){s.addEventListener('pointermove',function(e){var r=s.getBoundingClientRect();s.style.setProperty('--sx',(e.clientX-r.left)+'px');s.style.setProperty('--sy',(e.clientY-r.top)+'px')})});

/* ============ Count up ============ */
$$('.num[data-count]').forEach(function(el){
  var host=el.closest('.reveal')||el,prev=host._onIn;
  host._onIn=function(){if(prev)prev();if(RM)return;
    var to=+el.dataset.count,dec=+(el.dataset.dec||0),pre=el.dataset.prefix||'',suf=el.dataset.suffix||'',cm=el.dataset.comma,t0=null;
    function step(t){if(!t0)t0=t;var k=clamp((t-t0)/1600,0,1),e=1-Math.pow(1-k,4),v=(to*e).toFixed(dec);if(cm)v=Number(v).toLocaleString('en-US');el.textContent=pre+v+suf;if(k<1)requestAnimationFrame(step)}
    requestAnimationFrame(step);
  };
});
$('#wordmark').innerHTML='Lumora'.split('').map(function(c,i){return '<span style="--i:'+i+'">'+c+'</span>'}).join('');

/* ============ Forms ============ */
var emailRe=/^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/;
$$('select.inp').forEach(function(s){s.addEventListener('change',function(){s.classList.toggle('empty',!s.value)})});
function setErr(inp,msg){inp.setAttribute('aria-invalid',msg?'true':'false');var e=document.getElementById(inp.getAttribute('aria-describedby'));if(e)e.textContent=msg||''}
$('#demoForm').addEventListener('submit',function(e){
  e.preventDefault();
  var n=$('#fName'),m=$('#fEmail'),z=$('#fZip'),first=null;
  [[n,n.value.trim()?'':'Please enter your name.'],[m,!m.value.trim()?'Please enter your email.':emailRe.test(m.value.trim())?'':"That email doesn't look quite right."],[z,/^\d{5}(-\d{4})?$/.test(z.value.trim())?'':'Please enter a 5-digit ZIP code.']].forEach(function(p){setErr(p[0],p[1]);if(p[1]&&!first)first=p[0]});
  if(first){first.focus();return}
  var name=n.value.trim().split(' ')[0].replace(/[<>&"]/g,'');
  $('#formCard').innerHTML='<div class="success" role="status"><span class="big"><svg class="ic"><use href="#i-check"/></svg></span><h3>Thanks, '+name+'.</h3><p>Your savings estimate is on its way. Most arrive the same day.</p></div>';
});
$$('#demoForm .inp[required]').forEach(function(i){i.addEventListener('input',function(){if(i.getAttribute('aria-invalid')==='true')setErr(i,'')})});
$('#eaForm').addEventListener('submit',function(e){
  e.preventDefault();var i=$('#eaEmail'),msg=$('#eaMsg');
  if(!emailRe.test(i.value.trim())){i.setAttribute('aria-invalid','true');msg.style.color='#c2410c';msg.textContent='Enter a valid email to start your free trial.';i.focus();return}
  i.setAttribute('aria-invalid','false');msg.style.color='';msg.textContent="You're in. Check your inbox to pair your system.";e.target.querySelector('button').textContent='Added ✓';i.value='';
});

/* ============ 3D array ============ */
var model=$('#model'),rig=$('#rig'),hint=$('#dragHint');
(function(){
  var s='';[-280,0,280].forEach(function(x){
    s+='<div class="leg" style="height:63px;left:'+(x-5)+'px;top:-63px;transform:translateZ(110px)"><div class="x"></div></div>';
    s+='<div class="leg" style="height:170px;left:'+(x-5)+'px;top:-170px;transform:translateZ(-110px)"><div class="x"></div></div>';
  });
  s+='<div class="rail" style="top:-70px;transform:translateZ(110px)"></div><div class="rail" style="top:-176px;transform:translateZ(-110px)"></div>';
  $('#legs').innerHTML=s;
})();
var VIEWS={front:{rx:-14,ry:-24,c:'Six panels angled at 24 degrees to catch the midday sun, paired with a 13.5 kWh home battery.'},side:{rx:-8,ry:-90,c:'A low-profile frame keeps the system tidy on any roof or ground mount.'},back:{rx:-14,ry:-154,c:'Rear rails route every string to the inverter and battery beside the array.'},top:{rx:-72,ry:-12,c:"Rows spaced so no panel shades its neighbour, even in winter's low sun."}};
var rot={rx:-14,ry:-24},scl=1;
function applyRig(){rig.style.transform='translateX('+(-45*scl)+'px) scale('+scl+') rotateX('+rot.rx+'deg) rotateY('+rot.ry+'deg)'}
function fitRig(){scl=clamp(model.clientWidth/1080,.36,.95);applyRig()}
function setView(k){var v=VIEWS[k];rot.rx=v.rx;var t=v.ry;while(t-rot.ry>180)t-=360;while(t-rot.ry<-180)t+=360;rot.ry=t;applyRig();
  $$('#vbtns button').forEach(function(b){b.setAttribute('aria-pressed',b.dataset.view===k)});
  var c=$('#vcap');c.style.opacity=0;setTimeout(function(){c.textContent=v.c;c.style.opacity=1},200)}
$$('#vbtns button').forEach(function(b){b.addEventListener('click',function(){setView(b.dataset.view)})});
var drag=null;
model.addEventListener('pointerdown',function(e){drag={x:e.clientX,y:e.clientY,rx:rot.rx,ry:rot.ry};model.classList.add('dragging');model.setPointerCapture(e.pointerId);hint.style.opacity=0});
model.addEventListener('pointermove',function(e){if(!drag)return;rot.ry=drag.ry+(e.clientX-drag.x)*.45;rot.rx=clamp(drag.rx-(e.clientY-drag.y)*.3,-82,-2);applyRig()});
function endDrag(){if(!drag)return;drag=null;model.classList.remove('dragging');$$('#vbtns button').forEach(function(b){b.setAttribute('aria-pressed','false')})}
model.addEventListener('pointerup',endDrag);model.addEventListener('pointercancel',endDrag);
model.addEventListener('keydown',function(e){var k=e.key;if(k==='ArrowLeft')rot.ry-=15;else if(k==='ArrowRight')rot.ry+=15;else if(k==='ArrowUp')rot.rx=clamp(rot.rx-8,-82,-2);else if(k==='ArrowDown')rot.rx=clamp(rot.rx+8,-82,-2);else return;e.preventDefault();hint.style.opacity=0;applyRig()});
fitRig();

/* ============ Hero framing ============ */
var heroSticky=$('#heroSticky'),heroStage=$('#heroStage');
function layoutHero(){
  var W=heroSticky.clientWidth,H=heroSticky.clientHeight,svg=$('#sceneSvg'),s,vx=0,vy,vw=1780,vh;
  if(W>=900){
    s=W/1780;
    if(H/s<700){s=H/700;vw=W/s;vx=1780-vw}
    vh=H/s;var ty=H-884*s;ty=ty>0?ty*.28:ty;vy=-ty/s;
    heroStage.style.transform='translate('+(-vx*s).toFixed(1)+'px,'+ty.toFixed(1)+'px) scale('+s.toFixed(5)+')';
  }else{
    vw=920;vx=860;s=W/vw;vh=H/s;vy=884+(H*.1)/s-vh;heroStage.style.transform='';
  }
  var vb=vx.toFixed(1)+' '+vy.toFixed(1)+' '+vw.toFixed(1)+' '+vh.toFixed(1);
  svg.setAttribute('viewBox',vb);
  $('#villaLayer').style.transform='translate('+(-vx*s).toFixed(1)+'px,'+(-vy*s).toFixed(1)+'px) scale('+s.toFixed(5)+')';
}
layoutHero();

/* ============ Scroll engine ============ */
var heroScene=$('#heroScene'),sceneSvg=$('#sceneLayers'),heroContent=$('#heroUI'),heroTag=$('#heroTag'),heroShade=$('#heroShade');
var man=$('#manifesto'),mFill=$('#mFill'),mPct=$('#mPct'),mGlow=$('#mGlow');
var sol=$('#solutions'),track=$('#solTrack'),stagesLi=$$('.stages li'),stageFill=$('#stageFill'),stageDot=$('#stageDot');
var tl=$('#timeline'),tlFill=$('#tlFill'),tlDot=$('#tlDot');
var aboutArt=$('#aboutArt'),aboutPar=$('#aboutPar'),modelScale=$('#modelScale'),prog=$('#progress');
var artWrap=$('.about-art-wrap');artWrap._onIn=function(){aboutArt.classList.add('in')};io.observe(artWrap);
var lg=window.matchMedia('(min-width:1024px)'),dist=0;
function measureSol(){if(lg.matches){track.style.transform='';dist=Math.max(0,track.scrollWidth-window.innerWidth);sol.style.setProperty('--dist',dist+'px')}else{dist=0;track.style.transform='';sol.style.removeProperty('--dist')}}
function secP(el){var r=el.getBoundingClientRect(),h=r.height-window.innerHeight;return h>0?clamp(-r.top/h,0,1):(r.top<0?1:0)}
var ticking=false;
function onScroll(){if(!ticking){ticking=true;requestAnimationFrame(update)}}
function update(){
  ticking=false;var y=window.scrollY,vh=window.innerHeight,max=doc.scrollHeight-vh;
  prog.style.transform='scaleX('+(max>0?y/max:0)+')';
  header.classList.toggle('scrolled',y>40||!menu.hidden);
  header.classList.toggle('hide',y>lastY&&y>vh*.9&&menu.hidden);lastY=y;
  var hp=secP(hero);
  document.body.classList.toggle('hero-night',hero.classList.contains('is-night')&&hp<.4);
  if(!RM){
    var ins=hp*5.5;heroScene.style.clipPath='inset('+ins+'% '+(hp*4)+'% '+ins+'% '+(hp*4)+'% round '+(hp*36)+'px)';
    sceneSvg.style.transform='scale('+(1+hp*.1)+')';
    heroContent.style.opacity=clamp(1-hp*2.8,0,1);heroContent.style.transform='translateY('+(-hp*70)+'px)';
    heroShade.style.opacity=clamp((hp-.2)*2.2,0,1);
    var tp=clamp((hp-.38)/.36,0,1);heroTag.style.opacity=tp;heroTag.style.filter='blur('+((1-tp)*10)+'px)';heroTag.style.transform='translateY(-50%) scale('+lerp(.92,1,tp)+')';
  }
  var mp=clamp(secP(man)/.85,0,1),lit=Math.round(mp*mTokens.length);
  for(var i=0;i<mTokens.length;i++)mTokens[i].classList.toggle('on',i<lit||RM);
  mFill.style.transform='scaleX('+mp+')';mPct.textContent=Math.round(mp*100)+'%';mGlow.style.opacity=mp;
  if(!RM){var dr=dashTilt.getBoundingClientRect(),dp=clamp((vh-dr.top)/(vh*.7),0,1),e=1-Math.pow(1-dp,3);
    dashTilt.style.transform='translateY('+(80*(1-e))+'px) scale('+lerp(.86,1,e)+') rotateX('+(26*(1-e))+'deg)';dashTilt.style.opacity=lerp(.35,1,e)}
  if(lg.matches){var sp=secP(sol);track.style.transform='translate3d('+(-sp*dist)+'px,0,0)';
    stageFill.style.transform='scaleX('+sp+')';stageDot.style.left=(sp*100)+'%';
    var si=sp<.34?0:sp<.67?1:2;stagesLi.forEach(function(l,k){l.classList.toggle('on',k<=si)})}
  var tr=tl.getBoundingClientRect(),tpp=clamp((vh*.6-tr.top)/tr.height,0,1);
  tlFill.style.transform='scaleY('+tpp+')';tlDot.style.top=(tpp*100)+'%';
  if(!RM){var ar=aboutArt.getBoundingClientRect(),ap=clamp((vh-ar.top)/(vh+ar.height),0,1);aboutPar.style.transform='translateY('+lerp(-40,40,ap)+'px)';
    var mr=modelScale.getBoundingClientRect(),m2=clamp((vh-mr.top)/(vh*.75),0,1),me=1-Math.pow(1-m2,3);modelScale.style.transform='translateY('+(70*(1-me))+'px) scale('+lerp(.86,1,me)+')'}
}
window.addEventListener('scroll',onScroll,{passive:true});
window.addEventListener('resize',function(){layoutHero();measureSol();fitRig();onScroll()});
if(lg.addEventListener)lg.addEventListener('change',function(){measureSol();onScroll()});
measureSol();update();
if(document.fonts&&document.fonts.ready)document.fonts.ready.then(function(){measureSol();update()});
window.addEventListener('load',function(){measureSol();update()});
})();
</script>
</body>
</html>
```

