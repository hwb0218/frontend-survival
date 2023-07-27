# JSX

### Keyword

1. JSX
2. React Element
3. Virtual DOM
4. 선언적 API

<br />

---

### 1. JSX

JSX는 자바스크립트의 확장된 문법으로 열린 태그 닫힌 태그로 구성된 XML 문법을 따르며 HTML 문서처럼 사용할 수 있다.

#### `Babel 트랜스파일러`

- Babel이 JSX문법을 **`React.createElement(components, props, …children)`** 함수로 트랜스파일링하여 문법적 설탕을 제공한다.

> **`문법적 설탕`**  
> 읽는 사람 또는 사용하는 사람에게 편의를 위해 디자인된 문법으로
> 모든 상황에서 적합하지는 않지만, 작성자의 의도를 파악할 수 있는 상황에 사용시 직관적인 문법으로 가독성을 높인다. ex) 삼항연산자, nullish 병합 연산자 등

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

<br/>

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

<br/>

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

#### 재조정(Reconciliation)

하나의 트리를 가지고 다른 트리로 변환하기 위한 최소한의 연산 수를 구하는 알고리즘은 O(n3)의 시간 복잡도를 갖기 때문에 연산 비용이 너무 높다. React는 두 가지 가정을 기반으로 O(n) 복잡도의 휴리스틱 알고리즘을 구현했다.
여기서 휴리스틱이란 중요하지 않은 부분은 제외하고 중요한 부분만을 고려해서 최적의 값을 찾아내자는 방법이다.

1. 서로 다른 타입의 두 엘리먼트는 서로 다른 트리를 만들어낸다.
2. 개발자가 key prop을 통해, 여러 렌더링 사이(배열의 엘리먼트 렌더링)에서 어떤 자식 엘리먼트가 변경되지 않아야 할지 표시해 줄 수 있다.

##### 비교(Diffing) 알고리즘

Diffing 알고리즘은 Reconciliation 과정에서 이전 상태와 새로운 상태를 비교하여 변경 사항을 찾아내는 알고리즘이다.
두 개의 트리를 비교할 때, 리액트는 DOM Tree의 동일 레벨/계층끼리 **`level-by-level`**로 탐색한다.
해당 아이디어가 휴리스틱 알고리즘의 중요한 부분을 고려하는 것이다!

**`1-1. 엘리먼트의 타입이 다른 경우`**

두 루트 엘리먼트의 타입이 다르면, React는 이전 트리를 버리고 완전히 새로운 트리를 구축한다.

> 루트 엘리먼트라는 것이 트리의 프렉탈 구조적 관점으로 특정 컴포넌트에서의 루트 엘리먼트 또한 적용되는 의미인 것 같다. 그래서 해당 컴포넌트 혹은 엘리먼트의 타입이 다르다면 자식을 순회할 필요없이 해당 노드를 포함한 자식 노드를 새로운 Virtual DOM으로 대체하는 것이다.

**`1-2. 엘리먼트의 타입이 같은 경우`**

React는 두 엘리먼트의 속성을 확인하여, 동일한 속성의 내용은 유지하고 
변경된 속성만 갱신한다.

```jsx
// className 속성만 수정
<div className="before" title="stuff" />
<div className="after" title="stuff" />

// style의 color 속성만 수정 
<div style={{color: 'red', fontWeight: 'bold'}} />
<div style={{color: 'green', fontWeight: 'bold'}} />
```

**`2-1. 자식에 대한 재귀적 처리`**

배열의 맨 끝에 엘리먼트가 삽입되지 않고 만약 3번 인덱스에 엘리먼트가 삽입될 경우엔 뒤쪽에 위치한 엘리먼트를 새로운 엘리먼트로 인식하고 4번 인덱스부터 그 뒤의 모든 엘리먼트를 리렌더링한다. 때문에 React에서는 리스팅 컴포넌트를 렌더할 때 key값을 요구한다. 이 key를 기반으로 엘리먼트의 인덱스가 변경된다해도 **기존과 동일**하다는 것을 확인하고 **그저 위치만 이동한다.**

```jsx
const fruits = [{
  id: "1",
  name: "banana"
}, {
  id: "2",
  name: "apple"
}, {
  id: "3",
  name: "orange"
}];

function ArrayRenderComponents() {
  return (
    <ul>
      {fruits.map((fruit) => (
          <li key={fruit.id}>{fruit.name}</li>
      ))}
    </ul>
  );
}

<ul>
  <li key="1">banana</li>
  <li key="2">apple</li>
  <li key="3">orange</li>
</ul>

```

엘리먼트가 배열에 삽입된다면?

```javascript

<ul>
  <li key="1">banana</li>
  <li key="2">apple</li>
  <li key="4">mango</li>
  <li key="3">orange</li>
</ul>

```

key prop을 통해 React가 기존과 동일한 엘리먼트임을 확인하고 위치만 이동!

<br/>

---

### 4. 선언적 API

개발자가 DOM element를 선택해 addEventLinster로 이벤트를 등록하거나, classList를 add 하거나, 어떠한 부모 노드의 자식 엘리먼트로 추가될 지 직접 DOM 조작과 상태 변화에 대해 명령할 필요없이 선언적으로 React에게 UI를 어떻게 표현해야 하는지를 알려주는 방식이다.

#### 선언적 API와 Virtual DOM이 무슨 상관인가?

선언적으로 UI 구조를 작성하고, 컴포넌트가 반환한 React element 트리가 Virtual DOM이며 상태, 타입이 변경됐을 경우 Real DOM과 비교(diffing) 순회하여 리렌더링 최적화를 수행하기 때문이다.

<br />

---

### 궁금한 키워드

- React Fiber
