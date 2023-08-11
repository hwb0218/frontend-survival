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

<!-- > setInterval을 useEffect 내부에서 사용할 때 주의할 점은 컴포넌트가 리렌더될 때 마다 setInterval의 콜백함수가 -->

#### useEventListener

#### useLocalStorage

#### useDarkMode

---

### swr

---

### react-query
