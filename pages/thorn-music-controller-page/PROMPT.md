Build a product landing page for THORN/98, a fictional desktop music controller ($649; two detented dials, two long-throw faders, a joystick and three latching tape keys around one small screen), as one HTML file with no libraries and no images. The device itself is the hero, built in CSS 3D from layered DOM, and every control on it works.

TYPE AND TOKENS
Saira for display and labels (weight 700-800, tight tracking in headlines, wide-tracked uppercase in small labels) and Asap for text, both embedded as woff2 data URIs. Palette: fog #c9ced3, alloy #b2b6bd, steel #92959c, graphite #51575d, carbon #0f1215 (the screen), ink #1b1d21 with two softer greys, signal orange #fe5d01 (record and accents), lime #7bb470 → #a9d046 (power only). The page is a soft grey with a big diagonal light shaft. Three finishes as token sets on [data-finish]: fog (cool grey shell, graphite faders), graphite (dark shell, fog faders), sand (#dad4c9 shell, umber #4c463e faders); each sets the shell, face, grip, thumb, key and label colours. Buttons are soft raised pills with an orange dot.

THE DEVICE
- One artboard, 651 x 331 design units; inside the device 1em is one unit (font-size: var(--u)), so a single variable scales it.
- Depth: a helper stacks N copies of a slice at increasing translateZ to extrude the shell, the dial knurls, the fader caps and the keys; the scene is tilted in perspective and follows the cursor a few degrees, with a specular sheen gradient that moves with it.
- Parts: a speaker grille of 46 holes, an engraved logo, a deep recessed screen with a matte bezel, two dials with 0-80 scales, two faders (VOLUME, TUNER), a joystick in a ring, three tape keys (stop, play, record) down the right edge, a power key (the only lit control, lime when on) and two lever toggles on the right flank (shuffle, repeat).
- State object mirroring a state machine: power, playing, track, progress, shuffle, loop, rec, mode (Player, Radio, Tape), the two dials, the two faders, the tape key. Mirror it onto <html> as data-power / data-playing / data-rec / data-mode / data-shuffle / data-loop so CSS styles from it.
- Input: dials turn by drag or arrow keys in 80 detents across a 320° sweep (low and high EQ); faders drag (volume 0-100; tuner across FM 87.5-108); the joystick moves left or right between modes and plays or pauses on tap; play and record latch down like a cassette deck. Each control is focusable with a role, a label and an aria value.
- Sound: a mechanical click per detent and key, made in Web Audio from a short decaying noise burst through a band-pass filter (a deeper double "thunk" for latching keys), toggled by a speaker button in the nav.
- The screen is blank in standby ("Press POWER to begin" under the device); powered on it shows the mode, a track with a progress bar, the value just changed, and a breathing lime glow behind the glass while playing (orange while recording). Toasts confirm changes.

SECTIONS
1. nav: the THORN / 98 wordmark, four links (Controls, Display, Finish, Specs), the sound toggle and a Reserve pill.
2. hero: an eyebrow, the h1 "Music you can put your hands on." with "hands" in white, a lede, Reserve — $649 and Explore the controls, the device large below with a row of finish swatches.
3. controls ("All hardware. Zero menus."): five numbered cards, each with a small live copy of one control (dials, faders, joystick, tape keys, the power key) and a readout.
4. display ("A screen that speaks only when spoken to."): a close-up of the screen with three notes (three modes, ambient glow, side toggles).
5. finish ("One alloy. Three finishes."): three swatch cards with their hex pairs, plus the power, record and display colours and the type.
6. specs: a definition list (dimensions, weight, display, controls, audio, radio, connectivity, finishes), noting which finish is shown.
7. cta ("Turn it on."): a small device, the price and a refundable reservation. 8. footer: the wordmark and a line saying the product is fictional.

THINGS THAT BREAK
- Keep the stack depth modest; every layer is DOM, and a phone needs fewer.
- Set pointer capture on drag and convert pointer motion to value through the control's own rotation and scale, or dials jump when the device is tilted.
- Create the AudioContext lazily inside the first click, never at load, and wrap it in try/catch so a blocked context stays silent.
- The swatches change data-finish on <html>; a mini device can pin its own finish.

THE FLOOR
One h1, labelled sliders and buttons with keyboard control, aria-hidden decorative layers, visible focus rings. With motion reduced the tilt and glow stop. Under 900px the hero stacks and the device scales to the width. No horizontal scroll at 390px.
