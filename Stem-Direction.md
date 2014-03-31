There are a few ways to set stem direction in VexFlow.

* To auto-format the stem (determines direction based on staff line), pass an `auto_stem` property on `StaveNote` creation:

*It's important to note, that you must correctly pass in the `clef` property, otherwise auto-stemming will not behave accurately*
```javascript
var note = new Vex.Flow.StaveNote({
    clef: 'bass',
    keys: ['f/3'],
    duration: '4',
    auto_stem: true
});
```
* To set the direction yourself, pass a `stem_direction` property on creation
```javascript
var note = new Vex.Flow.StaveNote({
    keys: ['c/5'],
    duration: '4',
    stem_direction: 1 // 1 is up -1 is down
});
```

* You can also get/set the stem direction of a note after it's been created:

```javascript
var down = -1;
note.setStemDirection(down)
note.getStemDirection() // returns -1
```