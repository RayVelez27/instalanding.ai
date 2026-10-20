Build a dark landing page for Corelane, a fictional product that pools the idle CPU cores in a team's laptops with one on-site "core" server into a private build cluster, as one HTML file with no libraries and no images. Every machine, server and circuit is inline isometric SVG.

FONTS (Google Fonts)
Oswald 400/500 for display (uppercase hero, tight line-height 0.96) and buttons; Instrument Sans 400-600 for text.

TOKENS
night #0f054c (page), night-2 #160a5c, indigo #24126a, ring #706ec4 (pill outlines, rules at 32% alpha), lavender #e9e9fd (text, filled buttons), muted #b6b3e3, faint #8a86c9, cyan #42e8e0 (available, focus rings), magenta #e84298 (building). Wrap 1200px, gutter clamp(20px, 4vw, 40px).

ATOMS
Pill buttons 48px high: transparent with a 1.5px ring outline, or filled lavender with night text; Oswald uppercase, letter-spacing .04em. A brand mark of nine small squares in a 3x3 grid rotated 45deg (cyan, lavender, one magenta centre).

SECTIONS
1. nav: fixed; transparent at the top, then night at 78% with a 14px backdrop blur and a hairline after 12px of scroll. Links with a scaleX underline and a scroll-spy current state; Sign in (ring) and Start free trial (filled). Under 860px a round menu button opens a full-width drawer.
2. hero, 5/7 columns: headline YOUR TEAM'S LAPTOPS ARE ALREADY A BUILD CLUSTER, a lead, two buttons, a note. Right, a stage (aspect 400/320) with: a violet radial glow; a circuit-trace field behind the art (one path mirrored to the right, feathered on all four edges with intersecting mask gradients) where a pink-then-cyan ring of light (an animated radial gradient r 60 to 620 over 3.6s, masked by the traces) pulses outward along the lines; the isometric illustration of four laptops around a server whose top is a 9x9 grid of LED diamonds that light magenta in waves. Under it a segmented control "Team machines / Core server": the second swaps the art (fade and 0.985 scale for 220ms) to a stacked core server, the glow turns teal and the circuits give way to an isometric grid with rippling diamond rings, blinking tiles and rising motes around the core. Clicking (or Enter on) the server lifts it out of the stack and back.
3. product: "Spare cycles, put to work", a two-column ledger (not cards) of four features separated by hairlines, each with a small isometric glyph.
4. fleet: "Every machine on the team, one queue". Left: a lead, a readout list (Machines available N of 96, Full build on one laptop 41m 00s, Full build with Corelane), Run a build and a legend. Right: a 12x8 grid of buttons on a lavender plate tilted rotateX(57deg) rotateZ(45deg) with a 10-step stacked box-shadow for thickness. Cells are cyan (available, glowing), dark violet (asleep, nine start asleep) or magenta (building). Click a cell to toggle sleep; arrow keys move a roving tabindex. The estimate is 2460s / (1 + 0.16 x (n - 1)). Running spreads "building" outward from the centre (delay = distance x 70ms), clears each cell at a staggered time, counts the estimate up over 2.6s and announces start and finish in a live region.
5. how: three numbered steps with isometric art (a laptop, the core box, the stacked server); step 3 shows the one-line config in a code chip.
6. pricing: a Monthly/Yearly role="switch" (yearly saves 20%), three joined plans (Studio $0, Team $19/$24 per machine featured in lavender with a badge, Campus custom).
7. faq: details/summary with a chevron that rotates.
8. cta: a rounded card with a radial indigo gradient, headline, an email form with inline validation, and the small core-box art.
9. footer: four columns and a legal line saying the product is fictional.

THE HERO RUNTIME
The illustration is exported vector-animation data replayed by a small runtime: a JSON object of nodes (x, y, rotation, scale, opacity), colour-keyed elements, morphing paths (straight, rounded and cubic vertices rebuilt into a d string each frame) and keyframed animations (oneShot, loop or ping-pong, speed multiplier, a cubic-bezier ease solved by bisection). A four-layer state machine picks "laptops" or "server" from the segmented control and plays the "up" animation forwards or backwards on the server click. Only write attributes that changed (dirty sets), cap dt at 0.1s and pause the loop with an IntersectionObserver when the hero is offscreen.

THINGS THAT BREAK
- The animation targets elements by id (n1768, p14874...): keep those ids when editing the SVG.
- Give every repeated SVG its own gradient id prefix (lp, co, sv, ca) or the steps' art picks up the hero's gradients.
- Pause the SVG SMIL animations of the circuit field (pauseAnimations) while the core scene shows, and pause the core field's CSS animations when it is hidden.

THE FLOOR
A skip link, one h1, a main, aria-hidden decoration, labelled grid and form, visible cyan focus rings. Under prefers-reduced-motion: no entrance, no SMIL, the scene jumps to its end state and the build finishes instantly. No horizontal scroll at 390px.
