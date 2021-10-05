# IIFE (Immediately Invoked Function Expression)

IIFE는 정의되자마자 즉시 실행되는 함수를 말한다. IIFE는 크게 두 부분으로 나뉜다.

```js
(function () {
  statements;
})();
```

- 첫 번째: 괄호로 둘러싸인 익명 함수, 이는 전역 스코프에 불필요한 변수를 추가해서 오염시키는 것을 방지한다. 또한 IIFE 내부 안으로 다른 변수들이 진입하는 것을 차단해준다. 또한 내부의 변수는 외부로부터 접근이 불가능하다. 익명 함수를 괄호로 감싸주어야 자바스크립트 코드를 해석하는 parser가 이것을 함수 표현식으로 인지할 수 있기 때문이다. 괄호로 안 묶어주고 실행되면 syntaxError가 발생한다.
- 두 번째: 즉시 실행 함수를 생성하는 괄호().

```js
(function () {
  let name = "Martin";
})(); // IIFE 내부에 정의된 변수는 외부에서 접근이 불가능하다.

name; // "Uncaught ReferenceError: name is not defined" 가 나온다.
```

## IIFE를 변수에 할당하면 함수가 실행된 결과만 저장된다.

```js
let result = (function () {
  let comment = "Hello!";
  return comment;
})(); // 즉시 결과를 실행한다.

result; // "Hello!"
```

## IIFE 대용

```js
{
  let comment2 = "Hi there!";
  console.log(comment2);
}

comment2; // "Uncaught ReferenceError: comment2 is not defined"
```

위와 같은 방법으로 IIFE 대신 사용할 수도 있겠다. 외부에서 또한 접근 불가능하다.

# 참고

- [MDN - IIFE](https://developer.mozilla.org/ko/docs/Glossary/IIFE)
- [IIFE 블로그1](http://chanlee.github.io/2014/01/11/understand-javascript-iife/)
- [IIFE 블로그2](https://velog.io/@doondoony/javascript-iife)
