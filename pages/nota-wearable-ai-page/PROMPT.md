Build a product page for NOTA One, a fictional titanium AI wearable worn on a cord ("Remembers what you heard. Forgets when you ask it to."; it listens only while you hold a key, runs its model on the device and has a hardware mic switch), as one HTML file. No libraries. Google Fonts: Archivo with the width axis (wdth 62-125, wght 200-900) for display, Instrument Sans 400-600 for text, JetBrains Mono 400-700 for labels, and Noto Sans JP subset to the few Japanese characters used.

DESIGN SYSTEM
A quiet luxury catalogue: bead-blasted titanium bands (grey #C0BFBD with lighter and darker steps, ink #2A2928) alternate with sapphire-covered LCD glass bands (#171717 to #232323, text #F2F0EC). One signal orange #FF5B34 (with deep and light steps) for LEDs, the crown and the primary button, plus pink #EC2B63 and cyan #60B3DD for LED states. Archivo headlines at 600 with -0.035em tracking and a light grey second clause; mono uppercase labels; a multiply grain over everything. Buttons are hardware keys: a dark key in a black well, or an orange key with a glossy top. Safe-area aware gutters.

THE DEVICE (one live unit, every size in container units of the device)
A rounded-square titanium body with brushed texture, a bail and loop for the cord, four Torx screws, an orange mic switch on the top edge, a privacy LED, and a sapphire LCD: a battery and MIC icon, four mode cards (L R T Q), four seven-segment digits drawn as SVG polygons with a blinking colon, the mode word (LISTEN), a status line, a four-quadrant pie and four level matrices, over a canvas of faint sine waves. Under the screen: four mode LEDs (Listen, Recall, Translate, Quiet), a speaker grille, the ASK key in a machined well, and an orange knurled crown with an indicator. A foot with ノータ in orange and a serial. A soft sheen follows the pointer and the unit tilts slightly in 3D.
- Hold ASK (pointer, Space or Enter): the mic opens with a two-note chime, the LED turns orange (blue in Translate), the digits count seconds, the sine waves grow, the matrices bounce. Let go: it thinks (the pie cycles), then types a canned answer into a readout under the device with a blinking caret and a chime, and returns to idle. Saving a note turns the LED pink.
- The crown has four detents (drag, click to advance, arrow keys, wheel) and ticks; Quiet disables the key.
- The mic switch (or M) cuts the mics: the LED goes dark, the word reads MIC OFF, the key buzzes.
- It boots once: all segments lit (8888), every LED on, then settles to the clock.
- Sounds are tiny WebAudio oscillator blips, started on the first interaction.

SECTIONS
1. nav: sticky frosted titanium bar with the NOTA logo and an orange dot, four mono links and a "Reserve · $899" key.
2. hero: eyebrow, the two-clause headline, a lede and two buttons, then a dark studio panel with a faint grid holding the device hanging from a drawn cord, the readout, keyboard hints, and six callouts (Mic switch, Sapphire display, Microphone array, Privacy light, Mode crown, Titanium body) joined to the exact parts by measured leader lines (hidden under 1080px).
3. stats: a six-cell ruled strip (31 g, 3B on-device model, 0 bytes sent by default, 18 h, 38 mm, IP68).
4. how-it-works: three titanium cards (Hold the key with a key that keeps pressing itself, Say it plainly with a level meter, Read or listen with an LCD answer).
5. anatomy (dark): four close-ups, each a live clone of the device zoomed onto one part (crown, key, display, mic switch) with a code tag, copy and a small spec list.
6. privacy (dark): a ledger panel of three big seven-segment counters (words heard while the key was held, ticking up while you hold it; notes; 0 bytes sent), then "The light tells everyone what it's doing." and a legend of LED states (off, white, orange pulsing, pink, cyan).
7. modes: four small LCD screens, one per crown position, each animated (a rippling dot field, a grid of lit days, a Japanese line translating into English, a breathing dot).
8. build: a sticky technical drawing (the rear case with an embossed name, a Qi2 coil, an etched serial, Torx screws and lettered markers; the side profile with the switch and crown; dimension lines; a lettered legend) beside "Machined titanium and sapphire glass." and four facts.
9. specs (dark): a two-column technical sheet.
10. order: $899 and what's in the box on the left; three crown finishes (Signal orange, Chalk white, Graphite) as knob buttons on the right that recolour the crown on the live device and its close-ups, and a reserve button that answers inline (it is a concept page).
11. footer: a dark mono line.

THINGS THAT BREAK
- Size every part of the device in cqw so it scales as one object; px values break it at other widths.
- Make the close-ups by cloning the live device after its boot, drop the clone's canvas, make it inert and aria-hidden, scale it and centre the target part by measuring it; re-measure on resize and after fonts load.
- Measure the leader lines with the device's 3D tilt switched off, then restore it.
- Start the AudioContext only from a user gesture.
- Space must not scroll the page while it is held as the ASK key, except inside other controls.

THE FLOOR
One h1, a main, labelled ASK and mic switch buttons with aria-pressed, the crown as role="slider" with aria-valuetext, an aria-live readout, aria-hidden decorative LCD parts. prefers-reduced-motion stops the animations and skips the boot. No horizontal scroll at 390px.
