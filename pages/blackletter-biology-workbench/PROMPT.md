Build a single-file HTML landing page for "Mistfold", a fictional computational biology workbench (protein structure prediction, genomic alignment, molecular docking, single-cell analysis). The look is an illuminated manuscript on warm paper: blackletter headings, a serif body, framed panels with ornaments, and pale hand-drawn lab sketches drifting in the side margins. Google Fonts: UnifrakturMaguntia (headings and logo), Fanwood Text (body, 17px, line-height 1.55), Cinzel (numbers and small caps labels), JetBrains Mono (code). Rough.js 4.6.6 from jsDelivr for the sketches; everything else is hand-written CSS, inline SVG and one WebGL shader. Fictional brand, numbers and testimonial, labelled as such.

THE SYSTEM
- Tokens on :root: paper #f4f2ec, card #fdfcf9, tint #eef2ef, ink #4d524f / strong #1d2420 / soft #7a7f7b, lines #e2ded3 and #d3cec1, and the accents green #4c7264 (primary), blue #4c6d7b, violet #675a7c, mauve #86667f, mint #8fbcaa, lilac #b3a3c6. Three faint radial washes on a fixed body background.
- An SVG <symbol> sprite of 24x24 line icons (lens with a helix, microscope, hexagon, atom, folio, funnel, branching nodes, hexagon with a spark, open codex, sealed envelope), all stroked with one green-blue-violet userSpaceOnUse gradient.
- A four-point star as a data-URI SVG used as a CSS mask for every bullet, so bullets take any colour or gradient.
- Buttons: small uppercase serif, 1px green border, radius 6px with corner-shape: scoop (progressive), solid variant with a soft green shadow.
- Frames (.wbbase): 760px panels, padding 40px 30px, an inner 1px outline inset 7px, and a moving border: an @property --angle animated 0 to 360deg drives a conic gradient of greys with green-mint-blue and violet-lilac arcs, painted on a ::before with the padding-box/border-box background trick, plus a blurred copy at 28% opacity behind it as a glow. Stagger each frame's animation-delay so they are out of phase.

THE SECTIONS
- Sticky frosted nav: blackletter "Mistfold" logo, four uppercase links (hidden under 760px), a solid "Request access" button.
- Hero frame: the h1 "From Sequence to Structure" in 58px blackletter, an italic subtitle, a 60px vertical rule that draws down on load with a glowing spark that keeps travelling down it, an intro paragraph with a gradient left rule and a light sweep that runs down it every few seconds, four stats (0.92 median pLDDT, 40x faster alignment, 12M cells indexed, 100% reproducible runs) that rise in one by one with shimmering separators, and two CTAs.
- Modules frame: a small green label pill ("the instruments"), a 44px h2, an intro, a fleuron divider (❦ between fading rules), then four cards, each in its own accent via --accent: blackletter name, "compute intensity" as one to three filled hexagons, a description, star-bullet list, and a tinted footer split in two ("built on" / "outputs" with icons). Cards fade up as they enter with an IntersectionObserver.
- Workflow frame: four tinted steps (Ingest, Compose, Run, Publish), each with a pearl medal holding an icon inside a conic gradient ring cut out with mask-composite (it spins on hover), then a short Python SDK snippet in a paper-coloured code block with a green left rule and keyword, string and comment colours.
- Pricing frame: three tiers (Academic free, Lab $490/month featured with its own faster moving border, Enterprise custom) with star bullets, then an italic blockquote clearly labelled as an example testimonial.
- Finale: one wide frame that is both the CTA and the footer. A soft drifting aurora behind "Begin Your First Fold", a lead, an email + button form in one scooped pill (local only: on submit it shows an italic thank-you line in an aria-live region), three star-bulleted assurances, a fleuron rule, a four-column footer, a legal bar, and the "Mistfold" wordmark at the full width of the panel.

THE SHADER TEXT
One hidden WebGL canvas renders every blackletter heading, the nav logo and the footer wordmark. For each, rasterise the text into an offscreen 2D canvas as white on transparent (for headings, walk the text nodes and use Range.getClientRects so each word lands exactly where the DOM laid it out), upload it as a texture, and run a fragment shader that only draws where alpha is set: domain-warped fbm noise mapped through the five-colour green-mint-blue-violet-lilac palette, a bevel normal from the alpha gradient lit by a light that drifts and follows the pointer, a specular glint, a diagonal light band that sweeps across, and a little grain. Copy each result into a 2D canvas laid over the heading. Only after drawing, add a class that makes the real text transparent, so the CSS gradient text stays as the fallback and screen readers still read the real heading.

THE SKETCHES
A fixed full-viewport canvas behind the content, desktop only (min-width 1100px): twelve 24x24 biology icons (helix, benzene, atom, flask, cell, microscope, lens, petri dish, ribbon, virus, branching nodes, pipette) drawn with Rough.js in six muted inks at 32-54% alpha. Place them on a seeded grid in the two side margins, skipping any spot that would overlap a frame. Pre-render four rough "takes" of each and swap between them about seven times a second for a hand-drawn boil, with a slow bob and tilt.

THINGS THAT BREAK
- Wait for the blackletter font (document.fonts.load, with a timeout) before rasterising text, or the first frame is drawn in the fallback serif; re-layout on resize with a ResizeObserver.
- Never hide the headings in CSS up front: if WebGL is missing or the program fails to link, the gradient text must still be there.
- Cap the shader canvases at 1.5x DPR, pause any that are off screen with an IntersectionObserver, and skip frames while document.hidden.
- Load Rough.js with defer and start the sketches on DOMContentLoaded; guard on typeof rough so the page still works without it.
- Use overflow-x: clip on html and body (not hidden) so the sticky nav keeps sticking.
- Do not hotlink fonts or images from other sites: Google Fonts and a CDN script are the only external requests.

THE FLOOR
One h1, a main, data-section on every region, aria-hidden on the shader canvases, sketches and icons, a labelled email input, visible focus rings. Under prefers-reduced-motion every CSS animation and transition stops, the frames show a fixed ring angle, the cards are visible at once, and the shader renders one still frame. No horizontal scroll at 390px.
