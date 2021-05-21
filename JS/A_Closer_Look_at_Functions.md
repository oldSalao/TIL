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

## 2. How Passing Arguments Works: Value vs. Reference

자바스크립트에서 primitive와 reference는 함수에 전달될 때 다른 양상을 보인다. 아래 코드를 살펴보자.

```js
const flight = "LH234";
const jonas = {
  name: "Jonas Schmedtmann",
  passport: 24739479284,
};

const checkIn = function (flightNum, passenger) {
  flightNum = "Lh999";
  passenger.name = "Mr. " + passenger.name;

  if (passenger.passport === 24739479284) {
    alert("Check in");
  } else {
    alert("Wrong passport!");
  }
};

checkIn(flight, jonas); // alert : Check in
console.log(flight); // LH234
console.log(jonas); // {name: "Mr. Jonas Schmedtmann", passport: 24739479284}
```

checkIn 함수의 파라미터를 통해 전달되고 함수 안에서 값을 변경한 문자열 flight는 함수 밖에서 그 값이 변경되지 않았지만 객체 jonas의 경우는 name 프로퍼티가 변경된 것을 알 수 있다. 이는 마치 다른 언어의 call-by-value, call-by-reference 각각의 결과와 동일하다. 자바스크립트에서 위와같이 함수에 값을 전달하는 과정은 아래와 같다고 볼 수 있다.

```js
const flightNum = flight;
const passenger = jonas;
```

우리는 이미 primitive type과 reference type 간의 차이점을 알고 있다. 위와같은 상황에서 flightNum의 값을 변경하더라도 그것이 flight에는 반영이 되지 않지만 passenger의 프로퍼티를 변경하는 것은 jonas에 반영이 된다. 따라서 함수의 argument로써 reference type을 사용할때는 주의가 필요하다.

위의 과정을 살펴보면 결과가 그렇듯 jonas 객체는 함수가 호출될 때 call-by-reference가 이루어진듯 하지만 사실 자바스크립트에는 call-by-value만이 존재한다. 정확히 말하자면 자바스크립트는 함수에 reference가 아닌 reference(객체가 저장된 힙 메모리 주소)를 포함하고 있는 '값'을 파라미터에 넘겨주기 때문이다.
