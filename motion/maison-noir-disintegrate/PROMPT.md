# Maison Noir Disintegrate · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a luxury members' card that disintegrates into dust and reassembles on a loop, as one HTML file, one screen with no scrollbar. GSAP 3.12.5 and html2canvas 1.4.1, from cdnjs. Google Fonts: Cormorant Garamond (500/600, italics), Inter (400-600), JetBrains Mono 500. No image files: every part of the card is drawn with Canvas 2D at load.

THE STAGE
- Page #07070a, exactly one screen (100vh, overflow hidden, touch-action none): nothing scrolls; ink #f3ece0, gold #d9b876. A fixed ambient layer: a faint gold radial glow in the middle and a warm brown glow rising from below. A fixed soft contact shadow under the card (not part of the capture) and a SCROLL OR DRAG cue at the bottom whose 1px gold bar drips (scaleY 0 → 1, then fades, 2s loop). A PREPARING veil covers everything until the card is ready, then fades over 900ms.

THE CARD (#capture: fixed, centred, 600 × 400, radius 26, #0e0e11, overflow hidden)
- Layers: a background image, a diagonal glare band (warm white at 0.13 peak), a gold hairline bevel with a dark inner bevel and a bright top edge highlight.
- Content, absolutely placed: top left a faceted gold diamond mark and MAISON NOIR in foil caps (Cormorant 600, 27px, 5.5px tracking) over "PRIVATE RESERVE · EST. MMXXVI"; top right EDITION / "Nº 0001 / 1000" in foil italics; an EMV chip and an embossed contactless symbol; a hologram top right; the number "4729 1180 5562 0918" in silver JetBrains Mono 25px with a tiny "4729" under it; MEMBER A. VALENTINE, SINCE 2026, VALID THRU 10/31 in silver Inter 12px; bottom right OBSIDIAN in foil caps and a gold seal.
- Draw each asset on a canvas at 3× and place it as an <img>:
  - foil text: per-character fillText with manual spacing; an emboss pass (a black shadow offset down, a faint light copy 0.55px up), a vertical gold or silver gradient fill (gold #fff4d1 → #ecc985 → #b88d47 → #86622a → #e4c283 → #9c773a), then, with source-atop, brushed lines (one random black or white row per pixel at up to 0.14 alpha) and a diagonal sheen.
  - background (2×): a dark diagonal gradient, a warm bloom top left, brushed rows, a huge faint italic N watermark, three guilloché rosettes on the right (polar curves r = R + a·sin(f·t + k·0.42) + 0.35a·cos(f/2·t), many copies), 26 wavy engraved bands along the bottom, three lines of 3px microprint, a vignette and per-pixel grain.
  - chip: a gold gradient rounded rect with brushed rows, grooved contact lines drawn twice (dark, then light offset 0.6px) and a sheen; hologram: a conic hue gradient under a grey wash, fine diagonal rainbow lines, concentric rings, a diamond emblem with MN and "A U T H E N T I C"; seal: a scalloped radial-gold disc with a drop shadow, rosette engraving, two rings, circular microtext and a debossed italic MN.
- Wait for every font (document.fonts.load for each face, then fonts.ready) before drawing, and decode every image before capturing.

THE DISINTEGRATION
- Move the card to the top-left corner for the capture (so nothing is clipped on small screens), render it with html2canvas (backgroundColor null, scale min(devicePixelRatio, 1.5)), then hide the live card.
- Create 75 empty ImageData layers of the same size. For every pixel, three times: pick layer floor(75 × (Math.random() + 2x / width) / 3) and copy the pixel's RGBA into it. The x term pushes the left side into early layers; the random term keeps the edge ragged.
- Put each layer on its own canvas (class capture-canvas: fixed, centred, width min(600px, 92vw)) stacked in a fixed stage. Together they still show the card.
- For layer i: a paused gsap timeline with one tween of duration 1, delay (i / 75) × 2: rotate 30 × (random − 0.5) deg, translate 40px along a random angle (x = 40·sin a, y = 40·cos a), opacity 0.
- One progress p (0 whole → 1 dust) drives everything: render() sets every layer timeline's progress to p, fades the cue over p 0 → 0.13 and the contact shadow (opacity 0, scale 0.85) over p 0 → 0.4.
- A goal and an eased view: gsap.quickTo(view, "p", { duration: 0.9, ease: "power3.out", onUpdate: render }) chases the goal, which gives the soft lag of a scrub.
- The loop tweens the goal: to 1 over 4s (power1.inOut), hold 1.1s, back to 0 over 3s, hold 1.4s, then again, always starting from the current value.
- Input: the wheel adds deltaY / 1800 and a pointer drag adds its movement / 700 to the goal (clamped 0-1); either pauses the loop, which resumes 3.5s after the last input. Arrow keys glide between four stops (0, 0.3, 0.6, 1).

THINGS THAT BREAK
- html2canvas cannot see canvas-drawn effects it does not support (filters, blend modes); draw every asset into an image first and keep the card to positioned images, gradients and borders.
- Capture only after fonts and image decodes resolve, or the dust is made of fallback type.
- 75 full-size canvases are heavy: cap the capture scale at 1.5 and never re-capture on resize.
- Never make the page scroll to drive this: a scrollbar appears in every frame and preview it is embedded in. Drive the timelines' progress yourself.

THE FLOOR
One visually hidden h1 describing the card; the stage of fragments has role="img" and an aria-label; ambient layers, the cue and the veil are aria-hidden. prefers-reduced-motion stops the dripping cue and the loop; the dust only moves when the reader scrubs it. Works at 390px wide (the fragments scale to 92vw).
