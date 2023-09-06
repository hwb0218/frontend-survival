# props와 attrs

## Keyword

- props
- attrs

## 1. props

- React 컴포넌트에서 전달받은 props를 통해 동적으로 스타일 변경 가능
- props에 따라 여러개의 스타일 속성을 변경하고 싶을 때 `css` 함수를 이용한다.

```tsx
// Tagged templates은 함수로 파싱할 수 있어 아래와 같이 함수 표현식 사용이 가능하다는 점을 이용한다.
import styled, { css } from 'styled-components';

type ParagraphProps = {
  active?: boolean; 
}

const Paragraph = styled.p<ParagraphProps>`
  color: ${(props) => (props.active ? '#F00' : '#888')};
  ${(props) => props.active && css`
    font-weight: bold;
  `}
`;
```

---

## 2. attrs
