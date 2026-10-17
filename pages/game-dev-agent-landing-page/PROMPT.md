Build a single-file HTML landing page for "Sortie", a fictional AI agent for game developers by the fictional "Sortie Labs". Sortie works inside the studio's engine and repo: it writes gameplay code, blocks out levels, playtests the build overnight and files the bugs it finds. The page proves the claim with its hero: not a screenshot but a small live game scene in three.js that the visitor can fly without leaving the page. Fictional product, studios, quotes, awards and numbers, labelled as such in the footer.

STACK
- three.js 0.170.0 as an ES module through an import map: "three" maps to https://cdn.jsdelivr.net/npm/three@0.170.0/build/three.module.js and "three/addons/" to .../examples/jsm/ (EffectComposer, RenderPass, UnrealBloomPass, ShaderPass, OutputPass, RoomEnvironment, RoundedBoxGeometry, Horizontal/VerticalTiltShiftShader). The map must come before the module script. Everything is generated in code: no models, textures, images or audio files.
- Google Fonts: Fredoka 500/600/700 for display (rounded, game-like), Nunito 400/600/800 for body at 17px/1.6, and M PLUS Rounded 1c 700 loaded with the text= parameter set to only the kana used on the signs.
- Three scripts: a tiny classic loader script, a classic script for the page chrome, one module for the world. They talk through CustomEvents on document: "corgi:progress" ({p, label}), "corgi:coat" (a crew key), "corgi:play" and "corgi:shots" (a map of data URLs).

THE SYSTEM
- Tokens on :root: sky #8fbdea, sky-2 #c9def3, haze #f3e1de, peach #f6dccd, paper #fbf6ee, card #fffdf9, ink #39324f, ink-soft #6d6680, line #eadfd2, orange #e08a3c / deep #b9652a, blossom #f6b6c8 / deep #e7839f, leaf #5aa578 / deep #3f6b4f, gold #f2a93b, radius 22px, easing cubic-bezier(.2,.8,.2,1). A paper grain from an feTurbulence SVG data URI sits on the body and the crew section.
- Everything is outlined in ink like the game: cards and buttons have a 2-3px ink border and a hard 5-6px ink drop shadow that grows on hover and collapses on press. Primary buttons are gold pills, ghost buttons translucent white.
- The headline "Hand it the grind. / Keep the fun." is styled like game subtitle text: Fredoka 700 at clamp(50px, 7.6vw, 108px), gold fill, the second line orange, a thick white rim built from sixteen 5px text-shadow offsets, then a soft orange drop. No background-clip tricks: they fight the rim.
- One inline SVG <symbol> of a corgi face filled with var(--coat), var(--saddle) and var(--white). Custom properties inherit into <use>, so one symbol draws all four crew portraits, the dossier face, the capsule mascot and the hero fallback.

THE LOADER
- Only when WebGL exists, html gets .gl-wait and a fixed full-page loader covers everything: the hero's sky gradient, the wordmark with the same white rim, "An agent for game developers", a dotted trail with a small plane icon flying along it, a label and a percentage, and a rounded progress bar.
- The bar creeps on its own toward 68% while three.js downloads (an exponential ease), then follows the build stages the module reports ("Planting the trees" 70, "Painting the road" 84, "Fuelling the plane" 92, "Ready" 100). At 100 it fades out. A 25s safety timeout removes it regardless. Without WebGL it never shows.

THE WORLD (module script)
- An opaque renderer cleared to the horizon peach, DPR capped at 1.5, PCF soft shadows from a low golden sun (#ffe0b0, offset 26/15/12) that follows the plane, a warm rim light (#ffb27a) from behind it along the line of sight and a cool hemisphere fill. A RoomEnvironment PMREM at low intensity gives the clearcoats something to reflect. Fog peach from 34 to 118.
- A BackSide sphere with a gradient shader sky (horizon, haze, mid and top blues, plus a soft sun glow) follows the camera, matching the CSS fallback gradient.
- Ink outlines by inverted hull: a back-faced ink copy of each mesh scaled ~1.035-1.08. For instanced trees, a second InstancedMesh with the ink material and every matrix scaled up.
- Terrain: a 260x260 plane (84 segments, 64 on phones) with a sum-of-sines height, converted to non-indexed with one of five greens per triangle and a pale verge near the road. Dip vertices within 4.2 of the road so no facet pokes through it.
- The road is one closed centripetal CatmullRomCurve3 through 14 points on a wobbly ellipse, sampled 720 times into three ribbons with polygonOffset: an ink edge, a pale shoulder and a lavender-grey surface.
- Trees from a seeded PRNG so every load and the thumbnail match, at least 7 units off the road: 30% sakura (trunk plus three pink blobs), 15% pines (three stacked cones), the rest round trees, plus 1,100 verge grass tufts (500 on phones). Canopies, their ink hulls and the grass sway in the vertex shader via onBeforeCompile, phase-shifted by instance position; set customProgramCacheKey.
- The plane: a toy biplane built from RoundedBoxGeometry: a painted fuselage with a cream band and cowl, a tail with a blinking beacon, two cream wings with struts and sakura roundels, red and green wingtip lights that blink, a glass windshield, landing gear, a spinning propeller with a faint disc, and smoke puffs from the tail. The pilot is a corgi head (physical materials: velvet sheen fur, clearcoat eyes and nose with catchlights) in chrome goggles, with a bandana scarf whose vertices stream in the wind.
- Watching: the plane cruises 1.7 units over the road, banks with the turn rate, pitches with the climb and glances toward the pointer. Opening shot (skipped under reduced motion): the camera drops from 30 units up over 3.8s and settles on a three-quarter front view; the kicker and headline pop as it lands. On screens 900px and wider, setViewOffset shifts the frame by -17% of the width so the plane flies beside the copy; under 900px shift it vertically instead. Ease the offset.
- 24 glowing petal tokens hover along the road; flying through one bumps the HUD counter. 380 falling petals (160 on phones) wrap in a box that follows the plane. Nine unfogged cloud clusters far out.
- Post: EffectComposer with UnrealBloomPass (desktop only), then horizontal and vertical tilt-shift whose focus band follows the plane, then OutputPass.

PLAY MODE
- "Play a lap, right here" (and "Fly the demo" further down) hands over the controls: a chase camera, W faster, S slower, A/D bank, Shift boost, kept inside a 100-unit radius. Tokens stay gone until all 24 are taken, then a toast and they return. Esc or "Stop playing" exits and the plane eases back onto the nearest road sample over 1.2s. Capture keys only while playing; preventDefault only on arrows and space. On touch screens a four-button pad appears, driven by pointer capture.

SECTIONS (data-section in order)
1. nav: fixed, transparent over the hero, paper with blur after 40px. Plane-in-a-gold-circle logo, How it works / Crew / Briefing / FAQ, a gold "Request access" pill.
2. hero: kicker pill, headline, a sub, the play button (hidden until the world renders) and "Request early access", a controls note and a WORKS WITH row of engine chips (Unity, Unreal, Godot, Custom engines). A vertical white nameboard reading ソーティー sits top right on wide screens. A HUD chip shows petals, the current crew member and a sound toggle.
3. world (How it works): three ink-bordered cards whose inline SVG art is replaced by in-engine stills: reads the whole project first, works in the engine not beside it, flies the long jobs overnight.
4. corgis (The crew): a radiogroup of four specialists, each the same agent tuned for a job (Mochi gameplay, Kinako level design, Azuki playtest and QA, Yuki build and release), roving tabindex and arrow keys. A dossier shows the face, role, bio and Code / Editor / Testing bars out of 5. Choosing one fires "corgi:coat": the pilot's coat and the plane's paint change live, and a second small renderer spins a full 3D corgi on a pink disc in the dossier.
5. controls (Briefing): copy about briefing it like a teammate (plans, asks, opens a pull request; nothing merges without a person) beside a dark timestamped sortie log in keycap style.
6. stats: an ink band of four gold numbers (42 studios, 18,000 runs a night, 9 hrs, 0 unreviewed merges) that count up once on arrival and read correctly before that.
7. press: one big pull quote with a giant blossom quote mark, three laurel badges (the branch drawn once along a quadratic curve and mirrored) and two short quotes.
8. faq: native details/summary with a + that rotates to x.
9. cta: a store-style card with engine pills, a local-only email form (nothing is sent) with a dark "Request access" button, and a 4:3 key-art capsule rendered from the scene with the logo over it.
10. footer: logo, links and the fictional legal line.

PREMIUM DETAILS
- Station signs as section labels: each section is a stop on the line (SO02 to SO07) with a green-bordered code, the name in kana, the English name and a green band linking to the neighbouring stations.
- In-engine stills: after the opening shot, render four fixed shots through the main renderer (down the blossom tunnel, close on the pilot, flying away into the haze, the capsule key art) with toDataURL, restore the hero and send them in "corgi:shots"; the SVG art stays until each image loads, then cross-fades.
- Sound with Web Audio, off by default (HUD toggle or M): brown-noise wind through a wandering band-pass, pentatonic chimes, a far level-crossing bell, and a pluck per petal; suspended while the tab is hidden.
- A slight 3D tilt toward the pointer on cards and the capsule, CSS petal drift on the paper sections, a pop on the petal counter.

THINGS THAT BREAK
- Never give two elements the same id: a canvas and a section both called "world" let a ResizeObserver grow the canvas and the hero in a loop.
- Keep the static fallback (CSS sky, two hills, the SVG corgi) until the module has rendered a frame and added html.gl-on, and gate the play and sound buttons on that class, so a failed CDN never leaves a blank hero or a dead button.
- Pause the loop when the hero is off screen or the tab is hidden. Under prefers-reduced-motion render one still frame; play mode still animates because the visitor asked.
- The play buttons scroll with window.scrollTo, not scrollIntoView, which would also scroll a page embedding this one.
- Show the saddle meshes only when the coat has a separate saddle colour, or they z-fight.

THE FLOOR
- One h1, a main, aria-hidden on the canvases and decorative SVGs, labels on the movement pad, role=status on the toast, loader label and form message, visible focus rings.
- No horizontal scroll at 390px: grids collapse under 1000px, nav links hide under 760px, the HUD moves left.
- Reduced motion also turns off reveals, the petal drift, button transitions and the loader's bob.
