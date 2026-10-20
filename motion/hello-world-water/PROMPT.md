# Hello World Water · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build an interactive pool seen from straight above, where the water rises into the word HELLO, holds, collapses into ripples, and then rises into WORLD, in a loop. One HTML file, three.js 0.180 as an ES module from jsdelivr, no images.

THE STAGE
- Page #eef0ec, a canvas centred at min(900px, 90vw, 123vh) wide with a 20:13 aspect and a soft teal shadow. A perspective camera (42°) looking straight down, fitted so the 8 × 5.2 pool fills it. ACES tone mapping, sRGB output.
- If WebGL 2 or float render targets are missing, show a plain error message instead.

THE SIMULATION (GPU)
- A 256×256 half-float height field ping-ponged between two render targets at a fixed 1/120s step (accumulate dt, cap 1/20). Red is height, green is velocity.
- Each step: velocity += laplacian (weighted for the non-square cells) × 1.21 × dt, damped by exp(−0.64 dt); then a spring toward the word: velocity += (mask.r × letterHeight × form − height) × 95 × pull × dt with pull = form × (0.18 + 0.82 × mask.g), extra damping exp(−4 pull dt); height += velocity × dt. Up to 16 queued impulses per step add (1 − q) e^−q bumps.
- Word masks: draw the word in 900-weight Arial Black on a 256 canvas, scaled vertically by 8/5.2 so letters stay square on the water; a light blur for the letter (r) and a wide normalised blur for the pull (g).

THE TIMELINE
- form eases up over 2.8s (smootherstep), holds 3.8s, then lets go fast (9× the rise rate) for 1.6s, rests 1s, and the next word takes over. While rising, fine spray lifts off the strokes; on release, 11 splashes burst at random points of the word and push the leaves away.
- An ambient sum of ten directional sine waves (domain-warped, sheltered, and calmed 72% while the word stands) rides on top, in the shader and in a matching CPU function so floating things bob in sync.

RENDERING
- The water mesh (256×256 plane) displaces by the height map plus ambient waves; normals by central differences.
- Fragment: refract the view ray (1/1.333) into a box basin (floor at −1.35, walls at ±4 / ±2.6) with procedural tiles (two teals, darker grout), wall caustics, ambient occlusion near edges, absorption exp(−(0.34, 0.075, 0.032) t), and soft shadows from leaves and splashes projected along the sun. Reflect into a generated sky with Fresnel (0.02037 + 0.97963 (1 − cos)^5), a sharp sun highlight, and lift raised water brighter and greener with a pale rim on steep flanks so the word reads.
- Caustics: a second pass renders the same grid refracted to the floor into a 1024 target, intensity = area before refraction ÷ area after (dFdx/dFdy cross products), additive.
- The sun drifts slowly round; a hemisphere light and a sun light for the leaves and droplets.

THE LIFE IN IT
- Splashes: instanced glassy droplets with gravity that make a small impulse where they land, plus a crown mesh (a ring of 64 quads with lobed height) that grows and fades in 0.4–0.6s.
- Ten leaves (six afloat, the rest falling in every 7–13s): drift on a current with two pool-return jets, bob and tilt on the ambient swell, collide softly, spin down, ride up over raised letters and are shouldered downhill off them.
- Rain (W or a control): eases in, adds a fine chop to the shader, greys the sky, dims the sun, and drops streaks that make tiny impulses and occasional droplets.

INPUTS
- Drag: segmented impulses along the path and leaf stirring; fast drags throw splashes. Click: a pebble (deep impulse, crown, leaves pushed). Double-click: a cannonball (bigger cavity, a central jet 210ms later). Keys: R reset, W rain, N next word, Space a random pebble.

THE FLOOR
- The canvas is focusable with a visible focus ring and an aria-label describing the loop. Handle context loss with a message and reload on restore. Cap the pixel ratio at 1.7 and pause while the tab is hidden.
