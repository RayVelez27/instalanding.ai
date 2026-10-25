Build a landing page for Ochre, a fictional AI meditation app ("Meditation that listens": it hears your breath through the phone or earbuds, learns the shape of your day and builds a session that fits, from three minutes to a full night's sleep; private by design, breath analysed on device), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, from jsdelivr. Google Fonts: Reddit Sans 200-900 with italics, display set very light (100-300) and tight.

DESIGN SYSTEM
Ink #01262D, paper #F5C279 (the page), sun #EE8903, sage #586354, khaki #8C7D5A and rust #9A4703, with mixed tints for soft text on ink and on paper. A sunset poster: a big sun disc with a radial highlight, thin orbit arcs drawn as dashed SVG circles, and stepped "pillars" of sage, khaki and rust standing on a double rule like a skyline. Display headings Reddit Sans 200, -0.035em; small labels tracked 0.42em uppercase. Pill buttons whose fill wipes in from the left on hover; links redraw their underline; round icon buttons fill sun from below. An 8% multiply grain over everything and a sun progress line at the top.

PICTURES IN CODE (no image files)
- Canvas landscapes painted from presets: layered fbm ridges and dunes lit by slope, pine silhouettes, fog bands, sun with halo or a cratered moon, stars and a Milky Way band, an aurora, clouds, water that reflects the sky by redrawing rows with a ripple offset, wave streaks and glitter; vignette and grain. Seven presets: lake at dawn, ocean at dusk, desert night, forest rain (animated rain), northern lights (animated snow), valley fog, moon over water.
- Phone mockups built in HTML with container-query units: a titanium frame, dynamic island and glass glare, and four screens over a painted scene (Breathe with me with a glossy glass breathing orb that scales on a 10-second cycle and cues that fade in and out; a sleep story with a waveform and chips; a morning check-in with mood pills; a weekly insights bar chart).
- The hero phone screen is a real-time WebGL ocean: a ray-marched heightfield of rolling swells under a dusk sky with clouds and a low sun, Fresnel reflections and fog, tilting the phone toward the pointer; it falls back to the painted ocean without WebGL.
- A CSS candle with a flickering flame and glow, a glowing orb macro with ripples, and a studio of three phones with reflections.

STRUCTURE
1. A fixed header, transparent over the hero then frosted paper: sun mark and "Ochre", five links and "Start free"; under 1020px a two-line menu button opens a full-screen ink menu.
2. Hero (pinned for 110svh): an ink field covers the left 38%, "OCHRE" fills the width in weight 200 with its letters paper over the ink and ink over the paper, the sun sits on the split with an orbit arc, "in / out" in huge thin type on the ink, the pillars along the bottom, the phone rising from below, a tracked "iOS · Android · 14 days free", an intro with two buttons, and a three-column footer strip on a double rule. On scroll the ink sweeps across to cover everything, the sun sets behind the pillars, "in / out" glows sun-coloured and the copy fades.
3. A sun-coloured ticker. Manifesto (ink): a statement whose words light up as you scroll and three huge thin stats (3, 180, 9).
4. Features: six ruled rows (Adaptive sessions, Breath sensing, Sleep, Focus, Daily check-in, Weekly letter) with number, title, text, meta and a round picture; rows fill ink from below on hover.
5. Soundscapes (sun): six arch-topped painted scenes with glass play pills, in three columns drifting at different parallax speeds.
6. Privacy (ink, pinned 140svh): the moon-over-water scene opens from a circle as a dark moon slides off it and a ring expands, then "A quiet room in your pocket" and three facts appear.
7. A day with Ochre: a split background (ink left, paper right) with the title coloured to match; a sun line grows down the split with a dot running along it; four sticky times of day (07, 13, 19, 23) whose numbers turn sun as they pass, each beside a list of sessions.
8. Pricing (ink): four plans ($12, $70, $110, $240) whose coloured pillars rise in proportion to the price. Gallery: a 12-column collage of six pictures (check-in phone over the dawn lake, the orb macro, a sleep story under the aurora, the three-phone studio, a focus timer over forest rain, the candle) drifting at different speeds around a sun disc.
9. Reviews (ink): five quote cards with glossy initial gems in a marquee that pauses on hover. Trial (sun): "Your first breath is on us" whose letters turn paper inside an ink disc that grows from a dot. FAQ: sticky title, six details rows. Contact: an ink column of contacts and a paper column with a newsletter form, a rising sun and pillars. Footer: a double rule, four columns and a giant "OCHRE".

THINGS THAT BREAK
- Add .motion in the head before first paint unless prefers-reduced-motion, and remove it if GSAP has not arrived after 2.5s.
- Paint each canvas only when it nears the viewport, at its real size, and repaint on resize; keep rain and snow on a cached base image and pause them off screen.
- Cap the WebGL canvas at 1.75 DPR, stop its loop when off screen or hidden, and handle context loss.
- The hero split and the title gradient share one --split custom property so the letters always change colour exactly at the edge of the ink.

THE FLOOR
One h1 (the wordmark, with a screen-reader tagline), a main, every section with an id. Canvases that are pictures have role="img" and a label; decorative ones are aria-hidden. The menu button uses aria-expanded and swaps its label; Escape closes it. FAQ is details/summary; the signup has a label and a polite live status and sends nothing. Focus rings on everything. prefers-reduced-motion: no pinning, breathing, weather or marquee, one still frame of the ocean. No horizontal scroll at 390px.
