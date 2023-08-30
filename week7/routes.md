# Routes

## Keyword

- 라우터란?
- React Router
  - Browser Router
  - Route
  - Memory Router

## 1. 라우터란?

- 웹 애플리케이션에서 사용자가 요청한 URL 경로의 페이지로 연결하는 시스템을 말한다.
- 웹 애플리케이션의 페이지 또는 View간의 전환 및 관리를 담당한다.

---

## 2. React Router

- 리액트 애플리케이션에서 Clinet Side Routing을 구현하기 위한 라이브러리다.

### Clinet Side Routing

- 초기 페이지 로딩 이후에는 새로운 페이지를 서버에 요청할 필요가 없이 브라우저에서 라우팅을 처리한다.
- 다른 페이지로 이동하면 Javascript를 통해 컨텐츠를 동적으로 렌더링한다.
- 빠르고 부드러운 페이지 전환을 제공한다.
- 다만 초기 페이지 로딩시 필요한 리소스를 다운로드하므로 초기 로딩 속도가 느릴 수 있다.
- JS를 이용해 컨텐츠를 동적으로 생성하기 때문에 SEO 최적화 문제가 있다.

#### VS SSR(Server Side Routing)

- 페이지를 전환할 때 마다 서버에 요청을 보내고 새로운 페이지를 서버에서 렌더링한 후 브라우저에 전달한다.
- 페이지 전환마다 HTML 문서를 받아야 하므로 페이지 리로딩이 발생한다.
- 각 페이지를 서버로부터 받아오기 때문에 SEO 최적화에 용이하다.

### 2.1 Browser Router

- 브라우저의 history API을 사용하여 URL 경로에 따라 페이지 전환을 관리한다.

```jsx
import { BrowserRouter } from 'react-router-dom';

root.render((
  <BrowserRouter>
    <App />
  </BrowserRouter>
));
```

### 2.2 Route

- URL 경로에 따라 Route 컴포넌트를 렌더링하도록 지정할 수 있다.

```jsx
import { Routes, Route } from 'react-router-dom';

function App() {
  return (
    <div>
      <Header />
      <main>
        <Routes>
          <Route path="/" element={<HomePage />} />
          <Route path="/about" element={<AboutPage />} />
        </Routes>
      </main>
      <Footer />
    </div>
  );
}
```

### 2.3 Memory Router

- 브라우저 주소창의 URL을 조작하지 않고, 메모리에서 라우팅을 구성할 수 있다.
- 테스트 코드, 모바일 앱에서 브라우저 URL을 변경하지 않고 라우팅을 시뮬레이션 할 수 있다.
- initialEntries 속성은 Memory Router가 초기화 될 때 라우팅에 사용될 경로 배열을 지정한다.

```javascript
describe('App', () => {
  function renderApp(path: string) {
    render((
      <MemoryRouter initialEntries={[path]}>
        <App />
      </MemoryRouter>
    ));
  }

  context('when the current path is “/”', () => {
    it('renders the home page', () => {
      renderApp('/');

      screen.getByText(/Hello/);
    });
  });

  context('when the current path is “/about”', () => {
    it('renders the about page', () => {
      renderApp('/about');

      screen.getByText(/About/);
    });
  });
});
```

---

## 추가 키워드

### Routes

- Routes 컴포넌트는 여러 Route를 감싸서 그 중 규칙이 일치하는 라우트 단 하나만을 렌더링 시켜주는 역할을 한다.
