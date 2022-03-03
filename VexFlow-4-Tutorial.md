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

```
npm install vexflow
```

