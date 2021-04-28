# JavaScript Fundamentals - Part 1.

## 1. Value(값).

Value란 기본적으로 Data이며 프로그래밍에서 가장 기본적인 정보 단위이다.

<br/>

### 1-1. Type.

JavaScript는 동적타입 언어로, 런타임에 변수에 할당되는 값에 따른 동적타이핑을 수행하기 때문에 변수 키워드를 사용할 뿐 타입을 직접 지정하지는 않는다.

<br/>

#### 1-1-1 PRIMITIVE.

- Number : 부동 소수점 수. 정수, 실수를 포괄함. ( ex. 23, 30.2 )

- String : 문자열. ( ex. 'Jonas' )

- Boolean : 값이 오직 참 또는 거짓인 논리적인 타입. ( true, false )

- Undefined : 정의되지 않은 변수에 JavaScript 엔진이 자동으로 부여하는 값. 값과 타입 모두 Undefine으로 동일.

- Null : 명시적으로 '비어있음'을 나타내는데 사용하는 값. undefine과 유사하나 자동으로 부여가 되는것이 아닌 주로 의도를 지니고 부여하는 값이라는 것에 차이가 있다. null의 타입을 실제로 확인해보면 object로 나타나는데 이는 JavaScript의 오류,버그로 간주된다.

- Symbol : 고유하며 변경할 수 없는 값.

- BigInt : Number 타입이 가질 수 있는 수보다 큰 값의 정수.

<br/>

#### 1-1-2. OBJECT.

<br/>

## 2. Variable(변수).

Value와 같은 Data를 저장할 수 있는 공간. Data의 재사용을 가능하게 해준다.

<br/>

### 2-1. JavaScript 변수의 키워드.

es6에서 등장한 let, const와 그 이전부터 사용되어 온 var가 있다.
키워드를 사용하지 않은 변수는 전역변수가 된다.

- var : function-scoped. 재선언,재할당이 가능한 변수.

- let : block-scoped. 재선언 불가능,재할당은 가능한 변수. 값을 비운 상태로 선언 가능.

- const : 재선언,재할당이 모두 불가능한 변수. 값을 비운 상태로 선언 불가능.

변수의 값이 변경될 필요가 없다면 꼭 const를 사용하고 그외에는 let을 사용하는 것을 권장.

<br/>

### 2-2. 변수의 선언.

아래와 같이 변수를 선언하면 컴퓨터 메모리에 좌항의 변수가 생성되며 우항의 값이 변수에 저장된다.
(변수명은 camelCase를 따르도록 한다.)

```js
let firstName = "Jonas";
```

<br/>

### 2-3. 변수의 사용.

변수는 변수명으로 호출하여 사용한다.

```js
console.log(firstName);
```

## 3. Operator(연산자).

연산자는 값을 이용한 연산에 사용되는 기호이다.

<br/>

### 3-1. Mathematical Operators.

+, -, \*, ++, -- 등이 있음.

- **로 제곱을 수행할 수 있다.(ex. 2 ** 3 = 8)

<br/>

### 3-2. Assignment Operators.

=, +=, -=, \*= 등이 있음.

<br/>

### 3-3. Unary Operators.

!, +, -, ++, --, typeof 등이 있음.

- 단항 연산자로서의 +,- 는 피연산자를 숫자로 변환하며, -는 변환 후 변환된 숫자의 부호를 바꾼다.

<br/>

### 3-4. Comparison Operators.

\>, <, <=, >=, ==, ===, !=, !== 등이 있다.

<br/>

### 3-5. Logical Operators.

&&, ||, !가 있다.

<br/>

### 3-6. Operator Precedence

연산자들 사이에는 우선순위가 존재한다.
아래 링크를 참조.
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Operator_Precedence

<br/>

## 4. Strings and Template Literals

### 4-1. Template Literals

es6부터 도입된 문자열 표기법. 기본적으로 ``(backtick)을 사용하고 변수 또는 표현식은 ${}안에 작성하며 ""와 ''도 혼용 가능하다.

```js
const jonasNew = `I'm ${firstName}, a ${year - birthYear} years old ${job}!`;
```

<br/>

## 5. If/else

기본적으로 기존에 알고있는 if/else와 동일. 조건식에 boolean이 아닌 표현식이 기입되면 type coercion을 통해 boolean으로 형변환된다.

<br/>

## 6. Type Conversion and Coercion

자바스크립트에는 Type Conversion과 Type Coertion이 있다.

Type Conversion은 수동으로 타입을 변환하는 것이고 Type Coertion은 자바스크립트가 자동으로 타입을 변환하는 것이다.

### 6-1. Type Conversion

- Number() : 값의 타입을 숫자타입으로 변환하는 Function. 수가 아닌 문자열에 해당 함수를 사용하면 NaN (Not a Number)을 반환. (NaN의 타입은 Number이다. 즉, NaN은 잘못된 숫자를 의미한다.)

- String() : 값의 타입을 문자열 타입으로 변환하는 Function.

- Boolean() : 값의 타입을 Boolean 타입으로 변환하는 Function.

```js
//type conversion
const inputYear = "1991";

console.log(Number(inputYear)); // 1991
console.log(Number("Jonas")); // NaN
console.log(typeof NaN); // Number
console.log(String(23)); // "23"
console.log(Boolean(0)); // false
```

### 6-2. Type Coercion

자바스크립트는 서로 다른 타입의 값으로 연산을 수행할때 한쪽 값의 타입을 나머지 다른값의 타입과 일치하도록 자동으로 형 변환을 수행한다.

ex.

- 문자열 + 값 => 문자열

- 문자열 - 값 => 숫자

- etc...

```js
//type coercion
console.log("I am " + 26 + " years old"); // "I am 26 years old"
console.log("23" - 10); // 13
console.log("23" / 2); // 11.5
console.log("23" > 18); // true
```

## 7. Truthy and Falsy Value

### 7-1. Falsy value

falsy value는 정확히 false는 아니지만 boolean으로 형변환을 거치면 false가 되는 값이다. 아래의 다섯가지 값에 해당한다.

- 0

- ''

- undefined

- null

- NaN

### 7-2. Truthy value

falsy value가 아닌 값은 모두 truthy value에 해당하며 boolean으로 형변환을 거치면 true가 된다.

### Ex.

```js
console.log(Boolean(0)); //false
console.log(Boolean(undefined)); //false
console.log(Boolean("Jonas")); //true
console.log(Boolean({})); //true
console.log(Boolean("")); //false
```

```js
let height;

if (height) {
  console.log("YAY! height is defined!");
} else {
  //excute
  console.log("Height is UNDEFINED");
}
```

## 8. equality operator.

==,===

### 8-1. strict equality operator.(===,!==)

말 그대로 엄격하다. 값 뿐만 아니라 타입까지 비교한다.

<br/>

### 8-2. loose equality operator.(==,!=)

===와 달리 Type Coercion을 수행하여 값만 비교한다.

```js
console.log(18 === "18"); //false
console.log(18 == "18"); //true
```

가능한 한 === 사용을 권장한다.

<br/>

## 9. Statements and Expressions

### 9-1. Expression(표현식)

Expression은 값을 만들어내는 코드조각을 의미.

```js
3 + 4; //expression
1991; //expression
true && false && !false; //expression
```

### 9-2. Statement(문장)

Statement는 값을 만들어내지 않고 Action을 나타내는 코드를 의미한다. 하나의 완성된 문장이라고 생각하면 된다.

```js
if (23 > 30) {
  //여기서 "23 is bigger"는 expression
  const str = "23 is bigger";
} // if statement
```

### 9-3. 정리

표현식은 문장의 부분이 될 수 있지만 문장은 표현식의 부분이 될 수 없다. 표현식을 문장을 완성하기 위한 하나의 단어라고 생각할 수 있다.

## 10. Conditional Operator(삼항 연산자)

(조건이 되는 표현식)?(조건이 참일때 반환될 표현식):(조건이 거짓일때 반환될 표현식)

예시

```js
const age = 19;
const drink = age >= 18 ? "beer 🍺" : "water 💧";
console.log(drink); // beer 🍺
```

표현식으로써 if/else 문장의 기능을 수행할 수 있다.

```js
const age = 19;
console.log(`I like to drink ${age >= 18 ? "beer 🍺" : "water 💧"}`); // I like to drink beer 🍺
```

조건에 따라 변수에 값을 할당하는 등 간단한 코드에 사용하는 것을 권장.
