# CSS - 개요 및 기본 문법

---

## CSS ?

- Cascading Style Sheets의 약자
- HTML, XML과 같이 구조화되어 있는 문서에서 각각의 요소를 특정하여 디자인하기 위한 언어
- HTML이 문서의 구조를 정의한다면 CSS는 스타일링을 위한 언어 - 각각의 역할이 나눠져 있어 명확한 구분이 가능

> HTML 처럼 CSS도 독자적인 문법이 존재. 단, CSS만으로는 의미가 없으며 HTML 내부에 포함되어 문서에 대한 디자인을 정의내릴 수 있을 때 의미가 있다.

---

## CSS 기본 문법

```css
h1 {
  color: white;
  font-size: 20px;
}
```

### 선택자

- selector, 셀렉터
- HTML 내부에서 스타일을 정의하기 위해 요소를 선택하기 위해 제공되는 수단
- 위 코드 예제에선 h1이 셀렉터

### 속성

- property, 프로퍼티
- `표준으로 정해져 있는 속성`을 이용하여 해당 요소에 다양한 스타일 지정이 가능
- 위 예제 코드에선 h1 요소에 color와 font-size라는 속성을 명시하여 관련 값으로 스타일을 지정한다.

### 값

- value
- 속성값
- 해당 속성에서 실질적으로 사용 가능한 값(키워드, 크기단위, 색상값) 등을 부여하여 스타일을 변경
- 위 예제 코드에선 white, 20px 등이 color와 font-size의 속성값으로 사용되었다.

### Rule set

- 위 예제코드와 같이 셀렉터에 특정 속성을 지정하여 하나의 스타일을 부여하는 것을 Rule set이라 부른다.
- Rule set을 통해 브라우저에게 특정 요소를 어떻게 렌더링할 것인지 명령을 내릴 수 있다.

---

## HTML과 CSS 연동

### CSS 미적용시

![image](https://user-images.githubusercontent.com/104971437/169240968-d46a2022-a9f2-40c6-bd1e-da5b330dbded.png)

- HTML이 CSS를 포함하지 않는다면 브라우저에서 기본적으로 적용되는 CSS에 의해 렌더링 된다.
- user agent stylesheets 라고 한다.
- 위 이미지는 chrome 브라우저 개발자 도구에서 styles 탭에서 확인 한 모습
  - 이미 다른 CSS 파일이 적용되어져 있기 때문에 기본 브라우저 스타일 시트의 값들이 지워져 있는 것을 확인할 수 있었다.

### Link Style

```html
<link rel="stylesheet" href="./css/styles.css">
```

- HTML에서 외부에 있는 스타일 시트를 로드하는 방식
- 가장 일반적인 방식
- `link` 요소를 이용하여 내부의 속성을 통해 CSS파일의 경로와 현재 문서와의 관계를 명시해준다.

### Embedding style

- HTML 내부에 style을 포함시키는 방법
- style 요소를 이용하여 주로 head 요소 내부에 스타일을 지정하는 방식
- 특별한 경우나 작은 규모의 페이지가 아닌 이상 권장되는 방식은 아니라고 한다. (HTML, CSS의 각각의 역할 구분에 따라 따로 관리되는 것이 바람직)

### Inline style

- 인라인 스타일
- 특정 요소 내부에 style 속성(attribute)을 통해 스타일을 직접 지정하는 것
- JS를 통해 동적으로 CSS를 생성할 때 사용되는 경우가 있다고 한다.
- 내장 방식과 더불어 특별한 경우가 아니라면 지양되어야 하는 방식

---

## Reset CSS

- CSS를 초기화(리셋) 하는 것
- 앞 서 살펴본 user agent stylesheet(브라우저 기본 스타일 시트)에 따라 따로 CSS 가 없어도 기본적인 스타일이 지정된다.
- 브라우저 별로 이러한 기본 스타일 시트의 초기값들이 제각각이기 때문에 이를 하나의 스타일로 초기화해주는 작업이 필요한 데 이를 Reset CSS라고 한다.
- poiemaweb 학습에선 자주 사용되는 Reset CSS로 Eric Meyer나 nomalize를 알려주고 있다.

> 위 Reset CSS 내용들을 참고하여 개발자가 필요로 하는 초기화 스타일를 완성해 나가는 것이 매우 유용하다고 설명.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-syntax)