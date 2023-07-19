# 개발 환경

### Keyword
1. Node.js
2. NPM(Node Package Manager)
    - package.json / package-lock.json
    - node_modules
    - npx
3. ES Modules vs CommonJS

### 1. Node.js
> 구글이 chrome V8 Javascript 엔진을 개발하여 기존에 브라우저 환경에서만 작동하던 JS코드를 서버 측에서도 실행가능한 환경을 제공한 것이 Node.js      
> 이벤트 기반, 비동기 프로그래밍 모델을 따르며 서버 애플케리케이션 개발에 사용된다.
--- 
### 2. NPM(Node Package Manager)
> Node.js와 함께 설치되며, 이를 통해 패키지를 설치, 관리 및 공유할 수 있다.

#### package.json / package-lock.json
> Node.js 프로젝트의 루트 경로에 생성되는 의존성 관리를 위한 파일들

**`1. package.json`**
- 프로젝트 메타데이터 포함 
- 의존성 정보 관리
  - dependencies - 프로덕션 환경에 필요한 패키지들로 빌드 시 번들에 포함
  - devDependencies - 개발 환경에 필요한 패키지들로 빌드 시 번들에 포함안됨
- 스크립트 정의
  - 사용자 정의 스크립트를 실행해 빌드, 실행, 테스트등의 작업을 자동화한다.
##### 버전 정보 (x.x.x)
> major - 기존 버전과 호환되지 않게 API가 변경되면 올림      
> minor - 기존 버전과 호환되며 새로운 기능을 추가할 경우 올림       
> patch - 기존 버전과 호환되며 버그 수정시 올림 

**`2. package-lock.json`**
  - 의존성 트리를 고정시켜 다른 환경에서 프로젝트를 설치하거나 협업 시 상호간에 동일한 버전의 패키지를 설치할 수 있다. 

#### node_modules
> npm 패키지 매니저로 설치한 패키지들이 저장되는 디렉토리     
> Github에 올라가지 않도록 .gitignore에 node_modules 디렉토리 지정
#### npx
> npx는 Node.js를 설치하면 npm과 마찬가지로 함께 설치된다.
> 로컬에 패키지가 없을 경우 npx를 사용하면 패키지는 전역 환경에 **영구적 다운로드**가 아닌 **일시적으로 다운로드(캐싱)** 되는 것 이다.       
> 이후 패키지를 실행한 뒤 캐싱된 패키지를 **삭제**한다.
---
#### ES Modules vs CommonJS
**`1. ESM`**
- JS 표준 묘둘 시스템
- **import**/**export**문을 사용
- ESM Module Loader는 **Top-level-await**를 지원하기 때문에 비동기적으로 작동
- 정적인 구조로 정적 분석이 가능 (모듈 의존 관계를 런타임 이전에 분석함) 
- 정적 분석을 통해 사용하지 않는 코드를 제거하는 **Tree-shaking**이 가능해진다.

**`2. CJS`**
- JS 표준 모듈 시스템이 아님
- **require**/**module.exports**문을 사용
- CJS Module Loader는 동기적으로 작동
- 모듈을 동적으로 로딩하거나 조건부 로딩이 가능 (정적 분석이 어려워 런타임에 모듈 의존 관계 파악)
  ```javascript
  // 동적 로딩
  const utilName = /* 동적인 값 */
  const util = require(`./utils/${utilName}`)

  // 조건부
  function f() {
    if (동적인 조건) {
      module.exports = /* ... */
    }
  }
  ```

---
### 추가 정리
- Yarn
- Top-level-await [(관련 링크)](https://fe-developers.kakaoent.com/2022/220728-es2022/)
  > Top-level-await를 사용하면 모듈이 하나의 거대한 async함수 처럼 동작하게 되어 최상위 레벨에서도 비동기 처리가 가능하다.      
  **IIAFE**로 promise객체를 반환하는 방법도 있지만 보다 높은 가독성을 제공한다.     
  이를 통해 비동기 처리 결과값을 반환하는 모듈을 다른 모듈에서 import해 처리가 정상적으로 완료된 결과값을 보장받을 수 있다.
- Tree-shaking