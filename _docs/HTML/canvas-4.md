---
title: canvas - interaction
category: HTML
order: 4
---

## - interaction 움직임

```jsx
//예제 1) 사각형 누르는 것 감지하기
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");

ctx.fillRext(200, 200, 100, 100);

function clickHandler(e) {
  const x = e.layerX;
  const y = e.layerY;

  if(x > 200 &&
     x < 200 + 100 &&
     y > 200 &&
     y < 200 + 100>){

  }
}

canvas.addEventListener('click', clickHandler);

```

```jsx
//예제 2)
// - 랜덤으로 사각형 여러개가 가로로 지나가게 하기
// - 박스 클릭하면 panel로 띄우고 뒤에 박스들 멈추게 하기
...
// <script src="Box.js"></script>
// <script src="Panel.js"></script>
...
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");
const boxes = [];
const mousePos = { x: 0, y: 0 };
let panel;
let selectedBox; //클릭된 box넣어놓을 변수 (박스겹쳤을때 젤 큰숫자 클릭감지하려고)
let oX; //캔버스 중심점
let oY;
let step; //애플리케이션의 상태(단계)를 저장 1~4까지
let rafId;

ctx.font = "bold 30px sans-serif";

const canUtil = {
  toRadian: function(degree){
    return degree * Math.PI/180;
  }
};

function render() {
  ctx.clearRext(0,0, canvas.width, canvas.height);

  let box;

  for (let i =0; i < boxes.length; i++){
    box = boxes[i];
    // box.x += box.speed;  //각각 랜덤숫자만큼 가로로 이동
    // if(box.x > canvas.width){
    //   box.x = -box.width;
    // }
    box.draw();
  }
  switch(step){
    case 1: //step 1일때(박스클릭안했을시)만 박스들 움직이게 하기
      for (let i =0; i < boxes.length; i++){
        box = boxes[i];
        box.x += box.speed;  //각각 랜덤숫자만큼 가로로 이동
        if(box.x > canvas.width){
          box.x = -box.width;
        }
      }
      break;

    case 2:
      // panel.scale += 0.02; //동일한 속도로 이동.
      // scale은 0~1사이의 값이다.
      // 가속도했다가 줄이기. => 거리간격계산후 * 0.1(1/10만큼 이동) 점점 간격 좁혀서 이동하기
      // 현재크기 = 현재크기 + (목표크기 - 현재크기) * 0.1
      panel.scale = panel.scale + (1 - panel.scale) * 0.05;
      //각도 = 스케일(0~1) * 720;
      panel.angle = panel.scale * 720;  //스케일 속도에 맞게 2바퀴(720도) 회전하기
      panel.draw();
      if(panel.scale >= 0.999){
        panel.scale = 1;
        panel.angle = 720;
        step = 3;
      }
      break;

    case 3:
      panel.draw();
      break;
  }

  rafId = requestAnimationFrame(render);
  if(step === 3){
    panel.showContent();
    cancelAnimationFrame(rafId);
  }
}

let tempX, tempY, tempSpeed; //for문에서 변수생성은 바람직하지 않아서 밖으로 뺌.

function init(){
  step = 1;
  oX = canvas.width / 2;
  oY = canvas.height / 2;
  for (let i = 0; i < 10; i++) {
    tempX = Math.random() * canvas.width * 0.8;
    tempY = Math.random() * canvas.height * 0.8;
    tempSpeed = Math.random() * 4  + 1; //1~5 범위의 스피드 생성 (0나올때 1이어야 하니깐 +1)
    boxes.push(new Box(i, tempX, tempY, tempSpeed));
  }

  panel = new Panel();
  render();
}

canvas.addEventListener("click", (e) => {
  mousePos.x = e.layerX;
  mousePos.y = e.layerY;

  let box;
  for(let i = 0; i < boxes.length; i++;){
    box = boxes[i];
    if(mousePos.x > box.x &&
       mousePos.x < box.x + box.width &&
       mousePos.y > box.y &&
       mousePos.y < box.y + box.height){
         selectedBox = box;
    }
  }
  if(step === 1 && selectedBox){
    // console.log(selectedBox.index);
    step = 2;
  } else if(step === 3){
    step = 1;
    panel.scale = 0; //초기화
    selectedBox = null; //selectedBox찍었으면 다시 비워준다. (박스클릭했다가 밖 클릭해도 박스가 떠서)
    render(); //재귀해줌.반복
  }
});
init();

```

```jsx
//Box.js
class Box {
  constructor(index, x, y, speed) {
    this.index = index;
    this.x = x;
    this.y = y;
    this.speed = speed;
    this.width = 100;
    this.height = 100;
    this.draw(); //생성하는 순간 xy세팅되고 그리기
  }

  draw() {
    ctx.fillStyle = "rgba(0,0,0,0.5)";
    ctx.fillRect(this.x, this.y, 100, 100);
    ctx.fillStyle = "#fff";
    ctx.fillText(this.index, this.x + 30, this.y + 30);
  }
}
```

```jsx
//Panel.js
class Panel {
  constructor() {
    this.scale = 0;
    this.angle = 0;
  }

  draw() {
    ctx.fillStyle = "rgba(255,0,0,0.8)";
    //변환 초기화
    ctx.resetTransform();
    // ctx.setTransform(1,0,0,1,0,0);
    ctx.translate(oX, oY);
    ctx.scale(this.scale, this.scale);
    ctx.rotate(canUtil.toRadian(this.angle));
    ctx.translate(-oX, -oY);
    ctx.fillRext(oX - 150, oY - 150, 300, 300);
    ctx.resetTransform();
  }

  showContent(){
    ctx.fillStyle = '#fff';
    ctx.fillText(selectedBox, indexm oX, oY);

  }
}
```
