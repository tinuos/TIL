# JavaScript - 클래스(Class) 기본 사용법

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 클래스

- 프로그래밍에서 클래스는 객체 지향 프로그래밍에서 특정 객체를 생성하기 위해 변수와 메소드를 정의하는 일종의 틀(template)을 말한다. ([위키백과](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9E%98%EC%8A%A4_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)))
- 클래스를 이용하면 효율적인 코딩이 가능하며 생성하려는 객체에 대해 표준화를 적용할 수 있다.
- 클래스에 변수나 메서드(함수) 등을 정의하면 클래스를 통해 생성된 객체는 해당 변수나 메서드를 사용할 수 있다.

> 여기서는 책 예제 코드를 참고하여 constructor, get, set 함수 등의 사용에 대해 간단히 정리한다.

### 클래스 정의

```js
class Pet {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  petInfo() {
    console.log(`이름 : ${this.name} / 나이 : ${this.age}`);
  }
}

const dog1 = new Pet('흰둥이', 2);
const cat1 = new Pet('길동이', 4);

dog1.petInfo(); // 이름 : 흰둥이 / 나이 : 2
cat1.petInfo(); // 이름 : 길동이 / 나이 : 4
```

- 자바스크립트에서는 `class` 키워드를 이용하여 클래스를 정의한다.
- 클래스는 선언 후 호이스팅 될 때 초기화가 되지 않으므로 **선언과 생성에 있어 순차적으로 이루어져야 한다.**
- 클래스에서는 `constructor`라는 함수를 가진다.
  - constructor 는 인스턴스 객체를 초기화(기본값 설정 등)하기 위해 사용한다. (인스턴스가 가지는 초기 속성)
  - 클래스 내에서 constructor는 단 1개만 존재해야 한다. (1개 이상 구현시 SyntaxError)
  - 클래스에서 생성자를 따로 정의하지 않을 경우 `constructor() {}` 라는 기본 생성자가 적용된다.
  - constructor 내부에서 변수 생성시에는 `this` 키워드를 이용하며, 인자로 전달받는 변수를 할당할 수 있다.(위 코드 참고)
- 메서드는 위와 같이 함수 형태로 정의하면 된다.

### get과 set

```js
class Pet {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  petInfo() {
    console.log(`이름 : ${this.name} / 나이 : ${this.age}`);
  }

  getName() {
    return this.name;
  }
  getAge() {
    return this.age;
  }

  setName(name) {
    this.name = name;
  }
  setAge(age) {
    this.age = age;
  }

}

const dog1 = new Pet('흰둥이', 2);

console.log(dog1.getName()); // 흰둥이
console.log(dog1.getAge()); // 2

dog1.setName('길동이');
dog1.setAge(3);

console.log(dog1.getName()); // 길동이
console.log(dog1.getAge()); // 3
```

- 책에서는 get과 set 메서드를 작성하여 클래스에 정의된 변수에 접근하거나 수정하는 방법에 대해 알려준다.
  - 사용 이유에 대해서는 나와있지 않는데, 구글링을 해보니 OOP 관점에서 데이터 무결성을 지키기 위한 방법이라고 한다.
  - 변수에 대한 직접적인 접근을 막음으로써 무결성을 지킨다는 것.
  - 이 내용에 대해서는 클래스 심화 학습을 하거나 OOP 내용을 공부할 때 따로 정리해야 겠다.
- get 또는 set 메서드 내에서는 constructor 처럼 this 키워드를 이용하여 변수에 접근한다.
  - get 메서드 구현
    - 클래스 내에 `get-` 접두사를 붙인 메서드를 생성하여 관련 변수값을 가져오도록 구현한다. 값을 반환하기 위하여 return 을 사용 (위 예제코드 참고)
  - set 메서드 구현
    - 클래스 내에 `set-` 접두사를 붙인 메서드를 생성하여 관련 변수가 가지는 값을 수정하도록 한다. 함수 인자로 수정하고자 하는 값을 전달한다.

### 클래스 상속

```js
class Pet {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  petInfo() {
    console.log(`이름 : ${this.name} / 나이 : ${this.age}`);
  }

  getName() {
    return this.name;
  }
  getAge() {
    return this.age;
  }

  setName(name) {
    this.name = name;
  }
  setAge(age) {
    this.age = age;
  }

}

const dog1 = new Pet('흰둥이', 2);

console.log(dog1.getName()); // 흰둥이
console.log(dog1.getAge()); // 2

dog1.setName('길동이');
dog1.setAge(3);

console.log(dog1.getName()); // 길동이
console.log(dog1.getAge()); // 3

// class Cat 
class Cat extends Pet {
  constructor(name, age, type) {
    super(name, age);
    this.type = type;
  }

  petInfo() {
    console.log(`이름 : ${this.name} / 나이 : ${this.age} / 종류 : ${this.type}`);
  }
}

const cat2 = new Cat('냥이', 3, 'CAT');

cat2.petInfo(); // 이름 : 냥이 / 나이 : 3 / 종류 : CAT
```

- 클래스는 다른 클래스를 상속받아 사용할 수 있다.
  - 보통 부모 자식 관계로 설명
  - 부모 클래스로부터 상속받은 변수나 함수 등은 자식클래스에서 그대로 사용할 수 있게 되며, 자식 클래스는 추가적으로 필요한 부분만 정의하여 사용할 수 있다.
- `extends` 키워드를 이용하여 상속받고자 하는 부모 클래스를 명시한다.
- constructor 에서는 `super()`를 이용하여 부모의 constructor 설정을 그대로 가져와 사용할 수 있다.
- 또한 부모에 존재하는 메서드로 다시 정의하여 사용 가능하다.

---

**참고 자료**

- [위키백과 - 클래스(컴퓨터 프로그래밍)](https://ko.wikipedia.org/wiki/%ED%81%B4%EB%9E%98%EC%8A%A4_(%EC%BB%B4%ED%93%A8%ED%84%B0_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D))
- [MDN - Classes](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)