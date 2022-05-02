# 소스코드
``` java script
var s;
var scl = 20;
var food;
playfield = 600;

function setup() {
  createCanvas(playfield, 640);
  background(51);
  s = new Snake();
  frameRate (15);
  pickLocation();
  noStroke();
}

function draw() {
  background('#795548');
  scoreboard();
  if (s.eat(food)) {
    pickLocation();
  }
  s.death();
  s.update();
  s.show();

  fill ('#FFEB3B');
  star(food.x+10,food.y+10, 10, 5,5);
    
}

// 별 모양 추가


function star(x, y, radius1, radius2, npoints) {
  let angle = TWO_PI / npoints;
  let halfAngle = angle / 2.0;
  beginShape();
  for (let a = 0; a < TWO_PI; a += angle) {
    let sx = x + cos(a) * radius2;
    let sy = y + sin(a) * radius2;
    vertex(sx, sy);
    sx = x + cos(a + halfAngle) * radius1;
    sy = y + sin(a + halfAngle) * radius1;
    vertex(sx, sy);
  }
  endShape(CLOSE);
}
// 음식이 나타날 위치

function pickLocation() {
  var cols = floor(playfield/scl);
  var rows = floor(playfield/scl);
  food = createVector(floor(random(cols)), floor(random(rows)));
  food.mult(scl);

  // 음식이 꼬리와 겹쳐서 생성되는지 확인

  for (var i = 0; i < s.tail.length; i++) {
    var pos = s.tail[i];
    var d = dist(food.x, food.y, pos.x, pos.y);
    if (d < 1) {
      pickLocation();
    }
  }
}

// 점수판

function scoreboard() {
  fill(0);
  rect(0, 600, 600, 40);
  fill(255);
  textFont("Georgia");
  textSize(18);
  text("Score: ", 10, 625);
  text("Highscore: ", 450, 625)
  text(s.score, 70, 625);
  text(s.highscore, 540, 625)
}

// 컨트롤 기능

function keyPressed() {
  if (keyCode === UP_ARROW){
      s.dir(0, -1);
  }else if (keyCode === DOWN_ARROW) {
      s.dir(0, 1);
  }else if (keyCode === RIGHT_ARROW) {
      s.dir (1, 0);
  }else if (keyCode === LEFT_ARROW) {
      s.dir (-1, 0);
  }
}

// 뱀 만들기

function Snake() {
  this.x =0;
  this.y =0;
  this.xspeed = 1;
  this.yspeed = 0;
  this.total = 0;
  this.tail = [];
  this.score = 1;
  this.highscore = 1;

// 이동, 이동방향

  this.dir = function(x,y) {
    this.xspeed = x;
    this.yspeed = y;
  }

// 음식을 먹으면 점수가 오르고 꼬리가 1개 더 생김

  this.eat = function(pos) {
    var d = dist(this.x, this.y, pos.x, pos.y);
    if (d < 1) {
      this.total++;
      this.score++;
      text(this.score, 70, 625);
      if (this.score > this.highscore) {
        this.highscore = this.score;
      }
      text(this.highscore, 540, 625);
      return true;
    } else {
      return false;
    }
  }

// 머리가 꼬리에 닿을 때 사망

  this.death = function() {
    for (var i = 0; i < this.tail.length; i++) {
      var pos = this.tail[i];
      var d = dist(this.x, this.y, pos.x, pos.y);
      if (d < 1) {
        this.total = 0;
        this.score = 0;
        this.tail = [];
      }
    }
  }

// 꼬리와 위치 업데이트

  this.update = function(){
    if (this.total === this.tail.length) {
      for (var i = 0; i < this.tail.length-1; i++) {
        this.tail[i] = this.tail[i+1];
    }

    }
    this.tail[this.total-1] = createVector(this.x, this.y);

    this.x = this.x + this.xspeed*scl;
    this.y = this.y + this.yspeed*scl;

    this.x = constrain(this.x, 0, playfield-scl);
    this.y = constrain(this.y, 0, playfield-scl);


  }
  
// 머리와 꼬리를 화면에 보여줌

  this.show = function(){
    fill('#4CAF50');
    for (var i = 0; i < this.tail.length; i++) {
        ellipse(this.tail[i].x+10, this.tail[i].y+10, scl, scl);
    }

    ellipse(this.x+10, this.y+10, scl, scl);
  }
}
```
## 실행결과
![1](img/snakeTeam2.gif)

## 변형 내용
* 프레임레이트를 약간 올려서 이동속도를 조금 올려봤습니다.
* 먹이의 모양을 원이 아닌 별 모양으로 바꿔봤습니다.
* 뱀의 모양을 사각형이 아닌 원으로 바꿔봤습니다.
* 배경과 뱀의 색깔을 바꿔봤습니다.
* 스코어 보드에서 최고기록을 달성했을 때 문구가 출력되게 했습니다.

