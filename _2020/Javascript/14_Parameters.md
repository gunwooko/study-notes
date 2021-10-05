# 매개변수

매개변수(parameter)란 함수의 정의에서 전달받은 인수를(전달인자) 함수 내부로 전달하기 위해 사용하는 변수를 의미한다. 인수(argument)란 함수가 호출될 때 함수로 값을 전달해주는 값을 말한다.

```js
function multiple(a, b) {
  // 2. 매개변수(parameters)를 통해 전달받은
  //    인자를 사용할 수 있다.
  let result = a * b;
  return result;
}

multiple(2, 3); // 1. 전달인자(arguments)와 함께 함수에 전달한다.
```

만일, 전달인자(arguments)의 길이가 유동적이라면?
보통 opcional한 parameter를 MDN에서 볼 수 있듯이 대괄호 [] 로 표시한다.

```js
function getMaxNum(...nums) {
  let result = Math.max(...nums);
  console.log(result);
}

getMaxNum(3, 4, 700, 5, 6, 7); // 700
```

위에서 볼 수 있듯이, 전달인자가 유동적이라면, rest parameter를 이용해 매개변수를 지정해준다. (ES6) 이렇게 하면 매개변수가 배열의 형태로 전달된다.

```js
function getMaxNum() {
  console.log(arguments);
  // arguments 라는 키워드를 이용할 수도 있다. {0:3, 1:4, 3:700, 4: 7}
  // 다만, 이 arguments객체는 배열같아 보이지만, 배열이 아니다.
  // 이를 유사배열이라 부른다. 이 말은 배열의 method를 사용할 수 없다는 말과 같다.
}
getMaxNum(3, 4, 700, 7); // {0:3, 1:4, 3:700, 4: 7}
```

매개변수에 기본값을 넣어주고 싶을 경우에는 Default Parameter를(ES6) 할당해 줄 수 있다. 문자열, 숫자, 객체 등 어떠한 타입도 가능하다.

```js
function getRoute(destination, departure = "SYD") {
  // departure부분이 기본값으로 들어갔다.
  return "출발지: " + departure + ", " + "도착지: " + destination;
}

getRoute("INC"); // "출발지: SYD, 도착지: INC"
```

만일 반대로 하게되면

```js
function getRoute(departure = "SYD", destination) {
  // departure부분이 기본값으로 들어갔다.
  return "출발지: " + departure + ", " + "도착지: " + destination;
}
// 중간에 기본 매개변수가 들어가는 경우, undefined로 넣어줄 때 기본값으로 처리한다.
getRoute(undefined, "INC"); // "출발지: SYD, 도착지: INC"
```

> 기본 함수 매개변수(default function parameter)를 사용하면 값이 없거나 undefined가 전달될 경우 매개변수를 기본값으로 초기화할 수 있습니다.

# 참고

- [MDN 기본 매개변수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Default_parameters#%EC%84%A4%EB%AA%85)
