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

### Unicode

### CORS란?