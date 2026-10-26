INSTALANDING.AI · Corvel Hard-Tech Capital Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Corvel Hard-Tech Capital Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/corvel-hard-tech-capital-page

corvel-capital.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Corvel Hard-Tech Capital Page
  slug     corvel-hard-tech-capital-page
  prompt   https://instalanding.ai/p/corvel-hard-tech-capital-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/corvel-hard-tech-capital-page
  license  MIT. Fictional firm; every name, deal, figure and quote is invented. Replace them before shipping.

  MAP
  tokens    :root custom properties in the one <style>: --paper #ebe8e1, --paper-hi, --ink #0c1016, --red #ff5b1a,
            --mid; fonts (--f-display Inter Tight, --f-mono JetBrains Mono, --f-text Newsreader); --gut, --max,
            --head-h, --stroke, --dot (halftone cell); --ramp (the dot-gradient section edge), --rays (the sunburst)
  sections  nav, hero, services, story, portfolio, stats, process, team, reviews, gallery, pricing, faq, contact, footer
  scripts   1) the art generator: every "photo" is generated SVG from a seeded PRNG ([data-art] = wafer, die, orbit,
            candles, curve, reactor, constellation, storage, tokamak, portrait, pcb, depth, spectrum, contour),
            shown through a CSS halftone screen (.ht). 2) GSAP 3.13 + ScrollTrigger + SplitText + Lenis 1.3 (jsdelivr):
            the pinned cover that blows the masthead letters and floating cards outward, split-line headings, the
            misregistered two-plate print, the horizontal portfolio track, stamped figures, arch reveals on the team,
            the quote marquee, the halftone "develop" on the gallery, swinging price tags, the contact sunburst lines.
            Small vanilla handlers: menu, header states, Equity/Debt toggle, form, burst geometry.
  assets    none: no images, all art is inline SVG drawn by script; fonts from Google Fonts

  ADAPTING
  - html.motion is added in <head> only when motion is allowed, and removed if GSAP has not loaded after 2.5s;
    every hidden-until-animated state is scoped under .motion, so the page is complete without it.
  - Change a picture by changing its data-art / data-seed / data-vb, not by adding <img>: the halftone screen
    (filter contrast + a rotated dot grid + mix-blend) expects the generated art inside .ht-scr.
  - Big numbers and wordmarks size from --len (their character count): update style="--len:N" with the text.
  - The Equity/Debt toggle swaps .bill-once and .bill-monthly inside the section via data-bill-state.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Corvel — capital for things that are hard to build</title>
<meta name="description" content="Corvel is a hard-tech investment firm: venture equity, equipment debt and project finance for fabs, satellites, energy storage and fusion.">
<script>(function(d){if(!matchMedia('(prefers-reduced-motion: reduce)').matches){d.classList.add('motion');setTimeout(function(){if(!window.gsap)d.classList.remove('motion')},2500)}})(document.documentElement);</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400..900&family=JetBrains+Mono:wght@400..700&family=Newsreader:opsz,wght@6..72,400..700&display=swap" rel="stylesheet">
<style>@property --dr{syntax:'<percentage>';inherits:true;initial-value:34%;}
:root{--paper:#ebe8e1;--paper-hi:#f7f5f0;--ink:#0c1016;--red:#ff5b1a;--mid:#8b939e;--ink-soft:color-mix(in oklab, var(--ink) 68%, var(--paper));--line:color-mix(in oklab, var(--ink) 60%, var(--paper));--f-display:'Inter Tight', 'Helvetica Neue', Arial, sans-serif;--f-cond:'Inter Tight', 'Helvetica Neue', Arial, sans-serif;--f-mono:'JetBrains Mono', ui-monospace, Menlo, monospace;--f-text:'Newsreader', Georgia, serif;--gut:clamp(16px, 4vw, 56px);--max:1320px;--head-h:64px;--r-s:4px;--r-m:12px;--stroke:1.5px;--dot:clamp(5px, .5vw, 8px);--sec-y:clamp(88px, 11vw, 168px);--ramp-h:clamp(60px, 8vw, 120px);--ease:cubic-bezier(.2,.7,.2,1);--grain:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='240' height='240'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 -7 0 0 0 2.75'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");--ramp:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='12' height='120'%3E%3Ccircle cx='6' cy='6' r='0.5'/%3E%3Ccircle cx='0' cy='18' r='1.5'/%3E%3Ccircle cx='12' cy='18' r='1.5'/%3E%3Ccircle cx='6' cy='30' r='2.4'/%3E%3Ccircle cx='0' cy='42' r='3.4'/%3E%3Ccircle cx='12' cy='42' r='3.4'/%3E%3Ccircle cx='6' cy='54' r='4.3'/%3E%3Ccircle cx='0' cy='66' r='5.3'/%3E%3Ccircle cx='12' cy='66' r='5.3'/%3E%3Ccircle cx='6' cy='78' r='6.2'/%3E%3Ccircle cx='0' cy='90' r='7.2'/%3E%3Ccircle cx='12' cy='90' r='7.2'/%3E%3Ccircle cx='6' cy='102' r='8.1'/%3E%3Ccircle cx='0' cy='114' r='9'/%3E%3Ccircle cx='12' cy='114' r='9'/%3E%3C/svg%3E");--rays:repeating-conic-gradient(var(--red) 0deg .7deg, transparent .7deg 7.5deg), repeating-conic-gradient(color-mix(in oklab, var(--paper) 14%, var(--ink)) 0deg .25deg, var(--ink) .25deg 1.5deg);}
*,*::before,*::after{box-sizing:border-box}html{-webkit-text-size-adjust:100%;text-size-adjust:100%}html.lenis,html.lenis body{height:auto}.lenis.lenis-smooth{scroll-behavior:auto!important}body{margin:0;background:var(--paper);color:var(--ink);font:400 18px/1.55 var(--f-text);font-optical-sizing:auto;-webkit-font-smoothing:antialiased;overflow-x:clip}img{display:block;max-width:100%}a{color:inherit}button{font:inherit;color:inherit}h1,h2,h3,h4,p,ul,ol,figure,blockquote,dl,dd{margin:0}ul,ol{padding:0;list-style:none}main>*{position:relative;overflow-x:clip}.wrap{width:min(100% - 2*var(--gut), var(--max));margin-inline:auto}.sr{position:absolute;width:1px;height:1px;overflow:hidden;clip-path:inset(50%);white-space:nowrap}:focus-visible{outline:2px solid var(--red);outline-offset:3px}
.h2{font:800 clamp(40px, 6.2vw, 92px)/.94 var(--f-display);letter-spacing:-.04em;text-wrap:balance}.h3{font:700 clamp(26px, 2.6vw, 38px)/1.02 var(--f-display);letter-spacing:-.03em}.lede{font:400 clamp(19px, 1.6vw, 23px)/1.45 var(--f-text);max-width:34em}.meta{font:500 13px/1.3 var(--f-mono);color:var(--ink-soft);text-transform:uppercase;letter-spacing:.06em}
.btn{display:inline-flex;align-items:stretch;text-decoration:none;white-space:nowrap;font:600 15px/1 var(--f-cond);letter-spacing:-.005em;border:var(--stroke) solid var(--ink);background:var(--ink);color:var(--paper);box-shadow:4px 4px 0 var(--btn-shadow, var(--red));transition:transform .28s var(--ease), box-shadow .28s var(--ease);cursor:pointer}.btn>span{display:flex;align-items:center;padding:.85em 1.05em}.btn .btn-v{background:var(--paper-hi);color:var(--ink);font:500 12px/1 var(--f-mono);text-transform:uppercase;letter-spacing:.04em}.btn--light{background:var(--paper-hi);color:var(--ink)}@media (hover:hover){.btn:hover{transform:translate(4px,4px);box-shadow:0 0 0 var(--btn-shadow, var(--red))}}
.tlink{--dr:30%;text-decoration:none;padding-bottom:5px;background:radial-gradient(circle, currentColor var(--dr), transparent calc(var(--dr) + 6%)) 0 100%/6px 6px repeat-x;transition:--dr .35s var(--ease)}@media (hover:hover){.tlink:hover{--dr:78%}}
.ibtn{position:relative;display:inline-grid;place-items:center;width:46px;height:46px;border-radius:50%;border:var(--stroke) solid currentColor;background:transparent;cursor:pointer;isolation:isolate;overflow:hidden;padding:0}.ibtn::before{content:'';position:absolute;inset:-30%;z-index:-1;background:repeating-conic-gradient(var(--red) 0 12deg, transparent 12deg 30deg);opacity:0;transform:rotate(-40deg) scale(.5);transition:opacity .3s, transform .5s var(--ease)}@media (hover:hover){.ibtn:hover::before{opacity:1;transform:none}}.ibtn svg{width:20px;height:20px}
.chip{display:inline-flex;align-items:stretch;font:500 12px/1 var(--f-mono);letter-spacing:.02em;border:var(--stroke) solid var(--ink);background:var(--paper-hi);color:var(--ink);white-space:nowrap;max-width:100%}.chip>span{display:flex;align-items:center;padding:.6em .75em}.chip .chip-k{background:var(--ink);color:var(--paper-hi);text-transform:uppercase;letter-spacing:.06em}.chip .chip-v{overflow:hidden;text-overflow:ellipsis}
.art{position:absolute;inset:0}.art svg{display:block;width:100%;height:100%}.a-ink{fill:var(--ink)}.a-red{fill:var(--red)}.a-pap{fill:var(--paper-hi)}.a-mid{fill:var(--mid)}.s-ink{stroke:var(--ink)}.s-red{stroke:var(--red)}.s-pap{stroke:var(--paper-hi)}
.ht{position:relative;overflow:hidden;background:var(--paper);isolation:isolate}.ht-scr{position:absolute;inset:0;overflow:hidden;background:#fff;filter:contrast(20);mix-blend-mode:multiply}.ht-scr .art{filter:grayscale(1) contrast(var(--ht-c, .62)) brightness(var(--ht-b, 1.3))}.ht-scr::after{content:'';position:absolute;inset:-50%;background:radial-gradient(closest-side, color-mix(in srgb, #000 60%, #fff), #fff) 0 0/var(--dot) var(--dot);mix-blend-mode:multiply;transform:rotate(var(--ht-a, 45deg))}.ht::after{content:'';position:absolute;inset:0;background:var(--ht-ink, var(--ink));mix-blend-mode:lighten;pointer-events:none}.ht--red{--ht-ink:var(--red)}.ph{position:relative;overflow:hidden;background:var(--ink)}
.ramp-top::before{content:'';position:absolute;left:0;right:0;top:calc(1px - var(--ramp-h));height:var(--ramp-h);background:var(--ramp-c, var(--ink));-webkit-mask:var(--ramp) 0 0/calc(var(--ramp-h) / 10) var(--ramp-h) repeat-x;mask:var(--ramp) 0 0/calc(var(--ramp-h) / 10) var(--ramp-h) repeat-x;pointer-events:none;z-index:1}
.site-head{position:fixed;inset:0 0 auto;z-index:60;height:var(--head-h);display:flex;align-items:center;gap:24px;padding:0 var(--gut);color:var(--ink);transition:transform .45s var(--ease), background-color .3s, color .3s}.site-head.is-solid{background:var(--paper);box-shadow:0 var(--stroke) 0 color-mix(in oklab, var(--ink) 25%, transparent)}.site-head.on-dark{background:var(--ink);color:var(--paper);box-shadow:none;--btn-shadow:var(--red)}.site-head.on-dark .btn{border-color:var(--paper-hi)}.site-head.is-hidden{transform:translateY(-100%)}.brand{font:900 28px/1 var(--f-display);letter-spacing:-.05em;text-decoration:none;white-space:nowrap;transition:opacity .3s, transform .3s var(--ease)}.brand i{font-style:normal;color:var(--red)}.site-head.at-cover .brand{opacity:0;transform:translateY(-8px);pointer-events:none}.nav{margin-left:auto;display:flex;gap:clamp(16px, 2.2vw, 32px)}.nav a{font:500 15px/1 var(--f-cond);white-space:nowrap}.head-cta{flex:none}.menu-btn{display:none}
.menu{position:fixed;inset:0;z-index:70;background:var(--paper);color:var(--ink);padding:calc(var(--head-h) + 24px) var(--gut) 32px;display:flex;flex-direction:column;gap:28px;overflow-y:auto;visibility:hidden;clip-path:circle(0 at calc(100% - 40px) 32px);transition:clip-path .6s var(--ease), visibility 0s .6s}.menu.is-open{visibility:visible;clip-path:circle(150% at calc(100% - 40px) 32px);transition:clip-path .6s var(--ease)}.menu-close{position:absolute;top:9px;right:var(--gut)}.menu ul{display:flex;flex-direction:column}.menu li a{display:flex;justify-content:space-between;align-items:center;gap:16px;padding:14px 0;border-bottom:var(--stroke) solid var(--red);text-decoration:none;font:800 clamp(34px, 9vw, 56px)/1 var(--f-display);letter-spacing:-.04em}.menu li a svg{flex:none;width:22px;height:22px;color:var(--red)}.menu .btn{align-self:flex-start}@media (max-width:900px){.nav,.head-cta{display:none}.menu-btn{display:inline-grid;margin-left:auto}}
.cover{background:var(--paper)}.motion .cover-pin{height:calc(100svh + 90vh)}.cover-stage{position:sticky;top:0;height:100svh;min-height:620px;overflow:hidden;--mast-w:min(60vw, 820px);--arch-top:calc(var(--head-h) + min(240px, 29svh) * .8 + 58px)}.cover-head{position:absolute;z-index:3;top:calc(var(--head-h) - 6px);left:50%;width:var(--mast-w);margin-left:calc(var(--mast-w) / -2)}.cover-title{display:block;text-align:center;font-weight:inherit}.mast{display:block;font:900 min(240px, 29svh, calc(var(--mast-w) / (var(--len) * .55)))/.8 var(--f-display);letter-spacing:-.06em;color:var(--ink);white-space:nowrap}.mast-ch{display:inline-block}.cover-tag{display:block;max-width:54%;margin-top:.7em;text-align:left;font:500 clamp(12px, 1.05vw, 15px)/1.3 var(--f-mono);text-transform:uppercase;letter-spacing:.04em;color:var(--red)}.cover-mail{position:absolute;right:0;bottom:0;max-width:44%;text-align:right;font:500 clamp(12px, 1.05vw, 15px)/1.3 var(--f-mono);color:var(--red);overflow-wrap:anywhere}
.cover-art{position:absolute;z-index:2;left:50%;bottom:64px;height:calc(100% - var(--arch-top) - 64px);width:min(44vw, 600px, (100svh - var(--arch-top) - 64px) * 1.25);transform:translateX(-50%)}.cover-lines{position:absolute;left:50%;top:60%;width:3000px;height:3000px;margin:-1500px 0 0 -1500px;pointer-events:none;overflow:visible;z-index:-1}.cover-lines line{stroke:var(--ink);stroke-width:1;stroke-opacity:.7;vector-effect:non-scaling-stroke}.cover-lines .dash{stroke-dasharray:3 7}.arch-line{position:absolute;inset:-14px -14px -10px;border:var(--stroke) solid var(--ink);border-radius:999px 999px 0 0;background:var(--paper)}.arch{position:absolute;inset:0;overflow:hidden;border-radius:999px 999px 0 0;background:var(--ink);isolation:isolate}.rays-turn{position:absolute;left:50%;top:60%;width:320%;aspect-ratio:1;margin:-160% 0 0 -160%}.rays{position:absolute;inset:0;border-radius:50%;background:var(--rays)}.arch-dots{position:absolute;inset:0;background:radial-gradient(circle, var(--ink) 0 38%, transparent 42%) 0 0/9px 9px;-webkit-mask:linear-gradient(to top, #000 8%, transparent 58%);mask:linear-gradient(to top, #000 8%, transparent 58%)}.arch-grain{position:absolute;inset:0;background:var(--paper);-webkit-mask:var(--grain);mask:var(--grain);opacity:.35}
.ray-word{position:absolute;z-index:3;padding:.3em .55em;background:var(--ink);color:var(--red);font:600 clamp(11px, 1.2vw, 16px)/1 var(--f-mono);letter-spacing:.1em;text-transform:uppercase;white-space:nowrap;rotate:var(--rot);box-shadow:0 0 0 1px color-mix(in oklab, var(--red) 50%, var(--ink))}.ray-word--a{left:1%;top:50%;--rot:-14deg}.ray-word--b{right:-3%;top:33%;--rot:12deg}
.print{position:absolute;z-index:4;left:50%;top:21%;width:54%;margin-left:-27%;transform:rotate(-5deg);background:var(--paper-hi);padding:5% 5% 0;box-shadow:0 0 0 var(--stroke) var(--ink), 9px 9px 0 color-mix(in oklab, var(--ink) 85%, #000)}.print .ht{aspect-ratio:1;--dot:5px;--ht-c:.75;--ht-b:1.15}.print figcaption{margin:6% 0;padding:.6em .4em;background:var(--ink);color:var(--red);text-align:center;font:600 clamp(11px, 1.25vw, 17px)/1 var(--f-mono);text-transform:uppercase;letter-spacing:.12em;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.cv-f{position:absolute;z-index:3;background:var(--paper-hi);padding:4%;box-shadow:0 0 0 var(--stroke) var(--ink), 6px 6px 0 var(--red)}.cv-f .ph{width:100%;height:100%}.cv-f--a{left:-27%;top:2%;width:30%;aspect-ratio:.86;rotate:-9deg;padding-bottom:9%}.cv-f--b{right:-22%;top:6%;width:25%;aspect-ratio:1;border-radius:50%;padding:5%}.cv-f--b .ph{border-radius:50%}.cv-f--c{left:-19%;top:66%;width:25%;aspect-ratio:.72;border-radius:22px;rotate:9deg;padding:5% 5% 12%}.cv-f--c .ph{border-radius:12px}.cv-f--d{right:-26%;top:57%;width:34%;aspect-ratio:1.3;rotate:-6deg}
.bubble{position:absolute;z-index:4;left:27%;top:-7%;display:flex;align-items:center;gap:.6em;padding:.7em .85em;background:var(--paper-hi);border:var(--stroke) solid var(--ink);border-radius:10px;font:600 clamp(12px, 1vw, 15px)/1.15 var(--f-cond);max-width:48%;box-shadow:5px 5px 0 var(--ink)}.bubble::after{content:'';position:absolute;left:22%;bottom:-9px;width:14px;height:14px;background:var(--paper-hi);border:solid var(--ink);border-width:0 var(--stroke) var(--stroke) 0;transform:rotate(45deg)}.bubble svg{flex:none;width:1.3em;height:1.3em;color:var(--red)}
.dandelion{position:absolute;z-index:1;top:calc(var(--head-h) - 10px);right:calc(var(--gut) * .6);width:min(22vw, 290px);color:var(--ink);pointer-events:none}.dandelion--l{right:auto;left:calc(var(--gut) * .6);transform:scaleX(-1)}.sym-core{fill:var(--paper)}.sym-node{fill:var(--red)}
.cover-chips{position:absolute;z-index:5;left:var(--gut);right:var(--gut);bottom:14px;display:flex;justify-content:space-between;align-items:flex-end;gap:12px;pointer-events:none}.cover-chips>*{pointer-events:auto}.cover-aside{position:absolute;z-index:6;top:calc(var(--head-h) + 130px);left:calc(var(--gut) - 12px);width:min(17vw, 232px);padding:2px 12px 12px;background:var(--paper)}.cover-no{position:absolute;z-index:6;top:calc(var(--head-h) + 200px);right:calc(var(--gut) - 12px);width:min(15vw, 212px);padding:8px 12px;background:var(--paper);text-align:left;color:var(--red)}.cover-no b{display:block;font:900 clamp(56px, 6vw, 84px)/.85 var(--f-display);letter-spacing:-.05em}.cover-no span{display:block;margin-top:.5em;font:500 14px/1.3 var(--f-cond);color:var(--ink)}
.toc li{border-bottom:var(--stroke) solid color-mix(in oklab, var(--red) 70%, var(--paper));padding:10px 0 7px}.toc li+li{margin-top:12px}.toc a{display:grid;grid-template-columns:1fr auto;gap:2px 10px;text-decoration:none}.toc b{font:600 16px/1.15 var(--f-cond);letter-spacing:-.01em}.toc svg{width:10px;height:16px;color:var(--red);align-self:center;transition:transform .3s var(--ease)}.toc small{grid-column:1/-1;margin-top:8px;font:500 11px/1.2 var(--f-mono);text-transform:uppercase;letter-spacing:.08em;color:var(--ink-soft)}@media (hover:hover){.toc a:hover svg{transform:translateX(5px)}}
@media (max-width:1180px){.cover-aside,.cover-no{position:static;width:auto;background:none;padding:0}.cover-extra{display:grid;grid-template-columns:1.4fr 1fr;gap:28px;padding:40px 0 8px}.cover-no{align-self:start}.dandelion--l{display:none}}@media (min-width:1181px){.cover-extra{display:contents}}
@media (max-width:760px){.cover-stage{--mast-w:calc(100vw - 2 * var(--gut));--arch-top:calc(var(--head-h) + min(240px, 29svh, (100vw - 2 * var(--gut)) / 3.3) * .8 + 50px)}.motion .cover-pin{height:calc(100svh + 60vh)}.cover-head{top:calc(var(--head-h) - 2px)}.cover-tag,.cover-mail{font-size:11px}.cover-art{width:min(80vw, (100svh - var(--arch-top) - 64px) * .9)}.cover-extra{grid-template-columns:1fr;gap:24px}.dandelion{display:none}.ray-word--a{left:-8%}.ray-word--b{right:-8%}.bubble{left:8%;top:-1%;max-width:62%}.cv-f--a{top:9%}.cv-f--c{top:64%}.ray-word--a{top:52%}.cv-f--a{left:-19%;width:32%}.cv-f--b{right:-15%;width:27%}.cv-f--c{left:-14%;width:27%}.cv-f--d{right:-17%;width:36%}.chip{font-size:11px}.cover-chips{flex-direction:column;align-items:flex-start;gap:6px;bottom:10px}.cover-chips .btn{align-self:flex-end;font-size:13px}}
.contents{padding:var(--sec-y) 0}.contents-grid{display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 7fr);gap:clamp(32px, 6vw, 96px)}.contents-head{position:sticky;top:calc(var(--head-h) + 32px);align-self:start}.contents-head .lede{margin-top:28px}.contents-head .dandelion-s{display:block;width:150px;margin:0 0 18px -8px;color:var(--ink)}
.svc{position:relative;display:grid;grid-template-columns:minmax(0,1fr) auto;gap:10px 24px;padding:26px 0 22px}.svc::after{content:'';position:absolute;left:0;right:0;bottom:0;height:1.5px;background:var(--red);transform-origin:left}.svc h3{font:700 clamp(26px, 2.7vw, 38px)/1.02 var(--f-display);letter-spacing:-.035em}.svc p{grid-column:1;max-width:36em;color:color-mix(in oklab, var(--ink) 88%, var(--paper))}.svc .svc-price{grid-column:2;grid-row:1;align-self:start;text-align:right;font:500 13px/1.2 var(--f-mono);text-transform:uppercase;letter-spacing:.04em;color:var(--red);white-space:nowrap;padding-top:8px}.svc .svc-list{grid-column:1/-1;display:flex;flex-wrap:wrap;gap:6px 18px;font:500 12px/1.3 var(--f-mono);text-transform:uppercase;letter-spacing:.05em;color:var(--ink-soft)}.svc .svc-list li{display:flex;align-items:center;gap:8px}.svc .svc-list li::before{content:'';width:6px;height:6px;background:var(--red)}@media (max-width:860px){.contents-grid{grid-template-columns:1fr}.contents-head{position:static}}
.feature{padding:var(--sec-y) 0;background:var(--paper-hi)}.feature-grid{display:grid;grid-template-columns:minmax(0, 6fr) minmax(0, 6fr);gap:clamp(32px, 5vw, 80px);align-items:start}.reg{position:relative;aspect-ratio:4/5;margin:18px}.reg-stack{position:absolute;inset:0;overflow:hidden;background:var(--paper-hi);isolation:isolate;box-shadow:0 0 0 var(--stroke) var(--ink)}.reg-plate{position:absolute;inset:0;mix-blend-mode:multiply;will-change:transform}.reg-plate.ht{background:var(--paper-hi)}.reg-plate--r{background:#fff}.reg-plate--r.ht{background:#fff}.reg{--ht-b:1.2;--ht-c:.7}.reg-plate--r .ht-scr .art{filter:grayscale(1) invert(1) contrast(.45) brightness(1.55)}.reg-plate--r{--ht-a:15deg;--dot:clamp(7px, .75vw, 11px)}.reg-mark{position:absolute;width:44px;height:44px;color:var(--ink);will-change:transform}.reg-mark circle,.reg-mark line{fill:none;stroke:currentColor;stroke-width:1.3}.reg-mark--r{color:var(--red);mix-blend-mode:multiply}.reg-mark.tl{left:-34px;top:-34px}.reg-mark.br{right:-34px;bottom:-34px}.reg figcaption{position:absolute;left:0;bottom:-16px;z-index:2}
.feature-text{padding-top:clamp(0px, 3vw, 40px)}.reg-title{--mx:0em;--my:0em;text-shadow:var(--mx) var(--my) 0 var(--red)}.motion .reg-title{--mx:.06em;--my:-.045em}.feature-text .lede{margin-top:32px}.cols{margin-top:32px;columns:2;column-gap:32px;font-size:17px}.cols p+p{margin-top:1em}.dropcap::first-letter{float:left;font:900 4.4em/.78 var(--f-display);color:var(--red);margin:.04em .08em 0 0}.sign{margin-top:28px;display:flex;align-items:center;gap:14px;font:500 13px/1.3 var(--f-mono);text-transform:uppercase;letter-spacing:.05em}.sign::before{content:'';width:48px;height:2px;background:var(--red)}@media (max-width:860px){.feature-grid{grid-template-columns:1fr}.reg{margin:14px 14px 30px}.cols{columns:1}}
.work{background:var(--ink);color:var(--paper);padding-top:var(--sec-y)}.work-head{display:grid;grid-template-columns:minmax(0, 7fr) minmax(0, 5fr);gap:32px;align-items:end;margin-bottom:clamp(40px, 6vw, 72px)}.work-head .lede{color:color-mix(in oklab, var(--paper) 82%, var(--ink))}.work-track{display:flex;flex-direction:column;gap:40px;padding:0 var(--gut) var(--sec-y)}.spread{display:grid;grid-template-columns:minmax(0, 1.1fr) minmax(0, 1fr);background:var(--paper-hi);color:var(--ink);box-shadow:10px 10px 0 var(--red)}.spread-ph{position:relative;min-height:300px;margin:0;border-right:var(--stroke) solid var(--ink)}.spread-ph .tag-k{position:absolute;left:14px;top:14px;z-index:2}.spread-txt{display:flex;flex-direction:column;gap:16px;padding:clamp(22px, 3.2vw, 48px)}.spread-year{display:flex;align-items:flex-end;gap:14px;container-type:inline-size}.spread-year b{flex:none;font:900 min(clamp(64px, 8.4vw, 136px), 64cqi / (var(--len) * .6))/.8 var(--f-display);letter-spacing:-.05em;color:var(--red)}.spread-year span{font:500 12px/1.3 var(--f-mono);text-transform:uppercase;letter-spacing:.05em;color:var(--ink-soft);padding-bottom:4px}.spread-name{font:800 clamp(34px, 4.2vw, 66px)/.94 var(--f-display);letter-spacing:-.045em}.spread-txt p:not([class]){font-size:clamp(16px, 1.3vw, 18.5px);max-width:30em}.spread-result{margin-top:auto;padding-top:14px;border-top:1.5px solid var(--red);font:600 17px/1.3 var(--f-cond);letter-spacing:-.01em}
.motion .work-pin{height:calc(100svh + var(--dist, 0px))}.motion .work-stage{position:sticky;top:0;height:100svh;overflow:hidden;display:flex;align-items:center;padding-top:calc(var(--head-h) * .5)}.motion .work-track{flex-direction:row;align-items:stretch;gap:clamp(24px, 4vw, 64px);width:max-content;padding:0 var(--gut);will-change:transform}.motion .spread{width:min(1040px, 80vw);min-height:min(68svh, 580px)}.motion .spread{rotate:var(--tilt, 0deg)}@media (max-width:760px){.work-head{grid-template-columns:1fr}.spread{grid-template-columns:1fr;grid-template-rows:auto 1fr}.spread-ph{min-height:0;aspect-ratio:16/10;border-right:0;border-bottom:var(--stroke) solid var(--ink)}.motion .spread{width:84vw;min-height:0}.motion .work-stage{padding-top:var(--head-h)}.spread-txt p:not([class]){font-size:15.5px;line-height:1.45}}
.figures{background:var(--red);color:var(--paper-hi);padding:var(--sec-y) 0;--ramp-c:var(--red)}.fig-rays{position:absolute;inset:0;overflow:hidden;pointer-events:none}.fig-rays div{position:absolute;left:50%;top:100%;width:max(220vw, 1800px);aspect-ratio:1;margin:calc(max(220vw, 1800px) / -2) 0 0 calc(max(220vw, 1800px) / -2);border-radius:50%;background:repeating-conic-gradient(color-mix(in oklab, var(--red) 88%, var(--ink)) 0 .6deg, transparent .6deg 6deg)}.figures .wrap{position:relative}.fig-title{max-width:12em}.fig-list{display:grid;grid-template-columns:repeat(4, minmax(0, 1fr));gap:clamp(20px, 3vw, 44px);margin-top:clamp(48px, 7vw, 96px)}.fig{container-type:inline-size;padding-top:18px;border-top:1.5px solid var(--paper-hi)}.fig b{display:block;font:900 min(clamp(72px, 9vw, 136px), 100cqi / (var(--len) * .6))/.82 var(--f-display);letter-spacing:-.055em;color:var(--ink)}.fig span{display:block;margin-top:16px;font:500 16px/1.35 var(--f-cond);max-width:17em}.motion [data-stamp] b{opacity:0}@media (max-width:860px){.fig-list{grid-template-columns:repeat(2, minmax(0, 1fr))}}
.process{padding:var(--sec-y) 0}.process-grid{display:grid;grid-template-columns:minmax(0, 5fr) minmax(0, 7fr);gap:clamp(32px, 6vw, 96px)}.process-head{position:sticky;top:calc(var(--head-h) + 32px);align-self:start;display:flex;flex-direction:column;align-items:flex-start;gap:28px}.proofs{display:flex;flex-direction:column;gap:clamp(48px, 10vh, 110px)}.proof{position:sticky;top:calc(var(--head-h) + 28px + var(--i, 0) * 14px);background:var(--paper-hi);border:var(--stroke) solid var(--ink);padding:clamp(22px, 3vw, 40px);box-shadow:8px 8px 0 var(--ink);rotate:var(--tilt, 0deg)}.proof::before,.proof::after{content:'';position:absolute;width:18px;height:18px;border:solid var(--ink);pointer-events:none}.proof::before{left:-12px;top:-12px;border-width:0 var(--stroke) var(--stroke) 0}.proof::after{right:-12px;bottom:-12px;border-width:var(--stroke) 0 0 var(--stroke)}.proof-bar{display:block;width:min(100%, 216px);height:12px;margin-bottom:24px;background:linear-gradient(90deg, var(--ink) 0 16.6%, color-mix(in oklab, var(--ink) 55%, var(--paper-hi)) 16.6% 33.3%, var(--red) 33.3% 50%, color-mix(in oklab, var(--red) 50%, var(--paper-hi)) 50% 66.6%, color-mix(in oklab, var(--ink) 25%, var(--paper-hi)) 66.6% 83.3%, var(--paper) 83.3%);box-shadow:0 0 0 1px var(--ink)}.proof .meta{color:var(--red);font-weight:600}.proof .h3{margin:8px 0 14px}@media (max-width:860px){.process-grid{grid-template-columns:1fr}.process-head{position:static}.proof{top:calc(var(--head-h) + 16px + var(--i, 0) * 10px)}}
.team{padding:var(--sec-y) 0}.team-head,.voices-head,.gallery-head{display:grid;grid-template-columns:minmax(0, 7fr) minmax(0, 5fr);gap:32px;align-items:end;margin-bottom:clamp(40px, 6vw, 80px)}.people{display:grid;grid-template-columns:repeat(auto-fit, minmax(min(100%, 230px), 1fr));gap:clamp(28px, 3vw, 44px) clamp(20px, 2.4vw, 36px)}.person{display:flex;flex-direction:column;align-items:flex-start;gap:12px}.person-arch{width:100%;aspect-ratio:3/4;border-radius:999px 999px 0 0;box-shadow:0 0 0 var(--stroke) var(--ink);outline:var(--stroke) solid var(--ink);outline-offset:8px;margin-bottom:18px;--ht-c:.7;--ht-b:1.2}.person-name{font:800 clamp(26px, 2.3vw, 34px)/1 var(--f-display);letter-spacing:-.04em;margin-top:4px}.person-note{font-size:16px;line-height:1.5;color:color-mix(in oklab, var(--ink) 85%, var(--paper))}.motion [data-people]:not(.is-in) .person-arch{clip-path:inset(100% 0 0 0)}@media (max-width:760px){.people{grid-template-columns:repeat(2, minmax(0, 1fr))}.person-note{font-size:14.5px}}@media (max-width:760px){.team-head,.voices-head,.gallery-head{grid-template-columns:1fr}}
.voices{background:var(--ink);color:var(--paper);padding:var(--sec-y) 0}.voices .lede{color:color-mix(in oklab, var(--paper) 82%, var(--ink))}.marquee{padding:12px 0 28px}.mq-track{display:flex;flex-wrap:wrap;gap:28px;padding:0 var(--gut)}.quote{position:relative;flex:1 1 300px;max-width:440px;display:flex;flex-direction:column;gap:16px;padding:26px 26px 22px;background:var(--paper-hi);color:var(--ink);border-radius:var(--r-m);box-shadow:7px 7px 0 var(--red);margin-bottom:22px}.quote::after{content:'';position:absolute;left:34px;bottom:-11px;width:20px;height:20px;background:var(--paper-hi);transform:rotate(45deg)}.quote svg{width:26px;height:26px;color:var(--red)}.quote blockquote{font:500 19px/1.4 var(--f-text)}.quote-by{display:flex;flex-wrap:wrap;gap:4px 10px;align-items:baseline;margin-top:auto;font:600 15px/1.2 var(--f-cond)}.quote-by span{font:500 11px/1.2 var(--f-mono);text-transform:uppercase;letter-spacing:.05em;color:var(--ink-soft)}.motion .marquee{overflow:hidden}.motion .mq-track{flex-wrap:nowrap;width:max-content;animation:mq var(--mq-dur, 60s) linear infinite}.motion .quote{flex:none;width:min(420px, 80vw);max-width:none}.motion .marquee:hover .mq-track,.motion .marquee:focus-within .mq-track,.motion .marquee.is-off .mq-track{animation-play-state:paused}@keyframes mq{to{transform:translateX(-50%)}}
@property --mr{syntax:'<percentage>';inherits:false;initial-value:80%;}.gallery{padding:var(--sec-y) 0}.collage{display:grid;grid-template-columns:repeat(12, minmax(0, 1fr));gap:clamp(14px, 1.8vw, 24px)}.g{display:flex;flex-direction:column;gap:10px;min-width:0}.g>div{flex:1;min-height:0;box-shadow:0 0 0 var(--stroke) var(--ink)}.g figcaption{font:500 11.5px/1.3 var(--f-mono);text-transform:uppercase;letter-spacing:.05em;color:var(--ink-soft)}.g--a{grid-column:1/8;grid-row:1/3}.g--a>div{min-height:clamp(300px, 40vw, 560px)}.g--b{grid-column:8/13;grid-row:1}.g--c{grid-column:8/10;grid-row:2}.g--d{grid-column:10/13;grid-row:2}.g--e{grid-column:1/5;grid-row:3}.g--f{grid-column:5/13;grid-row:3}.g--b>div,.g--c>div,.g--d>div{min-height:clamp(150px, 16vw, 230px)}.g--e>div,.g--f>div{min-height:clamp(220px, 26vw, 380px)}.motion [data-develop] .g>div{--mr:0%;-webkit-mask:radial-gradient(circle, #000 var(--mr), transparent calc(var(--mr) + 1.5%)) 0 0/16px 16px;mask:radial-gradient(circle, #000 var(--mr), transparent calc(var(--mr) + 1.5%)) 0 0/16px 16px;transition:--mr 1.3s cubic-bezier(.5,0,.3,1)}.motion [data-develop] .g.is-in>div{--mr:80%}.motion [data-develop] .g.is-done>div{-webkit-mask:none;mask:none}@media (max-width:760px){.collage{grid-template-columns:repeat(2, minmax(0, 1fr))}.g--a{grid-column:1/3;grid-row:auto}.g--a>div{min-height:260px}.g--b,.g--f{grid-column:1/3;grid-row:auto}.g--c,.g--d,.g--e{grid-column:auto;grid-row:auto}.g--e{grid-column:1/3}}
.pricing{background:var(--ink);color:var(--paper);padding:var(--sec-y) 0}.pricing-head{display:flex;flex-wrap:wrap;justify-content:space-between;align-items:flex-end;gap:28px;margin-bottom:clamp(40px, 6vw, 72px)}.pricing-head .h2{max-width:11em}.bill{display:inline-flex;flex-wrap:wrap;gap:4px;padding:4px;border:var(--stroke) solid color-mix(in oklab, var(--paper) 40%, transparent);border-radius:999px}.bill-opt{border:0;background:transparent;color:var(--paper);padding:.8em 1.3em;border-radius:999px;font:500 13px/1 var(--f-mono);text-transform:uppercase;letter-spacing:.06em;white-space:nowrap;cursor:pointer;transition:background-color .25s, color .25s}.bill-opt[aria-pressed="true"]{background:var(--red);color:var(--ink)}@media (hover:hover){.bill-opt[aria-pressed="false"]:hover{color:var(--red)}}
.tags{display:grid;grid-template-columns:repeat(auto-fit, minmax(min(100%, 280px), 1fr));gap:clamp(20px, 2.6vw, 36px);align-items:start}.tag{position:relative;display:flex;flex-direction:column;align-items:flex-start;gap:16px;padding:40px clamp(22px, 2.4vw, 34px) 30px;background:var(--paper-hi);color:var(--ink);border-radius:var(--r-m);box-shadow:8px 8px 0 var(--red);--btn-shadow:var(--red)}.tag::before{content:'';position:absolute;top:18px;right:20px;width:16px;height:16px;border-radius:50%;background:var(--ink);box-shadow:0 0 0 3px color-mix(in oklab, var(--ink) 20%, var(--paper-hi))}.tag::after{content:'';position:absolute;top:-40px;right:27px;width:var(--stroke);height:66px;background:var(--paper);rotate:14deg;transform-origin:bottom}.tag--hot{background:var(--red);color:var(--ink);box-shadow:8px 8px 0 var(--paper-hi);--btn-shadow:var(--paper-hi)}.tag--hot::before{box-shadow:0 0 0 3px color-mix(in oklab, var(--paper-hi) 45%, var(--red))}.tag-name{font:800 clamp(34px, 3.2vw, 46px)/.95 var(--f-display);letter-spacing:-.045em;padding-right:28px}.tag-for{font-size:16.5px;line-height:1.45;min-height:3em}.tag-price{width:100%;container-type:inline-size;padding:14px 0;border-block:var(--stroke) solid currentColor}.tag-price b{display:block;font:900 min(clamp(48px, 4.8vw, 72px), 100cqi / (var(--len) * .6))/.9 var(--f-display);letter-spacing:-.05em;color:var(--red);white-space:nowrap}.tag--hot .tag-price b{color:var(--ink)}.tag-price span{display:block;margin-top:8px;font:500 12px/1.2 var(--f-mono);text-transform:uppercase;letter-spacing:.05em}.bill-monthly{display:none!important}[data-bill-state="monthly"] .bill-monthly{display:block!important}[data-bill-state="monthly"] .bill-once{display:none!important}.tag-list{display:flex;flex-direction:column;gap:8px;font:500 15px/1.35 var(--f-cond);margin-bottom:6px}.tag-list li{display:flex;gap:10px;align-items:baseline}.tag-list li::before{content:'';flex:none;width:7px;height:7px;background:currentColor;translate:0 -2px}.tag .btn{margin-top:auto}.tag--hot .btn{border-color:var(--ink)}.pricing-note{margin-top:40px;max-width:44em;font-size:15px;color:color-mix(in oklab, var(--paper) 72%, var(--ink))}.motion [data-tags] .tag{opacity:0}
.faq{padding:var(--sec-y) 0}.faq-head{display:grid;grid-template-columns:minmax(0, 7fr) minmax(0, 5fr);gap:32px;align-items:end;margin-bottom:clamp(32px, 5vw, 64px)}.qa{position:relative}.qa::after{content:'';position:absolute;left:0;right:0;bottom:0;height:1.5px;background:var(--red);transform-origin:left}.qa summary{display:flex;justify-content:space-between;align-items:center;gap:20px;padding:24px 0;cursor:pointer;list-style:none;font:700 clamp(22px, 2.5vw, 34px)/1.1 var(--f-display);letter-spacing:-.035em}.qa summary::-webkit-details-marker{display:none}.qa summary svg{flex:none;width:44px;height:44px;padding:12px;border:var(--stroke) solid var(--ink);border-radius:50%;color:var(--red);transition:rotate .35s var(--ease), background-color .25s}.qa[open] summary svg{rotate:180deg;background:var(--ink)}@media (hover:hover){.qa summary:hover span{color:var(--red)}}.qa-a{padding:0 64px 28px 0;max-width:48em}.qa[open] .qa-a{animation:qa-in .45s var(--ease)}@keyframes qa-in{from{opacity:0;translate:0 -8px}}@media (max-width:760px){.faq-head{grid-template-columns:1fr}.qa-a{padding-right:0}}
.contact{padding:var(--sec-y) 0 calc(var(--sec-y) * .9)}.contact-burst{position:absolute;inset:0;width:100%;height:100%;pointer-events:none;color:var(--ink);overflow:hidden}.contact-burst line{stroke:currentColor;stroke-width:1;stroke-opacity:.75;fill:none}.contact-burst .dash{stroke-dasharray:.018 .012}.contact-burst circle{fill:var(--paper);stroke:currentColor;stroke-width:1.3}.contact-sun{position:absolute;left:50%;bottom:0;width:min(1320px, 104vw);height:56%;margin-left:calc(min(1320px, 104vw) / -2);border-radius:999px 999px 0 0;overflow:hidden;background:var(--ink);isolation:isolate}.contact-sun-rays{position:absolute;left:50%;top:100%;width:300%;aspect-ratio:1;margin:-150% 0 0 -150%;border-radius:50%;background:var(--rays)}.motion .contact-sun-rays{animation:spin 160s linear infinite reverse}.contact.is-off .contact-sun-rays{animation-play-state:paused}.contact-in{position:relative;z-index:2;display:flex;flex-direction:column;align-items:center}.contact-intro{text-align:center;max-width:1120px}.contact-title{font:900 clamp(54px, 10.5vw, 168px)/.86 var(--f-display);letter-spacing:-.055em;text-wrap:balance}.contact-lede{margin:28px auto 0;max-width:32em}
.contact-card{position:relative;margin-top:clamp(56px, 8vw, 110px);width:100%;max-width:1060px;display:grid;grid-template-columns:minmax(0, 1fr) minmax(0, 1.35fr);gap:clamp(28px, 4vw, 56px);padding:clamp(24px, 3.4vw, 48px);background:var(--paper-hi);border:var(--stroke) solid var(--ink);box-shadow:10px 10px 0 var(--red)}.contact-list{display:flex;flex-direction:column;gap:20px}.contact-list dt{font:600 11.5px/1.2 var(--f-mono);letter-spacing:.1em;text-transform:uppercase;color:var(--red)}.contact-list dd{margin:4px 0 0;font-size:18px;line-height:1.4;overflow-wrap:anywhere}.contact-form{display:grid;grid-template-columns:repeat(2, minmax(0, 1fr));gap:18px 22px;align-content:start}.contact-form label{display:flex;flex-direction:column;gap:6px;min-width:0}.contact-form label.full{grid-column:1/-1}.contact-form label span{font:500 11.5px/1.2 var(--f-mono);text-transform:uppercase;letter-spacing:.06em;color:var(--ink-soft)}.contact-form input,.contact-form textarea{width:100%;border:0;border-bottom:var(--stroke) solid var(--ink);background:transparent;padding:8px 0;font:400 18px/1.4 var(--f-text);color:var(--ink);border-radius:0;resize:vertical}.contact-form input:focus,.contact-form textarea:focus{outline:none;border-bottom-color:var(--red);box-shadow:0 1px 0 var(--red)}.contact-form .btn{justify-self:start;margin-top:6px}.form-status{grid-column:1/-1;font:500 13px/1.3 var(--f-mono);color:var(--red);min-height:1.3em}@media (max-width:760px){.contact-card{grid-template-columns:1fr}.contact-form{grid-template-columns:1fr}.contact-sun{height:46%}}
.site-foot{position:relative;background:var(--ink);color:var(--paper);padding:clamp(72px, 9vw, 120px) 0 28px;overflow-x:clip}.foot-mark{display:block;font:900 min(34vw, calc((100vw - 2 * var(--gut)) / (var(--len) * .58)))/.8 var(--f-display);letter-spacing:-.06em;color:var(--red);white-space:nowrap;text-align:center;margin-bottom:clamp(40px, 6vw, 72px)}.foot-grid{display:grid;grid-template-columns:repeat(auto-fit, minmax(190px, 1fr));gap:32px;padding-top:28px;border-top:var(--stroke) solid color-mix(in oklab, var(--paper) 25%, transparent)}.foot-grid h3{font:600 11.5px/1.2 var(--f-mono);letter-spacing:.1em;text-transform:uppercase;color:var(--red);margin-bottom:12px}.foot-grid li{margin:6px 0}.foot-grid p,.foot-grid li{font-size:16px}.foot-base{display:flex;flex-wrap:wrap;justify-content:space-between;gap:12px;margin-top:48px}.foot-base .chip{border-color:var(--paper-hi)}.site-foot .chip .chip-k{background:var(--red);color:var(--ink)}.foot-legal{margin-top:28px;max-width:62em;font:400 11.5px/1.6 var(--f-mono);color:color-mix(in oklab, var(--paper) 50%, var(--ink))}
.motion [data-reveal]{opacity:0}.motion [data-rule]::after{transform:scaleX(0);transition:transform 1.3s var(--ease)}.motion [data-rule].ruled::after{transform:none}.motion [data-rule]>*{opacity:0}.motion [data-split]{visibility:hidden}@keyframes spin{to{rotate:360deg}}@keyframes bob{from{translate:0 -6px}to{translate:0 6px}}.motion .rays{animation:spin 150s linear infinite}.motion .cover-art [data-fly]{animation:bob 2.8s ease-in-out infinite alternate}.motion .cover-art .cv-f--b{animation-duration:3.3s;animation-delay:-1s}.motion .cover-art .cv-f--c{animation-duration:3.1s;animation-delay:-2s}.motion .cover-art .cv-f--d{animation-duration:2.5s;animation-delay:-.6s}.motion .cover-art .ray-word{animation-duration:3.6s}.motion .cover-art .bubble{animation-duration:2.2s;animation-delay:-1.4s}.cover-stage.is-off .rays,.cover-stage.is-off [data-fly]{animation-play-state:paused}</style>
</head>
<body>
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <symbol id="sym-orbit" viewBox="-160 -160 320 170">
    <g fill="none" stroke="currentColor" stroke-width="1.2" vector-effect="non-scaling-stroke">
      <ellipse cx="0" cy="-75" rx="150" ry="34"/>
      <ellipse cx="0" cy="-75" rx="150" ry="34" transform="rotate(28 0 -75)"/>
      <ellipse cx="0" cy="-75" rx="150" ry="34" transform="rotate(-28 0 -75)" stroke-dasharray="4 6"/>
      <ellipse cx="0" cy="-75" rx="58" ry="58" stroke-dasharray="1 5"/>
      <circle class="sym-core" cx="0" cy="-75" r="28"/>
      <circle cx="0" cy="-75" r="16"/>
      <path d="M-10 -75h20M0 -85v20"/>
    </g>
    <circle class="sym-node" cx="132.4" cy="-4.6" r="5"/><circle class="sym-node" cx="132.4" cy="-145.4" r="5"/><circle class="sym-node" cx="-150" cy="-75" r="5"/><circle class="sym-node" cx="0" cy="-109" r="4"/>
  </symbol>
</svg>
<header class="site-head at-cover" data-head data-section="nav">
  <a class="brand" href="#cover" aria-label="Corvel, back to top">corvel<i>.</i></a>
  <nav class="nav" aria-label="Main">
    <a class="tlink" href="#contents">Capital</a>
    <a class="tlink" href="#work">Portfolio</a>
    <a class="tlink" href="#team">Partners</a>
    <a class="tlink" href="#pricing">Terms</a>
    <a class="tlink" href="#contact">Contact</a>
  </nav>
  <a class="btn head-cta" href="#contact"><span>Pitch a build</span></a>
  <button class="ibtn menu-btn" type="button" aria-expanded="false" aria-controls="menu" aria-label="Open menu" data-label-open="Open menu" data-label-close="Close menu">
    <svg viewBox="0 0 20 20" aria-hidden="true"><path d="M3 7h14M3 13h14" stroke="currentColor" stroke-width="1.8" fill="none"/></svg>
  </button>
  <div class="menu" id="menu" data-menu>
    <button class="ibtn menu-close" type="button" aria-label="Close menu" data-menu-close>
      <svg viewBox="0 0 20 20" aria-hidden="true"><path d="M5 5l10 10M15 5L5 15" stroke="currentColor" stroke-width="1.8" fill="none"/></svg>
    </button>
    <ul>
      <li><a href="#contents">Capital<svg viewBox="0 0 12 20" aria-hidden="true"><path d="M2 2l8 8-8 8" fill="none" stroke="currentColor" stroke-width="2"/></svg></a></li>
      <li><a href="#work">Portfolio<svg viewBox="0 0 12 20" aria-hidden="true"><path d="M2 2l8 8-8 8" fill="none" stroke="currentColor" stroke-width="2"/></svg></a></li>
      <li><a href="#team">Partners<svg viewBox="0 0 12 20" aria-hidden="true"><path d="M2 2l8 8-8 8" fill="none" stroke="currentColor" stroke-width="2"/></svg></a></li>
      <li><a href="#pricing">Terms<svg viewBox="0 0 12 20" aria-hidden="true"><path d="M2 2l8 8-8 8" fill="none" stroke="currentColor" stroke-width="2"/></svg></a></li>
      <li><a href="#contact">Contact<svg viewBox="0 0 12 20" aria-hidden="true"><path d="M2 2l8 8-8 8" fill="none" stroke="currentColor" stroke-width="2"/></svg></a></li>
    </ul>
    <a class="btn" href="#contact"><span>Pitch a build</span></a>
  </div>
</header>

<main>
  <section id="cover" class="cover" data-kind="hero" data-section="hero">
    <div class="cover-pin">
      <div class="cover-stage" data-cover-stage>
        <svg class="dandelion dandelion--l" aria-hidden="true"><use href="#sym-orbit"/></svg>
        <svg class="dandelion dandelion--r" aria-hidden="true"><use href="#sym-orbit"/></svg>

        <div class="cover-head">
          <h1 class="cover-title"><span class="mast" style="--len:6" data-mast>corvel</span><span class="cover-tag">Capital for things that are hard to build</span></h1>
          <a class="cover-mail tlink" href="mailto:deals@corvel.capital">deals@corvel.capital</a>
        </div>

        <div class="cover-art" data-fixed="4" data-burst>
          <svg class="cover-lines" viewBox="-1500 -1500 3000 3000" aria-hidden="true"><line x1="-299.3" y1="20.9" x2="-1496.3" y2="104.6"/><line x1="-311.6" y1="-25.8" x2="-1494.9" y2="-123.8"/><line x1="-309" y1="-82.4" x2="-1449.4" y2="-386.5"/><line x1="-297.7" y1="-148.2" x2="-1342.8" y2="-668.4"/><line x1="-277.7" y1="-211.4" x2="-1193.6" y2="-908.5" class="dash"/><line x1="-235.6" y1="-248.5" x2="-1032.1" y2="-1088.5"/><line x1="-201.2" y1="-275.4" x2="-884.9" y2="-1211.2"/><line x1="-139.6" y1="-319.3" x2="-601" y2="-1374.3" class="dash"/><line x1="-83.2" y1="-345.5" x2="-351.2" y2="-1458.3"/><line x1="-15.6" y1="-334.3" x2="-70.1" y2="-1498.4"/><line x1="54.7" y1="-317.7" x2="254.6" y2="-1478.2" class="dash"/><line x1="118.8" y1="-297.1" x2="556.9" y2="-1392.8" class="dash"/><line x1="165.7" y1="-280.4" x2="763.1" y2="-1291.4" class="dash"/><line x1="228.3" y1="-243.1" x2="1026.9" y2="-1093.4"/><line x1="250.1" y1="-172" x2="1235.8" y2="-850.2" class="dash"/><line x1="301.6" y1="-135.3" x2="1368.6" y2="-614"/><line x1="340.8" y1="-97.8" x2="1441.8" y2="-413.6" class="dash"/><line x1="318.4" y1="-38" x2="1489.4" y2="-178"/></svg>
          <div class="arch-line"></div>
          <div class="arch" data-arch>
            <div class="rays-turn" data-rays-turn><div class="rays" data-rays></div></div>
            <div class="arch-dots"></div>
            <div class="arch-grain"></div>
          </div>
          <span class="ray-word ray-word--a" data-fly>Underwrite</span>
          <span class="ray-word ray-word--b" data-fly>Build</span>
          <figure class="print" data-print>
            <div class="ht"><div class="ht-scr"><div class="art" data-art="wafer" data-seed="11" data-vb="400 400" role="img" aria-label="A 300 mm silicon wafer with a grid of dies"></div></div></div>
            <figcaption>Tape-out No. 04</figcaption>
          </figure>
          <figure class="cv-f cv-f--a" data-fly><div class="ph"><div class="art" data-art="die" data-seed="3" data-vb="300 350" role="img" aria-label="A chip die with bond wires"></div></div></figure>
          <figure class="cv-f cv-f--b" data-fly><div class="ph"><div class="art" data-art="orbit" data-seed="5" data-vb="300 300" role="img" aria-label="A planet with three satellite orbits"></div></div></figure>
          <figure class="cv-f cv-f--c" data-fly><div class="ph"><div class="art" data-art="candles" data-seed="8" data-vb="300 420" role="img" aria-label="A candlestick price chart"></div></div></figure>
          <figure class="cv-f cv-f--d" data-fly><div class="ph"><div class="art" data-art="curve" data-seed="2" data-vb="520 400" role="img" aria-label="A family of yield curves"></div></div></figure>
          <p class="bubble" data-fly><svg viewBox="0 0 24 24" aria-hidden="true"><path d="M13.5 2 4 14h7l-1.5 8L19 10h-7z" fill="currentColor"/></svg><span>$4.2B deployed into hardware</span></p>
        </div>

        <div class="cover-chips">
          <p class="chip"><span class="chip-k">Plate</span><span class="chip-v">300 mm wafer map, drawn in code</span></p>
          <a class="btn" href="#contact"><span>Pitch a build</span><span class="btn-v">Reply in 24 h</span></a>
        </div>
      </div>
    </div>
    <div class="cover-extra wrap">
      <nav class="cover-aside toc" aria-label="On this page">
        <ul>
          <li><a href="#contents"><b>Capital shaped like the machine</b><svg viewBox="0 0 10 16" aria-hidden="true"><path d="M2 2l6 6-6 6" fill="none" stroke="currentColor" stroke-width="1.6"/></svg><small>Instruments</small></a></li>
          <li><a href="#work"><b>Four builds, financed end to end</b><svg viewBox="0 0 10 16" aria-hidden="true"><path d="M2 2l6 6-6 6" fill="none" stroke="currentColor" stroke-width="1.6"/></svg><small>Portfolio</small></a></li>
          <li><a href="#pricing"><b>Plain terms, no fee games</b><svg viewBox="0 0 10 16" aria-hidden="true"><path d="M2 2l6 6-6 6" fill="none" stroke="currentColor" stroke-width="1.6"/></svg><small>Terms</small></a></li>
        </ul>
      </nav>
      <p class="cover-no"><b>3</b><span>lead allocations left in Fund IV this year</span></p>
    </div>
  </section>

  <section id="contents" class="contents" data-kind="services" data-section="services">
    <div class="wrap contents-grid">
      <div class="contents-head">
        <svg class="dandelion-s" viewBox="-160 -160 320 170" aria-hidden="true"><use href="#sym-orbit"/></svg>
        <h2 class="h2" data-split>Capital shaped like the machine</h2>
        <p class="lede" data-reveal>Five instruments, one habit: we start from the engineering, then shape the money around how the thing is actually built, tested and paid for.</p>
      </div>
      <ul class="svc-list-wrap">
        <li class="svc" data-rule>
          <h3>Venture equity</h3>
          <span class="svc-price">from $5M</span>
          <p>Series A to C for hardware companies past their first working prototype. We lead, we take a board seat, and we put an engineer on it.</p>
          <ul class="svc-list"><li>Lead or co-lead</li><li>Board seat</li><li>Technical diligence</li></ul>
        </li>
        <li class="svc" data-rule>
          <h3>Project finance</h3>
          <span class="svc-price">from $40M</span>
          <p>Non-recourse debt for first-of-a-kind plants, released in tranches as each stage of commissioning is proven.</p>
          <ul class="svc-list"><li>FOAK plants</li><li>Milestone tranches</li><li>Lender syndicate</li></ul>
        </li>
        <li class="svc" data-rule>
          <h3>Equipment debt</h3>
          <span class="svc-price">from $10M</span>
          <p>Loans and leases secured against the tools themselves — lithography, test stands, kilns — priced on what they are worth on the resale market.</p>
          <ul class="svc-list"><li>Tool-backed loans</li><li>Lease structures</li><li>Residual modelling</li></ul>
        </li>
        <li class="svc" data-rule>
          <h3>Public co-funding</h3>
          <span class="svc-price">advisory</span>
          <p>We assemble government loans, grants and tax credits alongside private capital, so the public money arrives on the same schedule as ours.</p>
          <ul class="svc-list"><li>Loan programmes</li><li>Grant applications</li><li>Tax credit transfer</li></ul>
        </li>
        <li class="svc" data-rule>
          <h3>Offtake and supply</h3>
          <span class="svc-price">included</span>
          <p>Introductions to the anchor customers, foundries and suppliers who turn a prototype into a contracted order book.</p>
          <ul class="svc-list"><li>Anchor customers</li><li>Offtake contracts</li><li>Supplier network</li></ul>
        </li>
      </ul>
    </div>
  </section>

  <section id="feature" class="feature" data-kind="story" data-section="story">
    <div class="wrap feature-grid">
      <figure class="reg" data-reg>
        <div class="reg-stack">
          <div class="reg-plate reg-plate--k ht" data-plate-k><div class="ht-scr"><div class="art" data-art="reactor" data-seed="19" data-vb="400 500" role="img" aria-label="Top-down view of a toroidal reactor with field coils"></div></div></div>
        </div>
        <svg class="reg-mark tl" viewBox="0 0 44 44" aria-hidden="true" data-mark-k><circle cx="22" cy="22" r="11"/><line x1="22" y1="2" x2="22" y2="42"/><line x1="2" y1="22" x2="42" y2="22"/></svg>
        <svg class="reg-mark br" viewBox="0 0 44 44" aria-hidden="true" data-mark-k><circle cx="22" cy="22" r="11"/><line x1="22" y1="2" x2="22" y2="42"/><line x1="2" y1="22" x2="42" y2="22"/></svg>
        <figcaption class="chip"><span class="chip-k">In diligence</span><span class="chip-v">Toroidal field coil layout</span></figcaption>
      </figure>
      <div class="feature-text">
        <h2 class="h2 reg-title" data-reg-title>Hard tech isn't too risky. It's mispriced.</h2>
        <p class="lede" data-reveal>Venture funds price the slide deck; banks price the past. A fab, a launcher or a reactor needs someone who can read the engineering and the balance sheet at the same time.</p>
        <div class="cols" data-reveal>
          <p class="dropcap">Most of the companies we back have to obey physics before they can obey a growth chart. A fab that needs two years of tools. A launcher that needs a test stand. A reactor that needs a licence and a magnet nobody has built before.</p>
          <p>None of that is unfinanceable. It needs capital that knows how the hardware fails, how it depreciates and what it fetches on the second-hand market. We price the machine, not the mood — and every deal begins on the factory floor.</p>
        </div>
        <p class="sign" data-reveal>Mara Lindqvist and Daniel Okafor, managing partners</p>
      </div>
    </div>
  </section>

  <section id="work" class="work ramp-top" data-kind="projects" data-tone="dark" data-section="portfolio">
    <div class="wrap work-head">
      <h2 class="h2" data-split>Four builds, financed end to end</h2>
      <p class="lede" data-reveal>Fabs, satellites, storage and fusion. Each one was told it was too early for a bank and too heavy for venture.</p>
    </div>
    <div class="work-pin" data-track>
      <div class="work-stage">
        <div class="work-track">
          <article class="spread">
            <figure class="spread-ph ph"><div class="art" data-art="wafer" data-opt="bins" data-fit="meet" data-seed="23" data-vb="400 400" role="img" aria-label="Wafer map with dies colour-coded by yield bin"></div></figure>
            <div class="spread-txt">
              <p class="spread-year"><b style="--len:4">2019</b><span>Semiconductors · GaN power</span></p>
              <h3 class="spread-name">Halden Semiconductor</h3>
              <p>We led a $62M Series B and structured $140M of equipment debt against 41 tools, so the fab could buy its line without selling another quarter of the company.</p>
              <p class="spread-result">First wafers out 11 weeks early; 94% line yield by month nine.</p>
            </div>
          </article>
          <article class="spread">
            <figure class="spread-ph ph"><div class="art" data-art="constellation" data-seed="31" data-vb="600 400" role="img" aria-label="A satellite constellation with crosslinks above the curve of the Earth"></div></figure>
            <div class="spread-txt">
              <p class="spread-year"><b style="--len:4">2021</b><span>Space · SAR imaging</span></p>
              <h3 class="spread-name">Kestrel Orbital</h3>
              <p>Banks valued the satellites as scrap. We financed 48 of them against signed imaging contracts, with launch insurance built into the facility.</p>
              <p class="spread-result">Launch to revenue in 7 months; $310M contracted backlog.</p>
            </div>
          </article>
          <article class="spread">
            <figure class="spread-ph ph"><div class="art" data-art="storage" data-seed="41" data-vb="600 400" role="img" aria-label="Site plan of battery containers with a state-of-charge curve"></div></figure>
            <div class="spread-txt">
              <p class="spread-year"><b style="--len:4">2022</b><span>Energy · Long-duration storage</span></p>
              <h3 class="spread-name">Vela Grid</h3>
              <p>A 200 MWh first-of-a-kind plant, financed with non-recourse project debt released in four tranches tied to commissioning tests.</p>
              <p class="spread-result">Commercial operation on budget; refinanced 210 bps tighter.</p>
            </div>
          </article>
          <article class="spread">
            <figure class="spread-ph ph"><div class="art" data-art="tokamak" data-seed="53" data-vb="600 400" role="img" aria-label="Cross-section of a tokamak plasma with nested flux surfaces"></div></figure>
            <div class="spread-txt">
              <p class="spread-year"><b style="--len:4">2024</b><span>Fusion · Magnet systems</span></p>
              <h3 class="spread-name">Aurel Fusion</h3>
              <p>Milestone-based equity for a high-field magnet test facility: each tranche unlocked by a measured field strength, not a calendar date.</p>
              <p class="spread-result">Hit 12.2 T on schedule; unlocked a $95M follow-on in 14 months.</p>
            </div>
          </article>
        </div>
      </div>
    </div>
  </section>

  <section id="figures" class="figures ramp-top" data-kind="stats" data-tone="dark" data-section="stats">
    <div class="fig-rays" aria-hidden="true"><div></div></div>
    <div class="wrap">
      <h2 class="h2 fig-title" data-split>Small fund, deep bench</h2>
      <ul class="fig-list">
        <li class="fig" data-stamp><b style="--len:5">$4.2B</b><span>deployed into hardware since 2011, equity and debt combined</span></li>
        <li class="fig" data-stamp><b style="--len:2">71</b><span>companies building fabs, launchers, reactors and robots</span></li>
        <li class="fig" data-stamp><b style="--len:2">21</b><span>days, on average, from first site visit to term sheet</span></li>
        <li class="fig" data-stamp><b style="--len:1">0</b><span>defaults in our project-finance book. We underwrite the engineering first</span></li>
      </ul>
    </div>
  </section>

  <section id="process" class="process" data-kind="steps" data-section="process">
    <div class="wrap process-grid">
      <div class="process-head">
        <h2 class="h2" data-split>From a lab bench to a balance sheet</h2>
        <p class="lede" data-reveal>Every deal follows the same five steps. The first one always happens on your floor, not in our office.</p>
        <a class="btn" href="#contact" data-reveal><span>Book a site visit</span></a>
      </div>
      <ol class="proofs" data-proofs>
        <li class="proof">
          <span class="proof-bar" aria-hidden="true"></span>
          <p class="meta">Week 1</p>
          <h3 class="h3">Site visit and teardown</h3>
          <p>We come to the lab or the line, pull the bill of materials apart and talk to the engineers who built the prototype — not only the founders who pitch it.</p>
        </li>
        <li class="proof">
          <span class="proof-bar" aria-hidden="true"></span>
          <p class="meta">Weeks 1–2</p>
          <h3 class="h3">Technical diligence</h3>
          <p>An in-house engineer models yield, uptime, degradation and unit cost. You keep the report whether we invest or not.</p>
        </li>
        <li class="proof">
          <span class="proof-bar" aria-hidden="true"></span>
          <p class="meta">Week 3</p>
          <h3 class="h3">Term sheet</h3>
          <p>One document, equity and debt side by side, with every covenant, milestone and fee written in plain numbers.</p>
        </li>
        <li class="proof">
          <span class="proof-bar" aria-hidden="true"></span>
          <p class="meta">Weeks 4–8</p>
          <h3 class="h3">Structure and close</h3>
          <p>We syndicate lenders, line up offtakers and public co-funding, and close on the date written in the term sheet.</p>
        </li>
        <li class="proof">
          <span class="proof-bar" aria-hidden="true"></span>
          <p class="meta">After close</p>
          <h3 class="h3">Stay on the floor</h3>
          <p>Quarterly operating reviews, and a partner on call the day a tool slips or a supplier fails.</p>
        </li>
      </ol>
    </div>
  </section>

  <section id="team" class="team" data-kind="team" data-section="team">
    <div class="wrap">
      <div class="team-head">
        <h2 class="h2" data-split>Four partners, two disciplines</h2>
        <p class="lede" data-reveal>Two engineers, a credit structurer and an operator. Every deal is signed off by both sides of the table.</p>
      </div>
      <ul class="people" data-people>
        <li class="person">
          <div class="person-arch ht"><div class="ht-scr"><div class="art" data-art="portrait" data-seed="61" data-vb="300 400" role="img" aria-label="Halftone portrait silhouette of Mara Lindqvist"></div></div></div>
          <h3 class="person-name">Mara Lindqvist</h3>
          <p class="chip"><span class="chip-k">Managing partner</span><span class="chip-v">Semiconductors</span></p>
          <p class="person-note">Ran a 300 mm lithography bay for nine years before she ever read a term sheet.</p>
        </li>
        <li class="person">
          <div class="person-arch ht"><div class="ht-scr"><div class="art" data-art="portrait" data-seed="72" data-vb="300 400" role="img" aria-label="Halftone portrait silhouette of Daniel Okafor"></div></div></div>
          <h3 class="person-name">Daniel Okafor</h3>
          <p class="chip"><span class="chip-k">Managing partner</span><span class="chip-v">Credit</span></p>
          <p class="person-note">Structured project debt behind twelve gigawatts of power plants. Still reads indentures for fun.</p>
        </li>
        <li class="person">
          <div class="person-arch ht"><div class="ht-scr"><div class="art" data-art="portrait" data-seed="88" data-vb="300 400" role="img" aria-label="Halftone portrait silhouette of Priya Raman"></div></div></div>
          <h3 class="person-name">Priya Raman</h3>
          <p class="chip"><span class="chip-k">Partner</span><span class="chip-v">Space</span></p>
          <p class="person-note">Former propulsion lead. Can estimate a satellite's lifespan from its thruster datasheet.</p>
        </li>
        <li class="person">
          <div class="person-arch ht"><div class="ht-scr"><div class="art" data-art="portrait" data-seed="97" data-vb="300 400" role="img" aria-label="Halftone portrait silhouette of Henrik Vos"></div></div></div>
          <h3 class="person-name">Henrik Vos</h3>
          <p class="chip"><span class="chip-k">Operating partner</span><span class="chip-v">Manufacturing</span></p>
          <p class="person-note">Has commissioned eleven factories on three continents and still carries a torque wrench in his bag.</p>
        </li>
      </ul>
    </div>
  </section>

  <section id="voices" class="voices ramp-top" data-kind="reviews" data-tone="dark" data-section="reviews">
    <div class="wrap voices-head">
      <h2 class="h2" data-split>What founders say</h2>
      <p class="lede" data-reveal>Most of our founders heard no from a bank and a venture fund in the same week. Here is what happened next.</p>
    </div>
    <div class="marquee" data-marquee>
      <ul class="mq-track">
        <li class="quote">
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 18h6l2-6V5H3v7h3zm10 0h6l2-6V5h-8v7h3z" fill="currentColor"/></svg>
          <blockquote>They sent a process engineer before they sent a term sheet. Nobody else asked to see our yield data.</blockquote>
          <p class="quote-by"><b>Lena Hart</b><span>CEO, Halden Semiconductor</span></p>
        </li>
        <li class="quote">
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 18h6l2-6V5H3v7h3zm10 0h6l2-6V5h-8v7h3z" fill="currentColor"/></svg>
          <blockquote>Our bank priced the satellites as scrap metal. Corvel priced them as revenue in orbit.</blockquote>
          <p class="quote-by"><b>Tomás Arce</b><span>CFO, Kestrel Orbital</span></p>
        </li>
        <li class="quote">
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 18h6l2-6V5H3v7h3zm10 0h6l2-6V5h-8v7h3z" fill="currentColor"/></svg>
          <blockquote>The debt closed on the day they said it would. Eighteen months later, so did the plant.</blockquote>
          <p class="quote-by"><b>Grace Mbeki</b><span>Founder, Vela Grid</span></p>
        </li>
        <li class="quote">
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 18h6l2-6V5H3v7h3zm10 0h6l2-6V5h-8v7h3z" fill="currentColor"/></svg>
          <blockquote>We asked for a cheque. We got a funding schedule that matched the physics.</blockquote>
          <p class="quote-by"><b>Jonas Weil</b><span>CTO, Aurel Fusion</span></p>
        </li>
        <li class="quote">
          <svg viewBox="0 0 24 24" aria-hidden="true"><path d="M3 18h6l2-6V5H3v7h3zm10 0h6l2-6V5h-8v7h3z" fill="currentColor"/></svg>
          <blockquote>Clear terms, no fee games, and a partner who actually opens the CAD files.</blockquote>
          <p class="quote-by"><b>Sofia Marin</b><span>CEO, Ostra Robotics</span></p>
        </li>
      </ul>
    </div>
  </section>

  <section id="gallery" class="gallery" data-kind="gallery" data-section="gallery">
    <div class="wrap">
      <div class="gallery-head">
        <h2 class="h2" data-split>On the desk this quarter</h2>
        <p class="lede" data-reveal>Models, test data and site maps from live diligence. Every image on this page is drawn from code, not stock.</p>
      </div>
      <div class="collage" data-fixed="6" data-develop>
        <figure class="g g--a"><div class="ph"><div class="art" data-art="pcb" data-seed="101" data-vb="700 560" role="img" aria-label="Circuit board traces around a processor"></div></div><figcaption>Board teardown, satellite bus</figcaption></figure>
        <figure class="g g--b"><div class="ht"><div class="ht-scr"><div class="art" data-art="depth" data-seed="113" data-vb="560 300" role="img" aria-label="Order book depth chart"></div></div></div><figcaption>Order book, secondary block sale</figcaption></figure>
        <figure class="g g--c"><div class="ht ht--red"><div class="ht-scr"><div class="art" data-art="spectrum" data-seed="127" data-vb="320 300" role="img" aria-label="Vibration spectrum bars"></div></div></div><figcaption>Vibration spectrum, launch qual</figcaption></figure>
        <figure class="g g--d"><div class="ph"><div class="art" data-art="die" data-seed="131" data-vb="360 300" role="img" aria-label="Chip die macro"></div></div><figcaption>Die shot, 650 V GaN switch</figcaption></figure>
        <figure class="g g--e"><div class="ph"><div class="art" data-art="contour" data-seed="137" data-vb="480 400" role="img" aria-label="Topographic site survey contours"></div></div><figcaption>Site survey, 200 MWh plant</figcaption></figure>
        <figure class="g g--f"><div class="ht"><div class="ht-scr"><div class="art" data-art="candles" data-seed="149" data-vb="820 360" role="img" aria-label="Candlestick chart of portfolio marks"></div></div></div><figcaption>Mark-to-market, Fund III</figcaption></figure>
      </div>
    </div>
  </section>

  <section id="pricing" class="pricing ramp-top" data-kind="pricing" data-tone="dark" data-section="pricing">
    <div class="wrap">
      <div class="pricing-head">
        <h2 class="h2" data-split>Plain terms, no fee games</h2>
        <div class="bill" role="group" aria-label="Instrument" data-bill>
          <button type="button" class="bill-opt" aria-pressed="true" data-bill-set="once">Equity</button>
          <button type="button" class="bill-opt" aria-pressed="false" data-bill-set="monthly">Debt</button>
        </div>
      </div>
      <ul class="tags" data-tags>
        <li class="tag">
          <h3 class="tag-name">Prototype</h3>
          <p class="tag-for">A working unit, a first customer and a line to build.</p>
          <p class="tag-price"><b class="bill-once" style="--len:6">$5–15M</b><b class="bill-monthly" style="--len:4">$10M</b><span class="bill-once">equity cheque, lead</span><span class="bill-monthly">venture debt, up to</span></p>
          <ul class="tag-list"><li>Lead or co-lead</li><li>Diligence report, yours to keep</li><li>Foundry and supplier introductions</li></ul>
          <a class="btn btn--light" href="#contact"><span>Discuss Prototype</span></a>
        </li>
        <li class="tag tag--hot">
          <h3 class="tag-name">Scale</h3>
          <p class="tag-for">The line works. Now it needs tools, people and a second shift.</p>
          <p class="tag-price"><b class="bill-once" style="--len:7">$15–60M</b><b class="bill-monthly" style="--len:5">$120M</b><span class="bill-once">equity cheque, lead</span><span class="bill-monthly">tool-backed debt, up to</span></p>
          <ul class="tag-list"><li>Everything in Prototype</li><li>Equity and equipment debt together</li><li>Board seat with an engineer on it</li><li>Quarterly operating reviews</li></ul>
          <a class="btn" href="#contact"><span>Discuss Scale</span></a>
        </li>
        <li class="tag">
          <h3 class="tag-name">First plant</h3>
          <p class="tag-for">A first-of-a-kind facility, financed like infrastructure.</p>
          <p class="tag-price"><b class="bill-once" style="--len:5">$60M+</b><b class="bill-monthly" style="--len:5">$500M</b><span class="bill-once">equity, with partners</span><span class="bill-monthly">project debt, arranged</span></p>
          <ul class="tag-list"><li>Everything in Scale</li><li>Non-recourse project finance</li><li>Offtake and EPC structuring</li><li>Public co-funding applications</li></ul>
          <a class="btn btn--light" href="#contact"><span>Discuss First plant</span></a>
        </li>
      </ul>
      <p class="pricing-note">Indicative ranges, not an offer. Every structure is priced on diligence. We charge founders no deal or monitoring fees; legal costs are capped and agreed in the term sheet.</p>
    </div>
  </section>

  <section id="faq" class="faq" data-kind="faq" data-section="faq">
    <div class="wrap">
      <div class="faq-head">
        <h2 class="h2" data-split>Questions founders ask us first</h2>
        <p class="lede" data-reveal>Anything else, ask at <a class="tlink" href="mailto:deals@corvel.capital">deals@corvel.capital</a>. A partner answers, usually the same day.</p>
      </div>
      <div class="qa-list">
        <details class="qa" data-rule>
          <summary><span>Do we need revenue before you invest?</span><svg viewBox="0 0 16 16" aria-hidden="true"><path d="M3 6l5 5 5-5" fill="none" stroke="currentColor" stroke-width="1.8"/></svg></summary>
          <div class="qa-a"><p>No. We underwrite engineering milestones: a working prototype, a yield number, a qualified part. Revenue is one milestone among several, not the first.</p></div>
        </details>
        <details class="qa" data-rule>
          <summary><span>Can you finance a first-of-a-kind plant?</span><svg viewBox="0 0 16 16" aria-hidden="true"><path d="M3 6l5 5 5-5" fill="none" stroke="currentColor" stroke-width="1.8"/></svg></summary>
          <div class="qa-a"><p>Yes — that is most of our debt book. We release capital in tranches tied to commissioning, so each lender takes the risk it understands at the moment it understands it.</p></div>
        </details>
        <details class="qa" data-rule>
          <summary><span>Where do you invest?</span><svg viewBox="0 0 16 16" aria-hidden="true"><path d="M3 6l5 5 5-5" fill="none" stroke="currentColor" stroke-width="1.8"/></svg></summary>
          <div class="qa-a"><p>North America and Europe, across semiconductors, space, energy, advanced manufacturing and robotics. The first meeting is always on site.</p></div>
        </details>
        <details class="qa" data-rule>
          <summary><span>Who owns the IP?</span><svg viewBox="0 0 16 16" aria-hidden="true"><path d="M3 6l5 5 5-5" fill="none" stroke="currentColor" stroke-width="1.8"/></svg></summary>
          <div class="qa-a"><p>You do. Our debt is secured against equipment and contracts, never against patents or source files.</p></div>
        </details>
        <details class="qa" data-rule>
          <summary><span>How fast can you move?</span><svg viewBox="0 0 16 16" aria-hidden="true"><path d="M3 6l5 5 5-5" fill="none" stroke="currentColor" stroke-width="1.8"/></svg></summary>
          <div class="qa-a"><p>Term sheets average 21 days from the first site visit. Fund IV is allocating now, and the investment committee meets every second Thursday.</p></div>
        </details>
      </div>
    </div>
  </section>

  <section id="contact" class="contact" data-kind="contact" data-section="contact">
    <svg class="contact-burst" aria-hidden="true" data-burst-lines></svg>
    <div class="contact-sun" aria-hidden="true" data-sun><div class="contact-sun-rays"></div><div class="arch-grain"></div></div>
    <div class="wrap contact-in">
      <div class="contact-intro" data-burst-center>
        <h2 class="contact-title">Bring us the bill of materials.</h2>
        <p class="lede contact-lede">A deck, a cap table, a tool list, a photo of the prototype at 2 a.m. Send what you have and a partner will tell you what we see — within a day.</p>
      </div>
      <div class="contact-card">
        <dl class="contact-list">
          <div><dt>Email</dt><dd><a class="tlink" href="mailto:deals@corvel.capital">deals@corvel.capital</a></dd></div>
          <div><dt>Phone</dt><dd><a class="tlink" href="tel:+14155550142">+1 (415) 555-0142</a></dd></div>
          <div><dt>Office</dt><dd>88 Foundry Row, San Francisco, CA 94107</dd></div>
          <div><dt>Hours</dt><dd>Monday to Friday, 08:00–18:00 PT</dd></div>
        </dl>
        <form class="contact-form" novalidate data-form data-sent="Received. A partner will reply within one business day." data-error="Please add your name and a way to reach you.">
          <label><span>Your name</span><input name="name" autocomplete="name" required></label>
          <label><span>Email</span><input name="reach" type="email" autocomplete="email" required></label>
          <label class="full"><span>What are you building, and what will it cost?</span><textarea name="msg" rows="3"></textarea></label>
          <button class="btn" type="submit"><span>Send it over</span></button>
          <p class="form-status" role="status" aria-live="polite"></p>
        </form>
      </div>
    </div>
  </section>
</main>

<footer class="site-foot ramp-top" data-section="footer">
  <div class="wrap">
    <span class="foot-mark" style="--len:6" aria-hidden="true">corvel</span>
    <div class="foot-grid">
      <div>
        <h3>Office</h3>
        <p>88 Foundry Row<br>San Francisco, CA 94107</p>
      </div>
      <div>
        <h3>Talk to us</h3>
        <ul>
          <li><a class="tlink" href="mailto:deals@corvel.capital">deals@corvel.capital</a></li>
          <li><a class="tlink" href="tel:+14155550142">+1 (415) 555-0142</a></li>
        </ul>
      </div>
      <div>
        <h3>Pages</h3>
        <ul>
          <li><a class="tlink" href="#contents">Capital</a></li>
          <li><a class="tlink" href="#work">Portfolio</a></li>
          <li><a class="tlink" href="#pricing">Terms</a></li>
        </ul>
      </div>
      <div>
        <h3>Elsewhere</h3>
        <ul>
          <li><a class="tlink" href="#">LinkedIn</a></li>
          <li><a class="tlink" href="#">Annual letter</a></li>
          <li><a class="tlink" href="#">Careers</a></li>
        </ul>
      </div>
    </div>
    <div class="foot-base">
      <p class="chip"><span class="chip-k">© 2026</span><span class="chip-v">Corvel Capital Partners</span></p>
      <p class="chip"><span class="chip-k">Underwritten</span><span class="chip-v">in silicon, steel and spreadsheets</span></p>
    </div>
    <p class="foot-legal">Nothing on this page is an offer to sell, or a solicitation of an offer to buy, any security. Portfolio figures are illustrative and past performance is not indicative of future results. Corvel is a fictional firm made for a template demo; every company, person and number here is invented.</p>
  </div>
</footer>

<script>(()=>{
/* Generative SVG art — replaces every photo on the page */
const R=seed=>{let s=(seed*7919+13)%233280;return()=>(s=(s*9301+49297)%233280)/233280};
const n=v=>Math.round(v*10)/10;
const G={
wafer(r,W,H,id,opt){const cx=W/2,cy=H/2,R0=Math.min(W,H)/2-14,st=R0/8.2,bins=opt==='bins';
 let b=`<defs><radialGradient id="wg${id}" cx=".36" cy=".3" r=".9"><stop offset="0" style="stop-color:var(--paper-hi)"/><stop offset=".55" style="stop-color:#8b939e"/><stop offset="1" style="stop-color:#262c35"/></radialGradient></defs><rect width="${W}" height="${H}" class="a-ink"/><circle cx="${cx}" cy="${cy}" r="${R0}" fill="url(#wg${id})"/>`;
 for(let x=cx-R0;x<cx+R0;x+=st)for(let y=cy-R0;y<cy+R0;y+=st){if(Math.hypot(x+st/2-cx,y+st/2-cy)>R0-st*.75)continue;const v=r();let c,o;
  if(bins){c=v<.08?'a-red':v<.2?'a-mid':'a-pap';o=v<.2?1:n(.55+r()*.4)}else{c=v<.06?'a-red':v<.14?'a-ink':'';o=v<.06?1:.35}
  b+=`<rect x="${n(x+1)}" y="${n(y+1)}" width="${n(st-2)}" height="${n(st-2)}" fill="none" class="${c} s-ink" fill-opacity="${o}" stroke-opacity=".45" stroke-width=".7"/>`}
 b+=`<path d="M${n(cx-9)} ${n(cy+R0)}l9-11 9 11z" class="a-ink"/><circle cx="${cx}" cy="${cy}" r="${R0}" fill="none" class="s-pap" stroke-opacity=".5"/><path d="M${n(cx-R0*.7)} ${n(cy+R0*.7)}L${n(cx+R0*.7)} ${n(cy-R0*.7)}" class="s-pap" stroke-opacity=".12" stroke-width="${n(R0*.25)}"/>`;return b},
die(r,W,H){const s=Math.min(W,H)*.66,x0=(W-s)/2,y0=(H-s)/2,np=12,L=Math.max(W,H)*.2;let b=`<rect width="${W}" height="${H}" class="a-ink"/><g fill="none" class="s-pap" stroke-opacity=".45" stroke-width=".8">`;
 for(let i=0;i<np;i++){const t=x0+s*(i+.5)/np,u=y0+s*(i+.5)/np;b+=`<path d="M${n(t)} ${n(y0)}L${n(t+(t-W/2)*.3)} ${n(y0-L)}M${n(t)} ${n(y0+s)}L${n(t+(t-W/2)*.3)} ${n(y0+s+L)}M${n(x0)} ${n(u)}L${n(x0-L)} ${n(u+(u-H/2)*.3)}M${n(x0+s)} ${n(u)}L${n(x0+s+L)} ${n(u+(u-H/2)*.3)}"/>`}
 b+=`</g><rect x="${n(x0)}" y="${n(y0)}" width="${n(s)}" height="${n(s)}" rx="3" style="fill:#363d48"/>`;
 for(let i=0;i<np;i++){const t=x0+s*(i+.5)/np,u=y0+s*(i+.5)/np;b+=`<g class="a-pap" fill-opacity=".85"><rect x="${n(t-3)}" y="${n(y0+4)}" width="6" height="6"/><rect x="${n(t-3)}" y="${n(y0+s-10)}" width="6" height="6"/><rect x="${n(x0+4)}" y="${n(u-3)}" width="6" height="6"/><rect x="${n(x0+s-10)}" y="${n(u-3)}" width="6" height="6"/></g>`}
 const m=18,cw=(s-m*2)/4;for(let i=0;i<4;i++)for(let j=0;j<4;j++){const v=r(),bx=x0+m+i*cw+3,by=y0+m+j*cw+3,w=cw-6;
  if(v<.14)b+=`<rect x="${n(bx)}" y="${n(by)}" width="${n(w)}" height="${n(w)}" class="a-red"/>`;
  else if(v<.45){b+=`<rect x="${n(bx)}" y="${n(by)}" width="${n(w)}" height="${n(w)}" class="a-pap" fill-opacity=".1"/>`;for(let k=1;k<7;k++)b+=`<line x1="${n(bx)}" x2="${n(bx+w)}" y1="${n(by+w*k/7)}" y2="${n(by+w*k/7)}" class="s-pap" stroke-opacity=".4" stroke-width=".7"/>`}
  else b+=`<rect x="${n(bx)}" y="${n(by)}" width="${n(w)}" height="${n(w)}" class="a-pap" fill-opacity="${n(.08+r()*.38)}"/>`}
 return b},
orbit(r,W,H,id){const cx=W/2,cy=H/2,m=Math.min(W,H);let b=`<defs><radialGradient id="og${id}" cx=".35" cy=".3" r=".8"><stop offset="0" style="stop-color:var(--paper-hi)"/><stop offset=".6" style="stop-color:#6d7581"/><stop offset="1" style="stop-color:#1a1f27"/></radialGradient></defs><rect width="${W}" height="${H}" class="a-ink"/>`;
 for(let i=0;i<50;i++)b+=`<circle cx="${n(r()*W)}" cy="${n(r()*H)}" r="${n(.4+r()*1.1)}" class="a-pap" fill-opacity="${n(.2+r()*.6)}"/>`;
 b+=`<circle cx="${cx}" cy="${cy}" r="${n(m*.2)}" fill="url(#og${id})"/>`;
 [[-20,.44,.15],[25,.4,.12],[70,.46,.18]].forEach(([a,rx,ry],i)=>{b+=`<g transform="rotate(${a} ${cx} ${cy})"><ellipse cx="${cx}" cy="${cy}" rx="${n(m*rx)}" ry="${n(m*ry)}" fill="none" class="s-pap" stroke-opacity=".55"${i==1?' stroke-dasharray="4 5"':''}/><circle cx="${n(cx+m*rx)}" cy="${cy}" r="${n(m*.024)}" class="a-red"/></g>`});return b},
candles(r,W,H){const N=Math.max(18,Math.round(W/16)),cw=W/N;let p=100;const d=[];
 for(let i=0;i<N;i++){const o=p,c=o+(r()-.46)*6,hi=Math.max(o,c)+r()*3,lo=Math.min(o,c)-r()*3;d.push([o,c,hi,lo]);p=c}
 const mx=Math.max(...d.map(x=>x[2])),mn=Math.min(...d.map(x=>x[3])),Y=v=>n(H*.1+(mx-v)/(mx-mn)*H*.8);
 let b=`<rect width="${W}" height="${H}" class="a-pap"/>`;for(let k=1;k<6;k++)b+=`<line x1="0" x2="${W}" y1="${n(H*k/6)}" y2="${n(H*k/6)}" class="s-ink" stroke-opacity=".12"/>`;
 let ma='';d.forEach(([o,c,hi,lo],i)=>{const x=i*cw+cw/2,up=c>=o;b+=`<line x1="${n(x)}" x2="${n(x)}" y1="${Y(hi)}" y2="${Y(lo)}" class="s-ink" stroke-width="1.2"/><rect x="${n(x-cw*.32)}" y="${Math.min(Y(o),Y(c))}" width="${n(cw*.64)}" height="${n(Math.max(1.5,Math.abs(Y(o)-Y(c))))}" class="${up?'a-red':'a-ink'}"/>`;
  const sl=d.slice(Math.max(0,i-4),i+1);ma+=`${i?'L':'M'}${n(x)} ${Y(sl.reduce((a,q)=>a+q[1],0)/sl.length)}`});
 return b+`<path d="${ma}" fill="none" class="s-ink" stroke-opacity=".55" stroke-width="1.5"/>`},
curve(r,W,H){let b=`<rect width="${W}" height="${H}" class="a-ink"/>`;
 for(let k=1;k<8;k++)b+=`<line x1="${n(W*k/8)}" x2="${n(W*k/8)}" y1="0" y2="${H}" class="s-pap" stroke-opacity=".08"/>`;
 for(let k=1;k<6;k++)b+=`<line y1="${n(H*k/6)}" y2="${n(H*k/6)}" x1="0" x2="${W}" class="s-pap" stroke-opacity=".08"/>`;
 for(let c=0;c<6;c++){const base=H*(.8-c*.05-r()*.04),amp=H*(.2+r()*.2),kk=.15+r()*.25,last=c==5;let d='';
  for(let i=0;i<=40;i++){const t=i/40;d+=`${i?'L':'M'}${n(W*.06+t*W*.88)} ${n(base-amp*(1-Math.exp(-t/kk)))}`}
  b+=`<path d="${d}" fill="none" class="${last?'s-red':'s-pap'}" stroke-opacity="${last?1:n(.2+c*.08)}" stroke-width="${last?2.5:1.2}"/>`}
 ['3M','2Y','5Y','10Y','30Y'].forEach((t,i)=>b+=`<text x="${n(W*.06+i/4*W*.88)}" y="${n(H*.95)}" class="a-pap" fill-opacity=".55" font-size="${n(H*.045)}" text-anchor="middle" style="font-family:var(--f-mono)">${t}</text>`);return b},
reactor(r,W,H,id){const cx=W/2,cy=H/2,m=Math.min(W,H);let b=`<defs><radialGradient id="rg${id}"><stop offset=".3" style="stop-color:#1a1f27"/><stop offset=".62" style="stop-color:var(--paper-hi)"/><stop offset=".82" style="stop-color:#8b939e"/><stop offset="1" style="stop-color:#1a1f27"/></radialGradient><radialGradient id="rh${id}"><stop offset="0" style="stop-color:#5b6370"/><stop offset="1" style="stop-color:var(--ink)"/></radialGradient></defs><rect width="${W}" height="${H}" fill="url(#rh${id})"/><circle cx="${cx}" cy="${cy}" r="${n(m*.42)}" fill="url(#rg${id})"/>`;
 for(let k=0;k<9;k++)b+=`<circle cx="${cx}" cy="${cy}" r="${n(m*(.2+k*.022))}" fill="none" class="s-pap" stroke-opacity="${n(.15+r()*.45)}"/>`;
 for(let i=0;i<16;i++)b+=`<rect x="${n(cx-m*.03)}" y="${n(cy-m*.48)}" width="${n(m*.06)}" height="${n(m*.13)}" rx="2" class="a-pap s-ink" fill-opacity=".85" transform="rotate(${i*22.5} ${cx} ${cy})"/>`;
 b+=`<circle cx="${cx}" cy="${cy}" r="${n(m*.08)}" class="a-mid s-ink"/>`;
 for(let i=0;i<3;i++){const a=(i*120+20)*Math.PI/180;b+=`<line x1="${n(cx+Math.cos(a)*m*.5)}" y1="${n(cy+Math.sin(a)*m*.5)}" x2="${n(cx+Math.cos(a)*m*.24)}" y2="${n(cy+Math.sin(a)*m*.24)}" class="s-red" stroke-width="2" stroke-dasharray="6 4"/>`}return b},
constellation(r,W,H,id){let b=`<defs><radialGradient id="eg${id}" cx=".5" cy="0" r="1"><stop offset="0" style="stop-color:#4a5260"/><stop offset=".35" style="stop-color:var(--ink)"/></radialGradient></defs><rect width="${W}" height="${H}" class="a-ink"/>`;
 for(let i=0;i<80;i++)b+=`<circle cx="${n(r()*W)}" cy="${n(r()*H*.7)}" r="${n(.4+r())}" class="a-pap" fill-opacity="${n(.15+r()*.6)}"/>`;
 const ex=W/2,ey=H*2.4,ER=H*1.75;b+=`<circle cx="${ex}" cy="${n(ey)}" r="${n(ER)}" fill="url(#eg${id})"/><circle cx="${ex}" cy="${n(ey)}" r="${n(ER)}" fill="none" class="s-red" stroke-opacity=".8" stroke-width="1.5"/>`;
 const rows=[1.1,1.17,1.25].map((k,o)=>{const Rr=ER*k;b+=`<circle cx="${ex}" cy="${n(ey)}" r="${n(Rr)}" fill="none" class="s-pap" stroke-opacity=".22"${o==1?' stroke-dasharray="3 6"':''}/>`;const row=[];for(let j=0;j<11;j++){const a=-Math.PI/2+(j-5)*.11+o*.04;row.push([ex+Rr*Math.cos(a),ey+Rr*Math.sin(a)])}return row});
 rows.forEach((row,o)=>row.forEach(([x,y],j)=>{if(j)b+=`<line x1="${n(row[j-1][0])}" y1="${n(row[j-1][1])}" x2="${n(x)}" y2="${n(y)}" class="s-red" stroke-opacity=".7" stroke-dasharray="3 4"/>`;if(o)b+=`<line x1="${n(rows[o-1][j][0])}" y1="${n(rows[o-1][j][1])}" x2="${n(x)}" y2="${n(y)}" class="s-pap" stroke-opacity=".18"/>`;
  if(r()<.3){const dx=(x-ex),dy=(y-ey),l=Math.hypot(dx,dy);b+=`<line x1="${n(x)}" y1="${n(y)}" x2="${n(ex+dx/l*ER)}" y2="${n(ey+dy/l*ER)}" class="s-pap" stroke-opacity=".16"/>`}}));
 rows.flat().forEach(([x,y])=>b+=`<rect x="${n(x-7)}" y="${n(y-1.5)}" width="14" height="3" class="a-pap" fill-opacity=".8"/><circle cx="${n(x)}" cy="${n(y)}" r="2.6" class="a-red"/>`);return b},
storage(r,W,H){let b=`<rect width="${W}" height="${H}" class="a-ink"/>`;const cols=10,rows=4,gx=W*.06,gy=H*.1,cw=(W-gx*2)/cols,ch=H*.44/rows;
 for(let i=0;i<cols;i++)for(let j=0;j<rows;j++){const v=r();b+=`<rect x="${n(gx+i*cw+3)}" y="${n(gy+j*ch+3)}" width="${n(cw-6)}" height="${n(ch-6)}" class="${v<.22?'a-red':'a-pap'} s-pap" fill-opacity="${v<.22?.85:n(.05+r()*.15)}" stroke-opacity=".35"/>`}
 const y0=H*.92,top=H*.62,pts=[];for(let i=0;i<=48;i++){const t=i/48,v=.5+.38*Math.sin(t*Math.PI*2-1.2)+.06*(r()-.5);pts.push([gx+t*(W-gx*2),y0-v*(y0-top)])}
 const line=pts.map((p,i)=>`${i?'L':'M'}${n(p[0])} ${n(p[1])}`).join('');
 b+=`<line x1="${n(gx)}" x2="${n(W-gx)}" y1="${n(y0)}" y2="${n(y0)}" class="s-pap" stroke-opacity=".3"/><path d="${line}L${n(W-gx)} ${n(y0)}L${n(gx)} ${n(y0)}Z" class="a-red" fill-opacity=".14"/><path d="${line}" fill="none" class="s-red" stroke-width="2"/>`;
 ['00:00','06:00','12:00','18:00','24:00'].forEach((t,i)=>b+=`<text x="${n(gx+i/4*(W-gx*2))}" y="${n(H*.985)}" font-size="${n(H*.035)}" text-anchor="middle" class="a-pap" fill-opacity=".5" style="font-family:var(--f-mono)">${t}</text>`);return b},
tokamak(r,W,H,id){const cx=W*.56,cy=H/2,m=H*.4;let b=`<defs><radialGradient id="tg${id}" cx=".45" cy=".5" r=".6"><stop offset="0" style="stop-color:var(--red)"/><stop offset=".55" style="stop-color:var(--red);stop-opacity:.35"/><stop offset="1" style="stop-color:var(--red);stop-opacity:0"/></radialGradient></defs><rect width="${W}" height="${H}" class="a-ink"/>`;
 const D=s=>{const x0=cx-m*.55*s,xr=cx+m*.95*s;return`M${n(x0)} ${n(cy-m*s)}C${n(xr)} ${n(cy-m*s-m*.08*s)} ${n(xr)} ${n(cy+m*s+m*.08*s)} ${n(x0)} ${n(cy+m*s)}Z`};
 b+=`<rect x="${n(cx-m*1.05)}" y="${n(cy-m*1.1)}" width="${n(m*.2)}" height="${n(m*2.2)}" class="a-pap s-pap" fill-opacity=".1" stroke-opacity=".4"/><path d="${D(1.34)}" fill="none" class="s-pap" stroke-opacity=".14" stroke-width="${n(m*.08)}"/><path d="${D(1.34)}" fill="none" class="s-pap" stroke-opacity=".45"/><path d="${D(1.12)}" fill="none" class="s-pap" stroke-opacity=".75" stroke-width="2"/><path d="${D(.95)}" fill="url(#tg${id})"/>`;
 for(let k=1;k<8;k++)b+=`<path d="${D(.95-k*.11)}" fill="none" class="${k==3?'s-red':'s-pap'}" stroke-opacity="${k==3?.95:.28}"/>`;
 [[-.15,-1.3],[.75,-.95],[1.1,0],[.75,.95],[-.15,1.3]].forEach(([a,c])=>b+=`<rect x="${n(cx+a*m-7)}" y="${n(cy+c*m-7)}" width="14" height="14" class="a-pap" fill-opacity=".6"/>`);
 b+=`<text x="${n(W*.04)}" y="${n(H*.2)}" font-size="${n(H*.04)}" class="a-pap" fill-opacity=".6" style="font-family:var(--f-mono)">Ip 8.7 MA</text><text x="${n(W*.04)}" y="${n(H*.26)}" font-size="${n(H*.04)}" class="a-red" style="font-family:var(--f-mono)">B0 12.2 T</text>`;return b},
portrait(r,W,H,id){const dx=(r()-.5)*24,hs=.92+r()*.16,cx=W/2+dx,hy=H*.37,rx=W*.19*hs,ry=H*.17*hs;
 let b=`<defs><linearGradient id="pb${id}" x2="0" y2="1"><stop offset="0" style="stop-color:var(--paper-hi)"/><stop offset="1" style="stop-color:#7b838f"/></linearGradient><linearGradient id="pf${id}" x2="1" y2="1"><stop offset="0" style="stop-color:#a3aab3"/><stop offset=".5" style="stop-color:#3c434e"/><stop offset="1" style="stop-color:#14181e"/></linearGradient></defs><rect width="${W}" height="${H}" fill="url(#pb${id})"/>`;
 b+=`<path d="M${n(cx-W*.44)} ${H}C${n(cx-W*.42)} ${n(H*.7)} ${n(cx-W*.22)} ${n(H*.64)} ${n(cx)} ${n(H*.64)}C${n(cx+W*.22)} ${n(H*.64)} ${n(cx+W*.42)} ${n(H*.7)} ${n(cx+W*.44)} ${H}Z" fill="url(#pf${id})"/><rect x="${n(cx-W*.07)}" y="${n(hy+ry*.6)}" width="${n(W*.14)}" height="${n(H*.14)}" fill="url(#pf${id})"/><ellipse cx="${n(cx)}" cy="${n(hy)}" rx="${n(rx)}" ry="${n(ry)}" fill="url(#pf${id})"/>`;
 if(r()>.25)b+=`<path d="M${n(cx-rx*1.02)} ${n(hy)}C${n(cx-rx*1.05)} ${n(hy-ry*1.4)} ${n(cx+rx*1.05)} ${n(hy-ry*1.4)} ${n(cx+rx*1.02)} ${n(hy)}C${n(cx+rx*.7)} ${n(hy-ry*.55)} ${n(cx-rx*.6)} ${n(hy-ry*.6)} ${n(cx-rx*1.02)} ${n(hy)}Z" style="fill:#14181e" fill-opacity=".9"/>`;
 return b+`<path d="M${n(cx-W*.1)} ${n(H*.66)}L${n(cx)} ${n(H*.78)}L${n(cx+W*.1)} ${n(H*.66)}" fill="none" class="s-pap" stroke-opacity=".7" stroke-width="3"/>`},
pcb(r,W,H){const g=20;let b=`<rect width="${W}" height="${H}" class="a-ink"/>`;
 for(let t=0;t<34;t++){let x=0,y=Math.round(r()*H/g)*g,d=`M0 ${y}`;const hot=r()<.12;
  while(x<W){x+=g*(2+Math.floor(r()*6));d+=`L${x} ${y}`;if(r()<.6){const s=(r()<.5?-1:1)*g*(1+Math.floor(r()*2));x+=Math.abs(s);y=Math.min(H-g,Math.max(g,y+s));d+=`L${x} ${y}`}}
  b+=`<path d="${d}" fill="none" class="${hot?'s-red':'s-pap'}" stroke-opacity="${hot?.95:n(.12+r()*.22)}" stroke-width="${hot?2.4:1.6}" stroke-linejoin="round"/>`}
 for(let i=0;i<46;i++)b+=`<circle cx="${Math.round(r()*W/g)*g}" cy="${Math.round(r()*H/g)*g}" r="4" class="a-ink s-pap" stroke-opacity=".5"/>`;
 const cs=Math.min(W,H)*.3,cx=W*.55,cy=H*.48;for(let i=0;i<14;i++){const t=-cs/2+cs*(i+.5)/14;b+=`<g class="s-pap" stroke-opacity=".7" stroke-width="2"><line x1="${n(cx+t)}" x2="${n(cx+t)}" y1="${n(cy-cs/2-10)}" y2="${n(cy+cs/2+10)}"/><line y1="${n(cy+t)}" y2="${n(cy+t)}" x1="${n(cx-cs/2-10)}" x2="${n(cx+cs/2+10)}"/></g>`}
 return b+`<rect x="${n(cx-cs/2)}" y="${n(cy-cs/2)}" width="${n(cs)}" height="${n(cs)}" rx="4" style="fill:#1f252e" class="s-pap" stroke-opacity=".6"/><circle cx="${n(cx-cs/2+12)}" cy="${n(cy-cs/2+12)}" r="4" class="a-red"/><text x="${n(cx)}" y="${n(cy+5)}" text-anchor="middle" font-size="${n(cs*.11)}" class="a-pap" fill-opacity=".7" style="font-family:var(--f-mono)">CVL-7</text>`},
depth(r,W,H){const mid=W/2,N=22;let b=`<rect width="${W}" height="${H}" class="a-pap"/>`;for(let k=1;k<5;k++)b+=`<line x1="0" x2="${W}" y1="${n(H*k/5)}" y2="${n(H*k/5)}" class="s-ink" stroke-opacity=".12"/>`;
 const side=dir=>{let y=H*.92,x=mid,p=`M${mid} ${H}`;for(let i=0;i<N;i++){const nx=mid+dir*(i+1)*(mid/N);y=Math.max(H*.08,y-r()*H*.04*(1+i*.06));p+=`L${n(x)} ${n(y)}L${n(nx)} ${n(y)}`;x=nx}return p+`L${n(x)} ${H}Z`};
 return b+`<path d="${side(-1)}" style="fill:#2a313c"/><path d="${side(1)}" class="a-red"/><line x1="${mid}" x2="${mid}" y1="0" y2="${H}" class="s-ink" stroke-dasharray="4 4"/>`},
spectrum(r,W,H){const N=56,bw=W/N,pk=[.18,.41,.66].map(c=>c*N);let b=`<rect width="${W}" height="${H}" class="a-ink"/>`;
 for(let i=0;i<N;i++){let v=.08+r()*.12;pk.forEach((p,j)=>v+=(.75-j*.15)*Math.exp(-((i-p)**2)/(2*(1.6+j)**2)));v=Math.min(.95,v);const h=v*H*.9,hot=pk.some(p=>Math.abs(i-p)<1.2);
  b+=`<rect x="${n(i*bw+bw*.15)}" y="${n(H-h)}" width="${n(bw*.7)}" height="${n(h)}" class="${hot?'a-red':'a-pap'}" fill-opacity="${hot?1:n(.35+v*.6)}"/>`}return b},
contour(r,W,H){let b=`<rect width="${W}" height="${H}" class="a-pap"/>`;
 [[W*.38,H*.45,1.2],[W*.76,H*.66,.75]].forEach(([cx,cy,sc],ci)=>{const p1=r()*6,p2=r()*6;for(let k=1;k<=12;k++){const r0=k*Math.min(W,H)*.045*sc;let d='';
  for(let i=0;i<=72;i++){const t=i/72*Math.PI*2,rr=r0*(1+.16*Math.sin(3*t+p1+k*.15)+.08*Math.sin(5*t+p2));d+=`${i?'L':'M'}${n(cx+rr*Math.cos(t))} ${n(cy+rr*Math.sin(t))}`}
  const hot=ci==0&&k==7;b+=`<path d="${d}Z" fill="none" class="${hot?'s-red':'s-ink'}" stroke-opacity="${hot?1:(k%4==0?.7:.32)}" stroke-width="${hot?2:(k%4==0?1.4:.8)}"/>`}
  b+=`<path d="M${n(cx-6)} ${n(cy)}h12M${n(cx)} ${n(cy-6)}v12" class="s-red" stroke-width="1.5"/>`});return b}
};
document.querySelectorAll('[data-art]').forEach((el,i)=>{const fn=G[el.dataset.art];if(!fn)return;const[W,H]=(el.dataset.vb||'400 400').split(' ').map(Number);
 try{el.innerHTML=`<svg viewBox="0 0 ${W} ${H}" preserveAspectRatio="xMidYMid ${el.dataset.fit||'slice'}" aria-hidden="true" focusable="false">${fn(R(+(el.dataset.seed||i+1)),W,H,i,el.dataset.opt)}</svg>`}catch(e){console.error(e)}});
})();</script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/gsap.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/ScrollTrigger.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/gsap@3.13.0/dist/SplitText.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/lenis@1.3.4/dist/lenis.min.js"></script>
<script>(()=>{const $=(s,r=document)=>r.querySelector(s);const $$=(s,r=document)=>[...r.querySelectorAll(s)];const init=(sel,fn)=>$$(sel).forEach(el=>{try{fn(el)}catch(e){console.error(e)}});const root=document.documentElement;init('[data-head]',head=>{const btn=$('.menu-btn',head),menu=$('[data-menu]',head),close=$('[data-menu-close]',head);const set=open=>{if(!menu)return;menu.classList.toggle('is-open',open);if(btn){btn.setAttribute('aria-expanded',open);btn.setAttribute('aria-label',open?btn.dataset.labelClose||'':btn.dataset.labelOpen||'')}document.body.style.overflow=open?'hidden':'';window.__lenis&&(open?window.__lenis.stop():window.__lenis.start())};btn&&btn.addEventListener('click',()=>set(!menu.classList.contains('is-open')));close&&close.addEventListener('click',()=>set(false));menu&&$$('a',menu).forEach(a=>a.addEventListener('click',()=>set(false)));addEventListener('keydown',e=>{if(e.key==='Escape')set(false)});const cover=$('[data-mast]');let last=scrollY,upFrom=null;const onScroll=()=>{const y=scrollY;head.classList.toggle('is-solid',y>40);if(y<80){head.classList.remove('is-hidden');upFrom=null}else if(y>last){head.classList.add('is-hidden');upFrom=null}else if(y<last){if(upFrom===null)upFrom=last;if(upFrom-y>10)head.classList.remove('is-hidden')}last=y;if(cover)head.classList.toggle('at-cover',cover.getBoundingClientRect().bottom>0);else head.classList.remove('at-cover')};addEventListener('scroll',onScroll,{passive:true});onScroll();const darks=$$('[data-tone="dark"]');if(darks.length&&'IntersectionObserver'in window){const on=new Set;const io=new IntersectionObserver(es=>{es.forEach(e=>e.isIntersecting?on.add(e.target):on.delete(e.target));head.classList.toggle('on-dark',on.size>0)},{rootMargin:`0px 0px -${Math.max(0,innerHeight-40)}px 0px`});darks.forEach(d=>io.observe(d))}});init('[data-proofs]',list=>{[...list.children].forEach((c,i)=>{c.style.setProperty('--i',i);c.style.setProperty('--tilt',(i%2?0.9:-0.7)+'deg')})});init('[data-reg]',fig=>{const k=$('[data-plate-k]',fig);if(!k)return;const r=k.cloneNode(true);r.removeAttribute('data-plate-k');r.classList.remove('reg-plate--k');r.classList.add('reg-plate--r','ht--red');r.setAttribute('aria-hidden','true');const a=$('.art',r);if(a){a.removeAttribute('role');a.removeAttribute('aria-label')}k.after(r);fig.__plateR=r;fig.__marksR=$$('[data-mark-k]',fig).map(m=>{const c=m.cloneNode(true);c.removeAttribute('data-mark-k');c.classList.add('reg-mark--r');m.after(c);return c})});init('[data-bill]',bill=>{const host=bill.closest('section')||document.body;const opts=$$('[data-bill-set]',bill);opts.forEach(o=>o.addEventListener('click',()=>{opts.forEach(x=>x.setAttribute('aria-pressed',x===o));host.setAttribute('data-bill-state',o.dataset.billSet)}))});init('[data-form]',form=>{const status=$('.form-status',form);form.addEventListener('submit',e=>{e.preventDefault();const ok=form.checkValidity();if(status)status.textContent=ok?form.dataset.sent||'':form.dataset.error||'';if(ok)form.reset()})});init('[data-burst-lines]',svg=>{const sec=svg.closest('section')||svg.parentElement;const c=sec&&$('[data-burst-center]',sec);if(!c)return;const NS='http://www.w3.org/2000/svg',n=innerWidth<700?24:38,items=[];for(let i=0;i<n;i++){const l=document.createElementNS(NS,'line');l.setAttribute('pathLength','1');if(i%4===2)l.setAttribute('class','dash');svg.append(l);const dot=i%3===0?document.createElementNS(NS,'circle'):null;if(dot){dot.setAttribute('r','6.5');svg.append(dot)}items.push({l,dot,a:(i+0.35*Math.sin(i*2.1))/n*Math.PI*2})}svg.__burst=items;const draw=()=>{const sr=sec.getBoundingClientRect(),cr=c.getBoundingClientRect();const W=sr.width,H=sr.height,cx=cr.left-sr.left+cr.width/2,cy=cr.top-sr.top+cr.height/2;const rx=cr.width/2+36,ry=cr.height/2+36,R=Math.hypot(Math.max(cx,W-cx),Math.max(cy,H-cy));svg.setAttribute('viewBox','0 0 '+W+' '+H);items.forEach(({l,dot,a},i)=>{const cos=Math.cos(a),sin=Math.sin(a);const r0=1/Math.sqrt(cos*cos/(rx*rx)+sin*sin/(ry*ry));const r1=dot?r0+70+i*53%150:R;l.setAttribute('x1',cx+cos*r0);l.setAttribute('y1',cy+sin*r0);l.setAttribute('x2',cx+cos*r1);l.setAttribute('y2',cy+sin*r1);if(dot){dot.setAttribute('cx',cx+cos*(r1+6.5));dot.setAttribute('cy',cy+sin*(r1+6.5))}})};draw();let t;addEventListener('resize',()=>{clearTimeout(t);t=setTimeout(draw,150)});if(document.fonts)document.fonts.ready.then(draw)});if(!root.classList.contains('motion')||!window.gsap||!window.ScrollTrigger)return;const{gsap,ScrollTrigger}=window;gsap.registerPlugin(ScrollTrigger);if(window.SplitText)gsap.registerPlugin(window.SplitText);let lenis=null;if(window.Lenis){lenis=new window.Lenis({lerp:0.11,smoothWheel:true});window.__lenis=lenis;lenis.on('scroll',ScrollTrigger.update);gsap.ticker.add(t=>lenis.raf(t*1000));gsap.ticker.lagSmoothing(0)}$$('a[href^="#"]').forEach(a=>a.addEventListener('click',e=>{const id=a.getAttribute('href');const t=id.length>1&&document.getElementById(id.slice(1));if(!t||!lenis)return;e.preventDefault();lenis.scrollTo(t,{offset:0,duration:1.4})}));const onNear=(els,fn,margin='0px 0px -12% 0px')=>{if(!els.length)return;const io=new IntersectionObserver(es=>es.forEach(e=>{if(!e.isIntersecting)return;io.unobserve(e.target);try{fn(e.target)}catch(err){console.error(err)}}),{rootMargin:margin});els.forEach(el=>io.observe(el))};onNear($$('[data-reveal]'),el=>{gsap.fromTo(el,{opacity:0,y:36},{opacity:1,y:0,duration:1,ease:'power3.out',clearProps:'transform'})});onNear($$('[data-rule]'),el=>{el.classList.add('ruled');gsap.fromTo(el.children,{opacity:0,y:18},{opacity:1,y:0,duration:0.8,stagger:0.06,ease:'power3.out',clearProps:'transform'})});if(!window.SplitText)$$('[data-split]').forEach(el=>{el.style.visibility='visible'});else document.fonts.ready.then(()=>{onNear($$('[data-split]'),el=>{window.SplitText.create(el,{type:'lines',mask:'lines',autoSplit:true,onSplit:s=>{gsap.set(el,{visibility:'visible'});return gsap.from(s.lines,{yPercent:105,duration:1.05,stagger:0.09,ease:'power4.out'})}})})});init('[data-cover-stage]',stage=>{const art=$('[data-burst]',stage),turn=$('[data-rays-turn]',stage);new IntersectionObserver(es=>es.forEach(e=>stage.classList.toggle('is-off',!e.isIntersecting))).observe(stage);const flyers=art?$$('[data-fly]',art):[];const pin=stage.parentElement;if(!pin||!art)return;const build=()=>{const tl=gsap.timeline({scrollTrigger:{trigger:pin,start:'top top',end:'bottom bottom',scrub:0.6,invalidateOnRefresh:true}});const origin=()=>{const r=art.getBoundingClientRect();return{x:r.left+r.width/2,y:r.top+r.height*0.6}};flyers.forEach((f,i)=>{const vec=()=>{const o=origin(),r=f.getBoundingClientRect();const dx=r.left+r.width/2-o.x,dy=r.top+r.height/2-o.y,d=Math.hypot(dx,dy)||1;return{x:dx/d,y:dy/d}};const k=0.75+i%3*0.2;tl.to(f,{xPercent:()=>vec().x*260*k,yPercent:()=>vec().y*220*k,x:()=>vec().x*innerWidth*0.18*k,y:()=>vec().y*innerHeight*0.2*k,rotation:(i%2?1:-1)*(18+i*5),ease:'power2.in',duration:1},0)});if(turn)tl.to(turn,{rotation:55,scale:1.25,ease:'none',duration:1},0);const archBits=$$('.arch, .arch-line',art);tl.to(archBits,{scale:1.32,transformOrigin:'50% 100%',ease:'power1.inOut',duration:1},0);const lines=$('.cover-lines',art);if(lines)tl.to(lines,{scale:1.35,rotation:-8,ease:'none',duration:1},0);const print=$('[data-print]',art);if(print)tl.to(print,{rotation:0,scale:1.18,yPercent:-6,ease:'power2.inOut',duration:1},0);const head=$('.cover-head',stage);if(head)tl.to(head,{yPercent:-55,ease:'power1.in',duration:1},0);const dands=$$('.dandelion',stage);if(dands.length)tl.to(dands,{opacity:0,y:-60,ease:'power1.in',duration:0.6},0);const chips=$('.cover-chips',stage);if(chips)tl.to(chips,{opacity:0,y:30,duration:0.4},0);const mast=$('[data-mast]',stage);if(mast&&window.SplitText){const split=window.SplitText.create(mast,{type:'chars',charsClass:'mast-ch'});const n=split.chars.length,mid=(n-1)/2;split.chars.forEach((c,i)=>{const off=n>1?(i-mid)/mid:0;tl.to(c,{xPercent:off*150,yPercent:-20-Math.abs(off)*60,rotation:off*22,ease:'power1.inOut',duration:1},0)})}};document.fonts.ready.then(()=>{build();ScrollTrigger.refresh()})});init('[data-reg]',fig=>{const k=$('[data-plate-k]',fig),r=fig.__plateR,marksR=fig.__marksR||[];if(!k||!r)return;const sec=fig.closest('section')||fig;const title=$('[data-reg-title]',sec);const tl=gsap.timeline({scrollTrigger:{trigger:fig,start:'top 85%',end:'center 45%',scrub:0.8}});tl.fromTo(r,{xPercent:-7,yPercent:5,rotation:-2.2},{xPercent:0,yPercent:0,rotation:0,ease:'power2.out',duration:1},0).fromTo(k,{xPercent:4,yPercent:-3},{xPercent:0,yPercent:0,ease:'power2.out',duration:1},0).fromTo(marksR,{x:-26,y:18},{x:0,y:0,ease:'power2.out',duration:1},0);if(title)tl.fromTo(title,{'--mx':'0.09em','--my':'-0.06em'},{'--mx':'0em','--my':'0em',ease:'power2.out',duration:1},0.1)});init('[data-track]',pin=>{const track=$('.work-track',pin);if(!track)return;const cards=[...track.children];cards.forEach((c,i)=>c.style.setProperty('--tilt',(i%2?0.8:-1)+'deg'));const dist=()=>Math.max(0,track.scrollWidth-innerWidth);const setDist=()=>pin.style.setProperty('--dist',dist()+'px');setDist();gsap.to(track,{x:()=>-dist(),ease:'none',scrollTrigger:{trigger:pin,start:'top top',end:()=>'+='+dist(),scrub:0.5,invalidateOnRefresh:true,onRefreshInit:setDist}})});onNear($$('.fig-list'),list=>{const bs=$$('[data-stamp] b',list);gsap.fromTo(bs,{opacity:0,scale:1.45,rotation:-9},{opacity:1,scale:1,rotation:0,duration:0.55,stagger:0.14,ease:'back.out(2.2)',clearProps:'transform'})},'0px 0px -20% 0px');onNear($$('[data-people]'),list=>{const arches=$$('.person-arch',list);list.classList.add('is-in');gsap.fromTo(arches,{clipPath:'inset(100% 0 0 0)'},{clipPath:'inset(0% 0 0 0)',duration:1.3,stagger:0.12,ease:'power3.inOut',clearProps:'clipPath'});gsap.from($$('.person-arch .art',list),{scale:1.18,duration:1.6,stagger:0.12,ease:'power3.out',clearProps:'transform'})},'0px 0px -15% 0px');init('[data-marquee]',mq=>{const track=$('.mq-track',mq);if(!track||!track.children.length)return;[...track.children].forEach(li=>{const c=li.cloneNode(true);c.setAttribute('aria-hidden','true');$$('a, button',c).forEach(x=>x.tabIndex=-1);track.append(c)});const setDur=()=>track.style.setProperty('--mq-dur',Math.max(30,track.scrollWidth/2/38)+'s');setDur();addEventListener('resize',setDur);new IntersectionObserver(es=>es.forEach(e=>mq.classList.toggle('is-off',!e.isIntersecting))).observe(mq)});onNear($$('[data-develop]'),grid=>{$$('.g',grid).forEach((g,i)=>{setTimeout(()=>{g.classList.add('is-in');setTimeout(()=>g.classList.add('is-done'),1400)},i*160)})},'0px 0px -18% 0px');onNear($$('[data-tags]'),list=>{const tags=[...list.children];gsap.fromTo(tags,{opacity:0,y:-70,rotation:i=>i%2?5:-4},{opacity:1,y:0,rotation:0,duration:0.9,stagger:0.13,ease:'back.out(1.6)',clearProps:'transform'})},'0px 0px -15% 0px');init('[data-burst-lines]',svg=>{const items=svg.__burst,sec=svg.closest('section');if(!items||!sec)return;const lines=items.map(x=>x.l),dots=items.map(x=>x.dot).filter(Boolean);const sun=$('[data-sun]',sec);new IntersectionObserver(es=>es.forEach(e=>sec.classList.toggle('is-off',!e.isIntersecting))).observe(sec);const tl=gsap.timeline({scrollTrigger:{trigger:sec,start:'top 80%',end:'center 50%',scrub:0.7}});tl.fromTo(lines,{strokeDasharray:'1 1',strokeDashoffset:1},{strokeDashoffset:0,ease:'power2.out',duration:1,stagger:{each:0.02,from:'random'}},0);if(dots.length)tl.fromTo(dots,{scale:0,transformOrigin:'50% 50%'},{scale:1,ease:'back.out(3)',duration:0.3,stagger:{each:0.03,from:'random'}},0.75);if(sun)tl.fromTo(sun,{yPercent:75},{yPercent:0,ease:'power2.out',duration:1.2},0)})})();</script>
</body>
</html>
```

