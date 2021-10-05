# Scope

Scope는 변수 접근 규칙에 따른 유효 범위이다. 변수와 그 값이 어디서부터 어디까지가 유효한지 판단하는 범위이다. 자바스크립트에선 함수가 선언되는(lexical) 동시에 자신만의 scope를 가진다.

#### Lexical scope vs Dynamic scope

- Lexical scope는 코드를 작성할 때 유효 범위가 결정된다.
- Dynamic scope는 함수가 실행될 때 결정된다. (`this` - execution context)

```js
let hello = "hello";

function toSomeone() {
  let who = "Martin";

  return hello + " " + who;
}

console.log(toSomeone()); // hello Martin"
console.log(who); // ReferenceError
```

ReferenceError가 발생하는 이유는 변수 who는 toSomeone() 함수 안에서만 적용이 되기 때문이다. 즉, 함수 안의 범위에서만 사용할 수 있기 때문이다. 이를 Local Scope라고 부른다. 자바스크립트에선 기본적으로 함수가 선언되는 동시에 자신만의 scope를 가지게 되는데, 이 local scope 안쪽에 선언된 변수는 밖에서 사용이 불가능하다. Scope는 변수와 그 값이 어디서부터 어디까지 유효한지를 판단하는 범위가 되겠다. Scope에는 다양한 규칙들이 있다.

## 1. Local scope와 global scope의 차이

```js
let hello = "hello"; // global scope에서 정의된 변수 = 전역 변수

function toSomeone() {
  let who = "Martin"; // local scope에서 정의된 변수 = 지역 변수

  return hello + " " + who;
}

console.log(toSomeone()); // hello Martin"
console.log(who); // ReferenceError 바깥쪽에서 함수 안에 정의된 변수를 가져올 수 없다.
```

위의 결과로 알 수 있는 사실은 **scope는 중첩이 가능**하다. 함수 안에 함수를 넣을 수 있는 것과 같다. Global scope는 최상단의 scope로, 전역 변수는 어디서든 접근이 가능하다. 즉, 위에서 보는 것과 같이, 안쪽 scope에서 바깥/함수에 접근하는 것은 가능하지만, 바깥쪽 scope에서 안쪽 변수/함수에 접근하는 것은 불가능하다. 또한 지역 변수는 함수 내에서 전역 변수보다 더 높은 우선순위를 가진다.

## 2. Function scope와 block scope의 차이

Block scope는 중괄호로 시작하고, 끝나는 단위를 부른다.

```js
for (let i = 0; i < 5; i++) {
  console.log(i); // 0 부터 4까지 반복된다.
}
console.log(i); // ReferenceError
```

ReferenceError가 나오는 이유는 변수 i는 block scope 안에서만 사용할 수 있기 때문이다.

```js
for (var i = 0; i < 5; i++) {
  // 변수키워드 var를 사용해서 지정
  console.log(i); // 0 부터 4까지 반복된다.
}
console.log(i); // 5가 나온다
```

그 이유는 `var`는 block scope가 아닌 function scope의 유효범위를 가지고 있기 때문이다.
변수를 선언할 때 `var`보다 `let`를 추천하는 이유는 block 범위를 벗어나도 (같은 function scope에서는) 사용이 가능한 `var`은 예상할 수 없는 위험이 있기때문에 block scope로 예측하기 쉬운 `let` 키워드를 사용하기를 추천한다.

또 다른 변수를 선언하는 키워드로 `const`가 있다. 주로 값이 변하지 않는 변수, 상수를 정의할 때 사용하는 키워드이다. `let`과 동일하게 block scope를 따르고, 값을 재정의하려고 하면 `TypeError`를 낸다. 값을 변형시키고 싶지 않을 때 `const`를 사용할 수 있다.

```js
console.log(a); // undefined
var a = "hello";

console.log(b); // ReferenceError: b is not defined
let b = "world";
```

### let, const, var

|             |     let     |    const    |      var       |
| :---------: | :---------: | :---------: | :------------: |
|  유효범위   | block scope | block scope | function scope |
| 값의 재정의 |    가능     |   불가능    |      가능      |
|   재선언    |   불가능    |   불가능    |      가능      |

let이나 const에 다시 선언할 경우 `Syntax Error: Identifier "이름" has already been declared.`가 나온다.
가능한 재선언을 안하는게 좋다. 실제 코딩을 하면서 재선언을 할 필요는 없다, 만일 한다면 그 이유는 전에 선언했다는 사실을 깜박하거나 실수이다. 즉, 버그이다. `var`로 선언을 할 경우 재선언이 가능해지기 때문에 또한 되도록 `var`를 사용하지 않는 게 좋다. `let` 키워드는 이러한 실수를 막아준다.

## 3. 전역 변수와 window 객체

`window` 객체는 전역 범위를 대표하는 객체이다. 즉, global scope에서 선언된 함수, 그리고 var 키워드를 이용해 선언된 변수는 window 객체와 연결되어 있다.

```js
var name = "Sofia"; // 함수의 외부에서 선언된 모든 변수는 전역 범위이다.
console.log(window.name); // Sofia
```

되도록 전역 범위에 너무 많은 변수를 선언하지 않는 게 좋다. 최상의 scope이기 때문에 변수 이름이 겹칠 수 있다. 그렇기에 {} 중괄호 안에 let 키워드를 사용해서 변수를 지정하자. `{ let ...... }`

#### node.js에서는 global이 전역 객체이다.

## 4. 선언 없이 초기화된 전역 변수

절대로, 선언 키워드 없이 변수를 초기화하지 말자.

```js
function showMe() {
  age = 70; // 여기서 age는 전역 변수로 취급된다. 즉, age === window.age 같다.
  console.log(age);
}
showMe(); // 70
console.log(age); // 70
```

여기서 버그로 내보내지 않아서, 에러로 뜨지 않아 위험하다.
이런 실수를 방지하고 싶을 경우, Strict Mode를 사용할 수 있다. 문법적으로 실수할 수 있는 부분들을 에러로 판단한다. (콘솔에선 사용할 수 없다. 파일에 저장 후 사용)

```js
"use strict"; // js파일 상단에 문자열로 넣어준다.

function showMe() {
  age = 70; // ReferenceError가 나온다.
  console.log(age);
}
showMe();
console.log(age);
```

## 5. Hoisting

선언된 변수 및 함수를 scope의 상단으로 끌어올리는(hoist) 것을 말한다. 변수 선언은 범위에 따라 선언과 할당으로 분리된다. 함수 내에서 선언한 function scope의 변수는 해당 함수의 최상위로 가고, 함수 밖에서 선언한 global scope의 전역변수는 유효 범위(스크립트 단위)의 최상단에 선언된다.  
중요한 점은 **`var` 변수 선언**과 **함수선언문**에서만 호이스팅이 일어난다. 그리고 `var` 변수-함수의 선언만 위로 끌어올려지며, 할당은 끌어 올려지지 않고 제자리 있는다. (실제로 코드가 움직이는 것이 아닌, 자바스크립트 내부적으로 끌어올려서 처리하는 것이다.)
`let`, `const` 변수 선언과 함수표현식에서는 호이스팅이 발생하지 않는다.

항상 코드를 작성할 때 scope를 생각해서 작성하는 것이 좋다. `var` 변수 선언을 사용하게 될 경우 호이스팅, 재할당, scope의 예측이 복잡하기에, 되도록 `let`과 `const`로 변수 선언하는 것이 좋다.

# 참고

- [호이스팅 관련 블로그1](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html)
- [호이스팅 관련 블로그2](https://ojava.tistory.com/144)
- [scope 관련 영상 및 설명](https://www.yalco.kr/27_scope/)
