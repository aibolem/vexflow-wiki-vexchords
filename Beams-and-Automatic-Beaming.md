(In progress, unedited)
# Beams
In order to beam sets of notes together, VexFlow provides a `Beam` object. But before we can use it, we need to create some `StaveNotes`. 

*Note: These code samples are incomplete. We assume you understand how to set up the rendering context, build a `Stave` and draw VexFlow objects.*

```javascript
var note_data = [
  { keys: ["f/4"], duration: "8"},
  { keys: ["e/4"], duration: "8"},
  { keys: ["d/4"], duration: "8"},
  { keys: ["c/4"], duration: "16"},
  { keys: ["c/4"], duration: "16"},
  { keys: ["c/5"], duration: "8"},
  { keys: ["b/4"], duration: "8"},
  { keys: ["c/5"], duration: "8"},
  { keys: ["c/5"], duration: "32"},
  { keys: ["c/5"], duration: "32"},
  { keys: ["b/4"], duration: "32"},
  { keys: ["f/4"], duration: "32"}
];

function createNote(note_data) {
  return new Vex.Flow.StaveNote(note_data);
}

var formatter = new Vex.Flow.Formatter();
var notes = note_data.map(createNote);
var voice = new Vex.Flow.Voice(Vex.Flow.TIME4_4);

voice.addTickables(notes);
formatter.joinVoices([voice]).formatToStave([voice], stave);
voice.draw(ctx, stave);
```

When you render the notes, you should get the following:

![](http://i.imgur.com/dyYywtv.png)

So now lets say that you want to break the notes into two sets of beams. One beam across the first 5 notes, and another beam across the following 7. It's really as simple as passing the group of notes to into the creation of a `Beam` object.

```javascript
var group1 = notes.slice(0, 5);
var group2 = notes.slice(5, 12);

var beam1 = new Vex.Flow.Beam(group1);
var beam2 = new Vex.Flow.Beam(group2);

beam1.setContext(context).draw();
beam2.setContext(context).draw();

voice.draw(context, stave);
```

![](http://i.imgur.com/o83YUJh.png)

# Automatic Beaming

For long scores, manually creating a `Beam` object for each group of notes is very cumbersome. Luckily, the `Beam` module provides a static method that allow us to automatically generate beams for our notes. It's appropriately named `.generateBeams()`. It has two parameters, the `notes` to automatically beam and a `config` object. The `config` object provides many options to beam your notes in different ways, but let's start simple.

```javascript
var beams = Beam.generateBeams(notes);

beams.forEach(function(beam) {
  beam.setContext(context).draw();
});
```

![](http://i.imgur.com/lcQU7F3.png)

Notice two things:

1. Stem directions were changed
2. The default beam groups are per quarter note

`.generateBeams()` will calculate an appropriate stem direction for the entire beam group, even if it was set to a different position earlier. There are two alternatives for dealing with stem directions with beams.

### Force Stem Direction

You can force a stem direction for every note, by passing a `stem_direction` property to the `config` object.

```javascript
var beams = Beam.generateBeams(notes, {
  stem_direction: -1
});
```
![](http://i.imgur.com/mUdQqmH.png)

### Maintain Stem Directions 

*Important: Not in master yet. Pull request pending.*

By setting `maintain_stem_directions` to `true`, the stem directions for each note will not be altered. Take a look at the initial stem directions for the following notes:

![](http://i.imgur.com/TbBBIGo.png)

By generating the beams using `maintain_stem_directions`, the beams are further split up within the beat group where the stem direction changed.
```javascript
var beams = Beam.generateBeams(notes, {
  maintain_stem_directions: true
});
```
![](http://i.imgur.com/IvRf0c2.png)

### Beaming Rests

By default, rests break up beam groups. 

![](http://i.imgur.com/pR8W4nV.png)

By setting `beam_rests` to `true`, the beams will extend over rests.
```javascript
var beams = Beam.generateBeams(notes, {
  beam_rests: true
});
```
![](http://i.imgur.com/QDc37uG.png)

### Beam Middle Rests Only

You can also set the `beam_middle_only` to `true` so that beams only extend across rests if they are in between notes.

```javascript
var beams = Beam.generateBeams(notes, {
  beam_rests: true,
  beam_middle_only: true
});
```
![](http://i.imgur.com/3XogNvn.png)

### Stemlets

Additionally, you can generate beams that draw stemlets over rests.
```javascript
var beams = Vex.Flow.Beam.generateBeams(notes, {
  beam_rests: true,
  show_stemlets: true
});
```
![](http://i.imgur.com/11WSh9Z.png)
### Custom Beam Groups

You can pass in custom beam group sequences to the `groups` property of the `config` object. These beam groups are represented by an array of `Vex.Flow.Fractions`, where each `Fraction` represents a single beam group. The following example beams in groups of 3 8th notes.

```javascript
var beams = Beam.generateBeams(notes, {
  groups: [new Vex.Flow.Fraction(3, 8)]
});
```
![](http://i.imgur.com/2j09Adk.png)

The following example beams notes in sequences of 3 and then 5 8th notes
```javascript
var beams = Beam.generateBeams(notes, {
  groups: [
    new Vex.Flow.Fraction(3, 8),
    new Vex.Flow.Fraction(5, 8)
  ]
});
```
![](http://i.imgur.com/o4WzoFN.png)