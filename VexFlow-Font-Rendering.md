VexFlow comes with a pluggable font system for music glyphs. It currently supports [Bravura](https://github.com/steinbergmedia/bravura) (a [SMuFL](https://www.smufl.org/) font by Steinberg), and [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) (by Simon Tatham.)

## Changing the Font Stack

You can set your font stack by setting `VF.DEFAULT_FONT_STACK`, or calling `setFontStack()` on an element.

```javascript
# Use Bravura as the main font, and fallback to Gonville or Custom (in that order) if glyphs are not found
VF.DEFAULT_FONT_STACK = [VF.Fonts.Bravura, VF.Fonts.Gonville, VF.Fonts.Custom]
```

## Font files

VexFlow font files are located in `src/fonts/`. Currently we have:

```
# Bravura fonts and metrics
bravura_glyphs.js
bravura_metrics.js

# Custom glyphs (e.g. microtonals) and metrics
custom_glyphs.js
custom_metrics.js

# Gonville fonts and metrics
gonville_glyphs.js
gonville_metrics.js
```

## Adding New Glyph codes

Tools to add, remove, and modify VexFlow glyphs are in `tools/smufl`. See documentation in https://github.com/0xfe/vexflow/tree/master/tools/smufl.

## Font Rendering

The glyph rendering code is in `src/glyph.js`. TODO: expand.

### Adding Custom Glyphs

You can add custom glyphs by adding a new path to `src/font/custom_glyphs.js`. Make sure to give it a unique glyph code. See instructions in https://github.com/0xfe/vexflow/tree/master/tools/smufl for regenerating font files.

The path structure consists of the following fields:

* `x_min`: left-most x value 
* `x_max`: right-most x value
* `o`: a long string consisting of repeated *commands* followed by coordinates. (Below.)

The full width of the glyph must be `x_max - x_min`.

#### Commands in `o` are:

* `m` - MoveTo(x,y)
* `l` - LineTo(x,y)
* `q` - QuadraticCurveTo(cpx, cpy, x, y)
* `b` - BeizerCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)

The cp* parameters are coordinates to control points for the curves. All coordinates are scaled by `point_size * 72 / (Vex.Flow.Font.resolution * 100)`.

To see the rendering code, see `Vex.Flow.Glyph.renderOutline()` in `src/glyph.js`.