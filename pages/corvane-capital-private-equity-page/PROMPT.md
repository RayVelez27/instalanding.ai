Build a landing page for Corvane Capital, a fictional New York private equity firm that partners with founder-led software companies ($8.4B under management, 47 platforms since 2012, Fund IV of $2.8B now investing), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, all from jsdelivr. Google Fonts: Instrument Serif (with italic) for display, Inter Tight 300-600 for text, JetBrains Mono 400-500 for labels.

DESIGN SYSTEM
Near-black ink #0A0B0D with a raised #111317, ivory paper #EEEAE1 and a warmer bone #E3DDD1, gold #C6A15B with a highlight #E6CC93, a champagne field #BFA06A, muted grey #7F838A. Each section declares data-tone (dark, ivory, bone or gold), and the tone re-points three variables: the rule colour, the soft text colour and the accent. Instrument Serif 400 at -0.035em tracking and line-height .84 for the giants; h2s end on an italic, gold (or ink-gold on paper) phrase. Mono labels at 11px, uppercase, wide tracking. Radius 2px everywhere. A 6% SVG film grain fixed over the page.

THE RULED GRID
Every section is a .sheet that draws its own ruled field: a ::before inset by the page gutter with 1px vertical rules at 0, 25, 50, 75 and 100% (0, 50 and 100% under 760px). Content sits on a matching four-column grid (two columns on phones) with an inner cell padding, so every heading, figure and paragraph starts on a rule. The header is a strip of the same grid.

PICTURES IN CODE (no image files)
- Strategy: five SVG plates at 400 × 260 on #0E1013 with a faint grid and two mono corner labels: a stack of six floating isometric layers (the top one gold) for vertical software, a jittered 9 × 5 node network with gold dashes running along random edges for infrastructure, six dashed rings turning at different speeds with a radar sweep and a hexagon for security, seven settlement curves funnelling through a gold node with dots riding them (animateMotion) for financial rails, and a pulsing dot field under a gold signal line for data and AI.
- About: a 600 × 380 chart, platform revenue index (1.19^t) against a dimmer public SaaS index (1.088^t) over seven years, the gold line drawing in and the area fading in when it enters view, an "ENTRY 1.0x" and a "PLATFORM 3.3x" callout.
- Team: eight portraits drawn from the name: a seeded PRNG (mulberry32 seeded by an FNV hash of the name) jitters a dark silhouette (head, ears, neck, shoulders, faint lapels) on a gold radial glow with scanlines and five orbit arcs (one gold, ending in a dot) that turn on hover; the first name picks a hair shape (long, bob, bun, crop, short).
- Offices: five tiles: a rotated street grid with a gold avenue (New York), concentric bay ellipses (San Francisco), scattered island circles (Stockholm), bent meridians with a gold prime meridian (London), a dot field swelling at the centre (Singapore), each with its city, latitude and a live clock for that time zone (Intl.DateTimeFormat, every second).
- Portfolio glyphs (one of four marks, seeded by company name) and three insight thumbnails (a compounding bar chart, nested frames, scattered circles).
- Hero: a canvas of 46 ridgelines, each a row of summed sines lifted by a Gaussian envelope centred on the window, filled with ink beneath so nearer ridges hide farther ones, every eleventh line gold; it animates only while the hero is visible, at DPR at most 1.75.

STRUCTURE
1. A fixed header: the mark (three bars, one gold; they fan to an asterisk and back on a loop), "Corvane", a three-line mono tagline, six links, "LP portal" and a gold Contact block; under 900px a plus button opens a full-screen menu. The header recolours to the tone of the section under it.
2. Hero: a giant "Compounding" with a gold italic d, three mono stats (AUM, platforms, since), the ridgeline window in the right column with HUD corners ("Fund IV — investing", coordinates), the lede and two actions, and a "$2.8B" Fund IV figure.
3. About: "Operators first. Investors by discipline." with the chart and a row of four counting facts (14 years, $8.4B, 47, 3.1x) under rules that draw in.
4. Strategy: "Five theses, one discipline"; on wide screens a sticky stage on the left shows the plate for the thesis in the middle of the viewport, each new plate wiping in from below (or above when scrolling up) with a 01 / 05 counter; on narrow screens each plate sits in its row.
5. Principles: a champagne field that grows from one grid cell to the full screen, then pins. A mark of six strokes starts as a fan; per principle one stroke swings upright into a row, the previous principle clips up and out, the next rises in, and a progress bar fills.
6. Process: "The first hundred days", four steps on a line that fills as you scroll, each node lighting as it passes.
7. People (eight portraits that open like a shutter, staggered by column), Portfolio (a pull quote whose words brighten as you read and a marquee of seven companies that pauses on hover and focus and off screen), Offices (a collage moving at five parallax depths), Coverage (six huge sector names drifting left and right in alternation), Criteria (four bars that fill to their value with mono figures).
8. Track record: four funds in a ledger with a Gross / Net switch that swaps every IRR and multiple from data attributes with a rise; rows open from below one after another; a plain-words disclaimer that the figures are illustrative.
9. FAQ (details elements whose top rules draw in), Insights (three posts with wiping thumbnails), Contact: "Every lasting partnership starts with a conversation." with details and a form (I am a founder / LP / advisor, name, email, company, ARR, message) that thanks inline and sends nothing.
10. Footer: a lead line, three link columns, a back-to-top button, then a giant "Corvane" wordmark sized to the full width whose letters rise from random depths as it scrolls in while the mark's strokes fall into line, and a base row noting the firm is fictional.

THINGS THAT BREAK
- The hero is one pinned stage: measure the window's box inside the pin, clip the full-bleed stage to that box, and scrub the clip-path to inset(0) over the first 62% while the topo's centre, spread and amplitude ease from the window's geometry to full-screen values. Recompute on refresh (onRefreshInit, function values) or a resize leaves the clip at stale pixels.
- Size the giants from their container: container-type inline-size and font-size min(100cqi / (--len × .47), 36svh), with --len the character count; the footer word subtracts its padding and the mark's width.
- Add a .motion class in the head before first paint unless prefers-reduced-motion, and drop it if GSAP has not arrived after 2.5s. Pinned hero and principles and the sticky strategy stage live behind .motion and an .is-live class set by script, so the page still reads as plain sections without GSAP.
- Run SplitText after document.fonts.ready and revert line splits when they finish, or the lines break wrongly after a resize.
- Queue every ScrollTrigger setup and spread the queue across frames (8ms budget), then refresh once.
- The marquee clones its cards until the track overflows by one full span; mark the clones aria-hidden.

THE FLOOR
One h1, a main, every section with an id. The menu button has aria-expanded and a swapping label; Escape closes it. The gross / net switch is a group of buttons with aria-pressed. Decorative SVGs and the canvas are aria-hidden. A custom difference-blend cursor only on fine pointers. prefers-reduced-motion: no pinning, no marquee, no topo animation, no cursor. No horizontal scroll at 390px.
