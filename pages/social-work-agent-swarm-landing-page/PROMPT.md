INSTALANDING.AI · Social Work Agent Swarm Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Social Work Agent Swarm Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/social-work-agent-swarm-landing-page

kindswarm-casework.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Social Work Agent Swarm Landing Page
  slug     social-work-agent-swarm-landing-page
  prompt   https://instalanding.ai/p/social-work-agent-swarm-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/social-work-agent-swarm-landing-page
  license  MIT. Fictional product ("Kind Swarm"), agents, prices, counties, certifications and numbers. Not a real service
           and not advice on how to run casework. Replace copy, numbers, pricing and the [bracketed] placeholders
           before shipping.

  MAP
  styles    one <style>: type (.disp Stardos Stencil, .serif italic IBM Plex Sans Condensed, .label IBM Plex Mono),
            buttons (.btn-ink / .btn-paper / .btn-lime with hard offset shadows), the .rings background (concentric
            arcs from two colours: --c1 / --c2 / --s, used by .hero-rings, .mq-rings, .ink-rings and the card stages
            .st1 to .st8), the animoji characters (.moji: .bod bobs, .eye blinks, .pupil follows the pointer, .react
            on a poke), cards, steps, the approval queue, guardrail rules and plans. Fonts from Google Fonts.
  sections  hero (with nav), marquee, how, zero, crew, queue, guardrails, pricing, book, footer
  defs      one hidden <svg> at the top holds the shared gradients (ks-blue, ks-violet, ks-sun, ks-peach, ks-peri,
            ks-lilac), gloss and shade, and the grain noise filter every character and .grain layer uses
  scripts   one inline script: pointer -> --px / --py on <html> (pupils), poke a character to replay .react,
            and the crew filter (data-filter pills hide cards whose data-tags don't match, and update the count)
  assets    none: every character is inline SVG; no images, no canvas, no Rive

  ADAPTING
  - An agent is one <article class="card" data-tags="..."> with a .stage (pick .st1 to .st8 for its colour),
    a tag and code, a character inside <button class="poke" data-poke>, name, price, description and skills.
  - Filter jobs are the data-filter pills; a card shows when its data-tags contain the picked job.
  - Stagger idle motion by giving characters .d1 to .d4.
  - Reduced motion stops every animation and transition, including the marquee and the bob.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Kind Swarm</title>
<meta name="description" content="Kind Swarm, a fictional swarm of small AI agents for social work. They draft, chase and remind; a person approves every step.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Stardos+Stencil:wght@400;700&family=IBM+Plex+Sans+Condensed:ital,wght@0,400;0,500;0,600;0,700;1,400;1,500&family=IBM+Plex+Mono:wght@500;600&display=swap" rel="stylesheet">
<style>
body{margin:0;background:#15111F}
html{scroll-behavior:smooth}
a{color:inherit}a:hover{color:inherit}
.ks{font-family:"IBM Plex Sans Condensed","Arial Narrow",Arial,sans-serif;color:#15111F;-webkit-font-smoothing:antialiased;overflow-x:hidden}
.ks *{box-sizing:border-box}
.disp{font-family:"Stardos Stencil","Courier New",serif;font-weight:700;text-transform:uppercase;line-height:.92;letter-spacing:.01em;margin:0}
.serif{font-family:"IBM Plex Sans Condensed","Arial Narrow",sans-serif;font-style:italic;font-weight:400;text-transform:none;letter-spacing:-.02em}
.label{margin:0;font-family:"IBM Plex Mono",ui-monospace,Menlo,monospace;font-size:13px;font-weight:500;letter-spacing:.16em;text-transform:uppercase}
.wrap{width:100%;max-width:1440px;margin:0 auto;padding-left:clamp(16px,4vw,56px);padding-right:clamp(16px,4vw,56px)}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;min-height:56px;padding:0 28px;border:3px solid #15111F;border-radius:999px;font:600 17px/1 "IBM Plex Sans Condensed","Arial Narrow",sans-serif;text-decoration:none;cursor:pointer;box-shadow:8px 8px 0 #15111F;transition:transform .14s cubic-bezier(.2,.8,.2,1),box-shadow .14s cubic-bezier(.2,.8,.2,1)}
.btn:hover{transform:translate(-2px,-2px);box-shadow:10px 10px 0 #15111F}
.btn:active{transform:translate(8px,8px);box-shadow:0 0 0 #15111F}
.btn-ink{background:#15111F;color:#F4EFE6}.btn-ink:hover{color:#D4FF3A}
.btn-paper{background:#F4EFE6;color:#15111F}
.btn-lime{background:#D4FF3A;color:#15111F}
.on-ink .btn{border-color:#D4FF3A;box-shadow:8px 8px 0 #D4FF3A}
.on-ink .btn:hover{box-shadow:10px 10px 0 #D4FF3A}
a:focus-visible,button:focus-visible{outline:3px solid #3D7BFF;outline-offset:4px}
.navlink{text-decoration:none;font-weight:600;font-size:16px;padding:12px 4px}
.navlink:hover{text-decoration:underline;text-decoration-thickness:3px;text-underline-offset:6px}
.rings{--_g:var(--c2) 4% 14%,var(--c1) 14% 24%,var(--c2) 22% 34%,var(--c1) 34% 44%,var(--c2) 44% 56%,var(--c1) 56% 66%,var(--c2) 66% 76%,var(--c1) 76% 86%,var(--c2) 86% 96%;background-image:radial-gradient(100% 100% at 100% 0,var(--c1) 4%,var(--_g),var(--sh) 96%,#0000),radial-gradient(100% 100% at 0 100%,#0000,var(--sh) 4%,var(--_g),var(--c1) 96%);background-size:var(--s) var(--s)}
.hero-rings{--s:120px;--c1:#FF5A3C;--c2:#F0361A;--sh:#0005}
.st1{--c1:#9CC8FF;--c2:#84B6F7;background-color:#9CC8FF}
.st2{--c1:#FFE08A;--c2:#FFD15C;background-color:#FFE08A}
.st3{--c1:#FFC4A8;--c2:#FFAE8A;background-color:#FFC4A8}
.st4{--c1:#D6C2FF;--c2:#C3A8FF;background-color:#D6C2FF}
.st5{--c1:#FFB8D9;--c2:#FF9CC8;background-color:#FFB8D9}
.st6{--c1:#C9F26B;--c2:#B6E34A;background-color:#C9F26B}
.st7{--c1:#A8E6FF;--c2:#86D8F7;background-color:#A8E6FF}
.st8{--c1:#F2C4FF;--c2:#E6A8FA;background-color:#F2C4FF}
.grain{position:absolute;inset:0;width:100%;height:100%;pointer-events:none;opacity:.22;mix-blend-mode:multiply}
.moji{display:block;width:100%;height:100%;overflow:visible}
.moji .bod{transform-box:fill-box;transform-origin:50% 90%;animation:bob 3.4s cubic-bezier(.45,0,.55,1) infinite}
.moji .eye{transform-box:fill-box;transform-origin:center;animation:blink 5.6s infinite}
.moji .pupil{transform:translate(var(--px,0px),var(--py,0px));transition:transform .18s cubic-bezier(.2,.8,.2,1)}
.moji.d1 .bod{animation-delay:-.7s}.moji.d1 .eye{animation-delay:-1.9s}
.moji.d2 .bod{animation-delay:-1.5s}.moji.d2 .eye{animation-delay:-3.4s}
.moji.d3 .bod{animation-delay:-2.3s}.moji.d3 .eye{animation-delay:-.6s}
.moji.d4 .bod{animation-delay:-2.9s}.moji.d4 .eye{animation-delay:-4.6s}
.moji.react .bod{animation:poke .76s cubic-bezier(.3,1.4,.5,1)}
.poke{display:block;padding:0;border:0;background:none;cursor:pointer;border-radius:50%}
.poke svg{filter:drop-shadow(8px 8px 0 #15111F)}
.rise{animation:rise 1s cubic-bezier(.16,1,.3,1) both}
.mq-rings{--s:90px;--c1:#D4FF3A;--c2:#C6F230;--sh:#0002}
.wave-text{display:inline-block;--s:120px;--c1:#15111F;--c2:#5A160C;--sh:#0000;color:transparent;-webkit-background-clip:text;background-clip:text;animation:drift 16s linear infinite}
@keyframes drift{to{background-position:120px 120px}}
.ink-rings{--s:120px;--c1:#15111F;--c2:#221C3A;--sh:#0007}
.mqbox{padding:26px 0;-webkit-mask-image:linear-gradient(90deg,transparent,#000 7%,#000 93%,transparent);mask-image:linear-gradient(90deg,transparent,#000 7%,#000 93%,transparent)}
.mqbox:hover .mq{animation-play-state:paused}
.mq{display:flex;align-items:center;width:max-content;animation:mq 56s linear infinite}
.mq span:nth-of-type(even){color:transparent;-webkit-text-stroke:1.5px #15111F}
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(min(100%,280px),1fr));margin:0 auto}
.stat{display:flex;flex-direction:column-reverse;justify-content:flex-end;gap:12px;padding:32px 28px;border-left:1px solid rgba(244,239,230,.16)}
.stat:first-child{border-left:0;padding-left:0}
.stat dd{margin:0;font-family:"Stardos Stencil",serif;font-weight:700;font-size:clamp(44px,4.4vw,64px);line-height:.9;letter-spacing:.01em}
.stat dt{display:flex;align-items:center;gap:10px;font:500 13px/1.35 "IBM Plex Mono",ui-monospace,monospace;letter-spacing:.14em;text-transform:uppercase;color:#CFC6E8}
.live{flex:0 0 auto;width:9px;height:9px;border-radius:50%;background:#D4FF3A;animation:live 2s ease-out infinite}
@keyframes live{0%{box-shadow:0 0 0 0 rgba(212,255,58,.6)}70%{box-shadow:0 0 0 10px rgba(212,255,58,0)}100%{box-shadow:0 0 0 0 rgba(212,255,58,0)}}
.mq span{padding:0 28px;font-family:"Stardos Stencil",serif;font-weight:700;font-size:clamp(32px,4.4vw,64px);line-height:1.25;text-transform:uppercase;white-space:nowrap}
.mq svg{flex:0 0 auto}
.pill{min-height:44px;padding:0 20px;border:2px solid #F4EFE6;border-radius:999px;background:transparent;color:#F4EFE6;font:600 15px/1 "IBM Plex Sans Condensed","Arial Narrow",sans-serif;cursor:pointer;transition:background .15s,color .15s}
.pill:hover{background:rgba(244,239,230,.12)}
.pill.on{background:#D4FF3A;border-color:#D4FF3A;color:#15111F}
.card{display:flex;flex-direction:column;padding:10px;background:#F4EFE6;border-radius:30px;box-shadow:8px 8px 0 #D4FF3A;transition:transform .25s cubic-bezier(.2,.8,.2,1),box-shadow .25s cubic-bezier(.2,.8,.2,1)}
.card:hover{transform:translate(-3px,-3px);box-shadow:11px 11px 0 #D4FF3A}
.stage{--s:76px;--sh:#0002;position:relative;height:270px;display:grid;place-items:center;border:2.5px solid #15111F;border-radius:22px;overflow:hidden;box-shadow:inset 0 0 0 1px rgba(255,255,255,.45),inset 0 -60px 80px -40px rgba(21,17,31,.28)}
.stage::after{content:"";position:absolute;left:50%;bottom:34px;width:120px;height:16px;margin-left:-60px;border-radius:50%;background:rgba(21,17,31,.22);filter:blur(4px);transition:transform .3s cubic-bezier(.3,1.5,.5,1)}
.stage .poke{position:relative;z-index:1;width:164px;height:164px;transition:transform .35s cubic-bezier(.3,1.5,.5,1)}
.card:hover .stage .poke{transform:translateY(-8px) rotate(-4deg) scale(1.05)}
.card:hover .stage::after{transform:scale(.8)}
.tag{position:absolute;z-index:2;top:14px;left:14px;padding:9px 14px;border:2px solid #15111F;border-radius:999px;background:#FFFFFF;color:#15111F;font:600 13px/1 "IBM Plex Mono",ui-monospace,monospace;letter-spacing:.06em;text-transform:uppercase;box-shadow:0 2px 0 #15111F}
.code{position:absolute;z-index:2;top:14px;right:14px;padding:9px 12px;border:2px solid #15111F;border-radius:999px;background:#15111F;color:#FFFFFF;font:600 13px/1 "IBM Plex Mono",ui-monospace,monospace;letter-spacing:.08em}
.cbody{flex:1;display:flex;flex-direction:column;gap:12px;padding:22px 14px 14px}
.chead{display:flex;justify-content:space-between;align-items:center;gap:12px}
.chead{align-items:flex-start}
.cname{font-family:"IBM Plex Sans Condensed","Arial Narrow",sans-serif;font-weight:700;font-size:30px;line-height:1.05;letter-spacing:-.01em;text-transform:none;color:#15111F}
.cprice{flex:0 0 auto;padding:9px 14px;border-radius:999px;background:#15111F;color:#FFFFFF;font:600 16px/1 "IBM Plex Mono",ui-monospace,monospace;white-space:nowrap}
.cprice small{font-size:13px;font-weight:500;color:#E4DEF2}
.cdesc{margin:0;font-size:17px;line-height:1.55;color:#2A2436}
.cskills{margin:auto 0 0;padding-top:14px;border-top:1.5px solid rgba(21,17,31,.25);font:500 13px/1.5 "IBM Plex Mono",ui-monospace,monospace;letter-spacing:.04em;text-transform:uppercase;color:#3A3347}
.step{display:flex;flex-direction:column;gap:16px;padding-top:24px;border-top:3px solid #15111F}
.num{font-family:"Stardos Stencil",serif;font-weight:700;font-size:96px;line-height:.8;color:transparent;-webkit-text-stroke:2.5px #15111F}
.qrow{display:grid;grid-template-columns:56px minmax(0,1fr) auto;gap:16px;align-items:center;padding:18px 22px;border-top:2px solid rgba(21,17,31,.12)}
.qbtn{min-height:44px;padding:0 16px;border:2px solid #15111F;border-radius:999px;background:#fff;font:600 14px/1 "IBM Plex Sans Condensed","Arial Narrow",sans-serif;cursor:pointer}
.qbtn.go{background:#15111F;color:#D4FF3A}
.chip{display:inline-flex;align-items:center;min-height:44px;padding:0 20px;border:2px solid #15111F;border-radius:999px;font-weight:700;font-size:15px;letter-spacing:.04em}
.rule{display:flex;flex-direction:column;gap:14px;padding:32px;border:2px solid #3B3358;border-radius:24px;background:#1F1A2E}
.plan{display:flex;flex-direction:column;gap:18px;padding:36px 32px;border:3px solid #15111F;border-radius:28px;background:#fff;box-shadow:8px 8px 0 #15111F}
.plan ul{margin:0;padding:0;list-style:none;display:flex;flex-direction:column;gap:10px;font-size:16px}
.plan li{padding-left:22px;position:relative}
.plan li::before{content:"";position:absolute;left:0;top:7px;width:10px;height:10px;transform:rotate(45deg);border-radius:2px;background:currentColor}
@keyframes bob{0%,100%{transform:translateY(0) scale(1,1)}50%{transform:translateY(-5px) scale(1.02,.98)}}
@keyframes blink{0%,93%,100%{transform:scaleY(1)}95%{transform:scaleY(.08)}}
@keyframes poke{0%{transform:scale(1,1)}18%{transform:translateY(5px) scale(1.12,.86)}45%{transform:translateY(-16px) scale(.92,1.12)}70%{transform:translateY(2px) scale(1.04,.97)}100%{transform:scale(1,1)}}
@keyframes rise{from{opacity:0;transform:translateY(70px)}to{opacity:1;transform:none}}
@keyframes mq{to{transform:translateX(-50%)}}
@media (prefers-reduced-motion: reduce){.ks *,.ks *::before{animation:none !important;transition:none !important}html{scroll-behavior:auto}}
[hidden]{display:none!important}
</style>
</head>
<body>
<div class="ks">

<svg width="0" height="0" style="position: absolute" aria-hidden="true" focusable="false">
<defs>
<linearGradient id="ks-blue" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#3D7BFF"></stop><stop offset="1" stop-color="#B56CFF"></stop></linearGradient>
<linearGradient id="ks-violet" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#3D7BFF"></stop><stop offset="1" stop-color="#C873FF"></stop></linearGradient>
<linearGradient id="ks-sun" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#FFD24A"></stop><stop offset="1" stop-color="#FF9A1C"></stop></linearGradient>
<linearGradient id="ks-peach" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#FFB36B"></stop><stop offset="1" stop-color="#FF6FB5"></stop></linearGradient>
<linearGradient id="ks-peri" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#7AA8FF"></stop><stop offset="1" stop-color="#B56CFF"></stop></linearGradient>
<linearGradient id="ks-lilac" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#E7A6FF"></stop><stop offset="1" stop-color="#B56CFF"></stop></linearGradient>
<radialGradient id="ks-gloss" cx=".32" cy=".24" r=".55"><stop offset="0" stop-color="#FFFFFF" stop-opacity=".6"></stop><stop offset="1" stop-color="#FFFFFF" stop-opacity="0"></stop></radialGradient>
<radialGradient id="ks-shade" cx=".62" cy=".9" r=".6"><stop offset="0" stop-color="#15111F" stop-opacity=".24"></stop><stop offset="1" stop-color="#15111F" stop-opacity="0"></stop></radialGradient>
<filter id="ks-noise"><feTurbulence type="fractalNoise" baseFrequency=".85" numOctaves="2" stitchTiles="stitch"></feTurbulence><feColorMatrix type="matrix" values="0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 .7 0"></feColorMatrix></filter>
</defs>
</svg>

<!-- HERO -->
<header id="top" data-section="hero" class="rings hero-rings" style="position: relative; overflow: hidden; background-color: #FF5A3C; color: #15111F">
<svg class="grain" aria-hidden="true"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<nav class="wrap" data-section="nav" aria-label="Primary" style="position: relative; display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 16px; padding-top: 24px; padding-bottom: 24px">
<a href="#top" aria-label="Kind Swarm home" style="display: flex; align-items: center; gap: 12px; text-decoration: none">
<span style="display: block; width: 44px; height: 44px">
<svg class="moji d2" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="10" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="9"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g></g></svg>
</span>
<span class="disp" style="font-size: 24px; line-height: 1">Kind Swarm</span>
</a>
<div style="display: flex; flex-wrap: wrap; align-items: center; gap: 8px 28px">
<a class="navlink" href="#how">How it works</a>
<a class="navlink" href="#crew">Agents</a>
<a class="navlink" href="#guardrails">Guardrails</a>
<a class="navlink" href="#pricing">Pricing</a>
<a class="btn btn-ink" href="#book" style="min-height: 48px; padding: 0 22px; font-size: 15px; box-shadow: none">Book a demo</a>
</div>
</nav>

<div class="wrap" style="position: relative; padding-top: clamp(24px, 4vw, 56px)">
<div class="rise" style="display: flex; flex-wrap: wrap; justify-content: space-between; gap: 12px; padding-bottom: 20px; border-bottom: 3px solid #15111F; animation-delay: .05s">
<p class="label">Agent swarms for social work</p>
<p class="label">Drafts, never decisions</p>
</div>
<h1 class="disp" aria-label="Kind Swarm" style="margin-top: clamp(16px, 2.5vw, 36px); font-size: clamp(60px, 17vw, 260px)">
<span style="display: flex; align-items: flex-end; gap: clamp(12px, 3vw, 48px)">
<span class="rise" style="display: block; animation-delay: .12s"><span class="rings wave-text">Kind</span></span>
<button class="poke rise" type="button" data-poke aria-label="Poke the swarm lead" style="width: clamp(80px, 17vw, 260px); height: clamp(80px, 17vw, 260px); margin-bottom: clamp(4px, 1vw, 16px); animation-delay: .32s">
<svg class="moji" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-violet)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M134 158l24-24" fill="none" stroke="#FFFFFF" stroke-width="3.5" stroke-linecap="round" opacity=".45"></path><g class="eye"><ellipse cx="74" cy="98" rx="20" ry="21.6" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="74" cy="99" r="11.2" fill="#15111F"></circle><circle cx="70" cy="94" r="3.4" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="126" cy="98" rx="20" ry="21.6" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="126" cy="99" r="11.2" fill="#15111F"></circle><circle cx="122" cy="94" r="3.4" fill="#FFFFFF"></circle></g></g><ellipse cx="62" cy="126" rx="9" ry="5" fill="#FF8FC4" opacity=".8"></ellipse><ellipse cx="138" cy="126" rx="9" ry="5" fill="#FF8FC4" opacity=".8"></ellipse><path d="M88 130q12 9 24 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path></g></svg>
</button>
</span>
<span class="rise" style="display: block; animation-delay: .22s"><span class="rings wave-text">Swarm</span></span>
</h1>

<div class="rise" style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 420px), 1fr)); gap: 40px 64px; align-items: end; padding-top: clamp(32px, 4vw, 56px); padding-bottom: clamp(48px, 6vw, 88px); animation-delay: .45s">
<p style="margin: 0">
<span class="serif" style="display: block; font-size: clamp(36px, 4.2vw, 64px); line-height: 1">They draft, fetch and remind.</span>
<span class="disp" style="display: block; margin-top: 8px; font-size: clamp(40px, 5vw, 76px)">People decide.</span>
</p>
<div style="display: flex; flex-direction: column; gap: 28px">
<p style="margin: 0; max-width: 520px; font-size: 20px; line-height: 1.5; font-weight: 500">Small AI agents that take the paperwork, the hold music and the forty-tab benefits search off a caseworker's desk.</p>
<div style="display: flex; flex-wrap: wrap; gap: 20px">
<a class="btn btn-ink" href="#crew" style="box-shadow: none">Meet the crew</a>
<a class="btn btn-paper" href="#guardrails">See the guardrails</a>
</div>
</div>
</div>
</div>

<div style="position: relative; background: #15111F; color: #F4EFE6">
<dl class="wrap stats">
<div class="stat"><dt>Agents on the desk</dt><dd>08</dd></div>
<div class="stat"><dt>Decisions without a person</dt><dd style="color: #D4FF3A">00</dd></div>
<div class="stat"><dt><span class="live" aria-hidden="true"></span>On call</dt><dd>24/7</dd></div>
</dl>
</div>
</header>

<!-- MARQUEE -->
<div data-section="marquee" class="rings mq-rings" aria-hidden="true" style="position: relative; overflow: hidden; background-color: #D4FF3A; color: #15111F; border-top: 3px solid #15111F; border-bottom: 3px solid #15111F">
<div class="mqbox">
<div class="mq">
<span>Intake drafted</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Benefits found</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Court date kept</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Housing matched</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Follow-up sent</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Human approved</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Intake drafted</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Benefits found</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Court date kept</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Housing matched</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Follow-up sent</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
<span>Human approved</span><svg width="26" height="26" viewBox="0 0 24 24"><path d="M12 0C12.8 7.2 16.8 11.2 24 12C16.8 12.8 12.8 16.8 12 24C11.2 16.8 7.2 12.8 0 12C7.2 11.2 11.2 7.2 12 0Z" fill="#15111F"></path></svg>
</div>
</div>
</div>

<!-- HOW -->
<section id="how" data-section="how" style="position: relative; overflow: hidden; background: #F4EFE6">
<svg class="grain" aria-hidden="true" style="opacity: .14"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<div class="wrap" style="position: relative; padding-top: clamp(80px, 10vw, 160px); padding-bottom: clamp(80px, 10vw, 160px)">
<p class="label">01 — How a swarm works</p>
<h2 class="disp" style="margin-top: 24px; font-size: clamp(48px, 8.4vw, 136px)">Many hands.<span class="serif" style="display: block; font-size: .72em; line-height: 1">one desk.</span></h2>
<p style="max-width: 600px; margin: 32px 0 0; font-size: 20px; line-height: 1.55; color: #3A3347">Each agent does one job and hands the rest on. The swarm splits a case into lanes, works them in parallel, then waits for you.</p>
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr)); gap: 56px 48px; margin-top: clamp(56px, 7vw, 104px)">
<article class="step">
<div style="display: flex; justify-content: space-between; align-items: flex-end">
<span class="num" aria-hidden="true">01</span>
<span style="display: block; width: 104px; height: 104px">
<svg class="moji d1" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M88 128q12 9 24 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path></g></svg>
</span>
</div>
<h3 class="disp" style="font-size: 34px">Say it plainly</h3>
<p style="margin: 0; font-size: 17px; line-height: 1.6; color: #3A3347">"New family, eviction notice, two kids, Spanish at home." That is the whole prompt. No forms to fill first.</p>
</article>
<article class="step">
<div style="display: flex; justify-content: space-between; align-items: flex-end">
<span class="num" aria-hidden="true">02</span>
<span style="display: block; width: 104px; height: 104px">
<svg class="moji d2" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-sun)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M86 126q14 13 28 0z" fill="#15111F"></path><path d="M150 150l26-40" stroke="#15111F" stroke-width="6" stroke-linecap="round"></path><path d="M178 92l5 11 12 2-9 8 2 12-10-6-10 6 2-12-9-8 12-2z" fill="#FFFFFF" stroke="#15111F" stroke-width="3" stroke-linejoin="round"></path></g></svg>
</span>
</div>
<h3 class="disp" style="font-size: 34px">Lanes, not a chatbot</h3>
<p style="margin: 0; font-size: 17px; line-height: 1.6; color: #3A3347">The scribe drafts the intake, the navigator checks benefits, the scout watches housing, the interpreter readies the letters.</p>
<p style="margin: 4px 0 0; padding: 16px 18px; border-radius: 14px; background: #15111F; color: #F4EFE6; font: 500 14px/1.8 ui-monospace, Menlo, monospace"><b style="color: #D4FF3A">scribe</b> → navigator · 1.8s<br><b style="color: #D4FF3A">navigator</b> → scout · 2.4s</p>
</article>
<article class="step">
<div style="display: flex; justify-content: space-between; align-items: flex-end">
<span class="num" aria-hidden="true">03</span>
<span style="display: block; width: 104px; height: 104px">
<svg class="moji d3" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M108 100q16-12 32 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path><path d="M86 124q16 12 30-2" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><g transform="translate(48 160) rotate(-8)"><rect x="-20" y="-6" width="40" height="34" rx="12" fill="#FFB21C" stroke="#15111F" stroke-width="3"></rect><rect x="-8" y="-34" width="15" height="34" rx="7.5" fill="#FFC94A" stroke="#15111F" stroke-width="3"></rect><path d="M-20 6h40M-20 16h40" stroke="#E08A0F" stroke-width="2.5" stroke-linecap="round"></path></g></g></svg>
</span>
</div>
<h3 class="disp" style="font-size: 34px">You sign it off</h3>
<p style="margin: 0; font-size: 17px; line-height: 1.6; color: #3A3347">Nothing reaches a client, a court or a landlord until a person reads it and presses send. The swarm waits well.</p>
</article>
</div>
</div>
</section>

<!-- THE ZERO -->
<section data-section="zero" aria-label="Zero decisions without a person" class="rings mq-rings" style="position: relative; overflow: hidden; background-color: #D4FF3A; border-top: 3px solid #15111F; border-bottom: 3px solid #15111F">
<svg class="grain" aria-hidden="true" style="opacity: .18"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<div class="wrap" style="position: relative; display: flex; flex-wrap: wrap; align-items: center; gap: 24px clamp(32px, 5vw, 80px); padding-top: clamp(56px, 7vw, 112px); padding-bottom: clamp(56px, 7vw, 112px)">
<p class="disp" aria-hidden="true" style="font-size: clamp(260px, 46vw, 680px); line-height: .78">0</p>
<div style="flex: 1 1 380px; display: flex; flex-direction: column; gap: 28px">
<span style="display: block; width: 120px; height: 120px">
<svg class="moji d4" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#4F86FF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M84 124q16 14 32 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><path d="M50 88h100l-4 6q-6 20-26 18q-14-2-16-16h-4q-2 14-16 16q-20 2-26-18z" fill="#15111F"></path><path d="M62 96l14-8M118 96l14-8" stroke="#FFFFFF" stroke-width="4" stroke-linecap="round" opacity=".8"></path><g transform="translate(156 152) rotate(70) scale(.9)"><rect x="-20" y="-6" width="40" height="34" rx="12" fill="#FFB21C" stroke="#15111F" stroke-width="3"></rect><rect x="-8" y="-34" width="15" height="34" rx="7.5" fill="#FFC94A" stroke="#15111F" stroke-width="3"></rect><path d="M-20 6h40M-20 16h40" stroke="#E08A0F" stroke-width="2.5" stroke-linecap="round"></path></g></g></svg>
</span>
<h2 class="disp" style="font-size: clamp(40px, 4.4vw, 72px)">Decisions made without a person.</h2>
<p class="serif" style="margin: 0; font-size: clamp(28px, 2.6vw, 40px); line-height: 1.15">Not one. The swarm drafts; a caseworker signs.</p>
</div>
</div>
</section>

<!-- THE CREW -->
<section id="crew" data-section="crew" class="on-ink" style="background: #15111F; color: #F4EFE6">
<div class="wrap" style="padding-top: clamp(80px, 10vw, 160px); padding-bottom: clamp(96px, 11vw, 176px)">
<p class="label" style="color: #D4FF3A">02 — The crew</p>
<div style="display: flex; flex-wrap: wrap; justify-content: space-between; align-items: flex-end; gap: 32px; margin-top: 24px">
<h2 class="disp" style="font-size: clamp(48px, 8.4vw, 136px)">Eight agents.<span class="serif" style="display: block; font-size: .72em; line-height: 1; color: #D4FF3A">one job each.</span></h2>
<p aria-live="polite" style="margin: 0; font-size: 15px; font-weight: 600; letter-spacing: .14em; text-transform: uppercase; color: #B9B0CC">Showing <span id="count">08</span> of 08</p>
</div>
<div role="group" aria-label="Filter agents by job" style="display: flex; flex-wrap: wrap; gap: 12px; margin-top: 48px">
<button type="button" class="pill on" aria-pressed="true" data-filter="all">All</button>
<button type="button" class="pill" aria-pressed="false" data-filter="intake">Intake</button>
<button type="button" class="pill" aria-pressed="false" data-filter="benefits">Benefits</button>
<button type="button" class="pill" aria-pressed="false" data-filter="housing">Housing</button>
<button type="button" class="pill" aria-pressed="false" data-filter="legal">Legal</button>
<button type="button" class="pill" aria-pressed="false" data-filter="crisis">Crisis</button>
<button type="button" class="pill" aria-pressed="false" data-filter="language">Language</button>
</div>
<div style="display: grid; grid-template-columns: repeat(auto-fill, minmax(min(100%, 320px), 1fr)); gap: 40px 36px; margin-top: 56px">

<article class="card" data-tags="intake">
<div class="stage rings st1">
<span class="tag">Most deployed</span><span class="code">AGT-01</span>
<button class="poke" type="button" data-poke aria-label="Poke the Intake Scribe">
<svg class="moji d1" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M134 158l24-24" fill="none" stroke="#FFFFFF" stroke-width="3.5" stroke-linecap="round" opacity=".45"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M88 128q12 9 24 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Intake Scribe</h3><span class="cprice">$14<small>/mo</small></span></div>
<p class="cdesc">Listens in, with consent, and drafts the intake note, the household map and the needs list while you keep eye contact. You edit it, you sign it.</p>
<p class="cskills">Speech-to-note · Needs list · Household map</p>
</div>
</article>

<article class="card" data-tags="benefits">
<div class="stage rings st2">
<span class="tag">Finds money</span><span class="code">AGT-02</span>
<button class="poke" type="button" data-poke aria-label="Poke the Benefits Navigator">
<svg class="moji d2" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-sun)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M134 158l24-24" fill="none" stroke="#FFFFFF" stroke-width="3.5" stroke-linecap="round" opacity=".45"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M86 126q14 13 28 0z" fill="#15111F"></path><path d="M150 150l26-40" stroke="#15111F" stroke-width="6" stroke-linecap="round"></path><path d="M178 92l5 11 12 2-9 8 2 12-10-6-10 6 2-12-9-8 12-2z" fill="#FFFFFF" stroke="#15111F" stroke-width="3" stroke-linejoin="round"></path><path d="M34 52l3 7 7 1-5 5 1 7-6-3-6 3 1-7-5-5 7-1z" fill="#FFFFFF" stroke="#15111F" stroke-width="2.5" stroke-linejoin="round"></path></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Benefits Navigator</h3><span class="cprice">$16<small>/mo</small></span></div>
<p class="cdesc">Checks a household against every program in your county, explains why each one fits, and drafts the applications with the right documents already attached.</p>
<p class="cskills">Eligibility · Pre-filled forms · Plain-language why</p>
</div>
</article>

<article class="card" data-tags="housing">
<div class="stage rings st3">
<span class="tag">Watches overnight</span><span class="code">AGT-03</span>
<button class="poke" type="button" data-poke aria-label="Poke the Housing Scout">
<svg class="moji d3" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peach)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M90 130h20" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><circle cx="124" cy="100" r="30" fill="#C8E6FF" fill-opacity=".35" stroke="#15111F" stroke-width="7"></circle><path d="M146 122l26 26" stroke="#15111F" stroke-width="12" stroke-linecap="round"></path><path d="M146 122l26 26" stroke="#3D7BFF" stroke-width="6" stroke-linecap="round"></path><path d="M110 86q8-6 16-2" stroke="#FFFFFF" stroke-width="4" fill="none" stroke-linecap="round"></path></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Housing Scout</h3><span class="cprice">$18<small>/mo</small></span></div>
<p class="cdesc">Watches shelter beds, waitlists and landlord listings overnight and wakes you with three real options, not forty tabs.</p>
<p class="cskills">Shelter beds · Waitlists · Listing alerts</p>
</div>
</article>

<article class="card" data-tags="legal">
<div class="stage rings st4">
<span class="tag">Never late</span><span class="code">AGT-04</span>
<button class="poke" type="button" data-poke aria-label="Poke the Court Date Keeper">
<svg class="moji d4" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peri)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="95" r="8.4" fill="#15111F"></circle><circle cx="73" cy="91" r="2.6" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="124" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="95" r="8.4" fill="#15111F"></circle><circle cx="121" cy="91" r="2.6" fill="#FFFFFF"></circle></g></g><path d="M92 122q8-5 16 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><g transform="translate(118 116) rotate(8)"><rect width="58" height="54" rx="8" fill="#FFFFFF" stroke="#15111F" stroke-width="3.5"></rect><rect width="58" height="16" rx="8" fill="#B56CFF" stroke="#15111F" stroke-width="3.5"></rect><path d="M14 -6v12M44 -6v12" stroke="#15111F" stroke-width="4" stroke-linecap="round"></path><text x="29" y="47" text-anchor="middle" font-family="Stardos Stencil, serif" font-weight="700" font-size="26" fill="#15111F">31</text></g></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Court Date Keeper</h3><span class="cprice">$12<small>/mo</small></span></div>
<p class="cdesc">Tracks hearings, filing windows and check-ins, and sends reminders the client can actually read, in the language they read.</p>
<p class="cskills">Hearings · Filing windows · Reminders</p>
</div>
</article>

<article class="card" data-tags="crisis">
<div class="stage rings st5">
<span class="tag">Included</span><span class="code">AGT-05</span>
<button class="poke" type="button" data-poke aria-label="Poke the Crisis Triage agent">
<svg class="moji d1" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-violet)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="64" cy="102" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="64" cy="103" r="8.4" fill="#15111F"></circle><circle cx="61" cy="99" r="2.6" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="100" cy="98" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="100" cy="99" r="8.4" fill="#15111F"></circle><circle cx="97" cy="95" r="2.6" fill="#FFFFFF"></circle></g></g><g class="eye"><ellipse cx="136" cy="102" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="136" cy="103" r="8.4" fill="#15111F"></circle><circle cx="133" cy="99" r="2.6" fill="#FFFFFF"></circle></g></g><path d="M52 84q12-8 24-2M124 82q12-6 24 2" fill="none" stroke="#15111F" stroke-width="4" stroke-linecap="round"></path><path d="M88 134q6-5 12 0t12 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><path d="M150 60q-6 9 0 12q6-3 0-12z" fill="#BFE3FF" stroke="#15111F" stroke-width="2.5"></path></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Crisis Triage</h3><span class="cprice">Free</span></div>
<p class="cdesc">Reads incoming messages for risk at 3am and pages the on-call person within seconds. It never answers a crisis on its own.</p>
<p class="cskills">Risk flags · Paging · Warm handoff</p>
</div>
</article>

<article class="card" data-tags="intake benefits">
<div class="stage rings st6">
<span class="tag">Quick</span><span class="code">AGT-06</span>
<button class="poke" type="button" data-poke aria-label="Poke the Follow-up Runner">
<svg class="moji d2" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#4F86FF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M84 124q16 14 32 0" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><path d="M50 88h100l-4 6q-6 20-26 18q-14-2-16-16h-4q-2 14-16 16q-20 2-26-18z" fill="#15111F"></path><path d="M62 96l14-8M118 96l14-8" stroke="#FFFFFF" stroke-width="4" stroke-linecap="round" opacity=".8"></path><g transform="translate(156 152) rotate(70) scale(.9)"><rect x="-20" y="-6" width="40" height="34" rx="12" fill="#FFB21C" stroke="#15111F" stroke-width="3"></rect><rect x="-8" y="-34" width="15" height="34" rx="7.5" fill="#FFC94A" stroke="#15111F" stroke-width="3"></rect><path d="M-20 6h40M-20 16h40" stroke="#E08A0F" stroke-width="2.5" stroke-linecap="round"></path></g></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Follow-up Runner</h3><span class="cprice">$10<small>/mo</small></span></div>
<p class="cdesc">Sends the check-in texts, chases the missing pay stub and books the next visit, in your words, from templates you approved.</p>
<p class="cskills">Check-ins · Document chase · Scheduling</p>
</div>
</article>

<article class="card" data-tags="language">
<div class="stage rings st7">
<span class="tag">38 languages</span><span class="code">AGT-07</span>
<button class="poke" type="button" data-poke aria-label="Poke the Interpreter">
<svg class="moji d3" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M104 30q-4-16 8-20q12-2 10 10" fill="none" stroke="#3D7BFF" stroke-width="8" stroke-linecap="round"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle><circle cx="72.6" cy="96.6" r="2.9" fill="#FFFFFF"></circle></g></g><path d="M108 100q16-12 32 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path><path d="M86 124q16 12 30-2" fill="none" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><g transform="translate(48 160) rotate(-8)"><rect x="-20" y="-6" width="40" height="34" rx="12" fill="#FFB21C" stroke="#15111F" stroke-width="3"></rect><rect x="-8" y="-34" width="15" height="34" rx="7.5" fill="#FFC94A" stroke="#15111F" stroke-width="3"></rect><path d="M-20 6h40M-20 16h40" stroke="#E08A0F" stroke-width="2.5" stroke-linecap="round"></path></g></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Interpreter</h3><span class="cprice">$15<small>/mo</small></span></div>
<p class="cdesc">Translates visits and letters with a confidence score on every sentence, so you know exactly when to bring in a human interpreter.</p>
<p class="cskills">Live visits · Letters · Confidence score</p>
</div>
</article>

<article class="card" data-tags="intake legal">
<div class="stage rings st8">
<span class="tag">Does the forms</span><span class="code">AGT-08</span>
<button class="poke" type="button" data-poke aria-label="Poke the Records Clerk">
<svg class="moji d4" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-lilac)" stroke="#15111F" stroke-width="5"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-shade)"></path><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-gloss)"></path><path d="M52 78q10-14 26-22" fill="none" stroke="#FFFFFF" stroke-width="7" stroke-linecap="round" opacity=".8"></path><path d="M62 88l26 26M88 88l-26 26" stroke="#15111F" stroke-width="7" stroke-linecap="round"></path><g class="eye"><ellipse cx="124" cy="102" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="103" r="9.5" fill="#15111F"></circle><circle cx="120.6" cy="98.6" r="2.9" fill="#FFFFFF"></circle></g><path d="M106 103A18 19 0 0 1 142 103Z" fill="#B56CFF" stroke="#15111F" stroke-width="3" stroke-linejoin="round"></path></g><path d="M108 82l30-8" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path><path d="M86 134h28" stroke="#15111F" stroke-width="4.5" stroke-linecap="round"></path></g></svg>
</button>
</div>
<div class="cbody">
<div class="chead"><h3 class="disp cname">Records Clerk</h3><span class="cprice">$9<small>/mo</small></span></div>
<p class="cdesc">Types the same address into eleven forms so nobody else has to. Tired. Accurate. Logs every field it touched.</p>
<p class="cskills">Form fill · Field audit · Redaction</p>
</div>
</article>

</div>
</div>
</section>

<!-- APPROVAL QUEUE -->
<section data-section="queue" style="position: relative; overflow: hidden; background: #F4EFE6">
<svg class="grain" aria-hidden="true" style="opacity: .14"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<div class="wrap" style="position: relative; padding-top: clamp(80px, 10vw, 160px); padding-bottom: clamp(80px, 10vw, 160px)">
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 440px), 1fr)); gap: 56px 72px; align-items: center">
<div>
<p class="label">03 — The approval queue</p>
<h2 class="disp" style="margin-top: 24px; font-size: clamp(44px, 6vw, 100px)">Nothing sends itself.</h2>
<p style="max-width: 520px; margin: 28px 0 0; font-size: 20px; line-height: 1.55; color: #3A3347">Letters, texts and filings land in one queue. A caseworker reads each draft, edits what needs editing, and presses approve. Then, and only then, it goes out.</p>
</div>
<div style="background: #FFFFFF; border: 3px solid #15111F; border-radius: 24px; box-shadow: 8px 8px 0 #15111F; overflow: hidden">
<div style="display: flex; justify-content: space-between; align-items: center; gap: 12px; padding: 18px 22px; background: #15111F; color: #F4EFE6">
<span style="font-weight: 700; font-size: 16px">Approval queue</span>
<span style="padding: 6px 12px; border-radius: 999px; background: #D4FF3A; color: #15111F; font-size: 13px; font-weight: 700">3 waiting</span>
</div>
<div class="qrow" style="border-top: 0">
<span style="display: block; width: 52px; height: 52px"><svg class="moji d1" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-sun)" stroke="#15111F" stroke-width="7"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M86 126q14 13 28 0z" fill="#15111F"></path></g></svg></span>
<div style="min-width: 0"><p style="margin: 0; font-weight: 700; font-size: 16px">SNAP application, pre-filled</p><p style="margin: 4px 0 0; font-size: 14px; color: #5A5168">Benefits Navigator · Rivera household</p></div>
<div style="display: flex; gap: 8px"><button class="qbtn" type="button">Edit</button><button class="qbtn go" type="button">Approve</button></div>
</div>
<div class="qrow">
<span style="display: block; width: 52px; height: 52px"><svg class="moji d3" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peri)" stroke="#15111F" stroke-width="7"></path><g class="eye"><ellipse cx="76" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="95" r="8.4" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="95" r="8.4" fill="#15111F"></circle></g></g><path d="M92 124q8-5 16 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<div style="min-width: 0"><p style="margin: 0; font-weight: 700; font-size: 16px">Hearing reminder, in Spanish</p><p style="margin: 4px 0 0; font-size: 14px; color: #5A5168">Court Date Keeper · Okafor case</p></div>
<div style="display: flex; gap: 8px"><button class="qbtn" type="button">Edit</button><button class="qbtn go" type="button">Approve</button></div>
</div>
<div class="qrow">
<span style="display: block; width: 52px; height: 52px"><svg class="moji d2" viewBox="0 0 200 200" aria-hidden="true"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peach)" stroke="#15111F" stroke-width="7"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M90 130h20" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<div style="min-width: 0"><p style="margin: 0; font-weight: 700; font-size: 16px">Three shelter options</p><p style="margin: 4px 0 0; font-size: 14px; color: #5A5168">Housing Scout · Tran family</p></div>
<div style="display: flex; gap: 8px"><button class="qbtn" type="button">Edit</button><button class="qbtn go" type="button">Approve</button></div>
</div>
</div>
</div>

<div style="display: flex; flex-wrap: wrap; align-items: center; gap: 14px; margin-top: clamp(64px, 8vw, 112px); padding-top: 32px; border-top: 3px solid #15111F">
<span class="label" style="margin-right: 12px">Built for</span>
<span class="chip">HIPAA</span>
<span class="chip">42 CFR Part 2</span>
<span class="chip">SOC 2</span>
<span class="chip">State retention rules</span>
</div>

<figure style="margin: clamp(64px, 8vw, 112px) 0 0">
<blockquote class="serif" style="margin: 0; max-width: 1180px; font-size: clamp(40px, 5.4vw, 84px); line-height: 1.02">“The swarm gave my caseworkers back <span style="padding: 0 .12em; background: #D4FF3A; font-style: normal; font-family: 'IBM Plex Mono', monospace; font-weight: 600; font-size: .7em">[X hours]</span> a week, and not one letter went out unread.”</blockquote>
<figcaption class="label" style="margin-top: 28px">[Name] — [Title], [Agency]</figcaption>
</figure>
</div>
</section>

<!-- GUARDRAILS -->
<section id="guardrails" data-section="guardrails" class="rings ink-rings" style="background-color: #15111F; color: #F4EFE6">
<div class="wrap" style="padding-top: clamp(80px, 10vw, 160px); padding-bottom: clamp(80px, 10vw, 160px)">
<p class="label" style="color: #D4FF3A">04 — Guardrails</p>
<h2 class="disp" style="margin-top: 24px; font-size: clamp(48px, 8.4vw, 136px)">Drafts.<span class="serif" style="display: block; font-size: .72em; line-height: 1; color: #D4FF3A">never decisions.</span></h2>
<p style="max-width: 640px; margin: 32px 0 0; font-size: 20px; line-height: 1.6; color: #CFC6E8">Casework is people's housing, children and freedom. The swarm is built to be useful and boring about it: it prepares, it reminds, it asks. A person is on every decision that matters.</p>
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 300px), 1fr)); gap: 24px; margin-top: clamp(56px, 7vw, 96px)">
<div class="rule"><p class="disp" style="font-size: 40px; color: #D4FF3A">Consent</p><p style="margin: 0; font-weight: 700; font-size: 19px">Listens only with consent</p><p style="margin: 0; font-size: 16px; line-height: 1.55; color: #CFC6E8">The scribe starts when the client says yes, out loud, and the note says so.</p></div>
<div class="rule"><p class="disp" style="font-size: 40px; color: #D4FF3A">Approve</p><p style="margin: 0; font-weight: 700; font-size: 19px">Nothing sends itself</p><p style="margin: 0; font-size: 16px; line-height: 1.55; color: #CFC6E8">Letters, texts and filings wait in a queue until a caseworker approves them.</p></div>
<div class="rule"><p class="disp" style="font-size: 40px; color: #D4FF3A">Escalate</p><p style="margin: 0; font-weight: 700; font-size: 19px">Crisis goes to a human</p><p style="margin: 0; font-size: 16px; line-height: 1.55; color: #CFC6E8">Triage pages the on-call worker. It never answers a crisis on its own.</p></div>
<div class="rule"><p class="disp" style="font-size: 40px; color: #D4FF3A">Audit</p><p style="margin: 0; font-weight: 700; font-size: 19px">Every action is logged</p><p style="margin: 0; font-size: 16px; line-height: 1.55; color: #CFC6E8">Who asked, which agent acted, what it read and what it changed, kept for your agency's retention period.</p></div>
</div>
</div>
</section>

<!-- PRICING -->
<section id="pricing" data-section="pricing" style="position: relative; overflow: hidden; background: #F4EFE6">
<svg class="grain" aria-hidden="true" style="opacity: .14"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<div class="wrap" style="position: relative; padding-top: clamp(80px, 10vw, 160px); padding-bottom: clamp(80px, 10vw, 160px)">
<p class="label">05 — Pricing</p>
<h2 class="disp" style="margin-top: 24px; font-size: clamp(48px, 8.4vw, 136px)">Pick your crew.</h2>
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(min(100%, 320px), 1fr)); gap: 36px; margin-top: clamp(56px, 7vw, 96px); align-items: stretch">
<div class="plan">
<p class="label">Pick &amp; mix</p>
<p style="margin: 0"><span class="disp" style="font-size: 60px">$9</span><span style="font-size: 16px; font-weight: 600; color: #5A5168"> from, per agent / month</span></p>
<p style="margin: 0; font-size: 17px; line-height: 1.55; color: #3A3347">Any agent, any seat count. Start with the one that hurts most.</p>
<ul><li>Choose from 8 agents</li><li>Crisis Triage included</li><li>Approval queue and audit log</li></ul>
<a class="btn btn-paper" href="#book" style="margin-top: auto">Start small</a>
</div>
<div class="plan" style="background: #15111F; color: #F4EFE6; box-shadow: 8px 8px 0 #FF3D1F">
<p class="label" style="color: #D4FF3A">Full swarm</p>
<p style="margin: 0"><span class="disp" style="font-size: 60px">[Price]</span><span style="font-size: 16px; font-weight: 600; color: #B9B0CC"> per caseworker / month</span></p>
<p style="margin: 0; font-size: 17px; line-height: 1.55; color: #CFC6E8">All eight agents, working the same case in parallel lanes.</p>
<ul style="color: #D4FF3A"><li><span style="color: #F4EFE6">Every agent, every seat</span></li><li><span style="color: #F4EFE6">Your templates and note formats</span></li><li><span style="color: #F4EFE6">Approval queue and audit log</span></li></ul>
<a class="btn btn-lime" href="#book" style="margin-top: auto; border-color: #D4FF3A; box-shadow: 8px 8px 0 #FF3D1F">Book a demo</a>
</div>
<div class="plan">
<p class="label">Agency</p>
<p style="margin: 0"><span class="disp" style="font-size: 60px">Let's talk</span></p>
<p style="margin: 0; font-size: 17px; line-height: 1.55; color: #3A3347">County-wide rollouts, your roles, your retention rules.</p>
<ul><li>SSO and role-based access</li><li>Custom agency templates</li><li>Retention and redaction controls</li></ul>
<a class="btn btn-paper" href="#book" style="margin-top: auto">Contact sales</a>
</div>
</div>
</div>
</section>

<!-- FINAL CTA + FOOTER -->
<section id="book" data-section="book" class="rings hero-rings" style="position: relative; overflow: hidden; background-color: #FF5A3C; color: #15111F; border-top: 3px solid #15111F">
<svg class="grain" aria-hidden="true"><rect width="100%" height="100%" filter="url(#ks-noise)"></rect></svg>
<div class="wrap" style="position: relative; padding-top: clamp(80px, 10vw, 160px)">
<div aria-hidden="true" style="display: flex; flex-wrap: wrap; gap: clamp(8px, 1.6vw, 24px); margin-bottom: 40px">
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d1" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M88 128q12 9 24 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d2" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-sun)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M86 126q14 13 28 0z" fill="#15111F"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d3" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peach)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M90 130h20" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d4" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-peri)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="76" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="95" r="8.4" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="124" cy="94" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="95" r="8.4" fill="#15111F"></circle></g></g><path d="M92 124q8-5 16 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d1" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-violet)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="64" cy="102" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="64" cy="103" r="8.4" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="100" cy="98" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="100" cy="99" r="8.4" fill="#15111F"></circle></g></g><g class="eye"><ellipse cx="136" cy="102" rx="15" ry="16.2" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="136" cy="103" r="8.4" fill="#15111F"></circle></g></g><path d="M88 134q6-5 12 0t12 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d2" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="6"></path><path d="M50 88h100l-4 6q-6 20-26 18q-14-2-16-16h-4q-2 14-16 16q-20 2-26-18z" fill="#15111F"></path><path d="M84 124q16 14 32 0" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d3" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-blue)" stroke="#15111F" stroke-width="6"></path><g class="eye"><ellipse cx="76" cy="100" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="76" cy="101" r="9.5" fill="#15111F"></circle></g></g><path d="M108 100q16-12 32 0" fill="none" stroke="#15111F" stroke-width="6" stroke-linecap="round"></path><path d="M86 124q16 12 30-2" fill="none" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
<span style="display: block; width: clamp(56px, 7vw, 96px); height: clamp(56px, 7vw, 96px)"><svg class="moji d4" viewBox="0 0 200 200"><g class="bod"><path d="M100 22C112 22 118 28 128 38L166 76C176 86 182 94 182 104S176 122 166 132L128 170C118 180 112 186 100 186S82 180 72 170L34 132C24 122 18 114 18 104S24 86 34 76L72 38C82 28 88 22 100 22Z" fill="url(#ks-lilac)" stroke="#15111F" stroke-width="6"></path><path d="M62 88l26 26M88 88l-26 26" stroke="#15111F" stroke-width="8" stroke-linecap="round"></path><g class="eye"><ellipse cx="124" cy="102" rx="17" ry="18.4" fill="#F6EFDC"></ellipse><g class="pupil"><circle cx="124" cy="103" r="9.5" fill="#15111F"></circle></g><path d="M106 103A18 19 0 0 1 142 103Z" fill="#B56CFF" stroke="#15111F" stroke-width="4" stroke-linejoin="round"></path></g><path d="M86 134h28" stroke="#15111F" stroke-width="5" stroke-linecap="round"></path></g></svg></span>
</div>
<h2 class="disp" style="font-size: clamp(56px, 10.5vw, 172px)"><span class="rings wave-text">Give the desk back.</span></h2>
<div style="display: flex; flex-wrap: wrap; align-items: center; gap: 24px 40px; margin-top: 48px; padding-bottom: clamp(80px, 9vw, 140px)">
<a class="btn btn-ink" href="#book" style="min-height: 68px; padding: 0 40px; font-size: 20px; box-shadow: none">Book a demo</a>
<p class="serif" style="margin: 0; font-size: clamp(26px, 2.4vw, 36px)">Thirty minutes. Bring a real case.</p>
</div>
</div>
<footer data-section="footer" style="position: relative; border-top: 3px solid #15111F">
<div class="wrap" style="display: flex; flex-wrap: wrap; justify-content: space-between; align-items: center; gap: 20px 40px; padding-top: 32px; padding-bottom: 20px">
<a href="#top" class="disp" style="font-size: 24px; line-height: 1; text-decoration: none">Kind Swarm</a>
<div style="display: flex; flex-wrap: wrap; gap: 8px 28px">
<a class="navlink" href="#how">How it works</a>
<a class="navlink" href="#crew">Agents</a>
<a class="navlink" href="#guardrails">Guardrails</a>
<a class="navlink" href="#pricing">Pricing</a>
</div>
</div>
<p class="wrap" style="margin: 0 auto; padding-bottom: 40px; font-size: 14px; line-height: 1.6; font-weight: 500">© 2026 Kind Swarm. A fictional product made for the INSTALANDING.AI library: the agents, prices, counties, certifications and numbers are invented, and nothing on this page is advice about running casework.</p>
</footer>
</section>

</div>
<script>
(function () {
  'use strict';

  /* Eyes follow the pointer: every pupil reads --px / --py from the root */
  var root = document.documentElement.style;
  window.addEventListener('pointermove', function (e) {
    var x = (e.clientX / window.innerWidth - 0.5) * 2, y = (e.clientY / window.innerHeight - 0.5) * 2;
    root.setProperty('--px', (x * 7).toFixed(2) + 'px');
    root.setProperty('--py', (y * 7).toFixed(2) + 'px');
  }, { passive: true });

  /* Poke a character: replay its .react animation (remove, reflow, add) */
  var pokeT;
  document.addEventListener('click', function (e) {
    var b = e.target.closest('[data-poke]');
    if (!b) return;
    var m = b.querySelector('.moji');
    var on = document.querySelectorAll('.moji.react');
    for (var i = 0; i < on.length; i++) on[i].classList.remove('react');
    void m.getBoundingClientRect();
    m.classList.add('react');
    clearTimeout(pokeT);
    pokeT = setTimeout(function () { m.classList.remove('react'); }, 780);
  });

  /* Filter the crew by job */
  var pills = document.querySelectorAll('[data-filter]'), cards = document.querySelectorAll('[data-tags]'), count = document.getElementById('count');
  for (var i = 0; i < pills.length; i++) pills[i].addEventListener('click', function () {
    var f = this.getAttribute('data-filter'), n = 0;
    for (var j = 0; j < pills.length; j++) {
      var on = pills[j] === this;
      pills[j].classList.toggle('on', on);
      pills[j].setAttribute('aria-pressed', on ? 'true' : 'false');
    }
    for (j = 0; j < cards.length; j++) {
      var show = f === 'all' || cards[j].getAttribute('data-tags').split(' ').indexOf(f) > -1;
      cards[j].hidden = !show;
      if (show) n++;
    }
    count.textContent = (n < 10 ? '0' : '') + n;
  });
})();
</script>
</body>
</html>
```

