> [비동기 호출](https://velog.io/@gunwooko/%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%98%B8%EC%B6%9C-Asynchronous-call) 관련해서 이전에 한번 글을 올린 적이 있는데, 콜백, 동기과 비동기, 비동기의 주요 사례에 관해 올렸다.

# Synchronous && Asynchronous

- 동기(Synchronous): 요청과 결과가 동시에 일어난다는 뜻이다.
- 비동기(Asynchronous): 요청과 그 결과가 동시에 일어나지 않는다는 뜻이다.

동기와 비동기는 처리해야 할 작업들을 어떤 흐름으로 처리할 것이냐에 대해 다룬다.

자바스크립트는 동기적이라고 말할 수 있는데, 호이스팅(hoisting)된 이후에 위에서 아래로 순차적으로 실행이 진행된다. 여기서 호이스팅이란, `var` 변수 선언, 혹은 `function declaration` 함수 선언들이 자동적으로 제일 위로 올라가는 것이다.

```js
// 동기적
console.log("첫번째");
console.log("두번째");
console.log("세번째");
// 위에서 아래로 순차적으로 실행된다.
```

```js
// 비동기적
console.log("첫번째");
setTimeout(() => {
  console.log("두번째"), 1000;
});
console.log("세번째");
// "첫번째" => "세번째" => "두번째" 순으로 실행된다.
// 항상 동기적으로 실행이 모두 이뤄진 이후에 비동기적 실행이 진행된다.
```

## Blocking && non-Blocking

블로킹과 넌블로킹은 처리해야 할 한 작업이, 전체적인 작업 흐름을 막냐 안막냐를 다룬다.

- Blocking: 호출된 함수가 자신의 일을 다 마칠 때까지 제어권을 계속 가지고서 호출한 함수에게 돌려주지 않는 것.
- non-Blocking: 호출된 함수가 자신의 일을 다 마치지 않았어도, 제어권을 건네주고서, 호출한 함수가 다른 일을 할 수 있도록 한 것.

보통 우리가 생각하는 비동기 함수란, 넌블로킹 방식으로 진행이 된다. 만일 비동기 적인 흐름에 블로킹 방식으로 일이 진행된다면, 결국 비동기적으로 일을 하고 싶더라도, 호출된 함수가 자신의 일을 다 마칠 때까지 기다려야하는 해프닝이 일어나게 될 것이다.
그러나 순차적으로 작업이 처리되어야 한다면, 동기적이거나 혹은 블로킹 방식으로 처리되야 할 것이다.

# 비동기와 콜백 (callback)

콜백 함수란, 다른 함수의 전달 인자로(argument) 넘겨주는 함수를 callback 함수라 부른다. 그리고 parameter로 callback 함수를 넘겨받는 함수는 필요에 따라 즉시 실행(synchronously)할 수도 있고, 아니면 나중에(asynchronously) 실행 할 수도 있다.

```js
// Sync callback
function printRightNow(print) {
  print();
}
printRightNow(() => console.log("hello world"));
```

```js
// Async callback
function printAfter(print, timeout) {
  setTimeout(print, timeout);
}
printAfter(() => console.log("print me after 3 sec!!"), 3000);
```

```js
// 또 다른 예
function printString(string) {
  setTimeout(() => {
    console.log(string);
  }, Math.floor(Math.random() * 1000) + 1);
}

const printAll = () => {
  printString("A");
  printString("B");
  printString("C");
};

printAll(); // 비동기로 처리된 함수의 리턴 순서는 그때마다 다르다...
```

## Callback Hell

콜백 지옥이 생기는 이유는, 위에서 본 예와 같이 비동기로 처리된 함수의 리턴 순서를 알 수가 없다. 그렇기에 콜백 함수의 인자로 또 콜백 함수를 넣어줌으로 비동기 함수의 결과 값을 예측할 수 있게 된다. 그러나 계속해서 이렇게 꼬리를 물게되면, 가독성도 떨어지고 에러가 발생할 경우 보수 또한 어려워진다.

```js
function printString(string, callback) {
  setTimeout(() => {
    console.log(string);
    callback();
  }, Math.floor(Math.random() * 1000) + 1);
}

const printAll = () => {
  printString("A", () => {
    printString("B", () => {
      printString("C", () => {});
    });
  });
};

printAll(); // A, B, C 차례로 반환된다.
```

# Promise

ES6에서 도입된, 비동기를 간편하게 처리할 수 있도록 도와주는 Object이다.
Promise 실행함수에는 두 개의 파라미터 `resolve`와 `reject`가 있다.

- resolve: 비동기 함수가 성공적으로 완료되었을 때
- reject: 비동기 함수의 처리가 실패했을 때

Promise에는 세가지 상태가 존재한다:

- 대기 (pending): 비동기 처리가 아직 수행되지 않은 상태 (resolve 또는 reject 함수가 아직 호출되지 않은 상태)
- 이행 (fulfilled / resolve): 연산을 성공적으로 완료함 (resolve 함수가 호출된 상태)
- 거부 (rejected / reject): 연산이 실패함 (reject 함수가 호출된 상태)

Promise에는 producer와 consumers가 존재하는데, producer에는 새로운 promise 객체를 생성하고, consumers에서는 그것을 사용한다.
Consumer 측에서는 Promise 객체의 후속 처리 메소드(`then`, `catch`)를 통해 비동기 처리 결과 또는 에러 메세지를 받아 처리한다. 에러 처리 방법에는 `catch`도 있지만, `then`의 두번째 인자로 에러를 처리할 수도 있다.

> then 메소드의 두 번째 콜백 함수는 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)만을 캐치한다. 하지만 catch 메소드는 비동기 처리에서 발생한 에러(reject 함수가 호출된 상태)뿐만 아니라 then 메소드 내부에서 발생한 에러도 캐치한다. 따라서 에러 처리는 catch 메소드를 사용하는 편이 보다 효율적이다.

- `then`: `resolve` 함수가 호출되면 실행, 새로운 Promise를 반환한다.
- `catch`: `reject` 함수가 호출되면 실행, 새로운 Promise를 반환한다.
- `finally`: Promise 처리가 완료되면 결과에 상관없이 지정된 콜백함수를 실행

```js
// Producer
// 한가지 알아야 할 것은 새로운 Promise가 만들어지면, 자동적으로 바로 실행이 된다.
const printStr = new Promise((resolve, reject) => {
  console.log("hello"); // 즉각 실행
});

const printString = (string) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log(string);
      resolve();
      // reject(new Error('wrong request!'))
    }, Math.floor(Math.random() * 1000) + 1);
  });
};

// Consumers: then, catch, finally
// Promise로 구현된 비동기 함수를 호출하는 곳이다.
const printAll = () => {
  printString("A")
    .then(() => {
      return printString("B");
    })
    .then(() => {
      return printString("C");
    })
    .catch((error) => {
      console.error(error);
    });
};

printAll();
```

또한 `then`이나 `catch` 메소드를 통해 Promise 객체를 반환하면 여러개의 Promise를 연결하여 사용할 수 있는데, 이것을 **Promise Chaining**이라고 부른다.

## Promise.all

`Promise.all` 메소드는 Promise 객체의 정적 메소드이다. Promise가 담겨있는 배열 등의 이터러블을 인자로 받는다.
반환 값으로는:

- 매개변수로 주어진 순회 가능한 객체가 비어 있으면 이미 이행한 Promise를 반환
- 객체에 Promise가 없으면, 비동기적으로 이행하는 Promise를 반환
- 객체에 Promise가 있으면, 대기 중인 Promise를 반환.

여기서 중요한 점은 모든 프로미스의 처리가 성공하면 각각의 프로미스가 resolve한 처리 결과를 배열에 담아 resolve하는 새로운 프로미스를 반환한다.

```js
Promise.all([
  new Promise((resolve) => setTimeout(() => resolve(1), 3000)),
  new Promise((resolve) => setTimeout(() => resolve(2), 2000)),
  new Promise((resolve) => setTimeout(() => resolve(3), 1000)),
])
  .then(console.log) // [ 1, 2, 3 ] 순서대로 배열에 담아서 반환.
  // 처리 순서가 보장된다.
  .catch(console.log);
```

만일 `Promise.all`의 두 개의 Promise 요청이 전달될 때, 만일 그 중 하나가 `rejected` 상태가 되는 경우, `then` 메서드가 아닌, `catch` 메서드를 따라간다. 즉, 배열 내 요소 중 하나라도 `reject`가 발생하면 `catch` 메서드를 따라간다. 또한 여러 프로미스가 실패한다 하면, 가장 먼저 실패한 프로미스가 reject한 에러가 `catch` 메소드로 전달되어 반환된다.

## Promise.race

`Promise.race` 메소드는 `Promise.all` 메소드와 동일하게 프로미스가 담겨 있는 배열 등의 이터러블을 인자로 전달 받는다. 그러나 다른점은 가장 먼저 처리된 프로미스가 resolve한 처리 결과를 resolve하는 새로운 프로미스를 반환한다. 처리가 실패했을 경우는 `Promise.all`과 같다.

# Async && await

`async` 함수는 Promise를 조금더 간편하게 사용할 수 있도록 해준다. `async` 키워드를 앞에 붙이는 함수는 항상 프로미스를 반환한다. 심지어 반환 값이 프로미스가 아니더라도, 자동으로 "이행상태"의 프로미스로(resolved promise) 감싸져서 반환된다. `await` 키워드는 `async` 함수 내에서만 사용할 수 있는데, 말 그대로 프로미스가 실행되어 (resolve or reject) 처리될 때까지 기다린다.

```js
async function test() {
  try {
    const response = await fetch("url...");
    // do something
  } catch (error) {
    // handle error
  }
}
```

```js
// example code
const printString = (string) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      console.log(string);
      resolve();
    }, Math.floor(Math.random() * 1000) + 1);
  });
};

const printAll = async () => {
  await printString("A");
  await printString("B");
  await printString("C");
};

printAll();
```

# 참고

- [동기와 비동기 관련 블로그 1](https://victorydntmd.tistory.com/8)
- [동기와 비동기 관련 블로그 2](https://siyoon210.tistory.com/147)
- [동기와 비동기 관련 블로그 3](https://musma.github.io/2019/04/17/blocking-and-synchronous.html)
- [동기와 비동기 관련 블로그 4](https://ahg223.com/classiccs/syncasync-nonblock/)
- [자바스크립트 비동기 처리 과정과 RxJS Scheduler](http://sculove.github.io/blog/2018/01/18/javascriptflow/)
- [자바스크립트와 이벤트 루프](https://meetup.toast.com/posts/89)
- [이벤트 루프 이해하기 영상 1](http://latentflip.com/loupe/?code=JC5vbignYnV0dG9uJywgJ2NsaWNrJywgZnVuY3Rpb24gb25DbGljaygpIHsKICAgIHNldFRpbWVvdXQoZnVuY3Rpb24gdGltZXIoKSB7CiAgICAgICAgY29uc29sZS5sb2coJ1lvdSBjbGlja2VkIHRoZSBidXR0b24hJyk7ICAgIAogICAgfSwgMjAwMCk7Cn0pOwoKY29uc29sZS5sb2coIkhpISIpOwoKc2V0VGltZW91dChmdW5jdGlvbiB0aW1lb3V0KCkgewogICAgY29uc29sZS5sb2coIkNsaWNrIHRoZSBidXR0b24hIik7Cn0sIDUwMDApOwoKY29uc29sZS5sb2coIldlbGNvbWUgdG8gbG91cGUuIik7!!!PGJ1dHRvbj5DbGljayBtZSE8L2J1dHRvbj4%3D)
- [프로미스 관련 영상 1](https://www.youtube.com/watch?v=JB_yU6Oe2eE&t=867s)
- [프로미스 관련 영상 2](https://www.youtube.com/watch?v=MBgGJSXg-dQ&t)
- [Poiema - 프로미스](https://poiemaweb.com/es6-promise)
- [프로미스 관련 블로그 1](https://medium.com/@kiwanjung/%EB%B2%88%EC%97%AD-async-await-%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0-%EC%A0%84%EC%97%90-promise%EB%A5%BC-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-955dbac2c4a4)
- [프로미스 관련 블로그 2](https://blueshw.github.io/2018/02/27/async-await/#settimeout)
- [MDN - Promise.all](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise/all)
- [Promise.all](https://attacomsian.com/blog/promise-all-javascript#)
- [Promise chaining](https://www.javascripttutorial.net/es6/promise-chaining/)
- [JS.info - Promise chaining](https://ko.javascript.info/promise-chaining)
- [Promise 실행순서 이해하기](https://g6ling.github.io/2016/11/18/dive-into-promise-chain/)
- [Promise hell](https://medium.com/sjk5766/promise-hell%EA%B3%BC-promise-chain-73a3349d7f01)
- [WebFundamentals - Promises](https://developers.google.com/web/fundamentals/primers/promises)
- [WebFundamentals - Async](https://developers.google.com/web/fundamentals/primers/async-functions)
- [JS.info - Async & await](https://javascript.info/async-await)
- [Promise와 async await의 활용 영상 1](https://www.youtube.com/watch?v=YJlGpxs72EQ)
- [async await 관련 영상 2](https://www.youtube.com/watch?v=aoQSOZfz3vQ&t=827s)
- [Advenced - Async JS](https://blog.bitsrc.io/understanding-asynchronous-javascript-the-event-loop-74cd408419ff)
