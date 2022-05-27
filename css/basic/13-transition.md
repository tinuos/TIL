# CSS - 트랜지션

- 요소의 상태변화를 일정시간 동안 제어하는 것에 대하여 학습

---

## 트랜지션

- transition
  -  (다른 상태·조건으로의) 이행, 과도라는 의미를 가진다.
  - CSS에서는 요소의 2가지 상태 사이에 `trasition` 이라는 속성을 이용하여 변화를 줄 수 있다.

### transition

- `transition` 속성은 아래의 속성들에 대한 단축 속성이다.
  - `transition-delay` - default : 0s
  - `transition-duration` - default : 0s
  - `transition-property` - default : all
  - `transition-timing-function` - default : ease
- **transition은 자동으로 발생하지 않는다.**
  - 요소의 상태 변화와 관련된 **가상 클래스 선택자**나 JS를 이용한 제어에 의해 발동
- 자동적으로 상태 변화를 제어하기 위해서는 **CSS 애니메이션 기능**을 사용해야 한다.

#### transition-property

- 기본값 : all
- 트랜지션의 대상이 되는 속성을 지정
- 지정하지 않을 경우 기본값에 따라 모든 속성이 트랜지션의 대상이 된다.
- 여러개의 프로퍼티 지정 시 `,`를 활용
- 모든 속성이 trasition-property로 동작하는 것은 아니다. (아래 poeimaweb 문서 참고)
- transition이 적용되는 속성들 중 레이아웃 변화와 관련된 속성들은 브라우저의 계산이 필요하기 때문에 성능 저하의 원인이 되기도 한다. (아래 poeimaweb 문서 참고, 주로 블럭 레벨 및 font 관련 속성들)

#### transition-duration

- 기본값 : 0s
- 지속시간에 대한 설정
- 기본값이 0이기 때문에 시간을 따로 설정하지 않을 경우 트랜지션 효과가 발생하지 않는다. - `transition` 단축 속성에선 반드시 지정해야 하는 속성값이다.
- transition-property 값과 1:1로 대응
  - 마찬가지로 `,`로 구분하며 순서대로 대응하게 된다.

#### transition-timing-function

- 기본값 : ease
- 타이밍 함수라 하여 transition의 변화에 효과를 부여할 수 있다.
- 기본적인 [키워드](https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function#values)가 제공된다. 키워드와 관련된 효과는 [이징 함수](https://easings.net/ko) 예제 참고
  - `ease`
  - `linear`
  - `ease-in`
  - `ease-out`
  - `ease-in-out`
- cubic bezier([베지에 곡선](https://ko.wikipedia.org/wiki/%EB%B2%A0%EC%A7%80%EC%97%90_%EA%B3%A1%EC%84%A0))를 계산하는 함수를 활용할 수도 있다.
  - ex) cubic-bezier(0.1, 0.7, 1.0, 0.1)

#### transition-delay

- 기본값 : 0s
- 대기시간을 지정하는 속성으로 실제 변화 시작 시간을 늦추기 위해 사용
- 지정된 시간만큼 대기한 뒤 트랜지션 효과가 발동된다.

> 트랜지션 생성기 사이트를 활용하여 다양한 효과들을 눈으로 확인하면서 작업하는 편이 효율적일 것 같다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-transition)