# Basic C - detail

## stdio.h

```c
#include <stdio.h>
// standard io 파일은 헤더파일로써 C언어로 작성되었고, .h로 끝나는 파일이다.
// 이 파일에는 printf 함수의 프로토타입이 담겨있어
// clang 컴파일러가 소스코드를 읽을 때 printf 함수가 무엇인지 알려준다.

int main(void)
{
    printf("hello, world!\n");
}
```

## 컴파일 과정

### 1. 전처리(Precompiling)

`#`으로 시작하는 소스코드에 추가된 해당 파일을 포함시키는 작업을 실행한다. 실질적인 컴파일링이 시작되기 전에 실행하라고 알려준다.

### 2. 컴파일링(Compiling)

이 과정에선 컴파일러 프로그램이 C 코드를 어셈블리어로 변경해준다. 어셈블리어는 컴퓨터가 이해할 수 있는 최대한 가까운 프로그램으로 만들어 준다. 저수준 프로그래밍 언어.

### 3. 어셈블링(Assembling)

어셈블리 코드를 오브젝트 코드로 변환시켜준다. 즉 바이너리로 명령어를 변경해준다. 해당 작업은 어셉를러라는 프로그램으로 수행되고, 만일 컴파일 되어야 할 파일이 하나라면 여기서 작업을 마치게 된다. 그렇지 않을 경우 링킹 단계가 추가된다.

### 4. 링킹(Linking)

컴파일하는 파일이 여러 개의 파일로 이루어져 있는 경우 링크라는 컴파일러 단계를 통해 하나의 오브젝트 파일로 합쳐져야 한다. 예를 들어 stdio.h, cs50.h 등의 파일을 현재 hello.c 파일에 합쳐준다.

## 디버깅

버그는 코드의 오류이다. 디버깅은 코드에 있는 버그를 확인하고 고치는 과정이다.

디버거란 프로그램은 버그를 찾는데 도움이 된다. 프로그램이 멈추는 특정 지점을 중지점이라 부른다.

`printf`, JS에는 `console.log`가 있다.

## 코드 스타일 가이드, 코드 디자인의 중요성

실제로 협업, 프로젝트를 진행 할 때에 특정한 스타일 가이드를 따르도록 한다.
여러사람들이 코드를 작성하기 때문에, 서로 불필요한 오해를 줄이고 코드를 이해하는데 드는 비용을 최소화해주기 때문이다.

# Arrays

여러 자료형이 있고, 각각의 자료형은 서로 다른 크기의 메모리를 차지하게 된다.

- bool: 불리언, 1byte
- char: 문자, 1byte
- int: 정수, 4bytes
- float: 실수, 4bytes
- long: 큰 정수, 8bytes
- double: 큰 실수, 8bytes
- string: 문자열, ?bytes

컴퓨터에는 물리적 칩, RAM 메모리가 있고, 예를 들어 메모리를 사각형 하나를 1바이트로 해서 나눠볼 수 있다. 그리고 위의 각각의 자료형이 저장될때 차지하게 되는 것이다.

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int score1 = 72;
    int score2 = 73;
    int score3 = 33;

    printf("Average: %i\n", (score1 + score2 + score3) / 3);
```

위 코드의 문제점으로 스코어가 고정되어 있고, 추가 혹은 빼고 싶을때 번거롭다. 또한 스코어가 반복되는 것을 확인할 수 있다.

C에서는 여러값을 저장할 수 있는 하나의 변수를 가지고 싶을때 배열을 사용한다. 아래에 배열을 사용해서 위의 코드를 수정한다면:

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int scores[3]; // int 자료형을 가지는 크기가 3인 배열을 생성한다
    scores[0] = 72;
    scores[1] = 73;
    scores[2] = 33;

    printf("Average: %i\n", (scores[0] + scores[1] + scores[2]) / 3);
}
```

그럼에도 불구하고 아직까지 개선할 부분이 있다. 아직 반복되는 부분이 있기 때문이다. 반복되는 부분이 많은 코드는 버그의 위험성에 더 많이 노출될 가능성이 크다.

```c
#include <cs50.h>
#include <stdio.h>

const int N = 3; // 전역변수를 선언해줄 수 있다.
// 전역변수는 전테적인 코드에서 변하지 않는 값임을 보여준다.
// 고정된 값 (상수)를 지정한다. 그리고 const 키워드를 사용해준다.
// 보통 관례적으로 전역변수의 이름은 대문자로 표기한다.
// 또한 코드의 상단에 배치된다.

int main(void)
{
    int scores[N];
    scores[0] = 72;
    scores[1] = 73;
    scores[2] = 33;

    printf("Average: %i\n", (scores[0] + scores[1] + scores[2]) / N);
}
```

```c
// 배열 예제
#include <cs50.h>
#include <stdio.h>

float average(int length, int array[]);

int main(void)
{
    int n = get_int("Scores:  ");

    int scores[n];

    for (int i = 0; i < n; i++)
    {
        scores[i] = get_int("Score %i: ", i + 1);
    }

    printf("Average: %.1f\n", average(n, scores));
}

//평균 계산 함수
float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return (float) sum / (float) length;
}
```

## 배열, 문자열 그리고 Null terminator

`\0`는 null를 의미한다. C에서 문자열의 끝을 나타낼 때 표현되기도 한다.

예를 들어 "hi!" 문자열이 실질적으로 차지하는 메모리는 3바이트가 아닌 4바이트가 된댜. 그 이유는 마지막 문자열이 끝나는 부분에 null terminator가 추가되기 때문이다.

## 문자열의 길이

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string s = get_string("Input: ");
    printf("Output:\n");
    for (int i = 0; s[i] != '\0'; i++)
    // 문자열의 끝이 null이라는 사실을 알 고 있기 때문에
    {
        printf("%c\n", s[i]);
    }
    printf("\n)
}
```

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h> // 문자열 관련 라이브러리: strlen 문자열의 길이를 알려주는 함수

int main(void)
{
    string s = get_string("Input: ");
    printf("Output:\n");
    for (int i = 0, n = strlen(s); i < n; i++)
    {
        printf("%c\n", s[i]);
    }
}
```

[ASCII 코드 확인 사이트](asciichart.com)

```c
// 소문자를 대문자로 변경하기
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main(void)
{
    string s = get_string("Before: ");
    printf("After:  ");
    for (int i = 0, n = strlen(s); i < n; i++)
    {
        if (s[i] >= 'a' && s[i] <= 'z')
        {
            printf("%c", s[i] - 32);
            // 위의 사이트에 확인해보면 대문자와 소문자가 32의 차이가 있음을 확인할 수 있다.
        }
        else
        {
            printf("%c", s[i]);
        }
    }
    printf("\n");
}
```

```c
#include <cs50.h>
#include <ctype.h> // 또다른 라이브러리: toupper함수
#include <stdio.h>
#include <string.h>

int main(void)
{
    string s = get_string("Before: ");
    printf("After:  ");
    for (int i = 0, n = strlen(s); i < n; i++)
    {
        printf("%c", toupper(s[i]));
    }
    printf("\n");
}
```

##

```c
#include <cs50.h>
#include <stdio.h>

int main(int argc, string argv[])
// argc는 main함수가 받게될 인수(입력의 개수)이다.
// argv[], argument vector 는 그 입력이 포함되어 있는 배열이다.
// 여기서 main 함수가 int를 리턴한다고 되어 있는데, 이는 코드가 잘 실행된다면 0이 반환된다.
{
    if (argc == 2)
    // 여기가 2인 이유는, argv[0]은 기본적으로 프로그램의 이름으로 저장되기 때문이다.
    // 만일 값이 추가된다면 argv[1]에서 부터 저장된다.
    {
        printf("hello, %s\n", argv[1]);
    }
    else
    {
        printf("hello, world\n");
    }
}
```
