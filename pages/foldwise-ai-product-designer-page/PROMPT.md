INSTALANDING.AI · Foldwise AI Product Designer Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Foldwise AI Product Designer Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/foldwise-ai-product-designer-page

foldwise-ai-product-designer.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Foldwise AI Product Designer Page
  slug     foldwise-ai-product-designer-page
  prompt   https://instalanding.ai/p/foldwise-ai-product-designer-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/foldwise-ai-product-designer-page
  license  Fictional brand ("Foldwise"), with fictional clients ("Tessel", "Kompas"); every case study, vendor, figure
           and note is invented, and the address uses the reserved .example domain. Replace before shipping.
           Every picture is inline SVG drawn by the script; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --canvas #e2e4e7, --paper #f9fafb, --stock #232427 (dark
            panels), --board #1b1c1f (the contact card), --ink #1e2024 with soft/table tints, reversed inks for dark
            panels; Familjen Grotesk 400-700 for everything
  sections  nav (the fixed bar), menu (the phone drawer), fold (a leporello of 12 panels: cover, contents, seven case
            studies, field notes, about, contact; each panel carries data-section)
  scripts   one IIFE: WORKS and NOTES data, tiny SVG helpers (T text, R rect, L line, win, phone) and seven ART
            plates; the panels are built into .lp-track, then render() folds them on scroll: panel i opens as
            progress passes i, alternating fold direction, with shading from the fold angle, and the track is
            shifted so the opening crease stays centred. Contents paging, a copy-to-clipboard address with a live
            Amsterdam clock, and the phone drawer.
  assets    no image files; Familjen Grotesk from Google Fonts; no libraries

  ADAPTING
  - Content lives in WORKS (id, title, line, client, year, art key, dark) and NOTES; each art key is a function in
    ART that returns one 400x300 SVG plate. Add a case study by adding both.
  - The strip is (N - 1) x 62% of a screen tall per panel; change the 0.62 in setup() for a slower or faster unfold.
  - Panels are drawn at 440x600 and scaled by --k so the whole book fits the window.
  - Under 810px the book lies flat as a vertical stack; under prefers-reduced-motion it lies flat as a sideways
    snap scroller, with the SVG animations paused.
  - Arrow keys step panel by panel on desktop; a case-study panel opens with a click, Enter or Space.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Foldwise, the AI-native senior product designer</title>
<meta name="description" content="Foldwise is an AI-native senior product designer, as an app. Case studies and notes on agents, trust, and designing with models in the loop.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Familjen+Grotesk:ital,wght@0,400..700;1,400..700&display=swap" rel="stylesheet">
<style>
:root{
  --canvas:#e2e4e7;--canvas-lit:#eeeff1;--paper:#f9fafb;--stock:#232427;--board:#1b1c1f;
  --ink:#1e2024;--ink-soft:#5b5f67;--ink-table:#52565e;--ink-rev:#f2f3f5;--ink-rev-soft:#a7abb2;
  --plate-light:#eceef1;--plate-dark:#151619;--sc:35,42,51;--hi:255,255,255;
  --font:"Familjen Grotesk","Helvetica Neue",Helvetica,Arial,sans-serif;
}
*{box-sizing:border-box}
html,body{margin:0;padding:0;background:var(--canvas)}
body{font-family:var(--font);color:var(--ink);-webkit-font-smoothing:antialiased;-moz-osx-font-smoothing:grayscale;font-feature-settings:"cv03","cv04","cv09","cv11"}
::selection{background:var(--ink);color:var(--paper)}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:0;padding:0;cursor:pointer}

/* top bar */
.bar{position:fixed;top:0;left:0;right:0;height:76px;padding:0 64px;display:flex;align-items:center;justify-content:space-between;z-index:30;pointer-events:none}
.bar>*{pointer-events:auto}
.bar .name{font-size:15px;font-weight:600;letter-spacing:-.01em}
.bar nav{display:flex;gap:28px;font-size:15px}
.menu-btn{display:none;height:40px;align-items:center;font-size:15px;font-weight:500}
.ul{position:relative}
.ul::after{content:"";position:absolute;left:0;right:0;bottom:-3px;height:1px;background:currentColor;transform:scaleX(0);transform-origin:0 50%;transition:transform .35s cubic-bezier(.2,.7,.2,1)}
.ul:hover::after{transform:scaleX(1)}
@media (max-width:1199.98px){.bar{padding:0 32px}.bar nav{gap:18px}}
@media (max-width:809.98px){.bar{height:56px;padding:0 16px;background:rgba(226,228,231,.86);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px)}.bar nav{display:none}.menu-btn{display:flex}}

/* mobile drawer */
.scrim{position:fixed;inset:0;background:rgba(35,31,32,.12);z-index:40;opacity:0;pointer-events:none;transition:opacity .3s}
.drawer{position:fixed;top:0;bottom:0;left:0;width:100%;background:var(--paper);z-index:41;padding:8px 16px 24px;display:flex;flex-direction:column;transform:translateY(-100%);transition:transform .45s cubic-bezier(.2,.72,.1,1),visibility 0s .45s;visibility:hidden;box-shadow:0 20px 40px -24px rgba(35,42,51,.4)}
.menu-open .scrim{opacity:1;pointer-events:auto}
.menu-open .drawer{transform:none;visibility:visible;transition-delay:0s}
.drawer .top{display:flex;justify-content:space-between;align-items:center;height:40px;font-size:15px}
.drawer .top b{font-weight:600}
.drawer .links{padding-top:28px;display:flex;flex-direction:column}
.drawer .links button{font-size:31px;font-weight:600;letter-spacing:-.028em;padding:4px 0;text-align:left}
.drawer .bottom{margin-top:auto;border-top:1px solid rgba(30,32,36,.14);padding-top:16px;display:flex;justify-content:space-between;font-size:14.5px}

/* leporello */
.lp{position:relative;width:100%;--margin:64px;--k:1;--pw:440px;--ph:600px;--dw:440px;--dh:600px}
.lp *{box-sizing:border-box;margin:0;padding:0}
.lp ul{list-style:none}
.lp :focus-visible{outline:2px solid var(--ink);outline-offset:4px}
.lp .lp-dark :focus-visible{outline-color:var(--ink-rev)}
.lp-lnk{position:relative;font-weight:500;cursor:pointer}
.lp-lnk::after,.lp-furn a::after{content:"";position:absolute;left:0;right:0;bottom:-3px;height:1px;background:currentColor;transform:scaleX(0);transform-origin:0 50%;transition:transform .35s cubic-bezier(.2,.7,.2,1)}
.lp-lnk:hover::after,.lp-furn a:hover::after{transform:scaleX(1)}
@media (max-width:960px){.lp{--margin:32px}}

.lp-strip{position:relative}
.lp-stage{position:sticky;top:0;height:100vh;height:100svh;overflow:hidden;perspective:2400px;perspective-origin:50% 48%;
  background:radial-gradient(150% 120% at 50% -16%,var(--canvas-lit) 0%,var(--canvas) 74%)}
.lp-track{position:absolute;left:0;top:50%;height:var(--ph);margin-top:calc(var(--ph) / -2 + 6px);transform-style:preserve-3d}
.lp:not(.lp-ready) .lp-track{visibility:hidden}
.lp-panel{position:absolute;left:0;top:0;display:block;width:var(--pw);height:var(--ph);transform-origin:0 50%;transform-style:preserve-3d;background:var(--paper);color:var(--ink);will-change:transform;cursor:default;overflow:hidden}
.lp-panel.lp-dark{background:var(--stock);color:var(--ink-rev)}
.lp-panel.lp-contact{background:var(--board)}
.lp-panel.lp-work{cursor:pointer}
.lp-pg{position:absolute;left:0;top:0;width:var(--dw);height:var(--dh);transform:scale(var(--k));transform-origin:0 0;display:flex;flex-direction:column;padding:20px}
.lp-shade{position:absolute;inset:0;pointer-events:none;
  background:
    linear-gradient(180deg,rgba(var(--hi),var(--rim,0)) 0,rgba(var(--hi),0) 2px),
    linear-gradient(0deg,rgba(var(--sc),var(--gnd,0)) 0,rgba(var(--sc),0) 46%),
    linear-gradient(rgba(var(--sc),var(--pt,0)),rgba(var(--sc),var(--pt,0))),
    linear-gradient(rgba(var(--sc),var(--sh,0)),rgba(var(--sc),var(--sh,0)))}
.lp-panel{--gnd:.1}
.lp-panel.lp-dark{--gnd:.16;--rim:.35}
.lp-track>.lp-panel:nth-child(even){--pt:.045}
.lp-track>.lp-panel.lp-dark:nth-child(even){--pt:.12}

.lp-cover .lp-pg{padding:26px 26px 24px}
.lp-cover h1{font-size:80px;line-height:.9;font-weight:700;letter-spacing:-.045em;margin-left:-4px;text-wrap:balance}
.lp-cover .lp-role{font-size:21px;line-height:1.22;font-weight:500;letter-spacing:-.012em;margin-top:26px;max-width:15em}
.lp-cover .lp-foot{margin-top:auto;display:flex;flex-direction:column;gap:18px}
.lp-cover .lp-lede{font-size:15px;line-height:1.45;color:var(--ink-soft);max-width:25em}
.lp-cover .lp-city{font-size:15px;font-weight:500}

.lp-plate{position:relative;height:318px;flex:none;background:var(--plate-light);overflow:hidden}
.lp-dark .lp-plate{background:var(--plate-dark)}
.lp-plate svg{position:absolute;inset:0;width:100%;height:100%;display:block;font-family:var(--font);font-variant-numeric:tabular-nums;transition:transform .6s cubic-bezier(.2,.7,.2,1)}
.lp-work:hover .lp-plate svg{transform:scale(1.025)}
.lp-cap{margin-top:24px;display:flex;flex-direction:column;flex:1;padding:0 6px}
.lp-cap h3{font-size:31px;line-height:1.02;font-weight:600;letter-spacing:-.028em}
.lp-cap p{font-size:15px;line-height:1.42;margin-top:12px;color:var(--ink-soft);max-width:24em}
.lp-dark .lp-cap p{color:var(--ink-rev-soft)}
.lp-cap .lp-meta{margin-top:auto;display:flex;justify-content:space-between;gap:12px;font-size:14px;font-variant-numeric:tabular-nums}
.lp-cap .lp-meta span:last-child{color:var(--ink-soft)}
.lp-dark .lp-cap .lp-meta span:last-child{color:var(--ink-rev-soft)}
.lp-sticker{position:absolute;left:14px;top:14px;z-index:2;background:var(--paper);color:var(--ink);font-size:12px;font-weight:500;padding:5px 8px 4px;border:1px solid var(--ink)}

.lp-index .lp-pg,.lp-notes .lp-pg,.lp-about .lp-pg{padding:26px}
.lp-iview{flex:1;min-height:0;overflow:hidden;margin-top:22px;border-bottom:1px solid rgba(242,243,245,.16)}
.lp-ilist{display:flex;flex-direction:column;transition:transform .55s cubic-bezier(.2,.7,.2,1)}
.lp-ilist li{border-top:1px solid rgba(242,243,245,.16)}
.lp-ilist a{display:grid;grid-template-columns:30px 1fr auto 40px;column-gap:12px;align-items:center;width:100%;height:42px;cursor:pointer}
.lp-ilist span{font-size:13px;color:var(--ink-rev-soft);font-variant-numeric:tabular-nums}
.lp-ilist span:last-child{text-align:right}
.lp-ilist b{font-size:18px;line-height:1.15;font-weight:600;letter-spacing:-.012em;transition:transform .35s cubic-bezier(.2,.7,.2,1);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.lp-ilist a:hover b{transform:translateX(6px)}
.lp-ifoot{display:flex;align-items:center;margin-top:auto;padding-top:14px;font-size:15px}
.lp-inav{margin-left:auto;display:flex;align-items:center;gap:8px;font-size:13px;color:var(--ink-rev-soft);font-variant-numeric:tabular-nums}
.lp-inav[hidden]{display:none}
.lp-arr{position:relative;width:32px;height:32px;border-radius:50%;border:1px solid rgba(242,243,245,.4);color:var(--ink-rev);display:grid;place-items:center;font-size:14px;transition:background .2s,opacity .2s}
.lp-arr:hover:not(:disabled){background:rgba(242,243,245,.12)}
.lp-arr:disabled{opacity:.3;cursor:default}

.lp-head{display:flex;justify-content:space-between;align-items:baseline;gap:12px}
.lp-head h2{font-size:31px;line-height:1;font-weight:600;letter-spacing:-.028em}
.lp-head span{font-size:13px;color:var(--ink-soft)}
.lp-dark .lp-head span{color:var(--ink-rev-soft)}
.lp-nlist{margin-top:26px;display:flex;flex-direction:column}
.lp-nlist li{padding:16px 0 17px;border-top:1px solid rgba(30,32,36,.14)}
.lp-nmeta{display:flex;justify-content:space-between;font-size:13px;color:var(--ink-soft);font-variant-numeric:tabular-nums}
.lp-nlist h4{font-size:20px;line-height:1.14;font-weight:600;letter-spacing:-.016em;margin-top:8px}
.lp-nlist p{font-size:14.5px;line-height:1.42;color:var(--ink-soft);margin-top:6px}
.lp-bio{font-size:19px;line-height:1.36;font-weight:450;letter-spacing:-.008em;margin-top:26px}
.lp-exp{margin-top:28px;font-size:14px;line-height:1.3}
.lp-exp li{display:grid;grid-template-columns:96px 1fr;column-gap:12px;padding:10px 0;border-top:1px solid rgba(242,243,245,.16)}
.lp-exp li span:first-child{grid-row:span 2;color:var(--ink-rev-soft);font-variant-numeric:tabular-nums}
.lp-exp b{font-weight:500}
.lp-exp li span:last-child{color:var(--ink-rev-soft)}
.lp-pgfoot{margin-top:auto;display:flex;gap:24px;font-size:15px}

/* contact card (the back of the book) */
.lp-contact .lp-pg{padding:28px;color:var(--ink-rev)}
.lp-contact::before{content:"";position:absolute;inset:0;pointer-events:none;background:linear-gradient(135deg,rgba(255,255,255,.05),rgba(255,255,255,0) 40%),radial-gradient(90% 70% at 30% 20%,rgba(255,255,255,.035),rgba(0,0,0,0))}
.lp-bc-top{display:flex;justify-content:space-between;font-size:13px;color:var(--ink-rev-soft);font-variant-numeric:tabular-nums}
.lp-bc-top b{font-weight:500;color:var(--ink-rev)}
.lp-bc-line{font-size:16px;line-height:1.42;color:var(--ink-rev-soft);margin-top:28px;max-width:22em}
.lp-mail{display:block;margin-top:auto;font-weight:600;letter-spacing:-.035em;line-height:.98;color:var(--ink-rev);font-size:40px;width:100%;text-align:left}
.lp-mail span{display:block;white-space:nowrap}
.lp-mail .lp-l2{position:relative;display:inline-block}
.lp-mail .lp-l2::after{content:"";position:absolute;left:0;right:0;bottom:-6px;height:2px;background:currentColor;transform:scaleX(0);transform-origin:0 50%;transition:transform .45s cubic-bezier(.2,.7,.2,1)}
.lp-mail:hover .lp-l2::after,.lp-mail:focus-visible .lp-l2::after{transform:scaleX(1)}
.lp-bc-state{display:flex;gap:18px;align-items:baseline;margin-top:18px;font-size:13px;color:var(--ink-rev-soft)}
.lp-bc-state .lp-ok{color:var(--ink-rev)}
.lp-bc-state a{color:var(--ink-rev)}
.lp-bc-links{display:flex;gap:22px;margin-top:28px;font-size:15px;flex-wrap:wrap}
.lp-bc-foot{margin-top:auto;display:flex;justify-content:space-between;align-items:flex-end;gap:16px}
.lp-bc-code{display:flex;align-items:flex-end;gap:12px;font-size:11.5px;line-height:1.3;color:var(--ink-rev-soft)}
.lp-bc-code svg{display:block;width:88px;height:88px;background:#F9FAFB;padding:6px}
.lp-bc-colo{display:flex;flex-direction:column;gap:4px;text-align:right;font-size:12px;color:var(--ink-rev-soft)}
.lp-bc-colo span:last-child{display:flex;gap:10px;justify-content:flex-end}
.lp .lp-m{display:none}

.lp-furn{position:absolute;left:var(--margin);right:var(--margin);bottom:30px;display:flex;justify-content:space-between;align-items:baseline;font-size:15px;z-index:5;pointer-events:none;color:var(--ink)}
.lp-furn>*{pointer-events:auto}
.lp-furn .lp-label{font-weight:500}
.lp-furn .lp-legal{display:flex;gap:14px;font-size:13px;color:var(--ink-table)}
.lp-furn a{position:relative}
.lp-furn .lp-hint{position:absolute;left:50%;transform:translateX(-50%);color:var(--ink-table);font-size:13px;white-space:nowrap;transition:opacity .3s}

/* flat fallbacks: phones, and reduced motion */
.lp-flat .lp-strip{height:auto!important}
.lp-flat .lp-stage{position:relative;height:auto;perspective:none}
.lp-flat .lp-track{position:relative;top:auto;margin:0;height:auto;display:flex;transform-style:flat}
.lp-flat .lp-panel{position:relative;transform:none!important;flex:none}
.lp-flat .lp-shade{display:none}
.lp-flat .lp-furn{display:none}
.lp-flat:not(.lp-v) .lp-stage{overflow-x:auto;overflow-y:hidden;padding:120px 0 110px;scroll-snap-type:x mandatory;scroll-padding-inline:var(--margin)}
.lp-flat:not(.lp-v) .lp-track{width:max-content;padding:0 var(--margin)}
.lp-flat:not(.lp-v) .lp-panel{scroll-snap-align:start}
.lp-v{--margin:16px}
.lp-v .lp-stage{overflow:visible;padding:72px 0 40px;background:linear-gradient(180deg,var(--canvas-lit) 0%,var(--canvas) 62%)}
.lp-v .lp-track{flex-direction:column;align-items:center;gap:14px}
.lp-v .lp-m{display:inline}
.lp-v .lp-d{display:none}
.lp-v .lp-bc-code{display:none}
.lp-v .lp-mail{font-size:33px}
.lp-v .lp-bc-foot{justify-content:flex-end}
@media (prefers-reduced-motion:reduce){*,*::before,*::after{transition-duration:.01ms!important;animation-duration:.01ms!important}}
</style>
</head>
<body>

<header class="bar" data-section="nav">
  <a class="name ul" href="#" data-go="cover">Foldwise</a>
  <nav>
    <a class="ul" href="#" data-go="index">Work</a>
    <a class="ul" href="#" data-go="notes">Notes</a>
    <a class="ul" href="#" data-go="about">About</a>
    <a class="ul" href="#" data-go="contact">Request access</a>
  </nav>
  <button class="menu-btn" type="button" aria-expanded="false" aria-controls="drawer">Menu</button>
</header>

<div class="scrim" aria-hidden="true"></div>
<div class="drawer" id="drawer" aria-hidden="true" data-section="menu">
  <div class="top"><b>Foldwise</b><button type="button" class="menu-close">Close</button></div>
  <div class="links">
    <button data-go="index">Work</button>
    <button data-go="notes">Notes</button>
    <button data-go="about">About</button>
    <button data-go="contact">Request access</button>
  </div>
  <div class="bottom"><span>Private beta</span><a href="mailto:hello@foldwise.example">hello@foldwise.example</a></div>
</div>

<main class="lp" id="lp">
  <section class="lp-strip" aria-label="Selected work" data-section="fold">
    <div class="lp-stage">
      <div class="lp-track"></div>
      <div class="lp-furn">
        <span class="lp-label">Designed with Foldwise</span>
        <span class="lp-hint" aria-live="polite"></span>
        <span class="lp-legal"><a href="#">Privacy</a><a href="#">Cookies</a></span>
      </div>
    </div>
  </section>
</main>

<script>
(() => {
/* ---------- content ---------- */
const WORKS = [
  {id:"agent-runs", t:"Agent runs", d:"What is the agent doing, and how sure is it? A run page that answers both while the work is still happening.", c:"Tessel", y:"2025", art:"run"},
  {id:"approval-queue", t:"Approval queue", d:"An internal tool for approving what the agents aren't sure about, on one screen.", c:"Tessel", y:"2026", art:"approvals", dark:true},
  {id:"model-routing", t:"Model routing", d:"An assistant that picks the smallest model that does the job well, and says why.", c:"Kompas", y:"2022", art:"routing"},
  {id:"autonomy-dial", t:"Autonomy dial", d:"Move a task from ask-first to act-alone without losing track of what changed.", c:"Tessel", y:"2025", art:"autonomy"},
  {id:"signal-design-system", t:"Signal design system", d:"One design system for how AI behaves on screen, from thinking to unsure to done, across three products.", c:"Kompas", y:"2023", art:"signal"},
  {id:"context-window", t:"Context window", d:"Drag across a conversation to choose what the model remembers.", c:"Kompas", y:"2024", art:"context"},
  {id:"undo-for-agents", t:"Undo for agents", d:"When an agent removes something, it leaves a gap. Click the gap to bring it back.", c:"Tessel", y:"2026", art:"undo"}
];
const NOTES = [
  {tag:"Trust", date:"23 Jun 2026", t:"Answers that aren't certain yet", d:"Why our agents describe confidence in words, and what a screen should say while the model is still working."},
  {tag:"Interaction", date:"2 Apr 2026", t:"Show the work, not the spinner", d:"A spinner tells you nothing. A list of steps tells you what to check and where to step in."},
  {tag:"Process", date:"14 Jan 2026", t:"What I check before shipping an AI feature", d:"The list I go through before a model-backed design goes to engineering. Most of it is about the answers nobody drew."}
];

/* ---------- tiny SVG helpers ---------- */
const VIOLET="#7064d6", INK="#1e2024", GREY="#7d828b", SOFT="#5b5f67", LINE="#e3e5e9", GREEN="#2f9e6b", AMBER="#d9962b", RED="#d2493f";
const T=(x,y,s,o={})=>`<text x="${x}" y="${y}" font-size="${o.s||8}" fill="${o.f||INK}" font-weight="${o.w||400}" text-anchor="${o.a||"start"}"${o.ls!=null?` letter-spacing="${o.ls}"`:""}${o.fl?` filter="url(#${o.fl})"`:""}${o.op!=null?` opacity="${o.op}"`:""}>${s}</text>`;
const R=(x,y,w,h,f,o={})=>`<rect x="${x}" y="${y}" width="${w}" height="${h}" rx="${o.r||0}" fill="${f}"${o.st?` stroke="${o.st}" stroke-width="${o.sw||1}"`:""}${o.da?` stroke-dasharray="${o.da}"`:""}${o.op!=null?` opacity="${o.op}"`:""}/>`;
const L=(x1,y1,x2,y2,c,w=1,da)=>`<line x1="${x1}" y1="${y1}" x2="${x2}" y2="${y2}" stroke="${c}" stroke-width="${w}"${da?` stroke-dasharray="${da}"`:""}/>`;
const CURSOR=(x,y)=>`<path transform="translate(${x},${y})" d="M0 0L0 13.5L3.6 10.2L6.2 15.6L8.4 14.6L5.8 9.4L10.4 9.4Z" fill="${INK}" stroke="#fff" stroke-width="1" stroke-linejoin="round"/>`;
let uid=0;
function svg(body,dark){
  const id="s"+(++uid);
  return {id, open:`<svg viewBox="0 0 400 300" preserveAspectRatio="xMidYMid slice" aria-hidden="true"><defs>
    <filter id="${id}" x="-15%" y="-15%" width="130%" height="140%"><feDropShadow dx="0" dy="8" stdDeviation="9" flood-color="#232a33" flood-opacity="${dark?.55:.16}"/></filter>
    <filter id="${id}b"><feGaussianBlur stdDeviation="1.7"/></filter></defs>`, close:"</svg>"};
}
function win(x,y,w,h,dark,title,fid){
  const bg=dark?"#1f2125":"#fff", bar=dark?"#26282d":"#f6f7f9", bd=dark?"#30333a":"#d9dce1", tc=dark?"#7d828b":"#8b9098";
  return `<g filter="url(#${fid})">${R(x,y,w,h,bg,{r:8,st:bd})}</g>
    <path d="M${x+.5} ${y+18.5}V${y+8}a7.5 7.5 0 0 1 7.5-7.5H${x+w-8}a7.5 7.5 0 0 1 7.5 7.5V${y+18.5}Z" fill="${bar}"/>
    ${L(x+.5,y+18.5,x+w-.5,y+18.5,bd)}
    <circle cx="${x+10}" cy="${y+9.5}" r="2.6" fill="${dark?"#43464d":"#d5d8dd"}"/><circle cx="${x+18}" cy="${y+9.5}" r="2.6" fill="${dark?"#43464d":"#d5d8dd"}"/><circle cx="${x+26}" cy="${y+9.5}" r="2.6" fill="${dark?"#43464d":"#d5d8dd"}"/>
    ${T(x+w/2,y+12,title,{s:6,f:tc,a:"middle"})}`;
}
function phone(x,y,w,h,fid){
  return `<g filter="url(#${fid})">${R(x,y,w,h,"#1e2024",{r:20})}</g>${R(x+5,y+5,w-10,h-10,"#fff",{r:15.5})}${R(x+w/2-16,y+9,32,7,"#1e2024",{r:3.5})}`;
}
const PRICES=[9,8,7,6,6,7,10,16,22,20,15,12,11,10,11,13,17,24,28,25,19,15,12,10];
function priceCol(v){
  const t=(v-6)/22, a=[47,158,107], b=[217,150,43], c=[210,73,63];
  const mix=(p,q,u)=>p.map((n,i)=>Math.round(n+(q[i]-n)*u));
  const m=t<.5?mix(a,b,t*2):mix(b,c,(t-.5)*2);
  return `rgb(${m.join(",")})`;
}

/* ---------- the seven plates ---------- */
const ART = {
run(){
  const s=svg(); let b=win(28,22,344,262,false,"Tessel — Agent runs",s.id);
  b+=R(28.5,40.5,74,243,"#f6f7f9",{r:0});
  b+=T(38,56,"Tessel",{s:8,w:700,ls:-.2});
  ["Home","Agents","Runs","Approvals","Evals"].forEach((n,i)=>{
    const y=72+i*14; if(i===2) b+=R(33,y-9,64,13,"#e6e8ec",{r:3});
    b+=T(38,y,n,{s:6.5,f:i===2?INK:SOFT,w:i===2?600:400});
  });
  b+=T(114,60,"Run #4821 · Month-end close",{s:11,w:600,ls:-.3});
  b+=T(114,72,"Reconciling 1,284 invoices against the ledger",{s:6.3,f:SOFT});
  b+=L(135,96,240,96,INK,1.4)+L(240,96,340,96,"#b7bbc2",1.4,"3 3");
  b+=`<circle cx="135" cy="96" r="4" fill="${INK}"/>`;
  b+=`<circle cx="240" cy="96" r="4" fill="none" stroke="${VIOLET}" stroke-width="1.2"><animate attributeName="r" values="4;10" dur="1.8s" repeatCount="indefinite"/><animate attributeName="opacity" values=".9;0" dur="1.8s" repeatCount="indefinite"/></circle><circle cx="240" cy="96" r="4" fill="${VIOLET}"/>`;
  b+=`<circle cx="340" cy="96" r="3.6" fill="#fff" stroke="#9ca1a9" stroke-width="1.2"/>`;
  [[135,"Read ledger","312 entries","00:42"],[240,"Matching","1,104 of 1,284","now"],[340,"Draft report","queued","next"]].forEach(([x,a,m,d])=>{
    b+=T(x,113,a,{s:6.5,w:600,a:"middle"})+T(x,122,m,{s:6.2,f:SOFT,a:"middle"})+T(x,130.5,d,{s:5.8,f:GREY,a:"middle"});
  });
  let d="M150 144H320V266"; for(let x=320;x>150;x-=10) d+=`L${x-5} 272L${x-10} 266`; d+="Z";
  b+=`<g filter="url(#${s.id})"><path d="${d}" fill="#fff" stroke="#dcdfe3"/></g>`;
  b+=`<path d="M233 144L240 137L247 144Z" fill="#fff"/>`;
  b+=T(162,161,"Run so far",{s:7,w:600})+T(308,161,"Working",{s:6,f:VIOLET,a:"end",w:500});
  [["Tool calls","1,926"],["Matched on its own","1,104"],["Sent to you to check","38"]].forEach(([k,v],i)=>{
    const y=180+i*13; b+=T(162,y,k,{s:6.3,f:SOFT})+T(308,y,v,{s:6.3,a:"end"});
  });
  b+=L(162,214,308,214,"#c9cdd3",.8,"2 2");
  b+=T(162,229,"Confidence",{s:8,w:600})+T(308,229,"High",{s:8,w:700,a:"end"});
  b+=T(162,246,"Model · tessel-fin-2",{s:5.8,f:GREY})+T(308,246,"Cost so far €3.12",{s:5.8,f:GREY,a:"end"});
  return s.open+b+s.close;
},
approvals(){
  const s=svg("",true); const lt="#f2f3f5", sf="#a7abb2";
  let b=win(28,22,344,262,true,"Approval queue",s.id);
  b+=T(44,60,"Approval queue",{s:12,w:600,f:lt,ls:-.3})+T(356,60,"24 waiting",{s:7,f:sf,a:"end"});
  [["All",true],["Low confidence",false],["Over €1,000",false]].forEach(([n,on],i)=>{
    const x=[44,68,127][i], w=n.length*3.4+12;
    b+=R(x,68,w,13,on?"#f2f3f5":"none",{r:6.5,st:on?null:"#3a3d44"})+T(x+w/2,77,n,{s:6,f:on?INK:sf,a:"middle",w:500});
  });
  b+=T(44,98,"Sure",{s:5.8,f:GREY})+T(84,98,"Vendor",{s:5.8,f:GREY})+T(176,98,"Agent wants to",{s:5.8,f:GREY})+T(356,98,"Amount",{s:5.8,f:GREY,a:"end"});
  const rows=[[RED,41,"Studio Verde","Pay invoice","€2,480.00"],[RED,52,"Noordlicht BV","Refund","€960.50"],[AMBER,63,"Kade &amp; Co","Write off","€312.00"],[AMBER,68,"Hollands Glas","Pay invoice","€1,145.90"],[AMBER,74,"Atelier Mos","Merge duplicate","€86.40"],["#6e737b",88,"Fietsplaats","Pay invoice","€44.00"],["#6e737b",91,"Bakkerij Om","Recode expense","€19.95"],["#6e737b",96,"Velt Studio","Pay invoice","€230.00"]];
  rows.forEach(([c,sc,n,act,a],i)=>{
    const y=103+i*21;
    b+=L(36,y,364,y,"#2c2f35");
    if(i===1) b+=R(36,y+.5,328,20.5,"#2a2d33")+R(36,y+.5,2.5,20.5,lt);
    b+=`<circle cx="48" cy="${y+10.5}" r="3" fill="${c}"/>`;
    b+=T(57,y+13,sc+"%",{s:6.5,f:lt,w:500});
    b+=T(84,y+13,n,{s:7,f:"#d9dbdf",fl:s.id+"b"});
    b+=T(176,y+13,act,{s:6.3,f:"#c4c7cd"});
    b+=T(356,y+13,a,{s:6.8,f:lt,a:"end",w:500});
  });
  b+=R(258,y0(1)+4,40,13,"#f2f3f5",{r:6.5})+T(278,y0(1)+12.6,"Approve",{s:5.8,f:INK,a:"middle",w:600});
  return s.open+b+s.close;
  function y0(i){return 103+i*21;}
},
routing(){
  const s=svg(); let b="";
  b+=phone(70,22,122,256,s.id);
  b+=T(85,52,"Summarise this thread",{s:6.2,f:GREY})+T(85,67,"Best model",{s:11,w:600,ls:-.3})+T(85,80,"for the job",{s:11,w:600,ls:-.3});
  b+=R(83,90,96,78,"#efedfd",{r:8});
  b+=T(91,107,"Small model",{s:10,w:700,ls:-.2})+T(91,119,"92% as good · ⅛ the cost",{s:6.2,f:"#5b4fc4"});
  const Q=[40,52,61,68,74,79,83,86,88,90,91,92,92,93,93,94,94,94,95,95,95,95,96,96];
  Q.forEach((v,i)=>{const h=2+(v-36)*.4; b+=R(91+i*3.5,160-h,2.6,h,i===11?VIOLET:"#cfcbee",{r:1});});
  [["Summarise","Small"],["Draft reply","Medium"],["Reconcile","Large"]].forEach(([k,v],i)=>{
    const y=186+i*18; b+=T(85,y,k,{s:6.5,w:500})+T(177,y,v,{s:6.2,f:SOFT,a:"end"})+L(85,y+6,177,y+6,LINE);
  });
  b+=R(83,246,96,17,INK,{r:8.5})+T(131,257,"Use for similar tasks",{s:6.3,f:"#fff",a:"middle",w:500});
  b+=phone(208,22,122,256,s.id);
  b+=T(223,52,"Today",{s:6.2,f:GREY})+T(223,67,"Cost per task",{s:11,w:600,ls:-.3});
  const tasks=[["Inbox",4,0],["Notes",3,0],["Recap",5,0],["Tag",2,0],["Reply",11,1],["Search",9,1],["Plan",14,1],["Draft",12,1],["Code",22,2],["Audit",26,2],["Close",24,2],["Sort",3,0]];
  const cols=["#a99ff7",VIOLET,"#3d2fa3"];
  tasks.forEach(([n,v,m],i)=>{
    const y=82+i*14.4;
    b+=T(223,y+5.6,n,{s:5.2,f:GREY});
    b+=R(246,y+1,v*2.4,6,cols[m],{r:3});
  });
  [["Small",0],["Medium",1],["Large",2]].forEach(([n,m],i)=>{const x=223+i*30; b+=`<circle cx="${x+2}" cy="261" r="2" fill="${cols[m]}"/>`+T(x+6,263,n,{s:5,f:SOFT});});
  return s.open+b+s.close;
},
autonomy(){
  const s=svg(); let b=win(28,22,344,262,false,"Tessel — Agents",s.id);
  b+=T(44,60,"Agent permissions",{s:12,w:600,ls:-.3})+T(44,72,"6 tasks · 3 run on their own",{s:6.3,f:SOFT});
  b+=T(326,60,"Act alone",{s:6,f:SOFT,a:"end"});
  b+=`<g transform="translate(343,57)"><circle r="10.5" fill="#fff" stroke="#c9cdd3"/>`;
  [-55,0,55].forEach(a=>b+=`<line y1="-7" y2="-9" stroke="#9ca1a9" stroke-width="1" transform="rotate(${a})"/>`);
  b+=`<line y1="1" y2="-6.5" stroke="${INK}" stroke-width="1.8" stroke-linecap="round" transform="rotate(55)"/><circle r="1.8" fill="${INK}"/></g>`;
  b+=T(44,93,"Task",{s:5.8,f:GREY})+T(138,93,"Team",{s:5.8,f:GREY})+T(206,93,"Mode",{s:5.8,f:GREY})+T(356,93,"Last run",{s:5.8,f:GREY,a:"end"});
  const st={"Act alone":["#e4f3ea","#2f7d58"],"Off":["#eceef1",SOFT],"Ask first":["#fbf0dc","#a86f12"]};
  const rows=[["Match invoices","Finance","Act alone","2m ago"],["Chase late payers","Ops","Ask first","1h ago"],["Flag duplicates","Finance","Act alone","just now"],["Issue refunds","Support","Ask first","3h ago"],["Tag expenses","Finance","Act alone","12m ago"],["Close the books","Finance","Off","30 Sep"]];
  rows.forEach(([o,c,x,a],i)=>{
    const y=99+i*29;
    b+=L(36,y,364,y,LINE);
    if(i===2) b+=R(36,y+.5,328,28.5,"#eef2f8");
    b+=T(44,y+17.5,o,{s:7,w:500})+T(138,y+17.5,c,{s:6.8,f:SOFT});
    const w=x.length*3.3+10; b+=R(206,y+9,w,12,st[x][0],{r:6})+T(206+w/2,y+17,x,{s:5.8,f:st[x][1],a:"middle",w:500});
    b+=T(356,y+17.5,a,{s:6.6,f:SOFT,a:"end"});
  });
  b+=CURSOR(258,164);
  return s.open+b+s.close;
},
signal(){
  const s=svg("",true); const lt="#f2f3f5";
  let b=win(28,22,344,262,true,"Signal — Foundations",s.id);
  b+=T(44,56,"Colour",{s:6.5,f:GREY,w:500});
  [["surface/base","#1b1c1f"],["surface/raised","#2a2c31"],["text/primary","#f2f3f5"],["ai/accent","#8b7cf6"],["sure","#3fb37f"],["unsure","#e0a23a"],["error","#e2574c"]].forEach(([n,c],i)=>{
    const y=64+i*20; b+=R(44,y,14,14,c,{r:3.5,st:"#3a3d44"})+T(64,y+9.5,n,{s:6.4,f:lt})+T(162,y+9.5,c.toUpperCase(),{s:5.4,f:GREY,a:"end"});
  });
  b+=L(174,46,174,272,"#2e3137");
  b+=T(186,56,"Buttons",{s:6.5,f:GREY,w:500});
  b+=R(186,64,54,18,lt,{r:4})+T(213,75.5,"Accept",{s:6.6,f:INK,a:"middle",w:600});
  b+=R(246,64,54,18,"none",{r:4,st:"#4a4e56"})+T(273,75.5,"Edit",{s:6.6,f:lt,a:"middle",w:500});
  b+=T(308,75.5,"Why this?",{s:6.6,f:"#b3a9fa",w:500});
  b+=T(186,100,"Prompt field",{s:6.5,f:GREY,w:500});
  b+=R(186,107,124,20,"#1b1c1f",{r:10,st:"#8b7cf6"})+T(196,120,"Ask about this invoice",{s:6.6,f:lt});
  b+=`<rect x="272" y="112" width="1" height="10" fill="${lt}"><animate attributeName="opacity" values="1;0;1" dur="1s" repeatCount="indefinite"/></rect>`;
  b+=`<path d="M298 111.5l1.4 3.6 3.6 1.4-3.6 1.4-1.4 3.6-1.4-3.6-3.6-1.4 3.6-1.4z" fill="#b3a9fa"/>`;
  b+=T(186,146,"States",{s:6.5,f:GREY,w:500});
  [["#262140","#8b7cf6","Thinking… read 3 sources so far"],["#16301f","#3fb37f","Done. 4 changes, all reversible."],["#3a2c16","#e0a23a","Not sure about line 12. Check it?"]].forEach(([bg,ac,t],i)=>{
    const y=153+i*24; b+=R(186,y,172,19,bg,{r:4})+R(186,y,2.5,19,ac)+T(194,y+12,t,{s:6.2,f:"#e6e7ea"});
  });
  b+=T(186,240,"Streaming",{s:6.5,f:GREY,w:500});
  [46,30,40,18].forEach((w,i)=>{b+=R(186+[0,50,84,128][i],254,w,5,"#8b7cf6",{r:2.5,op:[.9,.7,.5,.25][i]});});
  b+=T(44,234,"Type",{s:6.5,f:GREY,w:500});
  b+=T(44,262,"Aa",{s:26,w:600,f:lt,ls:-1})+T(84,250,"Familjen Grotesk",{s:6.5,f:lt})+T(84,261,"13 · 15 · 20 · 31",{s:6,f:GREY});
  return s.open+b+s.close;
},
context(){
  const s=svg(); let b=phone(139,20,122,262,s.id);
  b+=T(154,50,"Context window",{s:10.5,w:600,ls:-.3})+T(154,62,"Thread · 24 messages · 18k tokens",{s:6,f:GREY});
  const TOK=[6,9,4,12,8,5,14,7,10,6,4,11,9,5,8,13,7,10,6,12,9,15,8,5];
  TOK.forEach((v,i)=>{
    const h=8+v*5.4, inn=i>=16&&i<=21;
    b+=R(152+i*4,186-h,3,h,inn?VIOLET:"#c9cdd3",{r:1.2});
  });
  b+=R(214.5,94,24,96,"rgba(139,124,246,.1)",{r:3,st:INK,sw:1.1});
  b+=R(212.5,134,4,16,INK,{r:2})+R(236.5,134,4,16,INK,{r:2});
  b+=R(208,80,38,11,INK,{r:5.5})+T(227,87.8,"Remember",{s:5.6,f:"#fff",a:"middle",w:500});
  b+=T(152,198,"Start",{s:5,f:GREY})+T(248,198,"Now",{s:5,f:GREY,a:"end"});
  b+=L(152,191,248,191,LINE);
  b+=T(154,220,"6 recent messages",{s:11,w:700,ls:-.3})+T(154,232,"6.2k tokens · plus 2 pinned notes",{s:6.2,f:SOFT});
  b+=R(152,246,96,18,INK,{r:9})+T(200,257.5,"Apply",{s:6.6,f:"#fff",a:"middle",w:500});
  b+=CURSOR(238,148);
  return s.open+b+s.close;
},
undo(){
  const s=svg(); let b=win(28,22,344,262,false,"Tessel — Reports",s.id);
  b+=T(44,60,"Saved reports",{s:12,w:600,ls:-.3})+T(356,60,"Agent activity",{s:6.8,a:"end",w:500});
  const row=(y,n,m,d,k)=>{
    let r=R(44,y+7,16,16,"#eceef1",{r:4});
    r+=`<polyline points="${[[47,y+19],[51,y+15],[54,y+17],[57,y+11]].map(p=>p.join(",")).join(" ")}" fill="none" stroke="${["#5b8def",GREEN,AMBER,RED,SOFT][k]}" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>`;
    r+=T(68,y+14,n,{s:7.4,w:500})+T(68,y+23,m,{s:5.8,f:GREY})+T(356,y+17,d,{s:6.3,f:SOFT,a:"end"});
    return r+L(36,y+30,364,y+30,LINE);
  };
  b+=L(36,76,364,76,LINE);
  b+=row(76,"Monthly close","Built by Close agent · PDF","12 Oct",0);
  b+=row(106,"Refunds by vendor","Built by you · CSV","9 Oct",1);
  b+=R(40,140,320,24,"#f4f2fe",{r:6,st:"#a99ff7",da:"3 3"});
  b+=`<path d="M176 152a5 5 0 1 0 1.6-3.7" fill="none" stroke="${SOFT}" stroke-width="1.1" stroke-linecap="round"/><path d="M176.6 145.6l1.2 3.1-3.2.4" fill="none" stroke="${SOFT}" stroke-width="1.1" stroke-linecap="round" stroke-linejoin="round"/>`;
  b+=T(188,154.5,"Click to restore",{s:7,f:"#52565e",w:500});
  b+=T(52,154.5,"VAT summary",{s:6.3,f:"#a7abb2"})+L(52,152.4,94,152.4,"#a7abb2",.8);
  b+=T(352,154.5,"Removed by Close agent",{s:5.8,f:"#7064d6",a:"end"});
  b+=L(36,168,364,168,LINE);
  b+=row(168,"Fees per marketplace","Built by Close agent · CSV","2 Oct",2);
  b+=row(198,"Disputes, last 90 days","Built by you · CSV","28 Sep",3);
  b+=row(228,"Agent accuracy","Evals · PDF","21 Sep",4);
  b+=CURSOR(238,150);
  return s.open+b+s.close;
}
};

/* decorative QR-style mark, drawn in code */
function qr(){
  const n=21, on=new Set(); let seed=1337;
  const rnd=()=>(seed=(seed*16807)%2147483647)/2147483647;
  const finder=(ox,oy)=>{for(let y=0;y<7;y++)for(let x=0;x<7;x++){const e=x===0||y===0||x===6||y===6, c=x>=2&&x<=4&&y>=2&&y<=4; if(e||c)on.add((ox+x)+","+(oy+y));}};
  const inF=(x,y)=>(x<8&&y<8)||(x>12&&y<8)||(x<8&&y>12);
  finder(0,0);finder(14,0);finder(0,14);
  for(let y=0;y<n;y++)for(let x=0;x<n;x++) if(!inF(x,y)&&rnd()>.52) on.add(x+","+y);
  let p=""; on.forEach(k=>{const [x,y]=k.split(",");p+=`M${x} ${y}h1v1h-1z`;});
  return `<svg viewBox="0 0 21 21" aria-hidden="true" shape-rendering="crispEdges"><path d="${p}" fill="#1b1c1f"/></svg>`;
}

/* ---------- build the panels ---------- */
const P=[];
P.push(`<div class="lp-panel lp-cover" data-section="cover" data-id="cover" data-label="Foldwise"><div class="lp-pg">
  <h1>Foldwise</h1>
  <p class="lp-role">An AI-native senior product designer, as an app.</p>
  <div class="lp-foot"><p class="lp-lede">Foldwise designs alongside your team. It reads the brief, drafts the flows, works through every state nobody draws, and shows its reasoning before anything ships.</p><p class="lp-city">Private beta · Made in Amsterdam</p></div>
</div><i class="lp-shade"></i></div>`);

P.push(`<div class="lp-panel lp-index lp-dark" data-section="index" data-id="index" data-label="Contents"><div class="lp-pg">
  <div class="lp-head"><h2>Contents</h2><span>${WORKS.length} case studies</span></div>
  <div class="lp-iview"><ul class="lp-ilist">${WORKS.map((w,i)=>`<li><a href="#" data-go="${w.id}"><span>${String(i+1).padStart(2,"0")}</span><b>${w.t}</b><span>${w.c}</span><span>${w.y}</span></a></li>`).join("")}</ul></div>
  <div class="lp-ifoot"><a class="lp-lnk" href="#" data-go="notes">Notes</a>
    <span class="lp-inav" hidden><span class="lp-ipos">1 / 1</span><button class="lp-arr lp-prev" type="button" aria-label="Previous">←</button><button class="lp-arr lp-next" type="button" aria-label="Next">→</button></span></div>
</div><i class="lp-shade"></i></div>`);

WORKS.forEach(w=>{
  P.push(`<div class="lp-panel lp-work${w.dark?" lp-dark":""}" data-section="${w.id}" data-id="${w.id}" data-label="${w.t}" tabindex="0" role="link" aria-label="${w.t}, ${w.c}, ${w.y}"><div class="lp-pg">
    <div class="lp-plate">${w.dark?`<span class="lp-sticker">Internal tool</span>`:""}${ART[w.art]()}</div>
    <div class="lp-cap"><h3>${w.t}</h3><p>${w.d}</p><div class="lp-meta"><span>For ${w.c}</span><span>${w.y}</span></div></div>
  </div><i class="lp-shade"></i></div>`);
});

P.push(`<div class="lp-panel lp-notes" data-section="notes" data-id="notes" data-label="Field notes"><div class="lp-pg">
  <div class="lp-head"><h2>Field notes</h2><span>From the team</span></div>
  <ul class="lp-nlist">${NOTES.map(n=>`<li><div class="lp-nmeta"><span>${n.tag}</span><span>${n.date}</span></div><h4>${n.t}</h4><p>${n.d}</p></li>`).join("")}</ul>
  <div class="lp-pgfoot"><a class="lp-lnk" href="#" data-go="index">Back to contents</a></div>
</div><i class="lp-shade"></i></div>`);

P.push(`<div class="lp-panel lp-about lp-dark" data-section="about" data-id="about" data-label="About"><div class="lp-pg">
  <div class="lp-head"><h2>About Foldwise</h2><span>How it works</span></div>
  <p class="lp-bio">Foldwise works like a senior product designer who never loses context. It drafts screens, designs for answers that aren't certain yet, and hands off with a checklist. Teams at Tessel and Kompas use it for agents, approvals and design systems.</p>
  <ul class="lp-exp">
    <li><span>1 · Brief</span><b>Reads the problem</b><span>Your goals, data, constraints and design system</span></li>
    <li><span>2 · Draft</span><b>Designs every state</b><span>Flows, screens, errors, and what the AI says when unsure</span></li>
    <li><span>3 · Handoff</span><b>Ships with a checklist</b><span>Specs, edge cases and evals for engineering</span></li>
  </ul>
  <div class="lp-pgfoot"><a class="lp-lnk" href="#" data-go="contact">Request access</a><a class="lp-lnk" href="#" data-go="index">See the work</a></div>
</div><i class="lp-shade"></i></div>`);

const vcard="data:text/vcard;charset=utf-8,"+encodeURIComponent("BEGIN:VCARD\nVERSION:3.0\nN:;;;;\nFN:Foldwise\nORG:Foldwise\nTITLE:AI-native senior product designer\nEMAIL;TYPE=INTERNET:hello@foldwise.example\nURL:https://foldwise.example\nADR;TYPE=WORK:;;;Amsterdam;;;\nEND:VCARD");
P.push(`<div class="lp-panel lp-contact lp-dark" data-section="contact" data-id="contact" data-label="Request access"><div class="lp-pg">
  <div class="lp-bc-top"><b>Request access</b><span>Amsterdam <span class="lp-clock">--:--</span></span></div>
  <p class="lp-bc-line">Email is the fastest way in, whether you want early access, a demo for your team, or to talk about something you read here.</p>
  <button class="lp-mail" type="button" aria-label="Copy hello@foldwise.example"><span>hello@</span><span class="lp-l2">foldwise.example</span></button>
  <div class="lp-bc-state"><span class="lp-msg lp-d">Click the address to copy it</span><a class="lp-lnk lp-d" href="mailto:hello@foldwise.example">Open in mail app</a><span class="lp-msg lp-m">Tap the address to write</span><button class="lp-lnk lp-m lp-cp" type="button">Copy address</button></div>
  <div class="lp-bc-links"><a class="lp-lnk" href="#" data-go="index">Case studies</a><a class="lp-lnk" href="#" data-go="notes">Field notes</a><a class="lp-lnk lp-m" href="${vcard}" download="foldwise.vcf">Save contact</a></div>
  <div class="lp-bc-foot"><div class="lp-bc-code">${qr()}<span>Scan to save<br>our contact</span></div><div class="lp-bc-colo"><span>© 2026 Foldwise · a fictional studio</span><span><a class="lp-lnk" href="#">Privacy</a><a class="lp-lnk" href="#">Cookies</a></span></div></div>
</div><i class="lp-shade"></i></div>`);

const lp=document.getElementById("lp"), strip=lp.querySelector(".lp-strip"), stage=lp.querySelector(".lp-stage"), track=lp.querySelector(".lp-track"), hint=lp.querySelector(".lp-hint");
track.innerHTML=P.join("");
const panels=[...track.children], N=panels.length, idx=Object.fromEntries(panels.map((p,i)=>[p.dataset.id,i]));

/* ---------- the fold ---------- */
const mqV=matchMedia("(max-width: 809.98px)"), mqR=matchMedia("(prefers-reduced-motion: reduce)");
const FOLD=80*Math.PI/180, clamp=(v,a=0,b=1)=>Math.min(b,Math.max(a,v));
let k=1, maxScroll=1, prog=0, flat=false, raf=0;

function setup(){
  const v=mqV.matches; flat=v||mqR.matches;
  track.querySelectorAll("svg").forEach(s=>mqR.matches?s.pauseAnimations?.():s.unpauseAnimations?.());
  lp.classList.toggle("lp-flat",flat); lp.classList.toggle("lp-v",v);
  const vw=document.documentElement.clientWidth, vh=innerHeight;
  k = v ? Math.min(1,(vw-32)/440) : flat ? clamp((vh-250)/600,.55,1) : clamp(Math.min((vh-190)/600,(vw*.42)/440),.55,1.1);
  lp.style.setProperty("--k",k); lp.style.setProperty("--pw",440*k+"px"); lp.style.setProperty("--ph",600*k+"px");
  if(flat){strip.style.height=""; panels.forEach(p=>{p.style.transform="";p.style.removeProperty("--sh");});}
  else strip.style.height=(vh+(N-1)*vh*.62)+"px";
  maxScroll=Math.max(1,strip.offsetHeight-vh);
  render(); pageIndex();
  lp.classList.add("lp-ready");
}
function render(){
  raf=0; if(flat) return;
  const top=strip.getBoundingClientRect().top;
  prog=clamp(-top/maxScroll)*(N-1);
  const pw=440*k, xs=[0], zs=[0], th=[];
  for(let i=0;i<N;i++){
    const f=i===0?1:clamp(prog-i+1), s=i%2?1:-1;
    th[i]=s*(1-f)*FOLD;
    xs[i+1]=xs[i]+pw*Math.cos(th[i]); zs[i+1]=zs[i]-pw*Math.sin(th[i]);
  }
  const fi=1+prog*(N-2)/(N-1), a=Math.floor(fi), u=fi-a;
  const fx=xs[a]+(xs[Math.min(N,a+1)]-xs[a])*u;
  const off=stage.clientWidth/2-fx;
  panels.forEach((p,i)=>{
    p.style.transform=`translate3d(${(xs[i]+off).toFixed(2)}px,0,${zs[i].toFixed(2)}px) rotateY(${th[i].toFixed(4)}rad)`;
    const sn=Math.abs(Math.sin(th[i]));
    p.style.setProperty("--sh",(th[i]>0?sn*.34:sn*.1).toFixed(3));
  });
  const cur=Math.min(N-1,Math.round(prog));
  hint.textContent = prog<.08 ? "Scroll to unfold" : `${panels[cur].dataset.label} · ${cur+1} of ${N}`;
}
addEventListener("scroll",()=>{ if(!raf) raf=requestAnimationFrame(render); },{passive:true});
addEventListener("resize",setup);
mqV.addEventListener?.("change",setup); mqR.addEventListener?.("change",setup);

function goto(id){
  const i=typeof id==="number"?id:idx[id]; if(i==null) return;
  closeMenu();
  const smooth=mqR.matches?"auto":"smooth";
  if(lp.classList.contains("lp-v")){ const y=panels[i].getBoundingClientRect().top+scrollY-64; scrollTo({top:i===0?0:y,behavior:smooth}); return; }
  if(flat){ scrollTo({top:0,behavior:smooth}); stage.scrollTo({left:panels[i].offsetLeft-parseFloat(getComputedStyle(lp).getPropertyValue("--margin")),behavior:smooth}); return; }
  const top=strip.getBoundingClientRect().top+scrollY;
  scrollTo({top:top+i/(N-1)*maxScroll,behavior:smooth});
}
document.addEventListener("click",e=>{
  const g=e.target.closest("[data-go]");
  if(g){ e.preventDefault(); goto(g.dataset.go); return; }
  const w=e.target.closest(".lp-work");
  if(w && !flat){ const i=idx[w.dataset.id]; if(Math.abs(i-prog)>.3) goto(i); }
});
track.addEventListener("keydown",e=>{
  const w=e.target.closest?.(".lp-work");
  if(w && e.target===w && (e.key==="Enter"||e.key===" ")){ e.preventDefault(); goto(w.dataset.id); }
});
addEventListener("keydown",e=>{
  if(flat||e.target.closest("input,textarea")) return;
  if(e.key==="ArrowRight"){e.preventDefault();goto(Math.min(N-1,Math.round(prog)+1));}
  if(e.key==="ArrowLeft"){e.preventDefault();goto(Math.max(0,Math.round(prog)-1));}
});

/* ---------- contents paging ---------- */
const iview=lp.querySelector(".lp-iview"), ilist=lp.querySelector(".lp-ilist"), inav=lp.querySelector(".lp-inav");
let ipage=0;
function pageIndex(){
  const per=Math.max(1,Math.floor(iview.offsetHeight/42)), pages=Math.ceil(WORKS.length/per);
  ipage=Math.min(ipage,pages-1); inav.hidden=pages<2;
  ilist.style.transform=`translateY(${-ipage*per*42}px)`;
  inav.querySelector(".lp-ipos").textContent=`${ipage+1} / ${pages}`;
  inav.querySelector(".lp-prev").disabled=ipage===0; inav.querySelector(".lp-next").disabled=ipage>=pages-1;
}
inav.querySelector(".lp-prev").onclick=()=>{ipage--;pageIndex();};
inav.querySelector(".lp-next").onclick=()=>{ipage++;pageIndex();};

/* ---------- contact card ---------- */
const clock=lp.querySelector(".lp-clock"), fmt=new Intl.DateTimeFormat("en-GB",{hour:"2-digit",minute:"2-digit",timeZone:"Europe/Amsterdam"});
const tick=()=>clock.textContent=fmt.format(new Date()); tick(); setInterval(tick,20000);
const ADDR="hello@foldwise.example";
async function copy(){
  const msgs=lp.querySelectorAll(".lp-msg");
  try{ await navigator.clipboard.writeText(ADDR); msgs.forEach(m=>{m.textContent="Copied to clipboard";m.classList.add("lp-ok");}); }
  catch{ location.href="mailto:"+ADDR; return; }
  setTimeout(()=>msgs.forEach((m,i)=>{m.textContent=i?"Tap the address to write":"Click the address to copy it";m.classList.remove("lp-ok");}),2200);
}
lp.querySelector(".lp-mail").onclick=()=>{ if(lp.classList.contains("lp-v")) location.href="mailto:"+ADDR; else copy(); };
lp.querySelector(".lp-cp").onclick=copy;

/* ---------- mobile menu ---------- */
const mbtn=document.querySelector(".menu-btn"), drawer=document.getElementById("drawer");
function closeMenu(){
  if(!document.body.classList.contains("menu-open")) return;
  document.body.classList.remove("menu-open");mbtn.setAttribute("aria-expanded","false");drawer.setAttribute("aria-hidden","true");
  if(drawer.contains(document.activeElement)) mbtn.focus();
}
mbtn.onclick=()=>{document.body.classList.add("menu-open");mbtn.setAttribute("aria-expanded","true");drawer.setAttribute("aria-hidden","false");drawer.querySelector(".menu-close").focus();};
document.querySelector(".menu-close").onclick=closeMenu;
document.querySelector(".scrim").onclick=closeMenu;
addEventListener("keydown",e=>{if(e.key==="Escape")closeMenu();});

(document.fonts?document.fonts.ready:Promise.resolve()).then(setup);
setup();
})();
</script>
</body>
</html>
```
