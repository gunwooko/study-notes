# 화살표 함수 표현 =>

화살표 함수는 `function` 키워드 대신 `=>` 화살표를 사용해서 보다 편하고 간략한 방법으로 함수를 선언할 수 있다. 그러나 모든 함수를 이렇게 선언할 수 있는 것은 아니다. 화살표 함수는 다음과 같이 사용된다.

```js
    () => {statements} // 매개변수가 없을 경우 빈 소괄호를 사용한다.
     x => {statements} // 매개변수가 한 개인 경우, 소괄호를 생략할 수 있다.
(x, y) => {statements} // 매개변수가 여러 개인 경우, 소괄호를 생략할 수 없다.


x => { return x * x } // 한 라인으로 표기할 수 이다.
x => x * x // 함수 몸체가 한 줄의 statement 라면 중괄호를 생략할 수 있고
           // 또한 `return` 키워드도 생략할 수 있으며, 암묵적으로 return된다.


() => { return { a: 1 }; }
() => ({ a: 1 }) // 위 표현과 동일하다. 객체 반환시 소괄호를 사용한다.


() => { // 여러 라인일 때.
  const x = 10;
  return x * x;
};


// Rest parameter와 Default parameter를 지원한다.
(param1, param2, ...rest) => {statements}
(param1 = defaultVal1, param2, …, paramN = defaultValN) => {statements}
```

## 화살표 함수와 함수 표현식

화살표 함수는 익명 함수로만 사용할 수 있기 때문에 화살표 함수를 호출하기 위해서는 함수 표현식을 사용한다. 또한 콜백 함수로 사용할 수 있다.

```js
let pow = function (x) {
  return x * x;
};
console.log(pow(5)); // 25
// 위의 함수 표현식을 화살표 함수로 다시 작성하게 되면 다음과 같다.
let pow = (x) => x * x;
console.log(pow(5)); // 25
```

```js
var arr = [1, 2, 3, 4];

let multiply2 = arr.map(function (x) {
  return x * 2;
}); // [2, 4, 6, 8]

// 위에 있는 함수를 화살표 함수를 이용해 아래와 같이 표현할 수 있다
let multiply2 = arr.map((x) => x * 2); // [2, 4, 6, 8]
```

# 화살표 함수와 `this`

일반 함수는 함수를 호출할 때 함수가 어떻게 호출되었는지에 따라 `this`에 바인딩할 객체가 동적으로 결정된다. 그러나 화살표 함수에서는 `this`는 언제나 상위 스코프의 `this`를 가리킨다. 이를 `lexical this`라고도 부른다. 렉시컬 스코프는 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정된다.
화살표 함수는 call, apply, bind 메소드를 사용하여 `this`를 변경할 수 없다. 또한 화살표 함수로 메소드를 정의하는 것을 피해야 하는데, 그 이유는 메소드로 정의한 화살표 함수의 내부의 `this`는 메소드를 소유한(호출한) 객체를 가리키지 않고, 상위 컨택스트인 전역 객체 `window`를 가리키기 때문이다.

```js
const saySomething = {
  firstTime: "Nice to meet you",
  sayHi: () => console.log(`Hi ${this.firstTime}`),
  // 여기서 this는 전역 객체를 가리킨다.
};

saySomething.sayHi(); // Hi undefined 가 출력된다.
```

위 문제의 해결을 위해 [ES6의 메소드 축약 표현](https://poiemaweb.com/es6-enhanced-object-property#3-%EB%A9%94%EC%86%8C%EB%93%9C-%EC%B6%95%EC%95%BD-%ED%91%9C%ED%98%84)을 사용하면 좋다.

```js
const saySomething = {
  firstTime: "Nice to meet you",
  sayHi() {
    // === sayHi: function() {
    console.log(`Hi ${this.firstTime}`);
  },
};

saySomething.sayHi(); // Hi Nice to meet you 가 출력된다.
```

[화살표 함수는 `this`의 컨택스트를 만들지 않는다.](https://dev.to/jishvi/comment/39bf)
[화살표 함수는 `this`의 값을 저장하지 않는다. 즉, `this`를 자체적으로 바인딩 하지 않는다.](https://stackoverflow.com/questions/50538608/where-is-an-arrow-function-execution-context)

# 참고

- [ES6 문법 관련 영상](https://www.inflearn.com/course/es6-%EA%B0%95%EC%A2%8C-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8/dashboard)
- [화살표 함수 정리](https://poiemaweb.com/es6-arrow-function)
- [ES6 문법 정리](https://jsdev.kr/t/es6/2944)
- [MDN 화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/%EC%95%A0%EB%A1%9C%EC%9A%B0_%ED%8E%91%EC%85%98)
