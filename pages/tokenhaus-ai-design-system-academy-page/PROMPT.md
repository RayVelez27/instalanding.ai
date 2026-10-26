INSTALANDING.AI · tokenhaus AI Design System Academy Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
tokenhaus AI Design System Academy Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/tokenhaus-ai-design-system-academy-page

tokenhaus-design-academy.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · tokenhaus AI Design System Academy Page
  slug     tokenhaus-ai-design-system-academy-page
  prompt   https://instalanding.ai/p/tokenhaus-ai-design-system-academy-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/tokenhaus-ai-design-system-academy-page
  license  Fictional brand ("tokenhaus", online from Lisbon); every course, price, tutor, student, figure and quote is
           invented. Replace names, numbers and copy before shipping. Every picture is SVG drawn in code; no image files.

  MAP
  tokens    one :root block at the top of the <style>: four inks on paper: --paper, --ink, --amber, --sky, --pink and
            --light; Gabarito (--display, 900 uppercase) and Instrument Sans (--text); --k (fill-to-width ratio),
            --gut / --side / --wrap / --pad / --gap, --hh (header), --pill, --rq (the big quarter-round corner), --ease.
  sections  nav, hero, about, courses, manifesto, work, process, tutors, numbers, voices, fees, faq, contact, footer
            (each region carries data-section)
  scripts   1. Coded artwork: a token-swatch fan, a wall of component cards, a "Blue 500" specimen, stacked elevation
               sheets, radius curves, a case of amber glyph keys, a theme roller and four halftone portraits, all
               written into svg[data-art] as SVG strings
            2. UI that works without motion: the hide-on-scroll header and menu, echo copies of the outlined words,
               the sticky hero offset, the course and FAQ accordions, bar widths from their % labels
            3. (motion only) GSAP 3.13 + ScrollTrigger + SplitText and Lenis 1.3.4 (jsdelivr): hero tiles turning
               and pills shrinking to dots as the next section covers the sticky hero, lines masking up, course
               pills growing from circles, the "SYSTEM" echoes fanning out in four inks, the work grid sliding in
               from four sides, a rolling disc down the process rail, tutor prints wiping in, stat cards turning up
               from their corner, stacked quote cards, fee cards rising
  assets    no image files

  ADAPTING
  - A tile is <i class="t q|h|ring|dot|bar"> with --tb (ground), --tf (shape) and --r (quarter turns); data-turn
    sets how far it turns on scroll.
  - Fill-to-width words (.fit) size from --len (letters) times --k and are capped by --cap.
  - data-echo="n" adds n stacked outline copies of a word; data-echo-inks colours them pink, amber, light, ink.
  - prefers-reduced-motion: no sticky hero cover, scrubbing or loops; accordions and the page still work.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>tokenhaus — AI Design System Academy</title>
<meta name="description" content="Live cohorts on building design systems with AI: tokens, components, docs and code sync. Small groups, real products, an AI pair at every step.">
<script>(function(d){if(!matchMedia('(prefers-reduced-motion: reduce)').matches){d.classList.add('motion');setTimeout(function(){if(!window.gsap)d.classList.remove('motion')},2500)}})(document.documentElement);</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Gabarito:wght@600..900&family=Instrument+Sans:wght@400..600&display=swap">
<style>@property --m{syntax:'<length>';inherits:true;initial-value:0px;}:root{--paper:#e7ecf0;--ink:#212445;--amber:#ffa802;--sky:#00a9ff;--pink:#ff73a5;--light:#fdfefd;--display:'Gabarito', system-ui, sans-serif;--text:'Instrument Sans', system-ui, sans-serif;--k:.7;--gut:clamp(10px, 1.6vw, 22px);--hh:64px;--side:clamp(16px, 4vw, 56px);--wrap:1320px;--pad:clamp(80px, 11vw, 168px);--gap:clamp(14px, 1.8vw, 24px);--pill:999px;--rq:clamp(96px, 18vw, 280px);--ease:cubic-bezier(.7, 0, .2, 1);}@media (max-width:899px){:root{--hh:56px;}}*, *::before, *::after{box-sizing:border-box;}html{-webkit-text-size-adjust:100%;}body{margin:0;background:var(--paper);color:var(--ink);font:400 17px/1.55 var(--text);-webkit-font-smoothing:antialiased;}img{display:block;max-width:100%;}a{color:inherit;}h1, h2, h3, p, ul, ol, figure, blockquote, dl, dd{margin:0;padding:0;}ul, ol{list-style:none;}button{font:inherit;color:inherit;background:none;border:0;padding:0;cursor:pointer;}:focus-visible{outline:3px solid var(--sky);outline-offset:3px;}main > *{position:relative;z-index:1;background:var(--paper);overflow-x:clip;}.wrap{max-width:var(--wrap);margin-inline:auto;padding-inline:var(--side);}.vh{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap;}.motion [data-reveal]{opacity:0;}.h2{font:900 clamp(42px, 7.4vw, 112px)/.9 var(--display);letter-spacing:-.015em;text-transform:uppercase;overflow-wrap:break-word;hyphens:auto;}.h3{font:800 clamp(22px, 2.1vw, 30px)/1.05 var(--display);letter-spacing:-.005em;overflow-wrap:break-word;hyphens:auto;}.lead{font-size:clamp(17px, 1.35vw, 19px);line-height:1.5;max-width:38ch;}.fill{container-type:inline-size;}.fit{display:block;white-space:nowrap;font-size:min(var(--cap, 1000px), calc(100cqw / (var(--len) * var(--k))));}.t{position:relative;display:block;background:var(--tb);overflow:hidden;}.t > b{position:absolute;inset:0;background:var(--tf);rotate:calc(var(--r, 0) * 90deg);}.q > b{border-radius:0 100% 0 0;}.h > b{clip-path:circle(50% at 50% 100%);}.ring > b{border-radius:0 100% 0 0;background:radial-gradient(circle at 0 100%, var(--tb) 34.5%, var(--tf) 34.9%);}.dot > b{clip-path:circle(30% at 50% 50%);}.bar > b{inset:34% 8%;border-radius:var(--pill);}.eye{position:absolute;width:12%;aspect-ratio:1;border-radius:50%;background:var(--amber);left:50%;top:34%;}[data-echo]{position:relative;isolation:isolate;display:block;padding-bottom:calc(var(--n, 0) * var(--eg, .34em));text-shadow:0 .05em var(--eb), 0 -.05em var(--eb), .05em 0 var(--eb), -.05em 0 var(--eb), .035em .035em var(--eb), -.035em .035em var(--eb), .035em -.035em var(--eb), -.035em -.035em var(--eb);}.echo-copy{position:absolute;left:0;top:0;width:100%;pointer-events:none;user-select:none;color:var(--ec, inherit);}.btn{--bf:var(--ink);--bt:var(--light);--bh:var(--pink);--bht:var(--ink);position:relative;isolation:isolate;overflow:hidden;display:inline-flex;align-items:center;gap:.6em;white-space:nowrap;padding:1em 1.55em;border-radius:var(--pill);background:var(--bf);color:var(--bt);font:700 16px/1 var(--display);letter-spacing:.01em;text-decoration:none;transition:color .45s var(--ease);}.btn::before{content:"";position:absolute;inset:0;z-index:-1;background:var(--bh);clip-path:circle(0 at 0 100%);transition:clip-path .55s var(--ease);}.btn-sm{padding:.8em 1.25em;font-size:15px;}.lnk{position:relative;display:inline-block;white-space:nowrap;font-weight:600;text-decoration:none;padding-bottom:4px;}.lnk::after{content:"";position:absolute;left:0;right:0;bottom:0;height:3px;border-radius:var(--pill);background:currentColor;transform-origin:right;}.icon-btn{display:inline-grid;place-items:center;transition:rotate .5s var(--ease);}@media (hover:hover){.btn:hover{color:var(--bht);}.btn:hover::before{clip-path:circle(150% at 0 100%);}.lnk:hover::after{animation:pillrun .7s var(--ease);}.icon-btn:hover, .c-row:hover .icon-btn, .fq-q:hover .icon-btn{rotate:90deg;}}@keyframes pillrun{0%{transform:scaleX(1);transform-origin:right;}45%{transform:scaleX(0);transform-origin:right;}46%{transform:scaleX(0);transform-origin:left;}100%{transform:scaleX(1);transform-origin:left;}}.site-head{position:fixed;inset:0 0 auto;z-index:50;height:var(--hh);display:flex;align-items:center;gap:28px;padding-inline:var(--side);background:var(--paper);transition:transform .5s var(--ease);}.site-head.is-hidden{transform:translateY(-101%);}.brand{display:inline-flex;align-items:center;gap:10px;text-decoration:none;font:800 24px/1 var(--display);letter-spacing:-.02em;white-space:nowrap;}.mark{display:grid;grid-template-columns:1fr 1fr;width:34px;height:17px;}.mark .t{width:17px;height:17px;}.nav{display:flex;gap:28px;margin-left:auto;font-size:15px;}.head-cta{margin-left:8px;}.menu-btn{display:none;width:46px;height:46px;margin-left:auto;border-radius:50%;background:var(--amber);gap:4px;align-content:center;}.menu-btn i{display:block;width:20px;height:5px;border-radius:var(--pill);background:var(--ink);transition:transform .45s var(--ease), opacity .3s;}.menu-btn[aria-expanded="true"] i:nth-child(1){transform:translateY(9px) rotate(45deg);}.menu-btn[aria-expanded="true"] i:nth-child(2){opacity:0;}.menu-btn[aria-expanded="true"] i:nth-child(3){transform:translateY(-9px) rotate(-45deg);}.menu{position:fixed;inset:var(--hh) 0 0;background:var(--ink);color:var(--light);padding:28px var(--side) 40px;display:flex;flex-direction:column;gap:8px;overflow-y:auto;}.menu[hidden]{display:none;}.menu a{font:900 clamp(38px, 11vw, 64px)/1.05 var(--display);text-transform:uppercase;text-decoration:none;overflow-wrap:break-word;}.menu .btn{--bf:var(--amber);--bt:var(--ink);--bh:var(--pink);margin-top:24px;align-self:flex-start;font:700 17px/1 var(--display);text-transform:none;}@media (max-width:1079px){.nav, .head-cta{display:none;}.menu-btn{display:inline-grid;}}.hero{position:sticky;top:var(--stick, 0px);z-index:0;padding:calc(var(--hh) + var(--gut)) var(--gut) var(--gut);container-type:inline-size;}.hero-grid{--m:min(calc((100svh - var(--hh) - 2 * var(--gut)) / 4.42), calc(100cqw / 7));--fw:calc(var(--m) * 5.55);position:relative;display:grid;width:calc(7 * var(--m));margin-inline:auto;background:var(--ink);color:var(--light);grid-template-columns:repeat(7, var(--m));grid-template-rows:minmax(0, 1fr) auto auto auto;grid-template-areas:"fig fig fig fig pills pills pills" "fig fig fig fig top top top" "fig fig fig fig intro intro intro" "band band band band band band band";}.fig{grid-area:fig;height:calc(3 * var(--m));display:grid;grid-template-columns:repeat(4, 1fr);grid-template-rows:repeat(3, var(--m));}.fig .big{grid-column:span 2;grid-row:span 2;}.pills{grid-area:pills;min-height:calc(var(--m) * .9);background:var(--amber);display:flex;flex-direction:column;justify-content:space-evenly;gap:calc(var(--m) * .08);padding:calc(var(--m) * .14) calc(var(--m) * .16);overflow:hidden;}.pills i{display:block;width:86%;height:calc(var(--m) * .26);border-radius:var(--pill);background:var(--ink);}.h1{display:contents;}.h1-top{grid-area:top;display:block;background:var(--sky);color:var(--ink);padding:calc(var(--m) * .2) calc(var(--m) * .16) calc(var(--m) * .04);font:900 calc(var(--m) * .25)/.95 var(--display);text-transform:uppercase;letter-spacing:.01em;overflow-wrap:break-word;}.h1-top > span{--eb:var(--sky);}.intro{grid-area:intro;background:var(--sky);color:var(--ink);padding:calc(var(--m) * .1) calc(var(--m) * .16) calc(var(--m) * .18);display:grid;gap:16px;align-content:start;}.intro .lead{font-size:clamp(15px, 1.15vw, 18px);max-width:46ch;}.actions{display:flex;flex-wrap:wrap;align-items:center;gap:14px 24px;}.band{grid-area:band;position:relative;min-height:var(--m);}.corner{--r:0;position:absolute;left:0;bottom:0;width:var(--m);height:var(--m);}.h1-big{grid-area:band;position:relative;z-index:1;align-self:end;display:block;white-space:nowrap;padding:calc(var(--m) * .2) 0 calc(var(--m) * .12) calc(var(--m) * 1.26);font:900 min(calc(var(--m) * 1.35), calc(var(--fw) / (var(--len) * var(--k))))/.8 var(--display);text-transform:uppercase;letter-spacing:-.01em;}.shade{position:absolute;inset:0;background:var(--ink);opacity:0;pointer-events:none;z-index:2;}@media (max-width:899px){.hero-grid{--m:calc(100cqw / 4);--fw:calc(var(--m) * 3.2);width:100%;grid-template-columns:repeat(4, minmax(0, 1fr));grid-template-rows:auto;grid-template-areas:"fig fig fig fig" "top top top top" "band band band band" "intro intro intro intro" "pills pills pills pills";}.h1-top{padding:22px 20px 4px;font-size:calc(var(--m) * .3);}.band{min-height:0;}.corner{--r:3;left:auto;right:0;width:calc(var(--m) * .62);height:calc(var(--m) * .62);}.h1-big{padding:16px 0 18px 20px;font-size:min(calc(var(--m) * 1.1), calc(var(--fw) / (var(--len) * var(--k))));}.intro{background:var(--amber);padding:22px 20px 8px;}.pills{min-height:0;padding:14px 20px 22px;gap:10px;margin-top:-1px;}.pills i{height:20px;}}.about{padding-block:var(--pad);}.about-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:var(--gap);}.say{grid-column:1 / 12;font:700 clamp(28px, 4.3vw, 66px)/1.06 var(--display);letter-spacing:-.012em;}.about-photo{grid-column:1 / 7;margin-top:clamp(40px, 6vw, 96px);position:relative;overflow:hidden;border-radius:0 var(--rq) 0 0;background:var(--sky);aspect-ratio:5 / 4;}.about-photo img{width:100%;height:100%;object-fit:cover;}.principles{grid-column:8 / 13;margin-top:clamp(40px, 6vw, 96px);display:grid;align-content:end;}.principles li{display:grid;grid-template-columns:64px minmax(0, 1fr);gap:6px 22px;padding-block:26px;border-top:3px solid var(--ink);}.principles .t{width:64px;height:64px;grid-row:span 2;}.principles p{color:color-mix(in oklab, var(--ink) 78%, var(--paper));}@media (max-width:899px){.say, .about-photo, .principles{grid-column:1 / -1;}.principles{margin-top:12px;}.principles li{grid-template-columns:52px minmax(0, 1fr);gap:4px 18px;}.principles .t{width:52px;height:52px;}}.courses{background:var(--amber);padding-block:var(--pad);}.sec-head{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:var(--gap);align-items:end;margin-bottom:clamp(40px, 6vw, 88px);}.sec-head .h2{grid-column:1 / 9;}.sec-head .lead{grid-column:9 / 13;}@media (max-width:899px){.sec-head .h2, .sec-head .lead{grid-column:1 / -1;}}.c-list{display:grid;gap:12px;}.c-item{--rh:104px;}.c-row{width:100%;min-height:var(--rh);display:grid;grid-template-columns:minmax(0, 1fr) auto auto;align-items:center;gap:8px 32px;text-align:left;padding:16px 20px 16px 44px;border-radius:var(--pill);background:var(--ink);color:var(--light);}.c-name{font:800 clamp(24px, 3vw, 44px)/1 var(--display);letter-spacing:-.01em;overflow-wrap:break-word;}.c-meta{font-size:15px;font-weight:500;color:color-mix(in oklab, var(--light) 72%, var(--ink));white-space:nowrap;}.c-ico{grid-column:3;grid-row:1;position:relative;width:60px;height:60px;border-radius:50%;background:var(--amber);}.c-ico i{position:absolute;left:50%;top:50%;width:24px;height:6px;margin:-3px 0 0 -12px;border-radius:var(--pill);background:var(--ink);transition:transform .45s var(--ease);}.c-ico i + i{transform:rotate(90deg);}.c-item.is-open .c-ico i + i{transform:rotate(0deg);}.c-item.is-open .c-row{border-radius:calc(var(--rh) / 2) calc(var(--rh) / 2) 0 0;clip-path:none !important;}.c-body{background:var(--ink);color:var(--light);border-radius:0 0 calc(var(--rh) / 2) calc(var(--rh) / 2);padding:8px 44px 44px;display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:24px var(--gap);}.c-body[hidden]{display:none;}.c-body > p{grid-column:1 / 7;font-size:18px;color:color-mix(in oklab, var(--light) 86%, var(--ink));}.c-facts{grid-column:7 / 10;display:grid;gap:6px;font-size:15px;}.c-facts dt{color:color-mix(in oklab, var(--light) 60%, var(--ink));}.c-facts dd + dt{margin-top:10px;}.c-buy{grid-column:10 / 13;display:grid;align-content:start;justify-items:start;gap:16px;}.c-price{font:900 clamp(32px, 3.4vw, 48px)/1 var(--display);color:var(--amber);white-space:nowrap;}.c-buy .btn{--bf:var(--amber);--bt:var(--ink);--bh:var(--pink);}.motion .c-item.is-open .c-body > *{animation:rise .6s var(--ease) both;}@keyframes rise{from{opacity:0;transform:translateY(14px);}}@media (max-width:899px){.c-item{--rh:84px;}.c-row{grid-template-columns:minmax(0, 1fr) auto;padding:14px 12px 14px 26px;gap:4px 16px;}.c-name{grid-column:1;grid-row:1;}.c-meta{grid-column:1;grid-row:2;font-size:14px;white-space:normal;}.c-ico{grid-column:2;grid-row:1 / 3;width:52px;height:52px;}.c-body{padding:4px 26px 32px;grid-template-columns:1fr;}.c-body > p, .c-facts, .c-buy{grid-column:1;}}.manifesto{background:var(--sky);padding-block:var(--pad);}.motion .manifesto{height:250svh;padding-block:0;}.motion .mf-stage{position:sticky;top:0;height:100svh;}.mf-stage{display:grid;align-content:center;gap:clamp(24px, 4svh, 48px);padding:calc(var(--hh) + 12px) var(--side) 32px;max-width:var(--wrap);margin-inline:auto;}.mf-word{font-family:var(--display);font-weight:900;text-transform:uppercase;line-height:.78;letter-spacing:-.01em;color:var(--ink);}.mf-word .fit{--eb:var(--sky);--eg:.2em;--cap:38svh;}.echo-copy[data-ink="1"]{color:var(--pink);}.echo-copy[data-ink="2"]{color:var(--amber);}.echo-copy[data-ink="3"]{color:var(--light);}.echo-copy[data-ink="4"]{color:var(--ink);}.mf-text{justify-self:end;max-width:26ch;font:700 clamp(21px, 2.3vw, 34px)/1.15 var(--display);letter-spacing:-.005em;}@media (max-width:899px){.motion .manifesto{height:200svh;}.mf-text{justify-self:start;}}.work{padding-block:var(--pad);}.w-wrap{container-type:inline-size;}.w-grid{--gm:calc(100cqw / 6);display:grid;grid-template-columns:repeat(6, minmax(0, 1fr));grid-auto-rows:var(--gm);}.w-it{position:relative;overflow:hidden;background:var(--sky);}.w-it img{width:100%;height:100%;object-fit:cover;}.w-it figcaption{position:absolute;left:12px;bottom:12px;max-width:calc(100% - 24px);padding:7px 14px;border-radius:18px;background:var(--paper);font-size:13px;line-height:1.3;font-weight:500;}.w-it.t{background:var(--tb);}.w-a{grid-column:1 / 3;grid-row:1 / 3;border-radius:0 0 0 var(--rq);}.w-s1{grid-column:3;grid-row:1;}.w-b{grid-column:4;grid-row:1 / 3;background:var(--pink);}.w-c{grid-column:5 / 7;grid-row:1;background:var(--amber);border-radius:0 calc(var(--gm) / 2) 0 0;}.w-s2{grid-column:3;grid-row:2;}.w-d{grid-column:5;grid-row:2;}.w-s3{grid-column:6;grid-row:2;}.w-e{grid-column:1 / 4;grid-row:3;background:var(--amber);}.w-f{grid-column:4;grid-row:3;border-radius:var(--gm) 0 0 0;background:var(--pink);}.w-s4{grid-column:5;grid-row:3;}.w-s5{grid-column:6;grid-row:3;}@media (max-width:899px){.w-grid{--gm:calc(100cqw / 2);grid-template-columns:repeat(2, minmax(0, 1fr));}.w-a{grid-column:1 / 3;grid-row:1 / 3;}.w-s1{grid-column:1;grid-row:3;}.w-b{grid-column:2;grid-row:3 / 5;}.w-s2{grid-column:1;grid-row:4;}.w-c{grid-column:1 / 3;grid-row:5;}.w-d{grid-column:1;grid-row:6;}.w-s3{grid-column:2;grid-row:6;}.w-e{grid-column:1 / 3;grid-row:7;}.w-f{grid-column:1;grid-row:8;}.w-s4{grid-column:2;grid-row:8;}.w-s5{display:none;}}.process{background:var(--pink);padding-block:var(--pad);}.pr-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:var(--gap);}.pr-head{grid-column:1 / 6;align-self:start;position:sticky;top:calc(var(--hh) + 32px);display:grid;gap:28px;}.pr-list{--disc:clamp(52px, 5.2vw, 76px);grid-column:7 / 13;position:relative;padding-left:calc(var(--disc) + clamp(24px, 3vw, 48px));}.pr-rail{position:absolute;left:calc(var(--disc) / 2 - 3px);top:0;bottom:0;width:6px;border-radius:var(--pill);background:color-mix(in oklab, var(--ink) 22%, var(--pink));}.pr-disc{position:absolute;left:0;top:0;width:var(--disc);aspect-ratio:1;border-radius:50%;overflow:hidden;display:grid;grid-template-columns:1fr 1fr;}.pr-disc i{background:var(--ink);}.pr-disc i + i{background:var(--light);}.pr-disc i + i + i{background:var(--amber);}.pr-disc i + i + i + i{background:var(--ink);}.pr-step{display:grid;gap:12px;padding-bottom:clamp(56px, 8vw, 112px);transition:opacity .6s var(--ease);}.pr-step:last-child{padding-bottom:0;}.pr-when{font:800 15px/1 var(--display);letter-spacing:.02em;display:inline-block;justify-self:start;padding:8px 14px;border-radius:var(--pill);background:var(--ink);color:var(--pink);white-space:nowrap;}.pr-step .h3{font-size:clamp(30px, 3.4vw, 52px);font-weight:900;text-transform:uppercase;line-height:.95;}.pr-step p{max-width:42ch;}.motion .pr-step:not(.is-on){opacity:.38;}@media (max-width:899px){.pr-head, .pr-list{grid-column:1 / -1;}.pr-head{position:static;margin-bottom:40px;}}.tutors{background:var(--ink);color:var(--light);padding-block:var(--pad);}.tutors .lead{color:color-mix(in oklab, var(--light) 80%, var(--ink));}.tu-grid{display:grid;grid-template-columns:repeat(4, minmax(0, 1fr));gap:clamp(28px, 3vw, 40px) var(--gap);}.tu-photo{position:relative;aspect-ratio:4 / 5;overflow:hidden;background:var(--tb);border-radius:0 50% 0 0 / 0 40% 0 0;margin-bottom:18px;}.tu-photo img{width:100%;height:100%;object-fit:cover;filter:grayscale(1) contrast(1.12);mix-blend-mode:multiply;}.tu .h3{color:var(--light);}.tu-role{margin-top:6px;font-size:15px;color:var(--sky);}@media (max-width:899px){.tu-grid{grid-template-columns:repeat(2, minmax(0, 1fr));}.tu-role{font-size:14px;}}.numbers{padding-block:var(--pad);}.nu-top{display:grid;grid-template-columns:repeat(auto-fit, minmax(min(100%, 250px), 1fr));margin-bottom:clamp(56px, 8vw, 120px);}.nu-card{position:relative;container-type:inline-size;min-height:clamp(240px, 26vw, 360px);padding:clamp(20px, 2.4vw, 36px);display:grid;align-content:space-between;gap:20px;background:var(--tb);color:var(--tx, var(--ink));overflow:hidden;}.nu-card:last-child{border-radius:0 var(--rq) 0 0;}.nu-fig{--cap:clamp(84px, 11vw, 168px);font:900 min(var(--cap), calc(100cqw / (var(--len) * var(--k)))) / .82 var(--display);letter-spacing:-.02em;white-space:nowrap;}.nu-card p:last-child{max-width:24ch;font-weight:500;}.nu-chart{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:var(--gap);align-items:start;}.nu-chart .h2{grid-column:1 / 6;font-size:clamp(38px, 5vw, 76px);}.bars{grid-column:7 / 13;display:grid;gap:22px;}.bar{display:grid;grid-template-columns:minmax(0, 1fr) auto;gap:8px 16px;align-items:end;}.bar-label{font-weight:600;}.bar-val{font:900 clamp(26px, 2.6vw, 38px)/1 var(--display);white-space:nowrap;}.bar-track{grid-column:1 / -1;grid-row:2;height:clamp(28px, 3vw, 40px);border-radius:var(--pill);background:color-mix(in oklab, var(--ink) 10%, var(--paper));overflow:hidden;}.bar-fill{display:block;height:100%;width:calc(var(--v, 50) * 1%);min-width:clamp(28px, 3vw, 40px);border-radius:var(--pill);background:var(--c, var(--ink));}@media (max-width:899px){.nu-top{grid-template-columns:1fr;}.nu-card{min-height:200px;}.nu-chart .h2, .bars{grid-column:1 / -1;}}.voices{background:var(--sky);padding-block:var(--pad);}.vo-stack{display:grid;gap:clamp(20px, 4vw, 40px);}.vo-card{position:sticky;top:calc(var(--hh) + 20px);min-height:min(64svh, 540px);display:grid;align-content:space-between;gap:36px;padding:clamp(28px, 4vw, 64px);padding-right:clamp(28px, 16vw, 240px);background:var(--tb);color:var(--tx, var(--ink));overflow:hidden;border-radius:0 0 var(--rq) 0;transform-origin:50% 0;}.vo-card blockquote p{font:700 clamp(26px, 3.3vw, 50px)/1.1 var(--display);letter-spacing:-.01em;max-width:26ch;}.vo-who{font-size:16px;}.vo-who strong{font:800 20px/1.2 var(--display);display:block;}.vo-shape{position:absolute;right:0;top:0;width:clamp(64px, 12vw, 180px);aspect-ratio:1;}@media (max-width:899px){.vo-card{padding-right:28px;padding-top:calc(clamp(64px, 12vw, 180px) + 12px);min-height:0;}}.fees{padding-block:var(--pad);}.fe-grid{display:grid;grid-template-columns:repeat(auto-fit, minmax(min(100%, 280px), 1fr));gap:var(--gap);align-items:stretch;}.fe-card{position:relative;display:grid;grid-template-rows:auto auto auto 1fr auto;gap:18px;padding:0 clamp(22px, 2.4vw, 36px) clamp(26px, 2.6vw, 40px);background:var(--light);color:var(--ink);overflow:hidden;container-type:inline-size;}.fe-card.is-main{background:var(--ink);color:var(--light);}.fe-head{margin:0 calc(-1 * clamp(22px, 2.4vw, 36px)) 8px;height:clamp(110px, 11vw, 150px);background:var(--tb);overflow:hidden;position:relative;}.fe-head b{position:absolute;left:50%;bottom:0;width:64%;aspect-ratio:2 / 1;translate:-50% 0;background:var(--tf);border-radius:999px 999px 0 0;}.fe-head.q b{left:0;width:auto;height:100%;aspect-ratio:1;translate:none;border-radius:0 100% 0 0;}.fe-head.o b{width:auto;height:76%;aspect-ratio:1;bottom:12%;border-radius:50%;}.fe-price{display:grid;gap:4px;}.fe-num{--cap:clamp(56px, 6vw, 88px);font:900 min(var(--cap), calc(100cqw / (var(--len) * var(--k)))) / .9 var(--display);letter-spacing:-.02em;white-space:nowrap;}.fe-per{font-size:15px;color:color-mix(in oklab, currentColor 70%, transparent);}.fe-list{display:grid;gap:10px;align-content:start;}.fe-list li{position:relative;padding-left:30px;}.fe-list li::before{content:"";position:absolute;left:0;top:.55em;width:18px;height:8px;border-radius:var(--pill);background:var(--pink);}.fe-card .btn{justify-self:start;}.fe-card.is-main .btn{--bf:var(--amber);--bt:var(--ink);--bh:var(--pink);}.faq{background:var(--amber);padding-block:var(--pad);}.fq-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:var(--gap);}.fq-head{grid-column:1 / 6;align-self:start;display:grid;gap:24px;position:sticky;top:calc(var(--hh) + 32px);}.fq-list{grid-column:7 / 13;border-top:3px solid var(--ink);}.fq-item{border-bottom:3px solid var(--ink);}.fq-q{width:100%;display:grid;grid-template-columns:minmax(0, 1fr) auto;gap:20px;align-items:center;text-align:left;padding:24px 0;font:800 clamp(20px, 1.9vw, 27px)/1.15 var(--display);}.fq-ico{grid-column:2;grid-row:1;position:relative;width:46px;height:46px;border-radius:50%;background:var(--ink);}.fq-ico i{position:absolute;left:50%;top:50%;width:18px;height:5px;margin:-2.5px 0 0 -9px;border-radius:var(--pill);background:var(--amber);transition:transform .45s var(--ease);}.fq-ico i + i{transform:rotate(90deg);}.fq-item.is-open .fq-ico i + i{transform:rotate(0deg);}.fq-a{padding:0 64px 28px 0;max-width:60ch;}.fq-a[hidden]{display:none;}.motion .fq-item.is-open .fq-a{animation:rise .5s var(--ease) both;}@media (max-width:899px){.fq-head, .fq-list{grid-column:1 / -1;}.fq-head{position:static;margin-bottom:32px;}.fq-a{padding-right:0;}}.contact{background:var(--ink);color:var(--light);padding-block:var(--pad);}.ct-word{font-family:var(--display);font-weight:900;text-transform:uppercase;line-height:.8;letter-spacing:-.01em;margin-bottom:clamp(48px, 7vw, 104px);}.ct-word .fit{--eb:var(--ink);--eg:.24em;--cap:34svh;}.ct-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:48px var(--gap);align-items:end;}.ct-info{grid-column:1 / 8;display:grid;gap:36px;}.ct-info .lead{color:color-mix(in oklab, var(--light) 84%, var(--ink));}.ct-list{display:grid;grid-template-columns:repeat(2, minmax(0, 1fr));gap:28px var(--gap);}.ct-list dt{font-size:14px;font-weight:600;color:var(--sky);margin-bottom:6px;}.ct-list dd{font-size:18px;overflow-wrap:anywhere;}.ct-list .lnk{white-space:normal;}.contact .btn{--bf:var(--amber);--bt:var(--ink);--bh:var(--pink);}.ct-fig{grid-column:9 / 13;display:grid;grid-template-columns:repeat(3, 1fr);}.ct-fig .t{aspect-ratio:1;}@media (max-width:899px){.ct-info, .ct-fig{grid-column:1 / -1;}.ct-list{grid-template-columns:1fr;}}.foot{position:relative;z-index:1;background:var(--paper);padding-top:clamp(56px, 7vw, 96px);}.foot-grid{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:32px var(--gap);padding-bottom:clamp(40px, 5vw, 64px);font-size:15px;}.foot-grid .brand{grid-column:1 / 4;align-self:start;}.foot-addr{grid-column:4 / 7;}.foot-nav{grid-column:7 / 10;display:grid;gap:6px;justify-items:start;}.foot-social{grid-column:10 / 13;display:grid;gap:6px;justify-items:start;}.foot-copy{grid-column:1 / -1;color:color-mix(in oklab, var(--ink) 65%, var(--paper));}@media (max-width:899px){.foot-grid .brand, .foot-addr{grid-column:1 / -1;}.foot-nav{grid-column:1 / 7;}.foot-social{grid-column:7 / -1;}}.inks{display:grid;grid-template-columns:repeat(4, 1fr);height:clamp(18px, 2.4vw, 30px);}.inks i{display:block;background:var(--c);transform-origin:bottom;}@media (prefers-reduced-motion:reduce){*, *::before, *::after{transition:none !important;animation:none !important;}}
/* Coded artwork (replaces all photography) */
.art{display:block;width:100%;height:100%;}
.art .i{fill:var(--ink);}.art .a{fill:var(--amber);}.art .s{fill:var(--sky);}.art .p{fill:var(--pink);}.art .l{fill:var(--light);}.art .g{fill:var(--paper);}
.art .tx{font-family:var(--display);font-weight:900;letter-spacing:-.01em;}
.art .st{fill:none;stroke:var(--ink);stroke-width:7;stroke-linecap:round;}
.art .st2{fill:none;stroke:var(--ink);stroke-width:4.5;stroke-linecap:round;stroke-linejoin:round;}
</style>
</head>
<body>

<header class="site-head" data-head data-section="nav">
  <a class="brand" href="#hero" aria-label="tokenhaus, home">
    <span class="mark" aria-hidden="true"><i class="t q" style="--tb:var(--paper);--tf:var(--amber);--r:3"><b></b></i><i class="t dot" style="--tb:var(--paper);--tf:var(--ink)"><b></b></i></span>
    <span>tokenhaus</span>
  </a>
  <nav class="nav" aria-label="Main">
    <a class="lnk" href="#courses">Courses</a>
    <a class="lnk" href="#work">Work</a>
    <a class="lnk" href="#tutors">Tutors</a>
    <a class="lnk" href="#fees">Fees</a>
    <a class="lnk" href="#faq">FAQ</a>
  </nav>
  <a class="btn btn-sm head-cta" href="#contact">Apply now</a>
  <button class="menu-btn icon-btn" type="button" aria-expanded="false" aria-controls="menu" aria-label="Open menu" data-label-open="Open menu" data-label-close="Close menu"><i></i><i></i><i></i></button>
  <nav class="menu" id="menu" aria-label="Menu" hidden>
    <a href="#courses">Courses</a>
    <a href="#work">Work</a>
    <a href="#tutors">Tutors</a>
    <a href="#fees">Fees</a>
    <a href="#faq">FAQ</a>
    <a class="btn" href="#contact">Apply now</a>
  </nav>
</header>

<main>

<section id="hero" data-section="hero" class="hero" data-kind="hero">
  <div class="hero-grid">
    <div class="fig" aria-hidden="true" data-fixed="9">
      <i class="t q big" data-turn="-1" style="--tb:var(--sky);--tf:var(--ink);--r:0"><b></b><em class="eye"></em></i>
      <i class="t q" data-turn="2" style="--tb:var(--ink);--tf:var(--amber);--r:1"><b></b></i>
      <i class="t q" data-turn="-2" style="--tb:var(--ink);--tf:var(--pink);--r:2"><b></b></i>
      <i class="t q" data-turn="-1" style="--tb:var(--ink);--tf:var(--light);--r:3"><b></b></i>
      <i class="t q" data-turn="-1" style="--tb:var(--ink);--tf:var(--sky);--r:2"><b></b></i>
      <i class="t q" data-turn="2" style="--tb:var(--amber);--tf:var(--ink);--r:1"><b></b></i>
      <i class="t q" data-turn="-2" style="--tb:var(--amber);--tf:var(--ink);--r:2"><b></b></i>
      <i class="t q" data-turn="-1" style="--tb:var(--pink);--tf:var(--ink);--r:0"><b></b></i>
      <i class="t q" data-turn="-1" style="--tb:var(--pink);--tf:var(--ink);--r:1"><b></b></i>
    </div>
    <div class="pills" aria-hidden="true"><i></i><i></i><i></i></div>
    <h1 class="h1"><span class="h1-top"><span data-echo="2">AI design systems</span></span> <span class="h1-big" style="--len:7">Academy</span></h1>
    <div class="intro">
      <p class="lead">Live cohorts on building design systems with AI: tokens, components and docs that ship. Twelve people per cohort, real product briefs, and an AI pair at every step.</p>
      <div class="actions">
        <a class="btn" href="#contact">Join the winter cohort</a>
        <a class="lnk" href="#courses">See the courses</a>
      </div>
    </div>
    <div class="band" aria-hidden="true"><i class="t q corner" style="--tb:var(--ink);--tf:var(--pink)"><b></b></i></div>
    <i class="shade" aria-hidden="true"></i>
  </div>
</section>

<section id="about" data-section="about" class="about" data-kind="about">
  <div class="wrap about-grid">
    <h2 class="say" data-split>We teach design systems the way a good system works: one source of truth, a clear set of tokens and AI that does the repetitive part. Small cohorts, real products, and everything you build ships to code.</h2>
    <figure class="about-photo" data-reveal-corner>
      <svg class="art" data-art="fan" viewBox="0 0 500 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A fan of colour token swatches and an amber sample on a grid"></svg>
    </figure>
    <ul class="principles">
      <li data-reveal>
        <i class="t q" data-turn="1" aria-hidden="true" style="--tb:var(--amber);--tf:var(--ink);--r:0"><b></b></i>
        <h3 class="h3">Tokens first</h3>
        <p>Colour, type, space and radius defined once, before anyone draws a component.</p>
      </li>
      <li data-reveal>
        <i class="t h" data-turn="1" aria-hidden="true" style="--tb:var(--sky);--tf:var(--ink);--r:0"><b></b></i>
        <h3 class="h3">A system you can defend</h3>
        <p>Every token and variant has a reason, and you learn to explain it to engineers.</p>
      </li>
      <li data-reveal>
        <i class="t ring" data-turn="1" aria-hidden="true" style="--tb:var(--pink);--tf:var(--ink);--r:0"><b></b></i>
        <h3 class="h3">AI as a pair, not a pilot</h3>
        <p>Models draft components and docs. You set the rules and review every output.</p>
      </li>
    </ul>
  </div>
</section>

<section id="courses" data-section="courses" class="courses" data-kind="services">
  <div class="wrap">
    <div class="sec-head">
      <h2 class="h2">Courses that end in production</h2>
      <p class="lead">Each course runs for twelve weeks, live online two evenings a week or on Saturdays. Take one, or combine two for a full term.</p>
    </div>
    <ul class="c-list" data-grow>
      <li class="c-item">
        <button class="c-row" type="button" aria-expanded="false">
          <span class="c-ico icon-btn" aria-hidden="true"><i></i><i></i></span>
          <span class="c-name">Design tokens &amp; foundations</span>
          <span class="c-meta">12 weeks · Tue &amp; Thu evenings</span>
        </button>
        <div class="c-body" hidden>
          <p>From a blank file to a full token set: colour, type, spacing, radius and motion, with light and dark themes generated and checked by AI.</p>
          <dl class="c-facts"><dt>Level</dt><dd>Beginners welcome</dd><dt>You leave with</dt><dd>A production token library</dd></dl>
          <div class="c-buy"><span class="c-price">$480</span><a class="btn btn-sm" href="#contact">Book a place</a></div>
        </div>
      </li>
      <li class="c-item">
        <button class="c-row" type="button" aria-expanded="false">
          <span class="c-ico icon-btn" aria-hidden="true"><i></i><i></i></span>
          <span class="c-name">Component architecture</span>
          <span class="c-meta">12 weeks · Mon &amp; Wed evenings</span>
        </button>
        <div class="c-body" hidden>
          <p>Anatomy, variants, states and accessibility, so that one button can serve a hundred screens.</p>
          <dl class="c-facts"><dt>Level</dt><dd>Beginners welcome</dd><dt>You leave with</dt><dd>A 30-component library</dd></dl>
          <div class="c-buy"><span class="c-price">$480</span><a class="btn btn-sm" href="#contact">Book a place</a></div>
        </div>
      </li>
      <li class="c-item">
        <button class="c-row" type="button" aria-expanded="false">
          <span class="c-ico icon-btn" aria-hidden="true"><i></i><i></i></span>
          <span class="c-name">AI-assisted generation</span>
          <span class="c-meta">12 weeks · Saturdays</span>
        </button>
        <div class="c-body" hidden>
          <p>Prompts, rule files and review loops that let models draft components, variants and tests inside your system's constraints.</p>
          <dl class="c-facts"><dt>Level</dt><dd>Some experience</dd><dt>You leave with</dt><dd>Your own generation pipeline</dd></dl>
          <div class="c-buy"><span class="c-price">$520</span><a class="btn btn-sm" href="#contact">Book a place</a></div>
        </div>
      </li>
      <li class="c-item">
        <button class="c-row" type="button" aria-expanded="false">
          <span class="c-ico icon-btn" aria-hidden="true"><i></i><i></i></span>
          <span class="c-name">Docs &amp; governance</span>
          <span class="c-meta">12 weeks · Tue &amp; Thu evenings</span>
        </button>
        <div class="c-body" hidden>
          <p>Usage guidelines, contribution models and AI-written docs, built for a real product team who joins the final review.</p>
          <dl class="c-facts"><dt>Level</dt><dd>Some experience</dd><dt>You leave with</dt><dd>A living documentation site</dd></dl>
          <div class="c-buy"><span class="c-price">$560</span><a class="btn btn-sm" href="#contact">Book a place</a></div>
        </div>
      </li>
      <li class="c-item">
        <button class="c-row" type="button" aria-expanded="false">
          <span class="c-ico icon-btn" aria-hidden="true"><i></i><i></i></span>
          <span class="c-name">Design-to-code sync</span>
          <span class="c-meta">6 weeks · Saturdays</span>
        </button>
        <div class="c-body" hidden>
          <p>Figma variables to code tokens, automated in CI. Break the build, fix it, and learn exactly why it broke.</p>
          <dl class="c-facts"><dt>Level</dt><dd>Some code helps</dd><dt>You leave with</dt><dd>A synced repo and pipeline</dd></dl>
          <div class="c-buy"><span class="c-price">$290</span><a class="btn btn-sm" href="#contact">Book a place</a></div>
        </div>
      </li>
    </ul>
  </div>
</section>

<section id="manifesto" data-section="manifesto" class="manifesto" data-kind="manifesto">
  <div class="mf-stage">
    <h2 class="mf-word fill"><span class="fit" data-echo="3" data-echo-inks style="--len:6">System</span></h2>
    <p class="mf-text">A system is not a library. Twelve weeks of naming, constraining and automating, until one set of tokens and a few good rules carry the whole product.</p>
  </div>
</section>

<section id="work" data-section="work" class="work" data-kind="gallery">
  <div class="wrap">
    <div class="sec-head">
      <h2 class="h2">Systems from last cohort</h2>
      <p class="lead">Everything here was built by people who had never written a design token a year before.</p>
    </div>
    <div class="w-wrap">
      <div class="w-grid" data-fixed="11">
        <figure class="w-it w-a" data-from="l"><svg class="art" data-art="wall" viewBox="0 0 600 600" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A wall of colourful component and token cards"></svg><figcaption>Ines Moura · Component architecture</figcaption></figure>
        <i class="w-it t q w-s1" data-from="d" aria-hidden="true" style="--tb:var(--amber);--tf:var(--ink);--r:1"><b></b></i>
        <figure class="w-it w-b" data-from="d"><svg class="art" data-art="poster" viewBox="0 0 300 600" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A specimen card for the colour token Blue 500"></svg><figcaption>Tomás Reis · Design tokens</figcaption></figure>
        <figure class="w-it w-c" data-from="r"><svg class="art" data-art="paper" viewBox="0 0 600 300" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Coloured surfaces stacked in layers to show elevation"></svg><figcaption>Lea Brandt · Elevation tokens</figcaption></figure>
        <i class="w-it t h w-s2" data-from="l" aria-hidden="true" style="--tb:var(--pink);--tf:var(--ink);--r:0"><b></b></i>
        <figure class="w-it w-d" data-from="u"><svg class="art" data-art="curves" viewBox="0 0 300 300" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Curved shapes showing a set of corner radii"></svg><figcaption>Rui Alves · Shape &amp; radius</figcaption></figure>
        <i class="w-it t ring w-s3" data-from="r" aria-hidden="true" style="--tb:var(--sky);--tf:var(--ink);--r:2"><b></b></i>
        <figure class="w-it w-e" data-from="l"><svg class="art" data-art="typecase" viewBox="0 0 900 300" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Rows of amber key-like chips, each holding a single character"></svg><figcaption>The glyph set</figcaption></figure>
        <figure class="w-it w-f" data-from="u"><svg class="art" data-art="roller" viewBox="0 0 300 300" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A roller applying a pink theme across a surface"></svg><figcaption>Theme night</figcaption></figure>
        <i class="w-it t q w-s4" data-from="d" aria-hidden="true" style="--tb:var(--ink);--tf:var(--amber);--r:3"><b></b></i>
        <i class="w-it t dot w-s5" data-from="r" aria-hidden="true" style="--tb:var(--pink);--tf:var(--ink)"><b></b></i>
      </div>
    </div>
  </div>
</section>

<section id="process" data-section="process" class="process" data-kind="steps">
  <div class="wrap pr-grid">
    <div class="pr-head">
      <h2 class="h2">From brief to production</h2>
      <p class="lead">Every course follows the same twelve weeks, whatever you are building. Reviews every Thursday, AI audits every Saturday.</p>
      <div class="actions"><a class="btn" href="#fees">See the fees</a></div>
    </div>
    <div class="pr-list" data-roll>
      <i class="pr-rail" aria-hidden="true"></i>
      <i class="pr-disc" aria-hidden="true"><i></i><i></i><i></i><i></i></i>
      <ol class="pr-steps">
      <li class="pr-step">
        <span class="pr-when">Weeks 1–2</span>
        <h3 class="h3">Audit</h3>
        <p>A real product or a real cause. You inventory every colour, font and button before you design anything.</p>
      </li>
      <li class="pr-step">
        <span class="pr-when">Weeks 3–5</span>
        <h3 class="h3">Tokens</h3>
        <p>Fifty names, pared down to a scale. We review them together and lock the foundations.</p>
      </li>
      <li class="pr-step">
        <span class="pr-when">Weeks 6–9</span>
        <h3 class="h3">Components &amp; AI</h3>
        <p>Components meet the tokens and models draft the variants. Weekly reviews keep them honest.</p>
      </li>
      <li class="pr-step">
        <span class="pr-when">Weeks 10–12</span>
        <h3 class="h3">Ship</h3>
        <p>Docs, code sync and a release to a live product. Then demo day, and a glass of something.</p>
      </li>
      </ol>
    </div>
  </div>
</section>

<section id="tutors" data-section="tutors" class="tutors" data-kind="team">
  <div class="wrap">
    <div class="sec-head">
      <h2 class="h2">Taught by working system designers</h2>
      <p class="lead">Everyone who teaches here still runs design systems at product companies, so you learn how it is done this year, not ten years ago.</p>
    </div>
    <ul class="tu-grid" data-print>
      <li class="tu">
        <figure class="tu-photo" style="--tb:var(--amber)"><svg class="art" data-art="marta" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Illustrated portrait of a smiling woman with dark curly hair in a white shirt"></svg></figure>
        <h3 class="h3">Marta Quintela</h3>
        <p class="tu-role">Design tokens</p>
      </li>
      <li class="tu">
        <figure class="tu-photo" style="--tb:var(--sky)"><svg class="art" data-art="jonas" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Illustrated portrait of a man in a suit and tie"></svg></figure>
        <h3 class="h3">Jonas Weber</h3>
        <p class="tu-role">Component architecture</p>
      </li>
      <li class="tu">
        <figure class="tu-photo" style="--tb:var(--pink)"><svg class="art" data-art="aiyana" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Illustrated portrait of a woman with long dark hair in a long-sleeved top"></svg></figure>
        <h3 class="h3">Aiyana Brooks</h3>
        <p class="tu-role">Docs &amp; governance</p>
      </li>
      <li class="tu">
        <figure class="tu-photo" style="--tb:var(--amber)"><svg class="art" data-art="karim" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="Illustrated portrait of a smiling bearded man in a white T-shirt"></svg></figure>
        <h3 class="h3">Karim Haddad</h3>
        <p class="tu-role">AI-assisted generation</p>
      </li>
    </ul>
  </div>
</section>

<section id="numbers" data-section="numbers" class="numbers" data-kind="results">
  <div class="wrap">
    <ul class="nu-top" data-turn-in>
      <li class="nu-card" style="--tb:var(--amber)"><span class="nu-fig" style="--len:2">12</span><p>people in a cohort, never more, so every review gets to your work</p></li>
      <li class="nu-card" style="--tb:var(--pink)"><span class="nu-fig" style="--len:4">900+</span><p>graduates since the first cohort in a borrowed meeting room</p></li>
      <li class="nu-card" style="--tb:var(--ink);--tx:var(--light)"><span class="nu-fig" style="--len:3">94%</span><p>would recommend a course to a friend, in our last survey</p></li>
    </ul>
    <div class="nu-chart">
      <h2 class="h2">Where graduates go next</h2>
      <ul class="bars" data-bars>
        <li class="bar"><span class="bar-track"><i class="bar-fill" style="--c:var(--ink)"></i></span><span class="bar-label">Design system teams</span><span class="bar-val">46%</span></li>
        <li class="bar"><span class="bar-track"><i class="bar-fill" style="--c:var(--amber)"></i></span><span class="bar-label">Product design roles</span><span class="bar-val">31%</span></li>
        <li class="bar"><span class="bar-track"><i class="bar-fill" style="--c:var(--sky)"></i></span><span class="bar-label">Design engineering</span><span class="bar-val">17%</span></li>
        <li class="bar"><span class="bar-track"><i class="bar-fill" style="--c:var(--pink)"></i></span><span class="bar-label">Further study</span><span class="bar-val">6%</span></li>
      </ul>
    </div>
  </div>
</section>

<section id="voices" data-section="voices" class="voices" data-kind="reviews">
  <div class="wrap">
    <div class="sec-head">
      <h2 class="h2">What students say</h2>
      <p class="lead">Product designers, front-end engineers, a former architect and plenty of people new to systems. Here are four of them.</p>
    </div>
    <ul class="vo-stack" data-stack>
      <li class="vo-card" style="--tb:var(--amber)">
        <blockquote><p>“I came for one evening course and left with a token library, a component set and a new job.”</p></blockquote>
        <p class="vo-who"><strong>Sofia Lemos</strong>Design tokens, spring 2026</p>
        <i class="vo-shape t q" aria-hidden="true" style="--tb:var(--amber);--tf:var(--ink);--r:2"><b></b></i>
      </li>
      <li class="vo-card" style="--tb:var(--pink)">
        <blockquote><p>“The Thursday reviews were terrifying for two weeks and then the best part of my week.”</p></blockquote>
        <p class="vo-who"><strong>Daniel Okafor</strong>Component architecture, autumn 2025</p>
        <i class="vo-shape t h" aria-hidden="true" style="--tb:var(--pink);--tf:var(--ink);--r:2"><b></b></i>
      </li>
      <li class="vo-card" style="--tb:var(--ink);--tx:var(--light)">
        <blockquote><p>“Ten years of shipping screens, and nobody had ever shown me what a token is for.”</p></blockquote>
        <p class="vo-who"><strong>Helena Sousa</strong>Docs &amp; governance, spring 2025</p>
        <i class="vo-shape t ring" aria-hidden="true" style="--tb:var(--ink);--tf:var(--amber);--r:2"><b></b></i>
      </li>
      <li class="vo-card" style="--tb:var(--light)">
        <blockquote><p>“Letting the AI draft made me faster. Reviewing every draft made me much, much better.”</p></blockquote>
        <p class="vo-who"><strong>Mateo Ruiz</strong>AI-assisted generation, 2026</p>
        <i class="vo-shape t dot" aria-hidden="true" style="--tb:var(--light);--tf:var(--pink)"><b></b></i>
      </li>
    </ul>
  </div>
</section>

<section id="fees" data-section="fees" class="fees" data-kind="pricing">
  <div class="wrap">
    <div class="sec-head">
      <h2 class="h2">Fees, plainly</h2>
      <p class="lead">No enrolment fee, all tool seats and AI credits included, and you can pay in three parts at no extra cost.</p>
    </div>
    <ul class="fe-grid" data-rise>
      <li class="fe-card">
        <i class="fe-head" aria-hidden="true" style="--tb:var(--sky);--tf:var(--ink)"><b></b></i>
        <h3 class="h3">One course</h3>
        <p class="fe-price"><span class="fe-num" style="--len:4">$480</span><span class="fe-per">per twelve-week term</span></p>
        <ul class="fe-list"><li>Two live sessions a week, or Saturdays</li><li>All tool seats and AI credits</li><li>A slot on demo day</li></ul>
        <a class="btn" href="#contact">Choose one</a>
      </li>
      <li class="fe-card is-main">
        <i class="fe-head q" aria-hidden="true" style="--tb:var(--amber);--tf:var(--pink)"><b></b></i>
        <h3 class="h3">Two courses</h3>
        <p class="fe-price"><span class="fe-num" style="--len:4">$860</span><span class="fe-per">per term, save $100</span></p>
        <ul class="fe-list"><li>Any two courses in one term</li><li>Open office hours on Fridays</li><li>One system review with a tutor</li></ul>
        <a class="btn" href="#contact">Choose two</a>
      </li>
      <li class="fe-card">
        <i class="fe-head o" aria-hidden="true" style="--tb:var(--pink);--tf:var(--ink)"><b></b></i>
        <h3 class="h3">Full year</h3>
        <p class="fe-price"><span class="fe-num" style="--len:6">$1,900</span><span class="fe-per">three terms, six courses</span></p>
        <ul class="fe-list"><li>The whole programme, in order</li><li>A team workspace of your own</li><li>A published design system at the end</li></ul>
        <a class="btn" href="#contact">Choose the year</a>
      </li>
    </ul>
  </div>
</section>

<section id="faq" data-section="faq" class="faq" data-kind="faq">
  <div class="wrap fq-grid">
    <div class="fq-head">
      <h2 class="h2">Good questions</h2>
      <p class="lead">Anything else, write to us and a tutor will answer within a day.</p>
      <div><a class="lnk" href="#contact">Ask a question</a></div>
    </div>
    <ul class="fq-list">
      <li class="fq-item" data-reveal>
        <button class="fq-q" type="button" aria-expanded="false"><span class="fq-ico icon-btn" aria-hidden="true"><i></i><i></i></span><span class="fq-text">Do I need any experience?</span></button>
        <div class="fq-a" hidden><p>No. Most people start with Design tokens or Component architecture with no systems background at all. Curiosity and a laptop are enough.</p></div>
      </li>
      <li class="fq-item" data-reveal>
        <button class="fq-q" type="button" aria-expanded="false"><span class="fq-ico icon-btn" aria-hidden="true"><i></i><i></i></span><span class="fq-text">Which software will I use?</span></button>
        <div class="fq-a" hidden><p>We work in Figma, a code editor and the academy's AI workspace. Seats are included, so you do not need your own licences.</p></div>
      </li>
      <li class="fq-item" data-reveal>
        <button class="fq-q" type="button" aria-expanded="false"><span class="fq-ico icon-btn" aria-hidden="true"><i></i><i></i></span><span class="fq-text">Can I pay in parts?</span></button>
        <div class="fq-a" hidden><p>Yes, in three equal parts across the term, at no extra cost. Just tell us when you apply.</p></div>
      </li>
      <li class="fq-item" data-reveal>
        <button class="fq-q" type="button" aria-expanded="false"><span class="fq-ico icon-btn" aria-hidden="true"><i></i><i></i></span><span class="fq-text">What if I miss a session?</span></button>
        <div class="fq-a" hidden><p>Every session is recorded with notes and examples, and a tutor runs a catch-up hour every Saturday morning.</p></div>
      </li>
      <li class="fq-item" data-reveal>
        <button class="fq-q" type="button" aria-expanded="false"><span class="fq-ico icon-btn" aria-hidden="true"><i></i><i></i></span><span class="fq-text">Do I get a certificate?</span></button>
        <div class="fq-a" hidden><p>You get one for each finished course, but the system you publish will say far more about you.</p></div>
      </li>
    </ul>
  </div>
</section>

<section id="contact" data-section="contact" class="contact" data-kind="contact">
  <div class="wrap">
    <h2 class="ct-word fill"><span class="fit" data-echo="2" style="--len:9">Say hello</span></h2>
    <div class="ct-grid">
      <div class="ct-info">
        <p class="lead">Join a free open session, watch a system being built live, and meet the tutors. Or just write to us.</p>
        <dl class="ct-list">
          <div><dt>Where</dt><dd>Live online, worldwide<br>Demo day in Lisbon</dd></div>
          <div><dt>Email</dt><dd><a class="lnk" href="mailto:hello@tokenhaus.example">hello@tokenhaus.example</a></dd></div>
          <div><dt>Next cohort</dt><dd>Starts 12 January 2027</dd></div>
          <div><dt>Office hours</dt><dd>Mon–Thu 17:00–22:00 WET<br>Sat 10:00–18:00</dd></div>
        </dl>
        <div class="actions"><a class="btn" href="mailto:hello@tokenhaus.example">Book an open session</a><a class="lnk" href="#faq">Read the FAQ</a></div>
      </div>
      <div class="ct-fig" aria-hidden="true" data-fixed="6">
        <i class="t q" data-turn="1" style="--tb:var(--sky);--tf:var(--light);--r:3"><b></b></i>
        <i class="t q" data-turn="-1" style="--tb:var(--sky);--tf:var(--light);--r:0"><b></b></i>
        <i class="t h" data-turn="2" style="--tb:var(--amber);--tf:var(--ink);--r:0"><b></b></i>
        <i class="t q" data-turn="-1" style="--tb:var(--pink);--tf:var(--ink);--r:1"><b></b></i>
        <i class="t ring" data-turn="1" style="--tb:var(--amber);--tf:var(--ink);--r:2"><b></b></i>
        <i class="t q" data-turn="2" style="--tb:var(--pink);--tf:var(--light);--r:2"><b></b></i>
      </div>
    </div>
  </div>
</section>

</main>

<footer class="foot" data-section="footer">
  <div class="wrap foot-grid">
    <a class="brand" href="#hero" aria-label="tokenhaus, back to top">
      <span class="mark" aria-hidden="true"><i class="t q" style="--tb:var(--paper);--tf:var(--amber);--r:3"><b></b></i><i class="t dot" style="--tb:var(--paper);--tf:var(--ink)"><b></b></i></span>
      <span>tokenhaus</span>
    </a>
    <p class="foot-addr">tokenhaus · AI Design System Academy<br>Live online, from Lisbon</p>
    <nav class="foot-nav" aria-label="Footer">
      <a class="lnk" href="#courses">Courses</a>
      <a class="lnk" href="#fees">Fees</a>
      <a class="lnk" href="#contact">Contact</a>
    </nav>
    <div class="foot-social">
      <a class="lnk" href="#">Instagram</a>
      <a class="lnk" href="#">Are.na</a>
      <a class="lnk" href="#">Newsletter</a>
    </div>
    <p class="foot-copy">© 2026 tokenhaus · a fictional brand; every figure is illustrative. Made with four tokens.</p>
  </div>
  <div class="inks" aria-hidden="true"><i style="--c:var(--amber)"></i><i style="--c:var(--pink)"></i><i style="--c:var(--sky)"></i><i style="--c:var(--ink)"></i></div>
</footer>

<script>
/* Coded artwork: every former photo is drawn here as SVG in the four-ink palette */
(function(){
  let seed=7;
  const rnd=()=>{seed=(seed*16807)%2147483647;return (seed-1)/2147483646;};
  const at=o=>Object.entries(o).map(([k,v])=>`${k}="${v}"`).join(' ');
  const R=(x,y,w,h,c,o={})=>`<rect ${at({x,y,width:w,height:h,class:c,...o})}/>`;
  const C=(cx,cy,r,c,o={})=>`<circle ${at({cx,cy,r,class:c,...o})}/>`;
  const E=(cx,cy,rx,ry,c,o={})=>`<ellipse ${at({cx,cy,rx,ry,class:c,...o})}/>`;
  const P=(d,c,o={})=>`<path ${at({d,class:c,...o})}/>`;
  const T=(x,y,s,c,txt,o={})=>`<text ${at({x,y,'font-size':s,class:c+' tx',...o})}>${txt}</text>`;
  const G=(inner,o={})=>`<g ${at(o)}>${inner}</g>`;
  const shadow=(id,dx,dy,sd,op)=>`<filter id="${id}" x="-30%" y="-30%" width="160%" height="170%"><feDropShadow dx="${dx}" dy="${dy}" stdDeviation="${sd}" flood-color="#212445" flood-opacity="${op}"/></filter>`;
  const halftone=(id,col,gap,r)=>`<pattern id="${id}" width="${gap}" height="${gap}" patternUnits="userSpaceOnUse" patternTransform="rotate(45)">${C(gap/2,gap/2,r,col)}</pattern>`;

  const arts={
    fan(){
      let s=`<defs>${shadow('fan-ds',2,5,5,.25)}</defs>`+R(0,0,500,400,'l');
      s+=R(18,18,464,364,'s',{rx:14,opacity:.14});
      for(let x=43;x<482;x+=25)s+=R(x,18,1,364,'s',{opacity:.3});
      for(let y=43;y<382;y+=25)s+=R(18,y,464,1,'s',{opacity:.3});
      const card=(x,y,r,c)=>G(R(0,0,70,92,'l',{rx:4,filter:'url(#fan-ds)'})+R(6,6,58,52,c,{rx:2})+R(6,66,34,5,'i',{opacity:.6})+R(6,76,22,4,'i',{opacity:.3}),{transform:`translate(${x} ${y}) rotate(${r})`});
      s+=card(392,232,-10,'p')+card(300,284,14,'s')+card(412,298,4,'i');
      const px=74,py=372,angs=[84,74,64,54,44,34,24,14],cols=['s','p','i','a','s','p','i','a'],tints=[1,.75,.52,.32,.16];
      angs.forEach((ang,k)=>{
        let g=R(px-26,py-318,52,330,'l',{rx:8,filter:'url(#fan-ds)'});
        tints.forEach((op,j)=>g+=R(px-20,py-310+j*50,40,44,cols[k],{rx:3,opacity:op}));
        g+=R(px-20,py-52,26,4,'i',{opacity:.55})+R(px-20,py-42,16,3,'i',{opacity:.3});
        s+=G(g,{transform:`rotate(${ang} ${px} ${py})`});
      });
      s+=C(px,py,10,'i')+C(px,py,4,'l');
      s+=G(R(0,0,104,140,'l',{rx:6,filter:'url(#fan-ds)'})+R(8,8,88,92,'a',{rx:3})+R(8,110,46,6,'i',{rx:3})+R(8,122,28,4,'i',{opacity:.45,rx:2}),{transform:'translate(352 36) rotate(12)'});
      return s;
    },
    wall(){
      let s=`<defs>${shadow('wall-ds',2,8,8,.3)}</defs>`+R(0,0,600,600,'g');
      const W=170,H=244,pos=[[22,26],[215,40],[408,22],[22,320],[215,334],[408,316]];
      const comps=[
        (x,y,w,h)=>R(x,y,w,h,'a')+C(x+w*.52,y+h*.42,w*.42,'i')+C(x+w*.7,y+h*.28,w*.14,'p')+R(x+14,y+h-46,w*.6,10,'i',{rx:5})+R(x+14,y+h-30,w*.35,7,'i',{rx:3.5}),
        (x,y,w,h)=>R(x,y,w,h,'i')+P(`M${x} ${y+h} L${x} ${y+h-w} A${w} ${w} 0 0 1 ${x+w} ${y+h} Z`,'s')+T(x+12,y+42,34,'l','TOKEN')+T(x+12,y+74,34,'a','SETS'),
        (x,y,w,h)=>{let g=R(x,y,w,h,'p');for(let i=0;i<5;i++)g+=R(x,y+20+i*22,w,9,'i');return g+P(`M${x+20} ${y+h} A${w/2-20} ${w/2-20} 0 0 1 ${x+w-20} ${y+h} Z`,'a');},
        (x,y,w,h)=>{let g=R(x,y,w,h,'l');const cs=['i','a','p','s'];for(let r=0;r<4;r++)for(let c=0;c<3;c++)g+=C(x+30+c*55,y+34+r*50,20,cs[(r+c)%4]);return g+T(x+14,y+h-14,13,'i','SPACE 04');},
        (x,y,w,h)=>R(x,y,w,h,'s')+R(x+14,y+20,w-28,14,'p',{rx:7})+C(x+w-32,y+66,16,'l')+T(x+8,y+h-18,120,'i','04'),
        (x,y,w,h)=>R(x,y,w,h,'i')+C(x+w/2,y+h,w*.55,'a')+C(x+w/2,y+h*.36,22,'l')+T(x+12,y+30,15,'p','DARK MODE')
      ];
      pos.forEach(([x,y],k)=>{
        s+=`<clipPath id="wall-c${k}">${R(x,y,W,H,'')}</clipPath>`;
        s+=R(x,y,W,H,'l',{filter:'url(#wall-ds)'});
        s+=G(comps[k](x,y,W,H),{'clip-path':`url(#wall-c${k})`});
        s+=R(x+W/2-22,y-8,44,16,'i',{opacity:.12,transform:`rotate(${k%2?4:-4} ${x+W/2} ${y})`});
      });
      return s;
    },
    poster(){
      let s=`<defs>${shadow('po-ds',3,10,9,.3)}<clipPath id="po-c">${R(40,70,220,460,'')}</clipPath></defs>`+R(0,0,300,600,'g');
      s+=R(40,70,220,460,'s',{filter:'url(#po-ds)'});
      let g=C(150,210,104,'l')+C(178,232,58,'i')+P('M260 70 L260 150 A80 80 0 0 1 180 70 Z','i');
      for(let k=0;k<4;k++)g+=R(40,346+k*16,220,7,'l',{opacity:.9});
      g+=T(56,452,50,'i','BLUE')+T(56,500,50,'l','500')+R(56,512,90,4,'i');
      s+=G(g,{'clip-path':'url(#po-c)'});
      s+=R(128,60,44,18,'i',{opacity:.12,transform:'rotate(-5 150 69)'});
      return s;
    },
    paper(){
      let s=`<defs>${shadow('pa-ds',4,8,7,.28)}</defs>`+R(0,0,600,300,'a');
      const sheets=[['i',300,190,290,160,-14],['s',290,180,310,150,-6],['p',280,175,296,156,4],['l',270,170,306,150,11],['g',240,150,300,152,-2]];
      sheets.forEach(([c,w,h,cx,cy,r],k)=>{
        let g=R(-w/2,-h/2,w,h,c,{filter:'url(#pa-ds)'});
        if(k===sheets.length-1)g+=C(-62,-14,30,'p')+R(-10,-34,86,10,'i',{rx:5})+R(-10,-16,56,8,'i',{opacity:.4,rx:4})+R(-10,24,96,4,'i',{opacity:.25,rx:2});
        s+=G(g,{transform:`translate(${cx} ${cy}) rotate(${r})`});
      });
      return s;
    },
    curves(){
      let s=`<defs>${shadow('cu-ds',3,6,6,.28)}</defs>`+R(0,0,300,300,'l');
      s+=P('M0 300 L0 60 A240 240 0 0 1 240 300 Z','p',{filter:'url(#cu-ds)'});
      s+=P('M130 0 A170 170 0 0 0 300 170 L300 90 A90 90 0 0 1 210 0 Z','s',{filter:'url(#cu-ds)'});
      s+=P('M90 300 A80 80 0 0 1 250 300 Z','a',{filter:'url(#cu-ds)'});
      s+=C(206,118,30,'i',{filter:'url(#cu-ds)'});
      return s;
    },
    typecase(){
      seed=11;
      let s=`<defs>${shadow('tc-ds',1,3,2.5,.45)}<linearGradient id="tc-v" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fdfefd" stop-opacity=".08"/><stop offset="1" stop-color="#212445" stop-opacity=".35"/></linearGradient></defs>`+R(0,0,900,300,'i');
      const cols=15,rows=4,cw=880/cols,ch=280/rows,L='MODULOTYPEGRIDPRINKASQ?!';
      for(let r=0;r<rows;r++)for(let c=0;c<cols;c++){
        const x=10+c*cw,y=10+r*ch;
        s+=R((x+2).toFixed(1),y+2,(cw-4).toFixed(1),ch-4,'l',{opacity:.06,rx:3});
        if(rnd()<.1)continue;
        const bx=(x+7),by=y+7,bw=cw-14,bh=ch-14,pale=rnd()<.12;
        s+=R(bx.toFixed(1),by,bw.toFixed(1),bh,pale?'l':'a',{rx:4,filter:'url(#tc-ds)'});
        if(!pale)s+=R(bx.toFixed(1),by,bw.toFixed(1),bh,'i',{rx:4,opacity:(rnd()*.26).toFixed(2)});
        s+=R((bx+3).toFixed(1),by+3,(bw-6).toFixed(1),3,'l',{opacity:.3,rx:1.5});
        const letter=L[Math.floor(rnd()*L.length)];
        s+=`<text class="i tx" font-size="36" text-anchor="middle" transform="translate(${(bx+bw/2).toFixed(1)} ${(by+bh/2+13).toFixed(1)})">${letter}</text>`;
      }
      return s+R(0,0,900,300,'',{fill:'url(#tc-v)'});
    },
    roller(){
      seed=5;
      let s=`<defs>${shadow('ro-ds',3,7,6,.3)}</defs>`+R(0,0,300,300,'l');
      for(let y=30;y<300;y+=22)s+=R(24,y,(120+rnd()*120).toFixed(0),4,'i',{opacity:.06,rx:2});
      let g=R(-60,146,250,96,'p',{rx:10});
      for(let k=0;k<10;k++)g+=R(-60,150+k*9,(180+rnd()*70).toFixed(0),2,'l',{opacity:(.15+rnd()*.25).toFixed(2)});
      g+=G(R(168,136,42,116,'i',{rx:20})+R(177,146,7,96,'l',{opacity:.3,rx:3.5}),{filter:'url(#ro-ds)'});
      g+=P('M189 136 Q240 136 240 194 Q240 252 189 252','st');
      g+=R(240,182,74,24,'a',{rx:12,filter:'url(#ro-ds)'})+R(240,184,14,20,'i',{rx:3});
      s+=G(g,{transform:'rotate(-18 150 150)'});
      s+=C(60,72,7,'p')+C(82,58,4,'p')+C(250,262,5,'i',{opacity:.6});
      return s;
    }
  };

  function portrait(o){
    const id=o.id;
    let s=`<defs>${halftone(id+'-ht','i',9,1.6)}</defs>`;
    s+=C(o.hx,o.hy,140,'',{fill:`url(#${id}-ht)`,opacity:.22});
    s+=P(o.q,'i',{opacity:.1});
    if(o.back)s+=P(o.back,'i');
    s+=P('M28 500 Q34 370 200 358 Q366 370 372 500 Z',o.top);
    s+=R(170,270,60,102,'l',{rx:24})+R(170,300,60,34,'i',{opacity:.1});
    s+=E(127,232,11,20,'l')+E(273,232,11,20,'l');
    s+=E(200,222,74,90,'l');
    s+=P('M200 132 A74 90 0 0 1 200 312 A40 90 0 0 0 200 132 Z','i',{opacity:.07});
    s+=C(162,266,13,'p',{opacity:.35})+C(238,266,13,'p',{opacity:.35});
    s+=E(172,228,6,7.5,'i')+E(228,228,6,7.5,'i')+R(158,206,26,5,'i',{rx:2.5})+R(216,206,26,5,'i',{rx:2.5});
    s+=P('M200 238 Q192 258 204 262','st2');
    s+=o.mouth||P('M180 284 Q200 300 220 284','st2');
    return s+(o.hair||'')+(o.extra||'');
  }
  const curls=()=>{let h='';for(let t=150;t<=390;t+=15){const r=t*Math.PI/180;h+=C((200+88*Math.cos(r)).toFixed(1),(214+100*Math.sin(r)).toFixed(1),t%30?30:36,'i');}for(let k=0;k<4;k++)h+=C(112-k*4,290+k*30,28,'i')+C(288+k*4,290+k*30,28,'i');return h;};

  arts.marta=()=>portrait({id:'pm',hx:320,hy:110,q:'M0 0 L160 0 A160 160 0 0 1 0 160 Z',top:'l',hair:curls(),
    extra:P('M162 360 L184 398 L200 374','st2')+P('M238 360 L216 398 L200 374','st2')+C(200,420,4,'i')+C(200,452,4,'i')});
  arts.jonas=()=>portrait({id:'pj',hx:80,hy:120,q:'M400 0 L400 160 A160 160 0 0 1 240 0 Z',top:'i',
    hair:P('M124 222 Q118 126 202 122 Q286 128 278 222 Q272 176 240 164 Q206 178 168 162 Q132 176 124 222 Z','i'),
    extra:P('M168 360 L200 446 L232 360 Z','l')+P('M193 370 L207 370 L213 440 L200 458 L187 440 Z','p')+P('M168 360 L198 446 L150 424 L136 376 Z','l',{opacity:.12})+P('M232 360 L202 446 L250 424 L264 376 Z','l',{opacity:.12})});
  arts.aiyana=()=>portrait({id:'pa',hx:320,hy:390,q:'M0 0 L160 0 A160 160 0 0 1 0 160 Z',top:'s',
    back:'M118 230 Q112 116 200 112 Q288 116 282 230 L298 420 Q200 446 102 420 Z',
    hair:P('M124 226 Q122 124 200 120 Q278 124 276 226 Q262 172 214 160 Q170 176 140 168 Q126 190 124 226 Z','i')+P('M126 210 Q116 300 132 380 L156 380 Q142 300 146 214 Z','i')+P('M274 210 Q284 300 268 380 L244 380 Q258 300 254 214 Z','i'),
    extra:P('M164 362 Q200 388 236 362 Z','l')});
  arts.karim=()=>portrait({id:'pk',hx:90,hy:400,q:'M400 0 L400 160 A160 160 0 0 1 240 0 Z',top:'l',
    hair:P('M128 206 Q126 124 200 122 Q274 124 272 206 Q264 160 200 156 Q136 160 128 206 Z','i')+P('M128 240 Q130 334 200 338 Q270 334 272 240 Q262 300 200 306 Q138 300 128 240 Z','i')+P('M174 274 Q200 262 226 274 Q200 270 174 274 Z','i'),
    mouth:P('M174 278 Q200 308 226 278 Z','i')+P('M180 280 L220 280 Q216 288 200 290 Q184 288 180 280 Z','l'),
    extra:P('M166 362 Q200 392 234 362 Z','l')+P('M166 362 Q200 392 234 362','st2')});

  document.querySelectorAll('svg[data-art]').forEach(el=>{const f=arts[el.dataset.art];if(!f)return;try{el.innerHTML=f()}catch(e){console.error(e)}});
})();
</script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js" defer></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js" defer></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js" defer></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js" defer></script>
<script>document.addEventListener('DOMContentLoaded',()=>{const init=(sel,fn)=>document.querySelectorAll(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});const root=document.documentElement;init('[data-head]',head=>{let last=scrollY,up=0;addEventListener('scroll',()=>{const y=scrollY,d=y-last;last=y;if(head.classList.contains('menu-open')||y<120){head.classList.remove('is-hidden');up=0;return}if(d>0){up=0;head.classList.add('is-hidden')}else if(d<0){up-=d;if(up>8)head.classList.remove('is-hidden')}},{passive:true});const btn=head.querySelector('.menu-btn'),menu=head.querySelector('.menu');if(!btn||!menu)return;const set=open=>{btn.setAttribute('aria-expanded',open);menu.hidden=!open;head.classList.toggle('menu-open',open);btn.setAttribute('aria-label',open?btn.dataset.labelClose||'':btn.dataset.labelOpen||'')};btn.addEventListener('click',()=>set(btn.getAttribute('aria-expanded')!=='true'));menu.addEventListener('click',e=>{if(e.target.closest('a'))set(false)});addEventListener('keydown',e=>{if(e.key==='Escape')set(false)})});init('[data-echo]',el=>{const n=Math.max(0,parseInt(el.dataset.echo,10)||0),text=el.textContent;el.style.setProperty('--n',n);for(let i=1;i<=n;i++){const c=document.createElement('span');c.className='echo-copy';c.setAttribute('aria-hidden','true');c.textContent=text;c.style.zIndex=-i;c.style.transform='translateY(calc('+i+' * var(--eg, .34em)))';if(el.hasAttribute('data-echo-inks'))c.dataset.ink=i;el.append(c)}});const stick=()=>document.querySelectorAll('.hero').forEach(h=>h.style.setProperty('--stick',Math.min(0,innerHeight-h.offsetHeight)+'px'));stick();addEventListener('resize',stick);const accordion=(sel,btnSel,bodySel)=>init(sel,item=>{const row=item.querySelector(btnSel),body=item.querySelector(bodySel);if(!row||!body)return;row.addEventListener('click',()=>{const open=row.getAttribute('aria-expanded')!=='true';row.setAttribute('aria-expanded',open);body.hidden=!open;item.classList.toggle('is-open',open);if(window.ScrollTrigger)ScrollTrigger.refresh()})});accordion('.c-item','.c-row','.c-body');accordion('.fq-item','.fq-q','.fq-a');init('[data-bars]',list=>{const bars=[...list.querySelectorAll('.bar')].map(b=>({b,t:(b.querySelector('.bar-val')||{}).textContent||''}));const max=Math.max(1,...bars.map(x=>parseFloat(x.t.replace(/[^\d.]/g,''))||0));bars.forEach(({b,t})=>{const v=parseFloat(t.replace(/[^\d.]/g,'')),f=b.querySelector('.bar-fill');if(f&&!isNaN(v))f.style.setProperty('--v',Math.min(100,t.includes('%')?v:v/max*100))})});if(!root.classList.contains('motion')||!window.gsap||!window.ScrollTrigger)return;gsap.registerPlugin(ScrollTrigger);if(window.SplitText)gsap.registerPlugin(SplitText);const desktop=matchMedia('(min-width: 1024px) and (hover: hover)');let lenis=null;if(window.Lenis){lenis=new Lenis({lerp:.11});lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0)}document.addEventListener('click',e=>{const a=e.target.closest('a[href^="#"]');if(!a||!lenis)return;const id=a.getAttribute('href');if(id.length<2)return;const t=document.querySelector(id);if(!t)return;e.preventDefault();lenis.scrollTo(t,{duration:1.4})});const reveals=gsap.utils.toArray('[data-reveal]');if(reveals.length){gsap.set(reveals,{y:44});ScrollTrigger.batch(reveals,{start:'top 90%',once:true,onEnter:b=>gsap.to(b,{opacity:1,y:0,duration:.9,ease:'power3.out',stagger:.09,clearProps:'transform'})})}init('[data-reveal-corner]',fig=>{const img=fig.querySelector('img,.art');gsap.fromTo(fig,{clipPath:'circle(0% at 0% 100%)'},{clipPath:'circle(142% at 0% 100%)',ease:'none',scrollTrigger:{trigger:fig,start:'top 92%',end:'top 30%',scrub:.6}});if(img)gsap.fromTo(img,{yPercent:-6,scale:1.14},{yPercent:6,scale:1.14,ease:'none',scrollTrigger:{trigger:fig,start:'top bottom',end:'bottom top',scrub:true}})});if(window.SplitText)init('[data-split]',el=>{SplitText.create(el,{type:'lines',mask:'lines',autoSplit:true,onSplit:self=>gsap.from(self.lines,{yPercent:105,ease:'none',stagger:.12,scrollTrigger:{trigger:el,start:'top 85%',end:'bottom 55%',scrub:.6}})})});init('[data-turn]:not(.fig [data-turn])',t=>{const b=t.querySelector('b');if(!b)return;gsap.fromTo(b,{rotation:-90*(+t.dataset.turn||1)},{rotation:0,duration:1.1,ease:'back.out(1.6)',scrollTrigger:{trigger:t,start:'top 88%',toggleActions:'play none none reverse'}})});init('.hero',sec=>{const next=sec.nextElementSibling;const tiles=sec.querySelectorAll('.fig [data-turn] > b');const pills=sec.querySelectorAll('.pills i');const copies=sec.querySelectorAll('.echo-copy');const loops=[];pills.forEach((p,i)=>loops.push(gsap.fromTo(p,{xPercent:i%2?16:0},{xPercent:i%2?0:16,duration:3.4+i*.5,ease:'sine.inOut',yoyo:true,repeat:-1,delay:i*.6})));copies.forEach((c,i)=>loops.push(gsap.to(c,{yPercent:9*(i+1),duration:2.6,ease:'sine.inOut',yoyo:true,repeat:-1,delay:.4*i})));if(!next)return;gsap.set(pills,{clipPath:(i,el)=>`inset(0 0px 0 0 round ${el.offsetHeight}px)`});const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:next,start:'top bottom',end:'top 50%',scrub:.8,invalidateOnRefresh:true}});tiles.forEach((b,i)=>tl.to(b,{rotation:(+b.parentElement.dataset.turn||0)*90,duration:.55,ease:'power2.inOut'},i*.05));tl.to(pills,{clipPath:(i,el)=>`inset(0 ${el.offsetWidth-el.offsetHeight}px 0 0 round ${el.offsetHeight}px)`,stagger:.07,duration:.45},.15).to(copies,{y:(i,el)=>el.offsetHeight*.22*(i+1),duration:.6},.1);gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:next,start:'top bottom',end:'top top',scrub:.5,onToggle:s=>loops.forEach(l=>s.isActive||s.progress<1?l.play():l.pause())}}).to(sec.querySelector('.h1-big'),{xPercent:-6,duration:1},0).to(sec.querySelector('.shade'),{opacity:.6,duration:.6},.4)});init('.courses [data-grow]',list=>{const rows=list.querySelectorAll('.c-row');if(!rows.length)return;gsap.fromTo(rows,{clipPath:(i,el)=>`inset(0 ${el.offsetWidth-el.offsetHeight}px 0 0 round ${el.offsetHeight/2}px)`},{clipPath:(i,el)=>`inset(0 0px 0 0 round ${el.offsetHeight/2}px)`,ease:'power1.inOut',stagger:.15,scrollTrigger:{trigger:list,start:'top 82%',end:'bottom 70%',scrub:.6,invalidateOnRefresh:true}})});init('.manifesto',sec=>{const copies=sec.querySelectorAll('.echo-copy'),text=sec.querySelector('.mf-text');if(!copies.length)return;const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top top',end:'bottom bottom',scrub:.8,invalidateOnRefresh:true}});gsap.set(copies,{y:0});tl.fromTo(copies,{yPercent:0},{yPercent:i=>(i+1)*(innerWidth<900?125:58),xPercent:i=>i%2?-1.2:1.2,duration:.45,ease:'power2.out',stagger:.08},0).to(copies,{yPercent:i=>(i+1)*20,xPercent:0,duration:.35,ease:'power2.inOut',stagger:{each:.05,from:'end'}},.72);if(text)tl.fromTo(text,{opacity:0,y:40},{opacity:1,y:0,duration:.25},.82)});init('.w-grid',grid=>{const items=grid.querySelectorAll('.w-it');if(!items.length)return;const dir={l:[-1,0],r:[1,0],u:[0,-1],d:[0,1]};const tl=gsap.timeline({defaults:{ease:'power2.out',duration:.6},scrollTrigger:{trigger:grid,start:'top 88%',end:'center 52%',scrub:.9}});items.forEach((it,i)=>{const[x,y]=dir[it.dataset.from]||dir.d,at=i*.06;tl.from(it,{xPercent:x*100,yPercent:y*100,autoAlpha:0,ease:'power3.out'},at);const img=it.querySelector('img,.art'),b=it.querySelector(':scope > b');if(img)tl.from(img,{scale:1.35},at);if(b)tl.from(b,{rotation:(x||y)*180},at)})});init('[data-roll]',list=>{const disc=list.querySelector('.pr-disc'),steps=list.querySelectorAll('.pr-step');steps.forEach(s=>ScrollTrigger.create({trigger:s,start:'top 62%',onEnter:()=>s.classList.add('is-on'),onLeaveBack:()=>s.classList.remove('is-on')}));if(!disc)return;const run=()=>Math.max(0,list.offsetHeight-disc.offsetHeight);gsap.to(disc,{y:run,rotation:()=>run()/(disc.offsetWidth/2)*57.3,ease:'none',scrollTrigger:{trigger:list,start:'top 62%',end:()=>'+='+run(),scrub:.4,invalidateOnRefresh:true}})});init('[data-print]',grid=>{const photos=grid.querySelectorAll('.tu-photo');if(!photos.length)return;gsap.set(photos,{clipPath:'inset(0% 100% 0% 0%)'});gsap.set(grid.querySelectorAll('.tu-photo img,.tu-photo .art'),{clipPath:'inset(0% 0% 100% 0%)',x:14});ScrollTrigger.batch(photos,{start:'top 86%',once:true,onEnter:batch=>batch.forEach((p,i)=>{const img=p.querySelector('img,.art');const tl=gsap.timeline({delay:i*.14}).to(p,{clipPath:'inset(0% 0% 0% 0%)',duration:.7,ease:'power3.inOut'});if(img)tl.to(img,{clipPath:'inset(0% 0% 0% 0%)',duration:.8,ease:'power3.inOut'},.45).to(img,{x:0,duration:.6,ease:'back.out(2)'},1.05)})})});init('[data-turn-in]',row=>{const cards=row.children;if(!cards.length)return;gsap.from(cards,{rotation:-90,transformOrigin:'0% 100%',duration:1.2,ease:'power3.out',stagger:.14,scrollTrigger:{trigger:row,start:'top 78%',toggleActions:'play none none reverse'}})});init('[data-bars]',list=>{const fills=list.querySelectorAll('.bar-fill');if(!fills.length)return;gsap.from(fills,{clipPath:'inset(0% 100% 0% 0% round 999px)',duration:1.2,ease:'power3.inOut',stagger:.12,scrollTrigger:{trigger:list,start:'top 80%',toggleActions:'play none none reverse'}})});init('[data-stack]',stack=>{const cards=[...stack.querySelectorAll('.vo-card')];const top=()=>parseFloat(getComputedStyle(root).getPropertyValue('--hh'))+20;cards.forEach((c,i)=>{const n=cards[i+1];if(!n)return;gsap.to(c,{scale:.92,rotation:i%2?1.6:-1.6,ease:'none',scrollTrigger:{trigger:n,start:'top bottom',end:()=>'top '+top(),scrub:.4,invalidateOnRefresh:true}})})});init('[data-rise]',grid=>{const cards=grid.children;if(!cards.length)return;const tl=gsap.timeline({scrollTrigger:{trigger:grid,start:'top 80%',toggleActions:'play none none reverse'}});tl.from(cards,{clipPath:'inset(100% 0% 0% 0%)',y:70,duration:1,ease:'power3.out',stagger:.12}).from(grid.querySelectorAll('.fe-head b'),{yPercent:100,duration:.8,ease:'back.out(1.4)',stagger:.12},.35)});init('.foot .inks',inks=>gsap.from(inks.children,{scaleY:0,duration:.9,ease:'power3.out',stagger:.08,scrollTrigger:{trigger:inks,start:'top bottom',toggleActions:'play none none reverse'}}))});</script>
</body>
</html>
```

