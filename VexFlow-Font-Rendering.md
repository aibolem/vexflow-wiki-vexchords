VexFlow comes with a pluggable font system for music glyphs, based on [SMuFL](https://www.smufl.org/).

It currently supports [Bravura](https://github.com/steinbergmedia/bravura) (a [SMuFL](https://www.smufl.org/) font by Steinberg), and [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) (by Simon Tatham.)

## The VexFlow Font Stack

VexFlow resolves glyphs through a **font stack**.

The default font stack is: `[Bravura, Gonville, Custom]`. When VexFlow tries to resolve a glyph code, it searches each font in the stack, and returns the first glyph it finds. If it can't find a glyph, an exception is thrown.

You can change the default font stack by setting [`VF.DEFAULT_FONT_STACK`](https://github.com/0xfe/vexflow/blob/master/src/tables.js#L16) before building your score, or calling [`setFontStack()`](https://github.com/0xfe/vexflow/blob/master/src/element.js#L37) on a specific element.

```javascript
// Change default font to Gonville
VF.DEFAULT_FONT_STACK = [VF.Fonts.Gonville, VF.Fonts.Bravura, VF.Fonts.Custom]
```

### Supported Fonts

Vexflow currently supports the following fonts:

* [Bravura](https://github.com/steinbergmedia/bravura) - A SMuFL font made by Steinberg.
* [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) - A font made for Gnu Lilypond by Simon Tatham.
* Custom - A set of glyphs submitted by Vexflow contributors, e.g., microtonal accidentals, eastern music glyphs, etc.

## Font files

Each VexFlow font consists of a `glyph` file and a `metric` file, in the [`src/fonts`](https://github.com/0xfe/vexflow/tree/master/src/fonts) directory. For example, Bravura has [`src/fonts/bravura_glyphs.js`](https://github.com/0xfe/vexflow/tree/master/src/fonts/bravura_glyphs.js) and [`src/fonts/bravura_metrics.js`](https://github.com/0xfe/vexflow/tree/master/src/fonts/bravura_metrics.js).

The glyph files consist of coded drawing primitives (`moveTo`, `lineTo`, `bezierCurve`, etc.) for each glyph, indexed by glyph code (which is usually a SMuFL code.) The file is machine generated from a font file, and its format is described at the end of this document. Here's an example:

```javascript
    "bracketTop": {
      "x_min": 0,
      "x_max": 469,
      "y_min": 0,
      "y_max": 295,
      "ha": 295,
      "o": "m 0 168 l 0 0 l 180 0 b 674 390 410 43 616 150 b 675 405 675 396 675 400 b 664 425 675 416 671 422 b 628 405 651 425 635 415 b 157 179 613 389 432 199 l 12 179 b 0 168 3 179 0 177 z"
    },
    "bracketBottom": {
      "x_min": 0,
      "x_max": 469,
      "y_min": -295,
      "y_max": 0,
      "ha": 295,
      "o": "m 0 0 l 0 -168 b 12 -179 0 -177 3 -179 l 157 -179 b 628 -405 432 -199 613 -389 b 664 -425 635 -415 651 -425 b 675 -405 671 -422 675 -416 b 674 -390 675 -400 675 -396 b 180 0 616 -150 410 -43 z"
    },
```

The metric files consist of Vexflow-specific metrics for the font, such as stem lengths, positioning and scaling information, point-size overrides, etc. Metric files are more free form, since they're used differently by different elements, however there are some conventions. Here's an example:

```javascript
glyphs: {
    coda: {
      point: 20,
      shiftX: -7,
      shiftY: 8,
    },
    segno: {
      shiftX: -7,
    },
    flag: {
      shiftX: -0.75,
      tabStem: {
        shiftX: -1.75,
      },
      staveTempo: {
        shiftX: -1,
      }
    },
    clef: {
      gClef: {
        default: { scale: 1.1, shiftY: 1 },
        small: { shiftY: 1.5 }
      },
      fClef: {
        default: { shiftY: -0.5 }
      }
    },

   // ...
   // ...
}
```

## Glyph Rendering

Rendering a glyph consistently across different fonts, canvases, and backends involves a number of moving parts. At a high, level, here's what happens for the following call:

```javascript
Glyph.renderGlyph(ctx, x, y, 40, 'noteheadBlack', { fontStack: [...], category: 'stem' })
```

#### 1) Glyph Resolution

The glyph code (`noteheadBlack`) is resolved by searching the font stack and returning the first available glyph (along with its font, metrics, etc.) This glyph consists of a raw (unprocessed) outline made up of lines and curves.

#### 2) Load Font Metrics and Apply Transformations

Before the final outline can be calculated, some basic transformations may need to be applied.

If a `category` option is provided to `renderGlyph` (e.g., `stem`), the following variables are loaded from the `glyphs.stem` section of the font metrics file (`bravura_metrics.js`):  `scale`, `shiftX`, `shiftY`, and `point` from the `glyphs.stem`.

If no `category` is provided, then defaults are used (typically 0-positioned, and 1-scaled.)

#### 3) Bounding Box and Rendering Metrics

The bounding box for the glyph is then calculated, from which the width and height are derived. An origin shift may also be calculated if requested.

#### 4) Apply Styles on Rendering Backend

Depending on the rendering backend (e.g., SVG, Canvas, PDF), styles such as color, stroke-widths, etc. may be applied to the canvas.

#### 5) Draw!

The glyph is ready to be drawn -- depending on the outline and the transformations, a series of `moveTo`, `lineTo`, `bezierCurveTo`, or `quadraticCurveTo` calls may be sent to the backend. Once we're here the glyph is rendered, and canvas styles are restored (if necessary) for whatever comes next.

If you're interested in the gory details, the entire glyph rendering code is available in `src/glyph.js`.

## Font Metrics Files

The metrics file (e.g., [`src/font/bravura_metrics.js`](https://github.com/0xfe/vexflow/blob/master/src/fonts/bravura_metrics.js) consists of a single exported JavaScript configuration object. It has no pre-defined structure, but it does have some conventions. Here's a snippet from the `bravura_metrics.js` file.

```javascript
 clef: {
    default: {
      point: 32,
      width: 26,
    },
    small: {
      point: 26,
      width: 20,
    },

    // ...
  }
```

### Looking up a metric

You can lookup a metric from within any element with `this.lookupMetric(metricPath, optionalDefault)`. So to get the point-size for the small clef (see above), you can call:

```javascript
const clefPointSize = this.lookupMetric('clef.small.point', 40);
renderClef('treble', clefPointSize);
```

Above, if metric is not found, the default (`40` in this case) is returned. If no default is provided, an exception is thrown.

### Common sections

There can be some standardized metric sections used by common classes, e.g., `glyphs` used by the `category` option of the `Glyph` class.

```javascript
  glyphs: {

    // ...

    textNote: {
      point: 34,
      breathMarkTick: {
        point: 36,
        shiftY: 9,
      },
      breathMarkComma: {
        point: 36,
      },
      segno: {
        point: 30,
        shiftX: -7,
        shiftY: 8,
      },
      coda: {
        point: 20,
        shiftX: -7,
        shiftY: 8,
      }
    },

    // ...

  }
```

If a `category` option is provided to `Glyph` class, e.g., `{category: 'textNote'}`, the renderer will lookup metrics such as `textNote.{code}.point` or `textNote.{code}.shiftX` to apply size and shift overrides on a glyph. If it can't find a metric in `textNote.{code}.point`, it check's `textNote.point` next.

This way you can provide default options for a category, and customize them for specific SMuFL codes.

### Glyphs File Format

The Glyphs file (e.g. [`bravura_glyphs.js`](https://github.com/0xfe/vexflow/blob/master/src/fonts/bravura_glyphs.js), consists of glyph drawing outlines indexed by glyph code. These files are typically machine generated from OTF font files, however you can add custom glyphs by adding a new drawing outline to [`src/font/custom_glyphs.js`](https://github.com/0xfe/vexflow/blob/master/src/fonts/custom_glyphs.js).

The glyph structure consists of the following fields:

* `x_min`: left-most x value 
* `x_max`: right-most x value
* `ha`: height of glyph
* `o`: a long string consisting of repeated *drawing commands* followed by coordinates. (Below.)

The full width of the glyph must be `x_max - x_min`.

#### Drawing commands in `o` are:

* `m` - MoveTo(x,y)
* `l` - LineTo(x,y)
* `q` - QuadraticCurveTo(cpx, cpy, x, y)
* `b` - BeizerCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)

The cp* parameters are coordinates to control points for the curves. All coordinates are scaled by `point_size * 72 / (Vex.Flow.Font.resolution * 100)`.

To see the rendering code, see `Vex.Flow.Glyph.renderOutline()` in `src/glyph.js`. You can see how we generated the outlines for Bravura by examining [`tools/smufl/bravura_fontgen.js`](https://github.com/0xfe/vexflow/blob/master/tools/smufl/bravura_fontgen.js).

## Managing Glyphs

We have a bunch of tooling for glyph management in the [`tools/smufl`] directory (https://github.com/0xfe/vexflow/blob/master/tools/smufl). The tools depend on the configuration files in `config/` to pick SMuFL codepoints and associate them with UTF codes or legacy Vexflow font codes (e.g., `vf1`, `vb6`, etc.)

#### Configuration files

* [`tools/smufl/config/glyphnames.json`](https://github.com/0xfe/vexflow/blob/master/tools/smufl/config/glyphnames.json) - Mappings from SMuFL code-points to UTF code points. These are used to create the `src/font/font_glyphs.js` files for Vexflow.
* [`tools/smufl/config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/smufl/config/valid_codes.js) - List of SMuFL codes used by VexFlow, along with a mapping into legacy vexflow codes.

#### Tools

* `bravura_fontgen.js` - Tool to generate `src/fonts/bravura_glyphs.js` from OTF font files based on the above configuration. This tool can be used for any SMuFL-compliant OTF music font file.
* `gonville_fontgen.js` - Tool to generate `src/fonts/gonville_glyphs.js` and `src.fonts/custom_glyphs.js` from files in the `fonts/` directory.

#### Adding a new Bravura Glyph

1) Add the SMuFL glyph code to [`config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/smufl/config/valid_codes.js). You can find SMuFL glyph codes from the glyph browser at https://smufl.org. If there is no standard code for your glyph, see next section on creating custom glyphs.
2) If there's a Gonville glyph available, then set the value of the code in `valid_codes.js` to the Gonville glyph code. If not, simply set it to `null`.
3) Run `bravura_fontgen.js` to generate a new font file in `src/fonts/bravura_glyphs.js`.

```sh
$ node bravura_fontgen.js fonts/Bravura.otf ../../src/fonts/bravura_glyphs.js
```

4) Run `gonville_fontgen.js` to generate a new Gonville font file (if necessary.)
```sh
$ node gonville_fontgen.js ../../src/fonts/
```

5) Edit your element source file (e.g., `src/accidental.js` if this is a new accidental) and add the code.
6) Perform any scaling or repositioning by adding configuration to the relevant metrics file (`src/fonts/bravura_metrics.js`.)

#### Creating a custom glyph

1) Create a unique custom code (prefixed with `vex`), e.g., `vexMyNewAccidentalGlyph` and add it to [`config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/smufl/config/valid_codes.js). You can set the value type to `null`.
2) Add the glyph outline to `tools/smufl/fonts/custom_glyph.js`. See the *Glyph File Format* section below on how to do that.
3) Regenerate 'src/fonts/custom_glyphs.js` as so:

```sh
$ node gonville_fontgen.js ../../src/fonts/
```
5) Edit your element source file (e.g., `src/accidental.js` if this is a new accidental) and add the code.
6) Perform any scaling or repositioning by adding configuration to the relevant metrics file (`src/fonts/bravura_metrics.js`.)

## Testing

The Vexflow tests automatically run all renders using multiple font stacks, so there's not much more to do than to write tests! :-)

<img src="https://i.imgur.com/rfr4pth.png" width=600 />

## Resources

Here are some handy external resources to help you dig through stuff.

* [SMuFL Git Book](https://w3c.github.io/smufl/gitbook/tables/clefs.html) - Good place to browse glyphs and understand metadata.
* [OpenType Glyph Inspector](https://opentype.js.org/glyph-inspector.html) - Upload a font file and investigate glyphs.
* [SMuFL](https://smufl.org) home page -- Learn all about SMuFL
* [Bravura](https://github.com/steinbergmedia/bravura/tree/master/redist) Github Page -- Download Bravura font files
* [OpenType](opentype.js.org) home page -- The tools use the OpenType library to parse OTF fonts and generate Vexflow glyph files.

