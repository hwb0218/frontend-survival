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
- Confusing Classes -> 클래스의 메서드, 라이프사이클 메서드, 상태 관리 등이 섞여 혼란 야기 (ex. this 바인딩)

**`React Hooks의 도입`**

- Functional Component만 사용 -> 함수형 컴포넌트는 코드를 간결하게 작성하고 가독성을 높인다.
- 상태 관리 유무를 바로 알기 어려움 -> React가 내부적으로 최적화를 수행하므로 신경쓰지 않아도 된다.
- 복잡한 요소는 전부 Hook으로 격리 및 재사용 가능. -> custom hook으로 로직 재사용

---

### 2. Hooks

#### 2.1 useState

> useState -> state를 사용한다.  
> 함수형 컴포넌트에서 상태를 관리하기 위한 Hook, useState() 함수의 인자로 상태 초기값을 설정하며 배열을 반환한다.
> 첫번째 요소는 상태값, 두번째 요소는 상태 업데이트 함수

#### 2.2 useEffect

> useEffect -> Side-effect를 다룬다.  
> Side-effect는 React 컴포넌트의 렌더링과 직접적인 연관이 없는 네트워크 요청과 같은 외부 시스템 동기화 같은 작업들을 의미한다.
> 클래스 컴포넌트의 라이프사이클 메서드와 유사한 역할의 Hook, useEffect() 함수의 첫번째 인자는 함수며, 두번째 인자는 배열로 의존성 배열이라 부른다. 의존성 배열의 값들이 변경되면 첫번째 함수가 호출된다.
> 첫번째 함수는 함수를 반환하는데 이를 cleanup이라 부르며 컴포넌트가 업데이트 또는 언마운트될 때 이 함수가 실행된다.

```jsx
useEffect(() => {
  // 부수 효과를 처리하는 코드

  // cleanup 함수
  return () => {
    // cleanup 코드
  };
}, []);
```

> 만약 의존성 배열을 생략하면 매 렌더링마다 Side-effect 함수와 cleanup 함수가 실행된다.  
> 함수가 계속 호춛돼 무한루프로 인한 overflow가 발생할 수 있으므로 주의해야 한다.


#### 2.3  useContext

#### 2.4 useRef

#### 2.5 useLayoutEffect

---

### 3. React StrictMode?

---

### 추가 키워드

- HoC & Wrapper Hell
