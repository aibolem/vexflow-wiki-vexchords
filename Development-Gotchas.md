This list is a WIP and far from complete.

* The usage of the word `top` does not always mean the same thing. Sometimes it is relative to the stem direction, sometimes it is relative to the Canvas.
  * Examples 
    * A. `staveNote.getStemExtents()` returns a `topY` which references the y value of the stem's tip, **not** the top-most y point of the stem (which is what most people would expect, unfortunately). The `topY` is related to the stem direction, not the canvas.
    * B. `staveNote.getNoteheadBounds()` does the opposite. It returns a `y_top` and `y_bottom` that are relative to the canvas, not the stem direction.
  * **We should not have two different notions of "top" within the codebase.** It should always be relative to the Canvas coordinate system.

* There word `line` is very overloaded, and means drastically different things in different contexts
  * Examples
    * `staveNote.getKeyProps()` contains objects with a `line` property, that represents a more semantic understanding of the staff. Where the lines are indexed in a *1-based bottom-up* manner. ie, line `1` is E4 in treble clef -- the bottom-most line.
    * `stave.getYForLine(line)` takes a `line` argument which is intended to indexed in a *0-based top-down* manner. Meaning that the top-most line of the staff is line `0` 
    * `stave.getYFor{Top|Bottom}Text(line)` takes a `line` argument which is a *directional offset* from the `top_text_position` and `bottom_text_position` defined in `stave.options`
    * The `modifier.text_line`/`modifierContext.state.text_line` properties represent offsets from a modifier's *initial position*. There is not necessarily a relationship with the stave text positions. It could equally represent an offset from the stem tip or an offset from the stave's `top_text_position`
  * **We would ideally have one consistent way to reference locations on a staff.**

* The `stave` has an option called `spacing_between_lines_px` (often shorted to `line_spacing`) which is non-standard name for what is typically called the "staff/stave space".

* `Formatter#format` and `Formatter#formatToStave` take an `options` object with an `align_rests` property. However, if set to `false`, this will still align rests within beams. 