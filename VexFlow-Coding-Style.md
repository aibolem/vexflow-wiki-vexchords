### Principles

* Code must be readable.
* Code must be testable.
* In general, try to stick with the conventions in the existing code.

### Style

* No hard-tabs. Use 2 spaces.
* Comments get preprocessed through [Docco](http://jashkenas.github.io/docco/). This allows Markdown in comments.
* Take a look at `src/accidentals.js` for commenting boilerplate.
   * In particular, note the header at the top of the file.
   * If you contributed significantly to the file, feel free to add an "Author:" comment below the copyright.
   * All methods and parameters must be documented.
   * Run `grunt docco` to regenerate the documentation in `docs/`.
   * Take a look at [docs/accidental.html](http://www.vexflow.com/docs/accidental.html) for an example of a generated document.
* Respect API boundaries. If you don't want your code to break, don't reach into its internals. E.g., prefer `note.getStave()` to `note.stave`.
* Run `grunt jshint` before sending in a pull request.

### New Files

If you're writing code that requires a new file, e.g., a new element, class, modifier, etc.

* Create the `.js` file in `src/`
* Add the file to `SOURCES` in `Gruntfile`.
* Add a test file to `tests/`.
   * If your file was called `slurs.js` the test file should be `slurs_test.js`.
   * Use `tests/textnote_test.js` as a template.
* Include the test `.js` to `tests/flow.html` and add `Vex.Flow.Test.YourTest.Start()` to the document load function (also in `flow.html`.)
* Run `grunt` to lint, build, and generate docs, and visually inspect the docs to verify correctness.