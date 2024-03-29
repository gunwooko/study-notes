# 알고리즘 (algorithm)

알고리즘은 어떠한 문제를 해결하기 위한 절차를 만들어내는 과정 혹은 형태이다. 문제를 찾아 큰 문제를 잘게 분해하고, 절차를 생각해서 반복되는 부분을 찾는 과정을 알고리즘 문제를 풀면서 연습할 수 있다.
문제를 풀기 전에, 과정 하나하나를 의사코드 (pseudocode)로 적어낼 수 있는데, 의사코드는 우리가 사용하는 일반적인 언어로 작성하는데, 실행할 수 있는 코드는 아니지만 코딩하기 전에 어떻게 프로그램이 작동하는지 그 흐름을 파악하는 데 유용하다.

# 복잡도 (Complexity)

복잡도를 말할 때 시간 복잡도(time complexity)와 공간 복잡도(space complexity)가 존재한다. 이런 복잡도는 문제를 해결하고 알고리즘을 해결할 때에 시간이 얼마나 걸리고 공간을 얼마나 차지하는 것을 의미한다.

## 복잡도를 알아야 할 중요성

예를 들면, 아직 모바일 디바이스의 한계와 제약은 존재하고, 계속해서 떠오르는 머신러닝과 같은 작업은 많은 자원을 요구하기에 시간과 공간을 어떻게 하면 더 절약하고 줄여서 잘 사용하는 것에 따라 하드웨어와 서버 비용을 줄일 수 있다. 복잡도 잘 이해하면 코드의 효율성을 높일 수 있다.

# Time Complexity

문제를 해결하려 할 때 다양한 알고리즘을 사용할 수 있다. 즉, 다양한 접근 법(approaches)가 있다. 그리고 각 접근방식에는 얼마큼 시간상으로 효과적인지 아닌지를 확인할 수 있는데, 이때 시간 복잡도를 말 할 수 있다.

## Big-O Notation

시간 복잡도를 말할 때 사용된다. 즉, 알고리즘의 시간 효율성을 따져서 가장 시간이 오래 걸리는 안 좋은 방식을 찾아낼 수 있다.
Big-O Notation에는 시간 복잡도의 근사치를 나타내는 나타내는 표현이기에 정확한 값이 아닌, complexity types이 정해져 있다.

| Notation |      O(1)       |  O(log n)   |  O(n)  |   O(n2)   |      O(cn)      |
| :------: | :-------------: | :---------: | :----: | :-------: | :-------------: |
|          |    \*최고임     |             |   \*   |    \*     |  매우 안 좋음   |
|          | <= slow growing |             |        |           | fast growing => |
|   이름   |    constant     | logarithmic | linear | quadratic |  exponentional  |

### Big-O Notation의 complexity types 표기 규칙

- 앞에 개수를 무시한다. Ex) ~~2~~n => O(n), ~~3~~n2 => O(n2)
- 낮은 차수의 숫자는 무시한다. Ex) n~~+2~~ => O(n), n2~~+n~~ => O(n2)
