# JavaScript - HTML DOM

> [바닐라 자바스크립트 - 고승원 (비제이퍼블릭)](http://www.yes24.com/Product/Goods/105608999) 도서를 읽고 학습한 내용을 정리한 내용입니다.

---

## HTML DOM

![위키백과 DOM 이미지](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DOM-model.svg/330px-DOM-model.svg.png)

- DOM : The Document Object Model
- 문서 객체 모델
- HTML, XML 문서에 있는 모든 요소에 접근 가능하도록 하는 인터페이스로 W3C의 표준이다.
- DOM을 이용하여 웹 페이지가 가지는 구조를 프로그래밍 언어들에서 사용할 수 있게 된다.
- 브러우저는 표준에 따라 DOM이 구현되어 있다.
- DOM의 구조는 트리 형태를 가지면 노드와 객체로 문서를 표현하며, 이 정보를 이용하여 다양한 작업을 시도할 수 있다.
  - 모든 HTML의 요소 변경 가능
  - 모든 HTML의 속성 변경 가능
  - 모든 CSS 스타일 변경 가능
  - HTML 요소 및 속성 제거 또는 추가 가능
  - 페이지 내에 존재하는 모든 HTML 이벤트에 반응 가능
  - 새로운 HTML 이벤트 추가 가능

---

## DOM Element

- 자바스크립트에서 HTML 요소에 접근하는 방법
  - HTML 요소의 id 속성
  - HTML 요소의 class 속성
  - HTML 요소의 태그 명
  - CSS 선택자를 이용

### HTML 요소의 id 속성 활용

```html
~
<body>
  <div id="id-test">
    DOM id로 접근 테스트
  </div>
  <script>
    let divEl = document.getElementById('id-test');

    console.log(divEl);
    console.log(typeof divEl);
    console.dir(divEl);
  </script>
</body>
</html>
```

![image](https://user-images.githubusercontent.com/104971437/178679671-63481f17-938f-4e24-866e-3a174924cf81.png)

- document 객체의 메서드 중 `getElementById(id)`를 이용하여 요소를 참조한다.
  - document는 페이지 콘텐츠의 진입점 역할을 하는 객체
  - 브라우저가 불러오는 페이지에 접근하기 위한 객체이다.
  - 요소에 접근하거나 생성하는 등 문서 전반과 관련된 속성과 메서드들이 정의되어져 있다.
- HTML 에서 특정 요소에 정의한 id 속성을 위 메서드에 전달하여 참조한다.
  - HTML 요소가 발견되면 해당 요소를 **객체 형태**로 반환. 찾지 못할 경우엔 **null**을 반환한다.

> DOM을 통해 생성된 HTML 요소에 대한 정보가 객체 형태로 관리된다는 것이 중요. 해당 메서드를 통해 HTML 요소를 참조하여 DOM 관련 메서드를 이용하여 수정 등이 가능해지는 것.

### HTML 요소의 태그명 활용

```html
~
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  <script>
    const liEls = document.getElementsByTagName('li');

    console.log(liEls);
    console.log(liEls.item(0));
  </script>
~
```

- document의 메서드 중 `getElementByTagName(tagName)`을 이용하여 HTML 요소를 참조
- 해당되는 모든 요소를 **HTMLCollection**으로 반환하게 된다.
  - arguments와 같이 유사 배열 형태
  - 문서의 내용이 바뀔 때 실시간으로 업데이트 되는 컬렉션
  - WebKit에선 NodeList가 반환된다고 한다.

### HTML 요소의 class 활용

```html
~
  <ul>
      <li class="list-item">1</li>
      <li class="list-item">2</li>
      <li class="list-item">3</li>
      <li class="list-item">4</li>
      <li class="list-item">5</li>
  </ul>
  <script>
    const liEls = document.getElementsByClassName('list-item');

    console.log(liEls);
    console.log(liEls.item(0));
  </script>
~
```

- document의 메서드 중 `getElementByClassName(className)`을 이용하여 해당 클래스명을 갖고 있는 모든 요소를 참조한다.
- 클래스명과 일치하는 모든 요소를 **HTMLCollection**으로 반환

### CSS 선택자 활용

```html
~
  <ul>
    <li name="list-item1">1</li>
    <li name="list-item2 special">2</li>
    <li name="list-item3">3</li>
    <li name="list-item4 special">4</li>
    <li name="list-item5">5</li>
  </ul>
  <script>
    const liEls1 = document.querySelectorAll('[name*=list-item]');
    const liEls2 = document.querySelectorAll('[name^=list]');
    const liEls3 = document.querySelectorAll('[name~=special]');
    const liEl1 = document.querySelector('[name$=item3]');

    console.log(liEls1);
    console.log(liEls2);
    console.log(liEls3);
    
    console.log(liEl1);
  </script>
~
```

- document의 메서드 중 `querySelector(selector)`나 `querySelectorAll(selector)` 을 이용하여 HTML 요소를 참조하는 방법
  - `querySelector()`는 주어진 선택자를 만족하는 **첫 번째 요소를 반환**
  - `querySelectorAll()`는 주어진 선택자를 만족하는 모든 요소가 담긴 **NodeList를 반환**
- 사용하고자 하는 선택자 규칙을 그대로 전달한다. 
  - 태그 선택자
  - 클래스 선택자 (`.`표기)
  - id 선택자 (`#` 표기)
  - 복합 선택자 (2개 이상의 기본 선택자를 결합하여 사용)
    - 하위 선택자 (` ` 공백 표기)
    - 자식 선택자 (`>` 표기)
    - 인접 형제 선택자 (`+` 표기)
    - 일반 형제 선택자 (`~` 표기)
  - 속성 선택자(특정 속성이나 속성값을 활용하여 선택)
    - `[속성명]` : 해당 속성이 포함된 요소를 선택
    - `[속성명="속성값"]` : 해당 속성이 가지는 속성값과 정확히 일치하는 요소를 선택
    - `[속성명~="속성값"]` : 해당 속성에서 속성값이 포함되는 요소를 선택(공백으로 분리된 값이 일치)
    - `[속성명^="속성값"]` : 해당 속성값으로 시작하는 요소를 선택
    - `[속성명$="속성값"]` : 해당 속성값으로 끝나는 요소를 선택
    - `[속성명*="속성값"]` : 해당 속성값이 포함되는 요소를 선택
    - `[속성명|="속성값"]` : 해당 속성값을 정확하게 갖고 있거나 해당 속성값으로 시작하는 요소를 선택

> 속성 선택자만 헷갈려서 코드로 작성해보며 정리. 정규식 기호 사용과 매우 유사한 것이 많다.

---

## DOM Attribute

- DOM 요소가 가지는 속성을 가져오거나 수정할 수 있다.

### getAttribute('attributeName')

```html
~
  <div id="test">속성 정보 가져오기</div>

  <script>
    let divEl = document.getElementById('test');
    let divAttribute = divEl.getAttribute('id');

    console.log(divAttribute); // test
  </script>
~
```

- 해당 요소의 속성에 지정된 값을 반환
- 위 예제처럼 요소를 특정한 뒤 해당 요소에서 id라는 속성이 가지는 값을 가져올 수 있다.

### setAttribute(name, value)

```html
~
  <button id="test">속성 및 속성값 설정하기</button>

  <script>
    let btnEl = document.getElementById('test');

    btnEl.setAttribute('disabled', 'true');
  </script>
~
```

- 특정 요소의 속성의 값을 설정한다.
- 위 예제는 버튼 요소를 특정하고 setAttribute 메서드를 이용하여 disabled 속성을 적용하는 것으로 작성해보았다.

### hasAttribute(name)

```html
~
  <p id="test" style="color:red;">속성 확인하기</p>

  <script>
    let pEl = document.getElementById('test');
    
    console.log(pEl.hasAttribute('style')); // true
    console.log(pEl.hasAttribute('class')); // false
  </script>
~
```

- 특정 요소가 전달되는 이름과 일치하는 속성을 가지는 지 확인하는 메서드. boolean 값이 반환된다.

### removeAttribute(attrName)

```html
~
  <p id="test" style="color:red;">속성 확인하기</p>

  <script>
    let pEl = document.getElementById('test');
    
    console.log(pEl.hasAttribute('style')); // true
    pEl.removeAttribute('style');
    console.log(pEl.hasAttribute('style')); // false
    pEl.removeAttribute('class'); // 에러없이 동작한다.
  </script>
~
```

- 특정 요소가 가지는 속성을 제거할 때 사용한다.
- 제거하고자 하는 속성이 요소에 없더라도 아무런 에러가 발생하지 않는다.

---

## HTML 내용 변경

- 요소가 가지는 컨텐츠를 변경할 수 있다.
  - 컨텐츠는 요소가 가지는 내용으로 다른 HTML 요소나 텍스트일 수 있다.

### innerHTML

```html
~
  <p id="p1">innerHTML 확인</p>
  <p id="p2"><span>innerHTML 확인(span)</span></p>
  <p id="p3"></p>

  <script>
    let p1 = document.getElementById('p1');
    let p2 = document.getElementById('p2');
    let p3 = document.getElementById('p3');
    
    console.log(p1.innerHTML);
    console.log(p2.innerHTML);
    console.log(p3.innerHTML);

    p3.innerHTML = '<span style="color: red;">insert a span element</span>';  
  </script>
~
```

![image](https://user-images.githubusercontent.com/104971437/178862181-a23e5e13-b345-467e-a7ad-1905169f88fd.png)


- Element 가 가지는 속성으로 요소가 갖는 HTML 요소 내용을 문자열 형태로 가지고 있다.
- 단순히 속성을 참조하게 되면 특정 요소가 가지는 내부 요소를 문자열로 반환한다.
- 해당 속성에 HTML 구문으로 된 문자열을 할당하면 내부 요소로 삽입하게 된다.

### innerText

- 요소가 갖는 텍스트 컨텐츠를 포함하고 있는 속성
- 아래 MDN 예제 코드를 분석하여 정리하고자 한다.(Node.textContent 속성과 비교)

```html
~
  <h3>원본 요소:</h3>

  <p id="source">
    <style>#source { color: red; }</style>
  아래에서<br>이 글을<br>어떻게 인식하는지 살펴보세요.
    <span style="display:none">숨겨진 글</span>
  </p>

  <h3>textContent 결과:</h3>
  <textarea id="textContentOutput" rows="6" cols="30" readonly>...</textarea>

  <h3>innerText 결과:</h3>
  <textarea id="innerTextOutput" rows="6" cols="30" readonly>...</textarea>

  <script>
    const source = document.getElementById('source');
    const textContentOutput = document.getElementById('textContentOutput');
    const innerTextOutput = document.getElementById('innerTextOutput');

    textContentOutput.innerHTML = source.textContent;
    innerTextOutput.innerHTML = source.innerText;
  </script>
~
```

![image](https://user-images.githubusercontent.com/104971437/178864151-b23db33c-922a-4e87-9627-33bf72816e07.png)

- 원본 요소 \#source 의 innerText와 textContent의 결과를 비교하는 예제
  - source 에는 여러 내부 요소와 텍스트가 혼합되어 있다. (style{color:red}, span{display:none})
- 원본 요소를 textContent와 innerText로 각각 추출한 뒤 출력 요소에서 결과를 비교
  - textContent 결과
    - style, br, span 태그 등이 요소로써 렌더링되지 않고 오직 텍스트로만 결과를 출력하는 것을 확인할 수 있다.
  - innerText 결과
    - br과 span이 요소로서 반영되어 텍스트가 렌더링 되는 것을 확인할 수 있다.
- 정리
  - innerText는 특정 요소에 텍스트 콘텐츠를 삽입할 수 있는데, 만약 텍스트 내용 중 일부가 요소로써 특정될 수 있다면(사람이 읽을 수 있는) 이를 반영하여 렌더링한다. (이는 브라우저가 처리하는 작업으로 리플로우라고 하며 렌더링 시 추가계산 작업 등이 발생하기 때문에 textContent 보다 성능이 떨어질 수 있다고 설명하고 있다)
  - textContent는 style, script 요소가 가지는 텍스트 콘텐츠도 포함된다. 상황별로 가질 수 있는 값이 다를 수 있음을 유의할 것.([MDN 참고](https://developer.mozilla.org/ko/docs/Web/API/Node/textContent#%EC%84%A4%EB%AA%85))

### insertAdjacentHTML()

```html
~
  <ul id="number-list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>

  <script>
    let ulEl = document.getElementById('number-list');

    ulEl.insertAdjacentHTML('beforebegin', '<h3 style="color: tomato;">Start!!</h3>');
    ulEl.insertAdjacentHTML('afterbegin', '<li style="color: skyblue;">0</li>');
    ulEl.insertAdjacentHTML('beforeend', '<li style="color: royalblue;">6</li>');
    ulEl.insertAdjacentHTML('afterend', '<h3 style="color: purple;">End...</h3>');
  </script>
~
```


- 특정 요소에 위치 기준을 두어 요소를 삽입하는 메서드이다.
- `insertAdjacentHTML(position, text)`와 같이 2개의 인자를 받는다.
  - position에는 아래의 특정 키워드만 전달 가능
    - `beforebegin` : 시작 전 - 요소의 앞에
    - `afterbegin` : 시작 후 - 요소 안 가장 첫번째 자식으로
    - `beforeend` : 종료 전 - 요소 안 맨 마지막 자식으로
    - `afterend` : 종료 후 - 요소의 뒤에
- innerHTML의 경우 요소의 자식 노드가 전부 바뀌어 버린다는 문제가 있는데, 위 메서드를 활용하면 원하는 위치에 요소를 추가할 수 있다는 장점이 있다. 또한 처리 작업에 있어 이미 존재하는 요소는 건드리지 않기 때문에 작업이 더 빠르다고 한다.

### insertAdjacentText()

```html
~
  <p id="test">
    Lorem ipsum dolor sit amet consectetur adipisicing elit.
  </p>

  <script>
    let pEl = document.getElementById('test');

    pEl.insertAdjacentText('beforebegin', 'P 요소 전 텍스트 추가');
    pEl.insertAdjacentText('afterbegin', 'P 요소 안 맨 앞에 텍스트 추가');
    pEl.insertAdjacentText('beforeend', 'P 요소 안 맨 마지막에 텍스트 추가');
    pEl.insertAdjacentText('afterend', 'P 요소 다음 텍스트 추가');
  </script>
~
```

![image](https://user-images.githubusercontent.com/104971437/178882892-ba90ed47-3524-4067-9026-54e85dfdaa84.png)

- insertAdjacentHTML와 비슷하지만 텍스트를 삽입한다.
- 전달인자도 position, textString 으로 유사. position 값은 앞 서 정리한 키워드값 그대로 사용한다.

### remove()

- 특정 HTML 요소를 삭제할 때 사용하는 메서드

---

**참고 자료**

- [위키백과 - 문서 객체 모델](https://ko.wikipedia.org/wiki/%EB%AC%B8%EC%84%9C_%EA%B0%9D%EC%B2%B4_%EB%AA%A8%EB%8D%B8)
- [MDN - DOM 소개](https://developer.mozilla.org/ko/docs/Web/API/Document_Object_Model/Introduction)