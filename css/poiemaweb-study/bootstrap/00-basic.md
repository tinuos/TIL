# Bootstrap

- 프론트엔드 툴깃 중 하나인 부트스트랩에 대한 기본 개념 학습

---

## 부트스트랩


- 반응형 사이트를 위한 프론트엔드 프레임워크
- 트위터 개발자가 개발한 오픈소스
- 현재(22.6) 5버전까지 출시

### 소개글

Build fast, responsive sites with Bootstrap

Powerful, extensible, and feature-packed frontend toolkit. Build and customize with Sass, utilize prebuilt grid system and components, and bring projects to life with powerful JavaScript plugins.

- 부트스트랩 홈페이지 소개글
- 특징
  - Sass로 개발하거나 커스터마이징이 가능
  - 그리드 시스템, 컴포넌트 기능을 이용하여 사전에 구조적인 작업(?)이 가능
  - 자바스크립트 플러그인 사용 가능
- HTML, CSS, JS로 이미 구성되어 있는 기능을 적절히 사용하거나 커스터마이징하여 활용(프레임워크)

### 특징

#### 코드의 재사용 (Code reuse)

```html
<div class="alert alert-primary" role="alert">
  A simple primary alert—check it out!
</div>
<div class="alert alert-secondary" role="alert">
  A simple secondary alert—check it out!
</div>
<div class="alert alert-success" role="alert">
  A simple success alert—check it out!
</div>
<div class="alert alert-danger" role="alert">
  A simple danger alert—check it out!
</div>
<div class="alert alert-warning" role="alert">
  A simple warning alert—check it out!
</div>
<div class="alert alert-info" role="alert">
  A simple info alert—check it out!
</div>
<div class="alert alert-light" role="alert">
  A simple light alert—check it out!
</div>
<div class="alert alert-dark" role="alert">
  A simple dark alert—check it out!
</div>
```

- 여러가지 스타일을 클래스로 만들어 클래스명을 사용하는 것만으로도 적용되도록 만들어져 있다.
- 위 예제 코드는 부트스트랩에서 제공하는 Alerts 컴포넌트의 기본 예로 alert라는 기본 컴포넌트를 클래스로 등록하고 적용하고 싶은 색깔의 alert를 관련 클래스명으로 사용할 수 있다.
- 이러한 코드의 재사용성은 빠르게 개발이 가능하고 일관된 스타일의 코드 작성이 가능하다는 장점이 있다.

#### 프레임워크 개념과 특징

- Framewordk의 사전적 의미
  - 뼈대
  - 체계
  - 틀
- 소프트웨어에서 프레임워크
  - 소프트웨어 개발시 공통적으로 필요한 기능들을 재사용 관점에서 모아 구조화한 것.
  - 특정 환경에서 공통적으로 사용될만 한 것들을 미리 기본적으로 구축해 놓은 뒤 필요한 기능들은 프레임워크에서 제공하는 코드들을 이용해 추가해 나가는 것.
- Snippet
  - 정형화된, 자주 사용하는 코드 묶음 정도를 의미(재사용 가능한 소스코드)
  - 웹 디자인에서는 스니펫이 자주 사용된다고 한다. 이러한 스니펫이 사내에서 관리되지 않고 개별적으로 사용하게 되면 유지보수 등의 어려움이 발생할 수 있는데, 라이브러리나 프레임워크가 제공하는 코딩 스타일로 통일시키게 되면 이러한 문제를 어느 정도 해결 가능하다고 설명하고 있다. 대규모 회사나 팀 같은 경우 자체 서비스나 기능의 성능 향상 등의 이유로 프레임워크나 라이브러리를 독자적으로 개발하여 사용하는 경우도 있다고 함. 소규모일 경우에는 아무래도 비용적인 측면에서 어려움이 많기 때문에 부트스트랩과 같이 공식적으로 검증되고 사용자가 많은 프레임워크를 활용하는 형태로 진행.

#### 부트스트랩 장점

- 사용하기 쉽다.
  - 기본적인 HTML, CSS, JS에 대한 지식만 있다면 쉽게 적용 가능
- 반응형 디자인
  - 기본적으로 반응형 디자인을 제공
- 모바일 우선 접근
  - 3버전부터 모바일 우선 적용 스타일을 지원한다고 한다.
- 브라우저 호환
  - 대부분의 브라우저에 지원된다.

> poiemaweb 에서는 부트스트랩 3버전 기준으로 기본 내용이 작성되어져 있다.(현재 5버전) 5버전에서는 jquery 탈피(순수 바닐라 JS 적용), IE 미지원 등의 특징적인 변화가 있다는 것을 이해하고 사용할 필요가 있다.

## 부트스트랩 설치

- 부트스트랩을 사용하기 위해서는 다운로드를 해야 한다.
- 공식문서에서는 여러가지 설치 방법을 알려주는데 다음에 나온 것만 정리해본다.
  - Compiled CSS and JS
  - CDN via jsDelivr
  - Package managers

### Compiled CSS and JS

- 부트스트랩 동작을 위해 필요한 CSS와 JS 파일을 로컬에 다운받아 사용하는 방식이다.
- 해당 파일들을 다운받은 후 개발하고자 하는 프로젝트 안에 포함시켜 적용한다.

### CDN via jsDelivr

- 콘텐츠 전송 네트워크를 통해 사용
- CDN 서버로부터 부트스트랩 관련 CSS, JS 파일을 참조하여 사용.
  - HTML에 link와 script 요소를 이용하여 간단히 추가하여 사용한다.
- jsDelivr은 오픈 소스를 위한 무료 CDN

### Package managers

- 여기선 npm 에 대하여만 간단히 정리

#### npm

- npm을 알기 이전에 NodeJS를 알아야 한다.
- NodeJS는 웹브라우저에서만 사용하던 자바스크립트를 로컬이나 다른 환경에서도 실행 가능하게 만들어 주는 런타임 환경을 의미. 즉, 일반 로컬 환경에서도 자바스크립트를 사용할 수 있게 해준다.
- npm은 Node package manager의 약자로 자바스크립트(nodejs)로 작성된 프로젝트를 패키지화 하여 관리하는 패키지 관리자를 말한다. npm을 이용하면 node로 작성된 라이브러리나 프레임워크 등을 로컬에 손쉽게 다운로드 하여 사용 가능하다.

> 아직  자바스크립트에 대한 내용을 깊게 다루어 보지 않아 일단 npm 을 이용하여 쉽게 부트스트랩과 같은 라이브러리나 프레임워크 등을 설치할 수 있다는 정도로만 이해하고 넘어간다.



---

**참고 자료**

- [poiemaweb](https://poiemaweb.com/bootstrap-basics)
- [Bootstrap](https://getbootstrap.com/)