## Tuplets

In vexflow, a tuplet (triplet, quintuplet, etc...) is created by providing an array of notes and defining a tuplet ratio for how to rhythmically fit those notes into a different duration. A triplet, for instance, fits three notes into the space of two; it has the tuplet ratio 3:2. A quintuplet fits five notes in the space of four, and has the ratio 5:4. Vexflow supports both simple tuplets and highly-complex tuplets, including the nesting of tuplets within tuplets.

### Syntax:
> `var tuplet = new Vex.Flow.Tuplet(notes_array[, options_object]);`

#### Parameters:
`notes_array`
 * The notes array is typically made up of `StaveNote`s, but can be made up of any type of note that inherits from `StemmableNote`, including `GhostNote` and `TabNote`.

`options_object`
 * The properties of the `options_object` are:
  * `num_notes`: fit this many notes...
  * `notes_occupied`: ...into the space of this many notes.
  * `location`: 1 (above notes, ┌─3─┐) or -1 (below, └─3─┘). Defaults to 1 (above).
    For code legibility, you may use `Vex.Flow.Tuplet.LOCATION_TOP` and `Vex.Flow.Tuplet.LOCATION_BOTTOM`
  * `bracketed`: boolean, whether to draw a bracket or show only the number(s). Defaults true if all of the tuplet notes are beamed, false otherwise. _Note:_ If you are relying on the default, you should apply beams before you create the tuplet, as this is checked only on tuplet creation.
  * `ratioed`: boolean, whether to show both numbers of the tuplet ratio. True: ┌─5:4─┐ False: ┌─5─┐. Defaults true if the difference between `num_notes` and `notes_occupied` is greater than 1.
  * `y_offset`: The distance by which the entire tuplet should be offset, to avoid (for instance) an articulation. (Use negative values to raise the tuplet, positive values to lower it.)

`num_notes` and `notes_occupied` together make up the tuplet ratio, and when `ratioed` is true, the ratio will be displayed as ┌─`num_notes`:`notes_occupied`─┐. _Caution:_ despite its slightly misleading name, `num_notes` does _not_ refer to the number of notes within the tuplet itself. Rather, it refers to the upper value of the tuplet ratio.

While `num_notes` and `notes_occupied` are not strictly required, for code legibility they are highly recommended. When omitted, `num_notes` defaults to the number of notes in `notes_array`, so if those notes are not all the same duration, you should be sure to include `num_notes`. Because `notes_occupied` defaults to 2, you should be sure to specify a value for anything other than a basic triplet.

### Example
These options are illustrated in this image:
![Tuplet example image](http://s22.postimg.org/7ipvuu4up/Screen_Shot_2016_03_21_at_4_08_19_PM.png)

Which is generated using this code:
```javascript
// Setup the notes_array
var notes = [
  ["c/4", "16"],
  ["d/4", "16"],
  ["e/4", "16"],
  ["f/4", "16"],
  ["g/4", "16"],
  ["a/4", "4"],
  ["b/4", "4"],
  ["c/5", "8"],
  ["b/4", "16"],
  ["a/4", "16"],
  ["g/4", "16"],
  ["f/4", "16"],
  ["e/4", "16"],
  ["d/4", "16"],
  ["c/4", "8"],
  ["b/3", "8"],
  ["c/4", "8"]
].map(function(noteStruct){
  return new Vex.Flow.StaveNote({
    keys: [noteStruct[0]], 
    duration: noteStruct[1]
  });
});

// Setup the beams: we do this before defining tuplets so that default bracketing will work.
var beams = [
  [0, 5], // c/4 - g/4
  [8, 13], // b/4 - e/4
  [14, 17] // c/4, b/3, c/4
].map(function(i){
  return new Vex.Flow.Beam(notes.slice(i[0], i[1]));
});

// Now create the tuplets:
var quarterNoteTriplet = new Vex.Flow.Tuplet(notes.slice(0, 8), {
  num_notes: 3, notes_occupied: 2, ratioed: true
});

var nestedQuintuplet = new Vex.Flow.Tuplet(notes.slice(0,5), {
  num_notes: 5, notes_occupied: 4, location: -1, bracketed: true
});

var nestedTriplet = new Vex.Flow.Tuplet(notes.slice(6,8), {
  num_notes: 3, notes_occupied: 2, location: -1
});

var complexQuintuplet = new Vex.Flow.Tuplet(notes.slice(8,13), {
  num_notes: 5, notes_occupied: 3
})

var simpleTriplet = new Vex.Flow.Tuplet(notes.slice(14,17));

// Create the voice:
var voice = new Vex.Flow.Voice({num_beats:4, resolution:Vex.Flow.RESOLUTION})
voice.addTickables(notes);

// Format the voice:
var formatter = new Vex.Flow.Formatter();
formatter.format([voice], 775);

// Draw the voice:
voice.draw(ctx, stave);

// Draw the beams:
beams.forEach(function(beam){
  beam.setContext(ctx).draw();
});

// Draw the tuplets:
[ quarterNoteTriplet, nestedQuintuplet, nestedTriplet, complexQuintuplet, simpleTriplet ]
.forEach(function(tuplet){
  tuplet.setContext(ctx).draw();
});
```