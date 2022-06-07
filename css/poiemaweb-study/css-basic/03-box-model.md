# CSS - 박스 모델(Box model)

- HTML 구조를 가지는 요소들을 어떠한 모습으로 렌더링하는지에 대해 학습

---

## CSS Box model

![Whiteboard (2)](https://user-images.githubusercontent.com/104971437/169486422-3a481677-126f-4672-bb56-0d7e3ef1f941.png)

- CSS에서는 HTML 요소들을 박스 모델이라고 하는 방법으로 화면상에 표시한다.
- 간단히 설명하자면 박스 모델은 요소를 하나의 상자 안에 표현하는 방법으로 상자의 크기나 위치, 속성 등을 지정하여 배치하거나 디자인을 가능하게 한다.
- 상자는 4개의 부분으로 이루어 진다.
  - margin
  - border
  - padding
  - content

### margin

- 요소에 대한 네방향(top, right, bottom, left)의 바깥 여백 영역을 설정한다.
- `margin`은 margin-top, margin-right, margin-bottom, margin-left 의 단축 속성이며 이 4가지 속성을 개별적으로 적용할 수도 있다.
  - 단순히 1가지 값을 명시하면 요소의 4면에 모두 적용된다.
  - 2가지를 사용하면 상하, 3가지를 사용하면 상, 좌우, 하 순으로 적용된다. - [MDN 참고하기](https://developer.mozilla.org/ko/docs/Web/CSS/margin#%EB%8D%94_%EB%A7%8E%EC%9D%80_%EC%98%88%EC%A0%9C)
- 간단한 수평 중앙 정렬을 위해 margin을 사용할 수도 있다.
  - `margin: 0 auto;`
  - 상하로는 여백은 갖지 않고(0), 좌우로는 auto 값을 사용 (auto는 브라우저가 자동으로 계산한 값을 적용하고자 할 때 주로 사용되는 값, 여기선 해당 요소의 좌우 바깥 여백이 동일한 값을 갖는다)

#### margin collapse

- 여백 상쇄
- margin 사용시 여러 요소(블록)의 상하 마진의 경우 제일 큰 쪽의 여백의 크기가 하나로 적용되는 현상을 말한다.
- MDN의 [3가지 기본 여백 상쇄 상황](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing) 참고
- 살펴본 바로는 일반 문서 흐름에서만 발생하는 현상이며 아직 배우진 않았지만 floating 이나 절대위치 지정요소에서는 절대 상쇄되지 않는다고 한다.

> 여백 상쇄가 왜 생기게 되었는지에 대한 내용은 외국 작성자가 정리한 한 [문서](https://medium.com/@joseph0crick/margin-collapse-in-css-what-why-and-how-328c10e37ca0)를 참고했다. 여백 상쇄 배경에는 관련있는 콘텐츠들 사이의 상하여백을 더 쉽게 만들기 위해 디자인되었다고 설명하고 있다. 예를 들어 여백상쇄가 없다고 가정했을 때, 한 콘텐츠 내부의 여러 문단을 구분하기 위해 margin-top, margin-bottom을 사용한다면 문단 사이사이에는 여백을 계산하여 동일하게 맞출 수 있지만 최상단이나 최하단의 여백의 크기는 일정하지 않을 수 있는 문제가 발생한다. 따라서 상하로 이어지는 흐름에서 콘텐츠 간 (특히 형제 요소 간에) 구분을 명확히하고 바깥 여백이 잘 적용될 수 있도록 가장 큰 여백을 가진 요소를 기준으로 상쇄가 이루어진다고 생각해 볼 수 있다.

### padding

- padding은 요소의 안쪽(border 안)에 여백을 설정하기 위해 사용한다.
- margin처럼 개별 속성이 따로 존재하며 단축속성으로 사용가능하며 사용법은 거의 비슷하다.

### border

- border는 요소에 대한 테두리를 지정할 때 사용한다.
- border는 단축 속성으로 다음의 3가지 속성의 값을 통해 표현된다.
  - border-width - 굵기
  - border-style - 스타일
  - border-color - 색상
- border는 border-style 값이 없으면 border-width나 border-color가 지정되어 있더라도 화면상에 표현되지 않는다.
  - 보통 `border: 1px solid red;` 와 같이 단축 속성으로 많이 사용된다.
- 요소의 네 방향에 대한 개별속성이 존재하여 각각 따로 적용 가능하다.

#### border-radius

- 테두리 모서리를 둥글게 표현하기 위해 사용한다.
- border-radius은 단축 속성으로 값을 여러 개 사용하여 원하는 부분의 모서리를 디자인할 수 있다.(개별 속성을 활용해도 된다.)
- 길이 단위(px, em 등)나 %를 사용하여 모서리를 깎는다.
  - 길이 단위를 사용할 경우 `원의 반지름`의 값으로 계산되어 모서리의 굴곡이 설정된다.
  - 퍼센트의 경우 요소의 너비와 높이 길이에 대한 백분율로 결정된다.

### box-sizing

- 요소에 대한 너비와 높이를 계산하는 방법을 지정할 때 사용하는 속성
  - width와 height 속성을 이용하여 요소의 너비나 높이를 설정할 수 있다.
- 계산법은 아래 2가지 종류로 구분된다.
  - `content-box` - 따로 명시하지 않을 시 초기 기본값
  - `border-box`
- box-sizing 속성값은 상속되지 않는다.
  - Tip) Reset CSS로 따로 설정하여 사용하기

#### content-box

```css
div {
  width: 100px;
  height: 100px;
  border: 10px solid red;
  padding: 10px;
  margin: 5px;
}
```

- 콘텐츠 영역을 기준으로 width와 height가 적용된다. (안팎의 여백이나 테두리는 포함되지 않는다)
- 위 예제 코드에서 div 요소가 가지는 전체 너비나 높이는 margin을 제외한 140px이 된다.
  -  10 + 10 + **100** + 10 + 10

#### border-box

```css
div {
  box-sizing: border-box;
  width: 100px;
  height: 100px;
  border: 10px solid red;
  padding: 10px;
  margin: 5px;
}
```

- 콘텐츠 영역, padding, border가 포함된 값으로 계산한다.
- 위 코드의 경우 div 요소의 전체 너비는 margin을 제외한 `100px` 이 된다.
  - width나 height가 콘텐츠가 아니라 실질적으로 border에 맞춰지기 때문에 content 영역의 너비는 이에 맞게 60px의 너비와 높이를 가지게 된다.
  - 10 + 10 + 60 + 10 + 10 = **100**

> 정리하자면 content-box는 콘텐츠 영역으로 계산, border-box는 콘텐츠 영역과 패딩, 테두리를 포함하여 계산한다고 생각하면 된다. 박스모델 전체(padding, border 포함)를 지정하는 border-box를 사용하면 CSS 레이아웃을 직관적으로 사용할 수 있다고 조언하고 있다.
