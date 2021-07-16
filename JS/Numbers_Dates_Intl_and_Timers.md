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
