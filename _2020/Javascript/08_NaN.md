# NaN (Not-A-Number)

숫자가 아님을 나타낸다.

`NaN`은 다른 모든 값과 비교했을 때 같지 않고 다른 NaN과도 같지 않다. `===`, `!==` 연산자로 판별할 수 없다.

## isNaN()

`isNaN(value)` 어떤 값이 `NaN`인지 판별하는 함수.
주어진 값이 `NaN`이면 `true`, 아니면 `false`를 반환한다.

## Number.isNaN()

`Number.isNaN(value)` 주어진 값이 `NaN`인지 판별한다. 기존부터 존재한 전역 `isNaN()` 함수의 더 엄격한 버전이다.
주어진 값의 유형이 `Number`이고 값이 `NaN`이면 `true`, 아니면 `false`를 반환한다.
전역 `isNaN()` 함수와 달리, `Number.isNaN()`은 강제로 매개변수를 숫자로 변환하는 문제를 겪지 않는다. 오직 숫자형이고 또한 `NaN`인 값만이 `true`를 반환한다는 말이다.
