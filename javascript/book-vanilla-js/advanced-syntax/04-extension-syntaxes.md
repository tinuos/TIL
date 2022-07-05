# JavaScript - 추가 구문들

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

- 5.7, 5.8, 5.9, 5.10 내용을 한 문서 안에서 정리
  - Object Literal Syntax Extension
  - Spread Operator
  - Object Destructuring
  - Array Destructuring

---

## Object Literal Syntax Extension

- 객체 생성 관련 리터럴 방식의 확장
  - 리터럴(literal)은 소스 코드에서 코드의 고정된 값을 대표하는 용어를 뜻한다. JS를 예로 들자면 문자열 리터럴은 `"`, `'`, 템플릿 리터럴(백틱) 등이고, 숫자는 일반 숫자 문자, 배열 객체는 `[]` 등을 사용하는 것.
- JS에서 객체 관련 리터럴 방식은 `{}` 안에 키-값 형태로 데이터를 생성한다.
- ES6에서는 객체 리터럴과 관련하여 몇가지 구문이 추가되었다. (아래 코드 참고)
  - 프로퍼티 약식 : 프로퍼티 명과 변수명이 같을 경우 변수명만 표기할 수 있다.
  - 메서드 약식 : 함수표현식의 function 키워드를 생략할 수 있다.
  - 계산된 프로퍼티 명 : 변수가 가지는 값을 키값으로 활용할 수 있다.(`[]`안에 변수명 기입)

```js
let personName = "gildong";
let personAge = 19;
let personAddress = "seoul";
let addressKey = "personAddress";

// 기존 방식
const testObj = {
  personName: personName,
  personAge: personAge,
  personAddress: personAddress,
  sayHello: function(text) {
    console.log(text);
  }
}

console.log(testObj);
/*
{
  personName: 'gildong',
  personAge: 19,
  personAddress: 'seoul',
  sayHello: [Function: sayHello]
}
*/

// ES6 object literal extension
const testObjByES6Syntax = {
  // 프로퍼티 약식
  personName,
  personAge,
  // 계산된 프로퍼티
  [addressKey]: personAddress,
  // 메서드 약식
  sayHello(text) {
    console.log(text);
  }
};

console.log(testObjByES6Syntax);
/*
{
  personName: 'gildong',
  personAge: 19,
  personAddress: 'seoul',
  sayHello: [Function: sayHello]
}
*/
```

---

## Spread Operator

```js
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [6, 7, 8, 9, 10];
const arr3 = [...arr1, ...arr2];

const text = "JavaScript";
const textArr = [...text];

console.log(arr3); // [ 1, 2, 3, 4,  5, 6, 7, 8, 9, 10 ]
console.log(textArr); // [ 'J', 'a', 'v', 'a', 'S', 'c', 'r', 'i', 'p', 't' ]
```

- 전개 연산자, 전개 구문이라고 불린다.
- 배열이나 문자열과 같이 반복가능한 데이터의 요소들을 하나하나 분해해서 활용할 수 있는 구문

---

## Destructuring

- 구조 분해 할당
- 배열의 요소나 객체의 속성을 분해하여 그 값을 변수에 개별적으로 담을 수 있게 하는 표현식
- 객체나 배열의 구조를 분해할 수 있다.
  - 배열 분해 할당은 할당 위치(좌변)에서 `[]`를 구조에 맞게 사용한다.
  - 객체 분해 할당은 할당 위치(좌변)에서 `{}`를 구조에 맞게 사용한다.

**배열 구조분해 할당**

```js
const [one, two, three, four, five] = [1, 2, 3, 4, 5];
const [one1, two1, three1] = [1, 2, 3, 4, 5];
const [one2, two2, three2, four2, five2, six2] = [1, 2, 3, 4, 5];
const [one3, two3, ...restArr] = [1, 2, 3, 4, 5];
// nested array
const [first, last, [age, address]] = ["Gildong", "Hong", [19, "Seoul"]];

console.log(one, two, three, four, five); // 1 2 3 4 5
console.log(one1, two1, three1); // 1 2 3
console.log(six2); // undefined
console.log(restArr); // [ 3, 4, 5 ];
console.log(first, last, age, address); // Gildong Hong 19 Seoul
```

- 예제 코드에서도 볼 수 있듯이 배열의 구조에 따라 분해하여 할당한다고 생각하면 이해하기 쉽다.
- 할당 변수의 개수가 기준이 되는 배열보다 적거나 많아도 오류가 발생하지 않는다. (많으면 undefined가 자동으로 할당되고, 적으면 해당 위치까지 요소만 할당됨을 확인)
- 또한 중첩되는 배열이 있는 경우에도 가능하다.
- 전개 연산자를 이용하면 나머지 요소들을 배열 데이터로 한번에 묶을 수 있다.(단, 마지막에만 사용해야 한다)

**객체 구조분해 할당**

```js
function returnObject() {
  return {
    firstName: "Gildong",
    lastName: "Hong",
    age: 19,
    address: "Seoul"
  }
}

console.log(returnObject()); // { firstName: 'Gildong', lastName: 'Hong', age: 19, address: 'Seoul' }

const {firstName, age} = returnObject();
console.log(`* ${firstName} *의 나이는 * ${age} * 입니다.`); // * Gildong *의 나이는 * 19 * 입니다.
```

---

**참고 자료**

- [MDN - 객체 초기자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Object_initializer)
- [위키백과 - 리터럴](https://ko.wikipedia.org/wiki/%EB%A6%AC%ED%84%B0%EB%9F%B4)
- [MDN - 전개 구문](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [MDN - 구조 분해 할당](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)