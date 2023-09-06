# Style Basics

## Keyword

- className
- 의미있는 마크업

---

## 1. className

스타일을 설정할 때 className을 사용하는 이유는 JSX는 babel에 의해 자바스크립트 코드로 변환되기 때문에 class는 예약어로 인식하여 JSX는 HTML의 class가 아닌 className을 사용한다. 스타일 설정 시 객체를 전달한다.

### 객체의 키, 벨류를 이용한 클래스 문자열 사용하기

```jsx
function classNames(classes) {
  return Object.entries(classes)
    .filter(([key, value]) => value)
    .map(([key, value]) => key)
    .join(' ');
}

const classes = {
  'maybeClass': true,
  'otherClass': true,
  'probablyNotClass': false,
};

const myClassNames = classNames(classes);
// Output: "maybeClass otherClass"

<li className={myClassNames} />
```

> myClassNames 변수에 classes 객체에서 true로 설정된 클래스 이름이 공백으로 구분된 문자열로 저장된다.

---

## 2. 의미있는 마크업 (Semantic Markup)

### 정의

시맨틱 마크업이란 컨텐츠의 의미를 잘 전달하도록 HTML 문서를 작성하는 것을 말한다.

시맨틱 태그는 각각 의미를 지니고 있기 때문에 HTML 문서 구조를 보다 쉽게 이해할 수 있다.

### 시맨틱 마크업의 필요성

- HTML 문서의 가독성 향상과 유지보수에 용이하다.
  - `header, nav, footer`등 시맨틱 태그를 활용하면 다른 작업자가 문서 구조를 파악하기 수월해진다.
- 웹 접근성을 향상시킨다.
  - 시맨틱 마크업은 시각 장애인을 위한 브라우저 컨텐츠를 음성으로 안내해주는 스크린 리더를 통해 활용된다.
- 검색 엔진 최적화(SEO)
  - 시맨틱 마크업은 검색 엔진이 페이지의 컨텐츠를 효과적으로 분석하고 검색 순위를 향상시킬 수 있다.
