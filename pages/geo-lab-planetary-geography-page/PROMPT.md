Build a landing page for GEO/LAB, a fictional planetary geography laboratory ("Read the planet like a contour.": it turns elevation, strata and orbital telemetry into living, instrument-grade terrain models), as one HTML file. No libraries. Google Fonts: Instrument Serif (with italic) for headlines and big numbers, Inter Tight 300-600 for text, JetBrains Mono 300-500 for every label.

DESIGN SYSTEM
A game-style FUI map. Near-black field #010507 (with #030c10 and #061419 steps), one instrument cyan #00E3FF (teal #28F9EB, mint #4EFFE3, ice #9EFFF3 and sky #22C2DD steps), amber #DDA322 for datums, waypoints and targets, alert red #FF2C00 and ember #FF571D for hazards, text #E4FAFD with two dimmer greys, and hairlines of cyan at 22%, 10% and 5%. A film-grain overlay and a vignette over everything. Headlines in Instrument Serif with one italic cyan word that glows; mono caps labels at .14em; corner-bracket frames on panels; buttons with two clipped corners (clip-path), solid cyan or a ghost with an inset cyan line.

SECTIONS
1. boot: a full-screen loader with a cyan bar, a percentage and four log lines ("INITIALISING DATUM…" to "SURVEY 976 READY") that waits for the fonts, then fades and starts the hero's line reveal.
2. nav: fixed, frosting after 30px; a contour-ring logo with an amber dot, four "/ " mono links, a live UTC clock and a "Request access" button.
3. hero: a full-screen canvas of drifting contours: seeded Perlin fbm terrain with a massif behind the HUD, turned into 22 isolines by marching squares and redrawn at ~30fps as the field drifts, every fourth line brighter and a dashed amber datum. A dot grid, a left shade for the copy, a scanning band and two tick rails whose markers follow the pointer. The pointer gets a spinning reticle with its elevation and coordinates and a brighter lens of contours around it. A frosted HUD (top right) reads elevation at cursor in big serif, an elevation profile through that row with an amber cursor line, latitude, longitude, slope (turning to "Slope alert" in red on steep ground), and a 24-bar band histogram. Three diamond waypoints (two amber, one blinking red hazard) show their live elevations. Copy: the three-line h1 rising line by line, a lede, "Begin a survey" and "View instruments".
4. ticker: a marquee of peaks and deeps with their elevations (negatives in sky blue).
5. instruments: a 4-column ruled grid (2 on tablets, 1 on phones) of instrument cards (Contour Engine with self-drawing contours, Strata Scanner with floating stacked plates, Orbital Survey with orbiting dots, Hazard Lock with a pulsing red target), each with an ID, a status light (online, tracking, alert), a serif title, copy and a spec line; a cyan top line grows on hover.
6. strata (340vh, sticky): eight canvas-drawn elevation bands of an island (each filled where the terrain is above its threshold, with an edge line, inner contours, a dot grid and corner ticks; the summit band in amber) stacked in CSS 3D (rotateX 58°, rotateZ −36°). Scrolling eases them apart up to 58px each, lights them band by band with the matching rows of a TER 01-08 list, and counts a "band separation" readout; a progress line runs along the bottom.
7. orbital: a list of four bodies (click or Enter to target) beside an SVG solar map: a tick ring with degree labels, a dashed rotating ring, a radar sweep, dotted orbits, four bodies, two red ships on tilted ellipses pointing along their paths, and an amber "TARGET LOCK" reticle and line that follow the selected body with its distance in AU.
8. metrics: four ruled figures counting up (148 M KM² modelled, 0.12 M vertical RMSE, 8 bands, 90 S hazard latency) each with a small sparkline.
9. protocol: four steps (Acquire, Stratify, Model, Publish) on a dashed line, with bracketed number nodes and an output line.
10. pricing: three survey classes (Field $0, Survey $49 per seat as the recommended cyan card, Planetary custom).
11. cta: a dimmer contour canvas behind "Every map starts with a coordinate." and an email form that validates and answers in mono ("Coordinate logged…" or "Coordinate rejected…").
12. footer: logo, blurb, three link columns, a huge outlined GEO/lab wordmark and a coordinate bar.

THINGS THAT BREAK
- Marching squares: interpolate each crossing along its edge and handle the two saddle cases (5 and 10) with two segments, or lines break at every saddle.
- Only compute and draw the hero and CTA canvases while they are on screen (IntersectionObserver), cap the frame rate, and use a coarser grid on narrow screens.
- Size the canvases by devicePixelRatio (capped at 2) and rebuild the strata and canvases on resize, debounced.
- Keep the strata labels counter-rotated so they read flat, and hide them on phones.

THE FLOOR
One h1, a main, aria-hidden canvases, the ticker and the boot screen, an aria-label on the HUD and the orbital SVG, keyboard-selectable bodies, a labelled email field. prefers-reduced-motion skips the drift, the scan and the boot animation (the map redraws only under the pointer). No horizontal scroll at 390px; the HUD and waypoints hide on small screens.
