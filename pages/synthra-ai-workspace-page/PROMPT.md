INSTALANDING.AI · Synthra AI Workspace Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Synthra AI Workspace Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/synthra-ai-workspace-page

synthra-ai-workspace.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Synthra AI Workspace Page
  slug     synthra-ai-workspace-page
  prompt   https://instalanding.ai/p/synthra-ai-workspace-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/synthra-ai-workspace-page
  license  Fictional brand ("Synthra"); every customer, logo, metric, price and quote is invented.
           Replace names and copy before shipping. Every picture is CSS, SVG or generated markup; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --lime / --lime-2 / --lime-soft, --olive, --bg (pale lime
            paper), --ink, --night, greys and an SVG --grain; Plus Jakarta Sans and JetBrains Mono
  sections  nav, hero, partners, features, customer-stories, pricing, agents, testimonials, faq, cta, footer
            (each carries data-section)
  scripts   one plain script, no libraries: builds the hero ticker of eight CSS art tiles with glass product hints,
            a 12-tile 3D carousel of product tiles, a looping phone chat, the logo marquee, six sticky customer
            story cards, six agent orbs that flip to details, the testimonial track, the FAQ accordion and a
            scroll reveal
  assets    no image files; a small <symbol> sprite of icons at the top of <body>

  ADAPTING
  - Content lives in arrays in the script: tiles, artTiles + overlays, convo, brands, cases, agents, t (quotes), faq.
  - .surface gives any card the dark grain, .mesh a gradient backdrop, .glass the frosted panel, .shine a sweep.
  - prefers-reduced-motion: every animation and transition is off and revealed content shows at once.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Synthra — The AI Workspace That Works For You</title>
<meta name="description" content="Synthra is an AI workspace with specialist agents that research, write, analyze and automate — so your team ships more with less.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --lime:#d2e823; --lime-2:#e8f56a; --lime-soft:#f3fbc9; --lime-40:#d2e82366; --olive:#a5b00f; --olive-dk:#363508;
  --bg:#fbfde9; --ink:#0a0a0a; --night:#07080a; --white:#fff; --g700:#404040; --g500:#737373; --g300:#d4d4d4;
  --font:"Plus Jakarta Sans",Inter,system-ui,-apple-system,sans-serif;
  --mono:"JetBrains Mono",ui-monospace,Menlo,monospace;
  --grain:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.9' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 .55 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{font-family:var(--font);background:var(--bg);color:var(--ink);-webkit-font-smoothing:antialiased;overflow-x:hidden}
a{color:inherit;text-decoration:none}
button{font:inherit;border:0;background:none;cursor:pointer;color:inherit}
.wrap{max-width:1260px;margin:0 auto;padding:0 30px}
h1{font-size:56px;line-height:1.12;font-weight:600;letter-spacing:-.02em}
h2{font-size:48px;line-height:1.15;font-weight:600;letter-spacing:-.02em}
.lead{font-size:18px;line-height:1.55;color:var(--g700)}
section{position:relative}
.grad-text{background:linear-gradient(100deg,#0a0a0a 20%,#6d7a06 60%,#0a0a0a 90%);-webkit-background-clip:text;background-clip:text;color:transparent}

/* premium surface primitives */
.surface{position:relative;overflow:hidden;isolation:isolate;background:var(--night);color:#fff}
.surface::after{content:"";position:absolute;inset:0;background-image:var(--grain);opacity:.09;mix-blend-mode:overlay;pointer-events:none;z-index:5}
.mesh{position:absolute;inset:-20%;z-index:0;filter:saturate(1.1)}
.glass{background:linear-gradient(160deg,rgba(255,255,255,.14),rgba(255,255,255,.04));border:1px solid rgba(255,255,255,.14);
  backdrop-filter:blur(14px) saturate(1.3);-webkit-backdrop-filter:blur(14px) saturate(1.3);border-radius:14px;box-shadow:inset 0 1px 0 rgba(255,255,255,.18),0 10px 30px -10px rgba(0,0,0,.5)}
.orb{position:absolute;border-radius:50%;filter:blur(40px);opacity:.85;animation:drift 12s ease-in-out infinite}
@keyframes drift{33%{transform:translate(30px,-20px) scale(1.1)}66%{transform:translate(-20px,25px) scale(.95)}}
.shine{position:absolute;inset:0;z-index:4;pointer-events:none;background:linear-gradient(115deg,transparent 35%,rgba(255,255,255,.12) 48%,transparent 60%);background-size:250% 100%;animation:shine 6s ease-in-out infinite}
@keyframes shine{from{background-position:130% 0}to{background-position:-130% 0}}

/* glow */
.glow{position:absolute;left:50%;top:-590px;width:1164px;aspect-ratio:1;transform:translateX(-50%);border-radius:50%;
  background:radial-gradient(50% 50%,#e5ef91 0%,#fbfde9 100%);filter:blur(100px);z-index:0;pointer-events:none}

/* tag */
.tag{display:inline-flex;align-items:center;gap:8px;padding:10px 14px;border-radius:999px;font-size:14px;color:var(--olive);border:1px solid var(--lime);backdrop-filter:blur(4px)}
.tag::before{content:"";width:8px;height:8px;border-radius:50%;background:var(--olive)}
.tag.fill{background:var(--lime-40);border-color:transparent;color:var(--ink)}
.tag.fill::before{background:var(--ink);box-shadow:0 0 0 3px #0a0a0a22;animation:blink 1.6s infinite}
@keyframes blink{50%{opacity:.3}}
.head{display:flex;flex-direction:column;align-items:center;gap:18px;text-align:center;margin-bottom:48px}
.head h2,.head h1{max-width:820px}
.head p{max-width:600px}

/* buttons */
.btn{position:relative;overflow:hidden;display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:16px 24px;border-radius:999px;font-weight:600;font-size:16px;line-height:1.2;isolation:isolate;transition:color .35s}
.btn::before{content:"";position:absolute;inset:0;width:0;border-radius:999px;background:var(--fx,var(--lime));transition:width .45s cubic-bezier(.44,0,.56,1);z-index:-1}
.btn:hover::before{width:104%}
.btn.lime{background:var(--lime);color:#000;--fx:#fff}
.btn.dark{background:var(--ink);color:#fff}
.btn.dark:hover{color:#000}
.btn.light{background:#fff;color:#000;border:1px solid var(--lime)}
.btn.block{width:100%}

/* nav */
.nav{position:absolute;top:30px;left:0;right:0;z-index:10;display:flex;justify-content:center;padding:0 24px}
.nav-bar{width:100%;max-width:912px;background:#000;border-radius:50px;padding:12px;display:flex;align-items:center;justify-content:space-between;position:relative}
.logo{display:flex;align-items:center;gap:10px;color:#fff;font-weight:600;font-size:22px;padding-left:4px;letter-spacing:-.02em}
.mark{width:40px;height:40px;border-radius:12px;position:relative;overflow:hidden;background:conic-gradient(from 200deg,#d2e823,#7ee7c4,#8b7bff,#d2e823);display:grid;place-items:center}
.mark::after{content:"";position:absolute;inset:3px;border-radius:9px;background:#0a0a0a}
.mark svg{position:relative;z-index:1}
.nav-links{display:flex;gap:30px}
.nav-links a{color:#fff;font-weight:500;font-size:16px;transition:color .2s}
.nav-links a:hover{color:var(--lime)}
.burger{display:none;color:#fff;padding:6px}

/* hero */
.hero{padding:180px 0 80px;overflow:hidden}
.hero .head{position:relative;z-index:3;margin-bottom:56px}
.btn-row{display:flex;gap:18px;flex-wrap:wrap;justify-content:center}
.reel-stage{position:relative;height:600px;display:flex;align-items:center;z-index:2}
.ticker{display:flex;gap:16px;width:max-content;animation:scroll 50s linear infinite}
.ticker:hover{animation-play-state:paused}
@keyframes scroll{to{transform:translateX(-50%)}}

/* product tiles */
.tile{width:296px;height:360px;border-radius:20px;flex:none;box-shadow:0 30px 60px -30px rgba(20,25,0,.45)}
.tile .content{position:absolute;inset:0;z-index:3;padding:18px;display:flex;flex-direction:column}
.tile .label{display:flex;align-items:center;gap:8px;font-size:12px;font-weight:600;letter-spacing:.02em;color:#fffc}
.tile .label i{width:8px;height:8px;border-radius:50%;background:var(--lime);box-shadow:0 0 10px var(--lime)}
.tile .foot{margin-top:auto}
.mono{font-family:var(--mono)}
.bubble{padding:10px 12px;font-size:12.5px;line-height:1.45;border-radius:14px;max-width:85%}
.bubble.me{align-self:flex-end;background:#fff;color:#0a0a0a;border-bottom-right-radius:4px}
.bubble.ai{border-bottom-left-radius:4px}
.skel{height:8px;border-radius:6px;background:linear-gradient(90deg,rgba(255,255,255,.18),rgba(255,255,255,.45),rgba(255,255,255,.18));background-size:200% 100%;animation:sk 1.6s linear infinite;margin-top:7px}
@keyframes sk{to{background-position:-200% 0}}
.wave{display:flex;align-items:center;gap:4px;height:120px;justify-content:center}
.wave span{width:6px;border-radius:6px;background:linear-gradient(#e8f56a,#7ee7c4);animation:wv 1.2s ease-in-out infinite}
@keyframes wv{50%{transform:scaleY(.25)}}
.progress{height:4px;border-radius:4px;background:rgba(255,255,255,.18);overflow:hidden;margin-top:8px}
.progress span{display:block;height:100%;background:linear-gradient(90deg,#d2e823,#7ee7c4);animation:pg 5s ease-in-out infinite}
@keyframes pg{from{width:5%}to{width:100%}}

/* phone */
.phone{position:absolute;left:50%;top:50%;transform:translate(-50%,-50%);width:302px;height:614px;z-index:6;border-radius:52px;padding:10px;
  background:linear-gradient(145deg,#3a3a3a,#0d0d0d 40%,#262626);box-shadow:0 0 0 1.5px #555 inset,0 50px 80px -30px rgba(0,0,0,.6),0 0 0 6px #0a0a0a10}
.phone .screen{position:relative;width:100%;height:100%;border-radius:43px;overflow:hidden}
.phone .island{position:absolute;top:11px;left:50%;transform:translateX(-50%);width:96px;height:28px;background:#000;border-radius:20px;z-index:8}
.phone .appbar{position:absolute;top:52px;left:16px;right:16px;z-index:6;display:flex;align-items:center;justify-content:space-between}
.phone .appbar b{font-size:15px;font-weight:600;display:flex;align-items:center;gap:8px}
.phone .chat{position:absolute;inset:100px 14px 86px;z-index:6;display:flex;flex-direction:column;gap:10px;justify-content:flex-end;overflow:hidden}
.phone .composer{position:absolute;left:14px;right:14px;bottom:22px;z-index:6;display:flex;align-items:center;gap:8px;padding:8px 8px 8px 14px;border-radius:999px;font-size:12.5px;color:#fffa}
.phone .composer span{flex:1}
.send{width:34px;height:34px;border-radius:50%;background:var(--lime);display:grid;place-items:center}
.msg{opacity:0;transform:translateY(10px);transition:all .45s}
.msg.show{opacity:1;transform:none}
.typing{display:inline-flex;gap:4px}
.typing i{width:6px;height:6px;border-radius:50%;background:#fff;animation:tp 1s infinite}
.typing i:nth-child(2){animation-delay:.15s}.typing i:nth-child(3){animation-delay:.3s}
@keyframes tp{50%{opacity:.25;transform:translateY(-3px)}}
.cursor::after{content:"▍";animation:blink 1s infinite;color:var(--lime)}

/* partners */
.partners{padding:0 30px 120px;text-align:center}
.partners p{font-size:18px;font-weight:500;margin-bottom:20px}
.marquee{overflow:hidden;-webkit-mask-image:linear-gradient(90deg,transparent,#000 30%,#000 70%,transparent);mask-image:linear-gradient(90deg,transparent,#000 30%,#000 70%,transparent);max-width:1200px;margin:0 auto}
.marquee .track{display:flex;gap:48px;width:max-content;animation:scroll 30s linear infinite}
.brand{display:flex;align-items:center;gap:8px;height:32px;font-weight:700;font-size:20px;color:#2a2a2a;letter-spacing:-.02em;white-space:nowrap}
.brand svg{height:26px;width:26px}

/* features */
.features{padding-bottom:80px}
.grid3{display:grid;grid-template-columns:repeat(3,1fr);gap:20px}
.feat-card{border-radius:24px;padding:24px;display:flex;flex-direction:column;gap:28px;border:1px solid #d2e82366;transition:transform .4s}
.feat-card:hover{transform:translateY(-6px)}
.feat-card .vis{height:230px;border-radius:16px;position:relative;overflow:hidden;z-index:2}
.feat-card .txt{position:relative;z-index:6;display:flex;flex-direction:column;gap:8px}
.feat-card h3{font-size:20px;font-weight:500}
.feat-card p{font-size:16px;line-height:1.5;color:#d6d6d6}
.arrow-btn{position:relative;z-index:6;width:44px;height:44px;border-radius:50%;background:#fff;display:grid;place-items:center;box-shadow:inset 0 0 10px rgba(0,0,0,.75);transition:transform .3s}
.feat-card:hover .arrow-btn{transform:rotate(-45deg)}

/* use cases */
.cases{padding-bottom:80px}
.stack{display:flex;flex-direction:column;gap:20px}
.case{position:sticky;height:600px;border-radius:24px;display:flex;align-items:flex-end}
.case .body{position:relative;z-index:6;padding:40px;display:flex;flex-direction:column;gap:16px;max-width:620px}
.case .pill{align-self:flex-start;background:#fff;color:var(--ink);font-size:14px;font-weight:600;padding:8px 16px;border-radius:99px}
.case h3{font-size:40px;font-weight:500;line-height:1.2}
.case p{font-size:22px;line-height:1.4;color:#d4d4d4}
.case .panel{position:absolute;right:40px;top:40px;width:44%;max-width:470px;z-index:4;padding:20px;transition:transform .8s}
.case:hover .panel{transform:translateY(-8px) rotate(-1deg)}
.case .metric{font-size:56px;font-weight:600;letter-spacing:-.03em;background:linear-gradient(90deg,#fff,#e8f56a);-webkit-background-clip:text;background-clip:text;color:transparent}
.case .mlabel{font-size:13px;color:#fffb;margin-bottom:14px}

/* pricing */
.pricing{padding:80px 0}
.price{border-radius:20px;padding:20px;display:flex;flex-direction:column;gap:32px;background:var(--lime-soft);border:1px solid var(--lime)}
.price.feat{border:0}
.price .top{display:flex;flex-direction:column;gap:8px;position:relative;z-index:6}
.price .row{display:flex;justify-content:space-between;align-items:center}
.price h3{font-size:20px;font-weight:500}
.badge{display:flex;gap:4px;align-items:center;background:#fff;color:var(--ink);padding:4px 12px;border-radius:99px;font-size:14px;font-weight:500}
.desc{font-size:16px;line-height:1.5;color:var(--g700);max-width:320px}
.price.feat .desc{color:#d4d4d4}
.amt{display:flex;align-items:flex-end;gap:2px;position:relative;z-index:6}
.amt b{font-size:32px;font-weight:600;line-height:1.2;letter-spacing:-.02em}
.amt span{font-size:14px;color:var(--g500);padding-bottom:5px}
.price.feat .amt span{color:#fffa}
.feats{display:flex;flex-direction:column;gap:12px;position:relative;z-index:6}
.feats > p{font-size:18px;font-weight:500}
.feats ul{list-style:none;display:flex;flex-direction:column;gap:8px}
.feats li{display:flex;gap:8px;font-size:16px;line-height:1.5;color:var(--g700)}
.price.feat li{color:#fff}
.feats li svg{flex:none;margin-top:2px}
.price .btn{margin-top:auto;z-index:6}

/* agents */
.agents{padding:80px 0}
.agent-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;align-items:start}
.agent-col{display:flex;flex-direction:column;gap:18px}
.agent-col.mid{padding-top:150px}
.agent{height:450px;border-radius:20px;cursor:pointer}
.agent .core{position:absolute;left:50%;top:42%;width:190px;height:190px;transform:translate(-50%,-50%);z-index:3}
.agent .core .sphere{position:absolute;inset:0;border-radius:50%;
  background:radial-gradient(circle at 32% 28%,#fff 0 4%,var(--c2) 22%,var(--c1) 55%,#050505 100%);
  box-shadow:0 0 80px -10px var(--c1),inset -20px -30px 50px rgba(0,0,0,.55),inset 10px 10px 30px rgba(255,255,255,.25)}
.agent .core .halo{position:absolute;inset:-24px;border-radius:50%;background:conic-gradient(from 0deg,transparent,var(--c2),transparent 40%,var(--c1),transparent 80%);filter:blur(14px);opacity:.75;animation:spin 8s linear infinite}
.agent .core .orbit{position:absolute;inset:-40px;border:1px solid rgba(255,255,255,.18);border-radius:50%;transform:rotateX(70deg);animation:spin 10s linear infinite}
.agent .core .orbit::before{content:"";position:absolute;top:-4px;left:50%;width:8px;height:8px;border-radius:50%;background:#fff;box-shadow:0 0 12px #fff}
@keyframes spin{to{transform:rotate(360deg)}}
.agent .core .orbit{animation:orbit 9s linear infinite}
@keyframes orbit{from{transform:rotateX(72deg) rotateZ(0)}to{transform:rotateX(72deg) rotateZ(360deg)}}
.agent .info{position:absolute;left:0;right:0;bottom:22px;z-index:6;text-align:center;display:flex;flex-direction:column;gap:6px;transition:opacity .3s}
.agent .info b{font-size:20px;font-weight:500}
.agent .info span{font-size:15px;color:#fffb}
.agent .details{position:absolute;inset:8px;z-index:7;border-radius:16px;display:flex;flex-direction:column;justify-content:flex-end;align-items:center;gap:20px;padding:24px 18px;text-align:center;opacity:0;transform:scale(.4);transition:all .45s cubic-bezier(.3,1.3,.5,1)}
.agent:hover .details,.agent.open .details{opacity:1;transform:scale(1)}
.agent:hover .info,.agent.open .info{opacity:0}
.agent .details p{font-size:15px;line-height:1.5;color:#e9e9e9}
.chips{display:flex;flex-wrap:wrap;gap:6px;justify-content:center}
.chips span{font-size:12px;padding:6px 10px;border-radius:99px;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.2)}

/* testimonials */
.testi{padding:80px 0;overflow:hidden}
.t-track{display:flex;gap:20px;width:max-content;animation:scroll 40s linear infinite}
.t-wrap{-webkit-mask-image:linear-gradient(90deg,transparent,#000 10%,#000 90%,transparent);mask-image:linear-gradient(90deg,transparent,#000 10%,#000 90%,transparent)}
.t-wrap:hover .t-track{animation-play-state:paused}
.tcard{width:386px;height:400px;border-radius:24px;border:1px solid var(--lime);background:var(--lime-soft);padding:24px;display:flex;flex-direction:column;justify-content:space-between;color:var(--olive-dk)}
.stars{display:flex;align-items:center;gap:15px;font-size:20px;font-weight:500}
.stars div{display:flex;gap:5px}
.tcard blockquote{font-size:18px;line-height:1.55;font-weight:500;margin-top:20px}
.author{display:flex;gap:10px;align-items:center}
.avatar{width:52px;height:52px;border-radius:50%;position:relative;overflow:hidden;display:grid;place-items:center;font-weight:600;color:#fff;font-size:17px;box-shadow:inset 0 0 0 2px rgba(255,255,255,.35)}
.author b{display:block;font-size:20px;font-weight:500}
.author span{font-size:15px;color:var(--g500)}

/* faq */
.faq{padding-bottom:80px}
.faq-body{display:flex;gap:19px;align-items:stretch}
.faq-cta{flex:1;max-width:388px;border-radius:20px;padding:20px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:28px;background:var(--lime);position:relative;overflow:hidden}
.faq-cta .txt{width:100%;display:flex;flex-direction:column;gap:8px;position:relative;z-index:2}
.faq-cta h3{font-size:20px;font-weight:500}
.faq-cta p{color:var(--g700);line-height:1.5}
.acc{flex:2;display:flex;flex-direction:column;gap:8px}
.acc-item{border:1px solid var(--lime);border-radius:20px;background:#fff;padding:25px 20px;cursor:pointer;transition:background .3s}
.acc-item.open{background:var(--lime)}
.acc-q{display:flex;align-items:center;gap:8px;justify-content:space-between;font-size:20px;font-weight:500;line-height:1.4}
.acc-ic{flex:none;width:36px;height:36px;border-radius:50%;display:grid;place-items:center;background:var(--lime);box-shadow:inset 0 0 6px rgba(255,255,255,.75);transition:background .3s,transform .3s}
.acc-item.open .acc-ic{background:#000;color:#fff;transform:rotate(180deg)}
.acc-a{display:grid;grid-template-rows:0fr;transition:grid-template-rows .35s ease}
.acc-item.open .acc-a{grid-template-rows:1fr}
.acc-a > div{overflow:hidden}
.acc-a p{padding-top:8px;color:var(--g700);line-height:1.5}

/* cta */
.cta{background:#000;color:#fff;padding:80px 0;overflow:hidden}
.cta .glowcta{position:absolute;left:50%;top:55%;width:900px;height:500px;transform:translate(-50%,-50%);background:radial-gradient(closest-side,#d2e82333,transparent);pointer-events:none}
.cta .head h2{color:#fff;max-width:420px}
.cta .head p{color:var(--g500);max-width:320px}
.ring3d{height:500px;perspective:1100px;display:flex;align-items:center;justify-content:center}
.carousel{position:relative;width:200px;height:290px;transform-style:preserve-3d;animation:rot 45s linear infinite}
@keyframes rot{from{transform:rotateX(-6deg) rotateY(0)}to{transform:rotateX(-6deg) rotateY(-360deg)}}
.carousel .tile{position:absolute;inset:0;width:200px;height:290px;backface-visibility:hidden;transform:rotateY(calc(var(--i)*30deg)) translateZ(420px)}
.carousel .tile .content{padding:14px}

/* footer */
.footer{padding:80px 0}
.foot{display:flex;gap:16px;min-height:400px}
.foot-l{width:35%;background:var(--lime);border-radius:24px;padding:24px;display:flex;flex-direction:column;justify-content:space-between;gap:32px}
.foot-l .logo{color:var(--ink);font-size:24px;font-weight:600}
.foot-l p{color:var(--g700);line-height:1.5;margin-top:16px}
.foot-l h4{font-size:20px;font-weight:500;margin-bottom:16px}
.soc-grid{display:grid;grid-template-columns:1fr 1fr;gap:8px}
.soc-grid a{background:#fff;border-radius:999px;height:48px;display:flex;align-items:center;justify-content:center;gap:7px;font-size:14px;font-weight:500;transition:transform .2s}
.soc-grid a:hover{transform:translateY(-2px)}
.foot-r{flex:1;background:#000;border-radius:24px;padding:24px;display:grid;grid-template-columns:1fr 1fr 1fr;gap:40px 16px;color:#fff;align-content:start}
.foot-r h5{font-size:16px;font-weight:600;margin-bottom:16px}
.foot-r ul{list-style:none;display:flex;flex-direction:column;gap:13px}
.foot-r li a{color:rgba(255,255,255,.5);transition:color .5s}
.foot-r li a:hover{color:#fff}
.contact a{display:flex;align-items:center;gap:10px;color:var(--g500);margin-bottom:12px}
.contact i{width:26px;height:26px;border-radius:50%;background:#fff;display:grid;place-items:center;flex:none}
.status{display:inline-flex;align-items:center;gap:8px;font-size:13px;color:#fffa;margin-top:8px}
.status::before{content:"";width:8px;height:8px;border-radius:50%;background:#4ade80;box-shadow:0 0 8px #4ade80}

/* reveal */
.rv{opacity:0;transform:translateY(60px);transition:opacity .9s cubic-bezier(.2,.7,.2,1),transform .9s cubic-bezier(.2,.7,.2,1)}
.rv.in{opacity:1;transform:none}
.d1{transition-delay:.1s}.d2{transition-delay:.2s}.d3{transition-delay:.3s}

@media (max-width:1199px){
  h1{font-size:48px} h2{font-size:40px}
  .lead{font-size:15px}
  .hero{padding:140px 0 60px}
  .reel-stage{height:570px}
  .phone{width:275px;height:560px}
  .grid3{gap:16px}
  .feat-card .vis{height:170px}
  .pricing .grid3{grid-template-columns:1fr 1fr}
  .agent-grid{grid-template-columns:1fr 1fr}
  .agent-col.mid{padding-top:0}
  .agent-col.last{grid-column:span 2;flex-direction:row}
  .agent-col.last .agent{flex:1}
  .faq-body{flex-direction:column-reverse}
  .faq-cta{max-width:none}
  .foot{flex-direction:column}
  .foot-l{width:100%;flex-direction:row}
  .foot-l > div{flex:1}
  .case .panel{width:48%}
}
@media (max-width:809px){
  .wrap{padding:0 24px}
  h1{font-size:34px} h2{font-size:30px}
  .nav{top:20px}
  .nav-bar{padding:10px 16px 10px 10px}
  .burger{display:block}
  .nav-links{display:none;position:absolute;top:calc(100% + 8px);left:0;right:0;background:#000;border-radius:12px;padding:20px;flex-direction:column;gap:12px;text-align:center}
  .nav.open .nav-links{display:flex}
  .nav .bar-cta{display:none}
  .nav.open .nav-links .mob-cta{display:flex}
  .hero{padding:120px 0 60px}
  .head{margin-bottom:30px;gap:12px}
  .reel-stage{height:490px}
  .tile{width:267px;height:325px}
  .phone{width:226px;height:460px;border-radius:40px;padding:8px}
  .phone .screen{border-radius:33px}
  .phone .chat{inset:92px 10px 76px}
  .grid3,.pricing .grid3{grid-template-columns:1fr}
  .partners{padding:0 24px 60px}
  .case{height:540px}
  .case .panel{left:20px;right:20px;top:20px;width:auto}
  .case .metric{font-size:40px}
  .case .body{padding:20px}
  .case h3{font-size:28px} .case p{font-size:17px}
  .agent-grid{grid-template-columns:1fr}
  .agent-col.last{grid-column:auto;flex-direction:column}
  .tcard{width:320px;height:380px}
  .acc-q{font-size:16px}
  .ring3d{height:420px}
  .carousel{transform:scale(.75)}
  .foot-l{flex-direction:column}
  .foot-r{grid-template-columns:1fr}
}
.mob-cta{display:none}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}.rv{opacity:1;transform:none}.msg{opacity:1;transform:none}}
</style>
</head>
<body>

<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="i-spark" viewBox="0 0 24 24"><path d="M12 2c.6 4.6 2.4 7.4 10 10-7.6 2.6-9.4 5.4-10 10-.6-4.6-2.4-7.4-10-10 7.6-2.6 9.4-5.4 10-10Z" fill="currentColor"/></symbol>
    <symbol id="i-check" viewBox="0 0 20 20"><circle cx="10" cy="10" r="9" fill="currentColor"/><path d="m6 10.2 2.6 2.6L14 7.4" fill="none" stroke="var(--ck,#fff)" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/></symbol>
    <symbol id="i-star" viewBox="0 0 13 13"><path fill="currentColor" d="M6.27 0c.61 0 1.1.46 1.4 1.09l1.03 2.07c.1.2.4.36.51.38l1.86.31c.67.11 1.24.44 1.42 1.02.18.57-.09 1.17-.57 1.65l-1.45 1.46c-.13.13-.21.48-.18.66l.41 1.8c.17.75.11 1.5-.41 1.88-.53.39-1.26.22-1.92-.18l-1.74-1.04c-.22-.13-.48-.13-.71 0l-1.74 1.04c-.66.4-1.38.56-1.91.17-.53-.39-.59-1.13-.42-1.88l.41-1.8c.04-.18-.04-.53-.18-.66L.62 6.52C.14 6.03-.12 5.44.06 4.86c.18-.57.74-.9 1.41-1.01l1.86-.31c.12-.02.42-.18.5-.38l1.03-2.07C5.17.46 5.66 0 6.27 0Z"/></symbol>
    <symbol id="i-x" viewBox="0 0 24 24"><path d="M4 4l16 16M20 4 4 20" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/></symbol>
    <symbol id="i-li" viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="4" fill="none" stroke="currentColor" stroke-width="1.5"/><path d="M8 10v7M8 7v.01M12 17v-4a2.5 2.5 0 0 1 5 0v4M12 10v7" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/></symbol>
    <symbol id="i-gh" viewBox="0 0 24 24"><path d="M9 19c-4 1.5-4-2-6-2.5m12 5v-3.5c0-1 .1-1.4-.5-2 2.8-.3 5.5-1.4 5.5-6a4.6 4.6 0 0 0-1.3-3.2 4.2 4.2 0 0 0-.1-3.2s-1.1-.3-3.5 1.3a12 12 0 0 0-6.2 0C6.5 2.8 5.4 3.1 5.4 3.1a4.2 4.2 0 0 0-.1 3.2A4.6 4.6 0 0 0 4 9.5c0 4.6 2.7 5.7 5.5 6-.6.6-.6 1.2-.5 2V21" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/></symbol>
    <symbol id="i-dc" viewBox="0 0 24 24"><path d="M8 6c-2 .3-3.4 1-4 1.5C2.5 10.5 2 13.5 2.3 16.5 4 17.8 5.6 18.5 7 19l1-1.8M16 6c2 .3 3.4 1 4 1.5 1.5 3 2 6 1.7 9-1.7 1.3-3.3 2-4.7 2.5l-1-1.8M7.5 16.5c3 1.3 6 1.3 9 0M8 6.5c2.7-.8 5.3-.8 8 0" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/><circle cx="9" cy="12.5" r="1.3" fill="currentColor"/><circle cx="15" cy="12.5" r="1.3" fill="currentColor"/></symbol>
    <symbol id="i-yt" viewBox="0 0 24 24"><rect x="2.5" y="5" width="19" height="14" rx="4" fill="none" stroke="currentColor" stroke-width="1.5"/><path d="M10 9v6l5-3Z" fill="currentColor"/></symbol>
    <symbol id="i-arrow" viewBox="0 0 24 24"><path d="M5 19 19 5M8 5h11v11" fill="none" stroke="#000" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></symbol>
    <symbol id="i-down" viewBox="0 0 24 24"><path d="M12 5v14M5 12l7 7 7-7" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/></symbol>
    <symbol id="i-up" viewBox="0 0 24 24"><path d="M12 19V5M5 12l7-7 7 7" fill="none" stroke="#000" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"/></symbol>
    <symbol id="i-mail" viewBox="0 0 24 24"><rect x="3" y="5" width="18" height="14" rx="2" fill="none" stroke="#000" stroke-width="2"/><path d="m3 7 9 6 9-6" fill="none" stroke="#000" stroke-width="2"/></symbol>
    <symbol id="i-doc" viewBox="0 0 24 24"><path d="M6 2h9l5 5v15H6Z" fill="none" stroke="#000" stroke-width="2" stroke-linejoin="round"/><path d="M9 13h8M9 17h6" stroke="#000" stroke-width="2" stroke-linecap="round"/></symbol>
    <symbol id="i-pin" viewBox="0 0 24 24"><path d="M12 22s7-6.2 7-12a7 7 0 1 0-14 0c0 5.8 7 12 7 12Z" fill="none" stroke="#000" stroke-width="2"/><circle cx="12" cy="10" r="2.5" fill="none" stroke="#000" stroke-width="2"/></symbol>
  </defs>
</svg>

<div class="glow"></div>

<!-- NAV -->
<header class="nav" id="nav" data-section="nav">
  <div class="nav-bar">
    <a href="#" class="logo"><span class="mark"><svg width="18" height="18" style="color:#d2e823"><use href="#i-spark"/></svg></span>Synthra</a>
    <nav class="nav-links">
      <a href="#">Home</a><a href="#features">Product</a><a href="#agents">Agents</a><a href="#cases">Customers</a><a href="#pricing">Pricing</a>
      <a href="#contact" class="btn lime mob-cta">Start Free</a>
    </nav>
    <a href="#contact" class="btn lime bar-cta" style="padding:14px 24px">Start Free</a>
    <button class="burger" aria-label="Menu" onclick="document.getElementById('nav').classList.toggle('open')">
      <svg width="30" height="30" viewBox="0 0 24 24"><path d="M3.75 6h16.5M3.75 12h16.5M3.75 18h16.5" stroke="#fff" stroke-width="1.5" stroke-linecap="round"/></svg>
    </button>
  </div>
</header>

<!-- HERO -->
<section class="hero" data-section="hero">
  <div class="wrap head">
    <span class="tag fill rv">New · Synthra Agents 2.0 is live</span>
    <h1 class="rv d1">The AI workspace that <span class="grad-text">thinks, writes, and ships</span> with your team</h1>
    <p class="lead rv d2">Synthra brings specialist AI agents into one workspace — research, content, analytics, and automation that learn your business and get work done, not just suggested.</p>
    <div class="btn-row rv d3">
      <a href="#cases" class="btn light">See it in action</a>
      <a href="#contact" class="btn dark">Start free — no card</a>
    </div>
  </div>
  <div class="reel-stage">
    <div class="ticker" id="heroTicker"></div>
    <div class="phone">
      <div class="screen surface">
        <div class="mesh" style="background:radial-gradient(at 20% 15%,#3d4a0b 0,transparent 45%),radial-gradient(at 85% 35%,#1f3b4a 0,transparent 45%),radial-gradient(at 40% 95%,#2a1f4f 0,transparent 50%),#07080a"></div>
        <div class="orb" style="width:180px;height:180px;background:#d2e82355;left:-40px;top:120px"></div>
        <div class="orb" style="width:160px;height:160px;background:#7ee7c440;right:-50px;bottom:120px;animation-delay:-5s"></div>
        <div class="island"></div>
        <div class="appbar"><b><span class="mark" style="width:26px;height:26px;border-radius:8px"><svg width="12" height="12" style="color:#d2e823"><use href="#i-spark"/></svg></span>Synthra</b><span class="mono" style="font-size:10px;color:#fff9">Atlas · online</span></div>
        <div class="chat" id="chat"></div>
        <div class="composer glass"><span>Ask Synthra anything…</span><b class="send"><svg width="16" height="16"><use href="#i-up"/></svg></b></div>
      </div>
    </div>
  </div>
</section>

<!-- PARTNERS -->
<section class="partners" data-section="partners">
  <p class="rv">Trusted by 12,000+ teams moving faster with AI</p>
  <div class="marquee"><div class="track" id="brands"></div></div>
</section>

<!-- FEATURES -->
<section class="features" id="features" data-section="features">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">Product</span>
      <h2 class="rv d1">One workspace. Every kind of work, accelerated by AI.</h2>
      <p class="lead rv d2">Connect your tools once. Synthra reasons over your data, drafts the work, and runs the follow-through.</p>
    </div>
    <div class="grid3">
      <article class="feat-card surface rv">
        <div class="mesh" style="background:radial-gradient(at 10% 0%,#2f3a08 0,transparent 50%),#090a07"></div>
        <div class="vis glass" style="padding:16px;display:flex;flex-direction:column;gap:10px;border-radius:16px">
          <div class="orb" style="width:140px;height:140px;background:#d2e82366;right:-30px;top:-30px"></div>
          <div class="bubble me" style="position:relative;z-index:2">Summarize Q3 churn drivers</div>
          <div class="bubble ai glass" style="position:relative;z-index:2;width:85%">
            <div style="display:flex;gap:6px;align-items:center;color:#d2e823;font-size:11px;font-weight:600"><svg width="12" height="12"><use href="#i-spark"/></svg>Atlas · 4 sources</div>
            <div class="skel" style="width:95%"></div><div class="skel" style="width:80%"></div><div class="skel" style="width:60%"></div>
          </div>
        </div>
        <div class="txt"><h3>Ask Anything</h3><p>Grounded answers from your docs, data, and the web — with citations you can trust.</p></div>
        <span class="arrow-btn"><svg width="22" height="22"><use href="#i-arrow"/></svg></span>
        <div class="shine"></div>
      </article>
      <article class="feat-card surface rv d1">
        <div class="mesh" style="background:radial-gradient(at 90% 0%,#0f3a33 0,transparent 50%),#07090a"></div>
        <div class="vis" style="background:linear-gradient(160deg,#ffffff0d,#ffffff03);border:1px solid #ffffff1a">
          <svg viewBox="0 0 300 230" style="position:absolute;inset:0;width:100%;height:100%">
            <defs><linearGradient id="fl" x1="0" x2="1"><stop offset="0" stop-color="#d2e823"/><stop offset="1" stop-color="#7ee7c4"/></linearGradient>
              <filter id="gl"><feGaussianBlur stdDeviation="3"/><feMerge><feMergeNode/><feMergeNode in="SourceGraphic"/></feMerge></filter></defs>
            <g fill="none" stroke="url(#fl)" stroke-width="2" filter="url(#gl)">
              <path d="M70 60 C130 60 120 115 160 115"/><path d="M70 170 C130 170 120 115 160 115"/><path d="M200 115 C230 115 230 70 250 70"/><path d="M200 115 C230 115 230 165 250 165"/>
            </g>
            <g fill="#fff"><circle r="3.5"><animateMotion dur="2.2s" repeatCount="indefinite" path="M70 60 C130 60 120 115 160 115"/></circle>
              <circle r="3.5"><animateMotion dur="2.2s" begin="1.1s" repeatCount="indefinite" path="M70 170 C130 170 120 115 160 115"/></circle>
              <circle r="3.5"><animateMotion dur="1.8s" repeatCount="indefinite" path="M200 115 C230 115 230 70 250 70"/></circle>
              <circle r="3.5"><animateMotion dur="1.8s" begin=".9s" repeatCount="indefinite" path="M200 115 C230 115 230 165 250 165"/></circle></g>
            <g font-family="sans-serif" font-size="10" fill="#fff">
              <rect x="22" y="44" width="56" height="32" rx="9" fill="#ffffff14" stroke="#ffffff30"/><text x="50" y="64" text-anchor="middle">Email</text>
              <rect x="22" y="154" width="56" height="32" rx="9" fill="#ffffff14" stroke="#ffffff30"/><text x="50" y="174" text-anchor="middle">CRM</text>
              <rect x="152" y="95" width="56" height="40" rx="12" fill="#d2e823"/><text x="180" y="119" text-anchor="middle" fill="#000" font-weight="700">AI</text>
              <rect x="232" y="54" width="56" height="32" rx="9" fill="#ffffff14" stroke="#ffffff30"/><text x="260" y="74" text-anchor="middle">Slack</text>
              <rect x="232" y="150" width="56" height="32" rx="9" fill="#ffffff14" stroke="#ffffff30"/><text x="260" y="170" text-anchor="middle">Report</text>
            </g>
          </svg>
        </div>
        <div class="txt"><h3>Automate Workflows</h3><p>Describe a process in plain English. Agents build it, run it, and report back.</p></div>
        <span class="arrow-btn"><svg width="22" height="22"><use href="#i-arrow"/></svg></span>
        <div class="shine" style="animation-delay:-2s"></div>
      </article>
      <article class="feat-card surface rv d2">
        <div class="mesh" style="background:radial-gradient(at 50% 0%,#2a2260 0,transparent 55%),#08080b"></div>
        <div class="vis" style="background:linear-gradient(160deg,#ffffff0d,#ffffff03);border:1px solid #ffffff1a">
          <svg viewBox="0 0 300 230" style="position:absolute;inset:0;width:100%;height:100%">
            <defs><linearGradient id="ar" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#d2e823" stop-opacity=".55"/><stop offset="1" stop-color="#d2e823" stop-opacity="0"/></linearGradient></defs>
            <g stroke="#ffffff12"><line x1="20" y1="60" x2="280" y2="60"/><line x1="20" y1="110" x2="280" y2="110"/><line x1="20" y1="160" x2="280" y2="160"/></g>
            <path d="M20 180 L60 165 L100 172 L140 130 L180 140 L220 90 L280 55 L280 200 L20 200Z" fill="url(#ar)"/>
            <path d="M20 180 L60 165 L100 172 L140 130 L180 140 L220 90 L280 55" fill="none" stroke="#d2e823" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" stroke-dasharray="400" stroke-dashoffset="400"><animate attributeName="stroke-dashoffset" values="400;0;0" dur="5s" repeatCount="indefinite"/></path>
            <path d="M20 190 L60 185 L100 178 L140 170 L180 160 L220 150 L280 130" fill="none" stroke="#8b7bff" stroke-width="2" stroke-dasharray="5 6"/>
            <circle cx="220" cy="90" r="6" fill="#d2e823"><animate attributeName="r" values="5;9;5" dur="2s" repeatCount="indefinite"/></circle>
            <g transform="translate(150 22)"><rect width="120" height="44" rx="10" fill="#ffffff18" stroke="#ffffff30"/><text x="12" y="18" fill="#fffa" font-size="9" font-family="sans-serif">Forecast · Nov</text><text x="12" y="35" fill="#fff" font-size="15" font-weight="700" font-family="sans-serif">+24.8%</text></g>
          </svg>
        </div>
        <div class="txt"><h3>Insights &amp; Forecasts</h3><p>Ask in words, get charts. Synthra spots trends and flags what needs attention.</p></div>
        <span class="arrow-btn"><svg width="22" height="22"><use href="#i-arrow"/></svg></span>
        <div class="shine" style="animation-delay:-4s"></div>
      </article>
    </div>
  </div>
</section>

<!-- CUSTOMER STORIES -->
<section class="cases" id="cases" data-section="customer-stories">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">Customer Stories</span>
      <h2 class="rv d1">Results you can measure, not just demo</h2>
      <p class="lead rv d2">Teams use Synthra to cut busywork, answer faster, and grow revenue.</p>
    </div>
    <div class="stack" id="caseStack"></div>
  </div>
</section>

<!-- PRICING -->
<section class="pricing" id="pricing" data-section="pricing">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">Pricing</span>
      <h2 class="rv d1">Start free. Scale when AI starts paying for itself.</h2>
      <p class="lead rv d2">Simple per-seat pricing. Every plan includes a 14-day trial of Pro.</p>
    </div>
    <div class="grid3 rv">
      <div class="price">
        <div class="top"><div class="row"><h3>Starter</h3></div><p class="desc">For individuals exploring AI for everyday work.</p></div>
        <div class="amt"><b>$0</b><span>/month</span></div>
        <div class="feats"><p>Features included:</p><ul style="--ck:#fff;color:#0a0a0a">
          <li><svg width="20" height="20"><use href="#i-check"/></svg>500 AI messages / month</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>1 agent (Atlas Research)</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Upload docs up to 50MB</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>3 integrations</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Community support</li></ul></div>
        <a href="#contact" class="btn dark block">Start Free</a>
      </div>
      <div class="price feat surface">
        <div class="mesh" style="background:radial-gradient(at 50% -10%,#d2e823 0,#8fa312 18%,transparent 45%),radial-gradient(at 100% 100%,#1f3b4a 0,transparent 50%),#07080a"></div>
        <div class="orb" style="width:200px;height:200px;background:#d2e82340;right:-60px;top:40%"></div>
        <div class="top"><div class="row"><h3 style="color:#0a0a0a">Pro</h3><span class="badge"><svg width="14" height="14" style="color:#a5b00f"><use href="#i-spark"/></svg>Most popular</span></div>
          <p class="desc" style="color:#1a1a1a">For teams that want AI doing real work every day.</p></div>
        <div class="amt"><b>$29</b><span>/seat/month</span></div>
        <div class="feats"><p>Features included:</p><ul style="--ck:#0a0a0a;color:#d2e823">
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Everything in Starter</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Unlimited AI messages</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">All 6 specialist agents</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Workflow automations</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Unlimited integrations</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Shared team memory</span></li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg><span style="color:#fff">Priority support</span></li></ul></div>
        <a href="#contact" class="btn light block" style="border:0">Start 14-day trial</a>
        <div class="shine"></div>
      </div>
      <div class="price">
        <div class="top"><div class="row"><h3>Enterprise</h3></div><p class="desc">For organizations deploying AI at scale, securely.</p></div>
        <div class="amt"><b>Custom</b></div>
        <div class="feats"><p>Features included:</p><ul style="--ck:#fff;color:#0a0a0a">
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Everything in Pro</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>SSO, SCIM &amp; audit logs</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Private model deployment</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Custom agents &amp; fine-tuning</li>
          <li><svg width="20" height="20"><use href="#i-check"/></svg>Dedicated success manager</li></ul></div>
        <a href="#contact" class="btn dark block">Talk to Sales</a>
      </div>
    </div>
  </div>
</section>

<!-- AGENTS -->
<section class="agents" id="agents" data-section="agents">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">Agents</span>
      <h2 class="rv d1">Meet your new AI team</h2>
      <p class="lead rv d2">Six specialist agents that share context, hand off work, and never sleep.</p>
    </div>
    <div class="agent-grid" id="agentGrid"></div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testi" data-section="testimonials">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">Testimonials</span>
      <h2 class="rv d1">Loved by teams who ship</h2>
      <p class="lead rv d2">Don’t take our word for it — hear from the people using Synthra every day.</p>
    </div>
  </div>
  <div class="t-wrap rv"><div class="t-track" id="tTrack"></div></div>
</section>

<!-- FAQ -->
<section class="faq" data-section="faq">
  <div class="wrap">
    <div class="head">
      <span class="tag rv">FAQ</span>
      <h1 class="rv d1">Frequently Asked Questions</h1>
      <p class="lead rv d2">Everything you need to know about Synthra</p>
    </div>
    <div class="faq-body">
      <div class="faq-cta rv">
        <div style="position:relative;width:200px;height:200px">
          <div style="position:absolute;inset:10px;border-radius:50%;background:radial-gradient(circle at 32% 28%,#fff 0 5%,#e8f56a 22%,#6d7a06 60%,#0a0a0a 100%);box-shadow:0 20px 50px -10px #0007,inset -18px -24px 40px #0008"></div>
          <div style="position:absolute;inset:-6px;border-radius:50%;border:1px dashed #0a0a0a55;animation:spin 20s linear infinite"></div>
          <div class="glass" style="position:absolute;left:-10px;top:34px;padding:8px 12px;font-size:12px;font-weight:600;color:#0a0a0a;background:#ffffffaa;border-color:#fff;animation:drift 7s ease-in-out infinite">Is my data private?</div>
          <div class="glass" style="position:absolute;right:-16px;bottom:30px;padding:8px 12px;font-size:12px;font-weight:600;color:#fff;background:#0a0a0acc;animation:drift 8s ease-in-out infinite reverse"><span class="typing"><i></i><i></i><i></i></span></div>
        </div>
        <div class="txt"><h3>Still have questions?</h3><p>Our team (and our agents) reply in minutes, not days.</p><a href="#contact" class="btn dark block" style="--fx:#fff;margin-top:8px">Contact Us</a></div>
      </div>
      <div class="acc rv d1" id="acc"></div>
    </div>
  </div>
</section>

<!-- CTA -->
<section class="cta" id="contact" data-section="cta">
  <div class="glowcta"></div>
  <div class="wrap" style="position:relative">
    <div class="head" style="margin-bottom:0">
      <span class="tag rv">Get Started</span>
      <h2 class="rv d1">Put AI to work for your team today</h2>
      <p class="lead rv d2">Set up in five minutes. See your first automation run before lunch.</p>
    </div>
    <div class="ring3d"><div class="carousel" id="carousel"></div></div>
    <div class="btn-row rv"><a href="#contact" class="btn lime">Start Free</a><a href="#contact" class="btn light" style="background:transparent;color:#fff">Book a Demo</a></div>
  </div>
</section>

<!-- FOOTER -->
<footer class="footer" data-section="footer">
  <div class="wrap">
    <div class="foot rv">
      <div class="foot-l">
        <div>
          <a href="#" class="logo"><span class="mark"><svg width="18" height="18" style="color:#d2e823"><use href="#i-spark"/></svg></span>Synthra</a>
          <p>The AI workspace where specialist agents research, write, analyze, and automate — so your team can focus on what matters.</p>
        </div>
        <div>
          <h4>Follow Us</h4>
          <div class="soc-grid">
            <a href="https://x.com" target="_blank" rel="noopener"><svg width="18" height="18"><use href="#i-x"/></svg>X</a>
            <a href="https://linkedin.com" target="_blank" rel="noopener"><svg width="22" height="22"><use href="#i-li"/></svg>LinkedIn</a>
            <a href="https://github.com" target="_blank" rel="noopener"><svg width="22" height="22"><use href="#i-gh"/></svg>GitHub</a>
            <a href="https://youtube.com" target="_blank" rel="noopener"><svg width="22" height="22"><use href="#i-yt"/></svg>YouTube</a>
          </div>
        </div>
      </div>
      <div class="foot-r">
        <div><h5>Product</h5><ul><li><a href="#features">Overview</a></li><li><a href="#agents">Agents</a></li><li><a href="#features">Automations</a></li><li><a href="#pricing">Pricing</a></li><li><a href="#">Changelog</a></li></ul></div>
        <div><h5>Resources</h5><ul><li><a href="#">Docs</a></li><li><a href="#">API Reference</a></li><li><a href="#cases">Customer Stories</a></li><li><a href="#">Blog</a></li></ul></div>
        <div><h5>Company</h5><ul><li><a href="#">About</a></li><li><a href="#">Careers</a></li><li><a href="#">Security &amp; Trust</a></li><li><a href="#">Terms &amp; Privacy</a></li></ul></div>
        <div class="contact"><h5>Get in touch</h5>
          <a href="mailto:hello@synthra.ai"><i><svg width="14" height="14"><use href="#i-mail"/></svg></i>hello@synthra.ai</a>
          <a href="#"><i><svg width="14" height="14"><use href="#i-doc"/></svg></i>docs.synthra.ai</a>
          <a href="#"><i><svg width="14" height="14"><use href="#i-pin"/></svg></i>San Francisco, CA</a>
          <span class="status">All systems operational</span>
        </div>
      </div>
    </div>
  </div>
</footer>

<script>
/* ---------- premium product tiles (replace all videos) ---------- */
const mesh=(a,b,c)=>`<div class="mesh" style="background:radial-gradient(at 15% 10%,${a} 0,transparent 50%),radial-gradient(at 90% 40%,${b} 0,transparent 50%),radial-gradient(at 40% 100%,${c} 0,transparent 55%),#07080a"></div>`;
const tiles=[
 {lab:'Chat · Atlas',m:['#3d4a0b','#1f3b4a','#2a1f4f'],body:`<div style="display:flex;flex-direction:column;gap:8px;margin-top:16px">
   <div class="bubble me">Draft a launch email for our v2 release</div>
   <div class="bubble ai glass">Subject: Meet v2 — 2× faster, half the clicks<div class="skel" style="width:90%"></div><div class="skel" style="width:75%"></div><div class="skel" style="width:55%"></div></div></div>`},
 {lab:'Image · Studio',m:['#5a1e4f','#d2e823','#1d2b6b'],body:`<div style="position:relative;flex:1;margin:14px 0;border-radius:14px;overflow:hidden;background:conic-gradient(from 120deg at 60% 40%,#ff8fb1,#ffd36e,#d2e823,#7ee7c4,#8b7bff,#ff8fb1);filter:saturate(1.2)">
   <div style="position:absolute;inset:0;background:radial-gradient(circle at 30% 70%,#0008,transparent 60%)"></div>
   <div class="orb" style="width:90px;height:90px;background:#fff8;left:30%;top:20%;filter:blur(20px)"></div>
   <div style="position:absolute;inset:0;backdrop-filter:blur(var(--b,0));animation:unblur 5s ease-in-out infinite"></div></div>
   <div class="foot"><div style="display:flex;justify-content:space-between;font-size:12px;color:#fffc"><span>“neon dawn, glass city”</span><span class="mono">87%</span></div><div class="progress"><span></span></div></div>`},
 {lab:'Voice · Echo',m:['#0f3a33','#3d4a0b','#0a1e2e'],body:`<div class="wave" style="margin-top:40px">${Array.from({length:22},(_,i)=>`<span style="height:${30+Math.abs(Math.sin(i*.9))*80}px;animation-delay:-${(i*.11).toFixed(2)}s"></span>`).join('')}</div>
   <div class="foot glass" style="padding:10px 12px;font-size:12.5px;line-height:1.45">“Move the sync to Thursday and loop in design.” <span style="color:#d2e823">✓ Done</span></div>`},
 {lab:'Code · Forge',m:['#1d2b6b','#0f3a33','#3d4a0b'],body:`<div class="glass mono" style="margin-top:14px;padding:12px;font-size:11px;line-height:1.75;flex:1">
   <div><span style="color:#8b7bff">const</span> <span style="color:#7ee7c4">agent</span> = synthra.<span style="color:#d2e823">agent</span>(<span style="color:#ffb38a">"forge"</span>)</div>
   <div><span style="color:#8b7bff">await</span> agent.<span style="color:#d2e823">run</span>({</div><div>&nbsp;&nbsp;task: <span style="color:#ffb38a">"fix failing tests"</span>,</div><div>&nbsp;&nbsp;repo: <span style="color:#ffb38a">"web-app"</span></div><div>})</div>
   <div style="color:#4ade80;margin-top:8px">✓ 14 tests passing</div><div class="cursor" style="color:#fff8">PR #482 opened </div></div>`},
 {lab:'Insights · Lens',m:['#2a2260','#1f3b4a','#3d4a0b'],body:`<div style="margin-top:18px"><div style="font-size:12px;color:#fffa">Revenue this week</div><div style="font-size:34px;font-weight:600;letter-spacing:-.02em">$184.2K <span style="font-size:13px;color:#4ade80">▲ 18%</span></div></div>
   <svg viewBox="0 0 260 120" style="margin-top:auto;width:100%"><defs><linearGradient id="tg" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#d2e823" stop-opacity=".5"/><stop offset="1" stop-color="#d2e823" stop-opacity="0"/></linearGradient></defs>
   <path d="M0 100 L40 85 L80 90 L120 60 L160 66 L200 35 L260 20 L260 120 L0 120Z" fill="url(#tg)"/><path d="M0 100 L40 85 L80 90 L120 60 L160 66 L200 35 L260 20" fill="none" stroke="#d2e823" stroke-width="3" stroke-linejoin="round"/><circle cx="200" cy="35" r="5" fill="#fff"/></svg>`},
 {lab:'Automation · Relay',m:['#0f3a33','#2a2260','#3d4a0b'],body:`<div style="display:flex;flex-direction:column;gap:8px;margin-top:16px">
   ${['New lead in CRM','Enrich with Atlas','Draft reply with Quill','Notify #sales'].map((t,i)=>`<div class="glass" style="padding:10px 12px;font-size:12.5px;display:flex;align-items:center;gap:10px;border-radius:12px"><span style="width:22px;height:22px;border-radius:7px;display:grid;place-items:center;font-size:11px;font-weight:700;background:${i===1||i===2?'#d2e823':'#ffffff22'};color:${i===1||i===2?'#000':'#fff'}">${i+1}</span>${t}<span style="margin-left:auto;color:#4ade80">✓</span></div>`).join('')}</div>`}
];
function tile(t,mini){
  return `<div class="tile surface">${mesh(...t.m)}<div class="orb" style="width:140px;height:140px;background:${t.m[0]};left:${Math.random()*60}%;top:${Math.random()*50}%;animation-delay:-${Math.random()*10}s"></div>
   <div class="content"><div class="label"><i></i>${t.lab}</div>${mini?t.body.replace(/margin-top:\d+px/,'margin-top:10px'):t.body}</div><div class="shine" style="animation-delay:-${(Math.random()*6).toFixed(1)}s"></div></div>`;
}
/* ---------- decorative art tiles for the hero ticker ---------- */
const halftone=(()=>{let d='';for(let y=0;y<18;y++)for(let x=0;x<15;x++){const cx=10+x*20,cy=10+y*20,dist=Math.hypot(cx-170,cy-150)/150,r=Math.max(0,7.5*(1-dist));if(r>.6)d+=`<circle cx="${cx}" cy="${cy}" r="${r.toFixed(2)}"/>`;}return d})();
const topo=Array.from({length:11},(_,i)=>{const s=1-i*.085;return `<path transform="translate(148 180) scale(${s.toFixed(3)}) rotate(${i*9})" d="M0-170C70-160 160-110 150-20 140 70 90 150 0 160-90 170-160 90-165 0-170-90-80-180 0-170Z"/>`}).join('');
const artTiles=[
 /* liquid blobs on cream */
 `<div style="position:absolute;inset:0;background:#eef2d4"></div>
  <div class="morph" style="width:230px;height:230px;left:-30px;top:30px;background:radial-gradient(circle at 35% 30%,#f4fb9c,#d2e823 55%,#9fb20d)"></div>
  <div class="morph" style="width:190px;height:190px;right:-50px;bottom:-20px;background:radial-gradient(circle at 40% 35%,#ece6ff,#a99bff 60%,#6b5cd6);animation-delay:-4s;mix-blend-mode:multiply"></div>
  <div style="position:absolute;width:120px;height:120px;border:1.5px solid #0a0a0a33;border-radius:50%;left:110px;top:70px;animation:drift 10s ease-in-out infinite"></div>`,
 /* stacked arches on deep olive */
 `<div style="position:absolute;inset:0;background:linear-gradient(#1b1f07,#2c3310)"></div>
  <div style="position:absolute;width:70px;height:70px;border-radius:50%;left:170px;top:52px;background:radial-gradient(circle at 35% 30%,#fff7d6,#ffd36e);box-shadow:0 0 60px #ffd36e88;animation:drift 9s ease-in-out infinite"></div>
  <div class="arch" style="left:28px;width:150px;height:230px;background:#e9edc9"></div>
  <div class="arch" style="left:96px;width:150px;height:180px;background:#d2e823"></div>
  <div class="arch" style="left:160px;width:110px;height:120px;background:#a99bff"></div>
  <div class="arch" style="left:58px;width:70px;height:110px;background:#1b1f07"></div>`,
 /* aurora ribbons */
 `<div style="position:absolute;inset:0;background:#06070a"></div>
  <div class="aurora" style="background:conic-gradient(from 90deg at 50% 50%,transparent,#7ee7c4 18%,transparent 30%,#d2e823 52%,transparent 64%,#8b7bff 82%,transparent)"></div>
  <div style="position:absolute;inset:0;background:radial-gradient(ellipse at 50% 120%,#06070a 30%,transparent 70%)"></div>
  ${Array.from({length:14},(_,i)=>`<i class="star" style="left:${(i*53)%280+8}px;top:${(i*37)%150+14}px;animation-delay:-${i*.4}s"></i>`).join('')}`,
 /* glass sphere on pastel mesh */
 `<div style="position:absolute;inset:0;background:radial-gradient(at 15% 10%,#f3fbc9,transparent 55%),radial-gradient(at 90% 25%,#e2dcff,transparent 55%),radial-gradient(at 50% 100%,#c9f3e4,transparent 60%),#f4f6ea"></div>
  <div style="position:absolute;left:68px;bottom:58px;width:160px;height:26px;border-radius:50%;background:radial-gradient(closest-side,#0a0a0a40,transparent);animation:shadowb 6s ease-in-out infinite"></div>
  <div style="position:absolute;left:68px;top:70px;width:160px;height:160px;border-radius:50%;
    background:radial-gradient(circle at 30% 25%,#fff 0 6%,transparent 22%),radial-gradient(circle at 70% 80%,#d2e82399,transparent 45%),radial-gradient(circle at 50% 50%,#ffffff22,#a99bff55 70%,#6b5cd6aa);
    box-shadow:inset -12px -18px 40px #6b5cd655,inset 10px 10px 30px #ffffffaa,0 30px 50px -20px #6b5cd666;animation:bob 6s ease-in-out infinite"></div>`,
 /* topographic contours on lime */
 `<div style="position:absolute;inset:0;background:radial-gradient(circle at 50% 50%,#e8f56a,#c4d81e)"></div>
  <svg viewBox="0 0 296 360" style="position:absolute;inset:0;width:100%;height:100%"><g fill="none" stroke="#1b1f07" stroke-width="1.4" opacity=".75" style="transform-origin:148px 180px;animation:spin 60s linear infinite">${topo}</g>
  <circle cx="148" cy="180" r="10" fill="#1b1f07"/></svg>`,
 /* halftone sphere */
 `<div style="position:absolute;inset:0;background:#0b0c08"></div>
  <svg viewBox="0 0 296 360" style="position:absolute;inset:0;width:100%;height:100%"><defs><linearGradient id="htg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#f4fb9c"/><stop offset="1" stop-color="#7ee7c4"/></linearGradient></defs>
  <g fill="url(#htg)" style="animation:breathe 7s ease-in-out infinite;transform-origin:170px 150px">${halftone}</g></svg>`,
 /* op-art rings on cream */
 `<div style="position:absolute;inset:0;background:#f6f4ec"></div>
  <svg viewBox="0 0 296 360" style="position:absolute;inset:0;width:100%;height:100%">
   <circle cx="190" cy="120" r="70" fill="#d2e823"/>
   <g fill="none" stroke="#0a0a0a" stroke-width="1.6">${Array.from({length:12},(_,i)=>`<circle cx="${110+i*3}" cy="${210-i*2}" r="${14+i*12}"/>`).join('')}</g>
   <circle cx="190" cy="120" r="70" fill="#d2e823" style="mix-blend-mode:multiply"><animate attributeName="cx" values="190;170;190" dur="8s" repeatCount="indefinite"/></circle></svg>`,
 /* rotating petals on lilac */
 `<div style="position:absolute;inset:0;background:linear-gradient(160deg,#ece6ff,#c9bfff)"></div>
  <div style="position:absolute;left:148px;top:180px;width:0;height:0;animation:spin 30s linear infinite">
   ${Array.from({length:8},(_,i)=>`<span class="petal" style="transform:rotate(${i*45}deg);background:${['#d2e823','#7ee7c4','#ffffff','#ff8fb1'][i%4]}"></span>`).join('')}</div>
  <div style="position:absolute;left:128px;top:160px;width:40px;height:40px;border-radius:50%;background:#1b1f07"></div>`
];
const artStyle=document.createElement('style');
artStyle.textContent=`
.tile.art{background:#0a0a0a}
.tile.art::after{opacity:.14}
.morph{position:absolute;border-radius:42% 58% 63% 37%/45% 38% 62% 55%;animation:morph 12s ease-in-out infinite;filter:blur(.5px)}
@keyframes morph{25%{border-radius:60% 40% 35% 65%/55% 60% 40% 45%;transform:translate(14px,-10px) rotate(20deg)}50%{border-radius:38% 62% 55% 45%/40% 45% 55% 60%;transform:translate(-8px,16px) rotate(-10deg)}75%{border-radius:55% 45% 40% 60%/62% 38% 62% 38%;transform:translate(10px,6px) rotate(14deg)}}
.arch{position:absolute;bottom:0;border-radius:999px 999px 0 0}
.aurora{position:absolute;inset:-40%;filter:blur(38px);opacity:.9;animation:spin 16s linear infinite}
.star{position:absolute;width:2px;height:2px;border-radius:50%;background:#fff;box-shadow:0 0 6px #fff;animation:blink 2.6s ease-in-out infinite}
@keyframes bob{50%{transform:translateY(-16px)}}
@keyframes shadowb{50%{transform:scaleX(.8);opacity:.6}}
@keyframes breathe{50%{transform:scale(1.06)}}
.petal{position:absolute;left:-26px;top:-120px;width:52px;height:120px;border-radius:50%;transform-origin:26px 120px;mix-blend-mode:multiply;opacity:.85}`;
document.head.appendChild(artStyle);
/* light product hints layered over the art — one small element per card */
const sp=`<svg width="12" height="12" style="color:#a5b00f;flex:none"><use href="#i-spark"/></svg>`;
const overlays=[
 /* liquid → writing */
 `<div class="hint light" style="left:18px;right:18px;bottom:18px;flex-direction:column;align-items:flex-start;gap:6px"><span class="kick">${sp}Quill · writing</span><span style="font-size:14px;line-height:1.4;font-style:italic">“A launch story people actually finish reading<span class="cursor"></span>”</span></div>`,
 /* arches → automation */
 `<div class="hint light" style="left:18px;top:18px"><span class="dotlive"></span>4 workflows running</div>`,
 /* aurora → voice */
 `<div class="hint dark" style="left:50%;bottom:22px;transform:translateX(-50%);gap:3px;padding:10px 14px">${Array.from({length:12},(_,i)=>`<i class="wbar" style="height:${8+Math.abs(Math.sin(i*1.1))*18}px;animation-delay:-${(i*.12).toFixed(2)}s"></i>`).join('')}<span style="margin-left:8px">Echo · listening</span></div>`,
 /* sphere → agent thinking */
 `<div class="hint light" style="left:50%;bottom:22px;transform:translateX(-50%)"><span class="typing dk"><i></i><i></i><i></i></span>Atlas is thinking</div>`,
 /* contours → insights */
 `<div class="hint light" style="left:18px;bottom:18px;flex-direction:column;align-items:flex-start;gap:2px"><span class="kick">${sp}Lens · forecast</span><b style="font-size:26px;letter-spacing:-.02em">+24.8%</b></div>`,
 /* halftone → vision */
 `<div class="hint dark" style="left:18px;bottom:18px">${sp.replace('#a5b00f','#d2e823')}Vision · 98% match</div>`,
 /* rings → image studio */
 `<div class="hint light" style="left:18px;right:18px;bottom:18px;flex-direction:column;align-items:stretch;gap:8px"><span class="kick" style="justify-content:space-between;display:flex">Studio · generating<span class="mono">87%</span></span><span class="progress" style="margin:0;background:#0a0a0a18"><span></span></span></div>`,
 /* petals → ideas */
 `<div class="hint light" style="left:18px;top:18px">${sp}12 ideas generated</div>`
];
const hintStyle=document.createElement('style');
hintStyle.textContent=`
.hint{position:absolute;z-index:6;display:flex;align-items:center;gap:8px;padding:9px 13px;border-radius:14px;font-size:12.5px;font-weight:600;
  backdrop-filter:blur(14px) saturate(1.4);-webkit-backdrop-filter:blur(14px) saturate(1.4);box-shadow:0 12px 30px -12px #0005}
.hint.light{background:#ffffffb8;color:#0a0a0a;border:1px solid #ffffffd0}
.hint.dark{background:#0a0a0a8c;color:#fff;border:1px solid #ffffff26}
.hint .kick{display:inline-flex;align-items:center;gap:6px;font-size:11px;font-weight:600;color:#0a0a0a99;letter-spacing:.02em}
.dotlive{width:8px;height:8px;border-radius:50%;background:#4ade80;box-shadow:0 0 8px #4ade80;animation:blink 1.6s infinite}
.wbar{display:block;width:3px;border-radius:3px;background:#d2e823;animation:wv 1.1s ease-in-out infinite}
.typing.dk i{background:#0a0a0a}
.tile.art .morph,.tile.art .aurora,.tile.art .petal{opacity:.9}`;
document.head.appendChild(hintStyle);
const artTile=(a,i)=>`<div class="tile art surface">${a}${overlays[i%overlays.length]}<div class="shine" style="opacity:.5;animation-delay:-${i}s"></div></div>`;
document.getElementById('heroTicker').innerHTML=[...artTiles,...artTiles].map(artTile).join('');
document.getElementById('carousel').innerHTML=Array.from({length:12},(_,i)=>tile(tiles[i%tiles.length],true).replace('class="tile surface"',`class="tile surface" style="--i:${i}"`)).join('');
const st=document.createElement('style');st.textContent='@keyframes unblur{0%{backdrop-filter:blur(18px)}60%,100%{backdrop-filter:blur(0)}}';document.head.appendChild(st);

/* ---------- phone chat ---------- */
const convo=[
 ['me','What should I focus on this week?'],
 ['ai','Three priorities based on your calendar and pipeline:<br>① Close <b>Northwind</b> renewal ($42K)<br>② Ship onboarding v2<br>③ Reply to 6 hot leads'],
 ['me','Draft replies to the leads'],
 ['ai','Done ✦ 6 drafts ready in your inbox, personalized from CRM notes.']
];
const chat=document.getElementById('chat');
function runChat(){
  chat.innerHTML='';let d=400;
  convo.forEach(([who,txt])=>{
    if(who==='ai'){setTimeout(()=>{const t=document.createElement('div');t.className='bubble ai glass msg typingmsg';t.innerHTML='<span class="typing"><i></i><i></i><i></i></span>';chat.appendChild(t);requestAnimationFrame(()=>t.classList.add('show'))},d);d+=1300;}
    setTimeout(()=>{chat.querySelector('.typingmsg')?.remove();const m=document.createElement('div');m.className=`bubble ${who} msg ${who==='ai'?'glass':''}`;m.innerHTML=txt;chat.appendChild(m);requestAnimationFrame(()=>m.classList.add('show'))},d);
    d+=1400;
  });
  setTimeout(runChat,d+3000);
}
runChat();

/* ---------- logos ---------- */
const brands=[['Northwind','c'],['Kinetiq','t'],['Vertexa','d'],['Novalane','s'],['Brightly','h'],['Orbitly','o'],['Havenly','p'],['Quanta','q'],['Solace','w']];
const mark=t=>({c:'<circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="4" fill="var(--bg)"/>',t:'<path d="M12 2 22 20H2Z"/>',d:'<path d="M12 2 22 12 12 22 2 12Z"/>',s:'<rect x="2" y="2" width="20" height="20" rx="6"/><rect x="8" y="8" width="8" height="8" rx="2" fill="var(--bg)"/>',h:'<path d="M12 2l3 7 7 1-5 5 1.5 7L12 18l-6.5 4L7 15 2 10l7-1Z"/>',o:'<circle cx="8" cy="12" r="6"/><circle cx="16" cy="12" r="6" opacity=".5"/>',p:'<path d="M3 12h18M12 3v18" stroke="currentColor" stroke-width="5" stroke-linecap="round"/>',q:'<path d="M2 20 12 4l10 16" fill="none" stroke="currentColor" stroke-width="4" stroke-linejoin="round"/>',w:'<path d="M2 12c3-6 7-6 10 0s7 6 10 0" fill="none" stroke="currentColor" stroke-width="4" stroke-linecap="round"/>'}[t]);
const bHTML=brands.map(([n,t])=>`<div class="brand"><svg viewBox="0 0 24 24" fill="currentColor">${mark(t)}</svg>${n}</div>`).join('');
document.getElementById('brands').innerHTML=bHTML+bHTML;

/* ---------- customer stories ---------- */
const cases=[
 ['Customer Support','Northwind','Deployed Synthra agents across the help desk to resolve tier-1 tickets instantly and route the rest with full context.','68%','tickets resolved by AI',['#3d4a0b','#1f3b4a','#0a0a0a'],'bars'],
 ['Sales','Kinetiq','Automated lead research and first-touch outreach, giving reps back two days a week to spend on live deals.','3.4×','more qualified meetings',['#1d2b6b','#3d4a0b','#2a1f4f'],'line'],
 ['Marketing','Brightly','Turned one brief into a month of on-brand campaigns across email, social and web — reviewed, not rewritten.','11 hrs','saved per marketer weekly',['#5a1e4f','#2a2260','#3d4a0b'],'grid'],
 ['Finance','Quanta','Connected ERP and spreadsheets so leadership gets narrative forecasts and anomaly alerts every Monday.','92%','forecast accuracy',['#0f3a33','#1f3b4a','#3d4a0b'],'line'],
 ['Engineering','Vertexa','Forge agent triages bugs, writes fixes and opens PRs, so engineers review instead of grind.','41%','faster cycle time',['#2a2260','#0f3a33','#1d2b6b'],'code'],
 ['Operations','Havenly','Replaced 40+ manual handoffs with Relay automations that run quietly in the background, 24/7.','$1.2M','annual ops savings',['#3d4a0b','#5a1e4f','#0a1e2e'],'bars']
];
const panelArt={
 bars:`<svg viewBox="0 0 300 110" style="width:100%"><g>${[50,70,45,85,65,95,80].map((h,i)=>`<rect x="${i*42+4}" y="${110-h}" width="28" height="${h}" rx="6" fill="${i===5?'#d2e823':'#ffffff30'}"/>`).join('')}</g></svg>`,
 line:`<svg viewBox="0 0 300 110" style="width:100%"><path d="M0 95 C40 90 60 70 100 72 S160 40 200 38 S260 12 300 8" fill="none" stroke="#d2e823" stroke-width="4" stroke-linecap="round"/><path d="M0 100 C60 98 120 88 180 80 S260 66 300 60" fill="none" stroke="#ffffff55" stroke-width="2" stroke-dasharray="6 6"/></svg>`,
 grid:`<div style="display:grid;grid-template-columns:repeat(3,1fr);gap:8px">${['#ff8fb1,#ffd36e','#d2e823,#7ee7c4','#8b7bff,#ff8fb1','#7ee7c4,#1f3b4a','#ffd36e,#d2e823','#5a1e4f,#8b7bff'].map(g=>`<div style="aspect-ratio:1;border-radius:10px;background:linear-gradient(135deg,${g})"></div>`).join('')}</div>`,
 code:`<div class="mono" style="font-size:12px;line-height:1.8;color:#fffc"><div><span style="color:#4ade80">+</span> handle null session token</div><div><span style="color:#f87171">−</span> legacy retry loop</div><div><span style="color:#4ade80">+</span> add regression test</div><div style="color:#d2e823;margin-top:6px">✓ PR #482 approved</div></div>`
};
document.getElementById('caseStack').innerHTML=cases.map(([t,n,d,mv,ml,m,a],i)=>`
 <a href="#cases" class="case surface" style="top:${100+i*14}px">
   ${mesh(...m).replace('inset:-20%','inset:0')}
   <div class="orb" style="width:380px;height:380px;background:${m[0]};right:5%;top:10%"></div>
   <div class="glass panel"><div class="label" style="display:flex;gap:8px;align-items:center;font-size:12px;color:#fffa;margin-bottom:6px"><svg width="12" height="12" style="color:#d2e823"><use href="#i-spark"/></svg>Synthra impact report</div>
     <div class="metric">${mv}</div><div class="mlabel">${ml}</div>${panelArt[a]}</div>
   <div style="position:absolute;inset:0;background:linear-gradient(180deg,transparent 40%,#000c);z-index:3"></div>
   <div class="body"><span class="pill">${t}</span><h3>${n}</h3><p>${d}</p></div>
   <div class="shine" style="animation-delay:-${i}s"></div>
 </a>`).join('');

/* ---------- agents ---------- */
const agents=[
 ['Atlas','Research Agent','Searches your docs, data and the web, then writes cited briefs in seconds.',['Deep research','Citations','Summaries'],'#6d7a06','#e8f56a'],
 ['Quill','Writing Agent','Drafts emails, posts and docs in your brand voice — and learns from every edit.',['Brand voice','Long-form','Editing'],'#9b2c6b','#ff8fb1'],
 ['Lens','Analytics Agent','Turns plain-English questions into charts, forecasts and anomaly alerts.',['SQL','Forecasting','Dashboards'],'#3b2fa0','#a99bff'],
 ['Forge','Engineering Agent','Reviews code, fixes bugs and opens pull requests that pass your CI.',['Code review','Tests','PRs'],'#0f6b5a','#7ee7c4'],
 ['Relay','Automation Agent','Connects your tools and runs multi-step workflows around the clock.',['500+ apps','Triggers','Approvals'],'#a35a0a','#ffd36e'],
 ['Echo','Voice Agent','Joins meetings, takes notes and turns action items into tasks automatically.',['Transcripts','Action items','Recaps'],'#1f5f8b','#7fd1ff']
];
const agent=([n,r,d,chips,c1,c2])=>`<div class="agent surface" tabindex="0" style="--c1:${c1};--c2:${c2}">
  <div class="mesh" style="inset:0;background:radial-gradient(at 50% 35%,${c1}66 0,transparent 55%),#07080a"></div>
  <div class="core"><div class="halo"></div><div class="orbit"></div><div class="sphere"></div></div>
  <div class="info"><b>${n}</b><span>${r}</span></div>
  <div class="details glass"><div><b style="font-size:20px;font-weight:500;display:block;margin-bottom:4px">${n}</b><span style="font-size:14px;color:${c2}">${r}</span></div>
   <p>${d}</p><div class="chips">${chips.map(c=>`<span>${c}</span>`).join('')}</div></div>
  <div class="shine"></div></div>`;
document.getElementById('agentGrid').innerHTML=
 `<div class="agent-col rv">${agent(agents[0])}${agent(agents[1])}</div>
  <div class="agent-col mid rv d1">${agent(agents[2])}${agent(agents[3])}</div>
  <div class="agent-col last rv d2">${agent(agents[4])}${agent(agents[5])}</div>`;
document.querySelectorAll('.agent').forEach(m=>m.addEventListener('click',()=>m.classList.toggle('open')));

/* ---------- testimonials ---------- */
const t=[['Synthra replaced three tools and a lot of copy-paste. Our support team answers in minutes now, not hours.','Olivia Bennett','Head of Support, Northwind',['#6d7a06','#e8f56a']],
 ['The agents actually finish the work. Atlas writes research briefs my team used to spend a full day on.','Elena Rodriguez','VP Marketing, Brightly',['#9b2c6b','#ff8fb1']],
 ['Security review was painless and the ROI showed up in the first month. It’s now core to how we operate.','Sarah Turner','COO, Havenly',['#1f5f8b','#7fd1ff']],
 ['Forge opens PRs that pass CI on the first try more often than not. It feels like adding two engineers.','Marcus Lee','CTO, Vertexa',['#0f6b5a','#7ee7c4']]];
const star=o=>`<svg width="14" height="14" style="opacity:${o}"><use href="#i-star"/></svg>`;
const tc=([q,n,role,[c1,c2]])=>`<div class="tcard"><div><div class="stars"><div>${star(1)+star(1)+star(1)+star(1)+star(1)}</div>5.0/5</div><blockquote>“${q}”</blockquote></div>
 <div class="author"><div class="avatar" style="background:radial-gradient(circle at 30% 25%,${c2},${c1} 70%)">${n.split(' ').map(w=>w[0]).join('')}</div><div><b>${n}</b><span>${role}</span></div></div></div>`;
const tAll=t.map(tc).join('');
document.getElementById('tTrack').innerHTML=tAll+tAll+tAll+tAll;

/* ---------- faq ---------- */
const faq=[['Is my data used to train AI models?','Never. Your data stays yours — it’s encrypted, isolated per workspace, and never used to train models.'],
 ['Which tools does Synthra connect to?','500+ apps including Slack, Google Workspace, Notion, HubSpot, Salesforce, GitHub and Jira — plus a REST API for anything else.'],
 ['How long does setup take?','Most teams are up and running in under five minutes. Connect a few tools and your agents start learning immediately.'],
 ['Can I build my own agents?','Yes. Pro teams can customize agents with instructions and knowledge; Enterprise adds fully custom agents and fine-tuning.'],
 ['Can I cancel anytime?','Yes — monthly plans with no lock-in. Downgrade to Starter whenever you like and keep your workspace.']];
const acc=document.getElementById('acc');
acc.innerHTML=faq.map(([q,a],i)=>`<div class="acc-item${i===0?' open':''}" tabindex="0"><div class="acc-q">${q}<span class="acc-ic"><svg width="18" height="18"><use href="#i-down"/></svg></span></div><div class="acc-a"><div><p>${a}</p></div></div></div>`).join('');
acc.querySelectorAll('.acc-item').forEach(el=>{
  const go=()=>{const was=el.classList.contains('open');acc.querySelectorAll('.acc-item').forEach(x=>x.classList.remove('open'));if(!was)el.classList.add('open')};
  el.addEventListener('click',go);el.addEventListener('keydown',e=>{if(e.key==='Enter')go()});
});

/* ---------- reveal ---------- */
const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}}),{threshold:.12});
document.querySelectorAll('.rv').forEach(el=>io.observe(el));
document.querySelectorAll('.nav-links a').forEach(a=>a.addEventListener('click',()=>document.getElementById('nav').classList.remove('open')));
</script>
</body>
</html>
```

