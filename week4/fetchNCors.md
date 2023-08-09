# Fetch API & CORS

## keyword

- Fetch API란?
- Promise
- ReableStream
- Unicode
- CORS란?

### Fetch API란?

> 과거 클라이언트 사이드에선 XMLHttpRequest 객체를 이용해 페이지의 새로고침 없이(새로고침으로 인한 화이트 스크린 억제) 서버로 비동기 요청을 보냈었지만, Fetch API를 통해 보다 강력하고 유연한 데이터 통신을 제공한다.
> Promise 기반의 비동기 코드 작성을 통해 더 깔끔하고 간결한 코드를 작성할 수 있다.

### Promise

**`Event Loop`**

> 자바스크립트는 싱글 쓰레드 기반 언어로 단일 콜스택을 가지고 있어 한 번에 하나의 작업만을 처리할 수 있다. 그럼에도 동시에 여러가지 작업을 처리할 수 있는 이유는 **이벤트 루프**를 통해 비동기 방식으로 작업의 동시성을 보장하며 이는 자바스크립트 런타임인 브라우저 또는 Node.js가 담당한다. 이러한 비동기 작업은 callback 함수를 통해 Node.js나 Web API에 전달하는데 작업이 끝난 순서대로 callback 함수를 태스크 큐에 전달하며 이벤트 루프는 콜 스택이 비워져있다면 태스크 큐의 첫번째 함수를 꺼내 콜 스택에 추가한다.

**`Callback Hell`**

> Callback을 이용한 비동기 작업은 처리 순서를 보장하지 않기 때문에 동기적인 수행을 위해선 Callback을 중첩해서 사용하게 되는데 이는 프로그램을 복잡하게 만들고 유지보수를 어렵게 한다.

**`Promsie`**

> Promise는 Javascript에서 비동기 작업을 처리하기 위한 객체로 동기적 수행을 하기 위해 중첩된 콜백 지옥을 **`.then()`** 체이닝을 통해 해결할 수 있다.
> Promise를 사용하는 비동기 함수는 Promise 객체를 반환한다.

- Promise 객체는 (resolve, reject)를 파라미터로 하는 Callback 함수로 생성한다.
- **pending, fulfilled, rejected** 3가지 상태를 가진다. 
  - Promise 객체의 초기 상태는 pending
  - resolve 호출 -> fulfilled
  - reject 호출 -> rejected
- Promise.then() 함수로 fulfilled, rejected 상태에 대한 callback을 등록하고 사용할 수 있다.
- Promise.catch() 함수로 rejected 상태에 대한 callback을 등록하고 사용할 수 있다.
- 동작이 수행(fulfilled)되면 resolve 함수를, 취소(rejected)되면 reject함수로 결과를 반환한다.

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { message: "Data fetched successfully" };
      resolve(data);
    }, 1000);
  });
}

fetchData()
  .then(result => {
    // result = { message: "Data fetched successfully" }
    console.log("First .then() result:", result);
    return "Additional data";
  })
  .then(data => {
    // data = Additional data
    console.log("Second .then() data:", data);
    return 42;
  })
  .then(value => {
    // value = 42
    console.log("Third .then() value:", value);
  });
```

> 각 **`.then()`** **`.catch()`** 함수는 Promise 객체를 반환하기 때문에 함수 체이닝이 가능하다.

### ReadableStream

> 정리하자면 ReadableStream은 웹 플랫폼에서 사용되는 Streams API로 대용량의 데이터를 작은 조각(chunk)로 나누어 전송한다. 그래서 필요한만큼 데이터를 순차적으로 읽을 수 있어 메모리를 효율적으로 관리할 수 있다. 스트리밍이란 단어를 보니 UDP가 떠오르는데 빠르고 가볍게 데이터를 전송하는 전송 계층 프로토콜이 떠오른다. 가볍다라는 유사성이 보이긴 하지만, 두 개념의 직접적인 연관성은 딱히 없어보인다.

**`stream`**

> 스트림은 데이터를 작은 청크(chunk)로 나누어 처리하는 방식을 말한다.

### Unicode

**`문자 인코딩`**

> 컴퓨터는 0과 1로 이루어진 Binary(이진) 데이터를 처리하므로, 문자를 컴퓨터가 이용할 수 있는 바이너리 신호로 변환하여 저장하고 전송한다. 이 신호를 입력하는 인코딩과 문자를 해독하는 디코딩을 하기 위해서 미리 정해진 기준을 바탕으로 수행되어야 하는데, 이를 문자열 세트, 문자셋이라고 한다.

**`ASCII(아스키) 코드`**

> 아스키 코드는 초기 보급형 컴퓨터의 문자열 세트로
> 아스키 코드는 7bit로 구성되어 있으며, 0부터 127까지 총 128개의 문자(알파벳, 숫자, 특수 문자 등)를 나타내는 문자 인코딩이다.

**`Unicode`**

> 아스키 코드는 알파벳과 숫자만을 다룰 수 있기 때문에 다양한 언어와 문자 체계를 표현하기에 한계가 있어 표준 문자셋이 필요해졌고, 이후 전 세계의 모든 문자와 기호를 표현하기 위한 국제 표준 문자 인코드 방식인 유니코드가 개발되었다.

**`URL Encoding`**

> URL은 아스키 코드의 문자 집합만 사용할 수 있어, 한글과 같은 문자열을 URL에 삽입할 경우 URL Encoding으로 아스키 형태로 변환한다.

### CORS란?