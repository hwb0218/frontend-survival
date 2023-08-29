# Navigation

## Keyword

- Web APIs - History
- React Router - NavLink, Link, Navigate, useNavigate

## 1. Web APIs - History

- 웹 브라우저의 히스토리를 조작할 수 있는 기능을 제공하는 API
- 히스토리 스택으로 페이지 전환을 관리하고, 이전 페이지와 다음페이지로 이동같은 브라우저 동작을 조작할 수 있다.

---

## 2. React Router

다음 키워드들은 React Router에서 지원하는 다양한 라우팅 기능이다.

### NavLink

`<Link>`와 기능은 유사하지만, 현재 경로와 일치할 때 스타일을 적용한다.

### Link

다른 페이지로 이동하는 일반적인 링크의 역할을 하며 HTML의 `<a>` 태그와 유사한 기능을 제공하지만, 페이지 새로고침 없이 페이지 전환이 가능하다.

### Navigate

- Navigate는 렌더링될 때 페이지를 변경한다.
- 조건에 따라 라우팅을 처리하거나 특정 이벤트 후에 페이지를 변경할 때 사용
- `<Navigate>` 컴포넌트는 사실상 useNavigate 훅을 사용하는 래퍼(Wrapper) 컴포넌트로서, useNavigate와 동일한 인자를 props로 받을 수 있다.

### useNavigate

- 함수를 반환하며 프로그래밍 방식으로 페이지 전환을 수행할 수 있다.
- 첫 번째 인자로 이동할 페이지 `to`값을, 두 번째로 옵션 객체를 전달할 수 있다.

```jsx
import { Navigate, useNavigate } from 'react-router-dom';

<Navigate to="/about" />

const navigate = useNavigate();
navigate('/about');
```

- 히스토리 스택 변경량 입력 방식도 있다.

```jsx
import { Navigate, useNavigate } from 'react-router-dom';

<Navigate delta={-1} /> 

const navigate = useNavigate();
navigate(-1);
```

#### 옵션 객체

- replace: 페이지 이동 후 이전 페이지로 돌아갈 수 없다. 뒤로가기를 누르면 메인 페이지('/')로 이동한다.
- state: 페이지 전환 시 상태를 함께 전달할 수 있다. **`{ state: { productInfo: '상품 정보' } }`**
- preventScrollReset: 페이지 전환 시 스크롤 위치를 고정시킬 수 있다.
