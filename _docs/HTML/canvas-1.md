---
title: canvas - 기본설정
category: HTML
order: 1
---

# canvas

- canvas는 HTML5의 요소로서, Javascript를 사용해 웹페이지에 그림을 그리는데 사용한다.
- 캔버스의 크기는 300px _ 150px (width _ height)가 초기 설정값이며, HTML height와 width 속성을 사용하여 바꿀 수 있습니다.
- 캔버스에 그림을 그리려면 JS Context 객체를 사용하여 그림을 생성할 수 있습니다.

### VScode 설정

- **Extensions에서 live Server설치. (테스트하기 위해서)**  
  index.html에서 우클릭-Open with live Server 클릭해서 실행

### canvas 기본설정

- index.html

```jsx
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
        <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=0">
        <title>Canvas</title>
        <link rel="stylesheet" href="./style.css"> //css와 연결
    </head>
    <body>
        <script type="module" src="./App.js"></script> //App.js와 연결
    </body>
</html>
```

- style.css

```jsx
* {
  outline: 0;
  margin: 0;
  padding: 0;
}

html {
  width: 100%;
  height: 100%;
}

body {
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: #ffcaec; //배경색 아무거나
}

canvas {
  width: 100%;
  height: 100%;
}

```

- App.js

```jsx
class App {
  constructor() {
    this.canvas = document.createElement("canvas"); //canvas 생성
    document.body.appendChild(this.canvas); //body 하단에 canvas삽입
    this.ctx = this.canvas.getContext("2d"); //canvas 2d context가져오기
    //ctx:context   /getContext: 2d그래픽의 그리기함수 사용가능
    this.pixelRatio = window.devicePixelRatio > 1 ? 2 : 1;
    //현재 표시 장치의 <물리적 픽셀: CSS 픽셀의 비율>을 반환. 물리적픽셀 canvas width,height를 원하는사이즈보다 2배 크게 만들고, css에서 원하는사이즈로 줄인다. 그러면 줄어들면서 고해상도처럼 된다.

    window.addEventListener("resize", this.resize.bind(this), false);
    this.resize(); //윈도우 창크기 변할때마다 resize함수 호출.
    // 스크린사이즈 가져오기 위해서 resize이벤드 걸어주고

    window.requestAnimationFrame(this.animate.bind(this)); // 애니메이션 구현되는 부분
  }

  resize() {
    this.stageWidth = document.body.clientWidth;
    this.stageHeight = document.body.clientHeight;

    this.canvas.width = this.stageWidth * this.pixelRatio;
    this.canvas.height = this.stageHeight * this.pixelRatio;
    this.ctx.scale(this.pixelRatio, this.pixelRatio);
  }

  animate() {
    window.requestAnimationFrame(this.animate.bind(this));
    this.ctx.clearRect(0, 0, this.stageWidth, this.stageHeight);
  }
}

window.onload = () => {
  new App();
};
```

---

### \* 고해상도에서 canvas사용하기

물리적 픽셀을 2배로 만들고 css 픽셀에서 줄인다.  
canvas width,height를 원하는사이즈보다 2배 크게 만들고,  
css에서 원하는사이즈로 줄인다. 그러면 줄어들면서 고해상도처럼 된다.

```jsx
// 예제 1
class App {
  constructor() {
...
    this.pixelRatio = window.devicePixelRatio > 1 ? 2 : 1;
    // 2:1 <물리적 픽셀: CSS 픽셀의 비율>을 반환.

    window.addEventListener("resize", this.resize.bind(this), false);
    this.resize();

    window.requestAnimationFrame(this.animate.bind(this));
  }
//사이즈 지정하는 함수
  resize() {
    this.stageWidth = document.body.clientWidth;
    this.stageHeight = document.body.clientHeight;

    this.canvas.width = this.stageWidth * this.pixelRatio;
    this.canvas.height = this.stageHeight * this.pixelRatio;
    this.ctx.scale(this.pixelRatio, this.pixelRatio);
  }
//그림그리는 함수
  animate() {
    window.requestAnimationFrame(this.animate.bind(this)); //실제 구동
    this.ctx.clearRect(0, 0, this.stageWidth, this.stageHeight);
  }
}

```

```jsx
// 예제 2
class App {
  constructor() {
	...
    //윈도우 창 크기가 변할 때마다 resize 함수를 호출
    window.addEventListener('resize', this.resize.bind(this));
    this.resize();

    requestAnimationFrame(this.animate.bind(this));

  }
 //캔버스 사이즈 지정하는 함수
  resize() {
    this.stageWidth = document.body.clientWidth;
    this.stageHeight = document.body.clientHeight;

    this.canvas.width = this.stageWidth * 2;
    this.canvas.height = this.stageHeight * 2;
    this.ctx.scale(2, 2);
  }

  //그림 그리는 함수
  animate() {
    requestAnimationFrame(this.animate.bind(this));
    // requestAnimationFrame 여기에 캔버스를 일단 깨끗하게 지워주는 코드 추가
    this.ctx.clearRect(0, 0, this.stageWidth, this.stageHeight);
  }
}
window.onload = () => {
  new App();
};
```

- **stageWidth와 stageHeight?**  
  브라우저 크기를 기억하기 위한 변수다.
  매번 document.body.clientWidth로 부르지 않으려고 따로 변수에 담는다.

- **css에서 canvas width, height: 100%**  
  canvas width, height를 resize로 2배하면 브라우저 밖까지 커진다.  
  그래서 css에서 canvas width,height: 100% 각각 적용해줘야 한다.  
  두배지만 css에서 압축해서 브라우저에서 다 보이게 함으로 해상도가 높아보인다.

- **resize에서 ctx.scale(2, 2);**  
  **but)** ctx로 그린 그림크기도 작아지므로 canvas크기가 2배 커진만큼 ctx도 2배로 키워줘야 원래 비율대로 그림이 그려진다.

---

## resize()

- 브라우저 크기에 맞춰 **캔버스 크기를 지정**하는 resize 함수를 생성
- 윈도우 창이 바뀔 때마다 resize 호출

---

## animate()

> 애니메이션 영화를 찍듯이 (그리고, 지우고, 그리고)를 반복하면 움직이는 것처럼 표현된다.

1. 캔버스 비우기
   `ctx.clearRect(x,y,width,height)`
2. 캔버스 상태 저장하기
3. 실제 그리기
4. 새롭게 그리기 전에 저장된 상태를 복원하기

---

## requestAnimationFrame(callback);

- callback : 다음 repaint를 위한 애니메이션을 업데이트할 때 호출할 함수

* 브라우저 렌더할 때, **reflow**(색,위치 등 배치하는 과정), **repaint**(계산된 요소들을 그리는 과정)가 있다.
* animation동작할때 repaint과정이 끝나지도 았았는데 reflow(좌표이동)하는 경우에 부자연스러운 동작이 나타난다. 그래서 repaint할 준비과정이 최적화될 때까지 기다려준 다음, 업데이트하는 함수를 호출한다.
* 프레임유실을 막아준다.

---

> ##### [✅ 색,윤곽선,투명도,패턴 ...참고 사이트](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial/Applying_styles_and_colors){: target="\_blank"}

## 사각형

1. ctx.**fillRect**(x, y, width, height) : 색 채워진 사각형
2. ctx.**clearRect**(x, y, width, height) : 특정영역을 지우기
3. ctx.**strokeRect**(x, y, width, height) :테두리만 있는 사각형

## 선

1. ctx.**beginPath**() : 선 시작점 알리기
2. ctx.**moveTo**(x, y) : 펜을 해당 지점으로 이동한다
3. ctx.**lineTo**(x, y) : 선을 만든다 (보이진 않음)
4. ctx.**stroke**() : 윤곽선을 그린다 (보임)
5. ctx.**closePath**() : 선 마침점 알리기(fill()는 자동으로 닫히므로 안해도됨)

## 호(arc)나 원

1. ctx.**beginPath**() : 시작
2. ctx.**arc**(x, y, radius(반지름), startAngle(시작각), endAngle(끝각), counterclockwise) : counterclockwise는 true(시계방향) false(반시계방향)이다.
3. ctx.**fill**()
4. ctx.**stroke**()
5. ctx.**closePath**() : 끝

- endAngle에는 각도가 아닌 **radians**를 써줘야 한다.  
  `radians = degrees * Math.PI / 180`  
   **360도 = 2PI = Math.PI X 2** 이므로 원(360도) 그릴려면 Math.PI X 2를 써준다.

```jsx
//예제
function radians(degrees) {
  return (degrees * Math.PI) / 180;
}
ctx.beginPath();
ctx.arc(x, y, radius, 0, radians(360), false); //방법1) radians(360)
ctx.stroke();
ctx.beginPath(); //beginPath 써줘야 선이 계속이어지는 걸 방지한다
ctx.arc(x, y, radius, 0, radians(360), false);
ctx.stroke();
ctx.arc(240, 160, 20, 0, Math.PI * 2, false); //방법2) Math.PI*2
```
