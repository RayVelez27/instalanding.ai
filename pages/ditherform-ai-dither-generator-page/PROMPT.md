INSTALANDING.AI · Ditherform AI Dither Generator Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Ditherform AI Dither Generator Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/ditherform-ai-dither-generator-page

ditherform-ai-dither.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Ditherform AI Dither Generator Page
  slug     ditherform-ai-dither-generator-page
  prompt   https://instalanding.ai/p/ditherform-ai-dither-generator-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/ditherform-ai-dither-generator-page
  license  Fictional brand ("Ditherform"); every customer, logo, date and changelog entry is invented. Replace names
           and copy before shipping. Every picture is a live raymarched shape drawn in WebGL2; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --bg #0e0e0e, --card, --fg #edeae3, --mute, --line,
            --paper (the cream changelog), --ink; Sofia Sans Extra Condensed 900 for the fitted display type,
            Martian Mono for labels and body; two eases (--ease for reveals, --roll for link and arrow rolls)
  sections  nav, hero, intro, gallery, marquee, clients, changelog, cta, footer (each carries data-section)
  scripts   one classic IIFE: SVG client logos fitted to their box, one shared WebGL2 context that raymarches a
            morphing SDF shape into an offscreen target and Bayer-dithers it (2, 4 or 8) with a mask outline,
            then copies it into each [data-art] canvas; fit-to-width headings, reveals, hero parallax, a
            scroll-driven marquee, a flashing preset band and the phone menu
  assets    no image files; fonts from Google Fonts; every plate is a SPEC entry (shapes, palette, camera, matrix)

  ADAPTING
  - Add a plate: a <div class="art" data-art="name"> inside any sized box and a SPEC entry with that name.
  - Plates only draw while on screen, and changelog plates only while their row is hovered.
  - Breakpoints at 1200px (tablet) and 810px (phone, where the nav becomes a menu panel).
  - Without WebGL2 each plate falls back to its palette colour with a CSS dot grid.
  - prefers-reduced-motion: plates hold one shape and redraw only on pointer moves; reveals show at once.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Ditherform — AI 3D dither element generator</title>
<meta name="description" content="Describe a shape, get a live 3D dither element. Ditherform generates raymarched objects in ordered Bayer dots, ready to drop into any site.">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' fill='%230e0e0e'/%3E%3Ctext x='16' y='23' text-anchor='middle' font-family='Arial Narrow,Arial' font-weight='900' font-size='18' fill='%23edeae3'%3EDF%3C/text%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Martian+Mono:wght@400;700&family=Sofia+Sans+Extra+Condensed:ital,wght@0,600;0,900;1,900&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#0e0e0e;--card:#161616;--fg:#edeae3;--mute:#8a8a85;
  --line:#edeae324;--line2:#2a2a2a;
  --ink:#0e0e0e;--ink-mute:#0e0e0e9e;--ink-line:#0e0e0e29;--paper:#edeae3;
  --display:"Sofia Sans Extra Condensed","Arial Narrow",sans-serif;
  --mono:"Martian Mono",ui-monospace,monospace;
  --ease:cubic-bezier(.12,.23,.27,1);
  --roll:cubic-bezier(.65,0,.2,1);
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--fg);font-family:var(--mono);-webkit-font-smoothing:antialiased;overflow-x:hidden}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit}
.label{font:400 12px/1.4 var(--mono);letter-spacing:.04em;text-transform:uppercase;color:var(--mute)}
.label.fg{color:var(--fg)}
.body{font:400 12px/1.6 var(--mono)}
.ic{fill:none;stroke:currentColor;stroke-linecap:round;stroke-linejoin:round;stroke-width:2.25}

/* dithered SDF plates (image modules) */
.art{position:absolute;inset:0;overflow:hidden;background-color:#a0a890}
.art canvas{width:100%;height:100%;display:block;image-rendering:crisp-edges;image-rendering:pixelated}
.no-gl .art{background-image:radial-gradient(circle,#4f584266 1.1px,transparent 1.5px);background-size:7px 7px}

/* fit text */
.fit{display:block;width:100%;white-space:nowrap;font-family:var(--display);font-weight:900;text-transform:uppercase;line-height:.88}
.fit>span{display:inline-block;font-size:160px}

/* reveal */
[data-reveal]{opacity:0;transform:translateY(24px);transition:opacity .6s var(--ease),transform .6s var(--ease);transition-delay:var(--d,0s)}
[data-reveal].in{opacity:1;transform:none}

/* roll links */
.rl{display:inline-block;position:relative;overflow:hidden;vertical-align:top;line-height:1.4}
.rl>span{display:block;transition:transform .5s var(--roll)}
.rl>span+span{position:absolute;left:0;top:100%}
a:hover .rl>span{transform:translateY(-100%)}

/* nav */
.nav{position:fixed;top:0;left:0;right:0;z-index:50;height:64px;display:flex;justify-content:space-between;align-items:stretch;
  background:#0e0e0eb8;backdrop-filter:blur(16px);-webkit-backdrop-filter:blur(16px);border-bottom:1px solid var(--line2)}
.brand{display:flex;align-items:center;padding:0 24px;border-right:1px solid var(--line);font:900 32px/1 var(--display);text-transform:uppercase;color:var(--fg)}
.nav-r{display:flex}
.latest{display:flex;align-items:center;gap:12px;padding:0 24px;border-left:1px solid var(--line)}
.latest .thumb{width:32px;height:32px;position:relative;overflow:hidden}
.latest .body{color:var(--fg)}
.latest:hover .body{text-decoration:underline;text-underline-offset:3px}
.navlinks{display:flex}
.navlinks a{display:flex;align-items:center;padding:0 24px;border-left:1px solid var(--line)}
.menu-btn{display:none;flex-direction:column;align-items:flex-start;gap:4px;background:none;border:0;cursor:pointer;align-self:center;transform:scale(.84)}
.menu-btn .wb{height:16px;width:36px;overflow:hidden;position:relative;transition:width .4s var(--roll)}
.menu-btn .wb span{position:absolute;left:0;transition:top .4s var(--roll);color:var(--fg)}
.menu-btn .w1{top:0}.menu-btn .w2{top:16px}
.menu-btn .rule{height:1px;width:0;background:var(--fg);transition:width .4s var(--roll)}
.menu-btn:hover .rule{width:35px}
body.menu-open .menu-btn .wb{width:45px}
body.menu-open .menu-btn .w1{top:-16px}
body.menu-open .menu-btn .w2{top:0}
body.menu-open .menu-btn .rule{width:44px}
.mmenu{position:fixed;inset:64px 0 0 0;z-index:49;background:var(--bg);padding:16px 16px 32px;display:flex;flex-direction:column;justify-content:space-between;
  opacity:0;transform:translateY(-8px);pointer-events:none;transition:opacity .35s var(--ease),transform .35s var(--ease)}
body.menu-open .mmenu{opacity:1;transform:none;pointer-events:auto}
.mmenu nav a{display:block;font:900 64px/1 var(--display);text-transform:uppercase;padding:14px 0 10px;border-bottom:1px solid var(--line)}
.mmenu .mfoot{display:flex;flex-wrap:wrap;gap:12px 20px}

/* hero */
.hero{position:relative;z-index:1;display:flex;flex-direction:column;gap:24px;padding:80px 24px 64px}
.hero h1{position:sticky;top:64px;z-index:2;mix-blend-mode:difference;color:var(--fg)}
.hero-img{position:relative;height:80vh;overflow:clip;transform:scale(1.04);transition:transform 1.6s cubic-bezier(.2,.7,.2,1)}
.loaded .hero-img{transform:none}
.hero-img .art{inset:-60px 0;will-change:transform}

/* intro */
.intro{display:flex;gap:24px;padding:128px 24px}
.ic1{flex:1;display:flex;align-items:flex-start}
.stmt{position:sticky;top:368px;display:flex;flex-direction:column;gap:24px}
.stmt .body,.bio .body{max-width:320px;color:var(--fg)}
.portrait{flex:1.4;height:760px;position:relative;overflow:clip}
.portrait .art{inset:0 -3.6%}
.ic3{flex:1;display:flex;flex-direction:column;justify-content:flex-end}
.bio{display:flex;flex-direction:column;gap:24px;align-items:flex-start}

/* button */
.btn{display:inline-flex;align-items:center;padding:8px 8px 8px 16px;border:1px solid var(--line2);transition:border-color .3s}
.btn:hover{border-color:var(--mute)}
.slot{width:24px;height:24px;margin-left:8px;position:relative;overflow:hidden}
.slot svg{position:absolute;width:16px;height:16px;transform:translate(-50%,-50%);transition:left .45s var(--roll),top .45s var(--roll)}
.slot .ain{left:120%;top:-20%}.slot .aout{left:50%;top:50%}
.btn:hover .ain{left:50%;top:50%}.btn:hover .aout{left:-20%;top:120%}

/* selected work */
.work{position:relative;z-index:1;padding:128px 24px 0}
.grid{display:grid;grid-template-columns:1fr 1fr}
.card{position:relative;display:flex;overflow:clip;background:var(--card);height:560px}
.card.full{grid-column:1/-1}
.card.tall{height:680px}
.card .art{transition:transform 1.2s cubic-bezier(.2,.7,.2,1)}
.card:hover .art{transform:scale(1.04)}
.cap{position:relative;flex:1;display:flex;align-items:flex-start;padding:64px 24px 24px}
.cap-row{position:sticky;top:368px;flex:1;display:flex;justify-content:space-between;align-items:center;mix-blend-mode:difference;color:var(--fg)}
.cap h3{font:900 64px/.9 var(--display);text-transform:uppercase}
.meta{display:flex;gap:8px;opacity:0;transition:opacity .4s}
.meta .label{color:var(--fg)}
.card:hover .meta{opacity:1}

.band{position:relative;grid-column:1/-1;display:flex;align-items:center;justify-content:center;height:128px;background:var(--card);overflow:clip}
.band .flash{position:absolute;inset:0;opacity:0;transition:opacity .25s}
.band:hover .flash{opacity:1}
.band .scrim{position:absolute;inset:0;background:rgba(14,14,14,.35)}
.band h2{position:relative;z-index:1;font:900 64px/.9 var(--display);text-transform:uppercase}
.band .side{display:none;align-items:center;gap:16px}
.band .side .label{color:var(--ink-mute)}
.bdisc{width:64px;height:64px;border:1px solid var(--ink);border-radius:50%;display:flex;align-items:center;justify-content:center}
.bdisc svg{width:24px;height:24px;stroke-width:1.5}

/* marquee */
.marq-wrap{position:relative;z-index:1;padding:0 0 128px}
.marq{height:320px;overflow:hidden;display:flex;align-items:center;container-type:size}
.track{display:flex;flex-shrink:0;font:900 100cqh/1 var(--display);text-transform:uppercase;will-change:transform}
.mi{display:flex;align-items:center;flex-shrink:0;gap:.3em;padding-right:.3em;white-space:nowrap}
.sq{display:inline-block;width:.14em;height:.14em;background:currentColor}

/* clients */
.clients{position:relative;z-index:1;padding:0 24px 96px}
.clients .tag{padding:0 0 16px}
.wall{display:grid;grid-template-columns:repeat(4,1fr);border-top:1px solid var(--line);border-left:1px solid var(--line)}
.cell{position:relative;height:240px;display:flex;align-items:center;justify-content:center;padding:0 16px;border-right:1px solid var(--line);border-bottom:1px solid var(--line)}
.logo{width:100%;max-width:256px;aspect-ratio:10/3;color:var(--fg);opacity:.85;transition:opacity .3s}
.cell:hover .logo{opacity:1}
.logo svg{width:100%;height:100%;display:block}
.cell .label{position:absolute;left:16px;bottom:14px}

/* journal */
.journal{position:relative;z-index:1;background:var(--paper);color:var(--ink);display:flex;flex-direction:column;gap:48px;padding:48px 24px 96px}
.jhead{display:flex;flex-direction:column;gap:40px}
.introrow{display:flex;gap:24px}
.sp96{width:96px;flex:none}.grow{flex:1}.sp48{width:48px;flex:none}
.jintro{flex:1;max-width:320px}
.posts{border-bottom:1px solid var(--ink-line)}
.row{position:relative;display:flex;align-items:center;gap:24px;padding:24px 24px 24px 0;border-top:1px solid var(--ink-line);overflow:clip;
  transition:padding .5s var(--roll),color .4s}
.row .bg{position:absolute;inset:0;overflow:hidden;transform:translateY(-100%);transition:transform .5s var(--roll)}
.row .bg .art{transform:scale(1.08);transition:transform .9s var(--roll)}
.row .bg::after{content:"";position:absolute;inset:0;background:rgba(14,14,14,.55)}
.row>*:not(.bg){position:relative}
.date{width:96px;flex:none;color:var(--ink-mute)}
.rtitle{flex:1;font:900 48px/.9 var(--display);text-transform:uppercase}
.exc{flex:1;max-width:320px;color:var(--ink-mute);transition:color .4s}
.disc{width:48px;height:48px;flex:none;border:1px solid currentColor;border-radius:50%;position:relative;overflow:hidden}
.disc svg{position:absolute;width:20px;height:20px;left:13px;stroke-width:1.5;transition:top .5s var(--roll)}
.disc .i1{top:13px}.disc .i2{top:62px}
@media (hover:hover) and (min-width:810px){
  .row:hover{padding:24px;color:var(--paper)}
  .row:hover .bg{transform:none}
  .row:hover .bg .art{transform:scale(1)}
  .row:hover .date,.row:hover .exc{color:#edeae3b8}
  .row:hover .i1{top:-34px}.row:hover .i2{top:13px}
}

/* cta */
.cta{position:relative;z-index:2;display:flex;flex-direction:column;align-items:center;gap:40px;padding:160px 24px 112px;text-align:center}
.cta .fit{text-align:center}

/* footer */
.foot{display:flex;height:64px;border-top:1px solid var(--line)}
.copy{display:flex;align-items:center;padding:0 24px;border-right:1px solid var(--line)}
.fsp{flex:1}
.flinks{display:flex}
.flinks a{display:flex;align-items:center;justify-content:center;padding:0 24px;border-left:1px solid var(--line)}
.flinks .div{display:none}

/* tablet */
@media (max-width:1199.98px){
  .latest{display:none}
  .brand{padding:0 20px}
  .hero{padding:80px 20px 64px}
  .intro{flex-direction:column;gap:48px;padding:96px 20px}
  .ic1,.ic3{flex:none;width:100%}
  .stmt{position:static}
  .stmt .body,.bio .body{max-width:560px}
  .portrait{flex:none;width:100%;height:640px}
  .portrait .art{inset:0 -1.2%}
  .work{padding:128px 20px 64px}
  .card{height:440px}.card.tall{height:520px}
  .cap{padding:64px 20px 20px}
  .cap h3{font-size:48px}
  .meta{opacity:1}
  .band{background:var(--paper);color:var(--ink);justify-content:space-between;padding:0 20px;height:112px}
  .band .flash,.band .scrim{display:none}
  .band h2{font-size:48px}
  .band .side{display:flex}
  .marq-wrap{padding-bottom:128px}
  .marq{height:224px}
  .clients{padding:0 20px 72px}
  .wall{grid-template-columns:repeat(2,1fr)}
  .cell{height:200px}
  .journal{padding:40px 20px 64px}
  .jhead{gap:32px}
  .rtitle{font-size:40px}
  .cta{padding:120px 20px 80px}
  .foot{flex-direction:column;height:auto}
  .copy{height:56px;padding:0 20px;border-right:0;border-bottom:1px solid var(--line)}
  .fsp{display:none}
  .flinks{height:56px}
  .flinks a{flex:1;padding:0 12px}
  .flinks a:first-child{border-left:0}
}
/* phone */
@media (max-width:809.98px){
  .nav{padding:0 16px}
  .brand{padding:0;border:0;font-size:24px}
  .navlinks{display:none}
  .menu-btn{display:flex}
  .hero{padding:80px 16px 48px}
  .intro{gap:40px;padding:64px 16px}
  .portrait{height:480px}
  .work{padding:128px 16px 64px}
  .grid{display:flex;flex-direction:column}
  .card,.card.tall{height:400px}
  .cap{padding:64px 16px 16px}
  .cap-row{flex-direction:column;align-items:flex-start;gap:8px;flex:none;width:100%}
  .cap h3{font-size:40px}
  .band{height:96px;padding:0 16px}
  .band h2{font-size:40px}
  .band .side .label{display:none}
  .bdisc{width:48px;height:48px}
  .bdisc svg{width:20px;height:20px}
  .marq{height:112px}
  .clients{padding:0 16px 56px}
  .cell{height:148px;padding:0 12px}
  .cell .label{font-size:10px;left:12px;bottom:10px}
  .journal{padding:32px 16px 64px}
  .jhead{gap:24px}
  .sp96,.grow,.sp48{display:none}
  .jintro{max-width:none}
  .row{flex-direction:column;align-items:flex-start;gap:12px;padding:24px 0}
  .date,.exc{width:100%;max-width:none}
  .rtitle{font-size:32px;flex:none;width:100%}
  .disc{width:40px;height:40px}
  .disc svg{left:9px}.disc .i1{top:9px}
  .cta{gap:32px;padding:96px 16px 64px}
  .copy{justify-content:center;padding:0 16px}
  .flinks{display:grid;grid-template-columns:repeat(3,1fr);height:auto}
  .flinks a{height:56px}
  .flinks a:first-child{grid-column:1/-1}
  .flinks .div{display:block;grid-column:1/-1;height:1px;background:var(--line)}
}
@media (prefers-reduced-motion:reduce){
  *{transition:none!important;scroll-behavior:auto!important}
  [data-reveal]{opacity:1;transform:none}
}
</style>
</head>
<body>
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <symbol id="arw" viewBox="0 0 24 24"><path d="M7 7h10v10M7 17L17 7"/></symbol>
</svg>

<!-- NAV -->
<header class="nav" data-section="nav">
  <a class="brand" href="#top">Ditherform</a>
  <div class="nav-r">
    <a class="latest" href="#work">
      <div class="thumb" data-art="redroom"></div>
      <span class="body">New: Morph v2</span>
    </a>
    <nav class="navlinks">
      <a href="#work"><span class="label fg rl"><span>Gallery</span><span aria-hidden="true">Gallery</span></span></a>
      <a href="#intro"><span class="label fg rl"><span>Product</span><span aria-hidden="true">Product</span></span></a>
      <a href="#journal"><span class="label fg rl"><span>Changelog</span><span aria-hidden="true">Changelog</span></span></a>
      <a href="#contact"><span class="label fg rl"><span>Get access</span><span aria-hidden="true">Get access</span></span></a>
    </nav>
    <button class="menu-btn" aria-label="Toggle menu" aria-expanded="false">
      <span class="wb"><span class="label w1">Menu</span><span class="label w2">Close</span></span>
      <span class="rule"></span>
    </button>
  </div>
</header>
<div class="mmenu" aria-hidden="true">
  <nav>
    <a href="#work">Gallery</a><a href="#intro">Product</a><a href="#journal">Changelog</a><a href="#contact">Get access</a>
  </nav>
  <div class="mfoot">
    <a class="label fg" href="mailto:hello@ditherform.app">hello@ditherform.app</a>
    <a class="label" href="https://github.com" target="_blank" rel="noopener">GitHub</a>
    <a class="label" href="https://discord.com" target="_blank" rel="noopener">Discord</a>
    <a class="label" href="#intro">Docs</a>
  </div>
</div>

<main id="top">
  <!-- 01 HERO -->
  <section class="hero" data-section="hero">
    <h1 class="fit" data-reveal style="--d:.1s"><span>Ditherform</span></h1>
    <div class="hero-img"><div class="art" data-art="desert" id="heroArt"></div></div>
  </section>

  <!-- 02 INTRO -->
  <section class="intro" id="intro" data-section="intro">
    <div class="ic1">
      <div class="stmt">
        <p class="body" style="color:var(--mute)" data-reveal>[ What it is ]</p>
        <p class="body" data-reveal style="--d:.08s">Ditherform is an AI generator for 3D dither elements. Describe a shape in plain words and get a live, raymarched object rendered in ordered Bayer dots, ready for your site.</p>
      </div>
    </div>
    <div class="portrait"><div class="art" data-art="portrait"></div></div>
    <div class="ic3">
      <div class="bio">
        <p class="body" data-reveal>Prompt it, pick a palette, tune the matrix, then export a WebGL embed, a looping video or a sprite sheet. Every element stays code: no images, no video files, nothing to host.</p>
        <a class="btn" href="#intro" data-reveal style="--d:.08s">
          <span class="label fg">How it works</span>
          <span class="slot"><svg class="ic ain"><use href="#arw"/></svg><svg class="ic aout"><use href="#arw"/></svg></span>
        </a>
      </div>
    </div>
  </section>

  <!-- 03 SELECTED WORK -->
  <section class="work" id="work" data-section="gallery">
    <h2 class="fit" data-reveal><span>Generated elements</span></h2>
    <div class="grid">
      <a class="card full" href="#work">
        <div class="art" data-art="redroom"></div>
        <div class="cap"><div class="cap-row"><h3>Clay Loop</h3>
          <div class="meta"><span class="label">Morph</span><span class="label">▪</span><span class="label">4×4 Bayer</span></div></div></div>
      </a>
      <a class="card tall" href="#work">
        <div class="art" data-art="neutral"></div>
        <div class="cap"><div class="cap-row"><h3>Sand Column</h3>
          <div class="meta"><span class="label">Product</span><span class="label">▪</span><span class="label">8×8 Bayer</span></div></div></div>
      </a>
      <a class="card tall" href="#work">
        <div class="art" data-art="bareskin"></div>
        <div class="cap"><div class="cap-row"><h3>Peach Bloom</h3>
          <div class="meta"><span class="label">Hero</span><span class="label">▪</span><span class="label">2px outline</span></div></div></div>
      </a>
      <a class="card full" href="#work">
        <div class="art" data-art="concrete"></div>
        <div class="cap"><div class="cap-row"><h3>Stone Block</h3>
          <div class="meta"><span class="label">Architecture</span><span class="label">▪</span><span class="label">8×8 Bayer</span></div></div></div>
      </a>
      <a class="band" href="#work" id="band">
        <div class="flash" id="flash"></div>
        <div class="scrim"></div>
        <h2>Browse all presets</h2>
        <div class="side">
          <span class="label">48 presets</span>
          <span class="bdisc"><svg class="ic"><use href="#arw"/></svg></span>
        </div>
      </a>
    </div>
  </section>

  <!-- 04 MARQUEE -->
  <section class="marq-wrap" data-section="marquee" aria-label="Type a shape, get dots">
    <div class="marq"><div class="track" id="track">
      <div class="mi"><span>Type a shape, get dots</span><span class="sq"></span></div>
      <div class="mi" aria-hidden="true"><span>Type a shape, get dots</span><span class="sq"></span></div>
      <div class="mi" aria-hidden="true"><span>Type a shape, get dots</span><span class="sq"></span></div>
      <div class="mi" aria-hidden="true"><span>Type a shape, get dots</span><span class="sq"></span></div>
    </div></div>
  </section>

  <!-- 05 CLIENTS -->
  <section class="clients" data-section="clients">
    <div class="tag"><p class="label" data-reveal>[ Used by teams at ▪ 2025 – 2026 ]</p></div>
    <div class="wall">
      <div class="cell" data-reveal style="--d:0s"><div class="logo" data-logo="whitlock" role="img" aria-label="Kernel Studio logo"></div><p class="label">Landing page ▪ 2026</p></div>
      <div class="cell" data-reveal style="--d:.06s"><div class="logo" data-logo="lumen" role="img" aria-label="Lumen UI logo"></div><p class="label">Docs site ▪ 2026</p></div>
      <div class="cell" data-reveal style="--d:.12s"><div class="logo" data-logo="north" role="img" aria-label="North Current logo"></div><p class="label">Launch video ▪ 2025</p></div>
      <div class="cell" data-reveal style="--d:.18s"><div class="logo" data-logo="drycreek" role="img" aria-label="Peak Labs logo"></div><p class="label">Product UI ▪ 2026</p></div>
      <div class="cell" data-reveal style="--d:0s"><div class="logo" data-logo="caliche" role="img" aria-label="Frame Co. logo"></div><p class="label">Motion kit ▪ 2025</p></div>
      <div class="cell" data-reveal style="--d:.06s"><div class="logo" data-logo="hollis" role="img" aria-label="Pixel &amp; Rye logo"></div><p class="label">Brand refresh ▪ 2026</p></div>
      <div class="cell" data-reveal style="--d:.12s"><div class="logo" data-logo="pecos" role="img" aria-label="Arch OS logo"></div><p class="label">Onboarding ▪ 2025</p></div>
      <div class="cell" data-reveal style="--d:.18s"><div class="logo" data-logo="mesa" role="img" aria-label="Mesa Systems logo"></div><p class="label">Design system ▪ 2026</p></div>
    </div>
  </section>

  <!-- 06 JOURNAL -->
  <section class="journal" id="journal" data-section="changelog">
    <div class="jhead">
      <h2 class="fit" data-reveal><span>From the changelog</span></h2>
      <div class="introrow">
        <div class="sp96"></div><div class="grow"></div>
        <p class="body jintro" data-reveal>What shipped, what broke, and the occasional argument about thresholds. New releases land here first.</p>
        <div class="sp48"></div>
      </div>
    </div>
    <div class="posts">
      <a class="row" href="#journal" data-reveal style="--d:.1s">
        <div class="bg"><div class="art" data-art="redroom"></div></div>
        <p class="body date"><time datetime="2026-10-21">Oct 21</time></p>
        <h3 class="rtitle">Morph v2</h3>
        <p class="body exc">Blend any two prompts. Shapes now interpolate through their distance fields in one second, with no popping.</p>
        <span class="disc"><svg class="ic i2"><use href="#arw"/></svg><svg class="ic i1"><use href="#arw"/></svg></span>
      </a>
      <a class="row" href="#journal" data-reveal style="--d:.2s">
        <div class="bg"><div class="art" data-art="grass"></div></div>
        <p class="body date"><time datetime="2026-09-30">Sep 30</time></p>
        <h3 class="rtitle">Palettes from a photo</h3>
        <p class="body exc">Drop in a reference image and Ditherform pulls a two-ink palette that holds up at any matrix size.</p>
        <span class="disc"><svg class="ic i2"><use href="#arw"/></svg><svg class="ic i1"><use href="#arw"/></svg></span>
      </a>
      <a class="row" href="#journal" data-reveal style="--d:.3s">
        <div class="bg"><div class="art" data-art="packing"></div></div>
        <p class="body date"><time datetime="2026-09-09">Sep 9</time></p>
        <h3 class="rtitle">Export to sprite sheet</h3>
        <p class="body exc">Render any loop to a PNG strip for places WebGL can’t go: email, slides and game engines.</p>
        <span class="disc"><svg class="ic i2"><use href="#arw"/></svg><svg class="ic i1"><use href="#arw"/></svg></span>
      </a>
      <a class="row" href="#journal" data-reveal style="--d:.4s">
        <div class="bg"><div class="art" data-art="bareskin"></div></div>
        <p class="body date"><time datetime="2026-08-14">Aug 14</time></p>
        <h3 class="rtitle">Outlines that stay put</h3>
        <p class="body exc">Silhouette strokes now come from the hit mask, not the lighting, so edges stop shimmering as objects turn.</p>
        <span class="disc"><svg class="ic i2"><use href="#arw"/></svg><svg class="ic i1"><use href="#arw"/></svg></span>
      </a>
      <a class="row" href="#journal" data-reveal style="--d:.5s">
        <div class="bg"><div class="art" data-art="noon"></div></div>
        <p class="body date"><time datetime="2026-07-22">Jul 22</time></p>
        <h3 class="rtitle">8×8 Bayer, finally</h3>
        <p class="body exc">A finer matrix for big hero plates, plus a contrast curve that keeps midtones from turning to mud.</p>
        <span class="disc"><svg class="ic i2"><use href="#arw"/></svg><svg class="ic i1"><use href="#arw"/></svg></span>
      </a>
    </div>
  </section>

  <!-- 07 CTA -->
  <section class="cta" id="contact" data-section="cta">
    <h2 class="fit" data-reveal><span>Start dithering</span></h2>
    <a class="btn" href="mailto:hello@ditherform.app" data-reveal style="--d:.08s">
      <span class="label fg">Generate your first element</span>
      <span class="slot"><svg class="ic ain"><use href="#arw"/></svg><svg class="ic aout"><use href="#arw"/></svg></span>
    </a>
    <p class="label" data-reveal style="--d:.16s">Runs in the browser ▪ WebGL2</p>
  </section>
</main>

<footer class="foot" data-section="footer">
  <div class="copy"><p class="label">© 2026 Ditherform ▪ Made with dots</p></div>
  <div class="fsp"></div>
  <div class="flinks">
    <a href="mailto:hello@ditherform.app"><span class="label fg rl"><span>hello@ditherform.app</span><span aria-hidden="true">hello@ditherform.app</span></span></a>
    <span class="div"></span>
    <a href="https://github.com" target="_blank" rel="noopener"><span class="label fg rl"><span>GitHub</span><span aria-hidden="true">GitHub</span></span></a>
    <a href="https://discord.com" target="_blank" rel="noopener"><span class="label fg rl"><span>Discord</span><span aria-hidden="true">Discord</span></span></a>
    <a href="#intro"><span class="label fg rl"><span>Docs</span><span aria-hidden="true">Docs</span></span></a>
  </div>
</footer>

<script>
(function(){
/* ---------- client logos ---------- */
const T=(x,y,s,txt,f,extra='')=>`<text x="${x}" y="${y}" font-size="${s}" font-family="${f}" fill="currentColor" ${extra}>${txt}</text>`;
const D='Sofia Sans Extra Condensed,Arial Narrow,sans-serif', M='Martian Mono,monospace', S='Georgia,Times New Roman,serif';
const LOGO={
  whitlock:T(180,64,46,'Kernel',S,'text-anchor="middle" font-style="italic"')+T(180,90,10,'STUDIO',M,'text-anchor="middle" letter-spacing="7"'),
  lumen:`<circle cx="70" cy="54" r="20" fill="none" stroke="currentColor" stroke-width="3"/>${[0,45,90,135,180,225,270,315].map(a=>{const c=Math.cos(a*Math.PI/180),s=Math.sin(a*Math.PI/180);return`<line x1="${70+c*28}" y1="${54+s*28}" x2="${70+c*38}" y2="${54+s*38}" stroke="currentColor" stroke-width="3" stroke-linecap="round"/>`}).join('')}`+T(122,70,46,'LUMEN UI',D,'font-weight="900"'),
  north:[34,48,62].map(y=>`<path d="M30 ${y} q12 -10 24 0 t24 0 t24 0" fill="none" stroke="currentColor" stroke-width="3.5" stroke-linecap="round"/>`).join('')+T(118,68,40,'NORTH CURRENT',D,'font-weight="900"'),
  drycreek:`<path d="M30 76 L62 30 L80 54 L92 40 L118 76Z" fill="currentColor"/>`+T(132,62,44,'PEAK LABS',D,'font-weight="900"')+T(134,84,9,'DESIGN',M,'letter-spacing="6"'),
  caliche:`<rect x="26" y="30" width="62" height="48" rx="3" fill="none" stroke="currentColor" stroke-width="3"/>${[36,48,60,72].map(x=>`<rect x="${x-2}" y="34" width="5" height="6" fill="currentColor"/><rect x="${x-2}" y="68" width="5" height="6" fill="currentColor"/>`).join('')}`+T(102,66,32,'Frame Co.',S),
  hollis:T(150,70,40,'PIXEL',D,'font-weight="900" text-anchor="end"')+T(178,80,64,'&amp;',S,'font-style="italic" text-anchor="middle"')+T(206,70,40,'RYE',D,'font-weight="900"'),
  pecos:`<path d="M34 80 V52 A26 26 0 0 1 86 52 V80" fill="none" stroke="currentColor" stroke-width="4"/><path d="M48 80 V58 A12 12 0 0 1 72 58 V80" fill="currentColor"/>`+T(104,70,44,'ARCH OS',D,'font-weight="900"'),
  mesa:`<rect x="30" y="34" width="70" height="10" fill="currentColor"/><rect x="40" y="50" width="50" height="10" fill="currentColor"/><rect x="22" y="66" width="86" height="10" fill="currentColor"/>`+T(122,52,15,'MESA',M,'font-weight="700" letter-spacing="4"')+T(122,74,15,'SYSTEMS',M,'font-weight="700" letter-spacing="4"')
};
document.querySelectorAll('[data-logo]').forEach(el=>{el.innerHTML=`<svg viewBox="0 0 360 108" xmlns="http://www.w3.org/2000/svg">${LOGO[el.dataset.logo]}</svg>`;});
// keep every wordmark inside its 360-wide box whatever font is active
function fitLogos(){
  document.querySelectorAll('.logo text').forEach(t=>{
    t.removeAttribute('textLength');t.removeAttribute('lengthAdjust');
    const anchor=t.getAttribute('text-anchor'), x=+t.getAttribute('x');
    const room=anchor==='middle'?Math.min(x,360-x)*2-8:anchor==='end'?x-8:352-x;
    let len=0; try{len=t.getComputedTextLength();}catch(e){}
    if(len>room){t.setAttribute('textLength',room);t.setAttribute('lengthAdjust','spacingAndGlyphs');}
  });
}
fitLogos(); if(document.fonts) document.fonts.ready.then(fitLogos);

/* =========================================================
   DITHERED SDF PLATES — every image module is a live
   raymarched shape, Bayer-dithered with a solid outline.
   One shared WebGL2 context renders all of them.
========================================================= */
document.getElementById('flash').innerHTML='<div class="art" data-art="flash"></div>';
const reduce=matchMedia('(prefers-reduced-motion:reduce)').matches;

// [background, ink, light] per palette
const PAL={
  sage :[[160,168,144],[79,88,66],[149,157,132]],
  clay :[[201,160,140],[110,42,31],[185,141,120]],
  sand :[[196,180,154],[90,74,56],[179,163,136]],
  peach:[[214,186,165],[104,62,46],[198,169,147]],
  stone:[[186,187,182],[74,76,78],[168,169,164]],
  pool :[[159,180,184],[47,79,90],[142,163,167]]
};
// shapes: 0 rounded cube · 1 sphere · 2 cylinder · 3 torus · 4 octahedron · 5 capsule · 6 goursat
const SPEC={
  desert:  {shapes:[0,1,2,3,4,5,6],pal:'sage', zoom:1.2, yaw:.72, pitch:.55,every:3.2,bayer:4,outline:1},
  portrait:{shapes:[6,1,3],        pal:'sand', zoom:1.15,yaw:-.5, pitch:.4, every:3.6,bayer:4,outline:1},
  redroom: {shapes:[3,5,4],        pal:'clay', zoom:1.15,yaw:.9,  pitch:.6, every:3.4,bayer:4,outline:1},
  neutral: {shapes:[2,0,5],        pal:'sand', zoom:1.2, yaw:-.7, pitch:.5, every:3.8,bayer:8,outline:1},
  bareskin:{shapes:[1,6,0],        pal:'peach',zoom:1.1, yaw:.3,  pitch:.3, every:3.5,bayer:4,outline:2},
  concrete:{shapes:[0,4,2],        pal:'stone',zoom:1.2, yaw:.6,  pitch:.7, every:4.0,bayer:8,outline:1},
  grass:   {shapes:[5,2,3],        pal:'sage', zoom:1.2, yaw:-.3, pitch:.5, every:3.0,bayer:4,outline:1},
  packing: {shapes:[0,2,1],        pal:'sand', zoom:1.2, yaw:.4,  pitch:.9, every:3.0,bayer:2,outline:1},
  noon:    {shapes:[3,1,6],        pal:'pool', zoom:1.15,yaw:1.1, pitch:.8, every:3.2,bayer:4,outline:1},
  flash:   {shapes:[0,1,2,3,4,5,6],pal:'sage', zoom:1.2, yaw:.7,  pitch:.55,every:1,  bayer:4,outline:1}
};
const FLASH=Object.keys(SPEC).filter(k=>k!=='flash').map(k=>SPEC[k]);
const rgb=c=>`rgb(${c[0]},${c[1]},${c[2]})`;

const VS=`#version 300 es
void main(){
  vec2 p=vec2[3](vec2(-1.0,-1.0),vec2(3.0,-1.0),vec2(-1.0,3.0))[gl_VertexID];
  gl_Position=vec4(p,0.0,1.0);
}`;

const SCENE=`#version 300 es
precision highp float;
layout(location=0) out vec4 outColor;
layout(location=1) out vec4 outMask;
uniform vec2 uResolution;
uniform float uMorph;
uniform int uShapeA;
uniform int uShapeB;
uniform vec2 uCamera;
uniform float uZoom;
const float MAX_DISTANCE=30.0;
const int MAX_STEPS=100;
float sdSphere(vec3 p,float r){return length(p)-r;}
float sdRoundBox(vec3 p,vec3 b,float r){vec3 q=abs(p)-b;return length(max(q,0.0))+min(max(q.x,max(q.y,q.z)),0.0)-r;}
float sdCylinder(vec3 p,float h,float r){vec2 d=abs(vec2(length(p.xz),p.y))-vec2(r,h);return min(max(d.x,d.y),0.0)+length(max(d,0.0));}
float sdTorus(vec3 p,vec2 t){return length(vec2(length(p.xz)-t.x,p.y))-t.y;}
float sdOctahedron(vec3 p,float s){p=abs(p);return (p.x+p.y+p.z-s)*0.57735027;}
float sdCapsule(vec3 p,vec3 a,vec3 b,float r){vec3 pa=p-a,ba=b-a;float h=clamp(dot(pa,ba)/dot(ba,ba),0.0,1.0);return length(pa-ba*h)-r;}
float sdGoursat(vec3 p){
  vec3 p2=p*p; vec3 p3=p2*p;
  float f=dot(p2,p2)-dot(p,p)+0.40;
  vec3 g=4.0*p3-2.0*p;
  return f/max(length(g),0.0001);
}
float shapeDistance(vec3 p,int s){
  if(s==0) return sdRoundBox(p,vec3(0.70),0.15);
  if(s==1) return sdSphere(p,0.82);
  if(s==2) return sdCylinder(p,0.76,0.68);
  if(s==3) return sdTorus(p,vec2(0.84,0.43));
  if(s==4) return sdOctahedron(p,1.18);
  if(s==5) return sdCapsule(p,vec3(0.0,-0.58,0.0),vec3(0.0,0.58,0.0),0.63);
  return sdGoursat(p);
}
float objectDistance(vec3 p){
  return mix(shapeDistance(p,uShapeA),shapeDistance(p,uShapeB),clamp(uMorph,0.0,1.0));
}
vec3 getNormal(vec3 p){
  const float e=0.0015;
  return normalize(vec3(
    objectDistance(p+vec3(e,0,0))-objectDistance(p-vec3(e,0,0)),
    objectDistance(p+vec3(0,e,0))-objectDistance(p-vec3(0,e,0)),
    objectDistance(p+vec3(0,0,e))-objectDistance(p-vec3(0,0,e))));
}
float raymarch(vec3 ro,vec3 rd){
  float t=0.0;
  for(int i=0;i<MAX_STEPS;i++){
    float d=objectDistance(ro+rd*t);
    if(d<0.0015) return t;
    t+=max(d*0.85,0.001);
    if(t>MAX_DISTANCE) break;
  }
  return -1.0;
}
float softShadow(vec3 ro,vec3 rd,float md){
  float r=1.0,t=0.025;
  for(int i=0;i<48;i++){
    float h=objectDistance(ro+rd*t);
    if(h<0.001) return 0.0;
    r=min(r,12.0*h/t);
    t+=clamp(h,0.025,0.18);
    if(t>=md) break;
  }
  return clamp(r,0.0,1.0);
}
float ambientOcclusion(vec3 p,vec3 n){
  float r=0.0,w=1.0;
  for(int i=1;i<=5;i++){float h=0.035+0.10*float(i);r+=(h-objectDistance(p+n*h))*w;w*=0.72;}
  return clamp(1.0-r*1.5,0.0,1.0);
}
void main(){
  vec2 screen=gl_FragCoord.xy/uResolution*2.0-1.0;
  float asp=uResolution.x/uResolution.y;
  screen.x*=asp;
  screen/=min(asp,1.0);
  float yaw=uCamera.x, pitch=uCamera.y;
  vec3 ro=vec3(3.6*sin(yaw)*cos(pitch),3.6*sin(pitch),3.6*cos(yaw)*cos(pitch))*uZoom;
  vec3 fw=normalize(-ro);
  vec3 rt=normalize(cross(fw,vec3(0,1,0)));
  vec3 up=normalize(cross(rt,fw));
  vec3 rd=normalize(rt*screen.x+up*(screen.y-0.08)+fw*2.35);
  float objT=raymarch(ro,rd);
  float hit=objT>0.0?1.0:0.0;
  vec3 color=vec3(1.0);
  float floorY=-1.03, floorT=-1.0;
  if(rd.y<-0.0001) floorT=(floorY-ro.y)/rd.y;
  bool hitObj=objT>0.0;
  bool hitFloor=floorT>0.0&&(!hitObj||floorT<objT);
  vec3 lp=vec3(-3.8,5.0,3.0);
  if(hitObj){
    vec3 p=ro+rd*objT; vec3 n=getNormal(p);
    vec3 tl=lp-p; float ld=length(tl); vec3 l=tl/ld;
    float diff=max(dot(n,l),0.0);
    float sh=softShadow(p+n*0.008,l,ld);
    float ao=ambientOcclusion(p,n);
    float fill=max(dot(n,normalize(vec3(2.0,1.0,-3.0))),0.0);
    color=vec3(clamp((0.24+diff*sh*0.67+fill*0.09)*ao,0.0,0.96));
  } else if(hitFloor){
    vec3 p=ro+rd*floorT;
    vec3 tl=lp-p; float ld=length(tl); vec3 l=tl/ld;
    float sh=softShadow(vec3(p.x,floorY+0.012,p.z),l,ld);
    color=vec3(clamp((0.87+0.13*max(l.y,0.0))*mix(0.66,1.0,sh),0.0,0.98));
  }
  outColor=vec4(color,1.0);
  outMask=vec4(hit,0.0,0.0,1.0);
}`;

const FINAL=`#version 300 es
precision highp float;
out vec4 outColor;
uniform sampler2D uScene;
uniform sampler2D uMask;
uniform vec2 uOffset;
uniform ivec2 uSize;
uniform int uBayerSize;
uniform int uOutlineWidth;
uniform vec3 uBG;
uniform vec3 uInk;
uniform vec3 uLight;
float bayer2(ivec2 p){int v[4]=int[4](0,2,3,1);return (float(v[(p.y&1)*2+(p.x&1)])+0.5)/4.0;}
float bayer4(ivec2 p){int v[16]=int[16](0,8,2,10,12,4,14,6,3,11,1,9,15,7,13,5);return (float(v[(p.y&3)*4+(p.x&3)])+0.5)/16.0;}
float bayer8(ivec2 p){int v[64]=int[64](0,32,8,40,2,34,10,42,48,16,56,24,50,18,58,26,12,44,4,36,14,46,6,38,60,28,52,20,62,30,54,22,3,35,11,43,1,33,9,41,51,19,59,27,49,17,57,25,15,47,7,39,13,45,5,37,63,31,55,23,61,29,53,21);return (float(v[(p.y&7)*8+(p.x&7)])+0.5)/64.0;}
ivec2 cl(ivec2 p){return clamp(p,ivec2(0),uSize-1);}
void main(){
  ivec2 p=ivec2(gl_FragCoord.xy-uOffset);
  vec3 src=texelFetch(uScene,cl(p),0).rgb;
  float lum=dot(src,vec3(0.299,0.587,0.114));
  float cm=texelFetch(uMask,cl(p),0).r;
  float th=uBayerSize==2?bayer2(p):(uBayerSize==8?bayer8(p):bayer4(p));
  vec3 result=mix(uInk,uLight,step(th,lum));
  if(cm<0.5&&lum>0.995) result=uBG;
  float edge=0.0;
  for(int x=-3;x<=3;x++){for(int y=-3;y<=3;y++){
    if(abs(x)<=uOutlineWidth&&abs(y)<=uOutlineWidth&&(x!=0||y!=0)){
      if(cm<0.5&&texelFetch(uMask,cl(p+ivec2(x,y)),0).r>0.5) edge=1.0;
    }
  }}
  if(edge>0.5) result=uInk;
  outColor=vec4(result,1.0);
}`;

const glc=document.createElement('canvas');
const gl=glc.getContext('webgl2',{alpha:false,antialias:false,depth:false,stencil:false,premultipliedAlpha:false});
const mods=[];
let flashMod=null;

function initGL(){
  const sh=(t,s)=>{const o=gl.createShader(t);gl.shaderSource(o,s);gl.compileShader(o);if(!gl.getShaderParameter(o,gl.COMPILE_STATUS))throw new Error(gl.getShaderInfoLog(o));return o;};
  const prog=fs=>{const p=gl.createProgram();gl.attachShader(p,sh(gl.VERTEX_SHADER,VS));gl.attachShader(p,sh(gl.FRAGMENT_SHADER,fs));gl.linkProgram(p);if(!gl.getProgramParameter(p,gl.LINK_STATUS))throw new Error(gl.getProgramInfoLog(p));return p;};
  const P1=prog(SCENE), P2=prog(FINAL);
  const U=(p,names)=>Object.fromEntries(names.map(n=>[n,gl.getUniformLocation(p,n)]));
  const u1=U(P1,['uResolution','uMorph','uShapeA','uShapeB','uCamera','uZoom']);
  const u2=U(P2,['uScene','uMask','uOffset','uSize','uBayerSize','uOutlineWidth','uBG','uInk','uLight']);
  gl.bindVertexArray(gl.createVertexArray());
  const tex=()=>{const t=gl.createTexture();gl.bindTexture(gl.TEXTURE_2D,t);
    [gl.TEXTURE_MIN_FILTER,gl.TEXTURE_MAG_FILTER].forEach(k=>gl.texParameteri(gl.TEXTURE_2D,k,gl.NEAREST));
    [gl.TEXTURE_WRAP_S,gl.TEXTURE_WRAP_T].forEach(k=>gl.texParameteri(gl.TEXTURE_2D,k,gl.CLAMP_TO_EDGE));
    gl.texImage2D(gl.TEXTURE_2D,0,gl.RGBA8,1,1,0,gl.RGBA,gl.UNSIGNED_BYTE,null);return t;};
  const sceneTex=tex(), maskTex=tex(), fbo=gl.createFramebuffer();
  gl.bindFramebuffer(gl.FRAMEBUFFER,fbo);
  gl.framebufferTexture2D(gl.FRAMEBUFFER,gl.COLOR_ATTACHMENT0,gl.TEXTURE_2D,sceneTex,0);
  gl.framebufferTexture2D(gl.FRAMEBUFFER,gl.COLOR_ATTACHMENT1,gl.TEXTURE_2D,maskTex,0);
  gl.drawBuffers([gl.COLOR_ATTACHMENT0,gl.COLOR_ATTACHMENT1]);
  gl.bindFramebuffer(gl.FRAMEBUFFER,null);
  gl.disable(gl.BLEND);gl.disable(gl.DEPTH_TEST);

  let TW=0,TH=0;
  function ensure(w,h){
    if(w<=TW&&h<=TH) return;
    TW=Math.max(TW,w);TH=Math.max(TH,h);
    for(const t of [sceneTex,maskTex]){gl.bindTexture(gl.TEXTURE_2D,t);gl.texImage2D(gl.TEXTURE_2D,0,gl.RGBA8,TW,TH,0,gl.RGBA,gl.UNSIGNED_BYTE,null);}
    glc.width=TW;glc.height=TH;
  }
  const ease=t=>t<.5?4*t*t*t:1-Math.pow(-2*t+2,3)/2;

  return function draw(m,t){
    const w=m.w,h=m.h; if(w<2||h<2) return;
    ensure(w,h);
    let s=m.spec,A,B,mix=0;
    if(m===flashMod){
      s=FLASH[m.idx%FLASH.length];
      A=B=s.shapes[Math.floor(m.idx/FLASH.length)%s.shapes.length];
    } else if(reduce){
      A=B=s.shapes[0];
    } else {
      const ph=(t+m.t0)/s.every, i=Math.floor(ph), loc=(ph-i)*s.every, n=s.shapes.length;
      mix=ease(Math.min(loc/1.1,1)); A=s.shapes[i%n]; B=s.shapes[(i+1)%n];
    }
    m.px+=(m.tx-m.px)*.08; m.py+=(m.ty-m.py)*.08;
    const yaw=s.yaw+(reduce?0:t*.12)+m.px*.9;
    const pitch=Math.max(.05,Math.min(1.1,s.pitch+m.py*.6));
    const [bg,ink,light]=PAL[s.pal];

    gl.bindFramebuffer(gl.FRAMEBUFFER,fbo);
    gl.drawBuffers([gl.COLOR_ATTACHMENT0,gl.COLOR_ATTACHMENT1]);
    gl.viewport(0,0,w,h);
    gl.useProgram(P1);
    gl.uniform2f(u1.uResolution,w,h);
    gl.uniform1f(u1.uMorph,mix);
    gl.uniform1i(u1.uShapeA,A);gl.uniform1i(u1.uShapeB,B);
    gl.uniform2f(u1.uCamera,yaw,pitch);
    gl.uniform1f(u1.uZoom,s.zoom);
    gl.drawArrays(gl.TRIANGLES,0,3);

    gl.bindFramebuffer(gl.FRAMEBUFFER,null);
    gl.viewport(0,TH-h,w,h);
    gl.useProgram(P2);
    gl.activeTexture(gl.TEXTURE0);gl.bindTexture(gl.TEXTURE_2D,sceneTex);gl.uniform1i(u2.uScene,0);
    gl.activeTexture(gl.TEXTURE1);gl.bindTexture(gl.TEXTURE_2D,maskTex);gl.uniform1i(u2.uMask,1);
    gl.uniform2f(u2.uOffset,0,TH-h);
    gl.uniform2i(u2.uSize,w,h);
    gl.uniform1i(u2.uBayerSize,s.bayer);
    gl.uniform1i(u2.uOutlineWidth,s.outline);
    gl.uniform3f(u2.uBG,bg[0]/255,bg[1]/255,bg[2]/255);
    gl.uniform3f(u2.uInk,ink[0]/255,ink[1]/255,ink[2]/255);
    gl.uniform3f(u2.uLight,light[0]/255,light[1]/255,light[2]/255);
    gl.drawArrays(gl.TRIANGLES,0,3);

    m.ctx.drawImage(glc,0,0,w,h,0,0,w,h);
  };
}

let draw=null;
try{ if(gl) draw=initGL(); }catch(e){ console.error(e); draw=null; }
if(!draw) document.documentElement.classList.add('no-gl');

const byEl=new WeakMap();
const ro=new ResizeObserver(es=>es.forEach(e=>{
  const m=byEl.get(e.target); if(!m) return;
  const r=e.contentRect;
  m.w=Math.max(0,Math.round(r.width*m.scale)); m.h=Math.max(0,Math.round(r.height*m.scale));
  m.c.width=Math.max(1,m.w); m.c.height=Math.max(1,m.h); m.dirty=true;
}));
const vis=new IntersectionObserver(es=>es.forEach(e=>{const m=byEl.get(e.target); if(m){m.visible=e.isIntersecting; m.dirty=true;}}),{rootMargin:'120px 0px'});

document.querySelectorAll('[data-art]').forEach(el=>{
  const spec=SPEC[el.dataset.art]; if(!spec) return;
  el.style.backgroundColor=rgb(PAL[spec.pal][0]);
  if(!draw) return;
  const c=document.createElement('canvas'); el.appendChild(c);
  const ctx=c.getContext('2d'); ctx.imageSmoothingEnabled=false;
  const m={el,c,ctx,spec,scale:el.classList.contains('thumb')?1:.5,w:0,h:0,visible:false,
    gate:el.closest('.row,.band'),t0:Math.random()*spec.every,px:0,py:0,tx:0,ty:0,idx:0,dirty:true};
  if(el.dataset.art==='flash') flashMod=m;
  const host=el.closest('a,.portrait,.hero-img')||el;
  host.addEventListener('pointermove',e=>{const r=host.getBoundingClientRect();m.tx=(e.clientX-r.left)/r.width-.5;m.ty=(e.clientY-r.top)/r.height-.5;m.dirty=true;});
  host.addEventListener('pointerleave',()=>{m.tx=0;m.ty=0;m.dirty=true;});
  byEl.set(el,m); mods.push(m); ro.observe(el); vis.observe(el);
});

if(draw){
  const frame=now=>{
    const t=now/1000;
    for(const m of mods){
      if(!m.visible||m.w<2||m.h<2) continue;
      if(m.gate&&!m.gate.matches(':hover')) continue;
      const settling=Math.abs(m.tx-m.px)+Math.abs(m.ty-m.py)>.002;
      if(reduce&&!m.dirty&&!settling) continue;
      draw(m,t); m.dirty=false;
    }
    requestAnimationFrame(frame);
  };
  requestAnimationFrame(frame);
}

/* ---------- fit text ---------- */
function fit(){
  document.querySelectorAll('.fit').forEach(el=>{
    const s=el.firstElementChild; s.style.fontSize='100px';
    const w=s.getBoundingClientRect().width;
    if(w) s.style.fontSize=(100*el.clientWidth/w).toFixed(2)+'px';
  });
}
fit(); if(document.fonts) document.fonts.ready.then(fit);
let rt; addEventListener('resize',()=>{clearTimeout(rt);rt=setTimeout(fit,80);});

/* ---------- reveal on scroll ---------- */
const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target);}}),{rootMargin:'0px 0px -8% 0px'});
document.querySelectorAll('[data-reveal]').forEach(el=>io.observe(el));
requestAnimationFrame(()=>document.body.classList.add('loaded'));

/* ---------- hero parallax + marquee ---------- */
const hero=document.getElementById('heroArt');
const track=document.getElementById('track');
function tick(t){
  const y=scrollY;
  hero.style.transform=`translate3d(0,${Math.min(y*.08,60).toFixed(1)}px,0)`;
  const w=track.firstElementChild.offsetWidth||1;
  const x=((reduce?0:t*.04)+y*.6)%w;
  track.style.transform=`translate3d(${-x}px,0,0)`;
  requestAnimationFrame(tick);
}
requestAnimationFrame(tick);

/* ---------- "view all" band: flash through the plates ---------- */
const band=document.getElementById('band'); let ft;
band.addEventListener('mouseenter',()=>{
  if(innerWidth<1200||!flashMod) return;
  ft=setInterval(()=>{
    flashMod.idx++;
    flashMod.el.style.backgroundColor=rgb(PAL[FLASH[flashMod.idx%FLASH.length].pal][0]);
    flashMod.dirty=true;
  },140);
});
band.addEventListener('mouseleave',()=>clearInterval(ft));

/* ---------- phone menu ---------- */
const mb=document.querySelector('.menu-btn'), mm=document.querySelector('.mmenu');
const setMenu=o=>{document.body.classList.toggle('menu-open',o);mb.setAttribute('aria-expanded',o);mm.setAttribute('aria-hidden',!o);};
mb.addEventListener('click',()=>setMenu(!document.body.classList.contains('menu-open')));
mm.querySelectorAll('a').forEach(a=>a.addEventListener('click',()=>setMenu(false)));
addEventListener('resize',()=>{if(innerWidth>=810)setMenu(false);});
})();
</script>
</body>
</html>
```

