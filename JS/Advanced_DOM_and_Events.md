# Advanced DOM and Events

## 1. How the DOM Really Works

### 1-1. What is the DOM?

DOM은 기본적으로 자바스크립트와 브라우저 사이의 인터페이스이다. 조금 더 자세히 말하면 브라우저가 렌더링 과정에서 HTML 문서를 파싱한 것이라고 할 수 있다.

DOM에 대한 특징을 몇가지 설명한다면 아래와 같다.

- 자바스크립트가 브라우저와 상호작용 할 수 있도록 해준다.

- 자바스크립트로 html 요소를 생성,수정,삭제할 수 있으며 스타일, 클래스, 속성에도 접근이 가능하다. 이벤트를 감지하고 반응할 수 있다.

- HTML문서로부터 우리가 상호작용 할 수 있는 DOM 트리가 생성된다.

- DOM은 DOM 트리와 상호작용 하는데에 사용되는 수많은 메소드와 프로퍼티를 포함하고 있는 복잡한 API이다.

### 1-2. DOM Tree

DOM 트리의 모든 노드는 자바스크립트에서 객체로 표현된다. 노드에는 여러 하위 타입이 있는데, 이는 Element, Text, Comment, Document 등이다. 이 덕분에 html의 모든 내용이 DOM에 포함될 수 있다.

- Element : HTML 태그 요소. Element 노드에는 유용한 프로퍼티와 메소드가 존재한다.(innerHTML, classList, append(), insertAdjanetHTML 등) Element는 HTMLElement 라는 하위 타입을 지니고 있으며 이는 또 여러 종류의 자식 타입으로 나뉜다.( HTMLButtonElement, HTMLDivElement 등 HTML 요소의 모든 종류에 대한 타입이 존재) 특정 타입의 Element 노드에는 특별한 프로퍼티가 존재한다. (특정 HTML 태그에는 특별한 속성이 존재하기 때문)

- Text : 요소안에 포함된 문자.

- Comment : 주석.

- Document : 문서 전체를 나타냄. DOM의 진입점.

### 1-3. Inheritance

노드는 상위 타입이 지니고 있는 메소드, 프로퍼티에 접근이 가능하다. 예시를 들자면 HTMLButtonElement는 곧 Element이며 Node이다. 해당 부분에 대한 자세한 이야기는 OOP 파트에서 해보도록 한다.

### 1-4. EventTarget

우리가 모든 요소에 이벤트리스너를 추가할 수 있는 이유는 노드의 상위 타입으로 EventTarget이 존재하기 때문이다. EventTarget은 Window 노드 타입의 상위 타입이기도 하다.

위의 내용들과 더불어 아래 이미지를 참고하자. (여러가지 타입들을 정리한 슬라이드)

![](./common/images/node_types.jpg)

## 2. Selecting, Creating, and Deleting Elements

DOM 요소에 접근하는 방법에는 여러가지가 있다. 아래 예시를 보자. querySelector는 자주 사용해봤으니 넘어가고, document.documentElement, document.head, document.body 를 통해 각각 html, head, body 요소에 접근할 수 있다. querySelectorAll 은 노드리스트를 반환하는데, 이는 Array.from()을 사용하면 배열로 변환이 가능하다.

```js
console.log(document.documentElement); // <html>...</html>
console.log(document.head); // <head>...</head>
console.log(document.body); // <body>...</body>

console.log(document.querySelector(".header")); // <header class="header"></header>

const allSections = document.querySelectorAll(".section");

console.log(allSections); // NodeList(4) [section#section--1.section, section#section--2.section, section#section--3.section, section.section.section--sign-up]

const allSectionsArr = Array.from(document.querySelectorAll(".section"));

console.log(allSectionsArr); // (4) [section#section--1.section, section#section--2.section, section#section--3.section, section.section.section--sign-up]
```

### 2-1. Selecting Elements

아래 예시를 보면 getElementsByTagName, getElementsByClassName은 HTMLCollection을 반환하는 것을 알수 있는데, 이는 NodeList와는 조금 다르다. HTMLCollection은 살아있다고 표현을 하는데, 이는 문서가 변경되면 HTMLCollection 또한 자동으로 변경되기 때문이다. (NodeList는 이런 현상이 일어나지 않음) HTMLCollection 또한 NodeList와 마찬가지로 Array.form()을 통해 배열로 변환이 가능하다. (배열로 변환 시 문서가 변경되어도 요소가 변경되지 않음) HTMLCollection은 때로 유용할 수 있으니 해당 내용을 꼭 유념하자.

```js
console.log(document.getElementById("section--1")); // <section class="section" id="section--1">...</section>

const allButtons = document.getElementsByTagName("button");

console.log(allButtons); // HTMLCollection(9) [button.btn--text.btn--scroll-to, button.btn.operations__tab.operations__tab--1.operations__tab--active, button.btn.operations__tab.operations__tab--2, button.btn.operations__tab.operations__tab--3, button.slider__btn.slider__btn--left, button.slider__btn.slider__btn--right, button.btn.btn--show-modal, button.btn--close-modal, button.btn]

const allButtonsArr = Array.from(document.getElementsByTagName("button"));

console.log(allButtonsArr); // (9) [button.btn--text.btn--scroll-to, button.btn.operations__tab.operations__tab--1.operations__tab--active, button.btn.operations__tab.operations__tab--2, button.btn.operations__tab.operations__tab--3, button.slider__btn.slider__btn--left, button.slider__btn.slider__btn--right, button.btn.btn--show-modal, button.btn--close-modal, button.btn]

console.log(document.getElementsByClassName("btn")); // HTMLCollection(5) [button.btn.operations__tab.operations__tab--1.operations__tab--active, button.btn.operations__tab.operations__tab--2, button.btn.operations__tab.operations__tab--3, button.btn.btn--show-modal, button.btn]
```
