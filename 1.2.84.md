# Upcoming Release

- `Accidental.ApplyAccidentals()` no longer breaks on `Notes` that ignore ticks (ie: `TimeSigNote`)
- `Accidental.applyAccidentals()` now applies accidentals to `GraceNotes`
- Fix a `BoundingBox#mergeWith` case when one box contains another
- Fix blurry canvas rendering on retina screens
- Rebuild noteheads after `StaveNote#setKeyLine` is called
- Ensure `StaveNote.extraLeftPx` and `StaveNote.extraRightPx` get recalculated in `StaveNote#reset`
- `Factory` exposes a lot more elements -- **API is subject to change**
- `Factory` constructor `options.renderer.selector` renamed to `options.renderer.elementId` to more appropriately reflect the what the string represents
- Sori and koron microtonal accidentals have been added
- Tests have been refactored to use `Factory` and `EasyScore`
- The font transformation tool (`transform.html`) has been refactored, and generates a font by combining both the `Gonville` and `Microtonal` fonts.