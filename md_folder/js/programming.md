## 프로그래밍

### `프로그래밍이란 뭐라고 생각하나요?`

프로그래밍이란 컴퓨터에게 실행을 요구하는 일종의 커뮤니케이션이다.

0과 1밖에 알지 못하는 기계가 실행할 수 있는 정도로 정확하고 상세하게 요구사항을 설명하는 작업이며

그 결과물이 바로 코드이다. 모호하고 대략적인 요구사항을 전달해도 사람의 머리 속에 있는 의도를 정확히 파악해 

완벽하게 이해하는 컴퓨터는 절대 존재할 수 없다. 문제 해결 방안을 고려할 때 우리는 컴퓨터의 입장에서 문제를 바라보아야 한다.

이때 필요한 것이 컴퓨터 사고력이다.

요구사항의 명령을 수행할 주체는 컴퓨터이기 때문에 인간이 이해할 수 있는 자연어가 아닌 컴퓨터가 이해할 수 있는 언어,

기계어로 명령을 전달해야 한다. 허나 인간이 기계어를 이해하여 직접 기계어로 명령을 전달하는 것은 매우 어려운 작업인데

기계어는 우리가 사용하는 언어와는 너무나도 다른 체계를 가지며 비트 단위로 기술되어 있기 때문이다.

직접 기계어로 명령을 전달하는 대신 인간이 이해할 수 있는 약속된 구문(문법)으로 구성된 프로그래밍 언어를 사용하여

프로그램을 작성한 후, 그것을 컴퓨터가 이해할 수 있는 기계어로 변환하여 주는 일종의 번역기를 이용하는 것이 유용한 대안인데

이 일종의 번역기를 컴파일러(Compilter) 혹은 인터프리터(interpreter)라고 한다.

### `컴파일러란?`

컴파일러는 명령어 번역 프로그램이다.

사람이 작성한 코드를 기계어로 옮겨주는 역할을 한다.

C, C++, C#, JAVA는 사람이 이해하기 쉬운 형태의 언어이다. 즉 컴퓨터는 이해하지 못한다는 것이다.

여기서 컴파일러는 사람이 작성한 코드를 일정한 규칙을 가지고 컴퓨터가 이해할 수 있도록 바꿔준다.

### `인터프리터란?`

컴파일러를 거쳐 기계어로 변환되지 않고 사람이 작성한 프로그램을 한 줄 단위로 받아들여 번역하고, 번역함과 동시에

프로그램을 한 줄 단위로 즉시 실행시키는 프로그램이다.

번역 속도는 빠르지만 프로그램 실행 시 매번 번역해야 하는 특징이 있어 실행 속도는 느리다.

### `컴파일러와 인터프리터의 차이점`

|제목|컴파일러|인터프리터|
|------|---|---|
|번역단위|전체|줄|
|목적 프로그램|생성함|생성하지 않음|
|실행속도|빠름|느림|
|번역속도| 빠름|느림|
