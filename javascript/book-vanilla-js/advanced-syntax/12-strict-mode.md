# JavaScript - 엄격 모드(Strict Mode)

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Strict Mode

- 의미 그대로 엄격한 모드
- 엄격 모드 개념을 알기 이전에 자바스크립트의 역사에 대한 간단한 이해가 필요
  - 자바스크립트는 웹 브라우저에서 유일하게 동작하는 프로그래밍 언어
  - 초창기에 구현된 구문 및 기능 등이 그대로 쓰이면서 버전이 업그레이드 될 때마다 새로운 기능이 추가되는 식으로 발전해왔다. (그러한 기능들로 동작하는 사이트들을 완전히 배제할 수 없기 때문에?)
  - 옛날 방식의 자바스크립트의 구문과 기능들을 사용하게 되면 개발자가 인식하지 못하는 영역에서 에러가 발생할 가능성이 있다(ex. 변수 선언자 미사용, 함수 내 this 바인딩 대상, 구문에 따른 자바스크립트 엔진의 암묵적 처리 등). 이러한 문제에 근본적으로 대처하고자 나온 것이 ES5의 strict mode(엄격 모드)라 할 수 있겠다.
- ES5에서 엄격 모드가 나오면서 스크립트는 strict 또는 non-strict로 구분하게 된다.

### 엄격모드 특징

- 스크립트에 엄격모드를 적용하면 자바스크립트의 제한된 버전을 선택하여 구문 사용을 제한하게 할 수 있다.
- 브라우저의 지원 여부에 따라 엄격모드의 코드 실행 결과가 예상한 것과 다를 수 있다.
- 하위 버전과의 호환성 문제가 발생할 수 있다.

### 엄격모드 사용

- 엄격모드는 전역으로 지정하거나 함수 내에서만 적용하도록 설정할 수 있다.

```js
'use strict';

a = 10; // ReferenceError: a is not defined

console.log(a);
```

- `"use strict"` 또는 `'use strict'`를 스크립트 최상단에 표기하면 스크립트 전역에 엄격 모드가 적용된다.

```js
function thisKeywordTest() {
  console.log(this);
}

thisKeywordTest(); // global or window
```

```js
function noStrictFunction() {
  console.log(this);
}
function InnerStrictFunction() {
  'use strict';
  console.log(this);
}

noStrictFunction(); // global 또는 window 전역객체
InnerStrictFunction(); // undefined
```

- `"use strict"` 또는 `'use strict'`를 함수 선언 내부의 상단에 표기하면 해당 함수와 내부 함수에 엄격 모드가 적용된다.

> 위 내용 외에 다양한 엄격모드 처리 내용은 MDN 참고

---

## 추가 내용

- 앞 서 모듈 내용을 살펴볼 때 모듈로 처리되는 스크립트는 항상 엄격모드로 실행된다고 학습했는데, 이는 따로 엄격모드를 표기하지 않아도 엄격모드로 실행된다는 의미이다.

---

**참고 자료**

- [Poiemaweb - strict mode](https://poiemaweb.com/js-strict-mode)
- [MDN - Strict Mode](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Strict_mode)