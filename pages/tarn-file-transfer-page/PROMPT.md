Build a landing page for Tarn, a fictional heavy-file transfer service for studios ("Heavy files, handled lightly.": film cuts, raw shoots and whole archives, 2 TB per send, links that expire, no account needed to receive), as one HTML file. GSAP 3.13 with ScrollTrigger, and Lenis 1.3.4, from jsdelivr. Google Fonts: Hubot Sans (wdth 115, weights 300-400) for display, Geist 400-500 for text.

DESIGN SYSTEM
One family of steel-blue greys: ground #424C55, deep #333B43, steel #66727A, steel-hi #7E8A91, pane #56616A, frost #D3DDE3, and a near-white glow #E6EFF4, with inks #F3F6F8, #D9DFE3, #AAB4BB and a shade #14191E for shadows. No accent colour: everything is frosted glass. A .glass surface is a vertical gradient of its tint (--gl) with a frost glow at the bottom edge, an inner shadow at the top and a bright 1.5px rim top and bottom (--rim). Pill buttons and round icon buttons; on hover a diagonal sheen slides across, icon buttons lift their arrow and their underglow rises. Big rounded slabs (radius clamp(28px, 4.4vw, 60px)) hold the dark sections; cards at radius 22-30px. Headings in Hubot Sans 300 at width 115%, -0.025em, balanced.

PICTURES IN CODE (no image files)
- The hero slab is a gradient textured with an SVG filter: fractal noise lit by feSpecularLighting from a point light, blended in overlay, so it reads as brushed, frosted metal.
- Five gallery "photos" as inline SVG with grain, vignette and slow SMIL drift: a foggy sea with a sun haze and hundreds of glints on the water, a photo studio with an octagonal softbox, a light strip and a camera on a tripod with floating dust, concrete steps under the shadows of bare branches (recursively drawn), a mixing desk with rows of knobs and animated meters, and a mountain lake whose layered ridges, fog and treeline are mirrored through a turbulence displacement ripple. The contact picture is a still lake with trees, also reflected.

STRUCTURE
1. A fixed glass pill header: a glass dot and "tarn", four links, a "Send files" button; under 1024px a round menu button opens a glass dropdown.
2. Hero (200svh, sticky): the textured slab fills the screen inside an edge margin with "Heavy files, handled lightly.", a line of copy and three check chips. On load the stage is scaled 4x from its bottom-left corner so the round upload button and "Send files" pill fill the screen; scrolling the first screen shrinks it into place (one --p custom property drives translate and scale). The upload button has a conic highlight orbiting its rim.
3. Manifesto: a long paragraph in wide light type, signed by the founder; a round glass lens travels across it on scroll in a serpentine path, showing a 1.3x copy of the text inside, aligned to the words underneath.
4. Services (deep slab): six glass tiles with a chip each (Transfers, Review links, Archive, Vaults, Delivery pages, Watch folders); a large soft light travels across the grid on scroll and each tile's rim lights up as the light passes it.
5. Process: a sticky heading beside four glass steps, each with an inset toggle switch that flips on as the step reaches the middle of the screen, joined by a line that fills down.
6. Speed (deep slab): "A 60 GB folder, door to door." with a giant "9 min" and four inset bars (Tarn, shared drive sync, office FTP, email parts) that fill in proportion when they appear, Tarn's bar lit; a footnote on how it was measured.
7. Try it (lit slab): a big round upload button and a long glass pill. Choose or drop a file and the pill fills to "Link ready" and shows a fake link; nothing leaves the device.
8. Work: a 12-column collage of the five pictures with glass captions hanging off their bottom edges; each picture opens from a small pill shape to its full frame.
9. Pricing (lit slab): a monthly/yearly segmented control with a sliding glass thumb that swaps the prices with a rise; three plans (Light $0, Studio $16, House $44 per seat), the middle one glowing. Voices: six glass quote cards in a marquee that pauses on hover. FAQ: a sticky heading beside six glass accordion rows whose plus turns into an x. Contact: details list, the lake picture and a glass form overlapping it that thanks inline. Footer: a line, links and a giant engraved "tarn" wordmark rising into the bottom edge.

THINGS THAT BREAK
- Add .motion in the head before first paint unless prefers-reduced-motion, and remove it if GSAP has not arrived after 2.5s; the 200svh hero, the zoom and every hidden starting state live behind .motion.
- The lens copy must be the same width as the paragraph and offset by K x (lens position), measured again on every ScrollTrigger refresh, or the magnified words drift off the real ones.
- Measure tile centres on refresh, not once, so the light still lines up after the grid reflows.
- Clone the marquee cards once, mark the clones aria-hidden and inert, and animate the track by -50%.
- Pause the orbit, lens, light and marquee while their sections are off screen.

THE FLOOR
One h1, a main, every section with an id. Pictures are role="img" with a label and an aria-hidden SVG. The menu button uses aria-expanded and swaps its label; Escape closes it. FAQ questions are buttons with aria-expanded and aria-controls; the billing toggle uses aria-pressed; the send label and form note are live regions. Focus rings on everything. prefers-reduced-motion: no zoom, lens or light, switches shown on, marquee as a static grid. No horizontal scroll at 390px.
