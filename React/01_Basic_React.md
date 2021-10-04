# React

## React란?

우리가 웹사이트를 만들 때는 HTML, CSS로 구조와 디자인을 짜주고 JS을 적용해서 동적인 액션을 넣어 주거나, 혹은 REACT와 같은 라이브러리를 사용해서 만들 수 있다. 보통 유저와 여러 상호 작용이 많은 사이트를 만들 때는, DOM을 관리하는 것이 생각보다 어렵고 복잡하고, 보수 또한 어려운 문제가 있게 된다. 그렇기에 DOM 관리와 상태관리를 최소화하고, 오직 기능관리에만 집중할 수 있는 고민을 했는데, 지금 있는 React, Vue, Angular 등이 생겼다.
리엑트는 사용자 인터페이스를 만들기 위한 JavaScript 라이브러리이다. Component 라는 개념에 집중하고 있는 FrontEnd 라이브러리인데, Component는 하나의 의미를 가진 독립적인 단위 모듈이다. 나만의 HTML 태그라고 말할 수 있다. 더욱더 직관적이고 재활용이 가능하다. 즉, component 구조로 이루어진 리엑트는 재사용성과 유지보수에 있어서 탁월하다. 또한 VirtualDOM을 통한 렌더링이 이루어지는데, 리엑트는 virtualDOM을 통해 변화를 가상 DOM에 먼저 적용한 후, 비교를 통해 변화된 부분만 렌더링이 적용됨으로 연산을 줄여준다.

- [프레임워크와 라이브러리의 차이점](https://webclub.tistory.com/458)

## ES6

React는 ES6를 통해 만들어지는데, 적어도 아래의 7가지 개념을 반드시 알아야 한다.

- [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [Spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
- [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
- [Arrow function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- For-of loop
- [class keyword](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)

## JSX

자바스크립트의 확장 문법이다. React component를 화면에 보여주기 위해 사용된다. React Component에서는 반드시 JSX를 리턴해 주어야한다. 얼핏 보면 HTML처럼 보일 수 있지만, JSX는 자바스크립트의 확장 문법이다. JSX를 사용하지 않고서, react를 작성해야 한다면, 복잡하고 가독성도 안 좋다. 우리가 JSX 문법을 사용해서 작성하면, BABEL이 JS코드로 변환해준다. (리엑트는 JSX를 사용하기 때문에 작성한 코드를 컴파일하는 과정이 필요하다: Babel 사용)
JSX는 자바스크립트 코드로 변환되어야 하므로 때문에 주의해야 할 규칙이 있다:

- 반드시 하나의 엘리먼트로 감싸야 한다.
- JSX에선 내부에 JS코드를 작성할 수 있는데, JS코드를 적용할 땐 {} 안에 작성한다.
- JSX 내부에선 if문을 사용할 수 없다. 따라서 삼항연산자를 사용해야한다. 아니면 IIFE
- 엘리먼트의 클래스 이름을 적용할 때, `class=`가 아니라 `className`을 사용한다. 그이유는 ES6 문법 중에 class 키워드가 있기 때문이다.

## Babel && Webpack

Babel은 JSX를 자바스트립트로 변경시켜준다. 자바스크립트의 컴파일러다.
Webpack은 패키지 번들러인데 즉, 여러 컴포넌트를 하나로 합쳐서 전송이 간편하게 해준다. `create-react-app`으로 프로젝트를 시작하게 되면, webpack이 포함되서 받아지게 된다.

### Bundler 란?

번들러란 여러개의 나누어져 있는 파일들을 하나의 파일로 만들어주는 것을 말한다. 번들러를 통해 의존성을 고민하지 않아도 되었다.(모든 JS파일을 함쳐서 하나로 묶어준다.)
번들러를 사용하는 가장 큰 이유는 모듈화를 할 수록 전송해야 할 파일들이 늘어나기 때문이다. 이렇게 번들러를 통해 로딩 속도를 확연히 줄일 수 있어졌다.

- [React 개발 환경을 구축하면서 배우는 웹팩(Webpack) 기초](https://velog.io/@jeff0720/React-%EA%B0%9C%EB%B0%9C-%ED%99%98%EA%B2%BD%EC%9D%84-%EA%B5%AC%EC%B6%95%ED%95%98%EB%A9%B4%EC%84%9C-%EB%B0%B0%EC%9A%B0%EB%8A%94-Webpack-%EA%B8%B0%EC%B4%88)
- [Webpack 기초](https://velog.io/@hih0327/Webpack-%EA%B8%B0%EC%B4%88)

## Virtual DOM

모든 DOM 전체가(구조가) 변경되지 않고, 필요 부분만 변경되게 한다. `the diffing algorithm`을 통해 이루어지고, 시간복잡도 또한 조금 더 효율적으로 변한다.
다른 말로 표현하면 리엑크 컴포넌트는 render를 호출하여 새로운 결과값을 return 한다. 그러나 return 값은 바로 DOM에 반영되지 않는다. 즉, 바로 브라우저에 render되지 않는다. 여기서 Virtual DOM이 등장하는 것이다.

1. 컴포넌트가 랜더될 때, return 값을 토대로 Virtual DOM이 생성된다.
2. 이전 브라우저에 보이는 DOM과 비교하여, 변경된 부분을 확인하고,
3. 변경된 부분만 브라우저 상에 보여지는 DOM에 적용된다.

- [React와 Virtual DOM 영상](https://www.youtube.com/watch?v=muc2ZF0QIO4)
- [[번역] 리액트에 대해서 그 누구도 제대로 설명하기 어려운 것 - 왜 Virtual DOM 인가?](https://velopert.com/3236)

## React의 주요 개념: Component

컴포넌트 이름은 반드시 대문자로 시작해야 한다. 컴포넌트는 데이터(props, state)를 입력받아 DOM Node를 출력하는 함수의 역활을 한다. 또한 UI를 구성하는 개별적인 View 단위이다. 어플리케이션은 이런 컴포넌트들이 모여 마치 레고를 조립하듯이 완성된다. 각 컴포넌트들은 어플리케이션의 다른 부분, 또는 다른 어플리케이션에서 쉽게 재상용이 가능하다.

### Functional (함수형 컴포넌트)

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

함수형 컴포넌트는 간단히 JavaScript 함수 형식으로 정의하는 것이다. state 혹은 lifecycle이 없는 일반 JS 함수이므로 읽기 및 테스트가 수월한 것이 장점이다. 함수현 컴포넌트에서는 기본적으로 state와 lifecycle을 사용할 수 없다. 하지만 함수형에서도 사용할 수 있도록 **[Hooks](https://boxfoxs.tistory.com/395)**가 등장했다.

### Class (클래스형 컴포넌트)

```js
class PetInfo extends React.Component {
  constructor() {
    super();
    this.state = { name: "Popi", type: "cat" };
  }
  render() {
    return (
      <h2>
        I am {this.state.name} the {this.state.type}
      </h2>
    );
  }
}
```

ES6의 `class` 키워드를 사용해 만들어진 컴포넌트다. 클래스 컴포넌트는 몇 가지 특징이 있다.

- `extends` 키워드를 통해, `React.Component`에 대한 상속을 작성해야 한다.
  이렇게 해서 `React.Component`의 기능에 대한 접근 권한을 받는다.
- `render()` 메소드가 필수다. 이를 통해 HTML을 리턴한다.
- `contructor`는 클래스에서 states 혹은 props를 사용하기 위해 필요한 생성자이다.
- `super(props)`는 부모 클래스 생성자(리액트에서는 `React.Component`)를 가리킨다. (contructor에서 super 호출 전에 `this`를 사용할 수 없는 규칙이 있다.)
- 만일 `constructor` 생성자 메소드를 생략하게 되면, 자동적으로 `React.Component`를 물려받는다. 그러나 props를 받으려면, 생성자 함수가 필요할 것이다.

[함수형 컴포넌트와 클래스, 어떤 차이가 존재할까?](https://overreacted.io/ko/how-are-function-components-different-from-classes/)
[Dan Abramov - 왜 super(props) 를 명시해 줘야 하는가?](https://velog.io/@honeysuckle/%EB%B2%88%EC%97%AD-Dan-Abramov-%EC%99%9C-superprops-%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94%EA%B0%80)

## React의 주요 개념: Data flow

ex) 컵을 피라미드 형태로 쌓아두고 가장 윗부분에 물을 부으면, 아래의 컵으로 담기고, 또 그 아래의 컵에 물이 차는 형식 === 단방향 데이터 흐름 즉, 데이터가 한 방향으로만 이동한다. 아래로 흐른 물이 거꾸로 올라갈 수 없다. 부모 component에서 자식 component를 호출하는데, 부모에서 자식으로만 데이터가 흐른다. 자식에서 부모 쪽으로 직접적으로 데이터를 올려줄 순 없다. (간접적으로 가능)

## React의 주요 개념: Props

ex) 위의 컵에서 내려오는 물줄기를 props라고 할 수 있다. 즉, 상위 컴포넌트가 하위 컴포넌트에게 내려주는 데이터이다. 따라서, 하위 컴포넌트는 받은 데이터를 단순히 사용만 할 수 있지, 변경할 수는 없다.

- Props는 읽기 전용이다. 변경되지 않는 고정값이다.
  함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안 된다. React는 매우 유연하지만 한 가지 엄격한 규칙이 있는데, 모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 한다. 순수 함수란 입력값을 바꾸려 하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환한다.

## React의 주요 개념: State

ex) 컵 안에 들어 있는 물이라고 생각할 수 있다.
컴포넌트에서 동적인 데이터를 관리하는 경우, state를 생성한다. State는 컴포넌트가 갖는 상태이다. 객체의 형태로 컴포넌트 내에서 보관하고 관리한다. State를 유일하게 할당 할 수 있는 곳은 constructor이다. 그렇기에 State를 사용하기 위해선, class 컴포넌트로 작성되어야 하고, 또한 state의 값을 변경하고 싶을 때는 반드시 `setState`메서드를 사용해 변경해야 한다. **직접 State를 수정하면 안 된다.** 여기서 기억해야 할 부분은 state 값을 변경할 경우 `render()` 함수가 다시 실행 (호출) 된다. 직접 변경할 경우 리엑크가 변화를 감지하지 못하고, 다시 랜더를 하지 않는다.

- [state 변경 방법 - setState](https://reactjs.org/docs/react-component.html#setstate)
- `setState`는 여러 번 호출이 가능하다.

## React의 주요 개념: Life Cycle

컴포넌트의 수명을 나타내고, 페이지에 렌더되기 전 준비과정에서 시작해서 페이지에서 사라질 때 끝난다.
컴포넌트가 생성, 업데이트, 삭제될 때 일어나는 과정으로, (컴포넌트가 브라우저에 보여질 때, 업데이트될 때, 사라질 때) 각 과정(단계) 전, 후로 특정 메소드가 실행된다. 이렇게 실행되는 메소드를 적절히 이용할 수 있는데, 먼저 컴포넌트가 생성될 때 (즉, 작성된 컴포넌트가 호출되면) 먼저 생성자가 불린다. `constructor()` 그리고 컴포넌트 내에 `render()` 메소드가 실행된다. 이때, JSX를 반환하여 화면에 그려지는 작업이 일어난다. 이렇게 렌더가 끝나면, `componentDidMount()` 란 메소드가 불린다. 컴포넌트가 업데이트되는 경우 (state값이 변경됐을 때 업데이트가 일어난다) State 값이 변경됐을 때 `render()` 함수가 실행된다. 이렇게 화면에 렌더가 끝나면, `componentDidUpdate()`란 메소드가 실행된다.

- [componentDidMount](https://reactjs.org/docs/react-component.html#componentdidmount)

주의할 점은 `setState`를 사용해야만 LifeCycle 메소드 사용이 가능하다. 이렇게 컴포넌트에 이벤트가 발생하면, 항상 life cycle 메소드가 실행되는데, 우리는 이 메소드를 적절히 사용해, 원하는 타이밍에 원하는 작업을 수행할 수 있다. 그리고 life cycle 메소드를 사용하기 위해서는, 컴포넌트를 class 컴포넌트로 작성해야 한다. 함수형 컴포넌트에서는 life cycle 메소드가 실행되지 않는다.

- [컴포넌트 life cycle의 작동 순서](https://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
- [리액트 교과서 - 컴포넌트와 라이프사이클 이벤트](https://velog.io/@kyusung/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EA%B5%90%EA%B3%BC%EC%84%9C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EB%9D%BC%EC%9D%B4%ED%94%84%EC%82%AC%EC%9D%B4%ED%81%B4-%EC%9D%B4%EB%B2%A4%ED%8A%B8)
- [(React) Component Life Cycle Methods](https://jistol.github.io/frontend/2018/12/10/react-lifecycle-methods/)
- [React 16 Lifecycle Methods: How and When to Use Them](https://blog.bitsrc.io/react-16-lifecycle-methods-how-and-when-to-use-them-f4ad31fb2282)

![](https://images.velog.io/images/gunwooko/post/db0a82e0-2657-476f-9b7a-887169b80731/react%20life%20cycle.png)

## 이슈

- 콘솔에서 [unique key prop](https://reactjs.org/docs/lists-and-keys.html#basic-list-component)에 대한 경고를 발견할 경우.
  리엑트에서는 리스트를 나열할 때 각각의 엘리먼트에 고유한 key를 부여해서, 더욱 효과적인 렌더링을 하도록 한다.
- 리엑트에서 2개 이상의 엘리먼트를 렌더링하고 싶으면, 배열로 감싸거나, 빈 태그로 감싸주면 된다. 또한 `react.Fragment` 태그로 감싸줄 수도 있다.
- 예를 들어 구글에서 제공하는 API를 활용해보고 싶으면 `componentDidMount()`에 `setState`를 넣어준다. (`componentDidMount()` 메소드에서 API 호출과 같은 비동기 호출 작업이 이루어진다.)
- Youtube API 사용해서 원하는 동영상을 요청하기: 쿼리란 웹 서버에 특정한 정보를 보여달라는 웹 클라이언트 요청이다. 주로 문자열 기반으로 한 요청을 의미하고, 대개 데이터베이스로부터 특정한 키워드를 찾기 위해 사용된다. Youtube API 문서에서 제공하는 쿼리 매개변수를 이용하면 다양한 필터를 통해 원하는 영상을 요청할 수 있다. 매개변수(key, q, maxResult, type, videoEmbeddable)를 적절히 사용할 수 있다. [Youtube API - Sample API Requests](https://developers.google.com/youtube/v3/sample_requests#channel_subscribers)
- [[ React ] fetch -REST API / JSONPlaceholder](https://sheldhe93.tistory.com/6)
- [api 붙이기(Fetch)](https://velog.io/@aerirang647/api-api-%EB%B6%99%EC%9D%B4%EA%B8%B0Fetch)
- [React API 연동](https://velog.io/@johnque/React-API-%EC%97%B0%EB%8F%99-v9k692txn5)
- [React - HTTP GET 요청](https://riptutorial.com/ko/reactjs/example/22111/http-get-%EC%9A%94%EC%B2%AD)

# 참고

- [리엑트 공식 문서 - 리엑트 12가지 핵심개념](https://reactjs.org/docs/hello-world.html)
- [리엑트 공식 문서](https://ko.reactjs.org/)
- [리액트 교과서 - React 컴포넌트와 상태 객체](https://velog.io/@kyusung/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EA%B5%90%EA%B3%BC%EC%84%9C-React-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EC%83%81%ED%83%9C-%EA%B0%9D%EC%B2%B4)
- [노마드코드의 React 강의](https://www.youtube.com/playlist?list=PL7jH19IHhOLPp990qs8MbSsUlzKcTKuCf)
- [Velopert님의 React 강의](https://www.inflearn.com/course/react-%EA%B0%95%EC%A2%8C-velopert/dashboard)
- [Velopert와 함께하는 모던 리엑트 문서](https://react.vlpt.us/)
- [리엑트 공식 문서 - AJAX 와 APIs-어떻게 AJAX 호출을 할 수 있을까요?](https://ko.reactjs.org/docs/faq-ajax.html)
- [Stack overflow - when you get promise value in react component](https://stackoverflow.com/questions/42308244/get-promise-value-in-react-component)
- [리엑트에서 fetch를 이용한 api 호출 블로그 1](https://velog.io/@sv002/SMG-TIL-7-ReactJS%EC%97%90%EC%84%9C-fetch%ED%95%A8%EC%88%98%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-API%ED%98%B8%EC%B6%9C-feat.componentDidMount)
- [리엑트에서 api 붙이기 블로그 2](https://velog.io/@aerirang647/api-api-%EB%B6%99%EC%9D%B4%EA%B8%B0Fetch)
- [React 애플리케이션에서 데이터 불러오기](https://code.tutsplus.com/ko/tutorials/fetching-data-in-your-react-application--cms-30670)
- [Youtube 영상을 검색하려면, API의 Search:list 엔드포인트 사용하기](https://developers.google.com/youtube/v3/docs/search/list)
- [컨테이너 컴포넌트와 프레젠테이션 컴포넌트 1](https://velog.io/@kyusung/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EA%B5%90%EA%B3%BC%EC%84%9C-React-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8%EC%99%80-%EC%83%81%ED%83%9C-%EA%B0%9D%EC%B2%B4#react-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EC%83%81%ED%83%9C-%EA%B0%9D%EC%B2%B4)
- [컨테이너 컴포넌트와 프레젠테이션 컴포넌트 2](https://code.tutsplus.com/ko/tutorials/stateful-vs-stateless-functional-components-in-react--cms-29541)
- [Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)

# React - Lifting State Up

리엑트 컴포넌트가 트리 구조와 같이 이루어져 있는데, 만일 하위 컴포넌트에서 어떤 변경사항이 발생했을 때, 그리고 그 변경사항이 다른 여러 컴포넌트에도 동시에 적용이 되어야 한다면 어떻게 해야 할까?

여기서 우리는 lifting state up이 필요하다. 하위 컴포넌트에서 변경된 내용을 상위 컴포넌트까지 끌어 올려서, 상위 컴포넌트의 스테이트에 반영하는 것이다.

![](https://images.velog.io/images/gunwooko/post/caaf08d7-55bf-4c1b-8589-e5c24c345fb2/_-15.jpg)

# 참고

- [Stackoverflow - React js onClick can't pass value to method](https://stackoverflow.com/questions/29810914/react-js-onclick-cant-pass-value-to-method/29810951#29810951)

# Class 컴포넌트에서 props 기본 값 설정하기

```js
import React, { Component } from "react";

class MyName extends Component {
  static defaultProps = {
    name: "Martin",
  };

  render() {
    return (
      <div>
        안녕! 나는 <b>{this.props.name}</b> 이라고 해
      </div>
    );
  }
}

export default MyName;
```

아래와 같은 방식으로도 가능하다.

```js
import React, { Component } from "react";

class MyName extends Component {
  render() {
    return (
      <div>
        안녕! 나는 <b>{this.props.name}</b> 이라고 해
      </div>
    );
  }
}

MyName.defaultProps = {
  name: "Martin",
};

export default MyName;
```

## 참고

- [Velopert - 누구든지 하는 리액트 4편: props 와 state](https://velopert.com/3629)
