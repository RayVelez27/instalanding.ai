# Jelly Squeeze · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a drag-to-squeeze jelly toy as one HTML file: a glossy raspberry jelly on a white plate under a clear acrylic press. Drag vertically to press it flat; let go and it springs back with a wobble. No libraries, no images: everything is drawn in Canvas 2D.

THE STAGE
- Page #b1b3c0, ink #464e60, system-ui. One screen, overflow hidden, user-select none. A small tracked caps mark top-left. Centred, a 4:3 canvas wrapper, width min(640px, 94vw, (100svh − 96px) × 4/3), canvas radius clamp(22px, 6vw, 42px), fading and scaling in from 0.92.
- Bottom centre: an h1 "Drag vertically to squeeze" (17px, weight 450) and a custom "Follow mouse" checkbox (16px box, ink fill and white tick when checked), hidden on coarse pointers.
- Over the middle of the canvas, an invisible drag pad (72% × 78%, pill radius, cursor grab, touch-action none) with role="slider", aria-valuenow 0-100 and aria-valuetext.

THE SCENE (a 640 × 480 design space scaled to the canvas; DPR capped at 2)
- Background: vertical gradient #d4d5df → #c2c4d0 → #a7a9b8, a soft white floor glow.
- Plate: a shadow ellipse, a white-to-#d9dae6 ellipse (rx 236, ry 36) and an inner #eceef6 well, floor at y 352.
- Jelly: a superellipse outline (n = 3.6) sampled at 120 points in its own (u, v) space, mapped as x = cx + u·w/2·(1 − 0.13v + bulge), y = floor − v·h. Rest size 250 × 196.
- Fill inside a Path2D: a vertical gradient #ff9db0 → #f0416a → #a50f3c at 94% alpha; clipped to it, a warm screen-blend glow low right, twelve faint wide strokes for darker edges, 16 seeded bubbles (ring, faint fill, highlight dot), a white sheen down from the top face, a left rim light (stroke with a horizontal white → clear gradient), a rotated soft specular top-left and a small sharp one right. Outside: a 1px deep-pink outline, a dark contact shadow and a pink caustic glow on the plate.
- The press: a 42px translucent stem from the top and a 430 × 26 rounded acrylic slab (white gradient, white hairline, an inner highlight line), tinted pink where it touches the jelly. As it nears the jelly, darken the jelly's top face.

THE MOTION
- goal (0 lifted … 1 full squeeze) comes from the drag: Δy ÷ 220px (× 0.55 on touch). Keep the last 6 samples; on release, velocity = Δgoal ÷ Δt over them (0 if the pointer had stopped for 80ms). The throw: goal += vel·dt, vel ×= e^(−dt/0.28), stop dead at 0 or 1.
- shown += (goal − shown) × (1 − e^(−0.11·60·dt)). The press bottom sits at floor − (196 + 46) + shown × (196 + 46 − 0.42 × 196).
- The jelly height h is a damped spring toward 196: a = ω²(196 − h) − 2ζω·hv, ω = 2π·2.1, ζ = 0.05 + (1 − wobble) × 0.55, four sub-steps per frame. If h passes the gap under the press, clamp it and drop upward speed.
- Width w = 250 × (196 ÷ h)^0.55; bulge = squash × 0.26 × sin(πv)^1.4 where squash = 1 − h/196. Ripple r = 1 + min(|hv| / 5200, 0.035) × sin(5a − 17t) × sin(πv); the top face domes by clamp(hv × 0.035, −10, 14) × (1 − u²) above v 0.55. Bubbles go through the same map.
- Follow mouse: when ticked, goal = clientY ÷ innerHeight on every mousemove, and the drag is off.
- Keyboard on the slider: arrows ±0.1, Page Up/Down ±0.25, Home 0, End 1.

THINGS THAT BREAK
- Scrubbing pre-rendered frames needs hundreds of images; drawing the jelly live keeps it one file and lets the spring overshoot, which frames can't.
- Without the press as a hard ceiling the spring pushes the jelly through the slab on release.
- Clamp dt (50ms max) so a backgrounded tab doesn't come back to an exploded spring.
- A few wide edge strokes band visibly; use many faint ones.

THE FLOOR
- prefers-reduced-motion: no throw, no ripple or dome, a critically damped jelly that just follows the press, no fade-in. The canvas is aria-hidden; the slider carries the state. No horizontal scroll at 390px.
