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

_TODO: Insert image_

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

TODO: Add more steps from [tutorial](http://www.vexflow.com/docs/tutorial.html)



