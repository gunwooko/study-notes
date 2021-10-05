# Template literals

탬플릿 리터럴은 내장된 표현식을 허용하는 문자열 리터럴이다. 사용법은 다음과 같다.

```js
let str1 = "hello";
let str2 = "world";
// 보통이라면 문자열을 다음과 같이 합쳐준다:
"My first " + str1 + " " + str2 + "!";
// "My first hello world!" 가 반환된다.

// 탬플릿 리터럴을 사용해서 간단하게 사용할 수 있다.
// 탬플릿 리터럴은 백틱을 (``) 사용한다.
`My first ${str1} ${str2}!`;
// "My first hello world!" 위와 같은 문자열이 반환됨을 볼 수 있다.
```

탬플릿 리터럴이 편한 이유는 줄 바꿈, 여러 줄 문자열, 표현식, 문자열 삽입 등이 있다.
문자열로 탬플릿을 만들 때 유용하다.

```js
let templ = (username) => `<div>
  ${username}
</div>`;

templ('Martin');
// 아래와 같이 반환된다.
"<div>
  Martin
</div>"
```

# 참고

- [탬플릿 리터럴 블로그1](https://eblee-repo.tistory.com/38)
- [MDN - template literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)
