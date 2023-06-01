## 클래스

### 자바스크립트에서 클래스가 생기기 전에는 어떤 방식으로 객체지향 패턴을 구현했는가?

<br />

#### 1. 생성자 함수를 통한 객체지향 패턴 구현

<br />

생성자 함수는 속성과 메소드를 공유하는 객체를 만드는데 널리 사용되었다.

생성자 함수는 객체의 인스턴스를 생성하기 위해 new 키워드를 사용해 호출되는 일반 함수이다.

생성자 함수 내에서 this를 사용해 속성과 메서드를 정의할 수 있다.

```
function JavaScript (name, date) {
  this.name = name;
  this.date = date;

  this.introduce = function () {
    return `My name is ${this.name}, release date is ${this.date}`
  }
}

const react = new JavaScript('react', 2011);

console.log( react.introduce() ); // My name is react, release date is 2011
```

<br />

위 코드에서는 JavaScript 함수는 JavaScript 객체를 생성하기 위한 생성자 역할을 한다.

name과 date 속성은 this를 사용해 할당하고 생성자 함수는 introduce 메서드를 정의해 개체의 이름 및 날짜 속성을 결합한 문자열을 반환한다.

<br />

#### 2. 프토로타입을 통한 객체지향 패턴 구현

<br />

```
function JavaScript(name, date) {
  this.name = name;
  this.date = date;
}

JavaScript.prototype.introduce = function () {
  return `My name is ${this.name}, release date is ${this.date}`
}

const react = new JavaScript('react', 2011);

console.log( react.introduce() ); // My name is react, release date is 2011
```

<br />

위 코드에서는 introduce라는 메소드를 JavaScript.prototype에 추가한다.

new 키워드를 사용해 JavaScript 개체의 인스턴스를 생성하고 name과 date 값을 전달해 할당된 속성을 가진 새 개체가 생성된다.

점 표기법을 사용해 JavaScript 개체 프로토타입의 introduce 메소드에 액세스할 수 있다.

프로토타입에 메소드를 추가하면 개체의 모든 인스턴스 간에 메서드를 공유해 메모리 사용량을 줄이고 성능을 향상시킬 수 있다.

<br />

#### 3. 모듈 패턴을 통한 객체지향 패턴 구현

```
const counter = (function() {
  let count = 0;

  function increment() {
    count++;
    console.log('Count: ' + count);
  }

  function decrement() {
    count--;
    console.log('Count: ' + count);
  }

  return {
    increment: increment,
    decrement: decrement
  };
})();

counter.increment(); // Count: 1
counter.decrement(); // Count: 0
```

<br />

개인 데이터를 캡슐화하고 클로저를 사용해 외부에서 액세스 할 수 없는 개인 변수 및 함수를 생성한다.

위 코드에서는 즉시 호출된 함수 표현식(IIFE)를 사용해 변수 count와 전용 함수 increment 및 decrement를 생성한다. 

<br />

### 생성자 함수와 클래스의 차이점은?

<br />

#### 상태 유지

<br />

생성자 함수와 클래스는 객체를 정의하고 생성하는 방법은 다르지만 유사한 목적을 수행하는데

이 둘 사이의 주요 차이점은 다음과 같다.

<br />

#### 1. 클래스 생성자는 new와 함께 호출하지 않으면 에러가 발생한다.

```
class JavaScript {
  constructor () {

  }
}

function React () {

}

JavaScript(); // Uncaught TypeError: Class constructor JavaScript cannot be invoked without 'new'
React();
```

<br />

#### 2. 클래스 메서드는 열거할 수 없다.

<br />

클래스의 포로토타입 프로퍼티에 추가된 메서드 전체의 enumerable 플래그는 false 이다.

enumerable 플래그는 for ...in으로 객체를 순환할 때, key의 값의 반환 유무를 뜻한다.

for ...in으로 객체를 순환 할 때 , 프로토타입 프로퍼티에 저장된 함수 값을 반환하는 것에서 차이가 발생한다.

- 생성자 함수 -> 함수 반환 O
- class -> 함수 반환 X

<br />

```
function JavaScript(name, date) {
  this.name = name;
  this.date = date;
}

JavaScript.prototype.introduce = function () {

}

class React {
  constructor(name, date) {
    this.name = name;
    this.date = date;
  }

  introduce() {

  }
}

let javascript = new JavaScript('javascript', 1995);
let react = new React('react', 2011);

for(let key in javascript) {
  console.log(key); // name, date, introduce
}

for(let key in react) {
  console.log(key); // name, date
}
```

<br />

### 클래스 정의는?

MDN에서는 클래스를 "특별한 함수"라고 설명하고 있다.

함수를 함수 표현식과 함수 선언으로 정의할 수 있듯이 class도 마찬가지로

class 표현식과 class 선언 두 가지 방법을 제공한다.

<br />

- 클래스 선언

<br />

```
class Rectangle {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
}
```

<br />

- 클래스 표현식

<br />

```
let Rectangle = class Rectangle2 {
  constructor(height, width) {
    this.height = height;
    this.width = width;
  }
};
console.log(Rectangle.name); // 출력: "Rectangle2"
```

<br />

### 클래스의 상속은?

<br />

프로토타입에서는 상속 개념을 사용하기 위해 프로토타입 체인을 사용했다.

이 방법은 다소 복잡한 부분이 있는데 ES6에서 class를 지원하면서 extends 키워드를 통해

상속을 더 쉽게 구현할 수 있게 되었다.

<br />

프토토 타입 체인을 사용한 상속 개념

```
let Water = function () {};

Water.prototype.drink = function () {
    return '마시기';
}

let Coke = function () {
    Water.call(this);
}

Coke.prototype = new Water();

let coke = new Coke();

console.log(coke.drink()); // 마시기
```

<br />

class와 extends를 사용한 상속 개념

```
class Water {
    constructor() {
    	
    }

    drink() {
        return '마시기';
    }
}

class Coke extends Water{
  constructor() {
  	super();
  }
}


let coke = new Coke();

console.log(coke.drink());
```
