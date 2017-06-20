VexFlow abstracts away the rendering backend, and works on both SVG and HTML5 Canvas. Because of the higher resolution and ability to work with rendered elements as objects, SVG is the recommended choice. There's also preliminary support for NodeJS backends, allowing you to render to PDF (or bitmap images.)

The following boilerplate will get you started, for a deep dive into what it means, see [Understanding Renderer and Context](https://github.com/0xfe/vexflow/wiki/Understanding-Renderer-&-Context).

### SVG

You can render to SVG using the `Renderer.Backends.SVG` backend. VexFlow now has native support for SVG and does not require external libraries like RaphaelJS. To use it, create a `div` element in your HTML document:
``` html
    <div id="mySVGDiv"><!-- VexFlow will create an SVG here --></div>
```
Then initialize the renderer as so:
``` JavaScript
    var div = document.getElementById('mySVGDiv');
    var renderer = new Vex.Flow.Renderer(div, Vex.Flow.Renderer.Backends.SVG);
    renderer.resize(500, 200); // set the width, height & viewbox properties of your svg
```
You can tweak your SVG display using the properties `viewbox`, `viewport`, and `preserveAspectRatio`.

### HTML5 Canvas

You can use the `Renderer.Backends.CANVAS` backend to generate notation on Canvas elements. To use it, create a `canvas` element in your HTML file as so:

``` html
    <canvas id="myCanvas" width="500" height="300"></canvas>
```
And configure your renderer as so:
``` JavaScript
    var canvas = document.getElementById("myCanvas");
    var renderer = new Vex.Flow.Renderer(canvas, Vex.Flow.Renderer.Backends.CANVAS);     
```

### Raphael

`RAPHAEL` is the old deprecated backend that Renders to SVG. You can still use it with old versions of VexFlow to render to very old browsers (e.g., IE that uses VML.) But, you will also need to include the RaphaelJS library into your javascript.