# Web Architecture

## Client && Server

웹 아키텍쳐를 말하기에 앞서 웹이 작동하기 위해 필요한 체계와 같은 클라이언트와 서버를 알아야 한다. 현재 내가 사용하는 컴퓨터는 클라이언트가 될 수도 있고, 서버가 될 수도 있다. 물론 서버 컴퓨터는 안정성이 매우 중요하지만 각자 우리가 사용하는 컴퓨터 또한 서버가 될 수 있다. 그렇다면 어떤 컴퓨터가 서버고 클라이언트가 되는가?
웹브라우저가 설치된 컴퓨터를 클라이언트, 그리고 웹서버가 설치된 컴퓨터를 서버라고 부를 수 있다. 예를 들어 브라우저에 검색창에 웹주소를 적어서 보내면, 서버에서는 해당하는 웹주소의 정보를 브라우저로 응답한다. 즉, 요청하는 쪽이 클라이언트 응답하는 쪽이 서버라고 할 수 있다. 서버는 클라이언트의 요청을 받음과 동시에 또한 그 요청을 처리하기 위해서 데이터베이스와 통신하여 데이터를 꺼내와 응답한다. 한 가지 중요한 것은 서버는 클라이언트의 요청을 무시해서는 안 된다. 반드시 한 요청에는 한 응답이 따르는데, 잘못된 요청이라도 잘못됬다고 응답해주어야 한다.

#### 참고

- [MDN - 웹의 동작 방식](https://developer.mozilla.org/ko/docs/Learn/Getting_started_with_the_web/%EC%9B%B9%EC%9D%98_%EB%8F%99%EC%9E%91_%EB%B0%A9%EC%8B%9D)
- [클라이언트와 서버 관련 블로그 1](https://medium.com/@yms0214/%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8%EC%99%80-%EC%84%9C%EB%B2%84-3eb20cc2516b)

## Browser

브라우저는 프로그래밍 언어가 구동되는 환경, 즉 노드와 같은 런타임이다. 예를 들면, 자바스크립트로 작성한 클라이언트 코드를 브라우저에서 구동하여 모두가 볼 수 있는 view 단을 완성하는 역활을 주로 담당한다. 즉, 클라이언트가 요청(request)하면, 서버로부터 응답(response)을 받아볼 수 있게 한다.

- [브라우저는 어떻게 동작하는가](https://d2.naver.com/helloworld/59361)

## 데이터베이스

서비스의 모든 리소스를 저장하는 공간이다.

# 참고

- [Web Architecture 101](https://scvgoe.github.io/2018-12-25-%EB%B2%88%EC%97%AD-Web-Architecture-101/)

# API(Application Programming Interface)

서버에서 정의한 API 문서를 통해, 서버가 제공하는 리소스를 이용할 수 있다. API를 활용해서 UI를 만들 수 있다. 즉, 서버 자원을 잘 가져다 사용할 수 있게 만들어놓은 interface이다. 서버 측에서 API를 설계해 놓으면, 클라이언트는 API를 보고서 데이터베이스의 정보를 요청할 수 있다.

## RESTful API?

Representational State Transfer의 약자로 HTTP 메소드(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation(Create, Read, Update, Delete)을 적용하는 행위를 의미한다. 즉, 웹 서비스를 만드는데 사용되는 제약 모음이다.
클라이언트가 서버와 HTTP 요청과 응답을 통해서 교류를 할 수 있고, 서버에서 준비한 API를 통해서 클라이언트 측에서 API 규칙에 따라 요청을 보낼 수 있다. 리소스마다 서로 다른 API 규칙이 생기게 되고, 서버마다 다른 API 규칙이 생기게 되면 각 조건을 맞춰주는 것이 힘들게 된다. 그렇기에 REST란 제약을 만들어서 API의 규칙을 조금 더 통일성 있게 만들어 준다.

## 참고

- [API 기초 설명 by 노마드코드](https://www.youtube.com/watch?v=iyFHfzCRHA8&t=)
- [API 란](https://medium.com/@dydrlaks/api-%EB%9E%80-c0fd6222d34c)
- [REST API의 장단점](https://wallees.wordpress.com/2018/04/19/rest-api-%EC%9E%A5%EB%8B%A8%EC%A0%90/)
- [What is REST - Part1: Introduction](https://medium.com/extend/what-is-rest-a-simple-explanation-for-beginners-part-1-introduction-b4a072f8740f)
- [REST API란](https://velog.io/@wlsdud2194/HTTP-REST-API-%EB%9E%80)
- [REST API가 뭔가요? by 얄팍한 코딩사전](https://www.youtube.com/watch?v=iOueE9AXDQQ)
- [당신의 API가 RESTful하지 않은 5가지 증거](https://beyondj2ee.wordpress.com/2013/03/21/%EB%8B%B9%EC%8B%A0%EC%9D%98-api%EA%B0%80-restful-%ED%95%98%EC%A7%80-%EC%95%8A%EC%9D%80-5%EA%B0%80%EC%A7%80-%EC%A6%9D%EA%B1%B0/)
- [그런 REST API로 괜찮은가 - youtube영상](https://www.youtube.com/watch?v=RP_f5dMoHFc)

# HTTP

"HyperText Transfer Protocol"의 약자로서 클라이언트와 서버가 지켜야 할 규약인데, 다른말로 서로 통신할 때 사용하는 규칙이다. 서버와 클라이언트가 요청과 응답을 주고받을 때 어떻게 해야 하는지를 알려준다.
HTTP는 주로 HTML 문서를 주고받는 데에 쓰이며, TCP와 UDP를 통해 이루어지고, 80번 포트를 사용한다.

- [TCP](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%86%A1_%EC%A0%9C%EC%96%B4_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C): Transmission Control Protocol의 양자로, 근거리 통신망이나 인트라넷, 인터넷에 연결된 컴퓨터에서 실행되는 프로그램 간에 일련의 옥텟(커퓨팅에서 8개의 비트가 한데 모인 것, 초기 컴퓨터들은 1바이트가 꼭 8비트만을 의미하진 않았지만, 요즘에는 바이트하고 같은 의미가 되었다.)을 안정적으로, 순서대로, 에러 없이 교환할 수 있게 한다. TCP는 웹 브라우저들이 WWW(World Wide Web)에서 서버에 연결할 때 사용되며, 이메일 전송이나 파인 전송에도 사용된다.
- [UDP](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9A%A9%EC%9E%90_%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C): User Datagram Protocol의 약자로 TCP의 안정성이 필요하지 않는 애플리케이션의 경우 일반적으로 UDP를 사용하는데, 이것은 전달 확인 및 순차 보장 기능이 없는 대신 [오버헤드](<https://ko.wikipedia.org/wiki/%EC%98%A4%EB%B2%84%ED%97%A4%EB%93%9C#:~:text=%EC%98%A4%EB%B2%84%ED%97%A4%EB%93%9C(overhead)%EB%8A%94%20%EC%96%B4%EB%96%A4,%EC%8B%9C%EA%B0%84%20%C2%B7%20%EB%A9%94%EB%AA%A8%EB%A6%AC%20%EB%93%B1%EC%9D%84%20%EB%A7%90%ED%95%9C%EB%8B%A4.>)가 작고 지연시간이 짧다는 장점이 있다. 또한 UDP는 일반적으로 오류의 검사와 수정이 필요 없는 애플리케이션에서 수행할 것으로 가정한다.

## HTTP : 작동 방식

항상 요청과 응답의 형식으로 이루워져있다. 서버는 클라이언트의 요청을 무시해서는 안 된다. 요청하는 리소스가 없다거나, 잘못된 요청일 경우도 반드시 클라이언트에 응답해줘야 한다.

## HTTP : 구성

기본적으로 HTTP 요청(request)은 Header와 Body를 가지고 있다.

- Header에서는 주로 어디서 보내는 요청인가(origin), 컨텐츠 타입은 무엇인가(content-type), 어떤 클라이언트를 이용해 보냈는가(user-agent)등이 담겨있다.
- Body는 가지고 있는 메소드도 있고 아닌 메소드도 있지만, 서버에 데이터를 보내기 위한 공간으로 활용된다.
  위와 같이 HTTP 응답(response) 또한 Header와 Body를 가지고 있다.
  HTTP 메세지의 시작 줄과 HTTP 헤더를 묶어서 요청 헤드(head)라고 부르며, HTTP 메세지의 페이로드 영역은 본문(body)이라고 한다.

![](https://images.velog.io/images/gunwooko/post/b060e392-1b0b-48a2-82f6-8458f1251824/IMG-7255.jpg)

### HTTP Header : Content-Type

응답 내에 있는 컨텐츠 타입 헤더는 클라이언트에게 반환된 컨텐츠 유형이 실제로 무엇인지 알려준다. 브라우저들은 어떤 경우에는 MIME 스니핑을 해서 이 헤더의 값을 꼭 따르지 않을 경우가 있다. 이런 경우를 막고 싶다면 [`X-Content-Type-Options`](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/X-Content-Type-Options) 헤더를 `nosniff`으로 설정할 수도 있다.
MIME 스니핑이란 MIME 타입이 없을 때, 혹은 클라이언트가 타입이 잘못 설정됐다고 판단한 어떤 경우에, 브라우저들은 MIME 스니핑을 시도할 수도 있다. 이는 리소스를 훑어보고 정확한 MIME 타입을 추축해는 것이다.

- [MDN - Content-Type](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Content-Type)
- [MDN - MIME 타입](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)
- [MDN - MIME 타입 목록](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)

## HTTP : Properties

- Stateless: 각 처리(요청과 응답)는 모두 독립적이다. 문맥이 형성되지 않는다. 즉, 각 처리는 서로가 어떤 것을 했는지 모른다. (\*이 부분을 보안하기 위해 인증이란 것을 사용한다).
- Connectionless: 한 번의 요청에는 한 번만 응답한다. 응답 이후에는 연결이 끊기기 때문에, 더이상 응답할 수 없다.

## HTTP : Methods

- GET : 서버에 자원을 요청할 때
- POST : 서버에 자원을 생성할 때 (서버에 input data를 보내기 위함)
- PUT : 서버의 자원을 수정할 때 (완전 변경/요청된 url이 존재하지 않을 경우, 새로운 리소스를 생성 )
- PATCH : 서버의 자원을 수정할 때 (부분 변경)
- DELETE : 서버의 자원을 제거할 때
- OPTIONS : Target 서버의 지원 가능한 메소드를 알아보기 위해 사용
  curl을 이용해서 OPTIONS 요청을 서버에 보냄으로 서버에서 지원하는 메소드를 확인할 수 있다.
  `curl -X OPTIONS http://example.org -i`
  요청을 보내면, 응답에 `Allow`헤더가 포함되어서 오는데, 이를 통해 허용되는 메소드를 확인할 수 있다.
  또한 CORS에서 OPTIONS 메소드를 통해 Preflight(사전전달/사전요청)을 보내 서버가 해당 parameters를 포함한 요청을 보내도 되는지에 대한 응답을 줄 수 있게 한다.
  -- `Access-Control-Request-Method`
  -- `Access-Control-Request-Headers`
  -- `Access-Control-Allow-Methods`

- HEAD : GET과 동일하지만, 서버에서 Body를 반환하지 않음.

GET / DELETE / PUT 메소드는 멱등성을 가진다. 즉, 여러 번 요청해도 결과는 같다/달라지지 않는다.
패킷은 header와 body의 묶음을 가리킨다.

POST는 methos, header, body만 있으면 잘 요청된다.

![](https://images.velog.io/images/gunwooko/post/9d28252a-cb00-4beb-a3c7-6975fbf8b5dd/_2019-12-03__12.06.36.png) 출처:코드스테이츠

### 참고

- [HTTP Methods 정리](https://medium.com/@lyhlg0201/http-method-d561b77df7)
- [MDN - OPTIONS](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods/OPTIONS)
- [MDN - HTTP Methods](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods)
- [HTTP 관련 블로그 1](https://joshua1988.github.io/web-development/http-part1/)
- [HTTP 관련 블로그 2](https://joshua1988.github.io/web-development/web-protocols/)

## HTTP : Status Code

HTTP 요청이 성공적으로 이루어졌는지, 혹은 서버나 클라이언트에서의 문제로 실패했는지 여부를 알려주는 역활을 한다.

- 100대 : 정보 응답 (정보 제공)
- 200대 : 성공 응답
- 300대 : 리다이렉션 메세지(url이 들어갔는데, 바로 이동할 때)
- 400대 : 클라이언트 에러 응답 (클라이언트가 서버에 잘못된 요청을 했을 경우)
- 500대 : 서버 에러 응답 (서버에서의 에러)

### 참고

- [MDN - HTTP Status Code 관련 디테일](https://developer.mozilla.org/ko/docs/Web/HTTP/Status)

# AJAX

"Asynchronous Javscript and XML"의 약자로 비동기적인 웹 제작을 위해, 정보 표현을 위한 HTML과 CSS, 동적인 화면 출력 및 표시 정보와의 상호작용을 위한 DOM, 자바스크립트 등의 기술 집합을 칭하는 용어이다(웹 개발 기법).
AJAX 이전에는 `form.html`를 이용해서 정보를 서버에 제출하면, 서버에선 `result.html`이라는 새로운 페이지를 보내줬다. 즉, 페이지를 전부 다시 로딩했었다. 이때 중복되는 HTML 코드를 다시 사용자에게 다시 전송하면서, 대역폭을 낭비하는 비효율이 자주 발생하게 됐다. 그렇기에 필요한 데이터만을 서버에 요청해서 받은후, 클라이언트에서 데이터 처리를 할 수 있게 해주는 것이 **AJAX**이다. 이로 인해 다이나믹한 웹 페이지가 등장했는데, 페이지 깜빡임 없이 원활하게 작동하는 자바스크립트와 DOM 그리고 서버와 자유롭게 통신할 수 있는 `XMLHttpRequest(XHR)`로 AJAX를 구성하게 되었다.
웹 서버에서 전적으로 이루어지던 데이터 처리 가운데 일부분을 클라이언트에서 담당하게 되어, 브라우저와 서버 사이에 교환되는 데이터양과 서버의 데이터 처리량이 줄어듦으로 인해, 애플리케이션의 응답성이 전반적으로 향상하게 되는 결과를 가져왔다.

- AJAX의 장점:
  a. 페이지 이동 없이 빠른 속도로 화면을 전환할 수 있다.
  b. 서버 처리를 기다리지 않고, 비동기 요청이 가능하다.
  c. 수신하는 데이터양을 줄이고, 클라이언트에게 처리를 위임할 수 있다.
- AJAX의 단점:
  a. AJAX를 쓸 수 없는 브라우저에 대한 문제
  b. HTTP 클라이언트의 기능이 한정적이다.
  c. 페이지 이동 없는 통신으로 인한 보안 문제가 발생할 수도 있다.
  d. 지원하는 Charset이 한정적이다. ([charset이란](https://meaningone.tistory.com/191))
  e. 요청을 남발하면 역으로 서버 부하가 늘 수 있다.

초반에는 XMLHttpRequest를 사용해서 서버의 자원을 가져왔지만, jQuery ajax로 조금 더 간편하게 코드를 작성하기 시작했다. 그러나 이것마저도 어렵다 해서, 더욱 쓰기 쉬운 표준 API를 만들자고 해서 **fetch API**가 만들어졌고 현재 많은 부분에서 fetch API가 활용되는 중이다.

## 참고

- [AJAX와 CORS 블로그 1](https://victorydntmd.tistory.com/37?category=677321)
- [MDN - AJAX 시작하기](https://developer.mozilla.org/ko/docs/Web/Guide/AJAX/Getting_Started)

# OSI 7 Layer [Network]

"Open System Interconnection"의 약자로 개방형 시스템 간 상호연결 모델을 뜻한다. ISO(국제 표준화 기구)에서 OSI 모델을 개발했다. OSI는 네트워크 간의 상호 접속을 용이하게 하기 위해 규정한 네트워크 프로토콜이라고 할 수 있다.
OSI 7 Layer은 네트워크에서 통신이 일어나는 과정을 7단계로 나눈 것인데, 이렇게 나눈 이유는 통신이 일어나는 과정을 단계별로 파악하기 위해서이고, 이렇게 파악할 수 있으면 네트워크 통신에 문제가 발생하더라도 해당 파트만 고치면 되기 때문이다.

#### 1. 물리 계층 (Physical Layer)

데이터를 전기신호로 바꿔주는 역활을 한다. ex) 케이블 종류, 무선 주파수, 전압, 물리 요건들이 포함된다.

#### 2. 데이터링크 계층 (Data-Link Layer)

데이터의 물리적인 전송을 담당한다.

#### 3. 네트워크 계층 (Network Layer)

네트워크 연결 및 경로 설정을 담당한다. 라우터 기능 대부분이 여기에서 이뤄진다. 이곳에서 패킷을 목적지까지 가장 빠른 길로 전송하는 역활을 담당한다.

#### 4. 전송 계층 (Transport Layer)

데이터이 전송을 담당한다. 보낼 데이터의 용량과 속도, 목적지 등을 처리하는데, 이곳에서 가장 잘 알려진 것이 TCP이다.

#### 5. 세션 계층 (Session Layer)

통신을 관리하고 책임지는 계층이다. 2대의 기기, 컴퓨터 또는 서버 간의 통신을 하기 위해서는 세션을 만들어야 하는데 이 작업이 이곳에서 처리된다.

#### 6. 표현 계층 (Presentation Layer)

코드 간의 번역을 담당한다. 즉, 데이터의 형식(format)을 정의한다. 일반적으로 응용프로그램 형식을 네트워크 형식으로 혹은 반대로 변환하는 것을 나타낸다. 서로 다른 환경의 컴퓨터와 어플리케이션이 데이터를 서로 이해할 수 있도록 도와주는 계층이다. 데이터의 압축, 암호화의 기능도 수행한다.

#### 7. 응용 계층 (Application Layer)

사용자가 직접 눈으로 보고 실제로 작업하는 계층이다. 사용자와 직접적으로 상호작용하는 모든 응용 프로그램들이 여기에 속한다. ex) 웹브라우저, HTTP, 등

## 참고

- [wikipedia - OSI](https://ko.wikipedia.org/wiki/OSI_%EB%AA%A8%ED%98%95)
- [OSI 관련 블로그 1](https://jw3461.tistory.com/4)
- [OSI 관련 블로그 2](https://sophia2730.tistory.com/entry/Network-OSI-7-Layer%EB%9E%80)
- [OSI 관련 블로그 3](https://yellowh.tistory.com/19)
- [OSI 관련 블로그 4](http://www.incodom.kr/OSI)
- [OSI 관련 블로그 5](http://www.ciokorea.com/news/36536)

# Browser Security

브라우저는 항상 위협을 받는다. 그 이유 중 하나는 자바스크립트를 구동하기 때문이다. 왜냐하면 자바스크립트로 할 수 있는 것들이 많기 때문이다. ajax call을 해서 api를 호출해서 데이터는 받거나 전송할 수도 있고, 다이다믹하게 DOM을 제어 할 수도 있고, 인증 정보를 브라우저에 저장하거나 불러올 수도 있기 때문이다. 브라우저의 보안에 위협이 되는 대표적인 공격은 두 가지가 있다.

## XSS

"Cross Site Scripting"의 약자로, 클라이언트가 서버를 신뢰하기 때문에 발생하는 이슈이다. XSS 공격에서 해로운 컨텐츠는 자바스크립트를 활용해 전달된다. 공격에 대상은 어플리케이션이 아닌 어플리케이션을 사용하는 유저가 되겠다. 즉, 클라이언트에 악성 스크립트를 주입하는 공격이다. 주로 `input`을 통해 XSS 공격이 이루어지는 경우가 많다. XSS는 웹 페이지에 악성 스크립트를 삽입하는 공격이다.

### 어떻게 XSS를 방지할 수 있을까?

클라이언트나 악성 자바스크립트를 잘 골라서 보호해줘야 한다. 요즘 최신 브라우저는 웬만한 XSS 공격은 막아준다. 또 다른 방어 방법으론:

- 정규 표현식을 사용한다.
- Text Content를 사용한다.
- Sanitize-HTML 라이브러리로 문서를 안전하게 해준다.

### 참고

- [owasp - XSS에 관하여](https://owasp.org/www-community/attacks/xss/)
- [XSS는 무엇인가? 블로그 1](https://2ssue.github.io/base/190407_PJI/)
- [XSS와 CSRF 블로그 2](https://medium.com/humanscape-tech/xss%EC%99%80-csrf-fe0e219b4c38)
- [XSS 설명 영상](https://www.youtube.com/watch?v=LfI6TAchgT4)
- [RegEx Tutorial - 정규표현식 튜토리얼](https://flaviocopes.com/javascript-regular-expressions/#introduction-to-regular-expressions)
- [정규표현식 연습장](https://www.regextester.com/96605)
- [JavaScript security best practices](https://wpvip.com/documentation/vip-go/vip-code-review/javascript-security-best-practices/)
- [XSS 예방법](https://gomakethings.com/preventing-cross-site-scripting-attacks-when-using-innerhtml-in-vanilla-javascript/)
- [npm-Path-to-RegExp](https://www.npmjs.com/package/path-to-regexp)
- [OWASP Cheat Sheet Series](https://github.com/OWASP/CheatSheetSeries)

## CSRF (or XSRF)

"Cross Site Request Forgery"의 약자로, 서버가 클라이언트를 신뢰해서 발생하는 이슈이다. CSRF는 사용자가 의도치 않은 작업을 웹 페이지에 요청하게 만드는 공격이다. 서버는 인증정보를 가지고 오면 상대를 믿는다. 여기서 사용자가 인증정보를 가진 체 해커의 링크 같은 것을 누르면, 해커는 인증정보를 가로채서 서버에 요청을 보낼 수 있다.
예를 하나 들면) 한 유저가 은행 사이트에 가입, 로그인하면 은행 서버에서 section token을 유저에게 준다. 그리고서 유저가 해커가 만들어놓은 어떤 페이지에(피싱 사이트) 접속하게 되면 해커가 유저의 인증 정보를 가로챈다. 그리고서 은행에 유저인 척하며 돈을 다른 곳으로 송금을 하거나, 피해자의 명의로 스팸 글을 게시한다거나, 계정 정보를 변경하는 등의 피해를 일으킨다. CSRF는 악성 스크립트를 이용해 사용자가 의도하지 않은 행위를 하도록 하는 공격이다.

### 어떻게 CSRF를 방지할 수 있을까?

CSRF는 서버에서 클라이언트가 잘못된 요청을 보내도 잘 걸러내야 한다. 클라이언트의 HTTP 요청에서 referrer 헤더를 확인하는 것이 대표적인 방어법이다. referrer 헤더에는 요청을 보낸 페이지의 정보가 담겨있는데, 이곳을 확인해 만약 다른 도메인에서 보낸 요청이라면 차단하는 방식으로 처리할 수 있다.
다른 방법으로는 Security Token을 사용하는 방법이 있다.

### 참고

- [CSRF 공격이란? 블로그 1](https://itstory.tk/entry/CSRF-%EA%B3%B5%EA%B2%A9%EC%9D%B4%EB%9E%80-%EA%B7%B8%EB%A6%AC%EA%B3%A0-CSRF-%EB%B0%A9%EC%96%B4-%EB%B0%A9%EB%B2%95)
- [owasp - CSRF에 관하여](https://owasp.org/www-community/attacks/csrf)
- [CSRF이란 블로그 2](https://medium.com/@ashifm4/protection-from-cross-site-request-forgery-csrf-9cf4f542e268)

## CORS 그리고 그의 필요성

### SOP (Same-origin policy)?

CORS를 알아보기에 앞서 먼저 SOP에 대해 알아보자. 현대 웹 브라우저들은 다양한 위험을 예방하기 위해 브라우저 보안 정책을 도입하고 있다. 그중 SOP는 Origin의 세 가지 요소(프로토콜, 호스트, 포트번호)가 일치하는 웹페이지 간의 상호작용만을 허용하는 보안 정책이다.
SOP는 비교적 단순하고, 철저하다는 장점이 있지만, 오늘날 웹 페이지 기술의 발달로 인해 외부 서버에 대한 리소스 요청이 많다. 즉, 이런 SOP의 지나친 엄격함이 오히려 불편해지게 된 것이다. 이렇게 해서 등장한 것이 CORS이다.

### CORS (Cross Origin Resource Sharing)

CORS는 origin 서버 바깥에 대한 리소스 요청을 관리하는 방법이다. CORS가 중요한 역활을 하는데, 누가 서버의 리소스에 접근할 수 있는지를 결정할 뿐 아니라, 어떤 방식으로 접근할 수 있는지를 명시하는 일 또한 해낸다. 예를 들어 HTTP 메소드 요청을 허용할지 안 할지를 정할 수 있다. 요약해서 말하면, 서버에서 allow하는 조건들을 다 맞추고 있는가? 사전에 서버에 확인하는 요청이다.
CORS는 HTTP헤더를 통해 외부로부터의 요청을 관리하는데, HTTP헤더에는 전송하는 요청 또는 응답에 대한 정보가 담겨있다. 그곳에서 CORS와 관련된 헤더를 통해 cross-origin 요청을 관리할 수 있다.

- Access-Control-Allow-Origin 헤더: 서버의 리소스를 어떤 외부 도메인과 공유할 것인지를 규정할 수 있다. 만일 값이 `*` 라면, 이 서버의 리소스에는 어떠한 도메인이라도 접근할 수 있다. 즉, 어떤 요청이 어떤 origin에서 와도 허용한다. 반대로 헤더 값이 특정한 도메인으로 설정되어 있으면, 해당 도메인의 접근만 허용된다.
- Access-Control-Allow-Credentials
- Access-Control-Allow-Headers
- Access-Control-Allow-Methods
- Access-Control-Expose-Headers
- Access-Control-Max-Age
- Access-Control-Request-Headers
- Access-Control-Request-Method
- Origin

### Preflight request란?

보통 GET 요청을 허용하는 서버는 많다. 그러나 서버의 리소스를 변경하는 요청이라면 아무래도 까다롭게 처리될 수밖에 없다.
PUT, DELETE, PATCH, POST 등 서버 리소스를 변경하는 메서드를 사용하는 HTTP 요청의 경우, 실질적인 요청 전에 OPTIONS 메서드를 통한 preflight 요청이 발생한다. 여기서 실제 요청이 안전한지를 서버가 사전에 파악할 수 있도록 하는 수단이다.
CORS를 처리하는 방법은 사용하는 언어와 벡엔드 프레임워크에 따라 다르다.

### CORS 해석

```js
const defaultCorsHeader = {
  // 모든 도메인(*)을 허용한다
  "access-control-allow-origin": "*",
  // 메소드는 다음의 것들만 허용한다
  "access-control-allow-methods": "GET, POST, PUT, DELETE, OPTIONS",
  // 헤더에는 content-type과 accept만 사용 가능하다
  "access-control-allow-headers": "content-type, accept",
  // preflight request는 10초까지 허용된다
  "access-control-max-age": 10,
};
```

### 참고

- [MDN - CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
- [Codeacademy - what is CORS?](https://www.codecademy.com/articles/what-is-cors)
- [CORS란 무엇인가? 블로그 1](https://im-developer.tistory.com/165)
- [CORS 관련 HTTP Response/Request Headers](https://homoefficio.github.io/2015/07/21/Cross-Origin-Resource-Sharing/)
  [CORS는 왜 이렇게 우리를 힘들게 하는 걸까? 블로그 2](https://evan-moon.github.io/2020/05/21/about-cors/)
- [CORS 그리고 간단한 해결방법 블로그 3](https://velog.io/@wlsdud2194/cors)
- [CORS가 나오게 된 배경 이야기 영상](https://www.youtube.com/watch?v=yTzAjidyyqs)
- [CORS에 대하여](https://velog.io/@wlsdud2194/cors)

# 참고

- [XSS와 CSRF에 관하여 블로그1](https://github.com/SeonHyungJo/FE-Dev-Note/blob/master/Security/XSS%EC%99%80%20CSRF.md)

# PRE - fetch API

Fetch API를 보기 전에 알아야 할 것:

- [AJAX](https://velog.io/@gunwooko/AJAX)가 무엇인지,
- [API](https://velog.io/@gunwooko/API)가 무엇인지

### XMLHttpRequest

XMLHttpRequest는 HTTP를 통해서 쉽게 데이터를 받을 수 있게 해주는 객체를 제공한다.

#### 참고하기

- [XMLHttpRequest 란? 블로그 1](https://ocsusu.tistory.com/60)
- [XMLHttpRequest 사용법 블로그 2](https://kamang-it.tistory.com/entry/RESTfulajaxajax%EB%9E%80-XMLHttpRequest%EC%82%AC%EC%9A%A9%EB%B2%95-1)
- [XMLHttpRequest란 무엇일까 블로그 3](https://enfanthoon.tistory.com/m/73?category=885107)
- [XMLHttpRequest란 블로그 4](https://whitekeyboard.tistory.com/343)
- [XMLHttpRequest 객체](http://www.ktword.co.kr/abbr_view.php?m_temp1=5939&id=1382)

# fetch API

`fetch API`는 다양한 네트워크 요청 중, URL로 요청하는 API이다. fetch API는 Promise 형식으로 이루어져 있다.  
Fetch에는 일반적인 객체로 Request와 Response가 포함되어 있다. 또한 CORS나 HTTP 오리진 헤더의 행동에 관련한 개념에 대해서도 정의되어 있다.
Fetch API를 이용하면 Request나 Response와 같은 HTTP의 파이프라인을 구성하는 요소를 조작하는 것이 가능한데, 아래와 같이 코드를 작성할 수 있다.

```js
// GET 요청을 할 때
fetch("http://exampleURL.com")
  .then((res) => {
    console.log(res);

    // res : Response의 instance로 여러 정보를 담고 있다.
    //       일단, 우리가 원하는 정보가 바로나오지는 않는다는 것을 인지할 수 있는데
    //       따라서, 우리가 원하는 정보로 다음 .then()으로 넘겨줘야 한다.
    //       res.json()을 통해 원하는 정보를 얻을 수 있다..

    return res.json();
  })
  .then((res) => {
    console.log(res);

    // res : 위의 .then()에서 return해준 결과를 뜻한다.
    //       원하는 정보는 객체형태로 얻었다. 그 이후 원하는 작업을 하면 된다.

    // ... todo something
  })
  .catch((err) => {
    // 에러를 잡아준다.
    console.error(err);
  });
```

```js
let promise = fetch(url, [options]);
```

- url: 접근하고자 하는 url
- options: 선택 매개변수, method나 header들을 지정할 수 있다. 만일 아무것도 넘기지 않으면 요청은 GET 메서드로 진행된다.

```js
// POST 요청 보낼 때
let response = await fetch("/article/fetch/post/user", {
  method: "POST", // HTTP 메서드
  headers: {
    "Content-Type": "application/json;charset=utf-8",
  },
  body: JSON.stringify(user),
});

let result = await response.json();
```

## 응답 객체의 프로퍼티

- `response.status` 응답의 HTTP 코드
- `response.ok` 응답 상태가 200과 299 사이에 있는 경우 `true`를 반환
- `response.headers` 맵과 유사한 형태의 HTTP 헤더

## 응답 객체 메소드

- `response.text()` 응답을 텍스트 형태로 반환
- `response.json()` 응답을 파싱해 JSON 객체로 변경
- `response.formData()` 응답을 FormData 객체 형태로 반환

# 참고

- [MDN - Using fetch](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Fetch%EC%9D%98_%EC%82%AC%EC%9A%A9%EB%B2%95)
- [javascript.info - fetch](https://ko.javascript.info/fetch)
- [hacks.mozilla의 Fetch API!](http://hacks.mozilla.or.kr/2015/05/this-api-is-so-fetching/)
- [Using fetch 블로그 1](https://velog.io/@ejchaid/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%99%80-%EB%B0%B1%EC%9D%98-%EB%8C%80%ED%99%94-Using-Fetch)
- [fetch 함수 블로그 2](https://velog.io/@luna238/Javascript-%EC%84%9C%EB%B2%84%EC%97%90-%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%A5%BC-%ED%98%B8%EC%B6%9C%EC%9A%94%EC%B2%AD%ED%95%98%EB%8A%94-fetch%ED%95%A8%EC%88%98)
- [[React / React Naive TIPS] axios 와 fetch 어떤 것을 사용할까?](https://hoorooroob.tistory.com/entry/React-React-Naive-TIPS-axios-%EC%99%80-fetch-%EC%96%B4%EB%96%A4-%EA%B2%83%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%A0%EA%B9%8C)
- [axios 와 fetch 어떤 것을 사용할까? 블로그 3](https://www.codestates.com/)
