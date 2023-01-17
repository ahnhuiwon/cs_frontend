## `strict mode`

### strict mode란?

ES5부터 추가된 기능으로, 자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나

자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대한 명시적인 에러를 발생시킨다.

(ES6에 도입된 클래스와 모듈은 기본적으로 strict mode가 적용된다.)

<br />

### stric mode 적용하기

```
'use strict';

function number_func = () => {
  x = 10;
}

// 또는

function nunmber_func =() => {
  'use_strict';
  
  x = 10;
}
```

### strict mode를 통해 무엇을 예방할 수 있는가?

**1. 암묵적 전역**

선언하지 않은 변수를 참조하면 reference Error가 발생한다.

<br />

**2. 변수, 함수, 매개변수의 삭제**

delete 연산자로 변수, 함수, 매개변수를 삭제하면 Syntax Error가 발생한다.

```
(function () {
  'use strict';

  var x = 1;
  delete x;
  // SyntaxError: Delete of an unqualified identifier in strict mode.

  function foo(a) {
    delete a;
    // SyntaxError: Delete of an unqualified identifier in strict mode.
  }
  delete foo;
  // SyntaxError: Delete of an unqualified identifier in strict mode.
}());
```

<br />

**3. 매개변수 이름의 중복**

중복된 매개변수 이름을 사용하면 Syntax Error가 발생한다.

```
function () {
  'use strict';

  //SyntaxError: Duplicate parameter name not allowed in this context
  function foo(x, x) {
    return x + x;
  }
  console.log(foo(1, 2));
}());
```

<br />

**4. with문의 사용**

with문을 사용하면 Syntax Error가 발생한다.

with문은 전달된 객체를 스코프체인에 추가한다.

width문은 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있어서 코드가 간단해지긴 하지만

성능과 가독성이 나빠진다.

그래서 width는 사용하지 않는것이 좋다.

```
(function () {
  'use strict';

  // SyntaxError: Strict mode code may not include a with statement
  with({ x: 1 }) {
    console.log(x);
  }
}());
```

