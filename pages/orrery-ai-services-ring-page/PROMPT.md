INSTALANDING.AI · Orrery AI Services Ring Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Orrery AI Services Ring Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/orrery-ai-services-ring-page

orrery-services-ring.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Orrery AI Services Ring Page
  slug     orrery-ai-services-ring-page
  prompt   https://instalanding.ai/p/orrery-ai-services-ring-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/orrery-ai-services-ring-page
  license  Fictional brand ("Orrery"); every service, figure and scene is invented.
           Replace names and copy before shipping. All nine worlds are painted on canvas at load; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --accent (an @property colour that eases to each world's accent),
            --ink, --dim, --faint, --s (lens size), --cy (ring top); Instrument Serif, Geist and Geist Mono
  sections  nav, ring (the full-screen carousel stage), hud, about and contact sheets (each carries data-section)
  scripts   one IIFE, no libraries: a canvas toolkit (seeded noise, ridges, glows, reflections, bloom); nine painters
            (city, aurora, synthwave horizon, reef, orbit, blossom, circuit, crystal hollow, frontier) that paint a
            1600x1000 still each, plus a live animation layer per world; nine glass lenses on a turning ring with an
            SVG displacement filter; drag, wheel, arrows and auto-advance; a split-letter title; sheets and a form
  assets    no image files; the stills are encoded to blob URLs while the loader counts through them

  ADAPTING
  - Each service is one entry in WORLDS: name, sub, tag, accent, paint (the still), anim (the live layer) and icon.
  - The ring geometry is in layout(); AUTO sets the auto-advance interval.
  - prefers-reduced-motion: no auto-advance or grain, and the live layer draws a single frame.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Orrery — Nine AI services, one ring</title>
<meta name="description" content="Orrery is one AI platform with nine specialist services — forecasting, monitoring, generative, search, vision, coaching, code, documents and research — on a single turning ring.">
<meta name="theme-color" content="#050505">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Instrument+Serif:ital@0;1&family=Geist:wght@300;400;500&family=Geist+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
@property --accent{syntax:'<color>';inherits:true;initial-value:#2ee6ff}
:root{
  --accent:#2ee6ff;--ink:#f5f2ec;--dim:rgba(245,242,236,.6);--faint:rgba(245,242,236,.36);
  --ease:cubic-bezier(.16,1,.3,1);--s:150px;--cy:70vh;
  transition:--accent 1.6s cubic-bezier(.4,0,.2,1);
}
*{box-sizing:border-box;margin:0;padding:0}
html,body{height:100%;background:#050505;color:var(--ink);overflow:hidden;
  font-family:Geist,ui-sans-serif,system-ui,-apple-system,sans-serif;-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale}
::selection{background:var(--accent);color:#050505}
button{font:inherit;color:inherit;background:none;border:0;cursor:pointer}
a{color:inherit;text-decoration:none}

/* ───────── Stage ───────── */
#stage{position:fixed;inset:0;overflow:hidden;user-select:none;-webkit-user-select:none;touch-action:pan-y;cursor:grab}
#stage.dragging{cursor:grabbing}
.bgwrap{position:absolute;inset:-4%;will-change:transform}
.bg{position:absolute;inset:0;background-size:cover;background-position:50% 50%;opacity:0;transform:scale(1.14);
  transition:opacity 1.8s var(--ease),transform 10s cubic-bezier(.2,.6,.2,1)}
.bg.on{opacity:1;transform:scale(1.02)}
.live{position:absolute;inset:0;width:100%;height:100%;display:block;pointer-events:none}
.shade{position:absolute;inset:0;pointer-events:none;
  background:
   radial-gradient(130% 95% at 50% 42%,transparent 40%,rgba(0,0,0,.45) 78%,rgba(0,0,0,.84)),
   linear-gradient(to bottom,rgba(0,0,0,.5),transparent 20%,transparent 54%,rgba(0,0,0,.7) 100%)}
.glow{position:absolute;left:0;top:0;width:1000px;height:1000px;margin:-500px 0 0 -500px;border-radius:50%;pointer-events:none;
  background:radial-gradient(closest-side,color-mix(in srgb,var(--accent) 50%,transparent),transparent 72%);
  mix-blend-mode:screen;opacity:0;transition:opacity 2s var(--ease)}
.ready .glow{opacity:.5}
.vis-defs{position:absolute;width:0;height:0;overflow:hidden}

.track,.arcring{position:absolute;border-radius:50%;pointer-events:none;opacity:0;transition:opacity 2s var(--ease) .4s}
.ready .track,.ready .arcring{opacity:1}
.track::before{content:'';position:absolute;inset:0;border-radius:50%;border:1px solid rgba(255,255,255,.14)}
.track::after{content:'';position:absolute;inset:-16px;border-radius:50%;
  background:repeating-conic-gradient(rgba(255,255,255,.34) 0 .14deg,transparent .14deg 1.6deg);
  -webkit-mask:radial-gradient(farthest-side,transparent calc(100% - 6px),#000 calc(100% - 5px));
          mask:radial-gradient(farthest-side,transparent calc(100% - 6px),#000 calc(100% - 5px));opacity:.45}
.track i{position:absolute;inset:-16px;border-radius:50%;
  background:repeating-conic-gradient(rgba(255,255,255,.7) 0 .3deg,transparent .3deg 40deg);
  -webkit-mask:radial-gradient(farthest-side,transparent calc(100% - 11px),#000 calc(100% - 10px));
          mask:radial-gradient(farthest-side,transparent calc(100% - 11px),#000 calc(100% - 10px));opacity:.6}
.arcring{background:conic-gradient(from -30deg,transparent,color-mix(in srgb,var(--accent) 90%,#fff) 30deg,transparent 60deg);
  -webkit-mask:radial-gradient(farthest-side,transparent calc(100% - 1.5px),#000 calc(100% - 1px));
          mask:radial-gradient(farthest-side,transparent calc(100% - 1.5px),#000 calc(100% - 1px));filter:drop-shadow(0 0 6px var(--accent))}

/* ───────── Lenses ───────── */
.orbit{position:absolute;inset:0}
.med{position:absolute;left:0;top:0;width:var(--s);height:var(--s);border-radius:50%;will-change:transform,opacity;cursor:pointer;opacity:0}
.med-face{position:absolute;inset:0;border-radius:50%;overflow:hidden;background:#0b0b0b;
  box-shadow:0 46px 80px -34px rgba(0,0,0,.95),0 14px 30px -14px rgba(0,0,0,.8)}
.med-img{position:absolute;inset:0;background-size:cover;filter:url(#vis-glass);transform-origin:50% 50%}
.med-base{position:absolute;inset:0;background-size:cover;transform-origin:50% 50%}
.med-emblem{position:absolute;left:50%;top:50%;width:44%;height:44%;margin:-22% 0 0 -22%;border-radius:50%;display:grid;place-items:center;pointer-events:none;
  background-color:#0a0a0d;background-image:var(--blur,none);background-size:cover;background-position:center;
  box-shadow:inset 0 0 0 1px rgba(255,255,255,.3),inset 0 1.5px 0 rgba(255,255,255,.55),inset 0 -8px 14px rgba(0,0,0,.45),0 8px 20px -8px rgba(0,0,0,.8),0 0 0 3px rgba(0,0,0,.16);
  transition:transform .9s var(--ease)}
.med-emblem::before{content:'';position:absolute;inset:0;border-radius:50%;background:radial-gradient(120% 90% at 50% 0%,rgba(255,255,255,.3),rgba(255,255,255,.04) 46%,rgba(0,0,0,.3) 100%)}
.med-emblem::after{content:'';position:absolute;inset:-7px;border-radius:50%;
  background:repeating-conic-gradient(color-mix(in srgb,var(--c) 70%,#fff) 0 1.2deg,transparent 1.2deg 15deg);
  -webkit-mask:radial-gradient(farthest-side,transparent calc(100% - 3px),#000 calc(100% - 2.5px));mask:radial-gradient(farthest-side,transparent calc(100% - 3px),#000 calc(100% - 2.5px));
  opacity:.5;transition:opacity .9s,transform 1.4s var(--ease)}
.med-emblem svg{position:relative;width:58%;height:58%;fill:none;stroke:#fff;stroke-width:1.4;stroke-linecap:round;stroke-linejoin:round;overflow:visible;
  filter:drop-shadow(0 0 2.5px var(--c)) drop-shadow(0 0 7px color-mix(in srgb,var(--c) 65%,transparent)) drop-shadow(0 1px 1px rgba(0,0,0,.6))}
.med.on .med-emblem{transform:scale(1.06)}
.med.on .med-emblem::after{opacity:1;transform:rotate(30deg)}
.med-tint{position:absolute;inset:0;border-radius:50%;background:radial-gradient(circle at 50% 50%,transparent 55%,rgba(0,0,0,.35) 100%)}
.med-rim{position:absolute;inset:0;border-radius:50%;pointer-events:none;
  box-shadow:inset 0 0 0 1px rgba(255,255,255,.24),inset 0 2px 1px rgba(255,255,255,.6),inset 0 -4px 10px rgba(255,255,255,.2),inset 0 0 26px rgba(0,0,0,.4);
  background:
   radial-gradient(80% 55% at var(--lx,34%) var(--ly,10%),rgba(255,255,255,.46),rgba(255,255,255,.07) 40%,transparent 62%),
   radial-gradient(70% 38% at 50% 106%,rgba(255,255,255,.26),transparent 70%)}
.med-rim::after{content:'';position:absolute;inset:5%;border-radius:50%;border-top:1.5px solid rgba(255,255,255,.75);filter:blur(.8px);opacity:.75;transform:rotate(var(--rr,-28deg))}
.med-halo{position:absolute;inset:-11px;border-radius:50%;border:1px solid color-mix(in srgb,var(--accent) 75%,transparent);
  box-shadow:0 0 50px -8px var(--accent),inset 0 0 20px -10px var(--accent);opacity:0;transform:scale(.9);transition:opacity .9s var(--ease),transform .9s var(--ease)}
.med.on .med-halo{opacity:1;transform:scale(1)}
.med:focus-visible{outline:none}
.med:focus-visible .med-halo{opacity:1}

/* ───────── Title ───────── */
.title{position:absolute;left:0;right:0;text-align:center;pointer-events:none;padding:0 24px;opacity:0;transition:opacity 1.4s var(--ease) .3s}
.ready .title{opacity:1}
.title::before{content:'';position:absolute;left:50%;top:50%;width:min(1100px,130vw);height:150%;transform:translate(-50%,-50%);z-index:-1;
  background:radial-gradient(closest-side,rgba(0,0,0,.42),rgba(0,0,0,.18) 55%,transparent);filter:blur(10px)}
.title.light::before{background:radial-gradient(closest-side,rgba(30,10,30,.55),rgba(30,10,30,.25) 55%,transparent)}
.name,.sub{text-shadow:0 2px 24px rgba(0,0,0,.55),0 0 2px rgba(0,0,0,.35)}
.name{font-family:'Instrument Serif',Georgia,serif;font-weight:400;font-size:clamp(46px,8.6vw,142px);line-height:.92;letter-spacing:-.028em;
  margin:0 0 18px;white-space:nowrap}
.name .ch{display:inline-block;animation:chIn 1.25s var(--ease) both}
.name .it{font-style:italic;color:rgba(245,242,236,.8)}
.name.out .ch{animation:chOut .38s cubic-bezier(.5,0,.75,0) both}
@keyframes chIn{from{opacity:0;transform:translateY(.42em) rotate(5deg);filter:blur(12px)}}
@keyframes chOut{to{opacity:0;transform:translateY(-.22em);filter:blur(10px)}}
.sub{font:400 12.5px/1.4 'Geist Mono',monospace;letter-spacing:.3em;text-transform:uppercase;color:var(--dim);transition:opacity .5s,transform .8s var(--ease)}
.sub.out{opacity:0;transform:translateY(6px)}
.tag{display:inline-flex;align-items:center;gap:8px;margin-top:14px;padding:7px 12px;border-radius:999px;font:500 9.5px/1 'Geist Mono',monospace;letter-spacing:.26em;text-transform:uppercase;
  color:var(--ink);background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.14);-webkit-backdrop-filter:blur(12px);backdrop-filter:blur(12px);transition:opacity .5s}
.tag::before{content:'';width:5px;height:5px;border-radius:50%;background:var(--accent);box-shadow:0 0 8px var(--accent)}
.tag.out{opacity:0}

/* ───────── Chevrons ───────── */
.chev{position:absolute;top:var(--cy);width:60px;height:60px;margin-top:-30px;border-radius:50%;display:grid;place-items:center;z-index:5;
  background:linear-gradient(160deg,rgba(255,255,255,.14),rgba(255,255,255,.03));border:1px solid rgba(255,255,255,.16);
  -webkit-backdrop-filter:blur(16px) saturate(170%);backdrop-filter:blur(16px) saturate(170%);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.3),0 18px 40px -14px rgba(0,0,0,.7);
  transition:transform .5s var(--ease),background .4s,border-color .4s,opacity 1.2s;opacity:0}
.ready .chev{opacity:1}
.chev:hover{transform:scale(1.07);border-color:color-mix(in srgb,var(--accent) 60%,transparent)}
.chev:active{transform:scale(.96)}
.chev svg{transition:transform .5s var(--ease)}
.chev-l:hover svg{transform:translateX(-2px)}.chev-r:hover svg{transform:translateX(2px)}
.chev-l{left:clamp(14px,5vw,80px)}.chev-r{right:clamp(14px,5vw,80px)}

/* ───────── Nav ───────── */
.nav{position:fixed;top:0;left:0;right:0;z-index:40;display:flex;align-items:center;justify-content:space-between;padding:26px clamp(18px,3.4vw,44px)}
.mark{display:flex;align-items:center;gap:12px;font-family:'Instrument Serif',serif;font-size:27px;letter-spacing:-.01em}
.mark svg{width:24px;height:24px}
.mark .ringdot{transform-origin:12px 12px;animation:spin 18s linear infinite}
@keyframes spin{to{transform:rotate(360deg)}}
.links{display:flex;gap:6px;padding:5px;border-radius:999px;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.1);
  -webkit-backdrop-filter:blur(18px) saturate(160%);backdrop-filter:blur(18px) saturate(160%)}
.link{position:relative;font:500 11px/1 'Geist Mono',monospace;letter-spacing:.2em;text-transform:uppercase;padding:11px 16px;border-radius:999px;color:var(--dim);transition:color .3s,background .3s}
.link:hover{color:var(--ink);background:rgba(255,255,255,.06)}
.link.active{color:var(--ink);background:rgba(255,255,255,.1)}
.toggle{display:none;font:500 11px/1 'Geist Mono',monospace;letter-spacing:.22em;text-transform:uppercase;padding:12px 18px;border-radius:999px;
  background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.14);-webkit-backdrop-filter:blur(16px);backdrop-filter:blur(16px)}
.takeover{position:fixed;inset:0;z-index:35;display:flex;flex-direction:column;justify-content:center;padding:0 28px;
  background:rgba(6,6,6,.72);-webkit-backdrop-filter:blur(30px) saturate(140%);backdrop-filter:blur(30px) saturate(140%);
  opacity:0;visibility:hidden;transition:opacity .6s var(--ease),visibility .6s}
.takeover.open{opacity:1;visibility:visible}
.takeover a{display:flex;align-items:baseline;gap:18px;font-family:'Instrument Serif',serif;font-size:64px;line-height:1.1;letter-spacing:-.02em;opacity:0;transform:translateY(24px)}
.takeover.open a{animation:up .9s var(--ease) both}
.takeover a span{font:500 11px 'Geist Mono',monospace;letter-spacing:.2em;color:var(--faint)}
.takeover p{margin-top:40px;font:400 11px 'Geist Mono',monospace;letter-spacing:.3em;text-transform:uppercase;color:var(--faint)}
@keyframes up{to{opacity:1;transform:none}}

/* ───────── HUD ───────── */
.hud{position:fixed;left:0;right:0;bottom:0;z-index:30;display:grid;grid-template-columns:1fr auto 1fr;align-items:end;gap:20px;
  padding:0 clamp(18px,3.4vw,44px) calc(24px + env(safe-area-inset-bottom));opacity:0;transition:opacity 1.4s var(--ease) .6s;pointer-events:none}
.ready .hud{opacity:1}
.hud>*{pointer-events:auto}
.count{display:flex;align-items:baseline;gap:12px}
.count .cur{font-family:'Instrument Serif',serif;font-size:44px;line-height:.8;letter-spacing:-.02em;min-width:1.2em}
.count .tot{font:500 11px 'Geist Mono',monospace;letter-spacing:.2em;color:var(--faint)}
.count .sep{width:28px;height:1px;background:rgba(255,255,255,.3);transform:translateY(-6px)}
.segs{display:flex;gap:6px}
.seg{position:relative;width:30px;height:20px}
.seg::before,.seg i{content:'';position:absolute;left:0;right:0;top:9px;height:2px;border-radius:2px;background:rgba(255,255,255,.18)}
.seg i{right:auto;width:calc(var(--p,0)*100%);background:var(--ink)}
.seg.on::before{background:rgba(255,255,255,.3)}
.seg.on i{background:var(--accent);box-shadow:0 0 10px var(--accent)}
.seg.past i{width:100%;background:rgba(255,255,255,.55)}

.grain{position:fixed;inset:-50%;z-index:50;pointer-events:none;opacity:.07;mix-blend-mode:overlay;animation:grain 1s steps(6) infinite}
@keyframes grain{0%{transform:translate(0,0)}20%{transform:translate(-3%,2%)}40%{transform:translate(2%,-4%)}60%{transform:translate(-4%,-1%)}80%{transform:translate(3%,3%)}100%{transform:translate(0,0)}}

/* ───────── Sheets ───────── */
.sheet{position:fixed;inset:0;z-index:45;display:grid;place-items:center;padding:96px 20px 40px;overflow:auto;
  background:rgba(4,4,4,.42);-webkit-backdrop-filter:blur(28px) saturate(140%);backdrop-filter:blur(28px) saturate(140%);
  opacity:0;visibility:hidden;transition:opacity .7s var(--ease),visibility .7s}
.sheet.open{opacity:1;visibility:visible}
.card{position:relative;width:100%;max-width:680px;padding:clamp(28px,5vw,56px);border-radius:30px;
  background:linear-gradient(155deg,rgba(255,255,255,.11),rgba(255,255,255,.025) 60%);border:1px solid rgba(255,255,255,.14);
  box-shadow:inset 0 1px 0 rgba(255,255,255,.22),0 60px 120px -40px rgba(0,0,0,.9);transform:translateY(26px) scale(.98);transition:transform .9s var(--ease)}
.sheet.open .card{transform:none}
.card .k{font:500 11px 'Geist Mono',monospace;letter-spacing:.3em;text-transform:uppercase;color:var(--accent)}
.card h3{font-family:'Instrument Serif',serif;font-weight:400;font-size:clamp(40px,6vw,64px);line-height:1;letter-spacing:-.025em;margin:16px 0 22px}
.card h3 em{color:var(--dim)}
.card p{color:var(--dim);font-size:15.5px;line-height:1.7;font-weight:300;max-width:54ch}
.card p+p{margin-top:14px}
.close{position:absolute;top:20px;right:20px;width:42px;height:42px;border-radius:50%;display:grid;place-items:center;border:1px solid rgba(255,255,255,.16);transition:transform .5s var(--ease),background .3s}
.close:hover{transform:rotate(90deg);background:rgba(255,255,255,.08)}
.stats{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;margin-top:34px;border-radius:16px;overflow:hidden;background:rgba(255,255,255,.1)}
.stats div{background:rgba(10,10,10,.55);padding:18px}
.stats b{display:block;font-family:'Instrument Serif',serif;font-weight:400;font-size:34px;line-height:1}
.stats span{font:500 10px 'Geist Mono',monospace;letter-spacing:.2em;text-transform:uppercase;color:var(--faint)}
.worlds{display:flex;flex-wrap:wrap;gap:6px;margin-top:22px}
.worlds button{font:500 9.5px 'Geist Mono',monospace;letter-spacing:.2em;text-transform:uppercase;padding:8px 11px;border-radius:999px;border:1px solid rgba(255,255,255,.14);color:var(--dim);transition:color .3s,border-color .3s,background .3s}
.worlds button:hover{color:var(--ink);border-color:color-mix(in srgb,var(--accent) 60%,transparent);background:rgba(255,255,255,.05)}
form{display:grid;gap:12px;margin-top:26px}
.f{position:relative}
.f input,.f textarea{width:100%;padding:22px 16px 10px;border-radius:14px;border:1px solid rgba(255,255,255,.14);background:rgba(0,0,0,.25);color:var(--ink);font:300 15px Geist,sans-serif;outline:none;transition:border-color .3s,background .3s;resize:none}
.f textarea{height:120px}
.f select{width:100%;padding:22px 40px 10px 16px;border-radius:14px;border:1px solid rgba(255,255,255,.14);background:rgba(0,0,0,.25) url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='12' viewBox='0 0 24 24' fill='none' stroke='%23f5f2ec' stroke-width='2' stroke-linecap='round'%3E%3Cpath d='m6 9 6 6 6-6'/%3E%3C/svg%3E") no-repeat right 16px center;color:var(--ink);font:300 15px Geist,sans-serif;outline:none;-webkit-appearance:none;appearance:none}
.f select:focus{border-color:color-mix(in srgb,var(--accent) 70%,transparent)}
.f option{background:#111;color:#f5f2ec}
.f label{position:absolute;left:17px;top:9px;font:500 9.5px 'Geist Mono',monospace;letter-spacing:.22em;text-transform:uppercase;color:var(--faint)}
.f input:focus,.f textarea:focus{border-color:color-mix(in srgb,var(--accent) 70%,transparent);background:rgba(0,0,0,.35)}
.send{justify-self:start;display:inline-flex;align-items:center;gap:12px;margin-top:6px;padding:15px 22px;border-radius:999px;background:var(--ink);color:#080808;font:500 11px 'Geist Mono',monospace;letter-spacing:.22em;text-transform:uppercase;transition:transform .4s var(--ease),box-shadow .4s}
.send:hover{transform:translateY(-2px);box-shadow:0 14px 40px -12px var(--accent)}
.sent{display:none;font:500 11px 'Geist Mono',monospace;letter-spacing:.22em;text-transform:uppercase;color:var(--accent);margin-top:18px}

/* ───────── Loader ───────── */
#loader{position:fixed;inset:0;z-index:100;background:#050505;display:grid;place-items:center;text-align:center;transition:opacity 1.2s var(--ease),visibility 1.2s}
#loader.done{opacity:0;visibility:hidden}
.ld-mark{font-family:'Instrument Serif',serif;font-size:clamp(44px,7vw,72px);letter-spacing:-.02em;line-height:1}
.ld-mark span{display:inline-block;animation:chIn 1.4s var(--ease) both}
.ld-bar{width:200px;height:1px;background:rgba(255,255,255,.12);margin:26px auto 16px;overflow:hidden}
.ld-bar i{display:block;height:100%;width:0;background:linear-gradient(90deg,rgba(255,255,255,.4),#fff);transition:width .5s var(--ease)}
.ld-txt{font:500 10.5px 'Geist Mono',monospace;letter-spacing:.3em;text-transform:uppercase;color:var(--faint)}

@media (max-width:760px){
  .links{display:none}.toggle{display:block}
  .hud{grid-template-columns:auto 1fr}
  .segs{justify-self:end}
  .seg{width:18px}
  .chev{width:48px;height:48px;margin-top:-24px}
  .stats b{font-size:26px}
  .tag{display:none}
}
@media (prefers-reduced-motion:reduce){
  .bg{transition:opacity 1s}.grain,.mark .ringdot{animation:none}
}
</style>
</head>
<body>

<div id="loader" aria-hidden="true">
  <div>
    <div class="ld-mark" id="ldMark"></div>
    <div class="ld-bar"><i id="ldBar"></i></div>
    <div class="ld-txt" id="ldTxt">Calibrating models</div>
  </div>
</div>

<header class="nav" data-section="nav">
  <a class="mark" href="#" aria-label="Orrery, home" data-go="home">
    <svg viewBox="0 0 24 24" fill="none" aria-hidden="true">
      <circle cx="12" cy="12" r="9.5" stroke="currentColor" stroke-opacity=".55"/>
      <g class="ringdot"><circle cx="12" cy="2.5" r="2.2" fill="currentColor"/></g>
      <circle cx="12" cy="12" r="3" stroke="currentColor"/>
    </svg>
    Orrery
  </a>
  <nav class="links" aria-label="Primary">
    <a class="link active" href="#" data-go="home" aria-current="page">Services</a>
    <a class="link" href="#about" data-go="about">Platform</a>
    <a class="link" href="#contact" data-go="contact">Contact</a>
  </nav>
  <button class="toggle" type="button" aria-expanded="false" aria-controls="takeover" id="toggle">Menu</button>
</header>

<div class="takeover" id="takeover" aria-hidden="true">
  <a href="#" data-go="home" style="animation-delay:.06s"><span>01</span>Services</a>
  <a href="#about" data-go="about" style="animation-delay:.13s"><span>02</span>Platform</a>
  <a href="#contact" data-go="contact" style="animation-delay:.2s"><span>03</span>Contact</a>
  <p>Nine intelligences, one ring</p>
</div>

<main id="stage" data-section="ring" aria-roledescription="carousel" aria-label="Orrery services">
  <div class="bgwrap" id="bgwrap" aria-hidden="true"></div>
  <div class="shade" aria-hidden="true"></div>
  <div class="glow" id="glow" aria-hidden="true"></div>

  <svg class="vis-defs" aria-hidden="true" focusable="false">
    <defs>
      <filter id="vis-glass" filterUnits="userSpaceOnUse" primitiveUnits="userSpaceOnUse" x="0" y="0" width="150" height="150" color-interpolation-filters="sRGB">
        <feImage id="lensImg" x="0" y="0" width="150" height="150" preserveAspectRatio="none" result="map"/>
        <feDisplacementMap in="SourceGraphic" in2="map" scale="20" xChannelSelector="R" yChannelSelector="G" result="dr"/>
        <feColorMatrix in="dr" type="matrix" values="1 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0 0 0 1 0" result="r"/>
        <feDisplacementMap in="SourceGraphic" in2="map" scale="24" xChannelSelector="R" yChannelSelector="G" result="dg"/>
        <feColorMatrix in="dg" type="matrix" values="0 0 0 0 0  0 1 0 0 0  0 0 0 0 0  0 0 0 1 0" result="g"/>
        <feDisplacementMap in="SourceGraphic" in2="map" scale="28" xChannelSelector="R" yChannelSelector="G" result="db"/>
        <feColorMatrix in="db" type="matrix" values="0 0 0 0 0  0 0 0 0 0  0 0 1 0 0  0 0 0 1 0" result="b"/>
        <feBlend in="r" in2="g" mode="screen" result="rg"/>
        <feBlend in="rg" in2="b" mode="screen"/>
      </filter>
    </defs>
  </svg>

  <div class="track" id="track"><i></i></div>
  <div class="arcring" id="arcring"></div>
  <div class="orbit" id="orbit"></div>

  <div class="title" id="title" aria-live="polite">
    <h1 class="name" id="name"></h1>
    <div class="sub" id="sub"></div>
    <div class="tag" id="tag"></div>
  </div>

  <button type="button" class="chev chev-l" id="prev" aria-label="Rotate left">
    <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m15 18-6-6 6-6"/></svg>
  </button>
  <button type="button" class="chev chev-r" id="next" aria-label="Rotate right">
    <svg width="22" height="22" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m9 18 6-6-6-6"/></svg>
  </button>
</main>

<div class="hud" data-section="hud">
  <div class="count"><span class="cur" id="cur">01</span><span class="sep"></span><span class="tot">09</span></div>
  <div class="segs" id="segs" role="tablist" aria-label="Worlds"></div>
</div>

<section class="sheet" id="about" data-section="about" aria-hidden="true" aria-label="Platform">
  <div class="card">
    <button class="close" type="button" data-go="home" aria-label="Close">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg>
    </button>
    <div class="k">Platform</div>
    <h3>One intelligence, <em>nine disciplines.</em></h3>
    <p>Orrery is a single AI platform built from nine specialist services. Each one is trained deep on a single job: forecasting demand, catching anomalies, generating on-brand creative, searching what your team knows, reading the planet from orbit, coaching people, shipping code, reading documents and accelerating research.</p>
    <p>They share one account, one API and one security model, so a signal caught by one service can brief another. Turn the ring to meet each of them, or pick one below.</p>
    <div class="stats">
      <div><b>9</b><span>Services</span></div>
      <div><b>1</b><span>Platform</span></div>
      <div><b>1</b><span>API key</span></div>
    </div>
    <div class="worlds" id="worldList"></div>
  </div>
</section>

<section class="sheet" id="contact" data-section="contact" aria-hidden="true" aria-label="Contact">
  <div class="card">
    <button class="close" type="button" data-go="home" aria-label="Close">
      <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg>
    </button>
    <div class="k">Contact</div>
    <h3>Start a pilot, <em>pick your service.</em></h3>
    <p>Tell us what you're working on and which service fits. We'll come back with a scoped pilot on your own data.</p>
    <form id="form">
      <div class="f"><label for="fn">Name</label><input id="fn" required autocomplete="name"></div>
      <div class="f"><label for="fe">Work email</label><input id="fe" type="email" required autocomplete="email"></div>
      <div class="f"><label for="fs">Service</label><select id="fs"></select></div>
      <div class="f"><label for="fm">What are you working on?</label><textarea id="fm" required></textarea></div>
      <button class="send" type="submit">Send
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"><path d="M5 12h14M13 6l6 6-6 6"/></svg>
      </button>
    </form>
    <div class="sent" id="sent">Received — we'll be in touch with a pilot plan.</div>
  </div>
</section>

<div class="grain" id="grain" aria-hidden="true"></div>

<script>
(() => {
'use strict';
const TAU=Math.PI*2, WW=1600, HH=1000;

/* ════════════════════ Toolkit ════════════════════ */
function rng(seed){return function(){seed|=0;seed=seed+0x6D2B79F5|0;let t=Math.imul(seed^seed>>>15,1|seed);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296}}
function noise1(seed){const r=rng(seed),p=new Float32Array(1024);for(let i=0;i<1024;i++)p[i]=r();
  return x=>{const i=Math.floor(x),f=x-i,u=f*f*(3-2*f);const a=p[i&1023],b=p[(i+1)&1023];return a+(b-a)*u}}
function fbm(n,x,oct){let v=0,a=.5,f=1;for(let i=0;i<oct;i++){v+=a*n(x*f+i*13.7);f*=2.03;a*=.5}return v}
const hash=n=>{const s=Math.sin(n*127.1+311.7)*43758.5453;return s-Math.floor(s)};
const wrap=(v,m)=>((v%m)+m)%m;
function lin(c,x0,y0,x1,y1,stops){const g=c.createLinearGradient(x0,y0,x1,y1);stops.forEach(s=>g.addColorStop(s[0],s[1]));return g}
function rad(c,x,y,r,stops,x0,y0){const g=c.createRadialGradient(x0??x,y0??y,0,x,y,r);stops.forEach(s=>g.addColorStop(s[0],s[1]));return g}
function glow(c,x,y,r,col,a=1){c.save();c.globalCompositeOperation='lighter';c.globalAlpha=a;c.fillStyle=rad(c,x,y,r,[[0,col],[1,'rgba(0,0,0,0)']]);c.fillRect(x-r,y-r,r*2,r*2);c.restore()}
function dot(c,x,y,r,col){c.fillStyle=col;c.beginPath();c.arc(x,y,r,0,TAU);c.fill()}
function rr(c,x,y,w,h,r){r=Math.min(r,w/2,h/2);c.beginPath();c.moveTo(x+r,y);c.arcTo(x+w,y,x+w,y+h,r);c.arcTo(x+w,y+h,x,y+h,r);c.arcTo(x,y+h,x,y,r);c.arcTo(x,y,x+w,y,r);c.closePath()}
const SPR={},SOFT={};
function mkSpr(rgb,core){const s=document.createElement('canvas');s.width=s.height=64;const x=s.getContext('2d'),g=x.createRadialGradient(32,32,0,32,32,32);
  if(core){g.addColorStop(0,'rgba(255,255,255,1)');g.addColorStop(.14,`rgba(${rgb},.9)`);g.addColorStop(.42,`rgba(${rgb},.22)`);g.addColorStop(1,`rgba(${rgb},0)`)}
  else{g.addColorStop(0,`rgba(${rgb},1)`);g.addColorStop(.5,`rgba(${rgb},.35)`);g.addColorStop(1,`rgba(${rgb},0)`)}
  x.fillStyle=g;x.fillRect(0,0,64,64);return s}
/* glowing point (additive) */
function sg(c,rgb,x,y,size,a){if(!(a>.003))return;const s=SPR[rgb]||(SPR[rgb]=mkSpr(rgb,1));const o=c.globalCompositeOperation,p=c.globalAlpha;
  c.globalCompositeOperation='lighter';c.globalAlpha=Math.min(1,a);c.drawImage(s,x-size/2,y-size/2,size,size);c.globalCompositeOperation=o;c.globalAlpha=p}
/* soft blob (current blend) */
function sf(c,rgb,x,y,w,h,a){if(!(a>.003))return;const s=SOFT[rgb]||(SOFT[rgb]=mkSpr(rgb,0));const p=c.globalAlpha;c.globalAlpha=Math.min(1,a);c.drawImage(s,x-w/2,y-h/2,w,h);c.globalAlpha=p}
function stars(c,W,H,n,seed,maxY=1,bright=1,tint='255,255,255'){const r=rng(seed);c.save();
  for(let i=0;i<n;i++){const x=r()*W,y=Math.pow(r(),1.3)*H*maxY,s=r();c.globalAlpha=(.15+.85*s*s)*bright;
    dot(c,x,y,s>.97?1.6:s>.85?1.05:.55,`rgb(${tint})`);if(s>.985)sg(c,tint,x,y,22,.6*bright)}
  c.restore()}
function ridge(c,W,H,o){const n=noise1(o.seed),st=o.step||4,pts=[];
  for(let x=-st;x<=W+st;x+=st){let v=fbm(n,x/W*o.freq+(o.off||0),o.oct||5);if(o.sharp)v=1-Math.abs(v*2-1);if(o.mesa)v=Math.min(v*1.5,o.mesa);pts.push([x,o.base*H-v*o.amp*H])}
  c.beginPath();c.moveTo(-st,H+4);for(const p of pts)c.lineTo(p[0],p[1]);c.lineTo(W+st,H+4);c.closePath();c.fillStyle=o.fill;c.fill();
  if(o.rim){c.save();c.globalCompositeOperation='lighter';c.beginPath();pts.forEach((p,i)=>i?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));
    c.strokeStyle=o.rim;c.lineWidth=o.rimW||1.4;c.stroke();c.restore()}
  const f=x=>pts[Math.max(0,Math.min(pts.length-1,Math.round((x+st)/st)))][1];f.pts=pts;return f}
function band(c,W,y,h,col){c.fillStyle=lin(c,0,y-h,0,y+h,[[0,'rgba(0,0,0,0)'],[.5,col],[1,'rgba(0,0,0,0)']]);c.fillRect(0,y-h,W,h*2)}
function rays(c,x,y,len,n,ang,spread,rgb,seed,maxA=.12){const r=rng(seed);c.save();c.globalCompositeOperation='lighter';
  for(let i=0;i<n;i++){const a=ang+(r()-.5)*spread,w=.006+r()*.03;
    c.fillStyle=rad(c,x,y,len,[[0,`rgba(${rgb},${maxA*(.3+r()*.7)})`],[1,`rgba(${rgb},0)`]]);
    c.beginPath();c.moveTo(x,y);c.lineTo(x+Math.cos(a-w)*len,y+Math.sin(a-w)*len);c.lineTo(x+Math.cos(a+w)*len,y+Math.sin(a+w)*len);c.closePath();c.fill()}
  c.restore()}
function pine(c,x,y,h,w,col){c.fillStyle=col;c.beginPath();
  for(let t=0;t<5;t++){const ty=y-h*(t/5)*.85,tw=w*(1-t/5*.78);c.moveTo(x-tw/2,ty);c.lineTo(x,ty-h*.36);c.lineTo(x+tw/2,ty)}
  c.fill();c.fillRect(x-w*.035,y-h*.08,w*.07,h*.14)}
function finish(c,W,H,a=.45){c.fillStyle=rad(c,W/2,H/2,Math.hypot(W,H)*.55,[[0,'rgba(0,0,0,0)'],[.6,'rgba(0,0,0,0)'],[1,`rgba(0,0,0,${a})`]]);c.fillRect(0,0,W,H)}
function abovePath(pts,W){const p=new Path2D();p.moveTo(-40,-40);p.lineTo(W+40,-40);for(let i=pts.length-1;i>=0;i--)p.lineTo(pts[i][0],pts[i][1]);p.closePath();return p}
function reflect(c,W,H,hz,seed,amp,dark){
  const tmp=document.createElement('canvas');tmp.width=W;tmp.height=Math.ceil(hz);tmp.getContext('2d').drawImage(c.canvas,0,0);
  c.save();c.beginPath();c.rect(0,hz,W,H-hz);c.clip();c.fillStyle='#000';c.fillRect(0,hz,W,H-hz);c.translate(0,hz*2);c.scale(1,-1);c.globalAlpha=.9;c.drawImage(tmp,0,0);c.restore();
  const t2=document.createElement('canvas');t2.width=W;t2.height=H;t2.getContext('2d').drawImage(c.canvas,0,0);const n=noise1(seed);
  for(let y=Math.floor(hz)+1;y<H;y+=2){const k=(y-hz)/(H-hz);const sh=Math.sin(y*.21+n(y*.05)*6)*(.5+k*amp);c.drawImage(t2,0,y,W,2,sh,y,W,2)}
  c.fillStyle=lin(c,0,hz,0,H,[[0,`rgba(${dark},.12)`],[1,`rgba(${dark},.82)`]]);c.fillRect(0,hz,W,H-hz)}
function post(c,W,H,amt){if(!amt)return;const mk=(w,h)=>{const s=document.createElement('canvas');s.width=w;s.height=h;return s};
  const a=mk(W/4,H/4),ax=a.getContext('2d');ax.drawImage(c.canvas,0,0,W/4,H/4);ax.globalCompositeOperation='multiply';ax.drawImage(a,0,0);ax.drawImage(a,0,0);
  const b=mk(W/16,H/16);b.getContext('2d').drawImage(a,0,0,W/16,H/16);
  const d=mk(W/4,H/4),dx=d.getContext('2d');dx.imageSmoothingQuality='high';dx.drawImage(b,0,0,W/4,H/4);
  c.save();c.globalCompositeOperation='screen';c.imageSmoothingQuality='high';c.globalAlpha=amt;c.drawImage(d,0,0,W,H);c.globalAlpha=amt*.5;c.drawImage(a,0,0,W,H);c.restore()}
function causticTile(){const n=192,cv=document.createElement('canvas');cv.width=cv.height=n;const x=cv.getContext('2d'),im=x.createImageData(n,n);
  for(let j=0;j<n;j++)for(let i=0;i<n;i++){const u=i/n*TAU,v=j/n*TAU;const s=Math.sin(u*2+Math.sin(v*3)*1.4)+Math.sin(v*2+Math.sin(u*3+1)*1.4)+Math.sin(u+v+Math.sin(u*2-v)*1.2+2);
    const val=Math.pow(Math.max(0,1-Math.abs(s)*.55),7),o=(j*n+i)*4;im.data[o]=200;im.data[o+1]=250;im.data[o+2]=255;im.data[o+3]=val*255}
  x.putImageData(im,0,0);return cv}
function vSprite(stops,w=4,h=256){const s=document.createElement('canvas');s.width=w;s.height=h;const x=s.getContext('2d');x.fillStyle=lin(x,0,0,0,h,stops);x.fillRect(0,0,w,h);return s}

/* ════════════════════ I · Metropolis ════════════════════ */
function pCity(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H,[[0,'#03020b'],[.28,'#0f0926'],[.52,'#26103c'],[.7,'#4c1450'],[.82,'#2a0a2c'],[1,'#06030a']]);c.fillRect(0,0,W,H);
  glow(c,W*.52,H*.72,W*.8,'rgba(255,50,160,.3)');glow(c,W*.14,H*.72,W*.42,'rgba(40,130,255,.22)');glow(c,W*.9,H*.62,W*.38,'rgba(0,220,255,.15)');
  const r=rng(101);c.globalCompositeOperation='lighter';
  for(let i=0;i<80;i++)sf(c,r()<.7?'190,60,200':'60,120,255',r()*W,H*(.03+r()*.5),240+r()*560,16+r()*46,.05+r()*.07);
  c.globalCompositeOperation='source-over';
  stars(c,W,H,120,108,.25,.35);
  const towers=o=>{const r=rng(o.seed);let x=o.x0??-30;const tips=[];
    while(x<(o.x1??W+30)){const w=o.w0+r()*(o.w1-o.w0),h=o.h0+r()*(o.h1-o.h0),top=o.base-h;
      c.fillStyle=o.col;c.fillRect(x,top,w,H-top+10);const k=r();
      if(k<.3)c.fillRect(x+w*.15,top-h*.06,w*.7,h*.06+1);
      else if(k<.42){c.beginPath();c.moveTo(x,top+.5);c.lineTo(x+w/2,top-w*.45);c.lineTo(x+w,top+.5);c.fill()}
      if(r()<o.ant){const ax=x+w*(.3+r()*.4),ah=20+r()*80;c.fillRect(ax-1,top-ah,2,ah);tips.push([ax,top-ah])}
      if(o.win){const cw=o.cw,ch=o.ch;for(let yy=top+6;yy<Math.min(H,o.base+60);yy+=ch)for(let xx=x+3;xx<x+w-cw*.6;xx+=cw){if(r()<o.p){const q=r(),a=o.win*(.3+r()*.7);
        c.fillStyle=q<.55?`rgba(255,196,130,${a})`:q<.85?`rgba(110,220,255,${a})`:`rgba(255,80,190,${a})`;c.fillRect(xx,yy,cw*.5,ch*.45)}}}
      if(o.edge){c.fillStyle=o.edge;c.fillRect(x+w-1.5,top,1.5,H-top)}
      x+=w+r()*o.gap}
    return tips};
  const far=towers({seed:102,base:H*.74,h0:90,h1:300,w0:26,w1:80,gap:4,col:'#22123a',win:.28,cw:5,ch:7,p:.12,ant:.15});
  band(c,W,H*.64,H*.12,'rgba(255,70,170,.12)');
  const mid=towers({seed:103,base:H*.86,h0:170,h1:470,w0:50,w1:140,gap:10,col:'#130922',win:.6,cw:6,ch:9,p:.15,ant:.3,edge:'rgba(255,90,200,.22)'});
  D.ants=far.concat(mid).slice(0,26);
  // the spire
  const mx=W*.5,mw=130,mt=H*.12;
  c.globalCompositeOperation='lighter';sf(c,'255,60,180',mx,mt+H*.3,mw*5,H*.9,.18);c.globalCompositeOperation='source-over';
  c.fillStyle=lin(c,mx-mw/2,0,mx+mw/2,0,[[0,'#0b0516'],[.5,'#1c0f30'],[1,'#080412']]);
  c.beginPath();c.moveTo(mx-mw/2,H);c.lineTo(mx-mw/2,mt+90);c.lineTo(mx-mw*.32,mt+30);c.lineTo(mx-8,mt-20);c.lineTo(mx+8,mt-20);c.lineTo(mx+mw*.32,mt+30);c.lineTo(mx+mw/2,mt+90);c.lineTo(mx+mw/2,H);c.closePath();c.fill();
  c.fillRect(mx-1.5,mt-120,3,102);D.spire=[mx,mt-120];
  c.globalCompositeOperation='lighter';
  [[-mw*.4,'255,60,180'],[mw*.4,'60,220,255'],[0,'255,240,255']].forEach(([dx,col])=>{c.fillStyle=lin(c,0,mt+90,0,H*.9,[[0,`rgba(${col},.95)`],[1,`rgba(${col},0)`]]);c.fillRect(mx+dx-1,mt+90,2,H*.75);sf(c,col,mx+dx,mt+H*.28,26,H*.5,.22)});
  for(let y=mt+130;y<H*.8;y+=46){c.fillStyle='rgba(255,120,220,.22)';c.fillRect(mx-mw/2+4,y,mw-8,1.5)}
  sg(c,'255,90,210',mx,mt+30,200,.55);D.ring=[mx,mt+70];
  c.globalCompositeOperation='source-over';
  band(c,W,H*.82,H*.08,'rgba(255,60,160,.14)');
  towers({seed:104,x0:-40,x1:W*.17,base:H*.98,h0:H*.6,h1:H*1.05,w0:90,w1:170,gap:0,col:'#06030b',win:.45,cw:9,ch:13,p:.06,ant:0,edge:'rgba(80,200,255,.28)'});
  towers({seed:105,x0:W*.8,x1:W+40,base:H*.98,h0:H*.55,h1:H*1.0,w0:90,w1:170,gap:0,col:'#06030b',win:.45,cw:9,ch:13,p:.06,ant:0,edge:'rgba(255,80,190,.25)'});
  const neon=(x,y,w,h,rgb,seed)=>{const r=rng(seed);c.save();c.globalCompositeOperation='lighter';sf(c,rgb,x+w/2,y+h/2,w*5,h*1.5,.3);
    c.strokeStyle=`rgba(${rgb},.95)`;c.lineWidth=2;c.strokeRect(x,y,w,h);c.fillStyle=`rgba(${rgb},.92)`;const gw=w*.56;
    for(let yy=y+9;yy<y+h-gw;yy+=gw*1.3){const g=r();c.fillRect(x+w*.22,yy,gw,2);if(g<.6)c.fillRect(x+w*.22+(g<.3?0:gw-2),yy,2,gw*.9);if(g>.35)c.fillRect(x+w*.22,yy+gw*.9,gw,2);if(g>.7)c.fillRect(x+w*.22,yy+gw*.45,gw,2)}
    c.restore()};
  neon(W*.04,H*.3,34,220,'255,60,170',1);neon(W*.125,H*.48,28,150,'0,230,255',2);neon(W*.935,H*.46,30,180,'255,170,60',3);
  const b={x:W*.815,y:H*.2,w:140,h:190};D.board=b;
  c.save();rr(c,b.x,b.y,b.w,b.h,6);c.clip();c.fillStyle=lin(c,b.x,b.y,b.x,b.y+b.h,[[0,'#26e4ff'],[.55,'#7a5cff'],[1,'#ff3ea5']]);c.fillRect(b.x,b.y,b.w,b.h);
  dot(c,b.x+b.w*.5,b.y+b.h*.36,34,'rgba(255,255,255,.85)');c.strokeStyle='rgba(255,255,255,.7)';c.lineWidth=2;
  for(let k=0;k<4;k++){c.beginPath();for(let xx=0;xx<=b.w;xx+=6){const yy=b.y+b.h*.68+k*12+Math.sin(xx*.08+k)*4;if(xx)c.lineTo(b.x+xx,yy);else c.moveTo(b.x,yy)}c.stroke()}
  c.fillStyle='rgba(0,0,0,.18)';for(let yy=b.y;yy<b.y+b.h;yy+=3)c.fillRect(b.x,yy,b.w,1);c.restore();
  c.globalCompositeOperation='lighter';sf(c,'120,160,255',b.x+b.w/2,b.y+b.h/2,b.w*3,b.h*2,.35);c.globalCompositeOperation='source-over';
  // maglev
  const ty=H*.655;D.trackY=ty;c.fillStyle='#050209';c.fillRect(0,ty,W,12);for(let x=120;x<W;x+=380)c.fillRect(x,ty+12,16,H);
  c.globalCompositeOperation='lighter';c.fillStyle='rgba(0,220,255,.7)';c.fillRect(0,ty+12,W,1.5);c.fillStyle='rgba(255,80,200,.35)';c.fillRect(0,ty,W,1);c.globalCompositeOperation='source-over';
  // wet street
  const sy=H*.9;c.fillStyle=lin(c,0,sy,0,H,[[0,'#0c0514'],[1,'#030106']]);c.fillRect(0,sy,W,H-sy);
  c.globalCompositeOperation='lighter';const r2=rng(106);
  for(let i=0;i<160;i++){const x=r2()*W,q=r2(),col=q<.5?'255,70,180':q<.8?'60,210,255':'255,190,110',len=30+r2()*110,w=1+r2()*5;
    c.fillStyle=lin(c,0,sy,0,sy+len,[[0,`rgba(${col},${.15+r2()*.3})`],[1,`rgba(${col},0)`]]);c.fillRect(x,sy,w,len)}
  c.fillStyle='rgba(255,150,220,.4)';c.fillRect(0,sy,W,1);c.globalCompositeOperation='source-over';
  band(c,W,H*.9,H*.05,'rgba(200,80,180,.15)');
  finish(c,W,H,.5);
}
function aCity(c,t,D,px){
  const W=WW,H=HH;
  sg(c,'255,40,80',D.spire[0],D.spire[1],40+12*Math.sin(t*3),.6+.4*Math.sin(t*3));
  D.ants.forEach((p,i)=>{const b=Math.sin(t*2.2+i*1.7);if(b>.6)sg(c,'255,50,60',p[0],p[1],18,(b-.6)*2.5)});
  // billboard
  const b=D.board,fl=.5+.5*Math.sin(t*1.3)*Math.sin(t*7.1);c.globalCompositeOperation='lighter';
  c.globalAlpha=.1+.1*fl;c.fillStyle='#8ff';c.fillRect(b.x,b.y,b.w,b.h);
  c.globalAlpha=.35;c.fillStyle='#fff';c.fillRect(b.x,b.y+wrap(t*60,b.h),b.w,2);
  if(hash(Math.floor(t*8))>.93){c.globalAlpha=.35;c.fillRect(b.x,b.y,b.w,b.h)}
  c.globalAlpha=1;
  // flying cars
  for(let i=0;i<10;i++){const z=.35+hash(i+1)*.65,dir=i%2?1:-1,sp=(60+hash(i+2)*150)*z,y=H*(.18+hash(i+3)*.42)+Math.sin(t*.6+i)*6;
    const x=wrap(hash(i+4)*W+dir*t*sp,W+400)-200,s=z;
    c.globalAlpha=.25*z;c.fillStyle=dir>0?'#ff5050':'#ffdcc8';c.fillRect(dir>0?x-70*s:x,y-.5,70*s,1);c.globalAlpha=1;
    sg(c,'255,240,220',x+dir*6*s,y,22*s,.9);sg(c,'255,60,60',x-dir*6*s,y,16*s,.75)}
  // maglev train
  const ty=D.trackY,tl=560,tx=wrap(t*300,W*2.4)-tl-W*.4;
  if(tx>-tl&&tx<W){c.globalCompositeOperation='source-over';c.fillStyle='#0b0614';rr(c,tx,ty-16,tl,16,7);c.fill();
    c.globalCompositeOperation='lighter';c.fillStyle='rgba(120,230,255,.85)';for(let k=14;k<tl-14;k+=18)c.fillRect(tx+k,ty-12,11,5);
    sf(c,'80,220,255',tx+tl/2,ty-8,tl*1.3,60,.25);sg(c,'255,255,255',tx+tl,ty-8,60,.9)}
  c.globalCompositeOperation='lighter';
  [[W*.28,H*.74,0],[W*.7,H*.76,2.1]].forEach(([x,y,ph])=>{const a=-Math.PI/2+Math.sin(t*.25+ph)*.55,len=H*1.1,w=.05;
    c.fillStyle=lin(c,x,y,x+Math.cos(a)*len,y+Math.sin(a)*len,[[0,'rgba(200,220,255,.15)'],[1,'rgba(200,220,255,0)']]);
    c.beginPath();c.moveTo(x-3,y);c.lineTo(x+Math.cos(a-w)*len,y+Math.sin(a-w)*len);c.lineTo(x+Math.cos(a+w)*len,y+Math.sin(a+w)*len);c.lineTo(x+3,y);c.closePath();c.fill()});
  const [hx,hy]=D.ring;c.lineWidth=1.5;
  for(let k=0;k<3;k++){const ry=hy+k*26,rw=120-k*16;c.strokeStyle=k%2?'rgba(255,80,200,.8)':'rgba(80,230,255,.85)';c.setLineDash([18,10]);c.lineDashOffset=(k%2?-1:1)*t*40;c.globalAlpha=.5+.25*Math.sin(t*2+k);c.beginPath();c.ellipse(hx,ry,rw,rw*.16,0,0,TAU);c.stroke()}
  c.setLineDash([]);c.globalAlpha=1;sf(c,'255,80,200',hx,hy+26,340,80,.16);
  for(let i=0;i<4;i++){const x=wrap(hash(i*7.3)*W+t*(10+i*5),W+1000)-500;sf(c,'200,90,210',x,H*(.7+i*.05),900,80,.07)}
  // rain
  c.globalCompositeOperation='lighter';c.lineWidth=1;c.strokeStyle='rgba(170,190,255,.22)';c.beginPath();
  for(let i=0;i<320;i++){const z=hash(i*3.1),sp=1100+z*900,len=12+z*30,x0=hash(i*7.7)*W*1.25,y=wrap(hash(i*1.3)*H*1.2+t*sp,H*1.2)-H*.1,x=x0-y*.16-px*z*20;c.moveTo(x,y);c.lineTo(x-len*.16,y+len)}
  c.stroke();c.strokeStyle='rgba(210,220,255,.34)';c.lineWidth=1.7;c.beginPath();
  for(let i=0;i<50;i++){const sp=2200+hash(i*2.9)*600,len=40+hash(i*5.5)*30,x0=hash(i*9.3)*W*1.25,y=wrap(hash(i*4.1)*H*1.2+t*sp,H*1.2)-H*.1,x=x0-y*.16-px*30;c.moveTo(x,y);c.lineTo(x-len*.16,y+len)}
  c.stroke();
  c.strokeStyle='rgba(200,220,255,1)';c.lineWidth=1;
  for(let i=0;i<26;i++){const p=wrap(t*1.7+hash(i*9.1),1),x=hash(i*5.3+Math.floor(t*1.7+hash(i*9.1)))*W,y=H*(.92+hash(i*2.2)*.07);c.globalAlpha=(1-p)*.5;c.beginPath();c.ellipse(x,y,2+p*12,1+p*3,0,0,TAU);c.stroke()}
  c.globalAlpha=1;
}

/* ════════════════════ II · Aurora ════════════════════ */
const AN=[...Array(9)].map((_,i)=>noise1(2000+i*17));let AURG=null,AURP=null,SNOW=null;
function drawAurora(c,W,H,t,mul){
  if(!AURG){AURG=vSprite([[0,'rgba(120,80,255,0)'],[.35,'rgba(140,90,255,.22)'],[.72,'rgba(60,255,170,.6)'],[.93,'rgba(200,255,225,.95)'],[1,'rgba(60,255,170,0)']]);
            AURP=vSprite([[0,'rgba(255,80,200,0)'],[.4,'rgba(255,90,200,.25)'],[.8,'rgba(150,110,255,.55)'],[.95,'rgba(220,210,255,.8)'],[1,'rgba(150,110,255,0)']])}
  const R=[{y:.22,amp:.07,f:.0034,s:.12,h:.28,a:1,sp:AURG},{y:.3,amp:.05,f:.0052,s:-.09,h:.2,a:.8,sp:AURG},{y:.16,amp:.06,f:.0026,s:.07,h:.22,a:.6,sp:AURP}];
  const o=c.globalCompositeOperation;c.globalCompositeOperation='lighter';
  R.forEach((r,k)=>{for(let x=-10;x<W+10;x+=6){const u=x/W;
    const y=H*(r.y+r.amp*Math.sin(x*r.f+t*r.s*3+k*2)+.07*(AN[k](u*3+t*r.s)-.5));
    let it=AN[k+3](u*8-t*.22*(k+1));it=it*it*1.6*r.a*mul*(.35+.65*Math.sin(Math.max(0,Math.min(1,u))*Math.PI));if(it<.02)continue;
    const h=H*r.h*(.55+.9*AN[k+6](u*5+t*.08));c.globalAlpha=Math.min(1,it);c.drawImage(r.sp,x,y-h,7,h*1.12)}});
  c.globalAlpha=1;c.globalCompositeOperation=o}
function pAurora(c,W,H,D){
  const hz=H*.6;D.hz=hz;
  if(!SNOW)SNOW=vSprite([[0,'rgba(235,245,255,1)'],[.35,'rgba(225,238,255,.7)'],[1,'rgba(220,235,255,0)']],4,128);
  c.fillStyle=lin(c,0,0,0,hz,[[0,'#010208'],[.45,'#04122a'],[.85,'#0b2b40'],[1,'#164150']]);c.fillRect(0,0,W,hz);
  c.save();c.translate(W*.6,H*.22);c.rotate(-.42);c.globalCompositeOperation='lighter';sf(c,'110,130,255',0,0,W*1.4,H*.26,.22);sf(c,'255,200,180',W*.08,0,W*.55,H*.1,.1);
  const r=rng(201);c.fillStyle='#fff';for(let i=0;i<1600;i++){const x=(r()-.5)*W*1.5,y=(r()+r()+r()-1.5)*H*.07;c.globalAlpha=r()*.55;c.fillRect(x,y,1.1,1.1)}c.restore();
  stars(c,W,H,900,202,.62,.9);
  drawAurora(c,W,H,0,.55);
  const range=o=>{const fn=ridge(c,W,H,o);const p=new Path2D();p.moveTo(-10,H);fn.pts.forEach(q=>p.lineTo(q[0],q[1]));p.lineTo(W+10,H);p.closePath();
    c.save();c.clip(p);const n=noise1(o.seed+50);
    for(let i=1;i<fn.pts.length-1;i++){const [x,y]=fn.pts[i];const sl=fn.pts[i+1][1]-fn.pts[i-1][1];const lit=Math.max(0,Math.min(1,.5-sl*.06));const d=H*o.snow*(.3+n(x*.006)*1.1);
      c.globalAlpha=(.12+.5*lit)*o.snowA;c.drawImage(SNOW,x-6,y-1,12,d)}
    c.globalAlpha=1;c.fillStyle=lin(c,0,(o.base-o.amp)*H,0,o.base*H,[[0,'rgba(120,255,200,.12)'],[1,'rgba(0,0,0,0)']]);c.fillRect(0,0,W,H);c.restore();
    c.save();c.globalCompositeOperation='lighter';c.beginPath();fn.pts.forEach((q,i)=>i?c.lineTo(q[0],q[1]):c.moveTo(q[0],q[1]));c.strokeStyle='rgba(170,255,220,.3)';c.lineWidth=1.2;c.stroke();c.restore();return fn};
  const m0=range({base:.6,amp:.3,freq:1.8,seed:203,sharp:true,oct:5,fill:lin(c,0,H*.3,0,hz,[[0,'#40567a'],[1,'#121e33']]),snow:.12,snowA:.85});
  band(c,W,hz-H*.03,H*.05,'rgba(160,220,255,.12)');
  const m1=range({base:.6,amp:.14,freq:3.4,seed:207,sharp:true,oct:5,fill:lin(c,0,H*.46,0,hz,[[0,'#26354f'],[1,'#0a1220']]),snow:.06,snowA:.6});
  const pr=rng(208);for(let i=0;i<150;i++){const x=pr()*W,h=8+pr()*26;pine(c,x,hz+1,h,h*.36,'#050b14')}
  const sky=m0.pts.map((p,i)=>[p[0],Math.min(p[1],m1.pts[i][1])]);D.sky=abovePath(sky,W);
  D.water=new Path2D();D.water.moveTo(-10,hz*2-sky[0][1]);sky.forEach(p=>D.water.lineTo(p[0],hz*2-p[1]));D.water.lineTo(W+10,H+10);D.water.lineTo(-10,H+10);D.water.closePath();
  reflect(c,W,H,hz,211,10,'2,6,14');
  c.globalCompositeOperation='lighter';const sr=rng(212);for(let i=0;i<200;i++){const y=hz+Math.pow(sr(),1.4)*(H-hz),x=sr()*W;c.fillStyle=`rgba(150,255,210,${.02+sr()*.05})`;c.fillRect(x,y,10+sr()*120,1)}c.globalCompositeOperation='source-over';
  const ir=rng(214);for(let i=0;i<34;i++){const y=hz+H*.06+Math.pow(ir(),.8)*(H-hz)*.75,k=(y-hz)/(H-hz),x=ir()*W,w=(20+ir()*70)*(.4+k*1.6),h=w*(.12+k*.1);
    c.fillStyle=`rgba(190,215,235,${.14+k*.3})`;c.beginPath();for(let q=0;q<7;q++){const a=q/7*TAU,r0=.7+ir()*.3,qx=x+Math.cos(a)*w*r0,qy=y+Math.sin(a)*h*r0;if(q)c.lineTo(qx,qy);else c.moveTo(qx,qy)}c.closePath();c.fill();
    c.fillStyle=`rgba(235,245,255,${.25+k*.4})`;c.fillRect(x-w*.6,y-h*.5,w*1.1,1)}
  // shore & cabin
  c.fillStyle='#03060c';c.beginPath();c.moveTo(-10,H*.8);c.bezierCurveTo(W*.12,H*.78,W*.26,H*.86,W*.42,H+10);c.lineTo(-10,H+10);c.fill();
  const tr=rng(213);for(let i=0;i<22;i++){const x=tr()*W*.3,y=H*.8+Math.pow(x/(W*.42),2)*H*.2+8,h=40+tr()*120;if(Math.abs(x-W*.13)<60)continue;pine(c,x,y,h,h*.34,'#03060c')}
  const cx=W*.13,cy=H*.815;c.fillStyle='#070a10';c.fillRect(cx-34,cy-30,68,30);c.beginPath();c.moveTo(cx-42,cy-28);c.lineTo(cx,cy-58);c.lineTo(cx+42,cy-28);c.fill();c.fillRect(cx+18,cy-60,8,20);
  c.fillStyle='rgba(230,240,255,.82)';c.beginPath();c.moveTo(cx-42,cy-28);c.lineTo(cx,cy-58);c.lineTo(cx+42,cy-28);c.lineTo(cx+38,cy-31);c.lineTo(cx,cy-54);c.lineTo(cx-38,cy-31);c.fill();
  c.fillStyle='#ffc477';c.fillRect(cx-18,cy-21,12,10);c.fillRect(cx+6,cy-21,12,10);sg(c,'255,180,90',cx,cy-16,130,.6);
  D.cabin=[cx,cy-16];D.chim=[cx+22,cy-62];
  c.fillStyle='#03060c';c.beginPath();c.moveTo(W*.84,H+10);c.quadraticCurveTo(W*.92,H*.9,W+10,H*.88);c.lineTo(W+10,H+10);c.fill();
  finish(c,W,H,.5);
}
function aAurora(c,t,D,px){
  const W=WW,H=HH;
  c.save();c.clip(D.sky);drawAurora(c,W,H,t,.9);
  for(let i=0;i<24;i++){const x=hash(i*3.7)*W,y=hash(i*9.1)*H*.5,b=Math.pow(Math.max(0,Math.sin(t*(.7+hash(i)*1.3)+i*3)),8);sg(c,'220,235,255',x,y,12,b*.9)}
  const k=Math.floor(t/9),p=wrap(t,9);
  if(p<1.1){const x0=W*(.2+hash(k)*.5),y0=H*(.05+hash(k+.5)*.15),q=p/1.1,x=x0+q*260,y=y0+q*90;c.globalCompositeOperation='lighter';
    c.strokeStyle=lin(c,x-120,y-42,x,y,[[0,'rgba(255,255,255,0)'],[1,`rgba(255,255,255,${.9*(1-q)})`]]);c.lineWidth=1.5;c.beginPath();c.moveTo(x-120,y-42);c.lineTo(x,y);c.stroke()}
  c.restore();
  c.save();c.clip(D.water);c.translate(0,D.hz*2);c.scale(1,-1);drawAurora(c,W,H,t,.22);c.restore();
  for(let i=0;i<10;i++){const q=wrap(t*.12+i/10,1),[cx,cy]=D.chim;sf(c,'170,180,200',cx+q*40+Math.sin(t+i)*6,cy-q*90,14+q*44,14+q*44,(1-q)*.16)}
  sg(c,'255,170,80',D.cabin[0],D.cabin[1],90,.22+.08*Math.sin(t*5)*Math.sin(t*2.3));
  for(let i=0;i<110;i++){const z=hash(i*4.7),y=wrap(hash(i*2.3)*H+t*(16+z*44),H+20)-10,x=wrap(hash(i*8.1)*W+Math.sin(t*.7+i)*22*z+t*8,W);sg(c,'225,240,255',x-px*z*16,y,3+z*9,.3+z*.55)}
}

/* ════════════════════ III · Horizon (synthwave) ════════════════════ */
function palm(c,x,y,h,lean){const tx=x+lean*h,ty=y-h;c.strokeStyle='#06010c';c.lineCap='round';
  c.lineWidth=h*.04;c.beginPath();c.moveTo(x,y);c.quadraticCurveTo(x+lean*h*.15,y-h*.6,tx,ty);c.stroke();
  for(let k=0;k<9;k++){const a=-Math.PI/2+(k-4)*.44+lean*.5,len=h*(.3+((k*37)%10)/45);
    const P0=[tx,ty],P1=[tx+Math.cos(a)*len*.55,ty+Math.sin(a)*len*.55-len*.12],P2=[tx+Math.cos(a)*len,ty+Math.sin(a)*len*.45+len*.32];
    c.lineWidth=h*.011;c.beginPath();c.moveTo(P0[0],P0[1]);c.quadraticCurveTo(P1[0],P1[1],P2[0],P2[1]);c.stroke();
    c.lineWidth=h*.005;c.beginPath();for(let q=.15;q<1;q+=.07){const u=1-q,bx=u*u*P0[0]+2*u*q*P1[0]+q*q*P2[0],by=u*u*P0[1]+2*u*q*P1[1]+q*q*P2[1],L=len*.13*(1-q*.6);
      c.moveTo(bx,by);c.lineTo(bx-L*.5,by+L);c.moveTo(bx,by);c.lineTo(bx+L*.5,by+L)}c.stroke()}
  dot(c,tx,ty,h*.025,'#06010c')}
function pGrid(c,W,H,D){
  const hz=H*.62;D.hz=hz;
  c.fillStyle=lin(c,0,0,0,hz,[[0,'#05021a'],[.32,'#22074a'],[.6,'#6e1670'],[.82,'#ff3f7f'],[1,'#ffb06a']]);c.fillRect(0,0,W,hz);
  stars(c,W,H,520,301,.42,.85);
  const sx=W*.5,R=H*.23,sy=hz-R*.62;D.sun=[sx,sy,R];
  glow(c,sx,sy,R*2.8,'rgba(255,80,150,.32)');glow(c,sx,sy,R*1.6,'rgba(255,170,90,.32)');
  const sc=document.createElement('canvas');sc.width=sc.height=Math.ceil(R*2+4);const sx2=sc.getContext('2d');
  sx2.fillStyle=lin(sx2,0,0,0,sc.height,[[0,'#fff4a0'],[.35,'#ffc04a'],[.62,'#ff6a5a'],[1,'#ff2a9a']]);sx2.beginPath();sx2.arc(sc.width/2,sc.height/2,R,0,TAU);sx2.fill();
  D.sunC=sc;D.sunO=document.createElement('canvas');D.sunO.width=sc.width;D.sunO.height=sc.height;D.sunX=D.sunO.getContext('2d');
  const r0=rng(309);c.globalCompositeOperation='lighter';for(let i=0;i<8;i++)sf(c,'255,120,200',r0()*W,H*(.12+r0()*.3),400+r0()*500,10+r0()*20,.08);c.globalCompositeOperation='source-over';
  const mtn=(seed,amp,step,fillTop,fillBot,rgb)=>{const r=rng(seed),pts=[[-20,hz]];
    for(let x=-20;x<=W+step;x+=step*(.6+r()*.8)){const k=Math.min(1,Math.abs(x-W/2)/(W*.5));const h=amp*H*(.12+.88*Math.pow(k,1.2))*(.45+r()*.55);pts.push([x,hz-h])}
    pts.push([W+40,hz]);
    c.beginPath();pts.forEach((p,i)=>i?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.closePath();c.fillStyle=lin(c,0,hz-amp*H,0,hz,[[0,fillTop],[1,fillBot]]);c.fill();
    c.save();c.clip();c.globalCompositeOperation='lighter';c.strokeStyle=`rgba(${rgb},.2)`;c.lineWidth=1;c.beginPath();
    for(let i=1;i<pts.length-1;i++){c.moveTo(pts[i][0],pts[i][1]);c.lineTo(pts[i][0]+(r()-.5)*60,hz)}for(let y=hz-8;y>hz-amp*H;y-=12){c.moveTo(0,y);c.lineTo(W,y)}c.stroke();c.restore();
    c.save();c.globalCompositeOperation='lighter';c.beginPath();for(let i=1;i<pts.length-1;i++){if(i>1)c.lineTo(pts[i][0],pts[i][1]);else c.moveTo(pts[i][0],pts[i][1])}
    c.strokeStyle=`rgba(${rgb},.9)`;c.lineWidth=1.8;c.stroke();c.strokeStyle=`rgba(${rgb},.22)`;c.lineWidth=6;c.stroke();c.restore();
    return abovePath(pts,W)};
  D.skyA=mtn(302,.24,70,'#300c55','#14042c','255,70,210');
  band(c,W,hz-6,H*.03,'rgba(255,120,200,.25)');
  const cr=rng(310),cpts=[[W*.3,hz]];let qx=W*.3;
  while(qx<W*.7){const w=8+cr()*22,k=1-Math.abs(qx-W/2)/(W*.2),h=(8+cr()*46)*(.4+Math.max(0,k)*.9);cpts.push([qx,hz-h],[qx+w,hz-h]);
    c.fillStyle='#14042a';c.fillRect(qx,hz-h,w,h);c.globalCompositeOperation='lighter';
    for(let yy=hz-h+3;yy<hz-2;yy+=4)for(let xx=qx+2;xx<qx+w-2;xx+=4)if(cr()<.22){c.fillStyle=cr()<.6?'rgba(255,90,210,.8)':'rgba(90,230,255,.8)';c.fillRect(xx,yy,1.5,1.5)}
    c.fillStyle='rgba(255,120,220,.6)';c.fillRect(qx,hz-h,w,1);c.globalCompositeOperation='source-over';qx+=w+cr()*3}
  cpts.push([W*.7,hz]);D.skyC=abovePath(cpts,W);
  D.skyB=mtn(303,.13,48,'#1c0634','#0b0219','90,220,255');
  c.fillStyle=lin(c,0,hz,0,H,[[0,'#2a0640'],[.2,'#13032b'],[1,'#040010']]);c.fillRect(0,hz,W,H-hz);
  c.save();c.globalCompositeOperation='lighter';c.strokeStyle=lin(c,0,hz,0,H,[[0,'rgba(255,60,200,0)'],[.25,'rgba(255,60,200,.3)'],[1,'rgba(255,100,230,.95)']]);
  for(const lw of [5,1.4]){c.lineWidth=lw;c.globalAlpha=lw>2?.25:1;c.beginPath();for(let k=-36;k<=36;k++){c.moveTo(W/2,hz);c.lineTo(W/2+k*120,H)}c.stroke()}
  c.restore();
  c.fillStyle='rgba(5,0,15,.65)';c.beginPath();c.moveTo(W/2-3,hz);c.lineTo(W/2+3,hz);c.lineTo(W/2+300,H);c.lineTo(W/2-300,H);c.fill();
  c.save();c.globalCompositeOperation='lighter';c.strokeStyle=lin(c,0,hz,0,H,[[0,'rgba(90,220,255,0)'],[1,'rgba(90,220,255,.95)']]);c.lineWidth=2;
  c.beginPath();c.moveTo(W/2,hz);c.lineTo(W/2-300,H);c.moveTo(W/2,hz);c.lineTo(W/2+300,H);c.stroke();
  c.fillStyle='rgba(255,170,220,.9)';c.fillRect(0,hz-1,W,2);sf(c,'255,80,200',W/2,hz,W*1.4,60,.5);sf(c,'255,130,150',W/2,hz+30,R*2.2,70,.3);c.restore();
  c.save();c.globalCompositeOperation='lighter';for(let i=0;i<26;i++){const y=hz+3+i*i*.45,w=R*1.6*(1-i/30);c.fillStyle=`rgba(255,${150-i*3},${120+i*2},${.35*(1-i/26)})`;c.fillRect(W/2-w/2,y,w,1.2)}c.restore();
  palm(c,W*.07,H*1.0,H*.56,.16);palm(c,W*.16,H*.95,H*.4,-.08);palm(c,W*.92,H*.99,H*.52,-.2);
  finish(c,W,H,.45);
}
function aGrid(c,t,D){
  const W=WW,H=HH,hz=D.hz,[sx,sy,R]=D.sun,o=D.sunX,S=D.sunO.width;
  o.globalCompositeOperation='source-over';o.clearRect(0,0,S,S);o.drawImage(D.sunC,0,0);o.globalCompositeOperation='destination-out';
  for(let i=0;i<12;i++){const p=wrap(i/12+t*.04,1);o.fillRect(0,S*(.5+p*.5),S,1+p*p*13)}
  c.save();c.clip(D.skyA);c.clip(D.skyB);c.clip(D.skyC);c.drawImage(D.sunO,sx-S/2,sy-S/2);sg(c,'255,190,120',sx,sy,R*2.6,.22+.05*Math.sin(t*1.3));
  for(let i=0;i<22;i++){const x=hash(i*3.3)*W,y=hash(i*7.1)*H*.4,b=Math.pow(Math.max(0,Math.sin(t*(.6+hash(i)*1.4)+i*2)),6);sg(c,'255,220,255',x,y,12,b*.8)}
  c.restore();
  c.globalCompositeOperation='lighter';const K=(H-hz)*1.2;c.fillStyle='#ff4fd8';
  for(let i=0;i<34;i++){const d=wrap(i-t*2.4,34)+.85,y=hz+K/d;if(y>H+4)continue;const a=Math.min(1,2.6/d);
    c.globalAlpha=a*.9;c.fillRect(0,y-.5,W,Math.max(1,2.4/d));c.globalAlpha=a*.22;c.fillRect(0,y-3/d-1,W,6/d+2)}
  c.fillStyle='#bff6ff';
  for(let i=0;i<17;i++){const d0=wrap(i*2-t*2.4,34)+.85,y1=hz+K/(d0+.9),y2=Math.min(H,hz+K/d0);if(y1>H)continue;const w=14/d0;c.globalAlpha=Math.min(1,3/d0)*.85;c.fillRect(W/2-w/2,y1,w,y2-y1)}
  const d=5.2+Math.sin(t*.27)*.9,cy=hz+K/d,half=300*1.2/d,cx=W/2+half*.45+Math.sin(t*.4)*half*.08,sp=46/d;
  c.globalCompositeOperation='source-over';c.globalAlpha=1;c.fillStyle='#0a0014';rr(c,cx-sp*1.1,cy-sp*.55,sp*2.2,sp*.6,sp*.15);c.fill();
  sg(c,'255,40,70',cx-sp*.85,cy-sp*.3,sp*1.4,.95);sg(c,'255,40,70',cx+sp*.85,cy-sp*.3,sp*1.4,.95);
  c.globalCompositeOperation='lighter';c.globalAlpha=.6;c.fillStyle='#ff2850';c.fillRect(cx-sp*.9,cy-sp*.32,sp*1.8,sp*.06);c.globalAlpha=1;
}

/* ════════════════════ IV · Reef ════════════════════ */
function whale(c,x,y,s,col){c.save();c.translate(x,y);c.scale(s,s);c.fillStyle=col;c.beginPath();
  c.moveTo(-200,0);c.bezierCurveTo(-200,-40,-120,-58,-20,-50);c.bezierCurveTo(80,-42,150,-20,210,-6);c.lineTo(250,-30);c.quadraticCurveTo(262,-8,250,6);c.quadraticCurveTo(262,26,246,40);c.lineTo(210,8);
  c.bezierCurveTo(140,22,60,40,-40,38);c.bezierCurveTo(-140,36,-200,30,-200,0);c.fill();
  c.beginPath();c.moveTo(-90,28);c.quadraticCurveTo(-60,90,-10,110);c.quadraticCurveTo(-40,70,-40,32);c.fill();c.restore()}
function pReef(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H,[[0,'#7ae6ff'],[.09,'#22a8d8'],[.3,'#0b62a6'],[.62,'#063268'],[1,'#020d26']]);c.fillRect(0,0,W,H);
  const r=rng(401);c.globalCompositeOperation='lighter';for(let i=0;i<300;i++)sf(c,'225,255,255',r()*W,Math.pow(r(),2.2)*H*.13,26+r()*110,3+r()*9,.08+r()*.16);c.globalCompositeOperation='source-over';
  rays(c,W*.52,-H*.3,H*1.35,28,Math.PI/2,1.25,'190,245,255',402,.085);
  whale(c,W*.68,H*.33,.95,'rgba(6,36,76,.55)');
  ridge(c,W,H,{base:.74,amp:.13,freq:2.8,seed:403,oct:4,fill:'rgba(9,58,108,.6)'});
  band(c,W,H*.72,H*.08,'rgba(60,160,220,.12)');
  ridge(c,W,H,{base:.83,amp:.12,freq:3.6,seed:404,oct:4,fill:'#06305a'});
  ridge(c,W,H,{base:.93,amp:.05,freq:3,seed:405,oct:3,fill:lin(c,0,H*.86,0,H,[[0,'#2a6585'],[1,'#0a1f33']])});
  c.strokeStyle='rgba(150,220,240,.12)';c.lineWidth=1.2;for(let i=0;i<40;i++){const y=H*(.9+r()*.1),x=r()*W,l=60+r()*160;c.beginPath();c.moveTo(x,y);c.quadraticCurveTo(x+l/2,y-4,x+l,y);c.stroke()}
  const tips=[];
  const branch=(x,y,len,ang,d,w,col,tip,g)=>{const x2=x+Math.cos(ang)*len,y2=y+Math.sin(ang)*len;c.strokeStyle=col;c.lineWidth=w;c.lineCap='round';
    c.beginPath();c.moveTo(x,y);c.quadraticCurveTo(x+Math.cos(ang+.3)*len*.5,y+Math.sin(ang+.3)*len*.5,x2,y2);c.stroke();
    if(d<=0){tips.push([x2,y2,tip,1]);return}const n=2+(g()<.4?1:0);for(let i=0;i<n;i++)branch(x2,y2,len*(.62+g()*.2),ang+(i-(n-1)/2)*.55+(g()-.5)*.3,d-1,w*.72,col,tip,g)};
  const dome=(x,y,rx,ry,c1,c2)=>{c.save();c.beginPath();c.ellipse(x,y,rx,ry,0,Math.PI,TAU);c.closePath();c.fillStyle=rad(c,x,y,rx,[[0,c1],[1,c2]],x-rx*.3,y-ry*.8);c.fill();c.clip();
    c.strokeStyle='rgba(0,0,0,.25)';c.lineWidth=2;for(let k=0;k<9;k++){c.beginPath();for(let xx=-rx;xx<=rx;xx+=4){const yy=y-ry*(k/9)+Math.sin(xx*.15+k*2)*4;if(xx>-rx)c.lineTo(x+xx,yy);else c.moveTo(x+xx,yy)}c.stroke()}c.restore()};
  const fan=(x,y,s,col,seed)=>{const g=rng(seed);c.strokeStyle=col;c.lineCap='round';
    for(let i=0;i<46;i++){const a=-Math.PI/2+(i/45-.5)*1.9+(g()-.5)*.08,l=s*(.55+g()*.45);c.lineWidth=1.3+g()*1.2;c.beginPath();c.moveTo(x,y);c.quadraticCurveTo(x+Math.cos(a)*l*.5+(g()-.5)*20,y+Math.sin(a)*l*.5,x+Math.cos(a)*l,y+Math.sin(a)*l);c.stroke()}
    c.lineWidth=.8;c.globalAlpha=.6;for(let k=.3;k<1;k+=.1){c.beginPath();c.ellipse(x,y,s*k,s*k*.95,0,-Math.PI/2-.95,-Math.PI/2+.95);c.stroke()}c.globalAlpha=1;c.lineWidth=6;c.beginPath();c.moveTo(x,y+4);c.lineTo(x,y-s*.15);c.stroke()};
  const anem=(x,y,col,tip,seed)=>{const g=rng(seed);c.lineCap='round';for(let i=0;i<34;i++){const a=-Math.PI/2+(g()-.5)*2.2,l=30+g()*40,ex=x+Math.cos(a)*l,ey=y+Math.sin(a)*l;
    c.strokeStyle=col;c.lineWidth=3;c.beginPath();c.moveTo(x+(g()-.5)*20,y);c.quadraticCurveTo(x+Math.cos(a)*l*.4+(g()-.5)*14,y+Math.sin(a)*l*.6,ex,ey);c.stroke();tips.push([ex,ey,tip,.6])}};
  const tubes=(x,y,col,seed)=>{const g=rng(seed);for(let i=0;i<4;i++){const tx=x+(i-1.5)*20+(g()-.5)*8,h=50+g()*90,w=16+g()*6;
    c.fillStyle=lin(c,tx-w/2,0,tx+w/2,0,[[0,col[1]],[.5,col[0]],[1,col[1]]]);rr(c,tx-w/2,y-h,w,h+6,w/2);c.fill();c.fillStyle='rgba(10,10,30,.75)';c.beginPath();c.ellipse(tx,y-h+3,w*.38,3.5,0,0,TAU);c.fill()}};
  fan(W*.21,H*.93,200,'rgba(196,74,216,.85)',411);fan(W*.77,H*.94,170,'rgba(255,92,92,.8)',412);
  const rb=rng(413);
  branch(W*.07,H*.98,105,-Math.PI/2+.1,5,17,'#e8664a','255,190,140',rb);
  branch(W*.87,H*.98,115,-Math.PI/2-.12,5,18,'#ff4f8b','255,170,210',rb);
  branch(W*.43,H*.99,60,-Math.PI/2,4,9,'#ffb547','255,225,150',rb);
  dome(W*.14,H*.975,80,52,'#ffb27a','#8a3e2a');dome(W*.94,H*.97,70,46,'#b48bff','#3e2378');dome(W*.6,H*.985,52,30,'#7affd4','#1e6d64');
  anem(W*.3,H*.975,'rgba(255,120,180,.85)','255,160,220',414);anem(W*.69,H*.975,'rgba(110,255,210,.8)','120,255,220',415);
  tubes(W*.35,H*.985,['#ffd36a','#b8741c'],416);tubes(W*.985,H*.99,['#ff8a5c','#9a3a20'],417);
  tips.forEach(([x,y,rgb,s])=>sg(c,rgb,x,y,14*s,.55));
  const rs=document.createElement('canvas');rs.width=64;rs.height=256;const rx=rs.getContext('2d');
  rx.fillStyle=lin(rx,0,0,64,0,[[0,'rgba(210,250,255,0)'],[.5,'rgba(210,250,255,1)'],[1,'rgba(210,250,255,0)']]);rx.fillRect(0,0,64,256);
  rx.globalCompositeOperation='destination-in';rx.fillStyle=lin(rx,0,0,0,256,[[0,'#000'],[1,'rgba(0,0,0,0)']]);rx.fillRect(0,0,64,256);D.ray=rs;
  D.ctile=causticTile();D.cp=new Map();
  D.kelp=[[W*.015,H*.82,10],[W*.045,H*.62,8],[W*.1,H*.5,6],[W*.905,H*.55,7],[W*.95,H*.78,9],[W*.99,H*.66,10]];
  finish(c,W,H,.55);
}
function aReef(c,t,D,px){
  const W=WW,H=HH;c.globalCompositeOperation='lighter';
  for(let i=0;i<6;i++){const x=W*(.12+i*.155)+Math.sin(t*.25+i*1.7)*50,a=.07+.06*Math.sin(t*.6+i*1.3);c.save();c.translate(x,-40);c.rotate(.12+Math.sin(t*.2+i)*.04);c.globalAlpha=Math.max(0,a);c.drawImage(D.ray,-110,0,220,H);c.restore()}
  let pat=D.cp.get(c);if(!pat){pat=c.createPattern(D.ctile,'repeat');D.cp.set(c,pat)}
  for(const [y0,al] of [[.84,.16],[.89,.22]]){c.save();c.beginPath();c.rect(0,H*y0,W,H*(1-y0));c.clip();
    for(let k=0;k<2;k++){c.save();c.translate(W/2,H*.84);c.scale(1.4,.42);pat.setTransform(new DOMMatrix().translate(t*(k?-14:18)+k*60,t*(k?9:-6)).scale(k?1.3:1));
      c.fillStyle=pat;c.globalAlpha=al;c.fillRect(-W*.5/1.4-10,0,W/1.4+20,H*.16/.42+10);c.restore()}
    c.restore()}
  c.globalAlpha=1;
  for(let i=0;i<70;i++){const z=hash(i*5.9),x=wrap(hash(i*1.1)*W+t*(4+z*6),W),y=wrap(hash(i*2.6)*H+t*(6+z*10),H);sg(c,'200,240,255',x-px*z*14,y,2+z*5,.2+z*.4)}
  c.globalCompositeOperation='source-over';
  const fx=W*.5+Math.sin(t*.11)*W*.32,fy=H*.44+Math.sin(t*.19)*H*.09,dir=Math.cos(t*.11)>=0?1:-1;
  for(let i=0;i<48;i++){const a=hash(i*3.3)*TAU,r0=30+hash(i*5.1)*130,x=fx+Math.cos(a+t*.35)*r0*1.5,y=fy+Math.sin(a+t*.35)*r0*.45+Math.sin(t*2.2+i)*4,s=.55+hash(i*1.7)*.6,w=Math.sin(t*9+i)*1.5;
    c.fillStyle=`rgba(${170+(hash(i*2.2)*70|0)},225,255,.8)`;c.beginPath();c.ellipse(x,y,9*s,3.2*s,0,0,TAU);c.fill();
    c.beginPath();c.moveTo(x-dir*7*s,y);c.lineTo(x-dir*14*s,y-4*s+w);c.lineTo(x-dir*14*s,y+4*s+w);c.closePath();c.fill()}
  c.globalCompositeOperation='lighter';
  for(let j=0;j<4;j++){const ph=hash(j*9.9)*10,x=W*(.16+j*.23)+Math.sin(t*.23+ph)*60,y=wrap(H*(.25+hash(j*4.4)*.55)-t*(9+j*3),H*1.15)-H*.08,pu=Math.sin(t*1.5+ph),s=.65+hash(j*2.2)*.6,
    rw=36*s*(1+pu*.09),rh=28*s*(1-pu*.12),col=j%2?'255,120,220':'110,235,255';
    c.strokeStyle=`rgba(${col},.32)`;c.lineWidth=1.1;
    for(let k=0;k<8;k++){const bx=x+(k-3.5)*rw*.22;c.beginPath();c.moveTo(bx,y);for(let q=1;q<=12;q++)c.lineTo(bx+Math.sin(t*1.8+q*.5+k)*q*.9,y+q*9*s);c.stroke()}
    c.fillStyle=rad(c,x,y,rw,[[0,`rgba(${col},.1)`],[.75,`rgba(${col},.38)`],[1,`rgba(${col},.06)`]],x,y-rh*.6);
    c.beginPath();c.ellipse(x,y,rw,rh,0,Math.PI,TAU);c.quadraticCurveTo(x,y+rh*.35,x-rw,y);c.fill();sg(c,col,x,y-rh*.35,rw*2.2,.5)}
  c.strokeStyle='#dcfaff';c.lineWidth=1;
  for(let i=0;i<64;i++){const z=hash(i*6.6),x=hash(i*1.9)*W+Math.sin(t*2+i)*4*z,y=wrap(H-(t*(28+z*60)+hash(i*3.7)*H),H+20)-10;c.globalAlpha=.2+z*.45;c.beginPath();c.arc(x,y,1+z*3.5,0,TAU);c.stroke()}
  c.globalAlpha=1;c.globalCompositeOperation='source-over';
  D.kelp.forEach(([x,h,w],i)=>{const n=24,pts=[];for(let s=0;s<=n;s++){const u=s/n;pts.push([x+Math.sin(t*.85+u*3.2+i*1.7)*u*u*44+Math.sin(t*.45+i)*u*16,H+10-u*h])}
    c.strokeStyle=c.fillStyle='#031620';c.lineCap='round';c.lineWidth=w;c.beginPath();pts.forEach((p,k)=>k?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.stroke();
    for(let s=2;s<n;s+=2){const p=pts[s],side=(s/2)%2?1:-1;c.save();c.translate(p[0],p[1]);c.rotate(-Math.PI/2+side*(.85+Math.sin(t*1.2+s+i)*.15));c.beginPath();c.ellipse(20,0,24,6.5,0,0,TAU);c.fill();c.restore()}});
}

/* ════════════════════ V · Orbit ════════════════════ */
function station(c,x,y,s,D){c.save();c.translate(x,y);c.rotate(-.12);c.scale(s,s);
  c.strokeStyle='rgba(190,198,215,.85)';c.lineWidth=2;c.strokeRect(-340,-7,680,14);c.lineWidth=1;c.beginPath();for(let i=-340;i<340;i+=14){c.moveTo(i,-7);c.lineTo(i+14,7);c.moveTo(i+14,-7);c.lineTo(i,7)}c.stroke();
  const panel=(px,py,w,h)=>{c.fillStyle=lin(c,px,py,px+w,py+h,[[0,'#0c2150'],[.5,'#1f4490'],[1,'#0a1838']]);c.fillRect(px,py,w,h);
    c.strokeStyle='rgba(120,170,255,.28)';c.lineWidth=.8;c.beginPath();for(let gx=px+w/6;gx<px+w-1;gx+=w/6){c.moveTo(gx,py);c.lineTo(gx,py+h)}for(let gy=py+h/14;gy<py+h-1;gy+=h/14){c.moveTo(px,gy);c.lineTo(px+w,gy)}c.stroke();
    c.strokeStyle='rgba(255,200,120,.7)';c.lineWidth=1.4;c.strokeRect(px,py,w,h);c.fillStyle=lin(c,px,py,px+w,py+h,[[0,'rgba(255,255,255,0)'],[.52,'rgba(200,230,255,.22)'],[.6,'rgba(255,255,255,0)']]);c.fillRect(px,py,w,h)};
  for(const ax of [-305,-215,215,305]){c.fillStyle='#8a90a0';c.fillRect(ax-2,-150,4,300);panel(ax-36,-160,72,140);panel(ax-36,20,72,140)}
  const mod=(mx,my,w,h)=>{c.fillStyle=lin(c,0,my-h/2,0,my+h/2,[[0,'#f4f6fa'],[.42,'#bcc2cf'],[1,'#3b404d']]);rr(c,mx-w/2,my-h/2,w,h,h/2);c.fill();
    c.strokeStyle='rgba(50,55,70,.45)';c.lineWidth=1;c.beginPath();for(let k=mx-w/2+h*.6;k<mx+w/2-h*.4;k+=w/5){c.moveTo(k,my-h/2+2);c.lineTo(k,my+h/2-2)}c.stroke()};
  mod(-125,0,90,36);mod(125,0,90,36);mod(0,0,190,48);
  c.save();c.rotate(Math.PI/2);mod(-78,0,100,36);mod(78,0,80,30);c.restore();
  c.fillStyle='rgba(236,240,248,.9)';c.fillRect(-70,-128,26,64);c.fillRect(44,64,26,64);
  c.strokeStyle='rgba(120,130,150,.6)';c.beginPath();for(let k=0;k<6;k++){c.moveTo(-70,-128+k*11);c.lineTo(-44,-128+k*11);c.moveTo(44,64+k*11);c.lineTo(70,64+k*11)}c.stroke();
  c.globalCompositeOperation='lighter';c.fillStyle='rgba(255,230,200,.4)';c.fillRect(93,-24,2,48);c.fillRect(167,-18,2,36);c.fillRect(-82,-18,2,36);c.globalCompositeOperation='source-over';
  const m=c.getTransform();
  D.lights=[[-340,0,'255,60,60'],[340,0,'80,255,140'],[0,-128,'255,255,255'],[0,128,'255,255,255'],[-125,-18,'255,220,120']].map(([lx,ly,col])=>{const p=m.transformPoint(new DOMPoint(lx,ly));return[p.x,p.y,col]});
  c.restore()}
function pOrbit(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H,[[0,'#000003'],[1,'#02050d']]);c.fillRect(0,0,W,H);
  c.globalCompositeOperation='lighter';sf(c,'90,60,170',W*.18,H*.18,W*.7,H*.5,.16);sf(c,'40,90,170',W*.85,H*.12,W*.5,H*.4,.12);c.globalCompositeOperation='source-over';
  stars(c,W,H,1400,501,1,1,'230,240,255');
  const ex=W*.45,ey=H*2.1,ER=H*1.62;
  const sunX=W*.74,sunY=ey-Math.sqrt(ER*ER-(sunX-ex)**2);D.sunP=[sunX,sunY];
  c.save();c.beginPath();c.arc(ex,ey,ER,0,TAU);c.clip();c.fillStyle='#01050d';c.fillRect(0,0,W,H);
  c.fillStyle=rad(c,sunX,sunY+H*.05,W*.72,[[0,'rgba(90,170,255,.95)'],[.15,'rgba(30,100,190,.75)'],[.45,'rgba(8,40,90,.4)'],[1,'rgba(0,0,0,0)']]);c.fillRect(0,0,W,H);
  const r=rng(502);c.globalCompositeOperation='lighter';
  for(let i=0;i<520;i++){const x=r()*W,y=H*.48+Math.pow(r(),1.5)*H*.55,light=Math.max(0,1-Math.hypot(x-sunX,y-sunY)/(W*.55));if(light<.03)continue;
    sf(c,'230,240,255',x,y,40+r()*170,(6+r()*20)*(.4+(y-H*.48)/(H*.55)),light*.2)}
  for(let i=0;i<70;i++){const cx=r()*W,cy=H*.5+Math.pow(r(),1.2)*H*.5;if(Math.hypot(cx-sunX,cy-sunY)<W*.3)continue;const n=20+r()*60;c.fillStyle='rgb(255,190,110)';
    for(let k=0;k<n;k++){c.globalAlpha=.3+r()*.7;c.fillRect(cx+(r()-.5)*90,cy+(r()-.5)*90*((cy-H*.45)/(H*.6)),1.2,1.2)}c.globalAlpha=1;sf(c,'255,170,80',cx,cy,80,40,.12)}
  c.restore();
  c.save();c.globalCompositeOperation='lighter';
  for(const [lw,a] of [[34,.05],[16,.1],[7,.22],[2.2,.6]]){c.strokeStyle=lin(c,0,0,W,0,[[0,'rgba(60,130,255,.08)'],[.55,`rgba(80,170,255,${a})`],[.74,`rgba(210,240,255,${Math.min(1,a*1.8)})`],[.9,`rgba(80,170,255,${a})`],[1,'rgba(60,130,255,.06)']]);
    c.lineWidth=lw;c.beginPath();c.arc(ex,ey,ER+lw*.3,0,TAU);c.stroke()}c.restore();
  c.save();c.globalCompositeOperation='lighter';c.filter='blur(6px)';c.strokeStyle='rgba(80,255,170,.35)';c.lineWidth=10;c.beginPath();c.arc(ex,ey,ER+10,-Math.PI/2-.55,-Math.PI/2-.2);c.stroke();
  c.strokeStyle='rgba(170,90,255,.2)';c.lineWidth=18;c.beginPath();c.arc(ex,ey,ER+24,-Math.PI/2-.5,-Math.PI/2-.25);c.stroke();c.filter='none';c.restore();
  {const mx=W*.88,my=H*.3;dot(c,mx,my,20,'#c9ccd6');c.fillStyle=rad(c,mx,my,20,[[0,'rgba(0,0,0,0)'],[1,'rgba(0,0,0,.4)']]);c.beginPath();c.arc(mx,my,20,0,TAU);c.fill();c.fillStyle='rgba(2,4,10,.96)';c.beginPath();c.arc(mx-8,my-2,19.5,0,TAU);c.fill()}
  glow(c,sunX,sunY,W*.5,'rgba(120,170,255,.25)');glow(c,sunX,sunY,230,'rgba(255,240,220,.7)');sg(c,'255,250,240',sunX,sunY,130,1);
  c.save();c.globalCompositeOperation='lighter';c.fillStyle=lin(c,sunX-W*.55,0,sunX+W*.55,0,[[0,'rgba(120,180,255,0)'],[.5,'rgba(200,230,255,.85)'],[1,'rgba(120,180,255,0)']]);c.fillRect(sunX-W*.55,sunY-1.2,W*1.1,2.4);c.restore();
  station(c,W*.23,H*.27,.78,D);
  finish(c,W,H,.5);
}
function aOrbit(c,t,D,px,py){
  const W=WW,H=HH,[sx,sy]=D.sunP,fl=1+.06*Math.sin(t*1.3)+.03*Math.sin(t*5.1);
  sg(c,'255,250,240',sx,sy,190*fl,.5);c.globalCompositeOperation='lighter';
  const cx=W/2+px*40,cy=H/2+py*30;
  for(const [k,s,col,a] of [[.3,40,'120,200,255',.14],[.55,22,'255,180,120',.18],[.8,70,'140,255,200',.08],[1.25,120,'160,140,255',.07],[1.5,30,'255,220,160',.14]]){
    const x=sx+(cx-sx)*k*2,y=sy+(cy-sy)*k*2;sf(c,col,x,y,s*2,s*2,a*fl)}
  for(let i=0;i<7;i++){const x=wrap(hash(i*4.4)*W+t*(6+i*2),W+300)-150,y=H*(.15+hash(i*8.8)*.6)+Math.sin(t*.3+i)*20,s=60+hash(i*2.1)*120;sf(c,'150,190,255',x+px*s*.3,y,s,s,.05)}
  D.lights.forEach(([x,y,col],i)=>{const b=wrap(t+i*.37,1.6);if(b<.18)sg(c,col,x,y,34,1-b/.18)});
  const sp=wrap(t*.025,1),satx=W*(-.05+sp*1.1),saty=H*(.1+sp*.16);sg(c,'230,240,255',satx,saty,10,.9);if(wrap(t,3)<.15)sg(c,'255,255,255',satx,saty,44,.8);
  for(let i=0;i<30;i++){const x=hash(i*3.3)*W,y=hash(i*7.1)*H*.45,b=Math.pow(Math.max(0,Math.sin(t*(.6+hash(i)*1.4)+i*2)),6);sg(c,'220,235,255',x,y,10,b*.8)}
  const k=Math.floor(t/7),p=wrap(t,7);
  if(p<.9){const q=p/.9,x0=W*(.4+hash(k*3)*.5),y0=H*(.04+hash(k*5)*.2),x=x0-q*300,y=y0+q*110;c.strokeStyle=lin(c,x+140,y-52,x,y,[[0,'rgba(200,220,255,0)'],[1,`rgba(220,235,255,${.9*(1-q)})`]]);c.lineWidth=1.4;c.beginPath();c.moveTo(x+140,y-52);c.lineTo(x,y);c.stroke()}
}

/* ════════════════════ VI · Blossom ════════════════════ */
function pagoda(c,x,y,s,col){c.fillStyle=col;let yy=y;for(let i=0;i<5;i++){const w=(70-i*10)*s,h=15*s;c.fillRect(x-w*.32,yy-h,w*.64,h);yy-=h;
  c.beginPath();c.moveTo(x-w*.64,yy+1*s);c.quadraticCurveTo(x-w*.42,yy-1*s,x-w*.3,yy-8*s);c.lineTo(x+w*.3,yy-8*s);c.quadraticCurveTo(x+w*.42,yy-1*s,x+w*.64,yy+1*s);c.quadraticCurveTo(x,yy-2*s,x-w*.64,yy+1*s);c.fill();yy-=8*s}
  c.fillRect(x-1.2*s,yy-30*s,2.4*s,30*s)}
function torii(c,x,y,s,col){c.fillStyle=col;const w=90*s,h=80*s;c.fillRect(x-w*.36,y-h,8*s,h);c.fillRect(x+w*.36-8*s,y-h,8*s,h);c.fillRect(x-w*.42,y-h*.78,w*.84,6*s);
  c.beginPath();c.moveTo(x-w*.58,y-h-6*s);c.quadraticCurveTo(x,y-h+4*s,x+w*.58,y-h-6*s);c.lineTo(x+w*.52,y-h+5*s);c.quadraticCurveTo(x,y-h+13*s,x-w*.52,y-h+5*s);c.closePath();c.fill()}
function pBlossom(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H*.72,[[0,'#8aa2d8'],[.32,'#c6b2dc'],[.58,'#f2bfcd'],[.82,'#ffd6bd'],[1,'#ffe4c9']]);c.fillRect(0,0,W,H);
  const sx=W*.62,sy=H*.34;glow(c,sx,sy,W*.5,'rgba(255,235,215,.55)');glow(c,sx,sy,160,'rgba(255,255,248,.7)');dot(c,sx,sy,58,'#fff9f0');
  rays(c,sx,sy,W*1.1,26,Math.PI/2,Math.PI*1.3,'255,240,225',612,.07);
  const r=rng(601);for(let i=0;i<26;i++)sf(c,'255,240,246',r()*W,H*(.08+r()*.35),300+r()*500,14+r()*30,.25+r()*.25);
  const cols=[['#e7c6da','#f0d6e2'],['#d3aacb','#e0bad3'],['#b58eb8','#c6a0c2'],['#8f6c9b','#a07ea9'],['#5f4873','#6d5682']];
  const L=[{b:.53,a:.2,f:1.5},{b:.61,a:.15,f:2.2},{b:.69,a:.14,f:2.9},{b:.79,a:.12,f:3.3},{b:.92,a:.13,f:2.4}];
  L.forEach((l,i)=>{const fn=ridge(c,W,H,{base:l.b,amp:l.a,freq:l.f,seed:602+i*5,oct:4,fill:lin(c,0,(l.b-l.a)*H,0,l.b*H+60,[[0,cols[i][1]],[1,cols[i][0]]])});
    if(i===2){const px=W*.74;pagoda(c,px,fn(px)+8,1.1,'#9a76a2')}
    if(i===1){const tr=rng(631);for(let k=0;k<40;k++){const x=tr()*W,h=10+tr()*18;dot(c,x,fn(x)+4,h*.5,'rgba(190,140,180,.7)')}}
    if(i<4){c.fillStyle=lin(c,0,(l.b-.03)*H,0,(l.b+.07)*H,[[0,'rgba(255,236,242,0)'],[.55,'rgba(255,236,242,.5)'],[1,'rgba(255,236,242,0)']]);c.fillRect(0,(l.b-.03)*H,W,H*.1)}});
  const pts=[];for(let k=0;k<=30;k++){const u=k/30;pts.push([W*.53+Math.sin(u*4.2+.6)*W*.08*u-u*W*.06,H*.7+u*u*H*.32,8+u*u*420])}
  const rv=new Path2D();rv.moveTo(pts[0][0]-pts[0][2]/2,pts[0][1]);pts.forEach(p=>rv.lineTo(p[0]-p[2]/2,p[1]));for(let k=pts.length-1;k>=0;k--)rv.lineTo(pts[k][0]+pts[k][2]/2,pts[k][1]);rv.closePath();
  c.fillStyle=lin(c,0,H*.7,0,H,[[0,'#ffe8d8'],[.4,'#f6c6d2'],[1,'#b9a4d6']]);c.fill(rv);
  c.save();c.clip(rv);c.globalCompositeOperation='lighter';sf(c,'255,250,240',pts[18][0],H*.84,120,H*.4,.45);c.globalCompositeOperation='source-over';
  c.strokeStyle='rgba(255,255,255,.4)';c.lineWidth=1;for(let i=0;i<70;i++){const y=H*(.72+r()*.28),x=W*(.25+r()*.4);c.beginPath();c.moveTo(x,y);c.lineTo(x+10+r()*40,y);c.stroke()}
  const tp=pts[23],tx=tp[0]-tp[2]*.28,tyb=tp[1]+6;c.save();c.translate(0,tyb*2);c.scale(1,-1);c.globalAlpha=.28;torii(c,tx,tyb,.85,'#c8323c');c.restore();c.restore();
  c.strokeStyle='rgba(70,45,80,.35)';c.lineWidth=2;c.stroke(rv);
  torii(c,tx,tyb,.85,'#c8323c');
  D.lanterns=[];[8,12,15,19,25].forEach((k,i)=>{const p=pts[k],s=.6+k/30,x=p[0]+(hash(i*3+1)-.5)*p[2]*.5,y=p[1]+2;
    c.fillStyle='rgba(255,190,110,.35)';c.fillRect(x-1,y+2,2,16*s);c.fillStyle='#4a2a24';c.fillRect(x-4*s,y-2*s,8*s,3*s);c.fillStyle='#ffd08a';rr(c,x-3*s,y-9*s,6*s,7*s,2*s);c.fill();sg(c,'255,180,90',x,y-6*s,40*s,.7);D.lanterns.push([x,y-6*s,s])});
  const blos=[],tr=rng(611);
  const tree=(x,y,len,ang,d,w)=>{const x2=x+Math.cos(ang)*len,y2=y+Math.sin(ang)*len;c.strokeStyle='#2b1621';c.lineWidth=w;c.lineCap='round';
    c.beginPath();c.moveTo(x,y);c.quadraticCurveTo((x+x2)/2+(tr()-.5)*len*.35,(y+y2)/2+(tr()-.5)*len*.35,x2,y2);c.stroke();
    if(d<=2)blos.push([x2,y2,d]);if(d<=0)return;const n=d>4?2:(tr()<.55?3:2);for(let i=0;i<n;i++)tree(x2,y2,len*(.66+tr()*.18),ang+(i-(n-1)/2)*(.48+tr()*.3)+(tr()-.5)*.25,d-1,w*.66)};
  tree(-30,H*1.03,215,-1.0,7,44);tree(W+30,H*.04,165,Math.PI-.3,6,30);
  c.globalCompositeOperation='lighter';blos.forEach(([x,y])=>sf(c,'255,170,200',x,y,90,90,.07));c.globalCompositeOperation='source-over';
  const pal=['#ffd8e6','#ffc2d6','#ffaac6','#fff2f6','#f592b6'];
  blos.forEach(([x,y,d])=>{const n=d===0?12:d===1?8:5;for(let k=0;k<n;k++){const a=tr()*TAU,rd=tr()*26;c.globalAlpha=.55+tr()*.45;c.fillStyle=pal[(tr()*5)|0];c.beginPath();c.arc(x+Math.cos(a)*rd,y+Math.sin(a)*rd*.8,2.5+tr()*5.5,0,TAU);c.fill()}});c.globalAlpha=1;
  finish(c,W,H,.32);
}
function aBlossom(c,t,D,px){
  const W=WW,H=HH;
  for(let i=0;i<5;i++){const y=H*(.58+i*.06),x=wrap(hash(i*4.1)*W+t*(8+i*4),W+1200)-600;sf(c,'255,240,245',x,y,900,90,.16)}
  c.strokeStyle='rgba(80,60,100,.7)';c.lineWidth=1.6;
  for(let i=0;i<4;i++){const x=wrap(hash(i*2.9)*W+t*(28+i*5),W+200)-100,y=H*(.16+hash(i*6.6)*.16)+Math.sin(t*.8+i)*8,f=Math.sin(t*7+i*2)*5,s=.7+hash(i)*.5;
    c.beginPath();c.moveTo(x-10*s,y-f*s);c.quadraticCurveTo(x-4*s,y-2*s,x,y);c.quadraticCurveTo(x+4*s,y-2*s,x+10*s,y-f*s);c.stroke()}
  for(let i=0;i<110;i++){const z=.3+hash(i*1.7)*.7,sp=(30+hash(i*2.1)*40)*z;
    const x=wrap(hash(i*5.3)*W*1.3+t*(40+z*50)+Math.sin(t*.9+i)*30,W+100)-50-px*z*25,y=wrap(hash(i*8.9)*H+t*sp+Math.sin(t*1.3+i*.7)*14,H+40)-20;
    const rot=t*(1+hash(i*3.9)*2)+i,fl=Math.abs(Math.cos(t*(1.5+hash(i)*2)+i));
    c.save();c.translate(x,y);c.rotate(rot);c.fillStyle=i%5?'#ffbed4':'#fff0f6';c.globalAlpha=.55+z*.45;c.beginPath();c.ellipse(0,0,6*z+2,(3*z+1.2)*(.3+fl*.7),0,0,TAU);c.fill();c.restore()}
  c.globalAlpha=1;
  D.lanterns.forEach(([x,y,s],i)=>sg(c,'255,170,80',x,y,50*s,.25+.15*Math.sin(t*3+i*2)*Math.sin(t*1.7+i)));
  for(let i=0;i<6;i++){const x=wrap(hash(i*6.1)*W+t*(70+i*14),W+400)-200,y=wrap(hash(i*2.3)*H+t*(30+i*6)+Math.sin(t+i)*30,H+300)-150,s=90+hash(i*9.4)*120;sf(c,'255,175,205',x-px*40,y,s,s*.8,.2)}
}

/* ════════════════════ VII · Circuit ════════════════════ */
function cube(c,x,y,s,rot){const top=[],bot=[];for(let k=0;k<4;k++){const a=rot+k*Math.PI/2,qx=x+Math.cos(a)*s*.7,qy=Math.sin(a)*s*.32;top.push([qx,y-s*.5+qy]);bot.push([qx,y+s*.5+qy])}
  const faces=[];for(let k=0;k<4;k++){const k2=(k+1)%4,mid=rot+k*Math.PI/2+Math.PI/4;faces.push({d:Math.sin(mid),p:[top[k],top[k2],bot[k2],bot[k]],l:.5+.5*Math.cos(mid)})}
  faces.sort((a,b)=>a.d-b.d);const poly=p=>{c.beginPath();p.forEach((q,i)=>i?c.lineTo(q[0],q[1]):c.moveTo(q[0],q[1]));c.closePath()};
  for(const f of faces){poly(f.p);c.globalCompositeOperation='source-over';c.fillStyle=`rgba(${30+f.l*50|0},${22+f.l*36|0},${10+f.l*14|0},.88)`;c.fill();c.globalCompositeOperation='lighter';c.strokeStyle='rgba(255,200,110,.75)';c.lineWidth=1.1;c.stroke()}
  poly(top);c.globalCompositeOperation='source-over';c.fillStyle='rgba(90,70,30,.85)';c.fill();c.globalCompositeOperation='lighter';c.strokeStyle='rgba(255,220,150,.95)';c.stroke();sg(c,'255,190,90',x,y,s*3,.25)}
function pCircuit(c,W,H,D){
  const vx=W*.5,vy=H*.5;
  c.fillStyle=lin(c,0,0,0,H,[[0,'#020308'],[.5,'#07101c'],[1,'#020306']]);c.fillRect(0,0,W,H);
  glow(c,vx,H*.48,W*.55,'rgba(255,170,60,.16)');glow(c,vx,H*.3,W*.3,'rgba(80,160,255,.1)');
  const r=rng(701);for(let i=0;i<1000;i++){const x=r()*W,y=r()*H*.62,q=r();c.fillStyle=q<.75?`rgba(255,200,110,${r()*.45})`:`rgba(120,200,255,${r()*.45})`;const s=r()<.9?1:2;c.fillRect(x|0,y|0,s,s)}
  c.strokeStyle='rgba(255,190,90,.05)';c.lineWidth=1;const hs=34;c.beginPath();for(let row=0;row<12;row++)for(let col=0;col<30;col++){const cx=col*hs*1.5,cy=row*hs*1.73+(col%2?hs*.86:0);for(let k=0;k<6;k++){const a=k*Math.PI/3,b=(k+1)*Math.PI/3;c.moveTo(cx+Math.cos(a)*hs,cy+Math.sin(a)*hs);c.lineTo(cx+Math.cos(b)*hs,cy+Math.sin(b)*hs)}}c.stroke();
  for(let i=0;i<70;i++){const x=vx+(r()-.5)*W*.16,h=10+r()*60,w=2+r()*5;c.fillStyle=`rgba(255,190,90,${.08+r()*.2})`;c.fillRect(x,vy+H*.065-h,w,h)}
  const P=(u,v,side)=>{const z=1+u*9;return[vx+side*vx/z,vy+(H*.65-v*H)/z]};const traces=[];
  [-1,1].forEach(side=>{const q=[P(0,0,side),P(1,0,side),P(1,1,side),P(0,1,side)];
    c.beginPath();q.forEach((p,i)=>i?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.closePath();c.fillStyle=lin(c,q[0][0],0,q[1][0],0,[[0,'#03060c'],[.6,'#0a1624'],[1,'#13283a']]);c.fill();
    c.save();c.clip();c.strokeStyle='rgba(120,170,220,.07)';c.lineWidth=1;c.beginPath();
    for(let v=0;v<=1;v+=.05){const a=P(0,v,side),b=P(1,v,side);c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1])}for(let u=0;u<=1;u+=.04){const a=P(u,0,side),b=P(u,1,side);c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1])}c.stroke();
    for(let i=0;i<40;i++){const u0=r()*.95,v0=r()*.95,du=.01+r()*.05,dv=.03+r()*.1,a=P(u0,v0,side),b=P(u0+du,v0,side),e=P(u0+du,v0+dv,side),d=P(u0,v0+dv,side);
      c.fillStyle=`rgba(120,170,230,${.02+r()*.05})`;c.beginPath();c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1]);c.lineTo(e[0],e[1]);c.lineTo(d[0],d[1]);c.fill()}
    c.globalCompositeOperation='lighter';
    for(let i=0;i<64;i++){let u=r()*.92,v=.05+r()*.9;const uv=[[u,v]];let horiz=r()<.5;const segs=3+(r()*5|0);
      for(let k=0;k<segs;k++){if(horiz)u=Math.max(0,Math.min(1,u+(r()<.65?1:-1)*(.02+r()*.09)));else v=Math.max(.02,Math.min(.98,v+(r()<.5?1:-1)*(.04+r()*.12)));uv.push([u,v]);horiz=!horiz}
      const pts=uv.map(([a,b])=>P(a,b,side)),zAvg=1+uv.reduce((s,p)=>s+p[0],0)/uv.length*9,w=Math.max(.5,3/zAvg),col=r()<.78?'255,190,80':'110,210,255';
      c.strokeStyle=`rgba(${col},.18)`;c.lineWidth=w*4;c.beginPath();pts.forEach((p,k)=>k?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.stroke();c.strokeStyle=`rgba(${col},.85)`;c.lineWidth=w;c.stroke();
      const e=pts[pts.length-1];c.fillStyle=`rgba(${col},.9)`;c.beginPath();c.arc(e[0],e[1],w*1.8,0,TAU);c.fill();c.beginPath();c.arc(pts[0][0],pts[0][1],w*1.4,0,TAU);c.fill();
      const cum=[0];for(let k=1;k<pts.length;k++)cum.push(cum[k-1]+Math.hypot(pts[k][0]-pts[k-1][0],pts[k][1]-pts[k-1][1]));traces.push({pts,cum,len:cum[cum.length-1],col,w})}
    c.restore();c.save();c.globalCompositeOperation='lighter';c.strokeStyle='rgba(255,200,120,.5)';c.lineWidth=1.4;c.beginPath();c.moveTo(q[3][0],q[3][1]);c.lineTo(q[2][0],q[2][1]);c.stroke();c.restore()});
  D.traces=traces;
  {const a=P(0,1,1),b=P(1,1,1),e=P(1,1,-1),f=P(0,1,-1),sk=new Path2D();sk.moveTo(-10,-10);sk.lineTo(W+10,-10);sk.lineTo(W+10,a[1]);sk.lineTo(b[0],b[1]);sk.lineTo(e[0],e[1]);sk.lineTo(-10,f[1]);sk.closePath();D.sky=sk}
  const F=[[0,vy+H*.65],[W,vy+H*.65],[vx+vx/10,vy+H*.065],[vx-vx/10,vy+H*.065]];
  c.beginPath();F.forEach((p,i)=>i?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.closePath();c.fillStyle=lin(c,0,vy+H*.065,0,H,[[0,'#0d1824'],[1,'#020409']]);c.fill();
  c.save();c.clip();c.globalCompositeOperation='lighter';c.strokeStyle='rgba(255,190,90,.12)';c.lineWidth=1;c.beginPath();
  for(let z=1;z<=10;z*=1.18){const y=vy+H*.65/z;c.moveTo(vx-vx/z,y);c.lineTo(vx+vx/z,y)}for(let k=-10;k<=10;k++){c.moveTo(vx+k*vx/100,vy+H*.065);c.lineTo(vx+k*vx/10,vy+H*.65)}c.stroke();
  sf(c,'255,200,110',vx,H*.78,70,H*.45,.35);sf(c,'255,170,70',vx,H*.62,400,90,.25);c.restore();
  const by0=vy+H*.06,mt=H*.33;D.beam=[vx,mt,-20];
  c.save();c.globalCompositeOperation='lighter';sf(c,'255,190,90',vx,mt*.5,140,mt*1.4,.35);c.fillStyle=lin(c,0,0,0,mt,[[0,'rgba(255,220,150,.2)'],[1,'rgba(255,240,200,.9)']]);c.fillRect(vx-3,-20,6,mt+20);c.restore();
  c.fillStyle=lin(c,vx-34,0,vx+34,0,[[0,'#05070b'],[.5,'#141b24'],[1,'#030407']]);c.fillRect(vx-34,mt,68,by0-mt);
  c.save();c.globalCompositeOperation='lighter';c.fillStyle='rgba(255,210,140,.9)';c.fillRect(vx-1,mt,2,by0-mt);c.strokeStyle='rgba(255,200,120,.5)';c.lineWidth=1;c.strokeRect(vx-34,mt,68,by0-mt);sg(c,'255,230,170',vx,mt,150,.9);c.restore();
  D.cubes=[[W*.3,H*.42,24],[W*.7,H*.36,32],[W*.62,H*.58,16],[W*.37,H*.6,18],[W*.18,H*.18,40],[W*.83,H*.17,30]];
  finish(c,W,H,.55);
}
function aCircuit(c,t,D,px){
  const H=HH;c.globalCompositeOperation='lighter';
  D.traces.forEach((tr,i)=>{const p=wrap(t*(.25+hash(i*1.3)*.35)+hash(i*7.7),1.6);if(p>1)return;const d=p*tr.len;let k=1;while(k<tr.cum.length-1&&tr.cum[k]<d)k++;
    const a=tr.pts[k-1],b=tr.pts[k],f=(d-tr.cum[k-1])/Math.max(1e-6,tr.cum[k]-tr.cum[k-1]);sg(c,tr.col,a[0]+(b[0]-a[0])*f,a[1]+(b[1]-a[1])*f,tr.w*14,.9);
    if(p>.94){const e=tr.pts[tr.pts.length-1];sg(c,tr.col,e[0],e[1],tr.w*30,(p-.94)*16)}});
  const [bx,b0,b1]=D.beam,pu=.6+.4*Math.sin(t*2.2);
  sf(c,'255,200,110',bx,(b0+b1)/2,60+pu*30,b0-b1+200,.25*pu);c.globalAlpha=.8;c.fillStyle='#fff7e0';c.fillRect(bx-1.5,b1,3,b0-b1);
  c.lineWidth=1.5;c.strokeStyle='#ffd27a';for(let i=0;i<5;i++){const p=wrap(t*.12+i/5,1),y=b0-(b0-b1)*p,rw=40+p*80;c.globalAlpha=(1-p)*.7;c.beginPath();c.ellipse(bx,y,rw,rw*.18,0,0,TAU);c.stroke()}
  for(let i=0;i<90;i++){const p=wrap(t*(.05+hash(i)*.08)+hash(i*3.1),1),ang=hash(i*5.5)*TAU+t*.3,r0=30+hash(i*2.7)*260*(1-p*.6),x=bx+Math.cos(ang)*r0,y=H*.6-(H*.6-b1)*p;
    c.globalAlpha=Math.sin(p*Math.PI)*.8;c.fillStyle=i%6?'#ffd27a':'#8fe0ff';c.fillRect(x,y,2,2)}
  c.globalAlpha=1;
  c.save();c.clip(D.sky);c.fillStyle='#ffc86a';
  for(let i=0;i<46;i++){const x=(i+.5)*WW/46,sp=60+hash(i*3.3)*120,head=wrap(t*sp+hash(i*7.7)*H,H*1.3)-H*.1;
    for(let k=0;k<14;k++){const y=head-k*13;if(y<-10)break;c.globalAlpha=(1-k/14)*.26*(k?1:2.4);c.fillRect(x-2,y,hash(i*31+k+Math.floor(t*4+i))>.5?4:2.5,8)}}
  c.globalAlpha=1;c.restore();
  D.cubes.forEach(([x,y,s],i)=>cube(c,x-px*s*.4,y+Math.sin(t*.8+i)*12,s,t*.25+i));
  c.globalCompositeOperation='source-over';
}

/* ════════════════════ VIII · Hollow ════════════════════ */
function crystal(c,x,y,h,w,ang,P,G){c.save();c.translate(x,y);c.rotate(ang);
  const tipY=-h,shY=-h*.78,hw=w/2,off=w*.06;
  c.beginPath();c.moveTo(-hw,0);c.lineTo(-hw,shY);c.lineTo(off,tipY);c.lineTo(off*.4,0);c.closePath();c.fillStyle=lin(c,-hw,0,off,tipY,[[0,P[2]],[.6,P[1]],[1,P[0]]]);c.fill();
  c.beginPath();c.moveTo(off*.4,0);c.lineTo(off,tipY);c.lineTo(hw,shY);c.lineTo(hw,0);c.closePath();c.fillStyle=lin(c,hw,0,off,tipY,[[0,P[3]],[.5,P[2]],[1,P[1]]]);c.fill();
  c.globalCompositeOperation='lighter';c.fillStyle=lin(c,0,0,0,tipY,[[0,`rgba(${P[4]},0)`],[.5,`rgba(${P[4]},.22)`],[1,`rgba(${P[4]},.6)`]]);
  c.beginPath();c.moveTo(-hw,0);c.lineTo(-hw,shY);c.lineTo(off,tipY);c.lineTo(hw,shY);c.lineTo(hw,0);c.closePath();c.fill();
  c.strokeStyle=`rgba(${P[4]},.85)`;c.lineWidth=1.2;c.stroke();c.beginPath();c.moveTo(off,tipY);c.lineTo(off*.4,0);c.stroke();
  c.strokeStyle='rgba(255,255,255,.5)';c.lineWidth=2;c.beginPath();c.moveTo(-hw+w*.18,-h*.1);c.lineTo(-hw+w*.18,shY+h*.04);c.stroke();
  const m=c.getTransform();[[off,tipY],[-hw,shY]].forEach(([a,b])=>{const p=m.transformPoint(new DOMPoint(a,b));G.push([p.x,p.y,P[4]])});
  c.restore()}
function pHollow(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H,[[0,'#05030b'],[.55,'#120827'],[1,'#05020a']]);c.fillRect(0,0,W,H);
  const r=rng(801);for(let i=0;i<240;i++)sf(c,r()<.55?'46,22,80':'8,4,16',r()*W,r()*H,60+r()*280,40+r()*220,.22);
  c.globalCompositeOperation='lighter';sf(c,'150,80,255',W*.5,H*.58,W*1.1,H*.9,.28);sf(c,'40,220,200',W*.16,H*.8,W*.5,H*.5,.14);c.globalCompositeOperation='source-over';
  ridge(c,W,H,{base:.8,amp:.2,freq:4,seed:802,sharp:true,oct:4,fill:'rgba(20,10,40,.75)'});
  c.save();c.globalCompositeOperation='lighter';c.fillStyle=lin(c,0,0,0,H*.8,[[0,'rgba(235,215,255,.4)'],[1,'rgba(200,170,255,0)']]);
  c.beginPath();c.moveTo(W*.54,0);c.lineTo(W*.59,0);c.lineTo(W*.63,H*.8);c.lineTo(W*.4,H*.8);c.closePath();c.filter='blur(16px)';c.fill();c.filter='none';c.restore();
  sg(c,'240,220,255',W*.565,0,300,.8);
  const drips=[];for(let i=0;i<46;i++){const x=r()*W;if(x>W*.5&&x<W*.62)continue;const l=40+Math.pow(r(),1.5)*240,w=12+r()*46;
    c.fillStyle=lin(c,x-w/2,0,x+w/2,0,[[0,'#0a0614'],[.4,'#22143c'],[1,'#07040d']]);c.beginPath();c.moveTo(x-w/2,-5);c.quadraticCurveTo(x-w*.15,l*.6,x+(r()-.5)*6,l);c.quadraticCurveTo(x+w*.2,l*.55,x+w/2,-5);c.fill();
    if(drips.length<4&&l>130&&x>W*.25&&x<W*.8)drips.push([x,l])}
  D.drips=drips;
  const G=[],PAL={am:['#f3e6ff','#b98cff','#5b2bb0','#24104f','205,160,255'],te:['#e6fffb','#5ff0dc','#0f7f7a','#06302f','130,255,235'],ro:['#ffe9f4','#ff9ccf','#a8326f','#3d0f28','255,160,215']};
  const cluster=(x,y,n,hM,wM,spread,P,seed,base=0)=>{const g=rng(seed),list=[];for(let i=0;i<n;i++){const a=(n>1?(i/(n-1)-.5):0)*spread+(g()-.5)*.2;list.push({a,h:hM*(.45+g()*.55)*(1-Math.abs(a)*.35),w:wM*(.55+g()*.45),dx:a*wM*.55})}
    list.sort((p,q)=>q.h-p.h);c.globalCompositeOperation='lighter';sf(c,P[4],x,y-Math.cos(base)*hM*.3,wM*6,hM*1.4,.22);c.globalCompositeOperation='source-over';
    list.forEach(k=>crystal(c,x+k.dx,y,k.h,k.w,base+k.a,P,G));c.fillStyle='#07040e';c.beginPath();c.ellipse(x,y+6,wM*1.6,16,0,0,TAU);c.fill()};
  cluster(W*.22,-10,5,220,58,1.1,PAL.am,817,Math.PI);cluster(W*.8,-10,4,180,50,1.0,PAL.te,818,Math.PI);
  cluster(W*.5,H*.78,9,440,92,1.35,PAL.am,811);cluster(W*.15,H*.86,7,300,70,1.5,PAL.te,812);cluster(W*.86,H*.85,7,330,72,1.45,PAL.am,813);
  cluster(W*.33,H*.83,4,150,46,1.1,PAL.ro,814);cluster(W*.68,H*.82,5,180,50,1.2,PAL.te,815);cluster(W*.04,H*.74,3,120,40,.9,PAL.ro,816);
  const mush=(x,y,s,rgb,seed)=>{const g=rng(seed);for(let i=0;i<5;i++){const mx=x+(g()-.5)*60*s,h=(18+g()*40)*s,cw=(10+g()*16)*s,lean=(g()-.5)*.4,tx=mx+lean*h,ty=y-h;
    c.strokeStyle=`rgba(${rgb},.55)`;c.lineWidth=Math.max(1.5,cw*.22);c.lineCap='round';c.beginPath();c.moveTo(mx,y);c.quadraticCurveTo(mx,y-h*.6,tx,ty);c.stroke();
    c.fillStyle=rad(c,tx,ty,cw,[[0,'rgba(255,255,255,.95)'],[.35,`rgba(${rgb},.9)`],[1,`rgba(${rgb},.25)`]],tx,ty-cw*.3);c.beginPath();c.ellipse(tx,ty,cw,cw*.55,0,Math.PI,TAU);c.quadraticCurveTo(tx,ty+cw*.2,tx-cw,ty);c.fill();
    sg(c,rgb,tx,ty,cw*5,.45)}};
  mush(W*.24,H*.87,1,'90,255,220',841);mush(W*.76,H*.865,.9,'120,200,255',842);mush(W*.42,H*.865,.6,'255,140,220',843);
  const wall=(side,seed)=>{const n=noise1(seed),x0=side<0?-10:W+10;c.beginPath();c.moveTo(x0,-10);for(let y=-10;y<=H+10;y+=8){const w=W*(.03+.07*fbm(n,y/H*3,4));c.lineTo(side<0?w:W-w,y)}c.lineTo(x0,H+10);c.closePath();c.fillStyle='#040209';c.fill()};
  wall(-1,821);wall(1,822);
  {const vr=rng(845);c.save();c.globalCompositeOperation='lighter';c.lineWidth=1.2;
   for(let i=0;i<14;i++){const side=i%2?1:-1,col=i%3?'170,110,255':'90,255,220';let x=side<0?W*(.01+vr()*.05):W*(.94+vr()*.05),y=vr()*H*.8;c.strokeStyle=`rgba(${col},.5)`;c.beginPath();c.moveTo(x,y);
     for(let k=0;k<12;k++){x+=(vr()-.5)*22;y+=6+vr()*18;c.lineTo(x,y)}c.stroke();sg(c,col,x,y,18,.6)}c.restore()}
  const py=H*.865;D.poolY=py;reflect(c,W,H,py,831,8,'10,4,24');
  c.globalCompositeOperation='lighter';c.fillStyle='rgba(200,160,255,.35)';c.fillRect(0,py,W,1);c.globalCompositeOperation='source-over';
  D.glints=G;finish(c,W,H,.6);
}
function aHollow(c,t,D,px){
  const W=WW,H=HH;c.globalCompositeOperation='lighter';
  D.glints.forEach(([x,y,col],i)=>{const b=Math.pow(Math.max(0,Math.sin(t*(.5+hash(i)*.9)+hash(i*3)*20)),14);if(b<.02)return;sg(c,col,x,y,28,b);
    c.globalAlpha=b*.9;c.fillStyle='#fff';c.fillRect(x-14*b-2,y-.6,28*b+4,1.2);c.fillRect(x-.6,y-14*b-2,1.2,28*b+4);c.globalAlpha=1});
  for(let i=0;i<80;i++){const z=hash(i*2.2),y=wrap(H-(t*(8+z*16)+hash(i*4.4)*H),H),x=hash(i*6.1)*W+Math.sin(t*.4+i)*30*z;sg(c,i%3?'190,140,255':'110,255,230',x-px*z*20,y,6+z*10,(.25+z*.45)*(.6+.4*Math.sin(t*2+i)))}
  D.drips.forEach(([x,y0],i)=>{const per=5+i*1.3,p=wrap(t+i*1.9,per),fall=.9;
    if(p<fall)sg(c,'210,180,255',x,y0+(D.poolY+8-y0)*Math.pow(p/fall,2),9,.85);
    else{const q=(p-fall)/2.4;if(q<1){c.strokeStyle='#d2b4ff';c.lineWidth=1.2;for(let k=0;k<3;k++){const qq=q-k*.12;if(qq<=0)continue;c.globalAlpha=(1-qq)*.6;c.beginPath();c.ellipse(x,D.poolY+14,qq*90,qq*14,0,0,TAU);c.stroke()}c.globalAlpha=1}}});
  sf(c,'220,200,255',W*.55,H*.35,170,H*.8,.06+.04*Math.sin(t*.7));
  c.globalCompositeOperation='source-over';
}

/* ════════════════════ IX · Frontier ════════════════════ */
function dome(c,x,y,R,D){c.save();c.beginPath();c.ellipse(x,y,R,R*.92,0,Math.PI,TAU);c.closePath();
  c.fillStyle=rad(c,x,y,R,[[0,'rgba(255,200,130,.85)'],[.5,'rgba(160,90,60,.55)'],[1,'rgba(60,30,25,.7)']],x,y);c.fill();c.clip();
  c.strokeStyle='rgba(255,230,200,.33)';c.lineWidth=1;for(let k=1;k<6;k++){const yy=y-R*.92*k/6,rx=R*Math.sqrt(1-(k/6)**2);c.beginPath();c.moveTo(x-rx,yy);c.lineTo(x+rx,yy);c.stroke()}
  for(let k=-5;k<=5;k++){c.beginPath();c.ellipse(x,y,Math.abs(R*k/5.5),R*.92,0,Math.PI,TAU);c.stroke()}
  c.fillStyle=lin(c,x-R,y-R,x+R,y,[[0,'rgba(255,240,220,.35)'],[.5,'rgba(255,240,220,0)']]);c.fillRect(x-R,y-R,R*2,R);c.restore();
  c.strokeStyle='rgba(255,220,190,.6)';c.lineWidth=1.5;c.beginPath();c.ellipse(x,y,R,R*.92,0,Math.PI,TAU);c.stroke();c.fillStyle='#2a140e';c.fillRect(x-R-4,y-3,R*2+8,6);D.domes.push([x,y-R*.3,R])}
function pFrontier(c,W,H,D){
  c.fillStyle=lin(c,0,0,0,H*.68,[[0,'#120a12'],[.28,'#3a1d22'],[.58,'#9e553a'],[.84,'#d6956a'],[1,'#e8b38c']]);c.fillRect(0,0,W,H);
  stars(c,W,H,320,901,.3,.45);
  {const cr=rng(907);c.save();c.globalCompositeOperation='lighter';for(let i=0;i<22;i++){const x=cr()*W,y=H*(.12+cr()*.25);c.save();c.translate(x,y);c.rotate(-.08+cr()*.06);sf(c,'255,200,170',0,0,300+cr()*500,6+cr()*14,.06+cr()*.08);c.restore()}c.restore()}
  const sx=W*.29,sy=H*.53;D.sun=[sx,sy];
  glow(c,sx,sy,W*.42,'rgba(255,190,140,.25)');glow(c,sx,sy,190,'rgba(140,180,255,.5)');glow(c,sx,sy,60,'rgba(220,235,255,.85)');dot(c,sx,sy,12,'#f6f9ff');
  c.save();c.translate(W*.78,H*.15);c.rotate(.5);c.fillStyle='#d6c0ab';c.beginPath();c.ellipse(0,0,16,11,0,0,TAU);c.fill();c.fillStyle='rgba(40,18,14,.75)';c.beginPath();c.ellipse(5,1,13,10.5,0,0,TAU);c.fill();c.restore();
  dot(c,W*.62,H*.09,2.6,'#ead9c6');
  band(c,W,H*.6,H*.08,'rgba(235,160,110,.25)');
  ridge(c,W,H,{base:.67,amp:.16,freq:2.4,seed:902,mesa:.58,oct:4,fill:'rgba(152,82,58,.78)'});
  band(c,W,H*.66,H*.05,'rgba(235,160,115,.22)');
  ridge(c,W,H,{base:.74,amp:.1,freq:3.1,seed:903,mesa:.55,oct:4,fill:'#7c3b29',rim:'rgba(255,190,140,.22)'});
  const pl=ridge(c,W,H,{base:.8,amp:.025,freq:2,seed:904,oct:3,fill:lin(c,0,H*.77,0,H,[[0,'#5c2b1d'],[1,'#2a120c']])});
  D.domes=[];D.padLights=[];const g=x=>pl(x)+3;
  c.fillStyle='#8a6656';c.fillRect(W*.6,g(W*.6)-14,W*.16,10);c.fillStyle='rgba(255,220,190,.35)';c.fillRect(W*.6,g(W*.6)-14,W*.16,1.5);
  dome(c,W*.67,g(W*.67),84,D);dome(c,W*.755,g(W*.755),56,D);dome(c,W*.61,g(W*.61),40,D);
  for(let i=0;i<3;i++){const x=W*(.705+i*.022);c.fillStyle='#6e4c3e';c.fillRect(x,g(x)-22,28,22);c.fillStyle='#ffd49a';c.fillRect(x+5,g(x)-15,6,4);c.fillRect(x+16,g(x)-15,6,4)}
  const dx=W*.58,dy=g(dx);c.strokeStyle='#5a3a2e';c.lineWidth=3;c.beginPath();c.moveTo(dx,dy);c.lineTo(dx,dy-50);c.stroke();
  c.save();c.translate(dx,dy-52);c.rotate(-.6);c.fillStyle=lin(c,-22,0,22,0,[[0,'#e8d8cc'],[1,'#7a6258']]);c.beginPath();c.ellipse(0,0,24,9,0,0,Math.PI);c.fill();c.strokeStyle='#cbb';c.lineWidth=1.5;c.beginPath();c.moveTo(0,0);c.lineTo(0,-14);c.stroke();c.restore();
  const rx=W*.87,ry=g(rx),bw=30,bh=250;c.fillStyle='#24110b';c.fillRect(rx-60,ry-6,120,8);
  c.fillStyle=lin(c,rx-bw/2,0,rx+bw/2,0,[[0,'#f3ece6'],[.55,'#bfb0a6'],[1,'#5b4a43']]);c.beginPath();c.moveTo(rx-bw/2,ry-6);c.lineTo(rx-bw/2,ry-bh);c.quadraticCurveTo(rx-bw/2,ry-bh-50,rx,ry-bh-70);c.quadraticCurveTo(rx+bw/2,ry-bh-50,rx+bw/2,ry-bh);c.lineTo(rx+bw/2,ry-6);c.closePath();c.fill();
  c.fillStyle='#1a1210';c.fillRect(rx-bw/2,ry-bh*.62,bw,8);c.fillRect(rx-bw/2,ry-bh*.2,bw,5);
  c.fillStyle='#4a3a34';c.beginPath();c.moveTo(rx-bw/2,ry-6);c.lineTo(rx-bw/2-16,ry-6);c.lineTo(rx-bw/2,ry-46);c.fill();c.beginPath();c.moveTo(rx+bw/2,ry-6);c.lineTo(rx+bw/2+16,ry-6);c.lineTo(rx+bw/2,ry-46);c.fill();
  c.fillStyle='#ffe2b0';c.beginPath();c.arc(rx-3,ry-bh+10,3,0,TAU);c.fill();
  const gx=rx+30;c.strokeStyle='#3a221a';c.lineWidth=2;c.strokeRect(gx,ry-bh-20,18,bh+14);c.lineWidth=1;c.beginPath();for(let y=ry-6;y>ry-bh-20;y-=16){c.moveTo(gx,y);c.lineTo(gx+18,y-16);c.moveTo(gx+18,y);c.lineTo(gx,y-16)}c.stroke();
  c.lineWidth=3;c.beginPath();c.moveTo(gx,ry-bh*.7);c.lineTo(rx+bw/2,ry-bh*.7);c.stroke();
  D.beacon=[gx+9,ry-bh-24];D.rocket=[rx,ry];for(let i=0;i<6;i++)D.padLights.push([rx-55+i*22,ry-7]);
  band(c,W,H*.8,H*.03,'rgba(230,150,110,.15)');
  const fg=ridge(c,W,H,{base:.93,amp:.08,freq:3,seed:905,oct:5,fill:lin(c,0,H*.84,0,H,[[0,'#3c1b10'],[1,'#130705']])});
  const vx=W*.3,vy=fg(W*.3)+18;D.rover=[vx+58,vy-31];
  const r=rng(906);
  for(let i=0;i<6;i++){const x=W*(.05+r()*.9),y=H*(.9+r()*.07),w=30+r()*60;if(Math.abs(x-vx)<120)continue;c.fillStyle='rgba(20,8,4,.5)';c.beginPath();c.ellipse(x,y,w,w*.2,0,0,TAU);c.fill();c.strokeStyle='rgba(210,130,90,.3)';c.lineWidth=2;c.beginPath();c.ellipse(x,y,w,w*.2,0,.1,Math.PI-.1);c.stroke()}
  for(let i=0;i<70;i++){const x=r()*W,yb=fg(x)+r()*(H-fg(x)),s=Math.max(3,(4+r()*20)*(.5+(yb-H*.85)/(H*.15)));if(Math.abs(x-vx)<100&&yb<vy+24)continue;
    c.fillStyle=lin(c,x-s,yb-s,x+s,yb,[[0,'#8a4c34'],[.45,'#4a2216'],[1,'#1c0b06']]);c.beginPath();for(let k=0;k<7;k++){const a=Math.PI+k/6*Math.PI,r0=s*(.7+r()*.4),qx=x+Math.cos(a)*r0,qy=yb+Math.sin(a)*r0*.7;if(k)c.lineTo(qx,qy);else c.moveTo(qx,qy)}c.closePath();c.fill()}
  c.strokeStyle='rgba(20,8,4,.5)';c.lineWidth=3;c.setLineDash([5,4]);for(const o of [-10,10]){c.beginPath();c.moveTo(vx-40,vy+o*.3);c.quadraticCurveTo(vx-200,vy+20+o,vx-420,vy+120+o*1.5);c.stroke()}c.setLineDash([]);
  c.fillStyle='#2a1610';c.beginPath();c.ellipse(vx,vy+4,80,10,0,0,TAU);c.fill();
  c.fillStyle=lin(c,0,vy-44,0,vy-14,[[0,'#ece4dc'],[1,'#8a7a70']]);c.fillRect(vx-55,vy-44,110,26);
  c.fillStyle='#24345a';c.fillRect(vx-60,vy-52,120,8);c.strokeStyle='rgba(140,180,255,.4)';c.lineWidth=1;c.beginPath();for(let k=-60;k<60;k+=12){c.moveTo(vx+k,vy-52);c.lineTo(vx+k,vy-44)}c.stroke();
  c.fillStyle='#d8d0c8';c.fillRect(vx+30,vy-90,4,38);c.fillRect(vx+24,vy-98,18,10);c.fillStyle='#111';c.fillRect(vx+36,vy-95,5,4);
  for(const k of [-42,0,42]){c.fillStyle='#1a0f0c';c.beginPath();c.arc(vx+k,vy-8,12,0,TAU);c.fill();c.fillStyle='#6a5a52';c.beginPath();c.arc(vx+k,vy-8,4,0,TAU);c.fill();c.strokeStyle='#3a2a24';c.lineWidth=2;c.beginPath();c.moveTo(vx+k,vy-8);c.lineTo(vx+k,vy-18);c.stroke()}
  c.fillStyle='#fff3d6';c.fillRect(vx+54,vy-34,4,6);
  finish(c,W,H,.45);
}
function aFrontier(c,t,D){
  const W=WW,H=HH;
  const ddx=W*(.16+.07*Math.sin(t*.07)),ddy=H*.87;for(let k=0;k<16;k++){const u=k/15,y=ddy-u*H*.32,x=ddx+Math.sin(t*1.3+u*5)*14*u+u*40,w=10+u*70;sf(c,'200,130,90',x,y,w*2,18+u*16,.05+(1-u)*.05)}
  {const [rx,ry]=D.rocket;for(let i=0;i<10;i++){const p=wrap(t*.25+i/10,1);sf(c,'230,220,215',rx-30-p*160,ry-10-p*50+Math.sin(t+i)*4,30+p*120,20+p*70,(1-p)*.22)}}
  for(let i=0;i<5;i++){const y=H*(.62+i*.08),x=wrap(W+400-(t*(30+i*14)+hash(i*3.3)*W),W+1400)-700;sf(c,'220,140,95',x,y,1100,120+i*30,.12)}
  c.strokeStyle='rgba(240,170,120,.35)';c.lineWidth=1;c.beginPath();
  for(let i=0;i<160;i++){const z=hash(i*2.9),y=H*(.7+z*.3)+Math.sin(t*2+i)*3,x=wrap(hash(i*7.3)*W-t*(260+z*420),W+60)-30,l=8+z*30;c.moveTo(x,y);c.lineTo(x+l,y-l*.05)}c.stroke();
  const b=wrap(t,1.4);sg(c,'255,60,50',D.beacon[0],D.beacon[1],b<.2?54:16,b<.2?1:.4);
  D.padLights.forEach((p,i)=>{const on=wrap(t*2-i*.15,2)<.25;sg(c,'255,190,90',p[0],p[1],on?22:8,on?.9:.35)});
  c.globalCompositeOperation='lighter';D.domes.forEach(([x,y,R],i)=>sf(c,'255,190,120',x,y,R*2.6,R*1.4,.12+.06*Math.sin(t*.9+i)));
  const [rx,ry]=D.rover;sg(c,'255,250,230',rx,ry,28,.9);c.globalAlpha=.09+.02*Math.sin(t*9);c.fillStyle=lin(c,rx,0,rx+280,0,[[0,'rgba(255,245,220,1)'],[1,'rgba(255,245,220,0)']]);
  c.beginPath();c.moveTo(rx,ry);c.lineTo(rx+280,ry-34);c.lineTo(rx+280,ry+44);c.closePath();c.fill();c.globalAlpha=1;
  const a=t*.35,dx=W*.7+Math.cos(a)*W*.1,dy=H*.58+Math.sin(a*2)*H*.04;sg(c,'180,230,255',dx,dy,14,.9);if(wrap(t,1)<.12)sg(c,'255,80,80',dx,dy,32,.8);
  sg(c,'220,235,255',D.sun[0],D.sun[1],64+6*Math.sin(t*1.7),.32);
  c.globalCompositeOperation='source-over';
}

/* ════════════════════ Worlds ════════════════════ */
const petal=[0,72,144,216,288].map(a=>`<path transform="rotate(${a} 12 12)" d="M12 11.2C9.8 9.6 9.3 6.4 10.9 4.2L12 5.2l1.1-1C14.7 6.4 14.2 9.6 12 11.2z"/>`).join('');
const ICON={
  city:'<path d="M3 21h18"/><path d="M6 21V9l3-1.5V21"/><path d="M10.5 21V3.5L14 2v19"/><path d="M15.5 21V8.5H19V21"/><path d="M12.2 6v1M12.2 9.5v1M12.2 13v1M7.5 12v1M17.2 12v1"/>',
  aurora:'<path d="M3 20l5.5-8 3 4.2 2.2-3 5.3 6.8"/><path d="M3 20h18"/><path d="M3 9.5c2.5-2.6 5-.2 7.5-2.2s5-2 7-3.8 2.5-1 3.5-1.5"/><path d="M4 12.5c2.3-1.8 4.3.2 6.7-1.4s4.5-1.5 6.3-2.6 2.2-.7 3-1" opacity=".6"/>',
  horizon:'<path d="M5.5 12a6.5 6.5 0 0 1 13 0"/><path d="M6.2 9.6h11.6M7.8 7.6h8.4"/><path d="M2.5 12h19"/><path d="M12 12v9M8.5 12 4 21M15.5 12 20 21M6 15h12M4.6 18h14.8" opacity=".7"/>',
  reef:'<path d="M5.5 11a6.5 6.5 0 0 1 13 0"/><path d="M5.5 11c1 .8 2 .8 3.2 0 1.1.8 2.2.8 3.3 0 1.1.8 2.2.8 3.3 0 1.2.8 2.2.8 3.2 0"/><path d="M8 12c-.6 2.6.6 4-.2 7.5M12 12v9M16 12c.6 2.6-.6 4 .2 7.5"/><path d="M10 12.2c0 2.4.8 3.6.2 6M14 12.2c0 2.4-.8 3.6-.2 6" opacity=".6"/>',
  orbit:'<circle cx="12" cy="12" r="5"/><ellipse cx="12" cy="12" rx="10" ry="3.3" transform="rotate(-22 12 12)"/><circle cx="19.2" cy="4.8" r=".9"/><path d="M4.5 4.5v1.6M3.7 5.3h1.6" opacity=".7"/>',
  blossom:petal+'<circle cx="12" cy="12" r="1.1"/>',
  circuit:'<rect x="7" y="7" width="10" height="10" rx="1.6"/><rect x="10" y="10" width="4" height="4" rx=".6"/><path d="M10 3.5V7M14 3.5V7M10 17v3.5M14 17v3.5M3.5 10H7M3.5 14H7M17 10h3.5M17 14h3.5"/>',
  hollow:'<path d="M12 2.5 15.5 7v9.5L12 21.5l-3.5-5V7z"/><path d="M8.5 7 12 8.8 15.5 7M12 8.8v12.7"/><path d="M5 19V13l1.6-2.6L8.2 13" opacity=".7"/><path d="M15.8 13.2l1.6-2.4 1.6 2.4V19" opacity=".7"/>',
  frontier:'<path d="M12 2.5c2.8 2.3 3.9 5.6 3.9 9.3L14.5 16h-5l-1.4-4.2c0-3.7 1.1-7 3.9-9.3z"/><circle cx="12" cy="9" r="1.6"/><path d="M8.3 12.5 5.5 16.5l4 .3M15.7 12.5l2.8 4-4 .3"/><path d="M10.7 18.5c.2 1.4 1.3 2.8 1.3 2.8s1.1-1.4 1.3-2.8"/>'
};
const WORLDS=[
  {name:'City Pulse',sub:'Demand forecasting for living cities',tag:'Forecasting · Cities',accent:'#2ee6ff',pos:'50% 40%',scale:1.35,paint:pCity,icon:ICON.city,bloom:0.42,anim:aCity},
  {name:'Aurora Watch',sub:'Anomalies surface before the storm',tag:'Monitoring · Anomaly',accent:'#5dff9d',pos:'50% 36%',scale:1.3,paint:pAurora,icon:ICON.aurora,bloom:0.38,anim:aAurora},
  {name:'Horizon Studio',sub:'Generative visuals, on brand and on cue',tag:'Generative · Creative',accent:'#ff4fd8',pos:'50% 50%',scale:1.3,paint:pGrid,icon:ICON.horizon,bloom:0.4,anim:aGrid},
  {name:'Deep Reef',sub:'Search everything your team knows',tag:'Search · Knowledge',accent:'#4aa8ff',pos:'50% 55%',scale:1.25,paint:pReef,icon:ICON.reef,bloom:0.32,anim:aReef},
  {name:'Orbit Vision',sub:'Earth imagery, read by machine',tag:'Vision · Geospatial',accent:'#c9d6ff',pos:'62% 44%',scale:1.35,paint:pOrbit,icon:ICON.orbit,bloom:0.4,anim:aOrbit},
  {name:'Bloom Coach',sub:'A coach that grows with every team',tag:'Coaching · People',accent:'#ffb3cf',pos:'46% 50%',scale:1.25,paint:pBlossom,light:true,icon:ICON.blossom,bloom:0.12,anim:aBlossom},
  {name:'Circuit Forge',sub:'Agents that write, test and ship code',tag:'Code · Agents',accent:'#ffc23d',pos:'50% 42%',scale:1.4,paint:pCircuit,icon:ICON.circuit,bloom:0.45,anim:aCircuit},
  {name:'Crystal Lens',sub:'Clarity from every contract and form',tag:'Documents · Extraction',accent:'#a77bff',pos:'50% 62%',scale:1.3,paint:pHollow,icon:ICON.hollow,bloom:0.42,anim:aHollow},
  {name:'Frontier Lab',sub:'Research agents for the edge of science',tag:'Research · Science',accent:'#ff6a33',pos:'70% 64%',scale:1.55,paint:pFrontier,icon:ICON.frontier,bloom:0.26,anim:aFrontier},
];
const N=WORLDS.length,STEP=TAU/N,ROMAN=['I','II','III','IV','V','VI','VII','VIII','IX'];

/* ════════════════════ DOM ════════════════════ */
const $=s=>document.querySelector(s);
const root=document.documentElement,stage=$('#stage'),bgwrap=$('#bgwrap'),orbit=$('#orbit'),track=$('#track'),arcring=$('#arcring'),glowEl=$('#glow');
const nameEl=$('#name'),subEl=$('#sub'),tagEl=$('#tag'),titleEl=$('#title'),curEl=$('#cur'),segsEl=$('#segs');
const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
$('#ldMark').innerHTML=[...'Orrery'].map((ch,i)=>`<span style="animation-delay:${i*.05}s">${ch}</span>`).join('');

const bgs=[],meds=[],segs=[],built=new Array(N).fill(false);
WORLDS.forEach((w,i)=>{
  w.D={};
  const b=document.createElement('div');b.className='bg';bgwrap.appendChild(b);bgs.push(b);
  const m=document.createElement('div');m.className='med';m.tabIndex=0;m.setAttribute('role','button');m.setAttribute('aria-label',w.name);m.dataset.index=i;
  m.innerHTML=`<div class="med-halo"></div><div class="med-face"><div class="med-base" style="background-position:${w.pos};transform:scale(${w.scale})"></div><div class="med-img" style="background-position:${w.pos};transform:scale(${w.scale})"></div><div class="med-tint"></div></div><div class="med-emblem"><svg viewBox="0 0 24 24" aria-hidden="true">${w.icon}</svg></div><div class="med-rim"></div>`;m.style.setProperty('--c',w.accent);
  orbit.appendChild(m);meds.push(m);
  const s=document.createElement('button');s.className='seg';s.type='button';s.setAttribute('role','tab');s.setAttribute('aria-label',w.name);s.innerHTML='<i></i>';
  s.addEventListener('click',()=>{goTo(i);userTouched()});segsEl.appendChild(s);segs.push(s);
  const l=document.createElement('button');l.type='button';l.textContent=w.name;l.addEventListener('click',()=>{route('home');goTo(i)});$('#worldList').appendChild(l);
});

(()=>{const g=document.createElement('canvas');g.width=g.height=180;const x=g.getContext('2d'),d=x.createImageData(180,180);
  for(let i=0;i<d.data.length;i+=4){const v=Math.random()*255;d.data[i]=d.data[i+1]=d.data[i+2]=v;d.data[i+3]=255}
  x.putImageData(d,0,0);$('#grain').style.backgroundImage=`url(${g.toDataURL()})`})();

(()=>{const n=256,cv=document.createElement('canvas');cv.width=cv.height=n;const x=cv.getContext('2d'),d=x.createImageData(n,n);
  for(let j=0;j<n;j++)for(let i=0;i<n;i++){const u=(i+.5)/n*2-1,v=(j+.5)/n*2-1,r=Math.min(1,Math.hypot(u,v));
    const k=Math.pow(r,2.6)+.12*r,o=(j*n+i)*4;d.data[o]=Math.max(0,Math.min(255,128-u*k*127));d.data[o+1]=Math.max(0,Math.min(255,128-v*k*127));d.data[o+2]=128;d.data[o+3]=255}
  x.putImageData(d,0,0);const url=cv.toDataURL(),fe=$('#lensImg');fe.setAttribute('href',url);fe.setAttributeNS('http://www.w3.org/1999/xlink','xlink:href',url)})();

/* ════════════════════ Live layer ════════════════════ */
const live=document.createElement('canvas');live.className='live';const L=live.getContext('2d');
let liveIdx=-1,LM={k:1,x:0,y:0},liveDirty=true,animErr=false;
function sizeLive(){const el=bgs[liveIdx];if(!el)return;const w=el.clientWidth,h=el.clientHeight,d=Math.min(devicePixelRatio||1,1.25);
  live.width=Math.max(1,Math.round(w*d));live.height=Math.max(1,Math.round(h*d));const s=Math.max(w/WW,h/HH);LM={k:d*s,x:d*(w-WW*s)*.5,y:d*(h-HH*s)*.5};liveDirty=true}
function drawLive(t){const i=liveIdx;if(i<0||!built[i])return;if(reduce&&!liveDirty)return;
  L.setTransform(1,0,0,1,0,0);L.globalAlpha=1;L.globalCompositeOperation='source-over';L.clearRect(0,0,live.width,live.height);
  L.save();L.setTransform(LM.k,0,0,LM.k,LM.x,LM.y);
  try{WORLDS[i].anim(L,reduce?8:t/1000,WORLDS[i].D,pmx,pmy)}catch(e){if(!animErr){animErr=true;console.error(e)}}
  L.restore();liveDirty=false}

/* ════════════════════ Layout ════════════════════ */
let W,H,S,R,cx,cy,topY,mob;
function layout(){
  W=innerWidth;H=innerHeight;mob=W<760;
  S=Math.round(Math.max(88,Math.min(168,Math.min(W,H)*(mob?.26:.17))));
  R=mob?Math.max(W*1.05,420):Math.min(Math.max(W*.5,580),1000);
  topY=H*(mob?.68:.71);cx=W/2;cy=topY+R;
  root.style.setProperty('--s',S+'px');root.style.setProperty('--cy',topY+'px');
  for(const el of [track,arcring]){el.style.left=(cx-R)+'px';el.style.top=(cy-R)+'px';el.style.width=el.style.height=(R*2)+'px'}
  titleEl.style.bottom=(H-(topY-S*.72-(mob?34:46)))+'px';
  const f=$('#vis-glass');f.setAttribute('width',S);f.setAttribute('height',S);
  const fe=$('#lensImg');fe.setAttribute('width',S);fe.setAttribute('height',S);
  f.querySelectorAll('feDisplacementMap').forEach((el,i)=>el.setAttribute('scale',(S*[.15,.17,.19][i]).toFixed(1)));
  glowEl.style.transform=`translate(${cx}px,${topY}px)`;
  sizeLive();
}

/* ════════════════════ Motion ════════════════════ */
let rot=-3.2,vel=0,target=0,active=-1,dragging=false,intro=0,introStart=0,started=false;
let mx=0,my=0,pmx=0,pmy=0,lastTouch=-1e9,autoT=0;
const AUTO=8000,mod=i=>((i%N)+N)%N;

function setActive(i){
  if(i===active)return;const first=active<0;active=i;const w=WORLDS[i];
  root.style.setProperty('--accent',w.accent);
  bgs.forEach((b,k)=>b.classList.toggle('on',k===i));
  meds.forEach((m,k)=>m.classList.toggle('on',k===i));
  segs.forEach((s,k)=>{s.classList.toggle('on',k===i);s.classList.toggle('past',k<i);s.setAttribute('aria-selected',k===i)});
  curEl.textContent=String(i+1).padStart(2,'0');
  titleEl.classList.toggle('light',!!w.light);autoT=0;bgs[i].appendChild(live);liveIdx=i;sizeLive();
  const render=()=>{const words=w.name.split(' ');let html='',n=0;
    words.forEach((wd,wi)=>{const cls=wi===0?'ch it':'ch';for(const ch of wd)html+=`<span class="${cls}" style="animation-delay:${(n++)*.035}s">${ch}</span>`;
      if(wi<words.length-1)html+=`<span class="ch" style="animation-delay:${(n++)*.035}s">&nbsp;</span>`});
    nameEl.className='name';nameEl.innerHTML=html;subEl.textContent=w.sub;tagEl.textContent=w.tag;subEl.classList.remove('out');tagEl.classList.remove('out')};
  clearTimeout(setActive.t);
  if(first){render();return}
  nameEl.classList.add('out');subEl.classList.add('out');tagEl.classList.add('out');setActive.t=setTimeout(render,320);
}
function go(d){target=Math.round(target)+d;setActive(mod(Math.round(target)))}
function goTo(i){let d=i-mod(Math.round(target));if(d>N/2)d-=N;if(d<-N/2)d+=N;go(d)}
function userTouched(){lastTouch=performance.now();autoT=0}

$('#prev').addEventListener('click',e=>{e.stopPropagation();go(-1);userTouched()});
$('#next').addEventListener('click',e=>{e.stopPropagation();go(1);userTouched()});
addEventListener('keydown',e=>{if(sheetOpen)return;if(e.key==='ArrowLeft'){go(-1);userTouched()}else if(e.key==='ArrowRight'){go(1);userTouched()}
  else if((e.key==='Enter'||e.key===' ')&&document.activeElement?.classList.contains('med')){e.preventDefault();goTo(+document.activeElement.dataset.index);userTouched()}});
let wheelLock=0;
stage.addEventListener('wheel',e=>{e.preventDefault();if(sheetOpen)return;const now=performance.now();if(now<wheelLock)return;
  const d=Math.abs(e.deltaX)>Math.abs(e.deltaY)?e.deltaX:e.deltaY;if(Math.abs(d)<6)return;go(d>0?1:-1);wheelLock=now+620;userTouched()},{passive:false});
let px0=0,t0=0,moved=false,downMed=null,samples=[];
stage.addEventListener('pointerdown',e=>{if(e.button!==0||e.target.closest('button,a'))return;
  px0=e.clientX;t0=target;moved=false;downMed=e.target.closest('.med');samples=[[e.clientX,performance.now()]];
  stage.setPointerCapture(e.pointerId);dragging=true;stage.classList.add('dragging');userTouched()});
stage.addEventListener('pointermove',e=>{mx=e.clientX/W*2-1;my=e.clientY/H*2-1;
  if(!dragging)return;const dx=e.clientX-px0;if(Math.abs(dx)>5)moved=true;
  target=t0-dx/(R*STEP)*1.15;samples.push([e.clientX,performance.now()]);if(samples.length>6)samples.shift();setActive(mod(Math.round(target)))});
const end=()=>{if(!dragging)return;dragging=false;stage.classList.remove('dragging');
  if(moved){const a=samples[0],b=samples[samples.length-1],vx=(b[0]-a[0])/Math.max(16,b[1]-a[1]);
    target=Math.round(target+Math.max(-2,Math.min(2,-vx*220/(R*STEP))));setActive(mod(Math.round(target)))}
  else if(downMed)goTo(+downMed.dataset.index);else target=Math.round(target);
  userTouched()};
stage.addEventListener('pointerup',end);stage.addEventListener('pointercancel',end);

const ease=t=>1-Math.pow(1-t,4),cosA=Math.cos(STEP),cosB=Math.cos(STEP*2.4);
let last=performance.now();
function frame(t){
  const dt=Math.min(50,t-last);last=t;const k=dt/16.67;
  if(started)intro=Math.min(1,(t-introStart)/1800);
  if(dragging){rot+=(target-rot)*Math.min(1,.38*k);vel=0}else{vel=vel*Math.pow(.74,k)+(target-rot)*.075*k;rot+=vel*k}
  pmx+=(mx-pmx)*.05*k;pmy+=(my-pmy)*.05*k;
  bgwrap.style.transform=`translate3d(${-pmx*16}px,${-pmy*11}px,0)`;
  track.style.transform=`rotate(${-rot*40}deg)`;
  const ie=ease(intro);
  for(let i=0;i<N;i++){let d=i-rot;d=((d%N)+N+N/2)%N-N/2;const a=d*STEP,c=Math.cos(a),x=cx+R*Math.sin(a),y=cy-R*c,near=Math.max(0,1-Math.abs(d));
    let o=Math.max(0,Math.min(1,(c-cosB)/(cosA-cosB)));o=o*o*(3-2*o);
    const s=(.68+.32*Math.max(0,(c-cosB)/(1-cosB)))+near*near*.36,m=meds[i];
    m.style.transform=`translate3d(${x-S/2}px,${y-S/2+(1-ie)*120}px,0) scale(${s*(.8+.2*ie)})`;
    m.style.opacity=(o*ie).toFixed(3);m.style.zIndex=Math.round(c*100)+100;m.style.pointerEvents=o>.05?'auto':'none';
    m.style.setProperty('--rr',(-28+d*22)+'deg');
    if(near>.5){m.style.setProperty('--lx',(34+pmx*22)+'%');m.style.setProperty('--ly',(10+pmy*14)+'%')}}
  const idle=t-lastTouch>9000;
  if(started&&!reduce&&!sheetOpen&&!dragging&&idle&&!document.hidden){autoT+=dt;if(autoT>=AUTO)go(1)}
  const p=idle&&!sheetOpen&&!reduce?Math.min(1,autoT/AUTO):0;
  segs.forEach((s,i)=>s.style.setProperty('--p',i===active?p:0));
  drawLive(t);
  requestAnimationFrame(frame);
}

/* ════════════════════ Sheets & nav ════════════════════ */
let sheetOpen=null;
const takeover=$('#takeover'),toggle=$('#toggle');
function route(where){
  takeover.classList.remove('open');takeover.setAttribute('aria-hidden','true');toggle.setAttribute('aria-expanded','false');toggle.textContent='Menu';
  document.querySelectorAll('.sheet').forEach(s=>{const on=s.id===where;s.classList.toggle('open',on);s.setAttribute('aria-hidden',!on)});
  sheetOpen=where==='about'||where==='contact'?where:null;
  if(where==='contact'&&active>=0)$('#fs').selectedIndex=active;
  document.querySelectorAll('.link').forEach(l=>{const on=l.dataset.go===(where||'home');l.classList.toggle('active',on);if(on)l.setAttribute('aria-current','page');else l.removeAttribute('aria-current')});
  userTouched();
}
document.querySelectorAll('[data-go]').forEach(a=>a.addEventListener('click',e=>{e.preventDefault();route(a.dataset.go)}));
document.querySelectorAll('.sheet').forEach(s=>s.addEventListener('click',e=>{if(e.target===s)route('home')}));
addEventListener('keydown',e=>{if(e.key==='Escape')route('home')});
toggle.addEventListener('click',()=>{const open=!takeover.classList.contains('open');
  takeover.classList.toggle('open',open);takeover.setAttribute('aria-hidden',!open);toggle.setAttribute('aria-expanded',open);toggle.textContent=open?'Close':'Menu';
  if(open)takeover.querySelectorAll('a').forEach(a=>{a.style.animation='none';a.offsetWidth;a.style.animation=''})});
$('#fs').innerHTML=WORLDS.map(w=>`<option>${w.name}</option>`).join('')+'<option>Not sure yet</option>';
$('#form').addEventListener('submit',e=>{e.preventDefault();e.target.style.display='none';$('#sent').style.display='block'});

/* ════════════════════ Build ════════════════════ */
const raf=()=>new Promise(r=>requestAnimationFrame(r));
async function encode(cv,q){try{const blob=await new Promise(r=>cv.toBlob(r,'image/jpeg',q));if(blob)return URL.createObjectURL(blob)}catch(_){}return cv.toDataURL('image/jpeg',q)}
async function build(){
  layout();addEventListener('resize',layout);
  setActive(0);requestAnimationFrame(frame);
  const cv=document.createElement('canvas');cv.width=WW;cv.height=HH;const c=cv.getContext('2d');
  const tc=document.createElement('canvas');tc.width=800;tc.height=500;const tx=tc.getContext('2d');
  const b1=document.createElement('canvas');b1.width=20;b1.height=12;const bx1=b1.getContext('2d');const b2=document.createElement('canvas');b2.width=120;b2.height=72;const bx2=b2.getContext('2d');bx2.imageSmoothingQuality='high';
  const reset=()=>{c.setTransform(1,0,0,1,0,0);c.globalAlpha=1;c.globalCompositeOperation='source-over';if('filter' in c)c.filter='none';c.lineCap='butt';c.setLineDash([])};
  for(let i=0;i<N;i++){
    const w=WORLDS[i];$('#ldTxt').textContent=`Calibrating ${w.name} · ${String(i+1).padStart(2,'0')}/09`;
    await raf();
    reset();c.clearRect(0,0,WW,HH);
    try{w.paint(c,WW,HH,w.D)}catch(err){console.error(w.name,err)}
    reset();try{post(c,WW,HH,w.bloom)}catch(err){console.error(err)}
    bgs[i].style.backgroundImage=`url(${await encode(cv,.92)})`;
    reset();c.save();try{w.anim(c,12.5,w.D,0,0)}catch(err){console.error(w.name,err)}c.restore();
    tx.drawImage(cv,0,0,800,500);
    const tu=await encode(tc,.9);meds[i].querySelector('.med-img').style.backgroundImage=meds[i].querySelector('.med-base').style.backgroundImage=`url(${tu})`;
    bx1.drawImage(tc,0,0,20,12);bx2.clearRect(0,0,120,72);bx2.drawImage(b1,0,0,120,72);meds[i].style.setProperty('--blur',`url(${await encode(b2,.85)})`);
    built[i]=true;if(i===liveIdx)liveDirty=true;
    $('#ldBar').style.width=((i+1)/N*100)+'%';
  }
  await new Promise(r=>setTimeout(r,300));
  $('#loader').classList.add('done');document.body.classList.add('ready');
  started=true;introStart=performance.now();lastTouch=performance.now()-4000;target=0;
}
build();
})();
</script>
</body>
</html>
```

