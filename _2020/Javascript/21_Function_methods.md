# 함수 메소드 (Function Methods)

함수를 실행하는 다양한 방법이 존재한다.

- Function(method) 호출
- new 키워드를 이용한 호출
- 함수 메소드 call, apply, bind를 이용

이전 [this](https://velog.io/@gunwooko/this)를 배울 때 call과 apply 사용 방법과 차이점을 알아보았다. 여기서는 bind를 알아보겠다.

## bind

call과 apply와는 다르게, 함수를 바로 실행시키지 않고, this 값이 바인딩 된(묶인) 함수를 반환한다.

```js
function sum(x, y) {
  this.val = x + y;
  console.log(this.val);
}

let obj = { val: 0 };

let boundFn = sum.bind(obj, 3, 7);
// boundFn은 함수이다. 인자순서는 call과 같다.
boundFn(); // 10, sum은 여기서 실행된다.
// 보기에는 functoin invocation처럼 보이지만,
// 여기엔 this 값이 이미 바인딩되어 있다.
// bind는 함수를 실행하지 않고, 함수 자체를 리턴한다.
```

- 이외에도 `bind`를 사용해서 `setTimeout`을 `this`와 사용 시에 `this` 값이 `window` 객체로 변경되는 것에 대한 문제를 해결하며 사용할 수 있다. 이때 `setTimeout` 에는 함수를 인자로 넘겨야 하고(함수 실행을 넘기는 것이 아니다), `this` 값이 `window`로 들어가지 않도록 명시적으로 `this` 값을 인스턴스로 만들어 지정해줘야 한다.
- 또한 bind로 커링을 구현할 수 있다.

```js
function template(clientName, points) {
  return "<h1>" + clientName + "</h1><span>" + points + "</span>";
}

let templSofia = template.bind(null, "Sofia");
// templSofia 는 함수이다.
// 위에 같이 해주면, Sofia는 지정된 값이 된다.
templeSofia(20000);
// "<h1>Sofia</h1><span>20000</span>"
templeSofia(1);
// "<h1>Sofia</h1><span>1</span>"

let templManuel = template.bind(null, "Manuel");
templManuel(500);
// "<h1>Manuel</h1><span>500</span>"
```

## call과 apply로 prototype 기능 빌려쓰기

```js
// 예를 들어 이런 함수가 있다고 했을 때,
function moreThanTree(str) {
  return str.length > 3;
}

let arr = ["hello", "world", "sky", "ant"];

arr.filter(moreThanTree); // ["hello", "world"] 이렇게 반환할 수 있지만,
// filter와 arr의 위치를 바꿔서 해보고 싶을땐,
Array.prototype.filter.call(arr, moreThanTree); // ["hello", "world"]
Array.prototype.filter.apply(arr, [moreThanTree]); // ["hello", "world"]
// 이와 같은 방식으로도 가능하다.
```

위의 예시와 같은 방법이 유용하게 쓰일 수 있는 경우는, `querySelectorAll` 등을 사용해서 `element` 값을 모두 가져왔을 데 반환되는 값은 `NodeList`인데, 이는 유사 배열이다. `length`가 있고 뭔가 배열 메소드를 사용할 수 있을 것처럼 보이지만, 사용할 수 없고 Array.isArray로 확인했을 때에 false를 반환한다. 여기서 배열의 메소드를 사용하고 싶다면, 위의 방법으로 배열의 메소드 기능을 빌려와 사용할 수 있다.

```js
function getElementId(element) {
  return element.id;
}

Array.prototype.map.call(유사배열, getElementId);
// this 값으로 유사배열을 넣어서 배열 메소드의 기능을 빌려와 사용
```

# 참고

- [MDN setTimeout `this` 문제](https://developer.mozilla.org/ko/docs/Web/API/WindowTimers/setTimeout)
