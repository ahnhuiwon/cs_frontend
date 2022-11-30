## `타입변환과 단축 평가`

### `명시적 타입 변환이 무엇인가?`

개발자의 의도에 따라 값의 타입을 다른 타입으로 변환할 수 있는데 

이를 명시적 타입 변환 또는 타입 캐스팅이라고 한다.

<br />

### `명시적 타입 변환 함수를 예는?
```
let my_number = 10;

// 명시적 타입 변환
// 숫자를 문자열로 타입 캐스팅한다.
let my_string = my_number.toString();

console.log(typeof my_string, my_string); //  string 10
```
  
<br />

### `암묵적 타입 변환`
개발자의 의도와는 상관없이 표현식을 평가하는 도중에
자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되기도 한다.
이를 암묵적 타입 변환 또는 타입 강제 변환이라고 한다.

<br />

```
let my_number = 10;

// 암묵적 타입 변환
// 문자열 연결 연산자는 숫자 타입 my_number를 기반으로 새로운 문자열 생성
let my_string = my_number + '';

console.log(typeof my_string, my_string); //  string 10
```

<br />

### `truthy / falsy 한 값이란?`

#### `truthy`
자바스크립트에서 truthy인 값(참 같은 값)은 Boolean 문맥에서 true로 평가되는 값이다.
falsy값으로 정의된 값이 아니면 모두 truthy값으로 평가된다.
자바스크립트는 불리언 문맥에서 타입 변환을 사용하는데 truthy값을 true로 변환하기 떄문에
아래의 모든 if 블록을 실행하게 된다.

```
if (true)
if ({})
if ([])
if (42)
if ("0")
if ("false")
if (new Date())
if (-42)
if (12n)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)
```
<br />

#### `falsy`
falsy인 값(거짓 같은 값)은 Boolean 문맥에서 false로 평가되는 값이다.
다음은 자바스크립트에서의 falsy값의 종류를 나타낸 표이다.

```
false	//  키워드 false
0	//  Number zero.(0.0, 0x0 등등 또한 해당된다)
-0	//  Number Negative zero.(-0.0, -0x0 등등 또한 해당된다)
0n	//  BigInt zero. (0x0n 도 포함) BigInt negative zero는 없음에 유의하자(0n의 negative는 0n이다.)
"", '', ``	//  빈 문자열 값
null	//  어떠한 값도 없는 상태
undefined	
NaN	//  Not a Number
document.all	//  ?
```
