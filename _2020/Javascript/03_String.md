# 문자열을 다루기 (String Methods)

여기서는 자바스크립트에서 문자열을 다루는 여러 가지 방법들을 다룰 것이다. 한 가지 중요한 사실은 **문자열의 메소드는 모두 IMMUTABLE**이다. 원본 문자열을 건드리지 않는다. 즉, **원본이 변하지 않는다**. 변환시키고 싶으면 새로 대입 시켜 주어야 한다.

## How to access a character

### str[index]; // but read-only

기본적으로 문자열에선 인덱스를 통해 접근할 수 있다. 그러나 인덱스로 접근은 가능하지만, 수정을 하는 것처럼 사용하지는 못한다.

## How to concatenate strings

### + 연산자

```js
let a = "I am ";
let b = "Martin";
"hello" + " " + "world"; // 'hello world'
a + b; // 'I am Martin'
```

#### 문자열과 다른 타입 사이에 + 연산자를 쓰면, 문자열로 변환한다.

```js
"I am " + 28; // 'I am 28'
"It's " + true + ", isn't it?"; // "It's true, isn't it?"
```

### .toString() 메소드

```js
let num = 20200506;
num.toString(); // '20200506'

let arr = [123, "hello", 456, false, num];
arr.toString(); // '123,hello,456,false,20200506'
```

### .concat() 메소드

```js
const str1 = "Hi";
const str2 = "How are you?";

console.log(str1.concat(" ", str2));
// expected output: "Hi How are you?"

console.log(str2.concat(", ", str1));
// expected output: "How are you?, Hi"
```

concat() 메소드에서는 매개변수에 합칠 문자열이 들어가는데 여러 문자열 값을 넣을 수 있다.

## length PROPERTY

문자열의 전체 길이를 반환한다.

```js
let str = "BootCamp";
console.log(str.length); // 8
```

length property는 문자열에도 있고 배열에도 있다. 길이는 각 문자열, 혹은 배열이 가지고 있는 고유의 속성이기 때문이다.

## str.indexOf(searchValue)

찾고자 하는 문자열을 반환해준다.

- Arguments: 찾고자 하는 문자열
- Return value: 처음으로 일치하는 인덱스, 찾는 인덱스가 없으면 -1을 반환

## str.lastIndexOf(searchValue)

찾고자 하는 문자열을 반환해준다. str.indexOf()와 다른 점은 문자열 뒤에서부터 찾아준다.

## str.includes(searchValue)

문자열 내에 찾고자 하는 다른 문자열이 있는지 확인할 수 있다.

- Arguments: 찾고자 하는 문자열
- Return value: 문자열을 찾으면 true, 못 찾으면 false

## str.split(seperator)

문자열을 나누고 싶을 때 사용하면 좋다. 특히 csv형식을 처리할 때 유용하다.

- Arguments: 분리 기준이 될 문자열
- Return value: 주어진 문자열을 separator마다 끊은 부분 문자열을 담은 Array

## str.substring(start, end)

문자열에서 중간 부분만 가지고 오고 싶을 때 사용하면 좋다.

- Arguments: 시작index, 끝index. (순서는 변경되도 상관없다)
- Return value: 시작과 끝 index 사이의 문자열.

## str.slice(start, end)

문자열의 추출된 부분을 담는 새로운 문자열이 반환됩니다. substring() 메소드와 비슷하지만 몇 가지 차이점을 보인다.

- substring() 메소드에선 start와 end가 변경되어도 알아서 잘 작동하지만, slice() 메소드에선 빈 문자열이 반환된다.
- substring() 메소드에선 arguments에 음수 혹은 NaN이 들어가면 0으로 취급한다. 또한 slice() 메소드에서도 arguments에 NaN이 들어가면 0으로 취급한다, 그러나 음수가 들어갈 경우 문자열 끝부분부터 역방향으로 인덱스를 찾아 반환한다.

## str.toLowerCase()

- Arguments: 없음
- Return value: 소문자로 변환된 문자열

## str.toUpperCase()

- Arguments: 없음
- Return value: 대문자로 변환된 문자열

## str.trim()

- Arguments: 없음
- Return value: 양 끝에서 공백을 제거한 새로운 문자열, 여기서 공백이란 space, tap, \t, \r\n, \n 등이 있다.

## 문자열 정규표현식 Regular Expression

정규 표현식은 문자열에 나타나는 특정 문자 조합과 대응시키기 위해 사용되는 패턴이다. 자바스크립트에서, 정규 표현식 또한 객체다. [MDN 문자열 정규표현식에 관하여](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/%EC%A0%95%EA%B7%9C%EC%8B%9D). 이 패턴들은 RegExp의 exec 메소드와 test 메소드, 그리고 문자열의 match()메소드, replace()메소드, search()메소드, split()메소드와 함께 쓰인다.

### str.match(RegExp)

- Arguments: RegExp (매개변수를 전달하지 않고 사용하면, 빈 문자열[""]이 있는 Array가 반환된다.)
- Return value: 문자열이 정규식과 매치되는 부분을 검색해서 일치하는 부분이 있으면 Array에 담아서 반환한다. 일치하는 것이 없으면 `null`을 반환한다.

# 참고

[MDN](https://developer.mozilla.org/ko/)
