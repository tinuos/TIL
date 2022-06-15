# CSS - 폰트 및 텍스트

- 폰트(글꼴) 및 텍스트 관련 스타일을 지정하는 속성에 대해 학습

---

## font 관련 속성

### font-size

- 텍스트의 크기를 지정
- `px`, `%`, `em` 등 길이단위를 이용
  - % 사용 시엔 부모 요소의 폰트 크기 기분 비율이 정해진다.
- `large` 등 폰트 크기 관련 키워드 값도 사용할 수 있다.

### font-family

- 선택 요소에 폰트를 지정하기 위해 사용.
- 여러 폰트 지정이 가능
- 명시된 순서대로 폰트가 적용될 수 있는지 판단 후 사용 가능한 폰트가 적용된다.
  - 컴퓨터에 해당 폰트가 설치되어 있거나, 웹 폰트로 다운받아 사용할 수 있는 경우 바로 적용
- 명시한 모든 폰트가 적용될 수 없는 상황을 위해서 `generic family` 를 따로 지정하는 것을 권장
  - fallback(대비책) font를 설정하는 것
  - generic family 로 구분되는 폰트들은 운영체제에 기본적으로 설치되어져 있다.
  - serif, sans-serif, monoscape, cursive, fantasy, system-ui 등의 폰트를 제일 마지막에 명시해 놓는다.
- 폰트명에 따라 띄어쓰기가 들어가는 경우 따옴표로 감싸주어 명시한다.

### font-style

- 폰트를 이탤릭체(기울임)로 지정할 때 사용하는 속성
- 다음과 같은 속성값을 가질 수 있다.
  - `normal` - 기본값
  - `italic` - 이탤릭체로 표현(기울임꼴)
  - `oblique` - 기울임 표현
  - italic과 oblique는 서로 보완적인 속성값 정도로만 알아 놓기.

### font-weight

- 폰트의 굵기를 지정할 때 사용하는 속성
- 폰트를 위한 숫자 형태의 가중치 값과 키워드 값을 사용한다.
  - 가중치값 - 100 ~ 900
  - `normal` - 400
  - `bold` - 700
  - `lighter`, `bolder` - [상대적 가중치](https://developer.mozilla.org/ko/docs/Web/CSS/font-weight#%EC%83%81%EB%8C%80%EC%A0%81_%EA%B0%80%EC%A4%91%EC%B9%98%EC%9D%98_%EC%9D%98%EB%AF%B8)

### font

- 폰트 관련 속성들을 단축하여 사용할 수 있는 속성
  - font-style
  - font-variant
  - font-weight
  - **font-size** - 필수
  - line-height
  - **font-family** - 필수

### line-height

- 텍스트의 높이를 지정할 때 사용하는 속성
- 숫자나 길이 단위, % 등의 값을 사용
  - `normal` - 기본값. 사용자의 브라우저에 설정된 기본 줄높이에 맞춰진다. (보통 1.2라고 함)
  - `숫자표현` - 요소의 폰트 사이즈를 기준으로 해당 비율로 계산되 적용된다. - ex) 16px \* **1.5** = 24
  - `길이 단위` - px, em 등
  - `%` - 요소의 폰트 사이즈 기준 백분율 크기

> 텍스트의 수직 중앙 정렬을 하기 위해 해당 속성을 활용하기도 한다. 블럭 요소의 높이값 그대로 line-height를 설정하게 되면 텍스트의 줄 높이가 해당 요소의 전체 높이에 맞춰져 중앙 정렬되는 것. 이러한 방식의 중앙 정렬은 해당 요소나 부모 요소의 높이가 고정되어 있고 그 값을 사용할 때에만 적용 가능하다는 한계가 있다. (line-height 에서 사용할 수 있는 %나 숫자표현 값이 요소의 폰트 사이즈가 기준이 되기 때문에 - 100%로 설정해도 font-size 기준 100%가 되기 때문에 실제 영역 높이와는 상관없이 중앙 정렬 되지 않는다) - [관련 내용 참고](https://oursmalljoy.com/css-%EA%B8%80%EC%9E%90-%EC%88%98%EC%A7%81-%EA%B0%80%EC%9A%B4%EB%8D%B0-%EC%A0%95%EB%A0%AC-text-vertical-align/)

## 텍스트 관련

- 글자 관련 스타일 속성

### letter-spacing

- 글자 사이의 간격을 조정
- 기본값이나 길이 단위 값이 적용된다.
  - `normal` - 기본값. 현재 글꼴의 기본 간격. 사용자 측에 따라서 임의로 간격이 조정될 수 있다.
  - `길이 단위` - px, em 등. **음수 값 지정도 가능**. 값이 커질수록 간격이 넓어진다.

### text-align

- 텍스트의 수평 정렬을 위해 사용하는 속성
- 다음의 키워드 값을 이용하여 텍스트의 수평 정렬을 적용한다.
  - start, end
  - left, center, right
  - justify 등

### text-decoration

- 텍스트에 장식용 선을 적용하기 위해 사용하는 속성
- `-line`, `-color`, `-style`, `-thickness`의 단축 속성
- underline 등의 키워드 값을 통해 밑줄을 생성하거나 none 을 이용하여 제거할 수 있다.

### white-space

- 요소의 공백문자 처리과 관련된 속성
- 다음과 같은 값을 사용한다.
  - `normal` - 기본값. 연속되는 공백을 하나로 합친다. **개행 문자도 다른 공백 문자와 동일하게 처리**. 넘칠 경우에는 자동으로 줄을 바꾼다.
  - `nowrap` - 연속되는 공백을 하나로 합치며, 줄바꿈은 `<br>` 요소에서만 발생
  - `pre` - 연속되는 공백을 유지한다. 개행 문자 및 br 요소에서만 줄바꿈 발생
  - `pre-wrap` - pre 값은 특성을 그대로 가지는 대신, 한 줄이 길어서 넘칠 경우 자동으로 줄을 바꾼다.
  - 이 외에 `pre-line`, `break-spaces` 등의 값이 있다.

### text-overflow

- 부모 영역을 넘어서는 텍스트가 존재할 때 해당 콘텐츠를 어떻게 숨길지 지정할 때 사용하는 속성
- 이 속성을 사용하기 위해서는 텍스트를 감싸는 컨테이너에서 다음과 같은 설정이 필요
  - width를 가져야 한다. (블럭 레벨 요소여야 한다)
  - 자동 줄바꿈을 방지하기 위하여 `white-space: nowrap;`을 설정한다.
  - overflow 속성을 반드시 visible 이외의 값을 지정(주로 hidden을 많이 사용)
- 다음의 속성값을 이용하여 텍스트를 사라지게 하거나 `...` 처럼 표현(ellipsis). 또는 지원하는 브라우저에 따라 커스텀 문자열로 표현할 수도 있다.
  - `clip` - 위 조건 충족시 기본값. 텍스트를 보이지 않게 한다.
  - `ellipsis` - 생략 부호(...)로 표현
  - 커스텀 문자열

### overflow-wrap

![image](https://user-images.githubusercontent.com/104971437/169833711-1c936662-2310-4bf5-b8ea-8c87395c139e.png)

- 하나의 단어가 영역을 넘어갈 때 처리 방법을 지정할 때 사용하는 속성
- 다음과 같은 속성값을 사용
  - `normal` - 기본값(?). 단어와 단어 사이의 공백을 기준으로 줄바꿈이 일어난다.
  - `break-word` - 영역을 넘치지 않도록 임의의 지점에서 줄바꿈이 일어난다. 

> poiemaweb에서는 이 속성명이 word-wrap 으로 소개되어 있다. 둘 다 같은 속성. [MDN 설명 참고](https://developer.mozilla.org/ko/docs/Web/CSS/overflow-wrap)

### word-break

- 텍스트의 영역 밖을 벗어날 때 줄바꿈 처리에 대해 지정하는 속성
- 다음의 속성값을 가질 수 있다.
  - `normal` - 기본값. 기본 줄바꿈 규칙 적용
  - `break-all` - 한중일(CJK) 텍스트를 제외하고 어떠한 두 문자 사이에서도 줄바꿈이 발생할 수 있다.
  - `keep-all` - 한중일(CJK) 텍스트에서 줄을 바꿀 때 단어를 끊지 않는다.

> overflow-wrap과 word-break 모두 아주 긴 단어 발생 시(링크 주소 같은) 처리할 때 용이. 보통의 영문자를 사용할 때는 overflow-wrap을 사용하면 되겠고, 한중일 문자를 사용할 경우엔 word-break를 참고해봐야 겠다.

---

- [poiemaweb](https://poiemaweb.com/css3-font-text)