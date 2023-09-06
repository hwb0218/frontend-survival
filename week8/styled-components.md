# styled-components

## keyword

- styled-componets

## 1. styled-componets

- 대표적인 CSS-in-JS 라이브러리
- CSS 작성을 컴포넌트로 사고할 수 있는 장점
- sc라는 접두사가 붙은 유니크한 class name을 생성함
- React 컴포넌트에서 전달받은 props를 통해 동적으로 스타일 변경 가능
- Tagged templates literals을 사용해 함수 형태로 사용할 수 있다.

### 사용법

```jsx
import React from "react";
import styled from "styled-components";

const StyledButton = styled.button`
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 1rem;
  line-height: 1.5;
  border: 1px solid lightgray;
  color: gray;
  background: white;
`;

function Button({ children }) {
  return <StyledButton>{children}</StyledButton>;
}
```

Tagged templates은 함수로 파싱할 수 있어 아래와 같이 함수 표현식 사용이 가능하다.

```jsx
const StyledButton = styled.button`
  padding: 6px 12px;
  border-radius: 8px;
  font-size: 1rem;
  line-height: 1.5;
  border: 1px solid lightgray;

  color: ${(props) => props.color || "gray"};
  background: ${(props) => props.background || "white"};
`;
```

---

## 추가 키워드

### Tagged templates literals [링크](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)

템플릿 리터럴의 발전된 형태로 태그를 사용하면 템플릿 리터럴을 함수로 사용할 수 있다.
태그 함수의 첫 번째 파라미터는 정적 문자열의 배열을 나머지 파라미터엔 동적 데이터인 표현식을 전달받는다.

```javascript
function myTag(strings, personExp, ageExp) {
  var str0 = strings[0]; // "that "
  var str1 = strings[1]; // " is a "

  // 사실 이 예제의 string에서 표현식이 두 개 삽입되었으므로
  // ${age} 뒤에는 ''인 string이 존재하여
  // 기술적으로 strings 배열의 크기는 3이 됩니다.
  // var str2 = strings[2];

  var ageStr;
  if (ageExp > 99) {
    ageStr = "centenarian";
  } else {
    ageStr = "youngster";
  }

  // 심지어 이 함수내에서도 template literal을 반환할 수 있습니다.
  return str0 + personExp + str1 + ageStr;
}

var output = myTag`that ${person} is a ${age}`;

console.log(output);
// that Mike is a youngster
```

### with Babel

next.js는 SSR(Server Side Rendering) 프레임워크로 서버에서 pre-redering된 HTML 문서를 제공한다.
이를 통해 검색 엔진이 웹 사이트를 분석할 수 있도록 검색 엔진 최적화(SEO)를 제공한다.

초기 서버 사이드 렌더링 후 클라이언트 사이드 렌더링이 발생할 때 styled-components의 class name의 해시값이 서버와 클라이언트 간에 불일치할 수 있어 에러가 발생한다.
이는 `babel-plugin-styled-components`를 사용해 서버와 클라이언트 간에 일관된 class name을 생성해 문제를 해결할 수 있다.

또한, 보다 편리한 디버깅을 위해 컴포넌트 이름을 class name의 해쉬값 접두사로 추가한다.
