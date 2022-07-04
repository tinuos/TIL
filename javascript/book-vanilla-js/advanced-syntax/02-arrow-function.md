# JavaScript - Arrow Function

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Arrow Function

- ES6에 추가된 기능으로, 함수 표현식을 간편하게 표현할 수 있는 문법이며 화살표 함수라고 부른다(사용하는 문법 형태가 화살표처럼 생겨 붙여진 이름같다).
- 자바스크립트의 전통적인 함수 표현식 방법을 간편하게 줄일 수 있다. 

### 기본적인 사용법

```js
const generalFunctionExpression = function(greeting, lang) {
  console.log(greeting, lang, "Function Expression!");
}
const arrowFunctionExpression = (greeting, lang) => {
  console.log(greeting, lang, "Arrow Expression!");
}

generalFunctionExpression("Hello,", "JavaScript");
arrowFunctionExpression("Hello,", "JavaScript");
```

- `() => {}` 형태로 사용하며, `()`에는 매개변수, `{}`에는 함수 실행 코드가 들어간다.

```js
const noParam = () => {
  console.log("No, Pramameters");
}
const oneParamOneReturn = txt => console.log(txt);
const returnObj = txt => ({objectKey : txt});

oneParamOneReturn("Hello, Arrow Function.");
console.log(returnObj("Hello"));
```

- 매개변수가 아예 없는 경우에는 `()`로 표기한다.
- 매개변수가 하나라면 `()`를 생략할 수 있다. 
- 함수 실행의 결과가 return 구문 하나일 경우 `{}`를 생략할 수 있다.
  - 이 경우 객체값은 `()`로 감싸줘야 한다. (화살표 구문으로 인식되지 않게 하기 위한 방법)

---

**참고 자료**

- [MDN - 화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)