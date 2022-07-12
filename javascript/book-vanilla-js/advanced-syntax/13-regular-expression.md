# JavaScript - 정규 표현식(Regular Expression)
> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 정규 표현식

- regexp, 정규식 등으로 간단히 불린다.
- 정규식은 **특정한 규칙을 가진 문자열의 집합을 표현**하는 데 사용하는 형식 언어를 의미.
- 프로그래밍 언어마다 이러한 정규식을 처리하기 위한 기능이 내장되어 있다.
- 정규식은 해석하기 어렵고 특정 패턴을 구현하기에 다소 어렵다는 문제가 있지만 문자열의 포맷 처리 작업을 쉽게 해결할 수 있다는 이점도 있다.

### 자바스크립트의 정규식

- 자바스크립트에서는 내장 객체나 리터럴 방식을 이용하여 정규식을 작성할 수 있다.

#### 리터럴 방식

```js
let testString = "Hello, Java, JavaScript";

const reg = /JavaScript/;

console.log(reg); // /JavaScript/
console.log(typeof reg); // object
console.log(Object.prototype.toString.call(reg)); // [object RegExp]
```

- `/` 사이에 패턴을 넣어 사용
- 스크립트를 불러올 때 컴파일된다.

#### RegExp 생성자 함수 호출 방식

```js
const reg = new RegExp('JavaScript');
```

- RegExp 생성자 함수에 패턴을 전달하여 정규식을 만든다.
- **런타임에 컴파일 된다.**
  - 바뀔 수 있는 패턴 또는 사용자 입력 등 외부에서 패턴을 가져오는 경우에 사용

### 자바스크립트 정규식 함수

```js
let testString = "Hello, Java, JavaScript";

const reg = /JavaScript/;

console.log(reg.exec(testString));
/*
[
  'JavaScript',
  index: 13,
  input: 'Hello, Java, JavaScript',
  groups: undefined
]
*/
console.log(reg.test(testString)); // true

const matchResult = testString.match(/java/);
console.log(matchResult); // null

console.log(testString.search(reg)); // 13
console.log(testString.replace(reg, 'Python')); // Hello, Java, Python
console.log(testString.split(/Java/)); // [ 'Hello, ', ', ', 'Script' ]
```

- 정규식 처리와 관련된 여러 내장 함수가 있다.
  - `exec(str)` : 찾고자 하는 문자열 패턴을 전달하고 배열로 반환. 찾지 못할 경우에는 null 반환
  - `test(str)` : 대응되는 문자열이 있는지 검사 후 true나 false 반환
  - `str.match(regexp)` : 문자열 객체 내장 함수로, 대응되는 문자열을 찾아 배열로 반환한다. 없으면 null 반환. exec와 동일한 기능
  - `str.replace(regexp|substr, newSubstr|function)` : 대응되는 문자열을 찾아 다른 문자열로 치환. 문자열 객체의 내장 함수
  - `str.split(regexp|str)` : 지정 문자열로 기준을 나누어 배열로 반환. 문자열 객체의 내장 함수.
  - `str.search(regexp)` : 대응되는 문자열을 찾아 첫번째 인덱스를 반환. 없으면 -1 반환

### 정규식 특수문자

- 정규식에 특수문자를 활용하여 다양한 패턴에 대응할 수 있다.
  - `\` : 문자 그대로 인식. 특수 문자를 그대로 표현해야할 경우 유용
  - `^` : 시작 부분 대응
  - `$` : 끝 부분 대응
  - `$` : 끝 부분 대응
  - `*` : 0회 이상 반복 대응
  - `+` : 1회 이상 반복 대응
  - `?` : 0회 또는 1회 등장에 대응
  - `.` : 단일 문자에 대응
  - `[]` : 문자셋. `-`을 이용해서 문자의 범위를 지정할 수 있다. 제일 앞에 `^` 를 사용하면 부정 문자셋이 된다.

> 이 외에도 다양한 표현이 존재. 책에서 한번 살펴본 것으로 일단 만족하고 필요할 때 책이나 MDN 등을 참고해야 겠다. 

### 정규식 플래그

- 주요 플래그
  - `g` : 전역 검색
  - `i` : 대소문자를 구분하지 않는 검색
  - `m` : 다중 행 검색

### 정규식 사용 사례

- 책에서는 이메일 주소, 핸드폰 번호, 계좌번호 등 사용자로부터 입력받는 정보에 정규식을 적용하여 확인하는 절차로 활용 가능하다고 설명.

```js
const reg_email = /^([a-z]+\d*)+(\.?\w+)+@\w+(\.\w{2,3})+$/;
console.log(reg_email.test("abc@gmail.com"));
```

---

**참고 자료**

- [위키백과 - 정규 표현식](https://ko.wikipedia.org/wiki/%EC%A0%95%EA%B7%9C_%ED%91%9C%ED%98%84%EC%8B%9D)
- [MDN - 정규 표현식](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Regular_Expressions)