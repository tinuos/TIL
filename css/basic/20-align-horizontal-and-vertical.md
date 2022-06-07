# CSS - 수평 및 수직 정렬

- poiemaweb에서 CSS를 이용하여 수직 및 수평 정렬하는 방법에 대하여 학습

---

## 수평 정렬

### inline / inline-block

```html
<div class="container">
  <span class="test">A</span>
  <span class="test">A</span>
  <span class="test">A</span>
  <span class="test">A</span>
  <span class="test">A</span>
  <span class="test">A</span>
</div>
```

```css
.container {
  width: 500px;
  border: 1px solid #000;
  text-align: center;
}
```

- 정렬 대상이 인라인 요소나 인라인 블록 요소인 경우 해당 부모 요소에 `text-align: center`를 지정하면 중앙 정렬이 된다.

### block

```html
<div class="container">
  <div class="test"></div>
</div>
```

```css
.container {
  width: 500px;
  border: 1px solid #000;
}

.test {
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  margin: 0 auto;
}
```

- 정렬이 되는 대상 요소에 너비를 명시적으로 지정. 그리고 `margin-left, margin-right`를 `auto` 로 지정한다.
- 블록 요소의 경우 한 줄을 모두 차지하는 특성(width: 100%)으로 인해 너비를 따로 지정하지 않으면 중앙 정렬이 필요없다.

### 여러 개의 block 요소

```html
<div class="container">
  <div class="test"></div>
  <div class="test"></div>
  <div class="test"></div>
  <div class="test"></div>
  <div class="test"></div>
</div>
```

```css
.container {
  width: 800px;
  border: 1px solid #000;
  font-size: 0;
  text-align: center;
}

.test {
  box-sizing: border-box;
  display: inline-block;
  width: 100px;
  height: 100px;
  background-color: yellowgreen;
  border: 1px solid green; 
}
```

- 여러 개의 블럭 요소의 경우 모두 `inline-block`으로 바꾼 뒤 부모 요소에서 `text-align: center`로 정렬

### Flexbox

- flexbox를 이용하여 간단하게 수평 중앙 정렬 가능
- 부모 요소 스타일에 `display: flex`와 `justify-content: center`를 선언

## 수직 정렬

### inline / inline-block 요소

#### 한 줄(Single line)

- 정렬하고자 하는 요소의 부모에 상하로 동일한 padding을 지정하여 수직 중앙 정렬하는 방법
- padding을 사용할 수 없는 경우에는 요소의 높이와 행간 높이를 동일하게 설정한다.
  - 이 경우에 행간이 넓어질 수 있고, 클릭 등의 동작이 발생하지 않는 문제가 발생하기 때문에 여러 줄에선 사용하지 않아야 한다.

#### 여러줄(Multiple lines)

- 한 줄에서의 방법과 마찬가지로 padding을 상하로 적용시켜볼 수 있다.
- `vertical-align` 속성을 활용
  - 인라인이나 table의 셀에서의 수직 정렬을 위해 사용하는 속성
  - 블럭 요소에서는 사용할 수 없는 속성
  - baseline, top, bottom, middle 등의 키워드를 사용한다.
  - 요소의 라인 개념과 부모 요소에 대하여 상대적으로 수직 정렬이 적용되는 것을 이해하고 사용하는 것이 중요
- flexbox 활용
  - flex를 적용하면 인라인, 블럭 개념과는 별도로 요소를 항목대로 정렬할 수 있다.

### block 요소

#### 요소의 높이가 고정되어 있는 경우

![image](https://user-images.githubusercontent.com/104971437/172321569-8fec9456-af3e-46e2-a8c8-d150b8403065.png)

- position 을 이용하여 중앙 정렬한다.
- 부모 요소를 `relative`로 하여 기준을 주고, 요소의 높이의 반만큼 `margin-top`을 음수값으로 설정하여 중앙에 정렬되도록 한다.

#### 요소의 높이를 알 수 없는 경우

- 위 방법과 비슷하지만 transform(변형) 속성의 translateY(-50%)를 이용하여 다시 반만큼을 위로 이동시켜준다.

> 2가지 방법 position을 이용한 방법으로 부모 요소가 기준이 된다는 것이 포인트. offset의 시작점과 음수값의 이동을 이해하고 사용하는 것이 중요.

#### flexbox

- 부모 요소에 column 설정 후 justify-content를 이용하여 center로 정렬

## 수평 / 수직 정렬

### transform 이용

- 앞 서 블락 요소에서 배운 transform을 x축에도 활용하는 것
- top과 left를 50% 씩 준 뒤, 다시 transform을 이용하여 -50%씩 이동시키면 수직, 수평 중앙 정렬된다.

### flexbox 활용

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

---

## 정리

- CSS3 의 flexbox 기술이 나오기 전까지 활용되었던 수평, 수직 중앙 정렬에 대한 방법
  - 요소의 display 특성을 기준으로 변경하거나 관련 속성을 사용한다. (block, inline, inline-block)
  - 위치 요소로 지정하고 이동시켜 줌으로써 해결하는 방법 등
- flexbox
  - 축에 대한 기준으로 정렬되기 때문에 관련 속성값만 사용하면 되며, flex 사용 방향에 따른 축의 변경과 이에 대한 정렬 개념을 이해하는 것이 중요.

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-centering)