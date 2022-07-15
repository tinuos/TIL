# JavaScript - 브라우저 렌더링

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 렌더링 개념

- 렌더링(rendering)
  - 브라우저에서 렌더링은 HTML, CSS, JS 가 브라우저에서 출력되는 것을 의미한다.
- 브라우저 회사마다 이러한 렌더링 엔진을 가지고 있다.
  - 크롬 : 블링크
  - 사파리 : 웹킷
  - 파이어폭스 : 게코

## 렌더링 과정

- 렌더링 과정을 이해하기 위해서는 DOM과 CSSOM을 이해해야 한다.
- DOM(Document Object Model)
  - 문서 내에 HTML 요소를 객체화하는 것(문서를 구조화)
  - 트리(Tree) 형태로 구조화한다.
- CSSOM(CSS Object Model)
  - CSS를 대상으로 객체화하는 것
  - DOM Tree를 통해 구조화된 노드에 스타일이 붙여지는 개념으로 CSSOM 도 트리 형태로 구조화된다.
- 렌더링 트리(Rendering Tree)
  - DOM 트리와 CSSOM 트리를 결합하여 렌더링 트리를 생성
  - 페이지를 렌더링 하기 위해 필요한 노드만 포함된다.

### 레이아웃 단계

- 렌더링 트리가 생성되면 레이아웃이 가능해진다. 
- 레이아웃 단계에선 각 요소들이 페이지에서 배치되는 위치와 방법을 결정한다. (박스 모델)
- DOM 트리의 노드 수가 많을 수록 성능에 영향을 받을 수 있다.

### 페인트 단계

- 화면에 픽셀을 그리는 단계. 렌더트리 생성 - 레이아웃 단계를 거치면 페인팅이 가능하게 된다.
- 레이아웃 단계에서 계산된 스타일 속성값을 통해 픽셀로 변환되게 된다.

---

## 리플로우(Reflow), 리페인트(Repaint) 개념

- 리플로우
  - 이벤트 발생, 스타일 변경 등이 발생하는 경우 영향을 받는 모든 노드에 대해 렌더링 트리 생성과 레이아웃 과정을 다시 수행하는 것을 말한다.
  - 대표 속성
    - position, width, height, margin, padding, border, border-width, font-size, font-weight, line-height, text-align, overflow 등
- 리페인트
  - 리페인트는 페인트 단계를 다시 수행하는 것.
    - 리플로우가 발생한 경우
    - 레이아웃에 영향을 주지 않는 변경이 발생한 경우
  - 대표속성
    - background, color, text-decoration, border-style, border-radius 등

---

## 정리

- HTML를 파싱하여 DOM 트리를 생성하고 DOM 트리를 통해 구조화된 노드에 스타일을 붙인 CSSOM 트리를 생성. 이 두 트리를 결합하여 렌더링 트리를 생성하고 렌더링 트리에 있는 노드들이 갖는 스타일 속성을 통해 스타일 값 계산 및 레이아웃 작업을 실행. 이 후 픽셀로 그려지는 페인팅 단계를 거쳐 화면에 렌더링된다.
- MDN 에선 이러한 렌더링 단계를 CRP(Critical rendering path)라고 설명(중요 렌더링 경로). HTML, CSS, JS 등의 자원은 일단 로드가 되어야하기 때문에 path라고 설명한 것 같다. 최적화와 관련하여 이러한 자원의 로드 순서를 관리하는 것이 필요하다고 설명. (최적화 비용 관리에 대해서는 나중에 따로 정리하기 - 애니메이션 처리와 관련된 내용도 살펴봐야 겠다)

---

**참고 자료**

- [MDN - 중요 렌더링 경로](https://developer.mozilla.org/ko/docs/Web/Performance/Critical_rendering_path)
