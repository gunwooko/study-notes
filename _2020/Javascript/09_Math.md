# Math.

`Math`는 수학적인 상수와 함수를 위한 속성과 메서드를 가진 내장 객체이다.
`Math`는 `Number` 자료형만 지원하며 `BigInt`와는 사용할 수 없다.

## Math.abs()

`Math.abs(x)` 함수는 주어진 숫자의 절대값을 반환한다.
매개변수 x는 숫자가 들어간다.

- 빈 문자열이나 빈 배열 그리고 null을 제공하면 0을 반환한다.

## Number.isInteger(value)

정수인지, 아닌지 여부를 검사할 값이 들어가고, 정수를 판단한 결과가 불리안 값으로 반환된다.

## Math.min(value1, value2, ...) / Math.max(value1, value2, ...)

주어진 숫자 중 가장 작은 값 / 큰 값이 반환된다.

## Math.floor(x) / Math.round(x)

Arguments는 숫자이고, return value는 주어진 숫자의 내림/반올림 값이다.

## Math.random()

Arguments는 없고, return value는 0과 1 사이의 난수를 반환한다.

## Math.sqrt(x)

함수는 숫자의 제곱근을 반환한다. 만약 숫자가 음수이면 NaN를 반환한다.

## Math.pow(base, exponent)

함수는 숫자의 거듭제곱을 반환한다. 만약 숫자가 음수이면 NaN를 반환한다.

# 산술연산자

- 덧셈 (+)
- 뺄셈 (-)
- 나눗셈 (/)
- 곱셈 (\*)
- 나머지 (%)
- 거듭제곱 (\*\*)
- 증가 (++)
- 감소 (--)

# 참고

- [MDN 산술연산자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators)
