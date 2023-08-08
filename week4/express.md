# Express

## keyword

- Express란?
- REST API
- HTTP Method(CRUD)
- URL 구조

### Express란?

> Express는 웹 앱을 위한 강력한 기능을 제공하는 간결하고 유연한 Node.js 웹 앱 프레임워크다.

- 라우팅: HTTP 요청과 요청 처리 로직을 연결하는 라우팅 기능 제공 (ex. app.get(), app.post(), app.patch(), app.delete())
- 미들웨어: 요청과 응답 사이의 중간에서 로깅, 데이터 변환, 인증 등의 작업을 처리할 수 있다. (ex. app.use())

### REST API

> REST API는 클라이언트와 서버간에 데이터를 주고 받기위한 통신 아키텍처로 리소스를 식별하기 위해 URI에 명시하고, HTTP Method를 통해 자원에 대한 CRUD 작업을 정의한다.

**`로이 필딩의 REST API 아키텍처 4단계 레벨`**

1. 레벨 0: Swamp of POX (Plain Old XML)
   - REST API 원칙을 따르지않는 단계
   - 데이터는 XML 포멧으로 전송되며, 리소스를 식별하기 위한 URI 패턴이 없음
2. 레벨 1: Resources
   - URI에 리소스를 명시함
   - 아직 자원에 대한 행위인 CRUD 작업을 정의하지 않음
3. 레벨 2: HTTP Verbs
   - HTTP 메서드(GET, POST, PUT/PATCH, DELETE)를 통해 CRUD 작업을 명시함
4. 레벨 3: Hypermedia Controls
   - 하이퍼미디어 컨트롤은 클라이언트가 링크를 따라가며 API와 상호 작용하고, API 변화에 유연하게 대응할 수 있다.

> 대게는 레벨 1의 URI 리소스 명시와 레벨 2의 HTTP Verbs를 도입하는 수준으로 사용한다.

### HTTP Method(CRUD)

> 해당 자원에 대한 작업 및 처리(CRUD)는 HTTP Method를 이용한다.

#### URL 구조

> 자원 식별을 명사로 표현하고, 해당 자원에 대한 작업 및 처리(CRUD)는 HTTP Method를 이용한다.
> 조회 작업의 경우 Collection(복수), item(단수)로 나뉜다.

**`기본 리소스 URL: /products`**

- Read (목록 조회 = Collection) -> GET /products  
- Read (특정 데이터 조회 = Item) -> GET /products/{product_id}  
- Create (상품 생성 및 추가, Collection Pattern 활용) -> POST /products  
- Update (Item) -> PUT /products/{product_id}  
- Delete (Item) -> DELETE /products/{product_id}  

**Collection Pattern**을 활용하면 동일명의 엔드포인트로 자원에 대한 행위(CRUD)를 정의하므로 일관적인 API를 작성할 수 있다.

**`PUT / PATCH`**  

PUT은 존재하지 않는 데이터에 대해선 새로 생성하고, 존재한다면 해당 레코드 전체를 Overwirte한다.
PATCH는 레코드의 일부 데이터만 변경하는 Method이다.
