# Sass - Built in modules

- Sass에 내장되어 있는 다양한 모듈을 통해 활용할 수 있는 함수에 대해 학습
- poiemaweb 내용을  기준으로 자주 사용하는 것들로만 학습하되 Sass 공식 홈페이지 문서를 참고

> poiemaweb 에서 참고해 놓은 Sass Built-in function 문서 링크는 현재 존재하지 않고 버전 업 되면서 built-in modules 로 변경된 것 같다.

---

## 빌트인 모듈

- 여러가지 유용한 함수를 모듈별로 구분하여 제공
  - Sass: math module
  - Sass: string module
  - Sass: color module
  - Sass: list module
  - Sass: map module
  - Sass: selector module
  - Sass: meta module
- 주로 Sass 에서 사용되는 데이터 타입과 관련된 기능들로 분류되어 제공되며 선택자 처리와 관련된 모듈도 확인할 수 있다.

### 숫자 관련 함수

#### percentage($number)

```scss
.container {
  width: percentage(0.5);
}
```

```css
.container {
  width: 50%;
}
```

- 인자로 들어오는 number 값을 퍼센트 단위로 변화시킨다.

#### round($number)

```scss
.box {
  width: round(100.5px);
  height: round(100.4px);
}
```

```css
.box {
  width: 101px;
  height: 100px;
}
```

- 가장 가까운 숫자로 반올림한다.

#### ceil($number)

- 올림 처리

#### floor($number)

- 내림 처리

#### abs($number)

```scss
.box {
  width: abs(500px);
  height: abs(-500px);
}
```

```css
.box {
  width: 500px;
  height: 500px;
}
```

- 절대값 처리

### Introspection 관련 함수

- 자기 성찰이란 의미를 가지고 있는데 CS에선 주로 값에 대한 데이터 타입 등을 확인하는 의미로 사용
- 예전 버전에선 공식 홈페이지에서 관련 문서를 따로 분류해 놓은 것 같은데 현재는 **meta** 모듈 관련 문서에서 내용을 찾을 수 있다.

#### type-of($value)

- 인자로 전달받은 값의 타입을 반환해준다. 반환되는 타입은 아래 중 하나
  - number
  - string
  - color
  - list
  - map
  - calculation
  - bool
  - null
  - function
  - arglist

#### unit($number)

- 숫자값에 적용되어 있는 단위를 문자열 형태(`"~"`)로 반환한다.
- 디버깅을 위해 고안된 기능이라 한다. math 모듈 문서에서 확인 가능

#### unitless($number)

- 숫자값에 단위가 있는지 없는지를 불린값 형태로 반환한다.
- 단위가 없으면 true, 있으면 false 가 반환된다.

#### comparable(\$number1, \$number2)

- 인자로 받는 2개의 숫자값이 서로 덧셈, 뺄셈, 비교 연산이 가능한 지를 판단하여 불린값을 반환한다.
- true 일 경우 연산이 가능하며, false 일 경우 불가능

### 문자열 관련 함수

#### quote($string)

- 전달받는 문자열을 따옴표 문자열(quoted string)로 만든다.

#### unquote($string)

- 전달받는 문자열을 따옴표 제거 문자열(unquoted string)로 만든다.

### List 관련 함수

#### length($list)

- 리스트 데이터가 가지는 요소의 개수를 반환
- map 데이터에도 사용 가능

#### nth(\$list, \$n)

- 리스트의 n번째 요소를 반환한다.

#### append(\$list, \$value, \$separator: auto)

- 리스트의 맨 마지막에 요소를 추가한다.
- 3번째 인자는 구분자로 공백(space)이나 콤마(comma), 슬래쉬(slash)를 전달하여 요소 간 구분할 수 있다. 기본값은 auto로 list 타입으로 구분(공백)된다.

#### zip(\$list, \$list, \$list ...)

- 복수의 리스트를 전달하여 순서에 맞게 요소들을 결합한다.

### map 관련 함수

#### map-get(\$map, \$key, \$keys ...)

- map 데이터와 함께 key를 전달하여 key가 가지고 있는 value를 반환한다.
- 전달하는 key가 map 데이터에 없다면 null 이 반환된다.
- 보통 map과 key 2개의 인자를 전달하여 사용하는데 2번째 인자로 전달되는 key가 가지는 데이터 타입이 map일 경우 그 안에서 찾을 key를 또 전달할 수 있다. 즉 최종적으로 전달되는 마지막 key 인자와 일치하는 값이 반환된다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/sass-built-in-function)
- [Sass - Built-In Modules](https://sass-lang.com/documentation/modules)