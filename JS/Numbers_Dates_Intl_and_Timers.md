# Numbers, Dates, Intl and Timers

## 1. Converting and Checking Numbers

### 1-1. Convering

- Conversion

  Number() 또는 +연산자를 사용해서 형변환이 가능하다. + 연산자를 문자열 앞에 붙이면 자바스크립트는 강제 형변환을 수행한다.

  ```js
  console.log(Number("23"));
  console.log(+"23"); // 23.
  ```

- Parsing

  parseInt, parseFloat이 있다.parseInt는 정수값을 얻어내고 parseFloat은 실수값을 얻어낸다. 단순 형변환이 아니다. 아래 예시를 보면 '30px'에서 px를 제거한 30이라는 값을 얻어온다. 즉, 숫자뒤에 어떤 단위나 기호가 있어도 자바스크립트가 자동으로 숫자를 얻어내서 변환을 수행한다. 하지만 변환할 문자열이 숫자로 시작하지 않으면 변환이 제대로 수행되지 않는다. 그리고 두번째 파라미터로 문자열을 어떤 진법을 통해 숫자로 변환할지 지정할 수 있다.(parseFloat은 10진법만 가능) parsing은 CSS에서 값을 얻어올 때 용이하다.

  ```js
  console.log(Number.parseInt("30px")); // 30.

  console.log(Number.parseInt("e30")); // NaN.

  console.log(Number.parseInt("0010", 2)); // 2.

  console.log(Number.parseFloat("2.5rem")); // 2.5

  console.log(Number.parseInt("2.5")); // 2
  ```

### 1-2. Checking

- isNaN

  값이 NaN인지 판별하는 메소드.

  ```js
  console.log(Number.isNaN(20)); // false
  console.log(Number.isNaN("20")); // false
  console.log(Number.isNaN(+"20X")); // true
  console.log(Number.isNaN(23 / 0)); // false. infinity는 NaN이 아니다.
  ```

- isFinite

  값이 Number인지 판별하는 메소드. isNaN은 값이 NaN인지 아닌지 여부만 판별하므로 Number인지 아닌지 여부를 판별하려면 isFinite를 쓰자.

  ```js
  console.log(Number.isFinite(20)); // true
  console.log(Number.isFinite("20")); // false
  console.log(Number.isFinite(20 / 0)); // false
  console.log(Number.isFinite(+"20X")); // false
  ```

- isInteger

  값이 정수인지 여부를 판별하는 메소드.

  ```js
  console.log(Number.isInteger(23)); // true
  console.log(Number.isInteger(23.0)); // true
  console.log(Number.isInteger(23 / 0)); // false
  console.log(Number.isInteger(23.4)); // false
  ```

## 2. Math and Rounding

### 2-1. sqrt

제곱근을 구할 수 있는 메소드다. 세제곱근 이상을 구하려면 \*\* 연산자를 이용하자

```js
console.log(Math.sqrt(25)); // 5
console.log(25 ** (1 / 3)); // 2.92...
```

### 2-2. max,min

최댓값과 최솟값을 구할 수 있는 메소드이다. 인자에 대해 강제 형변환을 수행한다. 파싱을 수행하지는 않는다.

```js
console.log(Math.max(5, 18, 23, 11, 2)); // 23
console.log(Math.max(5, 18, "23", 11, 2)); // 23
console.log(Math.max(5, 18, "23px", 11, 2)); // NaN

console.log(Math.min(5, 18, 23, 11, 2)); // 2
```

### 2-3. PI

원주율 상수가 존재한다. 원의 넓이를 구하는데에 사용할 수 있다.

```js
console.log(Math.PI); // 상수가 존재한다.(PI)

console.log(Math.PI * Number.parseFloat("10px") ** 2); //반지름이 10px인 원의 넓이.
```

### 2-4. random

0에서 1사이의 난수를 발생시키는 메소드이다. 추가적인 연산을 통해서 난수의 범위를 설정할 수 있다.

```js
console.log(Math.random()); // 0~1 사이의 난수 발생.
console.log(Math.trunc(Math.random() * 6 + 1)); // 1~6 사이의 난수 발생.

const randomInt = (min, max) =>
  Math.floor(Math.random() * (max - min) + 1) + min; // min과 max사이의 난수를 발생시키는 함수.
```

### 2-5. round,ceil,floor,trunc

소수를 다루는 메소드들이다. round는 반올림, ceil은 올림, floor는 내림이며 trunc는 소수점 아래를 제거하는 메소드이다. 음수의 경우를 생각하면 trunc보다는 floor를 사용하는게 더 낫다. 해당 메소드들은 인자에 대해 강제 형변환을 수행한다.

```js
console.log(Math.round(23.4)); // 23
console.log(Math.round(23.9)); // 24

console.log(Math.ceil(23.3)); // 24
console.log(Math.ceil(23.7)); // 24

console.log(Math.floor(23.3)); // 23
console.log(Math.floor("23.6")); // 23

console.log(Math.trunc(-23.3)); // -23
console.log(Math.floor(-23.3)); // -24
```

### 2-6. toFixed

숫자를 소수점아래 특정 자리까지 표현할 수 있도록 하는 메소드이다. 반올림을 수행하며 문자열을 반환한다. 아래 예시를 보면 2.7은 primitive 이지만 자바스크립트가 해당 값에 대해 number 객체로 박싱을 수행하기 때문에 toFixed 메소드를 호출할 수 있는 것이다.

```js
console.log((2.7).toFixed(0)); // '3'
console.log((2.7).toFixed(3)); // '2.700'
console.log(+(2.345).toFixed(2)); // 2.35. 반올림을 수행함.
```

## 3. The Remainder Operator
