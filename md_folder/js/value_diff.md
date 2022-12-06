## `원시 값과 객체 비교`

### `동적 타이핑을 지원하는 자바스크립트에서 데이터의 타입을 크게 2개로 나누는 이유?`

자바스크립트가 제공하는 7가지 데이터 타입은 크게 원시 타입과 객체 타입으로 구분할 수 있다.

원시 값은 변경 불가능한 값이며 반면 객체는 변경 가능한 값이다.

원시 값을 변수에 할당시 변수(확보된 메모리 공간)에는 실제 값이 저장된다.

객체는 변수에 할당하면 변수(확보된 메모리 공간)에는 참조 값이 저장된다.
  
<br />

#### `값에 의한 전달?`

```
let my_number = 80;
let my_copy = my_number;

console.log(my_number); // 80
console.log(my_copy); //80

my_number = 100;

console.log(my_number); // 100
console.log(my_copy); // 80
```

<br />

변수에 변수를 할당시 무엇이 어떻게 전달될까? `my_copy = my_number`에서 my_number는 변수 값 80으로

평가되어 my_copy에도 80이 할당될 것이다. 이 때 새로운 숫자 값 80이 생성되어 my_copy 변수에 할당된다.

이처럼 변수에 원시 값을 갖는 변수를 할당하면 할당 받는 변수 my_copy에는 할당되는 변수 my_number의 원시 값이 복사되어 전달된다.

이를 값에 의한 전달이라고 한다.

위 코드의 경우 my_copy 변수에 원시 값을 갖는 my_number 변수를 할당하면 할당 받는 변수(my_copy)에는 

할당되는 변수 my_score의 원시 값 80이 복사되어 전달된다.

<br />

```
let my_number = 80;

// copy 변수에는 score 변수의 값 80이 복사되어 할당
let my_copy = my_number;

console.log(my_number, my_copy); // 80 80
console.log(my_number === my_copy); // true
```

<br />

위 코드를 보면 my_number 변수와 my_copy 변수는 숫자 값 80을 갖는다는 점에서 동일하다.

하지만 my_number 변수와 my_copy 변수의 값 80은 다른 메모리 공간에 저장된 별개의 값이다.

엄격하게 말하면 변수에는 값이 전달되는 것이 아닌 메모리 주소가 전달되기 때문이다. 변수와 같은 식별자는 값이 아닌

메모리 주소를 기억하고 있다.

중요한것은 결국 두 변수의 원시 값은 서로 다른 메모리 공간에 저장된 별개의 값이 되어

어느 한쪽에서 재할당을 통해 값을 변경하더라도 서로 간섭할 수 없다는 점이다.

<br />

### `참조에 의한 전달?`

```
let my_person = {
  name : 'ahn'
}

// 참조 값을 복사 (얕은 복사)
let my_copy = my_person;
```

<br />

객체를 가리키는 변수를 다른 변수에 할당하면 우너본의 참조 값이 복사되어 전달되는데 이를 참조에 의한 전달이라고 한다.

원본 my_person과 사본 my_copy는 저장된 메모리 주소는 다르지만 동일한 참조 값을 갖는다. 이는 두개의 식별자가 하나의 객체를 공유한다는 것을 의미하는데

원본 또는 사본 중 어느 한쪽에서 객체를 변경한다면 서로 영향을 주고 받는다.

```
let my_person = {
  name : 'ahn'
}

let my_copy = my_person;

console.log(my_copy === my_person); // true;

my_copy.name = 'huiwon';
my_person.age = 28;

console.log(my_person);
console.log(my_copy);
```

<br />

![image](https://user-images.githubusercontent.com/94499416/205834232-ddb519eb-1bf7-4b73-90c4-6869da9a913a.png)

<br />

값에 의한 전달과 참조에 의한 전달은 식별자가 기억하는 메모리 공간에 저장되어 있는 값을 복사해서

전달한다는 면에서 동일하다. 다만 식별자가 기억하는 메모리 공간, 즉 변수에

저장되어 있는 값이 원시 값이냐 참조 값이냐의 차이만 있을 뿐이다.
