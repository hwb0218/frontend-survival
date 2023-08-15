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

---

## 4. Test fixture
