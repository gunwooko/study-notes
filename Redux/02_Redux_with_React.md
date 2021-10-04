# React와 함께 사용하기

리덕스는 리액트를 사용하지 않고도 리덕스를 사용할 수 있지만, 일반적으로 리덕스는 리액트와 함께 사용될 때 그 효과를 많이 볼 수 있다. 그 이유는 리덕스는 액션에 반응하여 상태를 변경하기 때문에, 리엑트 혹은 [Deku](https://github.com/anthonyshort/deku)와 같이 UI를 상태에 대한 함수로 기술하는 것과 특히 잘 어울린다.

## [리덕스 공식 문서: React와 함께 사용하기](https://ko.redux.js.org/basics/usage-with-react/)

## Presentational 컴포넌트와 Container 컴포넌트의 차이점은 무엇인가요?

[Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
컴포넌트를 위의 두 종류로 나누는 것은 리덕스에서 자주 사용되는 패턴이다. 기능에 따라 컴포넌트를 분류하면 UI와 데이터를 관리하는 역활이 분리되어, 컴포넌트의 재사용성이 높아지고 구조를 명확하게 확인할 수 있다.

### Presentational Component

- 오직 뷰만을 담당하는 컴포넌트이다. (어떻게 보여질 지에 포커스)
- 리덕스와 연관되어 있지 않다. 리덕스를 의존하지 않는다.(즉, 리덕스를 사용하지 않아도 컴포넌트를 그대로 유지할 수 있다.)
- 보통 DOM 엘리먼트 또는 스타일을 갖고 있으며, 하위 컴포넌트로 또 다른 presentational 컴포넌트나 container 컴포넌트를 가지고 있을 수도 있다.
- 리덕스의 store에는 직접적인 접근 권한이 없으며 오직 props로만 데이터를 받아온다. (즉, 데이터를 읽기 위해 props에서 데이터를 읽고, 데이터를 변경하기 위해 props에서 콜백을 호출한다.)
- 대부분의 경우 state를 갖고 있지 않으며, 갖고 있을 경우엔 데이터에 관련된 것이 아니라 UI에 관한 것(어떤 컴포넌트를 숨기거나 보여주는 것과 관련된 boolean 값)이다.
- 주로 함수형 컴포넌트로 작성됩니다. state를 갖고 있어야 하거나, LifeCycle API를 사용할 때에는 클래스형 컴포넌트, 또는 Hooks로 작성된다.
- 컴포넌트를 직접 작성한다.

### Container Component

- 어떻게 동작할지에 포커스가 집중된다. (데이터 불러오기, 상태 변경하기)
- 리덕스와 연관되어 있다.
- Presentational 컴포넌트와, 하위의 Container 컴포넌트를 관리하는 역활을 담당한다.
- state를 가지고 있을 때가 많으며, 리덕스 store에 직접적으로 접근할 수 있다. (즉, 데이터를 읽기 위해 리덕스 상태를 구독하고, 데이터를 변경하기 위해 리덕스 랙션을 보낸다)
- 내부에서 DOM 엘리먼트를 직접적으로 사용하는 경우는 별로 없고, 스타일을 가지고 있으면 안 된다.
- 주로 React-Redux가 제공해주는 `connect()` 함수를 사용해 container 컴포넌트를 생성한다. (`store.subscribe()`을 사용해서 직접 작성도 가능하지만, 추천하지 않는다. 그 이유는 React-Redux에서 직접 구현하기 힘든 여러 성능을 최적화해주기 때문이다.)

## React-Redux

[React-Redux: Container 컴포넌트 구현하기](https://ko.redux.js.org/basics/usage-with-react/)

#### Provider

`<Provider />`의 하위 컴포넌트들은 redux store에 접근할 수 있다. 이 컴포넌트는 명시적으로 스토어를 넘겨주지 않아도 모든 container 컴포넌트에서 스토어를 사용할 수 있도록 해준다. 이 컴포넌트는 최상단 컴포넌트를 렌더해 줄 때 한 번만 사용하면 된다.

#### connect()

React-Redux 라이브러리에 내장된 `connect()` 함수는 `<Provider />` 컴포넌트 하위에 존재하는 컴포넌트들이 store에 접근할 수 있게 한다.

#### mapStateToProps

- 상태를 props로 보내기 위한 함수
- connect 함수에 첫 번째 인자로 들어가는 함수 혹은 객체로서, store의 값을 조회해야 할 때 사용한다.
- mapStateToProps는 기본적으로 store가 업데이트될 때마다 자동으로 호출된다.
- mapStateToProps 함수에서 현재 redux store의 상태를 어떻게 변형할지, 그리고 어떤 속성을 통해 presentational 컴포넌트로 넘겨줄지를 정의해주면 된다.

#### mapDispatchToProps

-Redux 액션을 보내기 위한 함수 ex) trigger를 위해

- connect 함수의 두 번째 인자로서, store를 변경해야 할 때 사용한다.
- store에 접근한 컴포넌트가 store의 상태를 바꿀 수 있도록 dispatch를 사용할 수 있게 만들어 준다.
- mapDispatchToProps 함수는 `dispatch()` 메소드를 인자로 받는다. dispatch(action)의 값을 props로 받아서 사용한다.
