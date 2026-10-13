Build a single-file HTML landing page for "Hollr", a fictional AI chat assistant that lives in a nostalgic mid-2000s instant-messenger window and has an Agent mode that plans and runs tasks. Oswald (display), Neuton (descriptive copy) and Verdana/Tahoma (UI, like the old clients) from Google Fonts; no libraries, no images. Fictional brand, pricing and copy.

THE PALETTE
A night-indigo page (#2c2b5c to #1d1c45) with drifting violet, magenta and blue blurred orbs, a dot grain and twinkling stars. The messenger chrome is pale (#D7E4F5, #EEF0FD, #F5F2F9) with glossy two-tone title bars: blue for chat, violet once Agent mode runs. Window borders are slate #586170. The brand gradient runs from violet #6a2fc4 to magenta #c0169f, with a lemon #e6e82a accent and online green. Buttons come in two kinds: classic bevelled grey with an inset shadow, and gradient pills with a moving sheen.

THE HEADINGS
Every section heading is a framed block: a tiny Neuton kicker tracked at .5em, then one or two lines of uppercase Oswald 700 filled with a slowly moving pastel gradient (lilac, pink, white, lemon, sky) clipped to the text, with a double rule above and below.

THE HERO
- A slim full-width nav styled as a glossy messenger title bar: logo, an "Online" status pill, links, and a "Sign in" button with its access-key letter underlined.
- The framed h1 "Your favorite contact now gets things done." Its kicker is a glass pill with a gradient NEW badge before "MEET HOLLR · YOUR AI CONTACT", and the tracking tightens on phones so the pill stays on one line down to 320px. Then a Neuton lede.
- The centrepiece is a working messenger window that rises in with a 3D tilt, has a conic glowing border that spins faster while the agent runs, and tilts toward the pointer. It has:
  - a title bar with window controls and a toolbar (Invite, Send Files, Video, Voice, Activities) with underlined access keys;
  - a chat log, robot and you avatars, and a status bar with a progress bar;
  - a composer with a Chat/Agent segmented control (a sliding gradient pill), emoticon buttons that insert ":)" and ";)", a Voice clip button and a Nudge button;
  - a textarea whose placeholder types and deletes example tasks, tool toggles (Web, Files, Calendar, Email, as aria-pressed chips) and a Run button.
- Chat mode answers with a typing indicator and typed keyword replies. Nudge shakes the window, plays a short square-wave buzz through Web Audio, and makes the bot promise shorter answers.
- Agent mode matches the task against playbooks (party, report, trip, email, meeting, or a generic plan). It posts a plan card, runs each step with a spinner and a tool tag, and skips any step whose tool is turned off (striking it through). It ends with a result card (Approve & continue, Refine). Run turns into Stop while it works.
- Floating stickers (Web search, Calendar hold) bob beside the window. Suggestion chips below start example runs.
- A perspective grid floor scrolls under the hero, and a spotlight follows the pointer.

THE REST
- Features: six window-styled cards, each with a 3D layered icon (a stack of slabs with a glossy face, floating and catching a sheen) in its own colour, and small animated glyphs (nudge arrows, a winking smiley, lines being written, sound waves, clock hands, a status ripple).
- How it works: a sticky left column with a giant outlined step number that rolls over and a rail that fills with scroll. Three sticky stacking cards on the right; the card being covered scales down and dims. Each card plays its own mini animation: a sign-in form typing a name, a chat that switches to Agent mode and ticks off a mini plan, and an approval with a history list.
- FAQ: a help chat window with searchable questions ("/" focuses the search). Opening one shows typing dots before the answer bubble. An empty state offers to ask Hollr instead.
- A mega footer: the framed "Hollr has signed in." with an email form, trust ticks, and a tilted buddy-list window (your status, Hollr online with a rotating status message, three "agents at work" progress bars). Then link columns, a giant outlined HOLLR wordmark with flowing colour, and a status strip with Back to top.
- A "Hollr has just signed in" toast slides up after a few seconds.

THE FLOOR
One h1, a main, data-section on every region, labelled inputs, real buttons, visible focus, aria-live on the chat log, no horizontal scroll at 390px. Under prefers-reduced-motion, every animation collapses to its end state, the console doesn't tilt and replies appear at once.
