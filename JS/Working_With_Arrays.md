# Working With Arrays

## 1. Simple Array Methods

자바스크립트에서 배열은 객체이며, 내장 메소드를 가지고있다. 이런 메소드들은 MDN을 통해 살펴보는것을 추천한다.

### 1-1. slice

shallow copy를 수행하며, 배열의 일부분을 복사하여 반환한다. 파라미터는 시작인덱스와 끝인덱스이다. 끝인덱스-1 까지의 요소까지 복사된다는 것에 유의하자. 또한 인덱스의 값으로 - 값을 넣을수 있는데, 제일 끝 인덱스가 -1이다.

```js
let arr = ["a", "b", "c", "d", "e"];

console.log(arr.slice(2, 4)); // ["c","d"]
console.log(arr.slice(2)); // ["c","d","e"]
console.log(arr.slice(-2)); // ["d","e"]
console.log(arr.slice(1, -2)); // ["b","c"]
console.log(arr.slice()); // ["a","b","c","d","e"]
console.log([...arr]); // ["a","b","c","d","e"]
console.log(arr); // ["a","b","c","d","e"]
```

### 1-2. splice

slice와는 다르게 원본 배열의 요소가 제거되고 제거된 요소로 이루어진 배열을 반환한다. 파라미터로는 시작 인덱스와 제거할 요소의 갯수를 받는다.

```js
let arr = ["a", "b", "c", "d", "e"];

console.log(arr.splice(3)); // ["d","e"]
console.log(arr.splice(0, 2)); // ["a", "b"]
console.log(arr.splice(-1)); // ["c"]
console.log(arr); // []
```

### 1-3. reverse

배열의 요소 순서를 뒤집는다. 원본 배열에 적용된다.

```js
const arr2 = ["j", "i", "h", "g", "f"];

console.log(arr2.reverse()); // ["f","g","h","i","j"]
console.log(arr2); // ["f","g","h","i","j"]
```

### 1-4. concat

두 배열을 하나의 배열로 합쳐서 반환한다.

```js
const letters = arr.concat(arr2);

console.log(letters); // ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j"]
console.log([...arr, ...arr2]); // ["a", "b", "c", "d", "e", "f", "g", "h", "i", "j"]
```

### 1-5. join

배열의 요소들 사이에 구분자를 넣어 문자열로 만들고 반환한다.

```js
console.log(letters.join(" - ")); // a - b - c - d - e - f - g - h - i - j
```
