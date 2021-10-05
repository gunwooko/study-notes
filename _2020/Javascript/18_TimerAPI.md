# 타이머 API

## setTimeout(callback, millisecond)

일정 시간 후에 함수를 실행한다.

- Arguments: 실행할 함수(callback 함수) / callback 함수 실행 전 기다려야 할 시간
- Return value: 임의의 타이머ID
- clearTimeout으로 취소할 수 있다.

### Example

```js
console.log(1);
setTimeout(function () {
  console.log(2);
}, 1000);
console.log(3);

// 1
// 3
// 2 순으로 호출된다.
```

```js
console.log(1);
setTimeout(function () {
  console.log(2);
}, 1000);
setTimeout(function () {
  console.log(3);
}, 0);
console.log(4);

// 1
// 4
// 3
// 2 순으로 호출된다.
```

첫번째 예는 예상이 가능했지만, 두번째 예시에선 1, 3, 4, 2 혹은 1, 3, 2, 4 순으로 호출될 줄 알았다. 그러나 1, 4, 3, 2 순으로 호출된 이유는 먼저 동기적 코드가 우선으로 실행되고, 비동기적 코드가 나중에 호출되기 때문이다. 즉, 동기적인 함수와 비동기적인 함수가 동시에 실행하게되면, 동기적인 함수가 우선적으로 실행된다. 비동기적인 함수는 순서성이 보장되지 않는다.

## setInterval(callback,millisecond)

일정 시간의 간격을 가지고 함수를 반복적으로 실행한다.

- Arguments: 실행할 함수(callback 함수) / callback 함수를 반복적으로 실행시키기 위한 시간 간격
- Return value: 임의의 타이머ID

## clearInterval(timerId)

반복 실행중인 타이머를 종료한다.

- Arguments: 타이머ID
- Return value: 없음
- 또한 setInterval()함수를 변수에 담아 변수를 arguments에 넣어줄 수 있다.
