## `생성자 함수에 의한 객체 생성`

### 생성자 함수란?

new 연산자와 함께 object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.

생성자 함수에 의해 생성된 객체를 인스턴스라고 한다.

```
const my_fruit = new Object();

my_fruit.name = 'banana';
my_fruit.myText = function() {
  console.log('This is ' + this.name);
}

console.log(my_fruit);
my_fruit.myText();
```

<br />

![image](https://user-images.githubusercontent.com/94499416/209273622-31a894f6-47a4-4c96-80cf-584e9d3b9da5.png)

<br />

new 연산자와 함께 object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.

빈 객체를 생성한 이후에는 프로퍼티 또는 메서드를 추가하여 객체를 완성 시킬 수 있다.

자바스크립트는 Object 생성자 함수 이외에도 String, Number, Boolean, Function, Array, Date, Promise 등의

빌트인 생성자 함수를 제공한다.

<br />

### `객체 리터럴로 만들 때와는 무슨 차이가 있는가?`

객체 리터럴에 의한 객체 생성 방식은 직관적이고 간편하다. 하지만 객체 리터럴에 의한 객체 생성 방식은

단 하나의 객체만 생성하기 떄문에 동일한 프로퍼티를 갖는 객체를 여러개 생성하는 경우

매번 같은 프로퍼티를 기술해야하기 때문에 비효율적이다.

```
const my_squre = {
  width : 10,
  height : 10,
  
  get_area() {
    return this.width * this.height;
  }
}

console.log(my_squre.get_area());

const my_squre2 = {
  width : 20,
  height : 20,
  
  get_area(){
    return this.width * this.height
  }
}

console.log(my_squre2.get_area());

```

<br />

### `왜 생성자 함수를 사용하는가?`

생성자 함수에 의한 객체 생성은 마치 객체(인스턴스)를 생성하기 위한 템플릿처럼 생성자 함수를 사용하여

프로퍼티가 동일한 객체 여러 개를 간편하게 생성할 수 있다.

```
function My_squre( width, height ) {
  this.width = width;
  this.height = height;
  
  this.get_area = function () {
    return width * height;
  }
}

const temp_squre = new My_squre(10, 10);
const temp_squre2 = new My_squre(20, 20);

console.log(temp_squre.get_area()); //  100
console.log(temp_squre2.get_area());  // 400
```

<br />

생성자 함수는 이름 그대로 객체를 생성하는 함수이다.

하지만 자바와 같은 클래스 기반 객체 지향 언어의 생성자와는 다르게 그 형식이 정해져 있지 않고

일반 함수와 동일한 방법으로 생성자 함수를 정의하고 호출 시 new 연산자와 함께 호출하면 생성자 함수로 동작한다.

new 연산자와 함께 생성자를 호출하지 않으면 생성자 함수가 아닌 일반 함수로 동작한다.

```
const my_squre3 = My_squre(10, 10);

console.log(width, height)  // 10, 10
```

<br />

### 생성자 함수가 객체(인스턴스)를 생성하는 과정

