# React State

React State에 대해 명확하게 이해하고, 코드 리팩터링 의도를 파악하고 흡수하자.

## Thinking in React (React로 사고하기)

**`Step 3: Find the minimal but complete representation of UI state`**

최소한의 완전한 UI state 찾기

**`Step 4: Identify where your state should live`**

state가 어디에 있어야 할지 파악하기  

**`Step 5: Add inverse data flow`**

역방향 데이터 흐름 추가하기  

<br />

---

### Keyword

- React state란?
- DRY 원칙
- SSOT(Single Source of Truth)
- useState
- 1급 객체(first-class object)란?
- Lifting State Up

<br />

---

### React의 State

- React의 State 컴포넌트 내부에서 사용되는 **동적인 데이터를 나타내는 객체**다.
- State의 변경은 컴포넌트 리렌더링을 트리거한다.
- 리렌더링이 발생하면 해당 컴포넌트를 포함한 하위 컴포넌트도 리렌더링된다.
- 모든 데이터가 State가 되는 것은 아니다.

### DRY 원칙

>Don't Repeat Yourself 원칙은 중복 코드를 피하고 코드를 재사용할 것을 강조하는 소프트웨어 디자인 원칙이다.

- 중복 로직을 함수나 클래스를 활용해 재사용한다.
- React의 경우 컴포넌트를 재사용해 코드 중복을 최소화한다.
- Custom Hooks를 활용해 공통 로직을 분리한다.

### SSOT(Single Source of Truth)

애플리케이션 내부의 모든 상태 정보를 하나의 소스에서 관리하자는 개념

> 즉, 컴포넌트 이곳저곳에서 상태를 무분별하게 사용하지 말고 해당 상태에 의존하는 모든 컴포넌트를 포함하는 상위 컴포넌트가 상태를 관리하자는 의미, 또는 전역 상태 관리 라이브러리를 통해 외부 Store에서 관리

### useState

React Hooks중 하나로 함수형 컴포넌트에서 상태를 관리하는 데 사용되는 함수

```jsx
const [state, setState] = useState(initialState);
```

- useState 함수는 배열을 반환하고 첫번째 요소는 현재 상태 값, 두번째는 상태 업데이트 함수
- initialState는 상태 초기값이며, 첫 렌더링 시에만 사용된다.
- setState 함수를 호출해 상태를 변경하면, 변경된 상태를 반영하기 위해 컴포넌트가 리렌더된다.

### 1급 객체(first-class object)

Javascript에서의 일급 객체는 다음과 같은 특징을 가진 객체다.

1. 함수를 변수의 값으로 할당할 수 있다. (ex. 함수 표현식)
2. 함수를 함수의 매개변수로 전달할 수 있다. (ex. 콜백 함수)
3. 함수를 함수의 반환 값으로 사용이 가능하다. (ex. 클로저)

일급 객체의 특징으로 인해 콜백 함수 패턴과 고차 함수 등의 다양한 기능을 통해 프로그래밍이 가능하다.

### Lifting State Up

### Inverse Data Flow
