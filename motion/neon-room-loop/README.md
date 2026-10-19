# Neon Room Loop · motion study

Infinite Loop · GSAP 3.12.5 · ScrollTrigger · one HTML file

Nine cards, each a different camera on one isometric neon room drawn in SVG, drift up and down in three columns that never end. The loop runs on its own; scrolling feeds the scroll velocity into it, so a flick sends the columns racing before they ease back to a cruise. Hover a card and it wakes from grey into full colour with a blue glow.

![Neon Room Loop](preview.jpg)

**Open the lab:** [instalanding.ai/motion/neon-room-loop](https://instalanding.ai/motion/neon-room-loop) — the study running live, slowed down and taken apart.

## Files

| File | What it is |
| --- | --- |
| [`index.html`](index.html) | The study: one file, opens from disk. |
| [`PROMPT.md`](PROMPT.md) | The one-shot prompt that builds it. |

## Choreography · one card's lap (20s)

| What moves | Change | When | Ease |
| --- | --- | --- | --- |
| y · columns 1 and 3 | 0 → −½ column, then wraps | 0s → 20s | `none` |
| y · column 2 | 0 → +½ column, the other way | 0s → 20s | `none` |
| offset · on scroll | velocity ÷ 2000, eases back to 0 | 6s → 6.5s | `power1.out` |
| filter · on hover | grey → full colour, glow | 12s → 12.6s | `power1.out` |

## Inputs

- SCROLL: Adds the scroll velocity to every card; harder flicks race further
- HOVER: Wakes a card from grey into colour with a neon edge
- IDLE: The columns keep drifting on their own, forever

## How it works · A loop that never resets

1. Each column's cards are appended twice, so the column is two identical halves. Every card tweens y by half the column height over 20s, linear, repeat -1: when the first half has scrolled away the second is exactly where it started.
2. A modifiers function wraps y with % (½ column height), so values never grow and the seam never shows. Columns 1 and 3 go up, column 2 goes down.
3. Inside the same modifier, a shared offset keeps adding additionalY: scroll velocity from ScrollTrigger (÷2000 down, ÷3000 up), tweened back to 0. The base tween never changes; the kick rides on top.
4. The cards are one SVG room rendered nine ways: boxes and planes in isometric space projected with (x − y)·0.866·s and (x + y)·0.5 − z, sorted by draw order, with a different scale and focus point per card (and one wireframe blueprint).

## Best for

portfolio and case-study walls, agency and studio hero sections, product screenshot galleries, event and gallery sites.

## Pairs with

- [Neon Glass App Landing Page](../../pages/neon-glass-app-landing-page)
- [Icon-Cut Card Stack Page](../../pages/icon-cut-card-stack-page)
- [Skewed Marquee Wall](../../pages/skewed-marquee-wall)

## Built on

- [Made by Beings](https://madebybeings.com) — The vertical image loop with scroll acceleration this study is built on, credited in the original
