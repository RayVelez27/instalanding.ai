INSTALANDING.AI · Linework AI Architect Assistant Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Linework AI Architect Assistant Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/linework-ai-architect-assistant-page

linework-architect-assistant.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Linework AI Architect Assistant Page
  slug     linework-ai-architect-assistant-page
  prompt   https://instalanding.ai/p/linework-ai-architect-assistant-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/linework-ai-architect-assistant-page
  license  Fictional product ("Linework"); every building, client, address, figure and quote is invented.
           Replace names and copy before shipping. Every picture is inline SVG generated in code; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --paper, --ink, --blue (#4353ff) / --blue-soft, --rule,
            --muted, --graphite, --ease / --draw curves; Urbanist (body), Instrument Sans (headings), IBM Plex Mono
  sections  nav, mobile-nav, hero, services, projects, process, studio, quotes, footer, dialogs
            (each carries data-section)
  scripts   one IIFE, no libraries: a stroke "draw system" (pathLength=1 dash offsets with staggered delays);
            nine procedural buildings (B) drawn as ink line sets and as shaded renders; a generated amphitheatre
            hero with a roaming blueprint lens; a filterable skyline with a project panel and a drawing/render
            compare dialog; a scroll-driven five-stage drawing; a studio figure; a harbour-city footer; a quote
            carousel; header, menu, counters and an early-access form
  assets    no image files

  ADAPTING
  - Projects live in P (copy, palette, which builder in B draws it); skyline x positions are in XS.
  - Add a building by writing a B entry that returns {w, h, fill, gy, L:[[class, path], ...]}.
  - prefers-reduced-motion: strokes show fully drawn, animations and transitions are near zero, reveals show.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Linework — AI Architect Assistant</title>
<meta name="description" content="Linework is an AI architect assistant. It reads the site, sketches massing options and drafts drawings line by line, so architects can focus on the decisions that matter.">
<meta name="theme-color" content="#f5f5f1">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Cg fill='none' stroke='%23121212' stroke-width='1.6'%3E%3Crect x='3.5' y='3.5' width='25' height='25'/%3E%3Cpath d='M10 28.5V16.5a6 6 0 0 1 12 0v12M3.5 10.5h25M16 3.5v7'/%3E%3C/g%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@400;500&family=Instrument+Sans:wght@400;500;600&family=Urbanist:wght@400;500;600&display=swap" rel="stylesheet">
<style>
:root{
  --paper:#f5f5f1;--ink:#121212;--blue:#4353ff;--blue-soft:#eef0ff;--rule:#e1e1da;--muted:#86867f;--graphite:#4b4b46;
  --sans:'Urbanist',system-ui,sans-serif;--head:'Instrument Sans',system-ui,sans-serif;--mono:'IBM Plex Mono',ui-monospace,monospace;
  --ease:cubic-bezier(.2,.8,.2,1);--draw:cubic-bezier(.65,.05,.25,1);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth;-webkit-text-size-adjust:100%}
body{background:var(--paper);color:var(--ink);font-family:var(--sans);font-size:16px;line-height:1.5;-webkit-font-smoothing:antialiased;overflow-x:hidden}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:0;cursor:pointer}
:focus-visible{outline:2px solid var(--blue);outline-offset:3px}
::selection{background:var(--blue);color:#fff}
.wrap{max-width:1400px;margin:0 auto;padding:0 20px}
@media(min-width:768px){.wrap{padding:0 32px}}
.dots{background-image:radial-gradient(rgba(18,18,18,.12) 1px,transparent 1.3px);background-size:22px 22px}
.eyebrow{font-family:var(--mono);font-size:11px;font-weight:500;letter-spacing:.14em;text-transform:uppercase;color:var(--muted)}
.eyebrow b{font-weight:500;color:var(--blue)}
h1,h2,h3{font-family:var(--head);font-weight:400}
.h2{font-size:clamp(2.4rem,5vw,4.25rem);line-height:1;letter-spacing:-.035em;margin-top:20px}
.lead{font-size:17px;line-height:1.65;color:rgba(18,18,18,.7)}
.i{width:16px;height:16px;fill:none;stroke:currentColor;stroke-width:2;stroke-linecap:round;stroke-linejoin:round;flex:none}
.btn{display:inline-flex;align-items:center;gap:8px;height:44px;padding:0 22px;border-radius:6px;background:var(--ink);color:#fff;font-size:15px;font-weight:500;transition:background .25s,box-shadow .25s;box-shadow:0 10px 30px -12px rgba(18,18,18,.6)}
.btn:hover{background:var(--blue);box-shadow:0 14px 34px -12px rgba(67,83,255,.75)}
.btn .i{transition:transform .25s var(--ease)}
.btn:hover .i{transform:translate(2px,-2px)}
.link{display:inline-flex;align-items:center;gap:8px;font-size:15px;font-weight:500;color:rgba(18,18,18,.8);text-underline-offset:4px;transition:color .2s}
.link:hover{color:var(--blue);text-decoration:underline}
.circ{width:44px;height:44px;border-radius:50%;border:1px solid var(--rule);display:inline-flex;align-items:center;justify-content:center;transition:border-color .2s,background .2s}
.circ:hover{border-color:var(--ink);background:#fff}

/* draw system */
.st{fill:none;stroke:currentColor;stroke-linecap:round;stroke-linejoin:round;stroke-dasharray:1 2;stroke-dashoffset:1}
.on .st,.st.on{stroke-dashoffset:0;transition:stroke-dashoffset var(--dur,800ms) var(--draw) calc(var(--bd,0ms) + var(--d,0ms))}
.static .st{stroke-dasharray:none;stroke-dashoffset:0;transition:none}
.so{stroke-width:calc(1.5px*var(--sw,1))}
.sl{stroke-width:calc(1.05px*var(--sw,1))}
.sw{stroke-width:calc(.75px*var(--sw,1))}
.sd{stroke-width:calc(.7px*var(--sw,1));opacity:.85}
.ss{stroke-width:calc(.55px*var(--sw,1));opacity:.7}
.sh{stroke-width:calc(.5px*var(--sw,1));opacity:.5}
.sg{stroke:var(--blue);stroke-width:calc(.65px*var(--sw,1));opacity:.75}
.sT{stroke-width:calc(.8px*var(--sw,1))}
.sx{fill:none;stroke:var(--blue);stroke-width:calc(.6px*var(--sw,1));stroke-dasharray:calc(5px*var(--sw,1)) calc(4px*var(--sw,1));opacity:0;transition:opacity .6s}
.dfill{fill:var(--paper)}
.dhatch{opacity:0;transition:opacity .5s}
.lbl{font-family:var(--mono);fill:currentColor;letter-spacing:.08em}

/* header */
.hdr{position:fixed;inset:0 0 auto;z-index:60;border-bottom:1px solid transparent;transition:background .35s,border-color .35s,backdrop-filter .35s}
.hdr.solid{background:rgba(245,245,241,.8);-webkit-backdrop-filter:blur(14px) saturate(1.4);backdrop-filter:blur(14px) saturate(1.4);border-color:var(--rule)}
.hdr-in{height:64px;display:flex;align-items:center;justify-content:space-between}
@media(min-width:768px){.hdr-in{height:72px}}
.logo{display:flex;align-items:center;gap:12px}
.logo svg{width:32px;height:32px;transition:color .3s}
.logo:hover svg{color:var(--blue)}
.logo b{display:block;font-family:var(--head);font-weight:500;font-size:17px;letter-spacing:-.01em;line-height:1}
.logo small{display:block;margin-top:4px;font-family:var(--mono);font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--muted);line-height:1}
.nav{display:none;gap:4px}
.nav a{padding:8px 16px;border-radius:999px;font-size:15px;color:rgba(18,18,18,.8);transition:color .2s,background .2s}
.nav a:hover{color:var(--blue)}
.nav a.cur{background:rgba(18,18,18,.05);color:var(--ink)}
.hdr .btn{display:none;height:40px;padding:0 12px 0 16px;font-size:14px;box-shadow:none}
.burger{width:44px;height:44px;display:inline-flex;align-items:center;justify-content:center;border-radius:6px}
.burger span{position:relative;width:20px;height:1.5px;background:var(--ink);transition:background .2s}
.burger span::before,.burger span::after{content:"";position:absolute;left:0;width:20px;height:1.5px;background:var(--ink);transition:transform .3s var(--ease)}
.burger span::before{top:-6px}.burger span::after{top:6px}
.menu-open .burger span{background:transparent}
.menu-open .burger span::before{transform:translateY(6px) rotate(45deg)}
.menu-open .burger span::after{transform:translateY(-6px) rotate(-45deg)}
@media(min-width:768px){.nav{display:flex}.hdr .btn{display:inline-flex}.burger{display:none}}
.mnav{position:fixed;inset:64px 0 0;z-index:55;background:var(--paper);padding:24px;display:flex;flex-direction:column;visibility:hidden;opacity:0;transition:opacity .3s,visibility .3s}
.menu-open .mnav{visibility:visible;opacity:1}
.mnav a.ml{display:flex;align-items:baseline;gap:16px;padding:20px 0;border-bottom:1px solid var(--rule);font-family:var(--head);font-size:36px;letter-spacing:-.02em;transform:translateY(12px);opacity:0;transition:transform .5s var(--ease),opacity .5s}
.menu-open .mnav a.ml{transform:none;opacity:1}
.mnav a.ml span{font-family:var(--mono);font-size:12px;color:var(--muted)}
.mnav .btn{margin-top:auto;justify-content:center;height:48px}

/* hero */
.hero{position:relative;overflow:hidden;padding-top:112px}
.hero-copy{position:relative;z-index:3;text-align:center;padding:0 20px}
.hero-copy>div{max-width:700px;margin:0 auto}
.hero h1{font-size:clamp(2.8rem,9vw,4.75rem);line-height:.96;letter-spacing:-.035em;animation:up 1s var(--ease) both}
.hero h1 span{color:var(--muted)}
.hero p.lead{max-width:500px;margin:24px auto 0;animation:up 1s var(--ease) .2s both}
.hero .ctas{margin-top:36px;display:flex;flex-wrap:wrap;gap:12px 24px;align-items:center;justify-content:center;animation:fade 1s .35s both}
.hint{margin-top:32px;font-family:var(--mono);font-size:10px;letter-spacing:.18em;text-transform:uppercase;color:var(--muted);animation:fade 1s .9s both}
.hint .t{display:none}
@media(pointer:coarse){.hint .m{display:none}.hint .t{display:inline}}
.hero-art{position:relative;margin-top:40px}
.hero-art svg{display:block;width:165%;margin-left:-8%;height:auto;touch-action:pan-y}
@media(min-width:640px){.hero-art svg{width:132%}}
@media(min-width:768px){.hero{padding-top:144px}.hero-art{margin-top:48px}.hero-art svg{width:118%;margin-left:-6%}}
@media(min-width:1024px){.hero-art svg{width:112%}}
@media(min-width:1280px){
  .hero{padding-top:64px}
  .hero-copy{position:absolute;left:38%;right:3%;top:clamp(7.5rem,9.5vw,10rem);padding:0;pointer-events:none}
  .hero-copy>div{pointer-events:auto}
  .hero h1{font-size:clamp(4.25rem,5.6vw,5.75rem)}
  .hero-art{margin-top:0;padding-top:56px}
  .hero-art svg{width:110%;margin-left:-7%}
}
.hero-art .ink{color:#1c1c1a}
#scan{opacity:0}
.hero-art.go #scan{animation:scan 2.4s var(--draw) .2s both}
@keyframes scan{0%{opacity:0;transform:translateY(0)}8%{opacity:1}90%{opacity:1}100%{opacity:0;transform:translateY(760px)}}
#lensFrame{opacity:0;transition:opacity .7s 2.2s}
.hero-art.go #lensFrame{opacity:1}
@keyframes up{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:none}}
@keyframes fade{from{opacity:0}to{opacity:1}}

/* services */
.services{position:relative;z-index:5;margin-top:-40px;padding:0 16px}
@media(min-width:768px){.services{margin-top:-9vw;padding:0 24px 0 14%}}
@media(min-width:1024px){.services{padding-left:17%}}
.card{position:relative;overflow:hidden;border:1px solid var(--rule);background:#fff;box-shadow:0 1px 0 rgba(0,0,0,.02),0 40px 80px -50px rgba(18,18,18,.35)}
.card>svg.x{position:absolute;inset:0;width:100%;height:100%;color:var(--rule);pointer-events:none}
.svc-top{position:relative;display:grid}
.svc-top>div{padding:48px 24px 40px;border-bottom:1px solid var(--rule)}
.svc-top>div:last-child{display:flex;align-items:flex-end;padding-top:32px}
.svc-top h2{margin-top:20px;max-width:12ch;font-size:clamp(2.2rem,4.4vw,3.6rem);line-height:1.02;letter-spacing:-.03em}
@media(min-width:768px){.svc-top{grid-template-columns:1fr 1fr}.svc-top>div{padding:80px 48px 56px}.svc-top>div:first-child{border-right:1px solid var(--rule)}.svc-top>div:last-child{padding-top:32px}}
@media(min-width:1024px){.svc-top>div{padding-left:64px;padding-right:64px}}
.svc-grid{position:relative;display:grid;gap:12px;padding:12px}
@media(min-width:768px){.svc-grid{grid-template-columns:repeat(3,1fr);gap:16px;padding:24px}}
@media(min-width:1024px){.svc-grid{padding:32px}}
.svc{display:flex;flex-direction:column;min-height:250px;height:100%;padding:24px;border:1px solid var(--rule);border-radius:4px;background:#f3f3f0;transition:background .3s,border-color .3s,transform .4s var(--ease)}
.svc:hover{background:#fff;border-color:rgba(67,83,255,.4);transform:translateY(-3px)}
@media(min-width:768px){.svc{min-height:290px}}
.svc h3{font-family:var(--mono);font-size:13px;color:rgba(18,18,18,.7)}
.svc h3 span{transition:color .3s}
.svc:hover h3 span{color:var(--blue)}
.svc svg{margin:auto 0 auto auto;width:84px;height:84px;color:rgba(18,18,18,.55);transition:color .3s}
.svc:hover svg{color:var(--blue)}
.svc svg path{fill:none;stroke:currentColor;stroke-width:1.2;stroke-linecap:round;stroke-linejoin:round;stroke-dasharray:1 2;stroke-dashoffset:1;transition:stroke-dashoffset 1s var(--draw) calc(var(--rd,0ms) + var(--d,0ms) + 200ms)}
.in .svc svg path,.svc.in svg path{stroke-dashoffset:0}
.svc p{margin-top:16px;font-size:15px;line-height:1.6;color:rgba(18,18,18,.7)}
[data-reveal]{opacity:0;transform:translateY(18px);transition:opacity .9s var(--ease) var(--rd,0ms),transform .9s var(--ease) var(--rd,0ms)}
[data-reveal].in{opacity:1;transform:none}

/* work */
.work{padding:112px 0 96px;scroll-margin-top:80px}
@media(min-width:768px){.work{padding:144px 0 128px}}
.work-head{display:grid;gap:32px}
@media(min-width:1024px){.work-head{grid-template-columns:1fr auto;align-items:end}}
.work-head .lead{margin-top:20px;max-width:520px}
.filters{display:flex;flex-wrap:wrap;gap:8px}
.chip{display:inline-flex;align-items:center;gap:8px;height:40px;padding:0 16px;border-radius:999px;border:1px solid var(--rule);background:#fff;font-size:14px;color:rgba(18,18,18,.8);transition:all .25s}
.chip:hover{border-color:rgba(18,18,18,.4)}
.chip span{font-family:var(--mono);font-size:11px;color:var(--muted)}
.chip[aria-pressed=true]{background:var(--ink);border-color:var(--ink);color:#fff}
.chip[aria-pressed=true] span{color:rgba(255,255,255,.6)}
.sky-wrap{position:relative;margin-top:40px}
@media(min-width:768px){.sky-wrap{margin-top:56px}}
.swipe{display:flex;align-items:center;gap:8px;margin-bottom:12px;padding:0 20px}
@media(min-width:768px){.swipe{display:none}}
.sky-scroll{overflow-x:auto;overscroll-behavior-x:contain;scrollbar-width:none}
.sky-scroll::-webkit-scrollbar{display:none}
.sky-in{position:relative;min-width:1080px;max-width:1800px;margin:0 auto;padding:0 20px}
@media(min-width:768px){.sky-in{padding:0 32px}}
.sky-svg{position:relative}
.sky-svg svg{display:block;width:100%;height:auto;--sw:2.3;color:var(--ink);overflow:visible}
.bg{cursor:pointer;transition:opacity .5s}
.bg .lift{transition:transform .55s var(--ease)}
.bg.active{color:var(--blue)}
.bg.active .lift{transform:translateY(-12px)}
.bg.active .dhatch,.bg.active .sx{opacity:1}
.bg.muted{opacity:.14;pointer-events:none}
.bubble{position:absolute;z-index:3;transform:translate(-50%,-100%);pointer-events:none;transition:left .55s var(--ease),top .55s var(--ease)}
.bubble div{display:flex;align-items:center;gap:8px;white-space:nowrap;border-radius:999px;background:var(--blue);color:#fff;padding:6px 10px 6px 12px;font-size:13px;font-weight:500;box-shadow:0 10px 26px -10px rgba(67,83,255,.85)}
.bubble div em{font-style:normal;font-family:var(--mono);font-size:11px;color:rgba(255,255,255,.7)}
.bubble i{display:block;margin:0 auto;width:1px;height:12px;background:var(--blue)}
.ticks{position:relative;height:48px;list-style:none}
.ticks li{position:absolute;top:4px;transform:translateX(-50%)}
.ticks a{display:flex;flex-direction:column;align-items:center;gap:4px;padding:4px 8px;font-family:var(--mono);font-size:11px;color:var(--muted);transition:color .3s,opacity .3s}
.ticks a::before{content:"";width:1px;height:8px;background:rgba(18,18,18,.3)}
.ticks a:hover{color:var(--ink)}
.ticks a.cur{color:var(--blue)}
.ticks a.cur::before{background:var(--blue)}
.ticks a.muted{opacity:.25}
.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);white-space:nowrap}

.panel{display:grid;margin-top:24px;overflow:hidden;border:1px solid var(--rule);background:#fff}
@media(min-width:768px){.panel{grid-template-columns:1.1fr 1fr}}
.pv{position:relative;display:block;aspect-ratio:16/11;overflow:hidden;border-bottom:1px solid var(--rule);background:var(--paper);cursor:pointer}
@media(min-width:768px){.pv{aspect-ratio:auto;min-height:460px;border-bottom:0;border-right:1px solid var(--rule)}}
.pv svg{position:absolute;inset:0;width:100%;height:100%}
.pv .sk svg{--sw:1;color:var(--ink)}
.pv .ph{position:absolute;inset:0;clip-path:circle(0% at var(--mx,50%) var(--my,50%));transition:clip-path .9s var(--ease)}
.pv.rev .ph{clip-path:circle(150% at var(--mx,50%) var(--my,50%))}
.pv .corner{position:absolute;z-index:2;width:20px;height:20px;border-color:rgba(67,83,255,.6);border-style:solid;border-width:0;pointer-events:none}
.pv .c1{left:16px;top:16px;border-left-width:1px;border-top-width:1px}
.pv .c2{right:16px;top:16px;border-right-width:1px;border-top-width:1px}
.pv .c3{right:16px;bottom:16px;border-right-width:1px;border-bottom-width:1px}
.ptag{position:absolute;z-index:2;left:12px;bottom:12px;display:grid;border-radius:999px;border:1px solid rgba(18,18,18,.1);background:rgba(255,255,255,.9);backdrop-filter:blur(6px);padding:4px 10px;font-family:var(--mono);font-size:10px;letter-spacing:.14em;text-transform:uppercase}
.ptag span{grid-area:1/1;transition:opacity .5s}
.ptag span+span{color:var(--blue);opacity:0}
.pv.rev .ptag span:first-child{opacity:0}
.pv.rev .ptag span+span{opacity:1}
.pinfo{display:flex;flex-direction:column;padding:24px}
@media(min-width:768px){.pinfo{padding:40px}}
@media(min-width:1024px){.pinfo{padding:48px}}
.pinfo.swap>*{animation:slideIn .55s var(--ease) both}
.pinfo.swap>*:nth-child(2){animation-delay:.04s}.pinfo.swap>*:nth-child(3){animation-delay:.08s}.pinfo.swap>*:nth-child(4){animation-delay:.12s}.pinfo.swap>*:nth-child(5){animation-delay:.16s}
@keyframes slideIn{from{opacity:0;transform:translateX(10px)}to{opacity:1;transform:none}}
.prow{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:12px}
.mono{font-family:var(--mono);font-size:12px;color:var(--muted)}
.badge{border-radius:999px;border:1px solid rgba(67,83,255,.3);background:var(--blue-soft);color:var(--blue);padding:4px 12px;font-size:12px;font-weight:500}
.pinfo h3{margin-top:24px;font-size:clamp(2rem,3.4vw,2.9rem);line-height:1.02;letter-spacing:-.03em}
.pinfo .meta{margin-top:12px;font-size:15px;color:rgba(18,18,18,.6)}
.pinfo .sum{margin-top:24px;font-size:17px;line-height:1.65;color:rgba(18,18,18,.75)}
.pinfo dl{display:grid;grid-template-columns:1fr 1fr;gap:16px 24px;margin-top:32px;padding-top:24px;border-top:1px solid var(--rule);font-size:14px}
dt{font-family:var(--mono);font-size:11px;letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
dd{margin-top:4px}
.pact{margin-top:auto;padding-top:40px;display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:16px}
.pact .btn{height:48px;box-shadow:none}
.pact>div{display:flex;gap:8px}

/* process */
.process{position:relative;border-top:1px solid var(--rule);border-bottom:1px solid var(--rule);background:#fff;scroll-margin-top:64px}
.process .head{padding-top:96px}
@media(min-width:768px){.process .head{padding-top:128px}}
.process h2{max-width:16ch}
.pgrid{display:grid;column-gap:64px;padding-bottom:64px}
@media(min-width:1024px){.pgrid{grid-template-columns:1.15fr 1fr;padding-bottom:96px}}
.pstick{position:sticky;top:64px;z-index:5;margin:0 -20px;padding:24px 20px 16px;background:#fff;border-bottom:1px solid var(--rule)}
@media(min-width:768px){.pstick{top:72px}}
@media(min-width:1024px){.pstick{top:112px;margin:0;padding:40px 0 0;height:calc(100svh - 9rem);border-bottom:0}}
.pbox{display:flex;flex-direction:column;height:100%;overflow:hidden;border:1px solid var(--rule)}
.pbar{display:flex;align-items:center;justify-content:space-between;gap:16px;padding:12px 16px;border-bottom:1px solid var(--rule);background:rgba(255,255,255,.75);backdrop-filter:blur(6px)}
.pbar p{font-family:var(--mono);font-size:11px;letter-spacing:.14em;text-transform:uppercase;color:var(--muted)}
.pbar p:last-child{color:var(--ink);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.pdraw{position:relative;flex:1;min-height:0;padding:16px 12px}
@media(min-width:768px){.pdraw{padding:24px}}
.pdraw svg{display:block;width:100%;height:30svh;--sw:1.5;color:#55554f}
@media(min-width:640px){.pdraw svg{height:36svh}}
@media(min-width:1024px){.pdraw svg{height:100%}}
.pdraw .st{transition:stroke-dashoffset .35s ease,stroke .8s}
.pdraw .st.on{transition:stroke-dashoffset var(--dur,900ms) var(--draw) var(--d,0ms),stroke .8s 1.2s}
.pdraw .st.cur{stroke:var(--blue)}
.pdraw .sx{transition:opacity .6s}
.pdraw .sx.on{opacity:.8}
.pdraw .lbl{opacity:0;transition:opacity .5s}
.pdraw .lbl.on{opacity:1;transition:opacity .6s var(--d,0ms)}
.pdraw .fade{opacity:0;transition:opacity .9s}
.pdraw .fade.on{opacity:1}
.psteps{display:grid;grid-template-columns:repeat(5,1fr);gap:6px;padding:12px;border-top:1px solid var(--rule);background:rgba(255,255,255,.75)}
.psteps button{display:flex;flex-direction:column;gap:8px;padding:4px 0;text-align:left}
.psteps i{display:block;height:3px;border-radius:9px;background:var(--rule);transition:background .5s}
.psteps button:hover i{background:rgba(18,18,18,.3)}
.psteps button.done i{background:rgba(67,83,255,.35)}
.psteps button.cur i{background:var(--blue)}
.psteps span{display:none;font-family:var(--mono);font-size:10px;letter-spacing:.1em;color:var(--muted)}
.psteps button.cur span{color:var(--ink)}
@media(min-width:640px){.psteps span{display:block}}
.slist{list-style:none}
.slist li{display:flex;align-items:center;min-height:62svh;padding:48px 0}
@media(min-width:1024px){.slist li{min-height:78svh}}
.slist li>div{opacity:.3;transition:opacity .5s}
.slist li.cur>div{opacity:1}
.slist .n{font-family:var(--mono);font-size:14px;color:var(--blue)}
.slist h3{margin-top:12px;font-size:30px;letter-spacing:-.02em}
@media(min-width:768px){.slist h3{font-size:40px;line-height:1.05}}
.slist p.lead{margin-top:20px;max-width:460px}
.pill{margin-top:24px;display:inline-flex;align-items:center;gap:8px;border-radius:999px;border:1px solid var(--rule);padding:4px 12px;font-family:var(--mono);font-size:11px;letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
.pill::before{content:"";width:6px;height:6px;border-radius:50%;background:var(--blue)}

/* studio */
.studio{padding:96px 0;scroll-margin-top:64px}
@media(min-width:768px){.studio{padding:128px 0}}
.sgrid{display:grid;gap:48px}
@media(min-width:1024px){.sgrid{grid-template-columns:.85fr 1.15fr;gap:80px}.sgrid figure{position:sticky;top:112px}}
.fig{position:relative;aspect-ratio:4/5;overflow:hidden;border:1px solid var(--rule);background:#e6e6e1}
.fig svg{display:block;width:100%;height:100%}
.fig .tag{position:absolute;left:16px;top:16px;font-family:var(--mono);font-size:10px;letter-spacing:.16em;text-transform:uppercase;color:#fff;mix-blend-mode:difference}
figcaption{margin-top:12px;display:flex;justify-content:space-between;font-family:var(--mono);font-size:11px;letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
#walker{animation:walk 14s linear infinite}
@keyframes walk{0%{transform:translateX(-140px)}100%{transform:translateX(560px)}}
.studio h2{margin-top:20px;font-size:clamp(2.2rem,4.4vw,3.75rem);line-height:1.03;letter-spacing:-.03em}
.cols{margin-top:32px;display:grid;gap:20px;font-size:17px;line-height:1.65;color:rgba(18,18,18,.75)}
@media(min-width:768px){.cols{grid-template-columns:1fr 1fr;gap:32px}}
.princ{margin-top:48px;list-style:none;border-top:1px solid var(--rule)}
.princ li{display:grid;gap:8px;padding:24px 0;border-bottom:1px solid var(--rule)}
@media(min-width:768px){.princ li{grid-template-columns:56px 1fr 1.3fr;gap:24px;align-items:baseline}}
.princ span{font-family:var(--mono);font-size:14px;color:var(--muted);transition:color .3s}
.princ li:hover span{color:var(--blue)}
.princ h3{font-size:20px;letter-spacing:-.01em}
@media(min-width:768px){.princ h3{font-size:24px}}
.princ p{font-size:15px;line-height:1.6;color:rgba(18,18,18,.7)}
.stats{margin-top:48px;display:grid;grid-template-columns:1fr 1fr;gap:1px;overflow:hidden;border:1px solid var(--rule);background:var(--rule)}
@media(min-width:768px){.stats{grid-template-columns:repeat(4,1fr)}}
.stats div{background:#fff;padding:20px}
@media(min-width:768px){.stats div{padding:24px}}
.stats dd{margin-top:12px;font-family:var(--head);font-size:48px;letter-spacing:-.04em;font-variant-numeric:tabular-nums;line-height:1}
@media(min-width:768px){.stats dd{font-size:56px}}

/* quotes */
.quotes{border-top:1px solid var(--rule);background:#fff;padding:96px 0;overflow:hidden}
@media(min-width:768px){.quotes{padding:128px 0}}
.quotes .wrap{max-width:1100px}
.qtop{display:flex;justify-content:space-between;gap:24px}
.qfig{margin-top:40px;min-height:300px}
@media(min-width:768px){.qfig{min-height:280px}}
.qfig.swap{animation:up .7s var(--ease) both}
.qfig blockquote{font-family:var(--head);font-size:clamp(1.75rem,3.6vw,3rem);line-height:1.12;letter-spacing:-.025em}
.qfig blockquote span{color:var(--blue)}
.qfig figcaption{margin-top:32px;justify-content:flex-start;align-items:center;gap:16px;font-family:var(--sans);font-size:16px;letter-spacing:0;text-transform:none;color:var(--ink)}
.qfig figcaption::before{content:"";width:40px;height:1px;background:rgba(18,18,18,.3)}
.qfig figcaption small{display:block;font-size:14px;color:rgba(18,18,18,.6)}
.qnav{margin-top:40px;display:flex;justify-content:space-between;align-items:center;gap:24px}
.qdots{display:flex;gap:8px}
.qdots button{height:44px;display:flex;align-items:center}
.qdots i{display:block;height:3px;width:20px;border-radius:9px;background:var(--rule);transition:all .5s}
.qdots button[aria-pressed=true] i{width:40px;background:var(--blue)}
.qnav>div:last-child{display:flex;gap:8px}

/* footer */
footer{position:relative;overflow:hidden;background:var(--ink);color:#fff;scroll-margin-top:64px}
.fgrid{display:grid;gap:48px;padding-top:80px}
@media(min-width:768px){.fgrid{padding-top:112px}}
@media(min-width:1024px){.fgrid{grid-template-columns:1.4fr 1fr;gap:80px}}
footer .eyebrow{color:rgba(255,255,255,.5)}
footer h2{margin-top:20px;max-width:42rem;font-size:36px;line-height:1.02;letter-spacing:-.03em}
@media(min-width:768px){footer h2{font-size:60px}}
.btn-w{margin-top:36px;height:48px;background:#fff;color:var(--ink);box-shadow:none}
.btn-w:hover{color:#fff}
.fcols{display:grid;grid-template-columns:1fr 1fr;gap:32px;font-size:15px}
.fcols address{margin-top:16px;font-style:normal;line-height:1.65;color:rgba(255,255,255,.8)}
.fcols p.h{margin-top:12px;color:rgba(255,255,255,.6);line-height:1.6}
.fcols ul{margin-top:16px;list-style:none;display:grid;gap:10px}
.fcols ul a{color:rgba(255,255,255,.8);transition:color .2s}
.fcols ul a:hover{color:#fff}
.city{margin-top:48px}
@media(min-width:768px){.city{margin-top:64px}}
.city svg{display:block;width:100%;height:auto;color:#fff;opacity:.62;--sw:1.6}
.fbot{border-top:1px solid rgba(255,255,255,.1)}
.fbot .wrap{display:flex;flex-direction:column;gap:16px;padding-top:24px;padding-bottom:24px;font-size:14px;color:rgba(255,255,255,.5)}
@media(min-width:768px){.fbot .wrap{flex-direction:row;align-items:center;justify-content:space-between}}
.fbot .wrap>div{display:flex;align-items:center;gap:12px}
.fbot a{display:inline-flex;align-items:center;gap:8px;color:rgba(255,255,255,.6);transition:color .2s}
.fbot a:hover{color:#fff}

/* dialogs */
dialog{margin:auto;border:0;padding:0;background:transparent;max-width:min(1180px,calc(100vw - 24px));width:100%;max-height:calc(100dvh - 24px);color:var(--ink)}
dialog::backdrop{background:rgba(18,18,18,.55);backdrop-filter:blur(6px)}
dialog[open]{animation:dlg .5s var(--ease)}
@keyframes dlg{from{opacity:0;transform:translateY(24px) scale(.98)}to{opacity:1;transform:none}}
.dbox{position:relative;display:grid;background:#fff;border:1px solid var(--rule);max-height:calc(100dvh - 24px);overflow:auto}
@media(min-width:900px){.dbox{grid-template-columns:1.15fr 1fr;overflow:hidden}}
.dart{position:relative;min-height:320px;background:var(--paper);border-bottom:1px solid var(--rule)}
@media(min-width:900px){.dart{min-height:620px;border-bottom:0;border-right:1px solid var(--rule)}}
.dart svg{position:absolute;inset:0;width:100%;height:100%}
.dart .ph{position:absolute;inset:0;clip-path:inset(0 0 0 50%)}
.dart .split{position:absolute;top:0;bottom:0;left:50%;width:1px;background:#fff;box-shadow:0 0 0 1px rgba(67,83,255,.4)}
.dart .split b{position:absolute;top:50%;left:50%;width:36px;height:36px;margin:-18px;border-radius:50%;background:#fff;border:1px solid var(--rule);display:flex;align-items:center;justify-content:center;font-family:var(--mono);font-size:10px;color:var(--blue);box-shadow:0 6px 18px -6px rgba(0,0,0,.3)}
.dart input{position:absolute;inset:0;width:100%;height:100%;opacity:0;cursor:ew-resize}
.dtxt{padding:28px;overflow:auto}
@media(min-width:900px){.dtxt{padding:48px;max-height:calc(100dvh - 24px)}}
.dtxt h3{margin-top:20px;font-size:clamp(2rem,3.4vw,2.8rem);line-height:1.02;letter-spacing:-.03em}
.dtxt .desc p{margin-top:16px;font-size:16px;line-height:1.7;color:rgba(18,18,18,.75)}
.dtxt dl{display:grid;grid-template-columns:1fr 1fr;gap:16px 24px;margin-top:28px;padding-top:24px;border-top:1px solid var(--rule);font-size:14px}
.xbtn{position:absolute;right:12px;top:12px;z-index:3;width:40px;height:40px;border-radius:50%;background:#fff;border:1px solid var(--rule);display:flex;align-items:center;justify-content:center}
.xbtn:hover{border-color:var(--ink)}
.form{display:grid;gap:14px;margin-top:28px}
.form label{display:grid;gap:6px;font-family:var(--mono);font-size:11px;letter-spacing:.12em;text-transform:uppercase;color:var(--muted)}
.form input,.form textarea,.form select{font:inherit;font-family:var(--sans);font-size:16px;letter-spacing:0;text-transform:none;color:var(--ink);background:var(--paper);border:1px solid var(--rule);border-radius:6px;padding:12px 14px;transition:border-color .2s,background .2s}
.form input:focus,.form textarea:focus,.form select:focus{outline:none;border-color:var(--blue);background:#fff}
.form textarea{min-height:120px;resize:vertical}
.form .btn{justify-self:start;margin-top:6px;box-shadow:none}
.sent{display:none;margin-top:28px;padding:20px;border:1px solid rgba(67,83,255,.3);background:var(--blue-soft);color:var(--blue);border-radius:6px}
.form.done{display:none}.form.done+.sent{display:block}

@media(prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.01ms!important;animation-iteration-count:1!important;transition-duration:.01ms!important;transition-delay:0ms!important;scroll-behavior:auto!important}
  .st{stroke-dasharray:none!important;stroke-dashoffset:0!important}
  [data-reveal]{opacity:1;transform:none}
}
</style>
</head>
<body>
<header class="hdr" id="hdr" data-section="nav">
  <div class="wrap hdr-in">
    <a href="#top" class="logo" aria-label="Linework, home">
      <svg viewBox="0 0 32 32" aria-hidden="true"><g fill="none" stroke="currentColor"><rect x="3.5" y="3.5" width="25" height="25" stroke-width="1.4"/><path d="M10 28.5V16.5a6 6 0 0 1 12 0v12" stroke-width="1.4"/><path d="M3.5 10.5h25M16 3.5v7" stroke-width=".9"/></g></svg>
      <span><b>Linework</b><small>AI Architect Assistant</small></span>
    </a>
    <nav class="nav" aria-label="Main">
      <a href="#work">Projects</a><a href="#process">How it works</a><a href="#studio">Why Linework</a><a href="#contact">Contact</a>
    </nav>
    <div style="display:flex;gap:8px;align-items:center">
      <button class="btn" data-enquire>Get early access <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
      <button class="burger" id="burger" aria-expanded="false" aria-controls="mnav"><span></span><b class="sr">Open menu</b></button>
    </div>
  </div>
</header>
<nav class="mnav dots" id="mnav" aria-label="Mobile" data-section="mobile-nav">
  <a class="ml" href="#work" style="transition-delay:.05s"><span>01</span>Projects</a>
  <a class="ml" href="#process" style="transition-delay:.1s"><span>02</span>How it works</a>
  <a class="ml" href="#studio" style="transition-delay:.15s"><span>03</span>Why Linework</a>
  <a class="ml" href="#contact" style="transition-delay:.2s"><span>04</span>Contact</a>
  <button class="btn" data-enquire>Get early access <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
</nav>

<main id="top">
<section class="hero dots" aria-labelledby="hero-title" data-section="hero">
  <div class="hero-copy"><div>
    <h1 id="hero-title"><span>Design</span> places<br>that last.</h1>
    <p class="lead">Linework is an AI architect assistant. It reads the site, sketches massing options and drafts drawings line by line, so you can spend your time on the decisions only an architect can make.</p>
    <div class="ctas">
      <button class="btn" data-enquire>Get early access <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
      <a class="link" href="#work">See what it drew <svg class="i" viewBox="0 0 24 24"><path d="M12 5v14M19 12l-7 7-7-7"/></svg></a>
    </div>
    <p class="hint"><span class="m">( Move across the drawing to see the blueprint )</span><span class="t">( Tap the drawing to move the blueprint )</span></p>
  </div></div>
  <div class="hero-art" id="heroArt"></div>
</section>

<section class="services" aria-labelledby="svc-title" data-section="services">
  <div class="card">
    <svg class="x" viewBox="0 0 100 100" preserveAspectRatio="none" aria-hidden="true"><line x1="0" y1="0" x2="100" y2="100" stroke="currentColor" vector-effect="non-scaling-stroke"/><line x1="100" y1="0" x2="50" y2="100" stroke="currentColor" vector-effect="non-scaling-stroke"/></svg>
    <div class="svc-top">
      <div><p class="eyebrow">( What it does )</p><h2 id="svc-title">An assistant that knows the ground</h2></div>
      <div><p class="lead" style="max-width:440px">From a bathing house for winter swimmers to a library for forty thousand neighbours, Linework starts every project with the site, the light and the people who will use it, then works beside you from the first sketch to the final handover.</p></div>
    </div>
    <div class="svc-grid">
      <div data-reveal style="--rd:0ms"><article class="svc"><h3><span>01</span> / Site and concept</h3>
        <svg viewBox="0 0 64 64" aria-hidden="true"><path pathLength="1" d="M6 56H58"/><path pathLength="1" style="--d:90ms" d="M14 56V24H50V56"/><path pathLength="1" style="--d:180ms" d="M10 24H54"/><path pathLength="1" style="--d:270ms" d="M14 24L32 11L50 24"/><path pathLength="1" style="--d:360ms" d="M20 56V45a5 5 0 0 1 10 0V56"/><path pathLength="1" style="--d:450ms" d="M34 56V45a5 5 0 0 1 10 0V56"/><path pathLength="1" style="--d:540ms" d="M20 33H28M36 33H44"/></svg>
        <p>Upload a plot and get sun paths, wind, setbacks and neighbour heights mapped, then compare massing options against the brief.</p></article></div>
      <div data-reveal style="--rd:120ms"><article class="svc"><h3><span>02</span> / Drawings and detail</h3>
        <svg viewBox="0 0 64 64" aria-hidden="true"><path pathLength="1" d="M6 56H58"/><path pathLength="1" style="--d:90ms" d="M16 56V30M16 44H32V56M16 30H22"/><path pathLength="1" style="--d:180ms" d="M44 6V20"/><path pathLength="1" style="--d:270ms" d="M37 27a7 7 0 0 1 14 0Z"/><path pathLength="1" style="--d:360ms" d="M38 36H54V52H38ZM46 36V52"/></svg>
        <p>Plans, sections and elevations drafted from your sketches and kept in step with every change, down to joints at 1:5.</p></article></div>
      <div data-reveal style="--rd:240ms"><article class="svc"><h3><span>03</span> / Masterplanning</h3>
        <svg viewBox="0 0 64 64" aria-hidden="true"><path pathLength="1" d="M8 8H56V56H8Z"/><path pathLength="1" style="--d:90ms" d="M14 14H27V25H14Z"/><path pathLength="1" style="--d:180ms" d="M36 14H50V27H36Z"/><path pathLength="1" style="--d:270ms" d="M14 37H25V50H14Z"/><path pathLength="1" style="--d:360ms" d="M35 36H50V50H35Z"/><path pathLength="1" style="--d:450ms" d="M8 56L56 8"/></svg>
        <p>Test streets, courtyards and whole neighbourhoods around the walk between them, with daylight and density checked as you draw.</p></article></div>
    </div>
  </div>
</section>

<section class="work" id="work" aria-labelledby="work-title" data-section="projects">
  <div class="wrap work-head">
    <div>
      <p class="eyebrow">( Drawn with Linework )</p>
      <h2 class="h2" id="work-title">The skyline so far</h2>
      <p class="lead">Every outline is a building that architects designed with Linework at their side. Hover one to read its story, click to walk inside, or filter the skyline by type and watch it rebuild.</p>
    </div>
    <div class="filters" role="group" aria-label="Filter projects by type" id="filters"></div>
  </div>
  <div class="sky-wrap">
    <p class="swipe eyebrow"><svg class="i" viewBox="0 0 24 24"><path d="m18 8 4 4-4 4M2 12h20M6 8l-4 4 4 4"/></svg>Swipe along the skyline, tap a building</p>
    <div class="sky-scroll"><div class="sky-in">
      <div class="sky-svg" id="sky"></div>
      <ol class="ticks" id="ticks" aria-label="Projects on the skyline"></ol>
    </div></div>
  </div>
  <div class="wrap">
    <div class="panel" role="region" aria-label="Selected project">
      <div class="pv" id="pv" role="button" tabindex="0" aria-label="Open project">
        <div class="sk dots"></div><div class="ph"></div>
        <span class="corner c1"></span><span class="corner c2"></span><span class="corner c3"></span>
        <span class="ptag" aria-hidden="true"><span>Drawing</span><span>Rendering</span></span>
      </div>
      <div class="pinfo" id="pinfo"></div>
    </div>
  </div>
</section>

<section class="process" id="process" aria-labelledby="process-title" data-section="process">
  <div class="wrap head">
    <p class="eyebrow">( How it works )</p>
    <h2 class="h2" id="process-title">From the first walk to the last brick</h2>
  </div>
  <div class="wrap pgrid">
    <div class="pstick"><div class="pbox dots">
      <div class="pbar"><p>Stage <b style="font-weight:500;color:var(--blue)" id="stN">01</b> / 05</p><p id="stT">Site and brief</p></div>
      <div class="pdraw" id="pdraw"></div>
      <div class="psteps" id="psteps"></div>
    </div></div>
    <ol class="slist" id="slist"></ol>
  </div>
</section>

<section class="studio" id="studio" aria-labelledby="studio-title" data-section="studio">
  <div class="wrap sgrid">
    <div data-reveal><figure>
      <div class="fig" id="fig"><span class="tag">Fig. 01</span></div>
      <figcaption><span>The Linework studio, Islands Brygge</span><span>Copenhagen</span></figcaption>
    </figure></div>
    <div>
      <p class="eyebrow">( Why Linework )</p>
      <h2 id="studio-title">Made by architects, for the long table covered in drawings.</h2>
      <div class="cols">
        <p>Linework was started in Copenhagen by a small team of architects and engineers who were tired of redrawing the same detail for the fifth time. It works the way a good studio does: site first, light first, and drawings that stay true to what gets built.</p>
        <p>It never replaces the architect. You make every decision and sign every sheet. Linework does the measuring, the redrawing and the checking, so you have time to draw a hundred versions before you draw it once.</p>
      </div>
      <ol class="princ">
        <li><span>01</span><h3>Light first</h3><p>Every option is tested against the sun at every hour and in every season before you see it.</p></li>
        <li><span>02</span><h3>Materials that age well</h3><p>Brick, timber, lime and stone come with real ageing and carbon data, not just a texture.</p></li>
        <li><span>03</span><h3>You stay the architect</h3><p>Every suggestion is shown, explained and reversible. Nothing reaches a drawing without your say.</p></li>
      </ol>
      <dl class="stats" id="stats">
        <div><dt>Drawing types</dt><dd data-n="42">0</dd></div>
        <div><dt>Countries supported</dt><dd data-n="9">0</dd></div>
        <div><dt>Building codes mapped</dt><dd data-n="11">0</dd></div>
        <div><dt>Hours saved per week</dt><dd data-n="18">0</dd></div>
      </dl>
    </div>
  </div>
</section>

<section class="quotes" aria-labelledby="q-title" data-section="quotes">
  <div class="wrap">
    <div class="qtop"><p class="eyebrow">( In their words )</p><p class="mono" aria-live="polite"><span style="color:var(--ink)" id="qn">01</span> / 03</p></div>
    <h2 id="q-title" class="sr">What clients say</h2>
    <figure class="qfig" id="qfig"></figure>
    <div class="qnav"><div class="qdots" id="qdots"></div>
      <div><button class="circ" id="qprev" aria-label="Previous quote"><svg class="i" viewBox="0 0 24 24"><path d="m12 19-7-7 7-7M19 12H5"/></svg></button><button class="circ" id="qnext" aria-label="Next quote"><svg class="i" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg></button></div>
    </div>
  </div>
</section>
</main>

<footer id="contact" data-section="footer">
  <div class="wrap fgrid">
    <div>
      <p class="eyebrow">( Try Linework )</p>
      <h2>Have a site, a brief, or a sketch on a napkin?</h2>
      <button class="btn btn-w" data-enquire>Start drawing <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
    </div>
    <div class="fcols">
      <div><p class="eyebrow">Linework</p><address>Islands Brygge 43, 2300 Copenhagen S, Denmark</address><p class="h">Support Monday to Friday, 9:00 to 17:00 CET</p></div>
      <nav aria-label="Footer"><p class="eyebrow">Explore</p><ul><li><a href="#work">Projects</a></li><li><a href="#process">How it works</a></li><li><a href="#studio">Why Linework</a></li><li><a href="#contact">Contact</a></li></ul></nav>
    </div>
  </div>
  <div class="city" id="city"></div>
  <div class="fbot"><div class="wrap">
    <div><svg viewBox="0 0 32 32" width="24" height="24" aria-hidden="true" style="color:rgba(255,255,255,.7)"><g fill="none" stroke="currentColor"><rect x="3.5" y="3.5" width="25" height="25" stroke-width="1.4"/><path d="M10 28.5V16.5a6 6 0 0 1 12 0v12" stroke-width="1.4"/><path d="M3.5 10.5h25M16 3.5v7" stroke-width=".9"/></g></svg><p>© 2026 Linework. Drawn and built in Copenhagen.</p></div>
    <a href="#top">Back to top <svg class="i" viewBox="0 0 24 24"><path d="m5 12 7-7 7 7M12 19V5"/></svg></a>
  </div></div>
</footer>

<dialog id="dlgP" aria-labelledby="dP-title" data-section="dialogs"><div class="dbox">
  <button class="xbtn" data-close aria-label="Close"><svg class="i" viewBox="0 0 24 24"><path d="M18 6 6 18M6 6l12 12"/></svg></button>
  <div class="dart" id="dart"></div>
  <div class="dtxt" id="dtxt"></div>
</div></dialog>

<dialog id="dlgE" aria-labelledby="dE-title" style="max-width:640px"><div class="dbox" style="grid-template-columns:1fr">
  <button class="xbtn" data-close aria-label="Close"><svg class="i" viewBox="0 0 24 24"><path d="M18 6 6 18M6 6l12 12"/></svg></button>
  <div class="dtxt">
    <p class="eyebrow">( Get early access )</p>
    <h3 id="dE-title">Tell Linework about your next site.</h3>
    <form class="form" id="form">
      <label>Your name<input name="n" required autocomplete="name"></label>
      <label>Studio or practice<input name="o" autocomplete="organization"></label>
      <label>Email<input name="e" type="email" required autocomplete="email"></label>
      <label>What you design most<select name="t"><option>Cultural</option><option>Residential</option><option>Workplace</option><option>Public</option><option>Not sure yet</option></select></label>
      <label>A project you would try it on<textarea name="b" placeholder="Where is the site, who will use it, and what should it feel like?"></textarea></label>
      <button class="btn" type="submit">Request access <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
    </form>
    <p class="sent">Thank you. This page is a static demo, so nothing was sent, but you would usually hear back within two working days.</p>
  </div>
</div></dialog>

<script>
(()=>{
const $=(s,c=document)=>c.querySelector(s),$$=(s,c=document)=>[...c.querySelectorAll(s)];
const RM=matchMedia('(prefers-reduced-motion: reduce)').matches;
const r1=n=>Math.round(n*10)/10;
const R=(x,y,w,h)=>`M${r1(x)} ${r1(y)}H${r1(x+w)}V${r1(y+h)}H${r1(x)}Z`;
function rng(seed){return()=>{seed=(seed*16807)%2147483647;return (seed-1)/2147483646}}
const circ=(x,y,r)=>`M${r1(x-r)} ${r1(y)}a${r} ${r} 0 1 0 ${r*2} 0a${r} ${r} 0 1 0 ${-r*2} 0`;
const arch=(cx,yb,hw,ys)=>`M${r1(cx-hw)} ${r1(yb)}V${r1(ys)}A${r1(hw)} ${r1(hw)} 0 0 1 ${r1(cx+hw)} ${r1(ys)}V${r1(yb)}`;
function person(x,g,s=1){const h=16*s;return `${circ(x,g-h+1.6*s,1.6*s)}M${r1(x)} ${r1(g-h+3.4*s)}V${r1(g-6*s)}L${r1(x-2.4*s)} ${r1(g)}M${r1(x)} ${r1(g-6*s)}L${r1(x+2.4*s)} ${r1(g)}M${r1(x-2.6*s)} ${r1(g-8*s)}L${r1(x)} ${r1(g-12.5*s)}L${r1(x+2.6*s)} ${r1(g-8*s)}`}
function tree(x,g,h,seed=3){const rnd=rng(seed),r=h*.4,cy=g-h+r;let d=`M${x} ${g}V${r1(cy+r*.2)}M${x} ${r1(cy+r*.55)}L${r1(x-r*.4)} ${r1(cy+r*.05)}M${x} ${r1(cy+r*.4)}L${r1(x+r*.45)} ${r1(cy)}`;const n=11,pts=[];for(let i=0;i<n;i++){const a=i/n*Math.PI*2,rr=r*(.82+rnd()*.3);pts.push([x+Math.cos(a)*rr,cy+Math.sin(a)*rr*.92])}d+=`M${r1(pts[0][0])} ${r1(pts[0][1])}`;for(let i=1;i<=n;i++){const p=pts[i%n];d+=`A${r1(r*.36)} ${r1(r*.36)} 0 0 1 ${r1(p[0])} ${r1(p[1])}`}return d}
function palm(x,g,h,lean){const tx=x+lean,ty=g-h;let d=`M${x} ${g}Q${r1(x+lean*.1)} ${r1(g-h*.5)} ${r1(tx)} ${r1(ty)}M${x+3} ${g}Q${r1(x+3+lean*.1)} ${r1(g-h*.5)} ${r1(tx+1.5)} ${r1(ty)}`;const L=h*.42;for(let i=0;i<9;i++){const a=Math.PI*(1.05+i*.11),ex=tx+Math.cos(a)*L,ey=ty+Math.sin(a)*L*.55+L*.38,cx=tx+Math.cos(a)*L*.55,cy=ty+Math.sin(a)*L*.75;d+=`M${r1(tx)} ${r1(ty)}Q${r1(cx)} ${r1(cy)} ${r1(ex)} ${r1(ey)}`}return d}

/* ---------- buildings ---------- */
const B={
library(){const L=[];let win='',hat='',fl='',col='',sof='',cr='';
 for(let j=0;j<6;j++)for(let i=0;i<7;i++){const x=22.4+i*38.85,y=52+j*34;win+=R(x,y,22,22);hat+=`M${r1(x+3)} ${y+22}V${y+3}H${r1(x+22)}`}
 for(let j=0;j<5;j++)fl+=`M0 ${80+j*34}H300`;for(let x=46;x<=254;x+=26)col+=`M${x} 300V270`;for(let x=24;x<272;x+=6)sof+=`M${x} 270L${x+8} 262`;for(let x=120;x<=180;x+=15)cr+=`M${x} 30V8`;
 L.push(['o','M0 262V30H300V262Z'],['o','M20 262V300M280 262V300'],['l',R(105,8,90,22)],['w',win],['h',hat],['h',fl],['d','M-3 35H303'],['g',col],['l',R(132,274,36,26)+'M150 274V300'],['h',sof],['g',cr],['T',person(64,300)+person(212,300,.95)+person(228,300,.85)]);
 return {w:300,h:300,fill:R(0,30,300,232)+R(20,262,260,38)+R(105,8,90,22),L,gy:30}},
tower(){const prof='M0 600V540H10V380H24V250H40V150H58V70H76V40H144V70H162V150H180V250H196V380H210V540H220V600Z';const bands=[[540,380,10,210],[380,250,24,196],[250,150,40,180],[150,70,58,162]];let gl='',vg='',hx='';
 bands.forEach(([b,t,l,r])=>{for(let y=b-10;y>t;y-=10)gl+=`M${l} ${y}H96M124 ${y}H${r}`;for(let x=l+12;x<96;x+=12)vg+=`M${x} ${b}V${t}`;for(let x=136;x<r;x+=12)vg+=`M${x} ${b}V${t}`});
 for(let y=540;y>70;y-=30)hx+=`M96 ${y}L124 ${y-30}M124 ${y}L96 ${y-30}`;let g='';for(let x=22;x<=198;x+=22)g+=`M${x} 600V552`;
 return {w:220,h:600,fill:prof,gy:250,L:[['o',prof],['l','M110 40V0M104 14H116'],['w',R(96,70,28,470)],['g',gl],['h',vg],['d',hx],['l','M-8 552H228'],['g',g],['T',person(36,600)+person(170,600)+person(186,600,.85)+'M1 540Q5 533 9 540M211 540Q215 533 219 540M11 380Q17 373 23 380M197 380Q203 373 209 380M25 250Q32 243 39 250M181 250Q188 243 195 250']]}},
arcade(){let vault='',vf='',win='',inner='',lun='';for(let i=0;i<7;i++){const x=i*65.714,cx=x+32.857;vault+=`M${r1(x)} 70A32.86 28 0 0 1 ${r1(x+65.71)} 70`;vf+=`M${r1(x)} 70A32.86 28 0 0 1 ${r1(x+65.71)} 70Z`;win+=arch(cx,180,22,122)+'Z';inner+=arch(cx,180,18,122);lun+=`M${r1(x+5)} 70A27.9 23 0 0 1 ${r1(x+60.7)} 70M${r1(cx-11)} 70A11 11 0 0 1 ${r1(cx+11)} 70M${r1(cx)} 70V59`}
 return {w:460,h:190,fill:R(0,70,460,120)+vf,gy:122,L:[['o','M0 190V70H460V190'],['o',vault],['l','M0 180H460M-3 76H463'],['w',win],['d',inner],['h','M0 82H460M0 88H460M0 94H460'],['d',lun],['l','M218 180V150H242V180M230 180V150'],['T',person(82,190)+person(302,190)+person(361,190,.9)]]}},
mosque(){let w='',mb='',mh='';[72,112,228,268].forEach(cx=>w+=arch(cx,268,11,236)+'Z');w+=arch(170,330,22,270)+'Z';for(let x=128;x<=212;x+=12)mb+=`M${x} 198V182`;for(let y=120;y<=300;y+=10)mh+=`M0 ${y}H24`;
 return {w:300,h:330,top:12,gy:200,fill:R(40,200,260,130)+R(110,178,120,22)+R(0,70,24,260)+'M0 70L12 18L24 70ZM110 178A60 80 0 0 1 230 178Z',L:[['o','M40 330V200H300V330M110 200V178H230V200'],['o','M110 178A60 80 0 0 1 230 178'],['o','M0 330V70H24V330M0 70L12 18L24 70'],['l','M170 98V78'+circ(170,74,4)+'M12 18V10'],['l','M-6 98H30V92H-6ZM36 206H304M105 178H235'],['w',w],['d',mb+'M118 178A52 72 0 0 1 222 178'+'M40 209H300M40 213H300'],['h',mh],['d','M7 86V78A5 5 0 0 1 17 78V86'],['T',person(112,330)+person(232,330,.9)+person(250,330,.85)]]}},
hut(){let st='',stl='',tiles='',rf='';for(let x=14;x<136;x+=16){if(x>60&&x<92)continue;st+=R(x,76,8,74);stl+=`M${x} 150V76M${x+8} 150V76`}let x=1;tiles='M1 70';for(let i=0;i<21;i++){tiles+=`A3.5 3.5 0 0 1 ${x+7} 70`;x+=7}for(let y=42.5;y<70;y+=5)rf+=`M${r1(18-(y-40)*.6)} ${y}H${r1(132+(y-40)*.6)}`;
 return {w:150,h:160,top:-56,gy:70,fill:'M10 160V70H0L18 40H132L150 70H140V160Z',L:[['o','M10 160V70M140 160V70M0 70H150M18 40H132M0 70L18 40M150 70L132 40'],['s',st],['h',stl],['l','M10 150H140'+R(66,92,24,58)],['d',tiles],['h',rf],['l','M30 40V-48'],['d','M30 -48L58 -42L30 -36'+circ(27,-30,8)],['w',R(102,104,14,9)],['T',person(108,160)+'M20 160L22 155M22 160L25 154M118 160L120 155M121 160L123 154M44 160L46 156']]}},
stack(){const T=[[130,380,170,50],[40,330,240,50],[90,280,230,50],[20,230,230,50],[70,180,230,50],[30,130,230,50],[110,80,180,50]];let f=R(0,372,130,58),o=R(0,372,130,58),sl='',w='',g='';
 T.forEach(([x,y,ww,hh])=>{f+=R(x,y,ww,hh);o+=R(x,y,ww,hh);sl+=`M${x} ${y+14}H${x+ww}`;w+=R(x+10,y+14,ww-20,36);for(let gx=x+25;gx<x+ww-10;gx+=15)g+=`M${gx} ${y+50}V${y+14}`});
 return {w:320,h:430,fill:f,gy:230,L:[['o',o],['l',sl],['w',w],['g',g],['l',R(30,386,50,44)],['h','M40 430V386M50 430V386M60 430V386M70 430V386'],['T',tree(345,430,60,5)+person(160,430)+person(96,430,.9)+person(56,430,.95)]]}},
pavilion(){let h='';for(let y=128;y<=200;y+=18)h+=`M140 ${y}H200`;
 return {w:340,h:220,gy:70,fill:R(0,70,340,40)+R(140,110,60,110)+R(36,208,268,12),L:[['o',R(0,70,340,40)],['o','M140 220V110M200 220V110'],['l',R(36,208,268,12)+'M26 220V214H36M314 220V214H304'],['d','M0 104H340M170 110V220'],['h','M0 81.3H340M0 92.6H340'+h],['l','M58 194H128M212 194H282M62 208V194M124 208V194M216 208V194M278 208V194'],['T',person(96,220)+person(242,220)+person(258,220,.8)+tree(-40,220,90,9)+tree(380,220,110,4)]]}},
terraces(){let g='';for(let x=145;x<290;x+=29)g+=`M${x} 250V166`;for(let x=182;x<310;x+=32)g+=`M${x} 150V100`;for(let x=213.5;x<300;x+=31.5)g+=`M${x} 84V34`;let st='M4 250';for(let i=0;i<12;i++)st+=`V${r1(250-(i+1)*8.33)}H${r1(4+(i+1)*8)}`;
 return {w:330,h:250,top:-6,gy:150,fill:'M4 250L100 150V250Z'+R(100,150,200,16)+R(116,166,174,84)+R(150,100,160,50)+R(130,84,200,16)+R(170,20,150,64),L:[['o',R(100,150,200,16)+'M116 166V250M290 166V250M150 100V150M310 100V150'+R(130,84,200,16)+'M170 84V20H320V84'],['l',st+'M4 250L100 160'],['w',R(126,172,154,74)+R(160,104,140,44)+R(182,34,126,48)],['g',g],['d','M182 66H308M4 228L100 128'],['h','M104 150V128H148V150M104 137L109 128M107 150L120 128M117 150L130 128M128 150L140 128'],['T',tree(150,84,28,6)+person(52,200,.9)+person(220,250)]]}},
villa(){let g='';[202.5,245,287.5].forEach(x=>g+=`M${x} 190V120`);for(let x=221.3;x<376;x+=31.25)g+=`M${r1(x)} 108V46`;let h='';for(let x=380;x<440;x+=3)h+=`M${x} 108V46`;for(let x=334;x<440;x+=8)h+=`M${x} 186L${x+6} 124`;
 return {w:440,h:190,top:-40,gy:108,fill:R(40,108,400,12)+R(150,34,290,12)+R(190,46,250,62)+R(160,120,280,70),L:[['o',R(40,108,400,12)+R(150,34,290,12)+'M440 46V108M440 120V190'],['l','M160 190V120M190 108V46M78 190V120M81 190V120M330 190V120'],['w',R(160,120,170,66)+R(190,46,186,62)],['g',g],['h',h],['d','M160 186H330'+R(205,172,46,14)],['T',palm(70,190,150,-10)+palm(100,190,170,14)+palm(426,34,26,2)+person(250,190)+person(124,190,.9)]]}}
};
const P=[
 {id:'kalkvaerket-library',ai:'Ran 140 daylight studies of the reading hall and kept every gallery plan in step as the atrium changed size.',t:'Kalkværket Library',loc:'Aarhus, Denmark',y:'2024',c:'Cultural',s:'Completed',a:'6,400 m²',cl:'Kalkværket Library Trust',dr:'library',sum:'A white cube of a library, hollowed out into a five storey reading hall lit by a single roof light.',d:['Kalkværket replaces a closed lime works on the edge of the old harbour with a public library for 40,000 neighbours. From the street it reads as a calm, stone clad cube punctured by a regular grid of deep windows. Inside, the cube is hollowed out into a five storey reading hall.','Every floor is a gallery around that hall, so you can see the whole collection from the moment you step inside. Daylight falls from a single glazed roof lantern and is bounced down by white oiled oak and lime plaster, which keeps the reading rooms bright without a single blind.','The ground floor stays open late as a covered square, with a café, a children\'s workshop and a hall for concerts and debates.'],pal:{mat:'#efede6',acc:'#d8d2c4',sky:['#cfdcea','#f4efe6'],gr:'#d8d3c7'}},
 {id:'nordhavn-tower',ai:'Tested the four setbacks against shadow on the quay and coordinated the timber hybrid floors with the engineers.',t:'Nordhavn Tower',loc:'Copenhagen, Denmark',y:'2027',c:'Workplace',s:'Under construction',a:'38,000 m²',cl:'Nordhavn Harbour Developments',dr:'tower',sum:'A 31 storey workplace tower that steps back as it rises, with a deep glazed slot carved into each facade.',d:['Nordhavn Tower marks the end of the new harbour promenade. Instead of a single extruded block, the tower steps back in four stages, so its shadow on the quay stays short and every setback becomes a planted terrace for the floors below.','A deep vertical slot is cut into each facade. It brings daylight to the centre of the floor plates and holds the winter gardens, where people can step outside thirty floors above the water.','The structure is a concrete core with a timber hybrid floor system, cutting embodied carbon by roughly a third compared with a conventional office tower. Completion is planned for 2027.'],pal:{mat:'#b7c4d1',acc:'#7d93a8',sky:['#8fb0d3','#e6eef4'],gr:'#c9ccc8'}},
 {id:'arkaden-sculpture-gallery',ai:'Simulated a full year of sun through every reveal and drew each brick and limestone junction at 1:5.',t:'Arkaden Sculpture Gallery',loc:'Lund, Sweden',y:'2022',c:'Cultural',s:'Completed',a:'2,150 m²',cl:'Arkaden Art Foundation',dr:'arcade',sum:'A long vaulted arcade for sculpture, where the sun moves across the floor like the hand of a clock.',d:['Arkaden is a single room, 46 metres long, built for a private collection of twentieth century sculpture. Seven barrel vaults rest on a rhythm of lime plastered arches, and every bay faces south through a deep reveal.','Linework simulated the sun path for a full year before the architects fixed the depth of the windows. In the morning the light lands on the floor, at midday it climbs the walls, and in the late afternoon it reaches the sculptures at the far end of the gallery.','The building is made from a short list of materials: hand pressed brick, lime plaster and polished limestone, chosen to age slowly and to ask for almost nothing in return.'],pal:{mat:'#c48d6b',acc:'#ecdfcc',sky:['#f2c79a','#fbeee0'],gr:'#d9c9b0'}},
 {id:'fjordlys-mosque',ai:'Set out the panel grid so every fibre cement panel could be replaced by hand, with a bolt schedule to match.',t:'Fjordlys Mosque',loc:'Bergen, Norway',y:'2021',c:'Cultural',s:'Completed',a:'380 m²',cl:'Bergen Islamic Community',dr:'mosque',sum:'A domed mosque for a fjord side community, clad in blue stained panels that darken in the rain.',d:['Fjordlys gives a growing community its first purpose built mosque. They asked for something unmistakably a place of prayer, yet quiet enough to sit among the boathouses along the shore.','The answer is a low prayer hall under a single shallow timber dome, with a slender minaret beside it marking the mosque from the water. Arched windows face the fjord, and the hall is lined in pale spruce that glows when the evening light comes off the water.','The outer skin is a stained fibre cement panel in deep fjord blue, fixed with visible stainless steel bolts so that every panel can be replaced by hand.'],pal:{mat:'#365a80',acc:'#e9dcbd',sky:['#5b6f95','#e8c9a8'],gr:'#5f6e6a'}},
 {id:'hornbaek-bathing-house',ai:'Turned the architects\' sketches into step by step build sheets that volunteers could follow on site.',t:'Hornbæk Bathing House',loc:'Hornbæk, Denmark',y:'2020',c:'Public',s:'Completed',a:'64 m²',cl:'Hornbæk Winter Bathers',dr:'hut',sum:'A small striped bathing house for winter swimmers, built by its members over eleven weekends.',d:['The winter bathers of Hornbæk had been changing behind a hedge for twenty years. They asked for a warm room, two showers and a place to hang wet towels, on a budget raised from bake sales and a local foundation.','The house is a simple timber box under a clay tile roof, painted in the blue and white stripes of the old beach cabins along this coast. A single door faces the path to the water, so the warm air stays inside on the coldest mornings.','It was built in eleven weekends by the members themselves, from drawings the architects generated with Linework and simplified to be read by people who had never built anything before.'],pal:{mat:'#f8f7f2',acc:'#3c62b8',roof:'#b2593c',sky:['#b9d3e6','#eef4f6'],gr:'#e6dcc4'}},
 {id:'stakken-workhouse',ai:'Generated dozens of stacking options and checked each tray for terrace size, views and structural offsets.',t:'Stakken Workhouse',loc:'Malmö, Sweden',y:'2022',c:'Workplace',s:'Completed',a:'8,900 m²',cl:'Stakken Studios',dr:'stack',sum:'Seven concrete trays stacked off axis, giving every studio a terrace and a view across the Sound.',d:['Stakken is a workhouse for makers: architects, furniture builders, ceramicists and a small print shop. Each floor is a deep concrete tray, shifted from the one below, so the building opens a covered terrace on every level.','The board marked concrete is left exposed inside and out, and services run visibly along the ceilings, so tenants can change their spaces without opening a single wall.','A long workshop wing wraps the base of the stack. Its large doors open onto a shared yard, where the work spills outside all summer.'],pal:{mat:'#bdbab2',acc:'#8f8c84',sky:['#d3d9de','#f1efea'],gr:'#c4c0b6'}},
 {id:'lysning-pavilion',ai:'Mapped every tree in the clearing so the roof could be placed without felling a single one.',t:'Lysning Pavilion',loc:'Silkeborg, Denmark',y:'2020',c:'Public',s:'Completed',a:'220 m²',cl:'Silkeborg Forest Trust',dr:'pavilion',sum:'A concrete roof balanced on a single core, cantilevering eleven metres over a forest clearing.',d:['Lysning means clearing. The pavilion gives walkers, school classes and forest workers a dry place to gather, without cutting down a single tree.','One concrete core carries the entire roof, cantilevering eleven metres in every direction. Underneath there are no walls at all, only a timber floor and a long bench, so the forest stays in view from every side.','The underside of the roof was cast against rough sawn boards, milled from trees that fell on the site in an earlier storm.'],pal:{mat:'#cfcbc2',acc:'#a9845a',sky:['#dfe6e4','#f3f1ea'],gr:'#9aa58a'}},
 {id:'villa-klint',ai:'Balanced summer shading against winter sun for each overhang and kept three floors of section drawings in sync.',t:'Villa Klint',loc:'Hellerup, Denmark',y:'2024',c:'Residential',s:'Completed',a:'410 m²',cl:'Private client',dr:'terraces',sum:'A family house stepped into a slope, where every floor slides out to shade the one below.',d:['Villa Klint sits on a steep garden plot facing the sea. The family wanted a house that felt open to the water but private from the road, with a separate floor for grandparents who visit for weeks at a time.','The house is three white rendered trays, each sliding out from the one below. The overhangs shade the large windows in summer, while the low winter sun reaches deep into the living rooms. An outdoor stair links every terrace to the garden.','Behind the white render sits a heavy masonry structure that stores the warmth of the day and keeps the house comfortable with very little heating.'],pal:{mat:'#f4f3ee',acc:'#cfd6d8',sky:['#a9c4dc','#eef3f5'],gr:'#a7b391'}},
 {id:'casa-areia',ai:'Modelled cross ventilation and roof overhangs so the house stays cool without air conditioning.',t:'Casa Areia',loc:'Comporta, Portugal',y:'2023',c:'Residential',s:'Completed',a:'540 m²',cl:'Private client',dr:'villa',sum:'A long, low holiday house between the dunes and the pool, with thin roofs that reach out to the palms.',d:['Casa Areia is a holiday house for a Danish family who spend every summer on the Alentejo coast. The plot runs from the pine forest down to the dunes, and the house lies across it like a long, low wall.','Two thin white roofs float above the glazing and reach far out over the terraces, so the rooms stay shaded through the hottest hours. The ground floor glazing slides away completely, turning the living room into a covered porch beside the pool.','Local lime render, cork insulation and reclaimed terracotta floors keep the house cool without air conditioning for most of the year.'],pal:{mat:'#f7f3ea',acc:'#6f9a6a',sky:['#7fb4dc','#f6eedf'],gr:'#e7d6b4'}}
];
P.forEach(p=>p.b=B[p.dr]());

const hatchDef=id=>`<pattern id="${id}" width="7" height="7" patternUnits="userSpaceOnUse" patternTransform="rotate(45)"><line x1="0" y1="0" x2="0" y2="7" stroke="#4353ff" stroke-width=".9" stroke-opacity=".32"/></pattern>`;
const ORD={o:0,l:260,s:340,w:400,h:520,g:560,d:600,T:760};
function drawB(b,hid){const top=b.top||0;let s=`<path class="dfill" d="${b.fill}"/><path class="dhatch" fill="url(#${hid})" d="${b.fill}"/>`;
 s+=`<path class="sx" d="M-30 ${b.gy||b.h/2}H${b.w+30}M${b.w/2} ${b.h+18}V${top-18}"/>`;
 let tk='';for(let x=-4;x<b.w;x+=7)tk+=`M${x} ${b.h+7}L${x+6} ${b.h+1}`;
 s+=`<path class="st so" pathLength="1" d="M-20 ${b.h}H${b.w+20}" style="--d:0ms"/><path class="st sh" pathLength="1" d="${tk}" style="--d:60ms"/>`;
 b.L.forEach(([c,d],i)=>{if(d)s+=`<path class="st s${c}" pathLength="1" d="${d}" style="--d:${ORD[c]+i*26}ms;--dur:${c==='o'?950:760}ms"/>`});return s}
function photoB(p,id){const b=p.b,w=b.w,h=b.h,top=b.top||0,pal=p.pal,k=-.85,big=Math.max(w,h-top);
 let s=`<defs><linearGradient id="${id}s" gradientUnits="userSpaceOnUse" x1="0" y1="${top-big}" x2="0" y2="${h}"><stop offset="0" stop-color="${pal.sky[0]}"/><stop offset="1" stop-color="${pal.sky[1]}"/></linearGradient>
 <linearGradient id="${id}gl" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#e3eef7"/><stop offset=".45" stop-color="#7f97ad"/><stop offset="1" stop-color="#3c4f63"/></linearGradient>
 <linearGradient id="${id}sh" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="${w}" y2="0"><stop offset="0" stop-color="#fff" stop-opacity=".22"/><stop offset=".5" stop-color="#000" stop-opacity="0"/><stop offset="1" stop-color="#000" stop-opacity=".2"/></linearGradient>
 <radialGradient id="${id}sun"><stop offset="0" stop-color="#fff8e6"/><stop offset=".3" stop-color="#fff2d0" stop-opacity=".8"/><stop offset="1" stop-color="#fff2d0" stop-opacity="0"/></radialGradient>
 <filter id="${id}b" x="-50%" y="-50%" width="200%" height="200%"><feGaussianBlur stdDeviation="${r1(big/80)}"/></filter></defs>
 <rect x="-9999" y="-9999" width="19998" height="${9999+h}" fill="url(#${id}s)"/>
 <circle cx="${r1(w*.86)}" cy="${r1(top+(h-top)*.08)}" r="${r1(big*.32)}" fill="url(#${id}sun)"/>`;
 let hill=`M${-big*2} ${h}`;const rr=rng(w|0);for(let x=-big*2;x<w+big*2;x+=big*.12)hill+=`Q${r1(x+big*.06)} ${r1(h-big*(.06+rr()*.07))} ${r1(x+big*.12)} ${r1(h-big*.02)}`;hill+=`V${h}Z`;
 s+=`<path d="${hill}" fill="#6f7d6a" opacity=".35"/><rect x="-9999" y="${h}" width="19998" height="9999" fill="${pal.gr}"/>`;
 s+=`<path d="${b.fill}" fill="#1a1a1a" opacity=".28" filter="url(#${id}b)" transform="matrix(1 0 ${k} -.2 ${r1(-k*h)} ${r1(h*1.2)})"/>`;
 s+=`<path d="${b.fill}" fill="${pal.mat}"/>`;
 if(pal.roof&&p.dr==='hut')s+=`<path d="M0 70L18 40H132L150 70Z" fill="${pal.roof}"/>`;
 b.L.forEach(([c,d])=>{if(!d)return;
  if(c==='s')s+=`<path d="${d}" fill="${pal.acc}"/>`;
  else if(c==='w')s+=`<path d="${d}" fill="url(#${id}gl)" stroke="rgba(0,0,0,.35)" stroke-width="${r1(big/500)}"/>`;});
 s+=`<path d="${b.fill}" fill="url(#${id}sh)"/>`;
 b.L.forEach(([c,d])=>{if(!d||c==='s'||c==='w')return;const sw=big/600;
  const st={o:['rgba(20,20,20,.5)',1.2],l:['rgba(20,20,20,.38)',.9],d:['rgba(20,20,20,.2)',.7],h:['rgba(20,20,20,.14)',.5],g:['rgba(255,255,255,.6)',.6],T:['#3b4a37',1]}[c];
  s+=`<path d="${d}" fill="none" stroke="${st[0]}" stroke-width="${r1(st[1]*sw*1.4*10)/10}" stroke-linecap="round" stroke-linejoin="round"/>`});
 return s}
function vbFor(b,padF=.17,ext=1.6){const top=b.top||0,big=Math.max(b.w,b.h-top),pad=big*padF;const x=-pad*ext,y=top-pad*1.2,w=b.w+pad*ext*2,h=b.h-top+pad*2;return {vb:`${r1(x)} ${r1(y)} ${r1(w)} ${r1(h)}`,sw:w/620}}

/* ---------- hero ---------- */
function heroArt(){const W=1600,H=760,G=660,X0=60;const sAt=x=>Math.max(.3,1-(x-X0)/W*.66),baseAt=x=>G-(1-sAt(x))*120;
 const TH=[128,112,104,66],TOT=410,topAt=x=>baseAt(x)-TOT*sAt(x);const xr=X0+560,xe=X0+1150,rnd=rng(11);
 const segs=[];let cx=xr;while(cx<xe){const t=(cx-xr)/(xe-xr),tp=topAt(cx),bs=baseAt(cx);let y=tp+(bs-tp)*Math.pow(t,.7)+(rnd()-.5)*44*sAt(cx);y=Math.min(bs-6,Math.max(tp,y));const step=(16+rnd()*28)*sAt(cx);segs.push([cx,cx+step,y]);cx+=step}
 const cutAt=x=>{if(x<=xr)return topAt(x);if(x>=xe)return baseAt(x);for(const s of segs)if(x>=s[0]&&x<s[1])return s[2];return baseAt(x)};
 const out=[];const push=(c,d,dl,dur=800)=>{if(d)out.push(`<path class="st s${c}" pathLength="1" d="${d}" style="--d:${Math.round(dl)}ms;--dur:${dur}ms"/>`)};
 // ground
 let gl=`M0 ${G+22}H${W}`,gt='';for(let x=4;x<W;x+=9)gt+=`M${x} ${G+30}L${x+7} ${G+23}`;push('o',gl,0,1400);push('h',gt,100,1200);
 let gb=`M${X0} ${baseAt(X0)}`;for(let x=X0;x<=W;x+=20)gb+=`L${x} ${r1(baseAt(x))}`;push('l',gb,150,1500);
 // outline
 let ol=`M${X0} ${r1(baseAt(X0))}V${r1(topAt(X0))}`;for(let x=X0;x<=xr;x+=20)ol+=`L${x} ${r1(topAt(x))}`;segs.forEach(s=>{ol+=`L${r1(s[0])} ${r1(s[2])}L${r1(s[1])} ${r1(s[2])}`});ol+=`L${r1(xe)} ${r1(baseAt(xe)-4)}`;push('o',ol,200,2200);
 // bays
 let x=X0,i=0;const cornices=[[],[],[],[]];
 while(x<W-30){const s=sAt(x),w=82*s,xm=x+w/2,bs=baseAt(xm),cut=cutAt(xm),dl=300+(x-X0)*.9;
  if(x+w>xe+20){ // ruins beyond
   if(i%2===0){const hh=(14+rnd()*36)*s;push('l',`M${r1(x+w*.15)} ${r1(bs)}V${r1(bs-hh)}H${r1(x+w*.42)}V${r1(bs-hh*.6)}`,dl)}
   let st='';for(let k=0;k<3;k++){const sx=x+rnd()*w,sw=(6+rnd()*14)*s,sh=(4+rnd()*7)*s;st+=`M${r1(sx)} ${r1(G+22)}L${r1(sx+sw*.1)} ${r1(G+22-sh)}L${r1(sx+sw*.8)} ${r1(G+22-sh*1.1)}L${r1(sx+sw)} ${r1(G+22)}`}push('d',st,dl+200);
   x+=w;i++;continue}
  let acc=0,lines='',det='',hat='',win='';
  for(let t=0;t<4;t++){const yb=bs-acc*s,yt=yb-TH[t]*s;acc+=TH[t];if(yb<=cut+3)break;
   cornices[t].push([x,x+w,yt,yt>cut]);
   if(t<3){const hw=w*.31,spring=yb-TH[t]*s*.4,ap=spring-hw;
    if(ap>=cut){win+=arch(xm,yb,hw,spring);det+=`M${r1(xm-hw-4*s)} ${r1(spring)}A${r1(hw+4*s)} ${r1(hw+4*s)} 0 0 1 ${r1(xm+hw+4*s)} ${r1(spring)}`;det+=`M${r1(xm-hw+w*.1)} ${r1(yb)}V${r1(spring)}A${r1(hw)} ${r1(hw)} 0 0 1 ${r1(xm+hw)} ${r1(spring-hw*.3)}`;
     for(let hx=xm-hw+3*s;hx<xm+hw;hx+=(hx>xm?3:4.5)*s){const dx=hx-xm,yy=spring-Math.sqrt(Math.max(0,hw*hw-dx*dx));hat+=`M${r1(hx)} ${r1(yb)}V${r1(yy+2)}`}}
    else if(spring>cut)win+=`M${r1(xm-hw)} ${r1(yb)}V${r1(Math.max(cut,spring))}M${r1(xm+hw)} ${r1(yb)}V${r1(Math.max(cut,spring))}`;
    lines+=`M${r1(x+w*.06)} ${r1(yb)}V${r1(Math.max(yt,cut))}M${r1(x+w*.12)} ${r1(yb)}V${r1(Math.max(yt,cut))}`;
    if(yt+7*s>cut)det+=`M${r1(x+w*.02)} ${r1(yt+7*s)}H${r1(x+w*.16)}`;
    det+=`M${r1(xm-hw-2*s)} ${r1(spring)}H${r1(xm-hw+2*s)}M${r1(xm+hw-2*s)} ${r1(spring)}H${r1(xm+hw+2*s)}`;
   }else if(i%2===0){const ry=yb-TH[3]*s*.62,rh=TH[3]*s*.3;if(ry>cut)win+=R(xm-w*.12,ry,w*.24,rh)}
  }
  push('l',lines,dl);push('w',win,dl+120);push('d',det,dl+260);push('h',hat,dl+360);
  let st='';if(x>xr-60){for(let k=0;k<2;k++){const sx=x+rnd()*w,sw=(7+rnd()*12)*s,sh=(4+rnd()*6)*s;st+=`M${r1(sx)} ${r1(bs)}L${r1(sx+sw*.2)} ${r1(bs-sh)}L${r1(sx+sw)} ${r1(bs-sh*.8)}L${r1(sx+sw)} ${r1(bs)}`}push('d',st,dl+300)}
  x+=w;i++}
 cornices.forEach((arr,t)=>{let d='',d2='';arr.forEach(([a,b,y,ok])=>{if(!ok)return;const s=sAt(a);d+=`M${r1(a)} ${r1(y)}L${r1(b)} ${r1(y-(sAt(a)-sAt(b))*-0)}`;d2+=`M${r1(a)} ${r1(y+5*s)}H${r1(b)}`});push('l',d,400+t*160,1700);push('d',d2,520+t*160,1700)});
 // foreground
 let T='';T+=tree(1470,G+22,190,8).replace(/A[\d.]+ [\d.]+/g,m=>m);
 const cyp=(x,h,wd)=>`M${x} ${G+22}V${G+10}M${x} ${G+10}C${x-wd} ${G-h*.3} ${x-wd*.6} ${G-h*.8} ${x} ${G+10-h}C${x+wd*.6} ${G-h*.8} ${x+wd} ${G-h*.3} ${x} ${G+10}`;
 T+=cyp(1530,230,26)+cyp(1566,180,20)+cyp(1392,150,18);
 let ch='';for(let k=0;k<26;k++){const yy=G+10-k*8;ch+=`M1524 ${yy}L${1536} ${yy-6}`}
 push('T',T,1700,1300);push('h',ch,2000,900);
 let ppl=person(560,G+22,1.3)+person(578,G+22,1.2)+person(820,G+22,1.25)+person(1040,G+22,1.3)+person(1180,G+22,1.1);push('T',ppl,1900,900);
 // guides
 const vx=X0+W/.66,vy=G-120;let gd='';[0,128,240,344,410].forEach(hh=>{const y0=G-hh;const y1=y0+(vy-y0)*((W-X0)/(vx-X0));gd+=`M${X0} ${y0}L${W} ${r1(y1)}`});
 out.unshift(`<path class="sx" style="opacity:.55" d="${gd}"/>`);
 let dim=`M30 ${G}V${r1(topAt(X0))}M24 ${G}H36M24 ${r1(topAt(X0))}H36`;push('g',dim,600);
 out.push(`<text class="lbl" x="18" y="${r1((G+topAt(X0))/2)}" font-size="11" transform="rotate(-90 18 ${r1((G+topAt(X0))/2)})" text-anchor="middle">41.0 m</text>`);
 return {svg:out.join(''),W,H,G,X0}}

function mountHero(){const h=heroArt(),el=$('#heroArt');
 el.innerHTML=`<svg viewBox="0 0 ${h.W} ${h.H}" role="img" aria-label="Ink drawing of a Roman amphitheatre: four tiers of arches rise on the left, then the wall curves away and steps down into a long ruin">
 <defs><clipPath id="lensClip"><rect id="lensRect" x="0" y="0" width="300" height="190"/></clipPath>
 <pattern id="bpGrid" width="20" height="20" patternUnits="userSpaceOnUse"><path d="M20 0H0V20" fill="none" stroke="#fff" stroke-opacity=".14" stroke-width=".6"/><circle cx="0" cy="0" r="1" fill="#fff" fill-opacity=".35"/></pattern></defs>
 <g class="ink art" style="--sw:1">${h.svg}</g>
 <g clip-path="url(#lensClip)"><rect width="${h.W}" height="${h.H}" fill="#4353ff"/><rect width="${h.W}" height="${h.H}" fill="url(#bpGrid)"/><g class="art" style="color:#fff;--sw:1.1">${h.svg.replace(/class="sx"/g,'class="sx" style="opacity:.9;stroke:#fff"')}</g></g>
 <line id="scan" x1="0" x2="${h.W}" y1="0" y2="0" stroke="#4353ff" stroke-width="1.2" style="filter:drop-shadow(0 0 8px rgba(67,83,255,.7))"/>
 <g id="lensFrame" style="pointer-events:none"><g fill="none" stroke="#4353ff" stroke-width="1.2"><path d="M0 16V0H16M284 0H300V16M300 174V190H284M16 190H0V174"/><path d="M-10 0H6M0 -10V6" stroke-width=".8"/></g>
 <text x="0" y="-12" class="lbl" font-size="11" style="fill:#4353ff">DETAIL A, 1:200</text>
 <g transform="translate(300 202)"><rect x="-128" y="0" width="128" height="20" rx="3" fill="#4353ff"/><text id="lensXY" x="-64" y="14" class="lbl" font-size="11" text-anchor="middle" style="fill:#fff">X 0.0 m  H 0.0 m</text></g></g></svg>`;
 const svg=$('svg',el),rect=$('#lensRect'),frame=$('#lensFrame'),xy=$('#lensXY');
 requestAnimationFrame(()=>{$$('.art',svg).forEach(g=>g.classList.add('on'));el.classList.add('go')});
 let tx=h.W*.32,ty=h.H*.42,cx=tx,cy=ty,user=false,t0=performance.now();
 const toSvg=e=>{const pt=svg.createSVGPoint();pt.x=e.clientX;pt.y=e.clientY;return pt.matrixTransform(svg.getScreenCTM().inverse())};
 svg.addEventListener('pointermove',e=>{if(e.pointerType==='touch')return;const p=toSvg(e);tx=p.x;ty=p.y;user=true});
 svg.addEventListener('pointerdown',e=>{const p=toSvg(e);tx=p.x;ty=p.y;user=true});
 svg.addEventListener('pointerleave',()=>{user=false;t0=performance.now()});
 const tick=now=>{if(!user){const t=(now-t0)/1000;tx=h.W*(.36+.2*Math.sin(t*.35));ty=h.H*(.48+.13*Math.sin(t*.6))}
  cx+=(tx-cx)*(RM?1:.12);cy+=(ty-cy)*(RM?1:.12);const lx=cx-150,ly=cy-95;rect.setAttribute('x',r1(lx));rect.setAttribute('y',r1(ly));frame.setAttribute('transform',`translate(${r1(lx)} ${r1(ly)})`);
  xy.textContent=`X ${((cx-h.X0)/10).toFixed(1).padStart(5,' ')} m  H ${Math.max(0,(h.G-cy)/10).toFixed(1)} m`;requestAnimationFrame(tick)};requestAnimationFrame(tick)}

/* ---------- skyline & panel ---------- */
const XS=[34,454,790,1366,1772,2028,2464,2920,3366],VB={x:-34,y:-660,w:3904,h:700};
let filter='All',act=0;
function mountSky(){let g='';P.forEach((p,i)=>{const b=p.b;g+=`<g class="bg" data-i="${i}" transform="translate(${XS[i]} ${-b.h})" style="--bd:${i*140}ms"><g class="lift"><rect x="-50" y="${(b.top||0)-50}" width="${b.w+100}" height="${b.h-(b.top||0)+60}" fill="transparent"/>${drawB(b,'hx1')}</g></g>`});
 let gt='';for(let x=-30;x<3870;x+=9)gt+=`M${x} 8L${x+7} 1`;
 $('#sky').innerHTML=`<svg viewBox="${VB.x} ${VB.y} ${VB.w} ${VB.h}" aria-hidden="true"><defs>${hatchDef('hx1')}</defs><path class="st so" pathLength="1" d="M-34 0H3870" style="--dur:1800ms"/><path class="st sh" pathLength="1" d="${gt}" style="--dur:1800ms"/>${g}</svg><div class="bubble" id="bubble"><div><em></em><span></span><svg class="i" viewBox="0 0 24 24" style="width:14px;height:14px"><path d="M7 7h10v10M7 17 17 7"/></svg></div><i></i></div>`;
 $('#ticks').innerHTML=P.map((p,i)=>`<li style="left:${r1((XS[i]+p.b.w/2-VB.x)/VB.w*1000)/10}%"><a href="#${p.id}" data-i="${i}">${String(i+1).padStart(2,'0')}<span class="sr">${p.t}</span></a></li>`).join('');
 const cats=['All','Cultural','Workplace','Public','Residential'];
 $('#filters').innerHTML=cats.map(c=>`<button class="chip" aria-pressed="${c==='All'}" data-c="${c}">${c}<span>${c==='All'?P.length:P.filter(p=>p.c===c).length}</span></button>`).join('');
 const svg=$('#sky svg');
 io(svg,()=>{svg.classList.add('on');$$('.bg',svg).forEach(b=>b.classList.add('on'))},.25);
 $$('.bg',svg).forEach(b=>{const i=+b.dataset.i;b.addEventListener('mouseenter',()=>setAct(i));b.addEventListener('click',()=>{if(act===i)openP(i);else setAct(i)})});
 $$('#ticks a').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();setAct(+a.dataset.i)}));
 $$('#filters .chip').forEach(c=>c.addEventListener('click',()=>{filter=c.dataset.c;$$('#filters .chip').forEach(x=>x.setAttribute('aria-pressed',x===c));
  $$('.bg',svg).forEach(b=>{const p=P[+b.dataset.i],ok=filter==='All'||p.c===filter;b.classList.toggle('muted',!ok);if(ok){b.classList.remove('on');b.getBBox();b.style.setProperty('--bd',(+b.dataset.i%4)*90+'ms');setTimeout(()=>b.classList.add('on'),40)}});
  $$('#ticks a').forEach(a=>{const p=P[+a.dataset.i];a.classList.toggle('muted',!(filter==='All'||p.c===filter))});
  if(!(filter==='All'||P[act].c===filter))setAct(P.findIndex(p=>p.c===filter))}));
 setAct(0,true)}
function vis(){return P.map((p,i)=>i).filter(i=>filter==='All'||P[i].c===filter)}
function setAct(i,first){if(i===act&&!first)return;act=i;const p=P[i],b=p.b;
 $$('#sky .bg').forEach(g=>g.classList.toggle('active',+g.dataset.i===i));
 $$('#ticks a').forEach(a=>a.classList.toggle('cur',+a.dataset.i===i));
 const bub=$('#bubble');bub.style.left=((XS[i]+b.w/2-VB.x)/VB.w*100)+'%';bub.style.top=((-b.h+(b.top||0)-20-VB.y)/VB.h*100)+'%';
 $('em',bub).textContent=String(i+1).padStart(2,'0');$('span',bub).textContent=p.t;
 const v=vbFor(b);
 $('#pv .sk').innerHTML=`<svg viewBox="${v.vb}" preserveAspectRatio="xMidYMid meet" style="--sw:${r1(v.sw*10)/10}" aria-hidden="true"><defs>${hatchDef('hx2')}</defs><g>${drawB(b,'hx2')}</g></svg>`;
 $('#pv .ph').innerHTML=`<svg viewBox="${v.vb}" preserveAspectRatio="xMidYMid meet" aria-hidden="true">${photoB(p,'pp'+i)}</svg>`;
 $('#pv').setAttribute('aria-label','Open '+p.t);
 const g=$('#pv .sk svg>g');requestAnimationFrame(()=>requestAnimationFrame(()=>g.classList.add('on')));
 const pi=$('#pinfo');pi.classList.remove('swap');void pi.offsetWidth;pi.classList.add('swap');
 pi.innerHTML=`<div class="prow"><p class="mono">No. ${String(i+1).padStart(2,'0')} / 09</p><span class="badge">${p.c}</span></div>
 <h3>${p.t}</h3><p class="meta">${p.loc}<span aria-hidden="true" style="margin:0 8px">·</span>${p.y}</p><p class="sum">${p.sum}</p>
 <dl><div><dt>Area</dt><dd>${p.a}</dd></div><div><dt>Status</dt><dd>${p.s}</dd></div></dl>
 <div class="pact"><button class="btn" id="viewP">View project <svg class="i" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17 17 7"/></svg></button><div><button class="circ" id="pPrev" aria-label="Previous building"><svg class="i" viewBox="0 0 24 24"><path d="m12 19-7-7 7-7M19 12H5"/></svg></button><button class="circ" id="pNext" aria-label="Next building"><svg class="i" viewBox="0 0 24 24"><path d="M5 12h14M12 5l7 7-7 7"/></svg></button></div></div>`;
 $('#viewP').onclick=()=>openP(act);
 const step=d=>{const v=vis(),k=v.indexOf(act);setAct(v[(k+d+v.length)%v.length])};$('#pPrev').onclick=()=>step(-1);$('#pNext').onclick=()=>step(1)}
function mountPv(){const pv=$('#pv');const mv=e=>{const r=pv.getBoundingClientRect();pv.style.setProperty('--mx',(e.clientX-r.left)+'px');pv.style.setProperty('--my',(e.clientY-r.top)+'px')};
 pv.addEventListener('pointerenter',e=>{if(e.pointerType==='touch')return;mv(e);pv.classList.add('rev')});pv.addEventListener('pointermove',mv);pv.addEventListener('pointerleave',()=>pv.classList.remove('rev'));
 pv.addEventListener('click',e=>{if(e.pointerType==='touch'||matchMedia('(pointer:coarse)').matches){if(!pv.classList.contains('rev')){mv(e);pv.classList.add('rev');return}}openP(act)});
 pv.addEventListener('keydown',e=>{if(e.key==='Enter'||e.key===' '){e.preventDefault();openP(act)}})}
function openP(i){const p=P[i],b=p.b,v=vbFor(b,.22,1.8),d=$('#dlgP');
 $('#dart').innerHTML=`<div class="dots" style="position:absolute;inset:0"><svg viewBox="${v.vb}" preserveAspectRatio="xMidYMid meet" style="--sw:${r1(v.sw*10)/10};color:var(--ink)"><defs>${hatchDef('hx4')}</defs><g>${drawB(b,'hx4')}</g></svg></div><div class="ph"><svg viewBox="${v.vb}" preserveAspectRatio="xMidYMid meet">${photoB(p,'dp')}</svg></div><div class="split"><b>⟷</b></div><input type="range" min="0" max="100" value="50" aria-label="Compare drawing and rendering">`;
 $('#dtxt').innerHTML=`<div class="prow"><p class="mono">No. ${String(i+1).padStart(2,'0')} / 09</p><span class="badge">${p.c}</span></div><h3 id="dP-title">${p.t}</h3><p class="lead" style="margin-top:12px">${p.sum}</p><div class="desc">${p.d.map(x=>`<p>${x}</p>`).join('')}</div><div style="margin-top:24px;padding:16px 18px;border:1px solid rgba(67,83,255,.3);background:var(--blue-soft);border-radius:6px"><p class="eyebrow" style="color:var(--blue)">With Linework</p><p style="margin-top:6px;font-size:15px;line-height:1.6">${p.ai}</p></div><dl><div><dt>Location</dt><dd>${p.loc}</dd></div><div><dt>Year</dt><dd>${p.y}</dd></div><div><dt>Area</dt><dd>${p.a}</dd></div><div><dt>Status</dt><dd>${p.s}</dd></div><div style="grid-column:1/-1"><dt>Client</dt><dd>${p.cl}</dd></div></dl>`;
 const rg=$('#dart input'),ph=$('#dart .ph'),sp=$('#dart .split');rg.oninput=()=>{ph.style.clipPath=`inset(0 0 0 ${rg.value}%)`;sp.style.left=rg.value+'%'};
 d.showModal();const g=$('#dart svg>g');requestAnimationFrame(()=>requestAnimationFrame(()=>g.classList.add('on')))}

/* ---------- process ---------- */
const STAGES=[['Site and brief','Drop in a plot, a few photos and your notes. Linework maps the sun, the wind, the setbacks and the neighbours, and drafts a brief you refine with your client.','Minutes, not weeks'],['Concept and massing','Ask for options and it sketches simple volumes, testing each against the plot, the light and the street. Keep the ones you like and send the rest back.','Dozens of options an hour'],['Structure','Grids, spans and floor depths are proposed early and checked with your engineers, so the structure becomes part of the architecture instead of something hidden behind it.','Shared with your engineers'],['Facade and detail','Choose materials for how they age. Linework drafts joints at 1:5, flags clashes and keeps every sheet in step when the design changes.','Every sheet stays in sync'],['Built and handed over','Through construction it tracks site queries, revisions and snag lists, then turns the final set into a handover pack the client can actually use.','To the last snag']];
function mountProcess(){const E=[];const a=(s,c,d,dur=900)=>E.push([s,c,d,dur]);
 let tk='';for(let x=100;x<=820;x+=7)tk+=`M${x} 477L${x+6} 471`;
 a(0,'o','M-64 470H964',1300);a(0,'h',tk,800);a(0,'x','M-40 470V280H40V470M860 470V330L910 270L960 330V470M60 330A390 290 0 0 1 840 330');
 a(0,'d',circ(450,40,13)+'M468 40H475M462.7 52.7L467.7 57.7M450 65V58M432.3 57.7L437.3 52.7M425 40H432M432.3 22.3L437.3 27.3M450 22V15M462.7 27.3L467.7 22.3');
 a(0,'d','M114 476L126 464M114 464L126 476M444 476L456 464M444 464L456 476M794 476L806 464M794 464L806 476M100 470V446L112 450L100 454M820 470V446L832 450L820 454');
 a(0,'T',tree(64,470,90,2));a(0,'d',circ(900,70,15)+'M900 88V50M894 60L900 50L906 60');
 a(0,'h','M-40 500Q60 494 160 500T360 500T560 500T760 500T960 500M-40 524Q80 518 200 524T440 524T680 524T920 524',1200);
 const mass='M120 330H520V470H120ZM110 330L150 262H520V330ZM520 150H800V470H520Z';
 a(1,'o','M120 470V330M107 330H523M108 334L152 258M147 262H523');a(1,'o','M520 470V150M800 470V150M509 150H811');
 let ft='';[110,180,250,320,390,460,510,580,650,720,790].forEach(x=>ft+=R(x,470,20,16));
 a(2,'l',ft);a(2,'l','M520 530V486M590 530V486M660 530V486M730 530V486M800 530V486');a(2,'l','M190 470V330M260 470V330M330 470V330M400 470V330M470 470V330M120 400H520');a(2,'d','M120 406H520');
 a(2,'d','M190 330V262M120 330L190 262M260 330V262M190 330L260 262M330 330V262M260 330L330 262M400 330V262M330 330L400 262M470 330V262M400 330L470 262');
 a(2,'l','M590 470V150M660 470V150M730 470V150M520 390H800M520 310H800M520 230H800');a(2,'d','M520 396H800M520 316H800M520 236H800M520 156H800');
 a(2,'g','M114 236H526M117 239L123 233M517 239L523 233M120 241V227M520 241V227M514 116H806M517 119L523 113M797 119L803 113M520 121V107M800 121V107M821.5 463H830.5L826 470ZM818 470H872M821.5 143H830.5L826 150ZM818 150H872');
 let hw='',hm='';for(let i=0;i<6;i++){const x=134+70*i,w=i===5?26:42;hw+=R(x,414,w,50)+R(x+4,342,w-8,48);hm+=`M${x+w/2} 464V414M${x+w/2} 390V342`}
 let bw='',bm='';for(let j=0;j<4;j++)for(let i=0;i<4;i++){if(j===3&&i===0)continue;const x=533+70*i,y=165+80*j;bw+=R(x,y,44,50);bm+=`M${x+22} ${y+50}V${y}`}
 let rh='';for(let k=0;k<8;k++){const y=266+k*8;rh+=`M${r1(147.6-k*4.7)} ${y}H520`}
 a(3,'d',hw);a(3,'g',hm);a(3,'d',bw);a(3,'g',bm);a(3,'h',rh,1200);a(3,'l','M530 470V400H580V470ZM555 470V400M508 394H604');a(3,'d','M514 144H806M532 144L558 130M568 144L594 130M604 144L630 130M640 144L666 130M676 144L702 130M712 144L738 130M748 144L774 130');
 a(4,'T',tree(168,470,60,4)+tree(882,470,80,6));a(4,'T',person(566,470)+person(614,470)+person(300,470,.95)+person(316,470,.8)+person(704,470));a(4,'T',circ(432,462,8)+circ(462,462,8)+'M432 462L444 450L462 462M444 450H456L462 462M442 446H448M456 450L458 444');
 const labels=[[0,900,108,'N'],[0,460,438,'SITE, 1:200'],[2,320,228,'28.00'],[2,660,108,'19.60'],[2,836,466,'±0.00','start'],[2,836,146,'+15.40','start']];
 let s=`<defs>${hatchDef('hx3')}</defs><path class="fade" data-s="1" d="${mass}" fill="url(#hx3)"/><path class="fade" data-s="4" d="${mass}" fill="#efe9dc" style="mix-blend-mode:multiply"/>`;
 const cnt=[0,0,0,0,0];E.forEach(([st,c,d,dur])=>{const k=cnt[st]++;s+=c==='x'?`<path class="sx" data-s="${st}" d="${d}"/>`:`<path class="st s${c}" data-s="${st}" pathLength="1" d="${d}" style="--d:${k*140}ms;--dur:${dur}ms"/>`});
 labels.forEach(([st,x,y,t,an])=>s+=`<text class="lbl" data-s="${st}" x="${x}" y="${y}" font-size="13" text-anchor="${an||'middle'}" style="--d:700ms">${t}</text>`);
 $('#pdraw').innerHTML=`<svg viewBox="-84 -5 1068 555" role="img" aria-label="A community house drawn stage by stage">${s}</svg>`;
 $('#psteps').innerHTML=STAGES.map((x,i)=>`<button aria-label="Stage 0${i+1}: ${x[0]}"><i></i><span>0${i+1}</span></button>`).join('');
 $('#slist').innerHTML=STAGES.map((x,i)=>`<li data-step="${i}"><div><p class="n">0${i+1}</p><h3>${x[0]}</h3><p class="lead">${x[1]}</p><p class="pill">${x[2]}</p></div></li>`).join('');
 let cur=-1;const set=n=>{if(n===cur)return;cur=n;$('#stN').textContent='0'+(n+1);$('#stT').textContent=STAGES[n][0];
  $$('#pdraw [data-s]').forEach(el=>{const s=+el.dataset.s;el.classList.toggle('on',s<=n);el.classList.toggle('cur',s===n)});
  $$('#psteps button').forEach((b,i)=>{b.classList.toggle('cur',i===n);b.classList.toggle('done',i<n);i===n?b.setAttribute('aria-current','step'):b.removeAttribute('aria-current')});
  $$('#slist li').forEach((l,i)=>l.classList.toggle('cur',i===n))};
 const ob=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting)set(+e.target.dataset.step)}),{rootMargin:'-45% 0px -45% 0px'});$$('#slist li').forEach(l=>ob.observe(l));
 $$('#psteps button').forEach((b,i)=>b.addEventListener('click',()=>{$$('#slist li')[i].scrollIntoView({behavior:RM?'auto':'smooth',block:'center'})}));
 io($('#pdraw'),()=>{if(cur<0)set(0)},.2)}

/* ---------- studio figure ---------- */
function mountFig(){const sheets=[[38,70,120,92,'library',-1.5],[176,58,104,138,'tower',1],[300,82,78,60,'hut',-2],[40,184,150,70,'arcade',.8],[208,214,96,84,'stack',-1],[318,160,64,104,'mosque',1.6],[60,280,110,62,'villa',1.2]];
 let s=`<defs><filter id="fb" x="-30%" y="-10%" width="160%" height="120%"><feGaussianBlur stdDeviation="7 1.5"/></filter><filter id="ds"><feDropShadow dx="1" dy="2" stdDeviation="2" flood-opacity=".18"/></filter>
 <linearGradient id="wall" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#e2e2dc"/><stop offset="1" stop-color="#c9c9c2"/></linearGradient><radialGradient id="lamp" cx=".5" cy="0" r="1"><stop offset="0" stop-color="#fff" stop-opacity=".55"/><stop offset="1" stop-color="#fff" stop-opacity="0"/></radialGradient></defs>
 <rect width="400" height="500" fill="url(#wall)"/>`;
 for(let y=0;y<380;y+=26)s+=`<path d="M0 ${y}H400" stroke="#000" stroke-opacity=".035"/>`;
 sheets.forEach(([x,y,w,h,k,rot],n)=>{const b=B[k](),top=b.top||0,sc=Math.min((w-14)/(b.w+40),(h-14)/(b.h-top+20));
  s+=`<g transform="rotate(${rot} ${x+w/2} ${y+h/2})" filter="url(#ds)"><rect x="${x}" y="${y}" width="${w}" height="${h}" fill="#fbfbf8"/><g class="static" style="color:#2a2a28;--sw:${r1(1.1/sc*10)/10}" transform="translate(${r1(x+(w-b.w*sc)/2)} ${r1(y+h-8-(b.h)*sc)}) scale(${r1(sc*1000)/1000})">${drawB(b,'hxs').replace('class="sx"','class="sx" style="display:none"')}</g><rect x="${x+w/2-9}" y="${y-5}" width="18" height="9" fill="#efe7cf" opacity=".85"/></g>`});
 s+=`<rect y="370" width="400" height="130" fill="#b9b8b1"/><path d="M0 372H400" stroke="#8e8d86"/><rect x="20" y="392" width="360" height="10" fill="#d8d7d0"/><path d="M40 402V500M360 402V500" stroke="#6f6e68" stroke-width="3"/>`;
 s+=`<g fill="none" stroke="#5b5a55"><path d="M70 392c0-8 40-8 40 0M120 392c0-10 60-10 60 0" stroke-width="1.2"/><ellipse cx="260" cy="388" rx="44" ry="5"/><path d="M216 388l-6-10h100l-6 10" /></g>`;
 s+=`<path d="M290 0V40" stroke="#333" stroke-width="1.2"/><path d="M270 40h40l-8 16h-24z" fill="#2c2c2a"/><path d="M262 56L180 380H400L318 56Z" fill="url(#lamp)"/>`;
 s+=`<g id="walker"><g filter="url(#fb)" fill="#262624" opacity=".86"><circle cx="0" cy="170" r="20"/><path d="M-30 196Q0 182 30 196L36 330H-36Z"/><path d="M-26 326L-34 480H-10L0 340L10 480H34L26 326Z"/></g></g>`;
 s+=`<rect width="400" height="500" fill="#000" opacity=".04"/>`;
 $('#fig').insertAdjacentHTML('beforeend',`<svg viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" role="img" aria-label="A colleague walking past drawings pinned to the wall of the studio" style="filter:grayscale(1) contrast(1.04)"><defs>${hatchDef('hxs')}</defs>${s}</svg>`)}

/* ---------- footer city ---------- */
function mountCity(){const W=3168,H=1180,Y=980,rnd=rng(21);const out=[];let dl=0;const push=(c,d,dur=900)=>{if(d){out.push(`<path class="st s${c}" pathLength="1" d="${d}" style="--d:${Math.round(dl)}ms;--dur:${dur}ms"/>`);dl+=22}};
 const winGrid=(x,y,w,h,cols,rows,ww,wh)=>{let d='';const gx=w/cols,gy=h/rows;for(let i=0;i<cols;i++)for(let j=0;j<rows;j++)d+=R(x+gx*i+(gx-ww)/2,y+gy*j+(gy-wh)/2,ww,wh);return d};
 const town=(x,w,h,type)=>{const t=Y-h;let o;if(type===0){o=`M${x} ${Y}V${t}`;const st=5,sw=w/2/st,sh=60/st;let cx=x;for(let i=0;i<st;i++){o+=`V${r1(t-sh*i-sh)}H${r1(cx+sw)}`;cx+=sw}for(let i=st;i>0;i--){o+=`V${r1(t-sh*(i-1))}H${r1(cx+sw)}`;cx+=sw}o+=`V${Y}`}else if(type===1)o=`M${x} ${Y}V${t}L${x+w/2} ${t-70}L${x+w} ${t}V${Y}`;else o=`M${x} ${Y}V${t}C${x} ${t-30} ${x+w*.3} ${t-40} ${x+w*.35} ${t-60}H${x+w*.65}C${x+w*.7} ${t-40} ${x+w} ${t-30} ${x+w} ${t}V${Y}`;
  push('o',o);push('d',winGrid(x+6,t+16,w-12,h-60,3,Math.max(2,Math.round(h/60)),9,22)+R(x+w/2-8,Y-34,16,34));push('h',`M${x} ${t+8}H${x+w}`)};
 let x=10;const ws=[58,66,52,70,60,56,64,62];ws.forEach((w,i)=>{town(x,w,200+((i*53)%120),i%3);x+=w});
 // warehouse
 x+=20;{const w=220,h=360,t=Y-h;push('o',`M${x} ${Y}V${t}L${x+w/2} ${t-90}L${x+w} ${t}V${Y}`);push('l',`M${x+w/2} ${t-60}V${t-20}H${x+w/2+40}M${x+w/2+34} ${t-20}V${t+10}`);let doors='';for(let j=0;j<5;j++)doors+=R(x+w/2-16,t+20+j*64,32,46);push('d',doors+winGrid(x+10,t+20,60,320,2,5,14,30)+winGrid(x+w-70,t+20,60,320,2,5,14,30));let br='';for(let y=t+8;y<Y;y+=10)br+=`M${x} ${y}H${x+8}M${x+w-8} ${y}H${x+w}`;push('h',br);x+=w+40}
 // mosque
 {const hx=x+40,hw=200,ht=Y-150;push('o',R(hx,ht,hw,150));push('o',`M${hx+40} ${ht}A60 70 0 0 1 ${hx+160} ${ht}`);push('l',`M${hx+100} ${ht-70}V${ht-96}`+circ(hx+100,ht-100,5));[x,x+270].forEach(mx=>{push('o',`M${mx} ${Y}V${Y-380}H${mx+22}V${Y}M${mx} ${Y-380}L${mx+11} ${Y-440}L${mx+22} ${Y-380}`);push('l',`M${mx-6} ${Y-300}H${mx+28}M${mx-6} ${Y-200}H${mx+28}`)});let w='';for(let i=0;i<5;i++)w+=arch(hx+28+i*36,Y-40,9,Y-90)+'Z';push('d',w);x+=330}
 // gallery
 {const w=300,t=Y-140;let v='',a='';for(let i=0;i<6;i++){const vx=x+i*50;v+=`M${vx} ${t}A25 22 0 0 1 ${vx+50} ${t}`;a+=arch(vx+25,Y-10,16,t+46)+'Z'}push('o',`M${x} ${Y}V${t}H${x+w}V${Y}`);push('o',v);push('d',a);push('h',`M${x} ${t+8}H${x+w}M${x} ${t+14}H${x+w}`);x+=w+40}
 // library
 {const w=210,h=270,t=Y-h;push('o',R(x,t,w,h));push('l',R(x+75,t-18,60,18));push('d',winGrid(x+8,t+12,w-16,h-50,6,6,16,18));push('g',`M${x+20} ${Y}V${Y-26}M${x+50} ${Y}V${Y-26}M${x+80} ${Y}V${Y-26}M${x+130} ${Y}V${Y-26}M${x+160} ${Y}V${Y-26}M${x+190} ${Y}V${Y-26}`);x+=w+50}
 // towers & cranes
 const tower=(x,w,h,fl=14)=>{const t=Y-h;push('o',R(x,t,w,h));let f='';for(let y=t+fl;y<Y;y+=fl)f+=`M${x} ${y}H${x+w}`;push('h',f);let v='';for(let vx=x+w/5;vx<x+w;vx+=w/5)v+=`M${r1(vx)} ${t}V${Y}`;push('g',v)};
 tower(x,110,520);tower(x+130,90,640,12);
 const crane=(cx,h,jl,cl)=>{const t=Y-h;let m=`M${cx-6} ${Y}V${t}M${cx+6} ${Y}V${t}`,z='';for(let y=Y;y>t;y-=14)z+=`M${cx-6} ${y}L${cx+6} ${y-14}`;push('l',m);push('h',z);push('l',`M${cx-cl} ${t}H${cx+jl}M${cx-cl} ${t+8}H${cx+jl}M${cx} ${t}V${t-34}L${cx+jl*.6} ${t}M${cx} ${t-34}L${cx-cl} ${t}`);push('d',R(cx-cl,t+8,cl*.4,18)+`M${cx+jl*.7} ${t+8}V${t+120}M${cx+jl*.7-6} ${t+120}H${cx+jl*.7+6}`)};
 crane(x+175,800,260,90);tower(x+240,120,460,15);crane(x+420,700,200,70);x+=500;
 // quay end, bridge
 push('o',`M0 ${Y}H${x}`,1600);
 {const bx=x,bw=560,dy=Y-46;push('o',`M${bx} ${dy}H${bx+bw}M${bx} ${dy+10}H${bx+bw}`);let a='';for(let i=0;i<3;i++){const ax=bx+20+i*180;a+=`M${ax} ${Y+60}A80 96 0 0 1 ${ax+160} ${Y+60}`}push('l',a);let rail='';for(let rx=bx;rx<bx+bw;rx+=14)rail+=`M${rx} ${dy}V${dy-14}`;push('h',rail+`M${bx} ${dy-14}H${bx+bw}`);push('T',person(bx+120,dy,2)+person(bx+300,dy,2)+person(bx+316,dy,1.8));x=bx+bw}
 push('o',`M${x} ${Y}H${W}`);
 const ws2=[60,54,66,58,62,56,70,60];ws2.forEach((w,i)=>{if(x+w>W)return;town(x,w,180+((i*37)%110),(i+1)%3);x+=w});
 // water + boats + reflections
 let wv='';for(let k=0;k<8;k++){const y=Y+24+k*24;wv+=`M0 ${y}`;for(let wx=0;wx<W;wx+=160)wv+=`Q${wx+40} ${y-4-rnd()*3} ${wx+80} ${y}T${wx+160} ${y}`}push('h',wv,1400);
 let rf='';for(let k=0;k<120;k++){const rx=rnd()*2200,ry=Y+14+rnd()*120;rf+=`M${r1(rx)} ${r1(ry)}H${r1(rx+10+rnd()*30)}`}push('h',rf,1000);
 const boat=(bx,by,s)=>{push('l',`M${bx} ${by}L${bx+12*s} ${by+16*s}H${bx+88*s}L${bx+100*s} ${by}Z`);push('d',`M${bx+40*s} ${by}V${by-90*s}L${bx+40*s+46*s} ${by-6*s}H${bx+40*s}M${bx+36*s} ${by}V${by-60*s}L${bx+2*s} ${by-6*s}`)};
 boat(2300,Y+70,1.2);boat(2650,Y+110,.9);boat(1050,Y+90,1);boat(1500,Y+60,.7);
 $('#city').innerHTML=`<svg viewBox="0 0 ${W} ${H}" preserveAspectRatio="xMidYMax slice" role="img" aria-label="Ink drawing of a harbour city: gabled townhouses and brick warehouses on the quay, a mosque with a dome and minarets, a vaulted gallery, a stone library, new towers with two cranes at work, a bridge and boats on the water"><g>${out.join('')}</g></svg>`;
 io($('#city svg'),s=>$('g',s).classList.add('on'),.15)}

/* ---------- quotes ---------- */
const Q=[['Our architects drew the library a hundred times before they drew it once. Linework is what made a hundred versions possible in a single month.','Ingrid Holm','Director, Kalkværket Library'],['It tested every way to stack seven trays before lunch. We spent the afternoon arguing about the good ones instead of drawing the bad ones.','Jonas Ek','Founder, Stakken Studios'],['Sixty volunteers built our bathing house from sheets Linework drew for people who had never held a saw. It still stands, and it still keeps us warm.','Lene Dahl','Chair, Hornbæk Winter Bathers']];
function mountQuotes(){let q=0,timer;const show=n=>{q=(n+Q.length)%Q.length;const f=$('#qfig');f.classList.remove('swap');void f.offsetWidth;f.classList.add('swap');
 f.innerHTML=`<blockquote><span>“</span>${Q[q][0]}<span>”</span></blockquote><figcaption><span>${Q[q][1]}<small>${Q[q][2]}</small></span></figcaption>`;$('#qn').textContent='0'+(q+1);
 $$('#qdots button').forEach((b,i)=>b.setAttribute('aria-pressed',i===q));clearInterval(timer);if(!RM)timer=setInterval(()=>show(q+1),8000)};
 $('#qdots').innerHTML=Q.map((_,i)=>`<button aria-label="Show quote ${i+1} of 3"><i></i></button>`).join('');
 $$('#qdots button').forEach((b,i)=>b.onclick=()=>show(i));$('#qprev').onclick=()=>show(q-1);$('#qnext').onclick=()=>show(q+1);show(0)}

/* ---------- utilities & chrome ---------- */
function io(el,fn,th=.2){if(!el)return;const o=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){fn(e.target);o.unobserve(e.target)}}),{threshold:th});o.observe(el)}
function chrome(){const hdr=$('#hdr');const onS=()=>hdr.classList.toggle('solid',scrollY>24);onS();addEventListener('scroll',onS,{passive:true});
 const bt=$('#burger');bt.onclick=()=>{const o=document.body.classList.toggle('menu-open');bt.setAttribute('aria-expanded',o);document.body.style.overflow=o?'hidden':''};
 $$('#mnav a').forEach(a=>a.onclick=()=>{document.body.classList.remove('menu-open');bt.setAttribute('aria-expanded',false);document.body.style.overflow=''});
 $$('[data-reveal]').forEach(el=>io(el,e=>e.classList.add('in'),.15));
 $$('#stats dd').forEach(dd=>io(dd,()=>{const n=+dd.dataset.n,t0=performance.now();const f=t=>{const k=Math.min(1,(t-t0)/1400);dd.textContent=Math.round(n*(1-Math.pow(1-k,3)));if(k<1)requestAnimationFrame(f)};RM?dd.textContent=n:requestAnimationFrame(f)},.5));
 const secs=['work','process','studio','contact'].map(id=>document.getElementById(id));const nl=$$('.nav a');
 const so=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){nl.forEach(a=>a.classList.toggle('cur',a.getAttribute('href')==='#'+e.target.id))}}),{rootMargin:'-50% 0px -50% 0px'});secs.forEach(s=>so.observe(s));
 $$('[data-enquire]').forEach(b=>b.addEventListener('click',()=>{document.body.classList.remove('menu-open');document.body.style.overflow='';$('#form').classList.remove('done');$('#dlgE').showModal()}));
 $('#form').addEventListener('submit',e=>{e.preventDefault();e.target.classList.add('done')});
 $$('dialog').forEach(d=>{d.addEventListener('click',e=>{if(e.target===d||e.target.closest('[data-close]'))d.close()})})}

mountHero();mountSky();mountPv();mountProcess();mountFig();mountCity();mountQuotes();chrome();
})();
</script>
</body>
</html>
```

