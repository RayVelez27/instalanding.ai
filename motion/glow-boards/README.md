# Glow Boards · motion study

Hover Stack · Canvas 2D decoded .riv · no runtime · state machine · one HTML file

Sixteen thin boards stand in a diagonal line over a pink-to-cyan glow. Hover one and it rises out of the stack on a soft overshoot, its frosted face catching the light; move on and it eases back into place. Run the pointer along the line and the boards ripple up one after another. A Rive state machine, decoded and redrawn with plain Canvas 2D: no runtime, no images.

![Glow Boards](preview.jpg)

**Open the lab:** [instalanding.ai/motion/glow-boards](https://instalanding.ai/motion/glow-boards) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one board's lift and settle (1s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| hover input | false → true as the pointer enters | 0s → 0.02s | `none` |
| y · lift | rises 26–81 units out of the stack | 0s → 0.53s | `power1.inOut` |
| y · settle | falls back on leave, slightly slower to start | 0.53s → 1s | `power1.inOut` |

## Inputs

- HOVER: Lifts the board under the pointer; leaving lets it settle
- SWEEP: Run the pointer along the stack and the boards ripple up in turn
- TAP: On touch, lifts the board you tap

## How it works · A Rive file without the Rive runtime

1. The .riv was decoded into plain data: the component tree (nodes, shapes, rectangles, fills, feathers), the 34 timeline animations and the state machine (17 layers, one per board, each switching between a hover and an unhover animation on a boolean input).
2. Every frame, each layer advances its current animation and writes the keyed property (the board's y) back into the tree; world matrices are recomposed parent to child and the shapes are painted back to front.
3. The glow is Rive's feather: a Gaussian-blurred rectangle. It is precomputed once per size as a sprite, a separable erf profile in x times one in y, and stretched into place, so a soft edge costs one drawImage.
4. Hover is hit-testing through the inverse world matrix: the pointer is mapped into each board's local space and checked against its rectangle, and enter or leave fires the listener that flips that board's input.

## Best for

AI and data product heroes, layered-stack or pipeline metaphors, dark launch pages, interactive section dividers.

## Pairs with

- [Neon Glass App Landing Page](../../pages/neon-glass-app-landing-page)
- [Icon-Cut Card Stack Page](../../pages/icon-cut-card-stack-page)
- [Holographic Ticket Landing Page](../../pages/holographic-ticket-landing-page)
- [Recessed Aperture Hero Page](../../pages/recessed-aperture-hero-page)
