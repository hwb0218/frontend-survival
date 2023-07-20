# TypeScript

### Keyword
1. REPL
2. TypeScript
   - 2-1 Interface vs Type
   - 2-2 타입 추론
   - 2-3 Union Type vs Intersection Type
   - 2-4 Optional Parameter


### 1. REPL
> Read-Eval-Print Loop의 약자     
> 인터프리터 언어에서 사용되는 대화형 개발 도구 또는 환경으로 터미널에 코드를 입력하면 즉시 실행 결과를 받을 수 있다. 
---
### 2. TypeScript
> **TypeScript**는 동적 타입 언어인 JavaScript에 정작 타입을 부여한 언어이다.     
> 브라우저는 **JavaScript** 파일만 실행 가능하므로 변환 과정인 **컴파일**이 필요하다.

##### **`왜 타입스크립트를 사용해야할까?`**
1. 코드 레벨에서 에러의 사전 예방
2. 편집기의 코드 가이드 및 자동 완성 기능 (개발 생산성 향상) 
   - 특정 변수에 타입이 지정되어 있을경우 해당 타입의 사용가능한 API를 미리 보기로 가이드 해준다.
  
~~`진짜 2번이 진또베기`~~

VSC 툴의 내부가 TS로 작성되어 있어 TS개발에 최적화되어 있다고 한다.

<br />

#### 2-1 Interface vs Type
> TypeScript에서 타입을 정의하는 방법들로 Type(Type alias)과 Interface의        
> 결정적 차이는 타입의 **확장(extends)** 가능 여부에 있다.

##### **`1. Interface`**
- 객체 또는 클래스 같은 구조화된 타입을 정의할 때 유용하다.
##### **`2. Type alias`**
- 유연한 타입 정의 제공 (Union, intersection, tuple 등)

```typescript
/* interface는 이러한 방법으로 직접 타입 연산자 사용이 불가능 */
type Color = 'white' | 'blue' | 'red';

/* 객체, 클래스 구조 타입 정의에 유용 */
interface Info {
  id: number;
  name: string;
}
```
<br />

#### 2-2 타입추론 (Type Inference)
> 변수등에 타입을 따로 지정하지 않아도 타입스크립트가 코드를 분석해 타입을 추론하는 과정을 의미
```typescript
const temp = 10;
// 변수 temp 타입은 number로 추론됨
```
##### `Best Common Type`
여러 표현식의 타입을 비교하여 가장 근접한 타입을 선택하는 규칙
```typescript
const foo = [1, null]
```
- 타입을 명시적으로 지정하지 않았지만 Best Common Type 규칙을 통해 `(number | null)[]` 타입으로 추론된다.

<br/>

#### 2-3 Union Type vs Intersection Type
> 연산자를 이용해 타입을 정의하는 방법      

##### **`1. Union Type`**
> OR 연산자(||) 처럼 'A이거나 B이다'를 정의하는 타입
```typescript
type Types = string | number;
let foo: Types;
foo = "Hello"; // 문자열 할당 가능
foo = 123; // 숫자 할당 가능
```
##### **`2. Intersection Type`**
> 합집합처럼 여러개의 타입을 모두 만족하도록 하나로 합칠 수 있다.
```typescript
interface Person {
  name: string;
  age: number;
}

interface Job {
  name: string;
  job: string;
}

type Manager = Person & Job;

// 결과
{
  name: string;
  age: number;
  job: string
}
```
<br/>

#### 2-4 Optional Parameter
> 함수 호출 시 매개변수, 인터페이스를 사용할 때 정의 된 속성을 생략 할 수 있다. 또한 정의되어 있지 않은 속성에 대해 인지할 수 있다.

```typescript
function foo(x: number, y?: number) {
  console.log(`x: ${x}, y: ${y}`);
}

foo(10) // x: 10, y: undefined (매개변수 y 생략가능)

interface Person {
  name: string;
  age?: number;
}

const bar = {
  name: 'dongdong',
  age: 30,
};

console.log(bar.oo); // 오류
```