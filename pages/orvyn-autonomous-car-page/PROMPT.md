Build a landing page for ORVYN ONE, a fictional AI-native grand tourer that unlocks autonomy in five verified stages ("It already knows the road ahead."), as one HTML file. No libraries. Google Fonts: Geist 200-600 (everything, mostly 200-300), Geist Mono 400/500 (labels), Instrument Serif italic (one word per heading).

DESIGN SYSTEM
Near-black (#020203 ground, #0b0b0f panels) with hairline white borders at 7-12%, ink #f3f2f7, mute #8b8a96, dim #55545f, and one five-colour spectrum: cyan #3fe0ff, blue #2f6bff, violet #6a2bff, magenta #ff1f6b, orange #ff4a12. Headings are Geist 300 with -0.04em tracking and one serif-italic word filled with the spectrum gradient. Mono labels are 11px, uppercase, tracked 0.18em. A moving film-grain overlay at 5.5%. The primary button is a dark pill whose 1px border is a conic spectrum spinning around it (an @property --sweep angle animated to 360deg) with a blurred copy glowing behind; the arrow nudges on hover. One out-ease (0.16, 1, 0.3, 1) and one in-out ease (0.7, 0, 0.2, 1).

SECTIONS
1. nav: fixed; logo (a dashed spectrum ring around a triangle) and ORVYN tracked wide, four mono links, a blinking "Fleet online · 41,208" and a Reserve button; it frosts after 20px.
2. hero: copy on the left (a NEW pill, the headline with "ahead." in serif spectrum, a lede, Reserve and a "Watch it drive" play link, and a glass level card: LVL number, a coloured dot, name and description that cross-fade, and five dots that fill up to the current level). On the right, the autonomy dial (below).
3. ticker: a marquee of fleet figures (4.12B autonomous km, 0.003 disengagements per 10k km, 300 m perception, model N-7.4, 22 sensors, 8 ms, 148 cities).
4. autonomy: "Autonomy, unlocked in five stages." A five-part progress bar and five level cards (Assisted, Partial, Conditional, High, Full, each in its own spectrum colour) that light up in turn when scrolled into view: a soft colour bloom, a lock whose shackle swings open, the name, a line and verified km / state.
5. systems: a six-column bento: a big perception card (a radar of rings and ticks with a car glyph at the centre, a rotating conic sweep and four labelled blips that flash as it passes, plus sensor counts), a neural driver card (36 live bars and 2,000 TOPS counting up), an energy card (a 270° tick gauge filling to 86%), a dual-motor card (28 flame bars and 2.9s), and an over-the-air card (three release rows, the newest tagged Tonight). Cards carry a pointer spotlight.
6. manifesto: one huge centred sentence whose words light up one by one as it scrolls through the viewport.
7. specs: a sticky square HUD on the left (tick rings, a spectrum arc that fills to 82%, 305 KM/H · VMAX, a live clock and coordinates in the corners) and a ten-row spec table on the right.
8. reserve: "Your first drive is its thousandth." with a pill email form that confirms inline, then a horizon: a huge spectrum ring rising like a planet edge with a blurred glow, ticks and the five level colours as segments along its rim, fading into the page.
9. footer: brand and three link columns, ORVYN as an outlined spectrum wordmark fading downward, and a status line.

THE DIAL (SVG over CSS rings)
- A square container. A back SVG (viewBox -500..500): five ring segments centred at 0, 30, 60, 90 and 120 degrees between r 322 and 352, labelled LVL 01-05 along the arc, each a button; above each, a lock pod at r 432 whose shackle rotates open and whose ring takes the level's colour once reached; a blurred wedge of the active colour behind the active segment; a slowly spinning dashed ring; a scanner line that enters from the left and stops at the outer ring.
- CSS rings stacked in the middle: a "heat" ring (a conic violet → magenta → orange gradient masked to a thin band, with a blurred copy) and a progress ring (a conic blue → cyan sweep from -135deg to an @property --span angle, chopped into fine ticks with a repeating conic gradient), both radial-masked to bands.
- A front SVG: 150 faint outer ticks, a counter-spinning ring of 180 coloured dots, 96 inner ticks coloured around the circle with a highlight that sweeps round every few seconds, a dark core disc with two pulsing rings, a white needle, and a centre readout (AUTONOMY, the big level number, the level name in its colour) sized in container units.
- setLevel(n): --span = 70 + n × 43 degrees (transitioned 1.5s), needle and wedge rotate, reached segments darken to their colour and the active one fills, pods up to n open, the card and dots update. It autoplays 1 → 5 every 3.4s; a click on a segment, pod or dot sets the level and pauses autoplay for 9s.

THINGS THAT BREAK
- Register --span and --sweep with @property, or the progress ring and button borders jump instead of animating.
- Build the dial's ticks with createElementNS, not innerHTML strings, and keep the rings and SVGs in one square box so they stay concentric.
- Run the shimmer, bars and flames only while they are on screen (IntersectionObserver).

THE FLOOR
One h1, a main, role="group" on the dial with labelled segments that work with Enter and Space, labelled level dots, aria-hidden on decorative SVGs and the ticker, a labelled email input. prefers-reduced-motion stops the grain, spins, shimmer, marquee, autoplay and bars and shows everything revealed. Under 820px the dial sits above the copy at full width; no horizontal scroll at 390px.
