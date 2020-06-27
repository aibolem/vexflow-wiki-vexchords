## Introduction
In VexFlow, the chord change module can create chord change symbols, like you'd see in a jazz or pop fake book.  

![](https://imgur.com/oCHK9dM.png)

To do this, it formats musical symbols (glyphs) from the rendering engine along-side ordinary text.  In order to do _that_, it needs to know some detailed information about the text font you're using.  So chord changes will work best if you use one of the fonts that VexFlow knows about.  Instructions for doing this, and adding additional text fonts, can be found later in this section.

## Fallback fonts
First we'll create a couple of chord symbols using the ugly, browser-safe fonts.  Note: this assumes you have read the VexFlow tutorial section on [modifiers](https://github.com/0xfe/vexflow/wiki/The-VexFlow-Tutorial#step-3-all-about-modifiers)

To create a chord symbol and add it to a note:

```javascript
 var chord1 = new VF.ChordSymbol().setFontSize(14).
  .addText('B')
  .addGlyph('accidentalFlat')
  .addText('7',{ symbolModifier:VF.ChordSymbol.symbolModifiers.SUPERSCRIPT })
  .addGlyph('accidentalFlat',{ symbolModifier:VF.ChordSymbol.symbolModifiers.SUPERSCRIPT });
  .addText('5',{ symbolModifier:VF.ChordSymbol.symbolModifiers.SUPERSCRIPT });
  // ...
  notes[0].addModifier(0,chord1);
```
What we just did was tell Vex to create a chord with three symbols: the letter 'B' for the key, the glyph corresponding with the accidental flat, and the chord extension '7b5' in superscript. [[run](https://jsfiddle.net/AaronDavidNewman/bpg6ow3n/)]


![](https://imgur.com/nIzD2lW.png)

The second chord in this example shows how you can save some typing, and let the logic choose symbols and text.  So the equivalent code would be:

```javascript
 var chord2 = new VF.ChordSymbol()
  .addGlyphOrText('Bb')
  .addGlyphOrText('7b5',{ symbolModifier:VF.ChordSymbol.symbolModifiers.SUPERSCRIPT });
  // ...
  notes[1].addModifier(0,chord2);
```

The logic automatically uses the flat symbol for 'b' and text for everything else. 
The Chord Symbols module supports 15 symbols at present: 

`+-()b#/`

result in the expected symbols, and other symbols can be specified explicitly with `addGlyph`:

`'diminished', 'halfDiminished', 'leftParenTall', 'rightParenTall', 'majorSeventh', 'leftBracket', 'rightBracket'`

You can see the unit tests for a full menagerie of Chord Symbol features.

## WebFonts
What we've done so far looks kind of 'meh.  The smaller image is a bit blurry, and the spacing between the notes isn't correct - this will cause problems for more complex formatting.  Using a supported font will fix this.

 The Chord Symbol module supports 2 external text fonts at the time of this writing.  The default font used depends on the engraving (music) font:  If you use the music font _**Petaluma**_, the default text font is '_**PetalumaScript**_' (both provided by Steinburg Media).  _**Bravura**_  and _**Gonville**_ music fonts default to _**RobotoSlab**_, one of the Roboto family of web fonts provided by Google Fonts [ [read more](https://fonts.google.com/specimen/Roboto+Slab)].  Both are provided under the SIL Open Font License [ [read more](https://www.smufl.org/fonts/)].

To use the fonts in your application, the simplest way is to just include the css to download the font.

``` css
@font-face {
  font-family: 'petalumaScript';
  src: url('https://aarondavidnewman.github.io/Smoosic/build/styles/fonts/petalumascript-webfont.woff2') format('woff2'),
    url('https://aarondavidnewman.github.io/Smoosic/build/styles/fonts/petalumascript-webfont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}

@font-face {
    font-family: 'robotoSlab';
    src: url('https://aarondavidnewman.github.io/Smoosic/build/styles/fonts/robotoslab-webfont.woff2') format('woff2'),
         url('https://aarondavidnewman.github.io/Smoosic/build/styles/fonts/robotoslab-webfont.woff') format('woff');
    font-weight: 500;
    font-style: normal;
}

```
VexFlow will try to use 'robotoSlab' or 'petalumaScript' font, and fall back to 'Times' or 'Arial' respectively.  You can also set the font explicitly for each chord, with this or any font you choose (see below on non-standard fonts):
``` javascript
var chord = new VF.ChordSymbol().setFont('robotoSlab',15,'normal').addGlyphOrText('Bb7');
```

Now we'll try again [ [run](https://jsfiddle.net/AaronDavidNewman/0em1k5jy/)]:

![](https://imgur.com/ROaXd84.png)

That looks better.  Now that we have fonts with some good formatting, we can do some more practical applications.

## Stacking
The last few examples show a superscript.  As you'd expect, `VF.ChordSymbol.symbolModifiers.SUBSCRIPT` gives you subscript.  If you do superscript immediately followed by a subscript, the logic will align them vertically and stack them.

[[run](https://jsfiddle.net/AaronDavidNewman/dtsgq087/)]:

![](https://imgur.com/07rgGF8.png)

## Some more tricks

You can sandbox these [[here](https://jsfiddle.net/AaronDavidNewman/4ucmjveL/)].

### Parenthesis:

You can put `leftParenTall` and `rightParenTall` on either side of the super/subscripts to get parenthesis on the full vertical extent of the chord.

![](https://imgur.com/HufgfOX.png)


``` javascript
var chord3 = new VF.ChordSymbol()
    .addGlyphOrText('D')
    .addGlyph('leftParenTall')
    .addGlyphOrText('6', { symbolModifier: VF.ChordSymbol.symbolModifiers.SUPERSCRIPT} )
    .addGlyphOrText('9', { symbolModifier: VF.ChordSymbol.symbolModifiers.SUBSCRIPT})
    .addGlyph('rightParenTall')
    .setFontSize(14);
```

### Thing over Other Thing
If you have an `csymDiagonalArrangementSlash` symbol in your chord, the logic will try to condense your chord - moving the left side up and to the right, and the right side down and to the left (commonly spoken as 'C over F'):

![](https://imgur.com/O4XWrsi.png)

``` javascript
var chord2 = new VF.ChordSymbol()
    .addGlyphOrText('C')
    .addGlyph('majorSeventh', { symbolModifier: VF.ChordSymbol.symbolModifiers.SUPERSCRIPT})
    .addGlyphOrText('/F');
```

### Chord symbol position
Chords can be positioned: left/right/center of the note (horizontally) or above and below the note (vertically).  Below may work nicely for music theory or figured base (My music theory years are far behind me so I'm not quite sure if these are right) [ [run](https://jsfiddle.net/AaronDavidNewman/zmdgtku1/)]:

![](https://imgur.com/lpsfnWT.png)

``` javascript

chords.push(new VF.ChordSymbol()
  .setVertical('bottom')
  .addText('I')
  .addTextSuperscript('6')
  .addTextSubscript('4'));
// ...
chords.push(new VF.ChordSymbol()
  .addLine(12)
  .setVertical('bottom'));

```

You can also double stack on the top or the bottom.  See the unit test cases for an example.

## But what if I want my own fonts?
Well, sure, just like the browser fallback fonts, you can use any fonts you want.  But you might have issues with the formatting, because VexFlow will still be using the metrics for the default fonts.  Most English fonts will have a pretty consistent vertical baseline, but the spacing between the letters might vary, especially for longer strings or more florid typefaces.

Here's an example of using a font from Google called 'Concert One'.  The formatting is a bit uneven, but for this example, at least, it works.

![](https://imgur.com/3ylgv7v.png)

``` css
@import url('https://fonts.googleapis.com/css2?family=Concert+One&display=swap');
```

``` javascript
  var chord4 = new VF.ChordSymbol()
    .addGlyphOrText('Ab').addGlyph('dim',
    { symbolModifier: VF.ChordSymbol.symbolModifiers.SUPERSCRIPT })    
    .setFont('Concert One',14,'normal');
```
### Disable text formatting
If the font you are using is far enough away from the defaults that the text overlaps, you can disable the text formatting.  This basically assumes you have a mono-spaced font, so the gaps between the letters may look strange but the font will be more readable.

Before disable formatting:

![](https://imgur.com/TbiFBge.png)

After disable formatting:

![](https://imgur.com/yZ4kcrD.png)

To disable formatting, set the following global before creating your chord symbol objects:

``` javascript 
// before doing anything:
VF.ChordSymbol.NOTEXTFORMAT = true;
// ...
```

Note the exaggerated gaps between the text and the symbols.

### Adding a new text font to VexFlow
The same utilities in VexFlow that extract glyphs from the music fonts can be used to extract the metrics from any Open-Type text font, using the following instructions:
1. Download the font you like, and use any online utility such as [[font squirrel](https://www.fontsquirrel.com/)] to create a .otf (open type font) file.
2. Place the file in the project directory /tools/smufl, and run the font_fontgen.js node utility.  This will produce a .json file with the formatting you want.
3.  Create myfont_metrics.js file in src/fonts, with the other font metrics files, using the metrics and other information in the JSON file.
4.  Update chordSymbols.js to use the new font.

Note: advanceWidth and leftSideBearing are the only metrics used currently.





