Build a landing page for tokenhaus, a fictional academy that teaches designers to build design systems with AI (twelve-week live cohorts of twelve people on tokens, components, AI-assisted generation, docs and design-to-code sync, with an AI pair at every step), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, from jsdelivr. Google Fonts: Gabarito 600-900 for display, Instrument Sans 400-600 for text.

DESIGN SYSTEM
Four inks on paper: paper #E7ECF0, ink #212445, amber #FFA802, sky #00A9FF, pink #FF73A5 and light #FDFEFD. Sections are full-bleed blocks of one ink. Display type is Gabarito 900 uppercase, tight. The shape language is a tile: an <i class="t"> square with a ground colour and one shape on top (a quarter circle, a half circle, a quarter ring, a dot or a pill) rotated in quarter turns by a custom property; tiles build the hero, the logo mark, the bullets, the work grid and the contact figure. Big quarter-round corners (radius clamp(96px, 18vw, 280px)) on single corners of photos and cards. Pill buttons whose hover fill grows as a circle from the bottom-left; links with a 3px pill underline that runs out and back in on hover; plus icons that turn 90deg.

ECHO TYPE
data-echo="n" adds n absolutely positioned copies of a word behind it, each pushed down by --eg and outlined in the section colour with an 8-way text-shadow, so the word reads as a stack. With data-echo-inks the copies are pink, amber, light and ink.

PICTURES IN CODE (no image files)
Every picture is an SVG string written into svg[data-art] from a seeded generator: a fan of eight colour-token strips over a grid with swatch cards and an amber sample; a wall of six component cards (a "TOKEN SETS" card, striped, a dot grid "SPACE 04", a big "04", dark mode) taped up; a "BLUE 500" specimen poster; five stacked sheets showing elevation; quarter-round radius curves; a case of amber glyph keys in an ink tray; a roller painting a pink theme; and four tutor portraits built from the same face with different hair, clothes and a halftone quarter circle.

STRUCTURE
1. A paper header that hides on scroll down and returns on scroll up: tile mark and "tokenhaus", five links, "Apply now"; under 1080px an amber round menu button (three pills that become an x) opens a full-screen ink menu.
2. Hero (sticky, so the next section slides over it): a 7 x 4.4 module grid sized from the viewport height: nine quarter-circle tiles (one double-size with an amber eye) on the left, an amber block of three ink pills, a sky block with "AI DESIGN SYSTEMS" echoed twice and the lead and buttons, and an ink band with "ACADEMY" filling the width beside a pink corner tile. As the next section rises the tiles turn, the pills shrink to dots, the echoes spread and the hero darkens.
3. About: a large statement whose lines mask up on scroll, the token fan photo opening from its bottom-left corner, and three principles with tile bullets that turn in.
4. Courses (amber): five ink pill rows that grow from circles to full width on scroll, each opening into an accordion with a description, level, outcome, price ($290-$560) and "Book a place".
5. Manifesto (sky): "SYSTEM" filling the width with four echoes in pink, amber, light and ink; pinned for 250svh they fan downward and settle back, then a line of text fades in.
6. Work: an 11-cell grid of the coded pictures and plain tiles (some with quarter-round corners and captions) that slide in from four sides.
7. Process (pink): a sticky heading beside four steps (Audit, Tokens, Components & AI, Ship) on a rail, with a four-colour disc that rolls down the rail and steps that brighten as they reach it.
8. Tutors (ink): four portraits that wipe in from the left, then the art drops in. Numbers: three stat cards (12, 900+, 94%) that turn up from their corner, and four pill bars of where graduates go.
9. Voices (sky): four sticky quote cards that scale and tilt as the next covers them. Fees: three cards ($480, $860, $1,900) with shape headers, the middle one ink. FAQ (amber): sticky heading, five accordion rows. Contact (ink): "SAY HELLO" echoed, details, and a six-tile figure. Footer with a four-ink strip that grows up.

THINGS THAT BREAK
- Add .motion in the head before first paint unless prefers-reduced-motion, and remove it if GSAP has not arrived after 2.5s.
- Size the hero module from both the viewport height and the container width, and set the sticky top to min(0, innerHeight - hero height) so a tall hero still scrolls into view.
- Measure pill widths inside the clip-path functions and use invalidateOnRefresh, and refresh ScrollTrigger when an accordion opens.
- Keep the echo copies aria-hidden and unselectable, and pause the hero loops once it is covered.

THE FLOOR
One h1 (the two hero lines), a main, every section with an id. Every coded picture has role="img" and a label; decorative tiles are aria-hidden. The menu button uses aria-expanded and swaps its label; Escape closes it. Accordions are buttons with aria-expanded. Focus rings on everything. prefers-reduced-motion: no sticky cover, scrubbing or loops. No horizontal scroll at 390px.
