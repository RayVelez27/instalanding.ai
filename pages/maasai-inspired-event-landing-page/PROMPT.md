Build a single-file HTML landing page for "Sundune Events", a fictional studio that hosts festivals, retreats, ceremonies and galas co-hosted with Maasai communities in Narok, Kajiado and Laikipia. The hero recreates a Rive animation (a Maasai-inspired event hero banner) without any Rive runtime, and every texture and illustration on the page is drawn in code: no image files. Warm dusk palette, an editorial serif, and copy that presents community hosts as partners, not performers. Fictional studio, clients, dates and numbers, labelled as such, with a credit line for the Rive design it recreates.

STACK
- No libraries. Google Fonts: Instrument Serif (headlines, numbers, the giant footer wordmark), Jost 400-600 (body 17px/1.65, nav, labels), Archivo Black (the giant MAASAI word in the hero).
- One inline SVG sprite: a front-facing warrior, a profile warrior, a bird, a cattail reed and an acacia as <symbol>s, plus the paints the generated art shares (gradients, patterns, blur and bead-shadow filters, an feTurbulence grain).

THE SYSTEM
- Tokens on :root: bg #ead5b8, surface #f2e3cd, ink #1c0b06, ink-soft #5e3d2c, accent #b3261e, hairlines at 18% and 38% ink, the shuka-red band set (red #b3261e, red-ink #f8e9d4, red-soft #f3cdb8, a translucent red-line and red-tex), and the dusk sky #cf7f3c / #e19a57 / #efbd85. A full dark set (bg #140805, ink #f1e2cc, accent #e5574a, red #9c1f18) under prefers-color-scheme and :root[data-theme="dark"].
- Layout is editorial: hairline rules instead of cards, big serif headlines (clamp(52px, 6.6vw, 108px), line-height .94, tracking -.018em), pill buttons, underline links that wipe away on hover.
- Textures cut from the warriors' own geometry, built once in the script as SVG data URIs and used as CSS masks so their colour comes from tokens: --m-shuka (the three folded-cloth panels of the front warrior's shuka, mirrored and tiled), --m-spear (tip, shaft and butt spike, repeated as a fence-like rule), --m-collar (the beaded collar V, as a chevron row). The footer wordmark uses the shuka texture through background-clip:text.

THE HERO
- A fixed 1672x940 stage (the original artboard), aspect-ratio 1672/940, width max(100%, hero height x 1.7787), anchored to the bottom and centred; every part inside is positioned in % of that box. Layers back to front, each with a data-depth for pointer parallax: sky (sun glow, a breathing sun disc, drifting flat clouds), faceted mountains with a haze band, the ground with flat-topped acacias, rocks and tufts, the word MAASAI in Archivo Black (x 600, y 773, textLength 1000, a cream-to-peach gradient, rising in on load), four warriors as buttons, a flapping bird flock drifting west, swaying reeds and seeded spiky grass clumps, then grain.
- Warriors: two front-facing (black and rust shuka, red belt, white edge lines, diamond-tipped spear) and two in profile (long rust robe, ochre sash, bracelets), at left 51.02% / 59.92% / 66.18% / 75.27% of the stage, two of them mirrored by flipping the inner <svg>.
- Copy on the left: a place line with a rule ("Narok, Kajiado and Laikipia, Kenya"), the h1 "Gatherings / that rise." whose two lines slide up out of masks, a lede, a dark pill "Plan your event", an underline link to the season, and a hint "Tap a warrior to see the adumu, the jumping dance" with a small spear icon.
- The adumu: one Web Animations leap shared by the hero warriors, the frieze silhouettes and the enquiry warrior: a crouch (translateY 2%, scaleY .93), a straight-legged spring to about -62% of its height, a short hang, an ease-in fall and a landing squash, with the shadow shrinking. On load the four leap left to right once the word has risen; after that one random warrior leaps every 9-13s while nobody is interacting.

SECTIONS (data-section in order)
1. nav: fixed, transparent over the hero; after 40px it gets a blurred bg and shrinks from 84 to 66px. Logo is three beads plus "Sundune" in the serif. Under 900px a Menu button opens a full-screen shuka-red sheet with huge serif links.
2. hero as above. A fixed spear on the right edge (wide screens) tracks scroll progress.
3. frieze: a shuka-red band where huge serif words (Story, Song, Fire, Land, Welcome) alternate with black warrior silhouettes. It drifts sideways with scroll and the silhouettes leap in a wave whenever you scroll, with a note about the adumu.
4. approach: a manifesto paragraph whose words light up one by one as you read down, then three principles with line icons in a ruled row (Community-led, A fair share, Light on the land).
5. experiences: a list of four big serif rows (Cultural festivals, Leadership retreats, Weddings and ceremonies, Sunset galas) with guest counts. Hovering or scrolling a row swaps a sticky 4:5 frame of generated art and its caption:
   - a beaded collar of nine rings in the six bead colours with a fringe of strands and metal drops, every bead placed by code on leather
   - a dawn ridge over the Laikipia plateau with mist, acacias and three walkers
   - two interlocked beaded bangles on a checked shuka
   - a long gala table in true perspective running down to a fire at dusk, with guests, plates, glasses, hurricane candles, strings of lights on posts, stars, a crescent moon and rising sparks
   On phones each row carries its own copy of the art inline.
6. stats: a serif sentence with counted-up accent numbers (140 gatherings, 9,400 guests, 6 partner communities), then ten bead circles where three fill in red, blue and orange beside "30% of every fee goes straight to the host community's own fund". A spear rule follows.
7. season: the 2027 season as a ruled list of six dates with a serif date, the event, a strand of 12 beads filled for places taken, a status (accent when few places are left) and an Enquire or Join waitlist button that prefills the form.
8. process: three steps whose top rule draws itself left to right and ends in a spearhead.
9. testimonial: a collar-chevron rule, a large serif quote and a named fictional client.
10. cta: on shuka red, "Let's plan something that lasts", a black warrior who leaps when the form is sent, and a local-only form: occasion chips (radio inputs), a guests range with a serif readout, a month select and underline inputs for name and email (placeholder you@company.example). It validates and thanks the person by first name; nothing is sent.
11. footer: four columns, then a giant "Sundune" wordmark filled with the shuka texture, the legal line with the Rive Marketplace credit, and Back to top.

THINGS THAT BREAK
- A <use> inside its own <svg> needs viewBox "0 0 w h". Copying the symbol's own viewBox onto the instance draws the shape outside its frame.
- Scope full-size SVG rules to direct children (.layer > svg) or the nested reed and bird SVGs collapse to zero height. Give the grain SVG an explicit width and height or it renders at 300x150.
- Mirror a warrior by flipping its inner <svg>, never the button, so the leap's translate and transform-origin stay upright.
- The masks only exist after the script sets them; set them first thing so nothing paints blank.
- Clone the experience art for phones after the generated beads, stars and lights are drawn, or the clones are empty.
- The frieze moves the track with transform from a rAF-throttled scroll handler, and its leaps are rate-limited to one wave every 1.5s.

THE FLOOR
- One h1, a main, labelled warrior buttons, a dialog role on the menu sheet with Escape to close and focus moved in and back, role=img with labels on the bead strands and the share beads, role=status on the form message, visible focus rings.
- Under 900px the hero stacks the copy over a window onto the stage centred on the warriors; no horizontal scroll at 390px.
- prefers-reduced-motion stops the flock, sway, sparks, flicker, frieze drift and ambient leaps, shows the counted numbers at once and lights the whole manifesto; a press still plays one leap.
