# JavaScript - XMLhttpRequest

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## XMLHttpRequest

- 서버와 상호작용하기 위한 인터페이스 객체. 줄여서 `XHR` 이라 한다.
- 클라이언트 사이드 Web API 중 하나 (웹 브라우저가 사용하는 api. Node 에선 사용이 불가능하다)
- XHR을 이용하면 페이지를 새로고침하지 않고도 서버에 데이터를 보내거나 가져오는 등 여러가지 작업에 활용할 수 있다.
- AJAX 프로그래밍에 많이 활용
  - AJAX?
    - Asynchronous JavaScript and XML
    - 비동기 통신 처리를 가능하게 하는 웹 앱 제작 기법을 일컫는 말
- XML 외에 다른 모든 종류의 데이터를 가져올 수 있다.

> AJAX 따로 정리하기. 여기선 비동기 통신과 관련된 기법이라는 것만 간단히 이해하고 넘어간다.

### 간단한 사용법 정리

#### XHR 객체 생성

```js
const xhr = new XMLHttpRequest();
```

- 생성자 함수를 이용하여 xhr 객체를 생성한다.

#### 요청을 위한 정보 설정

```js
```

- `open(method, url[, async])`
  - 요청(request) 초기화 메서드
  - 서버와의 통신이 이루어져야하기 때문에 http 등의 프로토콜 관련 내용과 URL 정보를 포함시켜야 한다.
  - 3번째 인자는 비동기와 관련된 것으로, 기본값은 true 이다.
  - method 관련
    - HTTP 요청 방식 중 하나를 문자열로 정의한다.
      - `GET` : 리소스 요청
      - `POST` : 리소스 생성
      - `PUT` : 리소스 수정
      - `PATCH` : 리소스 일부 수정
      - `DELETE` : 리소스 삭제
- `setRequestHeader(header, value)`
  - HTTP 헤더에는 요청과 응답에서 부가적인 정보를 명시되어 전달될 수 있도록 해준다.
  - 위 메서드는 HTTP 헤더 내용을 설정하기 위한 것.
  - 메서드를 사용할 때는 open 이후, send 메서드 전에 호출하여 설정하여야 한다.
  - HTTP 헤더에 명시되는 내용들을 맥락에 따라 3가지로 그룹핑되며 보안이나 통신에 따라 여러 내용으로 나뉘는데, 여기서는 책 내용에 따라 `content-type`에 대해서만 정리하려 한다.
  - **content-type**
    - HTTP 메시지 바디(본문)에 담기는 데이터의 미디어 타입을 명시하기 위한 헤더 정보로, HTTP body에 담긴 리소스가 어떤 타입인지를 알려주는 역할을 한다.
    - 웹 개발에서 자주 사용되는 타입 포맷은 MIME. 자주 사용되는 타입은 아래 3가지
      - content-type: application/json - json 데이터 전송
      - content-type: text/plain - 일반 텍스트 파일 전송
      - content-type: multipart/form-data - 파일 전송
- `send([body])`
  - 앞 서 사용한 메서드들을 통해 정의한 내용을 바탕으로 요청을 보내기 위해 사용하는 메서드
  - 전달인자는 옵션. POST 방식에서 전달인자로 데이터를 전달하면 http request의 body에 담겨 전송된다.

#### 응답 처리

- 요청에 대한 결과 응답은 load 이벤트를 통해 이루어진다.
- load에 대한 이벤트 처리함수를 이용하거나 `onload` 속성으로 처리함수를 참조하여 응답에 대한 처리를 확인할 수 있다.

---

## XHR 실습

- 책에서 알려주는 [jsonplaceholder](https://jsonplaceholder.typicode.com/guide/) 사이트를 통해 xhr의 기본적인 사용법을 실습.
- jsonplaceholder는 [json server](https://github.com/typicode/json-server) 라는 fake REST API 서버로 서버에 저장된 데이터를 json 파일로 받아 다양하게 실습해볼 수 있도록 가이드를 제공해주는 사이트이다. 위 링크는 json server의 깃헙 주소로,  요청을 시도할 때 지정해야 하는 url을 좀 더 상세하게 참고할 수 있다.
- 저자는 posts 리소스에 관해 요청, 생성, 수정, 삭제 등을 진행했다.
- http 메서드를 이용하여 서버에 있는 데이터를 변경하는 것은 요청 초기화 시 전달인자만 바꿔주고 생성이나 수정 같은 경우엔 send 메서드에 데이터를 보내면 된다(JSON.stringify()를 이용). 
- 여기선 반복문을 이용하여 특정 id와 관련된 photos 리소스만 요청하는 실습만 진행해보려 한다.

```js
// photos 관련 id로 리소스 요청 (id 범위 : 1 ~ 10)

for (let i = 1; i <= 10; i++) {  
  // XHR 객체 생성
  const xhr = new XMLHttpRequest();

  // 1. 요청 초기화
  xhr.open('GET', 'https://jsonplaceholder.typicode.com/photos/' + i.toString());
  // 2. 요청 Header 설정
  xhr.setRequestHeader('content-type', 'application/json');
  // 3. 요청
  xhr.send();
  // 4. 응답 처리
  xhr.onload = () => {
    if (xhr.status === 200) {
      const res = JSON.parse(xhr.response);
      console.log(res);
    } else {
      console.error(xhr.status, xhr.statusText);
    }
  }  
}
```

- for 기본 반복문을 통해 1 ~ 10 까지 id로 photo 데이터를 요청해본 코드 예제
- xhr 객체는 요청 및 응답과 관련하여 다양한 속성과 메서드를 활용할 수 있다.
  - onload 처리 함수에서 `xhr.status`를 이용하여 응답시 상태코드를 통해 조건문으로 처리.
  - `xhr.response` 에는 응답 메시지 데이터가 담겨 있다. Json server 에서는 json 데이터가 있고, parse 메서드를 이용하여 자바스크립트 데이터로 변환하여 확인.

![image](https://user-images.githubusercontent.com/104971437/177354757-8bb85e9e-a18c-45f8-af4e-70768aeaec64.png)

> 반복문 i의 순서대로 로그가 순차적으로 찍힐 줄 알았으나, 출력 결과를 확인해보니 순서대로 나오지 않았다. open 메서드의 3번째 인자로 false를 넣어보았으나 원하는 결과는 나오지 않았다. 아직 DOM, load 이벤트, 비동기 처리에 대한 상세한 내용을 몰라 해결이 안되는 듯... (솔직히 뭐가 뭔지 모르겠다 🤣)
>
> 비동기에 관한 내용을 추가적으로 학습한 뒤 순차적인 요청 처리를 어떻게 하는지에 대해 고민해봐야 겠다. 📝

---

**참고 자료**

- [MDN - XMLHttpRequest](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest)
- [위키백과 - Ajax](https://ko.wikipedia.org/wiki/Ajax)
- [MDN - HTTP 헤더](https://developer.mozilla.org/ko/docs/Web/HTTP/Headers)