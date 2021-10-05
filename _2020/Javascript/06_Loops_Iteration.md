# 반복문(Loops and iteration)

반복문은 같거나 비슷한 코드를 여러 번 실행시켜야 할 경우에 쓰는 구문이다. 반복문에는 반복할 내용과 반복할 조건을 코드로 작성해야 한다. 여기선 자바스크립트가 지원하는 반복문 중 `for`과 `while`를 살펴볼 것이다.

## `for` 구문 (`for` statement)

for 반복문은 어떤 특정한 조건이(조건문) 거짓으로 판별될 때까지 반복한다.

```js
let sum = 1;
// 반복할 조건을 소괄호 안에 초기화, 조건식, 증감문 순으로 넣어준다.
for (let n = 5; n <= 10; n = n + 1) {
  // 조건을 풀어 말하자면,
  // 초기화(initialExpression): 숫자(n)는 5부터 시작한다. let n = 5;
  // 조건식(condition): 숫자(n)이 10이 될때까지 반복한다. n <= 10;
  // 증감문(incrementExpression): 숫자(n)는 1씩 증가한다. n = n + 1; or n++;
  sum = sum + n; // 반복할 내용을 중괄호 안에 넣어준다.
}
console.log(sum); // 46
```

만일 조건문이 생략된다면, 그 조건문은 참으로 추정되어 무한 반복문이 실행된다는 말이다.
for문의 실행 순서는 다음과 같다:

1. 반복문에 진입할 때 초기화가 단 한 번 실행된다.
2. 조건식으로 넘어가 반복마다 해당 조건이 확인된다. false이면 반복문이 멈추고 다음으로 넘어간다.
3. 반복할 내용이 위의 조건식이 true면 계속해서 실행된다.
4. 증감문이 각 반복할 내용이 실행된 이후에 실행된다.

```js
let n = 5;
            조건이 true이면 sum = sum + n을 실행한 후, 증감문을 실행함
let n = 5 + 1;
            조건이 true이면 sum = sum + n을 실행한 후, 증감문을 실행함
let n = 6 + 1;
            조건이 true이면 sum = sum + n을 실행한 후, 증감문을 실행함
let n = 7 + 1;
            조건이 true이면 sum = sum + n을 실행한 후, 증감문을 실행함
     // 계속해서 이렇게 반복하다, 조건이 false가 나오면 반복문은 종료된다.
```

## `while` 구문 (`while` statement)

while 반복문은 if문처럼 조건식만 괄호 안에 넣어주고 초기화는 while문 밖에 넣어주고 증감문은 while 안 중괄호 안에 넣어준다. for문으로 할 수 있는 걸 while문으로 할 수 있고, while문으로 할 수 있는 걸 for문으로 할 수 있다. 초기화 혹은 증감문이 필요 없을 때 while을 사용하는 것도 좋다.

```js
let sum = 1;
let n = 5; // 초기화는 while문 밖에

while (n <= 10) {
  // 조건식만 while() 안에
  sum = sum + n;
  n = n + 1; // 증감문은 while 안쪽 {] 안에
}
console.log(sum); // 46
```

## 배열의 반복

배열과 반복문을 같이 사용하는 경우가 많다. 그렇다면 배열에서 반복문을 어떻게 적용해 볼 수 있을까? 다음과 같이 할 수 있다.
만일 내 호주머니에 1불이 3개, 2불이 1개, 5불이 1개, 10불이 5개가 뒤죽박죽 섞여 있다고 가정했을 때, 내 호주머니에 총 얼마가 있는지 그 합을 알고 싶다.

```js
let myPocket = [1, 10, 1, 10, 10, 1, 2, 10, 5, 10];
let sum = 0;
/* 조건을 만들어 줘야 한다:
숫자(n)은 0부터 시작한다. (myPocket의 0번째 인덱스부터 시작한다.) 초기화
숫자(n)은 myPocket의 길이보다 작을때까지 반복한다. 조건식
숫자(n)은 1씩 증가한다. (myPocket의 모든 인덱스를 합해야 하니깐) 증감문
위의 조건을 코드로 만들어 준다:
*/
for (let n = 0; n < myPocket.length; n++) {
  // 호주머니 안에 있는 금액의 총 합을 알고 싶다.
  sum = sum + myPocket[n];
}
console.log(sum); // 내 주머니에는 총 60불이 있다.
```

여기서 나와 아내가 맛있는 저녁 식사를 한 후에 총 40불을 내야 했다. 10불짜리 지폐 4장만 꺼내야 하는 상황인데, 어떻게 해야할까?

```js
let myPocket = [1, 10, 1, 10, 10, 1, 2, 10, 5, 10];
let payment = 0;
//먼저 for문으로 내 주머니의 각 인덱스 값에 접근을 해준다.
for (let n = 0; n < myPocket.length; n++) {
  if (myPocket[n] === 10) {
    // 여기서 if문으로 10불짜리 지폐만 꺼내준다.
    payment += myPocket[n];
  }
}
console.log(payment - 10); // 총 내야하는 금액은 40불이므로 10을 빼서 준다.
```

## `for...in`문

`for (variable in object) { ... }`이런 문법 형식을 가졌다. variable에는 매번 반복마다 새로운 속성이름이 변수가 지정된다. 입력된 객체의 항목들을 반복적으로 반환하여 '무언가'를 할 수 있게 해준다. 모든 객체에서 사용이 가능하다.

```js
var obj = {
  a: 1,
  b: 2,
  c: 3,
};

for (var prop in obj) {
  console.log(prop, obj[prop]); // a 1, b 2, c 3
}
```

## `for...of`문

`for...of` 명령문은 반복 가능한 객체(배열, map, set, 문자열, arguments객체 등)에 대해서 반복한다.

```js
let iterable = [10, 20, 30];

for (let value of iterable) {
  console.log(value); // 10, 20, 30
}
```

`map`에 대한 반복

```js
let iterable = new Map([
  ["a", 1],
  ["b", 2],
  ["c", 3],
]);

for (let entry of iterable) {
  console.log(entry);
}
// [a, 1]
// [b, 2]
// [c, 3]

for (let [key, value] of iterable) {
  console.log(value);
}
// 1
// 2
// 3
```

## `do...while`문

```js
do statement;
while (condition);
```

```js
let result = "";
let i = 0; // 초기화

do {
  i = i + 1; // 증감문
  result = result + i; // 실행할 내용
} while (i < 3); // 조건식

console.log(result); // '123' 이 나온다.
```

`do{}` 안에서 실행을 시키고서, while에서 조건이 `true`로 나오면 다시 `do{}`로 돌아가 실행시킨다.

# 참고

- [MDN](https://developer.mozilla.org/ko/)
- [MDN - for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
- [for...of 블로그1](https://jsdev.kr/t/for-in-vs-for-of/2938)
