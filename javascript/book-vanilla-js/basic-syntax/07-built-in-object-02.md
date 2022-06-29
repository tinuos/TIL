# JavaScript - 내장 객체 02

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 내장 객체

- JS 엔진 내부에 전역 범위에 존재하는 표준 내장객체에 대해 학습
  - 내장 객체가 가지는 다양한 함수를 사용하여 특정 데이터 타입이나 처리 로직에 따라 활용 가능
- [MDN 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)에서 항목별 표준 내장 객체에 대하여 살펴볼 수 있다.
- 여기서는 참고하는 책 기준으로 간단하게만 학습하고 정리할 예정.

---

### Date 객체

- 날짜와 시간 데이터를 다루기 위한 객체
- 사용자(호스트)의 장치가 가지는 현지 시간을 기준으로 날짜 및 시간을 보여준다.

#### Date 생성자

```js
const noValue = new Date();
console.log(noValue); // ex) 브라우저 : Wed Jun 29 2022 10:10:52 GMT+0900 (한국 표준시)

const milliseconds = new Date(1000000000);  // -> 1000000 초 : 약 11일
console.log(milliseconds); // ex) 브라우저 : Mon Jan 12 1970 22:46:40 GMT+0900 (한국 표준시)

const timeDatas1 = new Date(2001, 9, 10);
const timeDatas2 = new Date(2001, 9, 10, 20, 10, 30, 2000);
console.log(timeDatas1); // ex) 브라우저 Wed Oct 10 2001 00:00:00 GMT+0900 (한국 표준시)
console.log(timeDatas2); // ex) 브라우저 Wed Oct 10 2001 20:10:32 GMT+0900 (한국 표준시)
```

- 객체 인스턴스를 생성하는 `new` 연산자를 이용하여 생성
- Date 객체에 전달하는 값(매개변수)에 따라 날짜와 시간을 달리하여 생성할 수 있다.
  - 매개 변수 미 지정
    - 사용자 장치 기준 시간
  - millisecond 값 전달
    - 일반 정수로 값을 전달하면 `1970년 1월 1일 00:00:00 UTC(UNIX 시간)`으로부터 밀리초 단위로 표현.
  - 개별 시간 데이터 구성요소
    - year, month, day, hours, minutes, seconds, milliseconds 를 모두 매개변수에서 가져와 시간을 보여준다.
    - 이러한 방식으로 생성할 시 연과 월은 필수로 전달해야 하며(밀리세컨트 변환 방지) 나머지는 순차적으로 옵션(기본값이 다 정해져 있다)이다.
    - **월의 경우 인덱스 방식으로 1월은 0, 12월은 11로 전달해야 한다.**
  - 타임스탬프 문자열 전달
    - `Date.parse()` 가 해석할 수 있는 형태의 문자열로 전달.
    - 표준으로 정해진 시간 표시 포맷을 전달하는 방식. - 관련 [MDN 문서](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Date/Date#parameters)
    - **단, 브라우저마다 시간 표시 방법에 차이가 존재할 수 있어 권장되지 않는 방식이라 한다.**

#### GET 함수

```js
const testTime = new Date(2022, 5, 29, 11, 45, 30, 2000);

console.log(testTime.getFullYear()); // 2022
console.log(testTime.getMonth()); // 5
console.log(testTime.getDate()); // 29
console.log(testTime.getHours()); // 11
console.log(testTime.getMinutes()); // 45
console.log(testTime.getSeconds()); // 30
console.log(testTime.getMilliseconds()); // 2000
console.log(testTime.getDay()); // 3 : 수요일

console.log(testTime.getTime()); // 1656470732000 : Unix 타임부터 testTime 시간까지 밀리초 계산

console.log(Date.now()); // 현재 시간 반환
```

- 시간 데이터를 가지고 있는 Date 객체 내 특정 데이터를 가지고 올 수 있는 함수 종류
  - `getFullYear()` : 4자리 연도 반환
  - `getMonth()` : 0 ~ 11 사이의 월 인덱스 정보 반환 ( 1월은 0 ~ 12월은 11 )
  - `getDate()` : 1 ~ 31 사이의 일 정보 반환
  - `getHours()` : 0 ~ 23 사이의 시간 정보 반환
  - `getMinutes()` : 0 ~ 59 사이의 분 정보 반환
  - `getSeconds()` : 0 ~ 59 사이의 초 정보 반환
  - `getMilliseconds()` : 0 ~ 999 사이의 밀리초 정보 반환
  - `getTime()` : 1970년 1월 1일 이후에 해당하는 밀리초 정보 반환 (Date 객체가 가지는 시간 기준)
  - `getDay()` : 0 ~ 6 사이의 요일 정보 반환 ( 0은 일요일 ~ 1은 월요일 )
- `Date.now()` : 현재 기준 getTime()에 해당하는 정보 반환

#### SET 함수

```js
const testTime = new Date(2022, 5, 29, 11, 45, 30, 2000);

console.log(testTime); // 2022-06-~
console.log(testTime.setFullYear(1991)); // 1991
console.log(testTime.getFullYear());
console.log(testTime.setFullYear(2000, 2)); // 옵션 month 추가 설정
console.log(testTime); // 2000-03-~
```

- 시간 데이터를 가지고 있는 Date 객체 내 특정 데이터 설정하는 함수 종류
  - `setFullYear(yearValue[, monthValue[, dayValue]])` : 설정할 연도를 4자리로 전달. 월 및 일 관련 옵션 가능
  - `setMonth(monthValue[, dayValue])` : 설정할 월 인덱스 값 전달(0 ~ 11). 일 옵션 가능
  - `setDate(dayValue)` : 설정할 일 전달(1 ~ 31)
  - `setHours(hoursValue[, minutesValue[, secondsValue[, msValue]]])` : 설정할 시간 전달(0 ~ 23). 분, 초, 밀리초 옵션 가능
  - `setMinutes(minutesValue[, secondsValue[, msValue]])` : 설정할 분 전달(0 ~ 59). 초, 밀리초 옵션 가능
  - `setSeconds(secondsValue[, msValue])` : 설정할 초 전달(0 ~ 59). 밀리초 옵션 가능
  - `setMilliseconds(millisecondsValue)` : 설정할 밀리초 전달(0 ~ 999).
  - `setTime(timeValue)` : Unix 시간 기준 이후 밀리초 정보를 설정
- 하위 값 옵션이 가능한 함수들은 JS 버전이 업그레이드 되면서 가능하게 된 것이라 한다. (1.3 이전에는 단일값만 허용)

---

### Set 객체

```js
const testSetObj = new Set();

// size
console.log(testSetObj.size); // 0

// add()
console.log(testSetObj.add(1));
console.log(testSetObj.add(2));
console.log(testSetObj.add(2)); // 추가되지 않는다.
console.log(testSetObj.add(2)); // 추가되지 않는다.
console.log(testSetObj.add(3));
console.log(testSetObj.size); // 3

// has()
console.log(testSetObj.has(3)); // true
console.log(testSetObj.has(100)); // false

// delete()
console.log(testSetObj.delete(5)); // false
console.log(testSetObj.delete(2)); // true
console.log(testSetObj); // Set(2) { 1, 3 }

// forEach()
testSetObj.add('String');
testSetObj.forEach(function(currentValue, currentKey) {
  console.log(currentKey, ':', currentValue);
})

// clear()
testSetObj.clear();
console.log(testSetObj); // Set(0) {}
```

- Array 처럼 자료형에 관계없이 모든 형태의 값을 저장 가능
- 배열은 같은 값은 중복으로 저장할 수 있지만 Set은 중복 값을 허용하지 않아 **유일한 값을 보장**한다.
- `Set()` 생성자를 이용하여 생성
- 관련 주요 속성
  - `size` : Set 객체 내 존재하는 요소들의 개수를 반환. (Set 데이터 크기)
- 관련 주요 메서드
  - `add(value)` : Set 객체에 추가할 요소의 값. value가 이미 Set 객체 내에 존재한다면 추가되지 않는다.
  - `has(value)` : Set 객체 내 value 가 존재하는지 판단하여 있으면 true, 없으면 false를 반환한다.
  - `delete(value)` : Set 객체 내 value를 제거한다. 제거하면 true, 아니면 false 반환.
  - `clear()` : Set 객체 내 모든 요소를 제거.
  - `forEach(callback[, thisArg])` : Set 객체 내 모든 요소를 순회하며 반복하며, callback 함수에 작성된 로직을 수행한다.
    - callback 에서는 일반적으로 요소값만 활용(요소 키라는 매개변수가 있지만 요소값을 그대로 받기 때문에)

---

### Map 객체

```js
const testMapObj = new Map();

console.log(testMapObj); // Map(0) {}

// size
console.log(testMapObj.size); // 0

// set()
testMapObj.set('StringKey', 'StringValue');
testMapObj.set(1, 1000);
testMapObj.set({objectkey: 'objectkey'}, 'objectkey');
testMapObj.set(true, false);
testMapObj.set(function() {console.log('Hi, Map!')}, 'functionKey');
/*
Map(5) {
  'StringKey' => 'StringValue',
  1 => 1000,
  { objectkey: 'objectkey' } => 'objectkey',
  true => false,
  [Function (anonymous)] => 'functionKey'
}
*/

// get()
console.log(testMapObj.get(true)); // fasle
console.log(testMapObj.get(1)); // 1000

// has()
console.log(testMapObj.has(0)); // false
console.log(testMapObj.has('StringKey')); // true

// forEach()
testMapObj.forEach(function(value, key) {
  console.log(key, ':', value);
})

// delete()
console.log(testMapObj.delete('string')); // false
console.log(testMapObj.delete(true)); // true

// clear()
testMapObj.clear();
console.log(testMapObj.size); // 0
```

- Object 객체처럼 `key: value`를 쌍으로 하여 데이터를 저장하는 객체.
- Object와 Map의 차이점
  - Map은 key로 어떠한 형태의 종류도 올 수 있다는 것. (Object의 경우 String 또는 Symbol)
  - Map은 저장한 순서대로 요소의 순서가 결정된다. (Object의 경우 순서가 보장될 수 없다)
- `Map()` 생성자 함수와 `new` 연산자를 이용하여 생성. 그냥 생성 시 빈 Map 객체를 생성하며, 반복 가능한 데이터를 전달하여 생성할 수도 있다.
- 관련 주요 속성
  - `size` : Map 객체의 크기를 반환(요소의 개수)
- 관련 주요 메서드
  - `set(key, value)` : 키와 값 데이터를 전달하여 Map 객체 내 요소를 저장한다.
  - `get(key)` : Map 객체에 저장된 요소에 해당하는 키를 전달하여 값을 얻는다.
  - `has(key)` : Map 객체 내에 해당 키를 가진 요소가 있는지 판별한다. 불린값 반환
  - `delete(key)` : Map 객체 내에 해당 키를 가진 요소를 삭제한다. 불린값 반환
  - `clear()` : Map 객체 내 모든 요소를 삭제한다.
  - `forEach(callback[, thisArg])` : Map 객체 내 모든 요소를 순회하며  callback 함수 내 로직을 처리한다.
    - 콜백함수의 매개변수로는 value, key, map 을 활용할 수 있다.

> 빈번한 추가 및 삭제, 순서가 중요시 되는 로직, 데이터가 많은 경우에 Map을 활용해볼 수 있다고 권장. 추후에 Map 객체를 사용하거나 관련 코드를 참고할 때 따로 정리하기 📝

---

### Math 객체

```js
const zero = 0;
const num1 = 1.1;
const num2 = 2.2;
const num3 = 3.9;
const num4 = 4.1234567;

// Math.round(), Math.ceil(), Math. floor(), Math.trunc()
console.log(Math.round(num1)); // 1
console.log(Math.ceil(num2)); // 3
console.log(Math.floor(num3)); // 3
console.log(Math.trunc(num4)); // 4

// Math.sign(), Math.pow(), Math.sqrt(), Math.abs()
const num5 = -10000;
const num6 = 10000;

console.log(Math.sign(num5)); // -1
console.log(Math.sign(num6)); // 1
console.log(Math.sign(zero)); // 0
console.log(Math.pow(10, 4)); // 10000
console.log(Math.sqrt(num6)); // 100
console.log(Math.abs(num3)); // 3.9
console.log(Math.abs(num5)); // 10000

// Math.min(), Math.max()
console.log(Math.min(0, 100, 20, -10, -99, 99, 2)); // -99
console.log(Math.max(0, 100, 20, -10, -99, 99, 2)); // 100

// Math.random()
console.log(Math.random()); // 0 <= ?? < 1 미만의 값
// 0 ~ 9 까지의 난수
console.log(Math.floor(Math.random() * 10));
// 0 ~ N 까지의 난수 : 바로 위 코드에서 10자리에 N+1을 곱한다.
// 0 ~ 2까지의 난수를 구할 때
console.log(Math.floor(Math.random() * 3)); //  0 <= N < 3 : 0, 1, 2
// 1 ~ N 까지의 난수 : 바로 위 코드에서 3자리에 N을 곱한 후 그 결과에 +1을 한다.
// 1 ~ 99까지의 난수를 구할 때
console.log(Math.floor(Math.random() * 99) + 1); //0 <= N < 99 : 0 ~ 98 에서  + 1

// 책에 나온 최소, 최대 범위 내 난수를 구하는 함수 예제
function getRandomInteger(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min; 
}

console.log(getRandomInteger(3, 10)); 
```

- 수학적인 연산 및 상수 등을 활용할 수 있는 객체
- 따로 생성자 없이 Math 객체 자체 내에 있는 속성과 메서드를 정적으로 사용한다.
  - 정적으로 사용한다는 말은 따로 인스턴스를 만들지 않고 바로 클래스에 접근하여 사용한다는 의미.
- 관련 주요 메서드
  - `Math.round(x)` : 전달된 수를 기준으로 **반올림**하여 가장 가까운 정수를 반환
  - `Math.ceil(x)` : 전달된 수를 기준으로 **올림** 처리하여 반환
  - `Math.floor(x)` : 전달된 수를 기준으로 **내림** 처리하여 반환
  - `Math.trunc(x)` : 전달된 수에서 **소수부분을 버리고 정수부**를 반환
  - `Math.sign(x)` : 전달된 수의 부호를 판별하여 반환. 반환값은 양수일 경우 1, 음수일 경우 -1, 0이면 0
  - `Math.pow(base, exponent)` : base에 exponent를 제곱한 값을 반환
  - `Math.sqrt(x)` : 제곱근(squre root)을 반환
  - `Math.abs(x)` : 전달된 수의 절대값을 반환.
  - `Math.min([value1[, value2[, ...]]])` : 전달된 수 중에서 가장 작은 값을 반환한다.
  - `Math.max([value1[, value2[, ...]]])` : 전달된 수 중에서 가장 큰 값을 반환한다.
  - `Math.random()` : **0이상 1미만의 구간 (0 <= ? < 1)**에서 부동소수점 의사난수를 반환

---

**참고 자료**

- [MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects)