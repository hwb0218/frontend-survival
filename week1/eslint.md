# Parcel & ESLint

1. Bundler(번들러)
   - 1-1 Parcel
2. Lint(린트)
   - 2-1 ESLint

### 1. Bundler(번들러)
> 웹 애플리케이션을 구성하는 여러 개의 모듈이나 파일(JavaScript, CSS, HTML, Images 등)을 하나의 파일로 묶어주는 도구
- 웹 에플리케이션을 구성하는 리소스에 대한 번들링을 지원
- 코드 스플리팅을 통한 초기 페이지 로드 속도 개선(초기 로드시에 필요한 코드만 로드하고, 여러 개의 파일(chunk)로 나누어 필요한 시점에 로드함) ex. Dynamic import & lazy loading
- 변수의 유효 범위 문제를 해결함(모듈 시스템의 내장)
#### 1-1 Parcel
> Zero Configuration를 강조하는 번들링 도구로 별도의 설정없이 즉시 개발에 집중할 수 있다.
- 내부적으로 SWC를 사용해 빠른 컴파일링을 제공한다.

##### **`편의를 위해 추가하기`**
```json
"source": "./index.html",
```

---
<br />

### 2. Lint(린트)

#### 2-1 ESLint