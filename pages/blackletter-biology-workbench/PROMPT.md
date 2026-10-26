INSTALANDING.AI · Blackletter Biology Workbench

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Blackletter Biology Workbench · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/blackletter-biology-workbench

mistfold-biology-workbench.html:
```html
<!DOCTYPE html>
<!--
  INSTALANDING.AI · Blackletter Biology Workbench
  slug     blackletter-biology-workbench
  prompt   https://instalanding.ai/p/blackletter-biology-workbench.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/blackletter-biology-workbench
  license  MIT. Fictional brand ("Mistfold"); replace names, copy, numbers and pricing before shipping.

  MAP
  tokens    :root custom properties at the top of the <style>: --paper, --card, --tint, --ink / --ink-strong /
            --ink-soft, --line / --line-dark, the house accents (--bruma green, --northel blue, --noctum violet,
            --sakkrad mauve, --mint, --lilac, ...), --blackletter (UnifrakturMaguntia), --star (an inline SVG mask),
            --title-grad, and --ring / --ring-glow (the conic gradients behind the moving frame borders).
            Fonts from Google Fonts: Fanwood Text (body), Cinzel (numbers), UnifrakturMaguntia, JetBrains Mono.
  sections  nav, hero, modules, workflow, pricing, cta-footer
  scripts   Rough.js 4.6.6 from jsDelivr (hand-drawn margin sketches). Inline scripts, in order:
            1. module-card reveal (IntersectionObserver adds .in)
            2. WebGL shader text: one hidden GL context renders an fbm + bevel-lit texture through each
               heading's alpha and copies it into a 2D canvas laid over that heading (nav logo, h1, h2s,
               footer wordmark); the real text stays in the DOM, transparent, for screen readers
            3. waitlist form (local only, nothing is sent)
            4. sketched background: biology line icons drawn with Rough.js into a fixed canvas, in the side
               margins only, desktop (min-width 1100px) only
  assets    every icon is an inline SVG <symbol>; the star bullet is a data-URI mask; no images

  ADAPTING
  - The shader overlay only hides the real heading (.shaded) after the GL program links and the text
    is drawn, so the CSS gradient text is the fallback; do not hide headings in CSS up front.
  - Shader headings are re-rasterised from the DOM on resize and after document.fonts.ready; change a
    heading's text and it follows, but the blackletter face must load before layout or the first frame
    is drawn in the fallback serif.
  - The moving frame borders rely on @property --angle; browsers without it show a static ring.
  - The margin sketches avoid every .wbbase box; add a new top-level frame without .wbbase and icons
    will be drawn under it.
  - corner-shape: scoop is progressive: browsers without it fall back to ordinary rounded corners.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Mistfold · Computational Biology Platform</title>
<meta name="description" content="Mistfold, a fictional computational biology workbench: protein structure prediction, genomic alignment, molecular docking and single-cell analysis in one reproducible environment.">

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Fanwood+Text:ital@0;1&family=Cinzel:wght@400..900&family=UnifrakturMaguntia&family=JetBrains+Mono:wght@400;600&display=swap" rel="stylesheet">
<!-- Rough.js 4.6.6 (MIT License, © Preet Shihn): hand-drawn rendering for the background sketches -->
<script src="https://cdn.jsdelivr.net/npm/roughjs@4.6.6/bundled/rough.js" defer></script>

<style>
:root{
  --noctum:#675a7c; --groups:#4c7264; --alianza:#897a5d; --imperio:#85613a;
  --northel:#4c6d7b; --bruma:#4c7264; --vardarien:#4e663e; --daelarien:#7d7a4c;
  --sakkrad:#86667f; --sombrias:#792e2e; --shinzen:#5d4144; --dragones:#653e2f;
  --paper:#f4f2ec; --card:#fdfcf9; --tint:#eef2ef;
  --ink:#4d524f; --ink-strong:#1d2420; --ink-soft:#7a7f7b;
  --line:#e2ded3; --line-dark:#d3cec1;
  --mint:#8fbcaa; --lilac:#b3a3c6;
  --blackletter:'UnifrakturMaguntia',serif;
  --star:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24'%3E%3Cpath d='M12 1.5c.6 5.6 4.9 9.9 10.5 10.5-5.6.6-9.9 4.9-10.5 10.5C11.4 16.9 7.1 12.6 1.5 12 7.1 11.4 11.4 7.1 12 1.5z'/%3E%3C/svg%3E");
  --title-grad:linear-gradient(298deg,#1d2420 5%,var(--bruma),#7fae9c 70%,var(--bruma));
}

*{box-sizing:border-box}
.ico{fill:none;stroke:url(#ig);stroke-width:1.5;stroke-linecap:round;stroke-linejoin:round;overflow:visible}
html{scroll-behavior:smooth}
html,body{overflow-x:clip}
body{
  margin:0;color:var(--ink);font-family:"Fanwood Text",serif;font-size:17px;line-height:1.55;
  background:
    radial-gradient(ellipse 80% 50% at 50% -10%, rgba(76,114,100,.14), transparent 70%),
    radial-gradient(ellipse 60% 40% at 92% 55%, rgba(103,90,124,.09), transparent 70%),
    radial-gradient(ellipse 60% 40% at 5% 85%, rgba(76,109,123,.09), transparent 70%),
    var(--paper);
  background-attachment:fixed;
}
::selection{background:rgba(76,114,100,.2)}
a{color:var(--bruma);text-decoration:none}
a:hover{color:#2f5145}
a:focus-visible,button:focus-visible,input:focus-visible{outline:2px solid var(--bruma);outline-offset:3px}
h1{margin:0;font:inherit}

/* ---------- NAV ---------- */
.nav{position:sticky;top:0;z-index:20;backdrop-filter:blur(10px) saturate(1.2);background:rgba(250,249,245,.82);border-bottom:1px solid var(--line)}
.nav-in{max-width:1100px;margin:0 auto;padding:12px 16px;display:flex;align-items:center;justify-content:space-between;gap:16px}
.logo{font-family:var(--blackletter);font-size:28px;line-height:1;color:var(--ink-strong);display:flex;align-items:center;gap:10px}
.logo:hover{color:var(--ink-strong)}
.nav-links{display:flex;gap:22px;font-size:12px;text-transform:uppercase;letter-spacing:1px}
.nav-links a{color:var(--ink)}
.nav-links a:hover{color:var(--bruma)}
.btn{display:inline-flex;align-items:center;gap:8px;font-family:"Fanwood Text",serif;font-size:12px;text-transform:uppercase;letter-spacing:1.5px;
  padding:9px 16px;border:1px solid var(--bruma);color:var(--bruma);background:transparent;border-radius:6px;corner-shape:scoop;cursor:pointer;transition:.25s}
.btn:hover{background:var(--bruma);color:#fff}
.btn.solid{background:var(--bruma);color:#fff;box-shadow:0 6px 18px -8px rgba(76,114,100,.6)}
.btn.solid:hover{background:#3d5e52;border-color:#3d5e52;color:#fff}
@media (max-width:760px){.nav-links{display:none}}

/* ---------- WRAPPER (KApost) ---------- */
.KApost{position:relative;z-index:1;max-width:100%;width:fit-content;padding:56px 60px 20px;margin:0 auto}
@media (max-width:820px){.KApost{padding:30px 16px 10px;width:100%}}

/* ---------- BASE FRAME ---------- */
.wbbase{
  width:760px;max-width:100%;padding:40px 30px;margin:0 auto 44px;position:relative;
  outline:1px solid var(--line);outline-offset:-7px;corner-shape:scoop;border-radius:10px;
  text-align:justify
}

.wbbase tit{
  text-align:center;display:block;font-family:var(--blackletter);font-size:58px;
  background:var(--title-grad);background-size:350% 50%;animation:moveGradient 10s ease-in-out infinite;
  background-clip:text;-webkit-background-clip:text;color:transparent;-webkit-text-fill-color:transparent;
  font-weight:900;line-height:100%;letter-spacing:1px;
}
.wbbase h2.tit{font-weight:900;margin:0;font-family:var(--blackletter);font-size:44px;text-align:center;line-height:100%;
  background:var(--title-grad);background-size:350% 50%;animation:moveGradient 10s ease-in-out infinite;
  -webkit-background-clip:text;background-clip:text;color:transparent;-webkit-text-fill-color:transparent}
.subtitle{display:block;text-align:center;font-style:italic;color:var(--ink);margin-top:12px;font-size:19px}
@keyframes moveGradient{0%{background-position:0% 20%}50%{background-position:100% 50%}100%{background-position:0% 50%}}

.wbbase eti{
  width:fit-content;display:block;text-align:center;text-transform:uppercase;font-size:12px;letter-spacing:1px;line-height:100%;
  margin:0 auto 14px;background:var(--bruma);color:#fff;padding:4px 7px;border-radius:6px;position:relative;z-index:1
}

.wbsep{display:block;margin:18px auto;width:1px;height:60px;background:linear-gradient(to bottom,var(--bruma),transparent)}

/* intro */
.wbintro{width:560px;max-width:100%;margin:30px auto 0;position:relative}
.wbintro txt{
  display:block;margin:0 auto;padding:0 15px;max-height:none;
  border-left:1px solid;border-image:linear-gradient(to top,transparent,var(--groups)) 1;
}
.wbintro > .intro-ico{position:absolute;top:-30px;left:-11px;width:22px;height:22px}
.wbintro b{color:var(--ink-strong);font-weight:normal;font-style:italic}

.cta-row{display:flex;justify-content:center;gap:12px;flex-wrap:wrap;margin-top:28px}

/* ornament divider */
.wbsep2{width:100%;display:flex;align-items:center;justify-content:center;font-size:22px;color:var(--bruma);margin:34px 0 10px}
.wbsep2:before{width:30%;content:"";height:1px;background:linear-gradient(to left,var(--groups),transparent);margin-right:12px}
.wbsep2:after{width:30%;content:"";height:1px;background:linear-gradient(to right,var(--groups),transparent);margin-left:12px}

/* stats */
.stats{display:grid;grid-template-columns:repeat(4,1fr);gap:0;margin:24px auto 0;width:600px;max-width:100%}
.stat{text-align:center;padding:6px 8px;border-left:1px solid;border-image:linear-gradient(to bottom,transparent,var(--groups),transparent) 1}
.stat:first-child{border-left:0}
.stat strong{display:block;font-family:"Cinzel",serif;font-size:26px;color:var(--ink-strong);font-weight:600;line-height:1.1}
.stat span{font-size:10.5px;text-transform:uppercase;letter-spacing:1px;color:var(--ink-soft)}
@media (max-width:560px){.stats{grid-template-columns:repeat(2,1fr);row-gap:16px}.stat:nth-child(3){border-left:0}}

/* ---------- MODULE CARDS (wblugarb) ---------- */
.wblugarb{margin:15px auto;width:580px;max-width:100%}
.wblugarbbox{--accent:var(--bruma);
  width:100%;margin:22px auto;border:1px solid var(--line);overflow:hidden;background:#fff;
  box-shadow:0 1px 0 #fff inset, 0 14px 30px -22px rgba(29,36,32,.35);
  opacity:0;transform:translateY(16px);transition:opacity .7s ease, transform .7s ease, box-shadow .3s}
.wblugarbbox:hover{box-shadow:0 18px 40px -22px color-mix(in srgb,var(--accent) 70%,transparent)}
.wblugarbbox.in{opacity:1;transform:none}
.wblugarbbox-main{position:relative;display:flex;border-left:3px solid var(--accent)}
.wblugarbboxinfo{width:100%;position:relative;z-index:2;display:flex;flex-direction:column;justify-content:center;padding:26px 24px}
.wblugarbboxinfo nombre{display:block;font-family:var(--blackletter);font-size:30px;color:var(--accent);line-height:100%;margin-bottom:8px}
.wblugarbboxinfo n{display:block;text-transform:uppercase;font-size:9.5px;letter-spacing:.5px;line-height:100%;color:var(--ink-soft)}
.rate{display:inline-flex;gap:3px;vertical-align:-2px;margin-left:4px}
.rate .hex{width:11px;height:11px;stroke:var(--accent);stroke-width:2}
.rate .hex.on{fill:var(--accent);fill-opacity:.85}
.wblugarbboxinfo txt{display:block;margin-top:15px;padding-right:10px;font-size:16px}
.wblugarbboxinfo ul{margin:10px 0 0;padding:0;list-style:none;font-size:14.5px}
.wblugarbboxinfo li{padding-left:18px;position:relative;margin:3px 0}
.wblugarbboxinfo li:before{content:"";position:absolute;left:1px;top:.42em;width:10px;height:10px;background:var(--accent);-webkit-mask:var(--star) center/contain no-repeat;mask:var(--star) center/contain no-repeat}

.wblugarbbox-extra{height:92px;position:relative;border-top:1px solid var(--line);overflow:hidden;
  background:color-mix(in srgb,var(--accent) 7%,#fbfaf6)}
.wblugarbbox-extra fil1{position:absolute;inset:0;display:flex}
.wblugarbboxinspo{flex:1;margin:10px;text-align:center;text-transform:uppercase;font-size:11px;line-height:100%;color:var(--ink-soft);
  display:flex;flex-wrap:wrap;align-items:center;justify-content:center;align-content:center;gap:8px 0}
.wblugarbboxinspo + .wblugarbboxinspo{border-left:1px solid color-mix(in srgb,var(--accent) 20%,transparent)}
.wblugarbboxinspo n{text-decoration:1px underline solid var(--line-dark);text-underline-offset:3px}
.wblugarbboxinspo t{font-size:9.5px;letter-spacing:1px;display:block;width:100%;color:var(--ink-strong)}
.wblugarbboxinspo .ico{display:block;width:100%;height:20px;stroke:var(--accent)}

@media (max-width:600px){
  .wblugarbboxinfo{width:100%;padding:18px 18px 22px}
  .wbbase tit{font-size:40px}
}

/* ---------- WORKFLOW ---------- */
.flow{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;width:620px;max-width:100%;margin:26px auto 0}
.step{border:1px solid var(--line);border-radius:8px;corner-shape:scoop;padding:16px 12px;text-align:center;background:var(--tint)}
.medal{width:48px;height:48px;border-radius:50%;display:grid;place-items:center;margin:0 auto 6px;position:relative;
  background:radial-gradient(circle at 32% 26%,#fff 0,#f4f6f3 55%,#e7ece8 100%);
  box-shadow:inset 0 1px 0 #fff,0 6px 14px -8px rgba(29,36,32,.35)}
.medal:before{content:"";position:absolute;inset:-1px;border-radius:50%;padding:1px;
  background:conic-gradient(from 210deg,var(--bruma),var(--mint),var(--northel),var(--noctum),var(--lilac),var(--bruma));
  -webkit-mask:linear-gradient(#000 0 0) content-box,linear-gradient(#000 0 0);-webkit-mask-composite:xor;mask-composite:exclude}
.medal .ico{width:24px;height:24px}
.step:hover .medal:before{animation:medalSpin 2.4s linear infinite}
@keyframes medalSpin{to{transform:rotate(360deg)}}
.step b{display:block;font-family:"Cinzel",serif;color:var(--ink-strong);font-size:14px;margin:6px 0 4px;letter-spacing:.5px}
.step p{margin:0;font-size:14px;line-height:1.4;text-align:center}
@media (max-width:600px){.flow{grid-template-columns:1fr 1fr}}

pre.code{width:620px;max-width:100%;margin:22px auto 0;padding:16px 18px;background:#f3f1ea;border:1px solid var(--line);border-left:2px solid var(--bruma);
  font-family:"JetBrains Mono",monospace;font-size:12.5px;line-height:1.7;color:#2c4a40;overflow:auto;text-align:left}
pre.code .c{color:#80847f}
pre.code .k{color:var(--noctum)}
pre.code .s{color:#6a6740}

/* ---------- PRICING ---------- */
.tiers{display:grid;grid-template-columns:repeat(3,1fr);gap:14px;width:680px;max-width:100%;margin:26px auto 0}
.tier{border:1px solid var(--line);outline:1px solid var(--line);outline-offset:-5px;border-radius:10px;corner-shape:scoop;padding:24px 18px;text-align:center;background:#fff;display:flex;flex-direction:column}
.tier eti{margin-bottom:8px}
.tier .price{font-family:"Cinzel",serif;font-size:32px;color:var(--ink-strong);line-height:1.1}
.tier .price small{font-size:12px;color:var(--ink-soft);font-family:"Fanwood Text",serif}
.tier ul{list-style:none;padding:0;margin:14px 0 18px;font-size:14.5px;text-align:left;flex:1}
.tier li{padding:4px 0 4px 20px;position:relative;border-bottom:1px solid #efece4}
.tier li:before{content:"";position:absolute;left:2px;top:.62em;width:10px;height:10px;background:linear-gradient(135deg,var(--bruma),var(--noctum));-webkit-mask:var(--star) center/contain no-repeat;mask:var(--star) center/contain no-repeat}
.tier .btn{justify-content:center}
@media (max-width:680px){.tiers{grid-template-columns:1fr}}

blockquote{width:540px;max-width:100%;margin:26px auto 0;font-style:italic;font-size:19px;text-align:center;color:var(--ink-strong)}
blockquote cite{display:block;margin-top:10px;font-style:normal;font-size:11px;text-transform:uppercase;letter-spacing:1px;color:var(--ink-soft)}

.center{text-align:center}
@media (prefers-reduced-motion:reduce){*{animation:none!important;transition:none!important}.wblugarbbox{opacity:1;transform:none}}

/* ---------- HERO LINE MOTION ---------- */
@property --sweep{syntax:'<percentage>';inherits:false;initial-value:-30%}
.hero .wbsep{position:relative;overflow:visible;transform-origin:top;
  animation:lineDraw 1.4s cubic-bezier(.22,1,.36,1) .2s both}
.hero .wbsep:after{content:"";position:absolute;left:50%;top:0;width:3px;height:22px;margin-left:-1.5px;border-radius:2px;
  background:linear-gradient(to bottom,transparent,var(--bruma),transparent);
  box-shadow:0 0 10px 1px rgba(76,114,100,.35);opacity:0;
  animation:lineSpark 3.2s cubic-bezier(.65,0,.35,1) 1.6s infinite}
@keyframes lineDraw{from{transform:scaleY(0);opacity:0}to{transform:scaleY(1);opacity:1}}
@keyframes lineSpark{0%{top:-6px;opacity:0}12%{opacity:1}70%{opacity:.9}100%{top:calc(100% - 10px);opacity:0}}

.hero .wbintro:after{content:"";position:absolute;left:0;top:0;width:2px;margin-left:-.5px;height:100%;pointer-events:none;
  background:linear-gradient(to bottom,transparent calc(var(--sweep) - 12%),var(--bruma) var(--sweep),transparent calc(var(--sweep) + 12%));
  filter:drop-shadow(0 0 4px rgba(76,114,100,.5));
  animation:sweepDown 4.5s cubic-bezier(.45,0,.2,1) 2.2s infinite}
@keyframes sweepDown{0%{--sweep:-30%}60%,100%{--sweep:130%}}

.hero .stat{position:relative;border-left:0;
  opacity:0;animation:statIn .9s cubic-bezier(.22,1,.36,1) both}
.hero .stat:nth-child(1){animation-delay:.5s}.hero .stat:nth-child(2){animation-delay:.62s}
.hero .stat:nth-child(3){animation-delay:.74s}.hero .stat:nth-child(4){animation-delay:.86s}
@keyframes statIn{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
.hero .stat:before{content:"";position:absolute;left:0;top:0;bottom:0;width:1px;
  background:linear-gradient(to bottom,transparent,var(--line-dark) 30%,var(--bruma) 50%,var(--line-dark) 70%,transparent);
  background-size:100% 300%;background-position:50% 100%;
  animation:statLine 5s ease-in-out infinite}
.hero .stat:first-child:before{display:none}
.hero .stat:nth-child(2):before{animation-delay:1.2s}
.hero .stat:nth-child(3):before{animation-delay:1.5s}
.hero .stat:nth-child(4):before{animation-delay:1.8s}
@keyframes statLine{0%,100%{background-position:50% 100%}50%{background-position:50% 0%}}
@media (max-width:560px){.hero .stat:nth-child(3):before{display:none}}
@media (prefers-reduced-motion:reduce){.hero .stat{opacity:1}.hero .wbsep:after,.hero .wbintro:after{display:none}}

/* ---------- MOVING GRADIENT BORDERS ---------- */
@property --angle{syntax:'<angle>';inherits:true;initial-value:0deg}
:root{
  --ring:conic-gradient(from var(--angle),
    var(--line-dark) 0%, var(--bruma) 12%, var(--mint) 19%, var(--northel) 27%, var(--line-dark) 40%,
    var(--line-dark) 52%, var(--noctum) 64%, var(--lilac) 70%, var(--bruma) 80%, var(--line-dark) 92%);
  --ring-glow:conic-gradient(from var(--angle),
    transparent 0%, var(--bruma) 12%, var(--mint) 19%, var(--northel) 27%, transparent 40%,
    transparent 52%, var(--noctum) 64%, var(--lilac) 70%, var(--bruma) 80%, transparent 92%);
}
.wbbase, .tier.feat{
  position:relative;isolation:isolate;border:0;background:none;
  animation:ringSpin 9s linear infinite;
}
.tier.feat{box-shadow:none;animation-duration:6s}
#modules{animation-delay:-2.2s} #workflow{animation-delay:-4.5s} #pricing{animation-delay:-6.7s} #access{animation-delay:-1.1s}

.wbbase:before, .tier.feat:before{
  content:"";position:absolute;inset:0;z-index:-1;pointer-events:none;
  border:2px solid transparent;border-radius:inherit;corner-shape:scoop;
  background:linear-gradient(var(--card),var(--card)) padding-box, var(--ring) border-box;
}
.tier.feat:before{border-width:1.5px;background:linear-gradient(#fff,#fff) padding-box, var(--ring) border-box}
.wbbase:after, .tier.feat:after{
  content:"";position:absolute;inset:-3px;z-index:-2;pointer-events:none;border-radius:16px;
  background:var(--ring-glow);filter:blur(20px);opacity:.28;
}
@keyframes ringSpin{to{--angle:360deg}}
@media (prefers-reduced-motion:reduce){.wbbase,.tier.feat{--angle:35deg}}

/* ---------- FINALE: CTA + FOOTER ---------- */
.finale{width:1000px;max-width:calc(100% - 32px);margin:24px auto 40px;padding:0;text-align:left;overflow:hidden;border-radius:14px}
.finale:before{background:linear-gradient(#fdfcf9,#f7f5ef) padding-box, var(--ring) border-box}
.finale-cta{position:relative;padding:64px 40px 30px;text-align:center;overflow:hidden}
.finale-cta:before{ /* soft aurora behind the call to action */
  content:"";position:absolute;inset:-40% -10% auto;height:120%;z-index:-1;pointer-events:none;
  background:
    radial-gradient(40% 50% at 30% 50%, rgba(76,114,100,.11), transparent 70%),
    radial-gradient(35% 45% at 72% 45%, rgba(103,90,124,.09), transparent 70%),
    radial-gradient(30% 40% at 52% 70%, rgba(76,109,123,.10), transparent 70%);
  animation:aurora 16s ease-in-out infinite alternate}
@keyframes aurora{to{transform:translateX(4%) translateY(6%) scale(1.06)}}
.finale-cta h2.tit{font-size:52px}
.finale-cta p.lead{width:520px;max-width:100%;margin:16px auto 0;font-size:18px;text-align:center}
.signup{display:flex;gap:0;justify-content:center;margin:30px auto 0;width:470px;max-width:100%;
  background:#fff;border:1px solid var(--line-dark);border-radius:10px;corner-shape:scoop;padding:5px;
  box-shadow:0 18px 40px -26px rgba(29,36,32,.45);transition:border-color .25s, box-shadow .25s}
.signup:focus-within{border-color:var(--bruma);box-shadow:0 18px 40px -22px rgba(76,114,100,.55)}
.signup input{flex:1;min-width:0;background:transparent;border:0;color:var(--ink-strong);padding:10px 14px;font-family:"Fanwood Text",serif;font-size:17px;outline:none}
.signup input::placeholder{color:#8d918e}
.signup .btn{flex:none}
.assurances{display:flex;justify-content:center;flex-wrap:wrap;gap:6px 22px;margin-top:18px;font-size:11px;text-transform:uppercase;letter-spacing:1px;color:var(--ink-soft)}
.assurances span:before{content:"";display:inline-block;vertical-align:-1px;width:10px;height:10px;margin-right:7px;background:linear-gradient(135deg,var(--bruma),var(--noctum));-webkit-mask:var(--star) center/contain no-repeat;mask:var(--star) center/contain no-repeat}
.thanks{text-align:center;margin-top:12px;color:var(--bruma);font-style:italic;min-height:1.5em}

.finale-rule{display:flex;align-items:center;gap:14px;margin:0 40px;color:var(--bruma);font-size:18px}
.finale-rule:before,.finale-rule:after{content:"";flex:1;height:1px;background:linear-gradient(to right,transparent,var(--line-dark),transparent)}

.finale-foot{display:grid;grid-template-columns:1.6fr 1fr 1fr 1fr;gap:28px;padding:40px 40px 26px}
.finale-foot .logo{font-size:30px}
.finale-foot .brand p{margin:10px 0 0;font-size:15px;max-width:260px;color:var(--ink)}
.finale-foot h4{margin:4px 0 12px;font-family:"Cinzel",serif;font-weight:600;font-size:12px;letter-spacing:1.5px;text-transform:uppercase;color:var(--ink-strong)}
.finale-foot ul{list-style:none;margin:0;padding:0;font-size:15px}
.finale-foot li{margin:6px 0}
.finale-foot li a{color:var(--ink);background:linear-gradient(var(--bruma),var(--bruma)) left bottom/0 1px no-repeat;transition:background-size .3s,color .2s}
.finale-foot li a:hover{color:var(--bruma);background-size:100% 1px}

.finale-base{display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:10px;margin:0 40px;padding:16px 0 22px;border-top:1px solid var(--line);
  font-size:11.5px;letter-spacing:.5px;color:var(--ink-soft)}
.finale-base nav{display:flex;gap:18px}
.finale-base a{color:var(--ink-soft)}
.finale-base a:hover{color:var(--bruma)}

.finale-mark{position:relative;display:block;margin:8px 24px 26px;user-select:none;pointer-events:none}
.finale-mark canvas{display:block;width:100%;height:auto}
.finale-mark .mark-fallback{display:block;text-align:center;font-family:var(--blackletter);font-size:clamp(110px,22vw,260px);line-height:1.15;padding-bottom:.08em;
  background:linear-gradient(110deg,var(--bruma),var(--mint),var(--northel),var(--noctum),var(--lilac),var(--bruma));background-size:300% 100%;
  animation:moveGradient 12s ease-in-out infinite;-webkit-background-clip:text;background-clip:text;color:transparent;-webkit-text-fill-color:transparent}
.finale-mark.gl-on .mark-fallback{display:none}
.finale-mark:not(.gl-on) canvas{display:none}

@media (max-width:760px){
  .finale-cta{padding:48px 20px 40px}
  .finale-cta h2.tit{font-size:38px}
  .finale-foot{grid-template-columns:1fr 1fr;padding:32px 20px 20px}
  .finale-foot .brand{grid-column:1 / -1}
  .finale-rule,.finale-base{margin:0 20px}
  .finale-mark{margin:8px 12px 18px}
  .signup{flex-direction:column;gap:6px}
  .signup .btn{justify-content:center}
}

/* ---------- SHADER TEXT HOSTS ---------- */
.shader-host{position:relative}
.shader-canvas{position:absolute;pointer-events:none;display:block}
.shader-host.shaded{color:transparent!important;-webkit-text-fill-color:transparent!important;background:none!important;text-shadow:none!important}

/* ---------- SKETCHED BACKGROUND (desktop only) ---------- */
#sketchbg{position:fixed;inset:0;width:100vw;height:100vh;z-index:0;pointer-events:none;display:none}
@media (min-width:1100px){#sketchbg{display:block}}
</style>
</head>
<body>
<canvas id="sketchbg" aria-hidden="true"></canvas>
<svg width="0" height="0" style="position:absolute" aria-hidden="true" focusable="false">
  <defs>
    <linearGradient id="ig" gradientUnits="userSpaceOnUse" x1="2" y1="2" x2="22" y2="22">
      <stop offset="0" stop-color="#4c7264"/><stop offset=".55" stop-color="#4c6d7b"/><stop offset="1" stop-color="#675a7c"/>
    </linearGradient>
  </defs>
  <!-- lens with a helix inside -->
  <symbol id="i-lens" viewBox="0 0 24 24"><circle cx="10" cy="10" r="6.5"/><path d="M14.8 14.8l5.4 5.4"/><path d="M7.3 7.6c1.8 1.3 3.6 1.3 5.4 0M7.3 12.4c1.8-1.3 3.6-1.3 5.4 0M8.7 8.7v2.6M11.3 8.7v2.6"/></symbol>
  <!-- microscope -->
  <symbol id="i-scope" viewBox="0 0 24 24"><path d="M10 2.8l3 1.3-2.7 6.5-3-1.3z"/><path d="M8.6 10.6l-.8 1.9"/><path d="M13.6 7.2a6.3 6.3 0 0 1 2.2 10.6"/><path d="M4.8 20.6h14.4M9.2 17.6h6.6"/><circle cx="7.4" cy="14.3" r="1.1"/></symbol>
  <!-- hexagon (compute rating) -->
  <symbol id="i-hex" viewBox="0 0 24 24"><path d="M12 2.8l8 4.6v9.2l-8 4.6-8-4.6V7.4z"/></symbol>
  <!-- atom / foundation -->
  <symbol id="i-atom" viewBox="0 0 24 24"><ellipse cx="12" cy="12" rx="9.5" ry="3.6"/><ellipse cx="12" cy="12" rx="9.5" ry="3.6" transform="rotate(60 12 12)"/><ellipse cx="12" cy="12" rx="9.5" ry="3.6" transform="rotate(-60 12 12)"/><circle cx="12" cy="12" r="1.3" fill="url(#ig)" stroke="none"/></symbol>
  <!-- folded manuscript / outputs -->
  <symbol id="i-folio" viewBox="0 0 24 24"><path d="M6 3.5h8.5l3.5 3.5v13.5H6z"/><path d="M14.5 3.5V7H18"/><path d="M9 11.5h6M9 14.5h6M9 17.5h3.5"/></symbol>
  <!-- funnel / ingest -->
  <symbol id="i-funnel" viewBox="0 0 24 24"><path d="M3.8 4.5h16.4l-6.3 7.3v5.9l-3.8 2.8v-8.7z"/><path d="M7.5 8.2h9"/></symbol>
  <!-- branching nodes / compose -->
  <symbol id="i-branch" viewBox="0 0 24 24"><circle cx="6" cy="5.5" r="2"/><circle cx="6" cy="18.5" r="2"/><circle cx="18" cy="12" r="2"/><path d="M6 7.5v9M7.9 6.2c5 .3 7.7 2.4 8.4 4.1M7.9 17.8c5-.3 7.7-2.4 8.4-4.1"/></symbol>
  <!-- hexagon with spark / run -->
  <symbol id="i-surge" viewBox="0 0 24 24"><path d="M12 2.8l8 4.6v9.2l-8 4.6-8-4.6V7.4z"/><path d="M13.2 6.8L9.4 12.6h3.2l-1.6 4.6 3.9-5.9h-3.2z"/></symbol>
  <!-- open codex / publish -->
  <symbol id="i-codex" viewBox="0 0 24 24"><path d="M12 6.4C9.8 4.9 6.8 4.4 3.6 4.9v13.4c3.2-.5 6.2 0 8.4 1.5 2.2-1.5 5.2-2 8.4-1.5V4.9c-3.2-.5-6.2 0-8.4 1.5zM12 6.4v13.4"/><path d="M6.2 9.2c1.4-.1 2.7.1 3.6.6M14.2 9.8c.9-.5 2.2-.7 3.6-.6"/></symbol>
  <!-- envelope seal / access -->
  <symbol id="i-seal" viewBox="0 0 24 24"><path d="M3.5 6.5h17v11h-17z"/><path d="M3.5 6.8l8.5 6.4 8.5-6.4"/><circle cx="12" cy="15.6" r="2.1"/></symbol>
</svg>

<header class="nav" data-section="nav">
  <div class="nav-in">
    <a href="#top" class="logo" aria-label="Mistfold home">Mistfold</a>
    <nav class="nav-links" aria-label="Main">
      <a href="#modules">Modules</a>
      <a href="#workflow">Workflow</a>
      <a href="#pricing">Pricing</a>
      <a href="#access">Access</a>
    </nav>
    <a href="#access" class="btn solid">Request access</a>
  </div>
</header>

<main class="KApost" id="top">

  <!-- ================= HERO ================= -->
  <section class="wbbase hero" data-section="hero">
    <h1><tit>From Sequence to Structure</tit></h1>
    <span class="subtitle">One reproducible workbench for every question between genome and molecule.</span>
    <div class="wbsep" aria-hidden="true"></div>
    <div class="wbintro">
      <svg class="ico intro-ico" aria-hidden="true"><use href="#i-lens"/></svg>
      <txt>
        Mistfold is a computational biology workbench that brings <b>structure prediction, genomic alignment, molecular docking</b> and <b>single-cell analysis</b> into one reproducible environment. Every run is versioned, every parameter is recorded, and every result can be traced back to the raw data that produced it.
        <br><br>
        Point it at a FASTA file, a VCF, or a cloud bucket of reads. Mistfold provisions GPUs on demand, chains the right tools together, and hands you publication-ready figures — without a single hand-written cluster script.
      </txt>
    </div>
    <div class="stats">
      <div class="stat"><strong>0.92</strong><span>median pLDDT</span></div>
      <div class="stat"><strong>40×</strong><span>faster alignment</span></div>
      <div class="stat"><strong>12M</strong><span>cells indexed</span></div>
      <div class="stat"><strong>100%</strong><span>reproducible runs</span></div>
    </div>
    <div class="cta-row">
      <a href="#access" class="btn solid">Start a free project</a>
      <a href="#modules" class="btn">Explore modules</a>
    </div>
  </section>

  <!-- ================= MODULES ================= -->
  <section class="wbbase" id="modules" data-section="modules">
    <eti>the instruments</eti>
    <h2 class="tit">Modules of the Workbench</h2>
    <div class="wbsep" aria-hidden="true"></div>
    <div class="wbintro">
      <svg class="ico intro-ico" aria-hidden="true"><use href="#i-scope"/></svg>
      <txt>Four instruments, one shared data model. Outputs from one module feed directly into the next — a predicted fold becomes a docking target, a variant call becomes a structural hypothesis.</txt>
    </div>
    <div class="wbsep2" aria-hidden="true">❦</div>

    <div class="wblugarb">

      <!-- MODULE: FOLD -->
      <article class="wblugarbbox" style="--accent:var(--bruma)" data-component="module-card">
        <div class="wblugarbbox-main">
          <div class="wblugarbboxinfo">
            <nombre>Fold</nombre>
            <n>compute intensity high: <span class="rate"><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg></span></n>
            <txt>Predict 3D protein structures from sequence, including multimers and complexes. Confidence scores are mapped residue-by-residue so you know exactly which loops to trust.
              <ul><li>Monomer &amp; multimer prediction</li><li>Per-residue confidence overlays</li><li>Batch runs across whole proteomes</li></ul>
            </txt>
          </div>
        </div>
        <div class="wblugarbbox-extra"><fil1>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-atom"/></svg><n>built on</n><t>Attention-based folding networks</t></div>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-folio"/></svg><n>outputs</n><t>PDB · mmCIF · PAE maps</t></div>
        </fil1></div>
      </article>

      <!-- MODULE: ALIGN -->
      <article class="wblugarbbox" style="--accent:var(--northel)">
        <div class="wblugarbbox-main">
          <div class="wblugarbboxinfo">
            <nombre>Align</nombre>
            <n>compute intensity medium: <span class="rate"><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex" aria-hidden="true"><use href="#i-hex"/></svg></span></n>
            <txt>GPU-accelerated short- and long-read alignment with variant calling built in. Go from raw reads to annotated variants in a single pipeline that scales from one sample to a biobank.
              <ul><li>Illumina, ONT &amp; PacBio reads</li><li>SNV, indel &amp; structural variant calls</li><li>Pangenome reference graphs</li></ul>
            </txt>
          </div>
        </div>
        <div class="wblugarbbox-extra"><fil1>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-atom"/></svg><n>built on</n><t>Seed-and-extend · graph alignment</t></div>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-folio"/></svg><n>outputs</n><t>BAM · CRAM · VCF</t></div>
        </fil1></div>
      </article>

      <!-- MODULE: DOCK -->
      <article class="wblugarbbox" style="--accent:var(--noctum)">
        <div class="wblugarbbox-main">
          <div class="wblugarbboxinfo">
            <nombre>Dock</nombre>
            <n>compute intensity high: <span class="rate"><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg></span></n>
            <txt>Screen ligand libraries against predicted or experimental structures. Pocket detection, pose scoring and free-energy refinement run as one ranked campaign.
              <ul><li>Automatic binding-pocket detection</li><li>Million-compound virtual screens</li><li>Pose clustering &amp; interaction maps</li></ul>
            </txt>
          </div>
        </div>
        <div class="wblugarbbox-extra"><fil1>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-atom"/></svg><n>built on</n><t>Diffusion docking · FEP refinement</t></div>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-folio"/></svg><n>outputs</n><t>SDF · ranked hit lists</t></div>
        </fil1></div>
      </article>

      <!-- MODULE: EXPRESS -->
      <article class="wblugarbbox" style="--accent:var(--sakkrad)">
        <div class="wblugarbbox-main">
          <div class="wblugarbboxinfo">
            <nombre>Express</nombre>
            <n>compute intensity low: <span class="rate"><svg class="ico hex on" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex" aria-hidden="true"><use href="#i-hex"/></svg><svg class="ico hex" aria-hidden="true"><use href="#i-hex"/></svg></span></n>
            <txt>Single-cell and spatial transcriptomics, from count matrix to annotated atlas. Clustering, trajectory inference and cell-type labelling with reference atlases included.
              <ul><li>scRNA-seq, snATAC &amp; spatial data</li><li>Automatic cell-type annotation</li><li>Interactive embeddings you can share</li></ul>
            </txt>
          </div>
        </div>
        <div class="wblugarbbox-extra"><fil1>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-atom"/></svg><n>built on</n><t>Graph clustering · RNA velocity</t></div>
          <div class="wblugarbboxinspo"><svg class="ico" aria-hidden="true"><use href="#i-folio"/></svg><n>outputs</n><t>h5ad · atlases · UMAPs</t></div>
        </fil1></div>
      </article>

    </div>
  </section>

  <!-- ================= WORKFLOW ================= -->
  <section class="wbbase" id="workflow" data-section="workflow">
    <eti>the ritual</eti>
    <h2 class="tit">From Raw Data to Insight</h2>
    <div class="wbsep" aria-hidden="true"></div>
    <div class="flow">
      <div class="step"><span class="medal"><svg class="ico" aria-hidden="true"><use href="#i-funnel"/></svg></span><b>Ingest</b><p>Connect S3, GCS or upload FASTA, FASTQ, VCF.</p></div>
      <div class="step"><span class="medal"><svg class="ico" aria-hidden="true"><use href="#i-branch"/></svg></span><b>Compose</b><p>Chain modules into a versioned pipeline.</p></div>
      <div class="step"><span class="medal"><svg class="ico" aria-hidden="true"><use href="#i-surge"/></svg></span><b>Run</b><p>GPUs spin up on demand, then spin down.</p></div>
      <div class="step"><span class="medal"><svg class="ico" aria-hidden="true"><use href="#i-codex"/></svg></span><b>Publish</b><p>Export figures, notebooks and provenance.</p></div>
    </div>
    <div class="wbsep2" aria-hidden="true">❦</div>
    <p class="center" style="margin:0">Prefer code? The Python SDK speaks the same language as the workbench.</p>
<pre class="code" tabindex="0" aria-label="Python SDK example"><span class="k">import</span> mistfold <span class="k">as</span> mf

project = mf.Project(<span class="s">"kinase-screen"</span>)
target  = project.fold(<span class="s">"P00533.fasta"</span>)            <span class="c"># predict EGFR structure</span>
hits    = project.dock(target, library=<span class="s">"enamine-1M"</span>, top_k=<span class="s">500</span>)
hits.report().export(<span class="s">"results/"</span>)               <span class="c"># figures + full provenance</span></pre>
  </section>

  <!-- ================= PRICING ================= -->
  <section class="wbbase" id="pricing" data-section="pricing">
    <eti>the covenant</eti>
    <h2 class="tit">Plans</h2>
    <div class="wbsep" aria-hidden="true"></div>
    <div class="tiers">
      <div class="tier">
        <eti>academic</eti>
        <div class="price">Free</div>
        <ul><li>All four modules</li><li>200 GPU-hours / month</li><li>Public &amp; private projects</li><li>Community support</li></ul>
        <a href="#access" class="btn">Apply</a>
      </div>
      <div class="tier feat">
        <eti>lab</eti>
        <div class="price">$490<small> / month</small></div>
        <ul><li>Everything in Academic</li><li>2,000 GPU-hours / month</li><li>10 seats, shared workspaces</li><li>Priority queue</li></ul>
        <a href="#access" class="btn solid">Start trial</a>
      </div>
      <div class="tier">
        <eti>enterprise</eti>
        <div class="price">Custom</div>
        <ul><li>Deploy in your own cloud</li><li>SSO, audit logs, GxP options</li><li>Unlimited seats</li><li>Dedicated scientist support</li></ul>
        <a href="#access" class="btn">Talk to us</a>
      </div>
    </div>
    <blockquote>
      “We replaced three cluster scripts and a spreadsheet of parameters with one Mistfold pipeline. Our reviewers stopped asking how we got the numbers.”
      <cite>— Example testimonial · Structural biology lab</cite>
    </blockquote>
  </section>

</main>

<!-- ================= FINALE: CTA + FOOTER ================= -->
<footer class="wbbase finale" id="access" data-section="cta-footer">
  <div class="finale-cta">
    <eti>enter the mist</eti>
    <h2 class="tit">Begin Your First Fold</h2>
    <p class="lead">We're onboarding labs in small cohorts so every team gets hands-on help setting up its first pipeline. Leave your institutional email and we'll be in touch.</p>
    <form class="signup" id="signup" data-component="waitlist">
      <input type="email" required placeholder="you@lab.example" aria-label="Email address">
      <button class="btn solid" type="submit">Request access</button>
    </form>
    <div class="assurances"><span>Free for academic labs</span><span>No cluster setup</span><span>Your data stays yours</span></div>
    <div class="thanks" id="thanks" aria-live="polite"></div>
  </div>

  <div class="finale-rule" aria-hidden="true">❦</div>

  <div class="finale-foot">
    <div class="brand">
      <a href="#top" class="logo">Mistfold</a>
      <p>A reproducible workbench for structure, sequence and single-cell biology.</p>
    </div>
    <div>
      <h4>Product</h4>
      <ul><li><a href="#modules">Modules</a></li><li><a href="#workflow">Workflow</a></li><li><a href="#pricing">Pricing</a></li></ul>
    </div>
    <div>
      <h4>Resources</h4>
      <ul><li><a href="#workflow">Documentation</a></li><li><a href="#workflow">Python SDK</a></li><li><a href="#">Changelog</a></li></ul>
    </div>
    <div>
      <h4>Company</h4>
      <ul><li><a href="#">About</a></li><li><a href="#">Careers</a></li><li><a href="#access">Contact</a></li></ul>
    </div>
  </div>

  <div class="finale-base">
    <span>© 2026 Mistfold, a fictional company. Built for researchers who want to trust their results.</span>
    <nav aria-label="Legal"><a href="#">Privacy</a><a href="#">Terms</a><a href="#">Security</a></nav>
  </div>

  <div class="finale-mark" id="finaleMark" aria-hidden="true" data-component="shader-wordmark"><canvas></canvas><span class="mark-fallback">Mistfold</span></div>
</footer>

<script>
/* ---------- Reveal cards on scroll ---------- */
(function(){
  const boxes=document.querySelectorAll('.wblugarbbox');
  if(!('IntersectionObserver' in window)){boxes.forEach(b=>b.classList.add('in'));return}
  const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}}),{threshold:.15});
  boxes.forEach(b=>io.observe(b));
})();


/* ---------- Shader text: nav logo, headings, footer wordmark ---------- */
(function(){
  const glc=document.createElement('canvas');
  const gl=glc.getContext('webgl',{premultipliedAlpha:true,alpha:true,antialias:false});
  if(!gl) return;                                   // CSS gradient text stays as the fallback
  const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;

  const vs=`attribute vec2 p;varying vec2 vUv;void main(){vUv=p*.5+.5;gl_Position=vec4(p,0.,1.);}`;
  const fs=`precision highp float;
  uniform sampler2D uTex;uniform vec2 uRes;uniform float uTime,uUnit,uBevel;uniform vec2 uLight;varying vec2 vUv;
  float hash(vec2 p){return fract(sin(dot(p,vec2(127.1,311.7)))*43758.5453);}
  float noise(vec2 p){vec2 i=floor(p),f=fract(p);vec2 u=f*f*(3.-2.*f);
    return mix(mix(hash(i),hash(i+vec2(1,0)),u.x),mix(hash(i+vec2(0,1)),hash(i+vec2(1,1)),u.x),u.y);}
  float fbm(vec2 p){float v=0.,a=.5;for(int i=0;i<5;i++){v+=a*noise(p);p=p*2.03+vec2(1.7,9.2);a*=.5;}return v;}
  vec3 pal(float t){
    vec3 c0=vec3(.298,.447,.392),c1=vec3(.561,.737,.667),c2=vec3(.298,.427,.482),c3=vec3(.404,.353,.486),c4=vec3(.702,.639,.776);
    t=fract(t)*5.;vec3 c=mix(c0,c1,smoothstep(0.,1.,t));c=mix(c,c2,smoothstep(1.,2.,t));
    c=mix(c,c3,smoothstep(2.,3.,t));c=mix(c,c4,smoothstep(3.,4.,t));return mix(c,c0,smoothstep(4.,5.,t));}
  float A(vec2 uv){return texture2D(uTex,uv).a;}
  void main(){
    float a=A(vUv); if(a<.004){gl_FragColor=vec4(0.);return;}
    vec2 px=1./uRes; float r=uBevel;
    float dx=A(vUv+vec2(px.x*r,0.))-A(vUv-vec2(px.x*r,0.));
    float dy=A(vUv+vec2(0.,px.y*r))-A(vUv-vec2(0.,px.y*r));
    vec3 n=normalize(vec3(-dx,-dy,.55));
    vec2 asp=vec2(uRes.x/uRes.y,1.);
    vec2 p=vUv*uRes/uUnit; float t=uTime*.07;
    vec2 q=vec2(fbm(p+t),fbm(p+vec2(5.2,1.3)-t));
    float f=fbm(p+2.2*q+vec2(t*.6,-t*.35));
    vec3 col=pal(f*1.3+p.x*.12+t*.4);
    col*=.8+.38*f;
    vec3 L=normalize(vec3((uLight-vUv)*asp,.75));
    float diff=clamp(dot(n,L),0.,1.);
    float spec=pow(clamp(dot(n,normalize(L+vec3(0.,0.,1.))),0.,1.),48.);
    col=col*(.5+.62*diff)+vec3(spec*.6);
    float band=vUv.x+(vUv.y-.5)*.45*asp.y/asp.x*4.-(fract(uTime*.06)*1.9-.45);
    col+=vec3(.95,1.,.97)*smoothstep(.06,0.,abs(band))*.4;
    col+=(hash(gl_FragCoord.xy+fract(uTime))-.5)*.03;
    gl_FragColor=vec4(clamp(col,0.,1.)*a,a);
  }`;
  function sh(t,src){const o=gl.createShader(t);gl.shaderSource(o,src);gl.compileShader(o);
    if(!gl.getShaderParameter(o,gl.COMPILE_STATUS)){console.warn(gl.getShaderInfoLog(o));return null}return o}
  const v=sh(gl.VERTEX_SHADER,vs), f=sh(gl.FRAGMENT_SHADER,fs); if(!v||!f) return;
  const prog=gl.createProgram();gl.attachShader(prog,v);gl.attachShader(prog,f);gl.linkProgram(prog);
  if(!gl.getProgramParameter(prog,gl.LINK_STATUS)) return;
  gl.useProgram(prog);
  gl.bindBuffer(gl.ARRAY_BUFFER,gl.createBuffer());
  gl.bufferData(gl.ARRAY_BUFFER,new Float32Array([-1,-1,1,-1,-1,1,1,1]),gl.STATIC_DRAW);
  const loc=gl.getAttribLocation(prog,'p');gl.enableVertexAttribArray(loc);gl.vertexAttribPointer(loc,2,gl.FLOAT,false,0,0);
  const U={};['uRes','uTime','uUnit','uBevel','uLight'].forEach(n=>U[n]=gl.getUniformLocation(prog,n));
  gl.pixelStorei(gl.UNPACK_FLIP_Y_WEBGL,true);
  gl.enable(gl.BLEND);gl.blendFunc(gl.ONE,gl.ONE_MINUS_SRC_ALPHA);

  const items=[];
  function makeItem(el,canvas,mode,text){
    const tex=gl.createTexture();gl.bindTexture(gl.TEXTURE_2D,tex);
    [gl.TEXTURE_MIN_FILTER,gl.TEXTURE_MAG_FILTER].forEach(k=>gl.texParameteri(gl.TEXTURE_2D,k,gl.LINEAR));
    [gl.TEXTURE_WRAP_S,gl.TEXTURE_WRAP_T].forEach(k=>gl.texParameteri(gl.TEXTURE_2D,k,gl.CLAMP_TO_EDGE));
    const it={el,canvas,mode,text,ctx:canvas.getContext('2d'),off:document.createElement('canvas'),tex,
      w:0,h:0,unit:200,bevel:2,visible:true,light:[.3,.8],phase:items.length*1.7};
    items.push(it); return it;
  }

  // 1) inline headings + nav logo: canvas overlays the real text, which stays in the DOM for accessibility
  document.querySelectorAll('.nav .logo, .wbbase tit, .wbbase h2.tit').forEach(el=>{
    const c=document.createElement('canvas');c.className='shader-canvas';c.setAttribute('aria-hidden','true');
    el.classList.add('shader-host');el.appendChild(c);makeItem(el,c,'overlay');
  });
  // 2) footer wordmark: canvas sized to fit the panel width
  const mark=document.getElementById('finaleMark');
  if(mark){makeItem(mark,mark.querySelector('canvas'),'fit','Mistfold');mark.classList.add('gl-on');}

  function upload(it){
    gl.bindTexture(gl.TEXTURE_2D,it.tex);
    gl.texImage2D(gl.TEXTURE_2D,0,gl.RGBA,gl.RGBA,gl.UNSIGNED_BYTE,it.off);
  }
  function setFont(ctx,cs){
    ctx.font=`${cs.fontStyle} ${cs.fontWeight} ${cs.fontSize} ${cs.fontFamily}`;
    if('letterSpacing' in ctx) ctx.letterSpacing=(cs.letterSpacing==='normal'?'0px':cs.letterSpacing);
  }
  function layout(it){
    // DPR capped at 1.5: these canvases can be page-wide, and the noise is soft enough not to need more
    const dpr=Math.min(window.devicePixelRatio||1,1.5);
    const o=it.off.getContext('2d');
    if(it.mode==='overlay'){
      const el=it.el, cs=getComputedStyle(el), box=el.getBoundingClientRect();
      if(!box.width) return;
      const fsz=parseFloat(cs.fontSize), pad=Math.ceil(fsz*.35);
      const W=Math.ceil(box.width+pad*2), H=Math.ceil(box.height+pad*2);
      Object.assign(it.canvas.style,{left:-pad+'px',top:-pad+'px',width:W+'px',height:H+'px'});
      it.off.width=it.canvas.width=Math.round(W*dpr); it.off.height=it.canvas.height=Math.round(H*dpr);
      o.setTransform(dpr,0,0,dpr,0,0);o.clearRect(0,0,W,H);setFont(o,cs);o.fillStyle='#fff';o.textBaseline='alphabetic';
      const walker=document.createTreeWalker(el,NodeFilter.SHOW_TEXT); let node;
      while((node=walker.nextNode())){
        const re=/\S+/g; let m;
        while((m=re.exec(node.data))){
          const r=document.createRange();r.setStart(node,m.index);r.setEnd(node,m.index+m[0].length);
          const rect=r.getClientRects()[0]; if(!rect) continue;
          const mt=o.measureText(m[0]);
          const fA=mt.fontBoundingBoxAscent||fsz*.8, fD=mt.fontBoundingBoxDescent||fsz*.2;
          const base=rect.top-box.top+pad+(rect.height-(fA+fD))/2+fA;
          o.fillText(m[0],rect.left-box.left+pad,base);
        }
      }
      it.unit=fsz*dpr*1.5; it.bevel=Math.max(1,Math.min(3,fsz*dpr*.03));
    } else {
      const W=it.el.clientWidth; if(!W) return;
      const fam="UnifrakturMaguntia, serif";
      o.setTransform(1,0,0,1,0,0);o.font=`100px ${fam}`;
      const m=o.measureText(it.text);
      const w100=(m.actualBoundingBoxLeft+m.actualBoundingBoxRight)||m.width;
      const size=Math.min(W*.96/w100*100,320);
      o.font=`${size}px ${fam}`;
      const mm=o.measureText(it.text);
      const asc=mm.actualBoundingBoxAscent||size*.8, desc=mm.actualBoundingBoxDescent||size*.2;
      const left=mm.actualBoundingBoxLeft||0, tw=(mm.actualBoundingBoxLeft+mm.actualBoundingBoxRight)||mm.width;
      const pad=Math.ceil(size*.06), H=Math.ceil(asc+desc+pad*2);
      it.canvas.style.height=H+'px';
      it.off.width=it.canvas.width=Math.round(W*dpr); it.off.height=it.canvas.height=Math.round(H*dpr);
      o.setTransform(dpr,0,0,dpr,0,0);o.clearRect(0,0,W,H);o.font=`${size}px ${fam}`;o.fillStyle='#fff';
      o.fillText(it.text,(W-tw)/2+left,pad+asc);
      it.unit=it.canvas.height/1.8;
      it.bevel=2.5*Math.max(1,it.canvas.height/400);
    }
    it.w=it.canvas.width; it.h=it.canvas.height;
    upload(it);
    if(it.mode==='overlay') it.el.classList.add('shaded');
    const maxW=Math.max(...items.map(i=>i.w)), maxH=Math.max(...items.map(i=>i.h));
    if(glc.width<maxW||glc.height<maxH){glc.width=Math.max(glc.width,maxW);glc.height=Math.max(glc.height,maxH);}
    render(it,performance.now());
  }

  let pointer=null;
  addEventListener('pointermove',e=>pointer=[e.clientX,e.clientY],{passive:true});
  document.addEventListener('pointerleave',()=>pointer=null);

  function render(it,now){
    if(!it.w||!it.h) return;
    const t=now/1000+it.phase;
    let goal=[.5+.45*Math.cos(t*.35),.75+.35*Math.sin(t*.5)];
    if(pointer){
      const r=it.canvas.getBoundingClientRect(), m=Math.max(160,r.height);
      if(pointer[0]>r.left-m&&pointer[0]<r.right+m&&pointer[1]>r.top-m&&pointer[1]<r.bottom+m)
        goal=[(pointer[0]-r.left)/r.width,1-(pointer[1]-r.top)/r.height];
    }
    it.light[0]+=(goal[0]-it.light[0])*.07; it.light[1]+=(goal[1]-it.light[1])*.07;
    gl.viewport(0,0,it.w,it.h);
    gl.clearColor(0,0,0,0);gl.clear(gl.COLOR_BUFFER_BIT);
    gl.bindTexture(gl.TEXTURE_2D,it.tex);
    gl.uniform2f(U.uRes,it.w,it.h);gl.uniform1f(U.uTime,reduce?8.+it.phase:t);
    gl.uniform1f(U.uUnit,it.unit);gl.uniform1f(U.uBevel,it.bevel);gl.uniform2f(U.uLight,it.light[0],it.light[1]);
    gl.drawArrays(gl.TRIANGLE_STRIP,0,4);
    it.ctx.clearRect(0,0,it.w,it.h);
    it.ctx.drawImage(glc,0,glc.height-it.h,it.w,it.h,0,0,it.w,it.h);
  }
  // Skip work in a background tab: demos often sit in a preview iframe several tabs deep
  function loop(now){if(!document.hidden)items.forEach(it=>{if(it.visible)render(it,now)});requestAnimationFrame(loop);}

  if('IntersectionObserver' in window){
    const io=new IntersectionObserver(es=>es.forEach(e=>{const it=items.find(i=>i.canvas===e.target);if(it)it.visible=e.isIntersecting}),{rootMargin:'80px'});
    items.forEach(it=>io.observe(it.canvas));
  }
  // The blackletter face must be loaded before text is rasterised into the textures
  const fontsReady=document.fonts
    ? Promise.race([document.fonts.load('100px UnifrakturMaguntia').catch(()=>{}),new Promise(r=>setTimeout(r,2500))]).then(()=>document.fonts.ready)
    : Promise.resolve();
  fontsReady.then(()=>{
    items.forEach(layout);
    let rt; const ro=new ResizeObserver(()=>{clearTimeout(rt);rt=setTimeout(()=>items.forEach(layout),80)});
    items.forEach(it=>ro.observe(it.el));
    if(!reduce) requestAnimationFrame(loop);
  });
})();

/* ---------- Waitlist form (local only: nothing is sent anywhere) ---------- */
document.getElementById('signup').addEventListener('submit',e=>{
  e.preventDefault();
  document.getElementById('thanks').textContent='Your name is written in the ledger. We will reach you soon.';
  e.target.reset();
});
</script>

<script>
/* ---------- Sketched biology icons sprinkled in the desktop margins ---------- */
// Rough.js loads with defer from the CDN, so wait for it rather than assuming it is there
window.addEventListener('DOMContentLoaded',function(){
  const cv=document.getElementById('sketchbg'); if(!cv||typeof rough==='undefined') return;
  const mq=matchMedia('(min-width:1100px)');
  const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
  const ctx=cv.getContext('2d');
  const C=(cx,cy,r)=>`M${cx-r} ${cy}a${r} ${r} 0 1 0 ${2*r} 0a${r} ${r} 0 1 0 ${-2*r} 0`;

  // 24×24 line icons, drawn as plain paths (ellipses listed separately so they can be rotated)
  const ICONS={
    helix:{d:['M7 2c0 5 10 5 10 10S7 17 7 22','M17 2c0 5-10 5-10 10s10 5 10 10','M8.6 5.5h6.8M8.6 18.5h6.8M10 9h4M10 15h4']},
    benzene:{d:['M12 3l7.8 4.5v9L12 21l-7.8-4.5v-9z','M12 6.6l4.7 2.7M7.3 14.7l4.7 2.7M16.7 9.3v5.4',C(12,3,1.4),C(19.8,16.5,1.4),C(4.2,16.5,1.4)]},
    atom:{d:[C(12,12,1.4)],e:[[12,12,19,7.2,0],[12,12,19,7.2,60],[12,12,19,7.2,-60]]},
    flask:{d:['M9.5 2.5h5M10.5 2.5v6L4.6 18.6A1.8 1.8 0 0 0 6.2 21.5h11.6a1.8 1.8 0 0 0 1.6-2.9L13.5 8.5v-6','M7 15h10',C(10,18,.9),C(14,17.2,.6)]},
    cell:{d:[C(12,12,9.5),C(13.2,11,3.4),C(13.2,11,1.2),'M5.5 9.5c1 .6 1.4 1.6 1 2.6M8 17.5c1.3-.4 2.4 0 3 1M17.5 17c-.4-1 0-2 .9-2.5']},
    scope:{d:['M10 2.8l3 1.3-2.7 6.5-3-1.3z','M8.6 10.6l-.8 1.9','M13.6 7.2a6.3 6.3 0 0 1 2.2 10.6','M4.8 20.6h14.4M9.2 17.6h6.6',C(7.4,14.3,1.1)]},
    lens:{d:[C(10,10,6.5),'M14.8 14.8l5.4 5.4','M7.3 7.6c1.8 1.3 3.6 1.3 5.4 0M7.3 12.4c1.8-1.3 3.6-1.3 5.4 0']},
    petri:{d:['M2.5 12.5c0 3 4.3 5.5 9.5 5.5s9.5-2.5 9.5-5.5','M2.5 12.5c0-3 4.3-5.5 9.5-5.5s9.5 2.5 9.5 5.5S17.2 18 12 18 2.5 15.5 2.5 12.5z',C(8.5,12,1),C(14,13.3,1.4),C(15.5,10.6,.7)]},
    ribbon:{d:['M3 18c3-1 3-6 6-6s2 5 5 5 3-9 6-10','M3 15c3-1 3-6 6-6s2 5 5 5 3-9 6-10']},
    virus:{d:[C(12,12,5.5),'M12 6.5V3M12 17.5V21M6.5 12H3M17.5 12H21M8.1 8.1L5.6 5.6M15.9 15.9l2.5 2.5M15.9 8.1l2.5-2.5M8.1 15.9l-2.5 2.5',C(12,2.6,.9),C(12,21.4,.9),C(2.6,12,.9),C(21.4,12,.9)]},
    branch:{d:[C(6,5.5,2),C(6,18.5,2),C(18,12,2),'M6 7.5v9M7.9 6.2c5 .3 7.7 2.4 8.4 4.1M7.9 17.8c5-.3 7.7-2.4 8.4-4.1']},
    pipette:{d:['M18.5 2.5l3 3-2 2-3-3z','M17.5 6.5l-10 10-1 4-1 1M6.5 20.5l4-1 10-10','M10 14l2 2']}
  };
  const NAMES=Object.keys(ICONS);
  const COLORS=['#4c7264','#4c6d7b','#675a7c','#86667f','#6f9a8a','#7d7a4c'];

  let marks=[], docH=0, scrollY=0, last=0, dirty=true, seedTick=0;
  function rnd(seed){let x=seed;return()=>((x=(x*16807)%2147483647)/2147483647);}

  function place(){
    if(!mq.matches) return;
    docH=document.documentElement.scrollHeight;
    const blocks=[...document.querySelectorAll('.wbbase, .nav')].map(el=>{
      const r=el.getBoundingClientRect(); const m=46;
      return {l:r.left-m,r:r.right+m,t:r.top+scrollY-m,b:r.bottom+scrollY+m,fixed:el.classList.contains('nav')};
    });
    // lay out each side margin on its own grid so left and right get the same density
    const cw=document.documentElement.clientWidth;               // excludes the scrollbar
    const content=blocks.filter(b=>!b.fixed);
    const col=content.slice().sort((a,b)=>(a.r-a.l)-(b.r-b.l))[0]||{l:cw/2,r:cw/2};
    const innerL=col.l, innerR=col.r;   // narrowest frame = main column; wider frames are still avoided per icon
    const sides=[[16,innerL],[innerR,cw-16]];
    marks=[]; const cellH=150;
    sides.forEach(([x0,x1],si)=>{
      const R=rnd(20261015+si*7919), gw=x1-x0; if(gw<60) return;
      const cols=Math.max(1,Math.round(gw/150)), cellW=gw/cols;
      for(let y=90;y<docH-60;y+=cellH){
        for(let c=0;c<cols;c++){
          const size=24*(1.25+R()*1.15);
          const px=x0+c*cellW+(cellW-size)*(.1+R()*.8), py=y+R()*cellH*.7;
          const box={l:px-6,r:px+size+6,t:py-6,b:py+size+6};
          if(R()<.18) continue;
          if(content.some(b=>box.l<b.r&&box.r>b.l&&box.t<b.b&&box.b>b.t)) continue;
          if(px<8||px+size>cw-8) continue;
          marks.push({x:px,y:py,s:size/24,rot:(R()-.5)*50,name:NAMES[Math.floor(R()*NAMES.length)],
            color:COLORS[Math.floor(R()*COLORS.length)],alpha:.32+R()*.22,phase:R()*6.28,seed:1+Math.floor(R()*9999)});
        }
      }
    });
    dirty=true;
  }

  function size(){
    const dpr=Math.min(devicePixelRatio||1,2);
    cv.width=Math.round(innerWidth*dpr); cv.height=Math.round(innerHeight*dpr);
    ctx.setTransform(dpr,0,0,dpr,0,0);
  }

  // pre-render a few hand-drawn "takes" of each mark, then just swap between them (cheap boil)
  const TAKES=reduce?1:4;
  function takes(m){
    if(m.c) return m.c;
    const dpr=Math.min(devicePixelRatio||1,2), pad=6, S=Math.ceil(24*m.s+pad*2);
    m.c=[];
    for(let k=0;k<TAKES;k++){
      const oc=document.createElement('canvas'); oc.width=oc.height=Math.ceil(S*dpr);
      const o=oc.getContext('2d'), orc=rough.canvas(oc);
      o.setTransform(dpr,0,0,dpr,0,0); o.translate(pad,pad); o.scale(m.s,m.s);
      const ic=ICONS[m.name], opt={stroke:m.color,strokeWidth:1.25/m.s,roughness:.8,bowing:1.1,seed:m.seed+k*97};
      for(const d of ic.d) orc.path(d,opt);
      if(ic.e) for(const [cx,cy,w,h,a] of ic.e){o.save();o.translate(cx,cy);o.rotate(a*Math.PI/180);orc.ellipse(0,0,w,h,opt);o.restore();}
      m.c.push(oc);
    }
    m.S=S; return m.c;
  }
  function draw(t){
    ctx.clearRect(0,0,innerWidth,innerHeight);
    const vh=innerHeight;
    for(const m of marks){
      const bob=reduce?0:Math.sin(t/2600+m.phase)*5;
      const y=m.y-scrollY+bob;
      if(y<-90||y>vh+40) continue;
      const c=takes(m)[seedTick%TAKES];
      ctx.save(); ctx.globalAlpha=m.alpha;
      ctx.translate(m.x+12*m.s,y+12*m.s); ctx.rotate((m.rot+(reduce?0:Math.sin(t/4100+m.phase)*3))*Math.PI/180);
      ctx.drawImage(c,-m.S/2,-m.S/2,m.S,m.S);
      ctx.restore();
    }
  }

  function loop(t){
    requestAnimationFrame(loop);
    if(!mq.matches||document.hidden) return;
    // the hand-drawn "boil": swap to the next take ~7 times a second; scrolling redraws at once
    if(!reduce && t-last>150){ seedTick=(seedTick+1)%TAKES; last=t; dirty=true; }
    if(dirty || !reduce){ dirty=false; draw(t); }
  }

  addEventListener('scroll',()=>{scrollY=window.scrollY;dirty=true},{passive:true});
  let rt; addEventListener('resize',()=>{clearTimeout(rt);rt=setTimeout(()=>{size();scrollY=window.scrollY;place()},120)});
  mq.addEventListener?.('change',()=>{size();place()});
  const start=()=>{scrollY=window.scrollY;size();place();requestAnimationFrame(loop)};
  (document.fonts?document.fonts.ready:Promise.resolve()).then(()=>setTimeout(start,50));
  new ResizeObserver(()=>{clearTimeout(rt);rt=setTimeout(place,150)}).observe(document.body);
});
</script>
</body>
</html>
```

