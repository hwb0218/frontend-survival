# Testing Library

### Keyword
1. Jest
2. Describe-Context-It 패턴
3. React Testing Library

#### 1. Jest
> JavaScript Testing Framework      
> JS 애플리케이션 테스트를 수행해 코드 안정성과 품질을 유지하고 버그를 줄일 수 있다.      
- **expect**로 테스트 할 대상을 지정하고 **matcher**로 예상 결과와 실제 결과를 비교할 수 있다.
- callback, promise, async/await 비동기 코드 테스트를 수행할 수 있다.
- 모듈, 함수나 객체등을 mocking하여 대체할 수 있다. 

```javascript
// sum.js
function sum(a, b) {
  return a + b;
}

module.exports = sum;

// sum.test.js
describe('sum 함수', () => {
  it('두 수를 더한다.', () => {
    const res ult = sum(2, 3);
    expect(result).toBe(5);
  });

  it('음수를 더한다.', () => {
    const result = sum(-2, -3);
    expect(result).toBe(-5);
  });
});
```
Jest는 보통 (describe, it) 쌍으로 작성
- describe - 테스트 그룹화
- it - 개별 테스트 수행

##### **`SWC(Super-fast Web Compiler)`**
> Jest는 JS파일 테스트만 지원하므로, SWC를 사용해 TS를 JS로 변환해준다. 
- Javascript와 Typescript 코드 컴파일러
- JS의 ES6+ 문법을 ES5문법으로 트랜스파일링
- TS -> JS 컴파일링
---
#### 2. Describe-Context-It 패턴
> 테스트 스크립트를 구성하는데 도움이 되는 테스트 코드 구성 패턴
- Describe - 설명할 테스트 대상을 명시한다. 
- Context  - 테스트 대상이 놓인 상황을 설명한다.
- It - 테스트 대상의 행동을 설명한다.

##### **`한국어로 테스트 설명 작성 `** [(참조 링크)](https://johngrib.github.io/wiki/junit5-nested/#kotlin-describe-spec)

- Describe - 테스트 대상을 명사로 작성한다.
- Context는 - ~인 경우, ~할 때, 만약 ~ 하다면 과 같이 상황 또는 조건을 기술한다.
- it - 명사로 작성한 테스트 대상의 행동을 작성한다
  - 테스트 대상의 행동은 ~이다, ~한다, ~를 갖는다가 적절한다.
  - ~된다 같은 수동형 표현은 좋지 않다.
---
#### 3. React Testing Library
> React 컴포넌트를 테스트하기 위해 사용되는 라이브러리    
> 주로 Jest와 함께 사용한다.
- E2E Test와 같이 사용자 시나리오에 따라 컴포넌트의 동작을 테스트 (사용자 중심적 테스트)
- 다만 리액트 컴포넌트 테스트만 하는 상황은 지양하자
  - 너무 많은 테스트 코드로 인해 유지보수를 위한 테스트가 오히려 역효과를 가져올 수 있다.
---

### 키워드 추가 정리
- TDD
- BDD
- E2E (End To End)