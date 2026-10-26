INSTALANDING.AI · Recessed Aperture Hero Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Recessed Aperture Hero Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/recessed-aperture-hero-page

mnemo-context-window.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Recessed Aperture Hero Page
  slug     recessed-aperture-hero-page
  prompt   https://instalanding.ai/p/recessed-aperture-hero-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/recessed-aperture-hero-page
  license  MIT. Fictional brand; replace names, copy and numbers before shipping.
           Aperture and drifting pills adapted from a pen by Rafaela Lucas (credited in the footer).

  MAP
  tokens    :root custom properties at the top of the main <style>: --bg-1 #5531b8 (the flat surface), --bg-2/--bg-3,
            --coral, --cream, --g-warm / --g-cool gradients, --nm-lit / --nm-dim (soft-UI light and shade), --sans Barlow, --cond Barlow Condensed
  sections  nav, hero, features, stats, how-it-works, console, pricing, faq, footer
  scripts   one inline script, no libraries: hero aperture pointer parallax over [data-depth] layers; eviction-policy
            console (range + switches -> strip, dial, verdict); hero ask form with mode tabs writing JSON into #code;
            nav sheet menu (focus trap, Esc, scroll-spy); demo subscribe form (sends nothing)
  assets    none: CSS shapes and inline SVG; fonts from Google Fonts

  ADAPTING
  - Soft-UI surfaces (.nm + --offset/--inset/--inner) cast via ::before/::after at z-index -1, so .nm keeps z-index 0
    as its own stacking context; never give one overflow:hidden or the shadow is clipped and it goes flat.
  - The page background must stay the flat --bg-1 the surfaces are filled with; a gradient behind them gives the trick away.
  - Parallax moves the [data-depth] layer; keyframe a child inside it, never the layer itself, or the keyframe wins.
-->
<html lang="en"><head><meta charset=utf8><meta name=viewport content="width=device-width,initial-scale=1,viewport-fit=cover"><style>:root{color-scheme:light;box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px)}html{scroll-padding-top:env(safe-area-inset-top,0px)}body{margin:0;padding:0;font:14px -apple-system,BlinkMacSystemFont,sans-serif;background:#faf9f5;color:#141413}img{max-width:100%}[hidden]:not([hidden=until-found i]){display:none!important}</style></head><body>
<title>Mnemo — a million tokens your agent can reach</title>
<meta name="description" content="A fictional context layer for agents, staged inside a recessed parallax aperture with tokens drifting through it. One file, no images, no libraries." />
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link href="https://fonts.googleapis.com/css2?family=Barlow+Condensed:wght@400;500;600;700&family=Barlow:wght@300;400;500;600;700;800;900&display=swap" rel="stylesheet" />
<style>
:root {
  color-scheme: dark;
  --bg-1: #5531b8;
  --bg-2: #2a0f6e;
  --bg-3: #1a0b4a;
  --coral: #ff6b7d;
  --cream: #ffe8a3;
  --g-warm: linear-gradient(90deg, #ffe8a3 0%, #ff7a5c 100%);
  --g-cool: linear-gradient(90deg, #6f63ff 10%, #f25cff 95%);
  --sans: "Barlow", system-ui, sans-serif;
  --cond: "Barlow Condensed", "Barlow", sans-serif;
  --cubic: cubic-bezier(0.4, 0.35, 0, 1.53);
  --ease: cubic-bezier(0.2, 0.8, 0.2, 1);
  --nm-lit: #7254dc;
  --nm-dim: #3a1c92;
}
* { margin: 0; padding: 0; box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
.nm { position: relative; z-index: 0; background: var(--bg-1); }
.nm::before, .nm::after {
  content: ""; position: absolute; inset: 0;
  border-radius: inherit; z-index: -1; pointer-events: none;
}
.nm--offset::before {
  box-shadow: -10px -10px 30px 0 var(--nm-lit), 10px 10px 30px 0 rgba(22, 6, 72, 0.55);
}
.nm--inner::after {
  box-shadow: inset -10px -10px 10px 0 rgba(22, 6, 72, 0.4), inset 10px 10px 10px 0 var(--nm-lit);
}
.nm--inset::after {
  box-shadow: inset -10px -10px 10px 0 rgba(130, 100, 240, 0.5), inset 10px 10px 10px 0 var(--nm-dim);
}
.nm--wave { box-shadow: inset 4px 4px 6px 0 var(--nm-lit), inset -4px -4px 6px 0 rgba(22, 6, 72, 0.35); }
.nm--wave::before { box-shadow: 4px 4px 6px 0 var(--nm-lit), -4px -4px 6px 0 rgba(22, 6, 72, 0.35); }
.nm--cake { box-shadow: 4px 4px 6px 0 var(--nm-lit); }
.nm--cake::before {
  box-shadow: -20px -20px 20px 0 rgba(160, 120, 230, 0.4), 10px 10px 20px 0 rgba(22, 6, 72, 0.5);
}
html { scroll-behavior: smooth; }
body {
  font-family: var(--sans);
  color: #fff;
  background: var(--bg-1);
  overflow-x: clip;
}
a { color: inherit; text-decoration: none; }
button { font: inherit; color: inherit; border: 0; background: none; cursor: pointer; }
ul { list-style: none; }
.sr { position: absolute; width: 1px; height: 1px; margin: -1px; overflow: hidden; clip: rect(0 0 0 0); white-space: nowrap; }
.wrap { width: min(1140px, 100% - 44px); margin: 0 auto; }

/* film grain over everything: a flat violet field reads as digital, a
   few percent of noise reads as material */
body::after {
  content: ""; position: fixed; inset: 0; z-index: 50; pointer-events: none;
  opacity: 0.03; mix-blend-mode: overlay;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2' stitchTiles='stitch'/%3E%3CfeColorMatrix values='0 0 0 0 1 0 0 0 0 1 0 0 0 0 1 0 0 0 0.9 0'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
}
/* a hairline of light on the top edge of every raised surface, the way a
   real bevel catches the lamp */
.nm--offset { box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1); }

/* the nav is a floating pill: it holds the mark, the account actions and
   the burger, and the menu sheet drops out of it at every width */
/* at the top of the page the nav is a full-width bar that sits on the hero;
   once the page scrolls it gathers into a floating pill */
nav { position: fixed; top: env(safe-area-inset-top, 0px); left: 0; right: 0; z-index: 6; pointer-events: none; }
.menu {
  position: relative; z-index: 2; pointer-events: auto;
  width: 100%; max-width: 100%; height: 76px; margin: 0 auto;
  padding: 0 4%; border-radius: 0;
  display: grid; grid-template-columns: 1fr auto; align-items: center; gap: 16px;
  background: rgba(88, 54, 190, 0); border: 1px solid transparent; border-width: 0 0 1px;
  border-bottom-color: rgba(255, 255, 255, 0.08);
  box-shadow: none;
  transition: max-width 0.55s var(--cubic), height 0.45s var(--ease), padding 0.45s var(--ease),
              border-radius 0.45s var(--ease), transform 0.5s var(--cubic), background 0.35s var(--ease),
              box-shadow 0.4s var(--ease), border-color 0.35s var(--ease);
  animation: drop 0.8s 0.1s var(--cubic) backwards;
}
nav.scrolled .menu {
  max-width: min(880px, calc(100% - 24px)); height: 60px; padding: 0 10px 0 20px;
  border-radius: 30px; transform: translateY(14px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(70, 40, 170, 0.78);
  -webkit-backdrop-filter: blur(18px) saturate(1.4); backdrop-filter: blur(18px) saturate(1.4);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.16), 0 18px 40px -12px rgba(22, 6, 72, 0.75);
}
nav.open .menu { background: rgba(70, 40, 170, 0.92);
  -webkit-backdrop-filter: blur(18px) saturate(1.4); backdrop-filter: blur(18px) saturate(1.4); }
nav.scrolled .sheet { right: max(12px, calc(50% - 440px)); }
@keyframes drop { 0% { opacity: 0; transform: translateY(-16px) scale(0.96); } }
@keyframes fade { 0% { opacity: 0; } }
/* the mark: a recessed disc with a token pill passing through it — the
   aperture, at favicon scale */
.brand { display: inline-flex; align-items: center; gap: 10px; justify-self: start;
  font-size: 19px; font-weight: 700; letter-spacing: -0.02em; }
.brand svg { flex: none; }
.brand:focus-visible { outline: 2px solid var(--cream); outline-offset: 6px; border-radius: 6px; }
.menu-links { display: none; }
.menu-links a {
  padding: 8px 14px; border-radius: 10px;
  font-size: 14.5px; font-weight: 500; color: rgba(255, 255, 255, 0.88);
  transition: color 0.25s ease, background 0.25s ease;
}
.menu-links a:hover { color: #fff; background: rgba(255, 255, 255, 0.06); }
.menu-links a:focus-visible { outline: 2px solid var(--cream); outline-offset: 2px; }
.menu-actions { justify-self: end; display: flex; align-items: center; gap: 8px; }
.menu-actions .signin { padding: 8px 14px; font-size: 14.5px; font-weight: 500; color: rgba(255,255,255,0.88); transition: color 0.25s; }
.menu-actions .signin:hover { color: #fff; }
.signup {
  height: 38px; padding: 0 18px; border-radius: 999px;
  display: inline-flex; align-items: center;
  font-size: 14px; font-weight: 600;
  transition: transform 0.3s var(--cubic);
}
.signup.nm--offset::before { box-shadow: -4px -4px 10px 0 var(--nm-lit), 4px 4px 10px 0 rgba(22,6,72,0.5); }
.signup:hover { transform: translateY(-1px); }
.signup:active { transform: translateY(1px) scale(0.98); }
.signup:focus-visible, .menu-actions .signin:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }
/* the burger is a raised disc like everything else; open, it presses in
   and its three bars fold into a cross */
.burger { display: block; width: 42px; height: 42px; border-radius: 50%; position: relative; z-index: 0;
  background: var(--bg-1); transition: transform 0.35s var(--cubic); }
.burger::after { content: ""; position: absolute; inset: 0; border-radius: inherit; z-index: -1;
  box-shadow: -4px -4px 10px 0 var(--nm-lit), 4px 4px 10px 0 rgba(22,6,72,0.5);
  transition: box-shadow 0.35s var(--ease); }
.burger[aria-expanded="true"]::after {
  box-shadow: inset -3px -3px 6px 0 rgba(130,100,240,0.45), inset 3px 3px 6px 0 var(--nm-dim); }
.burger:active { transform: scale(0.94); }
.burger:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }
.burger i, .burger i::before, .burger i::after {
  position: absolute; left: 50%; top: 50%; width: 18px; height: 2px; margin: -1px 0 0 -9px;
  border-radius: 2px; background: #fff;
}
.burger i { transition: background 0.2s ease; }
.burger i::before, .burger i::after { content: ""; transition: transform 0.45s var(--cubic); }
.burger i::before { transform: translateY(-6px); }
.burger i::after { transform: translateY(6px); }
.burger[aria-expanded="true"] i { background: transparent; }
.burger[aria-expanded="true"] i::before { transform: rotate(45deg); background: var(--cream); }
.burger[aria-expanded="true"] i::after { transform: rotate(-45deg); background: var(--cream); }

/* ---------- the menu: a sheet that drops out of the pill ---------- */
@media all {
  .scrim {
    display: block; position: fixed; inset: 0; z-index: 0; pointer-events: auto;
    background: rgba(22, 6, 72, 0.42);
    -webkit-backdrop-filter: blur(10px) saturate(1.2); backdrop-filter: blur(10px) saturate(1.2);
    opacity: 0; visibility: hidden;
    transition: opacity 0.4s var(--ease), visibility 0s 0.4s;
  }
  .sheet {
    display: block; position: fixed; z-index: 1; pointer-events: auto;
    top: calc(env(safe-area-inset-top, 0px) + 84px); right: max(12px, calc(4% - 4px)); width: min(400px, calc(100% - 24px));
    max-height: calc(100dvh - 100px); overflow-y: auto; overscroll-behavior: contain;
    padding: 10px 10px 14px; border-radius: 26px;
    transform-origin: calc(100% - 28px) -10px;
    opacity: 0; visibility: hidden; transform: translateY(-8px) scale(0.96);
    transition: opacity 0.3s var(--ease), transform 0.45s var(--cubic), visibility 0s 0.45s;
  }
  .sheet.nm--offset::before { box-shadow: -10px -10px 30px 0 rgba(122,85,184,0.6), 16px 22px 44px 0 rgba(22,6,72,0.6); }
  nav.open .scrim { opacity: 1; visibility: visible; transition: opacity 0.4s var(--ease); }
  nav.open .sheet { opacity: 1; visibility: visible; transform: none;
    transition: opacity 0.3s var(--ease), transform 0.55s var(--cubic); }

  .sheet-head { display: flex; justify-content: space-between; align-items: center; padding: 10px 14px 8px; }
  .sheet-head span { font-family: var(--cond); font-size: 13px; font-weight: 600; letter-spacing: 2.4px;
    text-transform: uppercase; color: rgba(255,255,255,0.45); }
  .sheet-head b { font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 11.5px; font-weight: 500;
    color: rgba(255,255,255,0.4); }

  .sheet-links { display: grid; gap: 2px; }
  .sheet-links a {
    position: relative; display: grid; grid-template-columns: 30px 1fr auto; align-items: center; gap: 12px;
    padding: 14px 14px; border-radius: 16px;
    transition: background 0.25s ease;
  }
  .sheet-links a:hover, .sheet-links a:focus-visible { background: rgba(255,255,255,0.05); outline: 0; }
  .sheet-links a:focus-visible { box-shadow: inset 0 0 0 2px rgba(255,232,163,0.6); }
  .sheet-links .n { font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12px;
    color: rgba(255,255,255,0.35); transition: color 0.25s; }
  .sheet-links strong { display: block; font-size: 21px; font-weight: 700; letter-spacing: -0.02em; line-height: 1.15; }
  .sheet-links small { display: block; margin-top: 3px; font-size: 13.5px; color: rgba(255,255,255,0.68); }
  .sheet-links .go-ic {
    width: 32px; height: 32px; border-radius: 50%; display: grid; place-items: center;
    background: var(--bg-1); color: rgba(255,255,255,0.82);
    box-shadow: -3px -3px 6px 0 var(--nm-lit), 3px 3px 6px 0 rgba(22,6,72,0.5);
    transition: transform 0.35s var(--cubic), color 0.25s, box-shadow 0.3s var(--ease);
  }
  .sheet-links a:hover .go-ic { transform: translateX(3px); color: #fff; }
  .sheet-links a:active .go-ic { box-shadow: inset -2px -2px 4px 0 rgba(130,100,240,0.45), inset 2px 2px 4px 0 var(--nm-dim); }
  /* the section you are in is pressed into the sheet, with the token pill
     beside it, the same mark the aperture is made of */
  .sheet-links a[aria-current="true"] {
    background: var(--bg-1);
    box-shadow: inset -4px -4px 8px 0 rgba(130,100,240,0.4), inset 4px 4px 8px 0 var(--nm-dim);
  }
  .sheet-links a[aria-current="true"]::before {
    content: ""; position: absolute; left: -2px; top: 50%; width: 4px; height: 22px; margin-top: -11px;
    border-radius: 4px; background: var(--g-warm);
  }
  .sheet-links a[aria-current="true"] .n { color: var(--cream); }
  .sheet-links a + a::after {
    content: ""; position: absolute; left: 56px; right: 14px; top: -1px; height: 1px;
    background: rgba(255,255,255,0.06);
  }
  .sheet-links a[aria-current="true"]::after, .sheet-links a[aria-current="true"] + a::after { display: none; }

  .sheet-cta { display: grid; grid-template-columns: 1fr 1fr; gap: 10px; margin: 14px 4px 0; }
  .sheet-cta a {
    height: 48px; border-radius: 14px; display: grid; place-items: center;
    font-size: 15px; font-weight: 600; position: relative; z-index: 0;
    transition: transform 0.35s var(--cubic);
  }
  .sheet-cta a:active { transform: scale(0.97); }
  .sheet-cta a:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }
  .sheet-cta .ghost { background: var(--bg-1); }
  .sheet-cta .ghost::after { content: ""; position: absolute; inset: 0; border-radius: inherit; z-index: -1;
    box-shadow: inset -4px -4px 8px 0 rgba(130,100,240,0.4), inset 4px 4px 8px 0 var(--nm-dim); }
  .sheet-cta .solid { background: linear-gradient(135deg, #ffad5c, var(--coral)); color: #fff;
    box-shadow: 0 12px 22px rgba(43,12,85,0.45), inset 0 1px 0 rgba(255,255,255,0.35); }
  .sheet-foot { display: flex; justify-content: center; gap: 8px; align-items: center; margin-top: 14px;
    font-size: 13px; color: rgba(255,255,255,0.68); }
  .sheet-foot i { width: 6px; height: 6px; border-radius: 50%; background: var(--coral);
    box-shadow: 0 0 0 4px rgba(255,107,125,0.18); }

  /* the rows arrive one after another once the sheet has opened */
  .sheet .stagger { opacity: 0; transform: translateY(-6px); transition: opacity 0.2s ease, transform 0.2s ease; }
  nav.open .sheet .stagger { opacity: 1; transform: none;
    transition: opacity 0.45s var(--ease), transform 0.55s var(--cubic);
    transition-delay: calc(0.08s + var(--s, 0) * 0.05s); }
}

.stage {
  position: relative;
  padding: 132px 0 0;
  overflow: hidden;
  background:
    linear-gradient(rgba(255,255,255,0.045) 1px, transparent 1px) 0 0 / 96px 96px,
    linear-gradient(90deg, rgba(255,255,255,0.045) 1px, transparent 1px) 0 0 / 96px 96px,
    var(--bg-1);
}
.stage::after {
  content: ""; position: absolute; inset: auto 0 0; height: 55%;
  pointer-events: none; z-index: 0;
  background: linear-gradient(transparent, var(--bg-1) 55%);
}
.scene { position: absolute; inset: 0 0 auto; height: 760px; opacity: 0.55; }
/* the tokens go out of focus behind the copy: the nearest layer stays
   crisp, the two behind it soften, so the aperture reads as depth rather
   than as traffic crossing the headline */
.l-two .piece { filter: blur(2px); }
.l-three .piece { filter: blur(6px); }
/* the light the input card sits in */
.glow {
  position: absolute; z-index: 1; left: 50%; top: 380px;
  width: 980px; height: 560px; transform: translateX(-50%);
  pointer-events: none;
  background: radial-gradient(ellipse 50% 50% at 50% 50%,
    rgba(255, 150, 110, 0.34) 0%, rgba(242, 92, 255, 0.22) 40%, transparent 70%);
  animation: fade 1.6s 0.9s ease backwards, breathe 7s 2.5s ease-in-out infinite;
}
.layer {
  position: absolute; top: 20%; left: 20%;
  width: 60%; height: 60%; min-width: 400px; min-height: 400px;
  will-change: transform;
}
.layer .content {
  position: absolute; top: 50%; left: 50%;
  width: 1800px; height: 660px;
  display: flex; align-items: center; justify-content: center;
  transform: translate(-50%, -50%);
  animation: open 0.8s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
@keyframes open { 0% { width: 0; } }
.disc::before {
  content: ""; position: absolute; top: 50%; left: 50%;
  width: 800px; height: 800px; border-radius: 50%;
  background: var(--bg-1);
  box-shadow: inset -18px -18px 34px 0 rgba(130, 100, 240, 0.42),
              inset 18px 18px 34px 0 var(--nm-dim);
  transform: translate(-50%, -50%);
  animation: iris 0.8s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
.l-one .content::before {
  content: ""; position: absolute;
  width: 600px; height: 600px; border-radius: 50%;
  background: var(--bg-1);
  box-shadow: inset -16px -16px 30px 0 rgba(130, 100, 240, 0.38),
              inset 16px 16px 30px 0 var(--nm-dim);
  animation: iris 0.8s 0.4s cubic-bezier(1, 0.06, 0.25, 1) backwards;
}
@keyframes iris { 0% { width: 0; height: 0; } }
.piece {
  position: absolute; display: flex; z-index: 1;
  border-radius: 80px;
  animation: drift-l 13s cubic-bezier(1, 0.06, 0.25, 1) infinite both;
}
@keyframes drift-l { 50% { left: 80%; width: 56px; } }
@keyframes drift-r { 50% { right: 80%; width: 56px; } }
.piece.to-l { animation-name: drift-l; }
.piece.to-r { animation-name: drift-r; }
.l-one .piece { background: var(--g-cool); }
.l-one .piece:nth-child(1) { right: 7%; top: 12%; width: 260px; height: 56px; animation-delay: 0.5s; }
.l-one .piece:nth-child(2) { left: 9%; top: 44%; width: 320px; height: 82px; animation-delay: 1s; }
.l-one .piece:nth-child(3) { left: 30%; top: 80%; width: 170px; height: 38px; animation-delay: 1.5s; }
.l-one .piece:nth-child(4) { left: 14%; top: 64%; width: 230px; height: 48px; animation-delay: 7.5s; }
.l-two .piece { background: var(--g-warm); }
.l-two .piece:nth-child(1) { left: 6%; top: 22%; width: 280px; height: 70px; animation-delay: 2s; }
.l-two .piece:nth-child(2) { right: 14%; top: 19%; width: 380px; height: 88px; animation-delay: 2.5s; }
.l-two .piece:nth-child(3) { right: 5%; top: 85%; width: 300px; height: 40px; animation-delay: 3s; }
.l-two .piece:nth-child(4) { right: 10%; top: 58%; width: 260px; height: 56px; animation-delay: 9.5s; }
.l-three .piece { background: var(--coral); }
.l-three .piece:nth-child(1) { left: 19%; top: 30%; width: 180px; height: 36px; animation-delay: 3.5s; }
.l-three .piece:nth-child(2) { right: 22%; top: 57%; width: 290px; height: 66px; animation-delay: 4s; }
.l-three .piece:nth-child(3) { left: 36%; top: 70%; width: 180px; height: 38px; animation-delay: 4.5s; }
.l-three .piece:nth-child(4) { left: 4%; top: 15%; width: 240px; height: 44px; animation-delay: 11s; }
.layer.figure {
  display: flex !important; align-items: center; justify-content: center;
  top: 3%; height: 54%;
  z-index: 2;
}
.fig-in {
  display: flex; align-items: center;
  font-size: 200px; font-weight: 700; letter-spacing: 4px; line-height: 1;
  animation: punch 0.6s 1.2s cubic-bezier(0.3, 0.8, 1, 1.05) both;
}
@keyframes punch { 0% { opacity: 0; transform: scale(10) skew(20deg, 20deg); } }
.fig-in span { font-size: 0.23em; font-weight: 600; letter-spacing: 2px; align-self: flex-end; margin: 0 0 1.5em 0.18em; opacity: 0.7; }
.figure.back { color: var(--bg-2); z-index: 1; filter: blur(10px); opacity: 0.8; }
.figure.back .fig-in { animation-delay: 1s; }
@keyframes breathe { 50% { opacity: 0.7; transform: translateX(-50%) scale(1.06); } }
@keyframes lift { 0% { opacity: 0; transform: translateY(40px); } }

/* ---------- hero: badge, headline, sub, input card ---------- */
.corner {
  position: absolute; z-index: 1;
  font-family: var(--cond); font-size: 13px; letter-spacing: 2px; color: rgba(255,255,255,0.38);
}
.c-tl { top: 104px; left: 4%; } .c-tr { top: 104px; right: 4%; }
.c-bl { top: 440px; left: 4%; } .c-br { top: 440px; right: 4%; }

.hero {
  position: relative; z-index: 3; text-align: center;
  display: flex; flex-direction: column; align-items: center;
}
.pill {
  display: inline-flex; align-items: center; gap: 10px;
  height: 34px; padding: 0 6px 0 16px; border-radius: 40px;
  font-size: 13px; font-weight: 500; letter-spacing: 0.3px;
}
.pill.nm--offset::before { box-shadow: -4px -4px 10px 0 var(--nm-lit), 4px 4px 10px 0 rgba(22,6,72,0.5); }
.pill i {
  width: 22px; height: 22px; border-radius: 50%; display: grid; place-items: center;
  background: var(--bg-2); font-style: normal; font-size: 12px;
}
.pill:focus-visible { outline: 2px solid var(--cream); outline-offset: 4px; }
.hero h1 {
  margin-top: 8px;
  font-size: clamp(40px, 6.6vw, 80px); font-weight: 800; line-height: 1.0;
  letter-spacing: -0.045em;
  text-shadow: 0 2px 24px rgba(22, 6, 72, 0.45);
}
/* each line rises out of its own mask, one after the other */
.hero h1 .line { display: block; overflow: hidden; padding: 0.04em 0.06em 0.1em; margin: -0.04em -0.06em -0.1em; }
.hero h1 .line > span { display: inline-block; animation: rise 0.9s var(--ease) backwards; }
.hero h1 .line:nth-child(1) > span { animation-delay: 0.35s; }
.hero h1 .line:nth-child(2) > span { animation-delay: 0.47s; }
@keyframes rise { 0% { transform: translateY(105%); } }
.hero h1 em {
  font-style: normal; text-shadow: none;
  background: var(--g-warm); -webkit-background-clip: text; background-clip: text; color: transparent;
}
.hero .sub {
  margin-top: 22px; max-width: 42ch;
  font-size: 18px; font-weight: 400; line-height: 1.6; color: rgba(255, 255, 255, 0.82);
}
.hero .sub span {
  padding: 1px 8px; border-radius: 6px; white-space: nowrap;
  background: rgba(43, 12, 85, 0.45); color: var(--cream);
}

.ask { margin-top: 38px; width: min(620px, 100%); border-radius: 22px; text-align: left;
  transition: transform 0.4s var(--ease); }
.ask:focus-within { transform: translateY(-2px); }
.ask:focus-within::before { box-shadow: -12px -12px 34px 0 var(--nm-lit), 14px 14px 36px 0 rgba(22, 6, 72, 0.6), 0 0 0 1px rgba(255, 232, 163, 0.18); }
.ask::before { transition: box-shadow 0.4s var(--ease); }

/* the entrance, in order: nav, aperture, badge, headline lines, sub,
   the card, then the window — each step lands before the next starts */
.hero > .pill { animation: lift 0.7s 0.2s var(--ease) backwards; }
.hero > .sub { animation: lift 0.7s 0.62s var(--ease) backwards; }
.hero > .ask { animation: land 0.9s 0.76s var(--ease) backwards; }
@keyframes land { 0% { opacity: 0; transform: translateY(28px) scale(0.97); } }
.ask-field { display: flex; align-items: center; gap: 12px; padding: 20px 22px 16px; }
.ask-field svg { flex: none; opacity: 0.55; }
.ask-field input {
  flex: 1; min-width: 0; background: none; border: 0; outline: 0;
  font: inherit; font-size: 16px; color: #fff;
}
.ask-field input::placeholder { color: rgba(255, 255, 255, 0.45); }
.ask-bar {
  display: flex; align-items: center; justify-content: space-between; gap: 12px;
  padding: 12px 12px 12px 14px; border-top: 1px solid rgba(255, 255, 255, 0.08);
}
.modes { display: flex; gap: 4px; padding: 5px; border-radius: 14px; overflow-x: auto; scrollbar-width: none; }
.modes::-webkit-scrollbar { display: none; }
.modes.nm--inset::after {
  box-shadow: inset -4px -4px 6px 0 rgba(130,100,240,0.45), inset 4px 4px 6px 0 var(--nm-dim);
}
.mode {
  display: inline-flex; align-items: center; gap: 7px;
  height: 32px; padding: 0 12px; border-radius: 10px;
  font-size: 13.5px; font-weight: 500; white-space: nowrap; color: rgba(255, 255, 255, 0.74);
  transition: color 0.25s, background 0.25s, box-shadow 0.3s var(--ease), transform 0.35s var(--cubic);
}
.mode:hover { color: #fff; }
.mode:active { transform: scale(0.95); }
.mode[aria-selected="true"] {
  color: #fff; background: var(--bg-1);
  box-shadow: -3px -3px 6px 0 var(--nm-lit), 3px 3px 6px 0 rgba(22, 6, 72, 0.5);
}
.mode .ic { width: 12px; height: 4px; border-radius: 4px; background: var(--g-cool); }
.mode:nth-child(2) .ic { background: var(--g-warm); }
.mode:nth-child(3) .ic { background: var(--coral); }
.mode:nth-child(4) .ic { background: var(--cream); }
.mode .new {
  font-family: var(--cond); font-size: 11px; letter-spacing: 1px; text-transform: uppercase;
  padding: 1px 6px; border-radius: 6px; background: rgba(43, 12, 85, 0.55); color: var(--cream);
}
.go {
  flex: none; width: 52px; height: 40px; border-radius: 12px; display: grid; place-items: center;
  background: linear-gradient(135deg, #ffad5c, var(--coral)); color: #fff;
  box-shadow: 0 10px 18px rgba(43, 12, 85, 0.45);
  box-shadow: 0 10px 18px rgba(43, 12, 85, 0.45), inset 0 1px 0 rgba(255, 255, 255, 0.35);
  transition: transform 0.35s var(--cubic), box-shadow 0.25s;
}
.go svg { transition: transform 0.35s var(--cubic); }
.go:hover { transform: translateY(1px); box-shadow: 0 4px 8px rgba(43, 12, 85, 0.45), inset 0 1px 0 rgba(255,255,255,0.35); }
.go:hover svg { transform: translateX(3px); }
.go:active { transform: scale(0.93); }
.go:focus-visible, .mode:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }

/* ---------- hero: the preview window ---------- */
.preview { position: relative; z-index: 3; margin-top: 72px; animation: lift 1s 1s var(--ease) backwards; }
.win { border-radius: 22px; }
.win-bar { display: flex; align-items: center; gap: 14px; padding: 14px 18px; border-bottom: 1px solid rgba(255,255,255,0.08); }
.dots { display: flex; gap: 7px; }
.dots i { width: 10px; height: 10px; border-radius: 50%; background: rgba(255, 255, 255, 0.18); }
.urlbar {
  flex: 1; max-width: 420px; height: 26px; border-radius: 20px; padding: 0 12px;
  display: flex; align-items: center;
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; font-size: 12px; color: rgba(255,255,255,0.5);
}
.urlbar.nm--inset::after { box-shadow: inset -3px -3px 5px 0 rgba(130,100,240,0.4), inset 3px 3px 5px 0 var(--nm-dim); }
.win-body { display: grid; grid-template-columns: 1fr 1.05fr; min-height: 330px; }
.win-left { padding: 26px 24px; display: grid; align-content: start; gap: 16px; }
.sk-row { display: flex; gap: 10px; align-items: center; }
.sk { height: 12px; border-radius: 20px; background: rgba(255, 255, 255, 0.09); }
.sk.lab {
  height: auto; padding: 3px 9px; border-radius: 6px;
  font-family: var(--cond); font-size: 12px; letter-spacing: 1.4px; text-transform: uppercase;
  color: rgba(255, 255, 255, 0.62); background: rgba(43, 12, 85, 0.4);
}
.sk-card { padding: 16px; border-radius: 14px; border: 1px solid rgba(255, 107, 125, 0.45); display: grid; gap: 10px; }
.sk-card .bar { height: 10px; width: 30%; border-radius: 10px; background: var(--g-warm); opacity: 0.85; }
.win-code { position: relative; min-width: 0; border-left: 1px solid rgba(255,255,255,0.08); padding: 14px 0 60px; }
.code-head {
  display: flex; justify-content: space-between; align-items: center; padding: 0 18px 10px;
  font-family: var(--cond); font-size: 13px; letter-spacing: 2px; color: rgba(255, 255, 255, 0.4);
}
.code {
  margin: 0; padding: 0 18px; counter-reset: ln; white-space: pre; overflow-x: auto;
  font-family: ui-monospace, SFMono-Regular, Menlo, Consolas, monospace; font-size: 13px; line-height: 1.8;
  color: rgba(255, 255, 255, 0.75); transition: opacity 0.3s ease;
}
.code.dim { opacity: 0.3; }
/* the response writes itself in, a line at a time; --base is the wait
   before the first line (long on page load, short on a re-run) */
.code .ln { display: block; animation: type-in 0.4s var(--ease) backwards;
  animation-delay: calc(var(--base, 0ms) + var(--i, 0) * 55ms); }
@keyframes type-in { 0% { opacity: 0; transform: translateX(-6px); clip-path: inset(0 100% 0 0); } }
/* the block in the page the response came from lights up with it */
.sk-card { transition: border-color 0.5s ease, box-shadow 0.5s ease, background 0.5s ease; }
.sk-card.hit { border-color: rgba(255, 232, 163, 0.7); background: rgba(255, 232, 163, 0.04);
  box-shadow: 0 0 0 4px rgba(255, 107, 125, 0.12), 0 0 32px rgba(255, 107, 125, 0.18); }
.code .ln::before { counter-increment: ln; content: counter(ln); display: inline-block; width: 2.2em; color: rgba(255,255,255,0.28); }
.code .k { color: #fff; } .code .s { color: var(--coral); } .code .n { color: var(--cream); } .code .b { color: #c9b8ff; }
.status {
  position: absolute; right: 18px; bottom: 16px; height: 30px; padding: 0 14px; border-radius: 20px;
  display: inline-flex; align-items: center; gap: 8px;
  font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 12px;
}
.status.nm--offset::before { box-shadow: -3px -3px 7px 0 var(--nm-lit), 3px 3px 7px 0 rgba(22,6,72,0.5); }
.status i { width: 7px; height: 7px; border-radius: 50%; background: var(--cream); }
.status.busy i { background: var(--coral); animation: blink 0.8s infinite; }
@keyframes blink { 50% { opacity: 0.2; } }

/* ---------- hero: trusted-by strip ---------- */
.trust {
  position: relative; z-index: 3; margin-top: 72px;
  display: grid; grid-template-columns: 1.2fr repeat(5, 1fr); align-items: stretch;
  border-top: 1px solid rgba(255, 255, 255, 0.08);
}
.trust > * { padding: 28px 16px; display: grid; place-items: center; border-left: 1px solid rgba(255,255,255,0.08); }
.trust p { border-left: 0; padding-left: 0; place-items: center start; font-size: 14.5px; line-height: 1.4; color: rgba(255,255,255,0.82); }
.trust p b { color: var(--coral); font-weight: 600; }
.trust > span {
  font-family: var(--cond); font-weight: 600; font-size: 19px; letter-spacing: 1.5px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.62); text-align: center;
}

@media (max-width: 799px) {
  .stage { padding-top: 112px; }
  .corner { display: none; }
  .ask-bar { padding: 10px; gap: 8px; }
  .mode { padding: 0 9px; gap: 6px; font-size: 13px; }
  .mode .ic { display: none; }
  .mode .new { display: none; }
  .go { width: 44px; }
  .scene { opacity: 0.42; }
  .win-body { grid-template-columns: 1fr; min-height: 0; }
  .win-left { display: none; }
  .win-code { border-left: 0; }
  .trust { grid-template-columns: repeat(2, 1fr); }
  .trust p { grid-column: 1 / -1; place-items: center; text-align: center; padding: 22px 0 10px; }
  .trust > * { padding: 16px 10px; }
  .trust > span:nth-of-type(odd) { border-left: 0; }
  .trust > span:last-child { display: none; }
}
.eyebrow {
  font-family: var(--cond); font-size: 15px; font-weight: 600;
  letter-spacing: 4px; text-transform: uppercase; color: var(--cream);
  opacity: 0.85; margin-bottom: 14px;
}
.lede h1 {
  font-size: clamp(27px, 3.4vw, 38px); font-weight: 700; line-height: 1.16;
  letter-spacing: -0.01em; text-wrap: balance;
  text-shadow: 6px 6px 16px var(--bg-3);
}
.lede p {
  margin: 14px auto 28px; max-width: 46ch;
  font-size: 17px; line-height: 1.55; letter-spacing: 0.3px;
  text-shadow: 6px 6px 10px var(--bg-3);
}
.cta { display: flex; gap: 12px; justify-content: center; flex-wrap: wrap; }
.btn {
  height: 42px; padding: 0 28px; border-radius: 50px;
  font-family: var(--sans); font-weight: 600; font-size: 12px;
  letter-spacing: 1.4px; text-transform: uppercase;
  display: inline-flex; align-items: center;
  transition: all 0.3s ease;
}
.btn--solid { background: #fff; color: var(--bg-1); box-shadow: 0 15px 20px rgba(43, 12, 85, 0.5); }
.btn--solid:hover { background: var(--coral); color: #fff; transform: translateY(5px); box-shadow: 0 10px 10px -10px rgba(43, 12, 85, 0.5); }
.btn--ghost { border: 1px solid rgba(255, 255, 255, 0.4); }
.btn--ghost:hover { border-color: #fff; background: rgba(255, 255, 255, 0.1); transform: translateY(5px); }
.btn:focus-visible { outline: 2px solid var(--cream); outline-offset: 4px; }

.band { position: relative; z-index: 2; background: var(--bg-1); }
.sec { padding: 104px 0; }
.sec-head { max-width: 640px; margin-bottom: 52px; }
.sec-head h2 {
  margin-top: 12px; font-size: clamp(30px, 4vw, 44px); font-weight: 700;
  line-height: 1.1; letter-spacing: -0.02em; text-wrap: balance;
}
.sec-head p { margin-top: 14px; font-size: 17px; line-height: 1.6; color: rgba(255, 255, 255, 0.84); }
.grid-3 { display: grid; grid-template-columns: repeat(3, 1fr); gap: 22px; }
.card {
  padding: 34px 30px 36px; border-radius: 22px;
  transition: transform 0.4s var(--ease);
}
.card:hover { transform: translateY(-6px); }
.card::before { transition: opacity 0.4s var(--ease); }
.card::after { opacity: 0; transition: opacity 0.4s var(--ease);
  box-shadow: inset -10px -10px 10px 0 rgba(22, 6, 72, 0.4), inset 10px 10px 10px 0 var(--nm-lit); }
.card:active { transform: translateY(0); }
.card:active::before { opacity: 0; }
.card:active::after { opacity: 1; }
.dot {
  width: 62px; height: 62px; border-radius: 50%; margin-bottom: 22px;
  display: grid; place-items: center;
}
.dot i { display: block; width: 26px; height: 9px; border-radius: 40px; background: var(--g-cool); }
.card:nth-child(2) .dot i { width: 18px; background: var(--g-warm); }
.card:nth-child(3) .dot i { width: 30px; background: var(--coral); }
.card h3 { font-size: 21px; font-weight: 700; letter-spacing: -0.01em; margin-bottom: 10px; }
.card p { font-size: 15.5px; line-height: 1.65; color: rgba(255, 255, 255, 0.84); }
.card .tag {
  display: inline-block; margin-top: 20px;
  font-family: var(--cond); font-size: 13px; font-weight: 600;
  letter-spacing: 2.4px; text-transform: uppercase; color: var(--cream); opacity: 0.8;
}
.stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 20px; }
.stat { padding: 28px 26px 30px; border-radius: 20px; }
.stat b {
  display: block; font-size: 42px; font-weight: 800; letter-spacing: -0.02em; line-height: 1;
  background: var(--g-warm); -webkit-background-clip: text; background-clip: text; color: transparent;
}
.stat span {
  display: block; margin-top: 12px;
  font-family: var(--cond); font-size: 14px; font-weight: 500;
  letter-spacing: 2px; text-transform: uppercase; color: rgba(255, 255, 255, 0.72); line-height: 1.5;
}
.note {
  margin-top: 26px; text-align: center;
  font-family: var(--cond); font-size: 14px; letter-spacing: 2px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.42);
}
.console { display: grid; grid-template-columns: 1.15fr 1fr; gap: 26px; align-items: stretch; }
.panel { padding: 34px 32px 36px; border-radius: 26px; }
.panel h3 { font-size: 20px; font-weight: 700; margin-bottom: 4px; }
.panel .hint { font-family: var(--cond); font-size: 14px; letter-spacing: 1.6px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.62); margin-bottom: 26px; }
.row { display: flex; align-items: center; justify-content: space-between; gap: 18px; padding: 15px 0; }
.row + .row { border-top: 1px solid rgba(255, 255, 255, 0.07); }
.row b { display: block; font-size: 16px; font-weight: 600; }
.row small { display: block; font-size: 13.5px; color: rgba(255, 255, 255, 0.7); line-height: 1.45; }
.sw { flex: none; width: 66px; height: 34px; border-radius: 40px; position: relative; z-index: 0;
  background: var(--bg-1); cursor: pointer; }
.sw::after { content: ""; position: absolute; inset: 0; border-radius: inherit; z-index: -1;
  box-shadow: inset -6px -6px 8px 0 rgba(130, 100, 240, 0.42), inset 6px 6px 8px 0 var(--nm-dim); }
.sw i {
  position: absolute; top: 4px; left: 4px; width: 26px; height: 26px; border-radius: 50%;
  background: var(--bg-1);
  box-shadow: -4px -4px 7px 0 var(--nm-lit), 4px 4px 7px 0 rgba(22, 6, 72, 0.55);
  transition: transform 0.32s var(--cubic), background 0.32s ease;
}
.sw[aria-pressed="true"] i { transform: translateX(32px); background: var(--coral); }
.sw:focus-visible { outline: 2px solid var(--cream); outline-offset: 4px; }
.slider { margin-top: 8px; }
.track { position: relative; z-index: 0; height: 26px; border-radius: 40px; background: var(--bg-1); }
.track::after { content: ""; position: absolute; inset: 0; border-radius: inherit; z-index: -1;
  box-shadow: inset -6px -6px 8px 0 rgba(130, 100, 240, 0.42), inset 6px 6px 8px 0 var(--nm-dim); }
.track .fill { position: absolute; top: 7px; left: 8px; height: 12px; border-radius: 40px;
  background: var(--g-warm); width: calc((100% - 16px) * var(--v, 0.5)); pointer-events: none; }
.track input {
  position: absolute; inset: 0; width: 100%; height: 100%;
  opacity: 0; cursor: pointer; margin: 0;
}
.track input:focus-visible + .fill { outline: 2px solid var(--cream); outline-offset: 6px; }
.readout { display: flex; justify-content: space-between; margin-top: 12px;
  font-family: var(--cond); font-size: 14px; letter-spacing: 1.6px; text-transform: uppercase;
  color: rgba(255, 255, 255, 0.68); }
.readout b { color: var(--cream); font-weight: 600; }
/* ---------- the run model: ring + legend, span strip, sentence ---------- */
.dial { display: flex; flex-direction: column; gap: 22px; padding: 30px 28px 28px; border-radius: 26px; }
.dial-top { display: grid; grid-template-columns: auto 1fr; gap: 26px; align-items: center; }
.dial-head { display: flex; justify-content: space-between; align-items: baseline; gap: 12px; }
.dial-head h3 { font-size: 20px; font-weight: 700; }
.dial-head span { font-family: var(--cond); font-size: 14px; letter-spacing: 1.6px; text-transform: uppercase;
  color: rgba(255, 255, 255, 0.62); white-space: nowrap; }

.arc { position: absolute; inset: 0; width: 100%; height: 100%; transform: rotate(-90deg); overflow: visible; }
.arc circle { fill: none; stroke-width: 9; }
.arc .bed { stroke: rgba(22, 6, 72, 0.22); }
.arc .seg { transition: stroke-dasharray 0.7s var(--ease), stroke-dashoffset 0.7s var(--ease), stroke 0.4s ease, opacity 0.4s ease; }
.seg.pin { stroke: var(--cream); }
.seg.keep { stroke: #a48af0; }
.seg.stub { stroke: rgba(255, 255, 255, 0.55); stroke-dasharray: 0 999; }
.dial.over .seg.pin { stroke: var(--coral); }
.dial-sub { display: block; margin-top: 5px; font-family: var(--cond); font-size: 11.5px; letter-spacing: 1.4px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.62); text-align: center; }
.ring .ring .ring { flex-direction: column; }
.dial.over .dial-val { background: var(--coral); -webkit-background-clip: text; background-clip: text; }

.legend { display: grid; gap: 12px; }
.legend li { display: grid; grid-template-columns: 12px 1fr auto; gap: 10px; align-items: center; font-size: 14.5px; }
.legend li span { color: rgba(255, 255, 255, 0.84); }
.legend li b { font-family: ui-monospace, SFMono-Regular, Menlo, monospace; font-size: 13px; font-weight: 500;
  color: #fff; font-variant-numeric: tabular-nums; transition: color 0.3s; }
.legend li.dim b, .legend li.dim span { color: rgba(255, 255, 255, 0.35); }
.legend i { width: 12px; height: 6px; border-radius: 4px; }
.legend .k-pin i { background: var(--cream); }
.legend .k-keep i { background: #a48af0; }
.legend .k-stub i { background: repeating-linear-gradient(135deg, rgba(255,255,255,0.6) 0 2px, transparent 2px 4px); outline: 1px solid rgba(255,255,255,0.35); }
.legend .k-gone i { border: 1px dashed rgba(255, 255, 255, 0.5); }

/* the run itself, oldest top-left to newest bottom-right; each span is as
   wide as it is heavy, and changes state in place when the policy does */
.strip { padding: 14px; border-radius: 16px; display: grid; gap: 7px; }
.strip.nm--inset::after { box-shadow: inset -5px -5px 9px 0 rgba(130,100,240,0.4), inset 5px 5px 9px 0 var(--nm-dim); }
.strip-row { display: flex; gap: 5px; height: 16px; }
.span {
  position: relative; flex: var(--w) 1 0; min-width: 6px; border-radius: 6px;
  background: #a48af0;
  transition: flex-grow 0.6s var(--ease), background 0.4s ease, opacity 0.4s ease, box-shadow 0.4s ease, border-color 0.4s ease;
  border: 1px solid transparent;
}
.span[data-s="pin"] { background: var(--cream); box-shadow: 0 0 10px rgba(255, 232, 163, 0.35); }
.span[data-s="gone"] { background: transparent; border: 1px dashed rgba(255, 255, 255, 0.32); }
.span[data-s="stub"] { flex-grow: 4; background: repeating-linear-gradient(135deg, rgba(255,255,255,0.55) 0 2px, transparent 2px 4px);
  border-color: rgba(255, 255, 255, 0.35); }
.dial.over .span[data-s="pin"] { background: var(--coral); box-shadow: 0 0 10px rgba(255, 107, 125, 0.45); }
/* a cited span carries the coral dot whatever state it is in */
.span[data-cited]::after { content: ""; position: absolute; top: -3px; right: -2px; width: 6px; height: 6px;
  border-radius: 50%; background: var(--coral); box-shadow: 0 0 0 2px var(--bg-1); }
/* tool results get a notch, so pinning them is visibly a different set */
.span[data-type="tool"]::before { content: ""; position: absolute; left: 4px; top: 50%; width: 4px; height: 4px;
  margin-top: -2px; border-radius: 50%; background: rgba(22, 6, 72, 0.55); }
.span.flash { animation: flash 0.7s var(--ease); }
@keyframes flash { 40% { transform: translateY(-3px); filter: brightness(1.35); } }
.strip-axis { display: flex; justify-content: space-between; margin-top: 2px;
  font-family: var(--cond); font-size: 12px; letter-spacing: 1.6px; text-transform: uppercase; color: rgba(255,255,255,0.4); }
.strip-key { display: flex; gap: 14px; }
.strip-key em { font-style: normal; display: inline-flex; align-items: center; gap: 6px; }
.strip-key em::before { content: ""; width: 6px; height: 6px; border-radius: 50%; }
.strip-key .kc::before { background: var(--coral); }
.strip-key .kt::before { background: rgba(22, 6, 72, 0.7); box-shadow: 0 0 0 2px #a48af0; }

.verdict { min-height: 3.2em; font-size: 15px; line-height: 1.6; color: rgba(255, 255, 255, 0.88); }
.verdict b { color: #fff; font-weight: 600; }
.dial.over .verdict b.warn { color: var(--coral); }
.dial-head h3 { white-space: nowrap; }
@media (max-width: 520px) {
  .dial-top { grid-template-columns: 1fr; justify-items: center; }
  .legend { width: 100%; }
  .dial-head { flex-wrap: wrap; }
  .strip-axis { flex-wrap: wrap; row-gap: 8px; }
  .strip-key { order: 3; width: 100%; justify-content: center; }
}
.ring { position: relative; z-index: 0; width: 210px; height: 210px; border-radius: 50%; background: var(--bg-1);
  display: grid; place-items: center; flex: none; }
.ring::after { content: ""; position: absolute; inset: 0; border-radius: inherit; z-index: -1;
  box-shadow: inset -12px -12px 20px 0 rgba(130, 100, 240, 0.4), inset 12px 12px 20px 0 var(--nm-dim); }
.ring .ring { width: 148px; height: 148px; }
.ring .ring .ring { width: 96px; height: 96px; }
.ring .ring .ring::after {
  box-shadow: -8px -8px 14px 0 var(--nm-lit), 8px 8px 14px 0 rgba(22, 6, 72, 0.55);
}
.dial-val { font-size: 30px; font-weight: 800; letter-spacing: -0.02em; line-height: 1;
  background: var(--g-warm); -webkit-background-clip: text; background-clip: text; color: transparent; }
.dial-lab { margin-top: 18px; font-family: var(--cond); font-size: 14px; letter-spacing: 2px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.68); text-align: center; }
.plans { display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; }
.plan { padding: 34px 30px 36px; border-radius: 24px; display: flex; flex-direction: column; }
.plan-name { font-family: var(--cond); font-size: 15px; font-weight: 600; letter-spacing: 3px;
  text-transform: uppercase; color: var(--cream); opacity: 0.85; }
.price { margin: 18px 0 22px; padding: 18px 20px; border-radius: 18px; text-align: center; }
.price b { font-size: 36px; font-weight: 800; letter-spacing: -0.02em; }
.price span { font-family: var(--cond); font-size: 14px; letter-spacing: 1.6px;
  text-transform: uppercase; color: rgba(255, 255, 255, 0.68); display: block; margin-top: 2px; }
.plan ul { display: grid; gap: 10px; margin-bottom: 26px; }
.plan li { position: relative; padding-left: 26px; font-size: 15px; line-height: 1.5;
  color: rgba(255, 255, 255, 0.85); }
.plan li::before { content: ""; position: absolute; left: 0; top: 8px;
  width: 14px; height: 6px; border-radius: 40px; background: var(--g-cool); }
.plan .btn { margin-top: auto; align-self: stretch; justify-content: center; }
.qa { display: grid; gap: 14px; max-width: 820px; }
.q { border-radius: 18px; }
.q::before { box-shadow: -6px -6px 14px 0 var(--nm-lit), 6px 6px 14px 0 rgba(22, 6, 72, 0.5); }
.q[open]::before { box-shadow: -3px -3px 8px 0 var(--nm-lit), 3px 3px 8px 0 rgba(22, 6, 72, 0.4); }
.q summary {
  list-style: none; cursor: pointer; padding: 20px 24px;
  font-size: 17px; font-weight: 600; display: flex; align-items: center; justify-content: space-between; gap: 16px;
}
.q summary::-webkit-details-marker { display: none; }
.q summary i {
  flex: none; width: 26px; height: 26px; border-radius: 50%; position: relative; z-index: 0;
  background: var(--bg-1);
  box-shadow: -3px -3px 6px 0 var(--nm-lit), 3px 3px 6px 0 rgba(22, 6, 72, 0.55);
  transition: transform 0.3s var(--ease);
}
.q summary i::before, .q summary i::after {
  content: ""; position: absolute; top: 50%; left: 50%; width: 11px; height: 2px; border-radius: 2px;
  background: var(--cream); transform: translate(-50%, -50%);
}
.q summary i::after { transform: translate(-50%, -50%) rotate(90deg); transition: opacity 0.3s ease; }
.q[open] summary i { transform: rotate(180deg); }
.q[open] summary i::after { opacity: 0; }
.q p { padding: 0 24px 22px; font-size: 15.5px; line-height: 1.65; color: rgba(255, 255, 255, 0.84); }
.steps { display: grid; grid-template-columns: repeat(3, 1fr); gap: 22px; }
.step { position: relative; padding-top: 30px; }
.step::before {
  content: ""; position: absolute; top: 0; left: 0; right: 22px;
  height: 9px; border-radius: 40px; background: var(--g-cool); opacity: 0.85;
}
.step:nth-child(2)::before { background: var(--g-warm); }
.step:nth-child(3)::before { background: var(--coral); right: 0; }
.step b {
  display: block; font-family: var(--cond); font-size: 14px; font-weight: 600;
  letter-spacing: 3px; text-transform: uppercase; color: var(--cream); opacity: 0.85; margin-bottom: 10px;
}
.step h3 { font-size: 20px; font-weight: 700; margin-bottom: 9px; letter-spacing: -0.01em; }
.step p { font-size: 15.5px; line-height: 1.65; color: rgba(255, 255, 255, 0.82); }
@media (max-width: 980px) {
  .grid-3, .steps, .console, .plans { grid-template-columns: 1fr; }
  .stats { grid-template-columns: repeat(2, 1fr); }
  .step::before { right: 0; }
}
@media (max-width: 799px) {
  .menu { height: 64px; padding: 0 16px; }
  nav.scrolled .menu { height: 56px; padding: 0 7px 0 16px; }
  .menu-actions .signin { display: none; }
  .signup { transition: transform 0.35s var(--cubic), opacity 0.25s ease; }
  nav.open .signup { opacity: 0; pointer-events: none; transform: translateX(8px); }
  .layer { width: 90%; height: 90%; top: 5%; left: 5%; min-width: 280px; min-height: 280px; }
  .disc::before { width: 400px; height: 400px; }
  .layer .content { transform: translate(-50%, -50%) scale(0.23); }
  .fig-in { font-size: 104px; }
  .lede { margin-top: 128px; }
  .sec { padding: 78px 0; }
}
@media (max-height: 700px) {
  .layer { width: 60%; height: 60%; top: 20%; left: 20%; min-width: 280px; min-height: 280px; }
  .disc::before { width: 460px; height: 460px; }
  .layer .content { transform: translate(-50%, -50%) scale(0.42); }
  .fig-in { font-size: 120px; }
  .lede { margin-top: 132px; }
}
@media (prefers-reduced-motion: reduce) {
  html { scroll-behavior: auto; }
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
  .piece { animation: none !important; }
}

/* ---------- hero refresh: brighter aperture, vivid pills, glass cards ---------- */
.scene { opacity: 0.92; }
.l-one .piece { filter: none; }
.l-two .piece { filter: blur(10px); }
.l-three .piece { filter: blur(16px); background: linear-gradient(90deg, #ff9468, #ff5fa8); }
.l-one .piece { background: linear-gradient(90deg, #5b5cff, #e25cff); }
.l-two .piece { background: linear-gradient(90deg, #ffc98a, #ff6f91); }
/* the aperture reads as a lit dome: a bright rim up top, falling into shade */
.disc::before {
  background: radial-gradient(circle at 50% 30%, #6a45d6 0%, #5531b8 55%, #4a28a6 100%);
  box-shadow: inset 0 2px 0 rgba(200, 170, 255, 0.35), inset 0 0 0 1px rgba(190, 160, 255, 0.18),
              inset -18px -18px 40px 0 rgba(22, 6, 72, 0.35), inset 18px 18px 40px 0 rgba(150, 120, 255, 0.25),
              0 30px 90px -20px rgba(22, 6, 72, 0.55);
}
.l-one .content::before {
  background: radial-gradient(circle at 50% 35%, #6040cc 0%, #5230b2 70%);
  box-shadow: inset 0 0 0 1px rgba(190, 160, 255, 0.12), inset 0 20px 50px -10px rgba(22, 6, 72, 0.45),
              inset 0 -10px 40px -10px rgba(150, 120, 255, 0.25);
}

.badge {
  display: inline-flex; align-items: center; gap: 10px; height: 38px; padding: 0 20px 0 16px; border-radius: 999px;
  font-size: 15px; font-weight: 500; color: #fff;
  background: rgba(70, 40, 170, 0.45); border: 1px solid rgba(255, 255, 255, 0.22);
  -webkit-backdrop-filter: blur(10px); backdrop-filter: blur(10px);
  box-shadow: 0 0 24px -4px rgba(180, 120, 255, 0.45);
  animation: lift 0.7s 0.2s var(--ease) backwards;
}
.badge i { width: 10px; height: 10px; border-radius: 50%; background: #ffb35c; box-shadow: 0 0 10px 2px rgba(255, 170, 80, 0.7); }
.hero h1 { margin-top: 18px; font-size: clamp(44px, 7.6vw, 96px); font-weight: 900; line-height: 0.96; letter-spacing: -0.06em;
  text-shadow: 0 4px 30px rgba(22, 6, 72, 0.4); }
.hero h1 .line:nth-child(3) > span { animation-delay: 0.59s; }
.hero h1 em { background: linear-gradient(90deg, #ffe08a 0%, #ffb27a 35%, #ff6fa0 72%, #e65cff 100%);
  -webkit-background-clip: text; background-clip: text; padding-right: 0.04em; }
.hero .sub { margin-top: 22px; max-width: 38ch; font-size: 19px; line-height: 1.5; color: rgba(255, 255, 255, 0.88);
  text-shadow: 0 2px 14px rgba(22, 6, 72, 0.4); }
.hero > .chip { margin-top: 12px; padding: 5px 16px; border-radius: 999px; font-size: 17px; font-weight: 500;
  color: var(--cream); background: rgba(26, 8, 80, 0.55); border: 1px solid rgba(255, 255, 255, 0.12);
  animation: lift 0.7s 0.7s var(--ease) backwards; }

/* glass surfaces: the card and the window let the pills show through */
.ask, .win { background: rgba(110, 80, 230, 0.26); border: 1px solid rgba(255, 255, 255, 0.2);
  -webkit-backdrop-filter: blur(16px) saturate(1.3); backdrop-filter: blur(16px) saturate(1.3); }
.ask::before, .win::before, .ask:focus-within::before {
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.18), 0 24px 60px -18px rgba(22, 6, 72, 0.75), 0 0 50px -10px rgba(170, 110, 255, 0.35); }
.ask:focus-within { border-color: rgba(255, 232, 163, 0.45); }
.win { background: rgba(90, 60, 200, 0.4); }
.go { width: 56px; height: 46px; border-radius: 14px; background: linear-gradient(135deg, #ffbf5c, #ff6f7d);
  box-shadow: 0 10px 24px -6px rgba(255, 110, 120, 0.6), inset 0 1px 0 rgba(255, 255, 255, 0.45); }

/* sign up gets the glowing outline from the reference */
.signup { border: 1px solid rgba(255, 255, 255, 0.28); background: rgba(50, 24, 140, 0.55); }
.signup.nm--offset::before { box-shadow: 0 0 22px -2px rgba(170, 110, 255, 0.6); }


/* the pills keep to the edges of the aperture and sway outward, so the
   headline stays clear */
.piece { left: auto; right: auto; animation: sway 13s cubic-bezier(1, 0.06, 0.25, 1) infinite both; }
@keyframes sway { 50% { transform: translateX(calc(var(--dx, 1) * 90px)) scaleX(0.82); } }
.l-one .piece:nth-child(1) { right: 6%; left: auto; top: 12%; width: 260px; height: 56px; --dx: 1; transform-origin: left center; }
.l-one .piece:nth-child(2) { left: 6%; right: auto; top: 44%; width: 300px; height: 82px; --dx: -1; transform-origin: right center; }
.l-one .piece:nth-child(3) { left: 10%; right: auto; top: 80%; width: 170px; height: 38px; --dx: -1; transform-origin: right center; }
.l-one .piece:nth-child(4) { right: 8%; left: auto; top: 66%; width: 220px; height: 48px; --dx: 1; transform-origin: left center; }
.l-two .piece:nth-child(1) { left: 2%; right: auto; top: 22%; width: 280px; height: 70px; --dx: -1; transform-origin: right center; }
.l-two .piece:nth-child(2) { right: 3%; left: auto; top: 16%; width: 340px; height: 88px; --dx: 1; transform-origin: left center; }
.l-two .piece:nth-child(3) { right: 2%; left: auto; top: 86%; width: 300px; height: 40px; --dx: 1; transform-origin: left center; }
.l-two .piece:nth-child(4) { right: 7%; left: auto; top: 52%; width: 250px; height: 56px; --dx: 1; transform-origin: left center; }
.l-three .piece:nth-child(1) { left: 13%; right: auto; top: 32%; width: 180px; height: 36px; --dx: -1; transform-origin: right center; }
.l-three .piece:nth-child(2) { right: 13%; left: auto; top: 40%; width: 230px; height: 60px; --dx: 1; transform-origin: left center; }
.l-three .piece:nth-child(3) { left: 4%; right: auto; top: 68%; width: 210px; height: 40px; --dx: -1; transform-origin: right center; }
.l-three .piece:nth-child(4) { left: 1%; right: auto; top: 12%; width: 220px; height: 44px; --dx: -1; transform-origin: right center; }
/* wide screens show the section links in the pill; the burger stays */
@media (min-width: 900px) {
  .menu-links { display: flex; gap: 4px; }
  .menu { grid-template-columns: 1fr auto 1fr; }
}
@media (max-width: 799px) {
  .scene { opacity: 0.8; }
  .hero h1 { font-size: clamp(40px, 12vw, 60px); }
  .hero .sub { font-size: 17px; }
  .hero > .chip { font-size: 15px; }
  .go { width: 48px; height: 42px; }
}

/* ---------- finale: newsletter card under a dome, then the footer ---------- */
.finale { position: relative; overflow: hidden; padding: 0 0 28px;
  background:
    linear-gradient(rgba(255,255,255,0.035) 1px, transparent 1px) 0 0 / 96px 96px,
    linear-gradient(90deg, rgba(255,255,255,0.035) 1px, transparent 1px) 0 0 / 96px 96px,
    linear-gradient(var(--bg-1), #4a28a8 60%, #3c1d95 100%); }
.f-sky { position: absolute; inset: 0 0 auto; height: 620px; pointer-events: none; }
.f-dome { position: absolute; left: 50%; top: 72px; width: 600px; height: 600px; border-radius: 50%; transform: translateX(-50%);
  background: radial-gradient(circle at 50% 18%, #b48cff 0%, #8a5cf5 22%, #6a3fe0 48%, #4f2bb8 75%);
  box-shadow: inset 0 3px 0 rgba(255, 190, 255, 0.55), inset 0 30px 60px -20px rgba(255, 170, 255, 0.5),
              0 -10px 80px -10px rgba(220, 120, 255, 0.55); }
.f-dome::after { content: ""; position: absolute; inset: 8% 14% auto 34%; height: 45%; border-radius: 50%;
  background: radial-gradient(ellipse at 40% 30%, rgba(255, 255, 255, 0.16), transparent 60%); }
.f-orbit { position: absolute; left: 50%; top: 24px; width: 880px; height: 880px; margin-left: -440px; border-radius: 50%;
  border: 1px solid rgba(255, 150, 235, 0.38);
  -webkit-mask-image: linear-gradient(#000 45%, transparent 66%); mask-image: linear-gradient(#000 45%, transparent 66%);
  animation: orbit 90s linear infinite; }
@keyframes orbit { to { transform: rotate(360deg); } }
.f-orbit i { position: absolute; left: 50%; top: 50%; width: var(--s); height: var(--s); margin: calc(var(--s) / -2) 0 0 calc(var(--s) / -2);
  border-radius: 50%; background: var(--c); box-shadow: 0 0 14px 4px var(--g); transform: rotate(var(--a)) translateY(-440px); }
.f-orbit .o1 { --a: -42deg; --s: 16px; --c: #e2ddff; --g: rgba(200, 190, 255, 0.7); }
.f-orbit .o2 { --a: 18deg; --s: 14px; --c: #ff9070; --g: rgba(255, 140, 110, 0.7); }
.f-orbit .o3 { --a: 46deg; --s: 22px; --c: #ffe0ff; --g: rgba(255, 120, 230, 0.85); }
.f-orbit .o4 { --a: -58deg; --s: 9px; --c: #ff6fe0; --g: rgba(255, 110, 220, 0.8); }
.f-orbit .o5 { --a: -98deg; --s: 9px; --c: #ff7a70; --g: rgba(255, 110, 110, 0.7); }
.f-pills span { position: absolute; border-radius: 80px; animation: sway 12s cubic-bezier(1, 0.06, 0.25, 1) infinite both; }
.f-pills .p-cool { background: linear-gradient(90deg, #5b5cff, #e25cff); }
.f-pills .p-coral { background: linear-gradient(90deg, #ff8a6b, #ff5fa8); }
.f-pills .p-pink { background: linear-gradient(90deg, #ff6f9a, #e55cff); }
.f-pills .p-peach { background: linear-gradient(90deg, #ffbf8a, #ff6f91); }
.f-pills .b0 { filter: blur(1px); } .f-pills .b1 { filter: blur(5px); } .f-pills .b2 { filter: blur(12px); opacity: 0.85; }

.f-wrap { position: relative; z-index: 1; }
.f-card { width: min(800px, 100%); margin: 210px auto 0; padding: 28px 64px 34px; border-radius: 32px; text-align: center;
  display: flex; flex-direction: column; align-items: center;
  background: linear-gradient(180deg, rgba(110, 80, 230, 0.32), rgba(70, 40, 180, 0.38));
  border: 1px solid rgba(255, 255, 255, 0.2);
  -webkit-backdrop-filter: blur(22px) saturate(1.35); backdrop-filter: blur(22px) saturate(1.35);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.22), 0 40px 90px -30px rgba(15, 3, 55, 0.85), 0 0 70px -20px rgba(200, 110, 255, 0.45); }
.f-card .badge { animation: none; height: 36px; font-size: 14.5px; }
.f-card h2 { margin-top: 20px; font-size: clamp(34px, 4.6vw, 52px); font-weight: 900; line-height: 1.02; letter-spacing: -0.05em; text-wrap: balance; }
.f-card h2 em { font-style: normal; padding-right: 0.05em;
  background: linear-gradient(90deg, #ffc56a, #ff7d8f 70%, #ff5fb0); -webkit-background-clip: text; background-clip: text; color: transparent; }
.f-sub { margin-top: 14px; max-width: 40ch; font-size: 18px; line-height: 1.55; color: rgba(255, 255, 255, 0.86); }
.f-form { margin-top: 28px; width: min(660px, 100%); height: 64px; padding: 0 0 0 26px; border-radius: 999px;
  display: flex; align-items: center; gap: 14px;
  background: rgba(30, 10, 100, 0.32); border: 1px solid rgba(255, 255, 255, 0.2);
  box-shadow: inset 0 2px 10px rgba(15, 3, 55, 0.35); transition: border-color 0.3s, box-shadow 0.3s; }
.f-form:focus-within { border-color: rgba(255, 220, 160, 0.55); box-shadow: inset 0 2px 10px rgba(15, 3, 55, 0.35), 0 0 0 4px rgba(255, 180, 120, 0.12); }
.f-field { flex: 1; min-width: 0; display: flex; align-items: center; gap: 14px; color: rgba(255, 255, 255, 0.8); }
.f-field svg { flex: none; width: 24px; height: 24px; }
.f-field input { flex: 1; min-width: 0; height: 100%; background: none; border: 0; outline: 0; font: inherit; font-size: 17px; color: #fff; }
.f-field input::placeholder { color: rgba(255, 255, 255, 0.6); }
.f-form button { flex: none; height: 64px; margin: -1px -1px -1px 0; padding: 0 30px 0 40px; border-radius: 999px;
  display: inline-flex; align-items: center; gap: 18px; font-size: 18px; font-weight: 600; color: #2a0f5e;
  background: linear-gradient(90deg, #ffc35e, #ff8a7a 60%, #ff5fa8);
  box-shadow: 0 12px 30px -8px rgba(255, 100, 150, 0.7), inset 0 1px 0 rgba(255, 255, 255, 0.5);
  transition: transform 0.35s var(--cubic), box-shadow 0.3s; }
.f-form button svg { transition: transform 0.35s var(--cubic); }
.f-form button:hover { box-shadow: 0 16px 36px -8px rgba(255, 100, 150, 0.85), inset 0 1px 0 rgba(255, 255, 255, 0.5); }
.f-form button:hover svg { transform: translateX(4px); }
.f-form button:active { transform: scale(0.97); }
.f-form button:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }
.f-note { min-height: 1.5em; margin-top: 12px; font-size: 14px; color: rgba(255, 255, 255, 0.7); }
.f-note.ok { color: var(--cream); } .f-note.warn { color: #ffb0bd; }

.f-grid { margin-top: 44px; padding-top: 44px; border-top: 1px solid rgba(255, 255, 255, 0.12);
  display: grid; grid-template-columns: 1.35fr repeat(3, 0.85fr) 1.3fr; gap: 0; align-items: start; }
.f-brand { padding-right: 32px; }
.f-logo { display: inline-flex; align-items: center; gap: 16px; font-size: 30px; font-weight: 800; letter-spacing: -0.04em; }
.f-logo:focus-visible { outline: 2px solid var(--cream); outline-offset: 6px; border-radius: 12px; }
.f-mark { width: 58px; height: 58px; border-radius: 50%; display: grid; place-items: center;
  background: radial-gradient(circle at 40% 30%, #6a45e0, #2a0f6e); border: 1px solid rgba(255, 255, 255, 0.18);
  box-shadow: 0 0 26px -2px rgba(150, 100, 255, 0.7); }
.f-brand p { margin-top: 18px; max-width: 26ch; font-size: 18px; line-height: 1.55; color: rgba(255, 255, 255, 0.84); }
.f-social { margin-top: 28px; display: flex; gap: 24px; }
.f-social a { width: 50px; height: 50px; border-radius: 50%; display: grid; place-items: center; color: #fff;
  background: rgba(40, 16, 120, 0.35); border: 1px solid rgba(255, 255, 255, 0.16);
  transition: transform 0.35s var(--cubic), background 0.25s, box-shadow 0.3s; }
.f-social a:hover { transform: translateY(-3px); background: rgba(90, 60, 200, 0.5); box-shadow: 0 0 20px -4px rgba(190, 120, 255, 0.7); }
.f-social a:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; }
.f-col { display: flex; flex-direction: column; align-items: flex-start; gap: 14px; padding: 0 20px 0 56px;
  border-left: 1px solid rgba(255, 255, 255, 0.1); min-height: 230px; }
.f-col h3 { margin-bottom: 4px; font-size: 18px; font-weight: 700; letter-spacing: -0.01em; }
.f-col a { font-size: 17.5px; color: rgba(255, 255, 255, 0.8); transition: color 0.25s, transform 0.3s var(--cubic); }
.f-col a:hover { color: #fff; transform: translateX(3px); }
.f-col a:focus-visible, .f-fine a:focus-visible, .f-docs a:focus-visible { outline: 2px solid var(--cream); outline-offset: 3px; border-radius: 4px; }
.f-docs { margin-left: 24px; padding: 28px 28px 30px; border-radius: 24px;
  background: linear-gradient(180deg, rgba(110, 80, 230, 0.28), rgba(70, 40, 180, 0.3));
  border: 1px solid rgba(255, 255, 255, 0.2); box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.18), 0 0 40px -16px rgba(200, 110, 255, 0.5); }
.f-docs h3 { margin-top: 16px; font-size: 22px; font-weight: 800; letter-spacing: -0.03em; }
.f-docs p { margin-top: 8px; font-size: 17px; line-height: 1.55; color: rgba(255, 255, 255, 0.84); }
.f-docs a { margin-top: 20px; display: inline-flex; align-items: center; gap: 12px; font-size: 18px; font-weight: 600; color: #ffc56a; }
.f-docs a svg { transition: transform 0.35s var(--cubic); }
.f-docs a:hover svg { transform: translateX(4px); }

.f-bar { margin-top: 52px; padding-top: 34px; border-top: 1px solid rgba(255, 255, 255, 0.12);
  display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; gap: 14px 28px;
  font-size: 15px; color: rgba(255, 255, 255, 0.82); }
.f-bar-r { display: flex; align-items: center; flex-wrap: wrap; gap: 14px 32px; }
.f-ok { display: inline-flex; align-items: center; gap: 12px; }
.f-ok i { width: 9px; height: 9px; border-radius: 50%; background: #c6ff4a; box-shadow: 0 0 10px 1px rgba(198, 255, 74, 0.6); }
.f-sep { width: 1px; height: 22px; background: rgba(255, 255, 255, 0.2); }
.f-fine { margin-top: 18px; font-size: 12.5px; line-height: 1.6; color: rgba(255, 255, 255, 0.5); }
.f-fine a { color: rgba(255, 232, 163, 0.85); border-bottom: 1px solid rgba(255, 232, 163, 0.35); }

@media (max-width: 1100px) {
  .f-grid { grid-template-columns: repeat(3, 1fr); row-gap: 40px; }
  .f-brand { grid-column: 1 / -1; }
  .f-col { padding-left: 0; border-left: 0; min-height: 0; }
  .f-docs { grid-column: 1 / -1; margin-left: 0; }
}
@media (max-width: 799px) {
  .f-dome { width: 420px; height: 420px; top: 90px; }
  .f-orbit { width: 600px; height: 600px; margin-left: -300px; top: 50px; }
  .f-orbit i { transform: rotate(var(--a)) translateY(-300px); }
  .f-pills { display: none; }
  .f-card { margin-top: 200px; padding: 26px 20px 26px; border-radius: 26px; }
  .f-sub { font-size: 16.5px; }
  .f-form { height: auto; flex-direction: column; align-items: stretch; gap: 10px; padding: 8px; border-radius: 26px; }
  .f-field { height: 50px; padding: 0 12px; }
  .f-form button { height: 52px; margin: 0; justify-content: center; padding: 0 24px; }
  .f-grid { grid-template-columns: 1fr 1fr; }
  .f-social { gap: 14px; }
  .f-col:last-of-type { grid-column: 1 / -1; }
  .f-sep { display: none; }
}

/* roomier headings: looser tracking and a little extra space between words */
.hero h1 { letter-spacing: -0.025em; word-spacing: 0.08em; line-height: 1.02; }
.f-card h2 { letter-spacing: -0.02em; word-spacing: 0.07em; }
.sec-head h2 { letter-spacing: -0.005em; word-spacing: 0.05em; }
.card h3, .step h3, .f-docs h3 { letter-spacing: 0; word-spacing: 0.04em; }
.f-logo { letter-spacing: -0.015em; }
</style>
<nav data-section="nav" aria-label="Primary">
  <div class="menu">
    <a class="brand" href="#top" aria-label="Mnemo home">
      <svg width="28" height="28" viewBox="0 0 28 28" aria-hidden="true">
        <defs>
          <radialGradient id="mk-well" cx="30%" cy="30%" r="80%">
            <stop offset="0" stop-color="#2a0f6e" /><stop offset="1" stop-color="#8a5fd0" />
          </radialGradient>
          <linearGradient id="mk-pill" x1="0" x2="1">
            <stop offset="0" stop-color="#ffe8a3" /><stop offset="1" stop-color="#ff7a5c" />
          </linearGradient>
        </defs>
        <circle cx="14" cy="14" r="13" fill="url(#mk-well)" />
        <circle cx="14" cy="14" r="8.5" fill="#5531b8" />
        <rect x="2" y="11.25" width="21" height="5.5" rx="2.75" fill="url(#mk-pill)" />
      </svg>
      Mnemo
    </a>
    <div class="menu-links">
      <a href="#window">Product</a>
      <a href="#console">Policy</a>
      <a href="#plans">Pricing</a>
      <a href="#faq">FAQ</a>
    </div>
    <div class="menu-actions">
      <a class="signin" href="#plans">Sign in</a>
      <a class="signup nm nm--offset" href="#plans">Sign up</a>
      <button class="burger" type="button" aria-expanded="false" aria-controls="sheet">
        <i aria-hidden="true"></i><span class="sr">Menu</span>
      </button>
    </div>
  </div>

  <div class="scrim" aria-hidden="true"></div>
  <div class="sheet nm nm--offset" id="sheet" role="dialog" aria-modal="true" aria-label="Menu">
    <div class="sheet-head stagger" style="--s:0"><span>Menu</span><b>win_7f3a9c</b></div>
    <div class="sheet-links">
      <a class="stagger" style="--s:1" href="#window"><span class="n">01</span><span><strong>Product</strong><small>Resident, addressable, evictable</small></span><span class="go-ic" aria-hidden="true"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M9 6l6 6-6 6" /></svg></span></a>
      <a class="stagger" style="--s:2" href="#console"><span class="n">02</span><span><strong>Policy</strong><small>Decide what the window keeps</small></span><span class="go-ic" aria-hidden="true"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M9 6l6 6-6 6" /></svg></span></a>
      <a class="stagger" style="--s:3" href="#plans"><span class="n">03</span><span><strong>Pricing</strong><small>Per window, not per token resent</small></span><span class="go-ic" aria-hidden="true"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M9 6l6 6-6 6" /></svg></span></a>
      <a class="stagger" style="--s:4" href="#faq"><span class="n">04</span><span><strong>FAQ</strong><small>The ones worth asking</small></span><span class="go-ic" aria-hidden="true"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.4" stroke-linecap="round" stroke-linejoin="round"><path d="M9 6l6 6-6 6" /></svg></span></a>
    </div>
    <div class="sheet-cta stagger" style="--s:5">
      <a class="ghost" href="#plans">Sign in</a>
      <a class="solid" href="#plans">Sign up free</a>
    </div>
    <p class="sheet-foot stagger" style="--s:6"><i aria-hidden="true"></i>Team plan free for 60 days</p>
  </div>
</nav>

<header class="stage" id="top" data-section="hero">
  <div class="scene" id="scene" aria-hidden="true">
    <div class="layer disc" data-depth="1.2"></div>
    <div class="layer l-one" data-depth="0.9">
      <div class="content">
        <span class="piece to-r"></span><span class="piece to-l"></span><span class="piece to-l"></span><span class="piece to-l"></span>
      </div>
    </div>
    <div class="layer l-two" data-depth="0.6">
      <div class="content">
        <span class="piece to-l"></span><span class="piece to-r"></span><span class="piece to-r"></span><span class="piece to-r"></span>
      </div>
    </div>
    <div class="layer l-three" data-depth="0.4">
      <div class="content">
        <span class="piece to-l"></span><span class="piece to-r"></span><span class="piece to-l"></span><span class="piece to-l"></span>
      </div>
    </div>
  </div>


  <div class="glow" aria-hidden="true"></div>

  <div class="hero wrap">
    <span class="badge"><i aria-hidden="true"></i>Built for agents</span>
    <h1>
      <span class="line"><span>Give your agent</span></span>
      <span class="line"><span><em>a million tokens</em></span></span>
      <span class="line"><span>it can reach</span></span>
    </h1>
    <p class="sub">Keep the whole run resident and addressable, so the model stops re-reading what it knows.</p>
    <p class="chip">Runs on your metal, too.</p>

    <form class="ask nm nm--offset" id="ask" autocomplete="off">
      <label class="ask-field">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.8" aria-hidden="true">
          <rect x="3" y="4" width="18" height="16" rx="4" /><path d="M7 9h6M7 13h10M7 17h4" stroke-linecap="round" />
        </svg>
        <span class="sr">Request</span>
        <input type="text" placeholder="Name a run — e.g. support-triage-0412" />
      </label>
      <div class="ask-bar">
        <div class="modes nm nm--inset" role="tablist" aria-label="Mode">
          <button class="mode" type="button" role="tab" data-mode="open" aria-selected="true"><i class="ic" aria-hidden="true"></i>Open</button>
          <button class="mode" type="button" role="tab" data-mode="write" aria-selected="false"><i class="ic" aria-hidden="true"></i>Write <span class="new">New</span></button>
          <button class="mode" type="button" role="tab" data-mode="read" aria-selected="false"><i class="ic" aria-hidden="true"></i>Read</button>
          <button class="mode" type="button" role="tab" data-mode="replay" aria-selected="false"><i class="ic" aria-hidden="true"></i>Replay</button>
        </div>
        <button class="go" type="submit" aria-label="Run">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" /></svg>
        </button>
      </div>
    </form>
  </div>

  <div class="preview wrap" aria-hidden="true">
    <div class="win nm nm--offset">
      <div class="win-bar">
        <span class="dots"><i></i><i></i><i></i></span>
        <span class="urlbar nm nm--inset">mnemo://win_7f3a9c</span>
      </div>
      <div class="win-body">
        <div class="win-left">
          <div class="sk-row"><span class="sk lab">Run</span><span class="sk" style="width:110px"></span><span class="sk" style="width:60px;margin-left:auto"></span></div>
          <div class="sk-row"><span class="sk lab">Turns</span><span class="sk" style="width:64px"></span><span class="sk" style="width:64px"></span><span class="sk" style="width:64px"></span></div>
          <div class="sk-card">
            <span class="bar"></span>
            <span class="sk" style="width:92%"></span>
            <span class="sk" style="width:78%"></span>
            <span class="sk" style="width:54%"></span>
          </div>
          <span class="sk" style="width:86%"></span>
          <span class="sk" style="width:70%"></span>
          <span class="sk" style="width:40%;height:24px;margin-top:6px"></span>
        </div>
        <div class="win-code">
          <div class="code-head"><span class="dots"><i></i><i></i><i></i></span><span>[ .JSON ]</span></div>
          <pre class="code" id="code"></pre>
          <span class="status nm nm--offset" id="status"><i></i><span>Ready</span></span>
        </div>
      </div>
    </div>
  </div>

  <div class="trust wrap">
    <p><span>Trusted by <b>5,000+</b> teams running long agents</span></p>
    <span>Halcyon</span><span>Northwind</span><span>Quarry</span><span>Tessellate</span><span>Lumen&amp;Fold</span>
  </div>
</header>

<main class="band">
  <section class="sec" id="window" data-section="features">
    <div class="wrap">
      <div class="sec-head">
        <p class="eyebrow">What sits in the aperture</p>
        <h2>A context window is not a prompt you keep re-sending.</h2>
        <p>Every turn, every tool result and every document stays where the model left it. Mnemo addresses them directly, so a long run costs what a short one does.</p>
      </div>
      <div class="grid-3">
        <article class="card nm nm--offset">
          <div class="dot nm nm--inner" aria-hidden="true"><i></i></div>
          <h3>Resident, not replayed</h3>
          <p>The run is held once and referenced by handle. Turn forty does not pay to re-read turns one through thirty-nine, which is where a long agent loop quietly spends its budget.</p>
          <span class="tag">O(1) per turn</span>
        </article>
        <article class="card nm nm--offset">
          <div class="dot nm nm--inner" aria-hidden="true"><i></i></div>
          <h3>Addressable, not a blob</h3>
          <p>Ask for the third tool call or the paragraph a claim came from and get exactly that back. The window is an index, not one long string you slice by hand.</p>
          <span class="tag">Span-level reads</span>
        </article>
        <article class="card nm nm--offset">
          <div class="dot nm nm--inner" aria-hidden="true"><i></i></div>
          <h3>Evictable on your terms</h3>
          <p>You decide what ages out and what is pinned for the life of the run. Nothing disappears because a buffer filled up while you were not looking.</p>
          <span class="tag">Explicit policy</span>
        </article>
      </div>
    </div>
  </section>

  <section class="sec" style="padding-top: 0" data-section="stats" aria-label="Numbers">
    <div class="wrap">
      <div class="stats">
        <div class="stat nm nm--inset"><b>1M</b><span>tokens addressable per run</span></div>
        <div class="stat nm nm--inset"><b>6 ms</b><span>median span fetch</span></div>
        <div class="stat nm nm--inset"><b>0</b><span>re-reads on turn forty</span></div>
        <div class="stat nm nm--inset"><b>94%</b><span>fewer prompt tokens billed</span></div>
      </div>
      <p class="note">Invented product, invented figures — nothing here was measured.</p>
    </div>
  </section>

  <section class="sec" id="how" data-section="how-it-works" style="padding-top: 0">
    <div class="wrap">
      <div class="sec-head">
        <p class="eyebrow">Three calls</p>
        <h2>Open it, write to it, point the model at it.</h2>
      </div>
      <div class="steps">
        <article class="step">
          <b>01 — Open</b>
          <h3>Start a window</h3>
          <p>One call per run returns a handle. Everything after that is written against it, including the turns your framework would otherwise be concatenating for you.</p>
        </article>
        <article class="step">
          <b>02 — Write</b>
          <h3>Append as you go</h3>
          <p>Turns, tool results and documents go in as spans with whatever metadata you want to query them by later. Writes are append-only, so a replay is exact.</p>
        </article>
        <article class="step">
          <b>03 — Point</b>
          <h3>Hand over the handle</h3>
          <p>The model reads through the window instead of through your prompt. You send the question and the handle, and nothing else travels.</p>
        </article>
      </div>
    </div>
  </section>

  <section class="sec" id="console" data-section="console" style="padding-top: 0">
    <div class="wrap">
      <div class="sec-head">
        <p class="eyebrow">Eviction policy</p>
        <h2>You decide what the window keeps.</h2>
        <p>Nothing ages out on its own schedule. Set the policy once per run and the window holds to it.</p>
      </div>
      <div class="console" data-component="eviction-console">
        <div class="panel nm nm--offset">
          <h3>Retention</h3>
          <p class="hint">Applies to the whole run</p>
          <div class="row">
            <span><b>Pin tool results</b><small>Never evict a tool call or its output</small></span>
            <button class="sw" type="button" id="sw1" aria-pressed="true"><i aria-hidden="true"></i><span class="sr">Pin tool results</span></button>
          </div>
          <div class="row">
            <span><b>Pin cited spans</b><small>Keep anything an answer has pointed at</small></span>
            <button class="sw" type="button" id="sw2" aria-pressed="true"><i aria-hidden="true"></i><span class="sr">Pin cited spans</span></button>
          </div>
          <div class="row">
            <span><b>Summarise on evict</b><small>Leave a stub behind instead of a hole</small></span>
            <button class="sw" type="button" id="sw3" aria-pressed="false"><i aria-hidden="true"></i><span class="sr">Summarise on evict</span></button>
          </div>
          <div class="slider">
            <label class="sr" for="budget">Window budget</label>
            <div class="track" style="--v: 0.62">
              <input id="budget" type="range" min="50" max="1000" step="10" value="620" />
              <span class="fill" aria-hidden="true"></span>
            </div>
            <div class="readout"><span>Window budget</span><b id="budgetOut">620K tokens</b></div>
          </div>
        </div>
        <div class="dial nm nm--offset" id="model">
          <div class="dial-head"><h3>The run</h3><span id="runTotal">24 spans · 1,100K written</span></div>
          <div class="dial-top">
            <div class="ring">
              <svg class="arc" viewBox="0 0 210 210" aria-hidden="true">
                <circle class="bed" cx="105" cy="105" r="91" />
                <circle class="seg pin" cx="105" cy="105" r="91" />
                <circle class="seg keep" cx="105" cy="105" r="91" />
                <circle class="seg stub" cx="105" cy="105" r="91" />
              </svg>
              <div class="ring">
                <div class="ring"><span class="dial-val" id="dialVal">62%</span><span class="dial-sub" id="dialSub">in use</span></div>
              </div>
            </div>
            <ul class="legend">
              <li class="k-pin"><i></i><span>Pinned</span><b id="lgPin">0K</b></li>
              <li class="k-keep"><i></i><span>Kept</span><b id="lgKeep">0K</b></li>
              <li class="k-stub"><i></i><span>Stubs</span><b id="lgStub">0K</b></li>
              <li class="k-gone"><i></i><span>Evicted</span><b id="lgGone">0K</b></li>
            </ul>
          </div>
          <div>
            <div class="strip nm nm--inset" id="strip" aria-hidden="true"></div>
            <div class="strip-axis"><span>Oldest</span><span class="strip-key"><em class="kt">Tool result</em><em class="kc">Cited</em></span><span>Newest</span></div>
          </div>
          <p class="verdict" id="verdict" aria-live="polite"></p>
        </div>
      </div>
    </div>
  </section>

  <section class="sec" id="plans" data-section="pricing" style="padding-top: 0">
    <div class="wrap">
      <div class="sec-head">
        <p class="eyebrow">Plans</p>
        <h2>Priced per window, not per token you resend.</h2>
      </div>
      <div class="plans">
        <article class="plan nm nm--offset">
          <span class="plan-name">Solo</span>
          <div class="price nm nm--inset"><b>$0</b><span>one window at a time</span></div>
          <ul>
            <li>128K addressable per run</li>
            <li>Span reads and pins</li>
            <li>Seven day retention</li>
          </ul>
          <button class="btn btn--ghost" type="button">Start free</button>
        </article>
        <article class="plan nm nm--offset">
          <span class="plan-name">Team</span>
          <div class="price nm nm--inset"><b>$40</b><span>per seat, per month</span></div>
          <ul>
            <li>1M addressable per run</li>
            <li>Policy per run, not per org</li>
            <li>Replay from any append</li>
            <li>Ninety day retention</li>
          </ul>
          <button class="btn btn--solid" type="button">Start free</button>
        </article>
        <article class="plan nm nm--offset">
          <span class="plan-name">Self hosted</span>
          <div class="price nm nm--inset"><b>Talk</b><span>annual, on your metal</span></div>
          <ul>
            <li>Unlimited windows</li>
            <li>Your storage, your keys</li>
            <li>Air-gapped deploys</li>
          </ul>
          <button class="btn btn--ghost" type="button">Contact us</button>
        </article>
      </div>
    </div>
  </section>

  <section class="sec" id="faq" data-section="faq" style="padding-top: 0">
    <div class="wrap">
      <div class="sec-head">
        <p class="eyebrow">Questions</p>
        <h2>The ones worth asking.</h2>
      </div>
      <div class="qa">
        <details class="q nm nm--offset">
          <summary>Is this a vector store?<i aria-hidden="true"></i></summary>
          <p>No. A vector store is for finding things you did not know you had. A window is for holding things you already put there, in order, and reading them back by address. You would sensibly use both.</p>
        </details>
        <details class="q nm nm--offset">
          <summary>What happens when a run exceeds the budget?<i aria-hidden="true"></i></summary>
          <p>The policy you set decides. Pinned spans stay, the oldest unpinned spans go, and with summarise-on-evict a stub is left in their place so the order of the run is still readable.</p>
        </details>
        <details class="q nm nm--offset">
          <summary>Does the model need to know about Mnemo?<i aria-hidden="true"></i></summary>
          <p>Only enough to be handed a window id. Everything else is the runtime's job, so the same window works across whichever model you route to that day.</p>
        </details>
      </div>
    </div>
  </section>

</main>

<footer class="finale" id="start" data-section="footer">
  <div class="f-sky" aria-hidden="true">
    <div class="f-orbit"><i class="o1"></i><i class="o2"></i><i class="o3"></i><i class="o4"></i><i class="o5"></i></div>
    <div class="f-dome"></div>
    <div class="f-pills">
      <span class="p-pink b2" style="--dx:-1; left:9%; top:110px; width:170px; height:40px; animation-delay:0.0s"></span>
      <span class="p-peach b2" style="--dx:-1; left:6%; top:170px; width:260px; height:70px; animation-delay:1.3s"></span>
      <span class="p-cool b0" style="--dx:-1; left:13%; top:335px; width:260px; height:66px; animation-delay:2.6s"></span>
      <span class="p-coral b2" style="--dx:-1; left:10%; top:462px; width:76px; height:48px; animation-delay:3.9s"></span>
      <span class="p-cool b0" style="--dx:1; right:7%; top:86px; width:240px; height:56px; animation-delay:5.2s"></span>
      <span class="p-coral b2" style="--dx:1; right:9%; top:200px; width:240px; height:76px; animation-delay:6.5s"></span>
      <span class="p-cool b1" style="--dx:1; right:12%; top:395px; width:240px; height:64px; animation-delay:7.8s"></span>
      <span class="p-coral b2" style="--dx:1; right:11%; top:475px; width:64px; height:42px; animation-delay:9.1s"></span>
      <span class="p-cool b1 lo" style="--dx:-1; left:-1%; top:850px; width:100px; height:44px; animation-delay:10.4s"></span>
      <span class="p-coral b2 lo" style="--dx:1; right:-2%; top:858px; width:130px; height:50px; animation-delay:11.7s"></span>
    </div>
  </div>

  <div class="wrap f-wrap">
    <section class="f-card" aria-labelledby="f-title">
      <span class="badge"><i aria-hidden="true"></i>Stay in the loop</span>
      <h2 id="f-title">Build <em>faster,</em> together</h2>
      <p class="f-sub">Get new runs, templates, and product updates delivered to your inbox.</p>
      <form class="f-form" id="subscribe" novalidate>
        <label class="f-field">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="5" width="18" height="14" rx="3" /><path d="M4 7l8 6 8-6" /></svg>
          <span class="sr">Email address</span>
          <input id="sub-email" type="email" placeholder="Enter your email" autocomplete="email" required />
        </label>
        <button type="submit">Subscribe <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" /></svg></button>
      </form>
      <p class="f-note" id="sub-note" aria-live="polite"></p>
    </section>

    <div class="f-grid">
      <div class="f-brand">
        <a class="f-logo" href="#top"><span class="f-mark"><svg width="34" height="34" viewBox="0 0 28 28" aria-hidden="true"><defs><radialGradient id="fk-well" cx="30%" cy="30%" r="80%"><stop offset="0" stop-color="#2a0f6e" /><stop offset="1" stop-color="#8a5fd0" /></radialGradient><linearGradient id="fk-pill" x1="0" x2="1"><stop offset="0" stop-color="#ffe8a3" /><stop offset="1" stop-color="#ff7a5c" /></linearGradient></defs><circle cx="14" cy="14" r="13" fill="url(#fk-well)" /><circle cx="14" cy="14" r="8.5" fill="#5531b8" /><rect x="2" y="11.25" width="21" height="5.5" rx="2.75" fill="url(#fk-pill)" /></svg></span>Mnemo</a>
        <p>Give your agent a million tokens it can reach.</p>
        <div class="f-social"><a href="#top" aria-label="Source code"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M8 8l-4 4 4 4M16 8l4 4-4 4M13.5 5l-3 14" /></svg></a><a href="#top" aria-label="Community chat"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M4 6.5A2.5 2.5 0 0 1 6.5 4h11A2.5 2.5 0 0 1 20 6.5v7a2.5 2.5 0 0 1-2.5 2.5H10l-4.5 4v-4h0A1.5 1.5 0 0 1 4 14.5z" /></svg></a><a href="#top" aria-label="Video walkthroughs"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="3" y="5" width="18" height="14" rx="4" /><path d="M10.5 9.5l4 2.5-4 2.5z" fill="currentColor" /></svg></a><a href="#top" aria-label="Changelog feed"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.9" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 5a14 14 0 0 1 14 14M5 11a8 8 0 0 1 8 8" /><circle cx="6" cy="18" r="1.4" fill="currentColor" /></svg></a></div>
      </div>
      <div class="f-col" role="navigation" aria-label="Product">
        <h3>Product</h3>
        <a href="#window">Features</a><a href="#how">Use cases</a><a href="#plans">Pricing</a><a href="#how">Docs</a><a href="#faq">Changelog</a>
      </div>
      <div class="f-col" role="navigation" aria-label="Resources">
        <h3>Resources</h3>
        <a href="#console">Templates</a><a href="#how">Examples</a><a href="#faq">Community</a><a href="#window">Blog</a><a href="#top">Status</a>
      </div>
      <div class="f-col" role="navigation" aria-label="Company">
        <h3>Company</h3>
        <a href="#window">About</a><a href="#top">Careers</a><a href="#plans">Contact</a><a href="#faq">Privacy</a><a href="#faq">Terms</a>
      </div>
      <aside class="f-docs">
        <svg width="28" height="28" viewBox="0 0 24 24" aria-hidden="true"><defs><linearGradient id="spark" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#ffd27a" /><stop offset="1" stop-color="#ff6fa0" /></linearGradient></defs><path d="M10 3l1.6 5.4L17 10l-5.4 1.6L10 17l-1.6-5.4L3 10l5.4-1.6z" fill="url(#spark)" /><path d="M18 2.5l.7 2.3 2.3.7-2.3.7-.7 2.3-.7-2.3-2.3-.7 2.3-.7z" fill="#ff8ab6" /></svg>
        <h3>Built for agents</h3>
        <p>Deterministic, addressable and production ready.</p>
        <a href="#how">View docs <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><path d="M5 12h14M13 6l6 6-6 6" /></svg></a>
      </aside>
    </div>

    <div class="f-bar">
      <span>© 2026 Mnemo. All rights reserved.</span>
      <span class="f-bar-r"><span class="f-ok"><i aria-hidden="true"></i>All systems operational</span><span class="f-sep" aria-hidden="true"></span><span>Made for humans and agents.</span></span>
    </div>
    <p class="f-fine">Mnemo is a fictional product and every figure on this page is invented. Aperture and drifting pills adapted from a pen by <a href="https://www.rafaelalucas.com" target="_blank" rel="noopener">Rafaela Lucas</a>.</p>
  </div>
</footer>

<script>
(() => {
"use strict";
const REDUCED = matchMedia("(prefers-reduced-motion: reduce)").matches;

(() => {
  const scene = document.getElementById("scene");
  if (!scene || REDUCED) return;
  const layers = [...scene.querySelectorAll("[data-depth]")].map((el) => ({
    el, depth: parseFloat(el.dataset.depth) || 0, x: 0, y: 0,
  }));
  if (!layers.length) return;
  const REACH = 42;
  let tx = 0, ty = 0, raf = 0, visible = false;
  scene.parentElement.addEventListener("pointermove", (e) => {
    const r = scene.getBoundingClientRect();
    tx = (e.clientX - r.left) / r.width - 0.5;
    ty = (e.clientY - r.top) / r.height - 0.5;
  });
  scene.parentElement.addEventListener("pointerleave", () => { tx = 0; ty = 0; });
  function frame() {
    raf = requestAnimationFrame(frame);
    let moved = false;
    for (const L of layers) {
      const gx = -tx * REACH * L.depth, gy = -ty * REACH * L.depth;
      L.x += (gx - L.x) * 0.08;
      L.y += (gy - L.y) * 0.08;
      if (Math.abs(gx - L.x) > 0.01 || Math.abs(gy - L.y) > 0.01) moved = true;
      L.el.style.transform = "translate3d(" + L.x.toFixed(2) + "px," + L.y.toFixed(2) + "px,0)";
    }
    if (!moved) { cancelAnimationFrame(raf); raf = 0; }
  }
  const start = () => { if (!raf && visible && !document.hidden) raf = requestAnimationFrame(frame); };
  const stop = () => { if (raf) { cancelAnimationFrame(raf); raf = 0; } };
  scene.parentElement.addEventListener("pointermove", start);
  scene.parentElement.addEventListener("pointerleave", start);
  new IntersectionObserver((es) => {
    for (const e of es) visible = e.isIntersecting;
    visible ? start() : stop();
  }, { threshold: 0 }).observe(scene);
  document.addEventListener("visibilitychange", () => (document.hidden ? stop() : start()));
})();

(() => {
  const range = document.getElementById("budget");
  const track = range && range.closest(".track");
  const out = document.getElementById("budgetOut");
  const model = document.getElementById("model");
  const dial = document.getElementById("dialVal");
  const dialSub = document.getElementById("dialSub");
  const strip = document.getElementById("strip");
  const verdict = document.getElementById("verdict");
  const sw = { tool: document.getElementById("sw1"), cited: document.getElementById("sw2"), stub: document.getElementById("sw3") };
  const switches = Object.values(sw);
  if (!range || !track || !out || !model || !strip) return;

  /* An invented run, oldest first: [kind, size in K tokens, cited?].
     Tool results and documents are heavy, turns are light, and a few spans
     have been pointed at by an answer. */
  const RUN = [
    ["turn", 18], ["doc", 120], ["tool", 32], ["turn", 12], ["tool", 44, 1], ["turn", 20], ["doc", 96], ["tool", 22],
    ["turn", 16], ["tool", 36], ["turn", 14, 1], ["doc", 110], ["tool", 28], ["turn", 22], ["tool", 26, 1], ["turn", 10],
    ["doc", 84], ["tool", 18], ["turn", 18, 1], ["tool", 30], ["turn", 12], ["doc", 40, 1], ["tool", 16], ["turn", 14],
  ].map(([type, size, cited], i) => ({ i, type, size, cited: !!cited }));
  const STUB = 2;            /* a summary stub costs about 2K */
  const TOTAL = RUN.reduce((a, s) => a + s.size, 0);
  const NAME = { turn: "turn", tool: "tool result", doc: "document" };
  const fmt = (k) => k.toLocaleString("en-US") + "K";

  /* build the strip once; three rows of eight, each span as wide as it is heavy */
  const els = RUN.map((s) => {
    const el = document.createElement("span");
    el.className = "span";
    el.style.setProperty("--w", s.size);
    el.dataset.type = s.type;
    if (s.cited) el.dataset.cited = "";
    return el;
  });
  for (let r = 0; r < 3; r++) {
    const row = document.createElement("div");
    row.className = "strip-row";
    els.slice(r * 8, r * 8 + 8).forEach((e) => row.appendChild(e));
    strip.appendChild(row);
  }
  document.getElementById("runTotal").textContent = RUN.length + " spans · " + fmt(TOTAL) + " written";

  const on = (b) => b.getAttribute("aria-pressed") === "true";
  const C = 2 * Math.PI * 91, GAP = 3;
  const segs = { pin: model.querySelector(".seg.pin"), keep: model.querySelector(".seg.keep"), stub: model.querySelector(".seg.stub") };
  function arc(el, from, len) {
    /* lengths are fractions of the ring; a hairline gap separates segments */
    const L = Math.max(0, len * C - (len > 0 ? GAP : 0));
    el.style.strokeDasharray = L.toFixed(2) + " " + C.toFixed(2);
    el.style.strokeDashoffset = (-from * C).toFixed(2);
    el.style.opacity = len > 0 ? 1 : 0;
  }

  let first = true;
  function paint() {
    const budget = +range.value, min = +range.min, max = +range.max;
    track.style.setProperty("--v", ((budget - min) / (max - min)).toFixed(4));
    out.textContent = budget + "K tokens";
    const pinTool = on(sw.tool), pinCited = on(sw.cited), stubs = on(sw.stub);

    /* 1. pins stay, whatever they cost */
    const pinned = (s) => (pinTool && s.type === "tool") || (pinCited && s.cited);
    const state = RUN.map((s) => (pinned(s) ? "pin" : null));
    const pinK = RUN.reduce((a, s) => a + (pinned(s) ? s.size : 0), 0);

    /* 2. walk back from the newest unpinned span, keeping each while it
       fits; the moment one does not, it and everything older goes. With
       summarise on, every evicted span still costs a stub's worth. */
    const loose = RUN.filter((s) => !pinned(s)).reverse();
    let used = pinK, cut = false;
    loose.forEach((s, j) => {
      const olderStubs = stubs ? (loose.length - j - 1) * STUB : 0;
      if (!cut && used + s.size + olderStubs <= budget) { state[s.i] = "keep"; used += s.size; }
      else { cut = true; state[s.i] = stubs ? "stub" : "gone"; }
    });

    const sum = (k) => RUN.reduce((a, s) => a + (state[s.i] === k ? s.size : 0), 0);
    const count = (k) => state.filter((x) => x === k).length;
    const keepK = sum("keep"), goneN = count("stub") + count("gone");
    const goneK = sum("stub") + sum("gone"), stubK = count("stub") * STUB;
    const inUse = pinK + keepK + stubK;
    const over = pinK > budget;
    model.classList.toggle("over", over);

    /* the ring: each slice is its share of the budget; past 100% it closes */
    const scale = Math.max(budget, inUse);
    arc(segs.pin, 0, pinK / scale);
    arc(segs.keep, pinK / scale, keepK / scale);
    arc(segs.stub, (pinK + keepK) / scale, stubK / scale);
    dial.textContent = Math.round((inUse / budget) * 100) + "%";
    dialSub.textContent = over ? "over" : "in use";

    document.getElementById("lgPin").textContent = fmt(pinK);
    document.getElementById("lgKeep").textContent = fmt(keepK);
    document.getElementById("lgStub").textContent = fmt(stubK);
    document.getElementById("lgGone").textContent = fmt(goneK);
    model.querySelector(".k-stub").classList.toggle("dim", !stubs);
    model.querySelector(".k-pin").classList.toggle("dim", !pinK);

    /* the strip: only the spans whose state actually changed get a flash */
    els.forEach((el, i) => {
      const s = RUN[i], st = state[i];
      if (el.dataset.s !== st) {
        if (!first) { el.classList.remove("flash"); void el.offsetWidth; el.classList.add("flash"); }
        el.dataset.s = st;
      }
      el.title = "Span " + (i + 1) + " · " + NAME[s.type] + (s.cited ? ", cited" : "") + " · " + fmt(s.size) + " · " +
        { pin: "pinned", keep: "kept", stub: "evicted, stub left", gone: "evicted" }[st];
    });
    first = false;

    /* the sentence: what the policy just did, in words */
    const pinBits = [];
    if (pinTool) pinBits.push(RUN.filter((s) => s.type === "tool").length + " tool results");
    if (pinCited) pinBits.push(RUN.filter((s) => s.cited && !(pinTool && s.type === "tool")).length + (pinTool ? " more cited spans" : " cited spans"));
    let txt = pinBits.length ? "<b>Pinned " + pinBits.join(" and ") + "</b> (" + fmt(pinK) + "). " : "<b>Nothing is pinned</b>, so age alone decides. ";
    if (over) {
      txt += '<b class="warn">Pins alone need ' + fmt(pinK) + ", over the " + fmt(budget) + " budget.</b> Raise it or unpin something.";
    } else if (!goneN) {
      txt += "Everything fits, with " + fmt(budget - inUse) + " to spare.";
    } else {
      txt += "The " + goneN + " oldest unpinned span" + (goneN > 1 ? "s" : "") + " (" + fmt(goneK) + ") " + (goneN > 1 ? "were" : "was") + " evicted" +
        (stubs ? ", <b>each leaving a stub</b>, so the run still reads in order." : ", <b>leaving holes</b> in the run.");
    }
    verdict.innerHTML = txt;
  }
  range.addEventListener("input", paint);
  for (const b of switches) {
    b.addEventListener("click", () => {
      b.setAttribute("aria-pressed", String(b.getAttribute("aria-pressed") !== "true"));
      paint();
    });
  }
  paint();
})();

(() => {
  const form = document.getElementById("ask");
  const code = document.getElementById("code");
  const status = document.getElementById("status");
  if (!form || !code || !status) return;
  const input = form.querySelector("input");
  const tabs = [...form.querySelectorAll(".mode")];
  const statusText = status.querySelector("span");
  const MODES = {
    open:   { ph: "Name a run — e.g. support-triage-0412",
              out: (v) => ({ window: "win_7f3a9c", run: v || "support-triage-0412", budget: "620K", policy: { pin: ["tool_results", "cited_spans"] } }) },
    write:  { ph: "Paste a turn, a tool result or a document",
              out: (v) => ({ window: "win_7f3a9c", span: "sp_0041", kind: "tool_result", text: (v || "rows: 212, status: ok").slice(0, 34) + (v.length > 34 ? "…" : ""), appended: true }) },
    read:   { ph: "Ask for a span — e.g. the third tool call",
              out: (v) => ({ span: "sp_0003", turn: 3, query: v || "the third tool call", cited_by: ["ans_12"], fetch_ms: 6 }) },
    replay: { ph: "Replay from an append — e.g. sp_0040",
              out: (v) => ({ from: v || "sp_0040", turns: 38, exact: true, tokens_resent: 0 }) },
  };
  let mode = "open", timer = 0;
  const esc = (s) => s.replace(/[&<>]/g, (c) => ({ "&": "&amp;", "<": "&lt;", ">": "&gt;" }[c]));
  const card = document.querySelector(".sk-card");
  let base = REDUCED ? 0 : 1500;   /* first paint waits for the window to land */
  function render(obj) {
    const html = esc(JSON.stringify(obj, null, 2))
      .replace(/("(?:[^"\\]|\\.)*")(\s*:)?|\b(true|false|null)\b|(-?\d+(?:\.\d+)?)/g, (m, str, colon, lit, num) => {
        if (str) return colon ? '<span class="k">' + str + "</span>" + colon : '<span class="s">' + str + "</span>";
        if (lit) return '<span class="b">' + lit + "</span>";
        return '<span class="n">' + num + "</span>";
      });
    code.style.setProperty("--base", base + "ms");
    code.innerHTML = html.split("\n")
      .map((l, i) => '<span class="ln" style="--i:' + (REDUCED ? 0 : i) + '">' + l + "</span>").join("");
    base = 0;
  }
  const setStatus = (busy, text) => { status.classList.toggle("busy", busy); statusText.textContent = text; };
  function select(t) {
    for (const b of tabs) b.setAttribute("aria-selected", String(b === t));
    mode = t.dataset.mode;
    input.placeholder = MODES[mode].ph;
    clearTimeout(timer);
    code.classList.remove("dim");
    if (card) card.classList.remove("hit");
    render(MODES[mode].out(""));
    setStatus(false, "Ready");
  }
  for (const t of tabs) t.addEventListener("click", () => select(t));
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    clearTimeout(timer);
    setStatus(true, "Reading spans…");
    code.classList.add("dim");
    if (card) card.classList.remove("hit");
    timer = setTimeout(() => {
      render(MODES[mode].out(input.value.trim()));
      code.classList.remove("dim");
      if (card) card.classList.add("hit");
      setStatus(false, "Done · 6 ms");
    }, REDUCED ? 0 : 700);
  });
  select(tabs.find((t) => t.getAttribute("aria-selected") === "true") || tabs[0]);
})();

(() => {
  const nav = document.querySelector("nav");
  const burger = document.querySelector(".burger");
  const sheet = document.getElementById("sheet");
  const scrim = document.querySelector(".scrim");
  if (!nav || !burger || !sheet) return;
  const rows = [...sheet.querySelectorAll(".sheet-links a")];
  const focusables = () => [burger, ...sheet.querySelectorAll("a")];

  function setOpen(open, { restoreFocus = true } = {}) {
    nav.classList.toggle("open", open);
    burger.setAttribute("aria-expanded", String(open));
    burger.querySelector(".sr").textContent = open ? "Close menu" : "Menu";
    document.documentElement.style.overflow = open ? "hidden" : "";
    /* move focus into the menu for keyboard and screen-reader users, without
       drawing a ring on a menu that was opened by a tap */
    if (open) setTimeout(() => (rows.find((r) => r.getAttribute("aria-current") === "true") || rows[0])
      .focus({ preventScroll: true, focusVisible: openedByKey }), 120);
    else if (restoreFocus) burger.focus({ preventScroll: true });
  }
  const isOpen = () => nav.classList.contains("open");
  let openedByKey = false;
  burger.addEventListener("pointerdown", () => (openedByKey = false));
  burger.addEventListener("keydown", (e) => { if (e.key === "Enter" || e.key === " ") openedByKey = true; });
  burger.addEventListener("click", () => setOpen(!isOpen()));

  /* the bar frosts over once the page moves under it */
  const frost = () => nav.classList.toggle("scrolled", scrollY > 24);
  addEventListener("scroll", frost, { passive: true });
  frost();
  if (scrim) scrim.addEventListener("click", () => setOpen(false));
  for (const a of sheet.querySelectorAll("a")) a.addEventListener("click", () => setOpen(false, { restoreFocus: false }));
  document.addEventListener("keydown", (e) => {
    if (!isOpen()) return;
    if (e.key === "Escape") { e.preventDefault(); setOpen(false); return; }
    /* keep Tab inside the menu while it is open */
    if (e.key === "Tab") {
      const f = focusables(), i = f.indexOf(document.activeElement);
      if (e.shiftKey && i <= 0) { e.preventDefault(); f[f.length - 1].focus(); }
      else if (!e.shiftKey && i === f.length - 1) { e.preventDefault(); f[0].focus(); }
    }
  });

  /* mark the section currently on screen, so the menu opens on where you are */
  const targets = rows.map((r) => document.querySelector(r.getAttribute("href"))).filter(Boolean);
  let ticking = false;
  function spy() {
    ticking = false;
    const mid = innerHeight * 0.4;
    let current = null;
    for (const t of targets) { const r = t.getBoundingClientRect(); if (r.top <= mid && r.bottom > mid) current = t; }
    for (const r of rows) r.setAttribute("aria-current", String(!!current && r.getAttribute("href") === "#" + current.id));
  }
  addEventListener("scroll", () => { if (!ticking) { ticking = true; requestAnimationFrame(spy); } }, { passive: true });
  spy();
})();
(() => {
  const form = document.getElementById("subscribe");
  const note = document.getElementById("sub-note");
  if (!form || !note) return;
  const input = form.querySelector("input");
  form.addEventListener("submit", (e) => {
    e.preventDefault();
    const v = input.value.trim();
    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(v)) {
      note.textContent = "Enter an email address like you@company.com.";
      note.className = "f-note warn"; input.focus(); return;
    }
    note.textContent = "This is a demo page, so nothing was sent or stored.";
    note.className = "f-note ok";
  });
})();
})();
</script>

</body></html>
```

