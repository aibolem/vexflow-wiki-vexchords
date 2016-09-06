VexFlow currently supports microtones in two areas: accidentals and key signatures.

### Microtonal Accidentals
VexFlow supports SOME microtonal accidentals. The limitation comes mainly from the usage of the Gonville music font that does not contain glyphs for many such accidentals. Of course, assembling a full set of accidentals used across musical cultures and traditions is a major undertaking in and of itself, and music engraving systems all vary in their support.

The microtonal accidentals that VexFlow supports are:

Glyph | Mnemonic | Description | Notation System(s)
----- | -------- | ----------- | ------------------
  | # | sharp | Standard and all others
  | ## | double sharp | Standard and all others
  | b | flat | Standard and all others
  | bb | double flat | Standard and all others
  | n | natural | Standard and all others 
  | + | 1 quarter-tone sharp | Arabic / Stein-Zimmermann
  | + | 1 comma sharp | Turkish
  | ++ | 3 quarter-tones sharp | Arabic / Stein-Zimmermann
  | bs | 1 quarter-tone flat | Arabic
  | d | 1 quarter-tone flat | Stein-Zimmermann
  | d | 1 comma flat | Turkish
  | db | 3 quarter-tones flat | Stein-Zimmermann
  | +- | 5 commas sharp | Turkish
  | ++- | 8 commas sharp | Turkish
  | bs | 5 commas flat | Turkish
  | bss | 8 commas flat | Turkish
  | bbs | 9 commas flat (?) | Unknown
  

An example output from VexFlow is shown here. This is actually a screenshot from the [VF test module "Accidental"](https://github.com/0xfe/vexflow/blob/master/tests/accidental_tests.js#L261).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow-microtones.png]]

Support for [more accidentals](https://github.com/0xfe/vexflow/issues/318) will occur when Gonville is replaced with a more standard and comprehensive font, such as those that are [SMuFL](http://www.smufl.org/)-compatible. SMuFL support is [an ongoing topic](https://github.com/0xfe/vexflow/issues/350) for VexFlow. Once this happens, it will be trivial-ish to add new mnemonics to represent those accidentals.

### Microtonal Key Signatures
VexFlow allows to specify key signatures that contain arbitrary accidentals, including microtonal ones, in place of the standard sharp and flat. An example output is shown here. This is a screenshot from the [VF test module "KeySignature"](https://github.com/0xfe/vexflow/blob/master/tests/keysignature_tests.js#L165).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow-keysig-altered.png]]

However, microtonal key signature support is not complete, because other musical traditions do not follow the canonical style of key signature layout. For example, Arabic musical notation includes key signatures such as Bb Eb F#. This is currently a [work in progress](https://github.com/0xfe/vexflow/issues/328). 
