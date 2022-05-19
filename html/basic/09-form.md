# HTML - 폼(form)

## form

- form 태그를 이용하여 다양한 입력 양식 태그를 포함하여 입력 처리 양식을 생성
- 사용자의 입력을 처리할 수 있는 기술
  - 웹사이트에 사용자가 데이터를 전송할 수 있다.
  - 폼 요소 내부에 입력에 필요한 위젯 요소를 이용하여 다양한 양식의 데이터를 입력 가능

```html
<form action="서버명" method="HTTP Request method">
  ~ 입력 양식 요소
  <input type="submit" value="submit">
</form>
```

- `action`
  - 입력되는 데이터가 전송될 URL 값을 지정한다.
- `method`
  - [HTTP request method](https://developer.mozilla.org/ko/docs/Web/HTTP/Methods) 의 값을 명시
  - 대표적으로 GET과 POST 방식이 있다.
    - GET의 경우 입력 데이터가 URL의 쿼리스트링으로 담겨 보내진다.
      - 데이터가 URL에 그대로 노출되기 때문에 보안의 문제가 있으며, 전송될 수 있는 데이터의 한계가 존재
    - POST의 경우 HTTP Request의 body에 담겨 보내는 방식
- `type="submit"`
  - input 이나 button 요소의 type을 `submit`으로 작성하면 form 내부에서 서버로의 제출의 역할을 하는 요소로 작동한다.
  - 사용자가 submit 요소를 클릭하거나 동작시키면 form 요소에 설정된 주소와 요청 메서드에 따라 서버에 존재하는 처리 로직에 입력 데이터가 전달된다.

> 추가적인 HTTP 학습이 필요하며 REST API라는 것도 확인하기

---

## input

- 사용자로부터 입력을 받을 수 있는 대화형 컨트롤 양식을 생성
- 다양한 데이터 입력 유형이 있으며 `type` 속성을 통해 설정할 수 있다.
- input은 form 내부에 있어야 서버로 전달되지만, `ajax` 으로 처리할 경우에는 단독으로 서버에 전송 가능(꼭, form 요소 내부에 존재하지 않아도 된다)
- input 요소 내에 name 속성을 설정하여 key로, value를 값으로 하여 `key:value` 형태로 서버에 입력 데이터를 전송한다.
  - value는 속성으로도 지정할 수도 있으나 type이나 위젯 형식에 따라 주로 사용자가 선택한 value를 값으로 사용한다.
- input는 전역속성을 포함하며 type에 따라 다양한 속성을 지정할 수 있으므로 조합시 잘 확인해야 한다.

### input 유형(type 종류)

- [MDN 정리](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#%3Cinput%3E_%EC%9C%A0%ED%98%95)
  - button
  - checkbox
  - color
  - date
  - datetime
  - email
  - file
  - hidden
  - image
  - month
  - number
  - password
  - radio
  - range
  - reset
  - search
  - submit
  - tel
  - text
  - time
  - url
  - week

### input 속성

- [MDN 정리](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Input#%EC%86%8D%EC%84%B1)
  - type, name, value, disabled 등 모든 input 유형에 사용 가능한 것들도 있고, checked와 같이 특정 요소에서만 유효한 속성이 존재

> ajax 용어 확인. Asynchronous JavaScript and XML. 비동기 웹 애플리케이션을 위한 개발 기법 중 하나. 나중에 JS 학습 시 따로 정리

---

## select

```html
<select name="fruits1">
  <option value="apple" selected>apple</option>
  <option value="banana">banana</option>
  <option value="grape">grape</option>
  <option value="cherry" disabled>cherry</option>
</select>

<select name="fruits2">
  <optgroup label="red-color">
    <option value="apple" selected>apple</option>
  </optgroup>
  <optgroup label="others">
    <option value="banana">banana</option>
    <option value="grape">grape</option>
    <option value="cherry" disabled>cherry</option>
  </optgroup>
</select>
```

- 여러 개의 목록에서 여러 아이템을 선택하고자 할 때 사용하는 입력 양식 요소
  - ul, ol 처럼 기본적으로 중첩되어 동작하는 요소 중 하나로 아이템 항목 선택을 위해 `option` 이란 태그를 사용한다.
- select의 name을 키로, option 요소의 value를 값으로 하여 `key:value` 형태로 서버에 전송된다.
- optgroup 태그를 이용하여 option을 그룹화할 수도 있다.

---

## textarea

- 여러줄의 글자 입력시 사용

---

## button

- 클릭 가능한 버튼을 생성하기 위해 사용
- input으로도 type을 button으로 하여 생성할 수 있지만 빈태그가 아니라는 점이 차이점
  - 텍스트나 이미지 등의 콘텐츠 삽입 사능
- type으로 button, reset, 그리고 input에서 설명한 submit 중 지정 가능하다.
  - 인터넷 익스플로러 지원시 IE 버전에 따라 submit일 경우 전송되는 값이 다를 수 있음을 주의

---

## fieldset, legend

- 입력양식을 그룹화하기 위해 사용
- legend 는 fieldset 내부에 배치되는 요소로 fieldset 요소의 제목을 정의

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/html5-tag-forms)
- [MDN - Your first form](https://developer.mozilla.org/ko/docs/Learn/Forms/Your_first_form)