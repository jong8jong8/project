# [p5.js](https://p5js.org/)


- [생활코딩 - p5.js](https://opentutorials.org/course/4659)

- `index.html`

```html
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.5.0/lib/p5.js"></script>
  </head>
  <body>
    <script src="sketch.js"></script>
  </body>
</html>
```


- `sketch.js`

```javascript
function setup() {
  createCanvas(400, 400);
}

function draw() {
  if (mouseIsPressed) {
    fill(0);
  } else {
    fill(255);
  }
  ellipse(mouseX, mouseY, 80, 80);
}
```
