## Test

-   [ ] Modify `generate_png_images.js` lines ~31-43 to properly load VexFlow + tests. For versions <= 3.0.9, we need to require both vexflow-debug.js and vexflow-tests.js. For versions >= 4.0.0, we only need to require vexflow-debug-with-tests.js.
-   [ ] Run command line visual diffs against 3.0.9.
-   [ ] Run `flow.html` and visually inspect & compare against 3.0.9 to see if anything regressed.
-   [ ] @mscuthbert to npm install from `git+https://github.com/0xfe/vexflow.git` and test on his projects.

## Fix and Document

-   [ ] Classify/Triage Issues. Keep only the highest priority issues for this release. Push all other issues to a future release.
-   [ ] @ronyeh @rvilarl Update CHANGELOG for any breaking changes.

## Release

-   [ ] @0xfe @ronyeh to release to npm & GitHub

## DONE ✓

-   [x] @rvilarl @ronyeh Migrate src/ and tests/ to TypeScript.
-   [x] @tommadams PR to pass a RenderContext into Renderer. https://github.com/0xfe/vexflow/pull/1161
-   [x] @ronyeh released PetalumaScript.woff to unpkg under npm package `vexflow-fonts`.
-   [x] @ronyeh PR to Simplify / Consolidate `setFont()`. https://github.com/0xfe/vexflow/pull/1163
-   [x] Close issue [#1155](/0xfe/vexflow/issues/1155)
-   [x] Modify `flow.html` so that build versions >= 4.0.0 only load vexflow-debug-with-tests.js. Versions <= 3.0.9 need both JS files (when using the `ver=` query parameter).
