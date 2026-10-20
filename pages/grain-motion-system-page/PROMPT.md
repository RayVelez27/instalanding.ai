Build a single-file HTML landing page for "Grain", a fictional motion and surface system sold as plain CSS. Two halves have to agree with each other: a micro-transition token set (four easing curves, five durations) and a grainy radial gradient that is the only artwork on the page — and the gradient's middle stop is also the accent colour, so switching colourway re-themes every component in the same frame. Space Grotesk, Inter and JetBrains Mono from Google Fonts, everything else inline, no image files, no libraries. Say in the footer that the product and every number are invented.

THE MOTION HALF — nine numbers, and nothing outside them
- Curves: enter cubic-bezier(0, 0, 0.2, 1), exit (0.4, 0, 1, 1), standard (0.4, 0, 0.2, 1), spring (0.34, 1.56, 0.64, 1).
- Durations: micro 80ms, fast 120ms, standard 200ms, moderate 280ms, slow 400ms.
- Compose shorthands from those two tables (--t-color, --t-lift, --t-enter, --t-exit) and build every component from the shorthands. Nothing on the page may animate with a number that is not in the table.
- The rules that make it feel deliberate: cards lift 1-3px on the spring curve, everything that gets pressed snaps at a hard 60ms, focus rings never move anything, and a tooltip waits 400ms to appear and leaves instantly — set transition-delay on :hover and zero it on :not(:hover) or it hangs around.

THE BUTTON
Adapt the Uiverse button by ryota1231 rather than inventing one, and keep its whole choreography: a 100px pill that squares off to a 12px radius on hover, a 2px ring that expands to 10px of nothing, a small dot in the middle that grows into a full-bleed fill, and the label sliding sideways while one arrow leaves to the right and a second arrives from the left. Press scales it to 0.96.

Re-express the timing in the system's own table — the original runs 0.6s and 0.8s of cubic-bezier(0.23, 1, 0.32, 1), and a page whose headline is "fewer curves" cannot quietly adopt a fifth one. The radius morph, the label slide and the arrow travel are --d-slow on --ease-enter, the fill is --d-moderate, colour is --d-fast, and the press stays at 60ms. It reads the same and the table still has nine numbers in it.

Build it with no markup beyond a label span: the dot is .btn::before with isolation: isolate on the button and z-index: -1 on the dot, which puts it above the button's own background and below its label; the two arrows are the label's ::before and ::after, masked from one inline-SVG data URI so they take currentColor. Each variant owns a --fill (the accent for primary and danger, accent at 8% for secondary, surface-2 for ghost), so the colourway drives the button too. The 36px icon button runs the same choreography as a circle that squares off. Buttons that already carry an inline icon skip the arrows and keep everything else.

THE SURFACE HALF — the grain
An feTurbulence turbulence at baseFrequency 0.9, two octaves, feeding an feDisplacementMap at scale 30 over a radial-gradient(circle at 50% 100%, c1 20%, c2 40% 50%, c3 55%). Three things it needs:
- Draw the filtered layer at 110% and pull it back -5%: the default filter region clips at +10% and the displacement drags pixels past the element's edge, leaving bald corners otherwise.
- Animate the turbulence seed with SMIL — values="1;2;3;4" dur="0.8s" calcMode="discrete" — so it flickers like film. Animate it smoothly and it turns into a lava lamp.
- Ship a second, quieter filter at scale 11 for anything small. A 26px chip run through scale 30 dissolves into confetti.
Put the grain on a ::before so the host can still hold text: the hero panel, the nav mark, the section dots, the card thumbnails, the modal icon and the colourway swatches are all the same class.

HOW THE TWO HALVES MEET
Define a colourway as three gradient stops plus the accent they imply, on [data-way="..."] at the root, and derive --accent-soft/-mid/-glow with color-mix. Four ways: rose #c24a6d, amber #a96a1e, cyan #256f7c, violet #5c48b8. A swatch row sets one attribute on <html>; because every tint on the page is a mix of that one variable, the toggles, focus rings, badges, danger button, easing balls, section labels and the hero gradient all re-tint together. That single wire is the whole reason the page reads as one system rather than two references bolted together.

THE PALETTE AROUND IT
Warm paper: #f5f3ef ground, #fdfcf9 surface, #eeece7 and #e6e3dc for recessed, #dedad2 borders, #0d0d1a brand ink. Shadows are brown-tinted — rgba(90,55,20,.07) through .14 — because neutral grey shadows on a warm ground read as dirt. Space Grotesk for display (300 for the light half of a headline, 600-700 for the strong half), Inter for UI, JetBrains Mono for values.



FRACTURE
Every module reads as a plate that has been broken out of its frame: two or three jagged chunks snapped from its corners, dark and dead at rest. Put a pointer on one and the torn edges light amber along the break and the module's rim lights with them. Press it and the pieces fly home and vanish and the plate seals - rim lit, face warmed from the top. Amber throughout: the panel already has exactly one colour and this is not the place to introduce a second.
Break the plate at its OWN corners, clipped to itself. The version of this that floats shards outward into the space around the button works because a demo canvas is empty; a panel is not. Thrown outward they land on the headline and on the bay next door. Cropping each piece against the corner it came from is also what sells it - a shard cut off by the module's edge reads as snapped from it, where a whole pebble sitting on the face reads as debris dropped on top. Corners are the only region of these modules reliably free of content, since the bays centre their instrument and the cards run copy down the middle.
Scale the pieces to the module rather than picking a pixel size, or a 20px chip beside a 590px bay just looks like litter. Seven to nine vertices at 0.66-1 of the radius: more points or a wider jitter and the polygon comes out a spiky star that reads as a leaf instead of a chunk.
Generate them so no two modules break the same way, and so the page keeps plain plates if the script never runs - a module that is merely uncracked still looks like a module. Give each piece the vector back to its module's centre in a custom property and let the press state use it.

TYPE-ON
Headings and copy print themselves when they reach the viewport, a few glitch characters flickering through each letter before it settles. Two things make the difference between this reading as a machine printing its own labels and as a broken page.
Split IN PLACE. The usual version of this effect reads textContent and rebuilds the element from a flat string, which throws away every inline tag it contained - on this page that is the em carrying the one piece of colour in the headline. Walk the text nodes and wrap each character instead and the tree survives intact. Normalise whitespace while you are in there, or the newlines and indentation of your own source each take a typing tick and the line appears to stall.
Reveal with opacity, never display, so the block occupies its finished size from the first frame and nothing below it moves while the line runs. That also means the full sentence is in the accessibility tree the whole time, so there is no need for the hidden duplicate this effect usually ships with.
Keep it away from anything the page rewrites. Live readouts are replaced every frame; split one and its spans are gone on the next tick. Body copy also needs its own speed - 140 characters at a heading's pace is five seconds of somebody waiting to read a paragraph.
Give the panel real space above the first heading and below the last readout. The block padding is the only thing holding the headline off the top edge and the readings off the bottom one.

SECTIONS
Sticky blurred nav; a hero with the headline split light/bold, an install line with a copy button, and the grain panel carrying the caption in the accent with a real component card floating over its corner; 01 the colourway switch with three explainer cards; 02 the tokens, with four easing balls running the four curves against the same clock and a five-row duration scale that lights on hover; 03 a component bench with tabs for Buttons, Inputs and Overlays — every control live, each panel footed by a mono line naming the exact durations it just used; 04 three interactive-state cards; 05 three pricing tiers; 06 a FAQ built from native details/summary; a closer and a footer.

WHAT WILL BREAK
- A .nav-burger { display:none } declared before .btn { display:inline-flex } loses on source order, not specificity — the burger shows at every width. Scope it to .nav .nav-burger.
- White text on the grain only works over the saturated middle band. The top is pale and the bottom is cream, so put the caption in the accent instead of fighting it, and keep any white line inside the band.
- prefers-reduced-motion collapses every transition to 0.01ms, but CSS cannot reach a SMIL animation inside a filter. Call pauseAnimations() on the defs svg from script: the texture stays, the flicker stops.

RESPONSIVE AND A11Y FLOOR
Hero goes one column at 900px, the grids collapse 4-2-1, the nav links become a burger at 880px. No horizontal scroll at 390 or 1512. Every control is a real button with a focus ring, the dropdown and modal both close on escape and on outside click, the modal returns focus to the button that opened it, and the tab strip carries role="tablist" with aria-selected.

THE SECOND GRAIN — dither
The hero's grain and this one are opposites and the page should show both. The hero is continuous tone warped by a displacement map. Dither is a hard ordered break-up: a fill that holds solid and then falls apart into loose pixels at its edge.
Two mask layers make it. One is a small tiled PNG of random alpha, the other a radial gradient. Mask layers composite with add by default, and that default IS the effect rather than something to correct - where the gradient is opaque it wins and the colour stays solid, and only through the gradient's soft band does the noise get a say and scatter the edge. Force the layers to intersect and the whole shape dissolves at once, which is a different look. Set image-rendering to pixelated or the browser smooths the tile back into a gradient and there is nothing left to see.
Make the swept layer four times the element's width with the gradient repeating every half, then the hover animation can travel exactly one tile and the loop has no seam. A second layer on the same element, its gradient starting where the first finished and its mask cut further down, gives two colours meeting in a band of mixed pixels instead of on a line; the element's own background is the third colour.
Two places for it, doing two different jobs. On the cards under the hero, drive it from the accent so the colourway switcher still re-tints them - the section's whole argument is that one decision moves everything, and a card that ignores the switch contradicts the copy beside it. On the swatch walls, keep the source palette whole and fixed, because a wall re-tinted to match the page proves nothing about carrying multiple colours.
Lay the walls out on a grid, not wrapping flex. The captions are wider than the shapes and of different lengths, so a flex row breaks after five and strands the sixth on a line of its own.

