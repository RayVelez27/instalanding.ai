# Conveyor Gallery · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a portfolio gallery where the project covers ride a looping 3D conveyor belt, as one HTML file, one screen with no scrollbar. Plain WebGL 1, no libraries. Google Fonts: Inter (400-900), Instrument Serif (with italic) and JetBrains Mono (400/700). No image files: every cover is painted with Canvas 2D at load.

THE STAGE
- Black page, html and body 100% with overflow hidden. A stage laid out at 1080px tall and scaled to the window height, holding: a breathing volumetric light from above (stacked radial gradients, blurred 18px, a faint conic ray mask, a 10s scale and opacity loop), a soft dark gradient at the bottom, and a full-screen WebGL grain canvas (four hashed randoms averaged, redrawn every 80ms, soft-light at 0.22). The stage fades in over 1.6s.
- #app is fixed over everything with touch-action none: the conveyor canvas (a drop shadow 20px 32px 28px) and a list of real links, one per project, visually hidden but focusable (the focused one shows as a pill at the bottom).

THE COVERS (1200 × 900 each, painted once the fonts load, 2.5s cap)
Eight fictional sites, each a full hero composition: Monarch (private wealth, a bezier monarch butterfly with veins and spots on dark amber, "Wings of quiet wealth." in Instrument Serif), Spektral (a ring of light refracting a beam into a spectrum, a conic gradient glow, channel bars), Owari (ceramics on paper with speckle, a striped red sun, vertical Japanese type, huge OWARI), Trading Dashboard (candlesticks from a seeded walk, a moving average, volume, an order book with depth bars, Buy and Sell), Crypto Exchange ("Trade what comes next.", a sparkline card, four coin cards), Chartroom (a light social feed for traders: profile, trending tickers, two posts with charts, a top traders list), Apex (a grappling tour: GRAND and outlined SLAM, a bracket, a tilted yellow marquee band, three event cards) and Developer Community (a code editor with syntax colours, a terminal, three post cards, stats and stacked avatars). Use a seeded random so they paint the same every time. Each cover is also the image of its link.

THE BELT
- A stadium loop: two straights of length 5.8 at z = ±1.02 joined by half circles of radius 1.02 (y from −2.9 to 2.9). Build a ribbon of 257 vertex pairs along it, width (11.6 + 2π·1.02) / 8 × 4/3 so a cover keeps 4:3; each vertex has x, y, z, uv (side, distance round the loop) and its normal in y-z.
- Pack the covers into one atlas (columns ceil(√(8 × 0.75))), with an anisotropic filter when available.
- Fragment shader: phase = mod(uv.y × 8 + offset, 8); the floor is the cover, the fraction the row; sample the atlas with a half-texel inset. Flip the normal for the back face. Light: a fixed direction (−0.45, 1.1, 0.8), ambient 0.36 on the front and 0.14 on the back (darker round the folds), diffuse, a faint specular. Soft self-shadow: from each pixel cast five rays towards the light (one plus four jittered) against the two straight planes and the two half cylinders analytically, fading by distance from the ribbon's edges.
- Vertex shader: rotate the belt (x 0.07, y −0.594 plus a sway of 0.081 × sin(offset × 2π / 8), z −0.28), then a rig rotation from the pointer, then a look-at camera with a fixed projection and the view shifted up by 0.2.

THE MOTION (state: offset, velocity, present, targetPresent, pointer, parallax)
- Every frame, n = elapsed / (1000 / 60) capped at 3: decay = 0.94ⁿ; offset += velocity × 0.94 × (1 − decay) / 0.06 (wrapped 0-8); velocity ×= decay; present eases to targetPresent by 1 − 0.93ⁿ; parallax eases to the pointer by 1 − 0.968ⁿ.
- The wheel adds deltaY × 0.00019 to the velocity and deltaY × 0.00033 to targetPresent (clamped 0-1); a touch drag uses 0.00155 and 0.0024. An arrow key adds exactly 0.06 / 0.94 (one cover) and ±0.12 to targetPresent.
- The camera: e = smoothstep(present). Position (−2, −9.35, 10.99 − 4.79e) scaled by (1 − e) on x and y, zoomed out on tall screens by max(1, 0.9 × height / width); the belt's rotations and the parallax are multiplied by (1 − e), so at e = 1 the belt faces you flat.
- Picking: draw the mesh with each cover's index + 1 in the red channel, read the pixel under the pointer, then redraw. When the belt is nearly still, a cover under the pointer shows a pointer cursor; a click (not a drag) opens its link.
- Optional autoplay for previews: advance one cover every 2s and swing the camera to face-on and back every two covers.

THINGS THAT BREAK
- Never make the page scroll to drive this: the wheel and touch move the state directly, and the page has no scrollbar.
- Make the momentum frame-rate independent with the closed form above, or a 120Hz screen glides twice as far.
- Paint the covers only after the fonts load, or the atlas is set in fallback type.
- Handle webglcontextlost on both canvases (fall back to a grid of the cover links, and a generated noise texture for the grain) and webglcontextrestored.
- Cap the device pixel ratio at 2 and the atlas at the GPU's MAX_TEXTURE_SIZE (4096 at most).

THE FLOOR
One visually hidden h1; the canvas is aria-hidden and every cover is a real link with an aria-label, so keyboard and screen reader users get the gallery. prefers-reduced-motion drops momentum (the wheel moves the belt directly, the arrows snap one cover) and stops the light, grain and fade. Without WebGL it is a responsive grid of the same covers. Works at 390px wide (the camera pulls back on tall screens).
