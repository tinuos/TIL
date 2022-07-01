# JavaScript - this 와 Scope(범위) 기본 내용

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## this

- this 키워드를 이용하면 바인딩된 객체를 참조할 수 있다.
- this는 함수가 호출되는 패턴에 따라 각기 다른 값을 참조할 수 있다.
- this가 참조하는 값을 이해하기 위해서는 자바스크립트의 실행 컨텍스트 개념을 이해해야 한다. 참고하는 책에서는 실행 컨텍스트의 내용이 나와있지 않아 [poiemaweb 사이트의 내용](https://poiemaweb.com/js-execution-context)을 참고하여 간단하게만 정리해본다.

### 실행 컨텍스트

- Execution Context
- 자바스크립트에서 실행 컨텍스트는 실행 코드를 형상화하고 구분하는 추상적인 개념이라고 설명하고 있다. 코드에 따라 가질 수 있는 컨텍스트는 아래와 같이 3가지로 구분된다.
  - 전역 범위의 코드 - 가장 바깥에 존재하는 코드
  - eval()로 실행되는 코드
  - 함수 내에서 실행되는 코드
- 즉, 실행 컨텍스트란 자바스크립트 엔진 내부에서 실행 가능한 코드가 실행될 수 있는 프로그램 환경을 의미
- 코드가 실행되기 위해 필요한 정보들은 다음과 같다
  - 변수 - 전역, 지역, 매개, 객체의 속성
  - 함수 선언
  - 변수의 유효범위
  - this
- 실행 컨텍스트는 위와 같이 코드 실행에 필요한 정보들을 객체 형태로 관리하며, 자바스크립트 엔진은 이를 스택(LIFO) 형태로 실행한다.
- 실행 컨텍스트가 객체로서 관리될 때 아래와 같이 3가지 속성을 소유한다.
  - Variable object
  - Scope chain
  - `this Value`
- 여기서 this 가 갖는 값은 **함수가 호출한 패턴**에 따라 달라진다.

> 실행 컨텍스트와 관련된 자세한 내용은 추후에 따로 정리하기. 일단 자바스크립트 내에서 실행되는 코드가 있는 경우 객체 형태의 컨텍스트로 관리되며, 스택 구조로 쌓여 순차적으로 실행된다는 것으로 간단히 이해하고 넘어간다. 

### 함수 호출 방식에 따른 this의 값

- 함수가 호출 되는 방식에 따라 this에 바인딩할 객체가 동적으로 정해진다.
  - 여기서 바인딩(binding)은 사전 의미 그대로 묶는다라는 뜻으로 대상을 참조한다라고 이해하고 학습을 진행했다.

```js
var testValue = 1;

console.log(testValue); // 1
console.log(window.testValue); // 1 : var 변수 키워드 경우만 확인 가능
// console.log(global.testValue);
function testFunc() {
  console.log(this); // window or global
  function innerFunc() {
    console.log(this); // window or global
  }
  innerFunc();
}

var num = 10000;

var testObj = {
  num: 1,
  objMethod: function() {
    console.log(this); // testObj
    console.log(this.num); // testObj.num === 1;
    function innerFunc() {
      console.log(this); // window
      console.log(this.num) // 10000
    }
    innerFunc();
  }
}

testFunc();

testObj.objMethod();
```

- 전역 범위 관련
  - 전역에서 함수나 변수를 선언하면 기본적으로 전역 객체에 바인딩 된다.
    - 브라우저는 `window`, 노드는 `global`
  - **전역 함수, 내부 함수, 객체 메서드의 내부 함수, 콜백 함수 모두 전역객체에 바인딩된다.**
- 메서드 호출 관련
  - 객체 내부에 작성된 함수를 호출하는 경우 해당 함수 내부에 작성된 this는 호출되는 객체를 가리킨다.

### DOM 요소에 this가 바인딩되는 경우

```html
  <button type="button" onclick="buttonClick(this);">클릭 버튼</button>
  <script>
    function buttonClick(object) {
      console.log(object);
    }
  </script>
```

![image](https://user-images.githubusercontent.com/104971437/176869008-9f0503e6-5cb6-49e9-a4d2-c8232f198384.png)

- HTML 요소에서 이벤트 발생(onclick 등) 시 함수 파라미터로 **this** 전달 시 해당 this는 요소 그 자체가 된다.
  - cosole.dir 로 확인하면 HTML DOM 요소가 가지는 정보를 모두 확인할 수 있다.

> 실행 컨텍스트와 내용을 잘 모른 상태에서 정리하려니 너무 어려웠다. this는 위 내용이 정말 기본적인 내용... JS 엔진이 자동으로 하는 바인딩을 수동으로 하는 방법(call, apply, bind 호출), 생성자 함수에서의 this 바인딩 등등 자바스크립트의 처리 방법과 연관되어 정말 다양한 결과가 나올 수 있는 내용이 많다. 일단 여기서는 전역 바인딩과 객체 내의 메서드에서 this 바인딩, 그리고 DOM 요소 이벤트와 관련하여 바인딩되는 방법만 이해하고 넘어가기로 결정. this 및 실행 컨텍스트에 대한 자세한 내용도 따로 정리해야겠다. 📝

---

## Scope 개념

```js
const testGlobalScopeString = "Hello!!!";

function testScopefunc() {
  const testLocalScopeString = "JavaScript";

  console.log(testLocalScopeString); // "JavaScript"
  console.log(testGlobalScopeString); // "Hello!!!"
}

testScopefunc();
console.dir(testScopefunc);
```

![image](https://user-images.githubusercontent.com/104971437/176922568-81308a0b-90c7-4f42-8bd5-580aa9fe9ec9.png)

- 선언된 변수가 가지는 범위(접근성)에 대한 개념
- local scope (지역 범위)
  - 함수 내부에서 생성된 변수는 함수 안에서만 참조 가능 (밖에서는 참조할 수 없다)
- global scope (전역 범위)
  - 함수 밖 전역에서 선언된 변수는 함수 안에서도 참조 가능
- 앞 서 실행 컨텍스트는 객체 형태로 관리되며 코드 실행을 위해 가질 수 있는 속성 중 scope가 있다는 것을 알아보았다. 위 코드 예제에서 선언된 함수를 console.dir로 확인했을 때 scope에 전역에 생성된 변수와 값을 확인할 수 있다.

### Scope 관련 추가 내용

- 책에서는 코드로만 전역과 지역 스코프를 설명하고 있어 W3schools 내용을 참고하여 좀 더 정리...😭
- ES6(2015) 버전 이후 scope 의 종류
  - Global Scope
  - Function Scope
  - `Block Scope` (ES6에 추가)
- Block Scope
  - 블럭 스코프(범위)
  - `{}` 내에서만 스코프를 가지는 것
  - `let`과 `const` 키워드가 추가되면서 생긴 스코프 개념
  - let과 const 이전 변수를 생성하기 위해 사용하던 **var**은 블럭 스코프를 가지지 않기 때문에 `{}` 외부에서도 블럭 내부에 있는 var 변수에 접근할 수 있다.
- Function Scope
  - 자바스크립트에서 선언된 함수 내부에서는 함수 스코프가 적용된다.
  - 함수 내부에 선언된 변수는 외부에서 접근 불가능하다. (var, const, let 모두)

---

**참고 자료**

- [MDN - JavaScript 참고서 : this](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this)
- [Poiemaweb - 실행 컨텍스트](https://poiemaweb.com/js-execution-context)
- [Poiemaweb - this](https://poiemaweb.com/js-this#%ED%95%A8%EC%88%98-%ED%98%B8%EC%B6%9C-%EB%B0%A9%EC%8B%9D%EA%B3%BC-this-%EB%B0%94%EC%9D%B8%EB%94%A9)
- [W3schools - JS Scope](https://www.w3schools.com/js/js_scope.asp)