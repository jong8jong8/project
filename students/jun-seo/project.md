# 임준서
- [한글 지문자]([https://www.youtube.com/watch?v=aircAruvnKk](https://namu.wiki/w/%EC%88%98%EC%96%B4#s-2])
- [수어 모델]([https://en.wikipedia.org/wiki/Piano_key_frequencies](https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=103)https://aihub.or.kr/aihubdata/data/view.do?currMenu=115&topMenu=100&aihubDataSe=realm&dataSetSn=103])
---
-sketch.js
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
