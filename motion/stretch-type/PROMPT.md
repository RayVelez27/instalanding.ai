# Stretch Type · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a kinetic-type loop as one HTML file: the word MOTION in condensed red block letters on black, stacked three times, each letter's copies stretching and shrinking against each other. No libraries; the letters are SVG paths generated in JavaScript every frame.

THE STAGE
- Page #000, ink #ff3c38, system-ui. One screen, overflow hidden, user-select none. A small tracked caps mark top-left; a short caption at the bottom ("Drag up or down to scrub · Space to pause").
- Centred: an SVG, height min(70vh, 70svh), max-width 92vw, one path per letter copy (six letters × three copies), filled with currentColor. The stage wrapper is focusable with role="img" and a label; the SVG is aria-hidden.

THE LETTERS (design units: each column 486 tall, stroke 15.565, 11 between letters)
- Each glyph is draw(x, y, h, w) returning path data. I: a rect 16 wide. T: a 40-wide bar 15.565 tall and a centred stem. O: 38 wide, a rounded rect (r 13) plus a reversed inner rounded rect inset by the stroke, so nonzero fill leaves a counter.
- M (60 wide): two stems plus two diagonal bands 17 across, from the top corners to a centre apex at max(2.6 × stroke, 0.5h).
- N (50 wide): two stems plus a band from the inner top-left to the inner bottom-right whose vertical thickness is stroke × √(gap² + h²) ÷ gap, capped at 0.42h.
- Draw every subpath clockwise so overlaps merge under nonzero.

THE MOTION
- Per column, p = power1.inOut of a triangle wave: forward over 2.5s, back over 2.5s. Heights: top = short + (tall − short)·p, middle 162, bottom = tall − (tall − short)·p, where short = 72 and tall = 486 − 42 − 162 − short. Copies stack with 21-unit gaps.
- Each column runs on its own clock: (t + seek) × tempo, seek [1, 0, 1.5, 1, 0.5, 2], tempo [0.8, 1, 1.2, 1, 0.9, 1.1].
- Drag vertically on the stage to scrub (time += Δy ÷ stage height × 1.6 durations, holding while dragging). Space pauses; arrow keys pause and step a quarter stretch.
- prefers-reduced-motion: start paused on a mid pose; scrubbing and stepping still work.
