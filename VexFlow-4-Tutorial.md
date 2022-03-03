Below, we demonstrate different ways to display a VexFlow score in your project.

# script tag

The quickest way is to add <script> tags into a static HTML page.

First, we add a <script> tag to include the VexFlow library.

```
<script src="https://cdn.jsdelivr.net/npm/vexflow/build/cjs/vexflow.js"></script>
```

...

## CDN

You can use any CDN that serves NPM packages. Our favorites are jsdelivr and unpkg. Choose the one that works best for you!

**jsdelivr**

- Minified: https://cdn.jsdelivr.net/npm/vexflow/build/cjs/vexflow.js
- Debug: https://cdn.jsdelivr.net/npm/vexflow/build/cjs/vexflow-debug.js

**unpkg**

- Minified: https://unpkg.com/vexflow/build/cjs/vexflow.js
- Debug: https://unpkg.com/vexflow/build/cjs/vexflow-debug.js


## Common JS vs ES Module

...

# Node.js

...

# TypeScript

If your TypeScript project uses a bundler such as webpack or esbuild, you will need to make sure that VexFlow can be imported. The easiest way is to use npm:

```sh
npm install vexflow
```

In your `app.ts`, you can directly import the classes you need. 

```typescript
import { Vex, Flow, Factory, Stave, EasyScore } from "vexflow";
```

To check that VexFlow is imported correctly, you can print out the build information.

```typescript
console.log(Vex.Flow.BUILD);
```

The output will look something like: 
```json
{
    "VERSION": "4.0.1",
    "ID": "efbdff60979ea561ff45bc4ab0b0a9dc12fde868",
    "DATE": "2022-02-28T01:06:16.478Z"
}
```

The VexFlow 4 library adds about 800 KiB to your app bundle. If you don't need all three music engraving fonts, you can import a different entry file that includes a single music font:

```
// Choose one of the import paths below to create a smaller bundle.
// Each path maps to a different entry file in the vexflow npm package.
import { Vex, Flow, Factory, Stave, EasyScore } from "vexflow/bravura";
import { Vex, Flow, Factory, Stave, EasyScore } from "vexflow/gonville";
import { Vex, Flow, Factory, Stave, EasyScore } from "vexflow/petaluma";
```

For example, the `vexflow/gonville` entry point adds about 450 KiB to your app bundle.

To get this to work in the current TypeScript (version 4.6 as of February 2022), you'll need to edit your tsconfig.json file to define what "vexflow/bravura" will resolve to.

```typescript
{
    "compilerOptions": {
        "baseUrl": "./",
        "paths": {
            // Choose one of the options below to customize the font that will be statically compiled into your entry bundle.
            "vexflow/bravura":  ["node_modules/vexflow/entry/vexflow-bravura.ts"],  // 486 KiB
            "vexflow/gonville": ["node_modules/vexflow/entry/vexflow-gonville.ts"], // 439 KiB
            "vexflow/petaluma": ["node_modules/vexflow/entry/vexflow-petaluma.ts"]  // 460 KiB
        },
    ...
}
```

A future version of TypeScript will not require you to edit your tsconfig.json. Instead, TypeScript will understand the `exports` field in [VexFlow's package.json](https://github.com/0xfe/vexflow/blob/master/package.json#L5-L25), and importing `"vexflow/petaluma"` will automatically include only the Petaluma music font.