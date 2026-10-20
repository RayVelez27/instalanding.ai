# Glow Boards · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a stack of glowing boards that lift on hover, as one HTML file drawn with Canvas 2D: no libraries and no images. Black page, one full-viewport canvas.

THE SCENE (a 565 × 565 artboard, framed on the stack)
- Sixteen boards: 80 × 80 rectangles under a nested transform each (rotate -0.366 rad, scale 1.54-1.59 by 1.27; inside it rotate -0.12, scale 0.357 by 1.009; the shape itself rotate -1.018, scale 0.865 by 0.931), so each reads as a thin isometric plate standing at an angle. They sit in a diagonal line from about (152, 314) to (356, 181), stepping roughly 27 units right and 19 up, in pairs that share a position.
- Each board is layered fills: a #373737 base softened by a 30-unit feather, a #535252 face, a #cbc4c4 inner feather offset (-1, 1) for a lit edge, then two outer glows in rgba(235,235,235,0.4) and 0.25 with 20 and 40-unit feathers.
- Behind the stack, one large quadrilateral filled with two overlay-blended linear gradients: hot pink rgba(255,0,70,0.83) through electric blue rgba(8,0,255,0.82) to cyan #00f7ff. Overlay blending is what tints the grey boards pink at one end and cyan at the other.
- Paint back to front (the first in the tree is on top). Fit the stack box (x 100, y 108, w 372, h 336) to the viewport, contained and centred; cap DPR at 3.

THE FEATHER (soft glow)
A feathered rectangle is a Gaussian-blurred rectangle with sigma = strength / 2. Build it once per size and colour as a sprite: the alpha at each pixel is a separable product of two 1D profiles, 0.5 × (erf(u / (√2σ)) − erf((u − width) / (√2σ))), padded by 3σ, at 3 sprite pixels per unit. Draw it with the shape's transform. An inner feather is the shape clipped, minus a copy of itself offset by the feather offset (evenodd fill).

THE MOTION
- One boolean input and one state-machine layer per board. Hover true plays the hover animation: the board's y eases up over about 30 frames at 60fps on a cubic bezier around (0.42, 0, 0.35, 1.03) (a slight overshoot). Hover false plays the unhover back down over about 30 frames, slower to start (around 0.70, 0.02, 0.58, 1). Lifts range from 26 to 81 units depending on the board.
- Each frame: advance every layer's animation by dt (capped at 0.1s), write the sampled y back, recompose world matrices from parent to child, repaint.

HOVER
Map the pointer into artboard space, then into each board's local space through the inverse of its world matrix, and test it against the 80 × 80 rectangle. When a board's hit state changes, fire enter (hover true) or leave (hover false). pointerleave and pointercancel release everything.

THINGS THAT BREAK
- Composite in the order Rive does: each fill keeps its own blend mode, and the background gradient must be overlay, not normal, or the boards stay grey.
- Sample cubic eases by solving for t from x (bisection), not by treating the progress as t, or the overshoot vanishes.
- Precompute feather sprites; blurring every frame with a canvas filter costs far more and differs by browser.

THE FLOOR
The canvas has role="img" and an aria-label describing the stack; touch-action: none so a tap-drag hovers instead of scrolling. Works at 390px wide (the stack is contained and centred).
