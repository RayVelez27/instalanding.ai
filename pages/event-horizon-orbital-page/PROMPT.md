Build a single-file HTML landing page for "Halcyon Orbital", a fictional satellite-servicing company: inspection, refuelling, robotic repair, life-extension docking, relocation and end-of-life disposal, from LEO to GEO. Archivo (copy and the h1), Archivo Narrow (h2/h3) and JetBrains Mono (labels and HUD) from Google Fonts; three.js r128 from cdnjs; every texture drawn on canvas at load, no images. Fictional figures, fleet and contacts on an example domain.

THE PALETTE
Pure black with warm off-white ink #efebe2 and three steps of warm grey. One accent, amber #ffb45e, for CTAs, active states, HUD values and the glow. Pale ice blue #a9caff only for faults and secondary readouts. Labels are mono, uppercase and widely tracked. Headings are tight uppercase.

THE BLACK HOLE
A fixed, full-screen WebGL backdrop. One fragment shader ray-marches each pixel's light ray around the hole, bending it with a Schwarzschild-like acceleration (a = -1.5·h²·p/r⁵), and:
- marks rays that fall inside r = 1 as captured;
- accumulates a volumetric accretion disc between r = 3 and 13 that thickens outward, built from layered fbm arms, filaments and clumps, rotating Keplerian-fast near the centre;
- applies relativistic Doppler beaming and gravitational redshift, so one side of the disc is bright and blue-white and the other dim and red;
- shows a procedural starfield and faint nebula gas for rays that escape, plus a photon-ring halo.
Render the shader into a target, then a bright pass, a two-pass Gaussian bloom and an ACES composite with slight chromatic aberration, a warm grade, a vignette and fine grain. Run it in three quality tiers (pixel ratio and step count) and drop a tier if the first 90 frames average under 28 fps. Drag to orbit, double-click to reset, and let it slowly auto-orbit. Page scroll eases the camera in and over the disc. Below the hero, a fixed veil fades in to darken and frost the scene so the copy stays readable.

THE HERO
- A three-column nav: the logo (a small amber planet with a ring), centre links inside amber corner brackets with an amber dot on the section in view, and an outlined "Request a mission" button.
- Left: "NOTHING IN ORBIT HAS TO BE LOST." with "lost." in amber, a lede, a filled amber CTA and a ghost CTA, and three mono traits divided by amber hairlines.
- Top right: simulated live telemetry (range closing, closing rate, a drifting latitude, a docking-window countdown).
- Bottom right: a LEO/MEO/GEO radar whose rings and labels cycle, with dots orbiting at three speeds.
- A "Systems nominal" status box.
Scrims keep the left column readable without dimming the hole. The hero ignores pointer events, except on the buttons, so the scene stays draggable.

THE CARDS
Every panel is the same signature glass: a warm mesh-gradient fill (dark at the top, amber and peach glowing in the lower corners), an inset glow, and a 1px gradient border with an amber light sweeping round it (a conic gradient on an @property angle, desynchronised per card). Then:
- A four-up stats strip with count-ups.
- Six service cards. Each has a 3D scene, corner ticks and a live HUD:
  - Inspection: a drone circles a satellite while a LIDAR slice sweeps up it, revealing a point cloud and then finding a cracked cell.
  - Refuelling: propellant slugs run along a hose while a 24-segment gauge fills.
  - Repair: a two-link IK arm carries a reaction-wheel module into an empty bay and torques it in with sparks.
  - Docking: a tug closes on a client's aft end, captures it with a flash and fires its engine.
  - Relocation: a Hohmann transfer around a night-side planet with city lights, with burns at perigee and apogee.
  - Disposal: a satellite falls into a daylit limb, heats, trails plasma and breaks up.
- A four-phase mission timeline on diamond markers.
- Three coverage cards (LEO, MEO, GEO).
- Three fleet cards, each a turning procedural spacecraft (a tug with arms, an inspector with a scanning head, a propellant depot).
Draw all nine scenes with ONE shared WebGL renderer, copied into a 2D canvas per card, and only while on screen. Cards tilt the scene toward the pointer and dolly in on hover. Keep an inline SVG fallback in each card for no WebGL.

THE FOOTER
One large glass panel holding:
- "TELL US WHAT'S WRONG UP THERE." with three promises and a priority email line;
- a mission intake form (name, organisation, email, orbit regime, service, situation) with inline validation and a confirmation, no backend;
- a giant outlined wordmark fitted to its row by JS;
- link columns and a legal bar.

THE FLOOR
One h1, a main, data-section on every region, aria-hidden on the canvases, the veil, the telemetry and every decorative SVG, labelled form fields, visible focus, no horizontal scroll at 390px. A diagnostics overlay appears only if three.js, WebGL or a shader fails. Under prefers-reduced-motion, stop the sweeps, ticker, radar and pulses, stop the hole orbiting and freeze its disc, and render each card scene as one still at its showcase moment.
