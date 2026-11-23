# Surprise Keys · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a pressable isometric letter as one HTML file: a lowercase "a" made of 229 blue keys that breathe in and out, pop up when hovered and sink flush when pressed. White page, one full-viewport canvas, Canvas 2D, no libraries.

THE LETTER (a 600 × 589 artboard, contained and centred, clipped to its bounds)
- 229 instances of one 200 × 200 button, each scaled to 0.26, laid on a slightly skewed grid in the shape of a round lowercase a: a thick ring with a stem down its right side.
- Paint them in reverse order so the front rows overlap the rows behind.

ONE BUTTON
- The face: a square with its right edge raised 8 units, filled #317ae7, stroked #4c3cc5 at 5px with round joins.
- The extrusion: a five-point polygon filled and stroked #1b0d83, drawn under the face. Its back vertices are weighted to a fixed bone; its front vertices to a bone that follows the face. Skin it each frame so the walls stretch as the face moves.
- A hit area: the face's square at rest, invisible.

THE MOTION (only the face node's x and y move)
- Idle: ping-pong between raised (61, 61) and sunken (128, 125) over 41 frames at 60 fps, on cubic-bezier(0.34, 0.01, 0.35, 0.97).
- Hover: a single pose at (49, 49), above rest. Click: a single pose at (128, 125), flush with the base.
- Transitions mix from the current value to the target pose: idle → hover 70 ms (0, 0.79, 0.23, 0.97); hover → idle 300 ms (0.79, -0.01, 0.2, 0.99); hover → click 50 ms (0, 0.81, 0.23, 1.01); click → hover and click → idle 250 ms (0.73, 0, 0.3, 1).
- Every key runs its own copy of this three-state machine. Inputs: hover on pointer enter and leave, click on pointer down and up.

THE INPUT
- Map the pointer into artboard space, then into each key's space through the inverse of its world matrix, and hit-test the rest-pose square with a winding-number test. Points outside the artboard count as outside every key.
- Capture the pointer on down so a press released off the key still lets go.

THINGS THAT BREAK
- Sample cubic eases by solving t from x (Newton, then bisection), not by using progress as t, or the springs feel linear.
- An interrupted transition must start from the value it reached, not from the old pose, or keys jump when you sweep fast.
- Cap dt at 0.1s so a background tab doesn't fire every transition at once.

THE FLOOR
The canvas has role="img" and an aria-label describing the letter; touch-action none so a tap presses instead of scrolling. Works at 390px wide.
