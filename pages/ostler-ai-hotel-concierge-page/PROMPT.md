INSTALANDING.AI · Ostler AI Hotel Concierge Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Ostler AI Hotel Concierge Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/ostler-ai-hotel-concierge-page

ostler-hotel-concierge.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Ostler AI Hotel Concierge Page
  slug     ostler-ai-hotel-concierge-page
  prompt   https://instalanding.ai/p/ostler-ai-hotel-concierge-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/ostler-ai-hotel-concierge-page
  license  Fictional brand ("Ostler", Bristol); every hotel, figure, price, person and quote is invented.
           Replace names, numbers and copy before shipping. Every picture is inline SVG; no image files.

  MAP
  tokens    one :root block at the top of the <style>: ink --ink, red --red / --red-deep, cream --cream, olive --olive,
            Gabarito (--font-display, 900, tight) and Instrument Sans (--font-text), radii --r / --r-s, spacing --gap /
            --pad, --head, the corner square --mark, --k (the fill-to-width ratio) and the --spring / --out easings.
  sections  nav, hero, ticker, logos, story, modules, pricing, statement, process, changelog, voices, gallery, faq,
            contact, footer (each region carries data-section)
  scripts   0. (head) adds .motion unless prefers-reduced-motion, and takes it away again if GSAP never arrives
            1. UI that works without motion: the scroll progress bar, the menu, smooth anchor links, the local-only
               demo form that thanks inline
            2. (motion only) GSAP 3.13 + ScrollTrigger + SplitText and Lenis 1.3.4 (jsdelivr): the hero card tilting
               and shrinking while "Ostler" springs apart letter by letter and flies off, the pinned sideways module
               rail with tilting covers, the "Awake" knockout word zooming 9x into the hotel at night, sticky process
               cards that scale and tilt away, words and tags that bounce in, changelog rows wiping in, the quote
               marquee, the gallery prints drifting at different speeds
  assets    no image files; the phone, lock screen, dashboards, rooms and hotel facades are inline SVG

  ADAPTING
  - Fill-to-width words (.fill) size themselves from --len (letter count) times --k; change --len with the word.
  - Card colours come from .on-red / .on-cream / .on-olive; covers from .cover--red / --olive / --cream.
  - data-reveal="up|tag|wipe|drop", data-split, data-bounce and data-speed are the motion hooks.
  - prefers-reduced-motion: no pinning, scrubbing, grain or ticker; the rail becomes a grid.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#100c0d">
<title>Ostler — the AI concierge for independent hotels</title>
<meta name="description" content="Ostler answers guest messages in 41 languages, sells the extras and hands the tricky ones to your team. Live in independent hotels in fourteen days.">
<script>(()=>{const d=document.documentElement;if(matchMedia('(prefers-reduced-motion: reduce)').matches)return;d.classList.add('motion');setTimeout(()=>{if(!window.gsap)d.classList.remove('motion')},2500)})();</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Gabarito:wght@500..900&family=Instrument+Sans:ital,wght@0,400..700;1,400..700&display=swap">
<style>
:root{--ink:#100c0d;--red:#a72d2d;--red-deep:#7a2222;--cream:#e2dcce;--olive:#5b6a45;--font-display:"Gabarito", system-ui, sans-serif;--font-text:"Instrument Sans", system-ui, sans-serif;--muted:color-mix(in oklab, currentColor 72%, transparent);--line:color-mix(in oklab, currentColor 26%, transparent);--gap:clamp(10px, 1.4vw, 20px);--pad:clamp(22px, 4.4vw, 72px);--r:clamp(20px, 2.3vw, 34px);--r-s:clamp(12px, 1.2vw, 18px);--mark:clamp(7px, .65vw, 10px);--head:68px;--k:.52;--spring:cubic-bezier(.34, 1.56, .5, 1);--out:cubic-bezier(.2, .8, .2, 1);}
*,*::before,*::after{box-sizing:border-box}
html{-webkit-text-size-adjust:100%;scroll-padding-top:var(--head)}
body{margin:0;background:var(--ink);color:var(--cream);font:400 17px/1.55 var(--font-text);-webkit-font-smoothing:antialiased;text-rendering:optimizeLegibility}
::selection{background:var(--red);color:var(--cream)}
body::after{content:"";position:fixed;inset:-60px;z-index:90;pointer-events:none;opacity:.06;background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='240' height='240'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 1.4 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E")}
.motion body::after{animation:grain 1.2s steps(6) infinite}
@keyframes grain{0%{transform:translate(0,0)}20%{transform:translate(-22px,14px)}40%{transform:translate(16px,-24px)}60%{transform:translate(-12px,30px)}80%{transform:translate(26px,8px)}100%{transform:translate(0,0)}}
.sprite{position:absolute;width:0;height:0;overflow:hidden}
.art{display:block;width:100%;height:100%;transform-origin:50% 50%}
.art text{font-family:"Instrument Sans",system-ui,sans-serif}
.art .d{font-family:"Gabarito",system-ui,sans-serif}
a{color:inherit}
h1,h2,h3,h4,p,ul,ol,dl,dd,figure,blockquote{margin:0}
ul,ol{padding:0;list-style:none}
button,input,textarea{font:inherit;color:inherit}
:focus-visible{outline:2px solid currentColor;outline-offset:3px}
main>*{position:relative;overflow-x:clip}
main>*+*{margin-top:var(--gap)}
.progress{position:fixed;left:0;top:0;z-index:60;width:100%;height:3px;background:var(--red);transform-origin:0 50%;transform:scaleX(0);pointer-events:none}
.card{position:relative;margin:0 var(--gap);border-radius:var(--r);padding:var(--pad)}
.on-red{background:var(--red);color:var(--cream)}
.on-cream{background:var(--cream);color:var(--ink)}
.on-olive{background:var(--olive);color:var(--cream)}
.marks::before,.marks::after{content:"";position:absolute;width:var(--mark);height:var(--mark);background:currentColor;z-index:4;pointer-events:none}
.marks::before{top:calc(var(--pad) * .42);right:calc(var(--pad) * .42)}
.marks::after{bottom:calc(var(--pad) * .42);left:calc(var(--pad) * .42)}
.display{font-family:var(--font-display);font-weight:900;line-height:.8;letter-spacing:-.045em}
.fillbox{container-type:inline-size}
.fill{display:block;white-space:nowrap;font-size:calc(100cqi / (var(--len) * var(--k)))}
.h2{font-family:var(--font-display);font-weight:800;font-size:clamp(40px, 6vw, 96px);line-height:.9;letter-spacing:-.035em;text-wrap:balance}
.h3{font-family:var(--font-display);font-weight:800;font-size:clamp(24px, 2.3vw, 34px);line-height:1;letter-spacing:-.02em}
.lead{font-size:clamp(18px, 1.5vw, 21px);line-height:1.45;font-weight:500}
.muted{color:var(--muted)}
.eyebrow{font:600 13px/1 var(--font-text);letter-spacing:.14em;text-transform:uppercase;opacity:.75}
.btn{display:inline-flex;align-items:center;gap:.85em;white-space:nowrap;padding:.8em 1.2em .8em 1.45em;border:1.5px solid currentColor;border-radius:999px;font:500 15px/1 var(--font-text);text-decoration:none;color:inherit;position:relative;isolation:isolate;overflow:hidden;background:none;cursor:pointer;transition:transform .5s var(--spring),color .35s}
.btn::before{content:"";position:absolute;inset:-1px;z-index:-1;background:var(--btn-fill, var(--cream));clip-path:circle(0% at 88% 50%);transition:clip-path .55s var(--out)}
.btn__arrow{width:28px;height:12px;flex:none;transition:transform .45s var(--spring)}
.btn--solid{background:var(--cream);color:var(--ink);border-color:var(--cream);--btn-fill:var(--red);--btn-on:var(--cream)}
.on-cream .btn{--btn-fill:var(--ink);--btn-on:var(--cream)}
.on-cream .btn--solid{background:var(--ink);color:var(--cream);border-color:var(--ink);--btn-fill:var(--red)}
.btn:focus-visible{color:var(--btn-on, var(--ink))}
.btn:focus-visible::before{clip-path:circle(150% at 88% 50%)}
@media (hover:hover){.btn:hover{transform:rotate(-3deg);color:var(--btn-on, var(--ink))}.btn:hover::before{clip-path:circle(150% at 88% 50%)}.btn:hover .btn__arrow{transform:translateX(5px)}}
.link{text-decoration:underline;text-decoration-thickness:1.5px;text-underline-offset:.24em;text-decoration-color:var(--line);transition:text-decoration-color .3s}
@media (hover:hover){.link:hover{text-decoration-style:wavy;text-decoration-color:currentColor;text-decoration-thickness:1.5px}}
.link:focus-visible{text-decoration-style:wavy;text-decoration-color:currentColor}
.icon-btn{width:44px;height:44px;flex:none;display:inline-grid;place-items:center;border-radius:50%;border:1.5px solid currentColor;background:none;color:inherit;cursor:pointer;padding:0}
@keyframes wobble{0%{transform:rotate(0)}30%{transform:rotate(-14deg)}60%{transform:rotate(9deg)}100%{transform:rotate(0)}}
@media (hover:hover){.icon-btn:hover{animation:wobble .6s var(--spring)}}
.print{position:relative;overflow:hidden;background:var(--field, var(--red));isolation:isolate}
.print--olive{--field:var(--olive)}.print--cream{--field:var(--cream)}
.hdr{position:fixed;inset:0 0 auto;z-index:50;height:var(--head);padding:10px var(--gap) 0;pointer-events:none}
.hdr__bar{pointer-events:auto;height:100%;display:flex;align-items:center;gap:18px;padding:0 6px 0 clamp(14px, 1.6vw, 22px);border-radius:999px;background:color-mix(in oklab, var(--ink) 86%, transparent);-webkit-backdrop-filter:blur(14px) saturate(1.4);backdrop-filter:blur(14px) saturate(1.4);color:var(--cream);box-shadow:inset 0 0 0 1px color-mix(in oklab, var(--cream) 10%, transparent),0 10px 30px -12px rgba(0,0,0,.6)}
.hdr__brand{font-family:var(--font-display);font-weight:900;font-size:27px;letter-spacing:-.04em;text-decoration:none;margin-right:auto;white-space:nowrap;display:inline-flex;align-items:center;gap:10px}
.hdr__brand i{width:9px;height:9px;background:var(--red);border-radius:2px;transform:rotate(45deg)}
.hdr__nav{display:flex;gap:clamp(14px, 2vw, 30px);font-size:15px;font-weight:500}
.hdr__nav a{white-space:nowrap}
.hdr__cta{padding:.72em 1.05em .72em 1.3em}
.hdr__menu{display:none;border-color:var(--line)}
.hdr__menu span{display:block;width:16px;height:1.5px;background:currentColor;transition:transform .4s var(--spring);grid-area:1/1}
.hdr__menu span:first-child{transform:translateY(-3px)}
.hdr__menu span:last-child{transform:translateY(3px)}
.hdr.is-open .hdr__menu span:first-child{transform:rotate(45deg)}
.hdr.is-open .hdr__menu span:last-child{transform:rotate(-45deg)}
@media (max-width:900px){.hdr__menu{display:inline-grid}.hdr__cta{display:none}.hdr__nav{position:fixed;top:calc(var(--head) + 6px);left:var(--gap);right:var(--gap);flex-direction:column;gap:4px;padding:22px 24px 26px;border-radius:var(--r);background:var(--cream);color:var(--ink);font:800 clamp(30px, 8vw, 44px)/1.1 var(--font-display);letter-spacing:-.03em;opacity:0;visibility:hidden;transform:translateY(-10px) rotate(-1.5deg);transition:opacity .3s,transform .5s var(--spring),visibility 0s .3s}.hdr.is-open .hdr__nav{opacity:1;visibility:visible;transform:none;transition:opacity .3s,transform .5s var(--spring)}.hdr__nav a{text-decoration:none;white-space:normal}}
.hero{padding-top:var(--head)}
.hero>*{margin-top:var(--gap)}
.hero__card{position:relative;container-type:inline-size;margin-left:var(--gap);margin-right:var(--gap);height:calc(100svh - var(--head) - 2 * var(--gap));min-height:620px;border-radius:var(--r);color:var(--cream);display:grid;grid-template-columns:minmax(0, 1fr);align-content:end;justify-items:start;gap:26px;padding:var(--pad);transform-origin:50% 100%}
.hero__photo{position:absolute;inset:0;border-radius:inherit;overflow:hidden;background:#2a0d0f}
.hero__photo::after{content:"";position:absolute;inset:0;background:linear-gradient(to top, color-mix(in oklab, #1d0a0b 92%, transparent) 0%, color-mix(in oklab, #1d0a0b 40%, transparent) 36%, transparent 60%)}
.hero__wordclip{position:absolute;left:0;right:0;top:0;z-index:2;container-type:inline-size;clip-path:inset(0 -30% -200% -30%);pointer-events:none}
.hero__word{text-align:center;color:var(--cream);margin:-.075em auto 0;width:92cqi;font-size:min(calc(92cqi / (var(--len) * var(--k))), 36svh);white-space:nowrap;line-height:.8;mix-blend-mode:normal}
.hero__info{position:relative;z-index:3;width:min(560px, 44cqi);display:grid;gap:14px}
.hero__device{position:absolute;inset:0;z-index:1;overflow:hidden;border-radius:inherit;pointer-events:none}
.hero__phone{position:absolute;right:12.5cqi;top:min(20.5cqi, 29svh);width:min(40cqi, 600px);height:auto;overflow:visible}
.hero__title{font-family:var(--font-display);font-weight:800;font-size:clamp(28px, 3vw, 44px);line-height:.98;letter-spacing:-.025em;text-wrap:balance}
.hero__lead{font-size:16px;line-height:1.45;font-weight:500;max-width:44ch;color:color-mix(in oklab, var(--cream) 90%, transparent)}
.hero__addr{font-size:14px;line-height:1.4;margin-top:10px;color:color-mix(in oklab, var(--cream) 82%, transparent)}
.hero__side{position:relative;z-index:3;display:flex;flex-wrap:wrap;align-items:center;gap:12px 22px}
.hero__side .btn{order:-1}
.hero__hours{font-size:14px;font-weight:500;display:inline-flex;align-items:center;gap:8px}
.hero__hours i{width:8px;height:8px;border-radius:50%;background:#9fd18b;box-shadow:0 0 0 0 rgba(159,209,139,.7);animation:pulse 2.2s infinite}
@keyframes pulse{70%{box-shadow:0 0 0 9px rgba(159,209,139,0)}100%{box-shadow:0 0 0 0 rgba(159,209,139,0)}}
.hero__logo{width:34px;height:34px;display:grid;place-items:center;background:var(--cream);color:var(--ink);border-radius:5px;font:900 20px/1 var(--font-display);letter-spacing:-.05em}
.motion .hero{height:calc(max(100svh, 600px + var(--head) + 2 * var(--gap)) + 75svh)}
.motion .hero__card{position:sticky;top:calc(var(--head) + var(--gap))}
@media (max-width:900px){.hero__card{display:flex;flex-direction:column;justify-content:flex-end;align-items:stretch;gap:20px;height:auto;min-height:calc(100svh - var(--head) - 2 * var(--gap))}.hero__info{width:auto;max-width:560px}.hero__device{position:relative;inset:auto;flex:1 0 auto;min-height:clamp(230px, 40svh, 440px);margin:calc(19cqi - var(--pad)) calc(-1 * var(--pad)) 0;border-radius:0;-webkit-mask-image:linear-gradient(to bottom,#000 72%,transparent);mask-image:linear-gradient(to bottom,#000 72%,transparent)}.hero__phone{right:auto;left:50%;top:0;width:min(104cqi, 620px);transform:translateX(-50%)}.hero__phone .hd-card{display:none}}
@media (min-width:901px) and (max-height:780px){.hero__phone{width:min(36cqi, 520px)}.hero__phone .hd-low,.hero__addr{display:none}}
.ticker{overflow:hidden;padding:clamp(14px,1.6vw,22px) 0;border-block:1.5px solid color-mix(in oklab, var(--cream) 14%, transparent)}
.ticker__track{display:flex;width:max-content;animation:tick 52s linear infinite}
.ticker span{display:inline-flex;align-items:center;white-space:nowrap;font:800 clamp(26px,3.4vw,52px)/1 var(--font-display);letter-spacing:-.03em}
.ticker span em{font-style:normal;color:transparent;-webkit-text-stroke:1.2px var(--cream)}
.ticker i{display:inline-block;width:.38em;height:.38em;background:var(--red);border-radius:2px;transform:rotate(45deg);margin:0 .7em}
@keyframes tick{to{transform:translateX(-50%)}}
@media (prefers-reduced-motion:reduce){.ticker__track{animation:none}}
.logos{display:flex;flex-wrap:wrap;justify-content:center;align-items:center;gap:14px clamp(28px,4vw,64px);padding:clamp(26px,3vw,40px) var(--pad);color:color-mix(in oklab, var(--cream) 62%, transparent)}
.logos p{width:100%;text-align:center;font-size:13px;letter-spacing:.14em;text-transform:uppercase;font-weight:600;margin-bottom:6px}
.logos span{font-family:var(--font-display);font-weight:700;font-size:clamp(18px,1.7vw,24px);letter-spacing:-.01em;white-space:nowrap}
.logos span:nth-of-type(2n){font-family:Georgia, "Times New Roman", serif;font-style:italic;font-weight:400;letter-spacing:0}
.logos span:nth-of-type(3n){letter-spacing:.22em;text-transform:uppercase;font-size:clamp(13px,1.1vw,16px);font-weight:600}
.story__card{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:clamp(28px, 4vw, 64px) clamp(16px, 2vw, 32px)}
.story__title{grid-column:1/-1;max-width:18ch}
.story__photo{grid-column:1/span 4;align-self:start;border-radius:var(--r-s);transform:rotate(-3deg);aspect-ratio:4/5;box-shadow:0 30px 60px -30px rgba(16,12,13,.55)}
.story__body{grid-column:6/-1;display:grid;gap:clamp(28px, 3vw, 48px);align-content:start}
.story__text{max-width:52ch}
.facts{display:grid;grid-template-columns:repeat(auto-fit, minmax(170px, 1fr));gap:24px 28px;border-top:1.5px solid var(--line);padding-top:26px}
.facts strong{display:block;font-family:var(--font-display);font-weight:900;font-size:clamp(44px, 4.6vw, 76px);line-height:.9;letter-spacing:-.045em;color:var(--red)}
.facts span{display:block;margin-top:8px;font-size:15px;line-height:1.35}
@media (max-width:800px){.story__photo{grid-column:1/span 9}.story__body{grid-column:1/-1}}
.rails{padding:clamp(40px, 6vw, 90px) 0}
.rails__track{display:grid;grid-template-columns:repeat(auto-fill, minmax(min(100%, 300px), 1fr));gap:var(--gap) calc(var(--gap) * 1.5);padding:0 var(--gap)}
.rails__intro{display:grid;gap:22px;align-content:center;padding:clamp(10px, 2vw, 30px) clamp(4px, 1vw, 12px) 30px}
.rails__intro p{max-width:40ch}
.rails__intro .link{justify-self:start;font-weight:500}
.cover{position:relative;border-radius:var(--r);aspect-ratio:4/5;display:flex;flex-direction:column;justify-content:space-between;padding:0 0 clamp(18px, 2vw, 28px);box-shadow:0 40px 70px -40px rgba(0,0,0,.8)}
.cover__photo{position:absolute;inset:0;border-radius:inherit}
.cover__photo .art{position:absolute;top:0;left:-8%;width:116%;max-width:none;height:100%}
.cover__photo::after{content:"";position:absolute;inset:0;background:linear-gradient(to top, color-mix(in oklab, var(--field) 96%, transparent) 4%, transparent 42%)}
.cover__wordbox{position:relative;z-index:2;clip-path:inset(0 0 -100% 0);padding:0 5%}
.cover__word{margin-top:-.07em;text-align:center;line-height:.8}
.cover__info{position:relative;z-index:2;padding:0 clamp(18px, 2vw, 28px);display:grid;gap:8px}
.cover__price{font-family:var(--font-display);font-weight:800;font-size:clamp(22px, 2vw, 28px);line-height:1;letter-spacing:-.02em}
.cover__text{font-size:15px;line-height:1.4;max-width:34ch}
.cover--red{--field:var(--red);color:var(--cream)}
.cover--olive{--field:var(--olive);color:var(--cream)}
.cover--cream{--field:var(--cream);color:var(--ink)}
.cover.marks::before{top:18px;right:18px}
.cover.marks::after{display:none}
.motion .rails{padding:0;height:calc(100svh + var(--run, 0px));overflow-x:clip}
.motion .rails__pin{position:sticky;top:0;height:100svh;display:flex;align-items:center;padding-top:calc(var(--head) + 8px);overflow:clip}
.motion .rails__track{display:flex;align-items:center;width:max-content;gap:clamp(20px, 3vw, 48px);padding:0 max(var(--gap), 4vw)}
.motion .rails__intro{width:min(440px, 78vw);flex:none}
.motion .cover{width:clamp(270px, min(29vw, 52svh), 420px);flex:none;will-change:transform}
@media (max-width:700px){.motion .cover{width:min(80vw, 42svh);aspect-ratio:2/3}}
.foot{margin-top:var(--gap);padding:clamp(40px, 6vw, 80px) calc(var(--gap) + var(--pad) * .5) 28px;display:grid;grid-template-columns:1fr auto;gap:28px 40px;align-items:end}
.foot__brand{font-family:var(--font-display);font-weight:900;font-size:clamp(56px, 9vw, 150px);line-height:.8;letter-spacing:-.05em;text-decoration:none}
.foot__nav{display:flex;flex-wrap:wrap;gap:10px 26px;font-weight:500;justify-content:end}
.foot__small{grid-column:1/-1;display:flex;flex-wrap:wrap;justify-content:space-between;gap:10px 24px;border-top:1.5px solid var(--line);padding-top:20px;font-size:14px;color:var(--muted)}
@media (max-width:700px){.foot{grid-template-columns:1fr}.foot__nav{justify-content:start}}
.repairs__card{display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 7fr);gap:clamp(36px, 5vw, 96px)}
.repairs__head{display:grid;gap:22px;align-content:start}
.repairs__head .lead{max-width:36ch}
.repairs__photo{margin-top:clamp(6px, 1.5vw, 24px);border-radius:var(--r-s);aspect-ratio:5/4}
.prices{border-bottom:1.5px solid var(--line)}
.price{position:relative;display:grid;grid-template-columns:minmax(0, 1fr) auto;gap:6px 24px;padding:22px 0 20px}
.price__rule{position:absolute;left:0;right:0;top:0;height:1.5px;background:var(--line)}
.price__name{font-family:var(--font-display);font-weight:800;font-size:clamp(22px, 2.1vw, 32px);line-height:1.02;letter-spacing:-.02em}
.price__note{grid-column:1;font-size:15px;line-height:1.35;color:var(--muted)}
.price__cost{grid-column:2;grid-row:1/span 2;align-self:center;font-family:var(--font-display);font-weight:900;font-size:clamp(36px, 3.8vw, 60px);line-height:.9;letter-spacing:-.04em;white-space:nowrap;text-align:right}
.price__cost small{display:block;font:600 12px/1.2 var(--font-text);letter-spacing:.02em;opacity:.7;margin-top:6px}
.repairs__foot{margin-top:26px;display:flex;flex-wrap:wrap;gap:10px 22px;align-items:baseline;font-weight:500}
@media (max-width:860px){.repairs__card{grid-template-columns:1fr}.repairs__photo{aspect-ratio:3/2}}
.again__stage{position:relative;height:max(100svh, 640px);overflow:clip;isolation:isolate}
.again__photo{position:absolute;inset:0}
.again__knock{position:absolute;inset:0;z-index:1;background:var(--ink);mix-blend-mode:multiply;container-type:inline-size;display:grid;align-content:center;padding:0 3vw 16svh}
.again__word{color:#fff;text-align:center;line-height:.8}
.again__card{position:absolute;z-index:2;left:var(--gap);bottom:var(--gap);width:min(640px, calc(100% - 2 * var(--gap)));margin:0;padding:clamp(24px, 3vw, 46px);display:grid;gap:16px;justify-items:start}
.again__title{font-family:var(--font-display);font-weight:800;font-size:clamp(28px, 3vw, 46px);line-height:.96;letter-spacing:-.03em;text-wrap:balance}
.again__card p{max-width:48ch}
@media (max-width:700px){.again__knock{align-content:start;padding:22svh 3vw 0}}
.motion .again__knock{will-change:transform}
.motion .again{height:calc(max(100svh, 640px) + 160svh)}
.motion .again__stage{position:sticky;top:0}
.sell{padding:clamp(50px, 7vw, 110px) var(--gap);display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 7fr);gap:clamp(32px, 5vw, 80px);align-items:start}
.sell__intro{position:sticky;top:calc(var(--head) + 40px);display:grid;gap:22px;justify-items:start;padding-left:calc(var(--pad) * .5)}
.steps{display:grid;gap:var(--gap);counter-reset:step}
.step{position:relative;border-radius:var(--r);padding:clamp(24px, 3vw, 44px);display:grid;grid-template-columns:minmax(0, 1fr) minmax(0, 1.05fr);gap:24px 32px;min-height:min(60svh, 520px);transform-origin:50% 0;counter-increment:step}
.step__text{display:grid;gap:18px;align-content:space-between}
.step__text::before{content:"0" counter(step);font:700 14px/1 var(--font-text);letter-spacing:.12em;opacity:.7}
.step__title{font-family:var(--font-display);font-weight:900;font-size:clamp(38px, 4.2vw, 70px);line-height:.88;letter-spacing:-.04em;text-wrap:balance}
.step__text p{max-width:34ch}
.step__photo{border-radius:var(--r-s);min-height:220px}
.step__photo .art{position:absolute;inset:0;width:100%;height:100%}
.step.marks::after{display:none}
.motion .step{position:sticky;top:calc(var(--head) + 30px)}
@media (max-width:860px){.sell{grid-template-columns:1fr}.sell__intro{position:static;padding-left:0}}
@media (max-width:560px){.step{grid-template-columns:1fr;min-height:0}.step__photo{aspect-ratio:3/2;min-height:0}}
.drops__card{display:grid;grid-template-columns:minmax(0, 4fr) minmax(0, 8fr);gap:clamp(32px, 5vw, 90px)}
.drops__head{display:grid;gap:22px;align-content:start}
.drops__head .lead{max-width:30ch}
.drops__list{border-top:1.5px solid var(--line)}
.drop{display:grid;grid-template-columns:auto minmax(0, 1fr) auto;gap:10px clamp(20px, 3vw, 48px);align-items:center;padding:clamp(16px, 1.8vw, 26px) 0;border-bottom:1.5px solid var(--line)}
.drop__date{display:flex;align-items:baseline;gap:8px;min-width:3.2em;font-family:var(--font-display)}
.drop__day{font-weight:900;font-size:clamp(52px, 6vw, 100px);line-height:.8;letter-spacing:-.05em}
.drop__month{font-weight:700;font-size:clamp(16px, 1.4vw, 20px)}
.drop__body{display:grid;gap:6px}
.drop__title{font-family:var(--font-display);font-weight:800;font-size:clamp(22px, 2.1vw, 32px);line-height:1;letter-spacing:-.02em}
.drop__text{font-size:15px;line-height:1.4;color:var(--muted);max-width:46ch}
.drop__tag{justify-self:end;white-space:nowrap;font-size:14px;font-weight:600;padding:.5em 1em;border-radius:999px;background:var(--cream);color:var(--red)}
.drop__tag--soon{background:none;color:var(--cream);box-shadow:inset 0 0 0 1.5px var(--cream)}
@media (max-width:860px){.drops__card{grid-template-columns:1fr}}
@media (max-width:600px){.drop{grid-template-columns:auto minmax(0, 1fr)}.drop__tag{grid-column:2;justify-self:start}}
.voices__card{display:grid;gap:clamp(30px, 4vw, 56px);padding-left:0;padding-right:0}
.voices__title{padding:0 var(--pad);max-width:14ch}
.voices__row{overflow:hidden}
.voices__list{display:grid;grid-template-columns:repeat(auto-fill, minmax(min(100%, 280px), 1fr));gap:var(--gap);padding:0 var(--pad)}
.voice{display:grid;gap:22px;align-content:space-between;padding:clamp(22px, 2.2vw, 32px);border-radius:var(--r-s);background:var(--cream);color:var(--ink);position:relative}
.voice::before{content:"\201C";position:absolute;top:6px;right:18px;font:900 72px/1 var(--font-display);color:var(--red);opacity:.22}
.voice blockquote p{font-family:var(--font-display);font-weight:700;font-size:clamp(20px, 1.7vw, 25px);line-height:1.12;letter-spacing:-.015em}
.voice__who{font-size:14px;line-height:1.35;font-weight:600;color:var(--red)}
.voice__who span{display:block;font-weight:500;color:color-mix(in oklab, var(--ink) 60%, transparent)}
.motion .voices__list{display:flex;width:max-content;gap:0;padding:0}
.motion .voice{width:clamp(270px, 26vw, 380px);margin-right:var(--gap)}
.lookbook{display:grid;place-items:center;min-height:clamp(1000px, 96vw, 1400px);padding:clamp(80px, 10vw, 160px) var(--gap)}
.lookbook__stage{position:absolute;inset:0}
.shot{position:absolute;margin:0;border-radius:var(--r-s);overflow:hidden;background:var(--red-deep);box-shadow:0 30px 60px -28px rgba(0,0,0,.85)}
.shot figcaption{position:absolute;left:10px;bottom:10px;z-index:2;font:600 12px/1 var(--font-text);padding:.55em .85em;border-radius:999px;background:rgba(16,12,13,.62);-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px);color:var(--cream);white-space:nowrap}
.shot--a{left:3%;top:5%;width:24%;aspect-ratio:3/4;rotate:-5deg;z-index:1}
.shot--b{left:65%;top:2%;width:22%;aspect-ratio:4/5;rotate:4deg;z-index:3}
.shot--c{left:33%;top:9%;width:17%;aspect-ratio:3/4;rotate:3deg;z-index:1}
.shot--d{left:75%;top:45%;width:21%;aspect-ratio:3/4;rotate:-3deg;z-index:3}
.shot--e{left:7%;top:56%;width:21%;aspect-ratio:4/5;rotate:6deg;z-index:3}
.shot--f{left:39%;top:66%;width:26%;aspect-ratio:5/4;rotate:-2deg;z-index:1}
.lookbook__center{position:relative;z-index:2;width:100%;display:grid;justify-items:center;gap:22px;text-align:center}
.lookbook__wordbox{width:100%}
.lookbook__word{margin:0 auto;color:var(--cream)}
.lookbook__text{max-width:42ch;font-size:clamp(17px, 1.4vw, 20px);font-weight:500}
.lookbook__link{font-weight:500}
@media (max-width:700px){.lookbook{min-height:1260px}.shot--a{left:2%;top:2%;width:50%}.shot--b{left:52%;top:7%;width:46%}.shot--c{left:12%;top:23%;width:36%}.shot--d{left:54%;top:58%;width:44%}.shot--e{left:2%;top:66%;width:48%}.shot--f{left:36%;top:83%;width:54%}}
.faq__card{display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 7fr);gap:clamp(32px, 5vw, 90px)}
.faq__head{display:grid;gap:22px;align-content:start}
.faq__head p{max-width:34ch}
.faq__list{border-top:1.5px solid var(--line)}
.qa{border-bottom:1.5px solid var(--line)}
.qa summary{list-style:none;cursor:pointer;display:flex;align-items:center;justify-content:space-between;gap:24px;padding:22px 0}
.qa summary::-webkit-details-marker{display:none}
.qa__q{font-family:var(--font-display);font-weight:800;font-size:clamp(21px, 2vw, 30px);line-height:1.05;letter-spacing:-.02em;text-decoration:underline;text-decoration-color:transparent;text-decoration-thickness:1.5px;text-underline-offset:.2em}
.qa__icon{position:relative;width:40px;height:40px;flex:none;border-radius:50%;border:1.5px solid currentColor}
.qa__icon::before,.qa__icon::after{content:"";position:absolute;left:50%;top:50%;width:14px;height:1.5px;margin:-.75px 0 0 -7px;background:currentColor;transition:transform .45s var(--spring)}
.qa__icon::after{transform:rotate(90deg)}
.qa[open] .qa__icon::after{transform:rotate(0)}
.qa[open] .qa__icon::before{transform:rotate(180deg)}
.qa__a{padding:0 64px 24px 0}
.qa__a p{max-width:56ch}
@media (hover:hover){.qa summary:hover .qa__q{text-decoration-style:wavy;text-decoration-color:currentColor}.qa summary:hover .qa__icon{animation:wobble .6s var(--spring)}}
.qa summary:focus-visible .qa__q{text-decoration-style:wavy;text-decoration-color:currentColor}
@media (max-width:860px){.faq__card{grid-template-columns:1fr}.qa__a{padding-right:0}}
.visit__card{display:grid;gap:clamp(34px, 4vw, 64px);overflow:clip}
.visit__word{text-align:center;margin-top:-.02em}
.visit__grid{display:grid;grid-template-columns:minmax(0, 1fr) minmax(0, .9fr) minmax(0, 1fr);gap:clamp(24px, 3vw, 48px);align-items:start}
.visit__info{display:grid;gap:26px}
.hours{margin:0;display:grid;border-top:1.5px solid var(--line)}
.hours div{display:flex;justify-content:space-between;gap:16px;padding:12px 0;border-bottom:1.5px solid var(--line)}
.hours dt{font-weight:500}
.hours dd{margin:0;font-weight:600;white-space:nowrap}
.visit__links{display:flex;flex-wrap:wrap;gap:8px 22px;font-weight:500}
.visit__photo{margin:0;border-radius:var(--r-s);overflow:hidden;aspect-ratio:4/5}
.visit__form{display:grid;gap:18px;justify-items:start;padding:clamp(22px, 2.4vw, 34px);border-radius:var(--r-s);background:color-mix(in oklab, var(--red-deep) 70%, var(--red))}
.field{display:grid;gap:6px;width:100%;font-size:14px;font-weight:500}
.field input,.field textarea{width:100%;border:0;border-bottom:1.5px solid color-mix(in oklab, var(--cream) 50%, transparent);background:none;padding:8px 0 10px;font-size:17px;border-radius:0;resize:vertical;transition:border-color .3s}
.field input:focus,.field textarea:focus{outline:none;border-bottom-color:var(--cream)}
.field-row{display:grid;grid-template-columns:1fr 1fr;gap:18px;width:100%}
.visit__status{font-weight:600;min-height:1.4em}
@media (max-width:1000px){.visit__grid{grid-template-columns:1fr 1fr}.visit__photo{grid-row:span 2;aspect-ratio:auto;height:100%}}
@media (max-width:640px){.visit__grid{grid-template-columns:1fr}.visit__photo{grid-row:auto;aspect-ratio:4/3;height:auto}}
.motion .hero__photo .art,.motion .hero__chi,.motion .voices__list{will-change:transform}
@media (prefers-reduced-motion:reduce){.art animate{display:none}}
</style>
</head>
<body>

<!-- Shared SVG definitions -->
<svg class="sprite" aria-hidden="true" focusable="false">
  <defs>
    <filter id="sh" x="-30%" y="-30%" width="160%" height="170%"><feDropShadow dx="0" dy="18" stdDeviation="20" flood-color="#000" flood-opacity=".38"/></filter>
    <filter id="sh2" x="-20%" y="-30%" width="140%" height="170%"><feDropShadow dx="0" dy="5" stdDeviation="7" flood-color="#000" flood-opacity=".16"/></filter>
    <filter id="bl6" x="-30%" y="-30%" width="160%" height="160%"><feGaussianBlur stdDeviation="6"/></filter>
    <filter id="bl14" x="-50%" y="-50%" width="200%" height="200%"><feGaussianBlur stdDeviation="14"/></filter>
    <filter id="bl30" x="-80%" y="-80%" width="260%" height="260%"><feGaussianBlur stdDeviation="30"/></filter>
    <radialGradient id="glowW"><stop offset="0" stop-color="#ffe2ad" stop-opacity=".95"/><stop offset=".3" stop-color="#f3a556" stop-opacity=".45"/><stop offset="1" stop-color="#f3a556" stop-opacity="0"/></radialGradient>
    <radialGradient id="glowR"><stop offset="0" stop-color="#d9493d" stop-opacity=".8"/><stop offset="1" stop-color="#a72d2d" stop-opacity="0"/></radialGradient>
    <linearGradient id="lit" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffe0a3"/><stop offset=".6" stop-color="#f2a95a"/><stop offset="1" stop-color="#c9772f"/></linearGradient>
    <linearGradient id="brass" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#f6dc96"/><stop offset=".45" stop-color="#c79a3e"/><stop offset=".7" stop-color="#8f6a22"/><stop offset="1" stop-color="#e9c977"/></linearGradient>
    <linearGradient id="wood" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#6b3f27"/><stop offset="1" stop-color="#3a2015"/></linearGradient>
    <linearGradient id="linen" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fbf8f2"/><stop offset="1" stop-color="#d9d0bf"/></linearGradient>
    <linearGradient id="fadeR" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#a72d2d" stop-opacity=".28"/><stop offset="1" stop-color="#a72d2d" stop-opacity="0"/></linearGradient>
    <linearGradient id="fadeO" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#5b6a45" stop-opacity=".3"/><stop offset="1" stop-color="#5b6a45" stop-opacity="0"/></linearGradient>
    <symbol id="star" viewBox="0 0 20 20"><path d="M10 1l2.7 5.6 6.1.9-4.4 4.3 1 6.1L10 15l-5.4 2.9 1-6.1L1.2 7.5l6.1-.9Z"/></symbol>
    <symbol id="tick" viewBox="0 0 20 20"><path d="M5 10.5l3.2 3.2L15 6.5" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></symbol>
  </defs>
</svg>

<div class="progress" aria-hidden="true"></div>

<header class="hdr" data-section="nav">
  <div class="hdr__bar">
    <a class="hdr__brand" href="#hero"><i aria-hidden="true"></i>Ostler</a>
    <nav class="hdr__nav" id="nav" aria-label="Main">
      <a class="link" href="#rails">Product</a>
      <a class="link" href="#repairs">Pricing</a>
      <a class="link" href="#sell">How it works</a>
      <a class="link" href="#drops">Changelog</a>
      <a class="link" href="#visit">Contact</a>
    </nav>
    <a class="btn btn--solid hdr__cta" href="#visit"><span>Book a demo</span><svg class="btn__arrow" viewBox="0 0 28 12" aria-hidden="true"><path d="M0 6h26M21 1l5 5-5 5" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
    <button class="icon-btn hdr__menu" type="button" aria-expanded="false" aria-controls="nav" aria-label="Open menu" data-open="Open menu" data-close="Close menu"><span></span><span></span></button>
  </div>
</header>

<main>
  <!-- HERO -->
  <section id="hero" data-section="hero" class="hero" data-kind="hero">
    <div class="hero__card marks">
      <figure class="hero__photo">
        <svg class="art" viewBox="0 0 1600 1000" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A softly lit hotel lobby at night">
          <defs>
            <linearGradient id="hBg" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3b1113"/><stop offset=".55" stop-color="#25090b"/><stop offset="1" stop-color="#140607"/></linearGradient>
            <linearGradient id="hScreen" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f6f2ea"/><stop offset="1" stop-color="#efe9de"/></linearGradient>
            <linearGradient id="hBezel" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#4a4142"/><stop offset=".5" stop-color="#151112"/><stop offset="1" stop-color="#3a3233"/></linearGradient>
          </defs>
          <rect width="1600" height="1000" fill="url(#hBg)"/>
          <circle cx="260" cy="260" r="420" fill="url(#glowW)" opacity=".35"/>
          <circle cx="1380" cy="180" r="380" fill="url(#glowR)" opacity=".7"/>
          <circle cx="1250" cy="820" r="360" fill="url(#glowW)" opacity=".18"/>
          <g filter="url(#bl14)" fill="#ffcf8a">
            <circle cx="120" cy="140" r="34" opacity=".35"/><circle cx="330" cy="90" r="22" opacity=".45"/><circle cx="470" cy="210" r="40" opacity=".2"/><circle cx="210" cy="420" r="28" opacity=".3"/><circle cx="90" cy="610" r="46" opacity=".18"/><circle cx="420" cy="560" r="18" opacity=".4"/>
            <circle cx="1180" cy="110" r="30" opacity=".35"/><circle cx="1360" cy="320" r="44" opacity=".22"/><circle cx="1520" cy="160" r="24" opacity=".45"/><circle cx="1480" cy="560" r="36" opacity=".25"/><circle cx="1290" cy="520" r="16" opacity=".5"/><circle cx="1050" cy="60" r="20" opacity=".35"/>
          </g>
          <g stroke="#e2dcce" stroke-opacity=".12" stroke-width="2"><path d="M330 0V60M1180 0V80"/></g>
          <circle cx="330" cy="70" r="14" fill="#ffe2ad"/><circle cx="330" cy="70" r="90" fill="url(#glowW)" opacity=".6"/>
          <circle cx="1180" cy="90" r="12" fill="#ffe2ad"/><circle cx="1180" cy="90" r="80" fill="url(#glowW)" opacity=".55"/>
          <ellipse cx="820" cy="980" rx="320" ry="40" fill="#000" opacity=".5" filter="url(#bl30)"/>

        </svg>
      </figure>
      <div class="hero__device">
        <svg class="hero__phone" role="img" aria-label="A guest's phone showing a conversation with the hotel's Ostler concierge, with live notifications around it" viewBox="0 0 600 820" focusable="false">
          <!-- phone -->
          <g transform="translate(110 24) rotate(-3 190 390)">
            <rect x="-6" y="0" width="392" height="790" rx="62" fill="#000" opacity=".5" filter="url(#sh)"/>
            <rect x="-3" y="130" width="6" height="60" rx="3" fill="#2a2425"/><rect x="-3" y="210" width="6" height="60" rx="3" fill="#2a2425"/><rect x="377" y="170" width="6" height="96" rx="3" fill="#2a2425"/>
            <rect width="380" height="780" rx="60" fill="url(#hBezel)"/>
            <rect x="5" y="5" width="370" height="770" rx="56" fill="#0b0909"/>
            <g transform="translate(14 14)">
              <rect width="352" height="752" rx="46" fill="url(#hScreen)"/>
              <text x="36" y="36" font-size="15" font-weight="600" fill="#100c0d">23:41</text>
              <g fill="#100c0d"><rect x="252" y="28" width="3.5" height="7" rx="1"/><rect x="258" y="25" width="3.5" height="10" rx="1"/><rect x="264" y="22" width="3.5" height="13" rx="1"/><rect x="270" y="19" width="3.5" height="16" rx="1"/></g>
              <path d="M281 26a10 10 0 0 1 14 0M284 30a6 6 0 0 1 8 0" fill="none" stroke="#100c0d" stroke-width="2" stroke-linecap="round"/><circle cx="288" cy="33" r="1.6" fill="#100c0d"/>
              <rect x="302" y="22" width="26" height="13" rx="4" fill="none" stroke="#100c0d" stroke-opacity=".5" stroke-width="1.4"/><rect x="304.5" y="24.5" width="17" height="8" rx="2" fill="#100c0d"/><rect x="329.5" y="26" width="2" height="5" rx="1" fill="#100c0d" opacity=".5"/>
              <rect x="126" y="11" width="100" height="30" rx="15" fill="#000"/>
              <rect x="0" y="52" width="352" height="70" fill="#fbf9f4"/>
              <path d="M0 122H352" stroke="#e4ddd0"/>
              <path d="M24 80l-8 8 8 8" fill="none" stroke="#a72d2d" stroke-width="2.6" stroke-linecap="round" stroke-linejoin="round"/>
              <circle cx="56" cy="88" r="21" fill="#100c0d"/>
              <text x="56" y="93" text-anchor="middle" class="d" font-size="14" font-weight="800" fill="#e2dcce">HH</text>
              <circle cx="71" cy="103" r="5.5" fill="#5fb35a" stroke="#fbf9f4" stroke-width="2.4"/>
              <text x="88" y="84" font-size="15.5" font-weight="700" fill="#100c0d">The Harbour House</text>
              <text x="88" y="103" font-size="11.5" fill="#6b6466">Ostler concierge · replies instantly</text>
              <path d="M318 80v16M310 88h16" stroke="#a72d2d" stroke-width="2.2" stroke-linecap="round" opacity="0"/>
              <rect x="150" y="134" width="52" height="20" rx="10" fill="#e7e0d3"/>
              <text x="176" y="148" text-anchor="middle" font-size="11" font-weight="600" fill="#6b6466">Today</text>

              <rect x="106" y="164" width="232" height="65" rx="18" fill="#a72d2d"/>
              <text font-size="13.5" fill="#f6efe3"><tspan x="120" y="188">Hi! Our flight lands at 11pm —</tspan><tspan x="120" y="207">will anyone be at the desk?</tspan></text>
              <text x="326" y="222" text-anchor="end" font-size="10" fill="#f6efe3" opacity=".7">23:41 ✓✓</text>

              <rect x="14" y="241" width="262" height="84" rx="18" fill="#fff" stroke="#e7e0d3"/>
              <text font-size="13.5" fill="#1d1718"><tspan x="28" y="265">Welcome in advance, Ms Moreau.</tspan><tspan x="28" y="284">Our night porter, Sam, is on until</tspan><tspan x="28" y="303">7am — your key will be waiting.</tspan></text>
              <text x="264" y="318" text-anchor="end" font-size="10" fill="#8a8284">23:41</text>

              <rect x="14" y="331" width="262" height="84" rx="18" fill="#fff" stroke="#e7e0d3"/>
              <text font-size="13.5" fill="#1d1718"><tspan x="28" y="355">Shall I book a taxi from the</tspan><tspan x="28" y="374">airport? It's £42 and takes</tspan><tspan x="28" y="393">about 35 minutes.</tspan></text>
              <text x="264" y="408" text-anchor="end" font-size="10" fill="#8a8284">23:41</text>

              <rect x="122" y="427" width="216" height="65" rx="18" fill="#a72d2d"/>
              <text font-size="13.5" fill="#f6efe3"><tspan x="136" y="451">Yes please! And could we</tspan><tspan x="136" y="470">check out late on Sunday?</tspan></text>
              <text x="326" y="485" text-anchor="end" font-size="10" fill="#f6efe3" opacity=".7">23:42 ✓✓</text>

              <rect x="14" y="504" width="262" height="84" rx="18" fill="#fff" stroke="#e7e0d3"/>
              <text font-size="13.5" fill="#1d1718"><tspan x="28" y="528">All done. Taxi booked for 23:15</tspan><tspan x="28" y="547">under Moreau, and checkout is</tspan><tspan x="28" y="566">now 2pm — £35, on your bill.</tspan></text>
              <text x="264" y="581" text-anchor="end" font-size="10" fill="#8a8284">23:42</text>

              <rect x="14" y="596" width="262" height="80" rx="16" fill="#fff" stroke="#e7e0d3"/>
              <path d="M26 636H264" stroke="#efe9de"/>
              <circle cx="38" cy="616" r="12" fill="#f4e4e1"/><path d="M32 619h12l-1.5-5h-9Z" fill="#a72d2d"/><circle cx="34.5" cy="620.5" r="1.6" fill="#a72d2d"/><circle cx="41.5" cy="620.5" r="1.6" fill="#a72d2d"/>
              <text x="58" y="613" font-size="12.5" font-weight="700" fill="#1d1718">Airport taxi</text>
              <text x="58" y="627" font-size="10.5" fill="#8a8284">Sat 23:15 · driver details at 22:45</text>
              <text x="264" y="620" text-anchor="end" font-size="12.5" font-weight="700" fill="#1d1718">£42</text>
              <circle cx="38" cy="656" r="12" fill="#e8ecdf"/><circle cx="38" cy="656" r="6" fill="none" stroke="#5b6a45" stroke-width="1.8"/><path d="M38 652.5V656l2.2 1.6" stroke="#5b6a45" stroke-width="1.6" fill="none" stroke-linecap="round"/>
              <text x="58" y="653" font-size="12.5" font-weight="700" fill="#1d1718">Late checkout</text>
              <text x="58" y="667" font-size="10.5" fill="#8a8284">Sun 14:00 · Room 214</text>
              <text x="264" y="660" text-anchor="end" font-size="12.5" font-weight="700" fill="#1d1718">£35</text>

              <rect x="14" y="692" width="280" height="40" rx="20" fill="#fff" stroke="#e7e0d3"/>
              <text x="34" y="717" font-size="13.5" fill="#a39b9c">Message</text>
              <circle cx="318" cy="712" r="20" fill="#a72d2d"/>
              <path d="M318 721v-17M311 711l7-7 7 7" fill="none" stroke="#f6efe3" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/>
              <rect x="126" y="740" width="100" height="5" rx="2.5" fill="#100c0d"/>
            </g>
            <path d="M40 30C120 10 260 10 340 30" fill="none" stroke="#fff" stroke-opacity=".1" stroke-width="2"/>
          </g>

          <!-- floating notifications -->
          <g class="hd-card" transform="translate(470 330) rotate(3)">
            <rect width="270" height="92" rx="22" fill="#fbf9f4" filter="url(#sh)"/>
            <circle cx="46" cy="46" r="24" fill="#5b6a45"/><use href="#tick" x="32" y="32" width="28" height="28" color="#f6efe3"/>
            <text x="84" y="42" font-size="16" font-weight="700" fill="#100c0d">Late checkout sold</text>
            <text x="84" y="64" font-size="13" fill="#6b6466">Room 214 · <tspan font-weight="700" fill="#a72d2d">+£35</tspan></text>
          </g>
          <g class="hd-card" transform="translate(468 104) rotate(-3)">
            <rect width="250" height="152" rx="24" fill="#120d0e" filter="url(#sh)"/>
            <rect x=".5" y=".5" width="249" height="151" rx="23.5" fill="none" stroke="#fff" stroke-opacity=".08"/>
            <text x="24" y="38" font-size="11" font-weight="600" letter-spacing="1.6" fill="#a39a9b">MEDIAN REPLY · 24H</text>
            <text x="24" y="96" class="d" font-size="54" font-weight="800" fill="#e2dcce" letter-spacing="-2">9 sec</text>
            <text x="24" y="128" font-size="12" fill="#a39a9b">1,284 chats this week</text>
            <path d="M162 130 172 123 182 126 194 112 204 116 216 100 228 104" fill="none" stroke="#9fd18b" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/>
            <circle cx="228" cy="104" r="4" fill="#9fd18b"/>
          </g>
          <g class="hd-card hd-low" transform="translate(466 528) rotate(-2)">
            <rect width="276" height="96" rx="22" fill="#fbf9f4" filter="url(#sh)"/>
            <circle cx="44" cy="48" r="23" fill="#d39b2a"/>
            <text x="44" y="54" text-anchor="middle" class="d" font-size="18" font-weight="800" fill="#100c0d">SO</text>
            <text x="80" y="42" font-size="15.5" font-weight="700" fill="#100c0d">Handed to Sam</text>
            <text x="80" y="62" font-size="12.5" fill="#6b6466">Night porter · refund question</text>
            <rect x="220" y="22" width="40" height="20" rx="10" fill="#f4e4e1"/>
            <text x="240" y="36" text-anchor="middle" font-size="10" font-weight="700" fill="#a72d2d">2m</text>
          </g>
        </svg>
      </div>
      <div class="hero__wordclip"><h1 class="hero__word display" style="--len:6">Ostler</h1></div>
      <div class="hero__info">
        <p class="hero__title">An AI concierge that knows your hotel like your best night porter</p>
        <p class="hero__lead">Ostler answers guest messages in 41 languages, books the extras and hands the tricky ones to your team — on chat, SMS, email and the phone.</p>
        <p class="hero__addr">Live in 212 independent hotels<br>across fourteen countries</p>
      </div>
      <div class="hero__side">
        <p class="hero__hours"><i aria-hidden="true"></i>Online now · median reply 9 sec</p>
        <a class="btn" href="#rails"><span>See the product</span><svg class="btn__arrow" viewBox="0 0 28 12" aria-hidden="true"><path d="M0 6h26M21 1l5 5-5 5" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
      </div>
    </div>
  </section>

  <div class="ticker" data-section="ticker" aria-hidden="true">
    <div class="ticker__track">
      <span>Answers in 41 languages<i></i><em>Sells the extras</em><i></i>Hands off to humans<i></i><em>Live in 14 days</em><i></i>Never clocks off<i></i><em>GDPR-ready</em><i></i></span>
      <span>Answers in 41 languages<i></i><em>Sells the extras</em><i></i>Hands off to humans<i></i><em>Live in 14 days</em><i></i>Never clocks off<i></i><em>GDPR-ready</em><i></i></span>
    </div>
  </div>

  <div class="logos" data-section="logos" aria-label="Hotels using Ostler">
    <p>Trusted at the front desk of</p>
    <span>The Harbour House</span><span>Casa do Rio</span><span>Saltings</span><span>Kiln House</span><span>Hotel Lindqvist</span><span>Fernhill</span><span>The Wren</span>
  </div>

  <!-- STORY -->
  <section id="story" data-section="story" data-kind="about">
    <div class="story__card card on-cream marks">
      <h2 class="story__title h2" data-split>Guests don't want another app. They want an answer at 2am.</h2>
      <figure class="story__photo print" data-reveal="drop">
        <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A hotel manager's lock screen at 7am showing Ostler notifications from overnight">
          <defs>
            <linearGradient id="sBg" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#4a2018"/><stop offset=".6" stop-color="#2a1210"/><stop offset="1" stop-color="#170b0a"/></linearGradient>
          </defs>
          <rect width="400" height="500" fill="url(#sBg)"/>
          <circle cx="70" cy="120" r="220" fill="url(#glowW)" opacity=".55"/>
          <g filter="url(#bl14)">
            <rect x="250" y="40" width="130" height="190" rx="6" fill="#f4c88b" opacity=".35"/>
            <path d="M-20 420Q200 360 420 400V500H-20Z" fill="#e9dfcd" opacity=".35"/>
            <rect x="40" y="380" width="120" height="50" rx="20" fill="#f6efe3" opacity=".3"/>
          </g>
          <text x="200" y="58" text-anchor="middle" font-size="15" font-weight="500" fill="#f6efe3" opacity=".85">Saturday 24 October</text>
          <text x="200" y="128" text-anchor="middle" class="d" font-size="76" font-weight="700" fill="#f6efe3" letter-spacing="-2">07:02</text>
          <g>
            <rect x="22" y="160" width="356" height="88" rx="20" fill="#f6f2ea" opacity=".9" filter="url(#sh2)"/>
            <rect x="38" y="176" width="26" height="26" rx="7" fill="#a72d2d"/><text x="51" y="195" text-anchor="middle" class="d" font-size="16" font-weight="900" fill="#e2dcce">O</text>
            <text x="74" y="194" font-size="11.5" font-weight="600" letter-spacing=".8" fill="#6b6466">OSTLER</text>
            <text x="362" y="194" text-anchor="end" font-size="11.5" fill="#8a8284">now</text>
            <text x="38" y="222" font-size="14" font-weight="700" fill="#100c0d">Overnight summary is ready</text>
            <text x="38" y="239" font-size="12.5" fill="#4d4648">41 conversations · 3 need you this morning</text>
          </g>
          <g>
            <rect x="22" y="258" width="356" height="88" rx="20" fill="#f6f2ea" opacity=".86" filter="url(#sh2)"/>
            <rect x="38" y="274" width="26" height="26" rx="7" fill="#a72d2d"/><text x="51" y="293" text-anchor="middle" class="d" font-size="16" font-weight="900" fill="#e2dcce">O</text>
            <text x="74" y="292" font-size="11.5" font-weight="600" letter-spacing=".8" fill="#6b6466">OSTLER</text>
            <text x="362" y="292" text-anchor="end" font-size="11.5" fill="#8a8284">03:18</text>
            <text x="38" y="320" font-size="14" font-weight="700" fill="#100c0d">Room 108 · extra pillows</text>
            <text x="38" y="337" font-size="12.5" fill="#4d4648">Sent to housekeeping · delivered 03:29</text>
          </g>
          <g>
            <rect x="22" y="356" width="356" height="88" rx="20" fill="#f6f2ea" opacity=".82" filter="url(#sh2)"/>
            <rect x="38" y="372" width="26" height="26" rx="7" fill="#a72d2d"/><text x="51" y="391" text-anchor="middle" class="d" font-size="16" font-weight="900" fill="#e2dcce">O</text>
            <text x="74" y="390" font-size="11.5" font-weight="600" letter-spacing=".8" fill="#6b6466">OSTLER</text>
            <text x="362" y="390" text-anchor="end" font-size="11.5" fill="#8a8284">01:47</text>
            <text x="38" y="418" font-size="14" font-weight="700" fill="#100c0d">Review reply drafted</text>
            <text x="38" y="435" font-size="12.5" fill="#4d4648">5 stars from Daniel K. · tap to approve</text>
          </g>
          <rect x="150" y="478" width="100" height="5" rx="2.5" fill="#f6efe3" opacity=".7"/>
        </svg>
      </figure>
      <div class="story__body">
        <p class="story__text lead" data-reveal="up">Ostler started in 2021 at a 38-room hotel in Bristol, where the night porter was also the barman, the concierge and the IT department. Today it looks after guest conversations at more than two hundred independent hotels, each one trained on its own rooms, rules and quirks.</p>
        <ul class="facts">
          <li data-reveal="up"><strong>1.8M</strong><span>guest conversations handled since launch</span></li>
          <li data-reveal="up"><strong>9 sec</strong><span>median reply, at any hour of the night</span></li>
          <li data-reveal="up"><strong>87%</strong><span>resolved without staff stepping in</span></li>
        </ul>
      </div>
    </div>
  </section>

  <!-- PRODUCT MODULES -->
  <section id="rails" data-section="modules" class="rails" data-kind="collections">
    <div class="rails__pin">
      <div class="rails__track">
        <div class="rails__intro">
          <h2 class="h2">Six modules, one guest conversation</h2>
          <p class="lead muted">Start with the concierge and switch the rest on when you're ready. Every module shares the same memory of the guest, so nobody has to repeat themselves.</p>
          <a class="link" href="#drops">What shipped this month</a>
        </div>

        <article class="cover cover--red marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A guest asks about breakfast in French and Ostler replies in French">
              <rect width="400" height="500" fill="#a72d2d"/>
              <circle cx="320" cy="140" r="220" fill="#c03b35" opacity=".6"/>
              <g transform="translate(200 116) scale(.78) translate(-200 -100)"><g transform="translate(46 104)">
                <rect width="308" height="252" rx="22" fill="#fbf9f4" filter="url(#sh)"/>
                <circle cx="32" cy="32" r="15" fill="#e9e1d0"/><text x="32" y="36.5" text-anchor="middle" font-size="11" font-weight="700" fill="#6b6466">CL</text>
                <text x="56" y="30" font-size="14" font-weight="700" fill="#100c0d">Claire L.</text>
                <text x="56" y="46" font-size="11" fill="#8a8284">Room 312 · checked in</text>
                <rect x="216" y="20" width="76" height="24" rx="12" fill="#5b6a45"/>
                <text x="254" y="36" text-anchor="middle" font-size="11" font-weight="700" fill="#f6efe3">FR → EN</text>
                <path d="M16 60H292" stroke="#ece6da"/>
                <rect x="16" y="72" width="226" height="58" rx="16" fill="#efe9de"/>
                <text font-size="13.5" fill="#1d1718"><tspan x="30" y="96">Le petit-déjeuner est servi</tspan><tspan x="30" y="115">jusqu'à quelle heure ?</tspan></text>
                <text x="20" y="150" font-size="11.5" font-style="italic" fill="#8a8284">“What time is breakfast served until?”</text>
                <rect x="42" y="162" width="250" height="76" rx="16" fill="#a72d2d"/>
                <text font-size="13.5" fill="#f6efe3"><tspan x="56" y="186">Jusqu'à 10h30 en semaine, et</tspan><tspan x="56" y="205">11h le week-end. Bon appétit !</tspan></text>
                <text x="280" y="228" text-anchor="end" font-size="10" fill="#f6efe3" opacity=".75">07:12 · sent in 4s</text>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:9" data-bounce="still">Concierge</h3></div>
          <div class="cover__info"><p class="cover__price">From £4 / room</p><p class="cover__text">Answers questions about the room, the hotel and the area, in the guest's own language.</p></div>
        </article>

        <article class="cover cover--olive marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="An upgrade offer for a sea view suite, accepted by the guest">
              <defs>
                <linearGradient id="uSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f6c48a"/><stop offset=".7" stop-color="#e98a5a"/><stop offset="1" stop-color="#c76a4e"/></linearGradient>
                <linearGradient id="uSea" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#4f6f94"/><stop offset="1" stop-color="#22374f"/></linearGradient>
                <clipPath id="uClip"><path d="M0 22A22 22 0 0 1 22 0H266A22 22 0 0 1 288 22V112H0Z"/></clipPath>
              </defs>
              <rect width="400" height="500" fill="#5b6a45"/>
              <circle cx="90" cy="160" r="230" fill="#6c7b55" opacity=".6"/>
              <g transform="translate(200 116) scale(.78) translate(-200 -100)"><g transform="translate(56 92)">
                <rect width="288" height="268" rx="22" fill="#fbf9f4" filter="url(#sh)"/>
                <g clip-path="url(#uClip)">
                  <rect width="288" height="112" fill="url(#uSky)"/>
                  <circle cx="190" cy="74" r="20" fill="#ffe6b8"/>
                  <circle cx="190" cy="74" r="60" fill="url(#glowW)" opacity=".6"/>
                  <rect y="74" width="288" height="38" fill="url(#uSea)"/>
                  <path d="M170 82h40M160 90h60M176 98h28" stroke="#ffd59a" stroke-opacity=".7" stroke-width="2"/>
                  <path d="M0 104h288" stroke="#e8dcc6" stroke-width="8"/>
                  <path d="M96 0V112M192 0V112" stroke="#e8dcc6" stroke-width="5"/>
                  <path d="M0 0H70Q40 60 50 112H0Z" fill="#f2ead9" opacity=".85"/>
                </g>
                <rect x="14" y="14" width="70" height="22" rx="11" fill="#100c0d" opacity=".75"/>
                <text x="49" y="29" text-anchor="middle" font-size="10.5" font-weight="700" fill="#f6efe3">TONIGHT</text>
                <text x="18" y="140" font-size="16.5" font-weight="700" fill="#100c0d">Upgrade to the Sea View Suite</text>
                <text x="18" y="159" font-size="12" fill="#6b6466">Balcony, roll-top bath, checkout at noon</text>
                <text x="18" y="200" class="d" font-size="32" font-weight="800" fill="#a72d2d">+£60</text>
                <text x="114" y="198" font-size="12.5" fill="#8a8284">usually £95</text>
                <path d="M114 194H180" stroke="#8a8284" stroke-width="1.2"/>
                <rect x="18" y="218" width="124" height="34" rx="17" fill="#100c0d"/>
                <text x="80" y="240" text-anchor="middle" font-size="13" font-weight="600" fill="#f6efe3">Yes, upgrade me</text>
                <rect x="150" y="218" width="120" height="34" rx="17" fill="none" stroke="#cfc6b4" stroke-width="1.5"/>
                <text x="210" y="240" text-anchor="middle" font-size="13" font-weight="600" fill="#100c0d">No thanks</text>
              </g>
              <g transform="translate(206 340)">
                <rect width="160" height="36" rx="18" fill="#100c0d" filter="url(#sh2)"/>
                <circle cx="20" cy="18" r="5" fill="#9fd18b"/>
                <text x="32" y="23" font-size="12.5" font-weight="600" fill="#f6efe3">Accepted · 21:04</text>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:6" data-bounce="still">Upsell</h3></div>
          <div class="cover__info"><p class="cover__price">From £1 / room</p><p class="cover__text">Offers upgrades, late checkouts and tables at the moment guests actually want them.</p></div>
        </article>

        <article class="cover cover--cream marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A housekeeping task list created from guest messages">
              <rect width="400" height="500" fill="#e2dcce"/>
              <circle cx="200" cy="230" r="200" fill="#d6cfbe"/>
              <g transform="translate(200 116) scale(.78) translate(-200 -100)"><g transform="translate(36 100)">
                <rect width="328" height="272" rx="22" fill="#fff" filter="url(#sh)"/>
                <text x="20" y="36" font-size="16" font-weight="700" fill="#100c0d">Housekeeping</text>
                <text x="20" y="54" font-size="12" fill="#8a8284">Today · 12 open · 31 done</text>
                <rect x="250" y="22" width="58" height="24" rx="12" fill="#e3efdb"/>
                <circle cx="265" cy="34" r="4" fill="#4f8c3c"/>
                <text x="293" y="38" text-anchor="end" font-size="11" font-weight="700" fill="#3f6b2a">Live</text>
                <g font-size="12.5">
                  <path d="M16 70H312" stroke="#efe9de"/>
                  <rect x="16" y="82" width="44" height="26" rx="8" fill="#f0ebe1"/><text x="38" y="99.5" text-anchor="middle" font-weight="700" fill="#100c0d">108</text>
                  <text x="72" y="93" font-weight="600" fill="#100c0d">Extra pillows ×2</text><text x="72" y="108" font-size="10.5" fill="#8a8284">via chat · 03:18</text>
                  <rect x="226" y="83" width="86" height="24" rx="12" fill="#e3efdb"/><text x="269" y="99" text-anchor="middle" font-size="11" font-weight="700" fill="#3f6b2a">Done · 11m</text>
                  <path d="M16 118H312" stroke="#efe9de"/>
                  <rect x="16" y="130" width="44" height="26" rx="8" fill="#f0ebe1"/><text x="38" y="147.5" text-anchor="middle" font-weight="700" fill="#100c0d">214</text>
                  <text x="72" y="141" font-weight="600" fill="#100c0d">Skip clean until 2pm</text><text x="72" y="156" font-size="10.5" fill="#8a8284">late checkout · paid</text>
                  <rect x="226" y="131" width="86" height="24" rx="12" fill="#f6ead2"/><text x="269" y="147" text-anchor="middle" font-size="11" font-weight="700" fill="#9a6a10">Scheduled</text>
                  <path d="M16 166H312" stroke="#efe9de"/>
                  <rect x="16" y="178" width="44" height="26" rx="8" fill="#f0ebe1"/><text x="38" y="195.5" text-anchor="middle" font-weight="700" fill="#100c0d">305</text>
                  <text x="72" y="189" font-weight="600" fill="#100c0d">Shower draining slowly</text><text x="72" y="204" font-size="10.5" fill="#8a8284">via phone · 06:40</text>
                  <rect x="226" y="179" width="86" height="24" rx="12" fill="#f5dcdc"/><text x="269" y="195" text-anchor="middle" font-size="11" font-weight="700" fill="#a72d2d">Maintenance</text>
                  <path d="M16 214H312" stroke="#efe9de"/>
                  <rect x="16" y="226" width="44" height="26" rx="8" fill="#f0ebe1"/><text x="38" y="243.5" text-anchor="middle" font-weight="700" fill="#100c0d">117</text>
                  <text x="72" y="237" font-weight="600" fill="#100c0d">Travel cot for infant</text><text x="72" y="252" font-size="10.5" fill="#8a8284">pre-arrival · Sat</text>
                  <rect x="226" y="227" width="86" height="24" rx="12" fill="#e2e7ef"/><text x="269" y="243" text-anchor="middle" font-size="11" font-weight="700" fill="#2f4a6b">On its way</text>
                </g>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:5" data-bounce="still">Rooms</h3></div>
          <div class="cover__info"><p class="cover__price">From £1 / room</p><p class="cover__text">Turns “more towels please” into a ticket with a room number, an owner and an ETA.</p></div>
        </article>

        <article class="cover cover--red marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A five-star guest review with a reply drafted by Ostler, ready to approve">
              <rect width="400" height="500" fill="#a72d2d"/>
              <circle cx="80" cy="380" r="240" fill="#7a2222" opacity=".55"/>
              <g transform="translate(200 106) scale(.7) translate(-200 -100)"><g transform="translate(46 92)">
                <rect width="308" height="292" rx="22" fill="#fbf9f4" filter="url(#sh)"/>
                <g fill="#d8a531"><use href="#star" x="20" y="20" width="18" height="18"/><use href="#star" x="40" y="20" width="18" height="18"/><use href="#star" x="60" y="20" width="18" height="18"/><use href="#star" x="80" y="20" width="18" height="18"/><use href="#star" x="100" y="20" width="18" height="18"/></g>
                <text x="288" y="34" text-anchor="end" font-size="11" fill="#8a8284">2 days ago</text>
                <text x="20" y="62" font-size="12" font-weight="600" fill="#6b6466">Daniel K. · couple · 2 nights</text>
                <text font-size="14" font-style="italic" fill="#1d1718"><tspan x="20" y="90">“Spotless room and the best</tspan><tspan x="20" y="110">breakfast we've had in Bristol.</tspan><tspan x="20" y="130">Parking was a little tight.”</tspan></text>
                <path d="M20 148H288" stroke="#ece6da"/>
                <path d="M26 166l2 5 5 2-5 2-2 5-2-5-5-2 5-2Z" fill="#a72d2d"/>
                <text x="40" y="177" font-size="12" font-weight="700" fill="#a72d2d">Draft reply · in your voice</text>
                <text font-size="12.5" fill="#3a3233"><tspan x="20" y="200">Thank you, Daniel — we'll pass that</tspan><tspan x="20" y="218">on to Ana in the kitchen. Next time,</tspan><tspan x="20" y="236">ask us and we'll hold a space for you.</tspan></text>
                <rect x="20" y="250" width="104" height="30" rx="15" fill="#100c0d"/>
                <text x="72" y="270" text-anchor="middle" font-size="12.5" font-weight="600" fill="#f6efe3">Approve</text>
                <rect x="132" y="250" width="70" height="30" rx="15" fill="none" stroke="#cfc6b4" stroke-width="1.5"/>
                <text x="167" y="270" text-anchor="middle" font-size="12.5" font-weight="600" fill="#100c0d">Edit</text>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:7" data-bounce="still">Reviews</h3></div>
          <div class="cover__info"><p class="cover__price">From £0.50 / room</p><p class="cover__text">Drafts a reply to every review in your house voice, for you to approve in one tap.</p></div>
        </article>

        <article class="cover cover--olive marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A live phone call answered by Ostler, with waveform and transcript">
              <rect width="400" height="500" fill="#5b6a45"/>
              <circle cx="320" cy="360" r="230" fill="#4a5838"/>
              <g transform="translate(200 106) scale(.7) translate(-200 -100)"><g transform="translate(56 92)">
                <rect width="288" height="284" rx="26" fill="#120d0e" filter="url(#sh)"/>
                <rect x=".5" y=".5" width="287" height="283" rx="25.5" fill="none" stroke="#fff" stroke-opacity=".08"/>
                <circle cx="30" cy="32" r="5" fill="#e0574c"><animate attributeName="opacity" values="1;.3;1" dur="1.6s" repeatCount="indefinite"/></circle>
                <text x="42" y="36" font-size="11.5" font-weight="600" letter-spacing="1" fill="#a39a9b">LIVE CALL</text>
                <text x="264" y="36" text-anchor="end" font-size="13" font-weight="600" fill="#9fd18b">02:14</text>
                <text x="24" y="66" font-size="18" font-weight="700" fill="#f6efe3">+44 7700 900412</text>
                <g fill="#9fd18b">
                  <rect x="24" y="96" width="3.5" height="16" rx="1.75"/><rect x="31" y="90" width="3.5" height="28" rx="1.75"/><rect x="38" y="84" width="3.5" height="40" rx="1.75"/><rect x="45" y="92" width="3.5" height="24" rx="1.75"/><rect x="52" y="98" width="3.5" height="12" rx="1.75"/><rect x="59" y="86" width="3.5" height="36" rx="1.75"/><rect x="66" y="80" width="3.5" height="48" rx="1.75"/><rect x="73" y="88" width="3.5" height="32" rx="1.75"/><rect x="80" y="94" width="3.5" height="20" rx="1.75"/><rect x="87" y="100" width="3.5" height="8" rx="1.75"/><rect x="94" y="92" width="3.5" height="24" rx="1.75"/><rect x="101" y="84" width="3.5" height="40" rx="1.75"/><rect x="108" y="90" width="3.5" height="28" rx="1.75"/><rect x="115" y="96" width="3.5" height="16" rx="1.75"/><rect x="122" y="88" width="3.5" height="32" rx="1.75"/><rect x="129" y="82" width="3.5" height="44" rx="1.75"/><rect x="136" y="92" width="3.5" height="24" rx="1.75"/><rect x="143" y="98" width="3.5" height="12" rx="1.75"/>
                </g>
                <g fill="#9fd18b" opacity=".3">
                  <rect x="150" y="100" width="3.5" height="8" rx="1.75"/><rect x="157" y="96" width="3.5" height="16" rx="1.75"/><rect x="164" y="98" width="3.5" height="12" rx="1.75"/><rect x="171" y="100" width="3.5" height="8" rx="1.75"/><rect x="178" y="97" width="3.5" height="14" rx="1.75"/><rect x="185" y="100" width="3.5" height="8" rx="1.75"/><rect x="192" y="98" width="3.5" height="12" rx="1.75"/><rect x="199" y="100" width="3.5" height="8" rx="1.75"/><rect x="206" y="99" width="3.5" height="10" rx="1.75"/><rect x="213" y="100" width="3.5" height="8" rx="1.75"/><rect x="220" y="98" width="3.5" height="12" rx="1.75"/><rect x="227" y="100" width="3.5" height="8" rx="1.75"/><rect x="234" y="99" width="3.5" height="10" rx="1.75"/><rect x="241" y="100" width="3.5" height="8" rx="1.75"/><rect x="248" y="99" width="3.5" height="10" rx="1.75"/><rect x="255" y="100" width="3.5" height="8" rx="1.75"/>
                </g>
                <path d="M24 140H264" stroke="#fff" stroke-opacity=".08"/>
                <text x="24" y="162" font-size="10" font-weight="700" letter-spacing="1.2" fill="#857b7c">CALLER</text>
                <text x="24" y="181" font-size="13.5" fill="#e2dcce">Any chance of a table for four at 8?</text>
                <text x="24" y="207" font-size="10" font-weight="700" letter-spacing="1.2" fill="#d39b2a">OSTLER</text>
                <text font-size="13.5" fill="#f6efe3"><tspan x="24" y="226">8:15 by the window is free — shall</tspan><tspan x="24" y="244">I book it under Patel?</tspan></text>
                <rect x="24" y="254" width="186" height="22" rx="11" fill="#22301b"/>
                <use href="#tick" x="30" y="256" width="18" height="18" color="#9fd18b"/>
                <text x="52" y="269" font-size="11.5" font-weight="600" fill="#9fd18b">Booked · SMS confirmation sent</text>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:5" data-bounce="still">Voice</h3></div>
          <div class="cover__info"><p class="cover__price">From £2 / room</p><p class="cover__text">Picks up the phone when the desk can't, books what's needed and texts a summary.</p></div>
        </article>

        <article class="cover cover--cream marks">
          <figure class="cover__photo print">
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A chart of guest requests by hour, peaking overnight">
              <rect width="400" height="500" fill="#e2dcce"/>
              <circle cx="300" cy="140" r="200" fill="#d6cfbe"/>
              <g transform="translate(200 116) scale(.78) translate(-200 -100)"><g transform="translate(36 104)">
                <rect width="328" height="256" rx="22" fill="#fff" filter="url(#sh)"/>
                <text x="20" y="34" font-size="15" font-weight="700" fill="#100c0d">Guest requests by hour</text>
                <text x="20" y="52" font-size="11.5" fill="#8a8284">Last 30 days · 5,402 requests</text>
                <text x="308" y="40" text-anchor="end" class="d" font-size="28" font-weight="800" fill="#a72d2d">58%</text>
                <text x="308" y="55" text-anchor="end" font-size="10" fill="#8a8284">outside desk hours</text>
                <path d="M20 196H308M20 160H308M20 124H308" stroke="#f1ece3"/>
                <rect x="104" y="66" width="144" height="130" fill="#f6f2ea"/>
                <text x="176" y="80" text-anchor="middle" font-size="9.5" font-weight="600" fill="#a39b9c">DESK STAFFED</text>
                <g fill="#a72d2d">
                  <rect x="20" y="158" width="8" height="38" rx="2"/><rect x="32" y="166" width="8" height="30" rx="2"/><rect x="44" y="174" width="8" height="22" rx="2"/><rect x="56" y="182" width="8" height="14" rx="2"/><rect x="68" y="186" width="8" height="10" rx="2"/><rect x="80" y="184" width="8" height="12" rx="2"/><rect x="92" y="170" width="8" height="26" rx="2"/>
                  <rect x="248" y="140" width="8" height="56" rx="2"/><rect x="260" y="132" width="8" height="64" rx="2"/><rect x="272" y="126" width="8" height="70" rx="2"/><rect x="284" y="122" width="8" height="74" rx="2"/><rect x="296" y="130" width="8" height="66" rx="2"/>
                </g>
                <g fill="#cfc6b4">
                  <rect x="104" y="148" width="8" height="48" rx="2"/><rect x="116" y="134" width="8" height="62" rx="2"/><rect x="128" y="146" width="8" height="50" rx="2"/><rect x="140" y="162" width="8" height="34" rx="2"/><rect x="152" y="168" width="8" height="28" rx="2"/><rect x="164" y="166" width="8" height="30" rx="2"/><rect x="176" y="170" width="8" height="26" rx="2"/><rect x="188" y="168" width="8" height="28" rx="2"/><rect x="200" y="162" width="8" height="34" rx="2"/><rect x="212" y="156" width="8" height="40" rx="2"/><rect x="224" y="148" width="8" height="48" rx="2"/><rect x="236" y="142" width="8" height="54" rx="2"/>
                </g>
                <g font-size="10" fill="#a39b9c"><text x="20" y="212">00</text><text x="92" y="212">06</text><text x="164" y="212">12</text><text x="236" y="212">18</text><text x="292" y="212">23</text></g>
                <path d="M20 224H308" stroke="#f1ece3"/>
                <text x="20" y="243" font-size="12" fill="#100c0d"><tspan font-weight="700">Top ask:</tspan> breakfast times · 18% of all requests</text>
              </g>
            </g></svg>
          </figure>
          <div class="cover__wordbox fillbox"><h3 class="cover__word display fill" style="--len:8" data-bounce="still">Insights</h3></div>
          <div class="cover__info"><p class="cover__price">Included</p><p class="cover__text">Shows what guests ask, when they ask it, and what answering it is worth.</p></div>
        </article>
      </div>
    </div>
  </section>

  <!-- PRICING -->
  <section id="repairs" data-section="pricing" data-kind="pricing">
    <div class="repairs__card card on-olive marks">
      <div class="repairs__head">
        <h2 class="h2" data-split>Priced per room, not per seat</h2>
        <p class="lead">No setup fee, no per-message charges and no contract longer than a year. Everything below is per room, per month.</p>
        <figure class="repairs__photo print print--olive" data-parallax>
          <svg class="art" viewBox="0 0 500 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="The Ostler dashboard showing a week of conversations, resolution rate and extras sold">
            <rect width="500" height="400" fill="#5b6a45"/>
            <circle cx="420" cy="60" r="200" fill="#6c7b55" opacity=".6"/>
            <g transform="translate(28 36)">
              <rect width="444" height="328" rx="20" fill="#fbf9f4" filter="url(#sh)"/>
              <text x="22" y="36" font-size="16" font-weight="700" fill="#100c0d">This week</text>
              <text x="22" y="54" font-size="11.5" fill="#8a8284">The Harbour House · 38 rooms</text>
              <rect x="300" y="22" width="122" height="28" rx="14" fill="#f0ebe1"/>
              <rect x="302" y="24" width="58" height="24" rx="12" fill="#fff" filter="url(#sh2)"/>
              <text x="331" y="40" text-anchor="middle" font-size="11" font-weight="700" fill="#100c0d">Week</text>
              <text x="391" y="40" text-anchor="middle" font-size="11" font-weight="600" fill="#8a8284">Month</text>
              <g>
                <rect x="22" y="70" width="128" height="76" rx="14" fill="#f3eee4"/>
                <text x="36" y="92" font-size="10.5" fill="#6b6466">Conversations</text>
                <text x="36" y="122" class="d" font-size="25" font-weight="800" fill="#100c0d">1,284</text>
                <text x="36" y="138" font-size="10" font-weight="600" fill="#4f8c3c">▲ 12% vs last week</text>
                <rect x="158" y="70" width="128" height="76" rx="14" fill="#f3eee4"/>
                <text x="172" y="92" font-size="10.5" fill="#6b6466">Resolved by Ostler</text>
                <text x="172" y="122" class="d" font-size="25" font-weight="800" fill="#100c0d">87%</text>
                <text x="172" y="138" font-size="10" font-weight="600" fill="#4f8c3c">▲ 3 pts</text>
                <rect x="294" y="70" width="128" height="76" rx="14" fill="#100c0d"/>
                <text x="308" y="92" font-size="10.5" fill="#a39a9b">Extras sold</text>
                <text x="308" y="122" class="d" font-size="25" font-weight="800" fill="#f6efe3">£14,820</text>
                <text x="308" y="138" font-size="10" font-weight="600" fill="#9fd18b">▲ £2,310</text>
              </g>
              <g stroke="#ece6da"><path d="M30 176H414M30 216H414M30 256H414M30 296H414"/></g>
              <path d="M40 270 102 256 164 260 226 238 288 220 350 202 412 212V296H40Z" fill="url(#fadeR)"/>
              <path d="M40 270 102 256 164 260 226 238 288 220 350 202 412 212" fill="none" stroke="#a72d2d" stroke-width="2.6" stroke-linejoin="round" stroke-linecap="round"/>
              <path d="M40 290 102 288 164 291 226 286 288 284 350 280 412 283" fill="none" stroke="#5b6a45" stroke-width="2.2" stroke-dasharray="5 4" stroke-linecap="round"/>
              <circle cx="350" cy="202" r="5" fill="#a72d2d" stroke="#fff" stroke-width="2"/>
              <rect x="300" y="166" width="100" height="24" rx="8" fill="#100c0d"/>
              <text x="350" y="182" text-anchor="middle" font-size="10.5" font-weight="600" fill="#f6efe3">Sat · 241 chats</text>
              <g font-size="10" fill="#a39b9c" text-anchor="middle"><text x="40" y="316">Mon</text><text x="102" y="316">Tue</text><text x="164" y="316">Wed</text><text x="226" y="316">Thu</text><text x="288" y="316">Fri</text><text x="350" y="316">Sat</text><text x="412" y="316">Sun</text></g>
            </g>
          </svg>
        </figure>
      </div>
      <div class="repairs__list">
        <ul class="prices">
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Concierge</h3><p class="price__note">Unlimited guest conversations in 41 languages, on every channel</p><p class="price__cost" data-reveal="tag">£4<small>per room</small></p></li>
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Upsell</h3><p class="price__note">Upgrades, late checkout, add-ons and table bookings</p><p class="price__cost" data-reveal="tag">£1<small>per room</small></p></li>
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Rooms</h3><p class="price__note">Housekeeping and maintenance tickets from guest requests</p><p class="price__cost" data-reveal="tag">£1<small>per room</small></p></li>
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Reviews</h3><p class="price__note">Drafted replies on every major review site, approved by you</p><p class="price__cost" data-reveal="tag">50p<small>per room</small></p></li>
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Voice</h3><p class="price__note">Answers calls, with 300 minutes per room included</p><p class="price__cost" data-reveal="tag">£2<small>per room</small></p></li>
          <li class="price"><span class="price__rule" data-rule aria-hidden="true"></span><h3 class="price__name">Onboarding</h3><p class="price__note">Done with your team in fourteen days, one time only</p><p class="price__cost" data-reveal="tag">£0<small>always</small></p></li>
        </ul>
        <p class="repairs__foot"><span>Annual plans get two months free.</span><a class="link" href="#visit">Get a quote for your hotel</a></p>
      </div>
    </div>
  </section>

  <!-- STATEMENT -->
  <section id="again" data-section="statement" class="again" data-kind="statement">
    <div class="again__stage">
      <figure class="again__photo">
        <svg class="art" viewBox="0 0 1600 1000" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A boutique hotel at night, with a few windows still lit and the entrance glowing">
          <defs>
            <linearGradient id="aSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#0c1220"/><stop offset=".55" stop-color="#1e1b2e"/><stop offset="1" stop-color="#3a2427"/></linearGradient>
            <linearGradient id="aWall" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#2b2425"/><stop offset=".5" stop-color="#3a3031"/><stop offset="1" stop-color="#231d1e"/></linearGradient>
            <linearGradient id="aStreet" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#1a1416"/><stop offset="1" stop-color="#0b0809"/></linearGradient>
            <pattern id="aWin" x="320" y="160" width="120" height="130" patternUnits="userSpaceOnUse">
              <rect x="22" y="14" width="76" height="102" fill="#3e3536"/>
              <rect x="25" y="17" width="70" height="96" fill="#141011"/>
              <path d="M60 17V113M25 60H95" stroke="#2b2425" stroke-width="3"/>
              <rect x="18" y="114" width="84" height="6" fill="#4a4041"/>
            </pattern>
          </defs>
          <rect width="1600" height="1000" fill="url(#aSky)"/>
          <g fill="#f6efe3"><circle cx="140" cy="80" r="1.4"/><circle cx="260" cy="150" r="1"/><circle cx="420" cy="60" r="1.2"/><circle cx="1180" cy="70" r="1.4"/><circle cx="1320" cy="140" r="1"/><circle cx="1480" cy="60" r="1.2"/><circle cx="980" cy="40" r="1"/><circle cx="620" cy="30" r="1"/></g>
          <circle cx="1400" cy="120" r="34" fill="#f2ead8"/><circle cx="1400" cy="120" r="140" fill="url(#glowW)" opacity=".18"/>
          <rect x="0" y="300" width="330" height="600" fill="#161214"/>
          <rect x="1270" y="260" width="330" height="640" fill="#161214"/>
          <g fill="url(#lit)" opacity=".7"><rect x="60" y="360" width="50" height="70"/><rect x="200" y="520" width="50" height="70"/><rect x="1340" y="330" width="50" height="70"/><rect x="1470" y="480" width="50" height="70"/></g>
          <rect x="300" y="110" width="1000" height="790" fill="url(#aWall)"/>
          <rect x="290" y="100" width="1020" height="22" fill="#4a3f40"/>
          <rect x="300" y="122" width="1000" height="6" fill="#000" opacity=".3"/>
          <rect x="320" y="160" width="960" height="650" fill="url(#aWin)"/>
          <g>
            <rect x="465" y="177" width="70" height="96" fill="url(#lit)"/>
            <rect x="825" y="177" width="70" height="96" fill="url(#lit)"/>
            <rect x="345" y="307" width="70" height="96" fill="url(#lit)"/>
            <rect x="705" y="307" width="70" height="96" fill="url(#lit)"/>
            <rect x="1185" y="307" width="70" height="96" fill="url(#lit)"/>
            <rect x="585" y="437" width="70" height="96" fill="url(#lit)"/>
            <rect x="945" y="437" width="70" height="96" fill="url(#lit)"/>
            <rect x="465" y="567" width="70" height="96" fill="url(#lit)"/>
            <rect x="1065" y="567" width="70" height="96" fill="url(#lit)"/>
            <rect x="705" y="697" width="70" height="96" fill="url(#lit)"/>
            <rect x="1185" y="697" width="70" height="96" fill="url(#lit)"/>
          </g>
          <g fill="#7a2222" opacity=".55"><rect x="465" y="177" width="16" height="96"/><rect x="879" y="177" width="16" height="96"/><rect x="705" y="307" width="16" height="96"/><rect x="1239" y="307" width="16" height="96"/><rect x="585" y="437" width="16" height="96"/><rect x="999" y="437" width="16" height="96"/><rect x="465" y="567" width="16" height="96"/><rect x="1119" y="567" width="16" height="96"/></g>
          <g stroke="#2b2425" stroke-width="3"><path d="M500 177V273M465 220H535M860 177V273M825 220H895M380 307V403M345 350H415M740 307V403M705 350H775M1220 307V403M1185 350H1255M620 437V533M585 480H655M980 437V533M945 480H1015M500 567V663M465 610H535M1100 567V663M1065 610H1135M740 697V793M705 740H775M1220 697V793M1185 740H1255"/></g>
          <circle cx="400" cy="340" r="9" fill="#fff3d6"/>
          <g filter="url(#bl30)" fill="#f3a556" opacity=".35"><rect x="445" y="160" width="110" height="130"/><rect x="805" y="160" width="110" height="130"/><rect x="325" y="290" width="110" height="130"/><rect x="685" y="290" width="110" height="130"/><rect x="1165" y="290" width="110" height="130"/><rect x="565" y="420" width="110" height="130"/><rect x="925" y="420" width="110" height="130"/><rect x="445" y="550" width="110" height="130"/><rect x="1045" y="550" width="110" height="130"/><rect x="685" y="680" width="110" height="130"/><rect x="1165" y="680" width="110" height="130"/></g>
          <rect x="300" y="810" width="1000" height="90" fill="#1f1a1b"/>
          <rect x="720" y="790" width="160" height="110" fill="url(#lit)"/>
          <path d="M800 790V900" stroke="#3a2a1d" stroke-width="4"/>
          <rect x="640" y="770" width="320" height="34" rx="4" fill="#a72d2d"/>
          <path d="M640 804H960L940 816H660Z" fill="#7a2222"/>
          <text x="800" y="793" text-anchor="middle" class="d" font-size="18" font-weight="800" letter-spacing="3" fill="#f6efe3">THE HARBOUR HOUSE</text>
          <circle cx="800" cy="840" r="200" fill="url(#glowW)" opacity=".5"/>
          <g><rect x="604" y="820" width="10" height="80" fill="#2b2425"/><circle cx="609" cy="812" r="12" fill="#ffe2ad"/><circle cx="609" cy="812" r="80" fill="url(#glowW)" opacity=".7"/><rect x="986" y="820" width="10" height="80" fill="#2b2425"/><circle cx="991" cy="812" r="12" fill="#ffe2ad"/><circle cx="991" cy="812" r="80" fill="url(#glowW)" opacity=".7"/></g>
          <rect y="900" width="1600" height="100" fill="url(#aStreet)"/>
          <g filter="url(#bl14)" opacity=".45">
            <rect x="730" y="905" width="140" height="80" fill="#f3a556"/>
            <rect x="600" y="905" width="18" height="70" fill="#ffe2ad"/><rect x="982" y="905" width="18" height="70" fill="#ffe2ad"/>
            <rect x="470" y="910" width="60" height="50" fill="#f3a556" opacity=".5"/><rect x="1190" y="910" width="60" height="50" fill="#f3a556" opacity=".5"/>
          </g>
          <path d="M0 900H1600" stroke="#3a3031" stroke-width="3"/>
        </svg>
      </figure>
      <div class="again__knock"><p class="again__word display fill" style="--len:5" data-bounce="still">Awake</p></div>
      <div class="again__card card on-cream marks">
        <h2 class="again__title">Your front desk closes. Ostler doesn't.</h2>
        <p>Across our hotels, 58% of guest messages arrive when the desk is closed or short-handed. Answering in seconds instead of hours is the difference between a guest who books the spa and one who writes a review about waiting.</p>
        <a class="btn" href="#sell"><span>See how it works</span><svg class="btn__arrow" viewBox="0 0 28 12" aria-hidden="true"><path d="M0 6h26M21 1l5 5-5 5" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
      </div>
    </div>
  </section>

  <!-- HOW IT WORKS -->
  <section id="sell" data-section="process" class="sell" data-kind="process">
    <div class="sell__intro">
      <h2 class="h2" data-split>Live in fourteen days</h2>
      <p class="lead muted">No new hardware, no app for guests to download, and nothing for your team to learn beyond one shared inbox.</p>
      <a class="btn btn--solid" href="#visit"><span>Book a demo</span><svg class="btn__arrow" viewBox="0 0 28 12" aria-hidden="true"><path d="M0 6h26M21 1l5 5-5 5" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
    </div>
    <ol class="steps">
      <li class="step on-cream marks">
        <div class="step__text"><h3 class="step__title">Connect your systems</h3><p>We plug into your property management system, booking engine, POS and door locks. Read-only to start, if you'd rather.</p></div>
        <figure class="step__photo print print--cream">
          <svg class="art" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet" role="img" aria-label="Ostler connected to the hotel's property system, booking engine, point of sale and door locks">
            <rect width="600" height="400" fill="#e2dcce"/>
            <g fill="none" stroke="#a72d2d" stroke-width="2" stroke-dasharray="4 6" stroke-linecap="round">
              <path d="M200 68C262 68 250 150 262 168"><animate attributeName="stroke-dashoffset" from="0" to="-20" dur="1s" repeatCount="indefinite"/></path>
              <path d="M400 68C338 68 350 150 338 168"><animate attributeName="stroke-dashoffset" from="0" to="-20" dur="1s" repeatCount="indefinite"/></path>
              <path d="M200 332C262 332 250 250 262 232"><animate attributeName="stroke-dashoffset" from="0" to="-20" dur="1s" repeatCount="indefinite"/></path>
              <path d="M400 332C338 332 350 250 338 232"><animate attributeName="stroke-dashoffset" from="0" to="-20" dur="1s" repeatCount="indefinite"/></path>
            </g>
            <circle cx="300" cy="200" r="52" fill="none" stroke="#a72d2d" stroke-width="2"><animate attributeName="r" values="52;86" dur="2.4s" repeatCount="indefinite"/><animate attributeName="opacity" values=".7;0" dur="2.4s" repeatCount="indefinite"/></circle>
            <circle cx="300" cy="200" r="52" fill="#100c0d" filter="url(#sh)"/>
            <text x="300" y="215" text-anchor="middle" class="d" font-size="44" font-weight="900" fill="#e2dcce">O</text>
            <g font-size="13">
              <g transform="translate(30 40)"><rect width="172" height="58" rx="14" fill="#fff" filter="url(#sh2)"/><rect x="14" y="15" width="28" height="28" rx="8" fill="#2f4a6b"/><path d="M21 36V24h14v12M25 28h6M25 32h6" stroke="#fff" stroke-width="1.6" fill="none"/><text x="52" y="27" font-weight="700" fill="#100c0d">Property system</text><circle cx="56" cy="40" r="3.5" fill="#4f8c3c"/><text x="64" y="44" font-size="11" fill="#4f8c3c">Connected</text></g>
              <g transform="translate(398 40)"><rect width="172" height="58" rx="14" fill="#fff" filter="url(#sh2)"/><rect x="14" y="15" width="28" height="28" rx="8" fill="#a72d2d"/><rect x="20" y="22" width="16" height="14" rx="2" stroke="#fff" stroke-width="1.6" fill="none"/><path d="M20 26h16M24 20v4M32 20v4" stroke="#fff" stroke-width="1.6"/><text x="52" y="27" font-weight="700" fill="#100c0d">Booking engine</text><circle cx="56" cy="40" r="3.5" fill="#4f8c3c"/><text x="64" y="44" font-size="11" fill="#4f8c3c">Connected</text></g>
              <g transform="translate(30 304)"><rect width="172" height="58" rx="14" fill="#fff" filter="url(#sh2)"/><rect x="14" y="15" width="28" height="28" rx="8" fill="#5b6a45"/><rect x="20" y="21" width="16" height="16" rx="2" stroke="#fff" stroke-width="1.6" fill="none"/><path d="M20 26h16" stroke="#fff" stroke-width="1.6"/><text x="52" y="27" font-weight="700" fill="#100c0d">Point of sale</text><circle cx="56" cy="40" r="3.5" fill="#4f8c3c"/><text x="64" y="44" font-size="11" fill="#4f8c3c">Connected</text></g>
              <g transform="translate(398 304)"><rect width="172" height="58" rx="14" fill="#fff" filter="url(#sh2)"/><rect x="14" y="15" width="28" height="28" rx="8" fill="#d39b2a"/><rect x="21" y="27" width="14" height="10" rx="2" fill="#fff"/><path d="M24 27v-3a4 4 0 0 1 8 0v3" stroke="#fff" stroke-width="1.8" fill="none"/><text x="52" y="27" font-weight="700" fill="#100c0d">Door locks</text><circle cx="56" cy="40" r="3.5" fill="#d39b2a"><animate attributeName="opacity" values="1;.3;1" dur="1.4s" repeatCount="indefinite"/></circle><text x="64" y="44" font-size="11" fill="#9a6a10">Syncing 38 rooms…</text></g>
            </g>
          </svg>
        </figure>
      </li>
      <li class="step on-red marks">
        <div class="step__text"><h3 class="step__title">It learns your hotel</h3><p>We read your website, menus and house rules, then sit with your team for the answers that only live in their heads.</p></div>
        <figure class="step__photo print">
          <svg class="art" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet" role="img" aria-label="The hotel knowledge base, with learned facts and one question waiting for the team">
            <rect width="600" height="400" fill="#a72d2d"/>
            <circle cx="520" cy="60" r="220" fill="#c03b35" opacity=".5"/>
            <g transform="translate(60 30)">
              <rect width="480" height="340" rx="20" fill="#fbf9f4" filter="url(#sh)"/>
              <text x="24" y="40" font-size="16" font-weight="700" fill="#100c0d">Hotel knowledge</text>
              <text x="456" y="42" text-anchor="end" class="d" font-size="22" font-weight="800" fill="#a72d2d">312 facts</text>
              <rect x="24" y="56" width="432" height="6" rx="3" fill="#ece6da"/>
              <rect x="24" y="56" width="400" height="6" rx="3" fill="#a72d2d"/>
              <g font-size="13.5">
                <circle cx="36" cy="94" r="11" fill="#e3efdb"/><use href="#tick" x="27" y="85" width="18" height="18" color="#3f6b2a"/>
                <text x="56" y="92" font-weight="700" fill="#100c0d">Breakfast</text><text x="56" y="109" font-size="12" fill="#6b6466">07:00–10:30, until 11:00 at weekends</text>
                <circle cx="36" cy="142" r="11" fill="#e3efdb"/><use href="#tick" x="27" y="133" width="18" height="18" color="#3f6b2a"/>
                <text x="56" y="140" font-weight="700" fill="#100c0d">Parking</text><text x="56" y="157" font-size="12" fill="#6b6466">Six spaces, £18 a night, reserve before arrival</text>
                <circle cx="36" cy="190" r="11" fill="#e3efdb"/><use href="#tick" x="27" y="181" width="18" height="18" color="#3f6b2a"/>
                <text x="56" y="188" font-weight="700" fill="#100c0d">Pool</text><text x="56" y="205" font-size="12" fill="#6b6466">Heated to 28°C, open 07:00–21:00, towels poolside</text>
                <circle cx="36" cy="238" r="11" fill="#e3efdb"/><use href="#tick" x="27" y="229" width="18" height="18" color="#3f6b2a"/>
                <text x="56" y="236" font-weight="700" fill="#100c0d">Dogs</text><text x="56" y="253" font-size="12" fill="#6b6466">Welcome in ground-floor rooms, £25 per stay</text>
                <rect x="16" y="270" width="448" height="54" rx="12" fill="#fbf1de"/>
                <circle cx="36" cy="297" r="11" fill="#f6ead2" stroke="#d39b2a" stroke-width="1.5"/><text x="36" y="302" text-anchor="middle" font-size="13" font-weight="800" fill="#9a6a10">?</text>
                <text x="56" y="294" font-weight="700" fill="#100c0d">Resetting the boiler</text><text x="56" y="311" font-size="12" fill="#6b6466">Asked twice this month · only Callum knows</text>
                <rect x="354" y="285" width="98" height="24" rx="12" fill="#d39b2a"/><text x="403" y="301" text-anchor="middle" font-size="11" font-weight="700" fill="#100c0d">Needs answer</text>
              </g>
            </g>
          </svg>
        </figure>
      </li>
      <li class="step on-olive marks">
        <div class="step__text"><h3 class="step__title">Go live on every channel</h3><p>Switch on the channels you want. Anything Ostler isn't sure about goes straight to your team, with the whole conversation attached.</p></div>
        <figure class="step__photo print print--olive">
          <svg class="art" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet" role="img" aria-label="Channel settings with web chat, SMS, messaging apps and email switched on">
            <rect width="600" height="400" fill="#5b6a45"/>
            <circle cx="80" cy="340" r="220" fill="#4a5838"/>
            <g transform="translate(110 30)">
              <rect width="380" height="340" rx="20" fill="#fbf9f4" filter="url(#sh)"/>
              <text x="24" y="40" font-size="16" font-weight="700" fill="#100c0d">Channels</text>
              <rect x="300" y="24" width="56" height="24" rx="12" fill="#e3efdb"/><circle cx="315" cy="36" r="4" fill="#4f8c3c"/><text x="344" y="40" text-anchor="end" font-size="11" font-weight="700" fill="#3f6b2a">Live</text>
              <g font-size="14">
                <g transform="translate(0 64)"><path d="M24 0H356" stroke="#ece6da"/><circle cx="44" cy="30" r="16" fill="#f0ebe1"/><path d="M36 25h16v10h-9l-5 4v-4h-2Z" fill="#100c0d"/><text x="72" y="27" font-weight="700" fill="#100c0d">Web chat</text><text x="72" y="44" font-size="11.5" fill="#8a8284">On every page of your website</text><rect x="312" y="17" width="44" height="26" rx="13" fill="#5b6a45"/><circle cx="343" cy="30" r="10" fill="#fff"/></g>
                <g transform="translate(0 116)"><path d="M24 0H356" stroke="#ece6da"/><circle cx="44" cy="30" r="16" fill="#f0ebe1"/><rect x="38" y="20" width="12" height="20" rx="3" stroke="#100c0d" stroke-width="2" fill="none"/><text x="72" y="27" font-weight="700" fill="#100c0d">SMS</text><text x="72" y="44" font-size="11.5" fill="#8a8284">From your existing hotel number</text><rect x="312" y="17" width="44" height="26" rx="13" fill="#5b6a45"/><circle cx="343" cy="30" r="10" fill="#fff"/></g>
                <g transform="translate(0 168)"><path d="M24 0H356" stroke="#ece6da"/><circle cx="44" cy="30" r="16" fill="#f0ebe1"/><circle cx="44" cy="30" r="8" stroke="#100c0d" stroke-width="2" fill="none"/><path d="M38 37l-2 4 4-2" fill="#100c0d"/><text x="72" y="27" font-weight="700" fill="#100c0d">Messaging apps</text><text x="72" y="44" font-size="11.5" fill="#8a8284">Linked in about two minutes</text><rect x="312" y="17" width="44" height="26" rx="13" fill="#5b6a45"/><circle cx="343" cy="30" r="10" fill="#fff"/></g>
                <g transform="translate(0 220)"><path d="M24 0H356" stroke="#ece6da"/><circle cx="44" cy="30" r="16" fill="#f0ebe1"/><rect x="35" y="23" width="18" height="14" rx="2" stroke="#100c0d" stroke-width="2" fill="none"/><path d="M35 24l9 7 9-7" stroke="#100c0d" stroke-width="2" fill="none"/><text x="72" y="27" font-weight="700" fill="#100c0d">Email</text><text x="72" y="44" font-size="11.5" fill="#8a8284">reservations@ and info@ inboxes</text><rect x="312" y="17" width="44" height="26" rx="13" fill="#5b6a45"/><circle cx="343" cy="30" r="10" fill="#fff"/></g>
                <g transform="translate(0 272)"><path d="M24 0H356" stroke="#ece6da"/><circle cx="44" cy="30" r="16" fill="#f0ebe1"/><path d="M38 22c2-1 4 3 3 5l-1 1c1 3 3 5 6 6l1-1c2-1 6 1 5 3-1 3-4 4-7 3-5-2-9-6-10-11 0-3 1-5 3-6Z" fill="#100c0d"/><text x="72" y="27" font-weight="700" fill="#100c0d">Phone</text><rect x="118" y="15" width="40" height="17" rx="8.5" fill="#f6ead2"/><text x="138" y="27.5" text-anchor="middle" font-size="10" font-weight="700" fill="#9a6a10">Beta</text><text x="72" y="44" font-size="11.5" fill="#8a8284">After 11pm, or when the desk is busy</text><rect x="312" y="17" width="44" height="26" rx="13" fill="#d3cbb8"/><circle cx="325" cy="30" r="10" fill="#fff"/></g>
              </g>
            </g>
          </svg>
        </figure>
      </li>
      <li class="step on-cream marks">
        <div class="step__text"><h3 class="step__title">It gets better every night</h3><p>Every handoff becomes a new answer once your team approves it. Most hotels pass 90% resolution by week six.</p></div>
        <figure class="step__photo print print--cream">
          <svg class="art" viewBox="0 0 600 400" preserveAspectRatio="xMidYMid meet" role="img" aria-label="A chart of resolution rate climbing from 71% to 94% over eight weeks">
            <rect width="600" height="400" fill="#e2dcce"/>
            <g transform="translate(40 30)">
              <rect width="520" height="340" rx="20" fill="#fff" filter="url(#sh)"/>
              <text x="24" y="40" font-size="16" font-weight="700" fill="#100c0d">Resolved without staff</text>
              <text x="24" y="58" font-size="12" fill="#8a8284">First eight weeks · The Harbour House</text>
              <text x="496" y="52" text-anchor="end" class="d" font-size="40" font-weight="800" fill="#a72d2d">94%</text>
              <g stroke="#f1ece3"><path d="M70 300H496M70 250H496M70 200H496M70 150H496M70 100H496"/></g>
              <g font-size="10.5" fill="#a39b9c" text-anchor="end"><text x="58" y="304">60%</text><text x="58" y="254">70%</text><text x="58" y="204">80%</text><text x="58" y="154">90%</text><text x="58" y="104">100%</text></g>
              <path d="M70 245 130 220 190 200 250 180 310 165 370 150 430 140 490 130V300H70Z" fill="url(#fadeR)"/>
              <path d="M70 245 130 220 190 200 250 180 310 165 370 150 430 140 490 130" fill="none" stroke="#a72d2d" stroke-width="3" stroke-linejoin="round" stroke-linecap="round"/>
              <g fill="#fff" stroke="#a72d2d" stroke-width="2.2"><circle cx="70" cy="245" r="4.5"/><circle cx="130" cy="220" r="4.5"/><circle cx="190" cy="200" r="4.5"/><circle cx="250" cy="180" r="4.5"/><circle cx="310" cy="165" r="4.5"/><circle cx="370" cy="150" r="4.5"/><circle cx="430" cy="140" r="4.5"/></g>
              <circle cx="490" cy="130" r="7" fill="#a72d2d" stroke="#fff" stroke-width="2.5"/>
              <rect x="70" y="262" width="60" height="22" rx="11" fill="#100c0d"/><text x="100" y="277" text-anchor="middle" font-size="10.5" font-weight="600" fill="#f6efe3">Go-live</text>
              <rect x="270" y="110" width="150" height="26" rx="13" fill="#f6efe3" stroke="#e7e0d3"/><text x="345" y="127" text-anchor="middle" font-size="11" font-weight="600" fill="#5b6a45">+46 answers approved</text>
              <g font-size="10.5" fill="#a39b9c" text-anchor="middle"><text x="70" y="322">W1</text><text x="130" y="322">W2</text><text x="190" y="322">W3</text><text x="250" y="322">W4</text><text x="310" y="322">W5</text><text x="370" y="322">W6</text><text x="430" y="322">W7</text><text x="490" y="322">W8</text></g>
            </g>
          </svg>
        </figure>
      </li>
    </ol>
  </section>

  <!-- CHANGELOG -->
  <section id="drops" data-section="changelog" data-kind="events">
    <div class="drops__card card on-red marks">
      <div class="drops__head">
        <h2 class="h2" data-split>Shipped in October</h2>
        <p class="lead">We release every Thursday. Every hotel gets every feature, with no upgrade fees and no downtime.</p>
      </div>
      <ul class="drops__list">
        <li class="drop" data-reveal="wipe"><p class="drop__date"><span class="drop__day">01</span><span class="drop__month">Oct</span></p><div class="drop__body"><h3 class="drop__title">Voice in twelve languages</h3><p class="drop__text">The phone concierge now picks up in Spanish, Italian, Japanese and nine more.</p></div><p class="drop__tag">Live</p></li>
        <li class="drop" data-reveal="wipe"><p class="drop__date"><span class="drop__day">08</span><span class="drop__month">Oct</span></p><div class="drop__body"><h3 class="drop__title">Allergen-aware dining</h3><p class="drop__text">Room service and table bookings check the guest's dietary notes before confirming.</p></div><p class="drop__tag">Live</p></li>
        <li class="drop" data-reveal="wipe"><p class="drop__date"><span class="drop__day">15</span><span class="drop__month">Oct</span></p><div class="drop__body"><h3 class="drop__title">Group bookings</h3><p class="drop__text">Wedding and conference blocks, with one thread per guest and one for the organiser.</p></div><p class="drop__tag">Live</p></li>
        <li class="drop" data-reveal="wipe"><p class="drop__date"><span class="drop__day">22</span><span class="drop__month">Oct</span></p><div class="drop__body"><h3 class="drop__title">Shift handover notes</h3><p class="drop__text">A morning summary of everything that happened overnight, waiting for the day team.</p></div><p class="drop__tag">Live</p></li>
        <li class="drop" data-reveal="wipe"><p class="drop__date"><span class="drop__day">29</span><span class="drop__month">Oct</span></p><div class="drop__body"><h3 class="drop__title">Arrival-day upgrades</h3><p class="drop__text">Room upgrades offered on the morning of arrival, priced from live availability.</p></div><p class="drop__tag drop__tag--soon">Next Thursday</p></li>
      </ul>
    </div>
  </section>

  <!-- TESTIMONIALS -->
  <section id="voices" data-section="voices" data-kind="reviews">
    <div class="voices__card card on-olive marks">
      <h2 class="h2 voices__title" data-split>Heard at the front desk</h2>
      <div class="voices__row">
        <ul class="voices__list">
          <li class="voice"><blockquote><p>Our night porter used to spend half his shift on the phone. Now he's at the door when guests arrive.</p></blockquote><p class="voice__who">Elena R.<span>General Manager, Casa do Rio · 42 rooms</span></p></li>
          <li class="voice"><blockquote><p>It sold £11,000 of late checkouts in the first quarter. Nobody on my team ever wanted to ask for that money.</p></blockquote><p class="voice__who">James O.<span>Owner, Saltings · 24 rooms</span></p></li>
          <li class="voice"><blockquote><p>A guest asked in Korean at 3am whether the sauna was mixed. The answer was right, polite and in Korean.</p></blockquote><p class="voice__who">Marta K.<span>Operations Director, Hotel Lindqvist</span></p></li>
          <li class="voice"><blockquote><p>The handover note is the first thing I read every morning, before my email.</p></blockquote><p class="voice__who">Tom B.<span>Front Office Manager, The Wren</span></p></li>
          <li class="voice"><blockquote><p>We tried two chatbots before. This is the first one guests thank by name.</p></blockquote><p class="voice__who">Priya S.<span>General Manager, Fernhill · 61 rooms</span></p></li>
          <li class="voice"><blockquote><p>Setup took eleven days. Most of that was me finding the boiler manual.</p></blockquote><p class="voice__who">Callum D.<span>Owner, Kiln House · 9 rooms</span></p></li>
        </ul>
      </div>
    </div>
  </section>

  <!-- HOTELS GALLERY -->
  <section id="lookbook" data-section="gallery" class="lookbook" data-kind="gallery">
    <div class="lookbook__stage" data-fixed="6">
      <figure class="shot shot--a" data-speed="0.12">
        <svg class="art" viewBox="0 0 300 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A hotel bedroom lit by a bedside lamp">
          <defs>
            <linearGradient id="bWall" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#7a4632"/><stop offset="1" stop-color="#2e1912"/></linearGradient>
            <linearGradient id="bHead" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#6c7b55"/><stop offset="1" stop-color="#46532f"/></linearGradient>
          </defs>
          <rect width="300" height="400" fill="url(#bWall)"/>
          <circle cx="40" cy="210" r="190" fill="url(#glowW)" opacity=".75"/>
          <rect x="112" y="60" width="96" height="70" fill="#e9dfcd"/><rect x="118" y="66" width="84" height="58" fill="#a72d2d"/><path d="M118 110Q150 80 202 100V124H118Z" fill="#d39b2a"/><circle cx="180" cy="84" r="8" fill="#f6efe3"/>
          <rect x="44" y="150" width="232" height="130" rx="14" fill="url(#bHead)"/>
          <g stroke="#3e4a2f" stroke-width="2" opacity=".6"><path d="M90 156V276M136 156V276M182 156V276M228 156V276"/></g>
          <path d="M20 400V270Q160 250 300 270V400Z" fill="url(#linen)"/>
          <rect x="70" y="232" width="92" height="44" rx="18" fill="#fbf8f2"/><rect x="170" y="232" width="92" height="44" rx="18" fill="#efe8dc"/>
          <path d="M70 266Q116 278 162 266M170 266Q216 278 262 266" stroke="#d9d0bf" stroke-width="2" fill="none"/>
          <path d="M20 318Q160 300 300 318V350Q160 334 20 350Z" fill="#a72d2d"/>
          <path d="M20 330Q160 312 300 330" stroke="#7a2222" stroke-width="2" fill="none"/>
          <rect x="-10" y="268" width="56" height="80" fill="url(#wood)"/>
          <path d="M8 212H38L46 244H0Z" fill="#ffe6bb"/>
          <rect x="20" y="244" width="6" height="24" fill="#c79a3e"/>
          <ellipse cx="23" cy="268" rx="12" ry="3" fill="#8f6a22"/>
          <rect y="370" width="300" height="30" fill="#000" opacity=".2"/>
        </svg>
        <figcaption>The Harbour House · Bristol</figcaption>
      </figure>
      <figure class="shot shot--b" data-speed="0.4">
        <svg class="art" viewBox="0 0 320 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A rooftop pool at dusk">
          <defs>
            <linearGradient id="pSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3e2d55"/><stop offset=".5" stop-color="#c46a5a"/><stop offset="1" stop-color="#f7b267"/></linearGradient>
            <linearGradient id="pWater" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#4fb3c4"/><stop offset="1" stop-color="#145868"/></linearGradient>
          </defs>
          <rect width="320" height="240" fill="url(#pSky)"/>
          <circle cx="200" cy="200" r="26" fill="#ffe0a6"/><circle cx="200" cy="200" r="110" fill="url(#glowW)" opacity=".6"/>
          <path d="M0 214H24V196H40V206H62V182H80V214H110V200H130V214H170V190H186V214H240V176H256V198H280V214H320V240H0Z" fill="#2a1d2a"/>
          <rect y="236" width="320" height="164" fill="#d9cdb8"/>
          <path d="M30 262H290L320 340H0Z" fill="url(#pWater)"/>
          <path d="M30 262H290L292 268H28Z" fill="#fff" opacity=".5"/>
          <path d="M184 274h32M176 290h48M188 306h24M170 322h56" stroke="#ffd59a" stroke-width="3" stroke-linecap="round" opacity=".75"/>
          <path d="M50 284q20-6 40 0M240 300q20-6 40 0M90 320q20-6 40 0" stroke="#fff" stroke-opacity=".35" stroke-width="2" fill="none"/>
          <path d="M10 356H100L112 372H22Z" fill="#f6efe3"/><path d="M14 372H24V386M100 372H110V386" stroke="#8a8284" stroke-width="3"/>
          <path d="M150 356H240L252 372H162Z" fill="#f6efe3"/><path d="M154 372H164V386M240 372H250V386" stroke="#8a8284" stroke-width="3"/>
          <path d="M120 300L60 344H180Z" fill="#a72d2d"/><path d="M120 300V390" stroke="#3a2a1d" stroke-width="3"/>
          <rect x="196" y="346" width="14" height="10" rx="2" fill="#d39b2a"/>
        </svg>
        <figcaption>Casa do Rio · Porto</figcaption>
      </figure>
      <figure class="shot shot--c" data-speed="0.25">
        <svg class="art" viewBox="0 0 300 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A hotel lobby with a tall arched window and a chandelier">
          <defs>
            <linearGradient id="lWall" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3e4a2f"/><stop offset="1" stop-color="#1f2618"/></linearGradient>
            <linearGradient id="lWin" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffeac2"/><stop offset="1" stop-color="#e8a860"/></linearGradient>
            <pattern id="lFloor" width="40" height="40" patternUnits="userSpaceOnUse"><rect width="40" height="40" fill="#e9dfcd"/><rect width="20" height="20" fill="#2b2425"/><rect x="20" y="20" width="20" height="20" fill="#2b2425"/></pattern>
          </defs>
          <rect width="300" height="400" fill="url(#lWall)"/>
          <path d="M90 300V130a60 60 0 0 1 120 0V300Z" fill="url(#lWin)"/>
          <path d="M150 70V300M90 180H210M90 240H210" stroke="#3e4a2f" stroke-width="4"/>
          <path d="M90 300V130a60 60 0 0 1 120 0V300" fill="none" stroke="#2a3220" stroke-width="8"/>
          <circle cx="150" cy="200" r="180" fill="url(#glowW)" opacity=".35"/>
          <path d="M150 0V40" stroke="#c79a3e" stroke-width="2"/>
          <path d="M110 48Q150 70 190 48" stroke="url(#brass)" stroke-width="4" fill="none"/>
          <g fill="#fff3d6"><circle cx="110" cy="46" r="5"/><circle cx="130" cy="56" r="5"/><circle cx="150" cy="60" r="5"/><circle cx="170" cy="56" r="5"/><circle cx="190" cy="46" r="5"/></g>
          <circle cx="150" cy="52" r="70" fill="url(#glowW)" opacity=".7"/>
          <path d="M0 330H300V400H0Z" fill="url(#lFloor)" transform="matrix(1 0 0 1 0 0)"/>
          <path d="M0 330H300V400H0Z" fill="#000" opacity=".25"/>
          <path d="M40 330C40 300 260 300 260 330V372H40Z" fill="url(#wood)"/>
          <path d="M34 326C40 296 260 296 266 326" stroke="url(#brass)" stroke-width="5" fill="none"/>
          <ellipse cx="200" cy="309" rx="10" ry="3" fill="#8f6a22"/><path d="M191 309a9 9 0 0 1 18 0Z" fill="url(#brass)"/><circle cx="200" cy="299" r="2" fill="#c79a3e"/>
          <path d="M262 330C250 290 270 260 284 250M270 330C276 300 296 286 300 284" stroke="#5b6a45" stroke-width="6" fill="none" stroke-linecap="round"/>
          <ellipse cx="282" cy="250" rx="14" ry="8" fill="#6c7b55"/>
        </svg>
        <figcaption>Hotel Lindqvist · Stockholm</figcaption>
      </figure>
      <figure class="shot shot--d" data-speed="0.55">
        <svg class="art" viewBox="0 0 300 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A candlelit dinner table for two">
          <defs>
            <radialGradient id="dCloth" cx=".5" cy=".4" r=".7"><stop offset="0" stop-color="#fbf8f2"/><stop offset="1" stop-color="#bfb5a2"/></radialGradient>
            <linearGradient id="dWine" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#8f1f2a"/><stop offset="1" stop-color="#4a0d14"/></linearGradient>
          </defs>
          <rect width="300" height="400" fill="#1a1112"/>
          <circle cx="150" cy="190" r="200" fill="url(#glowW)" opacity=".45"/>
          <ellipse cx="150" cy="290" rx="190" ry="120" fill="url(#dCloth)"/>
          <ellipse cx="90" cy="300" rx="48" ry="22" fill="#fff" stroke="#d9d0bf" stroke-width="2"/><ellipse cx="90" cy="298" rx="30" ry="13" fill="#f3eee4"/>
          <path d="M76 296q8-8 18-2 10-6 16 2-10 8-34 0Z" fill="#a72d2d"/><circle cx="96" cy="292" r="4" fill="#5b6a45"/>
          <ellipse cx="210" cy="262" rx="44" ry="19" fill="#fff" stroke="#d9d0bf" stroke-width="2"/><ellipse cx="210" cy="260" rx="27" ry="11" fill="#f3eee4"/>
          <path d="M198 258q10-6 22 0-10 6-22 0Z" fill="#d39b2a"/>
          <path d="M34 300l4 30M146 300l-4 30M160 260l6 26M258 262l-4 24" stroke="#c9c1b0" stroke-width="3" stroke-linecap="round"/>
          <g><path d="M120 200h22q2 30-11 34-13-4-11-34Z" fill="#fff" fill-opacity=".25" stroke="#fff" stroke-opacity=".6"/><path d="M121 214h20q0 16-10 18-10-2-10-18Z" fill="url(#dWine)"/><path d="M131 234V264" stroke="#fff" stroke-opacity=".6" stroke-width="2"/><ellipse cx="131" cy="265" rx="10" ry="3" fill="#fff" fill-opacity=".4"/></g>
          <g><path d="M166 180h20q2 26-10 30-12-4-10-30Z" fill="#fff" fill-opacity=".25" stroke="#fff" stroke-opacity=".6"/><path d="M167 192h18q0 14-9 16-9-2-9-16Z" fill="url(#dWine)"/><path d="M176 210V238" stroke="#fff" stroke-opacity=".6" stroke-width="2"/><ellipse cx="176" cy="239" rx="9" ry="3" fill="#fff" fill-opacity=".4"/></g>
          <rect x="146" y="236" width="12" height="40" rx="2" fill="#f6efe3"/>
          <path d="M152 236q-6-10 0-20 6 10 0 20Z" fill="#ffd28a"/><path d="M152 234q-3-5 0-10 3 5 0 10Z" fill="#fff6e0"/>
          <circle cx="152" cy="226" r="60" fill="url(#glowW)" opacity=".8"/>
        </svg>
        <figcaption>Saltings · Whitstable</figcaption>
      </figure>
      <figure class="shot shot--e" data-speed="0.3">
        <svg class="art" viewBox="0 0 320 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A hotel spa with candles, stacked stones and folded towels">
          <defs>
            <linearGradient id="eSlat" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#8a5a3a"/><stop offset=".5" stop-color="#a87148"/><stop offset="1" stop-color="#7a4c30"/></linearGradient>
            <radialGradient id="eStone" cx=".4" cy=".35" r=".7"><stop offset="0" stop-color="#9a958d"/><stop offset="1" stop-color="#4a4642"/></radialGradient>
          </defs>
          <rect width="320" height="400" fill="#3a2418"/>
          <g fill="url(#eSlat)"><rect x="0" width="34" height="280"/><rect x="40" width="34" height="280"/><rect x="80" width="34" height="280"/><rect x="120" width="34" height="280"/><rect x="160" width="34" height="280"/><rect x="200" width="34" height="280"/><rect x="240" width="34" height="280"/><rect x="280" width="34" height="280"/></g>
          <rect width="320" height="280" fill="#1a0e08" opacity=".35"/>
          <rect y="280" width="320" height="120" fill="#e9dfcd"/>
          <rect y="280" width="320" height="8" fill="#000" opacity=".15"/>
          <g filter="url(#bl14)" fill="#fff" opacity=".22"><ellipse cx="90" cy="150" rx="40" ry="70"/><ellipse cx="230" cy="110" rx="30" ry="60"/></g>
          <ellipse cx="96" cy="332" rx="58" ry="16" fill="url(#eStone)"/><ellipse cx="96" cy="306" rx="44" ry="14" fill="url(#eStone)"/><ellipse cx="96" cy="284" rx="32" ry="12" fill="url(#eStone)"/><ellipse cx="96" cy="266" rx="20" ry="9" fill="url(#eStone)"/>
          <g><rect x="190" y="300" width="110" height="20" rx="8" fill="#f6efe3"/><rect x="194" y="318" width="110" height="20" rx="8" fill="#e9dfcd"/><rect x="186" y="336" width="110" height="20" rx="8" fill="#f6efe3"/><path d="M200 310h80M204 328h80M196 346h80" stroke="#d9d0bf" stroke-width="2"/></g>
          <g>
            <rect x="166" y="342" width="18" height="24" rx="3" fill="#f6efe3"/><path d="M175 342q-4-8 0-14 4 6 0 14Z" fill="#ffd28a"/><circle cx="175" cy="334" r="40" fill="url(#glowW)" opacity=".8"/>
            <rect x="24" y="352" width="16" height="20" rx="3" fill="#f6efe3"/><path d="M32 352q-4-7 0-12 4 5 0 12Z" fill="#ffd28a"/><circle cx="32" cy="345" r="34" fill="url(#glowW)" opacity=".8"/>
            <rect x="140" y="270" width="14" height="16" rx="3" fill="#f6efe3"/><path d="M147 270q-3-6 0-10 3 4 0 10Z" fill="#ffd28a"/><circle cx="147" cy="265" r="30" fill="url(#glowW)" opacity=".8"/>
          </g>
        </svg>
        <figcaption>Fernhill · Lake District</figcaption>
      </figure>
      <figure class="shot shot--f" data-speed="0.18">
        <svg class="art" viewBox="0 0 500 400" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A seaside hotel at golden hour">
          <defs>
            <linearGradient id="fSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f2c38a"/><stop offset="1" stop-color="#f6e2bf"/></linearGradient>
            <linearGradient id="fSea" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#5a86a0"/><stop offset="1" stop-color="#2a4a62"/></linearGradient>
            <linearGradient id="fWall" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#f6efe3"/><stop offset="1" stop-color="#d9cdb8"/></linearGradient>
          </defs>
          <rect width="500" height="230" fill="url(#fSky)"/>
          <circle cx="120" cy="180" r="34" fill="#fff1d0"/><circle cx="120" cy="180" r="150" fill="url(#glowW)" opacity=".6"/>
          <rect y="210" width="500" height="80" fill="url(#fSea)"/>
          <path d="M80 220h80M70 236h100M90 252h60M100 268h40" stroke="#ffe2ad" stroke-width="3" stroke-linecap="round" opacity=".7"/>
          <rect y="286" width="500" height="114" fill="#e6d3ad"/>
          <rect x="250" y="80" width="250" height="250" fill="url(#fWall)"/>
          <rect x="244" y="72" width="262" height="12" fill="#c9bca2"/>
          <g fill="#5b6a45"><rect x="270" y="110" width="12" height="40"/><rect x="314" y="110" width="12" height="40"/><rect x="340" y="110" width="12" height="40"/><rect x="384" y="110" width="12" height="40"/><rect x="410" y="110" width="12" height="40"/><rect x="454" y="110" width="12" height="40"/><rect x="270" y="180" width="12" height="40"/><rect x="314" y="180" width="12" height="40"/><rect x="340" y="180" width="12" height="40"/><rect x="384" y="180" width="12" height="40"/><rect x="410" y="180" width="12" height="40"/><rect x="454" y="180" width="12" height="40"/></g>
          <g fill="#2a3a4a"><rect x="282" y="110" width="32" height="40"/><rect x="352" y="110" width="32" height="40"/><rect x="422" y="110" width="32" height="40"/><rect x="282" y="180" width="32" height="40"/><rect x="352" y="180" width="32" height="40"/><rect x="422" y="180" width="32" height="40"/></g>
          <rect x="352" y="180" width="32" height="40" fill="url(#lit)"/>
          <path d="M250 250H500V268H250Z" fill="#a72d2d"/>
          <path d="M250 268q15 10 31 0 15 10 31 0 15 10 31 0 15 10 31 0 15 10 31 0 15 10 31 0 15 10 31 0 15 10 32 0Z" fill="#a72d2d"/>
          <rect x="250" y="282" width="250" height="48" fill="#2b2425"/>
          <g><path d="M60 330L30 312H90Z" fill="#f6efe3"/><path d="M60 312V360" stroke="#5a4a3a" stroke-width="3"/><path d="M160 336L128 316H192Z" fill="#a72d2d"/><path d="M160 316V366" stroke="#5a4a3a" stroke-width="3"/></g>
        </svg>
        <figcaption>The Wren · Falmouth</figcaption>
      </figure>
    </div>
    <div class="lookbook__center">
      <div class="lookbook__wordbox fillbox"><h2 class="lookbook__word display fill" style="--len:10" data-bounce="drop">Checked in</h2></div>
      <p class="lookbook__text">A few of the 212 hotels running Ostler tonight, from nine-room guesthouses to three-hundred-key resorts.</p>
      <a class="link lookbook__link" href="#voices">Hear from their teams</a>
    </div>
  </section>

  <!-- FAQ -->
  <section id="faq" data-section="faq" data-kind="faq">
    <div class="faq__card card on-cream marks">
      <div class="faq__head">
        <h2 class="h2" data-split>Asked in every demo</h2>
        <p class="muted">Anything else? Ask us on a call, or write and a person will answer within one working day.</p>
      </div>
      <div class="faq__list">
        <details class="qa" data-reveal="up"><summary><span class="qa__q">Does it replace my front desk team?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>No. It takes the repetitive questions so your team has time for the guests standing in front of them. Anything sensitive, unusual or upset goes to a person, with the full conversation attached.</p></div></details>
        <details class="qa" data-reveal="up"><summary><span class="qa__q">What happens when it doesn't know?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>It says so, tells the guest someone will reply shortly, and hands the thread to your team. Ostler only answers from your hotel's approved knowledge, never from guesswork.</p></div></details>
        <details class="qa" data-reveal="up"><summary><span class="qa__q">Which systems do you connect to?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>Most widely used property management systems, booking engines, POS platforms and door-lock providers. If yours isn't covered yet, we build the connector during onboarding at no extra cost.</p></div></details>
        <details class="qa" data-reveal="up"><summary><span class="qa__q">Where is guest data stored?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>In the EU, encrypted at rest and in transit. We sign a data processing agreement with every hotel and never use your guests' data to train models for anyone else.</p></div></details>
        <details class="qa" data-reveal="up"><summary><span class="qa__q">How long does setup take?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>Fourteen days on average, from signing to the first guest conversation. Expect about four hours of your team's time across that fortnight.</p></div></details>
        <details class="qa" data-reveal="up"><summary><span class="qa__q">Can we cancel?</span><span class="qa__icon" aria-hidden="true"></span></summary><div class="qa__a"><p>Monthly plans cancel with thirty days' notice. You keep a full export of every conversation, and your knowledge base, either way.</p></div></details>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="visit" data-section="contact" data-kind="contact">
    <div class="visit__card card on-red marks">
      <div class="visit__wordbox fillbox"><h2 class="visit__word display fill" style="--len:10" data-bounce="drop">Talk to us</h2></div>
      <div class="visit__grid">
        <div class="visit__info">
          <p class="lead">Thirty minutes over video, with your own hotel's questions answered live. Or visit us at Studio 3, Kiln Lane 14, Bristol.</p>
          <dl class="hours">
            <div><dt>Sales</dt><dd>Mon – Fri, 08:00 – 18:00</dd></div>
            <div><dt>Hotel support</dt><dd>24 / 7, every day</dd></div>
            <div><dt>First reply</dt><dd>Under 4 minutes</dd></div>
            <div><dt>Onboarding</dt><dd>14 days</dd></div>
          </dl>
          <p class="visit__links"><a class="link" href="mailto:hello@ostler.example">hello@ostler.example</a><a class="link" href="tel:+441174960123">0117 496 0123</a><a class="link" href="#visit">LinkedIn</a></p>
        </div>
        <figure class="visit__photo" data-parallax>
          <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A hotel reception desk at night with a brass bell, key boxes and a tablet running Ostler">
            <defs>
              <linearGradient id="vWall" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#5a1a1a"/><stop offset="1" stop-color="#2a0c0c"/></linearGradient>
              <linearGradient id="vTop" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3a2a22"/><stop offset="1" stop-color="#1e1410"/></linearGradient>
              <pattern id="vKeys" x="40" y="50" width="64" height="58" patternUnits="userSpaceOnUse"><rect x="2" y="2" width="60" height="54" fill="#3a1414"/><rect x="2" y="2" width="60" height="54" fill="none" stroke="#c79a3e" stroke-opacity=".5" stroke-width="2"/></pattern>
            </defs>
            <rect width="400" height="500" fill="url(#vWall)"/>
            <circle cx="70" cy="290" r="220" fill="url(#glowW)" opacity=".45"/>
            <rect x="40" y="50" width="320" height="174" fill="url(#vKeys)"/>
            <g fill="url(#brass)"><g transform="translate(64 66)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g><g transform="translate(192 66)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g><g transform="translate(320 66)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g><g transform="translate(128 124)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g><g transform="translate(256 182)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g><g transform="translate(64 182)"><circle r="5"/><rect x="-2" y="4" width="4" height="22"/><rect x="2" y="18" width="5" height="3"/><rect x="-9" y="26" width="18" height="14" rx="3" fill="#a72d2d"/></g></g>
            <g transform="translate(206 248)">
              <path d="M10 92L0 120H120L110 92Z" fill="#1a1415"/>
              <rect x="0" y="0" width="120" height="92" rx="10" fill="#120d0e"/>
              <rect x="6" y="6" width="108" height="80" rx="6" fill="#f6f2ea"/>
              <rect x="6" y="6" width="108" height="16" rx="6" fill="#a72d2d"/>
              <text x="14" y="18" font-size="8" font-weight="700" fill="#f6efe3">Ostler · Desk</text>
              <rect x="14" y="28" width="64" height="12" rx="6" fill="#e7e0d3"/><rect x="42" y="44" width="64" height="12" rx="6" fill="#a72d2d"/><rect x="14" y="60" width="78" height="12" rx="6" fill="#e7e0d3"/>
              <circle cx="60" cy="46" r="90" fill="#fff" opacity=".04"/>
            </g>
            <rect x="0" y="350" width="400" height="20" fill="url(#vTop)"/>
            <rect x="0" y="348" width="400" height="4" fill="url(#brass)"/>
            <rect x="0" y="370" width="400" height="130" fill="url(#wood)"/>
            <g stroke="#2a160e" stroke-width="2" opacity=".6"><path d="M40 370V500M100 370V500M160 370V500M220 370V500M280 370V500M340 370V500"/></g>
            <g transform="translate(110 316)">
              <ellipse cx="0" cy="34" rx="34" ry="7" fill="#000" opacity=".35"/>
              <ellipse cx="0" cy="30" rx="30" ry="6" fill="#5a3f14"/>
              <path d="M-28 30a28 26 0 0 1 56 0Z" fill="url(#brass)"/>
              <path d="M-18 16a20 18 0 0 1 14-10" stroke="#fff6dc" stroke-width="3" fill="none" stroke-linecap="round" opacity=".8"/>
              <rect x="-3" y="-4" width="6" height="8" fill="#8f6a22"/><circle cx="0" cy="-6" r="5" fill="url(#brass)"/>
            </g>
            <g><path d="M326 350V316l-8-18h28l-8 18v34Z" fill="#2b2425"/><path d="M312 298h44l-8-30h-28Z" fill="#ffe6bb"/><circle cx="334" cy="290" r="90" fill="url(#glowW)" opacity=".55"/></g>
          </svg>
        </figure>
        <form class="visit__form" data-sent="Thanks — we'll be in touch within one working day.">
          <h3 class="h3">Book a 30-minute demo</h3>
          <label class="field"><span>Your name</span><input name="name" autocomplete="name" required></label>
          <div class="field-row">
            <label class="field"><span>Hotel</span><input name="hotel" autocomplete="organization" required></label>
            <label class="field"><span>Rooms</span><input name="rooms" type="number" min="1" inputmode="numeric"></label>
          </div>
          <label class="field"><span>Work email</span><input type="email" name="email" autocomplete="email" required></label>
          <label class="field"><span>What would you hand over first?</span><textarea name="message" rows="2"></textarea></label>
          <button class="btn btn--solid" type="submit"><span>Request a demo</span><svg class="btn__arrow" viewBox="0 0 28 12" aria-hidden="true"><path d="M0 6h26M21 1l5 5-5 5" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></button>
          <p class="visit__status" role="status" aria-live="polite"></p>
        </form>
      </div>
    </div>
  </section>
</main>

<footer class="foot" data-section="footer">
  <a class="foot__brand" href="#hero">Ostler</a>
  <nav class="foot__nav" aria-label="Footer">
    <a class="link" href="#rails">Product</a>
    <a class="link" href="#repairs">Pricing</a>
    <a class="link" href="#sell">How it works</a>
    <a class="link" href="#faq">Questions</a>
    <a class="link" href="#visit">Contact</a>
  </nav>
  <p class="foot__small"><span>© 2026 Ostler · a fictional brand; every hotel and figure is illustrative</span><span>Made for hotels that still answer the phone.</span></p>
</footer>

<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js"></script>
<script>(()=>{const root=document.documentElement;const init=(sel,fn)=>document.querySelectorAll(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});let lenis=null;
const bar=document.querySelector('.progress');if(bar){let tick=false;const upd=()=>{const max=document.documentElement.scrollHeight-innerHeight;bar.style.transform='scaleX('+(max>0?Math.min(1,scrollY/max):0)+')';tick=false};addEventListener('scroll',()=>{if(!tick){tick=true;requestAnimationFrame(upd)}},{passive:true});upd()}
init('.hdr',hdr=>{const btn=hdr.querySelector('.hdr__menu');if(!btn)return;const set=open=>{hdr.classList.toggle('is-open',open);btn.setAttribute('aria-expanded',String(open));const label=open?btn.dataset.close:btn.dataset.open;if(label)btn.setAttribute('aria-label',label)};btn.addEventListener('click',()=>set(!hdr.classList.contains('is-open')));hdr.querySelectorAll('.hdr__nav a').forEach(a=>a.addEventListener('click',()=>set(false)));document.addEventListener('keydown',e=>{if(e.key==='Escape')set(false)})});
document.addEventListener('click',e=>{const a=e.target.closest('a[href^="#"]');if(!a||!lenis)return;const id=a.getAttribute('href');const t=id.length>1?document.getElementById(id.slice(1)):null;if(!t)return;e.preventDefault();lenis.scrollTo(t,{offset:-8,duration:1.4})});
init('.visit__form',form=>{const status=form.querySelector('.visit__status');form.addEventListener('submit',e=>{e.preventDefault();if(status)status.textContent=form.dataset.sent||'';form.reset()})});
if(!root.classList.contains('motion')||!window.gsap||!window.ScrollTrigger)return;gsap.registerPlugin(ScrollTrigger);ScrollTrigger.config({autoRefreshEvents:'visibilitychange,DOMContentLoaded,resize'});const hasSplit=!!window.SplitText;if(hasSplit)gsap.registerPlugin(SplitText);const small=()=>innerWidth<700;const rnd=i=>{const x=Math.sin(i*91.7+13.1)*43758.5453;return x-Math.floor(x)};const stance=k=>({rotation:i=>(rnd(i)-0.5)*16*k,yPercent:i=>(rnd(i+11)-0.5)*14*k});const fonts=document.fonts?document.fonts.ready:Promise.resolve();const queue=[];let running=false;const step=()=>{const job=queue.shift();if(job){try{job()}catch(e){console.error(e)}}if(queue.length)setTimeout(step,0);else running=false};const enqueue=fn=>{queue.push(fn);if(!running){running=true;setTimeout(step,0)}};const each=(sel,fn)=>document.querySelectorAll(sel).forEach(el=>enqueue(()=>fn(el)));const near=(el,fn)=>{const o=new IntersectionObserver(es=>{if(es.some(e=>e.isIntersecting)){o.disconnect();enqueue(fn)}},{rootMargin:'0px 0px 120% 0px'});o.observe(el)};const onEnter=(els,play)=>{const o=new IntersectionObserver(es=>{const hits=es.filter(e=>e.isIntersecting).map(e=>e.target);if(!hits.length)return;hits.forEach(t=>o.unobserve(t));play(hits)},{rootMargin:'0px 0px -12% 0px'});els.forEach(el=>o.observe(el))};const whileVisible=(el,anim)=>{anim.pause();new IntersectionObserver(es=>es.forEach(e=>e.isIntersecting?anim.resume():anim.pause())).observe(el)};
enqueue(()=>{if(!window.Lenis)return;lenis=new Lenis({lerp:0.11});lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0)});
const prep=sec=>{const q=s=>[...sec.querySelectorAll(s)];const ups=q('[data-reveal="up"]');if(ups.length){gsap.set(ups,{y:44,opacity:0});onEnter(ups,hits=>gsap.to(hits,{y:0,opacity:1,duration:1,ease:'power3.out',stagger:0.09,clearProps:'transform'}))}const tags=q('[data-reveal="tag"]');if(tags.length){gsap.set(tags,{scale:0.4,rotation:-14,opacity:0,transformOrigin:'70% 50%'});onEnter(tags,hits=>gsap.to(hits,{scale:1,rotation:0,opacity:1,duration:0.8,ease:'back.out(2.4)',stagger:0.08}))}const wipes=q('[data-reveal="wipe"]');if(wipes.length){gsap.set(wipes,{clipPath:'inset(0% 100% 0% 0%)'});onEnter(wipes,hits=>gsap.to(hits,{clipPath:'inset(0% 0% 0% 0%)',duration:1,ease:'power3.inOut',stagger:0.1,clearProps:'clipPath'}))}const rules=q('[data-rule]');if(rules.length){gsap.set(rules,{scaleX:0,transformOrigin:'0 50%'});onEnter(rules,hits=>gsap.to(hits,{scaleX:1,duration:1.1,ease:'power3.inOut',stagger:0.08}))}q('[data-reveal="drop"]').forEach(el=>{const r=gsap.getProperty(el,'rotation')||0;gsap.set(el,{yPercent:-18,rotation:r+9,scale:1.08,opacity:0});onEnter([el],()=>gsap.to(el,{yPercent:0,rotation:r,scale:1,opacity:1,duration:1.2,ease:'back.out(1.6)'}))});q('[data-parallax]').forEach(el=>{const art=el.querySelector('.art');if(art)gsap.fromTo(art,{yPercent:-7,scale:1.16},{yPercent:7,scale:1.16,ease:'none',scrollTrigger:{trigger:el,start:'top bottom',end:'bottom top',scrub:true}})});const groups=new Map;q('[data-speed]').forEach(el=>{const p=el.parentElement||el;if(!groups.has(p))groups.set(p,[]);groups.get(p).push(el)});groups.forEach((els,p)=>{const tl=gsap.timeline({scrollTrigger:{trigger:p,start:'top bottom',end:'bottom top',scrub:true}});els.forEach(el=>tl.to(el,{yPercent:-(parseFloat(el.dataset.speed)||0)*100,ease:'none'},0))});if(!hasSplit)return;q('[data-split]').forEach(el=>fonts.then(()=>enqueue(()=>{const split=SplitText.create(el,{type:'words'});gsap.set(split.words,{yPercent:80,rotation:i=>(rnd(i+4)-0.5)*26,opacity:0});onEnter([el],()=>gsap.to(split.words,{yPercent:0,rotation:0,opacity:1,duration:0.95,ease:'back.out(2.2)',stagger:0.045}))})));q('[data-bounce]').forEach(el=>fonts.then(()=>enqueue(()=>{const split=SplitText.create(el,{type:'chars',charsClass:'ch'});if(el.dataset.bounce!=='drop'){gsap.set(split.chars,stance(1));return}gsap.set(split.chars,{yPercent:-150,rotation:i=>(rnd(i+3)-0.5)*80,opacity:0});onEnter([el],()=>gsap.to(split.chars,{...stance(1),opacity:1,duration:1.3,ease:'elastic.out(1, 0.55)',stagger:{each:0.06,from:'random'}}))})))};
each('.hero',hero=>{const card=hero.querySelector('.hero__card'),word=hero.querySelector('.hero__word'),clip=hero.querySelector('.hero__wordclip');const photo=hero.querySelector('.hero__photo'),img=photo&&photo.querySelector('.art');const text=hero.querySelectorAll('.hero__info, .hero__side');if(!card)return;if(img)whileVisible(hero,gsap.fromTo(img,{scale:1},{scale:1.045,duration:9,ease:'sine.inOut',yoyo:true,repeat:-1}));const tl=gsap.timeline({scrollTrigger:{trigger:hero,start:'top top',end:'bottom bottom',scrub:0.8}});tl.to(card,{scale:small()?0.9:0.86,rotation:-2.5,yPercent:2,ease:'power1.in'},0);if(img)tl.to(img,{yPercent:6,ease:'none'},0);if(text.length)tl.to(text,{yPercent:-40,opacity:0,ease:'power1.in',stagger:0.05},0);if(clip)tl.to(clip,{clipPath:'inset(-300% -30% -200% -30%)',ease:'none',duration:0.15},0);if(!word||!hasSplit)return;fonts.then(()=>enqueue(()=>{const split=SplitText.create(word,{type:'chars',charsClass:'hero__ch'});const inner=split.chars.map(c=>{const s=document.createElement('span');s.className='hero__chi';s.style.display='inline-block';while(c.firstChild)s.append(c.firstChild);c.append(s);return s});gsap.to(inner,{...stance(1),duration:1.5,ease:'elastic.out(1, 0.45)',stagger:0.07,delay:0.1});const rock=gsap.to(inner,{rotation:i=>(rnd(i)-0.5)*16+(rnd(i+5)>0.5?3:-3),duration:2.4,ease:'sine.inOut',yoyo:true,repeat:-1,stagger:{each:0.4},delay:1.9,paused:true});whileVisible(hero,rock);tl.to(split.chars,{yPercent:i=>-(120+rnd(i+2)*190),xPercent:i=>(rnd(i+8)-0.5)*60,rotation:i=>(rnd(i+1)-0.5)*70,ease:'power2.in',stagger:0.03},0)}))});
each('.rails',sec=>{const pin=sec.querySelector('.rails__pin'),track=sec.querySelector('.rails__track');if(!pin||!track)return;const dist=()=>Math.max(0,track.scrollWidth-innerWidth);const size=()=>sec.style.setProperty('--run',dist()+'px');size();ScrollTrigger.addEventListener('refreshInit',size);const move=gsap.to(track,{x:()=>-dist(),ease:'none',scrollTrigger:{trigger:sec,start:'top top',end:'bottom bottom',scrub:0.6,invalidateOnRefresh:true}});near(sec,()=>sec.querySelectorAll('.cover').forEach((c,i)=>enqueue(()=>{const dir=i%2?-1:1,w=c.querySelector('.cover__word'),img=c.querySelector('.cover__photo .art');const tl=gsap.timeline({scrollTrigger:{trigger:c,containerAnimation:move,start:'left right',end:'right left',scrub:true}});tl.fromTo(c,{rotation:5*dir,yPercent:4},{rotation:-4*dir,yPercent:-3,ease:'none'},0);if(w)tl.fromTo(w,{xPercent:9},{xPercent:-9,ease:'none'},0);if(img)tl.fromTo(img,{xPercent:-5},{xPercent:5,ease:'none'},0)})))});
each('.again',sec=>{const stage=sec.querySelector('.again__stage'),knock=sec.querySelector('.again__knock'),word=sec.querySelector('.again__word');const img=sec.querySelector('.again__photo .art'),card=sec.querySelector('.again__card');if(!stage||!knock)return;const origin=()=>word?word.offsetLeft+word.offsetWidth/2+'px '+(word.offsetTop+word.offsetHeight*0.55)+'px':'50% 50%';const tl=gsap.timeline({scrollTrigger:{trigger:sec,start:'top top',end:'bottom bottom',scrub:0.8,invalidateOnRefresh:true}});tl.fromTo(knock,{scale:1,transformOrigin:origin},{scale:9,ease:'power2.in',duration:1},0.12).to(knock,{opacity:0,ease:'none',duration:0.35},0.75);if(img)tl.fromTo(img,{scale:1.3},{scale:1,ease:'none',duration:1.1},0);if(card)tl.fromTo(card,{yPercent:135,rotation:5},{yPercent:0,rotation:0,ease:'back.out(1.3)',duration:0.45},1.05)});
enqueue(()=>document.querySelectorAll('main > *').forEach(sec=>near(sec,()=>prep(sec))));
enqueue(()=>document.querySelectorAll('.sell').forEach(sec=>near(sec,()=>{const steps=gsap.utils.toArray(sec.querySelectorAll('.step'));steps.forEach((s,i)=>{const next=steps[i+1];if(!next)return;gsap.to(s,{scale:0.92,rotation:i%2?2.2:-2.2,yPercent:-2,ease:'none',scrollTrigger:{trigger:next,start:'top bottom',end:()=>'top '+(parseFloat(getComputedStyle(next).top)||100)+'px',scrub:true,invalidateOnRefresh:true}})})})));
enqueue(()=>document.querySelectorAll('.voices__row').forEach(row=>near(row,()=>{const list=row.querySelector('.voices__list');if(!list||!list.children.length)return;[...list.children].forEach(li=>{const c=li.cloneNode(true);c.setAttribute('aria-hidden','true');c.querySelectorAll('a, button').forEach(x=>x.setAttribute('tabindex','-1'));list.append(c)});const run=gsap.to(list,{xPercent:-50,duration:list.children.length*4.5,ease:'none',repeat:-1,paused:true});const hold=()=>gsap.to(run,{timeScale:0,duration:0.5}),go=()=>gsap.to(run,{timeScale:1,duration:0.5});row.addEventListener('mouseenter',hold);row.addEventListener('mouseleave',go);row.addEventListener('focusin',hold);row.addEventListener('focusout',go);whileVisible(row,run)})));
if(document.fonts&&document.fonts.status!=='loaded')fonts.then(()=>enqueue(()=>ScrollTrigger.refresh()))})();</script>
</body>
</html>
```

