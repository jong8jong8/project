# Image Classification (이미지 분류)

- [ImageNet](https://image-net.org/index.php)
- [MobileNet](https://github.com/tensorflow/tfjs-models/tree/master/mobilenet) - pre-trained on ImageNet (1000 classes)


### Basic Template

- `index.html`

```html
<html>

<head>
  <meta charset="UTF-8">
  <title>Image classification using MobileNet and p5.js</title>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.5.0/p5.min.js"></script>
  <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
</head>

<body>
  <h1>Image classification using MobileNet and p5.js</h1>
  <script src="sketch.js"></script>
</body>

</html>
```

- `sketch.js`

```javascript
// Initialize the Image Classifier method with MobileNet. A callback needs to be passed.
let classifier;

// A variable to hold the image we want to classify
let img;

function preload() {
  classifier = ml5.imageClassifier('MobileNet');
  img = loadImage('images/bird.jpeg');
}

function setup() {
  createCanvas(400, 400);
  classifier.classify(img, gotResult);
  image(img, 0, 0);
}

// A function to run when we get any errors and the results
function gotResult(error, results) {
  // Display error in the console
  if (error) {
    console.error(error);
  } else {
    // The results are in an array ordered by confidence.
    console.log(results);
    createDiv(`Label: ${results[0].label}`);
    createDiv(`Confidence: ${nf(results[0].confidence, 0, 2)}`);
  }
}
```
