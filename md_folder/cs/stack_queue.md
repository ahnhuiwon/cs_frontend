## `스택과 큐`

### 스택이란?

스택(stack)이란 쌓아 올린다는 것을 의미한다.

따라서 스택 자료구조라는 것은 책을 쌓는 것처럼 차곡차곡 쌓아 올린 형태의 자료구조를 말한다.

<br />

### 스택의 특징?

![stack](https://user-images.githubusercontent.com/94499416/211702730-199c84df-5167-4d1a-8cdf-4f5bed1705b1.png)

<br />

스택은 위 사진처럼 같은 구조와 크기의 자료를 정해진 방향으로만 쌓을 수 있고

**top으로 정한 곳을 통해서만 접근**할 수 있다.

> top은 가장 위에 있는 자료, 즉 가장 최근에 들어온 자료를 가르킨다.

삽입되는 새 자료는 top이 가리키는 자료의 위에 쌓이게 되며

스택에서 자료를 삭제할때 top을 통해서만 가능하다.

스택에서 top을 통해 **삽입하는 연산**을 'push', **top을 통한 삭제**는 'pop'이라고 한다.

따라서 스택은 시간 순서에 따라 자료가 쌓여서 **가장 마지막에 삽입된 자료가 가장 먼저 삭제**되는

구조적 특징을 가지게 된다.

이러한 스택의 구조를 **후입선출(LIFO, Last-In-First-Out) 구조**라고한다.

그리고 비어있는 스택에서 원소를 추출할려고 할 때 stack underflow라고 하며,

스택이 넘치는 경우 stack overflow라고 한다.

<br />



### 큐란?

큐(Queue)의 사전적 의미는

무엇을 기다리는 사람, 자동차 등의 줄 또는 서서 기다리는 것을 의미한다.

따라서 놀이동산에서 줄을 서서 기다리는것과 은행에서 먼저 온 사람의 업무를 창구에서 처리하는 것과 같이

선입선출(FIFO, First In First Out) 방식의 자료구조를 말한다.

<br />

### 큐의 특징?

![queue](https://user-images.githubusercontent.com/94499416/211702726-c835f9ca-4c6b-48e0-985a-a6043068215b.png)

<br />

정해진 한 곳(top)을 통해 삽입, 삭제가 이루어지는 스택과는 달리

큐는 한쪽 끝에서 삽입 작업이, 다른 쪽 끝에서 삭제 작업이 양쪽으로 이루어진다.

이때 삭제연산만 수행되는 곳을 프론트(front), 삽입 연산만 이루어지는 곳을 리어(rear)로 정하여

각각의 연산작업만 수행된다. 이때 큐의 리어에서 이루어지는 삽입 연산을 인큐(enQueue),

프론트에서 이루어지는 삭제 연산을 디큐(deQueue)라고 부른다.

- 큐의 가장 첫 원소를 front / 가장 끝 원소를 rear
- 큐는 들어올 때 rear로 들어오지만 front부터 빠지는 특성
- 접근 방법은 가장 첫원소와 끝 원소로만 가능
- 가장 먼저 들어온 프론트 원소가 가장 먼저 삭제

<br />

즉 큐에서 프론트 원소는 가장 먼저 큐에 들어왔던 첫번째 원소가 되며,

리어 원소는 가장 늦게 큐에 들어온 마지막 원소가 되는 것이다.
