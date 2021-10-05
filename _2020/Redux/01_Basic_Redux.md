# Redux?

리덕스는 상태 관련 라이브러리이다. 예를 들어 리엑트를 통해 컴포넌트 단위로 개발이 된 무언가를 리덕스를 통해 컴포넌트와 상태를 분리하는 것이다. 만일 상태가 컴포넌트에 제거될 수 있다면, class component보다 단순한 functional component만으로도 설계하고 개발이 가능하게 된다. 물론 리액트를 사용하지 않고도 리덕스를 사용할 수 있지만, 일반적으로 리덕스는 리액트와 함께 사용될 때 그 효과를 많이 볼 수 있다.

## 리엑트에서 상태 관리의 한계

계속해서 리엑트를 사용한다는 가정 안에서 생각을 한다면, 리엑트에서 가장 상위에 있는 컴퍼넌트에서 상태와 핸들러함수를 지정해주고, props로 상태와 핸들러함수를 하위 컴퍼넌트로 내려주고, 하위 컴퍼넌트에서 그 상태에 대한 이벤트를 실해해주는 것이 일반적이다(lifing state up). 그렇다면, 만일 또 다른 라인의 nested된 컴포넌트의 컴포넌트가 상위 컴퍼넌트의 상태 정보가 필요하다면 어떤 일이 일어나는가? 여기서 또한 상태가 지정된 상위 컴퍼넌트에서 아래로 쭉 props를 내려줘야 한다. 이런 문제를 props drilling이라고 한다. 중간에 있는 컴퍼넌트에서 설사 상태 정보가 필요하지 않더라도 내려줘야 하는 상황이 오는 것이다.

- 리엑트에서의 상태 관리는 class 컴포넌트 안에서 이뤄진다.
- 형제 컴퍼넌트 간의 정보 공유는 부모 컴퍼넌트를 통해 주고받는다.
- 친척 컴퍼넌트와의 정보 공유는 할아버지 컴퍼넌트에서 상태를 가지고 props를 통해 내려주는데, 중간에 엄마아빠 컴퍼넌트는 그냥 전달해주는 역활만 하게 되는 것이다.
  이러한 문제는 족보가 길어지면 길어질수록 복잡해주고, 누가 상태를 가지고 있고 관리하는지에 대한 문제가 생기게 된다.
- 너무 많은 props를 내려야 하는 경우 혹은, 너무 깊은 곳에 props를 전달해야 하는 경우가 생기면 관리하기 힘들어진다.
- [너무 많은 props를 내려야 해서 힘들어하는 한 개발자의 질문과 이에 대한 답변](https://www.reddit.com/r/reactjs/comments/4v3mcb/passing_down_too_many_props_to_child_components/)
- [Props drilling의 장단점](https://edykim.com/ko/post/prop-drilling/)

물론 리엑트를 통해 해결될 수 있는 일도 많다. 오늘날 프론트엔드 개발에서 자바스크립트 싱글 페이지 애들리케이션이 갖추어야 할 요건들이 점점 더 복잡해지고 있는데, 그 이유는 변화(mutation)와 비동기(asyncronicity)와 같이 앞의 변화를 추론해내기 어려운 두 가지 개념을 섞어서 사용하기 때문이다. 여기서 리엑트와 같은 라이브러리는 뷰 레이어에서 비동기와 DOM 조작을 없애버렸다. 하지만 리엑트는 데이터 관리에는 관여하지 않는데, 또 다른 복잡성의 이유는 오늘날 어느 때보다도 많은 상태를 자바스크립트 코드로 관리할 필요가 있다는 것이다. 수많은 상태가 존재하고 여기 저기서 필요로 하고 변경되고 이벤트가 발생하고 등등이 일어난다면, 언제 어디서 무슨 일이 일어나는지 알 수 없는 코드가 되고 만다. 즉, 상태를 언제, 왜, 어떻게 업데이트할지 제어할 수 없는 난관에 부딪히게 되는 것이다.

## 해결 방안은 Redux!

만약에 모든 컴퍼넌트가 접근할 수 있는 공용 스토어가 있다면? 필요한 상태 정보를 스토어에서 가져올 수 있다면? 그리고 스토어 관리자(dispatcher)를 통해 스토어의 상태를 변경할 수 있도록 관리한다면? 즉, 스토어에서 스토어 관리자 함수를 가져와서, 수정이 필요한 컴퍼넌트에 관리자를 전달하여, 그 컴퍼넌트에서 이벤트를 실행해서 상태에 변화를 준다면? 이 역활을 하는 것이 리덕스 라이브러리이다. 리덕스를 통해 상태 변화가 일어나는 시점에 제약을 두어 상태 변화를 예측할 수 있게 만드는 것이다.

## Redux의 기본 개념: 세가지 원칙

### [Store](https://ko.redux.js.org/basics/store/) : 상태가 관리되는 오직 하나의 공간

모든 상태는 하나의 스토어 안에 하나의 객체 트리 구조로 저장된다. 이렇게 해서 범용적인 애플리케이션을(universal application, 하나의 코드 베이스로 다양한 환경에서 실행 가능한 코드) 만들기 쉽게 되었다. 하나의 상태 트리만을 가지고 있게 때문에 디버깅에 용이하다.

### 상태는 읽기 전용이다 && Action : Simple JavaScript Object

필요한 정보를 순수한 객체에 적어 스토어로 보내는 것이다. 즉, 상태를 변화시키는 유일한 방법은 무슨 일이 일어나는지를 나타내는 액션 객체를 전달하는 방법뿐이다. 이를 통해 결코 뷰나 네트워크 콜백에서 상태를 직접 바꾸지 못한다. 액션은 그저 평범한 객체이기에, 기록을 남길 수 있고, 시리얼라이즈(serialized)할 수 있고, 저장할 수 있고, 이후에 테스트나 디버깅을 위해 재현하는 것도 가능하다.
여기서 시리얼라이즈, **즉 직렬화를 하는 이유는 state가 한 곳에서 관리되기에 데이터를 내보내기 쉽게 하기 위함이다. serialized는 JSON을 deserialzed는 PARSE하는 것과 비슷한 개념이다.**

### Reducer : 상태 변화를 일으키는 Pure funciton (순수 함수)

현재 상태와 Action을 이용해 다음 상태를 만들어낸다. 여기서 Pure function이란 Reducer에 들어간 Action과 상태를 변형시키거나 건드리지 않고서 새 상태를 만들어내고, 또한 항상 값은 상태 값을 내보낸다. 즉, 같은 Action과 state를 reducer로 보내면 항상 같은 새로운 상태가 나온다.
액션에 의해 상태 트리가 어떻게 변화하는지를 지정하기 위해서는 순수 리듀셔를 작성해야 하는데, 리듀셔는 그저 이전 상태와 액션을 받아 다음 상태를(새로운 상태 객체를 생성해서) 반환하는 순수 함수이다. 리듀서는 그저 함수이기 때문에 호출되는 순서를 정하거나 추가적인 데이터를 넘길 수도 있다.

```js
type Reducer<S, A> = (state: S, action: A) => S;
// Redux에서 누적값은 상태 객체이고, 누적될 값은 액션이다.
// 리듀서는 주어진 이전 상태와 액션에서 새로운 상태를 계산한다.
```

[공식문서 Redux-Reducer-상태설계하기](https://ko.redux.js.org/basics/reducers/)

## Action 이란?

액션은 애플리케이션에서 스토어로 보내는 데이터 묶음(객체)이다. 실행의 형태(type)과 값(value). Action은 생산자 함수이다: store.dispatch를 통해 실행의 형태와 값을 전달하는 함수.

- `store.dispatch()`를 통해 액션을(실행의 형태type와 값value) 보낼 수 있다. 또한 상태 변경을 일으키기 위한 유일한 방법이다.
- 액션은 반드시 어떤 형태의 액션이 실행될지 나타내는 `type` 속성을 가져야 한다. 타입은 일반적으로 문자열 상수로 정의된다. [액션 타입을 상수로 했을 때의 장점](https://ko.redux.js.org/recipes/reducing-boilerplate/)
  앱이 커지면서 다양한 타입이 생기면, 별도의 모듈로 분리할 수도 있다.
- `type`외에 액션 객체의 구조는 마음대로 할 수 있다. [Flux Standard Action에서의 액션을 어떻게 구성할지에 대한 권장사항](https://github.com/redux-utilities/flux-standard-action)

```js
const ADD_TODO = 'ADD_TODO' // 타입 속성을 정의해주고 `

// 액션
{
  type: ADD_TODO, // 액션 타입을 여기에 지정해 준다.
  text: 'Build my first Redux app' //
}
```

### Action 생산자

액션 생산자는 액션을 만드는 함수이다. Redux에서 액션 생산자는 액션을 반환한다.

```js
function addTodo(text) {
  return {
    type: ADD_TODO,
    text,
  };
}
```

그리고서 액션을 보내려면 결과값을 `dispatch()` 함수로 넘겨야 한다.

```js
dispatch(addTodo(text));

// 또한 자동으로 액션을 보내주는 바인드된 액션 생산자를 만들 수도 있다.
const boundAddTodo = (text) => dispatch(addTodo(text));
// 위에 바인드된 액션 생산자는 바로 호출할 수 있다.
boundAddTodo(text);
```

## Reducer란?

리덕스에서 애플리케이션의 모든 상태는 하나의 객체에 저장된다. 리듀서를 작성하기에 앞서 상태 객체가 어떻게 설계되었는지(생겼는지) 보는 것이 중요하다. 리듀서는 이전 상태와 액션을 받아 다음 상태를(new) 반환할 것이다. 여기서 리듀셔를 순수하게 유지하는 것이 매우 중요한데, 절대로 리듀서 내에서 하지 말아야 할 것이 있다.

- 인수들을 변경(mutable)하기 (기존 state를 직접 변경하지 않는다)
- API 호출이나 라우팅 전환 같은 side-effect 일으키기 (side-effect가 없는 순수 함수이다)
- `Data.now()`나 `Math.random()` 같이 순수하지 않은 함수 호출하기

### 리듀서의 목적

기존 상태를 직접 수정하지 않고(immutable) 새로운 상태를 반환하기 위해서 사용된다.

### [Object.assign()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)은 어떻게 작동하는가?

```js
let newState = {};
let currentState = { video: "이전비디오", isDarkMode: false };
Object.assign({}, currentState, { video: "새비디오" });
// 첫 번째 인자로 빈 객체를 넣어준다. immutable 해야하기 때문이다.
// 두 번째 인자로 기존 state
// 세 번째 인자로 변경하고 싶은 부분
```

### [Object spread operator](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)는 어떻게 작동하는가?

- [이전에 spread operator에 관해 쓴 블로그](https://velog.io/@gunwooko/Rest-Parameter)

### 상태 객체가 복잡하게 짜여있는 경우 어떻게 값을 바꾸면 좋은가?

```js
// 여기서 "Software Engineer"라는 값을 바꾸고 싶다면?
currentUser: {
  name: "Martin",
  company: {
    name: "Kesla",
    department: "Development",
    role: {
      name: "Software Engineer",
    }
  }
}
```

[Redux - 중첩된 객체 업데이트하기](https://ko.redux.js.org/recipes/structuring-reducers/immutable-update-patterns/)

### 왜 리듀서에서는 side-effect가 일어나면 안 되는가?

[이에 대한 답변](https://stackoverflow.com/questions/36016336/why-does-a-redux-reducer-have-to-be-side-effect-free)

## Redux - 주요 개념 정리

### Store

앱의 전체 상태를 저장하고 있는 저장소

#### 주요 메서드:

- `createStore(reducer)` Redux store를 생성한다.
- `getState()` 현재 state를 가져온다.
- `dispatch(action)` store의 reducer에 action을 전달한다. 리덕스에서 상태 변경을 일으킬 수 있는 유일한 방법

### Action

Store에 정보를 전달할 때 사용되는 데이터 묶음

### Action Creator

Action을 생성하는 함수

### Reducer

전달된 action을 통해, state를 어떻게 변화시킬지에 대한 정보가 담겨 있고, store와 정보를 주고받는 역할을 담당한다.

#### 주요 메서드:

- `combineReducers(reducer1, reducer2, ...)` 여러 개의 reducer들을 하나로 합칠 수 있다.

## Redux의 장점

![](https://images.velog.io/images/gunwooko/post/4003288a-37c9-4b80-88e5-3987786664bd/why_redux.png)

- 글로벌 상태 관리를 하게 될 때 굉장히 효과적이다. state를 스토어라는 공용 공간에서 관리를 하고, 각 컴포넌트가 스토어에 직접 접근하여 작업한다.
- 상태를 예측할 수 있게 만들어준다.
- 유지보수가 좋다. ex) 커다란 트리 구조의 컴퍼넌트를 관리하기 좋다. 컴포넌트들의 state 관련 로직들을 다른 파일들로 분리시켜 효율적으로 관리할 수 있다.
- 디버깅에 유리하다. ex) action과 state 로그 기록하게 되면
- 테스트를 붙이기 쉽다. (순수함수를 사용하기에? => 더 공부하기)

## 이슈

- [Flux 아키텍처](https://haruair.github.io/flux/docs/overview.html)
- [Redux DevTools: 크롬 개발자 도구 한편에 Redux 상태를 확인할 수 있게 도와준다.](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)
- [어쩌면 당신에게 Redux가 필요하지 않을 수도 있다.](https://orezytivarg.github.io/you-might-not-need-redux/)
- [Context API: 리액트 자체에서 전역적 상태 관리 솔루션 기능](https://ko.reactjs.org/docs/context.html)
- [또 다른 상태 관리 라이브러리 MobX](https://mobx.js.org/README.html)
- [DarkMode 구현은 CSS 만으로도 충분하다.](https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-color-scheme)

# 참고

- [Redux 공식 문서](https://ko.redux.js.org/)
- [리덕스를 도입하는데 주저하게 만드는 장벽들](https://www.youtube.com/watch?v=xsOhUX7DDl0)
- [리엑트에서 리덕스 전에 배워야 할 8가지](https://edykim.com/ko/post/learn-react-before-using-redux/)
