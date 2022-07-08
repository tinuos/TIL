# 알고리즘 및 자료구조 학습 - 큐

> [프로그래머스 - 코딩테스트 광탈 방지 A to Z : JavaScript](https://programmers.co.kr/learn/courses/13213) 를 보며 학습한 내용을 개인적으로 정리한 문서입니다.

---

## 큐(Queue)

![위키백과 큐 이미지](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/330px-Data_Queue.svg.png)

- FIFO : First In First Out
- 먼저 들어간 데이터가 먼저 나오는 형태의 선형 자료구조
- 대표적인 예로 놀이기구를 기다리는 대기열 형태의 줄을 생각하면 된다.
- 용어 정리
  - Dequeue : 큐에서 나오는 것
  - Enqueue : 큐에 들어가는 것
- 큐의 종류
  - 선형 큐(Linear queue)
  - 환형 큐(Circular queue)

---

## 선형 큐 사용

### 배열로 표현

- 선형큐를 배열로 표현할 때 발생할 수 있는 상황
  - 배열의 크기가 정해져 있을 때 계속 Enqueue를 하게 된다면 Dequeue 했던 빈 자리로 요소들을 순차적으로 앞으로 끌어와야 하므로 선형 시간이 소요된다. (`O(N)`)

### 연결 리스트 사용

- 큐를 연결리스트로 구현하면 배열에서 발생할 수 있는 선형시간 문제(요소 위치 이동 관련)를 상수시간으로 해결할 수 있다.

---

## 자바스크립트에서의 선형 큐 사용

### Array 객체로 구현

```js
class Queue {
  constructor() {
    this.queue = [];
    this.front = 0;
    this.rear = 0;
  }

  // Enqueue
  enqueue(value) {
    this.queue[this.rear++] = value;
  }

  // Dequeue
  dequeue() {
    const value = this.queue[this.front];
    delete this.queue[this.front];
    this.front += 1;
    return value;
  }

  // 큐의 제일 앞 요소 확인
  peek() {
    return this.queue[this.front];
  }

  // 큐의 크기 확인
  size() {
    return this.rear - this.front;
  }
}

// 사용
const queue = new Queue();
```

- 강의에선 클래스 문법을 이용하여 선형 큐를 구현했다.
- Queue 클래스에선 인스턴스 생성 시 빈 배열을 가지는 queue 속성과 초기에 각각 0을 가지면서 큐의 인덱스로 활용할 front, rear 속성을 설정한다.
- Enqueue 동작 시 현재 인스턴스의 rear 값에 넣고자 하는 값을 할당한다.
  - `this.queue[this.rear++] = value;` 처럼 후위 증감연산자를 사용하면
  일단 처음 Enqueue 될 때 rear = 0 으로 인덱스에 값을 집어넣은 뒤 rear를 증가시키게 된다. 
- Dequeue 동작 시 현재 큐의 front에 위치한 요소를 삭제한 뒤 front 값을 증가 시킨다.
  - Dequeue 되는 값을 반환하기 위해 현재 front가 가지는 값을 특정 변수에 할당한다.
  - `delete` 키워드를 이용하여 현재 front에 위치한 요소를 삭제한다.
  - 이 후 front의 값을 1 증가시켜 dequeue 된 다음 요소를 바라보게 한다.
  - 반환값으로는 앞 서 할당한 값을 설정.
- peek는 현재 큐에서 제일 앞에 있는 요소를 보여주는 메서드. front 속성을 활용한다.
- size는 현재 큐에 저장된 요소의 개수를 반환한다. 

> 여기서 중요한 점은 큐 내에 인덱스로 활용할 front, back(rear)속성을 따로 지정해 놓은 것. 자바스크립트에서 Array 객체가 동적으로 늘어나는 것을 이용하여 이동 연산없이 큐를 구현하기 위해 사용한 방법같다. 실제 enqueue 나 dequeue를 여러번 해본 후 인스턴스를 확인하면 queue 속성 배열에서 앞 쪽에 빈 요소가 명시되는 것을 확인할 수 있다. (delete 연산)

### 추가 정리

- 연결 리스트로 큐 구현은 앞 서 연결 리스트 작성 시 했던 노드, pop, push 부분과 위 Array 내용을 참고하여 dequeue, enqueue 등을 구현하면 된다.
- Queue 구현 시 Array에서 사용 가능한 **`shift()`는 사용하지 말 것!!!!**
  - shift 기능은 배열의 제일 앞 요소를 제거 후 반환하는 메서드 (pop과 비슷)
  - 내부적으로 요소들의 위치 이동 연산이 발생하기 때문에 `O(n)`의 선형시간이 소요된다.

---

## 환형 큐(Circular queue)

- 일반 선형 큐에서 front와 rear가 이어져 있는 형태의 큐
- 자바스크립트에서 환형 큐 구현
  - 앞 선 선형 큐 방식에서 큐의 최대 크기를 설정하는 속성을 추가
  - 그리고 enqueue 시 최대 크기를 이미 초과했을 경우 더 이상 추가되지 못하도록 조건을 작성한다.

> 환형 큐에 대해서는 추 후 사용할 일이 있을 때 따로 정리하기.

---

**참고 자료**

- [위키백과 - 큐](https://ko.wikipedia.org/wiki/%ED%81%90_(%EC%9E%90%EB%A3%8C_%EA%B5%AC%EC%A1%B0))