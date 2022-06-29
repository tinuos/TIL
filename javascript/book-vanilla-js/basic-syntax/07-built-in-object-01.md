# JavaScript - 내장 객체 01

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 내장 객체

- JS 엔진 내부에 전역 범위에 존재하는 표준 내장객체에 대해 학습
  - 내장 객체가 가지는 다양한 함수를 사용하여 특정 데이터 타입이나 처리 로직에 따라 활용 가능
- [MDN 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)에서 항목별 표준 내장 객체에 대하여 살펴볼 수 있다.
- 여기서는 참고하는 책 기준으로 간단하게만 학습하고 정리할 예정.

---

### Object 객체

- JS의 모든 객체의 루트가 되는 객체
- Object 객체를 통해 생성된 객체 인스턴스는 `.` 을 이용하여 프로퍼티(속성), 메서드(함수) 등을 추가할 수 있다.

> 추 후 this나 생성자 함수 등을 배운 뒤 자세히 학습하기 📝

---

### String 객체

```js
const testString = "Hello JavaScript!!!";

// length
console.log(testString.length); // 19

// indexOf()
console.log(testString.indexOf('Java')); // 6
console.log(testString.indexOf('Python')); // -1
console.log(testString.indexOf('a')); // 7
console.log(testString.indexOf('a', 8)); // 9

// lastIndexOf()
console.log(testString.lastIndexOf('a')); // 9
console.log(testString.lastIndexOf('a', 8)); // 7

// slice()
console.log(testString.slice(6, 10)); // Java : 10 + -1 = 9 까지 잘라낸다. (2번째 a)
console.log(testString.slice(6)); // JavaScript!!!
console.log(testString.slice(-3)); // !!!
console.log(testString.slice(-13, -3)); // JavaScript :  -3 + -1 = -4 까지 잘라낸다.(t까지)

// substring()
console.log(testString.substring(6, 10)); // Java
console.log(testString.substring(6)); // JavaScript!!!

// replace()
console.log(testString.replace('!!!', '???')) // Hello JavaScript???
console.log(testString.replace('a', 'A')); // Hello JAvaScript!!!
//  - 정규표현식 : i, g 옵션
console.log(testString.replace(/hello/, 'Welcome')); // Hello JavaScript!!!
console.log(testString.replace(/hello/i, 'Welcome')); // Welcome JavaScript!!!
console.log(testString.replace(/a/, 'A')); // Hello JAvaScript!!!
console.log(testString.replace(/a/g, 'A')); // Hello JAvAScript!!!

// toUpperCase(), toLowerCase()
console.log(testString.toUpperCase()); // HELLO JAVASCRIPT!!!
console.log(testString.toLowerCase()); // hello javascript!!!

// concat()
console.log(testString.concat(' ', 'Hello ', 'HTML', '!!!')); // Hello JavaScript!!! Hello HTML!!!

const testString2 = '   trim TEST |  ';

// trim(), trimStart(), trimEnd()
console.log(testString2.trim()); // 'trim TEST |'
console.log(testString2.trimStart()); // 'trim TEST |  '
console.log(testString2.trimEnd()); // '   trim TEST |'

const testString3 = 'zzz';

// padStart(), padEnd()
console.log(testString3.padStart('7', '*')); // ****zzz
console.log(testString3.padEnd('7', '*')); // zzz****

const testString4 = 'abcde';

// charAt()
console.log(testString4.charAt(2)); // c
console.log(testString4.charAt()); // a

// charCodeAt()
console.log(testString4.charCodeAt(2)); // 99
console.log(testString4.charCodeAt()); // 97

const testString5 = 'a,b,c,d,e';

// split()
console.log(testString5.split()); // [ 'a,b,c,d,e' ]
console.log(testString5.split("")); // [  'a', ',', 'b', ',', 'c', ',', 'd', ',', 'e' ]
console.log(testString5.split(',')); // [ 'a', 'b', 'c', 'd', 'e' ]
console.log(testString5.split(',', 3)); // [ 'a', 'b', 'c' ]

const testString6 = 'https://wwww.naver.com';

// startsWith(), endsWith()
console.log(testString6.startsWith('https://')); // true
console.log(testString6.startsWith('http://')); // false
console.log(testString6.endsWith('.com')); // true
console.log(testString6.endsWith('.co.kr')); // false
```

- 문자열을 다루기 위한 객체
- 문자열 관련 프로퍼티나 메서드를 활용 가능
- 관련 속성
  - `length` : 문자열의 길이를 반환
- 관련 메서드
  - `indexOf(searchValue[, fromIndex])`
    - 문자열 내 특정 문자열이 존재하는 **시작 인덱스**를 반환
    - 특정 문자열이 없을 경우 **-1**을 반환
    - 2번째 인자는 옵션으로 검색을 시작할 인덱스의 위치를 지정할 수 있다.
  - `lastIndexOf(searchValue[, fromIndex])`
    - 문자열 내 특정 문자열이 존재하는 마지막 **시작 인덱스**를 반환
    - 특정 문자열이 2개 이상 존재할 경우 문자열 끝에서 제일 가까운 특정 문자열의 시작 인덱스를 반환한다.
    - 특정 문자열이 없을 경우 **-1**을 반환
    - 2번째 인자는 옵션으로 검색을 시작할 인덱스의 위치를 지정할 수 있다.
  - `slice(beginIndex[, endIndex])`
    - 문자열에서 특정 부분의 문자열을 잘라내어 반환
    - 종료 인덱스 기준 **(종료 인덱스 - 1)** 부분까지 잘라낸다.
    - 두번째 인자인 종료 인덱스를 생략할 경우 시작 인덱스부터 문자열의 끝까지 잘라내어 반환
    - 시작 인덱스를 음수로 할 경우 뒤에서 부터 인덱스를 세어 잘라낸다.(맨 마지막 문자가 -1부터 시작)
    - 원본 문자열엔 영향을 주지 않는다.
  - `substring(indexStart[, indexEnd])`
    - 특정 문자열을 잘라낸다. 
    - slice()와 사용법이 거의 비슷. 단, 음수를 허용하지 않는다. (역방향으로 추출이 불가능)
    - 문자열 추출과 관련하여 `substr()`이란 메서드도 존재하나 [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/substr)에선 기능적인 특징과 웹 표준 명세의 이유로 사용을 제한할 것을 권하고 있어 따로 정리하진 않으려 한다. => **문자열 추출 시 slice 나 substring 메서드 활용**
  - `replace(regexp|substr, newSubstr|function)`
    - 문자열 내 특정 문자열을 새로운 문자열로 대체한 문자열을 반환해주는 메서드 (원본 문자열엔 영향을 주지 않는다)
    - 대소문자를 구분하며, 문자열에 특정 문자열이 하나 이상인 경우 맨 처음에 발견된 문자열만 대체하게 된다. 
    - 정규 표현식을 활용하면, 대소문자를 구분하지 않거나 정규표현식과 일치하는 모든 특정 문자열을 대체할 수 있다. (JS 정규 표현식 문법 및 자세한 내용은 추후 정규식에서 자세히 학습하기 📝)
      - `i` : insensitive의 약자. 대소문자를 구분하지 않는다.
      - `g` : global의 약자. 문자열에서 해당 정규 표현과 일치하는 모든 문자열을 찾게 된다.
  - `toUpperCase()` or `toLowerCase()`
    - 문자열을 대문자 또는 소문자로 변환한 새로운 문자열로 반환해주는 메서드
  - `concat(string2, string3[, ..., stringN])`
    - 문자열에 인수로 전달하는 문자열들을 차례로 이어붙인 문자열을 반환해주는 메서드
    - 문자열을 합쳐주는 기능
  - `trim()`, `trimStart()`, `trimEnd()`
    - 문자열에 공백을 제거한 새로운 문자열을 반환해주는 메서드들
    - `trim` 은 문자열의 양 쪽 끝에 있는 모든 공백 문자( 모든 공백문자(space, tab, NBSP 등)와 모든 개행문자(LF, CR 등)를 의미)를 제거하며, `trimStart`는 문자열 왼쪽 시작부분, `trimEnd`는 문자열 오른쪽 끝 부분의 모든 공백 문자를 제거한다.
  - `padStart(targetLength [, padString])`, `padEnd(targetLength [, padString])`
    - 지정한 길이만큼 지정한 문자를 앞이나 뒤에 추가한다.
    - 첫번째 인수인 지정 길이는 **목표로 하는 문자열의 총 길이**를 의미. 두번째 인수는 추가할 문자
    - 날짜나 숫자에서 앞에 0을 추가할 때 활용 가능
  - `charAt(index)`
    - 0과 문자열의 길이 - 1 사이의 정수값(인덱스)을 전달하여 문자열 내 특정 인덱스에 있는 단일 문자를 반환
    - 전달값이 없을 경우 기본값은 0이 되어 첫 문자를 반환
  - `charCodeAt(index)`
    - 문자열에서 전달되는 인덱스에 위치한 단일문자의 유니코드(UTF-16) 값을 반환해주는 메서드 (0 ~ 65535)
  - `split([separator[, limit]])`
    - 전달되는 구분자를 문자열 내에서 특정하여 문자를 나눠 배열로 반환해주는 메서드
    - 구분자로 빈 문자열을 전달할 경우 눈으로 인식하는 문자 하나하나로 나누는 것이 아니라, **UTF-16 코드유닛**으로 나누게 된다고 한다. 이 경우 예상치 못한 스플릿 작업이 발생할 수 있기 때문에 주의하여 사용할 것을 권장하고 있다. ([MDN 내용](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String/split#%EA%B5%AC%EB%AC%B8), [stack overflow 내용](https://stackoverflow.com/questions/4547609/how-to-get-character-array-from-a-string/34717402#34717402))
    - 두 번째 인수는 구분자로 나눠지는 요소의 개수를 제한하기 위해 사용. 정수로 전달하게 되면 해당 요소의 개수까지만 요소로 나눈 배열을 반환한다.
    - 날짜 포맷, 태그 포맷 등 특정 문자로 이루어져 있는 포맷에서 활용해 볼 수 있다.
  - `startsWith(searchString[, position])` or `endsWith(searchString[, position])`
    - 문자열의 시작이나 끝이 전달되는 문자열(첫번째 인수)과 맞는지 판단하는 메서드로 결과에 따라 true 또는 false를 반환한다.
    - 두번째 인수는 위치값(인덱스)을 전달하는데 기본값은 0이다.
    - 프로토콜 문자열이나 파일 확장자 추출 등에 활용해 볼 수 있다.

---

### Number 객체

```js
const a = 15;

// toString()
console.log(a.toString()); // 15
console.log(a.toString(2)); // 1111
console.log(a.toString(8)); // 17
console.log(a.toString(10)); // 15
console.log(a.toString(16)); // f
console.log(typeof a.toString()); // string

const b = 123456.789;

// toExponential()
console.log(a.toExponential()); // 1.5e+1
console.log(b.toExponential()); // 1.23456789e+5
console.log(b.toExponential(2)); // 1.23e+5

const c = 12.3456789;
const d = 12.94522222;

// toFixed()
console.log(c.toFixed()); // 12
console.log(c.toFixed(0)); // 12
console.log(c.toFixed(3)); // 12.346
console.log(d.toFixed(3)); // 12.945

// toPrecision()
console.log(c.toPrecision()); // 12.3456789
console.log(c.toPrecision(1)); // 1e+1
console.log(c.toPrecision(2)); // 12
console.log(d.toPrecision()); // 12.94522222
console.log(d.toPrecision(1)); // 1e+1
console.log(d.toPrecision(2)); // 13

// Number.parseInt()
console.log(Number.parseInt('10')); // 10
console.log(Number.parseInt('10.12345')); // 10
console.log(Number.parseInt('-10')); // -10
console.log(Number.parseInt('10', 2)); // 2
console.log(Number.parseInt('10', 8)); // 8
console.log(Number.parseInt('10', 10)); // 10
console.log(Number.parseInt('10', 16)); // 16

console.log(Number.parseInt('110110', 2)); // 54 = 32 + 16 + 0 + 4 + 2 + 0
console.log(Number.parseInt('71', 8)); // 57 = 56 + 1
console.log(Number.parseInt('f1d', 16)); // 3869 = 3840 + 16 + 13

console.log(Number.parseInt('10 years')); // 10
console.log(Number.parseInt('days 4000')); // NaN
console.log(Number.parseInt('              4000')); // 10

// Number.parseFloat()
console.log(Number.parseFloat('.123')); // 0.123
console.log(Number.parseFloat('1000')); // 1000
console.log(Number.parseFloat('2.999    abcdef')); // 0.1
console.log(Number.parseFloat('abcdef   2.999')); // NaN
console.log(Number.parseFloat('             1.1')); // 1.1

// Number.MAX_VALUE
console.log(Number.MAX_VALUE); // 1.7976931348623157e+308
console.log(Number.MAX_VALUE + 1e+308); // Infinity

// Number.MIN_VALUE
console.log(Number.MIN_VALUE); // 5e-324
```

- 숫자형 데이터를 다룰 때 유용한 속성 및 메서드를 제공하는 래퍼 객체
  - 래퍼 객체(Wrapper) : 원시형 값을 감싸는 객체를 의미.
- 자바스크립트의 숫자형 데이터는 정수나 실수를 따로 구분하지 않고, 실수로 표현. - 64비트 부동소수점
- 관련 속성
  - `Number.MAX_VALUE`
    - JS에서 다룰 수 있는 최대값
    - 약 1.79e+308(2^1024)
    - 이 값보다 큰 값은 `Infinity`로 표현된다.
  - `Number.MIN_VALUE`
    - JS에서 다룰 수 있는 최소값 (0에 가장 가깝지만 음수가 아닌 값)
    - 약 5e-324. 
    - 이 값보다 작은 값은 0으로 변환된다.
  - `Number.NaN`
    - Not-A-Number. 숫자가 아님을 나타낼 때 사용되는 값
  - 이 외 무한대 관련 속성 등이 있다.
- 관련 메서드
  - `toString([radix])`
    - 숫자형 데이터를 문자형으로 반환해주는 메서드. String 객체에 있는 많은 기능(메서드)을 사용하기 위해 활용해 볼 수 있다.
    - radix는 옵션으로 기수 값을 전달하여 해당 기수의 진법으로 변환된다. (2 ~ 36 사이의 정수 전달)
  - `toExponential([fractionDigits])`
    - 숫자를 지수형으로 반환
    - fractionDigits은 옵션으로 소수점 이하로 표시할 자릿수를 지정한다.
    - `e+` 다음에 오는 숫자를 `10 ^ 숫자` 로 하여 e앞의 숫자에 곱하는 식으로 계산하면 원래의 숫자
  - `toFixed([digits])`
    - 소수점 몇번째 자리까지 표시할 지 결정하는 메서드로 지정된 소수점 자릿우에 대한 **반올림 값**을 반환 - 고정 소수점 표기
    - digits은 옵션으로 기본값은 0. 기본적으로는 0 이상 ~ 20 이하의 값을 전달하여 소수점 뒤에 나타날 자릿수를 지정할 수 있다.
  - `toPrecision([precision])`
    - 정수, 소수 전체를 기준으로 몇번째 자리까지 보여줄지를 결정하는 메서드로 반올림값을 반환한다.
    - precision은 옵션. 단어의 뜻은 정확도를 의미. 전체 자릿수를 전달하며 1 ~ 100의 정수값을 전달(0 전달 시 에러 확인). 만약 정수 자릿수보다 작은 값을 전달하면 (ex. 12.45 -> precision : 1) 지수형된 값을 반환한다. (상단 코드 참고)
  - `parseInt(string, radix)`
    - 문자열을 파싱하여 특정 진수의 정수를 반환
    - 전역 함수 parseInt()와 동일한 기능을 가진다. (`Number.parseInt === parseInt`)
    - radix는 옵션으로 특정 진수를 설정한다. (2 ~ 32) 생략 시 10으로 취급(10진수)
    - 문자열의 시작이 숫자형이면 숫자형 데이터를 반환한다.
      - 공백을 제외한 첫 문자가 숫자형이면 가능
      - 숫자형이 아닌 경우 에러가 발생하지 않고 `NaN`이 반환됨을 유의할 것
  - `parseFloat(string)`
    - Number.parseInt()와 작동 방식이 유사하나 진수 설정 옵션이 없고 부동소수점 실수를 반환한다.

---

### Array 객체

```js
const arrayTest = ['apple', 'banana', 'cherry', 'mango'];

console.log(arrayTest);

// toString()
console.log(arrayTest.toString()); // apple,banana,cherry,mango

// join()
console.log(arrayTest.join()); // apple,banana,cherry,mango
console.log(arrayTest.join(' * ')); // apple * banana * cherry * mango
console.log(arrayTest.join('')); // applebananacherrymango

// pop()
console.log(arrayTest.pop()); // mango
console.log(arrayTest.toString()); //  apple,banana,cherry

// push()
console.log(arrayTest.push('mango')); // 4
console.log(arrayTest.toString()); // apple,banana,cherry,mango

// shift()
console.log(arrayTest.shift()); // apple
console.log(arrayTest.toString()); // banana,cherry,mango

// unshift()
console.log(arrayTest.unshift('apple')); // 4
console.log(arrayTest.toString()); // apple,banana,cherry,mango

// splice()
arrayTest.splice(1, 1); // [ 'apple', 'cherry', 'mango' ]
console.log(arrayTest);
arrayTest.splice(1, 0, 'banana'); // [ 'apple', 'banana', 'cherry', 'mango' ]
console.log(arrayTest);

// concat()
const concatTestArr = ['a', 1, true, {concat: "hello"}]

const emptyConcatArr = concatTestArr.concat(); // 얕은 복사

console.log(concatTestArr); // [ 'a', 1, true, { concat: 'hello' } ]
console.log(emptyConcatArr); // [ 'a', 1, true, { concat: 'hello' } ]
emptyConcatArr[3].concat = "JavaScript!!!";
console.log(concatTestArr); // [ 'a', 1, true, { concat: 'JavaScript!!!' } ]
console.log(emptyConcatArr); // [ 'a', 1, true, { concat: 'JavaScript!!!' } ]

// slice()
console.log(arrayTest.slice()); // [ 'apple', 'banana', 'cherry', 'mango' ]
console.log(arrayTest.slice(1)); // [ 'banana', 'cherry', 'mango' ]
console.log(arrayTest.slice(1, 3)); // [ 'banana', 'cherry' ]
console.log(arrayTest); // [ 'apple', 'banana', 'cherry', 'mango' ]

const sortTestArr = [ 'W', 'a', 'B', 'c', 1, 4, 2, 3, 5, 'z', 'F', 'y', 'G', 'O', 'w' ];

// sort()
console.log(sortTestArr.sort()); // [ 1, 2, 3, 4, 5, 'B','F', 'G', 'O', 'W', 'a', 'c', 'w', 'y', 'z' ]

const filterTestArr = ['#', '#####', '##', '####', '#####', '#', '###', '##', '####', '#####', '######'];

// filter()
console.log(filterTestArr.filter(function(element) {
  if (element.length < 4) {
    return element;
  }
}));

const mapTestArr = [1, 2, 4, 8, 16];

// map()
console.log(mapTestArr.map(function(element) { return element * 2 })); // [ 2, 4, 8, 16, 32 ]

const reduceTestArr = [1, 2, 3, 4, 5];
const emptyArr = [];

// reduce()
console.log(reduceTestArr.reduce(function(acc, currentValue) {
  return acc + currentValue; 
})); // 15 = 1(default) + 2 + 3 + 4 + 5
console.log(reduceTestArr.reduce(function(acc, currentValue) {
  return acc + currentValue; 
}, 100)); // 115 = 100(default) + 1 + 2 + 3 + 4 + 5
// console.log(emptyArr.reduce(function(acc, currentValue) {
//   return acc + currentValue;
// })); // TypeError: Reduce of empty array with no initial value
console.log(emptyArr.reduce(function(acc, currentValue) {
  return acc + currentValue;
}, 0)); // TypeError: Reduce of empty array with no initial value

const arrayTest2 = ['A', 'B', 'C'];

arrayTest2[1] = 'Z';
console.log(arrayTest2.toString()); // A,Z,C
```

- 리스트와 비슷한 배열을 생성하는 전역 객체
  - 리스트 : 시퀀스라고도 불리는 추상 자료형. 다른 자료형의 값을 모두 담을 수 있는 컨테이너의 역할을 하며, 같은 값을 중복적으로 담을 수 있고 각각은 별개의 요소로 취급.
  - 배열 : 번호(인덱스)와 이에 대응하는 데이터들로 이루어진 자료형을 의미. 일반적인 배열의 의미는 같은 종류의 값들을 순차적으로 저장하는 것을 의미하며, 시작점으로부터 위치값을 가진다.
  - MDN 설명 중 리스트와 비슷한 배열이라고 말하는 것은 다른 자료형들의 값들을 동시에 저장할 수 있으면서 인덱스를 통해 접근 가능하기 때문에 그렇게 설명한 것 같다.
  - `[]`와 `,`를 이용하여 리터럴 방식으로 바로 Array 데이터 생성 가능. 요소를 `,` 로 구분하며, JS의 다양한 데이터 타입의 값이 올 수 있다.
  - 배열 요소 변경 시 해당 요소의 인덱스로 접근하여 새로운 요소를 할당.
- 관련 속성
- 관련 메서드
  - `toString()`
    - 배열 내부를 문자열로 표현하여 반환.
    - 모든 요소를 `,`로 결합하여 하나의 문자열로 나타낸다.
  - `join([separator])`
    - 배열 내부의 모든 요소를 구분자로 결합하여 하나의 문자열로 반환.
    - 구분자는 옵션으로 문자열로 지정하며, 미지정시 쉼표로 구분. 빈 문자열일 경우 아무 문자 없이 연결된다.
  - `pop()`
    - 배열의 마지막 요소를 제거하고 이를 반환.
  - `push(element1[, ...[, elementN]])`
    - 배열의 맨 끝에 요소를 추가하고, 배열의 새로운 요소 길이를 반환.
  - `shift()`
    - 배열에서 첫 번째 요소를 제거 후 해당 요소를 반환
  - `unshift([...elementN])`
    - 배열의 맨 앞에 요소를 추가한 후 배열의 새로운 길이를 반환
  - `splice(start[, deleteCount[, item1[, item2[, ...]]]])`
    - 배열의 기존 요소를 삭제, 교체, 추가할 때 사용하는 메서드. 제거한 요소가 반환된다.
    - 필수값은 시작 인덱스. 변경이 일어날 요소의 시작을 지정
    - 두번째 deleteCount는 옵션으로 시작 인덱스를 포함하여 제거할 개수를 설정한다.
    - 세번째 인자부터는 제거 처리가 다 된 후 추가될 요소를 지정
  - `concat([value1[, value2[, ...[, valueN]]]])`
    - 문자열 concat 처럼 특정 배열을 이어 붙여 새로운 배열을 반환한다. (원본 배열에 영향을 주지 않는다)
    - **전달 값 생략 시 얕은 복사가 되니 주의할 것.** (객체 데이터가 갖는 모든 원시값을 복사하지 않는다. - 참조가 복사됨 : 상단 코드 참고)
  - `slice([begin[, end]])`
    - 배열의 특정 시작부터 특정 끝 지점까지의 얕은 복사복을 새로운 배열 객체로 반환
    - 원본 배열은 변하지 않는다.
    - 시작 및 종료 인덱스는 옵션. 시작 인덱스 미 지정 시 인덱스 0부터 slice 된다. 종료 인덱스 미 지정 시 배열의 끝까지 slice 된다.
    - 종료 인덱스 지정 시 `종료 인덱스 - 1` 까지 잘라낸다.
    - **slice 시 얕은 복사로 잘라낸다는 것에 주의하기** (객체 참조 복사)
  - `sort([compareFunction])`
    - 기본적으로 문자열의 유니코드 순서대로 배열 내 요소를 정렬. 정렬 함수를 인자로 전달하여 순서를 정의하여 정렬할 수도 있다.
    - 정렬 함수
      - 숫자 데이터 비교 정렬에 활용 가능
      - 함수의 반환값에 따라 정렬.
      - 오름차순 : function(a, b) {return a - b;}
        - a 는 첫번째 요소, b 는 두번째 요소
        - 만약 a - b가 양수일 경우 위치 변경이 일어난다. `return 1` (음수일 경우 일어나지 않음 `return -1`) 
        - 위치 변경이 일어나지 않을 때까지 위 과정을 반복
      - 내림차순 : 반환값이 오름차순의 반대 (b - a) 또는 오름차순으로 정렬 후 reverse() 사용
    - 정렬 함수는 sort() 메서드에서 정의된 대로 동작한다. 따라서, 위 함수 형태로 인자를 전달하여 정렬을 따로 정의해야 한다.
    - 정렬 처리 방식에 따라 오버헤드가 높아질 수도 있는데, 이 때는 map과 같이 사용하여 정렬할 내용을 미리 추출하고 이 범위 내에서 정렬할 것을 권장하고 있다.
  - `filter(callback(element[, index[, array]])[, thisArg])`
    - 주어진 함수의 특정 조건을 만족하는 새로운 배열을 반환
    - 콜백함수를 인자로 전달
      - 함수의 인자로 전달하는 함수를 콜백함수라 한다. 함수 로직 처리 시 전달받은 인자(함수)를 사용할 때 다시 함수를 호출한다고 하여 Call Back. 여기서는 filter라는 메서드가 정의될 때 전달받은 콜백함수를 내부에서 호출하도록 정의되어져 있다고 생각하면 된다.
    - 콜백함수 인자
      - 인자로는 요소, 현재 요소 인덱스(옵션), filter를 호출한 배열 전체(옵션)가 들어가며,  함수 처리 로직을 만족하는 경우에만 반환하도록 설정하여 새로운 배열을 만들어 낼 수 있다. (true일 경우에만)
  - `map(callback(currentValue[, index[, array]])[, thisArg])`
    - 배열의 요소마다 함수 호출의 결과를 모아 새로운 배열을 반환
    - filter처럼 콜백함수 사용이 유사. 
  - `reduce(callback(accumulator, currentValue[, currnentIndex, array][, initialValue]))`
    - 배열 요소를 하나씩 순회하여 콜백함수의 로직에 따라 처리된 값을 누적한 결과를 반환
    - 콜백함수에는 4개의 인수를 가질 수 있다.
      - accumulator : 누적값
      - currentValue : 현재 배열 요소
      - currentIndex : 현재 요소 인덱스
      - array : reduce가 참조하고 있는 배열 전체
    - initialValue 인자는 콜백 함수 최초 호출 시에 제공되는 초기값. 미 지정 시 배열의 첫번째 요소를 사용. **빈 배열에서 초기값 없이 reduce 호출 시 에러 발생 (상단 코드 참고)**

---

**참고 자료**

- [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)