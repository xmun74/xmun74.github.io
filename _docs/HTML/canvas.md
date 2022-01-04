---
title: canvas
category: HTML
order: 1
---

### - 고해상도에서 canvas사용하기

canvas width,height를 원하는사이즈보다 2배 크게 만들고,

css에서 원하는사이즈로 줄인다. 그러면 줄어들면서 고해상도처럼 된다.

```jsx
const canvas = documents.querySelector(".canvas"); // .클래스로 canvas호출
```

```jsx
const ctx = canvas.getContext("2d"); //ctx:context/getContext:2d그래픽의 그리기함수 사용가능
```

## 사각형

ctx.fillRect(x, y, width, height);

clearRect()

strokeRect()

---

## 원

ctx.arc(240, 160, 20, 0, Math.PI\*2, false);
