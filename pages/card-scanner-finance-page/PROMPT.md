Build a single-file HTML landing page for "NOVA", fictional autonomous finance agents that read every transaction, tokenize every card and reconcile and close the books in real time, with a person in the loop. Inter Tight (display), Inter (copy) and JetBrains Mono (UI) from Google Fonts; GSAP 3.12.5 with ScrollTrigger and three.js r128 from cdnjs; everything else inline, no images. Fictional vendors and figures.

THE PALETTE
Near-black violet (#050508, #0b0a14), pale lilac text, accents lilac #c4b5fd and violet #8b5cf6, with a warm ember #e3857a and cream #f1dba7 for the close. Heavy uppercase headlines in Inter Tight 900, filled with a radial gradient clipped to the text whose centre (--gy) GSAP scrubs with scroll, so the light travels down the words as they pass. Use three oklch palettes (lilac, indigo, ember) and interpolate in oklch where supported. Give each headline width: fit-content so the gradient box covers the longest line.

THE HERO
Left: a pulsing "Agents online · v2.4" pill, "AUTONOMOUS / FINANCE / AGENTS" with the middle word in the indigo palette, a lede, a pale pill CTA and a ghost "Watch demo" with a ringed play icon. Right: one scene built at a fixed 880x640 and scaled to its column. It contains:
- A tilted glowing orbit ellipse with a running highlight, dust and three dots riding it with SVG animateMotion.
- A glass JSON panel showing a live transaction whose fields flash as they change.
- A scrolling mini code panel and a faint ghost panel.
- Two metallic cards (copper and graphite: chip, contactless mark, brushed texture, perspective tilt) floating out of phase. A sweep of light crosses the graphite card when it gets tokenized.
- A checklist (Transaction read → Card tokenized → Risk analysis → Category assigned → Reconciled → Books updated) that steps through one transaction at a time, with a READ → TOKENIZE → ANALYZE → RECONCILE → CLOSE pipeline lighting in sync.
- A light beam dropping into a strip of water at the bottom of the hero, whose horizon line and reflection align to the beam.
Tilt the scene gently toward the pointer. Behind it all, three.js additive particle dust drifts sideways, and a low SVG rock silhouette sits on the waterline. Four big mono stats sit in the water strip.

THE SCANNER
Pin a section and scroll a horizontal track of cards through a fixed vertical light bar at the screen's centre. Each card is two layers, the solid card and a dark panel of churning code (pseudo-source about tokenizing, risk scores and ledgers, with a glitch flicker and a fading mask). Clip them against the bar every frame, so a card turns into code as it crosses. Fire a scan flash the first time it enters. Draw the bar on a 2D canvas as stacked additive glow layers with a particle spray that intensifies while a card is in the beam. Fade the bar in only once the intro text has scrolled past it. Below each card, a numbered caption: Tokenize, Score, Act, Close. A progress hairline tracks the scroll. Render particles only for sections on screen, in one requestAnimationFrame loop.

CONTROL
A bento of glass tiles with gradient hairline borders and a pointer-following glow:
- A live ledger: rows stream in at the top with a scanning badge that settles to Matched or Flagged, a light beam sweeps across the table, and the counts tick.
- Guardrails: four real role="switch" toggles drive an autonomy meter (Guarded, Supervised, Autonomous) and write to the audit trail.
- Connectors: chips orbiting a glowing NOVA core with depth-based scale and opacity.
- A signed audit trail with hashes, where human actions are marked in cream.
- Month-end: "2 days", in the ember palette, with before/after bars that grow on view.
- An approval card: Approve or Hold a payment, each logged, and a new request arrives four seconds later.

THE REST
A two-column FAQ (sticky head with a "Talk to a human" tile, native details with smooth height animation and a glowing left rule on the open item). Then a super footer: a framed stage with HUD corner brackets, "Put your finance ops on autopilot." with "autopilot." in ember, and a gooey spinning-gradient Deploy button. Clicking Deploy runs a simulated agent in a console (timer, progress bar, six log lines resolving to results, then three metrics popping in). Below it, link columns and a newsletter field. Last, a giant NOVA wordmark split by a moving scan line: solid on one side, wireframe on the other.

THE FLOOR
One h1, a main, data-section on every region, aria-hidden on every decorative canvas and the hero scene, real buttons with types, visible focus (including on the invisible button layered over the custom Deploy button), no horizontal scroll at 390px. Under prefers-reduced-motion, stop the decorative loops (orbit, floats, glitch, sweeps, the wordmark split). Keep the pinned scroll, because the reader drives it.
