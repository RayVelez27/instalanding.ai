Build a landing page for Hearthly, a fictional AI home assistant ("Your home, quietly looked after": it watches a home's water, heat, power, air and safety, explains problems in plain English and books vetted local pros at fixed prices), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, all from jsdelivr. Google Fonts: Instrument Sans 400-700 and Instrument Serif (italic, for one word per heading and the signatures). No images: every picture is inline SVG drawn in code.

DESIGN SYSTEM
Warm editorial. Paper #f6f2ea, ink #14130f, deep pine #0f1714, five tones (ember #e8693c, sage #b9d3b0, amber #f2b544, sky #9cc6dc, pine #1f4d43) and a highlighter yellow #f1dd9a that sweeps under links, signatures and the email on hover. Bold Instrument Sans headings with tight tracking and one serif-italic word. A paper grain over everything. Cards often have a folder tab cut into their top edge (clip-path shape() with an arc and a curve, falling back to plain radii). Buttons are ink pills that fill amber from below on hover with a diagonal arrow; icon buttons fill ink in a growing circle.

THE ILLUSTRATIONS (one SVG sprite of symbols)
Glossy, softly lit 3D-style objects on radial-gradient backgrounds with a top highlight, a bottom shadow and grain: an isometric house with a lit window, solar panel, tree and pulsing status light; a brushed-metal smart thermostat reading 68° HEATING with a glowing tick arc; a water drop over ripples; a wall EV charger with a charging ring; a leaf with a dew drop; a security camera with a lens and glowing ring; a chrome wrench; a mesh air purifier; and the Hearthly AI orb (an amber-to-ember sphere with an iridescent ring). Plus a full night scene (a modern house with warm glass walls, slatted timber, a lit pool, trees, a moon and noise clouds) and four illustrated team portraits.

SECTIONS
1. nav: fixed and frosted; logo, five links, search and account icons and a "Get the app" outline pill; it hides on scroll down; under 1000px a burger opens a full-width menu.
2. hero (pinned for about a screen and a half): "Your home, quietly looked after" centred, a spinning circular text badge with a play button on the left, two avatars and a plus on the right, and a five-column collage of tall, floating cards below: the thermostat, a "Filter swap booked" chip card, the house with "All systems healthy", the orb card with a dotted burst above it and an "Explore services" button, the water drop with "Slow leak found", the camera, and a "Saved $46 this month" chip card. Scrolling floods the orb card open (a clip-path inset from its measured box to the full screen) into the night scene while the other columns fly outward and the headline lifts away; then "It notices the drip before the ceiling does. Then it books the plumber." rises in.
3. intro: a short quote with a highlighted signature, and a feature link (38 home services covered).
4. services: four sticky folder cards in the tones (Repairs & Fixes, Seasonal Care, Smart Monitoring, Upgrades & Projects) whose tabs step across the width and stack as you scroll, the one underneath shrinking and dimming; each has a lead, a big number, a button and an illustration with a glass UI card (a diagnosis, an autumn plan, an overnight leak shut-off, three quotes with a rebate).
5. systems: five tall plates in an arch (Heat, Air, Power, Water, Safety with checks per day) whose colour washes open down to the caption and whose tabs pop up, centre first.
6. gallery: "Inside a Hearthly home", three drifting columns of illustrated job cards with a room chip and "Saved $…" captions.
7. process: "From first ping to fixed in 48 hours" with a dark chat mock-up (Hearthly flags a slow water heater, offers a $120 fixed-price flush, the user books it, typing dots), and a four-step rail (Hour 0, 1, 3, 48) whose line fills and dots light as you scroll.
8. stats: two big figures and five horizontal bars by trade that fill on view.
9. team: four illustrated portraits that rise into tabbed frames.
10. testimonials: a big quote that lights word by word on scroll, then a marquee of review cards that pauses on hover and focus.
11. pricing: a Monthly / Yearly toggle and three plans (Essentials $0, Home Plus $14 as the dark card with a "Most homes choose" tab, Concierge $39).
12. faq: five details rows with drawn rules and a plus that turns.
13. contact: "Let your home talk back", the email highlighted on scroll, support details, two buttons, and a tilted phone showing the app (a health score ring, four system tiles, a booked job).
14. footer: a dark panel with an orb, "Give your home a second set of eyes." and app store buttons, then brand, three link columns, a newsletter form, legal links, trust badges and socials.

THINGS THAT BREAK
- Put html.motion on in <head> only when motion is allowed, drop it if GSAP has not loaded in 2.5s, and scope every hidden state under .motion.
- Measure the flood's starting clip from the orb card's real box inside the sticky stage, and invalidate on refresh.
- Size the collage columns from both the width and the viewport height, so it fits one screen.
- Build scroll scenes lazily as they come near; refresh ScrollTrigger once fonts and the page have loaded.
- Clone the marquee's reviews for the loop, aria-hidden and out of the tab order.

THE FLOOR
One h1, a main, a labelled burger with aria-expanded, role="img" and aria-labels on meaningful illustrations, aria-pressed on the billing toggle, a labelled email field with a live message. With motion reduced the page is complete and static. No horizontal scroll at 390px.
