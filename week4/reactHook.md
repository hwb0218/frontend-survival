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

> Context API와 함께 사용되는 Hook으로 컴포넌트에 전역 상태를 공유할 수 있다. 이를 통해 컴포넌트간의 데이터 전달 과정, 즉 Props driling을 해결할 수 있다.

```jsx
import React, { useContext } from 'react';

const UserContext = React.createContext();

function App() {
  return (
    <UserContext.Provider value="John">
      <UserProfile />
    </UserContext.Provider>
  );
}

function UserProfile() {
  const user = useContext(UserContext);

  return <p>Welcome, {user}!</p>;
}
```

> Context 객체를 생성하고 Provider에 전역 상태를 공유할 하위 컴포넌트를 선언하면
> 각 하위 컴포넌트에서 useContext hook을 사용해 Context 값을 사용할 수 있다.

#### 2.4 useRef

> ref -> reference(참조) 참조를 관리하는 Hook  
> 값(current)이 바뀌어도 리렌더링을 트리거하지 않으며, 컴포넌트 렌더링과 관련없이 값을 유지한다.
> useRef() 함수는 DOM에 직접 접근하거나 컴포넌트 내부에서 데이터를 보존할 수 있다.
> 일반적인 사용법으로 input에 focus를 줄 수 있다.

```jsx
function Component() {
  const inputRef = useRef(null); 

  const focusInput = () => {
    // input 요소에 포커스를 준다.
    inputRef.current.focus(); 
  };

  return (
    <div>
      <input ref={inputRef} type="text" />
      <button onClick={focusInput}>Focus Input</button>
    </div>
  );
}
```

#### 2.5 useLayoutEffect

> useLayoutEffect는 컴포넌트 렌더링 전, 레이아웃과 페인트 과정이 일어나기 직전에 실행된다.
> 라우저 렌더링 전에 실행되기 때문에 무거운 작업을 수행한다면 성능에 영향을 미칠 것 이다.
> 실무에서 거의? 사용하지 않았던 hook

---

### 3. React StrictMode?

> React 애플리케이션 내에서 발생할 수 있는 잠재적인 문제를 감지하고 경고 메시지를 표시하는 래퍼 컴포넌트  
> 개발 환경에서만 활성화되며, 프로덕션에서는 무시된다.
> 만약, Effect 내부에서 console.log() 함수를 사용하고 컴포넌트 마운트시 브라우저 콘솔창에 로그가 두 번 찍힌다면 StrictMode를 사용하고 있을 확률이 높다.

- 중복된 Props 감지, 레거시 라이프사이클 메서드 사용, 부작용을 유발하는 렌더링에 대한 경고

---

### 추가 키워드

- HoC

**`HOC`**

> Higher Order Component = 고차 컴포넌트  
> 컴포넌트를 감싸는 컴포넌트로 특정 로직을 재활용하기 위한 패턴으로, 인자로 컴포넌트를 받고 새로운 컴포넌트를 생성한다.
> 유저 권한에 따른 페이지 접근을 제한하는 라우팅 처리로 HOC 패턴을 사용한 경험이 있다.

사용 예시

```jsx
import { useEffect } from 'react';

const withLogger = WrappedComponent => props => {
  useEffect(() => {
  console.log(WrappedComponent.name);
  }, []);

  return <WrappedComponent {...props} />;
}
```
