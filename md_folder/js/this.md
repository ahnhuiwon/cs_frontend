## this

### this란?

this란 '이것'이란 의미를 갖고 있으며 JavaScript 예약어이다.

<br />

### this 바인딩이란?

자바스크립트에서 this가 참조하는 것은 **함수가 호출되는 방식**에 따라 결정되는데

이것을 this 바인딩이라고 한다.

this 바인딩의 규칙은 다음과 같다.

- 기본 바인딩
- 암시적 바인딩
- 명시적 바인딩
- new 바인딩
- 화살표 함수

<br />

#### 기본 바인딩

4가지 가바스크립트의 this 바인딩 규칙 중 해당하는 것이 없을 때 적용되는 기본 규칙이다.

기본 바인딩이 적용될 경우 **this는 전역 객체에 바인딩** 된다.

(브라우저 환경인 경우 window, Node js 환경인 경우 global)

<br />

```
function console_func() {
  const window_num = 10;
  console.log(this.window_num);
}

console_func(); //  undefined
```

<br />

위 코드의 this는 전역 객체에 바인딩 되고 전역 객체에는 window_num이라는 프로퍼티가 없기 때문에 undefined가 출력된다.

전역 객체에 window_num이라는 프로퍼티가 있는 경우 해당 window_num 프로퍼티의 값을 출력하게 된다.

<br />

```
window.window_num = 10;

function console_func () {
  console.log(this.window_num);
}

console_func(); //  10
```

<br />

이와 별개로 엄격 모드에서는 기본 바인딩 대상에서 전역 객체는 제외된다.

전역 객체를 참조해야할 this가 있다면 그 값은 undefined가 된다.

```
'use strict'

window.window_num = 10;

function console_func () {
  console.log(this.window_num);
}

console_func(); //  Uncaught TypeError: Cannot read properties of undefined (reading 'window_num')
```

<br />

#### 암시적 바인딩

암시적 바인딩은 함수가 객체의 메소드로서 호출되는 상황에서 this가 바인딩 되는 것을 말한다.

이때 this는 해당 함수를 호출한 객체, 즉 콘텍스트 객체에 바인딩된다.

```
const human = {
  name : 'Mike',
  run : function () {
    console.log(this.name + "달리는 중...")
  }
}

human.run(); // Mike달리는 중...
```

<br />

암시적 바인딩을 사용할 때 발생할 수 있는 문제는 위와 같은 상황에서 함수를 매개변수로 넘겨서 실행하는 것이다. (콜백) 

위와 같은 상황에서 다음과 같이 객체에 정의되어 있는 함수의 레퍼런스를 매개변수로 전달하는 상황에서 어떤 결과가 나올까?

<br />

```
setInterval(human.run, 1000); // ?
```

답은 undefined이다. 이유는 setInterval 함수 안에 전달한 콜백은 human이라는 함수의 래퍼런스 일뿐, human의 콘텍스트를

가지고 있지 않기 때문이다. 이런 상황을 암시적 바인딩이 소실되었다고 한다.

따라서 아래 코드처럼 setInterval 내부에서 호출되는 콜백은 human 객체의 콘텍스트에서 실행되는 것이 아니기 때문에

this는 기본 바인딩이 적용돼서 전역 객체에 바인딩된다.

```
function setInterval(callback, delay){
  // delay만큼 대기...
  callback();   //  human.run()이 아닌 run()과 같다.
}
```

<br />

#### 명시적 바인딩

자바스크립트의 모든 function은 call(), apply(), bind()라는 프로토타입 메소드를 가지고 있다.

이 3가지 메소드 중 하나를 호출함으로써 this 바인딩을 코드에서 명시하는 것을 명시적 바인딩이라고 한다.

이때 this는 **내가 명시한 객체에 바인딩**된다.

<br />

```
const human = {
  name : 'Mike'
}

function run() {
  console.log(this.name);
}

run.call(human);  //  Mike
run.apply(human); //  Mike
```

<br />

run의 Function 프로토타입 메소드 call, apply의 매개변수로 바인딩할 객체를 넘겨주면서 

bar 함수를 실행할 때의 this 컨텍스트를 human으로 직접 바인딩 해주었다.

call()과 apply()의 동작은 같지만 두번째 매개변수로 객체의 인자를 전달해 주는데

call은 매개변수의 목록, apply는 배열을 받는다는 차이점이 있다.

<br />

**bind**

bind 메소드는 매개변수로 전달받은 오브젝트로 this가 바인딩된 함수를 반환한다.

이것을 하드 바인딩이라고 하는데 하드 바인딩된 함수는 이후 호출될 때마다 처음 정해진 this 바인딩을

가지고 호출된다.

<br />

```
const human = {
  name : 'Mike'
}

function run() {
  console.log(this.name);
}

const bounding = run.bind(human);

bounding(); //  Mike
```

<br />

#### new 바인딩

자바스크립트의 new 키워드는 함수를 호출할때 앞에 new 키워드를 사용하는 것으로 객체를 초기화할 때 사용하는데,

이때 사용되는 함수를 생성자 함수라고 한다.

그리고 생성자 함수에서는 this 키워드를 해당 생성자를 이용해 생성할 객체에 대한 참조로 사용한다.

<br />

```
function Human() {
  this.name = 'Mike';
}

const bounding = new Human();

console.log(bounding.name); //  Mike
```

<br />

#### 화살표 함수

ES6에서 추가된 화살표 함수는 this를 바인딩할 때 앞서 설명한 규칙들이 적용되지 않는다.

this에 어휘적 스코프(Lexical scope)가 적용된다. 즉, **화살표 함수를 정의하는 시점의 컨텍스트 객체가 this에 바인딩**된다.

<br />

```
const human = {
  name : 'Mike',
  run : function() {
    setInterval(()=>{
      console.log(this.name);
    },1000);
  }
}

human.run();  // 1초마다 Mike 출력...
```

<br />

setInterval의 콜백인 화살표 함수의 선언시에 this는 human 객체를 가리키고 있기 때문에 

콜백이 실행될 때 this는 human를 가리키게 된다.

화살표 함수로 선언시에 렉시컬 스코프를 통해 바인딩된 this는 apply, bind등의 함수나 new 함수로 오버라이드 할 수 없다.

그렇기 때문에 주로 콜백 함수로 사용할 때 유용하다.
