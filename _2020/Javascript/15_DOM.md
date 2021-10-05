# DOM (Document Object Model)

JavaSript를 이용해서 엘리먼트의 속성 값을 얻어내거나, 변경하는 방법. DOM이 자바스크립트는 아니고, DOM를 이용해서 자바스크립트에 접근을 할 수 있는 것이다. 앞서 다른 글에서 설명한 것과 같이 HTML의 구조는 tree structure이라고 했는데, 자바스크립트에는 객체가 이런 구조를 가지고 있다. 그렇기에 DOM은 HTML 문서의 구조와 관계를(엘리먼트와 그의 부모, 자식 엘리먼트) 객체(Obejct)로 표현한 모델이다. `document`라는 전역변수로 접근이 가능하다. (Console창에서 `document`를 치면 HTML 문서를 볼 수 있다.)
`console.dir(document)`를 치면 객체처럼 나오게 되는데 여기서 모든 속성을 볼 수 있다. 이는 자바스크립트처럼 키와 값에 접근할 수 있다는 말이다. `document`는 DOM를 대표하는 객체라고 할 수 있다. 콘솔창에서 엘리먼트를 클릭해서 `console.dir($0)`를 치면 그 엘리먼트에 해당하는 속성들을 객체 형식으로 확인할 수 있다.

## 엘리먼트에는 어떤 속성이 들어있나?

|              속성              |                                    속성이름                                     |
| :----------------------------: | :-----------------------------------------------------------------------------: |
|            태그이름            |                                     tagName                                     |
|               id               |                                       id                                        |
|           class목록            |                                    classList                                    |
|          class문자열           |                                    className                                    |
|           속성 객체            |                                   attributes                                    |
|          스타일 객체           |                                      style                                      |
|      엘리먼트에 담긴 내용      |                    **innerHTML**, innerText, **textContent**                    |
|          form 입력 값          |                                      value                                      |
|         자식 엘리먼트          |                                    children                                     |
|         부모 엘리먼트          |                                  parentElement                                  |
|           자식 노드            |                                   childNodes                                    |
|      data- 속성에 담긴 값      |                                     dataset                                     |
|             이벤트             |                       onclick, onmuouseover, onkeyup, etc                       |
| 좌표 정보 (기준점에 따라 다름) |       offsetTop, offsetLeft, scrollTop, scrollLeft, clientTop, clientLeft       |
| 크기 정보 (기준점에 따라 다름) | offsetWidth, offsetHeight, scrollWidth, scrollHeight, clientWidth, clientHeight |

### 엘레먼트에 닮긴 내용

- innerHTML: 태그가 전체적으로 보여진다. HTML 통째로 가져올 때 사용하면 된다.
- textContent: 실제 화면이 나오는게 아닌, 공백이 다 포함되어서 나온다.
- innerText: 실제로 화면에 보여지는 부분만 축출해서 보여준다.

여기서 innerHTML과 textContent는 내용을 실제로 수정할 수 있다. 단 innerHTML은 태그도 수정하여 링크도 걸 수 있다. textContent로 시도해보면 태그와 링크 자체가 문자열로 나오는 걸 알 수 있다. 즉, 위에 속성들은 값을 할당할 수 있다.

### form 입력 값: input 태그에서 값을 받아올 수 있다. `$0.value`

자식 엘리먼트와 자식 노드의 차이점은 자식엘리먼트를 불러올 땐 선택된 태그의 자식 태그만을 나타내지만, 자식 노드에선 태그와 text도 나온다(공백포함). "Text"는 노드이다.(문자열을 담은 객체 이다). 엘리먼트는 노드에 속해있고, Text는 노드이나, 엘리먼트는 아니다. <자세한건 다음에 다룬겠다>

### 데이터 속성

- dataset: 태그 자체에 데이터를 담아두고 싶을 때 사용 가능하다. 화면상에 보이지 않는다. dataset이란 속성을 이용해서 데이터를 불러올 수 있다.

### 이벤트 속성

예를 들어 어떤 버튼을 눌렀을 때 어떠한 액션이 나타나는 것을 이벤트다. `on~`으로 시작되는 속성들은 다 이벤트와 관련되어 있다.

- onkeydown, onkeypress: 키보드로 할 수 있는 이벤트
- onclick(이벤트 관련 속성): 대표적으로 `button`이 할 수 있는 이벤트이다.

콘솔창에서 해볼 수 있는 방법:

- 콘솔 엘리먼트 창에 button을 클릭하고, 콘솔창에 `$0.onclick`을 걸어준다.

```js
function foo() {
  console.log("마우스가 눌렸어요");
}

$0.onclick = foo; // 그리고서 마우스로 버튼을 눌렀으면 콘솔창에 뜬다.
```

## 엘리먼트 선택 / 값 받아오기 / 이벤트로 액션 취하기

자바스크립트를 이용해, 특정 엘리먼트를 선택하고, 가져올 수 있다.

- 태그를 이용: getElementsByTagName
- id를 이용: getElementById (단수로 쓰인 이유는 id는 유닉하기 때문이다)
- class를 이용: get ElementsByClassName
- selector를 이용: querySelector / querySelectorAll (이거 두개만 알면 위에 모두를 커버할 수 있다.)

### **document.""로 선택해서 사용한다.**

querySelector를 사용해보자. 예를 들어 id='username' / id='tweet' / class='comment'가 있다고 하면:

```js
document.querySelectorAll(".comment");
// comment 클래스에 담긴 값을 가져온다.
// 즉, 여러가지 값이 있는 클래스를 선택할때 (배열로 가져온다)
document.querySelectorAll(".comment")[0];
// 인덱스를 사용하여 선택할 수 있다.
let allcomment = document.querySelectorAll(".comment");
// 변수에 할당 할 수 있다.
document.querySelector("#username");
// id인 경우 하나의 값이기에, querySelector()로 사용 가능하다.

// (element)를 문자열로 넣어준다!!
```

이렇게 해서 input을 가져올 수 있다.

만일 입력창에서 사용자 이름과 글쓴 내용을 가져오고 싶다면 어떻게 할 수 있을까? 즉, 엘리먼트를 어떻게 가져올 수 있을까? (button에 id=`register`를 추가했다고 하자)

### 입력 값을 받아오기

```js
function getInputValue() {
  // 먼저 username과 tweet를 선택한다.
  // 그리고서 각각의 값을 얻어온다.

  let elemUsername = document.querySelector("#username");
  let elemTweet = document.getElementById("tweet"); // id를 가져온다고 명시했기에 #을 붙이지 않는다.

  // 값을 얻어오는 방식은 이렇게 된다:
  console.log(elemUsername.value);
  console.log(elemTweet.value);
}
```

### 얻어온 값을 이벤트로 나타내기

```js
document.querySelector("#register").onclick = getInputValue;
// 이렇게 하면 유저가 값을 타입하고 버튼을 클릭하면, username과 tweet을 받아온다.
```

그리고 여기서 받아온 값을 사용해야한다면? (만일 comment를 추가해야된다면?) DOM을 조작해야 한다.

## DOM 조작

### innerHTML

innerHTML 속성은 읽기 뿐 아니라, 쓰기도 가능하다. 가장 쓰기 쉬운 속성이지만, 느리고 보안 위협이 있다. (textContent가 안전하다)

### 메소드를 이용 createElement()

엘리먼트를 만드는 메소드를 사용한다. 메소드를 이용한 엘리먼트 생성은, 생성과 동시에 이벤트 핸들러 등록이 가능하다는 장점이 있다.

- `createElement()`메소드: 동적으로 엘리먼트를 생성한다.
  `document.creatElement('생성하고픈 엘리먼트')` -`appendChild(element)` 메소드를 사용하여 부모태그 안쪽에 엘리먼트를 추가할 수 있다.
  `부모태그.appendChild(element)`

#### 삭제하기

- innerHTML을 사용해서 삭제하기

```html
<div id="target">변경 전</div>
```

```js
let targe = document.querySelector('#target');
target.innerHTML = // 이렇게 비워두면 삭제된다.
```

```html
<div id="target"></div>
```

- 메소드 사용해서 삭제하기

### `<template>` 태그를 이용해서 조작할 수도 있다.

HTML파일에 `<template>` 태그를 사용해서 만들어 주고, JS파일에서 querySelector로 선택해주고, `let element = document.importNode(template 선택하고 만든 변수.content, true)`를 사용하고서, 부모태그에 `appendChild(element)`를 이용해서 사용한다. 중복사용이 가능하고, `<template>` 태그는 JS으로 실행 전까진, 브라우저에서는 보이지 않는다.

## `<script>` 적용

**한가지 알아야 할 중요한 사실!
`<script>`파일을 html에 적용할 때는 `<head>`태그 안 쪽이 아닌, `<body>` 태그가 끝나는 부분 바로 윗 쪽에 적요해야 한다! `<head>` 안에 넣어주면 DOM이 실행되지 않는다! (외부 script를 사용하고 싶을 때)
`<script src="script.js"></script>`**

# 참고

- [Vanilla JavaScript Quick Reference / Cheatsheet](https://gist.github.com/thegitfather/9c9f1a927cd57df14a59c268f118ce86)
- [DOM cheat sheet](https://gist.github.com/thegitfather/9c9f1a927cd57df14a59c268f118ce86)
