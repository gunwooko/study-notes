# Closure

클로져는** 외부 함수의 변수에 접근할 수 있는 내부 함수**를 의미한다. 또는, 이러한 작동 원리를 일컫는 용어이다. 자바스크립트의 가장 큰 장점 중 하나가 함수로 리턴할 수 있다.

```js
function outerFn() {
  let outerLet = "outer";
  console.log(outerLet);

  function innerFn() {
    // 여기에 있는 함수를 클로저 함수라 부른다.
    let innerLet = "inner";
    console.log(innerLet);
  }
  return innerFn;
}

let globalVar = "global";
```

클로저 함수 안에서는 지역 변수(innerLet), 외부 함수의 변수(outerLet), 전역변수(globalVar)의 접근이 전부 가능하다.

# 유용한 closure 예제

## 커링

함수 하나가 n개의 인자를 받는 대신, n개의 함수를 만들어 각각 인자를 받게 하는 방법.

```js
function adder(x) {
  return function (y) {
    return x + y;
  };
}

adder(2)(3); // 5

let add1000 = adder(1000); // x의 값을 고정해놓고 재사용할 수 있다.
add1000(2); // 1002
add1000(10); // 1010

let add7 = adder(7);
add7(2); // 9
```

즉, 외부함수의 변수가 저장되어서 보존되고, 내부함수의 인자를 변경하여 재사용 할 수 있는 템플릿 함수처럼 사용 할 수 있다.

## 클로저 모듈 패턴

변수를 스코프 안쪽에 가두어 함수 밖으로 노출 시키지 않는 방법. 외부에서 접근이 불가하기에 수정할 수 없다. 이것은 매우 유용하다.

```js
function makeCounter() {
  let privCounter = 0;

  return {
    // 객체와 같다.
    increment: function () {
      privCounter++;
    },
    decrement: function () {
      privCounter--;
    },
    getValue: function () {
      return privCounter;
    },
  };
}

let counter1 = makeCounter();
counter1.increment();
counter1.increment();
counter1.getValue(); // 2

let counter2 = makeCounter();
counter2.increment();
counter2.decrement();
counter2.increment();
counter2.getValue(); // 1
```

위의 예제에서 볼 수 있는 것처럼, 두 카운터에서 각기 다른 privCounter를 다루면서, privCounter를 밖으로 노출 시키지 않는다.
