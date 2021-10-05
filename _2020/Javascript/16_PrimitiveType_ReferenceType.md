# Primitive type (원시값)

자바스크립트의 데이터 타입중 하나인 primitive type (기본형 혹은 원시타입)에는 숫자, 문자열, 불리언, null, undefined 등이 있다.
원시값은 명시적인 값이다. 그 자체로 명시적이고 변형하지 않는 값이기에, `===`등을 사용할 수 있다.

```js
let x = 2;
let y = x;
y = 3
x ? // 2가 된다.
```

위의 예를 보면 변수 x에 2를 할당하고 변수 y에는 변수 x를 할당했다. 그다음 y에 다시 3을 할당했을 때, x의 값은 3이 아닌 2임을 볼 수 있다. 여기서 우리는 원시값 자체와 원시값을 할당한 변수를 혼동하면 안된다. x에는 2가 이미 할당됬음으로 그 값은 변하지 않고, 처음에 y에 할당한것은 x에 할당된 2였기 때문이다.

```js
let x = 2;
let y = x; // 여기는 y = 2 인 것이다.
y = 3
x ?// 2가 된다.
```

# Reference type (참조타입)

Reference type에는 객체, 배열, 함수 등이 있다.

```js
let x = { count: 100};
let y = x;
x.count=9999;
y.count ? // 9999가 된다.
```

여기서 x와 y는 같은 참조를 담고 있다. 즉, 동일한 객체를 가리킨다. 여기서 확실히 알 수 있는 사실은 객체타입에 할당되는 값은 실제 객체가 아닌 객체를 가리키는 주소값이다.

```js
let q = { name: "Martin" };
let w = q; // 같은 주소값을 가리킨다.
console.log(w); // { name: 'Martin'};
console.log(q); // { name: 'Martin'};
// 그렇기에 w 나 q 둘 중 하나라고 값을 변경시키면
// 같은 주소값을 가리키기에 둘다 동시에 값이 변경되는 것이다.

// 그런데 만일 이렇게 한다면?
q = { name: "Gabriel" };
// w의 값은 어떨까?
console.log(w); // { name: 'Martin'}; 가 나온다.
console.log(q); // { name: 'Gabriel'}; 이 나온다.
```

그 이유는 변수가 재할당 되었기 때문이다. 변수에 재할당을 하면서, 변수 `q`가 가리키는 주소값이 변경되었기 때문이다.

# 참고

- [MDN 원시값](https://developer.mozilla.org/ko/docs/Glossary/Primitive)
- [What are Primitive and Reference Types in JavaScript?](https://itnext.io/javascript-interview-prep-primitive-vs-reference-types-62eef165bec8)
- [Call by value와 참조타입의 재할당, 참조 성질](https://blueshw.github.io/2018/09/15/pass-by-reference/)
- [JavaScript Primitive vs. Reference Values](https://www.javascripttutorial.net/javascript-primitive-vs-reference-values/)
- [데이터타입](https://code-masterjung.tistory.com/32)
- [데이터 타입 알아보기](https://velog.io/@pa324/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%83%80%EC%9E%85-vpk356f07y)
