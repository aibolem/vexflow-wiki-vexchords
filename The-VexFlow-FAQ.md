### Basics
#### What is VexFlow?

VexFlow is an open-source web-based music notation rendering API. It is written completely in JavaScript, and runs right in the browser. VexFlow supports HTML5 Canvas and SVG, and runs on all modern browsers.

#### What platforms does it run on?

VexFlow has been tested on Google Chrome, Firefox, Safari, Opera, and Internet Explorer 10+.

#### What features does it support?

VexFlow has support for standard music, guitar tablature, and percussion notation. While it is a goal to support the vast majority of western music notation, VexFlow also supports a few alternative elements, such as, microtonal notation.

To see a everything VexFlow can render, take a look at the [tests](http://www.vexflow.com/tests/index.html) (scroll down to see the images.)

#### How do I learn to use the VexFlow API?

The best place to start is the (VexFlow Tutorial)[http://www.vexflow.com/docs/tutorial.html]. Once you're comfortable with the basics of the API, start looking at the tests in `tests/*.js` for examples of how to use the various notational elements and tools.

#### Why is the API so complex?

VexFlow is in its third iteration, where each iteration was a complete overhaul. While the first two iterations were much simpler, it turns out that the scope of musical notation is huge and complex.

The desire to support complex musical notation while also providing a high degree of flexibility, steers the design of VexFlow.

Also note that VexFlow is a low-level rendering API. If all you want to do is display music on a page, take a look at higher level libraries such as [VexTab](http://vexflow.com/vextab/).

### Formatting

1. How do I create and align multiple voices?
2. How do I align multiple staves?
3. How can I pre-calculate the width of a voice?
4. What are all these `context` classes? (`ModifierContext`, `TickContext` etc.)

### API

1. Can VexFlow automatically generate beams?
2. How do I render slurs?
3. How can I align text to notation?
4. Can I color notes individually?



