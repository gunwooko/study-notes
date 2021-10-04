# Express

Express는 Node.js의 핵심 모듈인 http와 [Connet 컴포넌트](https://github.com/senchalabs/connect#readme)를 기반으로 한 가장 인기 있는 프레임워크이다. Node에서의 서버 개발을 빠르고 손쉽게 도와준다.
Express는 다양한 장점이 있는데,

- 손쉽게 서버를 생성할 수 있다. (http 모듈이 express에 내장되어 있어서, 따로 http를 import 할 필요는 없다.)
- 미들웨어(Middleware) 구조로써 다양한 기능의 미들웨를 마음대로 선택해 결합해서 사용할 수 있다.
- 자체 라우터를 제공한다.

## Express로 웹서버 작성하기

```js
const express = require("express");
const app = express();
const PORT = 3000;

app.get("/", function (req, res) {
  res.send("Hello World!");
});

app.listen(PORT, () => {
  console.log(`server listen on ${PORT}`);
});
```

## 미들웨어 (Middleware)

Express의 가장 큰 장점 중 하나로, 미들웨어 함수는 요청(req)과 응답(res), 그리고 그다음의 미들웨어 함수(next)에 대한 접근 권한을 갖는 함수이다.
미들웨어는 중간 처리 역활을 수행하는데, 클라이언트의 요청에 대한 응답을 완수하기 전에 다양한 일을 처리할 수 있다. 미들웨어 함수 생명주기는 req-res 응답을 주기로 종료되고, 미들웨어 함수의 우선순위는 먼저 로드되는 미들웨어 함수가 먼저 실행된다. 즉, 코드 순서가 매우 중요하다.

```js
// 예시
const express = require("express");
const app = express();
const PORT = 3000;

const requestTime = (req, res, next) => {
  req.resquestTime = Data.now();
  next();
};

app.use(requestTime);

app.get("/", function (req, res) {
  let resText = "Hello World!";
  resText += "Requested at: " + req.requestTime + "";
  res.send(resText);
});

app.listen(PORT, () => {
  console.log(`server listen on ${PORT}`);
});
```

### 미들웨어 module : body-parser

body-parser는 body-stream을 메모리 객체에 매핑하기 위한 모듈이다. [Express 4.16 부터는 body-parser를 따로 설치하지 않아도 사용 가능하다.](https://medium.com/@mmajdanski/express-body-parser-and-why-may-not-need-it-335803cd048c)

### 참고

- [Writing middleware for use in Express apps](https://expressjs.com/en/guide/writing-middleware.html)
- [Express.js의 미들웨어](https://siner308.github.io/2020/01/04/express-middleware/)
- [cors header 설정 손쉽게 하는 법](https://www.npmjs.com/package/cors)
- [req.on('data',() => {}) 없이 data 받는법](https://www.npmjs.com/package/body-parser)
- [Node - Express 커스텀 미들웨어 만들기](https://backback.tistory.com/333)
- [Express - 오류 처리](https://expressjs.com/ko/guide/error-handling.html)

## 라우팅(Routing)

라우팅은 애플리케이션 엔드포인트(URI)의 정의, 그리고 URI가 클라이언트 요청에 응답하는 방식을 말한다. 라우팅은 코드의 과정을 분기하는 것이다. 파일을 하나로 해도 괜찮지만, 다루어야 할 규모가 커지고 엔드포인트 또한 많아지면 파일을 카테고리 별로 나누어서 가독성을 높히고 복잡도를 낮출 수 있게 된다. 서버에서 엔드포인트를 잘 정리해주면 좋은 코드가 될 수 있다. 각 라우트는 하나 이상의 핸들러 함수를 가질 수 있고, 이러한 함수는 라우트가 일치할 때 실행된다.

```js
// app은 express의 인스턴스이다.
// 첫 번째 인자로 들어가는 부분은 PATH이고 서버에서의 경로를 가리킨다.
// 이후 오는 함수가 HANDLER 함수이다. 라우트가 일치하면 실행된다.
app.get("/", function (req, res) {
  res.send("Hello World!");
});

app.post("/", function (req, res) {
  res.send("Got a POST request");
});
```

```js
// Express 라우터를 사용하지 않고서:
const requestHandler = function (req, res) {
  if (req.url === "/messages") {
    if (req.method === "GET") {
      res.end(messages);
    } else if (req.method === "POST") {
      req.on("data", function (req, res) {
        // do something ...
      });
    }
  }
};

// Express 라우터를 사용해서:
const router = express.Router();

router.get("/messages", (req, res) => {
  res.send(messages);
});
router.post("/messages", (req, res) => {
  // do something
});
```

### 참고

- [Express - 기본 라우팅](https://expressjs.com/ko/starter/basic-routing.html)
- [Express - 라우팅](https://expressjs.com/ko/guide/routing.html)
- [라우트 경로의 일치: path-to-regexp](https://www.npmjs.com/package/path-to-regexp)

# 참고

- [Expree 공식 문서](https://expressjs.com/en/4x/api.html#express-json-middleware)
- [MDN - Express/Node 소개](https://developer.mozilla.org/ko/docs/Learn/Server-side/Express_Nodejs/Introduction)
- [Express.js란 무엇인가?](https://wikibook.co.kr/article/what-is-expressjs/)
