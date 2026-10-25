Build a landing page for Easel, a fictional AI studio assistant for artists ("Your hand. A hundred more.": it sorts references, blocks in values, suggests palettes and preps print files while every stroke that matters stays the artist's; suggestions always land on their own named layers, it learns your palette and never imitates other artists, private by default), as one HTML file. GSAP 3.13 with ScrollTrigger, and Lenis 1.3, from jsdelivr. Google Fonts: Gabarito 700-900 for display, Rethink Sans 400-700 for text, each with a metric-matched local fallback.

DESIGN SYSTEM
Two inks like a risograph: blue #11138d (the page), pink #ed008e, paper #f3f3fa and ink #07061f. CSS cascade layers: tokens, base, atoms, layout, sections, scenes. Display type Gabarito 800-900, very tight. Pill buttons whose hover fill grows as a disc from below; links underlined with a dotted radial-gradient that swells into a solid bar on hover; round icon buttons with a dot that drops. A "trail" atom: a CSS mask of dots that shrink up a column, like ink left by a roller. Surfaces have a scalloped top edge from a radial mask.

PICTURES IN CODE (no image files)
Every illustration is a greyscale SVG (a hand with an ink roller on a slab, a print peeled from a block, a stapler on printed sheets, hands trimming a sheet on a cutting mat) inside .m-photo, where lighten and darken blends map dark to blue and light to pink, so they print as duotone. Six abstract "studies" (horizon, halftone ground, arcs and spheres) come from a seeded generator into svg[data-art]. Shared halftone, wood, brick and mat patterns in one hidden defs block.

STRUCTURE
1. A fixed nav, transparent then blue, that hides on scroll down: two-dot mark and "easel", five dotted links, "Start free"; under 900px a round menu button opens a full-screen pink menu.
2. Hero: "Your hand." in pink and "A hundred more." in paper, each line filling the width from its letter count, an intro and two buttons, and four lanes each with a pink drum disc that bobs and a dot trail. Scrolling on, the drums roll down and across into a four-band pink panel ("Layers, never a flattened image."), each band printing as its drum passes and the drums shrinking away; beside it a duotone photo and three facts.
3. Layers (paper): four named layers (Sketch, Colour, Light, Texture) beside a 4x4 chart where a blue plate of columns and a pink plate of rows in 0/30/60/100% halftone slide in from opposite sides into register, with crop marks.
4. How it works (blue): pinned, five numbered step cards (Gather, Block, Paint, Refine, Ship) slide sideways while a sheet prints its blue plate then its pink one and the sheets under it fan out.
5. Features (pink): six features in a two-column kit beside three duotone photos. Studies (blue): six study cards in three lanes that piston into line on scroll with dot trails.
6. Pricing: a form of pill radios, a seats number and an assists select beside a scalloped paper ticket that prices live (plan rate + assists + style model, x0.8 yearly). Uses (paper): six big rows (Concept art, Picture books, Comics, Tattoo flash, Album covers, Game textures) that drift sideways like a lens with a pink misregistered shadow away from the centre.
7. FAQ (pink): six details rows. Contact (blue): copy, email, a local-only signup form with a status line, and four drums that drop and print their trails. Footer (paper): "easel" filling the width, three columns and a base line.

THINGS THAT BREAK
- Queue every motion setup and run them in order after fonts load; if one throws, revert its GSAP context and undo the attribute changes it made, so a broken scene never breaks the rest.
- Measure the hero geometry in onRefresh after resetting transforms, and pause the bobbing when the hero is off screen.
- Headings with data-8b-motion="register" start with a pink offset shadow that settles into register as they scroll in; "screen" reveals photos through a growing dot mask once.

THE FLOOR
One h1, a skip link, a main, every section with an id and aria-labelledby. Photos have role="img" and a label; decorative drums and plates are aria-hidden. The menu button uses aria-expanded, takes focus to Close and Escape closes it. FAQ is details/summary; the forms have labels, the ticket total is aria-live and nothing is sent. Focus rings on everything. prefers-reduced-motion: no smooth scroll, pinning or scrubbing. No horizontal scroll at 390px.
