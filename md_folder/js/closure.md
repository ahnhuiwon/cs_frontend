## 클로저

### 클로저란?

MDN의 정의는 아래와 같다.

<br />

> 클로저는 함수와 그 함수가 선언됐을 때의 렉시컬 환경(Lexical environment)과의 조합이다.

<br />

문장이 굉장히 어렵다. 코드를 통해 자세히 보기 전에 쉽게 풀어서 얘기를 한다면

**클로저는 반환되는 내부함수는 자신이 선언됐을 때의 환경을 기억해 다른 환경에서 호출되어도 내부 함수가 선언되었던 환경에 접근할 수 있는 함수**

를 말한다.  

<br />

아래 코드를 살펴보자.

이해하기 쉽게 설명과 맞추기 위해서 함수를 한글로 작성했지만 왠만해서는 한글은 지양하자.

<br />

```
function 외부함수() {

	const x = 10;
    const 내부함수 = function () { console.log(x) }
    
    내부함수();
}

외부함수(); // 10
```

<br />

외부함수 안에서 내부함수가 선언되고 호출되었다.

이때 내부함수는 자신을 포함하고 있는 외부함수의 변수 x에 접근할 수 있는데

이는 내부함수가 외부함수 내부에 선언되었기 때문이다.

<br />

이번에는 내부함수를 외부함수 안에서 호출하는것이 아니라 반환하도록 변경해보자.

<br />

```
function 외부함수() {

	const x = 10;
    const 내부함수 = function () { console.log(x) }
    
    return 내부함수;
}

const 내부 = 외부함수(); 
내부(); // 10
```

<br />

외부함수는 내부함수를 반환하고 생을 마감했다. 

즉 외부함수는 실행된 이후 콜스택에서 제거되었으므로 외부함수의 변수 x 또한 유효하지 않게 되어 변수 x에 접근할 수 있는 방법이 달리 없어 보인다.

하지만 위 코드의 실행 결과는 변수 x의 값인 10이다.

이미 라이프 싸이클이 종료되어 콜스택에서 제거된 외부함수의 지역 변수인 x가 다시 부활이라도 한듯이 동작하고 있다.

이처럼 자신을 포함하고 있는 외부함수보다 내부함수가 더 오래 유지되는 경우, 외부함수 밖에서 내부함수가 호출되더라도 외부함수의 

지역 변수에 접근할 수 있는데 이러한 함수를 **클로저**라고 한다.

<br />

### 클로저를 사용하면 뭐가 좋죠?

<br />

#### 상태 유지

<br />

클로저가 가장 유용하게 사용되는 상황은 현재 상태를 기억하고 변경된 최신 상태를 유지한다는 것이다.

아래 코드를 살펴보자.

<br />


```
<!DOCTYPE html>
<html>
<body>
  <button class="toggle">버튼</button>
  <div class="box" style="width: 100px; height: 100px; background: green;"></div>

  <script>
    const box = document.querySelector('.box');
    const toggleBtn = document.querySelector('.toggle');
    
	class View {
    	constructor() {
        	let view = false;
            
            
            this.changeView = function() {
        		box.style.display = view ? 'block' : 'none';
            	view = !view;
        	};
        }
    }
    
    const display = new View();

	toggleBtn.addEventListener("click", () => {
        display.changeView();
    });
  </script>
</body>
</html>
```

위 코드는 class 문법을 사용해 closure 상황을 구현한 코드이다.

1. View 클래스는 생성자로 정의되어, 생성자 내부에서 로컬 변수인 view가 선언되고 false로 초기화된다. 

>이 변수는 클로저 내에 캡슐화된다.

2. changeView 메소드는 생성자 내에서 함수로 정의된다. 이 함수는 클로저로 인해 view 변수에 액세스 할 수 있고 호출되면 view 변수의 현재 값에 따라 block과 none 사이에서 box 요소의 표시 속성을 토글한다.
또한 view 값을 반대 상태로 뒤집는다.

3. View 클래스의 인스턴스는 display 변수를 사용하여 생성된다.

4. toggleBtn 버튼에 addEventListener 메소드를 사용해 이벤트 리스너를 추가한다.
버튼을 클릭하면 display 인스턴스의 changeView 메서드가 호출되어 box 요소의 가시성이 토글된다.

<br />

위 코드에서 클로저는 생성자 내에서 정의된 changeView 메서드가 생성자가 실행을 마친 후에도 view 변수에 액세스 할 수 있기 때문에 작동되며, <br />메소드가 view 변수에 클로저를 형성하여 해당 값을 유지하고 chageView 메소드가 호출될 때마다 액세스 할 수 있도록 하기 때문에 가능하다.

<br />

#### 전역 변수의 사용 억제 및 정보의 은닉화

<br />

```
<!DOCTYPE html>
<html>
<body>
  <p>Counting using a class</p>
  <button id="increase">+</button>
  <p id="count">0</p>
  <script>
    class Counter {
      constructor() {
        this.counter = 0;
      }

      increase() {
        return ++this.counter;
      }
    }

    const increaseBtn = document.getElementById('increase');
    const count = document.getElementById('count');
    const counter = new Counter();

    increaseBtn.addEventListener("click", () => {
        count.innerHTML = counter.increase();
    });
  </script>
</body>
</html>
```

<br />

전역변수가 있다면 잘 동작할 수 있지만 오류를 발생시킬 가능성이 있는 좋지 않은 코드이다. 

전역변수는 언제든지 누구나 접근이 가능하고 변경할 수 있다. 이는 의도치 않게 값이 변경될 수 있다는 것을 의미한다.

위와 같이 클로저를 사용한다면 카운터 클래스 내에서 카운트 상태와 동작을 캡슐화하여 코드를 보다 체계적이고 모듈식으로 만들 수 있다.

<br />

### 클로저를 어떻게 생성하나요?

<br />

#### 일반 함수에서의 클로저 구현


```
function createClosure() {
  let count = 0;

  function increment() {
    count++;
    console.log(count);
  }

  return increment;
}

const closure = createClosure();

closure(); // 1
closure(); // 2
```

<br />

1. createClosure 함수는 increment라는 내부 함수를 반환한다.

2. increment 함수는 클로저로 인해 외부 createClosure 함수에 정의된 count 변수에 액세스할 수 있다.

3. losure()가 호출될 때마다 count 변수를 증가시키고 업데이트된 값을 기록한다.

<br />

#### 클래스 구문에서의 클로저 구현

<br />

```
class Counter {
  constructor() {
    let count = 0;

    this.increment = function() {
      count++;
      console.log(count);
    };
  }
}

const counter = new Counter();

counter.increment(); // 1
counter.increment(); // 2
```

<br />

1. Counter 클래스에는 생성자 내에서 선언된 전용 변수 count가 있다.

2. 'increment' 메서드는 클래스 내 함수로 정의되며 클로저로 인해 'count' 변수에 액세스할 수 있다.

3. counter.increment()가 호출될 때마다 count 변수를 증가시키고 업데이트된 값을 기록한다.
