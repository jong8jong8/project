# 지한서 


- 외않되
```
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

    for (let k = 0; k < 3; k++) {
      

      let x1 = annotation.thumb[k][0];
      let y1 = annotation.thumb[k][1];
      if (k = 1) {
        strokeWeight(2);
        stroke(255, 255, 255);
        line(thumb_cmc_x, thumb_cmc_y, x1, y1);
      }
      let x2 = annotation.thumb[k+1][0];
      let y2 = annotation.thumb[k+1][1];
      strokeWeight(2);
      stroke(255, 255, 255);
      line(x1, y1, x2, y2);
      }
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
