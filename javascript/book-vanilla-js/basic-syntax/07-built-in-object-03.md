# JavaScript - 내장 객체 03

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 내장 객체

- JS 엔진 내부에 전역 범위에 존재하는 표준 내장객체에 대해 학습
  - 내장 객체가 가지는 다양한 함수를 사용하여 특정 데이터 타입이나 처리 로직에 따라 활용 가능
- [MDN 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)에서 항목별 표준 내장 객체에 대하여 살펴볼 수 있다.
- 여기서는 참고하는 책 기준으로 간단하게만 학습하고 정리할 예정.

---

### JSON 객체

```js
const testNum = 1000;
const testString = "Hello, JavaScript!";
const testBoolean = true;
const testArray = [1, 2, 3, 4, 5];
const testObj = {
  name: "gildong",
  age : 19,
  address: "seoul"
}

// JSON.stringify()

const numDataStringifyByJSON = JSON.stringify(testNum);
const stringDataStringifyByJSON = JSON.stringify(testString);
const booleanDataStringifyByJSON = JSON.stringify(testBoolean);
const arrayDataStringifyByJSON = JSON.stringify(testArray);
const objectDataStringifyByJSON = JSON.stringify(testObj);

console.log(numDataStringifyByJSON);
console.log(stringDataStringifyByJSON);
console.log(booleanDataStringifyByJSON);
console.log(arrayDataStringifyByJSON);
console.log(objectDataStringifyByJSON);

/*
1000
"Hello, JavaScript!"
true
[1,2,3,4,5]
{"name":"gildong","age":19,"address":"seoul"}
*/

// JSON.parse()
// 앞 서 변환된 문자열 데이터 활용
function JSONparseInfoPrint(text) {
  const parseData = JSON.parse(text);
  return console.log(parseData, ':', typeof parseData);
}

JSONparseInfoPrint(numDataStringifyByJSON);
JSONparseInfoPrint(stringDataStringifyByJSON);
JSONparseInfoPrint(booleanDataStringifyByJSON);
JSONparseInfoPrint(arrayDataStringifyByJSON);
JSONparseInfoPrint(objectDataStringifyByJSON);

/*
1000 : number
Hello, JavaScript! : string
true : boolean
[ 1, 2, 3, 4, 5 ] : object
{ name: 'gildong', age: 19, address: 'seoul' } : object
*/
```

- JavaScript Object Notation
- `키-값` 쌍으로 이루어진 데이터 객체를 전달하는 데이터 포맷
- 파일 확장자로는 `.json`을 사용
- 단순히 데이터를 표현하기 위한 경량 데이터 포맷이며, 데이터를 저장하거나 전송할 때 많이 사용한다고 한다.
- 특징 정리
  - 클라이언트 - 서버 간 데이터 전송 시 사용
  - 프로그래밍 언어에 상관없이 사용할 수 있는 데이터 포맷
  - 대부분의 언어에서 JSON 데이터 처리를 위한 라이브러리 제공
- 자바스크립트에서도 JSON 데이터 처리를 위한 내장 객체로 JSON이 제공된다.
- JSON 의 데이터 형식은 자바스크립트의 Object 객체와 유사하다. 단, key를 작성할 때는 반드시 **쌍따옴표(")**를 이용하여 작성한다.
- 관련 주요 메서드
  - `JSON.stringfy(value[, replacer[, space]])` : 자바스크립트에서 사용하는 값 또는 객체를 문자열 형태로 변환한다. 전달되는 값(value)은 **JSON 표기법으로 변환된다**([관련 MDN 내용](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify#%EC%84%A4%EB%AA%85)). 주로 데이터를 서버로 보내기 위해 객체 데이터를 JSON 형태로 변환하여 많이 활용. JSON 표기로 변환되기 때문에 객체 데이터 문자열 변환 시 속성에 `"`가 붙는 것을 확인할 수 있다.
  - `JSON.parse(text[, reviver])` : JSON 형태의 문자열을 해석하여 그 결과로 자바스크립트의 객체나 값을 생성한다. 주로 서버로부터 받은 문자열 데이터를 자바스크립트 객체로 변환할 때 많이 활용.

> stringify나 parse 뒤에 붙는 옵션 값들은 변환 전 포맷을 정의할 수 있도록 돕는 것들이다. (공백으로 구분하거나 함수 인자를 활용하거나) 나중에 따로 다뤄볼 기회가 있을 때 정리하기 📝

---

### Window 객체

![image](https://user-images.githubusercontent.com/104971437/176615112-92c485f3-e86b-43e4-9170-cdd1f7895d6d.png)

- Window 객체는 브라우저가 현재 보여주고 있는 창(탭)과 관련된 정보를 갖는다.
- Window 객체 내부에서 `window` 라는 전역 변수가 존재한다. 스크립트에 작성되는 전역 변수들은 window 객체의 프로퍼티가 된다. (위 이미지는 브라우저 콘솔에서 window에 접근한 것)
- window에는 다양한 기능이 내장되어 있는데, 이러한 기능에 접근할 때는 window를 접두사로 붙이지 않아도 참조 가능하다. (ex. `console.log()`)
- 관련 메서드
  - `alert([message])` : 경고 메시지가 담긴 대화 상자를 띄운다. 대화 상자가 처리되기 전까지 해당 페이지와 관련된 인터페이스 접근이 불가능하다.
  - `confirm([message])` : 진행 또는 종료 여부를 확인하는 메시지가 담긴 대화 상자를 띄운다. alert과는 다르게 확인, 취소 2개의 버튼이 있고, 선택한 것에 따라 확인이면 true, 취소면 false를 반환한다. alert과 같이 모달창 개념으로 페이지와 관련된 다른 상호작용이 무시된다.
  - `prompt([message, default])` : 사용자로부터 문자열 입력을 받을 수 있는 대화 상자를 띄운다. 대화 상자 내부에는 HTML의 input 태그와 같이 텍스트 입력을 받을 수 있는 인터페이스가 생긴다. 기본값을 설정할 수도 있는데 설정 시 대화 상자 입력폼에 기본값이 먼저 입력되어져 보여진다. 

```js
let count = 0;

const mySetInterval = setInterval(function() {
  if (count === 5) {
    clearInterval(mySetInterval);
  }
  console.log("Set Interval, 3000");
  count += 1;
}, 3000);
```

- 타이머 및 인터벌 함수
  - `setTimeout(code[, delay]), clearTimeout(timeoutID)`
    - setTimeout 함수는 정해진 시간을 만료했을 때 실행할 코드를 지정하는 타이머 함수
    - clearTimeout 함수는 setTimeout 함수의 실행을 취소하는 함수
    - setTimeout 함수에 전달하는 실행 코드는 함수이며, 지연되는 시간은 밀리초 단위의 정수로 전달한다.
  - `setInterval(code[, delay]), clearInterval(intervalID)`
    - setTimeout 함수와 작성 방식은 유사하지만 정해진 시간마다 지정된 코드를 반복 실행한다는 차이가 있다.
    - clearInterval 함수는 setInterval 함수의 실행을 취소하는 함수. clear 함수를 지정하지 않으면 인터벌 함수가 반복적으로 계속 실행되게 된다.

> 책에 있는 예제 코드를 참고하여 인터벌 함수만 확인. 아직 어떻게 활용해야 될 지 몰라 자세한 활용법은 추후 정리하기 📝

---

### Symbol 객체

```js
const symbolData = Symbol("Symbol test");

console.log(symbolData, ':', typeof symbolData); // Symbol(Symbol test) : symbol

const sameStringSymbol1 = Symbol('JS');
const sameStringSymbol2 = Symbol('JS');

console.log(sameStringSymbol1 === sameStringSymbol2); // false
```


- Symbol은 자바스크립트의 기본 원시타입 중 하나인 symbol 값과 관련된 내장 객체다.
- Symbol을 통한 값 생성시에는 `new` 연산자를 사용하지 않는다.
- Symbol을 통해 생성한 값은 **고유한 식별자로 사용될 수 있다**. 같은 문자열을 전달해도 생성된 값들은 서로 같지 않다. 항상 고유한 값을 가지게 된다. (코드 참고)
- 책에서는 Symbol 사용 시 다음과 같은 이점이 있다고 설명하고 있다.
  - 속성 충돌없이 유일한 값으로 사용 가능
    - 객체 내부에서 속성(키)명을 지정할 때 Symbol 값을 활용. 개발을 진행할 때 같은 속성명의 속성이 추가될 수 있는 경우(JS 버전 업데이트, 협의가 이루어지지 않은 네이밍 컨벤션 상황 등) 기존 속성이 덮여 쓰여지지 않고 저장된 내용 그대로 활용할 수 있다.

> 책에는 값 생성과 관련된 기본적인 내용만 있어 나중에 Symbol 활용에 대해 자세히 정리해야 겠다. 📝

---

**참고 자료**

- [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)