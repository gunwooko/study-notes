> 📝 궁금한 모든 것을 기록합니다.
> 😎 기록에서 멈추지 않고 나의 것으로 만듭니다.
> 🙈 잘못된 정보가 있다면 언제든지 댓글에 남겨주세요 :D

# 🧐 TypeScript?

> _Typed JavaScript at Any Scale.
> By understanding JavaScript, TypeScript saves you time catching errors and providing fixes before you run code._

타입스크립트는 MS에서 개발한 오픈소스로, 자바스크립트의 상위 집합(Superset)인 정적 타입 언어이다. 동적 타입 언어인 자바스크립트에 강한 타입 시스템을 적용해서 컴파일 환경에서 대부분의 에러를 확인할 수 있게 된다. TS는 JS가 실행되는 모든 환경, 플랫폼에서 사용될 수 있고, 최신 ECMAScript 기능을 지원한다. 또한 객체 지향 프로그래밍 환경을 제공함으로 class, interface, extends, 제네릭 등을 그대로 사용할 수 있다.  
![](https://images.velog.io/images/gunwooko/post/46eb738d-108e-4cfa-9361-d2e4c05594da/typescript_pic1.webp)

## TS 컴파일러 설치 및 사용하기

TS파일은 브라우저에서 동작하지 않기에 TS 컴파일러를 통해 JS파일로 변환해주어야 한다. 사실 TS컴파일러는 TS파일을 JS파일로 변환해주므로 컴파일링(고급어를 기계어로 변환)이라고 하기보단 트랜스파일링이 보다 적절한 표현이다.

#### TypeScript를 전역에 설치한다.

`npm install -g typescript`
`yarn global add typescript`

#### 성공적으로 TS가 설치되었다면 `tsc` 명령어를 사용할 수 있게된다.

- `tsc --version` or `tsc -v` TS 버전 첵크 명령어
- `tsx ./src/sample.ts` TS 파일을 경로로 지정해주면 해당 파일을 컴파일한다. 이때 확장자 .ts는 생략할 수 있다. 파일명을 지정해준다면 `tsconfig.json`는 무시된다.
- `tsc` 컴파일하고 싶은 프로젝트의 해당 경로 터미널에서 이 명령어를 사용하면 해당 폴더 내의 모든 TS 파일이 컴파일링된다. `tsconfig.json` 파일에 지정한 옵션대로 컴파일된다.
- `tsc sampleTsFile -t ES2015` 아무런 설정 옵션 없이 컴파일링을 진행하게되면 기본 설정인 자바스크립트의 ES3 버전으로 변환해준다. 터미널에서 자바스크립트 버전을 변경해주고 싶다면, `--target` 혹은 `-t`를 사용할 수 있다.
- `tsc --init` 명령어를 사용해 `tsconfig.json`을 생성할 수 있다.
- `tsc --watch` or `tsc -w` 명령어를 사용하면 트랜스파일링 대상 파일의 내용에 변경이 감지되었을 때 자동으로 트랜스파일링이 실행된다.
  또한 `tsconfig.json`에 watch 옵션을 추가할 수도 있다.

### 프로젝트 내에 TS 패키지를 사용하여 컴파일 하고 싶을 때

`yarn add typescript` or `npm install --save typescript` 명령어로 TS를 로컬 패키지로 설치해준다.
사전에 `yarn init -y` or `npm init -y` 명령어로 생성한 `package.json` 파일을 열어 `build` 스크립트를 만들어 `tsc` 명령어를 지정해준다.

```ts
{
  "name": "ts-practice",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "dependencies": {
    "typescript": "^4.2.3"
  },
  "scripts": {
    "build": "tsc" // 이젠 빌드할 때, yarn build or npm run build 를 입력하면 된다.
  }
}
```

### NodeJS 환경에서 테스트하고 싶을 때

[TS Node](https://github.com/TypeStrong/ts-node)를 사용하면 된다.
`npm install -D typescript @types/node ts-node`
여기서 `@types/node` 는 NodeJS API를 위한 타입 선언 모듈이다.

```shell
# Execute a script as `node` + `tsc`.
ts-node script.ts

# Starts a TypeScript REPL.
ts-node

# TypeScript on NodeJS!
npx ts-node sample.ts
```

## tsconfig.json 살펴보기

`tsconfig.json` 파일에서는 타입스크립트가 컴파일 될 때 필요한 옵션을 지정한다.

```ts
{
  "compilerOptions": {
    "target": "es5", // 컴파일된 코드가 어떤 JS 버전에서 실행될지 정의한다.
    "module": "commonjs", // 컴파일된 코드가 어떤 모듈 시스템을 사용할지 정의한다.
    "strict": true, // 모든 타입 체킹 옵션을 활성화하는 설정이다.
    "esModuleInterop": true, // commonjs 모듈 형태로 이루어진 파일은 es2015 모듈 형태로 불러올 수 있게 해준다.
    "outDir": "./dist" // 컴파일된 파일들이 저장되는 경로를 지정한다.
    "lib": ["ES2015", "DOM"] // 컴파일에 포함할 라이브러리를 지정한다.
  },
  "include": [ // 컴파일에 포함할 경로 설정
    "src/**/*.ts"
  ],
  "exclude": [ // 컴파일에 제외할 경로 설정
    "node_modules"
  ]
}
```

## 👀 References

- [TypeScript-Handbook 한글 문서](https://typescript-kr.github.io/)
- [자바스크립트 개발자를 위한 타입스크립트](https://ahnheejong.gitbook.io/ts-for-jsdev/)
- [한눈에 보는 타입스크립트](https://heropy.blog/2020/01/27/typescript/)
