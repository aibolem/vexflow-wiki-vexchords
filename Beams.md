In order to beam sets of notes together, VexFlow provides a `Beam` object. But before we can use it, we need to create some `StaveNotes`. 

*Note: These code samples are incomplete. We assume you understand [how to set up the rendering context, build a `Stave` and draw VexFlow objects](https://github.com/0xfe/vexflow/wiki/Understanding-Renderer-&-Context).*

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

![](https://i.imgur.com/dyYywtv.png)

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

![](https://i.imgur.com/o83YUJh.png)

Make the process of beaming easier by learning about [Automatic Beaming](https://github.com/0xfe/vexflow/wiki/Automatic-Beaming)

## Breaking the Secondary Beams

If you want to break the secondary beams, at a certain note, use the `.breakSecondaryAt(indices)` method. Where you pass in an array of `indices` for where to break the secondary beams. Here's an example, lets start with a couple beams:

![](https://i.imgur.com/LmRkCXe.png)

Now lets set the notes to break the beams at:

```javascript
beam1.breakSecondaryAt([1, 3]);
beam2.breakSecondaryAt([2]);
```

On draw, you should get the following breaks in the beams:
![](https://i.imgur.com/xfXsJfT.png)
