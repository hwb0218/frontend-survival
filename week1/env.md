# 개발 환경

### Keyword
1. Node.js
2. NPM(Node Package Manager)
    - package.json / package-lock.json
    - node_modules
    - npx
3. ES Modules vs CommonJS

#### 1. Node.js
> 구글이 chrome V8 Javascript 엔진을 개발하여 기존에 브라우저 환경에서만 작동하던 JS코드를 서버 측에서도 실행가능한 환경을 제공한 것이 Node.js      
> 이벤트 기반, 비동기 프로그래밍 모델을 따르며 서버 애플케리케이션 개발에 사용된다.
--- 
#### 2. NPM(Node Package Manager)
> Node.js와 함께 설치되며, 이를 통해 패키지를 설치, 관리 및 공유할 수 있다.

##### package.json / package-lock.json
> Node.js 프로젝트의 루트 경로에 생성되는 의존성 관리를 위한 파일들

1. package.json     
 - 프로젝트 메타데이터 포함 
 - 의존성 정보 관리
   - dependencies - 프로덕션 환경에 필요한 패키지들로 빌드 시 번들에 포함
   - devDependencies - 개발 환경에 필요한 패키지들로 빌드 시 번들에 포함안됨
###### 버전 정보 (x.x.x)
> major - 기존 버전과 호환되지 않게 API가 변경되면 올림      
> minor - 기존 버전과 호환되며 새로운 기능을 추가할 경우 올림       
> patch - 기존 버전과 호환되며 버그 수정시 올림 


2. package-lock.json

##### node_modules
##### npx

---
#### ES Modules vs CommonJS