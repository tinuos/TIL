# JavaScript - 반복문

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 반복문

- 프로그래밍 언어에서는 특정 코드블럭을 반복적으로 실행할 수 있는 반복 구문을 제공한다.
- JS에선 다음과 같은 반복문이 있다.
  - for 문
  - for - in 문
  - for - of 문
  - while 문

### for 문

```js
for ([initialization]; [condition]; [final-expression]) {
  // 반복 실행할 코드
}
```

- 위 용어들은 MDN 문서에서 참고하여 쓴 표기. (용어가 중요한게 아니라 어떻게 처리되는지가 중요)
- `initialization`
  - 시작 초기화
  - 반복문 시작 시 처음에 단 한번 실행.
  - 보통 `let i = 0` 과 같이 초기 변수의 값을 설정한다.
- `condition`
  - 반복 조건
  - 코드 블럭 실행 전 평가할 조건
  - 보통 앞 서 설정한 시작 변수 초기값과 반복할 횟수까지의 범위를 비교하는 형태로 사용. 이러한 비교 조건이 거짓이 될 경우 반복이 멈춘다. - ex. `i < 10`
    - 배열 내부의 요소를 반복할 경우 배열 길이와 비교하기도 한다.
- `final-expression`
  - 각 반복문의 코드블럭이 실행된 후 평가할 식을 설정하는 곳.
  - 보통 증감연산자(++, --)를 이용하여 앞 서 작성한 시작 변수의 값이 조건 범위를 넘어갈 수 있도록 설정한다. (반복이 중단될 수 있도록) - ex) `i++`

### for - in 문

```js
for (const key in object) {
  // 실행할 코드
}
```

```js
const forInTest = {
  a: 1,
  b: 2,
  c: 3
}

for (const key in forInTest) {
  console.log(key + " : " + forInTest[key]);
}

/*
"a : 1"
"b : 2"
"c : 3"
*/
```

- 문자열로 지정된 키를 갖는 모든 열거 가능한 속성을 반복하는 반복문
- 객체 내에 지정된 키의 수만큼 반복을 실행
- 배열 데이터(Array)를 전달하게 되면 내부 인덱스 번호를 키로 사용하게 된다.

### for - of 문

```js
for (const element of iterable) {
  // 실행 코드
}
```

- Array, Map, String 등 iterable 한 객체에서 사용 가능한 반복문
- for문 처럼 반복 조건을 설정할 필요없이 전달하는 데이터의 내부 요소의 갯수만큼 반복할 수 있다.
- 아래는 문자열 데이터의 for - of 문 예제

```js
let stringTest = "JavaScript";

for (const x of stringTest) {
  console.log(x);
}
```

### while 문

```js
while (조건식) {
  // 실행코드
}
```

```js
let count = 0;

while (count < 5) {
  console.log(count);
  count++;
}
```

- 조건식이 **true**일 경우에만 실행하는 반복문
- true일 경우 계속 반복하기 때문에(무한루프) 일반적으로 반복을 종료할 변수와 조건식을 같이 사용한다. for문에서 반복 종료를 위해 초기 시작변수와 반복 조건 및 증감식을 사용하는 것과 비슷하다. (2번째 예제코드 참고)

#### do ~ while 문

```js
do {
  //실행할 코드
} while (조건식);
```

- while문과 비슷하지만 실행 코드 묶음이 무조건 한번 실행된다는 차이점이 있다.

> for와 while은 조건식 및 증감 연산을 통해 종료 조건을 설정한다는 게 비슷하게 보인다. 책에서는 for 문은 특정 반복 횟수를 예측할 수 있을 때(배열의 요소를 반복하거나 특정 횟수만 반복하고 싶을 때), while의 경우 어떤 특정한 조건을 만족하는 동안 반복을 진행하고 싶을 때 활용하면 효율적으로 문제를 해결할 수 있다고 설명한다. 실제 개발하거나 알고리즘 문제를 많이 풀어보면서 활용해봐야 겠다.

---

**참고 자료**

- [MDN - for](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for)
- [MDN - for ... in](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...in)