Build a single-file HTML landing page for "Halcyra", a fictional AI agent platform ("Intelligence, orchestrated at scale"). Outfit from Google Fonts is the only font (500 for headlines, 200 for the light words set against them). No libraries, no images: every illustration is inline SVG built from one shared sprite. Fictional customers, figures and testimonial.

THE PALETTE
Near-black #06060a with glass surfaces (white at 3-5.5%) and hairlines (white at 8% and 14%). Text #f4f4f7, muted #9a9aab, dim #5f5f70. One five-stop spectrum carries the brand: lime #9be15d, teal #3fd1a8, sky #4cc4e8, iris #7f9cff, violet #a78bfa, used as --grad left to right for gradient text (slowly shimmering), pill tags and the primary button (whose gradient slides on hover). Headlines are tight (letter-spacing -.04em) with one phrase in each set in Outfit 200 and gradient text. Section kickers are uppercase with a small faceted diamond before them, in sky, or in sun, rose or mint variants for later sections. Behind the page sit fixed blurred colour orbs, a 72px grid masked to the top of the viewport and a fine SVG grain.

THE SPRITE
A hidden SVG holds the facet gradients and four low-poly symbols reused everywhere:
- #gem: a crystal in ice blues.
- #gem-g: the same crystal in greens.
- #orb: a geodesic hex ball in sunset oranges and magentas.
- #cube: an isometric data cube in aurora pinks with a few data marks.
Plus #cdot, a white callout dot with a lime centre. Callouts are always a pulsing lime dot, a thin white leader line with one elbow, and widely tracked uppercase labels.

THE HERO
A fixed pill nav (glass, blurred, darker once scrolled) with the logo (a gradient diamond with a dark inset), five links and a light "Start building" pill. Left: a "New · Agents 3.0 is live" eyebrow, the headline, a lede, and an email capture pill whose placeholder types and deletes three example addresses. It turns lime when valid, shakes red when not, and swaps to a success pill on submit. Below it, three ticked notes. Right: a 4x4 mosaic of tiles, each a different quarter-round shape (mixed border radii). They are glossy radial spheres in the five brand colours alternating with dark glass tiles holding an icon, an equaliser, a sparkline, a "tokens/s 18.4k" stat and a bobbing #orb. Tiles scale in one after another. Two glass stat cards float over the corners, and a "LIVE INFERENCE · EDGE" callout hangs below. Crystals drift around the hero. Then a marquee of fictional customer wordmarks.

THE MIDDLE
- How it works: three cards whose art panels are small SVG scenes of the sprite symbols bobbing, with callout labels.
- The platform: a horizontal slider of six cards with buttons, mouse drag with snap, and a gradient progress bar. Each card has a spinning conic-gradient border, pointer tilt and a spotlight, and a live visual: a chat exchange with typing dots, a node graph with flowing dashes, growing bars, shield rings, a typed SDK snippet, and an area chart.
- The iceberg: one faceted SVG iceberg in a framed panel, with five callouts down its length (Agents & UX, Workflows, Memory & evals, Models & runtime, GPUs & infra). Four stage buttons (Self-hosted, GPU cloud, Model APIs, Halcyra) move the waterline: the sky and the water tint translate together with a 1.5s ease. Each callout above the line reads "YOU MANAGE"; below, it dims and reads "HANDLED BY HALCYRA". The header counts the layers you still manage. It cycles on its own while on screen until someone clicks a stage.
- A performance bento: a 142ms p50 headline with comparison bars that fill on view, and count-up stats.
- Use-case buttons that swap the copy, three metrics and the art: the big symbol, its glow colour and the three callout labels change per team.
- An integrations orbit: dashed rings turning in opposite directions, flowing spokes and eight labelled nodes around a central crystal.
- A testimonial, three pricing plans (the featured one with a spinning conic border) and a FAQ with a sticky head and native details.

THE FINALE
A footer that turns to night: twinkling stars and an occasional shooting star, "The future of work runs on Halcyra.", a second email pill and a proof row. Then a horizon of three seeded low-poly terrain bands generated in JS from the sprite's gradients. The far and mid bands parallax, and a faceted #orb sun with a tilted ring rises out of them on scroll, with slowly turning conic rays behind it. Two callouts sit on the ridges: 4,000+ teams, 4.8B runs. Then link columns, a status pill and a giant outlined HALCYRA wordmark lit by a gradient spotlight that sweeps on its own and follows the pointer.

THE FLOOR
One h1, a main, data-section on every region, aria-hidden on every decorative SVG (the iceberg keeps role="img" and a label), stage and use-case buttons as toggle buttons with aria-pressed, visible focus everywhere, no horizontal scroll at 390px. Under prefers-reduced-motion, every animation runs once to its end state, the iceberg does not cycle and the placeholder does not type.
