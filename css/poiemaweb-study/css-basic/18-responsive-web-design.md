# CSS - 반응형 디자인

- 디바이스 해상도에 따라 레이아웃을 변화시켜줄 수 있는 반응형 디자인과 관련된 내용을 학습

---

## Responsive Web Design

- 반응형 웹 디자인은 사용자의 디바이스 화면 해상도에 따라 레이아웃을 변화하게 하여 가독성을 높이는 것을 말한다.
- 여러 디바이스의 화면 크기에 최적화된 페이지를 제공하는 것이 목적
- 반응형 디자인은 별도의 기술이 아니라 기존 CSS3 표준 레이아웃 기능과 속성들을 이용하여 구현해내는 것.

### viewport와 관련 meta tag

- viewport : CS에서 뷰포트는 가시 영역을 뜻한다. 웹 브라우저에서 뷰포트는 창(window) 내에서 전체 문서 중 보이는 부분을 뜻한다. 콘텐츠의 내용이 길어져서 가로나 세로로 스크롤이 형성될 경우 스크롤링을 통해 뷰포트 부분을 이동할 수 있다. 디바이스 사용에 따라 뷰포트의 특성이 달라진다.
  - PC : 일반적으로 가로가 넓은 형태로 사용. resize 가능(창 크기 변화를 통해 뷰포트의 크기가 변경될 수 있다)
  - Tablet : 가로 or 세로. 일반 스마트폰보다는 화면이 크기 때문에 보통 상황에 맞게 변형하여 사용하게 된다. resize 불가능
  - Smart Phone : 주로 세로로 사용. 가로로도 화면 전환이 가능하지만 일반적으로 세로가 긴 형태로 많이 사용. resize 불가능

#### viewport meta tag

- 앞 서 html을 학습할 때 head 요소 내부에 meta 태그를 통해 브라우저나 SEO에게 웹 문서에 대한 추가적인 정보를 알려줄 수 있다고 배웠다.
- meta 태그의 name 종류 중 `viewport`라는 표준 메타데이터 이름을 명시하면 해당 요소는 디바이스에 대하여 초기 사이즈(브라우저 화면 설정)에 대한 정보를 전달해준다. (모바일 장치에서 사용하는 브라우저에게)
- 너비나 높이, 그리고 모바일 장치의 특성 상 확대 및 축소 등과 같은 속성 등이 존재하며 관련 속성과 속성값은 meta 태그의 `content` 속성 내에 명시하며, 여러 개일 경우 `,`를 이용한다.

|속성|설명|ex|
|:---:|:---:|:---:|
|width|뷰포트의 너비. 기본값은 980px이라고 한다.|`width=240` or `width=device-width`|
|height|뷰포트의 높이.|`height=800` or `height=device-height`|
|initial-scale|뷰포트 초기 배율|`initial-scale=1.0`|
|user-scale|확대 축소 가능 여부|`user-scale=no`|
|maximum-scale|뷰포트 최대 배율|`maximum-scale=2.0`|
|minimum-scale|뷰포트 최소 배율|`minimum-scale=2.0`|

**예시**

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

- poiemaweb 에서 알려주는 가장 일반적인 예로 가로폭을 디바이스의 가로폭에 맞추고 화면 배율을 100%로 설정하는 방법

```html
<meta name="viewport" content="width=device-width,initial-scale=1,minimum-scale=1,maximum-scale=1,user-scalable=no">
```

- 이 코드는 모바일용 네이버 홈(m.naver.com)의 메타태그.
- 최대 최소 배율은 설정한 배율과 동일하게 가져가고 사용자의 확대가 불가능하게 지정했다.

### @media

- 반응형 디자인의 핵심 기술
- CSS의 `@media`을 이용하여 미디어의 종류에 따라 스타일을 다르게 지정하는 것을 **미디어 쿼리**라고 한다.
- 디바이스의 종류 뿐만 아니라 해상도나 너비 등의 특성을 명시하여 구분할 수 있다.
- 논리 연산자를 통해 다수의 쿼리를 결합하여 디바이스를 특정할 수 있다.

#### 미디어 쿼리 기본 구문

```css
@media not|only 미디어타입 and (표현식) {
  CSS 스타일 규칙
  ...
}
```

**미디어 타입**

- `all` - 모든 장치
- `print` - 출력물에 적용할 스타일. (출력 기기의 미리보기 등에서 스타일이 바뀌는 것을 확인할 수 있다.)
- `screen` - 화면
- `speech` - 음성 장치
- 연산자 관련
  - `not` - 작성된 쿼리가 거짓일 때에만 적용. 반드시 미디어 유형을 지정해야 한다.
  - `only` - 전체 쿼리가 일치할 때에만 적용. 반드시 미디어 유형을 지정해야 한다.
  - `and` - 쿼리 결합. 다수의 미디어 특성을 결합하여 하나의 미디어 쿼리로 만들 때 사용한다.

**관련 속성**

- 관련 속성은 poiemaweb 에 나온 내용만 정리
- device-width, device-height, device-aspect-ratio 속성은 미디어 쿼리 관련 표준에서 삭제되었다고 MDN에서 확인하여 따로 정리하지 않았다. 디바이스의 물리적인 너비나 높이, 가로세로비에 관한 것.
- orientation을 제외한 나머지 속성은 모두 `max-` or `min-` 접두사를 사용할 수 있다고 한다. (최대 / 최소 지정)

|속성|설명|
|:---:|:---:|
|width|뷰포트 너비(px)|
|height|뷰포트 높이(px)|
|orientation|디바이스 방향 - 가로는 landscape, 세로는 portrait 이라 한다. (풍경화 / 초상화)|
|color|디바이스에서 표현할 수 있는 최대 색상의 비트 수|
|monochrome|흑백 디바이스의 픽셀 당 비트수|
|resolution|디바이스 해상도(픽셀 밀도)|

- 일반적으로 반응형 디자인에서는 뷰포트의 너비에 따라 미디어 쿼리를 적용한다고 한다.
- 예상되는 디바이스 너비 크기를 특정하여 뷰포트가 반응하는 지점을 설정. (breakpoint)

**예시**

```css
@media screen and (min-width: 480px) {
  body {
    background-color: lightgreen;
  }
}
```

- 유형이 screen 이고 뷰포트 최소 너비가 480px(480px ~) 일 때에는 배경색이 lightgreen으로 적용된다. (480px 이하로 뷰포트가 작아지면 해당 색상이 적용되지 않는다)

> min과 max 로 사용 시 최소, 최대 크기 구분을 명확히 할 것. 모바일 기준일 경우 너비를 최소 크기부터 시작하여 늘려나가고, 모바일 아닐 경우 최대부터 시작하여 크기를 줄여나가는 쿼리를 작성한다.

## poiemaweb 예제

- 이전 Layout 예제에서 반응형을 고려하여 코드를 수정하는 방법에 대해서 학습
- 뷰포트의 크기가 줄어들면 발생하는 문제에 대해 확인하고 이를 수정

### Navigation Bar 반응형 크기 구성

- 뷰포트의 크기가 작아질 수록 헤더 영역의 네비게이션의 탭 목록들이 겹쳐지는 문제가 발생하게 된다.
- 메타 태그를 추가한 후 아래와 같이 미디어 쿼리를 추가

```css
/* Media Query */
/* for Desktop: 801px ~ */

/* for tablet: ~ 800px ~ */
@media screen and (max-width: 800px) {
  
}

/* for smartphone: ~ 480px ~ */
@media screen and (max-width: 480px) {

}
```

- 예제에선 non mobile first 방식으로 작성되어져 있다.
  - 이 방식은 max- 를 기준으로 크기를 지정하기 때문에 적용 우선순위에 따라 화면이 큰 순서부터 먼저 작성되어져야 한다. (화면 크기의 변화에 따라 탐색한다고 생각하면 된다)
- mobile first 방식일 경우에는 작은 화면을 우선으로 적용시킨다.

#### Navigation Bar - 태블릿

```css
/* for tablet: ~ 800px ~ */
@media screen and (max-width: 800px) {
  header {
    height: 120px;
    text-align: center;
  }
  nav {
    float: none;
  }
  #wrap {
    margin-top: 120px;
  }
  aside {
    top: 120px;
  }
}
```

- 태블릿 용으로 작성
- 태블릿에서 헤더는 높이가 높아지고 로고가 위에 배치되고 네비게이션 바는 아래에 배치되는 구조로 작성
  - header의 높이값을 2배로 하고 가운데 배치를 위해 text-align을 center로 지정
  - 상하 배치를 위해 nav의 float을 해제한다. (nav가 블럭 요소이기 때문에 자연스럽게 로고와 상하배치 된다)
- 앞서 header와 aside에는 fixed를 지정해 붕 떠있기 때문에 margin-top과 top을 이용하여 위치를 조정해준다.
  - `#wrap`의 margin-top의 경우 header가 fixed로 따로 배치되기 때문에 margin-top에 영향을 받지 않는다.
  - `aside` 또한 fixed 이기 때문에 일반 문서 흐름 위치에서 붕 떠버리게 된다. (header 60px에 맞춰) 따라서 간격을 더 주기 위해 태블릿용 헤더 높이에 맞춰준다.

#### Navigation Bar - 스마트폰

- poiema 예제에선 목록 아이콘을 이용하여 간단히 열고 닫히는 식으로 구현하며 아이콘 동작시 간단한 애니메이션을 추가하는 방법에 대해 알려준다.
- 목록에 사용되는 아이콘은 이미지가 아니라 앞 서 배운 HTML과 CSS 기능을 이용하여 간단하게 생성. 애니메이션 또한 마찬가지.

**HTML**

```html
<nav>
  <input type="checkbox" class="nav-toggle" id="nav-toggle">
  <label for="nav-toggle" class="navicon"><span class="navicon-bar"></span></label>
  <ul class="nav-items">
    ~
```

- 목록 상단에 input checkbox와 연결된 라벨 요소를 생성한다.
  - label의 특성과 checked 상태를 이용하여 아이콘 작업 진행

**CSS - nav icon**

```css
/* Nav Icon */
.navicon {
  cursor: pointer;
  height: 60px;
  padding: 28px 15px;
  position: absolute;
  top: 0;
  right: 0;

  -webkit-user-select: none;  /* Chrome all / Safari all */
  -moz-user-select: none;     /* Firefox all */
  -ms-user-select: none;      /* IE 10+ */
  user-select: none;          /* Likely future */
}
.navicon-bar {
  background-color: #333;
  display: block;
  width: 20px;
  height: 3px;
  position:relative;
  transition: background-color .2s ease-out;
}
.navicon-bar::before,
.navicon-bar::after {
  background-color: #333;
  content: "";
  display: block;
  height: 100%;
  width: 100%;
  position: absolute;
  transition: all .2s ease-out;
}
.navicon-bar::before {
  top: -7px;
}
.navicon-bar::after {
  top: 7px;
}

.nav-toggle:checked ~ .navicon > .navicon-bar {
  background-color: transparent;
}
.nav-toggle:checked ~ .navicon > .navicon-bar::before {
  transform: rotate(45deg);
  top: 0;
}
.nav-toggle:checked ~ .navicon > .navicon-bar::after {
  transform: rotate(-45deg);
  top: 0;
}

.nav-toggle {
  display: none;
}
.navicon {
  display: none;
}
```

- label 요소가 스마트폰 사용에서 목록 아이콘의 역할을 한다.
  - 클릭 가능 표시를 위해 cursor를 pointer로 지정
  - 클릭 영역 확대를 위해 높이는 헤더에 맞추고 padding을 지정한다.
  - 우측 상단에 고정시키기 위하여 position: absolute 부여
  - 간혹 텍스트가 클릭되는 (예제에서는 로고를 가지는 a요소) 것을 방지하기 위하여 user-select 옵션 설정(none)
- label 요소 내부에 navicon-bar 라는 span 요소를 놓고 이를 아이콘으로 표현한다.
  - 막대기 모양을 표현하기 위해 block으로 변경 후 width와 height, 그리고 배경색을 부여한다.
  - 실제 요소를 기준으로 위아래 막대가 추가될 것이기 때문에 position을 relative로 설정. 애니메이션에서 가운데 막대는 사라지는 형태이기 때문에 transition에서 배경 속성만 따로 설정
  - before와 after 가상 요소를 이용하여 추가 막대를 생성한다. absolute로 위치를 주어 실제 요소 기준으로 위아래로 배치되도록 하며, 애니메이션 동작시 x 자 형태로 변형되기 때문에 속성은 all로 설정
- input 클래스명인 nav-toggle을 이용하여 애니메이션 설정
  - `checked` 가상 클래스를 이용하여 변화를 감지
  - 기준 막대는 투명하게 설정. 앞 서 transition을 부여해 놓았기 때문에 동작시 흐릿하게 사라진다.
  - 상하 막대에는 transform 을 이용하여 각각 45도, -45도로 회전. 이 때 앞 서 위치잡을 때 사용한 top을 0으로 초기화하여 중간 막대를 기준으로 회전되게 한다.
- 체크박스 아이콘 및 목록 아이콘 비활성
  - `display: none`을 이용하여 문서상 요소는 존재하되 렌더링에서 제외시켜 공간을 차지하지 않도록 해준다.
  - css 적용 순서를 고려하여 맨 마지막에 위치시켜야 한다. (미디어 쿼리 작성 이전)

**CSS - smartphone**

```css
/* for smartphone: ~ 480px ~ */
@media screen and (max-width: 480px) {
  header {
    height: 60px;
  }
  .nav-items {
    display: none;
  }
  .navicon {
    display: block;
  }
  #wrap {
    margin-top: 60px;
  }
  aside {
    top: 60px;
  }
  .nav-toggle:checked ~ .nav-items {
    display: block;
    width: 100%;
    background-color: #fff;
    box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
  }
  .nav-items > li {
    display: block;
  }
  .nav-items > li > a {
    line-height: 50px;
  }
}
```

- tablet에서 적용되어져 있는 관련 높이 및 위치 설정을 스마트폰 용에 맞게 수정(여기선 60px)
- 목록 비활성을 위해 nav-items를 display none으로 변경해 놓고, 앞 서 숨겨두었던 목록 아이콘을 block 처리한다.
- checked 발동 시 (label 아이콘 클릭 시) 목록 아이템을 활성화 시킨다. 아이템들은 block을 명시하여 세로 배치가 되도록 한다.

### aside, section, footer 반응형 크기 구성

- footer의 경우 예제에서 1개의 텍스트만 갖고 따로 내부적인 요소 및 컨텐츠가 없어 그대로 구성
- 예제에서 article은 Desktop일 때 2열 가로배치로 변경하고 화면이 작아지면 원래 레이아웃인 1개로 적용시킨다.
- aside의 경우 smartphone 크기일 때 상단에 배치되는 것으로 변경

**Desktop에서 article 2열 배치**

```css
article {
  /* margin: 10px; */
  width: 48.5%;
  margin: 1%;
  padding: 25px;
  background-color: #fff;

  /* 2열 배치 */
  float: left;
}
article:nth-of-type(2n) {
  margin-left: 0;
}
article:nth-of-type(n+3) {
  margin-top: 0;
}
```

- 2열 배치 및 화면의 크기가 커져도 동일한 구획 및 여백을 가져가기 위해 width와 margin을 `%`로 변경한다.
  - width 에서 `%` 사용 시 컨테이너(부모 요소) 너비의 백분율. 여기서는 48.5%로 2개가 놓인다고 가정했을 때 97%가 된다. (article의 사이 및 양쪽 끝 여백 1% 씩을 고려한 것 같다)
  - margin 에서 `%` 사용 시에도 컨테이너 블록 너비의 백분률이 적용된다. (총합 100%)
- `nth-of-type`을 이용하여 중복되는 여백의 크기를 제한한다.
  - 앞 서 `margin: 1%`라는 단축속성을 이용하여 요소 4면의 여백을 동일하게 주었기 때문에, float: left를 해도 전체 크기를 넘어가게 되어 원했던 2열 배치가 되지 않는다. (좌우 예시 - 1%, 48.5%, 1%, 1%, 48.5%, 1% = 101%)
  - 따라서 홀수 번째 article에서는 왼쪽 여백을 0으로, 3번째 article을 포함한 이 후 요소들에게는 위쪽 여백을 0으로 주어 동일한 여백을 갖게 하여 2열 배치가 되도록 한다.

**Tablet 에서 article 1열 배치**

```css
/* for tablet: ~ 800px ~ */
@media screen and (max-width: 800px) {
  ~

  /* article 1열 배치 */
  article {
    width: inherit;
    display: block;
    margin: 10px;
    float: none;
  }
  article:nth-of-type(2n) {
    margin-left: 10px;
  }
  article:nth-of-type(n+2) {
    margin-top: 0;
  }
}
```

- 기존 article 선택자에서 지정한 width 값을 요소가 갖는 특성으로 전체 너비를 가지도록 다시 설정
  - 이 때 inherit를 사용. 부모 컨테이너 기준으로 레이아웃을 다시 계산하여 100%의 백분율 계산으로 다시 지정된다. ([MDN 계산값 문서 참고](https://developer.mozilla.org/ko/docs/Web/CSS/computed_value))
- float 및 margin 도 다시 지정한다. 특히 세로로 1개씩 배치되는 것을 계산하여 n+2로 작성된 것을 볼 수 있다. (2번째 article 부터 관련 margin 적용)

**moblie(480px이하)에서 aside 배치**

```css
/* for smartphone: ~ 480px ~ */
@media screen and (max-width: 480px) {
  ~

  /* aside */
  aside {
    top: 60px;
    position: static;
    width: 100%;
    padding: 5px 0;
  }
  /* aside nav */
  aside > ul {
    width: 100%;
  }
  aside > h1 {
    padding: 5px 0 10px 20px;
    color: #fff;
  }
  section {
    float: none;
    margin-left: 0;
  }

  ~
}
```

- 앞 서 스크롤시 고정이 되도록 aside에 fixed를 부여한 바 있다. 이를 일반 문서 흐름으로 배치하고 전체 너비를 갖게 한 뒤 적절한 padding을 지정한다.
- section 또한 float을 해제하여 일반 흐름을 배치하면 문서 구조 순서상 aside 아래 section이 진행되는 식으로 레이아웃을 변경할 수 있다.

---

**정리**

- 처음 레이아웃을 설정할 때 사용하는 기능 등을 명확히 인식하고 이를 화면 크기에 맞게 적절히 변화하면서 사용하는 법에 대해 배웠다.
- 예제에선 디자인에 대한 값들이 다 정해져 있어 무리없이 따라하고 확인할 수 있었지만 실제로 직접 생각해보면서 작성하면 어렵게 다가올 것 같다. 사이트 클론도 해보고 직접 만들어 보면서 연습을 많이 해야 할 듯. 화면 크기에 따라 레이아웃 기능을 자유자재로 다룰 수 있는 수준을 목표로 해야 겠다.
- 동적인 변화를 위해 주로 JS를 사용하는 것으로 알고 있었는데, HTML 요소와 CSS 기술을 이용하여 간단한 UI 및 애니메이션을 구현할 수 있다는 것이 흥미로웠다. 간단한 CSS 스킬에 대해 좀 더 찾아보고 데이터 변화를 다루지 않는 심플한 UI들도 많이 만져봐야 겠다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-responsive-web-design)
- [MDN - 반응형 디자인](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Responsive_Design)
- [MDN - 미디어 쿼리 초보자 안내서](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Media_queries)