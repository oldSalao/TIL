# JavaScript in the Browser: DOM and Events Fundamentals.

## 1. What's the DOM and DOM Manipulation

### 1-1. What is the DOM?

DOM(Document Object Model)은 HTML 문서의 구조화된 표현이다. DOM은 JavaScript가 HTML에 접근할 수 있도록 해주는 interface이다. (DOM은 HTML 문서를 JavaScript가 접근, 조작할 수 있는 형태로 Parsing하여 만들어진 결과물이다.) DOM은 HTML 페이지가 로드되는 즉시 브라우저에 의해 자동으로 생성되고 트리구조로 저장된다. 이 트리 안에서 각 HTML요소는 객체의 형태를 가진 하나의 node가 된다.

![img](./common/images/DOM-model.png)
( DOM Tree )

### 1-1. DOM Manipulation.

Javascript에서 DOM에 접근할때는 항상 진입점인 document Object를 거친다.

#### 예시

```js
const myElement = document.querySelector(".message");
```

### 1.2. DOM에 대한 오해

- DOM은 HTML이다?<br/>
  DOM은 HTML로부터 생성되지만 이 둘은 다른것이다. 특정한 상황에서 DOM과 HTML문서가 다르게 나타나는 것으로 이를 알 수 있다.

- DOM은 Javascript언어의 한 요소이다?<br/>
  DOM은 Javascript의 요소가 아니라 Web API의 요소이다. WEB API에 Javascript로 작성된 DOM객체와 프로퍼티가 존재하는 것이다. 즉, Javascript는 Web API를 통해서 DOM에 접근하는 것으로 볼 수 있다.

## 2. Events

이벤트란 mouse click, key press등 page에서 발생하는 특정 사건을 의미한다. 우리는 event listener를 통해 특정 이벤트가 발생했을 때 이에 반응할 수 있다.

### 2-1. addEventListener()

아래와 같이 addEventListener method를 사용하여 element에 event listener를 추가할 수 있다. 이 method는 첫번째 parameter로 이벤트의 종류, 두번째 parameter로 event handler function을 받는다. event handler function에는 이벤트가 발생했을때 실행할 코드를 작성한다.

```js
const btn = document.querySelector(".check");
btn.addEventListener("click", function () {
  console.log("clicked!");
});
```

이렇게 이벤트 리스너를 추가하면 자바스크립트 엔진은 이벤트가 발생했을때 이벤트 핸들러 함수를 자동으로 호출한다.
