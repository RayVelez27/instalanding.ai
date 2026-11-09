INSTALANDING.AI · Nimbus AI Assistant Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Nimbus AI Assistant Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/nimbus-ai-assistant-page

nimbus-ai-assistant.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Nimbus AI Assistant Page
  slug     nimbus-ai-assistant-page
  prompt   https://instalanding.ai/p/nimbus-ai-assistant-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/nimbus-ai-assistant-page
  license  Fictional product ("Nimbus", "Nimbus, Inc.") with fictional customers, people, quotes, figures and prices; the
           customer wordmarks are made up and drawn in SVG, and the email placeholder uses the reserved .example domain.
           Replace before shipping. The layout follows a design credited in the footer ("Design by Amar KZR"); keep the
           credit if you ship it.

  MAP
  tokens    :root: --bg #f6f6f6, --white, --ink #0c0c0c, --grey #4d4d4d, --muted, coral --accent #ff462e with -08 / -16
            tints and --accent-soft, --line, --glass, --shadow; Instrument Serif (h1, h2, prices, menu) and Inter from
            Google Fonts. The sky is #07588A → #E1F6F4.
  sections  nav, hero, process, integrations, testimonials, pricing, blog, faq, cta, footer (each carries data-section)
  scripts   one at the end of <body>: the glass-pill nav (shrinks on scroll, sliding hover highlight, active section,
            a full menu panel under 1200px), the three-slide process carousel, the logo ticker, the integrations orbit
            (three rings of tool tiles built from the icons array), the shared monthly / annual pricing switch, the FAQ
            accordion, the newsletter form, and the parallax cloud sky: clouds stamped from a radial "puff" on canvas,
            drifting sideways and parallaxing with scroll, in the hero and the CTA.
  assets    no image files: every picture (phones, app screens, orbit icons, logos, blog art, portraits) is CSS or SVG;
            the clouds are drawn on canvas

  ADAPTING
  - The hero and CTA skies are the same Sky() on two canvases; each only animates while it is on screen.
  - The phone status bar is .status; the footer's green "All systems normal" pill is .sys-status. They were one
    class in the source, which broke the phone status bars.
  - The orbit is built in script from the rings and icons arrays; tiles counter-rotate so the icons stay upright.
  - The CTA card overlaps the footer with a negative bottom margin (-240px, -170px on phones) and the footer has
    matching top padding; change them together.
  - prefers-reduced-motion: no CSS animation or transitions, the sky draws once, the process carousel does not
    auto-advance and the SVG blog art is paused.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Nimbus — AI Assistant</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#f6f6f6; --white:#fff; --ink:#0c0c0c; --grey:#4d4d4d; --muted:#bfbfbf;
  --accent:#ff462e; --accent-08:rgba(255,70,46,.08); --accent-16:rgba(255,70,46,.16);
  --accent-soft:#fff6f4; --line:#ebebeb; --glass:rgba(255,255,255,.1);
  --shadow:0 16px 40px rgba(0,0,0,.05);
  --serif:"Instrument Serif",Georgia,serif; --sans:"Inter",system-ui,sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--ink);font-family:var(--sans);font-weight:500;font-size:16px;line-height:1.2;-webkit-font-smoothing:antialiased;overflow-x:hidden}
a{color:inherit;text-decoration:none}
button{font:inherit;border:0;background:none;cursor:pointer;color:inherit}
h1,h2{font-family:var(--serif);font-weight:400;letter-spacing:-.03em}
h1{font-size:72px;line-height:1.1;text-wrap:balance}
h2{font-size:58px;line-height:1}
h3{font-size:30px;font-weight:500;line-height:1}
h4{font-size:22px;font-weight:500;line-height:1.2}
.lead{font-size:19px}
.small{font-size:14px}
.grey{color:var(--grey)}
.center{text-align:center}
.wrap{width:100%;max-width:1300px;margin:0 auto;padding:100px 40px}

/* buttons */
.btn{display:inline-flex;align-items:center;gap:8px;padding:12px 24px;border-radius:10px;box-shadow:var(--shadow);transition:transform .25s,opacity .25s;white-space:nowrap}
.btn:hover{transform:translateY(-2px)}
.btn-dark{background:var(--ink);color:#fff}
.btn-light{background:#fff;color:var(--ink)}
.btn svg{width:22px;height:22px}

/* tag */
.tag{display:inline-flex;align-items:center;gap:8px;padding:7px 12px;border-radius:15px;background:var(--accent-08);border:1px solid var(--accent-16);color:var(--accent);font-size:13px;font-weight:600}
.tag svg{width:16px;height:16px}
.tag.plain{background:var(--bg);border-color:transparent;color:var(--grey);font-size:12px}
.tag.soft{border-color:transparent;font-size:12px}
.tag.soft svg{width:14px;height:14px}
.ico{fill:none;stroke:currentColor;stroke-width:1.8;stroke-linecap:round;stroke-linejoin:round}

/* NAV — glass pill */
.ease{transition-timing-function:cubic-bezier(.2,.8,.2,1)}
.nav{position:fixed;top:0;left:0;right:0;padding:20px 24px 0;z-index:60;display:flex;justify-content:center;pointer-events:none}
.nav-inner{pointer-events:auto;position:relative;width:100%;max-width:1180px;height:64px;display:flex;align-items:center;justify-content:space-between;gap:16px;padding:0 8px 0 22px;border-radius:999px;
  background:linear-gradient(180deg,rgba(20,26,34,.38),rgba(8,12,18,.26));
  -webkit-backdrop-filter:blur(22px) saturate(170%);backdrop-filter:blur(22px) saturate(170%);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.16),0 12px 32px -12px rgba(2,18,34,.5),0 2px 6px rgba(0,0,0,.06);
  transition:max-width .7s cubic-bezier(.2,.8,.2,1),height .5s cubic-bezier(.2,.8,.2,1),background .5s}
.nav-inner::before,.int::before,.foot-wrap::after{content:"";position:absolute;inset:0;border-radius:inherit;padding:1px;pointer-events:none;
  background:linear-gradient(180deg,rgba(255,255,255,.38),rgba(255,255,255,.05) 55%,rgba(255,255,255,.16));
  -webkit-mask:linear-gradient(#000 0 0) content-box,linear-gradient(#000 0 0);-webkit-mask-composite:xor;mask-composite:exclude}
.nav.scrolled .nav-inner,.nav.open .nav-inner{max-width:940px;height:58px;background:linear-gradient(180deg,rgba(16,18,22,.84),rgba(9,10,13,.78))}
.logo{display:flex;align-items:center;gap:10px;color:#fff;font-size:19px;font-weight:600;letter-spacing:-.02em}
.logo-mark{width:30px;height:30px;flex:none}
.nav-links{position:relative;display:flex;gap:2px;color:rgba(255,255,255,.7);font-size:14.5px}
.nav-links a{position:relative;z-index:1;padding:9px 16px;border-radius:999px;transition:color .25s}
.nav-links a:hover,.nav-links a.active{color:#fff}
.nav-hl{position:absolute;top:0;left:0;height:100%;width:0;border-radius:999px;background:rgba(255,255,255,.1);box-shadow:inset 0 1px 0 rgba(255,255,255,.14);opacity:0;pointer-events:none;
  transition:transform .5s cubic-bezier(.2,.8,.2,1),width .5s cubic-bezier(.2,.8,.2,1),opacity .3s}
.nav-right{display:flex;gap:8px;align-items:center}
.nav-cta{display:inline-flex;align-items:center;gap:12px;height:48px;padding:0 6px 0 20px;border-radius:999px;background:#fff;color:#0c0c0c;font-size:14.5px;font-weight:600;white-space:nowrap;
  box-shadow:inset 0 -2px 0 rgba(0,0,0,.06),0 8px 22px -8px rgba(255,255,255,.45);transition:height .5s cubic-bezier(.2,.8,.2,1),transform .3s}
.nav-cta:hover{transform:translateY(-1px)}
.nav-cta .arr{width:36px;height:36px;border-radius:50%;background:#0c0c0c;color:#fff;display:flex;align-items:center;justify-content:center;transition:transform .5s cubic-bezier(.2,.8,.2,1)}
.nav-cta .arr svg{width:15px;height:15px}
.nav-cta:hover .arr{transform:rotate(-45deg)}
.nav.scrolled .nav-right .nav-cta{height:44px}
.nav.scrolled .nav-right .nav-cta .arr{width:32px;height:32px}
.menu-btn{display:none;position:relative;width:48px;height:48px;border-radius:50%;flex:none;background:rgba(255,255,255,.08);box-shadow:inset 0 1px 0 rgba(255,255,255,.16),inset 0 0 0 1px rgba(255,255,255,.06);transition:background .4s,transform .3s}
.menu-btn:active{transform:scale(.94)}
.menu-btn span{position:absolute;left:15px;height:1.5px;border-radius:2px;background:#fff;transition:transform .6s cubic-bezier(.7,0,.2,1),width .4s cubic-bezier(.7,0,.2,1),background .4s}
.menu-btn span:nth-child(1){top:20.5px;width:18px}
.menu-btn span:nth-child(2){top:26.5px;width:11px}
.menu-btn:hover span:nth-child(2){width:18px}
.nav.open .menu-btn{background:#fff}
.nav.open .menu-btn span{background:#0c0c0c;width:18px}
.nav.open .menu-btn span:nth-child(1){transform:translateY(3px) rotate(45deg)}
.nav.open .menu-btn span:nth-child(2){transform:translateY(-3px) rotate(-45deg)}
.menu-panel{display:none;position:absolute;top:calc(100% + 10px);left:0;right:0;padding:10px;border-radius:30px;
  background:linear-gradient(180deg,rgba(18,20,25,.94),rgba(9,10,13,.96));-webkit-backdrop-filter:blur(26px) saturate(170%);backdrop-filter:blur(26px) saturate(170%);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.14),inset 0 0 0 1px rgba(255,255,255,.06),0 40px 80px -24px rgba(0,0,0,.6);
  opacity:0;visibility:hidden;transform:translateY(-10px) scale(.98);transform-origin:top center;
  transition:opacity .35s,transform .6s cubic-bezier(.2,.8,.2,1),visibility 0s .6s}
.nav.open .menu-panel{opacity:1;visibility:visible;transform:none;transition:opacity .35s,transform .6s cubic-bezier(.2,.8,.2,1)}
.menu-label{display:flex;justify-content:space-between;padding:12px 18px 6px;font-size:11px;letter-spacing:.14em;text-transform:uppercase;color:rgba(255,255,255,.38)}
.menu-label i{font-style:normal;display:flex;align-items:center;gap:6px}
.menu-label i::before{content:"";width:6px;height:6px;border-radius:50%;background:#3ddc97;box-shadow:0 0 8px #3ddc97}
.mi{display:flex;align-items:center;gap:16px;padding:12px 12px 12px 18px;border-radius:20px;color:#fff;font-family:var(--serif);font-size:34px;line-height:1;letter-spacing:-.02em;
  opacity:0;transform:translateY(12px);transition:opacity .45s,transform .6s cubic-bezier(.2,.8,.2,1),background .25s}
.nav.open .mi{opacity:1;transform:none;transition-delay:calc(var(--i)*55ms + 120ms),calc(var(--i)*55ms + 120ms),0s}
.mi small{font-family:var(--sans);font-size:12px;color:rgba(255,255,255,.35);width:20px;letter-spacing:.04em}
.mi .go{margin-left:auto;width:40px;height:40px;border-radius:50%;display:flex;align-items:center;justify-content:center;box-shadow:inset 0 0 0 1px rgba(255,255,255,.14);color:rgba(255,255,255,.7);transition:transform .5s cubic-bezier(.2,.8,.2,1),background .3s,color .3s}
.mi .go svg{width:16px;height:16px}
.mi:hover{background:rgba(255,255,255,.05)}
.mi:hover .go{background:#fff;color:#0c0c0c;transform:rotate(-45deg)}
.menu-foot{display:flex;gap:8px;margin-top:8px;padding:10px 0 0;border-top:1px solid rgba(255,255,255,.07);opacity:0;transition:opacity .5s .4s}
.nav.open .menu-foot{opacity:1}
.menu-foot .nav-cta{flex:1;justify-content:space-between;height:52px}
.menu-foot .ghost{height:52px;padding:0 22px;border-radius:999px;display:flex;align-items:center;color:#fff;background:rgba(255,255,255,.07);box-shadow:inset 0 1px 0 rgba(255,255,255,.1);font-size:14.5px}
.nav-scrim{position:fixed;inset:0;z-index:55;background:rgba(4,10,18,.4);-webkit-backdrop-filter:blur(6px);backdrop-filter:blur(6px);opacity:0;visibility:hidden;transition:opacity .5s,visibility 0s .5s}
body.menu-open{overflow:hidden}
body.menu-open .nav-scrim{opacity:1;visibility:visible;transition:opacity .5s}

/* SKY (replaces cloud photo) */
.sky{position:absolute;inset:0;border-radius:inherit;overflow:hidden;background:linear-gradient(180deg,#07588A 0%,#E1F6F4 100%)}
.sky canvas{position:absolute;inset:0;width:100%;height:100%;display:block;margin:0}
.hero-text,.cta-card{text-shadow:0 1px 14px rgba(4,40,68,.28)}
.hero-text .btn,.cta-card .btn{text-shadow:none}
@keyframes drift{from{transform:translateX(-30px)}to{transform:translateX(30px)}}

/* HERO */
.hero{position:relative;padding:12px 12px 0}
.hero-card{position:relative;border-radius:10px;overflow:hidden;box-shadow:var(--shadow)}
.hero-content{position:relative;z-index:2;max-width:1220px;margin:0 auto;padding:200px 40px 0;display:flex;flex-direction:column;align-items:center;gap:42px}
.hero-text{display:flex;flex-direction:column;align-items:center;gap:16px;color:#fff}
.badge-logo{padding:4px;border-radius:14px;background:var(--glass);box-shadow:var(--shadow)}
.badge-logo div{padding:10px;border-radius:10px;background:#fff;display:flex}
.badge-logo svg{width:32px;height:32px}
.hero h1{max-width:900px;text-align:center}
.hero p{max-width:500px;text-align:center}
.cta-row{display:flex;gap:16px}
.fade-up{opacity:0;transform:translateY(20px);animation:up .9s cubic-bezier(.2,.8,.2,1) forwards}
@keyframes up{to{opacity:1;transform:none}}
.d1{animation-delay:.2s}.d2{animation-delay:.5s}.d3{animation-delay:.8s}.d4{animation-delay:1.1s}

/* phones */
.phones{position:relative;width:100%;max-width:800px;height:520px;overflow:hidden}
.phone{position:absolute;top:30px;width:300px;height:610px;border-radius:46px;background:#111;padding:12px;box-shadow:0 30px 60px rgba(0,0,0,.25),inset 0 0 0 2px #333}
.phone.left{left:80px;transform:rotate(-6deg);z-index:2}
.phone.right{right:80px;transform:rotate(6deg);top:60px}
.screen{position:relative;width:100%;height:100%;border-radius:36px;overflow:hidden;background:#fafafa;display:flex;flex-direction:column}
.notch{position:absolute;top:10px;left:50%;transform:translateX(-50%);width:90px;height:26px;border-radius:14px;background:#111;z-index:3}
.status{display:flex;justify-content:space-between;padding:14px 22px 0;font-size:12px;font-weight:600}
.app-head{display:flex;align-items:center;gap:10px;padding:26px 16px 12px;border-bottom:1px solid var(--line)}
.av{width:30px;height:30px;border-radius:50%;background:linear-gradient(135deg,#ff8a6b,var(--accent));display:flex;align-items:center;justify-content:center}
.av svg{width:16px;height:16px;color:#fff}
.chat{flex:1;padding:14px;display:flex;flex-direction:column;gap:10px;font-size:12px;line-height:1.4;font-weight:500}
.b{max-width:82%;padding:10px 12px;border-radius:16px}
.b.me{align-self:flex-end;background:var(--ink);color:#fff;border-bottom-right-radius:4px}
.b.ai{align-self:flex-start;background:#fff;box-shadow:0 2px 8px rgba(0,0,0,.06);border-bottom-left-radius:4px}
.typing{display:flex;gap:4px;padding:12px}
.typing i{width:6px;height:6px;border-radius:50%;background:#999;animation:blink 1.2s infinite}
.typing i:nth-child(2){animation-delay:.2s}.typing i:nth-child(3){animation-delay:.4s}
@keyframes blink{0%,100%{opacity:.25}50%{opacity:1}}
.inputbar{margin:10px;padding:10px 12px;border-radius:20px;background:#fff;box-shadow:0 2px 10px rgba(0,0,0,.08);font-size:12px;color:#999;display:flex;justify-content:space-between;align-items:center}
.send{width:26px;height:26px;border-radius:50%;background:var(--accent)}
.home-screen{padding:30px 16px 16px;display:flex;flex-direction:column;gap:12px}
.greet{font-family:var(--serif);font-size:30px;line-height:1}
.chips{display:flex;flex-wrap:wrap;gap:6px}
.chip{font-size:11px;padding:6px 10px;border-radius:12px;background:#fff;box-shadow:0 2px 6px rgba(0,0,0,.06)}
.mini-card{border-radius:16px;padding:12px;color:#fff;font-size:12px;line-height:1.35}
.bars{display:flex;align-items:flex-end;gap:5px;height:60px;margin-top:10px}
.bars i{flex:1;border-radius:4px;background:rgba(255,255,255,.7)}

/* PROCESS */
.process{display:flex;gap:42px;align-items:stretch}
.proc-text{flex:1;display:flex;flex-direction:column;justify-content:space-between;gap:24px}
.proc-text .top{display:flex;flex-direction:column;gap:16px;align-items:flex-start}
.ctrl{display:flex;gap:8px}
.ctrl button{width:40px;height:40px;border-radius:10px;background:#fff;box-shadow:var(--shadow);display:flex;align-items:center;justify-content:center;transition:opacity .2s}
.ctrl button svg{width:22px;height:22px}
.dots{display:flex;gap:6px}
.dots i{height:6px;width:6px;border-radius:3px;background:rgba(0,0,0,.5);transition:width .3s,background .3s}
.dots i.on{width:18px;background:var(--ink)}
.proc-visual{position:relative;width:66%;height:620px;border-radius:22px;overflow:hidden;box-shadow:var(--shadow);background:linear-gradient(140deg,#ffd5c8,#ffb59f 40%,#f6c9e8 75%,#cfd8ff)}
.proc-visual::before{content:"";position:absolute;inset:-20%;background:radial-gradient(circle at 20% 30%,#ff8a6b 0,transparent 35%),radial-gradient(circle at 80% 70%,#9eb6ff 0,transparent 35%),radial-gradient(circle at 70% 15%,#ffe2a8 0,transparent 30%);filter:blur(30px);animation:drift 14s ease-in-out infinite alternate}
.slide{position:absolute;inset:42px 42px 0;border-radius:10px 10px 0 0;background:#fff;box-shadow:var(--shadow);opacity:0;transform:translateY(16px);transition:opacity .6s,transform .6s;overflow:hidden;display:flex}
.slide.on{opacity:1;transform:none}
.side{width:150px;background:#fafafa;border-right:1px solid var(--line);padding:16px 12px;display:flex;flex-direction:column;gap:8px;font-size:12px}
.side b{display:flex;align-items:center;gap:6px;font-size:14px;margin-bottom:10px}
.side span{padding:8px 10px;border-radius:8px;color:var(--grey)}
.side span.act{background:#fff;color:var(--ink);box-shadow:0 2px 6px rgba(0,0,0,.05)}
.main{flex:1;padding:22px;display:flex;flex-direction:column;gap:14px;font-size:13px;min-width:0}
.main h5{font-family:var(--serif);font-weight:400;font-size:28px;letter-spacing:-.02em}
.kpis{display:grid;grid-template-columns:repeat(3,1fr);gap:10px}
.kpi{border:1px solid var(--line);border-radius:12px;padding:12px}
.kpi strong{display:block;font-size:22px;margin-top:6px}
.kpi em{font-style:normal;font-size:11px;color:#18a058}
.chart{border:1px solid var(--line);border-radius:12px;padding:14px;flex:1;min-height:150px;display:flex;flex-direction:column}
.chart svg{flex:1;width:100%}
.rows{display:flex;flex-direction:column;gap:8px}
.row{display:flex;align-items:center;gap:10px;border:1px solid var(--line);border-radius:10px;padding:10px 12px}
.check{width:16px;height:16px;border-radius:5px;border:1.5px solid #ccc;flex:none}
.check.done{background:var(--ink);border-color:var(--ink)}
.pill{margin-left:auto;font-size:11px;padding:4px 8px;border-radius:10px;background:var(--bg);color:var(--grey);white-space:nowrap}
.pill.hot{background:var(--accent-08);color:var(--accent)}
.prompt{border:1px solid var(--line);border-radius:14px;padding:14px;color:#999;display:flex;justify-content:space-between;align-items:center}

/* TRUSTED */
.trusted{display:flex;align-items:center;gap:16px;margin-top:8px}
.trusted p{max-width:140px;color:var(--grey)}
.ticker{flex:1;overflow:hidden;border-radius:22px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);height:104px;display:flex;align-items:center;mask-image:linear-gradient(90deg,transparent,#000 10%,#000 90%,transparent)}
.ticker-track{display:flex;gap:100px;animation:scroll 30s linear infinite;width:max-content;align-items:center;color:#262626}
.ticker-track svg{height:22px;width:auto;flex:none}
@keyframes scroll{to{transform:translateX(-50%)}}

/* INTEGRATIONS — dark showcase */
@keyframes spin{to{transform:rotate(360deg)}}
.int{position:relative;overflow:hidden;isolation:isolate;border-radius:32px;background:#07090c;color:#fff;display:grid;grid-template-columns:1fr 1.05fr;align-items:center;gap:24px;padding:80px 0 80px 72px;min-height:660px;box-shadow:0 50px 90px -40px rgba(0,0,0,.45)}
.int-glow{position:absolute;inset:0;z-index:-1;pointer-events:none;
  background:radial-gradient(600px 600px at 76% 50%,rgba(225,246,244,.05),transparent 60%),radial-gradient(700px 500px at 0% 0%,rgba(7,88,138,.35),transparent 60%),radial-gradient(400px 300px at 100% 100%,rgba(225,246,244,.06),transparent 70%)}
.int-grid{position:absolute;inset:0;z-index:-1;pointer-events:none;background-image:radial-gradient(rgba(255,255,255,.08) 1px,transparent 1px);background-size:24px 24px;
  -webkit-mask-image:radial-gradient(ellipse 60% 70% at 72% 50%,#000 10%,transparent 70%);mask-image:radial-gradient(ellipse 60% 70% at 72% 50%,#000 10%,transparent 70%)}
.int-copy{position:relative;z-index:2;display:flex;flex-direction:column;gap:20px;align-items:flex-start;max-width:520px}
.tag.dark{background:rgba(255,255,255,.06);border-color:rgba(255,255,255,.12);color:rgba(255,255,255,.88)}
.int h2{font-size:66px;line-height:.98}
.int h2 em{font-style:italic;padding-right:.08em;background:linear-gradient(95deg,#ffc2b6 0%,#ff6a4f 45%,#ff462e 60%,#ffd9cf 100%);-webkit-background-clip:text;background-clip:text;color:transparent}
.int-copy p{color:rgba(255,255,255,.58);font-size:18px;line-height:1.45;max-width:420px}
.int-actions{display:flex;gap:10px;flex-wrap:wrap;margin-top:10px}
.int-ghost{height:48px;padding:0 22px;border-radius:999px;display:flex;align-items:center;color:#fff;font-size:14.5px;background:rgba(255,255,255,.05);box-shadow:inset 0 1px 0 rgba(255,255,255,.1),inset 0 0 0 1px rgba(255,255,255,.08);transition:background .3s}
.int-ghost:hover{background:rgba(255,255,255,.1)}
.int-stats{display:grid;grid-template-columns:repeat(3,auto);gap:36px;margin-top:30px;padding-top:30px;border-top:1px solid rgba(255,255,255,.08)}
.int-stats b{display:block;font-family:var(--serif);font-weight:400;font-size:36px;letter-spacing:-.02em;line-height:1}
.int-stats span{display:block;margin-top:8px;font-size:13px;color:rgba(255,255,255,.48)}
.int-visual{position:relative;width:118%;aspect-ratio:1;justify-self:start;margin:-8% 0}
.ring{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);border-radius:50%}
.track{position:absolute;inset:0;border-radius:50%;box-shadow:inset 0 0 0 1px rgba(255,255,255,.07);animation:spin var(--dur) linear infinite;animation-direction:var(--dir)}
.ring.dashed .track{box-shadow:none;border:1px dashed rgba(255,255,255,.09)}
.track .comet{position:absolute;left:50%;top:0;width:5px;height:5px;margin:-2.5px;border-radius:50%;background:#e1f6f4;box-shadow:0 0 10px 2px rgba(225,246,244,.35)}
.arm{position:absolute;inset:0;pointer-events:none}
.node{position:absolute;left:50%;top:0;width:var(--s);aspect-ratio:1;transform:translate(-50%,-50%) rotate(calc(var(--a)*-1));pointer-events:auto}
.tile{width:100%;height:100%;border-radius:30%;display:flex;align-items:center;justify-content:center;color:rgba(255,255,255,.88);
  background:linear-gradient(180deg,rgba(255,255,255,.11),rgba(255,255,255,.025));-webkit-backdrop-filter:blur(8px);backdrop-filter:blur(8px);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.2),inset 0 0 0 1px rgba(255,255,255,.07),0 14px 28px -10px rgba(0,0,0,.7);
  animation:spin var(--dur) linear infinite;animation-direction:var(--rdir);transition:color .35s,box-shadow .35s}
.tile svg{width:44%;height:44%}
.node:hover .tile{color:var(--c);box-shadow:inset 0 1px 0 rgba(255,255,255,.25),inset 0 0 0 1px var(--c),0 0 30px -4px var(--c)}
.int:hover .track,.int:hover .tile{animation-play-state:paused}
.hub{position:absolute;left:50%;top:50%;width:21%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:32%;display:flex;align-items:center;justify-content:center;
  background:linear-gradient(160deg,#fff,#f1f1f1);box-shadow:0 0 0 10px rgba(255,255,255,.04),0 0 0 22px rgba(255,255,255,.025),0 24px 50px -16px rgba(0,0,0,.7),inset 0 -3px 0 rgba(0,0,0,.06)}
.hub svg{width:46%;height:46%}
@keyframes pulse{from{transform:scale(1);opacity:.9}to{transform:scale(1.9);opacity:0}}

/* section header */
.sec-head{display:flex;justify-content:space-between;align-items:flex-end;gap:16px;margin-bottom:42px}
.sec-head .t{display:flex;flex-direction:column;gap:16px;align-items:flex-start;max-width:620px}
.sec-head .t p{max-width:500px;color:var(--grey)}
.stats{display:flex;gap:8px}
.stat{width:145px;padding:16px;border-radius:22px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);display:flex;flex-direction:column;gap:6px}

/* testimonials */
.masonry{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;align-items:start}
.col{display:flex;flex-direction:column;gap:8px}
.tcard{padding:24px;border-radius:22px;background:#fff;border:1px solid var(--line);box-shadow:var(--shadow);display:flex;flex-direction:column;gap:24px}
.tcard.primary{background:linear-gradient(145deg,#fff,var(--accent-soft));border-color:var(--accent-16)}
.tcard.dark{background:var(--ink);color:#fff;border:0}
.tcard .lg{display:flex;justify-content:space-between;align-items:center}
.tcard .lg svg.mk{width:32px;height:32px}
.tcard .lg.left{justify-content:flex-start;gap:24px}
.person{display:flex;align-items:center;gap:14px}
.portrait{width:74px;height:74px;border-radius:18px;flex:none;position:relative;overflow:hidden}
.portrait::before{content:"";position:absolute;width:44%;height:44%;left:28%;top:18%;border-radius:50%;background:rgba(255,255,255,.85)}
.portrait::after{content:"";position:absolute;width:80%;height:50%;left:10%;bottom:-14%;border-radius:50% 50% 0 0;background:rgba(255,255,255,.85)}
.person .nm{font-weight:600}
.person .rl{font-size:14px;color:var(--grey);margin-top:6px}

/* pricing */
.price-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:8px}
.pcard{padding:24px;border-radius:22px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);display:flex;flex-direction:column;gap:24px}
.pcard.primary{background:linear-gradient(145deg,#fff,var(--accent-soft));border-color:var(--accent-16)}
.pcard.dark{background:var(--ink);color:#fff;border:0}
.pcard .tp{display:flex;justify-content:space-between;align-items:center}
.picon{padding:10px;border-radius:10px;border:1px solid var(--bg);display:flex}
.pcard.primary .picon{border-color:var(--accent-16)}
.pcard.dark .picon{border-color:rgba(255,255,255,.1)}
.picon svg{width:32px;height:32px}
.price{display:flex;align-items:flex-end;gap:6px}
.price .amt{font-family:var(--serif);font-size:58px;letter-spacing:-.03em;line-height:1}
.price .per{font-weight:600;color:var(--grey);padding-bottom:6px}
.pcard.dark .price .per,.pcard.dark .desc{color:var(--muted)}
.toggle{display:inline-flex;align-items:center;gap:6px;padding:7px 12px 7px 7px;border-radius:18px;border:1px solid var(--bg);align-self:flex-start;font-weight:600;cursor:pointer;user-select:none}
.pcard.primary .toggle{border-color:var(--accent-16)}
.pcard.dark .toggle{border-color:rgba(255,255,255,.1)}
.sw{width:44px;padding:3px;border-radius:11px;background:var(--grey);display:flex;transition:background .25s}
.sw i{width:16px;height:16px;border-radius:50%;background:#fff;box-shadow:0 4px 8px rgba(0,0,0,.25);transition:transform .25s}
.pcard.dark .sw{background:var(--muted)}.pcard.dark .sw i{background:var(--ink)}
.annual .sw{background:var(--accent)}.annual .sw i{transform:translateX(22px)}
.flist{display:flex;flex-direction:column;gap:16px}
.flist div{display:flex;gap:6px;align-items:center}
.flist svg{width:16px;height:16px;flex:none}
.pcard .btn{justify-content:center}
.pcard.dark .btn{background:#fff;color:var(--ink)}
.perks{margin-top:8px;padding:24px;border-radius:22px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);display:flex;align-items:center;gap:24px}
.perks div{flex:1;display:flex;gap:6px;align-items:center;justify-content:center}
.perks svg{width:16px;height:16px}
.perks hr{border:0;width:1px;align-self:stretch;background:var(--bg)}

/* blog */
.post{display:flex;border-radius:22px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);overflow:hidden;transition:transform .3s}
.post:hover{transform:translateY(-3px)}
.post:hover .art{transform:scale(1.04)}
.post.big .imgbox{flex:1;height:540px}
.post .imgbox{border-radius:22px;overflow:hidden;position:relative}
.art{position:absolute;inset:0;transition:transform .6s}
.post.big .ct{flex:1;padding:24px;display:flex;flex-direction:column;justify-content:space-between}
.post .ct .top{display:flex;flex-direction:column;gap:16px;align-items:flex-start}
.post .bot{display:flex;justify-content:space-between;align-items:center}
.writer{display:flex;align-items:center;gap:8px}
.writer .portrait{width:42px;height:42px;border-radius:21px}
.rt{display:flex;align-items:center;gap:6px}
.rt i{width:6px;height:6px;border-radius:3px;background:var(--ink)}
.small-posts{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-top:8px}
.post.sm{flex-direction:column}
.post.sm .imgbox{height:380px}
.post.sm .ct{padding:24px;display:flex;flex-direction:column;gap:16px}
/* art pieces */
.art-blob{background:linear-gradient(160deg,#d7d7d9,#a9a9ae)}
.art-blob::before{content:"";position:absolute;width:52%;aspect-ratio:1;left:24%;top:24%;border-radius:42% 58% 60% 40%/45% 40% 60% 55%;background:conic-gradient(from 30deg,#ff6b4a,#ffcf5c,#5ce1c2,#5c8dff,#c35cff,#ff6b4a);filter:blur(1px);box-shadow:0 40px 60px rgba(0,0,0,.25);animation:morph 9s ease-in-out infinite}
.art-blob::after{content:"";position:absolute;width:30%;height:5%;left:35%;bottom:12%;border-radius:50%;background:rgba(0,0,0,.18);filter:blur(10px)}
@keyframes morph{50%{border-radius:58% 42% 40% 60%/55% 60% 40% 45%;transform:rotate(20deg) translateY(-10px)}}
.art-robot{background:radial-gradient(circle at 50% 40%,#e9e9ea,#9a9aa0)}
.art-blue{background:linear-gradient(180deg,#0c2a6b,#123f9e)}
.art-jelly{background:radial-gradient(circle at 50% 30%,#2a1b4d,#0c0a1f)}

/* FAQ */
.faq{display:flex;gap:42px}
.faq-l{flex:1;display:flex;flex-direction:column;justify-content:space-between;gap:24px}
.faq-l .top,.faq-l .bottom{display:flex;flex-direction:column;gap:16px;align-items:flex-start}
.faq-r{width:60%;display:flex;flex-direction:column;gap:8px}
.qa{border-radius:10px;background:#fff;border:1px solid var(--bg);box-shadow:var(--shadow);padding:24px;cursor:pointer;transition:background .3s,border-color .3s}
.qa.open{background:linear-gradient(145deg,#fff,var(--accent-soft));border-color:var(--accent-16)}
.qa .q{display:flex;justify-content:space-between;gap:16px;align-items:center;font-size:19px}
.pm{width:16px;height:16px;position:relative;flex:none}
.pm::before,.pm::after{content:"";position:absolute;left:0;top:7px;width:16px;height:2px;border-radius:1px;background:var(--ink);transition:transform .3s}
.pm::before{transform:rotate(90deg)}
.qa.open .pm::before{transform:rotate(0)}
.qa .a{display:grid;grid-template-rows:0fr;transition:grid-template-rows .35s}
.qa .a p{overflow:hidden;color:var(--grey);line-height:1.35}
.qa.open .a{grid-template-rows:1fr}
.qa.open .a p{padding-top:16px}

/* CTA */
/* CTA — floats over the top of the footer panel */
.cta{position:relative;z-index:2;padding:100px 40px 0;max-width:1300px;margin:0 auto -240px}
.cta-card{position:relative;z-index:1;border-radius:30px;overflow:hidden;padding:110px 40px;display:flex;flex-direction:column;align-items:center;gap:16px;color:#fff;text-align:center;
  box-shadow:0 60px 120px -40px rgba(2,16,30,.75),0 0 0 1px rgba(255,255,255,.1)}
.cta-card > *:not(.sky){position:relative;z-index:1}

/* FOOTER — dark panel joined to the CTA */
.foot-wrap{position:relative;margin:0 12px 12px;border-radius:40px;background:#07090c;color:#fff;overflow:hidden;isolation:isolate}
.foot-wrap::before{content:"";position:absolute;inset:0;z-index:-1;pointer-events:none;
  background:radial-gradient(1000px 460px at 50% 0%,rgba(140,205,225,.22),transparent 70%),radial-gradient(700px 500px at 0% 100%,rgba(7,88,138,.28),transparent 70%),radial-gradient(500px 400px at 100% 90%,rgba(225,246,244,.05),transparent 70%)}
.foot{max-width:1300px;margin:0 auto;padding:340px 56px 0;display:flex;flex-direction:column;gap:64px}
.foot-top{display:flex;justify-content:space-between;align-items:flex-end;gap:40px;padding-bottom:56px;border-bottom:1px solid rgba(255,255,255,.08)}
.foot .logo{color:#fff}
.tagline{font-family:var(--serif);font-weight:400;font-size:52px;letter-spacing:-.025em;line-height:1;margin-top:28px}
.tagline em{color:#bfe3ef}
.addr{margin-top:14px;color:rgba(255,255,255,.45);font-size:14px}
.news{max-width:440px;width:100%;display:flex;flex-direction:column;gap:14px}
.eyebrow{font-size:11px;font-weight:500;letter-spacing:.14em;text-transform:uppercase;color:rgba(255,255,255,.4)}
.news p{color:rgba(255,255,255,.6);line-height:1.45}
.news-form{display:flex;align-items:center;gap:8px;height:60px;padding:6px 6px 6px 22px;border-radius:999px;background:rgba(255,255,255,.05);box-shadow:inset 0 1px 0 rgba(255,255,255,.08),inset 0 0 0 1px rgba(255,255,255,.08);transition:box-shadow .3s}
.news-form:focus-within{box-shadow:inset 0 0 0 1px rgba(191,227,239,.55),0 0 0 5px rgba(191,227,239,.08)}
.news-form input{flex:1;min-width:0;border:0;background:none;outline:none;font:inherit;color:#fff}
.news-form input::placeholder{color:rgba(255,255,255,.35)}
.news-form .nav-cta{font-family:inherit;cursor:pointer}
.foot-cols{display:grid;grid-template-columns:repeat(3,1fr) 1.3fr;gap:32px}
.foot-cols h6{font-size:11px;font-weight:500;letter-spacing:.14em;text-transform:uppercase;color:rgba(255,255,255,.4);margin-bottom:16px}
.fl{position:relative;display:block;width:fit-content;padding:7px 0;color:rgba(255,255,255,.78);transition:color .25s}
.fl::after{content:"";position:absolute;left:0;bottom:4px;width:100%;height:1px;background:currentColor;transform:scaleX(0);transform-origin:right;transition:transform .45s cubic-bezier(.2,.8,.2,1)}
.fl:hover{color:#fff}.fl:hover::after{transform:scaleX(1);transform-origin:left}
.socials{display:flex;gap:8px}
.socials a{width:46px;height:46px;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;background:rgba(255,255,255,.05);box-shadow:inset 0 1px 0 rgba(255,255,255,.1),inset 0 0 0 1px rgba(255,255,255,.08);transition:background .3s,color .3s,transform .3s}
.socials a:hover{background:#fff;color:#0c0c0c;transform:translateY(-2px)}
.socials svg{width:18px;height:18px}
.sys-status{display:inline-flex;align-items:center;gap:8px;margin-top:20px;padding:8px 14px;border-radius:999px;font-size:13px;color:#a6f0cc;background:rgba(61,220,151,.07);box-shadow:inset 0 0 0 1px rgba(61,220,151,.2)}
.sys-status::before{content:"";width:6px;height:6px;border-radius:50%;background:#3ddc97;box-shadow:0 0 8px #3ddc97}
.foot-bar{display:flex;justify-content:space-between;align-items:center;gap:16px;padding-top:24px;border-top:1px solid rgba(255,255,255,.08);font-size:13px;color:rgba(255,255,255,.45)}
.foot-bar a{color:rgba(255,255,255,.78);transition:color .25s}.foot-bar a:hover{color:#fff}
.foot-bar .legal{display:flex;gap:22px;flex-wrap:wrap}
.top-btn{display:inline-flex;align-items:center;gap:10px}
.top-btn i{width:34px;height:34px;border-radius:50%;display:flex;align-items:center;justify-content:center;box-shadow:inset 0 0 0 1px rgba(255,255,255,.16);transition:background .3s,color .3s,transform .4s cubic-bezier(.2,.8,.2,1)}
.top-btn i svg{width:14px;height:14px}
.top-btn:hover i{background:#fff;color:#0c0c0c;transform:translateY(-2px)}
.wordmark{font-family:var(--serif);font-style:italic;font-size:clamp(110px,27vw,400px);line-height:.85;text-align:center;letter-spacing:-.035em;margin:-28px -20px -.2em;padding-right:.06em;user-select:none;
  background:linear-gradient(180deg,rgba(225,246,244,.5) 0%,rgba(140,200,225,.16) 50%,rgba(255,255,255,0) 82%);-webkit-background-clip:text;background-clip:text;color:transparent}

.reveal{opacity:0;transform:translateY(20px);transition:opacity .8s cubic-bezier(.2,.8,.2,1),transform .8s cubic-bezier(.2,.8,.2,1)}
.reveal.in{opacity:1;transform:none}

/* RESPONSIVE */
@media (max-width:1199px){
  h1{font-size:60px} h2{font-size:48px} h3{font-size:26px}
  .nav-links{display:none}.menu-btn{display:block}.menu-panel{display:block}
  .int{grid-template-columns:1fr;padding:64px 48px 0;gap:0}
  .int-copy{max-width:640px}
  .int-visual{width:100%;max-width:640px;justify-self:center;margin:24px 0 -26%}
  .int-grid{-webkit-mask-image:radial-gradient(ellipse 80% 50% at 50% 80%,#000 10%,transparent 70%);mask-image:radial-gradient(ellipse 80% 50% at 50% 80%,#000 10%,transparent 70%)}
  .int-glow{background:radial-gradient(600px 500px at 50% 85%,rgba(225,246,244,.05),transparent 60%),radial-gradient(700px 500px at 0% 0%,rgba(7,88,138,.35),transparent 60%)}
  .process,.faq{flex-direction:column}
  .foot{padding:320px 40px 0}
  .foot-cols{grid-template-columns:repeat(3,1fr)}
  .foot-cols .connect{grid-column:span 3}
  .proc-visual,.faq-r{width:100%}
  .sec-head{flex-direction:column;align-items:flex-start}
  .masonry,.price-grid{grid-template-columns:repeat(2,1fr)}
  .price-grid .pcard:last-child{grid-column:span 2}
  .small-posts{grid-template-columns:repeat(2,1fr)}
  .small-posts .post:last-child{grid-column:span 2}
  .post.big{flex-direction:column}.post.big .imgbox{flex:none;height:400px}
}
@media (max-width:809px){
  h1{font-size:48px} h2{font-size:38px} h3{font-size:24px} .lead{font-size:19px}
  .wrap{padding:40px 20px}
  .nav{padding:12px 12px 0}
  .nav-right>.nav-cta{display:none}
  .nav-inner{height:60px;padding:0 6px 0 18px}
  .nav.scrolled .nav-inner,.nav.open .nav-inner{height:60px}
  .mi{font-size:30px}
  .int{padding:44px 24px 0;border-radius:26px}
  .int h2{font-size:44px}
  .int-stats{gap:18px;width:100%}
  .int-stats b{font-size:26px}
  .int-visual{width:112%;max-width:none;margin:28px 0 -30%}
  .hero{padding:8px 8px 0}
  .hero-content{padding:160px 20px 0}
  .cta-row{flex-direction:column;align-items:center}
  .phones{height:300px}
  .phone{width:170px;height:350px;border-radius:30px;padding:7px;top:20px}
  .phone.left{left:4%}.phone.right{right:4%;top:36px}
  .screen{border-radius:24px;zoom:.57}
  .proc-visual{height:310px}
  .slide{inset:16px 16px 0}
  .side{display:none}
  .trusted{flex-direction:column;align-items:flex-start}
  .trusted p{max-width:none}.ticker{width:100%}
  .stats{width:100%}.stat{flex:1;width:auto}
  .masonry,.price-grid,.small-posts{grid-template-columns:1fr}
  .price-grid .pcard:last-child,.small-posts .post:last-child{grid-column:auto}
  .perks{flex-direction:column;align-items:flex-start}.perks hr{display:none}.perks div{justify-content:flex-start}
  .post.big .bot{flex-direction:column;align-items:flex-start;gap:16px}
  .cta{padding:40px 20px 0;margin-bottom:-170px}.cta-card{padding:84px 20px;border-radius:24px}
  .foot-wrap{margin:0 8px 8px;border-radius:28px}
  .foot{padding:230px 22px 0;gap:44px}
  .foot-top{flex-direction:column;align-items:flex-start;padding-bottom:40px}
  .tagline{font-size:40px}
  .foot-cols{grid-template-columns:repeat(2,1fr);gap:28px 16px}
  .foot-cols .connect{grid-column:auto}
  .foot-bar{flex-direction:column;align-items:flex-start}
  .wordmark{margin-top:-10px}
}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}.reveal,.fade-up{opacity:1;transform:none}}
</style>
</head>
<body>

<!-- reusable icon sprites -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="i-bolt" viewBox="0 0 24 24"><path class="ico" d="M15 1.5 13.5 9l6 2.25L9 22.5l1.5-7.5-6-2.25Z"/></symbol>
    <symbol id="i-spark" viewBox="0 0 24 24"><path class="ico" d="M7.9 16.1 2.7 14.2a.75.75 0 0 1 0-1.4l5.2-1.9 1.9-5.2a.75.75 0 0 1 1.4 0l1.9 5.2 5.2 1.9a.75.75 0 0 1 0 1.4l-5.2 1.9-1.9 5.2a.75.75 0 0 1-1.4 0ZM16.5 1.5V6M21 6.75v3M14.25 3.75h4.5M19.5 8.25h3"/></symbol>
    <symbol id="i-list" viewBox="0 0 24 24"><path class="ico" d="M3.75 6h16.5M3.75 12H9M3.75 18h6.75M17.25 16.4 20 18l-.7-3.1 2.4-2-3.2-.3-1.3-2.9-1.2 2.9-3.3.3 2.5 2-.8 3.1Z"/></symbol>
    <symbol id="i-arrow" viewBox="0 0 24 24"><path class="ico" d="M3.75 12h9.75M13.5 5.25 20.25 12l-6.75 6.75Z"/></symbol>
    <symbol id="i-badge" viewBox="0 0 24 24"><path class="ico" d="M5.1 18.9c-.9-.9-.3-2.7-.7-3.7S2.25 13.2 2.25 12s1.7-2.1 2.1-3.2-.2-2.9.7-3.7 2.7-.3 3.7-.7S10.8 2.25 12 2.25s2.1 1.7 3.2 2.1 2.9-.2 3.7.7.3 2.7.7 3.7 2.1 1.9 2.1 3.2-1.7 2.1-2.1 3.2.2 2.9-.7 3.7-2.7.3-3.7.7-1.9 2.1-3.2 2.1-2.1-1.7-3.2-2.1-2.9.2-3.7-.7ZM8.25 12.75 10.5 15l5.25-5.25"/></symbol>
    <symbol id="i-check" viewBox="0 0 24 24"><rect x="2.25" y="3.75" width="19.5" height="16.5" rx="1.5" fill="currentColor" opacity=".08"/><path class="ico" d="m6 12.75 3.75 3.75 9-9"/></symbol>
    <symbol id="i-tag" viewBox="0 0 24 24"><path class="ico" d="M8.25 6h12M8.25 12h12M8.25 18h12"/><circle cx="4.1" cy="6" r="1.1" fill="currentColor"/><circle cx="4.1" cy="12" r="1.1" fill="currentColor"/><circle cx="4.1" cy="18" r="1.1" fill="currentColor"/></symbol>
    <symbol id="i-rocket" viewBox="0 0 24 24"><path class="ico" d="M17.9 10.6c2.3-2.3 2.4-4.9 2.3-6.1a.75.75 0 0 0-.7-.7c-1.2-.1-3.8.1-6.1 2.3L7.5 12l4.5 4.5ZM12.75 6.75H7l-4 4 4.5.7M17.25 11.25V17l-4 4-.7-4.5M8.9 17.6c-.4.8-1.6 2.6-5.1 2.6 0-3.5 1.8-4.7 2.6-5.1"/></symbol>
    <symbol id="i-crown" viewBox="0 0 24 24"><path class="ico" d="m3.7 9.35 1.5 8.8c.1.35.4.6.7.6h12.2c.4 0 .7-.25.8-.6l1.4-8.8M11.25 6.6l-3 6.9-3.7-4.5M12.75 6.6l3 6.9 3.7-4.5"/><circle cx="12" cy="4.9" r="1.9" class="ico"/><circle cx="20.6" cy="7.5" r="1.9" class="ico"/><circle cx="3.4" cy="7.5" r="1.9" class="ico"/></symbol>
    <symbol id="i-sliders" viewBox="0 0 24 24"><path class="ico" d="M12 7.5h8.25M3.75 7.5h3.75M18 16.5h2.25M3.75 16.5h9.75"/><circle cx="9.75" cy="7.5" r="2.25" class="ico"/><circle cx="15.75" cy="16.5" r="2.25" class="ico"/></symbol>
    <symbol id="i-pause" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" class="ico"/><path class="ico" d="M9.75 9v6M14.25 9v6"/></symbol>
    <symbol id="i-clock" viewBox="0 0 24 24"><path class="ico" d="M21 12.75A9 9 0 1 1 11.25 3M12 6.75V12h5.25"/><circle cx="15" cy="3.4" r="1.1" fill="currentColor"/><circle cx="18.4" cy="5.6" r="1.1" fill="currentColor"/><circle cx="20.6" cy="9" r="1.1" fill="currentColor"/></symbol>
    <symbol id="i-book" viewBox="0 0 24 24"><path class="ico" d="M15.75 21 10.5 17.25 5.25 21V6.75c0-.4.3-.75.75-.75h9c.4 0 .75.35.75.75ZM8.25 3h9.75c.4 0 .75.35.75.75V18"/></symbol>
    <symbol id="i-q" viewBox="0 0 24 24"><path class="ico" d="M5.1 18.9c-.9-.9-.3-2.7-.7-3.7S2.25 13.2 2.25 12s1.7-2.1 2.1-3.2-.2-2.9.7-3.7 2.7-.3 3.7-.7S10.8 2.25 12 2.25s2.1 1.7 3.2 2.1 2.9-.2 3.7.7.3 2.7.7 3.7 2.1 1.9 2.1 3.2-1.7 2.1-2.1 3.2.2 2.9-.7 3.7-2.7.3-3.7.7-1.9 2.1-3.2 2.1-2.1-1.7-3.2-2.1-2.9.2-3.7-.7ZM12 13.5v-.75c1.7 0 3-1.2 3-2.6s-1.3-2.65-3-2.65-3 1.2-3 2.6"/><circle cx="12" cy="17" r="1.1" fill="currentColor"/></symbol>
    <symbol id="i-chat" viewBox="0 0 24 24"><path class="ico" d="M12.4 20.25H4.5a.75.75 0 0 1-.75-.75v-7.9A8.6 8.6 0 0 1 12.4 3a8.6 8.6 0 0 1 8.6 8.6 8.6 8.6 0 0 1-8.6 8.65Z"/><circle cx="12.4" cy="12" r="1.1" fill="currentColor"/><circle cx="8.25" cy="12" r="1.1" fill="currentColor"/><circle cx="16.5" cy="12" r="1.1" fill="currentColor"/></symbol>
    <symbol id="i-x" viewBox="0 0 24 24"><path class="ico" d="M4.5 3.75H9l10.5 16.5H15ZM10.7 13.2 4.5 20M19.5 3.75l-6.2 6.8"/></symbol>
    <symbol id="i-ig" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="4.5" class="ico"/><circle cx="12" cy="12" r="3.75" class="ico"/><circle cx="16.9" cy="7.1" r="1.1" fill="currentColor"/></symbol>
    <symbol id="i-in" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx=".75" class="ico"/><path class="ico" d="M8.25 10.5v6M11.25 10.5v6M11.25 13.1a2.6 2.6 0 0 1 5.25 0v3.4"/><circle cx="8.25" cy="7.9" r="1.1" fill="currentColor"/></symbol>
  </defs>
</svg>

<!-- NAV -->
<nav class="nav" id="nav" data-section="nav">
  <div class="nav-inner">
    <a href="#hero" class="logo" aria-label="Nimbus home">
      <svg class="logo-mark" viewBox="0 0 32 32"><defs><linearGradient id="lm" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fff"/><stop offset="1" stop-color="#e9eef2"/></linearGradient></defs><circle cx="16" cy="16" r="16" fill="url(#lm)"/><circle cx="16" cy="16" r="10.5" fill="none" stroke="#ff462e" stroke-opacity=".22"/><path d="M16 8.5c.55 4 2.5 5.95 6.5 6.5-4 .55-5.95 2.5-6.5 6.5-.55-4-2.5-5.95-6.5-6.5 4-.55 5.95-2.5 6.5-6.5Z" fill="#ff462e"/></svg>
      Nimbus
    </a>
    <div class="nav-links" id="navLinks">
      <span class="nav-hl" id="navHl"></span>
      <a href="#process">Process</a><a href="#features">Integrations</a><a href="#testimonials">Customers</a><a href="#pricing">Pricing</a><a href="#blog">Journal</a>
    </div>
    <div class="nav-right">
      <a href="#pricing" class="nav-cta">Get started<span class="arr"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <button class="menu-btn" id="menuBtn" aria-label="Open menu" aria-expanded="false" aria-controls="menuPanel"><span></span><span></span></button>
    </div>
    <div class="menu-panel" id="menuPanel">
      <div class="menu-label"><span>Navigate</span><i>All systems normal</i></div>
      <a class="mi" href="#process" style="--i:0"><small>01</small>Process<span class="go"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a class="mi" href="#features" style="--i:1"><small>02</small>Integrations<span class="go"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a class="mi" href="#testimonials" style="--i:2"><small>03</small>Customers<span class="go"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a class="mi" href="#pricing" style="--i:3"><small>04</small>Pricing<span class="go"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <a class="mi" href="#blog" style="--i:4"><small>05</small>Journal<span class="go"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
      <div class="menu-foot">
        <a href="#pricing" class="nav-cta mi-link">Start a 14-day trial<span class="arr"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
        <a href="#" class="ghost mi-link">Sign in</a>
      </div>
    </div>
  </div>
</nav>
<div class="nav-scrim" id="navScrim"></div>

<main>
<!-- HERO -->
<section class="hero" id="hero" data-section="hero">
  <div class="hero-card">
    <div class="sky" aria-hidden="true"><canvas class="bg-canvas"></canvas></div>
    <div class="hero-content">
      <div class="hero-text">
        <div class="badge-logo fade-up"><div><svg viewBox="0 0 32 32"><path d="M16 4c.8 5.9 3.6 8.7 9.5 9.5-5.9.8-8.7 3.6-9.5 9.5-.8-5.9-3.6-8.7-9.5-9.5C12.4 12.7 15.2 9.9 16 4Z" fill="#ff462e"/><circle cx="25" cy="24" r="2.5" fill="#0c0c0c"/></svg></div></div>
        <h1 class="fade-up d1">Stop Switching Tools — One AI Assistant That Does It All.</h1>
        <p class="lead fade-up d2">Fast, accurate responses designed to enhance every conversation.</p>
        <div class="cta-row fade-up d3">
          <a href="#pricing" class="btn btn-dark"><svg><use href="#i-bolt"/></svg>Start a 14-day trial</a>
          <a href="#process" class="btn btn-light">Learn more</a>
        </div>
      </div>
      <div class="phones fade-up d4" role="img" aria-label="Two phones running Nimbus: a chat summarising customer feedback, and a home screen with a weekly focus chart">
        <!-- phone 1: chat -->
        <div class="phone left"><div class="screen">
          <div class="notch"></div>
          <div class="status"><span>9:41</span><span>●●● ▮</span></div>
          <div class="app-head"><div class="av"><svg><use href="#i-spark"/></svg></div><div><div style="font-weight:600;font-size:13px">Nimbus</div><div style="font-size:11px;color:#18a058">● Online</div></div></div>
          <div class="chat">
            <div class="b me">Summarize this week's customer feedback into 3 themes.</div>
            <div class="b ai"><b>Here's what stood out:</b><br>1. Faster onboarding requests<br>2. Praise for the new search<br>3. Pricing page confusion</div>
            <div class="b me">Draft a reply for theme 3.</div>
            <div class="b ai typing"><i></i><i></i><i></i></div>
          </div>
          <div class="inputbar">Ask anything… <span class="send"></span></div>
        </div></div>
        <!-- phone 2: home -->
        <div class="phone right"><div class="screen">
          <div class="notch"></div>
          <div class="status"><span>9:41</span><span>●●● ▮</span></div>
          <div class="home-screen">
            <div class="greet">Good morning,<br>Milo.</div>
            <div class="chips"><span class="chip">✍️ Write</span><span class="chip">📊 Analyze</span><span class="chip">🧠 Brainstorm</span><span class="chip">📅 Plan</span></div>
            <div class="mini-card" style="background:linear-gradient(135deg,#ff6b4a,#ff462e)"><b>Weekly focus</b><br>You saved 6.4 hrs this week<div class="bars"><i style="height:40%"></i><i style="height:65%"></i><i style="height:50%"></i><i style="height:85%"></i><i style="height:70%"></i><i style="height:100%"></i><i style="height:60%"></i></div></div>
            <div class="mini-card" style="background:#0c0c0c"><b>Up next</b><br>Product sync · 11:00<br><span style="opacity:.6">Briefing ready ✓</span></div>
          </div>
        </div></div>
      </div>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section class="wrap" id="process" data-section="process" style="padding-bottom:40px">
  <div class="process">
    <div class="proc-text reveal">
      <div class="top">
        <span class="tag"><svg><use href="#i-list"/></svg>Process</span>
        <h2>Smarter tools, better results.</h2>
        <p class="grey" style="max-width:500px">Unlock powerful AI capabilities designed to help you work faster and smarter.</p>
        <div class="ctrl">
          <button id="prev" aria-label="Previous" style="opacity:.7"><svg style="transform:rotate(180deg)"><use href="#i-arrow"/></svg></button>
          <button id="next" aria-label="Next"><svg><use href="#i-arrow"/></svg></button>
        </div>
      </div>
      <div class="dots" id="dots"><i class="on"></i><i></i><i></i></div>
    </div>
    <div class="proc-visual reveal">
      <!-- slide 1: chat workspace -->
      <div class="slide on">
        <div class="side"><b><svg width="18" height="18" style="color:#ff462e"><use href="#i-spark"/></svg>Nimbus</b><span class="act">Assistant</span><span>Insights</span><span>Tasks</span><span>Library</span><span>Settings</span></div>
        <div class="main">
          <h5>Ask. Get answers.</h5>
          <div class="chat" style="padding:0;flex:none">
            <div class="b me">Create a launch checklist for our new feature.</div>
            <div class="b ai">Done! I grouped 14 steps into <b>Prep</b>, <b>Launch day</b> and <b>Follow-up</b>, and assigned owners based on last sprint.</div>
            <div class="b me">Share it with the team.</div>
            <div class="b ai">Shared in #launch ✓ — 3 teammates have viewed it.</div>
          </div>
          <div style="flex:1"></div>
          <div class="prompt">Message Nimbus… <span class="send"></span></div>
        </div>
      </div>
      <!-- slide 2: insights -->
      <div class="slide">
        <div class="side"><b><svg width="18" height="18" style="color:#ff462e"><use href="#i-spark"/></svg>Nimbus</b><span>Assistant</span><span class="act">Insights</span><span>Tasks</span><span>Library</span><span>Settings</span></div>
        <div class="main">
          <h5>Insights</h5>
          <div class="kpis">
            <div class="kpi grey">Queries<strong style="color:#0c0c0c">12.4k</strong><em>▲ 18%</em></div>
            <div class="kpi grey">Time saved<strong style="color:#0c0c0c">142h</strong><em>▲ 24%</em></div>
            <div class="kpi grey">Accuracy<strong style="color:#0c0c0c">97.2%</strong><em>▲ 2%</em></div>
          </div>
          <div class="chart"><span class="grey">Weekly activity</span>
            <svg viewBox="0 0 400 140" preserveAspectRatio="none"><defs><linearGradient id="g1" x1="0" x2="0" y1="0" y2="1"><stop offset="0" stop-color="#ff462e" stop-opacity=".3"/><stop offset="1" stop-color="#ff462e" stop-opacity="0"/></linearGradient></defs><path d="M0 110 C40 100 60 70 100 75 S160 40 200 50 S260 20 300 30 S360 10 400 15 V140 H0Z" fill="url(#g1)"/><path d="M0 110 C40 100 60 70 100 75 S160 40 200 50 S260 20 300 30 S360 10 400 15" fill="none" stroke="#ff462e" stroke-width="2.5"/><path d="M0 125 C50 120 90 105 140 108 S230 90 280 92 S360 80 400 78" fill="none" stroke="#0c0c0c" stroke-width="2" stroke-dasharray="5 5" opacity=".4"/></svg>
          </div>
        </div>
      </div>
      <!-- slide 3: tasks -->
      <div class="slide">
        <div class="side"><b><svg width="18" height="18" style="color:#ff462e"><use href="#i-spark"/></svg>Nimbus</b><span>Assistant</span><span>Insights</span><span class="act">Tasks</span><span>Library</span><span>Settings</span></div>
        <div class="main">
          <h5>Automations</h5>
          <div class="rows">
            <div class="row"><span class="check done"></span>Summarize inbox every morning<span class="pill">Daily · 8:00</span></div>
            <div class="row"><span class="check done"></span>Draft replies to support tickets<span class="pill hot">Live</span></div>
            <div class="row"><span class="check"></span>Weekly metrics report to #team<span class="pill">Fridays</span></div>
            <div class="row"><span class="check"></span>Translate release notes (5 languages)<span class="pill">On release</span></div>
            <div class="row"><span class="check done"></span>Tag and route new leads<span class="pill hot">Live</span></div>
          </div>
          <div class="prompt">+ Describe a new automation…</div>
        </div>
      </div>
    </div>
  </div>
  <div class="trusted reveal" style="margin-top:42px">
    <p>Chosen by teams that scale quickly.</p>
    <div class="ticker"><div class="ticker-track" id="ticker">
      <svg viewBox="0 0 120 22"><circle cx="11" cy="11" r="9" fill="none" stroke="currentColor" stroke-width="4"/><text x="28" y="17" font-family="Inter" font-weight="700" font-size="17" fill="currentColor">Orbitly</text></svg>
      <svg viewBox="0 0 120 22"><path d="M2 20 11 2l9 18Z" fill="currentColor"/><text x="26" y="17" font-family="Inter" font-weight="700" font-size="17" fill="currentColor">Peakform</text></svg>
      <svg viewBox="0 0 110 22"><rect x="1" y="1" width="9" height="9" rx="2" fill="currentColor"/><rect x="12" y="12" width="9" height="9" rx="2" fill="currentColor"/><text x="28" y="17" font-family="Inter" font-weight="700" font-size="17" fill="currentColor">Blockr</text></svg>
      <svg viewBox="0 0 120 22"><path d="M2 11c4-9 8-9 10 0s6 9 10 0" fill="none" stroke="currentColor" stroke-width="3.5" stroke-linecap="round"/><text x="30" y="17" font-family="Inter" font-weight="700" font-size="17" fill="currentColor">Wavelet</text></svg>
      <svg viewBox="0 0 110 22"><path d="M11 1v20M1 11h20M4 4l14 14M18 4 4 18" stroke="currentColor" stroke-width="3" stroke-linecap="round"/><text x="28" y="17" font-family="Inter" font-weight="700" font-size="17" fill="currentColor">Novalux</text></svg>
    </div></div>
  </div>
</section>

<!-- FEATURES -->
<section class="wrap" id="features" data-section="integrations" style="padding-top:60px;padding-bottom:40px">
  <div class="int reveal">
    <div class="int-glow"></div>
    <div class="int-grid"></div>
    <div class="int-copy">
      <span class="tag dark"><svg><use href="#i-spark"/></svg>Integrations</span>
      <h2>Seamlessly connect your <em>favorite tools.</em></h2>
      <p>Integrate the apps and services you already use to streamline workflows.</p>
      <div class="int-actions">
        <a href="#pricing" class="nav-cta">Get started<span class="arr"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></a>
        <a href="#" class="int-ghost">Browse the directory</a>
      </div>
      <div class="int-stats">
        <div><b>200+</b><span>Native integrations</span></div>
        <div><b>2 min</b><span>Average setup</span></div>
        <div><b>SOC 2</b><span>Type II secured</span></div>
      </div>
    </div>
    <div class="int-visual" id="intVisual" role="img" aria-label="The Nimbus mark at the centre of three rings of connected tools">
      <div class="hub"><svg viewBox="0 0 32 32"><path d="M16 4c.8 5.9 3.6 8.7 9.5 9.5-5.9.8-8.7 3.6-9.5 9.5-.8-5.9-3.6-8.7-9.5-9.5C12.4 12.7 15.2 9.9 16 4Z" fill="#ff462e"/><circle cx="25" cy="24" r="2.5" fill="#0c0c0c"/></svg></div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="wrap" id="testimonials" data-section="testimonials">
  <div class="sec-head reveal">
    <div class="t">
      <span class="tag"><svg><use href="#i-badge"/></svg>Verified customer outcomes</span>
      <h2>Teams ship better work with Nimbus.</h2>
      <p>Short success stories from operators, founders, and product teams using AI where speed and quality matter most.</p>
    </div>
    <div class="stats">
      <div class="stat"><h3>41%</h3><span class="small grey">fewer support handoffs</span></div>
      <div class="stat"><h3>2.6×</h3><span class="small grey">faster research cycles</span></div>
    </div>
  </div>
  <div class="masonry" id="masonry">
    <div class="col">
      <div class="tcard primary reveal">
        <div class="lg"><svg class="mk" style="color:#ff462e" viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" class="ico"/><path class="ico" d="M12 3l3.4 9.6M4.2 7.5l10 1.8M4.2 8.7l6.6 7.8M8.6 14.4 12 21M9.7 17.7l10.1-1.8M19.8 7.5l-6.6 7.8"/></svg><span class="tag soft"><svg><use href="#i-check"/></svg>Verified</span></div>
        <div><h2>18 hrs</h2><p class="grey" style="margin-top:6px">saved per product sprint</p></div>
        <p class="lead">“Nimbus turned scattered research into decisions we could trust. We now brief stakeholders in minutes, not days.”</p>
        <div class="person"><div class="portrait" style="background:linear-gradient(135deg,#f7b267,#f4845f)"></div><div><div class="nm">Noah Bennett</div><div class="rl">Founder · Series A SaaS</div></div></div>
      </div>
      <div class="tcard reveal">
        <div class="lg left"><svg class="mk" viewBox="0 0 24 24"><path class="ico" d="M11.25 1.5v9l-9 2.25 9 2.25v9l2.25-9 9-2.25-9-2.25Z"/></svg><svg class="mk" viewBox="0 0 24 24"><rect x="3.75" y="3.75" width="11.25" height="11.25" class="ico"/><rect x="9" y="9" width="11.25" height="11.25" class="ico"/></svg><svg class="mk" viewBox="0 0 24 24"><path class="ico" d="M12 18.75s3.75-2 3.75-7.6c0-4.3-2.3-6.5-3.3-7.3a.75.75 0 0 0-.9 0c-1 .8-3.3 3-3.3 7.3 0 5.6 3.75 7.6 3.75 7.6ZM12 18.75c1.4 0 3.8 0 6.6-1.7s3.6-3.7 3.9-4.7a.75.75 0 0 0-.5-.9 7 7 0 0 0-2.9-.1M12 18.75c-1.4 0-3.8 0-6.6-1.7S1.8 13.3 1.5 12.3a.75.75 0 0 1 .5-.9 7 7 0 0 1 2.9-.1"/></svg></div>
        <p class="lead">Adopted by product teams who need confident answers, cleaner workflows, and faster customer follow-up.</p>
      </div>
    </div>
    <div class="col">
      <div class="tcard reveal">
        <div class="lg"><svg class="mk" viewBox="0 0 24 24"><path class="ico" d="M12 2.25 15.75 6 12 9.75 8.25 6ZM12 14.25 15.75 18 12 21.75 8.25 18ZM18 8.25 21.75 12 18 15.75 14.25 12ZM6 8.25 9.75 12 6 15.75 2.25 12Z"/></svg><span class="tag plain">Ops</span></div>
        <p class="lead">“The team finally has one reliable place to draft, compare, and approve client responses.”</p>
        <div class="person"><div class="portrait" style="background:linear-gradient(135deg,#7f9cf5,#5a67d8)"></div><div><div class="nm">Ethan Parker</div><div class="rl">Head of Product</div></div></div>
      </div>
      <div class="tcard reveal">
        <div class="lg"><svg class="mk" viewBox="0 0 24 24"><path class="ico" d="M3.75 3.75v16.5M7.5 5.25h10.5v5.25H7.5ZM7.5 13.5h13.5v5.25H7.5Z"/></svg><span class="tag plain">Support</span></div>
        <p class="lead">“The biggest shift was confidence: answers are consistent, even when the queue is busy.”</p>
        <div class="person"><div class="portrait" style="background:linear-gradient(135deg,#68d391,#2f855a)"></div><div><div class="nm">Lucas Bennett</div><div class="rl">Customer Experience Lead</div></div></div>
      </div>
    </div>
    <div class="col">
      <div class="tcard dark reveal" style="gap:24px">
        <div class="lg"><svg class="mk" viewBox="0 0 24 24" style="color:#fff"><path class="ico" d="M10 14.3l-.8.9a4.5 4.5 0 1 1 0-6.4l5.6 6.4a4.5 4.5 0 1 0 0-6.4l-.8.9"/></svg><svg width="24" height="24" style="color:#ff462e"><use href="#i-badge"/></svg></div>
        <div><h2 style="color:#fff">31%</h2><p style="margin-top:6px;color:#bfbfbf">more qualified trials from better onboarding answers</p></div>
        <p class="lead">“Prospects arrive with fewer objections because Nimbus answers them clearly before the demo.”</p>
      </div>
      <div class="tcard reveal">
        <div class="lg"><svg class="mk" viewBox="0 0 24 24"><path class="ico" d="M19.5 12v7.5a.75.75 0 0 1-.75.75H4.5a.75.75 0 0 1-.75-.75V5.25c0-.4.35-.75.75-.75H12"/><circle cx="18.4" cy="5.6" r="2.6" class="ico"/></svg><span class="tag plain">Strategy</span></div>
        <p class="lead">“What used to take hours of back-and-forth now happens in minutes.”</p>
        <div class="person"><div class="portrait" style="background:linear-gradient(135deg,#f6ad55,#c05621)"></div><div><div class="nm">Mason Carter</div><div class="rl">Director of Operations</div></div></div>
      </div>
    </div>
  </div>
</section>

<!-- PRICING -->
<section class="wrap" id="pricing" data-section="pricing">
  <div class="center reveal" style="display:flex;flex-direction:column;align-items:center;gap:16px;margin-bottom:42px">
    <span class="tag"><svg><use href="#i-tag"/></svg>Pricing</span>
    <h2 style="max-width:620px">Memberships for teams that ship every week.</h2>
    <p class="grey" style="max-width:500px">Premium design operations, clear monthly pricing, and enough flexibility to pause when the queue is empty.</p>
  </div>
  <div class="price-grid">
    <div class="pcard primary reveal" data-price="19">
      <div class="tp"><div class="picon"><svg><use href="#i-rocket"/></svg></div></div>
      <div><h4>Essential</h4><p class="grey desc" style="margin-top:6px">A lean subscription for focused landing pages, web polish, and small weekly design queues.</p></div>
      <div class="price"><span class="amt">$19</span><span class="per">/mo</span></div>
      <div class="toggle" role="switch" aria-checked="false" tabindex="0"><span class="sw"><i></i></span>Annual billing saves 15%</div>
      <div class="flist"><div><svg><use href="#i-check"/></svg>Unlimited AI chats</div><div><svg><use href="#i-check"/></svg>Context-aware responses</div><div><svg><use href="#i-check"/></svg>Instant response generation</div><div><svg><use href="#i-check"/></svg>Multi-language support</div><div><svg><use href="#i-check"/></svg>Custom training &amp; knowledge</div><div><svg><use href="#i-check"/></svg>Advanced AI models</div></div>
      <a href="#" class="btn btn-dark">Book a call</a>
    </div>
    <div class="pcard reveal" data-price="49">
      <div class="tp"><div class="picon"><svg><use href="#i-crown"/></svg></div><span class="tag plain">Most chosen</span></div>
      <div><h4>Studio</h4><p class="grey desc" style="margin-top:6px">A high-output design membership for teams that need weekly delivery and sharper direction.</p></div>
      <div class="price"><span class="amt">$49</span><span class="per">/mo</span></div>
      <div class="toggle" role="switch" aria-checked="false" tabindex="0"><span class="sw"><i></i></span>Annual billing saves 15%</div>
      <div class="flist"><div><svg><use href="#i-check"/></svg>Advanced AI reasoning</div><div><svg><use href="#i-check"/></svg>Role-based team access</div><div><svg><use href="#i-check"/></svg>Personalized AI tuning</div><div><svg><use href="#i-check"/></svg>Enhanced data security</div><div><svg><use href="#i-check"/></svg>Extended context memory</div><div><svg><use href="#i-check"/></svg>Premium support access</div></div>
      <a href="#" class="btn btn-dark">Book the studio plan</a>
    </div>
    <div class="pcard dark reveal" data-price="129">
      <div class="tp"><div class="picon"><svg><use href="#i-bolt"/></svg></div><span class="tag soft"><svg><use href="#i-spark"/></svg>Premium</span></div>
      <div><h4>Scale</h4><p class="desc" style="margin-top:6px">For growing teams that need more parallel requests, executive polish, and launch support.</p></div>
      <div class="price"><span class="amt">$129</span><span class="per">/mo</span></div>
      <div class="toggle" role="switch" aria-checked="false" tabindex="0"><span class="sw"><i></i></span>Annual billing saves 15%</div>
      <div class="flist"><div><svg><use href="#i-check"/></svg>Enterprise AI throughput</div><div><svg><use href="#i-check"/></svg>Four active requests</div><div><svg><use href="#i-check"/></svg>Advanced usage analytics</div><div><svg><use href="#i-check"/></svg>Custom workflows</div><div><svg><use href="#i-check"/></svg>Smart context handling</div><div><svg><use href="#i-check"/></svg>Enhanced security controls</div></div>
      <a href="#" class="btn">Talk to sales</a>
    </div>
  </div>
  <div class="perks reveal">
    <div><svg><use href="#i-sliders"/></svg>Unlimited requests</div><hr>
    <div><svg><use href="#i-pause"/></svg>Pause or cancel anytime</div><hr>
    <div><svg><use href="#i-clock"/></svg>Fast turnaround</div>
  </div>
</section>

<!-- BLOG -->
<section class="wrap" id="blog" data-section="blog">
  <div class="sec-head reveal">
    <div class="t">
      <span class="tag"><svg><use href="#i-book"/></svg>Blog</span>
      <h2>Discover insights, ideas, and innovation.</h2>
      <p>Insights and expertise in AI automation, intelligent conversations, and business productivity.</p>
    </div>
    <a href="#" class="btn btn-dark">View all</a>
  </div>
  <a href="#" class="post big reveal">
    <div class="imgbox"><div class="art art-blob"></div></div>
    <div class="ct">
      <div class="top"><span class="tag plain">Productivity boost</span><h3>How modern AI tools are transforming the way we work every day</h3><p class="grey">Discover how AI-powered tools are helping automate tasks and boost productivity.</p></div>
      <div class="bot">
        <div class="writer"><div class="portrait" style="background:linear-gradient(135deg,#90cdf4,#3182ce)"></div><div><div class="lead">Ethan Brooks</div><div class="grey" style="margin-top:6px">Machine Learning Engineer</div></div></div>
        <div class="rt"><i></i>4 min read</div>
      </div>
    </div>
  </a>
  <div class="small-posts">
    <a href="#" class="post sm reveal">
      <div class="imgbox"><div class="art art-robot">
        <svg viewBox="0 0 300 400" preserveAspectRatio="xMidYMid slice" style="position:absolute;inset:0;width:100%;height:100%">
          <defs><radialGradient id="rh" cx=".35" cy=".3"><stop offset="0" stop-color="#4a4a4f"/><stop offset="1" stop-color="#0c0c0e"/></radialGradient><filter id="fog"><feGaussianBlur stdDeviation="18"/></filter></defs>
          <ellipse cx="150" cy="370" rx="110" ry="60" fill="#111" />
          <rect x="128" y="270" width="44" height="70" rx="10" fill="#1a1a1d"/>
          <rect x="70" y="110" width="160" height="170" rx="70" fill="url(#rh)"/>
          <rect x="92" y="165" width="116" height="48" rx="24" fill="#050507"/>
          <circle cx="122" cy="189" r="9" fill="#ff462e"><animate attributeName="opacity" values="1;.3;1" dur="3s" repeatCount="indefinite"/></circle>
          <circle cx="178" cy="189" r="9" fill="#ff462e"><animate attributeName="opacity" values="1;.3;1" dur="3s" repeatCount="indefinite"/></circle>
          <ellipse cx="110" cy="140" rx="30" ry="12" fill="#fff" opacity=".18"/>
          <rect x="146" y="80" width="8" height="32" fill="#1a1a1d"/><circle cx="150" cy="76" r="8" fill="#1a1a1d"/>
          <g filter="url(#fog)" opacity=".75"><ellipse cx="60" cy="330" rx="120" ry="40" fill="#fff"/><ellipse cx="260" cy="300" rx="110" ry="36" fill="#fff"/></g>
        </svg>
      </div></div>
      <div class="ct"><div class="top"><span class="tag plain">Smarter workflows</span><h4>AI-powered customer support is the new standard</h4></div><div class="rt"><i></i>7 min read</div></div>
    </a>
    <a href="#" class="post sm reveal">
      <div class="imgbox"><div class="art art-blue">
        <svg viewBox="0 0 300 400" preserveAspectRatio="xMidYMid slice" style="position:absolute;inset:0;width:100%;height:100%">
          <defs><linearGradient id="bf" x1="0" x2="1"><stop offset="0" stop-color="#2b6cff"/><stop offset=".5" stop-color="#9cc4ff"/><stop offset="1" stop-color="#1846c9"/></linearGradient></defs>
          <g fill="url(#bf)" opacity=".9">
            <path d="M-20 120 C60 60 120 200 200 140 S320 80 340 120 L340 170 C280 130 230 230 160 200 S40 140 -20 190Z"><animate attributeName="d" dur="8s" repeatCount="indefinite" values="M-20 120 C60 60 120 200 200 140 S320 80 340 120 L340 170 C280 130 230 230 160 200 S40 140 -20 190Z;M-20 140 C70 90 110 170 200 170 S300 60 340 100 L340 160 C270 110 240 250 160 220 S50 170 -20 200Z;M-20 120 C60 60 120 200 200 140 S320 80 340 120 L340 170 C280 130 230 230 160 200 S40 140 -20 190Z"/></path>
            <path d="M-20 230 C80 180 140 300 220 250 S320 200 340 230 L340 290 C270 250 220 340 150 310 S30 260 -20 300Z" opacity=".7"><animate attributeName="d" dur="10s" repeatCount="indefinite" values="M-20 230 C80 180 140 300 220 250 S320 200 340 230 L340 290 C270 250 220 340 150 310 S30 260 -20 300Z;M-20 250 C60 200 160 280 220 280 S310 190 340 210 L340 280 C260 240 230 360 150 330 S40 280 -20 320Z;M-20 230 C80 180 140 300 220 250 S320 200 340 230 L340 290 C270 250 220 340 150 310 S30 260 -20 300Z"/></path>
          </g>
        </svg>
      </div></div>
      <div class="ct"><div class="top"><span class="tag plain">Instant insights</span><h4>Creating better experiences with AI</h4></div><div class="rt"><i></i>5 min read</div></div>
    </a>
    <a href="#" class="post sm reveal">
      <div class="imgbox"><div class="art art-jelly">
        <svg viewBox="0 0 400 300" preserveAspectRatio="xMidYMid slice" style="position:absolute;inset:0;width:100%;height:100%">
          <defs><radialGradient id="jb" cx=".5" cy=".3"><stop offset="0" stop-color="#ffd1f0"/><stop offset=".6" stop-color="#d36bff" stop-opacity=".8"/><stop offset="1" stop-color="#5b5cff" stop-opacity=".3"/></radialGradient><radialGradient id="jb2" cx=".5" cy=".3"><stop offset="0" stop-color="#fff2c4"/><stop offset=".6" stop-color="#ff8a5c" stop-opacity=".8"/><stop offset="1" stop-color="#ff462e" stop-opacity=".3"/></radialGradient></defs>
          <g><animateTransform attributeName="transform" type="translate" values="0 0;0 -14;0 0" dur="6s" repeatCount="indefinite"/>
            <path d="M120 120 Q170 30 220 120 Q170 110 120 120Z" fill="url(#jb)"/>
            <g stroke="#e9a6ff" stroke-width="2" fill="none" opacity=".7"><path d="M135 120 q-8 40 6 80"/><path d="M155 118 q8 50 -4 100"/><path d="M175 118 q-6 45 8 95"/><path d="M195 119 q10 40 -2 85"/><path d="M210 120 q-4 35 10 70"/></g>
          </g>
          <g><animateTransform attributeName="transform" type="translate" values="0 0;0 12;0 0" dur="7s" repeatCount="indefinite"/>
            <path d="M260 170 Q295 105 330 170 Q295 162 260 170Z" fill="url(#jb2)"/>
            <g stroke="#ffb38a" stroke-width="2" fill="none" opacity=".7"><path d="M272 170 q-6 30 4 60"/><path d="M290 168 q6 36 -2 70"/><path d="M308 169 q-4 30 6 64"/><path d="M322 170 q6 26 -2 50"/></g>
          </g>
          <g fill="#fff" opacity=".5"><circle cx="60" cy="60" r="1.5"/><circle cx="340" cy="40" r="1"/><circle cx="90" cy="230" r="1.2"/><circle cx="370" cy="250" r="1.5"/><circle cx="240" cy="60" r="1"/></g>
        </svg>
      </div></div>
      <div class="ct"><div class="top"><span class="tag plain">Trusted AI</span><h4>The rise of AI customer support</h4></div><div class="rt"><i></i>6 min read</div></div>
    </a>
  </div>
</section>

<!-- FAQ -->
<section class="wrap" id="questions" data-section="faq" style="padding-bottom:0">
  <div class="faq">
    <div class="faq-l reveal">
      <div class="top">
        <span class="tag"><svg><use href="#i-q"/></svg>FAQ</span>
        <h2>Got questions? we’ve got answers.</h2>
        <p class="grey" style="max-width:500px">Here are the most common questions we receive, along with clear answers.</p>
      </div>
      <div class="bottom">
        <svg width="32" height="32"><use href="#i-chat"/></svg>
        <p class="grey" style="max-width:500px">Can’t find what you’re looking for? We’re here to help with anything you need.</p>
        <a href="#" class="btn btn-dark">Contact support</a>
      </div>
    </div>
    <div class="faq-r" id="faq">
      <div class="qa reveal"><div class="q">How does the AI app work?<span class="pm"></span></div><div class="a"><p>The app analyzes your inputs, understands your intent, and generates accurate responses or actions using its built-in AI models. It adapts over time based on how you use it.</p></div></div>
      <div class="qa reveal"><div class="q">Can the AI app learn my preferences?<span class="pm"></span></div><div class="a"><p>Yes. The AI can remember your preferences, tone, and workflow (if memory features are enabled), helping it provide more personalized and relevant responses over time.</p></div></div>
      <div class="qa reveal"><div class="q">What kind of tasks does the AI app handle?<span class="pm"></span></div><div class="a"><p>It specializes in writing, content creation, automation, data assistance, idea generation, and everyday productivity tasks. You can ask it to draft, explain, summarize, or create almost anything.</p></div></div>
      <div class="qa reveal"><div class="q">Is my data secure when using the AI app?<span class="pm"></span></div><div class="a"><p>Yes. User data is protected with industry-standard security measures, and privacy controls help ensure your information remains safe and confidential.</p></div></div>
      <div class="qa reveal"><div class="q">Does the AI app offer ongoing support?<span class="pm"></span></div><div class="a"><p>Yes. The app automatically updates with new features, improved models, and performance enhancements as they become available.</p></div></div>
      <div class="qa reveal"><div class="q">How long does the app take to respond?<span class="pm"></span></div><div class="a"><p>Most responses are generated within seconds. More complex tasks may take slightly longer, but the app is optimized for fast output.</p></div></div>
      <div class="qa reveal"><div class="q">Can the AI app integrate with other tools?<span class="pm"></span></div><div class="a"><p>Depending on the version, the app can connect with external platforms, export outputs, and support API-based integrations for a smoother workflow.</p></div></div>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta" data-section="cta">
  <div class="cta-card reveal">
    <div class="sky" aria-hidden="true"><canvas class="bg-canvas"></canvas></div>
    <div class="badge-logo"><div><svg viewBox="0 0 32 32"><path d="M16 4c.8 5.9 3.6 8.7 9.5 9.5-5.9.8-8.7 3.6-9.5 9.5-.8-5.9-3.6-8.7-9.5-9.5C12.4 12.7 15.2 9.9 16 4Z" fill="#ff462e"/><circle cx="25" cy="24" r="2.5" fill="#0c0c0c"/></svg></div></div>
    <h2>Transform with AI.</h2>
    <p style="max-width:500px">Install the app and experience seamless, AI-driven productivity from day one.</p>
    <div class="cta-row"><a href="#pricing" class="btn btn-dark"><svg><use href="#i-bolt"/></svg>Start a 14-day trial</a><a href="#pricing" class="btn btn-light">Check pricing</a></div>
  </div>
</section>

</main>

<!-- FOOTER -->
<footer class="foot-wrap" data-section="footer">
  <div class="foot">
    <div class="foot-top reveal">
      <div>
        <a href="#hero" class="logo"><svg class="logo-mark" viewBox="0 0 32 32"><circle cx="16" cy="16" r="16" fill="#fff"/><circle cx="16" cy="16" r="10.5" fill="none" stroke="#ff462e" stroke-opacity=".22"/><path d="M16 8.5c.55 4 2.5 5.95 6.5 6.5-4 .55-5.95 2.5-6.5 6.5-.55-4-2.5-5.95-6.5-6.5 4-.55 5.95-2.5 6.5-6.5Z" fill="#ff462e"/></svg>Nimbus</a>
        <h2 class="tagline">Clarity, <em>on demand.</em></h2>
        <p class="addr">Los Angeles, CA 90011</p>
      </div>
      <div class="news">
        <span class="eyebrow">Newsletter</span>
        <p>Product notes and new integrations, once a month. No noise.</p>
        <form id="news" class="news-form"><input type="email" required placeholder="you@company.example" aria-label="Email"><button type="submit" class="nav-cta"><span class="lbl">Subscribe</span><span class="arr"><svg viewBox="0 0 24 24"><path class="ico" d="M5 12h14M13 6l6 6-6 6"/></svg></span></button></form>
      </div>
    </div>
    <div class="foot-cols reveal">
      <div><h6>Product</h6><a class="fl" href="#process">Process</a><a class="fl" href="#features">Integrations</a><a class="fl" href="#testimonials">Customers</a><a class="fl" href="#pricing">Pricing</a></div>
      <div><h6>Company</h6><a class="fl" href="#blog">Journal</a><a class="fl" href="#">Careers</a><a class="fl" href="#">Press</a><a class="fl" href="#">Contact</a></div>
      <div><h6>Legal</h6><a class="fl" href="#">Privacy policy</a><a class="fl" href="#">Terms &amp; conditions</a><a class="fl" href="#">Security</a><a class="fl" href="#">Cookies</a></div>
      <div class="connect"><h6>Connect</h6>
        <div class="socials"><a href="#" aria-label="X"><svg><use href="#i-x"/></svg></a><a href="#" aria-label="Instagram"><svg><use href="#i-ig"/></svg></a><a href="#" aria-label="LinkedIn"><svg><use href="#i-in"/></svg></a></div>
        <span class="sys-status">All systems normal</span>
      </div>
    </div>
    <div class="foot-bar">
      <span>© 2026 Nimbus, Inc. · Design by <a href="#">Amar KZR</a></span>
      <a href="#hero" class="top-btn">Back to top<i><svg viewBox="0 0 24 24"><path class="ico" d="M12 19V5M6 11l6-6 6 6"/></svg></i></a>
    </div>
    <div class="wordmark" aria-hidden="true">Nimbus</div>
  </div>
</footer>

<script>
// nav
const nav=document.getElementById('nav'),menuBtn=document.getElementById('menuBtn');
const onScroll=()=>nav.classList.toggle('scrolled',scrollY>60);
addEventListener('scroll',onScroll,{passive:true});onScroll();
function setMenu(open){
  nav.classList.toggle('open',open);document.body.classList.toggle('menu-open',open);
  menuBtn.setAttribute('aria-expanded',open);menuBtn.setAttribute('aria-label',open?'Close menu':'Open menu');
}
menuBtn.onclick=()=>setMenu(!nav.classList.contains('open'));
document.getElementById('navScrim').onclick=()=>setMenu(false);
document.querySelectorAll('.mi,.mi-link').forEach(a=>a.addEventListener('click',()=>setMenu(false)));
addEventListener('keydown',e=>{if(e.key==='Escape')setMenu(false)});
matchMedia('(min-width:1200px)').addEventListener('change',e=>{if(e.matches)setMenu(false)});

// sliding highlight + active section
const links=[...document.querySelectorAll('#navLinks a')],hl=document.getElementById('navHl');
let activeLink=null;
function moveHl(a){if(!a){hl.style.opacity=0;return}hl.style.opacity=1;hl.style.width=a.offsetWidth+'px';hl.style.transform=`translateX(${a.offsetLeft}px)`}
links.forEach(a=>a.addEventListener('mouseenter',()=>moveHl(a)));
document.getElementById('navLinks').addEventListener('mouseleave',()=>moveHl(activeLink));
const secObs=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){
  activeLink=links.find(l=>l.getAttribute('href')==='#'+e.target.id)||null;
  links.forEach(l=>l.classList.toggle('active',l===activeLink));moveHl(activeLink)}}),{rootMargin:'-45% 0px -50% 0px'});
['hero','process','features','testimonials','pricing','blog'].forEach(id=>{const s=document.getElementById(id);s&&secObs.observe(s)});

// process slider
const slides=[...document.querySelectorAll('.slide')],dots=[...document.querySelectorAll('#dots i')];
let cur=0,timer;
const calm=matchMedia('(prefers-reduced-motion: reduce)').matches;
function go(n){cur=(n+slides.length)%slides.length;slides.forEach((s,i)=>{s.classList.toggle('on',i===cur);s.setAttribute('aria-hidden',String(i!==cur))});dots.forEach((d,i)=>d.classList.toggle('on',i===cur));clearInterval(timer);if(!calm)timer=setInterval(()=>go(cur+1),5000)}
document.getElementById('next').onclick=()=>go(cur+1);
document.getElementById('prev').onclick=()=>go(cur-1);
dots.forEach((d,i)=>{d.style.cursor='pointer';d.onclick=()=>go(i)});
go(0);

// ticker duplicate
const tk=document.getElementById('ticker');tk.innerHTML+=tk.innerHTML;

// orbit icons (generic tool icons drawn in SVG)
const icons=[
 ['#ff462e','<path class="ico" d="M3 6.75h18v10.5H3ZM3 6.75l9 6 9-6"/>'],
 ['#3b82f6','<rect x="3.75" y="5.25" width="16.5" height="15" rx="1.5" class="ico"/><path class="ico" d="M3.75 9.75h16.5M8.25 3v4.5M15.75 3v4.5"/>'],
 ['#10b981','<path class="ico" d="M12.4 20.25H4.5v-8.6A8.6 8.6 0 1 1 12.4 20.25Z"/>'],
 ['#f59e0b','<path class="ico" d="M6 3h8.25L18.75 7.5V21H6ZM9 12h6M9 15.75h6"/>'],
 ['#8b5cf6','<path class="ico" d="M4.5 19.5V10.5M10 19.5V4.5M15.5 19.5v-6M21 19.5V8.25"/>'],
 ['#0c0c0c','<path class="ico" d="M8.25 7.5 3.75 12l4.5 4.5M15.75 7.5l4.5 4.5-4.5 4.5M13.5 5.25l-3 13.5"/>'],
 ['#ec4899','<path class="ico" d="M3 7.5h4.5l1.5-2.25h6L16.5 7.5H21v12H3Z"/><circle cx="12" cy="13.1" r="3.4" class="ico"/>'],
 ['#06b6d4','<path class="ico" d="M6.75 18.75a4.5 4.5 0 0 1-.4-9A6 6 0 0 1 18 8.25a4.5 4.5 0 0 1 .75 10.5Z"/>'],
 ['#ef4444','<path class="ico" d="M9 18V5.25l12-2.25V15.75"/><circle cx="6.75" cy="18" r="2.25" class="ico"/><circle cx="18.75" cy="15.75" r="2.25" class="ico"/>'],
 ['#22c55e','<path class="ico" d="M3 3.75h2.25l2.25 11.25h11.25L21 7.5H6.4"/><circle cx="9" cy="19.1" r="1.1" fill="currentColor"/><circle cx="17.25" cy="19.1" r="1.1" fill="currentColor"/>'],
 ['#6366f1','<path class="ico" d="M9 4.5 3.75 6.75v12.75L9 17.25l6 2.25 5.25-2.25V4.5L15 6.75Z M9 4.5v12.75M15 6.75V19.5"/>'],
 ['#f97316','<path class="ico" d="M3.75 6.75h7.5l1.5 2.25h7.5V18.75H3.75Z"/>']
];
const names=['Mail','Calendar','Chat','Docs','Analytics','Code','Media','Cloud','Music','Commerce','Maps','Files'];
const vis=document.getElementById('intVisual');
const rings=[
  {d:40,n:3,s:13,dur:'46s',dir:'normal',off:20},
  {d:68,n:5,s:11.5,dur:'70s',dir:'reverse',off:0,dashed:true},
  {d:96,n:7,s:10,dur:'100s',dir:'normal',off:12}
];
let k=0;
rings.forEach(r=>{
  const ring=document.createElement('div');ring.className='ring'+(r.dashed?' dashed':'');
  ring.style.cssText=`width:${r.d}%;height:${r.d}%`;
  const track=document.createElement('div');track.className='track';
  track.style.cssText=`--dur:${r.dur};--dir:${r.dir}`;
  track.innerHTML='<span class="comet"></span>';
  for(let i=0;i<r.n;i++){
    const a=r.off+i*360/r.n,[c,p]=icons[k%icons.length],nm=names[k%names.length];k++;
    const arm=document.createElement('div');arm.className='arm';arm.style.transform=`rotate(${a}deg)`;
    arm.innerHTML=`<div class="node" style="--a:${a}deg;--s:${r.s*100/r.d}%;--c:${c}" title="${nm}"><div class="tile" style="--dur:${r.dur};--rdir:${r.dir==='normal'?'reverse':'normal'}"><svg viewBox="0 0 24 24">${p}</svg></div></div>`;
    track.appendChild(arm);
  }
  ring.appendChild(track);vis.insertBefore(ring,vis.firstChild);
});

// pricing toggles (sync all cards)
const cards=[...document.querySelectorAll('.pcard')];let annual=false;
function setBilling(on){annual=on;cards.forEach(c=>{c.classList.toggle('annual',on);const t=c.querySelector('.toggle');t.setAttribute('aria-checked',on);const base=+c.dataset.price;c.querySelector('.amt').textContent='$'+(on?Math.round(base*.85):base)})}
cards.forEach(c=>{const t=c.querySelector('.toggle');t.onclick=()=>setBilling(!annual);t.onkeydown=e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();setBilling(!annual)}}});

// faq
const qas=[...document.querySelectorAll('.qa')];
function toggleQa(q){const o=q.classList.contains('open');qas.forEach(x=>{x.classList.remove('open');x.querySelector('.q').setAttribute('aria-expanded','false')});if(!o){q.classList.add('open');q.querySelector('.q').setAttribute('aria-expanded','true')}}
qas.forEach(q=>{const h=q.querySelector('.q');h.setAttribute('role','button');h.tabIndex=0;h.setAttribute('aria-expanded','false');
  q.onclick=()=>toggleQa(q);h.onkeydown=e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();toggleQa(q)}}});
// reduced motion also stills the SMIL art in the journal cards
if(calm)document.querySelectorAll('svg').forEach(v=>v.pauseAnimations&&v.pauseAnimations());

// newsletter
document.getElementById('news').onsubmit=e=>{e.preventDefault();const l=e.target.querySelector('.lbl');l.textContent="You're in";e.target.reset();setTimeout(()=>l.textContent='Subscribe',2500)};

// ===== Parallax cloud sky (canvas, procedural — no image assets) =====
(function(){
  const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
  const rnd=(a,b)=>Math.random()*(b-a)+a;

  // soft puff texture drawn in code (replaces the PNG cloud sprite)
  const puff=document.createElement('canvas');puff.width=puff.height=70;
  (()=>{const c=puff.getContext('2d'),g=c.createRadialGradient(35,35,0,35,35,35);
    g.addColorStop(0,'rgba(255,255,255,1)');g.addColorStop(.45,'rgba(255,255,255,.55)');g.addColorStop(1,'rgba(255,255,255,0)');
    c.fillStyle=g;c.fillRect(0,0,70,70);})();

  // build one cloud by stamping many rotated, scaled puffs
  function makeCloud(){
    const cv=document.createElement('canvas'),ctx=cv.getContext('2d');
    const W=cv.width=Math.round(rnd(400,700)),H=cv.height=Math.round(rnd(200,260));
    const w=puff.width,h=puff.height,hw=w/2,hh=h/2,max=2.5;
    let n=Math.ceil(rnd(20,90));
    while(n--){
      const s=rnd(.4,max);
      ctx.globalAlpha=Math.max(0,Math.random()-.2);
      ctx.translate(rnd(hw,W-w*max*1.3),rnd(hh+hh/4,H-h*max));
      ctx.scale(s,rnd(s-.3,s));ctx.translate(hw,hh);ctx.rotate(rnd(0,Math.PI/2));
      ctx.drawImage(puff,-hw,-hh);ctx.setTransform(1,0,0,1,0,0);
    }
    return cv;
  }

  // best-candidate sampling for even cloud spread
  function sampler(w,h,k){const pts=[];const d=(a,b)=>(a[0]-b[0])**2+(a[1]-b[1])**2;
    return()=>{let best=[Math.random()*w,Math.random()*h];
      if(pts.length){let bd=0;for(let i=0;i<k;i++){const c=[Math.random()*w,Math.random()*h];let m=Infinity;for(const p of pts)m=Math.min(m,d(p,c));if(m>bd){bd=m;best=c}}}
      pts.push(best);return best}}

  function Sky(canvas){
    const host=canvas.parentElement,ctx=canvas.getContext('2d');
    let W,H,dpr,els=[],ty=0,y=0,visible=true,raf;
    const DAMP=40;
    function build(){
      dpr=Math.min(devicePixelRatio||1,2);
      W=host.clientWidth;H=host.clientHeight;
      canvas.width=W*dpr;canvas.height=H*dpr;
      els=[];
      const n=Math.max(60,Math.round(W*H/5000));
      for(let i=0;i<n;i++){const d=rnd(.1,.3);els.push({t:'s',x:Math.random()*W,y:Math.random()*H*.9,r:rnd(1,2.6),d,z:d*13,a:rnd(.35,.9)})}
      const get=sampler(W,H,10),count=Math.max(8,Math.floor(W*H/(510*260)));
      for(let i=0;i<count;i++){const r=rnd(.4,1.2),p=get(),img=makeCloud();
        els.push({t:'c',img,x:p[0],y:p[1],w:img.width,h:img.height,d:r,z:r*13,a:r<.8?.8:Math.min(r,1),sp:r*rnd(.2,.4)})}
      els.sort((a,b)=>a.z-b.z);
    }
    function target(){const r=host.getBoundingClientRect();return Math.max(-H,Math.min(H*2,-r.top))}
    function draw(){
      y+=(-target()-y)/DAMP;
      ctx.setTransform(dpr,0,0,dpr,0,0);ctx.clearRect(0,0,W,H);
      const g=ctx.createLinearGradient(0,0,0,H);g.addColorStop(0,'#07588A');g.addColorStop(1,'#E1F6F4');
      ctx.fillStyle=g;ctx.fillRect(0,0,W,H);
      for(const e of els){
        ctx.save();ctx.globalAlpha=e.a;
        const cx=e.t==='c'?e.x+e.w/2:e.x,cy=e.t==='c'?e.y+e.h/2:e.y;
        ctx.translate(cx,cy);ctx.scale(e.d,e.d);ctx.translate(0,y);ctx.translate(-cx,-cy);
        if(e.t==='s'){ctx.beginPath();ctx.arc(e.x,e.y,e.r/e.d*.35,0,Math.PI*2);ctx.fillStyle='#fff';ctx.fill()}
        else{ctx.drawImage(e.img,e.x,e.y,e.w,e.h);
          if(!reduce){e.x=(e.x*e.d)>-e.w?e.x-e.sp:W+e.w*2}}
        ctx.restore();
      }
    }
    function loop(){draw();raf=visible&&!reduce?requestAnimationFrame(loop):0}
    new IntersectionObserver(([en])=>{visible=en.isIntersecting;if(visible&&!raf)loop()}).observe(host);
    let rt;addEventListener('resize',()=>{clearTimeout(rt);rt=setTimeout(()=>{build();y=-target();draw()},150)});
    build();y=-target();loop();
  }
  document.querySelectorAll('.sky canvas').forEach(Sky);
})();

// reveal on scroll
const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}}),{threshold:.12});
document.querySelectorAll('.reveal').forEach((el,i)=>{el.style.transitionDelay=(i%3)*80+'ms';io.observe(el)});
</script>
</body>
</html>
```
