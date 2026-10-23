Build a landing page for Mirai, a fictional AI companion app ("The AI companion that actually listens": it remembers what matters, checks in and keeps conversations private), as one HTML file. No libraries. Google Fonts: Sora 300-800 and JetBrains Mono 400/600. No images: the character and every illustration are inline SVG and CSS gradients.

DESIGN SYSTEM
Flat, bold and friendly. Purple #b914f0 with a deeper #8814ad for big background circles, charcoal #1f2525 (with #182020 and #2a3232 steps) for the page and the cloud shapes, and one mint accent #66ddc6 for dots, ticks, highlights and the primary button. Sora 700 for headings with tight tracking and the key words in mint; Sora 300 for body; uppercase mono eyebrows with a glowing mint dot. Rounded everything: 22px cards, 28-36px panels, pill buttons that lift on hover.

SECTIONS
1. nav: fixed; MIRAI wordmark, four links (the active one marked by a mint dot, the others underlined in mint on hover) and a white "Let's Talk!" pill that turns mint. It frosts and shrinks after 40px; under 760px a burger opens a floating menu card.
2. hero: one full-screen SVG scene (viewBox 1920 × 1080, sliced to cover): a purple sky with deep-purple circles, MIRAI huge in white Sora 800 across the middle, the character rising between the letters, charcoal clouds made of overlapping circles filling the bottom corners and drifting, clusters of mint bubbles that pop in and float, and two lines of copy ("Hey, I'm your new friend," top left, "The AI companion that actually listens" bottom right). An intro: clouds rise from below, the word lifts, the character slides up with a slight overshoot, the bubbles pop. A scroll cue and a small mono hint ("psst, move closer, she notices. just don't poke her.").
   - The character: a girl drawn in SVG gradients (skin, blush, a black bun of circles, swept hair with strand strokes, one big and one small eye with clipped irises and highlights, brows, a tiny nose and mouth, an earring, a mint top). A rig updates her every frame: eyes follow the pointer (or glance around on their own when idle), she blinks every few seconds (sometimes twice), her head sways and breathes and tilts toward the pointer, she perks up (brows up, pupils wider) when the pointer comes near or the nav CTA is hovered, and when clicked she is annoyed (lids half closed, brows flattened, a quick head shake) for two seconds.
   - Every layer has a parallax depth and shifts with the pointer.
   - Under 760px the SVG reframes its viewBox around the character and scales the word down, and the copy moves into text blocks above and below.
3. ticker: a marquee of feature words in big type, alternating solid white and outlined, separated by mint dots; it pauses on hover.
4. features: "A companion that actually gets you." with filter tabs (All, Conversation, Wellbeing, Privacy) over a 12-column grid of cards: one big Memory card and five smaller ones (Voice with an animated waveform, Check-ins, Privacy with a lock, Journal, Control), each with CSS-gradient art in the palette, a big glyph, a badge, a corner label and a play button that pops on hover.
5. stats: four ruled figures that count up (<300 ms voice response, 40+ languages, 24/7, 0 ads).
6. how-it-works: a purple band with big background circles and four numbered rows (Say hi, It learns your vibe, It remembers, It shows up) that fill charcoal and spin their arrow on hover.
7. demo: a phone-style chat card on the left (avatar, online status, "remembers 214 things about you") playing a looping conversation with typing dots before each reply, and on the right "Feels personal. Stays private." with three mint-checked trust points.
8. pricing: a Monthly / Yearly switch with a sliding knob (−20% tag) and three plans (Hello $0, Plus $9.99 or $7.99 as the purple card with mint dots, Family $19.99 or $15.99) whose prices and notes swap.
9. faq: five details rows whose plus turns into a mint minus.
10. waitlist: a rounded purple panel with circles and floating mint bubbles, "Someone's been waiting to meet you." and a pill email form that confirms inline.
11. footer: wordmark and blurb with four round social buttons, three link columns, MIRAI huge in outlined type and a line saying Mirai is an AI and not a substitute for professional care.

THINGS THAT BREAK
- Map the pointer into SVG coordinates with getScreenCTM().inverse() before comparing it to the face, or the gaze is off at every size but one.
- Rotate the head around the neck (a fixed pivot), scale the irises around their own centres, and clip the irises and lids to the eye whites.
- Ease every rig value toward its target each frame (eye, tilt, near, annoyed, parallax) instead of setting it, so she never snaps.
- Keep the wordmark and copy in the SVG on desktop but move the copy to HTML on phones, where the reframed scene has no room for it.

THE FLOOR
One h1 (visually hidden, the hero is an illustration), a main, an aria-label on the hero SVG, aria-hidden on the ticker and decorative art, a labelled burger and email input. prefers-reduced-motion stops the intro, sway, drift, floats and marquee; the gaze still follows. No horizontal scroll at 390px.
