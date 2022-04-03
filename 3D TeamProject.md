# 컴퓨터 그래픽스 팀프로젝트
## 소스코드
``` java script
var cols, rows;
var scl = 35;
var w = 4000;
var h = 3500;
var flying = 0;
var terrain = [];
let Bslider;
let Xslider;
let TT,YY
let img;
function setup() {
  createCanvas(windowWidth,windowHeight, WEBGL);
  colorMode(RGB);
  
  Bslider = createSlider(0, 255, 60, 10);
  Bslider.position(10, 10);
  Bslider.style('width', '80px');
  Xslider = createSlider(-500, 500, 60, 3);
  Xslider.position(10, 20);
  Xslider.style('width', '80px');
  Yslider = createSlider(-400, 200, 100, 2);
  Yslider.position(10, 30);
  Yslider.style('width', '80px');
 
  TT=windowWidth/2;
  YY=windowHeight;
  {
    
  cols = w / scl;
  rows = h / scl;
  for (var x = 0; x < cols; x++) {
    terrain[x] = [];
    for (var y = 0; y < rows; y++) {
      terrain[x][y] = 0; //specify a default value for now
    }
  }
}
  img=loadImage('https://upload.wikimedia.org/wikipedia/commons/thumb/7/7a/Italian_traffic_signs_-_SOS.svg/200px-Italian_traffic_signs_-_SOS.svg.png');

}
function draw() {
  flying -= 0.04;
  var yoff = flying;
  for (var y = 0; y < rows; y++) {
    var xoff = 0;
    for (var x = 0; x < cols; x++) {
      terrain[x][y] = map(noise(xoff, yoff), 0, 1, -80, 70);
      xoff += 0.15;
    }
    yoff += 0.15;
  }
  noStroke();
  let val = Bslider.value();
  background(140-val, 140+val, 140+val);
  
  translate(0, 150);
  rotateX(PI / 3);
  fill(200, 200, 200, 150);
  translate(-w / 2, -h / 2);
  for (var y = 0; y < rows -20; y++) {
    beginShape(TRIANGLE_STRIP);
    for (var x = 0; x < cols; x++) {
      let v=terrain[x][y];
      v=map(v, -200, 70, 0, 270);
      fill(90, 50-v+val, v-80+val,200);
      vertex(x * scl, y * scl, terrain[x][y]);
      vertex(x * scl, (y + 1) * scl, terrain[x][y + 1]);
    }
    endShape();
      //frameRate(30);
  }
 X = Xslider.value();
  Y = Yslider.value();
  
  translate(TT, YY);
  rotate(PI/4);
  
  push();
 fill(255,40,80);
   ambientLight(250);
  emissiveMaterial(250, 230, 60,200);
 // rotateZ(frameCount * 0.01);
  rotateX(frameCount * 0.005);
  rotateZ(frameCount * 0.015);
  rotateY(frameCount * 0.005);
  texture(img);
  box(200);
  TT = TT + 10;
  YY = YY - 1;
  if(TT > windowWidth*4){
    TT = windowWidth/2
    YY = windowHeight;
  }
  
  if (YY < 0) {
    YY = height;
  }
  pop();
  camera(X,Y,800,50,100,100);
}
```
![1](/img/3D-teamProject.gif)
## 변경점
* 바다를 컨셉으로 해서 날이 밝고 어두움에 따라 하늘과 바다의 색깔을 슬라이드를 이용해서 바꿔 봤습니다.
* 바다에 SOS 문구가 적혀있는 박스를 만들어서 왼쪽 끝에서 오른쪽 끝까지 떠다니게 만들었습니다.
* 슬라이드를 이용해서 좌우, 위아래의 시야를 돌릴 수 있도록 만들었습니다.
## 소감
