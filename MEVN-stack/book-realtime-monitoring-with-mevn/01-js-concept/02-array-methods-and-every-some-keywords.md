# 자바스크립트 - 배열 메서드와 every, some 메서드

> [실시간 모니터링 시스템을 만들며 정복하는 MEVN](http://www.yes24.com/Product/Goods/104208010) 도서를 학습하며 정리한 내용입니다.

---

## 많이 활용하는 배열 메서드 정리

- 책에서는 앞 서 정리한 화살표함수와 함께 많이 활용하는 배열 메서드들을 정리. 학습할 내용은 다음과 같다.
  - forEach
  - map
  - filter
  - reduce

### forEach

```js
function Students() {
  this.list = [];
}

const aClass = new Students();

aClass.list.push('gildong', 'chulsu', 'minsu', 'youngwoo');

aClass.list.forEach((studentName, index) => {
  console.log(`${index + 1} : ${studentName}`);
})

/*
1 : gildong
2 : chulsu
3 : minsu
4 : youngwoo
*/
```

```
arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```

- 배열 데이터에 존재하는 요소를 각각 반복할 때 사용하는 메서드
- 콜백함수를 인자로 받아 내부적으로 각 요소마다 실행한다.
  - 콜백함수의 인자로는 순서대로 `요소 값`, `요소 인덱스`, `순회 중인 배열`로 전달하여 콜백함수 내부에서 사용할 수 있다.
- 요소를 순회하며 처리하고자 할 때 주로 사용하며, 반환값은 undefined 이다. (메서드 체인의 중간 단계로 사용할 수 없다)

### map

```js
// 1.
const numList = [1, 2, 3, 4, 5];
const doubleList = numList.map((num) => num * 2);

console.log(doubleList); // [1, 2, 3, 4, 5]

// 2.
const numList2 = [10, 3, 24, 12, 53, 36, 33, 25, 74];
const oddList = numList2.map(num => {if(num % 2 === 1) return num;});

console.log(oddList); // [undefined, 3, undefined, undefined, 53, undefined, 33, 25, undefined]

// 3.
const numList3 = [1, , 3, , 5];
const doubleList2 = numList3.map(num => num * 2);

console.log(doubleList2); // [ 2, <1 empty item>, 6, <1 empty item>, 10 ]
```

```
arr.map(callback(currentvalue[, index[, array]])[, thisArg])
```

- forEach 문과 유사하지만 반환값이 달라진다. 각 요소를 순회하며 실행한 콜백함수의 결과를 모아 새로운 배열로 반환한다.
- 모든 요소의 콜백 실행의 반환 결과를 새로운 배열에 반영한다. 즉, 명시적 반환이 없더라도 (JS에서 명시적 반환이 없는 경우 함수 실행 시 undefined를 반환) undefined가 포함되는 것을 확인할 수 있다. (위 예제코드 2. 참고)
- 배열 값이 없는 경우에는 콜백 함수가 호출되지 않는다. 콜백함수를 호출하지 않으니 반환값 자체가 없고, undefined가 할당되지 않는 것을 확인할 수 있다.(위 예제코드 3. 참고)

### filter

```js
const numList1 = [1, 2, 3, 4, 5];
const oddList1 = numList1.filter(num => num % 2 === 1);

console.log(oddList1); // [ 1, 3, 5 ]

const numList2 = [2, 4, 6, 8, 10];
const oddList2 = numList2.filter(num => num % 2 === 1);

console.log(oddList2); // []
```

```
arr.filter(callback(element[, index[, array]])[, thisArg])
```

- map과 비슷하나, 각 요소를 순회하며 콜백 함수를 실행할 때 함수내 조건을 만족하는 요소만 모아 새로운 배열로 반환한다.
  - `true로 강제하는 값`으로 반환하는 것을 함수 내 테스트 조건으로 설정한다. (`Truthy` : Falsy가 아닌 모든 값)
- 어떠한 요소도 통과하지 못한 경우 빈 배열을 반환한다.

### reduce

```js
const numList = [1, 2, 3, 4, 5];

let reduceCount = 0;

let sumWithInitial = numList.reduce((previousValue, currentValue) => {
  reduceCount++;
  console.log(reduceCount, ': prev - ', previousValue, '/ current - ', currentValue);
  return previousValue + currentValue;
}, 100);
console.log(sumWithInitial);
/*
1 : prev -  100 / current -  1
2 : prev -  101 / current -  2
3 : prev -  103 / current -  3
4 : prev -  106 / current -  4
5 : prev -  110 / current -  5
115
*/

reduceCount = 0;

let sumNoInitial = numList.reduce((previousValue, currentValue) => {
  reduceCount++;
  console.log(reduceCount, ': prev - ', previousValue, '/ current - ', currentValue);
  return previousValue + currentValue;
});
console.log(sumNoInitial);
/*
1 : prev -  1 / current -  2
2 : prev -  3 / current -  3
3 : prev -  6 / current -  4
4 : prev -  10 / current -  5
15
*/
```

```
arr.reduce(callback[, initialValue])
```

- 각 요소에 대해 리듀서 함수(콜백함수)를 실행하여 하나의 계산된 결과값을 반환한다.
  - 사전에서 리듀서(reducer)로 검색을 해보니 변형이나 축소를 담당하는 어떠한 물체나 사물을 의미. 리듀서 함수도 같은 맥락으로 해석하면 될 듯 하다. (하나의 계산된 결과값으로 처리되도록 도와주는)
  - map이나 fliter와는 다르게 배열이 아닌 원시 값을 반환한다.
- 콜백 함수 인자도 map이나 filter 등의 메서드와는 조금 차이가 있다.
  - 콜백 함수 내에서 누적 처리에 활용하기 위해 이전 값과 현재 값을 인자로 받는다.
- reduce 함수는 2번째 인자로 초기값을 받을 수 있다.
  - 초기값 설정은 옵션 개념으로 설정하냐 안하냐에 따라 실행 횟수가 달라지게 된다. (위 예제코드 참고)
  - 초기값 설정 시 첫 이전 값으로 초기값을 사용.(반복 횟수 : arr.length)
  - 그렇지 않은 경우 배열의 첫번째 요소가 이전 값으로 사용된다.(반복 횟수 : arr.length - 1)

---

## every와 some 메서드

- filter 메서드와 유사해 보이는 메서드들.
- 처리 방식과 반환값의 차이가 있다.

### every

```js
const emptyArray = [];

const numList1 = [-432, -12, -475, -34, -876];
const numList2 = [65, 78, -24, 15, -35, 98, 62];

function isAllNegativeNumber(element, index, array) {
  return element < 0;
} 

console.log(emptyArray.every(isAllNegativeNumber)); // true
console.log(numList1.every(isAllNegativeNumber)); // true
console.log(numList2.every(isAllNegativeNumber)); // false

```

```
arr.every(callback(element[, index[, array]]), thisArg)
```

- 콜백 함수 로직이 모든 배열 요소에 대해 참인 값(truthy)을 반환하는 경우 true를 반환. 하나라도 falsy를 반환하는 경우 false를 반환한다.
  - 논리 연산 중 AND 연산을 생각하기
- 빈 배열의 경우 무조건 true가 반환되는 것에 대해 유의할 것.
- 추가적으로 위 메서드의 경우 지원되지 않는 브라우저가 존재할 수도 있다고 한다. ([MDN 폴리필 내용 참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every#polyfill))
  - 폴리필(polyfill)은 웹 브라우저 상 지원되지 않는 기능을 지원하기 위하여 해당 기능처럼 동작하는 것을 다른 방법으로 구현하는 것을 말한다.(플러그인)

### some

```js
const emptyArray = [];

const numList1 = [-432, -12, -475, -34, -876];
const numList2 = [65, 78, -24, 15, -35, 98, 62];
const numList3 = [1, 2, 3, 4, 5];
 
function isSomeNegativeNumber(element, index, array) {
  return element < 0;
}

console.log(emptyArray.some(isSomeNegativeNumber)); // false
console.log(numList1.some(isSomeNegativeNumber)); // true
console.log(numList2.some(isSomeNegativeNumber)); // true
console.log(numList3.some(isSomeNegativeNumber)); // false
```

```
arr.some(callback(element[, index[, array]]), thisArg)
```

- every 함수와는 반대. 배열 요소 중 하나라도 콜백 함수에서 Truthy 값을 반환할 경우 true를 반환한다. 모든 요소가 falsy인 경우에 false를 반환
  - 논리 연산 중 OR 연산을 생각하기
- 빈 배열의 경우 무조건 false가 반환되는 것에 대해 유의할 것.
- every 메서드처럼 폴리필에 대한 내용이 있다.

---

## 정리

- forEach, map, filter, reduce 에 대하여 학습
  - forEach의 경우 반환값이 없는 형태 > undefined (메서드 체이닝에서 중간 단계로 활용할 수 없다.)
  - map, filter 의 경우 새로운 배열을 반환한다.
  - reduce는 리듀서 함수를 이용하여 최종 원시 결과값을 반환. 2번째 인자(초기값)의 유무에 따라 실행 횟수가 달라질 수 있다.
- 논리값을 반환하는 every, some 메서드
  - 콜백 함수의 반환값의 종류에 따라(truty or falsy) 논리결과값을 반환하는 메서드들
  - 배열의 모든 요소가 특정 조건을 만족하는지, 아니면 일부라도 만족하는지 등을 판별할 때 활용할 수 있을 것 같다.
  - **빈 배열을 판별하는 상황에선 유의하여 활용할 것**.(every - true, some - false 반환) 구현하려는 로직에 따라 따로 빈 배열을 확인하는 절차가 선행되어야 할 것 같다.
- 추가 내용
  - 위에 학습한 메서드들 중 reduce를 제외하고 모두 thisArg라는 2번째 인자를 가질 수 있다. 
  - 어제 화살표 함수를 학습하며 자바스크립트의 this 바인딩에 대해 간략히 살펴보기는 했지만, 위 메서드에서 활용하여 설명하기에는 무리가 있어 따로 정리하진 않았다. (수동으로 바인딩하는 것이 잘 이해되지 않았다)
  - 실행 컨텍스트와 렉시컬 스코프(?), 그리고 this 바인딩이나 함수에 대한 심화 내용을 정리한 후 따로 thisArg 활용에 대해 실습해봐야 겠다. (자바스크립트 처리 과정에 대한 심오한 이해가 수반되어야 할 듯... 😂)

---

**참고 자료**

- [MDN - Array.prototype.forEach()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)
- [MDN - Array.prototype.map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [MDN - Array.prototype.filter()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [MDN - Array.prototype.reduce()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
- [MDN - Array.prototype.every()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
- [MDN - Array.prototype.some()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/some)