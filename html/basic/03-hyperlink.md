# HTML - 하이퍼링크

**목차**

- [하이퍼링크 개념](#하이퍼링크)
- [URL과 path](#url과-path)

---
---

## 하이퍼링크

- 하나의 하이퍼텍스트 문서에서 다른 형식의 데이터 자료를 연결해주는 참조를 의미(고리, link)
- 이미지, 동영상, 음악, 파일, 글 등의 자료를 연결할 수 있다.
- HTML에서는 a 요소를 이용하여 다른 페이지의 문서를 연결하는 것이 대표적인 예

> 웹에서 문서형태로 정보를 교환하기 위해 HTTP라는 하이퍼텍스트 관련 통신 프로토콜(규약)과 HTML을 사용해야 한다. HTML 내에서 하이퍼링크를 사용하므로 다른 주소에 있는 프로그램을 연결 가능하게 해준다.

### a 요소

```html
<a href="https://www.naver.com" title="네이버 포털 사이트" target="_blank">Naver</a>
```

- 하이퍼링크를 만들기 위해 사용되는 요소
- 기본적으로 인라인 특성을 가진다.
- `href` 속성을 이용하여 다른 데이터를 참조.
  - URL 이 명시되어야 한다. (URL 아래 따로 정리)
  - 꼭 HTTP일 필요는 없으며, 브라우저가 지원 가능한 URL 스키마를 사용
- `target`
  - URL이 표시될 위치
  - 브라우징의 맥락(현재탭 또는 다른탭)에 따라 표시할 위치를 달리할 수 있다.
  - `_self`, `_blank`, `_parent`, `_top` 등의 키워드 값을 사용(자세한 내용은 [MDN](https://developer.mozilla.org/ko/docs/Web/HTML/Element/a#attr-target) 참고하기)
  - 예시로 나온 `_blank`를 사용하면 새로운 탭에 URL의 자료가 처리된다.
- `title`
  - 하이퍼링크 제목
  - 하이퍼링크에 대한 툴팁을 제공하는 속성 (부가정보)
  - 마우스 호버 시 작동

---

## URL과 path

### URL

- Uniform Resource Locater
- 한국어로 번역하자면 유일 자원 식별자(?).
- 특정 파일이 존재하는 주소에 대한 텍스트 문자열을 의미

### path

- 파일이 위치하는 경로를 뜻한다.
- 절대 경로
  - 루트부터 시작하여 파일이 위치한 곳까지의 모든 경로
  - 웹에서는 프로토콜(http or https)과 도메인 네임(ip주소를 대신하는 서버 이름)을 포함한다.
  - 절대 경로를 사용하면 현재 어느 경로에 있든 같은 장소를 가리킬 수 있다.
  - `https://www.examplepath.com/docs/test.html`
    - examplepath 라는 서버에서 docs 디렉토리 아래 test.html이라는 html 문서를 가리킴
- 상대 경로
  - 현재 있는 파일 경로에서 상대적인 위치를 가리키는 경로
  - `.`를 사용하면 현재 있는 경로를 나타내며, `..`은 상위 경로로 이동을 의미한다.
  - `./otherdir/test.html`
    - 현재 파일이 있는 경로 주변에서 otherdir 디렉토리 아래에 있는 test.html을 가리킴
  - 현재 위치가 가장 중요

> URL 및 도메인에 대한 내용은 나중에 따로 정리하기

---
---

## 참고자료

- [MDN | Creating hyperlinks](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)