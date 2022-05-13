# HTML - 비디오와 오디오 컨텐츠

HTML 문서 내에 비디오, 오디오 컨텐츠 포함 및 캡션

---

## HTML5 이전에 비디오 또는 오디오 콘텐츠 삽입 방법

- HTML5 이전 버전에서는 따로 비디오와 오디오 콘텐츠를 위한 표준이나 기술이 존재하지 않았다.
  - [플러그인](https://ko.wikipedia.org/wiki/%ED%94%8C%EB%9F%AC%EA%B7%B8%EC%9D%B8) 기술(flash 등)을 이용하여 삽입

> 플러그인을 통해 영상이나 음성 콘텐츠를 제공할 수 있었고 한동안 유행했지만, HTML이나 CSS 특성을 잘 활용할 수 없는 문제와 더불어 보안, 웹 접근성 등의 문제들이 발생했다.

### HTML5 표준을 이용하여 적용

- HTML5 에서 비디오나 오디오 콘텐츠를 위한 표준 명세 발표
- 이와 더불어 이러한 요소들을 제어할 수 있는 JavaScript API 도 탑재되었다.

---

## 비디오 및 오디오 삽입

### video, audio 요소

- img 요소를 사용하는 것과 거의 비슷하다.
- `src` 속성을 통해 영상이 존재하는 경로를 작성
- `controls` 속성
  - 불속성으로 표기 시 영상 컨트롤러를 표시할 수 있다.
  - 기본적으로 브라우저 자체의 컨트롤러 인터페이스가 표시된다. (시작이나 정지, 볼륨 등의 최소한의 컨트롤 기능)
  - JavScript API를 통해 인터페이스 커스텀이 가능
  - 재생이나 볼륨 등과 관련된 특성들이 존재(아래에서 따로 정리)

#### p요소를 이용한 fallback content 처리

```html
<video src="rabbit320.webm" controls>
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.webm">link to the video</a> instead.</p> 
</video>
```

- 페이지에 접근하는 브라우저(사용자측)가 video 요소를 제대로 지원하지 못할 경우에 대한 대비책 관련 코드 예제
- 영상이 있는 실제 링크를 포함시킴으로써 사용자가 브라우저가 아니더라도 다른 방법을 통해 접근할 수 있도록 부가적으로 제공한다. 

> p 요소 내 텍스트들은 화면상에서 볼 수 없지만 개발자도구를 통해 보면 HTML 문서 내에서 video 요소 내부에 포함되어 있는 것을 확인할 수 있다. (MDN에서 말하는 다른 방법을 통한 접근의 예로 웹 크롤링이나 HTTP을 통한 데이터 응답 확인 등의 작업을 생각해볼 수 있지 않을까?)

---

## 호환성 처리하기

- 인터넷 익스플로러와 같이 video나 audio 요소들을 지원하지 않는 구형 브라우저들을 위해 호환을 해주어야 한다.

### 미디어 파일의 content

- 일단 제일 먼저 비디오나 오디오가 어떤 형식의 [컨테이너 포맷](https://developer.mozilla.org/ko/docs/Web/Media/Formats/Containers)을 따르는 지 알아야 한다.
- 컨테이너 포맷이란 파일 타입을 말하는 것으로 어떠한 파일이 가지는 특정한 형태(포맷)을 말한다.
  - MP3, Ogg, WebM, MPEG-4(MP4) 등
- 이러한 포맷에 따라 코덱(인코딩이나 디코딩 또는 둘 다)을 달리하여 영상이나 음성 등 데이터들을 처리해야 한다.
- 브라우저마다 지원하는 파일 포맷이 다를 수 있어 이를 체크해야 한다. - [관련 MDN 문서](https://developer.mozilla.org/ko/docs/Web/Media/Formats/Containers#%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80_%ED%98%B8%ED%99%98%EC%84%B1)

### source 요소 사용하여 적용하기

```html
<video controls>
  <source src="rabbit320.mp4" type="video/mp4">
  <source src="rabbit320.webm" type="video/webm">
  <p>Your browser doesn't support HTML5 video. Here is a <a href="rabbit320.mp4">link to the video</a> instead.</p>
</video>
```

- `source` 요소는 이미지나 비디오 자원의 위치를 명세하기 위한 요소이며 빈요소이다.
- `src`속성을 이용하여 경로를 작성하고, `type`을 이용해 파일 타입을 명시할 수 있다.
- source 사용은 선택적이나 브라우저의 호환성을 위해 추가하는 것을 권장
  - type은 [MIME type](https://developer.mozilla.org/ko/docs/Glossary/MIME_type)으로 명시 

> 브라우저 호환성을 위해 여러 형식의 콘텐츠와 포맷을 source를 통해 제공하면 브라우저가 자신이 실행할 수 있는 파일을 찾아 로드하여 동작하는 방식이라고 한다. - 포맷 타입으로 구분하기 때문에 브라우저가 사용할 수 없는 콘텐츠의 경우 스킵이 되어 효율적이라고도 설명하고 있다.

---

## video나 audio 요소의 특징

### 재생, 소리, 로드 관련 특성

- img 요소처럼 width나 height로 크기 설정이 가능하다.
- 콘텐츠 특성상 재생이나 소리 등이 중요하기 떄문에 관련 특성이 따로 존재하며, 파일의 크기가 일반적으로 크기 때문에 preload 라는 특성도 확인할 수 있다.
  - autoplay
  - loop
  - muted
  - poster (only video element)
  - preload

> audio 요소는 poster라는 속성만 제외하고는 video와 거의 유사하기 때문에 같이 정리

### 미디어 로드 재설정

- source 요소를 통해 미디어 콘텐츠를 지정했을 때 이를 JS로 다시 선택하여 `load()` 메서드를 이용하여 미디어 시작 설정을 초기화할 수 있다. 

### 트랙 추가와 삭제 감지

- 미디어 콘텐츠를 선택하여 JavaScript로 AudioTrackList 객체를 통해 처리 가능

> 이 부분에 대한 내용은 이해가 잘 되지 않아서 JS를 학습하고 트랙 관련 처리를 해야될 때 다시 한번 정리해봐야 겠다.

---

## 텍스트 트랙 삽입하기

```html
<video controls>
  <source src="example.mp4" type="video/mp4">
  <source src="example.webm" type="video/webm">
  <track kind="subtitles" src="subtitles_en.vtt" srclang="en">
</video>
```

- audio나 video 요소의 자식으로 `track` 요소를 사용하여 시간별로 자막을 삽입할 수 있다.
  - `src` 속성을 이용하여 vtt나 ttml 형식의 텍스트 트랙 파일을 적용 
  - `kind` 속성을 이용하여 해당 텍스트의 종류를 설정 가능
    - subtitles (속성 미사용시의 기본값)
    - captions
    - descriptions
    - chapters
    - metadata
  - `default` 속성을 이용하여 활성화할 기본 트랙을 설정 - 하나의 미디어 요소 당 하나의 트랙 요소에만 사용

> video caption maker 등을 이용하여 영상이나 음성 파일 등을 재생하며 vtt 파일을 간단히 생성할 수 있다. - [HTML5 Video Caption Maker](https://testdrive-archive.azurewebsites.net/Graphics/CaptionMaker/Default.html)

---
---

**참고 자료**

- [MDN | 비디오 그리고 오디오 컨텐츠](https://developer.mozilla.org/ko/docs/Learn/HTML/Multimedia_and_embedding/Video_and_audio_content)