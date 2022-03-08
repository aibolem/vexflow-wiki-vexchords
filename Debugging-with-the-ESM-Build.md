This guide demonstrates how to rapidly develop/modify/test features within the VexFlow library. It is targeted at developers who wish to edit VexFlow source code (to customize its capability beyond what is offered, or to submit a PR to the main repo).

The process below requires VexFlow 4 or newer (since earlier versions did not include an ESM build).

# Summary
1. Run `grunt test:browser:esm` from the `vexflow/` directory. This will open `http://127.0.0.1:8080/tests/flow.html?esm=true` and also compile the ESM build in watch mode.
1. Navigate to the test you want by using the "Module:" dropdown and/or the "Filter:" search box.
1. Modify VexFlow. When you save a source file, the ESM build will be recompiled.
1. Refresh your webpage and see the results.


*Note!* Your browser might serve up a cached version of the VexFlow library and test page when you refresh. If this happens, you can open the developer tools and disable caching while the dev tools are open.


# Detailed Example

Here is a process for quickly comparing a PR to the current head revision. This requires TWO clones of the vexflow repo (I'll call them **A** and **B** below).

In repo A, check out the master branch and run the following command:

```
grunt test:browser:esm
```

This compiles the ES modules build in watch mode. It also loads `flow.html` in a local web server so that you can use the compiled library that resides in `vexflow/build/esm/`.

The web server starts at port 8080 by default. To see the Bach demo page, navigate to: http://127.0.0.1:8080/tests/flow.html?esm=true&module=Bach%20Demo


In repo B, check out a recent PR. I use the [GitHub CLI](https://github.com/cli/cli) for this. You can [supply a PR URL or a PR number](https://cli.github.com/manual/gh_pr_checkout):

```
gh pr checkout https://github.com/0xfe/vexflow/pull/1339
```

In repo B, build the ESM version and open the `flow.html` test page:

```
grunt test:browser:esm
```

The second server usually starts at port 8081, since port 8080 is used to serve repo A. To see the same Bach demo under repo B, navigate to: http://127.0.0.1:8081/tests/flow.html?esm=true&module=Bach%20Demo


Now that you have two different versions in adjacent browser tabs, you can see the differences by quickly flipping between the two tabs.

## Iterate

Edit the VexFlow source in one of the repos, and wait a moment for the ESM watch to recompile. (It's usually pretty quick.)

Refresh the tab for the repo that you just modified.

The ESM build comprises unminimized JS files, to make debugging easier. You can open your browser's developer tools and set a breakpoint in any compiled ESM file, and then refresh the page.
