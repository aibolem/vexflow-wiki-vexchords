# Upcoming Release

- `Accidental.ApplyAccidentals()` no longer breaks on `Notes` that ignore ticks (ie: `TimeSigNote`)
- `Accidental.applyAccidentals()` now applies accidentals to `GraceNotes`
- Fix a `BoundingBox#mergeWith` case when one box contains another
- Fix blurry canvas rendering on retina screens
- Rebuild noteheads after `StaveNote#setKeyLine` is called
- Ensure `StaveNote.extraLeftPx` and `StaveNote.extraRightPx` get recalculated in `StaveNote#reset`
- Lots of elements have been added to the `Factory`
  * Not that the API is subject to change
- Refactored tests