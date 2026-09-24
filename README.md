A self-contained HTML lo-fi ambient and sound visualizer, video and webcam effects processor that responds to music. Tested in Chrome, Safari, Vivaldi.

Download the HTML to run locally or run directly from the GitHub page using this address: https://pittsburghmodular.github.io/pittsburghmodular/

<img width="1500" height="929" alt="Hello NV Screenshot" src="https://github.com/user-attachments/assets/cc41a4d6-a88b-48af-a9d6-bd9264b1c12e" />

# NULL VENTANA — User Guide

Null Ventana is a browser-based, audio-reactive visualizer. It draws generative shapes over an optional video file or live camera, runs everything through a chain of retro video effects, and can be modulated by LFOs and by whatever is coming into the audio input. Output can be screenshotted, recorded to MP4, floated as a virtual-camera source, and saved as presets.

Everything lives in one HTML file. Open it in a modern browser (Chrome or Edge recommended; Safari works; Firefox works but records WebM instead of MP4).

---

## 1. Quick start

1. Open `Null_Ventana.html` in your browser.
2. Press **MIC ON** at the bottom of the panel and allow microphone access. The four band meters in AUDIO INPUT should start moving.
3. Pick a shape under **SHAPE A**, a palette under **COLOR PALETTE**, and drag **RATE OF CHANGE** and **DENSITY** to taste.
4. Press **F** for fullscreen and **Tab** to hide the panel.

Nothing is uploaded anywhere; audio, video and camera stay in the browser.

---

## 2. Layout and global controls

The control panel sits on the left. The canvas fills the rest of the window.

**Panel behaviour**
- Every section header collapses when clicked. TEXT OVERLAY and VIDEO start collapsed; click their headers to open them.
- The panel stays up only while the mouse is over it and fades out the moment the mouse leaves the panel area (or the window). Move the mouse back over the strip on the left to bring it straight back. A key press or a touch shows it for a couple of seconds instead, since neither has a hover. The mouse cursor stays visible over the display.
- **DETACH ↗** pops the whole panel into its own window so the visuals can go fullscreen on one display while you drive them from another. Every control stays in sync in both windows. **ATTACH ↙** brings it back.
- **Double-click any slider** to reset it to its default.

**Keyboard**

| Key | Action |
|---|---|
| Tab | Hide / show the panel |
| Space | Pause / resume shape time (video keeps playing) |
| F | Fullscreen |
| R | New random seed |
| 1 – 9, 0 | Shape A: 1 = OFF, 2 = ORBS, 3 = RINGS, 4 = SCOPE, 5 = WAVES, 6 = TUNNEL, 7 = MEMORY, 8 = LISSAJOUS, 9 = ALTITUDE, 0 = BLOBS |

Shortcuts are ignored while you're typing in the text box.

**Bottom buttons**
- **PAUSE** — freezes shape animation.
- **RESEED** — new random seed; generated shapes rebuild with a different layout.
- **FULLSCREEN** — same as F.
- **BEAT RESEED** — reseeds automatically on every detected kick. Turns the mic on if needed.
- **MIC** — turns the audio input on/off.

---

## 3. Modulation: the MOD DEPTH / LFO RATE / AUDIO MOD groups

Most sliders have a small indented group under them with three sub-sliders. These modulate the parent slider around its current value:

- **MOD DEPTH** (-100% … +100%) — how far an LFO swings the parameter. Negative values invert the swing. 0% = off.
- **LFO RATE** (0.02 Hz … 5 Hz) — speed of that LFO. Around 0.1 Hz is a slow breathe; 2–5 Hz is a flicker.
- **AUDIO MOD** (-100% … +100%) — how much the named audio band pushes the parameter. Each parameter listens to a specific band (shown in the label): BASS, LOW-MID, HI-MID or AIR. Negative values pull the parameter down when the band is loud.

LFO and audio modulation add together on top of the slider's own value, and the result is clamped to the slider's range.

---

## 4. TEXT OVERLAY

Draws text on top of the visuals, crisp at full fidelity and degraded along with the picture as FIDELITY drops.

- **Text box** — type your text. **Enter** starts a new line; every line is centred on its own and the whole block stays centred on the Y POSITION. Text is uppercase.
- **FONT STYLE** — LED (5×7 dot matrix), SPACE (thin sans), BOLD (heavy sans with drop shadow), MONO (monospace).
- **SCALE** — letter height. Modulatable.
- **Y POSITION** — vertical position of the text block, 10–90% of the screen.
- **SCATTER FX** — letters (or dots/segments) drift apart. Modulatable.
- **ROTATE FX** — the block spins around its centre. Modulatable.
- **PULSE FX** — per-letter brightness flicker. Modulatable.
- **SCAN LINES FX** — rows of the text drop out in a rolling scan pattern. Modulatable.

Colours come from the current palette.

---

## 5. VIDEO

A video file and/or a live camera can be drawn beneath the shapes. Both pass through invert, comic ink, fidelity, RGB split, glitch, points, paint brush, blur, trails, feedback and the display filter like everything else.

**Video file**
- **LOAD VIDEO** — choose a local file (anything the browser can play: MP4, WebM, MOV…). It starts playing immediately, muted.
- **PLAY / STOP** — STOP returns the play head to LOOP START.
- **LOOP** — repeat between LOOP START and LOOP END.
- **PLAY HEAD** — follows playback; drag to scrub. The readout shows time / duration.
- **LOOP START / LOOP END** — the region used by LOOP and by GRANULAR RESET. Labels switch from % to timestamps once a file is loaded. With LOOP off, playback stops at LOOP END.

**GRANULAR RESET** (needs the mic)
On every detected beat the video jumps to a random point inside the LOOP START–END region and repeats a short random-length "grain" from there until the next beat. The trigger has its own detector that gets more sensitive when the input is loud, so busy passages fire on smaller hits.
- **GRAIN MAX LENGTH** — longest grain the loop can pick (0.1–8 s). Grains are always at least 0.15 s.
- **GRAIN CROSSFADE** — the frame before each jump or loop-wrap is held and faded out over the new picture so cuts don't flash (0 = hard cut, default 150 ms). Capped at half the grain length for very short grains.

With the camera on, GRANULAR RESET also loops the last slice (up to 2 s) of live footage from the moment of each beat.

**Source grade**
- **EXPOSURE / TEMPERATURE / SATURATION / SHADOWS / MIDTONES / HIGHLIGHTS** — a per-pixel grade applied to both the video file and the camera, each graded before SOURCE MIX blends them (the held frames used by GRAIN CROSSFADE are graded too). All six sit above the CAMERA button. Everything at neutral costs nothing.

**Camera**
- **CAMERA ON/OFF** and a device selector.
- **SOURCE MIX** — crossfade between the video file (left) and the camera (right). A source that isn't running drops out of the mix.

---

## 6. SHAPE A, SHAPE B and CROSSFADE

Two shape slots draw on top of the video layer.

- Pick a shape in each slot. **OFF** draws nothing, so a slot can be disabled to let the video or background show through.
- **BACKGROUND ON/OFF** per slot — OFF skips that shape's own backdrop fills so only the main geometry is drawn. A few shapes go further and open windows in themselves: ALTITUDE drops its sea, TUNNEL leaves half its wall panels unfilled, BLACKHOLE's disc becomes a clear hole and MEMORY keeps only its bright stripes (see the shape notes below).
- **CROSSFADE** — mixes A and B. When Shape B has BACKGROUND OFF the slider becomes **OVERLAY**: A stays at full opacity and B is layered on top.
- **AUTO ON/OFF** — sweeps the crossfade back and forth slowly by itself.

Available shapes: ORBS, RINGS, SCOPE, WAVES, TUNNEL, MEMORY, LISSAJOUS, ALTITUDE, BLOBS, POLYLOCK, SONAR, AURORA, ODYSSEY, SUPERNOVA, BLACKHOLE, CONSTELLATION, GLITCH, HLINES, MOIRE, COLORBARS, SPIROGRAPH, PULSES, FOREST, SNOW, RAIN, TRIANGLES, RISING, DIAMONDS, HOLLOW, SOLAR, LIMINAL, SYNTH, GROVE, VAPORWAVE, ASTEROIDS, CITY, PLANET, JELLYFISH, OIL PAINT, NEON CITY, SCRATCH, SKYLINE, AMOEBAS, PLAYFIELD, SPRITES, MUNCH, PADDLES, QUILT, LIQUID LIGHT, MATRIX, HARMONIC.

Each shape reacts to the audio bands in its own way — SCOPE draws the raw waveform, DIAMONDS drives each ring from a different band, PLANET flies faster and dips lower on the bass, and so on. Experiment.

### Newer shapes

- **LIQUID LIGHT** — a 1960s liquid light show: coloured oil and water dyes squeezed between two clock glasses on an overhead projector, filling the whole screen. Three translucent dye sheets, each a field of seeded droplets, slide at slightly different speeds and filter the light multiplicatively, so where a yellow sheet crosses a cyan one you get green, like gels on a light table. Every cell is shaded as a lens — a dark meniscus line, a bright refracted band just inside it, a highlight on the lit side and a shadow on the far side — so merged cells read as bulging, wet oil bubbles. Clusters of tiny bubbles and a few stray saturated drops sit on top, and the whole plate ripples. Bass heats the plate (droplets swell and merge) and each bass hit sloshes all the sheets sideways with a spring-back; low-mids drive the flow; treble tightens the rims and swells the bubbles. DENSITY sets droplets per sheet, bubble clusters and stray drops. The plate is very slightly translucent (oil about 92% opaque, water about 87%), so a video or the other slot shows through faintly; with BACKGROUND OFF the water drops out completely and only the oil cells and bubbles remain. It renders on a 288-pixel-wide plate (352 at the top FIDELITY step) and is one of the heavier shapes.
- **MATRIX** — after John Whitney's *Matrix III* (1972). A troupe of identical polygon outlines (hexagons on most seeds, sometimes triangles or squares) is spread around a circular or Lissajous orbit by "differential" phasing: copy *i* sits at phase *i* × step along the path, and the step drifts slowly, so the troupe keeps locking into perfect n-fold symmetry and dissolving out of it. Copies are graded in size and each carries nested, shrinking outlines that lag slightly behind it — the film's hexagons within hexagons. Some seeds add a mirrored second troupe. Lines are additive white with palette tints on the inner rings, so it works well as an overlay. Bass swells the orbit and adds rings, low-mids drive the phase, treble brightens the lines. DENSITY sets the number of copies (5–18) and nested rings.
- **HARMONIC** — Whitney's vertical line and dot fields. An evenly spaced row of strokes is bent sideways and lifted by sines of the same drifting phase step, so the row folds, bunches at the folds and spreads again. Stroke length follows the live spectrum across the row; when the music is quiet the strokes collapse to dots. On about half the seeds, high DENSITY switches to a dense full-height coloured curtain, like the film's colour passages. Bass stretches the strokes, low-mids drive the motion, treble whitens them. DENSITY sets the number of strokes (8–60). Draws only lines, so it is transparent with BACKGROUND OFF.
- **PLANET** — a low-orbit flyover of a procedurally generated planet, a different world for every seed. The surface is a wrapping height map built from fractal and ridged noise (how mountainous it is varies by seed) with a field of up to 300 craters stamped on top: bowls that flatten the ground beneath them, broken uneven rims, ejecta aprons on the fresher ones and central peaks in the largest. About half of the worlds have liquid pooling in the low ground, with soft shorelines and a sun glint. Every pixel casts a ray at the sphere from a camera pitched toward the curved horizon; the ground is lit by a seeded sun (crater bowls sit in their own shadow), leans with the view for a sense of depth, and hazes out toward the limb, where a glowing atmosphere rim wraps the planet. The sky holds a seeded nebula, a star field, the sun and sometimes a moon. The flyover drifts forward slowly, banking gently as the heading wanders; RATE OF CHANGE and PAUSE apply. Bass pushes the speed and dips the altitude, low-mids swell the atmosphere, high-mids exaggerate the relief, air brightens the stars, sun and nebula. DENSITY sets how many craters are stamped, how much fine surface grain there is and how many stars are out. Colours for the terrain, liquid, rim, sun and nebula come from the palette. With BACKGROUND OFF the sky drops out and only the planet and its glowing rim are drawn. A new seed takes a moment to build the surface and moving DENSITY restamps the craters, so expect a brief hitch on those.

- **VAPORWAVE** (rewritten) — a neon spectrogram grid under a low-poly wireframe mountain range. The floor is a height field: frequency runs across the columns (mirrored about a calm centre lane) and time runs into the distance, so every sound appears as a ridge at your feet and travels toward the horizon (some seeds reverse the direction or put the bass at the edges). Grid segments carrying energy light up toward white or an accent colour and the cells beneath them glow as tiles. Bass pulses the line glow, horizon line, sun and scroll speed; low-mids stretch the mountains; highs pump their neon edges and the stars. The grid reads the analyser spectrum directly in 32 bands. DENSITY changes the whole picture: grid cell size, mountain mesh resolution and number of ranges (one to three), stars, light streaks, sun stripe count and scanline pitch. SEED picks one of three scenes — night wireframe, dusk with a silhouette range and striped sun, or daylight pastel — plus horizon height, camera height and colour roles from the palette.
- **MEMORY** (replaces PLASMA) — a warped field of soft flowing stripes with a sheet of fine lines twisting through a pinch point, both bent by the same swirl so the lines ride the flow. Bass tightens the swirl, low-mids push the stripes along, highs sharpen the stripe edges, and each line carries its slice of the spectrum as a zigzag. DENSITY raises the stripe frequency and the number of lines. With BACKGROUND OFF only the bright stripes and the lines remain.
- **SUPERNOVA** (replaces LATTICE) — a pinwheel of translucent triangles, each stepped down to a dark core and trailed by ghost copies, surrounded by lacy fractal web clusters with glowing nodes drifting out along spiral arms. Bass swells the pinwheel, low-mids spin it, each cluster breathes on its own band, highs light the nodes. DENSITY adds blades, ghost trails, clusters and web depth.
- **ODYSSEY** (replaces WOBBLE) — curved, tapered ribbons of light flung out of a white-hot core, with hairline streaks and a soft coloured bloom behind. Bass throws the ribbons further and pulses the core, each ribbon's length and width follow its own slice of the spectrum, highs brighten the streaks. DENSITY sets the number of ribbons and streaks. It paints no backdrop, so it works well as an overlay.
- **BLACKHOLE** (replaces ECHO) — a star-filled black disc with a bright rim, wrapped in stacked polar blobs whose lobes are the spectrum folded around the circle, thin wobbling orbit loops and curtains of fine waves down both screen edges. Each blob layer also throws one large wing on its own band; bass breathes the disc. DENSITY adds blob layers, orbits, curtain bands and stars. (The crown of straight radial rays has been removed.) With BACKGROUND OFF the centre of the disc is a clear window onto whatever is underneath (Shape A or video), with only the rim and a few inner stars drawn over it.
- **OIL PAINT** — a seeded nature landscape built from thousands of thick brush dabs: a mood (day, sunset, dusk, mist, storm or gold), hazed mountain ridges, a lake or meadow, trees, rocks and wildflowers over canvas grain. The painting is re-dabbed every few seconds with a slow crossfade so the brushwork breathes. Bass swells the sun glow, mids push the clouds, treble adds lake shimmer. DENSITY runs through the whole canvas — sky strokes, ridge texture, water strokes, grass, trees and flowers fade in as it rises — so an LFO on DENSITY sweeps it from flat wash to full impasto. SEED picks a new scene; the palette re-tints it and colours the flowers and sun.
- **NEON CITY** — a dense wireframe vector city in true 3D. The camera glides quickly and smoothly (no bob) down a boulevard between deep blocks of towers, ziggurats, spired towers, wedges, drum towers and bridged slabs, all drawn purely in lines with a hand-drawn feel (edges of varying pen weight, some missing or doubled), plus floor hatching, mullions, bracing, mast lattices, glowing neon outlines, sagging cables with lamps, and braced gantries with chasing lights. Dart-shaped ships and drones move at their own pace regardless of the camera. Bass surges the edge glow and speed, mids add traffic, treble flickers the neon. DENSITY controls block depth and count, how many edges and details are drawn, gantries, cables and traffic.
- **SKYLINE** — a seeded city skyline painted with OIL PAINT's cached-dab engine in a watercolour hand: translucent layered washes with bleeding rims on granulated paper. A mood (dawn, day, dusk, night or storm) sets the sky, sun or moon; a Manhattan-dense massing of fourteen depth rows receding into the haze — heights shaped by two or three tall-tower districts with lower fabric between, narrow slivers squeezed between wide blocks, spires, setbacks, stepped art-deco crowns, twin slabs, tapered tops, rooftop water tanks and blinking antennas — over distant hills, an optional waterfront with boats and tower reflections, and sometimes a suspension bridge. Two variants are re-dabbed and crossfaded so the brushwork breathes. Bass slowly swells the sun/moon glow, mids send bird flocks across, treble brings more window lights slowly on (and off) at night — nothing flashes. DENSITY runs through the whole picture in tiers — sky washes, clouds, facade texture, windows, water ripples, birds. SEED picks a new city; the palette tints the sky, towers and window light.
- **AMOEBAS** — a microscope field of amoebae crawling about. Each cell is a morphing membrane with pseudopods that bulge out, pull the body along and retract, a translucent cytoplasm with a pale ectoplasm rim, a nucleus with nucleolus, a contractile vacuole that slowly swells and empties, food vacuoles, and streaming granules that flow toward the leading pseudopod. Debris and flagellated bacteria drift through the field, and the cells gently nudge each other apart. Bass pushes pseudopods out faster, mids speed the wandering, treble stirs the granules. DENSITY sets how many amoebae (4–24), granules and bacteria there are.
- **GROVE** (replaces DAISIES) — a quiet forest painted in the hand of a hand-drawn animation background: tall mossy trunks receding into blue haze, a soft canopy overhead with pale sky showing through, a hazy wall of far woods, a winding path, moss clumps and pale stones on the ground, diagonal light shafts and a paper grain over everything, all painted with soft dabs on a low-res canvas so edges stay brushy. The camera drifts slowly down the path (at shape time, so RATE OF CHANGE and PAUSE apply); the woods are generated from position along the walk, so it never loops and never ends. Trunks are shades of brown, leaves and ground shades of green — each tree picks its own leaf green, with neighbouring clusters shifting between them — and the palette only lightly tints the sky, haze and light. SEED picks a mood (morning, noon, golden, mist, dusk) and the layout; colours are saturated hard for a bold, storybook look. Small black crows cross the far woods now and then, flying behind the trees, never in the foreground. Bass swells the light shafts and leans the camera in a touch, low-mids are the wind through the leaves (and send crows more often), high-mids ripple the moss, treble brings out drifting motes in the light — nothing flashes. DENSITY sets how many trees stand in each stretch (they fade in smoothly rather than popping), plus ground detail, canopy, light shafts and motes. With BACKGROUND OFF the sky, ground, path, canopy band and shafts are skipped and only the trees, crows and motes remain.
- **SNOW** (replaces ECLIPSE) — a snowstorm in RAIN's perspective volume: white flakes of random size, most small and deep in the volume with a few big soft-edged ones drifting past close to the camera, tumbling down through a wind that wanders slowly on its own and gusts up with the bass. Bass drives the gusts and the fall speed, mids swirl the flakes, treble brightens them. DENSITY sets the number of flakes. No floor and no backdrop: it draws over whatever background is set and is transparent with BACKGROUND OFF.
- **SCRATCH** — a pencil frantically scrubbing across the full width of the display, like someone sloppily scratching out the picture: straight passes at a new angle each time it flips direction, overshooting the edges, stepping row by row through a random band, with randomly varying pen pressure. About one box in five is scrubbed vertically instead. Strokes fade out over about two seconds so it never fills the screen (roughly 5–8% coverage per pencil). Draws only lines, so it works well as Shape B with BACKGROUND OFF as an overlay. Bass speeds the hand, treble shakes it, DENSITY adds up to three pencils.

### Lo-fi set
Five shapes in the spirit of early home-console graphics: a coarse grid of wide, hard-edged pixels, half-screen patterns mirrored onto the other half, one colour per band of rows, five fixed brightness steps and motion in whole-pixel jumps. With BACKGROUND OFF each draws only its blocks — everything around them is transparent (PLAYFIELD's dim colour bands are its only backdrop, and they are dropped).
- **PLAYFIELD** — a half-screen block pattern, mirrored (or sometimes repeated) onto the other half, held for a few rows at a time and scrolling downward in whole rows with a new colour per band. The spectrum runs down the screen, bass at the top, and sets how far each row reaches out from the centre line; the outermost block of every row is bright, so the outline is a blocky mirrored spectrum. Low-mids drive the scroll, bass hits shift the colours. DENSITY makes the blocks smaller (10 to 32 per half-screen).
- **SPRITES** — ranks of generated 8×8 mirror-symmetric creatures, a different colour on every sprite line, marching sideways in pixel steps with a two-frame walk. Each rank belongs to one band, which hops it upward and switches it to double-width pixels when loud. Bass hits advance the march and every eighth hit breeds a new set of creatures; highs fire thin shots up the screen. DENSITY adds ranks and copies.
- **MUNCH** — munching squares. Every cell computes a number from its coordinates (x XOR y and two relatives) and that number picks a slice of the spectrum; the cell lights, in three brightness steps, when its slice is sounding, so the carpet of nested squares is the spectrum folded through XOR. A sweeping diagonal stays lit in silence, bass hits advance the phase and every eighth hit swaps the operator. The grid is folded four ways about the centre. DENSITY steps the grid from 16 to 64 cells across.
- **PADDLES** — bat and ball. A wall of bricks hangs from the top, one colour per row, each column as deep as its slice of the spectrum is loud. Square balls with stepped trails rattle between the wall and a bat that chases the lowest ball, rebounding off whichever bricks are lit at that instant. Bass speeds the balls and kicks them sideways, low-mids widen the bat. DENSITY adds balls, brick columns and rows.
- **QUILT** — a one-dimensional cellular automaton, one generation per ring. New generations are born at the centre and push the older ones outward in whole-cell steps, wrapped around the centre with eight-fold symmetry. The spectrum seeds live cells into each new generation, low-mids set how fast generations are born, each ring's brightness follows its band, every eighth bass hit changes the rule (90, 30, 150, 110, 54) and every sixteenth changes the ring geometry (squares, diamonds, hourglass). DENSITY makes the cells smaller (8 to 36 rings to the screen edge).

Notes on existing shapes: HALO has been removed; CONSTELLATION's lines are twice as thick and keep a fixed weight (audio changes how far the links reach and how bright they are, not their thickness); SCOPE's trace, fill, bars and dots span the full width of the display; ALTITUDE with BACKGROUND OFF makes everything below sea level transparent (and drops the map grid), so the coastline opens and closes as the mids drain the sea; TUNNEL with BACKGROUND OFF leaves half of its wall panels unfilled — the open panels are fixed to the tunnel so they travel with it, and keep a thin frame line; ASTEROIDS rocks are see-through wireframes with uniform thin edges; COLORBARS responds to DENSITY (bar count); RAIN is now just the drops — the wet floor, its ripples and the streetlamp glow are gone, and each streak is a small teardrop (round belly, tapered tail, a glint on the nearer ones) that falls further down the frame before recycling, so it draws over whatever background is set and is transparent with BACKGROUND OFF (bass speeds the fall and stretches the tails, mids swell the drops, treble brightens them, DENSITY sets the count); FOREST now renders on a 480-pixel-wide buffer instead of 208 — about 2.3× the resolution — with the ground written per pixel, so mountains, trees, floor detail and clouds are much finer while keeping the crisp pixel look.

---

## 7. Core sliders

- **RATE OF CHANGE** — speed of shape animation. Modulatable.
- **DENSITY** — how much stuff each shape draws (particle counts, line counts, ring counts). Every shape responds to it, and it follows the MOD DEPTH / LFO RATE / AUDIO MOD settings live. Modulatable.
- **FIDELITY** (default 80%) — the master "image quality" control. Low values pixelate the picture, posterise the colours, add colour fringing and heavy scan lines, and also drop the internal render resolution; high values are sharp and clean. The readout shows the working buffer width. Text overlay follows it. Modulatable — an AUDIO MOD on FIDELITY is a classic move.

---

## 8. EFFECTS & MODULATION

All nine are modulatable (the FEEDBACK KEY controls are not).
- **FLUX LINES** — crackling static-electricity lines thrown out from the edges and corners of the picture. Each frame the picture is analysed for edges and corners, and a fixed seeded set of line sites snap to the strongest ones near them and grow outward, mostly down the brightness slope away from bright shapes (about a third climb the other way, out of dark holes), all bent by a shared slow swirl so neighbouring lines comb together. What gets drawn around each traced path is a jagged zigzag that is re-struck several times a second at the line's own rate — it snaps between shapes rather than easing, its brightness flickers per strike and now and then a line blinks out. Every site has its own character: hair-fine or thicker, short or very long, solid, a scattered trail of specks, or solid with a speck tail, with knots along some and forked side-sparks that split off the solid lines. Lines take their colour from the palette (near-white entries are skipped) and fade in and grow out instead of popping. The slider sets how many lines, how long and how bright; the AUDIO MOD here listens to the bass. Sits first in the chain, right after the shapes, so it is inked, degraded, split, glitched, painted, blurred, smeared into TRAILS and fed back like the picture it grew from. Saved in presets.
- **COMIC INK** — black ink outlines with flattened colour.
- **RGB SPLIT** — horizontal separation of the red, green and blue channels.
- **GLITCH** — beat-triggered picture faults. Each detected bass onset rolls the dice: whether to glitch at all, for how long (a few frames up to about half a second), how hard, and which faults are in the burst — slice tearing that wraps around the frame, scattered and stretched blocks, vertical roll, a wide red/blue colour-plane split, frame stutter, mirrored bands, mosaic bands and inverted bars. The layout is re-rolled every one to four frames inside a burst, louder hits glitch harder, and a beat landing mid-burst sometimes just extends it. The slider scales the odds, the length and the violence; at low settings many beats pass clean. With no audio running, bursts arrive at random intervals instead (more often as the slider goes up).
- **POINTS** — redraws the picture as a stippling: small points placed wherever a shape or the image has something to show, and only there — not on a grid. The frame is analysed in small cells and each earns points in proportion to how bright it is and, much more, to how strong an edge runs through it, so contours pick up a dense chain of points while flat lit areas get a sparse fill and dark areas (the backdrop included) get nothing. Point positions are seeded per cell, so the stipple holds still while the picture moves through it rather than flickering. Points take the colour of the picture beneath them (dim cells get a mild lift), edge points are a little larger, and the bass swells them all (the AUDIO MOD here listens to the bass band). The slider sets the scale, from fine dense stippling to coarse sparse points.
  - The slider sets the pitch: low is a fine, dense screen, high is wide spacing with fat dots. The first ~15% of travel fades the dots in over the untouched picture, so a small LFO or AUDIO MOD on a low setting breathes the screen in and out. Sits between GLITCH and PAINT BRUSH in the chain, so the dot field can be painted, blurred, smeared into TRAILS and fed back. Saved in presets.
- **PAINT BRUSH** — repaints the picture as a hand-painted work: a field of oil brush strokes that follow the image. A coarse layer of fat strokes blocks in the picture; a fine layer of small strokes appears only along edges; a canvas weave is laid over the top. Strokes run along the edges of the picture and, in flat areas, along a slow swirl. Every stroke has its own character — its own brush load (width), opacity, curvature and chroma, and one of five behaviours: **flat** (some with bristle hairlines through the body), **tapered** (fat to thin as the brush lifts), **dab** (a short fat touch), **dry brush** (three thin streaks with canvas showing between) and **broken** (two slightly disagreeing strokes laid over each other). Some flat and tapered strokes carry a lit ridge of raised paint along one side.
  - The painting is meant to be calm. Each stroke remembers its colour, direction and length and only eases toward what the picture now wants — colour settles over about two seconds, direction over three — and the fine edge strokes fade in and out rather than popping. The paint canvas is never wiped: new strokes are laid over the previous painting, so the image reworks itself like wet paint being pushed around instead of being redrawn.
  - The slider fades the painting in over roughly its first two-thirds; the rest loosens the brush a little (fewer, fatter strokes). The stroke positions are fixed, so LFO or audio modulation of the amount thins the strokes smoothly rather than shuffling them. Sits between POINTS and BLUR in the chain, so the strokes get blurred, smeared into TRAILS and fed back like everything else. Saved in presets.
- **TRAILS** — persistence; the previous frames linger.
- **BLUR** — softens the whole picture.
- **FEEDBACK** (0–200%) — analog video feedback. The output is fed back into itself, zoomed and rotated a little each pass. Above 100% the loop regenerates and blooms; keep it below 100% for controlled tunnels.
  - **FEEDBACK KEY** — a key section modelled on a video mixer (Roland V-4EX style). **OFF** is the normal additive loop. With a key selected the loop works like a mixer feeding back on itself: the live picture is the foreground, the chosen colour or brightness is cut out of it, and the zoomed and rotated previous output shows through the hole. **CHROMA GREEN** and **CHROMA BLUE** cut out that colour; **LUMA BLACK** and **LUMA WHITE** cut out dark or bright areas.
  - **KEY LEVEL** — how much is keyed out: low cuts only the pure key colour, high cuts a wide range around it.
  - **KEY GAIN** — the edge of the key: low is soft and semi-transparent, high is a hard cut.
  - With a key on, the FEEDBACK slider sets how long the loop persists (at 100% and above the keyed areas never fade). CHROMA GREEN pairs with BACKGROUND → GREEN SCREEN; LUMA BLACK works with the ordinary dark palette backgrounds. Soft glows over a green screen spill a little green into the loop — raise KEY LEVEL to clean it up. The key needs canvas-filter support in the browser; without it the loop stays additive. The key choice and both sliders are saved in presets.

---

## 9. DISPLAY FILTER

Whole-picture film and video looks, applied to the finished frame after every effect in EFFECTS & MODULATION and just before OUTPUT GRADE — so dust, static, tape wobble and tint land on top of text, trails and the feedback loop the way a real film or tape transfer would. The panel sits in the same place in the chain: below EFFECTS & MODULATION, above OUTPUT GRADE.
- **NONE**
- **OLD PHOTO** — warm sepia tint, desaturation, slight softening, flicker, gate weave, dust specks, stains and a warm vignette.
- **16MM FILM** — heavy grain, gate weave, dust, warm tint. No flicker.
- **35MM FILM** — fine grain, gentle weave, less dust, near-neutral tint. No flicker.
- **VHS TAPE** — row wobble, colour-channel offset, desaturation, flicker, warm tint, heavier scan lines. No static or noise.
- **CABLE TV** — block noise, softening, static, colour-channel offset, heavier scan lines.

**FILTER LEVEL** sets the intensity of the selected filter and is modulatable. It now scales every part of the look — tint, desaturation, softening, wobble, colour offset, block noise, static, grain, dust and vignette — so a low level is a light touch of the filter rather than a full filter with less grain.

The filter runs on the GPU at full output resolution, so it costs about the same at any FIDELITY setting; the noise, dust and static keep the pixel size of the working buffer, so they still read as film grain rather than screen noise.

---

## 10. OUTPUT GRADE

A colour grade applied to the finished frame, after every other effect, so it colours everything: shapes, video, text, trails and feedback. Screenshots, recordings and the virtual camera all include it.

- **EXPOSURE** — ±2 EV.
- **TEMPERATURE** — cool (blue) to warm (amber).
- **SATURATION** — 0% (mono) to 200%.
- **SHADOWS / MIDTONES / HIGHLIGHTS** — lift or crush each part of the tone curve.
- **TINT COLOR** — hue of a colour tint, 0–360° (red, yellow, green, cyan, blue, magenta, back to red). The readout takes on the chosen colour.
- **TINT AMOUNT** — 0–100%, how strongly the output is pushed toward the tint colour. Low values shift the colour without darkening the picture; 100% acts like a full colour gel.
- **RESET GRADE** — all eight back to neutral.

The first six are the same controls as the source grade in the VIDEO section, but that one affects only the video file and camera picture; this one affects the whole output (the tint is output-only). All eight are saved in presets.

---

## 11. COLOR PALETTE and BACKGROUND

- **Swatches** — click any palette. Shape colours, text colours and the default background all come from it.
- **AUDIO PALETTE** — on every detected beat, jump to a random palette. Turns the mic on if needed.
- **INVERT** — inverts all rendered colours.
- **BACKGROUND** — PALETTE (the palette's own background colour), or an exact **BLACK**, **WHITE** or **GREEN SCREEN** underneath the shapes. GREEN SCREEN is pure #00ff00 so it stays keyable in another app.

---

## 12. AUDIO INPUT

- **Slider** — overall audio sensitivity. It scales all the band levels and the beat detector.
- **Device selector** — choose the input. To react to music playing on the computer rather than a mic, set a loopback/virtual audio device as the input (BlackHole on macOS, VB-Cable or Stereo Mix on Windows).
- **Band meters** — Sub/Bass, Low Mid, High Mid, High/Air. These are the four bands the AUDIO MOD sliders and the shapes listen to. Each band auto-levels so quiet sources still use the full range.

The input is captured raw (no echo cancellation, noise suppression or auto gain) so the visuals see the real signal.

---

## 13. EXPORT

**SCREENSHOT** — saves the current frame as a PNG at the window's resolution, scan lines included.

**Record**
- **● START REC / ■ STOP REC** — records to an MP4 file (H.264/AAC where the browser supports it, otherwise AV1 or VP9 in MP4; Firefox writes WebM and the button says so).
- **Length dropdown** — 10 s, 30 s, 1 min, 2 min or ∞. Recording stops and downloads automatically at the limit. Elapsed / max time shows in the section header.
- Recordings are rendered at the resolution set in VIRTUAL CAMERA (default 1920×1080), regardless of window size.
- Audio is always included: pressing record turns the mic on if it isn't already. If the mic is refused you still get video and the button reads "■ STOP (NO AUDIO)".
- **REC AUDIO LEVEL** — target peak of the saved audio (default 70%, shown as about -3 dB). The recorder auto-levels the input up to this and limits anything louder, so exports come out at normal video loudness. The live analysis path is not affected.
- MIC OFF is blocked while recording; stop the recording first.

**VIRTUAL CAMERA**
Browsers can't register themselves as a webcam device, so this feature gets you as close as a page can:
- **VIRTUAL CAM** floats the live output as a picture-in-picture window — no title bar, always on top, natively sized to the chosen resolution (720P / 1080P / 1440P / 4K). Drag it as large as you like; the browser caps it at your display size.
- To use it as a webcam in Zoom, Discord, Resolume, TouchDesigner, etc.: in **OBS Studio** add a **Window Capture** of that window and press **Start Virtual Camera**, then choose **OBS Virtual Camera** in the other app. One-time setup; after that it's just the VIRTUAL CAM button each session.
- In browsers without picture-in-picture the button falls back to a plain window; press **F** or double-click inside it for a frameless fullscreen picture.

**PRESETS**
- **SLOT 1–8** with **SAVE / LOAD** — stored in this browser. Filled slots are marked with •.
- **EXPORT FILE / IMPORT FILE** — download or load a `.json` preset you can keep, share or move between machines.
- A preset captures every slider, the text, Shape A/B, filter, palette, background mode, all toggles, the loop range, recording length and level, virtual-camera resolution, and the seed. It does not include the loaded video file, the play head position, or the audio/camera device choice.

---

## 14. Signal chain (for the curious)

Background → video file / camera (graded, mixed) → Shape A / Shape B (crossfade or overlay) → FLUX LINES → INVERT → COMIC INK → FIDELITY post-processing (posterise, grain, colour fringing) → FIDELITY downscale → text overlay (fidelity-treated) → RGB SPLIT → GLITCH → POINTS → PAINT BRUSH → BLUR → TRAILS → FEEDBACK (with optional KEY) → DISPLAY FILTER (weave / tape wobble, colour offset, softening, tint and flicker, block noise, static, grain, dust and stains, vignette) → OUTPUT GRADE (including TINT) → scan lines.

Knowing the order helps: FEEDBACK recirculates everything up to and including the text and effects; the DISPLAY FILTER comes after it, so the film or tape look sits on top of the loop rather than being fed back into it; COMIC INK is early, so it inks the video, shapes and FLUX LINES but not the later effects.

---

## 15. Tips

- **Reactive but not chaotic:** put a modest AUDIO MOD (30–50%) on FIDELITY, TRAILS or RGB SPLIT rather than on RATE OF CHANGE.
- **Beat-driven cuts:** LOAD VIDEO → GRANULAR RESET ON → set LOOP START/END to the interesting part of the clip → raise GRAIN CROSSFADE if the cuts feel too harsh.
- **Live camera as instrument:** CAMERA ON, SOURCE MIX fully right, GRANULAR RESET ON, then set Shape A to OFF and Shape B to a sparse shape with BACKGROUND OFF as an overlay.
- **Keyable output:** BACKGROUND → GREEN SCREEN, both shapes with BACKGROUND OFF, filter NONE, FIDELITY high.
- **Keyed feedback:** BACKGROUND → GREEN SCREEN, FEEDBACK KEY → CHROMA GREEN, FEEDBACK around 100%. The shapes stay crisp in front while their own history tunnels away behind them instead of washing over them.
- **Windows onto another shape:** put BLACKHOLE, TUNNEL or ALTITUDE in Shape B with BACKGROUND OFF and slide OVERLAY up — Shape A (or the video) shows through the disc, the open panels or the sea.
- **Beat-cut chaos:** GLITCH around 40–60% with MIC ON fires on the kick only; add a little AUDIO MOD on GLITCH so louder passages glitch harder and more often.
- **Living painting:** PAINT BRUSH at 70–100% over a slow shape (AURORA, GROVE, JELLYFISH) or a still camera, RATE OF CHANGE low, a touch of TRAILS. Add 20–30% AUDIO MOD on PAINT BRUSH so the brush loosens on the loud parts and tightens back up in the quiet ones.
- **Stippled drawing:** POINTS around 20–50% over a high-contrast shape (LIQUID LIGHT, AMOEBAS, BLOBS, ORBS) with a touch of TRAILS and BLUR; add 30–50% AUDIO MOD on POINTS so the stipple coarsens and the dots swell on the kick. Put FEEDBACK under 100% behind it and the dots tunnel away.
- **Static overlay:** FLUX LINES at 30–60% over a high-contrast shape (SUPERNOVA, RINGS, text) so the sparks have edges and corners to grow from; add 40–70% AUDIO MOD so the static flares on the kick.
- **Lo-fi overlay:** put SPRITES, PADDLES or QUILT in Shape B with BACKGROUND OFF over a video or a smooth shape in A — only the blocks land on top.
- **Whitney over oil:** LIQUID LIGHT in Shape A, MATRIX or HARMONIC in Shape B with BACKGROUND OFF and OVERLAY up — the white line figures float over the slow-moving dyes. A little TRAILS gives the lines the film's phosphor lag.
- **Performing:** DETACH the panel to a second display, F for fullscreen on the main one, and save a few slots to jump between looks with SAVE/LOAD.
- **Better recording audio:** feed a virtual audio device (BlackHole / VB-Cable) instead of a microphone for a clean direct signal.

---

## 16. Troubleshooting

- **Nothing reacts to sound** — press MIC ON and allow access; check the device selector; raise the AUDIO INPUT slider. The band meters should move.
- **MIC ERR** — the browser refused the microphone. Check site permissions and that no other app has exclusive use of the device.
- **CAMERA ERR** — same as above for the camera; try a different device in the selector.
- **Video won't play** — the browser may not support that codec/container. Re-encode to H.264 MP4 or VP9 WebM.
- **Recording is WebM, not MP4** — the browser (typically Firefox) has no MP4 muxer. Use Chrome, Edge or Safari, or convert afterwards.
- **POPUP BLOCKED** — allow pop-ups for the file so the DETACH panel and virtual camera windows can open.
- **Everything feels slow** — lower FIDELITY (it also lowers the render resolution), reduce DENSITY, turn off FEEDBACK, BLUR and PAINT BRUSH, or switch off one shape slot. The DISPLAY FILTER is cheap (no per-pixel work at the output resolution) and POINTS stays around a few milliseconds: it stamps its points into a buffer no wider than 960 pixels. PAINT BRUSH draws several thousand strokes a frame; raising its slider actually makes it cheaper (fewer, fatter strokes). VAPORWAVE at high DENSITY with loud input is one of the heavier shapes at the top FIDELITY step. PLANET ray-casts every pixel of a 224-pixel-wide buffer each frame and pauses briefly to rebuild its surface on a new seed or a DENSITY change, so BEAT RESEED with PLANET will stutter on every kick. LIQUID LIGHT shades every pixel of a 288-pixel-wide plate (352 at the top FIDELITY step) and is the heaviest shape at high DENSITY; if it drags, lower DENSITY or FIDELITY.
- **Old preset loads a different shape** — PLASMA, WOBBLE, LATTICE and ECHO were replaced; presets that used them load MEMORY, ODYSSEY, SUPERNOVA and BLACKHOLE respectively. HALO, SEQUENCER, DANCER, WEB and PIXEL WORLD were removed; presets that used them load RINGS, SYNTH, ORBS, TUNNEL and VAPORWAVE respectively.
- **Presets vanished** — slots live in the browser's local storage for that file location; clearing site data or moving the HTML file resets them. Use EXPORT FILE for anything you want to keep.

<img width="1500" height="963" alt="NV Screen" src="https://github.com/user-attachments/assets/d385c4a5-95db-47ff-830c-84131803d643" />
