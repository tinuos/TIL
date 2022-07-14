# JavaScript - REST API

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## API

![image](https://user-images.githubusercontent.com/104971437/178462131-773926b4-cd34-4524-89cb-ccba5285b9bb.png)

- Application Programming Interface 의 약자
- 일반적으로 소프트웨어 인터페이스를 의미.
- 인터페이스는 프로그램과 사용자가 상호작용할 수 있도록 도움을 주는 일종의 시스템을 말한다.
- 프로그램에 존재하는 기능들의 구현 내용을 알지 못해도 API를 이용하여 다른 기능과 통신하거나 그 자체 기능을 활용하여 프로그램 개발을 효율적으로 할 수 있다.
  - ex) 구글, 카카오 등의 지도 서비스. 네이버 등의 결제. 날씨 조회 등등

---

## REST API 정의

- REST - Representational State Transfer의 약자
  - 굳이 변역하여 이해해보자면 의미를 대신하는 상태 전송이라 할 수 있겠다.
- 상태는 자원, 즉 전송되는 데이터를 의미하며 이러한 자원을 이름으로 구분하여 주고받는 것이 REAT API 방식
- REST는 어떠한 기술이나 프레임워크, 라이브러리 등을 의미하는 것이 아니다. 네트워크 전송 방식을 구현하는 소프트웨어 아키텍쳐의 한 형식이다.
  - 소프트웨어 아키텍쳐 : 소프트웨어를 구성하는 요소들의 유기적인 관계를 표현하고 설계와 업그레이드를 통제하는 지침과 원칙
- API를 REST 방식으로 설계하고 제공하는 것을 REST API라고 하며, REST 원칙에 따라 구현되고 실행에 따르는 것에 RESTful 이란 용어를 사용.

> 아래부터는 [위키백과](https://ko.wikipedia.org/wiki/REST)와 책에 정리된 내용만 간추려 정리

### REST 기본 개념 및 활용 

- HTML, XML, JSON 중 일반적으로 `JSON 데이터`를 많이 주고 받는다.
- 웹에서 활용되는 기술과 HTTP 프로토콜을 그대로 사용
- 웹에서의 일반적인 REST API 처리과정 요약
  - 클라이언트
    - HTTP URI(Uniform Resource Identifier) 로 자원을 명시
    - HTTP Method(POST, GET, PUT, DELETE 등)를 이용하여 해당 작업의 CRUD를 요청
      - CRUD : Creat(생성), Read(조회), Update(수정), Delete(삭제)
      - HTTP의 메서드는 위 CRUD에 대응 (각각 POST, GET, PUT, DELETE)
  - 서버
    - 요청받은 URI 및 method 를 확인하여 구현 로직에 따라 JSON 데이터로 응답하거나 해당 자원을 처리한다.

> REST 적용 시 제한 조건 및 원칙 등의 추가적인 내용도 있다. 캐시나 계층화(네트워크) 등의 내용은 추가학습이 필요하며, REST 원칙에 따른 URI 작성법 등도 따로 정리가 필요. 일단, 여기서는 웹 상에서 REST API를 사용 시 주로 JSON 데이터로 주고 받으며, HTTP 메서드로 서버에게 자원 처리와 관련된 메시지를 전달한다라고만 정리해본다.

---

## JSON 서버를 이용한 REST 실습

> 책에 있는 간단한 실습 내용. 이 문서에 정리하지 않고 따로 저장소를 만들어 README에 정리.

- [실습 주소](https://github.com/tinuos/json-server-test)

---

**참고 자료**

- [위키백과 - REST](https://ko.wikipedia.org/wiki/REST)