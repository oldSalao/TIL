# Data Structures and Modern Operators

## 1. Destructuring (구조 분해 할당.)

구조 분해 할당 구문은 배열이나 객체의 속성을 해체하여 그 값을 개별 변수에 담을 수 있게 하는 JavaScript 표현식이다.

### 1-1. Arrays

배열의 구조 분해 할당은 기본적으로 아래와 같이 이루어진다.

```js
const arr = [2, 3, 4];
//일반적인 배열의 요소를 변수에 할당하는 방법
const a = arr[0];
const b = arr[1];
const c = arr[2];

//구조 분해 할당.
const [x, y, z] = arr;
console.log(x, y, z); // 2, 3, 4
```

다음과 같은 객체가 있다고 했을때,

```js
const restaurant = {
  name: "Classico Italiano",
  location: "Via Angelo Tavanti 23, Firenze, Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian", "Organic"],
  starterMenu: ["Focaccia", "Bruschetta", "Garlic Bread", "Caprese Salad"],
  mainMenu: ["Pizza", "Pasta", "Risotto"],
  order: function (starterIndex, mainIndex) {
    return [this.starterMenu[starterIndex], this.mainMenu[mainIndex]];
  },

  openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0, // Open 24 hours
      close: 24,
    },
  },
};
```

배열의 구조 분해 할당은 다양한 방법으로 사용 가능하다.

```js
const [first, , second] = restaurant.categories; // , , 로 인해 중간에 한 요소를 건너 뜀.
console.log(first, second); // Italian Vegetarian
```

```js
let [main, , secondary] = restaurant.categories;

//Switching variables
// const temp = main;
// main = secondary;
// secondary = temp;

//Switching variables with destructuring operator
[main, secondary] = [secondary, main];
```

```js
//Receive 2 return values from a function
const [starter, mainCourse] = restaurant.order(2, 2);
console.log(starter, mainCourse);
```

```js
// Nested destructuring
const nested = [2, 4, [5, 6]];

// const [i, , j] = nested;
// console.log(i, j); // 2 [5, 6]

const [i, , [j, k]] = nested;
console.log(i, j, k); // 2, 5, 6
```

```js
//Default values
const [p = 1, q = 1, r = 1] = [8, 9];
console.log(p, q, r); // 8 9 1
```

### 1-2. Objects

객체의 구조 분해 할당은 아래와 같이 이루어진다.

```js
const restaurant = {
  name: "Classico Italiano",
  location: "Via Angelo Tavanti 23, Firenze, Italy",
  categories: ["Italian", "Pizzeria", "Vegetarian", "Organic"],
  starterMenu: ["Focaccia", "Bruschetta", "Garlic Bread", "Caprese Salad"],
  mainMenu: ["Pizza", "Pasta", "Risotto"],
  order: function (starterIndex, mainIndex) {
    return [this.starterMenu[starterIndex], this.mainMenu[mainIndex]];
  },

  openingHours: {
    thu: {
      open: 12,
      close: 22,
    },
    fri: {
      open: 11,
      close: 23,
    },
    sat: {
      open: 0, // Open 24 hours
      close: 24,
    },
  },
};
```

위와 같은 객체가 있을때,

```js
const { name, openingHours, categories } = restaurant;
console.log(name, openingHours, categories); // Classico Italiano {thu: {…}, fri: {…}, sat: {…}} (4) ["Italian", "Pizzeria", "Vegetarian", "Organic"]
```

위처럼 배열의 구조 분해와 다르게 객체는 index를 사용하지 않기 때문에 변수로 할당할 프로퍼티 명을 좌변의 {} 안에 작성하고 우변에 객체를 작성하면 된다.

```js
const {
  name: restaurantName,
  openingHours: hours,
  categories: tags,
} = restaurant;

console.log(restaurantName, hours, tags); // Classico Italiano {thu: {…}, fri: {…}, sat: {…}} (4) ["Italian", "Pizzeria", "Vegetarian", "Organic"]
```

변수명을 임의로 정하고 싶다면 좌변을 {프로퍼티명:변수명,...}과 같이 작성한다.

```js
const { menu = [], starterMenu: starters = [] } = restaurant;

console.log(menu, starters);
```

위처럼 =을 사용하여 default값을 설정할 수 있다. {}안에 작성한 프로퍼티가 존재하지 않는다면 ( 존재한다면 default값은 적용되지 않는다. ) 해당 변수는 default값을 가지게 된다.

```js
let a = 111;
let b = 999;

const obj = { a: 23, b: 7, c: 14 };

// { a, b } = obj; //error
({ a, b } = obj);
console.log(a, b); // 23 7
```

배열의 구조 분해 할당과 마찬가지로 객체를 사용하여 변수의 값을 바꿀 수 있다. 괄호를 사용해야 한다는 것에 주의해야한다.

```js
const {
  fri: { open: o, close: c },
} = openingHours;
console.log(o, c);
```

중첩된 배열을 구조 분해할 수 있는것과 마찬가지로 객체도 가능한데, : 이후 {}를 중복으로 사용하면 된다.

```js
orderDelivery: function ({
    starterIndex = 1,
    mainIndex = 0,
    time = '20:00',
    address,
  }) {
    console.log(starterIndex);
    console.log(
      `Order received! ${this.starterMenu[starterIndex]} and ${this.mainMenu[mainIndex]} will be delivered to ${address} at ${time}`
    );
  },
```

restaurants 객체의 method를 위와같이 변경하면 객체를 arguments로 전달함과 동시에 구조 분해가 이루어진다. 또한 parameter에 = 를 사용하여 default 값을 설정할 수 있다.

```js
restaurant.orderDelivery({
  time: "22:30",
  address: "Via del sole, 21",
  mainIndex: 2,
  starterIndex: 2,
}); // Order received! Garlic Bread and Risotto will be delivered to Via del sole, 21 at 22:30

restaurant.orderDelivery({
  address: "Via del sole, 21",
  starterIndex: 2,
}); // Order received! Garlic Bread and Pizza will be delivered to Via del sole, 21 at 20:00
```

## 2. The Spread Operator (...)
