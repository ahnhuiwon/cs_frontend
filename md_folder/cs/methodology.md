## `개발 방법론`

### `폭포수(Waterfall) 방법론이란?`

쉽게 이해할 수 있도록 아래 그림을 먼저 살펴보자.

<br />

![waterfall](https://user-images.githubusercontent.com/94499416/183872478-14c2d80c-8b88-4f52-9b61-2949c150191f.png)

<br />

폭포수(Waterfull) 방법론은 그림에서 알 수 있듯이 소프트웨어 개발 단계를 위에서부터

아래로 폭포에서 물이 떨어지듯이 순차적으로 진행된다.

폭포수 방법론은 한단계씩 진행됨에 따라 다시 이전 단계로 가지 않고 계속 진행하기에

다음 단계로 가기 전에 완벽하게 요구사항을 반영하여 개발했다는 것을 전제로 한다.

> **요구사항 분석 -> 설계 -> 구현 -> 검증(테스트) -> 유지보수**

#### `장점`

  - 수직적으로 진행되기에 각 과장에 대한 이해가 용이하다.

#### `단점`

  - 수직적으로 진행되기 때문에 개발 도중에 요구사항이 변경되었을 경우
    추가적인 비용과 시간을 소비하게 된다.

### `애자일(Agile) 방법론이란?`

애자일 방법론은 폭포수 방법론과 다르게 소프트웨어 개발 단계를 명확하게 구분하지 않고

각 단계를 반복적으로 수행하면서 진행한다.

이때 요구사항을 추가하거나 제외하면서 소프트웨어를 개발하게 된다.

잦은 요구사항의 변경이나 큰 프로젝트를 맡게 되어 요구사항 분석 및 설계를 완벽하게 하기

어려운 경우, 에자일 방법론은 폭포수 방법론보다 적합한 개발 방법론이 될 수 있습니다.

#### `스크럼(Scrum)`

  스크럼은 프로젝트 관리를 위한 상호, 점진적 개발 방법론이며
  
  에자일 소프트웨어 개발중의 하나이다.
  
  <br />
  
  ![scrum](https://user-images.githubusercontent.com/94499416/183879032-440f69fc-2f2a-4376-b77b-106b79f87156.png)
  
  <br />

  - 제품 백로그(Product Backlog)
    * 개발할 제품에 대한 요구 사항 목록
  
  - 스프린트 백로그(Sprint Backlog)
    * 각각의 스프린트 목표에 도달하기 위해 필요한 작업 목록

  - 스프린트(Sprint)
    * 반복적인 개발 주기

  - 일일 스크럼 회의 (Daily Scrum Meeting)
    * 날마다 진행되는 미팅 (작업 및 오류등을 공유)
  
  <br />
  
  #### `스크럼 진행 방법`
  
  > 1. 제품에서 요구하는 기능과 우선순위를 제품 백로그로 정한다.
  > 2. 책임자가 정한 제품의 우선 순위에서 어디까지 작업할지 팀과 조율한다.
  >    조율하여 선정된 백로그가 이번 스프린트의 목표가 된다.
  > 3. 팀에서 스프린트 백로그를 작성한 뒤 작업을 할당한다.
  > 4. 스프린트를 진행하는 동안 모든 개발 팀원이 참여하는 일일 스크럼 회의를 가진다.
  > 5. 매회 스프린트가 종료할 때마다, 스프린트 리뷰 미팅을 통해 만들어진 제품을 학습하고 이해한다.
  > 6. 제품의 학습과 이해가 끝나면, 회고를 통해 팀의 개발 프로세스에 대한 개선 시간을 갖는다.
  > 7. 스프린트 기간 중 다음 스프린트를 준비하기 위해 책임자와 필요 인원이 모여 백로그를 준비하는 시간을 갖는다.

  #### `장점`

    - 개발 도중 요구사항이 변경되었을 경우, 해당 요구 사항을 반영하기 용이하다.
    - 개발하면서 지속적으로 테스트 되기에 개발 초기에 버그를 발견할 수 있다.

  #### `단점`
    - 폭포수 방법론에 비해 체계화된 문서가 적을 수 있다.