# 지한서 


- 손 스켈레톤 이다.
```js
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
    stroke(255, 255, 255);  // white
    line(wrist_x, wrist_y, thumb_cmc_x, thumb_cmc_y);

    // thumb lines

    for (let j = 0; j < 3; j++) {
      

      let x1 = annotation.thumb[j][0];
      let y1 = annotation.thumb[j][1];

      let x2 = annotation.thumb[j+1][0];
      let y2 = annotation.thumb[j+1][1];
      strokeWeight(2);
      stroke(255, 255, 255);
      line(x1, y1, x2, y2);
      }

      // index finger lines

      for (let j = 0; j < 3; j++) {
        let x1 = annotation.indexFinger[j][0];
        let y1 = annotation.indexFinger[j][1]
        if (j == 0) {
          line(wrist_x, wrist_y, x1, y1);
        }
        let x2 = annotation.indexFinger[j+1][0];
        let y2 = annotation.indexFinger[j+1][1];
        line(x1, y1, x2, y2);
      }

      // middle finger lines
      for (let j = 0; j < 3; j++) {
        let x1 = annotation.middleFinger[j][0];
        let y1 = annotation.middleFinger[j][1];
        let x2 = annotation.middleFinger[j+1][0];
        let y2 = annotation.middleFinger[j+1][1];
        line(x1, y1, x2, y2);
      }

      // ring finger
      for (let j = 0; j < 3; j++) {
        let x1 = annotation.ringFinger[j][0];
        let y1 = annotation.ringFinger[j][1];
        let x2 = annotation.ringFinger[j+1][0];
        let y2 = annotation.ringFinger[j+1][1];
        line(x1, y1, x2, y2);
      }

      // pinky
      for (let j = 0; j < 3; j++) {
        let x1 = annotation.pinky[j][0];
        let y1 = annotation.pinky[j][1];
        let x2 = annotation.pinky[j+1][0];
        let y2 = annotation.pinky[j+1][1];
        line(x1, y1, x2, y2);
      }
      
      // others and stuff
      let index_finger_mcp_x = annotation.indexFinger[0][0];
      let index_finger_mcp_y = annotation.indexFinger[0][1];

      let middle_finger_mcp_x = annotation.middleFinger[0][0];
      let middle_finger_mcp_y = annotation.middleFinger[0][1];

      let ring_finger_mcp_x = annotation.ringFinger[0][0];
      let ring_finger_mcp_y = annotation.ringFinger[0][1];

      let pinky_mcp_x = annotation.pinky[0][0];
      let pinky_mcp_y = annotation.pinky[0][1];

      line(index_finger_mcp_x, index_finger_mcp_y, middle_finger_mcp_x, middle_finger_mcp_y);
      line(middle_finger_mcp_x, middle_finger_mcp_y, ring_finger_mcp_x, ring_finger_mcp_y);
      line(ring_finger_mcp_x, ring_finger_mcp_y, pinky_mcp_x, pinky_mcp_y);
      line(wrist_x, wrist_y, pinky_mcp_x, pinky_mcp_y);
      line(wrist_x, wrist_y, middle_finger_mcp_x, middle_finger_mcp_y);
      line(wrist_x, wrist_y, ring_finger_mcp_x, ring_finger_mcp_y);
      
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
