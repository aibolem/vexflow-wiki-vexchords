Currently VexFlow is in the process of migrating to [eslint](http://eslint.org/). Using a much stricter config than the previous jshint config provided.

* [Currently completed files](https://github.com/0xfe/vexflow/wiki/Migrating-to-ESLint#complete)
* [Discussion](https://github.com/0xfe/vexflow/issues/361)
* [Active Branch](https://github.com/Silverwolf90/vexflow/tree/eslint-all)
* [Initial PR #369 - with 4 example files](https://github.com/0xfe/vexflow/pull/369)

## Using eslint 

You have two options:

Running `grunt eslint` will run eslint on all the  [`ESLINT_SOURCES`](https://github.com/Silverwolf90/vexflow/blob/eslint-all/Gruntfile.js#L23)  expected to pass in the Gruntfile. You could just add a failing file to that array.

Or you can run eslint independently of grunt:

`cd <vexflow root>`
`npm install`
`eslint <path>`

## Basic Steps

**UPDATE: In the [branch](https://github.com/Silverwolf90/vexflow/tree/eslint-all) the first two steps have been run on each file. Only manual edits remain**

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

Here's the current `.eslintrc`, acquaint yourself with the [eslint rules](http://eslint.org/docs/rules/) and feel free to make suggestions. Note that we're extending the [`eslint-config-airbnb-base`](https://www.npmjs.com/package/eslint-config-airbnb-base)

```json
{
  "extends": "airbnb-base",
  "root": true,
  "rules": {
    "max-len": [2, 100],
    "camelcase": [0],
    "no-case-declarations": [2],
    "no-confusing-arrow": [0],
    "new-cap": [0],
    "no-else-return": [0],
    "no-multi-spaces": [0],
    "no-param-reassign": [0],
    "no-shadow": [0],
    "no-use-before-define": [0],
    "prefer-template": [0],
    "space-before-function-paren": [2, "never"],
    "strict": [2, "global"]
  }
}
```

## Complete

See branch: https://github.com/Silverwolf90/vexflow/tree/eslint-all

- [x] accidental.js
- [ ] annotation.js
- [ ] articulation.js
- [ ] barnote.js
- [ ] beam.js
- [ ] bend.js
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
- [ ] music.js
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
- [ ] stemmablenote.js
- [x] stringnumber.js
- [ ] strokes.js
- [ ] svgcontext.js
- [ ] tables.js
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