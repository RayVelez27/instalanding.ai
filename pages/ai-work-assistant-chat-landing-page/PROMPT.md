Build a single-file HTML landing page for "Tidewell", a fictional AI assistant for work that reads your inbox, calendar and docs, then summarizes, drafts and schedules. The look is quiet, light and pastel: a near-black ink on white, Geist type set tight, soft blue and violet gradients, a faint page-wide grid that lights up around the cursor, two blurred glows behind a centred hero, and a real, scripted chat as the centrepiece. Full dark theme included. Fictional brand, investor, customers, inbox senders and testimonials, labelled as such in the footer.

STACK
- No libraries. Google Fonts: Geist 400-700 for everything, Geist Mono for times, step numbers and keycaps.
- One inline script. Avatars are gradients, icons are inline 24px stroke SVGs, integration marks are letters on tints.

THE SYSTEM
- Tokens on :root: bg #ffffff, bg-soft #f7f7f8, surface #ffffff, ink #0f1115, ink-2 #4f535b, ink-3 #9b9b9b, line #ececee, line-strong #e2e2e5, badge #f5f5f5, blue-1 #dbe5ff / blue-2 #cbdaff / blue-ink #1d6ad9, violet-1 #dfceff / violet-2 #d4bbff / violet-ink #422c6f, mint-1 #d3f5e4 / mint-ink #136c45, amber #d97706 / amber-soft #fff4e0, red-soft #ffe2e0 / red-ink #b42318, button #0f1115 on #fff.
- Two shadows: sm (0 1px 2px, 0 2px 8px at 4-5%) and lg (a three-layer drop out to 0 40px 80px -24px at 18%), plus two glows rgba(134,169,255,.45) and rgba(192,159,255,.45).
- A dark set (bg #0c0d10, surface #16171b, ink #f3f3f4, darker pastels, inverted button) applied by prefers-color-scheme: dark unless :root[data-theme="light"], and by :root[data-theme="dark"].
- Headlines are Geist 600-700 with letter-spacing -0.05em to -0.065em; the hero h1 "the ai for work" is clamp(48px, 9vw, 112px)/0.92 with "work" in ink-3. Pills everywhere: 40px buttons (48px large), a black primary with an inset highlight, a ghost with a 1px line.
- The logo is two overlapping 18px rounded squares, a blue gradient over a violet one with mix-blend-mode multiply (screen in dark).

SECTIONS (data-section in order)
1. nav: sticky, 78% bg via color-mix with saturate(180%) blur(14px), a hairline after 8px of scroll. Logo, Product / Integrations / Customers / Pricing, Sign in, Start free. Links hide under 860px.
2. hero, from back to front:
   - the two blurred glows (the grid now belongs to the whole page, below)
   - an amber eyebrow pill ("backed by foundry row", with an orange F tile), the h1, a sub, two CTAs and a small note
   - a 620px chat card (28px radius, the lg shadow, a top-light gradient border via mask-composite). Its header has an avatar, "Connected to your workspace" with a live green dot, and Mail / Calendar / Docs source pills. A 400px scrolling body starts with "Good afternoon, Jordan". The footer holds three suggestion chips, a composer (input plus a black send button, disabled when empty) and a hint row with an Enter keycap.
   - floating cards hanging off the chat edges, each bobbing with its own rotation through a --r variable: an email preview (left -170px, -4deg), a blue "Summarize this email…" command (top right, 3deg) and a violet AI summary (right -190px, 3.5deg)
   - six agent badges scattered around the stage (Analyze, Categorize, Summarize, Reply, Schedule, Archive)
3. logos: a muted row of six fictional wordmarks in varied faces.
4. product: three alternating feature rows, copy plus a 1/0.86 rounded canvas tinted with a radial pastel:
   - a stack of an email card, a command pill that types and erases three commands with a blinking caret, and a summary card, all floating
   - an inbox with category tabs (All / Needs reply / FYI / Later, with mono counts) that filter seven rows with coloured tags
   - a draft with Direct / Warm / Brief tone buttons that cross-fade the body text
5. how-it-works: three bordered step cards with mono 01-03.
6. integrations: a hub panel (36px radius, pastel radial washes, a masked dot grid): three tiles each side (Mail, Calendar, Team chat / Docs, Wiki, Tasks), each a 44px tinted icon tile coloured by its own --c, a name, a one-line meta and a mint "Live" chip, wired to a central 132px Tidewell mark with two expanding rings and a "6 sources in sync" label. The wires are one SVG with a 0-100 viewBox stretched over the panel (preserveAspectRatio none, vector-effect non-scaling-stroke): faint base curves plus gradient pulses that travel along them using pathLength=100 and a 10/90 dash. A footer strip lists the trust points and "40+ more via API". Under 900px the hub moves on top, the tiles go two then one per row, and the wires hide.
7. testimonials: a header with prev/next arrows and a full-bleed scroll-snap rail of eight 360px quote cards with gradient initials avatars. The rail pads itself to the content column with max(24px, (100vw - 1112px) / 2).
8. pricing: a Monthly / Yearly toggle (-20% in mint) that swaps prices from data-m / data-y. Starter $0, Pro $20 or $16 (violet-washed, "Most popular", lg shadow), Team $32 or $26 per seat.
9. faq: four native details rows with a + in a ring that rotates 45deg.
10. cta: a dark rounded card (ink background, bg text) with the two glows blurred inside, "get your afternoons back".
11. footer: brand blurb, three link columns, and a base row with the fictional notice.

PAGE GRID SPOTLIGHT
- One absolutely positioned layer behind main and footer (z-index 0 vs 1): a 64px grid at 4% ink, centred and faded in over the first 160px. On fine pointers a 520px patch of the same grid in blue with violet dots at the crossings, masked to a soft circle, plus a 560px blurred blue-violet glow, ease toward the cursor (12% per frame) in page coordinates, so they stay put while you scroll. Offset the patch's background-position by the base grid's centring so its lit lines land exactly on the base lines. Fade both out when the pointer leaves the window.

THE SCRIPTED CHAT
- When the chat is 40% on screen, wait 0.9s, type "Summarize what I missed this morning" into the composer character by character, then send it. Stop if the visitor has touched the input or a chip.
- A keyword router sends a prompt to one of four canned responses: draft/reply, summary/missed, afternoon/schedule/calendar, or a fallback that explains it is a demo inbox.
- Each response shows a small spinner with a "thinking" line (Reading 14 new emails…) for 1.1s, then streams its text word by word, 22-52ms per word. Rich blocks drop in between:
  - three thread cards with avatar, sender, subject, a one-line note and a Reply / Approve / Conflict tag
  - a draft card whose Send button turns mint and says Sent
  - three calendar slots, one protected violet focus block
- User bubbles are blue gradients with a 6px tail corner. Messages enter with a short translate-and-fade.
- Scroll the chat with its own scrollTop. scrollIntoView would also scroll any page embedding this one.

AGENT BADGES
- Each badge is a pill with an icon slot that expands from width 0 to 18px with an overshoot curve, and a label whose width animates.
- Each one loops on its own: idle, then processing (a spinning arc, "Reading…"), then success (a tick drawn with stroke-dashoffset, a small pop) or, about 6% of the time, error (a drawn cross and a shake), then back to idle.
- Labels swap with a blur: the old one slides down and out, the new one drops in. Measure the new label in a hidden span first and set the width before the swap, or the pill snaps instead of stretching. Clicking a badge steps it through the states.

THINGS THAT BREAK
- body needs overflow-x: clip, not hidden, or the sticky nav stops sticking.
- The floating cards and badges hang outside the chat. Hide the cards under 1040px and the badges under 1180px, or they cause horizontal scroll at 390px.
- The floating animation and the static rotation share transform, so the keyframes must include rotate(var(--r)). Otherwise the cards snap upright while they bob.
- The inbox and voice buttons need role=tab / aria-selected and aria-pressed kept in sync by the script, not only a visual .on class.

THE FLOOR
- One h1, a main, labelled send and arrow buttons, aria-live on the chat body, decorative badges aria-hidden and out of the tab order, visible focus rings.
- prefers-reduced-motion collapses every animation and transition, caps each scripted wait at 40ms, skips the badge loops and stops the typing loop after one command.
