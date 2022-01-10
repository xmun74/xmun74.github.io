---
title: canvas - video, transform
category: HTML
order: 3
---

## - video

1. 비디오 재생하기

```jsx
//예제 1
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <style>
      video {
        position:absolute;
        width:0;
        height:0;
      }
    </style>
  </head>
  <body>
  <h1>video</h1>
  <video class="video" src="../images/video.mp4" autoplay muted loop>
    autoplay:자동재생 muted:무음(크롬에선 소리나는 영상 자동재생 안됨.그래서
    무음해줘야함) loop:반복재생
  </video>;
    <script>
      const canvas = document.createElement("canvas");
      document.body.appendChild(this.canvas);
      this.ctx = this.canvas.getContext("2d");
      let canPlayState = false;

      ctx.textAlign = 'center';
      ctx.fillText('비디오재생중', 300, 200);
        //이미지 대신에 비디오를 그렸다
      const videoElem = document.querySelector('.video');
      videoElem.addEventListener('canplaythrough', render);

      function render() {
        ctx.drawImage(videoElem, 0, 0, 600, 400);
        requestAnimationFrame(render);
      }
    </script>
  </body>
</html>


```

---

# [transform 변형](https://developer.mozilla.org/ko/docs/Web/API/Canvas_API/Tutorial/Transformations)

> 초기화(resetTransform or setTransform) => translate 이동 => scale 늘리기 순으로 해야 한다.

- ctx.**save**()저장과 ctx.**restore**()복원
- ctx.**setTransform**(a, b, c, d, e, f) : 변환을 초기화해준다.  
  현재 변형 상태를 단위 행렬로 재설정하고 나서 동일한 인수로 transform() 메소드를 적용합니다. 이는 기본적으로 현재의 변형을 무효로 한 후에 명시된 변형으로 바뀌는데, 한번에 모든 게 진행됩니다. 단위행렬을 이용해서 변환을 초기화해주는 것이다.  
   ctx.**resetTransform**()
- ctx.**translate**(x, y) : 이동
- ctx.**scale**() : scale은 0~1사이의 값이다.

**1. save()저장과 restore()복원**

```jsx
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");

ctx.fillRect(100, 100, 200, 200);
ctx.fillStyle = "orange";
ctx.fillRect(150, 150, 200, 200);

ctx.save(); //전 상태를 저장 (오렌지)

ctx.fillStyle = "blue";
ctx.beginPath();
ctx.arc(300, 300, 50, 0, Math.PI * 2, false);
ctx.fill();

ctx.restore(); // 전 상태를 복원(블루)

ctx.beginPath();
ctx.arc(300, 300, 20, 0, Math.PI * 2, false);
ctx.fill(); // 저장된 색 출력 (오렌지)
```

**2. translate(x, y) 변환**

```jsx
// 센터 중심으로 점점 커지고, 회전하는 사각형을 애니메이션으로 만들기
const canvas = document.createElement("canvas");
document.body.appendChild(this.canvas);
this.ctx = this.canvas.getContext("2d");
let scaleValue = 1;
let rotationValue = 0;

function toRadian(d) {
  return (d * Math.PI) / 180;
}

function draw() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  ctx.save(); //초기 값 (0,0 왼쪽 위)
  ctx.setTransform(1, 0, 0, 1, 0, 0); //setTransform : 변환을 초기화해준다음에 변환하는 습관을 가져야 한다.
  ctx.translate(350, 350);
  ctx.scale(scaleValue, scaleValue);
  ctx.rotate(toRadian(rotationValue)); // 회전하기
  ctx.strokeRect(-50, -50, 100, 100); // 변환한 다음 그려줘야 보인다
  ctx.restore(); //복원 값(-50, -50)

  scaleValue += 0.001;
  rotationValue += 1;

  ctx.fillRext(10, 10, 30, 30);

  requestAnimationFrame(draw);
}
```

- canvas는 왼쪽 위가 중심 시작점이다. scale하려면 중심점으로 이동해서 크기를 키워야 한다.
- 변환을 초기화 => 변환하고 => scale 조정 해야한다.  
  ctx.setTransform(1, 0, 0, 1, 0, 0);  
  ctx.translate(350, 350);  
  ctx.scale(scaleValue, scaleValue);
