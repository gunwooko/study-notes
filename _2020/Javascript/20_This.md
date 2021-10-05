# Execution Context

`this`를 알아보기에 앞서, 자바스크립트 엔진에 코드를 실행하게 되면 어떤 일이 일어나는지 이해하는 것이 필요하다. 전역 영역에 코드를 작성되어 있을 때, 전역 메모리 테이블을 만들어서 저장한다. 메모리 상의 배열에 값이 담긴다. 그리고 자바스크립트에선 메모리 테이블이라 부르지 않고 **execution context (실행context)** 라 부른다. 전역 영역에 작성된 **global execution context**의 예를 들면:

```js
// Global memory 생성
var word = "hello";
function say(word) {
  return word + word;
}
```

| variable name |          value          |
| :-----------: | :---------------------: |
|     word      |         "hello"         |
|      say      | function say(word){...} |

그리고 함수 단위로 실행되는 영역에는 Local memory를 생성한다. 즉, local execution context가 생성된다. 한가지 중요한 사실은 execution context는 함수 scope 단위로 생성된다. Block scope에선 생성되지 않는다.

- Global execution context는 JS 엔진이 돌아갈 때 생성된다.
- Local execution context는 함수를 실행시에 생성된다.
- 어떤 함수가 호출되면, execution context가 만들어진다.
  -- call stack(메모리구조)에 push된다. (호출된 순서대로)
  -- 함수를 벗어나면 call stack에서 pop된다.
- 함수 scope 별로 생성된다.
- 그리고 함수 scope에 담기는 것은:
  -- scope 내 변수 및 함수(Local, Global)
  -- 전달 인자 (arguments)
  -- 호출된 근원 (caller)
  // 콘솔에 `arguments.callee.caller`를 사용해서 호출된 근원을 알 수도 있다.
  -- this

# `this` keyword

모든 함수 scope 내에서 자동으로 설정되는 특수한 식별자다. Execution context의 구성 요소 중 하나로, 함수가 실행되는 동안 이용할 수 있다. `this`를 알아볼 때 중요한 것은 여기에 어떤 값이 담기는지가 중요하다. 5가지 패턴이 있다.

# 5 Patterns of binding `this`

## 1. Global: window

콘솔창에 `this`를 치면 window가 나올 것이다.

## 2. Function invocation: window

함수를 실행했을 때 (호출했을 때) `this`는 window다. 또한 클로저함수로 작성하던지, 함수가 scope로 어려번 겹쳐있어도 `this`는 ()로 실행시키면 window다.

## 3. Method invocation: 부모 object

Method는 객체에 담긴 함수이다. Ex) obj.함수() 객체 안에 담긴 함수
Mothod 호출의 `this`는 바로 직계 부모가 담긴다. 다른 말로는, 함수가 실행되는 시점의 직계 부모가 담긴다.

- 사실 위의 2~3번은 같은 맥락이다. 위의 2번은 부모가 window이기 때문이다.

## 4. Construction mode (new 연산자로 생성된 function 영역의 this): 새로 생성된 객체

다른 말로 말하면, new키워드를 통해 만들어진 class의 instance가 `this`의 값이다. [더 자세한 내용은 객체지향으로 가보자](https://velog.io/@gunwooko/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5)

```js
function NewObject(name, food) {
  this.name = name;
  this.food = food;
  this.isWindow = function () {
    return this === window;
  };
}

const newObj = new NewObject("Sofi", "kimchi");
console.log(newObj.name); // Sofi
console.log(newObj.food); // kimchi
console.log(newObj.isWindow()); // false

const newObj2 = new NewObject("Martin", "bibimbab");
console.log(newObj2.name); // Martin
console.log(newObj2.food); // bibimbab
console.log(newObj2.isWindow()); // false
```

`newObj`와 `newObj2`의 경우 같은 생성자 함수로 만들어졌지만, 전혀 다른 객체이기 때문에 각 속성들은 서로 상관이 없다.

## 5. call or apply invocation: call, apply의 첫번째 인자로 명시된 객체

```js
foo(); // function invocation
window.foo(); // method invocation
foo.call(); // 함수이름.call(x) => x값을 this로 넘겨준다.
foo.apply(); // 함수이름.apply(x) => x값을 this로 넘겨준다.
```

이렇게 call()과 apply()를 사용할 수 있다. 여기서 call과 apply의 첫번째 arguments의 값은 무조건 `this`인데, 만일 `this`를 사용하지 않으면 `null`를 입력하고서 사용하면 된다. call과 apply의 차이점은 call에선 여러가지의 값을 쉼표로, apply에선 여러가지 값을 배열로 넘겨준다. 예를 들면:

```js
var sum = function (x, y) {
  this.val = x + y;
};
var obj = {
  val: 0,
};

sum.apply(obj, [3, 7]); // 배열로
console.log(obj.val); // 10

sum.call(obj, 3, 7); // 쉼표로
console.log(obj.val); // 10
```

```js
// this를 사용하지 않을 때
function sum(x, y) {
  return x + y;
}

sum.apply(null, [2, 8]); // 10
sum.call(null, 2, 8); // 10
```

그렇다면 언제 call 과 apply가 다른 점이 그렇게 많지 않은데 언제 apply를 사용하면 좋은지 예를 든다면:

```js
// arr의 값에서 가장 큰 값을 구하고 싶다면?
let arr = [1, 2, 3, 75, 84, 83, 5, 7, 8];

Math.max(arr); // NaN 이 나온다.

Math.max.apply(null, arr); // 84 가 잘 나오는 것을 볼 수 있다.
```

# 여러 문제로 알아보는 `this`

다음의 result 값은 무엇인가?

```js
var x = 10;
var strangeAdd = function (y) {
  var x = 20;
  return this.x + y;
};

result = strangeAdd(10);

// 답은 20 이다.
// 여기서 this가 가리키는 x는 전역에 선언된 x이기 때문이다.
// this는 함수가 실행될 때 실행되는 방식에 따라 결정된다.
// this 키워드는 호출된 함수가 실행할 때 가리키는 특정 객체이다.
```

```js
function foo() {
  console.log(this);
}

foo();

// 콘솔에는 전역객체가 찍힌다. (window or global object)
// function invocation 이기 때문이다.
```

```js
var obj = {
  foo: function () {
    console.log(this);
  },
};

obj.foo();
// 콘솔에는 obj가 찍힌다. ({foo: ƒ})
// method invocation 이기 때문이다.
```

```js
var obj = {
  foo: function () {
    console.log(this);
  },
};

var fn = obj.foo;
fn();
// 콘솔에는 전역객체가 찍힌다. obj가 찍힐 것 같았지만, 전역 객체인 이유는:
// this는 함수가 실행될 때 실행되는 방식에 따라 결정된다.
// function invocation 이기 때문이다.
```

```js
var obj = {
  foo: function () {
    console.log(this);
  },
};

var obj2 = {
  foo: obj.foo,
};

obj.foo.call(obj2);
// 콘솔에는 obj2가 찍힌다.
// call invocation 이기 때문인데, call()의 argument로 obj2가 들어갔기 때문이다.
```

# 참고

- [Poiemaweb - this](https://poiemaweb.com/js-this)
- [MDN - this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)
- [this 간략설명 youtube](https://www.youtube.com/watch?v=PAr92molMHU&t)
- [this 관련 블로그1](https://blueshw.github.io/2018/03/12/this/)
