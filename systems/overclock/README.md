# Overclock · design system

`overclock@1.0.0` · 14 components · 69 tokens · light

Pure ink on paper: hand-drawn panel outlines from an SVG wobble filter, halftone screentone and speed hatching, Bangers lettering stroked and tilted over Anton numerals and Barlow Condensed body, hard offset shadows, speech bubbles, and an animated sliced retro sun over a seeded city skyline. Extracted from the Manga Panel Dev Tool landing page.

![Overclock design system](poster.jpg)

The full board, every component at once: [preview.jpg](preview.jpg)

**Explore it live:** [instalanding.ai/systems/overclock](https://instalanding.ai/systems/overclock) — every component rendered, a token playground and COPY FOR AGENT.

## Files

| File | What it is |
| --- | --- |
| [`specimen.html`](specimen.html) | Every component live in one file. Each is a `<section data-component>`; the markup inside `.sp-demo` is the component. Opens from disk. |
| [`tokens.css`](tokens.css) | The design tokens as CSS custom properties (`--oc-*`). |
| [`overclock.css`](overclock.css) | Tokens plus every component's CSS, scoped under `.oc` with `oc-` class names, so it can't restyle anything else on your page. |

## Use it

1. Load the fonts: `<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Anton&family=Bangers&family=Barlow+Condensed:ital,wght@0,400;0,600;0,700;1,600&family=JetBrains+Mono:wght@400;700&display=swap">`
2. Link `overclock.css` and wrap the part of your page that uses the system in `<div class="oc">`.
3. Copy components from `specimen.html`. Interactive ones need the small script in its `<script id="oc-components-js">`, and any that draw SVG art need its `<svg id="oc-defs">`.
4. Change the look by editing the tokens, not the components.

## Components

- Navigation
- Buttons
- Cover
- Terminal panel
- Retro sun & skyline
- Stats strip
- Panel break
- Section title
- Feature panels
- Story steps
- Pricing
- Reader mail
- Final chapter
- Footer

## Conventions

**Typography**

- Lettering is Bangers (--oc-font-display), always uppercase: headlines in --oc-display-xl/-lg at line-height .86, white fill with a thick ink -webkit-text-stroke and a -2deg tilt; section heads --oc-display-md; buttons --oc-button with 2px tracking.
- Numerals and prices are Anton (--oc-font-numeral) at --oc-numeral-*; body is Barlow Condensed (--oc-font-body) at --oc-body/1.55; commands and terminals are JetBrains Mono (--oc-font-mono) at --oc-code.
- Labels (.oc-issue, .oc-role, stat captions) are tiny tracked uppercase on an inverted ink block. Katakana sound effects (.oc-jp, ゴゴゴ) are decoration and stay aria-hidden.

**Layout**

- Content sits in panels on a --oc-page-max (1120px) page with a --oc-gutter edge and --oc-gap between panels, like a comic page; sections open with .oc-section-title or an .oc-break strip.
- Grids collapse at 900px (stats 4 → 2, steps, pricing and FAQ to one column, the closing panel stacks) and 640px (nav links hide, headline drops to 50px).
- The featured panel (.oc-plan-hot) inverts to ink and tilts 1deg; small tags (.oc-hot-tag, .oc-num, .oc-bubble) tilt between -6deg and 4deg.

**Panels & ink**

- Black and white only: --oc-ink on --oc-paper/--oc-white, with greys (--oc-grey, --oc-mid) for shadows and screentone. The night panels use the --oc-night-* inks.
- Panel outlines are drawn by an :after overlay through url(#oc-sketchy); small labels use #oc-sketchy-sm. Both need the shared <svg id="oc-defs">.
- Shadows are hard and unblurred: --oc-shadow-btn / --oc-shadow-ink on buttons, --oc-shadow-panel (white then ink) on the terminal, --oc-shadow-frame on the page. Texture is screentone (--oc-tone-dot on --oc-tone-pitch) or 45deg hatching (--oc-hatch-pitch), never a gradient.

**Motion**

- Buttons lift 2px on hover and press flat on --oc-dur-press; the FAQ ring spins and fills over --oc-dur-open on --oc-ease-pop.
- Cover copy rises in on --oc-dur-rise with 80ms staggers; the sun's gaps slide down it and its rings pulse (--oc-dur-sunrise); the grid floor scrolls on --oc-dur-floor; skyline windows and the terminal cursor blink.
- The sun and skyline are built by the component script from data-oc-sun / data-oc-skyline settings. Under prefers-reduced-motion the sun is drawn as static slices and animations stop.

**Accessibility**

- Scene art (sun, skyline, sound effects, the terminal's static frame) is aria-hidden; meaning lives in the text beside it.
- FAQ uses native details/summary; the signup is a real form with a labelled email field, and its result is written as text (✓ / ✗) into .oc-signup-msg, not shown by colour alone.
- Ink on paper is above 17:1; keep stroked lettering for display sizes only and set body copy as plain ink.

## Extracted from

- [Manga Panel Dev Tool Page](../../pages/manga-panel-dev-tool-page) · [live](https://instalanding.ai/demos/overclock-deploy.html)

Every system is extracted from a real, working page: the components are its markup, not a redraw.

MIT.
