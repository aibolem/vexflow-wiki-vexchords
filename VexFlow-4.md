VexFlow 4 comprises [over 1600 commits from April 2020 to February 2022](https://github.com/0xfe/vexflow/compare/00ec15c67ff333ea49f4d3defbd9e22374c03684...4403e315277a73c072d74677abdae6fd398164f4)!


> [Apr 21 2020 / Commit 00ec15c67ff333ea49f4d3defbd9e22374c03684](https://github.com/0xfe/vexflow/commit/00ec15c67ff333ea49f4d3defbd9e22374c03684)
>
> ... 1611 commits ...
>
> [Feb 28, 2022 / Commit 4403e315277a73c072d74677abdae6fd398164f4](https://github.com/0xfe/vexflow/commit/4403e315277a73c072d74677abdae6fd398164f4)

See the [list of commits below](#full-list-of-commits).

# Main Features

## TypeScript

VexFlow 4 was converted to TypeScript, in an effort led by [Rodrigo Vilar](https://github.com/rvilarl) and [Ron Yeh](https://github.com/ronyeh). You can integrate the VexFlow source directly into your TypeScript projects, or you can import VexFlow through `npm install vexflow`.

## Common JS + ES Modules

VexFlow 4 supports both CJS and ESM projects. The compiled library targets ES6.

Common JS projects include web sites that use regular `<script src="...">` tags, and Node JS projects that use `require(...)`.

ES module projects include web sites that use `<script type="module" src="...">` tags, and Node JS projects that use the `import` keyword or `import()` function.


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

# Full List of Commits

Ordered from newest to oldest:


[4403e315277a73c072d74677abdae6fd398164f4](https://github.com/0xfe/vexflow/commit/4403e315277a73c072d74677abdae6fd398164f4) Merge pull request #1334 from ronyeh/release-script

[2c398e0e16f41c558885a03c53590f514edfd433](https://github.com/0xfe/vexflow/commit/2c398e0e16f41c558885a03c53590f514edfd433) Do not exit the program when calling TypeScript.compile(...). Instead, return true if the compilation was successful. Only expose the compile(...) function.

[dbd5de2bddd5cfaea762851a1b308a6a0d88976a](https://github.com/0xfe/vexflow/commit/dbd5de2bddd5cfaea762851a1b308a6a0d88976a) Call patch-package only when necessary.

[ee5bff01ff40b413acaf6f9fe8e9f9880407f599](https://github.com/0xfe/vexflow/commit/ee5bff01ff40b413acaf6f9fe8e9f9880407f599) Run typescript compiler programmatically. (Do not rely on global 'tsc'.)

[27583efa792d6b80fd8acc853ffc6efd0133597b](https://github.com/0xfe/vexflow/commit/27583efa792d6b80fd8acc853ffc6efd0133597b) Merge pull request #1333 from rvilarl/fix/easyscoretest

[62b007350374a12fde302b3ce3ce791ac60d8a3e](https://github.com/0xfe/vexflow/commit/62b007350374a12fde302b3ce3ce791ac60d8a3e) Remove build/ after releasing version 4.0.1-beta.2 to npm and GitHub.

[909286eb93b6f8c58ca8b6f766e12fc1ccf3602d](https://github.com/0xfe/vexflow/commit/909286eb93b6f8c58ca8b6f766e12fc1ccf3602d) Release VexFlow 4.0.1-beta.2

[a47aaac58a68297bda88e45b25695879d92ed8ef](https://github.com/0xfe/vexflow/commit/a47aaac58a68297bda88e45b25695879d92ed8ef) render notes in keys(...)

[567ba80618390639c170a60de47ab4d1f2eabbff](https://github.com/0xfe/vexflow/commit/567ba80618390639c170a60de47ab4d1f2eabbff) Merge pull request #1330 from rvilarl/fix/1329

[79e1ceb10b41aeb2972be55c038711dfff840180](https://github.com/0xfe/vexflow/commit/79e1ceb10b41aeb2972be55c038711dfff840180) Merge pull request #1332 from rvilarl/fix/formatterTests

[042d4d7b4e3e07f58439f8478e4e2e5ca4d9263d](https://github.com/0xfe/vexflow/commit/042d4d7b4e3e07f58439f8478e4e2e5ca4d9263d) keep num_beats constant in rightJustify

[1af7ba445c2d9d82918d08e5b51c17cff684886a](https://github.com/0xfe/vexflow/commit/1af7ba445c2d9d82918d08e5b51c17cff684886a) fix stringsDownBow glyph code

[564ac70500f6f601593e1dc6fdbd3d533cb6de05](https://github.com/0xfe/vexflow/commit/564ac70500f6f601593e1dc6fdbd3d533cb6de05) Merge pull request #1328 from AaronDavidNewman/fix-#1295

[7f379f8356ebfa1776d69b7fd8a97e9bb8423fb8](https://github.com/0xfe/vexflow/commit/7f379f8356ebfa1776d69b7fd8a97e9bb8423fb8) Remove build/ after releasing version 4.0.1-beta.1 to npm and GitHub.

[3bd0490b09ad489522c87d1a0a9c498f5bef5ce3](https://github.com/0xfe/vexflow/commit/3bd0490b09ad489522c87d1a0a9c498f5bef5ce3) Release VexFlow 4.0.1-beta.1

[ae783aca83e30a36759a9a134a1abfc9302c3b77](https://github.com/0xfe/vexflow/commit/ae783aca83e30a36759a9a134a1abfc9302c3b77) Fix grunt build:esm -- missing src directory.

[91a6714f837c6da5e0cced5d63ce695aaeccd484](https://github.com/0xfe/vexflow/commit/91a6714f837c6da5e0cced5d63ce695aaeccd484) Merge pull request #1263 from rvilarl/fix/1257

[7ef3699730ef2cf349967504a591f00a2b786230](https://github.com/0xfe/vexflow/commit/7ef3699730ef2cf349967504a591f00a2b786230) Consider horizontal position of annotations in width calc.

[fe6add6a6e3e37dbcf895bad00fc0d4187015db3](https://github.com/0xfe/vexflow/commit/fe6add6a6e3e37dbcf895bad00fc0d4187015db3) Remove build/ after releasing version 4.0.1-beta.0 to npm and GitHub.

[0a12fec28e79c415b5b1d1e88bf080d7d48a144b](https://github.com/0xfe/vexflow/commit/0a12fec28e79c415b5b1d1e88bf080d7d48a144b) Release VexFlow 4.0.1-beta.0

[9fbdff60979ed561ff45bc4ab0b0a9dc18fde898](https://github.com/0xfe/vexflow/commit/9fbdff60979ed561ff45bc4ab0b0a9dc18fde898) Add a newline so that `grunt test:reference` produces more readable output.

[19f95ede75a479b3290479f7e0d8983290b51635](https://github.com/0xfe/vexflow/commit/19f95ede75a479b3290479f7e0d8983290b51635) UPdate test case

[4b8dd86798a018ac387eca21c31121b152dad77b](https://github.com/0xfe/vexflow/commit/4b8dd86798a018ac387eca21c31121b152dad77b) changes for code reveiw

[3ae47b47e53d77fdcc53bbc50d7b743ce5ab1a21](https://github.com/0xfe/vexflow/commit/3ae47b47e53d77fdcc53bbc50d7b743ce5ab1a21) fix #1295 by more accurately reporting articulation and annotation width

[5d4ea3cbecb4f55e4f47454f3712a3542582d170](https://github.com/0xfe/vexflow/commit/5d4ea3cbecb4f55e4f47454f3712a3542582d170) Merge pull request #1327 from sschmidTU/feat/svg-classes

[69fcdf6567d6208fd4bdc168fe0c76c00b677169](https://github.com/0xfe/vexflow/commit/69fcdf6567d6208fd4bdc168fe0c76c00b677169) revert dot y-shift

[18c07e61bdfb9b1487969233e3cd7a432fabd7c4](https://github.com/0xfe/vexflow/commit/18c07e61bdfb9b1487969233e3cd7a432fabd7c4) adjust dot y-shift

[32552cff733210f12fe7bfb60a0e696c80dc5f95](https://github.com/0xfe/vexflow/commit/32552cff733210f12fe7bfb60a0e696c80dc5f95) feat(SVG): Add SVG group for stems within beams

[e915eb5a0ce1bcba92311f349a8ee0bd38250ab0](https://github.com/0xfe/vexflow/commit/e915eb5a0ce1bcba92311f349a8ee0bd38250ab0) feat(SVG): Add SVG classes for StaveTie, Beam (OSMDPatch)

[ee06e72135ba9e743c4b0fd0f1b4950d9cd0a759](https://github.com/0xfe/vexflow/commit/ee06e72135ba9e743c4b0fd0f1b4950d9cd0a759) review comments

[3db05680636535429a33784bcf13f6fc77a01273](https://github.com/0xfe/vexflow/commit/3db05680636535429a33784bcf13f6fc77a01273) noteHeadsSimple test

[47d47711819042b8f15158703c854a09dc729a0e](https://github.com/0xfe/vexflow/commit/47d47711819042b8f15158703c854a09dc729a0e) refactor note.dots

[208159e2b596f695c632ed0a627167f77d632e2d](https://github.com/0xfe/vexflow/commit/208159e2b596f695c632ed0a627167f77d632e2d) share noteheads

[21aa91676eea92002478b1389caefb1e0f78b2c7](https://github.com/0xfe/vexflow/commit/21aa91676eea92002478b1389caefb1e0f78b2c7) Merge pull request #1323 from rvilarl/fix/1312

[1e8e61b00e4fe3f977dd066c9b5c2d0243ede425](https://github.com/0xfe/vexflow/commit/1e8e61b00e4fe3f977dd066c9b5c2d0243ede425) review comments

[f68af3aa4d1c38cc6a687a40bf97f44d6f54672b](https://github.com/0xfe/vexflow/commit/f68af3aa4d1c38cc6a687a40bf97f44d6f54672b) Merge pull request #1326 from rvilarl/fix/1313

[938e08561b1e97610160fb4fced0d964ddab2dc8](https://github.com/0xfe/vexflow/commit/938e08561b1e97610160fb4fced0d964ddab2dc8) Merge pull request #1324 from rvilarl/fix/1309

[65a1f65e90b079ed69971392821893ad9304cf88](https://github.com/0xfe/vexflow/commit/65a1f65e90b079ed69971392821893ad9304cf88) Merge pull request #1322 from ronyeh/dependency-graph

[d370611e9d17a8b72503b6ba44bb9439f38eae31](https://github.com/0xfe/vexflow/commit/d370611e9d17a8b72503b6ba44bb9439f38eae31) Merge pull request #1321 from rvilarl/fix/1314

[b85150aa9e7b088b38996b0b7769342fe41a262e](https://github.com/0xfe/vexflow/commit/b85150aa9e7b088b38996b0b7769342fe41a262e) Merge pull request #1320 from rvilarl/fix/1316

[fddad1b9a69598c688989fc20073ef15ec36289e](https://github.com/0xfe/vexflow/commit/fddad1b9a69598c688989fc20073ef15ec36289e) fix #1313: segno position

[9e82da24dcf30caf809caa57af363619cad8c311](https://github.com/0xfe/vexflow/commit/9e82da24dcf30caf809caa57af363619cad8c311) fix #1309: make sure that postFormat is called

[27cda03db19e146bcda41d2bb4a53fbd6af8bee2](https://github.com/0xfe/vexflow/commit/27cda03db19e146bcda41d2bb4a53fbd6af8bee2) fix #1312 stem extension calculation fixed

[d11a3f5ca2fcca5b8428d3dba96952a4e6fdc7ea](https://github.com/0xfe/vexflow/commit/d11a3f5ca2fcca5b8428d3dba96952a4e6fdc7ea) Dependency graphs.

[ba6cf89e6a08b8cd6e7f0ff493d79b7840058a44](https://github.com/0xfe/vexflow/commit/ba6cf89e6a08b8cd6e7f0ff493d79b7840058a44) remove duplicated line

[2c8b8e75d9e63e2660721e74dd2987969ea959bf](https://github.com/0xfe/vexflow/commit/2c8b8e75d9e63e2660721e74dd2987969ea959bf) consider shifted notes

[37d7285b56c0f18e4fb45b878d6d5b49d1521495](https://github.com/0xfe/vexflow/commit/37d7285b56c0f18e4fb45b878d6d5b49d1521495) Remove build/ after releasing version 4.0.1-alpha.2 to npm and GitHub.

[54883ae7678ea27ff34fd241a3acbf42e2418348](https://github.com/0xfe/vexflow/commit/54883ae7678ea27ff34fd241a3acbf42e2418348) Release VexFlow 4.0.1-alpha.2

[0df10df6d1fab3a99f5aa306341a31c6e686d659](https://github.com/0xfe/vexflow/commit/0df10df6d1fab3a99f5aa306341a31c6e686d659) Merge pull request #1319 from ronyeh/release-script

[36be50a4da258b52ae6c1712ff50033eccaeb81d](https://github.com/0xfe/vexflow/commit/36be50a4da258b52ae6c1712ff50033eccaeb81d) Fix "Argument list too long" error during cleanup in visual_regression.sh.

[624249532eda6d9de4a70f0fe26008c8ad810a6d](https://github.com/0xfe/vexflow/commit/624249532eda6d9de4a70f0fe26008c8ad810a6d) Formatting

[35e8f043c5e3f9445bcd300244bc268d07be3e7a](https://github.com/0xfe/vexflow/commit/35e8f043c5e3f9445bcd300244bc268d07be3e7a) Improve flow.html to allow specifying params in the fragment identifier. This allows us to run flow.html tests on unpkg.com.

[4aa3112d82fe097d7bef73ac962ca93ea5069a1f](https://github.com/0xfe/vexflow/commit/4aa3112d82fe097d7bef73ac962ca93ea5069a1f) Fix release script bug: missing execSync import.

[a23f63cc3f38503192cdf999f204839c000c7aab](https://github.com/0xfe/vexflow/commit/a23f63cc3f38503192cdf999f204839c000c7aab) Remove "postinstall" script from package.json to fix https://github.com/0xfe/vexflow/issues/1318 Update package-lock.json's "hasInstallScript" field.

[d467208327b0a50fa2d21df836379a87d308a163](https://github.com/0xfe/vexflow/commit/d467208327b0a50fa2d21df836379a87d308a163) Remove build/ after releasing version 4.0.1-alpha.1 to npm and GitHub.

[7c2825dc8c9d7c7d37c3372156f7d3be7ea5538a](https://github.com/0xfe/vexflow/commit/7c2825dc8c9d7c7d37c3372156f7d3be7ea5538a) Release VexFlow 4.0.1-alpha.1

[21f1282380bb40da01de6dbcde437119f52b860d](https://github.com/0xfe/vexflow/commit/21f1282380bb40da01de6dbcde437119f52b860d) Merge pull request #1298 from ronyeh/is-category

[fe237a38cc137e0f52127d0e45d7bd2a701e613c](https://github.com/0xfe/vexflow/commit/fe237a38cc137e0f52127d0e45d7bd2a701e613c) Merge pull request #1300 from ronyeh/parameter-order

[e45f69585161bb517503bc8832db9d16fdd2fc04](https://github.com/0xfe/vexflow/commit/e45f69585161bb517503bc8832db9d16fdd2fc04) Merge branch 'master' into is-category

[52860b808891301e4968b3e0c5265fa4153c417e](https://github.com/0xfe/vexflow/commit/52860b808891301e4968b3e0c5265fa4153c417e) Docs

[d59cff53ba19a0911862f9f199f3d309039ea9cc](https://github.com/0xfe/vexflow/commit/d59cff53ba19a0911862f9f199f3d309039ea9cc) Tickable.addModifier() has the same API as Note.addModifier() to avoid unnecessary casts.

[3f1bb519cba0356f8f9398caad7dd42fb14457f4](https://github.com/0xfe/vexflow/commit/3f1bb519cba0356f8f9398caad7dd42fb14457f4) API docs updated.

[c2392d78d71ccab426674c09caed7ebd6e1346ce](https://github.com/0xfe/vexflow/commit/c2392d78d71ccab426674c09caed7ebd6e1346ce) Merge branch 'master' into parameter-order

[08045814013ff4941e220df7df17863b162355e9](https://github.com/0xfe/vexflow/commit/08045814013ff4941e220df7df17863b162355e9) Merge pull request #1306 from rvilarl/typedoc

[68a55db12d72deac0cf854323f2b36817f5cbc4b](https://github.com/0xfe/vexflow/commit/68a55db12d72deac0cf854323f2b36817f5cbc4b) Merge pull request #1305 from rvilarl/prettier

[ef794afe9b77f172525d569607d43e70a205615f](https://github.com/0xfe/vexflow/commit/ef794afe9b77f172525d569607d43e70a205615f) API documentation update

[154e315a46a84f6ee75a789c9413b9e2bf14d346](https://github.com/0xfe/vexflow/commit/154e315a46a84f6ee75a789c9413b9e2bf14d346) prettier changes

[e98a902e3a07767948c447bbebd0c6fcb3ef42b7](https://github.com/0xfe/vexflow/commit/e98a902e3a07767948c447bbebd0c6fcb3ef42b7) Merge pull request #1304 from ronyeh/release-script

[af5facdb45acbb63e55a3226e5868b04ebeb5cb6](https://github.com/0xfe/vexflow/commit/af5facdb45acbb63e55a3226e5868b04ebeb5cb6) Merge pull request #1296 from AaronDavidNewman/411-stringno

[ba8326b56954fa98d7b1d58be786407f5eb74ced](https://github.com/0xfe/vexflow/commit/ba8326b56954fa98d7b1d58be786407f5eb74ced) Merge pull request #1280 from rvilarl/refactor/staveNoteFormat

[589712d01b5c7c8640cc19ff863590ae4013cfe7](https://github.com/0xfe/vexflow/commit/589712d01b5c7c8640cc19ff863590ae4013cfe7) review comments

[b25c7d5be970293f4112c4744bf5a62410e5860a](https://github.com/0xfe/vexflow/commit/b25c7d5be970293f4112c4744bf5a62410e5860a) fix formatting issues

[a87f6634e79d408b862a9de5e06da664cb233f72](https://github.com/0xfe/vexflow/commit/a87f6634e79d408b862a9de5e06da664cb233f72) fix dots shift with no previous modifier

[b62ed38eb84fd49632ee92117bce6f84810db25c](https://github.com/0xfe/vexflow/commit/b62ed38eb84fd49632ee92117bce6f84810db25c) simplify format

[faec59e1683b42baf6c8823ae06dbf465c6ea1dc](https://github.com/0xfe/vexflow/commit/faec59e1683b42baf6c8823ae06dbf465c6ea1dc) Add patch-package so we can fix parse-path@4.0.3. Remove the patch after the fix is merged. The issue is filed at https://github.com/IonicaBizau/parse-path/pull/32 The patch manager https://www.npmjs.com/package/patch-package

[65fd2a6f3d7703f81ab71f6b6dbda57c28ad5b64](https://github.com/0xfe/vexflow/commit/65fd2a6f3d7703f81ab71f6b6dbda57c28ad5b64) Gruntfile.js improvements to skip an unnecessary git commit during release.

[316c01775458b42597e5598b91f5749e94e465d0](https://github.com/0xfe/vexflow/commit/316c01775458b42597e5598b91f5749e94e465d0) Merge pull request #1303 from rvilarl/puppeteerOptions

[077452e5e77ba47822f235f18742fe2a8ff239bd](https://github.com/0xfe/vexflow/commit/077452e5e77ba47822f235f18742fe2a8ff239bd) adjust puppeteer options for linux

[675754e84c1206b8385fa70583454cb68c60e615](https://github.com/0xfe/vexflow/commit/675754e84c1206b8385fa70583454cb68c60e615) Remove build/ after releasing version 4.0.1-alpha.0

[0ff80f5db128ed80914ddd7ef0fde6312d115811](https://github.com/0xfe/vexflow/commit/0ff80f5db128ed80914ddd7ef0fde6312d115811) Release VexFlow 4.0.1-alpha.0

[dfbcd277d400afd5adb5370576115bc084b98adb](https://github.com/0xfe/vexflow/commit/dfbcd277d400afd5adb5370576115bc084b98adb) Add build/ for release version 4.0.1-alpha.0.

[935fecc1f37e4fd8ef8c3526c045e322fb744e56](https://github.com/0xfe/vexflow/commit/935fecc1f37e4fd8ef8c3526c045e322fb744e56) Skip GitHub collaborator check during release.

[b9062f21e422afcababd8d971daa29c2193e4d5f](https://github.com/0xfe/vexflow/commit/b9062f21e422afcababd8d971daa29c2193e4d5f) Fix parameter order.

[9045a653dc191fa97ce3a3c7343e44b9b9b6e308](https://github.com/0xfe/vexflow/commit/9045a653dc191fa97ce3a3c7343e44b9b9b6e308) Merge branch 'master' into parameter-order

[50e466b9be664645de099fc4605e341b3e2d2ac7](https://github.com/0xfe/vexflow/commit/50e466b9be664645de099fc4605e341b3e2d2ac7) Merge branch 'master' into is-category

[42baa681f6f688cd3dcaced8758a2d96b270e18b](https://github.com/0xfe/vexflow/commit/42baa681f6f688cd3dcaced8758a2d96b270e18b) Merge pull request #1287 from ronyeh/test

[5c9123d06bd7fa9a5ae86b22b2a673995aa10857](https://github.com/0xfe/vexflow/commit/5c9123d06bd7fa9a5ae86b22b2a673995aa10857) eslint auto fix.

[85970b0636440f5f20246f66cecfab29debb64f8](https://github.com/0xfe/vexflow/commit/85970b0636440f5f20246f66cecfab29debb64f8) Merge branch 'master' into test

[38cf203b20fdbb0fa3461faba891a9b14185e5a7](https://github.com/0xfe/vexflow/commit/38cf203b20fdbb0fa3461faba891a9b14185e5a7) Merge https://github.com/0xfe/vexflow into 411-stringno

[f47e9f80e2c629c548e3ed43a88156c1d6b90ba6](https://github.com/0xfe/vexflow/commit/f47e9f80e2c629c548e3ed43a88156c1d6b90ba6) Merge pull request #1302 from AaronDavidNewman/issue-1301

[f8b31cfcea41f71999983d261d6145d93d39ebf4](https://github.com/0xfe/vexflow/commit/f8b31cfcea41f71999983d261d6145d93d39ebf4) remove unused ref, duplicate test

[ab0c629a8830d8b2af05762aa3d3a903e59004e6](https://github.com/0xfe/vexflow/commit/ab0c629a8830d8b2af05762aa3d3a903e59004e6) changes for code review

[9e08f1f9b1aae114338e19e88dfe64122071e516](https://github.com/0xfe/vexflow/commit/9e08f1f9b1aae114338e19e88dfe64122071e516) Merge branch 'master' into is-category

[f88ca8309b3e9a424675936e0d7f3a335f2dfb8d](https://github.com/0xfe/vexflow/commit/f88ca8309b3e9a424675936e0d7f3a335f2dfb8d) Fix errors in legacy formatter test page.

[c78dca72439eb25d66fec602b83047b8697dd2fb](https://github.com/0xfe/vexflow/commit/c78dca72439eb25d66fec602b83047b8697dd2fb) Merge branch 'master' into parameter-order

[7c22d31048e57ea7d0010c8d6dceddc8d6d52131](https://github.com/0xfe/vexflow/commit/7c22d31048e57ea7d0010c8d6dceddc8d6d52131) Merge branch 'master' into test

[8fbe60ff5cf2782d1cd7b0df4827ffda77d6df78](https://github.com/0xfe/vexflow/commit/8fbe60ff5cf2782d1cd7b0df4827ffda77d6df78) Merge pull request #1299 from ronyeh/typedoc

[cc428fc0307c49c77231b42652ddebd256523bdf](https://github.com/0xfe/vexflow/commit/cc428fc0307c49c77231b42652ddebd256523bdf) Base bend height on bend text

[e9133007dbf889864af9db936c69215e578e5f07](https://github.com/0xfe/vexflow/commit/e9133007dbf889864af9db936c69215e578e5f07) fix bend/vibrato vertical placement

[27a587de119e5cf26fafb45f10450c1533462747](https://github.com/0xfe/vexflow/commit/27a587de119e5cf26fafb45f10450c1533462747) Change parameter order of Note.addModifier(...) and Tickable.addModifier(...). The modifier argument is now first, and the index is now second (defaults to 0).

[81174c55f79b3576e2da66b5cfed4b86f2b44340](https://github.com/0xfe/vexflow/commit/81174c55f79b3576e2da66b5cfed4b86f2b44340) Add typedoc.json. Remove the footer. Add to .gitignore

[39ef9b5b2e6b28b7dbe27cce8877bc66e1f79912](https://github.com/0xfe/vexflow/commit/39ef9b5b2e6b28b7dbe27cce8877bc66e1f79912) Fix typeguard test.

[d87705b4a161cc4676c1e8b40fcadb77da8785d1](https://github.com/0xfe/vexflow/commit/d87705b4a161cc4676c1e8b40fcadb77da8785d1) Add CATEGORY string to RenderContext. Break the Glyph => Tables circular dependency.

[5168ab84a334e56ad4e83efe1b971defa31051e9](https://github.com/0xfe/vexflow/commit/5168ab84a334e56ad4e83efe1b971defa31051e9) Throw a RuntimeError instead of instantiating a useless Factory.

[151e452ff569958469ccd73f32218914cd0f823c](https://github.com/0xfe/vexflow/commit/151e452ff569958469ccd73f32218914cd0f823c) Avoid instanceof keyword. Use isCategory() instead.

[f5c1a334d3f02ad2956767540f8e185167eda3b1](https://github.com/0xfe/vexflow/commit/f5c1a334d3f02ad2956767540f8e185167eda3b1) Delay the call to new Formatter() to improve our chances of avoiding circular issues at runtime.

[a9dc12bbdbd475d999d88080f6f41d8dd10b1d7e](https://github.com/0xfe/vexflow/commit/a9dc12bbdbd475d999d88080f6f41d8dd10b1d7e) Use the Category enum instead of hard coded strings.

[791b6205b8e8d45ae494db8c9f1898a79c40c90e](https://github.com/0xfe/vexflow/commit/791b6205b8e8d45ae494db8c9f1898a79c40c90e) isCategory() no longer uses instanceof. Instead, it uses strings from a const enum.

[a70c6d6d41b7e9cfbcb539c411d3ced60dc26f78](https://github.com/0xfe/vexflow/commit/a70c6d6d41b7e9cfbcb539c411d3ced60dc26f78) Add -f flag to force the removal of the build/ folder after the release.

[66244de9769f0893529c22c9dbe4fc42454edc34](https://github.com/0xfe/vexflow/commit/66244de9769f0893529c22c9dbe4fc42454edc34) grunt test:release:X.Y.Z Visual regression test between build/ and releases/X.Y.Z/

[cf87a624473438afae6a0e1ed10d4fa5f49c63a5](https://github.com/0xfe/vexflow/commit/cf87a624473438afae6a0e1ed10d4fa5f49c63a5) Improve Gruntfile.js docs and ESM testing.

[81f6ac06a2f721e7eefdee4911968afe2e094b46](https://github.com/0xfe/vexflow/commit/81f6ac06a2f721e7eefdee4911968afe2e094b46) Update release-it package. Set package.json version to 4.0.0.

[9c949e26b73ace5febdba311f3ffcf73e2b73b70](https://github.com/0xfe/vexflow/commit/9c949e26b73ace5febdba311f3ffcf73e2b73b70) Docs and eslint auto-fixes.

[089919ddaea34bde20e3e45e7b4cd82e0b35f3c9](https://github.com/0xfe/vexflow/commit/089919ddaea34bde20e3e45e7b4cd82e0b35f3c9) Show when release dry-run mode is on. Set the package.json version to beta. Show a warning if GITHUB_TOKEN is not provided.

[c3365ff1bbdc10c648034508deb7f66b3d7ab101](https://github.com/0xfe/vexflow/commit/c3365ff1bbdc10c648034508deb7f66b3d7ab101) Merge branch 'master' into test

[25742768159c2105e91e98808e89aa878c27c268](https://github.com/0xfe/vexflow/commit/25742768159c2105e91e98808e89aa878c27c268) Use webpack string-replace-loader to write out the version info for CJS builds. For the ESM build, write out the version.js build file directly.

[93c008d8151f788fd68f7037919218461cf55b13](https://github.com/0xfe/vexflow/commit/93c008d8151f788fd68f7037919218461cf55b13) minor tweaks to formatting

[c865e03ab09f7b52ebbc5e0767f475144b397872](https://github.com/0xfe/vexflow/commit/c865e03ab09f7b52ebbc5e0767f475144b397872) fix  lint complaints

[f1bdace1a4a9a2b709ea65f92189fafbd6531595](https://github.com/0xfe/vexflow/commit/f1bdace1a4a9a2b709ea65f92189fafbd6531595) Fix the rest of bug 411

[54966e3d29d255e6af8e776ddb9fa154da135eb5](https://github.com/0xfe/vexflow/commit/54966e3d29d255e6af8e776ddb9fa154da135eb5) Merge pull request #1290 from rvilarl/fix/openGroup

[7096fb18f34ec572ffe48b598007a34c1ead9205](https://github.com/0xfe/vexflow/commit/7096fb18f34ec572ffe48b598007a34c1ead9205) Merge pull request #1270 from AaronDavidNewman/pr-1265

[6ab954e61884ad4807d984d812e9a712079827c5](https://github.com/0xfe/vexflow/commit/6ab954e61884ad4807d984d812e9a712079827c5) Fix lint warning in annotation.ts

[acad4a03b0422cf8dcb34563ca0c551470d96e73](https://github.com/0xfe/vexflow/commit/acad4a03b0422cf8dcb34563ca0c551470d96e73) Move release-it config and tasks into the Gruntfile.js. Only generate src/version.ts during a release build.

[19ef952af7aff3617e41526552585fff0ae1ad33](https://github.com/0xfe/vexflow/commit/19ef952af7aff3617e41526552585fff0ae1ad33) Merge https://github.com/0xfe/vexflow into pr-1265

[68fa5901f1bd33077eecb50ebdcb85d292210ff6](https://github.com/0xfe/vexflow/commit/68fa5901f1bd33077eecb50ebdcb85d292210ff6) Default grunt task: run sub tasks with concurrently().

[8d73225c2fe0000dd0de69628f56a7de6c316f5d](https://github.com/0xfe/vexflow/commit/8d73225c2fe0000dd0de69628f56a7de6c316f5d) fix fill optional parameter

[ccc704db354d4f9b3c11706b6b05a85cb5a9d401](https://github.com/0xfe/vexflow/commit/ccc704db354d4f9b3c11706b6b05a85cb5a9d401) GITHUB_TOKEN is required to run the release script.

[4311b53c466b263b9d9191f1703c55da74cf0aaf](https://github.com/0xfe/vexflow/commit/4311b53c466b263b9d9191f1703c55da74cf0aaf) Improve release script with better commit message and more robust handling of arguments.

[3650f3bd980a422c8d5291440a5de099ac462a28](https://github.com/0xfe/vexflow/commit/3650f3bd980a422c8d5291440a5de099ac462a28) Bug fix for loading font modules.

[aefb5f5b39bf0920a20fdd788253e944fbf2176e](https://github.com/0xfe/vexflow/commit/aefb5f5b39bf0920a20fdd788253e944fbf2176e) Small fix.

[116f5052a929bf70c4f84993691b8bbe67178e8a](https://github.com/0xfe/vexflow/commit/116f5052a929bf70c4f84993691b8bbe67178e8a) Add a task to clean the eslint cache.

[43fffb7a82ecd4159587b18a292801e501b876fb](https://github.com/0xfe/vexflow/commit/43fffb7a82ecd4159587b18a292801e501b876fb) Formatting & Comments.

[1376c110f77158d229c1a10c230fa289297baa53](https://github.com/0xfe/vexflow/commit/1376c110f77158d229c1a10c230fa289297baa53) Merge branch 'master' into test

[69f0419a3dfd958c7c62f5f4592cf6f8ce82e1d9](https://github.com/0xfe/vexflow/commit/69f0419a3dfd958c7c62f5f4592cf6f8ce82e1d9) Improve, test, and clean up the Gruntfile.js. Full `grunt` build is now 42s (on MBP 2016). Remove unused NPM packages. Gruntfile comments.

[e20bfc1e5e3fbc500a0f607ce60f2c76323c0ed5](https://github.com/0xfe/vexflow/commit/e20bfc1e5e3fbc500a0f607ce60f2c76323c0ed5) Merge pull request #1293 from RyoSusami/master

[b06ab94879f24d66f608eef88e1167d834eff7fb](https://github.com/0xfe/vexflow/commit/b06ab94879f24d66f608eef88e1167d834eff7fb) matched addModifier parameter order of formatter test

[f90033f77bdf43ba03546811d85405df3a182003](https://github.com/0xfe/vexflow/commit/f90033f77bdf43ba03546811d85405df3a182003) Visual regression tests for versions in releases/X.Y.Z/

[7f3fa41601f3e6a06be349323d4090a6800fa395](https://github.com/0xfe/vexflow/commit/7f3fa41601f3e6a06be349323d4090a6800fa395) Updated docs.

[59d80942c09e7cd14fc395ec5a1b8b882ab3a5c3](https://github.com/0xfe/vexflow/commit/59d80942c09e7cd14fc395ec5a1b8b882ab3a5c3) ESM watch.

[296837fecd8f1c1e4982a7d0e8919d26d54647d0](https://github.com/0xfe/vexflow/commit/296837fecd8f1c1e4982a7d0e8919d26d54647d0) Merge branch 'master' into test

[bb4b5d4a812ad5e9bebde7ed3bab05ed00b7563a](https://github.com/0xfe/vexflow/commit/bb4b5d4a812ad5e9bebde7ed3bab05ed00b7563a) Build performance: - ForkTsCheckerWebpackPlugin - webpack build cache - webpack watch

[1d6e4c38b869695116f80a8013ebed7fde18a91a](https://github.com/0xfe/vexflow/commit/1d6e4c38b869695116f80a8013ebed7fde18a91a) Release script proceeds only if the working directory is clean (other than the src/version.ts file, which is auto generated on each build).

[9bba924ad141805924b510f23cde77ce5f44df44](https://github.com/0xfe/vexflow/commit/9bba924ad141805924b510f23cde77ce5f44df44) fix openGroup optional parameters

[b404958b192f84d65043f5697ac3c22de2d0d881](https://github.com/0xfe/vexflow/commit/b404958b192f84d65043f5697ac3c22de2d0d881) Merge pull request #1264 from rvilarl/fix/1255

[7374ff8fd037c447b8d430893ff803ef7366c568](https://github.com/0xfe/vexflow/commit/7374ff8fd037c447b8d430893ff803ef7366c568) Merge pull request #1261 from rvilarl/fix/1258

[512772e0bcae04ae30a9a82db552e63801ed914f](https://github.com/0xfe/vexflow/commit/512772e0bcae04ae30a9a82db552e63801ed914f) Font Modules.

[4adc3bf56cc022b6ee1d96d363abecb58c535100](https://github.com/0xfe/vexflow/commit/4adc3bf56cc022b6ee1d96d363abecb58c535100) package.json files list.

[fafe6706632ec0ee2f6859b4f91ebcefb0cf5a5b](https://github.com/0xfe/vexflow/commit/fafe6706632ec0ee2f6859b4f91ebcefb0cf5a5b) source-map ON by default. Simplify Gruntfile.

[c59b1c1ddc5e06792df763f517c4bd7c2a854209](https://github.com/0xfe/vexflow/commit/c59b1c1ddc5e06792df763f517c4bd7c2a854209) fix rebase

[90469178e239165612817b2b2dbaad8a1bb6da6f](https://github.com/0xfe/vexflow/commit/90469178e239165612817b2b2dbaad8a1bb6da6f) fix addModifier missing parameter

[9cec4e776e1df0aeb0c24716dfa4eaa6cca81937](https://github.com/0xfe/vexflow/commit/9cec4e776e1df0aeb0c24716dfa4eaa6cca81937) review comments

[078d1502881b95ae68da5573dd713ba9170d2ed1](https://github.com/0xfe/vexflow/commit/078d1502881b95ae68da5573dd713ba9170d2ed1) glyph scale option

[5ea4a2d6131e0be50d6edd44b443f8fb4cfbfa9c](https://github.com/0xfe/vexflow/commit/5ea4a2d6131e0be50d6edd44b443f8fb4cfbfa9c) x_shit & y_shift considering scale

[6f638f6733a5c52dcc2710545753ff793e2f9fd1](https://github.com/0xfe/vexflow/commit/6f638f6733a5c52dcc2710545753ff793e2f9fd1) support for big tremolo

[2d0f77fe286232c83c1d0653d08904445910c9ba](https://github.com/0xfe/vexflow/commit/2d0f77fe286232c83c1d0653d08904445910c9ba) Merge pull request #1288 from AaronDavidNewman/411-tuplet

[9c377e60a121d0b24c62d13d225358e33c3c04fc](https://github.com/0xfe/vexflow/commit/9c377e60a121d0b24c62d13d225358e33c3c04fc) Update tuplet.ts

[0fb6971d66b50bd43372380c7ccabc14bbbd1fe5](https://github.com/0xfe/vexflow/commit/0fb6971d66b50bd43372380c7ccabc14bbbd1fe5) Added task: grunt watch:fast

[b75482920a4f97bc20d159b2fe7f74e081a33a19](https://github.com/0xfe/vexflow/commit/b75482920a4f97bc20d159b2fe7f74e081a33a19) Fix bug with import which breaks the ESM build.

[71847bf8f9d4f7e279961c2fae499f2b0f076022](https://github.com/0xfe/vexflow/commit/71847bf8f9d4f7e279961c2fae499f2b0f076022) API Docs.

[ca983b586280e6e73b6b25fdb111c4bd8d6ac55a](https://github.com/0xfe/vexflow/commit/ca983b586280e6e73b6b25fdb111c4bd8d6ac55a) Gruntfile. Docs.

[c3faf1b1c3eebfc547fecbe823319770e8d02ad7](https://github.com/0xfe/vexflow/commit/c3faf1b1c3eebfc547fecbe823319770e8d02ad7) Merge branch 'master' into test

[3b88905a0188dbe8e8c8f2d790fa4170d3d1fdab](https://github.com/0xfe/vexflow/commit/3b88905a0188dbe8e8c8f2d790fa4170d3d1fdab) Improve how flow.html handles older releases.

[0e3e8f0c8d11377f76cd9f0b3e3d8deb2ded70c4](https://github.com/0xfe/vexflow/commit/0e3e8f0c8d11377f76cd9f0b3e3d8deb2ded70c4) Gruntfile docs.

[633316c2a0a9a3403b5c69f8905c7ce0f3726dd2](https://github.com/0xfe/vexflow/commit/633316c2a0a9a3403b5c69f8905c7ce0f3726dd2) Disable source maps by default to get the full build under 50 seconds.

[61afed437ce54fc69fe71f88c166fc4eb1bc53b2](https://github.com/0xfe/vexflow/commit/61afed437ce54fc69fe71f88c166fc4eb1bc53b2) Update CHANGELOG.md

[5dcff7286ea0e7e137fa4eabbd1d8873f56e2fa5](https://github.com/0xfe/vexflow/commit/5dcff7286ea0e7e137fa4eabbd1d8873f56e2fa5) Update CHANGELOG.md

[0d3c1762f1818a3ffc2f58693aa397782d55f4c0](https://github.com/0xfe/vexflow/commit/0d3c1762f1818a3ffc2f58693aa397782d55f4c0) cleanup for review comments

[d883ead626acab631428b4a477a54a9f488a17ef](https://github.com/0xfe/vexflow/commit/d883ead626acab631428b4a477a54a9f488a17ef) review comments

[e436a0d4d951185afb5c8b83f6e70dc81a41c616](https://github.com/0xfe/vexflow/commit/e436a0d4d951185afb5c8b83f6e70dc81a41c616) refactor repetition x position

[a70dd2b152800f2dbef75652f13f5ff7ff881d45](https://github.com/0xfe/vexflow/commit/a70dd2b152800f2dbef75652f13f5ff7ff881d45) review comments

[abcc2fb4c8363c44dfb81ee32ade106dd0010b5e](https://github.com/0xfe/vexflow/commit/abcc2fb4c8363c44dfb81ee32ade106dd0010b5e) osmd patch: StaveRepetition

[1cd8ea036e8a4315e05d07276dc822afb801b97b](https://github.com/0xfe/vexflow/commit/1cd8ea036e8a4315e05d07276dc822afb801b97b) Merge pull request #1262 from rvilarl/fix/1256

[d8befb3a596d91c2c015d002cab07a4ed9fcb7fd](https://github.com/0xfe/vexflow/commit/d8befb3a596d91c2c015d002cab07a4ed9fcb7fd) use actualBoundingBox when fontBoundingBox is not available

[463d4d330da05c330338413a8dd2ce46d4ca5457](https://github.com/0xfe/vexflow/commit/463d4d330da05c330338413a8dd2ce46d4ca5457) font measures with svg approach

[84fb9c688b0df2b60fdc46e0e907198450eb2111](https://github.com/0xfe/vexflow/commit/84fb9c688b0df2b60fdc46e0e907198450eb2111) fix font height calculations

[aebecd49819a8c7bf3285df3f611c857b3472efc](https://github.com/0xfe/vexflow/commit/aebecd49819a8c7bf3285df3f611c857b3472efc) review comments

[a8191abf6039c67befdf21b92df7285a7115835a](https://github.com/0xfe/vexflow/commit/a8191abf6039c67befdf21b92df7285a7115835a) osmd patch stave & stavesection

[bff9df130a47a3c0777fd0bd4647aa5ccab6a070](https://github.com/0xfe/vexflow/commit/bff9df130a47a3c0777fd0bd4647aa5ccab6a070) Merge pull request #1286 from rvilarl/fix/1285

[22561865849f47942c7301ac9e2ba5d2ba571139](https://github.com/0xfe/vexflow/commit/22561865849f47942c7301ac9e2ba5d2ba571139) Merge pull request #1279 from rvilarl/circularDep

[54e73b6795b6b296ae760eca6ee6dd593589afb6](https://github.com/0xfe/vexflow/commit/54e73b6795b6b296ae760eca6ee6dd593589afb6) Improve webpack build performance. Use eslint cache to speed up builds.

[d8e9681536f7cfcbebb79c2906445eae432dddfe](https://github.com/0xfe/vexflow/commit/d8e9681536f7cfcbebb79c2906445eae432dddfe) Move scripts into Gruntfile.js. Improve release scripts. Improve test scripts.

[c5ad7ab10c15c8176b30549e0f64af2868f7df57](https://github.com/0xfe/vexflow/commit/c5ad7ab10c15c8176b30549e0f64af2868f7df57) Release-it script improvements. Add more dry-run options. Set requireUpstream to false for release-it testing.

[b67b661be3a8a60d2008abd67bfee0eb4258a845](https://github.com/0xfe/vexflow/commit/b67b661be3a8a60d2008abd67bfee0eb4258a845) Consolidate Grunt and NPM scripts.

[88c749dd266b62b75aa23ec6bdfb832b85e983d2](https://github.com/0xfe/vexflow/commit/88c749dd266b62b75aa23ec6bdfb832b85e983d2) Remove redundant check

[096d283d1ef6e92241265747704db282ba15e74e](https://github.com/0xfe/vexflow/commit/096d283d1ef6e92241265747704db282ba15e74e) Adjust modifiers for top tuplet also

[c25bdd704556f40c9150825d1f0c63606bb19d04](https://github.com/0xfe/vexflow/commit/c25bdd704556f40c9150825d1f0c63606bb19d04) Add release-it to manage releases.

[fb193a86c0e9b8d8ea1554c85b6d561a1b4e7f68](https://github.com/0xfe/vexflow/commit/fb193a86c0e9b8d8ea1554c85b6d561a1b4e7f68) Add ESM support to flow.html.

[d9f509149d341fed45c6cf3ac607dab2a354a22e](https://github.com/0xfe/vexflow/commit/d9f509149d341fed45c6cf3ac607dab2a354a22e) Improve grunt watch. Remove eslint for watch tasks.

[0c874f2b93456d65ee1824669debdbe43d0870d5](https://github.com/0xfe/vexflow/commit/0c874f2b93456d65ee1824669debdbe43d0870d5) Fix imports. Avoid importing from 'xxxx/src', which breaks the ESM import rewriting at the moment.

[bf406ef95d07ae534d3b46c443cc8815b8733556](https://github.com/0xfe/vexflow/commit/bf406ef95d07ae534d3b46c443cc8815b8733556) fix tabnotes stem length

[af71abfe339b36ab3e9bffa716e3b99e494a7a40](https://github.com/0xfe/vexflow/commit/af71abfe339b36ab3e9bffa716e3b99e494a7a40) Improving build process.

[10e5db43f1046bc78e93b84c68d5343293882a7c](https://github.com/0xfe/vexflow/commit/10e5db43f1046bc78e93b84c68d5343293882a7c) Part of issue 411: Tuplet vertical formatting

[01e21a16f48a1d59a2174a4f20a542d162f86794](https://github.com/0xfe/vexflow/commit/01e21a16f48a1d59a2174a4f20a542d162f86794) remove dots attribute in Note

[2afec4961b6299370e0a024e0820efeb619d4085](https://github.com/0xfe/vexflow/commit/2afec4961b6299370e0a024e0820efeb619d4085) buildAndAttach in Parenthesis and Dot

[f5d59916360b83c2f77a78d142b2083521d34333](https://github.com/0xfe/vexflow/commit/f5d59916360b83c2f77a78d142b2083521d34333) remove addAccidental addAnnotation addArticulation

[37a9fdea9a191bb15b444e2b517bae3cfb680c9c](https://github.com/0xfe/vexflow/commit/37a9fdea9a191bb15b444e2b517bae3cfb680c9c) revert addModifier parameter order

[bc06474f0ebcd11b7fdaf54f31e58ca8425ed336](https://github.com/0xfe/vexflow/commit/bc06474f0ebcd11b7fdaf54f31e58ca8425ed336) review comments

[0191f4f40d6fcf5fab40d5fe8f84200922fc2b42](https://github.com/0xfe/vexflow/commit/0191f4f40d6fcf5fab40d5fe8f84200922fc2b42) remove circular dependency

[ea20b0604b05912301c38417be14c55923a7192b](https://github.com/0xfe/vexflow/commit/ea20b0604b05912301c38417be14c55923a7192b) Merge pull request #1249 from rvilarl/parenthesisedNotehead

[52e8716ebd5218c228f750febdb4315a13c1feee](https://github.com/0xfe/vexflow/commit/52e8716ebd5218c228f750febdb4315a13c1feee) Merge https://github.com/0xfe/vexflow into pr-1265

[4b14a6360e8bf1f90a3a698e2f500b635ffadcd0](https://github.com/0xfe/vexflow/commit/4b14a6360e8bf1f90a3a698e2f500b635ffadcd0) typedoc comments

[cf3f2de9e329412a0afd122a87c0f6207681cab8](https://github.com/0xfe/vexflow/commit/cf3f2de9e329412a0afd122a87c0f6207681cab8) review comments

[ba60bdf57686ebc47d85f9754ccbdd3edbf2843a](https://github.com/0xfe/vexflow/commit/ba60bdf57686ebc47d85f9754ccbdd3edbf2843a) fix formatting issues

[7197f3ab28d678d8d51e927e31824c8e850c5e77](https://github.com/0xfe/vexflow/commit/7197f3ab28d678d8d51e927e31824c8e850c5e77) parenthesis as modifier

[c303b6af317c2a3f37e2fc8570dcee17012e6595](https://github.com/0xfe/vexflow/commit/c303b6af317c2a3f37e2fc8570dcee17012e6595) fix rebase

[faf4de9dde4e77f7b46a2ba7efeb0fb5eb1f226d](https://github.com/0xfe/vexflow/commit/faf4de9dde4e77f7b46a2ba7efeb0fb5eb1f226d) getWidth declared for parenthesis notes

[62110d8451bf73fcc8ca6dadf107491434b6718d](https://github.com/0xfe/vexflow/commit/62110d8451bf73fcc8ca6dadf107491434b6718d) parenthesised noteheads

[9817b2cd741fc2d570cb2a2eedecf6668d936436](https://github.com/0xfe/vexflow/commit/9817b2cd741fc2d570cb2a2eedecf6668d936436) Merge pull request #1278 from rvilarl/docUpdate

[fb40f63fb93b384d9c4418f1f5f77d073569add5](https://github.com/0xfe/vexflow/commit/fb40f63fb93b384d9c4418f1f5f77d073569add5) Merge pull request #1277 from rvilarl/npmUpgrade

[75a91d5fb25cf3b4566c50ca26d564a5cdf16f9e](https://github.com/0xfe/vexflow/commit/75a91d5fb25cf3b4566c50ca26d564a5cdf16f9e) documentation update

[62a069d15c0428475fa0bbcc9c5ba9ad9d5cd2a6](https://github.com/0xfe/vexflow/commit/62a069d15c0428475fa0bbcc9c5ba9ad9d5cd2a6) npm-upgrade

[c00655f014c0fc6853af2be812191124728e659d](https://github.com/0xfe/vexflow/commit/c00655f014c0fc6853af2be812191124728e659d) Merge pull request #1273 from h-sug1no/vrtest-puppeteer-backend-3

[4e22d6d732b28c240ba9ae27859b263418237704](https://github.com/0xfe/vexflow/commit/4e22d6d732b28c240ba9ae27859b263418237704) Merge branch '0xfe:master' into vrtest-puppeteer-backend-3

[4462c86e35f4ea7d0b22c8c2dad7e5658a7797bb](https://github.com/0xfe/vexflow/commit/4462c86e35f4ea7d0b22c8c2dad7e5658a7797bb) fix a merge issue in TabNote

[caeb47066d006b4b477a8f6478af69691d922261](https://github.com/0xfe/vexflow/commit/caeb47066d006b4b477a8f6478af69691d922261) Fix cases with TabNote, Bend and Annotation

[73039c4c8b5de00bf89ec7cab673a9aac4ecf87c](https://github.com/0xfe/vexflow/commit/73039c4c8b5de00bf89ec7cab673a9aac4ecf87c) Merge https://github.com/0xfe/vexflow into pr-1265

[d4550a128f532a9aa089f46539ee7f2f9be3a0d0](https://github.com/0xfe/vexflow/commit/d4550a128f532a9aa089f46539ee7f2f9be3a0d0) Merge pull request #1275 from rvilarl/fix/circularDependency

[092456ccdeae15392c3bde4bb06fc2760f800083](https://github.com/0xfe/vexflow/commit/092456ccdeae15392c3bde4bb06fc2760f800083) fix dependency

[8567216824f837450c86a28eec25989a3e6bb1b8](https://github.com/0xfe/vexflow/commit/8567216824f837450c86a28eec25989a3e6bb1b8) Merge https://github.com/0xfe/vexflow into pr-1265

[b8c0ebf38a54a649a9d6dfb2e49860d23dee6112](https://github.com/0xfe/vexflow/commit/b8c0ebf38a54a649a9d6dfb2e49860d23dee6112) fix issues regarding annotations on tab notes

[4e265c3930cbf910d99b619b8be9ba070e28855e](https://github.com/0xfe/vexflow/commit/4e265c3930cbf910d99b619b8be9ba070e28855e) fix circular dependency

[17d73549c278ef0d8d91f5db034fcd4db58f6b3b](https://github.com/0xfe/vexflow/commit/17d73549c278ef0d8d91f5db034fcd4db58f6b3b) reduce jsdom_jobs on platform with many cpus. - ex: MBP: 12 logical cpus.

[9b12482424dd0fc36846b9182519d3289a5e75bc](https://github.com/0xfe/vexflow/commit/9b12482424dd0fc36846b9182519d3289a5e75bc) Merge pull request #1260 from rvilarl/easyscoreMutedHarmonySlashGhost2

[a2570076497367ccba8ddc8a9ccdb299a882c754](https://github.com/0xfe/vexflow/commit/a2570076497367ccba8ddc8a9ccdb299a882c754) Merge pull request #1268 from h-sug1no/vrtest-puppeteer-backend-2

[63052e49e94bbfe13928a7c89b678a5ee6060a08](https://github.com/0xfe/vexflow/commit/63052e49e94bbfe13928a7c89b678a5ee6060a08) Merge https://github.com/0xfe/vexflow into pr-1265

[0a8eec238857cf52d82cc711a9fb61aa230cf756](https://github.com/0xfe/vexflow/commit/0a8eec238857cf52d82cc711a9fb61aa230cf756) consider cjs/

[c0b8f8c9e3de4c25dc765612077dddd3d42c2fd6](https://github.com/0xfe/vexflow/commit/c0b8f8c9e3de4c25dc765612077dddd3d42c2fd6) Merge branch 'master' into vrtest-puppeteer-backend-2

[8cd3b7eafc8d737412091104d7b974b3ac3283a7](https://github.com/0xfe/vexflow/commit/8cd3b7eafc8d737412091104d7b974b3ac3283a7) Merge pull request #1272 from rvilarl/fix/testReference

[56227ed3bede2b5ed815f1f2c311ad41db657505](https://github.com/0xfe/vexflow/commit/56227ed3bede2b5ed815f1f2c311ad41db657505) review comments

[dc3820fee2e2247ea5fba1548e4a6a1c766e9c0b](https://github.com/0xfe/vexflow/commit/dc3820fee2e2247ea5fba1548e4a6a1c766e9c0b) fix npm run test:reference

[611db12e2c45842ccc71e5367815ccb72504e969](https://github.com/0xfe/vexflow/commit/611db12e2c45842ccc71e5367815ccb72504e969) Merge pull request #1232 from ronyeh/ESM

[3ac39b2607dec8b4fb1005bae6b49a9be3fadac8](https://github.com/0xfe/vexflow/commit/3ac39b2607dec8b4fb1005bae6b49a9be3fadac8) Fix package.json types field.

[c3b67d4b9b61fe3a884136c0e38ace8bdd38ea3a](https://github.com/0xfe/vexflow/commit/c3b67d4b9b61fe3a884136c0e38ace8bdd38ea3a) easyscore support for ghostnote

[109389bccab8a1bec421a9a4118515a3bc0e0de2](https://github.com/0xfe/vexflow/commit/109389bccab8a1bec421a9a4118515a3bc0e0de2) Update comments and API docs.

[437d802e9280e626a74adb2ecaec6cbe669b1b2d](https://github.com/0xfe/vexflow/commit/437d802e9280e626a74adb2ecaec6cbe669b1b2d) eslint auto fixes.

[6bf26e9269bd8e5d6b7e621ed6d4391b2038c153](https://github.com/0xfe/vexflow/commit/6bf26e9269bd8e5d6b7e621ed6d4391b2038c153) Merge branch 'master' into ESM

[85a9dbbda476303eb0f7abc82ecc0f25b96fa6c8](https://github.com/0xfe/vexflow/commit/85a9dbbda476303eb0f7abc82ecc0f25b96fa6c8) fix failed test case due to annotation in ghost note

[9b4afe458a226534d403f4e14bc0836693c3bd1c](https://github.com/0xfe/vexflow/commit/9b4afe458a226534d403f4e14bc0836693c3bd1c) fix #1265

[5d26dffa612411f7bda23a18f074b5b735e351b6](https://github.com/0xfe/vexflow/commit/5d26dffa612411f7bda23a18f074b5b735e351b6) fix usage. (review comment)

[da0ad7ababa58e696664269dd2a5cc0f029c2c80](https://github.com/0xfe/vexflow/commit/da0ad7ababa58e696664269dd2a5cc0f029c2c80) Merge pull request #1269 from AaronDavidNewman/issue1267-articYPos

[501ec1e05b5c62ba0b31a0af406a60a7d4eb0fbb](https://github.com/0xfe/vexflow/commit/501ec1e05b5c62ba0b31a0af406a60a7d4eb0fbb) log resolved parallel option value.

[e82c9e3ebfb1373715ce219d6d818ed027d64891](https://github.com/0xfe/vexflow/commit/e82c9e3ebfb1373715ce219d6d818ed027d64891) cleanup.

[d6389fdca87a773796a6394244a5f0984fd1917f](https://github.com/0xfe/vexflow/commit/d6389fdca87a773796a6394244a5f0984fd1917f) [WIP]: cleanup.

[a3569f109a4273e4d2e4a94056813694a69d4be0](https://github.com/0xfe/vexflow/commit/a3569f109a4273e4d2e4a94056813694a69d4be0) [WIP]: fix child process management.

[efb7f9276b186315fb744a3f10e2ed3fc9888109](https://github.com/0xfe/vexflow/commit/efb7f9276b186315fb744a3f10e2ed3fc9888109) consider stem direction

[76c4a49c86fc90bbbb8f2fe2d67b8e601c75ec2f](https://github.com/0xfe/vexflow/commit/76c4a49c86fc90bbbb8f2fe2d67b8e601c75ec2f) fix overlapping vertical accidentals when outside staff

[c20426ec3a57f945af366750653b584a63d36fd5](https://github.com/0xfe/vexflow/commit/c20426ec3a57f945af366750653b584a63d36fd5) remove unused debug code.

[54e7fc9a553d96646e0518ae82868bc198e53d04](https://github.com/0xfe/vexflow/commit/54e7fc9a553d96646e0518ae82868bc198e53d04) [WIP]: rename --backend to --backends.

[bc85a14f95004c695d1eee1ffeffdd12fbff083f](https://github.com/0xfe/vexflow/commit/bc85a14f95004c695d1eee1ffeffdd12fbff083f) [WIP]: flow.html: support ver=releases* like jsdom backend. ex: npm run get:releases 3.0.9 then load flow.html?module=Beam&ver=releases/3.0.9

[c305de874df840de664f5505e4cb3bea4eecc3d0](https://github.com/0xfe/vexflow/commit/c305de874df840de664f5505e4cb3bea4eecc3d0) [WIP]: fix warning msg.

[8c1269410e87047e554935fb5ea72918876a8113](https://github.com/0xfe/vexflow/commit/8c1269410e87047e554935fb5ea72918876a8113) [WIP]: fix warning.

[75c3268ea6ef3b4d969bd0b038aef8a3c9bb7a88](https://github.com/0xfe/vexflow/commit/75c3268ea6ef3b4d969bd0b038aef8a3c9bb7a88) [WIP]: fix default job{s} values.

[095540a499d4c84ff7b43286c722300a996cddfa](https://github.com/0xfe/vexflow/commit/095540a499d4c84ff7b43286c722300a996cddfa) [WIP]: Merge branch 'master' into vrtest-puppeteer-backend-2

[9fe7451c33519c1dbfc989db9f0affda48dd83f4](https://github.com/0xfe/vexflow/commit/9fe7451c33519c1dbfc989db9f0affda48dd83f4) [WIP]: add --job{s} option comment.

[38f6d3205d019d23b94251f76808967e2f1d26b7](https://github.com/0xfe/vexflow/commit/38f6d3205d019d23b94251f76808967e2f1d26b7) [WIP]: fix filename for old builds.

[c311ca03d29deab150bbab05e70ce019bb0a1d6f](https://github.com/0xfe/vexflow/commit/c311ca03d29deab150bbab05e70ce019bb0a1d6f) [WIP]: rename jobId to job.

[7d6c6395568097c8a6763873c72dcdb3b76beef9](https://github.com/0xfe/vexflow/commit/7d6c6395568097c8a6763873c72dcdb3b76beef9) [WIP]: fix child proc management.

[9830cec05d3077a2f41e4d0b8a7c4543b6e78f46](https://github.com/0xfe/vexflow/commit/9830cec05d3077a2f41e4d0b8a7c4543b6e78f46) [WIP]: show "aborted." if errorCode != 0 on exit.

[3e4ca4fd6ff6e876705b0f600a04c781a540d719](https://github.com/0xfe/vexflow/commit/3e4ca4fd6ff6e876705b0f600a04c781a540d719) [WIP]: wait all children.

[b54e5997b7e8e2b58737ab6f752f8302565c8683](https://github.com/0xfe/vexflow/commit/b54e5997b7e8e2b58737ab6f752f8302565c8683) [WIP]: reduce progress log. - jsdom: fix old build support.

[f6d912a566cae6bc224c517f9fc3739634eab049](https://github.com/0xfe/vexflow/commit/f6d912a566cae6bc224c517f9fc3739634eab049) [WIP]: jsdom: use parallel option value as the jobs option value. - add usage().

[b5ad91f4183d12168e4b356cc1411ff2e6a57a25](https://github.com/0xfe/vexflow/commit/b5ad91f4183d12168e4b356cc1411ff2e6a57a25) [WIP]: show file save progress.

[aede9b3b7ae343fd35c0fab5a08831f7a66c68df](https://github.com/0xfe/vexflow/commit/aede9b3b7ae343fd35c0fab5a08831f7a66c68df) Update demos.

[c3ce10e100663ab480f36c7975736508ef23f4cf](https://github.com/0xfe/vexflow/commit/c3ce10e100663ab480f36c7975736508ef23f4cf) Rename Gruntfile.js variable to DEBUG_CIRCULAR_DEPENDENCIES.

[faba4186255cf5879a22494236bbd9c23d00cc55](https://github.com/0xfe/vexflow/commit/faba4186255cf5879a22494236bbd9c23d00cc55) [WIP]: add RunOptions{jobs:number, jobId: nuber} to run jsdom backend in parallel. - Moved the implementation of child process management from each backend to generate_images.js.

[205e17175347637b79348d447fc5577887095a80](https://github.com/0xfe/vexflow/commit/205e17175347637b79348d447fc5577887095a80) Merge pull request #1243 from rvilarl/fix/941

[d38a292f6f92265abc51ab20b4983da647fa0ce4](https://github.com/0xfe/vexflow/commit/d38a292f6f92265abc51ab20b4983da647fa0ce4) review comment

[13724d4410239db4507aa6210b3bcdcbe1be13df](https://github.com/0xfe/vexflow/commit/13724d4410239db4507aa6210b3bcdcbe1be13df) Merge pull request #1259 from rvilarl/easyscoreMutedHarmonySlash

[dca0556e0dfdbd3526aded4dd690442c973165e1](https://github.com/0xfe/vexflow/commit/dca0556e0dfdbd3526aded4dd690442c973165e1) Fix comments.

[8d9e20627e5dc114f40897525959ede2e38d6c0c](https://github.com/0xfe/vexflow/commit/8d9e20627e5dc114f40897525959ede2e38d6c0c) Documentation for the Gruntfile environment variables.

[29fa14f1a842e0add3afcdc4d11ac20b16484249](https://github.com/0xfe/vexflow/commit/29fa14f1a842e0add3afcdc4d11ac20b16484249) easyscore support for muted & harmonic

[00e977883222905c636ce6af9eaace697291f40f](https://github.com/0xfe/vexflow/commit/00e977883222905c636ce6af9eaace697291f40f) review comments

[539ecf96a70e1a7af7a557d65aa1653a6750a7c5](https://github.com/0xfe/vexflow/commit/539ecf96a70e1a7af7a557d65aa1653a6750a7c5) [WIP]: use (.name)elm.id to generate filename if available. (for recent flow.html dom tree).

[635f40d65c5665edecbaa9635df3d6be15755503](https://github.com/0xfe/vexflow/commit/635f40d65c5665edecbaa9635df3d6be15755503) [WIP]: remove console.log.

[422c97c397afe59c362bba09c516ca7a27e3c79b](https://github.com/0xfe/vexflow/commit/422c97c397afe59c362bba09c516ca7a27e3c79b) [WIP]: remove --backcompat option. - jsdom: run Bravura and other font to ensure backcompat filename.

[43626c30236bab5bd514733fb2c17bd1ec19b815](https://github.com/0xfe/vexflow/commit/43626c30236bab5bd514733fb2c17bd1ec19b815) [WIP]: vrtest: add pptr backend.

[c95c43b668b72426e1a943ab296f1e9ce4d6d1ff](https://github.com/0xfe/vexflow/commit/c95c43b668b72426e1a943ab296f1e9ce4d6d1ff) [WIP]: vrtest: add pptr backend.

[f1b359c255c639a9b9d909a9a4b2c96cbac6a6e7](https://github.com/0xfe/vexflow/commit/f1b359c255c639a9b9d909a9a4b2c96cbac6a6e7) Improve Gruntfile.js > ESM > copy package.json Update comments.

[f145b1df1c21c9719dc659cc26c519ecb6d11488](https://github.com/0xfe/vexflow/commit/f145b1df1c21c9719dc659cc26c519ecb6d11488) Cleanup. API Docs.

[5392e002121679386d180599f8460948252528bb](https://github.com/0xfe/vexflow/commit/5392e002121679386d180599f8460948252528bb) Merge branch 'master' into ESM

[f5393d023344468ad9a8b43c007882b521bda849](https://github.com/0xfe/vexflow/commit/f5393d023344468ad9a8b43c007882b521bda849) No more need for the publicPath module. Remove references to BASE_PATH.

[2add8106c54e14121a71e42e6956e45621af023b](https://github.com/0xfe/vexflow/commit/2add8106c54e14121a71e42e6956e45621af023b) fix percussion Basic0

[4a7522f5c8c66900c343b1058a1ce18228528ba8](https://github.com/0xfe/vexflow/commit/4a7522f5c8c66900c343b1058a1ce18228528ba8) stem size with beams fixed

[60391139e5ed21627e55308c4208bb26eb6025cc](https://github.com/0xfe/vexflow/commit/60391139e5ed21627e55308c4208bb26eb6025cc) fix stem & flag heights

[77bb43cd67fc2b6dfdc275c384d59b463564edf9](https://github.com/0xfe/vexflow/commit/77bb43cd67fc2b6dfdc275c384d59b463564edf9) Plug-in approach for music engraving fonts.

[3ccbd6415f60bcca720267de375b8ca6f2dd9a5f](https://github.com/0xfe/vexflow/commit/3ccbd6415f60bcca720267de375b8ca6f2dd9a5f) Merge pull request #1242 from rvilarl/noGlyphsAdditiveTimeSig

[00836020884d664137c26e7817206cf6c0203ccd](https://github.com/0xfe/vexflow/commit/00836020884d664137c26e7817206cf6c0203ccd) Merge pull request #1250 from ronyeh/get-releases

[4ae9441e022a92ac0d1829d01d26fc058b6babdf](https://github.com/0xfe/vexflow/commit/4ae9441e022a92ac0d1829d01d26fc058b6babdf) Small changes to support integration with OSMD. Include offscreencanvas type information directly, to remove a dependency.

[166dfd44961da814017f5d1cffd76efb753e0bdd](https://github.com/0xfe/vexflow/commit/166dfd44961da814017f5d1cffd76efb753e0bdd) Add a README. Cleanup.

[dc8033bbee57739ab7cf460034fd213b41ed52d2](https://github.com/0xfe/vexflow/commit/dc8033bbee57739ab7cf460034fd213b41ed52d2) Remove console.log() for temp folder.

[7e3f47ef71022372182b667c24c9387eacb8e4f8](https://github.com/0xfe/vexflow/commit/7e3f47ef71022372182b667c24c9387eacb8e4f8) Adds a script to retrieve releases by version number. For versions <= 3.0.9, release files are extracted from the git repository. For versions >= 4.0.0, release files are downloaded from npm.

[407ae45d5e9cdacf7fb7c128f42c85412aa82b8b](https://github.com/0xfe/vexflow/commit/407ae45d5e9cdacf7fb7c128f42c85412aa82b8b) Merge branch 'master' into ESM

[6523259265b8ef9746f9da8d265ca4a7105174cb](https://github.com/0xfe/vexflow/commit/6523259265b8ef9746f9da8d265ca4a7105174cb) Support dynamic font loading in as many situations as possible (including in web workers). For CJS builds, utilize webpack's publicPath feature. In ESM builds, dynamic import() works natively.

[30841cf44bf050d5ee473ecf1a0bec11f8191eb3](https://github.com/0xfe/vexflow/commit/30841cf44bf050d5ee473ecf1a0bec11f8191eb3) gonville inspector

[b31829e64a2f064bed6ea93ca6e00fb32af19526](https://github.com/0xfe/vexflow/commit/b31829e64a2f064bed6ea93ca6e00fb32af19526) TimeSignature examples

[4bf017e802a66a09d96f28451408a9c25f7eaa0f](https://github.com/0xfe/vexflow/commit/4bf017e802a66a09d96f28451408a9c25f7eaa0f) review comments

[15d96826e5c3dc341aab447163e4de015e8926ae](https://github.com/0xfe/vexflow/commit/15d96826e5c3dc341aab447163e4de015e8926ae) fix y location of time signatures without bottom glyphs

[62ff464bdb5092d5c7802ac61753b95727c0cf8e](https://github.com/0xfe/vexflow/commit/62ff464bdb5092d5c7802ac61753b95727c0cf8e) additive & complex signatures

[6a7b529b3ec3c55516444ad1341747f99dceffda](https://github.com/0xfe/vexflow/commit/6a7b529b3ec3c55516444ad1341747f99dceffda) Merge pull request #1248 from rvilarl/noGlyphsOnly

[29c43f06c4bb038d704f6c8ada6ccea6c6e13fcd](https://github.com/0xfe/vexflow/commit/29c43f06c4bb038d704f6c8ada6ccea6c6e13fcd) Change the test case so that it does not fail in Safari. https://github.com/0xfe/vexflow/issues/1240

[fa0b07770c79a3e6635e1d43869c0dde9e73320c](https://github.com/0xfe/vexflow/commit/fa0b07770c79a3e6635e1d43869c0dde9e73320c) Fix imports. Fix circular reference. Ran the build, which regenerated the docs/api/.

[e1807f4a60bf4d34c6582a33a30afaf0ab85b013](https://github.com/0xfe/vexflow/commit/e1807f4a60bf4d34c6582a33a30afaf0ab85b013) Merge branch 'master' into ESM

[10cd36ed57990efe9957607600a9e0c21702a19b](https://github.com/0xfe/vexflow/commit/10cd36ed57990efe9957607600a9e0c21702a19b) remove NOGLYPHS

[2b0e4c35fc168d6bebc433a5a80193e664c5fe16](https://github.com/0xfe/vexflow/commit/2b0e4c35fc168d6bebc433a5a80193e664c5fe16) Merge pull request #1246 from rvilarl/fix/1146

[e61f949e906583d7b4352a914e917c87e1b35df9](https://github.com/0xfe/vexflow/commit/e61f949e906583d7b4352a914e917c87e1b35df9) Merge pull request #1247 from rvilarl/fixReference

[bb7aae62bf253a27000c74137eca2732461844ce](https://github.com/0xfe/vexflow/commit/bb7aae62bf253a27000c74137eca2732461844ce) fix grunt reference

[93f0c9a552ea2f0196edcc478574e2d690ff0fb4](https://github.com/0xfe/vexflow/commit/93f0c9a552ea2f0196edcc478574e2d690ff0fb4) clean up options

[c3297ce4ed4437b972ce43cf5e9f130bf1756b64](https://github.com/0xfe/vexflow/commit/c3297ce4ed4437b972ce43cf5e9f130bf1756b64) Merge pull request #1244 from rvilarl/fix/1149

[3c9bd52d3a0c945ec0db0bedbf60b228beb79049](https://github.com/0xfe/vexflow/commit/3c9bd52d3a0c945ec0db0bedbf60b228beb79049) Merge pull request #1245 from rvilarl/fix/836

[1401ce6c6d2cd7a86e53912124821e902ed91e24](https://github.com/0xfe/vexflow/commit/1401ce6c6d2cd7a86e53912124821e902ed91e24) Extract individual font loading modules so we can support ESM/CJS better. Add node demo that loads music fonts dynamically.

[737b395c6053ded21ac1e96f4dc79f7b8271591d](https://github.com/0xfe/vexflow/commit/737b395c6053ded21ac1e96f4dc79f7b8271591d) ElementStyle documented

[23ef7e50b2e030b07d3c90f13f0849c2c964a4fc](https://github.com/0xfe/vexflow/commit/23ef7e50b2e030b07d3c90f13f0849c2c964a4fc) documentation update

[d77453b4fdfa507c2ed0fe4ed293ed727a4768fe](https://github.com/0xfe/vexflow/commit/d77453b4fdfa507c2ed0fe4ed293ed727a4768fe) setStyle documented

[32f9adc67e3918ce3dddc55b9d756ca4f373de4c](https://github.com/0xfe/vexflow/commit/32f9adc67e3918ce3dddc55b9d756ca4f373de4c) SystemParam / FormatOptions renamed

[c932ccb152aa8adbb56e6c75b23c5c29a96550ea](https://github.com/0xfe/vexflow/commit/c932ccb152aa8adbb56e6c75b23c5c29a96550ea) Fix circular dependencies with help from CircularDependencyPlugin.

[4d798ca1d315d63d01a7d630b46f6345ab13c1ba](https://github.com/0xfe/vexflow/commit/4d798ca1d315d63d01a7d630b46f6345ab13c1ba) Allow developers to customize the publicPath setting when using vexflow-core.js. This allows for flexibility in deployments.

[ce709de7bc034499b5a285addc1e53a23ee4d1a6](https://github.com/0xfe/vexflow/commit/ce709de7bc034499b5a285addc1e53a23ee4d1a6) Merge pull request #1239 from rvilarl/packagesUpgrade

[b185ed0470341ad4cff135308ceb9acc6e3dae3a](https://github.com/0xfe/vexflow/commit/b185ed0470341ad4cff135308ceb9acc6e3dae3a) documentation automatic update

[a8b7ed28213388ef4b3c744178ada5ae5725e074](https://github.com/0xfe/vexflow/commit/a8b7ed28213388ef4b3c744178ada5ae5725e074) png treated as binary, typedoc generates in docs/api

[040bf560eebcaaf0d036a4971643b4f3a2c8ac10](https://github.com/0xfe/vexflow/commit/040bf560eebcaaf0d036a4971643b4f3a2c8ac10) npm-upgrade after rebase

[a4a5f8b917afc4185f4aa642851013e511f99e36](https://github.com/0xfe/vexflow/commit/a4a5f8b917afc4185f4aa642851013e511f99e36) npm-upgrade

[3abb0bd9ddbf178b63ae1cbc2577dfc0df5225cd](https://github.com/0xfe/vexflow/commit/3abb0bd9ddbf178b63ae1cbc2577dfc0df5225cd) npm-upgrade & docco dependency removed

[e3d0eb8f7eab7900b645245adfa61a2a680fc015](https://github.com/0xfe/vexflow/commit/e3d0eb8f7eab7900b645245adfa61a2a680fc015) Merge pull request #1238 from rvilarl/test/411

[7174bcaa2e4839d37b1d84ee3eadb28c6e222228](https://github.com/0xfe/vexflow/commit/7174bcaa2e4839d37b1d84ee3eadb28c6e222228) Merge pull request #1230 from ronyeh/remove-releases

[5c6602b8a99d06f6d7eb2ae36f1dfc95b9b23c18](https://github.com/0xfe/vexflow/commit/5c6602b8a99d06f6d7eb2ae36f1dfc95b9b23c18) Add test for issue #411

[a44b7818de42be1fded3fd741088e809a47fa687](https://github.com/0xfe/vexflow/commit/a44b7818de42be1fded3fd741088e809a47fa687) Merge branch 'master' into remove-releases

[8fba46239218f1e8c13973e8357332899d8a5c4c](https://github.com/0xfe/vexflow/commit/8fba46239218f1e8c13973e8357332899d8a5c4c) Merge pull request #1233 from ronyeh/font/use-constants

[247f6cc1d4dfd7b752c639cf4175f1b2496978e7](https://github.com/0xfe/vexflow/commit/247f6cc1d4dfd7b752c639cf4175f1b2496978e7) Merge pull request #1229 from rvilarl/apiDocumentation

[00b5e22fcb9e46a2cd6648346ab574477e5badac](https://github.com/0xfe/vexflow/commit/00b5e22fcb9e46a2cd6648346ab574477e5badac) apidocs renamed to api

[b66967c787267ab8359cc9b441cc8ac14dfd480b](https://github.com/0xfe/vexflow/commit/b66967c787267ab8359cc9b441cc8ac14dfd480b) Bump GitHub CI Node version.

[d5a99f5f53d61304f96a3e007dbb27ca56f7e629](https://github.com/0xfe/vexflow/commit/d5a99f5f53d61304f96a3e007dbb27ca56f7e629) Update demos. Bump TypeScript to 4.5 release. Turn off source maps by default.

[406e06749c36b11b148b34827e80107b5b380951](https://github.com/0xfe/vexflow/commit/406e06749c36b11b148b34827e80107b5b380951) ESM support! - Move entry files out to vexflow/entry/* - Rewrite imports and exports to have the .js extension (for all files in build/esm/). - Update demos. - Write version.ts file with version number and commit ID.

[aa4985d9a422ea84f9daf79d90fe7d0611822ff9](https://github.com/0xfe/vexflow/commit/aa4985d9a422ea84f9daf79d90fe7d0611822ff9) Move @types/offscreencanvas to regular dependencies in package.json.

[6a9d9bf028413137322681a0503a87b0a9f0da79](https://github.com/0xfe/vexflow/commit/6a9d9bf028413137322681a0503a87b0a9f0da79) Introduce visual diff from master. Use Font.* constants to make default fonts more consistent and robust. Fixed: Annotation line height calculation.

[05c53aa55ac3c00903ce76b128b6369ff10aebdc](https://github.com/0xfe/vexflow/commit/05c53aa55ac3c00903ce76b128b6369ff10aebdc) Move @types/offscreencanvas to regular dependencies. Fixes https://github.com/0xfe/vexflow/issues/1234

[601ba8fa3f284c46d7a21064c6d5fe3f343cd7a3](https://github.com/0xfe/vexflow/commit/601ba8fa3f284c46d7a21064c6d5fe3f343cd7a3) Remove grunt-release, which fixes https://github.com/0xfe/vexflow/issues/1225

[5de2abf74f2db39ae193cacc842a0a7a7e90e174](https://github.com/0xfe/vexflow/commit/5de2abf74f2db39ae193cacc842a0a7a7e90e174) Fix https://github.com/0xfe/vexflow/issues/1180

[716d728d488072346a91e5fae4e185f34e296dab](https://github.com/0xfe/vexflow/commit/716d728d488072346a91e5fae4e185f34e296dab) No longer using the releases/ folder to publish to NPM.

[393bbf4b06d4e336fafc49566d3c2d9482e6ae0d](https://github.com/0xfe/vexflow/commit/393bbf4b06d4e336fafc49566d3c2d9482e6ae0d) api documentation issues fixed

[007c8cee18e062fd27b79099ea4ae62f488b39c1](https://github.com/0xfe/vexflow/commit/007c8cee18e062fd27b79099ea4ae62f488b39c1) Update README.

[d0a0d276a6c59eeed94ac6d8c5743ff221970557](https://github.com/0xfe/vexflow/commit/d0a0d276a6c59eeed94ac6d8c5743ff221970557) Remove JS files from releases/ folder.

[c72a5ba65572ddb7b0bcaac2352906e89da48c53](https://github.com/0xfe/vexflow/commit/c72a5ba65572ddb7b0bcaac2352906e89da48c53) Bump version.

[fd6ca9faa0ca62e7383c6cfe85dbdcbb8c8f2e7c](https://github.com/0xfe/vexflow/commit/fd6ca9faa0ca62e7383c6cfe85dbdcbb8c8f2e7c) Merge branch 'ronyeh-4.0.0-alpha'

[4c5f2d4518ea0b8060e0eadebf4cea58a9c92d25](https://github.com/0xfe/vexflow/commit/4c5f2d4518ea0b8060e0eadebf4cea58a9c92d25) Merge branch '4.0.0-alpha' of https://github.com/ronyeh/vexflow into ronyeh-4.0.0-alpha

[27f592b084e39b33003fbf8ee39131c58889ff1a](https://github.com/0xfe/vexflow/commit/27f592b084e39b33003fbf8ee39131c58889ff1a) Add AUTHORS.md.

[488135ff12ea501d540b79b1a68d3137752d3356](https://github.com/0xfe/vexflow/commit/488135ff12ea501d540b79b1a68d3137752d3356) Remove tests/ from the NPM package.

[33f2d8b15a85b1716058ef54e5d30b1e4279e44e](https://github.com/0xfe/vexflow/commit/33f2d8b15a85b1716058ef54e5d30b1e4279e44e) Comments.

[e596995ad011f5d0659b0b052a880bffb71ded0d](https://github.com/0xfe/vexflow/commit/e596995ad011f5d0659b0b052a880bffb71ded0d) Include OffscreenCanvas tests.

[b07a63fd8252899a57ec30b930e84309b0d1bfcb](https://github.com/0xfe/vexflow/commit/b07a63fd8252899a57ec30b930e84309b0d1bfcb) Improve demos.

[a835afd016a0181617a8149c64a36be123435bf1](https://github.com/0xfe/vexflow/commit/a835afd016a0181617a8149c64a36be123435bf1) Update README. Improve comments. http:// => https:// Fix some broken URLs.

[56ba6eac4edc915e9de59e454c02daf158d9a018](https://github.com/0xfe/vexflow/commit/56ba6eac4edc915e9de59e454c02daf158d9a018) Use isHTMLCanvas() and globalObject() util methods.

[ffe2ae88a26039fcc201f08c97994cefea8786fb](https://github.com/0xfe/vexflow/commit/ffe2ae88a26039fcc201f08c97994cefea8786fb) Merge branch 'master' into 4.0.0-alpha

[6be0ac8988eb7f09f208888374a0e5e268eff6ef](https://github.com/0xfe/vexflow/commit/6be0ac8988eb7f09f208888374a0e5e268eff6ef) Add globalObject() util method to retrieve globalThis or window.

[945393d5aff9cbfb65a1799620a986041e289ba5](https://github.com/0xfe/vexflow/commit/945393d5aff9cbfb65a1799620a986041e289ba5) Update demos. Include a PDF output demo.

[811b2d1fbbd5656e5c092301f0f69700782231e0](https://github.com/0xfe/vexflow/commit/811b2d1fbbd5656e5c092301f0f69700782231e0) Address review comments from 0xfe.

[7745beffa13056c60714faa383d0d6ff5568135d](https://github.com/0xfe/vexflow/commit/7745beffa13056c60714faa383d0d6ff5568135d) Merge pull request #1219 from tommadams/offscreen_canvas

[7e016c0beb94801509618860599a38b2186213e5](https://github.com/0xfe/vexflow/commit/7e016c0beb94801509618860599a38b2186213e5) Convert Tables from a JS object to a class with static methods.

[beb0c13ef9838e4c51ed0521f69a348da1fb103c](https://github.com/0xfe/vexflow/commit/beb0c13ef9838e4c51ed0521f69a348da1fb103c) Merge branch 'master' into 4.0.0-alpha

[871f4a772a274ce97dc81eccd892d3d762d215d5](https://github.com/0xfe/vexflow/commit/871f4a772a274ce97dc81eccd892d3d762d215d5) Merge pull request #1220 from ronyeh/fix/gruntwatch

[74787365846ff0cf284f4881d487d29620bffae3](https://github.com/0xfe/vexflow/commit/74787365846ff0cf284f4881d487d29620bffae3) Merge pull request #1223 from rvilarl/commentFixes

[cbd60f7a993921fb2d81ea523ff5f2a39cdf6e7f](https://github.com/0xfe/vexflow/commit/cbd60f7a993921fb2d81ea523ff5f2a39cdf6e7f) Flexible type checking for HTMLCanvasElement and HTMLDivElement. Fix demos.

[20c9b6293bc744b2e5d78cd9fc365a8affaa0f4e](https://github.com/0xfe/vexflow/commit/20c9b6293bc744b2e5d78cd9fc365a8affaa0f4e) Improvements to support use as an ES module. API adjustments to support the migration of music21j to VexFlow 4.

[5a118eef5bbb0a5f1f2c662708fd6936ee67b661](https://github.com/0xfe/vexflow/commit/5a118eef5bbb0a5f1f2c662708fd6936ee67b661) Improve font accessors in Element class.

[2971a8d36b0556818cc6c743a7950e52a41138e5](https://github.com/0xfe/vexflow/commit/2971a8d36b0556818cc6c743a7950e52a41138e5) comments fixed

[3b1a8db29b99b13b52d1b57623ee5f3d6dbad4e9](https://github.com/0xfe/vexflow/commit/3b1a8db29b99b13b52d1b57623ee5f3d6dbad4e9) Improve backwards compatibility with 3.0.9. - Make some protected members public. - Add accessors as needed.

[2503d3ebaf39d5f2c6f1f3a1cfd231e1b8e9f578](https://github.com/0xfe/vexflow/commit/2503d3ebaf39d5f2c6f1f3a1cfd231e1b8e9f578) Fix demos.

[cc3837d2f4e20be4dadfdf72435d5bc8ba322769](https://github.com/0xfe/vexflow/commit/cc3837d2f4e20be4dadfdf72435d5bc8ba322769) GCD bug fix by @rvilarl. Add tests.

[1189c15d07a9192bf282ff9fdc9f58e101617859](https://github.com/0xfe/vexflow/commit/1189c15d07a9192bf282ff9fdc9f58e101617859) Reorganize test runner to avoid circular references.

[8632f856ce6f1327992418afa919cf45b3c6b7fe](https://github.com/0xfe/vexflow/commit/8632f856ce6f1327992418afa919cf45b3c6b7fe) Add accessor methods to help with migrating projects from 3.0.9 to 4.0.0.

[46d88df631fbe03dd3e81a74554f751bfdbc47f2](https://github.com/0xfe/vexflow/commit/46d88df631fbe03dd3e81a74554f751bfdbc47f2) fix bug when running under node

[3082ff0eb17895e3394dfeb139b3036165105240](https://github.com/0xfe/vexflow/commit/3082ff0eb17895e3394dfeb139b3036165105240) Improve exports to handle all the different ways developers will want to use VexFlow: import / require / script. See: Gruntfile.js and package.json

[fafffbe5316ea551f232197cf670bca20fa585a1](https://github.com/0xfe/vexflow/commit/fafffbe5316ea551f232197cf670bca20fa585a1) Don't use namespace. Instead, just have static variables for Renderer.Backends and Renderer.LineEndType.

[caa9a10ec26dc54e07deea44b255031bd48f861e](https://github.com/0xfe/vexflow/commit/caa9a10ec26dc54e07deea44b255031bd48f861e) Improve backwards compatibility with 3.0.9 (e.g., in flow.html). Add new methods to help with migrating VexTab to VexFlow 4.0.0. Improve the build process.

[1496d1b9c83189a0b9cf24365dfd1d609cbe432f](https://github.com/0xfe/vexflow/commit/1496d1b9c83189a0b9cf24365dfd1d609cbe432f) Fix grunt watch with correct use of the webpack `ignored` field.

[eaac5851e837d23e321e2f7f31da239b1900b11b](https://github.com/0xfe/vexflow/commit/eaac5851e837d23e321e2f7f31da239b1900b11b) fix this.canvas type

[048f6be6e47976b82c7f8e13d3d854f306f2d403](https://github.com/0xfe/vexflow/commit/048f6be6e47976b82c7f8e13d3d854f306f2d403) Basic OffscreenCanvas support

[a48911f3c499363fa48963052cd0b1960d4215a5](https://github.com/0xfe/vexflow/commit/a48911f3c499363fa48963052cd0b1960d4215a5) Remove tsconfig-paths-webpack-plugin because we no longer use paths field in tsconfig.json.

[6f526b38efa90314266f89cc5e5384196d80a808](https://github.com/0xfe/vexflow/commit/6f526b38efa90314266f89cc5e5384196d80a808) Move Bounds interface to the BoundingBox source file.

[00cd284ea7c9ddc3964dc38489d47c62eb876c11](https://github.com/0xfe/vexflow/commit/00cd284ea7c9ddc3964dc38489d47c62eb876c11) Fix typedoc warnings and name collisions with HorizontalJustify and VerticalJustify enums.

[47a91de6814dd01908caea45b47b99243836bfbf](https://github.com/0xfe/vexflow/commit/47a91de6814dd01908caea45b47b99243836bfbf) Merge remote-tracking branch 'origin/master' into 4.0.0-alpha

[b10b36a25f8842f6dc356c6a377b9edf111e0b24](https://github.com/0xfe/vexflow/commit/b10b36a25f8842f6dc356c6a377b9edf111e0b24) Fix rebase issues. Run eslint / prettier on qunit files to support easier tweaking in the future.

[1f0a942de67124a192ae792db2d8409e8bd0eec0](https://github.com/0xfe/vexflow/commit/1f0a942de67124a192ae792db2d8409e8bd0eec0) Fix export of Vex.

[608414f4bfed15b6f6a0b6c2e0193485ae98211d](https://github.com/0xfe/vexflow/commit/608414f4bfed15b6f6a0b6c2e0193485ae98211d) Improve build process. Update demos. Fix capitalization. Fix README. eslint autofix markdown and JS.

[22f5c19755e2189da4c3a49b082b4fa84973b7a3](https://github.com/0xfe/vexflow/commit/22f5c19755e2189da4c3a49b082b4fa84973b7a3) Partial merge of branch 'master' into setFont. Includes relative path imports for test files from: https://github.com/0xfe/vexflow/pull/1209/

[a5784320cfa617edb822d9e531c52c89ca556eed](https://github.com/0xfe/vexflow/commit/a5784320cfa617edb822d9e531c52c89ca556eed) Use the package.json exports field to handle different VexFlow bundles. https://webpack.js.org/guides/package-exports/

[70e63930bbe4b00c463af102437a3eee7c50f03e](https://github.com/0xfe/vexflow/commit/70e63930bbe4b00c463af102437a3eee7c50f03e) Only include the build/ folder in the npm package.

[d59389613638f5c75ec89e4e680f1cf70e8ff87b](https://github.com/0xfe/vexflow/commit/d59389613638f5c75ec89e4e680f1cf70e8ff87b) Separate the setFont (all arguments undefined) into its own case, to support older TS compilers that complain about object spread with undefined.

[66efdf0786570c8006ac2c89351895e989142b16](https://github.com/0xfe/vexflow/commit/66efdf0786570c8006ac2c89351895e989142b16) Disable FontFace warnings to support distributions without the FontFace declarations. Fix eslint warnings.

[fe8d177a2ca67491fbaeb64125650365c5faf967](https://github.com/0xfe/vexflow/commit/fe8d177a2ca67491fbaeb64125650365c5faf967) Improve web font hosting approach in response to code review.

[d4a0113eec192caa8526fecd241ac0b420f2e2ee](https://github.com/0xfe/vexflow/commit/d4a0113eec192caa8526fecd241ac0b420f2e2ee) Zero visual diffs.

[69a37ee4bdd350caad4580b187c68d1cd334ac38](https://github.com/0xfe/vexflow/commit/69a37ee4bdd350caad4580b187c68d1cd334ac38) Clean up fontgen_xxx.js scripts. Make them use Prettier to format the JSON output.

[a08b73b6da0f8e282e0075cd561c23acff81f2e4](https://github.com/0xfe/vexflow/commit/a08b73b6da0f8e282e0075cd561c23acff81f2e4) Consolidate the setFont(...) API and handle edge cases. Add .font setter/getter to Element and rename internal instance member to `textFont`. Add test code for setFont() in tests/font_tests.ts. Other smaller fixes.

[f87c95ac0edfe3499abc124ca7de85a4821bf442](https://github.com/0xfe/vexflow/commit/f87c95ac0edfe3499abc124ca7de85a4821bf442) Use FontWeight / FontStyle constants more consistently. Improve OTF glyph inspector (Gonville font). Fix demos. Discovered a potential API stumbling block by writing tests.

[2e05120755776082a8b17a824497cafdf6e5a096](https://github.com/0xfe/vexflow/commit/2e05120755776082a8b17a824497cafdf6e5a096) Improve glyph inspector. - Support all fonts. - Support both OTF and extracted outlines. Add more documentation. Other small fixes.

[628aa690e023e699717a5085b8e3e9d647e48a57](https://github.com/0xfe/vexflow/commit/628aa690e023e699717a5085b8e3e9d647e48a57) Improve API for Flow and Tables. Fix visual diff in textbracket_tests.ts. More clean up.

[b22a45bbb5b3369087581bbfd38d3bd657509a4e](https://github.com/0xfe/vexflow/commit/b22a45bbb5b3369087581bbfd38d3bd657509a4e) Use the global font stack instead of the Element's local font stack. Use a precomputed string as a key for the glyph cache. Move new glyph inspector and legacy font tools to tools/fonts/. Update CHANGELOG.

[f79be12f85f2e82c69d95afffe8ab9683f60fa9f](https://github.com/0xfe/vexflow/commit/f79be12f85f2e82c69d95afffe8ab9683f60fa9f) Merge pull request #1213 from rvilarl/migration/eslintUpdate

[7c9ad363687d87762ed199ee5593fd85003c81d5](https://github.com/0xfe/vexflow/commit/7c9ad363687d87762ed199ee5593fd85003c81d5) Simple glyph inspector for Bravura/Petaluma. Update the legacy glyphs.html and transform.html.

[7e0d11c97052452be16b079aa75398edebd693c4](https://github.com/0xfe/vexflow/commit/7e0d11c97052452be16b079aa75398edebd693c4) Lazy loading of fonts only works when globalObject is not defined. Move OTF files. Bump vexflow-fonts. Clean up font scripts.

[b68c7c260424a873911005153a559947e1887e45](https://github.com/0xfe/vexflow/commit/b68c7c260424a873911005153a559947e1887e45) Reorganize fonts in the tools/ folder. Attempt to read/write OTF files. Cannot currently convert to WOFF. Continue to rely on FontSquirrel for now. Use the FontSquirrel version of PetalumaScript for better kerning. Add information on how to convert the OTF to WOFF via FontSquirrel.

[6ad76d4d55cbeb92d547d0d0fc2fe23b5f3af2ee](https://github.com/0xfe/vexflow/commit/6ad76d4d55cbeb92d547d0d0fc2fe23b5f3af2ee) Rename TextFont to TextFormatter. Rename TextFontTests to FontTests. Remove unused code.

[978ed448db173926115966daa713677140cf367e](https://github.com/0xfe/vexflow/commit/978ed448db173926115966daa713677140cf367e) Move general font methods into Font class. Methods remaining in TextFont deal with formatting / metrics. TextFont will be renamed to TextFormatter.

[2d400a54bab9a12c6c1bfe5efc7163fc4b326d9f](https://github.com/0xfe/vexflow/commit/2d400a54bab9a12c6c1bfe5efc7163fc4b326d9f) Add an element ID to the title div of test cases on flow.html. This allows us to use fragment identifiers to scroll directly to a test case (by using the name of the PNG file generated by our visual regression tests).

[9c7820418c3092c714e5f75cafaf3d61b9efcd2e](https://github.com/0xfe/vexflow/commit/9c7820418c3092c714e5f75cafaf3d61b9efcd2e) Add Gonville web fonts.

[e7e0c3577222dc90b2371c0233e706e008b88e81](https://github.com/0xfe/vexflow/commit/e7e0c3577222dc90b2371c0233e706e008b88e81) Clean up ChordSymbol. Improve how we handle default static TEXT_FONT. Factory.Annotation(params) now takes a FontInfo object. Note: Factory.Annotation() has a different default font than new Annotation(). Rename this.textFont to this.textFormatter.

[dffd1f3127ebaca2a0149517ddd18ade4543691f](https://github.com/0xfe/vexflow/commit/dffd1f3127ebaca2a0149517ddd18ade4543691f) eslintrc config updated

[10d7573392faead8bf7cc0a1637e82c2a23ff544](https://github.com/0xfe/vexflow/commit/10d7573392faead8bf7cc0a1637e82c2a23ff544) Load Roboto Slab and PetalumaScript with the FontFace API before running VexFlow tests. This fixes the test case: ChordSymbol › Chord Symbol Font Size Tests › Canvas + Bravura

[08134cb19e847d0d50878b2f85568519bd976347](https://github.com/0xfe/vexflow/commit/08134cb19e847d0d50878b2f85568519bd976347) Consolidate setFont(). Improve text font support. Improve naming to differentiate between text fonts and music fonts (for engraving). Remove DEFAULT_ prefix. Use Font.SERIF and Font.SANS_SERIF instead of 'Times' and 'Arial'. Rename getFontStack().

[5113a69bef0791f3068e7326a4b624a063bdde9f](https://github.com/0xfe/vexflow/commit/5113a69bef0791f3068e7326a4b624a063bdde9f) Merge pull request #1212 from ronyeh/font/glyphs-and-metrics-files

[f53771160d67d93ac567300f6dbb21483d3a7cc2](https://github.com/0xfe/vexflow/commit/f53771160d67d93ac567300f6dbb21483d3a7cc2) Run prettier / eslint on the font data files, to improve consistency and editability of the files.

[365e81ef839fce8ab7f1c7a8f325bbc0259ab7b7](https://github.com/0xfe/vexflow/commit/365e81ef839fce8ab7f1c7a8f325bbc0259ab7b7) Merge pull request #1209 from rvilarl/migration/4.0

[fe20e5b9ff13189b94d675329755ec91339bf214](https://github.com/0xfe/vexflow/commit/fe20e5b9ff13189b94d675329755ec91339bf214) Merge pull request #1205 from ronyeh/build

[18ee0ad02d06c8a3e5a9b050213824d9e62399a0](https://github.com/0xfe/vexflow/commit/18ee0ad02d06c8a3e5a9b050213824d9e62399a0) Update exclude path for legacy fonts.

[bdd4bbbdc23bc8a9febcb41cece4d73ede185ff5](https://github.com/0xfe/vexflow/commit/bdd4bbbdc23bc8a9febcb41cece4d73ede185ff5) Add flow-headless-browser.html to allow the qunit grunt task     to run a streamlined vexflow-tests.js. The full flow.html will     include things like async loading of web fonts, etc. Generate .d.ts files. Gruntfile improvements to allow for dynamic font loading. Delete jQuery file. Update glyphs.html to not require jQuery.

[79b46c0e99a6470543325d12b18718cbfe65e7de](https://github.com/0xfe/vexflow/commit/79b46c0e99a6470543325d12b18718cbfe65e7de) paths included in imports, eslint warnings fixed

[646318c5bb2ed8289c696b2833fca2018703a75e](https://github.com/0xfe/vexflow/commit/646318c5bb2ed8289c696b2833fca2018703a75e) Merge pull request #1206 from rvilarl/setFontMinor

[cb917769b3c23709b97f9a5b61cba9eaa8012016](https://github.com/0xfe/vexflow/commit/cb917769b3c23709b97f9a5b61cba9eaa8012016) Merge pull request #1208 from AaronDavidNewman/tables_key_properties_export

[8e78d82546ac258d5585cb978ddcdeb9da5e7515](https://github.com/0xfe/vexflow/commit/8e78d82546ac258d5585cb978ddcdeb9da5e7515) Merge pull request #1202 from ronyeh/tools

[a1bc011860545a7cf3eb444feecf062e97d69164](https://github.com/0xfe/vexflow/commit/a1bc011860545a7cf3eb444feecf062e97d69164) Merge pull request #1198 from rvilarl/fix/489

[55f2df24f4d3e79dec293a4533de8ac3c628ef49](https://github.com/0xfe/vexflow/commit/55f2df24f4d3e79dec293a4533de8ac3c628ef49) lint any

[0098150dbc28cb153f05eb25107bd49993a70a6a](https://github.com/0xfe/vexflow/commit/0098150dbc28cb153f05eb25107bd49993a70a6a) add some missing exports

[0d01c5ab37b046613a4396f0fa6fe454c5aa44d8](https://github.com/0xfe/vexflow/commit/0d01c5ab37b046613a4396f0fa6fe454c5aa44d8) additional testing without start/end note

[fa126cb391a0308b607f5665af7390b022c60db0](https://github.com/0xfe/vexflow/commit/fa126cb391a0308b607f5665af7390b022c60db0) fix getTieEndX

[7f5004a673248e15cd670f55d92948f810f66af0](https://github.com/0xfe/vexflow/commit/7f5004a673248e15cd670f55d92948f810f66af0) Merge pull request #1204 from AaronDavidNewman/petaluma_test_cases

[9136b5c4f3a9028201e866aff2a05661de15305d](https://github.com/0xfe/vexflow/commit/9136b5c4f3a9028201e866aff2a05661de15305d) Merge pull request #1201 from ronyeh/context2D

[13d82441d19275e659ee374644d5aa3d39717181](https://github.com/0xfe/vexflow/commit/13d82441d19275e659ee374644d5aa3d39717181) Merge pull request #1197 from AaronDavidNewman/master

[ece47b8872c3ddfc79989f5677132f473b6100bb](https://github.com/0xfe/vexflow/commit/ece47b8872c3ddfc79989f5677132f473b6100bb) Merge pull request #1203 from rvilarl/typo

[6e28ebba2a63e9e230484a4d5c1673e47e298772](https://github.com/0xfe/vexflow/commit/6e28ebba2a63e9e230484a4d5c1673e47e298772) Merge pull request #1193 from rvilarl/fix/ts-nocheck

[1e988740f06294632b4efbb15a13364056531f9a](https://github.com/0xfe/vexflow/commit/1e988740f06294632b4efbb15a13364056531f9a) Merge pull request #1191 from h-sug1no/parallel-generate-image-1

[cf0adffd3232edaca1d67e62ee3640db5d22f8de](https://github.com/0xfe/vexflow/commit/cf0adffd3232edaca1d67e62ee3640db5d22f8de) minor changes(Tables, Font)

[be8cf29972946af89bcec70fc352d68ae83757c0](https://github.com/0xfe/vexflow/commit/be8cf29972946af89bcec70fc352d68ae83757c0) remove unused 'score'

[8218a99966c35297008b58c015cacfb2fb98f7c4](https://github.com/0xfe/vexflow/commit/8218a99966c35297008b58c015cacfb2fb98f7c4) Merge https://github.com/0xfe/vexflow into petaluma_test_cases

[b82f633db3b16891ea09f5037864fdfb79fa9466](https://github.com/0xfe/vexflow/commit/b82f633db3b16891ea09f5037864fdfb79fa9466) Move formatter tests back to the original order

[f0d107c7fbc9dd2cec38ea0f09931b9829fe8b1d](https://github.com/0xfe/vexflow/commit/f0d107c7fbc9dd2cec38ea0f09931b9829fe8b1d) small fixes to stavenote and stringnumber

[a73a198444bff99959e4b787892a0919d82070d0](https://github.com/0xfe/vexflow/commit/a73a198444bff99959e4b787892a0919d82070d0) fix notehead tests and ornament test overflows

[3e04ad9e446cffa06f2050e0e7a9e225ed74cb98](https://github.com/0xfe/vexflow/commit/3e04ad9e446cffa06f2050e0e7a9e225ed74cb98) Fix overflowing key signature tests

[6eb7cdd9b9499497f7c40ba7f8f6e271701bc2cb](https://github.com/0xfe/vexflow/commit/6eb7cdd9b9499497f7c40ba7f8f6e271701bc2cb) minor changes

[242f1e06a8d15a8d261232a436426642d0739974](https://github.com/0xfe/vexflow/commit/242f1e06a8d15a8d261232a436426642d0739974) ts-ignore no longer required

[f70118e0ed06f4d06c1288f921dda3ae685d5e54](https://github.com/0xfe/vexflow/commit/f70118e0ed06f4d06c1288f921dda3ae685d5e54) imports sorted by eslint

[007649174ba5a326cc9c815d848c0704b9309fda](https://github.com/0xfe/vexflow/commit/007649174ba5a326cc9c815d848c0704b9309fda) rebase fixed

[0b4bf52a098662a250676766ecaa45bc2918dc29](https://github.com/0xfe/vexflow/commit/0b4bf52a098662a250676766ecaa45bc2918dc29) ts-nocheck resolved

[268a231bbb114ef2f6a5a43f8320a75f86e44cee](https://github.com/0xfe/vexflow/commit/268a231bbb114ef2f6a5a43f8320a75f86e44cee) SetStave typo fixed

[22190f9966c4b13fa50621abe6b5f3cc254ee43d](https://github.com/0xfe/vexflow/commit/22190f9966c4b13fa50621abe6b5f3cc254ee43d) Merge pull request #1195 from rvilarl/eslint-plugin-simple-import-sort

[3d9f6f111148bf58995c3e313af0ae17b98ddb1c](https://github.com/0xfe/vexflow/commit/3d9f6f111148bf58995c3e313af0ae17b98ddb1c) Merge pull request #1199 from rvilarl/fix/531

[d0220d2cefa8d392424e37c8882e5c982600184b](https://github.com/0xfe/vexflow/commit/d0220d2cefa8d392424e37c8882e5c982600184b) Merge pull request #1196 from rvilarl/fix/1189

[db254a43b00f751d9d8c3f38c4b303a69da7c550](https://github.com/0xfe/vexflow/commit/db254a43b00f751d9d8c3f38c4b303a69da7c550) Fix some overflow issues in test cases

[17d65d8702fafd3b76e3b51e33d4eadb524bb5cf](https://github.com/0xfe/vexflow/commit/17d65d8702fafd3b76e3b51e33d4eadb524bb5cf) Add `tools/fonts/@/` which is a separate NPM package called `vexflow-fonts`. This is used for hosting web font files that can be used with VexFlow 4.0. The font files are served via CDNs: - https://unpkg.com/browse/vexflow-fonts@1.0.3/ - https://cdn.jsdelivr.net/npm/vexflow-fonts@1.0.3/ It is a separate package so that we can update/fix font files without having to publish a new `vexflow` update to NPM.

[26a282342583ea9614696ba81337003ed77be9f8](https://github.com/0xfe/vexflow/commit/26a282342583ea9614696ba81337003ed77be9f8) Treat OTF and WOFF/WOFF2 font files as binary. Prevent git from corrupting our font files.

[072d78c6eded01f677f3cf2aefbad89afcb0120b](https://github.com/0xfe/vexflow/commit/072d78c6eded01f677f3cf2aefbad89afcb0120b) Rename vexFlowCanvasContext to context2D. Other smaller fixes.

[58da4fb9017866c3d56d78d33c7c718b72fbf8e7](https://github.com/0xfe/vexflow/commit/58da4fb9017866c3d56d78d33c7c718b72fbf8e7) npm-upgrade

[8d5a6880b235a7abfbecf7afae38eaee595519e9](https://github.com/0xfe/vexflow/commit/8d5a6880b235a7abfbecf7afae38eaee595519e9) remove empty line.

[45b9572763afe8000c3ea0938a126b324d5d097b](https://github.com/0xfe/vexflow/commit/45b9572763afe8000c3ea0938a126b324d5d097b) To improve symbol placement, use 10 (normal spacingBetweenLines)　as the default value for symbol_spacing.

[f2372ce51a82c7452215862ccd06f98d4f6a13fb](https://github.com/0xfe/vexflow/commit/f2372ce51a82c7452215862ccd06f98d4f6a13fb) [WIP]: Disable the semibreve_rest cache to render MMRest based on the current system font.

[adfdad7a1871e7bfce5984842cb68eb3333207f2](https://github.com/0xfe/vexflow/commit/adfdad7a1871e7bfce5984842cb68eb3333207f2) Fix notehead attachment Petaluma font

[2d8449842e0608582dfcc4439a59a79776a684e3](https://github.com/0xfe/vexflow/commit/2d8449842e0608582dfcc4439a59a79776a684e3) Requirement to SetStave before rendering documented

[e2f53db9fd92aae7f5e8a065075040773e27d2af](https://github.com/0xfe/vexflow/commit/e2f53db9fd92aae7f5e8a065075040773e27d2af) [WIP]: npm run cache:*:reference: check src directory before move. - cache:restore:reference: generate images if cache does not exist.

[dcdce61d068e8fe6fbb0fd8bc2fb129cb98092a6](https://github.com/0xfe/vexflow/commit/dcdce61d068e8fe6fbb0fd8bc2fb129cb98092a6) [WIP]: add comment.

[47a2150800491b72b8a0f8c6c4f5131693c15609](https://github.com/0xfe/vexflow/commit/47a2150800491b72b8a0f8c6c4f5131693c15609) fix issues 555, 792

[e80e7ffb8ce4fd8c41be533ec8fb95a1dbc2fbb6](https://github.com/0xfe/vexflow/commit/e80e7ffb8ce4fd8c41be533ec8fb95a1dbc2fbb6) bug resolved

[fc6c22c1519652804a278417dd63ee5cb751313f](https://github.com/0xfe/vexflow/commit/fc6c22c1519652804a278417dd63ee5cb751313f) eslint sort imports plugin

[725aa3327f11d5cd11c0ddaa099375f709d92874](https://github.com/0xfe/vexflow/commit/725aa3327f11d5cd11c0ddaa099375f709d92874) Merge pull request #1185 from rvilarl/fix/1172

[e3d9f14af80882f3a1139ed9aa798dffabecb1ec](https://github.com/0xfe/vexflow/commit/e3d9f14af80882f3a1139ed9aa798dffabecb1ec) Merge pull request #1192 from rvilarl/fix/1189

[a9b7c79591f4af36a88e37ff1ac214f5764a5297](https://github.com/0xfe/vexflow/commit/a9b7c79591f4af36a88e37ff1ac214f5764a5297) group stave

[de2e7f595819d709ad4847b1c40a6ee3936502b8](https://github.com/0xfe/vexflow/commit/de2e7f595819d709ad4847b1c40a6ee3936502b8) group clef

[a62158d50ae66f5b3d82a39694a217f988ec575f](https://github.com/0xfe/vexflow/commit/a62158d50ae66f5b3d82a39694a217f988ec575f) group timesignature

[f0ee1d97557afa26d52426c3c48c66f333a4e261](https://github.com/0xfe/vexflow/commit/f0ee1d97557afa26d52426c3c48c66f333a4e261) group keysignature

[fdd4749b708c49812e6bb2c44d9ca742b5593049](https://github.com/0xfe/vexflow/commit/fdd4749b708c49812e6bb2c44d9ca742b5593049) fix rebase

[31a6fd4fa61177b46deb9098fec9c3b8203891ee](https://github.com/0xfe/vexflow/commit/31a6fd4fa61177b46deb9098fec9c3b8203891ee) review comment

[f8a62fe66e6270f43ad650825a394ef7be40db06](https://github.com/0xfe/vexflow/commit/f8a62fe66e6270f43ad650825a394ef7be40db06) common.d.ts Note circular dependency resolved

[1a910280b12ed4a0fb91db728a5122ccc501b70b](https://github.com/0xfe/vexflow/commit/1a910280b12ed4a0fb91db728a5122ccc501b70b) Tables/Flow circular dependencies resolved

[95b7230a0f25f0a33448d2f3b0e2476fe0fd31c4](https://github.com/0xfe/vexflow/commit/95b7230a0f25f0a33448d2f3b0e2476fe0fd31c4) Merge pull request #1175 from AaronDavidNewman/master

[be92cd8222172af6fe9245968072bf9b04e1e58b](https://github.com/0xfe/vexflow/commit/be92cd8222172af6fe9245968072bf9b04e1e58b) - add VF_GENERATE_OPTIONS environment variable to specify options to `npm run generate*` - add `npm run test:reference:cache` to re-use generated `reference` test images.

[2845249935c3160770e3003f0d8cb469a4db4533](https://github.com/0xfe/vexflow/commit/2845249935c3160770e3003f0d8cb469a4db4533) [WIP]: add some options: - --parallel[=<jobs> : exec processes in parallel for each font. - --backcompat : generate test results for Bravura fonts with old-style file names.

[0fd60fd5308ab17724d94fe6f5f81366dbc4aa8f](https://github.com/0xfe/vexflow/commit/0fd60fd5308ab17724d94fe6f5f81366dbc4aa8f) [WIP]: Test the difference with cmp first to reduce the number of 'compare' command calls.

[8c6093ebba259123aeac38216e851eb1219072d1](https://github.com/0xfe/vexflow/commit/8c6093ebba259123aeac38216e851eb1219072d1) more code review comments

[9f84f36fdd537750024615f57b6cbd94777895ba](https://github.com/0xfe/vexflow/commit/9f84f36fdd537750024615f57b6cbd94777895ba) Merge pull request #1184 from rvilarl/fix/1070

[90f5d3d876b93cb1694d1c0a388f7a6d85754e79](https://github.com/0xfe/vexflow/commit/90f5d3d876b93cb1694d1c0a388f7a6d85754e79) Merge https://github.com/0xfe/vexflow

[9de95e55b39a049ea025d43bd4dcd255b105e65c](https://github.com/0xfe/vexflow/commit/9de95e55b39a049ea025d43bd4dcd255b105e65c) render_options accessesors removed

[93d80e1b3a54defb5c308ae69dd7cac394efa645](https://github.com/0xfe/vexflow/commit/93d80e1b3a54defb5c308ae69dd7cac394efa645) public render_options

[c8dcc183c6a32e58ddba4a06ffd2db7a41bd16fa](https://github.com/0xfe/vexflow/commit/c8dcc183c6a32e58ddba4a06ffd2db7a41bd16fa) render_options -> renderOptions

[90908785ad20dfd4cc55bb53c49bfbe66d50ee5e](https://github.com/0xfe/vexflow/commit/90908785ad20dfd4cc55bb53c49bfbe66d50ee5e) render_options protected

[ca9c6b75a11d19c6bdec928d55d75ed447868b49](https://github.com/0xfe/vexflow/commit/ca9c6b75a11d19c6bdec928d55d75ed447868b49) Merge pull request #1186 from rvilarl/tests/tremolo

[f526c2c73eef5da30399e59233b2997e8d8cef34](https://github.com/0xfe/vexflow/commit/f526c2c73eef5da30399e59233b2997e8d8cef34) moar code review comments

[8b7f7bcaf515db80fb9f8aebe9d65008607ba96e](https://github.com/0xfe/vexflow/commit/8b7f7bcaf515db80fb9f8aebe9d65008607ba96e) Merge https://github.com/0xfe/vexflow

[80c0d489b69e21dfb6164fe34b4c92a1a8369f3b](https://github.com/0xfe/vexflow/commit/80c0d489b69e21dfb6164fe34b4c92a1a8369f3b) tremolo tests added

[9b4a3419476cd3836256f2d29c46504b0b9da430](https://github.com/0xfe/vexflow/commit/9b4a3419476cd3836256f2d29c46504b0b9da430) Merge pull request #1183 from tommadams/abc

[47fc8d9c3312c2a632358fe7552da5163e8c392a](https://github.com/0xfe/vexflow/commit/47fc8d9c3312c2a632358fe7552da5163e8c392a) fix broken test

[a4920f128ff65f683da029d76feb8a6919eb1bf4](https://github.com/0xfe/vexflow/commit/a4920f128ff65f683da029d76feb8a6919eb1bf4) move RenderContext into its own module

[7117c7666884f4598d54aa8a61463aa00993439f](https://github.com/0xfe/vexflow/commit/7117c7666884f4598d54aa8a61463aa00993439f) make RenderContext an abstract base class

[1690990e0d5a9eff3c00465cf7cd276538b3dde9](https://github.com/0xfe/vexflow/commit/1690990e0d5a9eff3c00465cf7cd276538b3dde9) Merge pull request #1181 from rvilarl/migration/legacy

[d224ea5b75306d1de1da917e20ffda5444e45a58](https://github.com/0xfe/vexflow/commit/d224ea5b75306d1de1da917e20ffda5444e45a58) Merge pull request #1161 from tommadams/renderer

[0dea4ab4bc6e64c96b7af6a15e0820adb857386d](https://github.com/0xfe/vexflow/commit/0dea4ab4bc6e64c96b7af6a15e0820adb857386d) Merge pull request #1170 from rvilarl/fix/1169

[7854d72920eee6841a2186fa62d1f1e14d3e7c25](https://github.com/0xfe/vexflow/commit/7854d72920eee6841a2186fa62d1f1e14d3e7c25) exclude legacy fonts path

[ff5fb4349952c88da6181177544413bf6eea6cb5](https://github.com/0xfe/vexflow/commit/ff5fb4349952c88da6181177544413bf6eea6cb5) update for code review

[5ee860bb9f35cd5980183de79087067dfaa64dcd](https://github.com/0xfe/vexflow/commit/5ee860bb9f35cd5980183de79087067dfaa64dcd) legacy fonts migrated

[2b473c8221ed8bf7dc873d9a739664a937e66b1f](https://github.com/0xfe/vexflow/commit/2b473c8221ed8bf7dc873d9a739664a937e66b1f) address review comments and add custom RenderContext demo

[e8b960943eecd5b28422d047bceb4dd00990ae24](https://github.com/0xfe/vexflow/commit/e8b960943eecd5b28422d047bceb4dd00990ae24) Merge https://github.com/0xfe/vexflow

[f48bde41b4e1f36ac8f82ec5e9c4675c7d80e7e7](https://github.com/0xfe/vexflow/commit/f48bde41b4e1f36ac8f82ec5e9c4675c7d80e7e7) Merge pull request #1178 from ronyeh/fix/svg-arc

[0528bc25263285d9644b9542041bae90d7be6d53](https://github.com/0xfe/vexflow/commit/0528bc25263285d9644b9542041bae90d7be6d53) Add equal signs to handle the case where the arc is exactly a circle (TWO_PI radians).

[f9c71ad0e43f0ed86674b396965013649437d563](https://github.com/0xfe/vexflow/commit/f9c71ad0e43f0ed86674b396965013649437d563) fixes #1167

[85e6be68874ec32eed1c7b1db26c1f340bf828ad](https://github.com/0xfe/vexflow/commit/85e6be68874ec32eed1c7b1db26c1f340bf828ad) Merge https://github.com/0xfe/vexflow

[57f0f39468ebece8aeeeb8c1f9ccf5e30b1420c1](https://github.com/0xfe/vexflow/commit/57f0f39468ebece8aeeeb8c1f9ccf5e30b1420c1) automatic accidentals corner cases tests

[6a56fe5367c5a14b0958c99f5f27757ab803f1f2](https://github.com/0xfe/vexflow/commit/6a56fe5367c5a14b0958c99f5f27757ab803f1f2) fix #1169 applyAccidentals

[11db474eb281d7bd1efd675d8c5e4a8762db8250](https://github.com/0xfe/vexflow/commit/11db474eb281d7bd1efd675d8c5e4a8762db8250) Merge pull request #1173 from rvilarl/fix/1162

[7bf73ee1ac790d04d7f3074daac0370e06c232cf](https://github.com/0xfe/vexflow/commit/7bf73ee1ac790d04d7f3074daac0370e06c232cf) Merge pull request #1174 from rvilarl/fix/1124

[a88210b00efe6675a6a843ee0188524598a25be1](https://github.com/0xfe/vexflow/commit/a88210b00efe6675a6a843ee0188524598a25be1) Address issue 1167

[67cf72046ef73d01d1224efb8957ab1eca138e30](https://github.com/0xfe/vexflow/commit/67cf72046ef73d01d1224efb8957ab1eca138e30) remove unused imports

[b8192436d3ca52ef4a8fca1f45a4e15e0a895fcf](https://github.com/0xfe/vexflow/commit/b8192436d3ca52ef4a8fca1f45a4e15e0a895fcf) index instead of n

[37d59387f3a6588ed92472852303a05ee9baf331](https://github.com/0xfe/vexflow/commit/37d59387f3a6588ed92472852303a05ee9baf331) Merge branch 'master' of github.com:tommadams/vexflow into renderer

[781ab4ce70f05d2516730ccbaec4003fae73e26c](https://github.com/0xfe/vexflow/commit/781ab4ce70f05d2516730ccbaec4003fae73e26c) remove this.x check, cannot be undefined

[9497718faa0f0dfb7c4e796d954197b1debc2e54](https://github.com/0xfe/vexflow/commit/9497718faa0f0dfb7c4e796d954197b1debc2e54) TODO resolved

[1e46ddafb89c8c960408a2f35771b679453a26ad](https://github.com/0xfe/vexflow/commit/1e46ddafb89c8c960408a2f35771b679453a26ad) Merge pull request #1168 from rvilarl/fix/1156

[fa0f97fd46da622237a1df4074bbc4e2e786f7e2](https://github.com/0xfe/vexflow/commit/fa0f97fd46da622237a1df4074bbc4e2e786f7e2) Merge pull request #1171 from rvilarl/fix/castingStaveNote

[11013ddf32bc72f028eed65b906b3fcf26b007d7](https://github.com/0xfe/vexflow/commit/11013ddf32bc72f028eed65b906b3fcf26b007d7) remove StaveNote casting

[eeeaf4145e0f1b85212f59431290821c35226af2](https://github.com/0xfe/vexflow/commit/eeeaf4145e0f1b85212f59431290821c35226af2) remove drawVetical from Stave

[961f26aca6e1ad5244382925d2ece1d8d1837a09](https://github.com/0xfe/vexflow/commit/961f26aca6e1ad5244382925d2ece1d8d1837a09) Merge pull request #1148 from ronyeh/fix/noteStructs2

[55a55fddfd588c64068411fbcb8fe93c5778ecc8](https://github.com/0xfe/vexflow/commit/55a55fddfd588c64068411fbcb8fe93c5778ecc8) Merge pull request #1145 from tommadams/fillRect

[3f7d02fc3792939d977f7b91724f93b80397549e](https://github.com/0xfe/vexflow/commit/3f7d02fc3792939d977f7b91724f93b80397549e) Remove getOptions() from Stave and Factory. Use direct accessors. As suggested by: https://github.com/0xfe/vexflow/pull/1148#discussion_r717134986

[6a1304f3ba27643b0e158cfed902388d66f7a79f](https://github.com/0xfe/vexflow/commit/6a1304f3ba27643b0e158cfed902388d66f7a79f) Code Review Comments. Clean up ChordSymbol. Update CHANGELOG.

[05ad13c50783782628acfa01923f21b366117a02](https://github.com/0xfe/vexflow/commit/05ad13c50783782628acfa01923f21b366117a02) Remove Partial. Add Required. Fixes for Factory, Renderer, System.

[4bf07751e32451f64a34d4a718aa0ca849965e9b](https://github.com/0xfe/vexflow/commit/4bf07751e32451f64a34d4a718aa0ca849965e9b) Remove Partials from RepeatNote, StemmableNote, TabStave.

[ec40c493bcc262784be28467efeb4cee2ff90577](https://github.com/0xfe/vexflow/commit/ec40c493bcc262784be28467efeb4cee2ff90577) Remove Partial from Formatter and others.

[d20286f467d1ae316ad0db4bc205d9dd5f79d17f](https://github.com/0xfe/vexflow/commit/d20286f467d1ae316ad0db4bc205d9dd5f79d17f) Remove Partial from EasyScore.

[67bb570a408870d545957921fa998eb3980f00d4](https://github.com/0xfe/vexflow/commit/67bb570a408870d545957921fa998eb3980f00d4) Remove Partial from Voice.

[13a143f24e02e10b6bb80e5e5ffa7e17db88ee3f](https://github.com/0xfe/vexflow/commit/13a143f24e02e10b6bb80e5e5ffa7e17db88ee3f) Add Required to MultiMeasureRest.

[7e817f70dcbe9bbe29cc36c6b19d18a5998c18e7](https://github.com/0xfe/vexflow/commit/7e817f70dcbe9bbe29cc36c6b19d18a5998c18e7) Add Required to Factory. Handle null elementId.

[15670b1fff28f2ae8b8a9f9eed39fa085dbfbb2f](https://github.com/0xfe/vexflow/commit/15670b1fff28f2ae8b8a9f9eed39fa085dbfbb2f) Remove Partial from Curve.

[7d633c96286ea5d2974074baffc9988d5732c721](https://github.com/0xfe/vexflow/commit/7d633c96286ea5d2974074baffc9988d5732c721) Remove some Partial<...> and prefer using ? instead. Cast some fields "as number" for now. More to come in a future PR.

[f3553d32b0bce29feb09c7a9aefbdad298f38f0f](https://github.com/0xfe/vexflow/commit/f3553d32b0bce29feb09c7a9aefbdad298f38f0f) stave tests TODOs resolved

[3c0d9a43d08d3a523456de1bda9e67de02170fb4](https://github.com/0xfe/vexflow/commit/3c0d9a43d08d3a523456de1bda9e67de02170fb4) this.note_head removed

[6cfc617cb64ff66fc9bac8ab651a842b00958632](https://github.com/0xfe/vexflow/commit/6cfc617cb64ff66fc9bac8ab651a842b00958632) nullish approch on parameters

[0593f45cd8bb381f3f5becca9369a42e040dc5ec](https://github.com/0xfe/vexflow/commit/0593f45cd8bb381f3f5becca9369a42e040dc5ec) parameters TODO resolved

[c3223c79abf15b8e2d4c6dea2405a5db4c220d14](https://github.com/0xfe/vexflow/commit/c3223c79abf15b8e2d4c6dea2405a5db4c220d14) Notes constructor should take a Partial<...>

[9043e135944bdb78d83223a150603d14d91cd02d](https://github.com/0xfe/vexflow/commit/9043e135944bdb78d83223a150603d14d91cd02d) use window.HTMLCanvasElement so code works under node.js

[3ae2c72a258d6b971f4f65f578b079c4961568c6](https://github.com/0xfe/vexflow/commit/3ae2c72a258d6b971f4f65f578b079c4961568c6) add renderer test

[758a039d94a0e0c7d2a6b5b3f2ce78c0748bfdda](https://github.com/0xfe/vexflow/commit/758a039d94a0e0c7d2a6b5b3f2ce78c0748bfdda) allow render contexts to be passed directly to the Renderer constructor

[660f488b33e71e8a3ff1484c448e2efeaddfc4fa](https://github.com/0xfe/vexflow/commit/660f488b33e71e8a3ff1484c448e2efeaddfc4fa) Merge pull request #1159 from h-sug1no/fix-typo_semibrave-to-semibreve

[8af0532be2a8312a2c28d44182b703a37dbcd8ed](https://github.com/0xfe/vexflow/commit/8af0532be2a8312a2c28d44182b703a37dbcd8ed) fix typo: semibrave to semibreve.

[52e3bc7f7ffe947e228467c42cf4a427c89264c4](https://github.com/0xfe/vexflow/commit/52e3bc7f7ffe947e228467c42cf4a427c89264c4) Merge pull request #1151 from ronyeh/fix/document-not-defined

[ea0e6abfb365555b59d9ed0ad32e207b4472c924](https://github.com/0xfe/vexflow/commit/ea0e6abfb365555b59d9ed0ad32e207b4472c924) Merge pull request #1153 from tommadams/moveTo

[436a948bc69822d35c050990a46d35120cee3ae2](https://github.com/0xfe/vexflow/commit/436a948bc69822d35c050990a46d35120cee3ae2) remove redundant moveTo in Glyph.renderOutline

[90c505686a2742d43d9f0e8e328ab1c99983cd32](https://github.com/0xfe/vexflow/commit/90c505686a2742d43d9f0e8e328ab1c99983cd32) Delay call to document.createElementNS() to support loading VexFlow in NodeJS with jsdom.

[44605d07e6fe27eed4f10c4ec94bfb0e9b12f692](https://github.com/0xfe/vexflow/commit/44605d07e6fe27eed4f10c4ec94bfb0e9b12f692) Merge pull request #1138 from ronyeh/category

[07301c10e8050729076f49c4085cc2a629f28375](https://github.com/0xfe/vexflow/commit/07301c10e8050729076f49c4085cc2a629f28375) Merge pull request #1142 from tommadams/arc

[56ba9407f517135969e9cdae4841eacd37efc709](https://github.com/0xfe/vexflow/commit/56ba9407f517135969e9cdae4841eacd37efc709) Use StaveModifierPosition directly. Use computed property names in the Stave's sort order options. Make 2nd param of setEndTimeSignature() optional to conform to tests. Small fixes to xxx_tests.ts.

[bc0aa76914c99bd90c94e166d2b1a0c102fef0be](https://github.com/0xfe/vexflow/commit/bc0aa76914c99bd90c94e166d2b1a0c102fef0be) don't stroke fillRect

[b1e957e78e388ca4c60dfebcc4376af5fbf01d25](https://github.com/0xfe/vexflow/commit/b1e957e78e388ca4c60dfebcc4376af5fbf01d25) Update CHANGELOG. Move static properties and methods up.

[d48f90eb7c45eaebb1bd12d1c26f75c698b8b1b7](https://github.com/0xfe/vexflow/commit/d48f90eb7c45eaebb1bd12d1c26f75c698b8b1b7) Move static members to the top of classes.

[59c5b2eb65ee6e04e91be1309340dd92ea2983b3](https://github.com/0xfe/vexflow/commit/59c5b2eb65ee6e04e91be1309340dd92ea2983b3) Remove Element constructor's parameter. The type is now pulled from this.getCategory().

[b39973ef8c9c0d8a72ebc1d999d338d02ebe8da2](https://github.com/0xfe/vexflow/commit/b39973ef8c9c0d8a72ebc1d999d338d02ebe8da2) Standardize CATEGORY / getCategory() / this.setAttribute('type', ...). Improve the typeguard functions to check for .CATEGORY property directly.

[658633fadb9cd8541ccf1dda2c0aa31bd94dea1e](https://github.com/0xfe/vexflow/commit/658633fadb9cd8541ccf1dda2c0aa31bd94dea1e) Merge branch 'arc' of github.com:tommadams/vexflow into arc

[b2409e7d3cf54c3b26ea688609fcb38192cd4c8c](https://github.com/0xfe/vexflow/commit/b2409e7d3cf54c3b26ea688609fcb38192cd4c8c) fix svgcontext.arc

[46e4cac2f4bc92a576f38b58f660a4e7d9ebaa98](https://github.com/0xfe/vexflow/commit/46e4cac2f4bc92a576f38b58f660a4e7d9ebaa98) Merge pull request #1144 from tommadams/ledgerLine

[ad316342dfb4095c6255e6b0abbe328138221bc2](https://github.com/0xfe/vexflow/commit/ad316342dfb4095c6255e6b0abbe328138221bc2) Merge pull request #1137 from tommadams/textMeasure

[e20ad59029f737e8eb2ca03b9a0165f1dc8b9613](https://github.com/0xfe/vexflow/commit/e20ad59029f737e8eb2ca03b9a0165f1dc8b9613) ledger line tweaks

[e4121c095a1cdff81a5e0cd3a04382383d98aa1a](https://github.com/0xfe/vexflow/commit/e4121c095a1cdff81a5e0cd3a04382383d98aa1a) fix svgcontext.arc

[b5bfca94cd614ebeb54aed151d22671ae570dcda](https://github.com/0xfe/vexflow/commit/b5bfca94cd614ebeb54aed151d22671ae570dcda) Merge pull request #1135 from rvilarl/refactor/tickContext

[8b34bb1eb7d1401c0276e39eef7a3063ac9d82f7](https://github.com/0xfe/vexflow/commit/8b34bb1eb7d1401c0276e39eef7a3063ac9d82f7) formatter metrics reduced to freedom

[07e32525efc9c5f088f552bc612d98c675f895b0](https://github.com/0xfe/vexflow/commit/07e32525efc9c5f088f552bc612d98c675f895b0) formatterMetrics as member in TickContext

[01d3add8d3b3097235323aa67194b110f187af5e](https://github.com/0xfe/vexflow/commit/01d3add8d3b3097235323aa67194b110f187af5e) unused import removed

[819707ccc846f339cf38dfc6a0dc0be3ad9c5d34](https://github.com/0xfe/vexflow/commit/819707ccc846f339cf38dfc6a0dc0be3ad9c5d34) TickContext not extrending Tickable

[9096368ce9b31227e48ddf1fd7f03d5df130694f](https://github.com/0xfe/vexflow/commit/9096368ce9b31227e48ddf1fd7f03d5df130694f) Merge pull request #1136 from ronyeh/package-json

[8a025d9c319c85fe401f73b74b458e3a8f658975](https://github.com/0xfe/vexflow/commit/8a025d9c319c85fe401f73b74b458e3a8f658975) Merge pull request #1140 from tommadams/canvasContext

[ba6b292a9eacef098a4451568d5fc385bacb2573](https://github.com/0xfe/vexflow/commit/ba6b292a9eacef098a4451568d5fc385bacb2573) Merge pull request #1139 from rvilarl/fix/factoryGraceNote

[75f6437fb519f5d4c1b023c8c4afcff2b9aa7804](https://github.com/0xfe/vexflow/commit/75f6437fb519f5d4c1b023c8c4afcff2b9aa7804) glyphnote_tests TODOs fixed

[29035aad4222fb339fcd51b2efe2d8b5167e54f2](https://github.com/0xfe/vexflow/commit/29035aad4222fb339fcd51b2efe2d8b5167e54f2) glyphnote & repeatnote constructor parameters fixed

[5fe842ea9311c894152800a63470ee1d0dc3cbf9](https://github.com/0xfe/vexflow/commit/5fe842ea9311c894152800a63470ee1d0dc3cbf9) repeatnote constructor parameters fixed

[db2df9a1542994cd6965e5e7c6b4c73da555c71b](https://github.com/0xfe/vexflow/commit/db2df9a1542994cd6965e5e7c6b4c73da555c71b) glyphnote constructor parameters fixed

[72a60b4ce0a57fd9e02f59df451542c33bd09209](https://github.com/0xfe/vexflow/commit/72a60b4ce0a57fd9e02f59df451542c33bd09209) chordsymbol addText & addGlyphOrText parameters fixed

[3aaac5880a9b4423f48d015618afca98df76f37b](https://github.com/0xfe/vexflow/commit/3aaac5880a9b4423f48d015618afca98df76f37b) fix glow rendering

[1fef9eb2b8244e325ea42b6dd85fc12dd50eb93d](https://github.com/0xfe/vexflow/commit/1fef9eb2b8244e325ea42b6dd85fc12dd50eb93d) address review comments

[cbca85c0b8c2a7063de3b29e1c259890c7be9e75](https://github.com/0xfe/vexflow/commit/cbca85c0b8c2a7063de3b29e1c259890c7be9e75) note_struct -> noteStruct

[9cf148f49e0a515c60eca317e0e6b1e0e0cc78b1](https://github.com/0xfe/vexflow/commit/9cf148f49e0a515c60eca317e0e6b1e0e0cc78b1) TODO Factory.GraceNote resolved

[b5a28e84f8a413b468221c58737cb4ce8c8de983](https://github.com/0xfe/vexflow/commit/b5a28e84f8a413b468221c58737cb4ce8c8de983) GraceNote parameter accepts partials

[0ac5c1a3ef2556bc7c023c32278c387ef42233a5](https://github.com/0xfe/vexflow/commit/0ac5c1a3ef2556bc7c023c32278c387ef42233a5) constructor parameter accepts partials

[8e77f447b9489b4c1f494a072f36e7643073c7cf](https://github.com/0xfe/vexflow/commit/8e77f447b9489b4c1f494a072f36e7643073c7cf) constructor 2nd parameter optional

[2b0f630a3ac0c83b8170ffdc7535a30c98392bb4](https://github.com/0xfe/vexflow/commit/2b0f630a3ac0c83b8170ffdc7535a30c98392bb4) Remove webpack-dev-server.

[c1c8f71e1020f2a8d8bcf5fbf3fae6251223c4be](https://github.com/0xfe/vexflow/commit/c1c8f71e1020f2a8d8bcf5fbf3fae6251223c4be) clean up text measuring & add a cache

[0847b1c289cf71ea57aacd43760733a8b268d310](https://github.com/0xfe/vexflow/commit/0847b1c289cf71ea57aacd43760733a8b268d310) Upgraded:  eslint-plugin-import  ^2.23.4  →  ^2.24.2  grunt                  ^1.0.4  →   ^1.4.1  grunt-git             ^1.0.14  →   ^1.1.1  jsdom                 ^16.7.0  →  ^17.0.0  npm                   ^7.20.3  →  ^7.22.0  qunit                 ^2.16.0  →  ^2.17.0  webpack-dev-server    ^3.11.2  →   ^4.1.1

[4f6cd90249663956b147814deae1360a78fcfcd9](https://github.com/0xfe/vexflow/commit/4f6cd90249663956b147814deae1360a78fcfcd9) Remove jQuery.

[35235dd991a76442529c0d18249f535a131b9e78](https://github.com/0xfe/vexflow/commit/35235dd991a76442529c0d18249f535a131b9e78) Update webpack to 5.52.0. Update eslint-plugin-prettier to 4.0.0.

[00c4d787a885f6692df7b48c6abd91e27ed63672](https://github.com/0xfe/vexflow/commit/00c4d787a885f6692df7b48c6abd91e27ed63672) Update @typescript-eslint/eslint-plugin and @typescript-eslint/parser to 4.31.0.

[5b4a4a8eb6a78ae7ead3b738201bb6841a8ec9c9](https://github.com/0xfe/vexflow/commit/5b4a4a8eb6a78ae7ead3b738201bb6841a8ec9c9) Update typescript to 4.4.2. Update typedoc to 0.21.9.

[3075e6ad282e3a9fdb78bbf35644518e3ebe2d4a](https://github.com/0xfe/vexflow/commit/3075e6ad282e3a9fdb78bbf35644518e3ebe2d4a) Remove browserify.

[490970b96aace865669d5d2d44acfeb349bc112f](https://github.com/0xfe/vexflow/commit/490970b96aace865669d5d2d44acfeb349bc112f) Merge pull request #1134 from rvilarl/fix/easyscoreVoice

[118473e7760e888ce3efc0ee23206fcc3038a21c](https://github.com/0xfe/vexflow/commit/118473e7760e888ce3efc0ee23206fcc3038a21c) Merge pull request #1132 from AaronDavidNewman/master

[793b5ee97d9c8bd7df9f846eaca5f114e72dda19](https://github.com/0xfe/vexflow/commit/793b5ee97d9c8bd7df9f846eaca5f114e72dda19) Merge pull request #1133 from tommadams/gruntfile

[af902352f92c14ccb3589ace938d8f3158509cde](https://github.com/0xfe/vexflow/commit/af902352f92c14ccb3589ace938d8f3158509cde) EasyScore.voice accepts Note

[dda45f8e0902ee4f08737f5c990a9532e3032fbd](https://github.com/0xfe/vexflow/commit/dda45f8e0902ee4f08737f5c990a9532e3032fbd) minor gruntfile fix

[e7f8ebbe637b15a1a4760b15d3df4fc853404353](https://github.com/0xfe/vexflow/commit/e7f8ebbe637b15a1a4760b15d3df4fc853404353) Remove issue reference in comments

[23b79c806b07598119fbf38a12a152391c948bef](https://github.com/0xfe/vexflow/commit/23b79c806b07598119fbf38a12a152391c948bef) misspelling

[dd1f745a2236bab4b97ac1989fee9c9541607ffa](https://github.com/0xfe/vexflow/commit/dd1f745a2236bab4b97ac1989fee9c9541607ffa) Fix VF reference that breaks CI

[e17079653cd5f8a5103fd7d09fb11187c5068f17](https://github.com/0xfe/vexflow/commit/e17079653cd5f8a5103fd7d09fb11187c5068f17) Merge pull request #1117 from ronyeh/easyscore

[11d76101808217139c4f0d4a2aad6ef36aa8edeb](https://github.com/0xfe/vexflow/commit/11d76101808217139c4f0d4a2aad6ef36aa8edeb) Add a test case back

[57463a67d8c855d6a5d946b554287fd244a1aa47](https://github.com/0xfe/vexflow/commit/57463a67d8c855d6a5d946b554287fd244a1aa47) Merge https://github.com/0xfe/vexflow

[acfb12060ac14ef8a6a2a1d7b44a9cd13f6cb532](https://github.com/0xfe/vexflow/commit/acfb12060ac14ef8a6a2a1d7b44a9cd13f6cb532) Merge pull request #1072 from ronyeh/examples

[912556d722bcfec1ea7539101cc2821e3200bd55](https://github.com/0xfe/vexflow/commit/912556d722bcfec1ea7539101cc2821e3200bd55) Merge pull request #1131 from ronyeh/migration/tests

[35482512d563e9f5b4000b40e5c6174d89a84115](https://github.com/0xfe/vexflow/commit/35482512d563e9f5b4000b40e5c6174d89a84115) Update comment and use the accidentals constant from Music. Move up commit hooks.

[ec1efead0732b1b88736974802f2e616842f12b9](https://github.com/0xfe/vexflow/commit/ec1efead0732b1b88736974802f2e616842f12b9) Clean up EasyScore and Parser.

[d4c48d819b3b82a1ddfcabaf769dc94ae1c6e37d](https://github.com/0xfe/vexflow/commit/d4c48d819b3b82a1ddfcabaf769dc94ae1c6e37d) Add tests for the native Renderer API. The constructor's first element can be a string, canvas, or div. The output should be identical to the Factory API (which uses Renderer).

[24caf2e8321195b52e49341b0650c254b36ae2f2](https://github.com/0xfe/vexflow/commit/24caf2e8321195b52e49341b0650c254b36ae2f2) Address code review comments.

[2fd5d6e26ed477567040e246f15e55bf3739f23e](https://github.com/0xfe/vexflow/commit/2fd5d6e26ed477567040e246f15e55bf3739f23e) Node JS modules

[56ca142d044eb48800cfbcadf2fc6d65ac15eeb1](https://github.com/0xfe/vexflow/commit/56ca142d044eb48800cfbcadf2fc6d65ac15eeb1) Add demo for legacy Node JS. Improve comments.

[cacf7af8eeb57a52cc4d121340ff00d5d6a724a4](https://github.com/0xfe/vexflow/commit/cacf7af8eeb57a52cc4d121340ff00d5d6a724a4) Improve Gruntfile to support NodeJS module loading. Support window, globalThis, and this. Improve Node JS example.

[d22c2a960490ccb188384b191484ebe2dbcb924c](https://github.com/0xfe/vexflow/commit/d22c2a960490ccb188384b191484ebe2dbcb924c) This patch to VexFlow builds on PR #1045 Add comments and README. Add example for script type="module".

[fd1027c15d0c0cfa8210b1a3fc77836b75238b5a](https://github.com/0xfe/vexflow/commit/fd1027c15d0c0cfa8210b1a3fc77836b75238b5a) Replace try / catch blocks in tests with the QUnit throws() assertion. Fixes https://github.com/0xfe/vexflow/issues/1130

[fbafe0d4ac35dc78fb77e0c7705385ba817fcdd9](https://github.com/0xfe/vexflow/commit/fbafe0d4ac35dc78fb77e0c7705385ba817fcdd9) Merge https://github.com/0xfe/vexflow

[b0f79ac913afaa081c775c2afaae63b7840505c3](https://github.com/0xfe/vexflow/commit/b0f79ac913afaa081c775c2afaae63b7840505c3) Address issue 1122

[c712ef340fbc7de8f34a951561c47ad0584abe0e](https://github.com/0xfe/vexflow/commit/c712ef340fbc7de8f34a951561c47ad0584abe0e) Merge pull request #1128 from rvilarl/fix/systemFormat

[b8acbb5fa905b1d1c13f082d389b103aeebce0c7](https://github.com/0xfe/vexflow/commit/b8acbb5fa905b1d1c13f082d389b103aeebce0c7) Merge pull request #1094 from ronyeh/migration/tests

[7a58a0f2701fdbbfaf6077517f11eb6845ea089d](https://github.com/0xfe/vexflow/commit/7a58a0f2701fdbbfaf6077517f11eb6845ea089d) fix import

[4e2cc938c271b98adc7e105e13ea1594a1df5a44](https://github.com/0xfe/vexflow/commit/4e2cc938c271b98adc7e105e13ea1594a1df5a44) bounding box calculation

[950d7e103663275aaf278e3f69d8652d3c3b3017](https://github.com/0xfe/vexflow/commit/950d7e103663275aaf278e3f69d8652d3c3b3017) Comments. Include an unused test.

[f11ecb42144c27821ab03efecfbaffce4fa18607](https://github.com/0xfe/vexflow/commit/f11ecb42144c27821ab03efecfbaffce4fa18607) Merge branch 'master' into migration/tests Pull in recent upstream changes (e.g., defined(...)).

[6dad8b20631745be97db32dcaac8772aec6e278f](https://github.com/0xfe/vexflow/commit/6dad8b20631745be97db32dcaac8772aec6e278f) Move helper functions up. Test methods are now private to the JS module. Only the Start() method is exported.

[b37ddd7a228c69b165c96f4431598b703585fc37](https://github.com/0xfe/vexflow/commit/b37ddd7a228c69b165c96f4431598b703585fc37) Merge pull request #1123 from ronyeh/defined

[9e8fb997667f1ba6d9e291ace151158dd5d6399b](https://github.com/0xfe/vexflow/commit/9e8fb997667f1ba6d9e291ace151158dd5d6399b) Use Note.plotMetrics() directly.

[56fcd4320453e058954b66e2524ce9bcfe05c547](https://github.com/0xfe/vexflow/commit/56fcd4320453e058954b66e2524ce9bcfe05c547) Code review comments: - Move helper functions up. - Rename helper function in BachDemo to appendSystem().

[29a838e5d7a940c4b6c74afb2d19741d4ea67fab](https://github.com/0xfe/vexflow/commit/29a838e5d7a940c4b6c74afb2d19741d4ea67fab) Use defined() for this.glyph. Remove unused imports. Fixes https://github.com/0xfe/vexflow/issues/1115

[f6a5f8c654a737799e1124d3e1b7edd67cd6bb82](https://github.com/0xfe/vexflow/commit/f6a5f8c654a737799e1124d3e1b7edd67cd6bb82) EasyScore Merge the commitPiece() method with #1117.

[b79e5c73d07b53ab79887d5ee448d00952abf0d3](https://github.com/0xfe/vexflow/commit/b79e5c73d07b53ab79887d5ee448d00952abf0d3) Use defined() in Accidental, Articulation, Voice.

[8a3c6e8d84549d65029e12915047fba18c8779e9](https://github.com/0xfe/vexflow/commit/8a3c6e8d84549d65029e12915047fba18c8779e9) Use defined() in Clef.

[9f0f53dbe0ac37de432bc1e334815537004ec556](https://github.com/0xfe/vexflow/commit/9f0f53dbe0ac37de432bc1e334815537004ec556) Use defined() in Glyph, Modifier, Note, Ornament.

[9ca2f0a7e82f111dcebc34f38925f22ff41961d6](https://github.com/0xfe/vexflow/commit/9ca2f0a7e82f111dcebc34f38925f22ff41961d6) Use defined() for Font data and metrics. Improve comments.

[9afe93998adf1ecd0c978a796be7349dc486cfe0](https://github.com/0xfe/vexflow/commit/9afe93998adf1ecd0c978a796be7349dc486cfe0) checkTickContext()

[5b59396eae6cbc39a73e85314708faa5c942f19c](https://github.com/0xfe/vexflow/commit/5b59396eae6cbc39a73e85314708faa5c942f19c) checkContext(), checkModifierContext(), checkMetrics()

[50cf696bc17187d263789533fdc2dca6ae872140](https://github.com/0xfe/vexflow/commit/50cf696bc17187d263789533fdc2dca6ae872140) defined<T>(...) => defined(...)

[9eb1e89dcaad0a59c6ec7bf2a715e6cb2c4ff0cb](https://github.com/0xfe/vexflow/commit/9eb1e89dcaad0a59c6ec7bf2a715e6cb2c4ff0cb) Use or implement checkStave() as needed.

[483a1cabb4476bfe548f5ecf035b809bc89dccb6](https://github.com/0xfe/vexflow/commit/483a1cabb4476bfe548f5ecf035b809bc89dccb6) defined<number>(...) => defined(...). The <number> doesn't actually do a typeof check. It is just a sanity check by the TypeScript compiler that the first argument is actually specified as a 'number' in our code. It is possible that we can eventually remove some of these defined(...) calls whenever the argument's type is not number | undefined.

[74073f0e71fcc64b682ea3c5fe067abba85a6cd4](https://github.com/0xfe/vexflow/commit/74073f0e71fcc64b682ea3c5fe067abba85a6cd4) checkStave passes a RuntimeError code and message.

[5992d83a75f42564305f69f165bd62d9b302caea](https://github.com/0xfe/vexflow/commit/5992d83a75f42564305f69f165bd62d9b302caea) Use defined() for checkStave().

[a45a7da93b1b286208343964d8c0c9a6009608e0](https://github.com/0xfe/vexflow/commit/a45a7da93b1b286208343964d8c0c9a6009608e0) Rename check<T>() to defined<T>().

[4d7237728be5e4e69e1cd84ac6fedb7e226224ca](https://github.com/0xfe/vexflow/commit/4d7237728be5e4e69e1cd84ac6fedb7e226224ca) Improve consistency with the structure of test files.

[24295fcf83f171e6b8141d7b9e7e3ca9ece0aef4](https://github.com/0xfe/vexflow/commit/24295fcf83f171e6b8141d7b9e7e3ca9ece0aef4) Clean up #region #endregion markers.

[8677c964ec5597488461ffe77d44d8a06fe730bb](https://github.com/0xfe/vexflow/commit/8677c964ec5597488461ffe77d44d8a06fe730bb) Clean up BarlineTests. Uncomment the tests in AnnotationTests.

[b541023c7940183fa0170fa432b138f588270f7f](https://github.com/0xfe/vexflow/commit/b541023c7940183fa0170fa432b138f588270f7f) Use spread operator instead of .concat(). Add helper function to create EasyScore shortcut functions (via .bind()).

[b43154c8ed9a4c70fb63db2ae1e1cf786f722847](https://github.com/0xfe/vexflow/commit/b43154c8ed9a4c70fb63db2ae1e1cf786f722847) Tests for Stave, Accidental, Annotation, ChordSymbol, Parser, StaveConnector, StaveNote, Strokes, TimeSignature, and more...

[07be11fe86be7090d015832b533512d564bc90f1](https://github.com/0xfe/vexflow/commit/07be11fe86be7090d015832b533512d564bc90f1) TabSlideTests, ClefKeySignatureTests, ...

[f1723fc2fc2de259594047aac1cfa027d68b7c50](https://github.com/0xfe/vexflow/commit/f1723fc2fc2de259594047aac1cfa027d68b7c50) Tests for AutoBeamFormatting, Barline, Beam, BoundingBox, BoundingBoxComputation, Clef, Curve, Dot, GlyphNote, GraceNote, NoteSubGroup, Ornament, Rests, Rhythm, StaveNote, TabNote, TextNote, ThreeVoice, TickContext, Tuning, Tuplet...

[8ad86c2349ee2a0ee9590daa7cdaa7045cfd10da](https://github.com/0xfe/vexflow/commit/8ad86c2349ee2a0ee9590daa7cdaa7045cfd10da) ArticulationTests, PercussionTests, AnnotationTests, and more!

[9cecd997b6ecb8d3fb2d0984b2a6a2aee847236b](https://github.com/0xfe/vexflow/commit/9cecd997b6ecb8d3fb2d0984b2a6a2aee847236b) AccidentalTests, AnnotationTests, ArticulationTests, AutoBeamFormattingTests, BendTests, ChordSymbolTests, DotTests, and more...

[0c04294f55e0ab29be3fc592b63be14ce7187dfa](https://github.com/0xfe/vexflow/commit/0c04294f55e0ab29be3fc592b63be14ce7187dfa) TimeSignatureTests & AnnotationTests

[fef7f872eff9aac4ba7195210666eee3551db210](https://github.com/0xfe/vexflow/commit/fef7f872eff9aac4ba7195210666eee3551db210) Parser & EasyScore Tests. Remove explicit types where they can be inferred. Consistently use QUnit globals.

[1937c04510c23106f11e2b8fa8fd46de1aa808c5](https://github.com/0xfe/vexflow/commit/1937c04510c23106f11e2b8fa8fd46de1aa808c5) Vibrato Tests. Remove unused import. Update test case to not use VF global.

[b01d4649367310d0cc369099ec6932f849762343](https://github.com/0xfe/vexflow/commit/b01d4649367310d0cc369099ec6932f849762343) Accidental Tests. Move QUMock object into generate_png_images.js to avoid import ordering issue. Use BoundingBox getters.

[1202c05ab058737daa0408646a3cdbe6da5c6ff8](https://github.com/0xfe/vexflow/commit/1202c05ab058737daa0408646a3cdbe6da5c6ff8) StaveNote and Note had identical addModifier() methods. Remove from StaveNote. Consolidate duplicate implementations of addToModifierContext(mc).

[978aa682c0cd6f116377f29756d747bd35844c9f](https://github.com/0xfe/vexflow/commit/978aa682c0cd6f116377f29756d747bd35844c9f) Formatter Tests.

[417681d1c375e3fe1307822314ad298ff2443db6](https://github.com/0xfe/vexflow/commit/417681d1c375e3fe1307822314ad298ff2443db6) Improve tests. Use more accessors. Clean up more tests by removing @ts-nocheck.

[d9ce2a3d8bd3dbce00173e518d0976a47b83572d](https://github.com/0xfe/vexflow/commit/d9ce2a3d8bd3dbce00173e518d0976a47b83572d) Rhythm Tests Use accessor methods instead of directly accessing protected instance variables. Done removing VF.* from tests. VF is no longer an implicit global.

[9eea442b87b8a0358310ffc7f0e72431040dcfcb](https://github.com/0xfe/vexflow/commit/9eea442b87b8a0358310ffc7f0e72431040dcfcb) GraceTabNote & TabSlide Tests.

[a3ac41ef4041d5d321d10eaf96b1b52857349b58](https://github.com/0xfe/vexflow/commit/a3ac41ef4041d5d321d10eaf96b1b52857349b58) Merge pull request #1116 from ronyeh/tickables

[dcf7052143fa961aa2b9590ddc9f3352f657f693](https://github.com/0xfe/vexflow/commit/dcf7052143fa961aa2b9590ddc9f3352f657f693) Fix comment typo in Formatter.

[8d3444b786de98a5eb20172830b18777ec1852a5](https://github.com/0xfe/vexflow/commit/8d3444b786de98a5eb20172830b18777ec1852a5) Add comment for isRest().

[04ae893cb7b952a2837d40f74bb7899097679e8e](https://github.com/0xfe/vexflow/commit/04ae893cb7b952a2837d40f74bb7899097679e8e) Remove unused import.

[1782114594bc912c21d144faa1dffdb0b748c23c](https://github.com/0xfe/vexflow/commit/1782114594bc912c21d144faa1dffdb0b748c23c) Fix merge issue. Remove instanceof.

[9ce76f364ca7bb394a8a1dc1d42fda9861dee8f6](https://github.com/0xfe/vexflow/commit/9ce76f364ca7bb394a8a1dc1d42fda9861dee8f6) flow.html provides global access to QUnit functions, so we declare QUnit functions as global in TypeScript (via tests/types/qunit.d.ts). This simplifies test creation, because we no longer have to import individual QUnit functions before using them.

[742a4efa6e058a6635ad67c974641015c482a430](https://github.com/0xfe/vexflow/commit/742a4efa6e058a6635ad67c974641015c482a430) Remove unused import. Fix comments. Move isRest() back down to note.ts. Move qunit.ts type declarations into tests/types/

[87859b286399d743df575576e7cd0b3d758a26f1](https://github.com/0xfe/vexflow/commit/87859b286399d743df575576e7cd0b3d758a26f1) Move getKeys() and getKeyProps() up Note (where this.keys and this.keyProps are defined). Move isRest() up to Tickable, and fix the comment.

[72404242d343ef08e7bea5843e711dda3d4290e0](https://github.com/0xfe/vexflow/commit/72404242d343ef08e7bea5843e711dda3d4290e0) Use Modifier.CATEGORY.

[495ab14cadc9208052b15d6ec686d7606b16b607](https://github.com/0xfe/vexflow/commit/495ab14cadc9208052b15d6ec686d7606b16b607) Use Tickable instead of Note. Use isStaveNote(). Be consistent with imports. Always start with ./

[43c6b31b9738d28354470420c164a8d735fc423b](https://github.com/0xfe/vexflow/commit/43c6b31b9738d28354470420c164a8d735fc423b) Use this.setPreFormatted() or field initializers where possible. Sort imports. Add CATEGORY to Tickable.

[38653e80c0e0e19c1fe58fddf3f6d91b42c20ffb](https://github.com/0xfe/vexflow/commit/38653e80c0e0e19c1fe58fddf3f6d91b42c20ffb) Make the check<T>() function more flexible (so that it doesn't always just return a 'undefined' RuntimeError). Other small improvements.

[a58030ce33ad798499812bbb44c17fed68c68bb4](https://github.com/0xfe/vexflow/commit/a58030ce33ad798499812bbb44c17fed68c68bb4) Small improvements and fixes, including: - add initial value to .reduce() to handle empty arrays. - remove duplicate setPreFormatted() method from subclass. - group instance variables x, y, width, height together. - always check the this.preFormatted flag first. - fix typo.

[44fb8c011765f56e3c18b9c8617327c7ce11e434](https://github.com/0xfe/vexflow/commit/44fb8c011765f56e3c18b9c8617327c7ce11e434) Improvements with addModifier() and addToModifierContext(). Remove duplicate implementations and add comments to overrides.

[fcaa0d21c48d837323d7db5bae70098fe7adeda5](https://github.com/0xfe/vexflow/commit/fcaa0d21c48d837323d7db5bae70098fe7adeda5) Small fixes to setFont(). Test cases assume the last argument is optional.

[158994b73d876d05f0d2ac60c64adc428ec309d3](https://github.com/0xfe/vexflow/commit/158994b73d876d05f0d2ac60c64adc428ec309d3) Use Tickable instead of Note in accidental.ts.

[e7f0426a662cc9fb28760b3c547cd3a2b357e0da](https://github.com/0xfe/vexflow/commit/e7f0426a662cc9fb28760b3c547cd3a2b357e0da) Merge pull request #1091 from rvilarl/fix/accidentals

[51df1720a21f28f70dc1eb74405967d96444a12e](https://github.com/0xfe/vexflow/commit/51df1720a21f28f70dc1eb74405967d96444a12e) note keys tested

[1c3638b26c9368cb562d146a61956a2d793f1cc4](https://github.com/0xfe/vexflow/commit/1c3638b26c9368cb562d146a61956a2d793f1cc4) No Accidentals Necessary (EasyScore)

[95dd0bec101ddcef95856bfef8cffbc7a0b58185](https://github.com/0xfe/vexflow/commit/95dd0bec101ddcef95856bfef8cffbc7a0b58185) review comments

[134a6b32471909b87b35bf24544bf54546c900f6](https://github.com/0xfe/vexflow/commit/134a6b32471909b87b35bf24544bf54546c900f6) microtones & accidentals splitted

[1f4d4230a185eddbaac4cb2cceb32d0d50800fef](https://github.com/0xfe/vexflow/commit/1f4d4230a185eddbaac4cb2cceb32d0d50800fef) fix applyAccidentals

[23bde7d4ed40ff64511c37c99b43f806291b9160](https://github.com/0xfe/vexflow/commit/23bde7d4ed40ff64511c37c99b43f806291b9160) review comments

[704cb29ba7c7df8ab87c765d37a0ac8360d637d6](https://github.com/0xfe/vexflow/commit/704cb29ba7c7df8ab87c765d37a0ac8360d637d6) Note.keys keep accidental

[366057d9d21c710de49c9553e9c4025d885a8615](https://github.com/0xfe/vexflow/commit/366057d9d21c710de49c9553e9c4025d885a8615) Merge pull request #1112 from ronyeh/sort-imports-2

[f7c683ce30e3411e27ba74f53c491c229474ce98](https://github.com/0xfe/vexflow/commit/f7c683ce30e3411e27ba74f53c491c229474ce98) Rename declarations.ts to qunit_api.ts. Update comments. Fix import.

[8b3d0650c1e2723d83a90b06799668ab97833c57](https://github.com/0xfe/vexflow/commit/8b3d0650c1e2723d83a90b06799668ab97833c57) Sort Imports and Test Cases. Test Vex.Flow.* prefix for all classes.

[12ecf1eee743e15f23b52578f1bc3e5fac7717e2](https://github.com/0xfe/vexflow/commit/12ecf1eee743e15f23b52578f1bc3e5fac7717e2) Merge pull request #1110 from ronyeh/sort-imports

[77587f011699c6234a0095bb07f151ea09e065e5](https://github.com/0xfe/vexflow/commit/77587f011699c6234a0095bb07f151ea09e065e5) Fix a test case that permanently modified Vex.Flow.STAVE_LINE_THICKNESS. This results in visual diffs in the stave lines in test cases that were run after StaveConnectorTests.Start();

[6296dd3935ec0cbd226b4baa607ec66d535a1e55](https://github.com/0xfe/vexflow/commit/6296dd3935ec0cbd226b4baa607ec66d535a1e55) Merge pull request #1111 from ronyeh/changelog

[bea682556476dbe34f54a40a84907b660a101ad2](https://github.com/0xfe/vexflow/commit/bea682556476dbe34f54a40a84907b660a101ad2) Merge pull request #1098 from ronyeh/instanceof

[74daba83d8217d078b39f2018c7c5fcd1b76238f](https://github.com/0xfe/vexflow/commit/74daba83d8217d078b39f2018c7c5fcd1b76238f) Add a CHANGELOG.md to track breaking changes and new features.

[77d3d2a93bd8fc8c5a993eea605c915a921c6e82](https://github.com/0xfe/vexflow/commit/77d3d2a93bd8fc8c5a993eea605c915a921c6e82) Now that we target ES6, update the test case to reflect that isCategory() works as expected.

[e662d2d5ea63e5b2791ec15bbaa263976ed7bab9](https://github.com/0xfe/vexflow/commit/e662d2d5ea63e5b2791ec15bbaa263976ed7bab9) Type Guard test cases.

[45b568aab4d71fee5cc3cce046709ebbb39b10af](https://github.com/0xfe/vexflow/commit/45b568aab4d71fee5cc3cce046709ebbb39b10af) Improve tests. Add .CATEGORY to StemmableNote.

[a783a9a8ac20b040bd5a2b63204ccdc159f839b1](https://github.com/0xfe/vexflow/commit/a783a9a8ac20b040bd5a2b63204ccdc159f839b1) Improve isCategory(). Add typeguard helper functions. Add some tests (work in progress). Sort tests alphabetically in run.ts.

[c73b6babfd0d2eebaf95ccb223e477f02578c331](https://github.com/0xfe/vexflow/commit/c73b6babfd0d2eebaf95ccb223e477f02578c331) Walk up the prototype chain to check for .getCategory().

[e58e3fe73564bd33c3e10ee3a5e3baea903b540b](https://github.com/0xfe/vexflow/commit/e58e3fe73564bd33c3e10ee3a5e3baea903b540b) Implement isCategory<T>(T, obj) as a flexible type guard alternative to instanceof. Fixes https://github.com/0xfe/vexflow/issues/1096

[a08cc830287ba8e463eae5481fa888fa62b4419e](https://github.com/0xfe/vexflow/commit/a08cc830287ba8e463eae5481fa888fa62b4419e) Merge pull request #1108 from ronyeh/master

[d0ac5cbabb676c0776bf868e59c921d718c4a270](https://github.com/0xfe/vexflow/commit/d0ac5cbabb676c0776bf868e59c921d718c4a270) Change target to es6 in tsconfig.json. Change target to es6 in tsconfig.dynamic.json.

[5480e70c4cfbe47df692d873a59e9441d3b90736](https://github.com/0xfe/vexflow/commit/5480e70c4cfbe47df692d873a59e9441d3b90736) Merge pull request #1103 from tommadams/dev

[3208adb8c7a0a5f5990766360fda0e55804780f2](https://github.com/0xfe/vexflow/commit/3208adb8c7a0a5f5990766360fda0e55804780f2) auto formatting

[2ea06215a958b50cc5cfe74403366a8d3ca59f5e](https://github.com/0xfe/vexflow/commit/2ea06215a958b50cc5cfe74403366a8d3ca59f5e) Optimisations to the glyph code.

[24f91ee58fa2de3536b56ee90604d2dab36e498c](https://github.com/0xfe/vexflow/commit/24f91ee58fa2de3536b56ee90604d2dab36e498c) Merge pull request #1099 from ronyeh/instanceof-fraction

[1bcc739341dac5a29e0849339cd826b1bcad657f](https://github.com/0xfe/vexflow/commit/1bcc739341dac5a29e0849339cd826b1bcad657f) Merge pull request #1045 from aleen42/master

[5d30c8081d1d4f29a63ac8f6ad41ebe1704f157a](https://github.com/0xfe/vexflow/commit/5d30c8081d1d4f29a63ac8f6ad41ebe1704f157a) Merge pull request #1100 from rvilarl/fix/importHelpers

[ee1fc6076fc9351779e9a8d1f024dd6c37c448fb](https://github.com/0xfe/vexflow/commit/ee1fc6076fc9351779e9a8d1f024dd6c37c448fb) remove importHelpers

[b66a25ca9088ed5ebf2cd2d053cbfc58f8aa215f](https://github.com/0xfe/vexflow/commit/b66a25ca9088ed5ebf2cd2d053cbfc58f8aa215f) update packages

[8cdcd3aa606a24d8b9afe8cd664e96d2df59f746](https://github.com/0xfe/vexflow/commit/8cdcd3aa606a24d8b9afe8cd664e96d2df59f746) Improve comments.

[d15393f5a6af27d109ad24f01bee7c9700423205](https://github.com/0xfe/vexflow/commit/d15393f5a6af27d109ad24f01bee7c9700423205) Remove instanceof from Fraction. Partially addresses: https://github.com/0xfe/vexflow/issues/1096

[37e70ad84f26ebce2546c52ac0c9c3e7c4a127c9](https://github.com/0xfe/vexflow/commit/37e70ad84f26ebce2546c52ac0c9c3e7c4a127c9) Merge pull request #1095 from ronyeh/tabnoteposition

[a4a528d8991fbaf6899decd3208b4453ebbb5d5c](https://github.com/0xfe/vexflow/commit/a4a528d8991fbaf6899decd3208b4453ebbb5d5c) TabNoteStruct: Use number | string for fret positions. Fix: https://github.com/0xfe/vexflow/issues/1093 Unicode: Remove parseInt(). Fix: https://github.com/0xfe/vexflow/issues/1087

[4349c8050c654c99ae8fa2c61e9be16a62f39343](https://github.com/0xfe/vexflow/commit/4349c8050c654c99ae8fa2c61e9be16a62f39343) Merge pull request #1077 from tommadams/master

[2f3fc7c748ce827f434142ba41b9475461e9c9c2](https://github.com/0xfe/vexflow/commit/2f3fc7c748ce827f434142ba41b9475461e9c9c2) Merge pull request #1090 from ronyeh/master

[7ee47553f11c6116e20d3646996efa001f7345ba](https://github.com/0xfe/vexflow/commit/7ee47553f11c6116e20d3646996efa001f7345ba) Merge pull request #1080 from AaronDavidNewman/master

[c8e198fd4cf859394790cbfa78d906d0ae1835e0](https://github.com/0xfe/vexflow/commit/c8e198fd4cf859394790cbfa78d906d0ae1835e0) Merge pull request #1073 from rvilarl/api/easyscore

[8ab1be2bf8024d0e6308b0e82bba1482cbd6205f](https://github.com/0xfe/vexflow/commit/8ab1be2bf8024d0e6308b0e82bba1482cbd6205f) Update BoundingBoxComputationTests to TS

[83037a55893306e86da15746ce3748de39078a65](https://github.com/0xfe/vexflow/commit/83037a55893306e86da15746ce3748de39078a65) Merge remote-tracking branch 'upstream/master'

[4edc1700cc1200ab5a8f0098d211d247fba43558](https://github.com/0xfe/vexflow/commit/4edc1700cc1200ab5a8f0098d211d247fba43558) Restore the ability to run 'npm run test:reference' now that PR #1074 has been merged. Fixes Issue #1088.

[ce8a8db42d48fb7d5a8e33fd37d11c6a71b68701](https://github.com/0xfe/vexflow/commit/ce8a8db42d48fb7d5a8e33fd37d11c6a71b68701) Update formatter_tests.ts

[faccc9d92ac6c92607f6e6dd0b4d680e515f1f29](https://github.com/0xfe/vexflow/commit/faccc9d92ac6c92607f6e6dd0b4d680e515f1f29) Merge https://github.com/0xfe/vexflow

[cc6d288641bf7298b160dff0ba7c938dc8b44369](https://github.com/0xfe/vexflow/commit/cc6d288641bf7298b160dff0ba7c938dc8b44369) review comments

[6a2e59e7ed620f01d347b32dec246493ded0fe22](https://github.com/0xfe/vexflow/commit/6a2e59e7ed620f01d347b32dec246493ded0fe22) typo

[5e4793b95b1c707e82603d037795a33b31195ec5](https://github.com/0xfe/vexflow/commit/5e4793b95b1c707e82603d037795a33b31195ec5) review comment

[2f76642c8c291c9fdfce8197657d2055a3d8b192](https://github.com/0xfe/vexflow/commit/2f76642c8c291c9fdfce8197657d2055a3d8b192) allow r or R as NOTENAME for rests

[c8d2b4de5e1d27505a8140ec3c41fd4909e665bd](https://github.com/0xfe/vexflow/commit/c8d2b4de5e1d27505a8140ec3c41fd4909e665bd) add FormatOptions to SystemOptions to allow rest alignment

[fb79e6a8e45ba6d2eb94983f13e9dbd51265ecfb](https://github.com/0xfe/vexflow/commit/fb79e6a8e45ba6d2eb94983f13e9dbd51265ecfb) documentation update

[090791568c43ff33523211bffe73f4820962ce03](https://github.com/0xfe/vexflow/commit/090791568c43ff33523211bffe73f4820962ce03) TODOs resolved

[7a682f7075017ccdcebd30d06dcc0f9661126dd2](https://github.com/0xfe/vexflow/commit/7a682f7075017ccdcebd30d06dcc0f9661126dd2) Merge pull request #1074 from ronyeh/migration/tests

[4bb422054ad389cf06be91376771652868f6f1ca](https://github.com/0xfe/vexflow/commit/4bb422054ad389cf06be91376771652868f6f1ca) Merge pull request #1085 from rvilarl/fix/music

[fb001cd30cdd1ff630b11aff68bd54b93fc55bbb](https://github.com/0xfe/vexflow/commit/fb001cd30cdd1ff630b11aff68bd54b93fc55bbb) Beam Tests.

[d3a4248b882ffb360970b59543e7c52fec73540e](https://github.com/0xfe/vexflow/commit/d3a4248b882ffb360970b59543e7c52fec73540e) StringNumber and TabSlide

[a8c4629d189ee4707c7bfc6bfd5eda1abfbbd261](https://github.com/0xfe/vexflow/commit/a8c4629d189ee4707c7bfc6bfd5eda1abfbbd261) Remove more VF.* prefixes.

[b8cfe0606e8355c1c130d74baa78a8a692ad7622](https://github.com/0xfe/vexflow/commit/b8cfe0606e8355c1c130d74baa78a8a692ad7622) Grace Note Tests

[cdc81762987f17135b7d1e8c6c10d91389816ddd](https://github.com/0xfe/vexflow/commit/cdc81762987f17135b7d1e8c6c10d91389816ddd) Fix comment. Vex.Flow.Test no longer needs BUILD/VERSION since we now bundle VexFlow with the VexFlowTests library.

[bc623dd2b16fc169f5cf9ca28a08d8dd5874a0b2](https://github.com/0xfe/vexflow/commit/bc623dd2b16fc169f5cf9ca28a08d8dd5874a0b2) Restore Vex.Flow.BUILD and Vex.Flow.VERSION.

[ebe0e0153387d127957094e75d396bfc8a2ca80c](https://github.com/0xfe/vexflow/commit/ebe0e0153387d127957094e75d396bfc8a2ca80c) Remove ../src/ from imports.

[fad59ec3fa0659277763bad38276bfc7e9fa548b](https://github.com/0xfe/vexflow/commit/fad59ec3fa0659277763bad38276bfc7e9fa548b) Remove console.log()

[6ff0c3ef6a3ee4661fea4d51ce6b2e7b298b1853](https://github.com/0xfe/vexflow/commit/6ff0c3ef6a3ee4661fea4d51ce6b2e7b298b1853) Parser Tests.

[42c3766ac7e383680a87026d485d8f0fd5f989a3](https://github.com/0xfe/vexflow/commit/42c3766ac7e383680a87026d485d8f0fd5f989a3) Verify uses of the definite assignment assertion ! operator.

[891e3c9cd456804eb0ca4b018e3644de41b0bf35](https://github.com/0xfe/vexflow/commit/891e3c9cd456804eb0ca4b018e3644de41b0bf35) Clean up vexflow_test_helpers.

[421e3483f675d255d5cc64f7cdf90b5ea7cb4fc1](https://github.com/0xfe/vexflow/commit/421e3483f675d255d5cc64f7cdf90b5ea7cb4fc1) QUnit mock object for testing. Add propEqual to the global namespace.

[41c3de4ca78e9c8d78864eece0c1acd7bc7e4ce5](https://github.com/0xfe/vexflow/commit/41c3de4ca78e9c8d78864eece0c1acd7bc7e4ce5) Remove more VF.* prefixes.

[9a174ea8ac86ceca5f42b3c1a257712ce36d4378](https://github.com/0xfe/vexflow/commit/9a174ea8ac86ceca5f42b3c1a257712ce36d4378) Remove more VF.* prefixes. Add tests to verify VF.* still works.

[9004cb301914f4d9850479eb4c4193ba93deecea](https://github.com/0xfe/vexflow/commit/9004cb301914f4d9850479eb4c4193ba93deecea) typo

[303bbbe0900c8d6febf81576c81f7711398cdd1a](https://github.com/0xfe/vexflow/commit/303bbbe0900c8d6febf81576c81f7711398cdd1a) fix #1084

[507defe53395d1ce3eb935c8603db1ccce827005](https://github.com/0xfe/vexflow/commit/507defe53395d1ce3eb935c8603db1ccce827005) Be consistent with const run = VexFlowTests.runTests;

[c6f1b36f3211e856ac81c88fff442e21c72ddc04](https://github.com/0xfe/vexflow/commit/c6f1b36f3211e856ac81c88fff442e21c72ddc04) Investigated visual diff: StaveModifier.Vertical_Bar_Test The current build seems to have fixed a bug. The reference and releases build seems to produce incorrect output.

[725fd16b0fdd2fac0bcfc857ad0003cb1e97c753](https://github.com/0xfe/vexflow/commit/725fd16b0fdd2fac0bcfc857ad0003cb1e97c753) The ver param now supports loading versions hosted on https://unpkg.com/

[7900d8fd5d81bb324ddd2f54c7c6ea60e9aaa8c5](https://github.com/0xfe/vexflow/commit/7900d8fd5d81bb324ddd2f54c7c6ea60e9aaa8c5) Small fix so that generate_png_images.js continues to work with npm run generate:blessed  and  ./tools/visual_regression.sh blessed

[4cc62169fde19444fb46e0f9e3a5077490fb8ea2](https://github.com/0xfe/vexflow/commit/4cc62169fde19444fb46e0f9e3a5077490fb8ea2) Restore the old names for tests for now, so we can get to zero visual diffs.

[2a9cb86df41b562f31b2c2f9ce34075ede323196](https://github.com/0xfe/vexflow/commit/2a9cb86df41b562f31b2c2f9ce34075ede323196) Add tests to check that the VF.* API still works.

[ee7bf1c9b8427a3921f3dabb4edbcfc66e3cb6ef](https://github.com/0xfe/vexflow/commit/ee7bf1c9b8427a3921f3dabb4edbcfc66e3cb6ef) Clean up vexflow_test_helpers.

[8a866b916875aa8bc207d821ac650e13f7365652](https://github.com/0xfe/vexflow/commit/8a866b916875aa8bc207d821ac650e13f7365652) Clean up imports.

[085a5e096644720b79da651c6d855fb100c94a6e](https://github.com/0xfe/vexflow/commit/085a5e096644720b79da651c6d855fb100c94a6e) Remove more VF.* prefixes.

[1ef90df23e7bba459fd09b7be7132b8618d0cf19](https://github.com/0xfe/vexflow/commit/1ef90df23e7bba459fd09b7be7132b8618d0cf19) Fix small issues.

[ba1b77ae09a5c6d1152f50c9e35cb673b74bbc78](https://github.com/0xfe/vexflow/commit/ba1b77ae09a5c6d1152f50c9e35cb673b74bbc78) All tests migrated. 6137 assertions of 6137 passed, 0 failed. There are still some VF.* prefixes to remove.

[c0be3b343964490255e3371edea3a2a4199a1d9f](https://github.com/0xfe/vexflow/commit/c0be3b343964490255e3371edea3a2a4199a1d9f) Fix bug in Accidental Tests with 'this' being undefined. Clean up more tests.

[2db426c93abd401ac3b91a75f93d031505a993e1](https://github.com/0xfe/vexflow/commit/2db426c93abd401ac3b91a75f93d031505a993e1) Migrated the rest of the tests.

[1783fc5647d35829ccd7263cbcad6c87dacea420](https://github.com/0xfe/vexflow/commit/1783fc5647d35829ccd7263cbcad6c87dacea420) StaveTests, TabStaveTests, TabSlideTests, BeamTests, BarlineTests

[8d6b344ed627cba6596e6c7ec1cdaa89fc0e590b](https://github.com/0xfe/vexflow/commit/8d6b344ed627cba6596e6c7ec1cdaa89fc0e590b) StaveTests and BarlineTests

[4113c16fd47224bc2c1f215963e8c52e883f74ed](https://github.com/0xfe/vexflow/commit/4113c16fd47224bc2c1f215963e8c52e883f74ed) VibratoTests, VibratoBracketTests, AnnotationTests

[461f6eb485d44948a40ee00f331c28ac4eab1369](https://github.com/0xfe/vexflow/commit/461f6eb485d44948a40ee00f331c28ac4eab1369) StaveTieTests

[fc5d04bfbc81879cb2fbb45f6f013b844d0762c9](https://github.com/0xfe/vexflow/commit/fc5d04bfbc81879cb2fbb45f6f013b844d0762c9) TimeSignatureTests

[e3594aa5c86613dbef39b8032c48e3a46d442f7b](https://github.com/0xfe/vexflow/commit/e3594aa5c86613dbef39b8032c48e3a46d442f7b) StaveConnectorTests, MultiMeasureRestTests, PercussionTests, NoteSubGroupTests.

[5636fc45b019c9050c6bd0cd16bd1b98980faf8b](https://github.com/0xfe/vexflow/commit/5636fc45b019c9050c6bd0cd16bd1b98980faf8b) Articulation Tests.

[0f32e2ea90b74341d8694e77c94db36da563aaf3](https://github.com/0xfe/vexflow/commit/0f32e2ea90b74341d8694e77c94db36da563aaf3) Improve method signatures by adding param types and return types.

[f5bf44afb115477fb2d4b3255783cb69293e8a84](https://github.com/0xfe/vexflow/commit/f5bf44afb115477fb2d4b3255783cb69293e8a84) Clean up uses of vf.* vs VF.*

[4145d20e05a3e21011b0070766f8634bb4e68134](https://github.com/0xfe/vexflow/commit/4145d20e05a3e21011b0070766f8634bb4e68134) ChordSymbol Tests.

[7bd0bec94cf1805e6d55716b8f551a9ebad2e685](https://github.com/0xfe/vexflow/commit/7bd0bec94cf1805e6d55716b8f551a9ebad2e685) KeySignature Tests.

[08bdb20dddae589026c1a8a8889a9defb59afa27](https://github.com/0xfe/vexflow/commit/08bdb20dddae589026c1a8a8889a9defb59afa27) Rhythm & StaveHairpin.

[bc384ea966c7982bc228037934ceb7c96ac1fd37](https://github.com/0xfe/vexflow/commit/bc384ea966c7982bc228037934ceb7c96ac1fd37) Clef Tests.

[a9e49c4f9fd729a31b8b2786106bf55ceff63942](https://github.com/0xfe/vexflow/commit/a9e49c4f9fd729a31b8b2786106bf55ceff63942) Bend, Dot, Tuplet Tests.

[8a7f19acfb6600e94b899fb883c4f85c628a83dc](https://github.com/0xfe/vexflow/commit/8a7f19acfb6600e94b899fb883c4f85c628a83dc) Rename the rest of the JS files.

[98b1a163ec19cd67bd9434c3ee0718b3efc7e0b4](https://github.com/0xfe/vexflow/commit/98b1a163ec19cd67bd9434c3ee0718b3efc7e0b4) Migrate Modifier & TickContext. Discovered small bug in Mocks.js.

[e4ee76cc2f88ac342efdc9c4ecfc3f1f27f0b502](https://github.com/0xfe/vexflow/commit/e4ee76cc2f88ac342efdc9c4ecfc3f1f27f0b502) Rename

[ac962995abcb3cd3565e0ae647980ccb48fc3c3e](https://github.com/0xfe/vexflow/commit/ac962995abcb3cd3565e0ae647980ccb48fc3c3e) Modifier & TickContext

[4d08b1c19f5dfa7678f63eee967725741c0e3554](https://github.com/0xfe/vexflow/commit/4d08b1c19f5dfa7678f63eee967725741c0e3554) Formatter Tests.

[568f6bbfdc36546882f1fd9ff1edfe9300a45809](https://github.com/0xfe/vexflow/commit/568f6bbfdc36546882f1fd9ff1edfe9300a45809) Rename Formatter Tests.

[ebfb24b758e91951a7b8f08a3b8c5f0f7c0ef72a](https://github.com/0xfe/vexflow/commit/ebfb24b758e91951a7b8f08a3b8c5f0f7c0ef72a)  fix return type for minNoteHeadPadding

[2b0749c3d335dc80018db9b9af03b45d2edbe5da](https://github.com/0xfe/vexflow/commit/2b0749c3d335dc80018db9b9af03b45d2edbe5da) Migrate NoteHead and TabNote Tests. Improve EasyScore Tests.

[f6a5d3932e7f7bec61d35e4f6b89bdbc387964ba](https://github.com/0xfe/vexflow/commit/f6a5d3932e7f7bec61d35e4f6b89bdbc387964ba) Rename NoteHead and TabNote Tests.

[11a6a33ee42efd35e7e55a192776cb409e1fbf73](https://github.com/0xfe/vexflow/commit/11a6a33ee42efd35e7e55a192776cb409e1fbf73) Remove references to VexFlowTests where possible.

[fc345353bb691060426ee87282c9da7e6eff8171](https://github.com/0xfe/vexflow/commit/fc345353bb691060426ee87282c9da7e6eff8171) Migrate BoundingBox Tests.

[65f7d4252ff8fec7d4563b5d77e06000a50c6da8](https://github.com/0xfe/vexflow/commit/65f7d4252ff8fec7d4563b5d77e06000a50c6da8) Rename Bounding Box Tests.

[faa5a1710844569d2fe94fd1d87a53775b1fa1d0](https://github.com/0xfe/vexflow/commit/faa5a1710844569d2fe94fd1d87a53775b1fa1d0) More test migration.

[987375b5b6c6dbf8ea6b0f931c3b2cfa96b65d89](https://github.com/0xfe/vexflow/commit/987375b5b6c6dbf8ea6b0f931c3b2cfa96b65d89) Rename TextNoteTests, StaveLineTests, OrnamentTests, PedalMarkingTests, TextBracketTests, StaveModifierTests.

[1484a9b613135e0ced5704ecadd0d93928e1478d](https://github.com/0xfe/vexflow/commit/1484a9b613135e0ced5704ecadd0d93928e1478d) Factory, GhostNote, Style. Fix warnings in Accidental Tests.

[853eee4b4b1e3c7cfed15ec8f8c83eba272c9268](https://github.com/0xfe/vexflow/commit/853eee4b4b1e3c7cfed15ec8f8c83eba272c9268) Rename Factory, GhostNote, Style tests.

[e11e82947abe9bf57ee508e4a0fbb60cecc506cb](https://github.com/0xfe/vexflow/commit/e11e82947abe9bf57ee508e4a0fbb60cecc506cb) Clean up Accidental Tests. Fix small bugs.

[85ec9322e33bd6600318d5d9fcb1cf41bb8bf78a](https://github.com/0xfe/vexflow/commit/85ec9322e33bd6600318d5d9fcb1cf41bb8bf78a) Improve Accidental Tests. Rename VF.Test to VexFlowTests.

[e253bfb11de76ee01de4895128cdcae120ded713](https://github.com/0xfe/vexflow/commit/e253bfb11de76ee01de4895128cdcae120ded713) Fix eslint warnings.

[55125d307d69dfa2ceec2bb3da2c243ad28dffcd](https://github.com/0xfe/vexflow/commit/55125d307d69dfa2ceec2bb3da2c243ad28dffcd) Move shared concat to vexflow_test_helpers. Clean up GlyphNote Tests. Hide build folders from vscode to improve autocomplete / IntelliSense.

[906e3d0119191553b87518f4140d84db538d1582](https://github.com/0xfe/vexflow/commit/906e3d0119191553b87518f4140d84db538d1582) GlyphNote Tests

[be3d9253a435a1a10a4064c9e589b3414ced941c](https://github.com/0xfe/vexflow/commit/be3d9253a435a1a10a4064c9e589b3414ced941c) Rename GlyphNote Tests.

[6151b408f4ae4493432e53e3ca48a2dde615e03c](https://github.com/0xfe/vexflow/commit/6151b408f4ae4493432e53e3ca48a2dde615e03c) Stroke tests.

[9bac348bb7d0d3b963d87fbdde13476c6b2cfb9a](https://github.com/0xfe/vexflow/commit/9bac348bb7d0d3b963d87fbdde13476c6b2cfb9a) Clean up. Fix small bugs exposed by Bach Tests migration. Remove duplicate calls to this.setNotes(...) in Tie related classes.

[60cc37da0b83cf7d833afa76d93fdce5b9cbd93c](https://github.com/0xfe/vexflow/commit/60cc37da0b83cf7d833afa76d93fdce5b9cbd93c) add padding for notes with no modifiers

[a25d25d58612a84048be3446c5b4705b7b300da0](https://github.com/0xfe/vexflow/commit/a25d25d58612a84048be3446c5b4705b7b300da0) Rename Strokes test.

[eafd79668fb4a30b964c5fe3a03ee0ea1c24a268](https://github.com/0xfe/vexflow/commit/eafd79668fb4a30b964c5fe3a03ee0ea1c24a268) Generage PNG images will include both JS files if the src path is releases/ or reference/. It will do it the new way (single JS file) if the src path is build/.

[5ef6233ded32380216726ceaba3615c3d24a8a48](https://github.com/0xfe/vexflow/commit/5ef6233ded32380216726ceaba3615c3d24a8a48) Compute quadratic Beizer bounding box directly.

[367fa05e5e6495df9d74f1fd989fa8a4c716f779](https://github.com/0xfe/vexflow/commit/367fa05e5e6495df9d74f1fd989fa8a4c716f779) generate_png_images.js now only loads vexflow-tests.js TODO: Add a flag to decide whether to load BOTH JS files (the old way), or only one JS file (the new way).

[17be771f54934cf169dd75e45d097a25c596846e](https://github.com/0xfe/vexflow/commit/17be771f54934cf169dd75e45d097a25c596846e) Migrate StaveNote Tests.

[b35aa380fbf197742a21629c8b5292099049468d](https://github.com/0xfe/vexflow/commit/b35aa380fbf197742a21629c8b5292099049468d) Fix errors.

[f3ffac9aa4d0486d5cb4d4cc382da6aa19a2175c](https://github.com/0xfe/vexflow/commit/f3ffac9aa4d0486d5cb4d4cc382da6aa19a2175c) StaveNote Tests.

[aa664dc9f5d8b3c335ffed3783ed98071adf926d](https://github.com/0xfe/vexflow/commit/aa664dc9f5d8b3c335ffed3783ed98071adf926d) Rename StaveNote Tests.

[8c737459b9b648e3465ed6a19d76a09b9616c19a](https://github.com/0xfe/vexflow/commit/8c737459b9b648e3465ed6a19d76a09b9616c19a) Rely on /* eslint-disable */ and // @ts-nocheck to ignore warnings for now.

[e58f335ca2f40560a5b0625a6f833543c95d6e85](https://github.com/0xfe/vexflow/commit/e58f335ca2f40560a5b0625a6f833543c95d6e85) Rename run.js => run.ts.

[c6bc40f04c374d4e12209220922c618dcc94de8a](https://github.com/0xfe/vexflow/commit/c6bc40f04c374d4e12209220922c618dcc94de8a) Rename Three Voice & Voice Tests.

[6ebf776af0130581d84b21c24b820511aa6b3516](https://github.com/0xfe/vexflow/commit/6ebf776af0130581d84b21c24b820511aa6b3516) Rename Parser Tests and StringNumber Tests.

[058ef3bb97fc0696f6841d2b06cf05d22338fd80](https://github.com/0xfe/vexflow/commit/058ef3bb97fc0696f6841d2b06cf05d22338fd80) Registry, Parser, StringNumber, Three Voice.

[21c044c8fd4c0dfec042ef8e9b5cfd6fe444d57d](https://github.com/0xfe/vexflow/commit/21c044c8fd4c0dfec042ef8e9b5cfd6fe444d57d) Fix Glyph.getOutlineBoundingBox.

[eee5ff978ebcae0f080de8a9dcf3dddc64c0389c](https://github.com/0xfe/vexflow/commit/eee5ff978ebcae0f080de8a9dcf3dddc64c0389c) Demo of Node #1072

[ed413671ceb8a4cfe1a179c21b3c488a3fccecd0](https://github.com/0xfe/vexflow/commit/ed413671ceb8a4cfe1a179c21b3c488a3fccecd0) Edit signatures of Renders' constructor to support passing HTMLCanvasElement directly

[4587fbe2ad545ecff1c31723875748a3fb116fd0](https://github.com/0xfe/vexflow/commit/4587fbe2ad545ecff1c31723875748a3fb116fd0) Remove unnecessary validation and the internal variable `elementId` of `Renderer`

[12b95d264532ac0a97f20121b183de52983c6b03](https://github.com/0xfe/vexflow/commit/12b95d264532ac0a97f20121b183de52983c6b03) Fix wrong global definition genereated by Webpack in UMD styles

[6fee6a43841045197ea33f9a2edc48458454d1e5](https://github.com/0xfe/vexflow/commit/6fee6a43841045197ea33f9a2edc48458454d1e5) Rename Registry Tests.

[fc41b0d4c710a4e2571d12f0abe0ecc5adefbc0d](https://github.com/0xfe/vexflow/commit/fc41b0d4c710a4e2571d12f0abe0ecc5adefbc0d) Accidentals.

[aaa9559f857052361aafa272b484bd8340c41d74](https://github.com/0xfe/vexflow/commit/aaa9559f857052361aafa272b484bd8340c41d74) Rename Accidental Tests

[df48a4eaa52702c8b6c173231eb4806920f64291](https://github.com/0xfe/vexflow/commit/df48a4eaa52702c8b6c173231eb4806920f64291) Bach test.

[e6e363409f1ded846ede37452e6b8f90c22f186b](https://github.com/0xfe/vexflow/commit/e6e363409f1ded846ede37452e6b8f90c22f186b) Rename Bach test.

[6981e7e5ce767503e8d103e20c9f0eb209d8aaef](https://github.com/0xfe/vexflow/commit/6981e7e5ce767503e8d103e20c9f0eb209d8aaef) New approach: do not include vexflow-debug.js on flow.html.

[016e652b5b5ec8e518190757296fe3747c1c4880](https://github.com/0xfe/vexflow/commit/016e652b5b5ec8e518190757296fe3747c1c4880) Clean up test titles by removing duplicate word "Rests".

[7006e957a36045797bbba1c59deabcb7a7ff7304](https://github.com/0xfe/vexflow/commit/7006e957a36045797bbba1c59deabcb7a7ff7304) Add setters & getters to RenderContext to maintain compatibility with CanvasRenderingContext2D API.

[722aae3499eb4ac51bf9ec716155701d2485a782](https://github.com/0xfe/vexflow/commit/722aae3499eb4ac51bf9ec716155701d2485a782) Fix dot_shiftY of 128th rests. Other small fixes. Make sure to draw voice2 first.

[51496aac04b5aec60b4c2ee15c61b1ff37a1b47d](https://github.com/0xfe/vexflow/commit/51496aac04b5aec60b4c2ee15c61b1ff37a1b47d) Fix bug in tuplet.ts constructor by calling this.setTupletLocation() so it validates the input. Improve name for helper function: lookAhead => getRestLineForNextNoteGroup(). Improve comments.

[1468bff6c6d198a1228aed6b784ad6d3ab960d58](https://github.com/0xfe/vexflow/commit/1468bff6c6d198a1228aed6b784ad6d3ab960d58) Stave constructor's 4th param needs to be optional. Move ContextBuilder type declaration to renderer.ts.

[1e5e4499c958e3e9a012428b4c4d2ca75603eb6d](https://github.com/0xfe/vexflow/commit/1e5e4499c958e3e9a012428b4c4d2ca75603eb6d) Set reasonable defaults if the noteStruct does not provide clef, octave_shift, or stem_direction. Improve formatting. Clean up code.

[a3f8ebd0f07ef93a55739edd385159809cec53d5](https://github.com/0xfe/vexflow/commit/a3f8ebd0f07ef93a55739edd385159809cec53d5) Migrate Rests Tests.

[0a935006f399c5273454a4fb06522a3bb8d0d323](https://github.com/0xfe/vexflow/commit/0a935006f399c5273454a4fb06522a3bb8d0d323) Rename rests_tests.js => rests_tests.ts

[2315e7aba40a9bd0328ccb0b6c155eeff4489417](https://github.com/0xfe/vexflow/commit/2315e7aba40a9bd0328ccb0b6c155eeff4489417) Merge pull request #1067 from ronyeh/migration/vexflow_test_helpers

[4ca4a7cd73699c69948b740f71b3f970bfd7e59a](https://github.com/0xfe/vexflow/commit/4ca4a7cd73699c69948b740f71b3f970bfd7e59a) Fix font loading.

[c6f3a3d4719e60da2e478c9b8190e88eda9c0def](https://github.com/0xfe/vexflow/commit/c6f3a3d4719e60da2e478c9b8190e88eda9c0def) generate_png_images.js references NODE_FONT_STACKS and vexflow_testoutput. Remove empty helper functions. Use null instead.

[f6c16f5a0f86868b066f62349410b7ed24ac0b2f](https://github.com/0xfe/vexflow/commit/f6c16f5a0f86868b066f62349410b7ed24ac0b2f) Add ContextBuilder type to Renderer.

[893cde469b2900bf254097de69fd0b34ca10a296](https://github.com/0xfe/vexflow/commit/893cde469b2900bf254097de69fd0b34ca10a296) Move TestOptions into vexflow_test_helpers.

[13bc4fc87ee5a1f2865c66e31e8dae0954e86e2d](https://github.com/0xfe/vexflow/commit/13bc4fc87ee5a1f2865c66e31e8dae0954e86e2d) Add support for optionally testing all fonts in vexflow_test_helpers.ts.

[a0248a3439f22e3e05c8d637b499b881c4923b70](https://github.com/0xfe/vexflow/commit/a0248a3439f22e3e05c8d637b499b881c4923b70) Migrate VexFlowTests. Clean up EasyScore tests.

[c23f48573fc6a94691858365e7923e5f27207779](https://github.com/0xfe/vexflow/commit/c23f48573fc6a94691858365e7923e5f27207779) Rename vexflow_test_helpers.js => vexflow_test_helpers.ts

[3eea242fc47c7d540b226e969b6ad6a984ee5f7e](https://github.com/0xfe/vexflow/commit/3eea242fc47c7d540b226e969b6ad6a984ee5f7e) Merge pull request #1068 from rvilarl/feature/fontsLazyLoaded

[bc6a4ec63980692307700f682261c1b0b6d87705](https://github.com/0xfe/vexflow/commit/bc6a4ec63980692307700f682261c1b0b6d87705) lint error: log not used

[927f1c140707213fee92636244e9f3ab3333fee7](https://github.com/0xfe/vexflow/commit/927f1c140707213fee92636244e9f3ab3333fee7) Merge pull request #1069 from rvilarl/feature/defaultLedgerLine

[7acf57454098e8eb7482c0f67192ceefc341887d](https://github.com/0xfe/vexflow/commit/7acf57454098e8eb7482c0f67192ceefc341887d) Merge pull request #1071 from rvilarl/documentation

[92a8bbe0c89d4fd89c9b27644fe9fbee65f4aa7b](https://github.com/0xfe/vexflow/commit/92a8bbe0c89d4fd89c9b27644fe9fbee65f4aa7b) documentation update and #816

[719ab1d761f73ac834a53a074c5aa59c3a7a0837](https://github.com/0xfe/vexflow/commit/719ab1d761f73ac834a53a074c5aa59c3a7a0837) documentation update

[3029e4ead50b1ce33c2ea772eaafe3943a480acd](https://github.com/0xfe/vexflow/commit/3029e4ead50b1ce33c2ea772eaafe3943a480acd) default ledger line style in stave

[4bc3619df76cf35e2e23f3dcbd15a0f148885c19](https://github.com/0xfe/vexflow/commit/4bc3619df76cf35e2e23f3dcbd15a0f148885c19) static implementation synchronous

[5d9b31bf1795072f115b8e8edcf50b12b83debbc](https://github.com/0xfe/vexflow/commit/5d9b31bf1795072f115b8e8edcf50b12b83debbc) dynamic load of fonts.

[ed360f99b2e873657318686e6ac443cf0616e2a3](https://github.com/0xfe/vexflow/commit/ed360f99b2e873657318686e6ac443cf0616e2a3) npm upgrade

[49e68b36fb37705899e35da997349cd491e8b581](https://github.com/0xfe/vexflow/commit/49e68b36fb37705899e35da997349cd491e8b581) Fonsts.XXX is now a function

[7f8bf6303c7851cc061f98ab829a909cfe31da62](https://github.com/0xfe/vexflow/commit/7f8bf6303c7851cc061f98ab829a909cfe31da62) Merge pull request #1066 from rvilarl/documentation

[77a95affb598feea8236c3c86d3bca748ce2c7e8](https://github.com/0xfe/vexflow/commit/77a95affb598feea8236c3c86d3bca748ce2c7e8) Merge pull request #1064 from rvilarl/fix/OSMD

[5ee42541618b55f429f3c5eb40d4341f50777c42](https://github.com/0xfe/vexflow/commit/5ee42541618b55f429f3c5eb40d4341f50777c42) documentation update

[f1581374cdb1d104455db666c1aadbf7d0ae13ae](https://github.com/0xfe/vexflow/commit/f1581374cdb1d104455db666c1aadbf7d0ae13ae) documentation link added

[a6bada2ea55636dcf0ac2038b33f507dd00edfac](https://github.com/0xfe/vexflow/commit/a6bada2ea55636dcf0ac2038b33f507dd00edfac) documentation update

[a68b8c5ab7557a6bf898e7fe5ededf9786bc10e8](https://github.com/0xfe/vexflow/commit/a68b8c5ab7557a6bf898e7fe5ededf9786bc10e8) documentation update

[5f83c3c224039c0eee13fd5d5f3340e93a92e82b](https://github.com/0xfe/vexflow/commit/5f83c3c224039c0eee13fd5d5f3340e93a92e82b) documentation update

[ce4381ba0d2e47553c021273850f53706cc8cf12](https://github.com/0xfe/vexflow/commit/ce4381ba0d2e47553c021273850f53706cc8cf12) documentation update

[983a351d38952de8e70ca497eb9104ac842ba3e0](https://github.com/0xfe/vexflow/commit/983a351d38952de8e70ca497eb9104ac842ba3e0) get accessor not accepted in interface

[b2cdf0568a54c7d2353e7d8f88580d751b4264cd](https://github.com/0xfe/vexflow/commit/b2cdf0568a54c7d2353e7d8f88580d751b4264cd) remove MakeExecption

[6feaba3db7d8477b712caa3d7c7477a58f9447af](https://github.com/0xfe/vexflow/commit/6feaba3db7d8477b712caa3d7c7477a58f9447af) removed unused attribute

[73b01c61ea67c3a8539ec77eec424d2bc6ff5aba](https://github.com/0xfe/vexflow/commit/73b01c61ea67c3a8539ec77eec424d2bc6ff5aba) Merge pull request #1058 from rvilarl/documentation

[ab9aded2985dc50c7926538b3771d9956742084d](https://github.com/0xfe/vexflow/commit/ab9aded2985dc50c7926538b3771d9956742084d) review comments

[c7a1a9be4c251c603d87fb5baf87f271bb14709b](https://github.com/0xfe/vexflow/commit/c7a1a9be4c251c603d87fb5baf87f271bb14709b) documentation update, #865 and #1059

[21b7d41883f8c33c9d268c60f3d1af47d81d7094](https://github.com/0xfe/vexflow/commit/21b7d41883f8c33c9d268c60f3d1af47d81d7094) null resolved and #1059

[b8d1e446a2bdcdd8246ade1dc8aa115be7dc6a72](https://github.com/0xfe/vexflow/commit/b8d1e446a2bdcdd8246ade1dc8aa115be7dc6a72) ?: reviewed

[8c0abca576c71af3ff0c8bccf269c7c7b92685e5](https://github.com/0xfe/vexflow/commit/8c0abca576c71af3ff0c8bccf269c7c7b92685e5) null resolved

[b76afcc02fe47d8943ee51cedabe90d99e48b199](https://github.com/0xfe/vexflow/commit/b76afcc02fe47d8943ee51cedabe90d99e48b199) documentation update

[b4daf410abdd13d5697e985bc6e9fd14bbf79ad5](https://github.com/0xfe/vexflow/commit/b4daf410abdd13d5697e985bc6e9fd14bbf79ad5) documentation update, removal of attributes that were not required

[73f7381cc8b7f3404ebac39b46531cd64cccf052](https://github.com/0xfe/vexflow/commit/73f7381cc8b7f3404ebac39b46531cd64cccf052) documentation update and #1003

[80cff448cf6b12505a8e2e57a369b6a6c26b2c63](https://github.com/0xfe/vexflow/commit/80cff448cf6b12505a8e2e57a369b6a6c26b2c63) documentation update

[e4e81c487a19476ea5f4476e83602af9fc75ad0a](https://github.com/0xfe/vexflow/commit/e4e81c487a19476ea5f4476e83602af9fc75ad0a) documentation update

[c3a48e8bd2126f41ef3f0d7b507b2ef868859188](https://github.com/0xfe/vexflow/commit/c3a48e8bd2126f41ef3f0d7b507b2ef868859188) documentation update

[6c0406c07df2b7b4d4f6097dffab31e74e32fbab](https://github.com/0xfe/vexflow/commit/6c0406c07df2b7b4d4f6097dffab31e74e32fbab) documentation update

[c9836f6457ef0c29b4c26b44e8ce0a021c118bd7](https://github.com/0xfe/vexflow/commit/c9836f6457ef0c29b4c26b44e8ce0a021c118bd7) documentation update

[9c4e75fd20d3d7ccc7745abc7132cf4c4f656d20](https://github.com/0xfe/vexflow/commit/9c4e75fd20d3d7ccc7745abc7132cf4c4f656d20) Merge pull request #1056 from ronyeh/CanvasRenderingContext2DAPI

[4cbfdb1a50ca65601d11e59371187f83569c7aeb](https://github.com/0xfe/vexflow/commit/4cbfdb1a50ca65601d11e59371187f83569c7aeb) Merge pull request #1063 from AaronDavidNewman/master

[74698a0d49411ef7ac44e561f232c597027f4c9f](https://github.com/0xfe/vexflow/commit/74698a0d49411ef7ac44e561f232c597027f4c9f) use formatter.preCalculateMinWidth in system/factory

[8d8137ee0fb8d38eb0cc5dbcea12680cab8cb8d5](https://github.com/0xfe/vexflow/commit/8d8137ee0fb8d38eb0cc5dbcea12680cab8cb8d5) Merge pull request #1055 from AaronDavidNewman/master

[b9ac33df6b15ff870e4fbef428f7f41704489e6d](https://github.com/0xfe/vexflow/commit/b9ac33df6b15ff870e4fbef428f7f41704489e6d) Remove comment.

[eb4f3090f9aae0efe685ad98b4b3fa63def761e1](https://github.com/0xfe/vexflow/commit/eb4f3090f9aae0efe685ad98b4b3fa63def761e1) changes for code review

[31384d4433f0cbbd28ba6a66a6a45ac62dc00702](https://github.com/0xfe/vexflow/commit/31384d4433f0cbbd28ba6a66a6a45ac62dc00702) Merge pull request #1057 from rvilarl/doc/tuning

[aa3be6b43b57a38bd6e9cc1e19f3f6fb96bdd52f](https://github.com/0xfe/vexflow/commit/aa3be6b43b57a38bd6e9cc1e19f3f6fb96bdd52f) Merge pull request #1053 from rvilarl/doc/typedoc

[7be0906c04839e3f9ab6834e4311b198fb14a0c1](https://github.com/0xfe/vexflow/commit/7be0906c04839e3f9ab6834e4311b198fb14a0c1) Merge pull request #1052 from rvilarl/fix/ledgerLines

[dbe1de65949fa95ed5fbd40a317f8947df5649d5](https://github.com/0xfe/vexflow/commit/dbe1de65949fa95ed5fbd40a317f8947df5649d5) Merge pull request #1054 from rvilarl/doc/vibrato

[e9f2b18caf81c30362a3a236104550897456b765](https://github.com/0xfe/vexflow/commit/e9f2b18caf81c30362a3a236104550897456b765) documented, unnecessary protected variables removed

[7946de83eaad4ed6400464dd9377b28075f8db3b](https://github.com/0xfe/vexflow/commit/7946de83eaad4ed6400464dd9377b28075f8db3b) Fix typo in comment.

[50e337f7f55dd31fad8b049df72bb1c1c2c740de](https://github.com/0xfe/vexflow/commit/50e337f7f55dd31fad8b049df72bb1c1c2c740de) Remove debug code.

[15314c85fd70e31e5e4edc659ffaeafbb5ca431d](https://github.com/0xfe/vexflow/commit/15314c85fd70e31e5e4edc659ffaeafbb5ca431d) Clean up code. Add MIT License.

[e4c0fac494e78ae8254061a3bd0f849ad7af8085](https://github.com/0xfe/vexflow/commit/e4c0fac494e78ae8254061a3bd0f849ad7af8085) remove some dead test code

[713e368a2b6de691bd6d240c5ec1dd9a5efcc52f](https://github.com/0xfe/vexflow/commit/713e368a2b6de691bd6d240c5ec1dd9a5efcc52f) Merge https://github.com/0xfe/vexflow

[2bd213cfa7f280a5086135666e465a195134b49f](https://github.com/0xfe/vexflow/commit/2bd213cfa7f280a5086135666e465a195134b49f) Get preCalculateMinTotalWidth to compute correct value

[d45a356cbc89a10d2dc09741d2a07a41d29758c7](https://github.com/0xfe/vexflow/commit/d45a356cbc89a10d2dc09741d2a07a41d29758c7) documentation

[76d9ee9828e48bb0c60f93528f2023680d44bc3f](https://github.com/0xfe/vexflow/commit/76d9ee9828e48bb0c60f93528f2023680d44bc3f) Add setters (.font .fillStyle .strokeStyle) to maintain compatibility with the CanvasRenderingContext2D API.

[4b738255a6b04263b096f24116ddfe094f4fb68f](https://github.com/0xfe/vexflow/commit/4b738255a6b04263b096f24116ddfe094f4fb68f) typedoc complete

[538902708d7fac5e5545643e8eb7d538caf5e3da](https://github.com/0xfe/vexflow/commit/538902708d7fac5e5545643e8eb7d538caf5e3da) Ledger Lines default width 2.0

[6df8a11cf7545eb009a003dd9a89a030cfe02334](https://github.com/0xfe/vexflow/commit/6df8a11cf7545eb009a003dd9a89a030cfe02334) Ledger Lines default to double width

[a6dc98400aeec0bdb611a79a641097b4080b968f](https://github.com/0xfe/vexflow/commit/a6dc98400aeec0bdb611a79a641097b4080b968f) ElementStyle non optional attributes fixed

[f349614538da8633e611e834f1038bfade9a6e54](https://github.com/0xfe/vexflow/commit/f349614538da8633e611e834f1038bfade9a6e54) Merge pull request #1017 from rvilarl/migration/keysignature

[87f9a6241327b42fa36a7726bcd9b9f37c2e24c0](https://github.com/0xfe/vexflow/commit/87f9a6241327b42fa36a7726bcd9b9f37c2e24c0) review comments

[70430382f05244085448160dd64c27d32e5240b5](https://github.com/0xfe/vexflow/commit/70430382f05244085448160dd64c27d32e5240b5) check that this.keySpec is defined

[6b5e950b89d5b505d3d97c5a99f10a5e480f4830](https://github.com/0xfe/vexflow/commit/6b5e950b89d5b505d3d97c5a99f10a5e480f4830) keysignature migrated

[98c1e0602a52d449c5e9a55dad040113f13faa73](https://github.com/0xfe/vexflow/commit/98c1e0602a52d449c5e9a55dad040113f13faa73) keysignature renamed

[af9bc87f97862187cb1620f858811dff63274d19](https://github.com/0xfe/vexflow/commit/af9bc87f97862187cb1620f858811dff63274d19) Merge pull request #1047 from rvilarl/doc/voice

[d6c3a8dfdf14d1fe69e8932f41d1751a7e3412b0](https://github.com/0xfe/vexflow/commit/d6c3a8dfdf14d1fe69e8932f41d1751a7e3412b0) Merge pull request #1048 from ronyeh/TIME4_4

[83853acc6c2f50227ee1df1c7fc0f3ce17c09f3d](https://github.com/0xfe/vexflow/commit/83853acc6c2f50227ee1df1c7fc0f3ce17c09f3d) Merge pull request #1032 from rvilarl/migration/factory

[fe119060eefeb6fa79f7b019e20ad469b7aa3aec](https://github.com/0xfe/vexflow/commit/fe119060eefeb6fa79f7b019e20ad469b7aa3aec) Merge pull request #1018 from rvilarl/migration/keymanager

[090ca99db64fd9eadd9c9fa67715f06c41dd2a99](https://github.com/0xfe/vexflow/commit/090ca99db64fd9eadd9c9fa67715f06c41dd2a99) review comments

[d66c99ef83e000b564fa8db225dae835381f76f1](https://github.com/0xfe/vexflow/commit/d66c99ef83e000b564fa8db225dae835381f76f1) VoiceGroup Removed and Voice Documented

[1801b9f294c951d11671c2133127d92b184501cc](https://github.com/0xfe/vexflow/commit/1801b9f294c951d11671c2133127d92b184501cc) Replace VF.Test.TIME4_4 with VF.TIME4_4. VF.Test.TIME4_4 is undefined.

[d66f28efbb3d2ae3763fdfa0d9e4981e28446ec3](https://github.com/0xfe/vexflow/commit/d66f28efbb3d2ae3763fdfa0d9e4981e28446ec3) system resolved in factory

[533adedcc433b9d0167b470fa94fc63c7ef6ba56](https://github.com/0xfe/vexflow/commit/533adedcc433b9d0167b470fa94fc63c7ef6ba56) background optional in getCanvasContext & getSVGContext

[8b4354b50bb0668fee5a3b9075fc631afb55ff95](https://github.com/0xfe/vexflow/commit/8b4354b50bb0668fee5a3b9075fc631afb55ff95) review comments

[25b6f216fd934bf231d99b0d90ab0ebef5517eb1](https://github.com/0xfe/vexflow/commit/25b6f216fd934bf231d99b0d90ab0ebef5517eb1) multimeasurerest resolved in factory

[9f76cfe3d470f1a0dee560be0835a0c3b0d6d9e5](https://github.com/0xfe/vexflow/commit/9f76cfe3d470f1a0dee560be0835a0c3b0d6d9e5) chordsymbol interface fixed

[beabb9cca2236ebb121978d20260099d20334dba](https://github.com/0xfe/vexflow/commit/beabb9cca2236ebb121978d20260099d20334dba) factory&renderer migrated

[22866a86e55dbb5ec107f0d5d89774af6b0e842a](https://github.com/0xfe/vexflow/commit/22866a86e55dbb5ec107f0d5d89774af6b0e842a) factory&renderer renamed

[b9455f59d5a2818e8646452fa12752ad53fa2567](https://github.com/0xfe/vexflow/commit/b9455f59d5a2818e8646452fa12752ad53fa2567) review comments

[5a4d0a9bb3e5bfa7ce6e17b9cadda3a2f8e0686d](https://github.com/0xfe/vexflow/commit/5a4d0a9bb3e5bfa7ce6e17b9cadda3a2f8e0686d) KeyParts defined

[6f543fdc2aae9d3ac7e41eec3480132bfbda5915](https://github.com/0xfe/vexflow/commit/6f543fdc2aae9d3ac7e41eec3480132bfbda5915) keymanager migrated

[4fa33339310f440914771a54f4aac630f80ae571](https://github.com/0xfe/vexflow/commit/4fa33339310f440914771a54f4aac630f80ae571) keymanager renamed

[f8967def06c2a710658ede34d43413835f4aea0f](https://github.com/0xfe/vexflow/commit/f8967def06c2a710658ede34d43413835f4aea0f) Merge pull request #1046 from ronyeh/flow.ts

[149c0d4ed69181127a2887a5869153cdb9b700dd](https://github.com/0xfe/vexflow/commit/149c0d4ed69181127a2887a5869153cdb9b700dd) Merge pull request #1031 from rvilarl/migration/accidental

[05696186fc0a64fefedce28370e7a4ec09fdaab0](https://github.com/0xfe/vexflow/commit/05696186fc0a64fefedce28370e7a4ec09fdaab0) Merge pull request #1019 from rvilarl/migration/system

[ae61d1e0fa76b45300763dbe987acd44c3e52ae2](https://github.com/0xfe/vexflow/commit/ae61d1e0fa76b45300763dbe987acd44c3e52ae2) ?? 0 removed

[8860b9c028a3fee6ce79964d2c6f499a3d272488](https://github.com/0xfe/vexflow/commit/8860b9c028a3fee6ce79964d2c6f499a3d272488) ?. replaced by check

[e4733049a97be68328948a61bb2944eeb7b8eef8](https://github.com/0xfe/vexflow/commit/e4733049a97be68328948a61bb2944eeb7b8eef8) type Line must stay global

[c2dfe8af8950ccdb5b8c31af128c72b8bbc0bff6](https://github.com/0xfe/vexflow/commit/c2dfe8af8950ccdb5b8c31af128c72b8bbc0bff6) Review comments

[f923a9d2ea64b08c1f957d2960b9bc2c4c879c95](https://github.com/0xfe/vexflow/commit/f923a9d2ea64b08c1f957d2960b9bc2c4c879c95) accidentalColumnsTable type defined

[dd60164f21258ab781dac90d36550483ba0562d1](https://github.com/0xfe/vexflow/commit/dd60164f21258ab781dac90d36550483ba0562d1) review comments

[660a6ebd1ad29c1dfa4606811785785274e5dcb2](https://github.com/0xfe/vexflow/commit/660a6ebd1ad29c1dfa4606811785785274e5dcb2) accidental migrated

[1be5d2fa7bbc3cd4a4a2c7e5f2cf4e67d5611d09](https://github.com/0xfe/vexflow/commit/1be5d2fa7bbc3cd4a4a2c7e5f2cf4e67d5611d09) accidental renamed

[a5aaf2a9d07ebcbddc92da88ac060e1ad6d46f2a](https://github.com/0xfe/vexflow/commit/a5aaf2a9d07ebcbddc92da88ac060e1ad6d46f2a) review comments

[9cc29d28f1a7ee1ff65aad0ec4b3afa99a148590](https://github.com/0xfe/vexflow/commit/9cc29d28f1a7ee1ff65aad0ec4b3afa99a148590) Partial used to remove XXXItems

[a98b63d911f4ebd3b0a53f29d420ff5b697e7299](https://github.com/0xfe/vexflow/commit/a98b63d911f4ebd3b0a53f29d420ff5b697e7299) system migrated

[1c6f5eafd51c72174ef65055a154ebf2cd4bd056](https://github.com/0xfe/vexflow/commit/1c6f5eafd51c72174ef65055a154ebf2cd4bd056) system renamed

[c279530a48702de45fb66c6e519c2eb30edae9b3](https://github.com/0xfe/vexflow/commit/c279530a48702de45fb66c6e519c2eb30edae9b3) Use shorthand property names. Sort imports and keys.

[cdf30ae7daa6206f1447a24ef4ee7cb473696ddc](https://github.com/0xfe/vexflow/commit/cdf30ae7daa6206f1447a24ef4ee7cb473696ddc) Merge pull request #1044 from AaronDavidNewman/master

[01f4cdfce494c8831bf756d61983dca8456a1d0e](https://github.com/0xfe/vexflow/commit/01f4cdfce494c8831bf756d61983dca8456a1d0e) fix formatting merge bug

[1beaa3ab10ee20186691b971fa9c58b385937d73](https://github.com/0xfe/vexflow/commit/1beaa3ab10ee20186691b971fa9c58b385937d73) Merge pull request #1029 from ronyeh/webpack-define

[5463be0ea2570d54ba47f58c66c60b599b7f2b32](https://github.com/0xfe/vexflow/commit/5463be0ea2570d54ba47f58c66c60b599b7f2b32) Use TerserPlugin to tell webpack 5 to not extract the banner into a separate file: vexflow-min.js.LICENSE.txt

[5a8c02363e1a4728340740f08320a16f4c1e1cbe](https://github.com/0xfe/vexflow/commit/5a8c02363e1a4728340740f08320a16f4c1e1cbe) eslint autoformatted two files.

[26207af89a98a2b1aecb2780d7c7f0d5cc601a87](https://github.com/0xfe/vexflow/commit/26207af89a98a2b1aecb2780d7c7f0d5cc601a87) Clean up Gruntfile.js.

[10503767852cc652ac35507004cccf968160f2d9](https://github.com/0xfe/vexflow/commit/10503767852cc652ac35507004cccf968160f2d9) npm install to update package-lock.json.

[4dcb7feb8f7c05add68a31879d6496b2ec8bdef7](https://github.com/0xfe/vexflow/commit/4dcb7feb8f7c05add68a31879d6496b2ec8bdef7) Use webpack-inject-plugin to inject Vex.Flow.VERSION, Vex.Flow.BUILD, Vex.Flow.Test.VERSION, and Vex.Flow.Test.BUILD.

[7880a4e475d5e96c9e56fdb3ff9ea8319cfbfe7a](https://github.com/0xfe/vexflow/commit/7880a4e475d5e96c9e56fdb3ff9ea8319cfbfe7a) Fix build errors by adding version.js. Remove header.js. Credit font creators at the top of each font metrics file.

[fd1b85674eb771a748dde75b9f61082e2290a953](https://github.com/0xfe/vexflow/commit/fd1b85674eb771a748dde75b9f61082e2290a953) Add Vex.Flow.VERSION and Vex.Flow.BUILD via webpack.DefinePlugin. Add banner with version, build timestamp, and git hash via webpack.BannerPlugin.

[605b9a7bc15ec2eb687fd17c49ab87199b698999](https://github.com/0xfe/vexflow/commit/605b9a7bc15ec2eb687fd17c49ab87199b698999) Merge pull request #1041 from rvilarl/migration/update

[0802a9918cfa9fefca129b84f4dfda397d4a3604](https://github.com/0xfe/vexflow/commit/0802a9918cfa9fefca129b84f4dfda397d4a3604) npm-upgrade

[01ea34f3b1c4101ca12b623be84be161cab9a2fc](https://github.com/0xfe/vexflow/commit/01ea34f3b1c4101ca12b623be84be161cab9a2fc) webpack & ts-loader updated

[110100f544bcb3567099f73885c99a882dfd32c0](https://github.com/0xfe/vexflow/commit/110100f544bcb3567099f73885c99a882dfd32c0) typedoc update

[51aac328f30a56006355e7eba5e441e01460c8ab](https://github.com/0xfe/vexflow/commit/51aac328f30a56006355e7eba5e441e01460c8ab) Merge pull request #1038 from AaronDavidNewman/master

[f305f6cd1d3c0bf88f4c02ce24989109f80d4303](https://github.com/0xfe/vexflow/commit/f305f6cd1d3c0bf88f4c02ce24989109f80d4303) Merge pull request #1009 from rvilarl/migration/vex

[ef50228181647d1da9fb3c1854c4f304065df341](https://github.com/0xfe/vexflow/commit/ef50228181647d1da9fb3c1854c4f304065df341) review comments

[e843206f36369cd99cdf89d438edc18127debf2e](https://github.com/0xfe/vexflow/commit/e843206f36369cd99cdf89d438edc18127debf2e) Flow.ts added

[1d72fa40a5306e465fdfc966d3c0f2dd8a766909](https://github.com/0xfe/vexflow/commit/1d72fa40a5306e465fdfc966d3c0f2dd8a766909) common.ts deleted

[ba0518448695760f6fee2c273af0add97ba287b7](https://github.com/0xfe/vexflow/commit/ba0518448695760f6fee2c273af0add97ba287b7) review comments

[164f4f28115bfcb37b7792e3846b973033aaf7c7](https://github.com/0xfe/vexflow/commit/164f4f28115bfcb37b7792e3846b973033aaf7c7) remove duplicates from util

[fbfe96c590021c8624352ece7d8f9f648a4d4709](https://github.com/0xfe/vexflow/commit/fbfe96c590021c8624352ece7d8f9f648a4d4709) vex&tables migrated

[f855cdfc7fc33e624da3ade59ab6558c48af4a03](https://github.com/0xfe/vexflow/commit/f855cdfc7fc33e624da3ade59ab6558c48af4a03) tables renamed

[57e43fa4256149f232c6119450f81c62f14abff6](https://github.com/0xfe/vexflow/commit/57e43fa4256149f232c6119450f81c62f14abff6) vex renamed

[267e350c0987cb53e960954976180f0479f03ebd](https://github.com/0xfe/vexflow/commit/267e350c0987cb53e960954976180f0479f03ebd) Merge pull request #1027 from ronyeh/migration/canvascontext

[4fabaa36314a8a22144f1577e7f83d5360beb145](https://github.com/0xfe/vexflow/commit/4fabaa36314a8a22144f1577e7f83d5360beb145) Merge pull request #1040 from eliot-akira/check-empty-array

[f8ea52054487f235aea9e83c50635c5eab41f13a](https://github.com/0xfe/vexflow/commit/f8ea52054487f235aea9e83c50635c5eab41f13a) Correctly check for empty array

[e5a5676b958325d2e7a9c8c0dd2f157e0c2cf602](https://github.com/0xfe/vexflow/commit/e5a5676b958325d2e7a9c8c0dd2f157e0c2cf602) Fix issues due to rebasing from / merging with upstream.

[030fb7d749f47c24e7c05edfbb418ba14c2476b6](https://github.com/0xfe/vexflow/commit/030fb7d749f47c24e7c05edfbb418ba14c2476b6) Fix: CanvasRenderingContext2D.measureText() does not have a height field. Instead, estimate the height by measuring the width of the letter M.

[23cd4884d35a696b9d7a7bff234d807dd72cd5d8](https://github.com/0xfe/vexflow/commit/23cd4884d35a696b9d7a7bff234d807dd72cd5d8) Migrate CanvasContext. Fix some types, e.g., shadowBlur.

[028ab905db4fc8eb0fc6abb1a4eb9063f84e0cbb](https://github.com/0xfe/vexflow/commit/028ab905db4fc8eb0fc6abb1a4eb9063f84e0cbb) Reduce duplicate code in vexflow_test_helpers.

[24f08df91a8e26ae980d1e32075f5ff2a244aded](https://github.com/0xfe/vexflow/commit/24f08df91a8e26ae980d1e32075f5ff2a244aded) Rename CanvasContext.

[67a7f45b8e1efcace665a56d8804c66bbfce5fab](https://github.com/0xfe/vexflow/commit/67a7f45b8e1efcace665a56d8804c66bbfce5fab) Add additional padding to left of accidentals

[736b65491894a128c63c39e5d24252b4bb151ee3](https://github.com/0xfe/vexflow/commit/736b65491894a128c63c39e5d24252b4bb151ee3) Merge pull request #1037 from AaronDavidNewman/master

[4e6df4f00ca17959931892a3db7139ecbfa66ab5](https://github.com/0xfe/vexflow/commit/4e6df4f00ca17959931892a3db7139ecbfa66ab5) changes for code review

[8e33074e39a429ce40748650c833f09dbc88dd29](https://github.com/0xfe/vexflow/commit/8e33074e39a429ce40748650c833f09dbc88dd29) Merge pull request #1036 from rvilarl/migration/multimeasurerest

[ef4e39428361731735414fe2818e36dbe93070a3](https://github.com/0xfe/vexflow/commit/ef4e39428361731735414fe2818e36dbe93070a3) remove unused metrics, fix cut/paste error

[30739792e19ae611c138537f5f94884ca24e5fd7](https://github.com/0xfe/vexflow/commit/30739792e19ae611c138537f5f94884ca24e5fd7) Merge branch 'master' of https://github.com/0xfe/vexflow

[b328fcdd7f55fd3c22a07590d30b55e6b2cc574d](https://github.com/0xfe/vexflow/commit/b328fcdd7f55fd3c22a07590d30b55e6b2cc574d) partially address issue 846

[fa6641af53e69b333cc748ba852bcfd0d699acc0](https://github.com/0xfe/vexflow/commit/fa6641af53e69b333cc748ba852bcfd0d699acc0) timeSig to timeSigInfo

[7e8fbeb952cbcd802494df0fe4b580385796e799](https://github.com/0xfe/vexflow/commit/7e8fbeb952cbcd802494df0fe4b580385796e799) getTimeSig to getInfo, TimeSignature.timeSig to TimeSignature.info

[d8a02bd117f0083dfe6326079c08e24f38da432e](https://github.com/0xfe/vexflow/commit/d8a02bd117f0083dfe6326079c08e24f38da432e) Merge pull request #1035 from rvilarl/migration/multimeasurerest

[7a64beac9f2a9de24da51b7451ebd2956d729114](https://github.com/0xfe/vexflow/commit/7a64beac9f2a9de24da51b7451ebd2956d729114) multimeasurerest fix

[a85a83276a3ce27adf76e2a0fc3bf5c8792fb405](https://github.com/0xfe/vexflow/commit/a85a83276a3ce27adf76e2a0fc3bf5c8792fb405) Merge pull request #1024 from rvilarl/migration/chordsymbol

[1622d5b38479ccbf811f8e4ad2ef810adf5dc6bc](https://github.com/0xfe/vexflow/commit/1622d5b38479ccbf811f8e4ad2ef810adf5dc6bc) Merge pull request #1033 from ronyeh/delete/raphaelcontext

[d050050b6e1c3686bb8533fdfadc856de43d3617](https://github.com/0xfe/vexflow/commit/d050050b6e1c3686bb8533fdfadc856de43d3617) Merge pull request #1025 from ronyeh/migration/test/easyscore

[6058799728baa0b4a613d5b07ef1194225ff90c8](https://github.com/0xfe/vexflow/commit/6058799728baa0b4a613d5b07ef1194225ff90c8) Merge pull request #1021 from rvilarl/migration/ornament

[6075f71b53232c20526caa695fd8155895888373](https://github.com/0xfe/vexflow/commit/6075f71b53232c20526caa695fd8155895888373) Merge remote-tracking branch 'upstream/master' into migration/test/easyscore Resolve conflict.

[c3c7d143bf363603e5e86ade8ce8b00ff47dfc72](https://github.com/0xfe/vexflow/commit/c3c7d143bf363603e5e86ade8ce8b00ff47dfc72) Remove Raphael.

[0fef634f6f9c420993c9c5b43fdee973e4da571f](https://github.com/0xfe/vexflow/commit/0fef634f6f9c420993c9c5b43fdee973e4da571f) review comments

[e21840a54f26fdbb9b117b86a09b92bf3efc94d9](https://github.com/0xfe/vexflow/commit/e21840a54f26fdbb9b117b86a09b92bf3efc94d9) review comments

[de2f6d8d9eb6dbf9359f319333dca8178bf4ef6f](https://github.com/0xfe/vexflow/commit/de2f6d8d9eb6dbf9359f319333dca8178bf4ef6f) Merge pull request #1012 from rvilarl/migration/multimeasurerest

[9f3ebe1fc8f19a5c1c2e0ee840e766156db298c0](https://github.com/0xfe/vexflow/commit/9f3ebe1fc8f19a5c1c2e0ee840e766156db298c0) Merge pull request #1023 from rvilarl/migration/util

[41f144add7af45215db15a9b9f6506299caf7877](https://github.com/0xfe/vexflow/commit/41f144add7af45215db15a9b9f6506299caf7877) review comments

[5ccdf2e48fd1d559875a33d70e0f9832bb858bf7](https://github.com/0xfe/vexflow/commit/5ccdf2e48fd1d559875a33d70e0f9832bb858bf7) multimeasurerest migrated

[fa31af9be9811058b00224c65c13b32a72a15b9f](https://github.com/0xfe/vexflow/commit/fa31af9be9811058b00224c65c13b32a72a15b9f) multimeasurerest renamed

[edb6a67e68b9c97af2092ec73b9808ab494badf6](https://github.com/0xfe/vexflow/commit/edb6a67e68b9c97af2092ec73b9808ab494badf6) chordsymbol migrated

[9587d9e4650479923f83fb4496eb7a9de18fc7f9](https://github.com/0xfe/vexflow/commit/9587d9e4650479923f83fb4496eb7a9de18fc7f9) chordsymbol renamed

[a45e51faf60b23f3c6b659143f96989d28d2f09e](https://github.com/0xfe/vexflow/commit/a45e51faf60b23f3c6b659143f96989d28d2f09e) MakeException, midLine, drawDot, prefix

[fe151b3722248a25a0fbe9e5a5840a3faf3ac4a1](https://github.com/0xfe/vexflow/commit/fe151b3722248a25a0fbe9e5a5840a3faf3ac4a1) Merge pull request #1028 from ronyeh/fix/defaultfontstack

[1acece96b1272c1ec05ef8c6b88d3bb806ea0877](https://github.com/0xfe/vexflow/commit/1acece96b1272c1ec05ef8c6b88d3bb806ea0877) Remove flag for testing all fonts, since we now do visual diffs for all fonts by default.

[1f64a2b6a540e7656e8c70b94fd07c88e0c30a1c](https://github.com/0xfe/vexflow/commit/1f64a2b6a540e7656e8c70b94fd07c88e0c30a1c) Fix eslint warnings.

[a5c653af35fc0e9c7467586892ff7fb448ee3be8](https://github.com/0xfe/vexflow/commit/a5c653af35fc0e9c7467586892ff7fb448ee3be8) Run visual diff for all three fonts by default.

[abb0ad15094760e8ddbd096d4d0ade16436c1ecf](https://github.com/0xfe/vexflow/commit/abb0ad15094760e8ddbd096d4d0ade16436c1ecf) Use Flow.DEFAULT_FONT_STACK instead of DefaultFontStack, to allow developers to customize the music font. Test all three fonts with visual diffs by default.

[893df69a0a086f74514bf578c39c3260ad2115ae](https://github.com/0xfe/vexflow/commit/893df69a0a086f74514bf578c39c3260ad2115ae) Add eslint-disable-next-line for `any`.

[7ffd6d3d5aee7d2e32e7899a4fe41e63c87b7b8e](https://github.com/0xfe/vexflow/commit/7ffd6d3d5aee7d2e32e7899a4fe41e63c87b7b8e) Remove console.log.

[18090bdb4f42233d49729b6f084d3546d8723324](https://github.com/0xfe/vexflow/commit/18090bdb4f42233d49729b6f084d3546d8723324) Remove unused RuntimeError. Comment out global Vex.Flow.Test.EasyScore.

[14afdf8cbc39f9bed9266ecbca25ee60c9abe253](https://github.com/0xfe/vexflow/commit/14afdf8cbc39f9bed9266ecbca25ee60c9abe253) Migrate EasyScoreTests.

[08b75a3c1a5229b7eca17d469326ba3a7f326421](https://github.com/0xfe/vexflow/commit/08b75a3c1a5229b7eca17d469326ba3a7f326421) Rename easyscore_tests.js => .ts.

[ddffee2097902766b0ec78cff710172f54a4a28f](https://github.com/0xfe/vexflow/commit/ddffee2097902766b0ec78cff710172f54a4a28f) ornament migrated

[8af96ed58279f529c48b6e81c490dc7350cc9bff](https://github.com/0xfe/vexflow/commit/8af96ed58279f529c48b6e81c490dc7350cc9bff) ornament renamed

[2c77ad2af0a5cc79ba5857d3c640b6dd1280741d](https://github.com/0xfe/vexflow/commit/2c77ad2af0a5cc79ba5857d3c640b6dd1280741d) Merge pull request #1002 from ronyeh/modifier-index

[bc08be994871b5bd1b186939c6dfd1cce04d46c7](https://github.com/0xfe/vexflow/commit/bc08be994871b5bd1b186939c6dfd1cce04d46c7) Remove unused RuntimError

[fd9a0190434afdf4bb78a3214c4c809b67b4eb9c](https://github.com/0xfe/vexflow/commit/fd9a0190434afdf4bb78a3214c4c809b67b4eb9c) Merge branch 'master' into modifier-index

[268cd9a08438f569626afd07ac944a9cd2e3ce96](https://github.com/0xfe/vexflow/commit/268cd9a08438f569626afd07ac944a9cd2e3ce96) Merge pull request #1006 from ronyeh/migration/svgcontext

[3110a30cf55617b5f4488098d1b41ccec78420d0](https://github.com/0xfe/vexflow/commit/3110a30cf55617b5f4488098d1b41ccec78420d0) Merge pull request #1011 from rvilarl/migration/util

[807ad7ff2fc6d33ff03a9d693cdf52d427db0b5b](https://github.com/0xfe/vexflow/commit/807ad7ff2fc6d33ff03a9d693cdf52d427db0b5b) Review comments

[604d5bcb2c4cb7138be217a1466e32d630caa047](https://github.com/0xfe/vexflow/commit/604d5bcb2c4cb7138be217a1466e32d630caa047) Code review comments. Inline simple types. (e.g., Point => {x: number, y: number}). Add return types to methods missing return types.

[83771319dc0851efe5dbd598962c7a86610917bd](https://github.com/0xfe/vexflow/commit/83771319dc0851efe5dbd598962c7a86610917bd) Merge remote-tracking branch 'upstream/master' into migration/svgcontext

[66a760dc84ba6b4da9994474bcb7c9e93fe77e5b](https://github.com/0xfe/vexflow/commit/66a760dc84ba6b4da9994474bcb7c9e93fe77e5b) Merge: fix conflict.

[acef88e3058c68202f133cee475cd54d73212550](https://github.com/0xfe/vexflow/commit/acef88e3058c68202f133cee475cd54d73212550) Fix #1000 https://github.com/0xfe/vexflow/issues/1000

[4a3f4c20d65f74a119de8845276f5e6198d3c5a8](https://github.com/0xfe/vexflow/commit/4a3f4c20d65f74a119de8845276f5e6198d3c5a8) Remove comments that are redundant / incorrect / have typos.

[a8b567493a7b8d4ceccae1cf1419dc926154c498](https://github.com/0xfe/vexflow/commit/a8b567493a7b8d4ceccae1cf1419dc926154c498) review comments

[846093561de4aa2b2630e277a2771211e1650ea7](https://github.com/0xfe/vexflow/commit/846093561de4aa2b2630e277a2771211e1650ea7) DefaultFontStack

[6b7fe6b2652b92182a3620d0b59c30a0107087bb](https://github.com/0xfe/vexflow/commit/6b7fe6b2652b92182a3620d0b59c30a0107087bb) merge in TextFont resolved

[c6628f0514c8a8f7aa7b8110a3369ddb19ea0fa7](https://github.com/0xfe/vexflow/commit/c6628f0514c8a8f7aa7b8110a3369ddb19ea0fa7) merge

[794669fab0d12895871ee3a014aabc5a0083ca88](https://github.com/0xfe/vexflow/commit/794669fab0d12895871ee3a014aabc5a0083ca88) log, warn, max, min

[afcbae29d1c4de3cb0cfa0dcbd1accd117f08394](https://github.com/0xfe/vexflow/commit/afcbae29d1c4de3cb0cfa0dcbd1accd117f08394) Merge pull request #1015 from ronyeh/tests/flow.html

[e41741efa8e6b6dc7ce43d00c14bccdb15f37994](https://github.com/0xfe/vexflow/commit/e41741efa8e6b6dc7ce43d00c14bccdb15f37994) Merge pull request #1014 from ronyeh/fix/for-loop

[130f27e82e81805ad19a8cd6faf6aa65008a1d39](https://github.com/0xfe/vexflow/commit/130f27e82e81805ad19a8cd6faf6aa65008a1d39) Merge pull request #1016 from ronyeh/barlinetype

[4c19f9bc60938f73a55110644cca322a8360bf8e](https://github.com/0xfe/vexflow/commit/4c19f9bc60938f73a55110644cca322a8360bf8e) Fix formatting.

[981bc435bbb99a9d7eb5193a51af98621214bdfa](https://github.com/0xfe/vexflow/commit/981bc435bbb99a9d7eb5193a51af98621214bdfa) Replace instances of Barline.type with BarlineType. Tests remain unchanged for now.

[8bb45ee2904f3e8f0c22df561aa1431a895df3de](https://github.com/0xfe/vexflow/commit/8bb45ee2904f3e8f0c22df561aa1431a895df3de) Address code review comments. Replace Vex.Merge with ... object spread operator.

[d1e9306091cebbbd0e2e805352495cafbdfcd42e](https://github.com/0xfe/vexflow/commit/d1e9306091cebbbd0e2e805352495cafbdfcd42e) Change render_options.line_dash type to number[]. It was incorrectly typed as string. Introduce RenderOptions interface to reduce duplicate code. Add Point type.

[d33da34c7780d62e7eb6409c476aa80aadf4c7c4](https://github.com/0xfe/vexflow/commit/d33da34c7780d62e7eb6409c476aa80aadf4c7c4) Show a link to the VexFlow source file.

[a6d2ade2139adc2c6cfd4731f2c2b1418e845a33](https://github.com/0xfe/vexflow/commit/a6d2ade2139adc2c6cfd4731f2c2b1418e845a33) Add ver=XXX query param to flow.html to allow switching between different vexflow builds.

[1d7bbd9d7c0d7d08c71ed15f9fd9d823896fecfc](https://github.com/0xfe/vexflow/commit/1d7bbd9d7c0d7d08c71ed15f9fd9d823896fecfc) Comment. Currently exploring the correct typings for ctx.setLineDash(render_options.line_dash);

[49f6754f19125461b58f6f4dc1c32ef68c2165c5](https://github.com/0xfe/vexflow/commit/49f6754f19125461b58f6f4dc1c32ef68c2165c5) Fix issue https://github.com/0xfe/vexflow/issues/1013

[996c00812a31a99bd22cb4638d8f11ad57680d39](https://github.com/0xfe/vexflow/commit/996c00812a31a99bd22cb4638d8f11ad57680d39) Merge remote-tracking branch 'upstream/master' into migration/svgcontext

[e21a8d66dd9fc709c09697b57738fd0f5a33064c](https://github.com/0xfe/vexflow/commit/e21a8d66dd9fc709c09697b57738fd0f5a33064c) Return note from this.checkAttachedNote() so we can reference it in the rest of the draw() method.

[50dd9ebc84b6bf5637fc55a1174f0d210cfd7e26](https://github.com/0xfe/vexflow/commit/50dd9ebc84b6bf5637fc55a1174f0d210cfd7e26) Add Modifier.checkIndex() to check that index is not undefined.

[e942f85da0572d84c1ec93eddf12d6c4e8c907e7](https://github.com/0xfe/vexflow/commit/e942f85da0572d84c1ec93eddf12d6c4e8c907e7) Merge remote-tracking branch 'upstream/master' into modifier-index Modifier's this.index is optionally undefined.

[faf894c4adb650b864d7a10ab02e904fde5fd60e](https://github.com/0xfe/vexflow/commit/faf894c4adb650b864d7a10ab02e904fde5fd60e) Merge pull request #1010 from rvilarl/migration/util

[34b4975b52e353f44a63ae4b7244564b7483f39e](https://github.com/0xfe/vexflow/commit/34b4975b52e353f44a63ae4b7244564b7483f39e) RuntimeError

[64223d0ea4ce41d89f256174d11236cfae71f079](https://github.com/0xfe/vexflow/commit/64223d0ea4ce41d89f256174d11236cfae71f079) Merge pull request #1001 from ronyeh/migration/notesubgroup

[94fc2d88c05edbeeb64d40781199f361c5e1e6c0](https://github.com/0xfe/vexflow/commit/94fc2d88c05edbeeb64d40781199f361c5e1e6c0) Merge pull request #993 from rvilarl/migration/stavehairpin

[a8e11718bedfd441f9eab9cea6fded118edaad68](https://github.com/0xfe/vexflow/commit/a8e11718bedfd441f9eab9cea6fded118edaad68) Code review from 0xfe.

[723c969c0ec9328982f429a8a13be81a266386b2](https://github.com/0xfe/vexflow/commit/723c969c0ec9328982f429a8a13be81a266386b2) Merge remote-tracking branch 'upstream/master' into migration/notesubgroup

[cb019c41302d66033d91b8477fea3779f21791d2](https://github.com/0xfe/vexflow/commit/cb019c41302d66033d91b8477fea3779f21791d2) review comments

[0b1684e2efa1d1403b58c41a1e624f643b4f0a69](https://github.com/0xfe/vexflow/commit/0b1684e2efa1d1403b58c41a1e624f643b4f0a69) stavehairpin migrated

[f6b93dec03656c42d31a1f3da07cbeffd4742396](https://github.com/0xfe/vexflow/commit/f6b93dec03656c42d31a1f3da07cbeffd4742396) stavehairpin renamed

[1867140f5aa53db491147cbce3d80b677515d132](https://github.com/0xfe/vexflow/commit/1867140f5aa53db491147cbce3d80b677515d132) Merge pull request #1005 from ronyeh/fix/music.ts

[467e63d2c6cd0455a617c8bb501fd5995ec5c41e](https://github.com/0xfe/vexflow/commit/467e63d2c6cd0455a617c8bb501fd5995ec5c41e) Merge pull request #997 from rvilarl/migration/pedalmarking

[e32c93a9c3703dd575c184b20d63506718e70214](https://github.com/0xfe/vexflow/commit/e32c93a9c3703dd575c184b20d63506718e70214) Merge pull request #991 from rvilarl/migration/strokes

[0387d1847d2f599fb95a348fd72d038196274de5](https://github.com/0xfe/vexflow/commit/0387d1847d2f599fb95a348fd72d038196274de5) Merge pull request #995 from AaronDavidNewman/master

[f5bb3f287c344484a6428efbc0c15d876d7846aa](https://github.com/0xfe/vexflow/commit/f5bb3f287c344484a6428efbc0c15d876d7846aa) Merge pull request #989 from rvilarl/migration/staveline

[59d81088ec55c5d56f14e3d03daecd8230c197a3](https://github.com/0xfe/vexflow/commit/59d81088ec55c5d56f14e3d03daecd8230c197a3) Merge pull request #979 from rvilarl/migration/formatter2

[7d0b7feafc12956ad0b3f997ca2694a69276ceca](https://github.com/0xfe/vexflow/commit/7d0b7feafc12956ad0b3f997ca2694a69276ceca) Merge pull request #1007 from rvilarl/migration/typedoc

[08f205df7ec547f58048ba6e7b17a96d0f95dce2](https://github.com/0xfe/vexflow/commit/08f205df7ec547f58048ba6e7b17a96d0f95dce2) Merge pull request #999 from ronyeh/migration/easyscore2

[891882fc0b8eca77f7d0b6702536ac92e659cb7e](https://github.com/0xfe/vexflow/commit/891882fc0b8eca77f7d0b6702536ac92e659cb7e) Remove comment due to resolved issue with "return" statement.

[a5408ac0613524fea3a42e9632793e89faca7fc6](https://github.com/0xfe/vexflow/commit/a5408ac0613524fea3a42e9632793e89faca7fc6) Merge https://github.com/0xfe/vexflow

[901e278a6a2e4861787a4cdc69f4c5b29a028d8b](https://github.com/0xfe/vexflow/commit/901e278a6a2e4861787a4cdc69f4c5b29a028d8b) Address issue: https://github.com/0xfe/vexflow/issues/998 Previous implementation with concat() did not do anything. Change to push() to be consistent with how we track parsed notes.

[0e1fba9374cfd52ecca457fedbd84ac73810b245](https://github.com/0xfe/vexflow/commit/0e1fba9374cfd52ecca457fedbd84ac73810b245) Address code review comments.

[7b6783315a93eb123ebb1e4dd2f0252968cccf01](https://github.com/0xfe/vexflow/commit/7b6783315a93eb123ebb1e4dd2f0252968cccf01) review comments

[e2853f29235a42ef9dce88a4463cd0e98cc6eada](https://github.com/0xfe/vexflow/commit/e2853f29235a42ef9dce88a4463cd0e98cc6eada) review comments

[3afbd6a78600d17b3c759d3e30867de67ace97d5](https://github.com/0xfe/vexflow/commit/3afbd6a78600d17b3c759d3e30867de67ace97d5) review comments

[77a2c15dc810d97bb7ea88c207ed0bcb475f9199](https://github.com/0xfe/vexflow/commit/77a2c15dc810d97bb7ea88c207ed0bcb475f9199) typedoc update

[0776ded967864a3702d86558949ae194213c0b50](https://github.com/0xfe/vexflow/commit/0776ded967864a3702d86558949ae194213c0b50) documentation update

[a40a51399a1a6c53c08c438a1eb2d0f375f883e6](https://github.com/0xfe/vexflow/commit/a40a51399a1a6c53c08c438a1eb2d0f375f883e6) more review updates

[33045636548431b94460ca42008110fb51731e16](https://github.com/0xfe/vexflow/commit/33045636548431b94460ca42008110fb51731e16) Merge pull request #992 from rvilarl/migration/stringnumbers

[4d57499a5c9fc22f33d552a5a61aabc84ca1e93c](https://github.com/0xfe/vexflow/commit/4d57499a5c9fc22f33d552a5a61aabc84ca1e93c) Merge pull request #988 from rvilarl/migration/staverepetition

[08bec1c6bb3a64b28478ecfe9da416651d9112fd](https://github.com/0xfe/vexflow/commit/08bec1c6bb3a64b28478ecfe9da416651d9112fd) Merge pull request #996 from rvilarl/migration/staveconnector

[30ff7998cd03764bb9b369d0db22be275f3e94ef](https://github.com/0xfe/vexflow/commit/30ff7998cd03764bb9b369d0db22be275f3e94ef) Fix #1000 https://github.com/0xfe/vexflow/issues/1000

[c3b01b10b9e39aa61b06a5d24557031b82d4a91a](https://github.com/0xfe/vexflow/commit/c3b01b10b9e39aa61b06a5d24557031b82d4a91a) Remove comment.

[9a17c44873de8c8bb4d95e39017fefb6e4edb2af](https://github.com/0xfe/vexflow/commit/9a17c44873de8c8bb4d95e39017fefb6e4edb2af) Migrate SVGContext.

[14d9d9dbaac8b4a2fcf9106396eabfd3407fefc7](https://github.com/0xfe/vexflow/commit/14d9d9dbaac8b4a2fcf9106396eabfd3407fefc7) Fix inconsistencies with the way we check against null vs. undefined. Handle optional parameters inline.

[be2fe7eb1de6026b31c8c1ffa457373911762562](https://github.com/0xfe/vexflow/commit/be2fe7eb1de6026b31c8c1ffa457373911762562) Migrating SVGContext.

[d907eafc94e67b080dc5589685dd50d1a0e0e720](https://github.com/0xfe/vexflow/commit/d907eafc94e67b080dc5589685dd50d1a0e0e720) Migrating SVGContext.

[18b29a83b4254f40d572cfe7dad84f315335b991](https://github.com/0xfe/vexflow/commit/18b29a83b4254f40d572cfe7dad84f315335b991) Rename SVGContext.

[80e2afa18c666f025a574b292027b42b1e10a16d](https://github.com/0xfe/vexflow/commit/80e2afa18c666f025a574b292027b42b1e10a16d) Code review from @rvilarl.

[d27b2f220f2ad538e28e2c45d9c4b549ba0f8869](https://github.com/0xfe/vexflow/commit/d27b2f220f2ad538e28e2c45d9c4b549ba0f8869) Remove comments that are redundant / incorrect / have typos.

[5c92baf6e37c28f7dee6ca51602679d17a57627b](https://github.com/0xfe/vexflow/commit/5c92baf6e37c28f7dee6ca51602679d17a57627b) Modifier sets this.note to undefined, so subclasses should not override and set this.note to null.

[cce79c84663cd15a77082152f33e4a48bb582c61](https://github.com/0xfe/vexflow/commit/cce79c84663cd15a77082152f33e4a48bb582c61) Introduce Modifier.checkAttachedNote() to improve consistency with the way we check whether this.note and this.index are valid.

[bb0544684192e20245f292bf815cf8af77501394](https://github.com/0xfe/vexflow/commit/bb0544684192e20245f292bf815cf8af77501394) Migrate NoteSubGroup

[c9d30c8540350b89d370856d18a32492db4de83a](https://github.com/0xfe/vexflow/commit/c9d30c8540350b89d370856d18a32492db4de83a) Rename NoteSubGroup.

[3576f9df464e33b2f93f975032abbb1248a0f28f](https://github.com/0xfe/vexflow/commit/3576f9df464e33b2f93f975032abbb1248a0f28f) Handle eslint warings. Reduce usage of any. Add return types.

[bef47f14bf41a1ecbb83ef8adde4cbdc58d1755d](https://github.com/0xfe/vexflow/commit/bef47f14bf41a1ecbb83ef8adde4cbdc58d1755d) updates for code review

[6edd84182ecd1324774a93f37dbe192933775cfe](https://github.com/0xfe/vexflow/commit/6edd84182ecd1324774a93f37dbe192933775cfe) Migrate EasyScore. Still have "any" and possible bugs to fix.

[aa1603154d9ea53903c1f782a080676ab0e9c458](https://github.com/0xfe/vexflow/commit/aa1603154d9ea53903c1f782a080676ab0e9c458) pedalmarking migrated

[3dcee631be6cabffbbb7c095699747f2d2ba25e0](https://github.com/0xfe/vexflow/commit/3dcee631be6cabffbbb7c095699747f2d2ba25e0) pedalmarking renamed

[b331a23ab1059db0d27830b42cae3ecafebcedea](https://github.com/0xfe/vexflow/commit/b331a23ab1059db0d27830b42cae3ecafebcedea) staveconnector migrated

[29f7ceeb4695ab762effa8fb7ea27c009eee433e](https://github.com/0xfe/vexflow/commit/29f7ceeb4695ab762effa8fb7ea27c009eee433e) staveconnector renamed

[0e8b78c90a50b07d1745bd62c26a98c55467e85c](https://github.com/0xfe/vexflow/commit/0e8b78c90a50b07d1745bd62c26a98c55467e85c) Remove empty format call

[a31a50af75fe26da7e85887a0de44c9ff20d9ffa](https://github.com/0xfe/vexflow/commit/a31a50af75fe26da7e85887a0de44c9ff20d9ffa) Allow ChordSymbol to be attached to GlyphNotes.

[c1c5dfa41013632cd3a291fe0aa452806ca0d88c](https://github.com/0xfe/vexflow/commit/c1c5dfa41013632cd3a291fe0aa452806ca0d88c) stringnumber migrated

[bff4763beca276f9ea74c08480dbd91a90b783f9](https://github.com/0xfe/vexflow/commit/bff4763beca276f9ea74c08480dbd91a90b783f9) stringnumbers renamed

[b98b70e4639835405f9af669f624be7d0eb139ad](https://github.com/0xfe/vexflow/commit/b98b70e4639835405f9af669f624be7d0eb139ad) strokes migrated

[0c2511b3f257ca936d007ebf283821fbfd629f31](https://github.com/0xfe/vexflow/commit/0c2511b3f257ca936d007ebf283821fbfd629f31) strokes renamed

[6144be5b18e79b5c30bc0ef7155c823a878d06cd](https://github.com/0xfe/vexflow/commit/6144be5b18e79b5c30bc0ef7155c823a878d06cd) Export Rule and other types from Parser.

[4c04fa9a4fd50a56affc23e92cc39d8d334aa5b3](https://github.com/0xfe/vexflow/commit/4c04fa9a4fd50a56affc23e92cc39d8d334aa5b3) Rename EasyScore JS => TS.

[a0df9abae63adaa5e17c4afae7055234ff40cfbc](https://github.com/0xfe/vexflow/commit/a0df9abae63adaa5e17c4afae7055234ff40cfbc) staveline migrated

[42de1b454caff36b9d698efe0129de2e810e6cb3](https://github.com/0xfe/vexflow/commit/42de1b454caff36b9d698efe0129de2e810e6cb3) staveline renamed

[183fd27239bbbbc0bf4d3ec7d9f22fdcff801996](https://github.com/0xfe/vexflow/commit/183fd27239bbbbc0bf4d3ec7d9f22fdcff801996) staverepetition migrated

[a0f8826100903aabcfd3f0c082ac43f5fce13abc](https://github.com/0xfe/vexflow/commit/a0f8826100903aabcfd3f0c082ac43f5fce13abc) staverepetition renamed

[f8e27ee667a8841a61d1f1e621fe1ae7b957a9c8](https://github.com/0xfe/vexflow/commit/f8e27ee667a8841a61d1f1e621fe1ae7b957a9c8) review comments

[7a2e2ad2882f1ceb5e505861002000694c39b25b](https://github.com/0xfe/vexflow/commit/7a2e2ad2882f1ceb5e505861002000694c39b25b) total* removed from Note

[2e54f8a1c6d94e22a996a6b93c972cbadfcea25c](https://github.com/0xfe/vexflow/commit/2e54f8a1c6d94e22a996a6b93c972cbadfcea25c) fix rebase

[276269e5c5c221d07e6d80a69f640475c7387089](https://github.com/0xfe/vexflow/commit/276269e5c5c221d07e6d80a69f640475c7387089) totalPx calculation fixed

[f5f08f0cdd4e0b672e25adfc154bbb27b349884d](https://github.com/0xfe/vexflow/commit/f5f08f0cdd4e0b672e25adfc154bbb27b349884d) delete unused elements

[159d4bcd9accf25d46083df87dad30eacd6a33d7](https://github.com/0xfe/vexflow/commit/159d4bcd9accf25d46083df87dad30eacd6a33d7) alignRest fixed

[5a9e9181878c7395c3176cfe260f159acd281a88](https://github.com/0xfe/vexflow/commit/5a9e9181878c7395c3176cfe260f159acd281a88) review comments

[d470faf5d872689f500752ed18aee7432b22e1b8](https://github.com/0xfe/vexflow/commit/d470faf5d872689f500752ed18aee7432b22e1b8) formatter migrated

[4cc183bd2870d84bb539017a4d4f0002a762a9dc](https://github.com/0xfe/vexflow/commit/4cc183bd2870d84bb539017a4d4f0002a762a9dc) formatter renamed

[28f8239bd5208bb15182fc6dc35023b8eb70396c](https://github.com/0xfe/vexflow/commit/28f8239bd5208bb15182fc6dc35023b8eb70396c) formatter refactored

[3e13b92cc7437d5c6ac2b23fa2d056bb1f0f1564](https://github.com/0xfe/vexflow/commit/3e13b92cc7437d5c6ac2b23fa2d056bb1f0f1564) Merge pull request #984 from rvilarl/migration/articulation

[cff3862181167b3d2901faae8ce593cb9e91e6bd](https://github.com/0xfe/vexflow/commit/cff3862181167b3d2901faae8ce593cb9e91e6bd) review comments

[90e01f14e0190834d98346008ed9a66488b09752](https://github.com/0xfe/vexflow/commit/90e01f14e0190834d98346008ed9a66488b09752) review comments

[382fefbc14ae1de55470b9830fdd1885ecc44f18](https://github.com/0xfe/vexflow/commit/382fefbc14ae1de55470b9830fdd1885ecc44f18) articulation migrated

[cf2471c6803233dd888726fd2edf5baf500a4bdc](https://github.com/0xfe/vexflow/commit/cf2471c6803233dd888726fd2edf5baf500a4bdc) articulation renamed

[d7cc73aae7b7948d2f7cf6cccfc56b8b277e3841](https://github.com/0xfe/vexflow/commit/d7cc73aae7b7948d2f7cf6cccfc56b8b277e3841) Merge pull request #982 from rvilarl/migration/annotation

[f862047d118763b303a38353412c708ebfd2f8cc](https://github.com/0xfe/vexflow/commit/f862047d118763b303a38353412c708ebfd2f8cc) review comments

[06def181a36a2addb5449290cf89c44692681325](https://github.com/0xfe/vexflow/commit/06def181a36a2addb5449290cf89c44692681325) style missing in FontInfo

[ea235f94a743ed57e785e84886dd8ace937cc3e7](https://github.com/0xfe/vexflow/commit/ea235f94a743ed57e785e84886dd8ace937cc3e7) annotation migrated

[cf3cfb493c9e1a9bcdcdefe44ebac306c8069b0e](https://github.com/0xfe/vexflow/commit/cf3cfb493c9e1a9bcdcdefe44ebac306c8069b0e) annotation renamed

[7f53e61ca41293197afca78ecd3480ca2ca4e83d](https://github.com/0xfe/vexflow/commit/7f53e61ca41293197afca78ecd3480ca2ca4e83d) Merge pull request #986 from rvilarl/migration/textbracket

[17ea779505454d6a17367288a87e710ccc83e472](https://github.com/0xfe/vexflow/commit/17ea779505454d6a17367288a87e710ccc83e472) warn on deprecated accessors

[04e249b1ef556026e830d3f2b45dfe1bc7900720](https://github.com/0xfe/vexflow/commit/04e249b1ef556026e830d3f2b45dfe1bc7900720) Merge pull request #985 from rvilarl/migration/textdynamics

[09944b7878eb632ce87aa0b7ecbfd9cda34c8af7](https://github.com/0xfe/vexflow/commit/09944b7878eb632ce87aa0b7ecbfd9cda34c8af7) review comments

[ebed3bc90880fc7d9fc3352d7344c60d61039e64](https://github.com/0xfe/vexflow/commit/ebed3bc90880fc7d9fc3352d7344c60d61039e64) textdynamics migrated

[bcfc1e70d49ae505ec81f6886864c6505a714f14](https://github.com/0xfe/vexflow/commit/bcfc1e70d49ae505ec81f6886864c6505a714f14) textdynamics renamed

[d466fbfd1ee617ad98f472c10197c281124a9104](https://github.com/0xfe/vexflow/commit/d466fbfd1ee617ad98f472c10197c281124a9104) review comments

[4dfbf834cd015883941c68962c715ffeceae2275](https://github.com/0xfe/vexflow/commit/4dfbf834cd015883941c68962c715ffeceae2275) textbracket migrated

[cf1bb2db3bbeda486595cc46f6fbd64d02ed16c8](https://github.com/0xfe/vexflow/commit/cf1bb2db3bbeda486595cc46f6fbd64d02ed16c8) textbracket renamed

[3d1daed6bef39f85f8a0539e99a8c1e41051a9e6](https://github.com/0xfe/vexflow/commit/3d1daed6bef39f85f8a0539e99a8c1e41051a9e6) Merge pull request #983 from rvilarl/migration/checkStave

[c5edc22f57a7334fff28ed0b62a68e0f64f1ba45](https://github.com/0xfe/vexflow/commit/c5edc22f57a7334fff28ed0b62a68e0f64f1ba45) Merge pull request #981 from rvilarl/migration/tuplet

[5aca7ec88c78bc1f696374d9827265c90849e0f0](https://github.com/0xfe/vexflow/commit/5aca7ec88c78bc1f696374d9827265c90849e0f0) review comments

[60111ba147270898213aff75e4ea6b1a7bd92243](https://github.com/0xfe/vexflow/commit/60111ba147270898213aff75e4ea6b1a7bd92243) review comments

[b7ca76cd0d19ed024dda38659e90066047205042](https://github.com/0xfe/vexflow/commit/b7ca76cd0d19ed024dda38659e90066047205042) NoStave error simplified

[7b71fd6085b0166b05cde92894e71c55efb20a00](https://github.com/0xfe/vexflow/commit/7b71fd6085b0166b05cde92894e71c55efb20a00) tuplet migrated

[4b2d277fa19d523dc11ccbd848e47f27e0956279](https://github.com/0xfe/vexflow/commit/4b2d277fa19d523dc11ccbd848e47f27e0956279) tuplet renamed

[adda50f0d90212d5b8238f772d62b14a40288a17](https://github.com/0xfe/vexflow/commit/adda50f0d90212d5b8238f772d62b14a40288a17) Merge pull request #978 from rvilarl/migration/no-non-null-assertion

[c10d729e0a2ab8872f4d55d9feda60ad9289cf2e](https://github.com/0xfe/vexflow/commit/c10d729e0a2ab8872f4d55d9feda60ad9289cf2e) review comments

[7cfcd83349767b09a9574de12d2660482852e1fe](https://github.com/0xfe/vexflow/commit/7cfcd83349767b09a9574de12d2660482852e1fe) review comments

[d3f33678bd57b2f1d6713fff7abd584760518916](https://github.com/0xfe/vexflow/commit/d3f33678bd57b2f1d6713fff7abd584760518916) no-non-null-assertion warning enabled

[e4c83f18f99e3cee635cc6f43da76116689352ac](https://github.com/0xfe/vexflow/commit/e4c83f18f99e3cee635cc6f43da76116689352ac) Merge pull request #971 from AaronDavidNewman/master

[08ce4a7aff1b9f25b8716a732659229f1525398d](https://github.com/0xfe/vexflow/commit/08ce4a7aff1b9f25b8716a732659229f1525398d) Reduce to smallest width w/o overflow, fix text

[c5aa615a066a84d23497db15b9c363d69899c8d8](https://github.com/0xfe/vexflow/commit/c5aa615a066a84d23497db15b9c363d69899c8d8) Merge pull request #973 from rvilarl/migration/crescendo

[9c15a4fe6399a0ef7dd31ea0242c80998baba285](https://github.com/0xfe/vexflow/commit/9c15a4fe6399a0ef7dd31ea0242c80998baba285) Merge pull request #976 from rvilarl/migration/notehead

[9c16138e0669376279ab013ccacad1ee6673c43d](https://github.com/0xfe/vexflow/commit/9c16138e0669376279ab013ccacad1ee6673c43d) Merge pull request #972 from rvilarl/migration/dot

[7468ddce749e319ce179d67f39bc2b03ec37d5a4](https://github.com/0xfe/vexflow/commit/7468ddce749e319ce179d67f39bc2b03ec37d5a4) Merge pull request #977 from rvilarl/migration/typedoc

[9f1828d3b21e89cb94e5e7904f32d68ed595cc8b](https://github.com/0xfe/vexflow/commit/9f1828d3b21e89cb94e5e7904f32d68ed595cc8b) textnote missing in typedoc

[292ec47f6ac36726d27ae79cf3c437f96e851f3a](https://github.com/0xfe/vexflow/commit/292ec47f6ac36726d27ae79cf3c437f96e851f3a) documentation update & docco removed

[65da4f5b113c830754e71f33e1318701c3827732](https://github.com/0xfe/vexflow/commit/65da4f5b113c830754e71f33e1318701c3827732) Merge latest TS change

[140cdf5b2d7654acc577445524474097e0723db4](https://github.com/0xfe/vexflow/commit/140cdf5b2d7654acc577445524474097e0723db4) Merge https://github.com/0xfe/vexflow

[203e0b256e1d2f131f5408e1992bf1debd0c8d9f](https://github.com/0xfe/vexflow/commit/203e0b256e1d2f131f5408e1992bf1debd0c8d9f) Widen the staves that are currently overflowing

[b0c2124c8d77333e47663d06373a55509674ed8e](https://github.com/0xfe/vexflow/commit/b0c2124c8d77333e47663d06373a55509674ed8e) eslint comments removed

[769d7b1efe07acb8d490fd9b57be90af48ecfd47](https://github.com/0xfe/vexflow/commit/769d7b1efe07acb8d490fd9b57be90af48ecfd47) review comment

[f9ecbd9f46f561b44089e243af5becace6cacb65](https://github.com/0xfe/vexflow/commit/f9ecbd9f46f561b44089e243af5becace6cacb65) Merge pull request #975 from rvilarl/migration/gracenote

[0b6d27696517a3dc72ef8fdbc9de8df6fdf3a9dc](https://github.com/0xfe/vexflow/commit/0b6d27696517a3dc72ef8fdbc9de8df6fdf3a9dc) Merge pull request #967 from rvilarl/migration/tabnote

[8362d352fa67a4bb6c40d2c63b63c9fcedf689e3](https://github.com/0xfe/vexflow/commit/8362d352fa67a4bb6c40d2c63b63c9fcedf689e3) Merge pull request #960 from rvilarl/migration/timesignote

[14827d2b77904292ed889576dc4fc811a339a3ed](https://github.com/0xfe/vexflow/commit/14827d2b77904292ed889576dc4fc811a339a3ed) review comments

[20c7ee90b129574a0fe6403d8253e2862c274291](https://github.com/0xfe/vexflow/commit/20c7ee90b129574a0fe6403d8253e2862c274291) notehead migrated

[020942f4502ceeb64771619dcad98aa9e975bc8f](https://github.com/0xfe/vexflow/commit/020942f4502ceeb64771619dcad98aa9e975bc8f) notehead renamed

[f287487d76632a81c52b7a745a698651e9bba4a9](https://github.com/0xfe/vexflow/commit/f287487d76632a81c52b7a745a698651e9bba4a9) review comments

[78d618e39903c8207045c52b8f3c26e03fcfed48](https://github.com/0xfe/vexflow/commit/78d618e39903c8207045c52b8f3c26e03fcfed48) review comments

[423d99a4b54e0c443d19922786c96de76cbe2c7a](https://github.com/0xfe/vexflow/commit/423d99a4b54e0c443d19922786c96de76cbe2c7a) crescendo migrated

[f50072979fbd67bc49610b9fd5e3df6949167ead](https://github.com/0xfe/vexflow/commit/f50072979fbd67bc49610b9fd5e3df6949167ead) crescendo renamed

[1eb536659f9a74780596f9597da5d1b6e8a1d19e](https://github.com/0xfe/vexflow/commit/1eb536659f9a74780596f9597da5d1b6e8a1d19e) review comments

[103d451210b5fe8fceb668401692022e7d6d918e](https://github.com/0xfe/vexflow/commit/103d451210b5fe8fceb668401692022e7d6d918e) review comments

[60488cd56cde5d8826c7e98abae142cf358f0f3b](https://github.com/0xfe/vexflow/commit/60488cd56cde5d8826c7e98abae142cf358f0f3b) dot migrated

[585199dec6c35f5263e4644a77c2cf6301a92978](https://github.com/0xfe/vexflow/commit/585199dec6c35f5263e4644a77c2cf6301a92978) dot renamed

[904417d0d7787781ccc0f34a28da681539683647](https://github.com/0xfe/vexflow/commit/904417d0d7787781ccc0f34a28da681539683647) review comment

[c066faa93355353ee68463228e86176f4531c289](https://github.com/0xfe/vexflow/commit/c066faa93355353ee68463228e86176f4531c289) review comments

[fc575897b1ade84dddddc26cd532962e32994462](https://github.com/0xfe/vexflow/commit/fc575897b1ade84dddddc26cd532962e32994462) review comments

[c2e013bd048e7bf66cdbc580a47da9eed0e401df](https://github.com/0xfe/vexflow/commit/c2e013bd048e7bf66cdbc580a47da9eed0e401df) tabnote migrated

[52af5dbb7c7604b9d94623464a76802e925ea597](https://github.com/0xfe/vexflow/commit/52af5dbb7c7604b9d94623464a76802e925ea597) tabnote renamed

[9fe0bf29d9f4ee1e9c84f33f30f82b3bedc58c5d](https://github.com/0xfe/vexflow/commit/9fe0bf29d9f4ee1e9c84f33f30f82b3bedc58c5d) review comments

[d8bc645788c4f9cf2898d598de1370c64cd973c4](https://github.com/0xfe/vexflow/commit/d8bc645788c4f9cf2898d598de1370c64cd973c4) review comments

[577843cfb4099a43f56428f48874c7a84f3e331a](https://github.com/0xfe/vexflow/commit/577843cfb4099a43f56428f48874c7a84f3e331a) placeGlyphOnLine 3

[f759695aade2748ffee3e4ffb9d5d113c253575b](https://github.com/0xfe/vexflow/commit/f759695aade2748ffee3e4ffb9d5d113c253575b) review comments

[08d78e003e0fea7ae64f7b5da885e02279aa5f5e](https://github.com/0xfe/vexflow/commit/08d78e003e0fea7ae64f7b5da885e02279aa5f5e) timesignote timesignature migrated

[60664cc4040fc45398bd55346344ec6be7421219](https://github.com/0xfe/vexflow/commit/60664cc4040fc45398bd55346344ec6be7421219) timesignature renamed

[8f566a0abfd2527035f81299f522f6b9e32442fb](https://github.com/0xfe/vexflow/commit/8f566a0abfd2527035f81299f522f6b9e32442fb) timesignote renamed

[6dd7dd92137e144094640ebf9e0e34e66e5f5fbe](https://github.com/0xfe/vexflow/commit/6dd7dd92137e144094640ebf9e0e34e66e5f5fbe) Merge pull request #958 from rvilarl/migration/barnote

[a6087f88a31a6616b71dc090692cccfcae67944c](https://github.com/0xfe/vexflow/commit/a6087f88a31a6616b71dc090692cccfcae67944c) review comments

[490c91ff90012c58823ad37379fac94272f626b8](https://github.com/0xfe/vexflow/commit/490c91ff90012c58823ad37379fac94272f626b8) gracenote migrated

[c45cb37e8aedc56b4d362faed11d093cd6937b8e](https://github.com/0xfe/vexflow/commit/c45cb37e8aedc56b4d362faed11d093cd6937b8e) gracenote renamed

[d17c5a7d50d4de7eae2864c4044804bf2ceba549](https://github.com/0xfe/vexflow/commit/d17c5a7d50d4de7eae2864c4044804bf2ceba549) Merge pull request #954 from rvilarl/migration/stavetie

[c2263e9fec37954719dbbf912f74b3776e74e33d](https://github.com/0xfe/vexflow/commit/c2263e9fec37954719dbbf912f74b3776e74e33d) review comment reverted

[ea814a97ddc2ae2710c7ec0580ba9263a75545ab](https://github.com/0xfe/vexflow/commit/ea814a97ddc2ae2710c7ec0580ba9263a75545ab) Merge pull request #970 from rvilarl/migration/typedoc

[7ac480003f5d8525ace6a4ac7fb818a5ae34aefe](https://github.com/0xfe/vexflow/commit/7ac480003f5d8525ace6a4ac7fb818a5ae34aefe) Merge pull request #968 from ronyeh/webpack-test

[6c18e8504662484c6ecd77d85100e091d489a4ad](https://github.com/0xfe/vexflow/commit/6c18e8504662484c6ecd77d85100e091d489a4ad) Issue 969

[2f04d33eccc65a5894d822dfc08d103577b76621](https://github.com/0xfe/vexflow/commit/2f04d33eccc65a5894d822dfc08d103577b76621) documentation update

[83cf4a59161468731ddc3fc2d2d550d60803e6a7](https://github.com/0xfe/vexflow/commit/83cf4a59161468731ddc3fc2d2d550d60803e6a7) Remove '2' from 'Vexflow 2'.

[825fe98c5e65fa7a3a0eb86724b4158863bcadce](https://github.com/0xfe/vexflow/commit/825fe98c5e65fa7a3a0eb86724b4158863bcadce) Use webpack to bundle tests, instead of concatenating the JS files together.

[94ec622161c237cebf1c889706ddaa8696df92a9](https://github.com/0xfe/vexflow/commit/94ec622161c237cebf1c889706ddaa8696df92a9) Merge pull request #962 from rvilarl/migration/textnote

[8efec9e2b0f5e113d7d02175193c3ca0d61d2f4a](https://github.com/0xfe/vexflow/commit/8efec9e2b0f5e113d7d02175193c3ca0d61d2f4a) PR #609 test added

[b30d1a447d1da2812ac1843c67f3184beed9a532](https://github.com/0xfe/vexflow/commit/b30d1a447d1da2812ac1843c67f3184beed9a532) PR #609 include to allow styling

[c273bfb7f6bf7ee293d7d85d2fb58c3ab1948c59](https://github.com/0xfe/vexflow/commit/c273bfb7f6bf7ee293d7d85d2fb58c3ab1948c59) review changes

[dc3d9c8f351566d5482f4ca3722c4f78a122dda3](https://github.com/0xfe/vexflow/commit/dc3d9c8f351566d5482f4ca3722c4f78a122dda3) barnote stavebarline migrated

[4c94472f617030c5e66b5d70758f32686886ff8f](https://github.com/0xfe/vexflow/commit/4c94472f617030c5e66b5d70758f32686886ff8f) stavebarline renamed

[6671b2438e91755ea31a0a9cf150715870e0384b](https://github.com/0xfe/vexflow/commit/6671b2438e91755ea31a0a9cf150715870e0384b) barnote migration1

[97dc615d5880e80d45e582244a9023933f5b9f95](https://github.com/0xfe/vexflow/commit/97dc615d5880e80d45e582244a9023933f5b9f95) barnote renamed

[9c1e0cd704344314cdd6fe8a6bf680d6cd608eb0](https://github.com/0xfe/vexflow/commit/9c1e0cd704344314cdd6fe8a6bf680d6cd608eb0) review comment

[0515090235435d382d93d7d608a760f35cd582c7](https://github.com/0xfe/vexflow/commit/0515090235435d382d93d7d608a760f35cd582c7) review comments

[abcd8aa5092fbd586409bf83097818a8d59f0128](https://github.com/0xfe/vexflow/commit/abcd8aa5092fbd586409bf83097818a8d59f0128) review comments

[73e942112820f4806a7672c1393eb169d9291c00](https://github.com/0xfe/vexflow/commit/73e942112820f4806a7672c1393eb169d9291c00) stavetie tabtie tabslide migrated

[5bd44dd1d8433bdeb4713255a740d0cc9aaf9f67](https://github.com/0xfe/vexflow/commit/5bd44dd1d8433bdeb4713255a740d0cc9aaf9f67) tabslide renamed

[d42ebeac16b6cf17fd55d31f26f27850f5d8670f](https://github.com/0xfe/vexflow/commit/d42ebeac16b6cf17fd55d31f26f27850f5d8670f) tabtie renamed

[5636ac921f5b7ff87c4cfc191959132b6f18df2d](https://github.com/0xfe/vexflow/commit/5636ac921f5b7ff87c4cfc191959132b6f18df2d) stavetie renamed

[423ed7f6445d120eb6af76af4288be2ac3a69abc](https://github.com/0xfe/vexflow/commit/423ed7f6445d120eb6af76af4288be2ac3a69abc) Merge pull request #955 from rvilarl/migration/modifierContext

[ed45e4d4f29a4ce0086b9bae535f0e16e8f7696d](https://github.com/0xfe/vexflow/commit/ed45e4d4f29a4ce0086b9bae535f0e16e8f7696d) Merge pull request #965 from ronyeh/master

[6636c941306fafb8b69f2a39a52e42c6a9d1081c](https://github.com/0xfe/vexflow/commit/6636c941306fafb8b69f2a39a52e42c6a9d1081c) Merge pull request #945 from ronyeh/migration/parser2

[776d1e19b64781ad27fd9280baa4f6b64c374e5c](https://github.com/0xfe/vexflow/commit/776d1e19b64781ad27fd9280baa4f6b64c374e5c) review comments

[238150173d3d961b34220592de3fff39568832a4](https://github.com/0xfe/vexflow/commit/238150173d3d961b34220592de3fff39568832a4) review comment

[7d1e224f82941aa887137c1d79f88249273d9306](https://github.com/0xfe/vexflow/commit/7d1e224f82941aa887137c1d79f88249273d9306) Registry: methods that return this should use the 'this' return type.

[34210d1ccee67387fa40d504f1fba3576e3a2e33](https://github.com/0xfe/vexflow/commit/34210d1ccee67387fa40d504f1fba3576e3a2e33) Support mixed results array with GroupedResults type.

[f65f35183055c9143305830fc37924638b96d7ab](https://github.com/0xfe/vexflow/commit/f65f35183055c9143305830fc37924638b96d7ab) Add test case for Parser.

[ebe248e39cb2f95e542eba9d5e6d372eefa0a295](https://github.com/0xfe/vexflow/commit/ebe248e39cb2f95e542eba9d5e6d372eefa0a295) Move Parser types back into parser.ts. Inline the TriggerFunction's state parameter typing.

[1e548aae5ebecc42ad6ce2bcbad99e9bca1a5f5a](https://github.com/0xfe/vexflow/commit/1e548aae5ebecc42ad6ce2bcbad99e9bca1a5f5a) Migrate Parser to TypeScript. All tests pass. No visual diffs from reference build.

[ed23c3d95cf72594b389ffcfc299052880dfa1b3](https://github.com/0xfe/vexflow/commit/ed23c3d95cf72594b389ffcfc299052880dfa1b3) Initialize instance variables in the constructor().

[69a8a6f19a7e26ce055ee337d9ae7cd8acd48b72](https://github.com/0xfe/vexflow/commit/69a8a6f19a7e26ce055ee337d9ae7cd8acd48b72) Add Result interface which can contain data from lexing or parsing. Add typing to flattenMatches(...).

[c90f86e409178f43c3d0ac073149c16f0d3c2a4e](https://github.com/0xfe/vexflow/commit/c90f86e409178f43c3d0ac073149c16f0d3c2a4e) Add types that will be moved back to easyscore.ts and parser.ts.

[bb53ddc3a6a07c13442368fe1a2f52126d7faf77](https://github.com/0xfe/vexflow/commit/bb53ddc3a6a07c13442368fe1a2f52126d7faf77) Export the Grammar class from easyscore.js and import it into parser.ts.

[9c6a26364b80d1037f75b7b282dd176097a44f3c](https://github.com/0xfe/vexflow/commit/9c6a26364b80d1037f75b7b282dd176097a44f3c) Rename parser.js -> parser.ts.

[6748a752f70346487095061545ffb473e2dac317](https://github.com/0xfe/vexflow/commit/6748a752f70346487095061545ffb473e2dac317) Merge pull request #959 from ronyeh/migration/registry

[88e6bbf8b22debece54b175f77dab316052e8cc7](https://github.com/0xfe/vexflow/commit/88e6bbf8b22debece54b175f77dab316052e8cc7) Merge pull request #964 from ronyeh/grunt-watch-2

[c6e38bc0b9b74619132b0264fd3e494f9333ff50](https://github.com/0xfe/vexflow/commit/c6e38bc0b9b74619132b0264fd3e494f9333ff50) Fix typo

[50739aa3884c0f53227e9015d28e44c607f95f2e](https://github.com/0xfe/vexflow/commit/50739aa3884c0f53227e9015d28e44c607f95f2e) Merge pull request #957 from rvilarl/migration/stavetext

[c2f7f117564295fed5e3be4d83bc500a6292ec0f](https://github.com/0xfe/vexflow/commit/c2f7f117564295fed5e3be4d83bc500a6292ec0f) Use optional chaining to make the code more concise. Preserve API from version 3.0.9:   onUpdate(obj) and updateIndex(obj) both take a single object parameter.

[ecf0a2020f534d744e7397edab92e5fe5291e258](https://github.com/0xfe/vexflow/commit/ecf0a2020f534d744e7397edab92e5fe5291e258) Update 'grunt watch' to watch src/ and tests/ concurrently. It will trigger the correct webpack task when it notices a changed file.

[3555c63d3e33b8aa3e9a8230c44b452e9e15adad](https://github.com/0xfe/vexflow/commit/3555c63d3e33b8aa3e9a8230c44b452e9e15adad) textnote migrated

[2e19d4621413f0a82d3aed23a3e349efbd17c6a9](https://github.com/0xfe/vexflow/commit/2e19d4621413f0a82d3aed23a3e349efbd17c6a9) textnote renamed

[ae1ba4964231493546386b4bae7877caf803aade](https://github.com/0xfe/vexflow/commit/ae1ba4964231493546386b4bae7877caf803aade) ModifierContextMember refactored

[65074262b1dc216404d37631c0c0053555bdf75d](https://github.com/0xfe/vexflow/commit/65074262b1dc216404d37631c0c0053555bdf75d) review comments

[0fad62603ac1e67aef1db4059c186fae3214ae2d](https://github.com/0xfe/vexflow/commit/0fad62603ac1e67aef1db4059c186fae3214ae2d) review comments

[efe0ee45936e113054c5580f56e8aecfb5ad5be2](https://github.com/0xfe/vexflow/commit/efe0ee45936e113054c5580f56e8aecfb5ad5be2) modifiercontext migrated

[7e1cbc4923df466f810985a9b2598859744ef18e](https://github.com/0xfe/vexflow/commit/7e1cbc4923df466f810985a9b2598859744ef18e) modifiercontext renamed

[55305bc8f99a245812211f57e0078f55b99759c6](https://github.com/0xfe/vexflow/commit/55305bc8f99a245812211f57e0078f55b99759c6) Migrate Registry

[ce06497467e8f9fec76b2272a29d88fd92a256e0](https://github.com/0xfe/vexflow/commit/ce06497467e8f9fec76b2272a29d88fd92a256e0) Rename registry.js -> registry.ts.

[ba717d830c8a37d25f4e690f9b2983adc852d400](https://github.com/0xfe/vexflow/commit/ba717d830c8a37d25f4e690f9b2983adc852d400) Merge pull request #956 from rvilarl/migration/stavetempo

[1c7d1155517bc659e466d9b313c6eabb1c81f292](https://github.com/0xfe/vexflow/commit/1c7d1155517bc659e466d9b313c6eabb1c81f292) Merge pull request #950 from rvilarl/migration/clefnote

[afc5634fdf88b4196db3414ea0395a7aecd42d17](https://github.com/0xfe/vexflow/commit/afc5634fdf88b4196db3414ea0395a7aecd42d17) Merge pull request #951 from rvilarl/migration/vibratobracket

[1524e41d5417e7980d08503fb5786cdcaa132ce0](https://github.com/0xfe/vexflow/commit/1524e41d5417e7980d08503fb5786cdcaa132ce0) review comments

[fc409e8592a198861eadf4ba567d825eb17fb918](https://github.com/0xfe/vexflow/commit/fc409e8592a198861eadf4ba567d825eb17fb918) review comments

[466cd12e9f61b2a3f6755f96970aa559c2e1d585](https://github.com/0xfe/vexflow/commit/466cd12e9f61b2a3f6755f96970aa559c2e1d585) Merge pull request #953 from rvilarl/migration/stavevolta

[d306bedadb3a234e95fcb53d2c32c5830df83d6a](https://github.com/0xfe/vexflow/commit/d306bedadb3a234e95fcb53d2c32c5830df83d6a) review comment

[48583de20299c8e51550f860a37828269ddc4acd](https://github.com/0xfe/vexflow/commit/48583de20299c8e51550f860a37828269ddc4acd) review comments

[8e9c5e304a62ca4c385c54e37a26e6236249d9d5](https://github.com/0xfe/vexflow/commit/8e9c5e304a62ca4c385c54e37a26e6236249d9d5) clef migrated

[cb6f687826f1fd5eafe85cfa892bc441c9039651](https://github.com/0xfe/vexflow/commit/cb6f687826f1fd5eafe85cfa892bc441c9039651) clefnote migrated

[e2be3874c4c5f77364d2e54dd49930a5500214a3](https://github.com/0xfe/vexflow/commit/e2be3874c4c5f77364d2e54dd49930a5500214a3) clefnote renamed

[fc68c24745c2f120b54bd78050bfc01fd805d29d](https://github.com/0xfe/vexflow/commit/fc68c24745c2f120b54bd78050bfc01fd805d29d) review comment

[7f42c1d66d432eb442a75dc7ea4f20c97be4e1fc](https://github.com/0xfe/vexflow/commit/7f42c1d66d432eb442a75dc7ea4f20c97be4e1fc) review comments

[97a0026bd2ec0998fe2ff595d004b6b479b8cfa9](https://github.com/0xfe/vexflow/commit/97a0026bd2ec0998fe2ff595d004b6b479b8cfa9) vibratobracket migrated

[c368d694cef25d218562bed0a5b0f5d2e8843ef9](https://github.com/0xfe/vexflow/commit/c368d694cef25d218562bed0a5b0f5d2e8843ef9) vibratobracket renamed

[1964ccf14f81608f3ee01c80820778ba65177677](https://github.com/0xfe/vexflow/commit/1964ccf14f81608f3ee01c80820778ba65177677) review comments

[c8322dcd09d365e89e9295585c41057563302509](https://github.com/0xfe/vexflow/commit/c8322dcd09d365e89e9295585c41057563302509) stavetext migrated

[1d6446ff1d7b4caf6d69d16b75bd62e2bfa117c5](https://github.com/0xfe/vexflow/commit/1d6446ff1d7b4caf6d69d16b75bd62e2bfa117c5) stavetext renamed

[718a7411814cafdf0549b08cda819c5c50d8704a](https://github.com/0xfe/vexflow/commit/718a7411814cafdf0549b08cda819c5c50d8704a) stavetempo migrated

[d14f7cb29b26903fbc07b4786cabb13f9bf9e467](https://github.com/0xfe/vexflow/commit/d14f7cb29b26903fbc07b4786cabb13f9bf9e467) stavetempo renamed

[ff38b633e7f158269dddd3efa964b94e27f42865](https://github.com/0xfe/vexflow/commit/ff38b633e7f158269dddd3efa964b94e27f42865) stavevolta migrated

[2d2e0dc5ea19b5e5986821774832124a7b21fa26](https://github.com/0xfe/vexflow/commit/2d2e0dc5ea19b5e5986821774832124a7b21fa26) stavevolta renamed

[b39607051c41359dd0e7e4e9fcfa1f32790a106c](https://github.com/0xfe/vexflow/commit/b39607051c41359dd0e7e4e9fcfa1f32790a106c) Merge pull request #952 from rvilarl/migration/stavesection

[992beba2454993229e06743c97248912013f304b](https://github.com/0xfe/vexflow/commit/992beba2454993229e06743c97248912013f304b) Merge pull request #940 from ronyeh/master

[737fd8166cf4e2bd8e95a4a7e99945fb8267da90](https://github.com/0xfe/vexflow/commit/737fd8166cf4e2bd8e95a4a7e99945fb8267da90) Merge pull request #949 from ronyeh/vscode-search-exclude

[15c628d1841da1800f402ac0d5850309f7896176](https://github.com/0xfe/vexflow/commit/15c628d1841da1800f402ac0d5850309f7896176) stavesection migrated

[cad9ce5c69e22bbad5fb18bd14797ce997b9463b](https://github.com/0xfe/vexflow/commit/cad9ce5c69e22bbad5fb18bd14797ce997b9463b) stavesection renamed

[6b7bcd1e81197acca6def42a51250d5dc2da8746](https://github.com/0xfe/vexflow/commit/6b7bcd1e81197acca6def42a51250d5dc2da8746) Incorporate changes from code review.

[d547f7d5110929b5d572833e9ea2b31141b0b58b](https://github.com/0xfe/vexflow/commit/d547f7d5110929b5d572833e9ea2b31141b0b58b) Add releases/ to vscode's search.exclude.

[1a2d51e2df3e63048dda6320d2403eff5ec1d596](https://github.com/0xfe/vexflow/commit/1a2d51e2df3e63048dda6320d2403eff5ec1d596) Merge pull request #942 from rvilarl/migration/stavemodifier

[7e763f603daea2598cdc188c75c49a2adb8afb22](https://github.com/0xfe/vexflow/commit/7e763f603daea2598cdc188c75c49a2adb8afb22) review comments

[856d56299837ded1c698bc650bcb1f5be8370fd5](https://github.com/0xfe/vexflow/commit/856d56299837ded1c698bc650bcb1f5be8370fd5) review comments

[74a0101f5ce6a1f08c894db11dcba1dd0a35c952](https://github.com/0xfe/vexflow/commit/74a0101f5ce6a1f08c894db11dcba1dd0a35c952) stavemodifier migrated

[0696a7f8ab93dd34c33239d375bc8e1b89870bf9](https://github.com/0xfe/vexflow/commit/0696a7f8ab93dd34c33239d375bc8e1b89870bf9) stavemodifier renamed

[f9ac14ae7203fc4495d5a93d8f9428d70352118c](https://github.com/0xfe/vexflow/commit/f9ac14ae7203fc4495d5a93d8f9428d70352118c) Merge pull request #948 from rvilarl/migration/frethandfinger

[d9e958ce50c265788a408f04ad400250b2c24a1f](https://github.com/0xfe/vexflow/commit/d9e958ce50c265788a408f04ad400250b2c24a1f) Merge pull request #947 from rvilarl/migration/ghostnote

[73b0f6fa9f294f3adffff06716c173409f37425f](https://github.com/0xfe/vexflow/commit/73b0f6fa9f294f3adffff06716c173409f37425f) Merge pull request #933 from rvilarl/migration/boundingbox

[3817e3bbde2a5c1022b8d5f9d273ee1fc6488ce3](https://github.com/0xfe/vexflow/commit/3817e3bbde2a5c1022b8d5f9d273ee1fc6488ce3) frethandfinger migrated

[b081563229540b0ff2fbc8759b79ee2630033322](https://github.com/0xfe/vexflow/commit/b081563229540b0ff2fbc8759b79ee2630033322) Merge upstream changes before updating this pull request. Merge remote-tracking branch 'upstream/master'

[abf1f82077d300b685cd12e0cc6c68ee816e019a](https://github.com/0xfe/vexflow/commit/abf1f82077d300b685cd12e0cc6c68ee816e019a) Move constant out to font metrics files. This adjustment tells the stem to render shorter when there is a flag to be drawn. See: musicFont.lookupMetric('stem.renderHeightAdjustmentForFlag')

[aca7f43b046ae1cb1ef01bdb504d5a35b76f8de0](https://github.com/0xfe/vexflow/commit/aca7f43b046ae1cb1ef01bdb504d5a35b76f8de0) frethandfinger renamed

[f78f8f89c3e126beed8400d562b6fcde98af5764](https://github.com/0xfe/vexflow/commit/f78f8f89c3e126beed8400d562b6fcde98af5764) ghostnote migrated

[555a602209f26bf5b7cc9b907dc15d9fd1daaa26](https://github.com/0xfe/vexflow/commit/555a602209f26bf5b7cc9b907dc15d9fd1daaa26) ghostnote renamed

[f1fbec5aec166aa141b6c950388bd1ac69290074](https://github.com/0xfe/vexflow/commit/f1fbec5aec166aa141b6c950388bd1ac69290074) Merge pull request #938 from rvilarl/migration/voice

[ba337ac12d6e23282ded2c3f3d9d207b69e2ec18](https://github.com/0xfe/vexflow/commit/ba337ac12d6e23282ded2c3f3d9d207b69e2ec18) review comments

[78c89428ed7e6d2fb7361ac9f2390b34c7827ed0](https://github.com/0xfe/vexflow/commit/78c89428ed7e6d2fb7361ac9f2390b34c7827ed0) Merge pull request #939 from rvilarl/migration/bend

[b43376d172026da77a37a9578f1ff787562c85e9](https://github.com/0xfe/vexflow/commit/b43376d172026da77a37a9578f1ff787562c85e9) Merge pull request #943 from rvilarl/migration/typedoc2

[e5060f0285803b38ad1adf4534d85d2cc9a2cd85](https://github.com/0xfe/vexflow/commit/e5060f0285803b38ad1adf4534d85d2cc9a2cd85) typedoc update

[3f7cf5d7e2b2554e13c0d6039de30114a927f3b1](https://github.com/0xfe/vexflow/commit/3f7cf5d7e2b2554e13c0d6039de30114a927f3b1) note reverted to master

[3a3cea9e1570a22ca41bf2720ec05e1f64d9e304](https://github.com/0xfe/vexflow/commit/3a3cea9e1570a22ca41bf2720ec05e1f64d9e304) review comments

[ee207c3629ce2098c29c957e6a09fd5a5b6ce179](https://github.com/0xfe/vexflow/commit/ee207c3629ce2098c29c957e6a09fd5a5b6ce179) Fix flag shiftX issues that existed in version 3.0.9 for Gonville. Now, stems no longer extend past the end of the flag, and transition smoothly into the flag glyph. Verified at up to 32x context scale.

[e52f914621bca86d02e2899feb8c28c271f96d88](https://github.com/0xfe/vexflow/commit/e52f914621bca86d02e2899feb8c28c271f96d88) Fix flag shiftX issues that existed in version 3.0.9 for Petaluma. These issues were present in 16th, 64th, 128th notes. Now, the stem no longer protrudes past the end of the flag. The stem transitions more smoothly into the flag glyph. Verified at up to 32x context scale.

[fa8e2998fa2207656797c288306b522dbc3adcdc](https://github.com/0xfe/vexflow/commit/fa8e2998fa2207656797c288306b522dbc3adcdc) Tweak Bravura stem metrics. There is no way to get this perfect on the half notes, unless we change Flow.STEM_WIDTH to 1.2 (a thinner stem) so that it more faithfully reproduces the Bravura half note.

[0264303255bc40a9551d80a2eb21b8913b952c14](https://github.com/0xfe/vexflow/commit/0264303255bc40a9551d80a2eb21b8913b952c14) Adjust Petaluma metrics slightly to make it extra smooth.

[2419efdae1fa1a284aefaea942a6b3de3532d25e](https://github.com/0xfe/vexflow/commit/2419efdae1fa1a284aefaea942a6b3de3532d25e) Adjust stem metrics slightly to make it extra smooth.

[4bbf1868d4996035071552aba4dbf2595e2615f3](https://github.com/0xfe/vexflow/commit/4bbf1868d4996035071552aba4dbf2595e2615f3) Adjust Petaluma font metrics so that the note heads <=> stem transitions are visually smooth.

[120ebe0b01e832c395c475b777ad37851dd1e89f](https://github.com/0xfe/vexflow/commit/120ebe0b01e832c395c475b777ad37851dd1e89f) Improve the shiftX of the flags.

[f5a098fd4b5a4f6020fe4922e079963c9be9b0db](https://github.com/0xfe/vexflow/commit/f5a098fd4b5a4f6020fe4922e079963c9be9b0db) Set stem.renderHeightAdjustment = -3 to shorten the stem for notes with flags. This prevents the stem from poking out past the end of the flag.

[e2e0c8f51df9186258e72563a6380148528cacf0](https://github.com/0xfe/vexflow/commit/e2e0c8f51df9186258e72563a6380148528cacf0) Improve comments to answer the question posed by the FIXME.

[987e040f93c6ceaa2dacb7ea24b6c328a6e142b3](https://github.com/0xfe/vexflow/commit/987e040f93c6ceaa2dacb7ea24b6c328a6e142b3) Fix issues where note stem ends are visible beyond the note head and flags. This patch affects the Gonville font. Shift the flag a bit to align it with the stem.

[eec0cb5bb58807ff4f3143ffe4d0c81674834fa7](https://github.com/0xfe/vexflow/commit/eec0cb5bb58807ff4f3143ffe4d0c81674834fa7) Merge pull request #932 from ronyeh/vexflow_test_helpers

[3a5b5ffd20735fd5f7c1844ad622b39f8d0aa18b](https://github.com/0xfe/vexflow/commit/3a5b5ffd20735fd5f7c1844ad622b39f8d0aa18b) Merge pull request #934 from rvilarl/migration/curve

[befc5a2833a5f7b411f999859263fd40f5cbb184](https://github.com/0xfe/vexflow/commit/befc5a2833a5f7b411f999859263fd40f5cbb184) bend migrated

[bdde4f9c015178c6454ad808140ae9590e356438](https://github.com/0xfe/vexflow/commit/bdde4f9c015178c6454ad808140ae9590e356438) bend renamed

[5bbe70de5e5f35ce8a77bffbd69ae74b91d4fb47](https://github.com/0xfe/vexflow/commit/5bbe70de5e5f35ce8a77bffbd69ae74b91d4fb47) beam reverted to stemmablenote

[b4a7c59796c51c58df9126805acaff07f2304d16](https://github.com/0xfe/vexflow/commit/b4a7c59796c51c58df9126805acaff07f2304d16) beam adapted to use note

[9af0bcd79e866548b8471544ae398932b1217510](https://github.com/0xfe/vexflow/commit/9af0bcd79e866548b8471544ae398932b1217510) voice migrated

[98c38eb78616e32affec0710fa620758cc0eb9c1](https://github.com/0xfe/vexflow/commit/98c38eb78616e32affec0710fa620758cc0eb9c1) voice renamed

[105ebacff90bc791e05c113e1ae909cc7a182415](https://github.com/0xfe/vexflow/commit/105ebacff90bc791e05c113e1ae909cc7a182415) review changes

[e381f5abf37e154f415242dc9f7ee1c575d3870a](https://github.com/0xfe/vexflow/commit/e381f5abf37e154f415242dc9f7ee1c575d3870a) review comments

[d0c28080f2d01df11e29371848ebf9b6f935b1e3](https://github.com/0xfe/vexflow/commit/d0c28080f2d01df11e29371848ebf9b6f935b1e3) curve migrated

[178736a14d0d0994205e720c754845e252226777](https://github.com/0xfe/vexflow/commit/178736a14d0d0994205e720c754845e252226777) curve renamed

[e1f370e0534433a220825db3e6ed8ab3137ba8ce](https://github.com/0xfe/vexflow/commit/e1f370e0534433a220825db3e6ed8ab3137ba8ce) Add npm script to generate images for all fonts.

[9b650510b7946660c104166a38373364e6f8f15a](https://github.com/0xfe/vexflow/commit/9b650510b7946660c104166a38373364e6f8f15a) Default to testing only Bravura. Add a flag to generate_png_images.js to allow us to customize which fonts to test. For example:   node generate_png_images.js SCRIPT_DIR IMAGE_OUTPUT_DIR --fonts=all   node generate_png_images.js SCRIPT_DIR IMAGE_OUTPUT_DIR --fonts=petaluma   node generate_png_images.js SCRIPT_DIR IMAGE_OUTPUT_DIR --fonts=bravura,gonville

[091c6bb0d4c5f498d52b2c7f89268fa5b90869f2](https://github.com/0xfe/vexflow/commit/091c6bb0d4c5f498d52b2c7f89268fa5b90869f2) Merge remote-tracking branch 'upstream/master' into vexflow_test_helpers

[ec03fb3cf194c48b67c95f6798b0e9bec5491c2e](https://github.com/0xfe/vexflow/commit/ec03fb3cf194c48b67c95f6798b0e9bec5491c2e) Merge pull request #936 from rvilarl/migration/tremolo

[73a32c674e4b8b347bc8649f98c0690d92cb9dd5](https://github.com/0xfe/vexflow/commit/73a32c674e4b8b347bc8649f98c0690d92cb9dd5) tremolo migrated

[2c6738df90b7a89be614e6df2989bb2620e6f9be](https://github.com/0xfe/vexflow/commit/2c6738df90b7a89be614e6df2989bb2620e6f9be) tremolo renamed

[32f3d110306dba3e2bfaae615808163a5a2296ee](https://github.com/0xfe/vexflow/commit/32f3d110306dba3e2bfaae615808163a5a2296ee) review comments

[ad6f6a8af4711aebf0e0a6fe4dd8f282c3f19673](https://github.com/0xfe/vexflow/commit/ad6f6a8af4711aebf0e0a6fe4dd8f282c3f19673) boundingbox* migrated

[a5b151192dfc1193096b96f1cc4e5b6166b05071](https://github.com/0xfe/vexflow/commit/a5b151192dfc1193096b96f1cc4e5b6166b05071) boundingbox* renamed

[83f39461f1fe66df540cab09f6a0429c060c554d](https://github.com/0xfe/vexflow/commit/83f39461f1fe66df540cab09f6a0429c060c554d) Merge pull request #929 from rvilarl/migration/beam

[69772129ad1e5cca1cd0a0118f5cb282d680dfc9](https://github.com/0xfe/vexflow/commit/69772129ad1e5cca1cd0a0118f5cb282d680dfc9) review comments

[44c23b117cdf52f78cabdf306ce5f7b31a57e42f](https://github.com/0xfe/vexflow/commit/44c23b117cdf52f78cabdf306ce5f7b31a57e42f) review comments

[fe5a48e81deb7b2ca53f63ef845769bf3fe024e5](https://github.com/0xfe/vexflow/commit/fe5a48e81deb7b2ca53f63ef845769bf3fe024e5) review comments

[b4587966ccfe1f7e9b4f0c87c5fed9e745958678](https://github.com/0xfe/vexflow/commit/b4587966ccfe1f7e9b4f0c87c5fed9e745958678) beam migrated

[2e72505abfbbc836cc49651b0f7c1703dc5019bf](https://github.com/0xfe/vexflow/commit/2e72505abfbbc836cc49651b0f7c1703dc5019bf) beam renamed

[134338f9d021a0d42abe59ee166124ee7a2fe36a](https://github.com/0xfe/vexflow/commit/134338f9d021a0d42abe59ee166124ee7a2fe36a) Customize Vex.Flow.Test.FONTS_TO_TEST to test fewer fonts. By default we test Bravura, Petaluma, and Gonville.

[b373637eb2ae700a6c6cbe2606448fdea461b317](https://github.com/0xfe/vexflow/commit/b373637eb2ae700a6c6cbe2606448fdea461b317) Merge pull request #931 from rvilarl/fix/note

[8c9032900c3a11492b96249b433ec0fbbedc6ad4](https://github.com/0xfe/vexflow/commit/8c9032900c3a11492b96249b433ec0fbbedc6ad4) review comments

[f316920e48ab035b14c935043fd8482cbeed48e0](https://github.com/0xfe/vexflow/commit/f316920e48ab035b14c935043fd8482cbeed48e0) Merge pull request #928 from rvilarl/migration/glyphnote

[700590112342086b6e1228a7c21a82d2f93edbb3](https://github.com/0xfe/vexflow/commit/700590112342086b6e1228a7c21a82d2f93edbb3) Merge pull request #927 from rvilarl/migration/gracetabnote

[0b277d4e115a3c82c6339c6c3eeacda90d0d8cd3](https://github.com/0xfe/vexflow/commit/0b277d4e115a3c82c6339c6c3eeacda90d0d8cd3) Merge pull request #926 from ronyeh/master

[6f5c4fd6dfe959ee71e4debee68ca6c39af89f8f](https://github.com/0xfe/vexflow/commit/6f5c4fd6dfe959ee71e4debee68ca6c39af89f8f) Improve runNodeTest() so that it works similarly to runSVGTest(). runNodeTest() now tests all three fonts, and outputs images files with names like:

[101d1da905aa83acce9dc8c2bc01e2d6f80afec3](https://github.com/0xfe/vexflow/commit/101d1da905aa83acce9dc8c2bc01e2d6f80afec3) Fix typos. Changed .js => .sh and added an 's' to the misspelled file name.

[66167e6ca207cd9958b10140370d6a0cb7b40e11](https://github.com/0xfe/vexflow/commit/66167e6ca207cd9958b10140370d6a0cb7b40e11) getBoundingRect already availabe in Element

[7b0ad05115927e56afe61fbe0e0a2950182367c2](https://github.com/0xfe/vexflow/commit/7b0ad05115927e56afe61fbe0e0a2950182367c2) use NoteStruct

[0a1c2368037fc7912f9ef2766974aaf292c8b9ab](https://github.com/0xfe/vexflow/commit/0a1c2368037fc7912f9ef2766974aaf292c8b9ab) glyphnote migrated

[77b4ce3f47307ae9b03b6ed8003cbe0b437096f9](https://github.com/0xfe/vexflow/commit/77b4ce3f47307ae9b03b6ed8003cbe0b437096f9) glyphnote renamed

[13b6e7e220d106437136376ee0f4ac218e73a232](https://github.com/0xfe/vexflow/commit/13b6e7e220d106437136376ee0f4ac218e73a232) StaveNoteStruct import

[0fb7f33b96662d192888b410b5c025426fd3dabb](https://github.com/0xfe/vexflow/commit/0fb7f33b96662d192888b410b5c025426fd3dabb) gracetabnote migrated

[a87cb482e895aee374c3bd7b34ead1b67a8b1f5c](https://github.com/0xfe/vexflow/commit/a87cb482e895aee374c3bd7b34ead1b67a8b1f5c) gracetabnote renamed

[ba85ad829c6ef9f3f1dce74dc37ac46faffffe70](https://github.com/0xfe/vexflow/commit/ba85ad829c6ef9f3f1dce74dc37ac46faffffe70) Fix small issue where parts of the stem are visible around the note head. This patch affects the Bravura font.

[0f24ef768028c19efa76b423ff4be0dff3882447](https://github.com/0xfe/vexflow/commit/0f24ef768028c19efa76b423ff4be0dff3882447) Merge pull request #925 from rvilarl/vibrato

[3edd11c0eecb5137fcdd5b24388810295759797a](https://github.com/0xfe/vexflow/commit/3edd11c0eecb5137fcdd5b24388810295759797a) Merge pull request #924 from rvilarl/migration/typedoc1

[f155b9ba6351dc08f1af759bce23123c0bfb33a6](https://github.com/0xfe/vexflow/commit/f155b9ba6351dc08f1af759bce23123c0bfb33a6) Merge pull request #921 from rvilarl/migration/stavenote2

[8476a7f195cbd09eddd041bc1e9cef03dafeca24](https://github.com/0xfe/vexflow/commit/8476a7f195cbd09eddd041bc1e9cef03dafeca24) vibrato migrated

[2fad5c1ad55fdd47521097314418dc877a6058e0](https://github.com/0xfe/vexflow/commit/2fad5c1ad55fdd47521097314418dc877a6058e0) vibrato renamed

[4219d5e135cfd033e7327b3d4d531f7d4bb375c9](https://github.com/0xfe/vexflow/commit/4219d5e135cfd033e7327b3d4d531f7d4bb375c9) typedoc update

[ae2c16d8ba4654718f096991a2bcb340e4e00c67](https://github.com/0xfe/vexflow/commit/ae2c16d8ba4654718f096991a2bcb340e4e00c67) review comments

[1fc965454931f3906ca43b582704a87e21b00e30](https://github.com/0xfe/vexflow/commit/1fc965454931f3906ca43b582704a87e21b00e30) review changes

[feaf1cd5a85b271fb41192a9247d13d0c477b505](https://github.com/0xfe/vexflow/commit/feaf1cd5a85b271fb41192a9247d13d0c477b505) Merge pull request #923 from rvilarl/migration/keysignote

[231510df71de0dea6a04cb0fbd908ae9c1e5507f](https://github.com/0xfe/vexflow/commit/231510df71de0dea6a04cb0fbd908ae9c1e5507f) review comments

[16d7694ab3730ade880bb0fca8df9106f65bc391](https://github.com/0xfe/vexflow/commit/16d7694ab3730ade880bb0fca8df9106f65bc391) Merge pull request #922 from rvilarl/migration/tabstave

[06c55f427479974e86c15a292ceb24d7cb5c7c4d](https://github.com/0xfe/vexflow/commit/06c55f427479974e86c15a292ceb24d7cb5c7c4d) NoteStruct reworked

[b372227cc3cda31c0068119b42295300bf278b96](https://github.com/0xfe/vexflow/commit/b372227cc3cda31c0068119b42295300bf278b96) keysignote migrated

[f6224c80df73ab51fc726c3131744c15e4895357](https://github.com/0xfe/vexflow/commit/f6224c80df73ab51fc726c3131744c15e4895357) keysignote renamed

[097113aeeb32ae3d2dd6e3d48345f098ab7b17c6](https://github.com/0xfe/vexflow/commit/097113aeeb32ae3d2dd6e3d48345f098ab7b17c6) StaveOptions imported

[55ca12dd05a0d6a5452cea50e4b077e5d5b2005a](https://github.com/0xfe/vexflow/commit/55ca12dd05a0d6a5452cea50e4b077e5d5b2005a) tabstave migrated

[59fcb64659b003c72669c0d4da15d4ccbfa4edd6](https://github.com/0xfe/vexflow/commit/59fcb64659b003c72669c0d4da15d4ccbfa4edd6) tabstave renamed

[8c507a244378f1cefc16d77ef16f184d5ed04585](https://github.com/0xfe/vexflow/commit/8c507a244378f1cefc16d77ef16f184d5ed04585) stavenote migrated

[9412e7b0c5391fa273167f799db08ebf50b3872f](https://github.com/0xfe/vexflow/commit/9412e7b0c5391fa273167f799db08ebf50b3872f) stavenote renamed

[342540fb5ee7f59bb58ee23c0b1246a2646ac61a](https://github.com/0xfe/vexflow/commit/342540fb5ee7f59bb58ee23c0b1246a2646ac61a) Merge pull request #917 from rvilarl/migration/fixStemmableNote

[01c1f68b5ba36ce46dccc9295e27083244140d5c](https://github.com/0xfe/vexflow/commit/01c1f68b5ba36ce46dccc9295e27083244140d5c) review comments

[eb229aaa8c38576009797e219e46df351175ccdd](https://github.com/0xfe/vexflow/commit/eb229aaa8c38576009797e219e46df351175ccdd) fix getYForTopText

[446d456051c3b6c9db46426678b6aa256ce69fd5](https://github.com/0xfe/vexflow/commit/446d456051c3b6c9db46426678b6aa256ce69fd5) Merge pull request #915 from rvilarl/migration/stavenote1

[e71e8aff509fd610af03b260400f42930bd563d6](https://github.com/0xfe/vexflow/commit/e71e8aff509fd610af03b260400f42930bd563d6) Merge pull request #916 from rvilarl/migration/refImages

[6130c0f7768e03a66019633fc112324b57f13fba](https://github.com/0xfe/vexflow/commit/6130c0f7768e03a66019633fc112324b57f13fba) preparation for stavenote migration

[aacf4f7b2c060791609e684a6c8ab936c8095e36](https://github.com/0xfe/vexflow/commit/aacf4f7b2c060791609e684a6c8ab936c8095e36) element attributes any

[b90527a6f386f2f377d30f6691d709dfae494863](https://github.com/0xfe/vexflow/commit/b90527a6f386f2f377d30f6691d709dfae494863) addMofier parameters fixed

[898ad327f4c8b4abcc349f7f9c2e21238b4c8bea](https://github.com/0xfe/vexflow/commit/898ad327f4c8b4abcc349f7f9c2e21238b4c8bea) modifier migration

[c8463dce1a0f603625d81ad7397f345cc8599f72](https://github.com/0xfe/vexflow/commit/c8463dce1a0f603625d81ad7397f345cc8599f72) modifier renamed

[9ff92fcb55321278b10c15e387caf5671e980301](https://github.com/0xfe/vexflow/commit/9ff92fcb55321278b10c15e387caf5671e980301) standard locations

[5c0f99deb0cbc52da58e7bfe8b314a822590ff20](https://github.com/0xfe/vexflow/commit/5c0f99deb0cbc52da58e7bfe8b314a822590ff20) gitignore images-ref

[7996cdf56ba84a6dc5e52567e882ba92bb19fd18](https://github.com/0xfe/vexflow/commit/7996cdf56ba84a6dc5e52567e882ba92bb19fd18) visual regression on reference

[a61b6f59bcd9376c00bd853573cb3a487bc8264f](https://github.com/0xfe/vexflow/commit/a61b6f59bcd9376c00bd853573cb3a487bc8264f) Merge pull request #908 from rvilarl/migration/stave

[e317732836198bca1c4206230e8c00090fb08a50](https://github.com/0xfe/vexflow/commit/e317732836198bca1c4206230e8c00090fb08a50) factory interfaces removed

[2c79b3168c883a836e08783940abd4b9adbf9148](https://github.com/0xfe/vexflow/commit/2c79b3168c883a836e08783940abd4b9adbf9148) package-lock.json reverted

[c30d013cb8a29b98074b1861e08f822ba739eb71](https://github.com/0xfe/vexflow/commit/c30d013cb8a29b98074b1861e08f822ba739eb71) review comments

[c533c8bbe71587d4332b0c6e90f097b8023e962d](https://github.com/0xfe/vexflow/commit/c533c8bbe71587d4332b0c6e90f097b8023e962d) FontStruct -> FontInfo

[714b1feab6228a15abde2ba1060a07430b9e83b8](https://github.com/0xfe/vexflow/commit/714b1feab6228a15abde2ba1060a07430b9e83b8) stave migrated

[ca8d130a4c3744b97e43d061e20eef8d3a39940e](https://github.com/0xfe/vexflow/commit/ca8d130a4c3744b97e43d061e20eef8d3a39940e) stave renamed

[6527cb7777d185a246b022ff3e9e10e0bac4af7f](https://github.com/0xfe/vexflow/commit/6527cb7777d185a246b022ff3e9e10e0bac4af7f) Merge pull request #910 from rvilarl/migration/fixFlag

[8bc3833af5fa4c007032f652840b00cdc999a639](https://github.com/0xfe/vexflow/commit/8bc3833af5fa4c007032f652840b00cdc999a639) fix flags

[e8bc7d9feb451d8771dbc699a47d0e0a868f1d62](https://github.com/0xfe/vexflow/commit/e8bc7d9feb451d8771dbc699a47d0e0a868f1d62) Merge pull request #906 from rvilarl/migration/textfont

[0053aae2ee42707e8cb3c546478ef6ed547fbcfa](https://github.com/0xfe/vexflow/commit/0053aae2ee42707e8cb3c546478ef6ed547fbcfa) Merge pull request #907 from rvilarl/migration/stem

[7e752ad0a0be29cce34c303436cec4edbb000024](https://github.com/0xfe/vexflow/commit/7e752ad0a0be29cce34c303436cec4edbb000024) StemStruct -> StemOptions

[44a1c6de5ec108c26fbe52eab5b1176331ec9780](https://github.com/0xfe/vexflow/commit/44a1c6de5ec108c26fbe52eab5b1176331ec9780) review comments

[7bbca50f080cd447f0a30f680deacb5d0697f6b3](https://github.com/0xfe/vexflow/commit/7bbca50f080cd447f0a30f680deacb5d0697f6b3) any resolved

[f8686ec99d70f5a63a422c1767b63ca7e0f05fc1](https://github.com/0xfe/vexflow/commit/f8686ec99d70f5a63a422c1767b63ca7e0f05fc1) stem migrated

[46499c2f2f2ae39313738e8ebf3b0db73824c9fc](https://github.com/0xfe/vexflow/commit/46499c2f2f2ae39313738e8ebf3b0db73824c9fc) stem renamed

[cf109552c1f206a212ec9d7aced719e9ba726cb7](https://github.com/0xfe/vexflow/commit/cf109552c1f206a212ec9d7aced719e9ba726cb7) members protected

[844860227c2557562623c0d617ff4439eccf8e2a](https://github.com/0xfe/vexflow/commit/844860227c2557562623c0d617ff4439eccf8e2a) textfont migrated

[826b5d6b89084ab0a3b2f69bda3fb835a504ea71](https://github.com/0xfe/vexflow/commit/826b5d6b89084ab0a3b2f69bda3fb835a504ea71) textfont renamed

[fcd809ce605d2c31516e5b3ab4e0d9cfd6c6f431](https://github.com/0xfe/vexflow/commit/fcd809ce605d2c31516e5b3ab4e0d9cfd6c6f431) Merge pull request #903 from rvilarl/migration/repeatnote

[8689e67501878a0a04ec891d329dd243d5ddca43](https://github.com/0xfe/vexflow/commit/8689e67501878a0a04ec891d329dd243d5ddca43) repeatnote migrated

[67d496927b524667b293a85e4bf0bb8feb07417a](https://github.com/0xfe/vexflow/commit/67d496927b524667b293a85e4bf0bb8feb07417a) repeatnote renamed

[4add403d0a7d71bfa30c6de0c3dadc5d43904c62](https://github.com/0xfe/vexflow/commit/4add403d0a7d71bfa30c6de0c3dadc5d43904c62) Merge pull request #898 from rvilarl/migration/stemmablenote

[5adca1b21287f51f8b2c24b166cf0aa95b37c535](https://github.com/0xfe/vexflow/commit/5adca1b21287f51f8b2c24b166cf0aa95b37c535) ?? resolved, rebased, typedocs updated

[4ea4d8caa44d431213a3de6c87d0e07d4b71dd7a](https://github.com/0xfe/vexflow/commit/4ea4d8caa44d431213a3de6c87d0e07d4b71dd7a) flag checked with hasFlag()

[b0f5b92aef0c6fdb271bdd1b2e9fdde49658b2cf](https://github.com/0xfe/vexflow/commit/b0f5b92aef0c6fdb271bdd1b2e9fdde49658b2cf) ?? rather than git add src/stemmablenote.ts , hasFlag to check if a flag is required

[8ac6c30aa467c08594373848cff3f84d6b52ce70](https://github.com/0xfe/vexflow/commit/8ac6c30aa467c08594373848cff3f84d6b52ce70) stemmablenote migrated

[d71c85e795268c0defc7ada21f95f4d8a2a33ad7](https://github.com/0xfe/vexflow/commit/d71c85e795268c0defc7ada21f95f4d8a2a33ad7) stemmablenote renamed

[436132164b481c8ba166cd125ff7baf7304ea345](https://github.com/0xfe/vexflow/commit/436132164b481c8ba166cd125ff7baf7304ea345) Merge pull request #899 from rvilarl/migration/glyph

[315401a17296900df952a3646eae4f90b80563b8](https://github.com/0xfe/vexflow/commit/315401a17296900df952a3646eae4f90b80563b8) fonts renamed

[894097dcc2ba2bcc06eee817849235c75f4bbcb2](https://github.com/0xfe/vexflow/commit/894097dcc2ba2bcc06eee817849235c75f4bbcb2) font migrated

[6cb65307e6162c271ebd6450dd8f23fff7993fd0](https://github.com/0xfe/vexflow/commit/6cb65307e6162c271ebd6450dd8f23fff7993fd0) smufl renamed to font

[2f14ee341ea119a2c34eab35d103280dab09983a](https://github.com/0xfe/vexflow/commit/2f14ee341ea119a2c34eab35d103280dab09983a) Merge pull request #900 from rvilarl/migration/typedoc

[3079f464c06e5294ed7a6dfba64db4d9f844879d](https://github.com/0xfe/vexflow/commit/3079f464c06e5294ed7a6dfba64db4d9f844879d) never resolved

[40bb40506cf559a0b39836a54053fb04e8f4a3b8](https://github.com/0xfe/vexflow/commit/40bb40506cf559a0b39836a54053fb04e8f4a3b8) typedoc exports

[e7fb68969d172bcdff4d26fe796adb5962c78420](https://github.com/0xfe/vexflow/commit/e7fb68969d172bcdff4d26fe796adb5962c78420) review comments & any resolved

[b047b3e8d0300488f8a8f806eb1dd1d9c565d787](https://github.com/0xfe/vexflow/commit/b047b3e8d0300488f8a8f806eb1dd1d9c565d787) glyph migrated

[7c6f9be8fa7408504df3cb48c30ee65d0ecd986b](https://github.com/0xfe/vexflow/commit/7c6f9be8fa7408504df3cb48c30ee65d0ecd986b) glyph renamed

[3d15a49713772df9e9a9cba3f22ed551a9153c2a](https://github.com/0xfe/vexflow/commit/3d15a49713772df9e9a9cba3f22ed551a9153c2a) Merge pull request #896 from rvilarl/migration/gracenotegroup

[a3f9bd31f477aa417b0403b39abeaf82fe66cb06](https://github.com/0xfe/vexflow/commit/a3f9bd31f477aa417b0403b39abeaf82fe66cb06) args on L() to any

[e3947e860d2cb971a151c371d6686308754e0045](https://github.com/0xfe/vexflow/commit/e3947e860d2cb971a151c371d6686308754e0045) Merge pull request #894 from rvilarl/migration/tickcontext

[3278f218113608ab1767f645762257d43d475f0f](https://github.com/0xfe/vexflow/commit/3278f218113608ab1767f645762257d43d475f0f) review comments

[04b6f2222e4ead671e7c2850047a7a5e4863fd51](https://github.com/0xfe/vexflow/commit/04b6f2222e4ead671e7c2850047a7a5e4863fd51) Merge pull request #895 from rvilarl/migration/voicegroup

[bbb2efbdef4beee18809aec6feb531de200d1c8b](https://github.com/0xfe/vexflow/commit/bbb2efbdef4beee18809aec6feb531de200d1c8b) members protected

[400790db7b7dc31936047b6a67abbd37d766138b](https://github.com/0xfe/vexflow/commit/400790db7b7dc31936047b6a67abbd37d766138b) tickcontext migrated

[5d6f14f6fd0d0b63196d0c7e3be3e45ad998b2ea](https://github.com/0xfe/vexflow/commit/5d6f14f6fd0d0b63196d0c7e3be3e45ad998b2ea) tickcontext reanamed

[4894dedb2d8dc7ec3dd9c047a8e56d850ed4076b](https://github.com/0xfe/vexflow/commit/4894dedb2d8dc7ec3dd9c047a8e56d850ed4076b) review comments

[4acd824f2829a811f64b1ee0ea9b69b2d5c43430](https://github.com/0xfe/vexflow/commit/4acd824f2829a811f64b1ee0ea9b69b2d5c43430) review comments

[99651b1cf2b69123fe324b1487949f946c086286](https://github.com/0xfe/vexflow/commit/99651b1cf2b69123fe324b1487949f946c086286) Merge pull request #892 from rvilarl/migration/note

[ef19ed42c8bb9fe464b29da1055c2d2a0fceef0f](https://github.com/0xfe/vexflow/commit/ef19ed42c8bb9fe464b29da1055c2d2a0fceef0f) members protected

[5e12d522be39483d4b918be924f3734e9f002847](https://github.com/0xfe/vexflow/commit/5e12d522be39483d4b918be924f3734e9f002847) members protected

[a2dcbc402f79acf442157d59cb20e15a390d6dcb](https://github.com/0xfe/vexflow/commit/a2dcbc402f79acf442157d59cb20e15a390d6dcb) gracenotegroup migrated

[80f9fb3bbb24ec186243a322957bef2badb4d4a0](https://github.com/0xfe/vexflow/commit/80f9fb3bbb24ec186243a322957bef2badb4d4a0) gracenotegroup renamed

[56d295803f2e07178e3a2903d444baa49e5af389](https://github.com/0xfe/vexflow/commit/56d295803f2e07178e3a2903d444baa49e5af389) voicegroup migrated

[4039f33734f98cf17519ecc2d1fe51cf8eced42f](https://github.com/0xfe/vexflow/commit/4039f33734f98cf17519ecc2d1fe51cf8eced42f) voicegroup renamed

[59059abd0a87d73012552ed62d5cb9dc75360eba](https://github.com/0xfe/vexflow/commit/59059abd0a87d73012552ed62d5cb9dc75360eba) review comments

[a34ca0191305929ff578a157b77bf4f391d58ea3](https://github.com/0xfe/vexflow/commit/a34ca0191305929ff578a157b77bf4f391d58ea3) common back to .d.ts

[d809f0a59faf38d17275105f632523cfb6d5896a](https://github.com/0xfe/vexflow/commit/d809f0a59faf38d17275105f632523cfb6d5896a) review comments

[847f021a8d1dd40563d6ba547d743483010f9f04](https://github.com/0xfe/vexflow/commit/847f021a8d1dd40563d6ba547d743483010f9f04) common.d.ts renamed commn.ts

[a03a5e82e01e27807578f8ee150d4c1230950e75](https://github.com/0xfe/vexflow/commit/a03a5e82e01e27807578f8ee150d4c1230950e75) comments and NoteStruct fix

[84cc3b0e968ecd6284e2d97ee3de51fe9d7125e8](https://github.com/0xfe/vexflow/commit/84cc3b0e968ecd6284e2d97ee3de51fe9d7125e8) member protected, setBeam fixed

[c77daad9c0c0c01269f98ba495f8c5a426994753](https://github.com/0xfe/vexflow/commit/c77daad9c0c0c01269f98ba495f8c5a426994753) glyph in note left as any

[716f074e2c5326a1488b5d08424508f6a7fa074c](https://github.com/0xfe/vexflow/commit/716f074e2c5326a1488b5d08424508f6a7fa074c) implement getWidth

[3669f182b6b7dc15769d2befd94fa04ffce88904](https://github.com/0xfe/vexflow/commit/3669f182b6b7dc15769d2befd94fa04ffce88904) Review comments

[078d385c8210f295e27797b29855b69f072ba9fb](https://github.com/0xfe/vexflow/commit/078d385c8210f295e27797b29855b69f072ba9fb) any resolved

[492e182914cbb8a754be508d021ed06c7207cc9d](https://github.com/0xfe/vexflow/commit/492e182914cbb8a754be508d021ed06c7207cc9d) note migrated

[82329d8b2d299838bdd75eeea8c5b33c3cd6d0a4](https://github.com/0xfe/vexflow/commit/82329d8b2d299838bdd75eeea8c5b33c3cd6d0a4) Merge pull request #891 from rvilarl/migration/tickable

[8b904b5d9b37eff5e4847a35d116ce28a56f0604](https://github.com/0xfe/vexflow/commit/8b904b5d9b37eff5e4847a35d116ce28a56f0604) eslint-disable-next-line added in tests

[269cd30ff08b43fa9cad3b9e09b9d00ef5d201a1](https://github.com/0xfe/vexflow/commit/269cd30ff08b43fa9cad3b9e09b9d00ef5d201a1) eslint-disable-next-line added

[b6798bf860020450b9fe4f27fc64b44786977457](https://github.com/0xfe/vexflow/commit/b6798bf860020450b9fe4f27fc64b44786977457) Merge pull request #889 from rvilarl/migration2/fractionMusicTuningTest

[c48903f2288e8b2af518fcf63d6f28a8f8ec9e3e](https://github.com/0xfe/vexflow/commit/c48903f2288e8b2af518fcf63d6f28a8f8ec9e3e) function return value added

[3ff52c125aaf2c5a705f9e4eb114faa586b9e97e](https://github.com/0xfe/vexflow/commit/3ff52c125aaf2c5a705f9e4eb114faa586b9e97e) review comments and typedoc

[614cb9792cb1e7c7ee3b1ab2aa50982349d4fc35](https://github.com/0xfe/vexflow/commit/614cb9792cb1e7c7ee3b1ab2aa50982349d4fc35) remove newlines

[dc341075e5f97558f373e4585dfbd67b399cf0f4](https://github.com/0xfe/vexflow/commit/dc341075e5f97558f373e4585dfbd67b399cf0f4) tickable migrated

[5123664b765887d2902ab7f189744e8a8941d9a6](https://github.com/0xfe/vexflow/commit/5123664b765887d2902ab7f189744e8a8941d9a6) tickable renamed

[664f36d0ee8a20eccdbde97e6b488d06c4c10499](https://github.com/0xfe/vexflow/commit/664f36d0ee8a20eccdbde97e6b488d06c4c10499) Merge pull request #890 from rvilarl/migration2/element

[f9219776c6731cdbbf6da79fda05cd5c64585988](https://github.com/0xfe/vexflow/commit/f9219776c6731cdbbf6da79fda05cd5c64585988) element comments and types

[83a4794b487adc1b1a2409f25722ed7a8d21a45e](https://github.com/0xfe/vexflow/commit/83a4794b487adc1b1a2409f25722ed7a8d21a45e) Merge pull request #882 from rvilarl/migration/element

[4b212ee5f0e22ad6fc254088f60a30ede9ade6d4](https://github.com/0xfe/vexflow/commit/4b212ee5f0e22ad6fc254088f60a30ede9ade6d4) 2nd step to simplify tests

[a61490afc685ef93f4d1da6b15e296ede7f97476](https://github.com/0xfe/vexflow/commit/a61490afc685ef93f4d1da6b15e296ede7f97476) constructor parameter fixed

[442d0179dd191e00e34949f05a38db6972865852](https://github.com/0xfe/vexflow/commit/442d0179dd191e00e34949f05a38db6972865852) access to attr back to getAttribute

[7ccf519acbd7a8ee5f013a52a0abb5c8c7c21ed4](https://github.com/0xfe/vexflow/commit/7ccf519acbd7a8ee5f013a52a0abb5c8c7c21ed4) review comments

[825ec820a446e44c6a05f59351cb6b6e9494b4a3](https://github.com/0xfe/vexflow/commit/825ec820a446e44c6a05f59351cb6b6e9494b4a3) Merge pull request #888 from wassertim/bugfix/887

[1018bd927d6faa716ab320b0e5e6f5044cd3bd4d](https://github.com/0xfe/vexflow/commit/1018bd927d6faa716ab320b0e5e6f5044cd3bd4d) Style renamed to ElementStyle

[854b5e9fe70c431faf4570e27ec456d0816db708](https://github.com/0xfe/vexflow/commit/854b5e9fe70c431faf4570e27ec456d0816db708) 2 PRs approach two fix diff

[273c24b943872d5f48d11933a75d5310948268e4](https://github.com/0xfe/vexflow/commit/273c24b943872d5f48d11933a75d5310948268e4) typescript #887 add js files to ts-loader

[e1ac53d56e7a91b75366efc552ab1fbbd156c3c7](https://github.com/0xfe/vexflow/commit/e1ac53d56e7a91b75366efc552ab1fbbd156c3c7) element in typedoc

[79cac5b15d744c45f4064952e6f780098984ff49](https://github.com/0xfe/vexflow/commit/79cac5b15d744c45f4064952e6f780098984ff49) element refactored

[95b1e98bb1f9250cbb17b15344f044b4ef674e46](https://github.com/0xfe/vexflow/commit/95b1e98bb1f9250cbb17b15344f044b4ef674e46) element migrated

[95623df5fc2afe54f3dbd9ed974566010420f3e0](https://github.com/0xfe/vexflow/commit/95623df5fc2afe54f3dbd9ed974566010420f3e0) element.js renamed

[9d22e4cea7ab6ca83f96f86122e747e0488b3dec](https://github.com/0xfe/vexflow/commit/9d22e4cea7ab6ca83f96f86122e747e0488b3dec) Merge pull request #877 from rvilarl/migration/tuningFractionTest

[4b769afbab7e67b438f4915554b627d29c093d0f](https://github.com/0xfe/vexflow/commit/4b769afbab7e67b438f4915554b627d29c093d0f) no-inferrable-types reverted to off

[33c45b505ed507d97529e86375b5297d9057c22d](https://github.com/0xfe/vexflow/commit/33c45b505ed507d97529e86375b5297d9057c22d) tests reverted

[1154e6c9996cbfb6be161e7559dfacd41c777303](https://github.com/0xfe/vexflow/commit/1154e6c9996cbfb6be161e7559dfacd41c777303) Merge pull request #874 from rvilarl/ts_typedoc

[5a84a8192f253a55f57edbfa4f407dfe24541172](https://github.com/0xfe/vexflow/commit/5a84a8192f253a55f57edbfa4f407dfe24541172) Review comments

[ef07e1a9207ed034d55eeacc67f42e74dbdbbc87](https://github.com/0xfe/vexflow/commit/ef07e1a9207ed034d55eeacc67f42e74dbdbbc87) simplify test modules

[3285add85ceecda53a19fa88dc0296510967c654](https://github.com/0xfe/vexflow/commit/3285add85ceecda53a19fa88dc0296510967c654) fix typos

[2596ca67a2dc25650c5896afb58af6578cfe4d2f](https://github.com/0xfe/vexflow/commit/2596ca67a2dc25650c5896afb58af6578cfe4d2f) releases/typedoc removed

[4512a1ad7efb1d2ccbda30cb1c129ad5cea5e98d](https://github.com/0xfe/vexflow/commit/4512a1ad7efb1d2ccbda30cb1c129ad5cea5e98d) typedoc & grunt-typedoc moved to devDependencies

[b711c17e90baa05e033a09fc1ff4b1cdd75845f0](https://github.com/0xfe/vexflow/commit/b711c17e90baa05e033a09fc1ff4b1cdd75845f0) typedoc added

[7dddcf95baa0e6f5ba409af0fef41a440280a092](https://github.com/0xfe/vexflow/commit/7dddcf95baa0e6f5ba409af0fef41a440280a092) declaration.ts used in tests

[1c7ac5e6e83b9339cf0223cb517ceae775297a7c](https://github.com/0xfe/vexflow/commit/1c7ac5e6e83b9339cf0223cb517ceae775297a7c) music_tests and typescripts rules

[e41aac637e0914ff0887561f49aadd8c586556cb](https://github.com/0xfe/vexflow/commit/e41aac637e0914ff0887561f49aadd8c586556cb) linter fixes

[9e9842578a588cec294911f19c774fd6189828ae](https://github.com/0xfe/vexflow/commit/9e9842578a588cec294911f19c774fd6189828ae) tuning_tests & fractions_tests migrated

[1c028fc1d16d9efbde8fb9d9887e8cb7076934ba](https://github.com/0xfe/vexflow/commit/1c028fc1d16d9efbde8fb9d9887e8cb7076934ba) files renamed

[2d181692b6d3ac7c625b6fd77acb06e79600306b](https://github.com/0xfe/vexflow/commit/2d181692b6d3ac7c625b6fd77acb06e79600306b) Merge pull request #878 from wassertim/test_declarations

[e5465975b832c2a7fd4ecd714a9b52e288e3172a](https://github.com/0xfe/vexflow/commit/e5465975b832c2a7fd4ecd714a9b52e288e3172a) put test declarations in a separate file

[1458abaf2206343a786ecfaebeea680565607f67](https://github.com/0xfe/vexflow/commit/1458abaf2206343a786ecfaebeea680565607f67) Merge pull request #873 from wassertim/migration/music-ts

[de24f9e5cc2bdf2be36b35245278e13317bcba6a](https://github.com/0xfe/vexflow/commit/de24f9e5cc2bdf2be36b35245278e13317bcba6a) remove the font

[1154e77951ba8875564109377c7cce26433a0186](https://github.com/0xfe/vexflow/commit/1154e77951ba8875564109377c7cce26433a0186) put shims in a structure

[83c7aca8deaefddc6375b190af1fcd50614006cd](https://github.com/0xfe/vexflow/commit/83c7aca8deaefddc6375b190af1fcd50614006cd) add canonicalIntervals to the test

[8fe4a61c7d15839629526af57904880795fe1ddc](https://github.com/0xfe/vexflow/commit/8fe4a61c7d15839629526af57904880795fe1ddc) keep minimal change of music_tests.js

[8e4fb069405af9b784d31599030ca5350a3acf8c](https://github.com/0xfe/vexflow/commit/8e4fb069405af9b784d31599030ca5350a3acf8c) rollback release files

[a918bad2493c0a071d0882b898d91bf9f0b5665d](https://github.com/0xfe/vexflow/commit/a918bad2493c0a071d0882b898d91bf9f0b5665d) rollback release files

[17f23f3a1c5587e470634608769c7f4f0ed9a0f4](https://github.com/0xfe/vexflow/commit/17f23f3a1c5587e470634608769c7f4f0ed9a0f4) shim node objects

[ffe489a7d16cf9ac73860bc05a8c7de672b482c0](https://github.com/0xfe/vexflow/commit/ffe489a7d16cf9ac73860bc05a8c7de672b482c0) wip

[349cea4091211623174cdd4d20f9bf6a889592f7](https://github.com/0xfe/vexflow/commit/349cea4091211623174cdd4d20f9bf6a889592f7) bring music tests back

[ca4d3b2bcc54e1f1eef3bd14e08779fa03cb0857](https://github.com/0xfe/vexflow/commit/ca4d3b2bcc54e1f1eef3bd14e08779fa03cb0857) revert back to music_tests.js

[d768aaae5ab2eea81cec3769b764cf48a3e645f5](https://github.com/0xfe/vexflow/commit/d768aaae5ab2eea81cec3769b764cf48a3e645f5) set pretier to autofix

[a30ca33fad4445413ef8ec6cc8b6bb0c4b2509d9](https://github.com/0xfe/vexflow/commit/a30ca33fad4445413ef8ec6cc8b6bb0c4b2509d9) revert tsconfig

[0be4044885399c2b2a4d3d5fc83e20362c2f257b](https://github.com/0xfe/vexflow/commit/0be4044885399c2b2a4d3d5fc83e20362c2f257b) remove lint errors

[2624d561749e0a45a6d1f5e04ac3ba1fc7c67c4a](https://github.com/0xfe/vexflow/commit/2624d561749e0a45a6d1f5e04ac3ba1fc7c67c4a) fix remarks #858

[00724ce60cbec39045b7e095440d07c4eddbfa04](https://github.com/0xfe/vexflow/commit/00724ce60cbec39045b7e095440d07c4eddbfa04) compile all the tests with webpack. No concatenation, no flow_ts.html #858

[94c72fb3bf20dbe773eeb18ddc2606327effff2a](https://github.com/0xfe/vexflow/commit/94c72fb3bf20dbe773eeb18ddc2606327effff2a) Merge pull request #861 from rvilarl/ts_tuningFraction

[0d7f44c1f16117d0aa402f2fac9d937b39ab4e4f](https://github.com/0xfe/vexflow/commit/0d7f44c1f16117d0aa402f2fac9d937b39ab4e4f) Using Number to convert stringNum, comments update

[a31225c40e2584f9208fa3e831d7f840c00f14ad](https://github.com/0xfe/vexflow/commit/a31225c40e2584f9208fa3e831d7f840c00f14ad) Merge pull request #868 from AaronDavidNewman/master

[13deeb24d264057395f8eb6d81fd13c65390ed51](https://github.com/0xfe/vexflow/commit/13deeb24d264057395f8eb6d81fd13c65390ed51) remove annoying font warning

[8b581cf0ed82eeecd886bddcceb83f632b0dd3b5](https://github.com/0xfe/vexflow/commit/8b581cf0ed82eeecd886bddcceb83f632b0dd3b5) Merge https://github.com/0xfe/vexflow

[7e8db46b1fc2bec0168585e5b4d3c3836c014416](https://github.com/0xfe/vexflow/commit/7e8db46b1fc2bec0168585e5b4d3c3836c014416) ++ replacement reverted

[fc24e2a2ae3bb8179fae4f1480d591e9dcd5c023](https://github.com/0xfe/vexflow/commit/fc24e2a2ae3bb8179fae4f1480d591e9dcd5c023) review comments

[850db003c0c8a0f47eb9338a3fb7291022c341f3](https://github.com/0xfe/vexflow/commit/850db003c0c8a0f47eb9338a3fb7291022c341f3) fraction update

[2559fc8257f86a293da790112d7c0549ea6231fb](https://github.com/0xfe/vexflow/commit/2559fc8257f86a293da790112d7c0549ea6231fb) tuning & fraction typescript migration

[7faeed54f4ca8e5453297ec7a804a57b1a761fa7](https://github.com/0xfe/vexflow/commit/7faeed54f4ca8e5453297ec7a804a57b1a761fa7) tuning & fraction renamed

[7844a090509decfc4532621a8da3149dda347e7b](https://github.com/0xfe/vexflow/commit/7844a090509decfc4532621a8da3149dda347e7b) Merge pull request #866 from rvilarl/formatter/1

[29b8315579a9e1ca510058fe16cf386f52746c30](https://github.com/0xfe/vexflow/commit/29b8315579a9e1ca510058fe16cf386f52746c30) joinVoices has 1 parameter (fixes #860)

[23a8bc827f3ce09f241710d0cf17cab0b3f5560c](https://github.com/0xfe/vexflow/commit/23a8bc827f3ce09f241710d0cf17cab0b3f5560c) Merge pull request #864 from rvilarl/ts_mapGeneration

[c44adf1ffd27870cbc2005c4209e4ac9e905f5ec](https://github.com/0xfe/vexflow/commit/c44adf1ffd27870cbc2005c4209e4ac9e905f5ec) Gruntfile.js reverted

[101b7c11eee24bbca6514d5b4123872e41e9d3e8](https://github.com/0xfe/vexflow/commit/101b7c11eee24bbca6514d5b4123872e41e9d3e8) Merge pull request #863 from rvilarl/ts_dependenciesUpdate

[d5c276f21a29b28b662a6fcceb8ecc41130b53c8](https://github.com/0xfe/vexflow/commit/d5c276f21a29b28b662a6fcceb8ecc41130b53c8) map generation with typescript

[fdb3bff5a16d5dc9c3aaac8501248d63c46303e9](https://github.com/0xfe/vexflow/commit/fdb3bff5a16d5dc9c3aaac8501248d63c46303e9) #859 Dependencies updated to avoid checks fail on PR

[994ee49df8fb03b3c3a0f368b488a92e05a54f71](https://github.com/0xfe/vexflow/commit/994ee49df8fb03b3c3a0f368b488a92e05a54f71) change flow.css URLs to pull from cloud

[251f67b6444990d091fe060ca5a0ce8688c9b251](https://github.com/0xfe/vexflow/commit/251f67b6444990d091fe060ca5a0ce8688c9b251) Merge pull request #856 from rvilarl/ts_airbnb

[54234831928043e2757886c4e28af9d6cc1b211c](https://github.com/0xfe/vexflow/commit/54234831928043e2757886c4e28af9d6cc1b211c) Gruntfile eslint target fixed

[cd1477a52ed8d696df76c5fff11f22749978101c](https://github.com/0xfe/vexflow/commit/cd1477a52ed8d696df76c5fff11f22749978101c) package eslint updates reverted

[909c08235b54b7ea12d4eab56f4275725a9ae8fd](https://github.com/0xfe/vexflow/commit/909c08235b54b7ea12d4eab56f4275725a9ae8fd) airbnb removed again

[1d01aa8d732a057cbf6eaac28b89d4bf554ebc27](https://github.com/0xfe/vexflow/commit/1d01aa8d732a057cbf6eaac28b89d4bf554ebc27) class-methods-use changed to comment in file, test actions reverted

[dbef7a746071671ca6a840f79d1f62144edce512](https://github.com/0xfe/vexflow/commit/dbef7a746071671ca6a840f79d1f62144edce512) Merge pull request #857 from wassertim/fix_new_keyword_mess

[355dc974823217dfce1b3c9a85989ad112adcdca](https://github.com/0xfe/vexflow/commit/355dc974823217dfce1b3c9a85989ad112adcdca) fix new keyword mess

[3ef74e86c128edc82b091f369e24d7761a2cec3f](https://github.com/0xfe/vexflow/commit/3ef74e86c128edc82b091f369e24d7761a2cec3f) CI tests fixed

[98e2206e3c95c33189ae53e1b10b299920ec4fa7](https://github.com/0xfe/vexflow/commit/98e2206e3c95c33189ae53e1b10b299920ec4fa7) airbnb with rule to only warn on class-methods-use-this

[b33f4899182f651929889238b830a92b76e5c2d6](https://github.com/0xfe/vexflow/commit/b33f4899182f651929889238b830a92b76e5c2d6) airbnb changes removed

[1924b2cc268de33fb19bbc8ba62c59b635614ea4](https://github.com/0xfe/vexflow/commit/1924b2cc268de33fb19bbc8ba62c59b635614ea4) Merge pull request #849 from AaronDavidNewman/master

[5f087800757bb15526350b398652e94de353ca43](https://github.com/0xfe/vexflow/commit/5f087800757bb15526350b398652e94de353ca43) eslint-plugin-import updated

[f17a25484c6beb2a39fea17b612a12a81a95e5c1](https://github.com/0xfe/vexflow/commit/f17a25484c6beb2a39fea17b612a12a81a95e5c1) airbnb support & babel removal

[ec3e5c1fe52cf3e6d41b318a33b12dbabfb271d0](https://github.com/0xfe/vexflow/commit/ec3e5c1fe52cf3e6d41b318a33b12dbabfb271d0) Merge https://github.com/0xfe/vexflow

[5d5bba84bdeee601242cd84508b772dbb8fac250](https://github.com/0xfe/vexflow/commit/5d5bba84bdeee601242cd84508b772dbb8fac250) remove blank line

[a2dc44290021a5ae7a65fce2ed204121856bd364](https://github.com/0xfe/vexflow/commit/a2dc44290021a5ae7a65fce2ed204121856bd364) Merge pull request #851 from rvilarl/ts_infrastructure

[3b7908921664a792e693cfb91f0888fd35540bf1](https://github.com/0xfe/vexflow/commit/3b7908921664a792e693cfb91f0888fd35540bf1) changes based on code review

[11956436bb0f2e51a7256b337193cbdcd28daec7](https://github.com/0xfe/vexflow/commit/11956436bb0f2e51a7256b337193cbdcd28daec7) 2nd review comments addressed

[f0bb5793a2e5e28138a1d48669dc1f0b966c437f](https://github.com/0xfe/vexflow/commit/f0bb5793a2e5e28138a1d48669dc1f0b966c437f) Review comments closed

[0f73c6bbb0569c920a09eba82ad48feb0006046d](https://github.com/0xfe/vexflow/commit/0f73c6bbb0569c920a09eba82ad48feb0006046d) 0xfe review

[237d05c7d766137afa38af5989f060cee5d01beb](https://github.com/0xfe/vexflow/commit/237d05c7d766137afa38af5989f060cee5d01beb) testing and code review changes for annotation text metrics

[8dabd071462979de55478edd04ef8e8904930a97](https://github.com/0xfe/vexflow/commit/8dabd071462979de55478edd04ef8e8904930a97) Remove releases files

[2e2509c728b61a40c922d9d14c5c85b3c4f44395](https://github.com/0xfe/vexflow/commit/2e2509c728b61a40c922d9d14c5c85b3c4f44395) add typescript infrastructure and migrate music.js to ts (#850)

[e9209f6853cd16c01c2c470fc36370a4aad69513](https://github.com/0xfe/vexflow/commit/e9209f6853cd16c01c2c470fc36370a4aad69513) remove magic fraction, auto-set font size if provided

[3aacb8e359445b7e4d381e025cf75cb01e56ea06](https://github.com/0xfe/vexflow/commit/3aacb8e359445b7e4d381e025cf75cb01e56ea06) Merge branch 'master' of https://github.com/0xfe/vexflow

[71e89f65f59c3e13f38de3a431cd7a6b006db7e6](https://github.com/0xfe/vexflow/commit/71e89f65f59c3e13f38de3a431cd7a6b006db7e6) Use text metrics to calculate annotation widths

[5eb92750f65fe07d6115073d8e3be1a8fa2c191c](https://github.com/0xfe/vexflow/commit/5eb92750f65fe07d6115073d8e3be1a8fa2c191c) Add eslint --fix to grunt.

[aba42d95e6d3dd4e011e7003305cd2277595371e](https://github.com/0xfe/vexflow/commit/aba42d95e6d3dd4e011e7003305cd2277595371e) Overhaul and simplify eslint configuration, and add support for prettier

[dc97b0cc5bb93171c0038638c34362dc958222ca](https://github.com/0xfe/vexflow/commit/dc97b0cc5bb93171c0038638c34362dc958222ca) Stylistic fixes.

[e1945912204e3cb3b459004875ce7fee2976ada5](https://github.com/0xfe/vexflow/commit/e1945912204e3cb3b459004875ce7fee2976ada5) Fix #839. Don't shift more than 5% to the right of the previous context.

[7efc31f1190b3cb985e7f6c6446dfd2fb13cd146](https://github.com/0xfe/vexflow/commit/7efc31f1190b3cb985e7f6c6446dfd2fb13cd146) Fix some broken behavior in formatter. Undo #830.

[3fa288706e369c2c1548c5f1275657045d422917](https://github.com/0xfe/vexflow/commit/3fa288706e369c2c1548c5f1275657045d422917) Merge pull request #843 from AaronDavidNewman/master

[7e8261351f1922803545ed71b2035db1a70eb127](https://github.com/0xfe/vexflow/commit/7e8261351f1922803545ed71b2035db1a70eb127) correct <> in warning

[dd9e5064d4e65b925346d28a2a50e3b03a44d9e0](https://github.com/0xfe/vexflow/commit/dd9e5064d4e65b925346d28a2a50e3b03a44d9e0) add format warning

[23f8ed9b52834d4e6748a35d8ff288ea5679688f](https://github.com/0xfe/vexflow/commit/23f8ed9b52834d4e6748a35d8ff288ea5679688f) move accidental test

[c66ef9f5a51ea3359b7a1dadb20e27ef0684f55d](https://github.com/0xfe/vexflow/commit/c66ef9f5a51ea3359b7a1dadb20e27ef0684f55d) add some formatter test cases

[739b8e624caef080b214a2b85105ee59b78c2099](https://github.com/0xfe/vexflow/commit/739b8e624caef080b214a2b85105ee59b78c2099) Merge pull request #838 from AaronDavidNewman/master

[bfd1473bd8b01c11837fcd1348afafbc8fc3c3db](https://github.com/0xfe/vexflow/commit/bfd1473bd8b01c11837fcd1348afafbc8fc3c3db) revert release files to master version

[c9fc61eb0e519f7553df3c3f9b97ac1c2ca1ef3e](https://github.com/0xfe/vexflow/commit/c9fc61eb0e519f7553df3c3f9b97ac1c2ca1ef3e) remove text-font-specific fields from music font generator

[f1a83efb4918020e1870549369777e6fdb49da06](https://github.com/0xfe/vexflow/commit/f1a83efb4918020e1870549369777e6fdb49da06) update release build

[8f4c82fd8fc0603dae24f1aa110be8958bd846e1](https://github.com/0xfe/vexflow/commit/8f4c82fd8fc0603dae24f1aa110be8958bd846e1) chordsymbol factory fix, smufl fontgen skip missing glyphs

[1a6275c7b8e8759bd0623c6dee0779a4ce7c84e7](https://github.com/0xfe/vexflow/commit/1a6275c7b8e8759bd0623c6dee0779a4ce7c84e7) Merge pull request #830 from deemaagog/fix-preCalculateMinTotalWidth

[def7d9b319096fa9dae7ebb674fd87af8c27ee25](https://github.com/0xfe/vexflow/commit/def7d9b319096fa9dae7ebb674fd87af8c27ee25) Merge pull request #831 from AaronDavidNewman/master

[a3cb4fd3590cb32463126f879b41375f0cc6740b](https://github.com/0xfe/vexflow/commit/a3cb4fd3590cb32463126f879b41375f0cc6740b) Opt-out of reporting width for chord symbols

[d3de4a263b414ff3cd7e9d6f9c19d13ca289d4ed](https://github.com/0xfe/vexflow/commit/d3de4a263b414ff3cd7e9d6f9c19d13ca289d4ed) Fix

[656be044ae21053c32b2704b6c6fc7e26633f2fa](https://github.com/0xfe/vexflow/commit/656be044ae21053c32b2704b6c6fc7e26633f2fa) Merge pull request #826 from wassertim/draw_ledger_lines_in_stavenote_group

[382a219258994bf3bed59fec088f6cf873db351d](https://github.com/0xfe/vexflow/commit/382a219258994bf3bed59fec088f6cf873db351d) put drawLedgerLines to stavenotegroup

[1120c9b266aead283de82d10e7cd325c78638aad](https://github.com/0xfe/vexflow/commit/1120c9b266aead283de82d10e7cd325c78638aad) Merge pull request #819 from wassertim/travis_to_github_actions

[58933ac3d59ba00857b6eae35016f369bd84ec97](https://github.com/0xfe/vexflow/commit/58933ac3d59ba00857b6eae35016f369bd84ec97) use github actions instead of travis

[2ad22675669e8130d913ac010fd9b6a012561d31](https://github.com/0xfe/vexflow/commit/2ad22675669e8130d913ac010fd9b6a012561d31) Merge pull request #812 from AaronDavidNewman/master

[39b4842c5daaceead48b901cae0af00da727a92f](https://github.com/0xfe/vexflow/commit/39b4842c5daaceead48b901cae0af00da727a92f) Merge pull request #817 from Sagittal/master

[b0a18feca25eab5c7d3cfa53a06fea382c6984de](https://github.com/0xfe/vexflow/commit/b0a18feca25eab5c7d3cfa53a06fea382c6984de) Rename textFont.js to textfont.js

[2d270ada5354587858fda7d0493e970938fb9639](https://github.com/0xfe/vexflow/commit/2d270ada5354587858fda7d0493e970938fb9639) Changes for code review

[4c6ba6d658303fd463c54e3fd7ee52075bb5b671](https://github.com/0xfe/vexflow/commit/4c6ba6d658303fd463c54e3fd7ee52075bb5b671) improve sagittal tests

[85acbf06aea98a1a3aa369d3b521bdb21e60f2c8](https://github.com/0xfe/vexflow/commit/85acbf06aea98a1a3aa369d3b521bdb21e60f2c8) fix sagittal tests

[458c870508f90e875d2c97370d65a23555089a26](https://github.com/0xfe/vexflow/commit/458c870508f90e875d2c97370d65a23555089a26) register test to run, and give it distinct name

[6fcb2d98794511273c5e425c3a437f89febf2318](https://github.com/0xfe/vexflow/commit/6fcb2d98794511273c5e425c3a437f89febf2318) Add Sagittal accidentals

[00c8a0d17092c24e40dd4519d4b8ec59c711923c](https://github.com/0xfe/vexflow/commit/00c8a0d17092c24e40dd4519d4b8ec59c711923c) Merge pull request #813 from Andrew13648/master

[876d40e4e65c8e537d16e90c9aa331dc587e33fc](https://github.com/0xfe/vexflow/commit/876d40e4e65c8e537d16e90c9aa331dc587e33fc) Added support for fingerings in EasyScore

[c418322d0c5cd3f8714063cf429c3cc0cc3cbf73](https://github.com/0xfe/vexflow/commit/c418322d0c5cd3f8714063cf429c3cc0cc3cbf73) Merge branch 'master' of https://github.com/0xfe/vexflow

[3318d3488e06b0aaa0606781890cde936375621b](https://github.com/0xfe/vexflow/commit/3318d3488e06b0aaa0606781890cde936375621b) added missing semicolons for eslint

[94201479b86452cf6d49b24a62cc03cdca4be951](https://github.com/0xfe/vexflow/commit/94201479b86452cf6d49b24a62cc03cdca4be951) Text Font feature

[c07516f3ce3d997e2cc0855742f95e53b71d9bd8](https://github.com/0xfe/vexflow/commit/c07516f3ce3d997e2cc0855742f95e53b71d9bd8) Merge pull request #807 from mscuthbert/stem_length

[65bed623585f53cb22c771895f75105d6746d970](https://github.com/0xfe/vexflow/commit/65bed623585f53cb22c771895f75105d6746d970) No need for such a talk contextBuilder

[6899edbf5656bd9854add9f721f9d0dfeb63f0a2](https://github.com/0xfe/vexflow/commit/6899edbf5656bd9854add9f721f9d0dfeb63f0a2) add tests

[4f348c7474bd2251246a7ab73313f9f7fd2c5989](https://github.com/0xfe/vexflow/commit/4f348c7474bd2251246a7ab73313f9f7fd2c5989) stemExtension by note position

[d1ae486345772bdf75b749257d1ba4582d21c394](https://github.com/0xfe/vexflow/commit/d1ae486345772bdf75b749257d1ba4582d21c394) stemExtensionOverride to underscore

[f264d0c1d81b1ca40c4054271c3cc90339d9c1ff](https://github.com/0xfe/vexflow/commit/f264d0c1d81b1ca40c4054271c3cc90339d9c1ff) Merge pull request #804 from sschmidTU/feat/add-tabnote-context-group

[2050b52303128bee9671d7b0ea759f37a062bba9](https://github.com/0xfe/vexflow/commit/2050b52303128bee9671d7b0ea759f37a062bba9) Merge pull request #801 from AaronDavidNewman/master

[551a2a6478fd0b00c89adcd24b6c572207926b08](https://github.com/0xfe/vexflow/commit/551a2a6478fd0b00c89adcd24b6c572207926b08) add context/svg group for tabnote

[6d0b27ea50a8ccca121ddba9ee04588c628e6b3b](https://github.com/0xfe/vexflow/commit/6d0b27ea50a8ccca121ddba9ee04588c628e6b3b) updates based on code review

[f11786b5338b65adc6ed03cfd62aa9e1f29d9a16](https://github.com/0xfe/vexflow/commit/f11786b5338b65adc6ed03cfd62aa9e1f29d9a16) relocate jazz ornaments to ornaments module

[65d753426cc2fffc5ef35d5adc06f92cdca7314d](https://github.com/0xfe/vexflow/commit/65d753426cc2fffc5ef35d5adc06f92cdca7314d) fix some copy/paste comments

[5ec9dc27fc741b8b3267409b9f282f68539b2837](https://github.com/0xfe/vexflow/commit/5ec9dc27fc741b8b3267409b9f282f68539b2837) Jazzy ornaments and techniques - drop, doit, etc.

[c7ab29f90480125350d7d0ab3d95c4ce19f738cc](https://github.com/0xfe/vexflow/commit/c7ab29f90480125350d7d0ab3d95c4ce19f738cc) Merge pull request #797 from AaronDavidNewman/master

[a6c4871f373bdce048926edf0ba6ec4d011ade98](https://github.com/0xfe/vexflow/commit/a6c4871f373bdce048926edf0ba6ec4d011ade98) Get google font from google fonts

[4f0b42274c25b42c727aa0860f2a4df3a25e71f9](https://github.com/0xfe/vexflow/commit/4f0b42274c25b42c727aa0860f2a4df3a25e71f9) Merge fixes from smoosic branch

[0c51ce456be0bc1ce008a7de384770d2c041db51](https://github.com/0xfe/vexflow/commit/0c51ce456be0bc1ce008a7de384770d2c041db51) Merge pull request #796 from sschmidTU/fix/volta-length-with-modifiers-and-ds-offset

[11c9583c62b684d177cba2f98ecb4e7d97a72236](https://github.com/0xfe/vexflow/commit/11c9583c62b684d177cba2f98ecb4e7d97a72236) comment

[a8b2d6c259ed2765d21d9fb5309c95d24ab475b0](https://github.com/0xfe/vexflow/commit/a8b2d6c259ed2765d21d9fb5309c95d24ab475b0) fix wrong line commented (stave volta length)

[3c512be32f0d184db2e8208e49ba52331b711c75](https://github.com/0xfe/vexflow/commit/3c512be32f0d184db2e8208e49ba52331b711c75) fix linting

[f8801634bfc4d0f60efc3ab29eb03e02e187555e](https://github.com/0xfe/vexflow/commit/f8801634bfc4d0f60efc3ab29eb03e02e187555e) fix(volta, D.S.) fix length of voltas with beginning modifiers going beyond measure end, position of D.S. text

[3cc8680cb7e31eb2f9bcc981f275461352f128f6](https://github.com/0xfe/vexflow/commit/3cc8680cb7e31eb2f9bcc981f275461352f128f6) Merge pull request #795 from AaronDavidNewman/master

[2e6e61b15dc2ec9eeaf110ad1335313f6bc73cd9](https://github.com/0xfe/vexflow/commit/2e6e61b15dc2ec9eeaf110ad1335313f6bc73cd9) Environment variable to produce map for debug monolith

[9f413fa2a7be2e1835c98226371574fddb626c9c](https://github.com/0xfe/vexflow/commit/9f413fa2a7be2e1835c98226371574fddb626c9c) generate map file in debug mode

[1c5174a8bfff56fae009c98564632378c82ea9e8](https://github.com/0xfe/vexflow/commit/1c5174a8bfff56fae009c98564632378c82ea9e8) Merge pull request #790 from AaronDavidNewman/master

[9f29e6c6fdb4f9518ffe318be02034d2ac6d1b65](https://github.com/0xfe/vexflow/commit/9f29e6c6fdb4f9518ffe318be02034d2ac6d1b65) trying to do a case change for the file in GIT

[8b93c792b8be90a3f7f010dab2aa3748cd8cab6b](https://github.com/0xfe/vexflow/commit/8b93c792b8be90a3f7f010dab2aa3748cd8cab6b) Changes for code review

[b8807ce785f069e4d67518a8fd4c4773e4f125ce](https://github.com/0xfe/vexflow/commit/b8807ce785f069e4d67518a8fd4c4773e4f125ce) Move stacked logic to correct place

[cc2ee1967ee3853ebd4dab34edb59a3ddca29358](https://github.com/0xfe/vexflow/commit/cc2ee1967ee3853ebd4dab34edb59a3ddca29358) kerning tweak

[5069c4c581551128bbc070c36d9060d14bf3b4c2](https://github.com/0xfe/vexflow/commit/5069c4c581551128bbc070c36d9060d14bf3b4c2) Simple kerning

[284dd67a3565869562bef0697ff0980d7dc3c25c](https://github.com/0xfe/vexflow/commit/284dd67a3565869562bef0697ff0980d7dc3c25c) chord symbol contribution

[f7197ee18fa3a5ee02b9fbb5cfbf1272dd788fba](https://github.com/0xfe/vexflow/commit/f7197ee18fa3a5ee02b9fbb5cfbf1272dd788fba) Merge pull request #789 from h-sug1no/fix-easyscore-dots3

[252050a09b2010733eb6899c68fa1cb0a0e227fd](https://github.com/0xfe/vexflow/commit/252050a09b2010733eb6899c68fa1cb0a0e227fd) drawDotsTest: remove setMode(VF.Voice.Mode.SOFT).

[5a58d2bb77b5a31fe1eb5ac74e95425b80d76f1f](https://github.com/0xfe/vexflow/commit/5a58d2bb77b5a31fe1eb5ac74e95425b80d76f1f) {WIP}: fix easyScore DOTS.

[58c16a068f2236aa8cbe3e3cc464d9823fd437c9](https://github.com/0xfe/vexflow/commit/58c16a068f2236aa8cbe3e3cc464d9823fd437c9) {WIP}: add VFT.EasyScore.drawDotsTest(Temporarily with Voice.Mode.SOFT).

[bcf9e7c8386a73c143e714e72bcf66641fdc0f2a](https://github.com/0xfe/vexflow/commit/bcf9e7c8386a73c143e714e72bcf66641fdc0f2a) Merge pull request #785 from jeroenlammerts/master

[05cec53e10fd2c3b751b6d12cdc36f8e0410e033](https://github.com/0xfe/vexflow/commit/05cec53e10fd2c3b751b6d12cdc36f8e0410e033) Merge pull request #784 from cmigliorini/bugfix/auto-beam

[e4ad00bfd2d7abb393c0719eec54945b05cd8515](https://github.com/0xfe/vexflow/commit/e4ad00bfd2d7abb393c0719eec54945b05cd8515) Merge pull request #786 from AaronDavidNewman/master

[c649f207b16ea0166f4eec854bfbb19204cf2535](https://github.com/0xfe/vexflow/commit/c649f207b16ea0166f4eec854bfbb19204cf2535) Merge note_struct options for GraceNote

[e0f86adb788088ad479ab43dc151c6b4f2168f90](https://github.com/0xfe/vexflow/commit/e0f86adb788088ad479ab43dc151c6b4f2168f90) test multiple, irregular groups, with overflow

[253698ea503a684e019903ff7da0d9a7036d3565](https://github.com/0xfe/vexflow/commit/253698ea503a684e019903ff7da0d9a7036d3565) fix autobeam with irregular groups, and when group overflows

[79f10c0088e47db5a27a1416376ab49993850898](https://github.com/0xfe/vexflow/commit/79f10c0088e47db5a27a1416376ab49993850898) specify time signature for More Automatic Beaming

[64781c2f8c3cfb23ff4196ed54f752a627053d65](https://github.com/0xfe/vexflow/commit/64781c2f8c3cfb23ff4196ed54f752a627053d65) coding style tweak

[7fa3546061cb504742e196f6c3e61b78c192db06](https://github.com/0xfe/vexflow/commit/7fa3546061cb504742e196f6c3e61b78c192db06) Merge https://github.com/0xfe/vexflow

[511c7b3cbf2c5e563c0e2a73147272ab4069956e](https://github.com/0xfe/vexflow/commit/511c7b3cbf2c5e563c0e2a73147272ab4069956e) Merge pull request #787 from Andrew13648/master

[23d3ee0be2c0e45664ef10aa2bd4073f9c927653](https://github.com/0xfe/vexflow/commit/23d3ee0be2c0e45664ef10aa2bd4073f9c927653) added support for accent articulations in easyscore

[107a7ba8e885d259e24b1866089f5f977bae0635](https://github.com/0xfe/vexflow/commit/107a7ba8e885d259e24b1866089f5f977bae0635) Add chord symbol glyphs to vexflow fonts

[93bacea2484bee90b36e7fca5123ab7b7080a007](https://github.com/0xfe/vexflow/commit/93bacea2484bee90b36e7fca5123ab7b7080a007) add dotted autobeam test

[f4753d368df84627464bfa32c5af83c1bce0b175](https://github.com/0xfe/vexflow/commit/f4753d368df84627464bfa32c5af83c1bce0b175) Minor cleanup.

[00ec15c67ff333ea49f4d3defbd9e22374c03684](https://github.com/0xfe/vexflow/commit/00ec15c67ff333ea49f4d3defbd9e22374c03684) Committing release binaries for new version: 3.0.9[
](https://github.com/0xfe/vexflow/commit/)(https