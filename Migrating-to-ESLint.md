Currently VexFlow is in the process of migrating to [eslint](http://eslint.org/). Using a much stricter config than the previous jshint config provided.

* [Currently completed files](https://github.com/0xfe/vexflow/wiki/Migrating-to-ESLint#complete)
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
- [ ] boundingbox.js
- [ ] boundingboxcomputation.js
- [ ] canvascontext.js
- [x] clef.js
- [ ] clefnote.js
- [ ] crescendo.js
- [ ] curve.js
- [ ] dot.js
- [x] formatter.js
- [ ] fraction.js
- [x] frethandfinger.js
- [ ] ghostnote.js
- [ ] glyph.js
- [ ] gracenote.js
- [ ] gracenotegroup.js
- [ ] header.js
- [ ] index.js
- [ ] keymanager.js
- [ ] keysignature.js
- [ ] modifier.js
- [x] modifiercontext.js
- [x] music.js
- [ ] note.js
- [ ] notehead.js
- [ ] ornament.js
- [ ] pedalmarking.js
- [ ] raphaelcontext.js
- [ ] renderer.js
- [x] stave.js
- [ ] stavebarline.js
- [x] staveconnector.js
- [ ] stavehairpin.js
- [ ] staveline.js
- [ ] stavemodifier.js
- [x] stavenote.js
- [ ] staverepetition.js
- [ ] stavesection.js
- [ ] stavetempo.js
- [ ] stavetext.js
- [ ] stavetie.js
- [ ] stavevolta.js
- [ ] stem.js
- [x] stemmablenote.js
- [x] stringnumber.js
- [x] strokes.js
- [ ] svgcontext.js
- [x] tables.js
- [ ] tabnote.js
- [ ] tabslide.js
- [ ] tabstave.js
- [ ] tabtie.js
- [ ] textbracket.js
- [ ] textdynamics.js
- [ ] textnote.js
- [ ] tickable.js
- [ ] tickcontext.js
- [ ] timesignature.js
- [ ] timesignote.js
- [x] tremolo.js
- [x] tuning.js
- [ ] tuplet.js
- [x] vex.js
- [x] vibrato.js
- [x] voice.js
- [ ] voicegroup.js