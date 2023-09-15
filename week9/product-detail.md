# 상품 상세 보기

## 상품 상세

```tsx
export default function ProductDetailPage() {
  const params = useParams();

  const { loading, error } = useFetchProduct({
    productId: String(params.id),
  });

  if (loading) {
    return (
      <p>Loading...</p>
    );
  }

  if (error) {
    return (
      <p>Error!</p>
    );
  }

  return (
    <ProductDetail />
  );
}
```

> 장바구니 담기 기능으로 인한 props drilling 문제를 예방하기 위해서, ProductDetailPage에서 product를 내려주지 않도록 설계함.
> useFetchProduct 훅을 호출한 이유로 url pathname이 부정확할 경우 발생할 수 있는 page not found error를 해결하기 위한 목적도 있다.

## Null Object

```typescript
export const nullProductDetail: ProductDetail = {
  id: '',
  category: { id: '', name: '' },
  images: [],
  name: '',
  price: 0,
  options: [],
  description: '',
};
```

> 초기값이 null인 경우 Null Object를 사용해 처리할 수 있다.  
> 아무래도 초기값이 null이라면 객체 속성접근시 참조 에러가 발생할 수 있기도 해, 그에 따른 옵셔널 체이닝과 non-null assertion, as 문법, 타입 가드 등으로 처리할 수 있지만 일일히 처리하는 수고를 덜기 위해 사용하는 것 같다.

## jest - toBeEmptyDOMElment

테스트에서 컴포넌트가 빈 div를 반환하는지 확인하는 방법

```typescript
const { container } = render(<YourComponent />);

expect(container).toBeEmptyDOMElement();
```
