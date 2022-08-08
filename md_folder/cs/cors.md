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

#### `사전 요청(Preflight Request)?` 🔥

사전 요청은 OPTIONS 메소드를 통해 다른 도메인 리소스에 요청이 가능한지 확인하는 작업이다.

요청이 가능한 것을 확인하면 실제 요청을 보낸다.

##### `Preflight Request`

  - Origin : 요청 출처
  - Access-Control-Request-Method : 실제 요청의 메서드
  - Access-Control-Request-Headers : 실제 요청의 추가 헤더

##### `Preflight Response`

  - Access-Control-Allow-Origin : 허가 출처
  - Access-Control-Allow-Methods : 허가 메서드
  - Access-Control-Allow-Headers : 허가 헤더
  - Access-Control-Max-Age : Preflight 응답 캐시 시간

여기서 **Preflight Response**의 응답 코드는 200대여야하고 Body는 비어있는 것이 좋다.

#### `인증 요청 (Credentialed Request)`

인증 관련 헤더를 포함할 때 사용하는 요청이다.

클라이언트
 > 쿠키 또는 JWT 토큰을 담아 보낼 경우 credentials : include 를 포함하여 보낸다.

서버 
 > Access-Control-Allow-Credentials : true 해야 클라이언트의 인증 포함 요청에 허용이 가능하다.

### `CORS 해결 방법`

해결 방법에는 세 가지가 있다.

  - 프론트 프록시 서버 설정
    * 프론트 서버에서 백엔드 서버로 요청을 보낼 때, 대상의 URL을 변경한다.
  - 직접 헤더 설정
    * 직접 헤더에 설정을 추가한다.
  - 스프링부트 설정
    * 설정 클래스를 만들고 WebMvcConfigurer을 구현하면 addCorsMappings란 메서드를 사용하여 CORS의 출처 및 설정 관리를 할 수 있다.
