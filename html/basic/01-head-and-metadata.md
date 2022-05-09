# HTML - head 요소 기초 정리

**목차**

- [head 요소](#head-요소)
- [metadata](#metadata)
- [favicon](#favicon)
- [css, js 적용](#css-js-적용)
- [문서 기본 언어 설정](#문서-기본-언어-설정)

---
---

## head 요소

- [html 기본](./00-basic.md)에서 간단히 정리했듯이 head는 HTML 문서에 대한 추가 데이터들을 포함하는 요소이며, 사용자에게는 브라우저 화면상에 표시되지 않는 영역이다.
- html 문서에 적용되는 스타일, 스크립트 등을 연결하거나 head 요소 내부에서 사용되는 특정 요소들을 이용하여 `메타데이터`를 작성한다.

---

## metadata

- 메타데이터
- 데이터를 설명하는 데이터란 뜻
- head안에 작성되는 요소들은 해당 html(데이터)을 설명하는 데이터(메타데이터)가 된다.

### head 내에서 사용되는 title 요소

- `title`
  - 브라우저의 탭 등에서 `페이지 전체의 제목`을 표현하기 위해 사용되는 요소
  - head안에서만 사용된다.
  - SEO(검색엔진최적화)에 영향을 주는 요소 중 하나 - [관련 내용 MDN 문서](https://developer.mozilla.org/ko/docs/Web/HTML/Element/title#%ED%8E%98%EC%9D%B4%EC%A7%80_%EC%A0%9C%EB%AA%A9%EA%B3%BC_seo)

### meta 요소

```html
<meta charset="UTF-8">
```

- base, link, script, style, title 등의 메타 관련 요소로 표현할 수 없는 데이터를 나타내기 위해 사용되는 요소
- 대표적인 예로 문자인코딩 설정
- meta 요소는 다음 4가지 유형 중 하나를 가진다.
  - name
  - http-equiv
  - charset
  - itemprop
- name 관련
  - name 을 메타데이터 이름으로 `content`를 값으로 하여 쌍으로 메타데이터를 정의
  - HTML 명세에 의해 표준으로 정의된 name 이 존재
    - 관련 [MDN 문서](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta/name)
  - 페이지의 저작자나 설명, 키워드 등을 정의할 수 있다.
  - CSS 표준에 따른 이름 명세도 있다. (대표적으로 모바일 기기와 관련된 viewport)

> http-equiv나 itemprop 특성과 관련해서는 나중에 http를 배우거나 해당 속성을 사용해야 할 때 찾아보기로 하자.

---

## favicon

- favorites icon의 줄임말
- 웹 사이트나 웹 페이지를 대표하는 아이콘을 의미한다.

### link 요소 사용

```html
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
```

- 위 예제와 같이 link 요소와 관련 속성을 이용하여 페이지의 파비콘을 추가할 수 있다.
- 파비콘은 브라우저의 탭에서 설정된 경로의 아이콘 이미지로 표시된다.
- 페이지가 열리는 디바이스에 따라 파비콘을 다양하게 설정해야 될 수도 있다. (기본, apple 등)

---

## CSS, JS 적용

- CSS는 페이지를 꾸며주는 스타일 관련 언어
- JS는 JavaScript의 약자로 사용자의 상호작용 및 페이지를 동적으로 조작할 수 있는 스크립트 언어(프로그래밍 언어)
- head에서 link와 script 요소를 사용하여 각각 CSS와 JS를 연결할 수 있다.
  - `<link rel="stylesheet" href="styles.css">` 처럼 head내 link 요소를 이용하여 CSS 파일을 연결한다.
  - js의 경우 script를 사용하는 데 script 요소의 경우 꼭 head 내에 위치하지 않아도 된다. (MDN 에선 body의 닫힌 태그가 끝나지 전에 배치하는 것이 더 좋을 수도 있다고 설명)
- 해당 HTML 문서와 상호작용 되도록 작성된 CSS와 JS는 HTML가 필요로 하는 하나의 데이터가 되는 셈

> script 요소를  body 요소 맨 뒤에 작성하는 것에 대한 내용은 브라우저의 작동 원리와 관련된 것으로 보인다. 간단히 찾아본 바로는 HTML의 요소를 모두 파싱(분석)한 후에 js 엔진에서 필요한 것들을 찾아가는 것이라 하는데.. 이에 대해서는 DOM과 JS엔진 및 브라우저 렌더링에 대한 이해가 필요한 것 같다. 일단, 추후에 관련 내용이 나올 때 따로 정리하기로 결정.

---

## 문서 기본 언어 설정

- 요소 내에 `lang` 이라는 전역 속성을 사용
- lang에 사용되는 값은 특정 언어 태그여야 한다. (ex. `en, ko 등`)
- html 요소에 lang 속성을 지정하면 SEO와 접근성 측면에서 더 효과적이라고 한다.
- 전역 속성이기 때문에 다른 요소의 속성으로도 사용 가능하다. 이는 부분적으로 다른 언어로 인식되게 만든다.

---
---

## 참고자료

- [MDN | What's in the head? Metadata in HTML](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)