# Bootstrap - Grid system

- 부트스트랩의 그리드 시스템을 이용한 반응형 스타일 적용을 학습

---

## 그리드 시스템

- 부트스트랩에서는 그리드 시스템이란 것을 제공
  - 그리드는 격자라는 의미를 가진다.
- 행과 열로 이루어지는 격자 무늬의 기능을 이용해 요소의 스타일 모양과 크기를 제어한다.

### 소개글

Grid system

Use our powerful mobile-first flexbox grid to build layouts of all shapes and sizes thanks to a twelve column system, six default responsive tiers, Sass variables and mixins, and dozens of predefined classes.

- 모바일 우선 flexbox grid 레이아웃 제공
- 12개의 컬럼과 기본 6개의 반응형 계층을 제공(?)
- Sass 변수와 mixin 등

### 동작 방식

- 6개의 반응형 지점을 제공
- 수직, 수평으로 중앙 정렬되는 컨테이너 제공
- 열 요소들을 감싸는 행(row) 기능
- 12개의 공간에 따라 자유롭게 조합 가능한 열(column) 기능
- 반응형 거터(Gutter)
  - 여기서 거터는 각 열 사이의 공간(padding)을 말한다.
- Sass 기능을 이용하여 그리드를 직접 생성 가능(사용자 정의)

#### 6개의 반응형 지점(중단점이라고 표현. breakpoints)

![image](https://user-images.githubusercontent.com/104971437/172546068-58593df8-82f0-405d-8fa0-fe0730ba1d65.png)

- 부트스트랩에서 지정한 크기를 기준으로 중단점이 발생. (기본 예제 코드 작성 후 화면 크기를 늘이거나 줄이다 보면 특정 지점에서 열의 크기가 변화하는 것을 확인할 수 있다 - 기본 컨테이너 기준)
- `col` 클래스 다음에 크기에 따른 접두사를 붙임으로써 해당 너비에 도달할 시 레이아웃을 제어할 수 있다. 
- 따로 중단점 접두사를 붙이지 않으면 동일한 크기를 가지게 된다.

#### 컨테이너 개념

- 부트스트랩의 기본 구성 요소로 그리드 시스템 사용시 필요.
- 반응형 중단점, 모든 중단점, 정의된 중단점에 따라 접두사를 달리 붙여 사용
  - `.container`
  - `.container-fluid`
  - `.continaer-{breakpoint}`

#### 열의 너비 설정

![image](https://user-images.githubusercontent.com/104971437/172549895-fe608e76-0c2e-4289-b532-51ef5eb92a19.png)

- 그리드 시스템에서 열은 `12`개의 공간에 따라 자동적으로 배치된다.
- 열 사용시 `col` 클래스명 뒤에 `1 ~ 12`까지의 숫자를 붙여 각각 크기를 조정할 수 있다. 
- 만약 열 비율의 총합이 12를 넘어가게 되면 위 이미지와 같이 해당 행에 배치되지 못하고 넘어가게 되므로 유의할 것.

![image](https://user-images.githubusercontent.com/104971437/172550358-903ea237-f691-4c29-9d9e-808afba138cd.png)

- 한 열에만 너비 비율을 설정하면 나머지 열은 남는 크기에 따라 자동으로 비율을 나눠 갖게 된다.
- 추가적으로 행을 여러번 중첩하여 사용 가능하다.


---

**참고 자료**

- [Bootstrap](https://getbootstrap.com/docs/5.2/layout/grid/)