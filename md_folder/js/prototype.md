## `프로토타입`

### 객체지향 프로그래밍은 무엇을 의미하는가?

객체지향 프로그래밍(OOP, Objectr Oriented Programming)은 프로그래밍하는 대상을 하나의 객체(사물)로 정의하는 설계 방법으로

객체의 관점에서 구조를 만들고 사용하는 방법이다. 설명을 덧 붙인다면 단순한 자료 구조를 넘어서 기능(메소드)를 포함한

형태로 객체를 사용하는 프로그래밍이다.

<br />

### 객체지향 프로그래밍의 특징은?

1. 캡슐화

변수와 함수를 하나로 묶고 필요에 따라 접근 권한을 나누어 외부에서 함부로 접근하지 못하게 

제한을 두어 객체의 손상을 방지한다. 이에 따라 내부 구현 내용을 감추어 외부에서 확인 할 수 없도록 **정보 은닉**도 포함되게 된다.

2. 추상화

객체들이 사용하는 **공통적인 변수와 함수들을 따로 묶는 것**을 말한다.

예를 들어보자 여러 자동차가 있다고 치면, 이 자동차가 공통적으로 수행하는 행동 중 운전하기, 멈추기 등등이 있을 것이고

브랜드, 종류 등 공통 적으로 가지고 있는 특징들도 있을것이다.

이렇게 **공통적인 행동과 특징들을 가지고 하나의 객체를 정의 하는 과정**을 추상화로 볼 수 있다.

3. 상속

자식 객체가 부모 객체의 변수와 함수를 그대로 물려 받을 수 있는 것을 말한다.

예를 들어 자동차라는 객체에 운전하기, 멈추기 메서드가 있다면

승용차와 스포츠카 객체를 만들 때 자동차 객체를 상속 받아 승용차, 스포츠카 객체에서는 운전하기, 멈추기 메서드를 따로 구현하지 않고

자동차의 운전하기, 멈추기 메서드를 쓸 수 있다.

4. 다형성

같은 객체임에도 상황에 따라 다르게 동작할 수 있는 것을 뜻한다.

오버로딩이나 오버라이딩 같은 것을 사용하여 객체를 상황에 따라 다르게 사용 할 수 있다.

> 오버로딩(overloading)? 같은 이름의 함수명을 가지면서 매개 변수의 유형과 개수를 다르게 만들어 사용할 수 있다. (Javascript에서는 변수 타입이 자유로워 사실상 없는 개념) 

> 오버라이딩(overriding)? 부모 객체가 가지고 있는 함수를 자식 객체가 해당 함수를 재정의해서 사용할 수 있다.

```
class Car {
  drive() {
    console.log('적당한 속력으로 운전중...');
  }
}

class SportsCar extends Car {
  drive() {
    console.log('매우 빠른 속도로 운전중...')
  }
}

const sportsCar = new SportsCar();
sportsCar.drive();  // 매우 빠른 속도로 운전중...
```

<br />


### 자바스크립트는 객체지향 프로그래밍 언어인가?

자바스크립트는 멀티-패러다임 언어로 명령형, 함수형, 프로토타입 기반 객체지향 언어다.

비록 다른 객체지향 언어들과의 차이점으로 인한 논쟁들이 있긴 하지만, 자바스크립트는 강력한 객체지향 프로그래밍 능력들을 지니고 있다.

이전에는 클래스가 없어서 객체지향이 아니라고 생각하는 사람들도 있었으나 프로토타입 기반의 객체지향 언어이다.

ES6에서는 Class가 등장했지만 엄연히 Class가 새로운 객체지향 모델을 제공하는 것이 아니며 

Class도 사실 함수이고 기존 prototype 기반 패턴의 syntactic sugar이다.

> syntactic sugar 문법적 기능은 그대로인데, 직관적으로 쉽게 코드를 읽을 수 있게 만든다라는 뜻

<br />

### 프로토타입이란?

뜻을 찾아보면 일반적인 의미로 **원형**이라는 뜻을 가지고 있다.

이것을 객체에 의미를 부여한다면 **객체의 원형** 즉 **자신을 만들어낸 객체의 원형**을 뜻한다.

JavaScript에서는 이러한 프로토타입을 표현하는 용어가 있다.

- Prototype Link : 자신을 만들어낸 객체의 원형
- Prototype Object : 자신을 통해서 만들어질 객체의 원형

<br />

```
function car() {}
console.dir()
```

<br />

![image](https://user-images.githubusercontent.com/94499416/211996810-4ed21f7a-df2d-4c1d-8251-c5d3e5744b0b.png)

<br />

prototype 속성과 `__proto__` 속성을 확인 할 수 있다.

이들의 관계를 표시한다면 아래 이미지와 같다.

<br />

![image](https://user-images.githubusercontent.com/94499416/211997049-be1d9d9e-1ce7-4202-98f5-31ad832f726e.png)

<br />

- `__proto__` : 자신을 만들어낸 객체의 원형
- constructor : 생성자를 뜻하며 자신을 만들어낸 객체
- prototype : 자신을 원형으로 만들어진 새로운 객체

`__proto__` 속성은 Prototype Link로 연결되어 자신을 만들어낸 객체를 연결 시키고

constructor 속성은 Prototype Object로 연결되어 자신을 만들어낸 객체에 연결 시키고

prototype 속성은 Prototype Object로 연결되어 자신이 만들어 낸 새로운 객체에 연결시킨다.

그리고 Prototype Object는 생성 당시에 객체가 가진 정보를 토대로 새로운 객체를 생성한다.

```
let Car = function(brand) {
  this.brand = brand;
  this.drive = function() {
    console.log(this.brand + "운전중...");
  }
}

Car.drive = function() {
  console.log(this.brand + "정지중!");
}

let my_car = new Car('kia');
my_car.drive(); //  kia운전중...
```

<br />

위 코드처럼 중간에 정지중!으로 변경했지만 운전중... 그대로 나오는 것을 확인할 수 있다.

이는 Car 객체의 Prototype Object가 Car 객체 생성 당시의 정보인 drive 메서드를 복제하기 때문에

Car 객체를 이용해서 새로 만든 객체의 경우 운전중...을 출력하는 dirve 메소드가 그대로 복제된것이다.

<br />

**프로토타입 사용 이유**

JavaScript는 Class 라는 개념이 존재하지 않는다. 정확히는 Class 라는 키워드가 추가되어 클래스처럼 표현 할 수 있지만

이는 문법만 매핑을 한것이고 동작 방법은 프로토타입을 활용하여 객체를 생성하는 것과 같다.

JavaScript는 Class 라는 개념이 존재 하지 않기 때문에 프로토타입이라는 객체를 활용해 이를 Class 처럼 표현하기 위해 사용한다고 볼 수 있다.
