Build a single-file HTML landing page for "OVERCLOCK", a fictional one-command deploy tool, styled as an issue of a black-and-white manga. Bangers, Anton, Barlow Condensed and JetBrains Mono from Google Fonts, everything else inline. No images and no libraries: every illustration is inline SVG animated with SMIL, and the screentone is CSS. Strictly two inks, #111 and an off-white paper #f8f8f5. Use example domains only, especially in the curl | sh install line.

THE PAGE
One 1120px panel with a 4px ink border and a hard 10px offset shadow, sitting on a halftone-dotted grey desk. Under 640px the panel goes full bleed and loses the frame.

THE HAND-DRAWN LINE
Two SVG filters declared once (feTurbulence into feDisplacementMap): a strong one for outlines and a light one for display pieces. Never filter a box that contains body text, or the text wobbles too. Instead set border:0 on cards, steps, plans and the terminal and draw the outline as an ::after overlay with the filter on it. Apply the light filter directly to buttons, tags, badges, the logo mark and the big numbers.

THE HERO
A dot-screen background with a huge paper circle bleeding off the top left behind the copy. An "issue" tag (Vol. 03 · Dev Tools · 2026), then the h1 in Bangers, white fill with a 7px ink stroke using paint-order: stroke fill, rotated -2deg, with a boxed Japanese subtitle under it (限界を超えろ, beyond the limit). A lede on a padded paper panel (so the dot screen never runs behind the words) with one phrase reversed out in ink, two hard-shadow buttons that lift on hover and press on active, and a copyable install line.
On the right, a terminal panel tilted 1.5deg with a doubled offset shadow and a speech-bubble "12 seconds?!". It types oc deploy --prod, then streams detection, a cache hit, a build time, a block progress bar and a ✓ LIVE line, holds, and loops.
Behind it all, the scene: a retro sun rising into place, sliced by paper bars that slide down it and thicken as they go, two rings pulsing outward from it, a seeded skyline of ink buildings with lit and blinking windows, and a perspective grid floor scrolling toward the viewer. Reserve the hero's bottom padding for it.

THE SCENE BUILDER
Don't hand-write the suns and skylines. Mark them up as empty <g data-sun> and <g data-skyline> groups configured by data attributes (centre, radius, bar count, start, end, duration, invert; width, base, min and max height, seed, a dip so buildings shorten under the sun, night mode) and build them with one small script from a seeded PRNG, so the city is identical on every load. Pause each SVG's animations with an IntersectionObserver while it is off screen.

THE ROGUES' GALLERY
A diagonal-hatched break strip ("3 villains are wanted!"), then three villain cards in a 2+2 grid, the first full width split art/info. Each has a numbered tag, an animated scene, a boxed stat tag, a katakana sound effect, a name in Bangers, an ink "villain · defeated by X" role strip, a paragraph and a dashed-rule fact list:
The Slow Build: a speedometer whose needle swings from 14 MIN to 0.8 S with speed lines, over a conveyor of ticked boxes on spinning wheels.
Config Hell: four config file tabs whose tangled wires straighten into the OC badge, an "AUTO-DETECTED ✓" stamp and packets running down the wires.
The 3 AM Outage: an inverted night panel, a small sliced moon, twinkling stars, a skyline in night mode and a heartbeat line that spikes, with a "ROLLBACK!" flag.

THE REST
A "how it works" frame with a tab on its top edge, three steps with ghosted big numbers and code chips, and a note that uses strikethrough, wavy underline, an ink highlight and a hatched mark. A second break ("Choose your power level"), then three plans, the middle one inverted and tilted -1deg with a "Most picked!" tag.

READER MAIL
A third break ("Got questions?"), then a two-column FAQ of six native <details> items, the first open. Each summary is a tilted ink "Q.01" tag, the question in Bangers (wavy underline on hover) and a round plus that rotates into a filled minus when open. Wobble the item outlines with the same ::after overlay, hide the default marker, give the summary a dashed inset focus ring, and fade the answer in under a thick ink left rule.

THE FINAL CHAPTER
An ink end panel split copy and art. Copy: a bordered "Final chapter · Your move" kicker, "To be deployed…" in huge paper Bangers with a hard grey drop shadow, a tilted paper caption, a line of copy, a terminal-style signup (a "$" prompt cell, the email field and an ink "Join beta →" button fused into one paper bar with a hard shadow that lifts on focus-within), an inline validation line and three ✓ perks. Art: an inverted sliced sun setting on a horizon, pulsing rings, twinkling stars and a perspective floor whose cross-lines accelerate toward the viewer, with a floating paper chip showing the ✓ LIVE result. Faint concentric rings and a masked dot screen texture the ink. A thin footer.

THE FLOOR
One h1 and a main, data-section on every region, aria-hidden on every scene, the terminal given role="img" with a label describing the run, labels on the copy button and the email field, visible focus rings in both inks, no horizontal scroll at 390px. Under prefers-reduced-motion stop the typing (print the finished run), draw the suns as static slices and freeze every SMIL scene on a good frame rather than hiding it.
