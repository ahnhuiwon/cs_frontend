## `변수`

### `변수란?`

컴퓨터 메모리에 어떤 데이터를 저장하기 위한 이름을 가진 공간이다.

지정한 이름을 통해 정해진 공간에 값을 저장하고 사용한다.

<br />

### `식별자란?`

변수나 함수의 이름을 작성할 때 사용하는 이름을 의미한다.

#### 식별자는 다음과 같은 규칙이 있다.
- 영문자(대소문자)
- 숫자
- 특수문자의 경우 "_ "언더스코어 또는 $만을 사용한다.

#### 식별자 작성 방식
- Camel Case 방식 : var firstVar = 0;
- Underscore Case 방식 : var first_var = 0;

<br />

### `변수를 선언한다는 것은?`

변수를 선언할 때는 'let', 'var', 'const'라는 키워드를 사용한다.

이것은 곧 자바스크립트에 변수가 생겼다는 것을 의미하고

어떤 값을 넣을 수 있는 자리를 컴퓨터 메모리에 미리 잡아둔 것으로 이해할 수 있다.

키워드들은 소문자로 사용하며 한번 선언을 한 뒤에는 다시 선언을 하지 않는다.

<br />

```

let my_data; // my_data라는 이름을 가진 변수를 let 키워드로 선언

```

<br />

### `var 키워드?`

1. 중복 선언이 가능하다.

<br />


```

// 첫번째 변수 선언과 초기화
var a = 10;
console.log(a); // 10


// 두번째 변수 선언과 초기화
var a = 20;
console.log(a); // 20


// 세번째 변수 선언
var a;
console.log(a); // 20

```

<br />

var로 선언한 변수는 중복해서 선언과 초기화가 가능하다.

이러한 경우에는 마지막에 할당된 값이 변수에 저장된다.

단 초기화 없이 선언만 한 경우에(3번쨰) 에러는 발생하지 않고 선언문 자체가 무시된다.

<br>

2. 값의 재할당이 가능한 변수이다.

```

var a = 10;
a = 20;
console.log(a);  // 20

```

<br>

변수 선언 및 초기화 이후에 반복해서 다른 값을 재할당 할 수 있다.

<br>

3. 함수 레벨 스코프

var는 함수 내부에 선언된 변수만 지역변수로 한정하며, 나머지는 모두 전역변수로 간주한다.

<br />

```

function temp_func(){
    var a = 10;
    console.log(a);
}

hello(); // 10

console.log(a);  //ReferenceError: a is not defined

```

<br />

temp_func 함수 내부에서 선언된 a변수는 함수 내부에서만 참조가 가능하며, 외부에서 참조시 에러가 발생한다.

하지만 함수를 제외한 영역에서 var로 선언된 변수는 전역변수로 취급된다.

<br />

```

if(true){
  var a = 10;
  
  console.log(a); // 10
}

console.log(a) // 10

```

<br />

### `호이스팅이란?`

호이스팅을 설명하기 전에 아래의 코드를 한번 보자.

```

var n = 1;
function test() {
  console.log(n);
  var n = 2;
  console.log(n);
}
test();

```

<br />

위 코드를 실행한다면 콘솔 로그는 다음과 같은 결과가 나온다.

```
undefined
2
```

<br />

이런 예상치 못한 결과가 출력되는 이유의 원인은 var 키워드 사용시, 변수 호이스팅이 발생하였기 때문이다.

호이스팅이란 var 키워드를 사용하여 변수를 선언할 경우, 해당 변수가 속한 범위(scopre)의 최상단으로 올라가버리는 현상을 말한다.

그리고 포인트는 여기서 속한 범위(scopre)는 block 레벨이 아닌 function 레벨이라는 점이다.

function 레벨로 변수 호이스팅이 발생하면 위 코드는 다음과 같이 해석되어진다.

```

var n = 1;
function test() {
  var n; // hosting
  console.log(n);
  n = 2;
  console.log(n);
}
test();

```

첫번째 console.log(n)이 실행될 시점에는 n에 어떠한 값도 할당되지 않았기 때문에 undefined가 출력된것이다.

### `var 키워드의 문제점은?`

1. 예측하기가 어렵다

var를 사용할 경우, 전반적으로 코드가 어떻게 작동될지 직관적으로 예측하기 어려운 경우가 자주 발생한다.

<br />

```

console.log(my_number)

```

<br />

위 코드는 변수 my_number가 선언된적이 없기 때문에 Reference Error를 일으킨다.

<br />

```

console.log(my_number);

var my_number;

```

<br />

하지만 이 코드는 undefined를 출력한다. 변수 my_number의 선언이 호이스팅되기 때문이다.

<br />

2. for 문에서 var를 사용할때 이슈

<br />

```

var my_number = 0;

for(var i=0; i<10; i++) {
    my_number += i;
}

console.log("number : ", my_number);
console.log("i : ", i);

```

<br />

```
number : 45
i : 10
```

위 코드에서 변수 i의 값은 반복문이 끝나도 유지가 된다. 위에 설명한대로

var로 선언한 변수는 if 또는 for와 같은 block 레벨이 아닌 function 레벨에서 스코프가 정해지기 때문이다.

즉 for문 안에서 var로 선언한 변수도 block 레벨 스코프를 벗어나서 유효하게 된다.

<br />

3. for 문에서 var를 사용할 때 이슈2

<br />

```

const find_user = ( id, call_back) => {
    setTimeout(()=>{
        var temp_user = {
            id : id,
            name : "ahn - " + id,
            email : id + "@test.com"
        };
        
        call_back(temp_user);
    }, 1000);
}

```

<br />

위 코드는 사용자 아이디를 받아 임시 사용자를 콜백 함수로 넘기는 비동기 함수이다.

DB 연동처럼 setTimeout 함수를 이용해 1초의 지연을 주었다.

<br />

```
const result_user = (user_id) => {
    for(var i in user_id) {
        find_user(user_id[i], (user)=>{
            console.log("id 조회 ", user_id[i]);
            console.log("유저 조회 ", user);
        });
    }
}
```

<br />

위 코드는 사용자 아이디의 배열을 받아 여러 사용자의 정보를 출력해주는 함수이다.

아래와 같이 인자를 넘겨서 위 함수를 실행을 하면 의도치 않은 결과가 출력된다.

![image](https://user-images.githubusercontent.com/94499416/204429367-e72c7815-1021-45d7-b636-074d4e8e21a2.png)

<br />

왜 사용자 아이디가 배열의 마지막 요소로 고정이 되어버린걸까? 마찬가지로 var로 선언된 변수는 function 스코프를 가진다는 점과

비동기 함수의 non blocking 성질을 생각해보면 이해할 수 있다.

for문에서 각 콜백 함수를 넘길 시점에는 i값이 달랐지만, 콜백 함수가 실행될 시점에는 for 루프가 끝나기 때문에

i가 배열의 마지막 원소의 인덱스로 변경된 이후기 떄문이다.

<br />

정리한다면 var를 사용할 시에는 변수 호이스팅과 함수 스코프를 고려하면서 코딩을 해야한다.

그래야 전반적으로 코드가 어떻게 작동할지 예상하기 어려운 상황이 발생하는것에 대응하기 쉬워지기 떄문이다.

<br />

### `var 키워드의 문제점은?`
