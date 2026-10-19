# Coverflow Carousel · motion study

Carousel · GSAP 3.7.0 · ScrollTrigger · Draggable · one HTML file

Ten album covers swing through a perspective stage on one GSAP timeline. Scroll, drag, the arrow keys or a click scrub a playhead across it; the loop never ends because the scroll quietly wraps, and every stop snaps a cover to the centre with a floor reflection under it.

![Coverflow Carousel](preview.jpg)

**Open the lab:** [instalanding.ai/motion/coverflow-carousel](https://instalanding.ai/motion/coverflow-carousel) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one cover's life (1s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| opacity · scale | fade in, 0.5 → 1 | 0s → 0.1s | `none` |
| xPercent | 250 → −350 across the stage | 0s → 1s | `power1.inOut` |
| rotateY | −50° → 50°, the swing | 0s → 1s | `power4.inOut` |
| z · scale | lift 100px, 1.25× at centre | 0.4s → 0.6s | `none` · yoyo |
| zIndex | rises to the top, falls back | 0s → 1s | `none` · yoyo |
| opacity · scale | fade out, 1 → 0.5 | 0.9s → 1s | `none` |

## Inputs

- SCROLL: Scrubs the playhead; the page scroll is the timeline
- DRAG: Grab a cover and throw it sideways
- ← / →: One cover back or forward (A and D too)
- CLICK: Any cover takes the shortest way to the centre
- ◀ / ▶: The glossy step buttons under the stage

## How it works · Infinite without infinite scroll

1. Build the strip three times over and lay every cover's 1s life on one paused timeline, 0.1s apart.
2. Play only the middle copy: a second tween scrubs the timeline's totalTime across one cycle, so both ends always have covers.
3. Map 2000px of page scroll onto that cycle with ScrollTrigger (pinned). At the bottom, jump the scroll to the top and count one more lap; at the top, the reverse. The jump is invisible because the playhead keeps adding laps.
4. Ease toward the target with a 0.25s scrub tween instead of setting it, and snap to the nearest 1/10 on scrollEnd, so every stop lands a cover dead centre.

## Best for

music and media libraries, portfolio and case-study rails, product galleries, event line-ups.

## Pairs with

- [Starfork Game Studio Landing Page](../../pages/starfork-game-studio-landing-page)
- [Maasai-Inspired Event Landing Page](../../pages/maasai-inspired-event-landing-page)
- [Holographic Ticket Landing Page](../../pages/holographic-ticket-landing-page)
- [LED Metro Tech Storefront](../../pages/led-metro-tech-storefront)

## Built on

- [Jhey Tompkins (jh3y) on CodePen](https://codepen.io/jh3y) — The infinite scroll-driven album carousel this study is built on; the covers here are drawn in code
