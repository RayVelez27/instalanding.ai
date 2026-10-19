# Coverflow Carousel · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build an endless 3D cover-flow carousel as one HTML file: ten square album covers swing through a perspective stage, driven by the page's own scroll, with drag, keys, clicks and two step buttons. GSAP 3.7 with ScrollTrigger and Draggable from cdnjs; no other libraries and no image files.

THE STAGE
- Background hsl(0 0% 10%). A full-viewport .boxes layer with perspective 800px and transform-style preserve-3d, pinned by ScrollTrigger.
- Each .box is absolutely centred, 20vmin square with a 200px minimum, yPercent -50, display none until the timeline is built.
- Covers are generated in code: ten SVG data URIs at 300x300 (sunset rings, diagonal stripes, a dot field, sine waves, a triangle mosaic, a crescent night, Bauhaus shapes, blurred glow blobs, a tilted checkerboard, a sunburst), each with a small monospace label bottom-left. A seeded PRNG keeps the random ones identical on every load.
- Floor reflection: -webkit-box-reflect: below 0.5vmin with a transparent-to-white mask. Where box-reflect is unsupported, draw it with ::after (the cover flipped below) and ::before (a gradient from the background to transparent over it).
- Two round glossy step buttons under the stage (2px light border, a grey-to-black gradient that inverts while pressed, a play-triangle icon, the first rotated 180deg), lifted to z 200 so they sit in front of the covers. A small scroll hint icon nudges in the top-right corner.

ONE COVER'S LIFE (a 1s timeline)
- set: xPercent 250, rotateY -50, opacity 0, scale 0.5
- 0 → 0.1: opacity 1, scale 1 (and the reverse from 0.9 → 1)
- 0 → 1: xPercent 250 → -350, ease power1.inOut (the pan)
- 0 → 1: rotateY -50 → 50, ease power4.inOut (the swing, fast through the middle)
- 0.4 → 0.6: z 100 and scale 1.25, yoyo (the lift at the centre)
- 0 → 1: zIndex 1 → 10 and back, yoyo, ease none (whoever is centred is on top)
- Use immediateRender: false on the fromTo tweens that start later in the same timeline.

THE INFINITE LOOP
- Repeat the list three times and add each cover's timeline to one paused LOOP timeline at index × 0.1 (stagger 0.1, so a cycle is 1s for ten covers).
- Never play LOOP directly. LOOP_HEAD is a tween of LOOP's totalTime from cycle + 0.5 (the middle copy, with cover 0 centred) to += cycle, linear, repeat -1, paused.
- A PLAYHEAD object holds the position; a SCRUB tween (0.25s, power3) eases position toward its target and, on update, sets LOOP_HEAD.totalTime(wrap(position)).
- ScrollTrigger from 0 to +2000px, pinned. On update, the target is (iteration + progress) × LOOP_HEAD.duration(). Past the end, add one to iteration and jump the scroll to 1; scrolling up past the top, subtract one and jump to end - 1. The jumps are invisible because iteration carries the lap count.
- On scrollEnd, snap the position to the nearest 1/10 and scroll there, wrapping the lap if the snapped progress leaves 0..1.

INPUTS
- Arrow keys and A / D step one cover. The buttons step one cover. Clicking a cover finds the shortest signed distance from the centred cover (wrapping around) and scrolls there.
- Draggable on a hidden proxy with the covers as its trigger: on press remember the position, on drag move it by (startX - x) × 0.001, on release snap.

THINGS THAT BREAK
- Keep the page scrollable (hide the scrollbar, don't set overflow hidden), or wheel and trackpad never reach ScrollTrigger.
- Set the covers to display block only after the timelines exist, or they flash at the centre on load.
- zIndex must ride the timeline too: depth sorting alone does not order siblings inside a preserve-3d stage reliably.

THE FLOOR
- Buttons are real buttons with visually hidden labels; covers have alt text; under prefers-reduced-motion the scrub tween has zero duration so steps land instantly. Works at 390px wide (the cover minimum is 200px).
