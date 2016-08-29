VexFlow currently supports microtones in two areas: accidentals and key signatures.

### Microtonal Accidentals
VexFlow supports SOME microtonal accidentals. The limitation comes mainly from the usage of the Gonville music font that does not contain glyphs for many such accidentals. Of course, assembling a full set of accidentals used across musical cultures and traditions is a major undertaking in and of itself, and music engraving systems all vary in their support.

The microtonal accidentals that VexFlow supports are:

* one quarter sharp / one comma sharp: VexFlow mnemonic "+"
* one quarter flat / 4 commas flat: VexFlow mnemonic "bs"
* 3 quarters sharp: VexFlow mnemonic "++"
* 1 comma flat: VexFlow mnemonic "d"
* 5 commas sharp: VexFlow mnemonic "+-"
* 8 commas sharp: VexFlow mnemonic "++-"
* 8 commas flat: VexFlow mnemonic "bss"

This set ALMOST covers the Arabic / Turkish set of accidentals, with the exception of the **3 quarters flat**, which is not present in the Gonville font. Also, Persian accidentals (Koron and Sori) are not represented.

An example output from VexFlow is shown here. This is actually a screenshot from the [VF test module "Accidental"](https://github.com/0xfe/vexflow/blob/master/tests/accidental_tests.js#L261).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow-microtones.png]]

Support for more accidentals will occur when Gonville is replaced with a more standard and comprehensive font, such as those that are [SMuFL](http://www.smufl.org/)-compatible. SMuFL support is [an ongoing topic](https://github.com/0xfe/vexflow/issues/350) for VexFlow. Once this happens, it will be trivial-ish to add new mnemonics to represent those accidentals.

### Microtonal Key Signatures
VexFlow allows to specify key signatures that contain arbitrary accidentals, including microtonal ones, in place of the standard sharp and flat. An example output is shown here. This is a screenshot from the [VF test module "KeySignature"](https://github.com/0xfe/vexflow/blob/master/tests/keysignature_tests.js#L165).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow-keysig-altered.png]]

However, microtonal key signature support is not complete, because other musical traditions do not follow the canonical style of key signature layout. For example, Arabic musical notation includes key signatures such as Bb Eb F#. This is currently a [work in progress](https://github.com/0xfe/vexflow/issues/328). 
