Build a landing page for Somatic, a fictional AI wellness companion ("the AI that listens to your body": it reads sleep, heart rhythm, breath and movement from the ring, watch or phone you already own and turns them into one calm plan for today), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, all from jsdelivr. Google Fonts: Anybody (wdth 50-150, 100-900) at 58% width and weight 900 for display words, Bodoni Moda italic for the one emphasised word per heading, Space Grotesk 300-700 for text, Space Mono for labels.

DESIGN SYSTEM
Acid #D4FF3F, ink #0D0C0B, paper #ECEBE4, moss #1F2B24 and coral #FF5E3A, with a periwinkle #7AA0FF only inside the art. Sections alternate moss, acid, ink and paper at full bleed, no rounded corners anywhere: the shape language is the diamond (a 45deg square) for bullets, ticker separators, step marks, the menu icon and every reveal. Display words in Anybody 900 uppercase, condensed and set very tight; each h2 ends on a Bodoni italic word in coral or paper. Buttons are ink or acid rectangles whose hover fills from the centre with a rotated square; links have a block highlight that rises from a thin underline. A 22% SVG noise grain over the hero.

STRETCHED TYPE
- Rows of display type fill their container exactly: each .row is var(--r) x 100cqw tall, and its word's font-size is 100cqw / (--len x --k), then scaleY stretches it to the row height using the font's cap-height ratio --cap.
- After fonts load, measure the real cap height of Anybody on a canvas (actualBoundingBoxAscent at 100px) and each word's real width, and write --cap and --k back, so the words land edge to edge in any browser. --len (letter count) on each word is the fallback before the script runs.

PICTURES IN CODE (no image files)
- Hero: a canvas with a dark moss gradient, a coral glow bottom-left and a periwinkle glow top-right, 20 drifting contour rings, and a Fibonacci point sphere of 1,300 points that breathes, warps with two sines and turns toward the pointer; near points are acid and larger, far points paper and faint. The same frame is copied into a second canvas clipped to a diamond in the centre of the screen. Cap DPR at 1.5, pause off screen, one still frame under reduced motion.
- Program posters in SVG: a crescent moon over twinkling stars and sleep-stage bars (Sleep), pulsing concentric rings (Breathe), a filled HRV wave with a coral marker (Recover), a three-colour macro ring (Fuel), an orbiting focus dot (Focus).
- An ECG line with a coral scan running along it, a sleep hypnogram of coloured blocks on four levels, three topographic contour fields from perturbed circles, a scatter of 30 days of HRV dots with a trend line, a conic readiness ring, and a CSS breathing diamond that cycles Inhale, Hold, Exhale over 14 seconds.
- Team portraits are gradient fields with a diamond frame and the person's initials in Bodoni italic, blended with overlay.

STRUCTURE
1. A fixed acid header: wordmark "SOMATIC" with an italic "ai", five mono links, a "Start free" button; it hides on scroll down. Under 960px a Menu button with a turning diamond opens a full-screen acid menu with huge links.
2. Hero (moss, full height): a ticker, "SOMATIC" and "SIGNALS" stretched across the width, a reverse ticker, the two words again; the orb canvas behind, the diamond window on top. Pinned for 110% of a screen: the diamond grows until it covers the screen, the photo settles from 1.08 to 1, and the type rows stretch taller and drift up. The letters ripple in a slow scaleY wave.
3. About (acid): a ticker of biomarkers, a large lead paragraph whose lines rise in from masks, a 3:4 readiness figure (contours, a ring at 86, time 06:42) with parallax, three facts (24/7, 09, 4 min) and a button.
4. Programs (ink): pinned and scrolled sideways: an intro ("Pick your practice") and five tall posters, each with the program name stretched across its top, a mono meta strip between acid rules and a line of text; the art and the names drift in parallax as they cross.
5. Values (moss): four giant words (Private, Evidence, No guilt, Human loop), each letter stretching from flat to full height and beyond as it scrolls past, with a paragraph under each.
6. Your day (paper): five rows (Wake, Work, Pause, Move, Rest) with a giant day word, title and line, time, program and duration; each row is swept by an acid bar that wipes in and out before its content appears, and fills acid on hover.
7. Team (ink): four portraits that open from a point into a diamond and then to the full frame. Voices (acid): a featured quote whose words brighten as you scroll, a marquee of six ink quote cards that pauses on hover and focus, and a note that the testimonials are samples.
8. First week (paper): four steps on a rising staircase joined by a drawn line. Signals (ink with an acid frame): a bento of six tiles (live ECG, breathing diamond, last night's hypnogram, stress landscape, HRV dots, readiness ring) that tilt up into place.
9. The year so far (moss): three stats and a bar chart of nine months that grows in. Pricing (paper): three plans at $0, $12 and $29, the middle one acid, rising at different speeds. FAQ (acid): a sticky heading beside five accordion rows with a diamond plus that turns into an X. Contact (moss): drifting blurred colour orbs and contours behind "Begin gently", a waitlist card that thanks inline and sends nothing, and "LISTEN CLOSER" stretched across the bottom. Footer: a ticker, the wordmark, links and a medical disclaimer.

THINGS THAT BREAK
- Add a .motion class in the head before first paint unless prefers-reduced-motion, and drop it if GSAP has not loaded after 2.5s; pins, the sideways rail and every hidden-until-revealed state live behind .motion.
- The program rail's length is the track's scrollWidth minus the viewport: measure it on refreshInit with invalidateOnRefresh, or the pin ends early after a resize.
- The diamond window grows a custom property (--dd) inside clip-path; tween it with function values so it is recomputed on resize.
- Fit the stretched type after document.fonts.ready and only then create the ScrollTriggers, or every pin starts at the wrong place.
- Tickers clone their items enough times to cover the width, loop by exactly one period, play only while visible, and speed up with scroll velocity before easing back.
- Run every GSAP setup from a queue, one per task, so the first scroll does not stall.

THE FLOOR
One h1, a main, every section with an id. Decorative SVG and canvases are aria-hidden; the readiness figure has a role="img" label; cloned ticker items are aria-hidden and untabbable. The menu uses aria-expanded and swaps its label; Escape closes it. The FAQ buttons control their regions with aria-controls. Focus rings everywhere. The form status is a live region. A footer line says the product is a wellness tool that does not diagnose. prefers-reduced-motion: no pinning, no marquee, the orb drawn once. No horizontal scroll at 390px.
