# 자바스크립트 - 배열 내 요소를 확인하는 메서드들

> [실시간 모니터링 시스템을 만들며 정복하는 MEVN](http://www.yes24.com/Product/Goods/104208010) 도서를 학습하며 정리한 내용입니다.

---

## 배열 내 요소를 확인하는 메서드들

- 책 내용 기준 `find`, `findIndex` / `includes` 에 대하여 학습 (+ indexOf)

### find, findIndex

```js
const students = [
  {name: '길동', scores: {math: 30, eng: 75, kor: 55}},
  {name: '철수', scores: {math: 25, eng: 50, kor: 100}},
  {name: '영희', scores: {math: 88, eng: 85, kor: 97}},
  {name: '민수', scores: {math: 90, eng: 60, kor: 67}},
];

const highMathScore = e => e.scores.math >= 80;

const firstStudent = students.find(highMathScore);
const firstStudentIndex = students.findIndex(highMathScore);

console.log(firstStudent);
console.log(firstStudentIndex);
```

```
arr.find(callback(element[, index[, array]])[, thisArg])
arr.findIndex(callback(element[, index[, array]])[, thisArg])
```

- 2개의 메서드들 모두 배열 내에서 콜백함수 조건을 만족하는 요소를 찾는 것과 관련있다.
  - find의 경우 콜백함수 조건을 만족하는 요소를 찾을 경우 해당 요소를 반환한다. 이 때 인덱스 0부터 lentgh - 1까지 중 가장 먼저 해당하는 요소를 반환한다. (뒤에 요소가 콜백함수 조건을 만족하더라도 반환되지 않는다. 위 예제 중 민수) 
  - findIndex는 find와 처리가 비슷하지만 반환값으로 해당 요소가 배열에서 가지고 있는 인덱스를 반환한다.
  - 배열에서 해당 요소를 찾지 못한 경우 find는 `undefined`, findIndex는 `-1`를 반환한다. (아래 코드 참고)

```js
const students = [
  {name: '길동', scores: {math: 30, eng: 75, kor: 55}},
  {name: '철수', scores: {math: 25, eng: 50, kor: 100}},
  {name: '영희', scores: {math: 88, eng: 85, kor: 97}},
  {name: '민수', scores: {math: 90, eng: 60, kor: 67}},
];

const highEnglishScore = e => e.scores.eng >= 90;
const firstStudentName = students.find(highEnglishScore);
const firstStudentIndex = students.findIndex(highEnglishScore);

console.log(firstStudentName);
console.log(firstStudentIndex);
```

### includes

```js
const conturies = ['Belgium', 'Brazil', 'China', 'Egypt', 'England', 'South Korea'];

console.log(conturies.includes('south korea')); // false
console.log(conturies.includes('South Korea')); // true

console.log(conturies.includes('China', 1)); // true
console.log(conturies.includes('China', 2)); // true
console.log(conturies.includes('China', 3)); // false
```

```
arr.includes(valueToFind[, fromIndex])
```

- 배열 안에 해당 값이 존재하는 지 판별할 때 사용하는 메서드로 존재하면 true를, 존재하지 않으면 false를 반환한다.
  - 값으로 문자랑 문자를 비교 시 대소문자를 구분한다.
- 2번째 인자로 인덱스를 전달하여 배열 내에서 판별할 시작 위치를 지정할 수도 있다.
- 참고로 ES7 에서 나온 문법으로 성능 상 ES5의 indexOf 보다 훨씬 좋다고 한다.

### indexOf

```js
const conturies = ['Belgium', 'Brazil', 'China', 'Egypt', 'England', 'South Korea'];

console.log(conturies.indexOf('south korea')); // -1
console.log(conturies.indexOf('South Korea')); // 5

console.log(conturies.indexOf('China', 1)); // 2
console.log(conturies.indexOf('China', 2)); // 2
console.log(conturies.indexOf('China', 3)); // -1
```

```
arr.indexOf(searchElement[, fromIndex])
```

- 배열 내에서 찾으려고 하는 요소가 가지는 인덱스를 반환하는 메서드.
- 배열 내 요소가 없을 경우 `-1`을 반환한다.

---

## 정리

- includes를 사용하냐 indexOf를 사용하냐의 차이는 사용하려는 반환값인 것 같다. 즉, 단순히 확인 목적으로 불린값을 활용하느냐, 아니면 인덱스 값을 이용하여 다른 처리를 하느냐 정도.
- 다만, 책에서는 인덱스값도 findIndex가 성능이 훨씬 좋다고 설명하고 있어 indexOf라는 문법이 있다라는 것만 확인하면 될 것 같다.
- 정리해보자면, 배열 내에 요소를 찾아 요소 값 자체를 활용할 때는 find, 요소를 찾아 해당 인덱스를 활용할 때는 findIndex(or indexOf), 요소 유무를 확인하여 처리할 때는 includes를 활용하기.

---

**참고 자료**

- [MDN - Array.prototype.find()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
- [MDN - Array.prototype.findIndex()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)
- [MDN - Array.prototype.includes()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)
- [MDN - Array.prototype.indexOf()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf)