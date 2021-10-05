# 비동기 호출 (Asynchronous call)

자바스크립트 코드를 작성하다보면, 코드의 작동이 비동기로 이루어니는 경우가 대부분이라고 한다. 우선 비동기 호출을 알아보기전, callback 함수에 대해 먼저 알아보자.

## Callback

배열 메소드인 `map()`, `filter()`, `reduce()`, `forEach()` 등에서 callback 함수를 볼 수 있었다. 다른 함수의 전달 인자로(argument) 넘겨주는 함수를 callback 함수라 부른다. 그리고 parameter로 callback 함수를 넘겨받는 함수는 필요에 따라 즉시 실행(synchronously)할 수도 있고, 아니면 나중에(asynchronously) 실행 할 수도 있다. 또한 callback 함수가 사용되는 이벤트에 따른 함수(event handler)가 있다. Callback을 사용할 때 주의해야 할 점은, 함수 자체를 연결해줘야 하지 함수 실행을 연결하면 안된다. 함수 자체를 연결해주는 방법은: 함수명을 reference로 주던가, 새로운 익명 함수 안에서 callback을 실행시켜주던가, `bind()`를 사용해야 한다. 만일 함수 실행을 연결해주었을 때 `return` 값이 없으면, `undefined`이고, 그렇다면 `undefined`를 연결해준 거나 마찬가지이다.

## 동기와 비동기

- 동기 호출은 요청에 대한 결과가 즉각 동시에 일어나는 것과 같다. (synchronous)
- 비동기 호출은 요청에 대한 결과가 동시에 일어나지 않는다. (asynchronous)

동기와 비동기를 현실 세계에 비유하자면, 동기 호출의 경우는 중국집에 친구들 3명이 한 명씩 음식을 주문하는데, 주인아저씨가 친구1의 짜장면 주문을 받고서 바로 주방으로 들어가 먼저 짜장면 한 그릇 만들고, 그다음에 나와서 친구2의 짬뽕 주문을 받고서 바로 주방으로 들어가 짬뽕을 만들어서 나오고, 마지막으로 친구3의 볶음밥 주문을 받고서 다시 요리하러 주방으로 들어가는 순서가 되겠다. 이런 상황이 얼마나 비효율적인지 상상해보면 알 수 있다.(친구1은 이미 친구3이 요리 받기 전에 짜장면을 다 먹거나, 혹은 기다리느라 면이 다 불게 될 것이다. 반면에 비동기 호출은 친구1, 친구2, 친구3의 주문을 다 받고서 주방에 들어가 3개의 요리를 동시에 해서 나오게 된다.

## 비동기의 주요 사례

- DOM Element의 이벤트 핸들러 (마우스, 키보드 입력 (click, keydown 등) & 페이지로딩(DOMContentLoaded 등))
- 타이머 API (setTimeout 등) & 애니메이션 API (requestAnimationFrame)
- 서버에 자원 요청 및 응답 (fetch API (날씨API, 버스도착API 등 이미 작성되어 있는 서버 openAPI / 특정 서버에 URI로 요청하고 응답받기) & AJAX (XHR))

## Node.js는 어떻게 비동기 작업을 처리할까?

![](https://images.velog.io/images/gunwooko/post/037ef47d-2634-4d98-a114-3304759900c4/%EB%B9%84%EB%8F%99%EA%B8%B0.jpeg)

- Heap: 변수가 정의될 때 객체가 저장되는 장소(memory)이다.
- Call Stack: 스택에는 함수 호출이 쌓인다. 새로운 함수 호출이 발생하면, 해당 함수는 스택의 맨 위에 올라간다.
- Web api: JavaScript가 지원하지 않는, 조금 더 복잡한 작업(사용자 위치 파악, GeoLocation 등)을 할 수 있도록 브라우저가 제공하는 API다.
- Callback queue: 어떠한 이벤트가 발생했을 때, 실행되어야 할 콜백 함수들이 대기하는 곳입니다.
- Event loop: 콜 스택이 비어있는지 확인하고, 콜백 큐에서 대기 중인 작업을 실행시키는 역할을 담당한다.
- [Event-loop의 이해를 돕는 영상: Philip Roberts](https://vimeo.com/96425312)
- [EventLoop와 비동기 동작](https://velog.io/@wan088/JavaScript-EventLoop%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%8F%99%EC%9E%91)

## 공부해야 할 점:

- 동기적인 함수와 비동기적인 함수가 동시에 실행하게 되면, 동기적인 함수가 우선적으로 실행된다. 비동기 함수는 순서성이 보장되지 않는다고 할 수 있다.

# 참고

- [Event loop 관련 블로그](https://epthffh.tistory.com/?page=13)
- [MDN - 동시성 모델과 이벤트 루프](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)
- [Event-loop의 이해를 돕는 영상: Philip Roberts](https://vimeo.com/96425312)
- [EventLoop와 비동기 동작](https://velog.io/@wan088/JavaScript-EventLoop%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0-%EB%8F%99%EC%9E%91)
- [JavaScript Visualized: Event Loop](https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif)
- [JavaScript Visualized: Event Loop 번역](https://velog.io/@gtah2yk/-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%8B%9C%EA%B0%81%ED%99%94-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EB%A3%A8%ED%94%84-7yk5qv46ur)
