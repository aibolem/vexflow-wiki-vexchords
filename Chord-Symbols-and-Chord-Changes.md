In VexFlow, the chord change module can create chord change symbols, like you'd see in a jazz or pop fake book.

![](https://imgur.com/oCHK9dM.png)

To do this, it formats musical symbols (glyphs) from the rendering engine alongside ordinary text. To do that, it needs to know detailed information about the text font you're using. So chord changes will work best if you use one of the fonts that VexFlow knows about. Instructions for doing this, and adding additional text fonts, can be found [later in this guide](#add-a-new-text-font).

# Chord Symbols with Default Fonts

First we'll create a couple of chord symbols using the default browser-safe fonts. Note: this assumes you have read the VexFlow tutorial [section on modifiers](https://github.com/0xfe/vexflow/wiki/Tutorial#step-3-all-about-modifiers)

To create a chord symbol and add it to a note:

```javascript
const chord1 = new ChordSymbol()
    .setFontSize(14)
    .addText("B")
    .addGlyph("b")
    .addText("7", { symbolModifier: SymbolModifiers.SUPERSCRIPT })
    .addGlyph("(", { symbolModifier: SymbolModifiers.SUPERSCRIPT })
    .addGlyph("b", { symbolModifier: SymbolModifiers.SUPERSCRIPT })
    .addText("5", { symbolModifier: SymbolModifiers.SUPERSCRIPT })
    .addGlyph(")", { symbolModifier: SymbolModifiers.SUPERSCRIPT });
```

In the example above, we told VexFlow to create a chord with: the letter 'B' for the key, the glyph corresponding with the flat symbol, and the chord extension `7(♭5)` in superscript. [ See an example. ](https://jsfiddle.net/4gczbt1L/)

![](https://imgur.com/nIzD2lW.png)

The example below shows how you can let VexFlow automatically select between glyphs and text:

```javascript
const chord2 = new ChordSymbol().setFontSize(10).addGlyphOrText("Bb").addGlyphOrText("7(b5)", { symbolModifier: SymbolModifiers.SUPERSCRIPT });
staveNote.addModifier(chord2);
```

VexFlow automatically uses the flat symbol for 'b', the parentheses symbols ( and ), and text for the numbers and note names.
`ChordSymbol` supports [15 symbols at present](https://github.com/0xfe/vexflow/blob/46af63bb5eb52c66d3a30d978b3a08d04eecf5c6/src/chordsymbol.ts#L159-L220):

`+ - ( ) b # /`

result in the expected symbols, and other symbols can be specified explicitly with `addGlyph()`:

`'diminished', 'halfDiminished', 'leftParenTall', 'rightParenTall', 'majorSeventh', 'leftBracket', 'rightBracket'`

You can see the [ChordSymbol unit tests](https://github.com/0xfe/vexflow/blob/master/tests/chordsymbol_tests.ts) for more details.

# Web Fonts

What we've done so far looks kind of 'meh. The smaller image is a bit blurry, and the spacing between the notes isn't correct - this will cause problems for more complex formatting. Using a supported font will fix this.

The `ChordSymbol` module supports two external text fonts. The default font used depends on the music engraving font. If you use the music font _**Petaluma**_, the default text font is '_**PetalumaScript**_' (both provided by Steinburg Media). _**Bravura**_ and _**Gonville**_ music fonts default to _**RobotoSlab**_, one of the Roboto family of web fonts provided by Google Fonts [ [read more](https://fonts.google.com/specimen/Roboto+Slab)]. The music fonts are provided under the SIL Open Font License [ [read more](https://www.smufl.org/fonts/)]. Roboto Slab is licensed under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0).

To use the fonts, the simplest way is to call:

```
await Vex.Flow.Font.loadWebFonts();
```

Depending on the music engraving font, VexFlow either use 'Roboto Slab' or 'PetalumaScript', and fall back to 'Times' or 'Arial' respectively. You can also set the font explicitly for each chord:

```javascript
const chord = new ChordSymbol().setFont("Roboto Slab", 15).addGlyphOrText("Bb7");
```

Take a look at [this example](https://jsfiddle.net/w15pgfab/):

![](https://imgur.com/ROaXd84.png)

That looks better. Now that we have fonts with some good formatting, we can do some more practical applications.

## Stacking

The last few examples show a superscript. As you'd expect, `SymbolModifiers.SUBSCRIPT` gives you subscript. If you do superscript immediately followed by a subscript, the logic will align them vertically and stack them. [See this example.](https://jsfiddle.net/r9Ljckhn/)

![](https://imgur.com/07rgGF8.png)


## Parentheses

You can put `leftParenTall` and `rightParenTall` on either side of the superscript/subscript to get parenthesis on the full vertical extent of the chord.

![](https://imgur.com/HufgfOX.png)

```javascript
const chord3 = new ChordSymbol()
    .addGlyphOrText("D")
    .addGlyph("leftParenTall")
    .addGlyphOrText("6", { symbolModifier: SymbolModifiers.SUPERSCRIPT })
    .addGlyphOrText("9", { symbolModifier: SymbolModifiers.SUBSCRIPT })
    .addGlyph("rightParenTall")
    .setFontSize(14);
```

## ChordSymbol Sandbox

Try out these techniques in the [ChordSymbol Sandbox](https://jsfiddle.net/ydfhco2e/).


## Slash Chords (e.g., C over F)

If you have a `csymDiagonalArrangementSlash` symbol in your chord, VexFlow will condense your chord by moving the left part up and to the right, and the right part down and to the left. This allows you to render slash chords, like C/G or C/E or D/F♯:

```javascript
const slashChord = new ChordSymbol().addGlyphOrText("C").addGlyph("majorSeventh", { symbolModifier: SymbolModifiers.SUPERSCRIPT }).addGlyphOrText("/F");
```

![](https://imgur.com/O4XWrsi.png)

## Positioning

Chords can be positioned: left/right/center of the note (horizontally) or above and below the note (vertically). Below may work nicely for notation such as figured bass. [See this example](https://jsfiddle.net/k27L3egs/):

![](https://imgur.com/lpsfnWT.png)

```javascript
chords.push(new ChordSymbol().setVertical("bottom").addText("I").addTextSuperscript("6").addTextSubscript("4"));
// ...
chords.push(new ChordSymbol().addLine(12).setVertical("bottom"));
```

You can also double stack on the top or the bottom. See the unit test cases for an example.

# What if I want my own fonts?

Just like with the browser default fonts, you can use any font you want. But you might have issues with the formatting, because VexFlow will still be using the metrics for the default fonts. Most English fonts will have a similar vertical baseline, but the spacing between the letters might vary, especially for longer strings or more florid typefaces.

Here's an example of using a font called **Concert One**. The formatting is a bit uneven, but for this example, at least, it works.

![](https://imgur.com/3ylgv7v.png)

Load the web font with CSS:

```css
@import url("https://fonts.googleapis.com/css2?family=Concert+One&display=swap");
```

Create a chord symbol object and set the font:

```javascript
const chord = new ChordSymbol().addGlyphOrText("Ab").addGlyph("dim", { symbolModifier: SymbolModifiers.SUPERSCRIPT }).setFont("Concert One", 14, "normal");
```

# Add a new Text Font

The same [VexFlow tools](https://github.com/0xfe/vexflow/tree/master/tools/fonts) that extract glyphs from the music fonts can be used to extract the metrics from any OpenType text font:

1. Download the font you like, and use a utility such as [Font Squirrel](https://www.fontsquirrel.com/) to create a .otf (OpenType font) file.
2. Place the file in the project directory `vexflow/tools/fonts/`, and run the `fontgen_text.js` script. This will produce a .ts file with the formatting you want. For example:

```
node fontgen_text.js MyFont.otf myfont_glyphs.ts
```

3. Move the `myfont_glyphs.ts` file to `src/fonts/`, next to the other font glyphs files (petalumascript_glyphs.ts and robotoslab_glyphs.ts).
4. Update `src/fonts/textfonts.ts`to load the new font.
5. Optionally update elements to use the new text font by default. For example, `chordsymbol.ts` has a `TEXT_FONT` property that returns its default text font.

Note: `advanceWidth` and `leftSideBearing` are the only metrics used currently.
