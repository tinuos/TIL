# CSS - 상속과 스타일 적용 우선 순위

- 스타일 상속에 대한 이해
- cascading을 이해하고 이와 관련된 명시도, 구조적인 적용 우선순위에 대해 학습

---

## 스타일 상속

- inheritance
- 상위 요소(조상, 부모)가 갖는 스타일 속성들이 하위 요소(자손, 자식)들에게 그대로 적용되는 것을 상속이라 한다.
- 기본적으로 속성별로 상속이 되는 것과 되지 않는 것으로 분류되어져 있다.
  - 상속되는 속성 예
    - visibility, opacity, font, color, line-height, text-align, white-space, 
  - 상속되지 않는 속성 예
    - width, height, margin, padding, border, box-sizing, display, background, vertical-align, text-decoration, position, top, right, bottom, left, z-index, overflow, float
- color 속성은 특정 요소(button)에 따라 상속받지 않는 경우도 존재한다.
- 상속되지 않는 요소의 스타일 정의 시 해당 속성을 그대로 상속받아 사용하기 위해 `inherit` 키워드를 사용하여 명시적으로 상속받게 할 수 있다.

---

## Cascading

- 앞 서 배운 내용 중 CSS로 요소의 스타일을 다양하게 지정할 수 있는 방법들(선택자 활용방법, 스타일 적용방법)에 대한 기초를 학습했다.  이러한 여러 방식의 스타일 규칙이 하나의 요소를 특정하고 있다면 어느 것이 적용되어야 할까?
- Cascading은 사전적 의미로 폭포수의 뜻을 가지고 있는데, CSS는 이러한 의미를 갖는 스타일 적용 우선순위 규칙에 따라 요소에 특정 스타일이 부여된다.

### 중요도

- 스타일 선언에 대한 우선순위 적용 관련
- 스타일 규칙이 **어디에** 선언되어 있는지에 따라 적용 우선순위가 달라진다. 아래는 제일 우선 적용되는 순서부터 나열한 목록.
  - head 요소 내의 style 요소
  - head 요소 내의 @import 문
  - link 요소로 연결된 CSS 파일
  - link 요소로 연결된 CSS 파일 내의 @import 문
  - 브라우저 디폴트 스타일 시트
- HTML 문서 상 외부 스타일을 지정하는 link 요소가 style 요소보다 먼저 작성되었어도 스타일은 style 요소에 작성된 스타일이 먼저 적용된다.

> 웹폰트나 외부 스타일 규칙을 가져올 때 스타일 시트 안에서 @import 규칙을 사용할 경우, 특히 그로 인해 스타일 연결 구조가 복잡해질 수록 우선순위 적용에 더 유의하여야 한다.

### 명시도

- Specificity
- 주어진 CSS 선언에 적용되는 `가중치(weight)`. 아래와 같은 순서에 따라 우선순위가 적용된다.

> `!important` \> 인라인스타일 \> ID 선택자 \> class/속성/가상 선택자 \> 태그 선택자 \> 전체 선택자 \> 상속 속성

- [specifishity.com](https://specifishity.com/)에 명시도 관련 가중치 계산법이 그림 예시로 잘 나와있다.

### 선언 순서

```html
<!-- poiemaweb 예제 -->
<!DOCTYPE html>
<html>
<head>
  <style>
    p { color: blue; }
    p { color: red; }

    .red { color: red; }
    .blue { color: blue; }
  </style>
</head>
<body>
  <p>Will be RED.</p>
  <p class="blue red">Will be BLUE.</p>
</body>
</html>
```

- 나중에 선언된 스타일이 우선 적용
- 위 예제 이해하기
  - 태그 선택자의 경우 red 색상이 나중에 선언되어 문서의 Will be RED 문단은 빨간색이 된다.
  - 클래스 선택자도 마찬가지. 2번째 p요소에는 `blue red` 순으로 클래스가 부여되어 같은 속성에 한해서는 red 클래스가 가지는 빨간색이 적용될 것 같지만 blue가 적용된다. (선언 상 나중에 위치한)

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-inheritance-cascading)