# Redux 따라하기

## Keyword

- Redux
- Reflect

## Redux

---

## Reflect [Reflect 정적 메서드](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Reflect#%EC%A0%95%EC%A0%81_%EB%A9%94%EC%84%9C%EB%93%9C)

프로그래밍에서 리플렉션(Reflection)은 런타임에서 객체의 프로퍼티, 메서드를 다이나믹하게 조작하는 프로세스를 말한다.

자바스크립트에는 이미 리플렉션 기능이 존재한다. **`Object.keys()`**, **`Object.entries()`** 및 **`prototype`** 과 같은 Object 메서드들은 고전적인 리플렉션 기능이라 할 수 있다.
ES6에서는 위와 같은 기능들이 사용성이 나쁘고 메서드명이 길어, Reflect 내장 객체를 추가하였다.

MDN에서는 Proxy 객체와 메서드가 동일하다고 하며, Proxy처럼 중간에서 주어진 동작을 인터셉트하는 내장 객체라 설명한다. (단, Proxy는 생성자로 new 연산자를 이용해 인스턴스를 생성한다.)

**`Reflect.get() 정적 메서드`**

객체의 속성 값을 반환한다. obj[prop]을 호출하는 것과 같다.
