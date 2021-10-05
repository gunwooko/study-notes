# 조건문 (Conditional Expression)

조건문은 참 또는 거짓으로 평가되는 표현식이다. 조건문은 어떠한 조건을 판별하는 기준을 만드는 것인데, 조건문은 반드시 **비교 연산자 (comparison operator)** 가 필요하다.
_일치 연산자 ( `===` ), 불일치 연산자 (`!===` ), 초과 연산자 ( `>` ), 이상 연산자 ( `>=` ), 미만 연산자 ( `<` ), 이하 연산자 ( `<=` )_
**비교의 결과는 늘 boolean 값으로 리턴된다**.

## If()문

조건문은 아래와 같이 쓸 수 있다.

```js
if (조건1) {
  // 조건1이 참으로 평가될 경우 실행되는 코드
} else if (조건2) {
  // 조건1일 거짓으로 평가될 경우 조건2로 넘어온다.
  // 조건2가 참으로 평가될 경우 실행되는 코드
} else {
  // 모든 조건이 통과하지 않는 경우 실행되는 코드
}
```

여기서 조건에는 boolean으로 결과가 나오는 조건문 표현식이 들어간다. 또한, 조건문에 또 다른 조건문을 중첩해서 사용 할 수도 있다. 그리고 두 가지 조건을 한 번에 적용하고 싶으면 **논리 연산자 (logical operator)** 을 사용할 수 있다.  
_AND 연산자 ( `&&` ), OR 연산자 ( `||` ), NOT 연산자 ( `!` )_
여기서 NOT 연산자가 어떻게 쓰이는지는 예를 통해 더 자세히 알 수 있다.

```js
!false; // true
!(10 > 1); // false
!undefined; // true
!"hello world"; // false
```

여기서 기억해야 할 **6가지 falsy한 값**이 있는데 if 문에서 false로 변환이 되어, if 구문이 실행되지 않는다. 즉, `if(조건)`에서 falsy한 값이 나오면 그 아래 구문은 작동하지 않는다.

```js
if(false)
if(null) // '값이 없다'라는 의미
if(undefined) // '정의되지 않았다'라는 의미
if(0)
if(NaN) // 'Not a Number' '숫자가 아님'이라는 의미
if('') // 빈 문자열
```

## 삼항 조건 연산자

JavaScript에서 세 개의 피연산자를 취할 수 있는 유일한 연산자이다. 보통 if 명령문의 단축 형태로 쓰인다.
`condition ? exprIfTrue : exprIfFalse `

- condition: 조건식이 들어간다.
- exprIfTrue: 조건이 truthy한 값으로 판별되면 실행된다.
- exprIfFalse: 조건이 falsy한 값으로 판별되면 실행된다.

#### 삼항 조건 연산자의 장점

- if / else 문을 사용하는 함수를 반환하는 데 적합하다.
- 긴 if / else 문을 매우 깔끔하게 만들 수 있다. 동일한 로직을 표현하지만 코드를 읽기 쉽게 만들어 준다.

# 참고

- [MDN 상항조건연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)
