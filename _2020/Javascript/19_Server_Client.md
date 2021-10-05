# 서버와 클라이언트

요청하는 주체가 클라이언트, 요청에 따른 응답을 주는게 서버이다. 일반적으로 서버에게 HTTP(URL) 요청 후, 응답을 처리한다. 응답은 다양한 형태로 받을 수 있다. (JSON, HTML, plaintext 등) 요청을 했을 때 주는 방식은 서버의 마음이다.

## HTTP 요청은 fetch API 로

fetch는 전역객체이다 (window.fetch()) 그리고 서버에서 사용 가능한데, fetch API는 서버에서 API를 받아와서 사용하게끔 해주는 JS문법중 하나다. fetch API의 패턴은 다음과 같다.

```js
fetch("http://example.com/movies.json") // 서버요청 주소입력
  // 어떤 파일 형태로 받을 건지:
  .then(function (response) {
    return response.json();
    // 응답 형식에 따라 response.text() 아니면
    // response.html() 로 받을 수 있다.
  })

  // 콜백으로 받아서 출력:
  .then(function (myJson) {
    console.log(JSON.stringify(myJson));
  });
```

API 사용시 유의할 점은 API는 공짜가 아니다. 즉, 서비스 제공자로부터 권한을 받아야 한다. 그러므로 접근권한을 주는 `API key`는 암호처럼 취급되어야 한다.

## 서버에 기록하기

- HTTP 요청을 GET이 아닌 POST를 이용한다.
- 내용(payload)와 함께 전달한다.
- Example: 게시판에 새로운 글을 쓰고자 할때, 아이디와 비밀번호로 로그인을 하고자 할때.
  밑에는 MDN의 서버에 기록하기의 예시이다.

```js
var url = "https://example.com/profile";
var data = { username: "example" };

fetch(url, {
  method: "POST", // POST 방식을 이용한다.
  body: JSON.stringify(data), // 내용(payload)와 함께 전달한다.
  headers: {
    "Content-Type": "application/json",
  },
})
  .then((res) => res.json())
  .then((response) => console.log("Success:", JSON.stringify(response)))
  .catch((error) => console.error("Error:", error));
```

# 참고

- [MDN - using fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95)
- [Korean JSON](https://koreanjson.com/)
- [API store](https://www.apistore.co.kr/main.do)
