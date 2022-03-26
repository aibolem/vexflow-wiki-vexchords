When using VexFlow's `SVGContext` to render, it is possible to access the individual DOM elements in the rendered SVG and animate (or style them) much as one would on any other DOM node. The basic principle is to (1) open a group object in the SVG Context, (2) draw any elements you want within that group, (3) close the group, and (4) apply your animations/styling to this object.

```javascript
const staveNoteGroup = svgContext.openGroup();
staveNote.draw();
svgContext.closeGroup();

// Now use staveNoteGroup to apply any animations/transitions you want:
staveNoteGroup.style.transform = "opacity 5s linear";
staveNoteGroup.style.opacity = "0";
```

Imagine that we wanted to create a sight-reading app, in which notes scrolled into view, and a user had to play them on a keyboard before they reached the left hand side of the staff:
![](https://cloud.githubusercontent.com/assets/3900962/23332303/54ac5a06-fb6f-11e6-9826-630a9a2540a9.gif)

[Click here to see the example that we will walk through below](https://jsfiddle.net/cdunz8Lw/).

First we set up the DIVs & rendering boilerplate:
```html
<div id="container">
  <div id="output"></div>
</div>
<div id="controls">
  <button id='add-note'>Add Note</button>
  <button id='right-answer'>Right Answer</button>
</div>
```

We'll use a few CSS classes to handle layout and animation. We have an outer `#container` div with `overflow: hidden`, and an inner div `#output` where VexFlow will do the rendering, that is wider than the outer div, so that our note can scroll into view. `.scroll` defines the CSS transition rules for notes. `.scrolling` will be applied when a note is meant to actually move. `.correct` and `.too-slow` will animate a note depending on how the user answers:

```css
#container {
  width: 450px;
  height: 120px;
  overflow: hidden;
  border: 1px solid deeppink;
  margin: 10px;
}

#container>div {
  width: 10000px;
  height: 120px;
  white-space: nowrap;
}

#controls {
  padding: 15px;
}

#controls>button {
  margin: 5px;
}

.scroll {
  transition: transform 5s linear, opacity 0.5s ease-out, fill 0.2s linear;
}

.scrolling {
  transform: translate(-400px, 0);
}

.correct {
  opacity: 0;
}

.too-slow {
  transform: translate(-400px, 2000px);
}
```

Now let's add some boilerplate to set up VexFlow rendering with an `SVGContext`:

```javascript
// Basic boilerplate for using VexFlow with the SVG rendering context:
const { Renderer, TickContext, Stave, StaveNote, Accidental } = Vex.Flow;

// Create an SVG renderer and attach it to the DIV element named "boo".
const div = document.getElementById("output");
const renderer = new Renderer(div, Renderer.Backends.SVG);

// Configure the rendering context.
renderer.resize(500, 300);
const context = renderer.getContext();
```

A `TickContext` is required to draw anything that is placed horizontally in relation to time/rhythm, including all kinds of notes (`StaveNote`, `TabNote`, etc...). When used in conjunction with a `Voice` object, this allows VexFlow to space notes in real music horizontally relative to the duration of the note, the space available, and while preserving alignment with other voices or parts in the score.

While this is one of the incredibly powerful features of VexFlow, we definitely do not want to use it here. Instead, we want to be able to increase or decrease the rate at which notes appear based on how our user is doing. So, we'll handle adding notes to a `TickContext` manually, and will not create & format a `Voice` as we normally would:

```javascript
const tickContext = new TickContext();
```


Now let's create & draw a treble clef stave:
```javascript
// Create a stave of width 10000 at position 10, 40 on the canvas.
const stave = new Stave(10, 10, 10000).addClef("treble");

// Connect it to the rendering context and draw!
stave.setContext(context).draw();
```

Now we're ready to start creating the notes we'll draw. We could create an elaborate random-note generator that tracks which notes and accidental symbols a user needs more practice on. But let's keep it simple and predefine seven notes to scroll:

```javascript
const durations = ["8", "4", "2", "1"];

const notes = [
    ["c", "#", "4"],
    ["e", "b", "5"],
    ["g", "", "5"],
    ["d", "b", "4"],
    ["b", "bb", "3"],
    ["a", "b", "4"],
    ["f", "b", "5"],
].map(([letter, accidental, octave]) => {
    const note = new StaveNote({
        clef: "treble",
        keys: [`${letter}${accidental}/${octave}`],
        duration: durations[Math.floor(Math.random() * durations.length)],
    });
    note.setContext(context).setStave(stave);

    // If a StaveNote has an accidental, we must render it manually.
    // This is so that you get full control over whether to render
    // an accidental depending on the musical context. Here, if we
    // have one, we want to render it. (Theoretically, we might
    // add logic to render a natural sign if we had the same letter
    // name previously with an accidental. Or, perhaps every twelfth
    // note or so we might render a natural sign randomly, just to be
    // sure our user who's learning to read accidentals learns
    // what the natural symbol means.)
    if (accidental) {
        note.addModifier(new Accidental(accidental));
    }
    tickContext.addTickable(note);
    return note;
});
```

Now we've got our `StaveNote`s created and ready to go. But, before we can draw them, we have to first ask the `TickContext` to assign everything an x value. We do this by calling `tickContext.preFormat()`, which assigns x-values and other formatting values to notes. It must be called after we've created the `StaveNote`s and added them to the tick context, and before we try drawing them. We'll also set the left most x-value for the tick context, in this case, 400px to the right of the clef, which is just out of view of our `#container` div.

```javascript
tickContext.preFormat().setX(400)
```

To keep track of what notes are visible, and what note should be played next, we'll make an array:
```javascript
const visibleNoteGroups[];
```

Now we're ready to draw notes & add them to the staff:
```javascript
// Add a note to the staff from the notes array (if there are any left).
document.getElementById("add-note").addEventListener("click", (e) => {
    note = notes.shift();
    if (!note) {
        console.log("DONE!");
        return;
    }
    const group = context.openGroup();
    visibleNoteGroups.push(group);
    note.draw();
    context.closeGroup();
    group.classList.add("scroll");

    // Force a DOM-refresh by asking for the group's bounding box. Why? Most
    // modern browsers are smart enough to realize that adding .scroll class
    // hasn't changed anything about the rendering, so they wait to apply it
    // at the next dom refresh, when they can apply any other changes at the
    // same time for optimization. However, if we allow that to happen,
    // then sometimes the note will immediately jump to its fully transformed
    // position -- because the transform will be applied before the class with
    // its transition rule.
    const box = group.getBoundingClientRect();
    group.classList.add("scrolling");

    // If a user doesn't answer in time, make the note fall below the staff.
    window.setTimeout(() => {
        const index = visibleNoteGroups.indexOf(group);
        if (index === -1) return;
        group.classList.add("too-slow");
        visibleNoteGroups.shift();
    }, 5000);
});
```

Finally we want to give the user a sense of reward if they play the note correctly:

```javascript
// If a user plays/identifies the note in time, send it up to note heaven.
document.getElementById("right-answer").addEventListener("click", (e) => {
    if (visibleNoteGroups.length === 0) return;
    group = visibleNoteGroups.shift();
    group.classList.add("correct");

    // Coding challenge! Try adding a sound effect here (see: Tone.js).

    // The note will be somewhere in the middle of its move to the left -- by
    // getting its computed style we find its x-position, freeze it there, and
    // then send it straight up to note heaven with no horizontal motion.
    const transformMatrix = window.getComputedStyle(group).transform;
    // transformMatrix will be something like 'matrix(1, 0, 0, 1, -118, 0)'
    // where, since we're only translating in x, the 4th property will be
    // the current x-translation. You can dive into the gory details of
    // CSS3 transform matrices (along with matrix multiplication) if you want
    // at http://www.useragentman.com/blog/2011/01/07/css3-matrix-transform-for-the-mathematically-challenged/
    const x = transformMatrix.split(",")[4].trim();
    // And, finally, we set the note's style.transform property to send it skyward.
    group.style.transform = `translate(${x}px, -800px)`;
});
```

You can see all of it in action on [this example](https://jsfiddle.net/cdunz8Lw/).