# JavaScript - async, await 구문

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## async, await 구문

- async & await 는 비동기 처리와 관련하여 promise 방법보다 좀 더 간편하게 작성할 수 있는 구문이다.
- 해당 구문의 사용은 promise 기반에서 이뤄지기 때문에 promise 사용에 대한 이해가 선행되어야 한다.

### async function

```js
async function asyncFunc() {
  return 1;
}

console.log(asyncFunc()); // Promise {<fulfilled>: 1}
asyncFunc().then(console.log); // 1
```

- `async` 키워드를 함수 앞에 붙이면 비동기 함수로 정의된다.
- async 함수는 항상 프로미스를 반환하게 되어 있다.
  - 프로미스가 아닌 값이 반환되어도 프로미스로 감싸져서 반환되도록 처리된다.

### await keyword

- await는 async 함수 안에서만 사용 가능한 키워드이다.
- await 키워드를 만나면 프로미스가 처리될 때까지 기다린다.
- 처리 완료 후에는 결과에 따라 예외를 생성하거나 프로미스 객체의 결과값을 반환한다.

### 다양하게 활용하기

- 예외 처리
  - try ~ catch 를 통해 await에서 예외가 발생했을 때 에러처리를 할 수 있다.
- async 표현식
  - 일반 표현식에 async 키워드를 결합하여 사용.
  - 최상단에서 바로 await로 비동기 함수를 실행하고자 할 때 활용해볼 수 있다.
- Promise api 활용
  - Promise가 가지고 있는 api 중 all 메서드를 이용하여 모든 프로미스를 기다린 후에 처리할 수 있다. 이 때 처리할 프로미스들은 배열로 all 메서드에 전달하며, 결과값도 배열 형태로 반환한다.
  - race 메서드의 경우 비동기 처리 중 가장 먼저 완료된 프로미스만 반환한다.

---

**참고 자료**

- [드림코딩 async & await 영상](https://www.youtube.com/watch?v=aoQSOZfz3vQ)
- [모던 자바스크립트 - async & await](https://ko.javascript.info/async-await)