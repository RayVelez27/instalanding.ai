INSTALANDING.AI · Orrery Reasoning Engine Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Orrery Reasoning Engine Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/orrery-reasoning-engine-page

orrery-engine.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Orrery Reasoning Engine Page
  slug     orrery-reasoning-engine-page
  prompt   https://instalanding.ai/p/orrery-reasoning-engine-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/orrery-reasoning-engine-page
  license  MIT. Fictional company; every name, number, customer and quote is invented. Replace them before shipping.

  MAP
  tokens    :root at the top of <style>: ink, night, smoke, ash, haze, fog, mist, pearl, one ember accent (#d6b28a) and
            steel; fonts (--f-display Hubot Sans with the width axis, --f-text Instrument Sans); --pad, --max, --sec,
            radii, two eases, and two SVG noise textures (--grain, --frost). [data-tone=dark|light] on each section
            sets --fg, --fg2, --bg and --line, and the fixed header retints itself to the section under it.
  sections  nav, hero, brief, capabilities, process, gallery, results, team, reviews, pricing, faq, contact, footer
  scripts   1) the procedural art engine: every picture is a <canvas data-art="..."> drawn in code with a seeded PRNG
            (an orrery with planets, rings, moons and a lens flare; a search tree that prunes and commits; a memory
            sphere; agents asking to confirm; a chart being read; isometric server racks; attention grid, retrieval
            graph, token stream, terrain, rings, lattice, scan-line portraits), resized by ResizeObserver and only
            animated while on screen. 2) GSAP 3.13 + ScrollTrigger + SplitText + Lenis 1.3 (jsdelivr): the hero's
            clear window opening out of a blurred mirror of the same canvas, defogging text, a focus rail with
            travelling corner brackets, a horizontal gallery behind a frosted pane with a cut-out window, stacking
            review cards that veil, bars, figures and tier reveals.
  assets    none: every visual is canvas; fonts from Google Fonts

  ADAPTING
  - Add a picture with <canvas data-art="name" data-seed="n">; the seed fixes the composition. Renderers live in F.
  - html.motion is added in <head> only when motion is allowed and dropped if GSAP has not loaded in 2.5s; every
    hidden-until-animated state is scoped under .motion, so the page is complete without it.
  - Giant words, figures and prices size from --len (character count); update it with the text.
  - The pricing switch reads data-monthly / data-yearly on each price and label.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Orrery — the reasoning engine that shows its work</title>
<meta name="description" content="Orrery is a reasoning engine for teams that can't afford to guess. It reads everything you already have and tells you what it adds up to, with the sources behind every claim.">
<script>(function(){var d=document.documentElement;d.classList.add('js');if(!window.matchMedia('(prefers-reduced-motion: reduce)').matches){d.classList.add('motion');setTimeout(function(){if(!window.gsap)d.classList.remove('motion')},2500)}})();</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Hubot+Sans:wdth,wght@100..125,500..700&amp;family=Instrument+Sans:wght@400..700&amp;display=swap">
<style>:root{--ink:#111110;--night:#191816;--smoke:#2a2926;--ash:#55574f;--haze:#a6a9a3;--fog:#c8cac4;--mist:#e7e6e1;--pearl:#f5f4f0;--ember:#d6b28a;--steel:#7d8c8b;--f-display:"Hubot Sans", system-ui, sans-serif;--f-text:"Instrument Sans", system-ui, sans-serif;--pad:clamp(16px, 4.2vw, 64px);--max:1400px;--sec:clamp(96px, 12vw, 190px);--head-h:76px;--r:14px;--r-lg:24px;--ease:cubic-bezier(.19,1,.22,1);--ease-io:cubic-bezier(.77,0,.18,1);--grain:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='220' height='220'%3E%3Cfilter id='g' x='0' y='0' width='100%25' height='100%25'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.15' numOctaves='2' seed='4' stitchTiles='stitch'/%3E%3CfeDiffuseLighting lighting-color='white' surfaceScale='1.8' diffuseConstant='1.15'%3E%3CfeDistantLight azimuth='225' elevation='48'/%3E%3C/feDiffuseLighting%3E%3C/filter%3E%3Crect width='220' height='220' filter='url(%23g)'/%3E%3C/svg%3E");--frost:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='f' x='0' y='0' width='100%25' height='100%25'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.15' numOctaves='2' seed='9' stitchTiles='stitch'/%3E%3CfeDiffuseLighting lighting-color='white' surfaceScale='1.8' diffuseConstant='1.15'%3E%3CfeDistantLight azimuth='225' elevation='48'/%3E%3C/feDiffuseLighting%3E%3CfeColorMatrix type='matrix' values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 1.5 0 0 0 -1'/%3E%3C/filter%3E%3Crect width='200' height='200' filter='url(%23f)'/%3E%3C/svg%3E");}@media (max-width:760px){:root{--head-h:64px;--r:12px;--r-lg:18px}}*,*::before,*::after{box-sizing:border-box}html{-webkit-text-size-adjust:100%;background:var(--ink)}::selection{background:var(--ember);color:var(--ink)}body{margin:0;font-family:var(--f-text);font-size:17px;line-height:1.6;color:var(--pearl);background:var(--ink);-webkit-font-smoothing:antialiased;text-rendering:optimizeLegibility}canvas{display:block}a{color:inherit;text-decoration:none}button,input,textarea,select{font:inherit;color:inherit}button{background:none;border:0;padding:0;cursor:pointer}h1,h2,h3,h4,p,ul,ol,figure,blockquote{margin:0}ul,ol{padding:0;list-style:none}:focus-visible{outline:2px solid var(--ember);outline-offset:3px}main>*{position:relative;overflow-x:clip}[data-tone=dark]{--fg:var(--pearl);--fg2:var(--haze);--bg:var(--night);--line:color-mix(in oklab, var(--pearl) 15%, transparent);color:var(--fg)}[data-tone=light]{--fg:var(--ink);--fg2:var(--ash);--bg:var(--mist);--line:color-mix(in oklab, var(--ink) 14%, transparent);color:var(--fg)}main>[data-tone]{background:var(--bg)}.wrap{max-width:var(--max);margin-inline:auto;padding-inline:var(--pad)}.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap}.h2{font-family:var(--f-display);font-weight:600;font-stretch:112%;text-transform:uppercase;font-size:clamp(30px, 4.4vw, 68px);line-height:.96;letter-spacing:-.012em;overflow-wrap:break-word;hyphens:auto;text-wrap:balance}.caps{font-family:var(--f-display);font-weight:700;text-transform:uppercase;letter-spacing:.01em;font-size:clamp(14px, 1.2vw, 17px);line-height:1.2}.spaced{font-family:var(--f-display);font-weight:700;text-transform:uppercase;letter-spacing:.38em;font-size:13px;line-height:1.5}.lede{font-size:clamp(17px, 1.3vw, 20px);line-height:1.55;color:var(--fg2);max-width:46ch}.giant{display:block;font-family:var(--f-display);font-weight:600;font-stretch:125%;text-transform:uppercase;line-height:.8;letter-spacing:-.01em;white-space:nowrap;--k:.84}.bracket{position:absolute;display:block;width:var(--bk, 22px);height:var(--bk, 22px);pointer-events:none;color:inherit}.bracket>i{position:absolute;inset:0;border:0 solid currentColor}.bracket--tr>i{border-top-width:2px;border-right-width:2px;transform-origin:100% 0}.bracket--bl>i{border-bottom-width:2px;border-left-width:2px;transform-origin:0 100%}.framed{position:relative}.framed::before,.framed::after{content:"";position:absolute;width:20px;height:20px;border:0 solid currentColor;pointer-events:none;z-index:2}.framed::before{top:-12px;right:-12px;border-top-width:2px;border-right-width:2px}.framed::after{bottom:-12px;left:-12px;border-bottom-width:2px;border-left-width:2px}.btn{--b-bg:var(--fg);--b-fg:var(--bg);--b-fill:var(--ember);--b-fill-fg:var(--ink);position:relative;isolation:isolate;display:inline-flex;align-items:center;justify-content:center;gap:.7em;padding:1.05em 1.5em;border-radius:12px;background:var(--b-bg);color:var(--b-fg);font-family:var(--f-display);font-weight:700;font-size:14px;letter-spacing:.06em;text-transform:uppercase;line-height:1.1;white-space:nowrap;overflow:hidden;transition:color .5s var(--ease)}.btn::before{content:"";position:absolute;inset:0;z-index:-1;background:var(--b-fill);clip-path:inset(50% 0 50% 0 round 12px);transition:clip-path .6s var(--ease)}.btn--ghost{--b-bg:transparent;--b-fg:var(--fg);--b-fill:var(--fg);--b-fill-fg:var(--bg);box-shadow:inset 0 0 0 1px color-mix(in oklab, var(--fg) 38%, transparent)}.btn svg{width:14px;height:14px;flex:none}.link{position:relative;display:inline-flex;align-items:center;gap:.55em;font-weight:600;padding-bottom:5px;background:linear-gradient(color-mix(in oklab, currentColor 30%, transparent), color-mix(in oklab, currentColor 30%, transparent)) left bottom/100% 1px no-repeat}.link::after{content:"";position:absolute;left:0;right:0;bottom:0;height:2px;background:currentColor;transform:scaleX(0);transition:transform .6s var(--ease)}.link svg{width:13px;height:13px;flex:none}.icon-btn{position:relative;display:grid;place-items:center;width:46px;height:46px;flex:none}.icon-btn::before,.icon-btn::after{content:"";position:absolute;width:10px;height:10px;border:0 solid currentColor;opacity:0;transition:opacity .35s, transform .5s var(--ease)}.icon-btn::before{top:3px;right:3px;border-top-width:1.5px;border-right-width:1.5px;transform:translate(6px,-6px)}.icon-btn::after{bottom:3px;left:3px;border-bottom-width:1.5px;border-left-width:1.5px;transform:translate(-6px,6px)}@media (hover:hover){.btn:hover{color:var(--b-fill-fg)}.btn:hover::before{clip-path:inset(0 0 0 0 round 12px)}.link:hover::after{transform:scaleX(1)}.icon-btn:hover::before,.icon-btn:hover::after{opacity:1;transform:none}}.site-head{position:fixed;inset:0 0 auto 0;z-index:50;height:var(--head-h);display:flex;align-items:center;justify-content:space-between;gap:24px;padding-inline:var(--pad);color:var(--fg);transition:transform .55s var(--ease), color .35s, background-color .35s}.site-head::before{content:"";position:absolute;inset:0;z-index:-2;background:color-mix(in oklab, var(--bg) 90%, transparent);opacity:0;transition:opacity .35s}.site-head.is-solid::before{opacity:1}.site-head.is-hidden{transform:translateY(-102%)}.brand{display:inline-flex;align-items:center;gap:12px;font-family:var(--f-display);font-weight:700;letter-spacing:.36em;text-transform:uppercase;font-size:14px;white-space:nowrap;margin-right:-.34em}.brand svg{width:22px;height:22px;flex:none;color:var(--ember)}.nav{display:flex;align-items:center;gap:clamp(18px, 2.3vw, 36px)}.nav>a:not(.btn){font-size:15px;font-weight:550;white-space:nowrap}.nav .btn{padding:.9em 1.25em}.menu-btn{display:none}.menu-btn span{position:relative;width:22px;height:10px}.menu-btn span::before,.menu-btn span::after{content:"";position:absolute;left:0;right:0;height:2px;background:currentColor;transition:transform .45s var(--ease)}.menu-btn span::before{top:0}.menu-btn span::after{bottom:0}.menu-open .menu-btn span::before{transform:translateY(4px) rotate(45deg)}.menu-open .menu-btn span::after{transform:translateY(-4px) rotate(-45deg)}@media (min-width:1081px) and (hover:hover){.site-head.is-solid::before{background:color-mix(in oklab, var(--bg) 72%, transparent);backdrop-filter:blur(14px)}}@media (max-width:1080px){.menu-btn{display:grid}.nav{position:fixed;inset:0;z-index:-1;flex-direction:column;align-items:flex-start;justify-content:center;gap:14px;padding:calc(var(--head-h) + 24px) var(--pad) 48px;background:var(--night);color:var(--pearl);visibility:hidden;opacity:0;transition:opacity .45s var(--ease), visibility .45s}.nav::after{content:"";position:absolute;inset:0;z-index:-1;background:var(--grain);background-size:200px;mix-blend-mode:overlay;opacity:.35;pointer-events:none}.nav>a:not(.btn){font-family:var(--f-display);font-stretch:112%;font-weight:600;text-transform:uppercase;font-size:clamp(30px, 8.4vw, 52px);line-height:1.05;white-space:normal;overflow-wrap:anywhere}.nav .btn{margin-top:18px}.menu-open .nav{visibility:visible;opacity:1}.menu-open .site-head{--fg:var(--pearl);--bg:var(--night)}}.hero{height:100svh;background:var(--ink)}.motion .hero{height:210svh}.hero-stage{position:sticky;top:0;height:100svh;overflow:hidden;isolation:isolate;color:var(--pearl);--open:0;--sw:min(46vw, 720px);--sh:calc(var(--sw) / 3.5);--sy:53svh;--lf:clamp(15px, 2.05vw, 31px);--sr:16px;--edge:var(--pad)}.hero-fog,.hero-clear{position:absolute;inset:0}.hero-fog canvas,.hero-clear canvas{position:absolute;inset:0;width:100%;height:100%;background:var(--smoke)}.hero-fog canvas{filter:blur(20px) saturate(.8) brightness(1.15);transform:scale(1.06)}.hero-clear canvas{transform:scale(1.06);transform-origin:50% 45%}.hero-fog::after{content:"";position:absolute;inset:0;background:linear-gradient(180deg, color-mix(in oklab, var(--ink) 66%, transparent) 0%, transparent 30%, transparent 68%, color-mix(in oklab, var(--ink) 62%, transparent) 100%), linear-gradient(color-mix(in oklab, var(--mist) 8%, transparent), color-mix(in oklab, var(--mist) 8%, transparent))}.hero-haze{position:absolute;inset:-12%;pointer-events:none;background:radial-gradient(34% 30% at 30% 62%, color-mix(in oklab, var(--pearl) 30%, transparent), transparent 100%), radial-gradient(30% 26% at 72% 40%, color-mix(in oklab, var(--ember) 28%, transparent), transparent 100%)}.hero-title{position:absolute;inset:0;font:inherit;pointer-events:none}.hero-word{position:absolute;left:50%;translate:-50% 0;font-size:min(calc(100vw / (var(--len) * var(--k))), 30svh, calc((var(--sy) - var(--sh) / 2 - var(--head-h) - 1.5svh - var(--lf) * 1.15 - 12px - 34px) / .8));color:color-mix(in oklab, var(--pearl) 34%, transparent)}.hero-word--top{top:calc(var(--head-h) + 1.5svh)}.hero-word--bottom{bottom:-.03em;color:color-mix(in oklab, var(--fog) 30%, transparent)}.hero-grain{position:absolute;inset:0;background:var(--grain);background-size:190px;mix-blend-mode:overlay;opacity:.75;pointer-events:none}.hero-clear{z-index:2;--t:calc(var(--sy) - var(--sh) / 2);--b:calc(100% - var(--sy) - var(--sh) / 2);--l:calc((100% - var(--sw)) / 2);--c:calc(1 - var(--open));clip-path:inset(calc(var(--t) * var(--c)) calc(var(--l) * var(--c)) calc(var(--b) * var(--c)) calc(var(--l) * var(--c)) round calc(var(--sr) * var(--c)))}.hero-rim{position:absolute;z-index:3;left:50%;top:calc(var(--sy) - var(--sh) / 2);width:var(--sw);height:var(--sh);translate:-50% 0;border-radius:var(--sr);pointer-events:none;box-shadow:inset 0 0 0 1px color-mix(in oklab, var(--pearl) 55%, transparent), inset 0 2px 18px color-mix(in oklab, var(--pearl) 30%, transparent), 0 18px 50px color-mix(in oklab, var(--ink) 30%, transparent);opacity:calc(1 - var(--open) * 6)}.hero-bracket{z-index:4;--bk:clamp(18px, 2.5vw, 34px);color:var(--pearl)}.hero-bracket--tr{left:calc(50% + var(--sw) / 2 - var(--bk) * .55);top:calc(var(--sy) - var(--sh) / 2 - var(--bk) - 10px)}.hero-bracket--bl{left:calc(50% - var(--sw) / 2 - var(--bk) * .45);top:calc(var(--sy) + var(--sh) / 2 + 10px)}.hero-lines{position:absolute;inset:0;z-index:4;pointer-events:none}.hero-line{position:absolute;max-width:min(78vw, 640px);font-size:var(--lf);line-height:1.05;letter-spacing:-.005em;color:var(--pearl);text-shadow:0 2px 18px color-mix(in oklab, var(--ink) 45%, transparent);text-wrap:balance}.hero-line--a{left:calc(50% - var(--sw) * .64);bottom:calc(100svh - var(--sy) + var(--sh) / 2 + 12px)}.hero-line--b{right:calc(50% - var(--sw) * .66);top:calc(var(--sy) + var(--sh) / 2 + 12px);text-align:right}.hero-cta{position:absolute;z-index:4;left:50%;bottom:max(5svh, 26px);translate:-50% 0;display:inline-flex;align-items:center;gap:1em;max-width:calc(100vw - 2 * var(--pad));text-align:center;color:var(--pearl);font-size:clamp(12px, 1.05vw, 15px);padding-bottom:6px}.hero-cta::after{content:"";position:absolute;left:0;right:.38em;bottom:0;height:1px;background:currentColor;transform:scaleX(.18);transition:transform .7s var(--ease)}@media (hover:hover){.hero-cta:hover::after{transform:scaleX(1)}}@media (max-width:760px){.hero-stage{--sw:74vw;--sh:calc(var(--sw) / 3.3);--sy:44svh;--sr:12px}.hero-word--top{top:calc(var(--head-h) + 5svh)}.hero-word--bottom{bottom:9svh}.hero-cta{bottom:max(4svh, 22px);letter-spacing:.3em}}.brief{padding-block:var(--sec)}.brief-statement{font-family:var(--f-display);font-weight:500;font-stretch:100%;font-size:clamp(27px, 3.45vw, 54px);line-height:1.1;letter-spacing:-.02em;max-width:25em;text-wrap:pretty}.brief-foot{display:grid;grid-template-columns:repeat(12, minmax(0,1fr));gap:24px;margin-top:clamp(56px, 8vw, 120px);align-items:end}.brief-photo{grid-column:1 / span 6;color:var(--ink)}.brief-photo .slot{aspect-ratio:3.2/1}.brief-text{grid-column:8 / span 5;display:grid;gap:28px;justify-items:start}@media (max-width:860px){.brief-foot{grid-template-columns:minmax(0,1fr);row-gap:48px}.brief-photo,.brief-text{grid-column:1 / -1}.brief-photo .slot{aspect-ratio:2.4/1}}.marks{margin-top:clamp(64px, 8vw, 120px);padding-top:30px;border-top:1px solid var(--line);display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:22px 40px}.marks .spaced{color:var(--fg2);font-size:12px;letter-spacing:.3em}.mark{display:inline-flex;align-items:center;gap:.5em;font-family:var(--f-display);font-weight:600;font-stretch:118%;font-size:clamp(16px, 1.45vw, 21px);letter-spacing:-.01em;color:color-mix(in oklab, var(--fg) 58%, transparent);white-space:nowrap}.mark svg{width:1em;height:1em}.slot{position:relative;display:block;overflow:hidden;border-radius:var(--r);background:var(--night)}.slot::after{content:"";position:absolute;inset:0;z-index:1;background:var(--grain);background-size:180px;mix-blend-mode:overlay;opacity:.32;pointer-events:none}.slot canvas{position:absolute;inset:0;z-index:0;width:100%;height:100%}.motion [data-slot] .slot canvas,.motion .slot[data-slot] canvas{clip-path:inset(46% 7% 46% 7% round 10px)}.motion [data-reveal]{opacity:0}.files{padding-block:var(--sec)}.files-head{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,38ch);gap:24px 64px;align-items:end;margin-bottom:clamp(48px, 7vw, 104px)}.files-head .lede{justify-self:end}.files-head .link{grid-column:2;justify-self:start}.files-rail{position:relative}.file{position:relative;border-top:1px solid var(--line)}.file:last-child{border-bottom:1px solid var(--line)}.file-link{display:grid;grid-template-columns:minmax(110px, 2fr) minmax(0, 5fr) minmax(0, 5fr);gap:clamp(16px, 2.6vw, 44px);align-items:center;padding-block:clamp(30px, 4.6vw, 66px)}.file-meta{display:flex;flex-direction:column;gap:6px;align-self:start;padding-top:.4em}.file-year{font-family:var(--f-display);font-weight:700;font-size:15px;letter-spacing:.08em;color:var(--ember)}.file-topic{font-size:14px;color:var(--fg2)}.file-title{font-family:var(--f-display);font-weight:600;font-stretch:112%;text-transform:uppercase;font-size:clamp(24px, 3vw, 46px);line-height:1;letter-spacing:-.01em;overflow-wrap:break-word;hyphens:auto;transition:color .4s}.file-text{margin-top:16px;color:var(--fg2);max-width:48ch}.file-photo{aspect-ratio:2.2/1}.rail-bk{top:0;left:0;--bk:24px;color:var(--fg);opacity:0;transition:opacity .5s}.files-rail.is-live .rail-bk{opacity:1}.files-rail.is-live .file{transition:opacity .7s var(--ease), filter .7s var(--ease)}.files-rail.is-live .file:not(.is-focus){opacity:.3}.files-rail.is-live .file-photo canvas{clip-path:inset(46% 0 46% 0 round 8px);transition:clip-path 1.1s var(--ease)}.files-rail.is-live .file.is-focus .file-photo canvas{clip-path:inset(0 0 0 0 round 8px)}@media (min-width:1024px) and (hover:hover){.files-rail.is-live .file:not(.is-focus){filter:blur(2.5px)}}@media (hover:hover){.file-link:hover .file-title{color:var(--ember)}}@media (max-width:860px){.files-head{grid-template-columns:1fr}.files-head .lede{justify-self:start}.files-head .link{grid-column:1}.file-link{grid-template-columns:1fr;gap:18px}.file-meta{flex-direction:row;gap:14px;padding-top:0}.file-photo{aspect-ratio:1.9/1}}.method{padding-block:var(--sec)}.method-head,.impact-head{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,40ch);gap:24px 64px;align-items:end;margin-bottom:clamp(56px, 8vw, 120px)}.steps{display:grid;grid-auto-flow:column;grid-auto-columns:minmax(0,1fr);gap:clamp(16px, 2vw, 32px);--rise:clamp(40px, 5.2vw, 80px)}.step{position:relative;margin-top:calc(var(--i, 0) * var(--rise));padding-top:26px;display:grid;gap:12px;align-content:start}.step-rule{position:absolute;left:0;right:0;top:0;height:2px;background:currentColor}.step-rule::before{content:"";position:absolute;left:0;top:-7px;width:2px;height:16px;background:currentColor}.step-when{font-family:var(--f-display);font-weight:600;font-stretch:112%;font-size:clamp(22px, 2.3vw, 34px);line-height:1;letter-spacing:-.015em;overflow-wrap:break-word}.step-title{font-size:clamp(15px, 1.3vw, 19px);overflow-wrap:break-word;hyphens:auto}.step-text{font-size:16px;line-height:1.55;color:var(--fg2)}@media (max-width:860px){.method-head,.impact-head{grid-template-columns:1fr}.steps{grid-auto-flow:row;grid-auto-columns:auto;gap:44px}.step{margin-top:0;margin-left:min(calc(var(--i, 0) * 5vw), 22vw)}}.field{--shot-w:min(40vw, 580px);--gap:clamp(20px, 3vw, 48px);padding-bottom:var(--sec)}.field-head{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:end;gap:20px 64px;padding-top:var(--sec);margin-bottom:clamp(40px, 5vw, 72px)}.field-track{display:grid;grid-template-columns:repeat(auto-fill, minmax(min(100%, 300px), 1fr));gap:40px 24px;max-width:var(--max);margin-inline:auto;padding-inline:var(--pad)}.shot-photo{aspect-ratio:3/2}.shot figcaption{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:baseline;gap:4px 16px;padding-top:14px}.shot-note{font-size:14px;color:var(--fg2)}.shot-note::before{content:"";display:inline-block;width:6px;height:6px;margin-right:8px;border-radius:50%;background:var(--ember);box-shadow:0 0 10px var(--ember);vertical-align:.12em}.field-pane,.field-rim{display:none}.field.is-track{padding-bottom:0}.field.is-track .field-stage{position:sticky;top:0;height:100svh;overflow:hidden;display:flex;flex-direction:column}.field.is-track .field-head{padding-top:calc(var(--head-h) + 3svh);margin-bottom:0;position:relative;z-index:3;width:100%}.field.is-track .field-stage{--hole-w:calc(var(--shot-w) + 36px);--hole-h:calc(var(--shot-w) * .667 + 120px);--hole-cy:55%}.field.is-track .field-view{position:relative;z-index:1;flex:1;display:flex;align-items:center}.field.is-track .field-track{display:flex;gap:var(--gap);width:max-content;max-width:none;margin:0;padding:0 calc((100vw - var(--shot-w)) / 2);will-change:transform}.field.is-track .shot{width:var(--shot-w);flex:none}.field.is-track .field-pane{display:block;position:absolute;inset:0;z-index:2;pointer-events:none;background:color-mix(in oklab, var(--night) 64%, transparent);--hole:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Crect width='100%25' height='100%25' rx='18'/%3E%3C/svg%3E");-webkit-mask-image:var(--hole), linear-gradient(#000 0 0);mask-image:var(--hole), linear-gradient(#000 0 0);-webkit-mask-position:50% calc(var(--hole-cy) - var(--hole-h) / 2), 0 0;mask-position:50% calc(var(--hole-cy) - var(--hole-h) / 2), 0 0;-webkit-mask-size:var(--hole-w) var(--hole-h), 100% 100%;mask-size:var(--hole-w) var(--hole-h), 100% 100%;-webkit-mask-repeat:no-repeat;mask-repeat:no-repeat;-webkit-mask-composite:xor;mask-composite:exclude}.field.is-track .field-pane::after{content:"";position:absolute;inset:0;background:var(--frost);background-size:130px;opacity:.3}.field.is-track .field-rim{display:block;position:absolute;z-index:3;left:50%;top:var(--hole-cy);width:var(--hole-w);height:var(--hole-h);translate:-50% -50%;border-radius:18px;pointer-events:none;color:var(--pearl);box-shadow:inset 0 0 0 1px color-mix(in oklab, var(--pearl) 26%, transparent)}.field-rim .bracket--tr{top:-14px;right:-14px}.field-rim .bracket--bl{bottom:-14px;left:-14px}@media (min-width:1024px) and (hover:hover){.field.is-track .field-pane{background:color-mix(in oklab, var(--night) 46%, transparent);backdrop-filter:blur(16px) saturate(.55)}}@media (max-width:760px){.field{--shot-w:74vw;--gap:18px}.field.is-track .field-view{--hole-w:calc(var(--shot-w) + 20px)}}.impact{padding-block:var(--sec)}.outcomes{display:grid;grid-template-columns:repeat(2, minmax(0,1fr));gap:0 clamp(24px, 4vw, 72px)}.outcome{position:relative;container-type:inline-size;display:grid;gap:12px;align-content:start;padding:clamp(22px, 2.6vw, 36px) 0 clamp(40px, 4.4vw, 64px)}.outcome .rule{position:absolute;left:0;right:0;top:0;height:1px;background:color-mix(in oklab, var(--fg) 30%, transparent)}.figure{font-family:var(--f-display);font-weight:600;font-stretch:125%;line-height:1;letter-spacing:-.02em;overflow-y:clip;--k:.8;font-size:min(clamp(64px, 8.4vw, 136px), calc(100cqi / (var(--len) * var(--k))))}.figure>span{display:inline-block}.outcome-text{max-width:32ch;color:var(--fg2)}.funding{margin-top:clamp(48px, 6vw, 96px);display:grid;grid-template-columns:minmax(0,4fr) minmax(0,8fr);gap:28px 64px;align-items:start}.funding-copy{display:grid;gap:14px}.funding-note{color:var(--fg2);max-width:36ch}.bars{display:grid;gap:16px}.bar{display:grid;grid-template-columns:minmax(120px, 2.4fr) minmax(0, 7fr) minmax(56px, auto);align-items:center;gap:8px 20px}.bar-label{font-weight:600}.bar-value{font-family:var(--f-display);font-weight:700;font-size:18px;text-align:right;white-space:nowrap}.bar-track{position:relative;height:16px;border-radius:6px;overflow:hidden;background:color-mix(in oklab, var(--ink) 9%, transparent)}.bar-track::after{content:"";position:absolute;inset:0;background:var(--grain);background-size:120px;mix-blend-mode:overlay;opacity:.8}.bar-fill{position:absolute;inset:0;background:var(--ink);transform-origin:0 50%;transform:scaleX(var(--v, 0))}.bar:first-child .bar-fill{background:linear-gradient(90deg, var(--ink), #6b5640)}.motion [data-chart] .bar-fill{transform:scaleX(0)}@media (max-width:860px){.outcomes{grid-template-columns:1fr}.funding{grid-template-columns:1fr}.bar{grid-template-columns:minmax(0,1fr) auto}.bar-track{grid-column:1 / -1;order:3}}.people{padding-block:var(--sec)}.people-head,.support-head{display:grid;grid-template-columns:minmax(0,1fr) minmax(0,38ch);gap:24px 64px;align-items:end;margin-bottom:clamp(48px, 6vw, 96px)}.people-head .link{grid-column:2;justify-self:start}.people-grid{display:grid;grid-template-columns:repeat(4, minmax(0,1fr));gap:48px clamp(16px, 2vw, 28px)}.person{display:grid;gap:6px;align-content:start}.person-photo{aspect-ratio:4/5;margin-bottom:16px}.person-name{font-size:clamp(16px, 1.35vw, 20px);overflow-wrap:break-word}.person-role{font-family:var(--f-display);font-weight:700;font-size:14px;letter-spacing:.05em;color:var(--ember)}.person-note{margin-top:6px;font-size:15px;line-height:1.5;color:var(--fg2)}.motion .person-photo[data-slot] canvas{clip-path:inset(30% 8% 58% 8% round 10px)}@media (max-width:960px){.people-grid{grid-template-columns:repeat(2, minmax(0,1fr))}}.voices{padding-block:var(--sec)}.voices-title{margin-bottom:clamp(40px, 5vw, 80px)}.voice-stack{display:grid;gap:clamp(20px, 3vw, 40px)}.voice{--veil:0;position:relative;isolation:isolate;display:flex;flex-direction:column-reverse;justify-content:space-between;gap:48px;min-height:min(54svh, 500px);padding:clamp(34px, 4.6vw, 76px);border-radius:var(--r-lg);color:var(--ink);transform-origin:50% 0;background:linear-gradient(currentColor, currentColor) right 20px top 20px / 22px 2px no-repeat, linear-gradient(currentColor, currentColor) right 20px top 20px / 2px 22px no-repeat, linear-gradient(currentColor, currentColor) left 20px bottom 20px / 22px 2px no-repeat, linear-gradient(currentColor, currentColor) left 20px bottom 20px / 2px 22px no-repeat, var(--pearl);box-shadow:0 30px 70px -40px color-mix(in oklab, var(--ink) 50%, transparent)}.voice::after{content:"";position:absolute;inset:0;z-index:2;border-radius:inherit;pointer-events:none;background:var(--frost) 0 0 / 150px, color-mix(in oklab, var(--fog) 86%, transparent);opacity:var(--veil)}.voice-quote p{font-family:var(--f-display);font-weight:500;font-size:clamp(25px, 3.5vw, 56px);line-height:1.08;letter-spacing:-.022em;max-width:22em;text-wrap:pretty}.voice-by{display:flex;flex-wrap:wrap;align-items:baseline;gap:6px 18px;padding-right:40px}.voice-by span:last-child{color:var(--ash)}.motion .voice{position:sticky;top:calc(5svh + var(--i, 0) * 14px)}@media (max-width:760px){.voice{min-height:min(50svh, 400px)}}.support{padding-block:var(--sec)}.bill{grid-column:2;justify-self:start;display:inline-flex;gap:4px;padding:4px;border-radius:14px;box-shadow:inset 0 0 0 1px var(--line)}.bill-opt{padding:.75em 1.2em;border-radius:10px;font-family:var(--f-display);font-weight:700;font-size:14px;letter-spacing:.05em;text-transform:uppercase;white-space:nowrap;color:var(--fg2);transition:color .4s, background-color .4s}.bill-opt[aria-pressed=true]{background:var(--pearl);color:var(--ink)}.tiers{display:grid;grid-template-columns:repeat(3, minmax(0,1fr));gap:clamp(16px, 2vw, 28px);align-items:stretch}.tier{position:relative;isolation:isolate;display:flex;flex-direction:column;gap:18px;padding:clamp(26px, 2.8vw, 42px);border-radius:var(--r-lg);background:color-mix(in oklab, var(--pearl) 5%, transparent);box-shadow:inset 0 0 0 1px var(--line);container-type:inline-size}.tier::after{content:"";position:absolute;inset:0;z-index:-1;border-radius:inherit;background:var(--frost);background-size:140px;opacity:.16;pointer-events:none}.tier--key{--fg:var(--ink);--fg2:var(--ash);--bg:var(--mist);--line:color-mix(in oklab, var(--ink) 14%, transparent);color:var(--fg);background:linear-gradient(160deg, var(--pearl), var(--mist) 55%, #e9dccb)}.tier--key::after{opacity:0}.tier--key .bracket{--bk:24px;color:var(--ember)}.tier--key .bracket--tr{top:-14px;right:-14px}.tier--key .bracket--bl{bottom:-14px;left:-14px}.tier-price{display:flex;flex-wrap:wrap;align-items:baseline;gap:4px 12px;padding-bottom:22px;border-bottom:1px solid var(--line)}.price{font-family:var(--f-display);font-weight:600;font-stretch:125%;line-height:1;letter-spacing:-.02em;--k:.8;font-size:min(clamp(48px, 5.2vw, 80px), calc(100cqi / (var(--len) * var(--k))))}.per{font-size:15px;color:var(--fg2)}.tier-text{color:var(--fg2)}.ticks{display:grid;gap:10px;margin-bottom:auto;padding-bottom:14px}.ticks li{position:relative;padding-left:26px;font-size:15.5px;line-height:1.45}.ticks li::before{content:"";position:absolute;left:1px;top:.4em;width:11px;height:6px;border-left:2px solid currentColor;border-bottom:2px solid currentColor;transform:rotate(-45deg)}.tier .btn{align-self:stretch;padding-inline:1em;letter-spacing:.04em}@media (max-width:760px){.tier{padding:24px 20px}}.support-note{margin-top:36px;font-size:14px;color:var(--fg2)}@media (max-width:960px){.tiers{grid-template-columns:minmax(0,1fr);max-width:560px}}@media (max-width:860px){.people-head,.support-head{grid-template-columns:1fr}.people-head .link,.bill{grid-column:1}}.faq{padding-block:var(--sec)}.faq-grid{display:grid;grid-template-columns:minmax(0,5fr) minmax(0,7fr);gap:48px clamp(32px, 6vw, 120px);align-items:start}.faq-head{position:sticky;top:calc(var(--head-h) + 32px);display:grid;gap:24px;justify-items:start}.qa{position:relative}.qa:last-child{border-bottom:1px solid var(--line)}.qa .rule{position:absolute;left:0;right:0;top:0;height:1px;background:color-mix(in oklab, var(--fg) 30%, transparent)}.qa-q button{width:100%;display:flex;flex-direction:row-reverse;justify-content:space-between;align-items:center;gap:24px;padding:22px 0;text-align:left;font-family:var(--f-text);font-weight:600;font-size:clamp(18px, 1.6vw, 24px);line-height:1.2;letter-spacing:-.005em}.qa-text{min-width:0;overflow-wrap:break-word}.qa-icon i{position:relative;width:16px;height:16px}.qa-icon i::before,.qa-icon i::after{content:"";position:absolute;left:0;top:7px;width:16px;height:2px;background:currentColor;transition:transform .5s var(--ease)}.qa-icon i::after{transform:rotate(90deg)}.qa.is-open .qa-icon i::after{transform:rotate(0deg)}.qa-a{display:grid;grid-template-rows:0fr;visibility:hidden;transition:grid-template-rows .6s var(--ease), visibility .6s}.qa-a>div{overflow:hidden;min-height:0}.qa-a p{padding:0 64px 28px 0;max-width:60ch;color:var(--fg2);opacity:0;transform:translateY(-8px);transition:opacity .5s .08s, transform .7s var(--ease)}.qa.is-open .qa-a{grid-template-rows:1fr;visibility:visible}.qa.is-open .qa-a p{opacity:1;transform:none}@media (hover:hover){.qa-q button:hover .icon-btn::before,.qa-q button:hover .icon-btn::after{opacity:1;transform:none}}@media (max-width:860px){.faq-grid{grid-template-columns:minmax(0,1fr)}.faq-head{position:static}.qa-a p{padding-right:0}}.tip{padding-block:var(--sec);isolation:isolate}.tip-bg{position:absolute;inset:0;z-index:-1;overflow:hidden;background:var(--night)}.tip-bg canvas{position:absolute;inset:0;width:100%;height:100%;filter:blur(3px) saturate(.9) brightness(.8);transform:scale(1.18)}.tip-bg::before{content:"";position:absolute;inset:0;z-index:1;background:linear-gradient(90deg, color-mix(in oklab, var(--night) 88%, transparent) 0%, color-mix(in oklab, var(--night) 62%, transparent) 55%, color-mix(in oklab, var(--night) 30%, transparent) 100%)}.tip-bg::after{content:"";position:absolute;inset:0;z-index:2;background:var(--grain);background-size:190px;mix-blend-mode:overlay;opacity:.75}@media (max-width:860px){.tip-bg::before{background:linear-gradient(180deg, color-mix(in oklab, var(--night) 82%, transparent) 0%, color-mix(in oklab, var(--night) 60%, transparent) 55%, color-mix(in oklab, var(--night) 35%, transparent) 100%)}}.tip-grid{display:grid;grid-template-columns:minmax(0,6fr) minmax(0,5fr);gap:56px clamp(32px, 6vw, 110px);align-items:start}.tip-copy{display:grid;gap:28px;align-content:start}.tip .lede{color:color-mix(in oklab, var(--pearl) 84%, transparent)}.channels{display:grid;margin-top:12px;border-top:1px solid var(--line)}.channel{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:baseline;gap:6px 24px;padding:18px 0;border-bottom:1px solid var(--line)}.channel>span:last-child,.channel>a{color:var(--fg)}.channel .caps{color:var(--fg2)}.tip-form{--veil:0;position:relative;isolation:isolate;display:grid;gap:22px;padding:clamp(26px, 3.4vw, 48px);border-radius:var(--r-lg);background:var(--bg);color:var(--fg);box-shadow:0 40px 80px -40px color-mix(in oklab, var(--ink) 70%, transparent)}.tip-form::after{content:"";position:absolute;inset:0;z-index:5;border-radius:inherit;pointer-events:none;background:var(--frost) 0 0 / 150px, color-mix(in oklab, var(--fog) 80%, transparent);opacity:var(--veil)}.tip-form .bracket{--bk:24px;color:var(--pearl)}.tip-form .bracket--tr{top:-14px;right:-14px}.tip-form .bracket--bl{bottom:-14px;left:-14px}.tip-form-title{font-size:clamp(15px, 1.3vw, 18px)}.tip-row{position:relative;display:grid;gap:6px;padding-bottom:10px;border-bottom:1px solid var(--line)}.tip-row::after{content:"";position:absolute;left:0;right:0;bottom:-1px;height:2px;background:var(--fg);transform:scaleX(0);transition:transform .6s var(--ease)}.tip-row:focus-within::after{transform:scaleX(1)}.tip-label{font-size:14px;font-weight:600;color:var(--fg2)}.tip-row input,.tip-row textarea{width:100%;border:0;padding:6px 0;background:transparent;color:var(--fg);font-size:17px;resize:vertical;outline:none}.tip-row input::placeholder{color:color-mix(in oklab, var(--fg) 40%, transparent)}.tip-form .btn{justify-self:start}.tip-note{font-size:14px;color:var(--fg2)}.tip-form .form-status{color:var(--fg)}@media (max-width:860px){.tip-grid{grid-template-columns:minmax(0,1fr)}}@media (prefers-reduced-motion:reduce){*,*::before,*::after{transition:none !important}}.site-foot{position:relative;overflow:hidden;background:var(--ink);--bg:var(--ink);padding-top:clamp(88px, 10vw, 150px)}.foot-grid{display:grid;grid-template-columns:repeat(12, minmax(0,1fr));gap:48px 24px}.foot-news{grid-column:1 / span 5;display:grid;gap:18px;align-content:start}.foot-news .lede{max-width:40ch}.news-form{display:flex;gap:10px;flex-wrap:wrap;margin-top:8px}.news-form input{flex:1 1 220px;min-width:0;padding:1em 1.1em;border-radius:12px;border:1px solid var(--line);background:color-mix(in oklab, var(--pearl) 5%, transparent);color:var(--fg)}.news-form input::placeholder{color:color-mix(in oklab, var(--fg) 45%, transparent)}.form-status{min-height:1.5em;font-size:15px;color:var(--ember)}.foot-nav{grid-column:7 / span 6;display:grid;grid-template-columns:repeat(auto-fit, minmax(140px, 1fr));gap:32px 24px}.foot-nav h3{margin-bottom:14px;color:var(--fg2)}.foot-nav ul{display:grid;gap:10px}.foot-nav a{font-weight:500}.foot-legal{grid-column:1 / -1;display:flex;flex-wrap:wrap;justify-content:space-between;gap:12px 32px;padding-top:28px;border-top:1px solid var(--line);font-size:14px;color:var(--fg2)}.foot-mark{position:relative;margin-top:clamp(48px, 7vw, 96px);overflow:hidden}.foot-mark::before{content:"";position:absolute;inset:10% 15% -30%;z-index:0;background:radial-gradient(50% 60% at 50% 70%, color-mix(in oklab, var(--ember) 36%, transparent), transparent 100%)}.foot-word{position:relative;z-index:1;left:50%;translate:-50% 0;width:max-content;margin-bottom:-.1em;font-size:calc(96vw / (var(--len) * var(--k)));color:color-mix(in oklab, var(--fog) 40%, transparent)}.foot-mark .grain{position:absolute;inset:0;z-index:2;background:var(--grain);background-size:190px;mix-blend-mode:overlay;opacity:.9}@media (max-width:860px){.foot-grid{grid-template-columns:minmax(0,1fr)}.foot-news,.foot-nav,.foot-legal{grid-column:1 / -1}}</style>
</head>
<body>
<header class="site-head" data-tone="dark" data-section="nav">
  <a class="brand" href="#hero"><svg viewBox="0 0 24 24" aria-hidden="true"><circle cx="12" cy="12" r="2.6" fill="currentColor"/><ellipse cx="12" cy="12" rx="10" ry="4" transform="rotate(-24 12 12)" fill="none" stroke="currentColor" stroke-width="1.3"/><circle cx="21.1" cy="7.9" r="1.5" fill="currentColor"/></svg>Orrery</a>
  <nav class="nav" id="site-nav" aria-label="Main">
    <a href="#files">Capabilities</a>
    <a href="#method">Method</a>
    <a href="#people">The lab</a>
    <a href="#support">Pricing</a>
    <a class="btn" href="#tip">Request access</a>
  </nav>
  <button class="icon-btn menu-btn" type="button" aria-expanded="false" aria-controls="site-nav" aria-label="Open menu" data-label-open="Open menu" data-label-close="Close menu"><span></span></button>
</header>

<main>
  <section id="hero" class="hero" data-kind="hero" data-tone="dark" data-section="hero">
    <div class="hero-stage">
      <div class="hero-fog" aria-hidden="true"><canvas id="hero-fog"></canvas></div>
      <div class="hero-haze" aria-hidden="true"></div>
      <h1 class="hero-title">
        <span class="sr">Orrery — </span>
        <span class="giant hero-word hero-word--top" style="--len:5">Think</span>
        <span class="giant hero-word hero-word--bottom" style="--len:4">slow</span>
      </h1>
      <div class="hero-grain" aria-hidden="true"></div>
      <div class="hero-clear" aria-hidden="true"><canvas data-art="orrery" data-seed="4" data-dpr="1.5" data-mirror="hero-fog"></canvas></div>
      <div class="hero-rim" aria-hidden="true"></div>
      <span class="bracket bracket--tr hero-bracket hero-bracket--tr" aria-hidden="true"><i></i></span>
      <span class="bracket bracket--bl hero-bracket hero-bracket--bl" aria-hidden="true"><i></i></span>
      <p class="hero-lines">
        <span class="caps hero-line hero-line--a">Fast answers are cheap</span>
        <span class="caps hero-line hero-line--b">Right ones take a moment</span>
      </p>
      <a class="spaced hero-cta" href="#files">Meet Orrery 4</a>
    </div>
  </section>

  <section id="brief" class="brief" data-kind="manifesto" data-tone="light" data-section="brief">
    <div class="wrap">
      <h2 class="brief-statement" data-defog>Orrery is a reasoning engine for work that can't be guessed at. It reads the contracts, tickets, code and spreadsheets your team already has — and tells you what they add up to.</h2>
      <div class="brief-foot">
        <figure class="brief-photo framed" data-slot>
          <span class="slot"><canvas data-art="terrain" data-seed="11" role="img" aria-label="Rendered ridgelines of a latent space, one line highlighted in gold"></canvas></span>
        </figure>
        <div class="brief-text" data-reveal>
          <p class="lede">No training on your data. No ads. No black box. Every answer arrives with the sources behind it, so you can check the work line by line.</p>
          <a class="link" href="#method">How it reasons <svg viewBox="0 0 14 14" aria-hidden="true"><path d="M1 7h11M8 3l4 4-4 4" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
        </div>
      </div>
      <div class="marks" data-reveal>
        <span class="spaced">Trusted by 2,300 teams</span>
        <span class="mark"><svg viewBox="0 0 20 20" aria-hidden="true"><path d="M10 2 18 18H2z" fill="currentColor"/></svg>Kestrel Bio</span>
        <span class="mark"><svg viewBox="0 0 20 20" aria-hidden="true"><circle cx="10" cy="10" r="8" fill="none" stroke="currentColor" stroke-width="2.4"/></svg>Telluric</span>
        <span class="mark"><svg viewBox="0 0 20 20" aria-hidden="true"><rect x="3" y="3" width="14" height="14" rx="2" fill="currentColor"/></svg>Fieldhouse</span>
        <span class="mark"><svg viewBox="0 0 20 20" aria-hidden="true"><path d="M2 10h16M10 2v16" stroke="currentColor" stroke-width="3"/></svg>Annex Labs</span>
        <span class="mark"><svg viewBox="0 0 20 20" aria-hidden="true"><circle cx="7" cy="10" r="5" fill="currentColor"/><circle cx="13" cy="10" r="5" fill="none" stroke="currentColor" stroke-width="2"/></svg>Morrow &amp; Pike</span>
      </div>
    </div>
  </section>

  <section id="files" class="files" data-kind="investigations" data-tone="dark" data-section="capabilities">
    <div class="wrap">
      <div class="files-head">
        <h2 class="h2" data-reveal>The engine</h2>
        <p class="lede" data-reveal>Five systems, one model. Each took a year to get right — these are the ones teams build on.</p>
        <a class="link" href="#files" data-reveal>Read the model card <svg viewBox="0 0 14 14" aria-hidden="true"><path d="M1 7h11M8 3l4 4-4 4" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
      </div>
      <div class="files-rail">
        <ul class="files-list" role="list">
          <li class="file">
            <a class="file-link" href="#files">
              <span class="file-meta"><span class="file-year">v4.2</span><span class="file-topic">Reasoning</span></span>
              <span class="file-body"><h3 class="file-title">Deliberate mode</h3><p class="file-text">Give it a hard question and it takes minutes, not milliseconds — drafting, testing and discarding approaches before it commits to an answer.</p></span>
              <span class="slot file-photo"><canvas data-art="deliberate" data-seed="2" role="img" aria-label="A search tree exploring candidate paths, pruning them and committing to one answer"></canvas></span>
            </a>
          </li>
          <li class="file">
            <a class="file-link" href="#files">
              <span class="file-meta"><span class="file-year">v4.0</span><span class="file-topic">Memory</span></span>
              <span class="file-body"><h3 class="file-title">A context the size of your company</h3><p class="file-text">Ten million tokens of working memory. Every doc, thread and repository held at once, and recalled exactly.</p></span>
              <span class="slot file-photo"><canvas data-art="memory" data-seed="5" role="img" aria-label="Tokens streaming into a rotating sphere of memory, with recalled passages linked by arcs"></canvas></span>
            </a>
          </li>
          <li class="file">
            <a class="file-link" href="#files">
              <span class="file-meta"><span class="file-year">v3.8</span><span class="file-topic">Agents</span></span>
              <span class="file-body"><h3 class="file-title">Hands that ask first</h3><p class="file-text">Orrery acts across 400 tools — and stops to confirm anything that can't be undone.</p></span>
              <span class="slot file-photo"><canvas data-art="agents" data-seed="8" role="img" aria-label="A hub connected to orbiting tool icons, pausing on one to ask for confirmation"></canvas></span>
            </a>
          </li>
          <li class="file">
            <a class="file-link" href="#files">
              <span class="file-meta"><span class="file-year">v3.5</span><span class="file-topic">Vision</span></span>
              <span class="file-body"><h3 class="file-title">Reads the chart, not the caption</h3><p class="file-text">Scans, diagrams, whiteboards and dashboards, understood down to the axis labels and the footnotes.</p></span>
              <span class="slot file-photo"><canvas data-art="vision" data-seed="3" role="img" aria-label="A chart scanned left to right, with its axis, peak, legend and footnote boxed as they are recognised"></canvas></span>
            </a>
          </li>
          <li class="file">
            <a class="file-link" href="#files">
              <span class="file-meta"><span class="file-year">v3.1</span><span class="file-topic">Deployment</span></span>
              <span class="file-body"><h3 class="file-title">Runs where your data lives</h3><p class="file-text">Your cloud, your region, or your own racks. Nothing leaves unless you send it.</p></span>
              <span class="slot file-photo"><canvas data-art="deploy" data-seed="6" role="img" aria-label="Isometric server racks inside a sealed perimeter, with outbound traffic stopped at a lock"></canvas></span>
            </a>
          </li>
        </ul>
        <span class="bracket bracket--tr rail-bk rail-bk--tr" aria-hidden="true"><i></i></span>
        <span class="bracket bracket--bl rail-bk rail-bk--bl" aria-hidden="true"><i></i></span>
      </div>
    </div>
  </section>

  <section id="method" class="method" data-kind="process" data-tone="light" data-section="process">
    <div class="wrap">
      <div class="method-head">
        <h2 class="h2" data-reveal>How an answer gets made</h2>
        <p class="lede" data-reveal>Every response passes through the same five stages. Nothing reaches you until each one is done.</p>
      </div>
      <ul class="steps" role="list">
        <li class="step">
          <span class="step-rule" aria-hidden="true"></span>
          <p class="step-when">0.2 s</p>
          <h3 class="caps step-title">Parse the ask</h3>
          <p class="step-text">Orrery restates your question, flags anything ambiguous, and decides how hard it needs to think.</p>
        </li>
        <li class="step">
          <span class="step-rule" aria-hidden="true"></span>
          <p class="step-when">1–4 s</p>
          <h3 class="caps step-title">Evidence first</h3>
          <p class="step-text">It searches your sources before it writes a word. The documents decide whether there is an answer.</p>
        </li>
        <li class="step">
          <span class="step-rule" aria-hidden="true"></span>
          <p class="step-when">Up to 8 min</p>
          <h3 class="caps step-title">Reason in the open</h3>
          <p class="step-text">Hypotheses are drafted, tested and thrown away. Watch the working, or skip straight to the end.</p>
        </li>
        <li class="step">
          <span class="step-rule" aria-hidden="true"></span>
          <p class="step-when">Every claim</p>
          <h3 class="caps step-title">Verify twice</h3>
          <p class="step-text">Each statement is checked against at least two independent passages. Anything unsupported is cut or flagged.</p>
        </li>
        <li class="step">
          <span class="step-rule" aria-hidden="true"></span>
          <p class="step-when">After</p>
          <h3 class="caps step-title">Cite, then stay</h3>
          <p class="step-text">Answers ship with their sources. Change a document and Orrery tells you which answers it touched.</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="field" class="field" data-kind="gallery" data-tone="dark" data-section="gallery">
    <div class="field-stage">
      <div class="wrap field-head">
        <h2 class="h2">Inside the engine</h2>
        <p class="lede">Answers only go so far. These are live renderings of what Orrery is doing while it thinks.</p>
      </div>
      <div class="field-view">
        <ul class="field-track" role="list">
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="grid" data-seed="21" aria-hidden="true"></canvas></span><figcaption><span class="caps">Attention, layer 38</span><span class="shot-note">Vision · live</span></figcaption></figure></li>
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="graph" data-seed="22" aria-hidden="true"></canvas></span><figcaption><span class="caps">Retrieval graph</span><span class="shot-note">Evidence first · live</span></figcaption></figure></li>
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="stream" data-seed="23" aria-hidden="true"></canvas></span><figcaption><span class="caps">Token stream</span><span class="shot-note">Generation · live</span></figcaption></figure></li>
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="terrain" data-seed="24" aria-hidden="true"></canvas></span><figcaption><span class="caps">Latent terrain</span><span class="shot-note">Deliberate mode · live</span></figcaption></figure></li>
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="rings" data-seed="25" aria-hidden="true"></canvas></span><figcaption><span class="caps">Verifier consensus</span><span class="shot-note">Verify twice · live</span></figcaption></figure></li>
          <li class="shot"><figure><span class="slot shot-photo"><canvas data-art="lattice" data-seed="26" aria-hidden="true"></canvas></span><figcaption><span class="caps">Memory lattice</span><span class="shot-note">10M context · live</span></figcaption></figure></li>
        </ul>
      </div>
      <div class="field-pane" aria-hidden="true"></div>
      <div class="field-rim" aria-hidden="true"><span class="bracket bracket--tr"><i></i></span><span class="bracket bracket--bl"><i></i></span></div>
    </div>
  </section>

  <section id="impact" class="impact" data-kind="results" data-tone="light" data-section="results">
    <div class="wrap">
      <div class="impact-head">
        <h2 class="h2" data-reveal>What changed after</h2>
        <p class="lede" data-reveal>We count a release as finished when something moves for the teams using it: hours, errors, decisions.</p>
      </div>
      <ul class="outcomes" role="list">
        <li class="outcome"><span class="rule" data-draw aria-hidden="true"></span><p class="figure" style="--len:3"><span>41%</span></p><p class="outcome-text">fewer hours spent on research and review across customer teams</p></li>
        <li class="outcome"><span class="rule" data-draw aria-hidden="true"></span><p class="figure" style="--len:3"><span>10M</span></p><p class="outcome-text">tokens of working memory, recalled with 99.2% exact-match accuracy</p></li>
        <li class="outcome"><span class="rule" data-draw aria-hidden="true"></span><p class="figure" style="--len:1"><span>0</span></p><p class="outcome-text">bytes of customer data ever used to train a model</p></li>
        <li class="outcome"><span class="rule" data-draw aria-hidden="true"></span><p class="figure" style="--len:5"><span>2,300</span></p><p class="outcome-text">teams running Orrery in production today</p></li>
      </ul>
      <div class="funding">
        <div class="funding-copy">
          <h3 class="caps">Where an answer comes from</h3>
          <p class="funding-note">Orrery never answers from memory alone when your sources can answer instead. Audit logs export at any time.</p>
        </div>
        <ul class="bars" role="list" data-chart>
          <li class="bar"><span class="bar-label">Your sources</span><span class="bar-track"><span class="bar-fill"></span></span><span class="bar-value">71%</span></li>
          <li class="bar"><span class="bar-label">Model reasoning</span><span class="bar-track"><span class="bar-fill"></span></span><span class="bar-value">19%</span></li>
          <li class="bar"><span class="bar-label">Verification passes</span><span class="bar-track"><span class="bar-fill"></span></span><span class="bar-value">7%</span></li>
          <li class="bar"><span class="bar-label">Clarifying questions</span><span class="bar-track"><span class="bar-fill"></span></span><span class="bar-value">3%</span></li>
        </ul>
      </div>
    </div>
  </section>

  <section id="people" class="people" data-kind="team" data-tone="dark" data-section="team">
    <div class="wrap">
      <div class="people-head">
        <h2 class="h2" data-reveal>The lab</h2>
        <p class="lede" data-reveal>Forty researchers, twelve engineers and one ethicist with a veto. These four lead the work.</p>
        <a class="link" href="#tip" data-reveal>Join the lab <svg viewBox="0 0 14 14" aria-hidden="true"><path d="M1 7h11M8 3l4 4-4 4" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
      </div>
      <ul class="people-grid" role="list">
        <li class="person">
          <span class="slot person-photo" data-slot><canvas data-art="portrait" data-seed="31" aria-hidden="true"></canvas></span>
          <h3 class="caps person-name">Mira Castellane</h3>
          <p class="person-role">Chief executive</p>
          <p class="person-note">Ran applied research at two labs before Orrery. Still reads every eval report herself.</p>
        </li>
        <li class="person">
          <span class="slot person-photo" data-slot><canvas data-art="portrait" data-seed="47" aria-hidden="true"></canvas></span>
          <h3 class="caps person-name">Tomas Ferrer</h3>
          <p class="person-role">Head of research</p>
          <p class="person-note">Built the verifier that checks every claim. Re-runs the benchmarks nobody else wants to.</p>
        </li>
        <li class="person">
          <span class="slot person-photo" data-slot><canvas data-art="portrait" data-seed="52" aria-hidden="true"></canvas></span>
          <h3 class="caps person-name">Ada Lindqvist</h3>
          <p class="person-role">Interpretability</p>
          <p class="person-note">Spent nine months mapping layer 38. Made the live renderings on this page.</p>
        </li>
        <li class="person">
          <span class="slot person-photo" data-slot><canvas data-art="portrait" data-seed="64" aria-hidden="true"></canvas></span>
          <h3 class="caps person-name">Owen Hale</h3>
          <p class="person-role">Safety &amp; policy</p>
          <p class="person-note">Holds the veto on every release. Has used it four times, and we shipped better for it.</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="voices" class="voices" data-kind="reviews" data-tone="light" data-section="reviews">
    <div class="wrap">
      <h2 class="h2 voices-title" data-reveal>In their words</h2>
      <ul class="voice-stack" role="list">
        <li class="voice">
          <blockquote class="voice-quote"><p>Our analysts spent a week reconciling filings. Orrery does it overnight and shows us every page it read.</p></blockquote>
          <p class="voice-by"><span class="caps">Ruth Adebayo</span><span>Head of research, Kestrel Bio</span></p>
        </li>
        <li class="voice">
          <blockquote class="voice-quote"><p>It's the first model that tells me when it doesn't know. That alone changed how we use it.</p></blockquote>
          <p class="voice-by"><span class="caps">Colin Marsh</span><span>Staff engineer, Telluric</span></p>
        </li>
        <li class="voice">
          <blockquote class="voice-quote"><p>We gave it ten years of incident reports. It found the pattern three audits had missed.</p></blockquote>
          <p class="voice-by"><span class="caps">Dev Malhotra</span><span>VP operations, Fieldhouse</span></p>
        </li>
        <li class="voice">
          <blockquote class="voice-quote"><p>It is the one tab I open before the coffee is ready.</p></blockquote>
          <p class="voice-by"><span class="caps">Inês Carvalho</span><span>Founder, Annex Labs</span></p>
        </li>
      </ul>
    </div>
  </section>

  <section id="support" class="support" data-kind="pricing" data-tone="dark" data-section="pricing">
    <div class="wrap">
      <div class="support-head">
        <h2 class="h2" data-reveal>Choose your context</h2>
        <p class="lede" data-reveal>Start free with the full model. Upgrade when your questions get harder.</p>
        <div class="bill" role="group" aria-label="Billing period" data-reveal>
          <button class="bill-opt" type="button" aria-pressed="true" data-period="monthly">Monthly</button>
          <button class="bill-opt" type="button" aria-pressed="false" data-period="yearly">Yearly</button>
        </div>
      </div>
      <ul class="tiers" role="list">
        <li class="tier">
          <h3 class="caps tier-name">Personal</h3>
          <p class="tier-price"><span class="price" style="--len:2">$0</span><span class="per">always</span></p>
          <p class="tier-text">The full model, on your own files, for as long as you like.</p>
          <ul class="ticks" role="list"><li>Orrery 4 with standard reasoning</li><li>500K-token workspace</li><li>Cited answers, every time</li></ul>
          <a class="btn btn--ghost" href="#tip">Start free</a>
        </li>
        <li class="tier tier--key">
          <span class="bracket bracket--tr" aria-hidden="true"><i></i></span><span class="bracket bracket--bl" aria-hidden="true"><i></i></span>
          <h3 class="caps tier-name">Pro</h3>
          <p class="tier-price"><span class="price" style="--len:3" data-monthly="$24" data-yearly="$240">$24</span><span class="per" data-monthly="a month" data-yearly="a year">a month</span></p>
          <p class="tier-text">Most people who stay start here. Deliberate mode, unlocked.</p>
          <ul class="ticks" role="list"><li>Everything in Personal</li><li>Deliberate mode, up to 8 minutes</li><li>10M-token memory</li><li>Agents across 400 tools</li></ul>
          <a class="btn" href="#tip">Go Pro</a>
        </li>
        <li class="tier">
          <h3 class="caps tier-name">Team</h3>
          <p class="tier-price"><span class="price" style="--len:3" data-monthly="$60" data-yearly="$600">$60</span><span class="per" data-monthly="per seat, monthly" data-yearly="per seat, yearly">per seat, monthly</span></p>
          <p class="tier-text">Shared memory, admin controls, and deployment in your own cloud.</p>
          <ul class="ticks" role="list"><li>Everything in Pro</li><li>Private VPC or on-premises</li><li>SSO, SCIM and audit export</li><li>A named research engineer</li></ul>
          <a class="btn btn--ghost" href="#tip">Talk to us</a>
        </li>
      </ul>
      <p class="support-note">Prices in USD. Education and nonprofit teams get 50% off, always.</p>
    </div>
  </section>

  <section id="faq" class="faq" data-kind="faq" data-tone="light" data-section="faq">
    <div class="wrap faq-grid">
      <div class="faq-head">
        <h2 class="h2" data-reveal>Questions</h2>
        <p class="lede" data-reveal>If yours isn't here, ask us. A person on the team answers within one working day.</p>
        <a class="link" href="#tip" data-reveal>Ask the team <svg viewBox="0 0 14 14" aria-hidden="true"><path d="M1 7h11M8 3l4 4-4 4" fill="none" stroke="currentColor" stroke-width="1.5"/></svg></a>
      </div>
      <ul class="qa-list" role="list">
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">Is my data used to train Orrery?</span></button></h3>
          <div class="qa-a"><div><p>Never. Your files, prompts and outputs are excluded from training by contract, not by a setting, and deleted on your schedule.</p></div></div>
        </li>
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">What happens when it's wrong?</span></button></h3>
          <div class="qa-a"><div><p>It tells you how sure it is. Every claim links to its source, and anything it can't support is flagged before you ever see it.</p></div></div>
        </li>
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">Can it run on our own infrastructure?</span></button></h3>
          <div class="qa-a"><div><p>Yes. Team plans deploy to your VPC or your own racks, with the same model and the same updates as the cloud.</p></div></div>
        </li>
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">Which tools does it connect to?</span></button></h3>
          <div class="qa-a"><div><p>Over 400, from mail and calendars to data warehouses and code hosts. Agents ask before any action that can't be undone.</p></div></div>
        </li>
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">Is Orrery independently audited?</span></button></h3>
          <div class="qa-a"><div><p>Yes, every year, for both security and model behaviour. Reports are available to customers under NDA.</p></div></div>
        </li>
        <li class="qa">
          <span class="rule" data-draw aria-hidden="true"></span>
          <h3 class="qa-q"><button type="button" aria-expanded="false"><span class="icon-btn qa-icon" aria-hidden="true"><i></i></span><span class="qa-text">Can I cancel?</span></button></h3>
          <div class="qa-a"><div><p>Any time, in two clicks, with no questions asked. Yearly plans are refunded for the unused months.</p></div></div>
        </li>
      </ul>
    </div>
  </section>

  <section id="tip" class="tip" data-kind="contact" data-tone="dark" data-section="contact">
    <div class="tip-bg"><canvas data-art="graph" data-seed="77" data-parallax="7" data-dpr="1" aria-hidden="true"></canvas></div>
    <div class="wrap tip-grid">
      <div class="tip-copy">
        <h2 class="h2" data-reveal>Ready to ask something harder?</h2>
        <p class="lede" data-reveal>Tell us what your team is working on. We'll set up a private workspace, and a research engineer will walk you through it.</p>
        <ul class="channels" role="list">
          <li class="channel" data-reveal><span class="caps">Sales</span><a class="link" href="mailto:sales@orrery.example">sales@orrery.example</a></li>
          <li class="channel" data-reveal><span class="caps">Security</span><a class="link" href="mailto:security@orrery.example">security@orrery.example</a></li>
          <li class="channel" data-reveal><span class="caps">Studios</span><span>Bristol · San Francisco · Singapore</span></li>
          <li class="channel" data-reveal><span class="caps">Office hours</span><span>Weekdays 09:00–18:00, in your time zone</span></li>
        </ul>
      </div>
      <form class="tip-form" data-tone="light" data-sent="Received. A research engineer will reply within one working day." novalidate>
        <span class="bracket bracket--tr" aria-hidden="true"><i></i></span><span class="bracket bracket--bl" aria-hidden="true"><i></i></span>
        <h3 class="caps tip-form-title">Request access</h3>
        <label class="tip-row"><span class="tip-label">Your name</span><input name="name" autocomplete="name"></label>
        <label class="tip-row"><span class="tip-label">Work email</span><input name="email" type="email" autocomplete="email" placeholder="you@company.com" required></label>
        <label class="tip-row"><span class="tip-label">What will you ask it first?</span><textarea name="message" rows="5" required></textarea></label>
        <button class="btn" type="submit">Request access</button>
        <p class="tip-note">We reply within one working day. No sales sequences, ever.</p>
        <p class="form-status" role="status" aria-live="polite"></p>
      </form>
    </div>
  </section>
</main>

<footer class="site-foot" id="site-foot" data-tone="dark" data-section="footer">
  <div class="wrap foot-grid">
    <div class="foot-news">
      <h2 class="h2">The changelog</h2>
      <p class="lede">One email a month: what shipped, what we measured, and the evals behind it.</p>
      <form class="news-form" data-sent="You're on the list. The next changelog lands at the start of the month." novalidate>
        <label class="sr" for="news-email">Email address</label>
        <input id="news-email" type="email" name="email" placeholder="Your email" autocomplete="email" required>
        <button class="btn" type="submit">Subscribe</button>
        <p class="form-status" role="status" aria-live="polite"></p>
      </form>
    </div>
    <nav class="foot-nav" aria-label="Footer">
      <div><h3 class="caps">Product</h3><ul><li><a class="link" href="#files">Capabilities</a></li><li><a class="link" href="#method">Method</a></li><li><a class="link" href="#impact">Results</a></li></ul></div>
      <div><h3 class="caps">Company</h3><ul><li><a class="link" href="#support">Pricing</a></li><li><a class="link" href="#people">The lab</a></li><li><a class="link" href="#faq">Questions</a></li></ul></div>
      <div><h3 class="caps">Contact</h3><ul><li><a class="link" href="#tip">Request access</a></li><li><a class="link" href="mailto:press@orrery.example">Press</a></li><li><a class="link" href="mailto:security@orrery.example">Security</a></li></ul></div>
    </nav>
    <div class="foot-legal">
      <p>Orrery Labs · Model card · Usage policy · Responsible release policy</p>
      <p>© 2026 Orrery. Built to show its work. A fictional company made for a template demo.</p>
    </div>
  </div>
  <div class="foot-mark" aria-hidden="true">
    <span class="giant foot-word" style="--len:6">Orrery</span>
    <span class="grain"></span>
  </div>
</footer>

<!-- Procedural art engine: every visual on this page is drawn in code -->
<script>(()=>{
const PEARL='245,244,240',GOLD='214,178,138',STEEL='150,170,168',TAU=Math.PI*2;
const rng=a=>()=>{a|=0;a=a+0x6D2B79F5|0;let t=Math.imul(a^a>>>15,1|a);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296};
const bg=(c,w,h,flat)=>{if(flat){c.fillStyle=flat;c.fillRect(0,0,w,h);return}const g=c.createLinearGradient(0,0,w*.4,h);g.addColorStop(0,'#1f1e1b');g.addColorStop(1,'#0e0e0d');c.fillStyle=g;c.fillRect(0,0,w,h)};
const glow=(c,x,y,r,col,a)=>{if(!(r>0))return;const g=c.createRadialGradient(x,y,0,x,y,r);g.addColorStop(0,`rgba(${col},${a})`);g.addColorStop(1,`rgba(${col},0)`);c.fillStyle=g;c.fillRect(x-r,y-r,2*r,2*r)};
const F={};

/* Pointer for gentle parallax (hero only) */
const PT={x:0,y:0,tx:0,ty:0};
addEventListener('pointermove',e=>{PT.tx=e.clientX/innerWidth-.5;PT.ty=e.clientY/innerHeight-.5},{passive:true});

F.orrery=(w,h,R)=>{
  const cx=w*.5,cy=h*.46,B=Math.min(w*.56,h*.8),S=Math.max(.55,B/700);
  /* palettes: light / mid / dark / atmosphere */
  const PAL=[
    ['#f4efe6','#a39d94','#1d1b19','235,228,215'],
    ['#fde9c8','#d6b28a','#2e2015','214,178,138'],
    ['#e6efec','#7d8c8b','#151b1a','170,195,192'],
    ['#fff2dc','#c9a57c','#241911','226,190,145'],
    ['#f7d6bb','#b57a55','#22150e','206,140,100'],
    ['#eef4f7','#98abb5','#151c20','180,205,220'],
    ['#f5f4f0','#8c8a85','#1a1a19','230,230,225']];
  const DEF=[
    {f:.19,s:4.2},
    {f:.3,s:7.5,bands:1,label:['Reasoning','depth 0.94']},
    {f:.42,s:5.6},
    {f:.58,s:12.5,ring:1,bands:1,moons:2,label:['Memory','10M tokens']},
    {f:.72,s:9,bands:1,moons:1},
    {f:.87,s:5.8,label:['Verification','2× sourced'],ticks:1},
    {f:1.02,s:3.8,dash:1}];
  const PL=DEF.map((d,i)=>({...d,pal:PAL[i],r:B*d.f,sz:Math.max(3,d.s*S*1.55),ph:R()*TAU,
    sp:.32*Math.pow(d.f/.19,-1.5),
    bandSeed:Array.from({length:7},()=>[R()*2-1,.04+R()*.1,R()<.5]),
    moons:Array.from({length:d.moons||0},(_,k)=>({d:(2.1+k*1.1),sp:(1.1+R()*.8)*(k%2?1:1.3),ph:R()*TAU,s:.2+R()*.08}))}));

  /* dust: diffuse disc + a dense belt between orbits 3 and 4 */
  const dust=Array.from({length:1150},()=>{const belt=R()<.55;const f=belt?.485+(R()+R()-1)*.035:.1+Math.pow(R(),.75)*1.0;
    return{f,r:B*f,a:R()*TAU,sp:.32*Math.pow(Math.max(.12,f)/.19,-1.5),s:.35+R()*(belt?1.1:1.4),g:R()<(belt?.3:.12),al:.25+R()*.6,off:(R()-.5)*B*.012}});

  /* stars in three depth layers */
  const stars=Array.from({length:420},()=>({x:R()*w,y:R()*h,s:.3+Math.pow(R(),3)*1.6,a:.1+R()*.55,tw:R()*TAU,tws:.6+R()*2.2,d:.15+R()*.85,warm:R()<.25}));
  const glints=stars.filter(s=>s.s>1.1).slice(0,14);

  /* nebula: painted once at quarter resolution, upscaled for natural softness */
  const NS=4,neb=document.createElement('canvas');neb.width=Math.ceil(w/NS)+16;neb.height=Math.ceil(h/NS)+16;
  {const n=neb.getContext('2d'),nw=neb.width,nh=neb.height;
    const blob=(x,y,r,col,a)=>{const g=n.createRadialGradient(x,y,0,x,y,r);g.addColorStop(0,`rgba(${col},${a})`);g.addColorStop(.55,`rgba(${col},${a*.35})`);g.addColorStop(1,`rgba(${col},0)`);n.fillStyle=g;n.fillRect(x-r,y-r,r*2,r*2)};
    const cols=[GOLD,STEEL,'130,92,64','92,104,118','190,150,120'];
    for(let i=0;i<11;i++)blob(nw*.5+(R()-.5)*nw*.9,nh*.46+(R()-.5)*nh*.6,(.12+R()*.32)*nw,cols[i%cols.length],.05+R()*.11);
    n.save();n.translate(nw*.5,nh*.46);n.rotate(-.26);n.scale(1,.16);blob(0,0,nw*.55,GOLD,.22);blob(nw*.12,0,nw*.3,'255,236,210',.12);n.restore();
    const id=n.getImageData(0,0,nw,nh),p=id.data;for(let i=0;i<p.length;i+=4){const k=(R()-.5)*6;p[i]+=k;p[i+1]+=k;p[i+2]+=k}n.putImageData(id,0,0)}

  const sphere=(c,x,y,r,pal,lx,ly,bands,tl,seed)=>{
    c.save();c.beginPath();c.arc(x,y,r,0,TAU);c.clip();
    const g=c.createRadialGradient(x+lx*r*.5,y+ly*r*.5,r*.04,x+lx*r*.15,y+ly*r*.15,r*1.25);
    g.addColorStop(0,pal[0]);g.addColorStop(.45,pal[1]);g.addColorStop(1,pal[2]);c.fillStyle=g;c.fillRect(x-r,y-r,r*2,r*2);
    if(bands){c.save();c.translate(x,y);c.rotate(tl);for(const[o,hgt,light]of seed){c.fillStyle=light?'rgba(255,240,220,.16)':'rgba(30,18,10,.2)';c.fillRect(-r,o*r*.85,r*2,hgt*r*2)}c.restore()}
    const sh=c.createLinearGradient(x+lx*r,y+ly*r,x-lx*r,y-ly*r);
    sh.addColorStop(0,'rgba(6,5,4,0)');sh.addColorStop(.42,'rgba(6,5,4,0)');sh.addColorStop(.72,'rgba(6,5,4,.62)');sh.addColorStop(1,'rgba(6,5,4,.95)');
    c.fillStyle=sh;c.fillRect(x-r,y-r,r*2,r*2);c.restore();
    /* lit rim + atmosphere */
    const ang=Math.atan2(ly,lx);c.globalCompositeOperation='lighter';
    c.lineWidth=Math.max(.7,r*.13);c.strokeStyle=`rgba(${pal[3]},.55)`;c.beginPath();c.arc(x,y,r-c.lineWidth*.4,ang-1.15,ang+1.15);c.stroke();
    glow(c,x,y,r*2.4,pal[3],.16);glow(c,x+lx*r*.4,y+ly*r*.4,r*.7,'255,250,240',.18);
    c.globalCompositeOperation='source-over';
  };

  return(c,t)=>{
    PT.x+=(PT.tx-PT.x)*.035;PT.y+=(PT.ty-PT.y)*.035;
    const TL=-.26+PT.x*.07,SQ=.33+PT.y*.06,cT=Math.cos(TL),sT=Math.sin(TL);
    const ox=cx-PT.x*16,oy=cy-PT.y*12;
    const pos=(a,r)=>{const x=Math.cos(a)*r,y=Math.sin(a)*r*SQ;return[ox+x*cT-y*sT,oy+x*sT+y*cT,Math.sin(a)]};

    /* deep space */
    c.fillStyle='#0b0a09';c.fillRect(0,0,w,h);
    c.globalCompositeOperation='lighter';
    c.drawImage(neb,-8*NS-PT.x*30+Math.sin(t*.035)*16,-8*NS-PT.y*22+Math.cos(t*.03)*10,neb.width*NS,neb.height*NS);
    for(const s of stars){const tw=.55+.45*Math.sin(t*s.tws+s.tw);let x=(s.x-PT.x*s.d*40)%w;if(x<0)x+=w;const y=s.y-PT.y*s.d*28;
      c.fillStyle=`rgba(${s.warm?GOLD:PEARL},${s.a*tw})`;c.fillRect(x,y,s.s,s.s)}
    for(const s of glints){const tw=.4+.6*Math.pow(.5+.5*Math.sin(t*s.tws*.6+s.tw),2);let x=(s.x-PT.x*s.d*40)%w;if(x<0)x+=w;const y=s.y-PT.y*s.d*28,L=s.s*7*tw;
      c.strokeStyle=`rgba(255,248,236,${.35*tw})`;c.lineWidth=.6;c.beginPath();c.moveTo(x-L,y);c.lineTo(x+L,y);c.moveTo(x,y-L);c.lineTo(x,y+L);c.stroke();glow(c,x,y,s.s*5,'255,244,228',.25*tw)}
    c.globalCompositeOperation='source-over';

    /* orbit paths, ticks */
    const orbits=front=>{c.lineWidth=1;
      for(const p of PL){c.strokeStyle=`rgba(${PEARL},${front?.17:.06})`;if(p.dash)c.setLineDash([1.5,6]);c.beginPath();c.ellipse(ox,oy,p.r,p.r*SQ,TL,front?0:Math.PI,front?Math.PI:TAU);c.stroke();c.setLineDash([])
        if(p.ticks){c.beginPath();for(let k=0;k<180;k++){const a=k/180*TAU+t*.004,[x,y,z]=pos(a,p.r);if((z>0)!==front)continue;const L=(k%15?3:9)*S,dx=ox-x,dy=oy-y,m=Math.hypot(dx,dy)||1;c.moveTo(x,y);c.lineTo(x+dx/m*L,y+dy/m*L)}c.strokeStyle=`rgba(${PEARL},${front?.28:.1})`;c.stroke()}}};

    const dustPass=front=>{c.globalCompositeOperation='lighter';
      for(const d of dust){const a=d.a+t*d.sp,[x,y,z]=pos(a,d.r);if((z>0)!==front)continue;const al=d.al*(front?.7:.28)*(1-Math.abs(d.f-.6)*.3);
        c.fillStyle=d.g?`rgba(${GOLD},${al})`:`rgba(${PEARL},${al*.75})`;c.fillRect(x,y+d.off,d.s,d.s)}
      c.globalCompositeOperation='source-over'};

    const drawPlanet=(p,a)=>{const[x,y,z]=pos(a,p.r),k=1+.16*z,r=p.sz*k;
      let lx=ox-x,ly=oy-y;const m=Math.hypot(lx,ly)||1;lx/=m;ly/=m;
      /* comet-soft trail */
      const L=Math.min(1.05,.35+p.sp*2.2),N=16;c.lineCap='round';c.globalCompositeOperation='lighter';
      for(let i=0;i<N;i++){const a0=a-L*(1-i/N),a1=a-L*(1-(i+1)/N),[x0,y0]=pos(a0,p.r),[x1,y1]=pos(a1,p.r);
        c.lineWidth=Math.max(.8,r*.42*(i/N));c.strokeStyle=`rgba(${p.pal[3]},${Math.pow(i/N,2.2)*(.35+.25*z)})`;c.beginPath();c.moveTo(x0,y0);c.lineTo(x1,y1);c.stroke()}
      c.globalCompositeOperation='source-over';
      const ringTL=TL+.38,ringPass=back=>{if(!p.ring)return;const rw=[[1.55,.2],[1.72,.42],[1.86,.14],[2.0,.5],[2.18,.3],[2.34,.12]];
        for(const[f,al]of rw){c.lineWidth=Math.max(.6,r*.13);c.strokeStyle=`rgba(${GOLD},${al*(back?.55:1)})`;c.beginPath();c.ellipse(x,y,r*f,r*f*.3,ringTL,back?Math.PI:0,back?TAU:Math.PI);c.stroke()}};
      const moonPos=mn=>{const ma=mn.ph+t*mn.sp,dx=Math.cos(ma)*r*mn.d,dy=Math.sin(ma)*r*mn.d*.32;return[x+dx*cT-dy*sT,y+dx*sT+dy*cT,Math.sin(ma)]};
      const moons=front=>{for(const mn of p.moons){const[mx,my,mz]=moonPos(mn);if((mz>0)!==front)continue;let a2=ox-mx,b2=oy-my;const q=Math.hypot(a2,b2)||1;sphere(c,mx,my,Math.max(1.2,r*mn.s),PAL[6],a2/q,b2/q,0,TL,null)}};
      moons(false);ringPass(true);
      sphere(c,x,y,r,p.pal,lx,ly,p.bands,TL,p.bandSeed);
      ringPass(false);moons(true);
      return[x,y,z,r]};

    const planets=front=>{const out=[];
      const list=PL.map(p=>{const a=p.ph+t*p.sp;return{p,a,z:Math.sin(a)}}).filter(o=>(o.z>0)===front).sort((u,v)=>u.z-v.z);
      for(const o of list)out.push([o.p,drawPlanet(o.p,o.a)]);return out};

    orbits(false);dustPass(false);const back=planets(false);

    /* the sun */
    const pl=1+.035*Math.sin(t*1.3)+.015*Math.sin(t*3.7),cr=Math.max(5,B*.03);
    c.globalCompositeOperation='lighter';
    glow(c,ox,oy,B*1.15,GOLD,.08);glow(c,ox,oy,B*.4*pl,GOLD,.2);glow(c,ox,oy,B*.13*pl,'255,232,200',.38);
    c.lineWidth=1;for(let k=0;k<72;k++){const ang=k/72*TAU+t*.012,n=.5+.5*Math.sin(k*7.13+t*.6)*Math.cos(k*2.91-t*.41),len=B*(.035+.15*n*n),r0=cr*1.3;
      c.strokeStyle=`rgba(255,226,190,${.025+.08*n})`;c.beginPath();c.moveTo(ox+Math.cos(ang)*r0,oy+Math.sin(ang)*r0);c.lineTo(ox+Math.cos(ang)*(r0+len),oy+Math.sin(ang)*(r0+len));c.stroke()}
    c.strokeStyle=`rgba(${GOLD},.22)`;c.beginPath();c.arc(ox,oy,cr*2.1*pl,0,TAU);c.stroke();
    c.strokeStyle=`rgba(${GOLD},.08)`;c.beginPath();c.arc(ox,oy,cr*3.6*pl,0,TAU);c.stroke();
    c.globalCompositeOperation='source-over';
    {const g=c.createRadialGradient(ox-cr*.25,oy-cr*.25,0,ox,oy,cr);g.addColorStop(0,'#ffffff');g.addColorStop(.55,'#fff4e0');g.addColorStop(1,'#f0c995');c.fillStyle=g;c.beginPath();c.arc(ox,oy,cr*pl,0,TAU);c.fill()}
    c.globalCompositeOperation='lighter';glow(c,ox,oy,cr*2.4,'255,250,240',.45);c.globalCompositeOperation='source-over';

    orbits(true);dustPass(true);const front=planets(true);

    /* lens: anamorphic streak + ghosts */
    c.globalCompositeOperation='lighter';
    c.save();c.translate(ox,oy);c.scale(1,.03);glow(c,0,0,w*.55,GOLD,.24);c.restore();
    {const sg=c.createLinearGradient(ox-w*.48,0,ox+w*.48,0);sg.addColorStop(0,`rgba(${GOLD},0)`);sg.addColorStop(.5,'rgba(255,246,232,.42)');sg.addColorStop(1,`rgba(${GOLD},0)`);c.fillStyle=sg;c.fillRect(ox-w*.48,oy-.7,w*.96,1.4)}
    {let gx=Math.cos(.62+t*.025)+PT.x*1.2,gy=Math.sin(.62+t*.025)*.7+PT.y*1.2;const m=Math.hypot(gx,gy)||1;gx/=m;gy/=m;
      for(const[d,rr,col,al,hex]of[[.28,.03,STEEL,.12,0],[.52,.065,GOLD,.06,1],[.82,.11,STEEL,.045,0],[1.1,.022,GOLD,.14,0],[1.35,.05,'190,150,220',.04,1]]){
        const x=ox+gx*B*d,y=oy+gy*B*d,R2=B*rr;glow(c,x,y,R2,col,al);
        c.strokeStyle=`rgba(${col},${al*1.4})`;c.lineWidth=1;c.beginPath();
        if(hex){for(let k=0;k<=6;k++){const a=k/6*TAU+.3;k?c.lineTo(x+Math.cos(a)*R2*.8,y+Math.sin(a)*R2*.8):c.moveTo(x+Math.cos(a)*R2*.8,y+Math.sin(a)*R2*.8)}}else c.arc(x,y,R2*.8,0,TAU);c.stroke()}}
    c.globalCompositeOperation='source-over';

    /* instrument labels: collision-aware, sticky placement */
    const fs=Math.round(10*Math.max(.95,Math.min(1.25,S))),F1=`700 ${fs}px "Hubot Sans", system-ui, sans-serif`,F2=`600 ${fs-1}px "Hubot Sans", system-ui, sans-serif`;
    try{c.letterSpacing='2.5px'}catch(e){}
    const all=[...back,...front],taken=all.map(([,[x,y,,r]])=>({l:x-r-4,r:x+r+4,t:y-r-4,b:y+r+4}));taken.push({l:ox-cr*2.2,r:ox+cr*2.2,t:oy-cr*2.2,b:oy+cr*2.2});
    const hit=a=>a.l<8||a.r>w-8||a.t<8||a.b>h-8||taken.some(o=>a.l<o.r+10&&a.r>o.l-10&&a.t<o.b+8&&a.b>o.t-8);
    const CAND=[[1,-1],[1,1],[-1,-1],[-1,1]];
    for(const[p,[x,y,z,r]]of all.filter(([q])=>q.label).sort((m,n)=>n[1][2]-m[1][2])){
      const tgt=Math.max(0,Math.min(1,(z+.5)/.6))*.9;
      c.font=F1;const w1=c.measureText(p.label[0].toUpperCase()).width;c.font=F2;const tw=Math.max(w1,c.measureText(p.label[1]).width)+4;
      const order=p.lc!=null?[p.lc,0,1,2,3].filter((v,k,arr)=>arr.indexOf(v)===k):[0,1,2,3];let pick=null;
      if(tgt>.01)for(const ci of order){const[sx,sy]=CAND[ci],d=(r+12*S)*.8,x1=x+sx*d,y1=y+sy*d,x2=x1+sx*30*S,te=x2+sx*(8+tw);
        const box={l:Math.min(x2,te),r:Math.max(x2,te),t:y1-fs,b:y1+fs*2+4};if(!hit(box)){pick={ci,sx,sy,x1,y1,x2,box};break}}
      if(pick&&p.lc!=null&&pick.ci!==p.lc&&(p.la||0)>.05){pick=null}
      p.la=(p.la||0)+((pick?tgt:0)-(p.la||0))*.18;if(pick)p.lc=pick.ci;
      const al=p.la;if(al<.02||p.lc==null)continue;
      if(!pick){const[sx,sy]=CAND[p.lc],d=(r+12*S)*.8,x1=x+sx*d,y1=y+sy*d,x2=x1+sx*30*S,te=x2+sx*(8+tw);const bx={l:Math.min(x2,te),r:Math.max(x2,te),t:y1-fs,b:y1+fs*2+4};if(taken.slice(all.length+1).some(o=>bx.l<o.r+10&&bx.r>o.l-10&&bx.t<o.b+8&&bx.b>o.t-8)){p.la=0;continue}pick={sx,sy,x1,y1,x2,box:bx}}
      taken.push(pick.box);const{sx,sy,x1,y1,x2}=pick;
      c.strokeStyle=`rgba(${PEARL},${al*.55})`;c.lineWidth=1;c.beginPath();c.moveTo(x+sx*r*.75,y+sy*r*.75);c.lineTo(x1,y1);c.lineTo(x2,y1);c.stroke();
      c.fillStyle=`rgba(${GOLD},${al})`;c.fillRect(x2-1.5,y1-1.5,3,3);
      c.textAlign=sx<0?'right':'left';c.textBaseline='middle';c.font=F1;c.fillStyle=`rgba(${PEARL},${al})`;c.fillText(p.label[0].toUpperCase(),x2+sx*8,y1-1);
      c.font=F2;c.fillStyle=`rgba(${GOLD},${al*.85})`;c.fillText(p.label[1],x2+sx*8,y1+fs+2)}
    try{c.letterSpacing='0px'}catch(e){}c.textAlign='left';

    /* cinematic vignette */
    const v=c.createRadialGradient(ox,oy,B*.35,ox,oy,Math.hypot(w,h)*.62);v.addColorStop(0,'rgba(8,7,6,0)');v.addColorStop(1,'rgba(8,7,6,.78)');c.fillStyle=v;c.fillRect(0,0,w,h);
  };
};

/* ===== Premium engine renderers ===== */
const pTxt=(c,s,x,y,col,al,size=9,align='left',wt=700)=>{c.font=`${wt} ${size}px "Hubot Sans", system-ui, sans-serif`;try{c.letterSpacing='1.6px'}catch(e){}c.textAlign=align;c.textBaseline='middle';c.fillStyle=`rgba(${col},${al})`;c.fillText(s,x,y);try{c.letterSpacing='0px'}catch(e){}c.textAlign='left'};
const pBase=(c,w,h,fx,fy)=>{c.fillStyle='#0c0b0a';c.fillRect(0,0,w,h);c.globalCompositeOperation='lighter';glow(c,w*fx,h*fy,Math.max(w,h)*.7,GOLD,.12);glow(c,w*(1-fx),h*(1-fy)+h*.2,Math.max(w,h)*.5,STEEL,.06);c.globalCompositeOperation='source-over'};
const pVig=(c,w,h)=>{const v=c.createRadialGradient(w/2,h/2,Math.min(w,h)*.35,w/2,h/2,Math.hypot(w,h)*.62);v.addColorStop(0,'rgba(8,7,6,0)');v.addColorStop(1,'rgba(8,7,6,.72)');c.fillStyle=v;c.fillRect(0,0,w,h)};
const pBr=(c,x,y,bw,bh,cl)=>{c.moveTo(x,y+cl);c.lineTo(x,y);c.lineTo(x+cl,y);c.moveTo(x+bw-cl,y);c.lineTo(x+bw,y);c.lineTo(x+bw,y+cl);c.moveTo(x+bw,y+bh-cl);c.lineTo(x+bw,y+bh);c.lineTo(x+bw-cl,y+bh);c.moveTo(x+cl,y+bh);c.lineTo(x,y+bh);c.lineTo(x,y+bh-cl)};
const pHud=(c,w,h,tl,tr)=>{const m=12;c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.34)`;c.beginPath();pBr(c,m,m,w-2*m,h-2*m,9);c.stroke();
  pTxt(c,tl.toUpperCase(),m+16,m+5,PEARL,.62);pTxt(c,tr.toUpperCase(),w-m-16,m+5,GOLD,.92,9,'right');
  c.beginPath();for(let x=m+18,k=0;x<w-m-18;x+=6,k++){c.moveTo(x,h-m);c.lineTo(x,h-m-(k%10?2:5))}c.strokeStyle=`rgba(${PEARL},.13)`;c.stroke()};

/* 1 · Deliberate mode — a search tree that explores, prunes, commits */
F.deliberate=(w,h,R)=>{
  const LV=5,x0=w*.1,x1=w*.84,cy=h*.56,nodes=[{x:x0,y:cy,l:0,p:-1,win:true,kids:0}];let frontier=[0];
  for(let l=1;l<=LV;l++){const nf=[];
    for(const pi of frontier){const par=nodes[pi];if(!par.win&&l>2&&R()<.28)continue;const kids=par.win?3:(R()<.55?1:2);
      for(let k=0;k<kids;k++){const win=par.win&&k===0,spread=h*.3*(1-l/(LV+2));
        let y=win?(l===LV?cy:cy+(par.y-cy)*.35+(R()-.5)*h*.14):par.y+(R()-.5)*2*spread;y=Math.max(h*.3,Math.min(h*.82,y));
        nodes.push({x:x0+(x1-x0)*l/LV+(win?0:(R()-.5)*w*.025),y,l,p:pi,win,kids:0});par.kids++;nf.push(nodes.length-1)}}
    const wi=nf.find(i=>nodes[i].win);frontier=[wi,...nf.filter(i=>i!==wi).slice(0,12)]}
  const end=nodes.find(n=>n.win&&n.l===LV),P=8.5;
  const byLevel=l=>nodes.filter(n=>n.l<=l).length;
  return(c,t)=>{pBase(c,w,h,.78,.5);const u=(t%P)/P,grow=Math.min(1,u/.6)*LV,commit=Math.max(0,Math.min(1,(u-.62)/.12)),fade=u>.93?1-(u-.93)/.07:Math.min(1,u/.03);
    c.strokeStyle=`rgba(${PEARL},.05)`;c.lineWidth=1;c.beginPath();for(let l=0;l<=LV;l++){const x=x0+(x1-x0)*l/LV;c.moveTo(x,h*.24);c.lineTo(x,h*.86)}c.stroke();
    for(let l=1;l<=LV;l++)pTxt(c,'D'+l,x0+(x1-x0)*l/LV,h*.9,PEARL,.22,8,'center');
    if(commit<1){const fx=x0+(x1-x0)*grow/LV,g=c.createLinearGradient(fx-46,0,fx,0);g.addColorStop(0,`rgba(${GOLD},0)`);g.addColorStop(1,`rgba(${GOLD},${.16*(1-commit)})`);c.fillStyle=g;c.fillRect(fx-46,h*.22,46,h*.66);c.fillStyle=`rgba(255,238,214,${.7*(1-commit)})`;c.fillRect(fx,h*.22,1,h*.66)}
    c.lineCap='round';
    for(let i=1;i<nodes.length;i++){const n=nodes[i],p=nodes[n.p],f=Math.max(0,Math.min(1,grow-(n.l-1)));if(f<=0)continue;const dx=n.x-p.x;
      const bz=s=>{const a=1-s;return[a*a*a*p.x+3*a*a*s*(p.x+dx*.5)+3*a*s*s*(n.x-dx*.5)+s*s*s*n.x,a*a*a*p.y+3*a*a*s*p.y+3*a*s*s*n.y+s*s*s*n.y]};
      const gold=n.win&&commit>0;let al=n.win?.55+.45*commit:.4*(1-commit*.8);al*=fade;
      if(gold){c.shadowColor=`rgba(${GOLD},.9)`;c.shadowBlur=10*commit}
      c.strokeStyle=`rgba(${gold?GOLD:PEARL},${al})`;c.lineWidth=n.win?1.2+commit*1.3:1;c.beginPath();const S=20;for(let k=0;k<=Math.floor(S*f);k++){const[x,y]=bz(k/S);k?c.lineTo(x,y):c.moveTo(x,y)}c.stroke();c.shadowBlur=0;
      if(f>=1){const r=n.win?2.6:1.7;c.fillStyle=gold?`rgba(${GOLD},${fade})`:`rgba(${PEARL},${(n.win?.9:.65*(1-commit*.7))*fade})`;c.beginPath();c.arc(n.x,n.y,r,0,TAU);c.fill();
        if(!n.win&&n.kids===0&&commit>0){const q=3;c.strokeStyle=`rgba(${PEARL},${.35*commit*fade})`;c.lineWidth=1;c.beginPath();c.moveTo(n.x+4,n.y-q);c.lineTo(n.x+4+2*q,n.y+q);c.moveTo(n.x+4+2*q,n.y-q);c.lineTo(n.x+4,n.y+q);c.stroke()}}}
    c.globalCompositeOperation='lighter';glow(c,x0,cy,20,GOLD,.55*fade);
    if(commit>0){const pl=.5+.5*Math.sin(t*4);glow(c,end.x,end.y,30+pl*8,GOLD,.55*commit*fade);glow(c,end.x,end.y,10,'255,248,236',.9*commit*fade);
      const k=(t*.9)%1;c.strokeStyle=`rgba(${GOLD},${.5*(1-k)*commit*fade})`;c.lineWidth=1;c.beginPath();c.arc(end.x,end.y,6+k*22,0,TAU);c.stroke()}
    c.globalCompositeOperation='source-over';
    if(commit>0){pTxt(c,'ANSWER',end.x,end.y-20,PEARL,.9*commit*fade,9,'center');pTxt(c,'conf 0.97',end.x,end.y+20,GOLD,.9*commit*fade,8,'center',600)}
    pVig(c,w,h);
    pHud(c,w,h,'Deliberate · search',commit>0?'committed · 0.97':`exploring ${byLevel(Math.floor(grow))} paths`)};
};

/* 2 · Memory — a sphere of recalled context */
F.memory=(w,h,R)=>{
  const N=620,pts=[],ga=Math.PI*(3-Math.sqrt(5));for(let i=0;i<N;i++){const y=1-2*(i+.5)/N,r=Math.sqrt(1-y*y),a=i*ga;pts.push([Math.cos(a)*r,y,Math.sin(a)*r])}
  const hot=Array.from({length:14},()=>Math.floor(R()*N)),cx=w*.66,cy=h*.55,Rad=Math.min(h*.33,w*.2);
  const stream=Array.from({length:70},()=>({y:(R()-.5)*h*.55,o:R(),sp:.1+R()*.18,l:5+R()*24,g:R()<.16}));
  return(c,t)=>{pBase(c,w,h,.66,.55);
    for(const s of stream){const u=(s.o+t*s.sp)%1,x=w*.07+(cx-Rad*.95-w*.07)*u,y=cy+s.y*(1-u*u),al=Math.sin(Math.PI*u)*.55;c.fillStyle=s.g?`rgba(${GOLD},${al})`:`rgba(${PEARL},${al*.55})`;c.fillRect(x,y,s.l*(1-u*.7),1.6)}
    const ry=t*.22,rx=.42,cY=Math.cos(ry),sY=Math.sin(ry),cX=Math.cos(rx),sX=Math.sin(rx),scan=Math.sin(t*.6)*.85;
    const P=pts.map(([x,y,z])=>{const x1=x*cY+z*sY,z1=-x*sY+z*cY,y1=y*cX-z1*sX,z2=y*sX+z1*cX,s=3/(3+z2);return[cx+x1*s*Rad,cy+y1*s*Rad,z2,y]});
    c.globalCompositeOperation='lighter';glow(c,cx,cy,Rad*1.7,GOLD,.13);glow(c,cx-Rad*.3,cy-Rad*.35,Rad*.9,PEARL,.05);
    for(const[x,y,z,lat]of P){const d=(1-z)/2,sc=Math.exp(-Math.pow((lat-scan)/.05,2)),s=.6+1.4*d;
      c.fillStyle=sc>.15?`rgba(${GOLD},${.15+(.35+.6*d)*sc})`:`rgba(${PEARL},${.06+.6*d*d})`;c.fillRect(x-s/2,y-s/2,s,s)}
    const k=Math.floor(t/2.4),ph=(t/2.4)%1;let lab=null;
    for(let j=0;j<3;j++){const a=P[hot[(k+j*4)%hot.length]],b=P[hot[(k+j*4+1)%hot.length]],mx=(a[0]+b[0])/2,my=(a[1]+b[1])/2,ctrl=[cx+(mx-cx)*1.7,cy+(my-cy)*1.7-Rad*.25],al=Math.sin(Math.PI*ph)*(1-j*.28);
      c.strokeStyle=`rgba(${GOLD},${al*.85})`;c.lineWidth=1.1;c.beginPath();c.moveTo(a[0],a[1]);c.quadraticCurveTo(ctrl[0],ctrl[1],b[0],b[1]);c.stroke();
      glow(c,a[0],a[1],9,GOLD,al*.8);glow(c,b[0],b[1],9,GOLD,al*.8);const q=1-ph;glow(c,q*q*a[0]+2*q*ph*ctrl[0]+ph*ph*b[0],q*q*a[1]+2*q*ph*ctrl[1]+ph*ph*b[1],7,'255,242,222',al);
      if(j===0)lab=[b,al]}
    c.globalCompositeOperation='source-over';
    const A=Rad*1.32,Bv=A*.26,tl=-.18;c.strokeStyle=`rgba(${PEARL},.2)`;c.lineWidth=1;c.beginPath();c.ellipse(cx,cy,A,Bv,tl,0,TAU);c.stroke();
    c.setLineDash([1.5,4]);c.beginPath();c.ellipse(cx,cy,A*1.12,Bv*1.12,tl,0,TAU);c.stroke();c.setLineDash([]);
    const ma=t*.7,ex=Math.cos(ma)*A,ey=Math.sin(ma)*Bv,sx=cx+ex*Math.cos(tl)-ey*Math.sin(tl),sy=cy+ex*Math.sin(tl)+ey*Math.cos(tl);
    c.globalCompositeOperation='lighter';glow(c,sx,sy,10,GOLD,.7);c.globalCompositeOperation='source-over';c.fillStyle='#fff3e0';c.fillRect(sx-1.5,sy-1.5,3,3);
    if(lab&&lab[1]>.2){const[p,al]=lab,lx=cx-Rad*1.25,ly=cy-Rad*.78;c.strokeStyle=`rgba(${PEARL},${al*.5})`;c.lineWidth=1;c.beginPath();c.moveTo(p[0],p[1]);c.lineTo(lx+8,ly);c.lineTo(lx,ly);c.stroke();c.fillStyle=`rgba(${GOLD},${al})`;c.fillRect(lx-1.5,ly-1.5,3,3);
      pTxt(c,'RECALL',lx-7,ly-6,PEARL,al,8,'right');pTxt(c,'doc 4,812 · p.31',lx-7,ly+6,GOLD,al*.9,8,'right',600)}
    pTxt(c,'10,000,000',w*.07,cy+h*.33,PEARL,.5,8);pTxt(c,'TOKENS IN',w*.07,cy+h*.33-11,PEARL,.3,8);
    pVig(c,w,h);pHud(c,w,h,'Memory · 10M context','recall 99.2%')};
};

/* 3 · Agents — a hub that acts across tools, and stops to ask */
F.agents=(w,h,R)=>{
  const cx=w*.5,cy=h*.58,A=Math.min(w*.37,h*1.15),Bv=h*.26,G=['mail','cal','db','code','chart','doc','chat','card'],nodes=G.map((g,i)=>({g,ph:i/G.length*TAU,off:R()})),P=9;
  const glyph=(c,g,x,y,s)=>{c.beginPath();switch(g){
    case'mail':c.rect(x-s,y-s*.7,s*2,s*1.4);c.moveTo(x-s,y-s*.7);c.lineTo(x,y+s*.1);c.lineTo(x+s,y-s*.7);break;
    case'cal':c.rect(x-s,y-s*.8,s*2,s*1.7);c.moveTo(x-s,y-s*.3);c.lineTo(x+s,y-s*.3);c.moveTo(x-s*.4,y-s);c.lineTo(x-s*.4,y-s*.6);c.moveTo(x+s*.4,y-s);c.lineTo(x+s*.4,y-s*.6);break;
    case'db':c.ellipse(x,y-s*.6,s,s*.32,0,0,TAU);c.moveTo(x-s,y-s*.6);c.lineTo(x-s,y+s*.6);c.moveTo(x+s,y-s*.6);c.lineTo(x+s,y+s*.6);c.moveTo(x+s,y+s*.6);c.ellipse(x,y+s*.6,s,s*.32,0,0,Math.PI);break;
    case'code':c.moveTo(x-s*.3,y-s*.7);c.lineTo(x-s,y);c.lineTo(x-s*.3,y+s*.7);c.moveTo(x+s*.3,y-s*.7);c.lineTo(x+s,y);c.lineTo(x+s*.3,y+s*.7);break;
    case'chart':c.moveTo(x-s,y-s*.8);c.lineTo(x-s,y+s*.8);c.lineTo(x+s,y+s*.8);c.moveTo(x-s*.6,y+s*.3);c.lineTo(x-s*.1,y-s*.2);c.lineTo(x+s*.3,y+s*.1);c.lineTo(x+s*.9,y-s*.6);break;
    case'doc':c.rect(x-s*.75,y-s,s*1.5,s*2);c.moveTo(x-s*.4,y-s*.4);c.lineTo(x+s*.4,y-s*.4);c.moveTo(x-s*.4,y);c.lineTo(x+s*.4,y);c.moveTo(x-s*.4,y+s*.4);c.lineTo(x+s*.1,y+s*.4);break;
    case'chat':c.ellipse(x,y-s*.1,s,s*.7,0,0,TAU);c.moveTo(x-s*.3,y+s*.55);c.lineTo(x-s*.7,y+s);c.lineTo(x,y+s*.6);break;
    default:c.rect(x-s,y-s*.65,s*2,s*1.3);c.moveTo(x-s,y-s*.25);c.lineTo(x+s,y-s*.25);c.moveTo(x-s*.6,y+s*.3);c.lineTo(x-s*.1,y+s*.3)}c.stroke()};
  return(c,t)=>{pBase(c,w,h,.5,.58);const rot=t*.1,cyc=Math.floor(t/P),u=(t%P)/P,ci=(cyc*3)%nodes.length,confirming=u>.12&&u<.82;
    const pos=nodes.map((n,i)=>{const a=n.ph+rot;return{i,n,x:cx+Math.cos(a)*A,y:cy+Math.sin(a)*Bv,z:Math.sin(a)}});
    c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.1)`;c.beginPath();c.ellipse(cx,cy,A,Bv,0,0,TAU);c.stroke();c.setLineDash([2,5]);c.beginPath();c.ellipse(cx,cy,A*.55,Bv*.55,0,0,TAU);c.stroke();c.setLineDash([]);
    c.globalCompositeOperation='lighter';
    for(const p of pos){const isC=p.i===ci&&confirming,d=(1+p.z)/2;c.strokeStyle=`rgba(${isC?GOLD:PEARL},${isC?.55:.07+.12*d})`;c.beginPath();c.moveTo(cx,cy);c.lineTo(p.x,p.y);c.stroke();
      if(isC){const s=u<.62?.6:.6+(u-.62)/.2*.4,px=cx+(p.x-cx)*s,py=cy+(p.y-cy)*s,pl=.5+.5*Math.sin(t*6);glow(c,px,py,9+pl*4,GOLD,.7)}
      else{const s=(t*.45+p.n.off)%1,px=cx+(p.x-cx)*s,py=cy+(p.y-cy)*s;glow(c,px,py,5,PEARL,.45*d)}}
    glow(c,cx,cy,h*.5,GOLD,.16);glow(c,cx,cy,h*.13,'255,236,210',.55);c.globalCompositeOperation='source-over';
    c.fillStyle='#fff6e6';c.beginPath();c.arc(cx,cy,Math.max(3,h*.024),0,TAU);c.fill();
    c.strokeStyle=`rgba(${GOLD},.4)`;c.beginPath();c.arc(cx,cy,h*.065+Math.sin(t*2)*1.5,0,TAU);c.stroke();c.strokeStyle=`rgba(${GOLD},.15)`;c.beginPath();c.arc(cx,cy,h*.11,0,TAU);c.stroke();
    const sc=Math.min(1.35,Math.max(.8,h/180));
    for(const p of[...pos].sort((a,b)=>a.z-b.z)){const d=(1+p.z)/2,s=(8+5*d)*sc,isC=p.i===ci&&confirming;
      const g=c.createLinearGradient(p.x,p.y-s,p.x,p.y+s);g.addColorStop(0,'#2a2724');g.addColorStop(1,'#141312');c.fillStyle=g;c.strokeStyle=isC?`rgba(${GOLD},.95)`:`rgba(${PEARL},${.2+.4*d})`;c.lineWidth=1;
      c.beginPath();c.roundRect(p.x-s,p.y-s,s*2,s*2,s*.38);c.fill();c.stroke();
      c.strokeStyle=isC?`rgba(${GOLD},1)`:`rgba(${PEARL},${.35+.55*d})`;glyph(c,p.n.g,p.x,p.y,s*.45);
      if(isC){const k=(t*1.1)%1,e=k*9;c.strokeStyle=`rgba(${GOLD},${.6*(1-k)})`;c.beginPath();c.roundRect(p.x-s-e,p.y-s-e,(s+e)*2,(s+e)*2,s*.38+e*.6);c.stroke();
        const ok=u>=.62,ty=p.y<cy?p.y+s+11:p.y-s-11;pTxt(c,ok?'APPROVED':'CONFIRM?',p.x,ty,ok?PEARL:GOLD,.95,8,'center')}}
    pVig(c,w,h);pHud(c,w,h,'Agents · 400 tools',confirming?(u<.62?'awaiting approval':'approved · running'):`${(12+cyc*7)%97} actions`)};
};

/* 4 · Vision — a chart being read element by element */
F.vision=(w,h,R)=>{
  const L=w*.2,Rr=w*.82,T=h*.36,Bt=h*.72,n=26,d1=[],d2=[];let v=.28,v2=.5;
  for(let i=0;i<n;i++){v+=(R()-.42)*.13;v=Math.max(.08,Math.min(.86,v));d1.push(v);v2+=(R()-.5)*.08;v2=Math.max(.15,Math.min(.85,v2));d2.push(v2)}
  let pk=0;d1.forEach((y,i)=>{if(y>d1[pk])pk=i});d1[pk]=Math.min(.97,d1[pk]+.1);
  const X=i=>L+(Rr-L)*i/(n-1),Y=q=>Bt-(Bt-T)*q,P=7.5,pkRight=X(pk)>Rr-120;
  const boxes=[{x:L-28,y:T-4,w:22,h:Bt-T+8,label:'AXIS · USD M',lx:L-28,ly:T-11,at:L-28},
    {x:X(pk)-8,y:Y(d1[pk])-8,w:16,h:16,label:'PEAK +38%',lx:pkRight?X(pk)-12:X(pk)+14,ly:Y(d1[pk]),align:pkRight?'right':'left',at:X(pk)},
    {x:Rr-74,y:T-24,w:74,h:12,label:'LEGEND · 2',lx:Rr-80,ly:T-18,align:'right',at:Rr-74},
    {x:L,y:Bt+9,w:(Rr-L)*.5,h:10,label:'FOOTNOTE',lx:L+(Rr-L)*.5+8,ly:Bt+14,at:L}];
  const path=(c,d)=>{c.beginPath();d.forEach((q,i)=>i?c.lineTo(X(i),Y(q)):c.moveTo(X(i),Y(q)))};
  return(c,t)=>{pBase(c,w,h,.35,.45);const u=(t%P)/P,sx=L-34+(Rr+24-(L-34))*Math.min(1,u/.68),fade=u>.92?1-(u-.92)/.08:1;
    c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.07)`;c.beginPath();for(let k=0;k<=4;k++){const y=T+(Bt-T)*k/4;c.moveTo(L,y);c.lineTo(Rr,y)}for(let i=0;i<n;i+=5){c.moveTo(X(i),T);c.lineTo(X(i),Bt)}c.stroke();
    c.strokeStyle=`rgba(${PEARL},.42)`;c.beginPath();c.moveTo(L,T-2);c.lineTo(L,Bt);c.lineTo(Rr,Bt);c.stroke();
    c.fillStyle=`rgba(${PEARL},.3)`;for(let k=0;k<=4;k++)c.fillRect(L-22,T+(Bt-T)*k/4-1,14,2);
    c.fillStyle=`rgba(${PEARL},.55)`;c.fillRect(Rr-70,T-19,9,2);c.fillStyle=`rgba(${PEARL},.25)`;c.fillRect(Rr-58,T-19,18,2);c.fillStyle=`rgba(${STEEL},.6)`;c.fillRect(Rr-34,T-19,9,2);c.fillStyle=`rgba(${PEARL},.25)`;c.fillRect(Rr-22,T-19,18,2);
    c.fillStyle=`rgba(${PEARL},.18)`;c.fillRect(L,Bt+11,(Rr-L)*.48,2);c.fillRect(L,Bt+16,(Rr-L)*.3,2);
    path(c,d1);c.lineTo(Rr,Bt);c.lineTo(L,Bt);c.closePath();let g=c.createLinearGradient(0,T,0,Bt);g.addColorStop(0,`rgba(${PEARL},.1)`);g.addColorStop(1,`rgba(${PEARL},0)`);c.fillStyle=g;c.fill();
    c.setLineDash([3,4]);path(c,d2);c.strokeStyle=`rgba(${STEEL},.6)`;c.stroke();c.setLineDash([]);path(c,d1);c.strokeStyle=`rgba(${PEARL},.5)`;c.lineWidth=1.2;c.stroke();
    c.save();c.beginPath();c.rect(0,0,Math.max(0,sx),h);c.clip();
    path(c,d1);c.lineTo(Rr,Bt);c.lineTo(L,Bt);c.closePath();g=c.createLinearGradient(0,T,0,Bt);g.addColorStop(0,`rgba(${GOLD},${.3*fade})`);g.addColorStop(1,`rgba(${GOLD},0)`);c.fillStyle=g;c.fill();
    path(c,d1);c.strokeStyle=`rgba(${GOLD},${fade})`;c.lineWidth=1.6;c.shadowColor=`rgba(${GOLD},.8)`;c.shadowBlur=8;c.stroke();c.shadowBlur=0;
    c.fillStyle=`rgba(255,240,220,${fade})`;d1.forEach((q,i)=>c.fillRect(X(i)-1.2,Y(q)-1.2,2.4,2.4));c.restore();
    if(u<.7){g=c.createLinearGradient(sx-56,0,sx,0);g.addColorStop(0,`rgba(${GOLD},0)`);g.addColorStop(1,`rgba(${GOLD},.2)`);c.fillStyle=g;c.fillRect(sx-56,h*.2,56,h*.66);c.fillStyle='rgba(255,240,220,.85)';c.fillRect(sx,h*.2,1,h*.66);
      c.globalCompositeOperation='lighter';glow(c,sx,h*.2,10,GOLD,.6);glow(c,sx,h*.86,10,GOLD,.6);c.globalCompositeOperation='source-over'}
    let det=0;
    for(const b of boxes){if(sx<b.at)continue;det++;const e=1-Math.pow(1-Math.min(1,(sx-b.at)/40),3),pad=(1-e)*10,x=b.x-pad,y=b.y-pad,bw=b.w+pad*2,bh=b.h+pad*2;
      c.fillStyle=`rgba(${GOLD},${.07*e*fade})`;c.fillRect(x,y,bw,bh);c.strokeStyle=`rgba(${GOLD},${e*fade})`;c.lineWidth=1.2;c.beginPath();pBr(c,x,y,bw,bh,Math.min(6,bw/3,bh/3));c.stroke();
      pTxt(c,b.label,b.lx,b.ly,GOLD,e*fade,8,b.align||'left')}
    pVig(c,w,h);pHud(c,w,h,'Vision · parse',`${det}/4 elements`)};
};

/* 5 · Deployment — isometric racks inside a sealed perimeter */
F.deploy=(w,h,R)=>{
  const s=Math.min(h*.105,w*.06),C=Math.cos(Math.PI/6),ox=w*.45,oy=h*.14+s*.7,iso=(x,y,z=0)=>[ox+(x-y)*C*s,oy+(x+y)*.5*s-z*s];
  const racks=[{x:.7,y:1.5,a:1.1,b:1.35,H:2.5},{x:2.35,y:1.5,a:1.1,b:1.35,H:3.2},{x:4,y:1.5,a:1.1,b:1.35,H:2.1}].map(r=>({...r,leds:Array.from({length:Math.floor((r.H-.3)/.32)},()=>({ph:R()*TAU,rt:1+R()*5,gold:R()<.4}))}));
  const loop=[[.4,.4],[5.6,.4],[5.6,5.6],[.4,5.6]],segL=5.2,parts=Array.from({length:16},()=>({o:R(),sp:.03+R()*.03}));
  const loopAt=u=>{u=((u%1)+1)%1;const f=u*4,i=Math.floor(f),k=f-i,a=loop[i],b=loop[(i+1)%4];return[a[0]+(b[0]-a[0])*k,a[1]+(b[1]-a[1])*k]};
  const poly=(c,pts,fill,stroke)=>{c.beginPath();pts.forEach((p,i)=>i?c.lineTo(p[0],p[1]):c.moveTo(p[0],p[1]));c.closePath();if(fill){c.fillStyle=fill;c.fill()}if(stroke){c.strokeStyle=stroke;c.stroke()}};
  return(c,t)=>{pBase(c,w,h,.42,.55);c.lineWidth=1;
    c.strokeStyle=`rgba(${PEARL},.05)`;c.beginPath();for(let i=-3;i<=10;i++){let[a,b]=[iso(i,-3),iso(i,10)];c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1]);[a,b]=[iso(-3,i),iso(10,i)];c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1])}c.stroke();
    const per=[iso(0,0),iso(6,0),iso(6,6),iso(0,6)];poly(c,per,`rgba(${GOLD},.05)`);
    c.globalCompositeOperation='lighter';{const m=iso(3,3);glow(c,m[0],m[1],s*5,GOLD,.12)}c.globalCompositeOperation='source-over';
    c.setLineDash([4,4]);c.lineDashOffset=-t*10;poly(c,per,null,`rgba(${GOLD},.75)`);c.setLineDash([]);
    poly(c,[iso(0,0,.45),iso(6,0,.45),iso(6,6,.45),iso(0,6,.45)],null,`rgba(${GOLD},.14)`);
    c.strokeStyle=`rgba(${GOLD},.1)`;c.beginPath();for(const[x,y]of[[0,0],[6,0],[6,6],[0,6]]){const a=iso(x,y),b=iso(x,y,.45);c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1])}c.stroke();
    poly(c,loop.map(([x,y])=>iso(x,y)),null,`rgba(${PEARL},.12)`);
    c.strokeStyle=`rgba(${PEARL},.1)`;c.beginPath();for(const r of racks){const a=iso(r.x+r.a/2,r.y+r.b),b=iso(r.x+r.a/2,5.6);c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1])}c.stroke();
    c.globalCompositeOperation='lighter';
    for(const p of parts){const[x,y]=loopAt(p.o+t*p.sp),q=iso(x,y);glow(c,q[0],q[1],6,GOLD,.7);c.fillStyle='rgba(255,240,220,.9)';c.fillRect(q[0]-1,q[1]-1,2,2)}
    racks.forEach((r,i)=>{const u=(t*.35+i*.33)%1,q=iso(r.x+r.a/2,r.y+r.b+(5.6-r.y-r.b)*u);glow(c,q[0],q[1],5,PEARL,.6)});
    const eu=Math.min(1,((t*.4)%1.4)),ex=5.6+.4*eu,eq=iso(ex,4);glow(c,eq[0],eq[1],6,GOLD,.6*(eu<1?1:0));
    c.globalCompositeOperation='source-over';
    c.setLineDash([2,4]);c.strokeStyle=`rgba(${PEARL},.18)`;c.beginPath();let a=iso(6,4),b=iso(9.4,4);c.moveTo(a[0],a[1]);c.lineTo(b[0],b[1]);c.stroke();c.setLineDash([]);
    pTxt(c,'PUBLIC NET',b[0]+6,b[1],PEARL,.3,8);
    for(const r of racks){const{x,y,a:A,b:Bb,H}=r;
      poly(c,[iso(x+A,y,0),iso(x+A,y+Bb,0),iso(x+A,y+Bb,H),iso(x+A,y,H)],'#151413',`rgba(${PEARL},.14)`);
      const fg=c.createLinearGradient(0,iso(x,y+Bb,H)[1],0,iso(x,y+Bb,0)[1]);fg.addColorStop(0,'#2e2b27');fg.addColorStop(1,'#1c1a18');
      poly(c,[iso(x,y+Bb,0),iso(x+A,y+Bb,0),iso(x+A,y+Bb,H),iso(x,y+Bb,H)],fg,`rgba(${PEARL},.18)`);
      poly(c,[iso(x,y,H),iso(x+A,y,H),iso(x+A,y+Bb,H),iso(x,y+Bb,H)],'#423d37',`rgba(${PEARL},.25)`);
      c.strokeStyle=`rgba(${GOLD},.55)`;c.beginPath();let p=iso(x,y+Bb,H),q=iso(x+A,y+Bb,H);c.moveTo(p[0],p[1]);c.lineTo(q[0],q[1]);c.stroke();
      c.strokeStyle=`rgba(${PEARL},.1)`;c.beginPath();r.leds.forEach((l,k)=>{const z=.3+k*.32;p=iso(x+.1,y+Bb,z);q=iso(x+A-.1,y+Bb,z);c.moveTo(p[0],p[1]);c.lineTo(q[0],q[1])});c.stroke();
      r.leds.forEach((l,k)=>{const z=.3+k*.32+.15,on=Math.sin(t*l.rt+l.ph)>-.2,q2=iso(x+A-.22,y+Bb,z),q3=iso(x+A-.4,y+Bb,z);
        c.fillStyle=on?(l.gold?`rgba(${GOLD},1)`:`rgba(${STEEL},.9)`):'rgba(80,78,72,.6)';c.fillRect(q2[0]-1,q2[1]-1,2,2);c.fillStyle=`rgba(${PEARL},.35)`;c.fillRect(q3[0]-1,q3[1]-.5,2,1);
        if(on&&l.gold){c.globalCompositeOperation='lighter';glow(c,q2[0],q2[1],5,GOLD,.5);c.globalCompositeOperation='source-over'}})}
    {const L=iso(6,4,.3),pl=.5+.5*Math.sin(t*3);c.globalCompositeOperation='lighter';glow(c,L[0],L[1],12+pl*4,GOLD,.35);c.globalCompositeOperation='source-over';
      c.fillStyle='#1a1816';c.strokeStyle=`rgba(${GOLD},1)`;c.lineWidth=1.2;c.beginPath();c.roundRect(L[0]-4.5,L[1]-2,9,7,1.5);c.fill();c.stroke();c.beginPath();c.arc(L[0],L[1]-2,2.8,Math.PI,TAU);c.stroke()}
    pVig(c,w,h);pHud(c,w,h,'Private VPC · eu-west','egress 0 B')};
};

F.waves=(w,h,R)=>{
  const n=Math.max(18,Math.round(h/8)),fs=Array.from({length:4},()=>({k:.6+R()*2.4,s:(.25+R()*.55)*(R()<.5?-1:1),p:R()*TAU,a:.4+R()*.8})),hi=Math.floor(n*(.35+R()*.3));
  return(c,t)=>{bg(c,w,h);glow(c,w*.5,h*.5,Math.max(w,h)*.6,GOLD,.07);
    for(let i=0;i<n;i++){const y0=h*(i+.5)/n,mid=1-Math.abs(i-n/2)/(n/2);c.beginPath();
      for(let x=0;x<=w+5;x+=5){const u=x/w,env=Math.pow(Math.max(0,Math.sin(Math.PI*u)),1.5);let d=0;for(const f of fs)d+=f.a*Math.sin(u*f.k*TAU+t*f.s+f.p+i*.21);const y=y0+d*h*.05*env*(.4+mid);x?c.lineTo(x,y):c.moveTo(x,y)}
      if(i===hi){c.strokeStyle=`rgba(${GOLD},.95)`;c.lineWidth=1.6;c.shadowColor=`rgba(${GOLD},.9)`;c.shadowBlur=14}else{c.strokeStyle=`rgba(${PEARL},${.07+.3*mid})`;c.lineWidth=1;c.shadowBlur=0}c.stroke()}
    c.shadowBlur=0};
};

F.grid=(w,h,R)=>{
  const cell=Math.max(9,Math.min(w,h)/16),cols=Math.ceil(w/cell),rows=Math.ceil(h/cell),ph=R()*TAU,heads=Array.from({length:5},()=>({u:R(),v:R(),s:.06+R()*.1}));
  return(c,t)=>{bg(c,w,h,'#121211');const q=Math.floor(t*2.4)%rows;
    for(let r=0;r<rows;r++)for(let k=0;k<cols;k++){const u=k/cols,v=r/rows,d=u-v;
      let val=.7*Math.exp(-d*d*50)+.2*(.5+.5*Math.sin(k*.33+t*.8+ph)*Math.cos(r*.29-t*.5));
      for(const hd of heads){const du=u-hd.u-Math.sin(t*.2+hd.s*30)*.05,dv=v-hd.v;val+=.55*Math.exp(-(du*du+dv*dv)/(hd.s*hd.s))}
      const qr=r===q;if(qr)val+=.25;val=Math.min(1,val);
      c.fillStyle=val>.62?`rgba(${GOLD},${val})`:`rgba(${PEARL},${val*(qr?.6:.42)})`;
      c.fillRect(k*cell+1,r*cell+1,cell-2,cell-2)}
  };
};

F.graph=(w,h,R)=>{
  const N=Math.min(70,Math.round(18+w*h/9000));
  const nodes=Array.from({length:N},()=>({x:R()*w,y:R()*h,r:1.2+R()*2.4,hub:R()<.12,ph:R()*TAU}));
  const edges=[];nodes.forEach((a,i)=>{const near=nodes.map((b,j)=>({j,d:(a.x-b.x)**2+(a.y-b.y)**2})).filter(o=>o.j!==i).sort((p,q)=>p.d-q.d).slice(0,3);near.forEach(o=>{if(!edges.some(e=>(e.a===o.j&&e.b===i)))edges.push({a:i,b:o.j,ph:R(),sp:.12+R()*.35,on:R()<.45})})});
  return(c,t)=>{bg(c,w,h);glow(c,w*.6,h*.4,Math.max(w,h)*.55,GOLD,.08);
    const P=nodes.map(n=>({x:n.x+Math.sin(t*.3+n.ph)*6,y:n.y+Math.cos(t*.25+n.ph)*5}));
    c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.13)`;c.beginPath();for(const e of edges){c.moveTo(P[e.a].x,P[e.a].y);c.lineTo(P[e.b].x,P[e.b].y)}c.stroke();
    for(const e of edges){if(!e.on)continue;const p=(t*e.sp+e.ph)%1,x=P[e.a].x+(P[e.b].x-P[e.a].x)*p,y=P[e.a].y+(P[e.b].y-P[e.a].y)*p;glow(c,x,y,9,GOLD,.55);c.fillStyle=`rgba(${GOLD},1)`;c.fillRect(x-1,y-1,2,2)}
    nodes.forEach((n,i)=>{const p=P[i];if(n.hub){const k=.5+.5*Math.sin(t*1.5+n.ph);c.strokeStyle=`rgba(${GOLD},${.35+.4*k})`;c.beginPath();c.arc(p.x,p.y,7+k*3,0,TAU);c.stroke();glow(c,p.x,p.y,22,GOLD,.25)}
      c.fillStyle=`rgba(${PEARL},${n.hub?1:.75})`;c.beginPath();c.arc(p.x,p.y,n.hub?3.2:n.r,0,TAU);c.fill()});
  };
};

F.stream=(w,h,R)=>{
  const lh=Math.max(12,h/20),rows=Math.ceil(h/lh)+1;
  const lines=Array.from({length:rows},()=>{let L=0;const arr=[];while(L<w*1.6){const tw=6+Math.pow(R(),2)*54;arr.push({x:L,w:tw,g:R()<.07,a:.12+R()*.28});L+=tw+5}return{arr,L,sp:14+R()*36}});
  return(c,t)=>{bg(c,w,h);const cur=w*.64;glow(c,cur,h*.5,w*.45,GOLD,.08);
    lines.forEach((ln,r)=>{const y=r*lh+lh*.3,th=lh*.42,off=(t*ln.sp)%ln.L;
      for(const tk of ln.arr)for(const rep of [0,ln.L]){const x=tk.x-off+rep;if(x>w||x+tk.w<0)continue;
        const near=Math.exp(-Math.pow((x-cur)/(w*.12),2)),ahead=x>cur;
        if(tk.g&&!ahead)c.fillStyle=`rgba(${GOLD},.9)`;else c.fillStyle=`rgba(${PEARL},${(tk.a+near*.5)*(ahead?.18:1)})`;
        c.fillRect(x,y,tk.w,th)}});
    const g=c.createLinearGradient(0,0,0,h);g.addColorStop(0,`rgba(${GOLD},0)`);g.addColorStop(.5,`rgba(${GOLD},1)`);g.addColorStop(1,`rgba(${GOLD},0)`);
    c.fillStyle=g;c.shadowColor=`rgba(${GOLD},.9)`;c.shadowBlur=16;c.fillRect(cur-1,0,2,h);c.shadowBlur=0};
};

F.terrain=(w,h,R)=>{
  const n=Math.max(16,Math.round(h/11)),fs=Array.from({length:5},()=>({k:3+R()*10,s:.15+R()*.4,p:R()*TAU,a:.3+R()})),cx=.35+R()*.3,hi=Math.floor(n*.55);
  return(c,t)=>{bg(c,w,h,'#121211');glow(c,w*cx,h*.3,w*.55,GOLD,.1);
    const top=h*.16,span=h*.8;
    for(let i=0;i<n;i++){const y0=top+span*i/(n-1),pts=[];
      for(let x=0;x<=w+4;x+=4){const u=x/w,env=Math.exp(-Math.pow((u-cx)/.2,2))+.3*Math.exp(-Math.pow((u-cx-.27)/.07,2));let d=0;for(const f of fs)d+=f.a*Math.sin(u*f.k+i*.37*f.a+t*f.s+f.p);pts.push(x,y0-Math.abs(d)*env*h*.085-env*h*.03)}
      c.beginPath();c.moveTo(0,h);for(let j=0;j<pts.length;j+=2)c.lineTo(pts[j],pts[j+1]);c.lineTo(w,h);c.closePath();c.fillStyle='#121211';c.fill();
      c.beginPath();for(let j=0;j<pts.length;j+=2)j?c.lineTo(pts[j],pts[j+1]):c.moveTo(pts[j],pts[j+1]);
      if(i===hi){c.strokeStyle=`rgba(${GOLD},.95)`;c.shadowColor=`rgba(${GOLD},.8)`;c.shadowBlur=10;c.lineWidth=1.4}else{c.strokeStyle=`rgba(${PEARL},${.14+.6*(i/n)})`;c.shadowBlur=0;c.lineWidth=1}c.stroke()}
    c.shadowBlur=0};
};

F.rings=(w,h,R)=>{
  const cx=w*.5,cy=h*.5,m=Math.min(w*.9,h*1.6);
  const rings=Array.from({length:8},(_,i)=>{const arcs=[];let a=R()*TAU;const cnt=2+Math.floor(R()*5);for(let j=0;j<cnt;j++){const len=.2+R()*1.2;arcs.push([a,len]);a+=len+.15+R()*.6}return{r:m*(.08+i*.052),sp:(.08+R()*.35)*(i%2?-1:1),arcs,gold:R()<.28,lw:R()<.3?2:1}});
  return(c,t)=>{bg(c,w,h);glow(c,cx,cy,m*.55,GOLD,.12);
    c.strokeStyle=`rgba(${PEARL},.18)`;c.lineWidth=1;c.beginPath();const rt=m*.5;for(let k=0;k<120;k++){const a=k/120*TAU+t*.03,l=k%10?4:10;c.moveTo(cx+Math.cos(a)*rt,cy+Math.sin(a)*rt);c.lineTo(cx+Math.cos(a)*(rt+l),cy+Math.sin(a)*(rt+l))}c.stroke();
    for(const rg of rings){c.lineWidth=rg.lw;c.strokeStyle=rg.gold?`rgba(${GOLD},.9)`:`rgba(${PEARL},.42)`;for(const[a0,len]of rg.arcs){c.beginPath();c.arc(cx,cy,rg.r,a0+t*rg.sp,a0+len+t*rg.sp);c.stroke()}}
    const p=(t*.3)%1;c.strokeStyle=`rgba(${GOLD},${.6*(1-p)})`;c.lineWidth=1;c.beginPath();c.arc(cx,cy,m*.05+p*m*.42,0,TAU);c.stroke();
    glow(c,cx,cy,m*.09,PEARL,.9);c.fillStyle='#fffaf2';c.beginPath();c.arc(cx,cy,m*.018*(1+.2*Math.sin(t*2)),0,TAU);c.fill()};
};

F.lattice=(w,h,R)=>{
  const G=6,pts=[];for(let i=0;i<G;i++)for(let j=0;j<G;j++)for(let k=0;k<G;k++)pts.push({p:[i/(G-1)*2-1,j/(G-1)*2-1,k/(G-1)*2-1],g:R()<.08,ph:R()*TAU});
  const idx=(i,j,k)=>i*G*G+j*G+k,edges=[];for(let i=0;i<G;i++)for(let j=0;j<G;j++)for(let k=0;k<G;k++){if(i<G-1)edges.push([idx(i,j,k),idx(i+1,j,k)]);if(j<G-1)edges.push([idx(i,j,k),idx(i,j+1,k)]);if(k<G-1)edges.push([idx(i,j,k),idx(i,j,k+1)])}
  const cx=w*.5,cy=h*.5,S=Math.min(w,h*1.4)*.28,f=3.4,ph=R()*TAU;
  return(c,t)=>{bg(c,w,h);glow(c,cx,cy,Math.max(w,h)*.5,GOLD,.08);
    const ry=t*.22+ph,rx=.55+Math.sin(t*.17)*.15,cY=Math.cos(ry),sY=Math.sin(ry),cX=Math.cos(rx),sX=Math.sin(rx);
    const P=pts.map(o=>{let[x,y,z]=o.p;let x1=x*cY+z*sY,z1=-x*sY+z*cY;let y1=y*cX-z1*sX,z2=y*sX+z1*cX;const s=f/(f+z2);return{x:cx+x1*s*S,y:cy+y1*s*S,d:(1-z2)/2,s}});
    c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.09)`;c.beginPath();for(const[a,b]of edges){c.moveTo(P[a].x,P[a].y);c.lineTo(P[b].x,P[b].y)}c.stroke();
    pts.forEach((o,i)=>{const p=P[i];if(o.g){const k=.5+.5*Math.sin(t*2+o.ph);glow(c,p.x,p.y,14*p.s,GOLD,.5*k);c.fillStyle=`rgba(${GOLD},${.5+.5*k})`}else c.fillStyle=`rgba(${PEARL},${.2+.7*p.d})`;c.beginPath();c.arc(p.x,p.y,(o.g?2.2:1)+1.2*p.d,0,TAU);c.fill()});
  };
};

F.portrait=(w,h,R)=>{
  const tint=[GOLD,PEARL,STEEL][Math.floor(R()*3)],tilt=(R()-.5)*.14,hx=w*(.5+(R()-.5)*.05),hy=h*(.37+R()*.03),hr=w*(.15+R()*.03),sp=3,ph=R()*TAU;let grad=null;
  const shape=c=>{c.beginPath();c.ellipse(hx,hy,hr,hr*1.3,tilt,0,TAU);c.rect(hx-hr*.42,hy+hr,hr*.84,h*.2);c.ellipse(w*.5,h*1.04,w*.47,h*.33,0,0,TAU)};
  return(c,t)=>{bg(c,w,h);glow(c,w*.22,h*.12,w*1.1,tint,.14);
    c.lineWidth=1;c.strokeStyle=`rgba(${PEARL},.045)`;c.beginPath();for(let y=1;y<h;y+=sp){c.moveTo(0,y);c.lineTo(w,y)}c.stroke();
    if(!grad){grad=c.createLinearGradient(hx-hr*1.6,hy-hr,hx+hr*1.8,hy+hr*2.2);grad.addColorStop(0,`rgba(${PEARL},.95)`);grad.addColorStop(.55,`rgba(${tint},.55)`);grad.addColorStop(1,`rgba(${PEARL},.08)`)}
    c.save();shape(c);c.clip();const band=((t*.09+ph/TAU)%1.3-.15)*h;
    for(let y=1,i=0;y<h;y+=sp,i++){const near=Math.exp(-Math.pow((y-band)/(h*.05),2));c.lineWidth=.6+1.1*(.5+.5*Math.sin(i*.45+ph+t*.6));c.strokeStyle=grad;c.globalAlpha=.65+.35*near;c.beginPath();c.moveTo(0,y);c.lineTo(w,y);c.stroke();
      if(near>.05){c.globalAlpha=near*.7;c.strokeStyle=`rgb(${GOLD})`;c.beginPath();c.moveTo(0,y);c.lineTo(w,y);c.stroke()}}
    c.restore();c.globalAlpha=1};
};

const reduce=matchMedia('(prefers-reduced-motion: reduce)').matches;
let T=7.3;const items=[];
const paint=it=>{if(!it.draw)return;it.ctx.save();try{it.draw(it.ctx,T)}catch(e){console.error(e)}it.ctx.restore();
  if(it.mirror){const m=it.mirror,mw=Math.max(1,Math.round(it.w/4)),mh=Math.max(1,Math.round(it.h/4));if(m.width!==mw||m.height!==mh){m.width=mw;m.height=mh}m.getContext('2d').drawImage(it.cv,0,0,mw,mh)}};
const size=it=>{const p=it.cv.parentElement,w=p.clientWidth,h=p.clientHeight;if(!w||!h||(w===it.w&&h===it.h))return;const d=Math.min(window.devicePixelRatio||1,it.max);
  it.cv.width=Math.round(w*d);it.cv.height=Math.round(h*d);it.ctx.setTransform(d,0,0,d,0,0);it.w=w;it.h=h;it.draw=F[it.type](w,h,rng(it.seed*7919+13));paint(it)};
const ro=new ResizeObserver(es=>es.forEach(e=>items.forEach(it=>{if(it.cv.parentElement===e.target)size(it)})));
const io=new IntersectionObserver(es=>es.forEach(e=>{const it=items.find(i=>i.cv===e.target);if(it)it.vis=e.isIntersecting}),{rootMargin:'160px'});
document.querySelectorAll('canvas[data-art]').forEach(cv=>{const type=cv.dataset.art;if(!F[type])return;
  const it={cv,ctx:cv.getContext('2d'),type,seed:+cv.dataset.seed||1,max:+cv.dataset.dpr||2,w:0,h:0,vis:false,draw:null,mirror:cv.dataset.mirror?document.getElementById(cv.dataset.mirror):null};
  items.push(it);size(it);ro.observe(cv.parentElement);io.observe(cv)});
if(!reduce){let last=performance.now();const loop=now=>{T+=Math.min(.05,(now-last)/1000);last=now;for(const it of items)if(it.vis)paint(it);requestAnimationFrame(loop)};requestAnimationFrame(loop)}
})();</script>

<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js"></script>
<script>(()=>{const init=(sel,fn)=>document.querySelectorAll(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});const root=document.documentElement;let lenis=null;const setMenu=open=>{root.classList.toggle('menu-open',open);const btn=document.querySelector('.menu-btn');if(btn){btn.setAttribute('aria-expanded',String(open));const l=btn.dataset[open?'labelClose':'labelOpen'];if(l)btn.setAttribute('aria-label',l)}if(lenis)open?lenis.stop():lenis.start()};init('.menu-btn',btn=>btn.addEventListener('click',()=>setMenu(!root.classList.contains('menu-open'))));document.addEventListener('keydown',e=>{if(e.key==='Escape'&&root.classList.contains('menu-open'))setMenu(false)});document.addEventListener('click',e=>{const a=e.target.closest&&e.target.closest('a[href^="#"]');if(!a)return;const id=a.getAttribute('href');if(root.classList.contains('menu-open'))setMenu(false);if(id.length<2)return;const t=document.getElementById(id.slice(1));if(!t)return;e.preventDefault();if(lenis)lenis.scrollTo(t,{duration:1.4});else t.scrollIntoView()});init('.site-head',head=>{let last=scrollY,tone=head.dataset.tone||'dark',marks=[],half=38;const read=()=>{half=head.offsetHeight/2;marks=[...document.querySelectorAll('main > [data-tone], body > footer[data-tone]')].map(el=>({top:el.getBoundingClientRect().top+scrollY,tone:el.dataset.tone}))};const onScroll=()=>{const y=scrollY,d=y-last;last=y;if(y<120||root.classList.contains('menu-open'))head.classList.remove('is-hidden');else if(d>0)head.classList.add('is-hidden');else if(d<-3)head.classList.remove('is-hidden');head.classList.toggle('is-solid',y>40&&!head.classList.contains('is-hidden'));const probe=y+half;let t=marks.length?marks[0].tone:tone;for(const m of marks)if(m.top<=probe)t=m.tone;if(t!==tone){tone=t;head.dataset.tone=t}};onScroll();addEventListener('scroll',onScroll,{passive:true});if(document.readyState==='complete')read();else addEventListener('load',read);addEventListener('resize',read);document.addEventListener('layout:changed',()=>{read();onScroll()})});init('.qa-list',list=>{const items=[...list.querySelectorAll('.qa')];items.forEach(qa=>{const btn=qa.querySelector('.qa-q button');if(!btn)return;btn.addEventListener('click',()=>{const open=!qa.classList.contains('is-open');items.forEach(o=>{o.classList.remove('is-open');const b=o.querySelector('.qa-q button');if(b)b.setAttribute('aria-expanded','false')});qa.classList.toggle('is-open',open);btn.setAttribute('aria-expanded',String(open))})})});init('form[data-sent]',form=>{const status=form.querySelector('.form-status');form.addEventListener('submit',e=>{e.preventDefault();if(!form.checkValidity()){form.reportValidity();return}if(status)status.textContent=form.dataset.sent;form.reset()})});init('.steps, .voice-stack',list=>[...list.children].forEach((li,i)=>li.style.setProperty('--i',i)));init('.support',sec=>{const opts=[...sec.querySelectorAll('.bill-opt')];if(!opts.length)return;const set=period=>{opts.forEach(o=>o.setAttribute('aria-pressed',String(o.dataset.period===period)));sec.querySelectorAll('[data-'+period+']').forEach(el=>{const t=el.dataset[period];if(t==null)return;el.textContent=t;if(el.classList.contains('price'))el.style.setProperty('--len',t.length)})};opts.forEach(o=>o.addEventListener('click',()=>set(o.dataset.period)))});init('[data-chart]',chart=>{const bars=[...chart.querySelectorAll('.bar')].map(bar=>({fill:bar.querySelector('.bar-fill'),text:(bar.querySelector('.bar-value')||{}).textContent||''}));const nums=bars.map(b=>parseFloat(b.text.replace(/[^\d.,-]/g,'').replace(',','.'))||0);const pct=bars.every(b=>b.text.includes('%')),max=pct?100:Math.max(1,...nums);bars.forEach((b,i)=>{if(b.fill)b.fill.style.setProperty('--v',Math.max(0,Math.min(1,nums[i]/max)))})});if(!root.classList.contains('motion')||!window.gsap||!window.ScrollTrigger)return;gsap.registerPlugin(ScrollTrigger);if(window.SplitText)gsap.registerPlugin(SplitText);const desk=matchMedia('(min-width: 1024px) and (hover: hover)').matches;if(window.Lenis){lenis=new Lenis({lerp:0.1});lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0)}ScrollTrigger.config({ignoreMobileResize:true});ScrollTrigger.addEventListener('refresh',()=>document.dispatchEvent(new Event('layout:changed')));const queue=[];const later=fn=>queue.push(fn);const idle=window.requestIdleCallback?cb=>requestIdleCallback(cb,{timeout:700}):cb=>setTimeout(cb,30);const drain=()=>{const fn=queue.shift();if(!fn){ScrollTrigger.refresh();return}try{fn()}catch(e){console.error(e)}idle(drain)};const onView=(els,fn,margin='0px 0px -12% 0px')=>{if(!els.length)return;const io=new IntersectionObserver(entries=>{const hits=entries.filter(e=>e.isIntersecting).map(e=>e.target);hits.forEach(el=>io.unobserve(el));if(hits.length)fn(hits)},{rootMargin:margin});els.forEach(el=>io.observe(el))};later(()=>{const reveals=[...document.querySelectorAll('[data-reveal]')];gsap.set(reveals,{y:36});onView(reveals,els=>gsap.to(els,{opacity:1,y:0,duration:1.2,ease:'expo.out',stagger:.08,clearProps:'transform'}))});later(()=>onView([...document.querySelectorAll('[data-slot]')],els=>els.forEach(el=>{const cv=el.querySelector('canvas');if(cv)gsap.to(cv,{clipPath:'inset(0% 0% 0% 0% round 10px)',duration:1.6,ease:'expo.inOut'})}),'0px 0px -18% 0px'));later(()=>{const draws=[...document.querySelectorAll('[data-draw]')];gsap.set(draws,{scaleX:0,transformOrigin:'0 50%'});onView(draws,els=>gsap.to(els,{scaleX:1,duration:1.4,ease:'expo.out',stagger:.06}))});later(()=>init('[data-parallax]',el=>{const v=parseFloat(el.dataset.parallax)||10;gsap.fromTo(el,{yPercent:-v},{yPercent:v,ease:'none',scrollTrigger:{trigger:el.parentElement,start:'top bottom',end:'bottom top',scrub:true}})}));later(()=>onView([...document.querySelectorAll('[data-defog]')],els=>els.forEach(el=>{if(!window.SplitText)return;try{SplitText.create(el,{type:'lines',linesClass:'fog-line',autoSplit:true,onSplit:self=>gsap.fromTo(self.lines,desk?{opacity:.12,y:16,filter:'blur(9px)'}:{opacity:.12,y:16},{...desk?{filter:'blur(0px)'}:{},opacity:1,y:0,stagger:.14,ease:'none',scrollTrigger:{trigger:el,start:'top 85%',end:'bottom 55%',scrub:true}})})}catch(e){console.error(e)}}),'0px 0px 60% 0px'));init('.hero',sec=>{const stage=sec.querySelector('.hero-stage');if(!stage)return;const $=s=>sec.querySelector(s);const top=$('.hero-word--top'),bot=$('.hero-word--bottom'),la=$('.hero-line--a'),lb=$('.hero-line--b');const tr=$('.hero-bracket--tr'),bl=$('.hero-bracket--bl'),haze=$('.hero-haze');const edge=()=>parseFloat(getComputedStyle(stage).paddingLeft)||Math.max(16,innerWidth*.042);const headH=()=>(document.querySelector('.site-head')||{}).offsetHeight||0;const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec,start:'top top',end:'bottom bottom',scrub:true,invalidateOnRefresh:true}});tl.fromTo(stage,{'--open':0},{'--open':1,duration:.8,ease:'power2.inOut'},0);const sharp=$('.hero-clear canvas');if(sharp)tl.to(sharp,{scale:1,duration:.8,ease:'power2.inOut'},0);if(top)tl.to(top,{yPercent:-55,opacity:0,duration:.6,ease:'power1.in'},0);if(bot)tl.to(bot,{yPercent:55,opacity:0,duration:.6,ease:'power1.in'},0);if(la)tl.to(la,{xPercent:-30,opacity:0,duration:.35},0);if(lb)tl.to(lb,{xPercent:30,opacity:0,duration:.35},0);if(tr)tl.to(tr,{x:()=>stage.clientWidth-edge()-tr.offsetLeft-tr.offsetWidth,y:()=>headH()+8-tr.offsetTop,duration:.8,ease:'power2.inOut'},0);if(bl)tl.to(bl,{x:()=>edge()-bl.offsetLeft,y:()=>stage.clientHeight-edge()*1.6-bl.offsetTop-bl.offsetHeight,duration:.8,ease:'power2.inOut'},0);tl.to({},{duration:.25});const loops=[];if(haze)loops.push(gsap.to(haze,{xPercent:7,yPercent:-5,scale:1.1,duration:8,ease:'sine.inOut',yoyo:true,repeat:-1}));[tr,bl].forEach(b=>{const i=b&&b.firstElementChild;if(i)loops.push(gsap.to(i,{scale:1.2,duration:1.7,ease:'sine.inOut',yoyo:true,repeat:-1}))});ScrollTrigger.create({trigger:sec,start:'top bottom',end:'bottom top',onToggle:s=>loops.forEach(l=>s.isActive?l.resume():l.pause())})});later(()=>init('.files',sec=>{const rail=sec.querySelector('.files-rail');const rows=rail?[...rail.querySelectorAll('.file')]:[];if(!rows.length)return;const tr=rail.querySelector('.rail-bk--tr'),bl=rail.querySelector('.rail-bk--bl');let marks=[],railTop=0,cur=-1;const box=row=>{const ph=row.querySelector('.file-photo')||row;let x=0,y=0,el=ph;while(el&&el!==rail){x+=el.offsetLeft;y+=el.offsetTop;el=el.offsetParent}return{x,y,w:ph.offsetWidth,h:ph.offsetHeight}};const measure=()=>{railTop=rail.getBoundingClientRect().top+scrollY;marks=rows.map(r=>({top:r.offsetTop,bottom:r.offsetTop+r.offsetHeight}));if(cur>=0)place(cur,true)};const place=(i,now)=>{if(!tr||!bl)return;const b=box(rows[i]),g=10,d=now?0:.9;gsap.to(tr,{x:b.x+b.w+g-tr.offsetWidth,y:b.y-g,duration:d,ease:'expo.out',overwrite:true});gsap.to(bl,{x:b.x-g,y:b.y+b.h+g-bl.offsetHeight,duration:d,ease:'expo.out',overwrite:true})};const focus=i=>{if(i===cur)return;const first=cur<0;cur=i;rows.forEach((r,j)=>r.classList.toggle('is-focus',j===i));place(i,first)};const update=()=>{const y=scrollY+innerHeight*.5-railTop;let i=marks.findIndex(m=>y<m.bottom);if(i<0)i=marks.length-1;focus(Math.max(0,i))};rail.classList.add('is-live');ScrollTrigger.create({trigger:rail,start:'top bottom',end:'bottom top',onRefresh:()=>{measure();update()},onUpdate:update})}));later(()=>onView([...document.querySelectorAll('[data-chart]')],charts=>charts.forEach(chart=>{const fills=[...chart.querySelectorAll('.bar-fill')];gsap.to(fills,{scaleX:i=>parseFloat(fills[i].style.getPropertyValue('--v'))||0,duration:1.8,ease:'expo.out',stagger:.12})})));later(()=>init('.method',sec=>{const steps=[...sec.querySelectorAll('.step')];if(!steps.length)return;const tl=gsap.timeline({defaults:{ease:'none'},scrollTrigger:{trigger:sec.querySelector('.steps')||sec,start:'top 80%',end:'bottom 65%',scrub:true}});steps.forEach((s,i)=>{const rule=s.querySelector('.step-rule'),title=s.querySelector('.step-title'),rest=[...s.querySelectorAll('.step-when, .step-text')];const at=i*.45;if(rule)tl.fromTo(rule,{scaleX:0,transformOrigin:'0 50%'},{scaleX:1,duration:.55,ease:'power2.out'},at);if(title)tl.fromTo(title,{clipPath:'inset(0% 100% 0% 0%)'},{clipPath:'inset(0% 0% 0% 0%)',duration:.55,ease:'power2.out'},at+.12);if(rest.length)tl.fromTo(rest,{opacity:0,y:14},{opacity:1,y:0,duration:.45},at+.28)})}));later(()=>init('.field',sec=>{const stage=sec.querySelector('.field-stage'),view=sec.querySelector('.field-view'),track=sec.querySelector('.field-track');const shots=track?[...track.querySelectorAll('.shot')]:[];if(!stage||!view||!shots.length)return;sec.classList.add('is-track');let pos=[],dist=0;const size=()=>{dist=Math.max(0,track.scrollWidth-innerWidth);sec.style.height=dist+stage.offsetHeight+'px';stage.style.setProperty('--hole-h',Math.max(...shots.map(s=>s.offsetHeight))+36+'px');stage.style.setProperty('--hole-cy',view.offsetTop+view.offsetHeight/2+'px');pos=shots.map(s=>({c:s.offsetLeft+s.offsetWidth/2,w:s.offsetWidth,img:s.querySelector('canvas')}))};size();const depth=x=>{const mid=innerWidth/2;pos.forEach((p,i)=>{const d=Math.min(1,Math.abs(p.c+x-mid)/(p.w*1.1));gsap.set(shots[i],{scale:1-d*.08});if(p.img)gsap.set(p.img,{xPercent:(p.c+x-mid)/innerWidth*-8,scale:1.1})})};const tl=gsap.timeline({defaults:{ease:'power2.inOut'},scrollTrigger:{trigger:sec,start:'top top',end:()=>'+='+dist,scrub:true,invalidateOnRefresh:true,onRefreshInit:size,onUpdate:()=>depth(gsap.getProperty(track,'x')),onRefresh:()=>depth(gsap.getProperty(track,'x'))}});for(let i=1;i<shots.length;i++)tl.to(track,{x:()=>-(dist*i)/(shots.length-1),duration:1});if(shots.length<2)tl.to(track,{x:0,duration:1})}));later(()=>init('.impact',sec=>{const figs=[...sec.querySelectorAll('.figure > span')];gsap.set(figs,{yPercent:105});onView(figs,els=>gsap.to(els,{yPercent:0,duration:1.4,ease:'expo.out',stagger:.1}),'0px 0px -8% 0px')}));later(()=>init('.voices',sec=>{const cards=[...sec.querySelectorAll('.voice')];cards.slice(0,-1).forEach((card,i)=>{const next=cards[i+1];gsap.fromTo(card,{scale:1,'--veil':0},{scale:.92,'--veil':.82,ease:'none',scrollTrigger:{trigger:next,start:'top bottom',end:()=>'top '+(parseFloat(getComputedStyle(next).top)||0)+'px',scrub:true,invalidateOnRefresh:true}})})}));later(()=>init('.support',sec=>{const tiers=[...sec.querySelectorAll('.tier')];if(!tiers.length)return;const marks=[...sec.querySelectorAll('.tier--key .bracket')];gsap.set(tiers,{clipPath:'inset(48% -30px 48% -30px round 24px)'});gsap.set(marks,{opacity:0,scale:1.8});onView([sec.querySelector('.tiers')||tiers[0]],()=>{gsap.to(tiers,{clipPath:'inset(0% -30px 0% -30px round 24px)',duration:1.3,ease:'expo.inOut',stagger:.12,onComplete:()=>gsap.set(tiers,{clearProps:'clipPath'})});gsap.to(marks,{opacity:1,scale:1,duration:.9,ease:'expo.out',delay:.9,stagger:.08})},'0px 0px -15% 0px')}));later(()=>init('.tip',sec=>{const form=sec.querySelector('.tip-form');if(!form)return;const marks=[...form.querySelectorAll('.bracket')];gsap.fromTo(form,{'--veil':1},{'--veil':0,ease:'none',scrollTrigger:{trigger:form,start:'top 95%',end:'center 55%',scrub:true}});if(marks.length)gsap.fromTo(marks,{opacity:0,scale:1.8},{opacity:1,scale:1,ease:'none',scrollTrigger:{trigger:form,start:'center 70%',end:'center 55%',scrub:true}})}));later(()=>init('.site-foot',foot=>{const w=foot.querySelector('.foot-word');if(w)gsap.fromTo(w,{yPercent:40},{yPercent:0,ease:'none',scrollTrigger:{trigger:foot,start:'top bottom',end:'bottom bottom',scrub:true}})}));idle(drain);if(document.fonts&&document.fonts.status!=='loaded')document.fonts.ready.then(()=>{if(!queue.length)ScrollTrigger.refresh()})})();</script>
</body>
</html>
```

