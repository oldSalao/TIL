# JavaScript Fundamentals - Part 2.

## 1. Strict Mode

Strict Mode는 JavaScript에서 활성화할 수 있는 특별한 mode로 기존에는 조용히 무시되는 에러들을 명시해줌으로써 안전한 자바스크립트 코드를 작성하는데에 도움을 준다. 스크립트 최상단에 "use strict"를 작성하여 활성화한다.

### 예시

아래의 예시는 선언되지 않은 변수에 true를 할당한 것으로 strict 모드를 사용하지 않을 때에는 에러가 출력되지 않지만 strict 모드가 활성화되면 에러가 출력된다.

```js
"use strict";

let hasDriversLicense = false;
const passTest = true;

if (passTest) {
  hasDriverLicense = true; //Uncaught ReferenceError: hasDriverLicense is not defined
}
if (hasDriversLicense) {
  console.log("I can drive :D");
}
```

## 2. Functions

기본적으로 재사용이 가능한 코드 조각이며 parameter를 통해 값(arguments)을 입력받거나 return으로 값을 반환할 수 있다.

```js
function fruitProcessor(apples, oranges) {
  console.log(apples, oranges);
  const juice = `Juice with ${apples} apples and ${oranges} oranges.`;
  return juice;
}

const appleJuice = fruitProcessor(5, 0); //5 0 출력
console.log(appleJuice); //Juice with 5 apples and 0 oranges. 출력.
console.log(fruitProcessor(3, 2)); //3 2와 Juice with 3 apples and 2 oranges. 출력
```

## 3. Function Declarations vs. Expressions

### 3-1. anonymous function

이름이 없는 함수. 아래 예시의 함수 ( function (birthYear) {...} )는 표현식(Function Expressions)이라고 볼 수 있으며 변수 calcAge는 함수가 된다.

```js
const calcAge = function (birthYear) {
  return 2021 - birthYear + 1;
};
const age = calcAge(1995); // 27 출력.
```

### 3-2. Function Declarations

익명함수가 아닌 함수는 호이스팅으로 인해 선언하기전에 사용이 가능하다.

```js
const age = calcAge(1996);
console.log(age); // 26 출력.

function calcAge(birthYear) {
  return 2021 - birthYear + 1;
}
```

## 4. Arrow Functions

function expressions 의 한 형태이다.
(parameter) => {body} 와 같이 작성하며 변수에 할당하여 호출가능하다. 함수의 내용이 한 라인이라면 (parameter) => line 과 같이 작성가능(return 키워드 필요없음.). this 키워드를 사용하지 못한다.

### 예시.

```js
const yearsUntilRetirement = (birthYear, firstName) => {
  const age = 2021 - birthYear + 1;
  const retirement = 65 - age;
  return `${firstName} retires in ${retirement} years`;
};
console.log(yearsUntilRetirement(1996, "Jonas"));
```

```js
const calcAge = (birthYear) => 2021 - birthYear + 1;
const age = calcAge(1996);
console.log(age);
```

## 5. Arrays

JavaScript에서의 배열에는 모든 타입이 담길 수 있으며 가변길이 배열이다. 배열의 선언 방법은 아래와 같다.

```js
const friends = ["Micheal", "Steven", "Peter"];
const years = new Array(1991, 1984, 2000, 2021);
```

배열의 요소에 접근할때는 배열변수명[인덱스]를 사용한다. 그리고 배열의 길이를 구할때에는 length 프로퍼티를 사용한다.

```js
const friends = ["Micheal", "Steven", "Peter"];

console.log(friends[0]); // Micheal
console.log(friends[2]); // Peter
console.log(friends.length); // 3
console.log(friends[friends.length - 1]); // Peter
```

아래의 예시를 보면 const 변수로 선언된 배열의 요소가 변경되는데 이것이 가능한 이유는 primitive 타입은 불변성을 지니지만 배열은 그렇지 않기 때문이다. 하지만 아래와 동일한 상황에서 배열 자체를 변경하는것은 불가능하다.

```js
const friends = ["Micheal", "Steven", "Peter"];
console.log(friends); // (3) ["Micheal", "Steven", "Peter"]
friends[2] = "Jay";
console.log(friends); // (3) ["Micheal", "Steven", "Jay"]
//friends = ["Bob","Alice"]; // error
```

배열의 각 요소의 타입이 달라도 상관없다.

```js
const friends = ["Micheal", "Steven", "Peter"];
const firstName = "Jonas";
const Jonas = [firstName, "Schmedtmann", 2037 - 1991, "teacher", friends];
console.log(Jonas); // (5) ["Jonas", "Schmedtmann", 46, "teacher", Array(3)]
```

## 6. Basic Array Operations (Methods)

### 6-1. 요소 추가.

- Array.push(추가할 값) : 배열의 끝에 요소 추가. 반환값은 추가 후 배열의 길이.

- Array.unshift(추가할 값) : 배열의 시작에 요소 추가. 반환값은 추가 후 배열의 길이.

### 6-2. 요소 제거.

- Array.pop() : 배열의 마지막 요소 제거. 반환값은 제거된 요소.

- Array.shift() : 배열의 첫 요소 제거. 반환값은 제거된 요소.

### 6-3. 요소 검색

- Array.indexOf(찾을 요소) : 입력된 요소의 인덱스를 반환. 입력된 요소가 존재하지 않으면 -1 반환.

- Array.includes(찾을 요소) : ES6에서 도입된 메소드, 입력된 요소가 있다면 true, 없다면 false. 비교는 strict equality Operator(===)를 통해서 이루어짐
