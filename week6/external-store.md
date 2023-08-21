# External Store

## Keyword

1. 관심사의 분리
2. Layered Architecture
3. Flux Architecture
4. useReducer
5. useCallback

## 1. 관심사의 분리

## 2. Layered Architecture

## 3. Flux Architecture

## 4. useReducer

## 5. useCallback

---

React에서 성능을 최적화 할 때 사용하며, 함수를 메모이제이션(memoization)하기 위해 사용하는 hook이다. 컴포넌트는 렌더링 될 때마다 내부에 선언한 함수가 새롭게 생성되는데 useCallback을 통해 기존 함수를 저장하고 재사용한다.

**`메모이제이션(memoization)`**

> 함수 호출결과를 캐싱하고 동일한 입력이 다시 발생할 때 캐싱된 결과를 반환하는 프로그래밍 기술이다.

```jsx
const memo = useCallback('함수', '배열');
```

- 두번째 인자인 의존성 배열에 삽입한 요소의 값이 변경되면 함수를 재선언한다.
- 그런데 컴포넌트가 렌더링 될 때 마다 함수가 새로 선언되는 것은 자바스크립트가 브라우저에서 얼마나 빨리 실행되는지를 생각해보면 성능상 큰 문제가 되지 않는다.
- 따라서 단순히 컴포넌트 내부에서 함수를 반복 생성하지 않기 위해 **`useCallback()을`** 사용하는 것은 큰 의미가 없거나 오히려 **`손해일`** 수 있다.

그렇다면 어떻게 사용해야 의미있는 성능향상을 기대할 수 있나?

### 자바스크립트 함수 동등성

자바스크립트에서 함수는 객체(정확히는 일급객체)로 취급되는데, 동일한 코드의 함수일지라도 다른 함수로 판단한다. 이는 메모리 주소에 의한 참조 비교를 수행하기 때문이다.(각 함수가 저장된 메모리 주소가 같지않다)

```javascript
const add1 = () => x + y; 
const add2 = () => x + y; 
add1 === add2 // false
```

이러한 자바스크립트의 특성은 함수를 다른 함수의 인자로 넘기거나, 자식컴포넌트의 props로 넘길 때 함수의 참조가 달라서 예상치 못한 성능 문제가 발생할 수 있다.

### 예상치 못한 성능 문제

fetch API를 사용해 데이터를 가져오는 fetchData 함수와 useEffect의 의존성 배열에 해당 함수를 추가한 예시다.

```jsx
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = () =>
    fetch(`https://your-api.com/users/${userId}`)
      .then((response) => response.json())
      .then(({ user }) => user);

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```

- fetchUser의 함수가 변경되면 useEffect를 호출해 유저 데이터를 다시 받아오는 로직이다.
- 문제점은 함수의 동등성으로 인한 서로 다른 함수로 판단하기 때문에 무한루프에 빠진다.
- userId값과 상관없이 fetchUser 함수는 렌더링될 때 마다 새로운 참조값으로 변경되기 때문에 useEffect의 effect 콜백함수를 호출하고 user 상태를 업데이트하고 컴포넌트가 리렌더되고 다시 fetchUser 함수의 참조값이 변경되고 이런 사이클의 무한루프에 빠지게 된다.

### 해결 방법

이럴때 useCallback hook을 이용해 함수의 동등성을 유지한다.

```jsx
import React, { useState, useEffect } from "react";

function Profile({ userId }) {
  const [user, setUser] = useState(null);

  const fetchUser = useCallback(
    () =>
      fetch(`https://your-api.com/users/${userId}`)
        .then((response) => response.json())
        .then(({ user }) => user),
    [userId]
  );

  useEffect(() => {
    fetchUser().then((user) => setUser(user));
  }, [fetchUser]);

  // ...
}
```

- **`useCallback()`** 훅을 이용해 함수의 참조값을 동일하게 유지시킨다.
- fetchUser함수는 의존성 배열의 userId값이 변경되지 않는한 재호출되지 않는다.

### useMemo

useMemo hook또한 메모이제이션이 사용되는데, 기존과 동일한 입력이 발생할 경우 캐싱된 값을 재사용한다.