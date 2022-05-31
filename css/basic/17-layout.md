# CSS - 레이아웃

- 요소의 적절한 배치를 위한 레이아웃 방법에 대해 학습

---

## 레이아웃 설계

- 레이아웃은 요소들을 의도된 디자인에 맞춰 공간을 배정하고 정렬하는 것
- HTML에서는 semantic tag라 하여 사용 의미에 맞게 구조적으로 활용하는 요소들에 대하여 학습했다.(header, main, nav 등) 이러한 요소들은 단순히 문서 구조상의 의미만 갖을 뿐 시각적인 배치는 CSS 다양한 기술을 통해 이루어진다.
- CSS에서는 레이아웃을 위한 다양한 기술이 존재한다.
  - normal flow (일반 문서 구조 흐름)
  - 요소의 display 특성 (inline, block, inline-block)
  - floats
  - flex box
  - grid
  - positioning
  - column layout (다단)
  - table (old layout, old method)
- CSS3 표준이 자리잡기 전에는 table 태그의 마크업을 통해 레이아웃을 했다고 한다. 이러한 방식은 구조적으로 유연하지 않고, 웹 접근성에 있어서도 문제가 발생하는 옛날 방식. 현대적인 웹 페이지 레이아웃에선 사용하지 않아야 하는 방식이다.

> 이 문서에선 기본적인 웹페이지 구조를 poiemaweb 예제를 통해 따라해보며 정리. float을 이용하여 레이아웃을 정렬하는 방식에 대해 좀 더 자세히 알아본다.

---

## poiemaweb 예제 

### 레이아웃 구조

![image](https://user-images.githubusercontent.com/104971437/170949101-86d79b66-a7a4-4751-8faa-14768bcbf904.png)

- 전체적으로 `div`를 통해 감싸며 중앙 메인 콘텐츠 부분에서도 `div`로 감싼 구조(각각 `wrap`, `content-wrap`로 id 속성 부여)
- 크게 header, main(콘텐츠 영역), footer로 나뉘며 navigation은 header에, aside는 메인 div에 포함
- 이 실습 페이지에서는 각각의 래퍼 요소에 float을 주어 가로 배치로 레이아웃을 설정해보는 것을 학습한다.

> 예제에서는 따로 스타일 시트를 구분하지 않고 HTML의 style 요소를 이용하여 내부 스타일을 적용했는데 복습 차원에서 외부 스타일 시트로 분리하여 작업하기로 결정.

#### reset css

```css
/* RESET CSS */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #58666e;
  background-color: #f0f3f4;
}
li {
  list-style: none;
}
a {
  text-decoration: none;
}
```

- 전체 선택자를 이용하여 사용자 에이전트 스타일의 `margin`과 `paading`을 **0**으로 초기화하고 외곽선까지 너비를 적용하는 `border-box`를 적용
- body 에는 폰트 및 폰트 색상과 배경색을 추가한다.
  - 현재 내 로컬(윈도우)을 확인해보니 헬베티카 관련 폰트는 설치되어 있지 않고 Arial 만 있는 상태
  - 따라서, 내 로컬에 있는 브라우저로 이 페이지를 본다면 폰트는 Arial이 적용된다.
- li와 a 요소에 적용되는 기본 스타일을 적용하지 않는다.
- 그냥 추가로 정리
  - 헬베티카는 디자인 영역에서 꽤 유명한 유료 폰트인 듯 하다.
  - 크롬이나 웨일에서 font finder라는 확장 프로그램을 이용하여 요소에 어떤 폰트가 설정되어 있는지 확인할 수 있다. 글꼴 관련 스타일 속성들만 추려내기 때문에 꽤 유용한 것 같다.
  ![image](https://user-images.githubusercontent.com/104971437/170961648-4e25ca68-2ca9-4aa4-8d5e-ea0b5641127e.png)

#### header

**HTML**

```html
~
<header>
  <a href="#home" class="logo">
    <img src="https://poiemaweb.com/img/logo.png">
  </a>
  <nav>
    <ul class="nav-items">
      <li><a href="#home">Home</a></li>
      <li><a href="#news">News</a></li>
      <li><a href="#contact">Contact</a></li>
      <li><a href="#about">About</a></li>
    </ul>
  </nav>
</header>
~
```

**CSS**

```css
/* HEADER */
header {
  width: 100%;
  height: 60px;
  z-index: 2000;
  background-color: #fff;
  box-shadow: 0 2px 2px rgba(0, 0, 0, 0.05), 0 1px 0 rgba(0, 0, 0, 0.05);
}
.logo {
  display: inline-block;
  height: 36px;
  margin: 12px 0 12px 25px;
}
.logo > img {
  height: 36px;
}
nav {
  float: right;
}
.nav-items > li {
  display: inline-block;
}
.nav-items > li > a {
  line-height: 60px;
  padding: 0 30px;
  color: rgba(0, 0, 0, 0.4);
}
```

- header 구조
  - 로고 이미지와 네비게이션
  - 높이는 60px, 배경 및 그림자 추가
  - z-index 를 높게 주어 해당 요소가 항상 다른 요소보다 위에 있도록 설정. 아직 position을 주지 않았지만 추후에 스크롤 시 헤더가 고정되게 하기 위해 추가된 속성 같다.
  - 네이게이션 요소에 `float: right`를 주어 우측에 배치되도록 설정
- logo 설정
  - 로고 이미지를 a 태그로 감싸 클릭시 Home 으로 갈 수 있도록 하이퍼링크 지정
  - a 요소는 인라인 특성을 갖기 때문에 margin을 주기 위해 디스플레이를 `inline-block`으로 설정. 여기선 헤더 높이값에 맞추기 위해 상하 마진에 12px 씩 지정하고 높이를 36px로 설정한 것을 확인할 수 있다.
- nav 영역
  - 우측 배치를 위해 nav 요소를 `float: right`로 지정한다.
  - 한 라인에 가로로 배치되기 위하여 li 요소를 선택하여 `inline-block`으로 설정한다. 
  - a 요소 안 텍스트를 수직 정렬하기 위하여 `line-height`를 이용. a가 기본적으로 인라인 특성이기에 가능한 방식. font-size를 기준으로 계산되어 줄높이가 설정되는 line-height를 header 높이와 동일하게 지정하여 텍스트가 가운데에 위치되는 것처럼 정렬할 수 있다. 또한 양 옆에 여백을 주기 위해 padding 좌우 값을 설정. 텍스트의 주변에 마우스가 올려져도 a요소의 줄높이와 크기만큼 li를 차지하기 때문에 하이퍼링크 동작이 가능하게 되며, li 사이에는 inline-block 시 생기는 여백으로 인해 잠깐 원래대로 돌아오는 것도 확인할 수 있다.
  - a요소 hover 시 텍스트 색상 변경도 추가하여 사용자가 탭 메뉴 선택을 구별 가능하게 해준다.

#### content wrap 영역(aside, section)

**HTML**

```html
<!-- Content wrap -->
<div id="content-wrap">
  <aside>
    <h1>Aside</h1>
    <ul>
      <li><a href="#" class="active">London</a></li>
      <li><a href="#">Paris</a></li>
      <li><a href="#">Tokyo</a></li>
      <li><a href="#">Newyork</a></li>
    </ul>
  </aside>
  <section>
    <article id="london">
      <h1>London</h1>
      <p>Lorem ~</p>
    </article>
    <article id="paris">
      <h1>Paris</h1>
      <p>Lorem ~</p>
    </article>
    <article id="tokyo">
      <h1>Tokyo</h1>
      <p>Lorem ~</p>
    </article>
    <article id="newyork">
      <h1>Newyork</h1>
      <p>Lorem ~</p>
    </article>
  </section>
</div>
```

- aside 영역과 section 영역을 감싸는 `content-wrap` 요소로 전체 영역을 지정
- aside 는 왼쪽, section 은 오른쪽 영역을 차지

```css
/* Aside */
aside {
  position: fixed;
  top: 60px;
  bottom: 0;
  width: 200px;
  padding-top: 25px;
  background-color: #333;
}
/* Aside navi */
aside > ul {
  width: 200px;
}
aside > ul > li > a {
  display: block;
  color: #fff;
  padding: 10px 0 10px 20px;
}
aside > ul > li > a.active {
  background-color: #4CAF50;
}
aside > ul > li > a:hover:not(.active) {
  background-color: #555;
}
aside > h1 {
  padding: 20px 0 20px 20px;
  color: #fff;
}
```

- 처음 레이아웃을 잡을 때 aside 는 `float: left`로, section 은 `float: right` 로 설정한 후 width를 퍼센트 값으로 주어 구분. 이후에 스크롤 시 aside를 고정하기 위하여 position 값을 준다고 설명.
  - bottom을 `0`으로 주지 않으면 콘텐츠 내용의 높이만큼의 영역을 갖게 된다.
  - header를 `position: fixed`로 지정하여 스크롤 시 고정되도록 변경하였기 때문에 aside의 top도 60px을 부여. 스크롤 시 aside도 고정되어 내부 네비게이션을 사용자가 계속 확인할 수 있게 된다.
  - 이 외 스타일 규칙들은 hover 나 컬러값 같은 세부 스타일
- section 은 float의 right를 그대로 유지하되 레이아웃을 잡기 위해 설정한 width 를 삭제하고 margin-left 를 aside 만큼 주어 나머지 공간을 모두 차지하도록 설정
  - float 에서 배운 clearfix 를 이용하여 전체 content-wrap에 추가하여 전체 높이를 인식할 수 있도록 처리한다.
- h1 관련 내용
  - h1 ~ h6 은 문서의 논리적인 구조나 웹 접근성에 따라 작성해야 된다고 알고 있는데, 여기선 aside나 article 모두 h1이 쓰였다. 이 부분에 대해선 레이아웃을 다루다 보니 poiemaweb 에서 따로 설명되어 있지 않은데 나중에 따로 찾아보아야 할 듯.(article 로 구분되면 h1을 여러개 써도 되는지??)
  - 한편 font-size와 관련하여 처음에 어떠한 설정(reset CSS 등)도 하지 않았기 때문에 아래 이미지와 같이 h1 이 각각의 요소에 따라 다른 크기로 사용자 에이전트 스타일에 맞게 형성되는 것을 볼 수 있다.
  ![image](https://user-images.githubusercontent.com/104971437/171141220-b7ee0d40-c1f4-4c9b-83d5-a48feb51ee69.png)
  같은 글씨 크기를 적용하기 위해 reset CSS로 따로 설정해준다.
  ```css
    h1 {
      font-size: 1.8em;
    }
  ```

#### footer

**HTML**

```html
<!-- content-wrap 영역 다음에 위치 -->
<footer>@ Copyright 2016 ungmo2</footer>
```

**CSS**

```css
footer {
  position: absolute;
  height: 60px;
  width: 100%;
  padding: 0 25px;
  line-height: 60px;
  color: #8a8c8f;
  border-top: 1px solid #dee5e7;
  background-color: #f2f2f2;
}
```

- 일반적인 웹 디자인에서 footer 는 페이지의 하단에 위치하며 이 예제에서도 같은 레이아웃을 가진다.
- 다만 여기서는 aside와 section 영역이 각각 position, float으로 부유 특성을 가지기 때문에 footer 요소를 따로 레이아웃 설정하지 않으면 일반 문서 흐름에 따라 배치되어 보이지 않는 상태가 된다.
- 따라서 absolute로 position 을 부여하여 위에 부유할 수 있도록 배치해준다. 앞 서 content-wrap에 clearfix 설정을 했기 때문에 래퍼가 끝나는 지점에서 footer가 의도된 레이아웃에 따라 자연스럽게 배치되는 방식. (콘텐츠의 내용(article)이 적을 수록 footer가 딸려 올라간다는 문제 확인)

---

**정리**

- 간단히 시맨틱 태그들만 이용하는 예제인데도 따라해보는데 무척 애를 먹었다. 실제 문서가 복잡해질 수록 레이아웃에 대해 좀 더 상세히 분류해야 겠다고 생각.
- 간단한 텍스트일 경우 line-height 를 이용하여 수직 정렬을 할 수 있다는 것에 대하여 배웠고, float을 통해 영역을 간단하게 나누는 방법에 대해서도 알게 되었다. 중요한 것은 어떻게 구역을 나누고 어떠한 레이아웃 기술을 적용할 지에 대해 명확히 해야 한다는 것. 또한 문서에서 요소의 흐름(일반 문서 흐름과 요소가 부유되는 특성 등)을 이해하는 것도 중요하다.


---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-layout)
- [MDN - CSS 레이아웃](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout)