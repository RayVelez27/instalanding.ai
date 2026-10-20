# Hello World Water · motion study

Webgl Simulation · three.js 0.180 · GLSL shaders · GPU wave sim · one HTML file

A real wave simulation on the GPU, seen from straight above a tiled pool. The water pulls itself up into the word HELLO, holds it while leaves are shouldered aside, then lets go: the letters fall back as travelling ripples and splashes before WORLD rises in their place. Caustics dance on the tiles, the sun drifts, leaves float and bob on the swell, and you can drag through the water, drop pebbles, double-click for a cannonball or bring on the rain.

![Hello World Water](preview.jpg)

**Open the lab:** [instalanding.ai/motion/hello-world-water](https://instalanding.ai/motion/hello-world-water) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one word's life (9.2s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| form · spring | 0 → 1, the water pulls up into the word | 0s → 2.76s | `power1.inOut` |
| spray | fine drops lift off the rising strokes | 0s → 2.76s | `power1.inOut` · yoyo |
| calm | ambient chop drops 72% around the word | 0s → 2.76s | `power1.out` |
| leaves | shouldered downhill off the strokes | 0.92s → 6.624s | `none` |
| form · release | 1 → 0 fast: the letters collapse | 6.624s → 7.176s | `power3.out` |
| splashes | 11 crowns burst along the strokes | 6.624s → 7.36s | `power2.in` |
| ripples | travel out and reflect off the walls | 6.624s → 9.2s | `power1.out` |

## Inputs

- DRAG: Wakes through the water; drag fast and it throws spray
- CLICK: Drops a pebble: a ring, a crown of droplets, leaves pushed away
- DOUBLE-CLICK: A cannonball: a deep cavity, then a central jet a moment later
- W: Rain on and off (N: next word · R: reset · SPACE: a pebble)

## How it works · Typography made of water

1. The surface is a 256×256 height field on the GPU: a fixed 120Hz step of the 2D wave equation, ping-ponged between two half-float render targets, with impulses (pebbles, wakes, raindrops, jets) added as gaussian bumps.
2. Each word is drawn to a canvas, stretched to the pool's 8×5.2 aspect, and blurred twice: a sharp mask for the letter height and a wide one for how strongly to pull. The simulation adds a spring toward mask × height × form.
3. form eases up over 2.8s, holds for 3.8s, then drops fast. With the spring gone the raised letters are just water, so they collapse on their own into ripples that travel and reflect: nothing is faked.
4. Rendering is a refraction ray-trace: refract the view through the surface normal into a tiled basin, light it with caustics (a second pass that compares each triangle's area before and after refraction), mix in a sky reflection by Fresnel, and brighten the raised letters so the word reads from above.

## Best for

launch and announcement moments, hero headlines that need a wow, wellness, travel and summer brands, developer and creative tools.

## Pairs with

- [Tide Reveal Agent Page](../../pages/tide-reveal-agent-page)
- [Wind Field Routing Page](../../pages/wind-field-routing-page)
- [Grain Motion System Page](../../pages/grain-motion-system-page)
- [Monax Analytics Landing Page](../../pages/monax-analytics-landing-page)
