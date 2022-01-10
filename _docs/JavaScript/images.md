---
title: Web API
category: JavaScript
order: 1
---

_\* MDN 요약_

## API

#### [(**A**pplication **P**rogramming **I**nterfaces: 응용 프로그래밍 인터페이스) 란?](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Client-side_web_APIs/Introduction){: target="\_blank"}

개발자가 복잡한 기능을 만들기 위해서 프로그래밍 언어로 제공되는 구성이다. 개발자는 해당 프로그래밍 언어의 함수를 활용하여 기능을 구현하고 어플리케이션을 만들 수 있게 된다.

![plug-socket](../plug-socket.png)

MDN의 **콘센트 예시**를 들면 콘센트에 코드(API)를 꽂아서 전자레인지, TV 등을 사용하는 것과 같다. 우리는 코드를 꽂기만 하면 내부동작이 어떻게 되는지는 상관하지 않고 기능들을 사용한다. 여기서 코드가 API인 것이다.

또 다른 **키보드 예시**로는, 키보드(API)를 누르면 프로그램들이 서로 소통해서 컴퓨터 화면에 글자를 출력하듯이. 사용자는 키보드를 누르기만 하면 다양한 기능들을 사용할 수 있다. API는 데이터와 서버를 가진 사람들이 프로그램들을 서로 소통하기 위해 만들었다. 공공api, 날씨api 등처럼 다양하게 디자인할 수 있다. 키보드를 누르는 순간, 내부에선 많은 일들이 일어나지만 어떻게 작업되는지는 볼 수 없다.

### ⭕클라리언트 측 APIs (**Client**-side JavaScript)

- **브라우저 Browser API**  
  웹 브라우저에 내장된 API로 브라우저와 컴퓨터환경의 데이터를 노출하고 사용하는 작업들을 수행할 수 있다.

- **타사 Third-party API**  
  브라우저에 내장되어 있지 않은 API로 웹에서 해당코드와 정보를 검색해야 한다.  
  EX) 트위터 API ....

### ❌타사 APIs (Third-party API)

트위터, 구글 지도, 페이스북, 텔레그램, 유튜브 API 등 매우 다양하게 존재한다.

### 📝Web API로 하는 작업

- 브라우저에 로드된 **문서를 조작하는 API**.  
  <span style="color:#008000"> 예) HTML, CSS 조작하는 DOM(Document Object Model) API (HTML생성, 제거 및 변경, 새 스타일을 적용 ...)</span>

- **서버에서 데이터를 가져오는 API**가 일반적으로 사용된다. 서버에서 전체 페이지를 재로드하지 않아도 즉시 업데이트할 수 있다. 그러면 사이트가 더 반응적이면서 빠르게 보여진다.  
  <span style="color:#008000">예) XMLHttpRequest에 Fetch API</span>

- **그래픽을 그리고 조작하는 API**. HTML요소에 포함된 픽셀 데이터를 프로그래밍 방식으로 업데이트해 2D, 3D 장면으로 생성하게 해준다. 이는 애니메이션처럼 연속된 장면을 만들기 위해 사용된다.  
  <span style="color:#008000">예) Canvas, WebGL canvas </span>

- **오디오 및 비디오 API**. 자막표시, 캡쳐 등 멀티미디어 작업을 할때 사용한다.  
  <span style="color:#008000">예) HTMLMediaElement, Web Audio API 및 WebRTC</span>

- **장치(Device) API**. 하드웨어에서 데이터 조작하고 검색하기 위한 API로 웹 앱에서 유용한 방식이다.  
  <span style="color:#008000">예) Notifications, Vibration API</span>

- **클라리언트 측 저장소(Client-side storage) API**. 클라이언트 측에서 페이지로드 간에 상태를 저장한다.  
  <span style="color:#008000">예) Web Storage API, IndexedDB API</span>

### 🎮API의 작동 방법

**- 객체 기반으로 상호작용**  
코드는 데이터, 기능이 담긴 컨테이너 역할을 하는 하나 이상의 JavaScript 객체를 이용하여 API와 상호작용한다.

**- Entry Point 진입점 존재**  
Web API 사용할때 진입점이 있다.  
예) canvas API는 `getContext('2d')`, DOM API는 `document()` 등

**- 이벤트를 사용하여 상태 변경**  
일부 API에 event가 없더라도, 대부분은 최소한 몇 개가 포함된다.  
예) XMLHttpRequest()은 `onload`, `open`, `send` ...

**- 적절한 경우 보안 메커니즘 적용**  
예) WebAPI 중 잠재적으로 민감한 데이터 전송시에는 HTTPS를 통한 페이지에서만 작동된다.
