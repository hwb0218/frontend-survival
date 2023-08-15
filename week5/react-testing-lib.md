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

#### React Testing Library

React Testing Library는 실제 브라우저 DOM을 기준으로 테스트를 작성하게 된다. React의 컴포넌트의 내부 구현과 변경사항 대해 관심이 없으며, 사용자 브라우저에 렌더되는 UI의 실제 동작을 테스트하는데 초점을 맞춘다.

---

## 2. given - when - then 패턴

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

테스트 실행을 위해 베이스라인으로서 사용되는 객체들의 고정된 상태
테스트 픽스처의 목적은 결과를 반복가능할 수 있도록 알 수 있고, 고정된 환경에서 테스트할 수 있음을 보장하기 위함이다.
