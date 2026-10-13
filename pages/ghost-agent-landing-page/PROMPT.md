Build a single-file HTML landing page for "Haunt", a fictional company whose AI agents work like ghosts: invisible, in the tools a team already uses, noticed only when the work is done. Archivo from Google Fonts (the variable width axis), everything else inline. No images and no libraries: the logo, the favicon and both kinds of ghost are inline SVG or pure CSS. Fictional brand, invented customers and figures, example.com-style contact details.

THE TYPE AND THE PALETTE
Near-black #060409 night, a slightly lifted #0b0711 for alternate sections, warm off-white text. One accent run, cyan #49e7ff to violet #9769ff to pink #ff4fc8, used as a gradient on the key word of the hero, the step numbers and thin rules. Display type is Archivo at font-stretch 125% and weight 900, uppercase, line-height .8, tight negative tracking; labels are the same face at weight 500, small, wide-tracked caps. Every headline ends in a cyan full stop, and one word per headline is outlined (transparent fill, a 1-2px text stroke).

THE HERO
Full height, a vertical gradient from deep teal at the foot through plum to magenta at the top, with a pink radial off the top right. The signature shape: a big rounded bottom-right corner (clamp 64px to 240px), plus an inverse curve under the bottom-left made from two pseudo-elements, one filled with the hero's bottom colour and one with the page colour rounded on its top-left, so the hero pours into the next section. Keep the bottom colour in one custom property both use.
Behind the copy, twenty pixel ghosts float up the hero: each one is a single span built from seven linear-gradient rectangles (head, eyes, mouth, body, a fading tail) all sized off one --size variable, plus-lighter blended, wobbling with a squash-and-stretch keyframe while it rises. Pause them when the hero is off screen and drop them under prefers-reduced-motion.
Copy: "AI agents that work like ghosts." with "ghosts" in the gradient, a lede, a filled pink-to-violet pill and a ghost pill, and a right-aligned meta line in small caps.

THE NAV
Transparent over the hero, dark glass with a hairline after 20px. A gradient ghost logo that bobs and blinks, the wordmark, and a MENU button whose three lines fold into an X. It opens a full-screen takeover: big numbered links on the left, a contact column on the right. Mark it inert while closed, focus the first link on open, close on Escape and on any link, and lock the page scroll while it is open.

THE AGENTS
Four rows, not cards: number, name with a role in cyan small caps, a sentence, and pill tags on the right. Scout researches, Scribe writes, Sentinel watches, Poltergeist does ops. Rows get a faint violet wash on hover.

THE CUSTOMERS
A 12-column grid of four tall cards, 7/5 then 5/7, each a dark radial colour field with the client's initials as a huge outlined monogram, a category line, the name and one result. Cards take a real photo through a custom property (--img). Below, a 2x2 client wall and a placeholder quote.

GHOST SHIFT
The live demo. A 10x10 board of task cells behind the stage, masked to a radial so it fades at the edges, every third cell labelled SCOUT, every fifth SCRIBE, every fifteenth SENTINEL. Three cute SVG ghosts stand in a row, the middle one larger, each with a bobbing body and a shadow ellipse that shrinks as it rises; clone them from one <template>. A pill player underneath: SUMMON AGENTS starts a 480ms beat that clears one task per beat, lights the current cell and three random ones in pink, violet or cyan, hops the matching ghost, flashes its name as an outlined word behind the stage, and updates a status line and a gradient progress bar. The intro fades and blurs away while it runs. After 100 the board refills. The button toggles to SEND THEM HOME.

HOW IT WORKS
Three steps (Summon, Assign, Vanish) with big gradient numbers, and a four-up stats row.

THE CYBER CARDS
The customer cards and the steps tilt toward the pointer in 3D (up to 7 and 10 degrees). Inject the decoration with JS so the markup stays clean: a glare that follows the pointer, three corner glows, four sweeping gradient lines, a scan bar, six drifting particles and four corner brackets that slide outward on hover. Skip the tilt on touch and under reduced motion.

THE CLOSE
A floating ghost, "Let something haunt you.", contact lines, and a demo form: name, work email, company, a custom listbox select for team size (options with a sub-line and a check, full keyboard support: arrows, Home, End, Enter, Escape, type-ahead) and a textarea. Submitting opens a prefilled mailto. Then a thin footer.

THE FLOOR
A skip link, one h1, a main, labels on every field, aria-hidden on all the decorative ghosts and layers, visible cyan focus rings, no horizontal scroll at 390px.
