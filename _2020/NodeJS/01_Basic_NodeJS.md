# Runtime

런타임은 프로그래밍 언어가 구동되는 환경, 즉 프로그램이다. 런타인에서 코드가 실행된다고 말할 수 있다. 자바스크립트의 런타임으로는:

1. 브라우저: HTML `<script>` 태그를 사용
2. Node.js: 서버 뿐 아니라, 다양한 환경에서 사용가능하다.

- [Node.js Architecture - youtubeVideo](https://www.youtube.com/watch?v=XUSHH0E-7zk)
- [How Node.js Works?](https://www.youtube.com/watch?time_continue=1&v=jOupHNvDIq8&feature=emb_title)

# NVM (Node Version Manager)

간단한 명령어로 Node를 설치하고
`$ nvm install 10.13.0`
다양한 node version을 옮겨다닐 수 있게 해주는 프로그램이다.
`$ nvm use 12.13.0`
NVM은 다양한 node version을 설치하고 관리할 수 있는 프로그램이다.
또 다른 명령어:

- `$ nvm ls`: 현재 nvm을 통해 설치한 node version을 확인할 수 있다.
- `$ nvm --version`: nvm 버전 확인
- `$ node -v`: node 버전 확인
- `$ nvm ls-remote --lts`: node의 모든 버전 확인 (Long Term Support)

# NPM (Node Package Manager)

필요한 모듈을 다운로드할 수 있는, 모듈들이 모여있는 모듈 스토어다.
하나의 프로그램은 다양한 모듈이 합쳐져서 만들어지는데, 이미 검증된 코드(모듈)를 가져다가 사용할 수 있다. 모듈은 "기능"이라고 생각하면 편하다.

## Package.json

프로그램을 실행시키기 위해 필요한 모듈들이 무엇인지, 프로그램을 실행시키는 방법이 무엇인지, 프로그램을 테스트하는 방법 등이 명시되어 있다.
예) Repository에서 파일을 가져와 package.json에서 필요한 모듈을 확인해 `npm`를 이용해 다운 받아 사용하면 된다. `npm install`이 완료되면 `node_modules`이란 디렉토리가 생성되는데, 이곳에 프로그램을 실행시키기 위한 실제 모듈들이 있다.
`Package.json`의 구조에는 다음과 같은 중요한 것들이 있다:

- `dependencies`: 프로젝트가 돌아가기 위해 반드시 필요한 모듈이 무엇인지 적혀있다.
- `devDependencies`: 개발하는 환경에서 필요한 모듈이 적혀있다. 하지만, 실제 프로그램 동작에는 직접적인 영향을 주지 않는 모듈을 명시한다.
- `scripts`: `npm`으로 실행시킬 수 있는 명령어를 정의한다. 만일 명령어를 실행시켰는데 "정의되지 않은 명령어"라고 오류가 뜨면, `package.json` 파일의 `scripts`에 해당 명령어가 정의되었는지 확인해서 알아볼 수 있다.  
  `npm run 명령어` 이와 같은 방법으로 scripts의 명령어를 실행 시킬 수 있다.

## npm 관련 알면 좋은 지식

- `npm ls` npm 설치 항목 목록을 보여준다.
- `npm --depth=0 ls` local에 설치된 npm 모듈을 확인할 수 있다.
- `npm -g --depth=0 ls` global에 설치된 npm 모듈을 확인할 수 있다.

# Code Quality

좋은 코드가 무엇이지 생각했을 때, 많은 답변이 있을 것이다. 읽기 편안한 코드, 관리하기 쉽고 편안하게 짜인 코드, 등이 있을 것이다. 기본적으로 코드의 quality를 따졌을 때는 기본적으로 3가지를 보면 된다.

1. 작성한 코드가 의도한 대로 실행되는가?
2. 작성한 코드가 문제나 에러가 있진 않은가?
3. 작성한 코드가 읽기 쉽고, 유지하기 쉽고, 범용성이 넓은가?

# Testing

테스팅을 통해 1~2번을 확인할 수 있다. 테스팅하는 다양한 방법이 존재한다.

- End to End Test,
- Integration Test,
- Unit Test,
  여기서 unit test 중 Facebook이 만든 "Jest"가 있는데, [Jest 설치 방법은 jest 공식 문서를 참고하면 된다.](https://jestjs.io/docs/en/getting-started)

`npm install jest` 설치
`npm unistall jest` 삭제
`npx jest` 실행 (=== `npm run jest`)
`npm install --save-dev jest` jest를 `package.json`의 `devDependencies`에 설치한다.
`npm install -g jest` Global영역에 설치. 모든 node 프로그램이 jest를 사용할 수 있도록 해준다. 이것을 추천하지 않는 이유는, 버전이 안 맞아서 오류가 생길 수 있다.

Jest 설치 후에 아래의 `add.js` 파일을 테스트한다고 가정했을 때,

```js
function add(a, b) {
  return a + b;
}
module.exports = add;
```

`add.test.js` 파일을 만들어서 `add.js`에 관한 test case를 작성한다.

```js
const add = require("./add");

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

Jest를 실행하기 전 `package.json` 파일의 `scripts`에 `jest`가 나타나는지 확인한다. 없다면 추가해줘야 한다.

```js
{
  "scripts": {
    "test": "jest"
  }
}
```

그리고서 CLI로 `npm run test`을 실행해준다.

```js
PASS  ./add.test.js
✓ adds 1 + 2 to equal 3 (5ms)
```

그럼 위와 같이 테스트가 성공적으로 실행됨을 볼 수 있다.

# Linting

Lint를 통해 2~3번을 확인할 수 있다. 지정한 코드 스타일을 지키는지 안 지키는지 확인해주는 도구이다. 예를 들어 한 팀에서 어떤 규칙을 정하고 서로 그 규칙을 지키며 일관된 코드 스타일을 유지할 수 있게 도와주는 도구이다. 이렇게 하게 되면 내가 작성하지 않는 코드도 코드 파악이 용이하고 코드 내의 오류를 쉽게 찾을 수 있게 된다. 코드를 작성하는데 일관된 규칙을 정한 것을 style guide라고 한다.
다양한 종류의 linter가 존재하는데 그중 "Eslint"가 있다.
[Eslint 설치 방법은 eslint 공식 문서를 참고하면 된다.](https://eslint.org/docs/user-guide/getting-started)
`npx eslint` 실행 (=== `npm run eslint`)
`npm install eslint --save-dev` eslint를 `package.json`의 `devDependencies`에 설치한다.
설치를 완료한 후에 `npm run lint`를 CLI에서 실행했을 때 lint에러를 잡아낸다면 성공적으로 lint를 설정한 것이다.

또한 서로 규칙을 만들어서 잘 지켜졌는지 첵크하는 포인트가 있는데, 이 시점을 다양하게 설정할 수 있다.

- 코드를 작성할 때 - plugin for your IDE
- 코드를 커밋할 때 - Git hooks (규칙이 다 지켜져야 커밋 가능)
- 코드 테스트를 할 때 - CI (Continuous Integration)

## 유의할 점

Node 환경에서 eslint를 코드에 적용해 진행한다는 것은 document 또는 window 객체와 같은 DOM을 사용할 수 없다는 것을 의미한다. (Browser에선 document나 window 객체 사용 가능, 문제 없음) 그렇기 때문에 eslint를 실행했을 때 document 또는 window 같은 객체를 사용하게 되면 **"정의되지 않았다고 판단한다 - `no-undef`"**. 이 문제를 해결하기 위해선 eslint에 [추가로 설정해줘야 한다.](https://eslint.org/docs/user-guide/configuring#specifying-globals)

# 참고

- [JEST 공식 문서](https://jestjs.io/docs/en/getting-started)
- [ESLINT 공식 문서](https://eslint.org/docs/user-guide/getting-started)
- [Eslint - Specifying Environments
  ](https://eslint.org/docs/user-guide/configuring#specifying-environments)

# Node.js Review

Node.js는 V8 엔진으로 만들어진 자바스크립트 런타임이다. V8 엔진은 자바스크립트를 기계어(native machine code)로 컴파일해준다. 즉, Node.js는 자바스크립를 컴파일하여 구동하고, 이벤트 기반 및 논블로킹 I/O 모델로 속도가 빠르다.

- 이벤트: 유저의 버튼 클릭이나 네트워크에 리소스를 요청(GET)하는 것 등 (fetch 요청)
- 블로킹: 다음 함수의 실행이 현재 함수의 종료 이후에 이루어 이는 것
- 논블로킹: 다음 함수의 실행이 현재 함수의 종료를 기다리지 않음. 모든 작업이 비동기적으로 일어난다.
- I/O 모델: 인풋(request)을 주면 아웃풋(response)을 반환하는 모델. 로컬 파일을 읽거나 쓰는 것, API에 HTTP 요청하는 것들이 있다.
- [Node.js Architecture](https://www.youtube.com/watch?v=XUSHH0E-7zk)
- [How Node.js Works?](https://www.youtube.com/watch?time_continue=1&v=jOupHNvDIq8&feature=emb_title)
- [Event Loop](https://www.youtube.com/watch?v=8aGhZQkoFbQ&feature=emb_title)

Node.js에는 별도의 설치를 하지 않아도, 내장된, Node.js과 함께 번들링되어 있는 모듈들이 있다. `require('')` 방식으로 사용할 수 있고 예를 들어 `fs`, `http`, `url`, `path` 등이 있다.

```js
const fs = require("fs");
const http = require("http");

// File System은 file을 읽고, 쓰고, 수정하고, 삭제가 가능하다
fs.readFile("./something.json", (err, data) => {
  console.log(data);
});

// http는 클라이언트로서 GET요청이 가능하고, 서버로서 서버를 생성할 수 있다.
http.get("http://localhost:5000/api", (res) => {
  console.log(res);
});
```

## NPM & Package.json

Node Package Manager로 세계에서 가장 큰 오픈소스 라이브러리 생태계 중 하나로, NPM을 통해서 간편하게 다양한 모듈들을 가져와서 사용할 수 있게 해준다. `package.json`에 프로젝트에 관한 정보, 설정된 script 코드, 개발과 관련된 dependency와 devDependency 같은 정보가 적혀있다.

- 여기서 설정된 script 코드를 cli에서 실행시킬 수 있다. ex) `npm test`, `npm start`
- `npm init` 을 해당 디렉토리에서 cli로 실행시키면, 설정 이후 `package.json`이 만들어진다. 이후 JS 파일을 만들어서 실행시키려면, `node index.js` 명령어로 실행시킬 수 있다. 이 명령어를 `package.json`의 script에 넣으려면 `"start": "node index.js"`를 입력해준다.
- `npm install` 명령어로 `package.json`의 dependency와 devDependency를 설치할 수 있다.
- devDependency에는 프러덕션과 직접적인 관계는 없지만, 컴파일하거나 테스트를 하는 등 개발만을 위해 설치한 패키지들이 적혀있다. 이런 devDependency를 설치하려면 `--dev` 옵션과 함께 설치/등록한다. -`yarn add @babel/core --dev` -`npm install @babel/core --save-dev`

- dependencies는 프러덕션과 직접적인 관련이 있다. 여기서 `npm`을 사용해서 설치할 때에는 반드시 `--save` 옵션을 줘야 한다. 이렇게 하면, dependency에 기록된다. -`yarn add react` -`npm install --save react`
  이렇게 `--save`를 하는 이유는 일반적으로 git에선 node 모듈들이 제외대상이 되기 때문에, 우리가 clone해서 `npm install`을 하는 이유는 `package.json`에 기록되어 있는 dependency를 바탕으로 설치하기 위함이다. `git clone`을 해도 node모듈이 함께 담겨서 오진 않으니깐 npm으로 알아서 설치해주는 것이다. 만일 dependency에 등록이 안 되어 있고, 코드에서 사용되는 모듈이 있다면? `npm install`을 해도 설치가 해당 모듈은 설치가 되지 않고, 코드를 실행할 때에 오류가 발생할 것이다.
- [package-lock.json이란?](https://junwoo45.github.io/2019-10-02-package-lock/)

## 서버 만들기

```js
// server.js

const http = require("http"); // node.js의 모듈 http

const server = http.createServer((req, res) => {
  res.writeHead(200, { "content-type": "application/json" });
  res.end(JSON.stringify("Hello World!"));
});

console.log("Listening on http://localhost:3000");
server.listen(3000, "localhost");

// node server.js 를 터미널에 실행해주고,
// http://localhost:3000 으로 접속하면,
// 서버가 실행되고 있음을 알 수 있다.

// 또한 JSON형식으로 출력되는 것을 알 수 있는데,
// JSON형식으로 데이터를 주고받는 것이 일반적이다.
```

# Node.js module

## Node.js 내장 모듈을 사용하는 방법

모듈이란, 어떤 기능을 떼서 조립할 수 있는 형태로 만든 부분이다. 모듈은 이해하는 컴퓨터 지식의 범위만큼 사용할 수 있고, Node.js에는 다양한 모듈들이 내장되어 있다. 그렇기에 사용하고자 하는 기능을 가진 모듈을 언제든지 가져와 사용할 수 있다.

### fs.readFile 사용하기

다양한 모듈 중에서도 파일 시스템 모듈은 파일을 읽거나 저장하는데 쓸모있는 모듈이다.
그중 `readFile`이라는 메소드를 예로 들어서 어떻게 모듈을 불러와 사용 할 수 있는지를 살펴보자.
먼저 모듈을 사용하고 싶으면, 이를 불러오는 과정은 필수적이다. 예전에 브라우저에서는 `<script>`태그를 사용해서 `src =`에 불러오고 싶은 JS파일을 넣었다면, Node.js에서는 JS 코드 가장 상단에 `require`를 이용해서 불러올 수 있다.

```js
const fs = require("fs"); // 파일 시스템 모듈을 불러올 수 있다.

// 아래선 파일 시스템 모듈에 속한 메소드를 마음껏 사용할 수 있다!
fs.readFile("/path/to/myBook", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

공식 문서를 살펴보면 각 메소드마다의 사용법이 다른 것을 확인할 수 있다. fs.readFile에서는 다음과 같은 인자를 넣어줄 수 있는데,

- `path`: 파일 주소 (다양한 타입으로 넘길 수 있지만, 주로 문자열로 넘긴다.)
- `options`: 대괄호로 감싼 두번째 인자 `options`는 생략이 가능하다. 여기서는 사용한다면 객체 혹은 문자열로 전달해주고, 인코딩 방식을 넘긴다. ex) `utf8`
- `callback` 함수: 파일을 읽고 난 후에 비동기적으로 실행되는 함수이다. 콜백 함수에는 두가지 파라미터가 존재하는데, err와 data가 있다. 에러가 발생하지 않으면 err는 `null`값으로 처리되고, `data`에 문자열이나 Buffer하는 객체가 전달된다. 공식문서에 나와있듯이 `data`의 타입은 인코딩을 설정해주었냐에 따라 달라진다.

## 3rd-party 모듈을 사용하는 방법

3rd-party란 공식적으로 제공하는 것이 아닌 다른 모든 '제3자'의 것을 말한다. Node.js 공식 문서에 제공되지 않는 모든 것은 전부 3rd-party라고 할 수 있다. 이때는 모듈을 `npm`을 이용해 설치한 이후에 node.js 내장 모듈을 사용하듯 `require`를 통해 사용할 수 있다.

## Node.js에서 경로를 다룰 때 유용한 모듈

- `__dirname`: 현재 파일의 디렉토리 경로를 알려준다. 또한 `__dirname`은 글로벌 객체이기 때문에 따로 import 할 필요 없이 사용할 수 있다.
- `__path`: 파일 및 디렉토리 경로 작업을 위한 유틸리티를 제공한다.

# 참고

- [npm 파일시스템 블로그 1](https://niceman.tistory.com/98)
- [node.js 내장 모듈 목록](https://nodejs.org/dist/latest-v12.x/docs/api/)
- [파일 시스템 모듈](https://nodejs.org/dist/latest-v12.x/docs/api/fs.html)
- [How to use \_\_dirname in Node.js](https://www.digitalocean.com/community/tutorials/nodejs-how-to-use__dirname)
- [Path 모듈](https://nodejs.org/api/path.html#path_path)

# CommonJS

범용적이니 목적으로 JavaScript를 사용하기 위해 모듈화를 진행하는데, CommonJS는 JS 모듈화 작업의 선두 주자이다.
CommonJS를 이용하여 모듈을 내보내거나/불러올 수 있다.
모듈화는 세 가지 부분으로 이루어지는데:

- 스코프(Scope): 모든 모듈은 자신만의 독립적인 실행 영역이 있어야 한다.
- 정의(Definition): 모듈 정의는 전역객체인 exports 객체를 이용한다.
- 사용(Usage): 모듈 사용은 require 함수를 이용한다.

다음과 같이 내보낼 수 있고,

```js
// foo.js
exports.foo = () => { ... };

// bar.js
exports.bar = () => { ... };

// baz.js
exports.baz = () => { ... };
```

다음과 같이 불러와 사용할 수 있다.

```js
const foo = require("./js/foo");
const bar = require("./js/bar");
const baz = require("./js/baz");
```

#### 한 가지 중요한 점: module.exports vs exports

모듈을 보내는 데는 두 가지 표현 방식이 있는데, 둘 다 사용방식은 같다.
원래는 module.exports만 있었는데, 조금 더 짧게 사용하고자 exports가 생겼다. 아무거나 사용하면 되지만, 한 가지 주의할 점은 이 둘을 섞어 사용하면 안 된다. 그 이유는 exports는 module.exports 사용을 도와주는 helper로써 module.exports를 참조할 뿐이다. 만일 섞어 사용하면서, module.exports에 뭔가 있다면, exports는 무시되고 만다.

# 참고

- [JavaScript 표준을 위한 움직임: CommonJS와 AMD](https://d2.naver.com/helloworld/12864)

# How to debug Node app

서버 개발을 돕는 다양한 툴들이 있다.

## Nodemon

Nodemon은 서버를 켰을 때 JS파일의 변경상황을 실시간으로 그때그때 보여준다. 서버 관련 프로젝크를 진행할 때 매우 유용하다. `npm install --save nodemon` 명령어로 nodemon을 설치할 수 있다.

### inspect 옵션을 이용한 디버깅

Node 혹은 Nodemon을 설치한 후에 package.json파일의 script 부분에서 nodemon에 `nodemon --inspect` 혹은 `nodemos --inspect-brk` 옵션을 넣어서 사용할 수 있다. 인스팩트를 한 결과는 콘솔창에 node 아이콘이 생성되는데, 여기를 통해 확인할 수 있다. 이후에 postman을 이용해 요청하고 inspect를 통해서 확인할 수 있다.

## Postman

개발한 API를 테스트하고, 테스트 결과를 공유하여 API 개발의 생산성을 높여주는 플랫폼이다.

# 참고

- [POSTMAN 활용법](https://meetup.toast.com/posts/107)
- [how to debug node app 공식문서](https://nodejs.org/en/docs/guides/debugging-getting-started/)

> Chatterbox Server 스프린트 때 도움을 받은 자료 모음

# Node.js & Server

- [node.js - HTTP 트랜잭션 해부](https://nodejs.org/ko/docs/guides/anatomy-of-an-http-transaction/)
- [How can I read POST data?](https://nodejs.org/ko/knowledge/HTTP/servers/how-to-read-POST-data/)
- [node.js - API for Stream Consumers](https://nodejs.org/api/stream.html#stream_api_for_stream_consumers)
- [How to allow CORS with Node.js (without using Express)](https://stackoverflow.com/questions/44405448/how-to-allow-cors-with-node-js-without-using-express)
- [node.js 서버 만들기 블로그 1](https://velog.io/@wimes/node.js-REST-API-%EC%84%9C%EB%B2%84-%EB%A7%8C%EB%93%A4%EA%B8%B0-3.-%EB%A7%8C%EB%93%A4%EA%B8%B0#404-%EC%97%90%EB%9F%AC)
- [node.js를 이용한 api 서버 만들기 블로그 2](http://52.78.22.201/tutorials/nodejs/api-server-by-nodejs-03/)
- [body-parser에 관하여 블로그 3](https://medium.com/@chullino/1%EB%B6%84-%ED%8C%A8%ED%82%A4%EC%A7%80-%EC%86%8C%EA%B0%9C-body-parser%EB%A5%BC-%EC%86%8C%EA%B0%9C%ED%95%A9%EB%8B%88%EB%8B%A4-%ED%95%98%EC%A7%80%EB%A7%8C-body-parser%EB%A5%BC-%EC%93%B0%EC%A7%80-%EB%A7%88%EC%84%B8%EC%9A%94-bc3cbe0b2fd)
- [Node.js - API - HTTP](https://nodejs.org/dist/latest-v13.x/docs/api/http.html)
- [Node.js에서 이메일 보내기 nodemailer](https://www.npmjs.com/package/nodemailer)
- [[Back-end] Node.js에서 메일 전송하기 (feat. Nodemailer & Gmail)](https://velog.io/@josworks27/Back-end-Node.js%EC%97%90%EC%84%9C-%EB%A9%94%EC%9D%BC-%EC%A0%84%EC%86%A1%ED%95%98%EA%B8%B0-feat.-Nodemailer-Gmail)
- [Request - Simplified HTTP client](https://github.com/request/request)
