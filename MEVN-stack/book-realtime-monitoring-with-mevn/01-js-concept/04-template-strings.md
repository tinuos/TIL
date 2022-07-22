# 자바스크립트 - 템플릿 리터럴

> [실시간 모니터링 시스템을 만들며 정복하는 MEVN](http://www.yes24.com/Product/Goods/104208010) 도서를 학습하며 정리한 내용입니다.

---

## 템플릿 리터럴을 이용하여 문자열 생성하기

- 기존 `"`, `'` 문자열 리터럴 방식보다 좀 더 간편하게 사용할 수 있는 템플릿 리터럴에 대하여 학습

### 리터럴??

```js
// 생성자 함수를 이용한 객체 생성방식

function Person(name, age, address) {
  this.name = name;
  this.age = age;
  this.address = address;
}

Person.prototype.sayMyName = function() {
  console.log('Hello! My name is "' + this.name + '".');
}

const gildong = new Person('gildong', 19, 'Seoul');

// 객체 리터럴을 이용한 객체 생성 방식

const chulsu = {
  name: 'chulsu',
  age: 20,
  address: 'Jeju',
  sayMyName() {
    console.log('Hello! My name is "' + this.name + '".');
  }
}

gildong.sayMyName();
chulsu.sayMyName();
```

- literal
- 프로그래밍 언어 안에서 데이터 타입이 가질 수 있는 값을 대표하는 용어라고 설명(위키백과)
- 대표적으로 자바스크립트의 `{}`을 이용한 객체 리터럴 방식이 있다. (위 에제 코드 참고 - 생성자 함수 vs 객체 리터럴 방식으로 간단히 작성해보았다)
- 개발 진행 관점에서 리터럴 방식은 일단 코드가 직관적이며, 단순히 열거하는 형태로 데이터를 손쉽게 작성할 수 있다라는 장점이 있다고 생각한다.

### 템플릿 리터럴

```js
// 일반 문자열

console.log("일반 문자열에서는 이스케이프 시퀀스를 이용하여 \n한 줄을 띄어 쓸 수 있습니다.\n");

// Template literals
console.log(`템플릿 리터럴 방식의
            문자열은
    공백 문자를 인식하기 때문에
이스케이프 관련 문자를 사용하지 않고도


자유롭게 사용할 수 있습니다.`);
```
- 템플릿 리터럴은 \`(백틱 기호. 보통 ~ 기호 키와 같이 있는 키. 숫자 1 옆)를 이용하여 문자열 데이터를 생성하는 구문을 말한다. 
- ES6에 나온 구문으로 템플릿 리터럴 이전에는 기본 문자열 리터럴을 이용하여 문자열을 생성했다.
- 템플릿 리터럴은 보간 처리가 가능하며, 줄바꿈 처리도 인식하기 때문에 보다 직관적이면서 쉽게 문자열 데이터를 생성할 수 있다.

#### 보간 처리

```js
const a = 10;
const b = 90;

console.log(a + ' 더하기 ' + b + '은 ' + (a + b) + '입니다.');
console.log(`${a} 더하기 ${b}은 ${a + b}입니다.`);
```

- 보간 처리에서 보간(interpolation)은 수학에서 두 지점간의 연결 위한 방법을 말한다.
- 많은 프로그래밍 언어에서 문자열 연결 처리를 위해 이러한 보간 기능을 제공한다.
- 자바스크립트의 일반 문자열에서는 `+` 연산을 이용하여 표현식을 처리가 가능했다. 템플릿 리터럴에서는 `${}` 표기법 내에 표현식을 넣어 표현식이 처리한 값이 문자열로 변환되어 다른 문자열들과 연결할 수 있다.
- 위의 간단한 예제코드만 봐도 알 수 있듯이 코드를 좀 더 직관적으로 해석할 수 있고 가독성이 훨씬 좋아진다.

---

**참고 자료**

- [위키백과 - 리터럴](https://ko.wikipedia.org/wiki/%EB%A6%AC%ED%84%B0%EB%9F%B4)
- [MDN - 템플릿 리터럴](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Template_literals)
- [Poiemaweb - 템플릿 리터럴](https://poiemaweb.com/es6-template-literals)