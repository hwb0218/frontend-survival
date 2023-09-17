# 장바구니에 상품 담기

## Store 테스트

```typescript
describe('ProductFormStore', () => {
  let store: ProductFormStore;

  beforeEach(() => {
    store = new ProductFormStore();
  });

  describe('changeQuantity', () => {
    context('with correct value', () => {
      it('changes quantity', () => {
        store.changeQuantity(3);

        expect(store.quantity).toBe(3);
      });
    });

    context('with incorrect value', () => {
      it("doesn't changes quantity", () => {
        store.changeQuantity(-1);
        store.changeQuantity(11);

        expect(store.quantity).toBe(1);
      });
    });
  });
});
```

> changeQuantity action이 무수히 많이 발생할 경우라 가정했을 때, Quantity 컴포넌트를 테스트하는 것이 아닌 Store 테스트 파일에 작성한다.
> FireEvent를 여러번 실행하는 복잡성이 증가하기 때문이다. 실제로 위의 코드에서 changeQuantity 메서드에 인자만 넘겨주어 간단하게 테스트가 가능하다.
> 비즈니스 로직은 스토어에서 관리하므로 테스트가 용이해지는 효과를 보인다.

## 메서드와 getter 활용하기

```tsx
export default function Price() {
  const [{ product }] = useProductDetailStore();
  const [{ quantity }] = useProductFormStore();

  return (
    <Container>
      {numberFormat(product.price * quantity)}
      원
    </Container>
  );
}
```

> 만약 `numberFormat(product.price * quantity)` 코드가 비즈니스 로직이라 판단되면 ProductFormStore에서
> 메서드, getter를 활용해 접근 가능하다.

```typescript
import { singleton } from 'tsyringe';
import { Action, Store } from 'usestore-ts';

import {
  ProductDetail, ProductOptionItem, nullProductDetail,
} from '../types';

@singleton()
@Store()
export default class ProductFormStore {
  product: ProductDetail = nullProductDetail;

  quantity = 1;

  @Action()
  setProduct(product: ProductDetail) {
    this.product = product;
  }

  @Action()
  changeQuantity(quantity: number) {
    if (quantity <= 0) {
      return;
    }
    if (quantity > 10) {
      return;
    }
    this.quantity = quantity;
  }

  get price() {
    return this.product.price * this.quantity;
  }
}
```
