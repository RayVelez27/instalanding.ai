INSTALANDING.AI · Mirai AI Companion Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Mirai AI Companion Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/mirai-ai-companion-page

mirai-ai-companion.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Mirai AI Companion Page
  slug     mirai-ai-companion-page
  prompt   https://instalanding.ai/p/mirai-ai-companion-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/mirai-ai-companion-page
  license  MIT. Fictional product; every name, figure, price and quote is invented. Replace them before shipping.

  MAP
  tokens    :root at the top of <style>: purple #b914f0 with a deep #8814ad, three charcoal inks (#1f2525, #182020,
            #2a3232), one mint accent #66ddc6, muted text, a hairline, a 22px radius and the --wrap width; fonts Sora
            300-800 and JetBrains Mono for labels.
  sections  nav, hero, ticker, features, stats, how-it-works, demo, pricing, faq, waitlist, footer
  scripts   one inline script, no libraries: the hero is one SVG (a Rive scene redrawn by hand) with a character rig run
            every frame: eyes follow the pointer, idle glances, blinks, a near state (brows up, pupils wider) and an
            annoyed state when she is poked (lids half down, brows flat, a head shake), breathing sway, and layered
            parallax by data-depth; an intro where clouds rise, the wordmark lifts and she slides up; viewBox reframing
            on phones. Plus the nav, the ticker clone, reveals, counters, feature filter tabs, a looping chat demo
            with typing dots, the monthly / yearly price toggle and the waitlist form.
  assets    none: the character, clouds, bubbles and art are inline SVG and CSS gradients; fonts from Google Fonts

  ADAPTING
  - The rig reads the face centre from CX / CY (the character's translate) plus the face offset; move the character
    and update both, or the eyes track the wrong point.
  - Each .lyr has a data-depth: positive layers move against the pointer, negative ones with it.
  - Under 760px the stage reframes its viewBox and scales the wordmark; the copy moves into .mobile-intro blocks.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mirai — Your AI Companion</title>
<meta name="description" content="Mirai is an AI companion that listens, remembers what matters and keeps your conversations private.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Sora:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<style>
:root{
  --purple:#b914f0;
  --purple-deep:#8814ad;
  --purple-ink:#4a0a63;
  --ink:#1f2525;
  --ink-2:#182020;
  --ink-3:#2a3232;
  --line:rgba(255,255,255,.09);
  --mint:#66ddc6;
  --mint-deep:#1fa88f;
  --white:#ffffff;
  --muted:#a7b2b0;
  --radius:22px;
  --wrap:min(1180px, calc(100% - 32px));
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;-webkit-text-size-adjust:100%}
body{font-family:'Sora',system-ui,sans-serif;background:var(--ink);color:var(--white);overflow-x:hidden;-webkit-font-smoothing:antialiased}
a{color:inherit;text-decoration:none}
button{font:inherit;cursor:pointer;border:0;background:none;color:inherit}
img,svg{display:block}
::selection{background:var(--mint);color:var(--ink)}
.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap}

/* ───────────── NAV ───────────── */
.nav{position:fixed;inset:0 0 auto 0;z-index:50;transition:background .35s,backdrop-filter .35s,box-shadow .35s}
.nav-in{width:min(70.3vw,1380px);margin:0 auto;height:96px;display:flex;align-items:center;justify-content:space-between;transition:height .35s}
.nav.scrolled{background:rgba(24,32,32,.72);backdrop-filter:blur(16px) saturate(1.3);-webkit-backdrop-filter:blur(16px) saturate(1.3);box-shadow:0 1px 0 var(--line)}
.nav.scrolled .nav-in{height:72px}
.logo{font-weight:700;font-size:clamp(20px,1.72vw,33px);letter-spacing:.01em}
.links{display:flex;gap:clamp(18px,1.95vw,38px);font-size:clamp(13px,1.17vw,22px);font-weight:400}
.links a{position:relative;opacity:.95;transition:opacity .2s}
.links a:hover{opacity:1}
.links a.active{font-weight:600}
.links a.active::after{content:"";position:absolute;left:50%;bottom:-12px;width:6px;height:6px;margin-left:-3px;border-radius:50%;background:var(--mint)}
.links a:not(.active)::before{content:"";position:absolute;left:0;right:0;bottom:-6px;height:2px;background:var(--mint);transform:scaleX(0);transform-origin:left;transition:transform .3s}
.links a:not(.active):hover::before{transform:scaleX(1)}
.pill{background:var(--white);color:#111;font-weight:600;font-size:clamp(13px,1.1vw,21px);padding:.55em 2.3em;border-radius:999px;transition:transform .25s,box-shadow .25s,background .25s;white-space:nowrap}
.pill:hover{transform:translateY(-2px);box-shadow:0 10px 30px -8px rgba(102,221,198,.65);background:var(--mint)}
.burger{display:none;width:44px;height:44px;border-radius:12px;align-items:center;justify-content:center}
.burger span{display:block;width:20px;height:2px;background:#fff;position:relative}
.burger span::before,.burger span::after{content:"";position:absolute;left:0;width:20px;height:2px;background:#fff;transition:transform .3s}
.burger span::before{top:-6px}.burger span::after{top:6px}
.nav.open .burger span{background:transparent}
.nav.open .burger span::before{transform:translateY(6px) rotate(45deg)}
.nav.open .burger span::after{transform:translateY(-6px) rotate(-45deg)}

/* ───────────── HERO ───────────── */
.hero{position:relative;height:100vh;height:100svh;min-height:600px;background:var(--purple);overflow:hidden;isolation:isolate}
.stage{position:absolute;inset:0;width:100%;height:100%}
.stage text{font-family:'Sora',sans-serif}
.mobile-intro{display:none}
.lyr{transition:transform .6s cubic-bezier(.2,.7,.2,1)}
/* intro */
.intro .clouds-l{animation:riseL 1.4s cubic-bezier(.2,.8,.2,1) both}
.intro .clouds-r{animation:riseR 1.4s cubic-bezier(.2,.8,.2,1) both .05s}
.intro .blobs{animation:fadeScale 1.6s ease both}
.intro .word tspan,.intro .word{animation:wordIn 1.1s cubic-bezier(.2,.8,.2,1) both .35s}
.intro .char-wrap{animation:charUp 1.3s cubic-bezier(.2,1.2,.3,1) both .55s}
.intro .bub{animation:pop .7s cubic-bezier(.3,1.6,.5,1) both}
.intro .copy{animation:fadeUp 1s ease both 1s}
@keyframes riseL{from{transform:translate(-120px,260px)}to{transform:none}}
@keyframes riseR{from{transform:translate(120px,260px)}to{transform:none}}
@keyframes fadeScale{from{opacity:0;transform:scale(1.08)}to{opacity:1;transform:none}}
@keyframes wordIn{from{opacity:0;transform:translateY(80px)}to{opacity:1;transform:none}}
@keyframes charUp{from{transform:translateY(520px)}to{transform:none}}
@keyframes pop{from{transform:scale(0)}to{transform:scale(1)}}
@keyframes fadeUp{from{opacity:0;transform:translateY(24px)}to{opacity:1;transform:none}}
.word{transform-box:fill-box;transform-origin:center}
.bub{transform-box:fill-box;transform-origin:center}
.float{animation:floaty var(--d,6s) ease-in-out infinite alternate;transform-box:fill-box;transform-origin:center}
@keyframes floaty{0%{transform:translate(0,0)}100%{transform:translate(var(--fx,6px),var(--fy,-14px))}}
.cloud-drift{animation:drift 14s ease-in-out infinite alternate}
.cloud-drift.b{animation-duration:18s;animation-direction:alternate-reverse}
@keyframes drift{from{transform:translateX(-10px)}to{transform:translateX(12px)}}
#char{cursor:pointer}
.scroll-cue{position:absolute;left:50%;bottom:22px;transform:translateX(-50%);z-index:3;display:flex;flex-direction:column;align-items:center;gap:8px;font:500 11px/1 'JetBrains Mono',monospace;letter-spacing:.2em;text-transform:uppercase;color:rgba(255,255,255,.55)}
.scroll-cue i{width:22px;height:34px;border:1.5px solid rgba(255,255,255,.4);border-radius:12px;position:relative}
.scroll-cue i::after{content:"";position:absolute;left:50%;top:7px;width:3px;height:7px;margin-left:-1.5px;border-radius:2px;background:var(--mint);animation:wheel 1.8s ease-in-out infinite}
@keyframes wheel{0%{opacity:0;transform:translateY(-3px)}40%{opacity:1}100%{opacity:0;transform:translateY(10px)}}
.hint{position:absolute;right:clamp(16px,4vw,60px);bottom:26px;z-index:3;font:500 11px/1.4 'JetBrains Mono',monospace;color:rgba(255,255,255,.45);letter-spacing:.08em;text-align:right}

/* ───────────── COMMON ───────────── */
section{position:relative}
.wrap{width:var(--wrap);margin:0 auto}
.eyebrow{display:inline-flex;align-items:center;gap:10px;font:600 12px/1 'JetBrains Mono',monospace;letter-spacing:.18em;text-transform:uppercase;color:var(--mint)}
.eyebrow::before{content:"";width:8px;height:8px;border-radius:50%;background:var(--mint);box-shadow:0 0 0 4px rgba(102,221,198,.18)}
h2{font-size:clamp(34px,5.2vw,72px);line-height:1.02;font-weight:700;letter-spacing:-.035em;margin:18px 0 0}
h2 em{font-style:normal;color:var(--mint)}
.lede{color:var(--muted);font-size:clamp(15px,1.25vw,18px);line-height:1.65;max-width:560px;margin-top:18px;font-weight:300}
.reveal{opacity:0;transform:translateY(40px);transition:opacity 1s ease,transform 1s cubic-bezier(.2,.7,.2,1)}
.reveal.in{opacity:1;transform:none}
.btn{display:inline-flex;align-items:center;gap:10px;padding:16px 26px;border-radius:999px;font-weight:600;font-size:15px;transition:transform .25s,box-shadow .25s,background .25s,color .25s}
.btn-mint{background:var(--mint);color:var(--ink)}
.btn-mint:hover{transform:translateY(-2px);box-shadow:0 16px 40px -12px rgba(102,221,198,.7)}
.btn-ghost{border:1px solid rgba(255,255,255,.2)}
.btn-ghost:hover{background:#fff;color:var(--ink)}
.btn svg{width:18px;height:18px}

/* ticker */
.ticker{background:var(--ink);padding:26px 0 30px;border-bottom:1px solid var(--line);overflow:hidden}
.track{display:flex;gap:56px;width:max-content;animation:tick 38s linear infinite}
.ticker:hover .track{animation-play-state:paused}
.track span{display:flex;align-items:center;gap:56px;font-size:clamp(22px,2.6vw,38px);font-weight:700;letter-spacing:-.02em;white-space:nowrap;color:transparent;-webkit-text-stroke:1.2px rgba(255,255,255,.55)}
.track span:nth-child(3n+1){color:#fff;-webkit-text-stroke:0}
.track span::after{content:"";width:14px;height:14px;border-radius:50%;background:var(--mint)}
@keyframes tick{to{transform:translateX(-50%)}}

/* featured */
.featured{padding:clamp(80px,11vw,150px) 0 60px}
.sec-head{display:flex;justify-content:space-between;align-items:flex-end;gap:32px;flex-wrap:wrap}
.tabs{display:flex;gap:6px;padding:6px;border:1px solid var(--line);border-radius:999px;background:var(--ink-2)}
.tabs button{padding:10px 18px;border-radius:999px;font-size:13px;font-weight:500;color:var(--muted);transition:.25s}
.tabs button.on{background:#fff;color:var(--ink)}
.grid{display:grid;grid-template-columns:repeat(12,1fr);gap:20px;margin-top:56px}
.card{grid-column:span 4;border-radius:var(--radius);background:var(--ink-2);border:1px solid var(--line);overflow:hidden;transition:transform .5s cubic-bezier(.2,.7,.2,1),border-color .3s,opacity .4s;position:relative}
.card.big{grid-column:span 8;grid-row:span 2}
.card:hover{transform:translateY(-6px);border-color:rgba(102,221,198,.35)}
.card.hide{display:none}
.thumb{position:relative;aspect-ratio:16/10;overflow:hidden}
.card.big .thumb{aspect-ratio:auto;height:calc(100% - 190px);min-height:300px}
.thumb .art{position:absolute;inset:0;transition:transform .8s cubic-bezier(.2,.7,.2,1)}
.card:hover .art{transform:scale(1.06)}
.thumb .glyph{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-weight:800;letter-spacing:-.06em;color:rgba(255,255,255,.94);font-size:clamp(60px,9vw,130px);text-shadow:0 10px 40px rgba(0,0,0,.25)}
.card.big .glyph{font-size:clamp(90px,15vw,240px)}
.badge{position:absolute;left:16px;top:16px;font:600 11px/1 'JetBrains Mono',monospace;letter-spacing:.12em;text-transform:uppercase;background:rgba(10,14,14,.55);backdrop-filter:blur(8px);padding:8px 10px;border-radius:8px}
.badge.prem{background:var(--mint);color:var(--ink)}
.dur{position:absolute;right:14px;bottom:14px;font:600 12px/1 'JetBrains Mono',monospace;background:rgba(10,14,14,.7);padding:6px 8px;border-radius:6px}
.play{position:absolute;left:50%;top:50%;width:72px;height:72px;margin:-36px 0 0 -36px;border-radius:50%;background:rgba(255,255,255,.95);display:flex;align-items:center;justify-content:center;transform:scale(.6);opacity:0;transition:.35s cubic-bezier(.3,1.5,.5,1)}
.card:hover .play{transform:scale(1);opacity:1}
.play svg{width:24px;height:24px;margin-left:4px;fill:var(--ink)}
.card-body{padding:22px 22px 24px}
.meta{display:flex;gap:12px;font:500 12px/1 'JetBrains Mono',monospace;color:var(--muted);letter-spacing:.04em}
.meta b{color:var(--mint);font-weight:600}
.card h3{font-size:clamp(17px,1.45vw,21px);line-height:1.3;font-weight:600;letter-spacing:-.015em;margin-top:12px}
.card.big h3{font-size:clamp(22px,2.3vw,32px)}

/* stats */
.stats{padding:60px 0 clamp(80px,10vw,140px)}
.stat-row{display:grid;grid-template-columns:repeat(4,1fr);border-top:1px solid var(--line);border-bottom:1px solid var(--line)}
.stat{padding:42px 28px;border-left:1px solid var(--line)}
.stat:first-child{border-left:0;padding-left:0}
.stat .n{font-size:clamp(40px,5.4vw,78px);font-weight:700;letter-spacing:-.05em;line-height:1}
.stat .n sup{font-size:.45em;color:var(--mint);margin-left:4px;vertical-align:top;position:relative;top:.25em}
.stat p{color:var(--muted);font-size:14px;margin-top:12px;font-weight:300}

/* series */
.series{padding:clamp(80px,10vw,140px) 0;background:var(--purple);overflow:hidden;color:#fff}
.series::before{content:"";position:absolute;width:900px;height:900px;border-radius:50%;background:var(--purple-deep);right:-380px;top:-420px}
.series::after{content:"";position:absolute;width:520px;height:520px;border-radius:50%;background:var(--purple-deep);left:-260px;bottom:-280px}
.series .wrap{position:relative;z-index:1}
.series .eyebrow{color:#fff}
.series .eyebrow::before{background:var(--mint)}
.series .lede{color:rgba(255,255,255,.78)}
.s-list{margin-top:60px;border-top:1px solid rgba(255,255,255,.22)}
.s-item{display:grid;grid-template-columns:90px 1.2fr 1fr 60px;align-items:center;gap:24px;padding:30px 0;border-bottom:1px solid rgba(255,255,255,.22);position:relative;transition:padding .4s}
.s-item::before{content:"";position:absolute;inset:0 -24px;background:var(--ink);border-radius:20px;transform:scaleY(0);transition:transform .45s cubic-bezier(.2,.7,.2,1);z-index:-1}
.s-item:hover::before{transform:scaleY(1)}
.s-item:hover{padding-left:20px;padding-right:20px}
.s-num{font:600 14px/1 'JetBrains Mono',monospace;color:var(--mint)}
.s-item h3{font-size:clamp(24px,3.2vw,44px);font-weight:700;letter-spacing:-.035em}
.s-item p{font-size:15px;line-height:1.55;color:rgba(255,255,255,.8);font-weight:300}
.s-arrow{width:56px;height:56px;border-radius:50%;border:1px solid rgba(255,255,255,.35);display:flex;align-items:center;justify-content:center;transition:.35s}
.s-item:hover .s-arrow{background:var(--mint);border-color:var(--mint);transform:rotate(-45deg)}
.s-item:hover .s-arrow svg{stroke:var(--ink)}
.s-arrow svg{width:20px;height:20px;stroke:#fff;fill:none;stroke-width:2}

/* studio / about */
.studio{padding:clamp(80px,11vw,160px) 0}
.studio-grid{display:grid;grid-template-columns:1.05fr 1fr;gap:clamp(40px,6vw,90px);align-items:center}
.checks{list-style:none;margin-top:32px;display:grid;gap:16px}
.checks li{display:flex;gap:14px;align-items:flex-start;font-size:16px;line-height:1.5;color:#dfe7e5;font-weight:300}
.checks li b{font-weight:600;color:#fff}
.checks svg{flex:none;width:24px;height:24px;margin-top:1px}

/* pricing */
.pricing{padding:clamp(80px,10vw,140px) 0;background:var(--ink-2);border-top:1px solid var(--line)}
.center{text-align:center}
.center .lede{margin-left:auto;margin-right:auto}
.toggle{display:inline-flex;margin-top:34px;padding:6px;border-radius:999px;border:1px solid var(--line);background:var(--ink);position:relative}
.toggle button{position:relative;z-index:1;padding:10px 22px;font-size:14px;font-weight:500;color:var(--muted);transition:color .3s}
.toggle button.on{color:var(--ink)}
.toggle .knob{position:absolute;top:6px;bottom:6px;left:6px;border-radius:999px;background:#fff;transition:transform .4s cubic-bezier(.3,1.3,.5,1),width .4s}
.save{font:600 10px 'JetBrains Mono',monospace;background:var(--mint);color:var(--ink);padding:3px 6px;border-radius:5px;margin-left:6px;letter-spacing:.06em}
.plans{display:grid;grid-template-columns:repeat(3,1fr);gap:20px;margin-top:56px;align-items:stretch}
.plan{border-radius:28px;padding:34px 30px 32px;background:var(--ink);border:1px solid var(--line);display:flex;flex-direction:column;position:relative;overflow:hidden;transition:transform .4s}
.plan:hover{transform:translateY(-6px)}
.plan.hot{background:var(--purple);border-color:transparent;box-shadow:0 40px 100px -30px rgba(185,20,240,.6)}
.plan.hot::before{content:"";position:absolute;width:360px;height:360px;border-radius:50%;background:var(--purple-deep);right:-150px;top:-170px}
.plan.hot::after{content:"";position:absolute;width:70px;height:70px;border-radius:50%;background:var(--mint);right:30px;top:24px;box-shadow:-46px 40px 0 -22px var(--mint),20px 70px 0 -28px var(--mint)}
.plan>*{position:relative;z-index:1}
.plan .tag{font:600 12px 'JetBrains Mono',monospace;letter-spacing:.16em;text-transform:uppercase;color:var(--mint)}
.plan.hot .tag{color:#fff}
.plan h3{font-size:28px;font-weight:700;letter-spacing:-.03em;margin-top:14px}
.price{display:flex;align-items:baseline;gap:6px;margin:26px 0 6px}
.price b{font-size:64px;font-weight:700;letter-spacing:-.06em;line-height:1}
.price span{color:var(--muted);font-size:15px}
.plan.hot .price span,.plan.hot .sub,.plan.hot li{color:rgba(255,255,255,.88)}
.sub{color:var(--muted);font-size:14px;min-height:22px}
.plan ul{list-style:none;margin:28px 0 32px;display:grid;gap:13px;flex:1}
.plan li{display:flex;gap:12px;font-size:15px;color:#d2dcda;font-weight:300;line-height:1.45}
.plan li::before{content:"";flex:none;width:18px;height:18px;margin-top:2px;border-radius:50%;background:rgba(102,221,198,.16) url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='%2366ddc6' stroke-width='3.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M6 12.5l4 4 8-9'/%3E%3C/svg%3E") center/11px no-repeat}
.plan.hot li::before{background-color:rgba(255,255,255,.2);background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='white' stroke-width='3.5' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpath d='M6 12.5l4 4 8-9'/%3E%3C/svg%3E")}
.plan .btn{justify-content:center;width:100%}
.plan.hot .btn-mint{background:#fff}
.plan.hot .btn-mint:hover{background:var(--mint)}

/* faq */
.faq{padding:clamp(80px,10vw,140px) 0}
.faq-grid{display:grid;grid-template-columns:.8fr 1.2fr;gap:clamp(40px,6vw,90px)}
details{border-bottom:1px solid var(--line)}
details:first-child{border-top:1px solid var(--line)}
summary{list-style:none;cursor:pointer;display:flex;justify-content:space-between;align-items:center;gap:20px;padding:26px 0;font-size:clamp(17px,1.5vw,21px);font-weight:500;letter-spacing:-.01em}
summary::-webkit-details-marker{display:none}
summary i{flex:none;width:36px;height:36px;border-radius:50%;border:1px solid rgba(255,255,255,.2);position:relative;transition:.35s}
summary i::before,summary i::after{content:"";position:absolute;left:50%;top:50%;width:12px;height:1.5px;margin:-.75px 0 0 -6px;background:#fff;transition:.35s}
summary i::after{transform:rotate(90deg)}
details[open] summary i{background:var(--mint);border-color:var(--mint);transform:rotate(180deg)}
details[open] summary i::before,details[open] summary i::after{background:var(--ink)}
details[open] summary i::after{transform:rotate(0)}
details p{color:var(--muted);line-height:1.7;padding:0 60px 26px 0;font-weight:300;font-size:15.5px}

/* newsletter cta */
.cta{padding:0 0 clamp(60px,8vw,110px)}
.cta-box{position:relative;border-radius:36px;background:var(--purple);overflow:hidden;padding:clamp(48px,7vw,100px) clamp(24px,6vw,90px);isolation:isolate}
.cta-box svg.bg{position:absolute;inset:0;width:100%;height:100%;z-index:-1}
.cta-box h2{max-width:760px}
.cta-box .lede{color:rgba(255,255,255,.82)}
.form{display:flex;gap:10px;margin-top:36px;max-width:560px;background:rgba(31,37,37,.9);padding:8px;border-radius:999px;border:1px solid rgba(255,255,255,.12)}
.form input{flex:1;min-width:0;background:none;border:0;outline:0;color:#fff;font:400 16px 'Sora',sans-serif;padding:0 18px}
.form input::placeholder{color:#8a9896}
.form .btn{padding:14px 22px}
.form-note{font:500 12px 'JetBrains Mono',monospace;color:rgba(255,255,255,.7);margin-top:16px;letter-spacing:.04em;min-height:18px}

/* footer */
footer{border-top:1px solid var(--line);padding:70px 0 34px}
.f-top{display:grid;grid-template-columns:1.4fr repeat(3,1fr);gap:40px}
.f-top h4{font:600 12px 'JetBrains Mono',monospace;letter-spacing:.16em;text-transform:uppercase;color:var(--muted);margin-bottom:18px}
.f-top a{display:block;color:#dfe7e5;font-size:15px;padding:6px 0;font-weight:300;transition:color .2s}
.f-top a:hover{color:var(--mint)}
.f-brand p{color:var(--muted);font-size:15px;line-height:1.6;margin-top:14px;max-width:300px;font-weight:300}
.socials{display:flex;gap:10px;margin-top:22px}
.socials a{width:42px;height:42px;border-radius:50%;border:1px solid var(--line);display:flex;align-items:center;justify-content:center;padding:0;transition:.25s}
.socials a:hover{background:var(--mint);border-color:var(--mint)}
.socials a:hover svg{fill:var(--ink)}
.socials svg{width:17px;height:17px;fill:#fff}
.mega{font-size:clamp(80px,22vw,340px);font-weight:800;letter-spacing:-.06em;line-height:.8;margin-top:70px;color:transparent;-webkit-text-stroke:1.5px rgba(255,255,255,.14);text-align:center;user-select:none;white-space:nowrap}
.f-bot{display:flex;justify-content:space-between;gap:20px;flex-wrap:wrap;margin-top:40px;color:#7d8a88;font-size:13px}


/* chat phone */
.phone{border-radius:34px;background:#0f1515;border:1px solid var(--line);box-shadow:0 40px 120px -40px rgba(185,20,240,.5);overflow:hidden;max-width:520px;width:100%;justify-self:center;display:flex;flex-direction:column}
.ph-top{display:flex;align-items:center;gap:14px;padding:18px 22px;border-bottom:1px solid var(--line)}
.ph-av svg{width:44px;height:44px}
.ph-top b{display:block;font-size:16px;font-weight:600}
.ph-top small{display:flex;align-items:center;gap:7px;font:500 11.5px 'JetBrains Mono',monospace;color:var(--muted);margin-top:4px}
.ph-top small i{width:7px;height:7px;border-radius:50%;background:var(--mint);box-shadow:0 0 0 3px rgba(102,221,198,.2)}
.ph-body{height:400px;overflow:hidden;padding:22px;display:flex;flex-direction:column;gap:10px;justify-content:flex-end}
.msg{max-width:82%;padding:12px 16px;border-radius:20px;font-size:14.5px;line-height:1.5;opacity:0;transform:translateY(10px) scale(.97);transition:opacity .35s,transform .45s cubic-bezier(.3,1.4,.5,1)}
.msg.in{opacity:1;transform:none}
.msg.me{align-self:flex-end;background:var(--purple);border-bottom-right-radius:6px}
.msg.ai{align-self:flex-start;background:var(--ink-3);border-bottom-left-radius:6px;color:#e6eeec}
.msg.typing{display:flex;gap:5px;padding:16px 18px}
.msg.typing i{width:7px;height:7px;border-radius:50%;background:var(--mint);animation:dots 1s ease-in-out infinite}
.msg.typing i:nth-child(2){animation-delay:.15s}.msg.typing i:nth-child(3){animation-delay:.3s}
@keyframes dots{0%,60%,100%{transform:translateY(0);opacity:.5}30%{transform:translateY(-5px);opacity:1}}
.ph-input{display:flex;align-items:center;justify-content:space-between;margin:0 16px 16px;padding:8px 8px 8px 20px;border-radius:999px;background:var(--ink-2);border:1px solid var(--line);color:#7d8a88;font-size:14px}
.ph-input button{width:40px;height:40px;border-radius:50%;background:var(--mint);color:var(--ink);display:flex;align-items:center;justify-content:center}
.ph-input svg{width:18px;height:18px}
/* feature glyph variants */
.glyph.wave{gap:8px;mix-blend-mode:normal}
.glyph.wave i{width:10px;border-radius:6px;background:#fff;height:30%;animation:wv 1.1s ease-in-out infinite alternate}
.glyph.wave i:nth-child(2){animation-delay:.1s;height:50%}.glyph.wave i:nth-child(3){animation-delay:.2s;height:70%}.glyph.wave i:nth-child(4){animation-delay:.3s;height:40%}.glyph.wave i:nth-child(5){animation-delay:.4s;height:62%}.glyph.wave i:nth-child(6){animation-delay:.5s;height:36%}.glyph.wave i:nth-child(7){animation-delay:.6s;height:22%}
@keyframes wv{from{transform:scaleY(.4)}to{transform:scaleY(1)}}
.glyph.lock svg{width:34%;height:auto}

/* ───────────── RESPONSIVE ───────────── */
@media (max-width:1000px){
  .card,.card.big{grid-column:span 6}
  .card.big{grid-row:auto}
  .card.big .thumb{height:auto;aspect-ratio:16/10;min-height:0}
  .studio-grid,.faq-grid{grid-template-columns:1fr}
  .plans{grid-template-columns:1fr;max-width:520px;margin-left:auto;margin-right:auto}
  .f-top{grid-template-columns:1fr 1fr}
  .f-brand{grid-column:1/-1}
  .stat-row{grid-template-columns:repeat(2,1fr)}
  .stat:nth-child(3){border-left:0;padding-left:0}
  .stat:nth-child(-n+2){border-bottom:1px solid var(--line)}
  .s-item{grid-template-columns:60px 1fr 56px}
  .s-item p{grid-column:2/3;grid-row:2}
  .s-item .s-arrow{grid-row:1/3;grid-column:3}
}
@media (max-width:760px){
  .nav-in{width:calc(100% - 32px);height:70px}
  .links{position:fixed;inset:70px 16px auto 16px;flex-direction:column;gap:0;background:rgba(24,32,32,.96);backdrop-filter:blur(14px);border:1px solid var(--line);border-radius:20px;padding:10px;font-size:17px;transform:translateY(-10px);opacity:0;pointer-events:none;transition:.3s}
  .links a{padding:14px 16px}
  .links a.active::after{left:auto;right:18px;top:50%;bottom:auto;margin-top:-3px}
  .nav.open .links{transform:none;opacity:1;pointer-events:auto}
  .nav.open{background:rgba(24,32,32,.9)}
  .burger{display:flex}
  .nav .pill{display:none}
  .hero{height:auto;min-height:0;padding-top:96px}
  .stage{position:relative;height:auto;aspect-ratio:1120/880}
  .stage .copy{display:none}
  .mobile-intro{display:block;position:relative;z-index:2;padding:16px 24px 0;font-size:24px;line-height:1.35}
  .mobile-intro .tagline{margin-top:10px;font-size:15px;color:rgba(255,255,255,.85);font-weight:300}
  .scroll-cue,.hint{display:none}
  .card,.card.big{grid-column:1/-1}
  .tabs{overflow-x:auto;max-width:100%}
  .tabs button{white-space:nowrap}
  .stat{padding:28px 16px}
  .stat:nth-child(odd){padding-left:0;border-left:0}
  .s-item{grid-template-columns:40px 1fr 44px;gap:14px;padding:22px 0}
  .s-item:hover{padding-left:0;padding-right:0}
  .s-item::before{display:none}
  .s-arrow{width:44px;height:44px}
  details p{padding-right:0}
  .form{flex-direction:column;border-radius:22px}
  .form input{padding:14px}
  .f-top{grid-template-columns:1fr 1fr;gap:28px}
}
@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.001ms!important;animation-iteration-count:1!important;transition-duration:.001ms!important}
  .reveal{opacity:1;transform:none}
}
</style>
</head>
<body>

<!-- ═════════════ NAV ═════════════ -->
<header class="nav" id="nav" data-section="nav">
  <div class="nav-in">
    <a href="#top" class="logo">MIRAI</a>
    <nav class="links" id="links">
      <a href="#top" class="active">Home</a>
      <a href="#features">Features</a>
      <a href="#how">How it works</a>
      <a href="#pricing">Pricing</a>
    </nav>
    <a href="#demo" class="pill">Let’s Talk!</a>
    <button class="burger" id="burger" aria-label="Menu"><span></span></button>
  </div>
</header>

<!-- ═════════════ HERO (pure SVG recreation of the Rive scene) ═════════════ -->
<main>
<section class="hero intro" id="top" data-section="hero">
  <h1 class="sr">Mirai, the AI companion that actually listens</h1>
  <div class="mobile-intro">
    <div>Hey,<br>I’m your new friend,</div>
  </div>

  <svg class="stage" id="stage" viewBox="0 0 1920 1080" preserveAspectRatio="xMidYMid slice" aria-label="Animated illustration of Mirai, the AI companion, peeking out between clouds">
    <defs>
      <linearGradient id="skin" x1="0" y1="0" x2=".25" y2="1">
        <stop offset="0" stop-color="#fbd6c6"/><stop offset=".55" stop-color="#f8c4b0"/><stop offset="1" stop-color="#f3a68e"/>
      </linearGradient>
      <linearGradient id="skinLid" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0" stop-color="#f9cdbb"/><stop offset="1" stop-color="#f4b7a1"/>
      </linearGradient>
      <linearGradient id="ear" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0" stop-color="#f9c9b4"/><stop offset="1" stop-color="#f28c72"/>
      </linearGradient>
      <linearGradient id="earL" x1="1" y1="0" x2="0" y2="1">
        <stop offset="0" stop-color="#f9c4ae"/><stop offset="1" stop-color="#f2876e"/>
      </linearGradient>
      <linearGradient id="neck" x1="0" y1="0" x2="0" y2="1">
        <stop offset="0" stop-color="#e5917a"/><stop offset=".45" stop-color="#f4b49d"/><stop offset="1" stop-color="#f8c3b0"/>
      </linearGradient>
      <linearGradient id="shirt" x1=".3" y1="0" x2=".7" y2="1">
        <stop offset="0" stop-color="#63dcc5"/><stop offset=".55" stop-color="#3fc1a8"/><stop offset="1" stop-color="#1aa18a"/>
      </linearGradient>
      <linearGradient id="shirtHi" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0" stop-color="#7ce6d2"/><stop offset="1" stop-color="#3cc2a8"/>
      </linearGradient>
      <radialGradient id="iris" cx=".45" cy=".4" r=".65">
        <stop offset="0" stop-color="#1e0703"/><stop offset=".45" stop-color="#4a170a"/><stop offset="1" stop-color="#9a4319"/>
      </radialGradient>
      <linearGradient id="hair" x1="0" y1="0" x2="1" y2="1">
        <stop offset="0" stop-color="#2b2b2b"/><stop offset="1" stop-color="#151515"/>
      </linearGradient>
      <radialGradient id="blush" cx=".5" cy=".5" r=".5">
        <stop offset="0" stop-color="#f28a74" stop-opacity=".45"/><stop offset="1" stop-color="#f28a74" stop-opacity="0"/>
      </radialGradient>
      <clipPath id="eyeR"><ellipse cx="248" cy="240" rx="41" ry="47"/></clipPath>
      <clipPath id="eyeL"><ellipse cx="131" cy="268" rx="25" ry="42"/></clipPath>
    </defs>

    <!-- sky -->
    <rect width="1920" height="1080" fill="#b914f0"/>

    <!-- deep purple blobs -->
    <g class="blobs"><g class="lyr" data-depth="6">
      <circle cx="-210" cy="270" r="420" fill="#8814ad"/>
      <circle cx="250" cy="560" r="180" fill="#8814ad"/>
      <circle cx="2150" cy="300" r="420" fill="#8814ad"/>
      <circle cx="740" cy="965" r="195" fill="#8814ad"/>
      <circle cx="1440" cy="835" r="205" fill="#8814ad"/>
      <circle cx="1080" cy="1010" r="180" fill="#8814ad"/>
    </g></g>

    <!-- giant wordmark -->
    <g class="lyr" data-depth="10" id="wordLayer">
      <g id="wordScale">
        <text class="word" x="285" y="693" font-size="404" font-weight="800" fill="#fff" textLength="1365" lengthAdjust="spacingAndGlyphs" letter-spacing="-6">MIRAI</text>
      </g>
    </g>

    <!-- character -->
    <g class="lyr" data-depth="4" id="charLayer">
     <g class="char-wrap">
      <g id="char" transform="translate(700,250)">
        <!-- body -->
        <g id="body">
          <path d="M228,330 L305,318 L318,452 L240,478 Z" fill="url(#neck)"/>
          <path d="M243,448 C262,428 286,412 302,404 C344,452 382,566 398,730 L178,770 C188,650 208,532 243,448 Z" fill="url(#shirt)"/>
          <path d="M230,466 L246,444 L256,462 Z" fill="#3a0b52"/>
          <path d="M252,740 C262,628 288,540 322,508 C350,520 374,606 384,726 Z" fill="url(#shirtHi)" opacity=".75"/>
          <path d="M246,728 L334,722 L300,812 Z" fill="#f7bca7"/>
        </g>
        <!-- head -->
        <g id="head">
          <!-- bun -->
          <g fill="#070707">
            <circle cx="360" cy="48" r="46"/><circle cx="402" cy="56" r="36"/><circle cx="420" cy="92" r="27"/>
            <circle cx="330" cy="34" r="28"/><circle cx="388" cy="22" r="27"/><circle cx="425" cy="62" r="20"/>
          </g>
          <!-- ears -->
          <path d="M392,212 C420,200 452,200 459,222 C464,252 440,284 378,296 Z" fill="url(#ear)"/>
          <path d="M404,232 C424,224 444,226 446,238 C444,258 424,276 392,280 Z" fill="#f2856b" opacity=".55"/>
          <path d="M128,282 C104,280 76,282 60,285 C70,316 92,342 132,348 Z" fill="url(#earL)"/>
          <!-- earring -->
          <path d="M368,296 a14,16 0 1 0 14,22" fill="none" stroke="#e8e8e8" stroke-width="7" stroke-linecap="round"/>
          <!-- face -->
          <path d="M96,155 C104,92 196,58 290,66 C372,74 424,138 422,212 C420,284 378,334 318,358 C258,380 188,378 148,352 C108,326 90,280 90,232 C90,200 92,175 96,155 Z" fill="url(#skin)"/>
          <ellipse cx="300" cy="300" rx="70" ry="40" fill="url(#blush)"/>
          <ellipse cx="128" cy="320" rx="40" ry="26" fill="url(#blush)"/>
          <path d="M320,356 C300,368 270,372 240,370 C290,360 330,330 360,300 C350,325 338,344 320,356 Z" fill="#ec9b84" opacity=".55"/>
          <!-- right (big) eye -->
          <ellipse cx="248" cy="240" rx="46" ry="52" fill="#f6d2c1"/>
          <g clip-path="url(#eyeR)">
            <ellipse cx="248" cy="240" rx="41" ry="47" fill="#f2e6d5"/>
            <g id="irisR">
              <circle cx="255" cy="243" r="31" fill="url(#iris)"/>
              <circle cx="257" cy="246" r="13" fill="#170502" opacity=".75"/>
              <circle cx="240" cy="220" r="8.5" fill="#fff"/>
              <circle cx="231" cy="234" r="3.6" fill="#fff"/>
            </g>
            <g id="lidR">
              <rect x="200" y="96" width="100" height="97" fill="url(#skinLid)"/>
              <rect x="200" y="189" width="100" height="5" fill="#3a1a12"/>
            </g>
          </g>
          <!-- left (small) eye -->
          <ellipse cx="131" cy="268" rx="29" ry="46" fill="#f6d2c1"/>
          <g clip-path="url(#eyeL)">
            <ellipse cx="131" cy="268" rx="25" ry="42" fill="#f2e6d5"/>
            <g id="irisL">
              <ellipse cx="138" cy="268" rx="17" ry="26" fill="url(#iris)"/>
              <ellipse cx="139" cy="271" rx="7" ry="11" fill="#170502" opacity=".75"/>
              <circle cx="122" cy="258" r="5.5" fill="#fff"/>
            </g>
            <g id="lidL">
              <rect x="100" y="140" width="64" height="86" fill="url(#skinLid)"/>
              <rect x="100" y="222" width="64" height="4" fill="#3a1a12"/>
            </g>
          </g>
          <!-- brows -->
          <path id="browR" d="M170,182 C186,164 222,158 252,170 C254,174 252,178 248,178 C222,170 196,174 176,188 C172,190 168,186 170,182 Z" fill="#1d1d1d"/>
          <path id="browL" d="M100,216 C104,200 114,192 128,188 C131,188 132,192 129,194 C118,200 111,208 108,218 C106,222 99,221 100,216 Z" fill="#1d1d1d"/>
          <!-- nose + mouth -->
          <path d="M159,292 C164,281 186,280 192,291 C190,303 166,306 159,292 Z" fill="#f2836f"/>
          <circle cx="170" cy="295" r="2.6" fill="#b5463a"/><circle cx="182" cy="295" r="2.6" fill="#b5463a"/>
          <path d="M172,322 L193,320 L186,333 Z" fill="#e0605c"/>
          <!-- hair -->
          <path d="M90,150 C84,86 150,36 236,28 C306,22 362,48 392,94 C414,126 428,166 420,202 C414,224 390,230 364,224 C344,216 334,196 330,176 C318,142 300,118 270,108 C230,96 190,102 158,114 C132,124 110,140 90,150 Z" fill="url(#hair)"/>
          <path d="M92,150 C92,124 104,98 126,80 C122,108 112,132 92,150 Z" fill="#111"/>
          <path d="M94,148 C100,160 102,178 100,196 L90,200 C88,180 88,162 94,148 Z" fill="#141414"/>
          <g fill="none" stroke="#3c3c3c" stroke-width="7" stroke-linecap="round" opacity=".75">
            <path d="M140,96 C170,62 214,46 258,46"/>
            <path d="M206,98 C236,66 280,58 318,66"/>
            <path d="M300,108 C330,90 362,92 384,108"/>
            <path d="M330,150 C352,134 384,134 406,146"/>
            <path d="M342,190 C362,176 390,176 412,186"/>
          </g>
          <g fill="none" stroke="#0a0a0a" stroke-width="4" stroke-linecap="round" opacity=".8">
            <path d="M168,112 C190,78 222,62 262,58"/>
            <path d="M262,110 C290,84 330,80 360,92"/>
            <path d="M336,170 C356,156 382,156 402,166"/>
          </g>
        </g>
      </g>
     </g>
    </g>

    <!-- dark clouds -->
    <g class="clouds-l"><g class="lyr" data-depth="-14"><g class="cloud-drift">
      <circle cx="-260" cy="480" r="440" fill="#1f2525"/>
      <circle cx="170" cy="885" r="262" fill="#1f2525"/>
      <circle cx="480" cy="965" r="245" fill="#1f2525"/>
      <circle cx="800" cy="1125" r="212" fill="#1f2525"/>
    </g></g></g>
    <g class="clouds-r"><g class="lyr" data-depth="-14"><g class="cloud-drift b">
      <circle cx="1250" cy="1150" r="290" fill="#1f2525"/>
      <circle cx="1700" cy="1000" r="380" fill="#1f2525"/>
      <circle cx="2200" cy="480" r="430" fill="#1f2525"/>
    </g></g></g>

    <!-- mint bubbles -->
    <g class="lyr" data-depth="22" fill="#66ddc6">
      <g class="bub" style="animation-delay:1.0s"><circle class="float" style="--d:5s;--fx:4px;--fy:-10px" cx="260" cy="453" r="20"/></g>
      <g class="bub" style="animation-delay:1.05s"><circle class="float" style="--d:6.5s;--fx:-6px;--fy:-12px" cx="189" cy="518" r="35"/></g>
      <g class="bub" style="animation-delay:1.1s"><circle class="float" style="--d:7s;--fx:6px;--fy:-8px" cx="280" cy="566" r="35"/></g>
      <g class="bub" style="animation-delay:1.15s"><circle class="float" style="--d:8s;--fx:-4px;--fy:-16px" cx="219" cy="639" r="67"/></g>
      <g class="bub" style="animation-delay:1.25s"><circle class="float" style="--d:4.5s;--fx:3px;--fy:-9px" cx="639" cy="772" r="20"/></g>
      <g class="bub" style="animation-delay:1.3s"><circle class="float" style="--d:5.5s;--fx:-3px;--fy:-7px" cx="592" cy="755" r="9"/></g>
      <g class="bub" style="animation-delay:1.32s"><circle class="float" style="--d:6s;--fx:4px;--fy:-6px" cx="591" cy="795" r="12"/></g>
      <g class="bub" style="animation-delay:1.1s"><circle class="float" style="--d:5.2s;--fx:-5px;--fy:-12px" cx="1738" cy="213" r="20"/></g>
      <g class="bub" style="animation-delay:1.15s"><circle class="float" style="--d:4.2s;--fx:4px;--fy:-8px" cx="1774" cy="170" r="11"/></g>
      <g class="bub" style="animation-delay:1.2s"><circle class="float" style="--d:6.8s;--fx:5px;--fy:-12px" cx="1749" cy="483" r="34"/></g>
      <g class="bub" style="animation-delay:1.25s"><circle class="float" style="--d:7.6s;--fx:-5px;--fy:-16px" cx="1771" cy="558" r="67"/></g>
      <g class="bub" style="animation-delay:1.3s"><circle class="float" style="--d:6.2s;--fx:6px;--fy:-10px" cx="1710" cy="602" r="36"/></g>
      <g class="bub" style="animation-delay:1.35s"><circle class="float" style="--d:5s;--fx:-4px;--fy:-9px" cx="1642" cy="580" r="20"/></g>
    </g>

    <!-- copy -->
    <g class="copy lyr" data-depth="8" fill="#fff" font-size="43" font-weight="400">
      <text x="335" y="268">Hey,</text>
      <text x="335" y="323">I’m your new friend,</text>
      <text x="1210" y="860">The AI companion</text>
      <text x="1210" y="913">that actually listens</text>
    </g>
  </svg>

  <div class="mobile-intro" style="padding-bottom:20px;background:#1f2525;margin-top:-2px">
    <p class="tagline" style="margin-top:0">The AI companion that actually listens: it remembers what matters, checks in when you need it and keeps everything private.</p>
  </div>

  <a href="#features" class="scroll-cue"><i></i>Scroll</a>
  <div class="hint">psst — move closer, she notices.<br>just don’t poke her.</div>
</section>

<!-- ═════════════ TICKER ═════════════ -->
<div class="ticker" aria-hidden="true" data-section="ticker">
  <div class="track" id="track">
    <span>Remembers you</span><span>Real voice</span><span>Daily check-ins</span><span>Private by design</span><span>Learns your vibe</span><span>40+ languages</span><span>Mood journal</span><span>Works offline</span><span>Always kind</span>
  </div>
</div>

<!-- ═════════════ FEATURES ═════════════ -->
<section class="featured" id="features" data-section="features">
  <div class="wrap">
    <div class="sec-head reveal">
      <div>
        <span class="eyebrow">Meet Mirai</span>
        <h2>A companion that<br><em>actually gets you.</em></h2>
      </div>
      <div class="tabs" id="tabs">
        <button class="on" data-f="all">All</button>
        <button data-f="talk">Conversation</button>
        <button data-f="care">Wellbeing</button>
        <button data-f="trust">Privacy</button>
      </div>
    </div>

    <div class="grid" id="grid">
      <article class="card big reveal" data-cat="talk">
        <div class="thumb">
          <div class="art" style="background:radial-gradient(circle at 78% 30%,#66ddc6 0 9%,transparent 9.4%),radial-gradient(circle at 86% 44%,#66ddc6 0 4%,transparent 4.3%),radial-gradient(circle at 20% 120%,#1f2525 0 38%,transparent 38.3%),radial-gradient(circle at 70% 130%,#8814ad 0 40%,transparent 40.3%),#b914f0"></div>
          <div class="glyph">∞</div>
          <span class="badge prem">Signature</span>
          <span class="dur">Long-term memory</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Memory</b><span>Yours to edit</span></div>
          <h3>Remembers your dog’s name, your big interview and your coffee order, so you never start from zero.</h3>
        </div>
      </article>

      <article class="card reveal" data-cat="talk">
        <div class="thumb">
          <div class="art" style="background:radial-gradient(circle at 30% 40%,#b914f0 0 26%,transparent 26.4%),radial-gradient(circle at 75% 75%,#66ddc6 0 14%,transparent 14.4%),linear-gradient(135deg,#2a3232,#141a1a)"></div>
          <div class="glyph wave"><i></i><i></i><i></i><i></i><i></i><i></i><i></i></div>
          <span class="badge">Voice</span><span class="dur">&lt;300 ms</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Conversation</b><span>Hands-free</span></div>
          <h3>Talk out loud. It answers in a warm, natural voice and lets you interrupt.</h3>
        </div>
      </article>

      <article class="card reveal" data-cat="care">
        <div class="thumb">
          <div class="art" style="background:radial-gradient(circle at 50% 120%,#66ddc6 0 34%,transparent 34.4%),radial-gradient(circle at 50% 120%,#1fa88f 0 48%,transparent 48.4%),linear-gradient(180deg,#b914f0,#8814ad)"></div>
          <div class="glyph">☀︎</div>
          <span class="badge">Check-ins</span><span class="dur">8:00 AM</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Wellbeing</b><span>Your schedule</span></div>
          <h3>Gentle morning and evening check-ins, timed around your day, never naggy.</h3>
        </div>
      </article>

      <article class="card reveal" data-cat="trust">
        <div class="thumb">
          <div class="art" style="background:repeating-linear-gradient(90deg,rgba(102,221,198,.12) 0 2px,transparent 2px 28px),repeating-linear-gradient(0deg,rgba(102,221,198,.12) 0 2px,transparent 2px 28px),linear-gradient(160deg,#1a6e60,#0f1515 70%)"></div>
          <div class="glyph lock"><svg viewBox="0 0 64 64" fill="none" stroke="#fff" stroke-width="5" stroke-linecap="round"><rect x="12" y="28" width="40" height="28" rx="7" fill="rgba(255,255,255,.14)"/><path d="M21 28v-7a11 11 0 0 1 22 0v7"/><circle cx="32" cy="42" r="3.5" fill="#fff" stroke="none"/></svg></div>
          <span class="badge prem">On-device</span><span class="dur">E2E encrypted</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Privacy</b><span>Zero ads</span></div>
          <h3>Your conversations are encrypted and never sold, shared or used to target ads.</h3>
        </div>
      </article>

      <article class="card reveal" data-cat="care">
        <div class="thumb">
          <div class="art" style="background:conic-gradient(from 200deg at 60% 60%,#8814ad,#b914f0,#66ddc6,#8814ad)"></div>
          <div class="glyph">◐</div>
          <span class="badge">Journal</span><span class="dur">Weekly recap</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Wellbeing</b><span>Mood insights</span></div>
          <h3>A mood journal that writes itself and notices patterns you might miss.</h3>
        </div>
      </article>

      <article class="card reveal" data-cat="trust">
        <div class="thumb">
          <div class="art" style="background:radial-gradient(circle at 20% 20%,#66ddc6 0 6%,transparent 6.4%),radial-gradient(circle at 30% 36%,#66ddc6 0 3%,transparent 3.4%),radial-gradient(circle at 100% 100%,#b914f0 0 46%,transparent 46.4%),#1f2525"></div>
          <div class="glyph">⤓</div>
          <span class="badge">Control</span><span class="dur">1-tap delete</span>
        </div>
        <div class="card-body">
          <div class="meta"><b>Privacy</b><span>Export anytime</span></div>
          <h3>See everything Mirai remembers. Edit it, export it or wipe it in one tap.</h3>
        </div>
      </article>
    </div>
  </div>
</section>

<!-- ═════════════ STATS ═════════════ -->
<section class="stats" data-section="stats">
  <div class="wrap">
    <div class="stat-row reveal">
      <div class="stat"><div class="n"><sup style="margin:0 4px 0 0">&lt;</sup><span data-count="300">0</span><sup>ms</sup></div><p>Voice response time</p></div>
      <div class="stat"><div class="n"><span data-count="40">0</span><sup>+</sup></div><p>Languages, with natural accents</p></div>
      <div class="stat"><div class="n">24/7</div><p>There at 3 AM, no appointment needed</p></div>
      <div class="stat"><div class="n"><span data-count="0">0</span></div><p>Ads, trackers or data sold. Ever.</p></div>
    </div>
  </div>
</section>

<!-- ═════════════ HOW IT WORKS ═════════════ -->
<section class="series" id="how" data-section="how-it-works">
  <div class="wrap">
    <div class="reveal">
      <span class="eyebrow">How it works</span>
      <h2>From “hi” to<br>“how did you know?”</h2>
      <p class="lede">Mirai starts as a good listener and gets to know you over time, at your pace and on your terms.</p>
    </div>
    <div class="s-list">
      <a href="#pricing" class="s-item reveal"><span class="s-num">01</span><h3>Say hi</h3><p>No setup quiz. Just start talking, by text or voice, whenever you like.</p><span class="s-arrow"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a href="#pricing" class="s-item reveal"><span class="s-num">02</span><h3>It learns your vibe</h3><p>Playful or calm, chatty or brief: Mirai adapts its tone to match you.</p><span class="s-arrow"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a href="#pricing" class="s-item reveal"><span class="s-num">03</span><h3>It remembers</h3><p>Important moments are saved to a memory you can see, edit and delete.</p><span class="s-arrow"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a href="#pricing" class="s-item reveal"><span class="s-num">04</span><h3>It shows up</h3><p>Thoughtful nudges, celebrations and check-ins, only when you want them.</p><span class="s-arrow"><svg viewBox="0 0 24 24"><path d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
    </div>
  </div>
</section>

<!-- ═════════════ CHAT DEMO ═════════════ -->
<section class="studio" id="demo" data-section="demo">
  <div class="wrap studio-grid">
    <div class="phone reveal" data-component="chat-demo">
      <div class="ph-top">
        <span class="ph-av"><svg viewBox="0 0 40 40"><circle cx="20" cy="20" r="20" fill="#b914f0"/><circle cx="20" cy="22" r="11" fill="#f8c4b0"/><path d="M9 20c0-8 6-12 12-12s10 4 10 10c-3-4-8-6-13-5-4 1-7 4-9 7z" fill="#1d1d1d"/><circle cx="28" cy="8" r="5" fill="#070707"/><circle cx="17" cy="23" r="2.2" fill="#3a1208"/><circle cx="24" cy="22" r="2.6" fill="#3a1208"/></svg></span>
        <div><b>Mirai</b><small><i></i>online · remembers 214 things about you</small></div>
      </div>
      <div class="ph-body" id="chat"></div>
      <div class="ph-input"><span>Message Mirai…</span><button aria-label="Voice"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><rect x="9" y="3" width="6" height="11" rx="3"/><path d="M5 11a7 7 0 0 0 14 0M12 18v3"/></svg></button></div>
    </div>
    <div class="reveal">
      <span class="eyebrow">Built on trust</span>
      <h2>Feels personal.<br>Stays <em>private.</em></h2>
      <p class="lede">Mirai is designed to be a supportive friend, not a product that mines you. You can always see what it knows and why it said what it said.</p>
      <ul class="checks">
        <li><svg viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="11" fill="#66ddc6"/><path d="M7 12.5l3.2 3.2L17 9" stroke="#1f2525" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></svg><span><b>Memory you can read.</b> Every saved detail lives in a plain list you can edit or erase.</span></li>
        <li><svg viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="11" fill="#66ddc6"/><path d="M7 12.5l3.2 3.2L17 9" stroke="#1f2525" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></svg><span><b>Encrypted end to end.</b> Chats are locked to your devices. Not even our team can read them.</span></li>
        <li><svg viewBox="0 0 24 24" fill="none"><circle cx="12" cy="12" r="11" fill="#66ddc6"/><path d="M7 12.5l3.2 3.2L17 9" stroke="#1f2525" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></svg><span><b>Honest about being AI.</b> Mirai never pretends to be human and points you to real people when it matters.</span></li>
      </ul>
    </div>
  </div>
</section>

<!-- ═════════════ PRICING ═════════════ -->
<section class="pricing" id="pricing" data-section="pricing">
  <div class="wrap">
    <div class="center reveal">
      <span class="eyebrow">Pricing</span>
      <h2>Friendship,<br><em>upgraded.</em></h2>
      <p class="lede">Start free and stay free as long as you like. Upgrade for voice, deeper memory and a companion that grows with you.</p>
      <div class="toggle" id="toggle">
        <span class="knob" id="knob"></span>
        <button class="on" data-b="m">Monthly</button>
        <button data-b="y">Yearly <span class="save">−20%</span></button>
      </div>
    </div>
    <div class="plans">
      <div class="plan reveal">
        <span class="tag">Free</span>
        <h3>Hello</h3>
        <div class="price"><b>$0</b><span>/ forever</span></div>
        <p class="sub">A great listener, on the house.</p>
        <ul><li>Unlimited text chat</li><li>30-day memory</li><li>Daily check-ins</li><li>Mood journal basics</li></ul>
        <a href="#waitlist" class="btn btn-ghost">Start free</a>
      </div>
      <div class="plan hot reveal">
        <span class="tag">Most loved</span>
        <h3>Plus</h3>
        <div class="price"><b data-m="9.99" data-y="7.99">$9.99</b><span>/ month</span></div>
        <p class="sub" data-m="Billed monthly, cancel anytime." data-y="Billed $95.88 yearly.">Billed monthly, cancel anytime.</p>
        <ul><li>Real-time voice conversations</li><li>Lifelong memory you control</li><li>Custom personality &amp; avatar</li><li>Weekly insight recaps</li></ul>
        <a href="#waitlist" class="btn btn-mint">Get Mirai Plus</a>
      </div>
      <div class="plan reveal">
        <span class="tag">Households</span>
        <h3>Family</h3>
        <div class="price"><b data-m="19.99" data-y="15.99">$19.99</b><span>/ month</span></div>
        <p class="sub" data-m="Up to 5 people, private memories each." data-y="Billed $191.88 yearly.">Up to 5 people, private memories each.</p>
        <ul><li>Everything in Plus, for 5 people</li><li>Separate, private companions</li><li>Shared reminders &amp; lists</li><li>Priority support</li></ul>
        <a href="#waitlist" class="btn btn-ghost">Get Family</a>
      </div>
    </div>
  </div>
</section>

<!-- ═════════════ FAQ ═════════════ -->
<section class="faq" id="faq" data-section="faq">
  <div class="wrap faq-grid">
    <div class="reveal">
      <span class="eyebrow">FAQ</span>
      <h2>Questions,<br><em>answered.</em></h2>
      <p class="lede">Still curious? Tap “Let’s Talk!” and ask Mirai yourself.</p>
    </div>
    <div class="reveal">
      <details open><summary>Who can read my conversations?<i></i></summary><p>Only you. Chats are end-to-end encrypted and tied to your devices. We don’t sell data, show ads or train on your private conversations without your opt-in.</p></details>
      <details><summary>Can I control what Mirai remembers?<i></i></summary><p>Yes. Open Memory to see every saved detail in plain language. Edit or delete anything, pause memory for a chat, or wipe everything in one tap.</p></details>
      <details><summary>Is Mirai a replacement for therapy?<i></i></summary><p>No. Mirai is a supportive companion, not a medical or crisis service. If you’re going through something serious, it will encourage you to reach out to people you trust and share professional and crisis resources.</p></details>
      <details><summary>Does it work offline?<i></i></summary><p>Text chat and your journal work offline on supported devices. Voice and some features need a connection and sync when you’re back online.</p></details>
      <details><summary>Can I cancel anytime?<i></i></summary><p>Yes. Cancel in one click and you keep Plus until the end of the billing period. Your companion and memories stay on the free plan.</p></details>
    </div>
  </div>
</section>

<!-- ═════════════ WAITLIST CTA ═════════════ -->
<section class="cta" id="waitlist" data-section="waitlist">
  <div class="wrap">
    <div class="cta-box reveal">
      <svg class="bg" viewBox="0 0 1200 520" preserveAspectRatio="xMidYMid slice" aria-hidden="true">
        <circle cx="1180" cy="40" r="260" fill="#8814ad"/>
        <circle cx="1250" cy="520" r="250" fill="#1f2525"/>
        <circle cx="960" cy="610" r="150" fill="#1f2525"/>
        <g fill="#66ddc6"><circle class="float" style="--d:6s" cx="1010" cy="300" r="34"/><circle class="float" style="--d:5s;--fx:-5px" cx="1070" cy="250" r="16"/><circle class="float" style="--d:7s" cx="940" cy="360" r="12"/></g>
      </svg>
      <span class="eyebrow" style="color:#fff">Early access</span>
      <h2>Someone’s been<br>waiting to meet you.</h2>
      <p class="lede">Join the early-access list. We’re letting people in every week, and early members get three months of Plus free.</p>
      <form class="form" id="form">
        <input type="email" required placeholder="you@email.com" aria-label="Email address">
        <button class="btn btn-mint" type="submit">Get early access <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg></button>
      </form>
      <p class="form-note" id="note">iOS · Android · Web · No spam, ever.</p>
    </div>
  </div>
</section>

<!-- ═════════════ FOOTER ═════════════ -->
</main>

<footer data-section="footer">
  <div class="wrap">
    <div class="f-top">
      <div class="f-brand">
        <a href="#top" class="logo">MIRAI</a>
        <p>An AI companion that listens, remembers and keeps your secrets.</p>
        <div class="socials">
          <a href="#" aria-label="Code"><svg viewBox="0 0 24 24"><path d="M12 .5a11.5 11.5 0 0 0-3.64 22.4c.58.1.79-.25.79-.56v-2c-3.2.7-3.88-1.37-3.88-1.37-.52-1.33-1.28-1.69-1.28-1.69-1.04-.71.08-.7.08-.7 1.16.08 1.77 1.19 1.77 1.19 1.03 1.76 2.7 1.25 3.35.96.1-.75.4-1.25.73-1.54-2.56-.29-5.24-1.28-5.24-5.69 0-1.26.45-2.29 1.19-3.1-.12-.29-.52-1.46.11-3.05 0 0 .97-.31 3.17 1.18a11 11 0 0 1 5.77 0c2.2-1.49 3.17-1.18 3.17-1.18.63 1.59.23 2.76.11 3.05.74.81 1.19 1.84 1.19 3.1 0 4.42-2.69 5.39-5.25 5.68.41.36.78 1.06.78 2.14v3.17c0 .31.21.67.8.56A11.5 11.5 0 0 0 12 .5z"/></svg></a>
          <a href="#" aria-label="Social"><svg viewBox="0 0 24 24"><path d="M17.8 2h3.4l-7.4 8.5L22.5 22h-6.8l-5.3-7-6.1 7H.9l7.9-9L.5 2h7l4.8 6.4L17.8 2zm-1.2 18h1.9L6.5 3.9H4.5L16.6 20z"/></svg></a>
          <a href="#" aria-label="Community"><svg viewBox="0 0 24 24"><path d="M4 4h16a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2H9l-5 4v-4a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2z"/></svg></a>
          <a href="#waitlist" aria-label="Newsletter"><svg viewBox="0 0 24 24"><path d="M2 5h20v14H2zm2 2v.5l8 5 8-5V7zm16 2.9-8 5-8-5V17h16z"/></svg></a>
        </div>
      </div>
      <div><h4>Product</h4><a href="#features">Features</a><a href="#how">How it works</a><a href="#pricing">Pricing</a><a href="#demo">Live demo</a></div>
      <div><h4>Trust</h4><a href="#">Privacy promise</a><a href="#">Safety center</a><a href="#">Security</a><a href="#faq">FAQ</a></div>
      <div><h4>Company</h4><a href="#">About</a><a href="#">Careers</a><a href="#">Press kit</a><a href="#">Contact</a></div>
    </div>
    <div class="mega">MIRAI</div>
    <div class="f-bot"><span>© 2026 Mirai Labs. Mirai is an AI and not a substitute for professional care.</span><span>Privacy · Terms · Cookies</span></div>
  </div>
</footer>

<script>
(()=>{
const $=s=>document.querySelector(s), $$=s=>[...document.querySelectorAll(s)];
const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;

/* ── nav ── */
const nav=$('#nav');
const onScroll=()=>nav.classList.toggle('scrolled',scrollY>40);
addEventListener('scroll',onScroll,{passive:true});onScroll();
$('#burger').onclick=()=>nav.classList.toggle('open');
$$('#links a').forEach(a=>a.onclick=()=>nav.classList.remove('open'));

/* ── hero: responsive framing ── */
const stage=$('#stage'), wordScale=$('#wordScale');
function frame(){
  if(innerWidth<=760){
    stage.setAttribute('viewBox','400 200 1120 880');
    stage.setAttribute('preserveAspectRatio','xMidYMax meet');
    wordScale.setAttribute('transform','translate(967 549) scale(.72) translate(-967 -549)');
  }else{
    stage.setAttribute('viewBox','0 0 1920 1080');
    stage.setAttribute('preserveAspectRatio','xMidYMid slice');
    wordScale.removeAttribute('transform');
  }
}
frame();addEventListener('resize',frame);
setTimeout(()=>$('.hero').classList.remove('intro'),2600);

/* ── character rig (state machine: idle / near / annoyed / blink) ── */
const head=$('#head'), irisR=$('#irisR'), irisL=$('#irisL'), lidR=$('#lidR'), lidL=$('#lidL'), browR=$('#browR'), browL=$('#browL'), body=$('#body'), charEl=$('#char');
const CX=700, CY=250;                 // character offset in stage
const FACE={x:CX+250,y:CY+240};       // face centre in stage coords
const S={ptr:null,lastMove:0,near:0,nearT:0,ann:0,annT:0,blink:0,nextBlink:performance.now()+1800,blinkStart:0,
         eye:{x:0,y:0},eyeT:{x:0,y:0},glanceAt:0,tilt:0,tiltT:0,par:{x:0,y:0},parT:{x:0,y:0},annoyUntil:0,pokes:[]};
const lerp=(a,b,t)=>a+(b-a)*t, clamp=(v,a,b)=>Math.max(a,Math.min(b,v));

function toStage(e){
  const p=stage.createSVGPoint();p.x=e.clientX;p.y=e.clientY;
  const m=stage.getScreenCTM(); if(!m) return null;
  return p.matrixTransform(m.inverse());
}
const hero=$('.hero');
hero.addEventListener('pointermove',e=>{
  const p=toStage(e); if(!p) return;
  S.ptr=p; S.lastMove=performance.now();
  const r=hero.getBoundingClientRect();
  S.parT.x=(e.clientX-r.left)/r.width-.5; S.parT.y=(e.clientY-r.top)/r.height-.5;
});
hero.addEventListener('pointerleave',()=>{S.ptr=null;S.parT.x=S.parT.y=0});
function annoy(){
  S.annoyUntil=performance.now()+2200;
  if(!reduce){ head.animate([{transform:'translate(0,0)'},{transform:'translate(-6px,2px)'},{transform:'translate(5px,-1px)'},{transform:'translate(0,0)'}],{duration:320,easing:'ease-out'}) }
}
charEl.addEventListener('pointerdown',e=>{e.preventDefault();annoy()});
$('.nav .pill').addEventListener('pointerenter',()=>{S.forceNear=performance.now()+1400});

function tick(now){
  const t=now/1000;
  const active=S.ptr && now-S.lastMove<4000;
  // targets for gaze
  if(active){
    const dx=S.ptr.x-FACE.x, dy=S.ptr.y-FACE.y, d=Math.hypot(dx,dy)||1;
    const k=Math.min(1,d/260);
    S.eyeT.x=dx/d*k; S.eyeT.y=dy/d*k;
    S.near=(d<420)||(S.forceNear>now)?1:0;
    S.tiltT=clamp(dx/90,-5,5);
  }else{
    S.near=(S.forceNear>now)?1:0;
    if(now>S.glanceAt){ // idle glances like the Rive idle loop
      const opts=[[-.9,.25],[-.6,-.4],[.2,.1],[.7,-.2],[-1,.5],[0,0]];
      const o=opts[Math.floor(Math.random()*opts.length)];
      S.eyeT.x=o[0];S.eyeT.y=o[1]; S.glanceAt=now+1400+Math.random()*2200;
      S.tiltT=o[0]*3;
    }
  }
  // annoyed if poked repeatedly: rapid passes through face
  const annoyed=now<S.annoyUntil?1:0;
  S.nearT=lerp(S.nearT,S.near,.12); S.annT=lerp(S.annT,annoyed,.14);
  S.eye.x=lerp(S.eye.x,S.eyeT.x,.16); S.eye.y=lerp(S.eye.y,S.eyeT.y,.16);
  S.tilt=lerp(S.tilt,S.tiltT,.06);
  S.par.x=lerp(S.par.x,S.parT.x,.07); S.par.y=lerp(S.par.y,S.parT.y,.07);

  // blink
  if(now>S.nextBlink && S.blinkStart===0){S.blinkStart=now}
  let b=0;
  if(S.blinkStart){
    const p=(now-S.blinkStart)/170;
    b=p<.5?p*2:Math.max(0,2-p*2);
    if(p>=1){S.blinkStart=0;S.nextBlink=now+2200+Math.random()*3200; if(Math.random()<.2)S.nextBlink=now+220}
  }

  // apply — idle breathing + sway (Character Idle)
  const sway=reduce?0:Math.sin(t*1.3)*1.6, bob=reduce?0:Math.sin(t*2.1)*3;
  const ang=S.tilt+sway-S.annT*3;
  head.setAttribute('transform',`translate(0 ${bob*.6 - S.nearT*4}) rotate(${ang} 268 350)`);
  body.setAttribute('transform',`translate(0 ${bob*.35})`);
  // eyes (Near = wider / pupils bigger)
  const ex=S.eye.x*10, ey=S.eye.y*9, ps=1+S.nearT*.08;
  irisR.setAttribute('transform',`translate(${ex} ${ey}) translate(255 243) scale(${ps}) translate(-255 -243)`);
  irisL.setAttribute('transform',`translate(${ex*.7} ${ey*.9}) translate(138 268) scale(${ps}) translate(-138 -268)`);
  // lids: open 0 → annoyed half → blink closed
  const half=S.annT*.5, lid=Math.max(half,b)-S.nearT*.06;
  lidR.setAttribute('transform',`translate(0 ${lid*98})`);
  lidL.setAttribute('transform',`translate(0 ${lid*88})`);
  // brows: raise when near, lower+flatten when annoyed
  const by=-S.nearT*9 + S.annT*16;
  browR.setAttribute('transform',`translate(0 ${by}) rotate(${S.annT*7 - S.nearT*2} 210 172)`);
  browL.setAttribute('transform',`translate(0 ${by*.8}) rotate(${-S.annT*10} 114 204)`);
  // parallax layers
  $$('.lyr').forEach(l=>{const d=+l.dataset.depth||0; l.setAttribute('transform',`translate(${(-S.par.x*d*2.2).toFixed(2)} ${(-S.par.y*d*1.4).toFixed(2)})`)});
  requestAnimationFrame(tick);
}
requestAnimationFrame(tick);

/* ── ticker duplicate ── */
const track=$('#track'); track.innerHTML+=track.innerHTML;

/* ── reveal ── */
const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}}),{threshold:.14});
$$('.reveal').forEach((el,i)=>{el.style.transitionDelay=(i%3)*90+'ms';io.observe(el)});

/* ── counters ── */
const cio=new IntersectionObserver(es=>es.forEach(e=>{
  if(!e.isIntersecting)return; cio.unobserve(e.target);
  const el=e.target, to=+el.dataset.count, dec=+(el.dataset.dec||0), t0=performance.now(), dur=1600;
  const step=n=>{const p=Math.min(1,(n-t0)/dur), v=to*(1-Math.pow(1-p,3)); el.textContent=v.toFixed(dec); if(p<1)requestAnimationFrame(step)};
  requestAnimationFrame(step);
}),{threshold:.6});
$$('[data-count]').forEach(el=>cio.observe(el));

/* ── filter tabs ── */
$$('#tabs button').forEach(b=>b.onclick=()=>{
  $$('#tabs button').forEach(x=>x.classList.toggle('on',x===b));
  const f=b.dataset.f;
  $$('#grid .card').forEach(c=>c.classList.toggle('hide',f!=='all'&&c.dataset.cat!==f));
});

/* ── chat demo ── */
const convo=[
 ['me','ugh, the interview is tomorrow and I can’t sleep'],
 ['ai','The product design one at the studio you love? You prepped your portfolio story all weekend, and it’s good.'],
 ['me','what if I freeze on the case study'],
 ['ai','Then you pause, sip water and start with the “why”, like we practiced Tuesday. Want a 2-minute run-through now?'],
 ['me','yes please 🙏'],
 ['ai','Okay! Pretend I’m the hiring lead. “Walk me through a project you’re proud of.” Go 🎤'],
];
const chatEl=$('#chat'); let chatOn=false;
function bubble(who,txt){const d=document.createElement('div');d.className='msg '+who;d.textContent=txt;chatEl.appendChild(d);requestAnimationFrame(()=>d.classList.add('in'));chatEl.scrollTop=chatEl.scrollHeight;return d}
function runChat(){
  if(chatOn)return; chatOn=true; let i=0;
  const next=()=>{
    if(i>=convo.length){setTimeout(()=>{chatEl.innerHTML='';i=0;next()},6000);return}
    const [who,txt]=convo[i++];
    if(who==='ai'){
      const t=document.createElement('div');t.className='msg ai typing in';t.innerHTML='<i></i><i></i><i></i>';chatEl.appendChild(t);chatEl.scrollTop=chatEl.scrollHeight;
      setTimeout(()=>{t.remove();bubble('ai',txt);setTimeout(next,1300)},900+txt.length*12);
    }else{bubble('me',txt);setTimeout(next,900)}
  };
  next();
}
new IntersectionObserver((es,o)=>es.forEach(e=>{if(e.isIntersecting){runChat();o.disconnect()}}),{threshold:.35}).observe(chatEl);

/* ── pricing toggle ── */
const knob=$('#knob'), tb=$$('#toggle button');
function setKnob(b){knob.style.width=b.offsetWidth+'px';knob.style.transform=`translateX(${b.offsetLeft-6}px)`}
tb.forEach(b=>b.onclick=()=>{
  tb.forEach(x=>x.classList.toggle('on',x===b)); setKnob(b);
  const k=b.dataset.b;
  $$('.price b[data-m]').forEach(p=>p.textContent='$'+p.dataset[k]);
  $$('.sub[data-m]').forEach(p=>p.textContent=p.dataset[k]);
});
requestAnimationFrame(()=>setKnob(tb[0])); addEventListener('resize',()=>setKnob($('#toggle button.on')));

/* ── newsletter ── */
$('#form').addEventListener('submit',e=>{e.preventDefault();$('#note').textContent='✦ You’re on the list. Your invite is on its way.';e.target.reset()});
})();
</script>
</body>
</html>
```

