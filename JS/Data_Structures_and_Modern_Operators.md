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
