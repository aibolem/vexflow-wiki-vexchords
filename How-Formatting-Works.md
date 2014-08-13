(Draft, unedited)

VexFlow is really split up into two aspects, the Formatting related objects and the Rendering related objects.

The formatting related objects are the following:
* `Formatter`
* `ModifierContext`
* `TickContext`

The `TickContext` is what groups notes together across multiple voices. A `TickContext` is created for every unique tick position across all voices. See the following picture to see outlines of each `TickContext`.

*picture here*

Notice that these are these are what are in charge of providing x values to all `Tickable` based classes (eg: `Note`, `StaveNote`, etc-- any duration based class)

The `Formatter` is in charge of creating these `TickContexts` based on the voices provided, and if a width is included, it attempts to justify the `TickContexts` across that width. It purely deals with formatting across x values.

A `ModifierContext` contains a `Tickable` and its attached modifiers. One of its purposes is to keep track of the space needed on either side of the `Tickable`. The `TickContext` will use this data to expand as necessary. See below:

*picture here*

The `Formatter` creates the `ModifierContexts` when `Formatter.joinVoices(voices)` is called. You can pass multiple voices to the method in order to have Tickables at identical tick positions share a `ModifierContext`. This is specifically for formatting multiple voices onto the same Stave while making sure the modifiers do not overlap.

Notice what happens to the `TickContexts` when you do not create the `ModifierContexts`. Also notice that the accidentals are no longer avoiding each other but overlap. That's because the `ModifierContext` handles shifting modifiers to avoid collision.

*picture here*

It is important to note that basically every class has a `.preFormat()` and a `.postFormat()` method (modifiers do not, but instead have a `ModifierContext.format<modifierCategory>()`, this is bad and should be refactored into each individual object).
* `.preFormat()` deals with calculating widths so that the formatter can justify the objects. For modifiers this also deals with articulation stacking (but it's naive and could work better).
* `.postFormat()` deals with calculations that are necessary after x/y values have been assigned (eg: if stems have been extended for beams, articulations must be moved accordingly).

So let's take a look at the `Formatter.format()` "flow" from the top level.
* `Formatter.format(voices, justifyWidth, options)` gets called
  * `Formatter.createTickContexts(voices)` gets called, creates and stores the `TickContexts` that will exist across the voices. These contexts are not filled with any positioning data yet. They only contain the `Tickables` at that tick position.
  * `Formatter.preFormat(justifyWidth, canvasContext, voices)` gets called
    * For each `TickContext` we call `tickContext.preFormat()`
      * For each `Tickable` in the TickContext we call `tickable.preFormat()`
        * Each `tickable` has a `ModifierContext` which contains all the `tickable`'s modifiers (eg: accidentals, dots, etc), we call `modifierContext.preFormat()` to calculate the extra room the modifiers need on either side of the tickable
          * For each Modifier category in the `modifierContext`, we call `modifierContext.format<modifierCategory>()` we calculate and store the extra width needed. And we also modify the parent Tickable's properties with these calculated values.
      * For each `Tickable` (which now have calculated widths) in the `TickContext`,  we store the extra room needed on each side in the `tickContext` and the max width of the `Tickables`, giving us a total width for each `tickContext`
    * Since each `TickContext` has a calculated width, the `Formatter` can justify them throughout the provided j`ustifyWidth` accordingly
  * `Formatter.postFormat()` is called (but only if a Stave was provided to the formatter options, otherwise it is skipped because y values have not been provided)
    * Cascades down to the `ModifierContexts` like `.preFormat()` did.

One key thing to note, is that TickContext.x positions are not absolute, but relative to the provided width. So how does a StaveNote know where to render itself on the canvas? Note (the superclass of StaveNote) has a method called .getAbsoluteX(). See the code snippet:

```javascript
getAbsoluteX: function() {
  if (!this.tickContext) throw new Vex.RERR("NoTickContext",
      "Note needs a TickContext assigned for an X-Value");

  // Position note to left edge of tick context.
  var x = this.tickContext.getX();
  if (this.stave) x += this.stave.getNoteStartX() + this.render_options.stave_padding;
  return x;
}
```

So as you can see, with the combination of `stave.getNoteStartX()` (which returns the absolute X position for where notes are to start on this stave instance) and `tickContext.getX()` (which returns the relative X position of the `tickContext`), we get a correctly placed `StaveNote`.

**Where do the Y values for the `StaveNote.NoteHeads` come from?**
The Y values are assigned to the `NoteHeads` after calling `StaveNote.setStave(stave)`. Until a `Stave` is set, Y coordinate data does not exist. The Stave is the only source of data for Y positioning in VexFlow, any Note type class needs a `.setStave()` method in order to calculate y positions.