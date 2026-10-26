INSTALANDING.AI · Starfork Game Studio Landing Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Starfork Game Studio Landing Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/starfork-game-studio-landing-page

starfork-studio.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Starfork Game Studio Landing Page
  slug     starfork-game-studio-landing-page
  prompt   https://instalanding.ai/p/starfork-game-studio-landing-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/starfork-game-studio-landing-page
  license  MIT. Fictional studio ("Starfork Studio"), games ("Desk Dash!", "Moonmilk", "Paper Comets"), team, numbers
           and open roles. Replace copy and numbers before shipping.

  MAP
  styles    one <style>: page utilities (.btn, .ghost, .stars, .cube, .drift, .twinkle, .ch logo letters, sparks,
            confetti) then the character rig (.spr, poses .a-idle / .a-walk / .a-talk / .a-run / .a-punch / .a-jump /
            .a-death, per-character fidgets .k-pip … .k-tome). Most layout is inline style on the elements.
            Fonts from Google Fonts: Bricolage Grotesque (text), Lilita One (logo, game titles), JetBrains Mono (labels).
  sections  nav, hero, crew, play, games, studio, careers, footer
  loader    <head> adds .sf-wait to <html>: the page (.page) stays hidden under #sf-loader, so the first paint is
            only the loader. Pip runs a track and collects six coins as three signals arrive: the main script's
            'sf:ready' (every character drawn), the display fonts, and window load. It holds at 97% until all
            three are in, plays Pip's victory pose, then .sf-leaving cross-fades to the page. 12s and 15s fallbacks.
  scripts   the loader's own small script, then one inline script, in order:
            1. data: CREW, OBST, QUIZ, ROLES
            2. rig: sprite(el, kind, pose, fps, once, inplace) draws a character from SPR_DEFS + SPR_BODY[kind] with
               its own gradient ids, palette (SF_PAL) and feel (SF_FEEL); poses step whole frames like a sprite sheet,
               --dur = SF_FRAMES[pose] / fps. Any element with data-sprite="kind" data-anim="pose" is drawn on load.
            3. hero: a random cast member throws a punch every 2.6s
            4. crew: a radiogroup of portraits (arrow keys), a preview stage with pose buttons and a frame-rate select,
               stats, and Accept, which puts that character on the start line
            5. play: a 30-second runner (jump with Space, Up, W, a click or a tap), a countdown dial, a six-coin meter,
               desk-clutter obstacles, and fireworks + confetti on the finish
            6. careers: a three-question quiz (Maker / Thinker / Organizer) that ends on an open role
            7. buttons: every data-act="name" button runs ACTS[name]
  assets    none: every character, prop, cube, ring and planet is SVG or CSS; no images, no canvas, no Rive

  ADAPTING
  - The crew lives in CREW (name, role, quote, stats, jump). jump scales the runner's jump a little.
  - A new character needs a palette in SF_PAL, a feel in SF_FEEL and an SVG in SPR_BODY that keeps the rig's
    class names (.bd body, .fl/.fr feet, .sh shadow, .ac accessory, .ey eyes, .xx dead eyes, .mo/.mo2 mouths, .fx).
  - Obstacle types are OBST (size) plus OBST_SVG (art); spawn timing and speed are in loop().
  - The run lasts RUN seconds; collecting all six coins turns the finish into a "Perfect run!" with extra fireworks.
  - Quiz questions are QUIZ; each answer scores maker / thinker / organizer, and ROLES maps the winner to a job.
  - Loader labels live in LABELS in the loader script; its look is the .ld-* rules at the end of the <style>.
  - Reduced motion stops the drifting shapes, twinkles, cubes, logo bob, character poses and the fireworks.
    The runner still plays, because the visitor starts it.
  - Under 1000px the hero shows six of the cast, under 760px four, the nav links hide and the stage gets shorter.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<title>Starfork Studio</title>
<meta name="description" content="Starfork, a fictional nine-person game studio making tiny cosmic games. Meet the crew, play a lap of Desk Dash! in the browser and find your role.">
<script>
  /* Show the loader from the first paint (the page stays hidden under it). Never longer than 15s. */
  document.documentElement.classList.add('sf-wait');
  setTimeout(function () { document.documentElement.classList.remove('sf-wait'); }, 15000);
</script>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:opsz,wght@12..96,400..800&family=JetBrains+Mono:wght@500;700&family=Lilita+One&display=swap" rel="stylesheet">
<style>
body{margin:0;background:#07041a;color:#f4f1ff;font-family:"Bricolage Grotesque",system-ui,sans-serif;-webkit-font-smoothing:antialiased}
a{color:#f4f1ff}a:hover{color:#c9b8ff}
html{scroll-behavior:smooth}
*{box-sizing:border-box}
button{font:inherit;cursor:pointer}
:focus-visible{outline:2px solid #93f7cc;outline-offset:3px}
.stars{background-image:radial-gradient(1.4px 1.4px at 12% 18%,#fff 50%,transparent),radial-gradient(1px 1px at 22% 62%,#fff 50%,transparent),radial-gradient(1.4px 1.4px at 38% 12%,#fff 50%,transparent),radial-gradient(1px 1px at 61% 30%,#fff 50%,transparent),radial-gradient(1.4px 1.4px at 77% 14%,#fff 50%,transparent),radial-gradient(1px 1px at 88% 48%,#fff 50%,transparent),radial-gradient(1px 1px at 8% 44%,#fff 50%,transparent),radial-gradient(1.2px 1.2px at 52% 52%,#fff 50%,transparent),radial-gradient(1px 1px at 70% 66%,#fff 50%,transparent),radial-gradient(1px 1px at 31% 36%,#fff 50%,transparent),radial-gradient(1px 1px at 94% 8%,#fff 50%,transparent),radial-gradient(1px 1px at 4% 82%,#fff 50%,transparent)}
.ch{display:inline-block;background:linear-gradient(172deg,#fff1fa 0%,#ffc3ee 34%,#c9b8ff 64%,#8fb6ff 100%);-webkit-background-clip:text;background-clip:text;color:transparent;animation:letter 3.6s ease-in-out infinite}
@keyframes letter{50%{translate:0 -5px}}
.cast .fig{position:relative;filter:drop-shadow(0 16px 18px rgba(4,2,20,.55))}
.drift{animation:drift 10s ease-in-out infinite}
.drift.d2{animation-delay:-4s;animation-duration:13s}
.drift.d3{animation-delay:-7s;animation-duration:11s}
@keyframes drift{50%{translate:10px -16px;rotate:5deg}}
.twinkle{animation:twinkle 2.8s ease-in-out infinite}
.twinkle.t2{animation-delay:-1s}.twinkle.t3{animation-delay:-1.8s}
@keyframes twinkle{0%,100%{scale:.55;opacity:.4}50%{scale:1;opacity:1}}
.hxc polygon{transform-box:view-box}
.hxc polygon:nth-child(1){transform-origin:50px 50px;animation:hxrot 3.6s linear infinite reverse;animation-delay:var(--d,0s)}
.hxc polygon:nth-child(2){transform-origin:50px 60px;animation:hxrot 3.6s linear infinite;animation-delay:calc(var(--d,0s) - 1.2s)}
.hxc polygon:nth-child(3){transform-origin:40px 40px;animation:hxrot 3.6s linear infinite reverse;animation-delay:var(--d,0s)}
.hxc polygon:nth-child(4){transform-origin:40px 40px;animation:hxrot 3.6s linear infinite reverse;animation-delay:calc(var(--d,0s) - 1.8s)}
.hxc polygon:nth-child(5){transform-origin:60px 40px;animation:hxrot 3.6s linear infinite;animation-delay:var(--d,0s)}
.hxc polygon:nth-child(6){transform-origin:60px 40px;animation:hxrot 3.6s linear infinite;animation-delay:calc(var(--d,0s) - 2.4s)}
@keyframes hxrot{to{transform:rotate(360deg)}}
.cube{transform-style:preserve-3d;animation:cube 16s linear infinite}
.cube i{position:absolute;inset:0;backface-visibility:hidden;border-radius:6px}
@keyframes cube{from{transform:rotateX(-24deg) rotateY(0deg) rotateZ(8deg)}to{transform:rotateX(-24deg) rotateY(360deg) rotateZ(8deg)}}
.spin{animation:spin 80s linear infinite}
@keyframes spin{to{rotate:360deg}}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:10px;min-height:48px;padding:0 24px;border-radius:999px;border:0;font-weight:700;font-size:16px;letter-spacing:-.01em;text-decoration:none;color:#0b0726;background:linear-gradient(180deg,#ffffff,#e6defc);box-shadow:inset 0 -1px 0 rgba(11,7,38,.12),0 1px 0 rgba(255,255,255,.6),0 10px 30px -6px rgba(201,184,255,.55);transition:transform .25s cubic-bezier(.2,.8,.2,1),box-shadow .25s}
.btn:hover{color:#0b0726;transform:translateY(-2px);box-shadow:inset 0 -1px 0 rgba(11,7,38,.12),0 16px 40px -6px rgba(201,184,255,.7)}
.btn:active{transform:translateY(1px)}
.btn[disabled]{opacity:.4;cursor:not-allowed;transform:none}
.ghost{display:inline-flex;align-items:center;justify-content:center;gap:10px;min-height:48px;padding:0 22px;border-radius:999px;font-weight:600;font-size:16px;text-decoration:none;color:#f4f1ff;background:rgba(255,255,255,.05);border:1px solid rgba(255,255,255,.14);backdrop-filter:blur(10px);transition:background .25s,border-color .25s}
.ghost:hover{color:#fff;background:rgba(255,255,255,.1);border-color:rgba(255,255,255,.3)}
.navlink{color:#b9b3e2;text-decoration:none;font-weight:500;font-size:15px;transition:color .2s}
.navlink:hover{color:#fff}
.portrait{transition:transform .3s cubic-bezier(.3,1.5,.5,1),border-color .25s,box-shadow .3s}
.portrait:hover{transform:translateY(-4px)}
.card{transition:transform .45s cubic-bezier(.2,.8,.2,1),border-color .3s,box-shadow .45s}
.card:hover{transform:translateY(-6px);border-color:rgba(201,184,255,.35);box-shadow:0 40px 80px -30px rgba(80,50,220,.55)}
.opt{transition:background .2s,border-color .2s}
.opt:hover{background:rgba(255,255,255,.07)}
.seg{position:relative;display:inline-flex;align-items:center;justify-content:center;min-height:44px;padding:0 14px;border-radius:999px;cursor:pointer;font:600 13px/1 'JetBrains Mono',monospace;letter-spacing:.02em;transition:background .2s,border-color .2s,color .2s}
.seg:hover{background:rgba(255,255,255,.1)}
.seg:has(input:focus-visible){outline:2px solid #93f7cc;outline-offset:2px}
select option{background:#140b4a;color:#f4f1ff}
.popin{animation:popin .55s cubic-bezier(.3,1.5,.5,1)}
@keyframes popin{from{scale:.7;opacity:0;translate:0 14px}}
.coinbob{animation:coinbob 1.4s ease-in-out infinite}
@keyframes coinbob{50%{translate:0 -6px}}
.spark{position:absolute;width:7px;height:7px;border-radius:50%;animation:burst 1s cubic-bezier(.2,.8,.2,1) forwards}
@keyframes burst{to{translate:var(--x) var(--y);scale:.2;opacity:0}}
.conf{position:absolute;top:-20px;width:8px;height:13px;border-radius:2px;animation:fall var(--dur) linear forwards}
@keyframes fall{to{translate:var(--x) 480px;rotate:720deg}}
.toast{transition:transform .4s cubic-bezier(.3,1.5,.5,1),opacity .3s}
.marquee{animation:marq 40s linear infinite}
.pulse{animation:pulse 2.2s ease-in-out infinite}
@keyframes pulse{0%,100%{box-shadow:0 0 0 0 rgba(147,247,204,.55)}50%{box-shadow:0 0 0 6px rgba(147,247,204,0)}}
.toplink{transition:transform .25s cubic-bezier(.2,.8,.2,1),background .25s,border-color .25s}
.toplink:hover{transform:translateY(-3px);background:rgba(255,255,255,.1);border-color:rgba(255,255,255,.3)}
@keyframes marq{to{translate:-50% 0}}
@media (max-width:1000px){.cast .who:nth-child(n+7){display:none}}
@media (max-width:760px){.navlinks{display:none!important}.cast .who{width:78px!important}.cast .who:nth-child(n+5){display:none}.hide-sm{display:none!important}.stage{height:340px!important}.horizon{bottom:-550px!important}}
@media (prefers-reduced-motion:reduce){ .hxc polygon,.pulse,.ch,.drift,.twinkle,.cube,.spin,.coinbob,.marquee,.popin{animation:none!important}html{scroll-behavior:auto}}
[hidden]{display:none!important}

/* ── Loader: a lap of Desk Dash! while the page gets ready ──
   <head> adds .sf-wait to <html>. The page stays hidden (cheap first paint: only
   this screen is drawn) until the characters, fonts and assets are in; then
   .sf-leaving fades the loader out while the page fades in. */
html.sf-wait{overflow:hidden}
html.sf-wait .page{visibility:hidden;opacity:0}
.page{transition:opacity .8s cubic-bezier(.2,.8,.2,1)}
.sf-loader{display:none;position:fixed;inset:0;z-index:100;place-items:center;overflow:hidden;padding:24px 16px;
  background:radial-gradient(90% 70% at 50% 28%,#33219e 0%,#1c1170 38%,#0c0730 72%,#07041a 100%);color:#f4f1ff;text-align:center}
html.sf-wait .sf-loader,html.sf-leaving .sf-loader{display:grid}
html.sf-leaving .sf-loader{opacity:0;transform:scale(1.04);pointer-events:none;transition:opacity .6s ease .1s,transform .7s cubic-bezier(.2,.8,.2,1)}
.ld-glow{position:absolute;border-radius:50%;pointer-events:none}
.ld-planet{position:absolute;left:50%;bottom:calc(120px - 2400px);width:2400px;height:2400px;margin-left:-1200px;border-radius:50%;pointer-events:none;
  background:radial-gradient(circle at 50% 2%,#6a3ad0 0%,#40198f 7%,#1e0c58 20%,#0d0633 40%,#07041a 60%);
  box-shadow:0 -1.5px 0 rgba(255,226,246,.9),0 -18px 60px rgba(255,143,216,.32),0 -60px 140px rgba(125,92,255,.35)}
.ld-inner{position:relative;display:grid;justify-items:center;width:min(560px,100%)}
.ld-pill{display:inline-flex;align-items:center;gap:10px;margin:0 0 18px;padding:7px 14px 7px 8px;border-radius:999px;
  background:rgba(255,255,255,.06);border:1px solid rgba(255,255,255,.12);font:500 13px/1 'JetBrains Mono',monospace;letter-spacing:.04em;color:#e3dcff}
.ld-pill span{padding:4px 8px;border-radius:999px;background:#93f7cc;color:#0b0726;font-weight:700}
.ld-logo{margin:0;font:400 clamp(64px,13vw,128px)/.84 'Lilita One',sans-serif;letter-spacing:.005em;
  filter:drop-shadow(0 8px 0 rgba(10,6,40,.5)) drop-shadow(0 24px 40px rgba(30,12,120,.6))}
.ld-logo>span{display:block}
.ld-track{position:relative;width:100%;height:118px;margin-top:30px}
.ld-ground{position:absolute;left:0;right:0;bottom:0;height:22px;border-radius:12px;
  background:repeating-linear-gradient(90deg,rgba(255,255,255,.08) 0 2px,transparent 2px 32px),linear-gradient(180deg,#4a1d93,#2a0d60);
  box-shadow:inset 0 1px 0 rgba(255,190,236,.75),0 -8px 26px rgba(255,143,216,.18);animation:ld-seams .32s linear infinite}
@keyframes ld-seams{to{background-position:-32px 0,0 0}}
.ld-runner{position:absolute;left:0;bottom:18px;width:78px}
.ld-coin{position:absolute;bottom:62px;width:26px;height:26px;margin-left:-13px;border-radius:50%;
  background:radial-gradient(circle at 50% 50%,#fff6e6 0 52%,#ffb347 54%);box-shadow:0 0 14px rgba(255,179,71,.85);
  animation:coinbob 1.4s ease-in-out infinite;transition:opacity .35s ease,transform .35s cubic-bezier(.3,1.5,.5,1)}
.ld-coin::after{content:"";position:absolute;inset:8px 10px;border-radius:2px;background:#ff8a1f}
.ld-coin.got{opacity:0;transform:translateY(-26px) scale(1.5)}
.ld-row{display:flex;justify-content:space-between;align-items:center;gap:16px;width:100%;margin-top:18px}
.ld-label{font:600 15px/1.2 'Bricolage Grotesque',system-ui,sans-serif;color:#d9d2fb;text-align:left}
.ld-meter{display:flex;gap:6px;padding:7px;border-radius:999px;background:rgba(9,5,34,.6);border:1px solid rgba(255,255,255,.12)}
.ld-meter i{display:block;width:16px;height:20px;border-radius:6px;background:rgba(255,255,255,.08);transition:background .3s,box-shadow .3s}
.ld-meter i.on{background:radial-gradient(circle at 40% 35%,#ffe2b0,#ffb347);box-shadow:0 0 12px rgba(255,179,71,.85)}
.ld-pct{min-width:4ch;font:700 22px/1 'JetBrains Mono',monospace;color:#fff;text-align:right;font-variant-numeric:tabular-nums}
@media (max-width:520px){.ld-meter i{width:12px;height:16px}.ld-label{font-size:13px}.ld-pct{font-size:18px}}
@media (prefers-reduced-motion:reduce){.ld-ground,.ld-coin{animation:none}html.sf-leaving .sf-loader{transform:none}}

/* ── Character rig ── */
.sfc polygon{transform-box:view-box}
.sfc polygon:nth-child(1){transform-origin:50px 50px;animation:sfrot 3.2s linear infinite reverse;animation-delay:var(--d,0s)}
.sfc polygon:nth-child(2){transform-origin:50px 60px;animation:sfrot 3.2s linear infinite;animation-delay:calc(var(--d,0s) - 1.07s)}
.sfc polygon:nth-child(3){transform-origin:40px 40px;animation:sfrot 3.2s linear infinite reverse;animation-delay:var(--d,0s)}
.sfc polygon:nth-child(4){transform-origin:40px 40px;animation:sfrot 3.2s linear infinite reverse;animation-delay:calc(var(--d,0s) - 1.6s)}
.sfc polygon:nth-child(5){transform-origin:60px 40px;animation:sfrot 3.2s linear infinite;animation-delay:var(--d,0s)}
.sfc polygon:nth-child(6){transform-origin:60px 40px;animation:sfrot 3.2s linear infinite;animation-delay:calc(var(--d,0s) - 2.13s)}
@keyframes sfrot{to{transform:rotate(360deg)}}

/* ── Sprite rig: every pose holds for whole frames (steps), like a sprite sheet ── */
.spr .bd,.spr .fl,.spr .fr,.spr .sh,.spr .ac,.spr .ey,.spr .xx,.spr .mo,.spr .mo2,.spr .fx,.spr .tip,.spr .cg,.spr .eg{animation-duration:var(--dur);animation-timing-function:steps(1,end);animation-iteration-count:var(--iter);animation-fill-mode:var(--fill)}
.spr .bd{transform-box:fill-box;transform-origin:50% 100%}
.spr .fl,.spr .fr,.spr .sh,.spr .ey,.spr .fx,.spr .mo2{transform-box:fill-box;transform-origin:50% 50%}
.spr .ac{transform-box:fill-box}
.spr .xx,.spr .mo2,.spr .fx{opacity:0}

/* Idle: shared breath + blink, each crew member has a signature fidget */
.a-idle .bd{animation-name:sf-idle-b}
.a-idle .ey{animation-name:sf-blink}
.a-idle .ac{animation-name:sf-idle-ac}
.k-pip.a-idle .ac{animation-name:sf-twirl}
.k-nib.a-idle .ac{animation-name:sf-hop}
.k-volt.a-idle .tip{animation-name:sf-tip}
.k-volt.a-idle .ac{animation-name:sf-wave}
.k-drip.a-idle .bd{animation-name:sf-jelly}
.k-gem.a-idle .bd{animation-name:sf-rock}
.k-gem.a-idle .ac{animation-name:sf-spin}
.k-puff.a-idle .bd{animation-name:sf-breathe}
.k-kit.a-idle .ac{animation-name:sf-rustle}
.k-tome.a-idle .ac{animation-name:sf-swing}
.k-tome.a-idle .bd{animation-name:sf-rock}

.a-walk .bd{animation-name:sf-walk-b}.a-walk .fl{animation-name:sf-walk-l}.a-walk .fr{animation-name:sf-walk-r}.a-walk .ac{animation-name:sf-walk-ac}.a-walk .sh{animation-name:sf-walk-sh}
.a-run .bd{animation-name:sf-run-b}.a-run .fl{animation-name:sf-run-l}.a-run .fr{animation-name:sf-run-r}.a-run .ac{animation-name:sf-run-ac}.a-run .sh{animation-name:sf-run-sh}
.a-talk .bd{animation-name:sf-talk-b}.a-talk .mo{animation-name:sf-talk-mo}.a-talk .mo2{animation-name:sf-talk-mo2}.a-talk .ac{animation-name:sf-talk-ac}
.a-punch .bd{animation-name:sf-punch-b}.a-punch .ac{animation-name:sf-punch-ac}.a-punch .fx{animation-name:sf-punch-fx}.a-punch .mo{animation-name:sf-punch-mo}.a-punch .mo2{animation-name:sf-punch-mo2}.a-punch .ey{animation-name:sf-punch-ey}.a-punch .fl{animation-name:sf-punch-f}
.a-jump .bd{animation-name:sf-jump-b}.a-jump .fl,.a-jump .fr{animation-name:sf-jump-f}.a-jump .sh{animation-name:sf-jump-sh}.a-jump .ac{animation-name:sf-jump-ac}
.a-death .bd{animation-name:sf-die-b}.a-death .ey{animation-name:sf-die-ey}.a-death .xx{animation-name:sf-die-xx}.a-death .fl,.a-death .fr{animation-name:sf-die-f}.a-death .sh{animation-name:sf-die-sh}
.k-drip.a-death .bd{animation-name:sf-melt}
.k-puff.a-death .bd{animation-name:sf-poof}
.k-volt.a-death .eg,.k-volt.a-death .tip{animation-name:sf-off}

@keyframes sf-idle-b{0%,100%{transform:none}25%,75%{transform:translateY(calc(var(--bob) * -.2px)) scale(calc(1 - var(--sq) * .012),calc(1 + var(--sq) * .018))}50%{transform:translateY(calc(var(--bob) * -.35px)) scale(calc(1 - var(--sq) * .02),calc(1 + var(--sq) * .03))}}
@keyframes sf-blink{0%,100%{transform:none}75%{transform:scaleY(.12)}87.5%{transform:none}}
@keyframes sf-idle-ac{0%,50%,100%{transform:none}25%{transform:rotate(6deg)}75%{transform:rotate(-6deg)}}
@keyframes sf-twirl{0%,100%{transform:none}12.5%{transform:rotate(-10deg)}25%{transform:rotate(-22deg)}37.5%{transform:rotate(-30deg)}50%{transform:rotate(-22deg)}62.5%{transform:rotate(-10deg)}75%{transform:rotate(4deg)}87.5%{transform:rotate(2deg)}}
@keyframes sf-hop{0%,50%,100%{transform:none}25%{transform:translateY(-3px) rotate(-8deg)}75%{transform:translateY(-2px) rotate(5deg)}}
@keyframes sf-tip{0%,25%,100%{opacity:1}50%{opacity:.15}62.5%{opacity:1}75%{opacity:.15}}
@keyframes sf-wave{0%,100%{transform:none}25%{transform:rotate(-16deg)}50%{transform:rotate(-4deg)}62.5%{transform:rotate(-18deg)}75%{transform:none}}
@keyframes sf-jelly{0%,50%,100%{transform:none}12.5%{transform:scale(1.06,.94)}25%{transform:scale(.95,1.06)}37.5%{transform:scale(1.03,.97)}62.5%{transform:scale(1.05,.95)}75%{transform:scale(.97,1.04)}87.5%{transform:none}}
@keyframes sf-rock{0%,50%,100%{transform:none}25%{transform:rotate(4deg)}75%{transform:rotate(-4deg)}}
@keyframes sf-spin{0%{transform:none}25%{transform:rotate(90deg)}50%{transform:rotate(180deg)}75%{transform:rotate(270deg)}100%{transform:rotate(360deg)}}
@keyframes sf-breathe{0%,100%{transform:none}25%,75%{transform:scale(1.04)}50%{transform:translateY(-2px) scale(1.08)}}
@keyframes sf-rustle{0%,50%,100%{transform:none}12.5%{transform:rotate(-10deg)}25%{transform:rotate(8deg)}37.5%{transform:rotate(-4deg)}}
@keyframes sf-swing{0%,50%,100%{transform:none}25%{transform:rotate(14deg)}75%{transform:rotate(-14deg)}}

@keyframes sf-walk-b{0%,50%,100%{transform:translateY(calc(var(--bob) * .3px)) scale(calc(1 + var(--sq) * .04),calc(1 - var(--sq) * .04))}12.5%{transform:translateY(calc(var(--bob) * -.4px)) rotate(calc(var(--lean) * .25deg))}25%{transform:translateY(calc(var(--bob) * -1px)) rotate(calc(var(--lean) * .25deg)) scale(calc(1 - var(--sq) * .03),calc(1 + var(--sq) * .04))}37.5%,87.5%{transform:translateY(calc(var(--bob) * -.4px))}62.5%{transform:translateY(calc(var(--bob) * -.4px)) rotate(calc(var(--lean) * -.25deg))}75%{transform:translateY(calc(var(--bob) * -1px)) rotate(calc(var(--lean) * -.25deg)) scale(calc(1 - var(--sq) * .03),calc(1 + var(--sq) * .04))}}
@keyframes sf-walk-l{0%,100%{transform:translate(6px,0)}12.5%{transform:translate(3px,0)}25%{transform:none}37.5%{transform:translate(-3px,0)}50%{transform:translate(-6px,0)}62.5%{transform:translate(-3px,-3px)}75%{transform:translate(0,-5px)}87.5%{transform:translate(3px,-2px)}}
@keyframes sf-walk-r{0%,100%{transform:translate(-6px,0)}12.5%{transform:translate(-3px,-3px)}25%{transform:translate(0,-5px)}37.5%{transform:translate(3px,-2px)}50%{transform:translate(6px,0)}62.5%{transform:translate(3px,0)}75%{transform:none}87.5%{transform:translate(-3px,0)}}
@keyframes sf-walk-ac{0%,50%,100%{transform:none}25%{transform:rotate(6deg)}75%{transform:rotate(-6deg)}}
@keyframes sf-walk-sh{0%,50%,100%{transform:none}25%,75%{transform:scale(.9)}}

@keyframes sf-run-b{0%,50%,100%{transform:translateY(calc(var(--bob) * .4px)) rotate(calc(var(--lean) * 1deg)) scale(calc(1 + var(--sq) * .06),calc(1 - var(--sq) * .06))}12.5%,62.5%{transform:translateY(calc(var(--bob) * -1.2px)) rotate(calc(var(--lean) * 1deg)) scale(calc(1 - var(--sq) * .04),calc(1 + var(--sq) * .06))}25%,75%{transform:translateY(calc(var(--bob) * -2px)) rotate(calc(var(--lean) * 1deg))}37.5%,87.5%{transform:translateY(calc(var(--bob) * -1px)) rotate(calc(var(--lean) * 1deg))}}
@keyframes sf-run-l{0%,100%{transform:translate(10px,0)}12.5%{transform:translate(4px,0)}25%{transform:translate(-4px,0)}37.5%{transform:translate(-10px,-1px)}50%{transform:translate(-8px,-8px)}62.5%{transform:translate(0,-10px)}75%{transform:translate(8px,-6px)}87.5%{transform:translate(11px,-2px)}}
@keyframes sf-run-r{0%,100%{transform:translate(-8px,-8px)}12.5%{transform:translate(0,-10px)}25%{transform:translate(8px,-6px)}37.5%{transform:translate(11px,-2px)}50%{transform:translate(10px,0)}62.5%{transform:translate(4px,0)}75%{transform:translate(-4px,0)}87.5%{transform:translate(-10px,-1px)}}
@keyframes sf-run-ac{0%,50%,100%{transform:rotate(-14deg)}25%,75%{transform:rotate(-22deg)}}
@keyframes sf-run-sh{0%,50%,100%{transform:none}25%,75%{transform:scale(.8)}}

@keyframes sf-talk-b{0%,25%,50%,87.5%,100%{transform:none}12.5%{transform:translateY(-1px) rotate(-2deg)}37.5%{transform:translateY(-2px) rotate(2deg)}62.5%{transform:translateY(-1px)}75%{transform:rotate(-1deg)}}
@keyframes sf-talk-mo{0%,25%,62.5%,87.5%,100%{opacity:1}12.5%,37.5%,50%,75%{opacity:0}}
@keyframes sf-talk-mo2{0%,25%,62.5%,87.5%,100%{opacity:0;transform:none}12.5%{opacity:1;transform:scale(.8,.7)}37.5%{opacity:1;transform:scale(1.15,1.25)}50%{opacity:1;transform:scale(1,.9)}75%{opacity:1;transform:scale(.9,.8)}}
@keyframes sf-talk-ac{0%,100%{transform:none}25%{transform:rotate(-12deg)}50%{transform:rotate(8deg)}75%{transform:rotate(-6deg)}}

@keyframes sf-punch-b{0%,87.5%,100%{transform:none}12.5%{transform:translateX(-3px) rotate(calc(var(--lean) * -1deg)) scale(calc(1 + var(--sq) * .05),calc(1 - var(--sq) * .05))}25%{transform:translateX(-5px) rotate(calc(var(--lean) * -1.5deg)) scale(calc(1 + var(--sq) * .07),calc(1 - var(--sq) * .07))}37.5%{transform:translateX(9px) rotate(calc(var(--lean) * 1.6deg)) scale(calc(1 - var(--sq) * .05),calc(1 + var(--sq) * .05))}50%{transform:translateX(10px) rotate(calc(var(--lean) * 1.4deg))}62.5%{transform:translateX(7px) rotate(calc(var(--lean) * .8deg))}75%{transform:translateX(3px) rotate(calc(var(--lean) * .3deg))}}
@keyframes sf-punch-ac{0%,87.5%,100%{transform:none}12.5%{transform:rotate(-30deg)}25%{transform:rotate(-48deg)}37.5%{transform:rotate(38deg)}50%{transform:rotate(52deg)}62.5%{transform:rotate(30deg)}75%{transform:rotate(10deg)}}
@keyframes sf-punch-fx{0%,25%{opacity:0;transform:scale(.3)}37.5%{opacity:1;transform:scale(.75)}50%{opacity:1;transform:scale(1.1)}62.5%{opacity:.8;transform:scale(1.3)}75%{opacity:.35;transform:scale(1.45)}87.5%,100%{opacity:0;transform:scale(1.5)}}
@keyframes sf-punch-mo{0%,25%,75%,100%{opacity:1}37.5%,50%,62.5%{opacity:0}}
@keyframes sf-punch-mo2{0%,25%,75%,100%{opacity:0;transform:none}37.5%,50%,62.5%{opacity:1;transform:scale(1.1,1.2)}}
@keyframes sf-punch-ey{0%,12.5%,37.5%,100%{transform:none}25%{transform:scaleY(.45)}}
@keyframes sf-punch-f{0%,25%,75%,100%{transform:none}37.5%,50%,62.5%{transform:translateX(6px)}}

@keyframes sf-jump-b{0%{transform:translateY(calc(var(--bob) * .4px)) scale(calc(1 + var(--sq) * .12),calc(1 - var(--sq) * .14))}12.5%{transform:translateY(calc(var(--jy) * -14px)) scale(calc(1 - var(--sq) * .08),calc(1 + var(--sq) * .14))}25%{transform:translateY(calc(var(--jy) * -28px)) scale(calc(1 - var(--sq) * .04),calc(1 + var(--sq) * .07))}37.5%{transform:translateY(calc(var(--jy) * -34px)) rotate(calc(var(--lean) * -.8deg))}50%{transform:translateY(calc(var(--jy) * -32px)) rotate(calc(var(--lean) * -1deg))}62.5%{transform:translateY(calc(var(--jy) * -18px)) scale(calc(1 - var(--sq) * .04),calc(1 + var(--sq) * .08))}75%{transform:translateY(calc(var(--bob) * .5px)) scale(calc(1 + var(--sq) * .14),calc(1 - var(--sq) * .16))}87.5%{transform:translateY(calc(var(--bob) * .1px)) scale(calc(1 + var(--sq) * .04),calc(1 - var(--sq) * .04))}100%{transform:none}}
@keyframes sf-jump-f{0%,75%,100%{transform:none}12.5%{transform:translateY(calc(var(--jy) * -12px))}25%{transform:translateY(calc(var(--jy) * -26px - 3px))}37.5%{transform:translateY(calc(var(--jy) * -34px - 6px))}50%{transform:translateY(calc(var(--jy) * -32px - 5px))}62.5%{transform:translateY(calc(var(--jy) * -18px - 2px))}}
@keyframes sf-jump-sh{0%,75%,100%{transform:none}12.5%{transform:scale(calc(1 - var(--jy) * .2))}25%,37.5%,50%{transform:scale(calc(1 - var(--jy) * .45))}62.5%{transform:scale(calc(1 - var(--jy) * .25))}}
@keyframes sf-jump-ac{0%,87.5%,100%{transform:none}25%{transform:rotate(-14deg)}50%{transform:rotate(-20deg)}75%{transform:rotate(6deg)}}

@keyframes sf-die-b{0%{transform:translate(-3px,-3px) rotate(-6deg)}12.5%{transform:translate(-4px,-8px) rotate(-12deg)}25%{transform:translate(2px,-6px) rotate(14deg)}37.5%{transform:translate(8px,0) rotate(48deg)}50%{transform:translate(14px,6px) rotate(80deg)}62.5%{transform:translate(16px,10px) rotate(94deg) scale(1.03,.97)}75%{transform:translate(16px,9px) rotate(88deg)}87.5%,100%{transform:translate(16px,10px) rotate(90deg)}}
@keyframes sf-die-ey{0%{opacity:1}12.5%,100%{opacity:0}}
@keyframes sf-die-xx{0%{opacity:0}12.5%,100%{opacity:1}}
@keyframes sf-die-f{0%,25%{transform:none}37.5%{transform:translate(4px,-2px)}62.5%,100%{transform:translate(6px,0) scale(.8)}}
@keyframes sf-die-sh{0%,25%{transform:none}50%,100%{transform:scale(1.35,1)}}
@keyframes sf-melt{0%{transform:translateY(-3px) scale(.96,1.05)}12.5%{transform:scale(1.06,.94)}25%{transform:scale(1.2,.8)}37.5%{transform:scale(1.4,.62)}50%{transform:scale(1.6,.46)}62.5%{transform:scale(1.75,.34)}75%{transform:scale(1.85,.28)}87.5%,100%{transform:scale(1.9,.24)}}
@keyframes sf-poof{0%{transform:scale(1.04);opacity:1}12.5%{transform:scale(1.12);opacity:1}25%{transform:scale(1.22);opacity:.85}37.5%{transform:scale(1.32);opacity:.6}50%{transform:scale(1.42);opacity:.35}62.5%{transform:scale(1.5);opacity:.15}75%,100%{transform:scale(1.55);opacity:0}}
@keyframes sf-off{0%{opacity:1}12.5%{opacity:.3}25%{opacity:1}37.5%,100%{opacity:0}}

@media (prefers-reduced-motion:reduce){.sfc polygon,.spr .bd,.spr .fl,.spr .fr,.spr .sh,.spr .ac,.spr .ey,.spr .mo,.spr .mo2,.spr .fx,.spr .tip,.spr .cg,.spr .eg{animation:none!important}}
</style>
</head>
<body>
<div class="sf-loader" id="sf-loader">
<div class="stars" aria-hidden="true" style="position: absolute; inset: 0; opacity: 0.75;"></div>
<div class="ld-glow" aria-hidden="true" style="left: -12%; top: -18%; width: 620px; height: 620px; background: radial-gradient(closest-side, rgba(255, 143, 216, 0.28), transparent);"></div>
<div class="ld-glow" aria-hidden="true" style="right: -10%; top: -6%; width: 720px; height: 720px; background: radial-gradient(closest-side, rgba(110, 140, 255, 0.3), transparent);"></div>
<div class="ld-planet" aria-hidden="true"></div>
<div class="ld-inner">
<p class="ld-pill"><span>NEW</span>Starfork Studio presents</p>
<div class="ld-logo" aria-hidden="true"><span aria-hidden="true" style="display: block;">
<span class="ch" style="transform: translateY(0px) rotate(-3deg); animation-delay: 0.00s;">D</span><span class="ch" style="transform: translateY(-6px) rotate(2deg); animation-delay: -0.18s;">e</span><span class="ch" style="transform: translateY(4px) rotate(-1deg); animation-delay: -0.36s;">s</span><span class="ch" style="transform: translateY(-3px) rotate(3deg); animation-delay: -0.54s;">k</span>
</span>
<span aria-hidden="true" style="display: block;">
<span class="ch" style="transform: translateY(-6px) rotate(-1deg); animation-delay: -0.40s;">D</span><span class="ch" style="transform: translateY(4px) rotate(3deg); animation-delay: -0.58s;">a</span><span class="ch" style="transform: translateY(-3px) rotate(-2deg); animation-delay: -0.76s;">s</span><span class="ch" style="transform: translateY(5px) rotate(-3deg); animation-delay: -0.94s;">h</span><span class="ch" style="background-image: linear-gradient(172deg, #eef4ff, #9dbcff 55%, #7fa5ff);transform: translateY(0px) rotate(2deg); animation-delay: -1.12s;">!</span>
</span></div>
<div class="ld-track" aria-hidden="true">
<span class="ld-coin"></span><span class="ld-coin"></span><span class="ld-coin"></span><span class="ld-coin"></span><span class="ld-coin"></span><span class="ld-coin"></span>
<div class="ld-ground"></div>
<div class="ld-runner" id="ld-runner"><div data-sprite="pip" data-anim="run"></div></div>
</div>
<div class="ld-row">
<span class="ld-label" id="ld-label" role="status">Waking the crew…</span>
<span class="ld-meter" aria-hidden="true"><i></i><i></i><i></i><i></i><i></i><i></i></span>
<b class="ld-pct" id="ld-pct" aria-hidden="true">0%</b>
</div>
</div>
</div>
<script>
  /* Loader. Pip runs the track as the page gets ready and collects a coin every sixth of the way.
     Real progress comes from three signals: the main script has drawn every character ('sf:ready'),
     the display fonts are in, and the page's load event. The bar also creeps on its own so it never
     looks stuck, holds at 97% until all three are in, and gives up after 12 seconds. */
  (function () {
    var d = document.documentElement;
    if (!d.classList.contains('sf-wait')) return;
    var $ = function (id) { return document.getElementById(id); };
    var runner = $('ld-runner'), pct = $('ld-pct'), label = $('ld-label');
    var coins = document.querySelectorAll('.ld-coin'), slots = document.querySelectorAll('.ld-meter i');
    var have = { script: false, fonts: false, load: false }, shown = 0, t0 = performance.now(), done = false;
    var LABELS = [[0, 'Waking the crew…'], [30, 'Polishing the cubes…'], [55, 'Stacking the desk clutter…'], [80, 'Tuning the jump…']];
    var reduced = window.matchMedia && matchMedia('(prefers-reduced-motion: reduce)').matches;

    for (var i = 0; i < coins.length; i++) coins[i].style.left = 'calc(39px + (100% - 78px) * ' + ((i + 0.5) / coins.length).toFixed(4) + ')';
    function real() { return 10 + (have.script ? 40 : 0) + (have.fonts ? 30 : 0) + (have.load ? 20 : 0); }
    document.addEventListener('sf:ready', function () { have.script = true; });
    window.addEventListener('load', function () { have.load = true; });
    var f = document.fonts;
    if (f && f.load) Promise.all([f.load('400 64px "Lilita One"'), f.load('700 40px "Bricolage Grotesque"'), f.load('500 13px "JetBrains Mono"')])
      .then(function () { return f.ready; }, function () {}).then(function () { have.fonts = true; });
    else have.fonts = true;

    function paint(v) {
      runner.style.left = 'calc((100% - 78px) * ' + (v / 100).toFixed(4) + ')';
      pct.textContent = Math.round(v) + '%';
      for (var i = 0; i < coins.length; i++) {
        var got = v / 100 >= (i + 0.5) / coins.length;
        coins[i].classList.toggle('got', got);
        slots[i].classList.toggle('on', got);
      }
      if (v < 100) for (var j = LABELS.length - 1; j >= 0; j--) if (v >= LABELS[j][0]) { label.textContent = LABELS[j][1]; break; }
    }
    function finish() {
      done = true;
      paint(100);
      label.textContent = 'Ready!';
      var fig = runner.firstElementChild;
      if (window.SF_SPRITE && fig) window.SF_SPRITE(fig, 'pip', 'punch', 12, true);
      setTimeout(function () {
        d.classList.add('sf-leaving');
        d.classList.remove('sf-wait');
        setTimeout(function () { d.classList.remove('sf-leaving'); $('sf-loader').remove(); }, 800);
      }, reduced ? 120 : 560);
    }
    function tick(now) {
      if (done) return;
      var target = real() >= 100 ? 100 : Math.min(97, Math.max(real(), 70 * (1 - Math.exp(-(now - t0) / 1600))));
      shown += (target - shown) * (target >= 100 ? 0.16 : 0.06);
      paint(shown);
      if (target >= 100 && shown > 99.5 && now - t0 > (reduced ? 0 : 900)) return finish();
      requestAnimationFrame(tick);
    }
    requestAnimationFrame(tick);
    setTimeout(function () { if (!done) { have.script = have.fonts = have.load = true; } }, 12000);
  })();
</script>
<div class="page" style="position: relative; overflow-x: clip; background: #07041a;">

<!-- NAV -->
<header data-section="nav" style="position: fixed; top: 14px; left: 0; right: 0; z-index: 30; display: flex; justify-content: center; padding: 0 16px;">
<nav aria-label="Primary" style="width: 100%; max-width: 1120px; display: flex; align-items: center; justify-content: space-between; gap: 16px; padding: 8px 8px 8px 18px; border-radius: 999px; background: rgba(13, 9, 40, 0.62); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06), 0 20px 50px -20px rgba(0, 0, 0, 0.6); backdrop-filter: blur(18px) saturate(140%);">
<a href="#top" aria-label="Starfork Studio home" style="display: flex; align-items: center; gap: 10px; text-decoration: none; font-weight: 700; font-size: 18px; letter-spacing: -0.02em;">
<svg width="30" height="30" viewBox="0 0 40 40" aria-hidden="true"><circle cx="20" cy="20" r="19" fill="#6a48ff"></circle><path d="M20 7l2.8 8.4H31l-6.6 5 2.6 8.3L20 23.6l-7 5.1 2.6-8.3-6.6-5h8.2z" fill="#ffe7f6"></path><circle cx="31" cy="9" r="4" fill="#93f7cc"></circle></svg>
Starfork
</a>
<div class="navlinks" style="display: flex; gap: 30px;">
<a class="navlink" href="#crew">Crew</a>
<a class="navlink" href="#play">Play</a>
<a class="navlink" href="#games">Games</a>
<a class="navlink" href="#studio">Studio</a>
<a class="navlink" href="#careers">Careers</a>
</div>
<a class="btn" href="#play" style="min-height: 42px; padding: 0 18px; font-size: 14px;">Play the demo</a>
</nav>
</header>

<!-- HERO -->
<section id="top" data-section="hero" style="position: relative; min-height: 100vh; overflow-x: clip; overflow-y: visible; isolation: isolate; background: radial-gradient(90% 70% at 50% 28%, #33219e 0%, #1c1170 38%, #0c0730 72%, #07041a 100%);">
<div aria-hidden="true" style="position: absolute; inset: 0; z-index: -1; pointer-events: none;">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.75;"></div>
<div style="position: absolute; left: -12%; top: -18%; width: 620px; height: 620px; border-radius: 50%; background: radial-gradient(closest-side, rgba(255, 143, 216, 0.28), transparent);"></div>
<div style="position: absolute; right: -10%; top: -6%; width: 720px; height: 720px; border-radius: 50%; background: radial-gradient(closest-side, rgba(110, 140, 255, 0.3), transparent);"></div>
<svg width="0" height="0" aria-hidden="true" style="position: absolute; width: 0; height: 0; overflow: hidden;"><defs><filter id="hx-goo" x="-30%" y="-30%" width="160%" height="160%"><feGaussianBlur stdDeviation="7"></feGaussianBlur><feColorMatrix type="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6"><animate attributeName="values" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 4 -1.2;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 4 -1.2;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6" keyTimes="0;.2;.4;.6;1" dur="1.8s" repeatCount="indefinite"></animate></feColorMatrix></filter></defs></svg>
<div class="drift" style="position: absolute; left: 7%; top: 19%;"><svg width="124" height="124" viewBox="0 0 120 120" style="display: block; overflow: visible; filter: drop-shadow(0 0 16px #a8ffd955) drop-shadow(0 18px 30px #1f9c7466);">
<defs>
<linearGradient id="hxa-body" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#71d7b1"></stop><stop offset="1" stop-color="#1f9c74"></stop></linearGradient>
<linearGradient id="hxa-dark" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#1f9c74"></stop><stop offset="1" stop-color="#06301f"></stop></linearGradient>
<linearGradient id="hxa-core" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="0" y2="100"><stop offset=".3" stop-color="#a8ffd9"><animate attributeName="stop-color" values="#a8ffd9;#a8ffad;#ceffa8;#faffa8;#b8ffa8;#a8ffd9" dur="7s" begin="-0.8s" repeatCount="indefinite"></animate></stop><stop offset=".7" stop-color="#1f9c74"><animate attributeName="stop-color" values="#1f9c74;#1f9c35;#479c1f;#869c1f;#289c1f;#1f9c74" dur="7s" begin="-0.8s" repeatCount="indefinite"></animate></stop></linearGradient>
<linearGradient id="hxa-rim" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#a8ffd9"></stop><stop offset=".45" stop-color="#a8ffd9" stop-opacity="0"></stop><stop offset=".7" stop-color="#1f9c74" stop-opacity="0"></stop><stop offset="1" stop-color="#1f9c74"></stop></linearGradient>
<radialGradient id="hxa-sheen" cx=".34" cy=".14" r=".72"><stop offset="0" stop-color="#ffffff" stop-opacity=".62"></stop><stop offset=".35" stop-color="#ffffff" stop-opacity=".14"></stop><stop offset=".6" stop-color="#ffffff" stop-opacity="0"></stop></radialGradient>
<radialGradient id="hxa-glow"><stop offset=".4" stop-color="#a8ffd9" stop-opacity=".6"></stop><stop offset="1" stop-color="#a8ffd9" stop-opacity="0"></stop></radialGradient>
<mask id="hxa-m" maskUnits="userSpaceOnUse" x="-20" y="-20" width="140" height="140"><g class="hxc" filter="url(#hx-goo)" fill="#ffffff" style="--d: -0.8s;"><polygon points="25,25 75,25 50,75"></polygon><polygon points="50,25 75,75 25,75"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon></g></mask>
<mask id="hxa-lens" maskUnits="userSpaceOnUse" x="-40" y="-40" width="280" height="200"><g fill="#ffffff" stroke="none"><path d="M60 32l22 13v38l-22 13-22-13V45z"></path></g></mask>
</defs>
<path d="M60 8l38 22v60l-38 22-38-22V30z" fill="url(#hxa-body)"></path>
<path d="M60 8l38 22-38 22-38-22z" fill="#ffffff" opacity=".22"></path>
<path d="M22 30l38 22v60L22 90z" fill="#000000" opacity=".16"></path>
<path d="M22 30l38 22 38-22M60 52v60" fill="none" stroke="#ffffff" stroke-opacity=".35" stroke-width="1"></path>
<path d="M60 8l38 22v60l-38 22-38-22V30z" fill="url(#hxa-sheen)"></path>
<path d="M60 8l38 22v60l-38 22-38-22V30z" fill="none" stroke="url(#hxa-rim)" stroke-width="1.6" stroke-linejoin="round"></path>





</svg></div>
<div class="drift d2 hide-sm" style="position: absolute; left: -36px; top: 50%;"><svg width="220" viewBox="0 0 200 120" style="display: block; overflow: visible; rotate: -16deg; filter: drop-shadow(0 0 16px #ffb3f055) drop-shadow(0 18px 30px #9b3fd666);">
<defs>
<linearGradient id="hxb-body" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#d785e6"></stop><stop offset="1" stop-color="#9b3fd6"></stop></linearGradient>
<linearGradient id="hxb-dark" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#9b3fd6"></stop><stop offset="1" stop-color="#2c0a4a"></stop></linearGradient>
<linearGradient id="hxb-core" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="0" y2="100"><stop offset=".3" stop-color="#ffb3f0"><animate attributeName="stop-color" values="#ffb3f0;#e8b3ff;#c2b3ff;#b3caff;#d5b3ff;#ffb3f0" dur="7s" begin="-2.1s" repeatCount="indefinite"></animate></stop><stop offset=".7" stop-color="#9b3fd6"><animate attributeName="stop-color" values="#9b3fd6;#4f3fd6;#3f7ad6;#3fc6d6;#3f54d6;#9b3fd6" dur="7s" begin="-2.1s" repeatCount="indefinite"></animate></stop></linearGradient>
<linearGradient id="hxb-rim" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffb3f0"></stop><stop offset=".45" stop-color="#ffb3f0" stop-opacity="0"></stop><stop offset=".7" stop-color="#9b3fd6" stop-opacity="0"></stop><stop offset="1" stop-color="#9b3fd6"></stop></linearGradient>
<radialGradient id="hxb-sheen" cx=".34" cy=".14" r=".72"><stop offset="0" stop-color="#ffffff" stop-opacity=".62"></stop><stop offset=".35" stop-color="#ffffff" stop-opacity=".14"></stop><stop offset=".6" stop-color="#ffffff" stop-opacity="0"></stop></radialGradient>
<radialGradient id="hxb-glow"><stop offset=".4" stop-color="#ffb3f0" stop-opacity=".6"></stop><stop offset="1" stop-color="#ffb3f0" stop-opacity="0"></stop></radialGradient>
<mask id="hxb-m" maskUnits="userSpaceOnUse" x="-20" y="-20" width="140" height="140"><g class="hxc" filter="url(#hx-goo)" fill="#ffffff" style="--d: -2.1s;"><polygon points="25,25 75,25 50,75"></polygon><polygon points="50,25 75,75 25,75"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon></g></mask>
<mask id="hxb-tube" maskUnits="userSpaceOnUse" x="-40" y="-40" width="280" height="200"><g fill="#ffffff" stroke="none"><path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z"></path></g></mask>
</defs>
<path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="#2c0a4a" transform="translate(0 9)"></path>
<path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="url(#hxb-dark)"></path>
<g mask="url(#hxb-tube)"><rect x="0" y="0" width="100" height="100" fill="url(#hxb-core)" mask="url(#hxb-m)" transform="translate(-30 -44) scale(2.6 1.6)"></rect></g>
<path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="url(#hxb-sheen)"></path>
<path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="none" stroke="url(#hxb-rim)" stroke-width="1.6"></path>
<path d="M30 48c22-16 70-22 112-14" fill="none" stroke="#ffffff" stroke-width="3" stroke-linecap="round" opacity=".55"></path>
<path d="M120 80c14-2 26-6 34-12" fill="none" stroke="#ffb3f0" stroke-width="1.5" stroke-linecap="round" opacity=".6"></path>
</svg></div>
<div class="drift d3 hide-sm" style="position: absolute; left: 25%; top: 33%;"><svg width="50" height="50" viewBox="0 0 120 120" style="display: block; overflow: visible; filter: drop-shadow(0 0 16px #a9d4ff55) drop-shadow(0 18px 30px #3557d866);">
<defs>
<linearGradient id="hxd-body" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#7ba2ef"></stop><stop offset="1" stop-color="#3557d8"></stop></linearGradient>
<linearGradient id="hxd-dark" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#3557d8"></stop><stop offset="1" stop-color="#0b1858"></stop></linearGradient>
<linearGradient id="hxd-core" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="0" y2="100"><stop offset=".3" stop-color="#a9d4ff"><animate attributeName="stop-color" values="#a9d4ff;#a9ffff;#a9ffd4;#a9ffa9;#a9ffea;#a9d4ff" dur="7s" begin="-2.7s" repeatCount="indefinite"></animate></stop><stop offset=".7" stop-color="#3557d8"><animate attributeName="stop-color" values="#3557d8;#35a8d8;#35d8b6;#35d865;#35d1d8;#3557d8" dur="7s" begin="-2.7s" repeatCount="indefinite"></animate></stop></linearGradient>
<linearGradient id="hxd-rim" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#a9d4ff"></stop><stop offset=".45" stop-color="#a9d4ff" stop-opacity="0"></stop><stop offset=".7" stop-color="#3557d8" stop-opacity="0"></stop><stop offset="1" stop-color="#3557d8"></stop></linearGradient>
<radialGradient id="hxd-sheen" cx=".34" cy=".14" r=".72"><stop offset="0" stop-color="#ffffff" stop-opacity=".62"></stop><stop offset=".35" stop-color="#ffffff" stop-opacity=".14"></stop><stop offset=".6" stop-color="#ffffff" stop-opacity="0"></stop></radialGradient>
<radialGradient id="hxd-glow"><stop offset=".4" stop-color="#a9d4ff" stop-opacity=".6"></stop><stop offset="1" stop-color="#a9d4ff" stop-opacity="0"></stop></radialGradient>
<mask id="hxd-m" maskUnits="userSpaceOnUse" x="-20" y="-20" width="140" height="140"><g class="hxc" filter="url(#hx-goo)" fill="#ffffff" style="--d: -2.7s;"><polygon points="25,25 75,25 50,75"></polygon><polygon points="50,25 75,75 25,75"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon></g></mask>
<mask id="hxd-lens" maskUnits="userSpaceOnUse" x="-40" y="-40" width="280" height="200"><g fill="#ffffff" stroke="none"><circle cx="60" cy="60" r="44"></circle></g></mask>
</defs>
<circle cx="60" cy="60" r="44" fill="url(#hxd-dark)"></circle>
<g mask="url(#hxd-lens)"><rect x="0" y="0" width="100" height="100" fill="url(#hxd-core)" mask="url(#hxd-m)" transform="translate(6 6) scale(1.08)"></rect></g>
<circle cx="60" cy="60" r="44" fill="url(#hxd-sheen)"></circle>
<circle cx="60" cy="60" r="44" fill="none" stroke="url(#hxd-rim)" stroke-width="2"></circle>
<ellipse cx="44" cy="36" rx="12" ry="6" fill="#ffffff" opacity=".7" transform="rotate(-28 44 36)"></ellipse>
<circle cx="80" cy="82" r="3" fill="#ffffff" opacity=".6"></circle>
</svg></div>
<div class="drift d2 hide-sm" style="position: absolute; right: 19%; top: 12%;"><svg width="62" height="62" viewBox="0 0 120 120" style="display: block; overflow: visible; filter: drop-shadow(0 0 16px #ffd27a55) drop-shadow(0 18px 30px #c2611a66);">
<defs>
<linearGradient id="hxc-body" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#e7a554"></stop><stop offset="1" stop-color="#c2611a"></stop></linearGradient>
<linearGradient id="hxc-dark" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#c2611a"></stop><stop offset="1" stop-color="#3d1504"></stop></linearGradient>
<linearGradient id="hxc-core" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="0" y2="100"><stop offset=".3" stop-color="#ffd27a"><animate attributeName="stop-color" values="#ffd27a;#ff907a;#ff7aa7;#ff7ae9;#ff7a86;#ffd27a" dur="7s" begin="-1.4s" repeatCount="indefinite"></animate></stop><stop offset=".7" stop-color="#c2611a"><animate attributeName="stop-color" values="#c2611a;#c21a27;#c21a7b;#b51ac2;#c21a51;#c2611a" dur="7s" begin="-1.4s" repeatCount="indefinite"></animate></stop></linearGradient>
<linearGradient id="hxc-rim" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#ffd27a"></stop><stop offset=".45" stop-color="#ffd27a" stop-opacity="0"></stop><stop offset=".7" stop-color="#c2611a" stop-opacity="0"></stop><stop offset="1" stop-color="#c2611a"></stop></linearGradient>
<radialGradient id="hxc-sheen" cx=".34" cy=".14" r=".72"><stop offset="0" stop-color="#ffffff" stop-opacity=".62"></stop><stop offset=".35" stop-color="#ffffff" stop-opacity=".14"></stop><stop offset=".6" stop-color="#ffffff" stop-opacity="0"></stop></radialGradient>
<radialGradient id="hxc-glow"><stop offset=".4" stop-color="#ffd27a" stop-opacity=".6"></stop><stop offset="1" stop-color="#ffd27a" stop-opacity="0"></stop></radialGradient>
<mask id="hxc-m" maskUnits="userSpaceOnUse" x="-20" y="-20" width="140" height="140"><g class="hxc" filter="url(#hx-goo)" fill="#ffffff" style="--d: -1.4s;"><polygon points="25,25 75,25 50,75"></polygon><polygon points="50,25 75,75 25,75"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon></g></mask>
<mask id="hxc-lens" maskUnits="userSpaceOnUse" x="-40" y="-40" width="280" height="200"><g fill="#ffffff" stroke="none"><circle cx="60" cy="60" r="30"></circle></g></mask>
</defs>
<circle cx="66" cy="65" r="46" fill="#3d1504"></circle>
<circle cx="60" cy="60" r="46" fill="url(#hxc-body)"></circle>
<circle cx="60" cy="60" r="46" fill="url(#hxc-sheen)"></circle>
<circle cx="60" cy="60" r="46" fill="none" stroke="url(#hxc-rim)" stroke-width="2"></circle>
<circle cx="60" cy="60" r="38" fill="none" stroke="#ffffff" stroke-opacity=".25" stroke-width="1.5" stroke-dasharray="2 5"></circle>
<circle cx="60" cy="60" r="30" fill="#3d1504"></circle>
<g mask="url(#hxc-lens)"><rect x="0" y="0" width="100" height="100" fill="url(#hxc-core)" mask="url(#hxc-m)" transform="translate(23 23) scale(0.74)"></rect></g>
<path d="M50 44h20M50 76h20M52 44q0 12 8 16q8-4 8-16M52 76q0-12 8-16q8 4 8 16" fill="none" stroke="#fff7e6" stroke-width="3" stroke-linecap="round" stroke-linejoin="round" opacity=".9"></path>
<circle cx="60" cy="60" r="30" fill="none" stroke="url(#hxc-rim)" stroke-width="1.4"></circle>
<ellipse cx="48" cy="46" rx="6" ry="3.5" fill="#ffffff" opacity=".75" transform="rotate(-30 48 46)"></ellipse>
</svg></div>
<div class="drift d3 hide-sm" style="position: absolute; right: 7%; top: 60%;"><svg width="108" height="108" viewBox="0 0 120 120" style="display: block; overflow: visible; filter: drop-shadow(0 0 16px #e2d4ff55) drop-shadow(0 18px 30px #6a48ff66);">
<defs>
<linearGradient id="hxe-body" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#b29cff"></stop><stop offset="1" stop-color="#6a48ff"></stop></linearGradient>
<linearGradient id="hxe-dark" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#6a48ff"></stop><stop offset="1" stop-color="#1b0f63"></stop></linearGradient>
<linearGradient id="hxe-core" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="0" y2="100"><stop offset=".3" stop-color="#e2d4ff"><animate attributeName="stop-color" values="#e2d4ff;#d4dcff;#d4f1ff;#d4fff8;#d4e6ff;#e2d4ff" dur="7s" begin="-0.3s" repeatCount="indefinite"></animate></stop><stop offset=".7" stop-color="#6a48ff"><animate attributeName="stop-color" values="#6a48ff;#4882ff;#48ddff;#48ffc5;#48afff;#6a48ff" dur="7s" begin="-0.3s" repeatCount="indefinite"></animate></stop></linearGradient>
<linearGradient id="hxe-rim" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#e2d4ff"></stop><stop offset=".45" stop-color="#e2d4ff" stop-opacity="0"></stop><stop offset=".7" stop-color="#6a48ff" stop-opacity="0"></stop><stop offset="1" stop-color="#6a48ff"></stop></linearGradient>
<radialGradient id="hxe-sheen" cx=".34" cy=".14" r=".72"><stop offset="0" stop-color="#ffffff" stop-opacity=".62"></stop><stop offset=".35" stop-color="#ffffff" stop-opacity=".14"></stop><stop offset=".6" stop-color="#ffffff" stop-opacity="0"></stop></radialGradient>
<radialGradient id="hxe-glow"><stop offset=".4" stop-color="#e2d4ff" stop-opacity=".6"></stop><stop offset="1" stop-color="#e2d4ff" stop-opacity="0"></stop></radialGradient>
<mask id="hxe-m" maskUnits="userSpaceOnUse" x="-20" y="-20" width="140" height="140"><g class="hxc" filter="url(#hx-goo)" fill="#ffffff" style="--d: -0.3s;"><polygon points="25,25 75,25 50,75"></polygon><polygon points="50,25 75,75 25,75"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon><polygon points="35,35 65,35 50,65"></polygon></g></mask>
<mask id="hxe-lens" maskUnits="userSpaceOnUse" x="-40" y="-40" width="280" height="200"><g fill="#ffffff" stroke="none"><circle cx="0" cy="0" r="13"></circle></g></mask>
</defs>
<path d="M60 14l40 22-40 22-40-22z" fill="url(#hxe-body)"></path>
<path d="M60 14l40 22-40 22-40-22z" fill="#ffffff" opacity=".24"></path>
<path d="M20 36l40 22v48L20 84z" fill="url(#hxe-body)"></path>
<path d="M60 58l40-22v48l-40 22z" fill="url(#hxe-dark)"></path>
<path d="M20 36l40 22 40-22v48l-40 22-40-22z" fill="url(#hxe-sheen)"></path>
<path d="M60 14l40 22v48l-40 22-40-22V36z" fill="none" stroke="url(#hxe-rim)" stroke-width="1.6" stroke-linejoin="round"></path>
<path d="M20 36l40 22 40-22M60 58v48" fill="none" stroke="#ffffff" stroke-opacity=".4" stroke-width="1"></path>
</svg></div>
<svg class="twinkle" width="18" height="18" viewBox="0 0 24 24" style="position: absolute; left: 14%; top: 22%;"><path fill="#fff" d="M12 0c.8 6.2 5.8 11.2 12 12-6.2.8-11.2 5.8-12 12C11.2 17.8 6.2 12.8 0 12 6.2 11.2 11.2 6.2 12 0z"></path></svg>
<svg class="twinkle t2" width="14" height="14" viewBox="0 0 24 24" style="position: absolute; left: 70%; top: 14%;"><path fill="#fff" d="M12 0c.8 6.2 5.8 11.2 12 12-6.2.8-11.2 5.8-12 12C11.2 17.8 6.2 12.8 0 12 6.2 11.2 11.2 6.2 12 0z"></path></svg>
<svg class="twinkle t2" width="12" height="12" viewBox="0 0 24 24" style="position: absolute; left: 34%; top: 9%;"><path fill="#fff" d="M12 0c.8 6.2 5.8 11.2 12 12-6.2.8-11.2 5.8-12 12C11.2 17.8 6.2 12.8 0 12 6.2 11.2 11.2 6.2 12 0z"></path></svg>

<div class="horizon" aria-hidden="true" style="position: absolute; left: 0; right: 0; bottom: -500px; height: 760px; pointer-events: none;">
<svg width="100%" height="100%" viewBox="0 0 1600 760" preserveAspectRatio="xMidYMin slice" style="display: block; overflow: visible;">
<defs>
<radialGradient id="pl-fill" gradientUnits="userSpaceOnUse" cx="800" cy="40" r="760">
<stop offset="0" stop-color="#6a3ad0"></stop>
<stop offset=".12" stop-color="#40198f"></stop>
<stop offset=".34" stop-color="#1e0c58"></stop>
<stop offset=".68" stop-color="#0d0633"></stop>
<stop offset="1" stop-color="#07041a"></stop>
</radialGradient>
<linearGradient id="pl-rim" gradientUnits="userSpaceOnUse" x1="0" y1="0" x2="1600" y2="0">
<stop offset="0" stop-color="#ff8fd8" stop-opacity="0"></stop>
<stop offset=".22" stop-color="#ff8fd8" stop-opacity=".35"></stop>
<stop offset=".5" stop-color="#ffe2f6" stop-opacity="1"></stop>
<stop offset=".78" stop-color="#8fb6ff" stop-opacity=".35"></stop>
<stop offset="1" stop-color="#8fb6ff" stop-opacity="0"></stop>
</linearGradient>
<radialGradient id="pl-lines" gradientUnits="userSpaceOnUse" cx="800" cy="40" r="640">
<stop offset="0" stop-color="#d6c8ff" stop-opacity=".22"></stop>
<stop offset="1" stop-color="#d6c8ff" stop-opacity="0"></stop>
</radialGradient>
<radialGradient id="pl-sheen" gradientUnits="userSpaceOnUse" cx="800" cy="60" r="520" gradientTransform="translate(800 60) scale(1 .16) translate(-800 -60)">
<stop offset="0" stop-color="#ffffff" stop-opacity=".16"></stop>
<stop offset="1" stop-color="#ffffff" stop-opacity="0"></stop>
</radialGradient>
<filter id="pl-blur" x="-10%" y="-60%" width="120%" height="220%"><feGaussianBlur stdDeviation="14"></feGaussianBlur></filter>
<filter id="pl-haze" x="-20%" y="-80%" width="140%" height="260%"><feGaussianBlur stdDeviation="48"></feGaussianBlur></filter>
<mask id="pl-clip" maskUnits="userSpaceOnUse" x="-100" y="-100" width="1800" height="1000"><g fill="#ffffff" stroke="none"><circle cx="800" cy="1740" r="1700"></circle></g></mask>
</defs>
<circle cx="800" cy="1740" r="1700" fill="none" stroke="#7d5cff" stroke-opacity=".45" stroke-width="110" filter="url(#pl-haze)"></circle>
<circle cx="800" cy="1740" r="1700" fill="url(#pl-fill)"></circle>
<g mask="url(#pl-clip)" fill="none" stroke="url(#pl-lines)" stroke-width="1">
<circle cx="800" cy="1740" r="1650"></circle>
<circle cx="800" cy="1740" r="1570"></circle>
<circle cx="800" cy="1740" r="1460"></circle>
<circle cx="800" cy="1740" r="1310"></circle>
<ellipse cx="800" cy="1740" rx="300" ry="1700"></ellipse>
<ellipse cx="800" cy="1740" rx="720" ry="1700"></ellipse>
<ellipse cx="800" cy="1740" rx="1180" ry="1700"></ellipse>
</g>
<rect x="0" y="0" width="1600" height="200" fill="url(#pl-sheen)" mask="url(#pl-clip)"></rect>
<circle cx="800" cy="1740" r="1700" fill="none" stroke="url(#pl-rim)" stroke-width="26" opacity=".55" filter="url(#pl-blur)"></circle>
<circle cx="800" cy="1740" r="1700" fill="none" stroke="url(#pl-rim)" stroke-width="1.6"></circle>
</svg>
</div>

<div class="cast" id="cast" style="position: absolute; left: 50%; bottom: 36px; transform: translateX(-50%); width: min(1100px, 96vw); display: flex; align-items: flex-end; justify-content: center;">

<div class="who" style="position: relative; width: 96px; margin: 0 -8px; transform: translateY(0px);">
<div class="fig"><div data-sprite="gem"></div></div>
</div>
<div class="who" style="position: relative; width: 104px; margin: 0 -8px; transform: translateY(-46px);">
<div class="fig"><div data-sprite="nib"></div></div>
</div>
<div class="who" style="position: relative; width: 98px; margin: 0 -8px; transform: translateY(-84px);">
<div class="fig"><div data-sprite="kit"></div></div>
</div>
<div class="who" style="position: relative; width: 120px; margin: 0 -8px; transform: translateY(-110px);">
<div class="fig"><div data-sprite="pip"></div></div>
</div>
<div class="who" style="position: relative; width: 150px; margin: 0 -8px; transform: translateY(-10px);">
<div class="fig"><div data-sprite="puff"></div></div>
</div>
<div class="who" style="position: relative; width: 112px; margin: 0 -8px; transform: translateY(-92px);">
<div class="fig"><div data-sprite="volt"></div></div>
</div>
<div class="who" style="position: relative; width: 100px; margin: 0 -8px; transform: translateY(-36px);">
<div class="fig"><div data-sprite="drip"></div></div>
</div>
<div class="who" style="position: relative; width: 94px; margin: 0 -8px; transform: translateY(0px);">
<div class="fig"><div data-sprite="tome"></div></div>
</div>
</div>
</div>

<div style="position: relative; z-index: 2; max-width: 1180px; margin: 0 auto; padding: 150px 20px 300px; text-align: center;">
<p style="display: inline-flex; align-items: center; gap: 10px; margin: 0 0 18px; padding: 7px 14px 7px 8px; border-radius: 999px; background: rgba(255, 255, 255, 0.06); border: 1px solid rgba(255, 255, 255, 0.12); font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.04em; color: #e3dcff;">
<span style="padding: 4px 8px; border-radius: 999px; background: #93f7cc; color: #0b0726; font-weight: 700;">NEW</span>
Starfork Studio presents
</p>
<h1 style="margin: 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: clamp(114px, min(21vw, 25.5vh), 276px); line-height: 0.84; letter-spacing: 0.005em; filter: drop-shadow(0 12px 0 rgba(10, 6, 40, 0.5)) drop-shadow(0 30px 50px rgba(30, 12, 120, 0.65));">
<span style="position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0 0 0 0);">Desk Dash!</span>
<span aria-hidden="true" style="display: block;">
<span class="ch" style="transform: translateY(0px) rotate(-3deg); animation-delay: 0.00s;">D</span><span class="ch" style="transform: translateY(-6px) rotate(2deg); animation-delay: -0.18s;">e</span><span class="ch" style="transform: translateY(4px) rotate(-1deg); animation-delay: -0.36s;">s</span><span class="ch" style="transform: translateY(-3px) rotate(3deg); animation-delay: -0.54s;">k</span>
</span>
<span aria-hidden="true" style="display: block;">
<span class="ch" style="transform: translateY(-6px) rotate(-1deg); animation-delay: -0.40s;">D</span><span class="ch" style="transform: translateY(4px) rotate(3deg); animation-delay: -0.58s;">a</span><span class="ch" style="transform: translateY(-3px) rotate(-2deg); animation-delay: -0.76s;">s</span><span class="ch" style="transform: translateY(5px) rotate(-3deg); animation-delay: -0.94s;">h</span><span class="ch" style="background-image: linear-gradient(172deg, #eef4ff, #9dbcff 55%, #7fa5ff);transform: translateY(0px) rotate(2deg); animation-delay: -1.12s;">!</span>
</span>
</span>
</sc-for>
</h1>
<p style="max-width: 560px; margin: 28px auto 0; font-size: clamp(17px, 1.6vw, 20px); line-height: 1.55; color: #d9d2fb;">A cosmic endless runner across the messiest desk in the galaxy. From Starfork, a nine-person studio that makes tiny games with big hearts.</p>
<div style="display: flex; flex-wrap: wrap; gap: 14px; justify-content: center; margin-top: 30px;">
<a class="btn" href="#play"><svg width="18" height="18" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M7 4.5v15l12-7.5z"></path></svg>Play a lap</a>
<a class="ghost" href="#crew">Meet the crew</a>
</div>
<div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 10px 22px; margin-top: 28px; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #9d96cf;">
<span>Coming 2026</span><span aria-hidden="true">·</span><span>PC</span><span aria-hidden="true">·</span><span>Switch</span>
</div>
</div>
</section>

<!-- CREW -->
<section id="crew" data-section="crew" style="position: relative; padding: 140px 20px; background: radial-gradient(60% 50% at 75% 45%, rgba(106, 72, 255, 0.2), transparent 70%);">
<div style="max-width: 1180px; margin: 0 auto;">
<div style="display: flex; flex-wrap: wrap; align-items: flex-end; justify-content: space-between; gap: 24px;">
<div>
<p style="margin: 0 0 16px; font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">01 — The crew</p>
<h2 style="margin: 0; font-size: clamp(44px, 6vw, 84px); font-weight: 700; line-height: 0.95; letter-spacing: -0.045em;">Pick a character.</h2>
</div>
<p style="max-width: 400px; margin: 0; font-size: 17px; line-height: 1.6; color: #aaa4d8;">Everyone at Starfork has a runner in the game. Pick one to read about them, then take them for a lap below.</p>
</div>

<div style="display: flex; flex-wrap: wrap; gap: 28px; margin-top: 56px; padding: 28px; border-radius: 32px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.045), rgba(255, 255, 255, 0.015)); border: 1px solid rgba(255, 255, 255, 0.09); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.06), 0 60px 120px -50px rgba(0, 0, 0, 0.8);">
<div role="radiogroup" id="crew-grid" aria-label="Pick a character" style="flex: 999 1 460px; min-width: 0; display: grid; grid-template-columns: repeat(4, minmax(0, 1fr)); gap: 14px; align-content: center;">

</div>

<div aria-live="polite" style="flex: 1 1 320px; min-width: 0; position: relative; overflow: hidden; padding: 26px; border-radius: 24px; text-align: center; background: radial-gradient(120% 80% at 50% 0%, #3a2392 0%, #1a0f55 55%, #0e0838 100%); border: 1px solid rgba(147, 247, 204, 0.45); box-shadow: 0 0 0 4px rgba(147, 247, 204, 0.06), 0 0 60px -10px rgba(147, 247, 204, 0.35);">
<div style="position: absolute; left: -20%; right: -20%; bottom: -30%; height: 60%; background: radial-gradient(closest-side, rgba(147, 247, 204, 0.22), transparent);"></div>
<div style="position: relative; height: 240px; border-radius: 18px; overflow: hidden; background: radial-gradient(80% 70% at 50% 40%, rgba(147, 247, 204, 0.12), transparent 70%), linear-gradient(180deg, #0b0630, #150c4c); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: inset 0 0 0 1px rgba(0, 0, 0, 0.35), inset 0 -40px 60px -30px rgba(147, 247, 204, 0.22);">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.5;"></div>
<div style="position: absolute; left: 0; right: 0; bottom: 0; height: 44px; background: repeating-linear-gradient(90deg, rgba(255, 255, 255, 0.07) 0 1px, transparent 1px 24px), linear-gradient(180deg, rgba(147, 247, 204, 0.14), transparent); border-top: 1px solid rgba(147, 247, 204, 0.4);"></div>
<span id="state-label" style="position: absolute; top: 12px; left: 14px; font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #cfc8f5;"></span>
<span style="position: absolute; top: 12px; right: 14px; display: inline-flex; align-items: center; gap: 6px; font: 700 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.08em; color: #6ee87a;"><span style="width: 6px; height: 6px; border-radius: 50%; background: #6ee87a; box-shadow: 0 0 8px #6ee87a;"></span><span id="fps-label"></span></span>
<div class="popin" id="preview" style="position: absolute; left: 50%; bottom: 26px; width: 168px; margin-left: -84px;"></div>
<svg class="twinkle" width="16" height="16" viewBox="0 0 24 24" style="position: absolute; left: 14%; top: 30%;"><path fill="#fff" d="M12 0c.8 6.2 5.8 11.2 12 12-6.2.8-11.2 5.8-12 12C11.2 17.8 6.2 12.8 0 12 6.2 11.2 11.2 6.2 12 0z"></path></svg>
<svg class="twinkle t2" width="12" height="12" viewBox="0 0 24 24" style="position: absolute; right: 14%; top: 40%;"><path fill="#fff" d="M12 0c.8 6.2 5.8 11.2 12 12-6.2.8-11.2 5.8-12 12C11.2 17.8 6.2 12.8 0 12 6.2 11.2 11.2 6.2 12 0z"></path></svg>
</div>
<div role="radiogroup" id="anim-opts" aria-label="Animation" style="position: relative; display: flex; flex-wrap: wrap; justify-content: center; gap: 6px; margin-top: 14px;">

</div>
<div style="position: relative; display: flex; justify-content: center; align-items: center; gap: 10px; margin-top: 10px;">
<label for="sf-fps" style="font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #9d96cf;">Frame rate</label>
<select id="sf-fps" style="min-height: 44px; padding: 0 14px; border-radius: 999px; background: rgba(255, 255, 255, 0.06); border: 1px solid rgba(255, 255, 255, 0.14); color: #f4f1ff; font: 600 13px/1 'JetBrains Mono', monospace; cursor: pointer;">
<option value="6">6 f/s</option>
<option value="12" selected>12 f/s</option>
<option value="24">24 f/s</option>
<option value="60">60 f/s</option>
</select>
</div>
<h3 id="cur-name" style="position: relative; margin: 6px 0 0; font-size: 40px; font-weight: 700; letter-spacing: -0.04em;"></h3>
<p id="cur-role" style="position: relative; margin: 6px 0 0; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #93f7cc;"></p>
<p id="cur-quote" style="position: relative; max-width: 26em; margin: 14px auto 0; font-size: 15px; line-height: 1.55; color: #d9d2fb;"></p>
<div id="cur-stats" style="position: relative; display: grid; gap: 10px; margin: 20px 0 22px; text-align: left;">

</div>
<button id="accept" class="btn" type="button" data-act="accept" style="position: relative; width: 100%;"></button>
</div>
</div>
</div>
</section>

<!-- PLAY -->
<section id="play" data-section="play" style="position: relative; padding: 120px 20px 140px;">
<div style="max-width: 1180px; margin: 0 auto;">
<div style="display: flex; flex-wrap: wrap; align-items: flex-end; justify-content: space-between; gap: 24px;">
<div>
<p style="margin: 0 0 16px; font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">02 — Playable demo</p>
<h2 style="margin: 0; font-size: clamp(44px, 6vw, 84px); font-weight: 700; line-height: 0.95; letter-spacing: -0.045em;">Thirty seconds of <span style="font-family: 'Lilita One', sans-serif; font-weight: 400; letter-spacing: 0; background: linear-gradient(172deg, #fff1fa, #ffc3ee 34%, #c9b8ff 64%, #8fb6ff); -webkit-background-clip: text; background-clip: text; color: transparent;">Desk Dash!</span></h2>
</div>
<p style="margin: 0; font-size: 15px; color: #aaa4d8;">Jump with <kbd style="display: inline-block; min-width: 28px; padding: 5px 8px; border-radius: 8px; background: rgba(255, 255, 255, 0.07); border: 1px solid rgba(255, 255, 255, 0.14); border-bottom-width: 2px; font: 700 12px/1 'JetBrains Mono', monospace; color: #fff; text-align: center;">Space</kbd> <kbd style="display: inline-block; min-width: 28px; padding: 5px 8px; border-radius: 8px; background: rgba(255, 255, 255, 0.07); border: 1px solid rgba(255, 255, 255, 0.14); border-bottom-width: 2px; font: 700 12px/1 'JetBrains Mono', monospace; color: #fff; text-align: center;">↑</kbd> <kbd style="display: inline-block; min-width: 28px; padding: 5px 8px; border-radius: 8px; background: rgba(255, 255, 255, 0.07); border: 1px solid rgba(255, 255, 255, 0.14); border-bottom-width: 2px; font: 700 12px/1 'JetBrains Mono', monospace; color: #fff; text-align: center;">W</kbd>, a click or a tap.</p>
</div>

<div style="margin-top: 36px; padding: 10px; border-radius: 34px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.09), rgba(255, 255, 255, 0.02)); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), 0 70px 140px -50px rgba(60, 30, 200, 0.6);">
<div class="stage" id="stage" tabindex="0" role="application" aria-label="Desk Dash! demo. Press Space or tap to jump." style="position: relative; height: 420px; border-radius: 26px; overflow: hidden; user-select: none; touch-action: manipulation; cursor: pointer; background: linear-gradient(180deg, #160d5c 0%, #2a1ea0 55%, #3d2cc6 100%);">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.85;"></div>
<div id="bg-far" style="position: absolute; left: 0; bottom: 64px; height: 100%; width: 200%;">
<div style="position: absolute; top: 0; bottom: 0; left: 0%; width: 50%;">
<svg width="180" height="230" viewBox="0 0 180 230" style="position: absolute; left: 6%; bottom: 0; opacity: 0.5;"><path d="M30 230h70M60 230V130l70-80" stroke="#1a1068" stroke-width="12" fill="none" stroke-linecap="round"></path><path d="M110 30l60 20-30 50z" fill="#1a1068"></path><circle cx="60" cy="130" r="12" fill="#1a1068"></circle></svg>
<svg width="460" height="180" viewBox="0 -70 460 180" style="position: absolute; left: 44%; bottom: 0; opacity: 0.45;"><rect x="0" y="0" width="460" height="16" rx="6" fill="#21177e"></rect><rect x="30" y="16" width="16" height="94" fill="#21177e"></rect><rect x="414" y="16" width="16" height="94" fill="#21177e"></rect><rect x="120" y="-70" width="150" height="70" rx="8" fill="#21177e"></rect></svg>
<div style="position: absolute; left: 30%; top: 22%; width: 80px; height: 80px; border-radius: 50%; background: radial-gradient(circle at 38% 32%, #6b5af0, #3326b0 70%); opacity: 0.7;"></div>
</div>
<div style="position: absolute; top: 0; bottom: 0; left: 50%; width: 50%;">
<svg width="180" height="230" viewBox="0 0 180 230" style="position: absolute; left: 6%; bottom: 0; opacity: 0.5;"><path d="M30 230h70M60 230V130l70-80" stroke="#1a1068" stroke-width="12" fill="none" stroke-linecap="round"></path><path d="M110 30l60 20-30 50z" fill="#1a1068"></path><circle cx="60" cy="130" r="12" fill="#1a1068"></circle></svg>
<svg width="460" height="180" viewBox="0 -70 460 180" style="position: absolute; left: 44%; bottom: 0; opacity: 0.45;"><rect x="0" y="0" width="460" height="16" rx="6" fill="#21177e"></rect><rect x="30" y="16" width="16" height="94" fill="#21177e"></rect><rect x="414" y="16" width="16" height="94" fill="#21177e"></rect><rect x="120" y="-70" width="150" height="70" rx="8" fill="#21177e"></rect></svg>
<div style="position: absolute; left: 30%; top: 22%; width: 80px; height: 80px; border-radius: 50%; background: radial-gradient(circle at 38% 32%, #6b5af0, #3326b0 70%); opacity: 0.7;"></div>
</div>
</div>
<div id="ground" style="position: absolute; left: 0; right: 0; bottom: 0; height: 64px; background: repeating-linear-gradient(90deg, rgba(255, 255, 255, 0.07) 0 2px, transparent 2px 64px) 0 0 / auto, linear-gradient(180deg, #4a1d93, #2a0d60); box-shadow: inset 0 1px 0 rgba(255, 190, 236, 0.7), 0 -10px 30px rgba(255, 143, 216, 0.18);"></div>

<div style="position: absolute; top: 18px; left: 18px; right: 18px; z-index: 4; display: flex; justify-content: space-between; align-items: center; pointer-events: none;">
<div aria-hidden="true" style="display: flex; align-items: center; gap: 12px; padding: 6px 14px 6px 6px; border-radius: 999px; background: rgba(9, 5, 34, 0.6); border: 1px solid rgba(255, 255, 255, 0.12); backdrop-filter: blur(8px);">
<span id="dial" style="display: flex; align-items: center; justify-content: center; width: 38px; height: 38px; border-radius: 50%; background: conic-gradient(#ff8fd8 0deg, rgba(255, 255, 255, 0.14) 0);"><span id="secs" style="width: 28px; height: 28px; border-radius: 50%; background: #120a45; display: flex; align-items: center; justify-content: center; font: 700 12px/1 'JetBrains Mono', monospace; color: #fff;"></span></span>
<span style="font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; color: #cfc8f5;">SEC</span>
</div>
<div id="meter" role="img" aria-label="Coins collected: 0 of 6" style="display: flex; gap: 6px; padding: 7px; border-radius: 999px; background: rgba(9, 5, 34, 0.6); border: 1px solid rgba(255, 255, 255, 0.12); backdrop-filter: blur(8px);">

</div>
</div>

<div id="obs-layer" style="display: contents;"></div>



<div id="player" style="position: absolute; left: 0; bottom: 64px; z-index: 3; width: 84px; transform: translate(100px, 0px);">
<div id="player-sprite"></div>
</div>

<div id="fx-layer" aria-hidden="true" style="position: absolute; inset: 0; z-index: 6; pointer-events: none; overflow: hidden;"></div>

<div id="ready-ov">
<div style="position: absolute; inset: 0; z-index: 5; display: flex; align-items: center; justify-content: center; text-align: center; padding: 20px; background: radial-gradient(closest-side, rgba(9, 5, 34, 0.78), rgba(9, 5, 34, 0.3));">
<div>
<p style="margin: 0 0 12px; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">Runner · <span id="runner-name"></span></p>
<h3 style="margin: 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: clamp(48px, 7vw, 80px); line-height: 1; background: linear-gradient(172deg, #fff1fa, #ffc3ee 34%, #c9b8ff 64%, #8fb6ff); -webkit-background-clip: text; background-clip: text; color: transparent;">Ready?</h3>
<p style="margin: 12px 0 24px; color: #d9d2fb;">Dodge the desk clutter. Grab all six coins.</p>
<button class="btn" type="button" data-act="start"><svg width="18" height="18" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M7 4.5v15l12-7.5z"></path></svg>Start run</button>
</div>
</div>
</div>

<div id="end-ov" hidden>
<div style="position: absolute; inset: 0; z-index: 5; display: flex; align-items: center; justify-content: center; text-align: center; padding: 20px; background: radial-gradient(closest-side, rgba(9, 5, 34, 0.82), rgba(9, 5, 34, 0.35));">
<div>
<h3 id="end-title" style="margin: 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: clamp(44px, 7vw, 76px); line-height: 1; background: linear-gradient(172deg, #fff1fa, #ffc3ee 34%, #c9b8ff 64%, #8fb6ff); -webkit-background-clip: text; background-clip: text; color: transparent;"></h3>
<div id="end-stars" aria-hidden="true" style="display: flex; justify-content: center; gap: 6px; margin-top: 14px;">
<svg width="32" height="32" viewBox="0 0 24 24"><path d="M12 2.5l2.9 6 6.6.8-4.9 4.5 1.3 6.5L12 17l-5.9 3.3 1.3-6.5-4.9-4.5 6.6-.8z" fill="rgba(255, 255, 255, 0.16)"></path></svg>
<svg width="32" height="32" viewBox="0 0 24 24"><path d="M12 2.5l2.9 6 6.6.8-4.9 4.5 1.3 6.5L12 17l-5.9 3.3 1.3-6.5-4.9-4.5 6.6-.8z" fill="rgba(255, 255, 255, 0.16)"></path></svg>
<svg width="32" height="32" viewBox="0 0 24 24"><path d="M12 2.5l2.9 6 6.6.8-4.9 4.5 1.3 6.5L12 17l-5.9 3.3 1.3-6.5-4.9-4.5 6.6-.8z" fill="rgba(255, 255, 255, 0.16)"></path></svg>
</div>
<p id="end-text" style="max-width: 30em; margin: 12px auto 24px; color: #d9d2fb;"></p>
<button class="btn" type="button" data-act="start">Run it back</button>
</div>
</div>
</div>
</div>
</div>
<p id="status" role="status" style="position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0 0 0 0);"></p>
</div>
</section>

<!-- GAMES -->
<section id="games" data-section="games" style="position: relative; padding: 120px 20px;">
<div style="max-width: 1180px; margin: 0 auto;">
<div style="display: flex; flex-wrap: wrap; align-items: flex-end; justify-content: space-between; gap: 24px;">
<div>
<p style="margin: 0 0 16px; font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">03 — Our games</p>
<h2 style="margin: 0; font-size: clamp(44px, 6vw, 84px); font-weight: 700; line-height: 0.95; letter-spacing: -0.045em;">Tiny worlds, big runs.</h2>
</div>
<p style="max-width: 400px; margin: 0; font-size: 17px; line-height: 1.6; color: #aaa4d8;">Three games in seven years. We would rather make one small thing feel perfect than ten things feel fine.</p>
</div>

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); gap: 22px; margin-top: 56px;">
<article class="card" style="position: relative; overflow: hidden; border-radius: 28px; background: #0f0a36; border: 1px solid rgba(255, 255, 255, 0.09);">
<div aria-hidden="true" style="position: relative; height: 260px; overflow: hidden; background: linear-gradient(180deg, #3b2bc4, #160d5c);">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.8;"></div>
<div style="position: absolute; left: 50%; bottom: -280px; width: 560px; height: 560px; margin-left: -280px; border-radius: 50%; background: radial-gradient(circle at 50% 3%, #5a2fb8, #120835 40%); box-shadow: 0 -1px 0 rgba(255, 190, 236, 0.6), 0 -20px 60px rgba(140, 100, 255, 0.4);"></div>
<div style="position: absolute; left: 18%; bottom: 34px; width: 70px;"><div data-sprite="drip" data-anim="walk"></div></div>
<div style="position: absolute; left: 50%; bottom: 26px; width: 112px; margin-left: -56px;"><div data-sprite="pip" data-anim="run"></div></div>
<div style="position: absolute; right: 16%; bottom: 30px; width: 74px;"><div data-sprite="volt" data-anim="talk"></div></div>
</div>
<div style="padding: 24px 26px 28px;">
<div style="display: flex; justify-content: space-between; align-items: center; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #9d96cf;"><span>No. 03</span><span style="padding: 6px 10px; border-radius: 999px; background: #93f7cc; color: #0b0726; font-weight: 700;">Coming 2026</span></div>
<h3 style="margin: 16px 0 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: 34px; letter-spacing: 0.01em;">Desk Dash!</h3>
<p style="margin: 10px 0 18px; font-size: 15px; line-height: 1.55; color: #aaa4d8;">A cosmic endless runner across the messiest desk in the galaxy. Eight runners, one coffee mug too many.</p>
<p style="margin: 0; font: 500 12px/1 'JetBrains Mono', monospace; color: #cfc8f5;">In development · PC · Switch</p>
</div>
</article>

<article class="card" style="position: relative; overflow: hidden; border-radius: 28px; background: #0f0a36; border: 1px solid rgba(255, 255, 255, 0.09);">
<div aria-hidden="true" style="position: relative; height: 260px; overflow: hidden; background: linear-gradient(180deg, #1f137d, #4a37d8);">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.8;"></div>
<div style="position: absolute; right: 12%; top: 18%; width: 124px; height: 124px; border-radius: 50%; background: radial-gradient(circle at 35% 30%, #fffaf0, #c9b8ff 70%); box-shadow: 0 0 70px rgba(201, 184, 255, 0.65);"></div>
<div style="position: absolute; left: 0; right: 0; bottom: 0; height: 64px; background: linear-gradient(180deg, #2c1a8a, #160d5c);"></div>
<div style="position: absolute; left: 22%; bottom: 22px; width: 92px;"><div data-sprite="puff"></div></div>
</div>
<div style="padding: 24px 26px 28px;">
<div style="display: flex; justify-content: space-between; align-items: center; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #9d96cf;"><span>No. 02</span><span>2024</span></div>
<h3 style="margin: 16px 0 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: 34px; letter-spacing: 0.01em;">Moonmilk</h3>
<p style="margin: 10px 0 18px; font-size: 15px; line-height: 1.55; color: #aaa4d8;">A cozy farming game on the far side of the moon. Grow star-melons, raise moon-cows, never pay rent.</p>
<p style="margin: 0; font: 500 12px/1 'JetBrains Mono', monospace; color: #cfc8f5;">PC · Mac · Switch</p>
</div>
</article>

<article class="card" style="position: relative; overflow: hidden; border-radius: 28px; background: #0f0a36; border: 1px solid rgba(255, 255, 255, 0.09);">
<div aria-hidden="true" style="position: relative; height: 260px; overflow: hidden; background: radial-gradient(circle at 50% 40%, #4b3ad0, #120835 72%);">
<div class="stars" style="position: absolute; inset: 0; opacity: 0.8;"></div>
<div style="position: absolute; left: 14%; top: 22%; width: 64px; height: 64px; perspective: 500px;">
<div class="cube" style="position: relative; width: 64px; height: 64px;">
<i style="background: linear-gradient(135deg, #8fb0ff, #5b7cf2); transform: translateZ(32px);"></i>
<i style="background: #1d1468; transform: rotateY(180deg) translateZ(32px);"></i>
<i style="background: linear-gradient(135deg, #f7a6ff, #b85cf5); transform: rotateY(90deg) translateZ(32px);"></i>
<i style="background: #22177d; transform: rotateY(-90deg) translateZ(32px);"></i>
<i style="background: #ffd1fb; transform: rotateX(90deg) translateZ(32px);"></i>
<i style="background: #1a1061; transform: rotateX(-90deg) translateZ(32px);"></i>
</div>
</div>
<svg width="160" viewBox="0 0 200 120" style="position: absolute; right: 8%; top: 28%; rotate: -14deg;"><path fill-rule="evenodd" d="M100 32c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="#2a1580"></path><path fill-rule="evenodd" d="M100 22c50 0 90 18 90 40s-40 40-90 40-90-18-90-40 40-40 90-40zm0 26c-26 0-44 6-44 14s18 14 44 14 44-6 44-14-18-14-44-14z" fill="#c47bff"></path></svg>
<div style="position: absolute; left: 44%; bottom: 18px; width: 84px;"><div data-sprite="nib" data-anim="jump"></div></div>
</div>
<div style="padding: 24px 26px 28px;">
<div style="display: flex; justify-content: space-between; align-items: center; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; text-transform: uppercase; color: #9d96cf;"><span>No. 01</span><span>2022</span></div>
<h3 style="margin: 16px 0 0; font-family: 'Lilita One', sans-serif; font-weight: 400; font-size: 34px; letter-spacing: 0.01em;">Paper Comets</h3>
<p style="margin: 10px 0 18px; font-size: 15px; line-height: 1.55; color: #aaa4d8;">Fold paper into comets and thread them through tiny solar systems. A puzzle game about gentle physics.</p>
<p style="margin: 0; font: 500 12px/1 'JetBrains Mono', monospace; color: #cfc8f5;">PC · iOS · Android</p>
</div>
</article>
</div>
</div>
</section>

<!-- STUDIO -->
<section id="studio" data-section="studio" style="position: relative; padding: 120px 20px;">
<div style="max-width: 1180px; margin: 0 auto;">
<div style="display: flex; flex-wrap: wrap; gap: 56px; align-items: center;">
<div style="flex: 1 1 440px; min-width: 0;">
<p style="margin: 0 0 16px; font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">04 — The studio</p>
<h2 style="margin: 0; font-size: clamp(44px, 5.6vw, 76px); font-weight: 700; line-height: 0.98; letter-spacing: -0.045em;">Nine people, one cat, a lot of cubes.</h2>
<p style="max-width: 32em; margin: 22px 0 0; font-size: 17px; line-height: 1.65; color: #aaa4d8;">Starfork lives in an old print shop with a skylight. We prototype on paper, playtest on Fridays and ship when it feels right, not when the calendar says so.</p>
</div>
<dl style="flex: 1 1 440px; min-width: 0; margin: 0; display: grid; grid-template-columns: repeat(2, minmax(0, 1fr)); border-radius: 28px; overflow: hidden; border: 1px solid rgba(255, 255, 255, 0.09); background: rgba(255, 255, 255, 0.09); gap: 1px;">
<div style="padding: 28px; background: #0c0730;"><dd style="margin: 0; font-size: clamp(48px, 5vw, 68px); font-weight: 700; letter-spacing: -0.05em; line-height: 1; color: #ff8fd8;">9</dd><dt style="margin-top: 12px; font: 500 12px/1.3 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #9d96cf;">People on the team</dt></div>
<div style="padding: 28px; background: #0c0730;"><dd style="margin: 0; font-size: clamp(48px, 5vw, 68px); font-weight: 700; letter-spacing: -0.05em; line-height: 1; color: #93f7cc;">3</dd><dt style="margin-top: 12px; font: 500 12px/1.3 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #9d96cf;">Games shipped</dt></div>
<div style="padding: 28px; background: #0c0730;"><dd style="margin: 0; font-size: clamp(48px, 5vw, 68px); font-weight: 700; letter-spacing: -0.05em; line-height: 1; color: #86b6ff;">2.4M</dd><dt style="margin-top: 12px; font: 500 12px/1.3 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #9d96cf;">Players so far</dt></div>
<div style="padding: 28px; background: #0c0730;"><dd style="margin: 0; font-size: clamp(48px, 5vw, 68px); font-weight: 700; letter-spacing: -0.05em; line-height: 1; color: #ffc46b;">1</dd><dt style="margin-top: 12px; font: 500 12px/1.3 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #9d96cf;">Office cat</dt></div>
</dl>
</div>

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr)); gap: 18px; margin-top: 64px;">
<article style="padding: 28px; border-radius: 24px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.01)); border: 1px solid rgba(255, 255, 255, 0.09);">
<svg width="44" height="44" viewBox="0 0 46 46" aria-hidden="true"><rect x="6" y="10" width="26" height="26" rx="6" fill="#ff8fd8"></rect><rect x="14" y="4" width="26" height="26" rx="6" fill="#c9b8ff" opacity=".85"></rect></svg>
<h3 style="margin: 18px 0 8px; font-size: 24px; font-weight: 700; letter-spacing: -0.03em;">Makers</h3>
<p style="margin: 0; font-size: 15px; line-height: 1.6; color: #aaa4d8;">Art, animation and feel. The jump has to feel good before anything else goes in.</p>
</article>
<article style="padding: 28px; border-radius: 24px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.01)); border: 1px solid rgba(255, 255, 255, 0.09);">
<svg width="44" height="44" viewBox="0 0 46 46" aria-hidden="true"><circle cx="23" cy="23" r="17" fill="none" stroke="#86b6ff" stroke-width="6"></circle><circle cx="23" cy="23" r="6" fill="#93f7cc"></circle></svg>
<h3 style="margin: 18px 0 8px; font-size: 24px; font-weight: 700; letter-spacing: -0.03em;">Thinkers</h3>
<p style="margin: 0; font-size: 15px; line-height: 1.6; color: #aaa4d8;">Systems, levels and the maths behind a fair run. Every obstacle earns its place.</p>
</article>
<article style="padding: 28px; border-radius: 24px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.05), rgba(255, 255, 255, 0.01)); border: 1px solid rgba(255, 255, 255, 0.09);">
<svg width="44" height="44" viewBox="0 0 46 46" aria-hidden="true"><rect x="6" y="8" width="34" height="8" rx="4" fill="#ffb347"></rect><rect x="6" y="20" width="24" height="8" rx="4" fill="#ffd9a0"></rect><rect x="6" y="32" width="30" height="8" rx="4" fill="#ff8fd8"></rect></svg>
<h3 style="margin: 18px 0 8px; font-size: 24px; font-weight: 700; letter-spacing: -0.03em;">Organizers</h3>
<p style="margin: 0; font-size: 15px; line-height: 1.6; color: #aaa4d8;">Production, builds and the calendar, so the makers and thinkers never crunch.</p>
</article>
</div>
</div>
</section>

<!-- CAREERS -->
<section id="careers" data-section="careers" style="position: relative; padding: 120px 20px 150px; background: radial-gradient(50% 45% at 50% 60%, rgba(147, 247, 204, 0.08), transparent 70%);">
<div style="max-width: 1180px; margin: 0 auto; text-align: center;">
<p style="margin: 0 0 16px; font: 500 13px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">05 — Careers</p>
<h2 style="margin: 0; font-size: clamp(44px, 6vw, 84px); font-weight: 700; line-height: 0.95; letter-spacing: -0.045em;">Find your role.</h2>
<p style="max-width: 32em; margin: 18px auto 0; font-size: 17px; line-height: 1.6; color: #aaa4d8;">Three quick questions, then we show you the open role that fits. No email needed.</p>

<div aria-live="polite" style="max-width: 620px; margin: 52px auto 0; padding: 40px 32px 32px; border-radius: 32px; background: linear-gradient(180deg, rgba(255, 255, 255, 0.055), rgba(255, 255, 255, 0.015)); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.07), 0 60px 120px -50px rgba(0, 0, 0, 0.8);">
<div id="quiz-open">
<div>
<p id="q-count" style="margin: 0 0 14px; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.14em; color: #9d96cf;"></p>
<fieldset style="margin: 0; padding: 0; border: 0;">
<legend id="q-q" style="width: 100%; padding: 0; font-size: clamp(24px, 3.2vw, 32px); font-weight: 700; line-height: 1.2; letter-spacing: -0.03em; color: #fff;"></legend>
<div id="q-opts" style="display: grid; gap: 10px; max-width: 380px; margin: 28px auto; text-align: left;">

</div>
</fieldset>
<div style="display: flex; justify-content: center; gap: 12px;">
<button class="ghost" type="button" data-act="back" id="q-back" hidden>Back</button>
<button id="q-next" class="btn" type="button" data-act="next" disabled></button>
</div>
<div id="q-dashes" aria-hidden="true" style="display: flex; justify-content: center; gap: 8px; margin-top: 26px;">

</div>
</div>
</div>
<div id="quiz-done" hidden>
<div>
<div class="popin" id="role-sprite" style="width: 150px; margin: 0 auto 8px;"></div>
<p style="margin: 0; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">You are a <span id="role-type"></span></p>
<h3 id="role-role" style="margin: 12px 0 0; font-size: 38px; font-weight: 700; letter-spacing: -0.04em;"></h3>
<p style="margin: 6px 0 0; font-size: 15px; color: #cfc8f5;">Working with <span id="role-mate"></span></p>
<p id="role-text" style="max-width: 30em; margin: 16px auto 22px; font-size: 16px; line-height: 1.6; color: #d9d2fb;"></p>
<div id="role-meta" style="display: flex; flex-wrap: wrap; justify-content: center; gap: 8px; margin-bottom: 26px;">

</div>
<div style="display: flex; flex-wrap: wrap; justify-content: center; gap: 12px;">
<button class="ghost" type="button" data-act="retake">Retake</button>
<button class="btn" type="button" data-act="apply">Apply for this role</button>
</div>
<p id="apply-msg" role="status" style="min-height: 1.6em; margin: 16px 0 0; font-size: 14px; font-weight: 600; color: #93f7cc;"></p>
</div>
</div>
</div>
</div>
</section>

<!-- FOOTER -->
<footer data-section="footer" style="position: relative; overflow: hidden; padding: 40px 20px 32px;">
<div aria-hidden="true" style="position: absolute; left: 50%; top: 0; width: 1000px; height: 420px; transform: translateX(-50%); background: radial-gradient(50% 55% at 50% 0%, rgba(125, 92, 255, 0.2), transparent 70%); pointer-events: none;"></div>
<div style="position: relative; max-width: 1180px; margin: 0 auto;">

<div style="position: relative; overflow: hidden; display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 32px; padding: 40px; border-radius: 32px; background: radial-gradient(90% 120% at 0% 0%, rgba(147, 247, 204, 0.1), transparent 55%), radial-gradient(90% 120% at 100% 100%, rgba(255, 143, 216, 0.12), transparent 55%), linear-gradient(180deg, rgba(255, 255, 255, 0.055), rgba(255, 255, 255, 0.015)); border: 1px solid rgba(255, 255, 255, 0.1); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.08), 0 60px 120px -60px rgba(80, 50, 220, 0.65);">
<div style="flex: 1 1 360px; min-width: 0;">
<p style="margin: 0 0 14px; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #93f7cc;">Thanks for stopping by</p>
<h2 style="margin: 0; font-size: clamp(34px, 4.4vw, 56px); font-weight: 700; line-height: 1; letter-spacing: -0.045em;">Take one more lap.</h2>
<p style="max-width: 30em; margin: 14px 0 0; font-size: 16px; line-height: 1.6; color: #aaa4d8;">Thirty seconds, six coins and the messiest desk in the galaxy. The whole crew is waiting on the start line.</p>
</div>
<div style="flex: 0 1 auto; display: flex; flex-direction: column; align-items: flex-start; gap: 22px;">
<div aria-hidden="true" style="display: flex; align-items: flex-end; padding: 0 6px;">
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="pip" data-anim="talk"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="nib" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="volt" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="drip" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="gem" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="puff" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="kit" data-anim="idle"></div></div>
<div style="width: 50px; margin: 0 -5px;"><div data-sprite="tome" data-anim="idle"></div></div>
</div>
<div style="display: flex; flex-wrap: wrap; gap: 12px;">
<a class="btn" href="#play"><svg width="18" height="18" viewBox="0 0 24 24" aria-hidden="true"><path fill="currentColor" d="M7 4.5v15l12-7.5z"></path></svg>Play the demo</a>
<a class="ghost" href="#careers">See open roles</a>
</div>
</div>
</div>

<div style="display: flex; flex-wrap: wrap; gap: 40px 56px; margin-top: 72px;">
<div style="flex: 2 1 300px; min-width: 0;">
<a href="#top" aria-label="Starfork Studio home" style="display: inline-flex; align-items: center; gap: 10px; text-decoration: none; font-weight: 700; font-size: 19px; letter-spacing: -0.02em;">
<svg width="32" height="32" viewBox="0 0 40 40" aria-hidden="true"><circle cx="20" cy="20" r="19" fill="#6a48ff"></circle><path d="M20 7l2.8 8.4H31l-6.6 5 2.6 8.3L20 23.6l-7 5.1 2.6-8.3-6.6-5h8.2z" fill="#ffe7f6"></path><circle cx="31" cy="9" r="4" fill="#93f7cc"></circle></svg>
Starfork
</a>
<p style="max-width: 24em; margin: 16px 0 0; font-size: 15px; line-height: 1.65; color: #aaa4d8;">A nine-person studio in an old print shop with a skylight, making tiny games with big hearts.</p>
<p style="display: inline-flex; align-items: center; gap: 10px; margin: 20px 0 0; padding: 8px 14px 8px 12px; border-radius: 999px; background: rgba(147, 247, 204, 0.07); border: 1px solid rgba(147, 247, 204, 0.22); font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.04em; color: #d9fff0;">
<span class="pulse" style="width: 8px; height: 8px; border-radius: 50%; background: #93f7cc;"></span>
Now building: Desk Dash!
</p>
</div>
<nav aria-label="Explore" style="flex: 1 1 140px; min-width: 0;">
<p style="margin: 0 0 18px; font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #8f88c4;">Explore</p>
<div style="display: flex; flex-direction: column; gap: 12px;">
<a class="navlink" href="#crew">The crew</a>
<a class="navlink" href="#play">Play the demo</a>
<a class="navlink" href="#studio">The studio</a>
</div>
</nav>
<nav aria-label="Games" style="flex: 1 1 140px; min-width: 0;">
<p style="margin: 0 0 18px; font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #8f88c4;">Games</p>
<div style="display: flex; flex-direction: column; gap: 12px;">
<a class="navlink" href="#games">Desk Dash!</a>
<a class="navlink" href="#games">Moonmilk</a>
<a class="navlink" href="#games">Paper Comets</a>
</div>
</nav>
<nav aria-label="Join" style="flex: 1 1 140px; min-width: 0;">
<p style="margin: 0 0 18px; font: 500 11px/1 'JetBrains Mono', monospace; letter-spacing: 0.16em; text-transform: uppercase; color: #8f88c4;">Join us</p>
<div style="display: flex; flex-direction: column; gap: 12px;">
<a class="navlink" href="#careers">Find your role</a>
<a class="navlink" href="#careers">Open roles</a>
</div>
</nav>
</div>

<div style="display: flex; flex-wrap: wrap; align-items: center; justify-content: space-between; gap: 18px; margin-top: 64px; padding-top: 24px; border-top: 1px solid rgba(255, 255, 255, 0.08);">
<p style="max-width: 46em; margin: 0; font-size: 13px; line-height: 1.6; color: #8f88c4;">© 2026 Starfork Studio. A fictional studio made for the INSTALANDING.AI library: the games, team, players and roles are invented.</p>
<a class="toplink" href="#top" style="display: inline-flex; align-items: center; gap: 10px; min-height: 44px; padding: 0 16px 0 18px; border-radius: 999px; text-decoration: none; font: 500 12px/1 'JetBrains Mono', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #e3dcff; background: rgba(255, 255, 255, 0.05); border: 1px solid rgba(255, 255, 255, 0.14);">Back to top<svg width="16" height="16" viewBox="0 0 24 24" aria-hidden="true" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 19V5M5 12l7-7 7 7"></path></svg></a>
</div>
</div>
</footer>

<div id="toast" role="status" class="toast" style="position: fixed; left: 50%; bottom: 24px; z-index: 50; max-width: calc(100% - 32px); padding: 13px 20px; border-radius: 999px; background: #f4f1ff; color: #0b0726; font-weight: 700; font-size: 15px; box-shadow: 0 20px 50px -10px rgba(0, 0, 0, 0.6); pointer-events: none; transform: translate(-50%, 160%); opacity: 0;"></div>
</div>
<script>
(function () {
  'use strict';

  /* ── 1. Data ─────────────────────────────────────────────────────────── */
  var CREW = [
    { k: 'pip',  name: 'Pip',  role: 'Creative director',    quote: '"If the jump does not make you smile, nothing else matters."', stats: [['Speed', 70], ['Jump', 80], ['Focus', 90]], jump: 1 },
    { k: 'nib',  name: 'Nib',  role: 'Narrative designer',   quote: 'Writes every line a character says, then cuts half of them.', stats: [['Speed', 60], ['Jump', 75], ['Focus', 95]], jump: 0.97 },
    { k: 'volt', name: 'Volt', role: 'Engine programmer',    quote: 'Keeps the game at 60 frames on a nine-year-old laptop.', stats: [['Speed', 90], ['Jump', 65], ['Focus', 85]], jump: 0.95 },
    { k: 'drip', name: 'Drip', role: 'Audio and party lead', quote: 'Every coin sound in Desk Dash! is Drip tapping a mug.', stats: [['Speed', 75], ['Jump', 90], ['Focus', 60]], jump: 1.06 },
    { k: 'gem',  name: 'Gem',  role: 'Technical artist',     quote: 'Makes the cubes shine without melting your GPU.', stats: [['Speed', 80], ['Jump', 70], ['Focus', 80]], jump: 1 },
    { k: 'puff', name: 'Puff', role: 'Character artist',     quote: 'Drew all eight of us, and made themself the fluffiest.', stats: [['Speed', 55], ['Jump', 95], ['Focus', 75]], jump: 1.08 },
    { k: 'kit',  name: 'Kit',  role: 'Tools engineer',       quote: 'Built the level editor the rest of the team lives in.', stats: [['Speed', 85], ['Jump', 60], ['Focus', 90]], jump: 0.94 },
    { k: 'tome', name: 'Tome', role: 'Producer',             quote: 'Owns the calendar, so nobody owns a crunch.', stats: [['Speed', 65], ['Jump', 70], ['Focus', 100]], jump: 0.98 }
  ];
  var OBST = [{ k: 'books', w: 66, h: 58 }, { k: 'mug', w: 56, h: 56 }, { k: 'wifi', w: 54, h: 74 }, { k: 'hurdle', w: 76, h: 50 }, { k: 'speaker', w: 48, h: 66 }];
  var QUIZ = [
    { q: 'Are you a Maker, Thinker, or Organizer?', a: [['Maker', 'maker'], ['Thinker', 'thinker'], ['Organizer', 'organizer']] },
    { q: 'A build breaks at 6pm. You…', a: [['Open the editor and fix it', 'maker'], ['Work out why it broke', 'thinker'], ['Re-plan tomorrow so nobody stays late', 'organizer']] },
    { q: 'Your favourite part of a game is…', a: [['How it feels', 'maker'], ['How it works', 'thinker'], ['That it shipped', 'organizer']] }
  ];
  var ROLES = {
    maker: { k: 'puff', role: 'Gameplay animator', text: 'You would sit next to Puff and make every jump, stumble and victory dance in Desk Dash! feel right.', meta: ['Full time', 'Studio or remote', 'Spine or Rive'] },
    thinker: { k: 'volt', role: 'Systems designer', text: 'You would tune the obstacle maths with Volt so every run is hard, fair and over in thirty seconds.', meta: ['Full time', 'Studio', 'Unity'] },
    organizer: { k: 'tome', role: 'Associate producer', text: 'You would run the calendar with Tome and keep the no-crunch promise we make to everyone who joins.', meta: ['Full time', 'Studio or remote', 'Jira, sadly'] }
  };
  var RUN = 30, PX = 100, PW = 84;
  var ANIMS = ['idle', 'walk', 'talk', 'run', 'punch', 'jump', 'death'];
  function crewOf(k) { for (var i = 0; i < CREW.length; i++) if (CREW[i].k === k) return CREW[i]; return CREW[0]; }
  function $(id) { return document.getElementById(id); }
  var reduced = typeof matchMedia === 'function' && matchMedia('(prefers-reduced-motion: reduce)').matches;

  /* ── 2. Sprite rig ───────────────────────────────────────────────────────
     Each character is one SVG template (SPR_BODY) plus shared gradient defs
     (SPR_DEFS), filled per instance with its own ids so gradients never clash.
     Poses are CSS classes (.a-idle, .a-run …) whose keyframes step a whole
     frame at a time, like a sprite sheet; --dur = frames / fps. */
  var SPR_DEFS = "<svg width=\"0\" height=\"0\" aria-hidden=\"true\" style=\"{{defsStyle}}\">\n<defs>\n<linearGradient id=\"base{{u}}\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\">\n<stop offset=\"0\" stop-color=\"{{two}}\"></stop>\n<stop offset=\".5\" stop-color=\"{{two}}\"></stop>\n<stop offset=\"1\" stop-color=\"{{deep}}\"></stop>\n</linearGradient>\n<linearGradient id=\"core{{u}}\" gradientUnits=\"userSpaceOnUse\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"100\">\n<stop offset=\".3\" stop-color=\"{{one}}\"><animate attributeName=\"stop-color\" values=\"{{oneShift}}\" dur=\"7s\" begin=\"{{begin}}\" repeatCount=\"indefinite\"></animate></stop>\n<stop offset=\".7\" stop-color=\"{{two}}\"><animate attributeName=\"stop-color\" values=\"{{twoShift}}\" dur=\"7s\" begin=\"{{begin}}\" repeatCount=\"indefinite\"></animate></stop>\n</linearGradient>\n<linearGradient id=\"rim{{u}}\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\">\n<stop offset=\"0\" stop-color=\"{{one}}\"></stop>\n<stop offset=\".45\" stop-color=\"{{one}}\" stop-opacity=\"0\"></stop>\n<stop offset=\".7\" stop-color=\"{{two}}\" stop-opacity=\"0\"></stop>\n<stop offset=\"1\" stop-color=\"{{two}}\"></stop>\n</linearGradient>\n<radialGradient id=\"sheen{{u}}\" cx=\".36\" cy=\".14\" r=\".72\">\n<stop offset=\"0\" stop-color=\"#ffffff\" stop-opacity=\".6\"></stop>\n<stop offset=\".35\" stop-color=\"#ffffff\" stop-opacity=\".14\"></stop>\n<stop offset=\".6\" stop-color=\"#ffffff\" stop-opacity=\"0\"></stop>\n</radialGradient>\n<linearGradient id=\"bodyg{{u}}\" x1=\"0\" y1=\"0\" x2=\"0\" y2=\"1\">\n<stop offset=\"0\" stop-color=\"{{bodyTop}}\"></stop>\n<stop offset=\"1\" stop-color=\"{{two}}\"></stop>\n</linearGradient>\n<radialGradient id=\"eglow{{u}}\">\n<stop offset=\".45\" stop-color=\"{{one}}\" stop-opacity=\".55\"></stop>\n<stop offset=\"1\" stop-color=\"{{one}}\" stop-opacity=\"0\"></stop>\n</radialGradient>\n<mask id=\"e{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\"></ellipse></g></mask>\n<radialGradient id=\"glow{{u}}\" cx=\".5\" cy=\"1.05\" r=\".75\">\n<stop offset=\"0\" stop-color=\"{{one}}\" stop-opacity=\".55\"></stop>\n<stop offset=\"1\" stop-color=\"{{one}}\" stop-opacity=\"0\"></stop>\n</radialGradient>\n<filter id=\"goo{{u}}\" x=\"-30%\" y=\"-30%\" width=\"160%\" height=\"160%\">\n<feGaussianBlur stdDeviation=\"7\"></feGaussianBlur>\n<feColorMatrix type=\"matrix\" values=\"1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6\"><animate attributeName=\"values\" values=\"1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 4 -1.2;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 4 -1.2;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6;1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 15 -6\" keyTimes=\"0;.2;.4;.6;1\" dur=\"1.8s\" begin=\"{{begin}}\" repeatCount=\"indefinite\"></animate></feColorMatrix>\n</filter>\n<mask id=\"m{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-20\" y=\"-20\" width=\"140\" height=\"140\">\n<g class=\"sfc\" filter=\"url(#goo{{u}})\" fill=\"#ffffff\" style=\"{{delayStyle}}\">\n<polygon points=\"25,25 75,25 50,75\"></polygon>\n<polygon points=\"50,25 75,75 25,75\"></polygon>\n<polygon points=\"35,35 65,35 50,65\"></polygon>\n<polygon points=\"35,35 65,35 50,65\"></polygon>\n<polygon points=\"35,35 65,35 50,65\"></polygon>\n<polygon points=\"35,35 65,35 50,65\"></polygon>\n</g>\n</mask>\n</defs>\n</svg>";
  var SPR_BODY = {
 "pip": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><ellipse id=\"s{{u}}\" cx=\"60\" cy=\"62\" rx=\"31\" ry=\"25\"></ellipse><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><ellipse cx=\"60\" cy=\"62\" rx=\"31\" ry=\"25\"></ellipse></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<path d=\"M38 104q22 10 44 0l-6-30H44z\" fill=\"#2bb8d6\"></path><path d=\"M44 74h32l2 10q-18 6-36 0z\" fill=\"#ffffff\" opacity=\".18\"></path><g fill=\"#fff\" opacity=\".9\"><circle cx=\"50\" cy=\"90\" r=\"2.2\"></circle><circle cx=\"64\" cy=\"98\" r=\"2.2\"></circle><circle cx=\"70\" cy=\"84\" r=\"2.2\"></circle><circle cx=\"56\" cy=\"80\" r=\"1.8\"></circle></g>\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></use>\n<path d=\"M40 44q20-34 40 0z\" fill=\"#2aa8d8\"></path><path d=\"M44 42q16-26 32 0\" fill=\"none\" stroke=\"#bff2ff\" stroke-width=\"2\" stroke-linecap=\"round\" opacity=\".7\"></path><ellipse cx=\"60\" cy=\"44\" rx=\"26\" ry=\"5\" fill=\"#1d86b8\"></ellipse><circle cx=\"60\" cy=\"18\" r=\"4\" fill=\"#ffe36b\"></circle><circle class=\"tip\" cx=\"60\" cy=\"18\" r=\"9\" fill=\"#ffe36b\" opacity=\".25\"></circle>\n<g class=\"ac\" style=\"transform-origin: 30% 92%;\"><g transform=\"rotate(25 96 70)\"><rect x=\"92\" y=\"44\" width=\"8\" height=\"40\" rx=\"4\" fill=\"#24164f\"></rect><path d=\"M92 44l4-10 4 10z\" fill=\"#ff8fd8\"></path><circle cx=\"96\" cy=\"33\" r=\"6\" fill=\"#ff8fd8\" opacity=\".35\"></circle></g><circle cx=\"92\" cy=\"80\" r=\"7\" fill=\"url(#base{{u}})\"></circle></g>\n<g transform=\"translate(60 62)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<g transform=\"translate(110 34)\"><g class=\"fx\"><path d=\"M0 -12c.8 6.4 5.6 11.2 12 12-6.4.8-11.2 5.6-12 12C-.8 5.6-5.6.8-12 0-5.6-.8-.8-5.6 0-12z\" fill=\"#ffe36b\"></path><path d=\"M14 4c.4 3.2 2.8 5.6 6 6-3.2.4-5.6 2.8-6 6-.4-3.2-2.8-5.6-6-6 3.2-.4 5.6-2.8 6-6z\" fill=\"#ff8fd8\"></path><path d=\"M-8 14c.3 2.4 2.1 4.2 4.5 4.5-2.4.3-4.2 2.1-4.5 4.5-.3-2.4-2.1-4.2-4.5-4.5 2.4-.3 4.2-2.1 4.5-4.5z\" fill=\"#93f7cc\"></path><circle cx=\"10\" cy=\"-10\" r=\"2\" fill=\"#fff\"></circle></g></g>\n</g>\n</svg>",
 "nib": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><rect id=\"s{{u}}\" x=\"32\" y=\"34\" width=\"56\" height=\"70\" rx=\"12\"></rect><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><rect x=\"32\" y=\"34\" width=\"56\" height=\"70\" rx=\"12\"></rect></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"><g stroke=\"#ffffff\" stroke-opacity=\".12\" stroke-width=\"1\"><path d=\"M32 60h56M32 70h56M32 80h56M32 90h56\"></path></g></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></use>\n<g fill=\"none\" stroke=\"#d9cfff\" stroke-width=\"3.5\" stroke-linecap=\"round\"><path d=\"M42 29v10M52 29v10M62 29v10M72 29v10M82 29v10\"></path></g>\n<g transform=\"translate(60 70)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<g class=\"ac\" style=\"transform-origin: 30% 60%;\"><path d=\"M80 80l16-6 0 12q-2 12-16 18q-14-6-16-18z\" fill=\"#93f7cc\" stroke=\"#2fae7b\" stroke-width=\"3\" transform=\"translate(8 0) scale(.9)\"></path><path d=\"M83 76l6-2\" stroke=\"#ffffff\" stroke-width=\"2\" stroke-linecap=\"round\" opacity=\".7\"></path></g>\n<g transform=\"translate(108 78)\"><g class=\"fx\"><circle cx=\"0\" cy=\"0\" r=\"9\" fill=\"#6b4fd8\"></circle><circle cx=\"11\" cy=\"-7\" r=\"3.5\" fill=\"#6b4fd8\"></circle><circle cx=\"12\" cy=\"7\" r=\"2.6\" fill=\"#8b6ff0\"></circle><circle cx=\"-4\" cy=\"12\" r=\"2.2\" fill=\"#8b6ff0\"></circle><circle cx=\"-2\" cy=\"-12\" r=\"2\" fill=\"#b49cff\"></circle><circle cx=\"-3\" cy=\"-3\" r=\"2.5\" fill=\"#ffffff\" opacity=\".5\"></circle></g></g>\n</g>\n</svg>",
 "volt": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><rect id=\"s{{u}}\" x=\"34\" y=\"40\" width=\"52\" height=\"42\" rx=\"8\"></rect><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><rect x=\"34\" y=\"40\" width=\"52\" height=\"42\" rx=\"8\"></rect></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"#d9701f\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"#d9701f\"></ellipse>\n<g class=\"bd\">\n<rect x=\"44\" y=\"88\" width=\"32\" height=\"18\" rx=\"5\" fill=\"#d9701f\"></rect>\n<path d=\"M56 22l4-10 4 10z\" fill=\"#ff8a2b\"></path><rect x=\"58\" y=\"22\" width=\"4\" height=\"12\" fill=\"#ff8a2b\"></rect><circle class=\"tip\" cx=\"60\" cy=\"12\" r=\"7\" fill=\"{{one}}\" opacity=\".45\"></circle>\n<rect x=\"26\" y=\"32\" width=\"68\" height=\"58\" rx=\"14\" fill=\"url(#bodyg{{u}})\"></rect>\n<rect x=\"26\" y=\"32\" width=\"68\" height=\"58\" rx=\"14\" fill=\"url(#sheen{{u}})\"></rect>\n<rect x=\"26\" y=\"32\" width=\"68\" height=\"58\" rx=\"14\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></rect>\n<use href=\"#s{{u}}\" fill=\"{{deep}}\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"><g stroke=\"#ffffff\" stroke-opacity=\".08\"><path d=\"M34 48h52M34 56h52M34 64h52M34 72h52\"></path></g></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\" opacity=\".7\"></use>\n<g transform=\"translate(60 60) scale(.9)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse></g></g>\n<path d=\"M26 66h-10l-4 8\" fill=\"none\" stroke=\"#ff8a2b\" stroke-width=\"6\" stroke-linecap=\"round\"></path>\n<g class=\"ac\" style=\"transform-origin: 0% 70%;\"><path d=\"M94 66h12l6-8\" fill=\"none\" stroke=\"#ff8a2b\" stroke-width=\"6\" stroke-linecap=\"round\"></path><path d=\"M108 52l8 4-8 6z\" fill=\"#fff\"></path></g>\n<g transform=\"translate(118 44)\"><g class=\"fx\"><circle cx=\"0\" cy=\"0\" r=\"15\" fill=\"{{one}}\" opacity=\".35\"></circle><path d=\"M2 -17l-9 16h7l-5 17 15-21h-8l7-12z\" fill=\"#ffe36b\" stroke=\"#fff6c2\" stroke-width=\"1.2\" stroke-linejoin=\"round\"></path></g></g>\n</g>\n</svg>",
 "drip": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><path id=\"s{{u}}\" d=\"M60 24q36 40 34 60q-2 24-34 24t-34-24q-2-20 34-60z\"></path><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><path d=\"M60 24q36 40 34 60q-2 24-34 24t-34-24q-2-20 34-60z\"></path></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></use>\n<g class=\"ac\" style=\"transform-origin: 50% 100%;\"><path d=\"M42 28l18-22 18 22z\" fill=\"#ff8fd8\"></path><path d=\"M48 21h24M53 14h14\" stroke=\"#ffe36b\" stroke-width=\"4\"></path><circle cx=\"60\" cy=\"6\" r=\"4\" fill=\"#93f7cc\"></circle></g>\n<g transform=\"translate(60 72)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<path d=\"M50 96l10 4-10 4zM70 96l-10 4 10 4z\" fill=\"#fff\"></path><circle cx=\"60\" cy=\"100\" r=\"3\" fill=\"#fff\"></circle>\n<g transform=\"translate(104 64)\"><g class=\"fx\"><path d=\"M0 -14q7 9 0 14q-7-5 0-14z\" fill=\"{{one}}\"></path><path d=\"M0 -14q7 9 0 14q-7-5 0-14z\" fill=\"{{one}}\" transform=\"rotate(55) translate(0 -4) scale(.7)\"></path><path d=\"M0 -14q7 9 0 14q-7-5 0-14z\" fill=\"{{one}}\" transform=\"rotate(-50) translate(0 -4) scale(.75)\"></path><path d=\"M0 -14q7 9 0 14q-7-5 0-14z\" fill=\"#ffffff\" opacity=\".8\" transform=\"rotate(110) translate(0 -6) scale(.45)\"></path><circle cx=\"-1\" cy=\"-7\" r=\"1.6\" fill=\"#ffffff\"></circle></g></g>\n</g>\n</svg>",
 "gem": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><path id=\"s{{u}}\" d=\"M60 18l36 20v40l-36 22-36-22V38z\"></path><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><path d=\"M60 18l36 20v40l-36 22-36-22V38z\"></path></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\">\n<path d=\"M60 18l36 20-36 18-36-18z\" fill=\"#ffffff\" opacity=\".18\"></path><path d=\"M24 38l36 18v44L24 78z\" fill=\"#000000\" opacity=\".14\"></path><path d=\"M60 56v44\" stroke=\"#ffffff\" stroke-opacity=\".25\" stroke-width=\"1\"></path><path d=\"M24 38l36 18 36-18\" fill=\"none\" stroke=\"#ffffff\" stroke-opacity=\".35\" stroke-width=\"1\"></path></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\" stroke-linejoin=\"round\"></use>\n<g transform=\"translate(60 66)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<g class=\"ac\" style=\"transform-origin: 50% 50%;\"><circle cx=\"100\" cy=\"98\" r=\"12\" fill=\"url(#base{{u}})\"></circle><circle cx=\"100\" cy=\"98\" r=\"12\" fill=\"url(#sheen{{u}})\"></circle><path d=\"M95 98h10M100 93v10\" stroke=\"#fff\" stroke-width=\"3\" stroke-linecap=\"round\"></path></g>\n<g transform=\"translate(108 46)\"><g class=\"fx\"><path d=\"M-14 0l28-12v5z\" fill=\"#ff8fd8\"></path><path d=\"M-14 0l28-2v5z\" fill=\"#ffe36b\"></path><path d=\"M-14 0l28 8v5z\" fill=\"#86b6ff\"></path><path d=\"M-14 -4l4 4-4 4-4-4z\" fill=\"#ffffff\"></path></g></g>\n</g>\n</svg>",
 "puff": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><g id=\"s{{u}}\"><circle cx=\"60\" cy=\"34\" r=\"18\"></circle><circle cx=\"84\" cy=\"46\" r=\"18\"></circle><circle cx=\"86\" cy=\"74\" r=\"18\"></circle><circle cx=\"60\" cy=\"88\" r=\"18\"></circle><circle cx=\"34\" cy=\"74\" r=\"18\"></circle><circle cx=\"36\" cy=\"46\" r=\"18\"></circle><circle cx=\"60\" cy=\"60\" r=\"30\"></circle></g><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><circle cx=\"60\" cy=\"34\" r=\"18\"></circle><circle cx=\"84\" cy=\"46\" r=\"18\"></circle><circle cx=\"86\" cy=\"74\" r=\"18\"></circle><circle cx=\"60\" cy=\"88\" r=\"18\"></circle><circle cx=\"34\" cy=\"74\" r=\"18\"></circle><circle cx=\"36\" cy=\"46\" r=\"18\"></circle><circle cx=\"60\" cy=\"60\" r=\"30\"></circle></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<g class=\"ac\" style=\"transform-origin: 50% 100%;\"><circle cx=\"52\" cy=\"16\" r=\"6\" fill=\"url(#bodyg{{u}})\"></circle><circle cx=\"61\" cy=\"11\" r=\"7\" fill=\"url(#bodyg{{u}})\"></circle><circle cx=\"69\" cy=\"17\" r=\"5\" fill=\"url(#bodyg{{u}})\"></circle><circle cx=\"59\" cy=\"9\" r=\"3\" fill=\"#ffffff\" opacity=\".5\"></circle></g>\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\" stroke=\"{{one}}\" stroke-opacity=\".35\" stroke-width=\"1.2\"></use>\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"><rect x=\"0\" y=\"0\" width=\"120\" height=\"120\" fill=\"url(#sheen{{u}})\"></rect></g>\n<g transform=\"translate(60 60)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<ellipse cx=\"44\" cy=\"74\" rx=\"6\" ry=\"3.5\" fill=\"#ff5f8f\" opacity=\".55\"></ellipse><ellipse cx=\"76\" cy=\"74\" rx=\"6\" ry=\"3.5\" fill=\"#ff5f8f\" opacity=\".55\"></ellipse>\n<g transform=\"translate(108 60)\"><g class=\"fx\"><g fill=\"#ffffff\" opacity=\".92\"><circle cx=\"-4\" cy=\"0\" r=\"7\"></circle><circle cx=\"5\" cy=\"-3\" r=\"8\"></circle><circle cx=\"12\" cy=\"3\" r=\"6\"></circle><circle cx=\"2\" cy=\"5\" r=\"6\"></circle></g><g fill=\"{{one}}\" opacity=\".8\"><circle cx=\"-10\" cy=\"-14\" r=\"4\"></circle><circle cx=\"-5\" cy=\"-16\" r=\"5\"></circle><circle cx=\"0\" cy=\"-13\" r=\"3.5\"></circle></g><g fill=\"{{one}}\" opacity=\".65\"><circle cx=\"-8\" cy=\"15\" r=\"3\"></circle><circle cx=\"-4\" cy=\"14\" r=\"4\"></circle></g></g></g>\n</g>\n</svg>",
 "kit": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><rect id=\"s{{u}}\" x=\"28\" y=\"40\" width=\"64\" height=\"62\" rx=\"10\"></rect><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><rect x=\"28\" y=\"40\" width=\"64\" height=\"62\" rx=\"10\"></rect></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<g class=\"ac\" style=\"transform-origin: 50% 100%;\"><path d=\"M50 30q-6-14 4-18q6 8-4 18zM62 30q2-16 14-14q-2 12-14 14z\" fill=\"#58c95a\"></path><path d=\"M53 27q-2-7 1-11M64 27q4-6 9-8\" fill=\"none\" stroke=\"#c6ffb0\" stroke-width=\"1.2\" opacity=\".7\"></path></g>\n<path d=\"M48 40v-8h24v8\" fill=\"none\" stroke=\"{{deep}}\" stroke-width=\"5\" stroke-linejoin=\"round\"></path>\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"><rect x=\"28\" y=\"40\" width=\"64\" height=\"16\" fill=\"#ffffff\" opacity=\".1\"></rect><path d=\"M28 56h64\" stroke=\"#ffffff\" stroke-opacity=\".3\" stroke-width=\"1\"></path></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></use>\n<rect x=\"54\" y=\"52\" width=\"12\" height=\"8\" rx=\"2\" fill=\"#ffd08a\"></rect>\n<g transform=\"translate(60 78)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<g transform=\"translate(86 22)\"><g class=\"fx\"><g transform=\"rotate(30)\"><rect x=\"-2.5\" y=\"-6\" width=\"5\" height=\"24\" rx=\"2.5\" fill=\"#d7dcef\"></rect><path d=\"M-7 -12a7 7 0 1 0 14 0l-3.5 3.5h-7z\" fill=\"#d7dcef\"></path><rect x=\"-1\" y=\"-4\" width=\"2\" height=\"18\" rx=\"1\" fill=\"#ffffff\" opacity=\".7\"></rect></g><circle cx=\"-12\" cy=\"-8\" r=\"2.4\" fill=\"#ffd08a\"></circle><circle cx=\"12\" cy=\"10\" r=\"2\" fill=\"#ffd08a\"></circle><path d=\"M-14 8l3 3M-11 8l-3 3\" stroke=\"#ffffff\" stroke-width=\"1.5\" stroke-linecap=\"round\"></path></g></g>\n</g>\n</svg>",
 "tome": "<svg viewBox=\"0 0 120 120\" aria-hidden=\"true\" style=\"display: block; width: 100%; height: 100%; overflow: visible;\">\n<defs><rect id=\"s{{u}}\" x=\"30\" y=\"28\" width=\"62\" height=\"78\" rx=\"9\"></rect><mask id=\"c{{u}}\" maskUnits=\"userSpaceOnUse\" x=\"-40\" y=\"-40\" width=\"280\" height=\"200\"><g fill=\"#ffffff\" stroke=\"none\"><rect x=\"30\" y=\"28\" width=\"62\" height=\"78\" rx=\"9\"></rect></g></mask></defs>\n<ellipse class=\"sh\" cx=\"60\" cy=\"115\" rx=\"26\" ry=\"4\" fill=\"#05021a\" opacity=\".45\"></ellipse>\n<ellipse class=\"fl\" cx=\"48\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse><ellipse class=\"fr\" cx=\"72\" cy=\"112\" rx=\"9\" ry=\"6\" fill=\"url(#base{{u}})\"></ellipse>\n<g class=\"bd\">\n<use href=\"#s{{u}}\" fill=\"url(#bodyg{{u}})\"></use>\n<g class=\"cg\" mask=\"url(#c{{u}})\"><rect x=\"30\" y=\"28\" width=\"12\" height=\"78\" fill=\"{{deep}}\" opacity=\".75\"></rect><path d=\"M42 28v78\" stroke=\"{{one}}\" stroke-opacity=\".5\" stroke-width=\"1\"></path></g>\n<use href=\"#s{{u}}\" fill=\"url(#sheen{{u}})\"></use>\n<use href=\"#s{{u}}\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1.6\"></use>\n<rect x=\"50\" y=\"38\" width=\"32\" height=\"5\" rx=\"2.5\" fill=\"#ffffff\" opacity=\".75\"></rect><rect x=\"50\" y=\"47\" width=\"22\" height=\"4\" rx=\"2\" fill=\"#ffffff\" opacity=\".45\"></rect>\n<g transform=\"translate(66 76)\" style=\"{{lidStyle}}\"><g class=\"ey\"><circle cx=\"-10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><circle cx=\"10\" cy=\"1\" r=\"12.5\" fill=\"url(#eglow{{u}})\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"{{deep}}\"></ellipse><g class=\"eg\" mask=\"url(#e{{u}})\"><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-28.5 -18.5) scale(.37)\"></rect><rect x=\"0\" y=\"0\" width=\"100\" height=\"100\" fill=\"url(#core{{u}})\" mask=\"url(#m{{u}})\" transform=\"translate(-8.5 -18.5) scale(.37)\"></rect><ellipse cx=\"-10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse><ellipse cx=\"10\" cy=\"7\" rx=\"7\" ry=\"5\" fill=\"{{one}}\" opacity=\".35\"></ellipse></g><circle cx=\"-8.8\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><circle cx=\"11.2\" cy=\"1.5\" r=\"2.5\" fill=\"#0b0726\"></circle><ellipse cx=\"-12.4\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><ellipse cx=\"7.6\" cy=\"-3.2\" rx=\"2.4\" ry=\"1.7\" fill=\"#ffffff\" opacity=\".9\"></ellipse><circle cx=\"-6.6\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><circle cx=\"13.4\" cy=\"4.2\" r=\".9\" fill=\"#ffffff\" opacity=\".7\"></circle><ellipse cx=\"-10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><ellipse cx=\"10\" cy=\"0\" rx=\"7\" ry=\"8\" fill=\"none\" stroke=\"url(#rim{{u}})\" stroke-width=\"1\"></ellipse><path d=\"M-17.6 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path><path d=\"M2.4 -1a7.6 8.6 0 0 1 15.2 0z\" fill=\"currentColor\"></path></g><g class=\"xx\"><path d=\"M-14 -4l8 8M-6 -4l-8 8M6 -4l8 8M14 -4l-8 8\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path></g><path class=\"mo\" d=\"M-5 12q5 4 10 0\" fill=\"none\" stroke=\"{{ink}}\" stroke-width=\"2.6\" stroke-linecap=\"round\"></path><g class=\"mo2\"><ellipse cx=\"0\" cy=\"13\" rx=\"4.4\" ry=\"3.6\" fill=\"{{ink}}\"></ellipse><ellipse cx=\"0\" cy=\"15\" rx=\"2.6\" ry=\"1.3\" fill=\"#ff7a9a\"></ellipse></g></g>\n<g class=\"ac\" style=\"transform-origin: 50% 0%;\"><rect x=\"86\" y=\"96\" width=\"10\" height=\"16\" fill=\"#93f7cc\"></rect><path d=\"M86 112l5-4 5 4z\" fill=\"#07041a\" opacity=\".55\"></path></g>\n<g transform=\"translate(104 40)\"><g class=\"fx\"><rect x=\"-9\" y=\"-7\" width=\"16\" height=\"12\" rx=\"1.5\" fill=\"#ffffff\" transform=\"rotate(-18)\"></rect><path d=\"M-6 -3h9M-6 0h7\" stroke=\"{{two}}\" stroke-width=\"1.2\" transform=\"rotate(-18)\"></path><rect x=\"4\" y=\"2\" width=\"12\" height=\"9\" rx=\"1.5\" fill=\"#fff2f7\" transform=\"rotate(14)\"></rect><rect x=\"-4\" y=\"10\" width=\"10\" height=\"7\" rx=\"1.2\" fill=\"{{one}}\" transform=\"rotate(-30)\"></rect></g></g>\n</g>\n</svg>"
};
  var SF_PAL = {
    pip:  ['#ffbf48', '#be4a1d', '#4a1406'],
    nib:  ['#ffb3e6', '#b8327f', '#3d0a2c'],
    volt: ['#b6ff8a', '#2f8f3a', '#0a2e12'],
    drip: ['#9fd0ff', '#2f5bd8', '#0a1a5c'],
    gem:  ['#e8ff8a', '#4f9c1d', '#163d06'],
    puff: ['#ffc8b4', '#c94a6a', '#43101f'],
    kit:  ['#ffa08f', '#b02a40', '#3a0812'],
    tome: ['#ffc6d8', '#a34068', '#36101f']
  };
  /* Each crew member moves differently: bounce height, squash (0 = rigid), lean into runs and lunges */
  var SF_FEEL = {
    pip:  { bob: 4,   sq: 1,   lean: 7 },
    nib:  { bob: 5,   sq: .9,  lean: 6 },
    volt: { bob: 2,   sq: 0,   lean: 4 },
    drip: { bob: 4,   sq: 1.8, lean: 6 },
    gem:  { bob: 3,   sq: 0,   lean: 5 },
    puff: { bob: 6,   sq: 1.2, lean: 4 },
    kit:  { bob: 2.5, sq: .5,  lean: 5 },
    tome: { bob: 3.5, sq: .4,  lean: 8 }
  };
  /* Frames per cycle; idle is held on threes, walk and death on twos, like hand-timed sprite sheets */
  var SF_FRAMES = { idle: 24, walk: 16, talk: 8, run: 8, punch: 8, jump: 8, death: 16 };
  var SF_SEQ = 0;
  function sfHue(hex, deg) {
    var r = parseInt(hex.slice(1, 3), 16) / 255, g = parseInt(hex.slice(3, 5), 16) / 255, b = parseInt(hex.slice(5, 7), 16) / 255;
    var max = Math.max(r, g, b), min = Math.min(r, g, b), l = (max + min) / 2, h = 0, s = 0, d = max - min;
    if (d) {
      s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
      h = max === r ? (g - b) / d + (g < b ? 6 : 0) : max === g ? (b - r) / d + 2 : (r - g) / d + 4;
      h *= 60;
    }
    h = ((h + deg) % 360 + 360) % 360;
    function f(n) { var k = (n + h / 30) % 12, a = s * Math.min(l, 1 - l); var c = l - a * Math.max(-1, Math.min(k - 3, 9 - k, 1)); return ('0' + Math.round(c * 255).toString(16)).slice(-2); }
    return '#' + f(0) + f(8) + f(4);
  }
  function sfMix(a, b, t) {
    var o = '#';
    for (var i = 1; i < 7; i += 2) { var x = parseInt(a.slice(i, i + 2), 16), y = parseInt(b.slice(i, i + 2), 16); o += ('0' + Math.round(x + (y - x) * t).toString(16)).slice(-2); }
    return o;
  }

  /* Draws (or re-poses) a character inside el. Changing only the pose keeps the
     SVG and just swaps classes, so the keyframes restart on the new pose. */
  function sprite(el, k, anim, fps, once, inplace) {
    if (!SF_FRAMES[anim]) anim = 'idle';
    fps = parseFloat(fps) || 12;
    var p = SF_PAL[k] || SF_PAL.pip, feel = SF_FEEL[k] || SF_FEEL.pip;
    if (el._k !== k) {
      var u = 'sf' + (++SF_SEQ) + Math.random().toString(36).slice(2, 6), delay = -(Math.random() * 3.2);
      var steps = [0, -30, -60, -90, -45, 0];
      var v = {
        u: u, one: p[0], two: p[1], deep: p[2],
        ink: k === 'volt' ? p[0] : '#1b1340',
        oneShift: steps.map(function (d) { return sfHue(p[0], d); }).join(';'),
        twoShift: steps.map(function (d) { return sfHue(p[1], d); }).join(';'),
        begin: delay.toFixed(2) + 's',
        delayStyle: '--d: ' + delay.toFixed(2) + 's;',
        defsStyle: 'position: absolute; width: 0; height: 0; overflow: hidden;',
        lidStyle: 'color: ' + (k === 'volt' ? p[2] : sfMix(p[0], p[1], .45)) + ';',
        bodyTop: sfMix(p[0], p[1], .45)
      };
      el.innerHTML = (SPR_DEFS + (SPR_BODY[k] || SPR_BODY.pip)).replace(/\{\{(\w+)\}\}/g, function (_, n) { return v[n]; });
      el._k = k;
    }
    var cls = 'spr k-' + k + ' a-' + anim;
    if (el.className === cls && el._fps === fps && el._once === !!once) return;
    el.className = cls; el._fps = fps; el._once = !!once;
    el.style.cssText = 'position: relative; display: block; width: 100%; aspect-ratio: 1; filter: drop-shadow(0 0 10px ' + p[0] + '55) drop-shadow(0 8px 18px ' + p[1] + '55); --bob: ' + feel.bob + '; --sq: ' + feel.sq + '; --lean: ' + feel.lean + '; --jy: ' + (inplace ? 0 : 1) + '; --dur: ' + (SF_FRAMES[anim] / fps).toFixed(3) + 's; --iter: ' + (once ? '1' : 'infinite') + '; --fill: ' + (once ? 'forwards' : 'none') + ';';
  }
  /* Restart a container's CSS entrance animation by swapping in a fresh copy,
     and return a new, empty element inside it to draw a character into */
  function fresh(el) { var n = el.cloneNode(false); el.parentNode.replaceChild(n, el); return n.appendChild(document.createElement('div')); }

  // Static characters in the markup: data-sprite="kind" data-anim="pose"
  var statics = document.querySelectorAll('[data-sprite]');
  for (var i = 0; i < statics.length; i++) sprite(statics[i], statics[i].getAttribute('data-sprite'), statics[i].getAttribute('data-anim') || 'idle', 12);

  /* ── 3. State ────────────────────────────────────────────────────────── */
  var st = { anim: 'idle', fps: '12', sel: 'pip', runner: 'pip', phase: 'ready', won: false, qi: 0, ans: [], done: false };

  /* ── 4. Hero: a random crew member throws a punch every few seconds ─── */
  var castFigs = document.querySelectorAll('#cast [data-sprite]');
  if (!reduced) {
    var heroT2;
    setInterval(function () {
      if (st.phase === 'run') return;
      var fig = castFigs[Math.floor(Math.random() * castFigs.length)];
      sprite(fig, fig._k, 'punch', 12);
      clearTimeout(heroT2);
      heroT2 = setTimeout(function () { sprite(fig, fig._k, 'idle', 12); }, 760);
    }, 2600);
  }

  /* ── 5. Toast ────────────────────────────────────────────────────────── */
  var toastEl = $('toast'), toastT;
  function toast(t) {
    clearTimeout(toastT);
    toastEl.textContent = t;
    toastEl.style.transform = 'translate(-50%, 0)'; toastEl.style.opacity = '1';
    toastT = setTimeout(function () { toastEl.style.transform = 'translate(-50%, 160%)'; toastEl.style.opacity = '0'; }, 2400);
  }

  /* ── 6. Crew: portraits, preview stage, pose + frame-rate controls ───── */
  function portraitStyle(on) {
    return 'position: relative; aspect-ratio: 1; padding: 0; border-radius: 24px; overflow: hidden; display: flex; align-items: center; justify-content: center; color: inherit; background: ' + (on ? 'radial-gradient(circle at 50% 35%, #3f2bb8, #170e55 75%)' : 'radial-gradient(circle at 50% 35%, #261a7a, #110a3e 75%)') + '; border: 1px solid ' + (on ? 'rgba(147, 247, 204, 0.9)' : 'rgba(255, 255, 255, 0.1)') + '; box-shadow: ' + (on ? '0 0 0 4px rgba(147, 247, 204, 0.12), 0 0 40px -6px rgba(147, 247, 204, 0.6), inset 0 0 26px rgba(147, 247, 204, 0.2)' : 'inset 0 1px 0 rgba(255, 255, 255, 0.06)') + ';';
  }
  function segStyle(on) {
    return 'color: ' + (on ? '#0b0726' : '#e3dcff') + '; background: ' + (on ? '#93f7cc' : 'rgba(255, 255, 255, 0.05)') + '; border: 1px solid ' + (on ? '#93f7cc' : 'rgba(255, 255, 255, 0.12)') + '; box-shadow: ' + (on ? '0 0 18px -4px rgba(147, 247, 204, 0.7)' : 'none') + ';';
  }
  var grid = $('crew-grid');
  grid.innerHTML = CREW.map(function (m) {
    return '<button class="portrait" type="button" role="radio" data-k="' + m.k + '" aria-label="' + m.name + ', ' + m.role + '">' +
      '<span style="display: block; width: 78%; margin: 0 auto; translate: 0 8%;"><span data-fig></span></span>' +
      '<span style="position: absolute; left: 0; right: 0; bottom: 10px; font: 500 11px/1 \'JetBrains Mono\', monospace; letter-spacing: 0.12em; text-transform: uppercase; color: #cfc8f5;">' + m.name + '</span></button>';
  }).join('');
  var portraits = grid.querySelectorAll('.portrait');
  for (i = 0; i < portraits.length; i++) sprite(portraits[i].querySelector('[data-fig]'), CREW[i].k, 'idle', 12);
  grid.addEventListener('click', function (e) { var b = e.target.closest('.portrait'); if (b) pick(b.getAttribute('data-k')); });
  grid.addEventListener('keydown', function (e) {
    var d = { ArrowRight: 1, ArrowDown: 1, ArrowLeft: -1, ArrowUp: -1 }[e.key];
    if (!d) return;
    e.preventDefault();
    var idx = (CREW.indexOf(crewOf(st.sel)) + d + CREW.length) % CREW.length;
    pick(CREW[idx].k);
    portraits[idx].focus();
  });

  $('anim-opts').innerHTML = ANIMS.map(function (v) {
    return '<label class="seg"><input type="radio" name="sf-anim" value="' + v + '" style="position: absolute; width: 1px; height: 1px; opacity: 0; margin: 0;"><span>' + v.charAt(0).toUpperCase() + v.slice(1) + '</span></label>';
  }).join('');
  $('anim-opts').addEventListener('change', function (e) { st.anim = e.target.value; renderPreview(false); });
  $('sf-fps').addEventListener('change', function (e) { st.fps = e.target.value; renderPreview(false); });

  var statsEl = $('cur-stats');
  statsEl.innerHTML = [0, 1, 2].map(function () {
    return '<div style="display: grid; grid-template-columns: 64px minmax(0, 1fr) 32px; gap: 12px; align-items: center; font: 500 12px/1 \'JetBrains Mono\', monospace; color: #cfc8f5;">' +
      '<span data-l></span><span role="img" style="display: block; height: 6px; border-radius: 99px; background: rgba(255, 255, 255, 0.1); overflow: hidden;"><span data-bar style="display: block; height: 100%; width: 0; border-radius: 99px; background: linear-gradient(90deg, #ff8fd8, #c9b8ff, #86b6ff); transition: width .5s;"></span></span>' +
      '<span data-v style="text-align: right; color: #fff;"></span></div>';
  }).join('');

  function pick(k) { if (k === st.sel) return; st.sel = k; renderCrew(); renderPreview(true); }
  function renderCrew() {
    var cur = crewOf(st.sel);
    for (var i = 0; i < portraits.length; i++) {
      var on = CREW[i].k === st.sel;
      portraits[i].setAttribute('aria-checked', on ? 'true' : 'false');
      portraits[i].tabIndex = on ? 0 : -1;
      portraits[i].style.cssText = portraitStyle(on);
    }
    $('cur-name').textContent = cur.name;
    $('cur-role').textContent = cur.role;
    $('cur-quote').textContent = cur.quote;
    var rows = statsEl.children;
    cur.stats.forEach(function (s, i) {
      rows[i].querySelector('[data-l]').textContent = s[0];
      rows[i].querySelector('[data-v]').textContent = s[1];
      rows[i].querySelector('[role=img]').setAttribute('aria-label', s[0] + ' ' + s[1] + ' out of 100');
      rows[i].querySelector('[data-bar]').style.width = s[1] + '%';
    });
    $('accept').textContent = st.runner === st.sel ? 'Ready to run' : 'Accept ' + cur.name;
  }
  var previewFig = null;
  function renderPreview(newKind) {
    if (newKind || !previewFig) previewFig = fresh($('preview'));
    sprite(previewFig, st.sel, st.anim, st.fps);
    $('state-label').textContent = st.anim + ' · ' + SF_FRAMES[st.anim] + 'f';
    $('fps-label').textContent = st.fps + ' FPS';
    var segs = $('anim-opts').querySelectorAll('.seg');
    for (var i = 0; i < segs.length; i++) {
      var on = ANIMS[i] === st.anim;
      segs[i].style.cssText = segStyle(on);
      segs[i].querySelector('input').checked = on;
    }
    if (st.phase !== 'run') sprite($('player-sprite'), st.runner, playerAnim(), st.fps, playerOnce(), true);
  }
  renderCrew();
  renderPreview(false);

  /* ── 7. Play: the 30-second runner ───────────────────────────────────── */
  var stage = $('stage'), obsLayer = $('obs-layer'), fxLayer = $('fx-layer'), player = $('player'), playerSpr = $('player-sprite');
  var bgFar = $('bg-far'), ground = $('ground'), dial = $('dial'), secs = $('secs'), meter = $('meter');
  var sim = null, raf = 0, last = 0, shownGot = -1;
  var OBST_SVG = {"books":"<svg viewBox=\"0 0 80 70\" width=\"66\" height=\"58\"><rect x=\"6\" y=\"46\" width=\"68\" height=\"20\" rx=\"4\" fill=\"#ff8fd8\"></rect><rect x=\"12\" y=\"26\" width=\"58\" height=\"20\" rx=\"4\" fill=\"#86b6ff\"></rect><rect x=\"4\" y=\"6\" width=\"62\" height=\"20\" rx=\"4\" fill=\"#93f7cc\"></rect><path d=\"M14 52h40M18 32h36M10 12h40\" stroke=\"#fff\" stroke-opacity=\".5\" stroke-width=\"3\" stroke-linecap=\"round\"></path></svg>","mug":"<svg viewBox=\"0 0 70 70\" width=\"56\" height=\"56\"><path d=\"M24 2q-6 8 0 14M36 2q-6 8 0 14\" fill=\"none\" stroke=\"#fff\" stroke-opacity=\".6\" stroke-width=\"3\" stroke-linecap=\"round\"></path><rect x=\"6\" y=\"20\" width=\"44\" height=\"48\" rx=\"8\" fill=\"#c9b8ff\"></rect><path d=\"M50 30h6a10 10 0 0 1 0 20h-6\" fill=\"none\" stroke=\"#c9b8ff\" stroke-width=\"7\"></path><rect x=\"6\" y=\"20\" width=\"44\" height=\"10\" rx=\"5\" fill=\"#2b1d73\"></rect></svg>","wifi":"<svg viewBox=\"0 0 70 96\" width=\"54\" height=\"74\"><rect x=\"32\" y=\"50\" width=\"6\" height=\"46\" fill=\"#8c7fd0\"></rect><circle cx=\"35\" cy=\"34\" r=\"30\" fill=\"#c13fd6\"></circle><circle cx=\"35\" cy=\"34\" r=\"23\" fill=\"#f3eaff\"></circle><path d=\"M22 34a18 18 0 0 1 26 0M27 40a10 10 0 0 1 16 0\" fill=\"none\" stroke=\"#3b2b9a\" stroke-width=\"4\" stroke-linecap=\"round\"></path><circle cx=\"35\" cy=\"46\" r=\"3\" fill=\"#3b2b9a\"></circle><path d=\"M18 18l34 34\" stroke=\"#c13fd6\" stroke-width=\"6\"></path></svg>","hurdle":"<svg viewBox=\"0 0 90 60\" width=\"76\" height=\"50\"><rect x=\"8\" y=\"14\" width=\"74\" height=\"14\" rx=\"3\" fill=\"#ece6ff\"></rect><path d=\"M14 14l10 14M34 14l10 14M54 14l10 14M74 14l6 9\" stroke=\"#86b6ff\" stroke-width=\"6\"></path><path d=\"M14 28v30M76 28v30\" stroke=\"#b3a6f0\" stroke-width=\"5\"></path></svg>","speaker":"<svg viewBox=\"0 0 60 80\" width=\"48\" height=\"66\"><rect x=\"2\" y=\"2\" width=\"56\" height=\"76\" rx=\"8\" fill=\"#c9b8ff\"></rect><rect x=\"40\" y=\"2\" width=\"18\" height=\"76\" rx=\"6\" fill=\"#8a75e6\"></rect><circle cx=\"22\" cy=\"24\" r=\"12\" fill=\"#2a1c7a\"></circle><circle cx=\"22\" cy=\"24\" r=\"5\" fill=\"#5b8cff\"></circle><circle cx=\"22\" cy=\"56\" r=\"14\" fill=\"#2a1c7a\"></circle><circle cx=\"22\" cy=\"56\" r=\"6\" fill=\"#5b8cff\"></circle></svg>"};
  var COIN_SVG = {"hour":"<svg viewBox=\"0 0 46 46\" width=\"46\" height=\"46\"><circle cx=\"23\" cy=\"23\" r=\"22\" fill=\"#ffb347\"></circle><circle cx=\"23\" cy=\"23\" r=\"16\" fill=\"#fff6e6\"></circle><path d=\"M16 13h14M16 33h14M17 13q0 8 6 10q6-2 6-10M17 33q0-8 6-10q6 2 6 10\" fill=\"#ffc46b\" stroke=\"#ff8a1f\" stroke-width=\"2\"></path></svg>","pencil":"<svg viewBox=\"0 0 46 46\" width=\"46\" height=\"46\"><circle cx=\"23\" cy=\"23\" r=\"22\" fill=\"#ffb347\"></circle><circle cx=\"23\" cy=\"23\" r=\"16\" fill=\"#fff6e6\"></circle><g transform=\"rotate(45 23 23)\"><rect x=\"19\" y=\"10\" width=\"8\" height=\"20\" rx=\"1\" fill=\"#ff8a1f\"></rect><path d=\"M19 30l4 7 4-7z\" fill=\"#2b1d73\"></path></g></svg>"};
  meter.innerHTML = '<span></span><span></span><span></span><span></span><span></span><span></span>';

  function playerAnim() { return st.phase === 'ready' ? 'idle' : st.phase === 'run' ? (sim && sim.y > 0.5 ? 'jump' : 'run') : (st.won ? 'punch' : 'death'); }
  function playerOnce() { return (st.phase === 'run' && !!sim && sim.y > 0.5) || (st.phase === 'end' && !st.won); }

  function startRun() {
    sim = { t: 0, y: 0, vy: 0, obs: [], coins: [], next: 1.4, ci: 0, got: 0, scroll: 0 };
    obsLayer.textContent = ''; fxLayer.textContent = ''; last = 0;
    st.phase = 'run';
    $('status').textContent = 'Run started. Thirty seconds.';
    showOverlays();
    stage.focus({ preventScroll: true });
    cancelAnimationFrame(raf);
    raf = requestAnimationFrame(loop);
  }
  function jump() { if (sim && st.phase === 'run' && sim.y <= 0.5) sim.vy = 760 * crewOf(st.runner).jump; }

  function addFx(cls, style, ms) {
    var el = document.createElement('i');
    el.className = cls; el.style.cssText = style;
    fxLayer.appendChild(el);
    setTimeout(function () { el.remove(); }, ms);
  }
  function burst(x, y, n, cols) {
    if (reduced) return;
    for (var i = 0; i < n; i++) {
      var a = Math.random() * Math.PI * 2, d = 40 + Math.random() * 70;
      addFx('spark', 'left:' + x.toFixed(0) + 'px;bottom:' + y.toFixed(0) + 'px;background:' + cols[i % cols.length] + ';--x:' + (Math.cos(a) * d).toFixed(1) + 'px;--y:' + (Math.sin(a) * d).toFixed(1) + 'px', 1000);
    }
  }
  function confetti(n) {
    if (reduced) return;
    var w = stage.clientWidth, cols = ['#ff8fd8', '#93f7cc', '#86b6ff', '#ffc46b', '#c9b8ff'];
    for (var i = 0; i < n; i++) addFx('conf', 'left:' + (Math.random() * w).toFixed(0) + 'px;background:' + cols[i % 5] + ';--x:' + (Math.random() * 120 - 60).toFixed(0) + 'px;--dur:' + (1.8 + Math.random() * 1.4).toFixed(2) + 's;animation-delay:' + (Math.random() * 0.6).toFixed(2) + 's', 3600);
  }

  function finish(won) {
    var s = sim, name = crewOf(st.runner).name, perfect = won && s.got === 6;
    var title = perfect ? 'Perfect run!' : won ? 'Shipped!' : 'Crunch!';
    var text = won ? (perfect ? 'All six coins and not a scratch. ' + name + ' is buying the coffee.' : 'You made it to the end with ' + s.got + ' of 6 coins.') : name + ' tripped over the clutter after ' + Math.floor(s.t) + ' seconds, with ' + s.got + ' of 6 coins.';
    var stars = won ? (s.got >= 6 ? 3 : s.got >= 3 ? 2 : 1) : 0;
    if (won) {
      var w = stage.clientWidth, h = stage.clientHeight;
      var sets = [['#ff8fd8', '#fff', '#c9b8ff'], ['#93f7cc', '#fff', '#86b6ff'], ['#ffc46b', '#ffb347', '#fff']];
      for (var i = 0; i < (perfect ? 6 : 3); i++) (function (i) { setTimeout(function () { burst(w * (0.15 + Math.random() * 0.7), h * (0.45 + Math.random() * 0.35), 26, sets[i % 3]); }, i * 260); })(i);
      confetti(perfect ? 90 : 50);
    }
    st.phase = 'end'; st.won = won;
    $('end-title').textContent = title;
    $('end-text').textContent = text;
    var starEls = $('end-stars').querySelectorAll('path');
    for (i = 0; i < starEls.length; i++) starEls[i].setAttribute('fill', i < stars ? '#ffc46b' : 'rgba(255, 255, 255, 0.16)');
    $('status').textContent = title + ' ' + text;
    showOverlays();
    draw();
  }

  function loop(now) {
    var s = sim;
    if (!s || st.phase !== 'run') return;
    var dt = last ? Math.min(0.05, (now - last) / 1000) : 0;
    last = now;
    s.t += dt;
    var sp = 300 + s.t * 9;
    s.scroll += sp * dt;
    s.vy -= 2100 * dt; s.y = Math.max(0, s.y + s.vy * dt); if (s.y === 0) s.vy = Math.max(0, s.vy);
    var W = stage.clientWidth;
    s.next -= dt;
    if (s.next <= 0 && s.t < RUN - 2) {
      var o = OBST[Math.floor(Math.random() * OBST.length)];
      s.obs.push(spawn({ k: o.k, x: W + 40, w: o.w, h: o.h }, OBST_SVG[o.k], ''));
      s.next = 1.1 + Math.random();
    }
    if (s.ci < 6 && s.t > 2.6 + s.ci * 4.2) {
      var ck = s.ci % 2 ? 'pencil' : 'hour';
      s.coins.push(spawn({ x: W + 40, y: s.ci % 2 ? 130 : 70, k: ck }, COIN_SVG[ck], 'coin'));
      s.ci++;
    }
    var px = PX + 16, pw = PW - 32, ph = PW * 0.82, dead = false;
    s.obs.forEach(function (o) { o.x -= sp * dt; if (o.x < px + pw && o.x + o.w - 8 > px && s.y < o.h - 10) dead = true; });
    s.obs = s.obs.filter(keep(-140));
    s.coins.forEach(function (c) {
      c.x -= sp * dt;
      if (!c.taken && c.x < px + pw && c.x + 46 > px && s.y + ph > c.y && s.y < c.y + 46) { c.taken = true; s.got++; burst(c.x + 23, 64 + c.y + 23, 14, ['#ffd9a0', '#ffb347', '#fff']); }
    });
    s.coins = s.coins.filter(function (c) { if (c.taken) { c.el.remove(); return false; } return keep(-60)(c); });
    if (dead) return finish(false);
    if (s.t >= RUN) return finish(true);
    draw();
    raf = requestAnimationFrame(loop);
  }
  function spawn(item, svg, kind) {
    var el = document.createElement('div');
    el.style.cssText = 'position: absolute; left: 0; bottom: 64px; z-index: 2;';
    el.innerHTML = kind === 'coin' ? '<div class="coinbob" style="filter: drop-shadow(0 0 12px rgba(255, 179, 71, 0.85));">' + svg + '</div>' : svg;
    obsLayer.appendChild(el);
    item.el = el;
    return item;
  }
  function keep(min) { return function (o) { if (o.x > min) return true; o.el.remove(); return false; }; }

  /* Per frame: move what moves, and only touch the rest when it changes */
  function draw() {
    var s = sim, t = s ? s.t : 0, scroll = s ? s.scroll : 0, y = s ? s.y : 0, got = s ? s.got : 0;
    var W = stage.clientWidth || 1200;
    var left = Math.max(0, RUN - (st.phase === 'ready' ? 0 : t)), prog = 1 - left / RUN;
    if (s) {
      s.obs.forEach(function (o) { o.el.style.transform = 'translateX(' + o.x.toFixed(1) + 'px)'; });
      s.coins.forEach(function (c) { c.el.style.transform = 'translate(' + c.x.toFixed(1) + 'px, ' + (-c.y) + 'px)'; });
    }
    bgFar.style.transform = 'translateX(' + (-(scroll * 0.18) % W).toFixed(1) + 'px)';
    ground.style.backgroundPosition = (-scroll % 64).toFixed(1) + 'px 0, 0 0';
    dial.style.background = 'conic-gradient(#ff8fd8 ' + (prog * 360).toFixed(1) + 'deg, rgba(255, 255, 255, 0.14) 0)';
    secs.textContent = Math.ceil(left);
    player.style.transform = 'translate(' + PX + 'px, ' + (-y).toFixed(1) + 'px)';
    sprite(playerSpr, st.runner, playerAnim(), st.fps, playerOnce(), true);
    if (got !== shownGot) {
      shownGot = got;
      meter.setAttribute('aria-label', 'Coins collected: ' + got + ' of 6');
      for (var i = 0; i < 6; i++) {
        var on = i < got;
        meter.children[i].style.cssText = 'display: block; width: 22px; height: 28px; border-radius: 8px; transition: background .3s, box-shadow .3s; background: ' + (on ? 'radial-gradient(circle at 40% 35%, #ffe2b0, #ffb347)' : 'rgba(255, 255, 255, 0.08)') + '; box-shadow: ' + (on ? '0 0 14px rgba(255, 179, 71, 0.85)' : 'inset 0 1px 0 rgba(255, 255, 255, 0.05)') + ';';
      }
    }
  }
  function showOverlays() {
    $('ready-ov').hidden = st.phase !== 'ready';
    $('end-ov').hidden = st.phase !== 'end';
    $('runner-name').textContent = crewOf(st.runner).name;
  }

  stage.addEventListener('keydown', function (e) {
    if (e.code !== 'Space' && e.code !== 'ArrowUp' && e.code !== 'KeyW') return;
    if (e.target && e.target.tagName === 'BUTTON') return;
    e.preventDefault();
    if (st.phase !== 'run') startRun(); else jump();
  });
  stage.addEventListener('pointerdown', function (e) {
    if (e.target.closest('button')) return;
    if (st.phase === 'run') { e.preventDefault(); jump(); }
  });
  draw();
  showOverlays();

  /* ── 8. Careers quiz ─────────────────────────────────────────────────── */
  function optStyle(on) {
    return 'display: flex; align-items: center; gap: 14px; min-height: 52px; padding: 12px 16px; border-radius: 16px; cursor: pointer; font-weight: 600; font-size: 16px; color: #f4f1ff; background: ' + (on ? 'rgba(147, 247, 204, 0.08)' : 'rgba(255, 255, 255, 0.035)') + '; border: 1px solid ' + (on ? 'rgba(147, 247, 204, 0.75)' : 'rgba(255, 255, 255, 0.09)') + ';';
  }
  $('q-dashes').innerHTML = QUIZ.map(function () { return '<span></span>'; }).join('');
  $('q-opts').addEventListener('change', function (e) { st.ans[st.qi] = e.target.value; renderAnswer(); });
  function renderQuestion() {
    var q = QUIZ[st.qi];
    $('q-count').textContent = 'QUESTION ' + (st.qi + 1) + ' / ' + QUIZ.length;
    $('q-q').textContent = q.q;
    $('q-opts').innerHTML = q.a.map(function (a) {
      return '<label class="opt"><input type="radio" name="q' + st.qi + '" value="' + a[1] + '" style="width: 18px; height: 18px; margin: 0; accent-color: #93f7cc;"><span>' + a[0] + '</span></label>';
    }).join('');
    $('q-back').hidden = st.qi === 0;
    $('q-next').textContent = st.qi === QUIZ.length - 1 ? 'See my role' : 'Next';
    var dashes = $('q-dashes').children;
    for (var i = 0; i < dashes.length; i++) dashes[i].style.cssText = 'display: block; width: 36px; height: 4px; border-radius: 99px; transition: background .3s; background: ' + (i <= st.qi ? '#c9b8ff' : 'rgba(255, 255, 255, 0.14)') + ';';
    renderAnswer();
  }
  function renderAnswer() {
    var labels = $('q-opts').querySelectorAll('.opt');
    for (var i = 0; i < labels.length; i++) {
      var input = labels[i].querySelector('input'), on = st.ans[st.qi] === input.value;
      input.checked = on;
      labels[i].style.cssText = optStyle(on);
    }
    $('q-next').disabled = !st.ans[st.qi];
  }
  function renderQuiz() {
    $('quiz-open').hidden = st.done;
    $('quiz-done').hidden = !st.done;
    if (!st.done) return renderQuestion();
    var score = { maker: 0, thinker: 0, organizer: 0 };
    st.ans.forEach(function (a) { score[a]++; });
    var best = Object.keys(score).sort(function (a, b) { return score[b] - score[a]; })[0], R = ROLES[best];
    sprite(fresh($('role-sprite')), R.k, 'talk', 12);
    $('role-type').textContent = best;
    $('role-role').textContent = R.role;
    $('role-mate').textContent = crewOf(R.k).name;
    $('role-text').textContent = R.text;
    $('role-meta').innerHTML = R.meta.map(function (m) {
      return '<span style="padding: 7px 12px; border-radius: 999px; background: rgba(255, 255, 255, 0.06); border: 1px solid rgba(255, 255, 255, 0.1); font: 500 12px/1 \'JetBrains Mono\', monospace; color: #e3dcff;">' + m + '</span>';
    }).join('');
  }
  renderQuiz();

  /* ── 9. Buttons: data-act="name" ─────────────────────────────────────── */
  var ACTS = {
    accept: function () {
      var cur = crewOf(st.sel);
      if (st.phase === 'run') { cancelAnimationFrame(raf); sim = null; obsLayer.textContent = ''; st.phase = 'ready'; }
      st.runner = st.sel;
      renderCrew(); showOverlays(); draw();
      toast(cur.name + ' is on the start line');
      $('play').scrollIntoView({ behavior: reduced ? 'auto' : 'smooth', block: 'start' });
    },
    start: startRun,
    back: function () { st.qi = Math.max(0, st.qi - 1); renderQuestion(); },
    next: function () {
      if (!st.ans[st.qi]) return;
      if (st.qi < QUIZ.length - 1) { st.qi++; renderQuestion(); } else { st.done = true; $('apply-msg').textContent = ''; renderQuiz(); }
    },
    retake: function () { st.qi = 0; st.ans = []; st.done = false; $('apply-msg').textContent = ''; renderQuiz(); },
    apply: function () { $('apply-msg').textContent = 'Demo only: nothing was sent. In the real thing this opens the application.'; }
  };
  document.addEventListener('click', function (e) {
    var b = e.target.closest('[data-act]');
    if (b && ACTS[b.getAttribute('data-act')]) ACTS[b.getAttribute('data-act')]();
  });

  /* ── 10. Tell the loader every character is drawn ──────────────────── */
  window.SF_SPRITE = sprite;
  document.dispatchEvent(new Event('sf:ready'));
})();
</script>
</body>
</html>
```

