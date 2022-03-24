# Features

VexFlow 4 (March 2022) is the first major release since April 2020. It is the result of over 1600 commits by 19 contributors, and comes with the following improvements:

## TypeScript

VexFlow 4 is written in TypeScript. The effort to rewrite VexFlow in TypeScript was led by [Rodrigo Vilar](https://github.com/rvilarl) and [Ron Yeh](https://github.com/ronyeh). You can integrate the source directly into your TypeScript projects, or you can import VexFlow through `npm install vexflow`.

## Common JS + ES Modules

VexFlow 4 supports both CJS and ESM projects. The compiled library targets ES6.

Common JS projects include web sites that use regular `<script src="...">` tags, and Node JS projects that use `require(...)`.

ES module projects include web sites that use `<script type="module" src="...">` tags, and Node JS projects that use the `import` keyword or `import()` function.

## More Features
* Automatic layout of notes was improved, thanks to @aarondavidnewman and others.
* Handling of music and text fonts was improved by @ronyeh and @rvilarl.
* The process for building and testing VexFlow was improved by @h-sug1no and @ronyeh.
* Performance & rendering improvements by @tommadams.

***


# Quick Start

To include a score into a static web page, add a script tag pointing to the `vexflow.js` into your HTML source. You can use a CDN that serves NPM packages, such as jsdelivr or unpkg:

```
<script src="https://cdn.jsdelivr.net/npm/vexflow@4.0.1-beta.2/build/cjs/vexflow.js"></script>
```

If you use NPM to install packages into your project, you can include vexflow as follows:

```
npm install vexflow
```

In your JS file:

```
import { Vex } from "vexflow"; // Adds about 800 KiB to your project.
```

# The Fun Details!

If you'd like to explore the source code, you can clone the repository and build with `grunt`:

```
git clone git@github.com:0xfe/vexflow.git .
npm install
grunt
```

## build/ folder

After compiling the source, take a look at the `build/` folder. For example: https://github.com/0xfe/vexflow/tree/909286eb93b6f8c58ca8b6f766e12fc1ccf3602d

```
build/
    esm/
    cjs/
    types/
```

The `cjs/` folder includes pre-bundled VexFlow libraries (and source maps) for use in your Common JS projects. See the CJS section below for a description of each file.

The `esm/` folder includes the compiled ES module files, which are essentially our TypeScript source files with all the typing information removed. Unlike with the CJS version, the ESM files are individual unminified JS files. Your project bundler will include the modules you import and pack it into your final production app bundle.

The `types/` folder includes \*.d.ts files, which can help during development (e.g., autocomplete and better compiler errors).

## CJS Files

Let's take a look at the files in the `cjs/` folder.

The \*.js.map are source map files, which provide your browser's developer tools extra information during debugging.

The main VexFlow library is:

```
vexflow.js
```

You can include `vexflow.js` in your production environment, and point to it with a regular `<script>` tag. It includes three music engraving fonts.

During debugging, you can use:

```
vexflow-debug.js
vexflow-debug-with-tests.js   <<< This one includes the unit tests.
```

What if you only care about one of the music engraving fonts? Instead of using `vexflow.js`, you can choose one of the following smaller libraries. Each one includes only one music font:

```
vexflow-bravura.js
vexflow-gonville.js
vexflow-petaluma.js
```

If you want the smallest initial download, while needing the flexibility to load all three music fonts on the fly, you'll need the following five files. `vexflow-core.js` is the main library without fonts. It will load one or more of the font files when you call `Vex.Flow.setMusicFont(...)` in your app.

```
vexflow-core.js
vexflow-font-bravura.js
vexflow-font-custom.js
vexflow-font-gonville.js
vexflow-font-petaluma.js
```

# Release Notes

VexFlow 4 was released on March 24, 2022.

It was the first major release since version 3.0.9, and included [1669 commits from April 2020 to March 2022](https://github.com/0xfe/vexflow/compare/00ec15c67ff333ea49f4d3defbd9e22374c03684...cb8a4ffe04863c63b2b7711c6f7d1872a619bc70)!

VexFlow 4 was brought to you by:

> **Rodrigo Vilar**, **Ron B. Yeh**, **Aaron David Newman**, **Mohit Muthanna Cheppudira**
> 
> @h-sug1no, Tom Madams, @wassertim, Michael Scott Cuthbert, Gregory Ristow
> 
> @sschmidTU, @cmloegcmluin, @sschmid, @cmigliorini, @Andrew13648
> 
> @aleen42, @RyoSusami, @jeroenlammerts, @eliot-akira, @deemaagog 

To see the list of commits, check out the repository and run one of the following git commands:

```
git log --pretty=tformat:"%H    %an    %s"  00ec15c67ff333ea49f4d3defbd9e22374c03684..46af63bb5eb52c66d3a30d978b3a08d04eecf5c6


git rev-list --ancestry-path 00ec15c67ff333ea49f4d3defbd9e22374c03684..46af63bb5eb52c66d3a30d978b3a08d04eecf5c6
```

To review the details of a specific commit on GitHub, prepend `https://github.com/0xfe/vexflow/commit/` to any commit ID. For example: [`https://github.com/0xfe/vexflow/commit/151e452ff569958469ccd73f32218914cd0f823c`](https://github.com/0xfe/vexflow/commit/151e452ff569958469ccd73f32218914cd0f823c).

To see a list of commits preceding a particular commit, prepend `https://github.com/0xfe/vexflow/commits/` to any commit ID. For example: [`https://github.com/0xfe/vexflow/commits/151e452ff569958469ccd73f32218914cd0f823c`](https://github.com/0xfe/vexflow/commits/151e452ff569958469ccd73f32218914cd0f823c).