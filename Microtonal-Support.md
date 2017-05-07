VexFlow currently supports microtones in two areas: accidentals and key signatures.

### Microtonal Accidentals
VexFlow supports SOME microtonal accidentals. The limitation comes mainly from the usage of the Gonville music font that does not contain glyphs for many such accidentals. Of course, assembling a full set of accidentals used across musical cultures and traditions is a major undertaking in and of itself, and music engraving systems all vary in their support.

The microtonal accidentals that VexFlow supports are:

Glyph | Mnemonic | Description | Notation System(s)
----- | -------- | ----------- | ------------------
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%23.png]] | # | sharp | Standard and all others
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%23%23.png]] | ## | double sharp | Standard and all others
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/b.png]] | b | flat | Standard and all others
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/bb.png]] | bb | double flat | Standard and all others
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/n.png]] | n | natural | Standard and all others 
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%2B.png]] | + | 1 quarter-tone sharp | Arabic / Stein-Zimmermann
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%2B.png]] | + | 1 comma sharp | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%2B%2B.png]] | ++ | 3 quarter-tones sharp | Arabic / Stein-Zimmermann
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/bs.png]] | bs | 1 quarter-tone flat | Arabic
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/d.png]] | d | 1 quarter-tone flat | Stein-Zimmermann
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/d.png]] | d | 1 comma flat | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/db.png]] | db | 3 quarter-tones flat | Stein-Zimmermann
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%2B-.png]] | +- | 5 commas sharp | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/%2B%2B-.png]] | ++- | 8 commas sharp | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/bs.png]] | bs | 5 commas flat | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/bss.png]] | bss | 8 commas flat | Turkish
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/bbs.png]] | bbs | 9 commas flat (?) | Unknown
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/k.png]] | k | 2-3 commas flat (koron) | Iranian
[[https://github.com/infojunkie/music-l10n/raw/master/images/vexflow/o.png]] | o | 2-3 commas sharp (sori) | Iranian
  

An example output from VexFlow is shown here. This is actually a screenshot from the [VF test module "Accidental"](https://github.com/0xfe/vexflow/blob/master/tests/accidental_tests.js#L302).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow/microtones.png]]

It is planned to further expand support for microtonal accidentals when Gonville is replaced with a more standard and comprehensive font, such as those that are [SMuFL](http://www.smufl.org/)-compatible. SMuFL support is [an ongoing topic](https://github.com/0xfe/vexflow/issues/350) for VexFlow. Once this happens, it will be trivial-ish to add new mnemonics to represent those accidentals.

### Microtonal Key Signatures
VexFlow allows to specify key signatures that contain arbitrary accidentals, including microtonal ones, in place of the standard sharp and flat. An example output is shown here. This is a screenshot from the [VF test module "KeySignature"](https://github.com/0xfe/vexflow/blob/master/tests/keysignature_tests.js#L165).
[[https://github.com/infojunkie/music-l10n/blob/master/images/vexflow/keysig-altered.png]]

However, microtonal key signature support is not complete, because other musical traditions do not follow the canonical style of key signature layout. For example, Arabic musical notation includes key signatures such as Bb Eb F#. This is currently a [work in progress](https://github.com/0xfe/vexflow/issues/328). 
