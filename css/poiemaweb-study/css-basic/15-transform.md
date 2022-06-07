# CSS - 트랜스폼

- 요소의 변형과 관련된 스타일을 제어하는 트랜스폼에 대하여 학습

---

## 트랜스폼(transform)

- 요소의 **형태(모양) 변환**에 관련된 기능을 제공. 형태 변환에는 크게 다음으로 구분된다.
  - 요소의 이동 (translate)
  - 요소의 크기 변화 (scale)
  - 요소의 기울기 (skew)
  - 요소의 회전 (rotate)
- 트랜스폼 자체는 애니메이션 효과가 제공되지 않는다. `transition` 이나 `animation` 을 함께 사용하여 효과를 부여한다.

### transform

- `transform` 속성은 트랜스폼 효과를 부여하기 위해 사용하는 속성이다.
- 속성값은 관련 [CSS 변형 함수](https://developer.mozilla.org/ko/docs/Web/CSS/transform-function)로 전달

#### 예시

```css
.box:hover {
  transition: 1s;
  transform: rotate(180deg) scale(1.5) translate(5px) skew(45deg);
}
```

### transform-origin

- 요소의 변형 적용 기준점을 지정
- 기본은 요소의 정중앙 (50%, 50%)
- %, px, 방향 키워드(top, right, bottom, left) 등을 사용하여 지정한다.

## 3D 트랜스폼

- 입체적 변형을 위해 사용
- 속성값에 `3d` 가 추가되며 x, y 이외에 z 축 관련 설정도 지정하여 변화시킬 수 있다.
  - translate3d(x, y, z)
  - scale3d(x, y, z)
  - rotate3d(x, y, z)

> 자세한 구문 및 사용법은 아래 문서 참고. transform 관련 함수와 좌표 계산 등을 통해 요소의 형태 변환 기능이 있다라는 정도로만 정리. 행렬 계산으로 변형을 처리하기 위해 `matrix()`라는 함수도 사용 가능하다.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-transform)
- [MDN - CSS 변형 사용하기](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Transforms/Using_CSS_transforms)
- [MDN - transform](https://developer.mozilla.org/ko/docs/Web/CSS/transform)


