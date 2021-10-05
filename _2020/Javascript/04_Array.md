# 배열 (Array)

배열은 순서가 있는 값이다. 그리고 이 값을 요소(element)라고 부르고 그 순서를 인덱스(index)라고 부른다. 이 순서는 1이 아닌 0부터 시작한다.
배열은 대괄호(square bracket)를 이용해서 만들고 각각의 원소(element)는 쉼표로 구분해준다.
배열 값에 조회하려면 인덱스를 이용해 접근을 할 수 있다.

```js
let firstArray = [12, 13, 43, 64, 98];
// index:  0   1   2   3   4  순서가 되겠다.
firstArray[3]; // 64가 나오겠다.
```

만일 여기에 값을 변경하고 싶다면, 변수에 값을 할당하는 것과 같다.

```js
firstArray[3] = 777; // 등호(equal sign)를 사용해서 값을 변경한다.
// 변경 후 firstArray의 값을 불러오면 다음과 같다
firstArray; // [12, 13, 43, 777, 98];
```

만일 인덱스를 벗어나는 값을 부르게 되면 `undefined` 값이 나온다.

```js
firstArray[5]; // undefined
```

배열에선 중첩해서 사용이 가능한데 예를 들면 다음과 같다.

```js
let myFavorite = [
  ["strawberry", "orange"],
  ["coffee", "tea"],
  ["haribo", "timtom"],
];
myFavorite[1]; // ['coffee', 'tea'] 가 나온다.
```

여기서 배열 안의 배열의 인덱스 값을 불러오고 싶으면,

```js
myFavorite[1][0]; // 'coffee' 가 나온다.
```

## console.table()로 배열 시각화하기

`console.table()`를 사용하면 배열을 보기 좋게 테이블로 시각화하여 볼 수 있다.

```js
let arr = ["korea", "australia", "argentina"];

console.table(arr);
```

![](https://images.velog.io/images/gunwooko/post/94bf1f76-67f5-4962-b9c7-9e8609b6caaa/consoleTableExemple.png)

## 배열의 길이를 알아내기

```js
let firstArray = [12, 13, 43, 64, 98];
// 여기서 길이를 알아내려면
firstArray.length; // 5가 나온다.
```

여기서 온점(dot)을 사용해서 변수가 가지고 있는 속성(property)에 접근할 수 있다. 또한 온점(dot)을 사용해서 관련된 명령(method)도 실행할 수 있다. 명령을 실행할 때는, 함수를 실행하는 것과 같이 괄호를 열고 닫는 형태로 실행한다.

# 배열 다루기 (Array Methods)

## 배열 판별하기 Array.isArray()

매개변수로 들어갈 인자가 배열인지 아닌지를 판별하고, true 아니면 false를 반환한다.

## Element의 존재 여부 확인하기 1 indexOf()

매개변수로 찾고자 하는 요소가 들어간다. 배열 내에 요소의 최소 index값이 반환된다. 찾을 수 없다면 -1이 반환된다. 여기서 불리언 값으로 존재 여부를 확인하고 싶다면 다음과 같다.

```js
let fruits = ["apple", "grape", "orange"];

fruits.indexOf("apple"); // 0
fruits.indexOf("orange"); // 2

fruits.indexOf("pizza"); // -1
fruits.indexOf("pizza") !== -1; // false
```

위에서 본 것과 같이 `arr.indexOf(searchElement) !== -1`과 같은 방식으로 불리언 값으로 존재 여부를 확인할 수 있다.

## Element의 존재 여부 확인하기 2 includes()

`arr.includes()`메소드는 존재 여부를 확인하고서 불리언 값을 반환한다. 그러나 지원하지 않는 브라우저가 존재한다. (Internet Explorer)

## 배열에 Element 추가하기 1 .push()

```js
let firstArray = [12, 13, 43, 64, 98];
// firstArray라는 배열 끝에 100이라는 값을 추가하려면
firstArray.push(100);
firstArray; // [12, 13, 43, 64, 98, 100];
```

`.push()` 메소드는 배열의 끝에 하나 이상의 값을 추가한다. 그리고 배열의 새로운 길이를 반환한다.

## 배열에 Element 추가하기 2 .unshift()

`.unshift()` 메소드는 새로운 요소를 배열 맨 앞쪽에 추가하고, 새로운 길이를 반환한다.

## 배열에 Element 제거하기 1 .pop()

```js
let firstArray = [12, 13, 43, 64, 98];
// firstArray라는 배열 마지막 값을 삭제하려면
firstArray.pop();
firstArray; // [12, 13, 43, 64];
```

`.pop()` 메소드는 배열의 마지막 요소를 삭제하고 그 요소를 반환한다. 만일 빈 배열의 경우 `undefined`를 반환한다.

## 배열에 Element 제거하기 2 .shift()

`.shift()` 메소드는 배열의 첫번째 요소를 제거하고, 제거한 요소를 반환한다. 요소를 삭제하고 그 요소를 반환한다.

## 원본이 변하지 않는 새로운 배열 만들기 .slice()

앞서 말한 배열에 요소를 삭제하고 추가하는 방식은 원본 배열을 변화시킨다. 그렇다면 원본을 그대로 유지하고 싶으면 어떻게 할 수 있을까? 원본을 복사하고서 그 복사본에 수정을 진행하면 원본을 그대로 유지 시킬 수 있다. 그럴 때 원본 배열을 그대로 복사하는 메소드가 `.slice()`다.

```js
let arr = ["a", "b", "c"];

let newArr = arr.slice(); // newArr의 값은 arr와 같다.

newArr.push("k", "w"); // 새로운 배열의 길이 5가 리턴된다.

newArr; // ["a", "b", "c", "k", "w"] 된다.
```

만일 newArr 에서 부분적으로만 가지고 와서 복사하고 싶다면? `.slice(start, end)`를 사용하면 된다. start는 시작하는 index 값이고, end에 끝나는 index는 포함하지 않고서 복사를 한다.

```js
newArr.slice(2, 4); // ["c", "k"]가 반환된다.
```

## 배열에 Element 삭제, 교체, 추가하기 .splice()

`.splice()`메소드는 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경한다.
`array.splice(start[, deleteCount[, item1[, item2[, ...]]]])`

- start: 배열의 변경을 시작할 index 값이다. 배열의 길이보다 큰 값이라면 실제 시작 index는 배열의 길이로 설정된다. 음수인 경우 배열의 끝에서부터 시작한다.
- deleteCount: 제거할 요소의 수이다. 0을 입력하면 아무런 요소도 제거하지 않는다.
- item1, item2: 추가할 요소이다. 아무 값도 입력하지 않으면 제거만 하게 된다.

## 배열끼리 합치기 .concat()

인자로 주어진 배열이나 값들을 기존 배열에 합쳐서 새 배열을 반환한다.

- 기존배열을 변경하지 않는다.
- 추가된 새로운 배열을 반환한다.

`array.concat([value1[, value2[, ...[, valueN]]]])`

## .flat() 하위배열을 이어붙인 하나의 배열로

모든 하위 배열 요소를 지정한 깊이까지 재귀적으로 이어붙인 새로운 배열을 생성한다. `flat()`메소드는 열의 구멍도 제거한다.

```js
const arr6 = [1, 2, , 4, 5, 6];
arr6.flat();
// [1, 2, 4, 5, 6]
```

[MDN flat()함수 관련 설명](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/flat)

## .join() 배열을 문자열로

배열의 모든 요소를 연결해 하나의 문자열로 만든다. 만약 `arr.length` 가 0이라면, 빈 문자열을 반환한다.

## .sort() 배열 정렬하기

배열의 요소를 적절한 위치에 정렬한 후 그 배열을 반환한다. 원 배열에서 정리가 되지, 복사된 배열이 나오는 것이 아니다.
`arr.sort([compareFunction])`
'compareFunction'은 정렬 순서를 정의하는 함수이다. 생략하면 배열은 각 요소의 문자열 변환에 따라 각 문자의 유니코드 코드 포인트 값에 따라 정렬된다. 예를 들어 숫자 70은 9보다 크지만, 유니코드 코드포인트 값에 따르면 70이 앞으로 간다.

## .find() / .findIndex()

주어진 판별 함수를 만족하는 **첫 번째 요소의 값을 반환** (`.find()`)한다. 그런 요소가 없다면 undefined를 반환한다. `.findIndex()`는 **첫 번째 요소의 인덱스**를 반환한다.
`arr.find(callback[, thisArg])`

- callback: 배열의 각 값에 대해 실행할 함수. 아래의 세 인자를 받는다.
  -- element: 콜백함수에서 처리할 현재 요소.
  -- index (optional): 콜백함수에서 처리할 현재 요소의 인덱스.
  -- array (optional): find 함수를 호출한 배열.
- thisArg: 선택 항목. 콜백이 호출될 때 this로 사용할 객체.

# 배열로 함수형 프로그래밍

## .forEach()

주어진 함수를 배열 요소 각각에 대해 실행한다.
`arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])`

- callback: 각 요소에 대해 실행할 함수. 다음 세 가지 매개변수를 받는다.
  -- element: 처리할 현재 요소.
  -- index (optional):처리할 현재 요소의 인덱스.
  -- array (optional): `.forEach()`을 호출한 배열.
- thisArg (optional): callback을 실행할 때 this로 사용하는 값.

## .map() 배열의 형태 바꾸기

배열 내의 모든 요소 각각에 대하여 주어진 함수를 호출한 결과를 모아 새로운 배열을 반환한다. 여기선 인풋이 함수고 리턴 값은 새로운 배열인데, 형태는 다르지만, 원본 배열과 길이는 같다. `.map()` 메소드는 **IMMUTABLE** 하다.
`arr.map(callback(currentValue[, index[, array]])[, thisArg])`

- callback: 새로운 배열 요소를 생성하는 함수. 다음 세 가지 매개변수를 받는다.
  -- element: 처리할 현재 요소.
  -- index (optional):처리할 현재 요소의 인덱스.
  -- array (optional): `.map()`을 호출한 배열.
- thisArg (optional): callback을 실행할 때 this로 사용하는 값.

## .filter() 조건 따라 걸러내기

주어진 함수의 테스트를 통과하는 모든 요소를 모아 새로운 배열로 반환한다. `.filter()` 메소드를 사용하려면, 불리안 값이 나오는 함수를 만들어서, 첫번째 인자에 넣어야 한다.

`arr.filter(callback(element[, index[, array]])[, thisArg])`

- callback: 각 요소를 시험할 함수(불리안 값이 나오는 함수). true를 반환하면 요소를 유지하고, false를 반환하면 버린다. 다음 세 가지 매개변수를 받는다.
  -- element: 처리할 현재 요소.
  -- index (optional):처리할 현재 요소의 인덱스.
  -- array (optional): `.filter()`를 호출한 배열.
- thisArg (optional): callback을 실행할 때 this로 사용하는 값.

## .reduce()

배열의 각 요소에 대해 주어진 리듀서(reducer) 함수를 실행하고, 하나의 결과값을 반환한다. 즉, 여러 개의 값이 담긴 배열이 줄여서(reduce) 최종적으로 하나의 값을(배열에서 문자열로, 숫자로, 객체로) 만드는 과정이다. **.reduce()함수는 IMMUTABLE이다.** 여기서 배열을 하나의 값으로 만드는 함수를 reducer라고 한다. reducer가 callback 함수이다. reducer의 구성요소는 다음과 같다.

- 누적값(accumulator): 배열의 요소를 하나하나 줄여나가면서 중간 과정 (결과)
- 현재값(currentValue): 리듀서가 배열을 지나갈 때 만나는 배열의 요소
- 초기값(initialValue): 배열을 줄이기 전, 누적값의 초기 상태

`arr.reduce(callback[, initialValue])`
전달인자는 다음과 같다: reducer, initialValue.
reducer함수는 반드시 리턴 값이 필요하며, 다음번 reducer 호출시, 첫번째 파라미터로 전달된다.

리턴값은 reducer가 마지막으로 반환한 값이 되겠다.

reducer함수의 파라미터 순서는 다음과 같다.
순서대로 누적값(accumulator), 현재요소(value), 인덱스(index), 원본배열(array)순 이다.

[MDN reduce()함수 다시 보기](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

# 참고

- [MDN](https://developer.mozilla.org/)
- [ZeroCho - map, reduce](https://www.zerocho.com/category/JavaScript/post/5acafb05f24445001b8d796d)
