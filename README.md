# generative-noodles

Bendy noodle segments grown into a grid, drawn as SVG for pen plotters. Runs in the
browser, no build step and no dependencies.

A web rewrite of [cadin/generative-noodles](https://github.com/cadin/generative-noodles)
by [Cadin Batrack](https://github.com/cadin), which is a Processing sketch. Same idea,
without Processing. All credit for the concept goes there.

![Screenshot](screenshot.png)

## Usage

Open `index.html` in a browser, or use the hosted version.

**`R`** randomize · **`G`** toggle the grid · **`S`** save an SVG · **`H`** toggle the panel

Every drawing comes from a seed. Type a seed back into the panel and the same noodles
return, so a plot you liked is never lost. The saved SVG carries its real paper size in
inches, so a plotter or a print dialog picks up the right dimensions without scaling,
and all settings ride along in a comment at the top of the file.

## How it works

Noodles are self-avoiding walks over a grid: pick a free cell, grow into a random free
neighbour, and when the head gets stuck, keep growing from the tail instead. The random
numbers come from a seeded generator, which is what makes a drawing reproducible.

The grid keeps every turn at 90 degrees, so the outline needs no offset curve maths.
A straight cell is two parallel lines, a corner is two concentric quarter arcs whose
radii are the cell half-width plus or minus half the noodle width, and each end is a
half-circle cap flush with the outer cell edge. One closed path per noodle.

Open `index.html?test=1` to run the geometry self check; the result lands in the
page title.

## Not built yet

Blackout cells, mask images, joiner and twist graphics, config load and save, and the
path edit mode from the original.

## License

MIT, see [LICENSE](LICENSE). The original Processing sketch by Cadin Batrack is
released under the Unlicense.
