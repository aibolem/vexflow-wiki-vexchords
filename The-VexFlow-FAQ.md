### Basics
#### What is VexFlow?

VexFlow is an open-source web-based music notation rendering API. It is written completely in JavaScript, and runs right in the browser. VexFlow supports HTML5 Canvas and SVG, and runs on all modern browsers.

#### What platforms does it run on?

VexFlow has been tested on Google Chrome, Firefox, Safari, Opera, and Internet Explorer 10+.

#### What features does it support?

VexFlow has support for standard music, guitar tablature, and percussion notation. While it is a goal to support the vast majority of western music notation, VexFlow also supports a few alternative elements, such as, microtonal notation.

To see a everything VexFlow can render, take a look at the [tests](http://www.vexflow.com/tests/index.html) (scroll down to see the images.)

#### How do I learn to use the VexFlow API?

The best place to start is the [VexFlow Tutorial](http://www.vexflow.com/docs/tutorial.html). Once you're comfortable with the basics of the API, start looking at the tests in `tests/*.js` for examples of how to use the various notational elements and tools.

#### Can I build mobile apps with VexFlow?

Yes, and there are a number of VexFlow-based mobile apps already out there. These apps typically use frameworks like [PhoneGap](phonegap.com) to build HTML5 applications on phones and tablets.

### Formatting

#### How do I auto-format my note modifiers (accidentals, etc)?

Even with a single voice, you must always call `Formatter.joinVoices([voice])` if you want your note modifiers to be formatted when calling `Formatter.format([voice])`.

#### How do I create and align multiple voices on a single stave?

If you have multiple voices on a single stave, call `Formatter.joinVoices` with an array containing the voices. This causes notes at simultaneous timestamps to share a `ModifierContext`, which, upon calling `.format()` (or `.formatToStave()`) positions the notes and their modifiers such that they don't collide with each other.

```javascript
voice1 = new Vex.Flow.Voice(...);
voice2 = new Vex.Flow.Voice(...);

voice1.addTickables([note1, note2, note3]);
voice2.addTickables([note1, note2, note3]);

formatter = new Vex.Flow.Formatter();
formatter.joinVoices([voice1, voice2]);
formatter.format([voice1, voice2], stave_length);
```

#### How do I align multiple voices across staves?

If you want to align voices across multiple staves (e.g., for building a grand staff), you should only call `joinVoices` on voices that **share a stave**. However, you should call `format` with **all aligned voices**. Remember that the formatter only positions the `x` coordinates, so the actual notes can be rendered anywhere.

```javascript
var voiceTreble = new Vex.Flow.Voice({num_beats:4, beat_value: 4, resolution:Vex.Flow.RESOLUTION});
var voiceBass = new Vex.Flow.Voice({num_beats:4, beat_value: 4, resolution:Vex.Flow.RESOLUTION});

voiceTreble.addTickables(notesTreble).setStave(staveTreble);
voiceBass.addTickables(notesBass).setStave(staveBass);

var formatter = new Vex.Flow.Formatter();

// Make sure the staves have the same starting point for notes
var startX = Math.max(staveTreble.getNoteStartX(), staveBass.getNoteStartX());
staveTreble.setNoteStartX(startX);
staveBass.setNoteStartX(startX);

// the treble and bass are joined independently but formatted together
formatter.joinVoices([voiceTreble]);
formatter.joinVoices([voiceBass]);
formatter.format([voiceTreble, voiceBass], stave_length - (startX - staveX));

voiceTreble.setContext(ctx).draw();
voiceBass.setContext(ctx).draw();
```

It is important to note that, since the stave modifiers (such as clef, key signature, etc.) take up room in the stave, you will need to render the voices such that they all start on the same `x` coordinate, else the notation will be misaligned. In the above code, `getNoteStartX()` and `setNoteStartX(...)` are used to do this.

#### How can I pre-calculate the width of a voice?

You can call `Formatter.getMinTotalWidth()` to return the minimum amount of horizontal space required to render a voice.

#### What are all these `context` classes? (`ModifierContext`, `TickContext` etc.)

### API

#### Can VexFlow automatically generate beams?

Yes, and there are a few ways to do it. See [Automatic Beaming](https://github.com/0xfe/vexflow/wiki/Automatic-Beaming) for more instructions.

#### Can I color notes individually?

Yes.  Each of the pitches within a StaveNote (known in VexFlow as "keys"), or the entire note (including stem) can be styled using StaveNote's setKeyStyle(keyIndex, styleObject) or setStyle(styleObject) properties.  

The styleObject is an object with any of these properties:
- fillStyle: the color of the fill (e.g. inner part of a notehead), in the form of a CSS accepted color value.
- strokeStyle: the color of the line strokes (e.g. the stem of a note)
- shadowColor: the color of a note's shadow
- shadowBlur: the blur radius of the shadow, in pixels, passed as an integer.

```javascript

// use StaveNote.setStyle() to color all noteheads & the stem:
var C7 = new Vex.Flow.StaveNote({ keys: ['C/4', 'E/4', 'G/4', 'Bb/4'], duration: '8'});
C7.setStyle({strokeStyle: "blue", stemStyle: "blue"});

// use StaveNote.setKeyStyle(keyIndex, styleObject) to style an individual notehead.
// in this example, we use keyIndex = 2, referring to the key "A/4"
var FMaj = new Vex.Flow.StaveNote({ keys: ['C/4', 'F/4', 'A/4'], duration: '8'});
FMaj.setKeyStyle(2, {shadowColor: "yellow", shadowBlur: 3});
```

#### How do I display grace notes?

Grace notes are created by adding a `GraceNoteGroup` modifier to your `StaveNote`. The `GraceNoteGroup` consists of `GraceNote` instances, which are only slightly different from `StaveNotes`. You can call `beamNotes()` on the group to auto-beam the grace notes.

```javascript
var notes = [
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: '8'})
];
 
var gracenote = new Vex.Flow.GraceNote({keys: ['d/4'], duration: '16', slash: true });
var gracenotegroup = new Vex.Flow.GraceNoteGroup([gracenote], true);
 
notes[0].addModifier(0, gracenotegroup.beamNotes());
 
var voice = new Vex.Flow.Voice({num_beats: 4, beat_value: 4});
voice.addTickables(notes);
 
var formatter = new Vex.Flow.Formatter();
formatter.joinVoices([voice]).formatToStave([voice], stave);
voice.draw(ctx, stave);
```

This [jsfiddle](https://jsfiddle.net/vW9v5/24/) is a more advanced example of grace notes.

#### How do I display mid-measure clef?

You can display mid-measure clef by adding a `NoteSubGroup` modifier to your `StaveNote`. The `NoteSubGroup` can consists of any kind of `Note` instances, but you may usually use `NoteSubGroup` with `ClefNote` only.

It is also possible to use `ClefNote` without `NoteSubGroup`, but it is not recommended because of multi-voice formatting issue, `ClefNote` without `NoteSubGroup` does not support multi-voice.

```javascript
var notes = [
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: 'q'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: 'q'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: 'q'}),
  new Vex.Flow.StaveNote({ keys: ['c/4'], duration: 'q'})
];
 
var clefNote = new Vex.Flow.ClefNote('bass', 'small');
var noteSubGroup = new Vex.Flow.NoteSubGroup([clefNote]);
notes[2].addModifier(0, noteSubGroup);

var voice = new Vex.Flow.Voice({num_beats: 4, beat_value: 4});
voice.addTickables(notes);
 
var formatter = new Vex.Flow.Formatter();
formatter.joinVoices([voice]).formatToStave([voice], stave);
voice.draw(ctx, stave);
```

[NoteSubGroup tests](http://public.vexflow.com/tests/?module=NoteSubGroup) have more advanced examples.



