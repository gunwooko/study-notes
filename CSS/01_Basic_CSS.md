# CSS

Cascading Style Sheets는 웹페이지 구성요소의 스타일을 정의하는 언어이다. HTML은 웹페이지의 요소를 구성한다면, CSS는 HTML의 스타일을 꾸며준다. 예를 들면, 검색창의 너비, 버튼의 크기와 스타일, 구성요소의 위치 외에도 다양하게 있다.

CSS를 사용하는 방법은 총 3가지가 있다.

- Inline
  HTML의 특정태그에 style 속성을 적용
- HTML 내부에 stylesheet 작성
  `<style></style>`태그를 이용, 보통 `<head>`태그 안에 삽입한다.
  태그를 선택하는 규칙(selector)에 따라 일괄 적용된다.
- HTML 외부에 stylesheet 작성
  `<link>`태그 이용, css 확장자로 저장된 stylesheet파일을 href속성을 사용해 삽입한다. 예를 들면: `<link rel="stylesheet" type="text/css" href="myStyle.css" />`

## CSS Selector

CSS 선택자는 CSS에서 요소(element)를 선택하는 규칙이다.

index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Page title</title>
    <link rel="stylesheet" type="text/css" href="myStyle.css" />
  </head>
  <body>
    <h1>Hi there!<h1>
    <h1>This is an example<h1>
    <div>Contents here!
      <span>Contents here!</span>
    </div>
  </body>
</html>
```

myStyle.css

```css
h1 {
  color: red;
}
```

여기서 Hi there!에 빨간색, This is an example에 파란색을 적용하고 싶으면 어떻게 하면 좋을까? 두가지 방법을 사용할 수 있다.

### 각각의 요소(element)에 고유한 ID를 부여하기

- id 속성을 사용해서 #identifier과 같이 #을 이용해 고유 id를 선택한다.

index.html

```html
<h1 id="hi">
  Hi there!
  <h1>
    <h1 id="ex">
      This is an example
      <h1></h1>
    </h1>
  </h1>
</h1>
```

myStyle.css

```css
#hi {
  color: red;
}
#ex {
  color: blue;
}
```

### 종류(class)를 만들고 element에 class 부여하기

- 각기 다른 색의 특성을 가진 class를 만들고, 해당 element에 적용할 수 있다.
- 여러 태그에 class를 부여 가능하고, 한 태그에 여러 class 적용도 가능하다. 공백을 이용해 여러 class를 지정한다.
- .className과 같이 .(dot)을 이용해 class를 선택한다.

index.html

```html
<h1 class="red">
  Hi there!
  <h1>
    <h1 class="blue fontStyle">
      This is an example
      <h1></h1>
    </h1>
  </h1>
</h1>
```

myStyle.css

```css
.red {
  color: red;
}
.blue {
  color: blue;
}
.fontStyle {
  font-size: 2em;
  font-weight: bold;
}
```

### Class Selector vs ID Selector

- class와 id 둘 선택자 모두 자유롭게 이름을 붙일 수 있다.
- class는 동일한 값을 갖는 element가 많지만, id는 문서 내에서 단 하나의 element가 유일한 값을 가진다.
- class는 element가 여러 값을 가질 수 있지만, id에서는 element는 단 하나의 값을 가진다.
- class는 스타일을 분류하는데 사용되고, id는 특정 element를 이름 붙이는데 사용한다.

## 기본 스타일링

### font-

- `font-family` 글씨 서체를 지정하는 속성
- `font-size` 글씨의크기를 나타내는 속성
- `font-style` 글씨에 스타일을 주는 속성
- `font-weight` 글씨의 굵기를 조절하는 속성
- `font-variant` 대소문자에 대한 속성
- `line-height` 줄 간격을 조절하는 속성
- `font` `font-`로 시작하는 모든 속성을 `font`하나로 줄여서 선언할 수 있다. 속성의 순서는 다음과 같다: `font : font-style font-variant font-weight font-size/line-height font-family`

### backgraound-

- `background-color` 배경 색을 넣는 속성
  속성 값은 rgb() 또는 #으로 시작하는 HEX, 색상 이름 등이 들어 갈 수 있다.
- `background-image` 배경에 이미지를 넣는 속성
  `background-image: url('../img/bg.png');` 이미지의 주소를 넣는 방식으로 실행된다.
- `background-repeat` `background-image`속성으로 넣어준 이미지를 반복시킬지 아닐지 등을 선택한다.
- `background-position` `background-image`로 넣은 이미지의 좌표 값을 정하는 속성
- `background-attachment` 배경이미지를 어떻게 고정할지를 정하는 속성
- `background` 위의 모든 속성을 하나로 줄여서 선언할 수 있다.

### text-

- `text-decoration` 글자에 밑줄 또는 취소선등을 넣을 수 있는 속성
- `text-align` 문단의 정렬을 조절하는 속성
- `text-indent` 문단의 들여쓰기를 조절하는 속성
- `text-transform` 영문자들을 모두 대문자 또는 소문자로 변경할 수 있는 속성
- `letter-spacing` 글자 간의 간격을 줄 수 있는 속성
- `word-spacing` 단어 간의 띄어쓰기의 간격을 조절하는 속성
- `vertical-align` 글자와 글자간의 수직정렬(나란히 나오는 인라인 요소와 인라인 요소 간의 정렬)
- `white-space` 줄 바꿈에 대한 설정을 할 수 있는 속성

## Box Model & Layout

모든 HTML의 요소들은 박스로 생각할 수 있고, box model이란 용어는 디자인과 layout을 말할 때 사용된다.
![](https://images.velog.io/images/gunwooko/post/517a8c68-eeff-4630-b438-d7f9a7accc9f/Box%20Model.png)
**Content**: 이곳은 내용 즉, 문서 혹은 이미지가 담기는 공간이다.
**Padding**: 패딩은 콘텐츠 주위의 영역이다.
**Border**: 콘텐츠와 패딩을 감싸는 테두리다.
**Margin**: 테두리 밖의 영역이다.

![](https://images.velog.io/images/gunwooko/post/8d846938-3cea-40d0-a668-90704690bacb/element%20layout.png)

### Border

기본적으로 모든 요소는 사각형 형태를 띄고 있다. 요소의 테두리 역시 네 개의 방향을 가지고 있다. 테두리의 방향을 `border-top`, `border-right`와 같은 방식으로 선언할 수 있다.
각 변마다 선의 굵기(width), 선의 형태(style), 선의 색상(color)를 지정해 줄 수 있다. 예를 들면 `border-top-width: 3px; `, `border-left-style: dashed; `, `border-bottom-color: red; `와 같은 방식으로 지정할 수 있다.
myStyle.css

```css
div {
  border-top: 3px dashed blue; /*top 테두리에 굵기 형태 색상 지정*/
  border-width: 3px 2px 4px 6px; /*항상 위 오른쪽 아래 왼쪽 순으로 지정*/
}
```

### Margin

요소와 요소와의 간격, 바깥 여백를 주는 속성이다. border과 같이 방향을 선택할 수 있고 만일 요소간의 사이의 간격에서 마진끼리 서로 겹쳐지면 둘중 큰 간격으로 간격이 벌어진다.

### Padding

요소 안, 내부 여백을 주는 속성이다. Margin과 작성 방식이 같다.

### width와 height

각각 너비와 높이를 지정해주는 속성인데 블록 요소에서만 적용 가능하다. 주로 px, em, % 단위가 값으로 올 수 있고, %를 사용시 부모 요소의 너비 혹은 높이를 기준으로 적용된다. 또한 width와 height는 padding과 border를 제외한 길이이다. 그렇기에 padding과 border를 고려해야 한다.

### Position

CSS position 속성은 문서 상에 요소를 배치하는 방법을 지정한다. top, right, bottom, left 속성이 요소를 배치할 최종 위치를 결정한다.

- Static: 기본값. 기본적인 요소는 위에서 아래로, 왼쪽에서 오른쪽으로 확장된다. 왼쪽 상단의 좌표가 (0, 0)이 된다. 픽셀(px)단위나 퍼센트(%)단위등을 사용할 수 있다.
  예를 들면, 흔히보는 광고처럼 사진이 고정된다.
- Relative: 기본값 + 상대적인 위치
- Fixed: 브라우저 화면의 좌상단을 기준으로 절대적인 위치
  좌표계를 바탕으로 절대/상대적인 위치에 positioning할 수 있다.
- Absolute: 부모 중 기준점이 있는 경우 그 기준으로 절대적인 위치
- Stiky: 기본적으로 relative 처럼 작동하나, 스크롤 영역을 벗어나면 fixed 처럼 작동한다.
  예를 들면, 스크롤바에 영향을 받아 움직인다.

### Display 속성

요소를 어떻게 표시할지 설정한다.

- display: inline; 요소를 inline 처럼 표시하여 줄바꿈이 이러나지 않는다.
- display: block; 요소를 block요소 처럼(div처럼) 표시되어 요소 앞뒤로 줄바꿈이 된다.
- **display: none; 박스가 생성되지 않아 공간도 차지하지 않는다.**
- display: inline-block; 요소는 inline인데 내부는 block처럼 표시

### Visibility 속성

요소를 보일지 말지를 설정한다. 예를 들어 `visibility: hidden;`을 사용하면 공간이 남는걸 볼 수 있다. (공간유지)

### Float

float 속성은 글을 작성할 때, 본문 중간에 이미지를 넣고자 하거나, 이미지가 본문 중간에 왼쪽이나 오른쪽으로 위치하고, 텍스트가 자연스럽게 그 옆에 나오고 있는 모습을 만들게 해준다. 요소를 띄워서 왼쪽이나 오른쪽에 배치할 수 있도록 만들어 준다.

### Z-index

CSS z-index 속성은 위치 지정 요소와, 그 자손 또는 하위 플렉스 아이템의 Z축 순서를 지정한다. 더 큰 z-index 값을 가진 요소가 작은 값의 요소 위를 덮는다.

# 참고

- [The Difference Between ID and Class](https://css-tricks.com/the-difference-between-id-and-class/)
- [w3schools boxmodel](https://www.w3schools.com/css/css_boxmodel.asp)
- [CSS 레이아웃](https://joshua1988.github.io/web-development/css/layout-basic/)
- [반응형 웹 디자인](https://developers.google.com/web/fundamentals/design-and-ux/responsive/?hl=ko)
- [MDN Position-CSS](https://developer.mozilla.org/ko/docs/Web/CSS/position)
- [MDN CSS 참고서](https://developer.mozilla.org/ko/docs/Web/CSS/Reference#pcls)
- [CSS 기본](http://webberstudy.com/html-css/css-1/border/)
