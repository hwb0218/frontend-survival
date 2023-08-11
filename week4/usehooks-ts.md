# usehooks-ts Lib

## keyword

- usehooks-ts
  - useBoolean
  - useEffectOnce
  - useFetch
  - useInterval
  - useEventListener
  - useLocalStorage
  - useDarkMode
- swr
- react-query

### usehooks-ts

> Custom Hook을 모아놓은 라이브러리, 잘 만들어 놓은 Custom Hook을 통해 아이디어를 얻어가자.

#### useBoolean

> 참과 거짓을 판별하는 Hook, toggle과 같이 의도가 명확한 함수를 사용하자.

```jsx
import { useBoolean } from 'usehooks-ts';

const { value : playing, toggle } = useBoolean();

const handleClick = () => toggle();
```

#### useEffectOnce

> 비어있는 의존성 배열을 넣어 컴포넌트 마운트 시 딱 한 번만 실행하는 effect, once을 붙여 한 번만 실행됨을 명시적으로 알 수 있다.

```jsx
import { useEffectOnce } from 'usehooks-ts';

  useEffectOnce(() => {
    const fetchProducts = async () => {
      const url = 'http://localhost:3000/products';
      const response = await fetch(url);
      const data = await response.json();
      setProducts(data.products);
    };

    fetchProducts();
  });
```

#### useFetch

> 서버 API에 요청을 보내는 Hook, 간단하게 사용할 때 유용하다.

```jsx
import { useFetch } from 'usehooks-ts';

const url = 'http://localhost:3000/products';
const { data = {products: []} } = useFetch(url);
```

#### useInterval

> setInterval을 컴포넌트 내부에서 사용할 때 주의할 점은 setInterval의 콜백함수는 클로저로서 외부 변수를 참조한다. 떄문에 해당 값이 변경되었어도, 함수가 정의될 당시의 값을 기억하고 있어 동일한 값을 참조하게 된다.

```jsx
function IntervalComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      // setCount(count + 1); => X
      setCount(prevCount => prevCount + 1); 
    }, 1000);

    return () => {
      clearInterval(interval);
    };
  }, []);

  return <div>...</div>;
}
```

> setInterval을 사용해야 할 경우 useInterval을 사용하고, 직접 구현 해야한다면 custom hook을 만들어 해결해야한다.

**`useInterval 코드`**

```jsx
import { useEffect, useLayoutEffect } from 'react'

export const useIsomorphicLayoutEffect =
  typeof window !== 'undefined' ? useLayoutEffect : useEffect
```

> 내부 로직에 useIsomorphicLayoutEffect Hook을 사용하고 있는데 실행 환경이 브라우저면 DOM 렌더링 전에 실행되는 useLayoutEffect 훅을 사용하고 아니라면 useEffect를 사용한다.

#### useEventListener

> window 객체에 접근하는 행위도 외부 시스템과 싱크하는 부수 효과이므로 useEffect 내부에서 조작하는데
> useEventListener의 장점은 useEffect를 생략하고 브라우저 스크롤, 리사이즈 이벤트와 같이 window 객체에 접근해 브라우저 자체 UI를 조작할 때 유용한 것 같다. 특수하게 외부에 물려있는 코드가 많을 경우 해당 훅을 쓰면 유용하다고 한다.

#### useLocalStorage

> 웹 스토리지, localStorage를 통해 객체를 JSON으로 영속화(외부에 데이터 저장이 지속되는)
> 헤당 기능을 사용하면 팝업을 며칠간 안보기, 테마 색상 변경하기 등이 가능

#### useDarkMode

> useDarkMode 내부적으로 useLocalStorage 훅을 사용하고 있음(브라우저가 종료 후 재실행 됐을 때 테마는 지속되어야 함)  

> 좋은 기능들이 많이 있는 것 같은데, 개인적으로는 가져다 쓰기만 하면 라이브러리에 너무 의존하게 되니 직접 구현이 가능한 부분은 최대한 구현할 수 있도록 한다.

---

### swr

---

### react-query

> React Query는 React 애플리케이션의 비동기 데이터를 caching하여 필요할 때 다시 가져올 수 있다.

- 요청 데이터를 메모리에 캐싱하여 동일한 데이터에 대한 반복적인 요청을 캐시에서 제공함 (네트워크 비용 절약)
- 데이터 요청 실패시 자동 재시도

예제 코드

```jsx
import { useQuery } from '@tanstack/react-query';

function Products() {
  const { isLoading, error, data: products } = useQuery(['queryKey'], async () => {
    return fetch('request url').then((res) => res.json());
  })

  if (isLoading) return <p>Loading...</p>;

  if (error) return <p>{error}</p>;
}
```

> 첫번째 컴포넌트가 요청 데이터를 queryKey의 이름 아래에 요청 데이터를 메모리에 캐싱하기 때문에
> 두번째 컴포넌트가 똑같은 queryKey로 네트워크 통신 시도 시, 동일한 데이터에 대한 반복적인 요청이므로 해당 데이터를 캐시에서 제공하여 불필요한 네트워크 요청을 줄인다.
> 즉, A라는 key를 사용하는 모든 요청에 대해서 동일한 캐시를 사용한다.
