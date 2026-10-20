# Dusk Valley Parallax · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a scroll-driven SVG parallax landscape as one HTML file: a valley at sunset that, over one long scroll, sinks into dusk and lifts away into a starry night. GSAP 3.12 and ScrollTrigger from cdnjs; no other libraries and no image files.

THE STAGE
- body background #1d1d3a, scrollbar hidden but the page really scrolls. One svg.parallax, position fixed, 100% × 100vh, viewBox 0 0 750 500, preserveAspectRatio "xMidYMax slice", z-index 3. Behind it an empty .scrollElement, position absolute, 6000px tall: it is the timeline's length.
- The sky is a rect filled with a radial gradient centred at (375, −30), r ≈ 319: the first stop (#F5C54E, id sun) is the sun's disc, then #FFDBA6, #F7BB93, #F2995E, #f07560 and #FFAB93 out to the edge.
- Flat-shaded layers drawn as paths, each with its own linear gradient. Scene 1: nine pine ridges from pink-mauve (#d98981) in the distance to near-black navy (#120e22) in front, two big soft white cloud banks at 0.5 opacity and four thin white clouds. Scene 2: six rolling dusk ridges and a flock of five bats (hidden). Scene 3: a purple night sky (radial, pink at the horizon to navy), seventy small stars, a shooting star (a tapered white gradient tail with a bright head), four jagged night ridges with mix-blend multiply and two faint dinosaur skeletons in the foreground. Plus a bird silhouette and two chevron scroll arrows.

THE CHOREOGRAPHY (all scrubbed by scroll)
- Scene 1, top to 45% of the length, scrub 3: with speed = 100, ridges move y 1.7–5 × speed and x −2.5 to +1.6 × speed (the nearest most), the big cloud banks y 4.5 × speed, the opening clouds part ±300, the arrow drops away.
- Clouds, to 70%, scrub 1: cloud1 x +500, cloud2 +1000, cloud3 −1000, cloud4 −700.
- Sun, to 2150px, scrub 2: the gradient's cy −50 → 330 and the stops spread (0.15, 0.18, 0.25, 0.46): it sinks and softens.
- Scene 2, 15% → 40%, scrub 3: its ridges rise from y 500–900 to 0, a little staggered. The bird crosses the sky (x +800, y −250) and flips round when its trigger ends.
- Sun swells, 2000px → 5000px: the sun stop's offset → 1.4 and it turns #ffff00, so the disc fills the sky; the dusk ridges darken (#623951 → #261F36).
- Bats, 40% → 70%: from y 400, scale 0 to y 20, scale 0.8, power3.out; on enter each bat flaps (scaleX 0.5 yoyo, 9 repeats, staggered 0.1s).
- Transition, 60% → bottom: scene 3 starts at y = the SVG's height − 40; the dusk ridge lifts to y −(height + 100) at scale 1.5 and the night sky rises to 0.
- Scene 3, 70% → bottom: the night ridges climb from y 300–1000 to −550, staggered 0.03; stars fade to 0.5 and rise; the sky gradient's cy → 600 and r → 500; the up arrow fades in. The shooting star crosses from 4200px (x −700, y −250).

THINGS THAT BREAK
- Animate SVG gradients with attr tweens (cy, r, offset, stop-color): CSS transforms can't reach them.
- Give every scene its own ScrollTrigger range and keep scrub at 2–3; scrub true (no lag) flattens the depth.
- Set transformOrigin before scaling the bats, or they scale from the SVG's corner.
- Start from the top on reload (history.scrollRestoration = "manual"), or a mid-scroll restore lands between scenes with tweens half-set.

THE FLOOR
- prefers-reduced-motion stops the bobbing arrows and the twinkle; the scroll still drives the scenes, so nothing moves unless the reader moves it. The SVG slices to cover any aspect ratio; at 490px and below the arrows scale to 0.8 and lift. No horizontal scroll at 390px.
