# React Hook

## keyword

- React Hook 이란
- Hooks
  - useState
  - useEffect
  - useContext
  - useRef
  - useLayoutEffect
- React StrictMode 란

### 1. React Hook?

> React Hooks는 버전 16.8에 도입된 API로 클래스 컴포넌트만 가능했던 상태관리가 함수형 컴포넌트에서도 가능하며, 코드를 보다 간결하게 작성하고 재사용하기 쉽게 만들어주는 패러다임을 제공한다.

**`기존 방식의 문제점`**

- Wrapper Hell (HoC) -> 고차 컴포넌트의 중첩으로 발생하는 코드의 복잡성
- Huge Components -> 크기가 큰 복잡한 기능을 가진 컴포넌트
- Confusing Classes -> 클래스의 메서드, 라이프사이클 메서드, 상태 관리 등이 섞여 혼란 야기

**`React Hooks의 도입`**

- Functional Component만 사용 -> 함수형 컴포넌트는 코드 가독성을 높인다.
- 상태 관리 유무를 바로 알기 어려움 -> React가 내부적으로 최적화를 수행하므로 신경쓰지 않아도 된다.
- 복잡한 요소는 전부 Hook으로 격리 및 재사용 가능. -> custom hook으로 로직 재사용

---

### 2. Hooks

#### 2.1 useState

#### 2.2 useEffect

#### 2.3  useContext

#### 2.4 useRef

#### 2.5 useLayoutEffect

---

### 3. React StrictMode?

---

### 추가 키워드

- HoC & Wrapper Hell
