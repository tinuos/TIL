# CSS - 배경(background)

- 요소에 배경을 설정하는 법을 학습

---

## background 속성

- background 속성을 이용하여 요소에 배경 관련 스타일을 지정할 수 있다.
- `-부가속성`으로 배경에 대한 여러 가지 특성을 개별적으로 지정 가능하다. ([배경 및 테두리 관련 속성](https://developer.mozilla.org/ko/docs/web/css/css_backgrounds_and_borders))

> 여기선 poiemaweb에서 정리된 속성들만 정리하고, 다른 속성들은 추후 사용 시 간단히 정리하는 방향으로 학습

### background-image

- 요소에 배경 이미지를 지정할 때 사용하는 속성
- 일반적으로 `url(이미지경로)`을 이용하여 이미지를 지정하며 `,`를 통해 하나의 요소 안에 여러 개의 이미지 지정이 가능하다.
  - `,` 를 통해 여러개의 이미지를 지정하면, 제일 먼저 지정된 이미지가 제일 위에 위치
  - 이미지 시작의 기본값은 좌상단이므로 여러개의 이미지 위치를 조정하기 위해서는 `background-position` 을 활용. (미설정 시 겹쳐져서 보이게 된다)
- 접근성 관련
  - 브라우저는 배경 속성을 사용한 이미지에 대하여 부가적인 접근성 기술이 제공하지 않는다.
  - 문서에서 이미지가 정보로서 제공되어야 한다면 img 태그 등을 이용하여 구조적으로 작성하는 것이 바람직하다. - [MDN 접근성 관련](https://developer.mozilla.org/ko/docs/Web/CSS/background-image#%EC%A0%91%EA%B7%BC%EC%84%B1_%EA%B3%A0%EB%A0%A4%EC%82%AC%ED%95%AD)

### background-repeat

- 요소에 적용된 배경 이미지의 반복 처리 관련 속성
- 가로나 세로로 반복을 설정할 수 있으며, 다음과 같은 값을 가진다.
  - `repeat` - 요소의 배경 영역을 채울 때까지 이미지 반복 (기본값)
  - `no-repeat` - 이미지를 반복하지 않는다. 배경 영역에 이미지가 다 차지 않을 수 있다.(background-position 속성을 통해 위치 지정 가능)
  - 이외에 `repeat-x`, `repeat-y` 와 같이 축별로 반복을 설정하는 값과, space, round 등의 반복처리 값도 존재

> 전체 배경 무늬를 넣기 위해 반복을 사용하면 쉽게 적용할 수 있다.

### bacground-size

```css
.box1 {
  bacgkround-size: contain;
}
.box2 {
  bacgkround-size: auto 50%;
}
```

- 배경 이미지의 크기를 설정
- width, height 순으로 배경 이미지의 너비와 높이를 모두 지정하거나, 하나만 사용할 경우 `너비`만 적용된다.(높이는 자동- auto)
  - `%`로 크기 지정시 [MDN 설정 참고하기](https://developer.mozilla.org/ko/docs/Web/CSS/background-size) - `background-origin` 속성에 따라 결정되며, `background-attachment`가 fixed (고정)일 경우에는 **viewport(뷰포트)**의 너비가 기준.
- 다중 배경 이미지들의 크기를 개별로 조정하려면 `,`를 사용
- 아래와 같은 속성값을 이용하거나 px, % 등의 길이 단위를 이용하여 배경 이미지의 크기를 조절할 수 있다.
  - `auto` - 기본값. 원본 이미지의 크기가 그대로 유지되어 적용된다.
  - `contain` - 요소에 배경 이미지가 보이지 않는 부분없이 전체가 들어갈 수 있도록 이미지가 조정된다.(요소 영역에 따라 남는 부분이 생길수도 있다)
  - `cover` - 요소의 width, height 중 큰 값에 배경 이미지의 원본 비율을 유지하여 남김없이 맞춘다. 이에 따라 이미지의 일부분이 보이지 않을 수 있다.

### backgournd-attachment

- 요소의 배경 이미지의 고정과 관련된 속성
  - 스크롤 작동에 있어 배경 이미지의 고정 방법을 지정
- 다음과 같은 속성값을 사용
  - `scroll` - 기본값. 배경을 요소 자체에 고정. 요소에 존재하는 스크롤을 동작시켜도 배경은 요소에 고정된다.
  - `fixed` - 뷰포트에 대해 고정.
  - `local` - 요소의 콘텐츠에 대해 고정. 요소에 스크롤 존재 시 콘텐츠와 함께 스크롤.

> parallex 효과(시차 효과 - 멀리 있는 것은 거의 움직이지 않거나 천천히 움직이고, 가까이 있는 것은 아주 빨리 움직이는 현상, 천문학 관련 용어)를 주기 위해 `fixed` 를 활용할 수 있다. 가까운 것에 대해 좀 더 입체적인 느낌을 줄 수 있는 효과 또는 디자인.

### background-position

- 배경 이미지의 초기 위치를 지정하기 위해 사용하는 속성
- 초기값은 `0% 0%`라고 나와있는데 이는 좌측 상단에 위치하게 된다.(순서대로 각각 좌측과 상단의 시작 offset 기준)
  - position 값을 섞어서 4개로 사용시 시작 offset을 변경할 수 있다.
- 위치 지정 시 사용되는 다음의 값들을 하나나 여러개를 이용하여 적용 가능
  - top
  - right
  - bottom
  - left
  - +) center

### background-color

- 요소의 배경 색상을 지정하기 위해 사용하는 속성
- 색상값, transparent 키워드를 지정

### backgournd 단축 속성

- `background` 속성을 이용하여 배경 이미지와 관련된 속성들의 값을 모두 지정하여 사용할 수 있다.
  - `-attachment`
  - `-clip`
  - `-color`
  - `-image`
  - `-origin`
  - `-position`
  - `-repeat`
  - `-size` - position 바로 뒤에 위치, `/`로 구분

### background-origin

- 배경의 원점을 지정하는 속성
- border, padding, content 로 구분하여 지정할 수 있다.
  - `border-box`
  - `padding-box` - 기본값
  - `content-box`
- background-attachment 가 `fixed` 인 경우에는 무시된다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-background)