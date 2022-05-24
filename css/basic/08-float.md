# CSS - 요소 정렬 관련

- 정렬 방식 중 하나인 `float`에 대하여 학습

---

## float

- float은 텍스트나 인라인의 요소가 일반적인 문서 흐름에서 빠져나와 좌우측의 흐름에 배치되도록 할 때 사용하는 속성
- img 요소를 텍스트 콘텐츠에 그대로 사용할 시 img 가 인라인 특성을 갖기 때문에 아래 이미지와 같이 해당 행의 높이를 모두 차지하게 된다.

![image](https://user-images.githubusercontent.com/104971437/169974062-a5cae245-75a4-474c-9b80-35b008aec4c6.png)

- float을 사용하게 되면 현재 진행중인 흐름에서 빠져나와 사용한 속성값에 따라 좌측이나 우측에 이미지를 배치할 수 있어 간단한 레이아웃 구조를 구성할 수 있다.

![image](https://user-images.githubusercontent.com/104971437/169975078-e425a264-b89c-4e5f-81a1-310ecb4cfc7d.png)

> 요소의 배치가 어느정도 가능하다는 점에 따라 모던 레이아웃 방식(flex-box, grid 등)의 기술이 나오기 전까지 스타일 구조를 잡을 때 많이 사용하던 속성이었다고 한다.

### 정렬 관련

- float 속성값을 사용하면 해당 요소는 떠다닌다고 표현(부동, float)한다. - 일반 문서 흐름에서 벗어나는 것
- float 에서는 다음의 속성 값을 이용하여 정렬이 가능
  - `none` - 기본값. 요소가 '부동'되지 않는다.
  - `left` - 요소가 좌측부터 가로로 정렬된다.
  - `right` - 요소가 우측부터 가로로 정렬된다. 먼저 작성된 요소가 제일 우측에 정렬된다. (역순)
- float은 좌우측 정렬만 가능하기 때문에 가운데 정렬은 `margin` 속성을 활용해야 한다. (width값 부여 및 margin 가로 auto)

### width 관련

![image](https://user-images.githubusercontent.com/104971437/169977991-547bfb18-c38b-4413-b317-26f7237e5710.png)

- float 속성을 적용하는 블럭 레벨 요소가 width 값을 갖지 않으면 해당 요소는 콘텐츠에 맞게 width 값이 최소화 된다.
- 위 이미지에서 주황색 박스는 아무것도 적용하지 않고, 빨간색 박스에는 `float:left`가 적용되어 있는 예제이다. 코드 작성 순서는 빨간색 박스, 주황색 박스 순. 두 박스 모두 블럭 레벨 요소에 width 값을 주지 않은 상태로, 주황색 박스가 빨간색 박스 너비와는 상관없이 100%를 차지하는 것을 확인할 수 있다. 빨간색 박스는 앞 서 말한 float width 특성에 따른 너비 대로 왼편에 부유하여 자리를 차지하게 되는 구조. 주황색 박스의 콘텐츠는 부유하고 있는 자리 이후에 남는 공간에서 표시된다.

### clearfix

- float 정리시 `clear` 속성을 사용
- float을 사용하게 되면 주변 요소의 배치에 영향을 미치기 때문에 따로 해제시켜 주어야 하는 작업이 필요하다. - [참고 자료](https://naradesign.github.io/float-clearing.html)
- 일반적인 흐름에서 벗어나기 때문에 float이 적용된 자식요소를 가지고 있는 부모 요소는 자식 요소들의 높이를 정확히 판별할 수 없어 정렬에 문제가 발생할 수 있다고 한다.
- 해결 방법
  - 부모 컨테이너에 overflow: hidden 적용
  - 부모 컨테이너에 clear를 위한 마지막 자식 요소를 따로 설정
  - 부모 컨테이너에 clear 관련 클래스 스타일을 따로 지정
    - `::after` 가상 요소 선택자를 이용한 방법 (아래 코드 참고)
  - 이 외에 inline-block, flow-root 등을 지정하는 해결법도 있다고 한다.

```css
.clearfix:after {
  content: "";
  display: block;
  clear: both;
}
```

- 컨테이너 마지막에 아무런 내용도 가지지 않고 단지 clear 해제 값만 가지는 요소를 가상 추가하는 방법으로 가장 깔금하고 간편한 방식이라고 poiemaweb에서 소개하고 있다.
- after는 content와 같이 사용되는 데 기본적인 특성은 **인라인**이다. 따라서, 가상요소의 display를 block으로 지정하여 해제한다.

> 왜 clearfix에서 display: block이 되어야 하는지에 대해 관련 자료를 찾다보니 BFC(Block Formatting Context)라는 용어가 나왔다. 일단 BFC로 흐름 적용을 위해 block으로 지정해야 한다라고만 이해하고 나중에 BFC와 floats(부동 요소)에 관한 내용을 따로 정리해야 겠다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-float)
- [MDN - float 학습](https://developer.mozilla.org/ko/docs/Learn/CSS/CSS_layout/Floats)