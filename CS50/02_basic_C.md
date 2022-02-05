# Basic C

## 기초: 함수선언 그리고 컴파일러

```c
// hello.c
// stdtio.h 이름의 파일을 찾아서 printf 함수에 접근할 수 있도록 해준다.
#include <stdio.h>
// 함수 선언
int main(void){
    // 이곳에 코드 작성
    // 문자열을 항상 쌍따옴표로 감싸주기
    printf("hello world!\n");
}
```

우리가 작성한 소스코드를 컴퓨터가 이해하도록(이진법으로===machine code) 변환(번역)해주어야 하는데 이런 작업을 컴파일러(compiler)라는 프로그램이 해준다.

- `clang`은 c로 작성된 코드를 컴파일하기 위해 만들어진 프로그램이다.
- `clang hello.c`: `clang` 컴파일러로 `hello.c`에 작성된 c 코드를 컴파일해줘
- 위의 결과로 (컴파일의 결과로) `a.out`이란 파일이 생성되고, 이 파일을 컴퓨터가 실행할 수 있게된다. => `./a.out`
- `clang` 명령어 뒤에 몇가지 옵션을 줄 수 있다.
  - `clang -o [아무이름] hello.c`: 이렇게 하게 되면 [아무이름]이란 파일에 `hello.c` 소스코드가 컴파일되어 저장된다.
- `ls` 명령어로 파일을 확인할 때 파일명 뒤에 `*`가 붙는것은 기계어 즉, 컴퓨터가 실행할 수 있는 파일이란 뜻이다.

## 변수지정 그리고 타입선언

```c`
// string.c
#include <cs50.h>
#include <stdio.h>
int main(void)
{
// C언어에서는 데이터의 타입을 정확하게 명시해주어야 한다.
// 사용자의 입력값이 answer에 저장: 해당 입력값은 문자열이다.
string answer = get_string("Where are you from?\n"); // get_string은 사용자의 입력을 저장한다고 하자(예시 cs50의 라이브러리임).
// 받은 입력값 answer의 타입을 지정해준다.
// % 뒤에 문자열 string의 앞에를 따서 %s 라고 지정한다.
// %s 는 형식 지정자로써 예시에선 answer이 값을 $s에 넣어준다.
printf("hello, %s\n", answer);
}

````

- `clang -o string string.c -lcs50`: `string.c`파일을 `string`이란 이름으로, 그리고 `cs50`의 코드와 연결해서 컴파일후 저장하라. 여기서 `-l` 옵션은 link 연결하라는 뜻이다.

- 위와 같이 너무 복잡한 명령어대신 사용할 수 있는 것이 `make` 명령어이다. `make [파일이름 without .c]`를 통해 위의 명령어와 같은 결과를 만들어 낼 수 있다.

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

// 또한 else도 있다.
if(conditional statement){
    // do something;
}else{
    // do something if the conditinal statement is falsy;
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
````

## 자료형, 형식 지정자 그리고 연산자

다양한 데이터 타입

- bool: 불리언 표현, 예) True, False, 1, 0, yes, no
- char: 문자 하나, 예) 'a', 'Z', '?'
- string: 문자열
- int: 특정 크기 또는 특정 비트까지의 정수, 예) 5, 28, -3, 0
- long: 더 큰 크기의 정수 (int로 셀 수 없는 정도의 큰 숫자 예: 40억 +)
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

```c
// 예시: int.c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int age = get_int("What's your age?\n");
    int days = age * 365;
    printf("You are at least %i days old.\n", days);
}
```

```c
// 예시: float.c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    float price = get_float("What's the price?\n");
    printf("Your total is %f.\n", price * 1.0625);
    // 여기서 소수점 2번째 자리까지만 원한다면,
    printf("Your total is %.2f.\n", price * 1.0625);
}
```

```c
// 예시: custom function: cough
#include <stdio.h>

void cough(void); // 이부분이 누락된다면 cough를 찾을 수 없다는 에러메세지가 나오게된다.
// 위와 같은 방법으로 컴퓨터에게 cough란 이름의 함수가 존재한다는 사실을 알려줌으로 에러를 피할 수 있다.

int main(void)
{
    fot(let i = 0; i < 3 ; i++){
        cough();
    }
}

void cough(void)
{
    printf("cough!\n");
}
```

```c
// 예시: 매개변수를 넣은 함수
#include <stdio.h>

void cough(int n);

int main(void)
{
  cough(3);
  //이렇게 해주면 조금더 직관적이 cough 함수가 어떻게 짜여져있는지 숨길 수 있다.
}

// 또한 한가지 중요한 것은 여기서 앞쪽 void는 함수의 출력 타입이다.
void cough(int n)
{
    fot(let i = 0; i < n ; i++){
       printf("cough!\n");
    }
}
```

## 하드웨어의 한계

```c
// 예시: overflow.c
#include <stdio.h>
#include <unistd.h> // 공식문서 확인하기

int main(void)
{
    for(int i = 1; ; i *= 2)
    {
        printf("%i\n", i);
        sleep(1); // 1초씩 잠들게 한다. 공식문서확인하기
    }
}

// 위의 결과로 계속해서 2배의 값이 1초마다 나타남을 확인할 수 있다.
// 그러나 어느 순간 부터 숫자가 많이 커지게 되면 계속 증가하다가 더 큰값을 기억한 비트가 없음을 확인할 수 있다.
```
