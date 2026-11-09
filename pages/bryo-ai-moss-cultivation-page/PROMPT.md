INSTALANDING.AI · Bryo AI Moss Cultivation Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Bryo AI Moss Cultivation Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/bryo-ai-moss-cultivation-page

bryo-ai-moss-cultivation.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Bryo AI Moss Cultivation Page
  slug     bryo-ai-moss-cultivation-page
  prompt   https://instalanding.ai/p/bryo-ai-moss-cultivation-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/bryo-ai-moss-cultivation-page
  license  Fictional company ("Bryo", "Bryo Labs") and product (Bryo Pod, Bryo Cloud); every figure, price, species
           count and quote is invented and the email placeholder uses example.com. Replace before shipping.

  MAP
  tokens    :root: --ink #10291a, --ink2, --mist #e7ebe8, --paper #f6f7f4, lime --lime #c6f35c / --lime2 #a9dd3a,
            --glass, --line; Inter Tight (--sans) and JetBrains Mono (--mono) from Google Fonts
  sections  nav, hero (#story: a 640vh sticky scroll story), use-cases (#sol), how-it-works (#how), product (#pod),
            pricing, faq, cta (#start), footer (each carries data-section)
  scripts   two at the end of <body>. The first paints every picture in code: a layered valley (sky, far / mid / near
            ridges with conifers and a lit flux tower, mist bands, distant floating islands), a moss-capped floating
            island and floating rocks lit per pixel (islandShader), and a bipinnate fern; renderScene() dollies a
            virtual camera through those depth layers as you scroll, and the frame() loop drives the five story
            layers (hero, vision headline, fog + word-by-word account with hotspots, field card with a coverage
            sparkline and a feature list), the rocks, pointer parallax, the use-case card art and the counting stats.
            The second does scroll reveals (.rv) and the live moss-growth simulation in #grow.
  assets    no image files, no libraries; the hero plate, fern cut-out, rocks and card art are canvases turned into
            data URLs at load

  ADAPTING
  - Story timing lives in frame(): every element maps scroll progress through seg(sp, a, b); keep the windows in
    order or layers overlap. #story's 640vh height sets how long the story lasts.
  - The scene geometry is a 1600x900 frame (FW / FH, vanishing point VPX / VPY); the hero h1 is placed above the
    fern by layoutHero(), so move them together.
  - Building the scene costs a second or two of main-thread time at load (per-pixel shading); lower R in buildFern
    / buildIsland to make it cheaper.
  - prefers-reduced-motion stops the mist, fog, bobbing rocks, pings and pointer parallax, shows the headline and
    reveals at once, counts the stats instantly and draws the growth simulation as one still frame; the scroll
    story still follows the scrollbar.
-->
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <title>Bryo — The AI That Grows Moss</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500;600&family=JetBrains+Mono:wght@400;500&display=swap"
      rel="stylesheet"
    />
    <style>
      :root {
        --ink: #10291a;
        --ink2: #2c4434;
        --mist: #e7ebe8;
        --paper: #f6f7f4;
        --lime: #c6f35c;
        --lime2: #a9dd3a;
        --glass: rgba(244, 247, 243, 0.16);
        --line: rgba(255, 255, 255, 0.28);
        --sans: "Inter Tight", "Helvetica Neue", Arial, sans-serif;
        --mono: "JetBrains Mono", ui-monospace, Menlo, monospace;
      }
      * { box-sizing: border-box; margin: 0; padding: 0; }
      html, body { background: var(--mist); }
      body {
        font-family: var(--sans);
        color: var(--ink);
        -webkit-font-smoothing: antialiased;
        overflow-x: hidden;
      }
      a { color: inherit; text-decoration: none; }
      .mono {
        font-family: var(--mono);
        text-transform: uppercase;
        letter-spacing: 0.14em;
        font-size: 11px;
      }
      .chip {
        display: inline-flex;
        align-items: center;
        justify-content: center;
        height: 22px;
        padding: 0 9px;
        background: var(--lime);
        color: var(--ink);
        border-radius: 3px;
        font: 500 10.5px var(--mono);
        letter-spacing: 0.16em;
        text-transform: uppercase;
        white-space: nowrap;
      }
      nav {
        position: fixed;
        z-index: 50;
        top: 0;
        left: 0;
        width: 100%;
        display: grid;
        grid-template-columns: 1fr auto 1fr;
        align-items: center;
        padding: 22px 34px;
        color: var(--ink);
      }
      .brand {
        display: flex;
        align-items: center;
        gap: 9px;
        font-size: 21px;
        font-weight: 600;
        letter-spacing: -0.02em;
      }
      .brand svg { width: 32px; height: 32px; }
      .menu { display: flex; align-items: center; gap: 30px; }
      .menu a {
        display: flex;
        align-items: center;
        gap: 7px;
        font: 400 11.5px var(--mono);
        letter-spacing: 0.14em;
        text-transform: uppercase;
        transition: color 0.25s;
      }
      .menu a:hover { color: var(--lime2); }
      .chev {
        width: 6px;
        height: 6px;
        border-right: 1.3px solid currentColor;
        border-bottom: 1.3px solid currentColor;
        transform: translateY(-2px) rotate(45deg);
      }
      .talk {
        justify-self: end;
        display: flex;
        align-items: center;
        gap: 12px;
        font: 400 11.5px var(--mono);
        letter-spacing: 0.16em;
      }
      .talk i {
        width: 20px;
        height: 20px;
        border-radius: 3px;
        background: var(--lime);
        display: grid;
        place-items: center;
        font: 500 18px var(--sans);
        font-style: normal;
        transition: transform 0.3s;
      }
      .talk:hover i { transform: translateX(3px); }
      #story { position: relative; height: 640vh; }
      .stage {
        position: sticky;
        top: 0;
        height: 100vh;
        overflow: hidden;
        background: #dfe3e0;
        isolation: isolate;
      }
      .cam {
        position: absolute;
        inset: -9% -3% -3%;
        will-change: transform;
      }
      .cam canvas,
      .cam .plate,
      .camF img {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
      }
      .cam canvas { z-index: 0; }
      .plate { z-index: 1; }
      .mist {
        position: absolute;
        z-index: 2;
        inset: -10%;
        pointer-events: none;
        background:
          radial-gradient(40% 30% at 20% 80%, rgba(255, 255, 255, 0.55), transparent 70%),
          radial-gradient(35% 25% at 85% 30%, rgba(255, 255, 255, 0.4), transparent 70%);
        animation: drift 18s ease-in-out infinite alternate;
      }
      @keyframes drift { to { transform: translate3d(4%, -2%, 0); } }
      .fog {
        position: absolute;
        z-index: 4;
        left: -8vw;
        top: -6vh;
        width: 56vw;
        height: 60vh;
        visibility: hidden;
        opacity: 0;
        pointer-events: none;
        -webkit-mask: radial-gradient(ellipse 52% 48% at 46% 46%, #000 44%, rgba(0, 0, 0, 0.7) 64%, transparent 100%);
        mask: radial-gradient(ellipse 52% 48% at 46% 46%, #000 44%, rgba(0, 0, 0, 0.7) 64%, transparent 100%);
      }
      .fog > div { position: absolute; inset: 0; }
      .f0 {
        background: radial-gradient(60% 55% at 40% 45%, #d9dddd, #cfd4d4 60%, #c9cfcf);
        filter: blur(10px);
      }
      .f1,
      .f2 {
        inset: -20% !important;
        opacity: 0.55;
        filter: blur(14px);
        background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 700 460' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.006 .014' numOctaves='3' seed='4'/%3E%3CfeColorMatrix values='0 0 0 0 .84 0 0 0 0 .86 0 0 0 0 .86 0 0 0 1.4 -.7'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
        animation: fogA 26s ease-in-out infinite alternate;
      }
      .f2 {
        opacity: 0.9;
        filter: blur(8px);
        background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 700 460' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.004 .009' numOctaves='4' seed='11'/%3E%3CfeColorMatrix values='0 0 0 0 .9 0 0 0 0 .92 0 0 0 0 .92 0 0 0 1.6 -.55'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
        animation: fogB 19s ease-in-out infinite alternate;
      }
      @keyframes fogA { to { transform: translate3d(6%, 3%, 0) scale(1.08); } }
      @keyframes fogB { to { transform: translate3d(-7%, -2%, 0) scale(1.12); } }
      .layer { position: absolute; inset: 0; pointer-events: none; }
      .layer > * { pointer-events: auto; }
      #L2, #L3, #L4 { z-index: 8; }
      .hero-copy {
        position: absolute;
        left: 0;
        right: 0;
        top: 12.5vh;
        text-align: center;
        z-index: 5;
      }
      .hero-copy h1 {
        font-size: clamp(44px, 6vw, 96px);
        font-weight: 500;
        line-height: 0.92;
        letter-spacing: -0.045em;
        margin-top: 18px;
        color: var(--ink);
      }
      .hero-copy .line {
        display: block;
        overflow: hidden;
        padding-bottom: 0.06em;
        white-space: nowrap;
      }
      .hero-copy .line span {
        display: inline-block;
        transform: translateY(105%);
        animation: rise 1.1s cubic-bezier(0.2, 0.8, 0.2, 1) 0.15s forwards;
      }
      @keyframes rise { to { transform: translateY(0); } }
      .camF { z-index: 6; visibility: hidden; pointer-events: none; }
      .camF img {
        -webkit-mask-image: linear-gradient(90deg, transparent 25%, #000 27.5%, #000 71.5%, transparent 74%);
        mask-image: linear-gradient(90deg, transparent 25%, #000 27.5%, #000 71.5%, transparent 74%);
      }
      .hud { position: absolute; left: 53.5%; top: 62%; color: white; }
      .hud .cross { position: absolute; left: -44px; top: 4px; width: 22px; height: 22px; }
      .cross:before,
      .cross:after { content: ""; position: absolute; background: white; }
      .cross:before { width: 22px; height: 1px; top: 10px; }
      .cross:after { height: 22px; width: 1px; left: 10px; }
      .hud pre {
        font: 400 11px/1.65 var(--mono);
        letter-spacing: 0.12em;
        text-shadow: 0 1px 6px rgba(0, 0, 0, 0.35);
        margin-top: 12px;
      }
      .hud:after {
        content: "";
        position: absolute;
        left: -8px;
        top: -8px;
        right: -14px;
        bottom: -10px;
        border: 1px solid rgba(255, 255, 255, 0.55);
        clip-path: polygon(0 0, 14px 0, 14px 1px, 1px 1px, 1px 14px, 0 14px, 0 0, 100% 0, 100% 14px, calc(100% - 1px) 14px, calc(100% - 1px) 1px, calc(100% - 14px) 1px, calc(100% - 14px) 0, 100% 0, 100% 100%, calc(100% - 14px) 100%, calc(100% - 14px) calc(100% - 1px), calc(100% - 1px) calc(100% - 1px), calc(100% - 1px) calc(100% - 14px), 100% calc(100% - 14px), 100% 100%, 0 100%, 0 calc(100% - 14px), 1px calc(100% - 14px), 1px calc(100% - 1px), 14px calc(100% - 1px), 14px 100%, 0 100%);
      }
      .caption {
        position: absolute;
        left: 34px;
        bottom: 34px;
        padding-left: 16px;
        border-left: 2px solid var(--lime);
        font: 400 11.5px/1.75 var(--mono);
        letter-spacing: 0.13em;
        text-transform: uppercase;
        color: var(--ink2);
      }
      .hint {
        position: absolute;
        right: 34px;
        bottom: 36px;
        display: flex;
        align-items: center;
        gap: 12px;
        font: 400 11px var(--mono);
        letter-spacing: 0.16em;
        color: var(--ink2);
      }
      .vision {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: min(820px, 90vw);
        text-align: center;
        color: white;
      }
      .vision h2 {
        font-size: clamp(34px, 4.6vw, 70px);
        font-weight: 500;
        line-height: 1;
        letter-spacing: -0.04em;
        margin: 18px 0 20px;
        text-shadow: 0 2px 40px rgba(10, 30, 15, 0.55), 0 1px 3px rgba(10, 30, 15, 0.3);
      }
      .vision h2 span { display: inline-block; }
      .vision p {
        font-size: 16px;
        line-height: 1.45;
        text-shadow: 0 1px 14px rgba(10, 30, 15, 0.7);
      }
      .acct {
        position: absolute;
        left: 34px;
        top: 14vh;
        width: min(560px, 86vw);
        font-size: clamp(20px, 1.9vw, 29px);
        line-height: 1.16;
        letter-spacing: -0.02em;
        color: var(--ink);
        text-shadow: 0 0 24px rgba(255, 255, 255, 0.8);
      }
      .acct span { display: inline-block; }
      .hotspot {
        position: absolute;
        display: flex;
        align-items: flex-start;
        gap: 9px;
        cursor: pointer;
        transform-origin: left center;
      }
      .dot {
        width: 22px;
        height: 22px;
        flex: 0 0 22px;
        border-radius: 50%;
        background: var(--lime);
        display: grid;
        place-items: center;
        position: relative;
        transition: transform 0.25s;
      }
      .dot:before,
      .dot:after {
        content: "";
        position: absolute;
        background: var(--ink);
        width: 10px;
        height: 1.4px;
      }
      .dot:after { transform: rotate(90deg); }
      .dot:active { transform: scale(1.15); }
      .dot:before { animation: ping 2.4s infinite; }
      @keyframes ping {
        0% { box-shadow: 0 0 0 0 rgba(198, 243, 92, 0.7); }
        70% { box-shadow: 0 0 0 14px rgba(198, 243, 92, 0); }
        100% { box-shadow: 0 0 0 0 rgba(198, 243, 92, 0); }
      }
      .hot-label {
        background: rgba(246, 248, 245, 0.72);
        backdrop-filter: blur(8px);
        padding: 6px 9px;
        border-radius: 4px;
        font: 400 10.5px var(--mono);
        letter-spacing: 0.14em;
        text-transform: uppercase;
        white-space: nowrap;
      }
      .hotspot em {
        display: block;
        max-height: 0;
        overflow: hidden;
        color: #4f8a12;
        font: 500 12px var(--mono);
        font-style: normal;
        transition: max-height 0.45s;
        font-size: 12px;
      }
      .hotspot.on em,
      .hotspot:hover em { max-height: 20px; }
      .rock { position: absolute; overflow: hidden; z-index: 7; pointer-events: none; }
      .bob { position: absolute; inset: 0; animation: bob 7s ease-in-out infinite alternate; }
      .bob img { position: absolute; max-width: none; width: 100%; height: auto; }
      .rk1 { left: 4%; top: 13%; width: 7.5vw; aspect-ratio: 260/295; }
      .rk1 .bob { animation-duration: 6s; }
      .rk1 img,
      .rk3 img { width: 100%; height: 100%; left: 0; top: 0; }
      .rk3 { left: 80%; top: 58%; width: 14vw; aspect-ratio: 265/270; }
      .rk3 .bob { animation-duration: 8.5s; animation-delay: -3s; }
      @keyframes bob {
        from { transform: translateY(-1.2%) rotate(-1.2deg); }
        to { transform: translateY(1.6%) rotate(1.4deg); }
      }
      .cred {
        position: absolute;
        left: 34px;
        top: 13vh;
        max-width: 380px;
        font-size: clamp(22px, 2vw, 30px);
        line-height: 1.08;
        letter-spacing: -0.025em;
        text-shadow: 0 0 24px rgba(255, 255, 255, 0.8);
      }
      .fieldtag {
        display: flex;
        width: max-content;
        background: var(--lime);
        padding: 4px 8px;
        border-radius: 3px;
        font: 500 10.5px var(--mono);
        margin-bottom: 12px;
        text-shadow: none;
      }
      .carbon {
        position: absolute;
        left: 38%;
        top: 38vh;
        width: 250px;
        padding: 18px;
        border-radius: 10px;
        background: rgba(40, 58, 44, 0.32);
        border: 1px solid rgba(255, 255, 255, 0.22);
        backdrop-filter: blur(16px) saturate(1.2);
        color: white;
      }
      .carbon h4 { font-size: 15px; font-weight: 500; line-height: 1.12; }
      .carbon .note { font: 400 9.5px var(--mono); opacity: 0.7; margin-top: 8px; }
      .carbon .num { font-size: 46px; font-weight: 500; letter-spacing: -0.04em; margin-top: 10px; }
      .carbon .unit { font: 400 10px var(--mono); }
      .gain {
        position: absolute;
        right: 16px;
        top: 96px;
        background: var(--lime);
        color: var(--ink);
        padding: 5px 7px;
        border-radius: 3px;
        font: 500 9px var(--mono);
      }
      .spark { width: 220px; height: 70px; margin-top: 5px; overflow: visible; }
      .spark polyline {
        fill: none;
        stroke: var(--lime);
        stroke-width: 1.6;
        stroke-linecap: round;
        stroke-linejoin: round;
      }
      .spark circle { fill: white; }
      .spark .last { fill: var(--lime); }
      .carbon footer { font: 400 9px var(--mono); letter-spacing: 0.1em; opacity: 0.75; }
      .feats {
        position: absolute;
        right: 34px;
        top: 30vh;
        width: min(400px, 36vw);
        padding: 6px 16px;
        border-radius: 10px;
        background: rgba(246, 248, 245, 0.62);
        backdrop-filter: blur(14px);
      }
      .feat {
        display: grid;
        grid-template-columns: 30px 1fr 16px;
        gap: 8px;
        align-items: center;
        padding: 11px 0;
        border-bottom: 1px solid rgba(16, 41, 26, 0.14);
        font: 400 11px var(--mono);
        letter-spacing: 0.12em;
        text-transform: uppercase;
        transition: color 0.3s, padding 0.3s;
      }
      .feat:last-child { border: 0; }
      .feat .idx { opacity: 0.6; }
      .feat .arrow { transition: transform 0.3s; }
      .feat:hover,
      .feat.on { color: #4f8a12; padding-left: 6px; }
      .feat:hover .arrow,
      .feat.on .arrow { transform: translateX(4px); }
      .prog {
        position: absolute;
        z-index: 20;
        bottom: 22px;
        left: 50%;
        transform: translateX(-50%);
        width: 120px;
        height: 2px;
        background: rgba(16, 41, 26, 0.18);
        border-radius: 2px;
      }
      .prog i {
        display: block;
        height: 100%;
        width: 100%;
        background: var(--lime2);
        transform: scaleX(0);
        transform-origin: left;
      }
      #sol {
        position: relative;
        z-index: 5;
        margin-top: -30vh;
        background: #fff;
        border-radius: 22px 22px 0 0;
        padding: 70px 34px 90px;
        box-shadow: 0 -30px 60px rgba(16, 41, 26, 0.12);
      }
      .sol-head {
        display: flex;
        justify-content: space-between;
        align-items: flex-end;
        gap: 40px;
        flex-wrap: wrap;
      }
      .sol-head h2 {
        font-size: clamp(34px, 3.9vw, 58px);
        font-weight: 500;
        line-height: 1;
        letter-spacing: -0.04em;
        max-width: 640px;
        margin-top: 20px;
      }
      .sol-head p { font-size: 15px; line-height: 1.5; color: #4a5a4f; max-width: 360px; }
      .cards { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; margin-top: 54px; }
      .sol-card {
        height: 440px;
        border-radius: 12px;
        overflow: hidden;
        position: relative;
        background: #1b3122;
        color: white;
        transform-style: preserve-3d;
        transition: transform 0.2s;
      }
      .card-bg {
        position: absolute;
        inset: 0;
        background-size: cover;
        transition: transform 1.2s cubic-bezier(0.2, 0.8, 0.2, 1);
      }
      .sol-card:hover .card-bg { transform: scale(1.07); }
      .sol-card:after {
        content: "";
        position: absolute;
        inset: 0;
        background: linear-gradient(180deg, rgba(10, 25, 15, 0.45), transparent 35%, transparent 55%, rgba(10, 25, 15, 0.75));
        pointer-events: none;
      }
      .card-top {
        position: absolute;
        z-index: 1;
        top: 18px;
        left: 18px;
        right: 18px;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
      .bracket { font: 400 10px var(--mono); letter-spacing: 0.12em; }
      .circle {
        width: 28px;
        height: 28px;
        border-radius: 50%;
        background: var(--lime);
        color: var(--ink);
        display: grid;
        place-items: center;
        font-size: 19px;
        transition: transform 0.3s;
      }
      .sol-card:hover .circle { transform: rotate(-45deg); }
      .card-copy { position: absolute; z-index: 1; left: 22px; right: 22px; bottom: 22px; }
      .card-copy h3 { font-size: 25px; font-weight: 500; letter-spacing: -0.03em; line-height: 1.05; }
      .card-copy p {
        font-size: 13.5px;
        line-height: 1.45;
        max-height: 0;
        overflow: hidden;
        opacity: 0;
        transition: max-height 0.6s, opacity 0.4s;
        margin-top: 8px;
      }
      .sol-card:hover .card-copy p { max-height: 80px; opacity: 1; }
      .stats { display: grid; grid-template-columns: repeat(4, 1fr); margin-top: 60px; }
      .stat { border-top: 1px solid #e0e5e0; padding: 22px 0 0; }
      .stat strong { display: block; font-size: 44px; font-weight: 500; letter-spacing: -0.04em; }
      .stat span {
        font: 400 10.5px var(--mono);
        letter-spacing: 0.14em;
        text-transform: uppercase;
        color: #6a7a6f;
      }
      .sec { position: relative; z-index: 5; background: #fff; padding: 110px 34px; }
      .sec-head h2,
      .pod-copy h2,
      .cta h2 {
        font-size: clamp(34px, 3.9vw, 58px);
        font-weight: 500;
        line-height: 1;
        letter-spacing: -0.04em;
        max-width: 720px;
        margin-top: 20px;
      }
      .rv { opacity: 0; transform: translateY(28px); transition: opacity 0.9s, transform 0.9s cubic-bezier(0.2, 0.8, 0.2, 1); }
      .rv.in { opacity: 1; transform: none; }
      #how { background: var(--paper); border-top: 1px solid #e0e5e0; }
      .steps { list-style: none; display: grid; grid-template-columns: repeat(4, 1fr); gap: 14px; margin-top: 54px; }
      .step { background: #fff; border: 1px solid #e0e5e0; border-radius: 12px; padding: 24px 22px 28px; min-height: 280px; display: flex; flex-direction: column; }
      .step:nth-child(2) { transition-delay: 0.08s; }
      .step:nth-child(3) { transition-delay: 0.16s; }
      .step:nth-child(4) { transition-delay: 0.24s; }
      .step-n { font: 400 10.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: #6a7a6f; }
      .step svg { width: 48px; height: 48px; margin: 34px 0 auto; fill: none; stroke: var(--ink); stroke-width: 1.6; stroke-linecap: round; stroke-linejoin: round; }
      .step svg circle:nth-of-type(odd) { fill: var(--lime); }
      .step h3 { font-size: 22px; font-weight: 500; letter-spacing: -0.03em; margin-top: 30px; }
      .step p { font-size: 14px; line-height: 1.5; color: #4a5a4f; margin-top: 8px; }
      .pod { display: grid; grid-template-columns: 1fr 1.1fr; gap: 60px; align-items: center; }
      .pod-copy p { font-size: 15px; line-height: 1.55; color: #4a5a4f; max-width: 460px; margin-top: 22px; }
      .spec { list-style: none; margin-top: 34px; max-width: 460px; }
      .spec li { display: flex; justify-content: space-between; gap: 20px; padding: 13px 0; border-top: 1px solid #e0e5e0; font-size: 14px; }
      .spec li span { font: 400 10.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; color: #6a7a6f; padding-top: 3px; }
      .spec li strong { font-weight: 500; text-align: right; }
      .pod-viz { background: var(--ink); border-radius: 14px; padding: 14px; color: #fff; box-shadow: 0 40px 80px rgba(16, 41, 26, 0.22); }
      .viz-top,
      .viz-bot { display: flex; justify-content: space-between; font: 400 10.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; }
      .viz-top { padding: 4px 4px 12px; color: rgba(255, 255, 255, 0.7); }
      #vDay { color: var(--lime); }
      #grow { display: block; width: 100%; height: auto; aspect-ratio: 1040/760; border-radius: 8px; background: #555a52; }
      .viz-bot { padding: 14px 4px 4px; }
      .viz-bot div { display: flex; flex-direction: column; gap: 6px; color: rgba(255, 255, 255, 0.6); }
      .viz-bot strong { font: 500 24px var(--sans); letter-spacing: -0.03em; color: #fff; text-transform: none; }
      #pricing { border-top: 1px solid #e0e5e0; }
      .plans { display: grid; grid-template-columns: repeat(3, 1fr); gap: 14px; margin-top: 54px; }
      .plan { border: 1px solid #e0e5e0; border-radius: 12px; padding: 26px; display: flex; flex-direction: column; }
      .plan:nth-child(2) { transition-delay: 0.08s; }
      .plan:nth-child(3) { transition-delay: 0.16s; }
      .plan.featured { background: var(--ink); color: #fff; border-color: var(--ink); }
      .plan-n { display: flex; justify-content: space-between; align-items: center; font: 400 11px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; }
      .plan-n em { font-style: normal; background: var(--lime); color: var(--ink); padding: 4px 7px; border-radius: 3px; font-size: 9.5px; }
      .price { font-size: 52px; font-weight: 500; letter-spacing: -0.045em; margin-top: 30px; }
      .price small { font: 400 10.5px var(--mono); letter-spacing: 0.12em; text-transform: uppercase; margin-left: 8px; opacity: 0.6; }
      .plan > p { font-size: 14px; line-height: 1.5; opacity: 0.75; margin-top: 8px; }
      .plan ul { list-style: none; margin: 26px 0 30px; flex: 1; }
      .plan li { padding: 10px 0 10px 22px; border-top: 1px solid rgba(127, 140, 130, 0.25); font-size: 14px; position: relative; }
      .plan li:before { content: ""; position: absolute; left: 2px; top: 15px; width: 8px; height: 8px; border-radius: 50%; background: var(--lime2); }
      .btn {
        display: inline-flex; align-items: center; justify-content: center; gap: 10px; height: 46px; padding: 0 20px; border: 0; border-radius: 6px;
        background: var(--lime); color: var(--ink); font: 500 11.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; cursor: pointer;
        transition: transform 0.25s, background 0.25s;
      }
      .btn:hover { transform: translateY(-2px); background: #d4fa73; }
      .btn i { font: 500 18px var(--sans); font-style: normal; }
      .btn.ghost { background: transparent; border: 1px solid var(--ink); }
      .btn.ghost:hover { background: var(--ink); color: #fff; }
      .faq { background: var(--paper); border-top: 1px solid #e0e5e0; display: grid; grid-template-columns: 1fr 1.3fr; gap: 60px; }
      .qs details { border-top: 1px solid #d6ddd7; }
      .qs details:last-child { border-bottom: 1px solid #d6ddd7; }
      .qs summary { list-style: none; cursor: pointer; display: flex; justify-content: space-between; gap: 20px; padding: 20px 0; font-size: 19px; font-weight: 500; letter-spacing: -0.02em; }
      .qs summary::-webkit-details-marker { display: none; }
      .qs summary:after { content: "+"; flex: 0 0 26px; height: 26px; border-radius: 50%; background: var(--lime); display: grid; place-items: center; font-size: 18px; transition: transform 0.3s; }
      .qs details[open] summary:after { transform: rotate(45deg); }
      .qs p { font-size: 15px; line-height: 1.55; color: #4a5a4f; padding: 0 50px 22px 0; }
      .cta { position: relative; z-index: 5; overflow: hidden; background: var(--ink); color: #fff; padding: 130px 34px 150px; }
      .cta-in { position: relative; z-index: 1; max-width: 760px; }
      .cta-form { display: flex; flex-wrap: wrap; gap: 10px; margin-top: 40px; max-width: 560px; }
      .cta-form input { flex: 1 1 240px; height: 46px; padding: 0 16px; border-radius: 6px; border: 1px solid rgba(255, 255, 255, 0.25); background: rgba(255, 255, 255, 0.06); color: #fff; font: 400 15px var(--sans); outline: none; }
      .cta-form input:focus { border-color: var(--lime); }
      .cta-form input::placeholder { color: rgba(255, 255, 255, 0.45); }
      .thanks { display: none; flex-basis: 100%; font: 400 11px var(--mono); letter-spacing: 0.12em; text-transform: uppercase; color: var(--lime); padding-top: 6px; }
      .cta-form.sent input,
      .cta-form.sent button { display: none; }
      .cta-form.sent .thanks { display: block; }
      .cta-moss {
        position: absolute; right: -6%; bottom: -30%; width: 62%; aspect-ratio: 1; border-radius: 50%;
        background: radial-gradient(circle at 40% 35%, #a9dd3a 0, #5f8a2a 22%, #2d4a1c 48%, rgba(16, 41, 26, 0) 70%);
        filter: blur(2px); opacity: 0.75;
        -webkit-mask: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 400 400'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.045' numOctaves='4' seed='3'/%3E%3CfeColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3.2 -1.3'/%3E%3C/filter%3E%3Crect width='400' height='400' filter='url(%23n)'/%3E%3C/svg%3E") center/cover;
        mask: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 400 400'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='.045' numOctaves='4' seed='3'/%3E%3CfeColorMatrix values='0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 3.2 -1.3'/%3E%3C/filter%3E%3Crect width='400' height='400' filter='url(%23n)'/%3E%3C/svg%3E") center/cover;
      }
      .foot { position: relative; z-index: 5; background: #0b1d12; color: rgba(255, 255, 255, 0.8); padding: 60px 34px 30px; }
      .foot-top { display: flex; justify-content: space-between; gap: 40px; flex-wrap: wrap; }
      .foot .brand { color: #fff; }
      .foot-top p { margin-top: 12px; font-size: 14px; opacity: 0.6; }
      .cols { display: flex; gap: 70px; flex-wrap: wrap; }
      .cols > div { display: flex; flex-direction: column; gap: 10px; font-size: 14px; }
      .cols span { font: 400 10.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; opacity: 0.5; margin-bottom: 6px; }
      .cols a:hover { color: var(--lime); }
      .foot-bot { display: flex; justify-content: space-between; gap: 20px; margin-top: 60px; padding-top: 20px; border-top: 1px solid rgba(255, 255, 255, 0.12); font: 400 10.5px var(--mono); letter-spacing: 0.14em; text-transform: uppercase; opacity: 0.55; }
      @media (max-width: 1000px) {
        .steps { grid-template-columns: repeat(2, 1fr); }
        .pod, .faq { grid-template-columns: 1fr; gap: 40px; }
      }
      @media (max-width: 820px) {
        .sec { padding: 80px 18px; }
        .steps, .plans { grid-template-columns: 1fr; }
        .step { min-height: 0; }
        .step svg { margin: 24px 0 0; }
        .cta { padding: 90px 18px 110px; }
        .cta-moss { width: 110%; right: -40%; bottom: -45%; }
        .foot { padding: 50px 18px 26px; }
        .cols { gap: 36px; }
        .foot-bot { flex-direction: column; gap: 8px; }
        .qs p { padding-right: 0; }
        .viz-bot strong { font-size: 19px; }
      }
      @media (max-width: 820px) {
        nav { padding: 16px 18px; }
        .menu { display: none; }
        .brand { font-size: 19px; }
        .rk1 { width: 16vw; }
        .rk3 { width: 30vw; top: 70%; }
        .hero-copy { top: 12.5vh; padding: 0 18px; }
        .hero-copy h1 { font-size: clamp(44px, 6vw, 96px); white-space: normal; }
        .hero-copy .line { white-space: normal; }
        .hud { left: 50%; top: 66%; }
        .caption { left: 18px; right: 18px; bottom: 70px; }
        .hint { right: 18px; bottom: 24px; }
        .cred { left: 18px; top: 11vh; max-width: 80vw; }
        .carbon { left: 18px; top: auto; bottom: 6vh; width: 210px; padding: 14px; }
        .carbon .spark { width: 180px; }
        .feats { right: 18px; top: auto; bottom: 6vh; width: 45vw; padding: 5px 10px; }
        .feat { font-size: 9.5px; grid-template-columns: 24px 1fr 0; gap: 5px; }
        .feat .arrow { display: none; }
        .cards { grid-template-columns: 1fr; }
        .sol-card { height: 340px; }
        #sol { padding: 50px 18px 70px; }
        .stats { grid-template-columns: repeat(2, 1fr); gap: 28px 18px; }
        .vision { width: 90vw; }
        .acct { left: 18px; width: 86vw; }
        .fog { width: 80vw; }
      }
      @media (max-width: 480px) {
        #L3 .hotspot[style*="left: 83%"] { left: 60% !important; }
        .hero-copy h1 { font-size: clamp(42px, 10vw, 58px); }
        .caption { font-size: 9px; }
        .carbon { width: 190px; }
        .carbon .spark { width: 160px; }
        .feats { width: 43vw; }
        .feat { font-size: 8px; letter-spacing: 0.06em; }
        .cred { font-size: 22px; }
        .hot-label { font-size: 8px; }
        .hotspot { gap: 5px; }
        .hotspot .dot { width: 18px; height: 18px; flex-basis: 18px; }
        .hotspot .dot:before,
        .hotspot .dot:after { width: 8px; }
      }
      /* with the menu hidden, keep the CTA in the right-hand column */
      @media (max-width: 820px) {
        .talk { grid-column: 3; }
      }
      @media (prefers-reduced-motion: reduce) {
        .mist, .f1, .f2, .bob, .dot:before { animation: none; }
        .hero-copy .line span { animation: none; transform: none; }
        .rv { opacity: 1; transform: none; transition: none; }
        .card-bg, .sol-card, .card-copy p { transition: none; }
      }
    </style>
  </head>
  <body>
    <nav data-section="nav">
      <a class="brand" href="#top" aria-label="Bryo home">
        <svg viewBox="0 0 32 32" aria-hidden="true">
          <path d="M16 2l12 7v14l-12 7-12-7V9z" fill="currentColor" />
          <path d="M16 8c-4 4-5 9-1 16 1-5 4-9 8-11-3 0-5 1-7 3 0-3 0-5 0-8z" fill="#c6f35c" />
        </svg>
        Bryo
      </a>
      <div class="menu">
        <a href="#pod">Product <i class="chev"></i></a><a href="#how">How it grows <i class="chev"></i></a><a href="#sol">Use cases <i class="chev"></i></a><a href="#pricing">Pricing <i class="chev"></i></a>
      </div>
      <a class="talk" href="#start">START GROWING <i>›</i></a>
    </nav>
    <main id="top">
      <section id="story" data-section="hero">
        <div class="stage">
          <div class="cam" id="cam">
            <canvas id="cv"></canvas><img class="plate" id="plate" alt="" />
            <div class="mist"></div>
          </div>
          <div class="fog" id="fog">
            <div class="f0"></div>
            <div class="f1"></div>
            <div class="f2"></div>
          </div>
          <div class="layer" id="L0">
            <div class="hero-copy" id="heroCopy">
              <span class="chip">Autonomous moss cultivation</span>
              <h1><span class="line"><span>The AI That Grows Moss</span></span></h1>
            </div>
          </div>
          <div class="cam camF" id="camF"><img id="fernImg" alt="" /></div>
          <div class="rock rk1" data-x="-.3" data-y="-.6" data-d="1.3">
            <div class="bob"><img data-rock="1" alt="" /></div>
          </div>
          <div class="rock rk3" data-x="1" data-y=".55" data-d="1.8">
            <div class="bob"><img data-rock="3" alt="" /></div>
          </div>
          <div class="layer" id="L1">
            <div class="hud" id="hud">
              <i class="cross"></i><span class="chip">Live colony</span>
              <pre>
SPECIES  HYPNUM CUPR.
HUMIDITY 92 %
GROWTH   +0.4 MM/DAY</pre>
            </div>
            <div class="caption" id="caption">
              Autonomous bryophyte cultivation.<br />Vision models, micro-misting,<br />and infinite patience.
            </div>
            <div class="hint" id="hint">SCROLL TO EXPLORE</div>
          </div>
          <div class="layer" id="L2">
            <div class="vision" id="vision">
              <span class="chip">How Bryo thinks</span>
              <h2>
                <span>From</span> <span>Bare</span> <span>Stone</span>
                <span>to</span><br /><span>Living,</span> <span>Breathing</span><br /><span>Green</span>
                <span>Carpet</span>
              </h2>
              <p>
                Bryo watches light, moisture and spore density every minute,<br />then
                tends each colony exactly when it needs it.
              </p>
            </div>
          </div>
          <div class="layer" id="L3">
            <p class="acct" id="acct"></p>
            <div class="hotspot" style="left: 12%; top: 58%" data-name="Spore density" data-value="1.2M / m²">
              <i class="dot"></i>
              <div><div class="hot-label">Spore density</div><em>1.2M / m²</em></div>
            </div>
            <div class="hotspot" style="left: 33%; top: 41%" data-name="Mist cycle" data-value="every 14 min">
              <i class="dot"></i>
              <div><div class="hot-label">Mist cycle</div><em>every 14 min</em></div>
            </div>
            <div class="hotspot" style="left: 70%; top: 66%" data-name="Colony health" data-value="97 % vital">
              <i class="dot"></i>
              <div><div class="hot-label">Colony health</div><em>97 % vital</em></div>
            </div>
            <div class="hotspot" style="left: 83%; top: 47%" data-name="Light (PAR)" data-value="86 µmol">
              <i class="dot"></i>
              <div><div class="hot-label">Light (PAR)</div><em>86 µmol</em></div>
            </div>
          </div>
          <div class="layer" id="L4">
            <div class="cred" id="cred">
              <span class="fieldtag">✕ Grow bed 07</span>Living
              surfaces that tend themselves
            </div>
            <div class="carbon" id="carbon">
              <h4>Moss coverage<br />this season</h4>
              <div class="note">Bed 07 · 12 weeks</div>
              <div class="num"><span id="carbonNum">0</span><span class="unit"> % cover</span></div>
              <span class="gain">+9 % / wk</span><svg class="spark" viewBox="0 0 220 70" aria-label="Moss coverage trend">
                <polyline id="sparkline" points="0,60 30,55 60,57 90,44 120,46 150,30 180,24 214,10" stroke-dasharray="260" stroke-dashoffset="260" />
                <circle cx="90" cy="44" r="2.4" />
                <circle cx="150" cy="30" r="2.4" />
                <circle class="last" cx="214" cy="10" r="3.4" />
              </svg>
              <footer>W1 · W4 · W8 · W12</footer>
            </div>
            <div class="feats" id="feats">
              <div class="feat"><span class="idx">01</span><span>Computer-vision colony mapping</span><span class="arrow">→</span></div>
              <div class="feat"><span class="idx">02</span><span>Adaptive misting &amp; humidity control</span><span class="arrow">→</span></div>
              <div class="feat"><span class="idx">03</span><span>Species-matched spore blends</span><span class="arrow">→</span></div>
              <div class="feat"><span class="idx">04</span><span>Self-learning growth models</span><span class="arrow">→</span></div>
              <div class="feat"><span class="idx">05</span><span>Scales from tabletop to rooftop</span><span class="arrow">→</span></div>
            </div>
          </div>
          <div class="prog"><i id="progress"></i></div>
        </div>
      </section>
      <section id="sol" data-section="use-cases">
        <div class="sol-head">
          <div>
            <span class="chip">What Bryo grows</span>
            <h2>Living surfaces, grown on autopilot</h2>
          </div>
          <p>
            Moss cools buildings, holds rainwater, filters fine dust and needs no
            soil. It’s also slow and fussy, which is exactly the kind of work an AI
            is good at.
          </p>
        </div>
        <div class="cards">
          <article class="sol-card">
            <div class="card-bg" data-art="forest" style="background-position: 22% 70%; background-size: 260%"></div>
            <div class="card-top"><span class="bracket">[Restoration]</span><span class="circle">→</span></div>
            <div class="card-copy">
              <h3>Rewilding bare &amp;<br />burned ground</h3>
              <p>Moss is nature’s first coloniser. Bryo seeds native species that stabilise soil and make room for everything that follows.</p>
            </div>
          </article>
          <article class="sol-card">
            <div class="card-bg" data-art="fields" style="background-position: 50% 50%; background-size: 190%"></div>
            <div class="card-top"><span class="bracket">[Infrastructure]</span><span class="circle">→</span></div>
            <div class="card-copy">
              <h3>Groundcover for<br />solar &amp; road verges</h3>
              <p>A living mat under panels and along verges that holds dust, slows runoff, and never needs mowing.</p>
            </div>
          </article>
          <article class="sol-card">
            <div class="card-bg" data-art="forest" style="background-position: 62% 30%; background-size: 230%"></div>
            <div class="card-top"><span class="bracket">[Conservation]</span><span class="circle">→</span></div>
            <div class="card-copy">
              <h3>Rare species<br />propagation</h3>
              <p>Botanic gardens use Bryo to grow endangered bryophytes from a few spores into banked, healthy colonies.</p>
            </div>
          </article>
        </div>
        <div class="stats">
          <div class="stat"><strong data-count="1240" data-format="comma">0</strong><span>Grow beds online</span></div>
          <div class="stat"><strong data-count="38">0</strong><span>Moss species cultivated</span></div>
          <div class="stat"><strong data-count="2.1" data-decimals="1">0</strong><span>Million m² grown</span></div>
          <div class="stat"><strong data-count="99.4" data-decimals="1">0</strong><span>% Colony survival</span></div>
        </div>
      </section>
      <section id="how" class="sec" data-section="how-it-works">
        <div class="sec-head rv">
          <span class="chip">How it grows</span>
          <h2>Four loops, running every minute of every day</h2>
        </div>
        <ol class="steps">
          <li class="step rv">
            <span class="step-n">01 / Scan</span>
            <svg viewBox="0 0 48 48" aria-hidden="true"><path d="M6 16V6h10M32 6h10v10M42 32v10H32M16 42H6V32" /><circle cx="24" cy="24" r="7" /><path d="M24 17v-3M24 34v-3M17 24h-3M34 24h-3" /></svg>
            <h3>Read the surface</h3>
            <p>Multispectral cameras map texture, shade and existing colonies down to the millimetre.</p>
          </li>
          <li class="step rv">
            <span class="step-n">02 / Seed</span>
            <svg viewBox="0 0 48 48" aria-hidden="true"><circle cx="14" cy="16" r="3" /><circle cx="30" cy="12" r="2" /><circle cx="24" cy="26" r="4" /><circle cx="36" cy="30" r="2.5" /><circle cx="14" cy="34" r="2" /><path d="M6 42c8-4 28-4 36 0" /></svg>
            <h3>Match the species</h3>
            <p>Bryo picks from 38 cultivated species and blends spores for the exact light and stone it found.</p>
          </li>
          <li class="step rv">
            <span class="step-n">03 / Tend</span>
            <svg viewBox="0 0 48 48" aria-hidden="true"><path d="M24 6c7 10 12 16 12 23a12 12 0 0 1-24 0c0-7 5-13 12-23z" /><path d="M19 30a5 5 0 0 0 5 5" /></svg>
            <h3>Mist, shade, feed</h3>
            <p>Micro-misters and adaptive shade fire in short cycles, holding humidity in the narrow band moss loves.</p>
          </li>
          <li class="step rv">
            <span class="step-n">04 / Learn</span>
            <svg viewBox="0 0 48 48" aria-hidden="true"><path d="M38 20a15 15 0 0 0-27-6M10 28a15 15 0 0 0 27 6" /><path d="M11 6v8h8M37 42v-8h-8" /></svg>
            <h3>Get better every bed</h3>
            <p>Every frame of growth trains the model, so each new installation takes hold faster than the last.</p>
          </li>
        </ol>
      </section>
      <section id="pod" class="sec pod" data-section="product">
        <div class="pod-copy rv">
          <span class="chip">The Bryo Pod</span>
          <h2>A gardener that never sleeps, in a box the size of a book</h2>
          <p>
            Each Pod carries a camera, humidity and light sensors, a micro-mister
            and a spore cartridge. Mount it, point it at bare stone, and walk
            away — Bryo Cloud handles the rest.
          </p>
          <ul class="spec">
            <li><span>Coverage</span><strong>Up to 12 m² per Pod</strong></li>
            <li><span>Power</span><strong>Solar + 30-day battery</strong></li>
            <li><span>Water</span><strong>4 L reservoir, rain-fed refill</strong></li>
            <li><span>Connectivity</span><strong>LTE-M or Wi-Fi mesh</strong></li>
          </ul>
        </div>
        <div class="pod-viz rv">
          <div class="viz-top"><span>Live bed · simulation</span><span id="vDay">Day 0</span></div>
          <canvas id="grow" width="1040" height="760" aria-label="Simulated moss colonies spreading across stone"></canvas>
          <div class="viz-bot">
            <div><span>Coverage</span><strong id="vCov">0%</strong></div>
            <div><span>Humidity</span><strong id="vHum">92%</strong></div>
            <div><span>Next mist</span><strong id="vMist">14 min</strong></div>
          </div>
        </div>
      </section>
      <section id="pricing" class="sec" data-section="pricing">
        <div class="sec-head rv">
          <span class="chip">Pricing</span>
          <h2>Start with one bed. Grow from there.</h2>
        </div>
        <div class="plans">
          <article class="plan rv">
            <span class="plan-n">Seedling</span>
            <div class="price">$29<small>/ Pod / month</small></div>
            <p>For balconies, courtyards and curious people.</p>
            <ul><li>1 Bryo Pod</li><li>3 regional species blends</li><li>App + weekly growth reports</li><li>Spore refills every quarter</li></ul>
            <a class="btn ghost" href="#start">Start growing</a>
          </article>
          <article class="plan featured rv">
            <span class="plan-n">Colony <em>Most planted</em></span>
            <div class="price">$24<small>/ Pod / month</small></div>
            <p>For buildings, campuses and landscape teams, from 10 Pods.</p>
            <ul><li>Fleet dashboard &amp; alerts</li><li>All 38 cultivated species</li><li>Priority spore refills</li><li>API &amp; BMS integration</li></ul>
            <a class="btn" href="#start">Start growing</a>
          </article>
          <article class="plan rv">
            <span class="plan-n">Canopy</span>
            <div class="price">Custom</div>
            <p>For cities, restoration programs and research gardens.</p>
            <ul><li>Unlimited Pods</li><li>Site survey &amp; installation</li><li>Custom species research</li><li>Dedicated grow scientist</li></ul>
            <a class="btn ghost" href="#start">Talk to us</a>
          </article>
        </div>
      </section>
      <section id="faq" class="sec faq" data-section="faq">
        <div class="sec-head rv">
          <span class="chip">Questions</span>
          <h2>Things people ask before they go green</h2>
        </div>
        <div class="qs rv">
          <details open><summary>How long until I see green?</summary><p>Most beds show visible colonies within three to five weeks and reach 80% cover in a single season, depending on climate and species.</p></details>
          <details><summary>Does it work indoors?</summary><p>Yes. Indoor Pods add a full-spectrum grow light and closed-loop misting, so living walls thrive far from any window.</p></details>
          <details><summary>What does the AI actually do?</summary><p>It watches the bed through the Pod’s camera, predicts how each colony will spread, and decides when to mist, shade or reseed. Every decision is logged in the app so you can see why.</p></details>
          <details><summary>Is it good for the environment?</summary><p>Moss needs no soil or fertiliser, cools surfaces, stores rainwater and traps fine dust. Bryo only plants species native to your region.</p></details>
          <details><summary>What if a Pod goes offline?</summary><p>It falls back to an on-device schedule tuned to the last 30 days of data, and syncs with Bryo Cloud as soon as it reconnects.</p></details>
        </div>
      </section>
      <section id="start" class="cta" data-section="cta">
        <div class="cta-in rv">
          <span class="chip">Get started</span>
          <h2>Bare stone today.<br />Living carpet by spring.</h2>
          <form class="cta-form" onsubmit="event.preventDefault(); this.classList.add('sent');">
            <input type="email" required placeholder="you@example.com" aria-label="Email address" />
            <button class="btn" type="submit">Join the waitlist <i>›</i></button>
            <span class="thanks">You’re on the list. We’ll be in touch before the next growing season.</span>
          </form>
        </div>
        <div class="cta-moss" aria-hidden="true"></div>
      </section>
    </main>
    <footer class="foot" data-section="footer">
      <div class="foot-top">
        <div>
          <a class="brand" href="#top">
            <svg viewBox="0 0 32 32" aria-hidden="true"><path d="M16 2l12 7v14l-12 7-12-7V9z" fill="currentColor" /><path d="M16 8c-4 4-5 9-1 16 1-5 4-9 8-11-3 0-5 1-7 3 0-3 0-5 0-8z" fill="#c6f35c" /></svg>
            Bryo
          </a>
          <p>The AI that grows moss.</p>
        </div>
        <div class="cols" role="navigation" aria-label="Footer">
          <div><span>Product</span><a href="#pod">Bryo Pod</a><a href="#how">Bryo Cloud</a><a href="#sol">Species library</a><a href="#pricing">Pricing</a></div>
          <div><span>Company</span><a href="#top">About</a><a href="#top">Research</a><a href="#top">Careers</a><a href="#top">Press</a></div>
          <div><span>Resources</span><a href="#faq">Grow guides</a><a href="#faq">API docs</a><a href="#faq">Support</a><a href="#faq">Status</a></div>
        </div>
      </div>
      <div class="foot-bot"><span>© 2026 Bryo Labs</span><span>Grown, not manufactured.</span></div>
    </footer>
    <script>
      (() => {
        const REDUCE = matchMedia("(prefers-reduced-motion: reduce)").matches;
        const $ = (s) => document.querySelector(s),
          $$ = (s) => [...document.querySelectorAll(s)],
          clamp = (v) => Math.max(0, Math.min(1, v)),
          seg = (p, a, b) => clamp((p - a) / (b - a)),
          ease = (t) => (t < 0.5 ? 4 * t * t * t : 1 - Math.pow(-2 * t + 2, 3) / 2);

        /* =====================================================================
           PROCEDURAL ART — replaces every photo and the push-in video.
           The scene is a 1600×900 "frame" (same geometry the original
           video / plate used), rendered as depth layers that a virtual
           camera dollies through.
           ===================================================================== */
        const FW = 1600, FH = 900, VPX = 800, VPY = 410, ZEND = 4;
        const mk = (w, h) => Object.assign(document.createElement("canvas"), { width: w, height: h });
        const mkRng = (a) => () => {
          a |= 0; a = (a + 0x6d2b79f5) | 0;
          let t = Math.imul(a ^ (a >>> 15), 1 | a);
          t = (t + Math.imul(t ^ (t >>> 7), 61 | t)) ^ t;
          return ((t ^ (t >>> 14)) >>> 0) / 4294967296;
        };
        const mkNoise = (seed) => {
          const r = mkRng(seed), v = new Float32Array(1024);
          for (let i = 0; i < 1024; i++) v[i] = r();
          const n = (x) => {
            const i = Math.floor(x), f = x - i, u = f * f * (3 - 2 * f);
            return v[i & 1023] * (1 - u) + v[(i + 1) & 1023] * u;
          };
          return (x, o = 4) => {
            let a = 0, am = 0.5, fr = 1, nm = 0;
            for (let k = 0; k < o; k++) { a += n(x * fr + k * 17.31) * am; nm += am; am *= 0.5; fr *= 2.07; }
            return a / nm;
          };
        };
        const mkNoise2 = (seed) => {
          const r = mkRng(seed), v = new Float32Array(65536);
          for (let i = 0; i < 65536; i++) v[i] = r();
          const at = (x, y) => v[((y & 255) << 8) | (x & 255)];
          const n = (x, y) => {
            const xi = Math.floor(x), yi = Math.floor(y), xf = x - xi, yf = y - yi,
              u = xf * xf * (3 - 2 * xf), w = yf * yf * (3 - 2 * yf),
              a = at(xi, yi), b = at(xi + 1, yi), c = at(xi, yi + 1), d = at(xi + 1, yi + 1);
            return a + (b - a) * u + (c - a) * w + (a - b - c + d) * u * w;
          };
          return (x, y, o = 4) => {
            let a = 0, am = 0.5, fr = 1, nm = 0;
            for (let k = 0; k < o; k++) { a += n(x * fr + k * 31.7, y * fr + k * 11.3) * am; nm += am; am *= 0.5; fr *= 2.03; }
            return a / nm;
          };
        };
        const hexA = (hex, a) => hex + Math.round(clamp(a) * 255).toString(16).padStart(2, "0");
        const lerpHex = (a, b, t) => {
          const A = parseInt(a.slice(1), 16), B = parseInt(b.slice(1), 16),
            ch = (s) => Math.round(((A >> s) & 255) * (1 - t) + ((B >> s) & 255) * t);
          return "#" + ((1 << 24) | (ch(16) << 16) | (ch(8) << 8) | ch(0)).toString(16).slice(1);
        };
        const lin = (g, x0, y0, x1, y1, stops) => {
          const gr = g.createLinearGradient(x0, y0, x1, y1);
          stops.forEach(([o, c]) => gr.addColorStop(o, c));
          return gr;
        };
        // vertical colour that holds until y1 then fades to transparent by y2
        const vfade = (g, y0, y1, y2, col) => lin(g, 0, y0, 0, y2, [[0, col], [clamp((y1 - y0) / (y2 - y0)), col], [1, hexA(col, 0)]]);
        function conifer(p, x, y, w, h) {
          p.moveTo(x, y - h);
          p.lineTo(x + w * 0.5, y - h * 0.58); p.lineTo(x + w * 0.28, y - h * 0.58);
          p.lineTo(x + w * 0.78, y - h * 0.22); p.lineTo(x + w * 0.5, y - h * 0.22);
          p.lineTo(x + w, y); p.lineTo(x - w, y);
          p.lineTo(x - w * 0.5, y - h * 0.22); p.lineTo(x - w * 0.78, y - h * 0.22);
          p.lineTo(x - w * 0.28, y - h * 0.58); p.lineTo(x - w * 0.5, y - h * 0.58);
          p.closePath();
        }
        function ridge(base, amp, freq, seed, step = 5) {
          const n = mkNoise(seed), pts = [], p = new Path2D();
          p.moveTo(-80, 1300);
          for (let x = -80; x <= 1680; x += step) {
            const y = base - amp * (n(x * freq + 50, 5) - 0.3) * 1.6;
            pts.push([x, y]); p.lineTo(x, y);
          }
          p.lineTo(1680, 1300); p.closePath();
          return { p, pts };
        }
        function ridgeTrees(pts, r, dens, h0, h1, sink) {
          const p = new Path2D();
          for (const [x, y] of pts)
            if (r() < dens) { const h = h0 + r() * (h1 - h0); conifer(p, x + r() * 4, y + sink * (0.4 + r()), h * 0.26, h); }
          return p;
        }
        const fadeSolid = (d) => clamp((d - 0.05) / 0.4);
        function band(z, cy, half, a, col = "231,235,232", fade = fadeSolid) {
          return {
            z, fade,
            draw(g) {
              g.fillStyle = lin(g, 0, cy - half * 2, 0, cy + half * 2, [
                [0, `rgba(${col},0)`], [0.25, `rgba(${col},${a * 0.7})`], [0.5, `rgba(${col},${a})`],
                [0.75, `rgba(${col},${a * 0.7})`], [1, `rgba(${col},0)`],
              ]);
              g.fillRect(-4000, -4000, 9600, 9000);
            },
          };
        }

        function drawSky(g) {
          g.fillStyle = lin(g, 0, 0, 0, FH, [[0, "#d2d9d5"], [0.42, "#e8ebe9"], [0.62, "#eceeec"], [1, "#dde2df"]]);
          g.fillRect(-400, -400, 2400, 1700);
          const sun = g.createRadialGradient(1180, 160, 0, 1180, 160, 560);
          sun.addColorStop(0, "rgba(255,255,252,.6)"); sun.addColorStop(1, "rgba(255,255,252,0)");
          g.fillStyle = sun; g.fillRect(-400, -400, 2400, 1700);
          for (const [an, wd, al] of [[2.2, 0.05, 0.14], [2.45, 0.035, 0.1], [2.0, 0.03, 0.1], [2.7, 0.025, 0.08], [1.85, 0.04, 0.09]]) {
            const len = 1500;
            g.fillStyle = lin(g, 1180, 160, 1180 + Math.cos(an) * len, 160 + Math.sin(an) * len, [[0, `rgba(255,255,246,${al})`], [1, "rgba(255,255,246,0)"]]);
            g.beginPath(); g.moveTo(1180, 160);
            g.lineTo(1180 + Math.cos(an - wd) * len, 160 + Math.sin(an - wd) * len);
            g.lineTo(1180 + Math.cos(an + wd) * len, 160 + Math.sin(an + wd) * len);
            g.fill();
          }
        }

        /* ---------- far ridges ---------- */
        function buildFar() {
          const r = mkRng(101), R = [ridge(392, 48, 0.0035, 1), ridge(415, 38, 0.0055, 2), ridge(437, 30, 0.008, 3)],
            cols = ["#c8d0cc", "#bac5c0", "#adbab4"], trees = ridgeTrees(R[2].pts, r, 0.5, 3, 7, 2);
          return {
            z: 14, fade: fadeSolid,
            draw(g) {
              R.forEach((rd, i) => { g.fillStyle = vfade(g, 300, 520, 600, cols[i]); g.fill(rd.p); });
              g.fillStyle = vfade(g, 300, 520, 600, "#a2b0a9"); g.fill(trees);
            },
          };
        }
        /* ---------- mid forested hills ---------- */
        function buildMid() {
          const r = mkRng(202), A = ridge(456, 32, 0.0065, 4), B = ridge(476, 24, 0.01, 5),
            tA = ridgeTrees(A.pts, r, 0.75, 6, 12, 3), tB = ridgeTrees(B.pts, r, 0.8, 7, 14, 3);
          return {
            z: 10, fade: fadeSolid,
            draw(g) {
              g.fillStyle = vfade(g, 380, 560, 640, "#9aad9f"); g.fill(A.p);
              g.fillStyle = vfade(g, 380, 560, 640, "#8ca293"); g.fill(tA);
              g.fillStyle = vfade(g, 400, 560, 640, "#879e8e"); g.fill(B.p);
              g.fillStyle = vfade(g, 400, 560, 640, "#7a9282"); g.fill(tB);
            },
          };
        }
        /* ---------- near valley forest + flux tower (Field station 07) ---------- */
        function buildNear() {
          const r = mkRng(303), A = ridge(498, 30, 0.007, 6), B = ridge(520, 26, 0.011, 7),
            tA = ridgeTrees(A.pts, r, 0.85, 9, 18, 4), tB = ridgeTrees(B.pts, r, 0.9, 10, 22, 4), rows = [];
          for (let k = 0; k < 11; k++) {
            const p = new Path2D(), y = 532 + k * 9, sp = 6.5 + k * 0.5, h0 = 12 + k * 1.6;
            for (let x = 110 + r() * sp; x < 1490; x += sp * (0.75 + r() * 0.5)) {
              const h = h0 * (1 + r() * 0.7);
              conifer(p, x, y + (r() - 0.5) * 6, h * 0.27, h);
            }
            rows.push({ p, col: lerpHex("#4d6b53", "#2b4532", k / 10) });
          }
          const tower = new Path2D(), tx = 612, tb = 552, th = 66;
          const L = (u) => tx - 9 + 6 * u, Rr = (u) => tx + 9 - 6 * u;
          tower.moveTo(L(0), tb); tower.lineTo(L(1), tb - th);
          tower.moveTo(Rr(0), tb); tower.lineTo(Rr(1), tb - th);
          for (let i = 0; i < 5; i++) {
            const u0 = i / 5, u1 = (i + 1) / 5;
            tower.moveTo(L(u0), tb - th * u0); tower.lineTo(Rr(u1), tb - th * u1);
            tower.moveTo(Rr(u0), tb - th * u0); tower.lineTo(L(u1), tb - th * u1);
            tower.moveTo(L(u1), tb - th * u1); tower.lineTo(Rr(u1), tb - th * u1);
          }
          tower.moveTo(tx, tb - th); tower.lineTo(tx, tb - th - 10);
          tower.moveTo(tx - 9, tb - th - 6); tower.lineTo(tx + 9, tb - th - 6);
          const drawTower = (g) => {
            g.strokeStyle = "#26352a"; g.lineWidth = 1.1; g.stroke(tower);
            const gl = g.createRadialGradient(tx, tb - th - 11, 0, tx, tb - th - 11, 11);
            gl.addColorStop(0, "rgba(198,243,92,.85)"); gl.addColorStop(1, "rgba(198,243,92,0)");
            g.fillStyle = gl; g.fillRect(tx - 12, tb - th - 23, 24, 24);
            g.fillStyle = "#c6f35c"; g.beginPath(); g.arc(tx, tb - th - 11, 2, 0, 6.283); g.fill();
          };
          return {
            z: 7, fade: fadeSolid,
            draw(g) {
              g.fillStyle = vfade(g, 420, 650, 730, "#6c8971"); g.fill(A.p);
              g.fillStyle = vfade(g, 420, 650, 730, "#5f7c65"); g.fill(tA);
              g.fillStyle = vfade(g, 440, 650, 730, "#58755e"); g.fill(B.p);
              g.fillStyle = vfade(g, 440, 650, 730, "#4b6951"); g.fill(tB);
              rows.forEach((rw, i) => {
                g.fillStyle = vfade(g, 450, 650, 730, rw.col); g.fill(rw.p);
                if (i === 2) drawTower(g);
              });
            },
          };
        }
        /* ---------- shared per-pixel shader: moss-capped floating rock ----------
           Analytic silhouette → height field → bump-mapped lighting (sun upper-right),
           moss clumps + spore speckles on top, lichen-flecked rock strata below,
           hanging moss strands over the lip, fog swallowing the base. */
        const sm = (a, b, x) => { const t = clamp((x - a) / (b - a)); return t * t * (3 - 2 * t); };
        const mixc = (a, b, t) => [a[0] + (b[0] - a[0]) * t, a[1] + (b[1] - a[1]) * t, a[2] + (b[2] - a[2]) * t];
        const rgb = (c, f = 1) => `rgb(${Math.min(255, c[0] * f) | 0},${Math.min(255, c[1] * f) | 0},${Math.min(255, c[2] * f) | 0})`;
        const LX = 0.45, LY = -0.72, LZ = 0.53;
        function islandShader(o) {
          const { cx, cy, rx, back, front, depth, seed, x0, y0, w, h, R } = o,
            fog = o.fog || [223, 227, 224], haze = o.haze || 0, fogAlpha = !!o.fogAlpha,
            W = Math.ceil(w * R), Hh = Math.ceil(h * R),
            N = mkNoise2(seed), n1 = mkNoise(seed + 1), n2 = mkNoise(seed + 2), n3 = mkNoise(seed + 3), n4 = mkNoise(seed + 4),
            cBY = new Float32Array(W), cFY = new Float32Array(W), cDY = new Float32Array(W),
            cUY = new Float32Array(W), cU = new Float32Array(W), cS = new Float32Array(W);
          for (let px = 0; px < W; px++) {
            const fx = x0 + (px + 0.5) / R, u = (fx - cx) / rx, q = Math.max(0, 1 - u * u), sq = Math.sqrt(q);
            cU[px] = u; cS[px] = sq;
            if (q <= 0) { cBY[px] = 1e9; continue; }
            cBY[px] = cy - back * sq * (0.8 + 0.4 * n1(u * 6 + 3, 3));
            cFY[px] = cy + front * sq + front * 0.14 * (n2(u * 14, 3) - 0.5) * sq;
            cDY[px] = cFY[px] + front * sq * (0.2 + 0.8 * Math.pow(q, 0.7) * n4(u * 5, 3) + 0.7 * Math.pow(n4(u * 55 + 7, 3), 2) + 0.4 * Math.pow(n4(u * 260 + 3, 2), 3));
            const uu = (u + 1) / 2, s = Math.sin(Math.PI * Math.pow(uu, 1.08));
            cUY[px] = cFY[px] + depth * Math.pow(s, 2.6) * (0.86 + 0.28 * n3(u * 3, 3)) + depth * 0.07 * (n3(u * 22 + 9, 2) - 0.5) * s;
          }
          const n = W * Hh, H1 = new Float32Array(n), H2 = new Float32Array(n), RG = new Uint8Array(n),
            A1 = new Float32Array(n), A2 = new Float32Array(n);
          for (let py = 0; py < Hh; py++) {
            const fy = y0 + (py + 0.5) / R;
            for (let px = 0; px < W; px++) {
              const bY = cBY[px];
              if (fy < bY - 1 / R) continue;
              const i = py * W + px, u = cU[px], fY = cFY[px];
              if (fy < fY) {
                const v = (fy - bY) / (fY - bY + 1e-6), tx = u * 34, ty = (v - 0.5) * 2 * cS[px] * 34;
                H1[i] = 0.42 * N(tx * 0.17, ty * 0.17, 4) + 0.43 * N(tx, ty, 3) + 0.15 * N(tx * 4.6, ty * 4.6, 2);
                A1[i] = clamp((fy - bY) * R + 0.5); RG[i] = 1;
              } else {
                const uY = cUY[px], dY = cDY[px];
                if (fy < uY + 2 / R) {
                  const tx = u * 11, ty = ((fy - cy) / rx) * 30, rr = 1 - Math.abs(2 * N(tx * 0.6, ty * 0.35, 4) - 1);
                  H1[i] = 0.42 * rr + 0.3 * N(tx * 2.6, ty * 2.2, 3) + 0.28 * (0.5 + 0.5 * Math.sin(ty * 0.9 + 5 * N(tx * 0.2, ty * 0.2, 2)));
                  A1[i] = clamp((uY - fy) * R * 0.35); RG[i] = 2;
                }
                if (fy < dY + 1 / R) {
                  const tx = u * 150, ty = ((fy - cy) / rx) * 14;
                  H2[i] = 0.45 * N(tx, ty, 3) + 0.35 * N(tx * 0.3, ty * 2.5, 3) + 0.2 * N(tx * 3, ty * 0.6, 2);
                  A2[i] = clamp((dY - fy) * R * 0.3) * (0.75 + 0.25 * sm(0.2, 0.6, H2[i])); RG[i] |= 4;
                }
              }
            }
          }
          const c = mk(W, Hh), g = c.getContext("2d"), img = g.createImageData(W, Hh), D = img.data, bS = (rx * R) / 940,
            MD = [50, 72, 27], MM = [102, 136, 45], MB = [172, 194, 76], MS = [182, 172, 94], MK = [40, 64, 30],
            RD = [84, 86, 78], RL = [156, 155, 142], LI = [150, 162, 118], LO = [184, 150, 88], RW = [58, 60, 50],
            DD = [24, 40, 16], DL = [88, 118, 44];
          const shade = (nx, ny, nz) => Math.max(0, (nx * LX + ny * LY + nz * LZ) / Math.hypot(nx, ny, nz));
          for (let py = 1; py < Hh - 1; py++) {
            const fy = y0 + (py + 0.5) / R;
            for (let px = 1; px < W - 1; px++) {
              const i = py * W + px, rg = RG[i];
              if (!rg) continue;
              const u = cU[px], fY = cFY[px];
              let col = null, a = 0;
              if (rg === 1) {
                const hh = H1[i], b = 7 * bS, dx = (H1[i + 1] - H1[i - 1]) * b, dy = (H1[i + W] - H1[i - W]) * b,
                  dif = shade(-dx + u * 0.35, -dy - 0.9, 0.45),
                  v = (fy - cBY[px]) / (fY - cBY[px] + 1e-6), tx = u * 34, ty = (v - 0.5) * 2 * cS[px] * 34;
                let cl = mixc(MD, MM, sm(0.3, 0.72, hh));
                cl = mixc(cl, MB, sm(0.6, 0.88, hh) * 0.85);
                const cv = N(tx * 0.07 + 30, ty * 0.07, 3);
                cl = mixc(cl, MS, sm(0.6, 0.78, cv) * 0.45);
                cl = mixc(cl, MK, sm(0.42, 0.22, cv) * 0.45);
                const sp = N(tx * 7 + 90, ty * 7, 1);
                if (sp > 0.84) cl = mixc(cl, [218, 196, 100], Math.min(1, (sp - 0.84) / 0.1) * 0.7);
                const ao = 0.55 + 0.45 * sm(0.22, 0.7, hh), lip = 1 - 0.3 * sm(0.8, 1, v), L = (0.36 + 0.95 * dif) * ao * lip,
                  tr = sm(0.7, 0.95, hh) * dif * 28;
                col = [cl[0] * L * 0.97 + tr * 0.8, cl[1] * L + tr, cl[2] * L * 0.94 + tr * 0.3];
                a = A1[i];
              } else {
                let rc = null, ra = 0;
                if (rg & 2) {
                  const hh = H1[i], b = 4 * bS, dx = (H1[i + 1] - H1[i - 1]) * b, dy = (H1[i + W] - H1[i - W]) * b,
                    dif = shade(-dx + u * 0.95, -dy + 0.45, 0.8),
                    tx = u * 11, ty = ((fy - cy) / rx) * 30, gn = N(tx * 0.35 + 50, ty * 0.35, 3);
                  let cl = mixc(RD, RL, sm(0.25, 0.75, gn * 0.6 + hh * 0.4));
                  cl = mixc(cl, LI, sm(0.6, 0.72, N(tx * 1.3 + 80, ty * 0.9, 3)) * 0.75);
                  if (N(tx * 3.5 + 20, ty * 2.5, 2) > 0.76) cl = mixc(cl, LO, 0.55);
                  const dd = (fy - fY) / depth;
                  cl = mixc(cl, RW, (1 - sm(0, 0.22, dd)) * 0.55);
                  const ao = (0.55 + 0.45 * hh) * (0.35 + 0.65 * sm(0, 0.12, dd)), L = (0.42 + 0.9 * dif) * ao;
                  rc = [cl[0] * L, cl[1] * L, cl[2] * L * 1.03];
                  const f = sm(0.3, 1.0, dd) * 0.92;
                  if (fogAlpha) { ra = A1[i] * (1 - f * 0.85); rc = mixc(rc, fog, f * 0.5); }
                  else { rc = mixc(rc, fog, f); ra = A1[i]; }
                }
                if (rg & 4) {
                  const hh = H2[i], b = 3 * bS, dx = (H2[i + 1] - H2[i - 1]) * b,
                    dif = shade(-dx + u * 0.6, 0.05, 1), dd = (fy - fY) / (cDY[px] - fY + 1e-6),
                    cl = mixc(mixc(DD, DL, sm(0.25, 0.8, hh)), MM, (1 - sm(0, 0.35, dd)) * 0.35), L = (0.32 + 0.85 * dif) * (0.5 + 0.5 * (1 - dd)),
                    dc = [cl[0] * L, cl[1] * L, cl[2] * L], da = A2[i];
                  if (rc) {
                    a = da + ra * (1 - da);
                    const wr = (ra * (1 - da)) / (a || 1);
                    col = mixc(dc, rc, wr);
                  } else { col = dc; a = da; }
                } else { col = rc; a = ra; }
              }
              if (!col || a <= 0) continue;
              if (haze) col = mixc(col, fog, haze);
              const k = i * 4;
              D[k] = col[0]; D[k + 1] = col[1]; D[k + 2] = col[2]; D[k + 3] = a * 255;
            }
          }
          g.putImageData(img, 0, 0);
          const col = (fx) => Math.max(0, Math.min(W - 1, Math.round((fx - x0) * R)));
          c.mid = (fx) => (cBY[col(fx)] + cFY[col(fx)]) / 2;
          c.front = (fx) => cFY[col(fx)];
          c.drip = (fx) => cDY[col(fx)];
          return c;
        }
        // pre-render a vector layer into a bitmap (optionally with atmospheric blur)
        function bake(L, x0, y0, w, h, R, blur) {
          const c = mk(Math.ceil(w * R), Math.ceil(h * R)), g = c.getContext("2d");
          if (blur) g.filter = `blur(${blur}px)`;
          g.setTransform(R, 0, 0, R, -x0 * R, -y0 * R);
          L.draw(g);
          return { z: L.z, fade: L.fade, draw(gg) { gg.drawImage(c, x0, y0, w, h); } };
        }
        /* ---------- distant mini floating islands ---------- */
        function buildMinis() {
          const items = [[470, 300, 16], [1140, 268, 12], [1320, 392, 9], [300, 420, 7], [1010, 345, 6]].map(([x, y, s], i) => {
            const R = 8, bx = x - s * 1.15, by = y - s * 0.5, bw = s * 2.3, bh = s * 2.6;
            return {
              c: islandShader({ cx: x, cy: y, rx: s, back: s * 0.22, front: s * 0.16, depth: s * 1.9, seed: 500 + i * 7, x0: bx, y0: by, w: bw, h: bh, R, haze: 0.28 }),
              bx, by, bw, bh,
            };
          });
          return { z: 6, fade: fadeSolid, draw(g) { items.forEach((it) => g.drawImage(it.c, it.bx, it.by, it.bw, it.bh)); } };
        }
        /* ---------- detailed little conifer ---------- */
        function realTree(g, x, y, h, r) {
          g.save();
          g.translate(x - h * 0.22, y + 1); g.scale(1, 0.18);
          const sg = g.createRadialGradient(0, 0, 0, 0, 0, h * 0.4);
          sg.addColorStop(0, "rgba(10,20,6,.45)"); sg.addColorStop(1, "rgba(10,20,6,0)");
          g.fillStyle = sg; g.fillRect(-h * 0.5, -h * 0.5, h, h);
          g.restore();
          g.lineCap = "round";
          g.strokeStyle = "#3a2c1e"; g.lineWidth = h * 0.035;
          g.beginPath(); g.moveTo(x, y); g.lineTo(x, y - h); g.stroke();
          const n = Math.round(h * 0.9);
          for (let k = 0; k < n; k++) {
            const t = k / n, yy = y - h * 0.1 - t * h * 0.9, len = h * 0.3 * Math.pow(1 - t, 0.9) * (0.75 + r() * 0.5) + h * 0.02;
            for (const s of [-1, 1]) {
              g.strokeStyle = s > 0 ? lerpHex("#2f4a26", "#6a8a40", 0.3 + r() * 0.7) : lerpHex("#142416", "#2c4426", r());
              g.lineWidth = h * 0.03 * (1.2 - t * 0.6);
              g.beginPath(); g.moveTo(x, yy);
              g.quadraticCurveTo(x + s * len * 0.6, yy - len * 0.05, x + s * len, yy + len * 0.24);
              g.stroke();
            }
          }
        }
        /* ---------- the floating moss island ---------- */
        function buildIsland() {
          const x0 = 320, y0 = 430, w = 960, h = 470, R = 2, r = mkRng(36);
          const c = islandShader({ cx: 800, cy: 520, rx: 470, back: 52, front: 40, depth: 355, seed: 35, x0, y0, w, h, R, haze: 0.03 });
          const g = c.getContext("2d");
          g.setTransform(R, 0, 0, R, -x0 * R, -y0 * R);
          // contact shadow of the fern on the moss
          g.globalCompositeOperation = "source-atop";
          g.save(); g.translate(790, 508); g.scale(1, 0.13);
          const gr = g.createRadialGradient(0, 0, 0, 0, 0, 300);
          gr.addColorStop(0, "rgba(12,24,6,.62)"); gr.addColorStop(0.45, "rgba(12,24,6,.28)"); gr.addColorStop(1, "rgba(12,24,6,0)");
          g.fillStyle = gr; g.fillRect(-320, -320, 640, 640);
          g.restore();
          g.globalCompositeOperation = "source-over";
          // hanging roots
          g.lineCap = "round";
          for (let i = 0; i < 28; i++) {
            const x = 420 + r() * 760, y = c.drip(x) - 4, len = 30 + r() * 115, sw = (r() - 0.5) * 34, p = new Path2D();
            p.moveTo(x, y); p.bezierCurveTo(x + 8, y + len * 0.3, x - 10 + sw * 0.3, y + len * 0.65, x + sw, y + len);
            g.strokeStyle = lin(g, 0, y, 0, y + len, [[0, "rgba(40,34,22,.9)"], [1, "rgba(120,118,104,0)"]]);
            g.lineWidth = 1.4 + r() * 1.6; g.stroke(p);
            g.save(); g.translate(0.45, 0);
            g.strokeStyle = lin(g, 0, y, 0, y + len, [[0, "rgba(176,156,112,.4)"], [1, "rgba(176,156,112,0)"]]);
            g.lineWidth = 0.45; g.stroke(p); g.restore();
          }
          // trees and a shrub on the moss
          [[440, 48], [466, 32], [1172, 42]].forEach(([x, th]) => realTree(g, x, c.mid(x) + 6, th, r));
          for (let i = 0; i < 420; i++) {
            const an = r() * 6.283, rr = Math.sqrt(r()) * 16, x = 1118 + Math.cos(an) * rr * 1.3, y = c.mid(1118) - 4 + Math.sin(an) * rr * 0.75,
              lit = clamp(0.5 + (x - 1118) / 30 - (y - c.mid(1118)) / 40);
            g.fillStyle = rgb(mixc([28, 46, 20], [120, 150, 60], lit * (0.6 + r() * 0.4)));
            g.beginPath(); g.ellipse(x, y, 1.6 + r(), 1.1, r() * 3, 0, 6.283); g.fill();
          }
          return { z: 3, fade: fadeSolid, draw(gg) { gg.drawImage(c, x0, y0, w, h); } };
        }
        /* ---------- the fern: bipinnate fronds, self-shadowed, depth-blurred ---------- */
        function fernPinna(p, rib, x, y, a, l, w, T, bend) {
          const c = Math.cos(a), s = Math.sin(a),
            pt = (t, off) => { const o = off + bend * l * t * t; return [x + c * l * t - s * o, y + s * l * t + c * o]; },
            tp = (t) => Math.pow(Math.max(0, 1 - t * 0.9), 0.75);
          p.moveTo(x, y);
          for (let k = 1; k <= T; k++) {
            const t1 = k / T, tm = (k - 0.45) / T, C = pt(tm + 0.12 / T, w * 1.5 * tp(tm)), E = pt(t1, w * 0.25 * tp(t1));
            p.quadraticCurveTo(C[0], C[1], E[0], E[1]);
          }
          const tip = pt(1.04, 0);
          p.lineTo(tip[0], tip[1]);
          for (let k = T; k >= 1; k--) {
            const t0 = (k - 1) / T, tm = (k - 0.45) / T, C = pt(tm + 0.12 / T, -w * 1.5 * tp(tm)), E = pt(t0, -w * 0.25 * tp(t0));
            p.quadraticCurveTo(C[0], C[1], E[0], E[1]);
          }
          p.closePath();
          const r0 = pt(0, 0), r1 = pt(0.5, 0), r2 = pt(0.96, 0);
          rib.moveTo(r0[0], r0[1]); rib.quadraticCurveTo(r1[0], r1[1], r2[0], r2[1]);
        }
        function buildFern() {
          const x0 = 290, y0 = 40, w = 1020, h = 520, R = 2.5, W = w * R, H = h * R, r = mkRng(21), NZ = mkNoise2(77),
            main = mk(W, H), back = mk(W, H), gm = main.getContext("2d"), gb = back.getContext("2d");
          [gm, gb].forEach((g) => g.setTransform(R, 0, 0, R, -x0 * R, -y0 * R));
          const items = [];
          for (let i = 0; i < 42; i++) {
            const f = clamp((i + (r() - 0.5) * 0.8) / 41), gg = Math.abs(f - 0.5) * 2, side = f < 0.5 ? -1 : 1, dz = r(),
              a0 = -Math.PI / 2 + (f - 0.5) * 2 * 1.3 + (r() - 0.5) * 0.12,
              L = (230 + gg * 160) * (0.86 + r() * 0.2) * (0.9 + 0.12 * dz),
              droop = side * (0.2 + gg * 0.85 + dz * 0.12) * (0.8 + r() * 0.35),
              bx = 800 + (r() - 0.5) * 36, by = 498 + (r() - 0.5) * 4,
              cx = bx + Math.cos(a0) * L * 0.62, cy = by + Math.sin(a0) * L * 0.62,
              a1 = a0 + droop, tx = cx + Math.cos(a1) * L * 0.5, ty = cy + Math.sin(a1) * L * 0.5,
              leaf = new Path2D(), rib = new Path2D(), rach = new Path2D(), M = 30,
              maxPl = (46 + gg * 16) * (0.9 + r() * 0.2), tw = 0.62 + r() * 0.38;
            const P = (u) => { const om = 1 - u; return [om * om * bx + 2 * u * om * cx + u * u * tx, om * om * by + 2 * u * om * cy + u * u * ty]; },
              Dv = (u) => { const om = 1 - u; return [2 * om * (cx - bx) + 2 * u * (tx - cx), 2 * om * (cy - by) + 2 * u * (ty - cy)]; };
            for (let j = 0; j < M; j++) {
              const u = 0.08 + (0.9 * j) / (M - 1), [dx, dy] = Dv(u), ta = Math.atan2(dy, dx),
                base = maxPl * Math.pow(Math.sin(Math.PI * Math.min(0.98, u * 0.92 + 0.06)), 0.75) * (1.05 - u * 0.55);
              for (const s of [-1, 1]) {
                const pl = base * (s > 0 ? 1 : tw) * (0.92 + r() * 0.16), [qx, qy] = P(s > 0 ? u : u + 0.012);
                fernPinna(leaf, rib, qx, qy, ta + s * (1.02 - u * 0.32), pl, pl * 0.15, Math.max(3, Math.round(4 + pl / 7)), s * -0.06);
              }
            }
            const left = [], right = [];
            for (let k = 0; k <= 24; k++) {
              const u = k / 24, [px, py] = P(u), [dx, dy] = Dv(u), ln = Math.hypot(dx, dy) || 1, wd = (2.6 * (1 - u) + 0.4) / 2;
              left.push([px - (dy / ln) * wd, py + (dx / ln) * wd]);
              right.push([px + (dy / ln) * wd, py - (dx / ln) * wd]);
            }
            rach.moveTo(left[0][0], left[0][1]);
            left.forEach((p) => rach.lineTo(p[0], p[1]));
            right.reverse().forEach((p) => rach.lineTo(p[0], p[1]));
            rach.closePath();
            items.push({ dz, leaf, rib, rach, bx, by, tx, ty, lit: Math.max(0, Math.cos(a0 + droop * 0.5)) });
          }
          items.sort((a, b) => a.dz - b.dz);
          const SH = 10000;
          const drawFrond = (g, it, shadow, hazeAmt) => {
            if (shadow) {
              g.save();
              g.globalCompositeOperation = "source-atop";
              g.shadowColor = "rgba(6,16,3,.55)"; g.shadowBlur = 9; g.shadowOffsetX = SH * R - 5; g.shadowOffsetY = 7;
              g.translate(-SH, 0); g.fillStyle = "#000"; g.fill(it.leaf); g.fill(it.rach);
              g.restore();
            }
            const d = it.dz, lf = 1 + it.lit * 0.2, hz = [150, 165, 150],
              base = mixc(mixc([20, 36, 13], [40, 66, 22], d), hz, hazeAmt),
              mid = mixc(mixc([38, 62, 21], [80, 120, 37], d), hz, hazeAmt),
              tip = mixc(mixc([60, 90, 31], [146, 184, 68], d), hz, hazeAmt);
            g.fillStyle = lin(g, it.bx, it.by, it.tx, it.ty, [[0, rgb(base)], [0.45, rgb(mid, lf)], [1, rgb(tip, lf)]]);
            g.fill(it.leaf);
            g.strokeStyle = "rgba(16,30,8,.32)"; g.lineWidth = 0.32; g.stroke(it.leaf);
            g.strokeStyle = `rgba(212,238,152,${0.1 + 0.24 * d})`; g.lineWidth = 0.42; g.stroke(it.rib);
            g.fillStyle = lin(g, it.bx, it.by, it.tx, it.ty, [[0, "#4a3a22"], [0.25, "#4f6a2a"], [1, "#82a347"]]);
            g.fill(it.rach);
          };
          items.filter((it) => it.dz < 0.33).forEach((it) => drawFrond(gb, it, false, 0.12));
          gm.save(); gm.setTransform(1, 0, 0, 1, 0, 0); gm.filter = "blur(2.2px)"; gm.drawImage(back, 0, 0); gm.restore();
          // crown of scaly stipes
          gm.save(); gm.translate(800, 501); gm.scale(1, 0.3);
          const cg = gm.createRadialGradient(0, -6, 0, 0, 0, 62);
          cg.addColorStop(0, "#5a4a2c"); cg.addColorStop(0.6, "rgba(52,42,24,.8)"); cg.addColorStop(1, "rgba(40,32,18,0)");
          gm.fillStyle = cg; gm.beginPath(); gm.arc(0, 0, 62, 0, 6.283); gm.fill();
          gm.restore();
          items.filter((it) => it.dz >= 0.33).forEach((it) => drawFrond(gm, it, true, 0));
          // fiddleheads with fuzzy coils
          gm.lineCap = "round";
          [[772, -1, 452], [832, 1, 446]].forEach(([x, dir, yt]) => {
            const fid = new Path2D(), ccx = x + dir * 16, ccy = yt + 2;
            fid.moveTo(x, 500); fid.quadraticCurveTo(x - dir * 4, (500 + yt) / 2, x + dir * 6, yt + 10);
            for (let th = 0; th <= Math.PI * 3.6; th += 0.12) {
              const rad = 10 * (1 - th / (Math.PI * 4));
              fid.lineTo(ccx - dir * rad * Math.cos(th), ccy - rad * Math.sin(th));
            }
            gm.strokeStyle = "#3d5a22"; gm.lineWidth = 4; gm.stroke(fid);
            gm.strokeStyle = "#8db04e"; gm.lineWidth = 2.2; gm.stroke(fid);
            gm.save(); gm.translate(0.6, -0.6); gm.strokeStyle = "rgba(220,240,170,.5)"; gm.lineWidth = 0.6; gm.stroke(fid); gm.restore();
            gm.strokeStyle = "rgba(150,112,70,.55)"; gm.lineWidth = 0.35;
            for (let k = 0; k < 90; k++) {
              const an = r() * 6.283, rr = 3 + r() * 9;
              gm.beginPath(); gm.moveTo(ccx + Math.cos(an) * rr, ccy + Math.sin(an) * rr);
              gm.lineTo(ccx + Math.cos(an) * (rr + 1.6), ccy + Math.sin(an) * (rr + 1.6)); gm.stroke();
            }
          });
          // light: warm sun from upper right, occlusion at the crown, shade on low fronds
          gm.save();
          gm.globalCompositeOperation = "source-atop";
          gm.fillStyle = lin(gm, 1250, 60, 760, 520, [[0, "rgba(255,248,190,.24)"], [0.6, "rgba(255,248,190,0)"]]);
          gm.fillRect(x0, y0, w, h);
          const ao = gm.createRadialGradient(800, 505, 0, 800, 505, 210);
          ao.addColorStop(0, "rgba(6,16,3,.68)"); ao.addColorStop(1, "rgba(6,16,3,0)");
          gm.fillStyle = ao; gm.fillRect(x0, y0, w, h);
          gm.fillStyle = lin(gm, 0, 360, 0, 560, [[0, "rgba(8,18,5,0)"], [1, "rgba(8,18,5,.42)"]]);
          gm.fillRect(x0, y0, w, h);
          gm.restore();
          // fine leaf grain
          const id = gm.getImageData(0, 0, W, H), D = id.data;
          for (let py = 0; py < H; py++)
            for (let px = 0; px < W; px++) {
              const k = (py * W + px) * 4;
              if (!D[k + 3]) continue;
              const m = 0.86 + 0.28 * NZ(px * 0.07, py * 0.07, 2);
              D[k] *= m; D[k + 1] *= m; D[k + 2] *= m * 0.97;
            }
          gm.putImageData(id, 0, 0);
          return { z: 2.75, fade: fadeSolid, draw(g) { g.drawImage(main, x0, y0, w, h); } };
        }

        const FERN = buildFern();
        const LAYERS = [
          bake(buildFar(), 0, 250, 1600, 650, 1.25, 1.6), band(12, 445, 60, 0.45),
          bake(buildMid(), 0, 300, 1600, 600, 1.4, 1.0), band(8.6, 485, 55, 0.35),
          bake(buildNear(), 0, 380, 1600, 520, 2, 0.6), bake(buildMinis(), 0, 230, 1600, 260, 2, 0.8),
          band(5.4, 470, 90, 0.22), band(3.5, 500, 150, 0.8, "231,235,232", (d) => clamp((d - 0.02) / 0.9)),
          buildIsland(), FERN,
        ];
        // renders the scene at camera progress t (0..1) into a canvas, cover-fitted like object-fit: cover
        function renderScene(g, t, cw, ch, only) {
          const k = Math.max(cw / FW, ch / FH), ox = (cw - FW * k) / 2, oy = (ch - FH * k) / 2, c = t * ZEND;
          g.setTransform(1, 0, 0, 1, 0, 0); g.globalAlpha = 1;
          if (only) g.clearRect(0, 0, cw, ch);
          else { g.setTransform(k, 0, 0, k, ox, oy); drawSky(g); }
          g.imageSmoothingQuality = "high";
          for (const L of LAYERS) {
            if (only && L !== only) continue;
            const d = L.z - c, a = L.fade(d);
            if (a <= 0.002 || d <= 0) continue;
            const s = L.z / d;
            g.globalAlpha = a;
            g.setTransform(k * s, 0, 0, k * s, ox + k * VPX * (1 - s), oy + k * VPY * (1 - s));
            L.draw(g);
          }
          g.setTransform(1, 0, 0, 1, 0, 0); g.globalAlpha = 1;
        }

        /* ---------- floating rock sprites (same shader, rendered in px) ---------- */
        function rockArt(w, h, seed, sprig) {
          const c = islandShader({ cx: w / 2, cy: h * 0.3, rx: w * 0.42, back: h * 0.1, front: h * 0.075, depth: h * 0.56, seed, x0: 0, y0: 0, w, h, R: 1, fogAlpha: true }),
            g = c.getContext("2d"), r = mkRng(seed + 40);
          if (sprig) {
            g.lineCap = "round";
            for (let i = 0; i < 26; i++) {
              const bx = w / 2 + (r() - 0.5) * w * 0.5, by = c.mid(bx) + (r() - 0.3) * h * 0.04, l = h * (0.05 + r() * 0.1), lean = (r() - 0.5) * l * 1.1;
              g.strokeStyle = lin(g, bx, by, bx + lean, by - l, [[0, "#3c5a22"], [1, "#a6c65e"]]);
              g.lineWidth = w * (0.004 + r() * 0.004);
              g.beginPath(); g.moveTo(bx, by); g.quadraticCurveTo(bx + lean * 0.2, by - l * 0.6, bx + lean, by - l); g.stroke();
            }
          }
          return c.toDataURL("image/png");
        }
        /* ---------- solution card artwork ---------- */
        function forestArt(W, H, seed) {
          const c = mk(W, H), g = c.getContext("2d"), r = mkRng(seed), n2 = mkNoise2(seed),
            sw = (W / 5) | 0, sh = (H / 5) | 0, sc = mk(sw, sh), sg = sc.getContext("2d"), id = sg.createImageData(sw, sh);
          for (let y = 0; y < sh; y++)
            for (let x = 0; x < sw; x++) {
              const p = n2(x * 5 * 0.0035, y * 5 * 0.0035), q = n2(x * 0.09 + 40, y * 0.09 + 40, 3), i = (y * sw + x) * 4;
              let R, G, B;
              if (p > 0.66) { R = 36 + q * 34; G = 60 + q * 40; B = 64 + q * 36; }
              else if (p > 0.56) { R = 104 + q * 40; G = 92 + q * 30; B = 58 + q * 18; }
              else { R = 26 + q * 18; G = 46 + q * 22; B = 28 + q * 12; }
              id.data[i] = R; id.data[i + 1] = G; id.data[i + 2] = B; id.data[i + 3] = 255;
            }
          sg.putImageData(id, 0, 0);
          g.imageSmoothingEnabled = true; g.imageSmoothingQuality = "high";
          g.drawImage(sc, 0, 0, W, H);
          const pal = ["#2f5a2a", "#3b6a2f", "#2a4d27", "#4a7a34", "#5c8a3a", "#24432a", "#456f33"];
          for (let i = 0; i < 12000; i++) {
            const x = r() * W, y = r() * H, p = n2(x * 0.0035, y * 0.0035);
            if (p > 0.54 + r() * 0.03) continue;
            const rad = (6 + r() * 9) * (1 - Math.max(0, p - 0.45) * 3);
            const roll = r(), col = roll < 0.015 ? "#9cc24f" : roll < 0.025 ? "#a58a3e" : pal[(r() * pal.length) | 0];
            g.fillStyle = "rgba(8,18,10,.45)"; g.beginPath(); g.arc(x + rad * 0.35, y + rad * 0.4, rad, 0, 6.283); g.fill();
            g.fillStyle = col; g.beginPath(); g.arc(x, y, rad, 0, 6.283); g.fill();
            g.fillStyle = "rgba(255,255,225,.16)"; g.beginPath(); g.arc(x - rad * 0.3, y - rad * 0.35, rad * 0.5, 0, 6.283); g.fill();
          }
          const nC = mkNoise(seed + 9), creek = new Path2D();
          for (let x = -20; x <= W + 20; x += 18) {
            const y = H * 0.66 - x * 0.28 + 60 * Math.sin(x * 0.009) + 70 * (nC(x * 0.006, 3) - 0.5);
            x < 0 ? creek.moveTo(x, y) : creek.lineTo(x, y);
          }
          g.lineCap = "round"; g.lineJoin = "round";
          g.strokeStyle = "#3a3524"; g.lineWidth = 16; g.stroke(creek);
          g.strokeStyle = "#22383a"; g.lineWidth = 10; g.stroke(creek);
          g.strokeStyle = "rgba(170,200,195,.35)"; g.lineWidth = 3; g.stroke(creek);
          for (let i = 0; i < 4; i++) {
            const mx = r() * W, my = r() * H, mr = 220 + r() * 260, gr = g.createRadialGradient(mx, my, 0, mx, my, mr);
            gr.addColorStop(0, "rgba(235,240,236,.22)"); gr.addColorStop(1, "rgba(235,240,236,0)");
            g.fillStyle = gr; g.fillRect(0, 0, W, H);
          }
          return c.toDataURL("image/jpeg", 0.88);
        }
        function fieldsArt(W, H, seed) {
          const c = mk(W, H), g = c.getContext("2d"), r = mkRng(seed);
          g.fillStyle = "#55663f"; g.fillRect(0, 0, W, H);
          const pal = ["#7d9744", "#9fb257", "#c4b064", "#8b7848", "#5e7d39", "#b59e57", "#a8ba6a", "#6f8a3e"];
          g.save(); g.translate(W / 2, H / 2); g.rotate(-0.38);
          for (let gy = -7; gy <= 7; gy++)
            for (let gx = -7; gx <= 7; gx++) {
              const w = 170 + r() * 40, h = 118 + r() * 30, x = gx * 196 + (r() - 0.5) * 8 + (gy % 2) * 40, y = gy * 146;
              if (r() < 0.12) {
                g.fillStyle = "#2f4a2a"; g.fillRect(x, y, w, h);
                for (let k = 0; k < 110; k++) {
                  const px = x + r() * w, py = y + r() * h, rad = 5 + r() * 6;
                  g.fillStyle = "rgba(10,20,10,.4)"; g.beginPath(); g.arc(px + 2, py + 2, rad, 0, 6.283); g.fill();
                  g.fillStyle = ["#3b6a2f", "#2f5a2a", "#4a7a34"][k % 3]; g.beginPath(); g.arc(px, py, rad, 0, 6.283); g.fill();
                }
              } else {
                g.fillStyle = pal[(r() * pal.length) | 0]; g.fillRect(x, y, w, h);
                const vert = r() < 0.5, step = 5 + r() * 3;
                g.strokeStyle = "rgba(30,40,20,.22)"; g.lineWidth = 1.4; g.beginPath();
                if (vert) for (let k = x + step / 2; k < x + w; k += step) { g.moveTo(k, y + 2); g.lineTo(k, y + h - 2); }
                else for (let k = y + step / 2; k < y + h; k += step) { g.moveTo(x + 2, k); g.lineTo(x + w - 2, k); }
                g.stroke();
                g.fillStyle = lin(g, x, y, x + w, y + h, [[0, "rgba(255,255,230,.10)"], [1, "rgba(0,0,0,.12)"]]);
                g.fillRect(x, y, w, h);
              }
              g.strokeStyle = "rgba(38,54,30,.55)"; g.lineWidth = 3; g.strokeRect(x - 2, y - 2, w + 4, h + 4);
            }
          g.restore();
          const P = [[-40, H * 0.86], [W * 0.3, H * 0.62], [W * 0.55, H * 0.58], [W + 40, H * 0.18]];
          const road = new Path2D();
          road.moveTo(...P[0]); road.bezierCurveTo(...P[1], ...P[2], ...P[3]);
          g.lineCap = "round";
          g.strokeStyle = "#6f6b5e"; g.lineWidth = 34; g.stroke(road);
          g.strokeStyle = "#cfcbbd"; g.lineWidth = 26; g.stroke(road);
          g.setLineDash([16, 14]); g.strokeStyle = "#f2efe4"; g.lineWidth = 2; g.stroke(road); g.setLineDash([]);
          const bez = (t) => {
            const m = 1 - t;
            return [0, 1].map((k) => m * m * m * P[0][k] + 3 * m * m * t * P[1][k] + 3 * m * t * t * P[2][k] + t * t * t * P[3][k]);
          };
          [[0.18, -1, "#eef1ec"], [0.33, 1, "#c6f35c"], [0.52, -1, "#eef1ec"], [0.71, 1, "#e3e6df"], [0.86, -1, "#eef1ec"]].forEach(([t, lane, col]) => {
            const [x, y] = bez(t), [x2, y2] = bez(t + 0.005);
            g.save(); g.translate(x, y); g.rotate(Math.atan2(y2 - y, x2 - x)); g.translate(0, lane * 6);
            g.fillStyle = "rgba(0,0,0,.25)"; g.fillRect(-19, -3, 42, 10);
            g.fillStyle = col; g.fillRect(-21, -5, 32, 10);
            g.fillStyle = "#2b3a2f"; g.fillRect(13, -4.5, 8, 9);
            g.restore();
          });
          const hz = g.createRadialGradient(W * 0.8, H * 0.1, 0, W * 0.8, H * 0.1, W * 0.6);
          hz.addColorStop(0, "rgba(240,244,238,.3)"); hz.addColorStop(1, "rgba(240,244,238,0)");
          g.fillStyle = hz; g.fillRect(0, 0, W, H);
          return c.toDataURL("image/jpeg", 0.88);
        }

        /* =====================================================================
           ORIGINAL PAGE LOGIC (frame-cache from video replaced by live render)
           ===================================================================== */
        const story = $("#story"),
          stage = $(".stage"),
          cam = $("#cam"),
          camF = $("#camF"),
          plate = $("#plate"),
          canvas = $("#cv"),
          ctx = canvas.getContext("2d", { alpha: false }),
          fog = $("#fog"),
          layers = ["#L0", "#L1", "#L2", "#L3", "#L4"].map($),
          acctText =
            "Bryo's growth engine models every colony at the millimetre scale — predicting where moss will spread, what it needs next, and when to step in — so living surfaces take hold in weeks, not seasons.";
        $("#acct").innerHTML = acctText
          .split(/(\s+)/)
          .map((w) => (w.trim() ? `<span>${w}</span>` : w))
          .join("");

        // hero plate (frame 0) and the fern foreground cut-out
        (() => {
          const pc = mk(2400, 1350);
          renderScene(pc.getContext("2d"), 0, 2400, 1350);
          plate.src = pc.toDataURL("image/jpeg", 0.9);
          const fc = mk(2400, 1350), fg = fc.getContext("2d");
          renderScene(fg, 0, 2400, 1350, FERN);
          fg.globalCompositeOperation = "destination-in";
          fg.fillStyle = lin(fg, 0, 430 * 1.5, 0, 510 * 1.5, [[0, "#000"], [1, "rgba(0,0,0,0)"]]);
          fg.fillRect(0, 0, 2400, 1350);
          $("#fernImg").src = fc.toDataURL("image/png");
          $('[data-rock="1"]').src = rockArt(520, 590, 3, false);
          $('[data-rock="3"]').src = rockArt(530, 540, 9, true);
        })();
        setTimeout(() => {
          const art = { forest: forestArt(1400, 1000, 5), fields: fieldsArt(1400, 1000, 8) };
          $$(".card-bg").forEach((el) => (el.style.backgroundImage = `url("${art[el.dataset.art]}")`));
        }, 0);

        let W = innerWidth,
          H = innerHeight,
          sp = 0, sx = 0, sy = 0, mx = 0, my = 0,
          want = 0, shown = -1, rendered = -1, dirty = true,
          NF = 121, lastT = 0, statsStarted = false;
        function layoutCanvas() {
          W = innerWidth;
          H = innerHeight;
          const d = Math.min(devicePixelRatio || 1, 1.5);
          canvas.width = Math.round(canvas.clientWidth * d);
          canvas.height = Math.round(canvas.clientHeight * d);
          dirty = true;
        }
        function layoutHero() {
          const hero = $("#heroCopy"),
            line = hero.querySelector("h1"),
            W = innerWidth,
            H = innerHeight;
          if (W < 821) {
            hero.style.top = "";
            line.style.fontSize = "";
            return;
          }
          const bw = W * 1.06,
            bh = H * 1.12,
            k = Math.max(bw / 1600, bh / 900),
            fernTop = -0.09 * H + (bh - 900 * k) / 2 + 245 * k + 0.06 * H;
          let fs = Math.min(104, 72 * k);
          line.style.fontSize = fs + "px";
          if (line.scrollWidth > W * 0.86) {
            fs *= (W * 0.86) / line.scrollWidth;
            line.style.fontSize = fs + "px";
          }
          requestAnimationFrame(() => {
            const blockH = hero.offsetHeight;
            hero.style.top = fernTop + 0.5 * fs - blockH + "px";
          });
        }
        addEventListener("resize", () => {
          layoutCanvas();
          layoutHero();
        });
        document.fonts?.ready.then(layoutHero);
        layoutCanvas();
        layoutHero();
        function drawWant(vp) {
          if (dirty || Math.abs(vp - rendered) > 1e-5) {
            renderScene(ctx, vp, canvas.width, canvas.height);
            rendered = vp;
            dirty = false;
          }
          shown = want;
        }
        const rocks = $$(".rock");
        // hotspots and feature rows toggle one at a time; buttons for keyboard and screen readers
        const toggles = (sel) => {
          const all = $$(sel);
          all.forEach((el) => {
            el.tabIndex = 0;
            el.setAttribute("role", "button");
            el.setAttribute("aria-pressed", "false");
            el.addEventListener("click", () => {
              const on = !el.classList.contains("on");
              all.forEach((x) => {
                x.classList.toggle("on", x === el && on);
                x.setAttribute("aria-pressed", String(x === el && on));
              });
            });
            el.addEventListener("keydown", (e) => {
              if (e.key === "Enter" || e.key === " ") { e.preventDefault(); el.click(); }
            });
          });
        };
        toggles(".hotspot");
        toggles(".feat");
        $$(".sol-card").forEach((card) => {
          card.addEventListener("pointermove", (e) => {
            const r = card.getBoundingClientRect(),
              x = (e.clientX - r.left) / r.width - 0.5,
              y = (e.clientY - r.top) / r.height - 0.5;
            card.style.transform = `perspective(1000px) rotateY(${x * 6}deg) rotateX(${-y * 6}deg)`;
          });
          card.addEventListener("pointerleave", () => (card.style.transform = ""));
        });
        const statEls = $$(".stat strong");
        function startStats() {
          if (statsStarted) return;
          statsStarted = true;
          const start = performance.now();
          function tick(now) {
            const t = REDUCE ? 1 : ease(clamp((now - start) / 1600));
            statEls.forEach((el) => {
              const n = Number(el.dataset.count),
                v = n * t,
                d = Number(el.dataset.decimals || 0);
              el.textContent = el.dataset.format === "comma" ? Math.round(v).toLocaleString("en-US") : v.toFixed(d);
            });
            if (t < 1) requestAnimationFrame(tick);
          }
          requestAnimationFrame(tick);
        }
        function frame(now) {
          const dt = Math.min(64, now - (lastT || now));
          lastT = now;
          const rect = story.getBoundingClientRect(),
            p = clamp(-rect.top / (story.offsetHeight - innerHeight));
          sp += (p - sp) * (1 - Math.pow(0.86, dt / 16.7));
          if (Math.abs(p - sp) < 0.0002) sp = p;
          const vp = ease(seg(sp, 0.05, 0.7));
          want = Math.round(vp * (NF - 1));
          drawWant(vp);
          mx = pointerX / innerWidth - 0.5;
          my = pointerY / innerHeight - 0.5;
          sx += (mx - sx) * 0.06;
          sy += (my - sy) * 0.06;
          const camTransform = `translate3d(${-sx * 18}px,${-sy * 12 + (1 - vp) * innerHeight * 0.06}px,0) scale(${1 + 0.02 * (1 - vp)})`;
          cam.style.transform = camTransform;
          camF.style.transform = camTransform;
          const ho = shown < 0 ? 0 : shown === 0 ? seg(sp, 0.06, 0.105) : 1;
          plate.style.opacity = 1 - ho;
          camF.style.opacity = 1 - ho;
          camF.style.visibility = ho < 1 ? "visible" : "hidden";
          plate.style.visibility = ho < 1 ? "visible" : "hidden";
          const h = seg(sp, 0.02, 0.1),
            hero = $("#heroCopy");
          hero.style.transform = `translate3d(${-sx * 10}px,${-h * 80 - sy * 6}px,0) scale(${1 + h * 0.12})`;
          hero.style.filter = `blur(${h * 14}px)`;
          hero.style.opacity = 1 - h;
          layers[0].style.visibility = h >= 1 ? "hidden" : "visible";
          $("#hud").style.transform = `translate3d(${sx * 26}px,${sy * 18 - h * 40}px,0)`;
          $("#hud").style.opacity = 1 - seg(sp, 0.02, 0.08);
          $("#caption").style.opacity = 1 - seg(sp, 0.01, 0.05);
          $("#hint").style.opacity = 1 - seg(sp, 0.01, 0.05);
          layers[1].style.visibility = h >= 1 ? "hidden" : "visible";
          const vIn = seg(sp, 0.16, 0.27),
            vOut = seg(sp, 0.34, 0.42),
            vision = $("#vision"),
            words = vision.querySelectorAll("h2 span");
          words.forEach((w, i) => {
            const k = clamp(vIn * 1.6 - i * 0.08);
            w.style.transform = `translate3d(0,${(1 - k) * 30 - vOut * 60}px,0)`;
            w.style.filter = `blur(${(1 - k) * 12 + vOut * 14}px)`;
            w.style.opacity = k * (1 - vOut);
          });
          const vOpacity = clamp(vIn * 2 - 0.6) * (1 - vOut);
          vision.querySelector(".chip").style.opacity = vOpacity;
          vision.querySelector("p").style.opacity = vOpacity;
          vision.querySelector(".chip").style.transform = `translateY(${-vOut * 50}px)`;
          vision.querySelector("p").style.transform = `translateY(${-vOut * 50}px)`;
          layers[2].style.visibility = vOpacity > 0 ? "visible" : "hidden";
          const fg = ease(seg(sp, 0.38, 0.47));
          fog.style.visibility = fg > 0 ? "visible" : "hidden";
          fog.style.opacity = fg;
          fog.style.transform = `translate3d(${(fg - 1) * 18 + sx * -10}vw,${sy * -6}px,0)`;
          const aIn = seg(sp, 0.45, 0.55),
            aOut = seg(sp, 0.63, 0.68),
            acct = $$("#acct span");
          acct.forEach((w, i) => {
            const k = clamp(aIn * 2.2 - (i / acct.length) * 1.2);
            w.style.opacity = (0.15 + 0.85 * k) * (1 - aOut);
            w.style.filter = `blur(${(1 - k) * 6 + aOut * 10}px)`;
          });
          $$(".hotspot").forEach((hot, i) => {
            const k = seg(sp, 0.49 + i * 0.02, 0.53 + i * 0.02);
            hot.style.transform = `translate3d(${-sx * 30}px,${-sy * 20}px,0) scale(${k * (1 - aOut)})`;
            hot.style.visibility = k * (1 - aOut) > 0 ? "visible" : "hidden";
          });
          layers[3].style.visibility = aIn > 0 && aOut < 1 ? "visible" : "hidden";
          const sIn = seg(sp, 0.72, 0.82),
            cred = $("#cred");
          cred.style.opacity = sIn;
          cred.style.transform = `translateY(${(1 - sIn) * 30}px)`;
          cred.style.filter = `blur(${(1 - sIn) * 8}px)`;
          const cIn = ease(seg(sp, 0.74, 0.86)),
            carbon = $("#carbon");
          carbon.style.opacity = cIn;
          carbon.style.transform = `translate3d(${-sx * 14}px,${(1 - cIn) * 60 + sy * -10}px,0) rotateY(${sx * 8}deg) rotateX(${-sy * 8}deg)`;
          $("#carbonNum").textContent = Math.round(86 * seg(sp, 0.76, 0.9));
          const dash = 1 - seg(sp, 0.77, 0.92);
          $("#sparkline").style.strokeDashoffset = 260 * dash;
          $$(".feat").forEach((f, i) => {
            const k = ease(seg(sp, 0.76 + i * 0.025, 0.82 + i * 0.025));
            f.style.opacity = k;
            f.style.transform = `translateX(${(1 - k) * 40}px)`;
          });
          layers[4].style.visibility = sIn > 0 ? "visible" : "hidden";
          $("#progress").style.transform = `scaleX(${sp})`;
          rocks.forEach((r) => {
            const fp = seg(sp, 0.02, 0.2),
              fe = fp * fp,
              x = Number(r.dataset.x),
              y = Number(r.dataset.y),
              d = Number(r.dataset.d);
            r.style.transform = `translate3d(${x * fp * 70 - sx * 24 * d}vw,${y * fp * 60 - sy * 16 * d}vh,0) scale(${1 + fe * 1.6 * d})`;
            r.style.filter = `blur(${fe * 5 * d}px)`;
            r.style.opacity = fp >= 1 ? 0 : 1;
          });
          const solTop = $("#sol").getBoundingClientRect().top;
          if (solTop < innerHeight * 0.6) startStats();
          requestAnimationFrame(frame);
        }
        let pointerX = innerWidth / 2,
          pointerY = innerHeight / 2;
        if (!REDUCE)
          addEventListener(
            "pointermove",
            (e) => {
              pointerX = e.clientX;
              pointerY = e.clientY;
            },
            { passive: true },
          );
        requestAnimationFrame(frame);
      })();
    </script>
    <script>
      /* reveal-on-scroll + live moss growth simulation (pure code) */
      (() => {
        const io = new IntersectionObserver(
          (es) => es.forEach((e) => e.isIntersecting && (e.target.classList.add("in"), io.unobserve(e.target))),
          { threshold: 0.15 },
        );
        document.querySelectorAll(".rv").forEach((el) => io.observe(el));

        const cv = document.getElementById("grow");
        if (!cv) return;
        const g = cv.getContext("2d"), W = 300, H = 219, off = document.createElement("canvas");
        off.width = W; off.height = H;
        const og = off.getContext("2d"), img = og.createImageData(W, H), D = img.data;
        let a = 1234;
        const rnd = () => {
          a |= 0; a = (a + 0x6d2b79f5) | 0;
          let t = Math.imul(a ^ (a >>> 15), 1 | a);
          t = (t + Math.imul(t ^ (t >>> 7), 61 | t)) ^ t;
          return ((t ^ (t >>> 14)) >>> 0) / 4294967296;
        };
        const T = new Float32Array(65536);
        for (let i = 0; i < 65536; i++) T[i] = rnd();
        const at = (x, y) => T[((y & 255) << 8) | (x & 255)];
        const vn = (x, y) => {
          const xi = Math.floor(x), yi = Math.floor(y), xf = x - xi, yf = y - yi, u = xf * xf * (3 - 2 * xf), v = yf * yf * (3 - 2 * yf),
            p = at(xi, yi), q = at(xi + 1, yi), r = at(xi, yi + 1), s = at(xi + 1, yi + 1);
          return p + (q - p) * u + (r - p) * v + (p - q - r + s) * u * v;
        };
        const fbm = (x, y, o) => { let s = 0, am = 0.5, f = 1, nm = 0; for (let k = 0; k < o; k++) { s += vn(x * f + k * 31, y * f + k * 17) * am; nm += am; am *= 0.5; f *= 2.03; } return s / nm; };
        const seeds = [[62, 58], [214, 146], [128, 176], [238, 46], [36, 168]];
        const F = new Float32Array(W * H), HM = new Float32Array(W * H), ST = new Float32Array(W * H);
        let mn = 9, mx = -9;
        for (let y = 0; y < H; y++)
          for (let x = 0; x < W; x++) {
            let d = 9;
            seeds.forEach(([sx, sy], k) => (d = Math.min(d, Math.hypot(x - sx, y - sy) / (150 + k * 12))));
            const i = y * W + x, f = d * 0.8 + fbm(x * 0.035, y * 0.035, 4) * 0.55;
            F[i] = f; mn = Math.min(mn, f); mx = Math.max(mx, f);
            HM[i] = 0.55 * fbm(x * 0.09, y * 0.09, 3) + 0.45 * fbm(x * 0.35, y * 0.35, 2);
            ST[i] = fbm(x * 0.02 + 40, y * 0.05, 4);
          }
        for (let i = 0; i < W * H; i++) F[i] = (F[i] - mn) / (mx - mn);
        const mix = (p, q, t) => p + (q - p) * t, sm = (e0, e1, x) => { const t = Math.max(0, Math.min(1, (x - e0) / (e1 - e0))); return t * t * (3 - 2 * t); };
        let vis = false, t0 = performance.now();
        new IntersectionObserver((es) => (vis = es[0].isIntersecting)).observe(cv);
        const vDay = document.getElementById("vDay"), vCov = document.getElementById("vCov"), vHum = document.getElementById("vHum"), vMist = document.getElementById("vMist");
        const REDUCE = matchMedia("(prefers-reduced-motion: reduce)").matches;
        let still = false;
        function draw(now) {
          if (!still) requestAnimationFrame(draw);
          if (!vis) { t0 = now - (t0 ? 0 : 0); return; }
          if (REDUCE) still = true;
          const cyc = 12000, p = REDUCE ? 0.8 : ((now - t0) % cyc) / cyc, gr = sm(0, 0.8, p), thr = gr * 1.04;
          let cov = 0;
          for (let y = 1; y < H - 1; y++)
            for (let x = 1; x < W - 1; x++) {
              const i = y * W + x, k = i * 4, f = F[i], h = HM[i], st = ST[i];
              const sx = (ST[i + 1] - ST[i - 1]) * 30, sy = (ST[i + W] - ST[i - W]) * 30, sl = 0.75 + Math.max(-0.3, Math.min(0.35, sx - sy));
              let r = mix(78, 140, st) * sl, gg = mix(80, 140, st) * sl, b = mix(74, 128, st) * sl;
              const e = sm(0, 0.05, thr - f);
              if (e > 0) {
                const hx = (HM[i + 1] - HM[i - 1]) * 9, hy = (HM[i + W] - HM[i - W]) * 9,
                  li = Math.max(0.25, Math.min(1.35, 0.8 + hx - hy)) * (0.5 + 0.5 * sm(0.25, 0.7, h)),
                  young = sm(0.06, 0, thr - f), mr = mix(mix(46, 120, h), 176, young * 0.6), mg = mix(mix(70, 160, h), 200, young * 0.5), mb = mix(mix(26, 52, h), 80, young * 0.4);
                r = mix(r, mr * li, e); gg = mix(gg, mg * li, e); b = mix(b, mb * li, e);
                if (e > 0.5) cov++;
              }
              D[k] = r; D[k + 1] = gg; D[k + 2] = b; D[k + 3] = 255;
            }
          og.putImageData(img, 0, 0);
          const cw = cv.width, ch = cv.height, s = cw / W;
          g.imageSmoothingEnabled = true; g.imageSmoothingQuality = "high";
          g.drawImage(off, 1, 1, W - 2, H - 2, 0, 0, cw, ch);
          // AI overlay: scan line + colony detection boxes
          const sy = ((now / 14) % (ch + 80)) - 40;
          const sg = g.createLinearGradient(0, sy - 40, 0, sy);
          sg.addColorStop(0, "rgba(198,243,92,0)"); sg.addColorStop(1, "rgba(198,243,92,.18)");
          g.fillStyle = sg; g.fillRect(0, sy - 40, cw, 40);
          g.fillStyle = "rgba(198,243,92,.9)"; g.fillRect(0, sy, cw, 2);
          g.font = "500 18px 'JetBrains Mono', monospace";
          seeds.forEach(([x, y], k) => {
            const rad = Math.max(0, gr * 1.04 - 0.02 - k * 0.04) * (150 + k * 12) * 0.62 * s;
            if (rad < 14) return;
            const bx = Math.max(4, x * s - rad), by = Math.max(4, y * s - rad), bw = Math.min(cw - 4, x * s + rad) - bx, bh = Math.min(ch - 4, y * s + rad) - by;
            g.strokeStyle = "rgba(198,243,92,.85)"; g.lineWidth = 2; g.setLineDash([10, 6]); g.strokeRect(bx, by, bw, bh); g.setLineDash([]);
            const label = `COLONY 0${k + 1} · ${Math.min(99, Math.round(60 + gr * 39 - k * 3))}%`, tw = g.measureText(label).width;
            g.fillStyle = "#c6f35c"; g.fillRect(bx, by, tw + 16, 30);
            g.fillStyle = "#10291a"; g.fillText(label, bx + 8, by + 21);
          });
          vDay.textContent = "Day " + Math.round(gr * 84);
          vCov.textContent = Math.round((cov / (W * H)) * 100) + "%";
          vHum.textContent = 90 + Math.round(3 * Math.sin(now / 1300)) + "%";
          vMist.textContent = 14 - (Math.floor(now / 700) % 15) + " min";
        }
        requestAnimationFrame(draw);
      })();
    </script>
  </body>
</html>
```
