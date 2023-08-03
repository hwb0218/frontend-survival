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

### React의 State

- State의 변경은 React의 리렌더링을 트리거한다.
- 리렌더링이 발생하면 해당 컴포넌트를 포함한 하위 컴포넌트도 리렌더링된다.
- 모든 데이터가 State가 되는 것은 아니다.

### Inverse Data Flow
