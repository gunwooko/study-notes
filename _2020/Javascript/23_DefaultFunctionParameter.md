# 기본 매개변수(Default function parameter)

자바스크립트에서 함수의 매개변수는 `undefined`가 기본이다. 그러나 다른 기본값을 설정해주고 싶을 때, 기본 매개변수가 유용하다.

```js
function sum(a, b = 2) {
  return a + b;
}

sum(4); // 6 이 나온다. b = 2 가 기본이기 때문이다.
```

```js
function sum(a, b = 2) {
  return a + b;
}

sum(4, 6);
// 10 이 나온다. b는 2가 기본값이지만 6를 매개변수로 새롭게 넣어줬기 때문이다.
```

# 참고

- [MDN - 기본 매개변수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Default_parameters)
- [기본 매개변수 블로그1](https://appletree.or.kr/blog/web-development/javascript/javascript-function%EC%9D%98-default-parameters-%EC%84%A4%EC%A0%95-%EB%B2%95/)
