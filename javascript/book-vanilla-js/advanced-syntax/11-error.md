# JavaScript - Error

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 에러 처리

- 프로그래밍 언어를 통해 코드를 작성할 땐 언어 자체가 가지는 구문에 따라 작성되고 실행되어져야 한다.
- 관련 언어 체계에 맞지 않는 구문을 사용하면 오류가 발생하며 이를 Error라 한다.
- 일반적으로 프로그래밍 언어에서는 이러한 에러를 처리하기 위해 다양한 구문 및 기능들을 제공한다.

> 여기서는 자바스크립트의 에러 처리와 관련된 try ... catch 문과 에러와 관련된 객체에 대하여 간단히 정리해본다.

---

## try ... catch 문

```js
try {
  try_statements
}
[catch (exception_var) {
  catch_statements
}]
[finally {
  finally_statements
}]
```

- 위 예제코드와 같이 try이 문은 try 블록, catch 블록, finally 블록으로 나눠 실행된다.
- try ... catch 구문을 사용하기 위해 try 블럭은 필수로 있어야 하며, catch 및 finally 는 선택 사항이다.

```js
try {
  noExistentFunction();
} catch (error) {
  console.log(error.name, ':', error.message);
} finally {
  console.log('Finally print');
}

/* Log result
ReferenceError : noExistentFunction is not defined
Finally print
*/
```

- try 블럭은 실제 실행되는 코드가 담기는 곳이다.
- catch 블럭은 try 구문에서 실행된 코드가 어떠한 오류로 인해 예외를 발생하게 되었을 때 처리하는 곳이다.
  - 자바스크립트에서 예외는 객체 형태로 관리되는데, try에서 발생한 예외에 대한 내용이 catch의 예외 변수(exception_var)에 전달되어 catch 블럭 내에서 처리가 가능하다.
- finally 블럭은 try나 catch의 처리와는 상관없이 마지막에 무조건 실행되는 코드를 작성하는 곳이다. 예외 발생 여부와 상관없이 처리된다.

---

## 오류의 유형

- 앞 서 catch 구문을 정리할 때 자바스크립트에서 예외는 객체 형태로 관리된다고 살펴보았다.
- 자바스크립트에서는 런타임 시(코드 실행 시) 오류가 발생했을 때 Error 객체를 생성한다.
- 구문 오류의 유형에 따라 다양한 에러가 존재하며 위 Error 객체를 기반으로 만들어져 있다.
- `Error()` 생성자 함수를 이용하여 사용자 정의 에러를 만들어 활용할 수도 있다.
- 오류의 유형
  - EvalError : 전역 함수 eval()에서 발생하는 오류 인스턴스
  - RangeError : 숫자 변수나 배열처럼 유효한 범위를 벗어난 경우 
  - ReferenceError : 정의되지 않은 변수, 함수 등 참조할 수 없는 경우
  - SyntaxError : eval() 코드를 분석하는 중 잘못된 구문이 있는 경우
  - TypeError : 요구되는 유효한 자료형이 아닌 경우
  - URIError : encodeURI()나 decodeURI() 함수에 적절하지 않은 인수를 제공한 경우
  - AggregateError : 하나의 동작이 여러개의 오류를 발생시키는 경우
  - InternalError : 엔진 내부에서 오류가 발생한 경우
- 관련 객체가 가지는 속성이나 메서드를 통해 오류의 내용을 좀 더 정확히 파악하고 관련 처리를 할 수 있다.(위 try 구문 예제코드 참고)

> 유형별 자세한 에러처리에 대한 내용은 모르지만 책과 MDN 내용을 참고하여 전체적으로 한번 정리. URI나 eval 등의 내용은 따로 찾아봐야 될 것 같다. 중요한 것은 에러가 객체 형태로 반환되며 에러 객체가 가지는 다양한 속성 및 메서드를 통해 에러의 내용을 확인하고 관련 처리를 할 수 있다는 것.

---

## throw

```js
try {
  throw "throwExceptionTest";
} catch (error) {
  console.log(error); // throwExceptionTest
  console.log(typeof error); // string
}
```

- 던져진다는 의미. 자바스크립트에서 에러를 일부러 발생시키기 위해 사용하는 구문으로 `throw`가 있다.
- 실행 로직에 있어 특정 조건(입력값의 변화 등)에 따라 추가적으로 발생할 수 있는 예외를 위해 throw로 던져주어 따로 처리가 가능하다. 또한 예상치 못한 사용자의 입력에 대비하여 강제적으로 예외를 발생시켜 실행 로직이 올바르게 작동하도록 환기시킬 수도 있다.
- `throw 표현식` 형태로 사용하며, 표현식의 결과값은 catch 구문에 전달되게 된다.

---

**참고 자료**

- [MDN - try ... catch](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/try...catch)
- [MDN - Error](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Error)
- [MDN - throw](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/throw)