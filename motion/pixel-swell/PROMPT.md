# Pixel Swell · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a scroll-driven pixel-art seascape as one HTML file, in CSS: four bands of striped, stair-stepped waves roll under a red sun as the page scrolls, and the sky deepens to navy. No canvas and no libraries; a few lines of script only to create the bars and to fill in where new CSS isn't supported.

THE STAGE
- Palette as custom properties: --punch-red #e63946, --honeydew #f1faee, --frosted-blue #a8dadc, --pacific-blue #77abbd, --cerulean #457b9d, --baltic-blue #31587a, --oxford-navy #1d3557.
- html background punch red, and html::after a fixed, click-through 16px punch-red border on top of everything (z-index 100): the frame.
- body 600vh tall with no margin. Its background is the whole sky and the sun: radial-gradient(circle 500vh at 50% 50vh, punch red 0 30vh, honeydew 30.7vh, frosted blue 100vh, oxford navy 400vh). The sun is the first stop, so it scrolls away with the page.
- body::after is film grain: fixed, z-index 16, mix-blend-mode overlay at 0.35, four radial-gradient dot grids (white 0.9 and 0.7, black 0.8 and 0.6, about 0.5–0.6px dots) at 3, 5, 7 and 11px so the pattern never visibly repeats, each offset with random(0px, size).
- Four .wave rows, each position fixed to the bottom, 70vh tall, display flex, align-items flex-end, holding 60 <i> bars (flex: 1).

THE CHOREOGRAPHY
- @property --a { syntax "<angle>"; inherits: true; initial-value 0deg }, plus --amp (<number>, 1) and --off (<angle>, 0deg), not inherited.
- .wave runs @keyframes roll { to { --a: 360deg } } with animation: roll linear both and animation-timeline: scroll(root). Multiply by --turns (2) in the formula, so the knob doesn't need new keyframes.
- Per band, back to front: base 46/38/30/22vh, swing 4/5/6/6vh, speed 1/−1/2/−2, step 14/18/22/26deg, and a two-colour vertical gradient stepping through frosted blue → pacific → cerulean → baltic → oxford navy.
- Each bar: --amp: random(0.5, 0.9); --off: random(-5deg, 5deg); height: round(down, calc(base + sin(calc(--a × turns × speed + sibling-index() × step + --off)) × swing × amp), 8px); background linear-gradient(c1, c2); mask-image repeating-linear-gradient(0deg, #000 0 6px, transparent 0 8px).

THINGS THAT BREAK
- Register --a with @property, or the keyframe can't interpolate it and the waves jump.
- Use --a's inherited value in the bars, so animate it on the .wave and let it inherit; --amp and --off must not inherit, or every bar gets its parent's single random value.
- sibling-index() and random() are new: give each bar an inline --i (1..60) and seeded --amp / --off from script, and switch to the native functions inside @supports. Without scroll timelines (Firefox), write scrollY / max × 360deg into --a on scroll.
- Set history.scrollRestoration = "manual" and start at the top, or a restored mid-scroll lands with the sun gone.

THE FLOOR
- Nothing moves unless the reader scrolls; the only idle motion is a small SCROLL cue bobbing inside the sun, which prefers-reduced-motion stops. Everything decorative is aria-hidden and click-through. No horizontal scroll at 390px.
