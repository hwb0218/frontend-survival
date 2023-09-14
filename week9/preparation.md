# 개발하기 전 준비

## 개발 환경 세팅

[개발 환경 세팅하기 가이드](https://github.com/megaptera-kr/textbook/tree/main/start-megaptera-shop-client)

## Test Helper

테스트할 때 styled-components의 Theme, React Router의 Link 등을 사용해 render 할 때 문제가 발생하므로 테스트 헬퍼 함수를 사용

```tsx
// eslint-disable-next-line import/no-extraneous-dependencies
import { render as originalRender } from '@testing-library/react';

import { ReactNode } from 'react';

import { MemoryRouter as Router } from 'react-router';

import { ThemeProvider } from 'styled-components';

import defaultTheme from './styles/defaultTheme';

type Option = {
  path?: string;
}

export default function render(
  node: ReactNode,
  { path = '/' }: Option = {},
) {
  return originalRender((
    <Router initialEntries={[path]}>
      <ThemeProvider theme={defaultTheme}>
        {node}
      </ThemeProvider>
    </Router>
  ));
}
```
