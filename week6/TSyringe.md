# TSyringe

External Store에 대한 강점을 보여주기 위한 강의인데, 한 번만 봐서는 이해가 잘 안됐다. 알고있지만 낯선 개념인 싱글톤 같은 것 때문인데
개념적으로 하나의 클래스에선 오직 하나의 인스턴스만 생성한다는 의미는 알고 있었지만, 코드에 패턴을 직접 적용하니 '엥 뭐지?' 라는 생각이 계속 들어 
이번 파트는 코드에 대한 이해를 완벽하게 흡수해야겠다.

## Keyword

- TSyringe
- 의존성 주입(Dependency Injection)
- reflect-metadata
- sington (싱글톤)

## 1. TSyringe

- Typescript용 의존성 주입 컨테이터 라이브러리
- 클래스, 함수 등의 의존성을 주입할 때 편리한 기능을 제공함.
- 코드의 가독성, 유지보수성, 테스트 용이성을 향상시킨다.

---

## 2. 의존성 주입(Dependency Injection)

- 의존성 주입은 컴포넌트(React 컴포넌트 아님, 프로그램 구성요소의 의미) 간의 결합을 최소화하고 코드를 모듈화하여 코드의 가독성, 유지보수성, 테스트 용이성을 향상시킨다.
- 클래스, 함수 등의 의존성 관리 로직을 외부로 분리하여 각 컴포넌트는 자신의 역할에만 집중할 수 있다.

> 의존성 주입이라고 하면 누가 의존하게 되는건지 헷갈리는 경우가 있다. 그래서 나는 극단적인 예시로 이해했는데,  
> 마약을 주사기로 나에게 주입하면 중독성으로 인해 나는 마약에 의존한다.

---

## 3. reflect-metadata

- metadata는 데이터를 위한 데이터를 의미하며 클래스, 프로퍼티, 메서드 등의 요소에 추가정보를 제공하는데 사용한다.
- reflect-metadata는 Typescript에서 데코레이터를 활용할 때 메타데이터를 지원하기 위한 라이브러리다.
- Typescript는 컴파일 타임에 타입 정보를 활용할 수 있지만, 런타임에는 정보를 얻기 어려워 reflect-metadata를 사용해 타입 정보를 런타임에 활용 가능하다.
- 주로 클래스나 프로퍼티에 메타데이터를 추가하고 읽어오는데 사용한다.

### 사용 예제

데코레이터(@)에 메타데이터를 추가한다.

**`클래스에 데코레이터에 메타데이터 추가`**

```typescript
import "reflect-metadata";

const MY_METADATA_KEY = "myMetadataKey";

function MyDecorator(data: any) {
  return Reflect.metadata(MY_METADATA_KEY, data);
}

@MyDecorator("Hello, metadata!")
class MyClass {
  // ...
}

const metadata = Reflect.getMetadata(MY_METADATA_KEY, MyClass);
console.log(metadata); // "Hello, metadata!"
```

**`메서드 데코레이터에 메타데이터 추가`**

```typescript
import "reflect-metadata";

const MY_METADATA_KEY = "myMetadataKey";

function MyDecorator(data: any) {
  return Reflect.metadata(MY_METADATA_KEY, data);
}

class MyClass {
  @MyDecorator("Hello, method metadata!")
  myMethod() {
    // ...
  }
}

const metadata = Reflect.getMetadata(MY_METADATA_KEY, MyClass.prototype, "myMethod");
console.log(metadata); // "Hello, method metadata!"
```

## 4. sington (싱글톤)

- 객체 지향 프로그래밍에서 사용되는 하나의 클래스는 오직 하나의 인스턴스만 생성하는 디자인 패턴
- 인스턴스가 오직 하나만 존재하며, 어디서든 동일한 인스턴스에 접근할 수 있고 공유 데이터를 사용할 수 있다.
- 전역적으로 사용해야 하는 설정, 데이터베이스 연결, 네트워크 연결 등의 공유 리소스를 관리할 때 주로 사용한다.

> 데이터베이스 연결 I/O 바운드 작업은 오버헤드가 큰 작업이라 싱클톤 패턴을 활용해 데이터베이스 연결을 미리 생성하여 커넥션 풀을 관리하는 것으로 알고있다.
