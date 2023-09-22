# 웹 최적화

프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1 정리

## Lighthouse

웹 서비스의 성능 측정과 품질 향상 가이드라인을 제공해주는 크롬 개발자 도구

- 추천항목: 리소스의 관점에서 가이드를 제공(로딩 성능 최적화)
- 진단항목: 페이지의 실행 관점에서 가이드를 제공(렌더링 성능 최적화)

---

## 이미지 사이즈 최적화

- 이미지 CDN을 사용한다(사용자에게 이미지를 전송하기 전 사이즈를 가공하거나 이메지 포멧 변경을 제공)
- 이미지를 업로드할 때 사이즈를 미리 가공한다.

> CDN?  
> 서버의 물리적 거리의 한계를 극복하기 위해 사용자와 가까운 곳에 컨텐츠 서버를 두는 기술

---

## 병목 코드 최적화

- 병목 현상을 발생시키는 코드를 찾아 최적화한다.

> 병목 현상  
> 하나의 구성 요소로 인한 전체 시스템 성능이 제한받는 현상

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
- listing page에서 preview 목적으로 보여주기 때문에 API예서 제공되는 90000자 이상의 문자열의 길이를 200자로 제한하여 특수 문자를 제거한다.

---

## 코드스플리팅

번들링 파일의 용량이 클 경우 리소스 로드, 렌더링 속도가 느려진다.
코드스플리팅은 초기 로딩 시, 당장 필요하지 않은 모듈을 떼어내기 위해 사용된다.

- 코드스플리팅을 적용하는 주체는 리액트가 아닌 webpack, parcel, vite등의 번들러에서 지원한다.
