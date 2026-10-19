# Neon Room Loop · one-shot prompt

Paste this into an AI builder or coding agent.

---

Build an endless three-column card loop with scroll acceleration as one HTML file: cards drift forever, columns alternate direction, and scrolling kicks them faster before they ease back. GSAP 3.12 and ScrollTrigger from cdnjs, Google Font Unbounded (400/600/800). No image files: every card is an SVG drawn by the script.

THE STAGE
- Palette: page radial #1d1935 → #07060f, whites #FBFAFE / #9E99C1 / #383358 / #282347, navy #1f2158, neon blues #5189fa and #287dd2, a red #D51E24.
- A 500vh section only gives the page something to scroll; the real view is a fixed .gallery of three flex columns (the middle one aligned to the bottom), 160% wide on phones so cards stay large.

THE CARDS
- Each card: 1rem padding around a 22px-radius frame with a hairline border, layered deep shadows, a 6px glowing blue status dot top-right, and a caption gradient at the bottom with an index ("02 / 09"), a title and a pill tag.
- At rest: filter saturate(.2) brightness(.78). On hover: full saturation, a blue border and glow, z-index on top, and the art scales 1.06 over 1.4s (cubic-bezier(.2,.7,.2,1)).
- The art is one isometric neon room rendered nine times with different cameras: describe the room as a list of boxes (x, y, z, w, d, h with top / left / right fills), flat quads on the walls and floor, and glows (radial-gradient ellipses). Project with P(x, y, z) = (ox + (x − y)·0.866·s, oy + ((x + y)·0.5 − z)·s), centring a focus point. The room: floor and rug, two walls with neon trims, a door with a neon frame, two paintings, a bookshelf with books, a media wall with speakers, a console and a glowing TV, a coffee table with a tablet, an L-shaped sofa. One card is a wireframe blueprint with a floor grid. Screens and some glows flicker (opacity .78 ↔ 1, 0.25s alternate).

THE LOOP
- Deal the nine cards three per column, then append a clone of each column's cards so every column is two identical halves.
- For every card: gsap.to(item, { y: '-=' or '+=' half the column height, duration 20, repeat -1, ease 'none', modifiers: { y: unitize(y => wrap) } }). Odd columns go down (+=), the rest up (-=).
- In the modifier, add a shared offset (offset += additionalY.val each call) and wrap: up columns y = (y + offset) % −half, down columns y = (y − offset) % half.
- ScrollTrigger on the section: on update take getVelocity(); set additionalY.val = −velocity / 2000 when scrolling down (÷3000 when up), and tween it back to 0 (default 0.5s, power1.out), killing the previous decay first.

THINGS THAT BREAK
- Measure each column's height after appending the clones, and wrap at exactly half of it, or a gap or a jump appears at the seam.
- Never change the base tween to speed up: the kick must ride on the offset, or the loop stutters every time the velocity changes.
- The gallery is position: fixed, so the page needs its tall section to scroll at all.

THE FLOOR
- prefers-reduced-motion stops the flicker; slow the loop right down for it as well. Captions are real text; each SVG has role="img" and an aria-label. No horizontal scroll at 390px.
