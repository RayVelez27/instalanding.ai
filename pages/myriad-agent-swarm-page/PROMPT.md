Build a one-screen landing page for Myriad OS, a fictional platform of specialist AI agents that work as one swarm, styled like a game's character-select screen, as one HTML file. No libraries. Google Fonts: Unbounded 300/500/700/800 (display), Space Grotesk 400/500 (body), JetBrains Mono 400/500 (labels).

DESIGN SYSTEM
Deep, glowing and tinted by the selected agent. Five colours are registered with @property (--c1 accent, --c2 light accent, --c3 near-white, --bg1 and --bg2 backgrounds) and :root transitions all five over 1.1s, so switching agent recolours every gradient, border and glow smoothly. Text is --c3 at 72%. Mono labels are uppercase and tracked 0.18-0.3em. Panels are chamfered with clip-path (a cut top-right and bottom-left corner) over a translucent accent gradient with a backdrop blur. A noise overlay and a vignette sit over everything. A custom cursor: a 38px accent ring that trails the pointer and grows over [data-cursor] elements, plus a 4px dot (hidden on touch).

THE AGENTS (data, five of them)
Each has a name, role, topology, model tier, a tagline, a paragraph, three stats (nodes, sync %, latency ms), a theme (c1, c2, c3, bg1, bg2) and four abilities (an icon, a name and a line; the fourth is the ULT). AEGIS the Sentinel (green #14d27c; Policy Gate, Sandbox, Seal, Bastion), AXON the Orchestrator (violet #8b6cff; Fan-out, Consensus, Re-route, Hive Mind), KESTR the Scout (amber #f5a742; Sweep, Deep Scan, Signal Lock, Skyline), LOOM the Synthesist (cyan #2fc6ff; Thread, Stack, Splice, Tapestry), ECHO the Critic (pink #ff4f8d; Replay, Weigh, Red Team, Resonance).

LAYOUT (one 100svh stage, min 740px)
1. nav: a hexagon logo of three linked nodes with MYRIAD tracked wide and a small OS, and a Launch console button.
2. hero, three columns:
   - the visual: a dashed orbit ring and a ring of 90 ticks turning slowly; inside it a circular grid of katakana glyphs, faint, with scattered cells pulsing on staggered nth-child timings and three random cells re-rolling every 140ms; the swarm canvas over it; a HUD bottom right with NODES, SYNC and LATENCY counting up to the agent's stats.
   - the copy: an outlined index number (01) that fills with a gradient, a vertical rule with a travelling glowing dot, the agent's name huge in Unbounded 800 with a gradient fill (scrambling through random characters into place on each switch), the tagline, a chamfered brief (ROLE / TOPOLOGY and the paragraph), four ability tiles keyed Q E C X (the fourth marked ULT) that show the ability's name and line below on hover, focus or click, and a chamfered Deploy <AGENT> button with a light sweep beside a View spec sheet link.
   - the rail: five hexagon buttons, each in its agent's colour with a glyph (a nested hexagon, an atom, a trefoil, a helix, a target), its number and name; the active one glows, scales up and shows a progress bar for the autoplay.
3. status: a bar along the bottom with a pinging dot and a live "12,480 agents online" count that drifts every 1.3s, and prev / 01 / 05 / next.
Switching agent fades the copy out (blur up) and staggers it back in (rise, blur down), recolours the page and reforms the swarm.

THE SWARM (Canvas 2D, additive)
- 640 points (380 under 700px wide). Five formations precomputed as target positions in 3D: an icosahedron's 30 edges plus its vertices (AEGIS), a Fibonacci sphere with two tilted rings (AXON), a trefoil knot (KESTR), a double helix with rungs (LOOM), seven concentric rings that ripple as a wave (ECHO). For each formation compute every point's two nearest neighbours once.
- Each point is a spring toward its target (velocity × 0.86 + offset × a per-point stiffness 0.012-0.04), with a small idle wobble; switching formation kicks every velocity randomly so the swarm bursts and reforms.
- Rotate slowly, tilt with the pointer (eased), project with a simple perspective (FOV 3.2) and scale to the visual's size. Points within 120px of the pointer are pushed away; up to nine beams are drawn from the pointer to nearby points.
- Draw with globalCompositeOperation lighter: a radial core glow, neighbour links (only when the projected link is short), points as cached radial-gradient sprites sized and faded by depth (every 23rd point a brighter hub), and message pulses that travel along links and hop up to six times. Colours ease toward the new theme each frame; rebuild the sprites when they change.

INPUT
Clicking the rail, the prev / next buttons, arrow keys, the mouse wheel (one step per 1.1s, desktop only) or a horizontal swipe on the visual changes agent. Autoplay advances every 9s and pauses while the pointer is over the copy or the rail.

THINGS THAT BREAK
- Register the five colours with @property or the theme jumps instead of transitioning.
- Precompute nearest neighbours per formation at load; doing it per frame is N² every frame.
- Size the glyph matrix from the orbit's measured box on resize, and only rebuild its cells when the column count changes.
- Cap the canvas DPR at 2.

THE FLOOR
One h1 (the agent name), the canvas and decorations aria-hidden, labelled rail buttons, an aria-live line for the selected ability, keyboard navigation. prefers-reduced-motion stops the glyph pulses, orbit spin, scramble, autoplay and pulses, and slows the swarm's rotation. Under 960px the layout stacks (visual, rail as a row, copy); no horizontal scroll at 390px.
