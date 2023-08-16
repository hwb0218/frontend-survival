# React Testing Library

## Keyword

1. React Testing Library
2. given - when - then 패턴
3. Mocking
4. Test fixture

---

## 1. React Testing Library

Behavior Driven Test(행위 주도 테스트) 방법론이 떠오르면서 주목받기 시작한 테스팅 라이브러리
기존의 관행이던 Implementation Driven Test(구현 주도 테스트)의 단점을 보완하기 위해 대두돼었다.

### Implementation Driven Test(구현 주도 테스트)

구현 주도 테스트는 애플리케이션이 어떻게 동작하는지에 초점을 둔다.
특정 엘리먼트의 태그가 무엇이며 어트리뷰트로 무엇이 쓰였는지, 어떠한 값이 쓰였는지에 대해 테스트한다.

### Behavior Driven Test(행위 주도 테스트)

사용자의 관점에서 UI와 인터렉션했하여 발생한 이벤트에 따라 화면에 변화가 일어나는지에 초점을 둔다.

### Enzyme vs React Testing Library

#### Enzyme

기존엔 React앱은 Enzyme을 이용해 IDT 방법론에 따라 테스트를 수행했으며, 실제 DOM이 아닌
React Virtual DOM을 기준으로 작성해야 한다. 예를 들면, 컴포넌트가 관리하고 있는 State, 전달되는 Props가 무엇인지에 대해 검증이 용이하다.

#### React-Testing-Library

React Testing Library는 실제 브라우저 DOM을 기준으로 테스트를 작성하게 된다. React의 컴포넌트의 내부 구현과 변경사항 대해 관심이 없으며, 사용자 브라우저에 렌더되는 UI의 실제 동작을 테스트하는데 초점을 맞춘다.

**`render, screen, fireEvent`**

- render

`render()` 함수는 React-Testing-Library에서 제공하는 모든 쿼리 함수와 기타 유틸리티 함수를 담고 있는 객체를 리턴한다.

```typescript
import { render } from "@testing-library/react";


const { container, getByText, getByRole } = render(<Component />);
```

- screen

`screen` 객체는 랜더링된 컴포넌트의 DOM 요소를 선택하는데 사용된다.

```typescript
import { screen } from "@testing-library/react";

render((
  <TextField
    label="Name"
    placeholder="Input your name"
    text={text}
    setText={setText}
  />
));

screen.getByLabelText('Name');
```

- fireEvent

`fireEvent` 객체는 컴포넌트 내에서 발생할 수 있는 이벤트를 가상으로 트리거할 수 있다.

```typescript
import { render, screen, fireEvent } from '@testing-library/react';

render(<Component />);
const buttonElement = screen.getByRole('button');
fireEvent.click(buttonElement);
```

---

## 2. given - when - then 패턴

테스트 코드 작성에 사용되는 패턴중 하나로 테스트 시나리오를 구조화하고 가독성을 높일 수 있다.

Given(주어진 상황): 테스트를 하기위해 기본적으로 세팅하는 초기 조건, 초기값

When(동작): 테스트를 하기위한 동작을 설정

then(결과): 동작의 기대 결과가 나왔는지 검증

```typescript
function add(a: number, b: number) {
    return a + b;
}

function subtract(a: number, b: number) {
    return a - b;
}
```

```typescript
const context = describe;

describe('계산기', () => {
    context('add 함수를 호출한다면', () => {
        it('두 수를 더한 값을 반환한다', () => {
            // Given - 초기 상태, 값
            const num1 = 5;
            const num2 = 3;

            // When - 동작 설정
            const result = add(num1, num2);

            // Then - 기대 결과 검증
            expect(result).toBe(8);
        });
    });

    context('subtract 함수를 호출한다면', () => {
        it('두 수를 뺀 값을 반환한다', () => {
            // Given - 초기 상태, 값
            const num1 = 10;
            const num2 = 4;

            // When - 동작 설정
            const result = subtract(num1, num2);

            // Then - 기대 결과 검증
            expect(result).toBe(6);
        });
    });
});

```

---

## 3. Mocking

Mocking은 외부 의존성(API 호출, DB 접근)을 가짜로 구현하여 외부 리소스에 의존하지 않고 테스트를 수행할 수 있다.

### 사용하는 이유?

1. 의존성 격리 - 네트워크 통신, DB 접근으로 부터 격리하여 의존성 변화의 영향을 받지 않아 독립적으로 실행될 수 있다.
2. 테스트 일관성 유지 - 외부 리소스는 변화할 수 있으므로 모킹을 통해 테스트의 일관성을 보장받을 수 있다.
3. 테스트 속도 향상 - API 호출, DB 상호작용으로 인한 시간을 소모하지 않으므로, 빠른 테스트가 가능하다.

### jest.mock()

jest.mock() 함수는 모듈을 모킹할 때 사용한다. 테스트 대상이 의존하는 모듈을 Mocking하여 원하는 동작을 수행하거나 가짜 데이터를 제공한다.

```typescript
// math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// 첫번째 인자는 모킹할 모듈, 두번째 인자는 모듈의 함수를 개별적으로 모킹하고 동작을 지정할 수 있음.
jest.mock('./math', () => ({
  ...math,
  subtract: jest.fn(),
}));
```

### jest.fn()

jest.fn() 함수는 가짜 함수를 생성할 때 사용한다. 함수 호출 여부, 반환 값, 호출 횟수등을 확인할 수 있다.

```typescript
// 빈 가짜 함수
const mockFn = jest.fn();
mockFn(); // 함수 호출시 undefined를 반환

// 인자로 함수를 전달하면, 특정 동작을 수행하는 가짜 함수를 생성한다.
const mockFn = jest.fn((a, b) => a + b);
```

---

## 4. Test fixture

테스트 코드에서 사용되는 초기값, 상태, 객체등을 제공하는 역할을 한다. 테스트를 작성할 때 반복적으로 사용되는 데이터를 테스트 코드에서
분리하여 관리하는 것

**`fixture`**

```typescript
// fixture/products.ts
const products = [
  {
    category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
  },
];

export default products;

// fixture/index.ts
import products from "./products";

export default {
  products,
};
```

**`app.test.tsx`**

```typescript
import { render, screen } from '@testing-library/react';

import App from './App';

import fixtures from '../fixture';

jest.mock('./hooks/useFetchProducts', () => () => fixtures.products);

test('App', () => {
  render(<App />);

  screen.getByText('Apple');
});
```

**`__mocks__`**

Mocking한 custom hooks를 모아놓은 폴더

```typescript
// __mocks__/useFetchProducts.ts
const useFetchProducts = jest.fn(); // Mocking custom hooks 

export default useFetchProducts;
```
