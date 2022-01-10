---
title: canvas - animation, image
category: HTML
order: 2
---

## - animation

1. 애니메이션 멈추기(종료)

```jsx
// 예제1 ) requestAnimationFrame전에 if문으로 멈추기
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");
let xPos = 10; //xPos : xPosition. x위치

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.beginPath();
  ctx.arc(xPos, 150, 10, 0, Math.PI * 2, false);
  ctx.fill();
  xPos += 1; // xPos = xPos + 1을 줄인것

  // 1. 애니메이션 멈추기(종료)
  // 방법1)return;하기 :반지름 -10 을 해서 캔버스 끝에 닿을때 멈춤
  if (xPos >= canvas.width - 10) {
    return;
  }
  requestAnimationFrame(draw);
}
```

```jsx
// 예제2 ) cancelAnimationFrame로 멈추기
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");
let xPos = 10;
let timerId;

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.beginPath();
  ctx.arc(xPos, 150, 10, 0, Math.PI * 2, false);
  ctx.fill();
  xPos += 1;

  // 1. 애니메이션 멈추기(종료)
  //방법2) cancelAnimationFrame로 멈춤
  timerId = requestAnimationFrame(draw);
  if (xPos >= canvas.width - 10) {
    cancelAnimationFrame(timerId);
  }
}
```

---

## - image

1. 이미지 삽입하기
   > ctx.**drawImage**(image, dx, dy);  
   > ctx.**drawImage**(image, dx, dy, dWidth, dHeight);  
   > ctx.**drawImage**(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
   > ![canvas_drawimage](../canvas_drawimage.jpg)

```jsx
// 예제
const canvas = document.createElement("canvas");
this.ctx = this.canvas.getContext("2d");

const imgElem = document.createElement("img");
imeElem.src = "../images/1.png";
imeElem.addEventListener("load", () => {
  ctx.drawImage(imgElem, 50, 50);
});
```

2. 그림판 만드는 예제

```jsx
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");
const control = document.querySelector(".control");
const saveBtn = document.querySelector(".save-btn");
let drawingMode; //1. true일때만 그리기
let brush = "color"; // color, image로 그리기
let colorValue = "black"; //2. 색상변경하기

const imgElm = new Image();
imgElm.src = "../images/2.png";

function downHandler() {
  drawingMode = true;
}
function upHandler() {
  drawingMode = false;
}

function moveHandler(e) {
  //event에서 clientY는 브라우저기준/ layerY는 캔버스기준 으로 감지함
  if (!drawingMode) return;

  switch (brush) {
    case "color":
      ctx.beginPath();
      ctx.arc(e.layerX, e.layerY, 10, 0, Math.PI * 2, false);
      ctx.fill();
      break;
    case "image":
      ctx.drawImage(imgElm, e.layerX, e.layerY, 50, 50);
      break;
  }
}

function setColor(e) {
  brush = e.target.getAttribute("data-type");
  colorValue = e.target.getAttribute("data-color"); //class명의 속성을 가져오게함
  ctx.fillStyle = colorValue;
}

//이미지 저장하기
function createImage() {
  const url = canvas.toDateURL("image/png");
  const imgElem = new Image();
  imgElem.src = url;
}

canvas.addEventListener("mousedown", downHandler); //마우스클릭할때
canvas.addEventListener("mousemove", moveHandler);
canvas.addEventListener("mouseup", upHandler); //마우스땠을때
control.addEventListener("click", setColor);
saveBtn.addEventListener("click", createImage);
```
