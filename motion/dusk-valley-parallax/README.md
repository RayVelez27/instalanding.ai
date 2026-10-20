# Dusk Valley Parallax · motion study

Scroll Parallax · GSAP 3.12.5 · ScrollTrigger · one HTML file

A single SVG landscape, thirty-odd layers deep, scrubbed by the page's scroll. Scroll down and the valley's ridges slide apart at their own depths while the sun sinks behind a dusk range rising from below. The sun swells until it fills the sky, a flock of bats bursts out of it, and then the whole dusk lifts away to reveal a night valley under twinkling stars, with a shooting star crossing it. Scroll back up and every frame plays in reverse.

![Dusk Valley Parallax](preview.jpg)

**Open the lab:** [instalanding.ai/motion/dusk-valley-parallax](https://instalanding.ai/motion/dusk-valley-parallax) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one scroll, 6000px (1s = 1000px) (6s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| x · clouds | four clouds drift apart, ±500–1000 | 0s → 4.2s | `none` |
| y · x · ridges, scene 1 | nine ridges fall away, nearest fastest | 0s → 2.4s | `power2.in` |
| cy · sun gradient | −50 → 330, the sun sinks | 0.06s → 2.16s | `none` |
| y · ridges, scene 2 | dusk range rises 500–900 → 0 | 0.9s → 2.4s | `power1.inOut` |
| offset · sun stops | the sun swells to fill the sky | 1.98s → 4.98s | `none` |
| y · scale · bats | burst out of the sun, 0 → 0.8 | 2.4s → 4.2s | `power3.out` |
| y · scale · dusk | lifts up and away, 1.5× | 3.6s → 6s | `power1.inOut` |
| y · ridges, scene 3 | night valley climbs in, stars appear | 4.2s → 6s | `power1.inOut` |
| x · y · falling star | crosses the night sky | 4.2s → 6s | `power1.out` |

## Inputs

- SCROLL: The only clock: every layer is scrubbed by the page's scroll, both ways
- ◀ / ▶: Glide to the previous or next scene: sunset, dusk, nightfall, starlight
- IDLE: The scroll arrows bob and the stars twinkle on their own

## How it works · A film strip on a scroll bar

1. Everything is one fixed, full-viewport SVG (viewBox 750×500, preserveAspectRatio xMidYMax slice), and a 6000px empty div behind it gives the page its length. The SVG never scrolls; the scroll only feeds the timelines.
2. Each scene is its own timeline bound to a slice of that length with ScrollTrigger and scrub 2–3, so layers ease toward the scroll position instead of snapping to it. That lag is what reads as depth.
3. Depth is a different multiple per layer: one speed unit, and the nearest ridge moves 3–5× while the far ones move 1–2×, some sideways in opposite directions, so the valley opens up rather than sliding.
4. The sun is not a shape: it is the first stops of the sky's radial gradient. Tweening the gradient's cy sinks it, and tweening the stop offsets and colours swells it, all as attr tweens on the SVG.
5. Scene 3 waits below the frame (y = SVG height − 40) and the dusk lifts out of view as it arrives, so the cut between scenes is a camera move, not a fade.

## Best for

storytelling and launch pages, outdoor, travel and festival brands, portfolio intros, games and story worlds.

## Pairs with

- [Sunset Scroll Story Page](../../pages/sunset-scroll-story-page)
- [Paper Sun Agent Page](../../pages/paper-sun-agent-page)
- [Maasai-Inspired Event Landing Page](../../pages/maasai-inspired-event-landing-page)
- [Event Horizon Orbital Page](../../pages/event-horizon-orbital-page)

## Built on

- [isladjan on CodePen](https://codepen.io/isladjan) — The scroll-driven SVG parallax this study is built on; the shooting star is redrawn inline here
