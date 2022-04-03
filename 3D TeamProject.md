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
### 이재경
```
팀 과제를 한다는 어떻게 시작해서 해결을 해야할지 막막했습니다.
수업시간에도 자세히 다루지 않고 빠르게 넘어간 느낌이 있어 팀프로젝트를 시작하기 전에 걱정이 많았습니다.
팀원들과 모인 후 서로의 코드들을 모아서 가장 좋은 코드를 만들고 서로 모르는 내용들을 설명해주고 하다보니
p5js와 더 가까워지고 더 배우는 시간을 가졌습니다.
camera를 사용하는데 약간의 힘든 점이 있었지만
수업시간에 배운 내용과 팀원들과 함께 하니 처음 배울대보다 확실하게 이해를 한 것 같습니다.
camera외에도 material, slider, 등을 사용해보며 아직 익숙하지 않은 명령어들을 사용할 수 있게 되었습니다.
다음에도 팀프로젝트를 하면 더욱 자신있게 할 수 있을것같습니다. 감사합니다.
```

### 박태현
```
이번 과제를 통하여 팀원들과 협동하며 terrain 생성을 하게 되었습니다. 저희 팀은 바다를 연출해 보고싶어
light, material을 통해 도형에 입체감을 더해봤고,
슬라이드 기능을 이용해 배경색,바다색,카메라 시점변경등을 활용해보니, 
더 많이 배워 여러 기능들을 더 써보고 싶다는 생각도 들었습니다.
제가 처음으로 하는 팀 프로젝트라 부족하고 어려운 부분이 많았지만 협동을 통해
잘 이겨낸 것 같습니다. 이번 기회로 많이 배운 것 같고 더 발전하는 사람이 되고 싶습니다. 감사합니다.
```

### 송태선
```
이번에 처음 팀과제를 하게 되었는데 지식도 아는게 조금밖에 없고 
막막하고 어려워서 힘들었는데 팀원들이 열심히 도와주어서 조금은 알게 되었고,
팀과제에서 나는 많은 기여가 되지 못해서 팀원들한테 미안한 마음도 들었고 팀원들 한테 고마마음도 들었다.
camera, meterial, slider 등등 생전 첨보는 생소한 단어들을 보고 당황하게 되었는데 팀원들과 함꼐하니 조금은 알게 되어서 뿌듯했고,
앞으로는 이런 팀과제가 있으면 이번에보다 팀에 많은 기여가 되고 싶다.
```

### 추승범
```
3D 지형 팀프로젝트를 하면서 아직 배울 점이 많다고 느꼈습니다.
만들어 보고 싶은 움직임이나 내용들이 잘 만들어지지 않아서 팀원들 모두가 답답함을 느꼈습니다.
하지만 끊임없이 의견을 주고받으며 원하는 결과를 만들어냈고 팀프로젝트를 성공시켰습니다.
어려운 부분도 많았지만 완성을 시키며 다방면으로 코딩에 대한 이해도가 늘어난 것 같습니다.
협업을 통한 코딩 경험을 쌓아서 기분이 좋습니다.
앞으로 더 잘하기 위해 컴퓨터 그래픽스 수업 더 열심히 듣고 공부하겠습니다.
감사합니다.
```
