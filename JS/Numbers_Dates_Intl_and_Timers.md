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

## 3. Working with BigInt

es2020에서 등장한 정수의 특별한 타입. 기본적으로 Number타입은 64비트로 표현된다. 이중에서 실질적으로 수를 저장하는데 사용되는 비트는 53비트이다. 나머지는 소수점의 위치와 부호를 저장하기 위해 쓰인다. 53비트로 표현할 수 있는 수에는 제한이 있기때문에 제한보다 더 큰 수를 저장하고 사용하기 위해서는 BigInt를 사용하면 된다.

숫자끝에 n을 붙이거나 BigInt 메소드를 사용한다. 아래 예시를 보면 두가지 경우의 값이 다르다. BigInt 메소드를 사용한 결과가 정확하지 않기 때문이다. 이는 먼저 자바스크립트가 해당 숫자를 내부적으로 나타내고 BigInt로 변환하는 과정에서 문제가 생기는 것으로 보인다. 따라서 BigInt 메소드는 작은 수가 BigInt 형을 요구할 때 사용하도록 하자.

```js
console.log(534252345345683495683490589203589230482n); // 534252345345683495683490589203589230482n
console.log(BigInt(534252345345683495683490589203589230482)); // 534252345345683531517394623281907105792n
```

BigInt는 연산이 가능하다. 하지만 일반 Number 타입의 값과는 연산이 불가능하다.(에러 발생)

```js
console.log(10000n + 10000n); // 20000n
console.log(3242592305893205892306893405689430n * 1000000n); // 3242592305893205892306893405689430000000n

const huge = 23178947281394789789n;
const num = 23;
// console.log(huge * num); // error!
console.log(huge * BigInt(num)); // 533115787472080165147n

console.log(20n > 15); // true
console.log(20n === 20); // false. BigInt와 Number는 다르다.
console.log(typeof 20n); // bigint
console.log(20n == 20); // true. 강제 형변환이 이루어진다.

console.log(huge + " is Really Big!!"); // 23178947281394789789 is Really Big!! 문자열과 결합되면 n이 사라지고 문자열로 형변환이 된다.
```

BigInt에는 Math의 메소드를 사용할 수 없다.

```js
// console.log(Math.sqrt(huge)); // error! BigInt에는 Math의 메소드를 사용할 수 없다.
```

BigInt에 나누기 연산을 수행하면 소수부분은 표현되지 않는다.

```js
console.log(10n / 3n); // 3n. 소수부분이 제거된다.
console.log(10 / 3); // 3.333333...
```

## 4. Creating Dates

자바스크립트에서 날짜,시간과 관련된 프로그래밍을 하기 위해서는 Date라는 특수한 객체를 사용한다.

```js
const now = new Date();

console.log(now); // Sat Jul 17 2021 13:09:19 GMT+0900 (대한민국 표준시)
```

파라미터에 문자열을 전달하면 자바스크립트가 해당 문자열을 파싱하여 날짜를 반환한다. 문자열의 포맷에 유의하여 사용하자.

```js
console.log(new Date("Jul 17 2021 13:07:40")); //Sat Jul 17 2021 13:08:15 GMT+0900 (대한민국 표준시)
console.log(new Date("December 24, 2021")); // Fri Dec 24 2021 00:00:00 GMT+0900 (대한민국 표준시)
```

연,월,일,시,분,초,ms 순서대로 숫자를 파라미터에 전달하는 것도 가능하다. 월은 0부터 시작인 것에 유의하자(10은 11월). 만약 일수가 해당 월의 일수를 넘어가면 자동으로 다음 월의 날짜로 이어져 알맞은 시간을 얻어낸다.

```js
console.log(new Date(2037, 10, 19, 15, 23, 5)); // Thu Nov 19 2037 15:23:05 GMT+0900 (대한민국 표준시)
console.log(new Date(2037, 10, 33)); // Thu Dec 03 2037 00:00:00 GMT+0900 (대한민국 표준시)
```

파라미터에 타임스탬프를 전달할 수도 있다. 타임스탬프란 1970 1월 1일 00:00:00에서부터 경과된 시간을 ms 단위로 표현한 것이다.

```js
console.log(new Date(1000)); // Thu Jan 01 1970 09:00:01 GMT+0900 (대한민국 표준시)
```

Date 객체는 몇가지 메소드를 지니고 있다. 아래 예시를 살펴보자.

```js
const future = new Date(2037, 10, 19, 15, 23);
console.log(future); // Thu Nov 19 2037 15:23:00 GMT+0900 (대한민국 표준시).
console.log(future.getFullYear()); // 2037. Date 객체의 연도를 반환하는 메소드.
console.log(future.getMonth()); // 10. 월을 반환하는 메소드.
console.log(future.getDate()); // 19. 일을 반환하는 메소드.
console.log(future.getDay()); // 4. 요일을 반환하는 메소드. 일요일이 0이다.
console.log(future.getHours()); // 15. 시를 반환하는 메소드.
console.log(future.getMinutes()); // 23. 분을 반환하는 메소드.
console.log(future.getSeconds()); // 0. 초를 반환하는 메소드.
console.log(future.toISOString()); //2037-11-19T06:23:00.000Z. ISO를 따르는 문자열을 반환.
console.log(future.getTime()); // 2142224580000. 타임스탬프를 반환하는 메소드.

console.log(Date.now()); // 1626496107242. 현재 시간의 타임스탬프를 반환함.

future.setFullYear(2040); // Date의 연,월,시 등을 셋팅할 수 있다.
console.log(future); // Mon Nov 19 2040 15:23:00 GMT+0900 (대한민국 표준시)
```

## 5. Operations With Dates

타임스탬프를 통한 연산이 가능하다. Date 객체는 숫자로 형변환이 가능한데 형변환 시 타임스탬프를 얻을 수 있다. 아래 예시를 살펴보자. 날짜의 차이를 구하는 함수 calcDaysPassed를 구현했다. 만약 복잡한 연산이 요구된다면 moment.js 라이브러리를 사용하도록 하자.

```js
const future = new Date(2037, 10, 19, 15, 23);

console.log(+future); // 2142224580000

const calcDaysPassed = (date1, date2) =>
  Math.abs((date2 - date1) / (1000 * 60 * 60 * 24));

const days1 = calcDaysPassed(new Date(2037, 3, 14), new Date(2037, 3, 24));
console.log(days1); // 10

const days2 = calcDaysPassed(
  new Date(2037, 3, 14),
  new Date(2037, 3, 24, 10, 8)
);
console.log(days2); // 10.4222222222...
```

## 6. Internationalizing Dates (Intl)

자바스크립트는 Intl이라는 국제화 API를 가지고 있다. 이를 이용하여 날짜,시간에 각국의 언어에 맞는 포맷을 적용할 수 있다. 아래 예시는 DateTimeFormat을 활용해서 Date에 포맷을 적용시키는 예이다. DateTimeFormat에는 ISO language code가 들어간다. 테이블을 참고하여 사용하자. ( http://www.lingoes.net/en/translator/langcode.htm )

```js
console.log(new Intl.DateTimeFormat("ko-KR").format(new Date())); // 2021. 7. 18.
console.log(new Intl.DateTimeFormat("en-US").format(new Date())); // 7/18/2021
```

아래와 같이 DateTimeFormat의 두번째 파라미터에 객체를 전달함으로써 원하는 포맷을 구성할 수도 있다. 프로퍼티의 값으로는 'numeric','long','2-digit','short','narrow' 등을 사용할 수 있다. (참고 : https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat )

```js
const options = {
  hour: "numeric",
  minute: "numeric",
  day: "numeric",
  month: "long",
  year: "numeric",
  weekday: "long",
};

console.log(new Intl.DateTimeFormat("ko-KR", options).format(new Date())); // 2021년 7월 18일 일요일 오후 7:23
```

첫번째 파라미터에 전달될 locale 값은 navigator를 통해 브라우저에서 정보를 얻어와 전달할 수도 있겠다.

```js
console.log(navigator.language); // ko-KR
```

## 7. Internationalizing Numbers (Intl)

Intl은 날짜,시간 뿐만 아니라 숫자에 대해서도 포맷을 적용시킬 수 있다. NumberFormat 메소드를 이용하는데, DateFormat과 마찬가지로 locale 파라미터를 지니고 있다.

```js
const num = 3884764.23;

console.log(new Intl.NumberFormat("en-US").format(num)); // 3,884,764.23
console.log(new Intl.NumberFormat("ar-SY").format(num)); // ٣٬٨٨٤٬٧٦٤٫٢٣
```

객체를 두번째 파라미터에 전달해서 포맷을 지정할 수도 있다. 아래 예시는 단위를 지정한 것이다.

```js
const num = 3884764.23;
const options = {
  style: "unit",
  unit: "mile-per-hour",
};

console.log(new Intl.NumberFormat("en-US", options).format(num)); // 3,884,764.23 mph
console.log(new Intl.NumberFormat("ar-SY", options).format(num)); //ميل/س٣٬٨٨٤٬٧٦٤٫٢٣
```

아래 예시는 통화 단위를 지정한 것이다.

```js
const num = 3884764.23;
const options = {
  style: "currency",
  currency: "EUR",
};

console.log(new Intl.NumberFormat("en-US", options).format(num)); // €3,884,764.23
console.log(new Intl.NumberFormat("ar-SY", options).format(num)); // ٣٬٨٨٤٬٧٦٤٫٢٣ €
```

옵션은 MDN을 참고하여 작성하자.
( https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Intl/NumberFormat )

## 8. Timers: setTimeout and setInterval

자바스크립트에는 두가지 타이머가 있다. 바로 setTimeout과 setInterval이다. setTimeout은 특정 시간이 경과하면 한번만 실행되지만 setInterval은 우리가 멈추지 않는 한 지속적으로 실행된다.

### 8-1. setTimeout

첫번째 파라미터는 콜백 함수를 전달받으며, 두번째 파라미터는 ms단위의 시간을 전달받는다. 두번째 파라미터에 전달한 시간이 경과하면 콜백 함수를 실행한다. 이때 지정한 시간동안 코드 실행은 멈추지않고 계속된다. 따라서 예시의 출력은 아래와 같이 나타난다.

    Waiting...
    Hello

```js
setTimeout(() => console.log("Hello"), 3000); // 3초후 Hello 출력.
console.log("Waiting..."); // Waiting...
```

위의 코드에서 자바스크립트는 setTimeout을 실행할 때 백그라운드에서 시간을 카운팅하기 시작하고 콜백 함수를 해당 시간이 경과하면 호출하기 위해서 등록해둔다. 이후 자바스크립트는 곧바로 다음 코드의 실행을 이어나간다. 이와같은 메커니즘을 비동기 자바스크립트라고 한다. (참고 : https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Introducing)

setTimeout에 전달한 콜백 함수의 호출은 우리에게서 이루어지지 않는다. 그렇다면 어떻게 인자를 부여할 수 있을까? setTimeout의 세번째 파라미터부터는 콜백 함수에 부여할 인자를 전달할 수 있다. 아래 예시를 보자.

```js
setTimeout(
  (firstName, lastName) => console.log(`Hello ${firstName} ${lastName}`),
  3000,
  "Ha Neul",
  "Lee"
); // 3초후 Hello Haneul Lee 출력.
console.log("Waiting..."); // Waiting...
```

clearTimeout()을 이용해 타이머를 중지시킬 수 있다. setTimeout()을 호출하고 이를 변수에 할당한 후(setTimeout의 반환값은 타이머 식별자이다.), clearTimeout의 인자로 해당 변수명을 입력하면 타이머가 중단된다.

```js
const myName = { firstName: "Ha Neul", lastName: "Lee" };
const helloTimer = setTimeout(
  (name) => console.log(`hello ${name.firstName} ${name.lastName}`),
  3000,
  myName
); // 3초후 Hello Ha Neul Lee 출력.
console.log("Waiting..."); // Waiting...

if (myName.lastName === "Lee") {
  clearTimeout(helloTimer);
}
```

### 8-2. setInterval

어떤 작업이 특정 시간이 경과할 때마다 지속적으로 수행되게 하려면 setInterval을 사용하면 된다. setTimeout과 마찬가지로 clearTimeout을 사용해 타이머를 중단시킬 수 있다. 아래 예시를 살펴보자.

```js
const clock = setInterval(() => {
  if (cnt === 10) {
    clearTimeout(clock);
  }
  const now = new Date();
  console.log(now);
  cnt++;
}, 1000); // 1초마다 날짜,시간을 출력한다. 10번 출력 후 정지.
```
