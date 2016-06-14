(This site is currently in edit mode).

The main purpose of this page is to describe in section 3. how to use SVG, but without the deprecated RAPHAEL library. 
The second purpose is to give you an overview of how you can set up these three options (choose only one)

* CANVAS 
* RAPHAEL
* SVG

On the side, implementation in a Wordpress-like website environment is mentioned.

###1. CANVAS:###

Canvas is the easiest to set up

Step 1. Find a place in your website where you can put html code into. In an old html-based site, this is just something like the index.html, in a wordpress site this might be a blog post with a block for plain html code. Maybe your theme offers such a code block. In your html code of the website, create a ``<canvas>`` element with width and height and give it an id like ``id="myCanvas"``.

    <canvas id="myCanvas" width="500px" height="300px">

Step 2. In your javascript vexflow code do   
     
     var renderer = new Vex.Flow.Renderer(yourCanvasElement_ID,Vex.Flow.Renderer.Backends.CANVAS);     


###2. RAPHAEL###

RAPHAEL is deprecated, best use SVG instead. In case you want to use RAPHAEL:

Step 1. In your html code of the website, create a ``<div>`` element with width and height and give it an id like   
        ``id="myRaphaelCanvas"``.

    <div id="myRaphaelCanvas" width="500px" height="300px">

Step 2. In your javascript vexflow code do   
        
    var renderer = new Vex.Flow.Renderer(yourRaphaelCanvasElement_ID, Vex.Flow.Renderer.Backends.RAPHAEL); 

Step 3. Download and include the raphael-min.js javascript library to be loaded in your source code the same way you do it with vexflow-min.js

###3. SVG###

This is the new way to use SVG without RAPHAEL

Step 1. In your html code of the website, create a ``<svg>`` element with width and height and give it an id like   
        ``id="mySVGCanvas"``.

    <svg id="mySVGCanvas" width="500px" height="300px">

Step 2. Within the ``<svg>`` element, specify the argument ``viewbox = "0 0 width height"`` and set it to the same width and height as specified in your ``<svg>`` element. Like so:

    <svg id="mySVGCanvas" width="500px" height="300px" viewbox = "0 0 500 300">

If you need more tweaking for your SVG canvas, you should familiarize with how an SVG coordinate system works, with the 3 important properties

* viewbox
* viewport 
* preserveAspectRatio 

so you can actually see the output in the virtual SVG world. If unfamiliar, best look at a SVG tutorial (google search) and read about those properties.

Step 3. In your javascript vexflow code do
 
    var renderer = new Vex.Flow.Renderer(yourSVGElement_ID, Vex.Flow.Renderer.Backends.SVG);

No additional libraries are required.