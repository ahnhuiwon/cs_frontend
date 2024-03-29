## `캐시(Cache)`

### `캐시(Cache)란?`

  > 자주 사용하는 데이터 또는 값을 미리 복사해 놓는 임시 장소. 

  아래와 같은 저장공간 계층 구조에서 확인할 수 있듯이, 캐시는 저장 공간이 작고
  
  비용이 비싼 대신 빠른 성능을 제공한다.

<br />

![cache1](https://user-images.githubusercontent.com/94499416/184054499-71e46004-d8fb-4053-a3c3-6205396926c7.png)

<br />

### `캐시(Cache)의 등장`

캐시란 나중에 요청할 결과를 미리 저장해둔 후 빠르게 서비스 해주는 것을 의미한다.

즉 미리 결과를 저장하고 나중에 요청이 오면, 그 요청에 대해서 DB, API를 참조하지 않고

캐시를 접근하여 요청을 처리하게 된다. 

이러한 캐시가 동작 할 수 있는 철학에는 파레토 법칙이 있다.

> 파레토 법칙이란 80%의 결과는 20%의 원인으로 인해 발생한다는 말이다.

<br />

![cache2](https://user-images.githubusercontent.com/94499416/184054726-99b4d970-9342-499b-b55a-f441c9194b32.png)

<br />

파레토의 법칙으로 인해 캐시가 효율적일 수 있는 이유는

모든 결과를 캐싱할 필요는 없으며, 사용자는 서비스를 할때 많이 사용되는 20%를 캐싱한다면

전체적으로 영향을 주어 효율을 극대화 할 수 있다는 말이다.

### `어떤 정보를 캐시에 담는가?`

모든 데이터를 캐시에 담기에는 저장 공간은 작다.

그렇기 때문에 파레토의 법칙에 해당하는 소수의 데이터를 선별하는데

이때 사용되는 것이 지역성이다.

<br />

![cache3](https://user-images.githubusercontent.com/94499416/184055216-aa8986ad-fa1f-4891-a1df-22e641a6cf3a.png)

<br />

**시간적 지역성**

특정 데이터가 한번 접근되었을 경우, 가까운 미래에 또 한번 데이터에 접근할 가능성이 높은것을 말한다.

**공간적 지역성**

데이터와가까운주소가순서대로접근되었을 경우를공간적지역성이라고한다.

> CPU 캐시나 디스크 캐시의 경우 한 메모리 주소에 접근할 때
> 그 주소뿐만 아니라 해당 블록을 전부 캐시에 가져오게 된다.
> 이때 메모리 주소를 오름차순, 내림차순으로 접근한다면
> 캐시에 이미 저장된 같은 블록의 데이터를 접근하게 되므로 캐시의 효율성이 크게 향상된다.

**순차 지역성**

공간 지역성과 함께 설명되기도 한다. 데이터가 순차적으로 엑세스 되는 경향을 보인다.

<br />

### `캐시의 사용 구조`

![cache5](https://user-images.githubusercontent.com/94499416/184055659-e304d275-cd5a-4c3f-935e-8523cdefb03e.png)

<br />

1. 사용자로부터 요청을 받는다.
2. 캐시와 작업르한다.
3. 실제 DB와 작업한다.
4. 다시 캐시와 작업한다.

> 캐시는 일반적으로 위의 이미지와 같은 플로우로 사용된다.
> 동일한 프로우에서 어떻게 사용하냐에 따라서 아래와 같이 나뉜다.

  - look aside cache (Lazy Loading)
  1. 캐시에 데이터 존재 확인
  2. 데이터가 있다면 캐시의 데이터 사용
  3. 데이터가 없다면 캐시의 실제 DB 데이터 사용
  4. DB에서 가져온 데이터를 캐시에 저장 
  <br />
    
    > look aside cache는 캐시를 한번 접근해 데이터가 있는지 판단한 후 있다면 캐시의 데이터를 사용하며
    > 데이터가 없다면 실제 DB 또는 API를 호출하는 로직으로 구현된다.

  - write back
  1. 데이터를 캐시에 저장
  2. 캐시에 있는 데이터를 일정 기간동안 체크한다.
  3. 모여있는 데이터를 DB에 저장
  4. 캐시에 있는 데이터 삭제  
  <br />
    
    > write back은 캐시를 다르게 이용하는 방법이다.
    > DB는 접근 횟수가 적을수록 시스템의 퍼포먼스는 좋아지는데
    > 데이터를 캐시에 모으고 일정한 주기 또는 크기가 되면 한번에 처리하는 방법이다.

<br />

### `캐시를 많이 쓸 수 없는 이유?`

위에서 살펴 보았듯이 컴퓨터를 구성하는 메모리 저장공간은 속도가 빠를 수록 용량이 작고 가격이 높다.

그래서 가격 떄문에 캐시에 저장할 적은 양의 정보를 잘 선택하는 것이 비용도 절약하고 효율도 높이는 방법이다.
