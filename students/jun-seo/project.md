# 임준서
- [한글 지문자](https://ko.wikipedia.org/wiki/%ED%95%9C%EA%B8%80_%EC%A7%80%EB%AC%B8%EC%9E%90)
- [k-nearest neighbors (KNN) algorithm](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm)

---
-`sketch.js`
```javascript
let video;
let poseNet;
let pose;
let skeleton;

let brain;  // ml5.neuralNetwork for custom training

let state = 'waiting';

let targetColor = [];
let textbox;

function setup() {
  createCanvas(640, 480);
  textbox = createInput('');
  video = createCapture(VIDEO);
  video.hide();
  poseNet = ml5.poseNet(video, modelLoaded);
  poseNet.on('pose', gotPoses);

  let options = {
    inputs: 63,  // 21 points (x,y,z)
    outputs: 38,  // 한글 자음 모음
    task: 'classification',
    debug: true
  }
  brain = ml5.neuralNetwork(options);
  // const modelDetails = {
  //   model: 'model/model.json',
  //   metadata: 'model/model_meta.json',
  //   weights: 'model/model.weights.bin'
  // }
  // brain.load(modelDetails, brainLoaded);
  // brain.loadData('mypose.json', dataReady);
}

function modelLoaded() {
  console.log('poseNet is ready');
}

// function brainLoaded() {
//   console.log('pose classification ready!');
// }

// function dataReady() {
//   brain.normalizeData();
//   brain.train({epochs: 100}, finished);
// }

// function finished() {
//   console.log('model trained');
//   brain.save();  // 3 files 
// }

function gotPoses(poses){
  // console.log(poses);
  if (poses.length > 0) {
    pose = poses[0].pose;
    skeleton = poses[0].skeleton;
    if (state == 'collecting') {
      let inputs = [];
      for (let i = 0; i < pose.keypoints.length; i++) {
        let x = pose.keypoints[i].position.x;
        let y = pose.keypoints[i].position.y;
        inputs.push(x);
        inputs.push(y);
      }
      brain.addData(inputs, targetColor);
    } 
  }
}

function delay(time) {
  return new Promise((resolve, reject) => {
    if (isNaN(time)) {
      reject(new Error('delay requires a valid number.'));
    } else {
      setTimeout(resolve, time);
    }
  });
}

async function keyPressed() {
  if (key == 's') {
    brain.saveData();
  } else if (key == 'd') {  // for data collection
    let r = rSlider.value();
    let g = gSlider.value();
    let b = bSlider.value();
    console.log(r, g, b);
    
    targetColor = [r, g, b];
    
    await delay(3000); // 3초 기다림 
    console.log('collecting');
    state = 'collecting';

    await delay(3000); // 3초 기다림 
    console.log('not collecting');
    state = 'waiting';
  }
}

function draw() {
  // flip image's left and right
  translate(video.width, 0);
  scale(-1, 1);
  image(video, 0, 0, video.width, video.height);

  if (pose) {
    for (let i = 0; i < pose.keypoints.length; i++) {
      let x = pose.keypoints[i].position.x;
      let y = pose.keypoints[i].position.y;
      fill(0);
      stroke(255);
      circle(x, y, 16);
    }
    for (let i = 0; i < skeleton.length; i++) {
        let a = skeleton[i][0];
        let b = skeleton[i][1];
        strokeWeight(2);
        stroke(0);
        line(a.position.x, a.position.y, b.position.x, b.position.y);
    }
  } 
}
```
-`sketch.js`(type2)
```javascript
llet video;
let handpose;
let landmark;
let annotation;
let textbox;
let button1;
let button2;

let brain;

let state = 'waiting';
let targetLabel;

function setup() {
  createCanvas(640, 480);
  textbox = createInput('');
  textbox.position(10,575);
  textbox.size(100);

  button1 = createButton('train');
  button1.position(125,575);
  //button1.mousePressed().;
  button2 = createButton('save');
  button2.position(175,575);
  button2.mousePressed(dataSaving);

  video = createCapture(VIDEO);
  video.hide();
  let options = {
    flipHorizontal: true,
    maxNumHands: 2,
    detectionConfidence: 0.8,
    scoreThreshold: 0.5
  }
  handpose = ml5.handpose(video, options, modelLoaded);
  handpose.on('hand', gotPoses);

  let nnOptions = {
    inputs: 63,  // 21 points (x,y,z)
    outputs: 30,  // 한글 자음 모음
    task: 'classification',
    debug: true
  }
  brain = ml5.neuralNetwork(nnOptions);
}

function modelLoaded() {
  console.log('Handpose is ready');
}

function gotPoses(poses){
  if (poses.length > 0) {
    landmark = poses[0].landmarks;
    annotation = poses[0].annotations;
    skeleton();
  }
}

function skeleton(){
  if (landmark.length > 0) {
    for (let i = 0; i < landmark.length; i++) {
      let x = landmark[i][0];
      let y = landmark[i][1];
      fill(255, 255, 255);
      noStroke();
      circle(x, y, 10);
    }
  }
  
    //lines 0
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

-`sketch.js` (train but no info)

```js
let video;
let handpose;
let landmark;
let annotation;
let textbox;
let trainBt;
let dataSavingBt;
let submitBt;
let key;
let p1;

let brain;

let state = 'waiting';
let targetLabel;

function setup() {
  createCanvas(640, 480);
  textbox = createInput('');
  textbox.position(10,575);
  textbox.size(100);
  
  submitBt = createButton('submit');
  submitBt.position(125,575);
  submitBt.mousePressed(bt);
  trainBt = createButton('train');
  trainBt.position(125,575);
  trainBt.mousePressed(buttonPressed);
  trainBt.hide();
  dataSavingBt = createButton('save');
  dataSavingBt.position(175,575);
  dataSavingBt.mousePressed(dataSaving);
  dataSavingBt.hide();

  video = createCapture(VIDEO);
  video.hide();
  let options = {
    flipHorizontal: true,
    maxNumHands: 1,
    detectionConfidence: 0.8,
    scoreThreshold: 0.5
  }
  handpose = ml5.handpose(video, options, modelLoaded);
  handpose.on('hand', gotPoses);

  let Settings = {
    inputs: 63,  // 21 points (x,y,z)
    outputs: 3,  // 한글 자음 모음
    task: 'classification',
    debug: true
  }
  brain = ml5.neuralNetwork(Settings);
}

function bt() {
submitBt.hide();
trainBt.show();
dataSavingBt.show();
textbox.hide();
p1 = createP(textbox.value());
p1.style('font-size','25px');
p1.position(175,575);
}

function modelLoaded() {
  console.log('Handpose is ready');
}

function gotPoses(poses){
  if (poses.length > 0) {
    landmark = poses[0].landmarks;
    annotation = poses[0].annotations;
    skeleton();
  }
}

function skeleton(){
  if (landmark.length > 0) {
    for (let i = 0; i < landmark.length; i++) {
      let x = landmark[i][0];
      let y = landmark[i][1];
      fill(255, 255, 255);
      noStroke();
      circle(x, y, 10);
    }
  }
  
    //lines 0
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

function buttonPressed() {
  targetLabel = key;
  console.log(targetLabel);
  setTimeout(function() {
    console.log('collecting');
    state = 'collecting';
    setTimeout(function() {
      console.log('not collecting');
      state = 'waiting';
    }, 5000);  // stop after 10 seconds later (prepare) 
  }, 10000);  // 10 seconds after a key is pressed (collect)
  p1.hide();
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
