# 웹 최적화

프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1 정리

## 1. Lighthouse

웹 서비스의 성능 측정과 품질 향상 가이드라인을 제공해주는 크롬 개발자 도구

- 추천항목: 리소스의 관점에서 가이드를 제공(로딩 성능 최적화)
- 진단항목: 페이지의 실행 관점에서 가이드를 제공(렌더링 성능 최적화)

---

## 2. 이미지 사이즈 최적화

- 이미지 CDN을 사용한다(사용자에게 이미지를 전송하기 전 사이즈를 가공하거나 이메지 포멧 변경을 제공)
- 이미지를 업로드할 때 사이즈를 미리 가공한다.

> CDN?  
> 서버의 물리적 거리의 한계를 극복하기 위해 사용자와 가까운 곳에 컨텐츠 서버를 두는 기술

---

## 3. 병목 코드 최적화

- 병목 현상을 발생시키는 코드를 Performance탭에서 분석 후 최적화한다.

> 병목 현상  
> 하나의 구성 요소로 인한 전체 시스템 성능이 제한받는 현상

![Performance](../images/%ED%8D%BC%ED%8F%AC%EB%A8%BC%EC%8A%A4.png)

위의 그림은 articles url로 네트워크 요청을 시도했는데, 병목 코드로 API 콜백 실행에 지연이 발생하고 있다.

![Performance](../images/%ED%8D%BC%ED%8F%AC%EB%A8%BC%EC%8A%A41.png)

자세히 보니 API 콜백 실행은 Article 컴포넌트 내부의 removeSpecialCharacter 함수로 인한 병목 현상이 발생해 렌더링 지연이 발생하고 있었다.

### 병목 코드 최적화 수행하기

**`Before`**

```jsx
/*
 * 파라미터로 넘어온 문자열에서 일부 특수문자를 제거하는 함수
 * (Markdown으로 된 문자열의 특수문자를 제거하기 위함)
 * */
function removeSpecialCharacter(str) {
  const removeCharacters = ['#', '_', '*', '~', '&', ';', '!', '[', ']', '`', '>', '\n', '=', '-']
  let _str = str
  let i = 0,
    j = 0

  for (i = 0; i < removeCharacters.length; i++) {
    j = 0
    while (j < _str.length) {
      if (_str[j] === removeCharacters[i]) {
        _str = _str.substring(0, j).concat(_str.substring(j + 1))
        continue
      }
      j++
    }
  }

  return _str
}
```

**`After`**

```jsx
function removeSpecialCharacter(str) {
  let _str = str.substring(0, 300);
  _str = _str.replace(/[#*_~&;![\]`>\n=-]/g, '')
  return _str
}
```

- replace 함수와 정규식을 사용해 특수 문자를 제거하자.
- listing page에서 preview 목적으로 보여주기 때문에 API예서 제공되는 90000자 이상의 문자열의 길이를 300자로 제한하여 특수 문자를 제거한다.

![Performance](../images/%ED%8D%BC%ED%8F%AC%EB%A8%BC%EC%8A%A42.png)

네트워크 요청시 리소스 로드 속도가 약 300ms에서 40ms로 개선됐다.

---

## 4. 코드 스플리팅

번들 파일의 코드를 분할하는 것, 번들 파일의 용량이 클 경우 리소스 로드, 렌더링 속도가 느려진다.
코드 스플리팅은 초기 로딩 시, 당장 필요하지 않은 모듈을 제거하고 필요한 시점에 불러와 페이지 로딩 성능을 향상시킨다.

- 페이지별로 분할하거나 공통으로 사용하는 모듈별로 분할하는 패턴을 사용할 수 있다.
- 코드 스플리팅을 적용하는 주체는 리액트가 아닌 webpack, parcel, vite등의 번들러에서 지원한다.

### 페이지(라우트) 단위의 코드스플리팅

- lazy 함수를 사용하면 페이지 전환 시 런타임에 해당 컴포넌트들을 import한다.
- Suspense는 라우팅시 컴포넌트를 동적으로 로드하므로 이 로딩되는 동안 로딩 화면을 보여준다.

```jsx
import React, { Suspense, lazy } from 'react'
import { Switch, Route } from 'react-router-dom'
import './App.css'

const ListPage = lazy(() => import('./pages/ListPage/index'));
const ViewPage = lazy(() => import('./pages/ViewPage/index'));

export default function App() {
  return (
    <div className="App">
      <Suspense fallback={<div>로딩 중...</div>}>
        <Switch>
          <Route path="/" component={ListPage} exact />
          <Route path="/view/:id" component={ViewPage} exact />
        </Switch>
      </Suspense>
    </div>
  )
}
```

### 스플리팅 결과

필요한 시점에 모듈을 다운로드 하고있다.

**`Root Page`**

![Root Page](../images/%EC%BD%94%EB%93%9C%EC%8A%A4%ED%94%8C%EB%A6%AC%ED%8C%851.png)

**`/view Page`**

![View Page](../images/%EC%BD%94%EB%93%9C%EC%8A%A4%ED%94%8C%EB%A6%AC%ED%8C%852.png)

---

## 5. 애니메이션 분석(Reflow, Repaint)

일반적으로 디스플레이 주사율은 초당 60프레임인데, 브라우저가 초당 20~30개의 화면밖에 못 그릴경우 애니메이션이 버벅이는 현상인 `쟁크`가 발생한다.

### 브라우저가 60프레임을 그리지 못하는 이유?

먼저 브라우저 렌더링 과정에 대해 알아야한다.

#### 브라우저 렌더링 과정(Critical Rendering Path)

1. 브라우저가 HTML, CSS, Javascript 퍄일등의 리소스를 다운로드 받음.
2. HTML, CSS를 가공해 각각 DOM, CSSOM 트리 형태의 자료구조로 변환.
3. DOM과 CSSOM을 병합해 Render Tree를 생성.
4. Layout 단계에서 컨텐츠의 위치, 크기에 대해 계산을 수행한다.
5. Paint 단계에서 렌더트리의 각 노드를 실제 픽셀로 변환한다.
6. 레이어를 합성해 실제 화면에 나타내는 composite 단계를 수행한다.

> `컨텐츠의 레이아웃, 스타일이 변경되면 해당 flow를 지속적으로 수행한다. Reflow, Repaint가 자주 발생할 경우 초당 60프레임을 보장받지 못하고 쟁크 현상이 발생하게 되는 것`

### Reflow

DOM 노드의 추가, 크기 및 위치변경 발생 시 레이아웃을 다시 계산하는 Reflow가 발생해 Render Tree를 재생성한다.
이 과정에서 픽셀값의 변경도 발생하므로 paint 단계 또한 수행된다. 즉, Critical Rendering Path의 모든 과정이 재실행된다.

> 리소스 파싱 > 렌더 트리 구축 > `레이아웃 > 페인트 > 레이어 합성`

### Repaint

DOM 노드의 스타일 변경 발생 시 리소스 파싱과 Render Tree를 재성성하지만, 레이아웃 단계를 생략하고 페인트과정만 수행된다.

> 리소스 파싱 > 렌더 트리 구축 > `페인트 > 레이어 합성`

### Reflow, Repaint 피하기

GPU의 도움을 받을 수 있는 CSS transfrom 속성을 사용해 Reflow, Repaint를 회피할 수 있다.

> 리소스 파싱 > 렌더 트리 구축 > `레이어 합성`

![css 속성](../images/css%EC%86%8D%EC%84%B1.png)