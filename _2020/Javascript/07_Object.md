# 객체 (Object)

객체는 하나의 변수에 여러 가지 정보가 담겨 있을 때 사용하면 적합한 자료구조이다. 객체는 키와 값(key-value pair) 쌍으로 이루어져 있다. 키와 값 사이는 콜론(:)으로 구분하고, 중괄호{curly bracket}를 이용해서 객체를 만든다. 그리고 쉼표(,)를 사용해서 키-값 쌍을 구분한다. 객체에서 키에 대한 값은 무엇이든 들어갈 수 있다.

```js
let user = {
  firsname: "gunwoo",
  lastname: "ko",
  language: ["korean", "spanish", "english"],
  major: "theology",
  hobby: "coding",
};
```

객체의 값을 사용하는 방법은 두 가지가 있다:

## **1. Dot notation**

온점(.)을 사용해서 가지고 올 수 있다. `.키워드`를 사용해서 해당하는 `값`을 가지고 올 수 있다.

```js
let user = {
  firsname: "gunwoo",
  lastname: "ko",
  language: ["korean", "spanish", "english"],
  major: "theology",
  hobby: "coding",
};

user.firstname; // 'gunwoo'
user.language; // ['korean', 'spanish', 'english']
```

## **2. Bracket notation**

대괄호([ ])를 사용해서 가지고 올 수 있다. `["키워드"]`를 사용해 해당하는 `값`을 가지고 올 수 있다.

```js
let user = {
  firsname: "gunwoo",
  lastname: "ko",
  language: ["korean", "spanish", "english"],
  major: "theology",
  hobby: "coding",
};

user["firstname"]; // 'gunwoo'
user["language"]; // ['korean', 'spanish', 'english']
```

여기서 주의할 점은 키워드가 문자열 형식으로 들어간다는 것이다. 만일 문자열로 가지고 오지 않는다면 에러가 나오게 된다.

```js
user[lastname];
```

![](https://images.velog.io/images/gunwooko/post/9536494d-f897-4efa-b19a-0c9c6a937760/referenceError.png)
lastname이 정의되지 않았다고 나온다. 여기서 지금 lastname은 키값이 아닌 변수로 취급되기 때문이다. 그렇다면 이 문제를 어떻게 해결할 수 있을까? 두 가지 방법이 있는데, 하나는 키값을 문자열 형식으로 넣는 것이고, 다른 방법은 문자열에 담은 키값을 변수로 지정하는 방법이 있다.

```js
let keyname = "lastname";
user[keyname]; // "ko"
user[keyname] === user["lastname"]; // true
user[keyname] === user.lastname; // true
user["lastname"] === user.lastname; // true
```

그런즉 `user[keyname]`과 `user['lastname']`은 같다.

그러면 언제 dot notation을 사용하고 bracket notation을 사용해야 될까? 키값이 동적일 때 bracket notation을 사용하면 된다. 즉, 키값이 변수일 때 bracket notation을 사용하면 된다. dot notation은 정해진 키 이름에만 사용할 수 있다.

## 객체에 값 추가하기

객체에 **dot notation**과 **bracket notation**을 이용해 값을 추가할 수도 있다.

```js
let user = {
  firsname: "gunwoo",
  lastname: "ko",
  language: ["korean", "spanish", "english"],
  major: "theology",
  hobby: "coding",
};

user.isMarried = true; // 불린 값을 넣어도 된다.
user["age"] = 28; // 숫자도 가능하다.
user.address = {
  // 객체 안에 객체도 가능하다.
  city: "red cliffs",
  state: "victoria",
  country: "australia",
};
```

## 객체에 값 삭제하기 'delete'

객체에 `delete` 키워드를 사용해 값을 삭제할 수 있다.

```js
delete user.major; // major 값이 삭제된다.
delete user["language"]; // language 값이 삭제된다.
```

## 객체에 해당 키가 있는지 확인하기 'in'

객체에서 `in` 연산자를 이용해서 해당하는 키가 있는지 확인할 수 있다.

```js
"lastname" in user; // true (불린 값으로 나온다)
"email" in user; // false
```

## 객체의 속성을 다른 객체로 복사하기Object.assign()

`Object.assign(target, ...sources)` 메소드는 열거할 수 있는 하나 이상의 출처 객체로부터 대상 객체로 속성을 복사할 때 사용한다. 대상 객체를 반환한다.

# 참고

- [MDN - Object.assign()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
