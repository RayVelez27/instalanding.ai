# Peekaboo Orange · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a peekaboo cursor-follow character as one HTML file: a cartoon orange hides in a hole under a bobbing arrow, pops up when the pointer arrives, follows it with his head and eyes, and ducks back down when it leaves. Charcoal page (#212121), one full-viewport canvas, Canvas 2D, no libraries.

THE STAGE
- A 500 × 500 artboard, contained and centred, so it fits a phone's width.
- A glowing purple hole: a flat ellipse with a magenta-to-violet gradient, low in the frame.
- Over it, a chunky 3D-style down arrow: a gold-to-violet gradient front face, a purple extruded side, a dark purple outline and a soft cream shine sweep.
- Above the arrow, INSTALANDING in a rounded bold face (Fredoka 700), extruded six steps down-left in purple, gold-to-violet front, the same outline. Parent it to the arrow so it moves with it.

THE CHARACTER (drawn in code)
- A big glossy orange head with freckles and a curled ear, a purple top hat tipped to one side, a green curl on top, green brows, big cream eyes with dark pupils, a button nose, one tooth and a purple tongue, on a thin stalk neck with a green polka-dot bow tie.

THE STATE MACHINE (one bool: hovered)
- Up/down layer: idle in the hole → (hovered) jump out, 1.33 s → a loop while up (a small sway, about 2 s) → (not hovered) jump in, 0.6 s → idle.
- Arrow layer: bob (2.5 s loop) → (hovered) dive into the hole, 0.33 s, squashing as it goes → rest out of sight → (not hovered) rise, 0.47 s, then a 200 ms blend back into the bob.
- Blink layer: a blink every 3 s, always running.

THE FOLLOW
- An invisible handle node moves to the pointer on every pointer move.
- A joystick maps the handle's position inside the 500 × 500 box to x and y from -1 to 1, and scrubs two hand-keyed animations (head turn and lean on x, tilt and eye height on y) to that point. Apply it after the state machine each frame.

THE INPUT
- A full-stage hitbox: enter sets hovered, leave clears it.
- Touch: ignore the pointerleave that follows a lifted finger. A tap calls him up, a drag steers his gaze, and a second tap without a drag sends him back.

THINGS THAT BREAK
- Hit-test and place the handle through the inverse of the view transform, the same one you draw with.
- Sample cubic eases by solving t from x, not by using progress as t.
- Cap dt at 0.1 s so a background tab doesn't fire every transition at once.

THE FLOOR
The canvas has role="img" and an aria-label describing the character; touch-action none so a drag doesn't scroll. Works at 390px wide.
