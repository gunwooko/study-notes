# 🤔 Authentication & Authorization?

HTTP의 stateless하고 connectionless한 특성으로 서버와 클라이언트는 연속적으로 통신을 할 수 없다. 그렇기에 권한 부여(authorization)을 구현하려면, 새로운 요청이 있을 때마다 매번 인증(authentication) 작업을 해 주어야 하는데, 이에 대한 보완책이 바로 쿠키(cookie)와 세션(session)이다. 세션과 쿠키는 별개의 개념이 아니다. 세션 또한 쿠리를 기반으로 하고, 서버에서 세션id가 생성되면, 응답시 쿠키에 세션id를 담아 클라이언트에 전달한다.

## 😯 인증과 권한부여의 차이

- 🕵‍♂ 인증(authentication): 카드키를 찍는 행동 혹은 과정 "너는 누구냐?"
  사용자가 누구인지 확인하는 절차이다. 로그인을 통해 신원을 확인한다.
- 👨‍🔧 권한부여(authorization): 카드키를 가지고 어떤 방에 들어가는 것 "어디까지 갈거냐?
  권한부여는 사용자의 신원이 성공적으로 인증된 후에 발생한다. 권한부여는 누가 무엇을 할 수 있는지 결정하는 규칙이다.

## 🧐 Authentication

가장 일반적인 인증 방법은 비밀번호를 사용하는 것이다. 또한 비밀번호 없이 사용자가 소유하고 있는 휴대폰인증, OTP인증, 등이 있고 사용자 고유의 생체기반 인증도 있다.

### SSO (Single Sign On)

한번의 시스템 인증을 통해 재인증 없이 다양한 시스템에 접근할 수 있는 방식이다.

### OAuth

소셜 네트워킹 플렛폼의 기존 자격 증명을 확인하고 인증하는 방식이다. (깃허브, 페이스북, 구글, 네이버, 카카오 로그인, 등)

## 🧐 Authorization

Session, [JWT](https://jwt.io/) 등을 이용해 인증을 확인하고, 서버가 해당 권한을 확인해 접근을 결정한다.

## Cookie

Cookie는 사용자의 정보를 사용자 메모리(브라우저)에서 관리한다.
서버가 사용자의 위치에 정보를 저장하고 불러올 수 있는 수단이다.

1. 특정 호스트에서 생성된 쿠키는 이후 모든 요청마다 서버로 다시 전송된다.
2. 이름, 값, 만료 날짜, 경로 정보로 구성되어 있다.
3. 필요할 때 참조나 재사용이 가능하다.
4. 4KB 이하 저장 가능하다.

## Session

일정 시간동안 동일한 사용자에 대한 상태 정보를 유지시키는 것. 즉, 클라이언트와 서버가 연결되어 있다 혹은 그 session이 유지되어 있다. 방문자(브라우저)가 웹서버에 접속하게 되면 방문자의 요구에 따른 (교류를 하고 있다) 정보를 저장하는 것을 말한다. Session은 사용자의 정보를 사용자 쪽이 아닌 서버 상에서 관리(저장)한다. 여기서 일정 시간이란 방문자가 웹 브라우저를 통해 웹 서버에 접속한 시점으로부터 웹 브라우저를 종료하여 연결을 끝내는 시점을 말한다.
서버와 클라이언트의 연결이 활성화 된 상태

1. 서버가 클라이언트에 대해 유일한 session ID를 부여하여 클라이언트를 구별하고, 웹 서버의 세션 스토리지에 세션 정보가 저장된다.
2. 일반적으로 이 유일한 클라이언트 ID가 서버에서 존재하는 상황을 Session이라고 말한다.
3. 각 클라이언트 ID의 Session 객체마다 Data를 관리할 수 있다.
4. 사용자의 정보 중 보안상 중요한 데이터는 Session을 이용해 서버에서 관리한다.
5. 데이터 저장 제한 없다.
6. 통신에만 발동되는 쿠키, 세션 쿠키라고도 한다.

## Token

인증을 위해 사용되는 암호화 된 문자열이다.

1. HTTP 통신의 Stateless 특징과 알맞다.
2. 유저의 인증 정보를 서버나 세션에 담아주지 않는다. 토큰 인증에서, 서버는 JWT(JSON Web Token)을 생성하여 클라이언트에 보낸다.
3. 클라이언트는 JWT를 로컬 스토리지 또는 쿠키에 저장하고, 세션과 마찬가지로 사용자가 보내는 모든 요청에 포함된다.
4. 유저의 활성화 여부를 신경쓰지 않고 넘겨진 요청에 담겨진 Token의 정합성만을 확인한다.
5. 서버에서 클라이언트의 상태 정보를 저장하지 않고 클라이언트에서 넘겨지는 요청만으로 작업을 처리하게 되는데 이런 경우 클라이언트 상태관리에 관한 비용이 없기 때문에 서버의 확장성이 높다. 즉, 세션 인증에서 서버가 세션 정보를 관리했던 것과 달리, 서버는 JWT를 저장하지 않고, 다만 토큰이 유효한지 여부만을 확인할 뿐이다. 또한 JWT를 추가적으로 저장할 공간이 필요 없기 때문에, 서비스가 커진다 하더라도, 서버에 추가적인 부하가 발생하지 않아 더욱 효율적이다.

### JWT를 안전하게 저장하기

- [JWT.IO](https://jwt.io/)
- [[Node.js / JWT] Express.js 서버에서 JWT 기반 회원인증 시스템 구현하기](https://velopert.com/2448)
- [Node.js & Express에서 JWT(JSON Web Token) 사용하기 -2-](https://tech.songyunseop.com/tags/jwt/)
- [Using JWT (JSON Web Tokens) to authorize users and protect API routes](https://medium.com/@maison.moa/using-jwt-json-web-tokens-to-authorize-users-and-protect-api-routes-3e04a1453c3e)

## 암호화(Encryption)

### 암호화란?

암호화는 일련의 정보를 임의의 방식을 사용하여 다른 형태로 변환하여 해당 방식에 대한 정보를 소유한 사람을 제외하고 이해할 수 없도록 '알고리즘'을 이용해 정보를 관리하는 과정.

## Hashing

하나의 문자열을 다른 값이나 키로 변환하는 단방향 암호화 기법이다. 어떠한 문자열에 '임의의 연산'을 적용하여 다른 문자열로 변환하는 것. 즉, 암호화해서 서로 주고 받는 것. 예를 들어 개인의 민감한 정보(비밀번호, 연락처, 등)를 그대로 노출 시키지 않고 한눈에 알아볼 수 없는 문자열로 변환하여 주고 받을 때 사용한다. 주로 Hashing은 서버 로직 내에서 이루어 지며 상대적으로 정보가 노출되기 쉬운 클라이언트 상에서의 보안을 신경쓰기 위해 사용된다.

#### Hashing을 하는데 몇 가지 조건/특징이 있다:

1. 모든 값에 대해 해시 값을 계산하는데 오래걸리지 않아야한다. (로그인하는데 10초가 걸릴 순 없는 일이다.)
2. 최대한 해시 값을 피해야하며, 모든 값은 고유한 해시 값을 가진다. (극히 드물지만, 전혀 다른 문자열이지만 같은 해시 값을 가진 경우가 있을 가능성이 있지만, 이것을 피해야한다.)
3. 아주 작은 단위의 변경이라도, 완전히 다른 해시 값을 가져야한다.

### 양방향 암호화: cipher

[Node: crypto - cipher](https://nodejs.org/api/crypto.html#crypto_class_cipher)

## Salting

해시 하려는 값(원본)에 추가하는 값.

1. 암호화를 진행했다면 '해당 알고리즘을 알고 있는 순간' 바로 원본을 얻어낼 수 있다. 그렇기에 그냥 해시만 사용하기에는 불안하다.
2. 원본 값에 임의로 약속된 추가 문자열을 추가하여 해시를 진행하여 기존 해시값과 전혀 다른 해시 값이 반환되어 알고리즘이 노출되더라도 원본 값을 보호할 수 있도록하는 안전장치이다.
3. 기존이라면 (암호화 하려는 값) => (해시 값)
   Salt 사용하면 (암호화 하려는 값) + (Salt 용 값) => (해시 값)
4. crypto 모듈에서는 pbkdf2(Password-Based Key Derivation Function 2)라는 비동기 메소드를 통해 솔트를 적용해 할 수도 있다.

```js
const crypto = require("crypto");
crypto.DEFAULT_ENCODING = "hex"; // hex로 인코딩한다.
// password, salt, iteration, 바이트 길이, 알고리즘, 콜백을 인자로 받는다.
crypto.pbkdf2("secret", "salt", 100000, 512, "sha512", (err, derivedKey) => {
  if (err) throw err;
  console.log(derivedKey); // '3745e48...aa39b34'
});
```

5. 만약 솔트 값이 고정되어 있다면, 유출 위험이 있다. 따라서 암호화 할 때마다 랜덤한 솔트 문자열을 생성한다면 좋을 것이다. 이와 관련하여 crypto에서 사용할 수 있는 메소드가 `randomBytes`이다.

```js
// 랜덤한 솔트를 64바이트 길이로 생성한다. 버퍼 형식으로 반환된다.
crypto.randomBytes(64, (err, buf) => {
  // 랜덤하게 생성된 버퍼를 base64를 통해 인코딩한다.
  const randomlyGeneratedSalt = buf.toString("base64");
  crypto.pbkdf2(
    "블루베리",
    randomlyGeneratedSalt,
    123456,
    64,
    "sha512",
    (err, derivedKey) => {
      if (err) throw err;
      console.log(derivedKey.toString("hex"));
    }
  );
});
// 랜덤으로 생성된 솔트는 해싱된 값(derivedKey)와 반드시 함께 저장해야 한다.
```

### Salt 해시 외의 방법: HMAC

- [Node: crypto - createHMA 메소드](https://nodejs.org/api/crypto.html#crypto_crypto_createhmac_algorithm_key_options)

## Crypto (NodeJS)

[NodeJS 내장 암호화 모듈이다.](https://nodejs.org/api/crypto.html)

```js
// 예시
const crypto = require("crypto"); // crypto 모듈을 가져온다.

const secret = "abcdefg";
const hash = crypto
  .createHmac("sha256", secret)
  // 'sha256'은 알고리즘 방식
  // secret은 Salt이다.
  .update("I love cupcakes")
  // hashing 할 값
  .digest("hex");
// 인코딩 방식 'hex'=> 16진수 (참고로 16진수에서 가장 큰수가 f이다)
console.log(hash);
// Prints:
//   c0fa1bc00531bd78ef38c628449c5102aeabd49b5dc3a2a516ea6ea959d6658e

// 값 + Salt =>
// 알고리즘으로 값을 변환하고 =>
// 변환 값을 입력 받은 방식으로 인코딩 =>
// Hash 값이 나온다.
```

## 이슈

- [비밀번호 안전도 검사](https://password.kaspersky.com/)
- [How secure is 256 bit security?](https://www.youtube.com/watch?v=S9JGmA5_unY&feature=youtu.be)
- [왠만한 암호 해싱](https://crackstation.net/)
- [안전한 패스워드 저장](https://d2.naver.com/helloworld/318732)
- [Salt vs Pepper](https://simplicable.com/new/salt-vs-pepper)
- [프론트에서 안전하게 로그인 처리하기 (ft. React)](https://velog.io/@yaytomato/%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%90%EC%84%9C-%EC%95%88%EC%A0%84%ED%95%98%EA%B2%8C-%EB%A1%9C%EA%B7%B8%EC%9D%B8-%EC%B2%98%EB%A6%AC%ED%95%98%EA%B8%B0)

# 참고

- [npm express-session](https://www.npmjs.com/package/express-session)
- [쿠키, 세션, 캐시란 무엇인가? - 영상](https://www.youtube.com/watch?v=OpoVuwxGRDI)
- [Difference between Cookie and Session](https://medium.com/@peterchang_82818/difference-session-cookie-token-vs-token-authentication-based-traditional-store-a177e8474ee3)
- [쉽게 알아보는 서버 인증 1편(세션/쿠키 , JWT)](https://tansfil.tistory.com/58)
- [authentication, session/token 블로그](https://velog.io/@naseriansuzie/imcourseTIL23#3-%ED%86%A0%ED%81%B0token%EC%9D%B4%EB%9E%80)
- [쿠키(Cookie)와 세션(Session) & 로그인 동작 방법](https://cjh5414.github.io/cookie-and-session/)
- [Node.js와 Cookie/Session으로 사용자 정보 저장 — Part 2](https://medium.com/wasd/node-js%EC%99%80-cookie-session%EC%9C%BC%EB%A1%9C-%EC%82%AC%EC%9A%A9%EC%9E%90-%EC%A0%95%EB%B3%B4-%EC%A0%80%EC%9E%A5-part-2-dbe84c2f13e4)
- [[Nodejs] [Express] 세션(Session) 사용하기](https://m.blog.naver.com/PostView.nhn?blogId=pjok1122&logNo=221555161680&categoryNo=0&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [Express에서의 Session 사용법](https://netframework.tistory.com/entry/Express%EC%97%90%EC%84%9C%EC%9D%98-Session-%EC%82%AC%EC%9A%A9%EB%B2%95)
