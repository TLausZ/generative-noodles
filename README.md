# generative-noodles

Bendy noodle segments grown into a grid, drawn as SVG for pen plotters. Runs in the
browser, no build step and no dependencies.

A web rewrite of [cadin/generative-noodles](https://github.com/cadin/generative-noodles)
by [Cadin Batrack](https://github.com/cadin), which is a Processing sketch. All credit
for the concept goes there.

![Screenshot](screenshot.png)

## Usage

Open `index.html` in a browser, or use the hosted version. Sliders sit in the left
panel, graphics and the mask in the right one; both fold away at the flap on their
inner edge.

**`R`** randomize · **`G`** grid · **`X`** paint blocked cells · **`I`** mask image ·
**`S`** save an SVG · **`H`** and **`E`** fold the panels

Paper is in centimetres, the button next to the Paper heading switches to inches. The
saved SVG carries that real size, so a plotter picks up the right dimensions without
scaling, and every setting rides along in a comment at the top of the file, seed
included.

## Blocking cells

Noodles avoid blocked cells, which is how you shape the drawing. Press **`X`** and
paint them, or load a black and white image with **`I`**: cells over dark pixels are
blocked. **Invert mask** swaps blocked and open, for a loaded image as well as for
cells you painted. Neither the blocked cells nor the grid end up in the saved SVG.

## Graphics

Ends and straight sections can carry your own SVG shapes: **Head** is the end cap,
**Tail** the other end, **Joiner** a piece that drops into straight sections, as often
as the Joiners slider says. Where a graphic sits, the outline is cut open and the shape
carries the line across.

Draw it on a square viewBox, vertically, with the noodle edges down the left and right
sides and the connection along the bottom edge; a joiner connects top and bottom. That
is the convention of the original, shown in the diagram under the buttons. Keep your
shapes to single lines: a traced outline gives every stroke two edges, which a plotter
then draws twice. Colour and stroke width in the file are dropped in favour of the pen
size from the panel.

Six SVGs sit next to `index.html` to start from: `roundEnd`, `twist` and `twistFill`,
plus `fingerHead`, `fingerTail` and `fingerJoiner` measured off the original diagram.

## How it works

Noodles are self-avoiding walks over a grid, from a seeded generator so a drawing can
be reproduced. Because the grid keeps every turn at 90 degrees, the outline needs no
offset curve maths: straight cells are parallel lines, corners are concentric quarter
arcs, ends are half-circle caps. One closed path per noodle, cut open where a graphic
or a crossing sits.

Open `index.html?test=1` for the geometry self check; the result lands in the page
title.

## License

MIT, see [LICENSE](LICENSE). The original Processing sketch is released under the
Unlicense.
