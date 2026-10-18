Build a single-file HTML landing page for "Kind Swarm", a fictional swarm of small AI agents for social work: they draft intake notes, find benefits, watch housing waitlists, keep court dates, translate and chase follow-ups, and a person approves everything. The look is loud and warm: flame-orange and lime blocks covered in concentric op-art ring patterns, huge stencil type, hard offset shadows, cream cards, and every agent is an animoji character, a glossy rounded diamond with big cartoon eyes. Fictional product, agents, prices and numbers, labelled as such in the footer. No images and no canvas: the characters are inline SVG with CSS and a few lines of JS.

STACK
- Google Fonts: Stardos Stencil 400/700 (display, uppercase, line-height .92), IBM Plex Sans Condensed 400-700 with italics (text, and an italic "serif" accent for second lines), IBM Plex Mono 500/600 (labels, tags, prices).

THE SYSTEM
- Colours: ink #15111F, cream #F4EFE6, flame #FF5A3C (deep #F0361A), lime #D4FF3A, focus blue #3D7BFF, muted lilac #B9B0CC / #CFC6E8.
- The .rings background: concentric arcs built from radial gradients alternating two colours (--c1 / --c2) at a tile size (--s), with a faint shadow tone. Variants: flame for the hero and closing CTA, lime for the marquee and the "zero" band, ink for guardrails, and eight pastel stage colours for the agent cards (blue, butter, peach, lilac, pink, lime, sky, orchid).
- A grain layer (an feTurbulence noise filter, multiplied at 22%) sits on the coloured bands.
- Buttons are pills with a 3px ink border and an 8px hard offset shadow that grows on hover and collapses when pressed: ink, paper and lime variants; on dark sections the border and shadow turn lime.
- Labels are mono, uppercase, letter-spaced ("02 — The crew").

THE CHARACTERS
- One hidden SVG holds shared gradients (blue to violet, sun, peach to pink, periwinkle, lilac), a gloss highlight and a shade. Each character is a glossy rounded-diamond body (most in blue-to-violet, the Benefits Navigator in sun, the Housing Scout in peach) with an ink outline offset as a hard shadow (drop-shadow 8px 8px 0 ink), big white eyes with ink pupils, and a face that tells its personality: the lead and the scribe have an antenna curl and a smile; the navigator sparkles with stars; the scout holds a magnifier; the court keeper holds a "31" calendar and looks anxious; crisis triage sweats with worried brows; the follow-up runner wears sunglasses and points; the interpreter winks with a thumbs up; the records clerk is exhausted, one eye an X and one heavy-lidded.
- .bod bobs (squash and stretch, 3.4s), .eye blinks every 5.6s, .pupil follows the pointer through --px / --py set on <html> (up to 7px). .d1 to .d4 stagger the timing. Clicking a character replays a .react squash-and-jump.

SECTIONS (data-section in order)
1. hero (flame rings, with the nav inside): logo character and "KIND SWARM" wordmark, four links and an ink "Book a demo". Mono labels "Agent swarms for social work" and "Drafts, never decisions" over a 3px rule. Then the giant h1 "KIND / SWARM" in Stardos Stencil filled with a slowly drifting dark ring pattern (background-clip text), with the big lead character rising in beside "KIND". Under it the italic "They draft, fetch and remind." over "PEOPLE DECIDE.", a sub, "Meet the crew" and "See the guardrails", and an ink stats strip: 08 agents on the desk, 00 (lime) decisions without a person, 24/7 on call with a pulsing lime dot.
2. marquee (lime rings): a slow edge-faded marquee of "Intake drafted · Benefits found · Court date kept · Housing matched · Follow-up sent · Human approved", alternating filled and outlined words, paused on hover.
3. how (cream): "Many hands. one desk." Three numbered steps with huge outlined numerals: Say it plainly, Lanes not a chatbot (with a hand-off trace "scribe → navigator · 1.8s"), You sign it off.
4. zero (lime band): a giant "0" and "Decisions made without a person. Not one."
5. crew (ink): "Eight agents. one job each." with "Showing 08 of 08" and a row of filter pills (All, Intake, Benefits, Housing, Legal, Crisis, Language; aria-pressed, the active one lime). A grid of cream cards with a lime hard shadow: a ringed pastel stage with a white tag ("Most deployed", "Finds money"…), a black agent code (AGT-01…), the character (lifts and tilts on hover), the name, a black price pill ($14/mo, Free…), a description and a mono skills line. Agents: Intake Scribe, Benefits Navigator, Housing Scout, Court Date Keeper, Crisis Triage, Follow-up Runner, Interpreter, Records Clerk. Filtering hides cards whose jobs don't match and updates the count.
6. queue (cream): "Nothing sends itself." beside an approval-queue panel with three drafts (SNAP application, hearing reminder in Spanish, three shelter options), each with the agent, the household, and Edit / Approve buttons; compliance chips (HIPAA, 42 CFR Part 2, SOC 2, State retention rules) and a testimonial.
7. guardrails (ink rings): "Drafts. never decisions." and four rule cards: Consent, Approve, Escalate, Audit.
8. pricing (cream): "Pick your crew." Three plans with hard shadows: Pick & mix (white, $9 from, per agent / month, Start small), Full swarm (ink with a flame shadow and lime bullets, per caseworker / month, a lime Book a demo) and Agency (white, Let's talk, Contact sales), each with a diamond-bullet list.
9. book (flame rings): "Give the desk back." with "Book a demo" and "Thirty minutes. Bring a real case."
10. footer: logo, links and the fictional legal line.

THE FLOOR
- One h1, real buttons and links, characters inside labelled buttons ("Poke the Intake Scribe"), the filter as a labelled group with aria-pressed and a polite live count, visible blue focus rings.
- Grids collapse to one column on phones and the hero type scales with the viewport; no horizontal scroll at 390px.
- Reduced motion stops every animation and transition: bob, blink, marquee, pattern drift, rise-in and poke.
