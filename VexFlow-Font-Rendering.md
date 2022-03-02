[VexFlow](https://vexflow.com) comes with a pluggable font system for music glyphs, based on [Standard Music Font Layout](https://www.smufl.org/) (SMuFL), developed by the [W3C Music Notation Community Group](https://www.w3.org/community/music-notation/).

By default, it supports the following fonts:

-   [Bravura](https://github.com/steinbergmedia/bravura) (a SMuFL font by Steinberg)
-   [Petaluma](https://github.com/steinbergmedia/petaluma) (a SMuFL font by Steinberg)
-   [Gonville](https://www.chiark.greenend.org.uk/~sgtatham/gonville/) (by Simon Tatham)
-   Custom - Glyphs submitted by Vexflow contributors (microtonal accidentals, eastern music glyphs, etc).

## Bravura

<img src="https://imgur.com/oS5L9eX.png" alt="Bravura" width=700/>

## Petaluma

<img src="https://imgur.com/uP2IXnf.png" alt="Petaluma" width=700/>

## Gonville

<img src="https://imgur.com/aCfdJij.png" alt="Gonville" width=700/>
<br><br>

# Font Stack

VexFlow resolves glyphs through a **font stack**.

The default font stack is: `[Bravura, Gonville, Custom]`. When VexFlow tries to resolve a glyph code, it searches each font in the stack, and returns the first glyph it finds. If it can't find a glyph, an exception is thrown.

Change the font stack by calling [`Flow.setMusicFont(...fontNames)`](https://github.com/0xfe/vexflow/blob/37d7285b56c0f18e4fb45b878d6d5b49d1521495/src/flow.ts#L215-L222):

```javascript
Vex.Flow.setMusicFont("Petaluma", "Bravura", "Gonville");
```

# Font Files

Each VexFlow music font consists of a **glyphs file**, a **metrics file** and a **loader file**, in the [`src/fonts`](https://github.com/0xfe/vexflow/tree/master/src/fonts) directory.

For example, Bravura has:

-   [`src/fonts/bravura_glyphs.ts`](https://github.com/0xfe/vexflow/tree/master/src/fonts/bravura_glyphs.ts)
-   [`src/fonts/bravura_metrics.ts`](https://github.com/0xfe/vexflow/tree/master/src/fonts/bravura_metrics.ts)
-   [`src/fonts/load_bravura.ts`](https://github.com/0xfe/vexflow/tree/master/src/fonts/load_bravura.ts).

**Glyphs files** include drawing primitives (`moveTo`, `lineTo`, `bezierCurve`, etc.) for each glyph, indexed by glyph code (a SMuFL code.) This file is generated from a OTF font file by a [script](#Tools). Here's an example:

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

The **metrics files** consist of Vexflow-specific metrics for the font, such as stem lengths, positioning and scaling information, point-size overrides, etc. Metrics files are more free form, since they're used differently by different elements, however there are some conventions. Here's an example:

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

The **container files** consist of a standard container importing the **glyphs file** and the **metrics file** which allows the generation of a separated file using the **dynamic import** feature of [Code Splitting|webpack](https://webpack.js.org/guides/code-splitting/). Here's an example:

```javascript
import { BravuraFont } from "./bravura_glyphs";
import { BravuraMetrics } from "./bravura_metrics";

const Bravura = {
    fontData: BravuraFont,
    metrics: BravuraMetrics,
};

export default Bravura;
```

# Glyph Rendering

Rendering a glyph consistently across different fonts, canvases, and backends involves a number of moving parts. Let's walk through what happens when the following line of code is run:

```javascript
Glyph.renderGlyph(ctx, x, y, fontSize, glyphCode, { category: "flag.tabStem" });
```

## 1) Glyph Resolution

The glyph code (e.g., `noteheadBlack`, `coda`) is resolved by searching the music font stack and returning the first available glyph (along with its font, metrics, etc.) This glyph consists of an unprocessed outline made up of lines and curves.

## 2) Load Font Metrics and Apply Transformations

Before the final outline can be calculated, some transformations may need to be applied.

If a `category` option is provided to `renderGlyph(...)` (e.g., `{ category: 'flag.tabStem' }` above), the following variables are loaded from the `glyphs.flag.tabStem` section of the font metrics file [`bravura_metrics.js`](https://github.com/0xfe/vexflow/blob/master/src/fonts/bravura_metrics.ts#L220-L222):

-   `scale`
-   `shiftX`
-   `shiftY`
-   `point`

If no `category` is provided, then defaults are used (typically 0-positioned, and 1-scaled.)

## 3) Bounding Box and Rendering Metrics

The bounding box for the glyph is then calculated, from which the width and height are derived. An origin shift may also be calculated if requested.

## 4) Apply Styles on Rendering Backend

Depending on the rendering backend (e.g., SVG, Canvas), styles such as color, stroke-widths, may be applied.

## 5) Draw

The glyph is ready to be drawn. Depending on the outline and the transformations, a series of `moveTo`, `lineTo`, `bezierCurveTo`, or `quadraticCurveTo` calls are sent to the backend. The glyph is rendered, and canvas styles are restored (if necessary) for whatever comes next.

If you're interested in the details, the entire glyph rendering code is available in [`src/glyph.ts`](https://github.com/0xfe/vexflow/blob/master/src/glyph.ts).

# Font Metrics Files

The **metrics files** (e.g., [`src/font/bravura_metrics.ts`](https://github.com/0xfe/vexflow/blob/master/src/fonts/bravura_metrics.ts) consist of a single exported configuration object. It has no pre-defined structure, but it does have some conventions. Here's a snippet from the `bravura_metrics.ts` file.

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

## Looking up a metric

You can lookup a metric from within any element with:

```
Tables.currentMusicFont().lookupMetric(metricPath, optionalDefault);
```

So to get the point-size for the small clef in the `bravura_metrics.ts` excerpt above, you can call:

```javascript
const clefPointSize = Tables.currentMusicFont().lookupMetric("clef.small.point", 40);
renderClef("treble", clefPointSize);
```

If metric is not found, the default (`40` in this case) is returned. If no default is provided, an exception is thrown.

## Common sections

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

If a `category` option is provided to `Glyph.renderGlyph(ctx, x, y, code, point, options)`, e.g., `{category: 'textNote'}`, the renderer will lookup metrics such as `textNote.{code}.scale` or `textNote.{code}.shiftX` to apply size and shift overrides on a glyph. If it can't find a metric for the specific code in `textNote.{code}.scale`, it checks the parent for a category default (`textNote.scale`).

This way you can provide default options for a category and customize them for specific SMuFL codes.

### Glyphs File Format

The Glyphs file (e.g. [`bravura_glyphs.ts`](https://github.com/0xfe/vexflow/blob/master/src/fonts/bravura_glyphs.ts) consists of glyph drawing outlines indexed by glyph code. These files are typically machine generated from OTF font files, however you can add custom glyphs by adding a new drawing outline to [`src/font/custom_glyphs.ts`](https://github.com/0xfe/vexflow/blob/master/src/fonts/custom_glyphs.ts).

The glyph structure consists of the following fields:

-   `x_min`: left-most x value
-   `x_max`: right-most x value
-   `ha`: height of glyph
-   `o`: a long string consisting of repeated _drawing commands_ followed by coordinates. (Below.)

The full width of the glyph must be `x_max - x_min`.

### Drawing commands in `o` are:

-   `m` - MoveTo(x,y)
-   `l` - LineTo(x,y)
-   `q` - QuadraticCurveTo(cpx, cpy, x, y)
-   `b` - BeizerCurveTo(cp1x, cp1y, cp2x, cp2y, x, y)

The cp* parameters are coordinates to control points for the curves. All coordinates are scaled by `point_size * 72 / (Vex.Flow.Font.resolution \* 100)`.

To see the rendering code, see `Vex.Flow.Glyph.renderOutline()` in `src/glyph.js`. You can see how we generated the outlines for Bravura by examining [`tools/fonts/fontgen_smufl.js`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/fontgen_smufl.js).

## Managing Glyphs

The tools for glyph management are in the [`tools/fonts/`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/) directory. The tools depend on the configuration files in `tools/fonts/config/` to pick SMuFL codepoints and associate them with UTF codes or legacy Vexflow font codes (e.g., `vf1`, `vb6`).

### Configuration files

-   [`tools/fonts/config/glyphnames.json`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/config/glyphnames.json) - Mappings from SMuFL code-points to UTF code points. These are used to create the `src/fonts/xxx_glyphs.ts` files for Vexflow.
-   [`tools/fonts/config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/config/valid_codes.js) - List of SMuFL codes used by VexFlow, along with a mapping into legacy vexflow codes.

### Tools

-   `fontgen_smufl.js` - Tool to generate `src/fonts/fontname_glyphs.js` from OTF font files based on the above configuration. This tool can be used for any SMuFL-compliant OTF music font file.
-   `fontgen_gonville_custom.js` - Tool to generate `src/fonts/gonville_glyphs.ts` and `src/fonts/custom_glyphs.ts` from files in the `tools/fonts/other/` directory.

### Add a New Glyph to an Existing Font

1. Add the SMuFL glyph code to [`config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/config/valid_codes.js). You can find SMuFL glyph codes from the glyph browser at https://smufl.org. If there is no standard code for your glyph, see next section on creating custom glyphs.
2. If there's a Gonville glyph available, then set the value of the code in `valid_codes.js` to the Gonville glyph code. If not, simply set it to `null`.
3. Run `fontgen_smufl.js` to generate the new Bravura and Petaluma glyph files.

```sh
$ node fontgen_smufl.js fonts/Bravura.otf ../../src/fonts/bravura_glyphs.js
$ node fontgen_smufl.js fonts/Petaluma-1.055.otf ../../src/fonts/petaluma_glyphs.js
```

4. Run `fontgen_gonville_custom.js` to generate a new Gonville font file (if necessary.)

```sh
node fontgen_gonville_custom.js ../../src/fonts/
```

5. Edit your element source file (e.g., `src/accidental.ts` if this is a new accidental) and add the code.
6. Adjust scale or position by adding configuration to the relevant metrics file (`src/fonts/bravura_metrics.ts`.)

### Create a custom glyph

1. Create a unique custom code (prefixed with `vex`), e.g., `vexMyNewAccidentalGlyph`, and add it to [`tools/fonts/config/valid_codes.js`](https://github.com/0xfe/vexflow/blob/master/tools/fonts/config/valid_codes.js). You can set the value to `null`.
2. Add the glyph outline to `tools/fonts/other/custom.js`.
3. Regenerate `src/fonts/custom_glyphs.ts` with this command:

```sh
node fontgen_gonville_custom.js ../../src/fonts/
```

5. Add the code to `tables.ts` (e.g., search for `vexAccidentalMicrotonal1`).
6. Adjust scale or position by adding configuration to the relevant metrics file (`src/fonts/bravura_metrics.ts`.)

## Testing

The Vexflow tests automatically run all renders using multiple font stacks, so there's not much more to do than to write tests! :-)

<img src="https://i.imgur.com/rfr4pth.png" width=600 />
<br><br>

# Add a New Font

For this example, the new font is named "Awesome" instead of Bravura / Petaluma / Gonville. If you want to try this with a real SMuFL font, you can try this with [Leland](https://github.com/MuseScoreFonts/Leland) or [Sebastian](https://github.com/fkretlow/sebastian).

In the VexFlow repository, search for `ADD_MUSIC_FONT` to see the integration points for a completely new font.

1. The first integration point is in `load_all.ts`. Follow the existing examples to import your font and call the load function on that font module. For example:

```typescript
import { loadAwesome } from "./load_awesome"; // <<< Added this!
import { loadBravura } from "./load_bravura";
import { loadCustom } from "./load_custom";
import { loadGonville } from "./load_gonville";
import { loadPetaluma } from "./load_petaluma";

export function loadAllMusicFonts(): void {
    loadAwesome(); // <<< Added this!
    loadBravura();
    loadCustom();
    loadGonville();
    loadPetaluma();
}
```

2. In the `src/fonts/` directory, create a new file called `load_awesome.ts`. Your loader file will look something like this:

```typescript
import { Font } from "../font";
import { AwesomeFont } from "./awesome_glyphs";
import { AwesomeMetrics } from "./awesome_metrics";

export function loadAwesome() {
    Font.load("Awesome", AwesomeFont, AwesomeMetrics);
}
```

Now we need to generate the `awesome_glyphs.ts` and `awesome_metrics.ts` files. These files should be placed in the `src/fonts/` directory.

3. Let's take a look at the glyphs file first. Open `bravura_glyphs.ts` to see what it should look like. It's a big file containing all the glyph outlines for each SMuFL code. To generate this file, we use the `fontgen_smufl.js` tool.

# More Info

Here are some handy external resources:

-   [SMuFL](https://www.smufl.org/version/latest/) – Browse the glyphs and understand metadata (e.g., [Clefs](https://www.smufl.org/version/latest/range/clefs/)).
-   [OpenType Glyph Inspector](https://opentype.js.org/glyph-inspector.html) - Upload a font file and investigate glyphs.
-   [Bravura](https://github.com/steinbergmedia/bravura/tree/master/redist) – Download Bravura font files.
-   [OpenType](opentype.js.org) – The tools use the OpenType library to parse OTF fonts and generate Vexflow glyph files.
