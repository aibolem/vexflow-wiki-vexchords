VexFlow is an engraving engine for music notation, and can be used as a rendering backend to various kinds of web-based music tools, libraries, and applications. It written entirely in JavaScript, and works with both HTML5 Canvas and SVG.

This tutorial expects you to have some JavaScript programming experience and a basic understanding of music notation terminology.

Enjoy the show!

## Step 1: The Basics [ [run](https://jsfiddle.net/gs4v6k6d/2//) ]

Lets start with a quick example. Below, we have an HTML DIV element with the following code:

```html
<div id="boo"></div>
```

Let's draw an empty stave on this canvas, and set the clef and time signature.

```javascript
VF = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element named "boo".
var div = document.getElementById("boo")
var renderer = new VF.Renderer(div, VF.Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(500, 500);
var context = renderer.getContext();
context.setFont("Arial", 10, "").setBackgroundFillStyle("#eed");

// Create a stave of width 400 at position 10, 40 on the canvas.
var stave = new VF.Stave(10, 40, 400);

// Add a clef and time signature.
stave.addClef("treble").addTimeSignature("4/4");

// Connect it to the rendering context and draw!
stave.setContext(context).draw();
```        

Here's what it looks like: [ [run](https://jsfiddle.net/gs4v6k6d/2/) ]

![](https://i.imgur.com/WZe5i06.png)

Above, we first create a rendering context from the `DIV` element and specify the `SVG` backend. The rendering context is an abstraction that gives VexFlow a consistent 2D drawing interface across various backends. Typically you would do this just once per application lifetime.

The context is configurable -- you can control various properties such as colors, fonts, zoom level, etc.

We then create our first VexFlow element, `VF.Stave`, give it a position and size, and assign it a clef and time signature.

Finally, we pass the context to the stave and call `draw`, which renders the new element onto the context.

Notice that the stave is not exactly drawn in position 0, 0. This is because it reserves some head-room for higher notes. The amount of headroom can be configured with the `VF.Stave` properties.

## Step 2: Add Some Notes [ [run](https://jsfiddle.net/8eckj32x/13/) ]

A `StaveNote` is a group of note heads representing a chord. It can consist of one or more notes, with or without a stem and flag.

A sequence of notes is represented by a `Voice`, and multiple voices can be grouped within a `VoiceGroup`.

Finally, you have the `Formatter`, which takes a voice group and alignes, justifies, and renders the voices based on configurable rules, so that all the voices in the group look pretty on the stave(s).

In the code below, we create a voice with two notes and a chord, and render it on the stave. 

```javascript
var notes = [
  // A quarter-note C.
  new VF.StaveNote({ keys: ["c/4"], duration: "q" }),

  // A quarter-note D.
  new VF.StaveNote({ keys: ["d/4"], duration: "q" }),

  // A quarter-note rest. Note that the key (b/4) specifies the vertical
  // position of the rest.
  new VF.StaveNote({ keys: ["b/4"], duration: "qr" }),

  // A C-Major chord.
  new VF.StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "q" })
];

// Create a voice in 4/4 and add above notes
var voice = new VF.Voice({num_beats: 4,  beat_value: 4});
voice.addTickables(notes);

// Format and justify the notes to 400 pixels.
var formatter = new VF.Formatter().joinVoices([voice]).format([voice], 400);

// Render voice
voice.draw(context, stave);
```

![](http://imgur.com/NT62Q7g.png)

Notice how the notes are justified evenly on the stave based on the duration of each note? This is the formatter in action - keeping voices aligned, while balancing the spacing between the notes.

Lets add a second voice with a single whole note to this tune. [ [run](https://jsfiddle.net/7y74r86s/4/) ]

```javascript
var notes = [
  new VF.StaveNote({ keys: ["c/5"], duration: "q" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "q" }),
  new VF.StaveNote({ keys: ["b/4"], duration: "qr" }),
  new VF.StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "q" })
];

var notes2 = [
  new VF.StaveNote({ keys: ["c/4"], duration: "w" })
];

// Create a voice in 4/4 and add above notes
var voices = [
	new VF.Voice({num_beats: 4,  beat_value: 4}).addTickables(notes),
	new VF.Voice({num_beats: 4,  beat_value: 4}).addTickables(notes2)]

// Format and justify the notes to 400 pixels.
var formatter = new VF.Formatter().joinVoices(voices).format(voices, 400);

// Render voices
voices.forEach(function(v) { v.draw(context, stave); })
```

![](http://imgur.com/sk1RC26.png)

## Step 3: All About Modifiers

A modifier is an element that is attached to a note. Modifiers typically inherit from the `VF.Modifier` base class, e.g., `VF.Accidental` representing accidentals, `VF.Vibrato` for vibratos, `VF.Annotation` for annotations , etc.

Modifiers are self-positioning -- they intelligently juxtapose themselves alongside other modifiers and notes based on standard music notation rules.

Let's add some accidentals and dots. [ [run](https://jsfiddle.net/1tqmkeft/9/) ]

```javascript
var notes = [
    new VF.StaveNote({ keys: ["e##/5"], duration: "8d" }).
      addAccidental(0, new VF.Accidental("##")).addDotToAll(),

    new VF.StaveNote({ keys: ["eb/5"], duration: "16" }).
      addAccidental(0, new VF.Accidental("b")),

    new VF.StaveNote({ keys: ["d/5", "eb/4"], duration: "h" }).
    	addDot(0),

    new VF.StaveNote({ keys: ["c/5", "eb/5", "g#/5"], duration: "q" }).
      addAccidental(1, new VF.Accidental("b")).
      addAccidental(2, new VF.Accidental("#")).addDotToAll()
  ];

VF.Formatter.FormatAndDraw(context, stave, notes);
```

![](http://imgur.com/3wVLRxx.png)

In the above example, note that even though we set the note names and durations correctly, we explicitly request the rendering of accidentals and dots.

This is by design, and allows us to decouple rendering logic and notational semantics. For example, you would not want to render the `#` accidental on `F#` when the key signature already includes it (e.g., key of `G`.)

Also notice that we `FormatAndDraw`, which is a handy helper function that takes care of all the plumbing related to displaying a sequence of notes.

Lets add a few more modifiers and see how they position themselves. [ [run](https://jsfiddle.net/htsm03pn/3/) ]

```javascript
var notes = [
    new VF.StaveNote(
      { keys: ["g/4", "b/4", "cb/5", "e/5", "g#/5", "b/5"],
        duration: "h" }).
      addAccidental(0, new VF.Accidental("bb")).
      addAccidental(1, new VF.Accidental("b")).
      addAccidental(2, new VF.Accidental("#")).
      addAccidental(3, new VF.Accidental("n")).
      addAccidental(4, new VF.Accidental("b")).
      addAccidental(5, new VF.Accidental("##")),
    new Vex.Flow.StaveNote({ keys: ["c/4"], duration: "h" })
  ];

  // Helper function to justify and draw a 4/4 voice
VF.Formatter.FormatAndDraw(context, stave, notes);
```

![](http://imgur.com/6cjs3Rf.png)

Notice how VexFlow position the accidentals such that they don't collide with each other?

## Step 3.5: An Interlude

We've covered a bit of ground here, and you're probably asking for lists of valid note names, accidentals, durations, etc., that you can use with the API.

Fortunately for you, there's a canonical location where this stuff is kept. [VexFlow Tables (vexflow/src/tables.js)](https://github.com/0xfe/vexflow/blob/master/src/tables.js)

Take a look at some of the following tables:

* `Flow.clefProperties.values` - List of valid clef names.
* `Flow.keyProperties.note_values` - The list of valid note names.
* `Flow.accidentalCodes.accidentals` - The list of valid accidental names.
* `Flow.keySignatures.keySpecs` - The list of valid keys.
* `Flow.durationToTicks` - The list of valid duration codes.
* `Flow.articulationCodes.articulations` - List of articulation codes.
* `Flow.ornamentCodes.ornaments` - List of ornament codes.

## Step 4: Beam Your Notes

VexFlow can beam your notes for you, but only if you ask it to. The Beam class, when passed a set of contiguous notes (in a shared voice), is responsible for rendering beams based on the durations of each contained note.
Let's create a melody. 

```javascript
var notes = [
  new VF.StaveNote({ keys: ["e##/5"], duration: "8d" }).
	  addAccidental(0, new VF.Accidental("##")).addDotToAll(),
  new VF.StaveNote({ keys: ["b/4"], duration: "16" }).
  	addAccidental(0, new VF.Accidental("b"))
];

var notes2 = [ /* another group of notes */ ];
var notes3 = [ /* another group of notes */ ];
var notes4 = [ /* another group of notes */ ];

// Create a beam for each group of notes
beams = [
  new VF.Beam(notes),
  new VF.Beam(notes2),
  new VF.Beam(notes3)
]

// Render the notes followed by the beams
var all_notes = notes.concat(notes2).concat(notes3).concat(notes4);
Vex.Flow.Formatter.FormatAndDraw(context, stave, all_notes);
beams.forEach(function(b) {b.setContext(context).draw()})
```

![](http://imgur.com/40H5CTT.png)

In the above example ([run](https://jsfiddle.net/fvqmq9rd/3/)], we created four groups of notes and beamed each groups. The slope of the beams is calculated automatically as a function of the direction of the music. The number of beam lines for each group is dependent on the duration of the notes underneath.

For long scores, manually creating a `Beam` object for each group of notes can get tedious. Luckily, the `Beam` module provides a static method, `generateBeams()`, that allow us to automatically generate beams for our notes. It has two parameters, the notes to automatically beam and a config object. The config object provides many options to beam your notes in different ways, but let's start simple.

```javascript
var notes = [
  new VF.StaveNote({ keys: ["e##/5"], duration: "8d" }).
	  addAccidental(0, new VF.Accidental("##")).addDotToAll(),
  new VF.StaveNote({ keys: ["b/4"], duration: "16" }).
  	addAccidental(0, new VF.Accidental("b")),
  new VF.StaveNote({ keys: ["c/4"], duration: "8" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "16" }),
  new VF.StaveNote({ keys: ["e/4"], duration: "16" }).
	  addAccidental(0, new VF.Accidental("b")),
  new VF.StaveNote({ keys: ["d/4"], duration: "16" }),
  new VF.StaveNote({ keys: ["e/4"], duration: "16" }).
  	addAccidental(0, new VF.Accidental("#")),
  new VF.StaveNote({ keys: ["g/4"], duration: "32" }),
  new VF.StaveNote({ keys: ["a/4"], duration: "32" }),
  new VF.StaveNote({ keys: ["g/4"], duration: "16" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "q" })
];

var beams = VF.Beam.generateBeams(notes);
Vex.Flow.Formatter.FormatAndDraw(context, stave, notes);
beams.forEach(function(b) {b.setContext(context).draw()})
```

![](http://imgur.com/fCh5jJz.png)

Notice two things above ([run](https://jsfiddle.net/18whg1he/1/)]:

* Notes were automatically grouped.
* The stem directions were automatically calculated.

`generateBeams()` will calculate an appropriate stem direction for the entire beam group, even if it was set to a different position earlier.

For more sophisticated beaming examples, take a look at the [Automatic Beaming](https://github.com/0xfe/vexflow/wiki/Automatic-Beaming) wiki page.

## Step 5: Ties

To render a tie, you create a `StaveTie` instance and pass it the two `StaveNotes`. Since the `StaveNote` elements can also be chords, you need to pass in the indices of the specific note heads you want to tie.

```javascript
var notes = [
  new VF.StaveNote({ keys: ["e##/5"], duration: "8d" }).
	  addAccidental(0, new VF.Accidental("##")).addDotToAll(),
  new VF.StaveNote({ keys: ["b/4"], duration: "16" }).
  	addAccidental(0, new VF.Accidental("b")),
  new VF.StaveNote({ keys: ["c/4"], duration: "8" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "16" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "16" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "q" }),
  new VF.StaveNote({ keys: ["d/4"], duration: "q" })
];

var beams = VF.Beam.generateBeams(notes);
VF.Formatter.FormatAndDraw(context, stave, notes);
beams.forEach(function(b) {b.setContext(context).draw()})

var ties = [
  new VF.StaveTie({
    first_note: notes[4],
    last_note: notes[5],
    first_indices: [0],
    last_indices: [0]
  }),
  new VF.StaveTie({
    first_note: notes[5],
    last_note: notes[6],
    first_indices: [0],
    last_indices: [0]
  })
];
ties.forEach(function(t) {t.setContext(context).draw()})
```

And here's what it looks like [[run](https://jsfiddle.net/x1mgkv5v/9/)]:

![](http://imgur.com/YUNpn9G.png)

And there you have beams and ties!

## Step 6: Guitar Tablature

VexFlow can also render guitar tablature. The mechanics for displaying tabs are the same as those for standard notation, except that you use different classes for staves and notes.

Let's write some tab. 

```javascript
// Create a tab stave of width 400 at position 10, 40 on the canvas.
var stave = new VF.TabStave(10, 40, 400);
stave.addClef("tab").setContext(context).draw();

var notes = [
  // A single note
  new VF.TabNote({
    positions: [{str: 3, fret: 7}],
    duration: "q"}),

  // A chord with the note on the 3rd string bent
  new VF.TabNote({
    positions: [{str: 2, fret: 10},
                {str: 3, fret: 9}],
    duration: "q"}).
  addModifier(new VF.Bend("Full"), 1),

  // A single note with a harsh vibrato
  new VF.TabNote({
    positions: [{str: 2, fret: 5}],
    duration: "h"}).
  addModifier(new VF.Vibrato().setHarsh(true).setVibratoWidth(70), 0)
];

VF.Formatter.FormatAndDraw(context, stave, notes);
```        

![](https://imgur.com/sHVMhtc.png)

Above ([run](https://jsfiddle.net/7yaykcjp/8/)), we replaced `Stave` with `TabStave` and `StaveNote` with `TabNote`. We also added a `Bend` and a `Vibrato` modifier.

There are two things we have to manually specify here -- the font style, and the background fill color. The former is used to display fret numbers, annotations, and other text. The latter is only required for the SVG backend (although using it with Canvas is harmless).