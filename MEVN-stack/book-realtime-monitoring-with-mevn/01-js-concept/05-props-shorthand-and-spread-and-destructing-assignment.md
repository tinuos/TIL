# 자바스크립트 - 속성 표기 생략, 스프레드 연산, 구조분해 할당

> [실시간 모니터링 시스템을 만들며 정복하는 MEVN](http://www.yes24.com/Product/Goods/104208010) 도서를 학습하며 정리한 내용입니다.

---

## ES6 이 후 나온 유용한 구문들

- 책 내용 기준 속성 구문 생략, 스프레드 연산자, 구조분해 할당에 대하여 학습한다.
- 스프레드 구문과 구조분해 할당에서 분류별 예제 정리가 많아 소주제별로 숫자를 표기한다.

### 1. 속성 표기 생략 or 구문 생략

```js
let name = 'gildong';
let age = 19;
let address = 'Seoul';

// Property shorthand
const gildong = {
  name,
  age,
  address,
  sayMyName() {
    console.log(`My name is ${this.name}`);
  }
}

// No property shorthand
const gildong2 = {
  name: name,
  age: age,
  address: address,
  sayMyName: function() {
    console.log(`My name is ${this.name}`);
  }
}

gildong.sayMyName();
gildong2.sayMyName();
```

- 책에서는 구문 생략이라 표현
- ES6에서 나온 구문으로 객체 리터럴 방식에서 속성 이름과 속성값으로 사용하려는 표현식의 이름이 같은 경우 속성값 표기를 생략할 수 있는 문법을 말한다. (Property shorthand) 
- 추가적으로 메서드 또한 위 예제와 같이 약식 형태로 작성 가능하다.

### 2. spread 연산자

- ES6에서 나온 문법으로 이터러블 대상을 개별 요소로 분리하는 연산을 시행한다.
- 이터러블 대상이란 배열이나 Map, Set 등 반복 가능한 객체를 말한다. (이터러블과 관련해서는 추후에 따로 정리할 예정)
- 스프레드 연산자는 `...`를 사용하며 해당 연산 뒤에 개별 요소로 분리할 대상의 이름을 명시한다.
- 책에서는 4가지 방식으로 활용하는 것을 알려주고 있는데 관련 코드를 작성해보며 정리해보려 한다.

#### 2-1) 함수 인자 전달시, 함수의 rest 매개변수 활용 시


```js
console.log(...[1, 2, 3, 4, 5]); // 1 2 3 4 5

// 함수의 인수로 spread를 이용하여 전달
function test(a, b, c) {
  console.log(a, b, c);
}

test(1, 2, 3); // 1 2 3
test(...[1, 2, 3]); // 1 2 3

// 함수의 rest 파라미터
function test2(a, ...rest) {
  console.log(a);
  console.log(rest[0]);
  console.log(rest[1]);
  console.log(a, rest);
}

test2(1, 2, 3);
/*
1
2
3
1 [ 2, 3 ]
*/
```

- 함수 호출 시 스프레드 연산자를 이용하여 함수 선언에서 정의된 매개변수에 개별적으로 전달할 수 있다.
- 또한 함수에서 rest 파라미터를 설정할 때 스프레드 연산자를 이용하여 호출 시 들어오는 인자들을 모아 배열로 만들어 사용할 수 있다.
- 2가지는 엄연히 다른 방식으로 사용되는 것으로 전자는 함수 선언 시 설정한 매개 변수에 인자들을 뿌려주는 역할이며, 후자는 호출 시 전달되는 인자의 개수를 확정할 수 없을 때 활용해 볼 수 있는 방법이다.

#### 2-2) 배열 연결

```js
const aArray = [1, 2, 3];
const bArray = [4, 5, 6];

const cArray = aArray.concat(bArray);

console.log(cArray, 'length :', cArray.length); // [ 1, 2, 3, 4, 5, 6 ] length : 6
```

- ES5에서는 concat을 이용하여 배열을 서로 연결하여 사용했다.

```js
const aArray = [1, 2, 3];
const bArray = [4, 5, 6];

const cArray = [...aArray, ...bArray];

console.log(cArray, 'length :', cArray.length); // [ 1, 2, 3, 4, 5, 6 ] length : 6
```

- ES6에서 스프레드 연산자가 나오면서 배열 리터럴 내에서 바로 배열을 합치는 게 가능해진다.
- 각가의 배열에 존재하는 요소들을 개별 요소로 만든 뒤 다시 배열이 되는 형태이다.
- 책에서 저자는 concat 이나 스프레드를 사용하여 배열을 합칠 경우에 성능을 고려하여 활용하라고 조언한다. 각자의 프로젝트 환경에서 사용되는 배열의 특성(사용량, 깊이) 등에 따라 2가지 방식의 연산 성능이 달라질 수 있기 때문이라고 설명한다. 이러한 것을 고려하여 [jsbenchme](https://jsbench.me/)와 같은 성능 사이트를 참고한 후 활용하라고 권장한다.
- 아래 이미지는 책에서 제공하는 주소를 이용해 테스트해 본 결과의 모습
  - 10길이의 배열끼리의 결합과 100길이의 배열끼리의 성능 비교
  - 10길이일 때는 spread가 100길이일 때는 concat이 빠른 것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/104971437/180366978-8544babf-ba47-4098-b2b5-964fe9f53a17.png)

#### 2-3) Math.max, Math.min 전달 인자에 사용하기

```js
const numList = [98, 20, 4, 89, 35, 29, 10];

const maxValue = Math.max(...numList);
const minValue = Math.min(...numList);

console.log(maxValue, minValue); // 98 4
```

- 사실 2-1에서 정리한 내용과 같은 내용
- 여러 라이브러리 제공하는 함수나 실무에서 다른 동료가 작성한 함수 내부에서 여러 개의 인자를 받아 처리되는 것을 확인했다면 스프레드 연산자를 이용하여 전달할 수 있는지 잘 체크해보고 활용하자.

#### 2-4) 객체 복사

```js
const gildongProps = {
  name: "gildong",
  age: 20,
  address: "Seoul",
};

const gildong = {
  ...gildongProps,
  scores: {
    math: 99,
    eng: 99,
    kor: 99,
  }
}

console.log(gildong);

/*
{
  name: 'gildong',
  age: 20,
  address: 'Seoul',
  scores: { math: 99, eng: 99, kor: 99 }
}
*/
```

- 객체 내부의 속성과 속성값으로 분해할 때 스프레드 연산자를 사용할 수 있다.
- 위 예제를 풀어서 설명하자면, gildong이란 객체를 생성할 때 gildongProps라는 객체를 스프레드 연산자로 받아 해당 객체가 가지는 키와 값 쌍을 gildong 객체 안에 개별 속성으로 뿌려주는 형태이다.
- 책에서는 **객체 속성 복사를 위해 스프레드 연산자 사용 시 객체 내 깊이가 1일 경우에만 사용할 것**을 당부하고 있다. 
( `{` 다음에 바로 오는 속성들이 깊이가 1. 속성값 안에 또 다른 속성을 명시하여 그 속성값이 참조형 데이터일 경우 깊이가 점점 길어지는 것으로 이해했다)
  - 이 내용은 책의 중반부에서 한번 다룬다고 하니 그 때 따로 정리하려 한다. (일단 조금 찾아보니 얕은 복사와 깊은 복사에 대한 내용인 듯)

### 3. 구조분해 할당

- Distructing Assignment
- 구조 분해 할당, 비구조화 할당. 의미 그대로 배열이나 객체 등 구조적인 데이터가 가지는 요소나 속성을 분해하여 특정 개별 변수에 할당하는 문법이다.

```js
let a, b, c;

[a, b, c] = [1, 2, 3];
console.log(a, b, c); // 1 2 3

[a, ...rest] = [4, 5, 6];
console.log(a, rest); // 4 [5, 6]
console.log(b, c); // 2 3

[ , b, ] = [ , 100, ];
console.log(a, b, c); // 4 100 3
```

- 배열의 경우 분해되어 할당되는 기준은 `인덱스`가 된다.
- 위 예제와 같이 할당되는 배열 구조의 순서대로 분해 대상의 요소의 순서가 그대로 할당된다.
- 추가적으로 rest 파라미터를 이용하여 분해되는 나머지 요소들을 배열 데이터의 요소로 할당받아 활용할 수도 있다.

```js
const gildong = {
  personName: 'gildong',
  personAge: 19,
  personAddress: 'Seoul',
}

let {personName, personAge, personAddress} = gildong;
console.log(personName, personAge, personAddress); // gildong 19 Seoul

let {name, age, address} = {name: 'chulsu', age: 20, address: 'Jeju'};
console.log(name, age, address); // chulsu 20 Jeju
```

- 배열에서 추출과 할당의 기준이 인덱스였다면, 객체 구조분해 할당 시에는 `키(속성명)`가 기준이 된다.
- 할당하려는 변수명을 객체가 가지고 있는 속성명과 동일하게 1:1로 대응되게 작성하면 속성이 가지고 있는 값이 해당 변수에 할당된다.

```js
// swap logic

let a_1 = 1;
let temp = 0;
let b_1 = 2;

console.log(a_1, b_1); // 1 2
temp = a_1;
a_1 = b_1;
b_1 = temp;
console.log(a_1, b_1); // 2 1

// Using Destructing

let a_2 = 1;
let b_2 = 2;
console.log(a_2, b_2); // 1 2
[b_2, a_2] = [a_2, b_2];
console.log(a_2, b_2); // 2 1
```

- 추가로 구조분해 할당 구문을 이용하면 임시변수 등을 만들지 않고도 간단히 변수들이 가지는 값들을 스왑할 수 있다.

---

## 정리

- 자바스크립트 코드를 좀 더 간결하고 쉽게 작성할 수 있는 문법들에 대하여 학습해보았다.
- 스프레드 연산은 특히 함수의 매개변수 처리에서, 구조분해 할당이나 객체 속성 구문 생략은 해당 데이터를 활용할 때 유용하게 사용할 수 있을 것 같다.
- 일단 그냥 드는 생각은 학습을 진행하면서 쉬운 예제들로만 작성해서 테스트했기 때문에 지금은 눈에 잘 들어오지만, 만약 복잡한 로직에서 이러한 구문이 많이 사용된 경우는 어떨까하고 약간 걱정이 앞선다. 그런 혼란을 겪지 않기 위해서라도 위의 문법들에 익숙해지고 많이 사용해보는 수밖에 없겠다. .🤣

---

**참고 자료**

- [MDN - 객체 초기자](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Object_initializer#%EA%B5%AC%EB%AC%B8)
- [Poiemaweb - enhanced object property](https://poiemaweb.com/es6-enhanced-object-property)
- [Poiemaweb - extended parameter handling](https://poiemaweb.com/es6-extended-parameter-handling#3-spread-%EB%AC%B8%EB%B2%95)
- [Poiemaweb - destructing](https://poiemaweb.com/es6-destructuring)