Fix small bugs and improve typings for the 4.0.0 release.

## Testing
* When VexFlow 4.0.0 is ready to be moved to `releases/`
  - [ ] Add sub directories `releases/4.0.0`, `releases/3.0.9`, `releases/1.2.90` to organize different versions.
  - [ ] Modify `generate_png_images.js` lines ~31-43 to properly load VexFlow + tests. For versions <= 3.0.9, we need to require both vexflow-debug.js and vexflow-tests.js. For versions >= 4.0.0, we only need to require vexflow-tests.js.
  - [ ] Similarly, modify `flow.html` so that build versions >= 4.0.0 only load vexflow-tests.js. Versions <= 3.0.9 need both JS files (when using the `ver=` query parameter).


## DONE ✓
- [x] Migrate src/ and tests/ to TypeScript.