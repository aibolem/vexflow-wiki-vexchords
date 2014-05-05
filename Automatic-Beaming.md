(In progress, unedited)

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