# 객체 지향 프로그래밍(Object Oriented Programming)

객체 지향 프로그래밍이란 마치 하나의 모델이 되는 청사진(blueprint)를 만들고, 그 청사진을 바탕으로 한 객체(object)를 만드는 프로그래밍 패턴이다. 예를 들어 자동차라는 청사진이 있으면 그를 바탕으로 마즈다2, 골프, 코롤라 등의 차들이 나오다. 여기서 청사진을 **class**라 부르고, 청사진을 바탕으로 한 객체를 **instance**라고 부른다.

ES5에서 **class는 함수로 정의**할 수 있다.

```js
function Car(brand, name, color) {
  // instance가 만들어질 때 실행되는 코드
}
```

ES6에서는 **class라는 키워드를 이용해서 정의**할 수도 있다.

```js
class Car {
  constructor(brand, name, color) {
    // instance가 만들어질 때 실행되는 코드
  }
}
```

위에서 볼 수 있는 것과 같이 class를 정의할 땐 첫글자를 대문자로 표기한다.

**`new` 키워드를 통해 class의 instance를 만들어낼 수 있다.**

```js
let mazda2 = new Car("mazda", "mazda2", "blue");
let golf = new Car("volkswagen", "golf", "white");
let corolla = new Car("toyota", "corolla", "red");
// 각각의 instance는 Car라는 class의 고유한 속성과 메소드를 갖는다.
```

객체 지향 프로그래밍을 하는 이유는 현실 세계를 기반으로 프로그래밍 모델을 만들 때에 유용하기 때문이다. 현실 세계의 내용들을 프로그래밍으로 불러올 때 쓰인다. 계속해서 차를 예로 들면: Car의 속성으론 brand, name, color, currentFuel, maxSpeed를 들 수 있고, Car의 메소드론 refuel(), setSpeed(), drive() 등을 들 수 있다. 속성은 Car의 특징들이고, 메소드는 Car가 할 수 있는 행동을 나타낸다고 할 수 있다. **class에 속성과 메소드를 정의하고, instance에서 이용한다**.

**클래스에서 속성을 정의**할 때:

```js
// ES5
function Car(brand, name, color) {
  this.brand = brand;
  this.name = name;
  this.color = color;
}
```

```js
// ES6
class Car {
  constructor(brand, name, color) {
    this.brand = brand;
    this.name = name;
    this.color = color;
  }
}
```

위에서 class의 속성을 정의한 후에 instance를 만들어서 사용할 수 있다.

```js
let mazda2 = new Car("mazda", "mazda2", "blue");

mazda2.brand; // 'mazda'
mazda2.color; // 'blue'
// 이런 방법으로 클래스의 속성에 접근해서 가져다 사용할 수 있다.
```

**클래스에서 메소드를 정의**할 때:

```js
// ES5
function Car(brand, name, color) {
  this.brand = brand;
  this.name = name;
  this.color = color;
}
Car.propotype.refuel = function () {
  // 연료 공급을 구현하는 코드
};

Car.propotype.drive = function () {
  // 운전을 구현하는 코드
};
```

```js
// ES6
class Car {
  constructor(brand, name, color) {
    this.brand = brand;
    this.name = name;
    this.color = color;
  }
  refuel() {}

  drive() {}
}
```

위의 예제를 응용해서 사용한다면 다음과 같다:

```js
Car.prototype.drive = function () {
  console.log(this.brand + "달려라!");
};

golf.drive(); // golf달려라!
corolla.drive(); // corolla달려라!
// 이런 방법으로 해당하는 속성과 메소드를 가져다가 사용할 수 있다.
```

#### 용어정리

- **prototype**: 모델의 청사진을 만들 때 쓰는 원형 객체(original form)이다. 여기에 속성이나 메소드를 정의할 수 있다.
- **constructor**: 인스턴스가 초기화될 때 실행하는 생성자 함수. `new` 키워드를 통해 Car가 생성될 때 실행되는 것이 생성자(constructor) 함수이다.
- **this**: 함수가 실행될 때, 해당 scope마다 생성되는 고유한 실행 context(execution context), `new` 키워드로 인스턴스를 생성했을 때에는, 해당 인스턴스가 바로 this의 값이 된다.

지금까지 객체 지향을 봤을 때 배열과 비슷하다는 사실을 알 수 있다.

```js
let arr = ["hello", "world", "good"];
arr.length; // 3
arr.push("night"); // 새 element를 추가합니다.

// 여기서 배열을 정의하는 것은 Array의 인스턴스를 만들어내는 것과 동일하다.
let arr = new Array("hello", "world", "good");
```

또 다른 예를 들자면 MDN 메소드 설명에 prototype이라고 붙어있는 이유는 push(), pop(), map() 등의 구현이 원형 객체(Array)에 정의되어 있기 때문이다.

[OOP 관련 TIL](https://velog.io/@gunwooko/2020JUNE17-OOP)

# 참고

- [ES6 - class](https://poiemaweb.com/es6-class)
- [MDN - super](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/super)
- [ES6 - class 관련 블로그1](https://jongmin92.github.io/2017/06/18/JavaScript/class/)
- [Constructor/prototype 관련 블로그2](https://www.zerocho.com/category/JavaScript/post/573c2acf91575c17008ad2fc)
- [OOP 4가지 장점에 관한 영상](https://www.youtube.com/watch?v=pTB0EiLXUC8)
- [OOP 관련 영상 1](https://www.youtube.com/watch?v=PFmuCDHHpwk)
- [OOP 관련 영상 2](https://www.youtube.com/watch?v=_DLhUBWsRtw)
