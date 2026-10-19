# Elastic Portrait Accordion · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build an elastic portrait accordion as one HTML file: an editorial row of five tall rounded portrait cards ("The Portrait Edit, Vol. I"); click one and it springs wide, zooms in a touch and reveals an italic caption, while the others squeeze thin. GSAP 3.12 from cdnjs; Google Fonts Cormorant Garamond (italic 400/500) and Inter (400/500). No other libraries, no image files.

THE STAGE
- body is a full-height flex centre on a 135deg gradient #295fd5 → #9d8ce0, user-select none, Inter. A small mark top-left: "The Portrait Edit" in Cormorant italic 20px, then "VOL. I" in 11px caps tracked .32em, white at 85%.
- One .group with white-space: nowrap, overflow hidden, padding 7vh 2vw 9vh. Each .item: inline-block, 15vw wide, 75vh tall, 1vw margin, 3vw radius, overflow hidden, isolation isolate, cursor pointer, a deep indigo drop shadow. ::after draws an inset 1px white hairline and a brighter top edge; ::before darkens the bottom 38% for the caption.
- Captions (.cap) sit bottom-left, hidden: "N° 02 — PORTRAIT" in 10px caps tracked .34em, the name in Cormorant italic clamp(26px, 5vh, 52px), and a 36px hairline rule.

THE PORTRAITS (one SVG function, five palettes)
- portrait(sitter, id) returns a 200x200 SVG (xMidYMid slice) with gradients namespaced by id: a background, drifting blurred orbs, then a gently breathing group with back hair, a garment, neck with shadow, ears, a face path filled with a radial skin gradient plus a side shade and a blurred rim light, highlight and blush ellipses, brows, eyes (white, gradient iris, pupil, catchlights, lids and a liner flick, all clipped to the eye shape; or closed with lashes), a nose and nostril shadow, lips from two gradient paths with highlights, then front hair and extras. A vignette and a feTurbulence grain overlay finish it.
- Sitters: Ember (long dark waves, sunset studio, a gold pendant), Lagoon (curls built from seeded circles, deep teal, gold hoops), Velvet (burgundy bob, eyes closed, black lapels), Aurum (copper bun, round gold frames, a ribbed green collar), Nocturne (pixie crop, moonlit sky with twinkling stars, pearl drop earrings). Use a seeded PRNG so the curls and stars are the same on every load.
- Ambient life in CSS: orbs drift (11-17s), eyes blink (scaleY .08 at 95.5% of a 6s loop), earrings sway ±5deg, the figure breathes 0.6px, stars twinkle. transform-box: fill-box so each shape moves around itself. All of it stops under prefers-reduced-motion.
- The SVG is absolutely positioned at top 0, left 50%, width max(75vh, 100%) with a negative margin of half that, height 75vh: it stays centred and covers the card at any width.

THE MOTION
- expand(item, i): mark every other card unclicked; tween all cards to width item.clicked ? 15vw : 8vw over 2s with ease elastic(1, 0.6); flip item.clicked; tween the clicked card to item.clicked ? 42vw : 15vw over 2.5s with ease elastic(1, 0.3). Both with overwrite: true.
- Every caption fades out and drops 12px (0.35s, power2.in); every portrait eases back to scale 1 (1.6s, power3.out). If the card opened: its caption rises in after 0.55s (1s, power3.out) and its portrait pushes in to scale 1.06 (2.4s, power3.out, transform-origin 50% 45%).

THINGS THAT BREAK
- Without overwrite, a quick second click leaves the first card's longer tween running after the new one ends, and two cards stay open.
- A fixed 75vh-wide SVG is narrower than a 42vw card on wide screens, which shows the card's edges and loses its rounded corners. Size it max(75vh, 100%).
- Namespace every gradient, clip path and filter id per portrait, or all five paint with the first one's colours.
- Keep the row on one line (nowrap): 4 × 8vw + 42vw plus margins stays under 100vw.

THE FLOOR
- Under prefers-reduced-motion, run the springs almost instantly and stop the ambient loops. Cards are clickable divs in the original; for production make them buttons with aria-expanded and give each SVG a label. Works at 390px wide (the widths are viewport units).
