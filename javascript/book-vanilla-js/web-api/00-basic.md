# JavaScript - Web APIs

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## Web APIs

- 웹 서버나 웹 브라우저를 위한 API.
- 웹 개발과 관련된 개념.
- 주로 클라이언트 측에서 많이 활용
  - 클라이언트 측에서 Web API에 접근한다는 것은 브라우저가 가지고 있는 API를 사용한다는 것. (Node를 이용한 로컬 환경에선 접근할 수 없다)
- 웹 생태계와 관련된 기술들에 접근할 수 있는 다양한 API가 존재한다.

> 여기서는 책에서 소개된 Web API를 기준으로 정리하기로 한다.

---

## LocalStorage, SessionStorage

- 브라우저가 가지는 저장소 (HTML5 에 추가)
- Web Storage API
  - sessionStorage, localStorage 를 제공
  - 동작하고 있는 페이지와 관련된 저장소를 제공(각각의 세부 개념은 아래에 따로 정리)
  - 각각의 저장소 객체가 가지는 메서드를 이용하여 브라우저 저장소에 데이터를 추가하거나 삭제할 수 있다.
  - 데이터는 객체 데이터처럼 key와 value 형태로 저장. 다만, 모든 값은 문자열로만 저장한다.
    - 주로 `JSON.stringify`를 이용하여 저장하고, 데이터를 가져올 때는 `JSON.parse`를 이용한다. (원래의 데이터 형태로 변환된다)
- 관련 메서드
  - 2개의 저장소 모두 아래의 메서드를 통해 데이터를 조회하고 삭제하는 등의 작업을 할 수 있다.
    - `Storage.key(index)` : 인덱스에 대응되는 key 이름을 반환
    - `Storage.getItem(keyName)` : keyName을 가진 키가 가지고 있는 값을 문자열로 반환. 없다면 null 을 반환한다.
    - `Storage.setItem(keyName, keyValue)` : keyName와 keyValue를 쌍으로 하는 데이터를 저장소에 등록한다. (문자열이어야 함)
    - `Storage.removeItem(keyName)` : keyName을 가지고 있는 key와 해당 값을 저장소에서 삭제한다.
    - `Storage.clear()` : 저장소 내 모든 데이터를 삭제한다.

### LocalStorage


```js
const students = [
  {id: 1, name: "gildong", age: 19},
  {id: 2, name: "chulsoo", age: 20},
  {id: 3, name: "younghee", age: 18},
]

function addStudents(students) {
  localStorage.setItem('students', JSON.stringify(students));
}

function getStudentInfo(id) {
  const students = JSON.parse(localStorage.getItem("students"));
  
  for (const info of students) {
    if (info.id === id) {
      console.log(`이름: ${info.name}, 나이: ${info.age}`);
    }
  }
}
function deleteStudent(id) {
  const students = JSON.parse(localStorage.getItem("students"));
  
  for (let i = 0; i < students.length; i++) {
    if (students[i].id === id) {
      students.splice(i, 1);
    }
  }
  
  localStorage.removeItem("students");
  localStorage.setItem("students", JSON.stringify(students));
}
function clearStorage() {
  localStorage.clear();
}


function init() {
  if (localStorage.length === 0) {
    addStudents(students);
  }
}

init();
getStudentInfo(2);
deleteStudent(2);
clearStorage();
```

- window.localStorage
- 데이터가 만료되지 않는 저장소
  - 페이지를 닫아도 저장되어 있던 데이터가 삭제되지 않는 이상 사라지지 않는다.
  - 페이지의 프로토콜은 구분된다. (각기 다른 localStorage에 저장 - ex. http vs https)
- 활용법
  - 보안에 위배되지 않거나 영구히 저장해도 상관없는 데이터 등
    - 사용자가 마지막으로 본 화면 URL
    - 웹 앱에서 설정 가능한 개인 테마, 개인화 등의 데이터
  - 브라우저의 개발자 도구 등에서 저장된 데이터를 확인할 수 있기 때문에 보안상 문제가 되는 데이터는 저장해선 안된다.
- 위 예제코드에선 5개의 관련 메서드를 다 활용하는 방식으로 작성해보았다.

> 위 예제에선 for문을 사용했지만 객체 데이터의 경우 내부 key들이 많아질수록 id를 특정해서 조회하거나 삭제할 때 단순히 반복문을 이용하면 안될 것 같다. (데이터가 100만개면...) 관련 예제나 자료구조 등을 학습한 뒤 따로 정리하기

### sessionStorage

- 세션 개념 저장소
  - 송수신자 간의 연결 상태를 유지할 때만 데이터 작업이 가능하다.
  - 브라우저 창을 닫는 순간 데이터는 자동으로 삭제

> localStorage 와 사용법이 동일하여 따로 코드로는 작성해보지 않았다. 앞 서 정리한 Storage 메서드를 활용하여 데이터 작업 가능. 화면 이동 간에 전달해야 하는 파라미터가 많은 경우 활용할 수 있다고 설명한다.

> localStorage와 sessionStorage 모두 같은 도메인 내에서 조회가 가능. 페이지 이동 시에도 같은 도메인이라면 저장소의 데이터를 활용할 수 있다. 단, 프로토콜은 구분됨을 유의(이 내용도 다른 에제가 있나 찾아봐야 겠다)

---

## Geolocation API

```js
// 현재 사용하는 브라우저에서 geolocation api 사용이 가능한지 확인
if ('geolocation' in navigator) {
  console.log("위치정보 사용 가능");

  // 콜백함수 처리. 여기선 success 시 콜백 함수만. 
  navigator.geolocation.getCurrentPosition((position) => {
    // position 객체 내 좌표 활용
    const latitude = position.coords.latitude; // 위도
    const longitude = position.coords.longitude; // 경도

    console.log(latitude, longitude);
  })

} else {
  console.log("위치정보 사용 불가능");
}
```

- 브라우저 사용자의 현재 위치 정보를 가져오는 API
- 위도(latitude) 및 경도(longitude) 데이터를 가져올 수 있다.
- navigator.geolocation 객체를 통해 사용
- 위치 정보 이용에 대한 권한 요청이 발생한다.
- 기본 사용법
  - `Geolocation.getCurrentPosition(success[, error[, options]])`을 이용하여 현재 위치 정보를 가져온다. 
    - 인자로 전달하는 success와 error는 위치 요청의 성공과 실패시 실행하는 콜백함수를 전달한다. 이 때 콜백함수에는 각각 GeolocationPosition, GeolocationPositionError 객체를 유일한 매개변수로 하여 전달한다. 전자는 위치정보가 담겨 있고 후자는 실패 원인이 담겨 있다. 이 객체를 함수 내부에서 사용하여 위도 경도나 위치 기록 시간 등을 활용한다.
  - 사용자의 이동에 따라 위치 정보를 처리하기 위해서는 `Geolocation.watchPosition(success[, error[, options]])` 메서드를 사용한다. 해제 시엔 `clearWatch(watchID)`를 사용.

---

## 추가내용 - encodeURI / decodeURI

```js
const encoded = encodeURI("http://domain.com?x=가나다라마바사");
console.log(encoded); // http://domain.com?x=%EA%B0%80%EB%82%98%EB%8B%A4%EB%9D%BC%EB%A7%88%EB%B0%94%EC%82%AC

const decoded = decodeURI(encoded);
console.log(decoded); // http://domain.com?x=가나다라마바사
```

- Web API는 아니지만 챕터에 추가적인 내용이 있어 정리
- encodeURI, decodeURI는 키워드 그대로 URI의 인코딩, 디코딩시 사용하는 표준 내장 객체
- ecodeURI
  - 특정 문자를 UTF-8로 인코딩하여 연속된 이스케이프 문자로 나타낸다.
  - URI나 URL이  한국어, 일본어, 중국어 등 영문자가 아닌 문자로 되어있는 경우 활용

> 책에는 Web Speech API 내용도 있었는데, 따로 정리하진 않고 깃헙 주소에 있는 예제코드만 확인하고 실행해 보았다. (음성 인식 관련 api)

---

## 정리

- Web API를 활용하기 위해서는 먼저 브라우저가 그러한 API 기능을 지원하는 지를 파악하고 이에 맞게 처리하는 것이 중요.
- 여기서는 일상에서 활용 가능한 것들로만 정리한 것 같은데(지도나 음성인식 등), 웹 생태계에서 사용되는 여러 개념이나 기술과 관련된 API가 무진장 많다는 것을 인지하고 관련 개념이 나왔을 때 활용해볼 수 있는 API가 있는지 찾아보는 식으로 학습하는 것이 좋을 듯 하다.

---

**참고 자료**

- [위키백과 - Web API](https://en.wikipedia.org/wiki/Web_API)
- [MDN - Web Storage API](https://developer.mozilla.org/ko/docs/Web/API/Web_Storage_API)
- [MDN - Window.localStorage](https://developer.mozilla.org/ko/docs/Web/API/Window/localStorage)
- [MDN - Geolocation API 사용하기](https://developer.mozilla.org/ko/docs/Web/API/Geolocation_API/Using_the_Geolocation_API)