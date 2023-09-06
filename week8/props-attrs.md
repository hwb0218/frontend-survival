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

- 컴포넌트에 기본 속성을 추가할 때 사용한다.
- 불필요하게 반복되는 속성을 처리할 때 유용 (button을 만들 때 적극 채용)

<!-- type ButtonProps = React.ButtonHTMLAttributes<HTMLButtonElement> & { type?: 'submit' } -->
```tsx
import styled, { css } from 'styled-components';

type ButtonProps = {
  type?: 'button' | 'submit' | 'reset';
  active?: boolean;
}

const Button = styled.button.attrs<ButtonProps>((props) => ({
  type: props.type ?? 'button',
}))<ButtonProps>`
  border: 1px solid #888;
  background: transparent;
  cursor: pointer;
`
```
