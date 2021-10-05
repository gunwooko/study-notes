# 타입 (Types)

변수에는 다양한 타입이 있다:

## - 숫자 number

## - 문자열 string

## - 불리언 boolean

논리적인 요소를 나타내고, `true`와 `false`의 두 가지 값을 가질 수 있다.

## - 배열 arrays

## - 객체 objects

## - 함수 function

## - Undefined

값을 할당하지 않는 변수는 `undefined` 값을 가진다.

## - Null

Null 타입은 딱 한 가지 값, `null`을 가질 수 있다. `null`은 자바스크립트의 원시 값 중 하나로, 어떤 값이 의도적으로 비어있음을 표현하며 불리언 연산에서는 false로 취급된다.

# 타입 알아내기 typeof 연산자

typeof 연산자는 피연산자 앞에 위치한다. `typeof operand`. 그리고 결과를 문자열로 반환한다.

```js
typeof 123; // 'number'
typeof "hello"; // 'string'
typeof true; // 'boolean'
typeof [1, 2, 3]; // 'object'
typeof { a: 1, b: 4 }; // 'object'
typeof function a() {}; // 'function'
typeof undefined; // 'undefined'
typeof null; // 'object'
typeof NaN; // 'number'
```

- 여기서 typeof 연산자로는 객체와 배열을 구분해내지 못하는 걸 알 수 있다. [배열 판별하기](https://velog.io/@gunwooko/%EB%B0%B0%EC%97%B4-Array).
