# Basic C

## 기초: 함수선언 그리고 컴파일러

```c
// stdtio.h 이름의 파일을 찾아서 printf 함수에 접근할 수 있도록 해준다.
#include <stdio.h>
// 함수 선언
int main(void){
    // 이곳에 코드 작성
    // 문자열을 항상 쌍따옴표로 감싸주기
    printf("hello world!");
}
```

우리가 작성한 소스코드를 컴퓨터가 이해하도록(이진법으로===machine code) 변환(번역)해주어야 하는데 이런 작업을 컴파일러(compiler)라는 프로그램이 해준다.

- `clang hello.c`: `clang` 컴파일러로 `hello.c` 코드를 컴파일해줘

- 컴파일의 결과로 `a.out`이란 파일이 생성되고, 이 파일을 컴퓨터가 실행할 수 있게된다.

## 변수지정 그리고 타입선언

```c
// C언어에서는 데이터의 타입을 정확하게 명시해주어야 한다.
// 사용자의 입력값이 answer에 저장: 해당 입력값은 문자열이다.
string answer = get_string("Where are you from?\n")

// 받은 입력값 answer의 타입을 지정해준다.
// % 뒤에 문자열 string의 앞에를 따서 %s 라고 지정한다.
printf("hello, %s\n", answer)
```

- `clang -o string stringTest.c`: `stringTest.c`파일을 `string.out`이란 이름으로 컴파일후 저장하라

## 정수(integer), if 조건문, else if 조건추가, == 일치 연산자 그리고 loof 반복수행

```c
// 숫자를 변수에 할당하고 싶을때
// int는 변수가 정수(integer)라는 것을 알려준다.
int counter = 0;

// 위에서 1를 더해고 싶을때
counter = counter + 1;

// 위의 동작을 간략하게 하고 싶을 때:
// 방법 1
counter += 1;
// 방법 2
counter++;

// 조건문 표현
if(x < y){
    // 조건을 넣어주고, 조건이 truthy 할 때 아래의 코드를 실행한다.
    // 아니면 다른 조건으로 넘어간다.
    printf("x is less than y");
} else if(x > y){
    printf("x is not less than y");
} else if(x == y){ // 일치 연산자
    printf("x is equal to y");
}

// 루프 while
while (true){
    printf("hello world!");
}

// 특정 횟수만큼 작업수행하기
int i = 0;
while(i < 50){
    printf("hello!");
    i = i + 1;
}

// 루프 for
// for (변수초기화, 변수 조건, 변수 증가) 순으로 작성한다.
for(int 1 = 0; i < 50; i = i + 1){
    printf("hello!!");
}
```

## 자료형, 형식 지정자 그리고 연산자

다양한 데이터 타입

- bool: 불리언 표현, 예) True, False, 1, 0, yes, no
- char: 문자 하나, 예) 'a', 'Z', '?'
- string: 문자열
- int: 특정 크기 또는 특정 비트까지의 정수, 예) 5, 28, -3, 0
- long: 더 큰 크기의 정수
- float: 부동소수점을 갖는 실수, 예) 3.14, 0.0, -28.56
- double: 부동소수점을 포함한 더 큰 실수

알아둘 점:

- `int`는 대략 40억까지 셀 수 있다. 40억개 이상의 데이터를 사용하는 경우가 아니라면 대부분 일반 사용자는 정수에 `int`를 사용한다.

형식 지정자란

- %c : char
- %f : float, double
- %i : int
- %li : long
- %s : string

기타 연산자 및 주석달기

- +: 더하기
- -: 빼기
- \*: 곱하기
- /: 나누기
- %: 나머지
- &&: 그리고
- ||: 또는
- //: 주석
