# CSS - image 요소 아래 공간 관련 학습

- 인라인 특성을 가지는 이미지 요소 사용 시 생기는 여백 공간에 대한 이해와 해결법 학습

--- 

## Typography

![image](https://user-images.githubusercontent.com/104971437/172333527-efde456c-fd38-49e1-b63a-e8bb27dfb438.png)

- [타이포그래피](https://ko.wikipedia.org/wiki/%ED%83%80%EC%9D%B4%ED%8F%AC%EA%B7%B8%EB%9E%98%ED%94%BC)
- 타이포그래피는 간단하게 문자나 활자 등의 기호 배치를 구성하고 표현하는 것을 의미한다.
- 관련 용어
  - ascender(어센더), descender(디센더) : 로마자 표기에서 baseline 기준으로 위(ascender)나 아래(descender)로 튀어나오는 부분을 뜻한다.
  - x-height : x-높이라 하여 baseline과 상위 평균 맞춤선인 mean line 사이의 거리를 말한다.
  - mean line : x-높이의 상단에 위치하는 가상의 선
  - baseline : 문자가 실제로 배치되기 위한 기준이 되는 선.

### image 요소

![image](https://user-images.githubusercontent.com/104971437/172345068-0bf68dd5-aa5f-4a85-8499-dd9e34486c4f.png)

- image 요소는 일반 텍스트와 같이 **인라인** 특성을 갖는다.
- line-height를 늘려보면 위 이미지와 같이 디센더 공간을 확인할 수 있는데 이는 이미지 요소가 텍스트와 같이 baseline 기준으로 배치되기 때문이다.

#### 공간 해결방법

- 이미지 요소의 특성을 `block` 으로 변경
- 인라인 요소나 테이블 셀의 수직 정렬에 사용되는 `vertical-align`을 bottom으로 조정하여 표시 위치를 조정할 수도 있다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-removing-white-space-image-element)