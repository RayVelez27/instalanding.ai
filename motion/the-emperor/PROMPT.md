# The Emperor · one-shot prompt

Paste this into an AI builder or coding agent.

---

Turn a layered battle painting into a living scene as one HTML file: a winged emperor in golden armour on a rock above an army, a storm sky with warships behind. Every image is inlined; the scene is drawn with Canvas 2D, skinned meshes in WebGL. No libraries.

THE PAINTING
- Cut the painting into layers (sky, warships, far army, machines, rock, the emperor's body parts, sword, cape, banners, hair) and rig the soft parts (cape, hair, banners, straps) as skinned meshes on bone chains.
- Contain the 1255 × 912 view in the window; cap DPR at 2. Fade in from black over 2.2s while the camera eases from 1.14 to 1.045 zoom over 5s, then breathes ±0.8%.

THE LIVING LAYER (drawn at points in the painting's own draw order, not on top)
- Behind the sky's foreground: god rays from behind the emperor, a wedge texture turning at 0.012 rad/s screen-blended at 0.11 ± 0.04, and a second copy counter-rotating.
- Sheet lightning: every 9-17s a flash at a random spot in the clouds, a sharp peak at 0.04s, often a second at 0.22s, and a 0.35 glow decaying at 2.2/s; a faint blue spill over the whole frame.
- Fog: two noise textures drifting in opposite directions across the far army, screen-blended.
- Embers in three depths (130 far behind the emperor, 80 mid in front, 12 near as large bokeh), rising with turbulence and wind; 45 ash flakes falling in the sky; 70 dust motes inside the emperor's back-light.
- The sword: a blue aura along the blade, nine energy sparks crawling from hilt to tip, a pulsing star at the tip.
- Grade: a warm soft-light pool around the emperor, a cool vignette, 6% film grain.

THE MOTION
- Wind: one curve, (0.65 + 0.55 × noise(t × 0.17) + 0.25 × sin(0.9t)) × (1 + 1.6 × gust). Each cloth bone rotates by amp × (0.45 + 0.35 × depth) × (0.7 sin(1.6t + φ − 0.75d) + 0.3 sin(2.9t + 1.3φ − 1.1d)) × wind.
- Lights breathe: the back-light on a slow sine, firelights on noise.
- Parallax: a target eases toward the pointer (or two slow sines when idle) with k = 1 − e^(−2.6 dt); the layers follow it through a distance constraint, the camera leans 8% the other way, the near embers 35% with it.
- Click: flare = 1.1 (decays 0.9/s), gust = 1 (decays 0.45/s), 70 sparks from the blade tip (70% blue), 26 hot embers from the click point, and a lightning strike.

SOUND (off until the speaker button is pressed)
- Web Audio only: looping pink-ish noise through a bandpass that follows the wind, a low sawtooth drone at 55/55.4/82.5 Hz under a 180 Hz lowpass, random highpass crackle, thunder as a falling lowpass noise burst, and a rising bandpass whoosh with three sine bells on ignite.

THE FLOOR
- prefers-reduced-motion: 35% of the particles, gentler wind, no camera drift or intro zoom. The canvas is described in an aria-label; the hint "Move to look · Click to ignite" fades in and out once.
