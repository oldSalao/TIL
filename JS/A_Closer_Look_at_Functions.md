# A Closer Look at Functions.

## 1. Default Parameters

함수의 파라미터에는 값이 전달되지 않을시에 사용할 기본값을 설정할 수 있다.

es6 이전에는 아래와 같이 shortcircuting을 활용해서 defalut parameter를 사용했다. 파라미터로 값이 전달되지 않으면 값이 undefined가 되는것을 이용한 것이다.

```js
const bookings = [];

const createBooking = function (flightNum, numPassanger, price) {
  numPassanger = numPassanger || 1;
  price = price || 199;

  const booking = {
    flightNum,
    numPassanger,
    price,
  };
  console.log(booking);
  bookings.push(booking);
};

createBooking("LH123"); // {flightNum: "LH123", numPassanger: 1, price: 199}
```

es6이후에는 아래처럼 간단하게 default 값을 설정할 수 있다.

```js
const bookings = [];

const createBooking = function (flightNum, numPassanger = 1, price = 199) {
  const booking = {
    flightNum,
    numPassanger,
    price,
  };
  console.log(booking);
  bookings.push(booking);
};

createBooking("LH123"); // {flightNum: "LH123", numPassanger: 1, price: 199}
```

또한 계산된 값을 default 값으로 설정할 수도 있다.

```js
const bookings = [];

const createBooking = function (
  flightNum,
  numPassanger = 1,
  price = 199 * numPassanger
) {
  const booking = {
    flightNum,
    numPassanger,
    price,
  };
  console.log(booking);
  bookings.push(booking);
};

createBooking("LH123"); // {flightNum: "LH123", numPassanger: 1, price: 199}
createBooking("LH123", 2, 800); // {flightNum: "LH123", numPassanger: 2, price: 800}
createBooking("LH123", 5); // {flightNum: "LH123", numPassanger: 5, price: 995}
```

만약 여러개의 파라미터중 값을 전달하고 싶지 않은 파라미터가 존재한다면 아래와같이 함수를 호출하면 된다.

```js
createBooking("LH123", undefined, 1000); // {flightNum: "LH123", numPassanger: 1, price: 1000}
```
