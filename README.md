A self-contained HTML lo-fi ambient and sound visualizer, video and webcam effects processor that responds to music. Tested in Chrome, Safari, Vivaldi.

Download the HTML to run locally or run directly from the GitHub page using this address: https://pittsburghmodular.github.io/pittsburghmodular/

<img width="1500" height="929" alt="Hello NV Screenshot" src="https://github.com/user-attachments/assets/cc41a4d6-a88b-48af-a9d6-bd9264b1c12e" />

# NULL VENTANA — User Guide

Null Ventana is a browser-based, audio-reactive visualizer and video mixer. Eight source layers — a live camera, two video files, a still image, three generative shapes and a text overlay — are stacked bottom to top in an order you can change by dragging, each with its own mute (and, for all but the text, its own mix), and the result runs through a chain of retro video effects. Almost everything can be modulated by LFOs and by whatever is coming into the audio input. Output can be screenshotted, recorded to MP4, floated as a virtual-camera source, and saved as presets.

Everything lives in one HTML file. Open it in a modern browser (Chrome or Edge recommended; Safari works; Firefox works but records WebM instead of MP4).

---

## 1. Quick start

1. Open `Null_Ventana.html` in your browser.
2. Open the **AUDIO INPUT** section, press **MIC ON** and allow microphone access. The header changes from OFF to the sensitivity percentage and the four band meters start moving.
3. Open **SHAPE A**, pick a shape from the dropdown (it reads SHAPE: … when closed), a palette under **COLOR PALETTE**, and drag that shape's **DENSITY** and **RATE OF CHANGE** to taste.
4. Press **F** for fullscreen and **Tab** to hide the panel.

Nothing is uploaded anywhere; audio, video and camera stay in the browser.

---

## 2. Layout and global controls

The control panel sits on the left. The canvas fills the rest of the window.

**The panel is the signal path, top to bottom.** Sources come first, in the order they are stacked (layer 1 at the bottom of the picture is at the top of the panel), then the global effects, then output, then housekeeping. The eight layers start in this order and can be rearranged (see **Layer order** below):

1. **CAMERA** — layer 1 (bottom)
2. **VIDEO FILE A** — layer 2
3. **VIDEO FILE B** — layer 3
4. **IMAGE** — layer 4
5. **SHAPE A** — layer 5
6. **SHAPE B** — layer 6
7. **SHAPE C** — layer 7
8. **TEXT OVERLAY** — layer 8 (top)
9. **GLOBAL EFFECTS** — RESOLUTION at the top, then the rest in chain order: pressure, static, ink, RGB, ASCII, fog, trails, glitch, paint, points, threshold, edges, contour, smear, dither, halftone, blur, feedback
10. **DISPLAY FILTER**
11. **COLOR PALETTE**, **OUTPUT GRADE**, **BACKGROUND**
12. **TRANSPORT** (pause, fullscreen, detach, reseed), **AUDIO INPUT** (mic, sensitivity, device, meters), **EXPORT**, **PRESETS**

Every source layer starts with a **MUTE** button, and every layer except the text overlay ends with a **MIX** slider. MUTE (red when on) silences that layer: it keeps running — the camera stream, video playback, grain loops and shape clocks all carry on — but nothing from it reaches the picture, so unmuting is instant. MIX is how much of the layer goes into the picture, over everything beneath it. There is no crossfader — set each layer's mix independently.

**Layer order**
- Drag any of the eight layer boxes up or down by its title bar to change where it sits in the stack. The picture restacks as you drag and the **LAYER n** labels renumber. Each layer title has a dotted grip on its left; with a mouse you can grab anywhere on the title, on a touch screen use the grip. A plain click still opens and closes the box, and the panel scrolls when you drag near its top or bottom edge.
- The panel always reads top to bottom as bottom layer to top layer, so dragging a box **down** the panel moves that layer **up** the stack.
- Any order works: a shape under a keyed video, the image on top of the shapes, the text behind a shape. The video and image titles show the layer number and the loaded file name side by side.
- The order is saved in presets and mirrored in the detached panel. There is no reset button; drag the boxes back, or load a preset saved with the order you want.

**Panel behaviour**
- Every section header collapses when clicked. All sections start collapsed; click a header to open it.
- The panel stays up only while the mouse is over it and fades out the moment the mouse leaves the panel area (or the window). Move the mouse back over the strip on the left to bring it straight back. A key press or a touch shows it for a couple of seconds instead, since neither has a hover. The mouse cursor stays visible over the display.
- **DETACH ↗** (in TRANSPORT) pops the whole panel into its own window so the visuals can go fullscreen on one display while you drive them from another. Every control stays in sync in both windows. **ATTACH ↙** brings it back.
- **Double-click any slider** to reset it to its default.
- **Drag a layer title** up or down to reorder the layers (see above).

**Keyboard**

| Key | Action |
|---|---|
| Tab | Hide / show the panel |
| Space | Pause / run — freezes the shapes, both video files and the camera |
| F | Fullscreen |
| R | New random seed |
| 1 – 9, 0 | Shape A, the first ten entries of the (alphabetical) shape list: 1 = OFF, 2 = 8-BIT MUNCH, 3 = 8-BIT PADDLES, 4 = 8-BIT PLAYFIELD, 5 = 8-BIT QUILT, 6 = 8-BIT SPRITES, 7 = ALTITUDE, 8 = AMOEBAS, 9 = ASTEROIDS, 0 = AURORA |

Shortcuts are ignored while you're typing in the text box.

**TRANSPORT**
- **PAUSE / RUN** — freezes everything that moves: shape time, both video files and the camera feed (a running camera grain loop picks up where it stopped).
- **FULLSCREEN** — same as F.
- **DETACH / ATTACH** — the pop-out panel, see above.
- **RESEED** — new random seed; generated shapes rebuild with a different layout (all three shape slots).
- **BEAT RESEED** — reseeds automatically on every detected kick. Turns the mic on if needed.

The **MIC ON/OFF** button lives in AUDIO INPUT (section 12).

---

## 3. Modulation: the MOD DEPTH / LFO RATE / AUDIO MOD groups

Most sliders — every effect, each layer's DENSITY, RATE OF CHANGE and MIX, and the image's SIZE — have a small indented group under them with three sub-sliders. These modulate the parent slider around its current value:

- **MOD DEPTH** (-100% … +100%) — how far an LFO swings the parameter. Negative values invert the swing. 0% = off.
- **LFO RATE** (0.02 Hz … 5 Hz) — speed of that LFO. Around 0.1 Hz is a slow breathe; 2–5 Hz is a flicker.
- **AUDIO MOD** (-100% … +100%) — how much the named audio band pushes the parameter. Each parameter listens to a specific band (shown in the label): BASS, LOW-MID, HIGH-MID or AIR. Negative values pull the parameter down when the band is loud.

LFO and audio modulation add together on top of the slider's own value, and the result is clamped to the slider's range.

---

## 4. Source layers 1–3: CAMERA, VIDEO FILE A, VIDEO FILE B

(Layer numbers in the section titles are the default order; drag the boxes to change it.)

The bottom three layers are live or recorded pictures. By default they are drawn beneath the shapes, and they pass through invert, ink, resolution, RGB split, fog, glitch, points, paint, blur, trails, feedback and the display filter like everything else. A source that isn't running (camera off, no file loaded, deck stopped) simply drops out of the stack.

Each of the three sections has the same shape, top to bottom: MUTE, its own controls, GRANULAR RESET, an eight-slider grade (six tone controls plus tint), a KEY section, then MIX.

**CAMERA (layer 1 by default)**
- **MUTE**, **CAMERA ON/OFF** and a device selector.

**VIDEO FILE A (layer 2 by default) and VIDEO FILE B (layer 3 by default)** — two independent decks with their own file, play head, loop, grain, grade and key.
- **MUTE** — silence this deck without stopping it.
- **LOAD VIDEO** — choose a local file (anything the browser can play: MP4, WebM, MOV…). It starts playing immediately, muted; the file name shows in the header next to the layer number.
- **START / STOP** — STOP returns the play head to LOOP START.
- **LOOP** — repeat between LOOP START and LOOP END.
- **FILL SCREEN** — every source is already scaled to cover the screen, so if a clip still shows black bars they are baked into the file (letterbox or pillarbox). With FILL SCREEN on, the deck measures those bars from a small copy of the picture about once a second and zooms past them so the real image fills the display. It follows the grade, key and grain hold frame, and is saved in presets.
- **PLAY HEAD** — follows playback; drag to scrub. The readout shows time / duration.
- **LOOP START / LOOP END** — the region used by LOOP and by GRANULAR RESET. Labels switch from % to timestamps once a file is loaded. With LOOP off, playback stops at LOOP END.

**GRANULAR RESET** (per source, needs the mic)
Each of the three sources has its own GRANULAR RESET button and grain sliders, so the camera and both decks can be granular independently. On every detected beat a video deck jumps to a random point inside its LOOP START–END region and repeats a short random-length "grain" from there until the next beat; the camera loops the last slice (up to 2 s) of live footage from the moment of the beat. The trigger has its own detector that gets more sensitive when the input is loud, so busy passages fire on smaller hits.
- **GRAIN MAX LENGTH** — longest grain the loop can pick (0.1–8 s; the camera is capped at 2 s). Grains are always at least 0.15 s.
- **GRAIN CROSSFADE** — the frame before each jump or loop-wrap is held and faded out over the new picture so cuts don't flash (0 = hard cut, default 150 ms). Capped at half the grain length for very short grains.

**Grade** (per source)
- **EXPOSURE / TEMPERATURE / SATURATION / SHADOWS / MIDTONES / HIGHLIGHTS** — a colour grade applied to that source alone, before it is mixed (the held frames used by GRAIN CROSSFADE are graded too). Each source has its own grade, so the camera can be cool and desaturated while video B is warm. Everything at neutral costs nothing.
- **TINT COLOR / TINT AMOUNT** — a colour gel over this source alone: pick a hue (the readout takes on the colour) and how strongly the layer is pushed toward it. The tint is luma-normalised, so moderate amounts recolour without darkening. It is baked into the same per-source lookup as the grade, so it costs nothing extra.
- The same eight controls appear in OUTPUT GRADE for the whole picture.

**KEY** (per source)
A keyer like the one on a video mixer: the chosen colour or brightness is cut out of this layer and the layers beneath show through the hole.
- **OFF / CHROMA GREEN / CHROMA BLUE / LUMA BLACK / LUMA WHITE** — what to cut: green or blue, or the dark or bright areas.
- **INVERT KEY** — flips the key: the keyed colour or brightness is what stays and everything else goes transparent (e.g. CHROMA GREEN + INVERT keeps only the green parts of a clip).
- **KEY LEVEL** — how much is keyed out: low cuts only the pure key colour, high cuts a wide range around it.
- **KEY GAIN** — the edge of the key: low is soft and semi-transparent, high is a hard cut.
- The key runs on the GPU alongside the grade (with a per-pixel fallback in browsers without canvas filters). Typical uses: green-screen footage in VIDEO FILE B keyed green over VIDEO FILE A; the camera on LUMA BLACK so its dark areas open onto the palette background; a clip on LUMA WHITE + INVERT so only its highlights land on top of the shapes.

**MIX** (per source)
- How much of this layer goes into the output, over the layers below it. 100% covers what is beneath; lower values blend. Modulatable — an LFO on a video deck's MIX fades it in and out, AUDIO MOD pumps it on the beat.

---

## 5. Source layer 4: IMAGE

A still picture, by default between the video decks and the shapes, always centred on the screen. The section, top to bottom:

- **MUTE** and **LOAD IMAGE** — any image the browser can show (PNG, JPEG, GIF, WebP…). The file name shows in the header next to the layer number.
- **SIZE** (10–300%) — how big the image is on the display. 100% covers the screen; smaller sizes leave the layers beneath showing around the picture, larger sizes zoom into its middle. Modulatable: the MOD DEPTH / LFO RATE / AUDIO MOD (BASS) group under it lets the image breathe on an LFO or swell on the kick (modulation can push it from 5% to 300%).
- **Grade** — the same EXPOSURE … HIGHLIGHTS and TINT COLOR / TINT AMOUNT as the video sources.
- **KEY** — the same keyer as the video sources (OFF / CHROMA GREEN / CHROMA BLUE / LUMA BLACK / LUMA WHITE, INVERT KEY, KEY LEVEL, KEY GAIN), so a logo on green or a picture's dark areas can open onto the layers below.
- **MIX** — modulatable, as on every layer.

The scaled copy is only redrawn when the size changes, so a static image costs one draw a frame. The loaded file is not part of a preset; everything else in the section is.

---

## 6. Source layers 5–7: SHAPE A, SHAPE B, SHAPE C

Three shape slots which, in the default order, draw on top of the image and video layers, Shape A lowest and Shape C highest. Each slot, top to bottom:

- **MUTE** — silence the slot without changing its settings.
- **Shape dropdown** — pick the shape. The closed control reads "SHAPE: NAME" so it is easy to spot; the open list shows plain names in alphabetical order, with **OFF** first. **OFF** draws nothing.
- **BACKGROUND ON/OFF** — OFF (the default) skips that shape's own backdrop fills so only the main geometry is drawn and the layers beneath show through. A few shapes go further and open windows in themselves: ALTITUDE drops its sea, TUNNEL leaves half its wall panels unfilled, BLACKHOLE's disc becomes a clear hole, MEMORY keeps only its bright stripes, MAGMA keeps only its glowing melt, COASTLINE drops its sand, FOREST drops its sky and CITY its asphalt (see the shape notes below). Turn it ON for the shape's full painted backdrop.
- **AUDIO BAND** — which part of the spectrum drives this shape. **ALL BANDS (SHAPE DEFAULT)** keeps the shape's own mapping (bass does one thing, treble another, as described in the shape notes). **BASS**, **LOW-MID**, **HIGH-MID** or **AIR** routes that one band into every reaction the shape has, so a shape that normally spins on the low-mids and flashes on the treble does both on the bass instead. Works for every shape.
- **AUDIO EFFECT** (0–200%) — how strongly the audio drives this shape: 0% holds it still (only the LFOs and its own drift remain), 100% is normal, 200% doubles every reaction. Both AUDIO BAND and AUDIO EFFECT are per slot, so the same shape can be quiet in A and wild in C.
- **DENSITY** — how much stuff the shape draws (particle counts, line counts, ring counts). Per slot, modulatable.
- **RATE OF CHANGE** — speed of that shape's animation. Per slot — each slot runs on its own clock — and modulatable.
- **MIX** — the slot's opacity over what is beneath it. Shape A defaults to 100%, B and C to 0%, so a fresh session shows one shape. Modulatable.

The same shape can sit in more than one slot: each slot keeps its own copy of the shape's internal state, its own seed and its own time offset, so the copies never move in lockstep.

Number keys 1–9 and 0 pick Shape A from the first ten entries of the list (see the keyboard table).

Available shapes (67, listed alphabetically as in the dropdown): 8-BIT MUNCH, 8-BIT PADDLES, 8-BIT PLAYFIELD, 8-BIT QUILT, 8-BIT SPRITES, ALTITUDE, AMOEBAS, ASTEROIDS, AURORA, BLACKHOLE, BLOB, BLOBS, BROKEN RING, CELL DIVISION, CHAOS CIRCLES, CITY, COASTLINE, COLORBARS, CONSTELLATION, DIAMONDS, DOT GRID, FLOW DOTS, FOREST, GLITCH, GROVE, HALLWAY, HARMONIC, HLINES, HOLLOW, JELLYFISH, LIMINAL, LIQUID LIGHT, LISSAJOUS, MAGMA, MATRIX, MEMORY, MESH GRID, MOIRE, NEON CITY, NODE GARDEN, NOISE CIRCLE, ODYSSEY, OIL PAINT, ORBS, PLANET, POLYLOCK, PULSES, RAIN, RESONANCE FIELD, RINGS, RISING, SCATTERED CUBES, SCOPE, SCRATCH, SKYLINE, SNOW, SOLAR, SONAR, SPIROGRAPH, SUPERNOVA, SWARM, SYNTH, TRIANGLES, TUNNEL, UNKNOWN PLEASURES, VAPORWAVE, WAVES.

Every shape follows RESOLUTION: at 100% the shapes are drawn up to 2048 pixels wide (never wider than the window), and the shapes that work in their own smaller buffers (PLANET, LIQUID LIGHT, MEMORY, FOREST, LIMINAL, OIL PAINT) grow those buffers with it.

Each shape reacts to the audio bands in its own way — SCOPE draws the raw waveform, DIAMONDS drives each ring from a different band, PLANET flies faster and dips lower on the bass, and so on. Experiment.

### WebGL-visualizer set
Six shapes in the spirit of browser music visualizers, drawn in plain 2D. All six keep their own state per slot, integrate their motion from time (so RATE OF CHANGE and PAUSE apply) and draw no backdrop, so they are transparent with BACKGROUND OFF and work as overlays.
- **MESH GRID** — a wireframe plane seen from a low, slowly yawing camera. Rings ripple out from the centre, the spectrum is laid along the radius (bass in the middle, treble at the rim), noise rolls across the whole sheet and every bass onset sends one extra crest outward. Bass raises the peaks, low-mids speed the ripple, high-mids stir the noise; the lines whiten at the crests. DENSITY sets the grid resolution.
- **SWARM** — three clouds of glowing particles, one per band: the bass cloud, the low-mid cloud and the high-mid cloud each swell with their own level (fast attack, slow release) as they drift around each other. Low-mids drive the orbit speed, high-mids stir the noise field that folds the clouds into one another, treble sizes and whitens every dot and throws sparks off the rims, and a bass onset flings all the particles outward before the orbits pull them back in. DENSITY sets the particle count (250–1,500).
- **UNKNOWN PLEASURES** — stacked oscilloscope traces. The live waveform is written into a short history and each line shows an older copy, so a hit rolls back through the stack like a ripple in time; a ridge in the middle, lifted by the spectrum, shapes every trace. Front lines hide the ones behind them (that occlusion is skipped with BACKGROUND OFF, so the layers beneath show through the whole stack). Bass raises the ridge, low-mids sharpen the trace, treble brightens the front lines. With no input it draws a synthetic wave. DENSITY sets the number of lines (10–36).
- **DOT GRID** — a field of dots breathing in rings from the centre: the spectrum runs along the radius, a slow swell circles outward and every bass onset launches a bright ring that travels to the edge. Dot size and brightness follow the local level; treble whitens the brightest dots. DENSITY sets the pitch of the grid.
- **BLOB** — a thin-lined wireframe ball whose surface is pushed in and out by rolling noise. Bass snaps the whole blob larger and throws spikes out of the noise crests on each kick, low-mids spin and stretch it, high-mids churn the noise and deepen the relief, treble whitens and thickens the front lines and lights the core; the spectrum runs pole to pole as extra relief. The back of the mesh is a faint ghost. DENSITY sets the mesh resolution.
- **HALLWAY** — a corridor of slabs receding to a vanishing point, walking slowly toward the viewer. The walls are what move: on every kick the near end of both walls, the floor and the ceiling hinges hard into the corridor while the far end stays put, then a pulse rolls down the hall to the vanishing point as the near end relaxes; between kicks the walls breathe with the bass and low-mids. Each slab also leans into the hall by its own band (nearest = bass, farthest = high-mids) through a smooth attack/release envelope, so the hall ripples rather than flickers. Beat timing runs on real time, so RATE OF CHANGE only changes the walking speed. DENSITY sets how many slabs line the hall.

### Generative pattern set
Seven shapes in the spirit of generative pattern studies: simple rules, drawn as lines, dots and small marks, that are orderly in silence and come apart with the sound. All keep their own state per slot and draw little or no backdrop, so they work as overlays.
- **FLOW DOTS** — a comb of points is released along the top edge and each one is followed down through a turning field, leaving a dot at a fixed interval. Near the top the dots hold a plain grid; further down the strands crowd and part. Bass deepens the turn, low-mids and high-mids slide the two waves that make it, the spectrum runs down the sheet (bass rows at the top) sizing the dots, and each kick drops a band of swollen dots down the strands. DENSITY sets the pitch of the comb.
- **NODE GARDEN** — nodes scattered across the field, each linked to every neighbour inside a radius. Slow noise carries the nodes around, so links form and break and clusters gather and dissolve. Bass widens the linking radius (a kick knits the whole garden together for a moment and sends a bright ring out through the links), high-mids speed the drift, every node swells with its own slice of the spectrum and treble whitens the busiest ones. DENSITY sets the number of nodes.
- **BROKEN RING** — a dense ring of small cells laid between concentric polygon outlines, of which only about a third are there at rest, so the ring is mostly open space with wandering islands of cells. It snaps to the sound: bass fills cells in and swells the ring, a kick closes more of it for an instant and flashes the outlines, low-mids turn it, high-mids churn the pattern, and each band of cells is lit by its part of the spectrum (bass on the inside). The number of sides comes from the seed. DENSITY sets the number of rings and of cells along each side.
- **SCATTERED CUBES** — a full isometric block of cubes with every cube pushed outward from the centre by its own amount, so the block hangs in the air as a slowly breathing cluster. Bass is the explosion: the spread tracks the bass level almost frame for frame, every kick blows the cluster apart and it is back together within a fraction of a second. High-mids churn the offsets, each layer is lit by its part of the spectrum and treble whitens the tops. DENSITY sets the cubes per side (3 to 6).
- **CHAOS CIRCLES** — rings of sketched circle outlines around a centre one, each ring holding six more than the last. In silence they sit in perfect order. Every kick throws each circle in its own direction and a spring pulls it back, high-mids keep them wandering, and the looser things get the rougher the hand that draws them. Each ring's circles swell with its part of the spectrum (bass in the middle), low-mids turn the rings against each other. DENSITY sets the number of rings.
- **NOISE CIRCLE** — a circle whose edge is pushed in and out by noise, drawn many times over, each copy reading the noise a moment later than the one inside it, so the outlines fan into a silk band that follows the same organic shape. Bass swells the circle, high-mids deepen the deformation and spread the band, the spectrum is wrapped round the rim (bass at the bottom, treble at the top, mirrored) and treble adds a fine tremor. BACKGROUND OFF drops the faint fill in the centre. DENSITY sets the number of outlines.
- **RESONANCE FIELD** — a grid of small marks pushed around by four wave sources at once, one per frequency band: long slow swells from the bass source, tight ripples from the treble one. Every mark is a slightly different shard (its own width, slant-cut ends, some tapered, some bulged) rather than a ruled dash; it is moved by the sum of the pushes and lies along it, and its length and colour are the summed wave height, so calm nodal lines and busy antinodes appear like the lines of a vibrating plate. A band's level is its source's strength, and a kick sends one sharp ring out of the bass source. DENSITY sets the grid pitch.

### High-resolution organic set
Three shapes drawn at the full size of the picture, so they stay sharp at every RESOLUTION. MAGMA and COASTLINE (and ALTITUDE, below) are worked out for every pixel by the graphics card and need WebGL; if the browser has none, MAGMA and COASTLINE show a short note instead and ALTITUDE falls back to its older low-resolution drawing. On a slow graphics card they lower their own working resolution to keep the frame rate up.
- **MAGMA** — the surface of a lava lake seen from above. A thick liquid folds slowly over itself and carries a skin of cooling crust: dark plates that drift, stretch and split, with the melt glowing in the cracks between them, heat soaking into the plate edges, and open pools of white-hot melt where the flow wells up. Bubbles of gas rise through it: each swells into a dome, thins, brightens and bursts with a flash, a ring running out across the melt and a spatter of glowing drops. Bass heats the lake (wider cracks, more open melt) and every hit sends up bubbles; low-mids drive the flow; treble makes the melt flicker. DENSITY sets the size of the plates (higher = smaller plates, more cracks) and how often bubbles rise. The colours are those of real lava, tinted a little by the palette. With BACKGROUND OFF the cold crust is left clear and only the glowing melt is drawn.
- **CELL DIVISION** — living cells under a microscope. Each cell is a soft bag: its membrane wobbles, flattens where it presses against a neighbour, and holds a nucleus, vacuoles, mitochondria and drifting granules. A grown cell divides the way cells do: the nucleus dissolves and the chromosomes appear, line up across the middle on a spindle of fibres, split and are drawn to opposite poles as the cell lengthens; the membrane pinches in at the waist, two new nuclei form and the waist closes. When the dish is full, an old cell breaks up and fades for every new one. Every bass hit starts a ready cell dividing and makes the membranes flinch; low-mids hurry a division along; high-mids make the membranes wobble; treble stirs the granules. DENSITY sets how many cells the dish holds (and so how big they are). Cells take the colours of the palette and hand them on, slightly changed, to their daughters. BACKGROUND OFF leaves only the cells.
- **COASTLINE** — a beach from the air, and what the waves do on it. The sea is on one side and the sand on the other (which side, the angle and the curve of the shore are seeded). Swells come in as long lines that bend to the shore and bunch up as the water shallows; each breaks at its own distance out into a white roller that leaves a field of foam behind it, thinning to a lace of bubbles and then to nothing. The roller runs up the sand as a thin sheet with a scalloped foaming edge, slows and drains back, leaving the sand dark and shining and a faint line of foam at the highest point it reached. The water is clear at the edge, turquoise and then deep blue further out, and glints in the sun. Low-mids bring the waves faster; bass builds them (higher run-up, breaking further out); high-mids keep the foam alive longer; treble makes the water glitter. DENSITY sets how closely the waves follow one another and how much foam they leave. With BACKGROUND OFF the sand is left clear: only the water and the foam are drawn.

### Newer shapes

- **LIQUID LIGHT** — a 1960s liquid light show: coloured oil and water dyes squeezed between two clock glasses on an overhead projector, filling the whole screen. Three translucent dye sheets, each a field of seeded droplets, slide at slightly different speeds and filter the light multiplicatively, so where a yellow sheet crosses a cyan one you get green, like gels on a light table. Every cell is shaded as a lens — a dark meniscus line, a bright refracted band just inside it, a highlight on the lit side and a shadow on the far side — so merged cells read as bulging, wet oil bubbles. Clusters of tiny bubbles and a few stray saturated drops sit on top, and the whole plate ripples. Bass heats the plate (droplets swell and merge) and each bass hit sloshes all the sheets sideways with a spring-back; low-mids drive the flow; treble tightens the rims and swells the bubbles. DENSITY sets droplets per sheet, bubble clusters and stray drops. The plate is very slightly translucent (oil about 92% opaque, water about 87%), so a video or the other slot shows through faintly; with BACKGROUND OFF the water drops out completely and only the oil cells and bubbles remain. The dye fields are read between pixels, so the rim of every cell is a smooth curve at any size. It renders on a 368-pixel-wide plate that grows with RESOLUTION (736 pixels at 100%) and is one of the heavier shapes.
- **MATRIX** — after John Whitney's *Matrix III* (1972). A troupe of identical polygon outlines (hexagons on most seeds, sometimes triangles or squares) is spread around a circular or Lissajous orbit by "differential" phasing: copy *i* sits at phase *i* × step along the path, and the step drifts slowly, so the troupe keeps locking into perfect n-fold symmetry and dissolving out of it. Copies are graded in size and each carries nested, shrinking outlines that lag slightly behind it — the film's hexagons within hexagons. Some seeds add a mirrored second troupe. Lines are additive white with palette tints on the inner rings, so it works well as an overlay. Bass swells the orbit and adds rings, low-mids drive the phase, treble brightens the lines. DENSITY sets the number of copies (5–18) and nested rings.
- **HARMONIC** — Whitney's vertical line and dot fields. An evenly spaced row of strokes is bent sideways and lifted by sines of the same drifting phase step, so the row folds, bunches at the folds and spreads again. Stroke length follows the live spectrum across the row; when the music is quiet the strokes collapse to dots. On about half the seeds, high DENSITY switches to a dense full-height coloured curtain, like the film's colour passages. Bass stretches the strokes, low-mids drive the motion, treble whitens them. DENSITY sets the number of strokes (8–60). Draws only lines, so it is transparent with BACKGROUND OFF.
- **PLANET** — a low-orbit flyover of a procedurally generated planet, a different world for every seed. The surface is a wrapping height map built from fractal and ridged noise (how mountainous it is varies by seed) with a field of up to 300 craters stamped on top: bowls that flatten the ground beneath them, broken uneven rims, ejecta aprons on the fresher ones and central peaks in the largest. About half of the worlds have liquid pooling in the low ground, with soft shorelines and a sun glint. Every pixel casts a ray at the sphere from a camera pitched toward the curved horizon; the ground is lit by a seeded sun (crater bowls sit in their own shadow), leans with the view for a sense of depth, and hazes out toward the limb, where the edge of the planet blends smoothly into a glowing atmosphere rim. The sky holds a seeded nebula, a star field, the sun and sometimes a moon. The flyover drifts forward slowly, banking gently as the heading wanders; RATE OF CHANGE and PAUSE apply. Bass pushes the speed and dips the altitude, low-mids swell the atmosphere, high-mids exaggerate the relief, air brightens the stars, sun and nebula. DENSITY sets how many craters are stamped, how much fine surface grain there is and how many stars are out. Colours for the terrain, liquid, rim, sun and nebula come from the palette. With BACKGROUND OFF the sky drops out and only the planet and its glowing rim are drawn. A new seed takes a moment to build the surface and moving DENSITY restamps the craters, so expect a brief hitch on those.

- **VAPORWAVE** (rewritten) — a neon spectrogram grid under a low-poly wireframe mountain range. The floor is a height field: frequency runs across the columns (mirrored about a calm centre lane) and time runs into the distance, so every sound appears as a ridge at your feet and travels toward the horizon (some seeds reverse the direction or put the bass at the edges). Grid segments carrying energy light up toward white or an accent colour and the cells beneath them glow as tiles. Bass pulses the line glow, horizon line, sun and scroll speed; low-mids stretch the mountains; highs pump their neon edges and the stars. The grid reads the analyser spectrum directly in 32 bands. DENSITY changes the whole picture: grid cell size, mountain mesh resolution and number of ranges (one to three), stars, light streaks, sun stripe count and scanline pitch. SEED picks one of three scenes — night wireframe, dusk with a silhouette range and striped sun, or daylight pastel — plus horizon height, camera height and colour roles from the palette.
- **MEMORY** (replaces PLASMA) — a warped field of soft flowing stripes with a sheet of fine lines twisting through a pinch point, both bent by the same swirl so the lines ride the flow. Bass tightens the swirl, low-mids push the stripes along, highs sharpen the stripe edges, and each line carries its slice of the spectrum as a smooth ripple — the lines are continuous curves with no corners. DENSITY raises the stripe frequency and the number of lines. With BACKGROUND OFF only the bright stripes and the lines remain.
- **SUPERNOVA** (replaces LATTICE) — a pinwheel of translucent triangles, each stepped down to a dark core and trailed by ghost copies, surrounded by lacy fractal web clusters with glowing nodes drifting out along spiral arms. Bass swells the pinwheel, low-mids spin it, each cluster breathes on its own band, highs light the nodes. DENSITY adds blades, ghost trails, clusters and web depth.
- **ODYSSEY** (replaces WOBBLE) — curved, tapered ribbons of light flung out of a white-hot core, with hairline streaks and a soft coloured bloom behind. Bass throws the ribbons further and pulses the core, each ribbon's length and width follow its own slice of the spectrum, highs brighten the streaks. DENSITY sets the number of ribbons and streaks. It paints no backdrop, so it works well as an overlay.
- **BLACKHOLE** (replaces ECHO) — a star-filled black disc with a bright rim, wrapped in stacked polar blobs whose lobes are the spectrum folded around the circle, thin wobbling orbit loops and curtains of fine waves down both screen edges. Each blob layer also throws one large wing on its own band; bass breathes the disc. DENSITY adds blob layers, orbits, curtain bands and stars. (The crown of straight radial rays has been removed.) With BACKGROUND OFF the centre of the disc is a clear window onto whatever is underneath (Shape A or video), with only the rim and a few inner stars drawn over it.
- **OIL PAINT** — a seeded landscape painted in oils: a mood (day, sunset, dusk, mist, storm or gold), hazed mountain ridges, a lake or meadow, trees, rocks and wildflowers over canvas grain. The scene is composed on the rule of thirds: the horizon lies on the upper or lower third line, the main stand of trees — one large tree with one or two companions — rises on one vertical third and the sun sits on the other, a smaller group stands further back, more trees are scattered through the middle distance and a hazy tree line runs along the far shore. Every mark is laid with a flat bristle brush: a stroke is streaked along its length, starts loaded and square and ends ragged, lighter along its upper edge and darker along its lower one the way a ridge of thick paint catches the light. Strokes follow the form they describe — long level strokes in the sky that bend round the sun, strokes down the slopes of the ridges, level drags across the water, short upward flicks for grass — and trees are built the way a painter builds them: trunk and boughs, foliage in shadow, local colour, then the lights on the sun's side. The painting is re-painted every few seconds, a layer at a time, and crossfaded so the brushwork breathes. Bass swells the sun glow, mids push the clouds, treble adds lake shimmer. DENSITY runs through the whole canvas in tiers — sky strokes, ridge texture, water strokes, grass, trees and flowers fade in as it rises. SEED picks a new scene; the palette re-tints it and colours the flowers and sun. It is painted at two to four times the resolution of its layout, following RESOLUTION, so the bristle marks stay crisp.
- **NEON CITY** — a dense wireframe vector city in true 3D. The camera glides quickly and smoothly (no bob) down a boulevard between deep blocks of towers, ziggurats, spired towers, wedges, drum towers and bridged slabs, all drawn purely in lines with a hand-drawn feel (edges of varying pen weight, some missing or doubled), plus floor hatching, mullions, bracing, mast lattices, glowing neon outlines, sagging cables with lamps, and braced gantries with chasing lights. Dart-shaped ships and drones move at their own pace regardless of the camera. Bass surges the edge glow and speed, mids add traffic, treble flickers the neon. DENSITY controls block depth and count, how many edges and details are drawn, gantries, cables and traffic.
- **SKYLINE** — a seeded city skyline painted with OIL PAINT's cached-dab engine in a watercolour hand: translucent layered washes with bleeding rims on granulated paper. A mood (dawn, day, dusk, night or storm) sets the sky, sun or moon; a Manhattan-dense massing of fourteen depth rows receding into the haze — heights shaped by two or three tall-tower districts with lower fabric between, buildings of more even width than before (the narrowest are twice as wide, the widest a quarter narrower), spires, setbacks, stepped art-deco crowns, twin slabs, tapered tops, rooftop water tanks and blinking antennas — over distant hills, an optional waterfront with boats and tower reflections, and sometimes a suspension bridge. Two variants are re-dabbed and crossfaded so the brushwork breathes. Bass slowly swells the sun/moon glow, mids send bird flocks across, treble brings more window lights slowly on (and off) at night — nothing flashes. DENSITY runs through the whole picture in tiers — sky washes, clouds, facade texture, windows, water ripples, birds. SEED picks a new city; the palette tints the sky, towers and window light.
- **AMOEBAS** — a microscope field of amoebae crawling about. Each cell is a morphing membrane with pseudopods that bulge out, pull the body along and retract, a translucent cytoplasm with a pale ectoplasm rim, a nucleus with nucleolus, a contractile vacuole that slowly swells and empties, food vacuoles, and streaming granules that flow toward the leading pseudopod. Debris and flagellated bacteria drift through the field, and the cells gently nudge each other apart. Bass pushes pseudopods out faster, mids speed the wandering, treble stirs the granules. DENSITY sets how many amoebae (4–24), granules and bacteria there are.
- **GROVE** (replaces DAISIES) — a walk through a real wood rather than a storybook one. Trunks of pine, broadleaf and birch stand at every distance and fade into the haze between them, each with its own girth, lean and bow, bark furrowed and lit down one side, moss at the foot, dead stubs on the pines and dark marks on the birches. The leaves are mostly overhead: crowns show whole only on distant trees, and the canopy closes in across the top of the view with light coming through its gaps. The floor is leaf litter and worn earth with patches of moss, ferns, grass, shrubs, saplings, stones and fallen wood, and spots of sun that shift on it; the brightest part of the picture is the haze at eye level beyond the trees. The camera drifts slowly down the path (at shape time, so RATE OF CHANGE and PAUSE apply) and the wood is generated from position along the walk, so it never loops and never ends. Colours are the muted greens, browns and greys of a real wood; the palette only tints the sky, the haze and the light. SEED sets the time of day and how much of the wood is pine. Small crows cross the far woods now and then, behind the trees. Bass swells the light shafts and leans the camera in, low-mids are the wind through the leaves (and send crows more often), high-mids stir the spots of sun on the ground, treble brings out drifting motes — nothing flashes. DENSITY sets how many trees stand in each stretch and how much undergrowth and canopy there is.
- **SNOW** (replaces ECLIPSE) — a snowstorm in RAIN's perspective volume: white flakes of random size, most small and deep in the volume with a few big soft-edged ones drifting past close to the camera, tumbling down through a wind that wanders slowly on its own and gusts up with the bass. Bass drives the gusts and the fall speed, mids swirl the flakes, treble brightens them. DENSITY sets the number of flakes. No floor and no backdrop: it draws over whatever background is set and is transparent with BACKGROUND OFF.
- **SCRATCH** — scratches, as on a strip of film or the back of a painted pane. Nothing is drawn until the sound asks for it: each bass hit drags one long scratch across the frame, and (from about a third of the DENSITY slider up) a treble or mid transient leaves a short one. A scratch is a single quick movement of the hand — it lands, runs in a slow arc with a little tremor, often ends in a hook, and thins out as the point lifts; the pressure wavers along it so the line swells, narrows and skips, and some have a fainter hairline running alongside. It is drawn in a fraction of a second and then fades. DENSITY also sets how many may be on screen at once; a harder hit makes a longer, slightly heavier scratch. Draws only thin lines, so it works well as an overlay.
- **JELLYFISH** — jellyfish swimming up through dark water, drawn the way a real medusa photographs: each bell is a smooth, nearly clear dome that contracts and relaxes (a quick squeeze, a slow recovery), brightest at its edge where the membrane is seen side-on, lit from above, with radial canals running from crown to margin and the four horseshoe gonads showing through it. Underneath hang ruffled, ribbon-like oral arms and a skirt of hair-fine tentacles that trail back along the way the animal has been travelling and ripple with every contraction. Far animals are smaller, dimmer and bluer. Bass makes them stroke harder, low-mids faster; high-mids brighten the membrane, treble the crown light and the margin. DENSITY sets how many animals there are and how many tentacles each trails.
- **CITY** — an isometric pixel-art city on an endless grid, scrolling past, drawn at twice its earlier resolution (416 pixels wide). No two neighbouring blocks are built alike: building blocks come as four lots, slabs, a large building ringed by little ones or a street of houses with gardens, and a building may be an office, a glass tower, a brick apartment house, a stepped stone tower, a shop with a striped awning, a house with a pitched roof or a warehouse, each with its own wall colour, height, share of lit windows and roof furniture; there are tower blocks, parks (a wood, a lawn round a pond, a formal garden, a sports ground or a playground, each on its own shade of grass) and squares with a fountain, a monument or a market of striped umbrellas. Traffic is cars, taxis, vans, buses and lorries. DENSITY raises the buildings, fills the empty lots, thickens the parks and adds traffic lanes; bass speeds the scroll and the traffic and makes cars hop, mids brighten windows, signs and paint, highs flare the headlights. With BACKGROUND OFF the asphalt is left clear.
- **LIMINAL** — a first-person walk through endless backrooms, lit the way the place is lit and no longer pixel art: every surface has a continuous texture and takes its brightness from the fluorescent panels in the ceiling (some lit, a few flickering, a few dead), so there are pools of light under the panels, dimmer stretches between and dark far rooms. Mono-yellow wallpaper with a faint woven stripe, stained and damp toward the floor; short beige carpet with old stains; ceiling tiles in their grid with a few water marks; a soft bloom round the lights, far rooms sinking into a brown murk, and a camera that bobs and sways. Bass quickens the walk, low-mids brighten the panels, treble lifts the vignette. DENSITY opens more doorways and lights more panels. The palette tints the place very slightly.

### 8-bit set
Five shapes in the spirit of early home-console graphics, listed in the dropdown with an **8-BIT** prefix (8-BIT PLAYFIELD, 8-BIT SPRITES, 8-BIT MUNCH, 8-BIT PADDLES, 8-BIT QUILT): a coarse grid of wide, hard-edged pixels, half-screen patterns mirrored onto the other half, one colour per band of rows, five fixed brightness steps and motion in whole-pixel jumps. With BACKGROUND OFF each draws only its blocks — everything around them is transparent (8-BIT PLAYFIELD's dim colour bands are its only backdrop, and they are dropped).
- **8-BIT PLAYFIELD** — a half-screen block pattern, mirrored (or sometimes repeated) onto the other half, held for a few rows at a time and scrolling downward in whole rows with a new colour per band. The spectrum runs down the screen, bass at the top, and sets how far each row reaches out from the centre line; the outermost block of every row is bright, so the outline is a blocky mirrored spectrum. Low-mids drive the scroll, bass hits shift the colours. DENSITY makes the blocks smaller (10 to 32 per half-screen).
- **8-BIT SPRITES** — ranks of generated 8×8 mirror-symmetric creatures, a different colour on every sprite line, marching sideways in pixel steps with a two-frame walk. Each rank belongs to one band, which hops it upward and switches it to double-width pixels when loud. Bass hits advance the march and every eighth hit breeds a new set of creatures; highs fire thin shots up the screen. DENSITY adds ranks and copies.
- **8-BIT MUNCH** — munching squares. Every cell computes a number from its coordinates (x XOR y and two relatives) and that number picks a slice of the spectrum; the cell lights, in three brightness steps, when its slice is sounding, so the carpet of nested squares is the spectrum folded through XOR. A sweeping diagonal stays lit in silence, bass hits advance the phase and every eighth hit swaps the operator. The grid is folded four ways about the centre. DENSITY steps the grid from 16 to 64 cells across.
- **8-BIT PADDLES** — bat and ball. A wall of bricks hangs from the top, one colour per row, each column as deep as its slice of the spectrum is loud. Square balls with stepped trails rattle between the wall and a bat that chases the lowest ball, rebounding off whichever bricks are lit at that instant. Bass speeds the balls and kicks them sideways, low-mids widen the bat. DENSITY adds balls, brick columns and rows.
- **8-BIT QUILT** — a one-dimensional cellular automaton, one generation per ring. New generations are born at the centre and push the older ones outward in whole-cell steps, wrapped around the centre with eight-fold symmetry. The spectrum seeds live cells into each new generation, low-mids set how fast generations are born, each ring's brightness follows its band, every eighth bass hit changes the rule (90, 30, 150, 110, 54) and every sixteenth changes the ring geometry (squares, diamonds, hourglass). DENSITY makes the cells smaller (8 to 36 rings to the screen edge).

Notes on existing shapes: HALO has been removed; CONSTELLATION's lines are twice as thick and keep a fixed weight (audio changes how far the links reach and how bright they are, not their thickness); SCOPE's trace, fill, bars and dots span the full width of the display; ALTITUDE with BACKGROUND OFF makes everything below sea level transparent (and drops the map grid), so the coastline opens and closes as the mids drain the sea; TUNNEL with BACKGROUND OFF leaves half of its wall panels unfilled — the open panels are fixed to the tunnel so they travel with it, and keep a thin frame line; ASTEROIDS rocks are see-through wireframes with uniform thin edges; COLORBARS responds to DENSITY (bar count); RAIN is now just the drops — the wet floor, its ripples and the streetlamp glow are gone, and each streak is a small teardrop (round belly, tapered tail, a glint on the nearer ones) that falls further down the frame before recycling, so it draws over whatever background is set and is transparent with BACKGROUND OFF (bass speeds the fall and stretches the tails, mids swell the drops, treble brightens them, DENSITY sets the count); FOREST is no longer pixel art: it is a smooth, realistic flight low over an alpine forest toward two ranges of mountains (ridged skylines with gullies, snow above an uneven snow line and haze at the foot), over ground of grass, bare earth and moss (and lakes on some seeds), between spruces, firs, pines and a few aspens that stand in four strengths of haze with their shadows, with grass tufts, ferns, stones, fallen logs and wildflowers between them — bass speeds the flight, low-mids steer, treble sets the trees swaying, DENSITY thickens the forest and undergrowth, and BACKGROUND OFF removes the sky; ALTITUDE's map is now drawn by the graphics card at the full size of the picture (up to 2048 pixels wide instead of a 192-pixel grid), with one more octave of terrain detail and thin, smooth contour, coastline and depth lines, every fifth contour heavier (without WebGL it falls back to the old drawing); SPIROGRAPH is one colour throughout — a palette colour picked by the SEED — in shades that run from deep to pale along the curve, instead of a rainbow.

---

## 7. TEXT OVERLAY — layer 8

The top layer by default. There it draws text over every source, crisp at full resolution and degraded along with the picture as RESOLUTION drops. Dragged lower in the stack, the text is mixed into the picture with the other layers instead: the layers above cover it, and PRESSURE, STATIC, INVERT, INK and RESOLUTION apply to it as they do to them. The section has no mix slider.

- **MUTE** — hides the text without clearing it; the text and all its settings are kept.
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

## 8. GLOBAL EFFECTS

Everything in this section acts on the whole mixed picture. RESOLUTION sits at the top of the section as the master control; the rest are listed in the order the chain applies them. All nineteen sliders are modulatable (the FEEDBACK KEY controls are not).
- **RESOLUTION** (default 100%, formerly FIDELITY) — the master "image quality" control. Low values pixelate the picture, posterise the colours, add colour fringing and heavy scan lines, and also drop the internal render resolution; high values are sharp and clean. The shapes are drawn 512, 768, 1024 or 1536 pixels wide as the slider rises and 2048 pixels wide at 100% (never wider than the window); the readout shows the percentage and the working buffer width. At 100% the posterise and grain pass is switched off entirely. Text overlay follows it. An AUDIO MOD (HIGH-MID) on RESOLUTION is a classic move. In the chain it acts after STATIC and before INK.
- **PRESSURE** — first in the chain, on the mixed sources before anything else: the picture is pulled along a slowly turning noise flow so it smears into streams, then combed with hair-fine strands (300–2,200) that follow the same flow in the colour of the picture where they start. The slider strengthens the flow and adds strands; the bass lengthens them. AUDIO MOD: LOW-MID.
- **STATIC** (formerly FLUX LINES) — crackling static-electricity lines thrown out from the edges and corners of the picture. Each frame the picture is analysed for edges and corners, and a fixed seeded set of line sites snap to the strongest ones near them and grow outward, mostly down the brightness slope away from bright shapes (about a third climb the other way, out of dark holes), all bent by a shared slow swirl so neighbouring lines comb together. What gets drawn around each traced path is a jagged zigzag that is re-struck several times a second at the line's own rate — it snaps between shapes rather than easing, its brightness flickers per strike and now and then a line blinks out. Every site has its own character: hair-fine or thicker, short or very long, solid, a scattered trail of specks, or solid with a speck tail, with knots along some and forked side-sparks that split off the solid lines. Lines take their colour from the palette (near-white entries are skipped) and fade in and grow out instead of popping. The slider sets how many lines, how long and how bright; the AUDIO MOD here listens to the bass. Sits second in the chain, right after PRESSURE, so it is degraded, inked, split, glitched, painted, blurred, smeared into TRAILS and fed back like the picture it grew from. Saved in presets.
- **INK** (formerly COMIC INK) — black ink outlines with flattened colour. It runs after the RESOLUTION downscale, so the ink lines are drawn over the pixelated picture instead of being pixelated with it.
- **RGB** (formerly RGB SPLIT) — horizontal separation of the red, green and blue channels.
- **ASCII** — the RGB-split picture as a grid of characters from a 70-step brightness ramp, coloured by the picture beneath, on the palette background. Character size grows with the slider; the bass brightens the ramp. AUDIO MOD: LOW-MID.
- **FOG** — banks of fog drifting across the picture: three sheets of soft noise sliding past each other over a thin even haze, a little heavier toward the bottom of the frame like ground fog. The fog is lit by the picture itself — in front of something bright it takes on that colour, mixed with a pale tone from the palette — and the same blurred light is added back as a glow, so lamps and bright shapes show through even thick fog. The slider runs from thin drifting wisps through heavy banks to a blanket in which only the lights show; bass thickens the fog a little and moves it faster. Sits after ASCII, so it drifts over everything so far, and the stages below (TRAILS, GLITCH, PAINT …) work on the fogged picture. AUDIO MOD: BASS.
- **TRAILS** — persistence; the previous frames linger. Sits here, before GLITCH, so the effects that follow work on the smeared picture. The range was halved: 100% on the slider is a long smear rather than a near-freeze, and modulation can't push it past that.
- **GLITCH** — beat-triggered picture faults. Each detected bass onset rolls the dice: whether to glitch at all, for how long (a few frames up to about half a second), how hard, and which faults are in the burst — slice tearing that wraps around the frame, scattered and stretched blocks, vertical roll, a wide red/blue colour-plane split, frame stutter, mirrored bands, mosaic bands and inverted bars. The layout is re-rolled every one to four frames inside a burst, louder hits glitch harder, and a beat landing mid-burst sometimes just extends it. The slider scales the odds, the length and the violence; at low settings many beats pass clean. With no audio running, bursts arrive at random intervals instead (more often as the slider goes up).
- **PAINT** (formerly PAINT BRUSH) — repaints the picture as a hand-painted work: a field of oil brush strokes that follow the image. A coarse layer of fat strokes blocks in the picture; a fine layer of small strokes appears only along edges; a canvas weave is laid over the top. Strokes run along the edges of the picture and, in flat areas, along a slow swirl. Every stroke has its own character — its own brush load (width), opacity, curvature and chroma, and one of five behaviours: **flat** (some with bristle hairlines through the body), **tapered** (fat to thin as the brush lifts), **dab** (a short fat touch), **dry brush** (three thin streaks with canvas showing between) and **broken** (two slightly disagreeing strokes laid over each other). Some flat and tapered strokes carry a lit ridge of raised paint along one side.
  - The painting is meant to be calm. A stroke, once laid, stays exactly as it is until the picture changes underneath it; only then is a new stroke painted there, on top of the old one. The paint canvas is never wiped, so a still picture holds perfectly still (and costs no brush strokes at all) and a moving one reworks itself like wet paint being pushed around instead of being redrawn. The view's slow breathing zoom and occasional frame jump are applied to the finished painting, so they do not disturb the strokes.
  - The slider fades the painting in over roughly its first two-thirds; the rest loosens the brush a little (fewer, fatter strokes; a looser brush applies to strokes painted from then on). The stroke positions are fixed, so LFO or audio modulation of the amount never shuffles them. Sits between GLITCH and POINTS in the chain, so the strokes are stippled, treated, blurred and fed back like everything else. Saved in presets.
- **POINTS** — redraws the picture as a stippling: small points placed wherever a shape or the image has something to show, and only there — not on a grid. The frame is analysed in small cells and each earns points in proportion to how bright it is and, much more, to how strong an edge runs through it, so contours pick up a dense chain of points while flat lit areas get a sparse fill and dark areas (the backdrop included) get nothing. Point positions are seeded per cell, so the stipple holds still while the picture moves through it rather than flickering. Points take the colour of the picture beneath them (dim cells get a mild lift), edge points are a little larger, and the bass swells them all (the AUDIO MOD here listens to the bass band). The slider sets the scale, from fine dense stippling to coarse sparse points.
  - The slider sets the pitch: low is a fine, dense screen, high is wide spacing with fat dots. The first ~15% of travel fades the dots in over the untouched picture, so a small LFO or AUDIO MOD on a low setting breathes the screen in and out. Sits after PAINT in the chain, so the painted picture is stippled and the dot field is then treated, blurred and fed back. Saved in presets.
- **Picture treatments** — six treatments in the spirit of WebGPU retro-effect tools, applied in this order after POINTS and before BLUR. They share one analysis: the frame is shrunk to a working buffer no wider than 768 pixels (so they cost the same at any window size) and each runs on it in turn; HALFTONE reads the result and draws its dots at full resolution. Every slider fades its treatment in over its first quarter and then drives its character; the group is skipped entirely when all six are at zero. Each has the usual MOD DEPTH / LFO RATE / AUDIO MOD group.
  - **THRESHOLD** — cuts the picture to two tones (palette background and white). The cut level rises with the slider; the bass nudges it. AUDIO MOD: BASS.
  - **EDGES** — Sobel edge detection in the picture's own colours. The first quarter lays the edges over the picture; the rest fades the picture out and whitens the edges until only glowing outlines remain. AUDIO MOD: HIGH-MID.
  - **CONTOUR** — topographic lines. Brightness is smoothed and quantised into bands (4–16, more as the slider rises, plus a couple on the bass) and a line in a palette colour is drawn wherever the band changes; the picture beneath fades to a dark wash. AUDIO MOD: LOW-MID.
  - **SMEAR** — runs of pixels brighter than a threshold are sorted by brightness along each row, so bright areas smear into streaks. The threshold falls as the slider rises (longer runs) and the bass pulls it lower; past halfway the streaks run vertically. AUDIO MOD: BASS.
  - **DITHER** — ordered (Bayer 8×8) dithering to a 1-bit screen per channel, dark tone from the palette background, in blocks that grow from 1 to 6 buffer pixels with the slider. AUDIO MOD: HIGH-MID.
  - **HALFTONE** — a grid of dots on the palette background, each sized by the brightness of its cell and coloured by it. The pitch widens with the slider; the bass fattens the dots. AUDIO MOD: BASS.
- **BLUR** — softens the whole picture.
- **FEEDBACK** (0–200%) — analog video feedback. The output is fed back into itself, zoomed and rotated a little each pass. Above 100% the loop regenerates and blooms; keep it below 100% for controlled tunnels.
  - **FEEDBACK KEY** — a key section modelled on a video mixer (Roland V-4EX style). **OFF** is the normal additive loop. With a key selected the loop works like a mixer feeding back on itself: the live picture is the foreground, the chosen colour or brightness is cut out of it, and the zoomed and rotated previous output shows through the hole. **CHROMA GREEN** and **CHROMA BLUE** cut out that colour; **LUMA BLACK** and **LUMA WHITE** cut out dark or bright areas.
  - **KEY LEVEL** — how much is keyed out: low cuts only the pure key colour, high cuts a wide range around it.
  - **KEY GAIN** — the edge of the key: low is soft and semi-transparent, high is a hard cut.
  - With a key on, the FEEDBACK slider sets how long the loop persists (at 100% and above the keyed areas never fade). CHROMA GREEN pairs with BACKGROUND → GREEN SCREEN; LUMA BLACK works with the ordinary dark palette backgrounds. Soft glows over a green screen spill a little green into the loop — raise KEY LEVEL to clean it up. The key needs canvas-filter support in the browser; without it the loop stays additive. The key choice and both sliders are saved in presets.

---

## 9. DISPLAY FILTER

Whole-picture film and video looks, applied to the finished frame after every effect in GLOBAL EFFECTS and just before OUTPUT GRADE — so dust, static, tape wobble and tint land on top of text, trails and the feedback loop the way a real film or tape transfer would. The panel sits in the same place in the chain: below GLOBAL EFFECTS, above the palette and OUTPUT GRADE.
- **NONE**
- **OLD PHOTO** — warm sepia tint, desaturation, slight softening, flicker, gate weave, dust specks, stains and a warm vignette.
- **16MM FILM** — heavy grain, gate weave, dust, warm tint. No flicker.
- **35MM FILM** — fine grain, gentle weave, less dust, near-neutral tint. No flicker.
- **VHS TAPE** — row wobble, colour-channel offset, desaturation, flicker, warm tint, heavier scan lines. No static or noise.

(CABLE TV has been removed; presets that used it load NONE.)

**FILTER LEVEL** sets the intensity of the selected filter and is modulatable. It now scales every part of the look — tint, desaturation, softening, wobble, colour offset, block noise, static, grain, dust and vignette — so a low level is a light touch of the filter rather than a full filter with less grain.

The filter runs on the GPU at full output resolution, so it costs about the same at any RESOLUTION setting; the noise, dust and static keep the pixel size of the working buffer, so they still read as film grain rather than screen noise.

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

The same eight controls appear as per-source grades in CAMERA, VIDEO FILE A / B and IMAGE, but those affect only their own layer before mixing; this one affects the whole output. All eight are saved in presets.

---

## 11. COLOR PALETTE and BACKGROUND

- **Swatches** — click any palette. Shape colours, text colours and the default background all come from it.
- **AUDIO PALETTE** — on every detected beat, jump to a random palette. Turns the mic on if needed.
- **INVERT** — inverts all rendered colours.
- **BACKGROUND** (its own section, below OUTPUT GRADE) — PALETTE (the palette's own background colour), or an exact **BLACK**, **WHITE** or **GREEN SCREEN** underneath every layer. GREEN SCREEN is pure #00ff00 so it stays keyable in another app.

---

## 12. AUDIO INPUT

The section header reads **OFF** until an input is running, then shows the sensitivity percentage.

- **MIC ON/OFF** — turns the audio input on or off (it was in TRANSPORT before). Recording, BEAT RESEED, AUDIO PALETTE and GRANULAR RESET turn it on for you when needed.
- **Slider** — overall audio sensitivity. It scales all the band levels and the beat detector. Each shape slot can further scale or re-route this with its own AUDIO BAND and AUDIO EFFECT controls.
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

---

## 14. PRESETS

- **SLOT 1–8** with **SAVE / LOAD** — stored in this browser. Filled slots are marked with •.
- **EXPORT FILE / IMPORT FILE** — download or load a `.json` preset you can keep, share or move between machines.
- A preset captures every slider (all three shapes' density, rate, mix and audio effect; every layer's mix, grade, tint, key and grain settings; the image size and its modulators), the text, Shape A/B/C and their AUDIO BAND choices, filter, palette, background mode, all toggles (mutes including the text overlay's, backgrounds, loops, fill screen, granular, key inverts), the layer order, both loop ranges, recording length and level, virtual-camera resolution, and the seed. It does not include the loaded video or image files, the play head positions, or the audio/camera device choice.
- Presets saved with the old single-video / crossfade panel still load: the crossfade becomes the Shape A and B mixes, the shared source grade and grain settings are copied to the camera and video A, and SOURCE MIX becomes the camera / video A mixes. Presets saved before the layers could be reordered load the standard order.

---

## 15. Signal chain (for the curious)

Background → the layers, bottom to top, in the order set in the panel — by default CAMERA (graded, tinted, keyed, mixed) → VIDEO FILE A → VIDEO FILE B → IMAGE (sized, graded, tinted, keyed, mixed) → SHAPE A → SHAPE B → SHAPE C (each at its own DENSITY, RATE, MIX and audio routing) → PRESSURE → STATIC → INVERT → RESOLUTION post-processing (posterise, grain, colour fringing; skipped at 100%) → RESOLUTION downscale → INK → TEXT OVERLAY (resolution-treated; when it is the top layer) → RGB → ASCII → FOG → TRAILS → GLITCH → PAINT → POINTS → THRESHOLD → EDGES → CONTOUR → SMEAR → DITHER → HALFTONE → BLUR → FEEDBACK (with optional KEY) → DISPLAY FILTER (weave / tape wobble, colour offset, softening, tint and flicker, block noise, static, grain, dust and stains, vignette) → OUTPUT GRADE (including TINT) → scan lines.

Knowing the order helps: FEEDBACK recirculates everything up to and including the text and effects; the DISPLAY FILTER comes after it, so the film or tape look sits on top of the loop rather than being fed back into it; INK is early, so it inks the video, shapes, PRESSURE and STATIC but not the later effects; TRAILS comes before GLITCH, so the glitches, paint, points and picture treatments cut into the smeared picture rather than being smeared themselves. Each source's own KEY happens as that layer is mixed in, so a keyed layer only ever opens onto the layers below it. A muted layer is simply skipped at its place in the stack. The TEXT OVERLAY is drawn after INK, straight onto the finished picture, only while it is the top layer; anywhere lower it is drawn in its place in the stack with the other layers and goes through PRESSURE, STATIC, INVERT, RESOLUTION and INK with them. FOG comes before TRAILS, so the fog is smeared, glitched, painted and fed back like the picture under it.

---

## 16. Tips

- **Reactive but not chaotic:** put a modest AUDIO MOD (30–50%) on RESOLUTION, TRAILS or RGB rather than on RATE OF CHANGE.
- **Beat-driven cuts:** LOAD VIDEO in deck A → its GRANULAR RESET ON → set LOOP START/END to the interesting part of the clip → raise GRAIN CROSSFADE if the cuts feel too harsh. Load a second clip in deck B with a different loop region and set both decks granular for two independent cutters.
- **Live camera as instrument:** CAMERA ON, its GRANULAR RESET ON, then Shape A MIX low or OFF and a sparse shape in Shape B with BACKGROUND OFF and MIX up.
- **Two-deck mixing:** load clips into VIDEO FILE A and B and put an LFO on deck B's MIX (or AUDIO MOD on it) — B fades over A on its own, and KEY on B cuts holes in it instead.
- **Green-screen compositing:** put green-screen footage in VIDEO FILE B, KEY → CHROMA GREEN, then anything in CAMERA or VIDEO FILE A shows through the hole. Raise KEY LEVEL to clean spill, lower KEY GAIN for softer edges.
- **Keyable output:** BACKGROUND → GREEN SCREEN, all shapes with BACKGROUND OFF (the default), filter NONE, RESOLUTION high.
- **Keyed feedback:** BACKGROUND → GREEN SCREEN, FEEDBACK KEY → CHROMA GREEN, FEEDBACK around 100%. The shapes stay crisp in front while their own history tunnels away behind them instead of washing over them.
- **Windows onto another shape:** put BLACKHOLE, TUNNEL or ALTITUDE in Shape B or C with BACKGROUND OFF and its MIX up — the layers beneath show through the disc, the open panels or the sea.
- **Beat-cut chaos:** GLITCH around 40–60% with MIC ON fires on the kick only; add a little AUDIO MOD on GLITCH so louder passages glitch harder and more often.
- **Living painting:** PAINT at 70–100% over a slow shape (AURORA, GROVE, JELLYFISH) or a still camera, RATE OF CHANGE low, a touch of TRAILS. Add 20–30% AUDIO MOD on PAINT so the brush loosens on the loud parts and tightens back up in the quiet ones.
- **Stippled drawing:** POINTS around 20–50% over a high-contrast shape (LIQUID LIGHT, AMOEBAS, BLOBS, ORBS) with a touch of TRAILS and BLUR; add 30–50% AUDIO MOD on POINTS so the stipple coarsens and the dots swell on the kick. Put FEEDBACK under 100% behind it and the dots tunnel away.
- **Terminal look:** ASCII at 30–50% over a video or a slow shape with RESOLUTION high; add 30% AUDIO MOD so the characters swell on the kick. CASSETTE palette gives amber-on-black.
- **Print look:** HALFTONE at 40–60% or DITHER at 20–40% over the camera; a touch of TRAILS softens the screen. THRESHOLD before HALFTONE gives a two-tone poster.
- **Glitch streaks:** SMEAR around 40% with 40–60% AUDIO MOD on it — the streaks lengthen on every bass hit and pull back between them. Push it past 50% for vertical rain.
- **Relief map:** CONTOUR at 40% over a soft shape (AURORA, LIQUID LIGHT) draws it as a map; EDGES at 60–80% over a hard one (ORBS, BLOBS, SUPERNOVA) leaves glowing outlines.
- **Combed picture:** PRESSURE at 30–60% — since it comes first in the chain, everything after it (INK, ASCII, the treatments) works on the combed picture; add a little FEEDBACK under 100% and the strands tunnel away.
- **Static overlay:** STATIC at 30–60% over a high-contrast shape (SUPERNOVA, RINGS, text) so the sparks have edges and corners to grow from; add 40–70% AUDIO MOD so the static flares on the kick.
- **Lo-fi overlay:** put 8-BIT SPRITES, 8-BIT PADDLES or 8-BIT QUILT in Shape C with MIX up over a video or a smooth shape in A — only the blocks land on top.
- **Three shapes:** with three slots and per-slot rates, try a slow full-screen shape in A (AURORA, LIQUID LIGHT), a mid-speed line shape in B (RINGS, HARMONIC, MESH GRID) and a fast sparse one in C (SNOW, SWARM, NODE GARDEN) at 40–60% MIX. MUTE lets you drop a layer in and out on cue without touching its mix.
- **Restack on the fly:** drag SHAPE A below VIDEO FILE A and key the video (LUMA BLACK or CHROMA GREEN) so the shape shows through the holes in the clip; or drag TEXT OVERLAY below a sparse shape so the shape passes in front of the lettering.
- **Lights in the fog:** FOG at 40–70% over NEON CITY, SKYLINE at night or JELLYFISH — the bright parts glow through while the rest sinks into the bank; 20–30% AUDIO MOD makes the fog roll in on the bass.
- **Lava and surf:** MAGMA or COASTLINE in Shape A with BACKGROUND OFF over a video — only the glowing melt, or the water and foam, land on top of the clip.
- **Corridor under a waveform:** HALLWAY in Shape A, UNKNOWN PLEASURES in Shape B with BACKGROUND OFF and MIX around 70% — the traces ripple over the breathing corridor.
- **Whitney over oil:** LIQUID LIGHT in Shape A, MATRIX or HARMONIC in Shape B with MIX up — the white line figures float over the slow-moving dyes. A little TRAILS gives the lines the film's phosphor lag.
- **Breathing logo:** load a PNG in IMAGE, SIZE around 40%, KEY → LUMA BLACK (or CHROMA GREEN for a green-backed file), then 20–40% AUDIO MOD (BASS) on SIZE so it pumps on the kick; a slow LFO at low depth keeps it alive between hits.
- **One band, many shapes:** put three shapes in A, B and C and set A's AUDIO BAND to BASS, B's to LOW-MID and C's to AIR — each layer moves to its own part of the mix. AUDIO EFFECT at 150–200% on the treble layer makes the highs sparkle.
- **Still shape, moving effects:** AUDIO EFFECT at 0% on a shape freezes its reactions while the global effects keep pumping on the same music.
- **Letterboxed clips:** FILL SCREEN on the deck crops away baked-in black bars, so a mixed bag of 4:3 and widescreen files all fill the frame.
- **Performing:** DETACH the panel to a second display, F for fullscreen on the main one, and save a few slots to jump between looks with SAVE/LOAD.
- **Better recording audio:** feed a virtual audio device (BlackHole / VB-Cable) instead of a microphone for a clean direct signal.

---

## 17. Troubleshooting

- **Nothing reacts to sound** — open AUDIO INPUT (its header reads OFF), press MIC ON and allow access; check the device selector; raise the sensitivity slider. The band meters should move. If one shape is still, check its AUDIO EFFECT isn't at 0%.
- **A layer is invisible** — check its MUTE button (red = muted) and its MIX, then its place in the stack: a layer above it at 100% MIX with its background on covers it. Drag it lower in the panel (which is higher in the stack), or turn the covering shape's BACKGROUND OFF.
- **MAGMA or COASTLINE shows a note instead of a picture** — the browser has no WebGL (or it is switched off). Turn on hardware acceleration in the browser settings. ALTITUDE falls back to its older low-resolution map in the same situation.
- **MIC ERR** — the browser refused the microphone. Check site permissions and that no other app has exclusive use of the device.
- **CAMERA ERR** — same as above for the camera; try a different device in the selector.
- **Video won't play** — the browser may not support that codec/container. Re-encode to H.264 MP4 or VP9 WebM.
- **Recording is WebM, not MP4** — the browser (typically Firefox) has no MP4 muxer. Use Chrome, Edge or Safari, or convert afterwards.
- **POPUP BLOCKED** — allow pop-ups for the file so the DETACH panel and virtual camera windows can open.
- **Everything feels slow** — RESOLUTION now defaults to 100%, which draws the shapes 2048 pixels wide: four times the pixels of the 1024 step, and for most shapes four times the work. Lowering RESOLUTION a little (92–99% is 1536 wide, 85–91% is 1024) is the first thing to try. Most effects and the heaviest shapes have been through two profiling passes (large gradients and vignettes painted once and reused, scratch buffers kept in main memory, integer pixel loops, no GPU read-backs in the RESOLUTION chain, SVG channel filters replaced with plain composites), so also make sure you're on the latest file. Then — reduce DENSITY, turn off BLUR and the picture treatments (TRAILS and FEEDBACK keep their memories at a working size no wider than 1280 pixels and PAINT only repaints the strokes whose part of the picture has changed, so those three cost about the same on a 4K or Retina window as on a laptop) (each active one is a pass over a 768-pixel-wide buffer; CONTOUR, SMEAR and PRESSURE are the heaviest), or set a shape slot to OFF or 0% MIX (a slot at 0% costs nothing). Two video decks with grades and keys cost two graded draws a frame, which is cheap on the GPU path. The DISPLAY FILTER is cheap (no per-pixel work at the output resolution) and POINTS stays around a few milliseconds: it stamps its points into a buffer no wider than 960 pixels. PAINT costs the most over a fast-moving picture (every changed area is re-stroked) and almost nothing over a still one; raising its slider makes it cheaper (fewer, fatter strokes). FOG is built on small canvases and costs the same at any window size. VAPORWAVE at high DENSITY with loud input is one of the heavier shapes at the top RESOLUTION step. The heaviest shapes at 100% RESOLUTION are SUPERNOVA, FOREST, LIQUID LIGHT, MEMORY, JELLYFISH, GROVE and LIMINAL. PLANET ray-casts every pixel of a 224-pixel-wide buffer each frame (448 at 100% RESOLUTION) and pauses briefly to rebuild its surface on a new seed or a DENSITY change, so BEAT RESEED with PLANET will stutter on every kick. LIQUID LIGHT shades every pixel of a 368-pixel-wide plate (736 at 100% RESOLUTION) and is among the heaviest shapes at high DENSITY; if it drags, lower DENSITY or RESOLUTION. MAGMA, COASTLINE and ALTITUDE are drawn by the graphics card and scale their own working resolution down on slower cards.
- **Old preset loads a different shape** — PLASMA, WOBBLE, LATTICE and ECHO were replaced; presets that used them load MEMORY, ODYSSEY, SUPERNOVA and BLACKHOLE respectively. HALO, SEQUENCER, DANCER, WEB and PIXEL WORLD were removed; presets that used them load RINGS, SYNTH, ORBS, TUNNEL and VAPORWAVE respectively. WAVY FORM and BASS BALL were renamed UNKNOWN PLEASURES and BLOB and load as such. PLAYFIELD, SPRITES, MUNCH, PADDLES and QUILT only gained their 8-BIT prefix; presets that used them load unchanged.
- **Video shows black bars** — turn on the deck's FILL SCREEN; the bars are part of the file and it zooms past them. A clip that fades fully to black keeps its last measured crop until the picture returns.
- **Old preset looks different** — it was saved with the crossfade panel; see PRESETS for how the old controls map onto the layers. Shape backgrounds now default to OFF and RESOLUTION to 100%, but a preset restores whatever it saved.
- **Presets vanished** — slots live in the browser's local storage for that file location; clearing site data or moving the HTML file resets them. Use EXPORT FILE for anything you want to keep.

<img width="1500" height="963" alt="NV Screen" src="https://github.com/user-attachments/assets/d385c4a5-95db-47ff-830c-84131803d643" />
