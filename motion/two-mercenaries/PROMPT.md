# Two Mercenaries · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a two-character select screen as one HTML file: a dark and a light mercenary split the frame, hover lights a side, click picks it, click again zooms in. Black page, one full-viewport canvas, every image inlined as base64.

THE SCENE (a 1080 × 1080 artboard, contained and centred)
- Two halves: left, a black-armoured soldier on a near-black field; right, a white-coated soldier on a soft white field with a floor shadow. Each soldier is its own nested 1920 × 1080 artboard, cropped into its half.
- Each soldier is a skinned image mesh: a WebP texture on a triangle mesh whose vertices are weighted to up to four bones of a small skeleton. Draw the meshes in WebGL to an offscreen canvas and composite them into the 2D scene.
- Under each soldier, a small circle-and-line marker; a faint gradient seam between the halves.

THE STATES
- One number input, State: 0 idle (both even), 1 Dark (left scales to 1.1 and widens over the right), 2 Light (the mirror), 3 Dark ZOOM, 4 Light ZOOM (a close-up of that soldier filling the frame).
- Two booleans, Hover dark and Hover light, on a second layer: the hovered side lifts in brightness and the other dims.
- Every state is a single pose; transitions mix from the current pose to the next over 100 to 250 ms on a cubic ease. Clicks walk 0 → pick → zoom → pick → 0.

THE IDLE
- Each soldier loops its own breathing timeline under every state: the bones' rotations and lengths ease back and forth, one over 2s and the other over 5s at 0.8 speed, so they never move in step.

THE RUNTIME
- Each frame: advance the state machine by dt (capped at 0.1s), sample keyed values into the tree, recompose world matrices parent to child, solve bones, skin the meshes, repaint back to front.
- Hit-test the pointer in artboard space through each half's inverse world matrix; enter and leave set the hover booleans, a click advances State.

THINGS THAT BREAK
- Sample cubic eases by solving t from x, not by using progress as t, or the blends feel linear.
- Premultiply alpha in WebGL, or the soldiers get dark fringes on the light side.
- Cap DPR and size the WebGL canvas once per resize, not per frame.

THE FLOOR
The canvas has role="img" and an aria-label describing the choice; touch-action none so a tap picks instead of scrolling. Works at 390px wide.
