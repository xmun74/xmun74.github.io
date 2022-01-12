---
title: theta(θ), degree, radian, π
category: JavaScript
order: 2
---

### θ(Theta:세타)

삼각함수에서 sinθ, cosθ등 각도를 세타로 표시하는데, 세타는 각도단위(60°, 90°..)가 아니라 호도법(Radian)이다.

### 60분법(Degree)

각도라고 표현하며 (ex.60°, 90°) 60분법, 영어로는 Degree라고 한다.

### 호도법(Radian:라디안)

: **호**의 길이로 **각도**를 표현하는 방법

- 수학에서는 각도(Degree:60분법)으로 표현하지 않고 호도법(Radian)으로 표현한다.
- 호의 길이가 1이고, 원의 반지름도 1이면 1 Radian이라고 부른다.

### 파이(π)

: 원의 지름이 1일때 원의 둘레의 길이를 설명할때 사용한다.  
파이(π) = 3.14...는 원의 지름이 1일때 원의 둘레의 길이를 말한다.

- 파이(π) = 원주 / 지름

---

##### 각도° = 라디안변환

360 degree = 2 \* Math.PI  
180 degree = Math.PI  
1 degree = (Math.PI / 180)  
x degree = (x \* Math.PI / 180)

##### 라디안, 각도 구하기

radian = degree \* (Math.PI / 180) = Math.atan2(y, x)  
degree = radian \* (180 / Math.PI)  
degree = Math.atan2(y, x) \* (180 / Math.PI)

##### atan2() 함수

1. Math.atan2(y, x) : 수직각도 구하는 함수
2. Math.atan2(y, x) + 90 \* (Math.PI / 180): 수평각도 구하는 함수

- 2-1) atan2(y, x)이 수직이니깐 수평으로 바꾸기 : 90을 더하기
- 2-2) atan2(t, x)이 라디안을 리턴함므로 => \* (Math.PI / 180) 하기
