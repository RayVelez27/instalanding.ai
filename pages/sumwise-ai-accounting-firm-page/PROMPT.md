Brief: Sumwise AI Accounting Firm Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/sumwise-ai-accounting-firm-page
Credit, if you build from it: keep the line above as a comment at the top of the file you produce.

Build a landing page for Sumwise, a fictional AI accounting firm for small business (bookkeeping, taxes, payroll, invoicing, bill pay and cash forecasts, done around the clock by an AI and checked by a licensed CPA), as one HTML file. GSAP 3.13 with ScrollTrigger, and Lenis 1.3, from jsdelivr. Google Sans 400-700 with a metric-matched Arial fallback.

DESIGN SYSTEM
White paper, ink #0b0b0b, orange #fe7141, lilac #cdabfe and sage #d1ddd3, with two greys. Square corners everywhere and hairline rules that draw in from the left. Headings Google Sans 500, very tight (-0.055em). Buttons are ink or orange blocks whose opposite colour opens from the centre on hover, with an arrow that slides or a plus that turns; links fill lilac from the bottom; highlighted words get a coloured marker that wipes in. Small uppercase badges in white.

PICTURES IN CODE (no image files)
One hidden SVG sprite holds every illustration, drawn in greys at 400 x 500 and multiplied over each frame's flat tint (orange, lilac or sage) with a grain overlay, so they print as duotone: receipts under a scanning beam, an invoice that gets a PAID stamp and flies off as a paper plane, a cash forecast with a pulsing dot, a tax return stamped FILED, an AI chip with dots running along its traces, a cheque and a calendar ticked off, a CPA shield with a check that draws in, a calculator on a ledger, a bank wired to cards and phones, a kitchen team marked PAID, a shoebox of receipts being scanned, and seven portraits built from one shared face with different hair, glasses, clothes and props. All animation is SMIL inside the sprite.

STRUCTURE
1. A white top bar with an ink wordmark and orange "AI" tag, an orange "Start free for 30 days" button, four bordered links and an orange scroll progress line; it hides on scroll down. Under 900px a "Menu +" button opens a full ink menu.
2. Hero (sticky stage): an ink cover card in the middle with "Accounting that does it all.", the lead, a live counter of transactions categorized today with a pinging dot, buttons and a big "24/7"; eight tinted illustration tiles with badges scattered around it. On scroll the ink spreads from the card to fill the screen, the tiles fly outward and back, and a statement appears with three highlighted trades (cut hair, bake bread, wire houses) above three principles.
3. Monthly close (lilac): four numbered notes beside a sticky one-page sample report for a bakery (profit, twelve cash bars, tax set aside, a "done for you" tally); as each note passes, its number fills and a sage band slides to the matching part of the report.
4. Services: three full-screen stacked slabs (Books orange, Taxes sage, Payroll lilac) with a giant name, copy, an illustration that resolves from big halftone dots, and an included list; each slab shrinks as the next covers it.
5. Everything: a ruled 4 x 3 grid of twelve jobs with icons and tags (Automated, You approve, CPA-signed) that deal in and fill colour on hover. Ask (orange): sample questions beside an ink chat window that replays a conversation with typing dots, including a mini cash chart card.
6. Switching: the shoebox illustration and three ruled steps. Tax year (ink, pinned): twelve month columns of deadline chips scroll sideways past an orange line, each chip filling with its colour as it crosses.
7. Stories: three alternating rows of an ink portrait panel and a tinted quote. Accountants: four portraits with CPA / CPP / EA badges that settle into the grid. FAQ (sage): six details rows.
8. Pricing: three plans ($49, $199, $499) whose coloured blocks are as tall as their price and rise on scroll. Contact: details and an ink form with coloured checkbox chips and a local-only status. Footer: columns, an orange "24/7" and a giant "Sumwise".

THINGS THAT BREAK
- Queue every motion setup and run them in order after fonts load; if one throws, revert its GSAP context and undo the attribute changes it made.
- Measure tile vectors, report bands and chip positions inside functions and use invalidateOnRefresh.
- Pause the hero tile pans when the stage is off screen, and only stack the service slabs on screens at least 900 x 680.

THE FLOOR
One h1, a main, every section with an id. Illustrations have role="img" and a label; sprites, rules and decorative bands are aria-hidden. The menu button uses aria-expanded, takes focus to Close and Escape closes it. FAQ is details/summary; the form has labels and a status line and sends nothing. Focus rings on everything. prefers-reduced-motion: no smooth scroll, pinning or scrubbing, and the chat shows in full. No horizontal scroll at 390px.
