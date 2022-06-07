# CSS - 웹 폰트

- 웹 페이지에 폰트를 적용하는 방법에 대하여 학습

---

## 웹 폰트(Web font)

- 웹 페이지 - 불특정 사용자에게 제공
  - 여러가지의 OS 사용 등 로컬 환경이 일정하지 않다.
  - 웹 브라우저는 로컬에 있는 소프트웨어로 폰트 사용시 로컬에 설치되어 있는 폰트 리소스를 사용
- 웹 폰트는 로컬에 설치되어 있지 않는 폰트를 웹페이지에서 요구할 때 사용하는 방식
  - HTML, CSS, JS 파일과 같이 서버에서 클라이언트로 폰트가 전송된다.

### CDN

- Content Delivery Network
- [콘텐츠 전송 네트워크](https://ko.wikipedia.org/wiki/%EC%BD%98%ED%85%90%EC%B8%A0_%EC%A0%84%EC%86%A1_%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC)를 이용하는 것. 사용자에게 콘텐츠를 전달하기 위해 제공되는 시스템을 말한다. 웹에서 필요로 하는 리소스뿐만 아니라 미디어, 소프트웨어, 문서, 애플리케이션, 스트리밍 등 다양한 요소들을 CDN으로 제공할 수 있다. 보통 서비스 회사 자신들의 콘텐츠를 CDN 회사에 사용료를 지불하고 제공하는 방식이라고 한다.
- 웹 폰트에선 대표적으로 구글 폰트가 있다.
- 웹 폰트 제공 업체마다 다를 수 있지만 HTML의 링크 요소나 CSS의 @import 규칙 등을 이용하여 간단한 사용방식을 알려준다.

### 서버 폰트 로딩 방식

```css
/* MDN 예제 */
@font-face {
  font-family: 'zantrokeregular';
  src: url('zantroke-webfont.woff2') format('woff2'),
       url('zantroke-webfont.woff') format('woff');
  font-weight: normal;
  font-style: normal;
}
```

- 웹페이지에 적용되는 폰트를 서버에 두고, `@font-face`로 적용될 폰트를 상세히 설정하는 방법
  - CDN 방식의 단점을 보완할 수 있다.
    - 제공되지 않는 폰트이거나 서비스 제공에 오류가 있을 경우
- 이 방식의 경우 브라우저마다 지원되는 폰트 파일 형식이 다를 수 있다는 문제가 있다. (아래 poiemaweb 참고 문서 확인)
- `@font-face` 규칙으로 폰트를 등록하고 `font-family` 속성으로 폰트를 선택하여 사용한다.

## 추가 내용

- 영문, 한문 폰트 혼용 시 영문 폰트 우선 지정

---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/css3-webfont)
- [MDN - Web fonts](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)