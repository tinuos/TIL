# 알고리즘 및 자료구조 학습 - 연결 리스트

> [프로그래머스 - 코딩테스트 광탈 방지 A to Z : JavaScript](https://programmers.co.kr/learn/courses/13213) 를 보며 학습한 내용을 개인적으로 정리한 문서입니다.

---

## 연결 리스트(Linked List)

- 연결 리스트
  - 각 요소를 포인터로 연결하여 관리하는 선형 자료구조
  - 각 요소는 노드(Node)라고 부른다. 데이터 영역과 포인터 영역을 가진다.
- 특징
  - 제한없이 요소를 추가할 수 있다. (메모리 허용 범위까지)
  - 탐색 시에는 `O(n)`의 시간이 소요된다.
  - 요소의 추가나 삭제 시엔 `O(1)`이 소요된다.
- 연결 리스트 종류
  - Singly Linked List
  - Doubly Linked List
  - Circular Linked List

### 배열과 연결리스트의 차이

#### 메모리 구조 차이

![image](https://user-images.githubusercontent.com/104971437/177474494-57fdc242-dfaa-4d20-a106-5d88039eab25.png)

- 배열의 경우 데이터가 메모리에 순차적으로 저장되는 반면에 연결 리스트는 포인터를 이용하여 저장되어 있는 영역을 따로따로 참조한다.

#### 조회, 추가, 삭제 등의 소요 시간 차이

![image](https://user-images.githubusercontent.com/104971437/177476139-7f577346-0ca1-4f2f-a485-ba56c79fd044.png)

- 배열의 경우 앞 서 살펴본 대로 추가나 삭제 시에 요소들의 이동이 필요하기 때문에 `O(n)`의 선형시간을 가진다.
- 연결 리스트의 경우 추가나 삭제시 포인터만 따로 지정하면 되기 때문에 `O(1)`의 상수시간을 가지게 된다.
- 조회 시엔 배열의 경우 인덱스만 알고 있다면 상수시간으로 조회 가능하지만, 연결 리스트는 헤드에서 부터 시작하여 탐색해야 하기 때문에 선형시간이 걸린다.

### 연결리스트 종류별 정리

#### 단일 연결 리스트

![image](https://user-images.githubusercontent.com/104971437/177492005-d9df9a74-f2c8-45bf-b9de-fb31e3011456.png)

- Singly Linked List
  - Head부터 Tail까지 단방향으로 이어지는 연결리스트로 가장 단순한 형태
  - tail의 포인터 영역을 null로 지정하여 더 이상 연결된 노드가 없음을 나타낸다.
  - 요소 찾기 : O(N) 소요
  - 요소 추가 : O(1) 소요
  - 요소 삭제 : O(1) 소요

#### 이중 연결 리스트

![image](https://user-images.githubusercontent.com/104971437/177493492-fdefa6b1-b383-4fa5-9602-3619fb08e427.png)

- Doubly Linked List
  - Head부터 Tail까지 양방향으로 이어지는 연결리스트. 단일 방향보다 자료구조의 크기가 조금 더 커진다.
  - 다음 노드와 이전 노드 참조를 위한 포인터를 갖는다.
  - 요소 추가와 삭제 시에는 단일 연결 리스트와 비슷하지만 이전 노드의 포인터도 따로 참조해줘야 한다는 차이점이 있다.
  - 요소 찾기 : O(N) 소요
  - 요소 추가 : O(1) 소요
  - 요소 삭제 : O(1) 소요

#### 환형 연결 리스트

- Circular Linked List
  - 단일 또는 이중 연결 리스트 에서 tail의 다음 노드를 head로 연결한 리스트. 

---

## 자바스크립트와 연결 리스트

- 강의에서는 class 문법을 이용하여 단일 연결 리스트를 구현하는 코드를 알려준다.
- class 구문은 따로 배우진 않아서 코드를 분석하면서 모르는 내용만 간략히 정리하려 한다.

```js
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class SinglyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  find(value) {
    let currentNode = this.head;
    while (currentNode.value !== value) {
      currentNode = currentNode.next;
    }
    return currentNode;
  }

  append(newValue) {
    const newNode = new Node(newValue);
    if (this.head === null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }
  }

  insert(node, newValue) {
    const newNode = new Node(newValue);
    newNode.next = node.next;
    node.next = newNode;
  }

  remove(value) {
    let preNode = this.head;
    while (preNode.next.value !== value) {
      preNode = preNode.next;
    }

    if (preNode.next !== null) {
      preNode.next = preNode.next.next;
    }
  }

  display() {
    let currentNode = this.head;
    let displayString = "[";
    while (currentNode !== null) {
      displayString += `${currentNode.value}, `;
      currentNode = currentNode.next;
    }
    displayString = displayString.substring(0, displayString.length - 2);
    displayString += "]";
    console.log(displayString);
  }
}

const linkedList = new SinglyLinkedList();
linkedList.append(1);
linkedList.append(3);
linkedList.append(4);
linkedList.append(5);
linkedList.display();
console.log(linkedList.find(3));
linkedList.remove(3);
linkedList.display();
linkedList.insert(linkedList.find(4), 100);
linkedList.display();
```

- Node와 SingleLinkedList 라는 클래스를 생성
  - Node의 경우 단일 연결 리스트에서 내부에서 사용할 자료 구조. 데이터 영역(value)과 포인터 영역(next)을 갖는 클래스로, 인스턴스 생성 시 데이터는 전달 값으로, 포인터는 null로 지정
  - SingleLinkedList는 생성시 head와 tail을 속성을 가지며, 초기에는 아무런 노드가 없기 때문에 null로 설정
- 조회 메서드 : find(value)
  - while 반복문을 이용하여 SingleLinkedList의 head 부터 순차적으로 찾고자하는 값을 탐색한다. 값이 갖지 않을 경우 노드가 가지는 다음 포인터(next)가 가리키는 노드를 설정한 가변 변수에 할당 받는다. 가변 변수의 시작은 head(여기서 this는 SingleLinkedList이다).
- 자료구조 맨 끝 노드 추가함수 : append(newValue)
  - head가 null이냐 아니냐에 따라 추가 방법이 달라진다. (아무것도 없는 상태라면 head, tail 모두 새로운 노드를 가리켜야 한다)
- 중간 삽입 함수 : insert(node, newValue)
  - Node 클래스를 이용하여 새로운 값을 가지는 노드를 만들고, 새로운 노드의 다음 포인터를 전달받은 노드의 next로 할당한다. 기존 node의 next는 새로운 노드로 지정
- 값을 조회 후 삭제 : remove(value)
  - 강사는 값을 조회 후 삭제하는 로직으로 구현(find 함수와 같이). 따라서 선형 시간이 소요된다.
  - 만약 특정 노드를 바로 삭제하는 것으로 구현하고 싶다면 insert와 같이 특정 노드를 전달인자로 주면 된다고 한다.

> 연결 리스트의 경우 코딩 테스트에서 많이 사용되지는 않는 자료구조라 한다. 일단 위 내용대로 개념 및 종류만 간단히 정리하고 넘어가고 추후 문제 풀 때 관련 내용이 나오면 블로그에 따로 정리해야 겠다.

---