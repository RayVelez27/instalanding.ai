# Redline Gauge · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a tap-to-rev neon speedometer as one HTML file: a glowing gauge in a dark glass card, wrapped in violet smoke, whose needle climbs three levels to the redline when you tap in rhythm. Near-black page (#060a12), one full-viewport canvas, Canvas 2D, no libraries.

THE STAGE
- A 1855 × 1044 artboard, contained and centred. On tall screens (width / height under 1.25) fit the card itself instead, so the gauge fills a phone's width.
- A dark navy glass card with rounded corners and a soft drop shadow, the gauge centred in it.

THE GAUGE (drawn in code)
- An outer bezel ring with a cool blue rim light along its top edge, a thin tick scale around the inside, and a dark inner face.
- A sweep of fine radial pink lines (#ff2fd0 to #ff7bf0) filling the upper arc, lit by a radial gradient whose end point you move to follow the needle.
- A thin glowing pink needle from a small ringed hub, and a short cyan arc near the bottom.
- Three layers of soft violet smoke around the gauge: one always drifting and slowly turning (a full turn in about 200 seconds), two that only appear for the burst.

THE STATE MACHINE (inputs: hover bool, click trigger, level number 0-3)
- Levels are single poses. Needle rotation: level 0 -150°, level 1 -55°, level 2 0°, level 3 +50°. Each level also moves the sweep gradient's end point.
- Transitions: 0 → 1 when level = 1, 1 → 2 when level = 2, 2 → 3 when level = 3, each a 500 ms blend on cubic-bezier(0, 0, 0.13, 1). If the next level doesn't arrive, each state falls back to idle.
- At level 3: hold 500 ms, then play the smoke burst (the two extra smoke layers fade in and roll out over about 4 s) while the needle blends back to idle over 2 s.
- A loop under everything: the needle wiggles a few degrees, ping-pong, about once a second.
- Hover: the rim brightens over 100 ms and fades back on leave. Every tap flashes a white ring over the dial for about 100 ms.

THE INPUT
- Four full-dial hit rings, one per level, stacked. Each level pose sets only the next level's ring to scale 1 and the rest to 0, so a tap always hits exactly one ring, and its listener sets level to the next number and fires click.
- A tap that arrives during a 500 ms blend is ignored, so the right rhythm is about four taps a second.

THINGS THAT BREAK
- Hit-test through the inverse of the view transform, the same one you draw with, or taps miss on phones.
- Sample cubic eases by solving t from x, not by using progress as t.
- Cap dt at 0.1 s so a background tab doesn't fire every transition at once.

THE FLOOR
The canvas has role="img" and an aria-label describing the gauge; touch-action none so taps don't scroll. Works at 390px wide.
