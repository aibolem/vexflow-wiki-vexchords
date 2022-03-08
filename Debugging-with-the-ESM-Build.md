This guide demonstrates how to rapidly develop/modify/test features within the VexFlow library. It is targeted at developers who wish to edit VexFlow source code (to customize its capability beyond what is offered, or to submit a PR to the main repo).

The process below requires VexFlow 4 or newer (since earlier versions did not include an ESM build).

Short Summary
1. Run `grunt test:browser:esm` from the `vexflow/` directory. This will open `http://127.0.0.1:8080/tests/flow.html?esm=true` and also compile the ESM build in watch mode.
1. Navigate to the test you want by using the "Module:" dropdown and/or the "Filter:" search box.
1. Modify VexFlow. When you save a source file, the ESM build will be recompiled.
1. Refresh your webpage and see the results.


*Note!* Your browser might serve up a cached version of the VexFlow library and test page when you refresh. If this happens, you can open the developer tools and disable caching while the dev tools are open.