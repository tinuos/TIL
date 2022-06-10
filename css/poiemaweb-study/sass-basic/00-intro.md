# Sass

- CSS 전처리기 중 하나인 Sass에 대한 기본 내용 학습

---

## CSS pre-processor

- CS에서 [전처리기](https://ko.wikipedia.org/wiki/%EC%A0%84%EC%B2%98%EB%A6%AC%EA%B8%B0)란 간단히 정리하면 입력되는 데이터를 처리하여 다른 프로그램에서 사용 가능한 출력물을 만들어주는 프로그램을 의미한다.
- CSS 전처리기는 CSS를 확장하여 작성된 코드를 웹 표준인 CSS로 변환해주는 프로그램이라 할 수 있다.
- 웹 브라우저는 HTML, CSS, JS 만 사용 가능하기 때문에(웹 표준에 따라 동작하도록 시스템이 개발되었기 때문에) CSS 전처리기로 작성한 스타일 코드는 그대로 사용할 수 없고 CSS 표준에 맞춰 코드가 변환되는 작업이 필요하다.

### CSS 전처리기를 사용하는 이유

- 앞 서 CSS 기본 내용을 배울 때 선택자를 이용하여 스타일 규칙을 적용하는 것에 대해 배웠다.
- 문서 구조가 간단할 경우엔 괜찮을지 몰라도, 프로젝트의 규모가 커지고 변경이 많을 수록 요소를 특정하는 방식 및 수정 등의 작업이 어려워질 수 있다.
- CSS 전처리기에는 표준 CSS가 가지지 않는 몇가지 기능을 추가하여 스타일 코드 작성 시 좀 더 효율적으로 처리할 수 있도록 도와준다.
- 대표적인 CSS 전처리기에는 아래와 같은 것이 있는데, 여기선 Sass의 기본 내용만 정리해보려 한다.
  - Sass
  - Less
  - Stylus
  - PostCSS

--- 

## Sass

- syntactically awesome stylesheets의 약자
- 문법적으로 굉장한 스타일시트란 뜻.
- CSS의 확장 개념으로 생각하면 되며, 아래와 같은 도구들을 가지고 있다.
  - 변수 사용
  - 조건문과 반복문
  - import
  - Nesting(중첩)
  - Mixin
  - Extend / inheritance (상속 관련)
- Sass를 이용하면 구조화된 스타일 시트를 작성할 수 있으며 믹스인 등을 이용하여 효율성을 높일 수 있다.

### Sass 설치

- 앞 서 전처러기 내용에서도 다뤘듯이 CSS 변환 작업을 위해 Sass 환경을 설치해야 한다. (트랜스파일링, 컴파일)

#### npm 이용

```
> npm install -g sass
```

- bootstrap 설치 시에도 잠깐 다뤘던 npm 을 통해 Sass를 설치할 수 있다.
- Node 설치 후(npm 포함되어 있음) 위와 같이 설치 명령을 통해 로컬에 전역으로 설치한다.
  - `-g` 옵션은 일반적으로 global(전역)의 단축어로 로컬의 어느 경로에서든 접근 가능하도록 설치한다는 의미(따로 부여하지 않을 경우 설치하는 프로젝트 경로 내에서 사용)

### Sass 명령어

- Sass를 설치했다면 터미널에서 관련 명령어를 사용할 수 있다. ([Dart Sass Command-Line Interface](https://sass-lang.com/documentation/cli/dart-sass))

```
> sass <input.scss> [output.css]
```

- 프로젝트 내에 존재하는 sass 파일을 css로 변환
  - 위 방식은 1:1 방식.

```
> sass input.scss:output.css ...
```

- 여러 파일을 동시에 변환하고자 한다면 위처럼 `:`을 사용하여 나열한다.
- 파일뿐만 아니라 디렉터리 경로명을 입력하면 내부의 모든 Sass 파일이 변환된다. (자세한 내용은 위 문서 참고)

> npm 프로젝트라면 package.json에 위와 같은 변환 명령어를 스트립트로 추가하여 간단히 사용할 수 있다. (npm 명령어로 실행)

#### 스타일 옵션

- 변환 실행시 사용 가능한 스타일 옵션이라는 것이 있다.
- CSS로 변환되는 출력물에 관한 스타일을 제어하는 것으로써 Dart Sass 에서는 아래와 같은 2가지 스타일이 있다고 함.
  - expanded
  - compressed
- expanded는 기본값으로 표준 스타일의 CSS 파일을 생성한다.
- compressed는 아래와 같이 압축하여 CSS 파일을 생성하는 방식. 빈 공간을 다 제거하여 한줄로 압축되며 데이터 크기가 줄어든다.

![image](https://user-images.githubusercontent.com/104971437/173011228-ff357f5e-cf5f-43b0-849f-4c481548aa79.png)

#### Watch 옵션

![image](https://user-images.githubusercontent.com/104971437/173012377-9fae79f2-45cf-4dba-a834-874ac8d68b05.png)

- `--watch` 을 추가하여 변환 명령어를 실행하면 터미널이 종료되지 않고 감지모드로 전환된다.
- 해당 옵션을 사용하면 sass가 input 파일(또는 디렉토리)을 실시간으로 감시하게 되어 수정 후 저장이 일어났을 경우에 output 바로 반영되게 된다. (자동 업데이트 개념)

### Sass 문법

- 2가지로 구분
  - Sass
  - Scss(Sassy CSS)
- Sass가 기본 표기법이었다가 버전업이 되면서 SCSS가 출현

#### SASS 문법

```sass
<!-- Sass 공식홈페이지 예제 코드 -->
@mixin button-base()
  @include typography(button)
  @include ripple-surface
  @include ripple-radius-bounded

  display: inline-flex
  position: relative
  height: $button-height
  border: none
  vertical-align: middle

  &:hover
    cursor: pointer

  &:disabled
    color: $mdc-button-disabled-ink-color
    cursor: default
    pointer-events: none
```

- 확장명 `.sass` 사용
- 중괄호(curly braces)와 세미콜론 대신 **들여쓰기(indent)를 이용하여 스타일 규칙을 정의한다.**

#### SCSS

```scss
// Sass 공식홈페이지 예제 코드
@mixin button-base() {
  @include typography(button);
  @include ripple-surface;
  @include ripple-radius-bounded;

  display: inline-flex;
  position: relative;
  height: $button-height;
  border: none;
  vertical-align: middle;

  &:hover { cursor: pointer; }

  &:disabled {
    color: $mdc-button-disabled-ink-color;
    cursor: default;
    pointer-events: none;
  }
}
```

- 확장명으로 `.scss` 사용
- 표준 CSS 처럼 **중괄호와 세미콜론을 사용하여 스타일 정의**

> poiemaweb을 통해 학습할 예정이므로 일단 Scss 방법으로 정리하고자 한다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/sass-basics)
- [Sass 공식홈페이지](https://sass-lang.com/)
- [MDN - 용어사전) CSS 전처리기](https://developer.mozilla.org/ko/docs/Glossary/CSS_preprocessor)