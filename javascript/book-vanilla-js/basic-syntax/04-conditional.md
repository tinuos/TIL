# JavaScript - 조건문

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 조건문

- 프로그래밍 언어에서 기본적으로 특정 조건을 만족할 때 실행할 코드를 구분하여 작성할 수 있는 방법을 제공하는 데 이를 조건문이라 한다.
- 실행 순서를 변경하여 다른 명령을 처리할 수 있는 작업을 프로그래밍에선 보통 분기라 하는데 조건문을 통해 간단히 작성할 수 있다.

### if, else if, else 문

```js
if (조건식) {
  // 실행할 코드 작성
} else if (조건식) {
  // 실행할 코드 작성
} else {
  // 실행할 코드 작성
}
```

- 조건식을 만족하는 경우에만 해당 블록(`{}`)에 있는 코드 묶음을 실행한다.
- if 뒤에 조건식을 넣어 해당 조건식이 참일 경우에만 블록 내부의 코드를 실행한다.
- else if는 if나 다른 else if 문의 조건식이 거짓일 경우 다른 조건을 판별하고 실행하기 위해 넣는 구문으로 보통 여러 조건을 달리 처리해야 할 때 사용한다.
- else 는 앞 서 모든 조건식이 거짓일 경우 실행할 코드를 작성하는 문이다.
- if는 단독으로 사용할 수 있지만, else if와 else는 단독으로 쓰일 수 없다.
- 조건식의 결과값은 불린값이여야 판별할 수 있기 때문에 보통 비교 연산자나 논리 연산자를 많이 사용한다.

#### falsy

```js
if (false) {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - false");
}

if (undefined) {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - undefined");
}

if (null) {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - null");
}

if (0) {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - 0");
}

if (NaN) {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - NaN");
}

if ("") {
  console.log("조건식의 결과가 참일 경우 실행");
} else {
  console.log("조건식의 결과가 거짓일 경우 실행 - 빈 문자열");
}
```

- JS에서는 비교 연산자나 논리 연산자 등의 연산 없이도 조건식(불리언 값이 기대되는 문맥)에서 어떠한 특정한 값에 대해 불린값으로 취급할 수 있다.
- 참으로 평가될 수 있는 값은 **truthy(참 같은 값)**, 거짓으로 평가될 수 있는 값은 **falsy(거짓 같은 값)** 라고 불린다.
- falsy로 취급될 수 있는 값은 다음과 같다.
  - `false`
  - `undefined`
  - `null`
  - `0`
  - `NaN`
  - 빈 문자열 - `'', ""`
- 위 falsy를 제외한 다른 값은 truthy로 평가된다.
- 예제코드는 if 조건식이 모두 falsy 이기 때문에 else에 있는 문자열이 출력된다.

### switch 문

```js
switch (표현식) {
  case case1value:
    //실행 코드
    break;
  case case1value:
    //실행 코드
    break;
  case case1value:
    //실행 코드
    break;
  // ...
  default:
    //실행 코드
}
```

- js에서 또 다른 조건문 중 하나
- 표현식의 값과 블록 내부의 case의 값이 일치하는 경우에만 실행 가능한 구문
- 여기서 case 값이 일치하는 경우 실행 구문 맨 마지막 줄에 `break`를 명시해야 중지할 수 있다. `break` 가 없을 경우 다음에 작성된 모든 case 문 및 default 값을 실행하기 때문.
- `default` 문은 어떠한 case 값도 일치하지 않는 경우 실행할 코드를 작성한다. (if문의 else와 유사)
- default를 다른 case 절 사이나 맨 처음에도 작성할 수 있지만 그럴 경우 case를 만족하는 경우가 없으면 default 뒤에 break가 없는 모든 case를 실행해버리게 된다. 따라서 default 절은 일반적으로 맨 마지막에 사용하고 break를 생략하여 실행 후 코드 블력이 끝나면 자동 종료되도록 작성한다.
- 숫자나 문자열, 특정 문자 같은 상수값을 통해 분기하고 싶은 경우 많이 활용

> if문의 경우 해당 조건을 만족하는 조건식을 찾기 위해 위에서부터 순차적으로 비교 연산이 이루어지는 비효율성이 있다고 책에서 설명하고 있다. 이에 비해 switch 문의 경우 표현식의 값을 통해 case에 바로 접근하기 때문에 if문 보다 효율성이 좋을 수 있다고 한다. 범위를 통한 비교 조건이 필요한 경우에는 if문을, 단순히 상수로만 비교 가능할 경우에는 switch문을 사용

---

**참고 자료**

- [MDN - 참 같은 값](https://developer.mozilla.org/ko/docs/Glossary/Truthy)
- [MDN - 거짓같은 값](https://developer.mozilla.org/ko/docs/Glossary/Falsy)
- [MDN - switch](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/switch)

