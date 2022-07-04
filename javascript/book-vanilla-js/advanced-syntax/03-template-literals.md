# JavaScript - Template litarals

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Template litarals

```js
const language = "JavaScript";

console.log('Hello ' + language);
console.log(`Hello ${language}`);

console.log(`Hello,
JavaScript
Template
Literals!!!`);
/*
Hello,
JavaScript
Template
Literals!!!
*/
```

- ES6에 추가된 구문으로 템플릿 리터럴이라 부른다.
- 기존 문자열 리터럴 생성과의 차이점
  - 기존에는 `"`나 `'`를 사용하지만, 템플릿 리터럴에선 \`(백틱) 기호를 사용한다.
  - 변수가 가지고 있는 데이터를 문자열로 연결하기 위해 기존에는 `+`를 사용했지만, 리터럴에서는 `${표현식}`을 이용하여 간편하게 추가할 수 있다. (보간법)
  - `"`, `'` 는 한 줄로 밖에 문자열을 표현할 수 없다(개행을 위해서는 개행문자 등을 따로 집어 넣는 방식). 템플릿 문자열의 경우 여러 줄 작성이 가능하다. (개행 문자를 인식하여 일부가 된다)

---

**참고 자료**

- [MDN - Template literals](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)