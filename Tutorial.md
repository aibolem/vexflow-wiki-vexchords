VexFlow is an engraving engine for music notation and can be used as a rendering backend to various kinds of web-based music tools, libraries, and applications. It written in TypeScript/JavaScript and works with both HTML5 Canvas and SVG.

This tutorial expects you to have JavaScript programming experience and a basic understanding of music notation terminology.

# Step 1: The Basics [ [run](https://jsfiddle.net/cwnsrep9/) ]

Let's start with a quick example. Below, we have an HTML DIV element with the following code:

```html
<div id="output"></div>
```

Add [some boilerplate](https://github.com/0xfe/vexflow/wiki/Understanding-Renderer-&-Context) to create and size an SVG and get a drawing `context`:

```javascript
VF = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element named "boo".
var div = document.getElementById("output");
var renderer = new VF.Renderer(div, VF.Renderer.Backends.SVG);

// Size our SVG:
renderer.resize(500, 500);

// And get a drawing context:
var context = renderer.getContext();
```

Let's draw an empty stave on this SVG, and set the clef and time signature.

```javascript
// Create a stave at position 10, 40 of width 400 on the canvas.
var stave = new VF.Stave(10, 40, 400);

// Add a clef and time signature.
stave.addClef("treble").addTimeSignature("4/4");

// Connect it to the rendering context and draw!
stave.setContext(context).draw();
```

[Here's what it looks like.](https://jsfiddle.net/cwnsrep9/)

![](https://i.imgur.com/WZe5i06.png)

Above, we first create a rendering context from the `DIV` element and specify the `SVG` backend. The rendering context is an abstraction that gives VexFlow a consistent 2D drawing interface across various backends. Typically you would do this just once per application lifetime.

The context is configurable – you can control various properties such as colors, fonts, zoom level, etc. (For a deep dive into VexFlow's drawing `context`, check out [Understanding Renderer & Context](https://github.com/0xfe/vexflow/wiki/Understanding-Renderer-&-Context))

We then create our first VexFlow element, `new Stave(...)`, give it a position and size, and assign it a clef and time signature.

Finally, we pass the context to the stave and call `draw`, which renders the new element onto the context.

Notice that the stave is not exactly drawn in position 0, 0. This is because it reserves some head-room for higher notes. The amount of headroom can be configured with the `Stave` properties.

# Step 2: Add Some Notes [ [run](https://jsfiddle.net/4gj06fqo/1/) ]

A `StaveNote` is a group of note heads representing a chord. It can consist of one or more notes with or without a stem and flag.

A sequence of notes is represented by a `Voice`, and multiple voices can be grouped within a `VoiceGroup`.

Finally, you have the `Formatter`, which takes a voice group and aligns, justifies, and renders the voices based on configurable rules, so that all the voices in the group look pretty on the stave(s).

In the code below we create a voice with two notes and a chord and render it on the stave.

```javascript
var notes = [
    // A quarter-note C.
    new VF.StaveNote({ clef: "treble", keys: ["c/4"], duration: "q" }),

    // A quarter-note D.
    new VF.StaveNote({ clef: "treble", keys: ["d/4"], duration: "q" }),

    // A quarter-note rest. Note that the key (b/4) specifies the vertical
    // position of the rest.
    new VF.StaveNote({ clef: "treble", keys: ["b/4"], duration: "qr" }),

    // A C-Major chord.
    new VF.StaveNote({ clef: "treble", keys: ["c/4", "e/4", "g/4"], duration: "q" }),
];

// Create a voice in 4/4 and add the notes from above
var voice = new VF.Voice({ num_beats: 4, beat_value: 4 });
voice.addTickables(notes);

// Format and justify the notes to 350 pixels (50 pixels left for key and time signatures).
var formatter = new VF.Formatter().joinVoices([voice]).format([voice], 350);

// Render voice
voice.draw(context, stave);
```

![](http://imgur.com/NT62Q7g.png)

Notice how the notes are justified evenly on the stave based on the duration of each note? This is the formatter in action - keeping voices aligned while balancing the spacing between the notes.

Let's add a second voice with a single whole note to this tune. [ [run](https://jsfiddle.net/n501pwm4/1/) ]

```javascript
var notes = [
    new VF.StaveNote({ clef: "treble", keys: ["c/5"], duration: "q" }),
    new VF.StaveNote({ clef: "treble", keys: ["d/4"], duration: "q" }),
    new VF.StaveNote({ clef: "treble", keys: ["b/4"], duration: "qr" }),
    new VF.StaveNote({ clef: "treble", keys: ["c/4", "e/4", "g/4"], duration: "q" }),
];

var notes2 = [new VF.StaveNote({ clef: "treble", keys: ["c/4"], duration: "w" })];

// Create a voice in 4/4 and add the notes from above
var voices = [new VF.Voice({ num_beats: 4, beat_value: 4 }).addTickables(notes), new VF.Voice({ num_beats: 4, beat_value: 4 }).addTickables(notes2)];

// Format and justify the notes to 400 pixels.
var formatter = new VF.Formatter().joinVoices(voices).format(voices, 400);

// Render voices
voices.forEach(function (v) {
    v.draw(context, stave);
});
```

![](http://imgur.com/sk1RC26.png)

# Step 3: Modifiers

A modifier is an element that is attached to a note. Modifiers typically inherit from the `Modifier` base class. VexFlow supports modifiers like `Accidental`, `Vibrato`, `Annotation`, and more.

Modifiers are self-positioning – they intelligently juxtapose themselves alongside other modifiers and notes based on standard music notation rules.

Let's add some accidentals and dots. [ [run](https://jsfiddle.net/4rt75dja/) ]

```javascript
var notes = [
    new VF.StaveNote({ clef: "treble", keys: ["e##/5"], duration: "8d" }).addModifier(new Accidental("##")).addDotToAll(),

    new StaveNote({ clef: "treble", keys: ["eb/5"], duration: "16" }).addModifier(new Accidental("b")),

    new StaveNote({ clef: "treble", keys: ["d/5", "eb/4"], duration: "h" }).addDot(0),

    new StaveNote({ clef: "treble", keys: ["c/5", "eb/5", "g#/5"], duration: "q" }).addAccidental(1, new Accidental("b")).addAccidental(2, new Accidental("#")).addDotToAll(),
];

Formatter.FormatAndDraw(context, stave, notes);
```

![](http://imgur.com/3wVLRxx.png)

Notice that in the above example, even though we set the note names and durations correctly, we explicitly request the rendering of accidentals and dots.

This is by design and allows us to decouple rendering logic and notational semantics. For example, you would not want to render the `#` accidental on `F#` when the key signature already includes it (e.g. key of `G`).

Also notice that we `FormatAndDraw`, which is a handy helper function that takes care of all the plumbing related to displaying a sequence of notes.

Let's add a few more modifiers and see how they position themselves. [See this example.](https://jsfiddle.net/6fovsLy8/)

```javascript
const notes = [
    new StaveNote({ keys: ["g/4", "b/4", "cb/5", "e/5", "g#/5", "b/5"], duration: "h" })
        .addModifier(new Accidental("bb"), 0)
        .addModifier(new Accidental("b"), 1)
        .addModifier(new Accidental("#"), 2)
        .addModifier(new Accidental("n"), 3)
        .addModifier(new Accidental("b"), 4)
        .addModifier(new Accidental("##"), 5),
    new StaveNote({ keys: ["c/4"], duration: "h" }),
];

// Helper function to justify and draw a 4/4 voice
Formatter.FormatAndDraw(context, stave, notes);
```

![](http://imgur.com/6cjs3Rf.png)

Notice how VexFlow positions the accidentals such that they don't collide with each other?

# Interlude

We've covered a bit of ground here, and you're probably asking for lists of valid note names, accidentals, durations, etc. that you can use with the API.

Fortunately, there is a canonical location where this stuff is kept. [VexFlow Tables (vexflow/src/tables.js)](https://github.com/0xfe/vexflow/blob/master/src/tables.ts)

Take a look at some of the following tables:

-   `Flow.clefProperties.values` - List of valid clef names.
-   `Flow.keyProperties.note_values` - The list of valid note names.
-   `Flow.accidentalCodes.accidentals` - The list of valid accidental names.
-   `Flow.keySignatures.keySpecs` - The list of valid keys.
-   `Flow.durationToTicks` - The list of valid duration codes.
-   `Flow.articulationCodes.articulations` - List of articulation codes.
-   `Flow.ornamentCodes.ornaments` - List of ornament codes.





# Step 4: Beam Your Notes

VexFlow can beam your notes for you, but only if you ask it to. The `Beam` class, when passed a set of adjacent notes (in a shared voice), is responsible for rendering beams based on the durations of each note. See this example:

```javascript
const notes = [new StaveNote({ clef: "treble", keys: ["e##/5"], duration: "8d" }).addAccidental(0, new Accidental("##")).addDotToAll(), new StaveNote({ clef: "treble", keys: ["b/4"], duration: "16" }).addAccidental(0, new Accidental("b"))];

var notes2 = [
    /* another group of notes */
];
var notes3 = [
    /* another group of notes */
];
var notes4 = [
    /* another group of notes */
];

// Create a beam for each group of notes
beams = [new Beam(notes), new Beam(notes2), new Beam(notes3)];

// Render the notes followed by the beams
var all_notes = notes.concat(notes2).concat(notes3).concat(notes4);
Vex.Flow.Formatter.FormatAndDraw(context, stave, all_notes);
beams.forEach(function (b) {
    b.setContext(context).draw();
});
```

![](http://imgur.com/40H5CTT.png)

In [the above example](https://jsfiddle.net/fvqmq9rd/3/), we created four groups of notes and beamed each groups. The slope of the beams is calculated automatically as a function of the direction of the music. The number of beam lines for each group is dependent on the duration of the notes underneath.

For long scores, manually creating a `Beam` object for each group of notes can get tedious. Luckily, the `Beam` class provides a static method, `generateBeams()`, that allow us to automatically generate beams for our notes. It has two parameters, 1) the notes to beam and 2) a config object. The config object provides options to beam your notes in different ways, but let's start simple.

```javascript
var notes = [
    new StaveNote({ clef: "treble", keys: ["e##/5"], duration: "8d" }).addAccidental(0, new Accidental("##")).addDotToAll(),
    new StaveNote({ clef: "treble", keys: ["b/4"], duration: "16" }).addAccidental(0, new Accidental("b")),
    new StaveNote({ clef: "treble", keys: ["c/4"], duration: "8" }),
    new StaveNote({ clef: "treble", keys: ["d/4"], duration: "16" }),
    new StaveNote({ clef: "treble", keys: ["e/4"], duration: "16" }).addAccidental(0, new Accidental("b")),
    new StaveNote({ clef: "treble", keys: ["d/4"], duration: "16" }),
    new StaveNote({ clef: "treble", keys: ["e/4"], duration: "16" }).addAccidental(0, new Accidental("#")),
    new StaveNote({ clef: "treble", keys: ["g/4"], duration: "32" }),
    new StaveNote({ clef: "treble", keys: ["a/4"], duration: "32" }),
    new StaveNote({ clef: "treble", keys: ["g/4"], duration: "16" }),
    new StaveNote({ clef: "treble", keys: ["d/4"], duration: "q" }),
];

var beams = VF.Beam.generateBeams(notes);
Vex.Flow.Formatter.FormatAndDraw(context, stave, notes);
beams.forEach(function (b) {
    b.setContext(context).draw();
});
```

![](http://imgur.com/fCh5jJz.png)

Notice two things above ([run](https://jsfiddle.net/18whg1he/1/)):

-   Notes were automatically grouped.
-   The stem directions were automatically calculated.

`generateBeams()` will calculate an appropriate stem direction for the entire beam group, even if it was set to a different position earlier.

For more sophisticated beaming examples, take a look at the [Beams](https://github.com/0xfe/vexflow/wiki/Beams) and the [Automatic Beaming](https://github.com/0xfe/vexflow/wiki/Automatic-Beaming) wiki pages.



+++++
















# Step 5: Ties

To render a tie, create a `StaveTie` instance and pass it two `StaveNotes`. Since `StaveNote` elements can also be chords, you need to pass in the indices of the specific note heads you want to tie together. [See this example](https://jsfiddle.net/bLc07tzj/):

```javascript
const { Renderer, Formatter, Stave, StaveNote, Accidental, Beam, Dot, StaveTie } = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element named "boo".
const div = document.getElementById("output");
const renderer = new Renderer(div, Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(500, 500);
const context = renderer.getContext();

// Create a stave of width 400 at position 10, 40 on the canvas.
const stave = new Stave(10, 40, 400);

// Add a clef and time signature.
stave.addClef("treble").addTimeSignature("4/4");

// Connect it to the rendering context and draw!
stave.setContext(context).draw();

const notes = [
    dotted(
        new StaveNote({
            keys: ["e##/5"],
            duration: "8d",
        }).addModifier(new Accidental("##"))
    ),
    new StaveNote({
        keys: ["b/4"],
        duration: "16",
    }).addModifier(new Accidental("b")),
    new StaveNote({
        keys: ["c/4"],
        duration: "8",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "16",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "16",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "q",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "q",
    }),
];

const beams = Beam.generateBeams(notes);
Formatter.FormatAndDraw(context, stave, notes);
beams.forEach(function (b) {
    b.setContext(context).draw();
});

const ties = [
    new StaveTie({
        first_note: notes[4],
        last_note: notes[5],
        first_indices: [0],
        last_indices: [0],
    }),
    new StaveTie({
        first_note: notes[5],
        last_note: notes[6],
        first_indices: [0],
        last_indices: [0],
    }),
];

ties.forEach((t) => {
    t.setContext(context).draw();
});

// A helper function to add a dot to a note.
function dotted(note) {
    Dot.buildAndAttach([note]);
    return note;
}
```

And [here's what it looks like](https://jsfiddle.net/bLc07tzj/):

![](http://imgur.com/YUNpn9G.png)




# Step 6: Guitar Tablature

VexFlow can also render guitar tablature. The mechanics for displaying tabs are the same as those for standard notation, except that you use different classes for staves and notes.

[See this example](https://jsfiddle.net/fudezsmr/):

```javascript
const { Renderer, TabStave, TabNote, Bend, Vibrato, Formatter } = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element with id="output".
const div = document.getElementById("output");
const renderer = new Renderer(div, Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(500, 300);
const context = renderer.getContext();

// Create a tab stave of width 400 at position 10, 40 on the canvas.
const stave = new TabStave(10, 40, 400);
stave.addClef("tab").setContext(context).draw();

const notes = [
    // A single note
    new TabNote({
        positions: [{ str: 3, fret: 7 }],
        duration: "q",
    }),

    // A chord with the note on the 3rd string bent
    new TabNote({
        positions: [
            { str: 2, fret: 10 },
            { str: 3, fret: 9 },
        ],
        duration: "q",
    }).addModifier(new Bend("Full"), 1),

    // A single note with a harsh vibrato
    new TabNote({
        positions: [{ str: 2, fret: 5 }],
        duration: "h",
    }).addModifier(new Vibrato().setHarsh(true).setVibratoWidth(70), 0),
];

Formatter.FormatAndDraw(context, stave, notes);
```

![](https://imgur.com/sHVMhtc.png)

In [the example above](https://jsfiddle.net/fudezsmr/) instead of using `Stave` and `StaveNote`, we use `TabStave` and `TabNote`. We also added a `Bend` and a `Vibrato` modifier.

# Step 7: Barlines

The `Stave` APIs were designed such that you don't have more than one bar / measure per stave. The idea is that you render a new `Stave` for every bar, and either attach it by juxtaposing it to an existing stave or rendering it in a new row. [See this example](https://jsfiddle.net/zrx6k5ao/):

```javascript
// This approach to importing classes works in CJS contexts (i.e., a regular <script src="..."> tag).
const { Stave, StaveNote, Beam, Formatter, Renderer } = Vex;

// Create an SVG renderer and attach it to the DIV element with id="output".
const div = document.getElementById("output");
const renderer = new Renderer(div, Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(720, 130);
const context = renderer.getContext();

// Measure 1
const staveMeasure1 = new Stave(10, 0, 300);
staveMeasure1.addClef("treble").setContext(context).draw();

const notesMeasure1 = [new StaveNote({ keys: ["c/4"], duration: "q" }), new StaveNote({ keys: ["d/4"], duration: "q" }), new StaveNote({ keys: ["b/4"], duration: "qr" }), new StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "q" })];

// Helper function to justify and draw a 4/4 voice
Formatter.FormatAndDraw(context, staveMeasure1, notesMeasure1);

// Measure 2 - second measure is placed adjacent to first measure.
const staveMeasure2 = new Stave(staveMeasure1.width + staveMeasure1.x, 0, 400);

const notesMeasure2_part1 = [new StaveNote({ keys: ["c/4"], duration: "8" }), new StaveNote({ keys: ["d/4"], duration: "8" }), new StaveNote({ keys: ["b/4"], duration: "8" }), new StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "8" })];

const notesMeasure2_part2 = [new StaveNote({ keys: ["c/4"], duration: "8" }), new StaveNote({ keys: ["d/4"], duration: "8" }), new StaveNote({ keys: ["b/4"], duration: "8" }), new StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "8" })];

// Create the beams for 8th notes in second measure.
const beam1 = new Beam(notesMeasure2_part1);
const beam2 = new Beam(notesMeasure2_part2);

const notesMeasure2 = notesMeasure2_part1.concat(notesMeasure2_part2);

staveMeasure2.setContext(context).draw();
Formatter.FormatAndDraw(context, staveMeasure2, notesMeasure2);

// Render beams
beam1.setContext(context).draw();
beam2.setContext(context).draw();
```

![](https://i.imgur.com/rrh0wZS.png)
