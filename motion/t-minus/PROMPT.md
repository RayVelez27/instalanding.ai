# T−Minus · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build a countdown loop as one HTML file: a 5×5 grid of frosted glass tiles counting from nine to zero, every tile cropping its own slice of one giant numeral. No libraries; Bricolage Grotesque 700 for the digit and JetBrains Mono for the HUD, from Google Fonts.

THE STAGE
- Near-black radial background; a blurred aurora of three hue-tinted radial gradients that drifts slowly; a vignette; animated film grain. Keep the oversized layers inside fixed, overflow-hidden boxes so phones do not widen the layout.
- Centred: a square of min(60vmin, 620px) holding the grid, a blurred copy of the digit behind it that swells with the pulse, four corner brackets and three hidden shockwave rings. The grid has a faint reflection below (-webkit-box-reflect) and tilts toward the pointer (perspective 1400px), swaying gently when idle.
- HUD in mono caps: Live / Paused with a blinking dot and Sequence 001 top-left; a T−00:09.000 timecode and the current hue top-right; ten progress segments and Space / R hints at the bottom.

THE TILES
- Each tile: rounded, a 1px inner line, a soft top gloss, backdrop blur, and a radial light that follows the pointer across the whole grid.
- Its digit is a ::before at the full grid size (size ÷ 0.73, text-box: trim-both cap alphabetic), filled with a three-stop gradient clipped to the text. With dx, dy the tile's offset from the centre and pitch = (size + gap) ÷ 5: translate(−dx·pitch·t, −dy·pitch·t) scale(m + (1 − m)·t), where t = 0.2 + 0.8·zoom and m = 0.7 ÷ 5. At zoom 1 the tiles join into one numeral; at 0 each shows a small whole digit.

THE MOTION
- Clock in JS. Each tile reads the time minus 0.06s per step of Manhattan distance from the centre; its digit is 9 − floor(local) mod 10 and its --zoom is a cubic in-out of a triangle wave over each second (registered with @property).
- One registered --h: 205 + 20 per second counted (blue → magenta → orange), transitioned over 900ms; tiles add (dx + dy) × 7.
- At zero: three rings scale from 0.15 to 2.8 and fade (staggered 0.1s), a screen-blended flash, and the grid kicks to 1.045.
- Space pauses, R or a click restarts, arrow keys pause and step a quarter second.
- prefers-reduced-motion: start paused on a full-size digit; no tilt, drift, grain or shockwave.
