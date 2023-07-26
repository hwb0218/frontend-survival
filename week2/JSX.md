# JSX

### Keyword

1. JSX
2. React Element
3. Virtual DOM
4. 선언적 API
5. 재조정(Reconciliation)

### 1. JSX

JSX는 자바스크립트의 확장된 문법으로 열린 태그 닫힌 태그로 구성된 XML 문법을 따르며 HTML 문서처럼 사용할 수 있다.

#### `Babel 트랜스파일링`

- Babel이 JSX문법을 **`React.createElement(components, props, …children)`** 함수로 트랜스파일링하여 문법적 설탕을 제공한다.
- React는 해당 함수를 사용해 React element 트리를 갱신한다.
- JSX로 할 수 있는 모든 것은 Vanilla JS로도 가능하다.

##### `코드 예시`

```javascript
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

```javascript
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

### 3. Virtual DOM

### 4. 선언적 API

### 5. 재조정(Reconciliation)

### 키워드 추가 정리

- React Fiber
