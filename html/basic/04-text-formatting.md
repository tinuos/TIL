# HTML - 텍스트 관련 추가 학습

**목차**

- [설명 목록](#설명-목록)
- [인용구](#인용구)
- [약어](#약어)
- [연락처](#연락처)
- [첨자 표기](#첨자-표시)
- [코드 표현](#코드-표현)
- [시간 및 날짜](#시간과-날짜-표시)

---
---

## 설명 목록

- ul, ol 등의 기본 목록과는 다른 형태의 목록 방식

### `dl` 태그 사용
  - description list
  - 용어 사전, 메타데이터(키, 값) 형태의 내용을 표현할 때 주로 사용
  - dl 내부에서 용어는 `dt`(description term) 태그를, 용어에 대한 정의는 `dd`(description definition) 태그를 사용
  - 브라우저에선 기본적으로 용어의 정의 부분에서 들여쓰기 형태의 스타일이 적용된다.

--- 

## 인용구

- 요소가 가질 수 있는 블럭 또는 인라인에 따라 다른 요소를 사용

### blockquutes

- 블록 레벨 컨텐츠의 섹션이 인용된 경우 사용
- `blockqoute` 태그 사용
  - 해당 요소에서 `cite` 속성을 이용하여 출처 표기

### Inline quotations

- 줄 안에 적용되는 짧은 인용구
- `q` 태그를 사용
  - blockqoute 처럼 `cite` 속성을 이용하여 출처 표기

### Citations

- 위 blockqoute나 q 태그 외에 `cite` 태그를 이용하여 저작물의 출처를 표기할 수도 있다.
- cite 태그는 콘텐츠를 포함해야 하며(인용 제목), 기본적으로 브라우저 상에서 기울임 꼴로 표시된다.
- MDN 에서 [사용일람](https://developer.mozilla.org/ko/docs/Web/HTML/Element/cite#%EC%82%AC%EC%9A%A9_%EC%9D%BC%EB%9E%8C) 확인해보기

---

## 약어

- 줄임말을 표현하기 위해 사용

### abbr 태그

- abbreviation
- 머리글자나 약어를 나타내기 위해 사용
- 해당 요소에 title 속성을 지정하여 전체 글자를 표시할 수 있다. (호버시 툴팁 작동)

---

## 연락처

- 연락처 및 주소 사용

### address 태그

- 연락처 표기용으로 사용하는 태그
- 현재의 맥락에 따라 물리적인 주소, URL, 이메일, 전화번호, SNS, 좌표 등의 정보를 포함하여 사용 가능하다고 한다.
- 보통 모던 웹 페이지 레이아웃 중 footer 에 많이 활용

---

## 첨자 표시

- 첨자를 사용시 쓰는 태그 존재
  - 첨자는 문자의 상하나 좌우에 덧붙여 부가적인 의미를 부여하는 문자를 의미
- 보통 수학식이나 날짜 등에 올바른 의미를 부여하기 위해 사용

### 사용 태그

- `sup`
  - superscript
  - 위로 활자가 인라인 텍스트로 배치된다.
  - 더 작게 표현되며 기준선 위로 표시
  - 지수, 서수 표현이 대표적
    - `<p>x<sup>2</sup></p>`
    - `<p>20<sup>th</sup></p>`
- `sub`
  - subscript
  - 아래로 활자가 인라인 텍스트로 배치된다.
  - 더 작게 표현되며 기준선 아래로 표시
  - 각주나 변수 등의 표기에 자주 사용된다.
    - sup와 사용법 동일

---

## 코드 표현

### code 태그

- 일반적인 컴퓨터 코드를 나타내기 위해 사용

### pre 태그

- 편집기에서 작성한 내용 그대로 표시
- 브라우저가 공백이나 줄바꿈을 무시하는 반면, pre 태그를 사용하면 편집기에 작성된 그대로 렌더링된다.

> 이 외 var, kbd, samp 등의 태그는 나중에 활용할 때 자세히 정리하기

---

## 시간과 날짜 표시

- 텍스트로 작성된 날짜를 기계가 판독할 수 있도록 하기 위함

### time 태그

```html
<p>The concert took place on <time datetime="2001-05-15 19:00">May 15</time>.</p>
```

- 시간의 특정 지점 또는 구간을 나타낼 때 사용
- `datetime` 속성을 이용하여 시간을 정의할 수 있다.
  - 속성값은 계산상의 문제로 인해 지정된 유형만 작성되어야 한다.
  - [사용 가능한 datetime 값 예시](https://developer.mozilla.org/ko/docs/Web/HTML/Element/time#%EC%9C%A0%ED%9A%A8%ED%95%9C_datetime_%EA%B0%92)
- time 요소에 지정된 시간을 활용하여 알람이나 일정 추가 등의 기능을 구현할 수 있다.

---
---

## 참고자료

- [MDN | Advanced text formatting](https://developer.mozilla.org/ko/docs/Learn/HTML/Introduction_to_HTML/Advanced_text_formatting)
