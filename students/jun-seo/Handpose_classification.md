# 가위바위보
---
- `index.html`
```html
<!DOCTYPE html>
<html>
  <head>
    <title>ml5.js 연습</title>
    <meta charset="utf-8">
    <script src="https://cdn.jsdelivr.net/npm/p5@1/lib/p5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/p5@1/lib/addons/p5.sound.min.js"></script>
    <script src="https://unpkg.com/ml5@latest/dist/ml5.min.js"></script>
    <script src="https://cdn.jsdelivr.net/gh/IDMNYU/p5.js-speech@0.0.3/lib/p5.speech.js"></script>
  </head>

  <body>
    <h1>Handpose prediction with Handpose and ml5.neuralNetwork</h1>
    <script src="sketch.js"></script>
  </body>
</html>
```

- `sketch.js`(custom train)
```js
let video;
let handpose;
let landmark;
let annotation;
let textbox;
let button1;
let button2;

let brain;  // ml5.neuralNetwork for custom training

let state = 'waiting';
let targetLabel;

function setup() {
  createCanvas(640, 480);
  video = createCapture(VIDEO);
  video.hide();

  textbox = createInput('');
  textbox.position(10,575);
  textbox.size(100);

  button1 = createButton('train');
  button1.position(125,575);
  //button1.mousePressed().;
  
  button2 = createButton('save');
  button2.position(175,575);
  button2.mousePressed(dataSaving);

  let options = {
    inputs: 34,  // 17 points (x,y)
    outputs: 4,
    task: 'classification',
    debug: true
  }

  brain = ml5.neuralNetwork(options);

  let horizontal = {
    flipHorizontal: true
  }
  handpose = ml5.handpose(video, horizontal, modelLoaded);
  
  handpose.on('hand', gotPoses);
}

function modelLoaded() {
  console.log('Handpose is ready');
}

function btPressed() {
  console.log(textbox.value());
  setTimeout(function() {
    console.log('collecting');
    state = 'collecting';
    setTimeout(function() {
      console.log('not collecting');
      state = 'waiting';
    }, 10000);  // stop after 10 seconds later 
  }, 10000);  // 10 seconds after a key is pressed
}

function gotPoses(poses){
  console.log(poses);
  if (poses.length > 0) {
    landmark = poses[0].landmarks;
    annotation = poses[0].annotations;
  }

  for (let i = 0; i < landmark.length; i++) {
    let x = landmark[i][0];
    let y = landmark[i][1];
    fill(255, 0, 0);
    noStroke();
    circle(x, y, 10);
  }

  // lines 0
  let wrist_x = annotation.palmBase[0][0];
  let wrist_y = annotation.palmBase[0][1];
  fill(0);  // black
  noStroke();
  circle(wrist_x, wrist_y, 10);

  let thumb_cmc_x = annotation.thumb[0][0];
  let thumb_cmc_y = annotation.thumb[0][1];
  
  let indexFinger_mcp_x = annotation.indexFinger[0][0];
  let indexFinger_mcp_y = annotation.indexFinger[0][1];

  let middleFinger_mcp_x= annotation.middleFinger[0][0];
  let middleFinger_mcp_y = annotation.middleFinger[0][1];
  
  let ringFinger_mcp_x = annotation.ringFinger[0][0];
  let ringFinger_mcp_y = annotation.ringFinger[0][1];
  
  let pinky_mcp_x = annotation.pinky[0][0];
  let pinky_mcp_y = annotation.pinky[0][1];
  
  fill(255);  // white
  noStroke();
  circle(thumb_cmc_x, thumb_cmc_y, 10);

  strokeWeight(2);
  stroke(0, 255, 0);  // green
  line(wrist_x, wrist_y, thumb_cmc_x, thumb_cmc_y);
  line(wrist_x, wrist_y, indexFinger_mcp_x, indexFinger_mcp_y);
  line(wrist_x, wrist_y, middleFinger_mcp_x, middleFinger_mcp_y);
  line(wrist_x, wrist_y, ringFinger_mcp_x, ringFinger_mcp_y);
  line(wrist_x, wrist_y, pinky_mcp_x, pinky_mcp_y);
  line(indexFinger_mcp_x, indexFinger_mcp_y, middleFinger_mcp_x, middleFinger_mcp_y);
  line(middleFinger_mcp_x, middleFinger_mcp_y, ringFinger_mcp_x, ringFinger_mcp_y,);
  line(ringFinger_mcp_x, ringFinger_mcp_y, pinky_mcp_x, pinky_mcp_y);
  
  //thumb
  for (let i = 0; i < 3; i++) {
      let a = annotation.thumb[i][0];
      let b = annotation.thumb[i][1];
      let c = annotation.thumb[i+1][0];
      let d = annotation.thumb[i+1][1];
      strokeWeight(2);
      stroke(0,255,0);
      line(a,b,c,d);
  }
  
  //indexFinger
  for (let i = 0; i < 3; i++) {
    let a = annotation.indexFinger[i][0];
    let b = annotation.indexFinger[i][1];
    let c = annotation.indexFinger[i+1][0];
    let d = annotation.indexFinger[i+1][1];
    strokeWeight(2);
    stroke(0,255,0);
    line(a,b,c,d);
  }

  //middleFinger
  for (let i = 0; i < 3; i++) {
    let a = annotation.middleFinger[i][0];
    let b = annotation.middleFinger[i][1];
    let c = annotation.middleFinger[i+1][0];
    let d = annotation.middleFinger[i+1][1];
    strokeWeight(2);
    stroke(0,255,0);
    line(a,b,c,d);
  }

  //ringFinger
  for (let i = 0; i < 3; i++) {
    let a = annotation.ringFinger[i][0];
    let b = annotation.ringFinger[i][1];
    let c = annotation.ringFinger[i+1][0];
    let d = annotation.ringFinger[i+1][1];
    strokeWeight(2);
    stroke(0,255,0);
    line(a,b,c,d);
  }

  //pinky
  for (let i = 0; i < 3; i++) {
    let a = annotation.pinky[i][0];
    let b = annotation.pinky[i][1];
    let c = annotation.pinky[i+1][0];
    let d = annotation.pinky[i+1][1];
    strokeWeight(2);
    stroke(0,255,0);
    line(a,b,c,d);
  }
}

function dataSaving(){
  brain.saveData('sign_language');
  brain.save();
}

function draw() {
  push();
  // flip image's left and right
  translate(video.width, 0);
  scale(-1, 1);
  image(video, 0, 0);
  pop();
}
```
