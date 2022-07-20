# 자바스크립트 - 화살표 함수와 기본 매개변수

> [실시간 모니터링 시스템을 만들며 정복하는 MEVN](http://www.yes24.com/Product/Goods/104208010) 도서를 학습하며 정리한 내용입니다.

---

## 화살표 함수(Arrow Function)

```js
{
  (parameters) => {
    // 함수 실행 로직

    // [return]
  }
}
```

- ES6에 추가된 구문으로, 함수 표현식의 간편한 대안
- 화살표 함수를 이용하면 함수를 좀 더 깔끔하게 작성할 수 있다.
- 화살표 함수는 일반 함수와는 다른 특징을 가지며, 이는 함수 사용에 있어 제한점으로 작용할 수 있다.
- 익명 함수로만 사용. 함수 표현식처럼 사용하거나 콜백 함수로 많이 활용.

### 화살표 함수 기본 구문

- 화살표 함수는 매개변수 사용과 함수 실행 블록에 있어서 다른 형태를 가질 수 있다.

```js
// 1. 매개변수 관련

// 1-1) 매개 변수가 없는 경우
const testA = () => { console.log("Test Arrow Functions") };
testA();

// 1-2) 매개 변수가 여러개인 경우
const testB = (num = 0, a, b, c) => { return num + a + b + c; };
console.log(testB(10, 1, 2, 3));

// 1-3) 매개 변수가 하나인 경우
const testC = text => { console.log(text) };
testC("Hello JavaScript!!");

// 2. 함수 실행 블록 관련

// 2-1) 실행 블록에서 한 줄만 처리하는 경우
const testD = text => console.log(text);
testD("한 줄 실행은 암묵적으로 return으로 처리된다.");

// 2-2) 한 줄이지만 객체 리터럴을 반환하는 경우
const testE = () => ({ name: 'gildong', age: 20 });
console.log(testE());

// 2-3) 여러 줄로 작성되는 경우
const testF = (sum = 0, a, b) => {
  sum = a + b;
  return sum;
}
console.log(testF(0, 100, 1000));
```

- 매개변수가 하나일 땐 `()`를, 함수 실행 구문이 한 줄일 땐 `{}` 표기를 줄일 수 있다는 것이 특징.
- 실행 구문이 한 줄 일때는 암묵적으로 return으로 처리된다고 한다.
- 객체 리터럴을 한 줄로 하여 리턴 처리하는 경우 구문 표기인 `{}`와 구분하기 위해 `()`로 감싸준다. (위 예제 2-2 참고)

### 화살표 함수 내에서 this가 가지는 의미

#### 일반 함수 this

- 자바스크립트에서 함수 호출 시에는 arguments, this를 암묵적으로 전달받는데, 이 중 this는 함수 호출 방식에 따라 바인딩할 객체가 동적으로 결정된다.

```js
// 내부함수

// 1) 일반함수 안 내부함수
function normalFunc() {
  console.log(this.toString()); // [object global] or [object window]

  function innerFunc() {
    console.log(this.toString()); // [object global] or [object window]
  }

  innerFunc();
}

normalFunc();

const testObj = {
  name: "gildong",
  address: "Seoul",
  sayMyName: function() {
    console.log(this.name); // gildong
    // 2) 메서드 내 내부함수
    function plusAddress() {
      console.log(this.address); // undefined
    }
    plusAddress();
  },
  sayHello: function() {
    // 3) 콜백함수
    setTimeout(function () {
      console.log(this.name); // undefined
    }, 1000)
  },
} 

testObj.sayHello();
testObj.sayMyName();
```

- 내부 함수 호출 시
  - 일반함수, 콜백함수, 메소드 내 선언된 함수의 경우 어떠한 것이든 상관없이 this는 전역객체(브라우저는 window, 노드는 global)를 바인딩한다.
- 객체 내 메소드 호출 시
  - 객체 내 메소드 내부의 this는 해당 메소드를 호출한 객체에 바인딩 된다. (위 2) 내용 중 gildong)
  - `prototype` 객체 메서드도 일반 메소드처럼 호출 객체에 바인딩 된다.
- 생성자 함수 호출 시
  - `new` 연산자를 이용하여 함수를 호출하는 것으로 객체를 생성한다.
  - 이 경우 함수 안에 this가 정의되어 있다면 해당 this는 생성자 함수를 통해 생성되는 객체를 가리킨다. (new 없이 호출할 경우에는 전역 객체를 바인딩한다)

> 정리하자면 함수의 호출 방식에 따라 this가 바인딩(가리키는 대상)되는데 생성자 함수, 객체 메서드 방식의 호출을 제외한 모든 함수의 내부 this는 전역 객체를 가리킨다. (모든 내부 함수, 콜백 함수)

#### 화살표 함수의 this

- 화살표 함수는 함수 선언시 this에 바인딩할 객체가 정적으로 결정된다고 한다.
- 즉, 일반 함수는 호출 방식에 따라 this 바인딩이 동적으로 결정되지만, 화살표 함수 내 this 바인딩의 경우 정해져 있는 방식이 있다는 것.
- 화살표 함수의 this 바인딩은 **화살표 함수를 둘러싸는 상위 스코프의 this를 가리킨다.** MDN에선 이를 일반 변수 조회범위를 따르는 것이라 하는데, 현재 범위에서 존재하지 않는 this를 찾을 때 바로 바깥 범위에서 this를 찾는 것으로 검색을 끝내는 방식이라 한다.

```js
function Person(){
  this.age = 0;

  setTimeout(() => {
    this.age++; // |this|는 Person 객체를 참조
    console.log(this);
  }, 1000);
}

var p = new Person();

console.log(p.age);
```

- 위 내용은 생성자 함수를 통해 객체를 생성하는 MDN의 예제코드이다.
- 앞 서 new 연산을 통한 생성자 함수를 호출하는 경우에 this는 함수가 생성하는 객체에 바인딩된다는 것을 알아보았다.
- setTimeout() 함수 내에 화살표함수를 콜백으로 사용했는데 이 경우 Person으로 바인딩 된 this를 사용할 수 있게 되어 age에 접근이 가능해진다.
- 위 예제만으로는 이해가 잘 되지 않아 다른 예제를 살펴보았다.

```js
const testObj = {
  value: 0,
  testMethod: function() {
    console.log(this); // testObj
    this.value++;

    setTimeout(() => {
      console.log(this);  // testObj
      console.log(this.value); // 1
    }, 1000);
  }
}

testObj.testMethod();
```

- 객체 메서드 내 this는 객체를 가리키는 데 코드를 보면 setTimeout 에서 콜백으로 실행한 화살표 함수가 가지는 this가 상위 스코프(메서드)에서 바인딩된 객체를 가리키는 것을 확인할 수 있다.

```js
function arrow() {
  setTimeout(() => {
    console.log(this);
  }, 1000)
}

function noArrow() {
  setTimeout(function() {
    console.log(this);
  }, 1000)
}

const p1 = new arrow();
const p2 = new noArrow();
```

- 위 내용은 책에 나온 예제 코드.
- MDN 예제와 비슷한 내용인데 setTimeout 사용시 일반 함수 표현식과 비교한 내용
- 생성자 함수 호출 시 화살표 함수의 경우 arrow 함수에서 바인딩된 this(arrow())를 그대로 사용한다. (상위 스코프)
- setTimeout 함수의 경우 스택에서 실행되지 않고 따로 백그라운드에서 호출되어 실행되는 함수로 this 가 호출된 곳에서 바인딩된다고 설명한다.

### 화살표 함수를 사용하면 안되는 경우

- poiemaweb 에 정리되어 있는 내용으로 다음과 같이 설명
  - 메소드 정의 및 프로토타입 할당
    - 객체의 상위 컨텍스트인 전역 객체가 this 바인딩이 되어 this를 객체 멤버 참조용으로 활용할 수 없다. (ES6 축약 메소드 표현 사용 권장 `methodName() {}`)
  - 생성자 함수
    - 생성자 함수는 prototype 속성을 가질 수 있지만, 화살표 함수는 prototype 속성을 가질 수 없다. 사용 시 구문 오류 발생. (prototype에 대해서 추후 따로 정리하기)
  - addEventListener 함수의 콜백 함수
    - 콜백 함수로서 화살표 함수를 사용할 경우 함수 내부 this는 상위 컨텍스트인 전역객체로 바인딩되어 버린다.
    - 따라서, 요소를 특정한 객체로 바인딩 하려면 일반 함수 표현식을 이용하여 이벤트 리스너에 바인딩된 객체를 가리키도록 한다.

> prototype 내용을 제외하면 모두 화살표 함수가 갖는 this 바인딩 특성 때문에 발생. 즉, 객체를 this로 바인딩하여 활용할 때에는 일반 함수를 사용하기.

---

## 정리

- 함수 호출에 따른 this의 동적 바인딩에 대해 학습 (일반 함수, 내부 함수, 콜백 함수, 생성자 함수, 객체 메서드 함수 등)
- 화살표 함수는 상위 컨텍스트에서 바인딩 된 this 를 참조(?)하는 정적 바인딩을 한다.

> 자바스크립트가 this를 처리하는 방법, 특히 생성자 함수와 prototype 에서의 바인딩 되는 과정을 좀 더 찾아보고 정리해야 겠다. (this가 바인딩 되는 시기??)

---

**참고 자료**

- [MDN - 화살표 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Poiemaweb - 화살표 함수](https://poiemaweb.com/es6-arrow-function)
- [Poiemaweb - this](https://poiemaweb.com/js-this)