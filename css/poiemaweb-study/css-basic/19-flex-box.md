# CSS - 플렉스 박스 레이아웃

- CSS3에서 나온 새로운 레이아웃 방식 중 하나인 flex box 모듈에 대해 학습

---

## flex box

- 의미를 그대로 풀어쓰면 유연한 상자라는 뜻
- flex 기술 관련 속성을 통해 **행과 열**을 기준으로 항목들을 좀 더 손쉽게 배치할 수 있는 레이아웃 방법
- 주요 특징
  - 행, 열 기준으로 설정하는 기준(중심 또는 간격)에 맞춰 배치가 가능하다.
  - 컨테이너에 맞춰 요소들이 가지는 너비나 높이가 일정한 크기를 가지게 할 수 있다.

> 행, 열이라는 기준이 명확한 1차원 레이아웃 기술로 가로, 세로 정렬에 있어 강력한 기능을 제공한다.

## 사용

![W3C - flex box](https://www.w3.org/TR/css-flexbox/images/flex-direction-terms.svg)

- flex Container, flex item
- flex 레이아웃을 적용하기 위해 부모 요소를 `display: flex`로 지정한다.
  - 지정된 부모 요소는 flex container가 되며 내부에 오는 바로 하위의 자식 요소들을 flex item 이 된다.
- flex container, flex item 별로 적용해야 하는 속성이 달라진다.
- 위 이미지와 같이 main 축과 cross 축이 교차하는 형태이며 설정하는 속성값에 따라 방향(행이나 열)이 달라질 수 있다.

### flex Container 관련 속성

#### flex-direction

- 주축(main axis)의 방향을 설정
- 기본값은 `row`로, 좌에서 우로 가로로 배치된다.
  - `row-reverse` : 우에서 좌로 가로 배치된다. 주 축은 오른쪽 끝에서 시작.
  - `column` : 위에서 아래로 세로로 배치된다. 주축의 시작은 위에서 시작.
  - `column-reverse` : 아래에서 위로 세로로 배치된다. 주축은 아래에서 시작.

#### flex-wrap

- 주축을 기준으로 항목들의 모든 너비의 합이 컨테이너의 너비를 넘어갈 때 줄바꿈에 대한 제어를 하기 위한 속성
- 기본값은 `nowrap`으로 개행이 일어나지 않고 1줄에 배치되며 모든 항목이 컨테이너 안에 배치될 수 있도록 너비가 줄어든다. overflow와 같이 사용 시 컨테이너를 넘치지 않고 스크롤을 생성할 수 있다.
  - `wrap` : 너비가 넘어갈 때 개행이 일어나며 flex-direction 방향을 그대로 따른다.
  - `wrap-reverse` : wrap과 반대 방향으로 쌓인다.

#### flex-flow

- flex-direction과 flex-wrap의 단축속성
- 기본값 `row nowrap`

#### justify-content

- flex 레이아웃에서 컨테이너의 **주축**을 기준으로 항목들을 정렬하기 위해 지정하는 속성
- 관련 속성값
  - `flex-start` : 주축의 시작점을 기준으로 정렬. 기본값
  - `flex-end` : 주축의 끝점을 기준으로 정렬.
  - `center` : 주축 기준 중앙 정렬.
  - `space-between` : 첫 항목과 마지막 항목은 주축의 시작과 끝에 정렬되고 항목들 사이에는 균등한 간격이 형성된다.
  - `space-around` : 모든 항목을 균등한 간격으로 정렬.

#### align-items

- flex 레이아웃에서 컨테이너의 **교차축**을 기준으로 항목들을 정렬하기 위해 지정하는 속성
- 관련 속성값
  - `stretch` : 교차축의 시작과 끝까지 꽉찬 길이를 갖는다. 기본값으로 만약 row 방향에서 항목 요소에 height를 설정하지 않으면 끝까지 늘어난다.
  - `flex-start` : 교차축의 시작점 기준으로 정렬
  - `flex-end` : 교차축의 끝점 기준으로 정렬
  - `center` : 교차축 기준 중앙 정렬
  - `baseline` : 컨테이너가 가지는 baseline을 기준으로 정렬

#### align-content

- flex 레이아웃에서 컨테이너의 **교차축**을 기준으로 항목간 정렬을 지정하기 위한 속성
- align-item이 행별로 정렬되는 것이라면, align-content는 모든 항목에 동일한 정렬을 적용.
- 관련 속성
  - `stretch` : 줄바꿈이 일어난 이후 균일한 공간에 정렬되어 배치. 기본값
  - `flex-start` : 교차축의 시작점을 기준으로 쌓여(stack)서 정렬된다.
  - `flex-end` : 교차축의 끝점을 기준으로 쌓여서 정렬.
  - `center` : 교차축을 기준으로 중앙 정렬
  - `space-between` : 교차축 기준 justify-content의 동작과 동일
  - `space-around` : 교차축 기준 justify-content의 동작과 동일

### flex Item 관련 속성

- flex item 요소에 개별적으로 적용할 수 있는 속성들에 대하여 알아본다.

#### order

- 배치 순서를 지정. 기본값은 0으로 HTML 작성 순서에 따라 배치된다.
- 양수, 음수 등을 값으로 사용하여 항목들간에 순서를 조정할 수 있다. 제일 빠른 순서를 가지는 항목이 먼저 배치된다.

#### flex-grow

- flex 컨테이너 내부에서 항목이 할당 가능한 정도를 지정할 때 사용. 
- 형제 요소 항목들과 상대적으로 공간이 확대된다.
- 기본값은 0.
- 음수는 무효
- 기본값이 0이기 때문에 컨테이너에 공간이 남을 경우 자동으로 확대되지 않는다.
- flex-grow가 어느 항목 하나에라도 적용되어야(또는 몇몇, 모든) 남는 여백에 대해 관련 속성값의 비율로 공간이 할당된다. 또한 컨테이너의 너비가 넓어지더라도 flex-grow에 설정된 대로 크기가 늘어나는 것을 확인할 수 있다. (기존에 남는 공간이 더 커지는 개념이기 때문에)

#### flex-shrink

- flex-grow와는 반대로 동작하는 속성. 축소될 때에 대한 값을 설정한다.
- 기본값은 1이며, 음수는 무효.
- 0을 지정하면 축소가 해제되는 것으로 기존의 너비를 그대로 유지한다.

#### flex-basis

```css
.item {
  width: 200px;
  height: 100px;
  line-height: 100px;
  text-align: center;
  background-color: orange;
  border: 1px solid blue;
}

.item:nth-child(3) {
  flex-basis: 100px; /* 우선 */
}
```

- 항목에 대한 너비의 기본값을 지정
- 초기 기본값은 auto
- px, % 등의 단위로 지정
- auto 값을 가지지 않는 flex-basis와 width가 동시에 적용된 경우 flex-basis가 우선한다.

#### flex

- flex-grow, flex-shrink, flex-basis의 단축 속성
- 기본값은 0 1 auto

#### align-self

- 특정 항목에 교차축을 기준으로 한 정렬을 부여하기 위한 속성
- align-items 보다 우선하여(override) 적용된다.
- 기본값은 auto로 컨테이너의 align-items의 계산된 값이 적용된다.
- 이 외에 관련 속성값은 align-items 처럼 `flex-start | flex-end | center | baseline | stretch` 등을 사용할 수 있다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-flexbox)
- [MDN - flexbox의 기본 개념](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- [MDN - Flexbox - 웹 개발 학습하기](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Flexbox)
- [MDN - CSS Flexible Box Layout](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout)