# Global Style & Theme

## keyword

- Reset CSS
- `box-sizing` 속성
- `word-break` 속성
- Theme
- ThemeProvider

## 1. Reset CSS [링크](https://meyerweb.com/eric/tools/css/reset/)

각각의 웹 브라우저마다 디폴트로 제공하는 스타일을 초기화할 수 있다. (예를 들어, li의 불렛 포인트와 body의 margin)

---

## 2. `box-sizing` 속성

### 박스 모델(box model)

모든 HTML 요소는 박스 모양으로 구성되며, 이것을 박스 모델(box model)이라 부른다.

#### 박스 모델의 구성 요소

1. 컨텐츠 영역 (Content Area)
2. 패딩 (안쪽 여백, Padding)
3. 테두리 (테두리 여백, Border)
4. 마진 (바깥 여백, Margin)

> box-sizing: border-box 속성 사용시 border, padding을 고려해 박스 크기가 결정된다.  
> width: 200px 일 경우, border와 padding이 각각 10px을 차지한다면 컨텐츠 크기는 160px

---

## 3. `word-break` 속성

`word-break` 속성은 텍스트가 컨텐츠 영역 밖으로 오버플로 할 때 줄을 바꿀지 결정한다.

- keep-all: 한중일 텍스트는 단어 단위로 줄바꿈을 적용한다.
- break-all: 문자 단위로 줄바꿈을 적용한다.

---

## 4. Theme

- 디자인 시스템의 규칙을 정의하는데 사용
- 다양한 상황에 대한(ex. dark mode) 활용이 가능하다.
- '의미' 단위로 스타일을 정의한다.

```jsx
const defaultTheme = {
  colors: {
    background: '#FFF',
    text: '#000',
    primary: '#F00',
    secondary: '#00F',
  },
};

export default defaultTheme;
```

---

## 5. ThemeProvider

`<ThemeProvider>` 래퍼 컴포넌트는 Context API를 통해 아래에 있는 모든 React 컴포넌트에 테마를 제공한다.
