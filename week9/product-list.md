# 목록 보기

## 1. 상품 목록

1. 상품 목록 얻기
2. 상품 목록 보여주기

> 상품 목록은 useFetchProducts 훅이 담당하고, 상품 목록 보여주기는 Products 컴포넌트가 담당한다.  
> Products 컴포넌트에서 훅을 호출해도 되지만, page에서 네트워크 통신 커스텀훅을 호출하고 컴포넌트는 UI구현에 집중할 수 있도록 관심사를 분리한다.
> 이는 테스트 코드 작성이 쉬워지고 의미단위(도메인 측면, 컴포넌트가 지닌 의미)에서 컴포넌트가 분리되어 유연한 구조를 만들 수 있다.

---

## 2. 컴포넌트의 점진적 분리

> 하나의 파일에 컴포넌트의 덩치가 거대해질 경우 폴더 구조를 잡아가며 점진적으로 컴포넌트를 분리해 나가면 된다.

---

## 3. api fetch hook을 간단히 구현하고 화면에 집중

> 화면에 컨텐츠를 보여주는 것이 핵심이므로 컴포넌트에 집중한다.  
> 서버 API구현이 완료되었다면 사용하면 되고, 아닐경우 MSW를 이용해 네트워크 통신을 mocking 한다.

---

## 4. nullish 병합 연산자(??)를 사용한 이유

```tsx
const apiBaseUrl = 'https://shop-demo-api-01.fly.dev';

export default function useFetchProducts() {
  type Data = {
    products: ProductSummary[];
  };

  const { data } = useFetch<Data>(`${apiBaseUrl}/products`);

  return {
    products: data?.products ?? [],
  };
}
```

> 컴포넌트가 렌더링된 후 비동기 통신을 수행하기 때문에 아직 데이터를 받지 못한 경우 컴포넌트에서 data?.products에 접근할 때 런타임 에러가 발생한다.  
> 때문에 초기값으로 빈 배열을 지정해주는 것.

---

## 5. intl API [링크](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

> 국가별로 상이한 날짜, 통화 표기법등 데이터 포맷팅 문제를 해결할 수 있도록 API를 제공한다.

---

## 6. Axios vs Fetch

Fetch API는 모던 브라우저에서 내장된 API로 따로 설치할 필요가 없다.
Axios는 서드파티 라이브러리로 CDN이나 npm, yarn 같은 패키지 매니저를 통해 설치한다.

### 문법

두 방법 모두 첫번째 인자로 요청 url과 두번째는 선택적 인자로 option 객체를 받는다.

`Fetch`는 GET을 제외한 요청시 option 객체의 method 속성 설정이 필요하다.

`Axios`는 axios 객체에 http request method가 정의되어 있다.

```javascript
fetch(url, {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({}),
});
```

```javascript
axios.get(url, {
  // 설정 옵션
});
```

### JSON 데이터 처리

`Fetch`는 then 매서드에서 처리된 promise를 반환한다. 이 때 JSON 포멧이 아니므로 **`.json()`** 메서드를 사용해 직렬화를 수행한다. 해당 메서드를 사용하면 resolve된 promise를 반환한다.

```javascript
const url = "https://jsonplaceholder.typicode.com/todos";

axios.get(url).then((response) => console.log(response.data));

```

`Axios`는 기본적으로 JSON 포멧의 응답 데이터를 반환한다.