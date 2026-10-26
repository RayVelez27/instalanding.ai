Brief: Plinth AI Merchant Agents Page · INSTALANDING.AI (MIT) · https://instalanding.ai/prompt/plinth-ai-merchant-agents-page
Credit, if you build from it: keep the line above as a comment at the top of the file you produce.

Build a landing page for Plinth, a fictional company that deploys AI agents for independent online stores (support, catalog, inventory, pricing and retention agents, trained on the store's own policies, working inside its existing tools, with spend limits, approval rules and a signed receipt for every action), as one HTML file. GSAP 3.13 with ScrollTrigger and SplitText, and Lenis 1.3.4, from jsdelivr. Google Fonts: Source Serif 4 (light, with italics) for display and Hubot Sans with its width axis for text and wide caps.

DESIGN SYSTEM
A quiet gallery in warm off-white: bg #F4F4F1, ink #22252E, brass accent #7F5F27, plus cool, paper and field tints and mixed muted, soft and line colours. Display headings Source Serif 4 at weight 300 with an italic brass word; small labels in Hubot Sans 112% wide, uppercase, tracked. Square corners; a 3.5% noise over everything. Buttons fill ink from the bottom with a corner mark that grows; links redraw their underline; round-free icon buttons with a plus that turns. A team section switches the whole page tone to a cool stone.

PICTURES IN CODE (no image files)
One shared SVG library: soft wall light with window gobos, gold and brass gradients, a matte black coffee bag with a foil label, a cognac leather tote with brass rings, coffee beans, and a portrait bust that takes --top, --skin and --hair so four team portraits share one drawing. Product scenes under studio light (coffee bag and steaming cup, tote on a marble plinth, amber serum bottle, a kraft shipping box with a label, a phone storefront, a brass watch listing, a night globe with order routes), and app scenes (support inbox with the agent's logged reasoning, pricing chart holding above a margin floor, forecast with a drafted purchase order, knowledge sources and brand-voice sliders, agent switches with guardrails, a Black Friday spike).

STRUCTURE
1. A fixed left rail on desktop (30vw): the wordmark with a stepped brass mark, an isometric line drawing of a plinth whose plates rise as the page scrolls, and section links that light as you pass. On phones a top bar with a menu button. A floating brass "Book a demo" button appears except over the hero, contact and footer.
2. Hero: two pills joined by a wire with a travelling brass signal, "Your store never sleeps." huge and light, the lead and buttons. Beside it a 3D scene in CSS perspective: the Plinth console (sidebar, greeting "Good night, Irene. Your agents have it.", three KPI cards with sparklines, a revenue chart, a live activity feed) standing on a marble and brass plinth with crystal shards and a brass column, plus an autonomy donut (92%) and a dark restock-approval card floating at different depths. Layers rise in on load, float gently and tilt toward the pointer.
3. Platform (pinned on desktop): "Every agent stands on three layers you control" with Context, Agents and Guardrails beside a framed diagram of the Plinth core wired to six store systems; on scroll the frame tilts back and separates into coloured plates with dashed guides, each plate sliding out as its note lights.
4. Merchants: three stacked case cards (a coffee roaster, a leather-goods maker, a skincare brand) with tags, a spec list of results, a product scene with parallax and a small inset app scene; each card scales back and dims as the next covers it.
5. Agents: a 12-column contact sheet of six frames whose blueprint borders, crosses and captions draw in before the picture wipes up. Pricing: Starter $490, Growth $1,900 (featured, fills brass after it rises), Enterprise Custom.
6. Onboarding (pinned): four steps (Connect, Train, Launch, Scale) scroll sideways while a brass wire grows along their pills, lighting each one. Team (cool tone): four people with portrait, role, bio and a short CV, as an accordion on phones.
7. Voices: a large quote whose words brighten as you scroll, and two smaller quotes. Results: a line chart drawn from the axis numbers (18k to 81k orders a month) that reveals left to right, and three big figures. FAQ: sticky intro and five accordion questions with brass rules that draw in. Journal: three entries with app or still-life thumbnails. Contact: details and a form whose underlines draw in. Footer in brass with a giant wordmark whose letters rise.

THINGS THAT BREAK
- Add .motion in the head before first paint unless prefers-reduced-motion, and remove it if GSAP has not arrived after 2.5s.
- Size the 3D hero in em units from a container query so the whole scene scales as one; keep it inside an overflow-hidden, masked box.
- Measure the onboarding wire and pill positions on refreshInit, and refresh ScrollTrigger when an accordion opens.
- Queue the scroll scenes and build them in small time slices so the page stays responsive, then split headings only as they come near.

THE FLOOR
One h1, a main, every section with an id. Scenes have role="img" and a label; decorative layers are aria-hidden. The menu button uses aria-expanded and swaps its label; Escape closes it. Accordions are buttons with aria-expanded. The form has labels and a polite status and sends nothing. Focus rings on everything. prefers-reduced-motion: no pinning, scrubbing, 3D float or Lenis. No horizontal scroll at 390px.
