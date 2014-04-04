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

#### Why is the API so complex?

VexFlow is in its third iteration, where each iteration was a complete overhaul. While the first two iterations were much simpler, it turns out that the scope of musical notation is huge and complex.

The desire to support complex musical notation while also providing a high degree of flexibility, steers the design of VexFlow.

Also note that VexFlow is a low-level rendering API. If all you want to do is display music on a page, take a look at higher level libraries such as [VexTab](http://vexflow.com/vextab/).

#### Can I build mobile apps with VexFlow?

Yes, and there are a number of VexFlow-based mobile apps already out there. These apps typically use frameworks like [PhoneGap](phonegap.com) to build HTML5 applications on phones and tablets.

#### Can VexFlow generate audio output from the scores?
#### Is there a VexFlow editor to enter music without writing code?
#### How do I import MusicXML / LilyPond / MEI notation?

### Formatting

#### How do I create and align multiple voices on a single stave?

If you have multiple voices on a single stave, call `Formatter.joinVoices` on them. This puts notes on the identical beats into the same `ModifierContext`, which in turn positions the various elements such that they don't collide with each other.

```javascript
voice1 = new Vex.Flow.Voice(...);
voice2 = new Vex.Flow.Voice(...);

voice1.addTickables([note1, note2, note3]);
voice2.addTickables([note1, note2, note3]);

formatter = new Vex.Flow.Formatter();
formatter.joinVoices([voice1, voice2]);
```

#### How do I align multiple voices across staves?

If you want to align voices across multiple stave (e.g., for building a grand staff), you can simply run the formatter without joining any voices. Remember that the formatter only positions the `x` coordinates, so the actual notes can be rendered anywhere.

```javascript
var voiceTreble = new Vex.Flow.Voice({num_beats:4, beat_value: 4, resolution:Vex.Flow.RESOLUTION});
var voiceBass = new Vex.Flow.Voice({num_beats:4, beat_value: 4, resolution:Vex.Flow.RESOLUTION});

voiceTreble.addTickables(notesTreble);
voiceBass.addTickables(notesBass);

var formatter = new Vex.Flow.Formatter();
formatter.format([voiceTreble, voiceBass], stave_length);

var max_x = Math.max(staveTreble.getNoteStartX(), staveBass.getNoteStartX());
staveTreble.setNoteStartX(max_x);
staveBass.setNoteStartX(max_x);

voiceTreble.draw(ctx, staveTreble);
voiceBass.draw(ctx, staveBass);
```

It is important to note that, since the stave modifiers (such as clef, key signature, etc.) take up room in the stave, you will need to render the voices such that they all start on the same `x` coordinate, else the notation will be misaligned. In the above code, `getNoteStartX()` and `setNoteStartX(...)` are used to do this.

#### How can I pre-calculate the width of a voice?

You can call `Formatter.getMinTotalWidth()` to return the minimum amount of horizontal space required to render a voice.

#### What are all these `context` classes? (`ModifierContext`, `TickContext` etc.)

### API

#### Can VexFlow automatically generate beams?

Yes, and there are a few ways to do it.

#### How do I render slurs?
#### How can I align text to notation?
#### Can I color notes individually?
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




