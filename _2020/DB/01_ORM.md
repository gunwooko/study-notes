# ORM

Object Relational Mapping의 약자로, JS 객체와 관계형 데이터베이스의 데이터를 자동으로 맵핑, 즉 연결해주는 것을 말한다. OOP에는 클래스란 개념이 있고, RDBMS에는 테이블이란 개념이 있다. 이 둘의 형태는 서로 다르기 때문에 ORM을 이용해서 자바스크립트의 객체 형태로 데이터베이스를 다룰 수 있다. 즉, 관계형 데이터베이스를 객체처럼 쉽게 표현하자는 것이다.
ORM의 장점을 이해할 수 있다.

- 데이터베이스가 익숙하지 않은 개발자에게 도움을 준다.
- JS 파일을 SQL문을 사용하지 않고서 데이터베이스에 접근할 수 있다. (ORM이 대신 해준다)
- MVC 디자인 패턴에서 Model을 기술하는 도구이다. (Model과 DB의 연결고리)

## Sequelize

Node.js 기반의 ORM으로 MySQL뿐 아니라, PostgreSQL, MariaDB, SQLite, MS-SQL도 지원한다. Promise 기반의 ORM이기에 비동기 처리에 용이하다. 프로미스 기반이기 때문에 `then`과 `catch`를 사용할 수 있다.

- [Sequelize 설치](https://sequelize.org/)

### Sequelize-cli

명령어를 사용해 데이터베이스 작업을 할 수 있게 해준다. CLI의 대표적인 기능으로 Migration, Sedd, Model 생성등이 있다.

- [Sequelize Migrations 문서](https://sequelize.org/master/manual/migrations.html)
- `npx sequelize-cli --help`을 통해 명령의 종류를 파악할 수 있다.
- 마이그레이션은 스키마 변경에 따른 데이터 이주(migration)를 뜻한다. 이를 통해 데이터를 안전하게 보존할 수 있다. 코드에 적혀져 있는 데이터베이스 테이블에 대해 실제 DB에 테이블을 생성하는 개념이다.
- Seed는 생성된 테이블에 데이터를 추가한다.
- 모델은 테이블 생성이다.

### ORM 설정 (bootstraping)

프로젝트 초기 단계를 자동으로 설정할 수 있도록 도와주는 일이다. [Migrations](https://sequelize.org/master/manual/migrations.html) 문서를 통해 bootstraping을 해줄 수 있다. 성공적으로 끝나면 다음 파일 및 폴더들이 생성된다.

> config/config.json
> models/
> migrations/
> seeders/

이후에 설정 파일을 통해 MySQL 접속 설정을 해야한다.

### Sequelize 예시

```js
const Sequelize = require("sequelize");
const db = new Sequelize("dbName", "root", "password"); // 개인정보

const User = db.define("User", {
  // table을 만들어 준다
  //또한 기본으로 PRIMARY KEY 설정을 해준다
  username: Sequelize.STRING,
});

const Message = db.define("Message", {
  userid: Sequelize.INTEGER,
  text: Sequelize.STRING,
  roomname: Sequlize.STRING,
});

User.asyn() // 위의 객체지향 코드와 schema를 일치시켜준다
  .then(function () {
    return User.create({ username: "Martin Ko" });
  })
  .then(function () {
    return User.findAll({ where: { username: "Martin Ko" } });
  })
  .then(function (users) {
    users.forEach(function (user) {
      console.log(user.username + "exists");
    });
    db.close();
  })
  .catch(function (err) {
    console.error(err);
    db.close();
  });
```

### 몇 가지 질문:

1. 기본적으로 development, test, production 환경 중 어떤 환경을 사용하고 있나요? 여러 개의 환경이 분리되어 있는 이유는 무엇인가요?

- development는 개발용
- test는 테스트용
- production은 배포용으로 사용된다.

2. 설정 파일은 .gitignore에 등록되어 있습니다. 설정 파일을 git의 관리를 받게 하는 대신, 환경 변수를 사용하게 만들 수 있나요?

- `ENV`를 사용하면 된다.

3. 왜 Sequelize의 타입 정의와 MySQL의 타입 정의가 다를까요?

- Sequelize가 여러 관계형 DB들에 적용되어야 하기 때문에 (호환성문제)

4. 마이그레이션을 할 때 주의해야 할 점은 무엇인가요?
   보통은 migration 파일을 수정하지 않고, 다시 새로 만들어서 수정한다. (migration-skeleton) 또한 Migration Up/down 실행시 상항 변경 상황에 대해서 생각하고 주의해야한다. 최초에 만든 model을 migration 하게 되면 초기화 된다.
5. Sequelize-meta란?

- "Migration을 했다"라는 기록이다.

## 참고

- [sequelize와 express 연동](https://m.blog.naver.com/agilesoft/220986043490)
- [sequelize 모델 정의](https://victorydntmd.tistory.com/29?category=677306)
- [sequelize - hooks](http://52.78.22.201/tutorials/expressjs/expressjs_orm_four/)
- [sequelize - Hooks[번역]](https://pjt3591oo.github.io/blog/node.js/2017/04/09/sequelize_hooks.html)
- [ORM이란 블로그 1](https://gmlwjd9405.github.io/2019/02/01/orm.html)
- [ORM이란 블로그 2](http://www.incodom.kr/ORM)
- [ORM이란 블로그 3](https://m.blog.naver.com/PostView.nhn?blogId=ljc8808&logNo=220461868128&proxyReferer=https:%2F%2Fwww.google.com%2F)
- [ORM이란 블로그 4](https://velog.io/@josworks27/ORM%EC%9D%B4%EB%9E%80)
- [ORM이란 블로그 5](https://miaow-miaow.tistory.com/46)
- [ORM이란 블로그 6](https://velog.io/@alskt0419/ORM%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C...-iek4f0o3fg)
- [Sequelize](http://slides.com/thiagooliveirabonfim/sequelize#/7/0/0)

#### Sequelize ORM official Docs

- [Sequelize ORM for Node](https://sequelize.org/v5/)
- [sequelize-cli](https://sequelize.org/v5/manual/migrations.html)

# 이슈

- [TypeORM](https://typeorm.io/#/)
  [TypeORM 시작하기](https://velog.io/@josworks27/typeORM-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0)
  [TypeScript을 사용해 TypeOrm 시작하기](https://medium.com/@hckcksrl/typescript%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%B4-typeorm-%EC%8B%9C%EC%9E%91%ED%95%98%EA%B8%B0-cb7140b69c6c)
