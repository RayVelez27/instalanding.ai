INSTALANDING.AI · Auren AI Meditation Guide Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Auren AI Meditation Guide Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/auren-ai-meditation-guide-page

auren-ai-meditation.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Auren AI Meditation Guide Page
  slug     auren-ai-meditation-guide-page
  prompt   https://instalanding.ai/p/auren-ai-meditation-guide-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/auren-ai-meditation-guide-page
  license  Fictional brand ("Auren"); every member, quote, note and figure is invented.
           Replace names and copy before shipping. Every picture is CSS, SVG or a WebGL shader drawn in code; no image files.

  MAP
  tokens    one :root block at the top of the <style>: --bg, --fg, --muted, --gold / --gold-2, --card, --line,
            --aur (the aurora text gradient), --noise, --gut; DM Sans (light, optical sizing) and Instrument Serif italic
  sections  intro, nav, hero, method, practices, how-it-works, explore, stories, journal, footer (each carries data-section)
  scripts   one IIFE, no libraries: an ART library of 17 generative scenes (orb, mist ridges, app session, AI chat,
            aurora, moon, dunes, breath rings, silk waves, stones, ripple, night, bloom, ink, zen sand, window light,
            aura) painted into any [data-art] with a seeded RNG and paused off screen; a WebGL domain-warped fbm band;
            word-split headings; a counting intro; a fitted wordmark; sticky stacked cards; marquee rows; a stories
            carousel; a field-note dialog
  assets    no image files

  ADAPTING
  - Drop <div data-art="orb|mist|app|chat|aurora|moon|dunes|breath|waves|stones|ripple|night|petal|ink|zen|light|aura">
    anywhere; paint() builds it. Content lives in WORK, SVC, ROWS, QUOTES and NOTES.
  - prefers-reduced-motion: the intro is skipped, animations and transitions cut to near zero, marquees stop.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Auren — The AI meditation guide that listens</title>
<meta name="description" content="Auren is an AI meditation guide. It listens to how you arrive, then composes a session around your breath, your mood and your night.">
<meta name="theme-color" content="#09090b">
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Cdefs%3E%3CradialGradient id='g' cx='.38' cy='.32'%3E%3Cstop offset='0' stop-color='%23fff5e6'/%3E%3Cstop offset='.4' stop-color='%23ff8fae'/%3E%3Cstop offset='1' stop-color='%236b4cff'/%3E%3C/radialGradient%3E%3C/defs%3E%3Crect width='32' height='32' rx='8' fill='%2309090b'/%3E%3Ccircle cx='16' cy='16' r='8' fill='url(%23g)'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:opsz,wght@9..40,200..700&family=Instrument+Serif:ital@0;1&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#09090b;--fg:#f2eee7;--muted:#8e8a94;--gold:#d6b98a;--gold-2:#efdcb6;--ink:#09090b;
  --surface:#141317;--card:#121115;--card-h:#17161b;--line:rgba(255,255,255,.09);
  --ease:cubic-bezier(.22,1,.36,1);
  --aur:linear-gradient(100deg,#efdcb6 0%,#e7b98f 30%,#d7a3c9 62%,#a9c8e6 100%);
  --noise:url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg' width='180' height='180'><filter id='n'><feTurbulence type='fractalNoise' baseFrequency='.85' numOctaves='3' stitchTiles='stitch'/><feColorMatrix values='0 0 0 0 .5 0 0 0 0 .5 0 0 0 0 .5 0 0 0 1 0'/></filter><rect width='100%' height='100%' filter='url(%23n)'/></svg>");
  --gut:16px;
}
@media (min-width:768px){:root{--gut:30px}}
*{box-sizing:border-box;margin:0;padding:0}
html{background:var(--bg);-webkit-text-size-adjust:100%;scroll-behavior:smooth}
body{background:var(--bg);color:var(--fg);font-family:'DM Sans',system-ui,sans-serif;font-optical-sizing:auto;line-height:1.5;overflow-x:clip;-webkit-font-smoothing:antialiased}
a{color:inherit;text-decoration:none}
button{font:inherit;color:inherit;background:none;border:0;cursor:pointer}
ul,ol{list-style:none}
::selection{background:var(--gold);color:var(--ink)}
.sr-only{position:absolute!important;width:1px;height:1px;overflow:hidden;clip:rect(0 0 0 0);white-space:nowrap}
.skip{position:fixed;left:16px;top:-60px;z-index:200;background:var(--gold);color:var(--ink);padding:10px 20px;border-radius:99px;font-size:14px;font-weight:500;transition:top .3s}
.skip:focus{top:16px}
:focus-visible{outline:1px solid var(--gold);outline-offset:4px;border-radius:4px}
.serif{font-family:'Instrument Serif',serif;font-style:italic;font-weight:400;letter-spacing:-.02em}
.grad{background:var(--aur);-webkit-background-clip:text;background-clip:text;color:transparent}
.px{padding-left:var(--gut);padding-right:var(--gut)}
.eyebrow{font-size:14px;letter-spacing:.02em;color:var(--muted)}
.eyebrow b{color:var(--gold);font-weight:400;margin-right:6px}
.type-display{font-size:clamp(2.6rem,6vw,5.6rem);font-weight:300;line-height:1;letter-spacing:-.045em}
.type-xl{font-size:clamp(3.2rem,9vw,8.6rem);font-weight:300;line-height:.92;letter-spacing:-.055em}
.type-title{font-size:clamp(1.8rem,3.4vw,3rem);font-weight:300;line-height:1.05;letter-spacing:-.035em}

/* grain */
.grain{position:fixed;inset:-50%;z-index:95;pointer-events:none;background-image:var(--noise);opacity:.06;animation:grain 1s steps(6) infinite}
@keyframes grain{0%{transform:translate(0,0)}20%{transform:translate(-4%,3%)}40%{transform:translate(3%,-2%)}60%{transform:translate(-2%,-4%)}80%{transform:translate(4%,2%)}100%{transform:translate(0,0)}}


/* intro */
.intro{position:fixed;inset:0;z-index:120;overflow:hidden}
.intro .pn{position:absolute;inset-inline:0;height:calc(50% + 1px);background:var(--bg);transition:transform 1.1s var(--ease)}
.intro .pn.t{top:0}.intro .pn.b{bottom:0}
.intro.out .pn.t{transform:translateY(-100%)}.intro.out .pn.b{transform:translateY(100%)}
.intro .meta{position:absolute;top:0;inset-inline:0;height:72px;display:flex;align-items:center;justify-content:space-between;padding:0 var(--gut);font-size:11px;letter-spacing:.22em;text-transform:uppercase;color:var(--muted)}
.intro .mid{position:absolute;inset:0;display:grid;place-items:center}
.intro .grid{display:grid;gap:40px;align-items:center;justify-items:center}
@media(min-width:768px){.intro .grid{grid-template-columns:1fr auto 1fr;gap:56px}}
.intro .names{height:3.45em;overflow:hidden;font-size:clamp(1.9rem,4.4vw,3.9rem);font-weight:300;line-height:1;letter-spacing:-.05em;-webkit-mask-image:linear-gradient(transparent,#000 38%,#000 62%,transparent);mask-image:linear-gradient(transparent,#000 38%,#000 62%,transparent)}
.intro .names ul{padding-top:1.15em;transition:transform .5s var(--ease)}
.intro .names li{height:1.15em;display:flex;align-items:center;justify-content:center;white-space:nowrap;color:rgba(242,238,231,.3)}
.intro .names li.cur{color:var(--fg)}
@media(min-width:768px){.intro .names{justify-self:end;text-align:right}.intro .names li{justify-content:flex-end}}
.intro .thumb{width:clamp(96px,10vw,140px);aspect-ratio:4/5;border-radius:8px;overflow:hidden;position:relative;box-shadow:0 40px 120px -30px #000}
.intro .count{font-size:clamp(3.25rem,8vw,7.5rem);font-weight:200;line-height:1;letter-spacing:-.06em;font-variant-numeric:tabular-nums}
@media(min-width:768px){.intro .cnt{justify-self:start}}
.intro .bar{display:block;height:1px;background:var(--line);margin-top:12px}
.intro .bar i{display:block;height:100%;background:var(--aur);transform-origin:left;transform:scaleX(0)}
.intro .skipb{position:absolute;bottom:24px;right:clamp(1.25rem,4vw,3rem);font-size:11px;letter-spacing:.22em;text-transform:uppercase;color:var(--muted);padding:8px 0}
.intro .skipb:hover{color:var(--gold)}
.intro .mid,.intro .meta,.intro .skipb{transition:opacity .5s}
.intro.out .mid,.intro.out .meta,.intro.out .skipb{opacity:0}
.intro.gone{display:none}

/* header */
header.site{position:fixed;inset-inline:0;top:0;z-index:60;color:#fff;mix-blend-mode:difference;transition:transform .7s var(--ease)}
header.site.hide{transform:translateY(-100%)}
header .row{position:relative;height:72px;display:flex;align-items:center;padding:0 var(--gut)}
header .logo{position:absolute;left:var(--gut);top:50%;transform:translateY(-50%);font-weight:600;text-transform:uppercase;letter-spacing:-.06em;font-size:26px;opacity:0;pointer-events:none;transition:opacity .5s}
header.site.logo-on .logo{opacity:1;pointer-events:auto}
header nav{display:none;flex:1}
@media(min-width:768px){header nav{display:flex}header .logo{font-size:28px}}
header nav ul{display:flex;width:100%;justify-content:space-between;font-size:13px;text-transform:uppercase;letter-spacing:.04em}
header nav a{position:relative;display:inline-flex;padding:8px 0;color:rgba(255,255,255,.8);transition:color .3s}
header nav a:hover,header nav a.cur{color:#fff}
header nav a::after{content:"";position:absolute;inset-inline:0;bottom:4px;height:1px;background:#fff;transform:scaleX(0);transform-origin:left;transition:transform .5s var(--ease)}
header nav a:hover::after,header nav a.cur::after{transform:scaleX(1)}
header nav li:first-child{min-width:clamp(80px,12vw,160px)}
.burger{margin-left:auto;width:44px;height:44px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px}
.burger i{display:block;height:1px;width:24px;background:#fff;transition:transform .4s var(--ease),width .4s}
.burger i+i{width:16px;align-self:flex-end;margin-right:10px}
@media(min-width:768px){.burger{display:none}}
.mmenu{position:fixed;inset:0;z-index:58;background:var(--bg);display:flex;flex-direction:column;justify-content:flex-end;padding:96px var(--gut) 40px;clip-path:inset(0 0 100% 0);transition:clip-path .8s var(--ease)}
.mmenu.open{clip-path:inset(0)}
.mmenu a{display:block;font-size:clamp(3rem,15vw,5rem);font-weight:300;letter-spacing:-.05em;line-height:1.05}
.mmenu a span{color:var(--gold);font-size:14px;letter-spacing:0;vertical-align:top;margin-right:10px}
.mmenu p{margin-top:40px;color:var(--muted);font-size:14px}
body.menu-open .burger i:first-child{transform:translateY(3.5px) rotate(45deg)}
body.menu-open .burger i+i{width:24px;margin-right:0;transform:translateY(-3.5px) rotate(-45deg)}

/* ================= ART ================= */
.art{position:absolute;inset:0;overflow:hidden;background:#0c0b10;container-type:size;isolation:isolate}
.art>*{position:absolute;display:block}
.art::before{content:"";position:absolute;inset:0;z-index:19;pointer-events:none;background:radial-gradient(120% 100% at 50% 50%,transparent 55%,rgba(0,0,0,.35) 100%)}
.art::after{content:"";position:absolute;inset:0;background-image:var(--noise);opacity:.16;mix-blend-mode:overlay;pointer-events:none;z-index:20}
.art.light::before{background:radial-gradient(120% 100% at 50% 50%,transparent 60%,rgba(60,40,20,.18) 100%)}
.art.off *{animation-play-state:paused!important}
.st{position:absolute;border-radius:50%;background:#fff}
.st.tw{animation:tw 4s ease-in-out infinite}
@keyframes tw{50%{opacity:.15}}
@keyframes breathe{50%{transform:scale(1.07);opacity:.85}}
@keyframes rot{to{transform:rotate(360deg)}}
@keyframes drift{50%{transform:translateX(6%)}}
@keyframes inhale{0%,100%{transform:translate(-50%,-50%) scale(.8)}50%{transform:translate(-50%,-50%) scale(1)}}

/* orb */
.a-orb{background:radial-gradient(120% 90% at 50% 28%,#211a36 0%,#0c0a14 52%,#050507 100%)}
.ob-floor{left:0;right:0;bottom:0;height:33%;background:linear-gradient(180deg,rgba(255,255,255,.035),transparent 50%),linear-gradient(180deg,#0f0d17,#050507);box-shadow:0 -1px 0 rgba(255,255,255,.05)}
.ob-glow{left:50%;top:42%;width:95%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,rgba(160,120,255,.28),rgba(255,140,120,.08) 40%,transparent 62%);filter:blur(3cqw);animation:breathe 9s ease-in-out infinite}
.ob-caustic{left:20%;right:20%;bottom:13%;height:15%;border-radius:50%;background:conic-gradient(from 90deg,#ffb36b66,#ff6bd666,#7a6bff66,#6bd4ff55,#b8ff9e44,#ffb36b66);filter:blur(3.2cqw);animation:breathe 9s ease-in-out infinite}
.ob-shadow{left:33%;right:33%;bottom:25.5%;height:4%;border-radius:50%;background:radial-gradient(ellipse,rgba(0,0,0,.95),transparent 70%);filter:blur(.8cqw)}
.ob{left:50%;top:42%;width:min(48cqw,52cqh);aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;overflow:hidden;animation:inhale2 9s ease-in-out infinite;box-shadow:0 5cqw 12cqw rgba(0,0,0,.65),0 0 8cqw rgba(170,130,255,.25)}
@keyframes inhale2{0%,100%{transform:translate(-50%,-50%) scale(.96)}50%{transform:translate(-50%,-50%) scale(1.04)}}
.ob i{position:absolute;border-radius:50%}
.ob .c1{inset:-35%;background:conic-gradient(from 0deg,#ff9a62,#ff4f9e,#7a5cff,#33c8ff,#9effc6,#ffd36b,#ff9a62);filter:blur(5cqw);animation:rot 16s linear infinite;opacity:.9}
.ob .c2{inset:-20%;background:conic-gradient(from 180deg,transparent,#ffffff55,transparent 30%,#7a5cff88,transparent 60%);filter:blur(3cqw);animation:rot 11s linear infinite reverse;mix-blend-mode:screen}
.ob .c3{inset:0;background:radial-gradient(circle at 50% 118%,rgba(255,255,255,.45),transparent 45%),radial-gradient(circle at 50% 46%,transparent 40%,rgba(12,8,24,.5) 70%,rgba(8,6,16,.92) 100%)}
.ob .c4{left:17%;top:9%;width:42%;height:26%;background:radial-gradient(ellipse at 50% 45%,rgba(255,255,255,.9),rgba(255,255,255,0) 70%);filter:blur(.5cqw);transform:rotate(-28deg)}
.ob .c5{inset:0;box-shadow:inset 0 0 0 .25cqw rgba(255,255,255,.14),inset -2cqw -3cqw 6cqw rgba(255,255,255,.14),inset 2cqw 2cqw 5cqw rgba(0,0,0,.3)}

/* mist ridges at dawn */
.a-mist{background:linear-gradient(180deg,#0a0d1c 0%,#1d2040 22%,#47395c 40%,#a7677a 54%,#eaa07e 63%,#f6d1a3 70%,#f9e2bf 74%)}
.mi-sun{left:50%;top:67%;width:70%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,#fff8e8 0,#ffe0ae 5%,rgba(255,196,145,.5) 20%,rgba(255,170,140,.12) 42%,transparent 62%);animation:breathe 12s ease-in-out infinite}
.mi-r{left:0;bottom:0;width:100%;height:56%}
.mi-fog{left:-20%;width:140%;height:12%;background:linear-gradient(180deg,transparent,rgba(255,226,210,.22),transparent);filter:blur(1.4cqw);animation:drift 18s ease-in-out infinite}

/* app session screen */
.a-app{background:radial-gradient(90% 60% at 50% 35%,#2a2045 0%,#0e0b16 58%,#060608 100%)}
.ap-halo{left:50%;top:48%;width:120%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,rgba(140,100,255,.3),rgba(255,140,110,.1) 35%,transparent 60%);filter:blur(4cqw);animation:breathe 8s ease-in-out infinite}
.ap-floor{left:15%;right:15%;bottom:2%;height:8%;border-radius:50%;background:radial-gradient(ellipse,rgba(170,140,255,.35),transparent 70%);filter:blur(2cqw)}
.ap-ph{--pw:min(58cqw,38cqh);left:50%;top:50%;width:var(--pw);aspect-ratio:9/19.3;transform:translate(-50%,-50%) rotate(var(--tilt,0deg));border-radius:calc(var(--pw)*.16);padding:calc(var(--pw)*.028);background:linear-gradient(145deg,#6a6a73 0%,#1a1a1f 24%,#2f2f37 60%,#0e0e12 100%);box-shadow:inset 0 0 0 calc(var(--pw)*.006) rgba(255,255,255,.18),0 calc(var(--pw)*.12) calc(var(--pw)*.3) rgba(0,0,0,.7);font-size:calc(var(--pw)*.052)}
.ap-scr{position:relative;height:100%;border-radius:calc(var(--pw)*.135);overflow:hidden;background:radial-gradient(80% 38% at 15% 0%,rgba(122,92,255,.55),transparent 70%),radial-gradient(60% 34% at 100% 12%,rgba(255,140,100,.38),transparent 70%),radial-gradient(90% 45% at 50% 105%,rgba(60,190,220,.22),transparent 70%),#0b0a12;color:#f2eee7;display:flex;flex-direction:column;padding:2.4em 1.3em 1.5em;font-family:'DM Sans',sans-serif}
.ap-scr::after{content:"";position:absolute;inset:0;background:linear-gradient(125deg,rgba(255,255,255,.1),transparent 30%);pointer-events:none}
.ap-isl{position:absolute;top:.65em;left:50%;width:30%;height:1.35em;transform:translateX(-50%);background:#000;border-radius:1em}
.ap-top{display:flex;justify-content:space-between;font-size:.58em;color:rgba(255,255,255,.55);letter-spacing:.14em;text-transform:uppercase}
.ap-h{margin-top:.7em;font-family:'Instrument Serif',serif;font-style:italic;font-size:1.95em;line-height:.95;letter-spacing:-.02em}
.ap-sub{font-size:.62em;color:rgba(255,255,255,.55);margin-top:.5em}
.ap-br{position:relative;flex:1;min-height:0}
.ap-br .ring{position:absolute;left:50%;top:50%;width:var(--s);aspect-ratio:1;border-radius:50%;border:1px solid rgba(255,255,255,.13);animation:inhale 8s ease-in-out infinite;animation-delay:var(--d,0s)}
.ap-core{position:absolute;left:50%;top:50%;width:44%;aspect-ratio:1;border-radius:50%;overflow:hidden;animation:inhale 8s ease-in-out infinite;box-shadow:0 0 3em rgba(255,130,170,.5),0 0 6em rgba(122,92,255,.45)}
.ap-core i{position:absolute;inset:-30%;background:conic-gradient(from 0deg,#ffb37a,#ff6fa8,#8a6bff,#5ad2ff,#ffb37a);filter:blur(1.2em);animation:rot 10s linear infinite}
.ap-core b{position:absolute;inset:0;border-radius:50%;background:radial-gradient(circle at 36% 30%,rgba(255,255,255,.85),transparent 26%),radial-gradient(circle,transparent 50%,rgba(10,6,20,.45) 100%)}
.ap-say{position:relative;height:1.3em;margin-top:.4em}
.ap-say span{position:absolute;inset:0;text-align:center;font-size:.68em;letter-spacing:.24em;text-transform:uppercase;color:rgba(255,255,255,.8);opacity:0;animation:say 8s infinite}
.ap-say span+span{animation-delay:4s}
@keyframes say{0%{opacity:0}8%,40%{opacity:1}50%,100%{opacity:0}}
.ap-prog{margin-top:1em;height:2px;border-radius:2px;background:rgba(255,255,255,.12);overflow:hidden}
.ap-prog i{display:block;height:100%;width:64%;background:var(--aur)}
.ap-time{display:flex;justify-content:space-between;font-size:.55em;color:rgba(255,255,255,.5);margin-top:.6em;font-variant-numeric:tabular-nums}
.ap-ctl{margin-top:1em;display:flex;justify-content:center;align-items:center;gap:1.1em}
.ap-ctl span{width:2.2em;height:2.2em;border-radius:50%;display:grid;place-items:center;background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.12)}
.ap-ctl span.p{width:3.2em;height:3.2em;background:#f2eee7;color:#111;border:0;box-shadow:0 0 2em rgba(255,255,255,.25)}
.ap-ctl svg{width:42%;height:42%}

/* ai chat */
.a-chat{background:radial-gradient(60% 50% at 15% 15%,#40308a 0,transparent 62%),radial-gradient(55% 50% at 95% 85%,#8a3f2c 0,transparent 62%),radial-gradient(50% 40% at 70% 20%,#1f4b5c 0,transparent 60%),#09090f}
.ch-blob{width:60%;aspect-ratio:1;border-radius:50%;filter:blur(6cqw);opacity:.6;animation:drift 14s ease-in-out infinite}
.ch-card{left:9%;right:9%;top:12%;bottom:12%;border-radius:4cqmin;padding:4.5cqmin;background:linear-gradient(160deg,rgba(255,255,255,.1),rgba(255,255,255,.03));border:1px solid rgba(255,255,255,.14);backdrop-filter:blur(2.4cqmin);-webkit-backdrop-filter:blur(2.4cqmin);box-shadow:0 4cqmin 10cqmin rgba(0,0,0,.45),inset 0 1px 0 rgba(255,255,255,.15);display:flex;flex-direction:column;gap:2.6cqmin;font-size:3.1cqmin;color:#f2eee7;overflow:hidden}
.ch-hd{display:flex;align-items:center;gap:2cqmin;font-size:.85em}
.ch-hd i{width:4.2cqmin;height:4.2cqmin;border-radius:50%;background:radial-gradient(circle at 36% 30%,#fff5e6,#ff8fae 45%,#6b4cff);box-shadow:0 0 3cqmin rgba(255,140,180,.6);animation:breathe 4s ease-in-out infinite}
.ch-hd small{margin-left:auto;color:rgba(255,255,255,.5);font-size:.85em;letter-spacing:.06em}
.ch-b{max-width:84%;padding:2.2cqmin 2.8cqmin;border-radius:3cqmin;line-height:1.35;background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.08)}
.ch-b.me{align-self:flex-end;background:linear-gradient(135deg,rgba(239,220,182,.95),rgba(214,185,138,.9));color:#1a140c;border:0;border-bottom-right-radius:.8cqmin}
.ch-b.ai{border-bottom-left-radius:.8cqmin}
.ch-wave{margin-top:auto;display:flex;align-items:center;gap:.9cqmin;height:9cqmin}
.ch-wave i{flex:1;border-radius:1cqmin;background:var(--aur);height:var(--h);animation:wv 1.6s ease-in-out infinite;animation-delay:var(--d)}
@keyframes wv{50%{transform:scaleY(.35)}}

/* aurora */
.a-aurora{background:linear-gradient(180deg,#02030a 0%,#06101f 45%,#0b1b2b 70%,#04070c 74%,#02040a 100%)}
.ar-c{left:-25%;width:150%;height:62%;mix-blend-mode:screen;filter:blur(2.2cqw);animation:sway 16s ease-in-out infinite}
.ar-c1{top:2%;background:radial-gradient(55% 32% at 50% 55%,rgba(70,255,190,.85),rgba(40,200,160,.25) 45%,transparent 75%);transform:skewX(-24deg) rotate(-10deg)}
.ar-c2{top:-6%;background:radial-gradient(45% 26% at 62% 50%,rgba(150,95,255,.7),transparent 72%);transform:skewX(18deg) rotate(6deg);animation-delay:-5s}
.ar-c3{top:14%;background:radial-gradient(40% 20% at 35% 50%,rgba(255,110,190,.45),transparent 75%);transform:skewX(-12deg) rotate(-3deg);animation-delay:-9s}
@keyframes sway{50%{translate:5% -2%;scale:1.05}}
.ar-str{inset:0 0 30% 0;background:repeating-linear-gradient(90deg,rgba(255,255,255,.07) 0 .25%,transparent .25% 1.1%);-webkit-mask-image:radial-gradient(60% 45% at 50% 40%,#000,transparent 75%);mask-image:radial-gradient(60% 45% at 50% 40%,#000,transparent 75%);mix-blend-mode:overlay}
.ar-hills{left:0;width:100%;bottom:25%;height:16%}
.ar-lake{left:0;right:0;bottom:0;height:26%;background:repeating-linear-gradient(180deg,rgba(255,255,255,.05) 0 .3cqh,transparent .3cqh 1.4cqh),radial-gradient(50% 60% at 45% 0%,rgba(70,255,190,.35),transparent 70%),radial-gradient(40% 50% at 65% 0%,rgba(150,95,255,.25),transparent 70%),#03060b}

/* moon over water */
.a-moon{background:linear-gradient(180deg,#04060e 0%,#0d1430 40%,#1e2a4c 58.5%,#0a1020 59%,#03050b 100%)}
.mn-halo{left:50%;top:27%;width:80%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,rgba(255,245,220,.28),rgba(160,180,255,.12) 30%,transparent 60%)}
.mn{left:50%;top:27%;width:min(22cqw,30cqh);aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(40% 32% at 60% 58%,rgba(120,110,95,.22),transparent 70%),radial-gradient(26% 22% at 32% 66%,rgba(120,110,95,.18),transparent 70%),radial-gradient(34% 26% at 46% 30%,rgba(120,110,95,.14),transparent 70%),radial-gradient(circle at 36% 34%,#fffbf2,#efe8da 42%,#c9c1b1 78%,#9d968a);box-shadow:inset -1.2cqw -1cqw 2.4cqw rgba(60,55,70,.35),0 0 5cqw rgba(255,245,220,.55),0 0 18cqw rgba(160,180,255,.22)}
.mn-hz{left:-10%;right:-10%;top:55%;height:6%;background:linear-gradient(transparent,rgba(190,200,240,.18),transparent);filter:blur(1cqw)}
.mn-ref{left:50%;top:59.5%;width:22%;height:40%;transform:translateX(-50%);background:repeating-linear-gradient(180deg,rgba(255,246,225,.85) 0 .45cqh,transparent .45cqh 1.5cqh);-webkit-mask-image:radial-gradient(50% 100% at 50% 0%,#000 10%,transparent 75%);mask-image:radial-gradient(50% 100% at 50% 0%,#000 10%,transparent 75%);filter:blur(.25cqw);animation:shim 3.5s ease-in-out infinite}
@keyframes shim{50%{transform:translateX(-50%) scaleX(1.35);opacity:.7}}
.mn-hills{left:0;width:100%;top:53%;height:6%}

/* dunes */
.a-dunes{background:linear-gradient(180deg,#241a36 0%,#6a3f5a 22%,#c97f62 42%,#f0b989 56%)}
.du-sun{left:64%;top:44%;width:50%;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,#fff3db 0,#ffd8a0 7%,rgba(255,180,130,.35) 25%,transparent 60%)}
.a-dunes svg{inset:0;width:100%;height:100%}

/* breath */
.a-breath{background:radial-gradient(circle at 50% 50%,#1e1636 0,#0a0812 62%,#050407 100%)}
.br-ring{left:50%;top:50%;width:var(--s);aspect-ratio:1;border-radius:50%;border:1px solid rgba(239,220,182,var(--o));animation:inhale 8s ease-in-out infinite;animation-delay:var(--d)}
.br-core{left:50%;top:50%;width:min(30cqw,30cqh);aspect-ratio:1;border-radius:50%;overflow:hidden;animation:inhale 8s ease-in-out infinite;box-shadow:0 0 8cqmin rgba(255,150,170,.45),0 0 18cqmin rgba(122,92,255,.35)}
.br-core i{position:absolute;inset:-30%;background:conic-gradient(from 90deg,#ffc08a,#ff7fae,#9a7bff,#69d6ff,#ffc08a);filter:blur(4cqmin);animation:rot 12s linear infinite}
.br-core b{position:absolute;inset:0;border-radius:50%;background:radial-gradient(circle at 36% 30%,rgba(255,255,255,.8),transparent 28%),radial-gradient(circle,transparent 48%,rgba(10,6,20,.45))}
.br-orb{left:50%;top:50%;width:0;height:0;animation:rot 50s linear infinite}
.br-orb span{position:absolute;border-radius:50%;background:#fff3dc;box-shadow:0 0 1.2cqmin #ffd9a8}
.br-t{left:0;right:0;bottom:9%;height:4cqmin}
.br-t span{position:absolute;inset:0;text-align:center;font-size:2.6cqmin;letter-spacing:.32em;text-transform:uppercase;color:rgba(239,220,182,.85);opacity:0;animation:say 8s infinite}
.br-t span+span{animation-delay:4s}

/* silk waves */
.a-waves{background:radial-gradient(80% 60% at 50% 50%,#17112b,#07060b 75%)}
.a-waves svg{left:-25%;top:0;width:150%;height:100%}
.wv-g{animation:wdrift 14s ease-in-out infinite alternate}
@keyframes wdrift{to{transform:translateX(-12%)}}

/* stones */
.a-stones{background:radial-gradient(90% 70% at 50% 25%,#ece7df 0,#d4ccbf 52%,#aaa093 100%)}
.sn-ground{left:0;right:0;bottom:0;height:34%;background:linear-gradient(180deg,rgba(255,255,255,.25),transparent 18%),linear-gradient(180deg,#c9c0b2,#a59a8b)}
.sn-sh{border-radius:50%;background:radial-gradient(ellipse,rgba(30,25,20,.55),transparent 70%);filter:blur(1cqw)}
.sn{border-radius:50%;box-shadow:inset 0 .8cqw 1.4cqw rgba(255,255,255,.22),inset 0 -1.2cqw 2cqw rgba(0,0,0,.35)}
.sn-light{inset:0;background:radial-gradient(60% 50% at 20% 10%,rgba(255,250,240,.5),transparent 60%);mix-blend-mode:soft-light}

/* ripple */
.a-ripple{background:radial-gradient(circle at 50% 50%,#17304a 0,#0a1622 52%,#03070b 100%);perspective:80cqw}
.rp{left:50%;top:54%;width:150%;aspect-ratio:1;transform:translate(-50%,-50%) rotateX(64deg)}
.rp i{position:absolute;left:50%;top:50%;width:0;aspect-ratio:1;border-radius:50%;transform:translate(-50%,-50%);border:1.5px solid rgba(200,232,255,.7);box-shadow:0 0 2cqw rgba(140,200,255,.45),inset 0 0 2cqw rgba(140,200,255,.25);animation:rip 7s cubic-bezier(.2,.6,.3,1) infinite;animation-delay:var(--d)}
@keyframes rip{0%{width:0;opacity:1}100%{width:90%;opacity:0}}
.rp-drop{left:50%;top:54%;width:2.4cqmin;aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:#e9f6ff;box-shadow:0 0 4cqmin 1cqmin rgba(170,220,255,.75);animation:breathe 3.5s ease-in-out infinite}
.rp-sheen{inset:0;background:linear-gradient(160deg,rgba(255,255,255,.08),transparent 40%),radial-gradient(40% 30% at 70% 15%,rgba(214,185,138,.25),transparent 70%)}

/* night */
.a-night{background:linear-gradient(180deg,#02030a 0%,#090c22 52%,#191637 80%,#2b1c3c 100%)}
.nt-mw{left:-20%;top:20%;width:140%;height:26%;transform:rotate(-24deg);background:radial-gradient(50% 50% at 50% 50%,rgba(190,170,255,.22),rgba(255,190,200,.06) 50%,transparent 75%);filter:blur(2cqw)}
.nt-moon{left:72%;top:22%;width:min(13cqw,18cqh);aspect-ratio:1;transform:translate(-50%,-50%) rotate(-20deg);border-radius:50%;box-shadow:inset calc(min(13cqw,18cqh)*-.22) calc(min(13cqw,18cqh)*.08) 0 0 #f6ecd6;filter:drop-shadow(0 0 2cqw rgba(255,240,210,.6))}
.nt-cl{border-radius:50%;filter:blur(4cqw);background:#2c2048;opacity:.85}

/* bloom */
.a-petal{background:radial-gradient(circle at 50% 50%,#28162e 0,#0b070e 62%,#050407 100%)}
.pt{left:50%;top:50%;width:0;height:0;animation:rot 80s linear infinite}
.pt i{position:absolute;left:0;top:calc(var(--h) / -2);width:var(--w);height:var(--h);transform-origin:0 50%;transform:rotate(var(--a));border-radius:50%;background:linear-gradient(90deg,rgba(255,200,170,0) 0%,var(--c1) 55%,var(--c2) 100%);mix-blend-mode:screen;box-shadow:inset 0 0 0 1px rgba(255,255,255,.06)}
.pt-core{left:50%;top:50%;width:min(16cqw,16cqh);aspect-ratio:1;transform:translate(-50%,-50%);border-radius:50%;background:radial-gradient(circle,#fff6e2 0,#ffd2a1 25%,rgba(255,150,170,.4) 55%,transparent 72%);animation:breathe 6s ease-in-out infinite}

/* ink */
.a-ink{background:radial-gradient(circle at 50% 40%,#f8f4ed,#e6dfd2 70%,#d2c8b8)}
.a-ink svg{inset:0;width:100%;height:100%}
.ink-g{transform-origin:50% 50%;animation:rot 90s linear infinite}

/* zen sand */
.a-zen{background:#d8d0c2}
.a-zen svg{inset:0;width:100%;height:100%}
.zn-light{inset:0;background:radial-gradient(70% 60% at 15% 10%,rgba(255,250,240,.45),transparent 60%),linear-gradient(200deg,transparent 60%,rgba(80,60,40,.18));mix-blend-mode:soft-light}

/* window light */
.a-light{background:linear-gradient(140deg,#efe2cf 0%,#dcc7ab 55%,#b9987a 100%)}
.lt-win{left:28%;top:6%;width:62%;height:82%;transform:skew(-16deg) rotate(3deg);filter:blur(.5cqw)}
.lt-win>i{position:absolute;inset:0;background:linear-gradient(170deg,rgba(255,250,236,.95),rgba(255,232,196,.7));box-shadow:0 0 6cqw rgba(255,240,210,.7)}
.lt-win>b{position:absolute;background:rgba(185,150,115,.55)}
.lt-leaf{left:40%;top:10%;width:56%;height:70%;filter:blur(.8cqw);opacity:.55;transform-origin:80% 0;animation:leaf 9s ease-in-out infinite}
@keyframes leaf{50%{transform:rotate(3deg) translateX(1%)}}
.lt-vase{left:12%;bottom:0;width:22%;height:32%;border-radius:45% 45% 8% 8%/60% 60% 8% 8%;background:radial-gradient(circle at 70% 30%,#f4ebdd,#cbb89d 45%,#8f7a60);box-shadow:3cqw 1cqw 4cqw rgba(90,60,30,.3)}
.lt-vase2{left:17%;bottom:30%;width:12%;height:6%;border-radius:50%;background:#7a6650}
.lt-dust{inset:0}
.lt-dust span{position:absolute;border-radius:50%;background:#fff8e6;box-shadow:0 0 .8cqmin #fff;animation:mote linear infinite}
@keyframes mote{0%{transform:translate(0,0);opacity:0}20%{opacity:.9}80%{opacity:.9}100%{transform:translate(6cqw,-14cqh);opacity:0}}

/* aura bg */
.a-aura{background:#09080c}
.au{border-radius:50%;filter:blur(9cqmin);animation:auramove 22s ease-in-out infinite alternate}
.au-1{left:-10%;top:0;width:70%;aspect-ratio:1;background:radial-gradient(circle,#4a2f8a,transparent 65%)}
.au-2{right:-15%;top:30%;width:70%;aspect-ratio:1;background:radial-gradient(circle,#8a4a2a,transparent 65%);animation-delay:-8s}
.au-3{left:25%;bottom:-25%;width:60%;aspect-ratio:1;background:radial-gradient(circle,#1d4a55,transparent 65%);animation-delay:-14s}
@keyframes auramove{50%{transform:translate(8%,-6%) scale(1.1)}100%{transform:translate(-6%,5%) scale(.95)}}

/* reveal */
[data-reveal]{opacity:0;transform:translateY(36px);transition:opacity 1.1s var(--ease),transform 1.1s var(--ease)}
[data-reveal="left"]{transform:translateX(-70px)}
[data-reveal].in{opacity:1;transform:none}
.rm{display:inline-block;overflow:hidden;vertical-align:top;padding-bottom:.2em;margin-bottom:-.2em}
.rw{display:inline-block;transform:translateY(105%);transition:transform 1.1s var(--ease)}
.in .rw,.rw.in{transform:none}

/* hero */
.hero{padding-top:72px}
.wm{padding:8px var(--gut) 20px}
@media(min-width:768px){.wm{padding:12px var(--gut) 32px}}
.wm h1{font-weight:600;text-transform:uppercase;letter-spacing:-.065em;line-height:.78;white-space:nowrap;font-size:26vw;display:inline-block}
.wm h1 span{display:inline-block;transform:translateY(110%);transition:transform 1.3s var(--ease)}
.wm h1 span:nth-child(2){transition-delay:.05s}.wm h1 span:nth-child(3){transition-delay:.1s}.wm h1 span:nth-child(4){transition-delay:.15s}.wm h1 span:nth-child(5){transition-delay:.2s}
.wm .clip{overflow:hidden;padding-top:.04em}
body.ready .wm h1 span{transform:none}
.hero-arts{display:flex;align-items:flex-start;gap:10px;padding:0 var(--gut)}
@media(min-width:768px){.hero-arts{gap:20px}}
.ha{position:relative;flex:1;min-width:0}
.ha .in-w{position:absolute;inset:0;border-radius:12px;overflow:hidden;opacity:0;transform:translateY(48px);transition:opacity 1.2s var(--ease),transform 1.4s var(--ease);box-shadow:0 0 0 1px rgba(255,255,255,.05)}
body.ready .ha .in-w{opacity:1;transform:none}
.ha:nth-child(2) .in-w{transition-delay:.12s}.ha:nth-child(3) .in-w{transition-delay:.24s}
.tag{position:absolute;left:12px;bottom:12px;z-index:30;font-size:11px;letter-spacing:.14em;text-transform:uppercase;color:rgba(255,255,255,.85);background:rgba(10,10,14,.3);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);padding:6px 11px;border-radius:99px;border:1px solid rgba(255,255,255,.14);display:none;align-items:center;gap:8px}
.tag i{width:6px;height:6px;border-radius:50%;background:#9effc6;box-shadow:0 0 8px #9effc6}
@media(min-width:768px){.tag{display:inline-flex}}
.hero-copy{display:grid;gap:56px;padding:80px var(--gut) 112px}
@media(min-width:768px){.hero-copy{grid-template-columns:1fr 1fr;gap:40px;padding:128px var(--gut) 176px}}
.hc-l{display:flex;align-items:flex-start;gap:20px}
@media(min-width:768px){.hc-l{gap:40px}}
.bob{margin-top:8px;flex:none;width:40px;height:40px;border-radius:50%;display:grid;place-items:center;border:1px solid var(--line);transition:color .3s,border-color .3s;animation:bob 2.6s ease-in-out infinite}
.bob:hover{color:var(--gold);border-color:var(--gold)}
@keyframes bob{50%{transform:translateY(6px)}}
.hc-l h2{max-width:15ch;font-size:clamp(2.25rem,3.9vw,3.75rem);font-weight:300;line-height:1.02;letter-spacing:-.045em}
.hc-r{max-width:29rem}
@media(min-width:768px){.hc-r{padding-left:6%}}
@media(min-width:1024px){.hc-r{padding-left:12%}}
.pill{display:inline-flex;align-items:center;gap:10px;border-radius:99px;border:1px solid var(--line);background:rgba(255,255,255,.03);padding:6px 14px;font-size:13px;color:rgba(242,238,231,.9)}
.pulse{position:relative;width:7px;height:7px;border-radius:50%;background:#9effc6}
.pulse::after{content:"";position:absolute;inset:0;border-radius:50%;background:#9effc6;animation:pulse 2s ease-out infinite}
@keyframes pulse{to{transform:scale(3.2);opacity:0}}
.hc-r p.t{margin-top:32px;line-height:1.7;color:var(--muted)}
.hc-r p.t+p.t{margin-top:20px}
.btns{margin-top:40px;display:flex;flex-wrap:wrap;gap:12px;align-items:center}
.btn{display:inline-flex;align-items:center;gap:10px;height:48px;padding:0 22px;border-radius:99px;font-size:14px;font-weight:500;transition:transform .5s var(--ease),box-shadow .5s,background .3s,color .3s}
.btn.pri{background:var(--fg);color:var(--ink);box-shadow:0 0 0 rgba(239,220,182,0)}
.btn.pri:hover{transform:translateY(-2px);box-shadow:0 10px 40px -8px rgba(239,220,182,.55)}
.btn.ghost{border:1px solid var(--line);color:var(--fg)}
.btn.ghost:hover{border-color:var(--gold);color:var(--gold)}
.lnk{margin-top:40px;display:inline-flex;align-items:center;gap:12px;font-size:14px;font-weight:500}
.lnk svg{color:var(--gold);transition:transform .5s var(--ease)}
.lnk:hover svg{transform:translateX(4px)}
.lnk .u{position:relative}
.lnk .u::before,.lnk .u::after{content:"";position:absolute;left:0;bottom:-4px;height:1px;width:100%;background:rgba(255,255,255,.2)}
.lnk .u::after{background:var(--gold);transform:scaleX(0);transform-origin:left;transition:transform .5s var(--ease)}
.lnk:hover .u::after{transform:scaleX(1)}

/* method band (shader) */
.band{position:relative;min-height:100svh;display:flex;align-items:center;justify-content:center;overflow:hidden;padding:112px 0}
.band .bg{position:absolute;inset:-8% 0;will-change:transform}
.band canvas{position:absolute;inset:0;width:100%;height:100%;display:block}
.band .sh{position:absolute;inset:0;pointer-events:none}
.band .sh.b{background:radial-gradient(ellipse 55% 60% at center,rgba(0,0,0,.4),transparent 75%)}
.band .sh.c{background:linear-gradient(var(--bg),transparent 160px,transparent calc(100% - 160px),var(--bg))}
.band .sh.g{background-image:var(--noise);opacity:.12;mix-blend-mode:overlay}
.band .txt{position:relative;z-index:2;max-width:40rem;padding:0 24px;text-align:center;display:flex;flex-direction:column;align-items:center}
.band .txt p{font-size:clamp(1.2rem,1.8vw,1.6rem);font-weight:300;line-height:1.45;letter-spacing:-.015em}
.band .txt p+p{margin-top:24px}
.band .txt a{margin-top:48px;font-size:14px;font-weight:500;text-decoration:underline;text-decoration-color:rgba(255,255,255,.5);text-underline-offset:7px;transition:color .3s,text-decoration-color .3s}
.band .txt a:hover{color:var(--gold);text-decoration-color:var(--gold)}
.stats{margin-top:56px;display:flex;gap:clamp(24px,5vw,64px);justify-content:center;flex-wrap:wrap}
.stats div{text-align:center}
.stats b{display:block;font-size:clamp(1.8rem,3vw,2.6rem);font-weight:300;letter-spacing:-.04em}
.stats span{font-size:12px;letter-spacing:.14em;text-transform:uppercase;color:rgba(242,238,231,.6)}

/* practices */
.sec{padding-top:112px;padding-bottom:112px}
@media(min-width:768px){.sec{padding-top:160px;padding-bottom:160px}}
.sec h2.type-display{margin-top:24px}
.work-grid{margin-top:56px;display:grid;gap:20px}
@media(min-width:768px){.work-grid{margin-top:80px;grid-template-columns:1fr 1fr}.work-grid li.wide{grid-column:span 2;width:calc(50% - 10px);margin:0 auto}}
.card{display:block;border-radius:12px;background:var(--card);padding:10px;transition:background .5s;text-align:left;width:100%}
.card:hover{background:var(--card-h)}
.card .media{position:relative;display:block;overflow:hidden;border-radius:8px;background:var(--surface)}
.card .media .art{transition:transform .9s var(--ease)}
.card:hover .media .art{transform:scale(1.035)}
.card .play{position:absolute;right:14px;bottom:14px;z-index:30;width:44px;height:44px;border-radius:50%;display:grid;place-items:center;background:rgba(255,255,255,.12);backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);border:1px solid rgba(255,255,255,.2);transform:scale(.85);opacity:0;transition:transform .5s var(--ease),opacity .4s}
.card:hover .play{transform:none;opacity:1}
.card .meta{display:block;padding:20px 10px 12px}
@media(min-width:768px){.card .meta{padding:20px 12px 16px}}
.card .row{display:flex;justify-content:space-between;gap:16px;font-size:12px;color:var(--muted)}
.card .row b{color:var(--gold);font-weight:400;margin-right:6px}
.card .ttl{display:block;margin-top:10px;font-size:clamp(1.25rem,1.8vw,1.65rem);font-weight:300;line-height:1.3;letter-spacing:-.025em}
.card .ds{display:block;margin-top:6px;font-size:14px;color:var(--muted);line-height:1.6;max-width:36rem}

/* how it works */
#how .head{display:flex;flex-direction:column;align-items:center;text-align:center}
.svc{margin-top:64px}
@media(min-width:768px){.svc{margin-top:96px}}
.svc li{position:sticky;padding-bottom:20px}
@media(min-width:768px){.svc li{padding-bottom:24px}}
.svc article{position:relative;height:min(78svh,760px);min-height:500px;display:flex;flex-direction:column;align-items:center;justify-content:space-between;overflow:hidden;border-radius:16px;border:1px solid var(--line);background:#111014;padding:32px 24px;box-shadow:0 -30px 70px -30px rgba(0,0,0,.9)}
@media(min-width:768px){.svc article{padding:40px 24px}}
.svc article::before{content:"";position:absolute;inset:0;background:radial-gradient(ellipse 60% 50% at 50% 45%,var(--tint,rgba(214,185,138,.08)),transparent 70%);pointer-events:none}
.svc .num{font-size:14px;color:var(--muted);font-variant-numeric:tabular-nums}
.svc .num b{color:var(--gold);font-weight:400;margin-right:6px}
.svc .tiles{position:relative;flex:1;display:flex;align-items:center;justify-content:center;padding:24px 0}
.svc .tile{position:relative;width:clamp(120px,16vw,230px);aspect-ratio:3/4;border-radius:12px;overflow:hidden;box-shadow:0 30px 60px -15px rgba(0,0,0,.85),0 0 0 1px rgba(255,255,255,.06);opacity:0;transition:opacity 1s var(--ease),transform 1.2s var(--ease)}
.svc .tile:first-child{transform:translateY(40px) rotate(-4deg);margin-right:-14px}
.svc .tile:last-child{transform:translateY(40px) rotate(4deg);margin-left:-14px;transition-delay:.12s}
.svc .tiles.in .tile{opacity:1}
.svc .tiles.in .tile:first-child{transform:rotate(-4deg)}
.svc .tiles.in .tile:last-child{transform:translateY(16px) rotate(4deg)}
.svc article:hover .tile:first-child{transform:rotate(-7deg) translateX(-10px)}
.svc article:hover .tile:last-child{transform:translateY(16px) rotate(7deg) translateX(10px)}
.svc h3{font-size:clamp(2rem,4.4vw,4rem);font-weight:300;line-height:1;letter-spacing:-.045em;text-align:center}
.svc p{margin:16px auto 0;max-width:30rem;color:var(--muted);text-align:center}

/* explore */
.explore{position:relative;overflow:hidden;padding:24px 0}
.mq{display:flex;flex-direction:column;gap:10px}
.mq .track{display:flex;width:max-content;animation:marq var(--dur,60s) linear infinite}
.mq .track.rev{animation-direction:reverse}
@keyframes marq{to{transform:translateX(-50%)}}
.mq .t{position:relative;flex:none;width:170px;aspect-ratio:15/14;margin-right:10px;border-radius:8px;overflow:hidden}
@media(min-width:768px){.mq .t{width:300px}}
.explore .ov1{position:absolute;inset:0;pointer-events:none;background:rgba(0,0,0,.4) radial-gradient(ellipse 70% 80% at 60% 50%,transparent,rgba(0,0,0,.75))}
.explore .ov2{position:absolute;inset:0 auto 0 0;width:62vw;pointer-events:none;background:linear-gradient(90deg,rgba(9,9,11,.96),rgba(9,9,11,.65),transparent)}
.explore .cta{position:absolute;inset:0;display:flex;flex-direction:column;align-items:flex-start;justify-content:center;padding:0 var(--gut)}
.explore h2{max-width:10ch}

/* stories */
.tst{position:relative;overflow:hidden;padding:128px var(--gut)}
@media(min-width:768px){.tst{padding:192px var(--gut)}}
.tst .bg{position:absolute;inset:0;opacity:.9}
.tst .fade{position:absolute;inset:0;background:linear-gradient(var(--bg),transparent 190px,transparent calc(100% - 190px),var(--bg));pointer-events:none}
.tst .box{position:relative;max-width:56rem;margin:0 auto;border-radius:20px;border:1px solid var(--line);background:linear-gradient(160deg,rgba(255,255,255,.06),rgba(0,0,0,.3));backdrop-filter:blur(24px);-webkit-backdrop-filter:blur(24px);padding:48px 24px;text-align:center;box-shadow:0 40px 120px -40px rgba(0,0,0,.9),inset 0 1px 0 rgba(255,255,255,.08)}
@media(min-width:768px){.tst .box{padding:80px 64px}}
.tst .quote-mark{font-family:'Instrument Serif',serif;font-size:72px;line-height:.5;display:block;height:28px}
.slides{position:relative;min-height:17rem;perspective:1400px;touch-action:pan-y;user-select:none;-webkit-user-select:none}
.slide{position:absolute;inset:0;display:flex;flex-direction:column;align-items:center;opacity:0;filter:blur(10px);transform:translateY(20px) rotateX(-10deg);transition:opacity .8s var(--ease),filter .8s var(--ease),transform .9s var(--ease);pointer-events:none}
.slide.on{opacity:1;filter:none;transform:none;pointer-events:auto;position:relative}
.slide blockquote{max-width:28ch;font-size:clamp(1.5rem,2.8vw,2.6rem);font-weight:300;line-height:1.2;letter-spacing:-.03em}
.slide figcaption{margin-top:40px;font-size:14px}
.slide figcaption span{display:block;color:var(--muted);margin-top:4px}
.tctl{margin-top:40px;display:flex;align-items:center;justify-content:center;gap:16px}
.tctl button{width:48px;height:48px;border-radius:50%;border:1px solid rgba(255,255,255,.15);display:grid;place-items:center;transition:background .3s,border-color .3s,color .3s}
.tctl button:hover{background:var(--gold-2);border-color:var(--gold-2);color:var(--ink)}
.tctl p{width:64px;text-align:center;font-size:14px;color:var(--muted);font-variant-numeric:tabular-nums}
.tctl p span{color:var(--fg)}
.tprog{margin:24px auto 0;width:120px;height:1px;background:var(--line);overflow:hidden}
.tprog i{display:block;height:100%;background:var(--aur);transform-origin:left;transform:scaleX(0)}

/* journal */
.jgrid{margin-top:56px;display:grid;gap:20px}
@media(min-width:768px){.jgrid{margin-top:80px;grid-template-columns:1fr 1fr}.jgrid .feat{grid-column:span 2}}
.jc{display:block;height:100%;width:100%;text-align:left;border-radius:12px;background:var(--card);padding:10px;transition:background .5s}
.jc:hover{background:var(--card-h)}
.jc .media{position:relative;display:block;aspect-ratio:4/5;border-radius:8px;overflow:hidden}
.jc .media .art{transition:transform 1.4s var(--ease)}
.jc:hover .media .art{transform:scale(1.05)}
@media(min-width:768px){.jc.f{display:grid;grid-template-columns:repeat(12,1fr);gap:24px}.jc.f .media{grid-column:span 5}.jc.f .body{grid-column:span 7;justify-content:flex-end;padding:16px 16px 24px}.jc:not(.f) .media{aspect-ratio:5/6}}
.jc .body{display:flex;flex-direction:column;padding:20px 10px 12px}
.jc .row{display:flex;justify-content:space-between;gap:16px;font-size:12px;color:var(--muted)}
.jc .row b{color:var(--gold);font-weight:400;margin-right:6px}
.jc .h{display:block;margin-top:12px;font-weight:300;letter-spacing:-.03em;font-size:clamp(1.35rem,2vw,1.85rem);line-height:1.1}
.jc.f .h{font-size:clamp(1.6rem,3.4vw,3.25rem);line-height:1.02}
.jc .ex{display:none;margin-top:20px;max-width:28rem;line-height:1.7;color:var(--muted)}
@media(min-width:768px){.jc .ex{display:block}}
.jc .rd2{margin-top:24px;display:inline-flex;align-items:center;gap:8px;font-size:14px}
.jc .rd2 span{text-decoration:underline;text-decoration-color:rgba(255,255,255,.25);text-underline-offset:6px;transition:color .3s,text-decoration-color .3s}
.jc:hover .rd2 span{color:var(--gold);text-decoration-color:var(--gold)}
.jc .rd2 svg{transition:transform .5s var(--ease),color .3s}
.jc:hover .rd2 svg{transform:translateX(4px);color:var(--gold)}
dialog.note{margin:auto;max-width:min(640px,calc(100% - 32px));width:100%;background:#111014;color:var(--fg);border:1px solid var(--line);border-radius:18px;padding:0;overflow:hidden}
dialog.note::backdrop{background:rgba(0,0,0,.7);backdrop-filter:blur(6px)}
dialog.note[open]{animation:dlg .6s var(--ease)}
@keyframes dlg{from{opacity:0;transform:translateY(24px) scale(.98)}}
dialog .dm{position:relative;height:220px}
dialog .db{padding:28px 28px 32px}
dialog .db h3{font-size:clamp(1.8rem,4vw,2.6rem);font-weight:300;letter-spacing:-.035em;line-height:1.05;margin:10px 0 18px}
dialog .db p{color:#bdb8c0;line-height:1.75}
dialog .db p+p{margin-top:14px}
dialog .x{position:absolute;top:14px;right:14px;z-index:40;width:40px;height:40px;border-radius:50%;background:rgba(0,0,0,.45);backdrop-filter:blur(8px);display:grid;place-items:center;border:1px solid rgba(255,255,255,.15)}
dialog .x:hover{background:var(--gold-2);color:var(--ink)}

/* footer */
footer{position:relative;overflow:hidden;border-top:1px solid var(--line);padding-top:96px}
@media(min-width:768px){footer{padding-top:128px}}
.getit{display:grid;gap:40px;padding-bottom:96px}
@media(min-width:900px){.getit{grid-template-columns:1.2fr 1fr;align-items:end}}
.getit h2{max-width:11ch}
.getit .side p{color:var(--muted);max-width:30rem;line-height:1.7}
.getit .mail{display:inline-block;margin-top:24px;font-size:15px;color:var(--fg);text-decoration:underline;text-decoration-color:rgba(255,255,255,.25);text-underline-offset:6px}
.getit .mail:hover{color:var(--gold)}
.ftop{display:flex;flex-direction:column;gap:48px;border-top:1px solid var(--line);padding-top:64px}
@media(min-width:768px){.ftop{flex-direction:row;align-items:flex-end;justify-content:space-between}}
.ftop ul{display:flex;flex-wrap:wrap;gap:12px 32px;font-size:15px}
.ftop a,.fbot a{color:rgba(242,238,231,.85);transition:color .3s}
.ftop a:hover,.fbot a:hover{color:var(--gold)}
.fbot{margin-top:64px;display:flex;flex-direction:column;gap:16px;border-top:1px solid var(--line);padding:24px 0;font-size:14px;color:var(--muted)}
@media(min-width:768px){.fbot{margin-top:96px;flex-direction:row;align-items:center;justify-content:space-between}}
.fbot ul{display:flex;gap:24px;flex-wrap:wrap}
.fwm{position:relative;margin-top:-4vw;pointer-events:none;user-select:none}
.fwm p{text-align:center;font-size:29vw;font-weight:300;line-height:.78;letter-spacing:-.075em;transform:translateY(46%)}
.fwm span{display:inline-block;color:transparent;background:linear-gradient(180deg,rgba(9,9,11,0) 35%,rgba(9,9,11,.75)),linear-gradient(115deg,#1a1430,#7a5cff 22%,#efdcb6 42%,#ff9a6b 58%,#5ad2ff 76%,#1a1430);background-size:100% 100%,300% 100%;-webkit-background-clip:text;background-clip:text;animation:shimmer 14s ease-in-out infinite alternate}
@keyframes shimmer{to{background-position:0 0,100% 0}}

@media (prefers-reduced-motion:reduce){
  *,*::before,*::after{animation-duration:.001s!important;animation-iteration-count:1!important;transition-duration:.001s!important}
  .mq .track{animation:none}
  html{scroll-behavior:auto}
}
</style>
</head>
<body>
<a class="skip" href="#main">Skip to content</a>

<div class="intro" id="intro" data-section="intro" role="status" aria-label="Loading Auren">
  <div class="pn t"></div><div class="pn b"></div>
  <div class="meta" aria-hidden="true"><span>Auren · AI Meditation</span><span>Take a breath</span></div>
  <div class="mid" aria-hidden="true">
    <div class="grid">
      <div class="names"><ul id="introNames"></ul></div>
      <div class="thumb"><div data-art="orb"></div></div>
      <div class="cnt"><span class="count" id="introCount">000</span><span class="bar"><i id="introBar"></i></span></div>
    </div>
  </div>
  <button class="skipb" id="introSkip" type="button">Skip</button>
</div>

<div class="grain" aria-hidden="true"></div>

<header class="site" id="hdr" data-section="nav">
  <div class="row">
    <a class="logo" href="#hero" aria-label="Auren, back to top">Auren</a>
    <nav aria-label="Main"><ul>
      <li><a href="#hero" class="cur" data-nav="hero">Home</a></li>
      <li><a href="#method" data-nav="method">Method</a></li>
      <li><a href="#practices" data-nav="practices">Practices</a></li>
      <li><a href="#download" data-nav="download">Get Auren</a></li>
    </ul></nav>
    <button class="burger" id="burger" type="button" aria-expanded="false" aria-controls="mmenu"><span class="sr-only">Open menu</span><i></i><i></i></button>
  </div>
</header>
<div class="mmenu" id="mmenu" aria-hidden="true">
  <a href="#hero"><span>01</span>Home</a>
  <a href="#method"><span>02</span>Method</a>
  <a href="#practices"><span>03</span>Practices</a>
  <a href="#download"><span>04</span>Get Auren</a>
  <p>Ten quiet minutes, composed for you.</p>
</div>

<main id="main" tabindex="-1">
  <section id="hero" class="hero" data-section="hero" aria-labelledby="hero-title">
    <div class="wm"><div class="clip"><h1 id="wordmark" aria-label="Auren, AI meditation"><span>A</span><span>U</span><span>R</span><span>E</span><span>N</span></h1></div></div>
    <div class="hero-arts">
      <div class="ha" style="aspect-ratio:11/12"><div class="in-w"><div data-art="mist" role="img" aria-label="Layered mountain ridges in morning mist at sunrise"></div><span class="tag">Dawn · 06:12</span></div></div>
      <div class="ha" style="aspect-ratio:2/3"><div class="in-w"><div data-art="app" role="img" aria-label="The Auren app mid-session, a glowing orb guiding the breath"></div><span class="tag"><i></i>Live session</span></div></div>
      <div class="ha" style="aspect-ratio:11/12"><div class="in-w"><div data-art="orb" role="img" aria-label="An iridescent glass orb breathing softly on a dark surface"></div><span class="tag">Listening</span></div></div>
    </div>
    <div class="hero-copy">
      <div class="hc-l">
        <button class="bob" type="button" id="scrollNext" aria-label="Scroll to the next section"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M12 5v14"/><path d="m19 12-7 7-7-7"/></svg></button>
        <h2 id="hero-title" data-split>Meditation that listens, then <span class="serif grad">guides you home.</span></h2>
      </div>
      <div class="hc-r">
        <div data-reveal><p class="pill"><span class="pulse" aria-hidden="true"></span>Early access is open</p></div>
        <div data-reveal><p class="t">Auren is an AI meditation guide. It hears how you arrive, through your voice, your breath and the hour you open it, then composes a session around the person you are today.</p></div>
        <div data-reveal><p class="t">No streaks to protect. No recordings played to everyone at once. Just a calmer you, a little more each day.</p></div>
        <div data-reveal class="btns"><a class="btn pri" href="#download">Begin your first session</a><a class="btn ghost" href="#method">How it works</a></div>
      </div>
    </div>
  </section>

  <section id="method" class="band" data-section="method" aria-label="The Auren method">
    <div class="bg" id="bandBg" aria-hidden="true"><div data-art="aura" id="bandFallback"></div><canvas id="shader"></canvas></div>
    <div class="sh b"></div><div class="sh g"></div><div class="sh c"></div>
    <div class="txt" data-reveal="left">
      <p>Most meditation apps press play on the same recording for everyone. Auren begins by listening, then shapes the pace, the voice, the length and the sound around how you actually feel.</p>
      <p>Close your eyes. <span class="serif grad" style="font-size:1.15em">Auren will do the rest.</span></p>
      <div class="stats">
        <div><b>60s</b><span>Check-in</span></div>
        <div><b>∞</b><span>Unique sessions</span></div>
        <div><b>0</b><span>Ads, ever</span></div>
      </div>
      <a href="#how">See how it works</a>
    </div>
  </section>

  <section id="practices" class="sec px" data-section="practices" aria-labelledby="practices-title">
    <p class="eyebrow"><b aria-hidden="true">/</b>Practices</p>
    <h2 class="type-display" id="practices-title" data-split style="max-width:13ch">Sessions shaped around you</h2>
    <ul class="work-grid" id="workGrid"></ul>
  </section>

  <section id="how" class="px" data-section="how-it-works" style="padding-top:clamp(112px,12vw,160px);padding-bottom:clamp(64px,7vw,96px)" aria-labelledby="how-title">
    <div class="head">
      <p class="eyebrow"><b aria-hidden="true">/</b>How it works</p>
      <h2 class="type-display" id="how-title" data-split style="margin-top:24px">A guide that <span class="serif grad">pays attention</span></h2>
    </div>
    <ol class="svc" id="svc"></ol>
  </section>

  <section class="explore" data-section="explore" aria-labelledby="explore-title">
    <div class="mq" id="mq" aria-hidden="true"></div>
    <div class="ov1"></div><div class="ov2"></div>
    <div class="cta">
      <h2 id="explore-title" class="type-xl" data-split>A library that writes itself</h2>
      <a class="lnk" href="#practices"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg><span class="u">Explore practices</span></a>
    </div>
  </section>

  <section class="tst" data-section="stories" aria-labelledby="t-title">
    <div class="bg" aria-hidden="true"><div data-art="aura"></div></div>
    <div class="fade"></div>
    <h2 id="t-title" class="sr-only">What members say</h2>
    <div class="box" data-reveal>
      <div role="region" aria-roledescription="carousel" aria-label="Member stories" tabindex="0" id="carousel">
        <span class="quote-mark grad" aria-hidden="true">“</span>
        <div class="slides" id="slides"></div>
        <div class="tctl">
          <button type="button" id="tPrev" aria-label="Previous story"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="m12 19-7-7 7-7"/><path d="M19 12H5"/></svg></button>
          <p aria-hidden="true"><span id="tIdx">01</span> / <span style="color:inherit" id="tTot">03</span></p>
          <button type="button" id="tNext" aria-label="Next story"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg></button>
        </div>
        <div class="tprog" aria-hidden="true"><i id="tProg"></i></div>
      </div>
      <p class="sr-only" aria-live="polite" id="tLive"></p>
    </div>
  </section>

  <section id="journal" class="sec px" data-section="journal" aria-labelledby="journal-title">
    <p class="eyebrow"><b aria-hidden="true">/</b>Field notes</p>
    <h2 class="type-display" id="journal-title" data-split style="margin-top:24px;max-width:13ch">On stillness, science and care</h2>
    <div class="jgrid" id="jgrid"></div>
  </section>
</main>

<dialog class="note" id="note">
  <button class="x" type="button" id="noteX" aria-label="Close note"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" aria-hidden="true"><path d="M18 6 6 18M6 6l12 12"/></svg></button>
  <div class="dm" id="noteMedia"></div>
  <div class="db"><p class="eyebrow" id="noteMeta"></p><h3 id="noteTitle"></h3><div id="noteBody"></div></div>
</dialog>

<footer id="download" data-section="footer">
  <div class="px">
    <div class="getit">
      <div>
        <p class="eyebrow"><b aria-hidden="true">/</b>Get Auren</p>
        <h2 class="type-xl" style="margin-top:24px">Begin <span class="serif grad">tonight.</span></h2>
      </div>
      <div class="side">
        <p>Your first fourteen days are on us. Download Auren, speak for a minute, and let your first session find you.</p>
        <div class="btns">
          <a class="btn pri" href="#"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="6" y="2" width="12" height="20" rx="3"/><path d="M11 18h2"/></svg>Download for iOS</a>
          <a class="btn ghost" href="#"><svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="6" y="2" width="12" height="20" rx="3"/><path d="M11 18h2"/></svg>Download for Android</a>
        </div>
        <a class="mail" href="mailto:hello@auren.app">hello@auren.app</a>
      </div>
    </div>
    <div class="ftop">
      <p class="type-title" style="max-width:18ch">Breathe slowly. <span class="serif grad">Return often.</span></p>
      <nav aria-label="Footer"><ul>
        <li><a href="#hero">Home</a></li><li><a href="#method">Method</a></li><li><a href="#practices">Practices</a></li><li><a href="#journal">Field notes</a></li><li><a href="#download">Get Auren</a></li>
      </ul></nav>
    </div>
    <div class="fbot">
      <p>© <span id="yr">2026</span> Auren. Not a substitute for professional care.</p>
      <ul>
        <li><a href="#">Privacy</a></li>
        <li><a href="#">Terms</a></li>
        <li><a href="https://www.instagram.com/auren.studio" target="_blank" rel="noopener noreferrer">Instagram</a></li>
      </ul>
    </div>
  </div>
  <div class="fwm" aria-hidden="true"><p><span>Auren</span></p></div>
</footer>

<script>
(() => {
const $ = (s, c=document) => c.querySelector(s);
const $$ = (s, c=document) => [...c.querySelectorAll(s)];
const reduce = matchMedia('(prefers-reduced-motion: reduce)').matches;
function rng(a){return function(){a|=0;a=a+0x6D2B79F5|0;let t=Math.imul(a^a>>>15,1|a);t=t+Math.imul(t^t>>>7,61|t)^t;return((t^t>>>14)>>>0)/4294967296}}
const f = n => (+n).toFixed(2);

/* ---------- generative helpers ---------- */
function stars(r,n,top=0,bot=60,max=.32){
  let s='';
  for(let i=0;i<n;i++){const z=.12+Math.pow(r(),3)*max;s+=`<i class="st${r()<.3?' tw':''}" style="left:${f(r()*100)}%;top:${f(top+r()*(bot-top))}%;width:${f(z)}cqmin;height:${f(z)}cqmin;opacity:${f(.3+r()*.7)};animation-delay:-${f(r()*4)}s"></i>`}
  return s;
}
function ridge(r,y0,amp,f1){
  const p1=r()*6,p2=r()*6,p3=r()*6;let d=`M0 60 L0 ${f(y0)}`;
  for(let x=0;x<=100;x+=1){const y=y0-amp*(.62*Math.abs(Math.sin(x*f1+p1))+.28*Math.sin(x*f1*2.7+p2)+.1*Math.sin(x*f1*7.3+p3));d+=` L${x} ${f(y)}`}
  return d+' L100 60 Z';
}

/* ---------- art library ---------- */
const ICON={prev:'<svg viewBox="0 0 24 24" fill="currentColor"><path d="M6 5h2v14H6zM20 5v14L9 12z"/></svg>',pause:'<svg viewBox="0 0 24 24" fill="currentColor"><path d="M7 5h3.5v14H7zM13.5 5H17v14h-3.5z"/></svg>',next:'<svg viewBox="0 0 24 24" fill="currentColor"><path d="M16 5h2v14h-2zM4 5v14l11-7z"/></svg>'};
const ART = {
  orb:()=>`<i class="ob-glow"></i><i class="ob-floor"></i><i class="ob-caustic"></i><i class="ob-shadow"></i><div class="ob"><i class="c1"></i><i class="c2"></i><i class="c3"></i><i class="c4"></i><i class="c5"></i></div>`,
  mist:(r,n)=>{
    const L=[[30,9,.06,'#7a5672',.75],[36,10,.05,'#583f62',.85],[42,11,.045,'#382a4c',.9],[48,12,.04,'#211a33',1],[54,10,.035,'#0e0c18',1]];
    let p='',fog='';
    L.forEach((l,i)=>{p+=`<path d="${ridge(r,l[0],l[1],l[2])}" fill="url(#mg${n}_${i})" opacity="${l[4]}"/>`});
    const defs=L.map((l,i)=>`<linearGradient id="mg${n}_${i}" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="${l[3]}"/><stop offset="1" stop-color="#0a0812"/></linearGradient>`).join('');
    [38,26,14].forEach((b,i)=>fog+=`<i class="mi-fog" style="bottom:${b}%;animation-delay:-${i*5}s;opacity:${.9-i*.2}"></i>`);
    return `${stars(r,40,0,30,.25)}<i class="mi-sun"></i><svg class="mi-r" viewBox="0 0 100 60" preserveAspectRatio="none" aria-hidden="true"><defs>${defs}</defs>${p}</svg>${fog}`},
  app:(r,n,el)=>`<i class="ap-halo"></i><i class="ap-floor"></i><div class="ap-ph" style="--tilt:${el.dataset.tilt||0}deg"><div class="ap-scr"><i class="ap-isl"></i><div class="ap-top"><span>Session 3 of 7</span><span>Focus</span></div><div class="ap-h">Morning<br>Clarity</div><div class="ap-sub">Composed for you · slow exhale</div><div class="ap-br"><i class="ring" style="--s:96%;--d:-.6s"></i><i class="ring" style="--s:78%;--d:-.3s"></i><i class="ring" style="--s:62%"></i><div class="ap-core"><i></i><b></b></div></div><div class="ap-say"><span>Breathe in</span><span>Breathe out</span></div><div class="ap-prog"><i></i></div><div class="ap-time"><span>05:07</span><span>08:00</span></div><div class="ap-ctl"><span>${ICON.prev}</span><span class="p">${ICON.pause}</span><span>${ICON.next}</span></div></div></div>`,
  chat:r=>{let w='';for(let i=0;i<26;i++)w+=`<i style="--h:${f(25+r()*75)}%;--d:-${f(r()*1.6)}s"></i>`;
    return `<i class="ch-blob" style="left:-10%;top:-10%;background:#6b4cff"></i><i class="ch-blob" style="right:-15%;bottom:-15%;background:#ff8a5c;animation-delay:-7s"></i><div class="ch-card"><div class="ch-hd"><i></i>Auren<small>listening…</small></div><div class="ch-b ai">Good evening. How are you arriving today?</div><div class="ch-b me">Tired. My head feels loud.</div><div class="ch-b ai">Thank you for telling me. Let’s lengthen the exhale first. I’ve shaped tonight to nine gentle minutes.</div><div class="ch-wave">${w}</div></div>`},
  aurora:(r,n)=>`${stars(r,70,0,60,.3)}<i class="ar-c ar-c1"></i><i class="ar-c ar-c2"></i><i class="ar-c ar-c3"></i><i class="ar-str"></i><svg class="ar-hills" viewBox="0 0 100 60" preserveAspectRatio="none" aria-hidden="true"><path d="${ridge(r,40,22,.05)}" fill="#03050a"/></svg><i class="ar-lake"></i>`,
  moon:(r)=>`${stars(r,60,0,52,.28)}<i class="mn-halo"></i><i class="mn"></i><i class="mn-hz"></i><svg class="mn-hills" viewBox="0 0 100 60" preserveAspectRatio="none" aria-hidden="true"><path d="${ridge(r,58,16,.04)}" fill="#070b18"/></svg><i class="mn-ref"></i>`,
  dunes:(r,n)=>{let rip='';for(let i=0;i<34;i++){const y=60+i*1.25+r()*.4,a=-5+r()*2;rip+=`<path d="M-5 ${f(y)} C 25 ${f(y+a)}, 55 ${f(y-a*.6)}, 105 ${f(y+3)}" stroke="${i%2?'rgba(255,232,200,.35)':'rgba(90,40,30,.28)'}" stroke-width="${i%2?.18:.28}" fill="none"/>`}
    return `${stars(r,20,0,20,.2)}<i class="du-sun"></i><svg viewBox="0 0 100 100" preserveAspectRatio="xMidYMid slice" aria-hidden="true"><defs><linearGradient id="d1${n}" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#f5c695"/><stop offset=".5" stop-color="#d98a5c"/><stop offset="1" stop-color="#7a3a2a"/></linearGradient><linearGradient id="d2${n}" x1="1" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#e3a173"/><stop offset=".6" stop-color="#9a4e34"/><stop offset="1" stop-color="#4a2018"/></linearGradient><linearGradient id="d3${n}" x1="0" y1="0" x2="0" y2="1"><stop offset="0" stop-color="#8a4430"/><stop offset="1" stop-color="#2a1210"/></linearGradient></defs><path d="M0 58 C 30 46, 55 50, 100 62 L100 100 L0 100Z" fill="url(#d1${n})"/>${rip}<path d="M-5 74 C 22 62, 58 64, 105 76 L105 100 L-5 100Z" fill="url(#d2${n})"/><path d="M-5 74 C 22 62, 58 64, 105 76" stroke="rgba(255,225,190,.5)" stroke-width=".3" fill="none"/><path d="M-5 88 C 35 79, 70 82, 105 91 V100 H-5Z" fill="url(#d3${n})"/></svg>`},
  breath:r=>{let s='',o='';[22,34,46,58,70,84,98].forEach((v,i)=>s+=`<i class="br-ring" style="--s:min(${v}cqw,${v}cqh);--o:${f(.5-i*.06)};--d:-${f(i*.18)}s"></i>`);
    for(let i=0;i<28;i++){const a=r()*360,d=14+r()*30,z=.3+r()*.7;o+=`<span style="transform:rotate(${f(a)}deg) translateX(${f(d)}cqmin);width:${f(z)}cqmin;height:${f(z)}cqmin;opacity:${f(.3+r()*.7)}"></span>`}
    return `${s}<div class="br-orb">${o}</div><div class="br-core"><i></i><b></b></div><div class="br-t"><span>Inhale · 4</span><span>Exhale · 4</span></div>`},
  waves:(r,n)=>{let p='';for(let i=0;i<54;i++){let d='';for(let x=-10;x<=310;x+=5){const y=50+Math.sin(x*.025+i*.055)*22*Math.sin(x*.008+1)+Math.sin(x*.06+i*.03)*4+(i-27)*.35;d+=(x===-10?'M':' L')+x+' '+f(y)}p+=`<path d="${d}" stroke="url(#wg${n})" stroke-width=".22" fill="none" opacity="${f(.25+.6*Math.sin(i/54*Math.PI))}"/>`}
    return `<svg viewBox="0 0 300 100" preserveAspectRatio="none" aria-hidden="true"><defs><linearGradient id="wg${n}" x1="0" y1="0" x2="1" y2="0"><stop offset="0" stop-color="#5ad2ff"/><stop offset=".35" stop-color="#9a7bff"/><stop offset=".65" stop-color="#ff8fae"/><stop offset="1" stop-color="#ffd38a"/></linearGradient><filter id="wb${n}"><feGaussianBlur stdDeviation="1.2"/></filter></defs><g class="wv-g"><g filter="url(#wb${n})" opacity=".7">${p}</g>${p}</g></svg>`},
  stones:()=>{const S=[[24,22,52,17,'#7a7570','#3d3a37','#1e1c1b'],[31,36.5,38,13,'#8f8a83','#4b4743','#242221'],[36.5,47.5,27,10,'#a29b91','#5a554f','#2c2a28'],[41.5,55.8,17,7.4,'#b8b0a4','#6f685f','#383430']];
    let s='<i class="sn-sh" style="left:16%;width:68%;bottom:19%;height:9%"></i>';
    S.forEach((v,i)=>{if(i)s+=`<i class="sn-sh" style="left:${v[0]+3}%;width:${v[2]-6}%;bottom:${v[1]-1.2}%;height:3%;opacity:.8"></i>`;s+=`<i class="sn" style="left:${v[0]}%;bottom:${v[1]}%;width:${v[2]}%;height:${v[3]}%;background:radial-gradient(ellipse at 38% 22%,${v[4]},${v[5]} 55%,${v[6]})"></i>`});
    return `<i class="sn-ground"></i>${s}<i class="sn-light"></i>`},
  ripple:()=>`<i class="rp-sheen"></i><div class="rp">${[0,1,2,3,4,5].map(i=>`<i style="--d:-${f(i*1.16)}s"></i>`).join('')}</div><i class="rp-drop"></i>`,
  night:r=>`<i class="nt-mw"></i>${stars(r,120,0,85,.35)}<i class="nt-moon"></i><i class="nt-cl" style="left:-20%;bottom:-18%;width:80%;height:38%"></i><i class="nt-cl" style="right:-25%;bottom:-22%;width:90%;height:42%;background:#3a2448"></i>`,
  petal:()=>{let p='';for(let i=0;i<12;i++)p+=`<i style="--a:${i*30}deg;--w:min(40cqw,40cqh);--h:min(15cqw,15cqh);--c1:rgba(255,160,180,.28);--c2:rgba(170,140,255,.45)"></i>`;for(let i=0;i<8;i++)p+=`<i style="--a:${i*45+22}deg;--w:min(26cqw,26cqh);--h:min(11cqw,11cqh);--c1:rgba(255,200,150,.3);--c2:rgba(255,140,170,.5)"></i>`;return `<div class="pt">${p}</div><i class="pt-core"></i>`},
  ink:(r,n)=>`<svg viewBox="0 0 100 100" preserveAspectRatio="xMidYMid slice" aria-hidden="true"><defs><filter id="ik${n}" x="-50%" y="-50%" width="200%" height="200%"><feGaussianBlur stdDeviation="2.4" result="b"/><feTurbulence type="fractalNoise" baseFrequency=".035" numOctaves="3" seed="${Math.floor(r()*99)}" result="t"/><feDisplacementMap in="b" in2="t" scale="22" xChannelSelector="R" yChannelSelector="G"/></filter></defs><g class="ink-g" filter="url(#ik${n})"><circle cx="46" cy="44" r="20" fill="#2c2a6e" opacity=".75"/><circle cx="60" cy="56" r="15" fill="#7a3f8f" opacity=".6"/><circle cx="38" cy="60" r="10" fill="#c9783a" opacity=".55"/><circle cx="56" cy="36" r="7" fill="#1d4a6a" opacity=".6"/></g></svg>`,
  zen:(r,n)=>{let l='';for(let y=1;y<104;y+=2.4){const a=r()*.6;l+=`<path d="M-2 ${f(y)} C 30 ${f(y+a)}, 70 ${f(y-a)}, 102 ${f(y)}" stroke="rgba(110,92,70,.32)" stroke-width=".42" fill="none"/><path d="M-2 ${f(y+.5)} C 30 ${f(y+.5+a)}, 70 ${f(y+.5-a)}, 102 ${f(y+.5)}" stroke="rgba(255,252,244,.55)" stroke-width=".25" fill="none"/>`}
    const ring=(cx,cy,r0,n2)=>{let s=`<circle cx="${cx}" cy="${cy}" r="${r0+n2*2.4+1}" fill="#d8d0c2"/>`;for(let i=n2;i>=0;i--){const rr=r0+i*2.4;s+=`<circle cx="${cx}" cy="${cy}" r="${rr}" fill="none" stroke="rgba(110,92,70,.32)" stroke-width=".42"/><circle cx="${cx}" cy="${cy}" r="${rr+.5}" fill="none" stroke="rgba(255,252,244,.55)" stroke-width=".25"/>`}return s};
    const stone=(cx,cy,rx,ry,id)=>`<ellipse cx="${cx+1.5}" cy="${cy+2}" rx="${rx}" ry="${ry}" fill="rgba(40,30,20,.35)" filter="url(#zb${n})"/><ellipse cx="${cx}" cy="${cy}" rx="${rx}" ry="${ry}" fill="url(#zs${n})"/>`;
    return `<svg viewBox="0 0 100 100" preserveAspectRatio="xMidYMid slice" aria-hidden="true"><defs><radialGradient id="zs${n}" cx=".35" cy=".3"><stop offset="0" stop-color="#8d8780"/><stop offset=".6" stop-color="#46423e"/><stop offset="1" stop-color="#1f1d1b"/></radialGradient><filter id="zb${n}"><feGaussianBlur stdDeviation="1.2"/></filter></defs><rect width="100" height="100" fill="#d8d0c2"/>${l}${ring(62,40,9,6)}${ring(26,76,5,4)}${stone(62,40,7.5,6)}${stone(26,76,4,3.4)}</svg><i class="zn-light"></i>`},
  light:r=>{let d='';for(let i=0;i<22;i++){const z=.3+r()*.6;d+=`<span style="left:${f(30+r()*55)}%;top:${f(20+r()*70)}%;width:${f(z)}cqmin;height:${f(z)}cqmin;animation-duration:${f(7+r()*8)}s;animation-delay:-${f(r()*10)}s"></span>`}
    const leaves=Array.from({length:9},(_,i)=>`<ellipse cx="${60+Math.cos(i)*20}" cy="${10+i*9}" rx="9" ry="3.2" transform="rotate(${-30+i*14} ${60+Math.cos(i)*20} ${10+i*9})"/>`).join('');
    return `<div class="lt-win"><i></i><b style="left:48.5%;top:0;bottom:0;width:3%"></b><b style="top:48%;left:0;right:0;height:3%"></b></div><svg class="lt-leaf" viewBox="0 0 100 100" aria-hidden="true" fill="rgba(110,75,40,.45)"><path d="M70 0 C 62 30, 58 60, 52 100" stroke="rgba(110,75,40,.45)" stroke-width="1" fill="none"/>${leaves}</svg><i class="lt-vase2"></i><i class="lt-vase"></i><div class="lt-dust">${d}</div>`},
  aura:()=>`<i class="au au-1"></i><i class="au au-2"></i><i class="au au-3"></i>`
};
const LIGHT=new Set(['stones','ink','zen','light']);
let artN=0;
const artIO='IntersectionObserver' in window?new IntersectionObserver(es=>es.forEach(e=>e.target.classList.toggle('off',!e.isIntersecting)),{rootMargin:'100px'}):null;
function paint(root=document){
  $$('[data-art]:not(.art)',root).forEach(el=>{
    const k=el.dataset.art,n=++artN;
    el.classList.add('art','a-'+k);if(LIGHT.has(k))el.classList.add('light');
    el.innerHTML=ART[k](rng(n*9973+k.charCodeAt(0)*31),n,el);
    if(artIO&&!el.closest('#intro'))artIO.observe(el);
  });
}

/* ---------- content ---------- */
const PLAY='<svg width="14" height="14" viewBox="0 0 24 24" fill="#fff" aria-hidden="true"><path d="M7 4v16l13-8z"/></svg>';
const WORK=[
  {art:'light',cat:'Focus',dur:'8 min',t:'Morning Clarity',d:'A bright, unhurried start. Auren reads your energy and sets a pace that wakes the mind without rushing it.',alt:'Morning sunlight through a window onto a warm wall'},
  {art:'moon',cat:'Sleep',dur:'22 min',t:'Deep Sleep Descent',d:'A wind-down that slows as you do, then fades into silence the moment your breathing settles.',alt:'A full moon over still water with a shimmering reflection'},
  {art:'breath',cat:'Breathwork',dur:'4 min',t:'Breath Reset',d:'Four minutes of guided rhythm, paced live to your own inhale and exhale.',alt:'Concentric rings of light expanding around a glowing orb'},
  {art:'waves',cat:'Sound',dur:'Endless',t:'Adaptive Soundscapes',d:'Generative audio that never loops, tuned in real time to settle your nervous system.',alt:'Silk-like ribbons of light flowing in waves'},
  {art:'aurora',cat:'Body',dur:'15 min',t:'Northern Lights Body Scan',d:'A slow journey through the body, guided by a voice that softens wherever you hold tension.',alt:'Green and violet aurora over a dark lake',wide:true}
];
$('#workGrid').innerHTML=WORK.map(w=>`<li class="${w.wide?'wide':''}"><div data-reveal><a class="card" href="#download" aria-label="${w.t}, ${w.cat}, ${w.dur}"><span class="media" style="aspect-ratio:16/10"><span data-art="${w.art}" role="img" aria-label="${w.alt}"></span><span class="play">${PLAY}</span></span><span class="meta"><span class="row"><span><b aria-hidden="true">/</b>${w.cat}</span><span>${w.dur}</span></span><span class="ttl">${w.t}</span><span class="ds">${w.d}</span></span></a></div></li>`).join('');

const SVC=[
  ['It listens','A one-minute voice check-in reads tone, pace and breath to sense how you are arriving today.','chat','ripple','rgba(122,92,255,.12)'],
  ['It adapts','Every session is composed in the moment. Length, pacing, voice and sound all shift to meet your state.','petal','ink','rgba(255,140,170,.1)'],
  ['It breathes with you','Your phone’s sensors follow your rhythm, so the breath guide moves at your pace, not a metronome’s.','app','breath','rgba(214,185,138,.1)'],
  ['It sounds like calm','Generative soundscapes that never repeat, layered from rain, tone and space to quiet a busy mind.','waves','dunes','rgba(90,210,255,.08)'],
  ['It walks you to sleep','Wind-down journeys that dim as you drift and end in silence when your breathing settles.','night','moon','rgba(122,92,255,.1)'],
  ['It keeps your trust','Check-ins are processed privately and never sold. Your inner life is not a dataset.','stones','zen','rgba(214,185,138,.08)']
];
$('#svc').innerHTML=SVC.map((s,i)=>`<li style="top:calc(5.5rem + ${i} * 1.1rem)"><article style="--tint:${s[4]}" aria-labelledby="svc-${i}"><p class="num"><b aria-hidden="true">/</b>0${i+1}</p><div class="tiles" data-io><div class="tile"><div data-art="${s[2]}"${s[2]==='app'?' data-tilt="-6"':''}></div></div><div class="tile"><div data-art="${s[3]}"></div></div></div><div><h3 id="svc-${i}">${s[0]}</h3><p>${s[1]}</p></div></article></li>`).join('');

const ROWS=[['mist','light','moon','aurora','waves','orb'],['dunes','petal','ink','stones','zen','night','chat'],['ripple','breath','app','orb','aurora','mist','petal']];
$('#mq').innerHTML=ROWS.map((r,i)=>{const set=r.map(a=>`<div class="t"><div data-art="${a}"></div></div>`).join('');return `<div class="track${i===1?' rev':''}" style="--dur:${55+i*12}s">${set}${set}</div>`}).join('');

const QUOTES=[
  ['After night shifts my mind never switched off. Auren notices how wired I am and starts slower. I am usually asleep before it ends.','Maya R.','ICU nurse, member since spring'],
  ['I have tried every meditation app. This is the first one that feels like it is actually paying attention to me.','Jonah K.','Founder, daily practice'],
  ['The check-in sounds small, but being asked how I am, and having the answer change something, is the whole point.','Elif T.','Graduate student']
];
$('#slides').innerHTML=QUOTES.map((q,i)=>`<figure class="slide${i?'':' on'}" aria-roledescription="slide" aria-label="${i+1} of ${QUOTES.length}"><blockquote>${q[0]}</blockquote><figcaption>${q[1]}<span>${q[2]}</span></figcaption></figure>`).join('');

const NOTES=[
  {art:'zen',cat:'Science',date:'Feb 3, 2026',dt:'2026-02-03',t:'Why Breath Comes First',ex:'Before a thought can settle, the body needs a signal that it is safe. A long, slow exhale is that signal.',body:['Every Auren session starts with the breath, not with an instruction to clear your mind. Slowing the exhale is one of the simplest ways to tell the nervous system it can stand down.','That is why the first minute of each session is shaped by your own rhythm. We meet you at your pace, then lengthen it, gently, a few seconds at a time.']},
  {art:'ink',cat:'Sound',date:'Dec 11, 2025',dt:'2025-12-11',t:'Designing Silence',ex:'',body:['Silence is not the absence of design. It is the hardest thing to compose.','Our soundscapes are built to recede. They thin out as your breathing settles, until the quiet itself becomes the practice.']},
  {art:'stones',cat:'Principles',date:'Sep 24, 2025',dt:'2025-09-24',t:'What an AI Guide Should Never Do',ex:'',body:['A meditation guide should never chase your attention, sell your feelings, or pretend to be a therapist.','Auren is built to support a practice, not to replace care. When a check-in suggests you might need more than a session, it says so plainly and points you to people who can help.']}
];
const arrow='<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14"/><path d="m12 5 7 7-7 7"/></svg>';
$('#jgrid').innerHTML=NOTES.map((n,i)=>`<div class="${i?'':'feat'}" data-reveal><button type="button" class="jc${i?'':' f'}" data-note="${i}" aria-label="Read &quot;${n.t}&quot;, ${n.cat}, ${n.date}"><span class="media"><span data-art="${n.art}"></span></span><span class="body"><span class="row"><span><b aria-hidden="true">/</b>${n.cat}</span><time datetime="${n.dt}">${n.date}</time></span><span class="h">${n.t}</span>${n.ex?`<span class="ex">${n.ex}</span>`:''}<span class="rd2"><span>Read the note</span>${arrow}</span></span></button></div>`).join('');

const NAMES=['Arriving','Listening','Breathing','Settling','Softening'];
$('#introNames').innerHTML=[...NAMES,...NAMES].map(n=>`<li>${n}</li>`).join('')+'<li>Auren</li>';

paint();

/* ---------- shader band ---------- */
(function(){
  const cv=$('#shader');const gl=cv.getContext('webgl',{antialias:false,premultipliedAlpha:false});
  if(!gl){cv.remove();return}
  $('#bandFallback').style.display='none';
  const vs='attribute vec2 p;void main(){gl_Position=vec4(p,0.,1.);}';
  const fs=`precision highp float;uniform vec2 R;uniform float T;
  float h(vec2 p){return fract(sin(dot(p,vec2(127.1,311.7)))*43758.5453);}
  float n(vec2 p){vec2 i=floor(p),f=fract(p);f=f*f*(3.-2.*f);return mix(mix(h(i),h(i+vec2(1,0)),f.x),mix(h(i+vec2(0,1)),h(i+vec2(1,1)),f.x),f.y);}
  float fbm(vec2 p){float v=0.,a=.5;for(int i=0;i<6;i++){v+=a*n(p);p=p*2.03+vec2(1.7,9.2);a*=.5;}return v;}
  void main(){vec2 p=(gl_FragCoord.xy-.5*R)/R.y;float t=T*.035;
    vec2 q=vec2(fbm(p*1.4+vec2(t,0.)),fbm(p*1.4+vec2(5.2,1.3)-t));
    vec2 r=vec2(fbm(p*1.2+2.*q+vec2(1.7,9.2)+.6*t),fbm(p*1.2+2.*q+vec2(8.3,2.8)-.4*t));
    float f=fbm(p*1.1+2.2*r);
    vec3 c=vec3(.02,.018,.035);
    c=mix(c,vec3(.20,.13,.42),smoothstep(.25,.75,f));
    c=mix(c,vec3(.98,.64,.46),smoothstep(.55,.95,f)*.85*length(q));
    c=mix(c,vec3(.25,.65,.72),smoothstep(.5,.9,r.y)*.28);
    c+=vec3(.9,.75,.55)*pow(max(0.,f-.55),3.)*2.2;
    float v=smoothstep(1.25,.15,length(p*vec2(.85,1.)));
    c*=v;c=pow(c,vec3(.95));
    gl_FragColor=vec4(c,1.);}`;
  const sh=(t,s)=>{const o=gl.createShader(t);gl.shaderSource(o,s);gl.compileShader(o);return o};
  const pr=gl.createProgram();gl.attachShader(pr,sh(gl.VERTEX_SHADER,vs));gl.attachShader(pr,sh(gl.FRAGMENT_SHADER,fs));gl.linkProgram(pr);
  if(!gl.getProgramParameter(pr,gl.LINK_STATUS)){cv.remove();$('#bandFallback').style.display='';return}
  gl.useProgram(pr);
  const b=gl.createBuffer();gl.bindBuffer(gl.ARRAY_BUFFER,b);gl.bufferData(gl.ARRAY_BUFFER,new Float32Array([-1,-1,1,-1,-1,1,1,1]),gl.STATIC_DRAW);
  const lp=gl.getAttribLocation(pr,'p');gl.enableVertexAttribArray(lp);gl.vertexAttribPointer(lp,2,gl.FLOAT,false,0,0);
  const uR=gl.getUniformLocation(pr,'R'),uT=gl.getUniformLocation(pr,'T');
  const size=()=>{const s=Math.min(1,(devicePixelRatio||1))*.5;cv.width=Math.max(2,cv.clientWidth*s|0);cv.height=Math.max(2,cv.clientHeight*s|0);gl.viewport(0,0,cv.width,cv.height)};
  size();addEventListener('resize',size);
  let vis=false;new IntersectionObserver(e=>vis=e[0].isIntersecting).observe(cv);
  const t0=performance.now();let drawn=false;
  const loop=t=>{if((vis&&!reduce)||!drawn){gl.uniform2f(uR,cv.width,cv.height);gl.uniform1f(uT,(t-t0)/1000+20);gl.drawArrays(gl.TRIANGLE_STRIP,0,4);drawn=true}requestAnimationFrame(loop)};
  requestAnimationFrame(loop);
})();

/* ---------- split words ---------- */
$$('[data-split]').forEach(el=>{
  let i=0;
  const walk=node=>{
    [...node.childNodes].forEach(c=>{
      if(c.nodeType===3){
        const frag=document.createDocumentFragment();
        c.textContent.split(/(\s+)/).forEach(w=>{
          if(!w)return;
          if(/^\s+$/.test(w)){frag.append(document.createTextNode(' '));return}
          const m=document.createElement('span');m.className='rm';
          const s=document.createElement('span');s.className='rw';s.textContent=w;s.style.transitionDelay=(i++*0.06)+'s';
          m.append(s);frag.append(m);
        });
        c.replaceWith(frag);
      } else if(c.nodeType===1){
        const m=document.createElement('span');m.className='rm';
        c.classList.add('rw');c.style.transitionDelay=(i++*0.06)+'s';
        c.replaceWith(m);m.append(c);
      }
    });
  };
  walk(el);
});

/* ---------- reveal ---------- */
const io=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){e.target.classList.add('in');io.unobserve(e.target)}}),{threshold:.15,rootMargin:'0px 0px -6% 0px'});
$$('[data-reveal],[data-split],[data-io]').forEach(el=>io.observe(el));

/* ---------- wordmark fit ---------- */
const wm=$('#wordmark');
function fitWM(){wm.style.fontSize='100px';const w=wm.getBoundingClientRect().width,cw=wm.parentElement.clientWidth;wm.style.fontSize=(100*cw/w*.995)+'px'}
fitWM();addEventListener('resize',fitWM);
if(document.fonts)document.fonts.ready.then(fitWM);

/* ---------- intro ---------- */
const intro=$('#intro');let introDone=false;
function finishIntro(){if(introDone)return;introDone=true;intro.classList.add('out');document.body.classList.add('ready');setTimeout(()=>{intro.classList.add('gone');intro.setAttribute('aria-hidden','true')},1200)}
$('#introSkip').addEventListener('click',finishIntro);
if(reduce){finishIntro()}else{
  const cnt=$('#introCount'),bar=$('#introBar'),ul=$('#introNames'),lis=$$('li',ul);
  const D=2400,t0=performance.now();let last=-1;
  const tick=t=>{
    if(introDone)return;
    const p=Math.min(1,(t-t0)/D),e=1-Math.pow(1-p,3);
    cnt.textContent=String(Math.round(e*100)).padStart(3,'0');
    bar.style.transform=`scaleX(${e})`;
    const idx=Math.min(lis.length-1,Math.floor(e*(lis.length-1)));
    if(idx!==last){last=idx;ul.style.transform=`translateY(${-idx*1.15}em)`;lis.forEach((l,i)=>l.classList.toggle('cur',i===idx))}
    if(p<1)requestAnimationFrame(tick);else setTimeout(finishIntro,350);
  };
  requestAnimationFrame(tick);
}

/* ---------- header ---------- */
const hdr=$('#hdr');let lastY=scrollY;
function onScroll(){
  const y=scrollY,wb=wm.getBoundingClientRect().bottom;
  hdr.classList.toggle('logo-on',wb<40);
  if(!document.body.classList.contains('menu-open'))hdr.classList.toggle('hide',y>lastY&&y>600);
  lastY=y;
  const band=$('#bandBg');if(band&&!reduce){const r=band.parentElement.getBoundingClientRect();const p=(r.top+r.height/2-innerHeight/2)/innerHeight;band.style.transform=`translateY(${p*-9}%)`}
}
addEventListener('scroll',onScroll,{passive:true});onScroll();
const secIO=new IntersectionObserver(es=>es.forEach(e=>{if(e.isIntersecting){const id=e.target.id;$$('[data-nav]').forEach(a=>a.classList.toggle('cur',a.dataset.nav===id))}}),{rootMargin:'-45% 0px -50% 0px'});
['hero','method','practices','download'].forEach(id=>secIO.observe(document.getElementById(id)));

/* ---------- mobile menu ---------- */
const burger=$('#burger'),mm=$('#mmenu');
function setMenu(o){document.body.classList.toggle('menu-open',o);mm.classList.toggle('open',o);burger.setAttribute('aria-expanded',o);mm.setAttribute('aria-hidden',!o);$('.sr-only',burger).textContent=o?'Close menu':'Open menu';document.body.style.overflow=o?'hidden':''}
burger.addEventListener('click',()=>setMenu(!mm.classList.contains('open')));
$$('a',mm).forEach(a=>a.addEventListener('click',()=>setMenu(false)));
addEventListener('keydown',e=>{if(e.key==='Escape')setMenu(false)});
$('#scrollNext').addEventListener('click',()=>$('#method').scrollIntoView({behavior:reduce?'auto':'smooth'}));

/* ---------- stories carousel ---------- */
const slides=$$('.slide'),idxEl=$('#tIdx'),live=$('#tLive'),prog=$('#tProg');let ti=0,start,paused=false;
const AUTO=7000;
function show(n){ti=(n+slides.length)%slides.length;slides.forEach((s,i)=>s.classList.toggle('on',i===ti));idxEl.textContent=String(ti+1).padStart(2,'0');live.textContent=`Story ${ti+1} of ${slides.length}, from ${QUOTES[ti][1]}`;start=performance.now()}
function loopT(t){if(!reduce){const p=Math.min(1,(t-start)/AUTO);prog.style.transform=`scaleX(${p})`;if(p>=1&&!paused)show(ti+1)}requestAnimationFrame(loopT)}
const car=$('#carousel');
car.addEventListener('pointerenter',()=>paused=true);car.addEventListener('pointerleave',()=>{paused=false;start=performance.now()});
$('#tPrev').addEventListener('click',()=>show(ti-1));$('#tNext').addEventListener('click',()=>show(ti+1));
car.addEventListener('keydown',e=>{if(e.key==='ArrowLeft')show(ti-1);if(e.key==='ArrowRight')show(ti+1)});
let dx0=null;$('#slides').addEventListener('pointerdown',e=>{dx0=e.clientX});
addEventListener('pointerup',e=>{if(dx0===null)return;const d=e.clientX-dx0;dx0=null;if(Math.abs(d)>60)show(ti+(d<0?1:-1))});
start=performance.now();requestAnimationFrame(loopT);
$('#tTot').textContent=String(slides.length).padStart(2,'0');

/* ---------- field note dialog ---------- */
const dlg=$('#note');
$$('[data-note]').forEach(b=>b.addEventListener('click',()=>{
  const n=NOTES[+b.dataset.note];
  $('#noteMedia').innerHTML=`<div data-art="${n.art}"></div>`;paint($('#noteMedia'));
  $('#noteMeta').innerHTML=`<b aria-hidden="true">/</b>${n.cat} · ${n.date}`;
  $('#noteTitle').textContent=n.t;
  $('#noteBody').innerHTML=n.body.map(p=>`<p>${p}</p>`).join('');
  if(dlg.showModal)dlg.showModal();else dlg.setAttribute('open','');
}));
$('#noteX').addEventListener('click',()=>dlg.close());
dlg.addEventListener('click',e=>{if(e.target===dlg)dlg.close()});
$$('a[href="#"]').forEach(a=>a.addEventListener('click',e=>e.preventDefault()));
$('#yr').textContent=new Date().getFullYear();
})();
</script>
</body>
</html>
```

