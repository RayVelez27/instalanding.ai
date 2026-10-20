Build a landing page for Halden, a fictional clinical equipment service (patient monitors, infusion pumps, ultrasound, ECG) in Seattle, as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3 for smooth scroll, all from jsdelivr. Google Fonts: Geist 300-600, Geist Mono 400/500, Instrument Serif (italic). Every device, monitor trace and "photo" is inline SVG; no images.

DESIGN SYSTEM
Use CSS cascade layers: tokens, base, atoms, layout, sections, scenes. Colours: ink #090c0e, paper #f3f5f6, light grey #d3d9dc, mid greys #8a959b and #58626a, line #1a2329, soft panel #e2e7ea, one cobalt signal #2b46ff, and a monitor green #3fd99a kept for live readouts only. Sections alternate dark (ink with a 7% fractal-noise SVG grain) and paper. Type atoms: a huge display (clamp 56-152px, weight 300, letter-spacing -0.05em, line-height 0.92), a large text (26-40px, weight 350), mono labels (11.5px, letter-spacing .08em, uppercase), and a justified "spread" eyebrow whose words are pushed to both edges. Italic Instrument Serif marks one phrase per headline. Pill buttons whose cobalt fill wipes in from the left on hover and whose trailing pill-dash slides; dashed underline links whose dashes flow on hover. A 4-column grid with a fluid gutter (16-28px), 2 columns under 48em.

SECTIONS
1. nav: a fixed blurred ink bar 60px high; brand mark of three pills; a "Bench open · Critical line 24/7" status with a pulsing green dot (only above 80em, or it collides with the links); four mono links; Book service. It hides on scroll down and returns on scroll up. Under 64em a full-screen menu replaces the links.
2. hero (sticky, 100svh): the word HALDEN drawn as a dot-matrix: each letter a 5 x 7 grid of rounded pill rows (grid-column spans), sized from the container and viewport height (--u), with rows that pulse sideways on a staggered loop. Below it the h1 ("Clinical equipment service, performed in view and documented to the line." with the last phrase in serif), a lead, actions, an animated ECG trace (three stacked paths: a faint base, a 35% tail and a glowing head, animated with stroke-dashoffset) and an address bar. Scrolling splits the wordmark: odd rows slide one way, even the other, stretching and thickening, then a paper flood grows out from the wordmark's box to fill the screen.
3. A paper second half: the stair headline "Most failing devices are fixable." with each word in its own grid cell, stepping down and right, the last word in a cobalt selection highlight, and three device illustrations (a bedside monitor with an NIBP alarm, an opened infusion pump, an ultrasound probe) placed in the stair's empty cells.
4. diagnosis (ink): "Fifteen minutes, free, on record." and a board of twelve checks (earth leakage, protective earth, ECG, SpO2, NIBP, battery, alarms, display, power, network, firmware, housing), each with a result; two are faults shown longer and in cobalt. On wide, tall screens the board pins and a cobalt band scans down it as you scroll, flipping each row from "Queued" to its result, then a summary with the quote fades in.
5. prices (paper): a rate card table grouped by device family with a bench-time bar per row (width from minutes) and a price.
6. bench (ink): "Done in plain sight." over one wide illustration cut into four vertical strips that settle into alignment as you scroll, and three short columns.
7. parts (paper): a three-grade comparison table (OEM, certified, rebuilt).
8. refurb (ink): "Second shift", a horizontally scrolling pinned shelf of five rebuilt devices with grade, price and Reserve.
9. fleet (paper): a weekly route board, one row per weekday with pickup windows as bars on an 08-18 axis; a cobalt time cursor sweeps across with scroll, colouring the window it is in.
10. mailin (ink): four mail-in steps with growing dashes. 11. reviews (paper): three large quotes where a cobalt box reads them word by word as you scroll. 12. faq (ink): details/summary with a pill marker that shrinks when open. 13. visit (paper): the words "Come to the bench." grow from small to full size into a staggered layout; facts, a photo, and a white booking form with inline validation. 14. footer with the ECG again and a fictional-business legal line.

MOTION RULES
Queue every scene so it runs after fonts load (SplitText and the stair measurements depend on them), lazily as its section nears, and revert it cleanly if it throws. Wrap each in gsap.matchMedia('(prefers-reduced-motion: no-preference)'). Drive Lenis from the GSAP ticker and feed its scroll to ScrollTrigger.update, with lagSmoothing(0).

THINGS THAT BREAK
- Measure positions (board rows, stair offsets, word boxes) inside onRefresh, never once at load: fonts and the sticky opening change them.
- The flood's clip-path must start at the wordmark's own box, computed from both rects on each refresh, or it jumps.
- The status line in the nav needs about 1280px beside the links; hide it below that.
- Keep the opening sticky stage and the flood inside one section, and reset the split rows at the end of the timeline so scrolling back up rebuilds the wordmark.

THE FLOOR
A skip link, one h1, a main, real tables with captions, labelled form fields, aria-hidden on decoration, visible focus rings. With motion reduced the page is complete and static. No horizontal scroll at 390px.
