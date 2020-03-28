The VexFlow glyphs were generated from the [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) font by Simon Tatham.

The glyph paths are stored in `src/fonts/vexflow_font.js` and accessible via the variable `Vex.Flow.Font.glyphs`. You can see the current set of glyphs by opening `src/glyph.html` in your browser. You can see all glyphs by opening `src/transform.html`.


<img align="center" src="https://i.imgur.com/KO1arxH.png" width=500 />


To add a Gonville glyph to `Vex.Flow.Font.glyphs`, edit `transform.html` and add the Gonville glyph code to `validGlyphCodes`. It generates a Javascript file you can use to update `src/fonts/vexflow_fonts.js`.

## Adding Custom Glyphs

You can add custom glyphs by adding a new path to `src/font/custom_glyphs.js`. Make sure to give it a unique glyph code.

The path structure consists of the following fields:

* `x_min`: left-most x value 
* `x_max`: right-most x value
* `o`: a long string consisting of repeated *commands* followed by coordinates. (Below.)

The full width of the glyph must be `x_max - x_min`.

### Commands in `o` are:

* `m` - MoveTo(x,y)
* `l` - LineTo(x,y)
* `q` - QuadraticCurveTo(cpx, cpy, x, y)
* `b` - BeizerCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)

The cp* parameters are coordinates to control points for the curves. All coordinates are scaled by `point_size * 72 / (Vex.Flow.Font.resolution * 100)`.

To see the rendering code, see `Vex.Flow.Glyph.renderOutline()` in `src/glyph.js`.