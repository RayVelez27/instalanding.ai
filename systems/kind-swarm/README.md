# Kind Swarm · design system

`kind-swarm@1.0.0` · 14 components · 89 tokens · light

Flame and lime bands of concentric op-art rings, Stardos Stencil set huge, 3px ink outlines with hard offset shadows that press flat on click, cream cards and glossy animoji characters whose eyes follow the pointer. Extracted from the Social Work Agent Swarm landing page.

![Kind Swarm design system](poster.jpg)

The full board, every component at once: [preview.jpg](preview.jpg)

**Explore it live:** [instalanding.ai/systems/kind-swarm](https://instalanding.ai/systems/kind-swarm) — every component rendered, a token playground and COPY FOR AGENT.

## Files

| File | What it is |
| --- | --- |
| [`specimen.html`](specimen.html) | Every component live in one file. Each is a `<section data-component>`; the markup inside `.sp-demo` is the component. Opens from disk. |
| [`tokens.css`](tokens.css) | The design tokens as CSS custom properties (`--ks-*`). |
| [`kind-swarm.css`](kind-swarm.css) | Tokens plus every component's CSS, scoped under `.ks` with `ks-` class names, so it can't restyle anything else on your page. |

## Use it

1. Load the fonts: `<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Stardos+Stencil:wght@400;700&family=IBM+Plex+Sans+Condensed:ital,wght@0,400;0,500;0,600;0,700;1,400;1,500&family=IBM+Plex+Mono:wght@500;600&display=swap">`
2. Link `kind-swarm.css` and wrap the part of your page that uses the system in `<div class="ks">`.
3. Copy components from `specimen.html`. Interactive ones need the small script in its `<script id="ks-components-js">`, and any that draw SVG art need its `<svg id="ks-defs">`.
4. Change the look by editing the tokens, not the components.

## Components

- Buttons
- Type
- Ring patterns
- Animoji characters
- Navigation
- Stats strip
- Marquee
- Filter pills
- Agent card
- Numbered step
- Approval queue
- Chips
- Rule cards
- Pricing plans

## Conventions

**Typography**

- Display: Stardos Stencil 700, uppercase, line-height .92 (--ks-leading-display), set very large (--ks-display-*). Pair a display line with an italic IBM Plex Sans Condensed second line (.ks-serif) at about .72em.
- Labels: IBM Plex Mono 500, 13px, uppercase, letter-spacing .16em (.ks-label), e.g. "02 — The crew".
- Body: IBM Plex Sans Condensed 400-700 at 17-20px, line-height 1.55; soft text uses --ks-text-soft on paper and --ks-on-ink-soft on ink.

**Layout**

- Full-bleed bands alternate flame rings, paper, lime rings and ink; separate them with 3px ink rules. Content sits in .ks-wrap (max 1440px, gutter clamp(16px, 4vw, 56px)) with section padding --ks-section-y.
- Grids use repeat(auto-fit, minmax(min(100%, 320px), 1fr)) with 36-56px gaps, so they collapse to one column on phones without breakpoints.
- Outline everything in ink (--ks-border 3px) and give raised things a hard offset shadow (--ks-shadow): never a blurred shadow.

**Patterns**

- Ring backgrounds: add .ks-rings plus a colour class (.ks-hero-rings, .ks-mq-rings, .ks-ink-rings, .ks-st1 to .ks-st8). The pattern reads --c1, --c2 and --s, so any band can be re-coloured with those three properties.
- .ks-wave-text clips the ring pattern into stencil type and drifts it slowly.
- Characters are inline SVG using the shared gradients in <svg id="ks-defs">; wrap one in <button class="ks-poke" data-ks-poke aria-label="..."> to make it pokeable.

**Motion**

- Buttons lift 2px and grow their shadow on hover, and press flat (translate by the shadow offset, shadow 0) on :active, in --ks-dur-press with --ks-ease-press.
- Characters bob (--ks-dur-bob), blink (--ks-dur-blink) and squash on a poke (--ks-dur-poke, --ks-ease-spring); stagger them with .ks-d1 to .ks-d4.
- Sections rise in with .ks-rise; the marquee loops over --ks-dur-marquee and pauses on hover.

**Accessibility**

- Focus is a 3px --ks-focus outline offset 4px on every link and button.
- Decorative SVG and the marquee are aria-hidden; pokeable characters are real buttons with a label; filter pills are buttons with aria-pressed.
- prefers-reduced-motion stops every animation and transition inside .ks.

## Extracted from

- [Social Work Agent Swarm Landing Page](../../pages/social-work-agent-swarm-landing-page) · [live](https://instalanding.ai/demos/kindswarm-casework.html)

Every system is extracted from a real, working page: the components are its markup, not a redraw.

MIT.
