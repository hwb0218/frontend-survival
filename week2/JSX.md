# JSX

### Keyword

1. JSX
2. React Element
3. Virtual DOM
4. 선언적 API
5. 재조정(Reconciliation)

### 1. JSX

JSX는 자바스크립트의 확장된 문법으로 열린 태그 닫힌 태그로 구성된 XML 문법을 따르며 HTML 문서처럼 사용할 수 있다.

#### `Babel 트랜스파일러`

- Babel이 JSX문법을 **`React.createElement(components, props, …children)`** 함수로 트랜스파일링하여 문법적 설탕을 제공한다.
- React는 해당 함수를 사용해 React element 트리를 갱신한다.
- JSX로 할 수 있는 모든 것은 Vanilla JS로도 가능하다.

**`코드 예시`**

```jsx
<div className="test">
  <p>Hello, world!</p>
  <Button type="submit">Send</Button>
<div>

// 변환 결과
React.createElement(
  "div",
  { className: "test" },
  React.createElement("p", null, "Hello, world!"),
  React.createElement(Button, { type: "submit" }, "Send")
);
```

위의 코드에서 만약 div 엘리먼트를 제거한다면?

```jsx
  // 에러 발생
  <p>Hello, world!</p>
  <Button type="submit">Send</Button>
```

인접한 JSX element는 둘러싸는 태그로 묶어야 한다는 에러메시지가 발생한다.
마치 문장을 세미콜론(;)을 사용하지 않고 한 줄에 연속적으로 입력했을 경우와 같은 셈이다.
ex) add(1, 2) add(3, 4) => Missing semicolon error  

---

### 2. React Element

React에서 UI를 구성하는 최소 단위 React Element, 일반적으로 JSX로 표현된다.
JSX 문법은 선언적 API를 제공해 유지보수 가능하고 개발 생산성을 증가시키지만, 공식문서는 React에서 JSX는 필수가 아니라고 설명한다.

#### `왜 필수가 아닌가?`

위의 JSX에서 설명한 것 처럼 Babel, swc와 같은 툴이 JSX 문법을 React.createElement 함수로 변환하는 것일 뿐이다.
(document.createElement 함수가 동작하는 것 처럼!)

#### `React automatic runtime`

React 17부터 automatic runtime이 도입되었는데, 더 이상 **`import React from 'react';`** 구문을 입력하지 않아도 된다. 이전에는 JSX가 React.createElement() 함수로 컴파일 되었기 때문에 해당 import 구문이 scope안에 있어야 했기 때문이다.

**`classic runtime`**

```jsx
import React from 'react';

function App() {
  return <h1>Hello World</h1>;
}

import React from 'react';

function App() {
  return React.createElement('h1', null, 'Hello world');
}
```

**`automatic runtime`**

```jsx
function App() {
  return <h1>Hello World</h1>;
}

import {jsx as _jsx} from 'react/jsx-runtime';

function App() {
  return _jsx('h1', { children: 'Hello world' });
}
```

코드 변환 시 **`import {jsx as _jsx} from 'react/jsx-runtime';`** import 구문이 추가된다.

---

### 3. Virtual DOM

Virtual DOM은 리액트가 DOM을 추상화, 가상적으로 표현해 메모리에 저장하고, ReactDOM과 같은 라이브러리에 의해 Real DOM과 동기화하는 프로그래밍 개념이다.

혹자: VDOM을 사용하는 것은 빠르기 때문이다! (X)

리액트팀 개발자 Dan Abramov의 답변:
현실은 유지보수 가능한 애플리케이션을 만들 수 있으며, 대부분의 사례에선 충분히 빠르다.

**`maiatainable`**

Vanilla JS로 DOM element를 직접 셀렉트해 가공하는 것이 과연 유지보수에 용이할까?

React는 선언적 API를 통해 개발자가 원하는 UI를 직접 명령형 프로그래밍 하는 것이 아닌, 원하는 상태를 선언적으로 프로그래밍해 React가 자동으로 UI를 업데이트할 수 있다. 그러므로 유지보수에 용이하다.

**`Fast enough`**

**`재조정(Reconciliation)`** 을 통해 대부분의 경우엔 충분히 빠르다.

### 4. 선언적 API

### 5. 재조정(Reconciliation)

### 키워드 추가 정리

- React Fiber
