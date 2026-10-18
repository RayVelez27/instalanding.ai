Build a single-file HTML landing page for "Cyber Bird", a one-button pixel arcade game concept, with the game itself playable inside the hero. The player flies an angular armored cyber-pickup on hover-jets through gaps between stacks of stainless-steel rockets over a starbase. Every graphic, on the page and in the game, is drawn by code at runtime: no image files. Credit the original open-source game it is built on (Tesla Bird by Pavel Troshkin) in the footer, and say it is an unaffiliated fan concept.

STACK
- Google Fonts: Jersey 10 (pixel display: logo, headings, numbers, keycaps), Geist 400-600 (body), Geist Mono (labels, 10-12px uppercase, wide tracking).
- Canvas 2D for the game, the sprites, a starfield and two mini scenes. One inline script.

THE SYSTEM
- Dark: page #04050b, text #eef3ff, muted #98a0b3, dim #5d6477, hairlines at 9% / 17% white. Accent cyan #2fe0ff (#7af0ff hover) with dark ink #031218 on it.
- Two registered colour properties (@property --glow, --glow2) drive the auroras and glows, so switching the sky theme (night: blue / cyan; dawn: violet / coral; day: blue / pale blue) cross-fades them in CSS. The theme is remembered and also re-skins the game.
- Behind everything: a fixed starfield canvas (parallax with scroll, tinted per theme), radial aura glows, and faint CRT scanlines.
- The title "CYBER" at clamp(108px, 19vw, 270px) with a hard black offset shadow and a big glow, and a tilted "BIRD" sticker in a cyan-to-blue gradient tucked under its right edge.
- Cards: 18px radius, faint white gradient, a cursor-following radial highlight. Keycaps are pixel boxes with a 3px border and a hard 4px black shadow.

SPRITES (all generated into offscreen canvases once)
- The pickup (42x15): a single triangular roofline with the apex at x=24, steel slab sides with panel lines, dark glass, a light bar and tail light, wheels drawn as shaded discs, and a crashed variant with cracked glass. A cyan light beam ahead of it.
- Jet smoke: a 14-frame strip of flame then expanding, dithered puffs.
- Rockets in three pieces (nose cone with fins, a tileable body, an engine section with bells), shaded by a steel ramp across the width with a dark heat-shield tile pattern on one side.
- Three starbase skies (night with stars and a moon, dawn with a striped sunset sun, day with a sun and clouds) built from dithered gradient bands, rolling hills, launch towers, rockets and tanks in silhouette, a lit ground edge and a road.

THE GAME
- Native 640x360, rendered at 3x into a canvas and scaled to cover its box with a ResizeObserver; pixel-crisp (imageSmoothingEnabled false, image-rendering pixelated).
- Physics: gravity 1100, a boost sets velocity to -270, horizontal speed 115; the truck tilts from -12deg on the climb to +30deg in the fall. Rocket pairs every step px with a gap of innerColumn px, and each gap may only drift maxGapShift px from the last. Presets: easy 200 / 96 / 50, normal 170 / 80 / 60, hard 145 / 70 / 72.
- Screens drawn on the canvas in Jersey 10: start ("CYBER BIRD", CLICK or SPACE keycaps), an in-flight HUD (a T+ mission clock, a charge timeline LIFTOFF / 25 / 50 / 75 / FULL, pixel gauges for score and altitude), and game over (charge, score and best gauges, NEW BEST, a PLAY button). Every 10 points charges 25%.
- Input: Space, Up or W or a click / tap boosts; keys only act while the game is at least half visible or fullscreen. Best scores per difficulty, run count and theme go to localStorage, each read and write wrapped in try/catch.
- Expose it as a factory, CyberBird('container', { difficulty, theme }), returning start, restart, destroy, getScore, getBestScore, getState, setTheme.

SECTIONS (data-section in order)
1. nav: a fixed blurred bar with the pixel truck and "CYBER BIRD", section links, a Night / Dawn / Day segmented switch and a pixel GitHub icon.
2. hero: the eyebrow "Game concept · One-button arcade" with a blinking pixel dot, the title, the lede, "Launch the game" (scrolls to and focuses the game) and "See the build"; then the console: a gradient-bordered frame with lamps, a live T+ clock, a difficulty switch and a fullscreen button, the 16:9 game screen (4:3 on phones), a telemetry row (score, best for the mode, charge, status) updated ten times a second, and a spec line (640x360 native, 3x pixel render, 0 image files, 1 html file).
3. marquee: big pixel words (LIFTOFF, 25% CHARGE … FULL CHARGE, CLICK OR SPACE) scrolling.
4. features: a six-column bento: a flight-model card with a mini canvas of the truck hovering, a tall obstacle card with an animated rocket gap, a sky card whose three canvas swatches switch the theme, a progression card with a conic gauge and a charge ladder, and a code card showing the embed API.
5. modes: three cards built from the presets with 12-cell meters for spacing, gap and drift, your best per mode, and a "Fly" button that switches difficulty and launches; the current mode is highlighted.
6. manual: control rows with pixel keycaps and four numbered pilot tips.
7. mission-log: bests per difficulty, total runs and peak charge read from localStorage, with a reset link.
8. cta: "YOU." with a cyan full stop and "Fly now".
9. footer: the credit and non-affiliation line, GitHub and X icons.

THINGS THAT BREAK
- Keep every sprite and sky in its own offscreen canvas and only drawImage per frame; regenerate a sky only when the theme or the stage size changes.
- Snap the scaled stage to whole game pixels, or the art shimmers as it moves.
- Load the Jersey 10 font (document.fonts.load) before the first canvas text, or the screens draw in the fallback face.
- Remove the game's listeners and cancel its animation frame in destroy(), because switching difficulty remounts it.

THE FLOOR
- Breakpoints at 960px (bento to two columns), 900px (modes, manual and log stack, links hide) and 640px (4:3 screen, two-column telemetry). No horizontal scroll at 390px.
- The game container is focusable with role=region and a visible focus ring, a polite status line announces start and game over, theme and difficulty switches use aria-pressed, decorative canvases are aria-hidden, and prefers-reduced-motion stops the marquee, starfield drift and mini scenes.
