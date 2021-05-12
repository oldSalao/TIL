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

위와 같은 객체가 있을때, 아래처럼 배열의 구조 분해와 다르게 객체는 index를 사용하지 않기 때문에 변수로 할당할 프로퍼티 명을 좌변의 {} 안에 작성하고 우변에 객체를 작성하면 된다.

```js
const { name, openingHours, categories } = restaurant;
console.log(name, openingHours, categories); // Classico Italiano {thu: {…}, fri: {…}, sat: {…}} (4) ["Italian", "Pizzeria", "Vegetarian", "Organic"]
```

변수명을 임의로 정하고 싶다면 좌변을 {프로퍼티명:변수명,...}과 같이 작성한다.

```js
const {
  name: restaurantName,
  openingHours: hours,
  categories: tags,
} = restaurant;

console.log(restaurantName, hours, tags); // Classico Italiano {thu: {…}, fri: {…}, sat: {…}} (4) ["Italian", "Pizzeria", "Vegetarian", "Organic"]
```

아래처럼 =을 사용하여 default값을 설정할 수 있다. {}안에 작성한 프로퍼티가 존재하지 않는다면 ( 존재한다면 default값은 적용되지 않는다. ) 해당 변수는 default값을 가지게 된다.

```js
const { menu = [], starterMenu: starters = [] } = restaurant;

console.log(menu, starters);
```

배열의 구조 분해 할당과 마찬가지로 객체를 사용하여 변수의 값을 바꿀 수 있다. 괄호를 사용해야 한다는 것에 주의해야한다.

```js
let a = 111;
let b = 999;

const obj = { a: 23, b: 7, c: 14 };

// { a, b } = obj; //error
({ a, b } = obj);
console.log(a, b); // 23 7
```

중첩된 배열을 구조 분해할 수 있는것과 마찬가지로 객체도 가능한데, : 이후 {}를 중복으로 사용하면 된다.

```js
const {
  fri: { open: o, close: c },
} = openingHours;
console.log(o, c);
```

restaurants 객체의 method를 아래와같이 변경하면 객체를 arguments로 전달함과 동시에 구조 분해가 이루어진다. 또한 parameter에 = 를 사용하여 default 값을 설정할 수 있다.

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

es6부터 제시된 연산자. iterable object(array, string, map, set. object는 불가능. es2018부터는 object도 사용 가능. )에 사용가능하다. 사용하면 모든 개별 요소의 값을 얻을 수 있다. 구조 분해 할당 연산자와 다른 점은 기본적으로 모든 요소를 얻는다는 것이며 새로운 변수를 생성하지 않는다는 것이다. Spread Operator는 쉼표로 구분된 값을 쓰는 장소에서만 사용할 수 있다.( ex.배열 생성( [ ] ), 함수의 parameter에 값 전달. )

아래는 배열에서의 예시이다.

```js
const arr = [7, 8, 9];
const badNewArr = [1, 2, arr[0], arr[1], arr[2]];
console.log(badNewArr); // [1, 2, 7, 8, 9]

const newArr = [1, 2, ...arr];
arr.push(4);
console.log(newArr); // [1, 2, 7, 8, 9]
console.log(arr); // [7, 8, 9, 4]
```

함수에서의 예시는 다음과 같다. 이를 통해 우리는 spread 연산자를 통해 콤마로 구분된 값을 얻는다는 것을 알 수 있다.

```js
console.log(...newArr); // 1 2 7 8 9
console.log(1, 2, 7, 8, 9); // 1 2 7 8 9
```

spread 연산자로 아래와 같이 얕은 복사를 수행하거나 두 객체를 병합할 수 있다.

```js
//Copy array
const mainMenuCopy = [...restaurant.mainMenu];
console.log(restaurant.mainMenu); // ["Pizza", "Pasta", "Risotto"]

//join 2 arrays
const menu = [...restaurant.starterMenu, ...restaurant.mainMenu];
console.log(menu); // ["Focaccia", "Bruschetta", "Garlic Bread", "Caprese Salad", "Pizza", "Pasta", "Risotto"]
```

위에서 설명했다시피 spread 연산자는 배열 외에도 iterable object( array, string, map, set )에 사용가능하다. (es2018 이후에는 object도 사용가능.)

문자열에서의 사용예.

```js
//Iterables : arrays, strings, maps, sets. Not objects
const str = "Jonas";
const letters = [...str, " ", "S."];
console.log(letters); // ["J", "o", "n", "a", "s", " ", "S."]
```

또한 콤마로 구분된 값을 사용하는 곳에만 적용이 된다

```js
console.log(...str); // J o n a s
// console.log(`${...str}`); // error!
```

함수의 parameter를 통한 값 전달에 사용되는 예를 보기위해 restaurant 객체에 아래와 같은 method를 추가했다.

```js
orderPasta: function (ing1, ing2, ing3) {
    console.log(`Here is your delicious pasta with ${ing1}, ${ing2}, ${ing3}`);
  },
```

orderPasta method에 spread 연산자를 이용하여 값을 전달하면 아래와 같다.

```js
const ingredients = ["mushrooms", "aspargus", "cheese"];

// restaurant.orderPasta(ingredients[0], ingredients[1], ingredients[2]);
restaurant.orderPasta(...ingredients); // Here is your delicious pasta with mushrooms, aspargus, cheese
```

es2018이후부터는 object에도 spread 연산자 사용이 가능해졌다. object에서의 사용 예.

```js
const restaurantCopy = { ...restaurant }; // Shallow copy
restaurantCopy.name = "Ristorante Roma";
console.log(restaurant.name); // Classico Italiano
console.log(restaurantCopy.name); // Ristorante Roma

const newRestaurant = { ...restaurant, founder: "Guiseppe", foundedIn: 1998 };

console.log(newRestaurant); // founder, foundedIn 프로퍼티가 추가되어 출력.
```

## 3. Rest Pattern and Parameters

Resr pattern은 spread 연산자와 문법이 같지만(...) 정 반대의 기능을 가졌다. Rest pattern은 spread 연산자와는 반대로 요소들을 모아서 객체를 생성한다. 기본적으로 우항에서 사용하는 spread 연산자와는 달리 Rest Pattern은 좌항에서 사용한다.

아래는 배열에서의 사용예이다. 구조 분해 할당 시 가장 끝에 위치하여 우항에서 할당되지 않고 남은 모든 요소들로 배열을 생성한다.

```js
const [a, b, ...others] = [1, 2, 3, 4, 5];

console.log(a, b, others); // 1 2 [3, 4, 5]
```

아래에서 나타난것과 같이 우항에서 사용하면 spread, 좌항에서 사용하면 rest pattern이며 rest pattern을 통해 만들어지는 배열은 구조 분해 할당 시 건너뛴 요소는 포함하지 않는다.

```js
const [pizza, , risotto, ...otherFood] = [
  ...restaurant.mainMenu,
  ...restaurant.starterMenu,
];

console.log(otherFood); // ["Focaccia", "Bruschetta", "Garlic Bread", "Caprese Salad"]
```

rest pattern은 객체에도 사용이 가능하다. 아래에 예시가 있다.

```js
const { sat, ...weekdays } = restaurant.openingHours;

console.log(weekdays); // {thu: {…}, fri: {…}}
```

또한 함수 정의시 parameter로도 사용이 가능하다. 사용법은 기본적으로 위와 같으며 예시를 보면 함수 호출 시 파라미터에 할당되지 않은 arguments로 배열을 생성하는 것을 알 수 있다.

```js
const add = function (a, b, ...numbers) {
  console.log(a, b, numbers);
};

add(2, 3); // 2 3 []
add(5, 3, 7, 2); // 5 3 [7, 2]
add(8, 2, 5, 3, 2, 1, 4); // 8 2 [5, 3, 2, 1, 4]
```

```js
const add = function (...numbers) {
  let sum = 0;
  for (let i = 0; i < numbers.length; i++) {
    sum += numbers[i];
  }
  console.log(sum);
};
const x = [23, 5, 7];

add(...x); // 35
```

## 4. Short Circuiting (&& and ||)

&&와 ||에는 모든 값을 사용할 수 있으며 또한 이들은 모든 값을 반환할 수 있다.

### 4-1. OR ( || )

|| 사용시 첫번째 피연산자가 truthy value라면 곧바로 그 값을 반환한다. 이 때, 다른 피연산자는 비교를 하지도 않는다. 이러한 현상을 Short Circuiting이라고 한다. 만약 두 피연산자가 모두 falsy value라면 마지막 피연산자를 반환한다.

예시

```js
console.log(3 || "Jonas"); // 3
console.log("" || "Jonas"); // Jonas
console.log(true || 0); // true
console.log(undefined || null); // null
console.log(undefined || 0 || "" || "Hello" || 23 || null); // Hello
```

이러한 성질은 default value를 설정하는데에 활용할 수 있다. 아래 예시에서 restaurant.numGuests는 존재하지 않는다.(undefined) 따라서 guests에는 10이 할당되는데 만약 존재한다면 Short Circuiting에 의해 10이아닌 restaurant.numGuests가 할당 될 것이다.

```js
const guests = restaurant.numGuests || 10;
console.log(guests); // 10
```

### 4-2. AND ( && )

AND는 OR과는 반대의 Short Circuiting을 수행한다. 첫번째 피연산자가 falsy value이면 다른 피연산자는 비교를 수행하지 않고 바로 해당 falsy value를 반환한다.
만약 모든 피연산자가 truthy value라면 마지막 피연산자를 반환한다.

예시

```js
console.log(0 && "Jonas"); // 0
console.log(7 && "Jonas"); // Jonas
console.log("Hello" && 23 && "null" && "Jonas"); // Jonas
```

아래 예시는 AND를 활용해서 restaurant.orderPizza Method가 존재하지 않는다면 곧바로 undefined를 반환하고 존재한다면 이를 호출하는 코드이다.

```js
restaurant.orderPizza && restaurant.orderPizza("mushrooms", "spinach");
```

## 5. The Nullish Coalescing Operator (??)

Nullish value란 null과 undefined를 의미한다.(0과 ''은 아님.) ??은 Nullish Coalescing Operator라고 하며 es2020에서 제시되었으며 ||과 같은 기능을 하지만 0과 ''을 truthy value 취급한다.

예시.

```js
restaurant.numGuests = 0;
// Nullish : null and undefined (Not 0 or ``)
const guestCorrect = restaurant.numGuests ?? 10; // 0
console.log(guestCorrect);
```

## 6. Looping Arrays: The for-of Loop

배열의 모든 요소에 대해 반복적인 작업을 해야할 때 활용하기 좋다. 문법은 아래 코드를 확인하자. for문 안에서 menu배열의 모든 요소가 순서대로 item 변수에 할당이 되고 우리는 이를 사용할 수 있게 된다.

```js
const menu = [...restaurant.starterMenu, ...restaurant.mainMenu];

for (const item of menu) {
  console.log(item); // menu 배열의 모든 요소 출력.
}
```

배열의 entries 메소드를 활용하여 모든 요소로부터 인덱스와 값으로 이루어진 배열을 얻을 수 있다.

```js
for (const item of menu.entries()) {
  console.log(item);
}
```
