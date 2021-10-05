# Rest Parameter

Rest parameter는 매개변수 이름 앞에 세개의 점 `...`을 붙여서 정의한 매개변수를 의미한다.

```js
let arr = [1, 2, 3, 4, 5, 6];
let spread = [...arr];

console.log(spread); // [1, 2, 3, 4, 5, 6]
```

Rest parameter는 함수에 전달된 인수들의 목록을 배열로 전달받는다.

```js
function foo(...rest) {
  console.log(Array.isArray(rest)); // true
  console.log(rest); // [ 1, 2, 3, 4, 5 ]
}

foo(1, 2, 3, 4, 5);
```

또 다른 예제를 보자.

```js
let arr2 = ["hello", "world"];
let spread2 = [...arr, "hello", ...["hello", "world"]];

console.log(spread2); //[1, 2, 3, "hello", "hello", "world"]
```

ES6에서는 rest parameter를 사용하여 가변 인자(인자의 개수를 사전에 알 수 없는)의 목록을 배열로 전달받을 수 있다. 이를 통해 유사 배열인 `arguments` 객체를 배열로 변환하는 번거로움을 피할 수 있다. 허나 ES6의 화살표 함수에서는 함수 객체의 `arguments` 프로퍼티가 없음으로 가변 인자 함수를 구현해야 할 때는 반드시 rest parameter를 사용해야 한다. `arguments`란 모든 아규먼트를 유사배열 형태로 참조하는 값이다. 또한 rest parameter는 반드시 마지막 마지막 파라미터여야 한다.

# Spread Operator

Spread 연산자는 rest parameter와 같이 `...`을 사용해서 나타낸다. Spread 연산자는 대상을 개별 요소로 분리시키는데, 문법의 대상은 iterable 해야한다.

```js
// ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다.
console.log(...[1, 2, 3]); // 1, 2, 3

// 문자열은 이터러블이다.
console.log(..."genius"); // g e n i u s

// Map과 Set은 이터러블이다.
console.log(
  ...new Map([
    ["a", "1"],
    ["b", "2"],
  ])
); // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3])); // 1 2 3

// 이터러블이 아닌 일반 객체는 Spread 문법의 대상이 될 수 없다.
console.log(...{ a: 1, b: 2 });
// TypeError: Found non-callable @@iterator
```

ES6에선 spread 연산자를 사용하여 배열을 인수로 함수에 전달하면, 배열의 요소를 분해하여 순차적으로 파라미터에 할당한다.

```js
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}

// 배열을 foo 함수의 인자로 전달하려고 한다.
const arr = [1, 2, 3];

/* ...[1, 2, 3]는 [1, 2, 3]을 개별 요소로 분리한다(→ 1, 2, 3)
   spread 문법에 의해 분리된 배열의 요소는 
   개별적인 인자로서 각각의 매개변수에 전달된다. */
foo(...arr);
// 1
// 2
// 3
```

앞에서 보게된 rest parameter는 spread 문법을 사용하여 파라미터를 정의한 것을 의미한다. 형태가 동일하지만 다르다. Rest parameter는 반드시 마지막 파라미터이어야 하지만 Spread 문법을 사용한 인수는 자유롭게 사용할 수 있다.

```js
function foo(r, s, v, w, x, y, z) {
  console.log(r); // 1
  console.log(s); // 2
  console.log(v); // 3
  console.log(w); // 4
  console.log(x); // 5
  console.log(y); // 6
  console.log(z); // 7
}

// spread 문법에 의해 분리된 배열의 요소는 개별적인 인자로서 각각의 매개변수에 전달된다.
foo(1, 2, ...[3, 4, 5], 6, ...[7]);
```

또한 Spread 문법을 사용하면 배열 리터럴 만으로 기존 배열의 요소를 새로운 배열의 요소로 concatenate 할 수 있다.

```js
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ] 가 반환된다.
```

이 외에서 spread 문법을 사용하여, push, splice 등의 배열 메소드의 기능을 해낼 수 있다. 또한 spread 문법을 사용해서 간편하게 배열을 복사할 수 있다.

```js
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
const copy = [...arr];

console.log(copy); // [ 1, 2, 3 ]

copy.push(4);
console.log(copy); // [ 1, 2, 3, 4 ]

console.log(arr); // [ 1, 2, 3 ] 원본은 변경되지 않는다.
```

# 참고

- [Rest parameter / spread 연산자 블로그1](https://jeong-pro.tistory.com/117)
- [ES6 rest parameter / spread syntax](https://poiemaweb.com/es6-extended-parameter-handling)
