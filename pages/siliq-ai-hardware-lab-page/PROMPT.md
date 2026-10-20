Build a landing page for Siliq, a fictional small-batch AI hardware lab and hardware school on "Foundry Row" (NPU sticks, RISC-V dev boards, tensor cards, inference chips; classes at a big workbench; a hardware leasing club), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3, all from jsdelivr. Google Fonts: Climate Crisis (display), Google Sans 400-700 (text), Playpen Sans 600-800 (handwritten notes). No images: every product, the lab and four portraits are inline SVG symbols in one sprite at the top of <body>, drawn as glossy sticker illustrations, and used with <use href>.

DESIGN SYSTEM
A playful bento of big rounded tiles on a pale sage ground. Tokens: ground #e4e8e3, paper #ffffff, sky #7cc4ea, honey #ffbf3c, tangerine #f47a3c, leaf #0a5c46 (the primary button), ink #0a1317. .tone-* classes set a tile's background, its blob and its little spark marks. Display type is Climate Crisis in caps, fitted to its container from its character count (--len) with container units. Tiles have a 28-36px radius; each product sits on an organic blob shape; three-stroke "spark" doodles and Playpen Sans notes with a dashed hand-drawn arrow ("Join in!") add the hand. Buttons are ink or leaf pills with a white secondary; one spring ease for every pop.

SECTIONS
1. nav: the logo (an S on a honey square plus the wordmark) in a white pill at left; links (Lineup, School, Compute club, Visit) and an Order button in a white pill at right. Under 900px a menu button opens a full sheet.
2. hero, a bento board: a big honey tile with "Built today!" as one fitted headline, a line and two buttons, a large chip illustration on an orange blob with a leaf "from $24" price badge; a tall white Edge NPU tile ($129, a blob and a spark); an orange "(4.8) stars from 1,200 builders" tile; a "Top picks" tile with four round product thumbnails; a sky "Workshops" tile with a robot arm and a handwritten Join in!. On scroll the board breaks apart, tiles flying off in their own directions, while a honey flood grows out of the main tile to fill the screen.
3. story: a quote ("We solder by hand, test in small batches...") split into lines that rise in on scroll, with stickers between the words, and three stats (2015, 36 modules, 48 h burn-in).
4. lineup: "On the bench": six product cards (NPU stick $89, Pocket board $59, Tensor card $1,299, Inference chip $24, Memory kit $210, Cooling kit $45), each a tone tile with the illustration popping in.
5. school: classes as date tiles (day and month, title, length and seats, price) with a private-session note and a Book a seat button.
6. process: "From wafer to rack", a timeline of four times (5:00 reflow on, 7:30 bench tested, 9:00 bikes out, 12:00 batch closed) that fills as you scroll.
7. gallery: "A peek inside", a strip of thumbnails that unfolds into a full grid of lab scenes on scroll.
8. team: four engineers with SVG portraits on coloured blobs, a role and a one-line joke each.
9. reviews: the 4.8 rating and an endless marquee of six forum quotes in coloured bubbles, paused on hover or focus.
10. pricing: "Compute club" with a Monthly/Yearly switch over three plans (Hobby node $49, Lab cluster $199 marked Most loved, Office rack $899) that fan out on view.
11. faq: details rows. 12. contact: hours, an address on Foundry Row and an order form. 13. footer: link cells, a Pre-order tile, the wordmark huge with a squash-and-stretch on view, and a legal line saying the business is fictional.

THINGS THAT BREAK
- Put html.motion on in <head> only when motion is allowed, and take it off if GSAP has not arrived in 2.5s; scope every hidden-until-animated state under .motion.
- Wait for document.fonts.ready before SplitText and before measuring fitted text, then refresh ScrollTrigger.
- The flood must start from the main tile's own box, measured on refresh; aim each flying tile from the board centre with function-based values and invalidateOnRefresh.
- The portraits are big SVG; keep only the ones used.

THE FLOOR
One h1, a main, a labelled menu button with aria-expanded, role="img" with labels on product pictures and aria-hidden decoration, aria-hidden cloned marquee items, a form that confirms in place, visible focus rings. With motion reduced the page is complete and static. Under 700px the bento becomes one column with paired small tiles. No horizontal scroll at 390px.
