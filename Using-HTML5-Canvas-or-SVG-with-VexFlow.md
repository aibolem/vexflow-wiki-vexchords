VexFlow abstracts away the rendering backend, and works on both HTML5 Canvas and SVG. There's also preliminary support for NodeJS backends, allowing you to render to PDF (or bitmap images.)

### HTML5 Canvas

You can use the `Renderer.Backends.CANVAS` backend to generate notation on Canvas elements. To use it, create a `canvas` element in your HTML file as so:

    <canvas id="myCanvas" width="500" height="300"></canvas>

And configure your renderer as so:
     
    var renderer = new Vex.Flow.Renderer(document.getElementById("myCanvas"),
                                         Vex.Flow.Renderer.Backends.CANVAS);     

### SVG

You can render to SVG using the `Renderer.Backends.SVG` backend. VexFlow now has native support for SVG and does not require RaphaelJS. To use it, create an `svg` element in your HTML document:

    <svg id="mySVGCanvas" width="500" height="300" viewbox = "0 0 500 300"></svg>

Then initialize the renderer as so:

    var renderer = new Vex.Flow.Renderer(document.getElementById("mySVGCanvas"),
                                         Vex.Flow.Renderer.Backends.SVG);

You can tweak your SVG display using the properties `viewbox`, `viewport`, and `preserveAspectRatio`.

### Raphael

`RAPHAEL` is the old deprecated backend that Renders to SVG. You can still use it with old versions of VexFlow to render to older browsers (e.g., IE that uses VML.) You will also need to include the RaphaelJS library into your javascript.