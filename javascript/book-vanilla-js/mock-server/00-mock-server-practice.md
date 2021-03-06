# JavaScript - Mock 서버

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Mock 개념

- Mock 데이터, Mock 서버 등에서 사용되는 mock의 의미는 모조품, 즉 가짜의 의미를 담고 있다.
- Mock 서버는 가짜로 데이터를 주는 서버를 만들어주고 이를 활용하여 테스트 및 개발을 진행할 수 있다.
- 책에서는 API 관련 툴인 [postman](https://www.postman.com/)에서 제공하는 mock 서버로 간단히 진행
  - postman 에서는 API 사용과 관련된 다양한 기능들을 제공한다.
  - mock 서버 기능은 회원가입을 해야만 진행 가능

> 책에서 하는 실습 내용은 postman 프로그램을 이용해서 진행. postman의 mock 서버 기능의 간단한 설정 방법만 나와있어 따로 정리하지는 않았다.

---

## 정리

- 앞 서 정리한 JSON Server나 postman의 mock 서버나 모두 테스트 또는 개발 진행을 위해 가짜로 데이터를 전달받을 수 있는 서버를 만들어 쉽게 활용해볼 수 있다는 내용이다.
- 위 챕터 마지막에 실무 팁으로 mock 서버 등을 활용하면 협업 시 빠르게 개발을 진행할 수 있다고 알려준다. 일반적으로 실무에선 기획 -> 데이터(백엔드) -> 화면 구현(프론트엔드) 순으로 진행된다고 하는데, 백엔드에서 API 서버를 구현하여 제공하기 전까지 프론트에서는 기다리는 상황이 발생한다고 한다. 이 때 기획에서 정립된 데이터 구조를 JSON 형태로 바꿔 백엔드와 프론트엔드에 모두 넘겨주면, 프론트엔드는 위와 같이 가짜 서버를 이용하여 빠르게 화면 구현을 진행할 수 있게 되며 최종 단계에선 서버 주소로만 변경하면 된다.

---