## `데이터 타입`

### `데이터 타입의 종류는 어떤 것들이 있는가?`

- 원시 타입(Primitive data type) : 원시 타입의 값은 변경 불가능한 값이며 값에 의한 전달이다.
  - Number
  - String
  - Boolean
  - null
  - undefined
  - symbol (ES6에서 추가됨)
- 객체 타입
  - Object
  
<br />

### `원시타입`

#### `숫자(Number)`

int, long, float, double과 같이 다양한 숫자 타입이 존재하는 C언어와 달리 자바스크립트에서는

단 하나의 숫자 타입만 존재한다.

자바스크립트는 모든 숫자를 64비트 부동 소수점 형태로 저장하기 때문에 정수나 실수의 구분 없이 변수에 바로 값을 대입할 수 있다.

다만 모든 숫자를 실수로 처리하기 때문에 나누기 연산을 할 경우 C언어와 달리 소수점까지 출력하므로 주의해야한다.

<br />

#### `문자열(String)`

C언어에서는 문자 하나만을 저장하는 char 타입이 존재하는 반면, 자바스크립트에서는 문자열의 길이에는

상관없이 string이라는 데이터 타입으로 값이 생성된다.

문자열을 다룰 때 조심해야할 점은 한 번 정의한 문자열은 변하지 않는다는 점이다.

<br />

```
let my_string = 'javascript';

my_string[0] = 'J';
console.log(my_string); //  javascript
```

<br />

#### `불린(Boolean)`

자바스크립트에서는 true와 false 값을 나타내는 불린 타입이 존재한다.

```
let my_flag = true;
console.log(my_flag); //  boolean
```

<br />


#### `undefined`

값이 할당되지 않은 변수를 undefined 타입으로 표현한다.

특이한 점은 undefined 타입의 변수 값 또한 undefined라는 것이다.

따라서 다음과 같이 아무런 값이 할당되지 않은 변수는 undefined 타입이 출력된다.

```
let my_temp;
console.log(typeof my_temp);  // undefined
console.log(my_temp); //  undefined
```

<br />

#### `null`

undefined와 달리 null 타입은 명시적으로 값이 비어있음을 나타내는데 사용한다.

다만 null 값을 할당한 변수의 데이터 타입을 확인하면 null이 아닌 object가 출력된다.

따라서 null 타입의 변수인지 확인하기 위해서는 typeof 연산자를 사용하는게 아니라 일치 연산자를 사용해야 한다.

```
let my_temp = null;
console.log(typeof my_temp);  // object
console.log(my_temp); //  null
```

<br />

#### `Symbol`

Symbol 타입은 아래에서 설명하겠다.

### `참조 타입`

#### `객체(Object)`

자바스크립트에서 원시 타입을 제외한 모든 값은 객체로 취급된다.

따라서 배열, 함수도 모두 객체로 표현하는데 주로 key-value 쌍의 데이터를 저장하며

하나의 값만 저장되는 기본 데이터 타입과는 다르게 여러 개의 프로퍼티(속성)를 저장할 수 있다.

이런 객체의 프로퍼티는 원시 데이터 타입의 값을 가지거나 다른 객체를 가리킬 수 있다.

이러한 성질로 함수도 객체의 프로퍼티로 지정할 수 있고 자바스크립트에서는 이런 프로퍼티를 **메서드**라고 부른다.

```
var my_object = {
  name : 'class',
  age : '28',
  job : 'teacher',
  get_info : function() {
    return this.name + " : " + this.age;
  }
}

console.log( my_object.name, my_object.age, my_object.job)
console.log( my_object.get_info() )
```

<br />

### `Symbol 타입이란?`

Symbol 타입은 ECMA Script 6에서 새롭게 등장한 데이터 타입으로, 

충돌 위험이 없는 고유한 프로퍼티를 만들기 위한 데이터 타입이다.

```
let my_temp = Symbol('temp');
console.log(typeof my_temp);  // symbol
console.log(my_temp === Symbol(my_temp)); //  false
```

<br />

### `데이터 타입이 필요한 이유?`

```
const score = 100;
```

변수 score와 리터럴 100이 있다. 숫자 값 100을 저장하기 위해 메모리 공간을 살펴보자.

- 1) 자바스크립트 엔진이 리터럴 100을 숫자 타입의 값으로 해석한다.
- 2) 숫자 타입의 값 100을 저장하기 위해 8바이트 메모리 공간을 확보한다.
- 3) 100을 2진수로 저장

식별자 score를 통해 숫자 타입의 값 100이 저장되어 있는 메모리 공간의 주소를 찾아갈 수 있다.

다만 값을 참조하려면 한번에 읽어들어야할 메모리 공간의 크기, 즉 메모리 셀의 개수(바이트 수)를 알아야 한다.

score 변수의 경우, 저장되어 있는 값이 숫자 타입이므로 8바이트 단위로 읽어 들이지 않으면 값이 훼손된다.

숫자 타입은 8바이트 단위로 저장되므로, score 변수를 참조하면 8바이트 단위로 메모리 공간에 저장된 값을 읽어들인다.

score 변수를 참조해 메모리 공간의 주소에서 읽어들인 2진수를 숫자로 해석한다.

**정리**
- 값을 저장할때 확보해야하는 메모리 공간의 크기를 결정하기 위해
- 값을 참조할때 한번에 읽어들여야할 메모리 공간의 크기를 결정하기 위해
- 메모리에 읽어들인 2진수를 어떻게 해석할지 결정하기 위해

<br />

### `동적타이핑이란?`

동적타이핑은 코드를 작성하는데 있어 컴퓨터적 구조를 생략한다.

따라서 변수를 지정할 때 해당 변수의 데이터 타입등을 명시하지 않아도 컴퓨터가 알아서 해석한다.

예를 들어 a = 15 변수를 지정할대 a가 숫자라고 명시하지 않더라도 컴퓨터는 이를 스스로 숫자라 해석한다.

이 방식은 코드를 보다 간결하게 해주며 코드의 로직을 보다 명확히 보여주지만

데이터 타입이 뭔지 파악하는 것을 컴퓨터에게 맡기기 때문에 그 만큼 실행속도가 느려진다.

<br />

### `정적타이핑이란?`

정적타이핑은 코드를 작성할 때 컴퓨터적 구조를 명시해준다.

int a = 15 라는 식으로 변수의 데이터 타입을 직접 명시하며 컴퓨터가 할 일을 덜어주는 것이다.

코드를 작성하는데 작은 정보들까지 개발자가 직접 신경쓰도록 하여 코드의 안정성과 정교함이 커진다.

다만 코드가 매우 길고 복잡해져 처음 프로그래밍에 입문하기에는 어렵다.

<br />
