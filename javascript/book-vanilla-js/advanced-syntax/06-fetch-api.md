# JavaScript - Fetch API

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Fetch API

- fetch는 가지고 오다라는 의미를 가지고 있다.
- MDN에선 fetch api를 네트워크 통신을 포함한 리소스 취득을 위한 인터페이스라고 소개하고 있다.
- 앞 서 배운 XMLHttpRequest와 같이 서버와 통신한다는 것은 유사하지만, fetch의 경우 promise를 반환하여 사용한다는 차이점이 있다. (promise에 대해서는 다음에 정리)
- fetch는 전역 함수 fetch()를 이용하여 사용할 수 있다.
- fetch 기능 내부에는 HTTP 통신에 필요한 요청과 응답에 대한 정의가 객체 형태로 포함되어 있다(각각 Request, Response).

> 여기서는 fetch 에 대한 기본 사용법을 알아보고 실습 내용을 통해 HTTP 메서드별 작동원리만 정리해보려 한다. 실습은 XHR와 같이 jsonplaceholder 사이트를 활용한다.

### 요청(GET)

```js
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then((response) => response.json())
  .then((json) => console.log(json));
```

- fetch 함수 `fetch(resource[, init])` 를 통해 요청한다.
  - resource는 가져오길 원하는 자우리소스의 URL이나 Request 객체를 전달한다.(일반적으로 URL을 사용)
  - init은 요청을 초기화하기 위해 전달하는 함수이다(옵션). GET 방식 요청은 두번째 인자를 전달하지 않아도 된다. init에는 HTTP 요청 방식(method, headers, body 등)과 관련된 속성들을 객체로 담아 전달해야 한다.
- fetch에선 GET 요청을 할 때 따로 HTTP 요청 방법을 명시하지 않아도 된다. (따로 `GET`을 명시할 필요가 없다는 뜻)
- `.then()`
  - Promise 방식에서 성공 또는 실패의 결과를 처리하기 위한 함수이다. (Promise.prototype.then())
  - 2개의 콜백함수를 인수로 받을 수 있는데 하나는 수행되었을 때,(onFulfiled) 다른 하나는 거절되었을 때(onRejected) 처리할 로직이 들어간다.
  - 위 fetch 예제에서는 하나의 콜백함수만 인자로 들어간 것을 확인할 수 있다.(response 부분)
  - then 함수 내에서 처리한 반환값(Promise)으로 또 다른 then 함수를 연결하여 사용할 수 있다(promise의 연장). 앞 선 then의 결과에 따라 콜백함수를 전달하여 또 다른 처리가 가능한 것.
  - fetch()가 반환하는 값은 fecth 내부에 정의된 Response 객체를 이용한 Promise 객체이기 때문에 가능하다. (내부적으로 반환값을 response 객체로 정의??)
  - 반환된 response 객체 내 있는 응답 본문에 있는 내용을 json 으로 파싱하기 위해 Response에 정의된.json() 함수를 이용한다. 이 함수 역시 또 다른 Promise를 반환하기 때문에 추가적으로 then()를 사용할 수 있다. 

### 생성(POST)

```js
fetch('https://jsonplaceholder.typicode.com/posts', {
  method: 'POST',
  body: JSON.stringify({
    title: 'gildong',
    body: 'HAHAHA',
    userId: 1,
  }),
  headers: {
    'content-type': 'application/json; charset=UTF-8',
  },
})
  .then((response) => response.json())
  .then((json) => console.log(json));
```

- GET을 제외한 다른 방식에서는 앞 서 살펴보았듯이 fetch의 2번째 인자로 HTTP 전송 방식에 대한 내용이 들어간 객체를 전달해야 한다.
- 위 예제 코드에선 HTTP 전송 방식과 관련된 속성 중 method, body, header 를 설정한 객체를 전달
- body(요청 메시지 본문)에서는 JSON.stringify를 이용하여 json 포맷의 문자열을 전달.
- header 에서는 미디어 타입과 문자셋 정보를 담아 보내주는 예제이다.
- 이 외에 수정이나 삭제 등의 메서드는 method 속성을 관련 메서드(PUT, DELETE 등)로 바꿔주면 되서 따로 정리하진 않으려 한다.
- 중요한 것은 fetch api를 사용하면서 서버에서 지정한 형식대로 요청 방식을 기입하는 것이 중요.

---

## 파일 업로드 관련 FormData 객체 사용하기

- 책에서 FormData 객체를 이용하여 fetch로 파일을 업로드 하는 내용이 있어 따로 간략히만 정리해본다.

### FormData

- HTML의 form 태그에 해당하는 from 필드와 그 값을 나타내는 일련의 key-value 쌍을 쉽게 생성해주는 객체
- querySelector 등으로 폼 필드의 요소를 선택한 변수에 FormData 객체의 append 메서드를 통해 쉽게 업로드된 파일에 대한 내용을 쉽게 저장할 수 있다.
- FormData가 객체이기 때문에 fetch에서 body 설정 시 해당 객체만 전달하면 쉽게 서버로 사용자가 업로드한 파일 정보를 보낼 수 있다. 

---

**참고 자료**

- [MDN - Fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API)
- [MDN - Fetch 사용하기](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API/Using_Fetch)
- [jsonplaceholder](https://jsonplaceholder.typicode.com/guide/)
- [MDN - FormData](https://developer.mozilla.org/ko/docs/Web/API/FormData)