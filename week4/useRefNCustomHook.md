# useRef & Custom Hook

## keyword

- useRef
- Hook의 규칙

### 1. useRef

> useRef는 렌더링에 필요하지 않은 값을 참조할 수 있는 React Hook으로
> 값(current)이 바뀌어도 리렌더링을 트리거하지 않으며, 컴포넌트가 언마운트될 때까지 동일한 객체가 유지된다.
> ref는 일반 JS객체(참조형 데이터)이기 때문에 React는 사용자가 언제 변경했는지 알지 못한다.

**`주요 용도`**

1. 컴포넌트가 언마운트될 때까지 동일한 값을 사용해야 할 경우
2. (useEffect 등과 함꼐 쓰면서 만나게 되는) 비동기 상황에서 현재 값을 제대로 쓰고 싶은 경우

1번 예시 코드

```jsx
// 외부에서 ref 객체를 참조할 경우
const ref = {
  value: 1,
}

function TimerControl() {
  ref.value += 1;
}

// useRef를 호출해 값을 참조할 경우
function TimerControl() {
  const ref = useRef(1);
  ref.current += 1;
}
```

> TimerControl 컴포넌트를 10번 재사용한다고 가정했을 때, 각 컴포넌트는 동일한 객체의 프로퍼티를 참조하므로 value의 값이 +10 증가할 것이다. 때문에 useRef hook을 호출해 각자의 컴포넌트가 독립적인 값을 갖게된다.

2번 예시 코드

```jsx
import { useState, useRef } from 'react';

const query = useRef('');
const [filterText, setFilterText] = useState('');

// filterText값이 변경될 때 마다 query.current에 값이 할당됨
useEffect(() => {
  query.current = filterText;
}, [filterText]);

useEffect(() => {
  setTimeout(() => {
    console.log(filterText);
  }, 5_000);
}, []);
```

> 클로저로 인한 변수를 캡처, 바인드를 깜빡하는 문제가 일어난다는 말에 첨언하자면, 함수형 컴포넌트는 결국 함수이기 때문에 생명주기가 끝나면 지역변수가 메모리에서 해제되는데 이 클로저 패턴을 이용할 시 함수의 생명주기가 끝났음에도 내부 함수에서 변수를 참조하고 있기 때문에 변수의 캡쳐, 바인드가 발생한다. useState도 내부적으로 클로저를 이용해 컴포넌트가 반환된 후에도 계속 상태값을 참조하며 화면에 보여주고 그 상태를 가지고 1씩 더하거나 하는등의 계산을 수행하며 업데이트 하는 것인데, 이러한 원리로 인하여 현재 useEffect는 컴포넌트가 마운트 시 한 번만 실행되므로 상태 업데이트로 인한 컴포넌트 리렌더링이 발생하기 전까진 당시의 상태값을 참조하여 5초 뒤에 빈 문자열이 출력된다.

---

### 2. Hook의 규칙

> React Hooks의 호출은 컴포넌트 또는 Custom Hook의 최상위 레벨에서 호출해야한다.
> 종종 조건문이나 콜백 함수 내부에서 호출하는 실수를 범한다.

잘못된 예제 코드

```jsx
const [playing, setPlaying] = useState(false);

if (playing) {
  const products = useFetchProducts();
  console.log(products);
}
```

---

### 추가 키워드

- Custom hook

**`Custom hook`**

> 로직을 재사용하기 위한 가장 쉬운 방법  
> React의 훅을 사용하여 컴포넌트 로직을 재사용하기 위한 함수이다. 커스텀 훅에 부수 효과 작업이나 상태 관리 로직을 캡슐화하여
> 컴포넌트의 코드를 보다 간결하게 작성할 수 있다. 커스텀 훅의 이름은 **`use`** 로 시작해야 한다.

예시 코드

```tsx
// 서버 요청 커스텀 훅
function useFetchProducts() {
  const [products, setProducts] = useState<Product[]>([]);

  useEffect(() => {
    const fetchProducts = async () => {
      const url = 'http://localhost:3000/products';
      const response = await fetch(url);
      const data = await response.json();
      setProducts(data.products);
    };

    fetchProducts();
  }, []);

  return products;
}
```

> 내부에서 API 요청을 보내거나, useEffect를 쓰거나 커스텀 훅을 호출하는 컴포넌트는 내부 로직에 대해 관심이 없고
> 그저 반환하는 값만 가져다 쓴다.
