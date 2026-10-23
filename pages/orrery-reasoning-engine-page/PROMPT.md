Build a dark-and-light landing page for Orrery, a fictional AI reasoning engine ("the reasoning engine that shows its work": it reads a team's contracts, tickets, code and spreadsheets and answers with the sources behind every claim), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3, all from jsdelivr. Google Fonts: Hubot Sans with the width axis (wdth 100-125, wght 500-700) for display, Instrument Sans 400-700 for text. No images: every picture is a <canvas data-art="..."> drawn by one procedural art engine.

DESIGN SYSTEM
Warm greys with one ember accent. Tokens: ink #111110, night #191816, smoke #2a2926, ash #55574f, haze #a6a9a3, fog #c8cac4, mist #e7e6e1, pearl #f5f4f0, ember #d6b28a, steel #7d8c8b; a fluid gutter (16-64px), max width 1400px, section padding clamp(96px, 12vw, 190px), radii 14 and 24, ease cubic-bezier(.19,1,.22,1). Two SVG noise textures as tokens: --grain (fractal noise through a diffuse light, used as an overlay on dark surfaces) and --frost (the same, turned into a white alpha frost for veils). Each section carries data-tone="dark" or "light", which sets --fg, --fg2, --bg and --line, so components restyle per section. Display type is Hubot Sans 600 uppercase at font-stretch 112-125%; labels are wide-tracked caps (.38em); body is Instrument Sans 17px. Corner brackets (two L-shaped 2px corners, top-right and bottom-left) frame anything important. Buttons fill with ember from the middle out (a clip-path inset that opens) on hover; text links have a 1px underline that a 2px rule sweeps over.

THE ART ENGINE
One script, a seeded PRNG (mulberry32) per canvas from data-seed, a renderer per data-art name in an object F, each returning a draw(ctx, t) closure. Canvases are sized by ResizeObserver at a capped devicePixelRatio (data-dpr), drawn once, then animated only while an IntersectionObserver says they are on screen; with reduced motion they are drawn once at a fixed time. Renderers:
- orrery: deep space with a quarter-resolution painted nebula, three depth layers of twinkling stars and cross-shaped glints, a pulsing sun with corona rays, seven planets on tilted elliptical orbits (shaded spheres with banding, a lit rim, atmosphere glow, comet-soft trails, a ringed planet, moons that pass in front and behind), a dust belt, orbit tick marks, an anamorphic lens streak with ghost flares, collision-aware instrument labels (Reasoning · depth 0.94, Memory · 10M tokens, Verification · 2x sourced) and a vignette; the pointer tilts it slightly.
- deliberate: a search tree growing left to right, a scan front, losing branches crossed out, the winning path committing in gold with "ANSWER conf 0.97".
- memory: tokens streaming into a rotating Fibonacci sphere of points, a scanning latitude, gold arcs linking recalled points, a "RECALL doc 4,812 · p.31" callout.
- agents: a glowing hub with tool tiles (mail, calendar, database, code, chart, doc, chat, card) on an orbit; one tile stops and asks "CONFIRM?" then "APPROVED".
- vision: a chart scanned left to right, its axis, peak, legend and footnote boxed in gold as they are recognised.
- deploy: isometric server racks with blinking LEDs inside a dashed gold perimeter, traffic looping inside, outbound traffic stopped at a lock.
- grid, graph, stream, terrain, rings, lattice: attention heatmap, retrieval graph with travelling pulses, token stream past a cursor, ridgeline terrain with one gold line, verifier rings, a rotating 3D lattice.
- portrait: a scan-line portrait silhouette with a gold band sweeping down.
The premium renderers share a HUD: corner brackets, a caps label top left, a gold status top right and a tick ruler along the bottom.

SECTIONS
1. nav: fixed; the brand (an orbit glyph and ORRERY tracked wide), four links and Request access. It hides on scroll down, returns on scroll up, turns solid (blurred on desktop) after 40px and retints to the tone of the section under it. Under 1080px a full-screen grain menu with huge links.
2. hero (pinned for two screens): a blurred, slightly enlarged copy of the orrery fills the screen (the sharp canvas mirrors itself into it at quarter size), a haze and grain over it, the words THINK and SLOW huge above and below (sized from --len and the space left), and in the middle a sharp window onto the orrery with a glass rim, two corner brackets and two caps lines ("Fast answers are cheap", "Right ones take a moment"). Scrolling opens the window to the full screen (a clip-path inset driven by --open), the words leave up and down, the lines slide out and the brackets travel to the screen corners.
3. brief (light): a large statement whose lines "defog" from blurred to sharp on scroll (SplitText lines), a framed terrain picture, a lede, and a row of five invented customer marks.
4. capabilities (dark): five rows (version, topic, title, text, picture). As you scroll, the row at the middle of the screen is in focus, the others dim and blur, its picture opens from a thin slit, and two corner brackets travel to frame it.
5. process (light): five stages that rise in a staircase, each with a rule that draws, a duration (0.2 s, 1-4 s, up to 8 min, every claim, after), a caps title that wipes in and a line of text.
6. gallery (dark): six live renderings in a horizontal track pinned and scrolled sideways, behind a frosted pane with a rounded window cut out of it (a mask with a hole) and corner brackets on the window; shots scale down away from the centre.
7. results (light): four huge figures rising out of their lines (41%, 10M, 0, 2,300), and four bars of where an answer comes from (your sources 71%, model reasoning 19%, verification 7%, clarifying questions 3%) that grow on view.
8. team (dark): four portraits that open from a slit, with name, role and a line each.
9. reviews (light): four quote cards that stick and stack; each one shrinks and frosts over as the next arrives.
10. pricing (dark): a Monthly/Yearly switch and three tiers (Personal $0, Pro $24 framed in ember brackets on a pale card, Team $60 per seat) that open from the middle.
11. faq (light): a sticky side column and an accordion that opens on grid-template-rows.
12. contact (dark): a blurred graph canvas behind, contact channels, and a light form card that unfrosts as it scrolls in.
13. footer: a newsletter, three link columns, a legal line saying the company is fictional, and ORRERY huge over an ember glow, rising on scroll.

THINGS THAT BREAK
- Put html.motion on in <head> only when motion is allowed, and take it off if GSAP has not arrived in 2.5s; scope every hidden-until-animated state under .motion.
- The hero window's clip-path and the rim must use the same custom properties (--sw, --sh, --sy, --sr), or they drift apart at other sizes.
- The horizontal gallery needs its scroll distance (track width minus the viewport) measured on every refresh, and the window hole positioned from the track's real height.
- Queue the scroll scenes and build them in idle time after fonts load, then refresh ScrollTrigger; re-read section tones for the header on every refresh.
- Canvases must stop drawing when off screen, or a page of eighteen animated canvases will burn a laptop.

THE FLOOR
One h1 (the hero words, with the brand in a visually hidden span), a main, a labelled menu button with aria-expanded, role="img" and an aria-label on every meaningful canvas, aria-hidden decoration, buttons with aria-pressed for billing and aria-expanded for questions, live form status, visible ember focus rings. With motion reduced the page is complete and static. No horizontal scroll at 390px.
