# [p5.js](https://p5js.org/)


- [생활코딩 - p5.js](https://opentutorials.org/course/4659)



## Basic Template

- `index.html`

```html
<!DOCTYPE html>
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
function setup() {  // only once
  createCanvas(400, 400);
}

function draw() {  // infinite loop
  if (mouseIsPressed) {
    fill(0);
  } else {
    fill(255);
  }
  ellipse(mouseX, mouseY, 80, 80);
}
```


## p5.js Excersice
- [Image Classification](./p5ex/image_classification.md)


