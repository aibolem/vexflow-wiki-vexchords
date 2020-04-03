### Principles

* Code must be readable.
* Code must be testable.
* In general, try to stick with the conventions in the existing code. (VexFlow is over a decade old, and there's a mix of styles in the code.)

### Preferred Style

* No hard-tabs. Use 2 spaces.
* Comments get preprocessed through [Docco](http://jashkenas.github.io/docco/). This allows Markdown in comments.
* Take a look at `src/accidentals.js` for commenting boilerplate.
   * In particular, note the header at the top of the file.
   * If you contributed significantly to the file, feel free to add an "Author:" comment below the copyright.
   * All methods and parameters must be documented.
   * Run `grunt docco` to regenerate the documentation in `docs/`.
   * Take a look at [docs/accidental.html](http://www.vexflow.com/docs/accidental.html) for an example of a generated document.
* Respect API boundaries. If you don't want your code to break, don't reach into its internals. E.g., prefer `note.getStave()` to `note.stave`.
* Run `grunt eslint` and `grunt test` before sending in a pull request.

### Preferred Abbreviations

In general, avoid abbreviations like the plague. Music already has ill-defined semantics and abbreviations only further obfuscate meaning. But here are some exceptions to avoid being verbose (where appropriate):

* `accidental` -> `accid`
  * Avoid `acc` because such an abbreviation could also refer to an `accent`
* `articulation` -> `artic`
* `bounding box` -> `bbox`

### New Files

If you're writing code that requires a new file, e.g., a new element, class, modifier, etc.

* Create the `.js` file in `src/` and a reference in `src/index.js`
* Add a test file to `tests/` and a reference in `tests/run.js`
  * Add `VF.Test.YourTest.Start()` to `tests/run.js`
  * If your file was called `slurs.js` the test file should be `slurs_test.js`.
* Run `grunt` to lint, build, and generate docs, and visually inspect the docs to verify correctness.
* Also run the [Visual Regression Tests](https://github.com/0xfe/vexflow/wiki/Visual-Regression-Tests) and verify that there are no unexpected regressions.