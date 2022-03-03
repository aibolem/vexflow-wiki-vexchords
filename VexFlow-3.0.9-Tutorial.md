This page includes details for integrating with VexFlow 3.0.9, which was published in April 2020.

# <script> tag

Add the following <script> tag to your HTML page:

```html
<script src="https://unpkg.com/vexflow@3.0.9/releases/vexflow-min.js"></script>
```

Then on the same page, add another <script> tag with the following code:

```html
<script>
const f = new Vex.Flow.Factory({
  renderer: { elementId: 'output', width: 500, height: 200 },
});

const score = f.EasyScore();
const system = f.System();

system
  .addStave({
    voices: [
      score.voice(score.notes('C#5/q, B4, A4, G#4', { stem: 'up' })),
      score.voice(score.notes('C#4/h, C#4', { stem: 'down' })),
    ],
  })
  .addClef('treble')
  .addTimeSignature('4/4');

f.draw();
</script>
```



# npm install

If you would like to bundle VexFlow into your web project (e.g., with webpack), you can install VexFlow from npm:

```
npm install vexflow@3.0.9
```

Then, in your project (e.g., app.js), do the following:

```javascript
import Vex from 'vexflow';

const f = new Vex.Flow.Factory({
  renderer: { elementId: 'output', width: 500, height: 200 },
});

const score = f.EasyScore();
const system = f.System();

system
  .addStave({
    voices: [
      score.voice(score.notes('C#5/q, B4, A4, G#4', { stem: 'up' })),
      score.voice(score.notes('C#4/h, C#4', { stem: 'down' })),
    ],
  })
  .addClef('treble')
  .addTimeSignature('4/4');

f.draw();
```
