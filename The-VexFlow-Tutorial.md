VexFlow is an engraving engine for music notation, and can be used as a rendering backend to various kinds of web-based music tools, libraries, and applications. It written entirely in JavaScript, and works with both HTML5 Canvas and SVG.

This tutorial expects you to have some JavaScript programming experience and a basic understanding of music notation terminology.

Enjoy the show!

## Step 1: The Basics [ [run](https://jsfiddle.net/nL0cn3vL/2/) ]

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

Here's what it looks like: [ [run](https://jsfiddle.net/nL0cn3vL/2/) ]

![](https://i.imgur.com/WZe5i06.png)

Above, we first create a rendering context from the `DIV` element and specify the `SVG` backend. The rendering context is an abstraction that gives VexFlow a consistent 2D drawing interface across various backends. Typically you would do this just once per application lifetime.

The context is configurable -- you can control various properties such as colors, fonts, zoom level, etc.

We then create our first VexFlow element, `VF.Stave`, give it a position and size, and assign it a clef and time signature.

Finally, we pass the context to the stave and call `draw`, which renders the new element onto the context.

Notice that the stave is not exactly drawn in position 0, 0. This is because it reserves some head-room for higher notes. The amount of headroom can be configured with the `VF.Stave` properties.

## Step 2: Add Some Notes [ [run](https://jsfiddle.net/8eckj32x/2/) ]

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

Lets add a second voice with a single whole note to this tune. [ [run](https://jsfiddle.net/7y74r86s/1/) ]

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

Let's add some accidentals and dots. [ [run](https://jsfiddle.net/1tqmkeft/3/) ]

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

Lets add a few more modifiers and see how they position themselves. [ [run](https://jsfiddle.net/htsm03pn/1/) ]

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

TODO: Add more steps from [tutorial](http://www.vexflow.com/docs/tutorial.html)





