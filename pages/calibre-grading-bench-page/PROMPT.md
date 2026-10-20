Build a dark landing page for Calibre, a fictional evaluation bench for AI answers ("Measure every answer before it ships"), as one HTML file with no libraries and no images. The hero is a centred headline over a tilted glass grading bench, lit from behind by a glowing planet horizon. The bench reads a model's answer claim by claim, highlights each claim in its verdict colour and swings a needle to the score.

FONTS (Google Fonts)
Archivo with the width axis (wdth 62-125, wght 100-900) for display: uppercase, weight 900, font-stretch 110%, letter-spacing -0.03em, line-height 0.92. Source Serif 4 for the answer text and italics, JetBrains Mono 400/500/700 for labels, chips and terminals.

TOKENS
One token set. Surfaces: void #08090b, alu #1c1e23 (hi #26292e, lo #15161a), well #0e0f12, hairlines rgba(255,255,255,.07/.12). Exactly three text greys: #eceef1, #a8aeb7, #7d838d. Amber #ff9426 (hi #ffb562, lo #e5750e). A verdict system, one hue per verdict, each with a lamp tone and a highlighter tone: green #4ad87a, yellow #ffd34d, orange #ff7d3a, red #ff4f44; on the bench and the verdict cards the highlighter tones are vivid and flat (#1d7a3b, #9c6c0e, #b0481a, #a8202b). A 4px spacing scale (4, 8, 12, 16, 24, 32, 48, 64, 96), three radii (16, 10, 4) and one ease, cubic-bezier(.2,.8,.2,1). One label style: mono 11px, letter-spacing .16em, uppercase, the third grey. A "gold" text gradient (#e6c43e → #ffbb30 → #ffa22a → #ff8c1e, background-clip text) marks one phrase per headline.

MATERIALS
- Glass: a 20px-radius card with a dark vertical gradient (rgba(34,36,42,.82) → rgba(14,15,18,.92)), a 1px inner hairline, a brighter 1px top edge and a deep drop shadow. Every card on the page uses it; on hover it lifts 4px and gains a glow in its own colour.
- Lamps: 8px dots, dark when off; on, they fill with their colour and glow.
- Icon tiles: 52px rounded squares on near-black with a radial glow in their colour and a drop-shadowed icon.
- Buttons: amber (a gradient with a 2px dark-orange base and an amber glow), secondary metal, and ghost glass with a backdrop blur. They lift 1px on hover.
- Pills: 38px rounded capsules with a lamp and mono uppercase text, used as section eyebrows.
- The highlighter means a verdict and appears nowhere else: a mark's ::before sits behind the text, coloured only through --c, and draws in by scaling X from the left.

SECTIONS
1. nav: sticky, blurred, a three-column grid: an amber gauge-glyph logo with CALIBRE in wide, tracked capitals; four links (Verdicts, How it works, Numbers, FAQ); Sign in (ghost) and Get a bench (amber).
2. hero, centred: a pill ("Eval bench for AI answers"), the h1 MEASURE EVERY ANSWER / BEFORE IT SHIPS. with "every answer" in gold, a lede with one italic serif phrase, two large buttons and three amber-icon trust notes. In the empty space either side of that copy, four floating glass "source" cards (a PDF, a web page, a database, a file), two a side and staggered (one beside the headline, one beside the lede), tilted in 3D toward the centre and drifting. Below, the stage: a 1380px planet (a near-black circle whose top rim burns amber through stacked inset and outer shadows), two lens flares, twinkling sparks, two layers of SVG rock terrain with an amber rim light (one behind the bench, one in front), and the bench tilted back 9deg on rotateX with a stacked glass layer behind it and an amber rim light along its lower edge. Under it a strip of eight invented customer logos.
3. verdicts: four glass cards, one per verdict (Grounded 1.00, Reworded 0.85, Stretched 0.35, Unsupported 0.00): an icon tile, the weight, a lit lamp tag, a title, a line of explanation and an example phrase whose mark draws in on view. Each card has a lit top edge and a glow in its verdict colour. Under them the formula: (1 + 0.85 + 0.35 + 1 + 0) ÷ 5 = 64.
4. how-it-works: three glass steps (Split, Check, Gate) joined by an amber pipeline line with a pulse travelling along it; each has an icon tile, a big outlined number, a title and a terminal well showing the command and result (5 claims; 2 grounded · 1 reworded · 1 stretched · 1 unsupported; 64 · blocked).
5. stats: one glass panel with a lit top edge and four figures (48M claims, 1 in 9 in amber, 210 ms, Zero) in silver-gradient display type, the numbers rolling up on view.
6. faq: a sticky side column (the heading and a "Still unsure?" contact card) beside five glass <details>; the open one gets an amber ring and its plus turns into an amber cross.
7. cta: a glass finale with a planet rising from the bottom, a glow floor, the headline PUT A NEEDLE ON / EVERY ANSWER. in gold, a lede, a glass email form with an amber button and three green-checked notes.
8. footer: a brand column with an "All benches operational" status, three link columns, the word CALIBRE huge in outlined, amber-tinted type, and a line saying the product and every number are fictional.

THE BENCH (the hero instrument)
- A top row: "// Run 0418 · support-bot" and a status (a lamp and "Scanning", pulsing while busy, green "Completed 4.6s" when done) with a replay icon button.
- Two cards side by side: the model answer (a serif paragraph of five claims, each a mark with a verdict and a source note in data attributes: two grounded, one reworded, one stretched, one unsupported) and a gauge: an SVG arc from -120° to +120° with a red → orange → yellow → green gradient stroke and a soft glow, 21 ticks placed with trigonometry (every fifth longer), an amber needle rotated by calc(-120deg + var(--a) * 240deg), the score in large display numerals over the hub, "Grounding" and a gate pill ("Gate ≥ 80 · passed/blocked").
- Four verdict chips with lamps and counts, and a source bar: a glowing tile, the checked span for the selected claim (its lamp in the verdict colour) and a next arrow that steps through the claims.
- A run: clear the marks and counts, then for each claim move an amber scanline to its line, wait about half a second, draw its mark, light its lamp, bump its count and set the needle's target to the running weighted score. Finish with the gate in green or red and the elapsed time. It runs once after load and replays on the button.
- The needle is a damped spring integrated per frame (stiffness 120, damping 14) toward the target, so it overshoots and settles; the score eases toward it. Stop the loop once it settles.

THINGS THAT BREAK
- A mark is inline-block, so a long claim cannot wrap. Split each claim into one span per word in script (each word its own ::before reaching over the following space, the last one not), staggering the draw by 40ms per word.
- Measure the scanline position from the claim's offset each run, since the text reflows by width.
- Keep the numbers on the page in agreement with the bench: 64, 2 / 1 / 1 / 1, gate 80.
- The planet and terrain are far wider than a phone: clip them inside the stage (clip-path on the stage, overflow hidden on the hero) and hide the floating source cards under 1280px, where the copy leaves no room beside it.

THE FLOOR
One h1, a main, labelled icon buttons, aria-hidden decoration, a live region on the source panel, visible amber focus rings, real labels on the form. Under prefers-reduced-motion the bench renders already graded with no scan and all animation is off. Below 1040px the verdicts and stats go to two columns and the FAQ stacks; below 860px the nav links hide, the bench untilts and stacks; below 560px everything is one column. No horizontal scroll at 390px.
