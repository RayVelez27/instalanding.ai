INSTALANDING.AI · Maasai-Inspired Event Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Maasai-Inspired Event Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/maasai-inspired-event-landing-page

maasai-event-hero.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Maasai-Inspired Event Landing Page
  slug     maasai-inspired-event-landing-page
  prompt   https://instalanding.ai/p/maasai-inspired-event-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/maasai-inspired-event-landing-page
  license  MIT for this file. The hero recreates the "Maasai-Inspired Event Hero Banner Concept" from the Rive
           Marketplace in plain SVG and CSS (no Rive runtime, no .riv, nothing copied from it but the design);
           keep that credit. Fictional studio ("Sundune Events"); replace names, dates, copy and numbers before shipping.

  MAP
  tokens    :root custom properties at the top of the <style>: --bg / --surface / --ink / --ink-soft / --accent, --line /
            --line-strong / --tex, the shuka-red band set (--red, --red-ink, --red-soft, --red-line, --red-tex), the dusk
            sky (--sky-1..3), --serif (Instrument Serif), --sans (Jost), --ease. A dark set follows (prefers-color-scheme
            and :root[data-theme="dark"]). Archivo Black sets the giant MAASAI word. Three texture masks are set by the
            script: --m-shuka, --m-spear, --m-collar (plus --img-shuka for the footer wordmark).
  sections  nav, hero, frieze, approach, experiences, stats, season, process, testimonial, cta, footer
  hero      .stage is the fixed 1672x940 composition (the Rive artboard) scaled to cover the hero and anchored to the
            bottom; every layer inside is positioned in % of that box. Layers: sky + sun + clouds, mountains, ground +
            acacias, the MAASAI word, four warriors (buttons), the bird flock, reeds and grass clumps, then grain.
  scripts   one inline script, in order:
            0. texture masks cut from the warriors' own SVG geometry (shuka folds, spear, beaded collar V) as data URIs
            1. the adumu leap (Web Animations), shared by the hero warriors, the frieze silhouettes and the enquiry
               warrior; one left-to-right leap on load, then an ambient leap every 9-13 s while nobody interacts
            2. seeded grass clumps
            3. generated art for What we host: a beaded collar, a dawn ridge, two interlocked bangles on a shuka,
               and a perspective gala table with candles, guests, strings of lights and a fire, every bead and bulb
               placed by code
            4. experiences: hover or scroll a row to show its art (sticky frame); on phones each row carries a copy
            5. season bead strands  6. manifesto words that light as you read  7. scroll: nav, spear progress
               marker, frieze drift and leaps  8. pointer parallax  9. observers (pause hero, count-up, process
               spears, share beads, active experience)  10. mobile menu sheet  11. season rows prefill the form
               12. local-only enquiry, the warrior leaps on send
  assets    no image files: warriors, birds, reeds and landscape are inline SVG <symbol>s and paths; all textures are
            masks built from those shapes; grain is feTurbulence

  ADAPTING
  - Scene parts are % of the 1672x940 stage, never px. Mirror a warrior by flipping its inner <svg>, not the button.
  - A <use> inside its own <svg> needs viewBox "0 0 w h"; the symbol's own viewBox on the instance draws it off-frame.
  - Full-size SVG rules are scoped to direct children (.layer > svg) so nested reed and bird SVGs keep their size.
  - The texture masks only exist after the script runs; anything masked with them is invisible without JS by design.
  - The experience art is cloned into each row for phones at load; edit the four SVGs in .frame, not the clones.
  - Under 900px the hero stacks the copy over a window onto the stage centred on the warriors (.655 of the width).
  - prefers-reduced-motion stops the flock, sway, sparks, flicker, frieze drift and ambient leaps and lights the
    whole manifesto at once; a press still plays one leap.
-->
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Sundune Events: gatherings hosted with Maasai communities</title>
<meta name="description" content="Sundune Events, a fictional events studio: festivals, retreats, ceremonies and galas co-hosted with Maasai community partners.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo+Black&family=Instrument+Serif:ital@0;1&family=Jost:wght@400;500;600&display=swap" rel="stylesheet">
<style>
:root{
  color-scheme:light;
  --bg:#ead5b8; --surface:#f2e3cd; --ink:#1c0b06; --ink-soft:#5e3d2c; --accent:#b3261e;
  --line:rgba(28,11,6,.18); --line-strong:rgba(28,11,6,.38); --tex:rgba(28,11,6,.07);
  --red:#b3261e; --red-ink:#f8e9d4; --red-soft:#f3cdb8; --red-line:rgba(248,233,212,.42); --red-tex:rgba(28,8,4,.24);
  --sky-1:#cf7f3c; --sky-2:#e19a57; --sky-3:#efbd85;
  --serif:'Instrument Serif','Iowan Old Style',Georgia,serif;
  --sans:'Jost','Avenir Next',system-ui,sans-serif;
  --ease:cubic-bezier(.2,.8,.2,1);
  box-sizing:border-box;
  padding-top:env(safe-area-inset-top,0px); padding-bottom:env(safe-area-inset-bottom,0px);
  background:linear-gradient(var(--sky-1) 50%, var(--bg) 50%);
}
@media (prefers-color-scheme:dark){
  :root:not([data-theme="light"]){
    color-scheme:dark;
    --bg:#140805; --surface:#1f0e08; --ink:#f1e2cc; --ink-soft:#b89c85; --accent:#e5574a;
    --line:rgba(241,226,204,.15); --line-strong:rgba(241,226,204,.4); --tex:rgba(241,226,204,.05);
    --red:#9c1f18; --red-tex:rgba(0,0,0,.3);
  }
}
:root[data-theme="dark"]{
  color-scheme:dark;
  --bg:#140805; --surface:#1f0e08; --ink:#f1e2cc; --ink-soft:#b89c85; --accent:#e5574a;
  --line:rgba(241,226,204,.15); --line-strong:rgba(241,226,204,.4); --tex:rgba(241,226,204,.05);
  --red:#9c1f18; --red-tex:rgba(0,0,0,.3);
}
*,*::before,*::after{box-sizing:border-box}
html{scroll-behavior:smooth;scroll-padding-top:calc(env(safe-area-inset-top,0px) + 76px)}
body{margin:0;background:var(--bg);color:var(--ink);font:400 17px/1.65 var(--sans);-webkit-font-smoothing:antialiased;overflow-x:clip}
a{color:inherit}
button,input,select{font:inherit;color:inherit}
h1,h2,h3{text-wrap:balance}
p{text-wrap:pretty}
:focus-visible{outline:2px solid currentColor;outline-offset:4px;border-radius:4px}
.sr-only{position:absolute;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);white-space:nowrap}
.wrap{width:min(1280px, 100% - 40px);margin-inline:auto}

/* Texture masks: colour from background, shape from the warriors */
.tx-shuka{-webkit-mask:var(--m-shuka) 0 0/160px auto repeat;mask:var(--m-shuka) 0 0/160px auto repeat}

/* ── Nav ── */
.nav{position:fixed;top:0;left:0;right:0;z-index:40;padding-top:env(safe-area-inset-top,0px);color:#2a1208;transition:background .45s, color .45s, box-shadow .45s}
html.scrolled .nav{background:color-mix(in srgb, var(--bg) 86%, transparent);-webkit-backdrop-filter:blur(14px) saturate(1.2);backdrop-filter:blur(14px) saturate(1.2);color:var(--ink);box-shadow:0 1px 0 var(--line)}
body::before{content:"";position:fixed;inset:0 0 auto;height:env(safe-area-inset-top,0px);z-index:41;transition:background .45s}
html.scrolled body::before{background:color-mix(in srgb, var(--bg) 86%, transparent);-webkit-backdrop-filter:blur(14px);backdrop-filter:blur(14px)}
.nav-in{display:flex;align-items:center;justify-content:space-between;gap:20px;height:84px;padding-inline:clamp(20px, 3.2vw, 56px);transition:height .45s var(--ease)}
html.scrolled .nav-in{height:66px}
.logo{display:inline-flex;align-items:center;gap:10px;font:400 32px/1 var(--serif);letter-spacing:-.01em;text-decoration:none;color:inherit}
.logo svg{width:28px;height:10px;flex:none}
.nav-links{display:flex;align-items:center;gap:clamp(22px, 3.4vw, 52px);list-style:none;margin:0;padding:0;font:500 15px/1 var(--sans)}
.nav-links a{position:relative;padding:6px 0;text-decoration:none}
.nav-links a:not(.pill)::after{content:"";position:absolute;left:0;right:0;bottom:0;height:1.5px;background:currentColor;transform:scaleX(0);transform-origin:left;transition:transform .35s var(--ease)}
.nav-links a:not(.pill):hover::after{transform:scaleX(1)}
.pill{display:inline-flex;align-items:center;padding:11px 20px !important;border:1.5px solid currentColor;border-radius:999px;transition:background .25s, color .25s}
.pill:hover{background:currentColor}
.pill:hover span{color:var(--bg)}
html:not(.scrolled) .pill:hover span{color:#efbd85}
.menu-btn{display:none;align-items:center;gap:10px;padding:10px 0;border:0;background:none;font:500 15px/1 var(--sans);cursor:pointer}
.menu-btn i{display:grid;gap:5px}
.menu-btn i::before,.menu-btn i::after{content:"";display:block;width:22px;height:1.5px;background:currentColor}

/* Mobile sheet */
.sheet{position:fixed;inset:0;z-index:60;display:flex;flex-direction:column;padding:calc(env(safe-area-inset-top,0px) + 20px) 24px calc(env(safe-area-inset-bottom,0px) + 28px);background:var(--red);color:var(--red-ink);
  transform:translateY(-100%);visibility:hidden;transition:transform .6s var(--ease), visibility 0s .6s}
.sheet.open{transform:none;visibility:visible;transition:transform .6s var(--ease)}
.sheet::before{content:"";position:absolute;inset:0;background:var(--red-tex);pointer-events:none;-webkit-mask:var(--m-shuka) 0 0/160px auto repeat;mask:var(--m-shuka) 0 0/160px auto repeat}
.sheet-top{position:relative;display:flex;justify-content:space-between;align-items:center;height:44px}
.sheet ul{position:relative;list-style:none;margin:auto 0;padding:0;display:grid;gap:6px}
.sheet ul a{font:400 clamp(48px, 13vw, 72px)/1.05 var(--serif);text-decoration:none}
.sheet .close{border:0;background:none;font:500 15px/1 var(--sans);cursor:pointer;padding:10px 0}
.sheet p{position:relative;margin:0;color:var(--red-soft);font-size:15px}

/* Spear scroll marker (wide screens) */
.spear-progress{position:fixed;right:24px;top:50%;width:14px;height:44vh;transform:translateY(-50%);z-index:30;pointer-events:none;display:none;color:var(--ink)}
.spear-progress::before{content:"";position:absolute;left:6.5px;top:0;bottom:0;width:1px;background:currentColor;opacity:.22}
.spear-progress svg{position:absolute;left:0;top:0;width:14px;height:74px;transform:translateY(calc(var(--p, 0) * (44vh - 74px)))}

/* ── Hero ── */
.hero{--hh:max(660px, 100svh);position:relative;height:var(--hh);overflow:hidden;isolation:isolate;background:linear-gradient(var(--sky-1), var(--sky-2) 45%, var(--sky-3));color:#2a1208}
.stage{position:absolute;bottom:0;left:50%;width:max(100%, calc(var(--hh) * 1.7787));aspect-ratio:1672/940;transform:translateX(-50%);z-index:-1}
.layer{position:absolute;inset:0;width:100%;height:100%;will-change:transform}
.layer > svg{display:block;width:100%;height:100%}
.hero-copy{position:relative;z-index:5;padding:clamp(140px, 20vh, 200px) 0 0 clamp(20px, 6vw, 104px);max-width:720px}
.place{display:flex;align-items:center;gap:14px;margin:0 0 26px;font:500 15px/1.4 var(--sans);color:#fff4e6;animation:fadeIn 1s var(--ease) .1s both}
.place::before{content:"";width:42px;height:1.5px;background:currentColor;flex:none}
.hero-title{margin:0;font:400 clamp(64px, 7.6vw, 128px)/.9 var(--serif);letter-spacing:-.018em;color:#4f1a0a}
.hero-title .lw{display:block;overflow:hidden;padding-bottom:.06em}
.hero-title .ln{display:block;animation:lineIn 1.3s var(--ease) both}
.hero-title .lw + .lw .ln{animation-delay:.14s}
@keyframes lineIn{from{transform:translateY(108%)}}
@keyframes fadeIn{from{opacity:0;transform:translateY(12px)}}
.lede-hero{margin:26px 0 36px;max-width:29em;font-size:18px;line-height:1.6;animation:fadeIn 1s var(--ease) .5s both}
.hero-ctas{display:flex;flex-wrap:wrap;align-items:center;gap:30px;animation:fadeIn 1s var(--ease) .65s both}
.btn{display:inline-flex;align-items:center;justify-content:center;padding:15px 28px;border-radius:999px;border:1.5px solid transparent;font:500 16px/1 var(--sans);text-decoration:none;cursor:pointer;transition:background .25s, color .25s, transform .35s var(--ease)}
.btn-hero{background:#4f1a0a;color:#fbeee0}
.btn-hero:hover{background:#2a1208;transform:translateY(-2px)}
.link-u{padding-bottom:5px;font:500 16px/1 var(--sans);color:#4f1a0a;text-decoration:none;background:linear-gradient(currentColor, currentColor) 0 100%/100% 1.5px no-repeat;transition:background-size .4s var(--ease)}
.link-u:hover{background-size:0 1.5px;background-position:100% 100%}
.adumu-hint{display:inline-flex;align-items:center;gap:12px;margin:40px 0 0;font:500 14px/1.3 var(--sans);color:#4f1a0a;animation:fadeIn 1s var(--ease) .8s both}
.adumu-hint svg{width:12px;height:40px;flex:none}

.sun{transform-box:fill-box;transform-origin:center;animation:sun 12s ease-in-out infinite alternate}
@keyframes sun{to{opacity:.84;transform:scale(1.025)}}
.cloud{animation:cloud 120s linear infinite alternate}
.cloud.b{animation-duration:150s;animation-direction:alternate-reverse}
@keyframes cloud{to{transform:translateX(-70px)}}
.masai{animation:masai 1.8s var(--ease) .25s both}
@keyframes masai{from{opacity:0;transform:translateY(70px)}}

.warrior{position:absolute;padding:0;border:0;background:none;cursor:pointer;-webkit-tap-highlight-color:transparent}
.warrior .body{display:block;transform-origin:50% 100%}
.warrior svg{display:block;width:100%;height:auto;overflow:visible}
.warrior .flip{transform:scaleX(-1)}
.warrior .shadow{position:absolute;left:12%;right:12%;bottom:-1.2%;height:2.2%;border-radius:50%;background:rgba(60,22,8,.35);filter:blur(3px)}
.warrior:focus-visible{outline:2px solid #fff3e2;outline-offset:6px}
.w-l{left:51.02%;bottom:13.83%;width:4.575%}
.w-s{left:59.92%;bottom:15.85%;width:6.22%}
.w-b{left:66.18%;bottom:15.32%;width:6.95%}
.w-r{left:75.27%;bottom:12.23%;width:4.65%}

.flock{position:absolute;left:51%;top:19%;width:13%;aspect-ratio:200/90;animation:flock 34s linear infinite}
.flock svg{position:absolute;width:15%;overflow:visible;animation:bob 2.6s ease-in-out infinite alternate}
@keyframes flock{from{transform:translateX(420%)} to{transform:translateX(-520%)}}
@keyframes bob{to{translate:0 14%}}
.wing{transform-box:view-box;transform-origin:460px 558px;animation:flap .46s ease-in-out infinite alternate;animation-delay:var(--d, 0s)}
@keyframes flap{from{transform:scaleY(1)} to{transform:scaleY(-.85)}}
.reed{position:absolute;bottom:-4%;transform-origin:50% 100%;animation:sway 5.4s ease-in-out infinite alternate}
.reed svg{display:block;width:100%;height:auto}
.reed-1{left:2.6%;width:3.9%;animation-delay:-1.1s}
.reed-2{left:89.4%;width:3.7%;animation-duration:6.2s}
.reed-3{left:92.8%;width:2.9%;bottom:-5%;animation-duration:4.8s;animation-delay:-2s}
@keyframes sway{from{transform:rotate(-2deg)} to{transform:rotate(2.2deg)}}
.clump g{transform-box:fill-box;transform-origin:50% 100%;animation:sway 6s ease-in-out infinite alternate}
.clump g.b{animation-duration:7.2s;animation-delay:-2s}
.grain{position:absolute;inset:0;width:100%;height:100%;z-index:8;pointer-events:none;mix-blend-mode:multiply;opacity:.16}
.hero.paused *{animation-play-state:paused !important}

/* ── Frieze: the shuka band, where the warriors keep dancing ── */
.frieze{position:relative;overflow:hidden;padding:clamp(56px, 7vw, 96px) 0 clamp(26px, 3vw, 40px);background:var(--red);color:var(--red-ink)}
.frieze::before{content:"";position:absolute;inset:0;background:var(--red-tex);-webkit-mask:var(--m-shuka) 0 0/160px auto repeat;mask:var(--m-shuka) 0 0/160px auto repeat}
.frieze-track{position:relative;display:flex;align-items:flex-end;gap:clamp(30px, 4vw, 64px);width:max-content;will-change:transform}
.frieze-word{font:400 clamp(72px, 10.5vw, 176px)/.82 var(--serif);letter-spacing:-.02em;white-space:nowrap}
.sil{display:block;flex:none;height:clamp(96px, 14vw, 230px);transform-origin:50% 100%}
.sil.side{aspect-ratio:105/610}
.sil.front{aspect-ratio:250/865}
.sil svg{display:block;width:100%;height:100%;overflow:visible;filter:brightness(0)}
.sil.flip svg{transform:scaleX(-1)}
.frieze-note{position:relative;display:flex;justify-content:space-between;gap:20px;margin-top:clamp(26px, 3vw, 40px);padding-inline:clamp(20px, 3.2vw, 56px);font-size:14px;color:var(--red-soft)}

/* ── Approach ── */
.approach{padding:clamp(110px, 14vw, 200px) 0 clamp(90px, 10vw, 150px)}
.label{display:flex;align-items:center;gap:12px;margin:0 0 30px;font:500 15px/1 var(--sans);color:var(--accent)}
.label svg{width:22px;height:14px}
.scrub{margin:0;max-width:21em;font:400 clamp(36px, 4.6vw, 70px)/1.1 var(--serif);letter-spacing:-.012em}
.js .scrub .w{opacity:.17;transition:opacity .3s}
.js .scrub .w.lit{opacity:1}
.principles{display:grid;grid-template-columns:repeat(3, minmax(0, 1fr));margin:clamp(70px, 8vw, 120px) 0 0;padding:0;list-style:none;border-top:1px solid var(--line)}
.principles li{padding:34px 34px 0 0}
.principles li + li{padding-left:34px;border-left:1px solid var(--line)}
.principles svg{display:block;width:44px;height:44px;margin-bottom:22px;color:var(--accent)}
.principles h3{margin:0 0 8px;font:600 18px/1.3 var(--sans)}
.principles p{margin:0;max-width:24em;color:var(--ink-soft);font-size:16px}

/* ── Experiences ── */
.experiences{padding:clamp(90px, 10vw, 150px) 0;border-top:1px solid var(--line)}
.sec-head{display:grid;grid-template-columns:minmax(0, 1fr) minmax(0, 25em);gap:40px;align-items:end;margin-bottom:clamp(48px, 6vw, 84px)}
h2{margin:0;font:400 clamp(52px, 6.6vw, 108px)/.94 var(--serif);letter-spacing:-.018em}
.sec-head p{margin:0;color:var(--ink-soft)}
.exp-grid{display:grid;grid-template-columns:minmax(0, 7fr) minmax(0, 5fr);gap:clamp(40px, 6vw, 96px);align-items:start}
.exp-list{list-style:none;margin:0;padding:0;border-top:1px solid var(--line)}
.exp{display:grid;grid-template-columns:minmax(0, 1fr) auto;gap:10px 32px;padding:34px 0;border-bottom:1px solid var(--line)}
.exp h3{grid-column:1 / -1;display:flex;align-items:center;margin:0;font:400 clamp(42px, 4.6vw, 72px)/1 var(--serif);letter-spacing:-.012em;transition:color .45s var(--ease), gap .6s var(--ease)}
.exp h3::before{content:"";flex:none;width:0;height:.6em;background:currentColor;-webkit-mask:var(--m-shuka) 0 0/70px auto repeat;mask:var(--m-shuka) 0 0/70px auto repeat;transition:width .6s var(--ease)}
.exp.on h3{gap:18px;color:var(--accent)}
.exp.on h3::before{width:.9em}
.exp p{margin:0;max-width:30em;color:var(--ink-soft)}
.exp .meta{align-self:end;text-align:right;font:500 14px/1.45 var(--sans);color:var(--ink-soft);white-space:nowrap}
.exp-inline{display:none}
.exp-stage{position:sticky;top:110px}
.frame{position:relative;aspect-ratio:4/5;overflow:hidden;border-radius:3px;background:#2a1208}
.frame{box-shadow:0 40px 70px -40px rgba(28,11,6,.6), 0 12px 24px -16px rgba(28,11,6,.4)}
.frame::after,.exp-inline::after{content:"";position:absolute;inset:0;border-radius:inherit;box-shadow:inset 0 0 0 1px rgba(255,248,236,.1);pointer-events:none}
.art-grain{mix-blend-mode:overlay;opacity:.3;pointer-events:none}
.art{position:absolute;inset:0;width:100%;height:100%;opacity:0;transform:scale(1.05);transition:opacity .8s var(--ease), transform 1.4s var(--ease)}
.art.on{opacity:1;transform:none}
.cap{display:flex;justify-content:space-between;gap:20px;margin:16px 0 0;font-size:14px;color:var(--ink-soft)}
.flicker{animation:flicker 1.8s ease-in-out infinite alternate}
@keyframes flicker{50%{opacity:.55} to{opacity:.9}}
.flame{transform-box:fill-box;transform-origin:50% 100%;animation:flame 1.3s ease-in-out infinite alternate}
.flame.b{animation-duration:1.7s;animation-delay:-.6s}
@keyframes flame{to{transform:scale(.9, 1.12) skewX(-3deg)}}
.spark{animation:spark 3s linear infinite}
@keyframes spark{from{transform:translate(0, 0);opacity:1} to{transform:translate(var(--dx, 0), -70px);opacity:0}}

/* ── Ledger ── */
.ledger{padding:clamp(100px, 12vw, 180px) 0 clamp(80px, 9vw, 130px);border-top:1px solid var(--line)}
.ledger-text{margin:0;max-width:17em;font:400 clamp(42px, 5.8vw, 92px)/1.04 var(--serif);letter-spacing:-.016em}
.ledger-text .n{color:var(--accent);font-variant-numeric:lining-nums tabular-nums}
.share{display:grid;grid-template-columns:auto minmax(0, 1fr);gap:28px 52px;align-items:center;margin-top:clamp(60px, 7vw, 100px);padding-top:40px;border-top:1px solid var(--line)}
.share-beads{display:flex;gap:clamp(6px, 1vw, 12px)}
.share-beads i{width:clamp(20px, 2.8vw, 34px);aspect-ratio:1;border-radius:50%;border:1.5px solid var(--line-strong);transition:background .5s var(--ease), border-color .5s, transform .5s var(--ease)}
.share.in .share-beads i.f{border-color:transparent;transform:scale(1.06)}
.share.in .share-beads i:nth-child(1){background:#c0281e}
.share.in .share-beads i:nth-child(2){background:#2350a8;transition-delay:.15s}
.share.in .share-beads i:nth-child(3){background:#e57a1f;transition-delay:.3s}
.share p{margin:0;max-width:30em;font-size:19px}
.share strong{font-weight:600}

.spears{height:64px;margin:0;background:var(--ink);-webkit-mask:var(--m-spear) 0 0/24px 64px repeat-x;mask:var(--m-spear) 0 0/24px 64px repeat-x}

/* ── Season ── */
.season{padding:clamp(90px, 10vw, 150px) 0}
.dates{list-style:none;margin:0;padding:0;border-top:1px solid var(--line)}
.date{display:grid;grid-template-columns:minmax(150px, 11em) minmax(0, 1fr) 176px minmax(140px, 10em) 132px;gap:20px 36px;align-items:center;padding:28px 0;border-bottom:1px solid var(--line)}
.when{font:400 clamp(30px, 2.8vw, 40px)/1 var(--serif);letter-spacing:-.01em;font-variant-numeric:lining-nums}
.what h3{margin:0;font:600 18px/1.3 var(--sans)}
.what p{margin:2px 0 0;font-size:15px;color:var(--ink-soft)}
.strand{display:flex;gap:5px}
.strand i{width:10px;height:10px;border-radius:50%;border:1.3px solid var(--line-strong)}
.strand i.f{background:var(--ink);border-color:var(--ink)}
.status{font-size:15px;color:var(--ink-soft)}
.status.hot{color:var(--accent);font-weight:500}
.btn-sm{justify-self:end;padding:11px 20px;border:1.5px solid var(--line-strong);border-radius:999px;font:500 15px/1 var(--sans);text-decoration:none;white-space:nowrap;transition:background .25s, color .25s, border-color .25s}
.btn-sm:hover{background:var(--ink);border-color:var(--ink);color:var(--bg)}
.season-note{margin:26px 0 0;color:var(--ink-soft);font-size:15px}

/* ── Process ── */
.process{padding:clamp(90px, 10vw, 150px) 0;border-top:1px solid var(--line)}
.steps{display:grid;grid-template-columns:repeat(3, minmax(0, 1fr));gap:clamp(28px, 4vw, 56px);margin:clamp(54px, 6vw, 84px) 0 0;padding:0;list-style:none;counter-reset:s}
.steps li{position:relative;padding-top:44px;counter-increment:s}
.steps li::before{content:"";position:absolute;top:0;left:0;right:14px;height:1.5px;background:var(--ink);transform-origin:left;transform:scaleX(0);transition:transform 1.1s var(--ease)}
.steps li::after{content:"";position:absolute;top:-4.25px;right:0;width:16px;height:10px;background:var(--ink);clip-path:polygon(0 50%, 40% 0, 100% 50%, 40% 100%);opacity:0;transition:opacity .3s}
.steps.in li::before{transform:none}
.steps.in li::after{opacity:1;transition-delay:.9s}
.steps.in li:nth-child(2)::before{transition-delay:.2s}
.steps.in li:nth-child(2)::after{transition-delay:1.1s}
.steps.in li:nth-child(3)::before{transition-delay:.4s}
.steps.in li:nth-child(3)::after{transition-delay:1.3s}
.steps .num{display:block;margin-bottom:18px;font:400 52px/1 var(--serif);color:var(--accent)}
.steps h3{margin:0 0 8px;font:600 19px/1.3 var(--sans)}
.steps p{margin:0;max-width:24em;color:var(--ink-soft)}

/* ── Testimonial ── */
.voice{padding:clamp(90px, 10vw, 160px) 0;border-top:1px solid var(--line)}
.voice figure{max-width:1040px;margin:0}
.collar{display:block;width:120px;height:16px;margin-bottom:38px;background:var(--accent);-webkit-mask:var(--m-collar) 0 0/auto 16px repeat-x;mask:var(--m-collar) 0 0/auto 16px repeat-x}
.voice blockquote{margin:0;font:400 clamp(36px, 4.4vw, 66px)/1.12 var(--serif);letter-spacing:-.012em}
.voice figcaption{margin-top:30px;color:var(--ink-soft)}
.voice figcaption b{display:block;font-weight:600;color:var(--ink)}

/* ── Enquire ── */
.enquire{position:relative;overflow:hidden;padding:clamp(90px, 10vw, 150px) 0;background:var(--red);color:var(--red-ink)}
.enquire::before{content:"";position:absolute;inset:0;background:var(--red-tex);-webkit-mask:var(--m-shuka) 0 0/160px auto repeat;mask:var(--m-shuka) 0 0/160px auto repeat}
.enq-grid{position:relative;display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 6fr);gap:clamp(40px, 6vw, 110px)}
.enquire h2{color:var(--red-ink)}
.enq-lede{margin:24px 0 0;max-width:24em;color:var(--red-soft);font-size:18px}
.enq-warrior{position:relative;width:118px;margin-top:56px}
.enq-warrior .body{display:block;transform-origin:50% 100%}
.enq-warrior svg{display:block;width:100%;height:auto;filter:brightness(0)}
.enq-warrior .shadow{position:absolute;left:10%;right:10%;bottom:-6px;height:10px;border-radius:50%;background:rgba(0,0,0,.35);filter:blur(4px)}
.form{display:grid;gap:30px;align-content:start}
.field-label{display:block;margin:0 0 12px;padding:0;font:500 14px/1 var(--sans);color:var(--red-soft)}
fieldset{margin:0;padding:0;border:0;min-width:0}
.chips{display:flex;flex-wrap:wrap;gap:10px}
.chip input{position:absolute;opacity:0;pointer-events:none}
.chip span{display:inline-block;padding:11px 18px;border:1.5px solid var(--red-line);border-radius:999px;font:500 15px/1 var(--sans);cursor:pointer;transition:background .25s, color .25s, border-color .25s}
.chip:hover span{border-color:var(--red-ink)}
.chip input:checked + span{background:var(--red-ink);border-color:var(--red-ink);color:#2a0d07}
.chip input:focus-visible + span{outline:2px solid var(--red-ink);outline-offset:3px}
.range-row{display:flex;justify-content:space-between;align-items:baseline}
.range-row output{font:400 34px/1 var(--serif)}
input[type=range]{width:100%;margin:6px 0 0;accent-color:var(--red-ink)}
.two{display:grid;grid-template-columns:repeat(2, minmax(0, 1fr));gap:30px}
.line-input{width:100%;min-width:0;padding:10px 0 12px;border:0;border-bottom:1.5px solid var(--red-line);border-radius:0;background:transparent;font-size:19px;color:var(--red-ink);transition:border-color .25s}
.line-input:focus{outline:none;border-bottom-color:var(--red-ink)}
.line-input::placeholder{color:rgba(248,233,212,.5)}
select.line-input{appearance:none;-webkit-appearance:none;cursor:pointer;background:linear-gradient(45deg, transparent 50%, currentColor 50%) right 6px center/7px 7px no-repeat, linear-gradient(-45deg, transparent 50%, currentColor 50%) right 0 center/7px 7px no-repeat;padding-right:24px}
select.line-input option{color:#1c0b06;background:#f8e9d4}
.submit-row{display:flex;flex-wrap:wrap;align-items:center;gap:22px}
.btn-light{background:var(--red-ink);color:#2a0d07}
.btn-light:hover{transform:translateY(-2px);background:#fff}
.form-msg{margin:0;min-height:1.6em;font-size:16px;color:var(--red-ink)}

/* ── Footer ── */
footer{padding:clamp(70px, 8vw, 110px) 0 40px;overflow:hidden}
.foot-cols{display:grid;grid-template-columns:2fr repeat(3, minmax(0, 1fr));gap:32px}
.foot-cols h3{margin:0 0 10px;font:600 15px/1.3 var(--sans)}
.foot-cols p,.foot-cols ul{margin:0;padding:0;list-style:none;color:var(--ink-soft);font-size:15px}
.foot-cols li + li{margin-top:4px}
.foot-cols a{text-decoration:none}
.foot-cols a:hover{color:var(--ink)}
.wordmark{display:block;margin:clamp(50px, 7vw, 90px) 0 0;font:400 clamp(104px, 26vw, 430px)/.78 var(--serif);letter-spacing:-.035em;white-space:nowrap;
  color:var(--accent);background:var(--img-shuka, none) 0 0/130px auto, linear-gradient(var(--accent), var(--accent));-webkit-background-clip:text;background-clip:text;-webkit-text-fill-color:transparent}
.legal{display:flex;flex-wrap:wrap;justify-content:space-between;gap:16px 30px;margin-top:34px;padding-top:24px;border-top:1px solid var(--line);font-size:13px;color:var(--ink-soft)}
.legal p{margin:0;max-width:62em}
.to-top{border:0;background:none;padding:0;font:500 13px/1.4 var(--sans);cursor:pointer;color:var(--ink)}

@media (min-width:1200px){ .spear-progress{display:block} }
@media (max-width:1100px){
  .date{grid-template-columns:minmax(130px, 9em) minmax(0, 1fr) auto;grid-template-areas:"when what act" "when strand status"}
  .when{grid-area:when;align-self:start}.what{grid-area:what}.strand{grid-area:strand}.status{grid-area:status;text-align:right}.date .btn-sm{grid-area:act;justify-self:end}
  .foot-cols{grid-template-columns:repeat(2, minmax(0, 1fr))}
}
@media (max-width:899px){
  .nav-links{display:none}
  .menu-btn{display:inline-flex}
  .nav-in{height:72px}
  html.scrolled .nav-in{height:62px}
  /* The scene stays a full-bleed background: it sits under the copy and rises behind it, nothing clips it */
  .hero{height:auto;--hh:clamp(580px, 60vw + 370px, 780px)}
  .hero-copy{padding:118px 20px 0;max-width:none}
  .hero-title{font-size:clamp(58px, 15vw, 96px)}
  .lede-hero{margin:22px 0 30px}
  .adumu-hint{margin-top:28px}
  .stage-window{position:relative;height:calc(var(--hh) * .6);margin-top:-8px}
  .stage{left:calc(50% - var(--hh) * 1.7787 * .655);transform:none;width:calc(var(--hh) * 1.7787)}
  .frieze-note{flex-direction:column;gap:2px}
  .principles{grid-template-columns:minmax(0, 1fr)}
  .principles li,.principles li + li{padding:30px 0;border-left:0;border-bottom:1px solid var(--line)}
  .sec-head{grid-template-columns:minmax(0, 1fr);gap:20px}
  .exp-grid{grid-template-columns:minmax(0, 1fr)}
  .exp-stage{display:none}
  .exp-inline{display:block;position:relative;grid-column:1 / -1;order:-1;aspect-ratio:4/3;margin-bottom:14px;overflow:hidden;border-radius:3px;background:#2a1208}
  .exp-inline svg{display:block;width:100%;height:100%}
  .exp h3{color:var(--ink) !important}
  .exp h3::before{display:none}
  .exp .meta{grid-column:1 / -1;text-align:left}
  .share{grid-template-columns:minmax(0, 1fr)}
  .steps{grid-template-columns:minmax(0, 1fr);gap:44px}
  .enq-grid{grid-template-columns:minmax(0, 1fr)}
  .enq-warrior{display:none}
}
@media (min-width:900px){ .stage-window{display:contents} }
@media (max-width:640px){
  .date{grid-template-columns:minmax(0, 1fr) auto;grid-template-areas:"when act" "what what" "strand status";gap:14px 20px}
  .two{grid-template-columns:minmax(0, 1fr)}
  .foot-cols{grid-template-columns:minmax(0, 1fr)}
  .frieze-word{font-size:64px}
  .sil{height:92px}
}
@media (prefers-reduced-motion:reduce){
  html{scroll-behavior:auto}
  .place,.hero-title .ln,.lede-hero,.hero-ctas,.adumu-hint,.sun,.cloud,.masai,.flock,.flock svg,.wing,.reed,.clump g,.flicker,.flame,.spark{animation:none}
  .flock{transform:translateX(0)}
  .art,.steps li::before,.steps li::after,.sheet{transition:none}
}
</style>
</head>
<body>

<!-- Sprite: the warriors, bird and reed from the Rive artboards, plus shared paints for the generated art -->
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <defs>
    <symbol id="w-front" viewBox="320 55 250 865">
      <path d="M343 60 L357 120 L343 148 L330 120Z" fill="#1a1514"/>
      <rect x="339.5" y="140" width="7" height="776" fill="#1d1918"/>
      <path d="M384 728 L412 756 L410 836 L380 838Z" fill="#4a1206"/>
      <path d="M494 735 L522 788 L497 818Z" fill="#4a1206"/>
      <path d="M410 750 L442 760 L436 893 L420 893Z" fill="#0b0807"/>
      <path d="M468 725 L500 732 L490 893 L473 893Z" fill="#0b0807"/>
      <path d="M420 890 L436 892 L436 910 L406 916 L407 906Z" fill="#0b0807"/>
      <path d="M472 890 L490 892 L503 905 L503 916 L470 915Z" fill="#0b0807"/>
      <path d="M438 360 L462 360 L460 392 L448 404 L436 392Z" fill="#22140f"/>
      <ellipse cx="450" cy="343" rx="21" ry="26" fill="#22140f"/>
      <path d="M469 348 Q479 355 472 369 Q466 360 469 348Z" fill="#140b08"/>
      <path d="M496 412 L518 420 L528 450 L540 500 L552 542 L556 605 L566 640 L556 652 L548 656 L546 628 L544 612 L530 552 L516 500 L504 462Z" fill="#1d130f"/>
      <path d="M380 418 L402 424 L398 470 L394 510 L388 538 L374 534 L354 508 L338 502 L330 492 L332 478 L348 474 L356 492 L374 508 L376 470Z" fill="#22140f"/>
      <path d="M388 412 L432 390 L448 404 L466 390 L492 406 L514 420 L500 470 L490 520 L410 522 L400 470Z" fill="#15100d"/>
      <path d="M400 410 L420 400 L448 432 L470 398 L492 408 L470 432 L436 460Z" fill="#a9441b"/>
      <path d="M420 400 L432 390 L448 410 L466 390 L470 398 L448 432Z" fill="#15100d"/>
      <path d="M432 390 L448 410 L466 390" stroke="#fff" stroke-width="2" fill="none" stroke-linejoin="round"/>
      <path d="M436 460 L470 492" stroke="#2c1d17" stroke-width="2"/>
      <path d="M388 412 L412 505" stroke="#fff" stroke-width="1.6"/>
      <path d="M410 504 L468 490 L484 522 L410 522Z" fill="#7a2410"/>
      <path d="M408 522 L484 522 L495 568 L446 548 L408 530Z" fill="#15100d"/>
      <path d="M408 530 L446 548 L430 780 L354 708Z" fill="#15100d"/>
      <path d="M446 548 L495 568 L530 785 L438 660Z" fill="#a9441b"/>
      <path d="M438 660 L492 730 L452 855 L430 780Z" fill="#3d1f18"/>
      <path d="M354 708 L430 780 L446 548 L495 568" stroke="#fff" stroke-width="3" fill="none" stroke-linejoin="round"/>
    </symbol>
    <symbol id="w-side" viewBox="345 155 105 610">
      <path d="M437 162 L445 195 L437 215 L429 195Z" fill="#141111"/>
      <path d="M435 205 L440 205 L434 680 L429 680Z" fill="#1b1716"/>
      <path d="M431 672 L439 690 L432 727 L424 690Z" fill="#141111"/>
      <path d="M388 684 L404 684 L398 728 L420 739 L418 743 L392 740 L386 732Z" fill="#0d0a09"/>
      <path d="M374 684 L394 684 L384 742 L406 754 L405 758 L366 757 L370 744Z" fill="#0b0807"/>
      <path d="M366 505 L404 505 L424 620 L428 688 L356 688 L360 590Z" fill="#6b2a10"/>
      <path d="M366 505 L382 505 L377 688 L356 688 L360 590Z" fill="#58220c"/>
      <path d="M404 505 L418 560 L438 626 L424 638 L410 580Z" fill="#a5562e"/>
      <path d="M418 560 L438 626" stroke="#f3e6da" stroke-width="1.4"/>
      <path d="M370 410 L400 410 L407 452 L404 522 L368 526 L352 460 L352 432Z" fill="#17110e"/>
      <path d="M378 410 L400 410 L407 452 L382 494 L376 476 L394 444Z" fill="#a3542d"/>
      <path d="M394 444 L407 452 L382 494 L376 476Z" fill="#b97a54"/>
      <path d="M378 411 L404 449" stroke="#f5e9dc" stroke-width="1.6"/>
      <path d="M386 396 L398 396 L401 414 L384 414Z" fill="#241712"/>
      <path d="M378 380 Q378 364 393 364 Q408 366 408 386 Q408 400 402 404 L394 406 Q382 404 378 392Z" fill="#2c1f19"/>
      <path d="M354 432 L374 436 L378 470 L380 496 L364 504 L358 470Z" fill="#241712"/>
      <path d="M368 494 L408 484 L428 462 L440 464 L438 476 L414 494 L374 510Z" fill="#241712"/>
      <path d="M357 464 L377 466" stroke="#c4672f" stroke-width="3"/>
      <path d="M359 471 L378 473" stroke="#f0d9c4" stroke-width="1.5"/>
      <path d="M405 486 L411 495" stroke="#c4672f" stroke-width="3"/>
      <ellipse cx="434" cy="468" rx="7" ry="8" fill="#241712"/>
    </symbol>
    <symbol id="bird" viewBox="270 470 480 280">
      <path class="wing" d="M404 560 L494 560 L548 582 Q584 598 596 614 L566 640 Q562 668 538 694 L478 732 Q456 676 418 628 Q396 600 410 578Z" fill="#7d4f2b"/>
      <path d="M278 548 L330 524 Q345 504 368 506 L520 508 Q600 512 742 545 Q640 552 560 576 Q480 588 400 582 Q350 572 336 552Z" fill="#8b5a32"/>
      <path class="wing" d="M418 556 L508 556 L560 575 Q600 588 615 603 L586 632 Q585 660 560 690 L505 726 Q480 670 430 620 Q408 598 425 575Z" fill="#a86e3c"/>
    </symbol>
    <symbol id="reed" viewBox="300 85 110 840">
      <path d="M372 920 Q318 700 322 465" stroke="#34201a" stroke-width="4" fill="none" stroke-linecap="round"/>
      <path d="M322 455 Q330 260 372 158" stroke="#34201a" stroke-width="20" fill="none" stroke-linecap="round"/>
      <path d="M374 150 L397 95" stroke="#34201a" stroke-width="4" stroke-linecap="round"/>
    </symbol>
    <symbol id="acacia" viewBox="-56 -74 112 76">
      <path d="M-2 0 L-1 -30 L-16 -48 L-14 -49 L0 -34 L12 -52 L14 -51 L2 -32 L2 0Z"/>
      <path d="M-50 -48 Q-34 -62 -8 -58 Q8 -66 32 -60 Q50 -56 56 -48 Q28 -44 0 -46 Q-24 -44 -50 -48Z"/>
      <path d="M-32 -58 Q-14 -70 10 -66 Q26 -68 38 -60 Q8 -56 -32 -58Z"/>
    </symbol>
    <!-- The shuka fold from #w-front (its three cloth panels and white edge), as an in-SVG pattern for the art -->
    <pattern id="pShuka" width="360" height="340" patternUnits="userSpaceOnUse" patternTransform="scale(.42)">
      <g fill="none" stroke="#1c0b06" stroke-width="3" stroke-linejoin="round">
        <path d="M58 5 L96 23 L80 255 L4 183Z"/><path d="M96 23 L145 43 L180 260 L88 135Z" fill="#1c0b06" fill-opacity=".5"/><path d="M88 135 L142 205 L102 330 L80 255Z"/>
        <g transform="translate(360 0) scale(-1 1)"><path d="M58 5 L96 23 L80 255 L4 183Z"/><path d="M96 23 L145 43 L180 260 L88 135Z" fill="#1c0b06" fill-opacity=".5"/><path d="M88 135 L142 205 L102 330 L80 255Z"/></g>
      </g>
    </pattern>
    <pattern id="pPlaid" width="52" height="52" patternUnits="userSpaceOnUse">
      <rect x="22" width="8" height="52" fill="#b3261e" opacity=".75"/><rect y="22" width="52" height="8" fill="#b3261e" opacity=".75"/>
      <rect x="38" width="3" height="52" fill="#000" opacity=".25"/><rect y="38" width="52" height="3" fill="#000" opacity=".25"/>
    </pattern>
    <linearGradient id="gDawn" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#f4cf9c"/><stop offset=".55" stop-color="#e09656"/><stop offset="1" stop-color="#b9592a"/></linearGradient>
    <radialGradient id="gGlow" cx=".5" cy=".95" r=".7"><stop offset="0" stop-color="#c2571d" stop-opacity=".9"/><stop offset=".45" stop-color="#7a2410" stop-opacity=".45"/><stop offset="1" stop-color="#1a0b06" stop-opacity="0"/></radialGradient>
    <filter id="toInk" color-interpolation-filters="sRGB"><feColorMatrix type="matrix" values="0 0 0 0 .07  0 0 0 0 .03  0 0 0 0 .02  0 0 0 1 0"/></filter>
    <!-- Paints for the What we host art -->
    <radialGradient id="gGloss" cx=".5" cy=".5" r=".5" fx=".34" fy=".3"><stop offset="0" stop-color="#fff" stop-opacity=".85"/><stop offset=".28" stop-color="#fff" stop-opacity=".12"/><stop offset=".7" stop-color="#000" stop-opacity="0"/><stop offset="1" stop-color="#000" stop-opacity=".38"/></radialGradient>
    <linearGradient id="gMetal" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#f1e9dc"/><stop offset=".5" stop-color="#b9ad9c"/><stop offset="1" stop-color="#6f6458"/></linearGradient>
    <radialGradient id="gLeather" cx=".4" cy=".22" r=".95"><stop offset="0" stop-color="#7a3418"/><stop offset=".5" stop-color="#3d180b"/><stop offset="1" stop-color="#160804"/></radialGradient>
    <radialGradient id="gVig" cx=".5" cy=".45" r=".78"><stop offset=".55" stop-color="#000" stop-opacity="0"/><stop offset="1" stop-color="#000" stop-opacity=".55"/></radialGradient>
    <linearGradient id="gDawnSky" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#e3a170"/><stop offset=".4" stop-color="#f4cd9a"/><stop offset=".6" stop-color="#fae3bd"/><stop offset="1" stop-color="#e49a62"/></linearGradient>
    <radialGradient id="gSunHalo"><stop offset="0" stop-color="#fff3da" stop-opacity=".95"/><stop offset=".3" stop-color="#fbdcae" stop-opacity=".5"/><stop offset="1" stop-color="#f6cf9a" stop-opacity="0"/></radialGradient>
    <linearGradient id="gMist" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#fbe1b8" stop-opacity="0"/><stop offset=".5" stop-color="#fbe1b8" stop-opacity=".6"/><stop offset="1" stop-color="#fbe1b8" stop-opacity="0"/></linearGradient>
    <radialGradient id="gPool" cx=".5" cy=".32" r=".75"><stop offset="0" stop-color="#ffd7a3" stop-opacity=".26"/><stop offset="1" stop-color="#ffd7a3" stop-opacity="0"/></radialGradient>
    <linearGradient id="gNight" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#070302"/><stop offset=".5" stop-color="#1d0b05"/><stop offset="1" stop-color="#3f170a"/></linearGradient>
    <linearGradient id="gHorizon" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#c55a24" stop-opacity="0"/><stop offset=".85" stop-color="#c55a24" stop-opacity=".5"/><stop offset="1" stop-color="#f09a52" stop-opacity=".75"/></linearGradient>
    <linearGradient id="gCloth" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3a190b"/><stop offset="1" stop-color="#c88a52"/></linearGradient>
    <pattern id="pShukaLt" width="360" height="340" patternUnits="userSpaceOnUse" patternTransform="scale(.5)">
      <g fill="none" stroke="#f8e9d4" stroke-opacity=".08" stroke-width="2.4" stroke-linejoin="round">
        <path d="M58 5 L96 23 L80 255 L4 183Z"/><path d="M96 23 L145 43 L180 260 L88 135Z"/><path d="M88 135 L142 205 L102 330 L80 255Z"/>
        <g transform="translate(360 0) scale(-1 1)"><path d="M58 5 L96 23 L80 255 L4 183Z"/><path d="M96 23 L145 43 L180 260 L88 135Z"/><path d="M88 135 L142 205 L102 330 L80 255Z"/></g>
      </g>
    </pattern>
    <pattern id="pCheck" width="90" height="90" patternUnits="userSpaceOnUse">
      <rect width="18" height="90" fill="#5e0f0a" opacity=".55"/><rect width="90" height="18" fill="#5e0f0a" opacity=".55"/>
      <rect x="26" width="3" height="90" fill="#140604" opacity=".55"/><rect y="26" width="90" height="3" fill="#140604" opacity=".55"/>
      <rect x="58" width="6" height="90" fill="#1f3f86" opacity=".5"/><rect y="58" width="90" height="6" fill="#1f3f86" opacity=".5"/>
      <rect x="71" width="1.5" height="90" fill="#f2c230" opacity=".45"/><rect y="71" width="90" height="1.5" fill="#f2c230" opacity=".45"/>
    </pattern>
    <pattern id="pWeave" width="4" height="4" patternUnits="userSpaceOnUse"><rect width="2" height="4" fill="#000" opacity=".1"/><rect width="4" height="2" fill="#fff" opacity=".05"/></pattern>
    <filter id="fBead" x="-5%" y="-5%" width="110%" height="110%"><feDropShadow dx=".8" dy="1.5" stdDeviation=".7" flood-color="#000" flood-opacity=".55"/></filter>
    <filter id="fSoft" x="-30%" y="-30%" width="160%" height="160%"><feGaussianBlur stdDeviation="9"/></filter>
    <filter id="fHaze" x="-30%" y="-60%" width="160%" height="220%"><feGaussianBlur stdDeviation="18"/></filter>
    <filter id="fGlow" x="-20%" y="-20%" width="140%" height="140%"><feGaussianBlur stdDeviation="4"/></filter>
    <filter id="fGrain" x="0" y="0" width="100%" height="100%"><feTurbulence type="fractalNoise" baseFrequency="1.1" numOctaves="2" stitchTiles="stitch"/><feColorMatrix type="saturate" values="0"/></filter>
    <linearGradient id="gDusk" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#0b0a1d"/><stop offset=".35" stop-color="#22122c"/><stop offset=".55" stop-color="#5a2230"/><stop offset=".64" stop-color="#b8502c"/><stop offset=".68" stop-color="#f08a3e"/></linearGradient>
    <radialGradient id="gFire" cx=".5" cy=".5" r=".5"><stop offset="0" stop-color="#ffc565" stop-opacity=".85"/><stop offset=".3" stop-color="#ff8a35" stop-opacity=".35"/><stop offset="1" stop-color="#ff6a1f" stop-opacity="0"/></radialGradient>
    <linearGradient id="gCloth2" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#6a3417"/><stop offset=".45" stop-color="#b7773f"/><stop offset="1" stop-color="#ecc996"/></linearGradient>
    <linearGradient id="gGround" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#2a1009"/><stop offset=".25" stop-color="#150805"/><stop offset="1" stop-color="#080302"/></linearGradient>
    <mask id="mMoon" maskUnits="userSpaceOnUse" x="300" y="58" width="40" height="40"><circle cx="318" cy="76" r="12" fill="#fff"/><circle cx="323.5" cy="71.5" r="11" fill="#000"/></mask>
    <filter id="linen" x="0" y="0" width="100%" height="100%">
      <feTurbulence type="fractalNoise" baseFrequency=".85 .55" numOctaves="2" stitchTiles="stitch"/>
      <feColorMatrix type="matrix" values="0 0 0 0 .55  0 0 0 0 .42  0 0 0 0 .32  0 0 0 1.4 -.35"/>
    </filter>
  </defs>
</svg>

<nav class="nav" data-section="nav" aria-label="Primary">
  <div class="nav-in">
    <a class="logo" href="#top" aria-label="Sundune Events, home">
      <svg viewBox="0 0 28 10" aria-hidden="true"><circle cx="5" cy="5" r="4" fill="#c0281e"/><circle cx="14" cy="5" r="4" fill="#f7efe4" stroke="rgba(0,0,0,.25)"/><circle cx="23" cy="5" r="4" fill="#2350a8"/></svg>Sundune
    </a>
    <ul class="nav-links">
      <li><a href="#experiences">Experiences</a></li>
      <li><a href="#approach">Approach</a></li>
      <li><a href="#season">2027 season</a></li>
      <li><a class="pill" href="#enquire"><span>Plan your event</span></a></li>
    </ul>
    <button class="menu-btn" type="button" aria-expanded="false" aria-controls="sheet"><i aria-hidden="true"></i>Menu</button>
  </div>
</nav>

<div class="sheet" id="sheet" role="dialog" aria-modal="true" aria-label="Menu">
  <div class="sheet-top"><span class="logo" style="font-size:28px">Sundune</span><button class="close" type="button">Close</button></div>
  <ul>
    <li><a href="#experiences">Experiences</a></li>
    <li><a href="#approach">Approach</a></li>
    <li><a href="#season">2027 season</a></li>
    <li><a href="#enquire">Plan your event</a></li>
  </ul>
  <p>Gatherings hosted with Maasai communities in Narok, Kajiado and Laikipia.</p>
</div>

<div class="spear-progress" aria-hidden="true">
  <svg viewBox="0 0 14 74" fill="currentColor"><path d="M7 0 L11 12 L7 18 L3 12Z"/><rect x="6.25" y="16" width="1.5" height="48"/><path d="M7 63 L8.6 68 L7 74 L5.4 68Z"/></svg>
</div>

<main id="top">
  <header class="hero" data-section="hero">
    <div class="hero-copy">
      <p class="place">Narok, Kajiado and Laikipia, Kenya</p>
      <h1 class="hero-title"><span class="lw"><span class="ln">Gatherings</span></span><span class="lw"><span class="ln">that rise.</span></span></h1>
      <p class="lede-hero">Festivals, retreats, ceremonies and galas, co-hosted with Maasai communities who lead every song, blessing and dance.</p>
      <div class="hero-ctas">
        <a class="btn btn-hero" href="#enquire">Plan your event</a>
        <a class="link-u" href="#season">See the 2027 season</a>
      </div>
      <p class="adumu-hint"><svg viewBox="0 0 14 74" fill="currentColor" aria-hidden="true"><path d="M7 0 L11 12 L7 18 L3 12Z"/><rect x="6.25" y="16" width="1.5" height="48"/><path d="M7 63 L8.6 68 L7 74 L5.4 68Z"/></svg>Tap a warrior to see the adumu, the jumping dance</p>
    </div>

    <div class="stage-window">
      <div class="stage" data-component="savanna-scene">
        <div class="layer" data-depth="4" aria-hidden="true">
          <svg viewBox="0 0 1672 940" preserveAspectRatio="none">
            <defs>
              <radialGradient id="sunGlow" cx="1108" cy="381" r="420" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#f7d3a0" stop-opacity=".9"/><stop offset=".35" stop-color="#f0bb80" stop-opacity=".35"/><stop offset="1" stop-color="#e19a57" stop-opacity="0"/>
              </radialGradient>
            </defs>
            <rect width="1672" height="940" fill="url(#sunGlow)"/>
            <circle class="sun" cx="1108" cy="381" r="130" fill="#f5c993" opacity=".92"/>
            <g class="cloud" fill="#f2b97c" opacity=".55">
              <path d="M1260 236 Q1300 214 1350 226 Q1390 206 1440 222 Q1500 210 1540 232 Q1600 230 1630 246 L1250 250Z"/>
              <path d="M1380 288 Q1420 272 1470 282 Q1520 270 1570 286 L1372 292Z"/>
            </g>
            <g class="cloud b" fill="#f4c28c" opacity=".5">
              <path d="M600 168 Q680 150 760 164 Q840 152 930 170 L590 174Z"/>
              <path d="M940 330 Q1000 316 1070 326 Q1130 318 1190 332 L930 336Z"/>
            </g>
          </svg>
        </div>
        <div class="layer" data-depth="8" aria-hidden="true">
          <svg viewBox="0 0 1672 940" preserveAspectRatio="none">
            <defs>
              <linearGradient id="mtn" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#c88a52"/><stop offset="1" stop-color="#dba46c"/></linearGradient>
              <linearGradient id="haze" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#efc08b" stop-opacity="0"/><stop offset=".55" stop-color="#efc08b" stop-opacity=".75"/><stop offset="1" stop-color="#e9b27a" stop-opacity=".35"/></linearGradient>
            </defs>
            <path d="M880 540 L1000 480 L1120 500 L1250 440 L1360 392 L1420 352 L1470 362 L1560 404 L1672 384 L1672 700 L880 700Z" fill="#d1945b"/>
            <path d="M1420 352 L1470 362 L1560 404 L1672 384 L1672 470 L1520 450 L1460 400Z" fill="#c07f48" opacity=".45"/>
            <path d="M-20 340 L40 312 L90 300 L150 290 L210 262 L300 220 L380 166 L470 128 L515 112 L548 132 L580 190 L640 232 L700 318 L790 380 L880 440 L980 484 L1060 524 L1110 562 L1110 720 L-20 720Z" fill="url(#mtn)"/>
            <path d="M515 112 L548 132 L580 190 L640 232 L700 318 L790 380 L880 440 L980 484 L760 452 L640 360 L560 250 L530 170Z" fill="#b5773f" opacity=".42"/>
            <path d="M470 128 L515 112 L505 200 L450 290 L400 360 L380 166Z" fill="#e6b47e" opacity=".32"/>
            <path d="M210 262 L300 220 L270 330 L180 400 L150 290Z" fill="#e2ad76" opacity=".25"/>
            <path d="M300 220 L380 166 L360 280 L300 360 L270 330Z" fill="#b97c45" opacity=".22"/>
            <path d="M1180 700 L1300 590 L1420 500 L1520 448 L1600 418 L1672 404 L1672 720 L1180 720Z" fill="#c78a52"/>
            <path d="M1520 448 L1600 418 L1672 404 L1672 560 L1560 520Z" fill="#b5773f" opacity=".35"/>
            <path d="M0 590 Q210 548 420 586 T 840 600 T 1260 606 T 1672 592 L1672 720 L0 720Z" fill="#d9a169"/>
            <rect y="470" width="1672" height="250" fill="url(#haze)"/>
          </svg>
        </div>
        <div class="layer" data-depth="12" aria-hidden="true">
          <svg viewBox="0 0 1672 940" preserveAspectRatio="none">
            <defs>
              <linearGradient id="ground" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#dfa466"/><stop offset=".45" stop-color="#cb8749"/><stop offset="1" stop-color="#a7643a"/></linearGradient>
            </defs>
            <path d="M0 668 Q400 652 836 660 T 1672 656 L1672 940 L0 940Z" fill="url(#ground)"/>
            <g fill="#9e6337" opacity=".5">
              <g transform="translate(70 668) scale(1.1)"><path d="M-2 0 L-1 -34 L-14 -52 L-12 -53 L0 -38 L10 -56 L12 -55 L2 -36 L2 0Z"/><path d="M-46 -52 Q-30 -66 -6 -62 Q8 -70 30 -64 Q46 -60 52 -52 Q26 -48 0 -50 Q-22 -48 -46 -52Z"/><path d="M-30 -62 Q-12 -74 10 -70 Q24 -72 34 -64 Q8 -60 -30 -62Z"/></g>
              <g transform="translate(176 676) scale(1.5)"><path d="M-2 0 L-1 -30 L-16 -48 L-14 -49 L0 -34 L12 -52 L14 -51 L2 -32 L2 0Z"/><path d="M-50 -48 Q-34 -62 -8 -58 Q8 -66 32 -60 Q50 -56 56 -48 Q28 -44 0 -46 Q-24 -44 -50 -48Z"/><path d="M-32 -58 Q-14 -70 10 -66 Q26 -68 38 -60 Q8 -56 -32 -58Z"/></g>
              <g transform="translate(286 670) scale(.85)"><path d="M-2 0 L-1 -30 L-14 -46 L-12 -47 L0 -33 L10 -50 L12 -49 L2 -31 L2 0Z"/><path d="M-44 -46 Q-28 -60 -6 -56 Q8 -64 28 -58 Q44 -54 50 -46 Q24 -42 0 -44 Q-20 -42 -44 -46Z"/></g>
              <g transform="translate(1508 668) scale(.8)"><path d="M-2 0 L-1 -30 L-14 -46 L-12 -47 L0 -33 L10 -50 L12 -49 L2 -31 L2 0Z"/><path d="M-44 -46 Q-28 -60 -6 -56 Q8 -64 28 -58 Q44 -54 50 -46 Q24 -42 0 -44 Q-20 -42 -44 -46Z"/></g>
            </g>
            <g fill="#8a5130" opacity=".4">
              <ellipse cx="420" cy="760" rx="160" ry="5"/><ellipse cx="1200" cy="790" rx="220" ry="6"/><ellipse cx="700" cy="860" rx="260" ry="7"/><ellipse cx="300" cy="900" rx="200" ry="6"/>
            </g>
            <g fill="#6e3f22" opacity=".65">
              <ellipse cx="560" cy="720" rx="9" ry="5"/><ellipse cx="760" cy="742" rx="6" ry="3.5"/><ellipse cx="1420" cy="760" rx="11" ry="6"/><ellipse cx="980" cy="826" rx="8" ry="4"/><ellipse cx="240" cy="780" rx="7" ry="4"/><ellipse cx="1560" cy="842" rx="9" ry="5"/>
            </g>
            <g stroke="#7c4a2a" stroke-width="2.4" stroke-linecap="round" fill="none" opacity=".7">
              <path d="M640 742 L630 712 M640 742 L644 706 M640 742 L656 714 M640 742 L620 724"/>
              <path d="M1080 756 L1072 730 M1080 756 L1084 724 M1080 756 L1096 732"/>
              <path d="M330 716 L322 694 M330 716 L334 690 M330 716 L346 698"/>
              <path d="M1330 720 L1324 700 M1330 720 L1334 696 M1330 720 L1346 704"/>
            </g>
          </svg>
        </div>
        <div class="layer" data-depth="14" aria-hidden="true">
          <svg viewBox="0 0 1672 940" preserveAspectRatio="none">
            <defs>
              <linearGradient id="word" x1="0" y1="541" x2="0" y2="773" gradientUnits="userSpaceOnUse">
                <stop offset="0" stop-color="#fff8f0"/><stop offset=".55" stop-color="#fde2c3"/><stop offset="1" stop-color="#f3b57b" stop-opacity=".75"/>
              </linearGradient>
            </defs>
            <text class="masai" x="600" y="773" textLength="1000" lengthAdjust="spacingAndGlyphs" font-family="'Archivo Black', 'Arial Black', sans-serif" font-size="322" fill="url(#word)">MAASAI</text>
          </svg>
        </div>
        <div class="layer" data-depth="16">
          <button class="warrior w-l" type="button" aria-label="Make the first warrior jump" data-lift="1.08">
            <span class="shadow" aria-hidden="true"></span>
            <span class="body"><svg viewBox="0 0 105 610" aria-hidden="true"><use href="#w-side"/></svg></span>
          </button>
          <button class="warrior w-s" type="button" aria-label="Make the second warrior jump" data-lift=".72">
            <span class="shadow" aria-hidden="true"></span>
            <span class="body"><svg viewBox="0 0 250 865" aria-hidden="true"><use href="#w-front"/></svg></span>
          </button>
          <button class="warrior w-b" type="button" aria-label="Make the third warrior jump" data-lift=".9">
            <span class="shadow" aria-hidden="true"></span>
            <span class="body"><svg class="flip" viewBox="0 0 250 865" aria-hidden="true"><use href="#w-front"/></svg></span>
          </button>
          <button class="warrior w-r" type="button" aria-label="Make the fourth warrior jump" data-lift="1.1">
            <span class="shadow" aria-hidden="true"></span>
            <span class="body"><svg class="flip" viewBox="0 0 105 610" aria-hidden="true"><use href="#w-side"/></svg></span>
          </button>
        </div>
        <div class="layer" data-depth="6" aria-hidden="true">
          <div class="flock">
            <svg viewBox="0 0 480 280" style="left:0;top:22%;--d:-.1s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:21%;top:4%;--d:-.3s;animation-delay:-.6s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:43%;top:-4%;--d:-.18s;animation-delay:-1.2s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:65%;top:-4%;--d:-.36s;animation-delay:-.3s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:11%;top:46%;--d:-.24s;animation-delay:-1.6s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:33%;top:62%;--d:-.06s;animation-delay:-.9s"><use href="#bird"/></svg>
            <svg viewBox="0 0 480 280" style="left:56%;top:80%;--d:-.3s;animation-delay:-2s"><use href="#bird"/></svg>
          </div>
        </div>
        <div class="layer" data-depth="26" aria-hidden="true">
          <div class="reed reed-1"><svg viewBox="0 0 110 840"><use href="#reed"/></svg></div>
          <div class="reed reed-2"><svg viewBox="0 0 110 840"><use href="#reed"/></svg></div>
          <div class="reed reed-3"><svg viewBox="0 0 110 840" style="transform:scaleX(-1)"><use href="#reed"/></svg></div>
          <svg class="clump" viewBox="0 0 1672 940" preserveAspectRatio="none" style="position:absolute;inset:0;width:100%;height:100%">
            <g data-clump="140,958,30,1"></g>
            <g class="b" data-clump="300,966,18,.7"></g>
            <g data-clump="1540,962,30,1.05"></g>
            <g class="b" data-clump="1420,970,16,.65"></g>
          </svg>
        </div>
      </div>
    </div>
    <svg class="grain" aria-hidden="true"><rect width="100%" height="100%" filter="url(#linen)"/></svg>
  </header>

  <!-- The frieze: words and warriors on shuka red; it moves as you scroll, and the warriors leap when you do -->
  <section class="frieze" data-section="frieze" aria-label="Story, song, fire, land, welcome">
    <div class="frieze-track" aria-hidden="true">
      <span class="frieze-word">Story</span><span class="sil side"><svg viewBox="0 0 105 610"><use href="#w-side"/></svg></span>
      <span class="frieze-word">Song</span><span class="sil front"><svg viewBox="0 0 250 865"><use href="#w-front"/></svg></span><span class="sil front flip"><svg viewBox="0 0 250 865"><use href="#w-front"/></svg></span>
      <span class="frieze-word">Fire</span><span class="sil side flip"><svg viewBox="0 0 105 610"><use href="#w-side"/></svg></span>
      <span class="frieze-word">Land</span><span class="sil front"><svg viewBox="0 0 250 865"><use href="#w-front"/></svg></span>
      <span class="frieze-word">Welcome</span><span class="sil side"><svg viewBox="0 0 105 610"><use href="#w-side"/></svg></span><span class="sil side flip"><svg viewBox="0 0 105 610"><use href="#w-side"/></svg></span>
    </div>
    <p class="frieze-note"><span>The adumu is danced by young men, each leaping as high as he can, straight-backed, heels never touching the ground.</span><span>Scroll to make them jump</span></p>
  </section>

  <section id="approach" class="approach" data-section="approach">
    <div class="wrap">
      <p class="label"><svg viewBox="0 0 22 14" aria-hidden="true"><path d="M2 2 L10 12 L20 2" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linejoin="round" stroke-linecap="round"/></svg>Our approach</p>
      <p class="scrub">We don’t stage culture. Every Sundune gathering is co-designed with Maasai community hosts, who set the terms, lead the ceremonies and are paid as partners, not performers.</p>
      <ul class="principles">
        <li>
          <svg viewBox="0 0 44 44" aria-hidden="true" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"><path d="M5 6 L22 26 L39 6"/><path d="M11 6 L22 19 L33 6" opacity=".55"/><circle cx="22" cy="35" r="4" fill="currentColor" stroke="none"/></svg>
          <h3>Community-led</h3><p>Elders and hosts shape every programme and can say no to anything in it.</p>
        </li>
        <li>
          <svg viewBox="0 0 44 44" aria-hidden="true" fill="currentColor"><path d="M22 2 L27 13 L22 19 L17 13Z"/><rect x="21" y="18" width="2" height="18"/><path d="M22 35 L24 39 L22 43 L20 39Z"/></svg>
          <h3>A fair share</h3><p>A fixed 30% of every fee goes straight to the host community’s own fund.</p>
        </li>
        <li>
          <svg viewBox="0 0 44 44" aria-hidden="true" fill="none" stroke="currentColor" stroke-width="2" stroke-linejoin="round"><path d="M14 3 L22 7 L19 36 L3 27Z"/><path d="M22 7 L33 11 L41 38 L20 20Z" fill="currentColor" fill-opacity=".35"/></svg>
          <h3>Light on the land</h3><p>Local suppliers, no single-use plastic, and every site left the way we found it.</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="experiences" class="experiences" data-section="experiences">
    <div class="wrap">
      <div class="sec-head">
        <h2>What we host</h2>
        <p>Four kinds of gathering, each designed with our community hosts around story, song, food and the land it happens on.</p>
      </div>
      <div class="exp-grid">
        <ul class="exp-list">
          <li class="exp on" data-i="0">
            <div class="exp-inline" aria-hidden="true"></div>
            <h3>Cultural festivals</h3>
            <p>Open-air days of music, beadwork, storytelling and food, led by the people whose culture it is.</p>
            <span class="meta">200 to 2,000 guests<br>One to three days</span>
          </li>
          <li class="exp" data-i="1">
            <div class="exp-inline" aria-hidden="true"></div>
            <h3>Leadership retreats</h3>
            <p>Three days on the plains for teams who want to slow down, listen to elders and talk about what lasts.</p>
            <span class="meta">12 to 60 guests<br>Two or three nights</span>
          </li>
          <li class="exp" data-i="2">
            <div class="exp-inline" aria-hidden="true"></div>
            <h3>Weddings and ceremonies</h3>
            <p>Celebrations that honour both families, with blessings, song and dress planned together with you.</p>
            <span class="meta">40 to 300 guests<br>One or two days</span>
          </li>
          <li class="exp" data-i="3">
            <div class="exp-inline" aria-hidden="true"></div>
            <h3>Sunset galas</h3>
            <p>Long tables under acacias, a choir at dusk and a fire that keeps going after the speeches stop.</p>
            <span class="meta">80 to 500 guests<br>One evening</span>
          </li>
        </ul>

        <div class="exp-stage" aria-hidden="true">
          <div class="frame">
            <!-- 0 Festival: a beaded collar laid flat on leather, every bead placed by the script -->
            <svg class="art on" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice">
              <rect width="400" height="500" fill="url(#gLeather)"/>
              <rect width="400" height="500" fill="url(#pShukaLt)"/>
              <circle cx="207" cy="228" r="100" fill="none" stroke="#000" stroke-width="100" opacity=".5" filter="url(#fSoft)"/>
              <g data-collar="200,218" filter="url(#fBead)"></g>
              <rect width="400" height="500" fill="url(#gVig)"/>
              <rect class="art-grain" width="400" height="500" filter="url(#fGrain)"/>
            </svg>
            <!-- 1 Retreat: first light over the Laikipia ridges, three walkers on the crest -->
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice">
              <rect width="400" height="500" fill="url(#gDawnSky)"/>
              <circle cx="252" cy="292" r="210" fill="url(#gSunHalo)"/>
              <circle cx="252" cy="292" r="56" fill="#fdeccc"/>
              <g fill="#fbe3bf" opacity=".6">
                <path d="M30 176 Q120 166 214 174 Q150 182 30 181Z"/><path d="M226 222 Q300 213 384 220 Q320 227 226 226Z"/><path d="M140 248 Q196 243 256 247 Q206 252 140 251Z" opacity=".7"/>
              </g>
              <g fill="none" stroke="#5a2a14" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" opacity=".7">
                <path d="M92 132 q5 -4 9 0 q4 -4 9 0"/><path d="M118 146 q4 -3 7 0 q3 -3 7 0"/><path d="M80 154 q3 -2.5 6 0 q3 -2.5 6 0"/>
              </g>
              <path d="M0 318 C60 300 110 292 170 302 S290 296 330 306 S390 300 400 304 L400 500 L0 500Z" fill="#e3a06a"/>
              <use href="#acacia" x="300" y="276" width="42" height="29" fill="#cf8752"/>
              <path d="M0 342 C70 326 130 318 200 330 S320 322 400 334 L400 500 L0 500Z" fill="#cd7f4a"/>
              <rect y="316" width="400" height="64" fill="url(#gMist)"/>
              <path d="M0 372 C80 352 150 350 230 362 S350 356 400 366 L400 500 L0 500Z" fill="#a45a2f"/>
              <use href="#acacia" x="8" y="245" width="170" height="115" fill="#5e2c15"/>
              <rect y="352" width="400" height="48" fill="url(#gMist)" opacity=".6"/>
              <path d="M0 410 C90 392 170 388 250 398 S360 396 400 404 L400 500 L0 500Z" fill="#6e3218"/>
              <g filter="url(#toInk)">
                <svg x="226" y="347" width="9" height="51" viewBox="0 0 105 610"><use href="#w-side"/></svg>
                <svg x="243" y="351" width="8.4" height="48" viewBox="0 0 105 610"><use href="#w-side"/></svg>
                <svg x="259" y="349" width="8.8" height="50" viewBox="0 0 105 610"><use href="#w-side"/></svg>
              </g>
              <path d="M0 452 C100 436 220 438 400 448 L400 500 L0 500Z" fill="#3e1a0b"/>
              <g stroke="#2a1006" stroke-width="2" stroke-linecap="round" fill="none">
                <path d="M28 476 l-6 -26 M32 476 l1 -30 M36 476 l8 -24"/><path d="M352 480 l-7 -22 M356 480 l0 -28 M360 480 l7 -20"/>
              </g>
              <rect width="400" height="500" fill="url(#gVig)" opacity=".7"/>
              <rect class="art-grain" width="400" height="500" filter="url(#fGrain)"/>
            </svg>
            <!-- 2 Ceremony: two beaded bangles, interlocked, on a shuka -->
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice">
              <rect width="400" height="500" fill="#931d14"/>
              <rect width="400" height="500" fill="url(#pCheck)"/>
              <rect width="400" height="500" fill="url(#pWeave)"/>
              <rect width="400" height="500" fill="url(#gPool)"/>
              <g fill="none" stroke="#000" stroke-width="30" opacity=".45" filter="url(#fSoft)"><circle cx="157" cy="231" r="74"/><circle cx="257" cy="231" r="74"/></g>
              <g data-bangles="150,222,250,222" filter="url(#fBead)"></g>
              <g data-loose="1" filter="url(#fBead)"></g>
              <rect width="400" height="500" fill="url(#gVig)"/>
              <rect class="art-grain" width="400" height="500" filter="url(#fGrain)"/>
            </svg>
            <!-- 3 Gala: a long dressed table running down to the fire, at dusk -->
            <svg class="art" viewBox="0 0 400 500" preserveAspectRatio="xMidYMid slice" data-gala="1">
              <rect width="400" height="500" fill="url(#gDusk)"/>
              <ellipse cx="190" cy="120" rx="260" ry="36" transform="rotate(-24 190 120)" fill="#e9dcf0" opacity=".07" filter="url(#fHaze)"/>
              <g data-stars="1"></g>
              <circle cx="318" cy="76" r="26" fill="#fbe9c8" opacity=".14" filter="url(#fGlow)"/>
              <circle cx="318" cy="76" r="12" fill="#fbe9c8" mask="url(#mMoon)"/>
              <path d="M0 300 C40 292 70 280 110 286 C150 292 170 274 210 279 C250 284 300 266 340 273 C370 278 390 270 400 274 L400 330 L0 330Z" fill="#3a1a26"/>
              <path d="M0 314 C60 306 120 310 170 306 C230 302 300 310 400 304 L400 330 L0 330Z" fill="#24100f"/>
              <ellipse cx="200" cy="322" rx="190" ry="70" fill="url(#gFire)"/>
              <path d="M0 324 Q200 316 400 322 L400 500 L0 500Z" fill="url(#gGround)"/>
              <g filter="url(#toInk)">
                <svg x="170" y="300" width="5.4" height="31" viewBox="0 0 105 610"><use href="#w-side"/></svg>
                <g transform="translate(456 0) scale(-1 1)"><svg x="226" y="301" width="5.2" height="30" viewBox="0 0 105 610"><use href="#w-side"/></svg></g>
              </g>
              <g class="fire">
                <ellipse cx="200" cy="318" rx="16" ry="22" fill="#ffb347" opacity=".55" filter="url(#fGlow)"/>
                <path d="M191 330 L209 327 M191 327 L209 330" stroke="#3a1a0c" stroke-width="1.4" stroke-linecap="round"/>
                <g transform="translate(200 329) scale(.72) translate(-200 -329)">
                <path class="flame" d="M200 296 C191 309 185 318 190 329 L210 329 C215 318 209 309 200 296Z" fill="#ffb347"/>
                <path class="flame b" d="M192 306 C185 316 183 323 186 329 L197 329 C194 321 196 314 192 306Z" fill="#ff7a24"/>
                <path class="flame b" d="M208 308 C215 317 217 324 214 329 L203 329 C206 321 204 315 208 308Z" fill="#ff7a24"/>
                <path class="flame" d="M200 311 C196 318 195 324 197 329 L203 329 C205 324 204 318 200 311Z" fill="#fff0c2"/>
                </g>
                <g data-sparks="1"></g>
              </g>
              <g data-table="1"></g>
              <g fill="#080302" transform="translate(-34 0)">
                <path d="M58 500 C60 430 52 380 64 330 C70 300 60 260 40 230 L46 226 C66 250 76 282 74 300 C86 270 110 240 140 220 L144 225 C116 248 92 280 82 320 C78 360 80 430 84 500Z"/>
                <path d="M40 230 C30 210 10 196 -10 190 L-8 184 C14 190 34 204 46 222Z"/><path d="M140 220 C156 206 170 196 186 192 L188 197 C172 202 156 212 144 226Z"/><path d="M64 300 C60 270 70 230 96 200 L100 204 C78 230 70 262 72 290Z"/>
                <path d="M-40 192 Q-10 170 30 174 Q60 162 100 168 Q140 162 170 174 Q200 172 216 188 Q186 197 150 193 Q120 201 90 195 Q50 203 20 197 Q-10 203 -40 192Z"/>
                <path d="M6 172 Q40 152 80 156 Q120 148 164 164 Q130 170 90 166 Q50 174 6 172Z"/>
                <path d="M54 202 Q90 191 130 197 Q162 195 194 206 Q160 212 130 208 Q96 214 54 202Z"/>
              </g>
              <g data-strings="1"></g>
              <rect width="400" height="500" fill="url(#gVig)"/>
              <rect class="art-grain" width="400" height="500" filter="url(#fGrain)"/>
            </svg>
          </div>
          <p class="cap"><span class="cap-text">A beaded collar in the six colours, laid flat</span><span>Drawn in code</span></p>
        </div>
      </div>
    </div>
  </section>

  <section class="ledger" data-section="stats" aria-label="Sundune in numbers">
    <div class="wrap">
      <p class="ledger-text">Since 2019 we’ve hosted <span class="n" data-to="140">140</span> gatherings for <span class="n" data-to="9400">9,400</span> guests, with <span class="n" data-to="6">6</span> partner communities.</p>
      <div class="share" data-inview>
        <div class="share-beads" role="img" aria-label="Three of ten beads filled: 30 percent">
          <i class="f"></i><i class="f"></i><i class="f"></i><i></i><i></i><i></i><i></i><i></i><i></i><i></i>
        </div>
        <p><strong>30% of every fee</strong> goes straight to the host community’s own fund, agreed in writing before we plan anything.</p>
      </div>
    </div>
  </section>

  <div class="spears" aria-hidden="true"></div>

  <section id="season" class="season" data-section="season">
    <div class="wrap">
      <div class="sec-head">
        <h2>The 2027 season</h2>
        <p>Six open gatherings anyone can join. Private events run all year. Each strand of beads shows how many places are taken.</p>
      </div>
      <ol class="dates">
        <li class="date">
          <span class="when">14–16 Mar</span>
          <div class="what"><h3>Leadership retreat</h3><p>Laikipia plateau, three nights</p></div>
          <span class="strand" data-taken="20" data-total="24"></span>
          <span class="status hot">4 places left</span>
          <a class="btn-sm" href="#enquire" data-occasion="Leadership retreat" data-month="March 2027">Enquire</a>
        </li>
        <li class="date">
          <span class="when">25 Apr</span>
          <div class="what"><h3>Cultural festival</h3><p>Narok, one day, open to all</p></div>
          <span class="strand" data-taken="380" data-total="1200"></span>
          <span class="status">Open</span>
          <a class="btn-sm" href="#enquire" data-occasion="Cultural festival" data-month="April 2027">Enquire</a>
        </li>
        <li class="date">
          <span class="when">6–8 Jun</span>
          <div class="what"><h3>Leadership retreat</h3><p>Loita Hills, two nights</p></div>
          <span class="strand" data-taken="18" data-total="18"></span>
          <span class="status">Full, waitlist open</span>
          <a class="btn-sm" href="#enquire" data-occasion="Leadership retreat" data-month="June 2027">Join waitlist</a>
        </li>
        <li class="date">
          <span class="when">22 Aug</span>
          <div class="what"><h3>Sunset gala</h3><p>Kajiado, under the acacias</p></div>
          <span class="strand" data-taken="180" data-total="220"></span>
          <span class="status hot">40 places left</span>
          <a class="btn-sm" href="#enquire" data-occasion="Sunset gala" data-month="August 2027">Enquire</a>
        </li>
        <li class="date">
          <span class="when">18–20 Sep</span>
          <div class="what"><h3>Cultural festival</h3><p>Narok, three days</p></div>
          <span class="strand" data-taken="900" data-total="2000"></span>
          <span class="status">Open</span>
          <a class="btn-sm" href="#enquire" data-occasion="Cultural festival" data-month="September 2027">Enquire</a>
        </li>
        <li class="date">
          <span class="when">4 Dec</span>
          <div class="what"><h3>Sunset gala</h3><p>Laikipia, the year’s last fire</p></div>
          <span class="strand" data-taken="200" data-total="200"></span>
          <span class="status">Full, waitlist open</span>
          <a class="btn-sm" href="#enquire" data-occasion="Sunset gala" data-month="December 2027">Join waitlist</a>
        </li>
      </ol>
    </div>
  </section>

  <section id="process" class="process" data-section="process">
    <div class="wrap">
      <h2>From first call to last song</h2>
      <ol class="steps" data-inview>
        <li><span class="num">1</span><h3>Tell us the occasion</h3><p>Who is coming, what you are marking and what you hope people carry home.</p></li>
        <li><span class="num">2</span><h3>Design it together</h3><p>We visit with our community hosts and shape the programme, the site and the food with you.</p></li>
        <li><span class="num">3</span><h3>Gather</h3><p>We run everything on the day, from transport to the last fire, so you can be a guest at your own event.</p></li>
      </ol>
    </div>
  </section>

  <section class="voice" data-section="testimonial" aria-label="What a client said">
    <div class="wrap">
      <figure>
        <span class="collar" aria-hidden="true"></span>
        <blockquote>“Nobody performed for us. We were welcomed, and that is the difference our team still talks about.”</blockquote>
        <figcaption><b>Amara Okafor</b>Head of People at a fictional client, leadership retreat in Laikipia</figcaption>
      </figure>
    </div>
  </section>

  <section id="enquire" class="enquire" data-section="cta">
    <div class="wrap enq-grid">
      <div>
        <h2>Let’s plan something that lasts</h2>
        <p class="enq-lede">Tell us a little and we’ll come back within two working days with ideas and a first estimate.</p>
        <div class="enq-warrior" aria-hidden="true"><span class="shadow"></span><span class="body"><svg viewBox="0 0 250 865"><use href="#w-front"/></svg></span></div>
      </div>
      <form class="form" id="enquiry" novalidate>
        <fieldset>
          <legend class="field-label">Occasion</legend>
          <div class="chips">
            <label class="chip"><input type="radio" name="occasion" value="Cultural festival" checked><span>Cultural festival</span></label>
            <label class="chip"><input type="radio" name="occasion" value="Leadership retreat"><span>Leadership retreat</span></label>
            <label class="chip"><input type="radio" name="occasion" value="Wedding or ceremony"><span>Wedding or ceremony</span></label>
            <label class="chip"><input type="radio" name="occasion" value="Sunset gala"><span>Sunset gala</span></label>
          </div>
        </fieldset>
        <div>
          <div class="range-row"><label class="field-label" for="guests">Guests</label><output id="guests-out" for="guests">80</output></div>
          <input id="guests" name="guests" type="range" min="10" max="2000" step="10" value="80">
        </div>
        <div>
          <label class="field-label" for="month">When</label>
          <select class="line-input" id="month" name="month">
            <option>Any time in 2027</option><option>January 2027</option><option>February 2027</option><option>March 2027</option><option>April 2027</option><option>May 2027</option><option>June 2027</option>
            <option>July 2027</option><option>August 2027</option><option>September 2027</option><option>October 2027</option><option>November 2027</option><option>December 2027</option>
          </select>
        </div>
        <div class="two">
          <div><label class="field-label" for="name">Your name</label><input class="line-input" id="name" name="name" autocomplete="name" required></div>
          <div><label class="field-label" for="email">Email</label><input class="line-input" id="email" name="email" type="email" autocomplete="email" placeholder="you@company.example" required></div>
        </div>
        <div class="submit-row">
          <button class="btn btn-light" type="submit">Send enquiry</button>
          <p class="form-msg" id="form-msg" role="status"></p>
        </div>
      </form>
    </div>
  </section>
</main>

<footer data-section="footer">
  <div class="wrap">
    <div class="foot-cols">
      <div><h3>Sundune Events</h3><p>Gatherings co-hosted with Maasai communities in Narok, Kajiado and Laikipia.</p></div>
      <div><h3>Visit</h3><p>Studio 4, Ngong Road<br>Nairobi, Kenya</p></div>
      <div><h3>Write</h3><ul><li><a href="#enquire">hello@sundune.example</a></li><li><a href="#enquire">press@sundune.example</a></li></ul></div>
      <div><h3>Explore</h3><ul><li><a href="#experiences">Experiences</a></li><li><a href="#approach">Approach</a></li><li><a href="#season">2027 season</a></li></ul></div>
    </div>
    <span class="wordmark" aria-hidden="true">Sundune</span>
    <div class="legal">
      <p>© 2026 Sundune Events. Sundune, its clients, partners, dates and numbers are fictional. Hero recreated in SVG and CSS from the “Maasai-Inspired Event Hero Banner Concept” on the Rive Marketplace; every texture on this page is cut from those warriors’ own shapes.</p>
      <button class="to-top" type="button">Back to top</button>
    </div>
  </div>
</footer>

<script>
(function () {
  var root = document.documentElement;
  root.classList.add('js');
  var reduced = matchMedia('(prefers-reduced-motion: reduce)');
  var hero = document.querySelector('.hero');

  /* 0. Textures cut from the warriors. Shuka: the three cloth panels and edge of #w-front, moved to the origin and mirrored.
        Spear: the tip, shaft and butt of #w-side. Collar: the beaded V of #w-front. */
  function uri(svg) { return 'url("data:image/svg+xml,' + encodeURIComponent(svg) + '")'; }
  var FOLD = '<path d="M58 5 L96 23 L80 255 L4 183Z"/><path d="M96 23 L145 43 L180 260 L88 135Z" fill-opacity=".5" fill="C"/><path d="M88 135 L142 205 L102 330 L80 255Z"/>';
  function shuka(c, op) {
    var f = FOLD.replace('C', c);
    return '<svg xmlns="http://www.w3.org/2000/svg" width="360" height="340" viewBox="0 0 360 340"><g fill="none" stroke="' + c + '" stroke-opacity="' + op + '" stroke-width="3" stroke-linejoin="round">' +
      f + '<g transform="translate(360 0) scale(-1 1)">' + f + '</g></g></svg>';
  }
  root.style.setProperty('--m-shuka', uri(shuka('#000', 1)));
  root.style.setProperty('--img-shuka', uri(shuka('#1c0b06', .6)));
  root.style.setProperty('--m-spear', uri('<svg xmlns="http://www.w3.org/2000/svg" width="120" height="340" viewBox="0 0 120 340"><path d="M60 0 L67 30 L60 44 L53 30Z"/><rect x="58.5" y="42" width="3" height="252"/><path d="M60 296 L63 312 L60 334 L57 312Z"/></svg>'));
  root.style.setProperty('--m-collar', uri('<svg xmlns="http://www.w3.org/2000/svg" width="40" height="24" viewBox="0 0 40 24"><path d="M3 3 L19 21 L37 3" fill="none" stroke="#000" stroke-width="3.4" stroke-linejoin="round" stroke-linecap="round"/></svg>'));

  /* 1. The adumu: crouch, straight-legged spring, hang, land. Shared by the hero, the frieze and the enquiry warrior. */
  function leap(body, shadow, lift, dur) {
    dur = dur || 1150;
    var a = body.animate([
      { transform: 'translateY(0) scaleY(1)', easing: 'ease-out' },
      { transform: 'translateY(2%) scaleY(.93)', offset: .14, easing: 'cubic-bezier(.15,.8,.35,1)' },
      { transform: 'translateY(' + lift + '%) scaleY(1.03)', offset: .42, easing: 'linear' },
      { transform: 'translateY(' + (lift - 3) + '%) scaleY(1)', offset: .54, easing: 'cubic-bezier(.55,0,.85,.4)' },
      { transform: 'translateY(1.5%) scaleY(.95)', offset: .86, easing: 'ease-out' },
      { transform: 'translateY(0) scaleY(1)' }
    ], { duration: dur });
    if (shadow) shadow.animate([
      { transform: 'scale(1)', opacity: 1 }, { transform: 'scale(1.1)', opacity: 1, offset: .14 },
      { transform: 'scale(.45)', opacity: .35, offset: .45 }, { transform: 'scale(.42)', opacity: .3, offset: .54 },
      { transform: 'scale(1.05)', opacity: 1, offset: .86 }, { transform: 'scale(1)', opacity: 1 }
    ], { duration: dur });
    return a;
  }
  var warriors = Array.prototype.slice.call(document.querySelectorAll('.warrior'));
  var lastTouch = 0;
  function jump(w) {
    if (w.dataset.busy) return;
    w.dataset.busy = '1';
    leap(w.querySelector('.body'), w.querySelector('.shadow'), -62 * parseFloat(w.dataset.lift || 1)).onfinish = function () { delete w.dataset.busy; };
  }
  warriors.forEach(function (w) { w.addEventListener('click', function () { lastTouch = Date.now(); jump(w); }); });
  // One orchestrated moment on load: once the word has risen, the four leap left to right
  if (!reduced.matches) setTimeout(function () { warriors.forEach(function (w, i) { setTimeout(function () { jump(w); }, i * 170); }); }, 1700);
  var prev = -1;
  (function ambient() {
    setTimeout(function () {
      if (!reduced.matches && !hero.classList.contains('paused') && !document.hidden && Date.now() - lastTouch > 9000) {
        var i; do { i = Math.floor(Math.random() * warriors.length); } while (i === prev);
        prev = i; jump(warriors[i]);
      }
      ambient();
    }, 9000 + Math.random() * 4000);
  })();

  /* 2. Seeded randomness for the grass, the bead rings and the stars */
  var seed = 7;
  function rnd() { seed = (seed * 16807) % 2147483647; return (seed - 1) / 2147483646; }
  var NS = 'http://www.w3.org/2000/svg';
  document.querySelectorAll('[data-clump]').forEach(function (g) {
    var p = g.dataset.clump.split(',').map(Number), bx = p[0], by = p[1], n = p[2], s = p[3];
    var cols = ['#2c170f', '#3b2016', '#4c2a1c', '#5d3624'], html = '';
    for (var i = 0; i < n; i++) {
      var ang = (-80 + 160 * (i / (n - 1)) + (rnd() - .5) * 16) * Math.PI / 180;
      var len = (150 + rnd() * 170) * s * (1 - Math.abs(ang) * .28), w = (9 + rnd() * 7) * s;
      var tx = bx + Math.sin(ang) * len, ty = by - Math.cos(ang) * len;
      var bend = (ang > 0 ? 1 : -1) * len * (.18 + rnd() * .2);
      var cx = bx + Math.sin(ang) * len * .55 + bend * .35, cy = by - Math.cos(ang) * len * .55 + Math.abs(bend) * .25;
      html += '<path fill="' + cols[Math.floor(rnd() * cols.length)] + '" d="M' + (bx - w) + ' ' + by + ' Q' + (cx - w * .4) + ' ' + cy + ' ' +
        (tx + bend * .2) + ' ' + (ty + Math.abs(bend) * .3) + ' Q' + (cx + w * .4) + ' ' + cy + ' ' + (bx + w) + ' ' + by + 'Z"/>';
    }
    g.innerHTML = html;
  });

  /* 3. Generated art: every bead, star, bulb and candle is placed here */
  var COL = { W: '#f3ebdd', R: '#c0281e', B: '#2350a8', O: '#e57a1f', G: '#2f8a4c', Y: '#f2c230' };
  function f1(v) { return (+v).toFixed(1); }
  function bead(x, y, r, c) {
    var p = 'cx="' + f1(x) + '" cy="' + f1(y) + '" r="' + f1(r) + '"';
    return '<circle ' + p + ' fill="' + c + '"/><circle ' + p + ' fill="url(#gGloss)"/>';
  }
  function star(x, y, r, o) { return '<circle cx="' + f1(x) + '" cy="' + f1(y) + '" r="' + r.toFixed(2) + '" fill="#fff4e2" opacity="' + o.toFixed(2) + '"/>'; }
  function seq(pat) { var out = []; pat.forEach(function (p) { for (var k = 0; k < p[1]; k++) out.push(COL[p[0]]); }); return out; }
  // One row of beads round a circle. gap leaves the collar's opening at the top; keep limits which beads are drawn.
  function row(cx, cy, R, r, pat, opt) {
    opt = opt || {};
    var sq = seq(pat), n = Math.floor(2 * Math.PI * R / (2 * r + .9)), out = '';
    for (var k = 0; k < n; k++) {
      var a = k / n * Math.PI * 2 + (opt.phase || 0), d = a + Math.PI / 2;
      if (opt.gap && Math.abs(Math.atan2(Math.sin(d), Math.cos(d))) < opt.gap) continue;
      if (opt.keep && !opt.keep(a)) continue;
      out += bead(cx + Math.cos(a) * R, cy + Math.sin(a) * R, r, sq[k % sq.length]);
    }
    return out;
  }
  // The collar: nine rings in colour blocks, open at the neck, with a fringe of bead strands ending in metal drops
  var RINGS = [[['W',1]], [['R',4],['W',1],['B',4],['W',1]], [['O',1]], [['W',1]], [['G',3],['Y',3],['R',3]], [['B',1]], [['W',2],['R',6]], [['Y',1]], [['R',5],['W',1],['O',5],['W',1]]];
  document.querySelectorAll('[data-collar]').forEach(function (g) {
    var c = g.dataset.collar.split(',').map(Number), out = '', R = 58 + 8 * 10.2;
    RINGS.forEach(function (p, i) { out += row(c[0], c[1], 58 + i * 10.2, 4.7, p, { gap: .14 }); });
    for (var i = 0, a; (a = 26 + i * 6.4) <= 154; i++) {
      var t = a * Math.PI / 180, ca = Math.cos(t), sa = Math.sin(t), n = i % 2 ? 4 : 3, d = R + n * 6.4 + 8;
      out += '<path d="M' + f1(c[0] + ca * R) + ' ' + f1(c[1] + sa * R) + ' L' + f1(c[0] + ca * d) + ' ' + f1(c[1] + sa * d) + '" stroke="#2a160c" stroke-width=".8"/>';
      for (var k = 1; k <= n; k++) out += bead(c[0] + ca * (R + k * 6.4), c[1] + sa * (R + k * 6.4), 2.9, k % 2 ? COL.W : COL.R);
      out += '<ellipse cx="' + f1(c[0] + ca * d) + '" cy="' + f1(c[1] + sa * d) + '" rx="3.7" ry="5.6" transform="rotate(' + (a - 90) + ' ' + f1(c[0] + ca * d) + ' ' + f1(c[1] + sa * d) + ')" fill="url(#gMetal)" stroke="#4d4339" stroke-width=".6"/>';
    }
    g.innerHTML = out;
  });
  // The bangles: A is drawn, then B, then A's beads at the top crossing again, so the two read as linked
  document.querySelectorAll('[data-bangles]').forEach(function (g) {
    var c = g.dataset.bangles.split(',').map(Number), top = Math.atan2(-54, (c[2] - c[0]) / 2);
    function ringA(keep) { return row(c[0], c[1], 80, 5.8, [['W',4],['B',2]], { keep: keep }) + row(c[0], c[1], 67, 4.6, [['O',1]], { keep: keep, phase: .04 }); }
    function near(a) { var d = a - top; return Math.abs(Math.atan2(Math.sin(d), Math.cos(d))) < .4; }
    g.innerHTML = ringA() + row(c[2], c[3], 80, 5.8, [['B',3],['W',1]]) + row(c[2], c[3], 67, 4.6, [['W',2],['R',2]], { phase: .04 }) + ringA(near);
  });
  document.querySelectorAll('[data-loose]').forEach(function (g) {
    var out = '', keys = 'WRBOGY';
    // A short loose strand trailing off the bangles, then three strays
    for (var i = 0; i < 12; i++) {
      var t = i / 11, x = 196 + t * 128, y = 352 + Math.sin(t * Math.PI * 1.2) * 34 + t * 30;
      out += bead(x, y, 4.6, COL[keys[(i * 2) % 6]]);
    }
    [[344, 430], [330, 452], [358, 458]].forEach(function (p, i) { out += bead(p[0], p[1], 4.6, COL[keys[i + 1]]); });
    g.innerHTML = out;
  });
  // The gala: the table, its settings and guests, the lights and the sparks, all drawn in true perspective.
  // z is distance down the table (1 = nearest row); the table vanishes at the fire on the horizon (y 318).
  document.querySelectorAll('[data-gala]').forEach(function (svg) {
    var HZ = 318, i;
    function Y(z, h) { return HZ + (182 - (h || 0)) / z; }   // h: height above the cloth, in near-row pixels
    function X(x, z) { return 200 + x * 130 / z; }
    function pt(x, z, h) { return f1(X(x, z)) + ' ' + f1(Y(z, h)); }

    var stars = '';
    for (i = 0; i < 150; i++) { var sy = rnd() * 250; stars += star(rnd() * 400, sy, .35 + rnd() * 1, (.2 + rnd() * .7) * (1 - sy / 300)); }
    [[64, 50], [250, 36], [150, 112], [372, 150]].forEach(function (p) {
      stars += '<path d="M' + (p[0] - 6) + ' ' + p[1] + 'h12M' + p[0] + ' ' + (p[1] - 6) + 'v12" stroke="#fff4e2" stroke-width=".5" opacity=".75"/>' + star(p[0], p[1], 1.3, 1);
    });
    svg.querySelector('[data-stars]').innerHTML = stars;

    var sparks = '';
    for (i = 0; i < 14; i++) {
      sparks += '<circle class="spark" style="--dx:' + ((rnd() - .5) * 30).toFixed(1) + 'px;animation-delay:-' + (rnd() * 2.8).toFixed(2) + 's;animation-duration:' + (2.2 + rnd() * 1.6).toFixed(2) + 's" cx="' + f1(196 + rnd() * 8) + '" cy="' + f1(302 + rnd() * 8) + '" r="' + (.6 + rnd() * .7).toFixed(2) + '" fill="#ffd27a"/>';
    }
    svg.querySelector('[data-sparks]').innerHTML = sparks;

    // Cloth, a shuka runner with its stripes converging on the fire, then the rows from far to near
    var out = '<path d="M' + pt(-1, 10) + ' L' + pt(1, 10) + ' L' + pt(1, .96) + ' L' + pt(-1, .96) + 'Z" fill="url(#gCloth2)"/>';
    out += '<path d="M' + pt(-1, 10) + ' L' + pt(-1, .96) + ' M' + pt(1, 10) + ' L' + pt(1, .96) + '" stroke="#ffd9a6" stroke-opacity=".45" stroke-width="1.2"/>';
    out += '<path d="M' + pt(-.14, 10) + ' L' + pt(.14, 10) + ' L' + pt(.14, .96) + ' L' + pt(-.14, .96) + 'Z" fill="#a8241b"/>';
    [[-.1, '#f2c230', .55], [.1, '#f2c230', .55], [-.05, '#1f3f86', .8], [.05, '#1f3f86', .8], [0, '#160604', .5]].forEach(function (l) {
      out += '<path d="M' + pt(l[0], 10) + ' L' + pt(l[0], .96) + '" stroke="' + l[1] + '" stroke-opacity="' + l[2] + '" stroke-width="1.1"/>';
    });
    var pools = '', rows = '';
    var ZS = [1.12, 1.42, 1.82, 2.36, 3.05, 4, 5.3, 7.1];
    for (var r = ZS.length - 1; r >= 0; r--) {
      var z = ZS[r], s = 1 / z, row = '';
      [-1, 1].forEach(function (side) {
        // chair, and a guest in most of them, rim-lit on the side facing the candles
        var cx = X(side * 1.16, z), base = Y(z) + 6 * s, rim = -side * 1.6 * s;
        row += '<path d="M' + f1(cx - 13 * s) + ' ' + f1(base) + ' L' + f1(cx - 13 * s) + ' ' + f1(base - 52 * s) + ' Q' + f1(cx) + ' ' + f1(base - 64 * s) + ' ' + f1(cx + 13 * s) + ' ' + f1(base - 52 * s) + ' L' + f1(cx + 13 * s) + ' ' + f1(base) + 'Z" fill="#160905"/>';
        if ((r + (side > 0 ? 1 : 0)) % 3 !== 0) {
          var hx = cx + side * 3 * s, hy = base - 62 * s, sh = 'M' + f1(hx - 17 * s) + ' ' + f1(base - 14 * s) + ' Q' + f1(hx - 18 * s) + ' ' + f1(base - 44 * s) + ' ' + f1(hx) + ' ' + f1(base - 46 * s) + ' Q' + f1(hx + 18 * s) + ' ' + f1(base - 44 * s) + ' ' + f1(hx + 17 * s) + ' ' + f1(base - 14 * s) + 'Z';
          row += '<g transform="translate(' + f1(rim) + ' 0)" fill="#ff9e52" opacity=".55"><path d="' + sh + '"/><circle cx="' + f1(hx) + '" cy="' + f1(hy) + '" r="' + f1(10 * s) + '"/></g>';
          row += '<g fill="#0a0403"><path d="' + sh + '"/><circle cx="' + f1(hx) + '" cy="' + f1(hy) + '" r="' + f1(10 * s) + '"/>';
          if (r % 2) row += '<path d="M' + f1(hx - 9 * s) + ' ' + f1(base - 44 * s) + ' Q' + f1(hx) + ' ' + f1(base - 34 * s) + ' ' + f1(hx + 9 * s) + ' ' + f1(base - 44 * s) + '" fill="none" stroke="' + (side > 0 ? '#c0281e' : '#2350a8') + '" stroke-width="' + f1(2.6 * s) + '"/>';
          row += '</g>';
        }
        // plate, then a glass catching the light
        var px = X(side * .6, z), py = Y(z, 3);
        row += '<ellipse cx="' + f1(px) + '" cy="' + f1(py) + '" rx="' + f1(15 * s) + '" ry="' + f1(5.2 * s) + '" fill="#f3e6d0"/><ellipse cx="' + f1(px) + '" cy="' + f1(py) + '" rx="' + f1(9.5 * s) + '" ry="' + f1(3.2 * s) + '" fill="#e2c9a6"/>';
        var gx = X(side * .4, z + .12), gy = Y(z + .12);
        row += '<path d="M' + f1(gx) + ' ' + f1(gy) + 'v' + f1(-7 * s) + '" stroke="#ffe6b8" stroke-opacity=".7" stroke-width="' + f1(.9 * s) + '"/><path d="M' + f1(gx - 3.4 * s) + ' ' + f1(gy - 15 * s) + ' Q' + f1(gx - 3.4 * s) + ' ' + f1(gy - 7 * s) + ' ' + f1(gx) + ' ' + f1(gy - 7 * s) + ' Q' + f1(gx + 3.4 * s) + ' ' + f1(gy - 7 * s) + ' ' + f1(gx + 3.4 * s) + ' ' + f1(gy - 15 * s) + '" fill="#ffe2ad" fill-opacity=".28" stroke="#fff1d2" stroke-opacity=".7" stroke-width="' + f1(.7 * s) + '"/>';
        // a hurricane candle between the settings
        var cz = z + .3, cs = 1 / cz, kx = X(side * .25, cz), ky = Y(cz);
        pools += '<circle cx="' + f1(kx) + '" cy="' + f1(ky - 8 * cs) + '" r="' + f1(20 * cs) + '" fill="#ff9d45" opacity=".4"/><ellipse cx="' + f1(kx) + '" cy="' + f1(ky) + '" rx="' + f1(30 * cs) + '" ry="' + f1(7 * cs) + '" fill="#ffc070" opacity=".5"/>';
        row += '<rect x="' + f1(kx - 1.6 * cs) + '" y="' + f1(ky - 8 * cs) + '" width="' + f1(3.2 * cs) + '" height="' + f1(8 * cs) + '" fill="#f4e6cc"/>' +
          '<ellipse class="flicker" style="animation-delay:-' + (rnd() * 1.8).toFixed(2) + 's" cx="' + f1(kx) + '" cy="' + f1(ky - 10.6 * cs) + '" rx="' + f1(1.6 * cs) + '" ry="' + f1(3.2 * cs) + '" fill="#ffd27a"/>' +
          '<rect x="' + f1(kx - 5 * cs) + '" y="' + f1(ky - 20 * cs) + '" width="' + f1(10 * cs) + '" height="' + f1(20 * cs) + '" rx="' + f1(4 * cs) + '" fill="#fff" fill-opacity=".06" stroke="#fff4dd" stroke-opacity=".35" stroke-width="' + f1(.6 * cs) + '"/>';
      });
      rows += row;
    }
    svg.querySelector('[data-table]').innerHTML = out + '<g filter="url(#fGlow)">' + pools + '</g>' + rows;

    // Two strings of lights on posts down both sides, sagging between posts and converging on the fire
    var POSTS = [.88, 1.5, 2.5, 4.2, 7, 11], wire = '', glow = '', bulbs = '', posts = '';
    [-1, 1].forEach(function (side) {
      for (var p = 0; p < POSTS.length; p++) {
        var z = POSTS[p];
        posts += '<path d="M' + pt(side * 1.38, z, -4) + ' L' + pt(side * 1.38, z, 300) + '" stroke="#0a0403" stroke-width="' + f1(3 / z) + '"/>';
        if (p === POSTS.length - 1) break;
        var z2 = POSTS[p + 1], ax = X(side * 1.38, z), ay = Y(z, 300), bx = X(side * 1.38, z2), by = Y(z2, 300);
        var mx = (ax + bx) / 2, my = (ay + by) / 2 + 22 / ((z + z2) / 2);
        wire += '<path d="M' + f1(ax) + ' ' + f1(ay) + 'Q' + f1(mx) + ' ' + f1(my * 2 - (ay + by) / 2) + ' ' + f1(bx) + ' ' + f1(by) + '" fill="none" stroke="#120604" stroke-width="' + f1(.9 / Math.sqrt(z)) + '"/>';
        var qx = mx, qy = my * 2 - (ay + by) / 2;
        for (var k = 1; k < 6; k++) {
          var t = k / 6, u = 1 - t, x = u * u * ax + 2 * u * t * qx + t * t * bx, y = u * u * ay + 2 * u * t * qy + t * t * by, br = 2.4 / Math.sqrt(z + t * (z2 - z));
          glow += '<circle cx="' + f1(x) + '" cy="' + f1(y + br) + '" r="' + f1(br * 3.2) + '" fill="#ffc56e" opacity=".55"/>';
          bulbs += '<circle cx="' + f1(x) + '" cy="' + f1(y + br) + '" r="' + f1(br) + '" fill="#fff0c8"/>';
        }
      }
    });
    svg.querySelector('[data-strings]').innerHTML = posts + wire + '<g filter="url(#fGlow)">' + glow + '</g>' + bulbs;
  });

  /* 4. Experiences: hover or scroll a row to show its art; on phones each row carries its own copy */
  var rows = Array.prototype.slice.call(document.querySelectorAll('.exp'));
  var arts = Array.prototype.slice.call(document.querySelectorAll('.frame .art'));
  var capText = document.querySelector('.cap-text');
  var CAPS = ['A beaded collar in the six colours, laid flat', 'First light on the Laikipia plateau', 'Two bangles, two families, one shuka', 'A long table set down to the fire, at dusk'];
  function setActive(i) {
    rows.forEach(function (r, k) { r.classList.toggle('on', k === i); });
    arts.forEach(function (a, k) { a.classList.toggle('on', k === i); });
    capText.textContent = CAPS[i];
  }
  rows.forEach(function (r, i) {
    var clone = arts[i].cloneNode(true);
    clone.classList.add('on'); clone.removeAttribute('class');
    r.querySelector('.exp-inline').appendChild(clone);
    r.addEventListener('mouseenter', function () { setActive(i); });
  });

  /* 5. Season: bead strands, 12 beads each, filled for places taken */
  document.querySelectorAll('.strand').forEach(function (s) {
    var t = +s.dataset.taken, n = +s.dataset.total, f = Math.round(t / n * 12), out = '';
    for (var i = 0; i < 12; i++) out += '<i' + (i < f ? ' class="f"' : '') + '></i>';
    s.innerHTML = out;
    s.setAttribute('role', 'img');
    s.setAttribute('aria-label', t.toLocaleString('en-GB') + ' of ' + n.toLocaleString('en-GB') + ' places taken');
  });

  /* 6. Manifesto: words light up as you read down */
  var scrub = document.querySelector('.scrub'), words = [];
  scrub.innerHTML = scrub.textContent.trim().split(/\s+/).map(function (w) { return '<span class="w">' + w + '</span>'; }).join(' ');
  words = Array.prototype.slice.call(scrub.querySelectorAll('.w'));

  /* 7. Scroll: nav state, spear marker, frieze drift and leaps, manifesto */
  var nav = document.querySelector('.nav'), spear = document.querySelector('.spear-progress');
  var frieze = document.querySelector('.frieze'), track = frieze.querySelector('.frieze-track');
  var sils = Array.prototype.slice.call(frieze.querySelectorAll('.sil'));
  var lastY = scrollY, lastWave = 0, ticking = false;
  function wave() {
    lastWave = Date.now();
    sils.forEach(function (s, i) {
      setTimeout(function () { if (!s.dataset.busy) { s.dataset.busy = 1; leap(s, null, -34 - (i % 3) * 8, 1000).onfinish = function () { delete s.dataset.busy; }; } }, i * 85);
    });
  }
  function onScroll() {
    ticking = false;
    var y = scrollY, h = innerHeight, max = document.documentElement.scrollHeight - h;
    root.classList.toggle('scrolled', y > 40);
    spear.style.setProperty('--p', max > 0 ? Math.min(1, y / max).toFixed(4) : 0);
    var r = frieze.getBoundingClientRect();
    if (r.bottom > 0 && r.top < h) {
      if (!reduced.matches) {
        var half = track.scrollWidth / 2, off = (h - r.top) * .5;
        track.style.transform = 'translate3d(' + (-(off % Math.max(half, 1)) - 40).toFixed(1) + 'px,0,0)';
        if (Math.abs(y - lastY) > 2 && Date.now() - lastWave > 1500) wave();
      }
    }
    var sr = scrub.getBoundingClientRect();
    var p = reduced.matches ? 1 : Math.max(0, Math.min(1, (h * .82 - sr.top) / (sr.height + h * .3)));
    var lit = Math.round(p * words.length);
    words.forEach(function (w, i) { w.classList.toggle('lit', i < lit); });
    lastY = y;
  }
  addEventListener('scroll', function () { if (!ticking) { ticking = true; requestAnimationFrame(onScroll); } }, { passive: true });
  addEventListener('resize', onScroll);
  onScroll();

  /* 8. Pointer parallax on the hero layers (fine pointers only) */
  var layers = Array.prototype.slice.call(document.querySelectorAll('.stage .layer'));
  var tx = 0, ty = 0, cx = 0, cy = 0, raf = 0;
  function tick() {
    cx += (tx - cx) * .06; cy += (ty - cy) * .06;
    layers.forEach(function (l) { var k = +l.dataset.depth; l.style.transform = 'translate3d(' + (cx * k).toFixed(2) + 'px,' + (cy * k * .4).toFixed(2) + 'px,0)'; });
    raf = Math.abs(tx - cx) > .001 || Math.abs(ty - cy) > .001 ? requestAnimationFrame(tick) : 0;
  }
  if (matchMedia('(pointer: fine)').matches) {
    hero.addEventListener('pointermove', function (e) {
      if (reduced.matches) return;
      var r = hero.getBoundingClientRect();
      tx = -((e.clientX - r.left) / r.width - .5); ty = -((e.clientY - r.top) / r.height - .5);
      if (!raf) raf = requestAnimationFrame(tick);
    });
  }

  /* 9. Observers: pause the hero off screen, draw the process spears, fill the share beads, count the ledger, track the active experience */
  var counters = Array.prototype.slice.call(document.querySelectorAll('.ledger .n'));
  function count() {
    counters.forEach(function (n) {
      var to = +n.dataset.to, t0 = performance.now();
      if (reduced.matches) { n.textContent = to.toLocaleString('en-GB'); return; }
      (function step(t) {
        var k = Math.min(1, (t - t0) / 1600), e = 1 - Math.pow(1 - k, 3);
        n.textContent = Math.round(to * e).toLocaleString('en-GB');
        if (k < 1) requestAnimationFrame(step);
      })(t0);
    });
  }
  if ('IntersectionObserver' in window) {
    new IntersectionObserver(function (e) { hero.classList.toggle('paused', !e[0].isIntersecting); }).observe(hero);
    var once = new IntersectionObserver(function (entries) {
      entries.forEach(function (e) { if (e.isIntersecting) { e.target.classList.add('in'); once.unobserve(e.target); } });
    }, { rootMargin: '0px 0px -12% 0px' });
    document.querySelectorAll('[data-inview]').forEach(function (el) { once.observe(el); });
    if (!reduced.matches) counters.forEach(function (n) { n.textContent = '0'; });
    var ledgerIO = new IntersectionObserver(function (e) { if (e[0].isIntersecting) { count(); ledgerIO.disconnect(); } }, { rootMargin: '0px 0px -20% 0px' });
    ledgerIO.observe(document.querySelector('.ledger-text'));
    var expIO = new IntersectionObserver(function (entries) {
      entries.forEach(function (e) { if (e.isIntersecting) setActive(+e.target.dataset.i); });
    }, { rootMargin: '-45% 0px -45% 0px' });
    rows.forEach(function (r) { expIO.observe(r); });
  } else {
    document.querySelectorAll('[data-inview]').forEach(function (el) { el.classList.add('in'); });
  }

  /* 10. Mobile menu */
  var menuBtn = document.querySelector('.menu-btn'), sheet = document.getElementById('sheet');
  function setMenu(open) {
    sheet.classList.toggle('open', open);
    menuBtn.setAttribute('aria-expanded', open);
    document.body.style.overflow = open ? 'hidden' : '';
    if (open) sheet.querySelector('.close').focus(); else menuBtn.focus();
  }
  menuBtn.addEventListener('click', function () { setMenu(true); });
  sheet.querySelector('.close').addEventListener('click', function () { setMenu(false); });
  sheet.querySelectorAll('a').forEach(function (a) { a.addEventListener('click', function () { setMenu(false); }); });
  addEventListener('keydown', function (e) { if (e.key === 'Escape' && sheet.classList.contains('open')) setMenu(false); });

  /* 11. Season rows prefill the enquiry */
  var form = document.getElementById('enquiry'), msg = document.getElementById('form-msg');
  document.querySelectorAll('[data-occasion]').forEach(function (b) {
    b.addEventListener('click', function () {
      var r = form.querySelector('input[value="' + b.dataset.occasion + '"]');
      if (r) r.checked = true;
      form.month.value = b.dataset.month;
      msg.textContent = '';
    });
  });

  /* 12. Enquiry (local only): the warrior leaps when it is sent */
  var guests = document.getElementById('guests'), out = document.getElementById('guests-out');
  function showGuests() { out.textContent = (+guests.value).toLocaleString('en-GB') + (+guests.value >= 2000 ? '+' : ''); }
  guests.addEventListener('input', showGuests); showGuests();
  var ew = document.querySelector('.enq-warrior');
  form.addEventListener('submit', function (e) {
    e.preventDefault();
    if (!form.name.value.trim() || !form.email.value || !form.email.checkValidity()) {
      msg.textContent = 'Add your name and a valid email address to send your enquiry.';
      (form.name.value.trim() ? form.email : form.name).focus();
      return;
    }
    msg.textContent = 'Enquiry sent, ' + form.name.value.trim().split(' ')[0] + '. This demo doesn’t send anything; a real one would get a reply within two working days.';
    leap(ew.querySelector('.body'), ew.querySelector('.shadow'), -48, 1150);
    form.reset(); showGuests();
  });

  document.querySelector('.to-top').addEventListener('click', function () { scrollTo({ top: 0, behavior: reduced.matches ? 'auto' : 'smooth' }); });
})();
</script>
</body>
</html>
```

