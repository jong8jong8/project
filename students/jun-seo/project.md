# 임준서

- `sketch.js`

```javascript
let video;
let handpose;
let landmark;
let annotation;

function setup() {
  createCanvas(640, 480);
  video = createCapture(VIDEO);
  video.hide();
  let options = {
    flipHorizontal: true
  }
  handpose = ml5.handpose(video, options, modelLoaded);
  
  handpose.on('hand', gotPoses);
}

function modelLoaded() {
  console.log('Handpose is ready');
}

function gotPoses(poses){
  console.log(poses);
  if (poses.length > 0) {
    landmark = poses[0].landmarks;
    annotation = poses[0].annotations;
    for (let i = 0; i < landmark.length; i++) {
      let x = landmark[i][0];
      let y = landmark[i][1];
      fill(0, 255, 0);
      noStroke();
      circle(x, y, 10);
    }

    // lines 0
    let wrist_x = annotation.palmBase[0][0];
    let wrist_y = annotation.palmBase[0][1];
    fill(255, 0, 0);  // red
    noStroke();
    circle(wrist_x, wrist_y, 10);

    let thumb_cmc_x = annotation.thumb[0][0];
    let thumb_cmc_y = annotation.thumb[0][1];
    fill(0, 0, 255);  // blue
    noStroke();
    circle(thumb_cmc_x, thumb_cmc_y, 10);

    strokeWeight(2);
    stroke(0, 255, 0);  // green
    line(wrist_x, wrist_y, thumb_cmc_x, thumb_cmc_y);
    //Thumb
    for (let i = 1; i < 3; i++) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //Index
    for (let i = 5; i < 8; i++) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //Middle
    for (let i = 9; i < 12; i++) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //Ring
    for (let i = 13; i < 16; i++) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //pinky
    for (let i = 17; i < 20; i++) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //MCP
    for (let i = 5; i < 17; i+=4) {
        let a = landmark[i][0];
        let b = landmark[i][1];
        strokeWeight(2);
        stroke(255);
        line(a.annotation.x, a.annotation.y, b.annotation.x, b.annotation.y);
    }
    //5:0
    line();

    //17:0
    line();
  }
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
