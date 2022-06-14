# Sass - SassScript

- Sass의 표현 문법에 대해 학습

---

## SassScript

### Statements

- Sass는 일련의 문(statements)들로 구성되며, CSS로 출력되기 위해 평가된다.
- 이러한 문들은 중괄호로 정의된 블럭을 가지며 다른 문들을 포함할 수 있다.
  - SCSS 에서는 문들을 `;`을 이용하여 구분한다.

### Expressions

- 표현식
- Sass에서는 표현식을 사용하여 값을 생성(?)한다.
- 표현식에는 CSS 속성이나 변수 선언등이 올 수 있다.
- 이러한 표현식을 통해 나오는 값들은 mixin이나 함수들에 전달 가능하다.
- Sass 공식 문서에서 Sass 표현식 구문을 `SassScript`라 부른다.

> 처음에 SassScript가 어떤 기능이나 구문의 이름인 줄 알았는데, 그냥 JavaScript 같이 스크립트 언어로써의 이름으로 불리는 것이라 이해하면 된다. 일반적으로 프로그래밍 언어의 범주에서 벗어나는 CSS를 확장하여 사용할 수 있기 때문. 변수나 데이터 타입 등을 정의하여 연산하거나 함수 등의 기능을 사용하여 스타일 코드를 작성할 수 있기 때문에 붙여진 이름 같다.

---

## Data type

- Sass는 속성값으로 활용할 수 있는 value 타입을 제공한다.
- 모든 표현식은 값을 생성하며, Sass 에서 사용할 수 있는 변수는 값을 가질 수 있다.
- 문자열, 숫자 등과 같이 CSS에서 사용되는 타입 및 Sass 만이 가지는 고유한 타입이 같이 존재한다.
- 데이터 타입
  - `Numbers`
  - `Strings`
  - `Colors`
  - `List of values`
  - `boolean`
  - `null`
  - `Maps`
  - `Function references`

> `Function references`에 관한 내용은 생략. 이 후 배울 Sass 믹스인이나 함수 등에서 자세히 정리하려 한다.

### Numbers

- 숫자형 데이터
- CSS에서도 사용되는 1.2, 13, 10px 같은 숫자 단위의 값을 표현한다.

### Strings

- 문자열 데이터
- CSS에서 사용하는 2가지 종류의 문자열을 모두 지원한다.
  - `quoted strings` : "Helvetica Neue" 와 같이 홑따옴표나 쌍따옴표를 이용하여 공백을 포함할 수 있는 방식
  - `unqouted strings` : **bold** 나 벤더 프리픽스 등 쿼터없이 사용하는 문자열을 말한다.

### Colors

- 색상 데이터
- CSS에서 색상값 처리에 사용되는 표현식을 모두 사용할 수 있다.
  - hex code : #ffffff
  - color names : purple, tomato
  - rgb(), rgba(), hsl(), hsla()

### List of values

- 데이터 목록
- 단축 속성 중 공백을 이용하여 여러 값을 설정하거나, 속성값으로 콤마(,)를 이용하여 여러 개를 나열하도록 표현할 수 있다.

### boolean

- 참과 거짓 데이터
- CSS 표준에는 없는 타입. Sass에서는 비교 연산자(>, == 등)나 논리 연산자(and, or 등)를 이용하여 불리언 타입의 값을 생성할 수 있다.
- 또한 `@if` 규칙이나 `if()` 등에서 불리언 값을 이용하여 값 생성을 제어할 수 있다.

### null

- 값의 부재를 표현하는 데이터
- 오직 `null` 만을 값으로 가지는 데이터 타입이다.
- 주로 함수의 결과에서 값이 존재하지 않을 때 생성된다고 한다.
- null 값을 가지는 스타일 규칙(속성이나 변수의 값이 null인 경우)은 CSS로 변환되지 않는다.

### Maps

```
<expression>: <expression>, <expression>: <expression>
```

- 키(key)와 값(value)으로 표현하는 데이터
- 키를 이용하여 일치하는 값을 빠르게 찾을 수 있다. 
- 콜론(:)을 이용하며, 콜론 앞이 키가 되고 뒤에가 값이 된다.

**예제 코드로 이해해보기**

```scss
// sass 공식 홈페이지 예제 코드
$font-weights: ("regular": 400, "medium": 500, "bold": 700);

@debug map.get($font-weights, "medium"); // 500
@debug map.get($font-weights, "extra-bold"); // null
```

- fon-weights 라는 변수에 `("regular": 400, "medium": 500, "bold": 700)`라는 Maps 데이터를 할당
- 빌트인 모듈(내장 모듈)인 map을 이용 - 빌트인 모듈은 Sass가 유용한 함수나 기능들을 종류별로 모듈화하여 제공하는 것을 의미한다. 여기서 사용된 map 빌트인 모듈은 Maps 데이터 타입과 관련된 함수 등을 사용할 수 있다.
  - `map.get($map, $key, $keys...)` 함수를 이용하여 특정 Map 데이터에 존재하는 키와 일치하는 값을 반환시킨다.
  - 만약 일치하는 키가 존재하면 해당 값을 반환하며, 없을 경우 `null`을 반환한다.

---

## 변수

```
<variable>: <expression>
```

```scss
// Sass 공식 홈페이지 예제 코드
$base-color: #c6538c;
$border-dark: rgba($base-color, 0.88);

.alert {
  border: 1px solid $border-dark;
}
```

- 값을 할당하여 사용할 수 있는 변수 기능을 제공한다.
  - 값 대신 변수 이름을 참조한다.
- `$`를 변수 이름 앞에 붙여 사용한다.
  - 변수 선언 및 할당, 참조 시에 모두 붙여야 한다.
  - `$변수명`을 한 세트로 사용
- 스타일 규칙이나 at 규칙에서만 선언되어야 하는 속성(property)과는 달리, 변수는 **어디에서든 선언될 수 있다.**


### 변수의 범위

- Sass 에서 사용되는 변수는 일반적으로 사용하는 곳에 따라 전역변수나 지역변수가 될 수 있다.

```scss
$height: 100px; // 전역 변수

p {
  width: 500px;
  height: $height; // 100px

  $color: tomato; // 지역 변수

  span {
    display: block;
    height: $height; // 100px
  }
}

div {
  color: $color; // Error: Undefined variable.
}
```

- 전역 변수
  - 스타일 규칙이나 at 규칙이 아닌 스타일 시트에서 작성되는 변수가 가지는 범위
  - 하위에 있는 모든 범위에서 해당 변수에 접근할 수 있다.
- 지역 변수
  - 코드 블록 내에서 선언된 변수
  - 코드 블록 내부와 코드 블록 아래 하위에서만 접근 가능하며 상위에선(외부) 접근이 불가능하다.
  - 지역 변수에 `!global`을 붙이면 전역 변수로 사용할 수 있다.

---

## 연산자

- 앞 서 배운 데이터 타입의 값들에 사용할 수 있는 다양한 연산자 구문에 대해 학습

### 숫자 관련 연산자

```scss
$width: 1000px;

.container {
    width: $width + 100px;
}

.box {
    width: $width + 1.2em; // Error: 1000px and 1.2em hqve imcopatible units.
}
```

- 사칙연산 및 나머지 연산
  - `+`, `-`, `*`, `/`, `%` : 덧셈, 뺄셈, 곱셈, 나눗셈, 나머지 연산
- 동등 및 부등
  - `==`
  - `!=`
- 상대적인 값을 가지는 단위의 경우 같은 단위의 갖는 값과의 연산만 수행할 수 있다.
  - `%, em, rem, vh, vw, vmin, vmax` 등 브라우저가 상대적으로 계산하는 단위
  - [calc()](https://developer.mozilla.org/ko/docs/Web/CSS/calc) 사용 시에는 혼합하여 결과값을 도출할 수 있다.
- 나눗셈 연산자 관련
  - CSS에서 `/`는 속성값을 구분하는 용도로 쓰이기 때문에 Sass 에서 `/`으로 나눗셈 연산을 하기 위해서는 몇가지 조건이 필요하다. (CSS 에서 주로 단축 속성의 속성값들을 표기할 때 같은 단위값을 구분하기 위한 용도로 `/`를 사용)
  - 변수에 대해 사용
  - 괄호 내에서 사용(나눗셈 연산을 `()`로 묶는다)
  - 다른 연산의 일부로서 사용(위의 사칙 연산자나 다른 연산자와 같이 사용)

### 컬러 연산자

**예제 코드를 통해 이해하기**

```scss
// poiemaweb 예제코드
p {
  color: #010203 + #040506;
  // R: 01 + 04 = 05
  // G: 02 + 05 = 07
  // B: 03 + 06 = 09
  // => #050709
}

p {
  color: #010203 * 2;
  // R: 01 * 2 = 02
  // G: 02 * 2 = 04
  // B: 03 * 2 = 06
  // => #020406
}

p {
  color: rgba(255, 0, 0, 0.75) + rgba(0, 255, 0, 0.75);
  // alpha(투명도)는 연산되지 않는다
  // color: rgba(255, 255, 0, 0.75);
}
```

- hex 코드나 rgb() 등으로 작성된 색상값은 연산이 가능
- rgba() 의 경우 투명도를 조절하는 알파 채널값은 연산되지 않는다.
- 투명도는 아래와 같이 관련 함수를 통해 연산 가능하다.

```scss
// poiemaweb 예제코드
$translucent-red: rgba(255, 0, 0, 0.5);

p {
  color: opacify($translucent-red, 0.3);
  // => color: rgba(255, 0, 0, 0.8);

  background-color: transparentize($translucent-red, 0.25);
  // => background-color: rgba(255, 0, 0, 0.25);
}
```

- `opacify($color, $amount)` : 전달되는 2번째 인수의 투명도를 첫번째 인수 색상의 투명도에 더해 불투명도를 증가
- `transparentize($color, $amount)` : 전달되는 2번째 인수의 투명도를 첫번째 인수 색상의 투명도에 빼서 불투명도를 감소

### 문자열 연산자

- `+` 연산으로 문자열을 연결시킬 수 있다.
- 따옴표가 있는 문자열과 없는 문자열을 연결할 때는 좌항을 기준으로 따옴표가 처리된다.

### 불린 연산자

- 불린 값을 위한 논리 연산자 종류
  - `&&` : and 연산
  - `||` : or 연산
  - `!` : not 연산
- 주로 `if` 함수 및 `@if` 규칙에 같이 사용된다.

---

## Interpolation : #{}

```scss
// poiemaweb 예제 코드
$name: foo;
$attr: border;

p.#{$name} {            // p.foo
  #{$attr}-color: blue; // border-color: blue;
}

.someclass {
  $font-size: 12px;
  $line-height: 30px;
  // 연산의 대상으로 취급되지 않도록
  font: #{$font-size} / #{$line-height}; // 12px / 30px
}
```

- 인터폴레이션. 보간법, 내사법.
- 변수가 가지고 있는 값을 문자열 그대로 삽입할 수 있는 구문.
- 위 예제 코드처럼 변수가 가지고 있는 값을 문자열 그대로 사용. 선택자의 이름으로 사용할 수 있다.
- 맨 마지막 라인은 나누기 연산의 특성과 관련된 내용. 만약 그대로 `$font-size`와 `$line-height` 변수를 써버리면 해당 자리에 숫자값이 그대로 표현되어 나누기 연산의 대상이 되어 버린다. 인터폴레이션을 이용하면 변수가 가지는 값을 문자열 그대로 넘겨주기 때문에 나누기 연산의 대상이 되지 않고, font 단축속성에서 font-size와 line-height를 구분하는 것으로 처리할 수 있다.

---

## Ampersand(&)

- 부모 요소를 참조할 수 있는 Sass 선택자(?)
- 기존 CSS에서 복잡한 구조의 요소들을 구체적으로 선택하기 위해서는 여러번의 작성이 필요했다. 
- Sass의 `&`를 활용하면 코드블럭 내부에서 상위 셀렉터를 바로 선택할 수 있기 때문에 이러한 복잡함을 줄일 수 있으며, 가독성도 훨씬 좋아진다.

---

## !default

```scss
$content: "First content";
$content: "Second content?" !default;
$new_content: "First time reference" !default;

#main {
  content: $content; // "First content"
  new-content: $new_content; // "First time reference"
}
```

- 할당되지 않은 변수의 초기값을 설정
- 이미 할당이 되어 있는 변수에는 적용되지 않는다. (null 타입일 경우 `!default`를 이용하여 할당 가능)

**예제 코드를 통해 이해하기**

- poiemaweb 예제코드
- _font.scss 를 main.scss에서 import 하여 적용

```scss
// _font.scss
$font-size: 16px !default;
$line-height: 1.5 !default;
$font-family: "Helvetica Neue", "Helvetica", "Arial", sans-serif !default;

body {
  font: #{$font-size}/$line-height $font-family;
}
```

```scss
// main.scss
$font-family: "Lucida Grande", "Lucida Sans Unicode", sans-serif;

@import "font";
```

- **_font.scss** 에서는 폰트와 관련된 기본 속성들의 값을 `!default`을 이용하여 부여
- **main.scss** 에서 import 하여 폰트를 적용. 따로 폰트와 관련된 속성값을 지정하지 않아도 !default로 작성된 값이 적용된다. 여기서 `$font-family`의 값들만 다시 선언하여 할당하고 있기 때문에 이 속성값을 제외하고는 **_font.scss**에서 작성된 기본값이 적용되며 아래와 같은 결과가 나오게 된다.

```css
body {
  font: 16px/1.5 "Lucida Grande", "Lucida Sans Unicode", sans-serif;
}
```

---

## 정리

- CSS를 좀 더 확장하여 편리하게 작성할 수 있는 여러 기능들에 대해 학습
- 특히 `&`나 연산 등을 이용하여 좀 더 쉽게 스타일 시트를 작성할 수 있다는 것을 알게 되었다.
- 마지막 `!default` 적용 내용과 관련하여 당연한 이야기지만 스타일 적용 순서가 가장 중요하다고 느꼈다. 초기화 및 공통 변수 및 값들은 미리 선언되어 있어야 하고 이들을 분류하여 import 하는 순서가 매우 중요. 이렇게 부분적으로 분류하는 것을 partial 이라 부르는 것 같다. 
  - [Sass-guideline](https://sass-guidelin.es/ko/)도 참고하기(설계와 관련하여 디렉토리와 파일을 구분하여 적용하는 7-1 패턴이란 게 있다는 것을 확인 - 세부적인 컴포넌트 구조 관련인 듯)

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/sass-script)
- [Sass - Structure of a Stylesheet](https://sass-lang.com/documentation/syntax/structure)
- [Sass - Values](https://sass-lang.com/documentation/values)