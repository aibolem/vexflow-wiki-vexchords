(This site is currently in edit mode).

The main purpose of this is to describe how to use SVG, but without the deprecated RAPHAEL library. 
The second purpose is to give an overview of how to set up the three options

* CANVAS 
* RAPHAEL
* SVG

On the side, implementation in a Wordpress-like website environment is mentioned.

###1. CANVAS:###

Canvas is the easiest to set up

Step 1. Find a place in your website where you can put html code into. In an old html-based site, this is just something like the index.html, in a wordpress site this might be a blog post with a block for plain html code. Maybe your theme offers such a code block. In your html code of the website, create a `<canvas>` element with width and height and give it an id like id="myCanvas".

Step 2. In your javascript vexflow code do   
``
var renderer = new Vex.Flow.Renderer(yourCanvasElement_ID, Vex.Flow.Renderer.Backends.CANVAS);
``

###2. RAPHAEL###

RAPHAEL is deprecated, best use SVG instead. In case you want to use RAPHAEL:

Step 1. In your html code of the website, create a   
        ``<div>``   
element with width and height and give it an id like   
        ``id="myRaphaelCanvas"``

Step 2. In your javascript vexflow code do   
        ``var renderer = new Vex.Flow.Renderer(yourRaphaelCanvasElement_ID, Vex.Flow.Renderer.Backends.RAPHAEL);``  

Step 3. Download and include the raphael-min.js javascript library to be loaded in your source code the same way you do it with vexflow-min.js

###3. SVG###

This is the new way to use SVG without RAPHAEL

Step 1. In your html code of the website, create a   
        ``<svg>``   
element with width and height and give it an id like   
        ``id="mySVGCanvas"``.

Step 2. Within the <svg> element, specify the argument   
        ``viewbox = "0 0 width height"``  
and set it to the same width and height as specified in your ``<svg>`` element. I had to familiarize with how SVG coordinate systems work, with viewbox, viewport and preserveAspectRatio properties to see the output.

Step 3. In your javascript vexflow code do  
``var renderer = new Vex.Flow.Renderer(yourSVGElement_ID, Vex.Flow.Renderer.Backends.SVG);`` 

No additional libraries are required.