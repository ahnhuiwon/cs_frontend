## `배열`

### `자바스크립트에서 객체란?`

자바스크립트에서 데이터를 표현하는 방식 중 하나로 key와 value 쌍으로 구성된다.

![image](https://user-images.githubusercontent.com/94499416/204729331-54f1f81c-2105-496d-a09d-a43f14952969.png)
  
<br />

#### `함수와 메서드의 차이점?`

함수와 메서드의 차이점은 호출 방식에 따라 다르다.

함수를 호출하는 객체가 있는 경우 메서드라고 말하며, 함수를 호출하는 객체가 없는 경우 함수라고 한다.

아래 코드를 확인해보자.

<br />

```
const my_object = {
  object_show : function() {
    console.log('my_show 메서드 호출');
  }
}

function func_show() {
  console.log('func_show 함수 호출');
}

my_object.object_show();  //  메서드 호출
func_show();  // 함수 호출
```

<br />

위 코드에서 object_show() 함수는 객체 my_object의 프로퍼티이며, my_object 객체를 통해 호출했으므로 메서드이다.

반면 func_show() 함수는 객체를 생성하지 않고 직접 호출했으므로 함수이다.

하지만 func_show() 함수는 객체 없이 호출되는 것처럼 보이지만, 사실 func_show()를 호출하는 객체가 존재한다.

전역 범위에서 함수가 선언되는 경우 전역 객체인 window의 프로퍼티가 된다.

아래 코드를 실행해보자.

<br />

```
function func_show() {
  console.log('func_show 함수 호출');
}

func_show();
window.func_show();
```

<br />

![image](https://user-images.githubusercontent.com/94499416/204731150-1cfb3238-bd49-42e4-8dba-44d7ba1d87d8.png)

<br />

위 이미지를 보면 전역 객체인 window 객체로 func_show()를 호출했으므로 메서드가 아닌가? 라고 생각을 할 수 있다.

하지만 자바스크립트에서 메서드라는 개념은 사용자가 정의한 객체의 프로퍼티가 함수인 경우다.

따라서 func_show()는 메서드가 아니라 함수인것이다.

<br />

### `자바스크립트에서 객체를 생성하는 방법은?`

자바스크립트에서 객체를 생성하는 방법은 다음과 같다.

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

<br />

#### `객체 리터럴`

객체 생성 방식 중 가장 일반적이고 간단한 방법으로, 컨텐츠를 그대로 대입하는 방법이다.

```
let my_object = {
  first_key : first_value,
  second_key : second_value,
  third_key : third_value,
}
```

<br />

#### `Object 생성자 함수`

new 키워드를 이용해 Object 생성자 함수를 호출하면 비어있는 객체를 얻을 수 있다.

다만 new Object()를 호출하면 비어있는 객체를 생성하기 때문에 객체 생성 직후에는 프로퍼티를 추가해줘야한다.

```
let my_object = new Object();

my_object.name = "heets";
my_object.price = "4500";
my_object.type = "electron"
```

<br />

#### `Object 생성자 함수`

new 키워드를 이용해 Object 생성자 함수를 호출하면 비어있는 객체를 얻을 수 있다.

다만 new Object()를 호출하면 비어있는 객체를 생성하기 때문에 객체 생성 직후에는 프로퍼티를 추가해줘야한다.

```
let my_object = new Object();

my_object.name = "heets";
my_object.price = "4500";
my_object.type = "electron"
```

<br />

#### `Object.create() 메서드`

지정된 프로토타입 객체와 프로퍼티를 가지고 새로운 객체를 만든다.

사용자가 프로토타입 객체를 직접 명시할 수 있으며 첫번째 인수로 사용할 객체, 두번쨰 인수로 새로운 객체의 추가할 프로퍼티 정보를 전달한다.

```
const my_object = Object.create(Object.prototype, {
    smoke : { value : "heets", writable: true, enumerable : true, configurable: true}
})

console.log(my_object);
```

<br />

생성자 함수를 통해 객체를 생성하면 같은 속성을 가진 객체를 여러 개 생성할 수 있다.

또한 생성자 함수에서 정의한 this는 생성자 함수로 생성된 인스턴스가 된다.

생성자 함수는 인스턴스를 생성하기 전에, 먼저 비어있는 객체를 생성한다.

this는 비어있는 객체를 가리키고 그 객체에 name, leg, food 프로퍼티를 추가한 것이다.

생성자 함수에 반환 값이 없다면 비어있는 객체에 새로운 프로퍼티를 추가한 this가 반환된다.

<br />

![image](https://user-images.githubusercontent.com/94499416/204735421-6c5702a5-96d2-4dc6-8c56-882742aa4b5d.png)

<br />

#### `클래스(ES6)`

클래스 생성자는 객체를 생성할 때 인자를 프로퍼티에 전달하여 생성한다.

```
class Animal {
  constructor(name, leg, food){
    this.name = name;
    this.leg = leg;
    this.food = food;
  }
}
```

다만 인자를 전달할 필요 없이 프로퍼티를 선언하고 할당 할 수 있다.

```
class Animal {
  name = 'monkey';
  leg = 2;
  food = "banana";
}
```
