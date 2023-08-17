# MSW

## Keyword

- Service worker
- MSW(Mock Service Worker)
- polyfill(폴리필)

## 1. Service worker

웹 애플리케이션에서 백그라운드 동기화, 푸시 알림 등이 가능하도록 지원해주는 도구. 서비스 워커는 브라우저의 백그라운드에서 실행되는 스크립트인데, 웹 애플리케이션과 브라우저 사이에서 중간 계층(프록시 서버)의 역할을 한다.

### 서비스 워커의 제약

1. 브라우저의 백그라운드에서 실행되므로, 요청이 없는한 작동하지 않는다(idle 상태). 강제로 종료하는 **`.terminate()`** 메서드는 존재하지 않는다.
2. 웹의 life cycle을 따르지 않는다. 웹페이지가 닫히더라도 자동으로 비활성화 되지 않는다.
3. 웹 페이지와 별도로 존재하므로 DOM, Window 요소에 접근할 수 없다.

### Proxy?

프록시는 요청을 인터셉트해서 특정 동작을 수행후 반환하는 역할을 한다.

---

## 2. MSW(Mock Service Worker)

MSW는 개발 및 테스트 환경에서 API 요청을 가로채서 가짜 응답을 제공하여 실제 서버에 의존하지 않고도 테스트를 수행하거나 개발할 수 있게 해준다. 모의 서버와 같은 역할을 한다.

### MSW 특징

1. 실제 서버가 준비되지 않은 초기 개발 단계에서 작업을 진행할 수 있음.
2. 가짜 응답을 제공하는 모의 서버를 생성해, 서버에 의존하지 않고 테스트할 수 있음.

**`jest.config.js`**

```javascript
module.exports = {
 //...
  setupFilesAfterEnv: [
    '@testing-library/jest-dom/extend-expect',
    '<rootDir>/src/setupTests.ts', // 추가
  ],
 //...
};
```

**`src/setupTests.ts`**

```typescript
import 'whatwg-fetch';
import server from './mocks/server';

// 핸들러가 없거나 응답이 정의되지 않은 요청이 발생했을 때 에러를 발생 
beforeAll(() => server.listen({ onUnhandledRequest: 'error' }));

afterAll(() => server.close());

afterEach(() => server.resetHandlers());
```

**`src/mocks/server.ts`**

```typescript
import { setupServer } from 'msw/node';

import handlers from './handlers';

const server = setupServer(...handlers);

export default server;
```

**`src/mocks/handlers.ts`**

```typescript
import { rest } from 'msw';

const BASE_URL = 'http://localhost:3000';

const handlers = [
  rest.get(`${BASE_URL}/products`, (req, res, ctx) => {
    const products = [
      {
        category: 'Fruits', price: '$1', stocked: true, name: 'Apple',
      },
    ];

    return res(
      ctx.status(200),
      ctx.json({ products }),
      );
    }),
  ];

export default handlers;
```

**`App.test.ts`**

```typescript
import { render, screen, waitFor } from '@testing-library/react';

import App from './App';

// 모듈을 mocking하는 jest.mock 불필요
test('App', async () => {
  render(<App />);

  await waitFor(() => {
    screen.getByText('Apple');
  });
});
```

**`Fetch API polyfill: whatwg-fetch`**

Fetch API는 브라우저에서 지원하는 API로 Node에서 사용하기 위해서 polyfill을 구성한다.
최신 버전의 Node.js에서는 Fetch 사용 가능하다고 함.

---

## 3. polyfill(폴리필)

단어의 뜻처럼 빠진 솜을 충전해주는 역할을 한다. JS의 최신문법을 지원하지 않는 런타임(브라우저, Node.js)에 코드 조각, 플러그인을 추가하는 역할

### Babel이 있는데 왠 Polyfill..?

바벨은 ES6+문법을 ES5로 트랜스파일링 하지만, ES5가 지원하지 않는 ES6의 Map, Promise, Set, Object.assigin()은 트랜스파일링이 불가능하다. 때문에 Pollyfill을 통해 코드 조각을 추가해야만 한다.우리가 의식하지 않아도 CRA(create-react-app)와 같은 CLI로 프로젝트 환경을 구성하면 내부적으로 polyfill 관련 core-js, regenerator-runtime 모듈을 세팅하므로 자동으로 폴리필을 구성하고 있었던 것.
