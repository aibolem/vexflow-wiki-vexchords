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

