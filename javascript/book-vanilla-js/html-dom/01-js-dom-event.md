# JavaScript - DOM 이벤트

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## 이벤트

- 사용자의 상호작용(클릭, 스크롤 등)이나 비동기 작업 등을 인해 발생하는 액션들을 이벤트라고 한다(시스템 내에서 일어나는 사건).
- DOM 내에 Event 객체가 있고 이 인터페이스를 기반으로 다양한 이벤트들로 구성된다.
- 요소들에게 이벤트 리스터를 부여하거나 해제하여 이벤트에 반응하도록 할 수 있다.
  - 이벤트 리스너는 의미 그대로 이벤트를 감지하는 것으로 이벤트가 발생했을 때 처리할 함수 로직을 전달한다.
  - 웹 브라우저는 이러한 이벤트 리스너를 가지고 있다가 이벤트가 발생하면 관련 함수를 실행시키는 것.(앞 서 학습한 이벤트 큐 - 이벤트 리스너 - 콜스택 내용)
  - 일반적으로 addEventListener, 해제는 removeEventListener 메서드를 사용하여 이벤트를 등록하거나 해제할 수 있다.
  - addEventListener(type, listener)
    - 이벤트 타입과 처리할 리스너를 등록한다.
    - 타입의 경우 문자열로 전달하며 이벤트 유형에 따라 키워드들이 정해져 있다.
    - 리스너로는 객체 또는 콜백 함수가 전달되는데 주로 콜백 함수를 많이 사용한다.
    - 3번째 인자는 옵션으로 이벤트 전파와 관련된 옵션으로 여기선 따로 정리하지 않는다.
    - removeEventListener() 도 추가 메서드와 유사한 방식으로 사용

> 이벤트 종류는 무수히 많은데 이 중  책에 정리된 주요 이벤트들만 MDN 내용을 참고하여 정리한다.

### click 이벤트(onclick)

```html
~
  <button>이 곳을 클릭하세요</button>
  <script>
    let btnEls = document.getElementsByTagName('button');

    function startAlert() {
      alert(`${btnEls.item(0).innerText} 버튼이 눌렸습니다.`);
    }
    
    btnEls.item(0).addEventListener('click', startAlert);
  </script>
~
```

- 마우스 이벤트 중 하나 (MouseEvent 인터페이스)
  - click 이 외에도 dblclick, mouseup, mousedown 등이 있다.
- 마우스의 주 버튼이 눌렀다가 놓였을 때를 감지하는 이벤트

### change 이벤트(onchange)

```html
~
  <select id="menu">
    <option value="Ramen">라면</option>
    <option value="Udon">우동</option>
    <option value="gimbap">김밥</option>
  </select>
  <script>
    const menu = document.getElementById('menu');

    function printMenuOption() {
      console.log("어떤 메뉴가 선택되었습니다.");
    }

    menu.addEventListener('change', printMenuOption);
  </script>
~
```

- 사용자에 의해 값이 바뀔 때 발생하는 이벤트
- input, select, textarea 등의 요소에서 감지할 수 있는 이벤트이다.

### focus 이벤트(onfocus)와 blur 이벤트(onblur)

- focus는 집중하다, blur는 흐려지다라는 의미

```html
~ 
  <label for="input-box">인풋 상자</label>
  <input type="text" id="input-box" />
  
  <script>
    const inputBox = document.querySelector('#input-box');

    function focusTest() {
      console.log("현재 상자가 포커스되었습니다.");
    }
    function blurTest() {
      console.log("포커스된 요소를 빠져나갔습니다.");
    }

    inputBox.addEventListener('focus', focusTest);
    inputBox.addEventListener('blur', blurTest);
  </script>
~
```

- focus 이벤트는 요소가 현재 집중받고 있는 상태인지를 감지하는 이벤트. 마우스로 선택되었거나 입력 요소 등에서 입력 필드에 포커스가 되는 경우(입력 대기 상태가 되는) 등을 예로 들 수 있다.
- blur 는 포커스가 해제될 때 발생하는 이벤트이다. 사용자가 값을 입력한 후 빠져나가려고 할 때 형식을 체크하는 용도로 활용해 볼 수 있다고 설명.

### key 이벤트(onkeydown, onkeypress, onkeyup)

```html
~
  <label for="input-box">인풋 상자</label>
  <input type="text" id="input-box" />
  
  <script>
    const inputBox = document.querySelector('#input-box');

    function printKeyDown(event) {
      console.log(event.type);
      console.log(`${event.key} 키가 눌렸습니다.`);
    }
    function printKeyPress(event) {
      console.log(event.type);
      console.log(`${event.key} 키가 눌려지고 있습니다.`);
    }
    function printKeyUp(event) {
      console.log(event.type);
      console.log(`${event.key} 키가 떼졌습니다.`);
    }

    inputBox.addEventListener('keydown', printKeyDown);
    inputBox.addEventListener('keypress', printKeyPress);
    inputBox.addEventListener('keyup', printKeyUp);
  </script>
~
```

- 키보드 입력과 관련된 이벤트
- 키 입력 시 keydown, keypress, keyup 순서로 이벤트가 발생
  - keydown은 키가 눌렸을 때
  - keypress는 키가 계속 눌려지고 있을 때
  - keyup은 누르고 있던 키를 땐 후
- 추가 내용
  - input 필드 값은 event.target.value 로 가져올 수 있다.

### scroll 이벤트(onscroll)

```html
~
  <p style="width: 200px; height: 100px; overflow-y: auto">
    Lorem ipsum dolor sit amet consectetur, adipisicing elit. Maxime quia dolor quasi aliquam necessitatibus amet nihil, fugit placeat neque mollitia officia aut dolores error deserunt nesciunt in porro ullam dolorum!
  </p>

  <script>
    const pEls = document.getElementsByTagName('p');

    function scrollTest() {
      console.log('스크롤 이벤트 감지');
    }

    pEls.item(0).addEventListener('scroll', scrollTest);

  </script>
~
```

- 문서나 요소에서 스크롤될 때 발생하는 이벤트
- 스크롤 이벤트를 제어하여 무한 스크롤 구현이 가능
  - 무한 스크롤은 스크롤이 최하단에 도달했을 때 다시 관련 콘텐츠를 로드하는 기법을 말한다.

### touch 이벤트

```html
~
  <p>
    Lorem ipsum dolor sit amet consectetur, adipisicing elit. Maxime quia dolor quasi aliquam necessitatibus amet nihil, fugit placeat neque mollitia officia aut dolores error deserunt nesciunt in porro ullam dolorum!
  </p>

  <script>
    const pEls = document.getElementsByTagName('p');

    function touchStartTest() {
      console.log('터치 이벤트 감지');
    }

    pEls.item(0).addEventListener('touchstart', touchStartTest);

  </script>
~
```

- 스마트폰, 태블릿 같은 터치 인식을 가진 장치에서 화면 터치 시 발생하는 이벤트
- touchtstart, touchend, touchcancel, touchmove 등의 이벤트가 있다.

### load 이벤트(onload), unload 이벤트(onunload)

```js
window.addEventListener("load", fucntion() {

})
```

- load는 페이지 내 모든 리소스가 로드되었을 때 발생하는 이벤트
- 모든 DOM 요소가 렌더링이 되고 난 이후에 발생
- 위와 같이 모든 DOM 요소가 load 된 이후에 DOM을 조작하는 코드를 구현해볼 수 있다.

> load 관련해서 좀 더 찾아보니 DOMContentLoaded 이벤트랑 많이 비교하는 글을 볼 수 있다. DOMContentloaded 는 DOM 트리까지만 로드되었을 때가 기준이 되는 이벤트(리소스 로드는 제외). 빠른 실행 속도를 위해서 사용된다.
 
- unload는 현재 웹 페이지에서 이동이 발생하거나 브라우저 창을 닫을 때 발생하는 이벤트
- 책에서는 창닫기 시 로그아웃 처리와 관련된 내용을 설명. (unload 이벤트를 이용하여 자동 로그아웃을 실행 - 보안 관련)

### 추가 내용

```html
~
  <div class="box"></div>

  <script>
    const box = document.querySelector('.box');

    box.style.background = 'yellowgreen';
    box.style.width = '300px';
    box.style.height = '300px';
    box.style.borderRadius = '50%';
  </script>
~
```

- 요소가 가지는 속성 중 `style` 을 이용하여 요소의 스타일을 제어할 수 있다.
- `.`을 이용한 객체 속성 할당 방식으로 적용.
- css 속성명을 카멜 표기법을 선택하고, 관련 값을 할당하는 방식이다.

---

**참고 자료**

- [MDN - 이벤트 참조](https://developer.mozilla.org/ko/docs/Web/Events)
- [MDN - Event](https://developer.mozilla.org/ko/docs/Web/API/Event)