# JavaScript - 함수와 파라미터(Parameter)

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 함수의 파라미터에서 기본값 사용하기

```js
function parameterTestFunc(a, b) {
  console.log(a, ':', typeof a); 
  console.log(b, ':', typeof b); 

  return a + b;
}

console.log(parameterTestFunc(1, 2));
/*
1 : number
2 : number
3
*/
console.log(parameterTestFunc());
/*
undefined : undefined
undefined : undefined
NaN
*/
```

- 파라미터는 매개 변수를 의미. 매개 변수는 변수의 특별한 한 종류. 함수 등의 작은 프로그램 내에서(서브 루틴) 입력값으로 활용할 수 있는 데이터를 받기 위한 하나의 기능이라고 보면 된다. 매개 변수에 전달되는 데이터는 인자(argument) 라고 부른다.
- 보통 함수 정의 시 매개변수를 같이 설정하여 내부에서 활용하는 방식으로 사용한다.
- 자바스크립트에서는 함수 호출 시 함수에 정의된 파라미터에 전달할 인자를 지정하지 않으면 **자동으로 해당 파라미터에 undefined 값을 할당한다.**
- 매개 변수가 함수 내부 로직에서 필수값이어야 한다면 기본값을 설정해 놓는게 좋다. 변수에 값을 할당하는 것처럼 함수 정의 시 매개변수에 `=`를 이용하여 기본값을 설정할 수 있다. - 아래 코드 참고

```js
function sendMessage(message = "text가 전달되지 않았습니다.") {
  console.log(message);
}

sendMessage("Hello JavaScript"); // Hello JavaScript
sendMessage(); // text가 전달되지 않았습니다.
```

---

## Rest 파라미터

```js
function generalParamFunc(a, b) {
  console.log(a + b);
}
function restParamFunc(a, ...b ) {
  const sumResult = b.reduce(function(acc, element) {
    return acc  + element;
  }, a);
  
  console.log(sumResult);
  console.log(a, typeof a, '/', b, typeof b);
}

generalParamFunc(1, 2); // 3
generalParamFunc(1); // NaN

restParamFunc(1); // 1  // 1 number / [] object
restParamFunc(1, 2); // 3  // 1 number / [ 2 ] object
restParamFunc(1, 2, 3, 4, 5); // 15  // 1 number / [ 2, 3, 4, 5 ] object
```

- 함수 정의 시 파라미터의 개수를 미리 지정해 놓으면 호출 시에 지정된 개수 만큼 인자를 전달해야 내부에서 문제가 발생하지 않는다.
- 정해지지 않은 파라미터의 개수를 처리하기 위해 나머지 파라미터(es6)를 사용할 수 있다. (가변항 함수)
- 나머지 파라미터는 매개변수를 처리하는 자리에 `...파라미터명` 으로 표기하는 방식이다. 사용에는 아래와 같은 조건이 붙는다.
  - 나머지 파라미터는 여러개 일 수 없다.
  - 기본 파라미터와 동시에 사용되는 경우 제일 마지막에 위치하여야 한다.
- 함수 호출 시 전달되는 인자들은 나머지 파라미터명으로 된 배열(Array) 객체에 순서대로 들어가게 되며, Array와 관련된 속성과 메서드를 사용할 수 있게 된다.

### 함수 arguments 와 나머지 파라미터의 차이점

```js
function checkArgumentsObj() {
  console.log(arguments);
  console.log(Object.prototype.toString.call(arguments));
}

checkArgumentsObj(1, 2, 3, 4, 5);
// [Arguments] { '0': 1, '1': 2, '2': 3, '3': 4, '4': 5 }
// [object Arguments]

console.log(Object.prototype.toString.call([]));
// [object Array]
```

- 자바스크립트의 모든 함수는 arguments라는 지역변수를 가지며 이를 활용할 수 있다.
- arguments는 호출된 함수가 가지는 모든 인수를 참조하며, 각각의 인수에 대하여 인덱스를 가진다.
- arguments는 length만을 갖는 하나의 객체로 Array가 아니다. (유사배열 객체) 따라서, Array와 관련된 메서드 등을 활용할 수 없다.
- 나머지 파라미터는 ES6에 추가된 함수의 기능으로 가변 인자를 좀 더 효율적으로 다루기 위해 만들어진 것이라 생각하면 된다.
- arguments 내에 인수 정보를 가변 인수 형식으로 활용하기 위해서는 `Array.from(arguments)` 나 전개 연산자(spread) 등을 통해 배열 데이터로 변환한 뒤 사용하면 된다. (아래 코드 내용 참고)

```js
function convertArgumentsData() {
  const argsArr = Array.from(arguments);
  // or 
  // const argsArr = [...arguments];
}
```

---

**참고 자료**

- [위키백과 - 매개변수](https://ko.wikipedia.org/wiki/%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))
- [MDN - 나머지 매개변수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/rest_parameters)
- [MDN - arguments 객체](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/arguments)