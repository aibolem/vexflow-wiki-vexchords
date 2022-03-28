# 4.0.1

4.0.1 is the first major release of VexFlow since version 3.0.9 in April 2020.

This document details the major changes, and includes links to PRs or issues where appropriate.

The list of [breaking changes](#breaking-changes) is at the bottom of this page.

## TypeScript

VexFlow has been converted to TypeScript! The project compiles to ES6.

## ES Modules + Common JS

VexFlow now provides an ESM build, in addition to the traditional CommonJS library that works with `require()`.

## Other Features

-   Improved handling of music fonts and text fonts.
-   Optional lazy loading of music fonts.
-   `setFont(...)` method can be called in these ways:
    -   `setFont(family, size, weight, style)`
    -   `setFont(cssShorthand)`
        -   e.g., `setFont('bold 10pt Arial')`
    -   `setFont(fontInfoObject)`
        -   e.g., `setFont({ family: 'Times', size: 12 })`

## Breaking Changes

### Gruntfile and package.json scripts

Many of the package.json scripts have been moved into Gruntfile.js. See the top of Gruntfile.js for a list of the different commands you can invoke while building & testing VexFlow. If you previously used commands like `npm run xxxx`, you can look for the equivalent command in the Gruntfile.js (in most cases, `npm run xxxx` changed to `grunt xxxx`).

### StaveNote: Removed addAccidental(), addArticulation(), addAnnotation(), addDot()

-   stavenote.ts no longer includes the above helper methods. Instead, call `note.addModifier(modifier, index)` directly.
-   `Note.addModifier(modifier: Modifier, index?: number): this` throws a RuntimeError if the parameters are reversed.
-   To add a dot, use `Dot.buildAndAttach(...)` or the following:

```typescript
const dot = new Dot();
dot.setDotShiftY(note.glyph.dot_shiftY);
note.addModifier(dot, i);
```

### Other Breaking Changes

-   The tsconfig.json `compilerOptions.target` has been updated to ES6 / ES2015. If you are targeting an older environment, you will need to build directly from source code (and change the target back to ES5).
-   `Stave.setNumLines(n: number)` requires a number. Previously, a string would also work. See: [stave.ts](https://github.com/0xfe/vexflow/blob/master/src/stave.ts) and [#1083](https://github.com/0xfe/vexflow/issues/1083).
-   `TickContext.getTickableForVoice(voiceIndex: number): Tickable` was previously named `getTickablesForVoice(voiceIndex: number): Note`. We removed the `s` because the method returns a single Tickable. You will need to update calls to this function if you are upgrading from a build from between April 2020 to August 2021.
-   `Element` and its subclasses have a static `CATEGORY` string property, used by VexFlow internally to differentiate objects. This string has been standardized to be singular, with UpperCamelCase capitalization.
    -   Examples:
        -   `Accidental.CATEGORY` is now `'Accidental'` instead of `'accidentals'`.
        -   `Modifier.CATEGORY` is now `'Modifier'` instead of `'none'`.
-   **ChordSymbol**
    -   `ChordSymbol.NO_TEXT_FORMAT` was previously named `ChordSymbol.NOTEXTFORMAT`.
    -   `ChordSymbol.metrics` was previously named `ChordSymbol.chordSymbolMetrics`.
-   `StaveNote.LEDGER_LINE_OFFSET` was previously named `StaveNote.DEFAULT_LEDGER_LINE_OFFSET`.
-   **Fonts**

    -   `TextFontMetrics` has been merged into `FontGlyph` due to substantial overlap.
    -   `Flow.NOTATION_FONT_SCALE` was previously named `Flow.DEFAULT_NOTATION_FONT_SCALE`.
    -   `setFont(...)` in `CanvasContext` and `SVGContext` previously took arguments: `family`, `size`, `weight`. The `weight` argument allowed strings like `'italic bold'`. This no longer works, and `'italic'` must now be passed into the `style` argument.

-   **Build Process**
    -   Gruntfile environment variable `VEX_DEVTOOL` was previously named `VEX_GENMAP`. This environment variable sets the [webpack devtool configuration option](https://webpack.js.org/configuration/devtool/).
