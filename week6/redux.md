# Redux 따라하기

## Keyword

- Redux
- Reflect

## 1. Redux

Redux는 자바스크립트 애플리케이션의 상태 관리를 위한 라이브러리다. 주로 React와 함께 사용되는데 일반 자바스크립트 환경에서도 사용 가능하고 Angular와 같은 다른 프레임워크에서도 사용된다.

FLUX는 데이터의 흐름을 단방향으로 정의하는 패턴으로, 실제 프로그램처럼 사용할 수 있는게 아닌 추상적인 개념들을 구조화시켜 정의한 것이며 Redux는 FLUX Achitecture를 실제로 구현한 구현체이다. **`즉 Redux는 Flux를 실제로 구현한 라이브러리이다.`**

이를 통해 애플리케이션의 수많은 상태를 효과적으로 관리하고 결과를 예측 가능하도록 설계할 수 있다.

### Redux의 3가지 규칙

- 1 - 하나의 애플리케이션에는 단 하나의 스토어를 사용한다.
- 2 - 상태는 읽기 전용이다.
  
> Redux는 내부적으로 데이터의 변경을 감지하기 위해 얕은 비교를 수행하기 때문에 새로운 상태를 생성하여 객체의 깊숙한 데이터를 비교하지 않고도 얕은 비교를 통해 좋은 성능을 유지할 수 있다.
> 
- 3 - 리듀서는 순수함수여야 한다.

---

## 2. Reflect [Reflect 정적 메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Reflect#%EC%A0%95%EC%A0%81_%EB%A9%94%EC%84%9C%EB%93%9C)

프로그래밍에서 리플렉션(Reflection)은 런타임에서 객체의 프로퍼티, 메서드를 다이나믹하게 조작하는 프로세스를 말한다.

자바스크립트에는 이미 리플렉션 기능이 존재한다. **`Object.keys()`**, **`Object.entries()`** 및 **`prototype`** 과 같은 Object 메서드들은 고전적인 리플렉션 기능이라 할 수 있다.
ES6에서는 위와 같은 기능들이 사용성이 나쁘고 메서드명이 길어, Reflect 내장 객체를 추가하였다.

MDN에서는 Proxy 객체와 메서드가 동일하다고 하며, Proxy처럼 중간에서 주어진 동작을 인터셉트하는 내장 객체라 설명한다. (단, Proxy는 생성자로 new 연산자를 이용해 인스턴스를 생성한다.)

**`Reflect.get() 정적 메서드`**

```javascript
Reflect.get(target, propertyKey[, receiver])
```

객체의 속성 값을 반환한다. target[propertyKey]를 호출하는 것과 같다.

```javascript
const object1 = {
  x: 1,
  y: 2,
};

console.log(Reflect.get(object1, 'x'));
// Expected output: 1

const array1 = ['zero', 'one'];

console.log(Reflect.get(array1, 1));
// Expected output: "one"
```
