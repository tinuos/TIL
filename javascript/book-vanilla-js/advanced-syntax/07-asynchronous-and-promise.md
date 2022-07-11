# JavaScript - 비동기 처리와 Promise

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 동기와 비동기

## 동기 방식(synchronous)

- 동기식 처리를 간단히 설명하자면 순차적으로 코드의 실행이 이루어지는 것을 말한다.

```js
const btn = document.querySelector('button');

btn.addEventListener('click', () => {
  alert('버튼이 클릭되었습니다.');

  // alert 모달 창이 닫히기 전까지 아래 코드는 실행되지 않는다.
  const pElement = document.createElement('p');
  pElement.textContent = "Hello, JavaScript!!!!!";
  document.body.appendChild(pElement);
})
```

- 위 예제 코드는 MDN에 나온 것으로 alert 모달 창의 처리가 끝나기 전까지는 p 요소 추가와 관련된 코드가 실행되지 않는다. 
- 이처럼 위에서 아래로 코드가 순차적으로 실행되면서 처리되는 것을 동기식 처리라 부른다.

### 비동기식(Asynchronous)

- 비동기식 처리는 순차적으로 처리되는 동기식 처리와는 다르게 앞 선 작업의 완료 여부와는 상관없이 새로운 작업을 시작하는 처리 방식
- 동기식의 처리가 직렬적인 형태라면, 비동기 처리는 병렬적인 형태를 보이게 된다. 작업이 처리되는 시간에 따라 늦게 실행되었어도 먼저 끝나는 경우가 발생할 수 있다.
- 자바스크립트에서는 아래와 같은 비동기 처리 방법이 있다.
  - call back 함수 사용
  - Promise
  - async / await

### 자바스크립트 런타임 환경

![image](https://user-images.githubusercontent.com/104971437/177732323-e96fb324-083c-4b55-8588-bfaed082590b.png)

- 자바스크립트 엔진은 싱글스레드 기반이라고 한다. 싱글스레드는 한번에 하나의 작업만 처리할 수 있는 방식을 의미.
- 비동기 작업의 처리는 이벤트 루프를 통해 이루어진다.
- 여기서는 콜스택, 메모리 힙, 이벤트 큐, 이벤트 루프의 작동 원리에 대해서만 간단히 정리한 후 Promise 내용을 학습하려 한다.

#### 콜 스택

- 자바스크립트에서 함수들의 호출은 콜스택에 프레임 형태로 관리되고 실행된다.
- 함수를 호출 시에 지역변수, 인수 등을 포함하는 프레임이 콜 스택에 쌓인다.
- 스택 구조에 따라(LIFO) 맨 위에 쌓인 함수 프레임부터 순차적으로 실행되는 구조

#### 메모리 힙

- 힙에는 참조 데이터가 저장된다.

#### 이벤트 큐와 이벤트 루프

- 이벤트 큐에는 Callback 함수를 처리할 메시지가 저장되는 곳
- 이벤트 루프는 콜백 메시지가 도착할 때까지 동기적으로(무한으로) 대기하는 기능을 말한다. 이벤트 루프는 콜백 메시지가 존재할 때 콜스택이 비어있는지를 확인한 후 해당 메시지가 처리하는 함수가 실행될 수 있도록 콜스택에 보내주는 역할을 한다. (FIFO으로 처리된다)
- setTimeout()과 같이 Web API를 이용하는 함수가 실행될 때의 순서는 다음과 같다.
  - 콜스택에 setTimeout() 함수 프레임이 올라온다.
  - Web API 에게 setTimeout 작업의 처리를 요청하며 콜스택에서는 제거된다.
  - Web API는 setTimeout 작업을 수행하고 콜백 메시지를 큐에게 보낸다.
  - 메시지를 받은 큐는 콜스택이 비어있는지 확인하고 비어있다면 콜백 메시지에 지정된 함수를 콜스택에 올린다.
  - 콜스택에는 큐에서 받은 함수가 push 되어 실행되고 작업이 완료되면 제거된다.
- 위와 같은 과정에 의해 비동기 처리가 가능한 것.

---

## 콜백 함수

- callback. 다시 부른다는 의미.
- 함수의 인자로 함수를 전달하고 함수 선언내에서 전달받은 함수를 실행하는 것.
- 콜백함수는 동기 콜백, 비동기 콜백으로 나뉠 수 있다.
  - 동기 콜백의 경우 비동기 관련 로직 없이 전달받은 함수 인자를 그대로 실행하는 것. 앞서 살펴본 대로 이벤트 루프 등의 추가적인 처리가 없기 때문에 콜스택에 순서대로 쌓여 실행.
  - 비동기 콜백의 경우 비동기로 처리되는 로직(ex. setTimeout 등) 내에서 함수를 실행. 이벤트 루프를 거치기 때문에 비동기적 처리가 일어난다.
- 콜백 지옥
  - 콜백 함수를 연이어서 추가적인 처리를 하는 상황을 의미한다.
  - 콜백으로만 로직을 구성할 경우 가독성이 떨어짐은 물론이고, 유지보수에도 어려움을 겪을 수 있다.
- 위와 같은 문제로 인하여 비동기 관련 콜백 처리를 좀 더 간편하게 하기 위해 promise, async & awiat 등의 기능과 구문 등이 나오게 되었다.

---

## Promise

- 자바스크립트에서 비동기 처리를 하기위해 사용되는 객체
- promise 라는 단어 자체가 약속의 의미를 갖고 있다. Promise 객체는 비동기 작업의 처리를 수행한 이 후에 성공 또는 실패의 결과를 나타낼 수 있다.

> 책 내용보다는 드림코딩 유튜브 채널에 간단하게 정리되어 있는 영상이 있어 MDN과 같이 참고했다.

### Promise 개념 이해하기

- Promise는 비동기 처리와 관련된 특정 기능들을 수행하는 객체이다.
- Promise는 상태(state)라는 것을 가지며, 내용은 아래와 같다.
  - pending - 대기 상태. 객체 초기 상태(이행이나 거절이 되지 않은)
  - fulfilled - 이행 상태. 연산이 성공적으로 완료된 상태
  - rejected - 거부 상태. 연산이 실패한 상태
- Promise는 연산이 처리되고 난 후 성공이냐 실패에 따라 수행되는 로직을 달리할 수 있다.
  - 이행이 되었을 때는 `.then`, 거부되었을 때는 `.catch` 메서드를 사용한다. (아래 따로 정리하기)
- Producer vs Consumer 개념
  - 드림코딩 영상에서 정보 생산자와 정보 사용자란 개념으로 Promise 사용법을 쉽게 알려주기에 따로 정리해본다.
  - 정보 생산자는 Promise 생성자 함수를 이용하여 만든 Promise 객체, 정보 사용자는 생성한 promise 객체를 이용하여 해당 객체가 반환하는 것들을 사용하는 로직을 의미하며 then, catch, finally 등을 사용한다.

### Promise 사용하기

#### promise 객체 생성

```js
const promise = new Promise((resolve, reject) => {
  ... something asynchronous

    resolve(someValue)

  or

    reject("failure reason") 
})
```

- `new Promise(executor)`와 같은 형태로 promise 객체를 생성한다.
  - executor는 resolve 및 reject 인수를 전달할 실행함수를 말한다.
  - **promise 내부 구현에 따라 executor 함수는 promise 객체 생성 시 바로 실행된다.**
- resolve, reject 함수
  - 생성 시 인자로 설정하는 함수들
  - resolve는 비동기 작업을 성공적으로 완료하였을 때 결과값을 반환하기 위해 실행
  - reject는 비동기 작업이 실패했을 때 오류의 원인을 반환하기 위해 실행

### promise 상태 처리

```js
promise
  .then(value => {
    console.log(value);
  })
  .catch(error => {
    console.log(error);
  })
  .finally(() => {console.log('finally')});
```

- 객체가 생성됨가 동시에 실행함수가 실행되어 결과값들을 반환한다.
- 이 때 promise 객체과 then, catch, finally 등으로 성공 또는 실패시 반환 결과들을 처리할 수 있다.
  - then 메서드에는 콜백 함수 또는 다른 프로미스 객체가 들어가며 인자는 resolve에서 반환하는 값을 사용할 수 있다.
  - catch 메서드에는 콜백 함수가 들어가며 인자는 reject 에서 처리하는 값을 사용한다. (주로 Error 객체를 이용)
  - finally 는 이행 또는 거부와는 상관없이 항상 실행되는 로직을 사용할 때 활용한다.

### promise chaining

```js
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});

fetchNumber
  .then(num => num * 2) // 2
  .then(num => num * 3) // 6
  .then(num => {
    return new Promise((resolve, reject) => {
      setTimeout(() => resolve(num - 1), 1000); // 5
    });
  })
  .then(num => console.log(num)); // 5
```

- 사슬처럼 계속 연결되는 상태
- 앞 서 then은 resolve 반환값을 처리할 콜백함수 또는 프로미스 객체를 전달받을 수 있다고 하였다.
- 위 예제 코드는 드림코딩 영상에 나오는 코드로 위와 같은 then 메서드를 이용하면 이행 시 반환되는 값을 계속 연결하여 처리가 가능하다. 단, resolve에 대한 반환값이 반드시 있어야 가능하다.

### promise Error Handling

- catch 또한 then 처럼 사슬 형태로 연달아 사용 가능하다.
- catch는 then 에 대한 실행처리에 맞게 사용 가능(모든 이행에 대한 오류를 잡아낼 수 있다)

---

**참고 자료**

- [MDN - Introducing Asynchronous JavaScript](https://developer.mozilla.org/ko/docs/Learn/JavaScript/Asynchronous/Introducing)
- [MDN - 이벤트 루프](https://developer.mozilla.org/ko/docs/Web/JavaScript/EventLoop)
- https://velog.io/@change/JavaScript-asyncawait%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C
- https://hudi.blog/async-javascript/
- [드림코딩 - 콜백 영상](https://youtu.be/s1vpVCrT8f4)
- [드림코딩 - Promise 영상](https://www.youtube.com/watch?v=JB_yU6Oe2eE)
- [MDN - Using Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Using_promises)
- [MDN - Promise](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Promise)