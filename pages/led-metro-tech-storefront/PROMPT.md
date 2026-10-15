Build a single-file HTML homepage for "Meridian", a fictional devices, apps and AI company (laptops, a tablet, a productivity suite, an AI assistant called Assist). Warm paper page, clay and frosted-glass surfaces, and one dark LED dot-matrix panel as the hero visual. GSAP 3.12.2 and ScrollTrigger from cdnjs; Google Fonts Bricolage Grotesque (headings), Fraunces italic (accent words), Instrument Sans (body copy), Inter as the fallback. No images: every device, icon and logo is CSS or inline SVG. Fictional brand, offers and copy, with a footnote saying so.

THE SYSTEM
- Tokens on :root: page #f6f5f1, ink #111317, grey #6f747c, hairline rgba(17,19,23,0.08), purple #9d8cdc / deep #6c5bbd, mint #8fdea0, near-black #16191e, clay-light #f1f0ec. Four clay shadow recipes (light, dark, purple, green: one outer drop plus an inset highlight top-left and an inset shade bottom-right) and a three-layer soft shadow for cards.
- A fixed SVG fractal-noise grain at 3.5% over everything, and three blurred colour blobs (purple, mint, peach) behind the hero.
- Every heading pairs a Bricolage word with one Fraunces italic accent filled with a purple gradient via background-clip:text and lit by an SVG glow filter (stacked feGaussianBlur + feColorMatrix + feOffset layers merged under the source). Dark surfaces use a warm white glow, the ballot banner a green one. Descriptions are a grey gradient clipped to text with one phrase in .hl set solid ink and bolder.
- Primary CTA: a dark pill with the label left and a 51px pink circle right holding a 2-column dotted arrow that slides on hover. On dark surfaces it inverts to a white pill.

THE HERO
- A sticky frosted nav (radius 22px, top 14px): globe-with-meridians brandmark + "meridian" wordmark, five links, a Personal/Business segmented control with a white thumb that GSAP slides between buttons, a search button, and a hamburger under 1024px.
- Left: a NEW badge pill, the h1 "Meridian Book Ultra" at 88px with "Ultra" as the accent, a lede, the CTA plus an underlined text link, and an "AI-powered suggestions" glass card with three chip links.
- Right: a small pixel-art glyph with a caption, then the LED panel: a dark rounded bezel with a white 6px ring and purple glow, a header row ("LIVE NETWORK" with a blinking green dot, Chase/Rainbow/Breathe mode buttons, six colour swatches that filter lines), and a 36x20 dot grid. Six metro lines are waypoint lists whose segments are straight or exactly 45 degrees; each is expanded to one LED per cell. Each LED is an <i> placed by --x/--y custom properties and sized from a --pitch that a ResizeObserver computes from the screen box. Cells shared by two lines get interchange rings, and a glowing white "train" per line rides a looping GSAP timeline along the waypoints. Chase is a per-LED opacity keyframe delayed by index; Rainbow sets hsl(i*9deg) and hue-rotates the layer; Breathe pulses the whole layer. On boot the LEDs scale in, staggered by index.
- Floating over the panel: a rotated black PRE-ORDER sticker, a white "$1,000 back" trade-in pill and a "Secure" pill, each on its own sine float. Below, a timeline rule ending in a mint "NEW RELEASE" clay tile, and a short h3 + paragraph.

THE REST
- Quick links: six white cards whose dark fill slides up from the bottom on hover while the icon tile turns mint and the arrow rotates -45deg.
- Featured: a 600px slider with three slides (dark laptop slide whose screen is a second LED map in Rainbow mode, a lavender tablet slide, a mint slide with three stacked laptops and a chip badge), a 6s progress bar, a count, and pause/prev/next buttons; the UI turns light on the dark slide.
- Travel light: a two-column card with three serif specs and a CSS laptop whose lid opens (rotateX -88 to 0) scrubbed by scroll, inside concentric rings.
- Three AI article cards with a cursor-following radial spotlight: orbiting satellites round a shield, a third LED map, and datacenter towers growing out of the ground with leaves.
- FAQ: a sticky intro column and a GSAP height accordion (one open at a time, aria-expanded, aria-controls).
- A dark ballot banner topped by a dot-matrix ticker: a 5x7 bitmap font rendered as SVG circles, doubled, and scrolled with steps() easing so it moves one LED column at a time.
- Footer: "Follow" plus the brandmark, socials, six link columns, a bottom bar and the fictional-brand footnote.

PERSONAL / BUSINESS
Both copies of every audience-specific string live in the DOM as [data-for="personal"] and [data-for="business"]; a body class hides one set. Business also swaps the accent to blue (#2f6fe0, its own glow filter, blue badge dot and button accent). Switching staggers the new copy in, shows a toast, and saves the choice to localStorage inside try/catch.

THINGS THAT BREAK
- body must use overflow-x: clip, not hidden, or the sticky nav stops sticking.
- ScrollTrigger.batch with once: true never fires for elements already past its start when the page loads scrolled or jumps to an anchor; also sweep on ScrollTrigger refresh and scrollEnd and reveal anything on screen.
- Never put a float loop and a scrubbed parallax on the same element's y: the LED panel gets only the parallax, the pills only the float, and the floating suggestion card gets no hover lift.
- In the single-column slide layout use grid-template-columns: minmax(0, 1fr); a bare 1fr grows to the 460px laptop and the slider clips it at 390px.
- Pause each map's train timelines while its screen is off screen, and re-place the segmented thumb after document.fonts.ready because the web fonts change the button widths.

THE FLOOR
One h1, a main, data-section on every region, aria-pressed on the toggles and swatches, aria-label on icon-only buttons, aria-hidden on decorative art, visible focus rings. Under prefers-reduced-motion: no intro, floats, trains or reveals, the slider does not autoplay, and the LED boards render fully formed. No horizontal scroll at 390px.
