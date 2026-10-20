# Kiln · design system

`kiln@1.0.0` · 14 components · 85 tokens · dark

Bead-blasted aluminium plates on a laminated copper edge, turned copper screws, recessed wells, engraved mono legends, amber and green lamps, analogue gauges and rocker switches that tip on a spring. Extracted from the Machine Front Panel landing page.

![Kiln design system](poster.jpg)

The full board, every component at once: [preview.jpg](preview.jpg)

**Explore it live:** [instalanding.ai/systems/kiln](https://instalanding.ai/systems/kiln) — every component rendered, a token playground and COPY FOR AGENT.

## Files

| File | What it is |
| --- | --- |
| [`specimen.html`](specimen.html) | Every component live in one file. Each is a `<section data-component>`; the markup inside `.sp-demo` is the component. Opens from disk. |
| [`tokens.css`](tokens.css) | The design tokens as CSS custom properties (`--kn-*`). |
| [`kiln.css`](kiln.css) | Tokens plus every component's CSS, scoped under `.kn` with `kn-` class names, so it can't restyle anything else on your page. |

## Use it

1. Load the fonts: `<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Archivo:wght@500;600;700;800;900&family=JetBrains+Mono:wght@400;500;700&display=swap">`
2. Link `kiln.css` and wrap the part of your page that uses the system in `<div class="kn">`.
3. Copy components from `specimen.html`. Interactive ones need the small script in its `<script id="kn-components-js">`, and any that draw SVG art need its `<svg id="kn-defs">`.
4. Change the look by editing the tokens, not the components.

## Components

- Buttons
- Type
- Top bar
- Status plate
- Rocker switches
- Gauge
- Heat window
- Readings strip
- Rating plate
- Compare switch
- Install log
- Rack picker
- FAQ
- Key slot

## Conventions

**Typography**

- Display: Archivo 900, uppercase, letter-spacing -0.035em to -0.04em, line-height 0.9-0.98 (--kn-display-*). Light it with one amber phrase (<em> in --kn-amber with a soft amber text-shadow).
- Legends are engraved, not printed: JetBrains Mono 500 at 9.5px, letter-spacing .34em, uppercase, --kn-engrave with a dark-above / light-below text-shadow (.kn-stencil). Eyebrows are 11px mono with .26em tracking.
- Values and readouts are JetBrains Mono (20-30px) in --kn-bright with a small mono unit in --kn-mute; body copy is Archivo 13.5-16px in --kn-mute, line-height 1.55-1.66.

**Layout**

- Content sits in .kn-wrap (min(1160px, 100% - 36px)); sections breathe with 92-150px of top padding and headers capped at about 50ch.
- Raised things are .kn-plate (anodised aluminium on the copper laminate edge, --kn-stack) with four .kn-screw corners; contained things sit in recessed .kn-well pockets; bays inside a plate use 14px padding and gaps.
- Grids are minmax(0, 1fr) columns that collapse to one column at 940px and 600px; long strips (readings, rack) re-flow rather than scroll.

**Materials**

- One material, done properly: brushed aluminium (gradient + fine machining lines + an overlay noise texture), lit top chamfer, dark lower edge, an engraved inner border. Never flat fills for raised surfaces.
- Copper is reserved for fasteners and edges (screws, rack ears, the laminate stack, the key and switch knob); amber is light (lamps, glows, focus), never a fill colour for big areas.
- Lamps are radial-gradient LEDs that also wash the metal around them (::after glow). Off lamps are --kn-led-off with an inset shadow. The rating plate is the one bright metal: sage aluminium with rivets.

**Motion**

- Motion is physical: switches, knobs and rack units move on --kn-spring (cubic-bezier(0.34, 1.7, 0.5, 1)); everything else eases on --kn-ease over --kn-dur-quick to --kn-dur-roll.
- Hover lights things rather than moving them: an amber 1px rim and an amber bloom (--kn-glow-amber). Counters roll, the gauge needle is damped, the heat window follows one --kn-heat value (0-1).
- Only small loops run on their own (the readings wave, the flip hint, a terminal caret); prefers-reduced-motion cuts every animation and transition inside .kn to near zero.

**Accessibility**

- Focus is a 2px --kn-amber outline offset 3-5px on every switch, button, rack unit and summary.
- Switches are real buttons with aria-pressed (rockers, rack units) or role=switch with aria-checked (the compare flipper); decorative lamps, grilles, screws and gauges are aria-hidden with the value repeated in text.
- Engraved legends are decorative; anything a reader needs is also in --kn-mute or brighter text. FAQ rows are native <details>.

## Extracted from

- [Machine Front Panel Page](../../pages/machine-front-panel-page) · [live](https://instalanding.ai/demos/kiln-panel.html)

Every system is extracted from a real, working page: the components are its markup, not a redraw.

MIT.
