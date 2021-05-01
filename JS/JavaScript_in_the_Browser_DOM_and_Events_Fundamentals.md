# JavaScript in the Browser: DOM and Events Fundamentals.

## 1. What's the DOM and DOM Manipulation

### 1-1. What is the DOM?

DOM(Document Object Model)은 HTML 문서의 구조화된 표현이다. DOM은 JavaScript가 HTML에 접근할 수 있도록 해주는 interface이다. (DOM은 HTML 문서를 JavaScript가 접근, 조작할 수 있는 형태로 Parsing하여 만들어진 결과물이다.) DOM은 HTML 페이지가 로드되는 즉시 브라우저에 의해 자동으로 생성되고 트리구조로 저장된다. 이 트리 안에서 각 HTML요소는 객체의 형태를 가진 하나의 node가 된다.

![img](./common/images/DOM-model.png)
( DOM Tree )

### 1-1. DOM Manipulation.

Javascript에서 DOM에 접근할때는 항상 진입점인 document Object를 거친다.

<<<<<<< HEAD
#### 예시

```js
const myElement = document.querySelector(".message");
```

=======
>>>>>>> 8189de694ed8eba7172ae9ba70d7a804c05e258e
### 1.2. DOM에 대한 오해

- DOM은 HTML이다?<br/>
  DOM은 HTML로부터 생성되지만 이 둘은 다른것이다. 특정한 경우에서 DOM과 HTML문서가 다르게 나타나는 것으로 이를 알 수 있다.

- DOM은 Javascript언어의 한 요소이다?<br/>
  DOM은 Javascript의 요소가 아니라 Web API의 요소이다. WEB API에 Javascript로 작성된 DOM객체와 프로퍼티가 존재하는 것이다. 즉, Javascript는 Web API를 통해서 DOM에 접근하는 것으로 볼 수 있다.
