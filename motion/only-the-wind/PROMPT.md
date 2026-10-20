# Only the Wind · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build an ambient, backlit evening scene as one HTML file: two travellers by a lake at sunset while cherry petals blow past in three depths, with a click that sends a gust through everything. No libraries and no image files: canvas 2D, inline SVG and CSS only. Google Fonts Shippori Mincho B1 (500/700) and Cormorant Garamond (italic 300/400).

THE PHOTOGRAPH (procedural, drawn once to a canvas)
- A seeded PRNG (mulberry32) and a tiling value-noise fBm.
- Sky gradient #a2979f → #c6b0a4 → #e7c69e → #f8dfb2 to the horizon at 66.5%; the sun at (38%, 54%) as a large radial scatter and a white core.
- Four mountain ridges from midpoint displacement, coloured by aerial perspective (mix #efd2ab haze toward #2c2027 ink by depth), the nearer two topped with tree bumps and one with a small five-tier pagoda; each ridge edge rim-lit where it crosses the sun. Haze pools in the valleys.
- A lake below the horizon: mirrored ridges at low alpha, thin ripple strokes, and a glittering sun path that widens toward the viewer. A near hill (dark #2c2023 → #0b0708) rim-lit along its top.
- Separate canvases: tileable fBm clouds lit from below that drift over 380s; crepuscular rays as thin wedges from the sun (screen blend, slow rotate); two bands of drifting mist; diffraction spikes.

THE FIGURES (inline SVG, backlit)
- A traveller in a straw hat, haori and hakama, a sword at the hip; a girl in a furisode with an obi, a hair ornament with dangles, holding a glowing oiled-paper parasol. A temple eave top-right with tile ends and rafters, a paper lantern with the character 風 and a glass wind chime with a paper strip.
- Each silhouette gets a rim-light filter: offset the alpha, subtract it, blur, flood with #ffdcaa and merge twice, so the sun wraps around the edges.
- Robes and hair strands breathe with SMIL path morphs (3–4s, spline eased); the lantern and chime swing (rotate −3° to 3.6°, 5s and 3.1s, alternate) and the strip flutters faster.

THE PETALS
- Three notched petal shapes drawn once to 160px sprites in two palettes (lit: #f29a83 → #ffd4c0 → #fff6e8; shade: #c66d8a → #e6a9bc → #f6dbe3) with veins, a deep base and a light edge; blurred copies (4 halvings) for the near field and a haze-tinted copy for the far one.
- Fields: far (130, 5–14px, hazed), mid (46, 15–32px) and near (9, 60–115px, blurred, three trailing ghosts). Scale counts by viewport area.
- Each petal: eases its vx toward a wind speed between min and max (smaller petals catch more wind), adds gravity × (1.5 − windFactor), adds sin(x × 0.01 + phase) × turbulence, damps vy by 0.98, tumbles on three axes, and respawns off the right edge when it leaves.
- Draw with setTransform from two axis vectors rotated by (angleX, angleY, angleZ): the shade sprite first, then the lit sprite at an alpha from how face-on it is plus a gaussian of its distance to the sun.

THE AIR AND THE LENS
- Grass: about one blade per 2.4px, each a quadratic curve swaying on two sines and bent by the gust, batched into six tone buckets (one fill each) with a rim stroke near the sun, batched by brightness.
- Dust motes that glow near the sun, soft bokeh rings drifting left, and lake glitter that twinkles (pow(sin, 8)).
- A lens flare that follows the sun on screen: bloom, a white core, a horizontal streak, the spikes, and six ghosts (dot, hexagon, ring, warm) placed along the line from the sun through the centre at k = 0.42 … 2.2.
- The camera breathes (scale 1.035 → 1.042, 16s alternate); the pointer parallaxes sky (8px), figures (12px) and grass (16px). Film finish: a soft-light grade, a vignette, animated grain, and a white flash that fades out on load.

THE WIND
- gust starts at 0; a click or Space adds 2.2 (capped at 3.5) and each frame multiplies it by 0.972. Petal speed × (1 + gust), turbulence × (1 + gust × 0.6), grass leans by gust × 0.28, dust and bokeh speed up.

THE HAIKU
- 花は散り / 名を覚えている / 風ばかり, set vertical (writing-mode vertical-rl) top-left in Shippori Mincho with a rough ink displacement filter; each character fades in from blur(8px), 0.13s apart. A thin rule grows under it and a red hanko seal (風) stamps in with an overshoot. An italic English caption bottom-left; a "Click to summon the wind" hint after 7s.

THE FLOOR
- prefers-reduced-motion stops every loop and the gust and cuts the petal count to 40%. Rebuild the canvases on resize (debounced). Cap the device pixel ratio at 1.5–2. The haiku moves in and the caption hides below 760px.
