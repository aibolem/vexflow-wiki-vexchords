VexFlow is an engraving engine for music notation and can be used as a rendering backend to various kinds of web-based music tools, libraries, and applications. It written in TypeScript/JavaScript and works with both HTML5 Canvas and SVG.

This tutorial expects you to have JavaScript programming experience and a basic understanding of music notation terminology.

# Step 1: The Basics [ [run](https://jsfiddle.net/cwnsrep9/) ]

Let's start with a quick example. Below, we have an HTML DIV element with the following code:

```html
<div id="output"></div>
```

Add [some boilerplate](https://github.com/0xfe/vexflow/wiki/Understanding-Renderer-&-Context) to create and size an SVG and get a drawing `context`:

```javascript
const { Renderer, Stave } = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element named "boo".
const div = document.getElementById("output");
const renderer = new Renderer(div, Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(500, 500);
const context = renderer.getContext();
```

Let's draw an empty stave on this SVG, and set the clef and time signature.

```javascript
// Create a stave of width 400 at position 10, 40 on the canvas.
const stave = new Stave(10, 40, 400);

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

# Step 2: Add Notes [ [run](https://jsfiddle.net/c36p8eo2/) ]

A `StaveNote` is a group of note heads representing a chord. It can consist of one or more notes with or without a stem and flag.

A sequence of notes is represented by a `Voice`.

Finally, you have the `Formatter`, which takes an array of voices and aligns, justifies, and renders the voices based on configurable rules, so that all the voices in the group look pretty on the stave(s).

In the code below we create a voice with two notes and a chord and render it on the stave.

```javascript
// Create the notes
const notes = [
    // A quarter-note C.
    new StaveNote({ keys: ["c/4"], duration: "q" }),

    // A quarter-note D.
    new StaveNote({ keys: ["d/4"], duration: "q" }),

    // A quarter-note rest. Note that the key (b/4) specifies the vertical
    // position of the rest.
    new StaveNote({ keys: ["b/4"], duration: "qr" }),

    // A C-Major chord.
    new StaveNote({ keys: ["c/4", "e/4", "g/4"], duration: "q" }),
];

// Create a voice in 4/4 and add above notes
const voice = new Voice({ num_beats: 4, beat_value: 4 });
voice.addTickables(notes);

// Format and justify the notes to 400 pixels.
new Formatter().joinVoices([voice]).format([voice], 350);

// Render voice
voice.draw(context, stave);
```

![](https://i.imgur.com/NT62Q7g.png)

Notice how the notes are justified evenly on the stave based on the duration of each note? This is the formatter in action - keeping voices aligned while balancing the spacing between the notes.

Let's add a second voice with a single whole note to this tune. [See this example:](https://jsfiddle.net/awe4vdms/)

```javascript
const notes = [
    new StaveNote({
        keys: ["c/5"],
        duration: "q",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "q",
    }),
    new StaveNote({
        keys: ["b/4"],
        duration: "qr",
    }),
    new StaveNote({
        keys: ["c/4", "e/4", "g/4"],
        duration: "q",
    }),
];

const notes2 = [
    new StaveNote({
        keys: ["c/4"],
        duration: "w",
    }),
];

// Create a voice in 4/4 and add above notes
const voices = [
    new Voice({
        num_beats: 4,
        beat_value: 4,
    }).addTickables(notes),
    new Voice({
        num_beats: 4,
        beat_value: 4,
    }).addTickables(notes2),
];

// Format and justify the notes to 400 pixels.
new Formatter().joinVoices(voices).format(voices, 350);

// Render voices.
voices.forEach(function (v) {
    v.draw(context, stave);
});
```

![](https://imgur.com/sk1RC26.png)

# Step 3: Modifiers [ [run](https://jsfiddle.net/4rt75dja/) ]

A modifier is an element that is attached to a note. Modifiers typically inherit from the `Modifier` base class. VexFlow supports modifiers like `Accidental`, `Vibrato`, `Annotation`, and more.

Modifiers are self-positioning – they juxtapose themselves alongside other modifiers and notes based on standard music notation rules.

Let's add some accidentals and dots. [See this example:](https://jsfiddle.net/4rt75dja/)

```javascript
const notes = [
    dotted(
        new StaveNote({
            keys: ["e##/5"],
            duration: "8d",
        }).addModifier(new Accidental("##"))
    ),

    new StaveNote({
        keys: ["eb/5"],
        duration: "16",
    }).addModifier(new Accidental("b")),

    dotted(
        new StaveNote({
            keys: ["eb/4", "d/5"],
            duration: "h",
        }),
        0 /* add dot to note at index==0 */
    ),

    dotted(
        new StaveNote({
            keys: ["c/5", "eb/5", "g#/5"],
            duration: "q",
        })
            .addModifier(new Accidental("b"), 1)
            .addModifier(new Accidental("#"), 2)
    ),
];

Formatter.FormatAndDraw(context, stave, notes);

function dotted(staveNote, noteIndex = -1) {
    if (noteIndex < 0) {
        Dot.buildAndAttach([staveNote], {
            all: true,
        });
    } else {
        Dot.buildAndAttach([staveNote], {
            index: noteIndex,
        });
    }
    return staveNote;
}
```

![](https://imgur.com/3wVLRxx.png)

Notice that in the above example, even though we set the note names and durations correctly, we explicitly request the rendering of accidentals and dots.

This allows us to decouple rendering logic and notational semantics. For example, you would not want to render the `#` accidental on `F#` when the key signature already includes it (e.g. key of `G`).

Also notice that we use `Formatter.FormatAndDraw(...)`, which is a helper function that takes care of all the plumbing related to displaying a sequence of notes.

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

// Helper function to justify and draw a 4/4 voice.
Formatter.FormatAndDraw(context, stave, notes);
```

![](https://imgur.com/6cjs3Rf.png)

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

# Step 4: Beam Your Notes [ [run](https://jsfiddle.net/47Ld0a28/) ]

VexFlow can beam your notes for you, but only if you ask it to. The `Beam` class, when passed a set of adjacent notes (in a shared voice), is responsible for rendering beams based on the durations of each note. [See this example](https://jsfiddle.net/47Ld0a28/):

```javascript
const { Renderer, Stave, StaveNote, Accidental, Beam, Formatter, Dot } = Vex.Flow;

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

const notes1 = [
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
];

const notes2 = [
    new StaveNote({
        keys: ["c/4"],
        duration: "8",
    }),
    new StaveNote({
        keys: ["d/4"],
        duration: "16",
    }),
    new StaveNote({
        keys: ["e/4"],
        duration: "16",
    }).addModifier(new Accidental("b")),
];

const notes3 = [
    new StaveNote({
        keys: ["d/4"],
        duration: "16",
    }),
    new StaveNote({
        keys: ["e/4"],
        duration: "16",
    }).addModifier(new Accidental("#")),
    new StaveNote({
        keys: ["g/4"],
        duration: "32",
    }),
    new StaveNote({
        keys: ["a/4"],
        duration: "32",
    }),
    new StaveNote({
        keys: ["g/4"],
        duration: "16",
    }),
];

const notes4 = [
    new StaveNote({
        keys: ["d/4"],
        duration: "q",
    }),
];

const allNotes = notes1.concat(notes2).concat(notes3).concat(notes4);

// Create the beams for the first three groups.
// This hides the normal stems and flags.
const beams = [new Beam(notes1), new Beam(notes2), new Beam(notes3)];

Formatter.FormatAndDraw(context, stave, allNotes);

// Draw the beams and stems.
beams.forEach((b) => {
    b.setContext(context).draw();
});

// Helper function.
function dotted(staveNote) {
    Dot.buildAndAttach([staveNote]);
    return staveNote;
}
```

![](https://imgur.com/40H5CTT.png)

In [the above example](https://jsfiddle.net/47Ld0a28/), we created beams for the first three groups of notes. The slope of the beams is calculated automatically as a function of the direction of the music. The number of beam lines for each group depends on the duration of the notes underneath.

For long scores, manually creating a `Beam` object for each group of notes can get tedious. Luckily, the `Beam` class provides a static method, [`generateBeams()`](https://github.com/0xfe/vexflow/blob/46af63bb5eb52c66d3a30d978b3a08d04eecf5c6/src/beam.ts#L185), that allow us to automatically generate beams for our notes. It takes two parameters, 1) the notes to beam and 2) a config object. The config object provides options to beam your notes in different ways, but let's start with [a basic example](https://jsfiddle.net/jaq5upb2/):

```javascript
const { Renderer, Stave, Accidental, StaveNote, Beam, Formatter, Dot } = Vex.Flow;

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
    dotted(new StaveNote({ keys: ["e##/5"], duration: "8d" }).addModifier(new Accidental("##"))),
    new StaveNote({ keys: ["b/4"], duration: "16" }).addModifier(new Accidental("b")),
    new StaveNote({ keys: ["c/4"], duration: "8" }),
    new StaveNote({ keys: ["d/4"], duration: "16" }),
    new StaveNote({ keys: ["e/4"], duration: "16" }).addModifier(new Accidental("b")),
    new StaveNote({ keys: ["d/4"], duration: "16" }),
    new StaveNote({ keys: ["e/4"], duration: "16" }).addModifier(new Accidental("#")),
    new StaveNote({ keys: ["g/4"], duration: "32" }),
    new StaveNote({ keys: ["a/4"], duration: "32" }),
    new StaveNote({ keys: ["g/4"], duration: "16" }),
    new StaveNote({ keys: ["d/4"], duration: "q" }),
];

const beams = Beam.generateBeams(notes);
Formatter.FormatAndDraw(context, stave, notes);
beams.forEach((b) => {
    b.setContext(context).draw();
});

// A helper function to add a dot to a note.
function dotted(note) {
    Dot.buildAndAttach([note]);
    return note;
}
```

![](https://imgur.com/fCh5jJz.png)

Notice two things [in the above example](https://jsfiddle.net/jaq5upb2/):

-   Notes were automatically grouped.
-   The stem directions were automatically calculated.

`generateBeams()` will calculate an appropriate stem direction for the entire beam group.

For more sophisticated beaming examples, take a look at the [Beams](https://github.com/0xfe/vexflow/wiki/Beams) and the [Automatic Beaming](https://github.com/0xfe/vexflow/wiki/Automatic-Beaming) wiki pages.

# Step 5: Ties [ [run](https://jsfiddle.net/bLc07tzj/) ]

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

![](https://imgur.com/YUNpn9G.png)

# Step 6: Guitar Tablature [ [run](https://jsfiddle.net/fudezsmr/) ]

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

# Step 7: Barlines [ [run](https://jsfiddle.net/zrx6k5ao/) ]

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
