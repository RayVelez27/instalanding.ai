INSTALANDING.AI · Event Horizon Orbital Page

The page below is the build. Use it as the starting point, not as inspiration:
- Keep its layout, design values (colours, type, spacing, radii) and motion exactly as they are.
- Replace the fictional brand, copy, names and numbers with mine.
- If I name a stack (React, Next.js, Vue, Svelte, Astro...), convert it faithfully to that stack;
  otherwise ship it as this one HTML file.
- Read the MAP and ADAPTING notes in its header comment before you edit.
- Check it in a real browser: no console errors, no horizontal scroll at 390px, reduced motion respected.

Credit: keep this line as a comment at the top of the file you produce:
Event Horizon Orbital Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/event-horizon-orbital-page

halcyon-orbital.html:
```html
<!doctype html>
<!--
  INSTALANDING.AI · Event Horizon Orbital Page
  slug     event-horizon-orbital-page
  prompt   https://instalanding.ai/p/event-horizon-orbital-page.txt   (the one-shot brief this file was built from)
  page     https://instalanding.ai/prompt/event-horizon-orbital-page
  license  MIT. Fictional brand ("Halcyon Orbital"); replace names, figures, fleet and contact details before shipping.

  MAP
  tokens    :root at the top of <style>: --ink #efebe2 / --soft / --dim / --faint warm greys on #000, hairlines
            --line and --line-strong, --amber #ffb45e (+ --amber-line, --amber-soft), --ice #a9caff for fault and
            secondary readouts, glass fills --glass/--glass-strong and --blur. Fonts: Archivo (copy, h1),
            Archivo Narrow (h2/h3 display), JetBrains Mono (labels, HUD), all from Google Fonts.
  sections  nav, hero, stats, services, process, coverage, fleet, cta (the footer: intake form + map)
  panels    every card shares one "signature glass" rule near the end of <style>: warm mesh gradient fill,
            inset glow, and a ::before gradient border with an amber light sweeping round it (--giro, @property).
  scripts   three.js r128 (cdnjs), then:
            1. page UI: nav state + the #velo veil that frosts the 3D scene below the hero, reveal + count-ups,
               simulated telemetry, nav section highlight, the LEO/MEO/GEO radar, footer wordmark fit, the form.
            2. the black hole: a full-screen fragment shader that ray-marches light around a Schwarzschild-like
               hole (bent rays, a volumetric accretion disc with Doppler beaming, a starfield and gas behind),
               then bright-pass, two-pass blur bloom and an ACES composite. Drag to orbit, double-click to reset,
               page scroll pulls the camera in. Quality drops a tier if it runs under ~28 fps.
            3. card "vitrines": nine small three.js scenes (three fleet spacecraft, six service animations)
               drawn by ONE shared WebGL renderer and copied into a 2D canvas per card, only while on screen.
  assets    none: every texture is drawn on canvas at load; the SVGs are inline fallbacks shown without WebGL.

  ADAPTING
  - The hero copy sits on scrims (.hero::before) tuned to keep the left column readable over the bright disc;
    if you move the copy right, move the scrim with it.
  - Shader constants live in FRAG_SIM: rIn/rOut (disc radii), uTemp (inner colour), uVel (spin), uDoppler.
    The step budget per tier is in `calidades`; more steps = sharper lensing, slower frames.
  - A card scene is chosen by data-vitrina on its container; add a factory to FABRICAS for a new one. HUD
    readouts bind by data-k, written by it.hud(key, value) from the scene's tick.
  - Under prefers-reduced-motion the panel sweeps, ticker, radar and pulses stop, the hole stops orbiting and
    its disc freezes, and each card scene renders one still frame at its showcase moment.
  - #error is a diagnostics overlay that shows only if three.js, WebGL or a shader fails.
-->
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Halcyon Orbital — Satellite Servicing & Life Extension</title>
<meta name="description" content="Inspection, refuelling, robotic repair, relocation and end-of-life disposal for satellites from LEO to GEO.">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Archivo+Narrow:wght@500;700&family=Archivo:wght@300;400;500;700;800&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
<style>
:root{
	--ink:#efebe2;
	--soft:#d4cfc4;
	--dim:#a39e92;
	--faint:#6e6a61;
	--line:rgba(239,235,226,.14);
	--line-strong:rgba(239,235,226,.30);
	--amber:#ffb45e;
	--amber-line:rgba(255,180,94,.55);
	--amber-soft:rgba(255,180,94,.12);
	--ice:#a9caff;
	--glass:rgba(10,10,13,.78);
	--glass-strong:rgba(8,8,11,.88);
	--blur:blur(22px) saturate(1.2);
	--mono:"JetBrains Mono","Courier New",ui-monospace,monospace;
	--sans:"Archivo",system-ui,-apple-system,"Segoe UI",sans-serif;
	--display:"Archivo Narrow","Arial Narrow","Helvetica Neue",Arial,sans-serif;
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
html,body{background:#000}
body{font-family:var(--sans);color:var(--ink);overflow-x:hidden;-webkit-font-smoothing:antialiased}
a{color:inherit}
::selection{background:var(--amber);color:#000}

/* ---------- WebGL backdrop ---------- */
#escena3d{position:fixed;inset:0;display:block;width:100vw;height:100vh;z-index:0;touch-action:pan-y;cursor:grab}
#escena3d:active{cursor:grabbing}
/* veil that fades in below the hero: darkens and frosts the 3D scene so copy stays readable */
#velo{position:fixed;inset:0;z-index:1;pointer-events:none;opacity:0;
	background:radial-gradient(ellipse at 50% 45%,rgba(4,4,6,.62),rgba(2,2,3,.9));
	-webkit-backdrop-filter:blur(10px);backdrop-filter:blur(10px)}

/* ---------- Nav ---------- */
nav{position:fixed;top:0;left:0;right:0;z-index:30;display:grid;grid-template-columns:1fr auto 1fr;align-items:center;
	padding:20px 36px;transition:background .3s,border-color .3s;border-bottom:1px solid transparent}
nav.solido{background:rgba(4,4,6,.82);-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur);border-color:var(--line)}
.marca{display:flex;align-items:center;gap:16px;text-decoration:none;justify-self:start}
.marca svg{width:44px;height:30px}
.marca span{font-family:var(--mono);font-size:14px;letter-spacing:.5em;text-transform:uppercase;font-weight:500}
.marca small{display:block;font-size:9px;letter-spacing:.32em;color:var(--dim);margin-top:5px;font-weight:400}
.nav-centro{position:relative;padding:10px 34px}
.nav-centro::before,.nav-centro::after{content:"";position:absolute;top:0;bottom:0;width:8px;border:1px solid var(--amber-line)}
.nav-centro::before{left:0;border-right:none}
.nav-centro::after{right:0;border-left:none}
nav ul{display:flex;gap:38px;list-style:none;font-family:var(--mono);font-size:12px;letter-spacing:.18em;text-transform:uppercase}
nav ul a{position:relative;text-decoration:none;color:var(--soft);transition:color .2s}
nav ul a:hover,nav ul a.activo{color:var(--ink)}
nav ul a.activo::before{content:"";position:absolute;left:-16px;top:50%;width:6px;height:6px;margin-top:-3px;border-radius:50%;
	background:var(--amber);box-shadow:0 0 10px var(--amber)}
nav > .btn{justify-self:end}

.btn{display:inline-flex;align-items:center;justify-content:center;gap:16px;font-family:var(--mono);font-size:12px;letter-spacing:.18em;
	font-weight:500;text-transform:uppercase;text-decoration:none;padding:15px 22px;border:1px solid var(--amber);color:var(--amber);
	background:rgba(0,0,0,.25);cursor:pointer;transition:background .2s,color .2s,border-color .2s}
.btn svg{width:12px;height:12px;flex:none;stroke:currentColor;fill:none;stroke-width:1.6}
.btn:hover{background:var(--amber);color:#000}
.btn.lleno{background:var(--amber);color:#0b0906;box-shadow:0 0 34px rgba(255,180,94,.28)}
.btn.lleno:hover{background:#ffc684}
.btn.fantasma{border-color:var(--line-strong);color:var(--ink);background:rgba(0,0,0,.35);-webkit-backdrop-filter:blur(6px);backdrop-filter:blur(6px)}
.btn.fantasma:hover{background:var(--ink);color:#000;border-color:var(--ink)}
.btn.fantasma svg.barras{fill:currentColor;stroke:none;width:14px;height:12px}
.btn:focus-visible,nav a:focus-visible,button:focus-visible{outline:1px solid var(--ink);outline-offset:3px}

/* ---------- Hero ---------- */
main{position:relative;z-index:2}
.hero{position:relative;min-height:100vh;min-height:100svh;pointer-events:none;
	display:flex;flex-direction:column;justify-content:center;padding:130px 56px 150px}
/* scrims: keep the left column and bottom bar readable without dimming the black hole */
.hero::before{content:"";position:absolute;inset:0;z-index:0;pointer-events:none;
	background:
		linear-gradient(90deg,rgba(0,0,0,.78) 0%,rgba(0,0,0,.5) 26%,rgba(0,0,0,0) 48%),
		linear-gradient(180deg,rgba(0,0,0,.55) 0%,rgba(0,0,0,0) 16%);
	/* fade the whole scrim out toward the bottom so it never ends on a hard edge */
	-webkit-mask-image:linear-gradient(180deg,#000 0%,#000 55%,transparent 100%);
	mask-image:linear-gradient(180deg,#000 0%,#000 55%,transparent 100%)}
/* soft dissolve that straddles the hero's bottom edge, plus a faint amber "horizon" glow */
.hero::after{content:"";position:absolute;left:0;right:0;bottom:-28vh;height:56vh;z-index:0;pointer-events:none;
	background:
		radial-gradient(ellipse 55% 45% at 50% 50%,rgba(255,170,80,.07),transparent 70%),
		linear-gradient(180deg,rgba(2,2,4,0) 0%,rgba(2,2,4,.38) 48%,rgba(2,2,4,0) 100%)}
.hero > *{position:relative;z-index:1}
.hero .interactivo{pointer-events:auto}

.hero-copia{max-width:640px}
.ceja{display:flex;align-items:center;gap:14px;font-family:var(--mono);font-size:13px;letter-spacing:.3em;text-transform:uppercase;margin-bottom:30px}
.ceja .c{color:var(--amber)}
.ceja em{font-style:normal;color:var(--amber)}
.ceja::after{content:"";width:54px;height:1px;background:var(--line-strong);margin-left:6px}
h1{font-family:var(--sans);font-weight:800;font-size:clamp(46px,5.9vw,98px);line-height:.94;letter-spacing:-.03em;text-transform:uppercase;
	text-shadow:0 4px 40px rgba(0,0,0,.55)}
h1 em{font-style:normal;color:var(--amber);text-shadow:0 0 50px rgba(255,180,94,.25)}
.hero-copia p{margin-top:30px;font-size:19px;line-height:1.55;color:var(--ink);font-weight:300;max-width:480px;text-shadow:0 2px 18px rgba(0,0,0,.8)}
.hero-ctas{display:flex;gap:26px;margin-top:42px;flex-wrap:wrap}
.hero-ctas .btn{padding:19px 28px;min-width:250px}
.rasgos{display:flex;margin-top:48px;font-family:var(--mono);font-size:11px;letter-spacing:.18em;text-transform:uppercase;line-height:2}
.rasgos div{padding:0 46px;border-left:1px solid var(--amber-line)}
.rasgos div:first-child{padding-left:0;border-left:none}
.rasgos strong{display:block;font-weight:500;color:var(--ink)}
.rasgos span{display:block;color:var(--dim)}

#datos{position:absolute;right:36px;top:112px;text-align:right;font-family:var(--mono);font-size:11px;
	letter-spacing:.12em;color:var(--dim);text-transform:uppercase;line-height:2.1;text-shadow:0 1px 10px rgba(0,0,0,.9)}
#datos b{color:var(--amber);font-weight:400;text-transform:none}
#datos .t{color:var(--ink);letter-spacing:.24em;font-size:12px;font-weight:500;margin-bottom:10px;display:block}

/* orbit radar */
.radar{position:absolute;right:36px;bottom:118px;display:flex;align-items:center;gap:26px}
.radar ul{list-style:none;font-family:var(--mono);font-size:12px;letter-spacing:.2em}
.radar li{display:flex;align-items:center;justify-content:flex-end;gap:14px;color:var(--dim);padding:13px 0;transition:color .4s;cursor:default}
.radar li::after{content:"";width:24px;height:1px;background:var(--line-strong);transition:all .4s}
.radar li.on{color:var(--ink)}
.radar li.on::after{background:var(--amber);height:2px;box-shadow:0 0 8px var(--amber)}
.radar svg{width:200px;height:200px;overflow:visible}
.radar .anillo{fill:none;stroke:rgba(239,235,226,.22);stroke-width:1;transition:stroke .4s}
.radar .anillo.on{stroke:rgba(255,180,94,.75)}
.radar .giro{transform-box:view-box;transform-origin:100px 100px;animation:girar linear infinite}
.radar .g1{animation-duration:9s}
.radar .g2{animation-duration:18s}
.radar .g3{animation-duration:32s}
@keyframes girar{to{transform:rotate(360deg)}}

/* bottom bar */
.pie-hero{position:absolute;left:36px;right:36px;bottom:28px;display:flex;justify-content:space-between;align-items:flex-end;gap:20px}
.estado-sis{display:flex;align-items:center;gap:22px;font-family:var(--mono);font-size:11px;letter-spacing:.18em;text-transform:uppercase}
.estado-sis .caja{display:flex;align-items:center;gap:14px;padding:13px 22px;border:1px solid var(--line-strong);color:var(--amber);background:rgba(0,0,0,.4)}
.estado-sis .caja::before{content:"";width:7px;height:7px;border-radius:50%;background:var(--amber);box-shadow:0 0 10px var(--amber);animation:pulso 2s infinite}
.estado-sis .lema{color:var(--dim)}
.estado-sis .lema::before{content:"|";margin-right:16px;color:var(--faint)}
.estado-sis .lema::after{content:"//";margin-left:16px;color:var(--faint)}
@keyframes pulso{50%{opacity:.3}}

.bajar{position:absolute;left:50%;bottom:28px;transform:translateX(-50%);font-family:var(--mono);font-size:12px;
	letter-spacing:.24em;color:var(--soft);text-transform:uppercase;text-decoration:none;display:flex;flex-direction:column;align-items:center;gap:12px}
.bajar i{width:1px;height:44px;background:linear-gradient(var(--amber),transparent);animation:caer 2.2s infinite}
@keyframes caer{0%{transform:scaleY(0);transform-origin:top}50%{transform:scaleY(1);transform-origin:top}51%{transform-origin:bottom}100%{transform:scaleY(0);transform-origin:bottom}}


/* optics console (popover) */
#panel{position:absolute;right:36px;bottom:92px;width:270px;display:none;background:var(--glass-strong);
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur);border:1px solid var(--line-strong);
	font-family:var(--mono);font-size:11px;letter-spacing:.08em;padding:14px 18px 6px;z-index:5}
#panel.abierto{display:block}
#panel .titulo{font-size:10px;letter-spacing:.24em;text-transform:uppercase;color:var(--ink);padding-bottom:12px;margin-bottom:12px;border-bottom:1px solid var(--line)}
#panel .fila{margin-bottom:12px}
#panel label{display:flex;justify-content:space-between;color:var(--dim);text-transform:uppercase;margin-bottom:6px}
#panel label b{color:var(--ink);font-weight:normal}
input[type=range]{-webkit-appearance:none;appearance:none;width:100%;height:2px;background:var(--line-strong);outline:none}
input[type=range]::-webkit-slider-thumb{-webkit-appearance:none;appearance:none;width:11px;height:11px;background:var(--amber);border-radius:50%;cursor:pointer}
input[type=range]::-moz-range-thumb{width:11px;height:11px;background:var(--amber);border:none;border-radius:50%;cursor:pointer}
#panel .toggles{display:flex;gap:6px;margin-top:2px}
#panel .toggles button{flex:1;background:none;border:1px solid var(--line);color:var(--dim);font-family:inherit;font-size:10px;
	letter-spacing:.1em;padding:6px 0;cursor:pointer;text-transform:uppercase;transition:all .2s}
#panel .toggles button.on{color:var(--amber);border-color:var(--amber)}
#panel .etiqueta{color:var(--dim);text-transform:uppercase;font-size:10px;letter-spacing:.14em;margin:8px 0 6px}

/* ---------- Ticker ---------- */
.cinta{border-top:1px solid var(--line);border-bottom:1px solid var(--line);background:var(--glass-strong);
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur);overflow:hidden;font-family:var(--mono);font-size:11px;letter-spacing:.2em;text-transform:uppercase;color:var(--soft)}
.cinta .pista{display:flex;width:max-content;animation:desfile 48s linear infinite}
.cinta span{padding:16px 32px;white-space:nowrap}
.cinta b{color:var(--amber);font-weight:normal}
@keyframes desfile{to{transform:translateX(-50%)}}

/* ---------- Sections ---------- */
section{position:relative;padding:120px 36px}
.envoltura{max-width:1180px;margin:0 auto}
/* section intros sit on a frosted plate so headings never fight the 3D scene */
.cabecera{display:inline-block;max-width:820px;padding:34px 38px 36px;background:var(--glass);border:1px solid var(--line);
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur)}
.rotulo{font-family:var(--mono);font-size:11px;letter-spacing:.3em;text-transform:uppercase;color:var(--amber);margin-bottom:18px;display:flex;gap:14px}
.rotulo span{color:var(--faint)}
h2{font-family:var(--display);font-weight:700;font-size:clamp(32px,4.4vw,58px);line-height:.98;text-transform:uppercase;max-width:760px}
.intro{margin-top:18px;max-width:600px;color:var(--soft);line-height:1.7;font-weight:300;font-size:16px}

.cifras{display:grid;grid-template-columns:repeat(4,1fr);border:1px solid var(--line);background:var(--glass);-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur)}
.cifras div{padding:34px 26px;border-right:1px solid var(--line)}
.cifras div:last-child{border-right:none}
.cifras strong{display:block;font-family:var(--display);font-size:clamp(34px,4vw,54px);font-weight:700;line-height:1}
.cifras strong b{font-weight:700}
.cifras strong sup{font-size:.42em;color:var(--amber);vertical-align:top;margin-left:4px}
.cifras span{display:block;margin-top:10px;font-family:var(--mono);font-size:10px;letter-spacing:.18em;text-transform:uppercase;color:var(--dim)}

.servicios{display:grid;grid-template-columns:repeat(3,1fr);gap:1px;background:var(--line);border:1px solid var(--line);margin-top:40px;
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur)}
.servicio{background:var(--glass-strong);padding:34px 28px 30px;position:relative;transition:background .3s}
.servicio:hover{background:rgba(26,18,10,.92)}
.servicio::after{content:"";position:absolute;left:0;top:0;height:2px;width:0;background:var(--amber);transition:width .4s}
.servicio:hover::after{width:100%}
.servicio .escena{position:relative;height:214px;margin:-33px -27px 26px;border-radius:15px 15px 0 0;overflow:hidden;
	display:grid;place-items:center;border-bottom:1px solid rgba(255,240,220,.12);
	background:radial-gradient(ellipse 70% 65% at 50% 52%,rgba(255,170,80,.12),transparent 72%),linear-gradient(180deg,rgba(0,0,0,.42),rgba(0,0,0,.08))}
.servicio .escena svg.respaldo{width:54px;height:54px;stroke:var(--amber);fill:none;stroke-width:1.2}
.servicio h3{font-family:var(--display);font-size:23px;text-transform:uppercase;letter-spacing:.02em;margin-bottom:10px}
.servicio p{font-size:15px;line-height:1.65;color:var(--soft);font-weight:300}
.servicio .tag{display:inline-block;margin-top:18px;font-family:var(--mono);font-size:10px;letter-spacing:.18em;color:var(--ice);text-transform:uppercase}

.dos{display:grid;grid-template-columns:1fr 1fr;gap:40px;align-items:start}
.dos .cabecera{display:block}
.pasos{list-style:none;margin:0;padding:34px 38px 34px 50px;background:var(--glass);border:1px solid var(--line);
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur)}
.pasos li{position:relative;padding:0 0 34px 28px;border-left:1px solid var(--line-strong)}
.pasos li:last-child{padding-bottom:0}
.pasos li::before{content:"";position:absolute;left:-5px;top:4px;width:9px;height:9px;border:1px solid var(--amber);background:#000;transform:rotate(45deg)}
.pasos .t{font-family:var(--mono);font-size:10px;letter-spacing:.22em;color:var(--amber);text-transform:uppercase}
.pasos h3{font-family:var(--display);font-size:23px;text-transform:uppercase;margin:6px 0 8px}
.pasos p{font-size:15px;line-height:1.65;color:var(--soft);font-weight:300}

.orbitas{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;margin-top:40px}
.orbita{border:1px solid var(--line);background:var(--glass-strong);-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur);padding:28px}
.orbita .alt{font-family:var(--mono);font-size:11px;letter-spacing:.18em;color:var(--dim);text-transform:uppercase}
.orbita h3{font-family:var(--display);font-size:46px;line-height:1;margin:10px 0 4px}
.orbita .nombre{font-family:var(--mono);font-size:11px;letter-spacing:.2em;color:var(--amber);text-transform:uppercase}
.orbita ul{list-style:none;margin-top:22px;border-top:1px solid var(--line)}
.orbita li{display:flex;justify-content:space-between;padding:11px 0;border-bottom:1px solid var(--line);font-size:14px;color:var(--soft)}
.orbita li b{font-family:var(--mono);font-weight:400;font-size:12px;color:var(--ink)}
.barra{height:2px;background:var(--line);margin-top:20px;position:relative}
.barra i{position:absolute;left:0;top:0;bottom:0;background:var(--amber);box-shadow:0 0 10px var(--amber)}

.flota{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;margin-top:40px}
.nave{border:1px solid var(--line);background:var(--glass-strong);-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur)}
.nave .vista{position:relative;height:250px;border-bottom:1px solid rgba(255,240,220,.12);display:grid;place-items:center;overflow:hidden;
	background:radial-gradient(ellipse 70% 60% at 50% 55%,rgba(255,170,80,.16),rgba(255,140,60,.04) 55%,transparent 75%),
		linear-gradient(180deg,rgba(0,0,0,.35),rgba(0,0,0,0) 60%)}
.nave .vista::after{content:"";position:absolute;left:12%;right:12%;bottom:18px;height:24px;border-radius:50%;pointer-events:none;
	background:radial-gradient(ellipse at center,rgba(255,170,80,.22),transparent 70%);filter:blur(4px)}
.nave .vista svg.respaldo{width:150px;height:110px;stroke:var(--ink);fill:none;stroke-width:1}
.con3d svg.respaldo{display:none}
canvas.vitrina{position:absolute;inset:0;width:100%;height:100%;display:block}
.hud{position:absolute;z-index:2;font-family:var(--mono);font-size:9px;letter-spacing:.2em;text-transform:uppercase;color:var(--dim);pointer-events:none;
	text-shadow:0 1px 6px rgba(0,0,0,.9)}
.hud b{color:var(--amber);font-weight:400}
.hud-tl{top:16px;left:18px}.hud-tr{top:16px;right:18px}.hud-bl{bottom:14px;left:18px}.hud-br{bottom:14px;right:18px}
.hud-ml{top:50%;right:18px;transform:translateY(-50%)}
.hud-ml b{color:var(--ice)}
:not(.con3d) > .hud-bl,:not(.con3d) > .hud-br,:not(.con3d) > .hud-ml{display:none}
.esquina{position:absolute;z-index:2;width:12px;height:12px;border:1px solid rgba(255,180,94,.5);pointer-events:none}
.e1{top:8px;left:8px;border-right:none!important;border-bottom:none!important}
.e2{top:8px;right:8px;border-left:none!important;border-bottom:none!important}
.e3{bottom:8px;left:8px;border-right:none!important;border-top:none!important}
.e4{bottom:8px;right:8px;border-left:none!important;border-top:none!important}
.nave .info{padding:22px 24px 24px}
.nave .estado{font-family:var(--mono);font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:#8be0a4;display:flex;align-items:center;gap:8px}
.nave .estado::before{content:"";width:6px;height:6px;border-radius:50%;background:currentColor;box-shadow:0 0 8px currentColor}
.nave .estado.amb{color:var(--amber)}
.nave h3{font-family:var(--display);font-size:25px;text-transform:uppercase;margin:10px 0 6px}
.nave p{font-size:14px;line-height:1.6;color:var(--soft);font-weight:300}
.nave dl{display:grid;grid-template-columns:1fr 1fr;gap:10px 14px;margin-top:16px;font-family:var(--mono);font-size:11px}
.nave dt{color:var(--dim);letter-spacing:.14em;text-transform:uppercase;font-size:9px}
.nave dd{color:var(--ink);margin-top:2px}

/* ---------- CTA footer ---------- */
.cierre{position:relative;z-index:2;padding:40px 36px 36px}
.cierre-panel{padding:64px 64px 0;overflow:hidden}
.cierre-panel::after{content:"";position:absolute;left:50%;top:-30%;width:70%;height:70%;transform:translateX(-50%);z-index:-1;pointer-events:none;
	background:radial-gradient(ellipse at center,rgba(255,180,94,.16),transparent 65%)}
.cierre-cta{display:grid;grid-template-columns:1.05fr 1fr;gap:64px;align-items:start}
.cierre-titulo{font-size:clamp(46px,6.2vw,98px);line-height:.92;max-width:none;letter-spacing:-.01em}
.cierre-titulo em{font-style:normal;color:var(--amber);text-shadow:0 0 50px rgba(255,180,94,.3)}
.cierre .intro{font-size:17px;max-width:520px;margin-top:24px}
.promesas{display:grid;grid-template-columns:repeat(3,1fr);margin-top:40px;border-top:1px solid rgba(255,240,220,.14);border-bottom:1px solid rgba(255,240,220,.14)}
.promesas div{padding:22px 18px 20px 0}
.promesas div+div{padding-left:22px;border-left:1px solid rgba(255,240,220,.14)}
.promesas strong{display:block;font-family:var(--display);font-size:clamp(28px,2.8vw,40px);font-weight:700;line-height:1}
.promesas sup{font-size:.42em;color:var(--amber);vertical-align:top;margin-left:4px;font-family:var(--mono);font-weight:400}
.promesas span{display:block;margin-top:8px;font-family:var(--mono);font-size:10px;letter-spacing:.16em;text-transform:uppercase;color:var(--dim);line-height:1.6}
.pulso{display:inline-block;flex:none;width:8px;height:8px;border-radius:50%;background:var(--amber);box-shadow:0 0 0 0 rgba(255,180,94,.6);animation:latido 2s infinite}
@keyframes latido{0%{box-shadow:0 0 0 0 rgba(255,180,94,.55)}70%{box-shadow:0 0 0 10px rgba(255,180,94,0)}100%{box-shadow:0 0 0 0 rgba(255,180,94,0)}}
.linea-directa{display:flex;align-items:center;gap:18px;margin-top:30px;padding:18px 22px;border-radius:14px;text-decoration:none;
	background:rgba(0,0,0,.35);border:1px solid rgba(255,240,220,.12);transition:border-color .25s,background .25s;max-width:520px}
.linea-directa:hover{border-color:var(--amber-line);background:rgba(255,180,94,.07)}
.linea-directa span:nth-child(2){flex:1;font-family:var(--mono);font-size:14px;color:var(--ink);letter-spacing:.02em}
.linea-directa small{display:block;font-size:9px;letter-spacing:.2em;text-transform:uppercase;color:var(--dim);margin-bottom:5px}
.linea-directa svg{width:14px;height:14px;stroke:var(--amber);fill:none;stroke-width:1.6}

.intake{padding:30px;border-radius:16px;background:rgba(0,0,0,.42);border:1px solid rgba(255,240,220,.12);
	box-shadow:inset 0 1px 0 rgba(255,240,220,.06),0 30px 60px -30px rgba(0,0,0,.8)}
.intake-cabeza{display:flex;align-items:center;gap:12px;font-family:var(--mono);font-size:10px;letter-spacing:.2em;text-transform:uppercase;
	color:var(--soft);padding-bottom:18px;margin-bottom:6px;border-bottom:1px solid rgba(255,240,220,.1)}
.intake-cabeza b{margin-left:auto;color:var(--amber);font-weight:400}
.enviar{width:100%;padding:18px 22px;margin-top:4px;border-radius:10px}
form{display:grid;grid-template-columns:1fr 1fr;gap:14px}
form .ancho{grid-column:1/-1}
form label{display:block;font-family:var(--mono);font-size:10px;letter-spacing:.2em;text-transform:uppercase;color:var(--dim);margin-bottom:6px}
form input,form select,form textarea{width:100%;background:rgba(0,0,0,.55);border:1px solid var(--line-strong);color:var(--ink);
	font-family:var(--sans);font-size:15px;padding:12px 13px;outline:none;letter-spacing:0;text-transform:none}
form input::placeholder,form textarea::placeholder{color:var(--faint)}
form select{appearance:none;background-image:linear-gradient(45deg,transparent 50%,var(--amber) 50%),linear-gradient(135deg,var(--amber) 50%,transparent 50%);
	background-position:calc(100% - 16px) 50%,calc(100% - 11px) 50%;background-size:5px 5px;background-repeat:no-repeat}
form select option{background:#111}
form textarea{min-height:110px;resize:vertical}
form input:focus,form select:focus,form textarea:focus{border-color:var(--amber)}
.confirmado{display:none;grid-column:1/-1;font-family:var(--mono);font-size:12px;letter-spacing:.14em;color:var(--amber);text-transform:uppercase;line-height:1.8}

.marca-gigante{margin:72px 0 0;text-align:center;white-space:nowrap;overflow:hidden;font-family:var(--display);font-weight:700;
	text-transform:uppercase;font-size:clamp(44px,12vw,168px);line-height:.82;letter-spacing:-.01em;user-select:none;
	color:transparent;-webkit-text-stroke:1px rgba(255,180,94,.28);
	background:linear-gradient(180deg,rgba(255,200,140,.20) 0%,rgba(255,180,94,.04) 70%);-webkit-background-clip:text;background-clip:text;
	-webkit-mask-image:linear-gradient(180deg,#000 40%,transparent 100%);mask-image:linear-gradient(180deg,#000 40%,transparent 100%)}

.cierre-mapa{display:grid;grid-template-columns:1.5fr 1fr 1fr 1.4fr;gap:40px;padding:44px 0 40px;border-top:1px solid rgba(255,240,220,.12)}
.cierre-marca .marca span{white-space:nowrap;font-size:13px;letter-spacing:.38em}
.cierre-marca p{margin-top:18px;max-width:300px;font-size:14px;line-height:1.65;color:var(--soft);font-weight:300}
.estado-mini{display:inline-flex;align-items:center;gap:12px;margin-top:22px;padding:9px 14px;border-radius:999px;
	border:1px solid rgba(255,240,220,.14);font-family:var(--mono);font-size:10px;letter-spacing:.16em;text-transform:uppercase;color:var(--amber)}
.estado-mini .pulso{width:6px;height:6px}
.cierre-mapa h4{font-family:var(--mono);font-size:10px;letter-spacing:.24em;text-transform:uppercase;color:var(--amber);font-weight:400;margin-bottom:18px}
.cierre-mapa ul{list-style:none}
.cierre-mapa li{margin-bottom:11px}
.cierre-mapa li a{text-decoration:none;color:var(--soft);font-size:14px;transition:color .2s}
.cierre-mapa li a:hover{color:var(--amber)}
.lista-contacto{font-family:var(--mono);font-size:12px;letter-spacing:.04em;color:var(--soft)}
.lista-contacto li{margin-bottom:14px;line-height:1.6}
.lista-contacto b{display:block;color:var(--dim);font-weight:normal;font-size:9px;letter-spacing:.2em;text-transform:uppercase;margin-bottom:2px}

.cierre-legal{display:flex;align-items:center;justify-content:space-between;gap:20px;flex-wrap:wrap;padding:22px 0 26px;
	border-top:1px solid rgba(255,240,220,.12);font-family:var(--mono);font-size:10px;letter-spacing:.16em;text-transform:uppercase;color:var(--dim)}
.cierre-legal .enlaces{display:flex;gap:26px}
.cierre-legal a{text-decoration:none;color:var(--dim);transition:color .2s}
.cierre-legal a:hover{color:var(--ink)}
.arriba{display:inline-flex;align-items:center;gap:10px;color:var(--amber)!important}
.arriba svg{width:12px;height:12px;stroke:currentColor;fill:none;stroke-width:1.6}

/* ---------- Signature glass panel (amber take on the gradient-mesh card) ---------- */
@property --giro{syntax:'<angle>';inherits:false;initial-value:0deg}
.cabecera,.cifras,.servicio,.pasos,.orbita,.nave,.cierre-panel,#panel{
	position:relative;isolation:isolate;border:none!important;border-radius:16px;
	background-color:rgba(14,11,9,.84);
	background-image:
		radial-gradient(at 88% 40%,rgba(14,11,9,.92) 0px,transparent 85%),
		radial-gradient(at 49% 30%,rgba(14,11,9,.92) 0px,transparent 85%),
		radial-gradient(at 14% 26%,rgba(14,11,9,.92) 0px,transparent 85%),
		radial-gradient(at 0% 64%,rgba(184,102,31,.42) 0px,transparent 85%),
		radial-gradient(at 41% 94%,rgba(255,215,161,.20) 0px,transparent 85%),
		radial-gradient(at 100% 99%,rgba(255,150,70,.36) 0px,transparent 85%);
	-webkit-backdrop-filter:var(--blur);backdrop-filter:var(--blur);
	box-shadow:inset 0 -16px 24px 0 rgba(255,228,196,.12),0 24px 60px -20px rgba(0,0,0,.7)}
/* gradient border + an amber light that sweeps around it */
.cabecera::before,.cifras::before,.servicio::before,.pasos::before,.orbita::before,.nave::before,.cierre-panel::before,#panel::before{
	content:"";position:absolute;inset:0;z-index:-1;pointer-events:none;border-radius:inherit;padding:1px;
	background:
		conic-gradient(from var(--giro),transparent 0deg,transparent 20deg,rgba(255,180,94,.95) 55deg,#ffe2bd 75deg,rgba(255,180,94,.95) 95deg,transparent 130deg,transparent 360deg),
		linear-gradient(0deg,rgba(255,240,220,.55) -50%,rgba(255,255,255,.07) 100%);
	-webkit-mask:linear-gradient(#000 0 0) content-box,linear-gradient(#000 0 0);
	-webkit-mask-composite:xor;mask:linear-gradient(#000 0 0) content-box exclude,linear-gradient(#000 0 0);
	animation:barrido 8s linear infinite}
@keyframes barrido{to{--giro:360deg}}
/* desynchronise the sweeps so a row of cards doesn't pulse in lockstep */
.servicio:nth-child(3n+2)::before,.orbita:nth-child(2)::before,.nave:nth-child(2)::before{animation-delay:-2.7s}
.servicio:nth-child(3n)::before,.orbita:nth-child(3)::before,.nave:nth-child(3)::before{animation-delay:-5.3s}
.servicio:nth-child(n+4)::before{animation-duration:9.5s}
.pasos::before{animation-delay:-4s}.cierre-panel::before{animation-duration:14s}
/* text over the warm lower corners: keep it crisp */
.servicio p,.pasos p,.nave p,.orbita li,.intro,.cierre .intro{text-shadow:0 1px 12px rgba(0,0,0,.55)}
.nave{overflow:hidden}
.cifras div{border-color:rgba(255,240,220,.12)!important}
.servicios{gap:18px;background:none;border:none;-webkit-backdrop-filter:none;backdrop-filter:none}
.servicio{transition:transform .35s ease,box-shadow .35s ease}
.servicio:hover{background-color:rgba(20,14,10,.88);transform:translateY(-4px);
	box-shadow:inset 0 -18px 28px 0 rgba(255,200,140,.18),0 30px 70px -24px rgba(0,0,0,.8)}
.servicio::after{border-radius:16px 16px 0 0;left:16px;right:16px;width:auto;transform:scaleX(0);transform-origin:left;transition:transform .4s}
.servicio:hover::after{width:auto;transform:scaleX(1)}
form input,form select,form textarea{border-radius:10px}
#panel .toggles button{border-radius:8px}

.aparecer{opacity:0;transform:translateY(26px);transition:opacity .9s ease,transform .9s ease}
.aparecer.visto{opacity:1;transform:none}

#error{display:none;position:fixed;inset:0;z-index:50;background:rgba(0,0,0,.92);padding:40px 30px;
	font-family:var(--mono);font-size:11px;line-height:1.8;color:#ff9d7a;white-space:pre-wrap;overflow:auto}
#error h2{font-size:12px;letter-spacing:.3em;text-transform:uppercase;color:var(--ink);margin-bottom:16px;font-weight:normal;font-family:var(--mono)}

@media (max-width:1280px){
	.radar{display:none}
	.rasgos div{padding:0 28px}
}
@media (max-width:1100px){
	nav{grid-template-columns:1fr auto}
	.nav-centro{display:none}
	#datos{display:none}
	.estado-sis .lema{display:none}
}
@media (max-width:980px){
	.servicios,.orbitas,.flota{grid-template-columns:1fr 1fr}
	.dos{grid-template-columns:1fr;gap:24px}
	.cierre-cta{grid-template-columns:1fr;gap:44px}
	.cierre-mapa{grid-template-columns:1fr 1fr}
	.cierre-marca{grid-column:1/-1}
	.cifras{grid-template-columns:1fr 1fr}
	.cifras div:nth-child(2){border-right:none}
	.cifras div:nth-child(-n+2){border-bottom:1px solid var(--line)}
	.hero::before{background:linear-gradient(90deg,rgba(0,0,0,.8),rgba(0,0,0,.35)),linear-gradient(0deg,rgba(0,0,0,.6),transparent 30%)}
}
@media (max-width:640px){
	nav{padding:14px 16px}
	nav > .btn{display:none}
	.marca span{font-size:12px;letter-spacing:.38em}
	section{padding:72px 16px}
	.hero{padding:110px 20px 120px;justify-content:flex-end}
	.ceja{font-size:11px;letter-spacing:.22em;margin-bottom:20px}
	.ceja::after{width:30px}
	.hero-copia p{font-size:16px;margin-top:20px}
	.hero-ctas{gap:12px;margin-top:28px}
	.hero-ctas .btn{width:100%;min-width:0;padding:17px 20px}
	.rasgos{margin-top:30px;font-size:9px;letter-spacing:.12em}
	.rasgos div{padding:0 14px}
	.pie-hero{left:20px;right:20px;bottom:20px}
	.estado-sis .caja{padding:10px 14px;font-size:10px}
	#panel{left:16px;right:16px;bottom:76px;width:auto}
	.cabecera{padding:24px 22px 26px;display:block}
	.pasos{padding:26px 22px 26px 34px}
	.servicios,.orbitas,.flota,form{grid-template-columns:1fr}
	.cierre{padding:24px 16px 16px}
	.cierre-panel{padding:36px 20px 0}
	.marca-gigante{margin:48px 0 0}
	.intake{padding:20px}
	.promesas{grid-template-columns:1fr}
	.promesas div,.promesas div+div{padding:16px 0;border-left:none}
	.promesas div+div{border-top:1px solid rgba(255,240,220,.14)}
	.cierre-mapa{grid-template-columns:1fr;gap:30px}
	.cierre-legal{flex-direction:column;align-items:flex-start}
	.cifras div{padding:24px 18px}
}
@media (prefers-reduced-motion:reduce){
	.cinta .pista,.pulso,.estado-sis .caja::before,.bajar i,.radar .giro,.cabecera::before,.cifras::before,.servicio::before,.pasos::before,.orbita::before,.nave::before,.cierre-panel::before,#panel::before{animation:none}
	.aparecer{opacity:1;transform:none;transition:none}
	html{scroll-behavior:auto}
}
</style>
</head>
<body>

<div id="velo" aria-hidden="true"></div>

<nav id="nav" aria-label="Primary" data-section="nav">
	<a class="marca" href="#inicio" aria-label="Halcyon Orbital home">
		<svg viewBox="0 0 44 30" aria-hidden="true">
			<defs><radialGradient id="gPlaneta" cx="38%" cy="35%" r="70%"><stop offset="0" stop-color="#ffd7a1"/><stop offset=".6" stop-color="#ffb45e"/><stop offset="1" stop-color="#b8661f"/></radialGradient></defs>
			<path d="M3 21 C 8 27, 36 19, 41 9" fill="none" stroke="#efebe2" stroke-width="1.6" stroke-linecap="round"/>
			<circle cx="22" cy="15" r="8.5" fill="url(#gPlaneta)"/>
			<path d="M41 9 C 37 4, 12 8, 5 17" fill="none" stroke="#efebe2" stroke-width="1.6" stroke-linecap="round"/>
		</svg>
		<span>Halcyon Orbital<small>Satellite servicing</small></span>
	</a>
	<div class="nav-centro">
		<ul>
			<li><a href="#servicios" data-seccion="servicios">Services</a></li>
			<li><a href="#proceso" data-seccion="proceso">Mission profile</a></li>
			<li><a href="#cobertura" data-seccion="cobertura">Coverage</a></li>
			<li><a href="#flota" data-seccion="flota">Fleet</a></li>
		</ul>
	</div>
	<a class="btn" href="#contacto">Request a mission <svg viewBox="0 0 12 12" aria-hidden="true"><path d="M4 2l4 4-4 4"/></svg></a>
</nav>

<main>
	<!-- HERO -->
	<header class="hero" id="inicio" data-section="hero">
		<div class="hero-copia">
			<h1>Nothing in<br>orbit has<br>to be <em>lost.</em></h1>
			<p>Inspection, refuelling, robotic repair, relocation and clean end-of-life disposal for satellites from LEO to GEO. We fly to your asset so your asset keeps flying.</p>
			<div class="hero-ctas interactivo">
				<a class="btn lleno" href="#contacto">Plan a servicing mission <svg viewBox="0 0 12 12" aria-hidden="true"><path d="M4 2l4 4-4 4"/></svg></a>
				<a class="btn fantasma" href="#servicios">See capabilities <svg class="barras" aria-hidden="true" viewBox="0 0 14 12"><rect x="0" y="8" width="2" height="4"/><rect x="4" y="5" width="2" height="7"/><rect x="8" y="2" width="2" height="10"/><rect x="12" y="0" width="2" height="12"/></svg></a>
			</div>
			<div class="rasgos">
				<div><strong>LEO → GEO</strong><span>Coverage</span></div>
				<div><strong>Experienced</strong><span>Flight team</span></div>
				<div><strong>End-to-end</strong><span>Asset lifecycle</span></div>
			</div>
		</div>

		<div id="datos" aria-hidden="true">
			<span class="t">Live telemetry</span>
			Servicer MK 3 · range to client <b id="tRango">412.0 m</b><br>
			Closing rate <b id="tVel">0.08 m/s</b><br>
			Station · lat <b id="tLat">53.3989° N</b><br>
			Next docking window <b id="tVentana">T−04:12:09</b>
		</div>

		<div class="radar" aria-hidden="true">
			<ul>
				<li data-anillo="0">LEO</li>
				<li data-anillo="1">MEO</li>
				<li data-anillo="2" class="on">GEO</li>
			</ul>
			<svg viewBox="0 0 200 200">
				<circle class="anillo" cx="100" cy="100" r="52"/>
				<circle class="anillo" cx="100" cy="100" r="74" stroke-dasharray="1 5"/>
				<circle class="anillo on" cx="100" cy="100" r="96" stroke-dasharray="2 6"/>
				<g fill="#efebe2" opacity=".75">
					<circle cx="100" cy="48" r="1.6"/><circle cx="100" cy="152" r="1.6"/><circle cx="48" cy="100" r="1.6"/><circle cx="152" cy="100" r="1.6"/>
					<circle cx="100" cy="4" r="1.2"/><circle cx="100" cy="196" r="1.2"/><circle cx="4" cy="100" r="1.2"/><circle cx="196" cy="100" r="1.2"/>
				</g>
				<path d="M100 92v16M92 100h16" stroke="#ffb45e" stroke-width="1.4"/>
				<g class="giro g1"><circle cx="100" cy="48" r="3" fill="#ffb45e"/></g>
				<g class="giro g2"><circle cx="152" cy="126" r="2.2" fill="#efebe2"/></g>
				<g class="giro g3"><circle cx="168" cy="168" r="4" fill="#ffb45e" style="filter:drop-shadow(0 0 5px #ffb45e)"/></g>
			</svg>
		</div>

		<div class="pie-hero">
			<div class="estado-sis">
				<span class="caja">Systems nominal</span>
				<span class="lema">Orbiting a more sustainable tomorrow</span>
			</div>
		</div>

	</header>

	<!-- STATS -->
	<section id="cifras" data-section="stats" aria-label="Track record">
		<div class="envoltura">
			<div class="cifras aparecer">
				<div><strong data-cuenta="214">0</strong><span>Satellites serviced</span></div>
				<div><strong><b data-cuenta="11.4" data-dec="1">0</b><sup>yrs</sup></strong><span>Avg. life added per client</span></div>
				<div><strong><b data-cuenta="99.2" data-dec="1">0</b><sup>%</sup></strong><span>Mission success rate</span></div>
				<div><strong data-cuenta="38">0</strong><span>Operators in 14 countries</span></div>
			</div>
		</div>
	</section>

	<!-- SERVICES -->
	<section id="servicios" data-section="services">
		<div class="envoltura">
			<div class="cabecera aparecer">
<div class="rotulo">01 <span>/</span> Capabilities</div>
			<h2 class="aparecer">A full-service garage, three hundred kilometres up and beyond.</h2>
			<p class="intro">Every servicer in our fleet carries dexterous robotic arms, a universal docking probe and its own propellant reserve — so one launch can cover several clients on the same orbital shell.</p>
			</div>

			<div class="servicios">
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="inspeccion">
						<span class="hud hud-tl">S-01 · <b>Inspect</b></span>
						<span class="hud hud-tr">Client · GEO-114</span>
						<span class="hud hud-bl">Points <b data-k="pts">0</b></span>
						<span class="hud hud-br">Scan <b data-k="scan">0%</b></span>
						<span class="hud hud-ml"><b data-k="falla">Searching</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><circle cx="20" cy="20" r="7"/><circle cx="20" cy="20" r="15" stroke-dasharray="2 4"/><path d="M20 2v6M20 32v6M2 20h6M32 20h6"/></svg>
					</div>
					<h3>Inspection &amp; diagnostics</h3>
					<p>Close-range flyarounds with stereo cameras, LIDAR and thermal imaging to find the fault before anyone touches the hardware.</p>
					<span class="tag">From 3 days on station</span>
				</article>
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="repostaje">
						<span class="hud hud-tl">S-02 · <b>Refuel</b></span>
						<span class="hud hud-tr">N₂H₄ · 22 bar</span>
						<span class="hud hud-bl">Flow <b data-k="flujo">1.60 kg/min</b></span>
						<span class="hud hud-br">Delivered <b data-k="kg">0 kg</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><path d="M14 6h12v6H14zM17 12v10M23 12v10"/><path d="M12 22h16l-3 12H15z"/><path d="M20 26v4"/></svg>
					</div>
					<h3>In-orbit refuelling</h3>
					<p>Valve-agnostic tooling transfers hydrazine or xenon into satellites never designed to be refuelled, adding years of station-keeping.</p>
					<span class="tag">Up to 400 kg per visit</span>
				</article>
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="reparacion">
						<span class="hud hud-tl">S-03 · <b>Repair</b></span>
						<span class="hud hud-tr">Bay 05 · RW-2</span>
						<span class="hud hud-bl">Torque <b data-k="par">— Nm</b></span>
						<span class="hud hud-br">Step <b data-k="paso">Approach</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><path d="M6 34l10-10M16 24l4-12 8-6 6 6-6 8-12 4"/><circle cx="28" cy="12" r="2"/></svg>
					</div>
					<h3>Robotic repair</h3>
					<p>Replace reaction wheels, re-seat jammed solar arrays, patch thermal blankets and swap out failed avionics modules with tele-operated precision.</p>
					<span class="tag">Sub-millimetre manipulation</span>
				</article>
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="acople">
						<span class="hud hud-tl">S-04 · <b>Dock</b></span>
						<span class="hud hud-tr">Aft capture</span>
						<span class="hud hud-bl">Range <b data-k="rango">0.0 m</b></span>
						<span class="hud hud-br"><b data-k="estado">Approach</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><rect x="13" y="13" width="14" height="14"/><path d="M4 20h9M27 20h9M20 4v9M20 27v9"/><path d="M6 15h4v10H6zM30 15h4v10h-4z"/></svg>
					</div>
					<h3>Life-extension docking</h3>
					<p>Our tug docks and stays attached, taking over attitude control and propulsion for a client whose own systems are spent.</p>
					<span class="tag">5–15 year contracts</span>
				</article>
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="relocacion">
						<span class="hud hud-tl">S-05 · <b>Relocate</b></span>
						<span class="hud hud-tr">Hohmann transfer</span>
						<span class="hud hud-bl">Alt <b data-k="alt">400 km</b></span>
						<span class="hud hud-br">Δv <b data-k="dv">Coast</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><ellipse cx="20" cy="20" rx="16" ry="7"/><ellipse cx="20" cy="20" rx="10" ry="4"/><path d="M30 14l6-2-2 6"/></svg>
					</div>
					<h3>Relocation &amp; orbit raising</h3>
					<p>Rescue stranded launches, shift a slot across the GEO arc or raise a sagging LEO constellation member back to its design altitude.</p>
					<span class="tag">Up to 2,800 kg client mass</span>
				</article>
				<article class="servicio aparecer">
					<div class="escena" data-vitrina="desorbitado">
						<span class="hud hud-tl">S-06 · <b>Dispose</b></span>
						<span class="hud hud-tr">Target · S. Pacific</span>
						<span class="hud hud-bl">Alt <b data-k="alt">400 km</b></span>
						<span class="hud hud-br"><b data-k="estado">Descent</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 40 40"><circle cx="20" cy="20" r="14"/><path d="M20 6c-6 8-6 20 0 28M10 30l20-20"/></svg>
					</div>
					<h3>End-of-life disposal</h3>
					<p>Controlled deorbit over unpopulated ocean, or a clean boost to graveyard orbit — fully compliant with the 5-year disposal rules.</p>
					<span class="tag">Licence paperwork included</span>
				</article>
			</div>
		</div>
	</section>

	<!-- PROCESS -->
	<section id="proceso" data-section="process">
		<div class="envoltura dos">
			<div class="cabecera aparecer">
				<div class="rotulo">02 <span>/</span> Mission profile</div>
				<h2 class="aparecer">From first call to hard dock in as little as ninety days.</h2>
				<p class="intro">Approaching a satellite that was never built to be approached is the hard part. We have rehearsed every phase thousands of times in simulation and dozens of times for real — and you watch it all live from our operations centre or your own.</p>
			</div>
			<ol class="pasos aparecer">
				<li><div class="t">Phase 1 · Weeks 1–3</div><h3>Assessment</h3><p>We ingest your telemetry, build a digital twin of the client vehicle and design a capture plan around its exact geometry and spin state.</p></li>
				<li><div class="t">Phase 2 · Weeks 4–10</div><h3>Phasing</h3><p>A servicer already on station transfers to your orbital plane, sharing the trip with other clients to keep propellant costs down.</p></li>
				<li><div class="t">Phase 3 · Final 72 hours</div><h3>Rendezvous &amp; capture</h3><p>Autonomous approach from 10 km to contact, with hold points where your team must give a go/no-go before we proceed.</p></li>
				<li><div class="t">Phase 4 · Ongoing</div><h3>Service &amp; release</h3><p>The work is done, verified with full imaging, and your satellite is released — or we stay docked for the life of the contract.</p></li>
			</ol>
		</div>
	</section>

	<!-- COVERAGE -->
	<section id="cobertura" data-section="coverage">
		<div class="envoltura">
			<div class="cabecera aparecer">
<div class="rotulo">03 <span>/</span> Coverage</div>
			<h2 class="aparecer">Wherever you parked it, we can reach it.</h2>
			</div>
			<div class="orbitas">
				<div class="orbita aparecer">
					<div class="alt">160 – 2,000 km</div>
					<h3>LEO</h3>
					<div class="nombre">Low Earth orbit</div>
					<ul>
						<li>Response time <b>≤ 21 days</b></li>
						<li>Typical services <b>Inspect · Deorbit</b></li>
						<li>Clients in range <b>~9,800</b></li>
					</ul>
					<div class="barra"><i style="width:92%"></i></div>
				</div>
				<div class="orbita aparecer">
					<div class="alt">2,000 – 35,000 km</div>
					<h3>MEO</h3>
					<div class="nombre">Medium Earth orbit</div>
					<ul>
						<li>Response time <b>≤ 45 days</b></li>
						<li>Typical services <b>Repair · Raise</b></li>
						<li>Clients in range <b>~140</b></li>
					</ul>
					<div class="barra"><i style="width:64%"></i></div>
				</div>
				<div class="orbita aparecer">
					<div class="alt">35,786 km</div>
					<h3>GEO</h3>
					<div class="nombre">Geostationary belt</div>
					<ul>
						<li>Response time <b>≤ 30 days</b></li>
						<li>Typical services <b>Refuel · Extend</b></li>
						<li>Clients in range <b>~560</b></li>
					</ul>
					<div class="barra"><i style="width:100%"></i></div>
				</div>
			</div>
		</div>
	</section>

	<!-- FLEET -->
	<section id="flota" data-section="fleet">
		<div class="envoltura">
			<div class="cabecera aparecer">
<div class="rotulo">04 <span>/</span> The fleet</div>
			<h2 class="aparecer">Three servicers on station. Two more on the pad.</h2>
			</div>
			<div class="flota">
				<article class="nave aparecer">
					<div class="vista" data-vitrina="flota-warden">
						<span class="hud hud-tl">Model · <b>HX-3</b></span>
						<span class="hud hud-tr">GEO</span>
						<span class="hud hud-bl">3D · live</span>
						<span class="hud hud-br">Yaw <b data-k="rot">000°</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 150 110"><rect x="58" y="38" width="34" height="34"/><path d="M8 48h44v14H8zM98 48h44v14H98zM52 55h6M92 55h6"/><path d="M18 48v14M28 48v14M38 48v14M108 48v14M118 48v14M128 48v14"/><path d="M75 72v14l-8 10M75 86l8 10"/><circle cx="75" cy="30" r="6"/></svg>
					</div>
					<div class="info">
						<div class="estado">On station · GEO</div>
						<h3>HX-3 “Warden”</h3>
						<p>Our flagship life-extension tug, currently closing on a client in the GEO arc.</p>
						<dl><div><dt>Dry mass</dt><dd>2,140 kg</dd></div><div><dt>Δv reserve</dt><dd>1.9 km/s</dd></div><div><dt>Arms</dt><dd>2 × 7-DOF</dd></div><div><dt>Missions</dt><dd>41</dd></div></dl>
					</div>
				</article>
				<article class="nave aparecer">
					<div class="vista" data-vitrina="flota-tern">
						<span class="hud hud-tl">Model · <b>LX-7</b></span>
						<span class="hud hud-tr">LEO</span>
						<span class="hud hud-bl">3D · live</span>
						<span class="hud hud-br">Yaw <b data-k="rot">000°</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 150 110"><path d="M55 30h40l10 25-10 25H55L45 55z"/><path d="M45 55H15M105 55h30"/><circle cx="12" cy="55" r="4"/><circle cx="138" cy="55" r="4"/><path d="M75 30V14M68 14h14"/><path d="M62 80l-6 16M88 80l6 16"/></svg>
					</div>
					<div class="info">
						<div class="estado">On station · LEO</div>
						<h3>LX-7 “Tern”</h3>
						<p>A nimble inspection-and-disposal craft built to hop between constellation shells.</p>
						<dl><div><dt>Dry mass</dt><dd>680 kg</dd></div><div><dt>Δv reserve</dt><dd>3.4 km/s</dd></div><div><dt>Sensors</dt><dd>LIDAR · IR</dd></div><div><dt>Missions</dt><dd>118</dd></div></dl>
					</div>
				</article>
				<article class="nave aparecer">
					<div class="vista" data-vitrina="flota-depot">
						<span class="hud hud-tl">Model · <b>RX-1</b></span>
						<span class="hud hud-tr">GEO −300</span>
						<span class="hud hud-bl">3D · live</span>
						<span class="hud hud-br">Yaw <b data-k="rot">000°</b></span>
						<i class="esquina e1"></i><i class="esquina e2"></i><i class="esquina e3"></i><i class="esquina e4"></i>
						<svg class="respaldo" aria-hidden="true" viewBox="0 0 150 110"><rect x="50" y="28" width="50" height="54" rx="4"/><path d="M60 28V18h30v10"/><circle cx="75" cy="55" r="12"/><path d="M75 43v24M63 55h24"/><path d="M50 40H20v30h30M100 40h30v30h-30"/></svg>
					</div>
					<div class="info">
						<div class="estado amb">Integration · launch Q2</div>
						<h3>RX-1 “Depot”</h3>
						<p>A propellant depot that will let our servicers refuel themselves without coming home.</p>
						<dl><div><dt>Capacity</dt><dd>3,600 kg</dd></div><div><dt>Ports</dt><dd>4 universal</dd></div><div><dt>Orbit</dt><dd>GEO −300 km</dd></div><div><dt>Design life</dt><dd>20 yrs</dd></div></dl>
					</div>
				</article>
			</div>
		</div>
	</section>

</main>

<!-- CTA FOOTER -->
<footer id="contacto" class="cierre" data-section="cta">
	<div class="envoltura">
		<div class="cierre-panel aparecer">
			<div class="cierre-cta">
				<div class="cierre-copia">
					<div class="rotulo">05 <span>/</span> Request a mission</div>
					<h2 class="cierre-titulo">Tell us what’s wrong <em>up there.</em></h2>
					<p class="intro">Share the basics and a mission engineer will come back within one business day with a feasibility read and a first launch-window estimate.</p>
					<div class="promesas">
						<div><strong>&lt; 24<sup>h</sup></strong><span>First engineering response</span></div>
						<div><strong>90<sup>days</sup></strong><span>Fastest call-to-dock</span></div>
						<div><strong>24/7</strong><span>Mission control on watch</span></div>
					</div>
					<a class="linea-directa" href="mailto:missions@halcyon-orbital.example">
						<span class="pulso"></span>
						<span><small>Priority line · anomalies &amp; emergencies</small>missions@halcyon-orbital.example</span>
						<svg viewBox="0 0 12 12" aria-hidden="true"><path d="M3 9l6-6M4 3h5v5"/></svg>
					</a>
				</div>

				<form id="formulario" class="intake" novalidate>
					<div class="intake-cabeza ancho"><span class="pulso"></span>Mission intake · encrypted channel <b>MSN-0218</b></div>
					<div><label for="fNombre">Name</label><input id="fNombre" required autocomplete="name" placeholder="Jordan Reyes"></div>
					<div><label for="fOrg">Operator / organisation</label><input id="fOrg" autocomplete="organization" placeholder="Your company"></div>
					<div><label for="fCorreo">Email</label><input id="fCorreo" type="email" required autocomplete="email" placeholder="you@operator.com"></div>
					<div><label for="fOrbita">Orbit regime</label>
						<select id="fOrbita"><option>LEO</option><option>MEO</option><option selected>GEO</option><option>Other / unsure</option></select></div>
					<div class="ancho"><label for="fServicio">Service needed</label>
						<select id="fServicio"><option>Inspection &amp; diagnostics</option><option>In-orbit refuelling</option><option>Robotic repair</option><option>Life-extension docking</option><option>Relocation &amp; orbit raising</option><option>End-of-life disposal</option></select></div>
					<div class="ancho"><label for="fMsg">Situation</label><textarea id="fMsg" placeholder="Satellite, launch year, symptoms, deadlines…"></textarea></div>
					<div class="ancho"><button class="btn lleno enviar" type="submit">Transmit request <svg viewBox="0 0 12 12" aria-hidden="true"><path d="M4 2l4 4-4 4"/></svg></button></div>
					<div class="confirmado" id="confirmado">Signal received. A mission engineer will be in touch within one business day.</div>
				</form>
			</div>

			<div class="marca-gigante" aria-hidden="true">Halcyon Orbital</div>

			<div class="cierre-mapa">
				<div class="cierre-marca">
					<a class="marca" href="#inicio" aria-label="Back to top">
						<svg viewBox="0 0 44 30" aria-hidden="true"><defs><radialGradient id="gPlaneta2" cx="38%" cy="35%" r="70%"><stop offset="0" stop-color="#ffd7a1"/><stop offset=".6" stop-color="#ffb45e"/><stop offset="1" stop-color="#b8661f"/></radialGradient></defs><path d="M3 21 C 8 27, 36 19, 41 9" fill="none" stroke="#efebe2" stroke-width="1.6" stroke-linecap="round"/><circle cx="22" cy="15" r="8.5" fill="url(#gPlaneta2)"/><path d="M41 9 C 37 4, 12 8, 5 17" fill="none" stroke="#efebe2" stroke-width="1.6" stroke-linecap="round"/></svg>
						<span>Halcyon Orbital<small>Satellite servicing</small></span>
					</a>
					<p>Inspection, refuelling, repair and responsible disposal — keeping orbit useful for the next generation of missions.</p>
					<div class="estado-mini"><span class="pulso"></span>All servicers nominal</div>
				</div>
				<div>
					<h4>Services</h4>
					<ul>
						<li><a href="#servicios">Inspection</a></li>
						<li><a href="#servicios">Refuelling</a></li>
						<li><a href="#servicios">Robotic repair</a></li>
						<li><a href="#servicios">Life extension</a></li>
						<li><a href="#servicios">Disposal</a></li>
					</ul>
				</div>
				<div>
					<h4>Company</h4>
					<ul>
						<li><a href="#proceso">Mission profile</a></li>
						<li><a href="#cobertura">Coverage</a></li>
						<li><a href="#flota">Fleet</a></li>
						<li><a href="#contacto">Careers</a></li>
					</ul>
				</div>
				<div>
					<h4>Operations</h4>
					<ul class="lista-contacto">
						<li><b>Control</b>24/7 · UTC</li>
						<li><b>Sites</b>Toulouse · Denver · Tanegashima</li>
						<li><b>Email</b>missions@halcyon-orbital.example</li>
					</ul>
				</div>
			</div>

			<div class="cierre-legal">
				<span>© 2026 Halcyon Orbital · Fictional demo brand</span>
				<span class="enlaces"><a href="#contacto">Privacy</a><a href="#contacto">Terms</a><a href="#contacto">Debris policy</a></span>
				<a class="arriba" href="#inicio">Back to orbit <svg viewBox="0 0 12 12" aria-hidden="true"><path d="M2 8l4-4 4 4"/></svg></a>
			</div>
		</div>
	</div>
</footer>

<div id="error" role="alert"><h2>Diagnostics</h2><div id="errorTexto"></div></div>

<script>
	function mostrarError(msg){
		var caja = document.getElementById('error');
		var txt  = document.getElementById('errorTexto');
		caja.style.display = 'block';
		txt.textContent += msg + '\n\n';
	}
	window.onerror = function(msg, src, linea){
		mostrarError('JS error: ' + msg + ' (line ' + linea + ')');
	};
</script>

<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"
	onerror="mostrarError('Could not load Three.js from the CDN. Check your connection or whether something is blocking cdnjs.cloudflare.com.')"></script>

<script>
/* ================= Page UI (independent of WebGL) ================= */
(function(){
	'use strict';
	var nav = document.getElementById('nav');
	var velo = document.getElementById('velo');
	function alDesplazar(){
		var y = window.scrollY, h = window.innerHeight;
		nav.classList.toggle('solido', y > 40);
		var k = Math.min(1, Math.max(0, (y - h * 0.08) / (h * 0.95)));
		velo.style.opacity = k * k * (3 - 2 * k);
	}
	window.addEventListener('scroll', alDesplazar, {passive:true});
	alDesplazar();

	var reducido = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;

	function contar(el){
		var fin = parseFloat(el.getAttribute('data-cuenta'));
		var dec = parseInt(el.getAttribute('data-dec') || '0', 10);
		if(reducido){ el.textContent = fin.toFixed(dec); return; }
		var t0 = performance.now(), dur = 1600;
		(function paso(t){
			var k = Math.min(1, (t - t0) / dur);
			k = 1 - Math.pow(1 - k, 3);
			el.textContent = (fin * k).toFixed(dec);
			if(k < 1) requestAnimationFrame(paso);
		})(t0);
	}

	if('IntersectionObserver' in window){
		var io = new IntersectionObserver(function(entradas){
			entradas.forEach(function(e){
				if(!e.isIntersecting) return;
				e.target.classList.add('visto');
				e.target.querySelectorAll('[data-cuenta]').forEach(contar);
				io.unobserve(e.target);
			});
		}, {threshold:0.15});
		document.querySelectorAll('.aparecer').forEach(function(el, i){
			el.style.transitionDelay = (i % 3) * 0.08 + 's';
			io.observe(el);
		});
	} else {
		document.querySelectorAll('.aparecer').forEach(function(el){ el.classList.add('visto'); });
		document.querySelectorAll('[data-cuenta]').forEach(contar);
	}

	/* simulated live telemetry */
	var rango = 412.0, ventana = 4*3600 + 12*60 + 9;
	var eR = document.getElementById('tRango'), eV = document.getElementById('tVel'), eW = document.getElementById('tVentana');
	setInterval(function(){
		var vel = 0.06 + Math.random() * 0.04;
		rango = rango > 2 ? rango - vel : 412.0;
		ventana = ventana > 0 ? ventana - 1 : 6*3600;
		eR.textContent = rango.toFixed(1) + ' m';
		eV.textContent = vel.toFixed(2) + ' m/s';
		var h = Math.floor(ventana/3600), m = Math.floor(ventana%3600/60), s = ventana%60;
		eW.textContent = 'T−' + String(h).padStart(2,'0') + ':' + String(m).padStart(2,'0') + ':' + String(s).padStart(2,'0');
	}, 1000);

	/* station latitude drifts slowly */
	var eL = document.getElementById('tLat'), lat = 53.3989;
	setInterval(function(){ lat += (Math.random() - 0.5) * 0.0006; eL.textContent = lat.toFixed(4) + '° N'; }, 1000);

	/* nav: highlight the section in view */
	var enlaces = document.querySelectorAll('nav ul a[data-seccion]');
	function marcar(id){ enlaces.forEach(function(a){ a.classList.toggle('activo', a.getAttribute('data-seccion') === id); }); }
	marcar('servicios');
	if('IntersectionObserver' in window){
		var ioNav = new IntersectionObserver(function(es){
			es.forEach(function(e){ if(e.isIntersecting) marcar(e.target.id); });
		}, {rootMargin:'-45% 0px -50% 0px'});
		['servicios','proceso','cobertura','flota'].forEach(function(id){ ioNav.observe(document.getElementById(id)); });
	}

	/* radar: cycle LEO / MEO / GEO highlight; hover a label to pick one */
	var etiquetas = document.querySelectorAll('.radar li');
	var anillos = document.querySelectorAll('.radar .anillo');
	var idxRadar = 2, pausaRadar = false;
	function radar(i){
		idxRadar = i;
		etiquetas.forEach(function(li, k){ li.classList.toggle('on', k === i); });
		anillos.forEach(function(c, k){ c.classList.toggle('on', k === i); });
	}
	etiquetas.forEach(function(li, k){
		li.addEventListener('mouseenter', function(){ pausaRadar = true; radar(k); });
		li.addEventListener('mouseleave', function(){ pausaRadar = false; });
	});
	if(!reducido) setInterval(function(){ if(!pausaRadar) radar((idxRadar + 1) % 3); }, 3200);

	/* size the footer wordmark to exactly fill its row, whatever font loads */
	var gigante = document.querySelector('.marca-gigante');
	function ajustarMarca(){
		if(!gigante) return;
		gigante.style.fontSize = '100px';
		var ancho = gigante.clientWidth, real = gigante.scrollWidth;
		if(real > 0) gigante.style.fontSize = Math.max(32, Math.floor(100 * ancho / real * 0.98)) + 'px';
	}
	ajustarMarca();
	window.addEventListener('resize', ajustarMarca);
	if(document.fonts && document.fonts.ready) document.fonts.ready.then(ajustarMarca);

	/* contact form (demo — no backend) */
	var form = document.getElementById('formulario');
	form.addEventListener('submit', function(e){
		e.preventDefault();
		var ok = true;
		['fNombre','fCorreo'].forEach(function(id){
			var c = document.getElementById(id);
			var valido = c.value.trim() && c.checkValidity();
			c.style.borderColor = valido ? '' : '#ff9d7a';
			if(!valido) ok = false;
		});
		if(!ok) return;
		document.getElementById('confirmado').style.display = 'block';
		form.querySelector('button[type=submit]').disabled = true;
	});
})();

/* ================= Black hole renderer ================= */
(function(){
	'use strict';

	if(typeof THREE === 'undefined'){ mostrarError('Three.js is not available (the CDN did not load).'); return; }

	var prueba = document.createElement('canvas');
	if(!(prueba.getContext('webgl') || prueba.getContext('experimental-webgl'))){
		mostrarError('Your browser or device does not support WebGL.'); return;
	}

	var renderer;
	try{
		renderer = new THREE.WebGLRenderer({antialias:false, powerPreference:'high-performance'});
	}catch(e){ mostrarError('Could not create the WebGL renderer: ' + e.message); return; }
	renderer.domElement.setAttribute('aria-hidden', 'true');
	renderer.domElement.id = 'escena3d';
	document.body.insertBefore(renderer.domElement, document.body.firstChild);

	var baseDPR = Math.min(window.devicePixelRatio || 1, 2);

	var calidades = {
		baja:  {dpr: 0.55, pasos: 150, iterBloom: 1},
		media: {dpr: 0.80, pasos: 230, iterBloom: 2},
		alta:  {dpr: 1.00, pasos: 320, iterBloom: 2}
	};
	var calidadActual = (window.innerWidth < 700) ? 'baja' : 'media';

	var escena = new THREE.Scene();
	var camara = new THREE.OrthographicCamera(-1, 1, 1, -1, 0, 1);
	var malla  = new THREE.Mesh(new THREE.PlaneBufferGeometry(2, 2));
	malla.frustumCulled = false;
	escena.add(malla);

	var VERT = 'void main(){ gl_Position = vec4(position, 1.0); }';

	var GLSL_COMUN = `
  vec3 decodificar(vec3 e){
    e = min(e, vec3(0.996));
    return e / (1.0 - e);
  }
  vec3 codificar(vec3 c){
    return c / (1.0 + c);
  }
`;

	var uSim = {
		uTime:    {value: 0},
		uRes:     {value: new THREE.Vector2(1, 1)},
		uCamDist: {value: 27.0},
		uYaw:     {value: 0.0},
		uPitch:   {value: 0.12},
		uVel:     {value: 1.0},
		uTemp:    {value: 0.45},
		uDoppler: {value: 1.0},
		uFondo:   {value: 1.0},
		uPasos:   {value: 230.0},
		tTexto:   {value: null},
		uTextoOn: {value: 1.0}
	};

	var FRAG_SIM = GLSL_COMUN + `
uniform float uTime, uCamDist, uYaw, uPitch;
uniform float uVel, uTemp, uDoppler, uFondo, uPasos;
uniform float uTextoOn;
uniform sampler2D tTexto;
uniform vec2  uRes;

float hash21(vec2 p){
  p = fract(p * vec2(123.34, 456.21));
  p += dot(p, p + 45.32);
  return fract(p.x * p.y);
}
float hash31(vec3 p){
  p = fract(p * 0.1031);
  p += dot(p, p.zyx + 31.32);
  return fract((p.x + p.y) * p.z);
}
float noise2(vec2 p){
  vec2 i = floor(p); vec2 f = fract(p);
  f = f * f * (3.0 - 2.0 * f);
  float a = hash21(i);
  float b = hash21(i + vec2(1.0, 0.0));
  float c = hash21(i + vec2(0.0, 1.0));
  float d = hash21(i + vec2(1.0, 1.0));
  return mix(mix(a, b, f.x), mix(c, d, f.x), f.y);
}
float fbm(vec2 p){
  float v = 0.0; float a = 0.55;
  for(int i = 0; i < 4; i++){
    v += a * noise2(p);
    p = p * 2.13 + vec2(13.7, 7.1);
    a *= 0.5;
  }
  return v;
}

vec3 cielo(vec3 rd){
  vec3 col = vec3(0.0);
  for(int capa = 0; capa < 4; capa++){
    float fc = float(capa);
    float esc = 140.0 + fc * 200.0;
    vec3 q = rd * esc;
    vec3 id = floor(q);
    float h = hash31(id);
    if(h > 0.990 - fc * 0.0025){
      vec3 c = fract(q) - 0.5;
      float d = length(c);
      float b = 1.0 - smoothstep(0.0, 0.5, d);
      b = pow(b, 12.0) * (0.5 + 1.6 * fract(h * 91.7));
      vec3 tinte = mix(vec3(0.65, 0.78, 1.0), vec3(1.0, 0.83, 0.62), fract(h * 53.1));
      if(fract(h * 17.3) > 0.90) b *= 6.0;
      col += b * tinte * 2.0;
    }
  }
  float n1 = fbm(rd.xy * 2.0 + rd.z * 1.3);
  float n2 = fbm(rd.zy * 3.1 - rd.x * 1.7 + 5.0);
  vec3 gas = vec3(0.020, 0.045, 0.110) * pow(n1, 2.6) * 0.50
           + vec3(0.090, 0.040, 0.022) * pow(n2, 3.2) * 0.40;
  float banda = exp(-pow((rd.y + 0.16) * 2.6, 2.0));
  float polvo = fbm(rd.xz * 5.0 + 2.3) * 0.7 + fbm(rd.xz * 11.0) * 0.5;
  gas += (vec3(0.05, 0.06, 0.10) + vec3(0.06, 0.04, 0.02) * polvo) * banda * polvo * 0.30;
  float oscuro = smoothstep(0.45, 0.75, fbm(rd.xz * 7.0 + 9.1));
  gas *= mix(1.0, 0.25, oscuro * banda);
  col += gas * uFondo;
  return col;
}

vec3 colorGas(float r, float rIn, float rOut){
  float t = clamp((r - rIn) / (rOut - rIn), 0.0, 1.0);
  vec3 nucleo = mix(vec3(1.00, 0.98, 0.94), vec3(0.80, 0.90, 1.00), uTemp);
  vec3 medio  = vec3(1.00, 0.60, 0.20);
  vec3 borde  = vec3(0.50, 0.14, 0.03);
  vec3 c = mix(nucleo, medio, smoothstep(0.0, 0.40, t));
  return mix(c, borde, smoothstep(0.40, 1.0, t));
}

vec4 disco(vec3 p, vec3 rd, float rIn, float rOut){
  float r = length(p.xz);
  if(r < rIn - 0.4 || r > rOut) return vec4(0.0);
  float H = 0.085 + 0.34 * pow(clamp((r - 2.0) / 11.0, 0.0, 1.0), 1.7);
  float y = p.y / H;
  if(abs(y) > 3.5) return vec4(0.0);
  float vertical = exp(-y * y * 2.1);
  float bruma = exp(-y * y * 0.45) * 0.16;

  float ang = atan(p.z, p.x);
  float omega = uVel * 0.9 / pow(r, 1.5);
  float a1 = ang + uTime * omega * 9.0;

  float brazos = fbm(vec2(r * 2.2, a1 * 2.4));
  float hebras = fbm(vec2(r * 14.0 - uTime * 0.05, a1 * 1.3) + 7.3);
  float hilos  = noise2(vec2(r * 46.0, a1 * 4.0));
  float espiral = fbm(vec2(r * 5.0, a1 * 3.5 + r * 2.2));
  float grumos  = pow(noise2(vec2(r * 3.5, a1 * 6.0)), 3.0);
  float dens = brazos * 0.42 + hebras * 0.38 + hilos * 0.14
             + espiral * 0.30 + grumos * 0.55;
  dens = smoothstep(0.12, 1.05, dens);
  dens = dens * dens * (1.2 + 0.5 * hebras);
  dens = dens * vertical + bruma * (0.4 + 0.6 * brazos);
  dens *= smoothstep(rIn - 0.4, rIn + 0.45, r);
  dens *= 1.0 - smoothstep(rOut - 2.6, rOut, r);

  if(dens < 0.003) return vec4(0.0);

  float perfil = pow(3.0 / r, 1.9);

  float beta = clamp(sqrt(0.5 / max(r - 1.0, 0.4)), 0.0, 0.85) * min(uVel, 1.6);
  vec3 velDir = normalize(vec3(-p.z, 0.0, p.x));
  float coseno = dot(rd, velDir);
  float dop = 1.0 / max(1.0 - beta * coseno, 0.15);
  float beaming = mix(1.0, pow(dop, 3.0), uDoppler);
  float shift = uDoppler * clamp(beta * coseno, -1.0, 1.0);

  float zGrav = sqrt(max(1.0 - 1.0 / r, 0.05));
  beaming *= mix(1.0, zGrav * zGrav, uDoppler * 0.7);

  vec3 col = colorGas(r, rIn, rOut);
  col = mix(col, vec3(1.0, 0.99, 0.95), clamp(perfil * 0.45, 0.0, 0.9));
  col = mix(col, vec3(0.72, 0.84, 1.00), max(shift, 0.0) * 0.55);
  col = mix(col, vec3(0.85, 0.25, 0.07), max(-shift, 0.0) * 0.6);

  return vec4(col * perfil * beaming * dens, dens);
}

void main(){
  vec2 uv = (gl_FragCoord.xy - 0.5 * uRes) / uRes.y;

  float cy = cos(uYaw); float sy = sin(uYaw);
  float cp = cos(uPitch); float sp = sin(uPitch);
  vec3 ro = uCamDist * vec3(cy * cp, sp, sy * cp);
  vec3 fw = normalize(-ro);
  vec3 rt = normalize(cross(fw, vec3(0.0, 1.0, 0.0)));
  vec3 up = cross(rt, fw);
  vec3 rd = normalize(fw * 1.5 + uv.x * rt + uv.y * up);

  vec3 p = ro;
  vec3 v = rd;
  vec3 hVec = cross(p, v);
  float h2 = dot(hVec, hVec);

  float rIn = 3.0; float rOut = 13.0;

  vec3 col = vec3(0.0);
  float transmit = 1.0;
  float capturado = 0.0;
  float minR = 100000.0;

  vec3 aDir = vec3(cy, 0.0, sy);
  vec3 tDir = vec3(-sy, 0.0, cy);
  float sPrev = dot(p, aDir) + 20.0;

  for(int i = 0; i < 480; i++){
    if(float(i) >= uPasos) break;

    float r2 = dot(p, p);
    float r  = sqrt(r2);
    minR = min(minR, r);

    float dt = clamp(r * 0.065, 0.018, 0.42);
    float grosor = 0.085 + 0.34 * pow(clamp((r - 2.0) / 11.0, 0.0, 1.0), 1.7);
    if(abs(p.y) < grosor * 3.5 && r > rIn - 1.0 && r < rOut + 0.5) dt *= 0.45;

    vec3 a = -1.5 * h2 * p / (r2 * r2 * r);
    v += a * dt;
    p += v * dt;

    if(dot(p, p) < 1.0){ capturado = 1.0; break; }

    if(transmit > 0.012){
      vec4 d = disco(p, normalize(v), rIn, rOut);
      if(d.a > 0.0){
        col += d.rgb * transmit * dt * 4.6;
        transmit *= exp(-d.a * dt * 2.8);
      }
    }

    if(uTextoOn > 0.5 && transmit > 0.012){
      float sNow = dot(p, aDir) + 20.0;
      if(sPrev * sNow < 0.0){
        float f = sPrev / (sPrev - sNow);
        vec3 q = mix(p - v * dt, p, f);
        vec2 uvT = vec2(fract(0.5 - dot(q, tDir) / 38.0 - uTime * 0.045),
                        0.5 + q.y / 19.0);
        if(uvT.y > 0.001 && uvT.y < 0.999){
          vec4 tx = texture2D(tTexto, uvT);
          col += tx.rgb * tx.a * transmit * 1.7;
          transmit *= (1.0 - tx.a * 0.92);
        }
      }
      sPrev = sNow;
    }

    if(dot(p, p) > 1400.0) break;
  }

  if(capturado < 0.5 && transmit > 0.012){
    col += cielo(normalize(v)) * transmit;
  }

  float halo = exp(-abs(minR - 1.5) * 3.0);
  col += vec3(1.0, 0.80, 0.52) * halo * 0.45 * mix(1.0, 0.35, capturado);
  col += vec3(1.0, 0.62, 0.32) * exp(-minR * 0.34) * 0.10;

  gl_FragColor = vec4(codificar(col), 1.0);
}
`;

	var uBright = { tSrc:{value:null}, uUmbral:{value:0.85} };
	var FRAG_BRIGHT = GLSL_COMUN + `
uniform sampler2D tSrc;
uniform float uUmbral;
varying vec2 vUv;
void main(){
  vec3 c = decodificar(texture2D(tSrc, vUv).rgb);
  c = max(c - uUmbral, vec3(0.0));
  gl_FragColor = vec4(codificar(c), 1.0);
}
`;

	var uBlur = {
		tSrc: {value: null},
		uDir: {value: new THREE.Vector2(1, 0)},
		uRes: {value: new THREE.Vector2(1, 1)}
	};
	var FRAG_BLUR = GLSL_COMUN + `
uniform sampler2D tSrc;
uniform vec2 uDir, uRes;
varying vec2 vUv;
void main(){
  vec2 px = uDir / uRes;
  vec3 suma = decodificar(texture2D(tSrc, vUv).rgb) * 0.227;
  float pesos[4];
  pesos[0] = 0.194; pesos[1] = 0.121; pesos[2] = 0.054; pesos[3] = 0.016;
  for(int i = 1; i <= 4; i++){
    float o = float(i) * 1.6;
    suma += decodificar(texture2D(tSrc, vUv + px * o).rgb) * pesos[i-1];
    suma += decodificar(texture2D(tSrc, vUv - px * o).rgb) * pesos[i-1];
  }
  gl_FragColor = vec4(codificar(suma), 1.0);
}
`;

	var uComp = {
		tEscena: {value: null},
		tBloom:  {value: null},
		uFuerza: {value: 0.9},
		uExpo:   {value: 1.0},
		uTime:   {value: 0},
		uAspecto:{value: 1.0}
	};
	var FRAG_COMP = GLSL_COMUN + `
uniform sampler2D tEscena, tBloom;
uniform float uFuerza, uExpo, uTime, uAspecto;
varying vec2 vUv;

float hash(vec2 p){
  p = fract(p * vec2(123.34, 456.21));
  p += dot(p, p + 45.32);
  return fract(p.x * p.y);
}
vec3 aces(vec3 x){
  return clamp((x * (2.51 * x + 0.03)) / (x * (2.43 * x + 0.59) + 0.14), 0.0, 1.0);
}
void main(){
  vec2 centro = vUv - 0.5;
  centro.x *= uAspecto;
  float radial = length(centro);

  vec2 dir = (vUv - 0.5) * radial * 0.012;
  float r = decodificar(texture2D(tEscena, vUv + dir).rgb).r;
  float g = decodificar(texture2D(tEscena, vUv).rgb).g;
  float b = decodificar(texture2D(tEscena, vUv - dir).rgb).b;
  vec3 col = vec3(r, g, b);

  col += decodificar(texture2D(tBloom, vUv).rgb) * uFuerza;
  col += decodificar(texture2D(tBloom, vec2(1.0) - vUv).rgb)
         * vec3(0.55, 0.70, 1.00) * 0.06;

  col *= uExpo;
  col *= vec3(1.06, 0.99, 0.88);
  float lum = dot(col, vec3(0.299, 0.587, 0.114));
  col = mix(vec3(lum), col, 0.92);

  col = aces(col);
  col = pow(col, vec3(1.0 / 1.10));
  col *= 1.0 - smoothstep(0.45, 1.05, radial) * 0.55;
  col += (hash(gl_FragCoord.xy + fract(uTime) * 100.0) - 0.5) * 0.022;

  gl_FragColor = vec4(col, 1.0);
}
`;

	var VERT_UV = `
varying vec2 vUv;
void main(){
  vUv = uv;
  gl_Position = vec4(position, 1.0);
}
`;

	var matSim    = new THREE.ShaderMaterial({uniforms: uSim,    vertexShader: VERT,    fragmentShader: FRAG_SIM});
	var matBright = new THREE.ShaderMaterial({uniforms: uBright, vertexShader: VERT_UV, fragmentShader: FRAG_BRIGHT});
	var matBlur   = new THREE.ShaderMaterial({uniforms: uBlur,   vertexShader: VERT_UV, fragmentShader: FRAG_BLUR});
	var matComp   = new THREE.ShaderMaterial({uniforms: uComp,   vertexShader: VERT_UV, fragmentShader: FRAG_COMP});

	/* Text banner hung in space behind the hole, bent by the lens */
	var lienzoTexto = document.createElement('canvas');
	lienzoTexto.width = 2048; lienzoTexto.height = 1024;
	var ctxT = lienzoTexto.getContext('2d');
	var texturaTexto = new THREE.CanvasTexture(lienzoTexto);
	texturaTexto.minFilter = THREE.LinearFilter;
	texturaTexto.magFilter = THREE.LinearFilter;
	texturaTexto.generateMipmaps = false;
	texturaTexto.wrapS = THREE.ClampToEdgeWrapping;
	texturaTexto.wrapT = THREE.ClampToEdgeWrapping;
	uSim.tTexto.value = texturaTexto;

	function dibujarTexto(str){
		var W = lienzoTexto.width, H = lienzoTexto.height;
		ctxT.clearRect(0, 0, W, H);
		str = (str || '').trim().toUpperCase();
		uSim.uTextoOn.value = str ? 1 : 0;
		if(!str){ texturaTexto.needsUpdate = true; return; }

		var tracking = 0.42;
		var tam = 250;
		var fuente = function(t){ return '700 ' + t + 'px "Archivo Narrow", "Arial Narrow", "Helvetica Neue", Arial, sans-serif'; };
		ctxT.font = fuente(tam);

		function anchoTotal(s){
			var w = 0;
			for(var i = 0; i < s.length; i++){
				w += ctxT.measureText(s[i]).width;
				if(i < s.length - 1) w += tracking * tam;
			}
			return w;
		}

		var margen = 130;
		var w = anchoTotal(str);
		if(w > W - margen * 2){
			tam = Math.max(64, tam * (W - margen * 2) / w);
			ctxT.font = fuente(tam);
			w = anchoTotal(str);
		}

		var x = (W - w) / 2;
		var y = H * 0.50;
		ctxT.textBaseline = 'middle';

		ctxT.shadowColor = 'rgba(255,180,94,0.85)';
		ctxT.shadowBlur = 48;
		ctxT.fillStyle = '#fff3df';
		for(var i = 0; i < str.length; i++){
			ctxT.fillText(str[i], x, y);
			x += ctxT.measureText(str[i]).width + tracking * tam;
		}
		ctxT.shadowBlur = 0;

		var lw = Math.min(w * 1.04, W - margen * 2);
		var lx = (W - lw) / 2;
		ctxT.fillStyle = 'rgba(255,243,223,0.7)';
		ctxT.fillRect(lx, y - tam * 0.74, lw, 4);
		ctxT.fillRect(lx, y + tam * 0.66, lw, 4);

		ctxT.font = '400 42px "JetBrains Mono", "Courier New", monospace';
		var sub = 'S A T E L L I T E   S E R V I C I N G   ·   L E O  —  G E O';
		var sw = ctxT.measureText(sub).width;
		if(sw < lw){
			ctxT.fillStyle = 'rgba(255,200,140,0.9)';
			ctxT.fillText(sub, (W - sw) / 2, y + tam * 0.66 + 66);
		}

		ctxT.save();
		ctxT.translate(48, H * 0.50);
		ctxT.rotate(Math.PI / 4);
		ctxT.shadowColor = 'rgba(255,180,94,0.8)';
		ctxT.shadowBlur = 28;
		ctxT.fillStyle = 'rgba(255,200,140,0.95)';
		ctxT.fillRect(-15, -15, 30, 30);
		ctxT.restore();

		texturaTexto.needsUpdate = true;
	}
	/* banner text removed for a clean scene: keep the texture blank */
	dibujarTexto('');

	var rtEscena = null, rtA = null, rtB = null;
	function crearRT(w, h){
		return new THREE.WebGLRenderTarget(Math.max(2, w|0), Math.max(2, h|0), {
			minFilter: THREE.LinearFilter, magFilter: THREE.LinearFilter,
			format: THREE.RGBAFormat, depthBuffer: false, stencilBuffer: false
		});
	}
	function reconstruirRTs(){
		if(rtEscena){ rtEscena.dispose(); rtA.dispose(); rtB.dispose(); }
		var pr = renderer.getPixelRatio();
		var W = window.innerWidth * pr, H = window.innerHeight * pr;
		rtEscena = crearRT(W, H);
		rtA = crearRT(W * 0.5, H * 0.5);
		rtB = crearRT(W * 0.5, H * 0.5);
	}

	function aplicarCalidad(nombre){
		calidadActual = nombre;
		var q = calidades[nombre];
		renderer.setPixelRatio(baseDPR * q.dpr);
		renderer.setSize(window.innerWidth, window.innerHeight);
		uSim.uPasos.value = q.pasos;
		uSim.uRes.value.set(window.innerWidth * renderer.getPixelRatio(),
			window.innerHeight * renderer.getPixelRatio());
		uComp.uAspecto.value = window.innerWidth / window.innerHeight;
		reconstruirRTs();
		['qBaja','qMedia','qAlta'].forEach(function(id){
			var el = document.getElementById(id);
			if(el) el.classList.toggle('on', id.toLowerCase() === 'q' + nombre);
		});
	}
	aplicarCalidad(calidadActual);

	try{
		malla.material = matSim; renderer.compile(escena, camara);
		malla.material = matComp; renderer.compile(escena, camara);
		var progs = renderer.info.programs;
		for(var i = 0; i < progs.length; i++){
			if(progs[i].diagnostics && !progs[i].diagnostics.runnable){
				var d = progs[i].diagnostics;
				mostrarError('The shader did not compile on your GPU.\n\nFragment: ' +
					(d.fragmentShader ? d.fragmentShader.log : '-'));
			}
		}
	}catch(e){ mostrarError('Shader compilation failed: ' + e.message); }

	/* Interaction: drag to orbit, page scroll dives toward the horizon */
	var yaw = 0, pitch = 0.12, dist = 27;
	var autoOrbita = true;
	var arrastrando = false, px = 0, py = 0;
	var lienzo = renderer.domElement;
	var scrollSuave = 0;

	lienzo.addEventListener('pointerdown', function(e){
		arrastrando = true; px = e.clientX; py = e.clientY;
		try{ lienzo.setPointerCapture(e.pointerId); }catch(_){}
	});
	lienzo.addEventListener('pointermove', function(e){
		if(!arrastrando) return;
		yaw   += (e.clientX - px) * 0.005;
		pitch += (e.clientY - py) * 0.004;
		pitch = Math.max(-1.35, Math.min(1.35, pitch));
		px = e.clientX; py = e.clientY;
	});
	lienzo.addEventListener('pointerup',     function(){ arrastrando = false; });
	lienzo.addEventListener('pointercancel', function(){ arrastrando = false; });
	lienzo.addEventListener('dblclick', function(){ yaw = 0; pitch = 0.12; dist = 27; });

	function liga(idSlider, idValor, obj, clave){
		var s = document.getElementById(idSlider);
		var v = document.getElementById(idValor);
		if(!s || !v) return;
		function sync(){
			obj[clave].value = parseFloat(s.value);
			v.textContent = parseFloat(s.value).toFixed(2);
		}
		s.addEventListener('input', sync);
		sync();
	}
	liga('sBrillo', 'vBrillo', uComp, 'uExpo');
	liga('sBloom',  'vBloom',  uComp, 'uFuerza');
	liga('sVel',    'vVel',    uSim,  'uVel');
	liga('sTemp',   'vTemp',   uSim,  'uTemp');


	function togglear(idBoton, obj, clave, alCambiar){
		var b = document.getElementById(idBoton);
		if(!b) return;
		b.addEventListener('click', function(){
			var on = !b.classList.contains('on');
			b.classList.toggle('on', on);
			if(obj) obj[clave].value = on ? 1 : 0;
			if(alCambiar) alCambiar(on);
		});
	}
	togglear('bDoppler', uSim, 'uDoppler');
	togglear('bFondo',   uSim, 'uFondo');
	togglear('bAuto', null, null, function(on){ autoOrbita = on; });


	var quieto = !!(window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches);
	if(quieto){
		autoOrbita = false;
	}

	var anchoPrevio = window.innerWidth;
	window.addEventListener('resize', function(){
		/* ignore mobile URL-bar height jitter; rebuild on real size changes */
		if(Math.abs(window.innerWidth - anchoPrevio) > 2 || !/Mobi/.test(navigator.userAgent)){
			anchoPrevio = window.innerWidth;
			aplicarCalidad(calidadActual);
		}
	});

	/* automatic downgrade if under ~28 fps */
	var muestrasFPS = 0, acumFPS = 0, degradado = false;

	var tPrev = performance.now();
	function animar(t){
		requestAnimationFrame(animar);
		if(document.hidden) return;
		var dt = Math.min((t - tPrev) / 1000, 0.05);
		tPrev = t;

		if(!degradado && muestrasFPS < 90){
			muestrasFPS++; acumFPS += dt;
			if(muestrasFPS === 90 && acumFPS / 90 > 1/28){
				degradado = true;
				if(calidadActual === 'alta') aplicarCalidad('media');
				else if(calidadActual === 'media') aplicarCalidad('baja');
			}
		}

		if(autoOrbita && !arrastrando) yaw += dt * 0.04;

		/* scroll progress pulls the camera in and tilts it over the disc */
		var maxScroll = Math.max(1, document.documentElement.scrollHeight - window.innerHeight);
		var objetivo = Math.min(1, window.scrollY / maxScroll);
		scrollSuave += (objetivo - scrollSuave) * Math.min(1, dt * 4);

		uSim.uTime.value    = quieto ? 12 : t / 1000;
		uSim.uYaw.value     = yaw + scrollSuave * 0.9;
		uSim.uPitch.value   = Math.max(-1.35, Math.min(1.35, pitch + scrollSuave * 0.38));
		uSim.uCamDist.value = Math.max(6.0, dist * (1 - scrollSuave * 0.5));
		uComp.uTime.value   = t / 1000;

		malla.material = matSim;
		renderer.setRenderTarget(rtEscena);
		renderer.render(escena, camara);

		malla.material = matBright;
		uBright.tSrc.value = rtEscena.texture;
		renderer.setRenderTarget(rtA);
		renderer.render(escena, camara);

		var iter = calidades[calidadActual].iterBloom;
		malla.material = matBlur;
		for(var k = 0; k < iter; k++){
			uBlur.uRes.value.set(rtA.width, rtA.height);
			uBlur.uDir.value.set(1 + k, 0);
			uBlur.tSrc.value = rtA.texture;
			renderer.setRenderTarget(rtB);
			renderer.render(escena, camara);

			uBlur.uDir.value.set(0, 1 + k);
			uBlur.tSrc.value = rtB.texture;
			renderer.setRenderTarget(rtA);
			renderer.render(escena, camara);
		}

		malla.material = matComp;
		uComp.tEscena.value = rtEscena.texture;
		uComp.tBloom.value  = rtA.texture;
		renderer.setRenderTarget(null);
		renderer.render(escena, camara);
	}
	requestAnimationFrame(animar);
})();
</script>
<script>
/* =====================================================================
   Card vitrines: live 3D scenes for the fleet and service cards.
   One shared WebGL renderer draws every visible scene into its own
   2D canvas, so nine views cost one GPU context instead of nine.
   ===================================================================== */
(function(){
	'use strict';
	if(typeof THREE === 'undefined') return;
	var contenedores = document.querySelectorAll('[data-vitrina]');
	if(!contenedores.length) return;
	var reducido = window.matchMedia && window.matchMedia('(prefers-reduced-motion: reduce)').matches;
	var DPR = Math.min(window.devicePixelRatio || 1, 2);
	var V3 = THREE.Vector3, PI = Math.PI;

	var ren;
	try{ ren = new THREE.WebGLRenderer({antialias:true, alpha:true, powerPreference:'low-power'}); }catch(e){ return; }
	if(!ren.getContext()) return;
	ren.setPixelRatio(1);
	ren.setClearColor(0x000000, 0);
	ren.outputEncoding = THREE.sRGBEncoding;
	ren.toneMapping = THREE.ACESFilmicToneMapping;
	ren.toneMappingExposure = 1.15;
	var glW = 0, glH = 0;

	/* ---------------- maths helpers ---------------- */
	function clamp(x, a, b){ return Math.max(a, Math.min(b, x)); }
	function suave(x){ x = clamp(x, 0, 1); return x * x * (3 - 2 * x); }
	function tramo(t, a, b){ return clamp((t - a) / (b - a), 0, 1); }
	function easeOut(x){ x = clamp(x, 0, 1); return 1 - Math.pow(1 - x, 3); }
	function easeIn(x){ x = clamp(x, 0, 1); return x * x * x; }
	function miles(n){ return Math.round(n).toString().replace(/\B(?=(\d{3})+(?!\d))/g, ','); }

	/* ---------------- procedural textures ---------------- */
	function lienzo(w, h){ var c = document.createElement('canvas'); c.width = w; c.height = h; return c; }
	function tex(c, srgb){ var t = new THREE.CanvasTexture(c); if(srgb !== false) t.encoding = THREE.sRGBEncoding; t.anisotropy = 4; return t; }

	function texPanel(){
		var c = lienzo(512, 256), x = c.getContext('2d');
		var g = x.createLinearGradient(0, 0, 512, 256);
		g.addColorStop(0, '#1b2c4a'); g.addColorStop(.55, '#0c1528'); g.addColorStop(1, '#060a14');
		x.fillStyle = g; x.fillRect(0, 0, 512, 256);
		for(var i = 0; i < 16; i++) for(var j = 0; j < 8; j++){
			var v = .9 + Math.random() * .2;
			x.fillStyle = 'rgba(' + (40 * v | 0) + ',' + (70 * v | 0) + ',' + (120 * v | 0) + ',.35)';
			x.fillRect(i * 32 + 2, j * 32 + 2, 28, 28);
		}
		x.strokeStyle = 'rgba(255,190,120,.55)'; x.lineWidth = 3; x.strokeRect(2, 2, 508, 252);
		x.lineWidth = 1.2; x.strokeStyle = 'rgba(255,190,120,.22)';
		for(i = 0; i <= 16; i++){ x.beginPath(); x.moveTo(i * 32, 0); x.lineTo(i * 32, 256); x.stroke(); }
		for(j = 0; j <= 8; j++){ x.beginPath(); x.moveTo(0, j * 32); x.lineTo(512, j * 32); x.stroke(); }
		return tex(c);
	}
	function texArrugado(base, claro, oscuro){
		var c = lienzo(256, 256), x = c.getContext('2d');
		x.fillStyle = base; x.fillRect(0, 0, 256, 256);
		for(var i = 0; i < 260; i++){
			var cx = Math.random() * 256, cy = Math.random() * 256, r = 6 + Math.random() * 22;
			x.fillStyle = Math.random() > .5 ? claro.replace('A', (Math.random() * .35).toFixed(2)) : oscuro.replace('A', (Math.random() * .35).toFixed(2));
			x.beginPath(); x.moveTo(cx, cy);
			for(var k = 0; k < 3; k++) x.lineTo(cx + (Math.random() - .5) * r * 2, cy + (Math.random() - .5) * r * 2);
			x.closePath(); x.fill();
		}
		return tex(c);
	}
	function texBrillo(){
		var c = lienzo(128, 128), x = c.getContext('2d');
		var g = x.createRadialGradient(64, 64, 0, 64, 64, 64);
		g.addColorStop(0, 'rgba(255,255,255,1)'); g.addColorStop(.25, 'rgba(255,255,255,.7)');
		g.addColorStop(.6, 'rgba(255,255,255,.16)'); g.addColorStop(1, 'rgba(255,255,255,0)');
		x.fillStyle = g; x.fillRect(0, 0, 128, 128);
		return new THREE.CanvasTexture(c);
	}
	function texEscaneo(){
		var c = lienzo(256, 256), x = c.getContext('2d');
		x.strokeStyle = 'rgba(255,190,120,.55)'; x.lineWidth = 1;
		for(var i = 0; i <= 256; i += 16){
			x.beginPath(); x.moveTo(i, 0); x.lineTo(i, 256); x.stroke();
			x.beginPath(); x.moveTo(0, i); x.lineTo(256, i); x.stroke();
		}
		x.strokeStyle = 'rgba(255,215,160,.95)'; x.lineWidth = 3;
		x.beginPath(); x.arc(128, 128, 118, 0, PI * 2); x.stroke();
		x.globalCompositeOperation = 'destination-in';
		var g = x.createRadialGradient(128, 128, 10, 128, 128, 128);
		g.addColorStop(0, 'rgba(0,0,0,1)'); g.addColorStop(.85, 'rgba(0,0,0,.8)'); g.addColorStop(1, 'rgba(0,0,0,0)');
		x.fillStyle = g; x.fillRect(0, 0, 256, 256);
		return new THREE.CanvasTexture(c);
	}
	/* continent mask shared by both planet styles, drawn as clustered blobs */
	function mascaraContinentes(w, h, semilla){
		var c = lienzo(w, h), x = c.getContext('2d');
		var r = semilla;
		function rnd(){ r = (r * 9301 + 49297) % 233280; return r / 233280; }
		x.fillStyle = '#fff';
		for(var k = 0; k < 7; k++){
			var cx = rnd() * w, cy = h * (.2 + rnd() * .6), n = 14 + (rnd() * 18 | 0);
			for(var i = 0; i < n; i++){
				x.beginPath();
				x.ellipse(cx + (rnd() - .5) * w * .16, cy + (rnd() - .5) * h * .22, 6 + rnd() * w * .05, 4 + rnd() * h * .07, rnd() * PI, 0, PI * 2);
				x.fill();
			}
		}
		return c;
	}
	function texPlanetaNoche(){
		var w = 512, h = 256, m = mascaraContinentes(w, h, 4127);
		var c = lienzo(w, h), x = c.getContext('2d');
		x.fillStyle = '#050c1a'; x.fillRect(0, 0, w, h);
		x.globalAlpha = .9; x.drawImage(m, 0, 0); x.globalCompositeOperation = 'source-atop';
		x.fillStyle = '#1b2232'; x.fillRect(0, 0, w, h); x.globalCompositeOperation = 'source-over'; x.globalAlpha = 1;
		/* re-tint ocean beneath (mask painted white then tinted) */
		var mapa = lienzo(w, h), mx = mapa.getContext('2d');
		mx.fillStyle = '#050c1a'; mx.fillRect(0, 0, w, h);
		var tinte = lienzo(w, h), tx = tinte.getContext('2d');
		tx.drawImage(m, 0, 0); tx.globalCompositeOperation = 'source-in'; tx.fillStyle = '#1f2636'; tx.fillRect(0, 0, w, h);
		mx.drawImage(tinte, 0, 0);
		/* city lights only on land */
		var luces = lienzo(w, h), lx = luces.getContext('2d');
		lx.fillStyle = '#000'; lx.fillRect(0, 0, w, h);
		var datos = m.getContext('2d').getImageData(0, 0, w, h).data;
		for(var i = 0; i < 4200; i++){
			var px = Math.random() * w | 0, py = Math.random() * h | 0;
			if(datos[(py * w + px) * 4 + 3] > 100){
				var a = Math.random();
				lx.fillStyle = 'rgba(255,' + (170 + a * 50 | 0) + ',' + (90 + a * 40 | 0) + ',' + (.35 + a * .65) + ')';
				lx.fillRect(px, py, a > .92 ? 2 : 1, 1);
			}
		}
		return {mapa:tex(mapa), luces:tex(luces)};
	}
	function texPlanetaDia(){
		var w = 1024, h = 512, m = mascaraContinentes(w, h, 811);
		var c = lienzo(w, h), x = c.getContext('2d');
		var g = x.createLinearGradient(0, 0, 0, h);
		g.addColorStop(0, '#173f66'); g.addColorStop(.5, '#0e2c4d'); g.addColorStop(1, '#173f66');
		x.fillStyle = g; x.fillRect(0, 0, w, h);
		var tierra = lienzo(w, h), tx = tierra.getContext('2d');
		tx.drawImage(m, 0, 0); tx.globalCompositeOperation = 'source-in';
		var g2 = tx.createLinearGradient(0, 0, w, h); g2.addColorStop(0, '#6b5636'); g2.addColorStop(.5, '#4f5a33'); g2.addColorStop(1, '#7a6040');
		tx.fillStyle = g2; tx.fillRect(0, 0, w, h);
		x.drawImage(tierra, 0, 0);
		for(var i = 0; i < 260; i++){
			x.fillStyle = 'rgba(245,240,232,' + (.06 + Math.random() * .22) + ')';
			x.beginPath();
			x.ellipse(Math.random() * w, Math.random() * h, 12 + Math.random() * 50, 2 + Math.random() * 5, (Math.random() - .5) * .5, 0, PI * 2);
			x.fill();
		}
		return tex(c);
	}

	/* ---------------- shared materials ---------------- */
	var BRILLO = texBrillo();
	var M = {
		foil:   new THREE.MeshStandardMaterial({color:0xffffff, map:texArrugado('#b8802e', 'rgba(255,224,160,A)', 'rgba(70,35,6,A)'), metalness:.78, roughness:.34, emissive:0x2a1300, emissiveIntensity:.35}),
		plata:  new THREE.MeshStandardMaterial({color:0xffffff, map:texArrugado('#9aa0a8', 'rgba(235,240,250,A)', 'rgba(30,34,42,A)'), metalness:.85, roughness:.3, emissive:0x0c0f14, emissiveIntensity:.4}),
		blanco: new THREE.MeshStandardMaterial({color:0xe2dccf, metalness:.15, roughness:.5}),
		blancoD:new THREE.MeshStandardMaterial({color:0xe2dccf, metalness:.25, roughness:.4, side:THREE.DoubleSide}),
		oscuro: new THREE.MeshStandardMaterial({color:0x2b2723, metalness:.7, roughness:.38}),
		oscuroD:new THREE.MeshStandardMaterial({color:0x3a332c, metalness:.85, roughness:.3, side:THREE.DoubleSide}),
		cromo:  new THREE.MeshStandardMaterial({color:0xb5aea2, metalness:.95, roughness:.22}),
		panel:  new THREE.MeshStandardMaterial({color:0xffffff, map:texPanel(), metalness:.55, roughness:.28, emissive:0x0b1630, emissiveIntensity:.5}),
		ambar:  new THREE.MeshBasicMaterial({color:0xffb45e}),
		hielo:  new THREE.MeshBasicMaterial({color:0x9fc4ff})
	};

	/* ---------------- geometry helpers ---------------- */
	function caja(w, h, d, m){ return new THREE.Mesh(new THREE.BoxGeometry(w, h, d), m); }
	function cil(rt, rb, h, m, seg){ return new THREE.Mesh(new THREE.CylinderGeometry(rt, rb, h, seg || 20), m); }
	function resplandor(escala, color){
		var s = new THREE.Sprite(new THREE.SpriteMaterial({map:BRILLO, color:color === undefined ? 0xffb45e : color, blending:THREE.AdditiveBlending, depthWrite:false, transparent:true}));
		s.scale.setScalar(escala); return s;
	}
	function ala(lado, n, w, h){
		var grupo = new THREE.Group();
		var yugo = cil(.025, .025, .34, M.cromo, 8); yugo.rotation.z = PI / 2; yugo.position.x = lado * .17; grupo.add(yugo);
		for(var i = 0; i < n; i++){
			var p = caja(w, .025, h, M.panel); p.position.x = lado * (.36 + w / 2 + i * (w + .035)); grupo.add(p);
			var b = cil(.018, .018, h * .9, M.cromo, 6); b.rotation.x = PI / 2; b.position.x = lado * (.36 + i * (w + .035) - .017); grupo.add(b);
		}
		return grupo;
	}
	/* stretch a unit-height cylinder between two points */
	var EJE_Y = new V3(0, 1, 0);
	function alinear(mesh, a, b){
		var d = new V3().subVectors(b, a), l = d.length();
		mesh.position.copy(a).addScaledVector(d, .5);
		mesh.scale.set(1, l, 1);
		mesh.quaternion.setFromUnitVectors(EJE_Y, d.normalize());
	}
	function lineaDe(puntos, color, opacidad, discontinua){
		var geo = new THREE.BufferGeometry().setFromPoints(puntos);
		var mat = discontinua
			? new THREE.LineDashedMaterial({color:color, transparent:true, opacity:opacidad, dashSize:.07, gapSize:.06})
			: new THREE.LineBasicMaterial({color:color, transparent:true, opacity:opacidad});
		var l = new THREE.Line(geo, mat); if(discontinua) l.computeLineDistances(); return l;
	}
	function circulo(r, fn){
		var p = []; for(var i = 0; i <= 160; i++){ var a = i / 160 * PI * 2; p.push(fn ? fn(a) : new V3(Math.cos(a) * r, 0, -Math.sin(a) * r)); } return p;
	}
	function estrellas(esc, n, rmin){
		var pos = new Float32Array(n * 3);
		for(var i = 0; i < n; i++){
			var r = rmin + Math.random() * 6, th = Math.random() * PI * 2, ph = Math.acos(2 * Math.random() - 1);
			pos[i * 3] = r * Math.sin(ph) * Math.cos(th); pos[i * 3 + 1] = r * Math.cos(ph); pos[i * 3 + 2] = -Math.abs(r * Math.sin(ph) * Math.sin(th));
		}
		var g = new THREE.BufferGeometry(); g.setAttribute('position', new THREE.BufferAttribute(pos, 3));
		var p = new THREE.Points(g, new THREE.PointsMaterial({color:0xf3e6d0, size:.045, transparent:true, opacity:.7}));
		esc.add(p); return p;
	}
	function luces(esc, tibio){
		esc.add(new THREE.HemisphereLight(0xffe2c0, 0x1a1006, .55));
		var k = new THREE.DirectionalLight(tibio ? 0xffc890 : 0xffd2a2, 2.4); k.position.set(3.5, 4, 5); esc.add(k);
		var r = new THREE.DirectionalLight(0x86aaff, 1.6); r.position.set(-4.5, 1.5, -3.5); esc.add(r);
		var b = new THREE.DirectionalLight(0xff8a3c, .7); b.position.set(0, -4, 2); esc.add(b);
		return k;
	}
	function base(fov, pos, mira){
		var esc = new THREE.Scene();
		var cam = new THREE.PerspectiveCamera(fov, 1.6, .05, 80);
		cam.position.fromArray(pos);
		var l = new V3().fromArray(mira || [0, 0, 0]);
		cam.lookAt(l);
		cam.userData.base = cam.position.clone(); cam.userData.mira = l;
		return {esc:esc, cam:cam};
	}
	function acercar(cam, k){ cam.position.copy(cam.userData.base).lerp(cam.userData.mira, k); cam.lookAt(cam.userData.mira); }
	function atmosfera(r, c1, c2, pot, inten){
		var mat = new THREE.ShaderMaterial({
			uniforms:{c1:{value:new THREE.Color(c1)}, c2:{value:new THREE.Color(c2)}, p:{value:pot}, k:{value:inten}},
			vertexShader:'varying vec3 vN; varying vec3 vV; void main(){ vec4 mv = modelViewMatrix * vec4(position,1.0); vN = normalize(normalMatrix * normal); vV = normalize(-mv.xyz); gl_Position = projectionMatrix * mv; }',
			fragmentShader:'uniform vec3 c1; uniform vec3 c2; uniform float p; uniform float k; varying vec3 vN; varying vec3 vV; void main(){ float f = pow(1.0 - max(dot(vN, vV), 0.0), p); gl_FragColor = vec4(mix(c1, c2, f) * f * k, f); }',
			transparent:true, blending:THREE.AdditiveBlending, depthWrite:false
		});
		return new THREE.Mesh(new THREE.SphereGeometry(r, 64, 40), mat);
	}
	/* pool of additive particles with per-point fading */
	function particulas(n, tam){
		var pos = new Float32Array(n * 3), col = new Float32Array(n * 3);
		var g = new THREE.BufferGeometry();
		g.setAttribute('position', new THREE.BufferAttribute(pos, 3));
		g.setAttribute('color', new THREE.BufferAttribute(col, 3));
		var p = new THREE.Points(g, new THREE.PointsMaterial({size:tam, map:BRILLO, vertexColors:true, transparent:true, blending:THREE.AdditiveBlending, depthWrite:false}));
		p.frustumCulled = false;
		p.userData = {vida:new Float32Array(n), vel:new Float32Array(n * 3), dur:new Float32Array(n), siguiente:0, n:n, tinte:[1, .7, .37]};
		return p;
	}
	function emitir(p, origen, vel, dur){
		var u = p.userData, i = u.siguiente; u.siguiente = (i + 1) % u.n;
		var pos = p.geometry.attributes.position.array;
		pos[i * 3] = origen.x; pos[i * 3 + 1] = origen.y; pos[i * 3 + 2] = origen.z;
		u.vel[i * 3] = vel.x; u.vel[i * 3 + 1] = vel.y; u.vel[i * 3 + 2] = vel.z;
		u.vida[i] = dur; u.dur[i] = dur;
	}
	function avanzarParticulas(p, dt, arrastre){
		var u = p.userData, pos = p.geometry.attributes.position.array, col = p.geometry.attributes.color.array;
		for(var i = 0; i < u.n; i++){
			if(u.vida[i] > 0){
				u.vida[i] -= dt;
				var f = Math.max(0, u.vida[i] / u.dur[i]);
				pos[i * 3] += u.vel[i * 3] * dt; pos[i * 3 + 1] += u.vel[i * 3 + 1] * dt; pos[i * 3 + 2] += u.vel[i * 3 + 2] * dt;
				if(arrastre){ u.vel[i * 3] *= arrastre; u.vel[i * 3 + 1] *= arrastre; u.vel[i * 3 + 2] *= arrastre; }
				col[i * 3] = u.tinte[0] * f; col[i * 3 + 1] = u.tinte[1] * f * f; col[i * 3 + 2] = u.tinte[2] * f * f * f;
			} else { col[i * 3] = col[i * 3 + 1] = col[i * 3 + 2] = 0; }
		}
		p.geometry.attributes.position.needsUpdate = true;
		p.geometry.attributes.color.needsUpdate = true;
	}
	function apagarParticulas(p){ p.userData.vida.fill(0); avanzarParticulas(p, 0); }

	/* =====================================================================
	   FLEET — the three company spacecraft
	   ===================================================================== */
	function construirNave(tipo){
		var g = new THREE.Group(), anim = [];
		if(tipo === 'warden'){
			g.add(caja(1, 1, 1.1, M.foil));
			var t1 = caja(1.04, .05, 1.14, M.blanco); t1.position.y = .53; g.add(t1);
			var t2 = t1.clone(); t2.position.y = -.53; g.add(t2);
			var izq = ala(-1, 3, .6, .74), der = ala(1, 3, .6, .74);
			izq.position.x = -.5; der.position.x = .5; g.add(izq, der);
			anim.push(function(t){ izq.rotation.x = der.rotation.x = Math.sin(t * .35) * .3; });
			var mastil = cil(.03, .03, .32, M.cromo, 8); mastil.position.set(.18, .7, -.15); g.add(mastil);
			var plato = new THREE.Mesh(new THREE.SphereGeometry(.34, 32, 10, 0, PI * 2, 0, .85), M.blancoD);
			plato.rotation.x = PI; plato.position.set(.18, 1.08, -.15);
			var platoG = new THREE.Group(); platoG.add(plato); g.add(platoG);
			var alim = cil(.012, .012, .3, M.cromo, 6); alim.position.set(.18, .98, -.15); g.add(alim);
			anim.push(function(t){ platoG.rotation.z = Math.sin(t * .5) * .06; });
			var anillo = new THREE.Mesh(new THREE.TorusGeometry(.3, .028, 10, 48), M.cromo); anillo.position.z = .58; g.add(anillo);
			var sonda = new THREE.Mesh(new THREE.ConeGeometry(.12, .5, 24), M.cromo); sonda.rotation.x = PI / 2; sonda.position.z = .86; g.add(sonda);
			var punta = resplandor(.28); punta.position.z = 1.12; g.add(punta);
			anim.push(function(t){ punta.material.opacity = .55 + .45 * Math.abs(Math.sin(t * 2.2)); });
			function brazo(x){
				var b = new THREE.Group(); b.position.set(x, .38, .5);
				b.add(new THREE.Mesh(new THREE.SphereGeometry(.07, 14, 14), M.oscuro));
				var hombro = new THREE.Group();
				var s1 = cil(.032, .032, .5, M.blanco, 10); s1.position.y = .25; hombro.add(s1);
				var codo = new THREE.Group(); codo.position.y = .5;
				codo.add(new THREE.Mesh(new THREE.SphereGeometry(.055, 12, 12), M.oscuro));
				var s2 = cil(.028, .028, .42, M.blanco, 10); s2.position.y = .21; codo.add(s2);
				var mu = new THREE.Group(); mu.position.y = .44;
				var d1 = caja(.02, .1, .02, M.ambar); d1.position.set(-.03, .05, 0);
				var d2 = d1.clone(); d2.position.x = .03; mu.add(d1, d2); codo.add(mu);
				hombro.add(codo); b.add(hombro); g.add(b);
				return {hombro:hombro, codo:codo, d1:d1, d2:d2};
			}
			var b1 = brazo(-.33), b2 = brazo(.33);
			anim.push(function(t){
				b1.hombro.rotation.x = .75 + Math.sin(t * .8) * .28;  b1.codo.rotation.x = .85 + Math.sin(t * .8 + 1.2) * .4;
				b2.hombro.rotation.x = .75 + Math.sin(t * .8 + 2.4) * .28; b2.codo.rotation.x = .85 + Math.sin(t * .8 + 3.6) * .4;
				var a = .03 + Math.abs(Math.sin(t * 1.6)) * .025;
				b1.d1.position.x = b2.d1.position.x = -a; b1.d2.position.x = b2.d2.position.x = a;
			});
			var tob = cil(.11, .22, .3, M.oscuroD, 24); tob.rotation.x = PI / 2; tob.position.z = -.7; g.add(tob);
			var llama = resplandor(.9); llama.position.z = -.92; g.add(llama);
			anim.push(function(t){ llama.scale.setScalar(.9 * (.8 + Math.sin(t * 9) * .06 + Math.sin(t * 23) * .04)); });
		}
		else if(tipo === 'tern'){
			g.add(cil(.42, .42, .85, M.foil, 6));
			var c1 = cil(.45, .45, .05, M.blanco, 6); c1.position.y = .45; g.add(c1);
			var c2 = c1.clone(); c2.position.y = -.45; g.add(c2);
			var aI = ala(-1, 2, .55, .6), aD = ala(1, 2, .55, .6);
			aI.position.x = -.38; aD.position.x = .38; aI.rotation.z = .14; aD.rotation.z = -.14; g.add(aI, aD);
			anim.push(function(t){ aI.rotation.x = aD.rotation.x = Math.sin(t * .4 + 1) * .22; });
			var boom = cil(.025, .025, .9, M.cromo, 8); boom.position.y = .92; g.add(boom);
			var cabeza = new THREE.Group(); cabeza.position.y = 1.4; g.add(cabeza);
			cabeza.add(new THREE.Mesh(new THREE.SphereGeometry(.15, 24, 18), M.cromo));
			var lente = cil(.08, .08, .08, M.ambar, 20); lente.rotation.x = PI / 2; lente.position.z = .14; cabeza.add(lente);
			var haz = new THREE.Mesh(new THREE.ConeGeometry(.42, 1.6, 32, 1, true),
				new THREE.MeshBasicMaterial({color:0xff9a3c, transparent:true, opacity:.1, blending:THREE.AdditiveBlending, depthWrite:false, side:THREE.DoubleSide}));
			haz.rotation.x = -PI / 2; haz.position.z = .95; cabeza.add(haz);
			var foco = resplandor(.36); foco.position.z = .2; cabeza.add(foco);
			anim.push(function(t){ cabeza.rotation.y = Math.sin(t * .7) * 1.1; cabeza.rotation.x = Math.sin(t * .45) * .25; haz.material.opacity = .07 + .06 * Math.abs(Math.sin(t * 3)); });
			[-1, 1].forEach(function(s){ var w = cil(.008, .008, .7, M.cromo, 4); w.position.set(s * .25, -.8, .2); w.rotation.z = s * .3; g.add(w); });
			var tb = cil(.07, .13, .18, M.oscuroD, 16); tb.position.y = -.58; g.add(tb);
			var ch = resplandor(.55); ch.position.y = -.72; g.add(ch);
			anim.push(function(t){ ch.material.opacity = .45 + .4 * Math.max(0, Math.sin(t * 1.3)); });
		}
		else {
			var cuerpo = cil(.32, .32, 1.2, M.blanco, 32); g.add(cuerpo);
			[-1, 1].forEach(function(s){
				var tq = new THREE.Mesh(new THREE.SphereGeometry(.5, 32, 24), M.foil); tq.position.y = s * .85; g.add(tq);
				var ci = new THREE.Mesh(new THREE.TorusGeometry(.5, .025, 8, 48), M.cromo); ci.rotation.x = PI / 2; ci.position.y = s * .85; g.add(ci);
			});
			var lz = [];
			for(var i = 0; i < 4; i++){
				var pu = new THREE.Group(); pu.rotation.y = i * PI / 2;
				var tu = cil(.11, .11, .26, M.oscuro, 20); tu.rotation.z = PI / 2; tu.position.x = .42; pu.add(tu);
				var ar = new THREE.Mesh(new THREE.TorusGeometry(.13, .022, 8, 32), M.cromo); ar.rotation.y = PI / 2; ar.position.x = .56; pu.add(ar);
				var l = resplandor(.3); l.position.set(.6, .17, 0); pu.add(l); lz.push(l);
				g.add(pu);
			}
			anim.push(function(t){ lz.forEach(function(l, k){ l.material.opacity = Math.max(.05, Math.sin(t * 2.4 - k * 1.57)); }); });
			var truss = cil(.03, .03, 2.6, M.cromo, 8); truss.rotation.z = PI / 2; g.add(truss);
			var pan = new THREE.Group(); g.add(pan);
			[-1, 1].forEach(function(s){ var p = caja(.75, .025, .62, M.panel); p.position.x = s; pan.add(p); var p2 = p.clone(); p2.position.x = s * 1.82; pan.add(p2); });
			anim.push(function(t){ pan.rotation.x = t * .25; cuerpo.rotation.y = t * .3; });
		}
		var bb = new THREE.Box3().setFromObject(g), tam = new V3(), cen = new V3();
		bb.getSize(tam); bb.getCenter(cen);
		g.children.forEach(function(c){ c.position.sub(cen); });
		var env = new THREE.Group(); env.add(g);
		env.scale.setScalar(({warden:3.35, tern:2.75, depot:3.5}[tipo] || 2.8) / Math.max(tam.x, tam.y, tam.z));
		return {grupo:env, anim:anim};
	}
	function escenaFlota(tipo, idx){
		var e = base(30, [0, .5, 5.8]);
		luces(e.esc);
		var est = estrellas(e.esc, 160, 9);
		var orb = new THREE.Group(); orb.rotation.set(1.25, 0, .22); e.esc.add(orb);
		orb.add(lineaDe(circulo(2.05, function(a){ return new V3(Math.cos(a) * 2.05, Math.sin(a) * 2.05, 0); }), 0xffb45e, .4, true));
		var traz = resplandor(.32); orb.add(traz);
		var mod = construirNave(tipo), piv = new THREE.Group(); piv.add(mod.grupo); e.esc.add(piv);
		var giro = -.6 + idx * .7;
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			giro += dt * (.22 + it.hover * .35);
			piv.rotation.y = giro + it.ty; piv.rotation.x = .3 + it.tx; piv.position.y = Math.sin(t * .9) * .06;
			mod.anim.forEach(function(f){ f(t); });
			traz.position.set(Math.cos(t * .55) * 2.05, Math.sin(t * .55) * 2.05, 0);
			est.rotation.y = t * .01;
			acercar(e.cam, it.hover * .08);
			it.hud('rot', ('00' + Math.round(((piv.rotation.y * 180 / PI) % 360 + 360) % 360)).slice(-3) + '°');
		}};
	}

	/* =====================================================================
	   S-01  INSPECTION — inspector drone circles a client while a LIDAR
	   slice sweeps it, building a point cloud and finding a fault.
	   ===================================================================== */
	function escenaInspeccion(){
		var e = base(32, [0, .75, 5.5], [0, .05, 0]);
		luces(e.esc); var est = estrellas(e.esc, 140, 9);
		var cliente = new THREE.Group(); e.esc.add(cliente);
		cliente.add(caja(.9, .9, .9, M.plata));
		var tp = caja(.95, .04, .95, M.blanco); tp.position.y = .47; cliente.add(tp);
		var a1 = ala(-1, 2, .46, .5), a2 = ala(1, 2, .46, .5); a1.position.x = -.45; a2.position.x = .45; cliente.add(a1, a2);
		var antena = cil(.012, .012, .55, M.cromo, 6); antena.position.set(.25, .74, .2); cliente.add(antena);
		var bocina = new THREE.Mesh(new THREE.ConeGeometry(.08, .16, 4, 1, true), M.oscuroD); bocina.position.set(-.2, .55, .3); cliente.add(bocina);
		/* the fault the scan finds: a cracked cell on the right wing */
		var falla = resplandor(.42, 0x9fc4ff); falla.position.set(1.15, .03, .12); cliente.add(falla);
		var aro = new THREE.Mesh(new THREE.RingGeometry(.1, .115, 48), new THREE.MeshBasicMaterial({color:0x9fc4ff, transparent:true, side:THREE.DoubleSide, depthWrite:false}));
		aro.position.copy(falla.position); aro.rotation.x = -PI / 2; cliente.add(aro);
		/* point cloud sampled on the bus surface, sorted bottom→top so drawRange reveals it */
		var N = 1100, pts = [];
		for(var i = 0; i < N; i++){
			var cara = i % 6, u = (Math.random() - .5) * .92, v = (Math.random() - .5) * .92, h = .462;
			var p = cara === 0 ? new V3(h, u, v) : cara === 1 ? new V3(-h, u, v) : cara === 2 ? new V3(u, h, v) : cara === 3 ? new V3(u, -h, v) : cara === 4 ? new V3(u, v, h) : new V3(u, v, -h);
			pts.push(p);
		}
		pts.sort(function(a, b){ return a.y - b.y; });
		var ys = pts.map(function(p){ return p.y; });
		var gn = new THREE.BufferGeometry().setFromPoints(pts);
		var nube = new THREE.Points(gn, new THREE.PointsMaterial({color:0xffc98a, size:.03, map:BRILLO, transparent:true, opacity:.9, depthWrite:false, blending:THREE.AdditiveBlending}));
		cliente.add(nube);
		var plano = new THREE.Mesh(new THREE.PlaneGeometry(2.1, 2.1), new THREE.MeshBasicMaterial({map:texEscaneo(), transparent:true, opacity:.5, blending:THREE.AdditiveBlending, depthWrite:false, side:THREE.DoubleSide}));
		plano.rotation.x = -PI / 2; cliente.add(plano);
		/* inspector drone + its path + laser */
		function ruta(a){ return new V3(Math.cos(a) * 1.85, .35 + Math.sin(a) * .45, Math.sin(a) * 1.55); }
		e.esc.add(lineaDe(circulo(0, ruta), 0xffb45e, .28, true));
		var dron = new THREE.Group(); e.esc.add(dron);
		dron.add(new THREE.Mesh(new THREE.IcosahedronGeometry(.13, 1), M.cromo));
		for(var k = 0; k < 4; k++){
			var brazo = caja(.24, .015, .03, M.oscuro); brazo.rotation.y = k * PI / 2 + PI / 4; brazo.position.set(Math.cos(k * PI / 2 + PI / 4) * .12, 0, -Math.sin(k * PI / 2 + PI / 4) * .12); dron.add(brazo);
		}
		var ojo = resplandor(.26); ojo.position.z = .13; dron.add(ojo);
		var laser = lineaDe([new V3(), new V3()], 0xffb45e, .6);
		laser.material.blending = THREE.AdditiveBlending; e.esc.add(laser);
		var lp = laser.geometry.attributes.position;
		var objetivo = new V3();
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			cliente.rotation.y = -.55 + Math.sin(t * .22) * .3 + it.ty;
			cliente.rotation.x = .12 + it.tx;
			var ciclo = (t % 6.5) / 6.5, y = -.55 + suave(ciclo / .85) * 1.1;
			plano.position.y = y;
			plano.material.opacity = ciclo < .85 ? .5 : .5 * (1 - tramo(ciclo, .85, .92));
			var n = 0; while(n < ys.length && ys[n] < y) n++;
			nube.geometry.setDrawRange(0, n);
			nube.material.opacity = .9 * (1 - tramo(ciclo, .93, 1));
			var hallada = ciclo > .45;
			falla.material.opacity = hallada ? .6 + .4 * Math.sin(t * 6) : .12;
			var fr = (t * .9) % 1; aro.scale.setScalar(1 + fr * 2.6); aro.material.opacity = hallada ? (1 - fr) * .9 : 0;
			var a = t * .55; dron.position.copy(ruta(a));
			dron.lookAt(0, y * .9, 0);
			cliente.updateMatrixWorld();
			objetivo.set(0, y, 0); cliente.localToWorld(objetivo);
			lp.setXYZ(0, dron.position.x, dron.position.y, dron.position.z); lp.setXYZ(1, objetivo.x, objetivo.y, objetivo.z); lp.needsUpdate = true;
			laser.material.opacity = ciclo < .86 ? .35 + .25 * Math.sin(t * 25) : 0;
			est.rotation.y = t * .01;
			acercar(e.cam, it.hover * .1);
			it.hud('scan', Math.round(suave(ciclo / .85) * 100) + '%');
			it.hud('pts', miles(n * 37));
			it.hud('falla', hallada ? 'Cell 7 · crack' : 'Searching');
		}};
	}

	/* =====================================================================
	   S-02  REFUELLING — servicer and client linked by a hose; propellant
	   slugs flow along it while the client's gauge ring fills.
	   ===================================================================== */
	function escenaRepostaje(){
		var e = base(30, [0, 1.05, 6.1], [0, -.12, 0]);
		luces(e.esc, true); var est = estrellas(e.esc, 150, 9);
		var par = new THREE.Group(); e.esc.add(par);
		/* servicer: horizontal tanker with radiator fins */
		var serv = new THREE.Group(); serv.position.set(-1.3, 0, 0); par.add(serv);
		var casco = cil(.36, .36, 1.05, M.foil, 28); casco.rotation.z = PI / 2; serv.add(casco);
		[-1, 1].forEach(function(s){
			var cap = new THREE.Mesh(new THREE.SphereGeometry(.36, 28, 14, 0, PI * 2, 0, PI / 2), M.blanco);
			cap.rotation.z = -s * PI / 2; cap.position.x = s * .52; serv.add(cap);
		});
		for(var i = 0; i < 5; i++){ var aleta = caja(.03, .5, .7, M.cromo); aleta.position.set(-.35 + i * .14, .52, 0); serv.add(aleta); }
		var panS = caja(1.0, .02, .42, M.panel); panS.position.set(0, -.62, 0); serv.add(panS);
		var puertoS = cil(.07, .07, .14, M.oscuro, 16); puertoS.rotation.z = PI / 2; puertoS.position.x = .9; serv.add(puertoS);
		/* client: boxy comsat, wings along z */
		var cli = new THREE.Group(); cli.position.set(1.3, 0, 0); par.add(cli);
		cli.add(caja(.8, .8, .8, M.blanco));
		var banda = caja(.82, .28, .82, M.oscuro); cli.add(banda);
		var aw1 = ala(1, 2, .42, .45), aw2 = ala(-1, 2, .42, .45);
		aw1.rotation.y = PI / 2; aw2.rotation.y = PI / 2; aw1.position.z = -.4; aw2.position.z = .4; cli.add(aw1, aw2);
		var puertoC = cil(.065, .065, .12, M.cromo, 16); puertoC.rotation.z = PI / 2; puertoC.position.x = -.46; cli.add(puertoC);
		/* fuel gauge: 24 segments on the client's front face */
		var segs = [], apagado = new THREE.MeshBasicMaterial({color:0x3a2a18});
		for(i = 0; i < 24; i++){
			var a = PI / 2 - i / 24 * PI * 2;
			var sg = caja(.05, .018, .012, apagado); sg.position.set(Math.cos(a) * .27, Math.sin(a) * .27, .41); sg.rotation.z = a; cli.add(sg); segs.push(sg);
		}
		var ojoC = resplandor(.18); ojoC.position.set(0, 0, .42); cli.add(ojoC);
		/* hose */
		var curva = new THREE.CatmullRomCurve3([new V3(-.33, 0, 0), new V3(-.05, -.42, .25), new V3(.35, -.48, .2), new V3(.78, -.02, 0)]);
		par.add(new THREE.Mesh(new THREE.TubeGeometry(curva, 80, .028, 10, false), M.oscuro));
		var paquetes = [];
		for(i = 0; i < 7; i++){ var pq = resplandor(.17); par.add(pq); paquetes.push(pq); }
		var chispa = resplandor(.3); chispa.position.set(.84, 0, 0); par.add(chispa);
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			par.rotation.y = Math.sin(t * .25) * .3 + it.ty; par.rotation.x = .1 + it.tx; par.position.y = Math.sin(t * .8) * .04;
			paquetes.forEach(function(p, k){ var u = (t * .32 + k / 7) % 1; p.position.copy(curva.getPointAt(u)); p.material.opacity = Math.sin(u * PI); });
			var lleno = (t % 11) / 11, encendidos = Math.floor(lleno * 24);
			segs.forEach(function(s, k){ s.material = k < encendidos ? M.ambar : apagado; });
			chispa.material.opacity = .5 + .5 * Math.abs(Math.sin(t * 7));
			ojoC.material.opacity = lleno > .96 ? 1 : .35;
			est.rotation.y = t * .01;
			acercar(e.cam, it.hover * .1);
			it.hud('kg', Math.round(lleno * 400) + ' kg');
			it.hud('flujo', (1.6 + Math.sin(t * 3) * .22).toFixed(2) + ' kg/min');
		}};
	}

	/* =====================================================================
	   S-03  ROBOTIC REPAIR — a two-link arm carries a reaction-wheel
	   module into an empty bay, torques it in (sparks), then stows.
	   ===================================================================== */
	function escenaReparacion(){
		var e = base(36, [.3, .35, 5.6], [.05, -.05, 0]);
		luces(e.esc); estrellas(e.esc, 90, 9);
		var pared = new THREE.Group(); pared.position.set(.6, .12, -.5); pared.rotation.y = -.42; pared.scale.setScalar(.86); e.esc.add(pared);
		pared.add(caja(2.5, 1.75, .16, M.blanco));
		var marco = caja(2.56, 1.81, .1, M.oscuro); marco.position.z = -.04; pared.add(marco);
		var bahias = [[-.74, .42], [0, .42], [.74, .42], [-.74, -.42], [0, -.42], [.74, -.42]], vacia = 4, leds = [];
		bahias.forEach(function(b, k){
			var hueco = caja(.62, .6, .04, M.oscuro); hueco.position.set(b[0], b[1], .085); pared.add(hueco);
			if(k !== vacia){
				var mod = caja(.54, .52, .09, M.plata); mod.position.set(b[0], b[1], .13); pared.add(mod);
				var led = resplandor(.08, k % 2 ? 0x8be0a4 : 0xffb45e); led.position.set(b[0] + .19, b[1] + .18, .19); pared.add(led); leds.push(led);
			}
		});
		var bv = bahias[vacia], borde = [];
		[[0, .3, .62, .02], [0, -.3, .62, .02], [.31, 0, .02, .6], [-.31, 0, .02, .6]].forEach(function(r){
			var m = caja(r[2], r[3], .02, M.ambar); m.position.set(bv[0] + r[0], bv[1] + r[1], .11); pared.add(m); borde.push(m);
		});
		pared.updateMatrixWorld(true);
		var pBahia = pared.localToWorld(new V3(bv[0], bv[1], .13));
		var n = pared.localToWorld(new V3(bv[0], bv[1], 1.13)).sub(pBahia).normalize();
		var pPre = pBahia.clone().addScaledVector(n, .8).add(new V3(-.1, .12, 0));
		var pReposo = new V3(-.6, .62, 1.35);
		/* reaction-wheel module */
		var modulo = new THREE.Group(); e.esc.add(modulo);
		var carcasa = cil(.2, .2, .12, M.oscuro, 28); carcasa.rotation.x = PI / 2; modulo.add(carcasa);
		var rueda = new THREE.Group(); rueda.position.z = .07; modulo.add(rueda);
		var disco = cil(.16, .16, .03, M.cromo, 32); disco.rotation.x = PI / 2; rueda.add(disco);
		for(var i = 0; i < 6; i++){ var rayo = caja(.3, .018, .035, M.oscuro); rayo.rotation.z = i * PI / 6; rayo.position.z = .02; rueda.add(rayo); }
		var aroM = new THREE.Mesh(new THREE.TorusGeometry(.2, .012, 8, 40), M.ambar); modulo.add(aroM);
		/* arm */
		var B = new V3(-1.3, -.62, 1.05), L1 = 1.15, L2 = 1.0;
		var pedestal = cil(.17, .24, .3, M.oscuro, 24); pedestal.position.copy(B).add(new V3(0, -.15, 0)); e.esc.add(pedestal);
		var e1 = cil(.065, .065, 1, M.blanco, 14), e2 = cil(.055, .055, 1, M.blanco, 14); e.esc.add(e1, e2);
		var j0 = new THREE.Mesh(new THREE.SphereGeometry(.11, 18, 18), M.oscuro), j1 = j0.clone(), j2 = new THREE.Mesh(new THREE.SphereGeometry(.085, 16, 16), M.oscuro);
		j0.position.copy(B); e.esc.add(j0, j1, j2);
		var efector = new THREE.Group(); e.esc.add(efector);
		var pinzaA = caja(.03, .03, .18, M.ambar), pinzaB = pinzaA.clone(); pinzaA.position.set(-.07, 0, .1); pinzaB.position.set(.07, 0, .1); efector.add(pinzaA, pinzaB);
		var chispas = particulas(90, .09); chispas.userData.tinte = [1, .8, .5]; e.esc.add(chispas);
		var W = new V3(), codo = new V3(), d = new V3(), perp = new V3(), ARRIBA = new V3(0, 1, 0), pM = new V3(), disparado = false;
		function ik(objetivo){
			d.subVectors(objetivo, B); var dist = clamp(d.length(), .2, L1 + L2 - .001); d.normalize();
			var ca = (L1 * L1 + dist * dist - L2 * L2) / (2 * L1 * dist), sa = Math.sqrt(Math.max(0, 1 - ca * ca));
			perp.copy(ARRIBA).addScaledVector(d, -ARRIBA.dot(d)).normalize();
			codo.copy(B).addScaledVector(d, L1 * ca).addScaledVector(perp, L1 * sa);
			alinear(e1, B, codo); alinear(e2, codo, objetivo);
			j1.position.copy(codo); j2.position.copy(objetivo);
			efector.position.copy(objetivo); efector.lookAt(pBahia);
		}
		var T = 7.6;
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			var c = t % T, paso, enMano = true, escala = 1;
			if(c < 2.6){ pM.lerpVectors(pReposo, pPre, suave(tramo(c, .6, 2.6))); paso = 'Approach'; escala = suave(tramo(c, 0, .6)); }
			else if(c < 3.6){ pM.lerpVectors(pPre, pBahia, suave(tramo(c, 2.6, 3.6))); paso = 'Insert'; }
			else if(c < 4.8){ pM.copy(pBahia); paso = 'Torque'; }
			else { pM.copy(pBahia); enMano = false; paso = c < 6.8 ? 'Stow' : 'Verify'; escala = 1 - suave(tramo(c, 6.9, 7.6)); }
			modulo.position.copy(pM); modulo.lookAt(pM.clone().add(n)); modulo.scale.setScalar(Math.max(.001, escala));
			if(enMano) W.copy(pM).addScaledVector(n, .24);
			else if(c < 5.6) W.lerpVectors(pBahia.clone().addScaledVector(n, .24), pPre.clone().addScaledVector(n, .24), suave(tramo(c, 4.8, 5.6)));
			else W.lerpVectors(pPre.clone().addScaledVector(n, .24), pReposo.clone().addScaledVector(n, .24), suave(tramo(c, 5.6, 6.8)));
			ik(W);
			var abierto = enMano ? .07 : .1; pinzaA.position.x = -abierto; pinzaB.position.x = abierto;
			rueda.rotation.z += dt * (paso === 'Torque' ? 22 : 3);
			if(c >= 3.6 && c < 4.6){
				if(!disparado){ disparado = true; }
				for(var k = 0; k < 3; k++){
					var v = new V3((Math.random() - .5) * 2.2, (Math.random() - .2) * 2.2, (Math.random() - .5) * 2.2).addScaledVector(n, 1.4);
					emitir(chispas, pBahia.clone().addScaledVector(n, .1), v, .4 + Math.random() * .5);
				}
			} else if(c < 3.6) disparado = false;
			avanzarParticulas(chispas, dt, .96);
			var pulso = paso === 'Approach' || paso === 'Insert' ? .5 + .5 * Math.sin(t * 6) : 0;
			borde.forEach(function(m){ m.visible = pulso > .05 || paso === 'Torque'; });
			leds.forEach(function(l, k){ l.material.opacity = .4 + .6 * Math.max(0, Math.sin(t * 2 + k)); });
			e.esc.rotation.y = it.ty * .6; e.esc.rotation.x = it.tx * .4;
			acercar(e.cam, it.hover * .1);
			it.hud('paso', paso);
			it.hud('par', paso === 'Torque' ? (.72 + Math.sin(t * 9) * .12).toFixed(2) + ' Nm' : '— Nm');
		}};
	}

	/* =====================================================================
	   S-04  LIFE-EXTENSION DOCKING — a tug closes on a client's aft end,
	   captures it with a flash, fires its own engine for the stack, backs off.
	   ===================================================================== */
	function escenaAcople(){
		var e = base(30, [4.3, 1.6, 4.4], [-.15, -.05, -1.25]);
		luces(e.esc); var est = estrellas(e.esc, 160, 10);
		var todo = new THREE.Group(); e.esc.add(todo);
		var cli = new THREE.Group(); todo.add(cli);
		cli.add(caja(1, 1, 1.2, M.blanco));
		var banda = caja(1.02, .42, 1.22, M.foil); cli.add(banda);
		var w1 = ala(-1, 3, .5, .62), w2 = ala(1, 3, .5, .62); w1.position.x = -.5; w2.position.x = .5; cli.add(w1, w2);
		var plato = new THREE.Mesh(new THREE.SphereGeometry(.42, 32, 10, 0, PI * 2, 0, .8), M.blancoD);
		plato.rotation.x = -PI / 2; plato.position.z = 1.0; cli.add(plato);
		var tob = cil(.12, .24, .32, M.oscuroD, 24); tob.rotation.x = PI / 2; tob.position.z = -.76; cli.add(tob);
		var C = new V3(0, 0, -.94);
		var tug = new THREE.Group(); todo.add(tug);
		var cuerpo = cil(.28, .28, .75, M.plata, 20); cuerpo.rotation.x = PI / 2; tug.add(cuerpo);
		var aroT = new THREE.Mesh(new THREE.TorusGeometry(.29, .02, 8, 40), M.ambar); aroT.position.z = .37; tug.add(aroT);
		var sonda = new THREE.Mesh(new THREE.ConeGeometry(.09, .3, 20), M.cromo); sonda.rotation.x = PI / 2; sonda.position.z = .525; tug.add(sonda);
		[-1, 1].forEach(function(s){ var p = caja(.95, .02, .36, M.panel); p.position.set(s * .78, 0, -.05); p.rotation.z = s * .22; tug.add(p); });
		var tobT = cil(.07, .14, .2, M.oscuroD, 16); tobT.rotation.x = PI / 2; tobT.position.z = -.47; tug.add(tobT);
		var motor = resplandor(.85); motor.position.z = -.7; tug.add(motor);
		var rcs = [[.32, 0], [-.32, 0], [0, .32], [0, -.32]].map(function(p){ var s = resplandor(.2, 0xffe2bd); s.position.set(p[0], p[1], .25); tug.add(s); return s; });
		var destello = resplandor(.4, 0xfff1dc); destello.position.copy(C); todo.add(destello);
		var guia = lineaDe([new V3(.35, .25, -5), C], 0xffb45e, .22, true); todo.add(guia);
		var inicio = new V3(.35, .25, -5.0), acoplado = new V3(0, 0, C.z - .675), T = 10.5;
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			var c = t % T, s, estado;
			if(c < 4){ s = easeOut(c / 4); estado = 'Approach'; }
			else if(c < 8.3){ s = 1; estado = c < 4.7 ? 'Contact' : 'Captured'; }
			else { s = 1 - easeIn(tramo(c, 8.3, T)); estado = 'Release'; }
			tug.position.lerpVectors(inicio, acoplado, s);
			var rango = Math.max(0, (C.z - (tug.position.z + .675))) * 6;
			rcs.forEach(function(r, k){ r.material.opacity = (estado === 'Approach' || estado === 'Release') && Math.sin(t * 31 + k * 2) > .55 ? .9 : 0; });
			var fd = tramo(c, 4, 4.8); destello.scale.setScalar(.2 + fd * 1.6); destello.material.opacity = c >= 4 && c < 4.8 ? 1 - fd : 0;
			motor.material.opacity = c > 5 && c < 8.1 ? .75 + Math.sin(t * 19) * .15 : 0;
			guia.material.opacity = estado === 'Approach' ? .25 : .06;
			todo.rotation.y = -.15 + Math.sin(t * .15) * .2 + it.ty;
			todo.rotation.x = it.tx * .5;
			est.rotation.y = t * .008;
			acercar(e.cam, it.hover * .1);
			it.hud('rango', rango.toFixed(1) + ' m');
			it.hud('estado', estado);
		}};
	}

	/* =====================================================================
	   S-05  RELOCATION — Hohmann transfer from a low orbit to a high one
	   around a night-side planet, with burns at perigee and apogee.
	   ===================================================================== */
	function escenaRelocacion(){
		var e = base(34, [0, 2.15, 5.0], [0, -.15, 0]);
		var clave = luces(e.esc); clave.position.set(-5, 2, 3);
		var est = estrellas(e.esc, 170, 9);
		var sis = new THREE.Group(); sis.rotation.z = .12; e.esc.add(sis);
		var tx = texPlanetaNoche();
		var planeta = new THREE.Mesh(new THREE.SphereGeometry(.56, 64, 40), new THREE.MeshStandardMaterial({map:tx.mapa, emissiveMap:tx.luces, emissive:0xffffff, emissiveIntensity:1.1, roughness:1, metalness:0}));
		planeta.rotation.z = .4; sis.add(planeta);
		sis.add(atmosfera(.6, 0x2a5cff, 0x9fc4ff, 2.6, 1.4));
		var r1 = 1.0, r2 = 2.05, ex = (r2 - r1) / (r2 + r1), sa = (r1 + r2) / 2;
		function radio(th){ return sa * (1 - ex * ex) / (1 + ex * Math.cos(th)); }
		function pt(r, th){ return new V3(Math.cos(th) * r, 0, -Math.sin(th) * r); }
		sis.add(lineaDe(circulo(r1), 0xe8e4da, .28, true));
		sis.add(lineaDe(circulo(r2), 0xffb45e, .45, true));
		var arco = []; for(var i = 0; i <= 80; i++){ var th = i / 80 * PI; arco.push(pt(radio(th), th)); }
		var transf = lineaDe(arco, 0xffb45e, .8); sis.add(transf);
		var nave = new THREE.Group(); sis.add(nave);
		nave.add(caja(.08, .06, .06, M.foil));
		var np = caja(.22, .008, .05, M.panel); nave.add(np);
		var halo = resplandor(.22); nave.add(halo);
		var quema = resplandor(.6, 0xffd29a); nave.add(quema);
		var NT = 70, tpos = new Float32Array(NT * 3), tcol = new Float32Array(NT * 3);
		var tg = new THREE.BufferGeometry(); tg.setAttribute('position', new THREE.BufferAttribute(tpos, 3)); tg.setAttribute('color', new THREE.BufferAttribute(tcol, 3));
		var estela = new THREE.Line(tg, new THREE.LineBasicMaterial({vertexColors:true, transparent:true, blending:THREE.AdditiveBlending})); estela.frustumCulled = false; sis.add(estela);
		var historia = [], p = new V3(), T = 12, cPrev = 0;
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			var c = t % T, r, th, dv = 'Coast', burn = 0;
			if(c < 3.5){ th = PI + (c / 3.5) * PI; r = r1; }
			else if(c < 7.5){ var u = (c - 3.5) / 4; th = PI * Math.sin(u * PI / 2); r = radio(th); }
			else { th = PI + ((c - 7.5) / 4.5) * PI * .95; r = r2; }
			if(c >= 3.5 && c < 4.1){ burn = 1 - tramo(c, 3.5, 4.1); dv = '+0.78 km/s'; }
			if(c >= 7.5 && c < 8.1){ burn = 1 - tramo(c, 7.5, 8.1); dv = '+0.71 km/s'; }
			p.copy(pt(r, th)); nave.position.copy(p);
			var fade = Math.min(tramo(c, 0, .4), 1 - tramo(c, T - .4, T));
			halo.material.opacity = fade; quema.material.opacity = burn; quema.scale.setScalar(.35 + burn * .5);
			if(c < cPrev) historia.length = 0; cPrev = c;
			historia.unshift(p.clone()); if(historia.length > NT) historia.pop();
			for(var k = 0; k < NT; k++){
				var q = historia[Math.min(k, historia.length - 1)] || p, f = (1 - k / NT) * fade;
				tpos[k * 3] = q.x; tpos[k * 3 + 1] = q.y; tpos[k * 3 + 2] = q.z;
				tcol[k * 3] = f; tcol[k * 3 + 1] = .7 * f; tcol[k * 3 + 2] = .37 * f;
			}
			tg.attributes.position.needsUpdate = true; tg.attributes.color.needsUpdate = true;
			transf.material.opacity = c >= 3.5 && c < 7.5 ? .85 : .3;
			planeta.rotation.y = t * .08;
			sis.rotation.y = it.ty * .8; sis.rotation.x = it.tx * .6;
			est.rotation.y = t * .006;
			acercar(e.cam, it.hover * .1);
			it.hud('alt', miles(400 + (r - r1) / (r2 - r1) * 35386) + ' km');
			it.hud('dv', dv);
		}};
	}

	/* =====================================================================
	   S-06  END-OF-LIFE DISPOSAL — a retired satellite falls into the
	   atmosphere over a daylit limb, heats, trails plasma and breaks up.
	   ===================================================================== */
	function escenaDesorbitado(){
		var e = base(32, [0, .55, 6.0], [0, -.25, 0]);
		var clave = luces(e.esc, true); clave.position.set(6, 1.2, -2.5); clave.intensity = 2.8;
		var est = estrellas(e.esc, 180, 10);
		var mundo = new THREE.Group(); e.esc.add(mundo);
		var tierra = new THREE.Mesh(new THREE.SphereGeometry(5, 96, 64), new THREE.MeshStandardMaterial({map:texPlanetaDia(), roughness:.95, metalness:0, color:0xb8b4ae}));
		tierra.position.set(.4, -6.7, -1.6); tierra.rotation.z = -.15; mundo.add(tierra);
		var atm = atmosfera(5.22, 0xff8a3c, 0x7fb2ff, 2.2, 1.6); atm.position.copy(tierra.position); mundo.add(atm);
		var curva = new THREE.CubicBezierCurve3(new V3(-1.75, .78, -.2), new V3(-.85, .75, 0), new V3(.45, .2, .3), new V3(1.45, -.95, .45));
		var trayecto = lineaDe(curva.getPoints(80), 0xe8e4da, .18, true); mundo.add(trayecto);
		var sat = new THREE.Group(); mundo.add(sat);
		var matSat = new THREE.MeshStandardMaterial({color:0x6b645a, metalness:.6, roughness:.5, emissive:0xff5a14, emissiveIntensity:0});
		sat.add(caja(.2, .2, .24, matSat));
		var panelRoto = caja(.42, .01, .16, M.panel); panelRoto.position.x = .3; panelRoto.rotation.z = .5; sat.add(panelRoto);
		var calor = resplandor(.5, 0xffc27a); sat.add(calor);
		var plasma = particulas(260, .14); plasma.userData.tinte = [1, .62, .3]; mundo.add(plasma);
		var trozos = [];
		for(var i = 0; i < 6; i++){
			var tz = new THREE.Group(); tz.add(caja(.05 + Math.random() * .05, .04, .05, matSat)); var gl = resplandor(.32, 0xffb070); tz.add(gl);
			tz.userData = {v:new V3(.5 + Math.random() * .6, -.5 - Math.random() * .5, (Math.random() - .5) * .8), gl:gl}; tz.visible = false; mundo.add(tz); trozos.push(tz);
		}
		var T = 9, punto = new V3(), tang = new V3(), roto = false, pRotura = new V3(), cPrev = 99;
		return {esc:e.esc, cam:e.cam, tick:function(t, dt, it){
			var c = t % T, u = easeIn(clamp(c / 6.4, 0, 1)) * .55 + clamp(c / 6.4, 0, 1) * .45, estado;
			var alt = 400 * Math.pow(1 - u, 1.7);
			if(c < cPrev){ roto = false; trozos.forEach(function(z){ z.visible = false; }); apagarParticulas(plasma); sat.visible = true; }
			var calorK = tramo(u, .5, .86);
			if(u < .86){
				curva.getPointAt(u, punto); sat.position.copy(punto);
				curva.getTangentAt(u, tang); sat.lookAt(punto.clone().add(tang)); sat.rotation.z += t * .4;
				matSat.emissiveIntensity = calorK * 1.6;
				calor.material.opacity = calorK; calor.scale.setScalar(.3 + calorK * .9);
				if(calorK > 0){
					var nEmit = 1 + Math.floor(calorK * 4);
					for(var k = 0; k < nEmit; k++) emitir(plasma, punto, tang.clone().multiplyScalar(-.6 - Math.random() * .6).add(new V3((Math.random() - .5) * .25, (Math.random() - .5) * .25, (Math.random() - .5) * .25)), .5 + Math.random() * .6);
				}
				estado = alt > 120 ? (c < 1.2 ? 'Deorbit burn' : 'Descent') : 'Entry interface';
			} else {
				if(!roto){ roto = true; sat.visible = false; pRotura.copy(sat.position); trozos.forEach(function(z){ z.position.copy(pRotura); z.visible = true; }); }
				var fu = tramo(c, 6.4, 8.2);
				trozos.forEach(function(z){
					z.position.addScaledVector(z.userData.v, dt); z.rotation.x += dt * 4; z.rotation.y += dt * 3;
					z.userData.gl.material.opacity = 1 - fu; z.children[0].material.emissiveIntensity = 1.6 * (1 - fu);
					if(fu >= 1) z.visible = false;
					else if(Math.random() < .5) emitir(plasma, z.position, z.userData.v.clone().multiplyScalar(-.4), .35);
				});
				estado = fu < 1 ? 'Breakup' : 'Splashdown zone';
			}
			cPrev = c;
			avanzarParticulas(plasma, dt);
			tierra.rotation.y = t * .015;
			mundo.rotation.y = it.ty * .5; mundo.rotation.x = it.tx * .35;
			est.rotation.y = t * .005;
			acercar(e.cam, it.hover * .08);
			it.hud('alt', (u < .86 ? Math.max(0, Math.round(alt)) : 0) + ' km');
			it.hud('estado', estado);
		}};
	}

	/* ---------------- registry ---------------- */
	var FABRICAS = {
		'flota-warden': function(){ return escenaFlota('warden', 0); },
		'flota-tern':   function(){ return escenaFlota('tern', 1); },
		'flota-depot':  function(){ return escenaFlota('depot', 2); },
		'inspeccion':   escenaInspeccion,
		'repostaje':    escenaRepostaje,
		'reparacion':   escenaReparacion,
		'acople':       escenaAcople,
		'relocacion':   escenaRelocacion,
		'desorbitado':  escenaDesorbitado
	};

	var items = [];
	contenedores.forEach(function(el, idx){
		var fab = FABRICAS[el.getAttribute('data-vitrina')];
		if(!fab) return;
		var esc;
		try{ esc = fab(); }catch(err){ if(window.console) console.warn('vitrina', err); return; }
		var cv = document.createElement('canvas'); cv.className = 'vitrina'; cv.setAttribute('aria-hidden', 'true');
		el.appendChild(cv); el.classList.add('con3d');
		var hudEls = {};
		el.querySelectorAll('[data-k]').forEach(function(h){ hudEls[h.getAttribute('data-k')] = h; });
		var it = {
			el:el, cv:cv, ctx:cv.getContext('2d'), esc:esc.esc, cam:esc.cam, tick:esc.tick,
			visible:true, hover:0, hoverObj:0, tx:0, ty:0, txObj:0, tyObj:0, w:0, h:0,
			fase:idx * 1.37, hudEls:hudEls, hudVal:{}, tFijo:4.2 + idx * .6, hechoFijo:false
		};
		it.hud = function(k, v){ var h = hudEls[k]; if(h && it.hudVal[k] !== v && (cuadro % 3 === 0 || reducido)){ it.hudVal[k] = v; h.textContent = v; } };
		var tarjeta = el.closest('.nave, .servicio') || el;
		tarjeta.addEventListener('pointermove', function(ev){
			var r = el.getBoundingClientRect();
			it.txObj = clamp((ev.clientY - r.top) / r.height - .5, -.7, .7) * .45;
			it.tyObj = clamp((ev.clientX - r.left) / r.width - .5, -.7, .7) * .8;
			it.hoverObj = 1;
		});
		tarjeta.addEventListener('pointerleave', function(){ it.txObj = it.tyObj = 0; it.hoverObj = 0; });
		items.push(it);
	});
	if(!items.length) return;

	if('IntersectionObserver' in window){
		var io = new IntersectionObserver(function(es){
			es.forEach(function(en){ items.forEach(function(it){ if(it.el === en.target){ it.visible = en.isIntersecting; } }); });
		}, {rootMargin:'100px'});
		items.forEach(function(it){ io.observe(it.el); });
	}

	var cuadro = 0, tPrev = performance.now();
	function pintar(it, t, dt){
		var w = Math.max(2, Math.round(it.el.clientWidth * DPR)), h = Math.max(2, Math.round(it.el.clientHeight * DPR));
		if(w !== it.w || h !== it.h){
			it.w = w; it.h = h; it.cv.width = w; it.cv.height = h;
			it.cam.aspect = w / h; it.cam.updateProjectionMatrix(); it.hechoFijo = false;
		}
		if(w > glW || h > glH){ glW = Math.max(glW, w); glH = Math.max(glH, h); ren.setSize(glW, glH, false); }
		it.hover += (it.hoverObj - it.hover) * Math.min(1, dt * 5);
		it.tx += (it.txObj - it.tx) * Math.min(1, dt * 4);
		it.ty += (it.tyObj - it.ty) * Math.min(1, dt * 4);
		it.tick(t, dt, it);
		ren.setScissorTest(true);
		ren.setViewport(0, 0, w, h); ren.setScissor(0, 0, w, h);
		ren.clear();
		ren.render(it.esc, it.cam);
		it.ctx.clearRect(0, 0, w, h);
		it.ctx.drawImage(ren.domElement, 0, glH - h, w, h, 0, 0, w, h);
	}

	function bucle(now){
		requestAnimationFrame(bucle);
		if(document.hidden) return;
		var dt = Math.min((now - tPrev) / 1000, .05); tPrev = now; cuadro++;
		var t = now / 1000;
		for(var i = 0; i < items.length; i++){
			var it = items[i];
			if(!it.visible) continue;
			if(reducido){
				if(it.hechoFijo && it.cv.width === Math.max(2, Math.round(it.el.clientWidth * DPR))) continue;
				/* settle a meaningful still frame: run the scene forward to its showcase moment */
				for(var k = 0; k < 40; k++) it.tick(it.tFijo - (40 - k) * .03, .03, it);
				pintar(it, it.tFijo, 0); it.hechoFijo = true;
			} else {
				pintar(it, t + it.fase, dt);
			}
		}
	}
	requestAnimationFrame(bucle);
})();
</script>
</body>
</html>
```

