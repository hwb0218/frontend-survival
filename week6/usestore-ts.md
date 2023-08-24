# usestore-ts

External Store를 사용함으로 concurrent feature에서 발생하는 티어링 문제를 겪어보질 않아 뭐가뭔지..
리액트 18에 추가된 기능을 사용해보질 않아서 그런가? 렌더링된 후 유저 인터렉션이 늦게 처리되는 경우를 겪어보질 않아 그럴수도 있겠다.

## Keyword

- usestore-ts
- useSyncExternalStore

---

## 1. usestore-ts

데코레이터를 이용해 Store, Action Store의 기능을 부여하고 사용할 수 있다. 내부적으로 useSyncExternalStore hook을 사용함.

---

## 2. useSyncExternalStore

- 외부 스토어를 구독할 수 있는 React Hook
- 컴포넌트 최상위 레벨에서 useSyncExternalStore를 호출하여 외부 데이터 저장소에서 값을 읽는다.

기존엔 UI렌더링 작업중 인터렉션이 발생하면 렌더링이 끝나기 전까지 인터렉션 처리가 지연됐다.
리액트 18부턴 concurrent feature라는 기능이 도입됐는데,
렌더링 도중 유저 인터렉션이 발생하면 렌더링 우선 순위를 바꿔 유연하게 UI를 렌더링 가능하게 만드는 기능이다.

문제는 의도치 않게 상태 불일치로 인한 서로 일치하지 않는 시점의 UI가 렌더되는 티어링이 발생하기 때문에 React의 internal store는 이를 대비해 내부 깊숙한 곳에 상태 처리를 할 수 있는
알고리즘을 구현해 놓았지만, external store를 사용할 경우 알고리즘이 적용되지 않아 티어링을 해결할 수 없다.
useSyncExternalStore 훅을 사용해 티어링이 발생하지 않도록 외부 저장소의 변경사항을 지켜보고 있다가 완료되면 다시 렌더링을 시작한다.
