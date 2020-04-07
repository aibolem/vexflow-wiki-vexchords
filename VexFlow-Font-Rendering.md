VexFlow comes with a pluggable font system for music glyphs, based on [SMuFL](https://www.smufl.org/).

It currently supports [Bravura](https://github.com/steinbergmedia/bravura) (a [SMuFL](https://www.smufl.org/) font by Steinberg), and [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) (by Simon Tatham.)

## The VexFlow Font Stack

VexFlow resolves glyphs through a **font stack**.

The default font stack is: `[Bravura, Gonville, Custom]`. When VexFlow tries to resolve a glyph code, it searches each font in the stack, and returns the first glyph it finds. If it can't find a glyph, an exception is thrown.

You can change the default font stack by setting `VF.DEFAULT_FONT_STACK` before building your score, or calling `setFontStack()` on a specific element.

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

Each VexFlow font consists of a `glyph` file and a `metric` file, in the `src/fonts` directory. For example, Bravura has `src/fonts/bravura_glyphs.js` and `src/fonts/bravura_metrics.js`.

The glyph files consist of drawing primitives for each glyph, indexed by glyph code (which is usually a SMuFL code.) The file is machine generated from a font file, and its format is described at the end of this document. Here's an example:

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

## Managing Glyphs

We have a bunch of tooling for glyph management in `tools/smufl`.

#### Configuration files

* `tools/smufl/config/glyphnames.json` - Mappings from SMuFL code-points to UTF code points. These are used to create the `src/font/font_glyphs.js` files for Vexflow.
* `tools/smufl/config/valid_codes.js` - List of SMuFL codes used by VexFlow, along with a mapping into legacy vexflow codes.

#### Tools

* `bravura_fontgen.js` - Tool to generate `src/fonts/bravura_glyphs.js` from OTF font files based on the above configuration. This tool can be used for any SMuFL-compliant OTF music font file.
* `gonville_fontgen.js` - Tool to generate `src/fonts/gonville_glyphs.js` and `src.fonts/custom_glyphs.js` from files in the `fonts/` directory.

#### Adding a new Bravura Glyph

1) Add the SMuFL glyph code to `config/valid_codes.js`. You can find SMuFL glyph codes from the glyph browser at https://smufl.org. If there is no standard code for your glyph, see next section on creating custom glyphs.
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

1) Create a unique custom code (prefixed with `vex`), e.g., `vexMyNewAccidentalGlyph` and add it to `config/valid_codes.js`. You can set the value type to `null`.
2) Add the glyph outline to `tools/smufl/fonts/custom_glyph.js`. See the *Glyph File Format* section below on how to do that.
3) Regenerate 'src/fonts/custom_glyphs.js` as so:

```sh
$ node gonville_fontgen.js ../../src/fonts/
```
5) Edit your element source file (e.g., `src/accidental.js` if this is a new accidental) and add the code.
6) Perform any scaling or repositioning by adding configuration to the relevant metrics file (`src/fonts/bravura_metrics.js`.)

## Font Rendering

The glyph rendering code is in `src/glyph.js`. TODO: expand.

## Metrics File Format

### Glyph File Format

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