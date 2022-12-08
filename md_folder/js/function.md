## `함수`

### `자바스크립트에서 함수를 정의하는 방법은?`

#### `named function declaration (명명 함수 선언)`

가장 대중적인 방법으로 함수의 이름이 say_hello 된다. 

호이스팅 되기 때문에 이 함수는 어느 스코프에서든 호출 할 수 있는 함수가 된다.

```
function say_hello(text) {
  console.log(text)
}

say_hello('Hi')
```

<br />

#### `anonymous function expression (익명 함수 표현)`

이름이 없는 함수를 변수에 담은 방식이다. 이름이 없는 함수긴 한데, 자바스크립트 엔진이 이름을 변수명으로 추정하여 넣는다.

다만 변수 할당은 호이스팅 되지 않으므로, 할당 된 이후에만 실행 가능하다.

```
const say_hello = function(text){
  console.log(text);
}

say_hello('Hi')
```

<br />

#### `named function expression (명명 함수 표현)`

2와 거의 동일하다. 다른 점은 함수 이름이 명확하게 선언되어 있으므로 JS 엔진에 의해 추론되지 않는 다는 것이다.

```
const say_hello = function hello_func(text){
  console.log(text);
}
```

<br />

#### `function constructor`

이는 eval()을 사용하는 것과 같기 때문에 굉장히 위험하다. 그리고 이 생성자는 전역 범위로 한정된 함수만 생성할 수 있다.

```
const my_calc = new Function('a', 'b', 'return a+b');
my_calc(1, 2);
```

<br />

#### `arrow function (화살표 함수)`

기존 함수와 몇가지 다른게 있다면
- constructor로 쓰일 수 없다.
- prototype을 가지고 있지 않는다.
- yield 키워드를 허용하지 않으므로 generator를 쓸 수 없다.
- this도 다르다.


```
const say_hello = (text) => {
  console.log(text);
}

say_hello('hi');
```

<br />

### `함수 선언문과 함수 표현식의 차이는?`

#### `함수 선언식 (function declartion)`

함수명이 정의되어 있고, 별도의 할당 명령이 없는 것

```
function sum_func(a, b) {
  return a + b
}
```

<br />

#### `함수 표현식 (function Expression)`

정의한 function을 별도의 변수에 할당하는 것

```
const sum_func = function (a, b) {
  return a + b
}
```

<br />

일단 주요 차이점은, 호이스팅에서 차이가 발생한다.

함수 선언식은 함수 전체를 호이스팅하는데, 정의된 범위의 맨 위로 호이스팅되어 함수 선언 전에 함수를 사용할 수 있다는 점이다.

반대로 함수 표현식은 별도의 변수에 할당하는데, 변수는 선언부와 할당부를 나누어 호이스팅하게 되어 선언부만 호이스팅하게 된다.

```
sum(50, 50); // 100
minus(100, 50) // Uncaught TypeError: minus is not a function

function sum(a, b) { // 함수 선언식
  return a + b;
}

var minus = function (a,b) { // 함수 표현식
  return a - b;
}
```

<br />

### `즉시 실행 함수(IIFE)란?`

즉시실행함수는 정의되자마자 즉시 실행되는 함수를 말한다.

즉시실행함수는 아래와 같이 소괄호()로 함수를 감싸서 실행하는 문법을 사용한다.

즉시실행함수에도 이름을 붙여서 사용할 수 있다. 다만 즉시실행함수는 선언과 동시에 호출되어 반환되기 때문에

재사용 할 수 없어 이름을 지어주는 것이 의미가 없다.

다만 즉시실행함수에 이름을 붙이냐, 안붙이냐는 개발자들 사이에서도 의견이 갈린다.

```
(function(){
  console.log(1);
})();

(()=>{
  console.log(1);
})();
```

#### `즉시실행함수의 사용 이유는?`

1. 필요 없는 전역 변수의 생성을 줄일 수 있다.

함수를 생성하면 그 함수는 전역 변수로써 남아있게 되고, 많은 변수의 생성은 전역 스코프를 오염시킬 수 있다.

즉시실행함수를 선언하면 내부 변수가 전역으로 저장되지 않기 때문에 전역 스코프의 오염을 줄일 수 있다.

2. private한 변수를 만들 수 있다.

즉시실행함수는 외부에서 접근 할 수 없는 자체적인 스코프를 가지게 된다. 이는 클로저의 사용 목적과도 비슷하며

내부 변수를 외부로부터 private 하게 보호할 수 있는 장점이 있다.
