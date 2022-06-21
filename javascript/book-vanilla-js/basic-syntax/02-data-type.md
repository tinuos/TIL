# JavaScript - 데이터 타입

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 데이터 타입

- 프로그래밍 언어에서 사용되는 데이터를 분류하기 위한 것을 자료형, 데이터 타입이라 한다.
- 일반적으로 정수나 실수 등의 숫자형, 문자를 처리하기 위한 문자열, 논리값을 표현하기 위한 불린(boolean) 등을 말하는데, 프로그래밍 언어의 특성에 따라 데이터 타입의 종류가 달라진다.
- JS 에서는 크게 **기본 자료형**과 **객체**로 구분

### 기본 자료형

- 원시값이라고도 부른다.(Primitive)
- 불변의 값을 정의하기 위한 자료형 - 변경할 수 없는
- 현재 아래 7가지를 기본 자료형에 속하는 데이터 타입으로 분류
  - String
  - Number
  - Boolean
  - Undefined
  - Null
  - Symbol
  - BigInt

> Symbol과 BigInt 는 추후 학습 📝

#### String

```js
let stringTestOne = "Hello World~~~~";
let stringTestTwo = 'Hello World!!!!!';
let stringTestThree = "Hello \"World\"!!!!!";
```

- 문자열을 처리하기 위한 자료형
- `'`나 `"` 로 묶어 문자열로 처리해준다.
  - 홑따옴표로 문자열 처리시 내부에서 `"` 사용 가능
  - 쌍따옴표로 문자열 처리시 내부에서 `'` 사용 가능
- `\`와 `'`, `"`를 결합하여 일반 문자 그대로 표현할 수 있다. (이스케이프 문자)

#### Number

- 숫자를 표현하기 위한 자료형
- JS에서 숫자는 항상 **64비트 부동소수점**으로 저장된다.

#### Boolean

- 참이나 거짓을 표현하기 위한 자료형
- 참은 `true`, 거짓은 `false`로 나타낸다.
- 주로 조건식에서 조건을 판별할 때 그에 대한 결과값으로 사용된다.

#### undefined

- 정의되지 않음을 표현하기 위한 자료형
- `undefined`란 값을 가지면 데이터가 존재하지 않음을 나타낸다.
- 변수에 값을 할당하지 않을 경우 undefined 가 자동으로 할당된다.

#### Null

- undefined와 마찬가지로 값이 없음을 나타내는 자료형
- `null` 이란 값을 단독으로 사용
- undefined와의 차이점
  - undefined와는 달리 null 은 개발자가 명시적으로 나타내는 데이터
  - undefined는 상황에 따라 자바스크립트 엔진이 자동으로 할당하는 경우가 발생한다. 이러한 내부적인 처리와 구별하기 위해서 명확한 의도로 정의되지 않음을 부여하고자 할 때는 명시적으로 null을 많이 사용한다고 한다.
- 메모리 공간 확보
  - 어떤 변수에 값이 할당되어 메모리 공간을 참조하고 있을 때, 이를 해제하기 위해 null을 부여할 수도 있다. 해제된 공간의 데이터는 JS 엔진의 가비지 콜렌션에 따라 일정 시간 이후 비워지게 되어 메모리 공간을 확보할 수 있다고 설명. (해당 공간에 대해 어떠한 참조도 없을 때)

### 객체(Objects)

- 객체란 실제 존재하는 대상을 의미. 프로그래밍에서의 객체는 클래스를 통해 구현된 실제 인스턴스를 의미한다. 실제 세계에서 어떤 대상은 이름이나 성격 등을 가지며 걷거나 말하기 등의 행위를 할 수 있다. 프로그래밍에서의 객체 또한 어떠한 데이터를 갖거나 처리하는 행위 등을 가질 수 있는데, 객체가 갖는 데이터는 속성, 처리 행위는 메서드라 부른다. 클래스는 이러한 객체를 생성하기 위한 일종의 틀을 의미한다. (객체에 대한 자세한 내용은 추후에 따로 정리하기. 😂 일단, 여기서 객체란 데이터는 여러 속성이나 메서드를 가질 수 있는 형태라고만 이해하고 넘어가자) 📝
- JS의 모든 것은 **객체(Object)**
- 책에서는 Object, Array 라는 객체에 대해서만 설명. (일단 책 기준으로 학습한 후 필요한 내용은 따로 정리하기) 📝

#### Object

```js
const student = {
  name: "gildong",
  age: 18,
  height: 178.5
}

console.log(student["name"]);  // "gildong"
console.log(student.age);  // 18
console.log(student.height);  // 178.5

student.height = 181.5;

console.log(student.height);  // 181.5
```

- [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures#%EA%B0%9D%EC%B2%B4) 에서는 속성의 컬렉션이라고 표현.
- Object 타입은 `Key(키): Value(값)` 쌍으로 데이터를 저장
  - 속성값에는 객체를 포함하여 모든 데이터 타입이 올 수 있다.
  - 속성키에는 문자열이나 심볼을 사용
- 객체 내 데이터를 참조
  - 속성키를 이용하여 값을 참조한다.
  - 참조시에는 `.`을 이용하여 속성키를 명시하거나, `[]`에 속성키를 문자열로 전달한다.
  - 참조와 더불어 할당연산자(=)를 이용하여 객체 내 데이터를 변경할 수도 있다. (위 코드 참고하기)

#### Array

```js
const arrayTest = [1, 1.1, "String", true, {key: "value"}];

console.log(arrayTest[0]); // 1
console.log(arrayTest[1]); // 1.1
console.log(arrayTest[2]); // String
console.log(arrayTest[3]); // true
console.log(arrayTest[4]); // {key: 'value'}

arrayTest[2] = "배열 내 요소의 데이터 변경";
console.log(arrayTest[2]); // 배열 내 요소의 데이터 변경
```


- 여러 개의 데이터 타입을 같이 저장할 수 있는 구조(객체)
  - 책에서는 여러 값을 하나의 단일 참조(single reference)로 저장할 수 있는 구조라고 설명
  - 순서를 갖는 형태
- `[]`와 내부에 `,`를 이용하여 요소를 구분
  - 특정 위치에 저장되는 데이터를 배열에선 요소라 표현한다.
- 요소 참조
  - 인덱스를 이용하여 요소에 접근 - 인덱스는 데이터를 참조하기 위한 지표를 말한다.
  - 배열 객체에서 인덱스는 번호를 사용하며 `0`부터 시작

> 여기선 배열이라는 불리는 Array도 객체 타입이라는 것만 이해하고 넘어가기. 4장이나 추후에 따로 학습하게 될 예정. 📝

### typeof

- `typeof` 라는 연산자를 이용하여 간단하게 데이터 타입을 확인할 수 있다.

---

**참고 자료**

- [MDN - JavaScript의 타입과 구조](https://developer.mozilla.org/ko/docs/Web/JavaScript/Data_structures)