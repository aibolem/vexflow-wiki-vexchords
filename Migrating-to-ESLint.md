# Archived

This page is an archive of the work completed in July 2016 to use eslint to enforce code quality / style. As of 2021, VexFlow still uses [eslint](https://eslint.org/). See: .eslintrc

---

Currently VexFlow is in the process of migrating to [eslint](http://eslint.org/). Using a much stricter config than the previous jshint config provided.

* [Currently completed files](#complete)
* [Discussion](https://github.com/0xfe/vexflow/issues/361)

## Using eslint 

You have two options:

Running `grunt eslint` will run eslint on all the  [`ESLINT_SOURCES`](https://github.com/Silverwolf90/vexflow/blob/eslint-all/Gruntfile.js#L23)  expected to pass in the Gruntfile. You could just add a failing file to that array.

Or you can run eslint independently of grunt:
```
cd <vexflow root>
npm install
eslint <path>
```

## Basic Steps

**UPDATE: On master, the first two steps have been run on each file. Only manual edits remain**

1. ~~Run code through [`Lebab`](https://github.com/mohebifar/lebab) with `lebab <filepath> -o <filepath>`~~
  - [`Lebab`](https://github.com/mohebifar/lebab) is an ES5 to ES6 converter.
  - You can install it with `npm`. 
  - It seems to work quite well, but be sure to review the result because some transforms are unsafe.

2. ~~Run `eslint --fix` <file>~~
  - This will fix some pretty trivial things, but definitely saves time.

3. Manual edits
  - Despite the automated bits, many errors will remain.
  - Sometimes minor refactoring will be required

4. When finished add the file name to the `ESLINT_SOURCES` array in the `Gruntfile`

## Config

Config located here: https://github.com/0xfe/vexflow/blob/master/.eslintrc.json

Acquaint yourself with the [eslint rules](http://eslint.org/docs/rules/) and feel free to make suggestions. Note that we're extending the [`eslint-config-airbnb-base`](https://www.npmjs.com/package/eslint-config-airbnb-base)

## Complete

- [x] accidental.js
- [x] annotation.js
- [x] articulation.js
- [x] barnote.js
- [x] beam.js
- [x] bend.js
- [x] boundingbox.js
- [x] boundingboxcomputation.js
- [x] canvascontext.js
- [x] clef.js
- [x] clefnote.js
- [x] crescendo.js
- [x] curve.js
- [x] dot.js
- [x] formatter.js
- [x] fraction.js
- [x] frethandfinger.js
- [x] ghostnote.js
- [x] glyph.js
- [x] gracenote.js
- [x] gracenotegroup.js
- [x] index.js
- [x] keymanager.js
- [x] keysignature.js
- [x] modifier.js
- [x] modifiercontext.js
- [x] music.js
- [x] note.js
- [x] notehead.js
- [x] ornament.js
- [x] pedalmarking.js
- [x] raphaelcontext.js
- [x] renderer.js
- [x] stave.js
- [x] stavebarline.js
- [x] staveconnector.js
- [x] stavehairpin.js
- [x] staveline.js
- [x] stavemodifier.js
- [x] stavenote.js
- [x] staverepetition.js
- [x] stavesection.js
- [x] stavetempo.js
- [x] stavetext.js
- [x] stavetie.js
- [x] stavevolta.js
- [x] stem.js
- [x] stemmablenote.js
- [x] stringnumber.js
- [x] strokes.js
- [x] svgcontext.js
- [x] tables.js
- [x] tabnote.js
- [x] tabslide.js
- [x] tabstave.js
- [x] tabtie.js
- [x] textbracket.js
- [x] textdynamics.js
- [x] textnote.js
- [x] tickable.js
- [x] tickcontext.js
- [x] timesignature.js
- [x] timesignote.js
- [x] tremolo.js
- [x] tuning.js
- [x] tuplet.js
- [x] vex.js
- [x] vibrato.js
- [x] voice.js
- [x] voicegroup.js