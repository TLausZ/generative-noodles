# generative-noodles

Bendy noodle segments grown into a grid, drawn as SVG for pen plotters. Runs in the
browser, no build step and no dependencies.

A web rewrite of [cadin/generative-noodles](https://github.com/cadin/generative-noodles)
by [Cadin Batrack](https://github.com/cadin), which is a Processing sketch. Same idea,
without Processing. All credit for the concept goes there.

![Screenshot](screenshot.png)

## Design

Sepia survey map, one warm colour family, no shadows and no transitions. The
tokens live in [DESIGN.md](DESIGN.md) and come from the Bitcoin Wiki Visualizer.

## Usage

Open `index.html` in a browser, or use the hosted version.

Sliders sit in the left panel, graphics and the mask in the right one. Both fold
away at the small flap on their inner edge.

**`R`** randomize · **`G`** toggle the grid · **`X`** paint blocked cells ·
**`I`** load a mask image · **`S`** save an SVG · **`H`** and **`E`** fold the panels

Every drawing comes from a seed. Type a seed back into the panel and the same noodles
return, so a plot you liked is never lost.

Paper is measured in centimetres, and the button next to the Paper heading switches to
inches without changing the sheet. The saved SVG carries that real size, so a plotter
or a print dialog picks up the right dimensions without scaling, and all settings ride
along in a comment at the top of the file.

## Blocking cells

Noodles avoid blocked cells, which is how you shape the drawing. Press **`X`** and
paint them with the mouse; drag to paint a run of cells, drag again over a blocked
cell to clear it. The layout regrows from the same seed when you let go.

A mask image does the same thing from a picture: **`I`** loads one, scales it to fit
the grid, and blocks every cell sitting over a dark pixel. **Invert mask** turns that
around, so the noodles grow inside the dark shape instead of around it. Space left
over by a mismatched aspect ratio counts as blocked either way. Change the grid size
and the mask is reapplied by itself. Painting by hand from then on drops the mask.

Blocked cells and the grid are drawing aids and never end up in the saved SVG.

## Crossings

With **Let noodles cross** on, a noodle may run straight over one that is already
there, as long as it meets it at a right angle in a straight section and the cell
behind is free. That includes crossing its own body: one right, one up, one left, two
down, and the noodle passes over itself.

Every cell records whether the run through it was horizontal or vertical. The run
along that recorded axis is the one underneath, so it gets cut open with a little air
on each side, while the run going across it stays whole. The gap is real geometry and
survives into the plot instead of being a trick of the screen.

## Graphics

Ends and straight sections can carry your own SVG shapes. Load them in the Graphics
row: **Head** is the end cap, **Tail** the other end if it should differ, **Joiner** a
piece that drops into straight sections. The Joiners slider sets how often that
happens; with the slider up and no file loaded you get the twist from the original
sketch.

Draw the graphic on a square viewBox, vertically, with the noodle edges running down
the left and right sides and the connection along the bottom edge. A joiner connects
on both the top and the bottom. That is the same convention as the original, so its
graphics work here unchanged. Colour, stroke width and fill in the file are dropped;
the pen size from the panel applies instead.

The diagram under the buttons is the one from the original repo and shows the
convention; click it to see it full size.

Six SVGs sit next to `index.html` as a starting point. `roundEnd.svg`, `twist.svg` and
`twistFill.svg` are the plain set, rebuilt from the original sketch. `fingerHead.svg`,
`fingerTail.svg` and `fingerJoiner.svg` are the finger from the diagram in that repo,
drawn as single centre lines after its proportions: a nail inside the cap, a longer
tip for the tail, and a knuckle collar as the joiner. The tail reaches past its box on
purpose and grows into the neighbouring cell.

Keep your own shapes to single lines too. A traced outline gives every stroke two
edges, which a plotter then draws twice.

Where a graphic sits, the outline is cut open and the shape carries the line across.

## How it works

Noodles are self-avoiding walks over a grid: pick a free cell, grow into a random free
neighbour, and when the head gets stuck, keep growing from the tail instead. Each cell
remembers whether the run through it was horizontal or vertical, which is what makes a
crossing decidable at growing time. The random numbers come from a seeded generator,
which is what makes a drawing reproducible.

The grid keeps every turn at 90 degrees, so the outline needs no offset curve maths.
A straight cell is two parallel lines, a corner is two concentric quarter arcs whose
radii are the cell half-width plus or minus half the noodle width, and each end is a
half-circle cap flush with the outer cell edge. That makes one closed path per noodle,
which a graphic then cuts open where it sits.

Open `index.html?test=1` to run the geometry self check; the result lands in the
page title.

## Not built yet

The path edit mode from the original.

## License

MIT, see [LICENSE](LICENSE). The original Processing sketch by Cadin Batrack is
released under the Unlicense.
