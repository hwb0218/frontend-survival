# React Component

React로 UI를 설계하는 5가지 원칙에 대해 지속적으로 훈련하고 복잡한 UI를 설계하기 위한 단순한 컴포넌트로 분리하는 과정에 대해 이해하자.

## Thinking in React (React로 사고하기)

**`Step 1: Break the UI into a component hierarchy`**

UI를 컴포넌트 계층 구조(하이라키)로 나누기

**`Step 2: Build a static version in React`**

React로 정적인 UI 만들기

<br />

---

### Keyword

- REST API 와 GraphQL
  - REST API 란 무엇인가
  - GraphQL은 왜 등장했는가?
  - REST API vs GraphQL
- JSON
- DSL(Domain-Specific Language)
- 선언형 프로그래밍
- 명령형 프로그래밍
- SRP(단일 책임 원칙)
- Atomic Design
- React component 와 props

<br />

---

### 데이터

백엔드에서 JSON 데이터를 응답하는 API를 제공한다고 가정

#### REST API

> 웹 서비스에서 브라우저와 서버간에 데이터를 주고 받기 위한 통신 아키텍처로 URI에 리소스를 명시하고, HTTP Request Method를 통해 자원에 대한 CRUD 작업을 정의한다.

- 리소스 중심
- GET, POST, PUT/PATCH, DELETE (CRUD 작업)

**`GraphQL`**

- REST API의 단점을 보완하기 위해 등장
- REST API 단점 - Over fetching & Under fetching  
  - Over fetching  
    필요한 데이터 보다 많은 데이터를 가져온 경우
  - Under fetching  
    필요한 데이터 보다 적은 데이터를 가져온 경우
- GraphQL은 단일 엔드포인트를 사용하고, 정보를 특정할 수 있기 때문에 하나의 요청만으로 필요한 데이터를 받을 수 있다.
- Query에 필요한 데이터를 작성한다.
- Query (Read), Mutation(Create, Update, Delete), Subscription(Event)

**`REST API vs GraphQL`**

GraphQL을 사용해보지 않아서 기술에 대한 장단점의 비교는 확실히 할 수 없지만, REST API는 자원 중심적으로 명시와 행위로 표현하므로 직관적인 이해가 가능한 장점과 Over/Under fetching의 단점이 존재하니 네트워크 비용과 페이지 초기 렌더링 속도를 끌어올리고 싶다면 GraphQL을 사용해 원하는 정보만 특정해 오버헤드를 줄일 수 있겠다는 생각이 든다. 추가적으로 단일 엔드포인트를 사용하는데 필요한 데이터를 쿼리로 요청하면 오히려 데이터 사이즈가 더 커지지 않을까?  

#### JSON (JavaScript Object Notation)

> Javascript 객체 문법을 따르는 문자열 데이터 포멧으로 key-value 쌍으로 이루어져 있으며 클라이언트와 서버간의 통신을 주고받을 때 사용한다.

프론트엔드는 위와 같은 형태의 데이터를 사용자가 볼 수 있도록 UI를 구성한다. React는 선언형 UI, 즉 XML과 유사한 문법을 사용해 HTML 문서처럼 작성할 수 있다.

#### DSL (Domain Specific Language)

> 특정 도메인이나 문제 영역을 해결하기 위해 특화된 언어를 말한다. SQL은 데이터베이스와 상호 작용하기 위한 쿼리 언어로 DSL의 예시다. GraphQL도 웹 서비스에서 데이터 통신을 위한 DSL이다. HTML과 CSS는 웹 페이지의 구조와 스타일링, 레이아웃을 지정하는 웹이라는 DSL로 볼 수 있다.

<br />

---

### 컴포넌트 계층 구조

React의 강력한 특징!

- 컴포넌트 기반 (React App 구성 요소)
- 자체 상태를 관리하는 캡슐화된 컴포넌트를 만들고, 이를 조합하여 복잡한 UI를 만들 수 있다.

#### 컴포넌트를 분리하는 기준들

1. 단일 책임 원칙 (SRP - Single Responsibility Principle)
2. CSS
3. Design's Layer
4. Information Architecture

**`1. 단일 책임 원칙 (SRP)`**

객체 지향 프로그래밍에서 원칙 중 하나
모든 클래스는 단 하나의 책임만 가지며 그 책임을 캡슐화해야 한다.
React에서 단일 책임 원칙은 모든 컴포넌트는 하나의 책임을 가져야 한다. 하나의 컴포넌트가 외부 API 호출, 이벤트 핸들링, 다수의 상테관리, 장황한 JSX 등으로 사이즈가 너무 커진다면 컴포넌트로 분리

**`2. CSS`**

클래스 선택자를 통해 어떠한 용도로 만들지 생각하고 컴포넌트 분리

**`3. Design's Layer`**

디자인 툴로 설계한 Layer(계층)에 따라 컴포넌트 분리

**`4. Information Architecture`**

JSON Schema(데이터 구조)에 따른 컴포넌트 분리  
자연스러운 SRP를 위해 강제되며 실제로 데이터 구조에따라 컴포넌트를 분리하게 됨. 주로 데이터 구조로 인해 강제적으로 컴포넌트를 분리하게 된다.

> 작은 컴포넌트를 조립해 다양한 가짓수의 UI를 생성할 수 있는 전형적인 방법

**`Atomic Design`** [관련 링크](https://fe-developers.kakaoent.com/2022/220505-how-page-part-use-atomic-design-system/)

> 디자인 시스템은 어떤 조직이 디지털 인터페이스를 디자인하고 구축하는 방식을 말한다.  
> Atomic Design은 디자인 시스템 방법론 중 하나로 React에 이를 도입해 웹 애플리케이션 UI를 구성하는 컴포넌트를 구조화하여 개발 생산성과 유지 보수를 용이하게 만들어준다.

- Atom  
  Atom은 컴포넌트를 가장 작은 단위로 분리한 것으로 일반적으로 HTML element 단위로 작성된다. 단독 사용은 어렵고, 이것들을 결합한 molecule, organism 단위로 결합해 유용하게 사용할 수 있다.
- Molecule  
  여러개의 Atom을 조합하여 SRP를 만족하는 하나의 일을 수행하는 단위. Input Atom에 텍스트를 입력하고 Button Atom을 클릭해 form을 전송하는 molecule의 예시가 있다.
  하나의 책임을 가지므로 재사용성과 UI의 일관성, 테스트에 용이하다.
- Organism  
  웹 서비스에서 표현될 수 있는 명확한 레이아웃과 특정 컨텍스트(특정 코드, 영역에 대한 환경정보)를 가진다. 컨텍스트를 가지기 때문에 재사용이 어렵다.
- Template  
  실제 콘텐츠는 없는 컴포넌트를 페이지 레이아웃에 맞게 배치한 와이어 프레임, 스켈레톤 UI
- Page  
  유저가 볼 수 있는 실제 컨텐츠를 담고 있다.
  
> Atom, Molecule, Organism 이 3가지 키워드가 중요하다고 생각한다. 연관된 컨텐츠 레이아웃을 기준으로 컴포넌트를 나누면 해당 컴포넌트는 Organism단위로 분리되는데, 각각 다른 페이지에서 동일한 UI를 사용하거나 한 페이지에서 특정 UI의 배치를 변경하는 등의 수정요청이 들어오면 오히려 새로운 컴포넌트를 만드는게 나은 경우가 많다. 이러한 이유로 본인의 경우 재사용성을 높이고 싶다면 가장 작은 단위 Atoms 컴포넌트를 우선적으로 생성하고, 만약 하나의 기능을 수행하는 컴포넌트가 필요하다면 Molecule로 조합하고 Organism을 최종적으로 생성한다. 결과적으론 Atom + Molecule 혼합된 Organism이 생성된다.

### Extract Function

> SRP를 위한 수단, 복잡한 코드를 함수로 추출하여 분리하고 재사용 가능한 구조로 만든다.  
> 일단 하나의 컴포넌트에서 길게 작성하고 분리할 수 있는 구조가 보이면 분리한다.

<br />

---

### React Component & Props

**`React Component`**

- component는 상태를 통해 동적인 UI를 표현할 수 있고, 이를 조합해 복잡한 UI를 구성 할 수 있다.  

**`Props`**

- React의 Props는 자식 컴포넌트로 데이터를 전달하는 방법으로 컴포넌트 간의 데이터 흐름을 생성한다.  
- TypeScript를 잘 사용하거나 잘못 사용하거나를 결정한다.
- 테스트 코드를 작성하여 재사용성을 평가할 수 있다.

<br />

---

### 선언형 / 명령형 프로그래밍

**`선언형 프로그래밍`**

- **무엇을(What)** 수행해야 하는지 개발자가 원하는 결과를 작성한다.
- 내부적인 구현을 추상화한다.

> 2주차에 선언적 API와 Virtual DOM에 대해 다룬적이 있는데 상기하고자 다시 정리
>
> 명령형으로 일일히 DOM 조작을 하지않고 React에 무엇을 수행해야 하는지 선언적으로 알려주는 방식이다. (마치 해줘!  같은 느낌이랄까)  
>  
> **`선언적 API와 Virtual DOM의 상관 관계`** 
>  
> JSX로 반환된 React element가 Virtual DOM을 생성하며, 상태 변경등으로 리렌더링이 트리거되면 Diffing 알고리즘을 통해 Virtual DOM과 Real DOM을 비교 순회하여 리렌더링 최적화를 수행한다. 개발자가 선언적 API를 통해 상태를 변경했을 뿐 React가 자동으로 변경된 내용을 반영한 UI 업데이트를 수행한다.

**`명령형 프로그래밍`**

- **어떻게(How)** 수행해야 하는지 개발자가 일일히 명시적으로 지정한다.
- 내부적인 구현을 명시적으로 작성한다.
