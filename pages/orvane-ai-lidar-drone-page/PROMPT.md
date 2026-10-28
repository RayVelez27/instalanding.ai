INSTALANDING.AI · Orvane AI LiDAR Drone Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Orvane AI LiDAR Drone Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/orvane-ai-lidar-drone-page

orvane-lidar-drone.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Orvane AI LiDAR Drone Page
  slug     orvane-ai-lidar-drone-page
  prompt   https://instalanding.ai/p/orvane-ai-lidar-drone-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/orvane-ai-lidar-drone-page
  license  Fictional brand ("Orvane Cortex"); every spec, site, coordinate and figure is invented.
           Replace names, numbers and copy before shipping. Every picture is drawn on canvas or in SVG; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --ink, --haze, --pale, --line, --glacier (cyan accent), --bg, --mist;
            Inter Tight (--sans, light display) and JetBrains Mono (--mono, bracketed labels)
  sections  nav, hero, promise, gear, numbers, solutions, capabilities, controller, software, terrain, footer
            (each region carries data-section); most are tall sections with a sticky full-screen .frame
  scripts   one IIFE, no libraries: a tiny 3D projector (camera, rotations) and a canvas render registry that only draws
            what is on screen; a point-cloud preloader; a shaded-mesh hero drone over a scanned terrain; a bridge sag
            and crack flag; a multi-echo radar; morphing point-cloud scenes per industry tab; a flyable drone with
            draggable sticks, triggers and WASD; a touchdown-to-delivery pipeline; a terrain drawn line by line with
            hotspot cards; a drag-to-turn drone viewer; a local-only request dialog
  assets    no image files

  ADAPTING
  - Scroll scenes read prog(section) (0-1 across the section's height); change --h / --hm to lengthen a scene.
  - Industry scenes are built in buildScene(k); terrain hotspots are the HS array.
  - prefers-reduced-motion: animations and transitions are cut to near zero and the preloader is short.
-->
<html lang="en" class="loading">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Orvane Cortex — AI LiDAR Drone Scanning</title>
<meta name="description" content="Orvane Cortex: an AI-powered LiDAR drone system that flies itself, measures bridges, power lines, turbines and terrain to the centimetre, and flags structural risks automatically.">
<meta name="theme-color" content="#f6f8f8">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'%3E%3Ccircle cx='12' cy='12' r='7.25' fill='none' stroke='%231d2a31' stroke-width='1.6'/%3E%3Cpath d='M1.5 12h3.2M19.3 12h3.2' stroke='%231d2a31' stroke-width='1.6' stroke-linecap='round'/%3E%3Ccircle cx='12' cy='12' r='2.6' fill='%238fe3f0'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@300;400;500&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
  --ink:#1d2a31;--ink2:#2b3b44;--haze:#7d8a91;--pale:#b9c3c8;--line:#dde3e5;--line2:#d3dadd;
  --glacier:#8fe3f0;--glacier2:#5fbfd0;--bg:#f6f8f8;--mist:#e8f1f4;
  --sans:'Inter Tight',system-ui,-apple-system,Segoe UI,sans-serif;--mono:'JetBrains Mono',ui-monospace,SFMono-Regular,Menlo,monospace;
  --ease:cubic-bezier(.22,1,.36,1);--ease2:cubic-bezier(.76,0,.24,1);
}
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%;scroll-behavior:auto}
html.loading{overflow:hidden}
body{background:var(--bg);color:var(--ink);font-family:var(--sans);-webkit-font-smoothing:antialiased;min-height:100vh}
main{overflow-x:clip;display:block}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:0;cursor:pointer}
canvas{display:block}
::selection{background:var(--glacier);color:var(--ink)}
.mono{font-family:var(--mono);font-size:11px;line-height:1.35;letter-spacing:.08em;text-transform:uppercase;font-weight:400}
.br::before{content:"[";margin-right:.6em}.br::after{content:"]";margin-left:.6em}
.cb::before{content:"{";margin-right:.6em}.cb::after{content:"}";margin-left:.6em}
.haze{color:var(--haze)}
.dash{display:inline-block;height:1px;width:48px;background:var(--pale);vertical-align:middle}
.lbl{display:flex;align-items:center;gap:16px;color:var(--haze)}
.display{font-weight:300;letter-spacing:-.075em;line-height:.8}
.mask{display:block;overflow:hidden;padding-bottom:.06em}
.mask>span{display:block;transform:translateY(105%);transition:transform 1.3s var(--ease)}
.in .mask>span{transform:none}
.rw{opacity:.13;transition:opacity .35s ease}
.rw.on{opacity:1}
@media(max-width:767px){.md{display:none!important}}
@media(min-width:768px){.sm{display:none!important}}


/* ---------- preloader ---------- */
#pre{position:fixed;inset:0;z-index:150;overflow:hidden}
#pre .pan{position:absolute;left:0;right:0;height:50%;background:#fbfcfc;transition:transform 1.25s var(--ease2) .55s}
#pre .pan.t{top:0}#pre .pan.b{bottom:0}
#pre .pan i{position:absolute;left:0;right:0;height:1px;background:var(--glacier2);transform:scaleX(0);transition:transform .62s cubic-bezier(.65,0,.35,1)}
#pre .pan.t i{bottom:0}#pre .pan.b i{top:0}
#pre .pc{position:absolute;inset:0;display:flex;flex-direction:column;justify-content:space-between;padding:20px 20px 24px;transition:opacity .5s ease}
#preCv{position:absolute;left:50%;top:50%;width:min(76vw,44svh);height:min(76vw,44svh);transform:translate(-50%,-50%)}
#pre .row{position:relative;display:flex;justify-content:space-between;align-items:flex-start;gap:24px}
#prePctWrap{display:flex;align-items:flex-start;font-size:clamp(64px,10vw,152px);font-weight:300;line-height:.8;letter-spacing:-.065em;font-variant-numeric:tabular-nums}
#prePctWrap .mono{margin:4px 0 0 8px;color:var(--haze)}
.pre-r{display:flex;flex-direction:column;align-items:flex-end;gap:6px;padding-bottom:4px;text-align:right}
#preStage.fx{animation:rise .5s var(--ease)}
@keyframes rise{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:none}}
.pre-bar{position:relative;height:1px;background:var(--line);overflow:hidden;margin-top:16px}
#preBar{position:absolute;inset:0;background:var(--ink);transform-origin:left;transform:scaleX(0)}
#pre.done .pan i{transform:scaleX(1)}
#pre.done .pan.t{transform:translateY(-100%)}#pre.done .pan.b{transform:translateY(100%)}
#pre.done .pc{opacity:0}
@media(min-width:768px){#pre .pc{padding:28px 40px 36px}#preCv{width:min(56vmin,460px);height:min(56vmin,460px)}}

/* ---------- chrome ---------- */
.rails{position:fixed;inset:0;pointer-events:none;z-index:-1}
.rails i{position:absolute;top:0;bottom:0;width:1px;background:var(--line)}
.rails .ruler{position:absolute;top:0;bottom:0;display:none}
@media(min-width:768px){.rails .ruler{display:block}}
.hdr{position:fixed;inset:0 0 auto;z-index:50}
.hdr-in{position:relative;height:56px;display:flex;align-items:center;justify-content:space-between;padding:0 16px;border-bottom:1px solid rgba(221,227,229,.7);background:rgba(255,255,255,.6);backdrop-filter:blur(12px) saturate(1.5);-webkit-backdrop-filter:blur(12px) saturate(1.5)}
.brand{display:flex;align-items:center;gap:10px}
.brand b{font-size:15px;font-weight:500;letter-spacing:-.03em}
.brand i{width:4px;height:4px;border-radius:50%;background:rgba(29,42,49,.35)}
.brand em{font-style:normal;font-size:13px;letter-spacing:-.01em;color:var(--haze)}
@media(max-width:639px){.brand em,.brand i{display:none}}
.hdr-mid{position:absolute;left:50%;transform:translateX(-50%);font-size:13px;letter-spacing:-.01em}
.hdr-r{display:flex;align-items:center;gap:20px}
.clock{min-width:110px;text-align:right}
.clock time{text-transform:none;font-variant-numeric:tabular-nums}
@media(max-width:639px){.clock{display:none}}
#menuBtn{height:28px;min-width:62px;border-radius:99px;background:#e4e9eb;padding:0 14px;font-size:13px;letter-spacing:-.01em;transition:background .3s}
#menuBtn:hover{background:#d7dee1}
@media(min-width:768px){.hdr-in{padding:0 24px}}

#menu{position:fixed;inset:0;z-index:40;background:rgba(246,248,248,.95);backdrop-filter:blur(24px);-webkit-backdrop-filter:blur(24px);clip-path:inset(0 0 100% 0);transition:clip-path .7s var(--ease2);visibility:hidden}
#menu.open{clip-path:inset(0 0 0 0);visibility:visible}
#menu .wrap{max-width:1600px;margin:0 auto;height:100%;display:flex;flex-direction:column;justify-content:space-between;gap:40px;overflow-y:auto;padding:96px 16px 32px}
#menu ul{list-style:none;border-top:1px solid var(--line)}
#menu li{border-bottom:1px solid var(--line)}
#menu li a{display:flex;align-items:baseline;gap:20px;padding:10px 0}
#menu li .mono{width:32px;flex-shrink:0;color:var(--haze)}
#menu li .t{display:block;font-size:clamp(34px,6.2vw,92px);font-weight:300;line-height:.95;letter-spacing:-.055em;transform:translateY(24px);opacity:0;transition:transform .7s var(--ease),opacity .7s var(--ease)}
#menu.open li .t{transform:none;opacity:1}
#menu li a:hover .t{transform:translateX(12px)}
#menu li svg{margin-left:auto;width:20px;height:20px;opacity:0;transform:translateX(-8px);transition:.5s}
#menu li a:hover svg{opacity:1;transform:none}
.menu-foot{display:flex;flex-direction:column;gap:24px}
.menu-foot p{max-width:24rem;font-size:15px;line-height:1.6;color:var(--haze)}
@media(min-width:768px){#menu .wrap{padding:96px 40px 40px}#menu li a{gap:32px;padding:14px 0}.menu-foot{flex-direction:row;align-items:flex-end;justify-content:space-between}}

.btn{display:inline-flex;align-items:center;gap:12px;height:48px;padding:0 24px;background:var(--ink);color:#fff;font-size:14px;letter-spacing:-.01em;transition:background .3s;align-self:flex-start}
.btn:hover{background:var(--ink2)}
.btn svg{width:16px;height:16px;transition:transform .3s}
.btn:hover svg{transform:translate(2px,-2px)}
.btn.lg{height:56px;padding:0 28px;font-size:15px}

#ring{position:fixed;right:16px;top:74px;z-index:30;width:44px;height:44px;pointer-events:none}
#ring svg{position:absolute;inset:0;transform:rotate(-90deg)}
#ring .win{position:absolute;inset:5px;overflow:hidden;border-radius:50%}
#ring .reel{transition:transform .7s cubic-bezier(.65,0,.35,1)}
#ring .reel div{height:34px;display:flex;align-items:center;justify-content:center;font-family:var(--mono);font-size:11px}
@media(min-width:768px){#ring{right:24px}}
#cursor{position:fixed;left:0;top:0;z-index:200;width:8px;height:8px;margin:-4px 0 0 -4px;border-radius:50%;background:#fff;mix-blend-mode:difference;pointer-events:none;opacity:0;transition:width .3s,height .3s,margin .3s,opacity .3s}
#cursor.big{width:36px;height:36px;margin:-18px 0 0 -18px}

/* ---------- generic sections ---------- */
.sec{position:relative;height:var(--h)}
@media(min-width:768px){.sec{height:var(--hm,var(--h))}}
.frame{position:sticky;top:0;height:100vh;height:100svh;overflow:hidden}
.hl{position:absolute;left:12px;right:12px;height:1px;background:var(--line);transform-origin:left;transform:scaleX(0);transition:transform 1.4s var(--ease)}
.vl{position:absolute;width:1px;background:var(--line);transform-origin:top;transform:scaleY(0);transition:transform 1.4s var(--ease) .2s}
.in .hl,.in .vl,.in.hl{transform:none}
@media(min-width:768px){.hl{left:20px;right:20px}}

/* ---------- hero ---------- */
#hero{position:relative;height:100vh;height:100svh;min-height:540px}
.hero-card{position:absolute;left:8px;right:8px;bottom:8px;top:64px;overflow:hidden;border-radius:28px;border:1px solid rgba(255,255,255,.7);box-shadow:inset 0 1px 0 rgba(255,255,255,.9),0 1px 0 rgba(29,42,49,.04);
background:radial-gradient(120% 85% at 50% -5%,rgba(255,255,255,.95) 0%,rgba(255,255,255,0) 58%),radial-gradient(70% 60% at 88% 105%,rgba(190,212,222,.6) 0%,rgba(190,212,222,0) 70%),radial-gradient(60% 55% at 6% 96%,rgba(205,222,229,.55) 0%,rgba(205,222,229,0) 70%),linear-gradient(180deg,#eef3f5 0%,#e4ebee 100%)}
@media(min-width:768px){.hero-card{left:12px;right:12px;bottom:12px}}
.ghost{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;pointer-events:none}
.ghost span{font-size:clamp(190px,40vw,780px);font-weight:300;line-height:1;letter-spacing:-.075em;white-space:nowrap;color:transparent;background:linear-gradient(180deg,rgba(255,255,255,.85),rgba(255,255,255,.15));-webkit-background-clip:text;background-clip:text;user-select:none;transform:translateY(-4%)}
#heroCv{position:absolute;inset:0;width:100%;height:100%}
.cross{position:absolute;width:16px;height:16px}
.hero-top{position:absolute;left:48px;top:22px;display:flex;align-items:center;gap:16px;color:var(--haze)}
.hero-h{position:absolute;left:20px;bottom:24px;max-width:680px;padding-right:48px;font-size:clamp(22px,2.7vw,42px);font-weight:300;line-height:1.08;letter-spacing:-.04em}
.hero-h .l{display:block;overflow:hidden}
.hero-h .l span{display:block;transform:translateY(110%);transition:transform 1.2s var(--ease)}
.ready .hero-h .l span{transform:none}
.ready .hero-h .l:nth-child(2) span{transition-delay:.12s;color:var(--haze)}
.hero-scroll{position:absolute;right:20px;bottom:24px;display:flex;align-items:center;gap:12px;font-size:13px}
.dots9{display:grid;grid-template-columns:repeat(3,3px);gap:3px}
.dots9 i{width:3px;height:3px;border-radius:50%;background:var(--ink);animation:dp 1.6s ease-in-out infinite}
@keyframes dp{0%,100%{opacity:.2}50%{opacity:1}}
.hud{position:absolute;right:20px;top:20px;display:flex;flex-direction:column;align-items:flex-end;gap:6px;color:var(--ink);opacity:0;transition:opacity 1s ease .6s}
.ready .hud{opacity:1}
.hud span{font-variant-numeric:tabular-nums}
.hud span b{font-weight:400;color:var(--haze);margin-right:.8em}
@media(min-width:768px){.hero-h{left:40px;bottom:40px;padding-right:0}.hero-scroll{right:40px;bottom:40px}.hud{right:72px;top:24px}}

/* ---------- promise ---------- */
#sagCv{position:absolute;right:0;top:84px;width:100%;height:42%}
@media(min-width:768px){#sagCv{width:42%;height:calc(100% - 84px)}}
.promise-copy{position:relative;height:100%;display:flex;flex-direction:column;justify-content:flex-end;padding:0 20px 96px}
.promise-copy>div{max-width:100%}
.promise-h{margin-top:24px;font-size:clamp(34px,5.1vw,92px);font-weight:300;line-height:1.02;letter-spacing:-.048em}
@media(min-width:768px){.promise-copy{justify-content:center;padding:0 40px}.promise-copy>div{width:54%}.promise-h{margin-top:32px}}
.corner-bl{position:absolute;left:20px;bottom:24px}
.ring-sm{position:absolute;right:20px;bottom:20px;width:48px;height:48px}
.ring-sm svg{position:absolute;inset:0;transform:rotate(-90deg)}
.ring-sm span{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-family:var(--mono);font-size:11px}
@media(min-width:768px){.corner-bl{left:40px;bottom:40px}.ring-sm{right:40px;bottom:36px}}

/* ---------- gear ---------- */
.gear-title{position:absolute;left:0;right:0;top:76px;padding:0 16px}
.giant{font-size:clamp(128px,25vw,440px)}
#gearCv{position:absolute;right:2%;top:72px;width:min(52vw,44svh);height:min(52vw,44svh)}
@media(min-width:768px){.gear-title{top:70px;padding:0 36px}#gearCv{right:5%;top:64px;width:min(46vw,52svh);height:min(46vw,52svh)}}
.gear-legend{position:absolute;right:20px;top:calc(72px + min(52vw,44svh));display:flex;gap:14px;color:var(--haze)}
.gear-legend i{display:inline-block;width:6px;height:6px;border-radius:50%;margin-right:6px;vertical-align:1px}
@media(min-width:768px){.gear-legend{right:calc(5% + 8px);top:calc(64px + min(46vw,52svh) - 6px)}}
.gear-grid{position:absolute;left:0;right:0;bottom:0;top:52%;display:grid;grid-template-rows:auto 1fr;gap:24px;padding:24px 20px 40px}
.gear-grid ul{list-style:none;display:flex;flex-direction:column;gap:8px}
.gear-grid li{display:flex;align-items:center;gap:12px;color:var(--haze)}
.gear-grid li i{width:6px;height:6px;border-radius:50%;border:1px solid var(--haze)}
.gear-big{font-size:clamp(24px,2.5vw,40px);font-weight:300;line-height:1.1;letter-spacing:-.035em;max-width:640px}
.gear-small{margin-top:20px;font-size:clamp(17px,1.45vw,23px);font-weight:300;line-height:1.4;letter-spacing:-.015em;max-width:640px}
@media(min-width:768px){.gear-grid{top:57%;grid-template-columns:1fr 1fr;grid-template-rows:1fr;gap:0;padding:32px 40px 40px}.gear-grid>div:first-child{display:flex;flex-direction:column;justify-content:space-between;padding-right:40px}.gear-grid>div:last-child{padding-left:40px}.gear-small{margin-top:24px}}

/* ---------- numbers ---------- */
.num-head{position:absolute;left:20px;top:84px;display:flex;align-items:center;gap:16px}
.num-head h2{font-weight:400;color:var(--haze)}
@media(min-width:768px){.num-head{left:40px}}
.arc-wrap{position:absolute;left:50%;top:22%;width:min(80vw,56vh);aspect-ratio:1;transform:translate(-50%,-50%)}
.arc-wrap svg,.arc-wrap canvas{position:absolute;inset:0;width:100%;height:100%;overflow:visible}
@media(min-width:768px){.arc-wrap{top:30%;width:min(36vw,56vh)}}
.num-bottom{position:absolute;left:0;right:0;bottom:0;top:50%}
@media(min-width:768px){.num-bottom{top:66%}}
.num-label{position:absolute;left:50%;top:0;transform:translate(-50%,calc(-100% - 42px));white-space:nowrap}
.num-badge{position:absolute;left:50%;top:0;z-index:2;width:56px;height:56px;border-radius:50%;border:1px solid var(--line);background:var(--bg);box-shadow:0 8px 24px -12px rgba(29,42,49,.25);display:flex;align-items:center;justify-content:center;transform:translate(-50%,-50%)}
.num-badge svg{width:32px;height:32px;fill:var(--ink)}
.num-badge g{transform-origin:16px 16px;transition:opacity .45s ease,transform .6s var(--ease);opacity:0;transform:scale(.6)}
.num-badge g.on{opacity:1;transform:none}
@media(min-width:768px){.num-badge{width:64px;height:64px}}
.num-grid{display:grid;grid-template-rows:repeat(3,1fr);height:100%;padding-top:36px}
.stat{display:flex;flex-direction:column;justify-content:center;gap:8px;padding:0 20px;color:#c6cdd0;transition:color .6s ease}
.stat+.stat{border-top:1px solid var(--line)}
.stat.on{color:var(--ink)}
.stat p{display:flex;align-items:baseline;gap:12px}
.stat .v{font-size:clamp(48px,7vw,124px);font-weight:300;line-height:.9;letter-spacing:-.06em;font-variant-numeric:tabular-nums}
.stat .u{font-size:clamp(16px,1.5vw,24px);letter-spacing:-.02em}
@media(min-width:768px){.num-grid{grid-template-columns:repeat(3,1fr);grid-template-rows:1fr;padding-top:0}.stat{padding:0 40px;gap:16px}.stat+.stat{border-top:0;border-left:1px solid var(--line)}}

/* ---------- solutions ---------- */
.sol-frame{display:flex;flex-direction:column;padding:68px 16px 20px}
@media(min-width:768px){.sol-frame{padding:72px 40px 32px}}
.sol-title{flex-shrink:0;font-size:clamp(60px,min(14.5vw,22vh),250px)}
.tabs-row{position:relative;margin-top:12px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid var(--line)}
.tabs{position:relative;display:flex;gap:20px;overflow-x:auto;scrollbar-width:none}
.tabs::-webkit-scrollbar{display:none}
.tabs button{flex-shrink:0;padding:12px 0;font-size:14px;letter-spacing:-.01em;color:#9aa3a8;transition:color .4s}
.tabs button[aria-selected=true]{color:var(--ink)}
#tabLine{position:absolute;bottom:0;left:0;height:2px;width:1px;background:var(--ink);transform-origin:left;transition:transform .6s var(--ease)}
@media(min-width:768px){.tabs-row{margin-top:20px}.tabs{gap:40px}.tabs button{padding:16px 0;font-size:17px}}
.sol-grid{margin-top:16px;flex:1;min-height:0;display:grid;grid-template-rows:auto 1fr auto;gap:16px}
@media(min-width:768px){.sol-grid{margin-top:32px;grid-template-columns:minmax(0,.9fr) minmax(0,1.5fr) minmax(0,.9fr);grid-template-rows:1fr;gap:32px}}
@media(min-width:1280px){.sol-grid{gap:48px}}
.stack{display:grid;align-content:start}
.stack>*{grid-area:1/1;transition:opacity .6s ease}
.sol-copy{font-size:15px;line-height:1.45;letter-spacing:-.01em}
.sol-copy .w{color:var(--pale);transition:color .5s ease}
.sol-copy.on .w{color:var(--ink)}
@media(min-width:768px){.sol-copy{font-size:clamp(17px,1.35vw,21px)}}
.sol-mid{display:flex;flex-direction:column;min-height:0;gap:12px}
.panel{position:relative;flex:1;min-height:180px;overflow:hidden;border-radius:20px;border:1px solid var(--line);background:radial-gradient(90% 70% at 50% 20%,#f2f6f5,#e3eae6 70%)}
@media(min-width:768px){.panel{max-height:min(54vh,34vw)}.sol-mid{gap:16px}}
.panel canvas{position:absolute;inset:0;width:100%;height:100%}
.sweep{position:absolute;left:0;right:0;top:0;height:10%;background:linear-gradient(180deg,transparent,rgba(255,255,255,.35),transparent);animation:sweep 4.5s linear infinite;pointer-events:none}
@keyframes sweep{from{transform:translateY(-100%)}to{transform:translateY(1000%)}}
.flash{position:absolute;left:0;right:0;top:0;height:1px;background:var(--glacier);box-shadow:0 0 14px 3px rgba(143,227,240,.85);opacity:0;pointer-events:none}
.flash.go{animation:flash 1.1s var(--ease)}
@keyframes flash{0%{opacity:1;transform:translateY(0)}100%{opacity:0;transform:translateY(var(--ph,300px))}}
.corners span{position:absolute;width:12px;height:12px;border-color:rgba(29,42,49,.5);border-style:solid;border-width:0}
.corners .a{left:12px;top:12px;border-left-width:1px;border-top-width:1px}.corners .b{right:12px;top:12px;border-right-width:1px;border-top-width:1px}
.corners .c{left:12px;bottom:12px;border-left-width:1px;border-bottom-width:1px}.corners .d{right:12px;bottom:12px;border-right-width:1px;border-bottom-width:1px}
.panel .tl{position:absolute;left:32px;top:14px;color:rgba(29,42,49,.75)}
.panel .bl{position:absolute;left:32px;right:32px;bottom:14px;display:grid;color:rgba(29,42,49,.75)}
.panel .bl span{grid-area:1/1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;transition:opacity .5s}
.chips{display:grid}
.chips ul{grid-area:1/1;list-style:none;display:flex;gap:8px;overflow-x:auto;scrollbar-width:none;transition:opacity .5s}
.chips ul::-webkit-scrollbar{display:none}
.chips li{flex-shrink:0;border-radius:99px;border:1px solid var(--line);background:rgba(255,255,255,.6);color:var(--haze);padding:6px 14px;font-size:12px;letter-spacing:-.01em;transition:background .4s,color .4s,border-color .4s}
.chips li.on{background:var(--ink);border-color:var(--ink);color:#fff}
@media(min-width:768px){.chips li{font-size:13px}}
.specs{display:grid;grid-template-columns:repeat(3,1fr);align-self:start;border-left:1px solid var(--line);border-top:1px solid var(--line)}
.specs>div{display:flex;flex-direction:column;gap:6px;border-right:1px solid var(--line);border-bottom:1px solid var(--line);padding:12px}
.specs dt{font-family:var(--mono);font-size:9px;text-transform:uppercase;letter-spacing:.1em;color:var(--haze);line-height:1.35}
.specs dd{display:flex;align-items:baseline;gap:6px}
.specs dd b{font-size:20px;font-weight:300;line-height:1;letter-spacing:-.04em;font-variant-numeric:tabular-nums}
.specs dd small{font-size:11px;color:var(--haze)}
@media(min-width:768px){.specs{grid-template-columns:1fr 1fr}.specs>div{padding:16px;gap:12px}.specs dt{font-size:10.5px}.specs dd b{font-size:clamp(24px,2.2vw,36px)}.specs dd small{font-size:13px}}
@media(min-width:1280px){.specs>div{padding:20px}}
@media(max-width:767px) and (max-height:740px){.specs{display:none}}

/* ---------- capabilities ---------- */
.cap-frame{display:flex;flex-direction:column;padding:68px 16px 48px}
@media(min-width:768px){.cap-frame{padding:72px 40px 56px}}
.cap-title{flex-shrink:0;font-size:clamp(52px,min(13vw,20vh),232px)}
.letters span{transition:color .3s}
.cap-grid{flex:1;min-height:0;display:grid;grid-template-rows:auto minmax(0,1fr) auto;gap:16px;padding-top:16px}
@media(min-width:768px){.cap-grid{grid-template-columns:minmax(0,1fr) minmax(0,.85fr) minmax(0,1fr);grid-template-rows:1fr;gap:40px;padding-top:32px}}
.steps{list-style:none;display:flex;gap:20px;position:relative}
.steps li{display:flex;align-items:baseline;gap:8px;color:#b4bcc0;transition:color .5s}
.steps li.on{color:var(--ink)}
.steps li span:last-child{font-size:17px;letter-spacing:-.03em}
.steps-tick{position:absolute;left:0;top:0;width:24px;height:1px;background:var(--ink);transition:transform .6s var(--ease)}
@media(min-width:768px){.steps{flex-direction:column;padding-left:40px}.steps li{gap:16px}.steps li span:last-child{font-size:clamp(24px,2.4vw,40px);font-weight:300}}
.live{position:relative;min-height:240px;overflow:hidden;border-radius:22px;border:1px solid rgba(255,255,255,.7);box-shadow:inset 0 1px 0 rgba(255,255,255,.8);
background:linear-gradient(rgba(29,42,49,.045) 1px,transparent 1px),linear-gradient(90deg,rgba(29,42,49,.045) 1px,transparent 1px),radial-gradient(90% 60% at 50% 30%,rgba(255,255,255,.75) 0%,rgba(255,255,255,0) 70%),linear-gradient(180deg,#e7eef1 0%,#dbe5e9 100%);background-size:28px 28px,28px 28px,100% 100%,100% 100%}
.live canvas{position:absolute;inset:0;width:100%;height:100%}
.live .tl{position:absolute;left:16px;top:16px;color:rgba(29,42,49,.7)}
.live .tr{position:absolute;right:16px;top:16px;display:flex;align-items:center;gap:8px;color:rgba(29,42,49,.6)}
.live .tr i{width:6px;height:6px;border-radius:50%;background:var(--glacier2);animation:dp 1.4s infinite}
.live .bl{position:absolute;left:16px;right:16px;bottom:16px;display:grid;color:rgba(29,42,49,.7)}
.live .bl span{grid-area:1/1;transition:opacity .5s}
.cap-stat{display:grid;align-content:start}
@media(min-width:768px){.cap-stat{align-content:center}}
.cap-stat>div{grid-area:1/1;transition:opacity .6s ease,transform .6s var(--ease)}
.cap-stat .big{font-size:clamp(48px,7.5vw,136px);font-weight:300;line-height:.9;letter-spacing:-.06em}
.cap-stat .txt{margin-top:12px;max-width:380px;font-size:15px;line-height:1.5;letter-spacing:-.01em;color:var(--haze)}
@media(min-width:768px){.cap-stat .txt{margin-top:24px;font-size:clamp(15px,1.15vw,18px)}}
.cap-foot{position:absolute;bottom:16px;color:var(--haze)}
@media(min-width:768px){.cap-foot{bottom:24px}}

/* ---------- controller ---------- */
.ctl-frame{display:flex;flex-direction:column;padding:68px 16px 0}
@media(min-width:768px){.ctl-frame{padding:72px 40px 0}}
.ctl-title{flex-shrink:0;font-size:clamp(52px,min(13vw,17vh),220px)}
.tele-m{margin-top:4px;display:grid;grid-template-columns:repeat(4,1fr);gap:6px;flex-shrink:0}
.tele-m div{border:1px solid var(--line);background:rgba(255,255,255,.45);padding:6px;text-align:center;font-size:9.5px;white-space:pre}
.ctl-grid{position:relative;flex:1;min-height:0;display:grid;grid-template-rows:auto minmax(0,1fr)}
@media(min-width:768px){.ctl-grid{grid-template-columns:minmax(0,1fr) minmax(0,2.1fr) minmax(0,.8fr);grid-template-rows:1fr;gap:32px}}
.ctl-left{display:flex;flex-direction:column;gap:8px;padding-top:16px}
.ctl-left .h{max-width:360px;font-size:clamp(20px,2vw,34px);font-weight:300;line-height:1.08;letter-spacing:-.035em}
.ctl-left .s{max-width:300px;font-size:15px;line-height:1.5;color:var(--haze)}
.ctl-left ul{list-style:none;display:flex;flex-direction:column;gap:10px;color:rgba(29,42,49,.7)}
@media(min-width:768px){.ctl-left{justify-content:space-between;padding:28px 0 32px}.ctl-left>div{display:flex;flex-direction:column;gap:16px}}
.ctl-mid{position:relative;display:flex;flex-direction:column;min-height:0}
.stage{position:relative;flex:1;min-height:120px}
.stage canvas{position:absolute;inset:0;width:100%;height:100%}
#compass{position:absolute;bottom:2%;left:50%;width:min(88%,560px);transform:translateX(-50%);overflow:visible;pointer-events:none}
.pad-zone{position:relative;height:30svh;flex-shrink:0}
@media(min-width:768px){.pad-zone{height:34svh}}
.pad{position:absolute;left:50%;top:46%;transform:translate(-50%,-50%);width:min(580px,96%);aspect-ratio:3/1;border-radius:999px;background:linear-gradient(180deg,#fdfefe 0%,#eef2f4 45%,#dde4e7 100%);border:1px solid #fff;box-shadow:0 36px 60px -32px rgba(29,42,49,.55),0 10px 20px -14px rgba(29,42,49,.3),inset 0 2px 0 #fff,inset 0 -8px 18px rgba(29,42,49,.07);display:grid;grid-template-columns:1fr 1.05fr 1fr;align-items:center;padding:0 4%;user-select:none;-webkit-user-select:none}
.pad::before{content:"";position:absolute;inset:7px;border-radius:999px;border:1px solid rgba(29,42,49,.06);pointer-events:none}
.trig{position:absolute;top:-10px;width:22%;height:20px;border-radius:12px 12px 4px 4px;background:linear-gradient(180deg,#eef2f4,#cfd8dc);border:1px solid #fff;box-shadow:0 -2px 6px rgba(29,42,49,.12);font-family:var(--mono);font-size:9px;letter-spacing:.1em;display:flex;align-items:center;justify-content:center;color:var(--haze);transition:transform .15s,background .2s;touch-action:none}
.trig.l{left:12%}.trig.r{right:12%}
.trig.on{transform:translateY(3px);background:linear-gradient(180deg,#dff6fa,#bfe9f1);color:var(--ink)}
.well{position:relative;justify-self:center;width:74%;aspect-ratio:1;border-radius:50%;background:radial-gradient(circle at 50% 38%,#e4eaed,#c8d1d5 75%);box-shadow:inset 0 5px 12px rgba(29,42,49,.28),inset 0 -2px 4px rgba(255,255,255,.7),0 1px 0 #fff;touch-action:none;cursor:grab}
.well::after{content:"";position:absolute;inset:16%;border-radius:50%;border:1px dashed rgba(29,42,49,.15)}
.knob{position:absolute;left:27%;top:27%;width:46%;height:46%;border-radius:50%;background:radial-gradient(circle at 38% 28%,#4a5b64,#1d2a31 58%,#0d1519);box-shadow:0 8px 14px rgba(0,0,0,.32),inset 0 1px 0 rgba(255,255,255,.18);z-index:1}
.knob::after{content:"";position:absolute;inset:28%;border-radius:50%;background:radial-gradient(circle at 40% 35%,#2f3e46,#162127);box-shadow:inset 0 1px 2px rgba(0,0,0,.5)}
.well.drag{cursor:grabbing}
.pad-mid{display:flex;flex-direction:column;align-items:center;gap:10px}
.screen{width:100%;border-radius:10px;background:linear-gradient(180deg,#1d2a31,#121b20);padding:7px 9px;color:#bfeaf2;font-family:var(--mono);font-size:8.5px;letter-spacing:.06em;display:grid;grid-template-columns:1fr 1fr;gap:2px 8px;box-shadow:inset 0 2px 6px rgba(0,0,0,.5)}
.screen span{white-space:nowrap;font-variant-numeric:tabular-nums}
.screen b{font-weight:400;color:#6f8790;margin-right:4px}
.pbtns{display:flex;gap:10px}
.pbtns button{width:26px;height:26px;border-radius:50%;background:linear-gradient(180deg,#fff,#d9e0e3);box-shadow:0 3px 6px rgba(29,42,49,.2),inset 0 1px 0 #fff;display:flex;align-items:center;justify-content:center;transition:transform .15s}
.pbtns button:active{transform:scale(.92)}
.pbtns button i{width:7px;height:7px;border-radius:50%;background:#c3ccd0;transition:background .3s,box-shadow .3s}
.pbtns button[aria-pressed=true] i{background:var(--glacier2);box-shadow:0 0 8px var(--glacier)}
.pbl{display:flex;gap:10px;font-family:var(--mono);font-size:7.5px;letter-spacing:.1em;color:var(--haze);text-transform:uppercase}
.pbl span{width:26px;text-align:center}
@media(max-width:520px){.screen{display:none}.pbtns button{width:22px;height:22px}.pbl span{width:22px}}
.keys{position:absolute;left:0;right:0;bottom:4px;text-align:center;color:var(--haze)}
.tele{display:flex;flex-direction:column;gap:8px;padding-top:28px}
.tele div{position:relative;overflow:hidden;border:1px solid var(--line);background:rgba(255,255,255,.45);padding:10px 12px;white-space:pre;font-variant-numeric:tabular-nums;backdrop-filter:blur(2px)}
.tele div i{position:absolute;left:0;right:0;bottom:0;height:1px;background:var(--line)}
.tele div i b{position:absolute;inset:0;background:var(--glacier2);transform-origin:left;transform:scaleX(0)}

/* ---------- software ---------- */
#software{position:relative;min-height:150vh;padding:14vh 0 40vh}
.sw-title{position:relative;z-index:3;padding:0 16px;font-size:clamp(96px,22vw,400px)}
@media(min-width:768px){.sw-title{padding:0 36px}}
.sw-body{position:relative;margin-top:40px}
.sw-grid{display:grid;gap:40px;padding:32px 20px 0}
.sw-copy{max-width:620px;font-size:clamp(20px,2vw,32px);font-weight:300;line-height:1.25;letter-spacing:-.03em}
@media(min-width:768px){.sw-body{margin-top:56px}.sw-grid{grid-template-columns:1fr 1fr;gap:0;padding:48px 40px 0}.sw-grid>div:first-child{display:flex;align-items:flex-end;padding:0 40px 8px 0}.sw-copy{padding-left:40px}}
.pipe{margin:72px 20px 0;border:1px solid var(--line);border-radius:22px;background:linear-gradient(180deg,rgba(255,255,255,.7),rgba(255,255,255,.3));padding:24px;box-shadow:inset 0 1px 0 #fff}
@media(min-width:768px){.pipe{margin:96px 40px 0;padding:32px 36px}}
.pipe-head{display:flex;justify-content:space-between;align-items:flex-end;gap:16px;flex-wrap:wrap}
.pipe-time{font-size:clamp(40px,5vw,80px);font-weight:300;letter-spacing:-.06em;line-height:.9;font-variant-numeric:tabular-nums}
.pipe-time small{font-size:.32em;letter-spacing:-.01em;color:var(--haze);margin-left:.4em}
.track{position:relative;margin:36px 0 0;height:1px;background:var(--line)}
.track b{position:absolute;inset:0;background:var(--ink);transform-origin:left;transform:scaleX(0)}
.track i{position:absolute;top:0;width:9px;height:9px;margin:-4px 0 0 -4px;border-radius:50%;background:var(--glacier);box-shadow:0 0 0 4px rgba(143,227,240,.25),0 0 14px var(--glacier)}
.pstages{list-style:none;display:grid;grid-template-columns:repeat(5,1fr);margin-top:-5px}
.pstages li{position:relative;padding-top:24px;color:var(--pale);transition:color .4s}
.pstages li::before{content:"";position:absolute;left:0;top:0;width:9px;height:9px;border-radius:50%;border:1px solid var(--pale);background:var(--bg);transition:.4s}
.pstages li.on{color:var(--ink)}
.pstages li.on::before{background:var(--ink);border-color:var(--ink)}
.pstages b{display:block;font-weight:400;font-size:clamp(14px,1.3vw,20px);letter-spacing:-.02em;margin-top:6px}
.pstages li .mono{font-size:10px}
@media(max-width:600px){.pstages b{font-size:12px}.pstages li .mono{display:none}}
.files{display:flex;flex-wrap:wrap;gap:8px;margin-top:28px}
.files span{border:1px solid var(--line);border-radius:8px;padding:8px 12px;background:#fff;opacity:.35;transform:translateY(4px);transition:.5s var(--ease)}
.files span.on{opacity:1;transform:none;border-color:var(--ink)}
.files span::before{content:"";display:inline-block;width:6px;height:6px;border-radius:50%;background:var(--glacier2);margin-right:8px;vertical-align:1px}
.sw-fade{position:absolute;left:0;right:0;bottom:0;height:40vh;background:linear-gradient(180deg,transparent,var(--mist));pointer-events:none}

/* ---------- terrain ---------- */
#terrain{background:var(--mist)}
#terrain .frame{background:var(--mist)}
.ter-head{position:absolute;left:20px;right:20px;top:84px;display:flex;justify-content:space-between;align-items:flex-start;gap:24px;z-index:6}
.ter-head p{max-width:300px;margin-top:12px;font-size:15px;line-height:1.45;color:var(--haze)}
@media(min-width:768px){.ter-head{left:40px;right:96px}}
#terClip{position:absolute;inset:0;overflow:hidden;clip-path:inset(58% 6% 6% 6% round 24px);z-index:2}
#terClip canvas,#terOver{position:absolute;inset:0;width:100%;height:100%}
#terOver{z-index:3;pointer-events:none}
.hs{position:absolute;left:0;top:0;z-index:5;opacity:0;visibility:hidden;transition:opacity .6s}
.hs.show{opacity:1;visibility:visible}
.hs .stem{position:absolute;left:0;bottom:0;width:1px;height:46px;background:linear-gradient(0deg,rgba(29,42,49,.7),rgba(29,42,49,.05))}
.hs .halo{position:absolute;left:-24px;top:-70px;width:48px;height:48px;border-radius:50%;border:1px solid rgba(29,42,49,.15);animation:halo 2.4s ease-out infinite}
@keyframes halo{0%{transform:scale(.6);opacity:1}100%{transform:scale(1.4);opacity:0}}
.hs button{position:absolute;left:-16px;top:-62px;width:32px;height:32px;border-radius:50%;background:var(--ink);color:#fff;display:flex;align-items:center;justify-content:center;box-shadow:0 8px 24px -8px rgba(29,42,49,.6);transition:transform .3s ease-out}
.hs button svg{width:16px;height:16px;transition:transform .5s}
.hs:hover button,.hs:focus-within button{transform:scale(1.1)}
.hs:hover button svg,.hs:focus-within button svg{transform:rotate(90deg)}
.card{position:absolute;left:24px;top:-46px;width:224px;transform:translateY(-50%) scale(.9);transform-origin:left;opacity:0;pointer-events:none;border-radius:16px;border:1px solid rgba(255,255,255,.7);background:rgba(255,255,255,.88);padding:16px;box-shadow:0 18px 40px -18px rgba(29,42,49,.45);backdrop-filter:blur(12px);transition:.3s ease-out}
.hs[data-side=left] .card{left:auto;right:24px;transform-origin:right}
.hs:hover .card,.hs:focus-within .card{opacity:1;transform:translateY(-50%) scale(1)}
.card dl{margin-top:12px;display:flex;flex-direction:column;gap:6px}
.card dl div{display:flex;justify-content:space-between;align-items:baseline;gap:16px;border-top:1px solid var(--line);padding-top:6px}
.card dt{font-size:12px;color:var(--haze)}
.card dd{font-size:14px;letter-spacing:-.02em;font-variant-numeric:tabular-nums}
.card dd.warn{color:#0f7f92}
.ter-foot{position:absolute;left:16px;right:16px;bottom:16px;display:flex;justify-content:space-between;align-items:flex-end;gap:16px;z-index:6;pointer-events:none;opacity:0;transition:opacity .6s}
.ter-foot>div{display:flex;flex-direction:column;gap:6px;background:rgba(232,241,244,.82);padding:8px 12px;border-radius:10px;backdrop-filter:blur(6px);-webkit-backdrop-filter:blur(6px)}
#terClip:has(.hs:hover),#terClip:has(.hs:focus-within){z-index:4}
@media(min-width:768px){.ter-foot{left:calc(6% + 32px);right:calc(6% + 32px);bottom:calc(6% + 28px)}}

/* ---------- footer ---------- */
footer{position:relative;display:flex;flex-direction:column;min-height:100vh;min-height:100svh;background:var(--bg)}
.ft-stage{position:relative;flex:1;min-height:44svh}
.ft-glow{position:absolute;inset:0;background:radial-gradient(48% 60% at 50% 58%,rgba(255,255,255,.95),rgba(255,255,255,0) 70%)}
#viewer{position:absolute;left:6%;right:6%;top:56px;bottom:56px;touch-action:pan-y;user-select:none;outline:none;cursor:grab;border-radius:4px}
#viewer:focus-visible{box-shadow:0 0 0 1px rgba(29,42,49,.2)}
#viewer canvas{position:absolute;inset:0;width:100%;height:100%}
.drag-hint{position:absolute;left:50%;bottom:48px;transform:translateX(-50%);display:inline-flex;align-items:center;gap:8px;white-space:nowrap;color:var(--haze);pointer-events:none;transition:opacity .7s}
.drag-hint svg{width:16px;height:16px}
@media(min-width:768px){.drag-hint{bottom:20px}}
.ft-corner{position:absolute;left:20px;right:20px;bottom:20px;display:flex;justify-content:space-between;color:var(--haze);pointer-events:none}
@media(min-width:768px){.ft-corner{left:40px;right:40px}}
.ft-line{margin:0 12px;height:1px;background:var(--line)}
@media(min-width:768px){.ft-line{margin:0 20px}}
.ft-cta{display:grid;gap:32px;padding:36px 20px 0}
.ft-cta h2{max-width:620px;font-size:clamp(30px,3.9vw,64px);font-weight:300;line-height:1.02;letter-spacing:-.045em}
.ft-cta>div{display:flex;flex-direction:column;align-items:flex-start;gap:24px}
.ft-cta p{max-width:420px;font-size:clamp(16px,1.3vw,20px);line-height:1.45;letter-spacing:-.015em;color:var(--haze)}
@media(min-width:768px){.ft-cta{grid-template-columns:1fr 1fr;gap:0;padding:48px 40px 0}.ft-cta h2{padding-right:40px}.ft-cta>div{padding-left:40px}}
.ft-nav{display:grid;grid-template-columns:1fr 1fr;gap:40px 24px;padding:48px 20px 32px}
.ft-word{grid-column:span 2;font-size:clamp(72px,13vw,210px);font-weight:300;line-height:.78;letter-spacing:-.075em;user-select:none}
.ft-nav nav{display:flex;flex-direction:column;gap:16px}
.ft-nav ul{list-style:none;display:flex;flex-direction:column;gap:8px}
.ft-nav li a,.ft-nav li button{display:inline-flex;align-items:center;gap:6px;font-size:15px;letter-spacing:-.01em;transition:transform .3s ease-out}
.ft-nav li a:hover,.ft-nav li button:hover{transform:translateX(4px)}
.ft-nav li svg{width:14px;height:14px;opacity:0;transform:translateX(-4px);transition:.3s}
.ft-nav li a:hover svg,.ft-nav li button:hover svg{opacity:1;transform:none}
@media(min-width:768px){.ft-nav{grid-template-columns:1fr auto auto;align-items:end;column-gap:96px;padding:64px 40px 40px}.ft-word{grid-column:auto}.ft-nav nav{padding-bottom:12px}}
.ft-bot{display:flex;flex-direction:column;gap:8px;border-top:1px solid var(--line);padding:20px;color:var(--haze)}
@media(min-width:768px){.ft-bot{flex-direction:row;justify-content:space-between;align-items:center;padding:20px 40px}}

/* ---------- dialog ---------- */
dialog{margin:auto;width:min(680px,calc(100vw - 24px));max-height:calc(100svh - 24px);overflow:hidden;border-radius:24px;border:1px solid var(--line);background:#f8fafa;padding:0;color:var(--ink);box-shadow:0 40px 80px -30px rgba(29,42,49,.45)}
dialog::backdrop{background:rgba(29,42,49,.28);backdrop-filter:blur(6px)}
dialog[open]{animation:dlg .5s var(--ease)}
@keyframes dlg{from{opacity:0;transform:translateY(16px) scale(.98)}to{opacity:1;transform:none}}
.dlg-in{max-height:calc(100svh - 24px);overflow-y:auto}
.dlg-head{display:flex;justify-content:space-between;align-items:flex-start;gap:24px;border-bottom:1px solid var(--line);padding:24px 24px 20px}
.dlg-head h2{margin-top:12px;font-size:clamp(26px,3.4vw,38px);font-weight:300;line-height:1.05;letter-spacing:-.045em}
.x{width:36px;height:36px;flex-shrink:0;border-radius:50%;background:#e4e9eb;display:flex;align-items:center;justify-content:center;transition:background .3s}
.x:hover{background:#d7dee1}.x svg{width:16px;height:16px}
form{display:flex;flex-direction:column;gap:24px;padding:24px 24px 28px}
.fgrid{display:grid;gap:24px}
@media(min-width:768px){.dlg-head{padding:32px 36px 20px}form{padding:24px 36px 36px}.fgrid{grid-template-columns:1fr 1fr}}
form label{display:flex;flex-direction:column;gap:6px}
form label>span{color:#66727a}
.inp{height:44px;width:100%;border:0;border-bottom:1px solid var(--line);background:transparent;font:inherit;font-size:15px;letter-spacing:-.01em;color:var(--ink);outline:none;border-radius:0;transition:border-color .3s,box-shadow .3s;appearance:none;-webkit-appearance:none}
.inp::placeholder{color:var(--pale)}
.inp:focus{border-color:var(--ink);box-shadow:0 1px 0 0 var(--ink)}
.inp[aria-invalid=true]{border-color:#c0392b;box-shadow:0 1px 0 0 #c0392b}
select.inp{cursor:pointer;background-image:linear-gradient(45deg,transparent 50%,var(--haze) 50%),linear-gradient(135deg,var(--haze) 50%,transparent 50%);background-position:calc(100% - 10px) 50%,calc(100% - 5px) 50%;background-size:5px 5px;background-repeat:no-repeat}
textarea.inp{height:auto;min-height:88px;resize:none;padding:10px 0;line-height:1.6}
.err{font-size:12px;color:#c0392b;min-height:0}
.ffoot{display:flex;flex-direction:column;gap:16px;border-top:1px solid var(--line);padding-top:24px}
.ffoot p{font-size:13px;color:#66727a}
@media(min-width:768px){.ffoot{flex-direction:row;align-items:center;justify-content:space-between}}
.ok{display:none;padding:48px 36px 56px;flex-direction:column;gap:16px;align-items:flex-start}
.ok.show{display:flex}
.ok h3{font-size:clamp(26px,3vw,36px);font-weight:300;letter-spacing:-.04em}
.ok p{color:var(--haze);max-width:420px;line-height:1.5}
.ok svg{width:56px;height:56px}
.spin{width:14px;height:14px;border-radius:50%;border:1.5px solid rgba(255,255,255,.35);border-top-color:#fff;animation:sp .8s linear infinite;display:none}
.busy .spin{display:block}.busy svg{display:none}
@keyframes sp{to{transform:rotate(360deg)}}
.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0)}
@media (prefers-reduced-motion:reduce){*{animation-duration:.01ms!important;transition-duration:.01ms!important}}
</style>
</head>
<body>

<!-- ============ PRELOADER ============ -->
<div id="pre" role="status" aria-label="Loading Orvane">
  <div class="pan t"><i></i></div><div class="pan b"><i></i></div>
  <div class="pc">
    <canvas id="preCv" aria-hidden="true"></canvas>
    <div class="row"><span class="mono br">Orvane Cortex</span><span class="mono br haze">AI pre-flight check</span></div>
    <div class="row" style="flex-direction:column;align-items:stretch;gap:0">
      <div style="display:flex;justify-content:space-between;align-items:flex-end;gap:24px">
        <p id="prePctWrap" aria-hidden="true"><span id="prePct">0</span><span class="mono">%</span></p>
        <div class="pre-r"><span class="mono haze" id="preIdx">01 / 04</span><span class="mono" id="preStage">Loading perception models</span><span class="mono haze">Points <span id="prePts">0</span></span></div>
      </div>
      <div class="pre-bar"><span id="preBar"></span></div>
    </div>
  </div>
</div>

<div class="rails" aria-hidden="true">
  <i style="left:12px"></i><i style="right:12px"></i>
  <div class="ruler" style="left:20px;width:8px;background-image:repeating-linear-gradient(to bottom,#e3e8ea 0 1px,transparent 1px 18px)"></div>
  <div class="ruler" style="left:20px;width:14px;background-image:repeating-linear-gradient(to bottom,#d3dadd 0 1px,transparent 1px 72px)"></div>
  <div class="ruler" style="right:20px;width:8px;background-image:repeating-linear-gradient(to bottom,#e3e8ea 0 1px,transparent 1px 18px)"></div>
  <div class="ruler" style="right:20px;width:14px;background-image:repeating-linear-gradient(to bottom,#d3dadd 0 1px,transparent 1px 72px)"></div>
</div>

<header class="hdr" data-section="nav">
  <div class="hdr-in">
    <a href="#hero" class="brand" aria-label="Orvane, back to top">
      <svg viewBox="0 0 24 24" fill="none" width="18" height="18" aria-hidden="true"><circle cx="12" cy="12" r="7.25" stroke="currentColor" stroke-width="1.6"/><path d="M1.5 12h3.2M19.3 12h3.2" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/><circle cx="12" cy="12" r="2.6" fill="#8fe3f0"/></svg>
      <b>orvane</b><i></i><em>AI LiDAR Drone Scanning</em>
    </a>
    <p class="hdr-mid md">Orvane Cortex</p>
    <div class="hdr-r">
      <p class="mono clock">GMT <time id="clock">--:--</time></p>
      <button id="menuBtn" type="button" aria-expanded="false" aria-controls="menu">menu</button>
    </div>
  </div>
</header>

<div id="menu" role="dialog" aria-modal="true" aria-label="Site menu" aria-hidden="true">
  <div class="wrap">
    <nav aria-label="Sections"><ul id="menuList"></ul></nav>
    <div class="menu-foot">
      <div style="display:flex;flex-direction:column;gap:12px"><span class="mono br haze">Orvane Cortex Platform</span><p>AI-powered LiDAR survey that flies, detects and reports on its own, for energy, infrastructure, industry and mapping teams.</p></div>
      <button class="btn" data-book>Book a Survey Flight<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M7 7h10v10M7 17 17 7"/></svg></button>
    </div>
  </div>
</div>

<div id="ring" aria-hidden="true">
  <svg viewBox="0 0 44 44"><circle cx="22" cy="22" r="20.5" fill="rgba(246,248,248,.7)" stroke="#d9dfe2"/><circle id="ringArc" cx="22" cy="22" r="20.5" fill="none" stroke="#1d2a31" stroke-dasharray="128.8" stroke-dashoffset="128.8"/></svg>
  <div class="win"><div class="reel" id="reel"><div>1</div><div>2</div><div>3</div><div>4</div><div>5</div><div>6</div></div></div>
</div>
<div id="cursor" aria-hidden="true"></div>

<main id="content">

<!-- ============ HERO ============ -->
<section id="hero" data-section="hero" aria-labelledby="hero-title">
  <div class="hero-card">
    <div class="ghost" aria-hidden="true"><span>orvane</span></div>
    <canvas id="heroCv" aria-hidden="true"></canvas>
    <svg class="cross" style="left:20px;top:20px" viewBox="0 0 16 16" aria-hidden="true"><path d="M8 0v16M0 8h16" stroke="#b9c3c8"/></svg>
    <svg class="cross md" style="right:20px;bottom:20px" viewBox="0 0 16 16" aria-hidden="true"><path d="M8 0v16M0 8h16" stroke="#b9c3c8"/></svg>
    <div class="hero-top"><span class="mono br">Orvane Cortex</span><span class="dash md"></span><span class="mono md">AI-powered survey system</span></div>
    <div class="hud mono md" aria-hidden="true">
      <span><b>ALT</b><em id="hAlt" style="font-style:normal">100.0</em> M</span>
      <span><b>PTS/S</b><em id="hPts" style="font-style:normal">240,000</em></span>
      <span><b>ECHO</b>5 / PULSE</span>
      <span><b>AI</b><em id="hAi" style="font-style:normal">3</em> FLAGS</span><span><b>LINE</b><em id="hLine" style="font-style:normal">014</em></span>
    </div>
    <h1 id="hero-title" class="hero-h">
      <span class="l"><span>AI-powered LiDAR for the structures we rely on.</span></span>
      <span class="l"><span>It flies itself, measures to the centimetre and flags what matters.</span></span>
    </h1>
    <div class="hero-scroll"><span class="md">Scroll Down</span><span class="dots9" aria-hidden="true"><i></i><i style="animation-delay:.16s"></i><i style="animation-delay:.32s"></i><i style="animation-delay:.16s"></i><i style="animation-delay:.32s"></i><i style="animation-delay:.48s"></i><i style="animation-delay:.32s"></i><i style="animation-delay:.48s"></i><i style="animation-delay:.64s"></i></span></div>
  </div>
</section>

<!-- ============ PROMISE ============ -->
<section id="promise" class="sec" data-section="promise" style="--h:220vh;--hm:240vh" aria-labelledby="promise-title">
  <div class="frame" data-io>
    <div class="hl" style="top:84px"></div>
    <div class="vl md" style="left:58%;top:84px;bottom:0"></div>
    <canvas id="sagCv" aria-hidden="true"></canvas>
    <div class="promise-copy"><div>
      <div class="lbl"><span class="mono br">Purpose</span><i class="dash"></i></div>
      <h2 id="promise-title" class="promise-h" data-words data-range="0.06,0.62">AI that finds the hairline crack and the slow sag years before either becomes a headline.</h2>
    </div></div>
    <span class="mono br haze corner-bl">AI early warning</span>
    <div class="ring-sm" aria-hidden="true"><svg viewBox="0 0 48 48"><circle cx="24" cy="24" r="21" fill="none" stroke="#dde3e5"/><circle id="promRing" cx="24" cy="24" r="21" fill="none" stroke="#1d2a31" stroke-dasharray="131.95" stroke-dashoffset="131.95"/></svg><span>01</span></div>
  </div>
</section>

<!-- ============ GEAR ============ -->
<section id="gear" class="sec" data-section="gear" style="--h:240vh;--hm:260vh" aria-labelledby="gear-title">
  <div class="frame" data-io>
    <div class="gear-title"><h2 id="gear-title" class="display giant"><span class="mask"><span>Gear</span></span></h2></div>
    <canvas id="gearCv" aria-hidden="true"></canvas>
    <div class="gear-legend mono md" aria-hidden="true"><span><i style="background:#1d2a31"></i>First return</span><span><i style="background:#5fbfd0"></i>Echo 2–5 · AI labelled</span></div>
    <div class="hl" style="top:52%"></div>
    <div class="vl md" style="left:50%;top:57%;bottom:0"></div>
    <div class="gear-grid">
      <div>
        <div class="lbl"><span class="mono br">Sensor head</span><i class="dash"></i></div>
        <ul class="md"><li><i></i><span class="mono">905 nm eye-safe laser</span></li><li><i></i><span class="mono">Onboard AI processor</span></li><li><i></i><span class="mono">Inertial unit at 200 Hz</span></li><li><i></i><span class="mono">20 MP colour camera</span></li></ul>
      </div>
      <div>
        <p class="gear-big" data-words data-range="0.1,0.45">One sensor head with its own AI, built in-house for nothing but measuring.</p>
        <p class="gear-small" data-words data-range="0.35,0.85">It fires up to 240,000 laser pulses a second and catches five echoes from each, and its onboard AI sorts leaves, wires and steel into labelled layers mid-flight.</p>
      </div>
    </div>
  </div>
</section>

<!-- ============ NUMBERS ============ -->
<section id="numbers" class="sec" data-section="numbers" style="--h:320vh;--hm:340vh" aria-labelledby="numbers-title">
  <div class="frame" data-io>
    <div class="num-head"><h2 id="numbers-title" class="mono">[ By the numbers ]</h2><i class="dash md"></i><span class="mono haze md">Tested at 100 m above ground</span></div>
    <div class="arc-wrap" aria-hidden="true"><canvas id="numCv"></canvas><svg id="arcSvg" viewBox="-112 -112 224 224"></svg></div>
    <div class="num-bottom">
      <div class="hl" style="top:0"></div>
      <div class="num-label mono">[ <span id="numLabel" aria-live="polite">ECHOES</span> ]</div>
      <div class="num-badge" aria-hidden="true"><svg viewBox="0 0 32 32">
        <g class="on"><circle cx="16" cy="16" r="3.2"/></g>
        <g><circle cx="10" cy="10" r="1.6"/><circle cx="16" cy="10" r="1.6"/><circle cx="22" cy="10" r="1.6"/><circle cx="10" cy="16" r="1.6"/><circle cx="16" cy="16" r="1.6"/><circle cx="22" cy="16" r="1.6"/><circle cx="10" cy="22" r="1.6"/><circle cx="16" cy="22" r="1.6"/><circle cx="22" cy="22" r="1.6"/></g>
        <g><circle cx="16" cy="16" r="1.8"/><circle cx="25" cy="16" r="1.35"/><circle cx="22.36" cy="22.36" r="1.35"/><circle cx="16" cy="25" r="1.35"/><circle cx="9.64" cy="22.36" r="1.35"/><circle cx="7" cy="16" r="1.35"/><circle cx="9.64" cy="9.64" r="1.35"/><circle cx="16" cy="7" r="1.35"/><circle cx="22.36" cy="9.64" r="1.35"/></g>
      </svg></div>
      <div class="num-grid">
        <div class="stat on"><p><span class="v" data-to="5">5</span><span class="u">echoes</span></p><span class="mono br">Echoes per pulse</span></div>
        <div class="stat"><p><span class="v">±<span data-to="2">2</span></span><span class="u">cm</span></p><span class="mono br">Positional accuracy</span></div>
        <div class="stat"><p><span class="v" data-to="450">450</span><span class="u">m</span></p><span class="mono br">Usable range</span></div>
      </div>
    </div>
  </div>
</section>

<!-- ============ SOLUTIONS ============ -->
<section id="solutions" class="sec" data-section="solutions" style="--h:400vh;--hm:440vh" aria-labelledby="solutions-title">
  <div class="frame sol-frame" data-io>
    <h2 id="solutions-title" class="display sol-title"><span class="mask"><span>Solutions</span></span></h2>
    <div style="display:flex;flex-direction:column;flex:1;min-height:0">
      <div class="tabs-row">
        <div class="tabs" role="tablist" aria-label="Industries">
          <button type="button" role="tab" aria-selected="true">Energy</button>
          <button type="button" role="tab" aria-selected="false">Infrastructure</button>
          <button type="button" role="tab" aria-selected="false">Industry</button>
          <button type="button" role="tab" aria-selected="false">Geospatial</button>
          <span id="tabLine" aria-hidden="true"></span>
        </div>
        <span class="mono haze md"><span id="solIdx">01</span> / 04</span>
      </div>
      <div class="sol-grid">
        <div class="stack" id="solCopy">
          <p class="sol-copy on"><span style="color:var(--ink)">Solar fields, wind farms and transmission corridors stretch further than any crew can walk in a season.</span> <span data-split>One autonomous pass maps every row, blade and span, and the AI flags whatever has moved since the last flight.</span></p>
          <p class="sol-copy" style="opacity:0"><span style="color:var(--ink)">Bridges, viaducts and towers carry their loads every day, often over water, rail or open road.</span> <span data-split>The AI measures deflection and spots surface wear to the millimetre while the traffic keeps moving underneath.</span></p>
          <p class="sol-copy" style="opacity:0"><span style="color:var(--ink)">Plants, tank farms and stockyards change shape every shift and rarely stop for an audit.</span> <span data-split>Scheduled flights record tanks, racks and piles in a single sweep, and the AI reports volumes and deformation, so inspection becomes routine instead of a shutdown.</span></p>
          <p class="sol-copy" style="opacity:0"><span style="color:var(--ink)">Slopes, coastlines and forests move quietly between survey seasons.</span> <span data-split>Multi-echo pulses see through the canopy, and the AI strips away the trees to give you a bare-ground elevation model in a day.</span></p>
        </div>
        <div class="sol-mid">
          <div class="panel" id="solPanel">
            <canvas id="solCv" aria-hidden="true"></canvas>
            <div class="flash" id="solFlash"></div>
            <div class="sweep" aria-hidden="true"></div>
            <div class="corners" aria-hidden="true"><span class="a"></span><span class="b"></span><span class="c"></span><span class="d"></span></div>
            <span class="mono br tl">AI analysis</span>
            <div class="bl mono" id="solCap">
              <span>Solar field 42 ha, AI row alignment check</span>
              <span style="opacity:0">Truss bridge 310 m, AI deflection check</span>
              <span style="opacity:0">Process plant 1.8 km², AI asset survey</span>
              <span style="opacity:0">Alpine catchment 96 km², AI bare-ground model</span>
            </div>
          </div>
          <div class="chips" id="chips">
            <ul aria-label="Energy applications"><li>Wind Turbines</li><li>Solar Farms</li><li>Power Lines</li><li>Substations</li></ul>
            <ul aria-label="Infrastructure applications" style="opacity:0"><li>Bridges</li><li>Towers</li><li>Rail Corridors</li><li>Tunnels</li></ul>
            <ul aria-label="Industry applications" style="opacity:0"><li>Refineries</li><li>Storage Tanks</li><li>Pipe Racks</li><li>Stockpiles</li></ul>
            <ul aria-label="Geospatial applications" style="opacity:0"><li>Topography</li><li>Forestry</li><li>Coastlines</li><li>Mining</li></ul>
          </div>
        </div>
        <dl class="specs" data-io>
          <div><dt>Scope</dt><dd><b><span data-count="360">0</span>°</b></dd></div>
          <div><dt>AI Models</dt><dd><b data-count="12">0</b></dd></div>
          <div><dt>Coverage</dt><dd><b data-count="100">0</b><small>km²/day</small></dd></div>
          <div><dt>Max Altitude</dt><dd><b data-count="500">0</b><small>m</small></dd></div>
          <div><dt>Accuracy</dt><dd><b>±<span data-count="2">0</span></b><small>cm</small></dd></div>
          <div><dt>Point Rate (K/S)</dt><dd><b data-count="240">0</b></dd></div>
        </dl>
      </div>
    </div>
  </div>
</section>

<!-- ============ CAPABILITIES ============ -->
<section id="capabilities" class="sec" data-section="capabilities" style="--h:360vh;--hm:380vh" aria-labelledby="capabilities-title">
  <div class="frame cap-frame" data-io>
    <h2 id="capabilities-title" aria-label="Capabilities" class="display cap-title"><span class="mask"><span class="letters" data-letters aria-hidden="true">Capabilities</span></span></h2>
    <div class="hl in" style="position:relative;left:0;right:0;margin-top:12px;flex-shrink:0;transform:none"></div>
    <div class="cap-grid">
      <div style="position:relative">
        <span class="steps-tick md" id="capTick" aria-hidden="true"></span>
        <ol class="steps" id="capSteps">
          <li class="on"><span class="mono md">01</span><span>Scan</span></li>
          <li><span class="mono md">02</span><span>Smart link</span></li>
          <li><span class="mono md">03</span><span>Compactness</span></li>
        </ol>
      </div>
      <div class="live">
        <canvas id="capCv" aria-hidden="true"></canvas>
        <span class="mono br tl">Live view</span>
        <span class="tr" aria-hidden="true"><i></i><span class="mono">Rec</span></span>
        <div class="bl mono" id="capCap"><span>Pulse rate 240 kHz, 5 echoes</span><span style="opacity:0">AI band switching, 2.4 and 5.8 GHz</span><span style="opacity:0">Packed 42 x 18 x 11 cm</span></div>
      </div>
      <div class="cap-stat" id="capStat">
        <div><p class="big">360°</p><p class="txt">Everything around and below is measured in one sweep at 240,000 points a second, and the AI labels ground, steel and canopy as it goes.</p></div>
        <div style="opacity:0"><p class="big">7 km</p><p class="txt">A secure two-band link streams the live point cloud and AI findings back to the operator, and switches bands on its own when it detects interference.</p></div>
        <div style="opacity:0"><p class="big">42 cm</p><p class="txt">Folds to 42 cm and is ready to fly in minutes. The AI plans the route, so there is no ground station and no tools.</p></div>
      </div>
    </div>
    <span class="mono br cap-foot" style="left:16px">Tech</span>
    <span class="mono br cap-foot" style="right:16px">Stats</span>
  </div>
</section>

<!-- ============ CONTROLLER ============ -->
<section id="controller" class="sec" data-section="controller" style="--h:400vh" aria-labelledby="controller-title">
  <div class="frame ctl-frame" data-io>
    <h2 id="controller-title" aria-label="Controller" class="display ctl-title"><span class="mask"><span class="letters" data-letters aria-hidden="true">Controller</span></span></h2>
    <div class="tele-m sm mono" aria-hidden="true"><div><span class="haze">Hdg</span> <span data-t="hdg">000°</span></div><div><span class="haze">Pit</span> <span data-t="pit"> 00°</span></div><div><span class="haze">Rol</span> <span data-t="rol"> 00°</span></div><div><span class="haze">Spd</span> <span data-t="spd">0.0</span></div></div>
    <div class="hl in" style="position:relative;left:0;right:0;margin-top:14px;flex-shrink:0;transform:none"></div>
    <div class="ctl-grid">
      <div class="ctl-left">
        <div>
          <span class="mono cb haze">AI-assisted pilot mode</span>
          <p class="h">Take the controls. The AI keeps you steady.</p>
          <p class="s md">The AI holds altitude and smooths every input, and maps each move in real time. Scanned ground lights up beneath you.</p>
        </div>
        <ul class="md mono"><li class="cb">Left stick — altitude + turn</li><li class="cb">Right stick — pitch + roll</li><li class="cb">Triggers — speed</li><li class="cb">Buttons — lights · scan · wake</li></ul>
      </div>
      <div class="ctl-mid">
        <div class="stage" id="stage"><canvas id="ctlCv" aria-hidden="true"></canvas><svg id="compass" viewBox="-100 -30 200 60" aria-hidden="true"></svg></div>
        <div class="pad-zone">
          <div class="pad" role="group" aria-label="Remote controller. Drag the sticks to fly the drone." data-cursor="hover">
            <div class="trig l" data-trig="q">L2 · SLOW</div><div class="trig r" data-trig="e">R2 · BOOST</div>
            <div class="well" id="stickL" aria-label="Left stick"><div class="knob"></div></div>
            <div class="pad-mid">
              <div class="screen" aria-hidden="true"><span><b>ALT</b><i data-t="alt" style="font-style:normal">12.0</i>m</span><span><b>BAT</b><i data-t="bat" style="font-style:normal">98</i>%</span><span><b>PTS</b><i data-t="pts" style="font-style:normal">0</i></span><span><b>LNK</b>5.8G</span></div>
              <div class="pbtns"><button type="button" data-act="lights" aria-pressed="true" aria-label="Lights"><i></i></button><button type="button" data-act="scan" aria-pressed="true" aria-label="Scan"><i></i></button><button type="button" data-act="awake" aria-pressed="true" aria-label="Wake"><i></i></button></div>
              <div class="pbl" aria-hidden="true"><span>LGT</span><span>SCN</span><span>WAK</span></div>
            </div>
            <div class="well" id="stickR" aria-label="Right stick"><div class="knob"></div></div>
          </div>
          <p class="keys mono md" aria-hidden="true">WASD fly · arrows pitch · Q E triggers · R reset</p>
        </div>
      </div>
      <div class="tele md mono" aria-hidden="true">
        <div>{ <span class="haze">Heading</span> <span data-t="hdg">000°</span> }<i><b data-bar="hdg"></b></i></div>
        <div>{ <span class="haze">Pitch</span>   <span data-t="pit"> 00°</span> }<i><b data-bar="pit"></b></i></div>
        <div>{ <span class="haze">Roll</span>    <span data-t="rol"> 00°</span> }<i><b data-bar="rol"></b></i></div>
        <div>{ <span class="haze">Speed</span>   <span data-t="spd">0.0</span> }<i><b data-bar="spd"></b></i></div>
        <div>{ <span class="haze">Mapped</span>  <span data-t="map">0%</span> }<i><b data-bar="map"></b></i></div>
      </div>
    </div>
  </div>
</section>

<!-- ============ SOFTWARE ============ -->
<section id="software" data-section="software" aria-labelledby="software-title">
  <h2 id="software-title" class="display sw-title" data-io aria-label="Software"><span class="mask"><span aria-hidden="true">Software</span></span></h2>
  <div class="sw-body" data-io>
    <div class="hl" style="position:relative;left:0;right:0;margin:0 12px"></div>
    <div class="vl md" style="left:50%;top:0;height:46vh"></div>
    <div class="sw-grid">
      <div><div class="lbl"><span class="mono br">AI pipeline</span><i class="dash"></i></div></div>
      <p class="sw-copy" data-words>The moment the drone lands, its AI cleans the data, classifies every point, flags defects and packages the results, so a finished deliverable reaches your team in under 20 minutes.</p>
    </div>
    <div class="pipe" id="pipe">
      <div class="pipe-head">
        <div><span class="mono haze">Touchdown → delivery</span><p class="pipe-time" id="pipeTime">00:00<small>min</small></p></div>
        <span class="mono haze" id="pipeState">Waiting for touchdown</span>
      </div>
      <div class="track"><b id="pipeFill"></b><i id="pipeDot" style="left:0"></i></div>
      <ol class="pstages" id="pStages">
        <li><b>Land</b><span class="mono">Offload</span></li>
        <li><b>Clean</b><span class="mono">Noise + drift</span></li>
        <li><b>AI classify</b><span class="mono">Ground · veg · steel</span></li>
        <li><b>AI detect</b><span class="mono">Defects + change</span></li>
        <li><b>Deliver</b><span class="mono">To your team</span></li>
      </ol>
      <div class="files mono" id="files"><span>pointcloud.laz</span><span>terrain_dem.tif</span><span>classified.las</span><span>ai_findings.pdf</span></div>
    </div>
  </div>
  <div class="sw-fade" aria-hidden="true"></div>
</section>

<!-- ============ TERRAIN ============ -->
<section id="terrain" class="sec" data-section="terrain" style="--h:380vh;--hm:400vh" aria-labelledby="terrain-title">
  <div class="frame">
    <div class="ter-head">
      <div><h2 id="terrain-title" class="mono">[ Terrain ]</h2><p>An entire range, flown in one pass, drawn line by line as it is scanned and checked by AI as it goes.</p></div>
      <span class="mono haze md">Live pass · <span id="terLine">000</span>/044</span>
    </div>
    <canvas id="terOver" aria-hidden="true"></canvas>
    <div id="terClip">
      <canvas id="terCv" aria-hidden="true"></canvas>
      <div id="hsWrap"></div>
    </div>
    <div class="ter-foot" id="terFoot">
      <div><span class="mono br">AI region survey</span><span class="mono" style="color:rgba(29,42,49,.7)">High ridge survey, sector N4</span></div>
      <div style="align-items:flex-end;text-align:right"><span class="mono">46.5583° N  8.0047° E</span><span class="mono" style="color:rgba(29,42,49,.7)">ALT 3,180 M</span></div>
    </div>
  </div>
</section>
</main>

<!-- ============ FOOTER ============ -->
<footer id="contact" data-section="footer" aria-labelledby="footer-title">
  <div class="ft-stage">
    <div class="ft-glow" aria-hidden="true"></div>
    <div id="viewer" role="application" aria-roledescription="drone viewer" aria-label="Drone viewer. Drag, or use the left and right arrow keys, to turn the drone." tabindex="0" data-cursor="hover"><canvas id="viewCv" aria-hidden="true"></canvas></div>
    <span class="mono drag-hint" id="dragHint" aria-hidden="true"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M16.466 7.5C15.643 4.237 13.952 2 12 2 9.239 2 7 6.477 7 12s2.239 10 5 10c.342 0 .677-.069 1-.2"/><path d="m15.194 13.707 3.814 1.86-1.86 3.814"/><path d="M19 15.57c-1.804.885-4.274 1.43-7 1.43-5.523 0-10-2.239-10-5s4.477-5 10-5c4.838 0 8.873 1.718 9.8 4"/></svg>Drag to turn</span>
    <div class="ft-corner"><span class="mono br">Orvane Cortex</span><span class="mono">AI cleared for flight</span></div>
  </div>
  <div class="ft-line"></div>
  <div class="ft-cta">
    <h2 id="footer-title">What should our AI inspect for you next?</h2>
    <div><p>Book a survey flight and get a complete point cloud and AI findings report back within 24 hours.</p><button class="btn lg" data-book>Book a Survey Flight<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M7 7h10v10M7 17 17 7"/></svg></button></div>
  </div>
  <div class="ft-nav">
    <p class="ft-word" aria-hidden="true">orvane</p>
    <nav aria-label="Platform"><span class="mono br haze">Platform</span><ul>
      <li><a href="#gear">Payload<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></a></li>
      <li><a href="#software">Software<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></a></li>
      <li><a href="#software">Integrations<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></a></li>
      <li><a href="#terrain">Data Delivery<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></a></li>
    </ul></nav>
    <nav aria-label="Company"><span class="mono br haze">Company</span><ul>
      <li><a href="#promise">About<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></a></li>
      <li><button type="button" data-book="careers">Careers<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></button></li>
      <li><button type="button" data-book="partnership">Contact<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></button></li>
      <li><button type="button" data-book="press">Press<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14m-7-7 7 7-7 7"/></svg></button></li>
    </ul></nav>
  </div>
  <div class="ft-bot"><span class="mono">© 2026 Orvane Aerial Systems. All rights reserved.</span><span class="mono">Specifications are indicative and may change without notice.</span><span class="mono">Orvane Cortex v1.0</span></div>
</footer>

<!-- ============ DIALOG ============ -->
<dialog id="dlg" aria-labelledby="request-title">
  <div class="dlg-in">
    <div class="dlg-head">
      <div><span class="mono br haze">Survey request</span><h2 id="request-title">Tell us what to fly over.</h2></div>
      <button type="button" class="x" aria-label="Close" data-close><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M18 6 6 18M6 6l12 12"/></svg></button>
    </div>
    <form id="form" novalidate>
      <div class="fgrid">
        <label><span class="mono">Name *</span><input class="inp" name="name" autocomplete="name" placeholder="Jordan Ellis"><span class="err" data-err="name"></span></label>
        <label><span class="mono">Work email *</span><input class="inp" type="email" name="email" autocomplete="email" placeholder="jordan@utility.com"><span class="err" data-err="email"></span></label>
        <label><span class="mono">Company</span><input class="inp" name="company" autocomplete="organization" placeholder="Northline Grid Operations"></label>
        <label><span class="mono">Site location</span><input class="inp" name="location" placeholder="Region, coordinates or address"></label>
        <label><span class="mono">Sector</span><select class="inp" name="sector"><option>Energy</option><option>Infrastructure</option><option>Industry</option><option>Geospatial</option><option>Other</option></select></label>
        <label><span class="mono">Topic</span><select class="inp" name="topic"><option value="survey">Survey flight</option><option value="partnership">Partnership</option><option value="careers">Careers</option><option value="press">Press</option></select></label>
      </div>
      <label><span class="mono">What should we inspect?</span><textarea class="inp" name="message" rows="3" placeholder="Asset type, approximate area and any deadlines."></textarea></label>
      <label class="sr" aria-hidden="true">Website<input tabindex="-1" autocomplete="off" name="website"></label>
      <div class="ffoot"><p>We reply within one business day.</p><button type="submit" class="btn" id="sendBtn">Send request<svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M7 7h10v10M7 17 17 7"/></svg><i class="spin"></i></button></div>
    </form>
    <div class="ok" id="ok">
      <svg viewBox="0 0 56 56" fill="none"><circle cx="28" cy="28" r="27" stroke="#dde3e5"/><circle cx="28" cy="28" r="27" stroke="#1d2a31" stroke-dasharray="170" stroke-dashoffset="170" style="transition:stroke-dashoffset 1s cubic-bezier(.22,1,.36,1)" id="okRing" transform="rotate(-90 28 28)"/><path d="m19 28.5 6 6 12-13" stroke="#1d2a31" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round"/><circle cx="28" cy="28" r="3" fill="#8fe3f0" opacity="0"/></svg>
      <span class="mono br haze">Flight logged</span>
      <h3>Request received.</h3>
      <p id="okTxt">We'll review the site and come back within one business day with a flight window.</p>
      <button class="btn" type="button" data-close>Close</button>
    </div>
  </div>
</dialog>

<script>
(()=>{
'use strict';
const $=(s,r=document)=>r.querySelector(s),$$=(s,r=document)=>[...r.querySelectorAll(s)];
const clamp=(v,a=0,b=1)=>v<a?a:v>b?b:v,lerp=(a,b,t)=>a+(b-a)*t;
const ease=t=>t<.5?4*t*t*t:1-Math.pow(-2*t+2,3)/2,eo=t=>1-Math.pow(1-t,3);
const DPR=Math.min(window.devicePixelRatio||1,2);
const RM=matchMedia('(prefers-reduced-motion: reduce)').matches;
const FINE=matchMedia('(pointer:fine)').matches;
const INK='#1d2a31',GL='#8fe3f0',GL2='#5fbfd0',MONO='JetBrains Mono, ui-monospace, monospace';
let VW=innerWidth,VH=innerHeight;
addEventListener('resize',()=>{VW=innerWidth;VH=innerHeight;},{passive:true});

function cv(c){const r=c.getBoundingClientRect(),w=Math.max(1,r.width),h=Math.max(1,r.height);
  if(c._w!==w||c._h!==h){c._w=w;c._h=h;c.width=Math.round(w*DPR);c.height=Math.round(h*DPR);}
  const x=c.getContext('2d');x.setTransform(DPR,0,0,DPR,0,0);x.clearRect(0,0,w,h);return[x,w,h];}
function prog(sec){const r=sec.getBoundingClientRect();return clamp(-r.top/Math.max(1,r.height-VH));}
function rng(s){return()=>{s|=0;s=s+0x6D2B79F5|0;let t=Math.imul(s^s>>>15,1|s);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296;};}
const rY=(p,a)=>{const c=Math.cos(a),s=Math.sin(a);return[p[0]*c+p[2]*s,p[1],-p[0]*s+p[2]*c];};
const rX=(p,a)=>{const c=Math.cos(a),s=Math.sin(a);return[p[0],p[1]*c-p[2]*s,p[1]*s+p[2]*c];};
const rZ=(p,a)=>{const c=Math.cos(a),s=Math.sin(a);return[p[0]*c-p[1]*s,p[0]*s+p[1]*c,p[2]];};
function camera(o){const cy=Math.cos(o.yaw),sy=Math.sin(o.yaw),cp=Math.cos(-o.pitch),sp=Math.sin(-o.pitch);
  return p=>{const x1=p[0]*cy+p[2]*sy,z1=-p[0]*sy+p[2]*cy;const y2=p[1]*cp-z1*sp,z2=p[1]*sp+z1*cp;const z=z2+o.dist,k=o.f/Math.max(.05,z);return[o.cx+x1*k,o.cy-y2*k,z,k];};}

/* ---------- render registry ---------- */
const R=[],vis=new WeakMap();
const io=new IntersectionObserver(es=>es.forEach(e=>vis.set(e.target,e.isIntersecting)),{rootMargin:'120px'});
function reg(el,fn){io.observe(el);R.push({el,fn});}

/* ---------- drone model ---------- */
const DRONE=(()=>{const dots=[],lines=[],rings=[],lights=[];const G=2.39996323;
  for(let i=0;i<240;i++){const y=1-2*(i+.5)/240,r=Math.sqrt(1-y*y),th=i*G;dots.push([Math.cos(th)*r*.36,y*.11+.03,Math.sin(th)*r*.27,0]);}
  for(let i=0;i<70;i++){const th=i*G,rr=Math.sqrt((i+.5)/70);dots.push([Math.cos(th)*rr*.22,.15,Math.sin(th)*rr*.17,0]);}
  for(let i=0;i<110;i++){const y=1-2*(i+.5)/110,r=Math.sqrt(1-y*y),th=i*G;dots.push([Math.cos(th)*r*.1,-.17+y*.09,.17+Math.sin(th)*r*.1,1]);}
  [[1,1],[1,-1],[-1,1],[-1,-1]].forEach(([a,b])=>{const ax=a*.72,az=b*.72;
    lines.push([[ax*.3,.03,az*.3],[ax,.05,az]],[[ax*.3,-.02,az*.3],[ax,.0,az]],[[ax,-.05,az],[ax,.1,az]]);
    for(let i=0;i<14;i++){const th=i/14*Math.PI*2;dots.push([ax+Math.cos(th)*.06,.02,az+Math.sin(th)*.06,2]);}
    rings.push([ax,.11,az]);lights.push([ax,-.06,az,b>0?1:0]);});
  [-1,1].forEach(s=>{lines.push([[s*.17,-.08,-.1],[s*.25,-.33,-.13]],[[s*.17,-.08,.12],[s*.25,-.33,.15]],[[s*.25,-.33,-.32],[s*.25,-.33,.34]]);});
  return{dots,lines,rings,lights};})();

function drawDrone(x,cam,o){
  const S=o.s||1,P0=o.pos,a=o.alpha==null?1:o.alpha;
  const cr=Math.cos(o.roll||0),sr=Math.sin(o.roll||0),ct=Math.cos(o.tilt||0),st=Math.sin(o.tilt||0),cy=Math.cos(o.yaw||0),sy=Math.sin(o.yaw||0);
  const tf=p=>{let X=p[0]*cr-p[1]*sr,Y=p[0]*sr+p[1]*cr,Z=p[2];const Y2=Y*ct-Z*st,Z2=Y*st+Z*ct;Y=Y2;Z=Z2;const X3=X*cy+Z*sy,Z3=-X*sy+Z*cy;return cam([X3*S+P0[0],Y*S+P0[1],Z3*S+P0[2]]);};
  x.lineCap='round';
  const spin=o.spin==null?1:o.spin,t=o.t||0;
  // rotor discs (back)
  for(const c of DRONE.rings){x.beginPath();for(let i=0;i<=40;i++){const th=i/40*Math.PI*2;const P=tf([c[0]+Math.cos(th)*.31,c[1],c[2]+Math.sin(th)*.31]);i?x.lineTo(P[0],P[1]):x.moveTo(P[0],P[1]);}
    if(spin>.05){x.fillStyle=`rgba(143,227,240,${.13*spin*a})`;x.fill();}
    x.strokeStyle=`rgba(29,42,49,${.3*a})`;x.lineWidth=1;x.stroke();}
  x.strokeStyle=`rgba(29,42,49,${.85*a})`;x.lineWidth=Math.max(1,1.4*Math.min(1.6,S));x.beginPath();
  for(const[p,q]of DRONE.lines){const A=tf(p),B=tf(q);x.moveTo(A[0],A[1]);x.lineTo(B[0],B[1]);}x.stroke();
  for(const d of DRONE.dots){const P=tf(d);const rr=Math.max(.55,P[3]*.0085*S);const dep=d[3]===1?.95:.55+.35*clamp((d[1]+.12)/.3);
    x.fillStyle=d[3]===1?`rgba(29,42,49,${a})`:`rgba(29,42,49,${dep*a})`;x.fillRect(P[0]-rr,P[1]-rr,rr*2,rr*2);}
  const L=tf([0,-.17,.275]);const lr=Math.max(1.5,L[3]*.035*S);
  const g=x.createRadialGradient(L[0],L[1],0,L[0],L[1],lr*3);g.addColorStop(0,`rgba(143,227,240,${a})`);g.addColorStop(1,'rgba(143,227,240,0)');
  x.fillStyle=g;x.beginPath();x.arc(L[0],L[1],lr*3,0,7);x.fill();x.fillStyle=`rgba(29,42,49,${a})`;x.beginPath();x.arc(L[0],L[1],lr*.55,0,7);x.fill();
  // blades
  x.lineWidth=Math.max(1,1.6*Math.min(1.6,S));
  DRONE.rings.forEach((c,i)=>{const ang=t*(2+38*spin)*(i%2?1:-1)+i;const dx=Math.cos(ang)*.29,dz=Math.sin(ang)*.29;const A=tf([c[0]+dx,c[1]+.01,c[2]+dz]),B=tf([c[0]-dx,c[1]+.01,c[2]-dz]);
    x.strokeStyle=`rgba(29,42,49,${(spin>.5?.45:.9)*a})`;x.beginPath();x.moveTo(A[0],A[1]);x.lineTo(B[0],B[1]);x.stroke();});
  if(o.lights){const blink=.55+.45*Math.sin(t*6);for(const l of DRONE.lights){const P=tf(l);const r=Math.max(2,P[3]*.05*S);const col=l[3]?'143,227,240':'255,255,255';
    const gg=x.createRadialGradient(P[0],P[1],0,P[0],P[1],r*2.2);gg.addColorStop(0,`rgba(${col},${blink*a})`);gg.addColorStop(1,`rgba(${col},0)`);x.fillStyle=gg;x.beginPath();x.arc(P[0],P[1],r*2.2,0,7);x.fill();}}
}


/* ---------- premium hero drone (shaded mesh) ---------- */
const nrm=a=>{const l=Math.hypot(a[0],a[1],a[2])||1;return[a[0]/l,a[1]/l,a[2]/l];};
const crs=(a,b)=>[a[1]*b[2]-a[2]*b[1],a[2]*b[0]-a[0]*b[2],a[0]*b[1]-a[1]*b[0]];
const HMAT={shell:{c:[232,238,241],a:.5,d:.55,s:.9,p:70,r:.5},glass:{c:[20,30,36],a:.75,d:.2,s:1.4,p:120,r:.45},carbon:{c:[36,46,52],a:.6,d:.45,s:.6,p:30,r:.2},
  metal:{c:[150,162,168],a:.42,d:.68,s:1.2,p:48,r:.15},lens:{c:[10,18,24],a:.7,d:.15,s:1.8,p:160,r:.4},accent:{c:[143,227,240],e:1},emis:{c:[175,240,250],e:1}};
const HMOT=[[.72,.72],[.72,-.72],[-.72,.72],[-.72,-.72]];
const HMESH=(()=>{const T=[];const P=(a,b,c,n,m)=>T.push({a,b,c,n,m});
  function ell(c,r,su,sv,m){for(let i=0;i<sv;i++)for(let j=0;j<su;j++){const v0=i/sv*Math.PI,v1=(i+1)/sv*Math.PI,u0=j/su*Math.PI*2,u1=(j+1)/su*Math.PI*2;
    const pt=(u,v)=>[c[0]+r[0]*Math.sin(v)*Math.cos(u),c[1]+r[1]*Math.cos(v),c[2]+r[2]*Math.sin(v)*Math.sin(u)];const um=(u0+u1)/2,vm=(v0+v1)/2;
    const n=nrm([Math.sin(vm)*Math.cos(um)/r[0],Math.cos(vm)/r[1],Math.sin(vm)*Math.sin(um)/r[2]]);const mm=typeof m==='function'?m(um,vm):m;
    const A=pt(u0,v0),B=pt(u1,v0),C=pt(u1,v1),D=pt(u0,v1);if(i>0)P(A,B,C,n,mm);if(i<sv-1)P(A,C,D,n,mm);}}
  function cyl(a,b,r0,r1,seg,m,capA,capB){const w=nrm([b[0]-a[0],b[1]-a[1],b[2]-a[2]]);const tt=Math.abs(w[1])<.9?[0,1,0]:[1,0,0];const u=nrm(crs(w,tt)),v=crs(w,u);
    const dir=k=>{const an=k/seg*Math.PI*2,c=Math.cos(an),s=Math.sin(an);return[u[0]*c+v[0]*s,u[1]*c+v[1]*s,u[2]*c+v[2]*s];};
    const at=(o,d,r)=>[o[0]+d[0]*r,o[1]+d[1]*r,o[2]+d[2]*r];
    for(let k=0;k<seg;k++){const d0=dir(k),d1=dir(k+1),dm=dir(k+.5);const p0=at(a,d0,r0),p1=at(a,d1,r0),q0=at(b,d0,r1),q1=at(b,d1,r1);
      P(p0,p1,q1,dm,m);P(p0,q1,q0,dm,m);if(capB)P(b,q0,q1,w,capB);if(capA)P(a,p1,p0,[-w[0],-w[1],-w[2]],capA);}}
  ell([0,.02,0],[.38,.125,.33],26,16,(u,v)=>Math.abs(v-1.67)<.1?'accent':(v<.9&&Math.sin(u)>-.1)?'glass':'shell');
  ell([0,-.065,-.02],[.31,.055,.26],22,8,'carbon');
  HMOT.forEach(([ax,az])=>{cyl([ax*.3,0,az*.3],[ax,0,az],.05,.032,10,'carbon');
    cyl([ax,-.055,az],[ax,.07,az],.086,.086,14,'metal','carbon',null);ell([ax,.07,az],[.082,.03,.082],14,5,'metal');
    cyl([ax,.004,az],[ax,.02,az],.09,.09,14,'accent');cyl([ax,.09,az],[ax,.125,az],.016,.016,8,'metal',null,'metal');});
  cyl([0,-.08,.17],[0,-.13,.19],.03,.03,10,'carbon');
  [-1,1].forEach(sx=>{cyl([sx*.115,-.115,.2],[sx*.115,-.19,.2],.013,.013,6,'metal');cyl([sx*.1,-.19,.2],[sx*.125,-.19,.2],.03,.03,12,'metal','metal','metal');});
  ell([0,-.19,.2],[.1,.095,.1],16,10,'carbon');
  cyl([0,-.19,.255],[0,-.19,.305],.066,.06,20,'metal',null,'lens');
  cyl([0,-.19,.305],[0,-.19,.311],.03,.03,14,'emis',null,'emis');
  [-1,1].forEach(sx=>{cyl([sx*.17,-.09,-.11],[sx*.25,-.335,-.14],.016,.013,6,'carbon');cyl([sx*.17,-.09,.12],[sx*.25,-.335,.16],.016,.013,6,'carbon');
    cyl([sx*.25,-.34,-.32],[sx*.25,-.34,.34],.018,.018,8,'carbon','carbon','carbon');});
  cyl([0,.13,-.13],[0,.2,-.13],.012,.012,8,'carbon');ell([0,.205,-.13],[.055,.016,.055],14,5,'shell');
  return T;})();
const LT=nrm([-.45,.82,-.38]);
function droneXf(o){const S=o.s||1,P0=o.pos,cr=Math.cos(o.roll||0),sr=Math.sin(o.roll||0),ct=Math.cos(o.tilt||0),st=Math.sin(o.tilt||0),cy=Math.cos(o.yaw||0),sy=Math.sin(o.yaw||0);
  const R=p=>{const X=p[0]*cr-p[1]*sr,Y=p[0]*sr+p[1]*cr,Z=p[2];const Y2=Y*ct-Z*st,Z2=Y*st+Z*ct;return[X*cy+Z2*sy,Y2,-X*sy+Z2*cy];};
  const f=p=>{const q=R(p);return[q[0]*S+P0[0],q[1]*S+P0[1],q[2]*S+P0[2]];};f.rot=R;return f;}
function heroDroneDraw(x,cp,o,t){const W=droneXf(o);const cyw=Math.cos(cp.yaw),syw=Math.sin(cp.yaw),cpp=Math.cos(-cp.pitch),spp=Math.sin(-cp.pitch);
  const C=p=>{const x1=p[0]*cyw+p[2]*syw,z1=-p[0]*syw+p[2]*cyw;return[x1,p[1]*cpp-z1*spp,p[1]*spp+z1*cpp];};
  const Pj=q=>{const k=cp.f/(q[2]+cp.dist);return[cp.cx+q[0]*k,cp.cy-q[1]*k,k];};
  const list=[];let b0=1e9,b1=1e9,b2=-1e9,b3=-1e9;
  for(const T of HMESH){const a=C(W(T.a)),b=C(W(T.b)),c=C(W(T.c));const mx=(a[0]+b[0]+c[0])/3,my=(a[1]+b[1]+c[1])/3,mz=(a[2]+b[2]+c[2])/3+cp.dist;
    const n=C(W.rot(T.n));const vl=Math.hypot(mx,my,mz);const V=[-mx/vl,-my/vl,-mz/vl];const ndv=n[0]*V[0]+n[1]*V[1]+n[2]*V[2];if(ndv<=0)continue;
    const M=HMAT[T.m];let r,g,bl;
    if(M.e){const pu=.88+.12*Math.sin(t*3);r=M.c[0]*pu;g=M.c[1]*pu;bl=M.c[2]*pu;}
    else{const d=Math.max(0,n[0]*LT[0]+n[1]*LT[1]+n[2]*LT[2]);const H=nrm([LT[0]+V[0],LT[1]+V[1],LT[2]+V[2]]);const sp=Math.pow(Math.max(0,n[0]*H[0]+n[1]*H[1]+n[2]*H[2]),M.p)*M.s;
      const rim=Math.pow(1-ndv,3)*M.r,bo=Math.max(0,-n[1])*.25,k=M.a+M.d*d;
      r=M.c[0]*k+255*sp+120*rim+50*bo;g=M.c[1]*k+255*sp+205*rim+140*bo;bl=M.c[2]*k+255*sp+222*rim+160*bo;}
    const A=Pj(a),B=Pj(b),Cc=Pj(c);
    for(const q of[A,B,Cc]){if(q[0]<b0)b0=q[0];if(q[1]<b1)b1=q[1];if(q[0]>b2)b2=q[0];if(q[1]>b3)b3=q[1];}
    list.push([mz,A,B,Cc,`rgb(${r>255?255:r|0},${g>255?255:g|0},${bl>255?255:bl|0})`]);}
  list.sort((p,q)=>q[0]-p[0]);x.lineJoin='round';x.lineWidth=.7;
  for(const L of list){x.fillStyle=x.strokeStyle=L[4];x.beginPath();x.moveTo(L[1][0],L[1][1]);x.lineTo(L[2][0],L[2][1]);x.lineTo(L[3][0],L[3][1]);x.closePath();x.fill();x.stroke();}
  HMOT.forEach(([ax,az],i)=>{const h0=Pj(C(W([ax,.128,az]))),ex=Pj(C(W([ax+.31,.128,az]))),ez=Pj(C(W([ax,.128,az+.31])));const dirn=i%2?1:-1;
    x.save();x.transform(ex[0]-h0[0],ex[1]-h0[1],ez[0]-h0[0],ez[1]-h0[1],h0[0],h0[1]);
    const gr=x.createRadialGradient(0,0,0,0,0,1);gr.addColorStop(0,'rgba(255,255,255,0)');gr.addColorStop(.55,'rgba(225,242,246,.10)');gr.addColorStop(.9,'rgba(143,227,240,.24)');gr.addColorStop(.965,'rgba(255,255,255,.55)');gr.addColorStop(1,'rgba(143,227,240,0)');
    x.fillStyle=gr;x.beginPath();x.arc(0,0,1,0,7);x.fill();
    const ang=t*24*dirn+i*1.3;
    for(let k=0;k<10;k++){x.save();x.rotate(ang-dirn*k*.065);x.fillStyle=`rgba(29,42,49,${.5*Math.pow(1-k/10,1.8)})`;
      for(let bb=0;bb<2;bb++){if(bb)x.rotate(Math.PI);x.beginPath();x.moveTo(.1,-.055);x.quadraticCurveTo(.6,-.09,.97,-.012);x.lineTo(.97,.018);x.quadraticCurveTo(.55,.05,.1,.05);x.closePath();x.fill();}
      x.restore();}
    const hg2=x.createRadialGradient(-.03,-.03,0,0,0,.11);hg2.addColorStop(0,'#c9d3d8');hg2.addColorStop(1,'#1d2a31');x.fillStyle=hg2;x.beginPath();x.arc(0,0,.11,0,7);x.fill();
    x.restore();});
  x.save();x.globalCompositeOperation='lighter';
  const glow=(p,rr,col,al)=>{const g=x.createRadialGradient(p[0],p[1],0,p[0],p[1],rr);g.addColorStop(0,`rgba(${col},${al})`);g.addColorStop(.25,`rgba(${col},${al*.45})`);g.addColorStop(1,`rgba(${col},0)`);x.fillStyle=g;x.beginPath();x.arc(p[0],p[1],rr,0,7);x.fill();};
  HMOT.forEach(([ax,az])=>{const p=Pj(C(W([ax,-.065,az])));const front=az>0;const st=front?.85+.15*Math.sin(t*2):(Math.sin(t*4.4)>.93?1:.25);glow(p,p[2]*.16*(o.s||1),front?'143,227,240':'255,226,206',st);});
  const lp=Pj(C(W([0,-.19,.312])));glow(lp,lp[2]*.22*(o.s||1)*(1+.08*Math.sin(t*5)),'143,227,240',.95);
  x.restore();
  return[b0,b1,b2,b3];}

/* ---------- preloader ---------- */
const pre=$('#pre'),preCv=$('#preCv'),prePct=$('#prePct'),preStage=$('#preStage'),preIdx=$('#preIdx'),prePts=$('#prePts'),preBar=$('#preBar');
const STG=['Loading perception models','Calibrating LiDAR and inertial unit','Planning autonomous route','Cleared for flight'];
const FIB=[];for(let i=0;i<1200;i++){const y=1-2*(i+.5)/1200,r=Math.sqrt(1-y*y),th=i*2.39996323;FIB.push([Math.cos(th)*r,y,Math.sin(th)*r]);}
const FIBO=FIB.map((_,i)=>i).sort((a,b)=>FIB[b][1]-FIB[a][1]);
const preStart=performance.now(),PRE_DUR=RM?500:2800;
function preFrame(now){const t=now/1000,p=clamp((now-preStart)/PRE_DUR),e=ease(p);
  const[x,w,h]=cv(preCv);const Rr=Math.min(w,h)*.4;const cam=camera({cx:w/2,cy:h/2,f:Rr*3.2,dist:3.2,yaw:t*.55,pitch:.32});
  const band=1-2*e;const n=Math.floor(FIBO.length*Math.min(1,e*1.08));
  for(let k=0;k<n;k++){const q=FIB[FIBO[k]];const P=cam(q);const d=clamp((4.2-P[2])/2);const near=Math.abs(q[1]-band)<.06;
    x.fillStyle=near?GL2:`rgba(29,42,49,${.12+.62*d})`;const s=near?2.4:.9+d*1.3;x.fillRect(P[0]-s/2,P[1]-s/2,s,s);}
  x.strokeStyle='rgba(95,191,208,.5)';x.lineWidth=1;x.beginPath();x.ellipse(w/2,h/2-band*Rr*.95,Rr*Math.sqrt(Math.max(0,1-band*band)),Rr*Math.sqrt(Math.max(0,1-band*band))*.3,0,0,7);x.stroke();
  prePct.textContent=Math.round(e*100);const si=Math.min(3,Math.floor(e*4));
  if(preStage._i!==si){preStage._i=si;preStage.textContent=STG[si];preStage.classList.remove('fx');void preStage.offsetWidth;preStage.classList.add('fx');preIdx.textContent='0'+(si+1)+' / 04';}
  prePts.textContent=Math.round(e*1284000).toLocaleString('en-US');preBar.style.transform=`scaleX(${e})`;
  if(p<1)requestAnimationFrame(preFrame);else finishPre();}
function finishPre(){pre.classList.add('done');setTimeout(()=>{document.documentElement.classList.remove('loading');document.body.classList.add('ready');},650);setTimeout(()=>pre.remove(),2000);}
requestAnimationFrame(preFrame);

/* ---------- chrome: clock, menu, cursor, ring ---------- */
const clock=$('#clock');function tick(){const d=new Date();clock.textContent=String(d.getUTCHours()).padStart(2,'0')+':'+String(d.getUTCMinutes()).padStart(2,'0')+':'+String(d.getUTCSeconds()).padStart(2,'0');}tick();setInterval(tick,1000);
const NAV=[['hero','Overview'],['gear','Gear'],['numbers','Numbers'],['solutions','Solutions'],['capabilities','Capabilities'],['terrain','Terrain']];
const menu=$('#menu'),menuBtn=$('#menuBtn'),ml=$('#menuList');
NAV.forEach(([id,t],i)=>{ml.insertAdjacentHTML('beforeend',`<li><a href="#${id}"><span class="mono">0${i+1}</span><span class="t" style="transition-delay:${i*55}ms">${t}</span><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M7 7h10v10M7 17 17 7"/></svg></a></li>`);});
function setMenu(o){menu.classList.toggle('open',o);menu.setAttribute('aria-hidden',!o);menuBtn.setAttribute('aria-expanded',o);menuBtn.textContent=o?'close':'menu';if(o)menu.removeAttribute('inert');else menu.setAttribute('inert','');}
setMenu(false);
menuBtn.addEventListener('click',()=>setMenu(!menu.classList.contains('open')));
$$('a',menu).forEach(a=>a.addEventListener('click',()=>setMenu(false)));
addEventListener('keydown',e=>{if(e.key==='Escape')setMenu(false);});
const cur=$('#cursor');let cx=0,cy=0,tx=0,ty=0;
if(FINE){addEventListener('pointermove',e=>{tx=e.clientX;ty=e.clientY;cur.style.opacity=1;const h=e.target.closest&&e.target.closest('a,button,[data-cursor],input,select,textarea,.well');cur.classList.toggle('big',!!h);},{passive:true});}
const ringArc=$('#ringArc'),reel=$('#reel');const navSecs=NAV.map(n=>document.getElementById(n[0]));

/* ---------- word & letter splitting ---------- */
$$('[data-words]').forEach(el=>{const words=el.textContent.trim().split(/\s+/);el.innerHTML=words.map(w=>`<span class="rw">${w}</span>`).join(' ');el._w=$$('.rw',el);
  const rg=el.dataset.range;if(rg){el._r=rg.split(',').map(Number);el._sec=el.closest('.sec');}});
$$('[data-split]').forEach(el=>{el.innerHTML=el.textContent.trim().split(/\s+/).map((w,i)=>`<span class="w" style="transition-delay:${i*28}ms">${w}</span>`).join(' ');});
$$('[data-letters]').forEach(el=>{el.innerHTML=[...el.textContent].map(c=>`<span>${c}</span>`).join('');el._l=$$('span',el);el._sec=el.closest('.sec');});

/* ---------- in-view classes & counters ---------- */
const io2=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');$$('[data-count]',e.target).forEach(countUp);}}),{threshold:.15});
$$('[data-io]').forEach(el=>io2.observe(el));
function countUp(el){if(el._done)return;el._done=1;const to=+el.dataset.count||+el.dataset.to,t0=performance.now();(function f(n){const p=clamp((n-t0)/1100);el.textContent=Math.round(to*eo(p));if(p<1)requestAnimationFrame(f);})(t0);}

/* ---------- HERO ---------- */
const heroCv=$('#heroCv');let mx=0,my=0,smx=0,smy=0;
addEventListener('pointermove',e=>{mx=e.clientX/VW-.5;my=e.clientY/VH-.5;},{passive:true});
const hg=(x,z)=>.32*Math.sin(x*.62+z*.27)+.22*Math.sin(z*.8-x*.45)+.09*Math.sin(x*1.9+z*1.4);
const HP=[];for(let i=0;i<=64;i++)for(let j=0;j<=34;j++){const X=-8+i*.25,Z=-1.6+j*.44;HP.push([X,-1.75+hg(X,Z),Z]);}
let heroBB=null;const hAlt=$('#hAlt'),hPts=$('#hPts'),hLine=$('#hLine');let hudT=0;
reg(heroCv,(t)=>{const[x,w,h]=cv(heroCv);smx=lerp(smx,mx,.05);smy=lerp(smy,my,.05);
  const f=Math.min(w<700?w*1.3:w*.8,h*1.2);const cp={cx:w/2,cy:h*.4,f,dist:6.2,yaw:smx*.3+Math.sin(t*.13)*.06,pitch:.36+smy*.08};const cam=camera(cp);
  const sz=((t*1.45)%17)-1.6;
  for(const p of HP){const P=cam(p);if(P[2]<.4||P[0]<-4||P[0]>w+4||P[1]>h+4)continue;const dz=p[2]-sz;let a,s=1.3,c='29,42,49';
    if(Math.abs(dz)<.22){c='95,191,208';a=.95;s=2.2;}else if(dz<0){a=.12+.4*clamp(1+dz/12);}else a=.08;
    const edge=clamp(Math.min(P[0],w-P[0])/(w*.12));x.fillStyle=`rgba(${c},${a*edge})`;x.fillRect(P[0]-s/2,P[1]-s/2,s,s);}
  const pose={pos:[0,.78+Math.sin(t*1.3)*.07,0],yaw:Math.PI+Math.sin(t*.4)*.32+smx*.5,tilt:-.07+Math.sin(t*.9)*.025,roll:Math.sin(t*.7)*.045,s:1.22};
  const DW=droneXf(pose);const src=cam(DW([0,-.19,.31]));
  const sp=[];for(let X=-6;X<=6.01;X+=.5)sp.push(cam([X,-1.75+hg(X,sz),sz]));
  const wg=x.createLinearGradient(0,src[1],0,Math.max(...sp.map(q=>q[1])));wg.addColorStop(0,'rgba(143,227,240,.22)');wg.addColorStop(1,'rgba(143,227,240,.02)');
  x.beginPath();x.moveTo(src[0],src[1]);sp.forEach(q=>x.lineTo(q[0],q[1]));x.closePath();x.fillStyle=wg;x.fill();
  x.strokeStyle='rgba(95,191,208,.3)';x.lineWidth=.6;x.beginPath();for(let i=0;i<sp.length;i+=3){x.moveTo(src[0],src[1]);x.lineTo(sp[i][0],sp[i][1]);}x.stroke();
  x.strokeStyle='rgba(95,191,208,.95)';x.lineWidth=1.4;x.shadowColor=GL;x.shadowBlur=10;x.beginPath();sp.forEach((q,i)=>i?x.lineTo(q[0],q[1]):x.moveTo(q[0],q[1]));x.stroke();x.shadowBlur=0;
  const sh=cam([0,-1.75+hg(0,0),0]);const shg=x.createRadialGradient(sh[0],sh[1],0,sh[0],sh[1],sh[3]*.7);shg.addColorStop(0,'rgba(29,42,49,.16)');shg.addColorStop(1,'rgba(29,42,49,0)');
  x.save();x.translate(sh[0],sh[1]);x.scale(1,.26);x.fillStyle=shg;x.beginPath();x.arc(0,0,sh[3]*.7,0,7);x.fill();x.restore();
  const top=cam(DW([0,-.34,0]));x.strokeStyle='rgba(29,42,49,.22)';x.lineWidth=1;x.setLineDash([2,4]);x.beginPath();x.moveTo(top[0],top[1]+4);x.lineTo(sh[0],sh[1]);x.stroke();x.setLineDash([]);
  x.beginPath();x.moveTo(sh[0]-6,sh[1]);x.lineTo(sh[0]+6,sh[1]);x.strokeStyle='rgba(29,42,49,.45)';x.stroke();
  const bb=heroDroneDraw(x,cp,pose,t);
  if(!heroBB)heroBB=bb.slice();for(let i=0;i<4;i++)heroBB[i]=lerp(heroBB[i],bb[i],.12);
  {const pd=22,L=12,[x0,y0,x1,y1]=[heroBB[0]-pd,heroBB[1]-pd,heroBB[2]+pd,heroBB[3]+pd];x.strokeStyle='rgba(29,42,49,.5)';x.lineWidth=1;x.beginPath();
   [[x0,y0,1,1],[x1,y0,-1,1],[x0,y1,1,-1],[x1,y1,-1,-1]].forEach(([a2,b2,sx,sy])=>{x.moveTo(a2,b2+sy*L);x.lineTo(a2,b2);x.lineTo(a2+sx*L,b2);});x.stroke();
   x.font=`10px ${MONO}`;x.fillStyle='rgba(29,42,49,.78)';x.fillText('ORVANE CORTEX',x0,y0-9);const lab='AI TRACKING',tw=x.measureText(lab).width;x.fillText(lab,x1-tw,y0-9);
   x.fillStyle=GL2;x.globalAlpha=.6+.4*Math.sin(t*4);x.beginPath();x.arc(x1-tw-9,y0-12.5,2.6,0,7);x.fill();x.globalAlpha=1;
   x.fillStyle='rgba(125,138,145,1)';x.fillText('AGL '+hAlt.textContent+' M',x0,y0-23);const l2='HDG '+String(Math.round((((pose.yaw-Math.PI)*180/Math.PI)%360+360)%360)).padStart(3,'0')+'°';x.fillText(l2,x1-x.measureText(l2).width,y0-23);}
  if(t-hudT>.12){hudT=t;hAlt.textContent=(100+Math.sin(t*1.3)*.4).toFixed(1);hPts.textContent=Math.round(239000+Math.random()*2000).toLocaleString('en-US');document.getElementById('hAi').textContent=String(3+(Math.floor(t/6)%3));hLine.textContent=String(Math.floor(t*1.45/17*40)%1000).padStart(3,'0');}
});

/* ---------- PROMISE sag ---------- */
const promSec=$('#promise'),sagCv=$('#sagCv'),promRing=$('#promRing');const SJ=Array.from({length:180},(_,i)=>{const r=rng(i+3);return[r()-.5,r()-.5,r()];});
reg(sagCv,(t)=>{const[x,w,h]=cv(sagCv);const p=prog(promSec);const e=eo(clamp((p-.05)/.55));
  const x0=w*.1,x1=w*.9,yb=h*.46,amp=Math.min(h*.1,46)*e;x.font=`10px ${MONO}`;
  // piers
  x.fillStyle='rgba(29,42,49,.08)';[x0,x1].forEach(px=>{x.fillRect(px-7,yb+10,14,h*.3);});
  x.strokeStyle='rgba(29,42,49,.25)';x.setLineDash([2,4]);x.beginPath();x.moveTo(x0-20,yb+10+h*.3);x.lineTo(x1+20,yb+10+h*.3);x.stroke();
  x.beginPath();x.moveTo(x0,yb);x.lineTo(x1,yb);x.strokeStyle='rgba(29,42,49,.35)';x.stroke();x.setLineDash([]);
  // deviation fill
  x.beginPath();x.moveTo(x0,yb);for(let i=0;i<=60;i++){const u=i/60;x.lineTo(lerp(x0,x1,u),yb+amp*Math.sin(Math.PI*u));}x.lineTo(x1,yb);x.closePath();
  const gf=x.createLinearGradient(0,yb,0,yb+amp+1);gf.addColorStop(0,'rgba(143,227,240,0)');gf.addColorStop(1,'rgba(143,227,240,.35)');x.fillStyle=gf;x.fill();
  // measured deck points (3 rows)
  for(let r=0;r<3;r++)for(let i=0;i<SJ.length;i++){const u=i/(SJ.length-1),X=lerp(x0,x1,u);const sag=amp*Math.sin(Math.PI*u);const Y=yb+sag+r*5+SJ[i][r%2]*1.4;
    const hot=sag>amp*.78&&e>.4;x.fillStyle=hot?GL2:`rgba(29,42,49,${.35+.4*SJ[i][2]})`;const s=hot?2:1.3;x.fillRect(X-s/2,Y-s/2,s,s);}
  // scanline
  const sx=x0+((t*.22)%1)*(x1-x0);const sl=x.createLinearGradient(sx-30,0,sx,0);sl.addColorStop(0,'rgba(143,227,240,0)');sl.addColorStop(1,'rgba(143,227,240,.4)');x.fillStyle=sl;x.fillRect(sx-30,yb-40,30,amp+60);
  // delta annotation
  if(e>.05){const mxp=(x0+x1)/2;x.strokeStyle=INK;x.lineWidth=1;x.beginPath();x.moveTo(mxp,yb-24);x.lineTo(mxp,yb+amp);x.moveTo(mxp-4,yb+amp-5);x.lineTo(mxp,yb+amp);x.lineTo(mxp+4,yb+amp-5);x.stroke();
    x.fillStyle=INK;x.fillText(`Δ ${(e*14).toFixed(1)} MM`,mxp+8,yb-14);x.fillStyle='rgba(125,138,145,1)';x.fillText('SAG · MIDSPAN',mxp+8,yb-28);}
  // crack
  const ce=clamp((p-.4)/.2);if(ce>0){const cu=.66,cX=lerp(x0,x1,cu),cY=yb+amp*Math.sin(Math.PI*cu)+5;x.strokeStyle=`rgba(29,42,49,${ce})`;x.beginPath();x.moveTo(cX,cY-4);
    for(let k=1;k<=5;k++)x.lineTo(cX+(k%2?2.5:-2)*ce,cY-4+k*3*ce);x.stroke();
    x.strokeStyle=`rgba(95,191,208,${ce})`;x.beginPath();x.arc(cX,cY+4,16+Math.sin(t*3)*1.5,0,7);x.stroke();
    x.beginPath();x.moveTo(cX+12,cY+16);x.lineTo(cX+34,cY+44);x.lineTo(cX+80,cY+44);x.stroke();x.fillStyle=`rgba(29,42,49,${ce})`;x.fillText('AI FLAG · CRACK 0.3 MM',cX+36,cY+58);}
  x.fillStyle='rgba(125,138,145,1)';x.fillText('SPAN 310 M',x0,yb+h*.3+26);x.fillText('DESIGN PROFILE',x0,yb-10);
  promRing.style.strokeDashoffset=131.95*(1-p);
});

/* ---------- GEAR radar ---------- */
const gearCv=$('#gearCv');const gHits=[];let gA=0;
function gearEnv(th){th=((th%(2*Math.PI))+2*Math.PI)%(2*Math.PI);const r=[];
  if(Math.abs(th-2.45)<.022||Math.abs(th-2.62)<.022||Math.abs(th-2.79)<.022)r.push(.3+.02*Math.sin(th*40));
  if(th>.5&&th<1.5){const R0=.46+.05*Math.sin(th*9);r.push(R0,R0+.055+.02*Math.sin(th*31),R0+.12);if(Math.sin(th*27)>-.2)r.push(R0+.19);}
  if(th>4.3&&th<5.45)r.push(Math.min(.95,.64/Math.cos(th-4.88)));else r.push(.9+.025*Math.sin(th*6)+.012*Math.sin(th*41));
  return r.slice(0,5);}
reg(gearCv,(t,dt)=>{const[x,w,h]=cv(gearCv);const c0=w/2,c1=h/2,Rr=Math.min(w,h)*.46;
  const na=gA+dt*2.3;for(let a=gA;a<na;a+=.026){gearEnv(a).forEach((r,k)=>gHits.push([a,r,t,k]));}gA=na;
  while(gHits.length&&t-gHits[0][2]>2.7)gHits.shift();
  x.strokeStyle='rgba(29,42,49,.12)';x.lineWidth=1;[1,.66,.33].forEach(k=>{x.beginPath();x.arc(c0,c1,Rr*k,0,7);x.stroke();});
  for(let i=0;i<72;i++){const a=i/72*Math.PI*2,m=i%6===0;x.strokeStyle=m?'rgba(29,42,49,.45)':'rgba(29,42,49,.18)';x.beginPath();x.moveTo(c0+Math.cos(a)*Rr*1.04,c1+Math.sin(a)*Rr*1.04);x.lineTo(c0+Math.cos(a)*Rr*(m?1.1:1.07),c1+Math.sin(a)*Rr*(m?1.1:1.07));x.stroke();}
  x.save();x.translate(c0,c1);x.rotate(gA);const wg=x.createLinearGradient(0,0,0,-Rr);
  x.beginPath();x.moveTo(0,0);x.arc(0,0,Rr,-.55,0);x.closePath();x.fillStyle='rgba(143,227,240,.13)';x.fill();
  x.strokeStyle='rgba(95,191,208,.8)';x.beginPath();x.moveTo(0,0);x.lineTo(Rr,0);x.stroke();x.restore();
  for(const[a,r,b,k]of gHits){const al=1-(t-b)/2.7;const X=c0+Math.cos(a)*r*Rr,Y=c1+Math.sin(a)*r*Rr;x.fillStyle=k===0?`rgba(29,42,49,${al*.85})`:`rgba(95,191,208,${al})`;const s=k===0?1.6:2.1;x.fillRect(X-s/2,Y-s/2,s,s);}
  const hr=Rr*.12;const hg2=x.createRadialGradient(c0-hr*.3,c1-hr*.3,0,c0,c1,hr);hg2.addColorStop(0,'#ffffff');hg2.addColorStop(1,'#dfe6e9');
  x.fillStyle=hg2;x.beginPath();x.arc(c0,c1,hr,0,7);x.fill();x.strokeStyle=INK;x.lineWidth=1.2;x.stroke();
  x.beginPath();x.arc(c0,c1,hr*.62,0,7);x.strokeStyle='rgba(29,42,49,.3)';x.lineWidth=1;x.stroke();
  x.strokeStyle=INK;x.lineWidth=2;x.beginPath();x.moveTo(c0-Math.cos(gA)*hr*.5,c1-Math.sin(gA)*hr*.5);x.lineTo(c0+Math.cos(gA)*hr*.5,c1+Math.sin(gA)*hr*.5);x.stroke();
  x.fillStyle=GL;x.beginPath();x.arc(c0,c1,hr*.18,0,7);x.fill();
  x.font=`10px ${MONO}`;x.fillStyle='rgba(125,138,145,1)';x.fillText('905 NM',c0+Rr*.36,c1-6);x.fillText('450 M',c0+Rr*1.0-34,c1+Rr*.08);
});

/* ---------- NUMBERS ---------- */
const numSec=$('#numbers'),arcSvg=$('#arcSvg'),numCv=$('#numCv'),numLabel=$('#numLabel'),stats=$$('.stat'),badges=$$('.num-badge g');
(()=>{let s=`<path id="arcMain" d="M -100 0 A 100 100 0 0 0 100 0" fill="none" stroke="#1d2a31" stroke-opacity=".55" stroke-width=".6" stroke-dasharray="314.16" stroke-dashoffset="314.16" vector-effect="non-scaling-stroke"/><path d="M -86 0 A 86 86 0 0 0 86 0" fill="none" stroke="#9aa3a8" stroke-width=".5" stroke-dasharray="1.5 4" vector-effect="non-scaling-stroke"/>`;
  for(let i=0;i<=36;i++){const a=Math.PI*i/36,c=Math.cos(a),sn=Math.sin(a),m=i%6===0,r2=m?91:95.2;s+=`<line x1="${(-100*c).toFixed(2)}" y1="${(100*sn).toFixed(2)}" x2="${(-r2*c).toFixed(2)}" y2="${(r2*sn).toFixed(2)}" stroke="${m?'#1d2a31':'#9aa3a8'}" stroke-width="${m?.8:.5}" vector-effect="non-scaling-stroke"/>`;}
  [150,90,30].forEach((deg,i)=>{const a=deg*Math.PI/180,c=Math.cos(a),sn=Math.sin(a),px=-sn,py=c;const tip=[102.5*c,102.5*sn],b1=[109*c+3.4*px,109*sn+3.4*py],b2=[109*c-3.4*px,109*sn-3.4*py];
    s+=`<polygon class="mk" data-i="${i}" points="${tip.map(v=>v.toFixed(2))} ${b1.map(v=>v.toFixed(2))} ${b2.map(v=>v.toFixed(2))}" fill="#1d2a31" style="transition:opacity .5s"/>`;});
  s+=`<circle r="2" fill="none" stroke="#8fe3f0" stroke-width=".8" vector-effect="non-scaling-stroke"/>`;arcSvg.innerHTML=s;})();
const arcMain=$('#arcMain'),mks=$$('.mk',arcSvg);let numIdx=-1;const numA=[1,0,0];const NL=['ECHOES','ACCURACY','RANGE'];
function setNum(i){if(i===numIdx)return;numIdx=i;stats.forEach((s,k)=>s.classList.toggle('on',k===i));badges.forEach((g,k)=>g.classList.toggle('on',k===i));mks.forEach((m,k)=>m.style.opacity=k===i?1:.2);numLabel.textContent=NL[i];
  const v=stats[i].querySelector('[data-to]');if(v){v._done=0;v.dataset.count=v.dataset.to;countUp(v);}}
const ACC=Array.from({length:60},()=>{const r=Math.random()*.9,a=Math.random()*7;return[Math.cos(a)*r,Math.sin(a)*r,Math.random()*7];});
reg(numCv,(t,dt)=>{const[x,w,h]=cv(numCv);const u=w/224,c0=w/2,c1=h/2;numA.forEach((v,i)=>numA[i]=lerp(v,i===numIdx?1:0,Math.min(1,dt*5)));
  if(numA[0]>.01){x.globalAlpha=numA[0];const cyc=(t*.7)%1;x.strokeStyle='rgba(29,42,49,.25)';x.setLineDash([2,3]);x.beginPath();x.moveTo(c0,c1);x.lineTo(c0,c1+80*u);x.stroke();x.setLineDash([]);
    const hy=c1+cyc*84*u;x.fillStyle=GL2;x.beginPath();x.arc(c0,hy,2.5,0,7);x.fill();
    [18,30,44,58,74].forEach((d,k)=>{const on=cyc*84>d;x.fillStyle=on?(k?GL2:INK):'rgba(29,42,49,.12)';x.beginPath();x.arc(c0,c1+d*u,on?3:2,0,7);x.fill();
      if(on){x.strokeStyle=`rgba(95,191,208,${.5*(1-(cyc*84-d)/84)})`;x.beginPath();x.arc(c0,c1+d*u,6+(cyc*84-d)*.3,0,7);x.stroke();}});x.globalAlpha=1;}
  if(numA[1]>.01){x.globalAlpha=numA[1];const ty=c1+46*u,rr=26*u;x.strokeStyle='rgba(29,42,49,.5)';x.beginPath();x.arc(c0,ty,rr,0,7);x.stroke();x.setLineDash([2,3]);x.beginPath();x.arc(c0,ty,rr*.5,0,7);x.stroke();x.setLineDash([]);
    x.beginPath();x.moveTo(c0-rr*1.4,ty);x.lineTo(c0+rr*1.4,ty);x.moveTo(c0,ty-rr*1.4);x.lineTo(c0,ty+rr*1.4);x.strokeStyle='rgba(29,42,49,.2)';x.stroke();
    for(const p of ACC){const j=Math.sin(t*2+p[2])*.06;x.fillStyle='rgba(95,191,208,.9)';x.fillRect(c0+(p[0]+j)*rr-1,ty+(p[1]-j)*rr-1,2,2);}
    x.font=`9px ${MONO}`;x.fillStyle=INK;x.fillText('±2 CM',c0+rr+6,ty-rr*.6);x.globalAlpha=1;}
  if(numA[2]>.01){x.globalAlpha=numA[2];for(let k=0;k<4;k++){const ph=((t*.35+k/4)%1);x.strokeStyle=`rgba(95,191,208,${(1-ph)*.8})`;x.beginPath();x.arc(c0,c1,ph*84*u,0,Math.PI);x.stroke();}
    [.25,.5,.75,1].forEach((k,i)=>{x.fillStyle='rgba(125,138,145,1)';x.font=`8px ${MONO}`;x.fillText(Math.round(450*k)+'',c0+3,c1+k*80*u-2);});x.globalAlpha=1;}
});

/* ---------- SOLUTIONS ---------- */
const solSec=$('#solutions'),solCv=$('#solCv'),tabs=$$('.tabs button'),tabLine=$('#tabLine'),solCopy=$$('#solCopy .sol-copy'),solCap=$$('#solCap span'),chipUls=$$('#chips ul'),solIdx=$('#solIdx'),solFlash=$('#solFlash');
const SN=2400;
function buildScene(k){const r=rng(19+k*7),pos=new Float32Array(SN*3),kind=new Uint8Array(SN);let n=0;
  const add=(X,Y,Z,c)=>{if(n>=SN)return;pos[n*3]=X;pos[n*3+1]=Y;pos[n*3+2]=Z;kind[n]=c;n++;};
  const seg=(a,b,c)=>{const t=r();add(lerp(a[0],b[0],t),lerp(a[1],b[1],t),lerp(a[2],b[2],t),c);};
  if(k===0){const rows=7;for(let i=0;i<1500;i++){const rw=i%rows,zc=-1.75+rw*.56,u=r()*5.4-2.7,v=r();const mis=rw===4&&u>.5&&u<1.7;const tl=mis?.95:.5;add(u,.14+v*.34*Math.sin(tl),zc+v*.34*Math.cos(tl),mis?2:1);}
    for(let i=0;i<160;i++){const rw=i%rows,u=-2.6+Math.floor(r()*12)*.47;seg([u,0,-1.75+rw*.56+.05],[u,.15,-1.75+rw*.56+.05],1);}
    while(n<SN){const X=r()*6.4-3.2,Z=r()*4.4-2.2;add(X,.03*Math.sin(X*1.3+Z),Z,0);}}
  else if(k===1){const d=X=>-.16*(1-(X/3)*(X/3));const S=[];
    for(let X=-3;X<3;X+=.5){[-.45,.45].forEach(z=>{S.push([[X,.6+d(X),z],[X+.5,.6+d(X+.5),z]]);if(X>=-2.5&&X<2.5)S.push([[X,1.2+d(X),z],[X+.5,1.2+d(X+.5),z]]);
      if(X>-3)S.push([[X,.6+d(X),z],[X,1.2+d(X),z]]);S.push([[X,.6+d(X),z],[X+.5,1.2+d(X+.5),z]]);});
      S.push([[X,1.2+d(X),-.45],[X,1.2+d(X),.45]]);}
    for(let i=0;i<1000;i++){const s=S[Math.floor(r()*S.length)];const t=r();const X=lerp(s[0][0],s[1][0],t);add(X,lerp(s[0][1],s[1][1],t),lerp(s[0][2],s[1][2],t),Math.abs(X)<.9?2:1);}
    for(let i=0;i<520;i++){const X=r()*6-3;add(X,.6+d(X),r()*.9-.45,Math.abs(X)<.9?2:1);}
    for(let i=0;i<220;i++){const X=(i%2?3:-3)+r()*.3-.15;add(X,r()*.6,r()*.9-.45,1);}
    while(n<SN){const X=r()*6.8-3.4,Z=r()*4.4-2.2;add(X,-.05+.03*Math.sin(X*3+Z*2),Z,0);}}
  else if(k===2){const tanks=[[-2.1,-.9],[-1.05,-.9],[-2.1,.35],[-1.05,.35]];
    for(let i=0;i<900;i++){const tk=tanks[i%4],a=r()*Math.PI*2,top=r()<.25;const rr=top?Math.sqrt(r())*.4:.4;add(tk[0]+Math.cos(a)*rr,top?.8:r()*.8,tk[1]+Math.sin(a)*rr,i%4===1?2:1);}
    for(let i=0;i<420;i++){const X=-.3+r()*3.1,pp=i%3;add(X,.55+pp*.07,-.25+pp*.06,1);}
    for(let i=0;i<120;i++){const X=-.3+Math.floor(r()*7)*.5;seg([X,0,-.3],[X,.7,-.3],1);}
    for(let i=0;i<420;i++){const a=r()*Math.PI*2,rr=Math.sqrt(r())*.75;add(1.75+Math.cos(a)*rr,.62*(1-rr/.75),1.15+Math.sin(a)*rr*.8,2);}
    while(n<SN){const X=r()*6.4-3.2,Z=r()*4.4-2.2;add(X,0,Z,0);}}
  else{const H=(X,Z)=>.45*Math.sin(X*.75+.4)*Math.cos(Z*.6)+.35*Math.exp(-((X-1.2)**2+(Z+.4)**2)/1.2)+.18*Math.sin(X*2.1+Z*1.7)*.4+.25;
    const trees=[];for(let i=0;i<34;i++)trees.push([r()*4-3,r()*3.6-1.8,.2+r()*.18]);
    for(let i=0;i<760;i++){const tr=trees[i%trees.length],a=r()*Math.PI*2,u=r()*2-1,rr=tr[2]*Math.sqrt(1-u*u);add(tr[0]+Math.cos(a)*rr,H(tr[0],tr[1])+.35+u*tr[2]*.8,tr[1]+Math.sin(a)*rr,1);}
    for(let i=0;i<420;i++){const tr=trees[i%trees.length],a=r()*Math.PI*2,rr=Math.sqrt(r())*tr[2]*1.1;const X=tr[0]+Math.cos(a)*rr,Z=tr[1]+Math.sin(a)*rr;add(X,H(X,Z),Z,2);}
    while(n<SN){const X=r()*6.4-3.2,Z=r()*4.4-2.2;add(X,H(X,Z),Z,0);}}
  const col=new Float32Array(SN*3);for(let i=0;i<SN;i++){let c;if(kind[i]===1)c=[29,42,49];else if(kind[i]===2)c=[60,170,190];else{const hh=clamp(pos[i*3+1]/1.1);c=[lerp(176,110,hh),lerp(188,126,hh),lerp(194,134,hh)];}col.set(c,i*3);}
  return{pos,col};}
const SCN=[0,1,2,3].map(buildScene);
const SC={pos:SCN[0].pos.slice(),col:SCN[0].col.slice(),from:null,fcol:null,to:0,start:0};let solK=0,solT=0;
function setSol(k){if(k===solK)return;solK=k;SC.from=SC.pos.slice();SC.fcol=SC.col.slice();SC.to=k;SC.start=solT;
  tabs.forEach((b,i)=>b.setAttribute('aria-selected',i===k));solCopy.forEach((p,i)=>{p.style.opacity=i===k?1:0;p.classList.toggle('on',i===k);});
  solCap.forEach((s,i)=>s.style.opacity=i===k?1:0);chipUls.forEach((u,i)=>u.style.opacity=i===k?1:0);solIdx.textContent='0'+(k+1);moveTabLine();
  solFlash.style.setProperty('--ph',$('#solPanel').offsetHeight+'px');solFlash.classList.remove('go');void solFlash.offsetWidth;solFlash.classList.add('go');}
function moveTabLine(){const b=tabs[solK];tabLine.style.transform=`translateX(${b.offsetLeft}px) scaleX(${b.offsetWidth})`;}
addEventListener('resize',moveTabLine);document.fonts&&document.fonts.ready.then(moveTabLine);setTimeout(moveTabLine,100);
tabs.forEach((b,i)=>b.addEventListener('click',()=>{const top=solSec.offsetTop+(i+.5)/4*(solSec.offsetHeight-VH);scrollTo({top,behavior:RM?'auto':'smooth'});}));
reg(solCv,(t)=>{solT=t;const[x,w,h]=cv(solCv);const cam=camera({cx:w/2,cy:h*.56,f:Math.min(w*1.05,h*1.9),dist:7.5,yaw:-.45+Math.sin(t*.15)*.35,pitch:.62});
  const T=SCN[SC.to];let done=true;
  for(let i=0;i<SN;i++){const i3=i*3;let px,py,pz,cr,cg,cb;
    if(SC.from){const d=(T.pos[i3]+3.2)/6.4*.5;const l=clamp((t-SC.start-d)/.9);if(l<1)done=false;const e=ease(l);const lift=Math.sin(Math.PI*e)*.35;
      px=lerp(SC.from[i3],T.pos[i3],e);py=lerp(SC.from[i3+1],T.pos[i3+1],e)+lift;pz=lerp(SC.from[i3+2],T.pos[i3+2],e);
      cr=lerp(SC.fcol[i3],T.col[i3],e);cg=lerp(SC.fcol[i3+1],T.col[i3+1],e);cb=lerp(SC.fcol[i3+2],T.col[i3+2],e);
      SC.pos[i3]=px;SC.pos[i3+1]=py-lift;SC.pos[i3+2]=pz;SC.col[i3]=cr;SC.col[i3+1]=cg;SC.col[i3+2]=cb;}
    else{px=SC.pos[i3];py=SC.pos[i3+1];pz=SC.pos[i3+2];cr=SC.col[i3];cg=SC.col[i3+1];cb=SC.col[i3+2];}
    const P=cam([px,py,pz]);const hl=cr<80&&cg>150;const s=hl?2.1:1.5;const pulse=hl?.75+.25*Math.sin(t*4+px*2):.9;
    x.fillStyle=`rgba(${cr|0},${cg|0},${cb|0},${pulse})`;x.fillRect(P[0]-s/2,P[1]-s/2,s,s);}
  if(SC.from&&done)SC.from=null;
});

/* ---------- CAPABILITIES ---------- */
const capSec=$('#capabilities'),capCv=$('#capCv'),capSteps=$$('#capSteps li'),capCap=$$('#capCap span'),capStat=$$('#capStat>div'),capTick=$('#capTick');let capK=-1;const capA=[1,0,0];
const CENV=[];{const r=rng(5);[[-.8,-.7,.36,.24],[.38,-.78,.3,.32],[.48,.32,.38,.22],[-.78,.36,.22,.38]].forEach(([x0,y0,ww,hh])=>{for(let i=0;i<80;i++){const s=r()*2*(ww+hh);let px,py;if(s<ww){px=x0+s;py=y0;}else if(s<ww+hh){px=x0+ww;py=y0+s-ww;}else if(s<2*ww+hh){px=x0+ww-(s-ww-hh);py=y0+hh;}else{px=x0;py=y0+hh-(s-2*ww-hh);}CENV.push([px,py,1]);}});
  [[-.2,.62],[.05,.7],[.85,-.1],[-.55,-.05],[.15,-.35]].forEach(([cx0,cy0])=>{for(let i=0;i<40;i++){const a=r()*7,rr=.05+r()*.06;CENV.push([cx0+Math.cos(a)*rr,cy0+Math.sin(a)*rr,2]);}});
  for(let i=0;i<520;i++){const a=r()*7,rr=Math.sqrt(r())*.98;CENV.push([Math.cos(a)*rr,Math.sin(a)*rr,0]);}CENV.forEach(p=>p.push(Math.atan2(p[1],p[0])));}
function setCap(k){if(k===capK)return;capK=k;capSteps.forEach((l,i)=>l.classList.toggle('on',i===k));capCap.forEach((s,i)=>s.style.opacity=i===k?1:0);
  capStat.forEach((s,i)=>{s.style.opacity=i===k?1:0;s.style.transform=i===k?'none':`translateY(${i<k?-14:14}px)`;});
  const li=capSteps[k];if(capTick&&li)capTick.style.transform=`translateY(${li.offsetTop+li.offsetHeight/2}px)`;}
function topDrone(x,X,Y,s,fold,t,a){x.save();x.translate(X,Y);x.globalAlpha*=a;x.strokeStyle=INK;x.lineWidth=1.4;
  const ang=[[1,-1],[1,1],[-1,1],[-1,-1]];ang.forEach(([sx,sy],i)=>{const base=Math.atan2(sy,sx);const tgt=sx>0?0:Math.PI;const an=lerp(base,base+(tgt-base)*.0+((sx>0?(sy>0?.75:-.75):(sy>0?-.75:.75)))*0,0)+ (sx>0?(sy<0?1:-1):(sy<0?-1:1))*fold*.62;
    const ax=Math.cos(an)*s,ay=Math.sin(an)*s;x.beginPath();x.moveTo(Math.cos(an)*s*.25,Math.sin(an)*s*.25);x.lineTo(ax,ay);x.stroke();
    x.beginPath();x.arc(ax,ay,s*.42,0,7);x.fillStyle=`rgba(143,227,240,${.15*(1-fold)})`;x.fill();x.strokeStyle='rgba(29,42,49,.3)';x.lineWidth=1;x.stroke();x.lineWidth=1.4;x.strokeStyle=INK;
    const b=t*14+i;x.beginPath();x.moveTo(ax+Math.cos(b)*s*.38,ay+Math.sin(b)*s*.38);x.lineTo(ax-Math.cos(b)*s*.38,ay-Math.sin(b)*s*.38);x.stroke();});
  x.fillStyle='#f7fafb';x.beginPath();x.roundRect?x.roundRect(-s*.32,-s*.22,s*.64,s*.44,s*.14):x.rect(-s*.32,-s*.22,s*.64,s*.44);x.fill();x.stroke();
  x.fillStyle=GL2;x.beginPath();x.arc(s*.2,0,s*.05,0,7);x.fill();x.restore();}
reg(capCv,(t,dt)=>{const[x,w,h]=cv(capCv);capA.forEach((v,i)=>capA[i]=lerp(v,i===capK?1:0,Math.min(1,dt*4)));const c0=w/2,c1=h/2,Rr=Math.min(w,h)*.38;
  if(capA[0]>.01){x.globalAlpha=capA[0];const A=(t*1.4)%(Math.PI*2);
    for(const p of CENV){let d=A-p[3];d=((d%(Math.PI*2))+Math.PI*2)%(Math.PI*2);const al=Math.max(.06,1-d/(Math.PI*2)*1.15);const X=c0+p[0]*Rr,Y=c1+p[1]*Rr;
      x.fillStyle=p[2]===1?`rgba(29,42,49,${al})`:p[2]===2?`rgba(95,191,208,${al})`:`rgba(29,42,49,${al*.35})`;const s=p[2]?1.8:1.2;x.fillRect(X-s/2,Y-s/2,s,s);}
    x.save();x.translate(c0,c1);x.rotate(A);x.beginPath();x.moveTo(0,0);x.arc(0,0,Rr,-.5,0);x.closePath();x.fillStyle='rgba(143,227,240,.18)';x.fill();x.strokeStyle='rgba(95,191,208,.9)';x.beginPath();x.moveTo(0,0);x.lineTo(Rr,0);x.stroke();x.restore();
    x.strokeStyle='rgba(29,42,49,.15)';x.beginPath();x.arc(c0,c1,Rr,0,7);x.stroke();topDrone(x,c0,c1,Rr*.13,0,t,1);x.globalAlpha=1;}
  if(capA[1]>.01){x.globalAlpha=capA[1];const O=[w*.2,h*.72],D=[w*.8,h*.3];const band=Math.floor(t/3)%2;
    const ctrl=[[w*.35,h*.15],[w*.62,h*.88]];
    ctrl.forEach((c,i)=>{const act=i===band;x.beginPath();x.moveTo(O[0],O[1]);if(!act){for(let k=0;k<=40;k++){const u=k/40;const bx=(1-u)*(1-u)*O[0]+2*(1-u)*u*c[0]+u*u*D[0],by=(1-u)*(1-u)*O[1]+2*(1-u)*u*c[1]+u*u*D[1];const j=Math.sin(u*60+t*20)*Math.exp(-((u-.5)**2)/.01)*8;x.lineTo(bx,by+j);}}else x.quadraticCurveTo(c[0],c[1],D[0],D[1]);
      x.strokeStyle=act?'rgba(29,42,49,.7)':'rgba(29,42,49,.18)';x.setLineDash(act?[]:[3,4]);x.lineWidth=act?1.3:1;x.stroke();x.setLineDash([]);
      const mid=[.25*O[0]+.5*c[0]+.25*D[0],.25*O[1]+.5*c[1]+.25*D[1]];x.font=`10px ${MONO}`;x.fillStyle=act?INK:'rgba(125,138,145,1)';x.fillText(i?'5.8 GHZ':'2.4 GHZ',mid[0]+8,mid[1]+(i?14:-6));
      if(!act){x.fillStyle='rgba(255,140,120,.18)';x.beginPath();x.arc(mid[0],mid[1],14+Math.sin(t*6)*3,0,7);x.fill();}
      if(act){const c2=ctrl[i];for(let k=0;k<7;k++){const u=1-((t*.45+k/7)%1);const bx=(1-u)*(1-u)*O[0]+2*(1-u)*u*c2[0]+u*u*D[0],by=(1-u)*(1-u)*O[1]+2*(1-u)*u*c2[1]+u*u*D[1];
        for(let q=0;q<5;q++){x.fillStyle=GL2;x.fillRect(bx+(q%3-1)*3,by+(q>2?3:-1),2,2);}}}});
    x.fillStyle='#fff';x.strokeStyle=INK;x.lineWidth=1.2;x.beginPath();x.rect(O[0]-18,O[1]-12,36,24);x.fill();x.stroke();x.fillStyle=GL2;x.fillRect(O[0]-12,O[1]-7,24,14);
    topDrone(x,D[0],D[1],Math.min(w,h)*.045,0,t,1);
    x.strokeStyle='rgba(29,42,49,.25)';x.setLineDash([2,3]);x.beginPath();x.moveTo(O[0],h*.9);x.lineTo(D[0],h*.9);x.stroke();x.setLineDash([]);x.fillStyle=INK;x.font=`10px ${MONO}`;x.fillText('7 KM LINK',(O[0]+D[0])/2-26,h*.9-6);x.globalAlpha=1;}
  if(capA[2]>.01){x.globalAlpha=capA[2];const fold=ease(clamp((Math.sin(t*.9)+1)/2*1.3-.15));const s=Math.min(w,h)*.16;topDrone(x,c0,c1,s,fold,t*(1-fold),1);
    const L=Math.round(lerp(96,42,fold)),W=Math.round(lerp(96,18,fold));const bw=lerp(s*2.8,s*1.9,fold),bh=lerp(s*2.8,s*1.0,fold);
    x.strokeStyle='rgba(29,42,49,.5)';x.lineWidth=1;x.setLineDash([3,3]);x.strokeRect(c0-bw/2,c1-bh/2,bw,bh);x.setLineDash([]);
    x.beginPath();x.moveTo(c0-bw/2,c1+bh/2+14);x.lineTo(c0+bw/2,c1+bh/2+14);x.moveTo(c0-bw/2,c1+bh/2+10);x.lineTo(c0-bw/2,c1+bh/2+18);x.moveTo(c0+bw/2,c1+bh/2+10);x.lineTo(c0+bw/2,c1+bh/2+18);
    x.moveTo(c0+bw/2+14,c1-bh/2);x.lineTo(c0+bw/2+14,c1+bh/2);x.stroke();x.font=`10px ${MONO}`;x.fillStyle=INK;x.fillText(L+' CM',c0-14,c1+bh/2+30);x.save();x.translate(c0+bw/2+26,c1+10);x.rotate(-Math.PI/2);x.fillText(W+' CM',0,0);x.restore();
    x.fillStyle='rgba(125,138,145,1)';x.fillText(fold>.9?'PACKED':fold<.1?'DEPLOYED':'FOLDING',16,h-40);x.globalAlpha=1;}
});

/* ---------- CONTROLLER ---------- */
const ctlSec=$('#controller'),ctlCv=$('#ctlCv'),compass=$('#compass');
(()=>{let s='';[[96,26,.16],[64,17.3,.1],[32,8.7,.08]].forEach(([a,b,o])=>s+=`<ellipse rx="${a}" ry="${b}" fill="none" stroke="#1d2a31" stroke-opacity="${o}" vector-effect="non-scaling-stroke"/>`);
  for(let i=0;i<72;i++){const a=i/72*Math.PI*2,m=i%6===0,r1=m?.9:.94;s+=`<line x1="${(Math.cos(a)*96*r1).toFixed(2)}" y1="${(Math.sin(a)*26*r1).toFixed(2)}" x2="${(Math.cos(a)*96).toFixed(2)}" y2="${(Math.sin(a)*26).toFixed(2)}" stroke="#1d2a31" stroke-opacity="${m?.4:.18}" vector-effect="non-scaling-stroke"/>`;}
  s+=`<line id="needle" x1="0" y1="0" x2="96" y2="0" stroke="#5fbfd0" stroke-opacity=".85" vector-effect="non-scaling-stroke"/><circle r="1.1" fill="#1d2a31" fill-opacity=".5"/>`;compass.innerHTML=s;})();
const needle=$('#needle');
const ctl={x:0,y:1.2,z:0,yaw:0,vx:0,vy:0,vz:0,tilt:0,roll:0,spin:1,awake:true,lights:true,scan:true,bat:98};
const sticks={L:{x:0,y:0},R:{x:0,y:0}},keys={},trig={q:0,e:0};
const GRID=[],GN=19;for(let i=0;i<GN;i++)for(let j=0;j<GN;j++)GRID.push({x:-4.5+i*.5,z:-4.5+j*.5,m:0});let mapped=0,pts=0;
const tEls={};$$('[data-t]').forEach(e=>(tEls[e.dataset.t]=tEls[e.dataset.t]||[]).push(e));const bars={};$$('[data-bar]').forEach(e=>bars[e.dataset.bar]=e);
function setT(k,v){(tEls[k]||[]).forEach(e=>e.textContent=v);}
function bindStick(el,S){const knob=$('.knob',el);let id=null;
  const upd=e=>{const r=el.getBoundingClientRect();const rad=r.width*.33;let dx=e.clientX-(r.left+r.width/2),dy=e.clientY-(r.top+r.height/2);const d=Math.hypot(dx,dy);if(d>rad){dx*=rad/d;dy*=rad/d;}
    S.x=dx/rad;S.y=-dy/rad;knob.style.transition='none';knob.style.transform=`translate(${dx}px,${dy}px)`;};
  el.addEventListener('pointerdown',e=>{id=e.pointerId;el.setPointerCapture(id);el.classList.add('drag');upd(e);e.preventDefault();});
  el.addEventListener('pointermove',e=>{if(e.pointerId===id)upd(e);});
  const end=e=>{if(e.pointerId!==id)return;id=null;S.x=0;S.y=0;el.classList.remove('drag');knob.style.transition='transform .35s cubic-bezier(.34,1.56,.64,1)';knob.style.transform='';};
  el.addEventListener('pointerup',end);el.addEventListener('pointercancel',end);}
bindStick($('#stickL'),sticks.L);bindStick($('#stickR'),sticks.R);
$$('[data-trig]').forEach(b=>{const k=b.dataset.trig;const on=v=>{trig[k]=v;b.classList.toggle('on',!!v);};b.addEventListener('pointerdown',e=>{b.setPointerCapture(e.pointerId);on(1);});b.addEventListener('pointerup',()=>on(0));b.addEventListener('pointercancel',()=>on(0));});
$$('[data-act]').forEach(b=>b.addEventListener('click',()=>{const k=b.dataset.act;ctl[k]=!ctl[k];b.setAttribute('aria-pressed',ctl[k]);}));
const KS=new Set(['w','a','s','d','q','e','arrowup','arrowdown','arrowleft','arrowright']);
function ctlActive(){const r=ctlSec.getBoundingClientRect();return r.top<VH*.3&&r.bottom>VH*.7;}
addEventListener('keydown',e=>{const k=e.key.toLowerCase();if(!ctlActive()||e.target.closest('input,textarea,select,dialog'))return;
  if(k==='r'){Object.assign(ctl,{x:0,y:1.2,z:0,yaw:0,vx:0,vy:0,vz:0});GRID.forEach(g=>g.m=0);return;}
  if(KS.has(k)){keys[k]=1;if(k.startsWith('arrow'))e.preventDefault();if(k==='q'||k==='e')$(`[data-trig="${k}"]`).classList.add('on');}});
addEventListener('keyup',e=>{const k=e.key.toLowerCase();keys[k]=0;if(k==='q'||k==='e')$(`[data-trig="${k}"]`).classList.remove('on');});
let telT=0;
reg(ctlCv,(t,dt)=>{const[x,w,h]=cv(ctlCv);
  const lx=clamp(sticks.L.x+(keys.d||0)-(keys.a||0),-1,1),ly=clamp(sticks.L.y+(keys.w||0)-(keys.s||0),-1,1);
  const rx=clamp(sticks.R.x+(keys.arrowright||0)-(keys.arrowleft||0),-1,1),ry=clamp(sticks.R.y+(keys.arrowup||0)-(keys.arrowdown||0),-1,1);
  const boost=(keys.e||trig.e)?1.9:(keys.q||trig.q)?.45:1;
  ctl.spin=lerp(ctl.spin,ctl.awake?1:0,Math.min(1,dt*2));
  if(ctl.awake){ctl.yaw+=lx*1.7*dt*boost;const fwd=ry*2.2*boost,side=rx*2.2*boost;
    const tvx=Math.sin(ctl.yaw)*fwd+Math.cos(ctl.yaw)*side,tvz=Math.cos(ctl.yaw)*fwd-Math.sin(ctl.yaw)*side;
    const k=Math.min(1,dt*2.5);ctl.vx=lerp(ctl.vx,tvx,k);ctl.vz=lerp(ctl.vz,tvz,k);ctl.vy=lerp(ctl.vy,ly*1.6,Math.min(1,dt*3));
    ctl.tilt=lerp(ctl.tilt,ry*.32*Math.min(boost,1.3),Math.min(1,dt*4));ctl.roll=lerp(ctl.roll,-rx*.32*Math.min(boost,1.3),Math.min(1,dt*4));}
  else{ctl.vx*=.92;ctl.vz*=.92;ctl.vy=lerp(ctl.vy,-1.4,Math.min(1,dt*2));ctl.tilt=lerp(ctl.tilt,0,Math.min(1,dt*4));ctl.roll=lerp(ctl.roll,0,Math.min(1,dt*4));}
  ctl.x=clamp(ctl.x+ctl.vx*dt,-4.2,4.2);ctl.z=clamp(ctl.z+ctl.vz*dt,-4.2,4.2);ctl.y=clamp(ctl.y+ctl.vy*dt,.34,3.2);
  if(ctl.awake&&ctl.scan&&ctl.y>.4){const rr=.35+ctl.y*.3;let nm=0;for(const g of GRID){if(!g.m&&Math.hypot(g.x-ctl.x,g.z-ctl.z)<rr){g.m=t;nm++;}}mapped+=nm;pts+=Math.round(240000*dt);}
  const cam=camera({cx:w/2,cy:h*.5,f:Math.min(w*1.05,h*1.7),dist:10,yaw:-.55+Math.sin(t*.1)*.08,pitch:.48});
  for(const g of GRID){const P=cam([g.x,0,g.z]);if(g.m){const age=clamp((t-g.m)/.8);x.fillStyle=`rgba(95,191,208,${.4+.5*age})`;const s=2+(1-age)*4;x.fillRect(P[0]-s/2,P[1]-s/2,s,s);}else{x.fillStyle='rgba(29,42,49,.2)';x.fillRect(P[0]-.75,P[1]-.75,1.5,1.5);}}
  const sh=cam([ctl.x,0,ctl.z]);const sk=1/(1+ctl.y*.4);x.fillStyle=`rgba(29,42,49,${.12*sk})`;x.beginPath();x.ellipse(sh[0],sh[1],sh[3]*.85*sk,sh[3]*.3*sk,0,0,7);x.fill();
  if(ctl.awake&&ctl.scan&&ctl.y>.4){const rr=.35+ctl.y*.3;const S=cam([ctl.x+Math.sin(ctl.yaw)*.17,ctl.y-.17,ctl.z+Math.cos(ctl.yaw)*.17]);x.beginPath();
    for(let i=0;i<=32;i++){const a=i/32*Math.PI*2;const P=cam([ctl.x+Math.cos(a)*rr,0,ctl.z+Math.sin(a)*rr]);i?x.lineTo(P[0],P[1]):x.moveTo(P[0],P[1]);}x.closePath();
    x.fillStyle='rgba(143,227,240,.14)';x.fill();x.strokeStyle='rgba(95,191,208,.55)';x.stroke();
    x.strokeStyle='rgba(95,191,208,.25)';x.beginPath();for(let i=0;i<8;i++){const a=i/8*Math.PI*2+t;const P=cam([ctl.x+Math.cos(a)*rr,0,ctl.z+Math.sin(a)*rr]);x.moveTo(S[0],S[1]);x.lineTo(P[0],P[1]);}x.stroke();}
  drawDrone(x,cam,{pos:[ctl.x,ctl.y+(ctl.awake?Math.sin(t*2)*.03:0),ctl.z],yaw:ctl.yaw,tilt:ctl.tilt,roll:ctl.roll,t,spin:ctl.spin,lights:ctl.lights,s:1.1});
  const hd=((ctl.yaw*180/Math.PI)%360+360)%360;needle.setAttribute('x2',(Math.sin(ctl.yaw)*96).toFixed(2));needle.setAttribute('y2',(Math.cos(ctl.yaw)*26).toFixed(2));
  if(t-telT>.08){telT=t;const sp=Math.hypot(ctl.vx,ctl.vz)*4.5;const pd=Math.round(ctl.tilt*180/Math.PI),rd=Math.round(-ctl.roll*180/Math.PI);const mp=Math.round(mapped/GRID.length*100);
    setT('hdg',String(Math.round(hd)).padStart(3,'0')+'°');setT('pit',(pd<0?'-':' ')+String(Math.abs(pd)).padStart(2,'0')+'°');setT('rol',(rd<0?'-':' ')+String(Math.abs(rd)).padStart(2,'0')+'°');
    setT('spd',sp.toFixed(1));setT('alt',(ctl.y*10).toFixed(1));setT('map',mp+'%');setT('pts',pts>999999?(pts/1e6).toFixed(1)+'M':pts>999?Math.round(pts/1000)+'K':pts);
    ctl.bat=Math.max(12,ctl.bat-(ctl.awake?.002:0));setT('bat',Math.round(ctl.bat));
    if(bars.hdg){bars.hdg.style.transform=`scaleX(${hd/360})`;bars.pit.style.transform=`scaleX(${Math.abs(pd)/20})`;bars.rol.style.transform=`scaleX(${Math.abs(rd)/20})`;bars.spd.style.transform=`scaleX(${clamp(sp/20)})`;bars.map.style.transform=`scaleX(${mp/100})`;}}
});

/* ---------- SOFTWARE pipeline ---------- */
const pipe=$('#pipe'),pTime=$('#pipeTime'),pFill=$('#pipeFill'),pDot=$('#pipeDot'),pSt=$$('#pStages li'),pFiles=$$('#files span'),pState=$('#pipeState');let pipeT0=null;
const PS=['Offloading flight data','Removing noise and drift','AI classifying returns','AI flagging defects and change','Delivered to your team'];
reg(pipe,(t)=>{if(pipeT0===null)pipeT0=t;const cyc=(t-pipeT0)%8,p=ease(clamp(cyc/6));const mins=p*18.7;
  pTime.innerHTML=String(Math.floor(mins)).padStart(2,'0')+':'+String(Math.floor((mins%1)*60)).padStart(2,'0')+'<small>min</small>';
  pFill.style.transform=`scaleX(${p})`;pDot.style.left=(p*100)+'%';const si=Math.min(4,Math.floor(p*4.999));pSt.forEach((l,i)=>l.classList.toggle('on',i<=si&&p>0));pState.textContent=p>=1?PS[4]:PS[si];
  pFiles.forEach((f,i)=>f.classList.toggle('on',p>.55+i*.12));});

/* ---------- TERRAIN ---------- */
const terSec=$('#terrain'),terCv=$('#terCv'),terOver=$('#terOver'),terClip=$('#terClip'),terFoot=$('#terFoot'),terLine=$('#terLine'),hsWrap=$('#hsWrap');
const TC=100,TR=44,TH=new Float32Array(TC*TR);const PK=[[.5,.22,1,.11],[.27,.42,.72,.1],[.73,.4,.82,.1],[.6,.72,.5,.09],[.16,.7,.45,.1],[.88,.18,.55,.09],[.38,.12,.6,.08]];
for(let j=0;j<TR;j++)for(let i=0;i<TC;i++){const u=i/(TC-1),v=j/(TR-1);let hh=0;for(const p of PK){const d2=((u-p[0])**2+((v-p[1])*.85)**2)/(p[3]*p[3]);hh+=p[2]*Math.exp(-d2);}
  hh+=.05*Math.sin(u*31+v*7)*Math.sin(v*17)+.04*Math.abs(Math.sin(u*57-v*21))+.02*Math.sin(u*120);hh*=Math.pow(Math.sin(Math.PI*u),.35);TH[j*TC+i]=Math.max(0,hh);}
function tPt(i,j,w,h){const u=i/(TC-1),v=j/(TR-1),k=.6+.4*v;return[w/2+(u-.5)*w*1.0*k,lerp(h*.4,h*.95,Math.pow(v,1.08))-TH[j*TC+i]*h*.3*k];}
const HS=[{n:'Summit N-07',u:.5,v:.22,d:[['Height','2,891 m'],['Gradient','36.8°'],['Open fracture','2.3 mm',1]]},{n:'Crest R-12',u:.73,v:.4,d:[['Height','2,648 m'],['Gradient','29.5°'],['Ground drift','3.6 mm/yr',1]]},
  {n:'Col S-03',u:.39,v:.33,d:[['Height','2,402 m'],['Gradient','18.2°'],['Loose rock','Stable']]},{n:'Buttress E-21',u:.27,v:.42,d:[['Height','2,733 m'],['Gradient','47.1°'],['Open fracture','4.0 mm',1]]}];
HS.forEach(hs=>{let bi=Math.round(hs.u*(TC-1)),bj=Math.round(hs.v*(TR-1));hs.i=bi;hs.j=bj;
  const el=document.createElement('div');el.className='hs';el.innerHTML=`<span class="stem"></span><span class="halo"></span><button type="button" aria-label="${hs.n} readings"><svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"><path d="M5 12h14M12 5v14"/></svg></button><div class="card"><p class="mono">${hs.n}</p><p class="mono" style="margin-top:4px;color:${hs.d.some(d=>d[2])?'#0f7f92':'var(--haze)'}">${hs.d.some(d=>d[2])?'● AI flagged':'○ AI clear'}</p><dl>${hs.d.map(d=>`<div><dt>${d[0]}</dt><dd${d[2]?' class="warn"':''}>${d[1]}</dd></div>`).join('')}</dl></div>`;hsWrap.appendChild(el);hs.el=el;});
let terP=0;
reg(terCv,(t)=>{const[x,w,h]=cv(terCv);const p=terP;const rev=clamp((p-.1)/.58)*TR;
  const bg=x.createLinearGradient(0,0,0,h);bg.addColorStop(0,'#cfe3eb');bg.addColorStop(.42,'#dcebf0');bg.addColorStop(.7,'#e2eef2');bg.addColorStop(1,'#e8f1f4');x.fillStyle=bg;x.fillRect(0,0,w,h);
  const nr=Math.min(TR,Math.ceil(rev));
  for(let j=0;j<nr;j++){const part=clamp(rev-j);const v=j/(TR-1);const imax=Math.floor((TC-1)*(j===nr-1?part:1));if(imax<1)continue;
    x.beginPath();let P=tPt(0,j,w,h);x.moveTo(P[0],P[1]);for(let i=1;i<=imax;i++){P=tPt(i,j,w,h);x.lineTo(P[0],P[1]);}
    const last=P;x.lineTo(last[0],h);x.lineTo(tPt(0,j,w,h)[0],h);x.closePath();x.fillStyle=bg;x.fill();
    x.beginPath();P=tPt(0,j,w,h);x.moveTo(P[0],P[1]);for(let i=1;i<=imax;i++){P=tPt(i,j,w,h);x.lineTo(P[0],P[1]);}
    const head=j===nr-1&&rev<TR;x.strokeStyle=head?GL2:`rgba(29,42,49,${.22+.55*v})`;x.lineWidth=head?1.8:1;if(head){x.shadowColor=GL;x.shadowBlur=10;}x.stroke();x.shadowBlur=0;}
  const g2=x.createRadialGradient(w/2,0,0,w/2,0,w*.8);g2.addColorStop(0,'rgba(255,255,255,.35)');g2.addColorStop(1,'rgba(255,255,255,0)');x.fillStyle=g2;x.fillRect(0,0,w,h*.7);
  HS.forEach(hs=>{const P=tPt(hs.i,hs.j,w,h);hs.el.style.transform=`translate(${P[0]}px,${P[1]}px)`;hs.el.dataset.side=P[0]>w*.62?'left':'right';hs.el.classList.toggle('show',rev>hs.j+1.5);});
  terLine.textContent=String(Math.floor(rev)).padStart(3,'0');
  // overlay: drone + lasers
  const[o,ow,oh]=cv(terOver);const dX=ow/2+Math.sin(t*.35)*ow*.16,dY=oh*.3+Math.sin(t*1.2)*4;
  if(rev<TR&&rev>0){const j=Math.min(TR-1,Math.floor(rev));o.strokeStyle='rgba(95,191,208,.28)';o.lineWidth=.8;o.beginPath();
    const ic=Math.round(((dX-ow/2)/(ow*(.6+.4*j/(TR-1)))+.5)*(TC-1));for(let k=-18;k<=18;k+=3){const i=clamp(ic+k,0,TC-1);const P=tPt(i,j,ow,oh);o.moveTo(dX,dY+8);o.lineTo(P[0],P[1]);}o.stroke();}
  const ocam=camera({cx:dX,cy:dY,f:Math.min(ow,oh)*.5,dist:7,yaw:.4,pitch:.45});drawDrone(o,ocam,{pos:[0,0,0],yaw:Math.sin(t*.35)*.3,tilt:.05,roll:Math.cos(t*.35)*.08,t,spin:1,lights:true});
});

/* ---------- FOOTER viewer ---------- */
const viewer=$('#viewer'),viewCv=$('#viewCv'),dragHint=$('#dragHint');let vYaw=.6,vVel=.25,vDrag=null;
viewer.addEventListener('pointerdown',e=>{vDrag={x:e.clientX,t:performance.now()};viewer.setPointerCapture(e.pointerId);dragHint.style.opacity=0;});
viewer.addEventListener('pointermove',e=>{if(!vDrag)return;const dx=e.clientX-vDrag.x;vDrag.x=e.clientX;vYaw+=dx*.01;vVel=dx*.6;});
const vEnd=()=>{vDrag=null;};viewer.addEventListener('pointerup',vEnd);viewer.addEventListener('pointercancel',vEnd);
viewer.addEventListener('keydown',e=>{if(e.key==='ArrowLeft'){vVel=-2.2;e.preventDefault();}if(e.key==='ArrowRight'){vVel=2.2;e.preventDefault();}});
reg(viewCv,(t,dt)=>{const[x,w,h]=cv(viewCv);if(!vDrag){vYaw+=vVel*dt;vVel=lerp(vVel,.25,Math.min(1,dt*1.5));}
  const cam=camera({cx:w/2,cy:h*.52,f:Math.min(w*.9,h*2.2),dist:6,yaw:0,pitch:.32});
  const sh=cam([0,-.62,0]);x.fillStyle='rgba(29,42,49,.08)';x.beginPath();x.ellipse(sh[0],sh[1],sh[3]*1.1,sh[3]*.24,0,0,7);x.fill();
  x.strokeStyle='rgba(29,42,49,.12)';x.setLineDash([2,4]);x.beginPath();x.ellipse(sh[0],sh[1],sh[3]*1.5,sh[3]*.36,0,0,7);x.stroke();x.setLineDash([]);
  for(let i=0;i<36;i++){const a=i/36*Math.PI*2+vYaw;const P=cam([Math.cos(a)*1.5,-.62,Math.sin(a)*1.5]);x.fillStyle=i%9===0?INK:'rgba(29,42,49,.25)';x.fillRect(P[0]-1,P[1]-1,2,2);}
  drawDrone(x,cam,{pos:[0,Math.sin(t*1.1)*.05,0],yaw:vYaw,tilt:.05,roll:0,t,spin:1,lights:true,s:1.25});
  x.font=`10px ${MONO}`;x.fillStyle='rgba(125,138,145,1)';x.fillText('HDG '+String(Math.round(((vYaw*180/Math.PI)%360+360)%360)).padStart(3,'0')+'°',w/2-28,h*.92);
});

/* ---------- DIALOG ---------- */
const dlg=$('#dlg'),form=$('#form'),ok=$('#ok'),sendBtn=$('#sendBtn');
$$('[data-book]').forEach(b=>b.addEventListener('click',()=>{setMenu(false);form.style.display='';ok.classList.remove('show');$('#okRing').style.strokeDashoffset=170;
  const tp=b.dataset.book;form.topic.value=tp&&tp!==''?tp:'survey';dlg.showModal();setTimeout(()=>form.name.focus(),50);}));
dlg.addEventListener('click',e=>{if(e.target===dlg||e.target.closest('[data-close]'))dlg.close();});
form.addEventListener('submit',e=>{e.preventDefault();let bad=false;const err=(n,m)=>{$(`[data-err="${n}"]`).textContent=m;form[n].setAttribute('aria-invalid',!!m);if(m)bad=true;};
  err('name',form.name.value.trim()?'':'Please add your name.');err('email',/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email.value.trim())?'':'Please use a valid work email.');
  if(bad){(form.querySelector('[aria-invalid=true]')||form.name).focus();return;}if(form.website.value)return;
  sendBtn.classList.add('busy');sendBtn.disabled=true;setTimeout(()=>{sendBtn.classList.remove('busy');sendBtn.disabled=false;form.style.display='none';ok.classList.add('show');
    $('#okTxt').textContent=`Thanks, ${form.name.value.trim().split(' ')[0]}. We'll review the site and reply to ${form.email.value.trim()} within one business day.`;requestAnimationFrame(()=>$('#okRing').style.strokeDashoffset=0);form.reset();},1100);});
$$('.inp',form).forEach(i=>i.addEventListener('input',()=>{i.removeAttribute('aria-invalid');const e=$(`[data-err="${i.name}"]`);if(e)e.textContent='';}));

/* ---------- scroll tick ---------- */
function scrollTick(){
  const st=scrollY,max=document.documentElement.scrollHeight-VH;ringArc.style.strokeDashoffset=128.8*(1-clamp(st/Math.max(1,max)));
  let ci=0;navSecs.forEach((s,i)=>{if(s.getBoundingClientRect().top<VH*.5)ci=i;});reel.style.transform=`translateY(${-34*ci}px)`;
  $$('[data-words]').forEach(el=>{let p;if(el._r){p=clamp((prog(el._sec)-el._r[0])/(el._r[1]-el._r[0]));}else{const r=el.getBoundingClientRect();p=clamp((VH*.9-r.top)/(VH*.55));}
    const n=Math.round(p*el._w.length);if(el._n!==n){el._n=n;el._w.forEach((w,i)=>w.classList.toggle('on',i<n));}});
  $$('[data-letters]').forEach(el=>{const p=prog(el._sec);const lit=clamp(p*2.2)*el._l.length;el._l.forEach((s,i)=>{const k=clamp(lit-i+1);s.style.color=`rgb(${Math.round(lerp(198,29,k))},${Math.round(lerp(205,42,k))},${Math.round(lerp(208,49,k))})`;});});
  const np=prog(numSec);arcMain.style.strokeDashoffset=314.16*(1-clamp(np*1.15));setNum(Math.min(2,Math.floor(np*3)));
  const sp=prog(solSec);setSol(Math.min(3,Math.floor(sp*4)));const sub=(sp*4)%1;const ci2=Math.min(3,Math.floor(sub*4));$$('li',chipUls[solK]).forEach((l,i)=>l.classList.toggle('on',i===ci2));
  setCap(Math.min(2,Math.floor(prog(capSec)*3)));
  terP=prog(terSec);const c=eo(clamp(terP/.22));terClip.style.clipPath=`inset(${lerp(58,14,c)}% ${lerp(6,3,c)}% ${lerp(6,4,c)}% ${lerp(6,3,c)}% round 24px)`;terFoot.style.opacity=clamp((terP-.2)/.15);
}
let last=performance.now();
function loop(now){const dt=Math.min(.05,(now-last)/1000);last=now;const t=now/1000;
  if(FINE){cx=lerp(cx,tx,.22);cy=lerp(cy,ty,.22);cur.style.transform=`translate(${cx}px,${cy}px)`;}
  scrollTick();for(const r of R)if(vis.get(r.el))r.fn(t,dt);requestAnimationFrame(loop);}
setSol(0);setCap(0);setNum(0);requestAnimationFrame(loop);
})();
</script>
</body>
</html>
```

