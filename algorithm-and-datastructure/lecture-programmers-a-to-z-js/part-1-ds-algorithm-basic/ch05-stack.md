# 알고리즘 및 자료구조 학습 - 스택

> [프로그래머스 - 코딩테스트 광탈 방지 A to Z : JavaScript](https://programmers.co.kr/learn/courses/13213) 를 보며 학습한 내용을 개인적으로 정리한 문서입니다.

---

## 스택(Stack)

![image](https://user-images.githubusercontent.com/104971437/177680005-9f554f0f-c2e2-4141-ad37-d3fe788b3eb1.png)

- LIFO : Last In First Out
- 나중에 들어간 데이터가 먼저 나오는 선형 자료구조
  - 앞 서 들어가 있는 데이터를 꺼내기 위해서는 나중에 들어간 데이터들을 먼저 꺼내야 한다. (제한적인 접근 방식)
  - 데이터의 접근은 스택 입구에서만 일어난다.(목록의 끝이라고도 함)
- `push` : 스택의 가장 윗 부분에 메모리를 생성하여 데이터를 넣는다.
- `pop` : 스택의 가장 위에 있는 데이터를 반환한다.
- ex) 자바스크립트의 함수 실행은 스택 메모리 구조에서 실행된다. (콜스택)

## 프로그래밍 언어에서 스택 사용

### Array로 표현하기

- 배열 구조를 스택으로 활용한다.
- 자바스크립트의 경우 배열로 자주 활용되는 Array 객체는 동적으로 크기가 변하기 때문에 쉽게 스택으로 사용할 수 있다.

### Linked List로 표현하기

- 단일 연결 리스트로 표현
- C언어와 같은 컴파일러 언어에서 배열의 경우 크기를 고정해야 되기 때문에 위와 같은 연결 리스트로 스택을 구현하여 활용할 수 있다.

### 자바스크립트에서 스택 사용

- `Array` 객체를 이용하여 구현
- Array의 인스턴스 메서드인 push(), pop() 등을 사용한다.

---

## 실습) 올바른 괄호 문제

### 내가 푼 풀이

```js
function solution(s){
  let answer = true;
  const sArray = s.split('');

  let openCount = 0;
  let closeCount = 0;
  
  while (sArray.length > 0) {
    const popData = sArray.pop();

    // 닫는 괄호 없이 바로 여는 괄호로 시작되는 경우
    // - 답 변수 변경 & 반복 종료
    if (popData === '(' && closeCount === 0) {
      answer = false;
      break;
    }

    // 올바른 괄호 체크
    if (popData === ')') {
      closeCount++;
    } else if (popData === '(') {
      openCount++;
    }

    if (openCount === closeCount) {
      closeCount = 0;
      openCount = 0;
      answer = true; // *****
    } else {
      answer = false; // *****
    }
  }

  return answer;
}
```

- 스택 처리 과정을 참고하여 배열 관련 메서드로 풀었으나 처음에는 시간 초과로 통과하지 못 했다. 논리를 한번 정리한 후 추가로 코드를 작성하여 통과 아닌 통과를 할 수 있었다. (코드의 주석 \*\*\*\*\* 부분)
- 생각한 논리
  - 처음 pop을 하는 문자가 `(`일 경우 바로 반복문을 종료시키는 조건을 제일 먼저 생각하게 되었다.
  - 이 후 pop하는 문자를 체크하는 로직을 생각했는데 openCount, closeCount 변수를 만들어 동일성을 체크하게 했다.
    - 만약 2개의 개수가 같다면 올바른 괄호 조건을 통과하는 것
    - 만약 2개의 개수가 다르다면 통과하지 못한 것.
      - 조건을 만족하여 반복문 통과만을 고민하다 보니 스택의 맨 아래에 있는 문자의 처리를 생각하지 못 했던 것 같다. (ex. `)(())()` )
- 위 로직에서 문자열이 만약 `((())()())` 이런 경우라면 어떨까?
  - `(`, `)` 모두 개수가 같지만, 올바른 괄호 조건은 만족하지 못한다.
  - 하지만 위 로직에서는 카운트 개수가 맞다면 true가 반환되도록 했기 때문에 정답은 true가 된다.
  - 프로그래머스 테스트 케이스에서는 위와 같은 케이스가 없는 것 같아 통과되었지만 내가 푼 풀이 자체에 문제가 있다는 것을 확인할 수 있었고, 강사 풀이를 참고하기로 했다.

### 강사 풀이 참고

```js
function solution(s){
  const stack = [];

  for (const c of s) {
    if (c === '(') {
      stack.push(c);
    } else {
      if (stack.length === 0) {
        return false;
      }
      stack.pop();
    }
  }

  return stack.length === 0;
}
```

- 풀이를 보니 정말 간단하게 작성할 수 있었던 문제
- 스택 자료구조를 빈 배열로 만든 뒤 `(`이면 push, `)`이면 pop을 해주는 식이다.
- 이 때 올바른 괄호 조건을 만족하기 위해 빈 스택에서 `)`를 꺼낼 경우에는 false가 되도록 조건을 주는 것이 중요.
- 반복문은 요소 반복이 가능한 `for ~ of` 문을 사용했다.
- 이처럼 간단한 문제에서는 스택 구조를 사용하지 않고 정수 데이터로 비교하여 풀이할 수도 있다고 한다. (숫자 세는 변수를 하나 설정하고 pop은 -1, push는 +1 로 사용하는 것. 배열을 사용하는 것보다 메모리를 조금 줄일 수 있다)

---

**참고 자료**

- [위키백과 - 스택](https://ko.wikipedia.org/wiki/%EC%8A%A4%ED%83%9D)