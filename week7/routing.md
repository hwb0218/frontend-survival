# Routing

## Keyword

- HTML DOM API
  - Location
  - pathname

## 1. HTML DOM API [링크](https://developer.mozilla.org/ko/docs/Web/API/Location)

HTML 문서의 요소에 접근하고 제어하는데 사용되는 인터페이스로 DOM(Document Object Model)은 HTML 요소를 트리구조로 나타내며, 각 요소는 Javascript를 통해 동적으로 조작할 수 있다.

### 1.1 Location

- 웹 브라우저의 현재 URL과 관련된 정보를 제어하고 조작하는데 사용되는 객체
- 현재 페이지의 프로토콜, 도메인 주소, 페이지 새로고침 및 이동 등의 기능을 제공

### 1.2 pathname

- 현재 URL의 path(경로)의 문자열을 가져온다.

**`ex) '/megaptera_fe/frontend-survival/week6/external-store'`**

## 추가 키워드

### URL Encoding

URL은 아스키 코드의 문자 집합만 사용할 수 있어, 한글과 같은 문자열을 URL에 삽입할 경우 URL Encoding으로 아스키 형태로 변환한다. 이 때 변환하는 규칙은 UTF-8을 따르먀, 한글 문자 1개는 3바이트로 인코딩 된다.
