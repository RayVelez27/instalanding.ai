# Only the Wind · motion study

Ambient Scene · Canvas 2D + SVG · no libraries · SMIL · CSS keyframes · one HTML file

Two travellers watch the sun set over a lake while cherry petals blow past in three layers of depth: hazy specks far off, crisp petals that catch the light as they tumble, and huge out-of-focus ones sweeping past the lens. Grass sways, a lantern and a wind chime swing under the eaves, dust glitters in the sun and a haiku inks itself in. Click and a gust tears through the whole scene, then dies away. Everything is drawn in code: canvas, SVG and CSS, no images.

![Only the Wind](preview.jpg)

**Open the lab:** [instalanding.ai/motion/only-the-wind](https://instalanding.ai/motion/only-the-wind) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one petal's crossing (10s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| x · petal | drifts right to left, eases to its wind speed | 0s → 10s | `power1.out` |
| y · petal | gravity plus a sine wave of turbulence | 0s → 10s | `power1.inOut` · yoyo |
| rotateX · Y · Z | tumbles in 3D, lit when it faces the sun | 0s → 10s | `none` |
| gust | +2.2 on a click, then ×0.972 a frame | 3s → 6.2s | `power3.out` |
| sway · grass | two sines per blade, bent by the gust | 0s → 10s | `power1.inOut` · yoyo |
| rotate · lantern · chime | −3° to 3.6°, 5s and 3.1s | 0s → 5s | `power1.inOut` · yoyo |
| scale · camera | breathes 1.035 → 1.042 over 16s | 0s → 10s | `power1.inOut` · yoyo |
| opacity · blur · haiku | inks in one character at a time | 1.5s → 4.5s | `power1.out` |

## Inputs

- CLICK: Summons a gust: petals race, grass bends flat, dust streams, then it all settles
- SPACE: The same gust from the keyboard
- MOVE: The pointer parallaxes the sky, the figures and the grass at different depths

## How it works · Depth from three fields and a fake lens

1. One petal model, three fields: far (130 small petals with a haze tint and one blur pass), mid (46 crisp ones) and near (9 huge ones drawn from a 4-pass blurred sprite with motion trails). Size, wind and blur together read as depth of field.
2. Each petal is a sprite drawn once, then projected with an affine setTransform from two rotated axis vectors: a full 3D tumble for the price of one drawImage. The face angle sets how much light comes through, and so does the distance to the sun.
3. Every petal eases toward its own wind speed (smaller ones catch more wind) and falls under gravity plus a sine of its x position. A gust adds to every field at once and decays by ×0.972 a frame, so one click is a whole weather event.
4. The photograph is procedural: ridgelines from midpoint displacement with aerial perspective, a sun path on the lake, fBm clouds, rays, mist and grain. Over the top, a lens flare (bloom, core, streak, spikes, ghosts mirrored through the centre) follows the sun as the scene parallaxes.

## Best for

storytelling and brand moments, travel, hospitality and tea brands, poetry, books and editorial, calm hero sections and 404 pages.

## Pairs with

- [Sunset Scroll Story Page](../../pages/sunset-scroll-story-page)
- [Paper Sun Agent Page](../../pages/paper-sun-agent-page)
- [CRAFT Studio WebGL Landing Page](../../pages/craft-studio-webgl-landing-page)
- [Generative Editorial Product Page](../../pages/generative-editorial-product-page)
