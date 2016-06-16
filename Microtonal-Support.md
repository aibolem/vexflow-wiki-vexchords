Vexflow supports some microtonal accidentals. The limitation comes mainly from the usage of the Gonville music font that does not contain glyphs for many such accidentals. Of course, assembling a full set of accidentals used across musical cultures and traditions is a major undertaking in an of itself, and music engraving systems all vary in their support.

The microtonal accidentals that VexFlow supports are:

* one quarter sharp / one comma sharp: glyph code v4f/v78, VexFlow mnemonic "+"
* one quarter flat / 4 commas flat: glyph code vb7, VexFlow mnemonic "bs"
* 3 quarters sharp: glyph code v51/v13, VexFlow mnemonic "++"
* 1 comma flat: glyph code v57/vab, VexFlow mnemonic "d"
* 5 commas sharp: glyph code v8d, VexFlow mnemonic "+-"
* 8 commas sharp: glyph code v7a, VexFlow mnemonic "++-"
* 8 commas flat: glyph code v39, VexFlow mnemonic "bss"

This set ALMOST covers the Arabic / Turkish set of accidentals, with the exception of the **3 quarters flat**, which is not present in the Gonville font. Also, Persian accidentals (Koron and Sori) are not represented.

An example output from VexFlow is shown here. This is actually a screenshot from the [VF test module "Accidental"](https://github.com/0xfe/vexflow/blob/master/tests/accidental_tests.js#L279).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow-microtones.png]]
