# CSS - 요소의 위치(position)

- 요소의 위치를 지정하는 방법과 관련 속성에 대하여 학습

---

## position

- HTML 문서 상에서 요소의 위치를 지정하기 위해 사용하는 속성
- 위치와 관련된 **top, right, bottom, left** 속성 등을 함께 사용하여 배치한다.
- 위치 지정과 관련된 `키워드 속성값`을 사용한다.
  - static
  - relative
  - absolute
  - fixed
  - sticky

### static

- 요소의 위치 지정과 관련된 기본값.
- 일반적인 문서 구조 흐름에 따라 요소를 배치한다. 따로 position 을 설정하지 않은 요소는 static을 가지게 된다.
- 위에서 아래로, 왼쪽에서 오른쪽으로 순서에 따른 배치 기준을 가지며, 부모 요소 내부에 포함된 요소는 부모 요소 위치를 기준으로 위의 배치가 적용된다.
- **위치 지정과 관련된 속성들(top, right, bottom, left, z-index)을 무시한다.**

### relative

![image](https://user-images.githubusercontent.com/104971437/169940527-36a08e3f-ba29-4b69-ba8a-be7794daaf5d.png)

- 요소의 상대적 위치를 지정
- 요소가 가지는 static 위치 기준에 따라 위치 지정 속성들을 이용하여 위치를 이동시킬 수 있다.
- 일반 문서 흐름에 따라 배치되기 때문에 요소의 크기 만큼 페이지 레이아웃에서 공간을 차지한다.
- **좌표 관련 위치 속성(top, right, bottom, left 등)들을 사용할 수 있다는 것이 포인트**이다.

### absolute

![image](https://user-images.githubusercontent.com/104971437/169941585-db2eae3f-b377-4141-889d-5e7cb1ed7d92.png)

- `가장 가까운 위치 지정 조상 요소(static이 아닌 relative, absolute, fixed 로 선언되어 있는)`를 기준으로 위치 관련 속성을 이용해 위치를 지정할 수 있다.
- 모든 조상 요소가 static일 경우 `document body`를 기준으로 하여 배치될 수 있다.
- 일반 문서 구조 흐름에서 벗어나며, 공간을 차지하지 않는다. (부유, 부유 객체?)

![image](https://user-images.githubusercontent.com/104971437/169941919-273bbec7-832c-483a-80e2-bf04f3fb0f65.png)

- **absolute 적용 시 블럭 레벨 요소의 너비(width)는 인라인 요소처럼 콘텐츠에 맞게 변화된다는 것에 유의할 것!(적절한 width를 따로 설정)**

> 일반적으로 부모 요소에 relative를 준 후 이동시키고자 하는 자식 요소에 absolute를 주는 방식으로 위치를 지정한다. 절대 위치라는 개념은 부모 요소가 위치지정 요소가 아닌 이상 어디에도 위치시킬 수 있기 때문(document body 기준)

### fixed

- 고정 위치
- 부모 요소와는 관계없이 **뷰포트를 기준으로 요소를 배치한다**
- 스크롤 작동과 관계없이 항상 화면의 같은 곳에 위치할 수 있다.
- absolute 와 마찬가지로 일반적인 문서 구조의 흐름에서 제외되며, 기존 레이아웃에서 공간을 차지하지 않는다. 또한 블럭 요소의 경우 width가 콘텐츠에 맞춰짐을 유의.

> 보통 사이트에서 배너 광고나 제일 위로가기 버튼, 챗 봇 서비스 버튼 등에 많이 사용. header의 사이드 메뉴 고정에서도 볼 수 있었다.

---

## z-index

![image](https://user-images.githubusercontent.com/104971437/169944467-c853fa57-8a82-4536-bde6-5d8b532be4b6.png)

- 요소에 `z축`의 순서를 지정하기 위해 사용하는 속성
- static이 아닌 위치지정 요소에 대하여 `쌓임 맥락`을 형성 가능하게 한다.
- 다음의 값을 통해 사용
  - `auto` - 기본값. 새로운 쌓임 맥락을 생성하지 않고 부모 요소에서의 쌓임 맥락의 위치와 동일
  - `정수값` - 값이 클수록 화면에 더 가깝게 된다.

> 쌓임 규칙에 대한 자세한 내용은 [이 문서](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Positioning/Understanding_z_index)를 참고. 

---

## overflow

- 요소의 콘텐츠의 양이 많아 요소의 블락 영역에 맞출 수 없을 때 처리하기 위한 속성
- 다음의 키워드 값을 통해 사용한다.
  - `visible` - 기본값. 영역을 벗어나더라도 표시한다.
  - `hidden` - 영역을 벗어난 부분은 보이지 않게 한다.
  - `scroll` - 가로든 세로든 영역을 벗어나지 않더라도 스크롤를 표시
  - `auto` - 가로나 세로, 또는 둘 다 영역을 벗어나는 경우에만 스크롤을 표시
- 특정 방향의 스크롤 표시를 위해서는 `overflow-x`나 `overflow-y`를 사용한다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-position)