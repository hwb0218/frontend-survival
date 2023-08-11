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

#### useLocalStorage

#### useDarkMode

---

### swr

---

### react-query
