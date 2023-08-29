# Router

## Keyword

- ReactRouter - RouterProvider

## 1. ReactRouter - RouterProvider

- React Router v6.4에 추가된 새로운 라우팅 방식
- 기존엔 컴포넌트 최상위에 `<BrowserRouter>`로 `<App>`컴포넌트를 감싸줬다.
- 해당 방식은 라우터 객체를 만들어 라우팅 정보만 별도의 파일로 관리
- 중첩된 경로는 `children`을 이용
- `<App>`컴포넌트를 거치지 않고 바로 브라우저 라우터를 생성 후 사용한다.

**`src/routes.tsx`**

```jsx
import { Outlet } from 'react-router-dom';

function Layout() {
  return (
    <div>
      <Header />
      <Outlet />
      <Footer />
    </div>
  );
}

const routes = [
  {
    element: <Layout />,
    children: [
      { path: '/', element: <HomePage /> },
      { path: '/about', element: <AboutPage /> },
    ],
  },
];

export default routes;

```

**`src/App.tsx`**

```jsx
import { createBrowserRouter, RouterProvider } from 'react-router-dom';

import routes from './routes';

const router = createBrowserRouter(routes);

root.render((
  <React.StrictMode>
    <RouterProvider router={router} />
  </React.StrictMode>
));
```

## 추가 키워드

### Outlet

- v6부터 컴포넌트의 children처럼 중첩 라우팅이 가능해짐
- 예를 들면, `/member`와 `/member/:memberId` 라우트가 각 한 줄씩 차지했는데 member하위에 :memberId 쿼리파라미터 라우트를 추가하면 중첩 라우팅이 가능
- 하위 라우트는 `url path` 세그먼트를 반복할 필요가 없음

```jsx
//v5
<Switch>
  <Route path="/member" />
  <Route path="/member/:memberId" />
</Switch>
 
//v6
<Routes>
  <Route path="/member">
    <Route path=":memberId" />
  </Route>
</Routes>
```

- 중첩라우팅을 구성 후 `<Outlet>` 컴포넌트로 상위 컴포넌트를 레이아웃화 할 수 있다.

```jsx
import { Outlet } from 'react-router-dom';

const routes = [
  {
    path: "/",
    element: <App1 />,
    errorElement: <NotFound />,
    children: [
      { index: true, element: <First /> },
      { path: "second", element: <Second /> },
      { path: "third", element: <Third /> },
    ],
  },
  {
    path: "/app2",
    element: <App2 />,
    errorElement: <NotFound />,
    children: [
      { index: true, element: <First /> },
      { path: "second", element: <Second /> },
      { path: "third", element: <Third /> },
    ],
  },
];
```

```jsx
import { Outlet } from "react-router-dom";

// App1.js
function App1() {
  return (
    <div>
      <h1>This is App1 Header</h1>
      <Outlet />
      <h2>This is App1 Footer</h2>
    </div>
  );
}
 
function App2() {
  return (
    <div>
      <h1>This is App2 Header</h1>
      <Outlet />
      <h2>This is App2 Footer</h2>
    </div>
  );
}
// App2.js
```

- 구성한 중첩 라우팅은 `<Outlet>`을 통해 자식 컴포넌트를 표현하고 상위 컴포넌트를 고정적으로 보여줄 수 있다.
