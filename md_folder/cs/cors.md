## CORS

### `SOP(Same Origin Policy)란?`

CORS를 공부하기 전에 SOP란 녀석이 나와서 여러분들은 의아할거다.

하지만 SOP를 알아야 CORS를 이해할 수 있다.

SOP는 다른 출처의 자원 사용을 제한하는 보안 방식이다.

http://localhost:3000를 예시로 들자면
  > http : 프로토콜,
  > localhost.com : 호스트,
  > 3000 : 포트,

그럼 SOP는 동일한 프로토콜과 호스트, 포트의 리소스만 허용한다는 건데 아래의 가상 시나리오를 들어보겠다.

 <br />

```
1. 사용자가 웹 사이트에 로그인(토큰 발급)을한다.
2. 해커가 클라이언트에게 'http://hacker.com'이라는 URL을 보낸다.
3. 사용자는 해커가 보낸 링크를 클릭함.
4. 해커가 보낸 페이지는 클라이언트의 토큰을 이용하여 개인정보를 탈취하는 스크립트가 포함되어 있다.
```

<br />

웹 사이트 서버는 토큰만으로 사용자를 판단한다면, 사용자와 해커의 요청을 구분하기 힘들 것이다.

반면 요청 URL을 확인한다면 사용자의 출처는 `http://www.naver.com/~ `이고

해커의 출처는 `http://hacker.com`일테니 서로 다른 출처를 확인하여 악의적인 요청을 방지할 수 있다.

HTTP의 일종으로 사용자가 웹 사이트를 방문할 경우,

그 사이트가 사용하고 있는 서버에서 사용자의 컴퓨터에 저장하는 KEY-VALUE값으로 구성된 작은 기록 정보 파일이다.

HTTP에서 클라이언트의 상태 정보를 사용자의 PC에 저장하였다가 필요할 때 정보를 참조하거나 재사용할 수 있다.

위와 같은 상황, 즉 요청의 출처가 다르다면 `Cross Origin SOP`에 위반이라고 한다.

하지만 매번 요청과 리소스를 동일한 출처로 받을 수는 없는데 이 때 필요한 것이 `CORS`이다.

### `CORS (Cross Origin Resource Sharing)`

CORS는 다른 출처의 자원을 공유하는 것이다.

CORS 접근 제어에 사용되는 3가지의 시나리오가 있다.

  - 단순 요청 (Simple Request)
  - 사전 요청 (Preflight Request)
  - 인증 요청 (Credentialed Request)

#### `단순 요청(Simple Request)`

Preflight 요청없이 바로 요청을 보낸다.

Simple Request는 아래와 같은 조건을 만족해야한다.

  - 메서드 : GET, POST, HEAD
  - Content-type은 아래 셋중 하나여야 한다.
    * application/x-www-form-urlencoded
    * multipart/form-data
    * text/plain
  - 헤더 : Accept, Accept-Language, Content-Language, Content-Type 만 허용 한다.

### `세션이란?` 🔥

방문자가 웹 서버에 접속해 있는 상태를 하나의 단위로 보고

그 상태를 유지시키는 기술을 세션이라 한다.>

### `세션의 특징`

1. 웹 서버에 상태를 유지하기 위한 정보를 저장한다.

2. 웹 서버의 저장되는 쿠키인 세션 쿠키도 있다.

3. 브라우저를 닫거나, 서버에서 세션을 삭제했을 떄만 삭제되므로, 쿠키보다 비교적 보안이 좋다.

4. 서버 용량이 허용하는 한에서 저장 데이터에 제한이 없다.

5. 각 사용자마다 고유한 Session ID를 부여한다.

### `세션의 동작방식`

![session_run](https://user-images.githubusercontent.com/94499416/182762543-ab58d9e8-efaa-4fc5-852d-4a040fd067f2.png)

### `쿠키와 세션의 차이`

|제목|내용|설명|
|------|---|---|
||쿠키(cookie)|세션(session)|
|저장위치|클라이언트 PC|웹 서버|
|저장형식|TEXT|OBJECT|
|만료 시점|쿠키 저장시 설정|브라우저 종료시 삭제|
|사용하는 자원|클라이언트|웹 서버|
|용량 제한|총 300개|서버가 허용하는 한 용량제한 없음|
|속도|세션보다 빠름|쿠키보다 느림|
|보안|세션보다 좋지 않음|쿠키보다 좋음|
