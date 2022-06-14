# Sass - CSS Extensions

- Sass에서 여러 기능을 이용하여 작업할 수 있는 방법에 대하여 학습
- poiemaweb 문서에 나온 기본적인 내용들을 기준으로 학습하며 공식홈페이지 내용을 참고한다.
  - Nesting(중첩)
  - @규칙 - import(가져오기), extend(상속) 등
  - 조건과 반복
  - Mixin
  - Function

---

## Nesting

- 중첩
- 스타일 규칙 선언을 중첩적으로 작성 (CSS에는 없는 기능)
- CSS에서 후손 요소를 특정하기 위해서는 부모 및 상위 요소들까지 선택해야 했지만, Sass 에서는 `&` 및 선택자 규칙 문법을 이용하여 코드블럭 하위에 그대로 작성할 수 있다.

**예제 코드를 통해 이해하기**

```scss
header {
  height: 60px;
  
  .header-box {
    display: flex;
    height: 60px;
    background-color: rgba(0, 150, 0, 0.2);
    
    &.logo {
      width: 60px;
      height: 50px;
    }
    
    &.h1 {
      font-size: 16px;
      color: #000;
        
      &:hover {
        color: #ff0000;
      }
    }
  }
}
```

```css
header {
  height: 60px;
}
header .header-box {
  display: flex;
  height: 60px;
  background-color: rgba(0, 150, 0, 0.2);
}
header .header-box.logo {
  width: 60px;
  height: 50px;
}
header .header-box.h1 {
  font-size: 16px;
  color: #000;
}
header .header-box.h1:hover {
  color: #ff0000;
}
```

- 위 예시와 같이 선택자의 하위 요소들에 연속적으로 스타일 규칙을 작성할 수 있다.
- 가상 클래스나 가상 요소 등을 사용할 때에는 `&`를 활용하면 좀 더 편리하게 작성 가능
- CSS에서 사용하는 복합 선택자 규칙의 모든 구문을 적용하여 사용 가능하다. - `,` `>`, `+`, `~` 등

```scss
.container {
  background: {
    color: tomato;
    repeat: no-repeat;
    size: cover;
    position: center;
  }
}
```

```css
.container {
  background-color: tomato;
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
```

- `-` 으로 구별될 수 있는 개별 속성도 중첩 기능을 이용하여 편리하게 작성할 수 있다.
- 유의할 점은 속성명과 코드블럭 사이에 `:`를 사용해야 된다는 것.

---

## at 규칙

- CSS에서는 `@` 식별자를 이용하여 특정 기능을 사용할 수 있는 at 규칙이라는 것이 있다. 대표적인 예로 CSS의 기본적인 학습에서 많이 볼 수 있는 `@import`가 있다.
- Sass 에서도 `@`을 이용한 다양한 기능을 가지는 at 규칙이 별도로 존재한다.

> 여기선 `@import` 와 `@extend`에 대해 정리하고 `@function`이나 `@mixin` 등 다른 내용들은 관련 학습에서 정리할 예정

### @import

- 가져오기
- 다른 스타일 시트 내용을 가져올 때 사용하는 규칙이다.

#### partials

- Sass 파일에 포함시킬 수 있는 또 다른 Sass 파일이나 그렇게 작업하는 것을 의미한다. (파일 분할)
- 파일 분할을 하는 이유는 프로젝트 규모가 커짐에 따라 기능별로 분류하고 유지보수를 좀 더 효율적으로 하기 위함.
- Sass 에서는 `_`을 이용하여 파일을 생성하면 partial로 분류하며 이 파일들은 import 될 수 있으나 CSS 파일로는 변환되지 않는다.
- 스니펫(코드조각)이나 레이아웃 구조 등을 partial로 작업하고 주 스타일 시트에서 이를 import 하는 방식으로 활용 가능
- top-level(최상단, 최상위)에서 사용하는 것이 일반적. 다만 경우에 따라 스타일 규칙 내에서 포함하여 사용할 수도 있다고 한다.

### @extend

- 확장. 스타일 상속을 위해 사용

**예제 코드를 통해 이해하기**

- poiemaweb 예제 코드

```scss
.error {
  border: 1px #f00;
  background-color: blue;
}

.seriousError {
  @extend .error;

  border-width: 3px;
  border-color: darkblue;
}
```

```css
.error, .seriousError {
  border: 1px #f00;
  background-color: blue;
}

.seriousError {
  border-width: 3px;
  border-color: darkblue;
}
```

- 어떤 규칙 내에 선언된 스타일을 가져와 다른 규칙에서 적용하고 싶을 때 사용
- `@extend`를 이용하여 공통 스타일을 그대로 가져오고 특정 스타일만 따로 선언하는 방식으로 활용 가능
- `@media` 규칙(미디어 쿼리 관련 지시문) 내부에서는 제대로 동작하지 않는다.
- 학습하다 보니 단점에 대한 내용도 확인.
  - 무부별하게 사용할 경우 어떤 스타일 규칙에서 내용을 가져와 최종적인 선택자 규칙이 만들어졌는지 이해하는데 까다로울 수 있다. - 유지보수가 어려워질 수 있다.
  - **extend 사용을 자제하고 Mixin을 활용할 것을 권장.**

---

## 조건과 반복

- 일반적인 프로그래밍 언어에서 사용하는 제어문을 Sass 에서 사용 가능

### if()

```scss
if($condition, $if-true, $if-false)
```

- 내장 함수인 `if()`를 이용하여 조건을 판단.
- 참과 거짓을 판별하여 결과값을 반환.
- 첫번째 인수의 결과값이 참이면 두번째 인수를, 거짓이면 세번째 인수를 반환한다.

### @if, @else if, @else

- 조건문
- 조건 분기를 위해 스타일 시트 내에서 사용하는 조건문
- `@else if` 를 사용하면 다양한 조건을 생성한다.
- 조건식의 결과(불린 데이터)가 참일 경우에만 실행. `@else`는 앞 선 모든 조건이 거짓일 경우에 실행된다.

### @for

- 반복문

**예제 코드를 통해 이해하기**

- poiemaweb 예제 코드

```scss
@for $i from 1 through 3 {
  .item-#{$i} { width: 2em * $i; }
}
```

```css
.item-1 {
  width: 2em;
}

.item-2 {
  width: 4em;
}

.item-3 {
  width: 6em;
}
```

- `$i` 로 반복되는 값을 담는 변수를 설정
- `from`과 `through`로 반복 횟수를 설정 (위 예제의 경우 1, 2, 3으로 3회 반복)
- 반복변수를 이용하여 선택자 규칙 명에는 인터폴레이션으로 번호를 부여, 속성값 width에는 피연산자로 활용

### @while

- 반복문
- 있기는 하나 내부적으로 반복을 종료시킬 방법이 없기 때문에 [사용을 권장하진 않는 것 같다](https://sass-guidelin.es/ko/#section-51). 

### @each

**예제 코드를 통해 이해하기**

- poiemaweb 예제 코드

```scss
// List
@each $animal in puma, sea-slug, egret, salamander {

  .#{$animal}-icon {
    background-image: url('/images/#{$animal}.png');
  }
}

// Map
// $header: h1, $size: 2em
// $header: h2, $size: 1.5em
// $header: h3, $size: 1.2em
@each $header, $size in (h1: 2em, h2: 1.5em, h3: 1.2em) {
  #{$header} {
    font-size: $size;
  }
}
```

- 특수(?) 반복문
- list, map 형태의 데이터의 반복을 위한 기능
- 반복을 위한 변수와 `in`을 사용하며 in 뒤에는 반복할 데이터 타입이 온다.
- 특히 **map 데이터의 경우 반복변수에 key와 value를 담아 구분하여 사용할 수 있다.**

---

## Mixin

- mixin은 섞다라는 의미를 가지고 있는데, Sass 믹스인으로 작성한 스타일 규칙이 다른 곳에서 사용될 수 있다.
- 앞서 배운 `@extend` 기능과 비슷하지만 함수처럼 인자를 전달받아 사용한다는 차이점이 있다.
- `@mixin mixin-name` 형태로 선언하며 믹스인을 불러와 사용하고자 하는 곳에서 `@include mixin-name` 으로 적용한다.


### 믹스인 관련 예제

- poiemaweb 예제 코드 참고

#### 벤더프리픽스

```scss
@mixin vendorPrefix($property, $value) {
  @each $prefix in -webkit-, -moz-, -ms-, -o-, '' {
    #{$prefix}#{$property}: $value;
  }
}

.border_radius {
  @include vendorPrefix(transition, 0.5s);
}
```

- 속성과 속성값을 넘겨받아 믹스인 내부에서 반복문을 실행하여 벤더 프리픽스를 부여하는 예제
- `-webkit-, -moz-, -ms-, -o-, ''` 리스트 데이터의 반복을 처리하기 위해 `@each` 반복 구문이 사용되었다.
- 변수가 가지는 값을 문자열 그대로 사용하기 위해 인터폴레이션(`#{}`)으로 전달

#### opacity

```scss
@mixin opacity($opacity) {
  opacity: $opacity; /* All modern browsers */
  $opacityIE: $opacity * 100;
  filter: alpha(opacity=$opacityIE); /* For IE5~IE9 */
}

.box {
  @include opacity(0.5);
}
```

- IE8 이하 버전에서는 opacity 대신 filter 속성과 alpha() 를 이용하여 투명도를 적용해야 한다. - [참고 자료](https://www.tutorialrepublic.com/css-tutorial/css-opacity.php)
- opacity 는 0.0 ~ 1.0 사이의 값을 사용하지만 alpha filter 에서는 0부터 100 사이의 값을 사용한다. 이에 따라 IE 전용 opacity 변수를 만들어 전달받은 opacity 값에 100을 곱해 준다.
- 해당 믹스인을 포함시키면 모든 브라우저에서 적용되는 opacity 속성과 IE8 버전 이하에서 적용되는 filter 속성이 같이 명시되어 투명도와 관련된 스타일의 호환성을 유지할 수 있게 된다.

#### position

```scss
@mixin position($position, $top: null, $right: null, $bottom: null, $left: null) {
  position: $position;
  top: $top;
  right: $right;
  bottom: $bottom;
  left: $left;
}

.box {
  @include position(absolute, $top: 10px, $left: 50%);
}
```

- position 특성과 위치 지정 속성값들을 전달받아 사용하는 형태
- 위치 지정 속성들은 초기값으로 null을 설정하여 사용하는 곳에서 포함될 때 따로 인자를 전달하지 않으면 트랜스파일링이 되지 않도록 한다.

> 추가적으로 Bourbon, Compass, SusySass와 같은 관련 프레임워크나 라이브러리 등을 활용하여 쉽게 사용할 수 있다고 한다. (관련 툴들을 따로 살펴보진 않았지만, 자주 사용하게 되는 속성들을 믹스인화 하여 해당 이름을 찾아 사용하는 형태일 것 같다)

---

## Function

- `@function` 으로 함수처럼 사용
- 믹스인과 다른 점은 값을 반환한다는 점이다.
  - 믹스인은 스타일 선언 등을 반환
  - `@function`은 `@return`을 이용하여 값을 반환

---

## 주석

- Sass 에서는 CSS 처럼 멀티라인 주석(`/* */`)을 사용할 수 있다.
- 또한 한줄 주석(`//`)이 제공되며, 이 주석의 경우 변환되는 CSS에 적용되지 않는다. (멀티라인 주석은 CSS 파일에 같이 변환되어 나타난다)

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/sass-css-extention)
- [Sass - Style Rules](https://sass-lang.com/documentation/style-rules)