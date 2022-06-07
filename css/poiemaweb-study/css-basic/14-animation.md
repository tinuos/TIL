# CSS - 애니메이션

- CSS로 애니메이션 처리에 대한 내용을 학습
  - transtion 과의 차이점
  - animation 관련 속성 및 @keyframe 처리

---

## CSS 애니메이션

- 앞서 배운 `transition`은 요소의 어떠한 상태 변화에 따라 스타일의 동적인 처리를 가능하게 했다.
- 이러한 `transition`은 요소의 상태 변화라는 트리거가 있어야 가능하며 기본적으로 자동으로 발동되지 않는다.
- `animation`도 transition처럼 스타일 변화를 위해 사용한다는 것은 비슷하나, 하나의 줄거리를 만들어 내부의 세세한 움직임과 재생, 반복, 정지 등도 제어 가능하다.

> 이러한 애니메이션 효과는 CSS가 아닌 JS로도 가능하다고 하는데, 렌더링 성능 등을 고려하여 적절히 선택해야 효율적이라고 한다. (아래 참고 문서 내 관련 내용 참고) jQuery 라는 JS 라이브러리에서도 애니메이션 기능이 제공된다고 함.

### animation

- `animation` 은 애니메이션 효과를 주기 위해 사용하는 속성으로 애니메이션 관련 속성의 단축 속성
- 아래와 같은 하위 속성값을 포함할 수 있다.
  - `animation-name` : `@keyframes` 애니메이션의 이름을 지정
  - `animation-duration` : 한 주기 단위 애니메이션 소요 시간 설정(기본값 : 0s)
  - `animation-timing-functiion` : 타이밍 함수 지정(기본값 : ease)
  - `animation-delay` : 대기시간 설정 - 요소 로드와 애니메이션 실제 실행 시간 사이(기본값 : 0s)
  - `animation-iteration-count` : 재생 횟수 설정(기본값 : 1)
  - `animation-direction` : 애니메이션 종료 이 후 반복 시 진행 방향 지정(기본값 : normal)
  - `animation-fill-mode` : 애니메이션 미실행 시 (종료 또는 대기) 요소의 스타일 지정
  - `animation-play-state` : 애니메이션 재생 상태(재생 또는 중지) 지정

### `@keyframes`

- 애니메이션을 여러 특정 시점으로 나누어 속성 변화를 제어하기 위해 사용
  - 0% ~ 100% 까지 %로 시점을 구분하거나, `from`, `to` 키워드를 사용
  - % 로 구분할 시 시점을 더 세분화 가능

### `animation-name`

- 하나 이상의 애니메이션 이름을 지정한다.
- 애니메이션 이름은 `@keyframes` 규칙의 식별자 이름에 대응된다.
- `,` 로 구분하여 여러 가지 키프레임 이름을 동시에 적용할 수 있다.

### `animation-duration`

- 애니메이션 소요 시간 지정
- 시간은 초(s)나 밀리 초(ms) 단위로 지정
- 애니메이션 효과 사용 시 **필수 지정값**
  - 기본값은 `0s`으로 따로 시간을 지정하지 않을 경우 실행되지 않는다.

### `animation-timing-function`

- 타이밍 함수
- 동적 표현과 관련된 수치 함수를 지정
- transition 내용 참고

### `animation-delay`

- 대기 시간 설정
- 초(s) 또는 밀리 초(ms) 단위로 설정한다.

### `animation-iteration-count`

- 애니메이션 반복 횟수 지정
- 기본값이 `1` 이기 때문에 따로 미지정 시 애니메이션은 한번만 발동된다.
  - 정수 형태로 횟수 표기
  - `infinite` 키워드로 무한 반복 설정이 가능하다.

### `animation-direction`

- 종료 이후 **반복 시** 애니메이션 진행 방향 설정
- 기본값은 normal로 시점(from, to / 0% ~ 100%)에 명시된 방향대로 진행된다.
  - `reverse` : 기본 방향과는 역방향으로 진행
  - `alternate` : 반복시 홀수번째 반복은 normal, 짝수번째에는 reverse 진행
  - `alternate-reverse` : 반복시 홀수번째 반복은 reverse, 짝수번째에는 normal 진행

### `animation-fill-mode`

- 애니메이션 미 실행시(대기나 종료) 요소의 스타일을 지정한다.
- 키워드값 사용
  - none
  - forwards
  - backwards
  - both
- 자세한 설명은 poiemaweb 예제 참고

> 대기, 종료 시 시작 프레임에 설정 스타일을 적용하냐 적용하지 않냐로 구분. 적용하지 않는 경우에는 요소에 미리 선언되어져 있던 스타일이 적용되어져 대기하는 식으로 처리된다.

### `animation-play-state`

- 재생 상태(재생 또는 중지)를 지정
- 기본값은 `running` 으로 현재 재생을 설정
  - `paused` : 애니메이션을 현재 중지한다.

> js로 이벤트를 설정하여 특정 이벤트에 재생, 중지 등을 제어할 수 있다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-animation)
- [MDN - CSS 애니메이션 사용하기](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Animations/Using_CSS_animations)
- [MDN - animation](https://developer.mozilla.org/ko/docs/Web/CSS/animation)