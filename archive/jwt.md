# JWT(JSON WEB TOKEN)

HTTP는 2가지 특징이 존재한다. 무상태성(Stateless), 비연결성(Connectionless)

**`무상태성(Stateless)`**

HTTP는 상태 정보를 저장하지 않는다. 이말은 즉, 누구의 요청인지 구분을 할 수 없다는 의미다.
따라서 요청 정보를 특정하기 위해서 Cookie, Session, Token 인증을 통해 클라이언트를 파악할 수 있다.

**`비연결성(Connectionless)`**

클라이언트와 서버간의 요청과 응답이 끝난뒤 연결을 끊어버리는 성질이다. HTTP는 인터넷 상에서 불특정 다수의 통신환경을 기반으로 설계되었기 때문에, 서버가 다수의 클라이언트와 연결을 계속 유지해야 한다면, 많은 리소스 점유등의 오버헤드가 발생한다.

HTTP의 이러한 특징으로 인해 아래의 방법으로 클라이언트 인증을 수행할 수 있다.

## Cookie, Session, Token

서버가 클라이언트 인증을 확인하는 방식으로 Cookie, Session, Token 방식이 있다.

## 쿠키(Cookie)

- 만료기간이 있는 key-value 형태의 저장소

![네이버 요청 헤더](../images/%EC%9A%94%EC%B2%AD%ED%97%A4%EB%8D%94.png)

![쿠키 인증 방식](../images/%EC%BF%A0%ED%82%A4.png)

### 쿠키의 단점

- 보안에 취약하다. 민감한 정보를 쿠키에 저장할 경우 그대로 노출
- 4kb의 용량제한
- 브라우저 마다 쿠키 지원 형태가 달라 브라우저간 공유가 불가능

## 세션(Session)

- 민감한 정보를 브라우저가 아닌 `서버에서 저장하고 관리함`

### 세선 객체

- 세션 객체는 Session ID를 key로 갖는 key-value로 구성
- value에 세선 생성 시간, 마지막 접근 시간, 기타 정보들이 Map형태로 저장됨

![세션 객체](../images/%EC%84%B8%EC%85%98%ED%8F%AC%EB%A9%A7.png)

## 토큰(Token)

---

## 참조

[JWT 토큰 인증 이란? (쿠키 vs 세션 vs 토큰)](https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-JWTjson-web-token-%EB%9E%80-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC)