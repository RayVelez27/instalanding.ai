Build a single-file HTML landing page for "Facetry", a fictional access-control and security platform ("Security, cut to shape."). The look is black glass and brushed chrome: near-black surfaces, metal gradient type and buttons, and one hero object, an extruded metal logo standing on a rough stone block in a real CSS 3D scene. The brand mark morphs between three shapes (diamonds, shield, triangle) on a spring, everywhere it appears. Fictional product, labelled as such in the footer. No libraries, no images, no web fonts: system UI and system mono, inline SVG, CSS 3D and one inline script.

THE SYSTEM
- Colours: page #000 with #09090b surfaces, text #f4f4f5 / #d4d4d8, soft #a1a1aa, muted #71717a, faint #3f3f46, hairlines white at 6% and 10%.
- --metal is a vertical gradient #fbfbfb → #e4e4e4 (18%) → #cccbcb (55%) → #9e9d9d. It fills .metal-text (background-clip text) in every headline's second line, primary buttons (dark ink text, inset white top line, soft white glow), badges, tags and tiny 45deg diamond bullets.
- Surfaces are 32px-radius cards with a top-lit radial (white 5% → 1% → black 40%), an inset 1px white top line at 12%, an inset hairline and a deep black drop shadow. Hover lifts 4px and brightens the top line.
- Background: a fixed diagonal stripe field (repeating 135deg gradient between #0e0f10 and #18191b, 70% opacity) drifting slowly, under a radial vignette that pulls the edges to black.
- Motion uses one ease, cubic-bezier(.16, 1, .3, 1). Reveals fade up 28px from an 8px blur with staggered delays.
- The rock texture is an inline SVG data URI (feTurbulence fractal noise into feDiffuseLighting with a distant light) used as a CSS variable.

THE MORPH ENGINE
- Each shape is four layers of cubic Bézier paths with the same number of points in every state: an outer and inner contour (an even-odd compound path) plus three detail layers. Straight polygon edges are converted to cubics (control points at thirds), so any state can tween into any other.
- A Morph class springs every coordinate toward the target state (stiffness 175, damping 22 by default) with a little scale kick on each switch, adds a motion blur proportional to speed, and marks itself settled when the speed falls below a threshold, so idle morphs cost nothing. It auto-advances every 2-3s, pauses on hover, and advances on click; tab buttons show a progress bar filling until the next switch. An IntersectionObserver stops off-screen instances. Under reduced motion it jumps straight to each state.
- Metal finish: SVG filters add a dark drop shadow and a 1px white top-edge highlight (feOffset + feComposite out + feFlood). Static icons across the page use the same paths and filters.

SECTIONS (data-section in order)
1. nav: a fixed floating pill (blurred dark glass, inset highlight) with the metal mark and "Facetry", four links, and a metal "Get started".
2. hero: a "2.0 · Adaptive policies are here" badge, the h1 "Security, / cut to shape." (second line in metal) at clamp(48px, 5.4vw, 92px), the lede, a big metal "Start building" and a ghost "See it move". Three chips (Precision, Protection, Foundation) with outlined icons double as the hero morph's tabs. The right side is a 640px CSS 3D scene (perspective 2200px, preserve-3d) tilted -19deg / -34deg that eases toward the pointer on a spring: a masked grid floor with a soft glow, a stone pedestal built from three clipped faces with chipped top edges and the rock texture, its shadow, the extruded logo (ten dark slices stepped 2.2px back in Z behind a brushed front face with a diagonal sheen), a flare, light rays, twinkling sparks, and glass panels with "+" corner marks floating at different depths: a tall back panel, a small icon tile, a dotted world map drawn from an ASCII grid, and a list (POLICIES, ACCESS, CONTROLS, MONITORING) whose active row follows the shape.
3. marquee: a masked strip of features with small icons, looping.
4. platform: "Three shapes. / One system." Three bento cards (Precision, Protection, Foundation) with a metal icon, a mono number, copy and diamond-bulleted lists, then a wide card with a "Policy as code" pitch beside a syntax-highlighted code window.
5. motion-lab: "Motion with mass." A stage card with its own morph and a dock of three tabs, beside a control card: presets (Default, Snappy, Bouncy, Heavy), stiffness and damping sliders with metal thumbs, and a live response curve (simulated at 240Hz over 1.4s) with a "settles in N ms" readout. Changing it retunes the lab morph.
6. stats: four big numbers that count up on a spring (3.2ms p99, 99.999%, 24 regions, 40B decisions).
7. pricing: "Pick your facet." Three tiers with metal icons; the middle one is featured with a glow and a "Most chosen" tag.
8. faq: four questions that open on an animated grid-template-rows 0fr → 1fr, with a plus that turns into a minus.
9. footer: one big rounded surface holding everything: a cursor-following spotlight, a huge outlined metal triangle slowly spinning behind, a hairline top edge; "Find your shape." with an email pill that swaps to "You're in ✓" and reshapes the CTA morph, assurance ticks, a tap-to-reshape stage; a live region band (SFO, IAD, LHR, FRA, SIN, SYD) with local clocks from Intl.DateTimeFormat and jittering p50 latency bars ticking every second; link columns with diamond hover markers; legal row and a back-to-top pill.

THINGS THAT BREAK
- Every morph state must have exactly the same number of numbers per layer, or the tween jumps. Keep the layer count fixed at four and pad simple shapes with extra cubic segments.
- A CSS blur on the 3D logo flattens its preserve-3d extrusion, so the hero morph skips motion blur.
- Give the hero grid columns min-width: 0 and scale the 3D scene with a --s variable per breakpoint, or the 640px scene pushes the page sideways.
- Run every morph, the parallax and the counters from one requestAnimationFrame loop with dt capped at 32ms, so a background tab does not explode the springs.

THE FLOOR
- Breakpoints at 1180px (hero stacks and centres), 920px (bento, lab, tiers and footer go to one column) and 640/520px (chips stack, region grid to two columns). No horizontal scroll at 390px.
- Real buttons for chips, tabs, presets and FAQ (aria-expanded), labelled sliders with outputs, a labelled email field, decorative SVG aria-hidden, and a prefers-reduced-motion block that stops the drift, marquee, sparks and spin and shows reveals immediately.
