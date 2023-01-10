## `함수와 일급 객체`

### 일급 객체란?

일급객체란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다.

일급객체의 조건에 대해서 정의를 알아보자.

- 변수에 할당할 수 있다.
- 다른 함수를 인자로 전달 받는다.
- 다른 함수의 결과로서 리턴할 수 있다.

위에 대한 조건으로 인해 알 수 있는 것은 함수를 데이터(string, number, boolean, array, object)

다루듯이 사용할 수 있다는점이다.

아래는 일급객체의 조건 예시를든 코드이다.

**변수에 할당한다**

```
const plus_func = (param) => {
  return param + param;
}
```

<br />

**다른 함수를 인자로 받는다**

```
const plus_func = (param) => {
  return param + param;
}

const plus_number = (func, param) => {
  return func(param);
}

const result = plus_number(plus_func, 2); // 4
```

<br />

**다른 함수의 결과로 리턴 될 수 있다**

```
const add_func = (param1) => {
  return (param2) => {
    return param1 + param2;
  }
}

add_func(3)(4); //  7
```

<br />

### 자바스크립트에서 함수가 일급 객체라면, 일급 객체로 뭘 할 수 있는가?

- 고차함수를 만들 수 있다.
- 콜백을 사용할 수 있다.

<br />

**고차 함수란?**

함수를 전달인자 또는 매개변수로 받거나 함수를 리턴하는 함수를 말한다.

```
// 다른 함수를 인자로 받는 경우
const plus_func = (param) => {
  return param + param;
}

const plus_number = (func, param) => {
  return func(param);
}

// 함수를 리턴하는 경우
const add_func = (param1) => {
  return (param2) => {
    return param1 + param2;
  }
}
```

<br />

**콜백 함수란?**

전달인자로 받는 함수이다.

```
const plus_func = (param) => {
  return param + param;
}

const plus_number = (func, param) => {
  return func(param);
}

plus_number(plus_func, 2);  //  4
```

<br />

### 함수형 프로그래밍이란? 

객체지향 프로그래밍과 달리 함수를 기반으로 돌아간다.

함수형 프로그래밍은 몇 가지 원칙이 있다.

- 입출력이 순수해야한다.
- 부작용이 없어야한다.
- 함수와 데이터를 중점으로 생각한다.

위 두 개는 같은 소리이다. 입출력이 순수하다는 것은 반드시 하나 이상의 인자를 받고, 받은 인자를 처리하여

반드시 결과물을 돌려주어여한다는 것이다. 인자를 제외한 다른 변수는 사용하면 안된다.

받은 인자만으로 결과물을 내어야하는데 이러한 함수를 순수함수라고 부른다.

부작용이 없어야한다는것은, 개발자가 바꾸고자하는 변수 외에는 바뀌어서는 안 된다는 뜻이다. 즉 원본 데이터는 불변해야 한다는것이다.

```
const my_arr = [1, 2, 3, 4, 5];
const my_map = my_arr.map(function(x) {
  return x * 2;
}); // [2, 4, 6, 8, 10]
```

<br />

### 순수 함수? 일반 함수와는 어떤 차이가 있는가? 

- 순수 함수 : 어떤 외부상태에 의존하지 않고 변경하지도 않는, 부수효과가 없는 함수
- 비순수함수 : 외부 상태에 의존하거나 외부상태를 변경하는, 부수효과가 있는 함수

<aside>
💡 부수효과(Side Effect)란?
  외부 상태를 변경하거나 함수로 들어온 인자 상태를 변경하는 
</aside>

<br />

**순수 함수**

동일한 인수가 전달되면 언제나 동일한 값을 반환하는 함수다. 

즉 오직 매개변수를 통해 함수 내부로 전달된 인수에게만 의존해 반환 값을 만든다.

```
var count = 0;

const increase = (param) => {
  return ++param;
}

count = increase(count);
console.log(count);
```

<br />

**비순수함수**

외부 상태에 따라 반환값이 달라지며 함수의 외부상태를 변경하는 부수효과가 있다.

```
var count = 0;

function increase() {
return ++n;
}

increase();
console.log(count);  //1
```

<br />

비순수함수는 외부상태를 변경하므로 상태변화를 추적하기 어려워진다.

따라서 함수 외부 상태의 변경을 지양하는 순수함수를 사용하는 것이 좋다.
