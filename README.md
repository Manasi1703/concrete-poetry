# Concrete Poetry

Type one emotion. Get a poem whose words *are* the shape of the feeling.

Concrete poetry is poetry where the layout carries the meaning: a poem about the sun spirals like a sun, a poem about falling apart literally falls apart. This page does that for any emotion you type: it writes a short poem, picks a shape for the feeling, and builds the shape out of the poem's own letters, one letter at a time.

Made by Manasi.

## Try it

It's a single HTML file with no build step.

1. Open `concrete-poetry.html` in a modern browser (Chrome, Safari, Firefox, Edge).
2. Type an emotion — `joy`, `lazy`, `heartbreak`, `confused`, anything — and press **write**.
3. Press **another** for a new arrangement of the same feeling.

An internet connection is needed the first time, to load the fonts and libraries from their CDNs.

## What you'll see

| You type | The poem becomes |
|---|---|
| happy, joy | a sun: the poem spirals inward, fragments radiate as rays |
| love | a heart filled edge to edge with text |
| anger | a flickering flame |
| sad | a teardrop |
| lonely | words trickling down the page and shrinking, like the mouse's tale in *Alice in Wonderland* |
| terrified | the first lines hold, then the rest falls apart letter by letter |
| confused | one line of text that keeps crossing itself in a knot |
| disappointed | lines that sag a little more each time |
| despair | letters running down the page like rain |
| nervous | trembling letters with a shaky after-image |
| peaceful | each line riding its own slow wave |
| lazy | a sloth |
| jealous | a coiled snake |
| proud | a crown |

There are around 190 built-in emotions, each with its own shape. Related forms match too (`terrifying` → `terrified`). A word that isn't on the list still gets a real shape, along with a poem written around that word.

## Controls

- **Scroll or pinch** — zoom toward the cursor, up to 4×. Zoom all the way out to snap back.
- **Drag** — move the poem around when zoomed in, so you can read it closely.
- **Drag the sun** — at full view, the sun spins like a dial and coasts to a stop.

## How it works

Everything lives in `concrete-poetry.html`.

1. **Words → shape + poem.** `WORDS` maps each emotion to a shape and a poem bank (joy, hope, love, anger, sadness, loneliness, fear, calm, surprise, weary). Each bank holds eight lines; the poem is a shuffle of them, with `{e}` replaced by your word.
2. **Shape → letter positions.** There are two kinds of shape:
   - **Layouts** (`LAYOUT`) place text along a path: spiral, waves, knot, zigzag, rings, rain, and so on.
   - **Silhouettes** take an emoji, draw it to a hidden canvas, read its outline from the alpha channel, and fill that outline row by row with justified text, like the pages of *House of Leaves*.
3. **Letters → WebGL.** Each letter is one instanced quad in [Three.js](https://threejs.org), cut from a font atlas drawn once on a canvas. A small shader moves each letter along a hop from just below its final spot and squashes it a little as it lands.
4. **Animation.** [GSAP](https://gsap.com) drives one progress value from 0 to 1. Each letter has its own delay, so the shape builds in reading order over 6–14 seconds, depending on how long the poem is.

### Built with

- [Three.js](https://threejs.org) 0.160 (WebGL rendering)
- [GSAP](https://gsap.com) 3.12 (animation)
- [Courier Prime](https://fonts.google.com/specimen/Courier+Prime) and [Averia Serif Libre](https://fonts.google.com/specimen/Averia+Serif+Libre) (Google Fonts)

## Make it your own

- **Add an emotion:** add a line to the `WORDS` list in the form `word shape bank`, for example `giddy 🎠 joy`. The shape can be any emoji or a layout name (`spiral`, `heart`, `tear`, `flame`, `tail`, `scatter`, `waves`, `burst`, `rings`, `knot`, `zigzag`, `droop`, `rain`, `echo`, `jitter`).
- **Write new lines:** edit a bank in `POEMS`. Use `{e}` wherever the typed word should appear.
- **Change the pace:** `JUMP` sets how long each letter spends mid-hop, and the duration `D` in `make()` sets how long the whole build takes.

## Notes

- The emoji silhouettes depend on the system's emoji font, so shapes can look slightly different on Mac, Windows and Android. Without an emoji font, a silhouette shape falls back to a heart.
- If your system is set to reduce motion, the poem appears already built, with no hop animation.

## Inspiration

Reference pieces: the hand-drawn sun poem *I Am Your Sun*, Lewis Carroll's mouse's tale from *Alice's Adventures in Wonderland*, the shaped pages of Mark Z. Danielewski's *House of Leaves*, and typographic text-portraits.
